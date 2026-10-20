---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/system/posix/pthread.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="pthread"></a>

# pthread接口介绍

> - 需要包含头文件#include \<posix/pthread.h\>;
> - 定义了系统任务创建，销毁等相关的接口

<a id="header-file"></a>

## Header File

- [pthread.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/posix/pthread.h)

<a id="functions"></a>

## Functions

<a id="_CPPv420pthread_attr_destroyP14pthread_attr_t"></a>

<a id="_CPPv320pthread_attr_destroyP14pthread_attr_t"></a> <a id="_CPPv220pthread_attr_destroyP14pthread_attr_t"></a> <a id="pthread_attr_destroy__pthread_attr_tP"></a> <a id="pthread_8h_1a4bcdbf47c17c7dcc51e9f05f5cb56d81"></a> int pthread\_attr\_destroy(pthread\_attr\_t \*attr)
:   Destroy the thread attributes object.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_attr_destroy.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv427pthread_attr_getdetachstatePK14pthread_attr_tPi"></a>

<a id="_CPPv327pthread_attr_getdetachstatePK14pthread_attr_tPi"></a> <a id="_CPPv227pthread_attr_getdetachstatePK14pthread_attr_tPi"></a> <a id="pthread_attr_getdetachstate__pthread_attr_tCP.iP"></a> <a id="pthread_8h_1a391c34da42e68ddd24f5ee0c070d5c4f"></a> int pthread\_attr\_getdetachstate(const pthread\_attr\_t \*attr, int \*detachstate)
:   Get detachstate attribute.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_attr_getdetachstate.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv426pthread_attr_getschedparamPK14pthread_attr_tP11sched_param"></a>

<a id="_CPPv326pthread_attr_getschedparamPK14pthread_attr_tP11sched_param"></a> <a id="_CPPv226pthread_attr_getschedparamPK14pthread_attr_tP11sched_param"></a> <a id="pthread_attr_getschedparam__pthread_attr_tCP.sched_paramP"></a> <a id="pthread_8h_1afd3d272d702481044f8a8cd253fd9b47"></a> int pthread\_attr\_getschedparam(const pthread\_attr\_t \*attr, struct [sched\_param](sched.md#_CPPv411sched_param "sched_param") \*param)
:   Get schedparam attribute.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_attr_getschedparam.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv425pthread_attr_getstacksizePK14pthread_attr_tP6size_t"></a>

<a id="_CPPv325pthread_attr_getstacksizePK14pthread_attr_tP6size_t"></a> <a id="_CPPv225pthread_attr_getstacksizePK14pthread_attr_tP6size_t"></a> <a id="pthread_attr_getstacksize__pthread_attr_tCP.sP"></a> <a id="pthread_8h_1ae23600d4670359ab12bfba20db2c9a37"></a> int pthread\_attr\_getstacksize(const pthread\_attr\_t \*attr, size\_t \*stacksize)
:   Get stacksize attribute.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_attr_getstacksize.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv417pthread_attr_initP14pthread_attr_t"></a>

<a id="_CPPv317pthread_attr_initP14pthread_attr_t"></a> <a id="_CPPv217pthread_attr_initP14pthread_attr_t"></a> <a id="pthread_attr_init__pthread_attr_tP"></a> <a id="pthread_8h_1a0b85ebb1e3aac081a4c0a5e85ae3cbe9"></a> int pthread\_attr\_init(pthread\_attr\_t \*attr)
:   Initialize the thread attributes object.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_attr_init.html>

    备注

    Currently, only stack size, [sched\_param](sched.md#structsched__param), and detach state attributes are supported. Also see pthread\_attr\_get\*() and pthread\_attr\_set\*().

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv427pthread_attr_setdetachstateP14pthread_attr_ti"></a>

<a id="_CPPv327pthread_attr_setdetachstateP14pthread_attr_ti"></a> <a id="_CPPv227pthread_attr_setdetachstateP14pthread_attr_ti"></a> <a id="pthread_attr_setdetachstate__pthread_attr_tP.i"></a> <a id="pthread_8h_1ae6ee78c307d8467b34a9b0c330993a54"></a> int pthread\_attr\_setdetachstate(pthread\_attr\_t \*attr, int detachstate)
:   Set detachstate attribute.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_attr_setdetachstate.html>

    Return values
    :   - **0** – \- Upon successful completion
        - **EINVAL** – \- The value of detachstate is not valid. Currently, supported detach states are \&#8212; PTHREAD\_CREATE\_DETACHED and PTHREAD\_CREATE\_JOINABLE.

<a id="_CPPv426pthread_attr_setschedparamP14pthread_attr_tPK11sched_param"></a>

<a id="_CPPv326pthread_attr_setschedparamP14pthread_attr_tPK11sched_param"></a> <a id="_CPPv226pthread_attr_setschedparamP14pthread_attr_tPK11sched_param"></a> <a id="pthread_attr_setschedparam__pthread_attr_tP.sched_paramCP"></a> <a id="pthread_8h_1a579e6529f0ce482312a5e77ac61cb4d5"></a> int pthread\_attr\_setschedparam(pthread\_attr\_t \*attr, const struct [sched\_param](sched.md#_CPPv411sched_param "sched_param") \*param)
:   Set schedparam attribute.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_attr_setschedparam.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EINVAL** – \- The value of param is not valid.
        - **ENOTSUP** – \- An attempt was made to set the attribute to an unsupported value.

<a id="_CPPv427pthread_attr_setschedpolicyP14pthread_attr_ti"></a>

<a id="_CPPv327pthread_attr_setschedpolicyP14pthread_attr_ti"></a> <a id="_CPPv227pthread_attr_setschedpolicyP14pthread_attr_ti"></a> <a id="pthread_attr_setschedpolicy__pthread_attr_tP.i"></a> <a id="pthread_8h_1a79b4c9e71486a87ef3014f1c660b33eb"></a> int pthread\_attr\_setschedpolicy(pthread\_attr\_t \*attr, int policy)
:   Set the schedpolicy attribute.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_attr_setschedpolicy.html>

    警告

    This function is a stub and always returns 0\.

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv425pthread_attr_setstacksizeP14pthread_attr_t6size_t"></a>

<a id="_CPPv325pthread_attr_setstacksizeP14pthread_attr_t6size_t"></a> <a id="_CPPv225pthread_attr_setstacksizeP14pthread_attr_t6size_t"></a> <a id="pthread_attr_setstacksize__pthread_attr_tP.s"></a> <a id="pthread_8h_1a812a9a455ae2ef2bb0dca4fff201a281"></a> int pthread\_attr\_setstacksize(pthread\_attr\_t \*attr, size\_t stacksize)
:   Set stacksize attribute.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_attr_setstacksize.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EINVAL** – \- The value of stacksize is less than {PTHREAD\_STACK\_MIN}.

<a id="_CPPv423pthread_barrier_destroyP17pthread_barrier_t"></a>

<a id="_CPPv323pthread_barrier_destroyP17pthread_barrier_t"></a> <a id="_CPPv223pthread_barrier_destroyP17pthread_barrier_t"></a> <a id="pthread_barrier_destroy__pthread_barrier_tP"></a> <a id="pthread_8h_1ae8ef9b4e2d7feaa1a28159991e7433ac"></a> int pthread\_barrier\_destroy(pthread\_barrier\_t \*barrier)
:   Destroy a barrier object.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_barrier_destroy.html>

    备注

    This function does not validate whether there is any thread blocking on the barrier before destroying.

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv420pthread_barrier_initP17pthread_barrier_tPK21pthread_barrierattr_tj"></a>

<a id="_CPPv320pthread_barrier_initP17pthread_barrier_tPK21pthread_barrierattr_tj"></a> <a id="_CPPv220pthread_barrier_initP17pthread_barrier_tPK21pthread_barrierattr_tj"></a> <a id="pthread_barrier_init__pthread_barrier_tP.pthread_barrierattr_tCP.unsigned"></a> <a id="pthread_8h_1ae3328293a058e9c0641dbdbdfff3761e"></a> int pthread\_barrier\_init(pthread\_barrier\_t \*barrier, const pthread\_barrierattr\_t \*attr, unsigned count)
:   Initialize a barrier object.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_barrier_init.html>

    备注

    attr is ignored.

    备注

    [pthread\_barrier\_init()](#pthread_8h_1ae3328293a058e9c0641dbdbdfff3761e) is implemented with FreeRTOS event group. To ensure count fits in event group, count may be at most 8 when configUSE\_16\_BIT\_TICKS is 1; it may be at most 24 otherwise. configUSE\_16\_BIT\_TICKS is configured in application FreeRTOSConfig.h file, which defines how many bits tick count type has. See further details and limitation about event group and configUSE\_16\_BIT\_TICKS in FreeRTOS site.

    Return values
    :   - **0** – \- Upon successful completion.
        - **EINVAL** – \- The value specified by count is equal to zero.
        - **ENOMEM** – \- count cannot fit into FreeRTOS event group type OR insufficient memory exists to initialize the barrier.

<a id="_CPPv420pthread_barrier_waitP17pthread_barrier_t"></a>

<a id="_CPPv320pthread_barrier_waitP17pthread_barrier_t"></a> <a id="_CPPv220pthread_barrier_waitP17pthread_barrier_t"></a> <a id="pthread_barrier_wait__pthread_barrier_tP"></a> <a id="pthread_8h_1a85f92053b4d12aa94927b364b5b757d9"></a> int pthread\_barrier\_wait(pthread\_barrier\_t \*barrier)
:   Synchronize at a barrier.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_barrier_wait.html>

    Return values
    :   - **PTHREAD\_BARRIER\_SERIAL\_THREAD** – \- Upon successful completion, the first thread.
        - **0** – \- Upon successful completion, other thread(s).

<a id="_CPPv414pthread_createP9pthread_tPK14pthread_attr_tPFPvPvEPv"></a>

<a id="_CPPv314pthread_createP9pthread_tPK14pthread_attr_tPFPvPvEPv"></a> <a id="_CPPv214pthread_createP9pthread_tPK14pthread_attr_tPFPvPvEPv"></a> <a id="pthread_8h_1acdedb73c415d4418ac8f2512a9a4596f"></a> int pthread\_create(pthread\_t \*thread, const pthread\_attr\_t \*attr, void \*(\*startroutine)(void\*), void \*arg)
:   Thread creation.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_create.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EAGAIN** – \- Insufficient memory for either thread structure or task creation.

<a id="_CPPv422pthread_cond_broadcastP14pthread_cond_t"></a>

<a id="_CPPv322pthread_cond_broadcastP14pthread_cond_t"></a> <a id="_CPPv222pthread_cond_broadcastP14pthread_cond_t"></a> <a id="pthread_cond_broadcast__pthread_cond_tP"></a> <a id="pthread_8h_1afc4b19aa8ea2dce0956579ce878b4998"></a> int pthread\_cond\_broadcast(pthread\_cond\_t \*cond)
:   Broadcast a condition.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_cond_broadcast.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv420pthread_cond_destroyP14pthread_cond_t"></a>

<a id="_CPPv320pthread_cond_destroyP14pthread_cond_t"></a> <a id="_CPPv220pthread_cond_destroyP14pthread_cond_t"></a> <a id="pthread_cond_destroy__pthread_cond_tP"></a> <a id="pthread_8h_1aa1587e01856a579b78effd0a1a284a47"></a> int pthread\_cond\_destroy(pthread\_cond\_t \*cond)
:   Destroy condition variables.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_cond_destroy.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv417pthread_cond_initP14pthread_cond_tPK18pthread_condattr_t"></a>

<a id="_CPPv317pthread_cond_initP14pthread_cond_tPK18pthread_condattr_t"></a> <a id="_CPPv217pthread_cond_initP14pthread_cond_tPK18pthread_condattr_t"></a> <a id="pthread_cond_init__pthread_cond_tP.pthread_condattr_tCP"></a> <a id="pthread_8h_1ad5b6c558bcd5260289981207b9ca9687"></a> int pthread\_cond\_init(pthread\_cond\_t \*cond, const pthread\_condattr\_t \*attr)
:   Initialize condition variables.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_cond_init.html>

    备注

    attr is ignored and treated as NULL. Default setting is always used.

    Return values
    :   - **0** – \- Upon successful completion.
        - **ENOMEM** – \- Insufficient memory exists to initialize the condition variable.

<a id="_CPPv419pthread_cond_signalP14pthread_cond_t"></a>

<a id="_CPPv319pthread_cond_signalP14pthread_cond_t"></a> <a id="_CPPv219pthread_cond_signalP14pthread_cond_t"></a> <a id="pthread_cond_signal__pthread_cond_tP"></a> <a id="pthread_8h_1a20f98235b024efb10e5c76a64f0d94e5"></a> int pthread\_cond\_signal(pthread\_cond\_t \*cond)
:   Signal a condition.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_cond_signal.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv422pthread_cond_timedwaitP14pthread_cond_tP15pthread_mutex_tPK8timespec"></a>

<a id="_CPPv322pthread_cond_timedwaitP14pthread_cond_tP15pthread_mutex_tPK8timespec"></a> <a id="_CPPv222pthread_cond_timedwaitP14pthread_cond_tP15pthread_mutex_tPK8timespec"></a> <a id="pthread_cond_timedwait__pthread_cond_tP.pthread_mutex_tP.timespecCP"></a> <a id="pthread_8h_1ab03e3ab6546f661d2b2f83bc12559e40"></a> int pthread\_cond\_timedwait(pthread\_cond\_t \*cond, pthread\_mutex\_t \*mutex, const struct [timespec](time.md#_CPPv48timespec "timespec") \*abstime)
:   Wait on a condition with a timeout.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_cond_timedwait.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EINVAL** – \- The abstime argument passed in does not refer to an initialized structure OR the abstime parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million.
        - **ETIMEDOUT** – \- The time specified by abstime to [pthread\_cond\_timedwait()](#pthread_8h_1ab03e3ab6546f661d2b2f83bc12559e40) has passed.

<a id="_CPPv417pthread_cond_waitP14pthread_cond_tP15pthread_mutex_t"></a>

<a id="_CPPv317pthread_cond_waitP14pthread_cond_tP15pthread_mutex_t"></a> <a id="_CPPv217pthread_cond_waitP14pthread_cond_tP15pthread_mutex_t"></a> <a id="pthread_cond_wait__pthread_cond_tP.pthread_mutex_tP"></a> <a id="pthread_8h_1a907ae104b6dfd8fc12e23e84952aa7ca"></a> int pthread\_cond\_wait(pthread\_cond\_t \*cond, pthread\_mutex\_t \*mutex)
:   Wait on a condition.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_cond_wait.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv413pthread_equal9pthread_t9pthread_t"></a>

<a id="_CPPv313pthread_equal9pthread_t9pthread_t"></a> <a id="_CPPv213pthread_equal9pthread_t9pthread_t"></a> <a id="pthread_equal__pthread_t.pthread_t"></a> <a id="pthread_8h_1a98ec817164a6641eda2341de473b659d"></a> int pthread\_equal(pthread\_t t1, pthread\_t t2)
:   Compare thread IDs.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_equal.html>

    Return values
    :   - **0** – \- t1 and t2 are both not NULL \&\& equal.
        - **non-zero** – \- otherwise.

<a id="_CPPv412pthread_exitPv"></a>

<a id="_CPPv312pthread_exitPv"></a> <a id="_CPPv212pthread_exitPv"></a> <a id="pthread_exit__voidP"></a> <a id="pthread_8h_1a090bdc13141e76205fab4cb3c5fab0e4"></a> void pthread\_exit(void \*value\_ptr)
:   Thread termination.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_exit.html>

    Return values
    :   **void** – \- this function cannot return to its caller.

<a id="_CPPv421pthread_getschedparam9pthread_tPiP11sched_param"></a>

<a id="_CPPv321pthread_getschedparam9pthread_tPiP11sched_param"></a> <a id="_CPPv221pthread_getschedparam9pthread_tPiP11sched_param"></a> <a id="pthread_getschedparam__pthread_t.iP.sched_paramP"></a> <a id="pthread_8h_1aae9850b3759769c748727e171c4c6e61"></a> int pthread\_getschedparam(pthread\_t thread, int \*policy, struct [sched\_param](sched.md#_CPPv411sched_param "sched_param") \*param)
:   Dynamic thread scheduling parameters access.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_getschedparam.html>

    备注

    policy is always set to SCHED\_OTHER by this function.

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv412pthread_join9pthread_tPPv"></a>

<a id="_CPPv312pthread_join9pthread_tPPv"></a> <a id="_CPPv212pthread_join9pthread_tPPv"></a> <a id="pthread_join__pthread_t.voidPP"></a> <a id="pthread_8h_1a28a15bba47cab57cbc9f5dac9af99c8b"></a> int pthread\_join(pthread\_t thread, void \*\*retval)
:   Wait for thread termination.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_join.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EDEADLK** – \- The value specified by the thread argument to [pthread\_join()](#pthread_8h_1a28a15bba47cab57cbc9f5dac9af99c8b) does not refer to a joinable thread OR multiple simultaneous calls to [pthread\_join()](#pthread_8h_1a28a15bba47cab57cbc9f5dac9af99c8b) specifying the same target thread OR the value specified by the thread argument to [pthread\_join()](#pthread_8h_1a28a15bba47cab57cbc9f5dac9af99c8b) refers to the calling thread.

<a id="_CPPv421pthread_mutex_destroyP15pthread_mutex_t"></a>

<a id="_CPPv321pthread_mutex_destroyP15pthread_mutex_t"></a> <a id="_CPPv221pthread_mutex_destroyP15pthread_mutex_t"></a> <a id="pthread_mutex_destroy__pthread_mutex_tP"></a> <a id="pthread_8h_1a3cf620ff3a40af11d79cf28901dc55e2"></a> int pthread\_mutex\_destroy(pthread\_mutex\_t \*mutex)
:   Destroy a mutex.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutex_destroy.html>

    备注

    If there exists a thread holding this mutex, this function returns 0 with mutex not being destroyed.

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv418pthread_mutex_initP15pthread_mutex_tPK19pthread_mutexattr_t"></a>

<a id="_CPPv318pthread_mutex_initP15pthread_mutex_tPK19pthread_mutexattr_t"></a> <a id="_CPPv218pthread_mutex_initP15pthread_mutex_tPK19pthread_mutexattr_t"></a> <a id="pthread_mutex_init__pthread_mutex_tP.pthread_mutexattr_tCP"></a> <a id="pthread_8h_1a7454d249ed94ad5d5e57ba1529d7a7f2"></a> int pthread\_mutex\_init(pthread\_mutex\_t \*mutex, const pthread\_mutexattr\_t \*attr)
:   Initialize a mutex.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutex_init.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **ENOMEM** – \- Insufficient memory exists to initialize the mutex structure.
        - **EAGAIN** – \- Unable to initialize the mutex structure member(s).

<a id="_CPPv418pthread_mutex_lockP15pthread_mutex_t"></a>

<a id="_CPPv318pthread_mutex_lockP15pthread_mutex_t"></a> <a id="_CPPv218pthread_mutex_lockP15pthread_mutex_t"></a> <a id="pthread_mutex_lock__pthread_mutex_tP"></a> <a id="pthread_8h_1a12809c44718c21544ceb280dc1a53573"></a> int pthread\_mutex\_lock(pthread\_mutex\_t \*mutex)
:   Lock a mutex.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutex_lock.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EINVAL** – \- the abstime parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million.
        - **EDEADLK** – \- The mutex type is PTHREAD\_MUTEX\_ERRORCHECK and the current thread already owns the mutex.

<a id="_CPPv423pthread_mutex_timedlockP15pthread_mutex_tPK8timespec"></a>

<a id="_CPPv323pthread_mutex_timedlockP15pthread_mutex_tPK8timespec"></a> <a id="_CPPv223pthread_mutex_timedlockP15pthread_mutex_tPK8timespec"></a> <a id="pthread_mutex_timedlock__pthread_mutex_tP.timespecCP"></a> <a id="pthread_8h_1a5f197c3d769dee7a09d911241a7b6766"></a> int pthread\_mutex\_timedlock(pthread\_mutex\_t \*mutex, const struct [timespec](time.md#_CPPv48timespec "timespec") \*abstime)
:   Lock a mutex with timeout.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutex_timedlock.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EINVAL** – \- The abstime argument passed in does not refer to an initialized structure OR the abstime parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million.
        - **EDEADLK** – \- The mutex type is PTHREAD\_MUTEX\_ERRORCHECK and the current thread already owns the mutex.
        - **ETIMEDOUT** – \- The mutex could not be locked before the specified timeout expired.

<a id="_CPPv421pthread_mutex_trylockP15pthread_mutex_t"></a>

<a id="_CPPv321pthread_mutex_trylockP15pthread_mutex_t"></a> <a id="_CPPv221pthread_mutex_trylockP15pthread_mutex_t"></a> <a id="pthread_mutex_trylock__pthread_mutex_tP"></a> <a id="pthread_8h_1a27da386211db1a7e9a3b2a0db4d22144"></a> int pthread\_mutex\_trylock(pthread\_mutex\_t \*mutex)
:   Attempt to lock a mutex. Fail immediately if mutex is already locked.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutex_trylock.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EINVAL** – \- the abstime parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million.
        - **EDEADLK** – \- The mutex type is PTHREAD\_MUTEX\_ERRORCHECK and the current thread already owns the mutex.
        - **EBUSY** – \- The mutex could not be acquired because it was already locked.

<a id="_CPPv420pthread_mutex_unlockP15pthread_mutex_t"></a>

<a id="_CPPv320pthread_mutex_unlockP15pthread_mutex_t"></a> <a id="_CPPv220pthread_mutex_unlockP15pthread_mutex_t"></a> <a id="pthread_mutex_unlock__pthread_mutex_tP"></a> <a id="pthread_8h_1a96184290ffb60e04c53a52869cf960a2"></a> int pthread\_mutex\_unlock(pthread\_mutex\_t \*mutex)
:   Unlock a mutex.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutex_unlock.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EPERM** – \- The mutex type is PTHREAD\_MUTEX\_ERRORCHECK or PTHREAD\_MUTEX\_RECURSIVE, and the current thread does not own the mutex.

<a id="_CPPv425pthread_mutexattr_destroyP19pthread_mutexattr_t"></a>

<a id="_CPPv325pthread_mutexattr_destroyP19pthread_mutexattr_t"></a> <a id="_CPPv225pthread_mutexattr_destroyP19pthread_mutexattr_t"></a> <a id="pthread_mutexattr_destroy__pthread_mutexattr_tP"></a> <a id="pthread_8h_1a2321aabf58224b06021185708d0f9658"></a> int pthread\_mutexattr\_destroy(pthread\_mutexattr\_t \*attr)
:   Destroy the mutex attributes object.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutexattr_destroy.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv425pthread_mutexattr_gettypePK19pthread_mutexattr_tPi"></a>

<a id="_CPPv325pthread_mutexattr_gettypePK19pthread_mutexattr_tPi"></a> <a id="_CPPv225pthread_mutexattr_gettypePK19pthread_mutexattr_tPi"></a> <a id="pthread_mutexattr_gettype__pthread_mutexattr_tCP.iP"></a> <a id="pthread_8h_1a7f064a4db96a009a5a9a7c7e5cc03599"></a> int pthread\_mutexattr\_gettype(const pthread\_mutexattr\_t \*attr, int \*type)
:   Get the mutex type attribute.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutexattr_gettype.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv422pthread_mutexattr_initP19pthread_mutexattr_t"></a>

<a id="_CPPv322pthread_mutexattr_initP19pthread_mutexattr_t"></a> <a id="_CPPv222pthread_mutexattr_initP19pthread_mutexattr_t"></a> <a id="pthread_mutexattr_init__pthread_mutexattr_tP"></a> <a id="pthread_8h_1af98f6b6c483077a39d1400b1de1577b8"></a> int pthread\_mutexattr\_init(pthread\_mutexattr\_t \*attr)
:   Initialize the mutex attributes object.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutexattr_init.html>

    备注

    Currently, only the type attribute is supported. Also see [pthread\_mutexattr\_settype()](#pthread_8h_1a8387c80e660e9426f801ac0217ecfae5) and [pthread\_mutexattr\_gettype()](#pthread_8h_1a7f064a4db96a009a5a9a7c7e5cc03599).

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv425pthread_mutexattr_settypeP19pthread_mutexattr_ti"></a>

<a id="_CPPv325pthread_mutexattr_settypeP19pthread_mutexattr_ti"></a> <a id="_CPPv225pthread_mutexattr_settypeP19pthread_mutexattr_ti"></a> <a id="pthread_mutexattr_settype__pthread_mutexattr_tP.i"></a> <a id="pthread_8h_1a8387c80e660e9426f801ac0217ecfae5"></a> int pthread\_mutexattr\_settype(pthread\_mutexattr\_t \*attr, int type)
:   Set the mutex type attribute.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_mutexattr_settype.html>

    Return values
    :   - **0** – \- Upon successful completion.
        - **EINVAL** – \- The value type is invalid.

<a id="_CPPv412pthread_selfv"></a>

<a id="_CPPv312pthread_selfv"></a> <a id="_CPPv212pthread_selfv"></a> <a id="pthread_self__void"></a> <a id="pthread_8h_1a4c4f5f3b4f8f45d9d897847d53b11aaa"></a> pthread\_t pthread\_self(void)
:   Get the calling thread ID.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_self.html>

    Return values
    :   **the** – thread ID of the calling thread.

<a id="_CPPv421pthread_setschedparam9pthread_tiPK11sched_param"></a>

<a id="_CPPv321pthread_setschedparam9pthread_tiPK11sched_param"></a> <a id="_CPPv221pthread_setschedparam9pthread_tiPK11sched_param"></a> <a id="pthread_setschedparam__pthread_t.i.sched_paramCP"></a> <a id="pthread_8h_1a14f50e1f5d815c90f1f4225eca5d3a8c"></a> int pthread\_setschedparam(pthread\_t thread, int policy, const struct [sched\_param](sched.md#_CPPv411sched_param "sched_param") \*param)
:   Dynamic thread scheduling parameters access.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/pthread_setschedparam.html>

    备注

    policy is ignored; only priority (param.sched\_priority) may be changed.

    Return values
    :   **0** – \- Upon successful completion.

<a id="macros"></a>

## Macros

<a id="c.PTHREAD_CREATE_DETACHED"></a>

<a id="pthread_8h_1a391c5eb0f6b5febc48710d0be3f62394"></a> PTHREAD\_CREATE\_DETACHED
:   Detached.

<a id="c.PTHREAD_CREATE_JOINABLE"></a>

<a id="pthread_8h_1afb10d234d831c7b57768d62786748bc7"></a> PTHREAD\_CREATE\_JOINABLE
:   Joinable (default).

<a id="c.PTHREAD_BARRIER_SERIAL_THREAD"></a>

<a id="pthread_8h_1a822c63bc662ad86cfb2dcec50edbb42b"></a> PTHREAD\_BARRIER\_SERIAL\_THREAD

<a id="c.PTHREAD_MUTEX_NORMAL"></a>

<a id="pthread_8h_1aae4b650085c2599674938f503d6253cf"></a> PTHREAD\_MUTEX\_NORMAL
:   Non-robust, deadlock on relock, does not remember owner.

<a id="c.PTHREAD_MUTEX_ERRORCHECK"></a>

<a id="pthread_8h_1aaf502496651f95b06be861af7902cb23"></a> PTHREAD\_MUTEX\_ERRORCHECK
:   Non-robust, error on relock, remembers owner.

<a id="c.PTHREAD_MUTEX_RECURSIVE"></a>

<a id="pthread_8h_1a715e9644a7183d98cb2c9dd41cb89645"></a> PTHREAD\_MUTEX\_RECURSIVE
:   Non-robust, recursive relock, remembers owner.

<a id="c.PTHREAD_MUTEX_DEFAULT"></a>

<a id="pthread_8h_1a2a9b96c0491ae490c17d0b400bc427b0"></a> PTHREAD\_MUTEX\_DEFAULT
:   PTHREAD\_MUTEX\_NORMAL (default).
