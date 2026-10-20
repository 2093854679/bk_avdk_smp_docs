---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/usb/bk_usbd_msc.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="usb-host-msd"></a>

# USB Host MSD

> BK7259的 USB Device MSC 默认是识别和使用SDcard或SDNAND，所以若使用U盘功能需要将SDcard的驱动相关宏也需要打开。

<a id="usb-device-msc"></a>

## USB Device MSC的宏定义配置

CONFIG\_USB\=y 打开USB的总开关宏定义 使能USB的代码功能

CONFIG\_USB\_VBAT\_CONTROL\_GPIO\_ID\=0x1C 默认使用的GPIO是GPIO\_28进行USB Vbus电的控制，用户根据自己的实际情况进行配置

CONFIG\_CHERRY\_USB\=y 默认使用的CherryUSB的开源代码，用户可根据实际情况进行版本的更新

CONFIG\_USB\_HOST\=n 主程序作为DEVICE 连接到HOST被枚举到为U盘
CONFIG\_USB\_DEVICE\=y

CONFIG\_USBD\_MSC\=y 打开MSC驱动的编译，作为U盘被HOST识别到

<a id="msd-cli"></a>

## MSD 主机驱动CLI测试示例

注：作为DEVICE，若需要使用U盘功能时，才将驱动初始化。若需要U盘功能实时待命识别，请将驱动在main函数中初始化

打开USB U盘驱动，被PC识别到：
:   输入命令：usbd msc\_init 初始化U盘驱动

<a id="id2"></a>
![USBD msc init](../../../../../_assets/3d71ed6eb17ba99af00c-usbd_msc_init.png)


USB DEVICE UDISK INIT

> 输入命令：usbd msc\_deinit 卸载U盘驱动

<a id="id3"></a>
![USBD msc uninit](../../../../../_assets/bd6aabb7a6b10d5eef87-usbd_msc_uninit.png)


USB DEVICE UDISK UNINIT

<a id="id1"></a>

## USB DEVICE MSC

> 更多详细开发可参考CherryUSB相关文档， <https://github.com/cherry-embedded/CherryUSB/blob/master/README_zh.md>

## 模块导航

- [简介](../../../introduction.md)
- [H/W 参考手册](../../../hw-reference.md)
- [API 参考手册](../../../api-reference.md)
- [开发者指南](../../../developer-guide.md)
- [软件架构与分层](../../architecture.md)
- [系统安全](../../security.md)
- [低功耗与电源管理](../../power_save.md)
- [设备管理框架](../../driver_model.md)
- [外设与驱动](../../peripheral.md)
- [DMA](../bk_dma.md)
- [HPDMA](../bk_hpdma.md)
- [HSPL](../bk_hspl.md)
- [IPI](../bk_ipi.md)
- [ICU](../bk_interrupt.md)
- [I3C](../bk_i3c.md)
- [PWM](../bk_pwm.md)
- [TRNG](../bk_trng.md)
- [SARADC](../bk_adc.md)
- [SPI](../bk_spi.md)
- [QSPI](../bk_qspi.md)
- [QSPI Flash](../bk_qspi_flash.md)
- [QSPI 文件系统](../bk_qspi_filesystem.md)
- [UART](../bk_uart.md)
- [Watchdog](../bk_wdt.md)
- [I2C](../bk_i2c.md)
- [TOUCH](../bk_touch.md)
- [USB](../bk_usb.md)
- [USB Host UVC+UAC](bk_usbh_uvc_uac.md)
- [USB Host Serial CH340](bk_usbh_serial_ch340.md)
- [USB Host MSD](bk_usbh_msd.md)
- [概述](../bk_usb.md)
- [USB 简介](../bk_usb.md)
- [USB 相关宏定义](../bk_usb.md)
- [USB 基本使用](../bk_usb.md)
- [USB 测试示例](../bk_usb.md)
- [USB HUB 端口数量和设备枚举信息调整的memory size](../bk_usb.md)
- [USB API 链接](../bk_usb.md)
- [I2S](../bk_i2s.md)
- [GPIO](../bk_gpio.md)
- [GSENSOR](../bk_gsensor.md)
- [RTC](../bk_rtc.md)
- [Calendar](../bk_calendar.md)
- [CKMN](../bk_ckmn.md)
- [OTP](../bk_otp.md)
- [FLASH](../bk_flash.md)
- [FLASH_PARTITION](../bk_flash_partition.md)
- [EFUSE](../bk_efuse.md)
- [PSRAM](../bk_psram.md)
- [CAN](../bk_can.md)
- [IRDA](../bk_irda.md)
- [LIN](../bk_lin.md)
- [Mailbox](../bk_mailbox.md)
- [TIMER](../bk_timer.md)
- [出错与日志](../../error_log.md)
- [系统调试](../../debug_trace.md)
- [CPU Hotplug](../../cpu_hotplug.md)
- [Wi-Fi](../../wifi.md)
- [Bluetooth](../../bluetooth.md)
- [HTTP](../../http.md)
- [Bootloader与Ota](../../bootloader_ota.md)
- [BK AT](../../at.md)
- [多媒体](../../multimedia.md)
- [显示](../../display.md)
- [VPU](../../vpu.md)
- [GPU](../../gpu.md)
- [NPU](../../npu.md)
- [音频](../../audio.md)
- [用例编写](../../examples.md)
- [文档系统](../../documentation.md)
- [摄像头](../../camera.md)
- [图像用户界面](../../gui.md)
- [多媒体网络传输](../../multimedia_network_transfer.md)
- [操作系统与内存管理](../../../os.md)
- [样例演示](../../../examples.md)
- [项目示例](../../../examples/projects.md)
- [应用开发](../../../application.md)
- [开发与贡献代码流程](../../../process.md)
- [云平台](../../../cloud.md)
- [常见问题](../../../FAQ.md)
- [支持的外设](../../../support_peripherals.md)
