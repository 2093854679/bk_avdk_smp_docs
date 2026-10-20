---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/system/posix/sched.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="sched"></a>

# sched接口介绍

> - 需要包含头文件#include \<posix/sched.h\>;
> - 定义了系统调度相关的接口

<a id="header-file"></a>

## Header File

- [sched.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/posix/sched.h)

<a id="functions"></a>

## Functions

<a id="_CPPv422sched_get_priority_maxi"></a>

<a id="_CPPv322sched_get_priority_maxi"></a> <a id="_CPPv222sched_get_priority_maxi"></a> <a id="sched_get_priority_max__i"></a> <a id="sched_8h_1afaebd1698caeb9b9b9e614ad84edd609"></a> int sched\_get\_priority\_max(int policy)
:   Get priority limit (max).

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_get_priority_max.html>

    备注

    policy is ignored.

    返回
    :   the maximum priority value (0-based) system configuration allows.

        e.g. if configMAX\_PRIORITIES \=\= 7, this function returns (configMAX\_PRIORITIES \- 1). configMAX\_PRIORITIES is configured in application FreeRTOSConfig.h file.

<a id="_CPPv422sched_get_priority_mini"></a>

<a id="_CPPv322sched_get_priority_mini"></a> <a id="_CPPv222sched_get_priority_mini"></a> <a id="sched_get_priority_min__i"></a> <a id="sched_8h_1af1f370fc36ea6b22ed42b5ee3cf82a81"></a> int sched\_get\_priority\_min(int policy)
:   Get priority limit (min).

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_get_priority_min.html>

    备注

    policy is ignored.

<a id="_CPPv411sched_yieldv"></a>

<a id="_CPPv311sched_yieldv"></a> <a id="_CPPv211sched_yieldv"></a> <a id="sched_yield__void"></a> <a id="sched_8h_1a357cd4b34c13011749dfffb42b489f09"></a> int sched\_yield(void)
:   Yield the processor.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_yield.html>

    Return values
    :   **0** – \- Upon successful completion

<a id="structures"></a>

## Structures

<a id="_CPPv411sched_param"></a>

<a id="_CPPv311sched_param"></a> <a id="_CPPv211sched_param"></a> <a id="sched_param"></a> <a id="structsched__param"></a> struct sched\_param
:   Scheduling parameters required for implementation of each supported scheduling policy.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N11sched_param14sched_priorityE"></a>

    <a id="_CPPv3N11sched_param14sched_priorityE"></a> <a id="_CPPv2N11sched_param14sched_priorityE"></a> <a id="sched_param::sched_priority__i"></a> <a id="structsched__param_1aa0f2640949273f2c30549ed8d1bb197e"></a> int sched\_priority
    :   Process or thread execution scheduling priority.

<a id="macros"></a>

## Macros

<a id="c.SCHED_OTHER"></a>

<a id="sched_8h_1a44c9baaf6f3c286f76783265b4938881"></a> SCHED\_OTHER
:   Another scheduling policy.
