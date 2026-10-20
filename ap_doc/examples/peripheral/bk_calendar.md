---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_calendar.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="calendar"></a>

# Calendar

<a id="id1"></a>

## 1 功能概述

Calendar demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [Calendar 开发指南](../../developer-guide/peripheral/bk_calendar.md)。

API 参考见 [Calendar API](../../api-reference/peripheral/bk_calendar.md)。

<a id="id2"></a>

## 2 代码路径

> - demo 路径：
>   :   `ap/components/bk_cli/cli_calendar.c`
> - 驱动源码路径：
>   :   `ap/middleware/driver/calendar/`

<a id="id3"></a>

## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_CALENDAR` | Calendar 驱动 | 依项目配置 |
| `CONFIG_CLI` | CLI 支持 | 依项目配置 |

<a id="cli"></a>

## 4 CLI 命令简介

使能 `CONFIG_CALENDAR` 后，使用 `calendar_driver init` 与 `calendar get_time_us` 读取日历时间。

备注

具体子命令以固件 `help` 输出为准。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [命令](../cli.md)
- [外设](../peripheral.md)
- [I2C](bk_i2c.md)
- [I3C](bk_i3c.md)
- [PWM](bk_pwm.md)
- [SDIO](bk_sdio.md)
- [SPI](bk_spi.md)
- [I2S](bk_i2s.md)
- [CAN](bk_can.md)
- [UART](bk_uart.md)
- [Watchdog](bk_wdt.md)
- [DMA](bk_dma.md)
- [HPDMA](bk_hpdma.md)
- [QSPI](bk_qspi.md)
- [QSPI Flash](bk_qspi_flash.md)
- [TIMER](bk_timer.md)
- [RTC](bk_rtc.md)
- [OTP](bk_otp.md)
- [FLASH](bk_flash.md)
- [PSRAM](bk_psram.md)
- [GPIO](bk_gpio.md)
- [USB](bk_usb.md)
- [TOUCH](bk_touch.md)
- [IPI](bk_ipi.md)
- [IRDA](bk_irda.md)
- [HSPL](bk_hspl.md)
- [平台](../platform.md)
- [项目示例](../projects.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
