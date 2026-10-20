---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/bootloader_ota/bk_ota_secure_overwrite.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="overwrite"></a>

# 安全 Overwrite 升级方案

<a id="id1"></a>

## 原理

`secureboot_overwrite` 只有一个可执行槽 ``` primary_all``（由 ``primary_tfm_s ``` \+
`primary_cpu0_app` \+ `primary_ap_app` 打包签名而成）。OTA 时 AP 把压缩且经 BL2
签名的镜像原样写入 `ota` 暂存区，再在 `ota_control` 末尾写入确认记录。复位后
BL2 按 MCUboot `OVERWRITE_ONLY` 策略：把 `ota` LZMA 解压覆盖到 `primary_all`，
再做 EC-P256 验签。v1 **不做** 主机侧加密；若 eFuse 打开了 Flash AES，BL2 写
`primary_all` 走 CBUS，由硬件 XTS-AES 加密。

特点：

- 节省 Flash：无需双份应用槽，但 `ota` 暂存区要能放下压缩包（参考工程 3072KB）。
- 安装窗口内掉电：靠 `ota_control` 首扇区 journal 按 64KB 块续传。
- 无 A/B 回滚：新镜像一旦覆盖成功并验签通过即成为唯一可执行镜像。

<a id="id2"></a>

## 参考工程与开关

- 工程：``` projects/secureboot_overwrite``（及 ``secureboot_overwrite_no_en ```）
- 编译：`make bk7259 PROJECT=secureboot_overwrite`
- AP：`CONFIG_SECURE_OTA_OVERWRITE=y`
- BL2：`CONFIG_OTA_OVERWRITE` / `CONFIG_OTA_CONFIRM_UPDATE`
- 产物：`build/bk7259/secureboot_overwrite/package/ota.bin`
- CLI：`ap_cmd http_ota http://<host>/.../ota.bin`

<a id="flash-8mb"></a>

## Flash 布局（8MB 参考表）

```
0x000000  bl1_control / boot_flag / partition / primary_manifest
0x004000  bl2                         96K
0x01C000  sys_its / sys_ps
0x020000  primary_tfm_s               320K   ─┐
0x070000  primary_cpu0_app            1644K   ├─ 虚拟 primary_all（BL2 签名一次）
0x20B000  primary_ap_app              1428K  ─┘  结束地址 64K 对齐
0x370000  ota                         3072K     AP 暂存压缩签名包
0x670000  ota_control                 8K        [0] journal  [末尾] confirm
...
0x7FE000  sys_rf / sys_net
```

`ota_control` 8KB \= 两个 4KB 扇区：

- 首扇区：掉电续传 journal（resume\_block\_t，35 字节/条，CRC8）
- 末扇区末 12 字节：ota\_confirm\_rec（安装请求）

<a id="ota-bin"></a>

## 升级包 ota.bin

打包器 `partition.py` 的 `gen_ota_bin_for_overwrite()`：把 `ota_signed.bin`
（压缩 \+ BL2 签名）加上 64 字节头（`image_num==1`）。

全局头 32 字节（LE，magic `"BK723658"`）：

| 偏移 | 类型 | 字段 |
| --- | --- | --- |
| 0 | 8 bytes | magic \= BK723658 |
| 8 | u32 | crc：对偏移 12 起至头结束（含 image header）做 CheckSumUtils CRC32 |
| 12 | u32 | version（打包器里的 global security counter，当前写 0） |
| 16 | u16 | `header_len` |
| 18 | u16 | `image_num`，Overwrite 必须为 1 |
| 20 | u32 | `flags` |
| 24 | u32\[2\] | `reserved` |

Image 头 32 字节：

| 偏移 | 类型 | 字段 |
| --- | --- | --- |
| 0 | u32 | `image_len`：payload 字节数，须 `<= ota` 分区大小 |
| 4 | u32 | `image_offset` |
| 8 | u32 | ``` flash_offset``（``ota ``` 分区偏移） |
| 12 | u32 | checksum：payload 的 CheckSumUtils CRC32 |
| 16 | u32 | version（security counter） |
| 20 | u32 | `flags` |
| 24 | u32\[2\] | `reserved` |

随后是 payload：`ota_signed.bin` 原样内容。AP **不解析** LZMA/签名，只做头 CRC \+ payload CRC，
按字节写入 `ota` 分区。

<a id="ota-confirm-rec"></a>

## 确认记录 `ota_confirm_rec`

AP `finish()` 与 BL2 `ota_confirm.c` 必须字节一致：

```
#define OTA_CONFIRM_REC_MAGIC  0x4F544143u   /* 'OTAC' */
#define OVERWRITE_CONFIRM      0xa16d8fb0    /* 由 _ota.h 生成 */

struct ota_confirm_rec {
    uint32_t magic;     /* OTA_CONFIRM_REC_MAGIC */
    uint32_t confirm;   /* OVERWRITE_CONFIRM 表示请求安装 */
    uint32_t crc;       /* CRC32({magic, confirm})，无最终取反 */
};
```

物理地址：`ota_control_base + ota_control_size - sizeof(record)`。
擦除扇区 → 写入 → 回读校验，最多 3 次。写入前先擦除 journal 首扇区，避免上次安装的
resume 记录让 BL2 误续传。

<a id="journal-resume-block-t"></a>

## Journal `resume_block_t`

BL2 `decompress_bl2.c`：

```
typedef struct {
    uint8_t index;       /* 已提交的 64KB 块号；0xFF 表示空 */
    uint8_t data[33];    /* BK7259 无 CRC 交织，保留布局 */
    uint8_t crc8;
} resume_block_t;
```

每成功写入一块 64KB 明文（或经 CBUS 加密后的密文）就追加一条 journal。
下次上电若 confirm 仍在，从 `index+1` 继续，避免整槽重装。

<a id="id3"></a>

## 端到端全流程

`secure_ow_state_t` 阶段：HEADER → PAYLOAD → DONE / ERROR。
下面把 AP 下载、BL2 安装、TF-M 确认画在一张图里，失败与掉电走右侧。

```
[AP 运行中] http_ota url
     |
     +-- 无 ota/ota_control 分区 / malloc 失败 --> ota_fail，不重启
     v
PHASE_HEADER 凑齐 64B
     +-- magic 不是 BK723658 ----+
     +-- 全局头 CRC 失败 --------+
     +-- image_num != 1 ---------+--> PHASE_ERROR，ota_fail，不重启
     +-- image_len 超 ota 槽 ----+     (confirm 未写，旧镜像仍可引导)
     v
PHASE_PAYLOAD 边收边写 ota[]
     扇区边界 erase + write + 回读 + 流式 CRC32
     +-- erase/write/回读失败 ------> PHASE_ERROR，ota_fail，不重启
     +-- 下载中复位 ----------------> confirm 未写，下次仍跑旧 primary_all
     v
收齐 payload，flush 尾包
     +-- payload CRC != checksum ---> PHASE_ERROR，ota_fail，不重启
     v
PHASE_DONE
     |
finish(): 先擦 journal 首扇区（必须空白）
          再写 {OTAC, OVERWRITE_CONFIRM, crc}，最多 3 次回读
     +-- journal 擦不干净 / confirm 写失败
     |     --> secure finalize failed，不重启
     v
reboot  ---------------------------------------------------------
     |
BootROM 验 BL2
     +-- BL2 验签失败 --> 无法启动
     v
BL2 读 ota_control 末尾 confirm
     +-- magic/crc 无效，或 confirm 不是 OVERWRITE_CONFIRM
     |     --> [ERR] no valid ota confirm record
     |         Swap type: none，引导现有 primary_all
     v
boot_copy_region()
     读 journal 得到已提交块号（无记录则从 0）
     每 64KB: LZMA 解压 -> 写 primary_all
              (Flash AES 开: CBUS；关: DBUS)
              写成功则追加 journal
     +-- 解压中掉电 --> 下次仍读到 confirm，从 index+1 续传
     v
EC-P256 验签 primary_all
     +-- 失败 --> 不跳转（执行区可能已部分覆盖，需重烧
     |            或仍保留 ota 包再复位重试）
     v
跳 TF-M
     |
TF-M: bk_ota_confirm_clear_if_armed()
     擦 journal + confirm，避免下次再装一遍
     |
进入 NS 应用（新固件）
```

日志对照（AP 侧）：

- `secure overwrite: stage ota @0x370000 size 0x300000`
- `secure overwrite hdr: img_len=... crc=...`
- `secure overwrite: staged n%`
- `secure overwrite: payload verified`
- `secure overwrite: armed OVERWRITE_CONFIRM @0x..., reboot to install`

BL2 侧若尚未确认安装：

- `[ERR] no valid ota confirm record (magic=0xffffffff)`
- `[FCE] Swap type: none`

这表示本次复位 **没有** 待安装请求（下载未完成、finish 未写入、或上次 TF-M 已清掉 confirm），
属于正常冷启动路径，不是升级成功。

<a id="id4"></a>

## 掉电与安全边界

- 下载中复位：`ota` 里是半包，confirm 未写，BL2 忽略，仍跑旧 `primary_all`。
- 已 arm confirm、解压中掉电：journal 记录已提交块，下次从下一 64KB 继续。
- TF-M 起来之后才清 confirm：防止“解压完但安全世界没起来”时丢失安装意图。
- AP 用数据总线写 `ota` / `ota_control`，不受 MPC 拦截；验签只在 BL2。
