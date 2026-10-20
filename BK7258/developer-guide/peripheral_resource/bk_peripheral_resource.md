---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral_resource/bk_peripheral_resource.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: SMP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 外设资源介绍

<a id="id2"></a>

## 概述

当前bk\_avdk\_smp支持AP和CP两个独立的子系统，本章节将介绍各个子系统上支持的外设资源。

<a id="cp"></a>

## 1 CP侧支持的外设资源

使用下列表格，将介绍CP侧支持哪些外设资源

> | NAME | Description | Detailed description of the link |
> | --- | --- | --- |
> | UART0 | CP侧仅支持使用UART0，用于输出log | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_uart.html](../../cp_doc/developer-guide/peripheral/bk_uart.md) |
> | WDT | CP侧支持WDT的相关操作，比如喂狗，重启 | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_wdt.html](../../cp_doc/developer-guide/peripheral/bk_wdt.md) |
> | RTC | CP侧支持RTC的读、写操作 | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_rtc.html](../../cp_doc/developer-guide/peripheral/bk_rtc.md) |
> | TIMER0 | CP侧仅支持使用TIMER0，通道是0\~2 | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_timer.html](../../cp_doc/developer-guide/peripheral/bk_timer.md) |
> | DMA | CP侧仅支持使用DMA通道12\~15 | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_dma.html](../../cp_doc/developer-guide/peripheral/bk_dma.md) |
> | OTP1 | CP侧仅支持使用OTP1 | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_otp.html](../../cp_doc/developer-guide/peripheral/bk_otp.md) |
> | FLASH | CP侧支持使用FLASH,可以直接操作FLASH媒介 | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_flash.html](../../cp_doc/developer-guide/peripheral/bk_flash.md) |
> | EFUSE | CP侧支持使用EFUSE | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_efuse.html](../../cp_doc/developer-guide/peripheral/bk_efuse.md) |
> | TRNG | CP侧支持使用TRNG | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_trng.html](../../cp_doc/developer-guide/peripheral/bk_trng.md) |
> | GPIO | CP侧默认仅支持使用GPIO10\~11，用于UART0输出log | [../../../../../../cp\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_gpio.html](../../cp_doc/developer-guide/peripheral/bk_gpio.md) |
>
> 重要
>
> *Note：对于GPIO,CP侧默认仅支持使用GPIO10\~11，涉及到低功耗，CP侧会用到其他的GPIO.*

<a id="ap"></a>

## 2 AP侧支持的外设资源

使用下列表格，将介绍AP侧支持哪些外设资源

> | NAME | Description | Detailed description of the link |
> | --- | --- | --- |
> | UART1\~2 | AP侧仅支持使用UART1\~2，不支持使用UART0 | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_uart.html](../../ap_doc/developer-guide/peripheral/bk_uart.md) |
> | WDT | AP侧只支持WDT的重启但依赖于mailbox,由CP侧进行reboot | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_wdt.html](../../ap_doc/developer-guide/peripheral/bk_wdt.md) |
> | RTC | AP侧只支持RTC的读操作、不支持写操作 | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_rtc.html](../../ap_doc/developer-guide/peripheral/bk_rtc.md) |
> | TIMER1 | AP侧仅支持使用TIMER1，通道是3\~5 | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_timer.html](../../ap_doc/developer-guide/peripheral/bk_timer.md) |
> | DMA | AP侧仅支持使用DMA通道0\~11 | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_dma.html](../../ap_doc/developer-guide/peripheral/bk_dma.md) |
> | OTP2 | AP侧仅支持使用OTP2 | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_otp.html](../../ap_doc/developer-guide/peripheral/bk_otp.md) |
> | FLASH | AP侧依赖于mailbox和CP侧通信,从而来操作FLASH媒介 | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_flash.html](../../ap_doc/developer-guide/peripheral/bk_flash.md) |
> | TRNG | AP侧支持使用TRNG， | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_trng.html](../../ap_doc/developer-guide/peripheral/bk_trng.md) |
> | GPIO | 除了GPIO10\~11，AP侧默认支持额外所有的GPIO | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_gpio.html](../../ap_doc/developer-guide/peripheral/bk_gpio.md) |
> | SPI | AP侧支持使用SPI | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_spi.html](../../ap_doc/developer-guide/peripheral/bk_spi.md) |
> | QSPI | AP侧支持使用QSPI | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_qspi.html](../../ap_doc/developer-guide/peripheral/bk_qspi.md) |
> | SDIO | AP侧支持使用SDIO | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/examples/peripheral/bk\_sdio.html](../../ap_doc/examples/peripheral/bk_sdio.md) |
> | USB | AP侧支持使用USB | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_usb.html](../../ap_doc/developer-guide/peripheral/bk_usb.md) |
> | CAN | AP侧支持使用CAN | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_can.html](../../ap_doc/developer-guide/peripheral/bk_can.md) |
> | TE200 | AP侧支持使用TE200 | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/security/mbedtls\_and\_trustengine.html](../../ap_doc/developer-guide/security/mbedtls_and_trustengine.md) |
> | PWM | AP侧支持使用PWM | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_pwm.html](../../ap_doc/developer-guide/peripheral/bk_pwm.md) |
> | KEY | AP侧支持使用KEY | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_gpio.html](../../ap_doc/developer-guide/peripheral/bk_gpio.md) |
> | I2C | AP侧支持使用I2C | [../../../../../../ap\_doc/bk7258/zh\_CN/v3.1.1/developer-guide/peripheral/bk\_i2c.html](../../ap_doc/developer-guide/peripheral/bk_i2c.md) |
>
> 重要
>
> *Note：对于GPIO,AP侧默认支持其他的GPIO（除了CP侧默认支持使用GPIO10\~11).*
