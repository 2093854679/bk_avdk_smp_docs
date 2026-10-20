---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_dma.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="dma"></a>

# DMA 使用指南

<a id="id1"></a>

## 概述

DMA 传输将数据从一个地址空间复制到另一个地址空间，提供在外设和存储器之间或者存储器与存储器之间的高速数据传输。一个典型的 DMA 实现通常如下图所示。

<a id="id14"></a>
![DMA Overview](../../../../../_assets/b21dd49324463c207849-dma.png)


DMA Overview

备注

实际 DMA 架构实现可能与上图不同，上图主要为方便理解的一个抽象概述图。

CPU，DMA 控制器，DMA 内存通过总线相连。一个 DMA 控制器可支持多个通道，不同的通道可并发传输。外设与内存之间进行数据传输前，需要先选择一个通道，配置好相应的参数。

BK7258有两个DMA硬件，每个DMA硬件是8个通道；因为与历史代码兼容（客户的API不需要做变更），所以将两个DMA通道的各8个通道统一编号到16通道。
虽然BK7258的16个DMA通道能同时工作，但由于总线只有两条，因此在特定时刻实际最多只有两个通道能在总线上传输数据。

BK7258 SMP 分为AP和CP 两个部分，DMA通道根据宏开关CONFIG\_DMA\_LOGIC\_CHAN\_CNT和CONFIG\_DMA\_LOGIC\_CHAN\_ID\_MIN默认分配如下：

> - CP: chan12 \~ chan15
> - AP: chan0 \~ chan11

当多个不同的 DMA 通道在同一时刻均有数据传输时，由 DMA 对通道进行调度。DMA 通道有两种调度方式：

> - 轮询调度，所有通道同一优先级，先请求先调度
> - 基于优先级调度，优先级高的先调度，可通过:cpp:func:bk\_dma\_init 设置调度方式与优先级。
>
>   配置参数：dma\_chan\_priority\_t chan\_prio; 优先级范围0-7，注意高优先级的通道使用频次高时，可能会阻塞低优先级的通道。

<a id="id2"></a>

## DMA 配置

为了进行 DMA 传输，通常需要进行下述配置:

> - 配置源与目的设备；源设备是指数据来源设备如FIFO或SRAM，目的设备是指需要将数据搬运到的FIFO或SRAM。及SRAM-\>SRAM,FIFO-\>SRAM, SRAM-\>FIFO, FIFO-\>FIFO。
> - 设置源与目的设备的数据宽度；不同的设备FIFO宽度不同，根据实际外设进行数据宽度的配置。
> - 设置数据量及要搬运的数据长度，DMA搬运是否结束的重要参考依据。
> - 传输次数（单次传输或者循环传输)

配置部分参考结构体,hal\_dma\_types.h:dma\_config\_t。

<a id="id3"></a>

## DMA 传输次数设置

DMA 传输次数可通过传输模式来设置， DMA 有两种传输模式：

> - SINGLE 模式, 仅执行1次数据搬运，将源数据搬运到目的地址，根据长度或结束地址来判断搬运结束。
> - REPEAT 模式, 循环搬运数据，当搬运到结束地址时自动跳转到起始地址。当搬运的数据长度达到填写长度时，会上报中断。

<a id="id4"></a>

### 单次模式

单次模式如下图所示，从 start 传输到 start \+ len 结束， 通常 len 设置成 end \- start， 即整个块的长度。

<a id="id15"></a>
![DMA Single Mode](../../../../../_assets/9e3519b78474766a6d06-dma_single.png)


DMA Single Mode

<a id="id5"></a>

### 循环模式

循环模式如下图所示，DMA 从 start 传输到 end 后会再次从 start 传输到 end, 一直重复直到 DMA 被 stop。
当 SRC or DST 设备为单地址时，在 Repeat 模式下每次均传输 Start 所指向的地址，直到 DMA 被 stop。

<a id="id16"></a>
![DMA Repeat Mode](../../../../../_assets/d91e29d16da9f06d7072-dma_repeat.png)


DMA Repeat Mode

<a id="id6"></a>

## DMA 传输场景

DMA 地址配置基本原则：

> - 如果要传输的地址为单地址，即进行 DMA 传输时设备地址可用的地址长度等于数据宽度时，则只需配置 start 地址，end 地址配置成 0。单地址的方式多用于FIFO到SRAM的数据搬运。

如 UART 设备， 位宽为 8bits, DMA 传输时每次都只使用这 8bits 传输，因此只需配置 start 地址为 UART FIFO 地址，end 设置成 0\.

> - 如果要传输的地址为块地址，Start配置成块地址的起始地址， end 配置成块地址的结束地址。注意Single模式时搬运的数据长度不得超过了end address \- start address;

<a id="id7"></a>

### 具体应用可分成下述三种场景：

> - 单地址到单地址传输 (应用场景，FIFO-\>FIFO)
> - 单地址到块地址传输 (应用场景，FIFO-\>SRAM)
> - 块地址到块地址传输 (应用场景，SRAM-\>SRAM)

<a id="id8"></a>

### 单地址到单地址传输

<a id="id17"></a>
![DMA case1](../../../../../_assets/78aca54b730656c4aff3-dma_s3.png)


DMA case1

如上图所示, SRC/DEST 需要将Start地址和End地址配置为相同。

<a id="id9"></a>

### 单地址到块地址传输

<a id="id18"></a>
![DMA case2](../../../../../_assets/fe56ca4c06cce7bdfc2c-dma_s2.png)


DMA case2

如上图所示, SRC将Start地址和End地址配置为相同， DEST配置 start/end 地址。

<a id="id10"></a>

### 块地址到块地址传输

<a id="id19"></a>
![DMA case3](../../../../../_assets/7d2c75b7b9f0a63ff121-dma_s1.png)


DMA case3

如上图所示, SRC和DEST都需要配置 start和end 地址。

<a id="id11"></a>

## DMA不同传输数据模式与场景结合介绍

> - 1、loop模式为地址环回模式。一般拷贝总长度trans\_len会大于loop\_end\_addr-loop\_start\_addr，即要存放数据的内存范围。 传输的起始地址从dest/src\_start\_addr开始，一直增长到loop\_end\_addr后环回到 loop\_start\_addr，一直重复这个过程直到总长度trans\_len搬完结束。本质是有限memory空间内的single.
> - 2、repeat模式只会根据填写的拷贝长度进行中断上报，可在暂停地址位置停止数据搬运。若将暂停地址设置在拷贝范围之外，则一致循环搬运数据。直到软件将Dma\_en 置为0。

**SINGLE模式搬运数据流程及可能情况**

以源/目的地址都是SRAM为例，填写好起始地址、搬运长度后，启动DMA搬运。若打开了half\_finish/finish中断，则在搬运一半长度/全部搬运完成后上报中断，需要软件写1清0。需要将源/目的地址配置为增长的方式，让地址逐步增长。如果设置的长度不是4字节对齐，造成DMA卡住，中断也不会上报， 还需要软件做超时机制进行flush\_src\_buff 将剩余字节刷入目的地址，确保数据的完整性。

**1、**
开始启动时一定时从start地址开始搬运数据

<a id="id20"></a>
![DMA single sramtsram2](../../../../../_assets/5b7d7510df97b03bc908-dma_sram2sram_start.png)


DMA Single SRAM To SRAM Start

**2、**
搬运过程遇到暂停地址，此时不会上报中断，只是停止搬运数据。暂停地址的检测是每一个节拍进行检测，所以更改暂停地址没有限制条件。需要软件去更改暂停地址，另外暂停地址如果在loop地址范围以外，理论上就无效等信息。

<a id="id21"></a>
![DMA single sramtsram2](../../../../../_assets/fc39c5d296d30da77342-dma_sram2sram_running1.png)


DMA Single SRAM To SRAM Running

备注

**源暂停地址，停止搬运但不会触发中断**

<a id="id22"></a>
![DMA single sramtsram3](../../../../../_assets/cdafd2041063a27296fc-dma_sram2sram_running2.png)


DMA Single SRAM To SRAM Running

备注

**目的暂停地址停止搬运但不会触发中断**

**3、**
如果打开一半长度搬运中断使能，搬动总长度的一半也会停下来，并触发中断。需要软件写1清0，硬件搬运数据不受中断的影响。

<a id="id23"></a>
![DMA single sramtsram3](../../../../../_assets/efba51c3bb2c51aaab59-dma_sram2sram_pause.png)


DMA Single SRAM To SRAM Half\_Finish

**4、**
打开搬运完成中断使能，总长度搬运完成触发中断。DMA\_EN 硬件自动置为0。

<a id="id24"></a>
![DMA single sramtsram3](../../../../../_assets/b30e78d243ef8091b347-dma_sram2sram_stop.png)


DMA Single SRAM To SRAM Finish

**REPEAT模式搬运数据流程及可能情况**

一般会打开src/dest\_addr\_loop和配置loop start address和loop end address，数据搬运的总长度主要用于中断的上报（half finish interrupt/finish interrupt）。灵活使用pause\_address，便于定位和继续搬运数据。Half finish和Finish中断上报只和填写的长度相关。完成中断的长度，仅仅是报中断，如果没有设置暂停地址，则不会暂停。使用情况主要针对，SRAM-\>FIFO,FIFO-\>SRAM 2种情况

**源地址SRAM/目的地址FIFO**

> - DMA数据搬运只有在 硬件遇到暂停地址 或 软件将DMA\_EN置为0的情况下主动停下来。所以软件启动后，一般只更新暂停地址，让搬运数据继续。
> - DMA会检测FIFO是否有准备好的状态，出现FIFO not ready，DMA会被拉住。当FIFO ready时，DMA会主动进行数据搬运。

<a id="id25"></a>
![DMA single sramtsram3](../../../../../_assets/1de466cb7ea05b1797a6-dma_sram2fifo.png)


DMA Repeat SRAM To FIFO

**目的地址SRAM/源地址FIFO**

> - 源地址是否有数据，根据FIFO的状态位进行判断。
> - 可依靠模块来确定是否有数据进入了FIFO，DMA配置好之后，软件通过暂停地址等状态寄存器进行动态调整。以达到repeat循环搬运数据的方式。

<a id="id26"></a>
![DMA single sramtsram3](../../../../../_assets/7399fdd744240540676f-dma_fifo2sram.png)


DMA Repeat FIFO To SRAM

**LOOP模式搬运数据流程及可能情况**

必须置位src/dest\_loop\_addr且配置相应的loop start address和loop end address，且数据搬运的总长度一定要大于差值（loop\_end\_address –loop\_start\_address）。灵活使用pause\_address，便于定位和继续搬运数据。Half finish和Finish中断上报只和填写的长度相关。

**源地址SRAM/目的地址FIFO**

**1、**
loop模式下，要注意SRAM的起始和结束地址范围，需要软件进行计算暂停地址。若在传输过程中出现数据异常时，DMA\_EN置为0，再次启动时一定是从start\_address开始搬运数据。DMA会检测FIFO是否允许进行数据的搬运，若Not Ready，则停止在搬运到的位置等待ready

<a id="id27"></a>
![DMA single sramtsram3](../../../../../_assets/7b7e7d345106bec04b97-dma_loop_s2f_start.png)


DMA Loop SRAM To FIFO Start

**2、**
搬运数据到loop end address时，总长度还没有搬完。则回到loop start address开始搬运数据，直到遇到暂停地址。

<a id="id28"></a>
![DMA single sramtsram3](../../../../../_assets/71342543635229ab0c5f-dma_loop_s2f_run.png)


DMA Loop SRAM To FIFO Running

**3、**
遇到暂停地址，此时DMA停止数据的搬运，可根据Remain 寄存器\[((0x1C \+ 0x10\*n) \* 4\) bit\[16:0\]\] 进行判断是否还需要设置暂停地址在范围进行下次暂停。若不需要暂停，则把暂停地址设置在范围之外。

<a id="id29"></a>
![DMA single sramtsram3](../../../../../_assets/817d5299461d5f913d26-dma_loop_s2f_p.png)


DMA Loop SRAM To FIFO PAUSE

**4、**
直到搬运数据到总长度，才会报Finish 中断。此时停止的地址需要软件进行计算确认，硬件停在范围之内。

<a id="id30"></a>
![DMA single sramtsram3](../../../../../_assets/5e49c20757df951d79a1-dma_loop_s2f_f.png)


DMA Loop SRAM To FIFO Finish

**目的地址SRAM/源地址FIFO**

**1、**
loop模式下，要注意SRAM的起始和结束地址范围，需要软件进行计算暂停地址。若在传输过程中出现数据异常时，DMA\_EN置为0，再次启动时一定是从start\_address开始搬运数据。DMA会检测FIFO是否允许进行数据的搬运，若Not Ready，则停止在搬运到的位置等待ready。

<a id="id31"></a>
![DMA single sramtsram3](../../../../../_assets/0fe000795c4048ce7bcb-dma_loop_f2s_s.png)


DMA Loop FIFO To SRAM Start

**2、**
搬运数据到loop end address时，总长度还没有搬完。则回到loop start address开始搬运数据，直到遇到暂停地址。

<a id="id32"></a>
![DMA single sramtsram3](../../../../../_assets/a76e7bcde48533cf38f4-dma_loop_f2s_r.png)


DMA Loop FIFO To SRAM Running

**3、**
源地址为FIFO，目的地址为SRAM时，一般一定要配置暂停地址用于数据搬运。SRAM一般使用Ringbuffer的方式进行数据存取。

<a id="id33"></a>
![DMA single sramtsram3](../../../../../_assets/a12f47161fa788fb0a4f-dma_loop_f2s_p.png)


DMA Loop FIFO To SRAM Pause

**4、**
直到搬运数据到总长度，才会报Finish 中断。此时停止的地址需要软件进行计算确认，硬件停在范围之内。

<a id="id34"></a>
![DMA single sramtsram3](../../../../../_assets/88a62dff6165161921ee-dma_loop_f2s_f.png)


DMA Loop FIFO To SRAM Finish

<a id="dma-api"></a>

## DMA API 链接

> [DMA的驱动API](../../api-reference/peripheral/bk_dma.md)

<a id="id12"></a>

## DMA 使用参考代码

> [DMA API使用参考程序](../../examples/peripheral/bk_dma.md)
