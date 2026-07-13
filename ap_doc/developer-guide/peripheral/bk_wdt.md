# Watchdog 使用指南



## 概述

watchdog 实际上是一个硬件定时器，定时器超时会触发系统 watchdog 重启。

BK7259 AP 侧没有独立的 AON_WDT 硬件驱动，AON_WDT 由 CP 侧管理。AP 侧 watchdog 相关能力分为两类：

> - `wwdt`：与 CPU 核绑定的硬件 Window Watchdog，承担 **Interrupt Watchdog** 角色。
> - `task_wdt`：软件实现的 **Task Watchdog**，不依赖 `bk_wdt_start()` / `bk_wdt_feed()` 这类 AON_WDT 兼容接口。


## watchdog 使用方法

watchdog 有两种常见的使用方式：

> - 在周期性中断中喂狗，如在 OS SysTick 中断中喂 `wwdt`。当软件出现关中断过长、SysTick 未能及时喂狗等问题时，`wwdt` 超时会触发 watchdog 重启，用于及时发现中断层面的异常。这类用法通常称为 **interrupt watchdog**。
> - 在周期性任务中喂狗，如在 idle task 中调用 `bk_task_wdt_feed()`。idle task 一般为系统中优先级最低的任务；当某个任务长期占用 CPU、idle 无法得到调度时，`task_wdt` 会检测到喂狗超时。这类用法通常称为 **task watchdog**。


## ARMINO Interrupt Watchdog（`wwdt`）

BK7259 AP 使用 `wwdt` 实现 Interrupt Watchdog。`wwdt` 与 CPU 核一一绑定，SMP 场景下各核通常各自对应一套独立的 `wwdt` 实例。

默认情况下，`wwdt` 会在 SysTick 路径中通过 `bk_wwdt_feed_current_core_from_isr()` 自动启动并周期性喂狗。超时时间由 `CONFIG_INT_WWDT_PERIOD_MS` 配置（默认 `2000` ms，即约 2 s），可在 menuconfig 中调整，或由 `CONFIG_SUPPORT_WWDT` 关闭。若 `wwdt` 超时，将触发硬件 watchdog 重启。

`bk_wwdt_feed()` 可重置当前核的 `wwdt` 定时器。驱动实现位于 `ap/middleware/driver/wwdt/wwdt_driver.c`。

备注

`wwdt` 触发超时（默认约 2 s）后，CPU 会进入 **NMI** 异常，随后从 Flash 复位启动。默认复位起始地址为 Flash `0x0`；该起始地址可通过 SYS 模块 reg4 的 bit[31:8]（`cpu0_offset` 字段）配置，实际启动地址为 `cpu0_offset * 256`。

备注

当 CPU 处于 off 状态时，`wwdt` 会掉电，计数值会归零；上电后硬件默认超时周期恢复为 ``` 0x4000``（约 500 ms，基于 32 kHz 时钟源）。CPU 重新上电后，``wwdt ``` 会在 SysTick 路径中自动启动并开始运行。

备注

通常应用不应关闭 Interrupt Watchdog。若应用需要完全自行实现 interrupt watchdog，请通过 menuconfig 关闭 `CONFIG_SUPPORT_WWDT`，或调用对外 API `bk_wwdt_stop()` 停止当前核 ``` wwdt``（内部会关闭硬件并设置 ``auto_start_disabled ```，禁止 SysTick 再次自动启动）。`bk_wwdt_close()` 为驱动内部接口，测试命令 `wwdt close` 会调用它，应用侧一般使用 `bk_wwdt_stop()` 即可。

备注

AP 侧没有 `wdt` / `aon_wdt` 测试命令。`wwdt` 测试代码位于 `ap/middleware/driver/wwdt/wwdt_test.c`。在 CP shell 下访问 AP 侧命令时需添加 `ap_cmd` 前缀。


## ARMINO Task Watchdog（`task_wdt`）

ARMINO 在 AP 侧也实现了 Task Watchdog，但并不是基于真正硬件 Watchdog，即不是基于 `bk_wwdt_start()` / `bk_wwdt_feed()` 实现。具体实现方式如下：

全局数组 `s_last_task_wdt_feed_tick[]` 记录各 SMP core 最近一次喂狗 tick；在 idle task 入口调用 `bk_task_wdt_feed()` 更新对应 core 的喂狗时间；在 SysTick 中断中通过 `bk_task_wdt_systick_check()` 周期检查距上次喂狗是否超出 ``` CONFIG_TASK_WDT_PERIOD_MS``（默认 ``60000 ``` ms）。若超时，会打印 `task watchdog triggered` 并通过 `BK_ASSERT(0)` 触发断言，用于定位任务调度异常。

驱动实现位于 `ap/middleware/driver/wdt/task_wdt.c`。

备注

通常应用应使能 task watchdog。除非应用自行实现 task watchdog，可通过 menuconfig 中 `CONFIG_TASK_WDT` 关闭系统默认的 task watchdog。


## 相关代码路径

> - `task_wdt` 驱动：`ap/middleware/driver/wdt/task_wdt.c`
> - `task_wdt` 测试代码：`ap/middleware/driver/wdt/task_wdt_test.c`
> - `task_wdt` Kconfig：`ap/middleware/driver/wdt/Kconfig`
> - `wwdt` 驱动：`ap/middleware/driver/wwdt/wwdt_driver.c`
> - `wwdt` 测试代码：`ap/middleware/driver/wwdt/wwdt_test.c`
> - `wwdt` API 头文件：`ap/include/driver/wwdt.h`
> - `wwdt` 类型定义：`ap/include/driver/wwdt_types.h`、`ap/include/driver/hal/hal_wwdt_types.h`
> - 默认配置：`ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig`


## 配置宏

| 宏 | BK7259 AP 默认值 | 说明 |
| --- | --- | --- |
| `CONFIG_TASK_WDT` | `y` | 使能 AP `task_wdt`。 |
| `CONFIG_TASK_WDT_PERIOD_MS` | `60000` | `task_wdt` 超时时间，单位 ms。 |
| `CONFIG_TASK_WDT_TEST` | `y` | 在 `CONFIG_CLI` 和 `DRIVER_TEST` 使能时编译 `task_wdt_test.c`。 |
| `CONFIG_SUPPORT_WWDT` | `y` | 使能 AP `wwdt` 驱动。 |
| `CONFIG_INT_WWDT_PERIOD_MS` | `2000` | `wwdt` 默认中断看门狗周期，单位 ms。 |
| `CONFIG_WWDT_TEST` | `y` | 在 `CONFIG_CLI` 和 `DRIVER_TEST` 使能时编译 `wwdt_test.c`。 |


## 测试与示例

AP 侧 CLI 测试命令在 CP shell 下需加 `ap_cmd` 前缀（例如 `ap_cmd task_wdt status`）。命令依赖 `CONFIG_CLI`、`DRIVER_TEST`，以及 `CONFIG_TASK_WDT_TEST`、`CONFIG_WWDT_TEST`。

完整命令列表、参数说明和串口演示见 [Watchdog](../../examples/peripheral/bk_wdt.md "../../examples/peripheral/bk_wdt.md")。`wwdt` API 参考见 [Watchdog](../../api-reference/peripheral/bk_wdt.md "../../api-reference/peripheral/bk_wdt.md")。
