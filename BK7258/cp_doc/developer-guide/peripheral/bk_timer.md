---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_timer.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="timer"></a>

# Timer使用指南

<a id="id1"></a>

## 1 功能概述

> ```
> 通用定时器组Timer0和Timer1各包含三个定时器，每个定时器有一个32位递增计数器。
> 每个定时器组的三个计数器由一个4位预分频器驱动。
> 通用定时器可用于在达到设定的周期后触发中断或充当硬件时钟。
> ```
>
> - Timer相关demo和配置介绍: [Timer相关demo和配置介绍](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_timer.html)

<a id="id2"></a>

## 2 Timer特性

> ```
> 每个 TIMG 模块具有如下特性：
> - 3 个定时器 (Timer0/1/2)
> - 3 个 32 位递增计数器
> - 可读取计数器的实时值
> - 4 位预分频器，用于对计数器时钟频率进行分频，分频系数介于 1 到 16之间
> ```

<a id="id3"></a>

## 3 Timer功能说明

<a id="id4"></a>
![timer](../../../../../_assets/7ac5520a5f1bd72078bf-timer_basic.png)


Figure 1\. 通用定时器组框图

Figure 1显示了通用定时器组的概览。

> ```
> - 时钟选择与预分频器
>   每个定时器组可以选择低功耗的32 kHz 时钟 (LPO_CLK) 或26 MHz 的外部时钟 (XTAL) 作为时钟源。时钟源的选择在系统模块中进行配置。
>   定时器组包含一个 4 位预分频器。时钟源经该预分频器分频，产生计数器使用的计数器时钟。
>   4 位预分频器的分频系数可通过 CLK_DIV 字段配置，选取从 1 到 16之间的任意值。
>
>
> - 32 位计数器
>   定时器组的主要模块由三个 32 位的递增计数器及其相关的计数器值寄存器组成。计数器采用递增方式计数。
>   当计数器启动位 (TIMERx_EN) 置 1 时，相应计数器才会启动。
>   在递增计数模式下，计数器从 0 计数到寄存器 TIMERx_VAL 设置的值，然后重新从 0 开始计数并生成计数器上溢事件。
>
>
> - 使用通用定时器组的步骤
>     若要使用通用定时器组，请执行以下步骤：
>       1) 配置定时器
>         a. 在系统模块配置相关位选择时钟源
>         b. 设置CLK_DIV 的值以配置 4 位预分频器
>         c. 在TIMERx_VAL 寄存器上写值设置相应定时器的计数周期
>       2) 置位 TIMERx_EN 使能相应定时器
>       3) 读取相应定时器的当前值
>         a. 配置 TIMERL_INDEX 选择要读取当前值的定时器
>         b. 置位 TIMERL_CNT_READ 将锁存定时器的当前值
>         c. 从 TIMERL_CNT 读取锁存的定时器的当前值
>
> - Timer中断
>     置位TIMERx_INT可使能相应定时器的中断。
>     定时器每次产生的电平中断必须由 CPU 清除。电平中断在超时后触发。超时后，电平中断会一直被拉高，直至手动清除中断。
> ```
