---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/system/posix/signal.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="signal"></a>

# signal接口介绍

> - 需要包含头文件#include \<posix/signal.h\>;
> - 定义了系统信号相关的接口

<a id="header-file"></a>

## Header File

- [signal.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/posix/signal.h)

<a id="unions"></a>

## Unions

<a id="_CPPv46sigval"></a>

<a id="_CPPv36sigval"></a> <a id="_CPPv26sigval"></a> <a id="unionsigval"></a> union sigval
:   *#include \<signal.h\>*

    Signal value.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N6sigval9sival_intE"></a>

    <a id="_CPPv3N6sigval9sival_intE"></a> <a id="_CPPv2N6sigval9sival_intE"></a> <a id="sigval::sival_int__i"></a> <a id="unionsigval_1a560393252ee7edc37df44bf1c11bdbdd"></a> int sival\_int
    :   Integer signal value.

    <a id="_CPPv4N6sigval9sival_ptrE"></a>

    <a id="_CPPv3N6sigval9sival_ptrE"></a> <a id="_CPPv2N6sigval9sival_ptrE"></a> <a id="sigval::sival_ptr__voidP"></a> <a id="unionsigval_1a4668f1bd7463de7b70bd0022207e26ac"></a> void \*sival\_ptr
    :   Pointer signal value.

<a id="structures"></a>

## Structures

<a id="_CPPv48sigevent"></a>

<a id="_CPPv38sigevent"></a> <a id="_CPPv28sigevent"></a> <a id="sigevent"></a> <a id="structsigevent"></a> struct sigevent
:   Signal event structure.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N8sigevent12sigev_notifyE"></a>

    <a id="_CPPv3N8sigevent12sigev_notifyE"></a> <a id="_CPPv2N8sigevent12sigev_notifyE"></a> <a id="sigevent::sigev_notify__i"></a> <a id="structsigevent_1aae9a19d879c38e0c4e8a9bf738c5081e"></a> int sigev\_notify
    :   Notification type. A value of SIGEV\_SIGNAL is not supported.

    <a id="_CPPv4N8sigevent11sigev_signoE"></a>

    <a id="_CPPv3N8sigevent11sigev_signoE"></a> <a id="_CPPv2N8sigevent11sigev_signoE"></a> <a id="sigevent::sigev_signo__i"></a> <a id="structsigevent_1a5c645ec1d12bb46efc3f4097c52b665d"></a> int sigev\_signo
    :   Signal number. This member is ignored.

    <a id="_CPPv4N8sigevent11sigev_valueE"></a>

    <a id="_CPPv3N8sigevent11sigev_valueE"></a> <a id="_CPPv2N8sigevent11sigev_valueE"></a> <a id="sigevent::sigev_value__sigval"></a> <a id="structsigevent_1a757af1e34b87e3f66bbc08c514017a2c"></a> union [sigval](#_CPPv46sigval "sigval") sigev\_value
    :   Signal value. Only the sival\_ptr member is used.

    <a id="_CPPv4N8sigevent21sigev_notify_functionE"></a>

    <a id="_CPPv3N8sigevent21sigev_notify_functionE"></a> <a id="_CPPv2N8sigevent21sigev_notify_functionE"></a> <a id="structsigevent_1ae47aee413b2a2fb09fd7601cb132d03b"></a> void (\*sigev\_notify\_function)(union [sigval](#_CPPv46sigval "sigval"))
    :   Notification function.

    <a id="_CPPv4N8sigevent23sigev_notify_attributesE"></a>

    <a id="_CPPv3N8sigevent23sigev_notify_attributesE"></a> <a id="_CPPv2N8sigevent23sigev_notify_attributesE"></a> <a id="sigevent::sigev_notify_attributes__pthread_attr_tP"></a> <a id="structsigevent_1a5a687d2092b237d76eb08e2d46a5115f"></a> pthread\_attr\_t \*sigev\_notify\_attributes
    :   Notification attributes.

<a id="macros"></a>

## Macros

<a id="c.SIGEV_NONE"></a>

<a id="signal_8h_1aced9a66610d9d61756999ce4f103740e"></a> SIGEV\_NONE
:   No asynchronous notification is delivered when the event of interest occurs.

<a id="c.SIGEV_SIGNAL"></a>

<a id="signal_8h_1a06d5881eeb84e6ac35f5b801c380dbb6"></a> SIGEV\_SIGNAL
:   A queued signal, with an application-defined value, is generated when the event of interest occurs. Not supported.

<a id="c.SIGEV_THREAD"></a>

<a id="signal_8h_1a29ccb6a17fa90a1357b478f62af7fca0"></a> SIGEV\_THREAD
:   A notification function is called to perform notification.
