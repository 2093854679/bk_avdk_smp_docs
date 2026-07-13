# UART



## 1 功能概述

> > UART (Universal Asynchronous Receiver and Transmitter) 通用异步接收器/发送器，用来实现不同设备之间的全双工或半双工数据交换。BK7258具有3个uart，uart0、uart1和uart2。
>
> - UART相关的理论介绍参考: [UART的驱动](../../developer-guide/peripheral/bk_uart.md "../../developer-guide/peripheral/bk_uart.md")


## 2 代码路径

> - demo路径：
>   :   `cp\components\bk_cli\cli_uart.c`
> - 驱动源码路径：
>   :   `cp\middleware\driver\uart\uart_driver.c`


## 3 uart相关宏配置

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG_UART0 | UART0使能配置 | `cp\middleware\soc\bk7259\bk7259.defconfig` | y |
> | CONFIG_UART1 | UART1使能配置 | `cp\middleware\soc\bk7259\bk7259.defconfig` | n |
> | CONFIG_UART2 | UART2使能配置 | `cp\middleware\soc\bk7259\bk7259.defconfig` | n |
> | CONFIG_UART_PRINT_PORT | 配置打印输出log的UART口 | `cp\middleware\soc\bk7259\bk7259.defconfig` | 0 |
> | CONFIG_PRINTF_BUF_SIZE | 配置打印输出log的BUFFER大小 | `cp\middleware\soc\bk7259\bk7259.defconfig` | 256 |
> | CONFIG_KFIFO_SIZE | 配置UART对应软件FIFO的大小 | `cp\middleware\soc\bk7259\bk7259.defconfig` | 128 |
> | CONFIG_UART_ERR_INTERRUPT | UART使能错误中断 | `cp\middleware\soc\bk7259\bk7259.defconfig` | y |
> | CONFIG_UART_TX_DMA | 配置UART的DMA的TX功能即拷贝RAM数据到UART的FIFO | `cp\middleware\soc\bk7259\bk7259.defconfig` | n |
> | CONFIG_UART_RX_DMA | 配置UART的DMA的RX功能即从UART的FIFO数据拷贝到RAM | `cp\middleware\soc\bk7259\bk7259.defconfig` | n |
> | UART_RX_DMA_KFIFO_SIZE | 配置UART的RX的DMA的KFIFO的大小 | `cp\middleware\soc\bk7259\bk7259.defconfig` | 128 |


## 4 UART PIN脚描述

> - UART0对应开发板子上的uart0,且对应有1组PIN脚，对应的硬件管脚如下：
>
>   > | UART0功能 | 组0 |
>   > | --- | --- |
>   > | UART0_TX | GPIO11 |
>   > | UART0_RX | GPIO10 |
> - UART1对应开发板子上的uart1,且对应有1组PIN脚，对应的硬件管脚如下：
>
>   > | UART1功能 | 组0 |
>   > | --- | --- |
>   > | UART1_TX | GPIO0 |
>   > | UART1_RX | GPIO1 |
> - UART2对应开发板子上的uart2,且对应有1组PIN脚，对应的硬件管脚如下：
>   :   | UART2功能 | 组0 |
>       | --- | --- |
>       | UART2_RX | GPIO40 |
>       | UART2_TX | GPIO41 |


---


## 5 UART demo 配置

> - demo支持的命令如下表：
>
>   > | Command | | Param | Description |
>   > | --- | --- | --- | --- |
>   > | uart_driver {init|deinit} | | {init|deinit}: | init/deinit the uart resoure common |
>   > | uart {id} init [baud_rate] [data_bits]  [parity] [stop_bits] [flow_ctrl]  [src_clk] [rx_dma_en] [tx_dma_en] | | {id}:uart id,value 0 | init uart and set working parameters |
>   > | {baud_rate}:uart baud rate |
>   > | {data_bits}: support value range 5 ~ 8 bits |
>   > | {parity}: support parity mode |
>   > | {stop_bits}:the stop bits len |
>   > | {flow_ctrl}: not support flow ctrl |
>   > | {src_clk}:uart working clock source |
>   > | {rx_dma_en}: enable uart rx dma |
>   > | {tx_dma_en}: enable uart tx dma |
>   > | uart_config  {id} | baud_rate {value} | {value}:support baud rate | set uart working parameters |
>   > | data_bits {value} | {value}:support value range 5 ~ 8 bits |
>   > | parity {value} | {value}:support parity none、 odd、 even |
>   > | stop_bits {value} | {value}:support 1 or 2 bits |
>   > | flow_ctrl {value} | {value}:support 0 or 1 |
>   > | rx_thresh {value} | {value}:support value range 0 ~ 255 bits |
>   > | tx_thresh {value} | {value}:support value range 0 ~ 255 bits |
>   > | rx_timeout{value} | {value}:support value range 0 ~ 3 bits |
>   > | uart_int {id} {enable|disable|reg} {tx|rx} | | {id}:uart id,value 0 | enable|disable uart tx|rx interrupt and register uart tx|rx handler |
>   > | {enable|disable}:enable|disable tx|rx interrupt |
>   > | {tx|rx}: register tx|rx interrupt handler |
>   > | uart {id} {read|write}  {length} | | {id}:uart id,value 0 | read specified length of data through uart |
>   > | {read|write}: read|write operation |
>   > | {length}: length to be read|write |

备注


-1.UART 模块的时钟源为 26M Hz，波特率是从 26M Hz 时钟源中分出的；


-2.计算方法为“除数 = （时钟源值 / 波特率）-1”。然后软件将除数值设置为 UART 寄存器；


-3.例如： 如果我们想设置波特率为 115200，则除数值为 = （26000000 / 115200）-1 == 224。软件将 224 设置为 UART 寄存器。因此，如果我们想设置其他波特率，只需计算除数值并将其设置为 UART 寄存器即可。（注意：除数值应该是整数类型）。
