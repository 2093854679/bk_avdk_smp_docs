# TIMER



## 1 功能概述

通用定时器（Timer）可用于周期中断、硬件计数和短延时。BK7259 CP 侧对外支持 `TIMER_ID0` ~ `TIMER_ID11`，测试命令参数使用 `0` ~ `11`。


- Timer 功能具体描述参考：[Timer 驱动工作原理](../../developer-guide/peripheral/bk_timer.md "../../developer-guide/peripheral/bk_timer.md")


## 2 代码路径

> - Timer 测试代码：
>   :   `cp/middleware/driver/timer/timer_test.c`
> - 驱动源码：
>   :   `cp/middleware/driver/timer/timer_driver.c`
> - API 头文件：
>   :   `cp/include/driver/timer.h`
> - Kconfig：
>   :   `cp/middleware/driver/timer/Kconfig`
> - 默认配置：
>   :   `cp/middleware/soc/bk7259/bk7259.defconfig`


## 3 Timer 相关宏配置

| NAME | Description | File | value |
| --- | --- | --- | --- |
| `CONFIG_TIMER` | 使能 Timer 驱动 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_TIMER_COUNTER` | 使能 Timer counter 能力 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_TIMER_SUPPORT_ID_BITS` | 支持通道 bitmask；`0` 表示不按 bitmask 额外限制 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `0` |
| `CONFIG_TIMER_US` | 使能 us 级 delay / timer API | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_TIMER_PM_CB_SUPPORT` | 低压睡眠回调支持 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `n` |
| `CONFIG_TIMER_TEST` | 编译 `timer_test.c` 中的 Timer 测试命令 | `cp/middleware/driver/timer/Kconfig` | `y` |
| `CONFIG_CLI` | 系统命令框架；Timer 测试命令入口依赖该宏 | 项目配置 / 默认配置 | `y` |


## 4 Timer 通道配置说明

Timer 硬件不依赖 PIN 管脚，无需配置 GPIO。BK7259 CP 侧有 4 个硬件 Timer 模块（Timer group），每个模块包含 3 个通道，共 12 个 Timer 通道；驱动 API 和测试命令使用 `TIMER_ID0` ~ `TIMER_ID11` 表示这些 CP Timer 通道。


## 5 Timer demo 配置

备注

当前 Timer 测试代码位于 `cp/middleware/driver/timer/timer_test.c`，不是旧的 `components/bk_cli/cli_timer.c`。`CONFIG_CLI` 只表示测试命令通过系统命令框架暴露给 shell。

demo 支持的命令如下表：

| Command | Param | Description |
| --- | --- | --- |
| `timer delay {us}` | `us`：延时时间，单位 us | 调用 `bk_delay_us()` 做阻塞延时。 |
| `timer {id} start {period_ms}` | `id`：CP 支持 `0` ~ `11`；`period_ms`：中断周期，单位 ms | 启动指定 Timer，并在每个周期触发测试 ISR。 |
| `timer {id} clk_src {src}` | `id`：Timer 通道 ID；`src`：`0` 为 32 kHz，`1` 为 26 MHz XTAL | 驱动通过 `id / 3` 定位该通道所属的硬件 Timer 模块，并切换该模块的时钟源。 |
| `timer {id} read` | `id`：Timer ID | 读取 Timer 当前计数值。 |
| `timer {id} get_period` | `id`：Timer ID | 读取周期寄存器值。 |
| `timer {id} stop` | `id`：Timer ID | 停止 Timer 并关闭中断。 |
| `timer {id} enable` | `id`：Timer ID | 使能 Timer 计数。 |
| `timer {id} disable` | `id`：Timer ID | 禁止 Timer 计数。 |


## 6 Timer demo 命令行演示

以下示例使用 `TIMER_ID1`，避免和 `CONFIG_TIMER_US` 下的 us timer 逻辑抢占 `TIMER_ID0`。

> **timer 1 start 2000**
> :   ```
>     [17:57:43.344]发->◇timer 1 start 2000
>     [17:57:43.350]收<-◆timer 1 start 2000
>     $cli:I(3810):[TIMER][START] channel:1, time_ms:2000
>     [17:57:45.352]收<-◆cli:I(5810):[TIMER][ISR] chan:1 clk:1
>     ```
>
> **timer 1 clk_src 0**
> :   ```
>     [17:58:12.100]发->◇timer 1 clk_src 0
>     [17:58:12.106]收<-◆timer 1 clk_src 0
>     $cli:I(6710):[TIMER][SET_CLOCK_SRC] 0-32K 1-xtal, clk_src:0
>     ```
>
> **timer 1 read**
> :   ```
>     [18:01:47.242]发->◇timer 1 read
>     [18:01:47.248]收<-◆timer 1 read
>     $cli:I(247706):[TIMER][READ] read cnt:2f025f5
>     ```
>
> **timer 1 get_period**
> :   ```
>     [18:02:26.882]发->◇timer 1 get_period
>     [18:02:26.888]收<-◆timer 1 get_period
>     $cli:I(287346):[TIMER][GET][PERIOD] period value:3197500
>     ```
>
> **timer 1 stop**
> :   ```
>     [19:28:30.946]发->◇timer 1 stop
>     [19:28:30.951]收<-◆timer 1 stop
>     $cli:I(5451368):[TIMER][STOP] channel:1
>     ```
