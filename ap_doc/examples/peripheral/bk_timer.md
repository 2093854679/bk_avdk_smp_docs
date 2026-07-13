# TIMER



## 1 功能概述

通用定时器（Timer）可用于周期中断、硬件计数和短延时。BK7259 AP 侧对外支持 `TIMER_ID12` ~ `TIMER_ID17`，测试命令参数使用 `12` ~ `17`。


- Timer 功能具体描述参考：[Timer 驱动工作原理](../../developer-guide/peripheral/bk_timer.md "../../developer-guide/peripheral/bk_timer.md")


## 2 代码路径

> - Timer 测试代码：
>   :   `ap/middleware/driver/timer/timer_test.c`
> - 驱动源码：
>   :   `ap/middleware/driver/timer/timer_driver.c`
> - API 头文件：
>   :   `ap/include/driver/timer.h`
> - Kconfig：
>   :   `ap/middleware/driver/timer/Kconfig`
> - 默认配置：
>   :   `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig`


## 3 Timer 相关宏配置

| NAME | Description | File | value |
| --- | --- | --- | --- |
| `CONFIG_TIMER` | 使能 Timer 驱动 | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `y` |
| `CONFIG_TIMER_COUNTER` | 使能 Timer counter 能力 | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `y` |
| `CONFIG_TIMER_SUPPORT_ID_BITS` | 支持通道 bitmask；`0` 表示不按 bitmask 额外限制 | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `0` |
| `CONFIG_TIMER_US` | 使能 us 级 delay / timer API | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `y` |
| `CONFIG_TIMER_PM_CB_SUPPORT` | 低压睡眠回调支持 | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `n` |
| `CONFIG_TIMER_TEST` | 编译 `timer_test.c` 中的 Timer 测试命令 | `ap/middleware/driver/timer/Kconfig` | `y` |
| `CONFIG_CLI` | 系统命令框架；Timer 测试命令入口依赖该宏 | 项目配置 / 默认配置 | `y` |


## 4 Timer 通道配置说明

Timer 硬件不依赖 PIN 管脚，无需配置 GPIO。BK7259 AP 侧有 2 个 Timer group，共 6 个硬件通道；驱动 API 和测试命令使用 `TIMER_ID12` ~ `TIMER_ID17` 表示这些 AP Timer 通道。


## 5 Timer demo 配置

备注

当前 Timer 测试代码位于 `ap/middleware/driver/timer/timer_test.c`，不是旧的 `components/bk_cli/cli_timer.c`。`CONFIG_CLI` 只表示测试命令通过系统命令框架暴露给 shell。

demo 支持的命令如下表：

| Command | Param | Description |
| --- | --- | --- |
| `timer delay {us}` | `us`：延时时间，单位 us | 调用 `bk_delay_us()` 做阻塞延时。 |
| `timer {id} start {period_ms}` | `id`：AP 支持 `12` ~ `17`；`period_ms`：中断周期，单位 ms | 启动指定 Timer，并在每个周期触发测试 ISR。 |
| `timer {id} read` | `id`：Timer ID | 读取 Timer 当前计数值。 |
| `timer {id} get_period` | `id`：Timer ID | 读取周期寄存器值。 |
| `timer {id} stop` | `id`：Timer ID | 停止 Timer 并关闭中断。 |
| `timer {id} enable` | `id`：Timer ID | 使能 Timer 计数。 |
| `timer {id} disable` | `id`：Timer ID | 禁止 Timer 计数。 |


## 6 Timer demo 命令行演示

AP 侧 Timer 测试命令在 CP shell 下执行时需要添加 `ap_cmd` 前缀，以下示例使用 `TIMER_ID12`。

1. 启动一个可用的 AP Timer 通道。

   > **ap_cmd timer 12 start 2000**
   > :   ```
   >     [17:57:43.344]发->◇ap_cmd timer 12 start 2000
   >     [17:57:43.350]收<-◆ap_cmd timer 12 start 2000
   >     $ap0:cli:I(3810):[TIMER][START] channel:12, time_ms:2000
   >     [17:57:45.352]收<-◆ap0:cli:I(5810):[TIMER][ISR] chan:12
   >     [17:57:47.352]收<-◆ap0:cli:I(7810):[TIMER][ISR] chan:12
   >     [17:57:49.352]收<-◆ap0:cli:I(9810):[TIMER][ISR] chan:12
   >     ```
2. 获取指定通道的 timer count 值。

   > **ap_cmd timer 12 read**
   > :   ```
   >     [18:01:47.242]发->◇ap_cmd timer 12 read
   >     [18:01:47.248]收<-◆ap_cmd timer 12 read
   >     $ap0:cli:I(247706):[TIMER][READ] read cnt:2f025f5
   >     ```
3. 获取指定通道的周期寄存器值。

   > **ap_cmd timer 12 get_period**
   > :   ```
   >     [18:02:26.882]发->◇ap_cmd timer 12 get_period
   >     [18:02:26.888]收<-◆ap_cmd timer 12 get_period
   >     $ap0:cli:I(287346):[TIMER][GET][PERIOD] period value:3197500
   >     ```
4. 停止指定通道计数，并关闭其中断。

   > **ap_cmd timer 12 stop**
   > :   ```
   >     [19:28:30.946]发->◇ap_cmd timer 12 stop
   >     [19:28:30.951]收<-◆ap_cmd timer 12 stop
   >     $ap0:cli:I(5451368):[TIMER][STOP] channel:12
   >     ```
5. 使能指定通道计数。

   > **ap_cmd timer 12 enable**
   > :   ```
   >     [19:32:15.802]发->◇ap_cmd timer 12 enable
   >     [19:32:15.807]收<-◆ap_cmd timer 12 enable
   >     $ap0:cli:I(5676222):[TIMER][ENABLE] channel:12
   >     [19:32:17.811]收<-◆ap0:cli:I(5678222):[TIMER][ISR] chan:12
   >     [19:32:19.809]收<-◆ap0:cli:I(5680222):[TIMER][ISR] chan:12
   >     ```
6. 关闭指定通道计数。

   > **ap_cmd timer 12 disable**
   > :   ```
   >     [19:31:36.980]发->◇ap_cmd timer 12 disable
   >     [19:31:36.986]收<-◆ap_cmd timer 12 disable
   >     $ap0:cli:I(5637400):[TIMER][DISABLE] channel:12
   >     ```
