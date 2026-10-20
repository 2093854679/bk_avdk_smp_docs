---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_usb.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="usb"></a>

# USB 使用指南

- [USB Host UVC\+UAC](usb/bk_usbh_uvc_uac.md)
- [USB Host Serial CH340](usb/bk_usbh_serial_ch340.md)
- [USB Host MSD](usb/bk_usbh_msd.md)
- [USB Device MSC](usb/bk_usbd_msc.md)

<a id="id1"></a>

## 概述

> 当前芯片支持的USB类型如下所示：

| USB类型 | 工作电压 | USB协议 | 设备协议 | 速度 | 编码协议 | 分辨率 | 端点\`wMaxPacketSize\` | 备注 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| UVC | 5.0v | USB 1.1/2.0 | UVC 1.5 | High/Full-Speed | MJPEG | 1280\*720 | 1024 | 不支持DRI字段 |
| UAC | 5.0v | USB 1.1/2.0 | UAC 1.0 | High/Full-Speed | ALL | N | 1024 |  |

<a id="id2"></a>

## USB 简介

USB（Universal Serial Bus）是一种通用的总线标准，用于连接主机和外设设备。USB 主机可以通过 USB 接口与 USB 设备连接，实现数据传输、电源供给等功能。

USB IF（USB Implementers Forum）是 USB 标准的制定者，它制定了 USB 标准，包括 USB 1.1、USB 2.0等，定义了 USB 接口的物理层、数据链路层、传输层、会话层、表示层等协议，以及 USB 设备类（Device Class）标准，常见的设备类包括 HID（Human Interface Device，人机接口设备）、MSC（Mass Storage Class，大容量存储设备）、CDC（Communication Device Class，通信设备）、Audio、Video 等。

博通BK7258芯片内置 USB 外设，支持各种各样的 USB 应用，包括 USB 多媒体类应用，USB 通信类应用，USB 存储类应用，USB 人机交互类应用等。

默认支持的驱动包括HUB、 UVC(USB Video Class)、UAC(USB Audio Class),其他类的驱动需要打开相应的宏开关进行编译加载。

<a id="id3"></a>

## USB 相关宏定义

CONFIG\_USB\=y 打开USB的总开关宏定义 使能USB的代码功能

CONFIG\_USB\_VBAT\_CONTROL\_GPIO\_ID\=0x1C 默认使用的GPIO是GPIO\_28进行USB Vbus电的控制，用户根据自己的实际情况进行配置

CONFIG\_CHERRY\_USB\=y 默认使用的CherryUSB的开源代码，用户可根据实际情况进行版本的更新

CONFIG\_USB\_HOST 主程序作为HOST 对连接上的设备进行设备枚举

CONFIG\_USB\_DEVICE 主程序作为DEVICE 连接到HOST被枚举

CONFIG\_TASK\_USB\_PRIO 设置USB Driver处理线程的优先级

CONFIG\_USB\_HUB\_MULTIPLE\_DEVICES 在Host模式下，支持HUB的驱动，以及支持HUB 统一接口的操作。注意最多支持1个HUB的连接

CONFIG\_USBHOST\_HUB\_MAX\_EHPORTS\=4 默认最多支持4个port 接口的HUB操作

CONFIG\_USBHOST\_HUB\_PORT\_SUPPORT\_MAX\_DEVICE\=5 默认每个接口支持5种class设备的连接

CONFIG\_USB\_UVC 支持USB Vidoe Class的HOST驱动

CONFIG\_USB\_UAC 支持USB Audio Class的HOST驱动

<a id="id4"></a>

## USB 基本使用

<a id="id6"></a>
![usb open close](../../../../../_assets/e1d86b14dc88cc3312ec-usb_open_close.png)


USB open

<a id="id5"></a>

## USB 测试示例

注：BK7258 USB 运行在AP侧， 测试目标：USB模块开关正常，枚举正常，解析正常，断开/连接等状态记录正常。

作为HOST 识别枚举U盘为例，输入命令和LOG信息如下图所示：

1、 系统默认启动了AP测，查看log如下

<a id="id7"></a>
![boot core1](../../../../../_assets/cd428e3bf2396bcc3c3a-cli_boot_cpu1.png)


AP Boot

2、默认串口输入cpu1 usb power 1c 1，log如下

<a id="id8"></a>
![usb power on](../../../../../_assets/0952c480d3d4b33c988f-cli_usb_power_on.png)


CLI USB PowerON

3、默认串口输入cpu1 usb open\_host，枚举成功log如下

<a id="id9"></a>
![usb open_host](../../../../../_assets/409dfa149ec24dcaa12d-cli_usb_open_host.png)


CLI USB Open Host

4、默认串口输入cpu1 usb close,log如下

<a id="id10"></a>
![usb open_host](../../../../../_assets/b8989656eb8475d635b2-cli_usb_check_support_dev.png)


CLI USB Close

5、默认串口输入cpu1 usb power 1c 0,log如下

<a id="id11"></a>
![usb open_host](../../../../../_assets/d7cec7c2e5af66d942cd-cli_usb_close.png)


CLI USB PowerDown

<a id="usb-hub-memory-size"></a>

## USB HUB 端口数量和设备枚举信息调整的memory size

若设备出现超过1024bytes的枚举信息，则需要对默认配置进行调整
使用hub时，需要根据设备情况对port 数据量进行配置

<a id="id12"></a>
![usb hub](../../../../../_assets/c210a57554f6b029452f-cli_usb_power_down.png)


USB HUB

<a id="usb-api"></a>

## USB API 链接

> [USB的驱动API](../../api-reference/peripheral/bk_usb.md)
