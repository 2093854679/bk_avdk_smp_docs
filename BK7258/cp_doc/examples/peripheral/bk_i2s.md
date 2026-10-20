---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_i2s.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="i2s-demo"></a>

# I2S demo

<a id="id1"></a>

## 1 功能概述

> I2S demo支持不同工作模式下master发送数据和salve接收数据。

<a id="id2"></a>

## 2 代码路径

> demo路径: `components\bk_cli\cli_i2s.c`
>
> I2S模块API接口的详细说明请参考结尾的链接。

<a id="cli"></a>

## 3 cli命令简介

demo支持的命令如下表:

| Command | Description |
| --- | --- |
| i2s\_master\_test {start\|stop} | 作为master在I2S模式下发送数据 |
| i2s\_slave\_test {start\|stop} | 作为slave在I2S模式下接收数据 |
| pcm\_master\_test {start\|stop} | 作为master在PCM模式下发送数据 |
| pcm\_slave\_test {start\|stop} | 作为slave在PCM模式下接收数据 |
| dtm\_master\_test {start\|stop} | 作为master在DTM\+PCM模式下发送数据 |
| dtm\_slave\_test {start\|stop} | 作为slave在DTM\+PCM模式下接收数据 |
| 2bd\_master\_test {start\|stop} | 作为master在2B\+D模式下发送数据 |
| 2bd\_slave\_test {start\|stop} | 作为slave在2B\+D模式下接收数据 |

demo运行依赖的宏配置:

| Name | Description | File | value |
| --- | --- | --- | --- |
| CONFIG\_I2S | 配置I2S功能使能 | `\middleware\soc\bk7258\bk7258_ap.defconfig` | y |
| CONFIG\_I2S\_TEST | 配置demo是否生效 | `\middleware\soc\bk7258\bk7258_ap.defconfig` | y |

demo运行依赖的库和驱动:
:   - GPIO GPIO驱动
    - DMA DMA驱动

<a id="id3"></a>

## 4 演示介绍

以I2S工作模式的demo为例，demo执行的步骤如下:

> 1.连接两块测试板子
> :   - 使用两块开发板进行测试，一块作为master端，一块作为slave端
>     - 将两块板子的CLK和SYNC引脚互连
>     - 将master的DIN引脚和slave的DOUT引脚连接
>     - 将master的DOUT引脚和slave的DIN引脚连接
>
> 2.开始slave端测试
> :   - slave端Uart发送AT指令 `i2s_slave_test start` 执行slave角色的I2S功能测试
>
> 3.开始master端测试
> :   - Uart发送AT指令 `i2s_master_test start` 执行master角色的I2S功能测试
>
> 4.停止测试
> :   - 观察串口log打印，同时使用逻辑分析仪抓取数据解析分析，待测试完成后，slave和master端分别Uart发送AT指令 `i2s_slave_test stop` 和 `i2s_master_test stop` 停止执行I2S功能测试

<a id="id4"></a>

## 5 详细配置及说明

重要

注意事项:
:   - 1. I2S通讯时master和slave的DIN和DOUT引脚连接要正确，master的DIN和slave的DOUT连接，master的DOUT和slave的DIN连接;
    - 2. master和slave的工作模式要一致;
    - 3. I2S使用的GPIO引脚没有外接导致信号异常的其他电路;

<a id="id5"></a>

## 参考链接

> API 参考 : @api-reference/peripheral/bk\_i2s.html 介绍I2S API接口
>
> [用户开发指南 :](../../developer-guide/peripheral/bk_i2s.md) 介绍I2S调试开发流程
>
> [示例 :](bk_i2s.md) 介绍I2S测试demo的使用
