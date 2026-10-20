---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_rtc.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# RTC

<a id="id1"></a>

## 1 功能概述

实时时钟（Real -Time Clock,RTC）是嵌入式系统中记录时间的硬件模块，在CP侧该模块提供注册闹钟和读取RTC时间的功能，bk7258只有一个RTC硬件模块（id 为 0）。

<a id="id2"></a>

## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_aon_rtc.c`
> - 驱动源码路径：
>   :   `cp\middleware\driver\rtc\aon_rtc_driver_64bit.c`

<a id="cli"></a>

## 3 cli命令简介

demo运行依赖的宏配置：

> | NAME | Description | File | | value |
> | --- | --- | --- | --- | --- |
> | CONFIG\_AON\_RTC | support rtc | `cp\middleware\soc\bk7258\bk7258.defconfig` \| y | | |

demo支持的命令如下表：

> | Command | Param | Description |
> | --- | --- | --- |
> | aon\_rtc\_driver init | none | init rtc driver control memory |
> | aon\_rtc\_driver deinit | none | free all resource related to rtc |
> | aon\_rtc\_get\_time {id} | id: rtc id number | get rtc time |
> | aon\_rtc\_register {id} {name} {period\_tick} {period\_cnt}, {callback} | id: rtc id number | register Alarm |
> | name: Alarm name |
> | period\_tick: rtc tick count |
> | period\_cnt: Alarm Repeat Count |
> | callback: register Callback Function |
> | aon\_rtc\_unregister {id} {name} | id: rtc id number | unregister Alarm |
> | name: Alarm name |

<a id="id3"></a>

## 4 演示介绍

> demo1执行的步骤如下：
>
> **aon\_rtc\_get\_time 0**
>
> ```
> [16:37:26.111]发→◇aon_rtc_get_time 0
> [16:37:26.116]收←◆aon_rtc_get_time 0
> os:I(10745):create shell_handle, tcb=28086f60, stack=[28085338-28086f38:7168], prio=5
>
> $cli:I(10746):id=0, tick_h=0 tick_l=10747 ms
> ```
>
> **aon\_rtc\_register 0 alarm1 64000 5**//注册name为alarm1的闹钟，2s触发一次，执行五次（64000/32000（RTC时钟源））
>
> ```
> [16:42:37.323]收←◆cli:I(8140):id=0, name=alarm1 alarmprm
>
> [16:42:39.323]收←◆cli:I(10140):id=0, name=alarm1 alarmprm
>
> [16:42:41.323]收←◆cli:I(12140):id=0, name=alarm1 alarmprm
>
> [16:42:43.323]收←◆cli:I(14140):id=0, name=alarm1 alarmprm
>
> [16:42:45.323]收←◆cli:I(16141):id=0, name=alarm1 alarmprm
> ```
