---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_wdt.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="watchdog"></a>

# Watchdog

<a id="id1"></a>

## 1 功能概述

BK7259 CP 侧 watchdog 测试覆盖 AON\_WDT 兼容命令 `wdt`、`task_wdt` 和 `wwdt`。`wdt` 命令在 BK7259 上使用 AON\_WDT 作为后端；AON\_WDT 专用驱动当前没有单独 CLI 测试命令。

- watchdog 功能说明参考：[Watchdog 使用指南](../../developer-guide/peripheral/bk_wdt.md)

<a id="id2"></a>

## 2 代码路径

> - AON\_WDT 兼容测试代码：
>   :   `cp/middleware/driver/wdt/wdt_test.c`
> - AON\_WDT 兼容封装驱动源码：
>   :   `cp/middleware/driver/wdt/wdt_driver.c`
> - AON\_WDT 专用驱动源码：
>   :   `cp/middleware/driver/aon_wdt/aon_wdt_driver.c`
> - `wwdt` 测试代码：
>   :   `cp/middleware/driver/wwdt/wwdt_test.c`
> - `wwdt` 驱动源码：
>   :   `cp/middleware/driver/wwdt/wwdt_driver.c`

<a id="id3"></a>

## 3 宏配置

| NAME | Description | File | value |
| --- | --- | --- | --- |
| `CONFIG_WDT_EN` | 使能 AON\_WDT 兼容封装驱动 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_INT_WDT` | 使能 AON\_WDT 兼容 interrupt watchdog | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_SUPPORT_AON_WDT` | AON\_WDT 兼容封装使用 AON\_WDT 后端 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_INT_WDT_PERIOD_MS` | AON\_WDT 兼容封装默认周期，单位 ms | `cp/middleware/soc/bk7259/bk7259.defconfig` | `8000` |
| `CONFIG_AON_WDT` | 使能 AON\_WDT 专用驱动 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_INT_AON_WDT_PERIOD_MS` | AON\_WDT 默认周期，单位 ms | `cp/middleware/soc/bk7259/bk7259.defconfig` | `8000` |
| `CONFIG_SUPPORT_WWDT` | 使能 `wwdt` 驱动 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_WWDT_TEST` | 编译 `wwdt_test.c` 中的测试命令 | `cp/middleware/driver/wwdt/Kconfig` | `y` |

<a id="id4"></a>

## 4 测试命令

| Command | Param | Description |
| --- | --- | --- |
| `wdt start {timeout_ms}` | `timeout_ms`：超时时间，单位 ms | 启动 AON\_WDT 兼容命令，BK7259 上对应 AON\_WDT 后端。 |
| `wdt stop` | none | 停止 AON\_WDT 兼容命令。 |
| `wdt feed` | none | 启动 WDT 并用 Timer 周期性喂狗。 |
| `wdt suspend` | none | 低功耗前挂起 AON\_WDT。 |
| `wdt resume` | none | 低功耗退出后恢复 AON\_WDT。 |
| `wdt no_feed [timeout_ms]` | `timeout_ms`：可选超时时间 | 启动 WDT 后停止周期喂狗，用于验证 watchdog reset。 |
| `wwdt start {timeout_ms} [enable_window] [window_val]` | `timeout_ms`：超时时间；`enable_window`：是否开启窗口 | 启动 `wwdt`。 |
| `wwdt status` | none | 打印 `wwdt` 状态。 |
| `wwdt feed_once` | none | 执行一次 `wwdt` 喂狗。 |
| `wwdt feed_timer` | none | 启动定时器周期性喂 `wwdt`。 |
| `wwdt feed_in_win` | none | 测试窗口内喂狗。 |
| `wwdt feed_out_win` | none | 测试窗口外喂狗。 |

<a id="id5"></a>

## 5 命令行演示

1. 启动 CP AON\_WDT 兼容命令。

   > **wdt start 8000**
   > :   ```
   >     [17:20:01.000]发->◇wdt start 8000
   >     [17:20:01.006]收<-◆wdt start 8000
   >     $cli:I(1000):wdt start, timeout=8000
   >     $cli:I(1000):AON_WDT_REG_BASE=0x00000000
   >     ```
2. 启动 Timer 周期性喂 AON\_WDT 兼容命令。

   > **wdt feed**
   > :   ```
   >     [17:20:05.000]发->◇wdt feed
   >     [17:20:05.006]收<-◆wdt feed
   >     $cli:I(5000):wdt feed
   >     ```
3. 停止 CP AON\_WDT 兼容命令。

   > **wdt stop**
   > :   ```
   >     [17:20:10.000]发->◇wdt stop
   >     [17:20:10.006]收<-◆wdt stop
   >     $cli:I(10000):wdt stop
   >     ```
4. 启动 CP `wwdt`。

   > **wwdt start 6000**
   > :   ```
   >     [17:20:20.000]发->◇wwdt start 6000
   >     [17:20:20.006]收<-◆wwdt start 6000
   >     $cli:I(20000):wwdt start, timeout=6000, is_enable_window:0
   >     ```
5. 查看 CP `wwdt` 状态。

   > **wwdt status**
   > :   ```
   >     [17:20:22.000]发->◇wwdt status
   >     [17:20:22.006]收<-◆wwdt status
   >     $cli:I(22000):wwdt status: core=0, wwdt_cpu=0, driver_inited=1, feed_time=125, skip_bits=0x0
   >     ```
6. 停止 CP `wwdt`。

   > **wwdt stop**
   > :   ```
   >     [17:20:30.000]发->◇wwdt stop
   >     [17:20:30.006]收<-◆wwdt stop
   >     $cli:I(30000):wwdt stop
   >     ```
