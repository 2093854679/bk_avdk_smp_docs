---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_rtc.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# RTC

<a id="id1"></a>

## 1 功能概述

实时时钟（Real -Time Clock,RTC）是嵌入式系统中记录时间的硬件模块，在AP侧该模块仅提供读取RTC时间以及操作NTP网络时间的接口，bk7258只有一个RTC硬件模块（id 为 0）。

- RTC功能具体描述参考: [RTC驱动工作原理](../../developer-guide/peripheral/bk_rtc.md)

<a id="id3"></a>

## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_aon_rtc.c`
> - 驱动源码路径：
>   :   `ap\middleware\driver\rtc\aon_rtc_driver_64bit.c`

<a id="cli"></a>

## 3 cli命令简介

demo运行依赖的宏配置：

> | NAME | Description | File | | value |
> | --- | --- | --- | --- | --- |
> | CONFIG\_AON\_RTC | support rtc | `ap\middleware\soc\bk7258\bk7258_ap.defconfig` \| y | | |

demo支持的命令如下表：

> | Command | Param | Description |
> | --- | --- | --- |
> | aon\_rtc\_get\_time {id} | rtc id | get rtc time |
> | aon\_rtc\_time\_of\_day set {sec\|usec} | sec: set sec | Set time of day |
> | usec: set usec |
> | aon\_rtc\_time\_of\_day get | none | Get time of day |

<a id="id4"></a>

## 4 演示介绍

> demo1执行的步骤如下：
>
> **cpu1 aon\_rtc\_get\_time 0**
> :   ```
>     [16:48:06.968]发→◇cpu1 aon_rtc_get_time 0
>     [16:48:06.974]收←◆cpu1 aon_rtc_get_time 0
>     os:I(337790):create shell_handle, tcb=28086ff0, stack=[280853c8-28086fc8:7168], prio=5
>
>     $
>     $cpu1:cli:I(337655):id=0, tick_h=0 tick_l=337792 ms
>     ```
