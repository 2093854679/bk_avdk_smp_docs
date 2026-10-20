---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_timer.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="timer"></a>

# Timer使用指南

<a id="id1"></a>

## 概述

通用定时器（Timer）用于周期中断、硬件计数和短延时。BK7259 AP 侧共有 6 个硬件 Timer 通道，按 2 个 Timer group 组织，每组 3 个通道；在 AP 驱动中对外暴露为 `TIMER_ID12` \~ `TIMER_ID17`，对应命令参数 `12` \~ `17`。

备注

AP 侧 Timer 测试命令由 `ap/middleware/driver/timer/timer_test.c` 导出，不是旧的 `components/bk_cli/cli_timer.c`。文档中出现 `CONFIG_CLI` 仅表示这些测试命令通过系统命令框架暴露给 shell。SMP 串口在 CP shell 下访问 AP 命令时，需要添加 `ap_cmd` 前缀，例如 `ap_cmd timer 12 start 2000`。

<a id="id2"></a>

## Timer 特性

> - 每个 Timer group 包含 3 个 32 bit 递增计数器。
> - 计数器可配置周期值，达到周期后触发中断并重新计数。
> - 支持读取当前计数值、启动、停止、enable/disable 计数。
> - 计数时钟支持 32 kHz 和 26 MHz 时钟源，AP 测试命令当前未开放 `clk_src` 子命令。
> - `CONFIG_TIMER_US=y` 时提供 `bk_delay_us()`、`bk_timer_start_us()` 等 us 级接口。

<a id="id3"></a>

## 相关代码路径

> - API 头文件：`ap/include/driver/timer.h`
> - 类型定义：`ap/include/driver/timer_types.h`、`ap/include/driver/hal/hal_timer_types.h`
> - 能力定义：`ap/include/soc/bk7259/timer_cap.h`
> - 驱动源码：`ap/middleware/driver/timer/timer_driver.c`
> - Timer 测试代码：`ap/middleware/driver/timer/timer_test.c`
> - Kconfig：`ap/middleware/driver/timer/Kconfig`
> - 默认配置：`ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig`

<a id="id4"></a>

## 配置宏

| 宏 | BK7259 AP 默认值 | 说明 |
| --- | --- | --- |
| `CONFIG_TIMER` | `y` | 使能 Timer 驱动。 |
| `CONFIG_TIMER_COUNTER` | `y` | 使能 Timer counter 能力。 |
| `CONFIG_TIMER_SUPPORT_ID_BITS` | `0` | 支持通道 bitmask。`0` 表示不按 bitmask 额外限制；AP 驱动仍只支持 `TIMER_ID12` \~ `TIMER_ID17`。 |
| `CONFIG_TIMER_US` | `y` | 使能 us 级 delay / timer API。使用该能力时 `TIMER_ID0` 会被 us timer 逻辑保留，但 AP 侧本身不支持 `TIMER_ID0`。 |
| `CONFIG_TIMER_PM_CB_SUPPORT` | `n` | 低压睡眠回调支持，默认关闭。 |
| `CONFIG_TIMER_TEST` | `y` | 使能 `timer_test.c` 中的 Timer 测试命令；实际编译还要求 `CONFIG_CLI=y`。 |

<a id="ap"></a>

## AP 侧测试命令

| 命令 | 说明 |
| --- | --- |
| `timer delay {us}` | 调用 `bk_delay_us()` 做 us 级阻塞延时。 |
| `timer {id} start {period_ms}` | 启动指定 Timer，按 `period_ms` 周期触发中断。AP 支持 `id` 为 `12` \~ `17`。 |
| `timer {id} read` | 读取指定 Timer 当前计数值。 |
| `timer {id} get_period` | 读取 `bk_timer_start()` 设置后换算得到的周期寄存器值。 |
| `timer {id} stop` | 停止指定 Timer 并关闭中断。 |
| `timer {id} enable` | 使能指定 Timer 计数。 |
| `timer {id} disable` | 禁止指定 Timer 计数。 |

<a id="id5"></a>

## Timer 功能说明

<a id="id6"></a>
![timer](../../../../_assets/e9bd4a02d2f71c1d6ec1-timer_basic.png)


Figure 1\. 通用定时器组框图

Figure 1 显示了通用定时器组的概览。

> - 时钟选择与预分频器：每个定时器组可以选择低功耗 32 kHz 时钟或 26 MHz XTAL 作为时钟源。计数器时钟由预分频器分频后提供。
> - 32 bit 计数器：计数器启动后从 0 递增到周期寄存器值，随后重新计数并触发中断。
> - 中断处理：Timer 超时后产生电平中断，驱动 ISR 负责清中断并调用用户 callback。

Timer 相关测试和使用介绍：[Timer 测试用例](../../examples/peripheral/bk_timer.md)
