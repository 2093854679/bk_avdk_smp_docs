---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_adc.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="saradc"></a>

# SARADC

<a id="id1"></a>

## 概述

BK7259 使用 SARADC V1.2。

<a id="id2"></a>

## 工作模式

BK7259 SARADC V1.2 硬件支持以下两种模式：

> - 单步模式（`ADC_SINGLE_STEP_MODE`）：硬件 `adc_mode` 为 0。
> - 连续模式（`ADC_CONTINUOUS_MODE`）：硬件 `adc_mode` 为 1。

公共类型中保留的 `ADC_SLEEP_MODE` 和 `ADC_SOFTWARE_CONTRL_MODE` 是兼容枚举，
BK7259 V1.2 HAL 不会将这两种枚举写入硬件模式寄存器，不应作为 BK7259
可用的硬件工作模式使用。

<a id="id3"></a>

## 连续采样与中断

连续模式的数据处理流程如下：

> 1. 驱动选择通道、配置时钟并启动转换。
> 2. 采样结果进入硬件 FIFO。
> 3. FIFO 数据量达到中断条件后产生中断。
> 4. 中断服务程序逐个读取 FIFO 数据并写入用户请求的 `uint16_t` 缓冲区。
> 5. 收集到请求的样本数后，驱动停止转换并唤醒等待任务。

BK7259 V1.2 驱动将 FIFO 中断阈值限制为 32。该阈值表示 FIFO 的中断触发条件，
不是 FIFO 容量，也不是用户读取缓冲区的大小。单步模式固定在采集两个数据后
产生中断。

`bk_adc_channel_read()` 默认采集 32 个样本，并对后半部分样本求平均值；
`bk_adc_channel_raw_read()` 返回用户指定数量的原始采样结果。兼容接口
`bk_adc_read()` 和 `bk_adc_read_raw()` 最终使用当前选中的通道执行相应读取。

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
