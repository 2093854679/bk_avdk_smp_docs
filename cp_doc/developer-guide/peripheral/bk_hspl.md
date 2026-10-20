---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_hspl.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="hspl"></a>

# HSPL 使用指南

<a id="id1"></a>

## 概述

HSPL（Hardware Spin Lock）是 BK7259 提供的硬件自旋锁，用于多核之间的互斥同步。芯片提供两个 HSPL 硬件实例，每个实例 16 个独立通道。

主要特性：

> - 双实例：BK\_HSPL\_ID\_0（基址 0x45010000，CP/AP 跨核互斥）、BK\_HSPL\_ID\_1（基址 0x480C0000，AP SMP 内部互斥）
> - 每实例 16 路通道，硬件原子加锁/解锁
> - 提供底层 channel API 与上层资源级 `bk_hspl_res_*` 封装

备注

CP 侧 `bk_hspl_res_*` 资源锁请使用 BK\_HSPL\_ID\_0；在 CP 上调用 BK\_HSPL\_ID\_1 相关路径可能返回 `BK_ERR_NOT_SUPPORT`。

<a id="id2"></a>

## 驱动初始化

```
bk_hspl_driver_init();
/* 使用 bk_hspl_try_lock / bk_hspl_res_lock 等接口 */
bk_hspl_driver_deinit();
```

<a id="id3"></a>

## 相关代码路径

> - 驱动头文件：`middleware/driver/hspl/hspl_driver.h`、`hspl_res_lock.h`
> - 驱动实现：`middleware/driver/hspl/hspl_driver.c`、`hspl_res_lock.c`
> - 测试代码：`middleware/driver/hspl/hspl_test.c`
> - Kconfig：middleware/driver/hspl/Kconfig（CONFIG\_HSPL、CONFIG\_HSPL\_TEST）

<a id="api"></a>

## API 参考

详见 [HSPL](../../api-reference/peripheral/bk_hspl.md)。

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
