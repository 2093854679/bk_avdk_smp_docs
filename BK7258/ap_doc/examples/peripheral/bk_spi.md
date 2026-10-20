---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_spi.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="spi"></a>

# SPI

<a id="id1"></a>

## 1 功能概述

> ```
> BK7258具有2路SPI控制器，其中SPI0对应3组PIN脚，SPI1对应1组PIN脚，用户可以根据硬件实际情况，进行PIN脚的划分；
> SPI支持主模式或从模式工作方式，基于三线或四线的全双工同步传输，三线模式相比四线模式少了一个CS片选管脚；
> SPI管脚通常可用于驱动外置flash，LCD屏或摄像头。
> ```
>
> - SPI功能具体描述参考: [SPI驱动工作原理](../../developer-guide/peripheral/bk_spi.md)

<a id="id3"></a>

## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_spi.c`
> - 驱动源码路径：
>   :   `middleware\driver\spi\spi_driver.c`
>
>       `middleware\driver\spi\spi_flash.c`

<a id="id4"></a>

## 3 SPI相关宏配置

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG\_SPI | SPI使能配置 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
> | CONFIG\_SPI\_DMA | SPI使能DMA配置 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
> | CONFIG\_SPI\_STATIS | SPI DEBUG使能，用于命令行dump spi寄存器信息 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
> | CONFIG\_SPI\_SUPPORT\_TX\_FIFO\_WR\_READY | SPI使能TX Fifo中断检测配置，一般建议使能 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
> | CONFIG\_SPI\_PM\_CB\_SUPPORT | SPI使能低功耗投票功能 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | n |
> | CONFIG\_SPI\_MST\_FLASH | SPI flash使能配置 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | n |

<a id="spi-pin"></a>

## 4 SPI PIN脚描述

> - SPI0对应3组PIN脚，用户可以根据硬件分布情况，使用其中一组：
>
>   > | SPI0功能 | 组0 | 组1 | 组2 |
>   > | --- | --- | --- | --- |
>   > | SPI0\_CLK | GPIO14 | GPIO44 | GPIO33 |
>   > | SPI0\_CS | GPIO15 | GPIO45 | GPIO34 |
>   > | SPI0\_MOSI | GPIO16 | GPIO46 | GPIO35 |
>   > | SPI0\_MISO | GPIO17 | GPIO47 | GPIO36 |
> - SPI1对应1组PIN脚，对应管脚如下：
>   :   | SPI1功能 | 组0 |
>       | --- | --- |
>       | SPI1\_CLK | GPIO2 |
>       | SPI1\_CS | GPIO3 |
>       | SPI1\_MOSI | GPIO4 |
>       | SPI1\_MISO | GPIO5 |

---

> - 对于SPI0，默认使用 GPIO14\~17 PIN脚组合，用户可以通过./middleware/soc/\<bk72xx\>/hal/spi\_ll.h修改选用的PIN脚组合。
>
>   > ```
>   > #define SPI0_LL_CSN_PIN     GPIO_15
>   > #define SPI0_LL_SCK_PIN     GPIO_14
>   > #define SPI0_LL_MOSI_PIN    GPIO_16
>   > #define SPI0_LL_MISO_PIN    GPIO_17
>   >
>   > #if 0
>   > #define SPI0_LL_CSN_PIN     GPIO_45
>   > #define SPI0_LL_SCK_PIN     GPIO_44
>   > #define SPI0_LL_MOSI_PIN    GPIO_46
>   > #define SPI0_LL_MISO_PIN    GPIO_47
>   > #endif
>   >
>   > #define SPI1_LL_SCK_PIN     GPIO_2
>   > #define SPI1_LL_CSN_PIN     GPIO_3
>   > #define SPI1_LL_MOSI_PIN    GPIO_4
>   > #define SPI1_LL_MISO_PIN    GPIO_5
>   > ```

---

<a id="spi-demo"></a>

## 5 SPI demo 配置

> - demo支持的命令如下表：
>
>   > | Command | | Param | Description |
>   > | --- | --- | --- | --- |
>   > | spi\_driver {init\|deinit} | | {init\|deinit}: | init/deinit the spi resoure common |
>   > | spi {id} init \[role\] \[bit\_width\]  \[polarity\] \[phase\] \[wire\_mode\]  \[baud\_rate\] \[bit\_order\] \[dma\_mode\] | | {id}:spi id,value range 0 \~ 1 | init spi and set working parameters |
>   > | {role}:master or slave |
>   > | {bit\_width}: support 8 or 16 bits |
>   > | {polarity}: CPOL support 0 or 1 |
>   > | {phase}:CPHA support 0 or 1 |
>   > | {wire\_mode}: support 3 or 4 wire mode |
>   > | {baud\_rate}:spi baud rate |
>   > | {bit\_order}: support LSB or MSB |
>   > | {dma\_mode}: support DMA |
>   > | spi\_config  {id} | baud\_rate {value} | {value}:support baud rate | set spi working parameters |
>   > | mode {value} | {value}:spi spi mode 0\~3 |
>   > | bit\_width {value} | {value}: support 8 or 16 bits |
>   > | wire\_mode {value} | {value}:support 3 or 4 wire mode |
>   > | bit\_order {value} | {value}:support LSB or MSB |
>   > | spi {id} {read\|write}  {length} | | {id}:spi id,value range 0 \~ 1 | read specified length of data through spi |
>   > | {read\|write}: read\|write operation |
>   > | {length}: length to be read\|write |
> - SPI 支持的波特率如下：
>
>   > ```
>   > static const uint32_t s_spi_clk_list[] = {
>   > 26000000, /**< DIV1 */
>   > 13000000, /**< DIV2 */
>   > 6500000,  /**< DIV4 */
>   > 5200000,  /**< DIV5 */
>   > 3250000,  /**< DIV8 */
>   > 2600000,  /**< DIV10 */
>   > 2000000,  /**< DIV13 */
>   > 1625000,  /**< DIV16 */
>   > 1300000,  /**< DIV20 */
>   > 1040000,  /**< DIV25 */
>   > 1000000,  /**< DIV26 */
>   > };
>   > ```
> - SPI模式和极性、相位的对应关系：
>   :   通常的，Mode表示工作模式，CPOL表示时钟极性，CPHA表示时钟相位。
>
>       | Mode | CPOL | CPHA |
>       | --- | --- | --- |
>       | 0 | 0 | 0 |
>       | 1 | 0 | 1 |
>       | 2 | 1 | 0 |
>       | 3 | 1 | 1 |

<a id="id5"></a>

## 6 SPI demo 命令行演示

> 1. bk7258开发板在con4中将SPI引出，使用2块bk7258开发板，按照下图进行连接（建议两个板子共地，以免数据采样不准确）：

<a id="id6"></a>
![SPI](../../../../../_assets/e647b2478a3f09a449a0-SPI_connect.png)


Figure 1\. 将2块开发板通过SPI对接

对应的GPIO：

> > | GPIO | FUNC |
> > | --- | --- |
> > | P44 | SCK |
> > | P45 | CSN |
> > | P46 | MOSI |
> > | P47 | MISO |
>
> 2. 启动开发板，对2块开发板分别输入初始化命令，分别设置为master和slave
>
> > 以下命令是基于CP的，AP侧可在命令前添加“cpu1”字段。
> >
> > - master： **spi 0 init master 8 1 1 4 10000000 MSB 1** //主机输入命令
> >
> >   > ```
> >   > [15:47:52.552]发→◇spi_driver init
> >   > [15:47:52.567]收←◆spi_driver init
> >   > cli:I(87880284):spi driver init
> >   > $
> >   > $
> >   > [15:50:51.443]发→◇spi 0 init master 8 1 1 4 10000000 MSB 1
> >   > [15:50:51.443]收←◆spi 0 init master 8 1 1 4 10000000 MSB 1
> >   > hal:I(88059168):spi select src_clk xtal
> >   > cli:I(88059168):spi init, spi_id=0
> >   > ```
> > - slave： **spi 0 init slave 8 1 1 4 10000000 MSB 1** //从机输入命令
> >
> >   > ```
> >   > [15:47:48.942]发→◇spi_driver init
> >   > [15:47:48.957]收←◆spi_driver init
> >   > cli:I(1085932):spi driver init
> >   > $
> >   > $
> >   > [15:52:33.910]发→◇spi 0 init slave 8 1 1 4 10000000 MSB 1
> >   > [15:52:33.910]收←◆spi 0 init slave 8 1 1 4 10000000 MSB 1
> >   > hal:I(1370886):spi select src_clk xtal
> >   > cli:I(1370888):spi init, spi_id=0
> >   > ```
> >
> > C） 从机进入接收状态，主机发送数据
> >
> > - slave： **spi 0 read 1024** //从机准备接收数据
> > - master： **spi 0 write 1024** //主机发送数据
> >
> >   > ```
> >   > [15:54:01.239]发→◇spi 0 write 1024
> >   > [15:54:01.255]收←◆spi 0 write 1024
> >   > cli:I(88248974):spi write bytes, spi_id=0, data_len=1024
> >   > $cli:I(88248984):spi Tx finish! UART send OK!
> >   > ```
> >
> > d）从机接收到数据
> >
> > > ```
> > > I(1458228):spi read, spi_id=0, size:1024
> > > cli:I(1458228):recv_buffer[0]=0x0
> > > cli:I(1458230):recv_buffer[1]=0x1
> > > cli:I(1458230):recv_buffer[2]=0x2
> > > cli:I(1458230):recv_buffer[3]=0x3
> > > ......
> > > cli:I(1458230):recv_buffer[3]=0xff
> > > ```
