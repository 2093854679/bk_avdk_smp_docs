---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_wdt.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="watchdog"></a>

# Watchdog

<a id="ap-wwdt-api"></a>

## AP `wwdt` API 状态

BK7259 AP 侧没有 AON\_WDT 硬件 API，对外可用的硬件看门狗 API 只有 `wwdt`。

| API | BK7259\_AP |
| --- | --- |
| `bk_wwdt_driver_init()` | Y |
| `bk_wwdt_driver_deinit()` | Y |
| `bk_wwdt_start()` | Y |
| `bk_wwdt_stop()` | Y |
| `bk_wwdt_feed()` | Y |
| `bk_wwdt_get_feed_time()` | Y |
| `bk_wwdt_set_feed_time()` | Y |
| `bk_wwdt_is_driver_inited()` | Y |
| `bk_wwdt_get_cpu_id()` | Y |

<a id="wwdt-api"></a>

## `wwdt` API 头文件

> - API 头文件：`ap/include/driver/wwdt.h`
> - 类型定义：`ap/include/driver/wwdt_types.h`、`ap/include/driver/hal/hal_wwdt_types.h`

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [外设](../peripheral.md)
- [DMA](bk_dma.md)
- [HPDMA](bk_hpdma.md)
- [EFUSE](bk_efuse.md)
- [GPIO](bk_gpio.md)
- [HSPL](bk_hspl.md)
- [ICU](bk_interrupt.md)
- [IPI](bk_ipi.md)
- [I3C](bk_i3c.md)
- [IRDA](bk_irda.md)
- [LIN](bk_lin.md)
- [Mailbox](bk_mailbox.md)
- [OTP](bk_otp.md)
- [PSRAM](bk_psram.md)
- [PWM](bk_pwm.md)
- [SARADC](bk_adc.md)
- [SPI](bk_spi.md)
- [QSPI](bk_qspi.md)
- [Timer](bk_timer.md)
- [TRNG](bk_trng.md)
- [UART](bk_uart.md)
- [USB](bk_usb.md)
- [I2C](bk_i2c.md)
- [TOUCH](bk_touch.md)
- [FLASH](bk_flash.md)
- [FLASH_PARTITION](bk_flash_partition.md)
- [I2S](bk_i2s.md)
- [CAN](bk_can.md)
- [Calendar](bk_calendar.md)
- [CKMN](bk_ckmn.md)
- [RTC](bk_rtc.md)
- [系统](../system.md)
- [网络](../network.md)
- [Wi-Fi](../wifi.md)
- [多媒体](../multimedia.md)
- [音频](../audio.md)
- [蓝牙](../bluetooth.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [项目示例](../../examples/projects.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
