---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/at/bk_at_brief.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bk-idk-at"></a>

# **BK IDK AT 简介**

<a id="id1"></a>

## **简介**

BK AT是博通集成公司开发的一个BK IDK的AT命令交互的组件，该组件最主要的目标在于降低客户的开发、学习和测试成本，方便客户快速上手、并形成版本，提高测试效率，方便形成高效稳定的自动化测试环境。通过BK AT指令，用户可以控制芯片实现不同的功能，如快速连接至Wi-Fi网络、开启蓝牙功能、实现大吞吐数据通信等功能，更加方便快捷的实现无线使生活更美好的愿景，加速万物互联的实现。

从实现的角度上，BK AT是BK IDK中的一部分，使用AT的宏控制。当打开AT的宏时，用户可以通过BK AT的接口，控制整个模组，可以将模组作为用户主机的外部扩展，来丰富用户自身主机的功能，即用户的主机作为主控设备，将想要发送的AT命令通过预先设定的 I/O 接口发送到模组即可，主机只需要接收模组返回的AT响应与AT消息，即可实现各种各样的通信与多媒体功能。同样，用户也可以通过PC对BK AT模组进行二次开发，开发自己的AT命令，来实现不同的功能。

BK AT并不要求用户主机的性能，用户可以通过配置AT每次接收的数据大小来实现不同性能主机的沟通。

BK AT指令以“AT”作为字符串的开头，并以回车换行(‘\\r\\n’)作为输入结尾，其中间的字符串为“AT指令”，其每条输入的命令 都代表一定的功能，BK AT在收到这样的指令之后，对于运行结果，会返回给客户“OK”或着“ERROR”提示，对于当前正在执行当中收到的新的AT命令，则会返回“BUSY”。

BK AT提供较为基础的AT命令集合，用户可以直接使用这些命令进行开发，当然，AT也支持用户自行开发适合自己的AT命令，以满足不同的开发需求，对于如何自行创建AT命令并注册，请参见入门指南。

在一般情况下，BK AT选择 UART 作为与外部MCU/PC设备交互的I/O接口，当然，BK AT同样支持您对于不同I/O接口选择的需求， 您可以根据您设备的具体情况，选择其他的通信接口，如SDIO、SPI等。另外，您在使用UART作为I/O端口时，BK AT同样支持自定义 AT端口设定(BK AT默认的AT端口为UART0)，关于具体的修改方式，请参见入门指南。

BK AT主要特性包括：

- 提供丰富的内部AT命令
- 方便用户独立AT命令创建空间，完成用户第三方AT命令创建
- 无需感知复杂的内部函数接口，仅需AT命令完成功能搭建
- 支持博通集成所有IDK的产品
- 支持多种I/O接口适配
- 具有独立网络连接功能，可协助性能稍弱的单片机实现上网

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
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [CPU Hotplug](../cpu_hotplug.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [Bootloader与Ota](../bootloader_ota.md)
- [BK AT](../at.md)
- [BK IDK AT 入门指南](bk_at_start_guide.md)
- [BK IDK AT 命令集](bk_at_commandset.md)
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
