---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_rtc.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# RTC

<a id="id1"></a>

## 1 功能概述

实时时钟（Real-Time Clock, RTC）是嵌入式系统中记录时间的硬件模块。BK7259 AP 侧提供读取 AON RTC tick、读取/设置 time of day 的 RTC 测试命令；BK7259 只有一个 AON RTC 硬件实例，ID 为 `0`。

- RTC 功能具体描述参考：[RTC 驱动工作原理](../../developer-guide/peripheral/bk_rtc.md)

<a id="id2"></a>

## 2 代码路径

> - RTC 测试代码：
>   :   `ap/middleware/driver/rtc/aon_rtc_test.c`
> - 驱动源码：
>   :   `ap/middleware/driver/rtc/aon_rtc_driver_64bit.c`
> - API 头文件：
>   :   `ap/include/driver/aon_rtc.h`
> - Kconfig：
>   :   `ap/middleware/driver/rtc/Kconfig`
> - 默认配置：
>   :   `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig`

<a id="id3"></a>

## 3 测试命令简介

demo 运行依赖的宏配置：

| NAME | Description | File | value |
| --- | --- | --- | --- |
| `CONFIG_AON_RTC` | 使能 AON RTC 驱动 | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `y` |
| `CONFIG_AON_RTC_64BIT` | 使用 64 bit RTC 驱动 | `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig` | `y` |
| `CONFIG_AON_RTC_TEST` | 编译 `aon_rtc_test.c` 中的 RTC 测试命令 | `ap/middleware/driver/rtc/Kconfig` | `y` |
| `CONFIG_CLI` | 系统命令框架；`CONFIG_AON_RTC_TEST` 的测试命令入口依赖该宏 | 项目配置 / 默认配置 | `y` |

demo 支持的命令如下表：

备注

当前 RTC 测试代码位于 `ap/middleware/driver/rtc/aon_rtc_test.c`，不是旧的 `cli_*.c` 测试源文件。`CONFIG_CLI` 只表示测试命令通过系统命令框架暴露给 shell。

| Command | Param | Description |
| --- | --- | --- |
| `aon_rtc_get_time {id}` | `id`：RTC ID，BK7259 为 `0` | 读取当前 RTC tick，并换算为 ms 输出。 |
| `aon_rtc_time_of_day get` | 无 | 读取当前 time of day。 |
| `aon_rtc_time_of_day set {sec} {usec}` | `sec`：秒；`usec`：微秒 | 设置 time of day 基准。 |

<a id="id4"></a>

## 4 演示介绍

AP 侧 RTC 测试命令在 CP shell 下执行时需要添加 `ap_cmd` 前缀，以下示例使用 `ap_cmd`：

> **ap\_cmd aon\_rtc\_get\_time 0**
> :   ```
>     [16:48:06.968]发->◇ap_cmd aon_rtc_get_time 0
>     [16:48:06.974]收<-◆ap_cmd aon_rtc_get_time 0
>     os:I(337790):create shell_handle, tcb=28086ff0, stack=[280853c8-28086fc8:7168], prio=5
>
>     $
>     $ap0:cli:I(337655):id=0, tick_h=0 tick_l=337792 ms
>     ```
>
> **ap\_cmd aon\_rtc\_time\_of\_day set 1710000000 0**
> :   ```
>     $ap0:cli:I(xxxx):aon_rtc_time_of_day set 1710000000 0
>     ```
>
> **ap\_cmd aon\_rtc\_time\_of\_day get**
> :   ```
>     $ap0:cli:I(xxxx):aon_rtc_time_of_day get
>     ```
