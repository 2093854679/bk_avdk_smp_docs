---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/bootloader_ota/bk_ota_secure_xip.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="direct-xip-a-b"></a>

# 安全 Direct-XIP A/B 升级方案

<a id="id1"></a>

## 原理

`secureboot_xip` 使用两个等长、连续的可执行槽（虚拟 primary\_all / secondary\_all）。
当前槽通过 Flash XIP remap 寄存器 bit0 选择（0\=A/primary，1\=B/secondary），CPU 始终从同一逻辑地址取指。
OTA 把签名镜像写入对侧空闲槽，再在 boot\_param 写入 TRIAL 记录。
复位后 BL2 按记录选择槽位，对目标槽做 EC-P256 验签；通过则 remap 到新槽直接执行（不搬运）。
TF-M 起来后把 TRIAL 提交为 NORMAL。试跑超过 try\_max（默认 5，最大 7）仍未确认则回滚到旧槽。

与 Overwrite 的差异：Flash 占用约为双份应用，但安装时不覆盖正在运行的槽，失败可回滚。

<a id="id2"></a>

## 参考工程与开关

- 工程：`projects/secureboot_xip`
- 编译：`make bk7259 PROJECT=secureboot_xip`
- AP：`CONFIG_SECURE_OTA_XIP=y`
- BL2/TF-M：`CONFIG_DIRECT_XIP`
- 产物：`build/bk7259/secureboot_xip/package/ota.bin`
- 查询当前槽：ab\_version（读 remap bit0）

<a id="flash-8mb"></a>

## Flash 布局（8MB 参考表）

```
0x000000  bl1_control / boot_flag / partition / primary_manifest
0x004000  bl2
0x020000  primary_tfm_s / cpu0_app / ap_app     槽 A（primary_all）
0x36C000  secondary_tfm_s / cpu0_app / ap_app   槽 B（secondary_all）
0x6CB000  boot_param                            8K，两扇区 ping-pong
0x7FE000  sys_rf / sys_net
```

无 `ota` 暂存区。槽大小由 `secondary_tfm_s.base - primary_tfm_s.base` 计算，
两槽必须等长且相邻。AP 通过 `bk_ota_get_current_partition()` 读
`SOC_FLASH_REG_BASE + 0x19*4` 的 bit0，得到运行槽，对侧即为写入槽。

<a id="ota-bin"></a>

## 升级包 ota.bin

头格式与 Overwrite 相同（magic BK723658，32B 全局头 \+ 32B image 头，image\_num 为 1）。
payload 来自 ``` ota_signed.bin``（BL2 签名后的 ``primary_all ```）。若打开 Flash AES，
打包器可对 payload 做 XTS-AES；Direct-XIP 下 BL2 remap 共享 tweak，同一密文可在两槽使用。

AP 同样只校验头 CRC 与 payload CRC，不在非安全世界验签。

<a id="boot-param-ab-flag-record-t"></a>

## `boot_param` / `ab_flag_record_t`

与非安全 AB 共用 `ab_flag.h` 布局（32 字节，两份 4KB ping-pong）。安全 XIP 把记录写在
`boot_param` 分区，供 BL2/SPE 读取。

| 偏移 | 类型 | 字段 |
| --- | --- | --- |
| 0x00 | u32 | `magic` \= ``` 0x31464241``（``ABF1 ```） |
| 0x04 | u16 | `struct_ver` \= 1 |
| 0x06 | u16 | `size` \= 32 |
| 0x08 | u32 | `seq`：单调新鲜度，大者更新；提交时写对侧扇区 |
| 0x0C | u8 | `exec_slot`：已提交槽（0\=A / 1\=B） |
| 0x0D | u8 | `update_slot`：试跑目标槽 |
| 0x0E | u8 | `boot_state`：`NORMAL=0x01` / `TRIAL=0x02` / `CONFIRMED=0x03` |
| 0x0F | u8 | `dl_state`：`IDLE/ONGOING/DONE` |
| 0x10 | u8 | `try_max`：默认 5，上限 7（AON PMU 3bit 计数） |
| 0x11 | 3\+8 bytes | reserved，必须为 0（计入 CRC） |
| 0x1C | u32 | `crc32`：zlib CRC32，覆盖前 28 字节 |

`ota_boot_param_set_trial(update_slot)`：

- `exec_slot` \= 当前 remap 运行槽（不以旧记录为准）
- `update_slot` \= 刚写完的空闲槽
- `boot_state` \= `TRIAL`，`dl_state` \= `DONE`
- 保留原 `try_max`；处女分区默认 5

<a id="id3"></a>

## 端到端全流程

下载解析与 Overwrite 相同（64B 头 \+ payload CRC），差别是写入对侧槽，武装的是
boot\_param TRIAL 而不是 ota\_control confirm。

```
[AP 运行中] 读 remap bit0 = running (0=A / 1=B)
     inactive = running xor 1
     写指针 = inactive 槽基址
     |
     +-- 槽分区缺失 --> ota_fail，不重启
     v
HEADER / PAYLOAD 写入 inactive 槽
     (magic / 头 CRC / image_num / 长度 / 写回读 / payload CRC)
     +-- 任一失败 --> PHASE_ERROR，ota_fail，不重启
     |                 TRIAL 未写，下次仍跑 running 槽
     +-- 下载中复位 --> 同上；对侧可能残留半包，下次 OTA 整槽重写
     v
PHASE_DONE
     |
finish(): ota_boot_param_set_trial(inactive)
     ping-pong 写对侧 4KB 扇区
     exec_slot=running, update_slot=inactive
     boot_state=TRIAL, dl_state=DONE
     +-- boot_param 分区缺失 / commit 失败
     |     --> secure finalize failed，不重启
     v
reboot  ---------------------------------------------------------
     |
BL2 boot_param_load() + decide_slot()
     |
     +-- 无合法记录 (处女分区) --> preferred = 槽 A
     +-- NORMAL / CONFIRMED    --> preferred = exec_slot
     |                             (不写 Flash，不清 PMU)
     +-- TRIAL --> AON PMU try_cnt++
                   try_cnt < try_max --> preferred = update_slot
                   否则 commit NORMAL(exec_slot)，清 PMU，回滚
     v
MCUboot 对 preferred 槽做 EC-P256 验签
     +-- 失败 --> reconcile 到另一合法槽并写回 boot_param
     |            两槽都坏则无法启动
     v
设置 remap bit0 = 选中槽，跳 TF-M
     |
TF-M: boot_param_confirm()
     +-- 不是 TRIAL --> 忽略
     +-- 是 TRIAL --> exec_slot = 实际 remap 运行槽
                      (若 BL2 已回滚，这里确认的是旧槽，不会把坏槽坐实)
                      写 NORMAL，清 PMU 试跑计数
     |
进入 NS 应用
```

试跑计数在 AON PMU（bl2\_reset\_count），不写 Flash。连续 OTA 前必须在确认时清零，
否则计数累加会误回滚。

<a id="id4"></a>

## 回滚语义

- 新槽验签失败：BL2 不切过去，reconcile 回旧槽。
- 新槽能起来但反复复位、未到 TF-M confirm：`try_cnt` 到 `try_max` 后回滚。
- 下载中复位：未写 TRIAL，下次仍引导旧槽；对侧可能残留半包，下次 OTA 会整槽重写。
