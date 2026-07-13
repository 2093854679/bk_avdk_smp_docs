# RTC 使用指南



## 概述

实时时钟（Real-Time Clock, RTC）是嵌入式系统中记录时间的硬件模块。BK7259 AP 侧使用 AON RTC 的 64 bit 计数接口读取单调时间，并提供 `gettimeofday` / `settimeofday` 形式的时间戳接口。

备注

BK7259 只有一个 AON RTC 硬件实例，ID 为 ``` 0``（``AON_RTC_ID_1 ```）。CP 侧负责完整的闹钟管理；AP 侧保留读当前 tick、读/设置 time of day、读 us/ms 单调时间等接口，不提供闹钟注册测试命令。


## RTC 使用方法

AP 侧 RTC 常见使用方式：

> - 统计代码执行时间：调用 `bk_aon_rtc_get_current_tick()`、`bk_aon_rtc_get_us()` 或 `bk_aon_rtc_get_ms()` 记录开始和结束时间，再计算耗时。
> - 维护系统时间：调用 `bk_rtc_settimeofday()` 设置时间基准，后续可通过 `bk_rtc_gettimeofday()` 读取当前时间。


## 相关代码路径

> - API 头文件：`ap/include/driver/aon_rtc.h`
> - 类型定义：`ap/include/driver/aon_rtc_types.h`
> - 驱动源码：`ap/middleware/driver/rtc/aon_rtc_driver_64bit.c`
> - RTC 测试代码：`ap/middleware/driver/rtc/aon_rtc_test.c`
> - Kconfig：`ap/middleware/driver/rtc/Kconfig`
> - 默认配置：`ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig`


## 配置宏

| 宏 | BK7259 AP 默认值 | 说明 |
| --- | --- | --- |
| `CONFIG_AON_RTC` | `y` | 使能 AON RTC 驱动。 |
| `CONFIG_AON_RTC_64BIT` | `y` | 使用 64 bit RTC 驱动实现。 |
| `CONFIG_AON_RTC_MANY_USERS` | `y` | 使用多用户 RTC 框架；AP 侧不开放单独 create/destroy timer 的测试命令。 |
| `CONFIG_AON_RTC_TEST` | `y` | 使能 RTC 测试代码；实际编译还要求 `CONFIG_CLI=y` 用于提供系统命令入口。 |
| `CONFIG_AON_RTC_DEBUG` | `n` | AP 默认不编译调试 timing test。 |
| `CONFIG_RTC_TIMER_PRECISION_TEST` | `n` | RTC 精度测试宏，默认关闭。 |


## AP 侧测试

AP 侧 RTC 测试命令由 `ap/middleware/driver/rtc/aon_rtc_test.c` 导出。SMP 串口在 CP shell 下访问 AP 命令时，需要在命令前添加 `ap_cmd` 前缀，例如 `ap_cmd aon_rtc_get_time 0`。

备注

当前 RTC 测试代码归属于 RTC driver 目录下的 `aon_rtc_test.c`，不是旧的 `cli_*.c` 测试源文件。文档中出现 `CONFIG_CLI` 仅表示这些 RTC 测试命令通过系统命令框架暴露给 shell。

| 命令 | 说明 |
| --- | --- |
| `aon_rtc_get_time {id}` | 读取指定 RTC ID 的当前 tick，并按 `bk_rtc_get_ms_tick_count()` 换算为 ms。 |
| `aon_rtc_time_of_day get` | 读取 `bk_rtc_gettimeofday()` 的当前时间。 |
| `aon_rtc_time_of_day set {sec} {usec}` | 调用 `bk_rtc_settimeofday()` 设置 time of day 基准。 |

RTC 相关测试和使用介绍：[RTC 测试用例](../../examples/peripheral/bk_rtc.md "../../examples/peripheral/bk_rtc.md")


## RTC API Reference

> [RTC 驱动 API](../../api-reference/peripheral/bk_rtc.md "../../api-reference/peripheral/bk_rtc.md")
