---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_lin.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="lin"></a>

# LIN

<a id="id1"></a>

## 1 功能概述

LIN demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [LIN 开发指南](../../developer-guide/peripheral/bk_lin.md)。

API 参考见 [LIN API](../../api-reference/peripheral/bk_lin.md)。

<a id="id2"></a>

## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/lin/lin_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/lin/`

<a id="id3"></a>

## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_LIN` | LIN 驱动 | 依项目配置 |
| `CONFIG_LIN_TEST` | LIN CLI 测试 | 依项目配置 |

<a id="cli"></a>

## 4 CLI 命令简介

使能 LIN 测试配置后，使用 `lin` 命令验证 LIN 总线通信。

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
- [DMA](bk_dma.md)
- [IPI](bk_ipi.md)
- [IRDA](bk_irda.md)
- [SARADC](bk_adc.md)
- [SDIO](bk_sdio.md)
- [I2S](bk_i2s.md)
- [UART](bk_uart.md)
- [Watchdog](bk_wdt.md)
- [GPIO](bk_gpio.md)
- [HSPL](bk_hspl.md)
- [RTC](bk_rtc.md)
- [Calendar](bk_calendar.md)
- [CKMN](bk_ckmn.md)
- [OTP](bk_otp.md)
- [FLASH](bk_flash.md)
- [EFUSE](bk_efuse.md)
- [PSRAM](bk_psram.md)
- [PWM](bk_pwm.md)
- [TOUCH](bk_touch.md)
- [TIMER](bk_timer.md)
- [平台](../platform.md)
- [VND_CAL](../vnd_cal/vnd_cal.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
