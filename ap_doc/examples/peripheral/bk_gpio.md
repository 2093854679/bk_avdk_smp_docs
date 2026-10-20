---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_gpio.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="gpio"></a>

# GPIO

<a id="id1"></a>

## 1 功能概述

GPIO demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [GPIO 开发指南](../../developer-guide/peripheral/bk_gpio.md)。

API 参考见 [GPIO API](../../api-reference/peripheral/bk_gpio.md)。

<a id="id2"></a>

## 2 代码路径

> - demo 路径：
>   :   `ap/middleware/driver/gpio/gpio_test.c`
> - 驱动源码路径：
>   :   `ap/middleware/driver/gpio/`

<a id="id3"></a>

## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_GPIO` | GPIO 驱动 | 依项目配置 |
| `CONFIG_GPIO_TEST` | GPIO CLI 测试 | 依项目配置 |
| `CONFIG_DRV_CLI_SUPPORT` | 驱动 CLI 支持 | 依项目配置 |

<a id="cli"></a>

## 4 CLI 命令简介

使能 `CONFIG_GPIO_TEST` 与 `CONFIG_DRV_CLI_SUPPORT` 后，执行 `gpio_driver init` 初始化，再使用 `gpio`、`gpio_int` 等子命令测试输入输出与中断。

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
- [USB](bk_usb.md)
- [TOUCH](bk_touch.md)
- [IPI](bk_ipi.md)
- [IRDA](bk_irda.md)
- [HSPL](bk_hspl.md)
- [Calendar](bk_calendar.md)
- [平台](../platform.md)
- [项目示例](../projects.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
