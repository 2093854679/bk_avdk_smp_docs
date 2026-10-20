---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_can.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="can"></a>

# CAN

<a id="id1"></a>

## CAN 简介

控制器局域网 (CAN, Controller Area Network) 总线是一种强大的串行总线系统，可实现网络节点之间高效可靠的通信。它使用多主总线配置并在没有 CPU 干预的情况下管理错误检测和处理。

<a id="id2"></a>

## CAN 控制器特性

1.支持 CAN 协议规范
:   CAN 2.0B（最多 8 字节有效载荷，经 Bosch 参考模型验证）
    CAN FD（最多 64 字节有效载荷，符合 ISO 11898-1:2015 或非 ISO Bosch）

2.可编程数据速率
:   CAN 2.0B 数据速率高达 1 Mbit/s
    CAN FD 数据速率高达 2 Mbit/s

3.可编程波特率预分频器，分频系数介于 1 到 256 之间
:   详细信息需要查看寄存器文档及设计文档

4.两个发送缓冲器
:   一个主发送缓冲器 (PTB)
    一个可选的可配置的辅助发送缓冲器 (STB)

5.通用参数选择缓冲区时隙的数量
:   该部分使用默认配置，不建议进行修改。

6.可在 FIFO 或优先决策模式下运行
:   默认使用FIFO模式，优先决策模式需要配置，参考API

7.独立和可编程的内部 29 位验收过滤器
:   可通过通用参数在 1 至 16 范围内选择验收过滤器数量

8.扩展功能
:   单发传输模式（用于 PTB 和/或 STB）
    只听模式
    环回模式（内部和外部）
    收发器待机模式

9.扩展的状态和错误报告
:   捕获最后发生的错误类型和仲裁丢失的位置
    可编程错误警告限制

10.可配置的中断源
:   默认只对用户支持TX和RX回调函数的注册使用

11.时间戳：
:   具有部分硬件支持的 ISO 11898-4 时间触发 CAN (TTCAN)
    CiA 603 时间戳

12.安全相关功能
:   具有附加地址保护的 ECC 内存保护
    内部逻辑核心的空间冗余

<a id="can-2-0-can-fd"></a>

## CAN 2.0 和 CAN FD 帧

CAN FD 是 CAN 2.0 的协议扩展。主要区别是：

> 数据有效载荷：CAN 2.0 最多 8 个字节，CAN FD 最多 64 个字节
> 一种用于 CAN 2.0 的可配置比特率，但用于 CAN FD 的是 2 种：仲裁速度慢，数据阶段速度快

CAN 2.0 和 CAN FD 的所有类型的帧如下图所示。

<a id="id5"></a>
![2.0 and fd](../../../../../_assets/3137ca1714a3d9dc1863-CAN_20_and_CAN_FD.png)


CAN 2.0 And CAN FD

Bosch 的 CAN FD 规范（非 ISO）使用名称 EDL，而 CAN FD ISO 规范使用名称 FDF 表示相同的位。两个名字都是同义词。本章节使用名称 FDF。
对于 CAN FD ISO 帧，填充计数作为 CRC 字段的一部分传输。对于 CAN FD 非 ISO 帧，填充计数不是帧的一部分。此外，CRC 校验器对非 ISO 和 ISO 帧有不同的初始化。因此 ISO 和非 ISO 帧是不兼容的。
CAN 控制器 核心中的 CAN 协议机器自动发送和接收帧并内置相应的控制和状态位。主机控制器需要选择所需的帧类型（IDE、RTR、FDF）、选择标识符并设置数据有效载荷。

缩写词在 CAN 规范在下表中进行了简要说明。对于经典 CAN 帧 (CAN 2.0)，一些位名称已使用 CAN FD ISO 规范重命名，但此处仍使用较旧的名称以便于向后引用。

| 缩写 | 描述 | 注释 |
| --- | --- | --- |
| ID | 标识符 IDentifier |  |
| RTR | 远程传输请求 Remote Transmission Request | 远程或数据帧 |
| SRR | 替代远程请求 Substitute Remote Request |  |
| RRS | 远程请求替换 Remote Request Substitution |  |
| IDE | 标识符扩展 IDentifier Extension | 标准或扩展帧 |
| DLC | 数据长度代码 Data Length Code | 有效载荷字节数 |
| EDL | 扩展数据长度 Extended Data Length | CAN 2.0 或 CAN FD 帧 |
| FDF | FD 格式指示器 FD Format indicator (\=EDL) | CAN 2.0 或 CAN FD 帧 |
| BRS | 比特率开关 Bit Rate Switch |  |
| ESI | 错误状态指示器 错误State Indicator |  |

<a id="id3"></a>

## CAN 驱动的宏定义开关

CONFIG\_CAN CAN驱动的总开关， 默认只编译CAN驱动部分，及主要can\_driver.c

CONFIG\_CAN\_TEST 在CONFIG\_CAN打开的状态下，打开测试部分进行单步测试，主要can\_test.c

CONFIG\_CAN\_DEMO 在CONFIG\_CAN打开的状态下，打开示例部分进行用例演示，主要can\_demo.c

1、只打开驱动部分时，CONFIG\_CAN\=y

2、进行API进行逐个测试时，CONFIG\_CAN\=y CONFIG\_CAN\_TEST\=y

3、进行实例进行测试验证时，CONFIG\_CAN\=y CONFIG\_CAN\_DEMO\=y

<a id="can-api"></a>

## CAN API使用必要了解的结构体说明

can\_config\_t:
:   protocol
    :   需要选择协议CAN 2.0B或CAN FD

    s\_speed
    :   S速度（Slow Speed）S速度是CAN总线的低速模式，其数据传输速率为125 kbps或更低。这种模式主要用于需要低成本、低功耗和低带宽的应用

    f\_speed
    :   F速度（Fast Speed）F速度是CAN总线的标准速度模式，其数据传输速率为500 kbps。这种模式主要用于需要高实时性和低延迟的应用

    tx\_size
    :   kfifo的深度，将要发送的数据暂存到软件FIFO中，用于对硬件tx fifo的扩展

    rx\_size
    :   kfifo的深度，将接收到的数据暂存到软件FIFO中，便于对硬件rx fifo的扩展

can\_frame\_tag\_t:
:   id
    :   标识符 IDentifier

    ide
    :   标识符扩展 IDentifier Extension

    rtr
    :   远程传输请求 Remote Transmission Request，只有2.0可以使用

    fdf
    :   FD 格式指示器 FD Format indicator (\=EDL)

    brs
    :   比特率开关 Bit Rate Switch，只有FD可用

    esi
    :   错误状态指示器 Error State Indicator，只有FD RX可用

        ttsen
        Time Triggered Switch，时间触发切换。它是一种用于CAN FD的技术，允许在特定时间触发切换位速率或其他参数

can\_frame\_s:
:   tag
    :   详细信息查看can\_frame\_tag\_t

    size
    :   发送数据的size

    data
    :   发送数据的buffer指针

can\_acc\_mask\_ide\_e:
:   CAN\_ACCEPT\_BOTH
    :   标准和扩展帧都支持

    CAN\_ACCEPT\_STANDARD
    :   仅支持标准帧

    CAN\_ACCEPT\_EXTENDED
    :   仅支持扩展帧

drv\_switch\_e:
:   DRIVER\_DISABLE
    不同协议驱动切换关闭

    DRIVER\_ENABLE
    不同协议驱动切换打开

can\_acc\_filter\_cmd\_s:
:   aide
    :   参考can\_acc\_mask\_ide\_e描述

    code
    :   ID不要超过29 bits

    mask
    :   对应的bit置位标志接收该ID设备的数据 1 disable, 0 enable

    seq
    :   0 to MAX\_ACF\_NUM, default 0 accept all

    onoff
    :   功能参考drv\_switch\_e描述

can\_callback\_des\_t:
:   cb
    :   回调函数指针(can\_callback)

    **\*param**
    :   私有参数

<a id="id4"></a>

## CAN API使用说明

bk\_err\_t bk\_can\_init(can\_dev\_t **\*can**);
:   初始化配置，注意查看上述结构体的配置

bk\_err\_t bk\_can\_driver\_init(void);
:   加载驱动

bk\_err\_t bk\_can\_driver\_deinit(void);
:   卸载驱动

bk\_err\_t bk\_can\_deinit(void);
:   卸载配置，释放资源

bk\_err\_t bk\_can\_receive(uint8\_t **\*data**, uint32\_t expect\_size, uint32\_t **\*recv\_size**, uint32\_t timeout);
:   接收数据，data是接收的buffer， expect\_size是接收的数据长度，recv\_size是实际数据长度，timeout是接收等待的时间
    接收数据分为两种，一种中断通知然后交给下半部进行数据读取。另一种是读取等待总线数据，接收到数据后将数据读走

bk\_err\_t bk\_can\_send\_ptb(can\_frame\_s **\*frame**);
:   优先发送数据，参数参考上一小节结构体介绍

bk\_err\_t bk\_can\_send(can\_frame\_s **\*frame**, uint32\_t timeout);
:   发送数据，等待数据发送完成

bk\_err\_t bk\_can\_acc\_filter\_set(can\_acc\_filter\_cmd\_s **\*cmd**);
:   硬件过滤器配置，只接受部分ID的数据，减少处理

void bk\_can\_register\_isr\_callback(can\_callback\_des\_t **\*rx\_cb**, can\_callback\_des\_t **\*tx\_cb**);
:   注册TXRX的中断处理回调函数，注意这两个函数都是在中断中执行，注意回调函数的处理内容

<a id="can-pin-and-gpio-map"></a>

## CAN Pin and GPIO Map

| CAN Pin | BK7258\_CP0 |
| --- | --- |
| CAN TX | 44 |
| CAN RX | 45 |
| CAN STBY | 46 |

注意：这三个PIN还与其他功能复用
GPIO\_44, SPI0\_SCK(IO)/ADC0(Z)/RGB\_b\[6\]/I8080\_d3(O)/I2S2\_SCK(IO)

GPIO\_45, SPI0\_NSS(IO)/ADC7(Z)/RGB\_b\[5\]/I8080\_d2(O)/I2S2\_SYNC(IO)

GPIO\_46, SPI0\_MOSI(IO)/ENET\_PHY\_INT(I)/TOUCH\[140\]/RGB\_b\[4\]/I8080\_d1(O)/I2S2\_DIN(IO)

<a id="can-api-reference"></a>

## CAN API Reference

> [CAN的驱动API](../../api-reference/peripheral/bk_can.md)
