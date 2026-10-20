---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/bootloader_ota/bk_ota_nosecure.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ab"></a>

# 非安全非 AB 升级方案

<a id="id1"></a>

## 原理

`projects/app` 等非安全工程使用传统 **download \+ up\_bootloader 覆盖** 模型：AP 把
`.rbl` 升级包写入 ``` ota``（历史名 download）分区；复位后 up_bootloader 发现该区非
``0xFFFFFFFF ```，校验 magic/CRC，再解压、解密、搬运到 `primary_cp_app` /
`primary_ap_app` 执行区，擦除 download 后跳转应用。

没有第二执行槽，也没有试跑/回滚。搬运过程中掉电可能导致执行区损坏，需重烧。

<a id="id2"></a>

## 参考工程与开关

- 工程：`projects/app`
- 编译：`make bk7259 PROJECT=app`
- `CONFIG_OTA_HTTP=y`，**不要** 打开 `CONFIG_HTTP_AB_PARTITION` /
  `CONFIG_SECURE_OTA_*`
- 后端：`ota_base_drv.c` 的默认 ``` s_ota_fun``（``finish == NULL ```）
- 产物：`build/bk7259/app/package/app_pack.rbl`
- CLI：`ap_cmd http_ota http://<host>/.../app_pack.rbl`

<a id="flash-8mb"></a>

## Flash 布局（8MB 参考表）

```
primary_bootloader     64K     l_bootloader + up_bootloader
primary_cp_app         1900K   CP 执行区
primary_ap_app         1156K   AP 执行区
ota                    1900K   下载暂存（须能放下 .rbl）
usr_config / easyflash / sys_rf / sys_net
```

`ota` 分区不需要时也可保留 4K 占位，但不能再做 OTA。

<a id="struct-ota-rbl-head"></a>

## 升级包 `struct ota_rbl_head`

RBL 头位于包内偏移 ``` 0x1000``（``RBL_HEAD_POS ```），定义在 `bk_ota_private.h`：

| 字段 | 含义 |
| --- | --- |
| `magic[4]` | RBL 魔数 |
| `algo` | 低 8bit 加密（NONE/XOR/AES256），高 8bit 压缩（GZIP/QuickLZ） |
| `timestamp` / `name` / `version` / `sn` | 包元数据 |
| `crc32` | `crc32(aes(zip(bin)))` |
| `hash` | 原始 bin 的 FNV hash（`RT_OTA_HASH_FNV_SEED=0x811C9DC5`） |
| `size_raw` | 原始固件长度 |
| `size_package` | 压缩加密后长度 |
| `info_crc32` | 头自身 CRC（不含本字段） |

<a id="id3"></a>

## 端到端全流程

`system_startup()` 在非 AB 工程走 ``` ota_main()``（探测 RBL 全量包或差分包），然后
``jump_to_app() ```。下面以全量 RBL（`ota_full_handler`）为主。

HTTP 下载期间关闭 STA PS，避免 MAC 定时中断被丢掉导致卡住。

```
[AP 运行中] http_ota url (.rbl)
     |
     ota_do_init(): pt = BK_PARTITION_OTA
     wr_address = ota 分区起点
     +-- init 失败 --> ota_fail，不重启
     v
HTTP 流写入 ota 分区
     1KB 缓冲，扇区边界 erase（可等 BLE 共存窗口）
     write + 回读，失败置 wr_err，后续包直接失败
     +-- HTTP/写 Flash 失败 --> ota_fail，不重启
     |                         download 可能半包；下次启动若 magic
     |                         不像 RBL 则跳过安装
     v
收齐 image_size，flush 尾包
     finish==NULL --> deinit + reboot
     |
------------------ 复位 ----------------
     |
bootrom -> 64KB bootloader
     |
ota_full_probe(download)
     +-- 分区空 (全 0xFF) ----------> 跳当前 app
     +-- 头 4 字节不是 "RBL\\0" -----> 跳当前 app
     v
ota_full_execute()
     校验 RBL 头 info_crc32 + 包体 CRC32
     +-- 失败 --> 作废头 4K + 尾 4K，跳旧 app
     |            (防止半包与下次下载拼成「合法」镜像)
     v
按 rbl_hdr.name 找目的分区 (application 等)
     +-- 找不到 --> 同样作废镜像，跳旧 app
     v
擦目的分区，按 algo 解压 (zlib) / 解密 (NONE/XOR/AES256)
     搬运到 app 执行区
     +-- 搬运中掉电 --> 执行区可能损坏，无 journal，通常需重烧
     v
成功则 download 区失效，jump_to_app 进新固件
     失败则 reboot 再走 ota_main 重试
```

与安全 Overwrite 的对比：安装者是 up\_bootloader 而不是 BL2；包格式是 RBL 而不是
BK723658 头；没有 ota\_control confirm/journal，也没有 EC-P256 和试跑回滚。
