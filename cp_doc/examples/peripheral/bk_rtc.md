---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_rtc.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# RTC

<a id="id1"></a>

## 1 功能概述

实时时钟（Real-Time Clock, RTC）是嵌入式系统中记录时间的硬件模块。BK7259 CP 侧提供 AON RTC 驱动初始化、读取当前 tick、注册/注销闹钟、自动闹钟测试、RTC clock source/ROSC 调试以及 dump/timing test 等 RTC 测试命令；BK7259 只有一个 AON RTC 硬件实例，ID 为 `0`。

- RTC 功能具体描述参考：[RTC 驱动工作原理](../../developer-guide/peripheral/bk_rtc.md)

<a id="id2"></a>

## 2 代码路径

> - RTC 测试代码：
>   :   `cp/middleware/driver/rtc/aon_rtc_test.c`
> - 驱动源码：
>   :   `cp/middleware/driver/rtc/aon_rtc_driver_64bit.c`
> - API 头文件：
>   :   `cp/include/driver/aon_rtc.h`
> - Kconfig：
>   :   `cp/middleware/driver/rtc/Kconfig`
> - 默认配置：
>   :   `cp/middleware/soc/bk7259/bk7259.defconfig`

<a id="id3"></a>

## 3 测试命令简介

demo 运行依赖的宏配置：

| NAME | Description | File | value |
| --- | --- | --- | --- |
| `CONFIG_AON_RTC` | 使能 AON RTC 驱动 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_AON_RTC_MANY_USERS` | 使用多用户闹钟链表管理 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_AON_RTC_TEST` | 编译 `aon_rtc_test.c` 中的 RTC 测试命令 | `cp/middleware/driver/rtc/Kconfig` | `y` |
| `CONFIG_AON_RTC_DEBUG` | 编译 `aon_rtc_timing_test` 和调试统计 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `y` |
| `CONFIG_RTC_TIMER_PRECISION_TEST` | 打开后闹钟回调输出 drift 统计 | `cp/middleware/soc/bk7259/bk7259.defconfig` | `n` |
| `CONFIG_CLI` | 系统命令框架；`CONFIG_AON_RTC_TEST` 的测试命令入口依赖该宏 | 项目配置 / 默认配置 | `y` |

demo 支持的命令如下表：

备注

当前 RTC 测试代码位于 `cp/middleware/driver/rtc/aon_rtc_test.c`，不是旧的 `cli_*.c` 测试源文件。`CONFIG_CLI` 只表示测试命令通过系统命令框架暴露给 shell。

| Command | Param | Description |
| --- | --- | --- |
| `aon_rtc_driver init` | 无 | 初始化 AON RTC 驱动控制结构和中断。 |
| `aon_rtc_driver deinit` | 无 | 释放 AON RTC 驱动资源。 |
| `aon_rtc_get_time {id}` | `id`：RTC ID，BK7259 为 `0` | 读取当前 RTC tick，并换算为 ms 输出。 |
| `aon_rtc_register {id} {name} {period_tick} {period_cnt}` | `name`：闹钟名；`period_tick`：RTC tick；`period_cnt`：触发次数 | 注册闹钟。测试代码固定使用 `alarm_callback`，命令行不需要也不支持传 callback 参数。 |
| `aon_rtc_unregister {id} {name}` | `name`：闹钟名 | 注销指定闹钟。 |
| `aon_rtc_auto_test {id} {start|stop}` | `start` / `stop` | 自动注册/注销 6 个预置闹钟，用于链表和重复注册测试。 |
| `aon_rtc_clock_src {26m|rosc}` | `26m` 或 `rosc` | 切换 LPO/RTC clock source。 |
| `aon_rtc_rosc_cal {auto|manual|disable} {interval}` | 校准模式和校准间隔 | 配置 ROSC 校准模式。代码中 help 字符串较旧，实际命令需要两个参数。 |
| `aon_rtc_rosc_test {enable|disable}` | `enable` 或 `disable` | 开关 ROSC test mode。代码中 help 字符串较旧，实际命令需要一个参数。 |
| `aon_rtc_dump {id}` | `id`：RTC ID | dump RTC 驱动和闹钟链表调试信息。 |
| `aon_rtc_timing_test {id} {rounds} {cycles} {set_tick}` | 仅 `CONFIG_AON_RTC_DEBUG=y` 时存在 | 测试 RTC get/set tick 的耗时。 |

备注

旧的 `aon_rtc {id} create/destroy` 和 `aon_rtc_int` 命令在代码中被 `#if 0` 关闭，BK7259 默认 `CONFIG_AON_RTC_MANY_USERS=y`，请使用 `aon_rtc_register` / `aon_rtc_unregister`。

<a id="id4"></a>

## 4 演示介绍

demo 执行步骤如下：

> **aon\_rtc\_driver init**
> :   ```
>     $aon_rtc_driver init
>     $cli:I(xxxx):aon_rtc driver init
>     ```
>
> **aon\_rtc\_get\_time 0**
> :   ```
>     [16:37:26.111]发->◇aon_rtc_get_time 0
>     [16:37:26.116]收<-◆aon_rtc_get_time 0
>     os:I(10745):create shell_handle, tcb=28086f60, stack=[28085338-28086f38:7168], prio=5
>
>     $cli:I(10746):id=0, tick_h=0 tick_l=10747 ms
>     ```
>
> **aon\_rtc\_register 0 alarm1 64000 5**
>
> 注册名为 `alarm1` 的闹钟。默认 ROSC 频率为 32000 Hz 时，`64000` tick 约等于 2 秒，`period_cnt=5` 表示触发 5 次。
>
> > ```
> > [16:42:37.323]收<-◆cli:I(8140):id=0, name=alarm1 alarmprm
> > [16:42:39.323]收<-◆cli:I(10140):id=0, name=alarm1 alarmprm
> > [16:42:41.323]收<-◆cli:I(12140):id=0, name=alarm1 alarmprm
> > [16:42:43.323]收<-◆cli:I(14140):id=0, name=alarm1 alarmprm
> > [16:42:45.323]收<-◆cli:I(16141):id=0, name=alarm1 alarmprm
> > ```
>
> **aon\_rtc\_unregister 0 alarm1**
> :   ```
>     $aon_rtc_unregister 0 alarm1
>     ```
>
> **aon\_rtc\_auto\_test 0 start / aon\_rtc\_auto\_test 0 stop**
> :   ```
>     $aon_rtc_auto_test 0 start
>     $cli:I(xxxx):id=0, name=alarm_1
>     $cli:I(xxxx):register name=alarm_4
>     $aon_rtc_auto_test 0 stop
>     ```
>
> **aon\_rtc\_clock\_src rosc**
> :   ```
>     $aon_rtc_clock_src rosc
>     ```
>
> **aon\_rtc\_rosc\_cal auto 10**
> :   ```
>     $aon_rtc_rosc_cal auto 10
>     $cli:I(xxxx):ROSC calibration mode: 0, interval: 10
>     ```
>
> **aon\_rtc\_rosc\_test enable**
> :   ```
>     $aon_rtc_rosc_test enable
>     ```
>
> **aon\_rtc\_dump 0**
> :   ```
>     $aon_rtc_dump 0
>     ```
