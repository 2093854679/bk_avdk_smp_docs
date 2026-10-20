---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_pwm.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="pwm"></a>

# PWM 使用指南

<a id="id1"></a>

## 概述

PWM 用于产生可配置占空比的方波。BK7259 CP 提供 12 路 PWM 通道（`pwm_cap.h`）。

> - API 参考：[PWM](../../api-reference/peripheral/bk_pwm.md)

<a id="id2"></a>

## 相关代码路径

> - API 头文件：`include/driver/pwm.h`
> - 驱动实现：`middleware/driver/pwm/`

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
- [TRNG](bk_trng.md)
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
