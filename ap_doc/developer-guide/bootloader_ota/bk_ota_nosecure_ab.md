---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/bootloader_ota/bk_ota_nosecure_ab.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ab"></a>

# 非安全 AB（位置无关）升级方案

<a id="id1"></a>

## 原理

`projects/app_ab` 在非安全启动下提供双执行槽：A 为 `primary_cp_app + primary_ap_app`
（分区名 `application`），B 为 `s_app`。镜像位置无关，通过 Flash remap bit0 选择
运行槽。OTA 写入对侧槽，下载完成后在 `ota_fina_executive` 提交 TRIAL 记录；bootloader
试跑新槽，应用 `bk_init()` 里调用 `bk_ota_double_check_for_execution()` 自动确认。

与安全 XIP 的相同点：ping-pong 标志、`try_max`、remap 切槽、失败回滚。
不同点：标志分区名是 `ota_fina_executive` 而不是 `boot_param`；安装者是
**up\_bootloader** 而不是 BL2；完整性是 RBL magic \+ `info_crc32` \+ 可选 FNV hash，
没有 EC-P256。

<a id="id2"></a>

## 参考工程与开关

- 工程：`projects/app_ab`
- 编译：`make bk7259 PROJECT=app_ab`
- AP：CONFIG\_HTTP\_AB\_PARTITION\=y，CONFIG\_OTA\_POSITION\_INDEPENDENT\_AB\=y
- 可选：CONFIG\_OTA\_HASH\_FUNCTION（下载后对目标槽做 hash）
- 产物：按 `ota_rbl.config` 生成的 A/B 升级包
- CLI：http\_ota、ab\_version、swap（两槽都有镜像时强制切槽）

<a id="flash-app-ab"></a>

## Flash 布局（参考 `app_ab` 分区表）

```
primary_bootloader     64K
primary_cp_app + primary_ap_app    槽 A（application）
s_app                  2516K       槽 B（与 A 等长的位置无关镜像）
ota_fina_executive     8K          AB 标志 ping-pong
usr_config / easyflash / sys_rf / sys_net
```

无独立 `ota` 暂存区：包直接写进对侧执行槽。

<a id="id3"></a>

## 标志记录

布局与安全 XIP 的 `ab_flag_record_t` 完全相同（见 [安全 Direct-XIP A/B 升级方案](bk_ota_secure_xip.md)），
必须与 bootloader、Python 打包器字节级一致，否则 CRC 会拒识合法记录。

提交规则（`ab_record_commit`）：

- 永远写 **对侧** 4KB 扇区，旧副本保持有效，掉电不会变成全 `0xFF`。
- `seq` 单调加一；读取取较大且 CRC 合法的一份。
- reserved 必须填 0，计入 CRC。

<a id="id4"></a>

## 端到端全流程

`system_startup()` 在 AB 工程直接走 `ab_boot_main()`，并不经过 download 区的
`ota_main()`。AP 把 .rbl 写进对侧执行槽；bootloader 只做校验、remap、跳转。

目标槽由 `bk_ota_get_update_partition()` 推导，恒为当前运行槽的对侧：
运行 A 则写 s\_app，运行 B 则写 application。

槽完整性：RBL 魔数 `RBL\\0` （槽尾偏移 0x1000）\+ 头 info\_crc32 \+ 固件 FNV hash。
任何切槽都以校验通过为前提，不会盲跳损坏分区。

```
[AP 运行于 A]                      [AP 运行于 B]
     |                                  |
下载 .rbl 到 s_app                 下载 .rbl 到 application
     +-- 写 Flash 失败 --> ota_fail，不重启，TRIAL 未写
     +-- 下载中复位 -----> TRIAL 未写，下次仍跑旧槽（对侧可能半包）
     v
可选 ota_do_hash_check() (CONFIG_OTA_HASH_FUNCTION)
     +-- hash 失败 --> 不武装，不重启
     v
bk_ota_update_partition_flag()
     ping-pong 写 ota_fina_executive
     exec_slot=running, update_slot=对侧
     boot_state=TRIAL, dl_state=DONE
     |
ota_success + reboot  (不走 finish 钩子)
     |
------------------ 复位：ab_boot_main() ----------------
     |
读 ota_fina_executive 最新合法记录 (seq 大且 CRC 过)
     |
     +-- 无记录: 探测 A 再探测 B
     |     有合法 RBL 的槽可引导；都坏则 DEAD (复位/需重烧)
     |
     +-- NORMAL:
     |     exec_slot hash 通过 --> 清 PMU，remap 跑 exec_slot
     |     exec_slot 坏、对侧好 --> 自愈写 NORMAL(对侧) 再跳
     |     两槽都坏 --> DEAD
     |
     +-- TRIAL:
           AON PMU count+1
           count>=try_max 或 update_slot hash 失败?
             否 --> remap 试跑 update_slot
             是 --> 旧 exec_slot 完好则回滚并写 NORMAL
                    否则 DEAD
     |
jump 到选中槽的 app
     |
AP bk_init() -> bk_ota_double_check_for_execution()
     +-- 不是 TRIAL --> 忽略
     +-- remap 运行槽 != update_slot --> bootloader 已回滚，不确认
     +-- 否则写 NORMAL(exec_slot=running)，清 PMU
     |
试跑成功，新槽成为提交槽
```

备注

升级目标不再由客户回调指定，SDK 自动取对侧槽；确认也不再需要客户选 A/B，
应用正常启动即视为试跑成功。
