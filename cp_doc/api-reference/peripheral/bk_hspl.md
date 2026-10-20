---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_hspl.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="hspl"></a>

# HSPL

BK7259 CP 侧 HSPL（Hardware Spin Lock）API。详细说明见
[HSPL 开发指南](../../developer-guide/peripheral/bk_hspl.md)。

<a id="hspl-driver-api"></a>

## HSPL Driver API

- `bk_hspl_driver_init` / `bk_hspl_driver_deinit`
- `bk_hspl_try_lock` / `bk_hspl_unlock`
- `bk_hspl_get_state`

<a id="hspl-resource-lock-api"></a>

## HSPL Resource Lock API

- `bk_hspl_res_lock` / `bk_hspl_res_try_lock` / `bk_hspl_res_unlock`
- `bk_hspl_res_lock_irqsave` / `bk_hspl_res_unlock_irqrestore`
- `bk_hspl_res_must_lock`
- `bk_hspl_res_get_map`

<a id="id1"></a>

## 头文件

- `middleware/driver/hspl/hspl_driver.h`
- `middleware/driver/hspl/hspl_res_lock.h`

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [外设](../peripheral.md)
- [DMA](bk_dma.md)
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
- [PWM](bk_pwm.md)
- [TOUCH](bk_touch.md)
- [Timer](bk_timer.md)
- [系统](../system.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
