---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/usb/bk_usbh_serial_ch340.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="usb-host-serial-ch340"></a>

# USB Host Serial CH340

> BK7258的 USB HOST 可以加载CH340的驱动。打开USB驱动后，连接识别到CH340设备，相关宏开关在CPU0的config中打开。

<a id="usb-serial-ch340"></a>

## USB Serial ch340的宏定义配置

CONFIG\_USB\=y 打开USB的总开关宏定义 使能USB的代码功能

CONFIG\_USB\_VBAT\_CONTROL\_GPIO\_ID\=0x1C 默认使用的GPIO是GPIO\_28进行USB Vbus电的控制，用户根据自己的实际情况进行配置

CONFIG\_CHERRY\_USB\=y 默认使用的CherryUSB的开源代码，用户可根据实际情况进行版本的更新

CONFIG\_USB\_HOST\=y 主程序作为HOST 对接口连接的设备进行枚举

CONFIG\_TASK\_USB\_PRIO\=2 USB的处理程序的TASK优先级配置为2

CONFIG\_USBH\_SERIAL\_CH340\=y 打开Serial ch340驱动的编译，能够做到打开USB后自动识别 CH340串口

<a id="serial-ch340-cli"></a>

## Serial ch340 主机驱动CLI测试示例

参考代码在cli\_usb.c中，API的调用及示例请参考由CONFIG\_USBH\_SERIAL\_CH340宏范围的code。
集合使用的demo，参考cli\_simulate\_uart\_demo init/deinit操作。

注册回调函数，设备连接成功后上报回调函数cli示例：
:   输入命令：
    usbh\_to\_uart reg\_cb 0 注册回调函数
    usbh\_to\_uart unreg\_cb 0 注销回调函数

<a id="id2"></a>
![cb init deinit](../../../../../../_assets/eb22987f88232dd82e38-usbh_serial_ch340_callback_init_deinit.png)


Serial CH340 Register callback

打开USB驱动对CH340 串口打开进行枚举：
:   输入命令：
    usbh\_to\_uart init 0

<a id="id3"></a>
![open USB for enumeration](../../../../../../_assets/4a229ccee65a93510d3f-usbh_serial_ch340_enumeration.png)


USB HOST for enumeration

关闭CH340的驱动，先触发断开中断，然后再关闭USB驱动:
:   usbh\_to\_uart deinit 0

<a id="id4"></a>
![mount_udisk](../../../../../../_assets/b314d4d396e88bc10275-usbh_serial_ch340_deinit.png)


USB HOST CH340 Driver Deinit

调用接口发送数据,log中显示发送成功后的回调函数。测试命令如下:
:   > usbh\_to\_uart write 0 128 100

    id:0 cnt:128 bytes timeout\_ms:100ms

<a id="id5"></a>
![send data](../../../../../../_assets/993515476fd117bbadcd-usbh_serial_ch340_send.png)


Send Data

调用接口接收数据,接收到数据后，触发回调函数。测试命令如下:
:   > usbh\_to\_uart read 0 32 1000

    id:0 cnt:32 bytes timeout\_ms:1000ms

<a id="id6"></a>
![receive data](../../../../../../_assets/799ab9d0d44a8c43e8d7-usbh_serial_ch340_receive.png)


Receive Data

<a id="api"></a>

## 基本API 调用流程图

<a id="id7"></a>
![flow](../../../../../../_assets/175f11066422ff43c028-usbh_serial_ch340_flow.png)


Flow chart

注:
1.回调函数注册是一次性将tx、rx、connect、disconnect回调函数都注册。

2.初始化的配置，除了波特率后续都不能更改。

3.发送数据，timeout大于0时，表示将一致等待数据发送直到结束。timeout等于0时，将把数据拷贝到fifo中，再发送，注意返回值错误时可能fifo不足。

4.接收数据时，可通过rx回调函数通知后再读出数据。或使用timeout等待数据的接收。

5.2种方式检测是否连接成功，①connect回调函数上报，②check检测是否有设备连接。

6.关闭时，将先上报disconnect，在对USB驱动进行关闭。

<a id="id1"></a>

## USB HOST Serial CH340

> 更多详细开发可参考CherryUSB相关文档， <https://github.com/cherry-embedded/CherryUSB/blob/master/README_zh.md>
