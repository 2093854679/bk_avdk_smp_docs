---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_wdt.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wdt"></a>

# WDT

<a id="id1"></a>

## 1 功能概述

看门狗定时器通常用来监测和处理系统或软件故障。当系统或软件发生某些错误事件时，如不能定时清除看门狗定时器的计数值，将造成看门狗超时，从而触发系统复位。

- WDT相关的理论介绍参考: [WDT的驱动](../../developer-guide/peripheral/bk_wdt.md)

备注

- 1、由于看门狗硬件资源只有一份，所以将其放在了cp上进行管理,若想配置看门狗，需要到CP侧进行 `cp/middleware/soc/bk7258/bk7258.defconfig` 配置；
- 2、喂狗的操作在CP上进行，如果超过配置的时间没有喂狗，会触发系统重启；
- 3、AP侧没有看门狗，通过核间心跳机制来检测ap是否正常运行；
- 4、AP侧上层应用主动调用bk\_reboot接口也可进行复位；

<a id="id3"></a>

## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_wdt.c`
> - 驱动源码路径：
>   :   `ap\middleware\driver\wdt\wdt_driver.c`
> - WDT相关的api介绍参考: [WDT的api介绍](../../api-reference/peripheral/bk_wdt.md)

<a id="cli"></a>

## 3 cli命令简介

demo运行依赖的宏配置：

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG\_INT\_WDT | support hardware wdt | `ap\middleware\soc\bk7258\bk7258.defconfig` | y |
> | CONFIG\_INT\_WDT\_PERIOD\_MS | Interrupt Watchdog Period(ms) | `ap\middleware\soc\bk7258\bk7258.defconfig` | 8000 |
> | CONFIG\_TASK\_WDT\_PERIOD\_MS | support software wdt | `ap\middleware\soc\bk7258\bk7258.defconfig` | y |
> | CONFIG\_TASK\_WDT\_PERIOD\_MS | Task Watchdog Period(ms) | `ap\middleware\soc\bk7258\bk7258.defconfig` | 16000 |
> | CONFIG\_NMI\_WDT\_EN | support NMI wdt | `ap\middleware\soc\bk7258\bk7258.defconfig` | y |

demo支持的命令如下表：

> | Command | Param | Description |
> | --- | --- | --- |
> | wdt\_driver init | none | init wdt driver control memory |
> | wdt\_driver deinit | none | free all resource related to wdt |
> | wdt {start\|stop\|feed\|enable\|disable\|while} | start:start wdt | start wdt and feed wdt |
> | stop:stop wdt |
> | feed: feed wdt |
> | enable: enable wdt |
> | disable: disable wdt |
> | while: wdt while |

<a id="id4"></a>

## 4 演示介绍

> > demo1执行的步骤如下：
>
> 1、顺序发送以下命令
>
> > **wdt start 1000**
> > :   ```
> >     [15:51:06.104]发→◇wdt start 1000
> >     [15:51:06.108]收←◆wdt start 1000
> >     os:I(127743):create shell_handle, tcb=28086ff0, stack=[280853c8-28086fc8:7168], prio=5
> >     $cli:I(127744):wdt start, timeout=1000
> >     ```
> >
> > **wdt feed**
> > :   ```
> >     [15:51:07.778]发→◇wdt feed
> >     [15:51:07.783]收←◆wdt feed
> >     os:I(129418):create shell_handle, tcb=28086ff0, stack=[280853c8-28086fc8:7168], prio=5
> >     $cli:I(129419):wdt feed
> >     ```
> >
> > **wdt stop**
> > :   ```
> >     [15:51:27.077]发→◇wdt stop
> >     [15:51:27.081]收←◆wdt stop
> >     os:I(148715):create shell_handle, tcb=28086ff0, stack=[280853c8-28086fc8:7168], prio=5
> >     $cli:I(148716):wdt stop
> >     ```
> >
> > **wdt enable**
> > :   ```
> >     [15:51:56.072]发→◇wdt enable
> >     [15:51:56.076]收←◆wdt enable
> >     os:I(177710):create shell_handle, tcb=28086ff0, stack=[280853c8-28086fc8:7168], prio=5
> >     $cli:I(177711):wdt debug enabled
> >     ```
> >
> > **wdt disable**
> > :   ```
> >     [15:51:57.418]发→◇ wdt disable
> >     [15:51:57.423]收←◆ wdt disable
> >     os:I(179056):create shell_handle, tcb=28086ff0, stack=[280853c8-28086fc8:7168], prio=5
> >     $cli:I(179057):wdt debug disabled`
> >     ```
