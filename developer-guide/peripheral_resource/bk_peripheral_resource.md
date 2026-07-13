# 外设资源介绍



## 概述

`bk_avdk_smp` 提供 AP 与 CP 两个独立子系统。本文介绍各子系统上 **SDK 驱动/API 层面** 的外设归属与使用约束，并非硬件完全隔离；最终以工程 `menuconfig`、`usr_gpio_cfg.h` 及 defconfig 为准。

职责边界与 log 路径见 [AP(SMP)+CP 架构](../architecture.md "../architecture.md")。多媒体（ISP/GPU/DPU/VPU 等）主要在 AP 侧，详见 AP 文档多媒体章节。


## 1 CP 侧支持的外设资源

| NAME | 说明 | 参考 |
| --- | --- | --- |
| UART0 | 系统 log 串口；AP log 经 Mailbox 转发后由此输出 | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_uart.html](../../cp_doc/developer-guide/peripheral/bk_uart.md "../../cp_doc/developer-guide/peripheral/bk_uart.md") |
| WDT | **AON WDT** （系统级复位，CP 配置/喂狗）；**WWDT** （各核 NMI）；**task_wdt** | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_wdt.html](../../cp_doc/developer-guide/peripheral/bk_wdt.md "../../cp_doc/developer-guide/peripheral/bk_wdt.md") |
| RTC | 完整 RTC 能力：读/写、闹钟注册与管理 | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_rtc.html](../../cp_doc/developer-guide/peripheral/bk_rtc.md "../../cp_doc/developer-guide/peripheral/bk_rtc.md") |
| Timer | ``` TIMER_ID0``~``TIMER_ID11 ``` （12 通道，4 个 Timer group） | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_timer.html](../../cp_doc/developer-guide/peripheral/bk_timer.md "../../cp_doc/developer-guide/peripheral/bk_timer.md") |
| DMA | 逻辑通道由 `CONFIG_DMA_LOGIC_CHAN_CNT` / `CONFIG_DMA_LOGIC_CHAN_ID_MIN` 划分；SDK 默认 **0~3** | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_dma.html](../../cp_doc/developer-guide/peripheral/bk_dma.md "../../cp_doc/developer-guide/peripheral/bk_dma.md") |
| Mailbox / IPI | 与 AP 协同、心跳、log/CLI 转发 | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/api-reference/system/logic_mailbox.html](../../cp_doc/api-reference/system/logic_mailbox.md "../../cp_doc/api-reference/system/logic_mailbox.md") |
| OTP1 | OTP1 区域 | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_otp.html](../../cp_doc/developer-guide/peripheral/bk_otp.md "../../cp_doc/developer-guide/peripheral/bk_otp.md") |
| FLASH | 可直接操作 Flash 媒介 | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_flash.html](../../cp_doc/developer-guide/peripheral/bk_flash.md "../../cp_doc/developer-guide/peripheral/bk_flash.md") |
| EFUSE | EFUSE 配置 | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_efuse.html](../../cp_doc/developer-guide/peripheral/bk_efuse.md "../../cp_doc/developer-guide/peripheral/bk_efuse.md") |
| TRNG | 真随机数 | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_trng.html](../../cp_doc/developer-guide/peripheral/bk_trng.md "../../cp_doc/developer-guide/peripheral/bk_trng.md") |
| GPIO | **默认** GPIO10~11 用于 UART0 log；低功耗场景可能占用更多 GPIO | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_gpio.html](../../cp_doc/developer-guide/peripheral/bk_gpio.md "../../cp_doc/developer-guide/peripheral/bk_gpio.md") |
| PSRAM | 适合动态申请后及时释放（如动态 log）；不宜放长期 task/queue | [../../../../../../cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_psram.html](../../cp_doc/developer-guide/peripheral/bk_psram.md "../../cp_doc/developer-guide/peripheral/bk_psram.md") |

重要

GPIO 默认分工可通过 `usr_gpio_cfg.h` 调整。Wi-Fi / BLE 连接栈运行在 CP，见架构文档 CP 子系统章节。


## 2 AP 侧支持的外设资源

| NAME | 说明 | 参考 |
| --- | --- | --- |
| UART1~2 | 应用侧串口；架构上 UART0 由 CP 独占用于系统 log | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_uart.html](../../ap_doc/developer-guide/peripheral/bk_uart.md "../../ap_doc/developer-guide/peripheral/bk_uart.md") |
| WDT | 无 AON_WDT 驱动封装；`bk_reboot` 经 Mailbox 通知 CP 并触发 AON 复位；本侧另有 WWDT / task_wdt | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_wdt.html](../../ap_doc/developer-guide/peripheral/bk_wdt.md "../../ap_doc/developer-guide/peripheral/bk_wdt.md") |
| RTC | 读 tick / `gettimeofday`、可 `settimeofday`；闹钟管理在 CP | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_rtc.html](../../ap_doc/developer-guide/peripheral/bk_rtc.md "../../ap_doc/developer-guide/peripheral/bk_rtc.md") |
| Timer | ``` TIMER_ID12``~``TIMER_ID17 ``` （6 通道，2 个 Timer group） | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_timer.html](../../ap_doc/developer-guide/peripheral/bk_timer.md "../../ap_doc/developer-guide/peripheral/bk_timer.md") |
| DMA | 逻辑通道由 `CONFIG_DMA_LOGIC_CHAN_*` 划分；SDK 默认 **4~7** （多媒体工程可能不同） | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_dma.html](../../ap_doc/developer-guide/peripheral/bk_dma.md "../../ap_doc/developer-guide/peripheral/bk_dma.md") |
| HPDMA | 高速 DMA | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_hpdma.html](../../ap_doc/developer-guide/peripheral/bk_hpdma.md "../../ap_doc/developer-guide/peripheral/bk_hpdma.md") |
| OTP2 | OTP2 客户可用区域 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_otp.html](../../ap_doc/developer-guide/peripheral/bk_otp.md "../../ap_doc/developer-guide/peripheral/bk_otp.md") |
| FLASH | 经 Mailbox 与 CP 协同操作 Flash | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_flash.html](../../ap_doc/developer-guide/peripheral/bk_flash.md "../../ap_doc/developer-guide/peripheral/bk_flash.md") |
| TRNG | 真随机数 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_trng.html](../../ap_doc/developer-guide/peripheral/bk_trng.md "../../ap_doc/developer-guide/peripheral/bk_trng.md") |
| GPIO | 除 CP 默认占用的 GPIO10~11 外，其余 GPIO 由 AP 工程配置 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_gpio.html](../../ap_doc/developer-guide/peripheral/bk_gpio.md "../../ap_doc/developer-guide/peripheral/bk_gpio.md") |
| PSRAM | 多媒体与大 buffer 主承载区 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_psram.html](../../ap_doc/developer-guide/peripheral/bk_psram.md "../../ap_doc/developer-guide/peripheral/bk_psram.md") |
| I2S | 音频 I2S | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_i2s.html](../../ap_doc/developer-guide/peripheral/bk_i2s.md "../../ap_doc/developer-guide/peripheral/bk_i2s.md") |
| SPI | SPI 控制器 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_spi.html](../../ap_doc/developer-guide/peripheral/bk_spi.md "../../ap_doc/developer-guide/peripheral/bk_spi.md") |
| QSPI | QSPI 控制器 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_qspi.html](../../ap_doc/developer-guide/peripheral/bk_qspi.md "../../ap_doc/developer-guide/peripheral/bk_qspi.md") |
| SDIO | SDIO 接口 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_sdio.html](../../ap_doc/examples/peripheral/bk_sdio.md "../../ap_doc/examples/peripheral/bk_sdio.md") |
| USB | USB 控制器 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_usb.html](../../ap_doc/developer-guide/peripheral/bk_usb.md "../../ap_doc/developer-guide/peripheral/bk_usb.md") |
| CAN | CAN 控制器 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_can.html](../../ap_doc/developer-guide/peripheral/bk_can.md "../../ap_doc/developer-guide/peripheral/bk_can.md") |
| TE200 | TrustEngine 安全加速 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/security/mbedtls_and_trustengine.html](../../ap_doc/developer-guide/security/mbedtls_and_trustengine.md "../../ap_doc/developer-guide/security/mbedtls_and_trustengine.md") |
| PWM | PWM 控制器 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_pwm.html](../../ap_doc/developer-guide/peripheral/bk_pwm.md "../../ap_doc/developer-guide/peripheral/bk_pwm.md") |
| KEY | 按键输入 （基于 GPIO） | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_gpio.html](../../ap_doc/developer-guide/peripheral/bk_gpio.md "../../ap_doc/developer-guide/peripheral/bk_gpio.md") |
| I2C | I2C 控制器 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_i2c.html](../../ap_doc/developer-guide/peripheral/bk_i2c.md "../../ap_doc/developer-guide/peripheral/bk_i2c.md") |
| ADC | ADC 采样 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_adc.html](../../ap_doc/developer-guide/peripheral/bk_adc.md "../../ap_doc/developer-guide/peripheral/bk_adc.md") |
| Mailbox / IPI / HSPL | 与 CP 协同、核间通信与资源互斥 | [../../../../../../ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_mailbox.html](../../ap_doc/developer-guide/peripheral/bk_mailbox.md "../../ap_doc/developer-guide/peripheral/bk_mailbox.md") |

重要

AP SMP 下各核共享外设与内存；具体中断路由见 [中断管理](../interrupt/bk_interrupt.md "../interrupt/bk_interrupt.md")。
