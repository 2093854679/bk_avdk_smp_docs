---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_rtc.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# RTC 使用指南

<a id="id1"></a>

## 概述

实时时钟（Real -Time Clock,RTC）是嵌入式系统中记录时间的硬件模块,RTC在低压和深度睡眠模式下可以不间断计时。

备注

RTC模块默认在CP上使用，AP上仅保留读取时间接口

<a id="id2"></a>

## RTC 使用方法

RTC 有两种常见的使用方式：

> - 统计代码执行时间，使用RTC来记录程序的开始和结束时间，从而计算出代码执行所需的时间。
> - 注册闹钟定期执行回调，设置RTC闹钟定期触发，执行指定的回调函数，实现定时任务的处理。

RTC相关测试和使用介绍: [RTC\_example\_driver](../../examples/peripheral/bk_rtc.md)

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
- [TRNG](bk_trng.md)
- [SARADC](bk_adc.md)
- [SPI](bk_spi.md)
- [UART](bk_uart.md)
- [WDT](bk_wdt.md)
- [I2S](bk_i2s.md)
- [GPIO](bk_gpio.md)
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
