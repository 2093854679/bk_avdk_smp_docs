---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_ap_fast_boot_config.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap"></a>

# AP快速启动配置说明

AP快速启动用于AP低功耗掉电后恢复原有FreeRTOS执行点，减少AP重新启动和业务重新初始化的时间。本功能建立在低功耗工程配置之上，参考工程为 `projects/pm/ap_fast_boot`。

<a id="id1"></a>

## 工作原理

普通AP掉电后再次上电时，会从复位流程重新启动。使能AP快速启动后，系统在AP掉电前保存CPU0架构上下文，将掉电的DTCM内容备份到保持供电的AP SRAM；AP再次上电时，从复位入口恢复DTCM和CPU上下文，然后回到掉电前保存的FreeRTOS执行点继续运行。

快速启动依赖PSRAM数据保持。低功耗期间系统保持PSRAM单元供电，避免AP恢复后访问到失效数据。该功能会增加一部分保持功耗，应根据启动时延和待机功耗要求进行取舍。

<a id="cp"></a>

## CP侧配置

在低功耗CP侧 `defconfig` 配置基础上，在 `projects/pm/ap_fast_boot/cp/config/bk7259/defconfig` 中增加：

```
   CONFIG_PSRAM_DATA_RETENTION_ENABLE=y
   CONFIG_PM_AP_FAST_BOOT_ENABLE=y

- ``CONFIG_PSRAM_DATA_RETENTION_ENABLE=y``：CP进入深度睡眠或低压睡眠时保持PSRAM单元供电，使PSRAM数据在AP掉电期间继续有效。
- ``CONFIG_PM_AP_FAST_BOOT_ENABLE=y``：使能CP侧AP快速启动协同流程。该宏依赖 ``CONFIG_PM_AP_POWERDOWN_WHEN_LV=y`` 和 ``CONFIG_PSRAM_DATA_RETENTION_ENABLE=y``。
```

<a id="id2"></a>

## AP侧配置

在低功耗AP侧 `defconfig` 配置基础上，在 `projects/pm/ap_fast_boot/ap/config/bk7259_ap/defconfig` 中增加：

```
   CONFIG_PSRAM_DATA_RETENTION_ENABLE=y
   CONFIG_PM_AP_FAST_BOOT_ENABLE=y

- ``CONFIG_PSRAM_DATA_RETENTION_ENABLE=y``：使能AP侧PSRAM数据保持支持。
- ``CONFIG_PM_AP_FAST_BOOT_ENABLE=y``：使能AP上下文保存和恢复流程。AP侧该宏依赖 ``CONFIG_SOC_SMP=y`` 和 ``CONFIG_PSRAM_DATA_RETENTION_ENABLE=y``，并会选择 ``CONFIG_DEEP_LV``。
```

<a id="id3"></a>

## 配置要求与注意事项

> - CP和AP两侧必须同时使能 `CONFIG_PSRAM_DATA_RETENTION_ENABLE` 和 `CONFIG_PM_AP_FAST_BOOT_ENABLE`，两侧配置不一致会导致快速启动流程无法正常协同。
> - 必须保留基础低功耗配置，包括CP侧 `CONFIG_PM_AP_POWERDOWN_WHEN_LV=y`、Deep LV支持，以及AP/CP之间正确的关机和唤醒流程。
> - AP掉电前应停止或挂起不能跨掉电恢复的外设访问，确保DMA、Mailbox、中断和共享资源处于可恢复状态。
> - 快速启动恢复的是保存点处的软件上下文，不表示所有掉电外设的硬件寄存器都会自动恢复。业务仍需按模块要求恢复掉电的外设和AP子电源域。
> - 使能PSRAM保持会提高低功耗电流。应在目标板上同时验证AP恢复时延、PSRAM数据完整性、反复睡眠唤醒稳定性和待机功耗。
> - 如果业务不需要保留AP运行上下文，关闭这两个宏可恢复普通AP冷启动流程，并减少PSRAM保持带来的功耗。
