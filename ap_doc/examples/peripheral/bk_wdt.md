---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_wdt.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="watchdog"></a>

# Watchdog

<a id="id1"></a>

## 1 功能概述

BK7259 AP 侧 watchdog 测试只覆盖 `task_wdt` 和 `wwdt`。AP 侧没有 `wdt` / `aon_wdt` 测试命令；AON\_WDT 由 CP 侧管理。

- watchdog 功能说明参考：[Watchdog 使用指南](../../developer-guide/peripheral/bk_wdt.md)

<a id="id2"></a>

## 2 代码路径

> - `task_wdt` 测试代码：
>   :   `ap/middleware/driver/wdt/task_wdt_test.c`
> - `task_wdt` 驱动源码：
>   :   `ap/middleware/driver/wdt/task_wdt.c`
> - `wwdt` 测试代码：
>   :   `ap/middleware/driver/wwdt/wwdt_test.c`
> - `wwdt` 驱动源码：
>   :   `ap/middleware/driver/wwdt/wwdt_driver.c`
> - `wwdt` API 头文件：
>   :   `ap/include/driver/wwdt.h`

<a id="id3"></a>

## 3 宏配置

| NAME | Description | File | value |
| --- | --- | --- | --- |
| `CONFIG_TASK_WDT` | 使能 `task_wdt` | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `y` |
| `CONFIG_TASK_WDT_PERIOD_MS` | `task_wdt` 超时时间，单位 ms | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `60000` |
| `CONFIG_TASK_WDT_TEST` | 编译 `task_wdt_test.c` 中的测试命令 | `ap/middleware/driver/wdt/Kconfig` | `y` |
| `CONFIG_SUPPORT_WWDT` | 使能 `wwdt` 驱动 | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `y` |
| `CONFIG_INT_WWDT_PERIOD_MS` | `wwdt` 默认周期，单位 ms | `ap/middleware/driver/wwdt/Kconfig` | `2000` |
| `CONFIG_WWDT_TEST` | 编译 `wwdt_test.c` 中的测试命令 | `ap/middleware/driver/wwdt/Kconfig` | `y` |
| `CONFIG_CLI` | 系统命令框架；测试命令入口依赖该宏 | 项目配置 / 默认配置 | `y` |

<a id="id4"></a>

## 4 测试命令

AP 侧测试命令在 CP shell 下执行时需要添加 `ap_cmd` 前缀。

| Command | Param | Description |
| --- | --- | --- |
| `task_wdt start` | none | 启动 `task_wdt`。 |
| `task_wdt status` | none | 打印 `task_wdt` 状态。 |
| `task_wdt feed_once` | none | 当前 core 执行一次喂狗。 |
| `task_wdt skip_feed_core {core}` | `core`：`0` 或 `1` | 设置指定 core 跳过喂狗。 |
| `task_wdt resume_feed_core {core}` | `core`：`0` 或 `1` | 恢复指定 core 喂狗。 |
| `task_wdt busy_core {core} {seconds}` | `core`：`0` 或 `1`；`seconds`：持续时间 | 在指定 core 上创建 busy 任务。 |
| `task_wdt hang_core {core}` | `core`：`0` 或 `1` | 在指定 core 上创建死循环任务。 |
| `wwdt start {timeout_ms} [enable_window] [window_val]` | `timeout_ms`：超时时间；`enable_window`：是否使能窗口 | 启动 `wwdt`。 |
| `wwdt status` | none | 打印 `wwdt` 状态。 |
| `wwdt feed_once` | none | 执行一次 `wwdt` 喂狗。 |
| `wwdt feed_timer` | none | 启动定时器周期性喂 `wwdt`。 |
| `wwdt feed_in_win` | none | 测试窗口内喂狗。 |
| `wwdt feed_out_win` | none | 测试窗口外喂狗。 |

<a id="id5"></a>

## 5 命令行演示

1. 查看 AP `task_wdt` 状态。

   > **ap\_cmd task\_wdt status**
   > :   ```
   >     [17:10:01.000]发->◇ap_cmd task_wdt status
   >     [17:10:01.006]收<-◆ap_cmd task_wdt status
   >     $ap0:cli:I(1000):task_wdt status: current_core=0, feed_bits=0x3, skip_bits=0x0
   >     $ap0:cli:I(1000):task_wdt core0 last_feed_tick=0:998
   >     $ap0:cli:I(1000):task_wdt core1 last_feed_tick=0:997
   >     ```
2. 当前 core 执行一次 `task_wdt` 喂狗。

   > **ap\_cmd task\_wdt feed\_once**
   > :   ```
   >     [17:10:05.000]发->◇ap_cmd task_wdt feed_once
   >     [17:10:05.006]收<-◆ap_cmd task_wdt feed_once
   >     $ap0:cli:I(5000):task_wdt feed_once, core=0
   >     ```
3. 启动 AP `wwdt`。

   > **ap\_cmd wwdt start 6000**
   > :   ```
   >     [17:10:10.000]发->◇ap_cmd wwdt start 6000
   >     [17:10:10.006]收<-◆ap_cmd wwdt start 6000
   >     $ap0:cli:I(10000):wwdt start, timeout=6000, is_enable_window:0
   >     ```
4. 查看 AP `wwdt` 状态。

   > **ap\_cmd wwdt status**
   > :   ```
   >     [17:10:12.000]发->◇ap_cmd wwdt status
   >     [17:10:12.006]收<-◆ap_cmd wwdt status
   >     $ap0:cli:I(12000):wwdt status: core=0, wwdt_cpu=2, driver_inited=1, feed_time=125, skip_bits=0x0
   >     ```
5. 停止 AP `wwdt`。

   > **ap\_cmd wwdt stop**
   > :   ```
   >     [17:10:20.000]发->◇ap_cmd wwdt stop
   >     [17:10:20.006]收<-◆ap_cmd wwdt stop
   >     $ap0:cli:I(20000):wwdt stop
   >     ```
