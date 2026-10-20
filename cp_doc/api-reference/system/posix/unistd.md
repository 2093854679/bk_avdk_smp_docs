---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/system/posix/unistd.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="unistd"></a>

# unistd接口介绍

> - 需要包含头文件#include \<posix/unistd.h\>;
> - 定义了系统sleep相关的接口

<a id="header-file"></a>

## Header File

- [unistd.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/posix/unistd.h)

<a id="functions"></a>

## Functions

<a id="_CPPv45sleepj"></a>

<a id="_CPPv35sleepj"></a> <a id="_CPPv25sleepj"></a> <a id="sleep__unsigned"></a> <a id="unistd_8h_1ad4669b3813c3b4a616a738317fdc974f"></a> unsigned sleep(unsigned seconds)
:   Suspend execution for an interval of time.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sleep.html>

    备注

    Return value of a positive number is not yet supported.

    参数
    :   **seconds** – **\[in\]** The number of seconds to suspend execution.

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv46usleep10useconds_t"></a>

<a id="_CPPv36usleep10useconds_t"></a> <a id="_CPPv26usleep10useconds_t"></a> <a id="usleep__useconds_t"></a> <a id="unistd_8h_1ac0383719bafa9b5b2aa25fabc586bd1f"></a> int usleep(useconds\_t usec)
:   Suspend execution for microsecond intervals.

    This is a useful, non-POSIX function.

    参数
    :   **usec** – **\[in\]** The number of microseconds to suspend execution.

    Return values
    :   **0** – \- Upon successful completion.
