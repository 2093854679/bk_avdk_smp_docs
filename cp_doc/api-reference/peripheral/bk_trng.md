---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_trng.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rng"></a>

# 随机数 (RNG)

BK7259 已移除独立 TRNG 外设驱动（`bk_trng_*` 不再提供）。CP 侧随机数统一通过
`bk_rand()` 与 `bk_fill_rand()` 获取，定义于 `components/bk_platform.h`。

详细说明见 [RNG 开发指南](../../developer-guide/peripheral/bk_trng.md)。

<a id="rng-api-reference"></a>

## RNG API Reference

<a id="c.bk_rand"></a>

int bk\_rand(void)
:   获取一个 32 位随机整数。

<a id="c.bk_fill_rand"></a>

int bk\_fill\_rand(void \*buff, size\_t len)
:   向缓冲区填充 `len` 字节随机数据。

    参数
    :   - **buff** – 输出缓冲区指针
        - **len** – 待填充字节数

    返回
    :   成功返回 `0`；参数无效时返回 `-1`

<a id="id1"></a>

## 头文件

- `components/bk_platform.h`

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
- [SARADC](bk_adc.md)
- [UART](bk_uart.md)
- [Watchdog](bk_wdt.md)
- [I2S](bk_i2s.md)
- [GPIO](bk_gpio.md)
- [HSPL](bk_hspl.md)
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
