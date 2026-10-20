---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/usb/bk_usbh_uvc_uac.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="usb-host-uvc-uac"></a>

# USB Host UVC\+UAC

bk\_usbh\_hub\_multiple\_classes\_api是BK7259的 USB UVC \+ UAC 主机经过hub操作的程序，支持从 USB 设备读取/写入/控制多媒体流。当前最多同时支持 2 路摄像头 \+ 1 路麦克风 \+ 1 路播放器数据流。
具体的综合使用示例，请参考avdk多媒体代码，谢谢。

<a id="uvc-uac"></a>

## UVC \+ UAC的宏定义配置

CONFIG\_USB\=y 打开USB的总开关宏定义 使能USB的代码功能

CONFIG\_USB\_VBAT\_CONTROL\_GPIO\_ID\=0x1C 默认使用的GPIO是GPIO\_28进行USB Vbus电的控制，用户根据自己的实际情况进行配置

CONFIG\_CHERRY\_USB\=y 默认使用的CherryUSB的开源代码，用户可根据实际情况进行版本的更新

CONFIG\_USB\_HOST\=y 主程序作为HOST 对接口连接的设备进行枚举

CONFIG\_TASK\_USB\_PRIO\=2 USB的处理程序的TASK优先级配置为2

CONFIG\_USBH\_UVC\=y 打开UVC的Host驱动

CONFIG\_USBH\_UAC\=y 打开UAC的Host驱动

<a id="id1"></a>

## UVC/UAC 主机驱动基本使用流程

<a id="id2"></a>
![uvc start stop](../../../../../_assets/33723a5b80016edcd6c2-uvc_start_stop.png)


UVC start/stop

<a id="uvc"></a>

## UVC 示例参考代码

代码请参考ap/components/bk\_uvc/src/bk\_uvc.c

作为HOST 运行Video设备为例，注册connect/disconnect回调函数,投票对usb上电，如下图所示：

<a id="id3"></a>
![uvc connect disconnect](../../../../../_assets/405392bfac9ff472cebe-cli_uvc_connect_disconnect.png)


UVC Connect/Disconnect

投上电票后，可以查看是否已经上电完成枚举到了当前Port的设备，若没有则需要等待Connect回调函数的上报。如下图所示：

<a id="id4"></a>
![uvc get param](../../../../../_assets/b4ca862bc8a657d2e383-cli_uvc_get_param.png)


UVC Check Param

Connect回调上报时，将设备的枚举信息及解析也会上报上来，如下图所示：

<a id="id5"></a>
![uvc set param](../../../../../_assets/688cefce1f38571e53a7-cli_uvc_set_param.png)


UVC Connect callback

先查验，枚举信息里的参数是否复合要求，然后建立通道，最后将其打开。如下图所示：

<a id="id6"></a>
![uvc start](../../../../../_assets/362a638b71a83a2dd92c-cli_uvc_start.png)


UVC Start

打开UVC之后，进行数据传输。先申请urb，对urb进行赋值，然后再用urb进行数据传输，如下图所示：

<a id="id7"></a>
![uvc start](../../../../../_assets/543d2205e31b0ff982c0-cli_uvc_trans.png)


UVC Data Trans

使用完成之后，进行UVC关闭，然后再对内存进行释放，如下图所示：

<a id="id8"></a>
![uvc stop](../../../../../_assets/7966e8e04d0159f13194-cli_uvc_stop.png)


UVC Stop

<a id="uac"></a>

## UAC 主机驱动使用代码示例

代码请参考ap/components/bk\_audio/audio\_stream/uac\_mic\_stream.c
代码请参考ap/components/bk\_audio/audio\_stream/uac\_speaker\_stream.c
