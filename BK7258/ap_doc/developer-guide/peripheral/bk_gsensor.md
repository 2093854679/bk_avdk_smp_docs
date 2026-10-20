---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_gsensor.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="gsensor"></a>

# Gsensor 软件使用指南

<a id="id1"></a>

## Gsensor概述

Gsensor 是高精度数字三轴加速度传感器，当前已经适配了SC7A20传感器。使用I2C进行数据传输，对X、Y、Z轴的采集数据进行分析。

<a id="id4"></a>
![gsensor_sc7a20](../../../../../_assets/b3df740349de6fb31514-gsensor_sc7a20.png)


Gsensor SC7A20

<a id="id2"></a>

## 宏定义含义

> CONFIG\_GSENSOR\_ENABLE 功能的总开关
> CONFIG\_GSENSOR\_DEMO\_EN 已经实现的一个DEMO，客户可以根据自己的情况决定是否使用该DEMO
> CONFIG\_GSENSOR\_ARITHEMTIC\_DEMO\_EN 算法识别DEMO，当前从传感器接收到的数据进行解析
> CONFIG\_GSENSOR\_SC7A20\_ENABLE 适配的传感器是 SC7A20
> CONFIG\_GSENSOR\_TEST\_EN CLI测试的命令行打开

宏开关的默认配置
:   CONFIG\_GSENSOR\_ENABLE\=y
    CONFIG\_GSENSOR\_DEMO\_EN\=y
    CONFIG\_GSENSOR\_ARITHEMTIC\_DEMO\_EN\=y
    CONFIG\_GSENSOR\_TEST\_EN\=n
    CONFIG\_GSENSOR\_SC7A20\_ENABLE\=y

<a id="id3"></a>

## 通用函数接口

> > 该部分的API为通用的接口，便于客户自行开发。可适配更多不同种类的Gsensor
>
> void\* bk\_gsensor\_init();
> 初始化gsensor驱动，将使用的Gsensor的名字进行挂在。为后续不同种类的Gsensor设计通用的接口
>
> void bk\_gsensor\_deinit();
> 卸载gsensor，将初始化时使用的指针进行卸载。
>
> int bk\_gsensor\_open();
> 打开gsensor，将传感器的供电等基本寄存器配置完成
>
> void bk\_gsensor\_close();
> 关闭gsensor，停止工作
>
> int bk\_gsensor\_setDatarate();
> 设置gsensor采集数据的频率
>
> int bk\_gsensor\_setMode();
> 设置gsensor的模式，正常运行模式和唤醒模式
>
> int bk\_gsensor\_setDateRange();
> 设置gsensor数据采集的量程
>
> int bk\_gsensor\_registerCallback();
> 数据接收到后，通过回调函数通知到应用层

<a id="gsensor-demo"></a>

## Gsensor Demo 接口函数

> bk\_err\_t gsensor\_demo\_init(void);
> Demo初始化，注册回调函数、初始化传感器、创建demo线程
>
> void gsensor\_demo\_deinit(void);
> 卸载Demo线程，卸载回调函数
>
> bk\_err\_t gsensor\_demo\_open();
> 打开Gsensor，发送基本配置到传感器上
>
> bk\_err\_t gsensor\_demo\_close();
> Gsensor，发送关闭配置到传感器上
>
> bk\_err\_t gsensor\_demo\_set\_normal();
> 设置为正常运行模式
>
> bk\_err\_t gsensor\_demo\_set\_wakeup();
> 设置为唤醒模式
>
> bk\_err\_t gsensor\_demo\_lowpower\_wakeup();
> 设置为低功耗唤醒模式

<a id="gsensor-arithemtic-demo"></a>

## Gsensor Arithemtic Demo接口函数

> void arithmetic\_module\_init(void);
> 创建算法处理线程
>
> void arithmetic\_module\_deinit(void);
> 卸载算法处理线程
>
> int arithmetic\_module\_copy\_data\_send\_msg();
> 通过该接口将数据发送到算法处理线程中
>
> void arithmetic\_module\_register\_status\_callback();
> 注册算法处理完成后识别到的当前状态
>
> void shake\_arithmetic\_set\_parameter();
> 设置晃动算法的参数
>
> PS：还有其他的算法可供参考，各种Gsensor的数据表现不一样。因此算法需要根据实际情况进行参数调整。
