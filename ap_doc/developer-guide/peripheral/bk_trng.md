---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_trng.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rng"></a>

# 随机数 (RNG) 使用指南

<a id="id1"></a>

## 概述

BK7259 已移除独立的 TRNG 外设驱动（`bk_trng_*` 系列 API 及 `driver/trng.h` 不再提供）。
系统随机数统一通过 `bk_rand()` 与 `bk_fill_rand()` 获取，定义于 `components/bk_platform.h`。

熵源由 PSA Mbed TLS 平台层在运行时选择，优先级如下：

1. TrustEngine TE200 硬件 TRNG（需开启 CONFIG\_TRUSTENGINE 与 CONFIG\_TE200\_ENTROPY）
2. OTP 随机数（CONFIG\_OTP\_V1，未启用 TrustEngine 时）
3. 软件 `rand()` 回退（`components/bk_system/bk_platform.c` 中的 weak 实现）

更多 TrustEngine / Mbed TLS 配置说明见 [Mbed TLS](../security/mbedtls_and_trustengine.md)。

<a id="id2"></a>

## 使用方法

获取 32 位随机整数:

```
#include <components/bk_platform.h>

int value = bk_rand();
```

填充缓冲区:

```
uint8_t buf[16];
if (bk_fill_rand(buf, sizeof(buf)) != 0) {
    /* buff 为 NULL 或 len 为 0 */
}
```

备注

启用 CONFIG\_PSA\_MBEDTLS 时，`bk_rand()` 与 `bk_fill_rand()` 由 PSA 平台层提供 strong 实现，覆盖 `bk_platform.c` 中的 weak 默认实现。系统启动后可直接调用，无需单独初始化 TRNG 外设。

<a id="id3"></a>

## 推荐配置

密码学或安全相关场景建议开启:

```
CONFIG_PSA_MBEDTLS=y
CONFIG_TRUSTENGINE=y
CONFIG_TE200_ENTROPY=y
```

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
- [HPDMA](bk_hpdma.md)
- [HSPL](bk_hspl.md)
- [IPI](bk_ipi.md)
- [ICU](bk_interrupt.md)
- [I3C](bk_i3c.md)
- [PWM](bk_pwm.md)
- [SARADC](bk_adc.md)
- [SPI](bk_spi.md)
- [QSPI](bk_qspi.md)
- [QSPI Flash](bk_qspi_flash.md)
- [QSPI 文件系统](bk_qspi_filesystem.md)
- [UART](bk_uart.md)
- [Watchdog](bk_wdt.md)
- [I2C](bk_i2c.md)
- [TOUCH](bk_touch.md)
- [USB](bk_usb.md)
- [I2S](bk_i2s.md)
- [GPIO](bk_gpio.md)
- [GSENSOR](bk_gsensor.md)
- [RTC](bk_rtc.md)
- [Calendar](bk_calendar.md)
- [CKMN](bk_ckmn.md)
- [OTP](bk_otp.md)
- [FLASH](bk_flash.md)
- [FLASH_PARTITION](bk_flash_partition.md)
- [EFUSE](bk_efuse.md)
- [PSRAM](bk_psram.md)
- [CAN](bk_can.md)
- [IRDA](bk_irda.md)
- [LIN](bk_lin.md)
- [Mailbox](bk_mailbox.md)
- [TIMER](bk_timer.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [CPU Hotplug](../cpu_hotplug.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [Bootloader与Ota](../bootloader_ota.md)
- [BK AT](../at.md)
- [多媒体](../multimedia.md)
- [显示](../display.md)
- [VPU](../vpu.md)
- [GPU](../gpu.md)
- [NPU](../npu.md)
- [音频](../audio.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [摄像头](../camera.md)
- [图像用户界面](../gui.md)
- [多媒体网络传输](../multimedia_network_transfer.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [项目示例](../../examples/projects.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
