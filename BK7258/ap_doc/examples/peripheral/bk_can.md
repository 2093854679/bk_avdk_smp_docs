---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_can.html
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

## 1 功能概述

模拟实际应用中，多个设备的单一功能，将设备分为：发送者(sender)接收者(receiver)监视者(moniter)干扰者(interfere)
发送者(sender)发送数据，可接收所有数据但只处理接收者(receiver)数据；
接收者(receiver)只接收发送者(sender)数据，再把数据发送出去；
监视者(moniter)监控所有数据，保持BUS正常传输数据；
干扰者(interfere)乱发数据，且不接受任何数据，用于测试过滤器、竞争等。

在执行demo前，可通过指令调整波特率，将所有设备进行波特率调高或降低。

通过设置已经过滤器，将设备设置位只接受特定ID的设备数据。

<a id="id2"></a>

## 2 代码路径

> demo路径：`middleware\driver\can_demo.c`

<a id="demo"></a>

## 3 demo命令简介

demo运行依赖的宏配置：

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG\_TRNG | need to get random data | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
> | CONFIG\_CLI | need cli | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |

demo支持的命令如下表：

> | Command | | Param | Description |
> | --- | --- | --- | --- |
> | can\_filter\_demo \[aid\] \[acode\] \[amask\] | | {aid}:choose standard or extended | Configure device ID filter |
> | {acode}: no more than 29 bits |
> | {amask}: 1 disable, 0 enable |
> | can\_speed\_demo \[s\_spend\] \[f\_speed\] | | {s\_spend}: Slow Speed | Dynamically adjust the setting speed |
> | {f\_speed}: Fast Speed |
> | can\_stb\_demo1 \[can\_id\] \[sender\|receiver\|moniter\|interfere\] \[start\|stop\] | | {can\_id}: device ID | CAN FD Tested demo using different  identities |
> | {sender\|receiver\|moniter\|interfere}: Identity |
> | {start\|stop}: start or stop |
> | can\_stb\_demo2 \[can\_id\] \[sender\|receiver\|moniter\|interfere\] \[start\|stop\] | | {can\_id}: device ID | CAN 20 Tested demo using different  identities |
> | {sender\|receiver\|moniter\|interfere}: Identity |
> | {start\|stop}: start or stop |

CAN 支持的波特率如下：

> CAN\_BR\_250K, //81%
>
> CAN\_BR\_500K, //81%
>
> CAN\_BR\_800K, //80%
>
> CAN\_BR\_1M, //81%
>
> CAN\_BR\_2M, //81%
>
> CAN\_BR\_4M, //81%
>
> CAN\_BR\_5M, //77%

<a id="id3"></a>

## 4 硬件环境连接介绍

使用的CAN Transceiver 为MCP2562FD 对应使用的小板PIN定义如下图所示

<a id="id5"></a>
![can_t](../../../../../_assets/36cf86e0a027afe81a01-can_transceiver.png)


Figure 1\. CAN Transceiver

开发板上与接收器连接对应的GPIO：
:   | GPIO | FUNC |
    | --- | --- |
    | P44 | CAN TX |
    | P45 | CAN RX |
    | P46 | CAN STBY |

BK7258开发板与CAN Transceiver PIN连接如下图所示，注意开发板3.3v 可能影响到vio Transceiver电压

<a id="id6"></a>
![CAN Transceiver connection board](../../../../../_assets/263ec9addc4d6238af9c-can_trans_connect_board.png)


Figure 2\. CAN Transceiver connection board

CAN Transceiver 需要连接到两端120Ω电阻的总线上，线上阻值为60Ω，测试用线如下图所示

<a id="id7"></a>
![can connect line](../../../../../_assets/0c7c34fbc25047d50a02-can_connect_line.png)


Figure 3\. CAN BUS

两块板子进行对发接收环形测试，测试用线如下图所示

<a id="id8"></a>
![can two boards](../../../../../_assets/adc05cea74da196dae63-can_two_boards_connect.png)


Figure 4\. CAN Data transmission test

四块板子进行测试，测试用线如下图所示

<a id="id9"></a>
![can four boards](../../../../../_assets/1204a7677f04372295d7-can_four_boards_connect.png)


Figure 5\. CAN System transmission test

<a id="id4"></a>

## 5 演示介绍

1、设置过滤器，保证设备只接收该ID的数据，是根据can\_filter\_demo:
:   can\_filter\_demo 0 0x10000008 0x1fffff08 过滤器设置只接收 ID 0x10000008的设备数据
    can\_filter\_demo 0 0x10000004 0x1fffff04 过滤器设置只接收 ID 0x10000004的设备数据

输入指令后，log如下图所示

<a id="id10"></a>
![set filterfilter](../../../../../_assets/7215906ec397df264320-can_set_filter_cfg.png)


Figure 6\. Filter Configure

2、若要进行动态配置波特率，请参考如下图所示demo

<a id="id11"></a>
![set speed](../../../../../_assets/18e314189560d9adb835-can_dy_set_speed.png)


Figure 7\. Dynamically set baud rate

3、 CAN FD示例1，2个设备进行对测，1个设备做发起方，1个设备做应答方

① id\_4 先保存64bits 的随机数据到全局变量；
② id\_4 将这组随机数据发送到 CAN总线上， 触发发送完成中断后，发送结束；
③ id\_8 设备 触发接收中断，在中断中发送msg到 task队列， 读取id\_1设备发送过来的数据；
④ id\_8 读取到的64bits 数据发送到CAN总线上， 触发发送完成中断后，发送结束；
⑤ id\_4 触发中断，在中断中发送msg到 task队列，在task中解析是否数据正确；

测试目标是数据通路正常，没有错误数据

测试命令:
:   can\_stb\_demo1 0x10000004 sender start

    can\_stb\_demo1 0x10000004 sender stop

    can\_stb\_demo1 0x10000008 receiver start

    can\_stb\_demo1 0x10000008 receiver stop

<a id="id12"></a>
![loop test](../../../../../_assets/6b36392f0680f1787ee9-can_2_device_loop_test.png)


Figure 8\. 2Devices data transmission loop test

传输过程中有数据错误时，出现如下打印

> ```
> cli:I(26642):====CAN DEMO1 FAIL==== send_buf[00]:0x62 receive_buf[05]:0x1f
> cli:I(26642):====CAN DEMO1 FAIL==== send_buf[01]:0x04 receive_buf[06]:0xfd
> cli:I(26642):====CAN DEMO1 FAIL==== send_buf[02]:0x4a receive_buf[07]:0xa7
> cli:I(26642):====CAN DEMO1 FAIL==== send_buf[03]:0x4d receive_buf[08]:0x73
> cli:I(26642):====CAN DEMO1 FAIL==== send_buf[04]:0x57 receive_buf[09]:0x76
> cli:I(26642):====CAN DEMO1 FAIL==== send_buf[05]:0x6c receive_buf[10]:0x99
> cli:I(26642):====CAN DEMO1 FAIL==== send_buf[06]:0x8e receive_buf[11]:0xa5
> cli:I(26642):====CAN DEMO1 FAIL==== send_buf[07]:0x3d receive_buf[12]:0x28
> ```

4、 在示例1的基础上增加1个设备作为示例2，共3个设备测试，1个监视器设备，1个设备做发起方，1个设备做应答方
监视器设备只接收数据，并对接收到的数据进行统计，便于确定对发数据的设备接收正常。
测试目标是CAN BUS正常数据收发，与示例1统计到的发送次数和接收次数进行比较，确保数据没有丢失。

测试命令：
:   can\_stb\_demo1 0x10000001 moniter start

    can\_stb\_demo1 0x10000001 moniter stop

<a id="id13"></a>
![loop test](../../../../../_assets/e7d2a2238f906bbe0856-can_demo_moniter.png)


Figure 9\. Demo Moniter

5、 在示例2的基础上增加1个设备作为示例3，共4个设备测试，1个干扰设备，1个监视器设备，1个设备做发起方，1个设备做应答方
干扰器只发送数据，扰乱线上状态，但不会将CAN总线搞坏掉，且干扰器的ID较高。
测试目标是让线上出现竞争的情况，且数据仍能正常传输。

测试命令：
:   can\_stb\_demo1 0x10000002 interfere start

    can\_stb\_demo1 0x10000002 interfere stop

<a id="id14"></a>
![loop test](../../../../../_assets/d71c4db4351a562fb105-can_four_boards_demo_test.png)


Figure 10\. CAN mini sys test

6、上述示例1、2、3都是在CAN FD协议下进行的，将命令头改为can\_20\_demo2，则使用CAN\_2.0进行测试。
其他目标一致
