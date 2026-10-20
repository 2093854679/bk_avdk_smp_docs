---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_trng.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rng"></a>

# 随机数 (RNG) 使用指南

<a id="id1"></a>

## 概述

BK7259 已移除独立的 TRNG 外设驱动（`bk_trng_*` API 及 `driver/trng.h` 不再提供）。
系统随机数统一通过 `bk_rand()` 与 `bk_fill_rand()` 获取，定义于 `components/bk_platform.h`。

熵源由 PSA Mbed TLS 平台层在运行时选择：TrustEngine TE200 硬件 TRNG、OTP 随机数，或软件 `rand()` 回退。

<a id="id2"></a>

## 使用方法

> - 获取随机整数：调用 `bk_rand()`
> - 填充随机字节：调用 `bk_fill_rand(buff, len)`

备注

启用 `CONFIG_PSA_MBEDTLS=y` 时，上述接口由 PSA 平台层提供 strong 实现，无需单独初始化 TRNG 外设。

<a id="id3"></a>

## 推荐配置

安全相关场景建议开启 `CONFIG_PSA_MBEDTLS`、`CONFIG_TRUSTENGINE` 与 `CONFIG_TE200_ENTROPY`。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [软件架构与分层](../architecture.md)
- [系统安全](../security.md)
- [低功耗与电源管理](../power_save.md)
- [设备管理框架](../driver_model.md)
- [外设与驱动](../peripheral.md)
- [DMA](bk_dma.md)
- [HSPL](bk_hspl.md)
- [IPI](bk_ipi.md)
- [ICU](bk_interrupt.md)
- [IRDA](bk_irda.md)
- [LIN](bk_lin.md)
- [SARADC](bk_adc.md)
- [UART](bk_uart.md)
- [Watchdog](bk_wdt.md)
- [I2S](bk_i2s.md)
- [GPIO](bk_gpio.md)
- [RTC](bk_rtc.md)
- [Calendar](bk_calendar.md)
- [CKMN](bk_ckmn.md)
- [OTP](bk_otp.md)
- [FLASH](bk_flash.md)
- [FLASH_PARTITION](bk_flash_partition.md)
- [EFUSE](bk_efuse.md)
- [PSRAM](bk_psram.md)
- [PWM](bk_pwm.md)
- [TOUCH](bk_touch.md)
- [TIMER](bk_timer.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [CPU Hotplug](../cpu_hotplug.md)
- [Wi-Fi](../wifi.md)
- [HTTP](../http.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
