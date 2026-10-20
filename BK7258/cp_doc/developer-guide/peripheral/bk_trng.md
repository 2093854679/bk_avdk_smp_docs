---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_trng.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="trng"></a>

# TRNG 使用指南

<a id="id1"></a>

## 概述

TRNG 真随机数发生器，集成在 Beken 芯片内部，通过随机噪声产生真随机数，不依赖于其他模块。

<a id="id2"></a>

## TRNG 使用方法

> - TRNG使能，可调用 bk\_trng\_start() 使能
> - 获取随机数，调用 bk\_rand() 获取

备注

默认情况下系统已经初始化 TRNG 模块，应用可以直接使用 bk\_rand()

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
- [ICU](bk_interrupt.md)
- [SARADC](bk_adc.md)
- [SPI](bk_spi.md)
- [UART](bk_uart.md)
- [WDT](bk_wdt.md)
- [I2S](bk_i2s.md)
- [GPIO](bk_gpio.md)
- [RTC](bk_rtc.md)
- [OTP](bk_otp.md)
- [FLASH](bk_flash.md)
- [EFUSE](bk_efuse.md)
- [PSRAM](bk_psram.md)
- [TIMER](bk_timer.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [OS 相关参考](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
