---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_wdt.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="watchdog"></a>

# Watchdog 使用指南

<a id="id1"></a>

## 概述

watchdog 实际上是一个硬件定时器，定时器超时会触发系统 watchdog 重启。

`bk_wdt_start(timeout_ms)` 可设置 AON\_WDT 兼容封装的 watchdog 定时器时间，目前时间配置范围为 `(1~0xFFFFFF)`；`bk_wdt_feed()` 可重置 watchdog 定时器。

BK7259 CP 侧同时提供 AON\_WDT 兼容封装、`wwdt` 和 `task_wdt` 三类能力：

> - `aon_wdt` / `bk_wdt_*`：AON Watchdog 及其兼容 API，由 `cp/middleware/driver/wdt/wdt_driver.c` 封装；`cp/middleware/driver/aon_wdt/aon_wdt_driver.c` 提供 `bk_aon_wdt_*` 专用 API。
> - `wwdt`：与 CPU 核绑定的硬件 Window Watchdog，承担 **Interrupt Watchdog** 角色。
> - `task_wdt`：软件实现的 **Task Watchdog**，不依赖 `bk_wdt_start()` / `bk_wdt_feed()` 实现。

<a id="id2"></a>

## watchdog 使用方法

watchdog 有两种常见的使用方式：

> - 在周期性中断或定时器中喂狗，如在 `TIMER_ID2` 中断中调用 `bk_wdt_feed_handle()` 喂 AON\_WDT，或在 SysTick 中断中喂 `wwdt`。当软件出现关中断过长、定时中断未能及时喂狗等问题时，硬件 watchdog 超时会触发系统重启，用于及时发现中断层面的异常。这类用法通常称为 **interrupt watchdog**。
> - 在周期性任务中喂狗，如在 idle task 中调用 `bk_task_wdt_feed()`。idle task 一般为系统中优先级最低的任务；当某个任务长期占用 CPU、idle 无法得到调度时，`task_wdt` 会检测到喂狗超时。这类用法通常称为 **task watchdog**。

<a id="armino-interrupt-watchdog"></a>

## ARMINO Interrupt Watchdog

BK7259 CP 提供两层 Interrupt Watchdog 能力：

<a id="aon-wdt-bk-wdt"></a>

### AON\_WDT 兼容封装（`bk_wdt_*`）

在 ARMINO 中，默认情况下 AON\_WDT 兼容封装的 Interrupt Watchdog 是使能的（`CONFIG_INT_WDT`）。`bk_wdt_driver_init()` 初始化运行时资源，并在 `CONFIG_INT_WDT` 或 `CONFIG_TASK_WDT` 使能时启动 `TIMER_ID2`，周期调用 `bk_wdt_feed_handle()` 喂狗。可通过 menuconfig 中 `CONFIG_INT_WDT_PERIOD_MS` 设置超时时间（默认 `8000` ms），或通过 `CONFIG_INT_WDT` 关闭该路径。

`bk_wdt_start(timeout_ms)` 设置 AON\_WDT 周期并启动硬件，`bk_wdt_feed()` 通过重新配置 AON\_WDT 周期完成喂狗。BK7259 上 `bk_wdt_*` 是 AON\_WDT 的兼容封装，不代表 CP 侧存在独立于 AON\_WDT 的另一类 WDT。

备注

当应用需要完全自己实现基于 AON\_WDT 的 interrupt watchdog 时，请通过 menuconfig 关闭 `CONFIG_INT_WDT`。

<a id="wwdt"></a>

### `wwdt`

`wwdt` 与 CPU 核一一绑定，SMP 场景下各核通常各自对应一套独立的 `wwdt` 实例。默认在 SysTick 路径中通过 `bk_wwdt_feed_current_core_from_isr()` 自动启动并周期性喂狗。超时时间由 `CONFIG_INT_WWDT_PERIOD_MS` 配置（默认 `2000` ms），可在 menuconfig 中调整，或由 `CONFIG_SUPPORT_WWDT` 关闭。若 `wwdt` 超时，将触发硬件 watchdog 重启。

备注

`wwdt` 触发超时（默认约 2 s）后，CPU 会进入 **NMI** 异常，随后从 Flash 复位启动。默认复位起始地址为 Flash `0x0`；该起始地址可通过 SYS 模块 reg4 的 bit\[31:8\]（`cpu0_offset` 字段）配置，实际启动地址为 `cpu0_offset * 256`。

备注

当 CPU 处于 off 状态时，`wwdt` 会掉电，计数值会归零；上电后硬件默认超时周期恢复为 ``` 0x4000``（约 500 ms，基于 32 kHz 时钟源）。CPU 重新上电后，``wwdt ``` 会在 SysTick 路径中自动启动并开始运行。

驱动实现位于 `cp/middleware/driver/wwdt/wwdt_driver.c`。

备注

CP 侧测试命令不在旧的 `components/bk_cli/cli_wdt.c` 中。AON\_WDT 兼容测试命令 `wdt` 来自 `cp/middleware/driver/wdt/wdt_test.c`，`wwdt` 测试命令来自 `cp/middleware/driver/wwdt/wwdt_test.c`，`task_wdt` 测试命令来自 `cp/middleware/driver/wdt/task_wdt_test.c`。

<a id="armino-task-watchdog-task-wdt"></a>

## ARMINO Task Watchdog（`task_wdt`）

ARMINO 在 CP 侧也实现了 Task Watchdog，但并不是基于真正硬件 Watchdog，即不是基于 `bk_wdt_start()` / `bk_wdt_feed()` 实现。具体实现方式如下：

全局数组 `s_last_task_wdt_feed_tick[]` 记录各 core 最近一次喂狗 tick；在 idle task 入口调用 `bk_task_wdt_feed()` 更新喂狗时间；在 SysTick 中断中通过 `bk_task_wdt_systick_check()` 周期检查是否超出 ``` CONFIG_TASK_WDT_PERIOD_MS``（默认 ``60000 ``` ms）。若超时，会打印 `task watchdog triggered` 并通过 `BK_ASSERT(0)` 触发断言，用于定位任务调度异常。

驱动实现位于 `cp/middleware/driver/wdt/task_wdt.c`。

备注

通常应用应使能 task watchdog。除非应用自行实现 task watchdog，可通过 menuconfig 中 `CONFIG_TASK_WDT` 关闭系统默认的 task watchdog。

<a id="aon-wdt-api"></a>

## AON\_WDT 专用 API

`bk_aon_wdt_get_period()`、`bk_aon_wdt_set_period()`、`bk_aon_wdt_feed()` 和 `bk_aon_wdt_stop()` 直接操作 AON\_WDT。`CONFIG_INT_AON_WDT` 使能时还提供 `bk_aon_wdt_get_feed_time()` 和 `bk_aon_wdt_set_feed_time()`，可通过 menuconfig 中 `CONFIG_INT_AON_WDT_PERIOD_MS` 配置默认周期（默认 `8000` ms）。

<a id="id3"></a>

## 相关代码路径

> - AON\_WDT 兼容封装驱动：`cp/middleware/driver/wdt/wdt_driver.c`
> - AON\_WDT 兼容测试代码：`cp/middleware/driver/wdt/wdt_test.c`
> - AON\_WDT 兼容 API 测试代码：`cp/middleware/driver/wdt/cli_wdt_api.c`
> - `task_wdt` 驱动：`cp/middleware/driver/wdt/task_wdt.c`
> - `task_wdt` 测试代码：`cp/middleware/driver/wdt/task_wdt_test.c`
> - AON\_WDT 专用驱动：`cp/middleware/driver/aon_wdt/aon_wdt_driver.c`
> - AON\_WDT API 头文件：`cp/include/driver/aon_wdt.h`
> - `wwdt` 驱动：`cp/middleware/driver/wwdt/wwdt_driver.c`
> - `wwdt` 测试代码：`cp/middleware/driver/wwdt/wwdt_test.c`
> - `wwdt` API 头文件：`cp/include/driver/wwdt.h`
> - 默认配置：`cp/middleware/soc/bk7259/bk7259.defconfig`

<a id="id4"></a>

## 配置宏

| 宏 | BK7259 CP 默认值 | 说明 |
| --- | --- | --- |
| `CONFIG_WDT_EN` | `y` | 使能 AON\_WDT 兼容封装驱动。 |
| `CONFIG_INT_WDT` | `y` | 使能 AON\_WDT 兼容 interrupt watchdog。 |
| `CONFIG_SUPPORT_AON_WDT` | `y` | AON\_WDT 兼容封装使用 AON\_WDT 后端。 |
| `CONFIG_INT_WDT_PERIOD_MS` | `8000` | AON\_WDT 兼容封装默认周期，单位 ms。 |
| `CONFIG_TASK_WDT` | `y` | 使能 `task_wdt`。 |
| `CONFIG_TASK_WDT_PERIOD_MS` | `60000` | `task_wdt` 超时时间，单位 ms。 |
| `CONFIG_WDT_TEST` | `y` | 在 `CONFIG_CLI` 和 `DRIVER_TEST` 使能时编译 `wdt_test.c`。 |
| `CONFIG_WDT_API_TEST` | `n` | 编译 `cli_wdt_api.c` 中的 argtable API 测试命令。 |
| `CONFIG_AON_WDT` | `y` | 使能 AON\_WDT 专用驱动。 |
| `CONFIG_INT_AON_WDT` | `y` | 使能 AON\_WDT interrupt watchdog。 |
| `CONFIG_INT_AON_WDT_PERIOD_MS` | `8000` | AON\_WDT 默认周期，单位 ms。 |
| `CONFIG_SUPPORT_WWDT` | `y` | 使能 `wwdt`。 |
| `CONFIG_INT_WWDT_PERIOD_MS` | `2000` | `wwdt` 默认周期，单位 ms。 |
| `CONFIG_WWDT_TEST` | `y` | 在 `CONFIG_CLI` 和 `DRIVER_TEST` 使能时编译 `wwdt_test.c`。 |

<a id="id5"></a>

## 测试与示例

CP 侧 CLI 测试命令需使能 CONFIG\_CLI 与 DRIVER\_TEST，并按模块打开 CONFIG\_WDT\_TEST、CONFIG\_TASK\_WDT\_TEST、CONFIG\_WWDT\_TEST 中对应的测试宏。

完整命令列表、参数说明和串口演示见 [Watchdog](../../examples/peripheral/bk_wdt.md)。AON\_WDT、`task_wdt`、`wwdt` 的 API 参考见 [Watchdog](../../api-reference/peripheral/bk_wdt.md)。
