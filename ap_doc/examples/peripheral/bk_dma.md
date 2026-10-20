---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_dma.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="dma"></a>

# DMA

<a id="dmaapi"></a>

## 1 基本DMA使用API调用流程及解析

基本流程为：初始化，配置，启动，等待中断，停止，如下图所示

<a id="id1"></a>
![Basic Process of DMA API](../../../../_assets/0bee304af1838beccce1-dma_api_basic_process.png)


Basic Process of DMA API

<a id="repeatefifosram"></a>

## 2 repeate模式从FIFO到SRAM的数据拷贝

Audio的FIFO和GDMA是相连的，可以进行源或目的地址的配置进行使用。

参考代码components/bk\_cli/cli\_aud.c，配置方法如下图所示配置：

<a id="id2"></a>
![dma api repeat mode](../../../../_assets/b58571dae364d2f3ac0d-dma_api_repeat_m.png)


DMA API Repeat Mode Config

参考代码components/bk\_cli/cli\_aud.c，配置方法如下图所示配置：

<a id="id3"></a>
![dma api repeat mode](../../../../_assets/abe599121bc4db1d62a1-dma_api_repeat_m_stop.png)


DMA API Repeat Mode Stop

备注

**Audio的FIFO和GDMA是相连的所以可以直接使用。若要确认使用的外设和FIFO是否与DMA相连，请查看dma\_reg.h**

<a id="singlesramsram"></a>

## 3 Single模式从SRAM到SRAM的数据拷贝

参考cli\_dma.c的dma\_chnl\_primenumber\_copy函数的实现。API的调用如下图所示：

<a id="id4"></a>
![dma api repeat mode](../../../../_assets/b26eb54d7991d9f7121f-dma_api_memcopy.png)


DMA API Single Mode

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [命令](../cli.md)
- [外设](../peripheral.md)
- [I2C](bk_i2c.md)
- [I3C](bk_i3c.md)
- [PWM](bk_pwm.md)
- [SDIO](bk_sdio.md)
- [SPI](bk_spi.md)
- [I2S](bk_i2s.md)
- [CAN](bk_can.md)
- [UART](bk_uart.md)
- [Watchdog](bk_wdt.md)
- [HPDMA](bk_hpdma.md)
- [QSPI](bk_qspi.md)
- [QSPI Flash](bk_qspi_flash.md)
- [TIMER](bk_timer.md)
- [RTC](bk_rtc.md)
- [OTP](bk_otp.md)
- [FLASH](bk_flash.md)
- [PSRAM](bk_psram.md)
- [GPIO](bk_gpio.md)
- [USB](bk_usb.md)
- [TOUCH](bk_touch.md)
- [IPI](bk_ipi.md)
- [IRDA](bk_irda.md)
- [HSPL](bk_hspl.md)
- [Calendar](bk_calendar.md)
- [平台](../platform.md)
- [项目示例](../projects.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
