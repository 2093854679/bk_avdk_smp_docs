---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_uart.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="uart"></a>

# UART

<a id="id1"></a>

## 1 功能概述

> UART (Universal Asynchronous Receiver and Transmitter) 通用异步接收器/发送器，用来实现不同设备之间的全双工或半双工数据交换。
>
> CP 中断驱动完整支持 UART0～UART4；UART5 及其中断归 AP 所有。默认配置
> `cp/middleware/soc/bk7259/bk7259.defconfig` 仅使能配置项
> `CONFIG_UART0` 。CP 日志口配置为 `CONFIG_UART_PRINT_PORT=0`
> （DL\_UART0）。

备注

> 允许 AP 与 CP 编译使能同一 UART 实例，但运行时一个实例及其 TX/RX 引脚
> 只能有一个所有者；不要在两侧并发初始化同一实例或分配同一组 UART 引脚。
> 默认日志口所有权为 CP UART0、AP UART5。

- UART相关的理论介绍参考: [UART的驱动](../../developer-guide/peripheral/bk_uart.md)

<a id="id3"></a>

## 2 代码路径

> - demo路径：
>   :   `cp\middleware\driver\uart\uart_test.c`
> - 驱动源码路径：
>   :   `cp\middleware\driver\uart\uart_driver.c`

<a id="id4"></a>

## 3 uart相关宏配置

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG\_UART0 | UART0使能配置 | `cp\middleware\soc\bk7259\bk7259.defconfig` | y |
> | CONFIG\_UART1 | UART1使能配置 | `cp\middleware\soc\bk7259\bk7259.defconfig` | n |
> | CONFIG\_UART2 | UART2使能配置 | `cp\middleware\soc\bk7259\bk7259.defconfig` | n |
> | CONFIG\_UART\_PRINT\_PORT | 配置打印输出log的UART口 | `cp\middleware\soc\bk7259\bk7259.defconfig` | 0 |
> | CONFIG\_PRINTF\_BUF\_SIZE | 配置打印输出log的BUFFER大小 | `cp\middleware\soc\bk7259\bk7259.defconfig` | 256 |
> | CONFIG\_KFIFO\_SIZE | 配置UART对应软件FIFO的大小 | `cp\middleware\soc\bk7259\bk7259.defconfig` | 128 |
> | CONFIG\_UART\_ERR\_INTERRUPT | UART使能错误中断 | `cp\middleware\soc\bk7259\bk7259.defconfig` | y |
> | CONFIG\_UART\_TX\_DMA | 配置UART的DMA的TX功能即拷贝RAM数据到UART的FIFO | `cp\middleware\soc\bk7259\bk7259.defconfig` | n |
> | CONFIG\_UART\_RX\_DMA | 配置UART的DMA的RX功能即从UART的FIFO数据拷贝到RAM | `cp\middleware\soc\bk7259\bk7259.defconfig` | n |
> | UART\_RX\_DMA\_KFIFO\_SIZE | 配置UART的RX的DMA的KFIFO的大小 | `cp\middleware\soc\bk7259\bk7259.defconfig` | 512 |

<a id="uart-pin"></a>

## 4 UART PIN脚描述

> - UART0对应开发板子上的uart0,且对应有1组PIN脚，对应的硬件管脚如下：
>
>   > | UART0功能 | 组0 |
>   > | --- | --- |
>   > | UART0\_TX | GPIO11 |
>   > | UART0\_RX | GPIO10 |
> - UART1对应开发板子上的uart1,且对应有1组PIN脚，对应的硬件管脚如下：
>
>   > | UART1功能 | 组0 |
>   > | --- | --- |
>   > | UART1\_TX | GPIO0 |
>   > | UART1\_RX | GPIO1 |
> - UART2对应开发板子上的uart2,且对应有1组PIN脚，对应的硬件管脚如下：
>   :   | UART2功能 | 组0 |
>       | --- | --- |
>       | UART2\_RX | GPIO40 |
>       | UART2\_TX | GPIO41 |
>
> 注：以上为默认引脚。UART 引脚以 usr\_gpio\_cfg.h 的 GPIO\_DEFAULT\_DEV\_CONFIG（对应 GPIO\_DEV\_UARTx\_TXD / GPIO\_DEV\_UARTx\_RXD）为准，修改引脚请修改该表。

---

<a id="uart-demo"></a>

## 5 UART demo 配置

> - demo支持的命令如下表：
>
>   > | Command | | Param | Description |
>   > | --- | --- | --- | --- |
>   > | uart\_driver {init\|deinit} | | {init\|deinit}: | init/deinit the uart resoure common |
>   > | uart {id} init \[baud\_rate\] \[data\_bits\]  \[parity\] \[stop\_bits\] \[flow\_ctrl\]  \[src\_clk\] \[rx\_dma\_en\] \[tx\_dma\_en\] | | {id}:uart id,value 0 | init uart and set working parameters |
>   > | {baud\_rate}:uart baud rate |
>   > | {data\_bits}: support value range 5 \~ 8 bits |
>   > | {parity}: support parity mode |
>   > | {stop\_bits}:the stop bits len |
>   > | {flow\_ctrl}: not support flow ctrl |
>   > | {src\_clk}:uart working clock source |
>   > | {rx\_dma\_en}: enable uart rx dma |
>   > | {tx\_dma\_en}: enable uart tx dma |
>   > | uart\_config  {id} | baud\_rate {value} | {value}:support baud rate | set uart working parameters |
>   > | data\_bits {value} | {value}:support value range 5 \~ 8 bits |
>   > | parity {value} | {value}:support parity none、 odd、 even |
>   > | stop\_bits {value} | {value}:support 1 or 2 bits |
>   > | flow\_ctrl {value} | {value}:support 0 or 1 |
>   > | rx\_thresh {value} | {value}:support value range 0 \~ 255 bits |
>   > | tx\_thresh {value} | {value}:support value range 0 \~ 255 bits |
>   > | rx\_timeout{value} | {value}:support value range 0 \~ 3 bits |
>   > | uart\_int {id} {enable\|disable\|reg} {tx\|rx} | | {id}:uart id,value 0 | enable\|disable uart tx\|rx interrupt and register uart tx\|rx handler |
>   > | {enable\|disable}:enable\|disable tx\|rx interrupt |
>   > | {tx\|rx}: register tx\|rx interrupt handler |
>   > | uart {id} {read\|write}  {length} | | {id}:uart id,value 0 | read specified length of data through uart |
>   > | {read\|write}: read\|write operation |
>   > | {length}: length to be read\|write |

备注

-1.UART 模块的时钟源为 26M Hz，波特率是从 26M Hz 时钟源中分出的；

-2.计算方法为“除数 \= （时钟源值 / 波特率）-1”。然后软件将除数值设置为 UART 寄存器；

-3.例如： 如果我们想设置波特率为 115200，则除数值为 \= （26000000 / 115200）-1 \=\= 224。软件将 224 设置为 UART 寄存器。因此，如果我们想设置其他波特率，只需计算除数值并将其设置为 UART 寄存器即可。（注意：除数值应该是整数类型）。
