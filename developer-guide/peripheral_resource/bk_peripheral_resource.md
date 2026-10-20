---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral_resource/bk_peripheral_resource.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 外设资源介绍

<a id="id2"></a>

## 概述

`bk_avdk_smp` 提供 AP 与 CP 两个独立子系统。本文介绍各子系统上 **SDK 驱动/API 层面** 的外设归属与使用约束，并非硬件完全隔离；最终以工程 `menuconfig`、`usr_gpio_cfg.h` 及 defconfig 为准。

职责边界与 log 路径见 [AP(SMP)\+CP 架构](../architecture.md)。多媒体（ISP/GPU/DPU/VPU 等）主要在 AP 侧，详见 AP 文档多媒体章节。

<a id="cp"></a>

## 1 CP 侧支持的外设资源

| NAME | 说明 | 参考 |
| --- | --- | --- |
| UART0 | 系统 log 串口；AP log 经 Mailbox 转发后由此输出 | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_uart.html](../../cp_doc/developer-guide/peripheral/bk_uart.md) |
| WDT | **AON WDT** （系统级复位，CP 配置/喂狗）；**WWDT** （各核 NMI）；**task\_wdt** | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_wdt.html](../../cp_doc/developer-guide/peripheral/bk_wdt.md) |
| RTC | 完整 RTC 能力：读/写、闹钟注册与管理 | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_rtc.html](../../cp_doc/developer-guide/peripheral/bk_rtc.md) |
| Timer | ``` TIMER_ID0``~``TIMER_ID11 ``` （12 通道，4 个 Timer group） | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_timer.html](../../cp_doc/developer-guide/peripheral/bk_timer.md) |
| DMA | 逻辑通道由 `CONFIG_DMA_LOGIC_CHAN_CNT` / `CONFIG_DMA_LOGIC_CHAN_ID_MIN` 划分；SDK 默认 **0\~3** | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_dma.html](../../cp_doc/developer-guide/peripheral/bk_dma.md) |
| Mailbox / IPI | 与 AP 协同、心跳、log/CLI 转发 | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/api-reference/system/logic\_mailbox.html](../../cp_doc/api-reference/system/logic_mailbox.md) |
| OTP1 | OTP1 区域 | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_otp.html](../../cp_doc/developer-guide/peripheral/bk_otp.md) |
| FLASH | 可直接操作 Flash 媒介 | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_flash.html](../../cp_doc/developer-guide/peripheral/bk_flash.md) |
| EFUSE | EFUSE 配置 | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_efuse.html](../../cp_doc/developer-guide/peripheral/bk_efuse.md) |
| TRNG | 真随机数 | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_trng.html](../../cp_doc/developer-guide/peripheral/bk_trng.md) |
| GPIO | **默认** GPIO10\~11 用于 UART0 log；低功耗场景可能占用更多 GPIO | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_gpio.html](../../cp_doc/developer-guide/peripheral/bk_gpio.md) |
| PSRAM | 适合动态申请后及时释放（如动态 log）；不宜放长期 task/queue | [../../../../../../cp\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_psram.html](../../cp_doc/developer-guide/peripheral/bk_psram.md) |

重要

GPIO 默认分工可通过 `usr_gpio_cfg.h` 调整。Wi-Fi / BLE 连接栈运行在 CP，见架构文档 CP 子系统章节。

<a id="ap"></a>

## 2 AP 侧支持的外设资源

| NAME | 说明 | 参考 |
| --- | --- | --- |
| UART1\~2 | 应用侧串口；架构上 UART0 由 CP 独占用于系统 log | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_uart.html](../../ap_doc/developer-guide/peripheral/bk_uart.md) |
| WDT | 无 AON\_WDT 驱动封装；`bk_reboot` 经 Mailbox 通知 CP 并触发 AON 复位；本侧另有 WWDT / task\_wdt | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_wdt.html](../../ap_doc/developer-guide/peripheral/bk_wdt.md) |
| RTC | 读 tick / `gettimeofday`、可 `settimeofday`；闹钟管理在 CP | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_rtc.html](../../ap_doc/developer-guide/peripheral/bk_rtc.md) |
| Timer | ``` TIMER_ID12``~``TIMER_ID17 ``` （6 通道，2 个 Timer group） | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_timer.html](../../ap_doc/developer-guide/peripheral/bk_timer.md) |
| DMA | 逻辑通道由 `CONFIG_DMA_LOGIC_CHAN_*` 划分；SDK 默认 **4\~7** （多媒体工程可能不同） | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_dma.html](../../ap_doc/developer-guide/peripheral/bk_dma.md) |
| HPDMA | 高速 DMA | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_hpdma.html](../../ap_doc/developer-guide/peripheral/bk_hpdma.md) |
| OTP2 | OTP2 客户可用区域 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_otp.html](../../ap_doc/developer-guide/peripheral/bk_otp.md) |
| FLASH | 经 Mailbox 与 CP 协同操作 Flash | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_flash.html](../../ap_doc/developer-guide/peripheral/bk_flash.md) |
| TRNG | 真随机数 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_trng.html](../../ap_doc/developer-guide/peripheral/bk_trng.md) |
| GPIO | 除 CP 默认占用的 GPIO10\~11 外，其余 GPIO 由 AP 工程配置 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_gpio.html](../../ap_doc/developer-guide/peripheral/bk_gpio.md) |
| PSRAM | 多媒体与大 buffer 主承载区 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_psram.html](../../ap_doc/developer-guide/peripheral/bk_psram.md) |
| I2S | 音频 I2S | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_i2s.html](../../ap_doc/developer-guide/peripheral/bk_i2s.md) |
| SPI | SPI 控制器 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_spi.html](../../ap_doc/developer-guide/peripheral/bk_spi.md) |
| QSPI | QSPI 控制器（Flash / PSRAM / LCD） | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_qspi.html](../../ap_doc/developer-guide/peripheral/bk_qspi.md) |
| QSPI Flash | 外挂 NOR / SPI-NAND Flash | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_qspi\_flash.html](../../ap_doc/developer-guide/peripheral/bk_qspi_flash.md) |
| SDIO | SDIO 接口 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/examples/peripheral/bk\_sdio.html](../../ap_doc/examples/peripheral/bk_sdio.md) |
| USB | USB 控制器 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_usb.html](../../ap_doc/developer-guide/peripheral/bk_usb.md) |
| CAN | CAN 控制器 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_can.html](../../ap_doc/developer-guide/peripheral/bk_can.md) |
| TE200 | TrustEngine 安全加速 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/security/mbedtls\_and\_trustengine.html](../../ap_doc/developer-guide/security/mbedtls_and_trustengine.md) |
| PWM | PWM 控制器 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_pwm.html](../../ap_doc/developer-guide/peripheral/bk_pwm.md) |
| KEY | 按键输入 （基于 GPIO） | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_gpio.html](../../ap_doc/developer-guide/peripheral/bk_gpio.md) |
| I2C | I2C 控制器 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_i2c.html](../../ap_doc/developer-guide/peripheral/bk_i2c.md) |
| ADC | ADC 采样 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_adc.html](../../ap_doc/developer-guide/peripheral/bk_adc.md) |
| Mailbox / IPI / HSPL | 与 CP 协同、核间通信与资源互斥 | [../../../../../../ap\_doc/bk7259/zh\_CN/v4.0.1/developer-guide/peripheral/bk\_mailbox.html](../../ap_doc/developer-guide/peripheral/bk_mailbox.md) |

重要

AP SMP 下各核共享外设与内存；具体中断路由见 [中断管理](../interrupt/bk_interrupt.md)。
