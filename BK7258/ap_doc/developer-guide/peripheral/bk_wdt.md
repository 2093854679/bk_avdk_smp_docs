---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_wdt.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wdt"></a>

# WDT 使用指南

<a id="id1"></a>

## 概述

- watchdog 实际上是一个定时器，其通常用来监测和处理系统或软件故障。当系统或软件发生某些错误事件时，如不能定时清除看门狗定时器的计数值，将造成看门狗超时，从而触发系统复位。
- watchdog主要分为硬件狗（Interrupt Watchdog）和软件狗（Task Watchdog）。
- WDT相关测试和配置介绍: [wdt\_test\_config\_driver](../../examples/peripheral/bk_wdt.md)

备注

- 1、由于看门狗硬件资源只有一份，所以将其放在了cp上进行管理,若想配置看门狗，需要到CP侧进行 `cp/middleware/soc/bk7258/bk7258.defconfig` 配置；
- 2、喂狗的操作在CP上进行，如果超过配置的时间没有喂狗，会触发系统重启；
- 3、AP侧没有看门狗，通过核间心跳机制来检测ap是否正常运行；
- 4、AP侧上层应用主动调用bk\_reboot接口也可进行复位；

<a id="interrupt-watchdog"></a>

## **Interrupt Watchdog**

- 在 ARMINO 中，默认情况下，Interrupt Watchdog 是使能的，应用不应该关闭 interrupt watchdog。
- 在周期性中断中喂狗，如在 OS tick 中断中喂狗，当因为软件问题，如关中断过长，tick 中断未能及时喂狗，导致 watchdog 超时，最终触发 watchdog 重启。通过这种方式，能及时发现软件中断异常问题。这类 watchdog 使用通常称为 interrupt watchdog。

<a id="id2"></a>

## **Interrupt watchdog 使用方法**

> - 1、在 `cp/middleware/soc/bk7258/bk7258.defconfig` 中，通过CONFIG\_INT\_WDT 来关闭或开启interrupt watchdog；
> - 2、在 `cp/middleware/soc/bk7258/bk7258.defconfig` 中，通过 CONFIG\_INT\_WDT\_PERIOD\_MS 来设置超时时间；
> - 3、中断喂狗操作是：bk\_wdt\_feed()；
>
> 备注
>
> - 1、若是建了新的工程，也可在该工程中进行配置，比如test/platform工程， 在 `test/platform/cp/config/bk7258/config`

<a id="task-watchdog"></a>

## **Task Watchdog**

在周期性任务中喂狗，如在 idle task 中喂狗，通常 idle task 为整个系统中优先级最低的 task, 当软件出现问题，如某个任务出现死循环长期占用 CPU，使 idle task 无法调度，导致未能及时喂狗，最终触发 watchdog 重启。通过这种方式，能及时发现软件任务调度上的问题。这类 watchdog 使用通常称为 task watchdog。

<a id="id3"></a>

## **Task watchdog 使用方法**

> - 1、在 `cp/middleware/soc/bk7258/bk7258.defconfig` 中，通过 CONFIG\_TASK\_WDT 来关闭或开启interrupt watchdog；
> - 2、在 `cp/middleware/soc/bk7258/bk7258.defconfig` 中，通过 CONFIG\_TASK\_WDT\_PERIOD\_MS 来设置超时时间；
> - 3、中断喂狗操作是：bk\_task\_task\_wdt\_feed()；
>
> 备注
>
> - 1、若是建了新的工程，也可在该工程中进行配置，比如test/platform工程， 在 `test/platform/cp/config/bk7258/config`

<a id="wdt-api"></a>

## **WDT api介绍**

- WDT相关的api介绍参考: [WDT的api介绍](../../api-reference/peripheral/bk_wdt.md)
