---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_rtc.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# RTC 使用指南

<a id="id1"></a>

## 概述

实时时钟（Real-Time Clock, RTC）是嵌入式系统中记录时间的硬件模块。BK7259 CP 侧使用 AON RTC 64 bit 驱动，提供驱动初始化、当前 tick 读取、闹钟注册/注销、RTC clock source/ROSC 调试以及 dump/timing test 等 RTC 测试能力。

备注

BK7259 只有一个 AON RTC 硬件实例，ID 为 ``` 0``（``AON_RTC_ID_1 ```）。CP 侧是完整 RTC 闹钟管理侧；AP 侧主要提供读时间和 time of day 接口。

<a id="id2"></a>

## RTC 使用方法

CP 侧 RTC 常见使用方式：

> - 统计代码执行时间：调用 `bk_aon_rtc_get_current_tick()`、`bk_aon_rtc_get_us()` 或 `bk_aon_rtc_get_ms()` 获取单调时间。
> - 注册闹钟定期执行回调：通过 `bk_alarm_register()` 设置闹钟周期和触发次数，通过 `bk_alarm_unregister()` 注销闹钟。回调运行在中断上下文中，不能执行阻塞、sleep、malloc/free 等操作。
> - 调试 RTC 时钟源和精度：通过 RTC 测试命令切换 `26m` / `rosc`，配置 ROSC 校准，或在打开测试宏后运行 timing/precision 测试。

<a id="id3"></a>

## 相关代码路径

> - API 头文件：`cp/include/driver/aon_rtc.h`
> - 类型定义：`cp/include/driver/aon_rtc_types.h`
> - 驱动源码：`cp/middleware/driver/rtc/aon_rtc_driver_64bit.c`
> - RTC 测试代码：`cp/middleware/driver/rtc/aon_rtc_test.c`
> - Kconfig：`cp/middleware/driver/rtc/Kconfig`
> - 默认配置：`cp/middleware/soc/bk7259/bk7259.defconfig`

<a id="id4"></a>

## 配置宏

| 宏 | BK7259 CP 默认值 | 说明 |
| --- | --- | --- |
| `CONFIG_AON_RTC` | `y` | 使能 AON RTC 驱动，并自动选择 64 bit 驱动。 |
| `CONFIG_AON_RTC_MANY_USERS` | `y` | 使能多用户闹钟链表管理；禁用旧的单用户 create/destroy 测试命令。 |
| `CONFIG_AON_RTC_TEST` | `y` | 使能 `aon_rtc_test.c` 中的 RTC 测试命令；实际编译还要求 `CONFIG_CLI=y` 用于提供系统命令入口。 |
| `CONFIG_AON_RTC_DEBUG` | `y` | 使能 `aon_rtc_timing_test` 和驱动调试统计。 |
| `CONFIG_RTC_TIMER_PRECISION_TEST` | `n` | RTC timer 精度测试宏。打开后，闹钟回调输出 drift 统计，而不是普通 alarm log。 |
| `CONFIG_AON_RTC_KEEP_TIME_SUPPORT` | `n` | 深睡/重启保留 time of day 的支持，默认关闭。 |
| `CONFIG_AON_RTC_DYNAMIC_CLOCK_SUPPORT` | `n` | RTC 动态 clock 频率支持，默认关闭。 |

RTC 相关测试和使用介绍：[RTC 测试用例](../../examples/peripheral/bk_rtc.md)

备注

当前 RTC 测试代码归属于 RTC driver 目录下的 `aon_rtc_test.c`，不是旧的 `cli_*.c` 测试源文件。文档中出现 `CONFIG_CLI` 仅表示这些 RTC 测试命令通过系统命令框架暴露给 shell。
