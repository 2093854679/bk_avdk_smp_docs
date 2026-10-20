---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_trng.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rng"></a>

# 随机数 (RNG)

<a id="rng-api-status"></a>

## RNG API Status

| API | BK7259\_AP |
| --- | --- |
| [`bk_rand()`](#c.bk_rand "bk_rand") | Y |
| [`bk_fill_rand()`](#c.bk_fill_rand "bk_fill_rand") | Y |

备注

以下 API 已移除，请勿在新代码中使用：`bk_trng_driver_init`、`bk_trng_driver_deinit`、
`bk_trng_start`、`bk_trng_stop`。随机数请改用 `bk_rand()` 与 `bk_fill_rand()`。

<a id="rng-api-reference"></a>

## RNG API Reference

<a id="c.bk_rand"></a>

int bk\_rand(void)
:   获取一个 32 位随机整数。

    返回值与 `RAND_MAX` 按位与后返回。熵源取决于工程配置（TrustEngine / OTP / 软件 `rand()`），
    详见 [随机数 (RNG) 使用指南](../../developer-guide/peripheral/bk_trng.md)。

<a id="c.bk_fill_rand"></a>

int bk\_fill\_rand(void \*buff, size\_t len)
:   向缓冲区填充 `len` 字节随机数据。

    参数
    :   - **buff** – 输出缓冲区指针
        - **len** – 待填充字节数

    返回
    :   成功返回 `0`；`buff` 为 `NULL` 或 `len` 为 `0` 时返回 `-1`

<a id="id1"></a>

## 头文件

- [ap/include/components/bk\_platform.h](https://github.com/bekencorp/bk_avdk_smp/blob/release/v4.0.1/ap/include/components/bk_platform.h)

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
- [UART](bk_uart.md)
- [USB](bk_usb.md)
- [Watchdog](bk_wdt.md)
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
