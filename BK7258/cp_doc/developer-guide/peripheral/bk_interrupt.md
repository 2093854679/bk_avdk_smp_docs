---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_interrupt.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="icu-interrupt-control-unit"></a>

# ICU (Interrupt Control Unit)

为了兼容不同的CPU架构，设计了中断管理的核心模块为ICU，源码位于middleware/driver/icu/interrupt\_base.c ，
在ICU中设置了一张map表，用来记录当前所有的外部中断的信息，如中断号、默认优先级等等。

<a id="id1"></a>
![ICU map](../../../../../_assets/8f9df2db5a6452d18e9e-icu_map.png)


ICU map

同时提供了如下API供应用层使用：

```
bk_err_t bk_int_isr_register(icu_int_src_t src, int_group_isr_t isr_callback, void*arg) 使能某个中断，配置为ICU_DEV_MAP中的优先级，并注册回调函数
bk_err_t bk_int_set_priority(icu_int_src_t int_src, uint32_t int_priority) 设置某个中断的优先级
bk_err_t bk_int_isr_unregister(icu_int_src_t src) 关闭某个中断
```

设置中断优先级方法：

> - 编译固件前重新配置icu map表中相关中断的优先级；
> - 在运行过程中调用函数bk\_int\_set\_priority()进行设置。

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
- [TRNG](bk_trng.md)
- [SARADC](bk_adc.md)
- [SPI](bk_spi.md)
- [UART](bk_uart.md)
- [WDT](bk_wdt.md)
- [I2S](bk_i2s.md)
- [GPIO](bk_gpio.md)
- [RTC](bk_rtc.md)
- [OTP](bk_otp.md)
- [FLASH](bk_flash.md)
- [EFUSE](bk_efuse.md)
- [PSRAM](bk_psram.md)
- [TIMER](bk_timer.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [OS 相关参考](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
