---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_timer.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="timer"></a>

# TIMER

<a id="id1"></a>

## 1 功能概述

> ```
> 通用定时器组Timer0和Timer1各包含三个定时器，每个定时器有一个32位递增计数器。
> 每个定时器组的三个计数器由一个4位预分频器驱动。
> 通用定时器可用于在达到设定的周期后触发中断或充当硬件时钟。
> ```
>
> - Timer功能具体描述参考: [Timer驱动工作原理](../../developer-guide/peripheral/bk_timer.md)

<a id="id3"></a>

## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_timer.c`
> - 驱动源码路径：
>   :   `middleware\driver\timer\timer_driver.c`

<a id="id4"></a>

## 3 Timer相关宏配置

<a id="id7"></a>

Timer相关宏配置


| NAME | Description | File | value |
| --- | --- | --- | --- |
| CONFIG\_TIMER | Timer驱动及其测试命令使能配置 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
| CONFIG\_TIMER\_SUPPORT\_ID\_BITS | 用于在多个CPU间划分Timer通道 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | 56 |
| CONFIG\_TIMER\_US | Timer使能us级别的delay函数API | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
| CONFIG\_TIMER\_PM\_CB\_SUPPORT | Timer使能低功耗投票功能 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | n |

<a id="id5"></a>

## 4 Timer 通道配置说明

> ```
> Timer硬件不依赖于PIN管脚，无需配置对应的GPIO。
> 由于Timer有两个定时器组Timer0和Timer1，各包含三个定时器，因此共有6个定时器通道。
> SDK将定时器定义为Timer通道 Channel 0 ~ 5，在CPU间划分如下。
> 对于CP： Channel 0 ~ 2, 其中通道2被默认用作喂狗的定时器；
> 对于AP： Channel 3 ~ 5；
> ```

<a id="timer-demo"></a>

## 5 Timer demo 配置

> - demo支持的命令如下表：

<a id="id8"></a>

Timer命令格式描述


| Command | Param | Description |
| --- | --- | --- |
| **timer {id} start {period}** | {id}: timer channel id, range 3\~5 in ap subsys {period}: the period for timer trigger interrupt callback, the unit is millisecond | Enable timer channel and it would trigger interrupt every period. |
| **timer {id} read** | {id}: timer channel id | Read the timer channel count value |
| **timer {id} get\_period** | {id}: timer channel id | Read the timer channel period value in register |
| **timer {id} stop** | {id}: timer channel id | Stop the timer and disable the timer interrupt |
| **timer {id} enable** | {id}: timer channel id | Enable timer set to 1 |
| **timer {id} disable** | {id}: timer channel id | Stop the timer, Enable timer set to 0 |

<a id="id6"></a>

## 6 Timer demo 命令行演示

> 1. bk7258启动开发板，启动其中一个可用的timer通道，样例以通道3为例。
>
> > - master： **cpu1 timer 3 start 2000**
> >
> >   > ```
> >   > [17:57:43.344]发→◇cpu1 timer 3 start 2000
> >   > [17:57:43.350]收←◆cpu1 timer 3 start 2000
> >   > $
> >   > $cpu1:cli:I(3810):[TIMER][START] channel:3, time_ms:2000
> >   > [17:57:45.352]收←◆cpu1:cli:I(5810):[TIMER][ISR] chan:3
> >   > [17:57:47.352]收←◆cpu1:cli:I(7810):[TIMER][ISR] chan:3
> >   > [17:57:49.352]收←◆cpu1:cli:I(9810):[TIMER][ISR] chan:3
> >   > ```
>
> 2. 获取指定通道的timer count值
>
> > - master： **cpu1 timer 3 read**
> >
> >   > ```
> >   > [18:01:47.242]发→◇cpu1 timer 3 read
> >   > [18:01:47.248]收←◆cpu1 timer 3 read
> >   > $cpu1:cli:I(247706):[TIMER][READ] read cnt:2f025f5
> >   > ```
>
> 3. 获取指定通道的timer根据ms转换后的周期寄存器值
>
> > - master： **cpu1 timer 3 get\_period**
> >
> >   > ```
> >   > [18:02:26.882]发→◇cpu1 timer 3 get_period
> >   > [18:02:26.888]收←◆cpu1 timer 3 get_period
> >   > $cpu1:cli:I(287346):[TIMER][GET][PERIOD] period value:3197500
> >   > ```
>
> 4. 停止指定通道的timer计数，并关闭其中断
>
> > - master： **cpu1 timer 3 stop**
> >
> >   > ```
> >   > [19:28:30.946]发→◇cpu1 timer 3 stop
> >   > [19:28:30.951]收←◆cpu1 timer 3 stop
> >   > $cpu1:cli:I(5451368):[TIMER][STOP] channel:3
> >   > ```
>
> 5. 使能指定通道的timer计数
>
> > - master： **cpu1 timer 3 enable**
> >
> >   > ```
> >   > [19:32:15.802]发→◇cpu1 timer 3 enable
> >   > [19:32:15.807]收←◆cpu1 timer 3 enable
> >   > $cpu1:cli:I(5676222):[TIMER][ENABLE] channel:3
> >   > [19:32:17.811]收←◆cpu1:cli:I(5678222):[TIMER][ISR] chan:3
> >   > [19:32:19.809]收←◆cpu1:cli:I(5680222):[TIMER][ISR] chan:3
> >   > ```
>
> 6. 关闭指定通道的timer计数
>
> > - master： **cpu1 timer 3 disable**
> >
> >   > ```
> >   > [19:31:36.980]发→◇cpu1 timer 3 disable
> >   > [19:31:36.986]收←◆cpu1 timer 3 disable
> >   > $cpu1:cli:I(5637400):[TIMER][DISABLE] channel:3
> >   > ```
