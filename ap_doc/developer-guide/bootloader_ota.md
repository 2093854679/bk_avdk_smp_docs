---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/bootloader_ota/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bootloader-ota"></a>

# Bootloader 与 OTA

本章按当前 `ap/components/ota` 与 BL2/TF-M 代码，说明 BK7259 的四套 HTTP 固件升级方案，
以及 BLE OTA。OTA 下载发生在 AP 非安全世界；安全方案的验签、解压覆盖或槽位选择由 BL2（MCUboot）完成。
四套 HTTP 方案共用同一套传输与 `f_ota_func_t` 后端框架，由 Kconfig 互斥选择后端。

<a id="id1"></a>

## 方案对照

| 项目 | 安全 Overwrite | 安全 XIP A/B | 非安全 AB | 非安全非 AB |
| --- | --- | --- | --- | --- |
| 参考工程 | `secureboot_overwrite` | `secureboot_xip` | `app_ab` | `app` |
| AP Kconfig | `CONFIG_SECURE_OTA_OVERWRITE` | `CONFIG_SECURE_OTA_XIP` | CONFIG\_HTTP\_AB\_PARTITION \+ CONFIG\_OTA\_POSITION\_INDEPENDENT\_AB | CONFIG\_OTA\_HTTP（默认后端） |
| 后端源码 | `ota_secure_overwrite.c` | `ota_secure_xip.c` | `ota_base_drv.c` \+ `ota_common.c` | `ota_base_drv.c` |
| 下载落点 | `ota` 暂存区 | 对侧 `primary_all` / `secondary_all` | 对侧 application / s\_app | ota（download）分区 |
| 升级包 | ota.bin（压缩签名 \+ 64B 头） | ota.bin（签名镜像 \+ 64B 头） | `app_pack.rbl` | `app_pack.rbl` |
| 安装者 | BL2 LZMA 解压覆盖 `primary_all` | BL2 Direct-XIP 切槽，原地执行 | up\_bootloader 设 remap bit | up\_bootloader 解压解密搬运到 app |
| 启动确认 | `ota_control` 末尾 `OVERWRITE_CONFIRM` | `boot_param` TRIAL 记录 | `ota_fina_executive` TRIAL 记录 | download 区非空即安装 |
| 回滚 | 无 A/B；掉电靠 journal 续传 | 试跑 `try_max` 次回滚 | 试跑 `try_max` 次回滚 | 无回滚 |
| 验签 | BL2 EC-P256 | BL2 EC-P256 | RBL CRC / 可选 FNV hash | RBL CRC / hash |

备注

- `CONFIG_SECURE_OTA_XIP` 与 `CONFIG_SECURE_OTA_OVERWRITE` 互斥，不可同时打开。
- 安全 OTA **不走** 已删除的 TF-M FWU / `CONFIG_SECURITY_OTA` 路径。
- HTTP CLI 统一为 ``` http_ota <url>``（AP：``ap_cmd http_ota ... ```）。

<a id="id2"></a>

## 四套方案阶段对照

每套方案都经过「下载 → 武装 → 复位 → 安装/选槽 → 确认」五段。差异在武装介质和安装者：

```
AP 非安全世界                    复位之后
----------------------          --------------------------------
1. HTTP 下载到目标分区
2. 校验（头 CRC / RBL / hash）
3. 武装安装意图（或直接 reboot）
       |                                  |
       v                                  v
Overwrite: 写 ota_control confirm    BL2: 解压覆盖 primary_all + 验签
                                     TF-M: 清 confirm
XIP:       写 boot_param TRIAL       BL2: 选槽 + 验签 + remap
                                     TF-M: TRIAL -> NORMAL
非安全 AB: 写 ota_fina_executive     bootloader: 选槽 + RBL/hash + remap
           TRIAL                     app init: 自动 confirm
非安全非AB: 不写标志，download       up_bootloader: 解压覆盖 app
            非空即视为待安装         无试跑、无回滚
```

各章「端到端全流程」含失败 / 掉电分支，不要只看成功箭头。

- [公共框架](bootloader_ota/bk_ota_framework.md)
- [安全 Overwrite 方案](bootloader_ota/bk_ota_secure_overwrite.md)
- [安全 XIP A/B 方案](bootloader_ota/bk_ota_secure_xip.md)
- [非安全非 AB 方案](bootloader_ota/bk_ota_nosecure.md)
- [非安全 AB 方案](bootloader_ota/bk_ota_nosecure_ab.md)
- [BLE\_OTA](bootloader_ota/ble_ota.md)
