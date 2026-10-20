---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/api-reference/system/posix/time.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="time"></a>

# time接口介绍

> - 需要包含头文件#include \<posix/time.h\>;
> - 定义了系统定时器相关的接口

<a id="header-file"></a>

## Header File

- [time.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/_header_files/include/posix/time.h)

<a id="functions"></a>

## Functions

<a id="_CPPv45clockv"></a>

<a id="_CPPv35clockv"></a> <a id="_CPPv25clockv"></a> <a id="clock__void"></a> <a id="time_8h_1ade863cfcca9ee19f20ca95796f8ddc1e"></a> clock\_t clock(void)
:   Report CPU time used.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/clock.html>

    备注

    This function does NOT report the number of ticks spent by the calling thread.

    返回
    :   The number of FreeRTOS ticks since the scheduler was started minus the ticks spent in the idle task.

<a id="_CPPv419clock_getcpuclockid5pid_tP9clockid_t"></a>

<a id="_CPPv319clock_getcpuclockid5pid_tP9clockid_t"></a> <a id="_CPPv219clock_getcpuclockid5pid_tP9clockid_t"></a> <a id="clock_getcpuclockid__pid_t.clockid_tP"></a> <a id="time_8h_1ab2cd29aa41b2b485b571f05ac22d9f7f"></a> int clock\_getcpuclockid(pid\_t pid, clockid\_t \*clock\_id)
:   Access a process CPU-time clock.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/clock_getcpuclockid.html>

    备注

    This function is currently unsupported.

    Return values
    :   **EPERM** –

<a id="_CPPv412clock_getres9clockid_tP8timespec"></a>

<a id="_CPPv312clock_getres9clockid_tP8timespec"></a> <a id="_CPPv212clock_getres9clockid_tP8timespec"></a> <a id="clock_getres__clockid_t.timespecP"></a> <a id="time_8h_1a463c567de23a4f064b415a959fe2a96b"></a> int clock\_getres(clockid\_t clock\_id, struct [timespec](#_CPPv48timespec "timespec") \*res)
:   Returns the resolution of a clock.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/clock_getres.html>

    备注

    clock\_id is ignored

    备注

    This function stores the resolution of the FreeRTOS tick count in the object res points to.

    Return values
    :   **0** – \- Upon successful execution

<a id="_CPPv413clock_gettime9clockid_tP8timespec"></a>

<a id="_CPPv313clock_gettime9clockid_tP8timespec"></a> <a id="_CPPv213clock_gettime9clockid_tP8timespec"></a> <a id="clock_gettime__clockid_t.timespecP"></a> <a id="time_8h_1a10b73e75d375e5c244e32ea46be775bf"></a> int clock\_gettime(clockid\_t clock\_id, struct [timespec](#_CPPv48timespec "timespec") \*tp)
:   Returns the current value for the specified clock, clock\_id.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/clock_gettime.html>

    备注

    clock\_id is ignored

    备注

    this function does not check for overflows of time\_t.

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv415clock_nanosleep9clockid_tiPK8timespecP8timespec"></a>

<a id="_CPPv315clock_nanosleep9clockid_tiPK8timespecP8timespec"></a> <a id="_CPPv215clock_nanosleep9clockid_tiPK8timespecP8timespec"></a> <a id="clock_nanosleep__clockid_t.i.timespecCP.timespecP"></a> <a id="time_8h_1a924d51d78cdcd9d7dee2613fb3a33cd1"></a> int clock\_nanosleep(clockid\_t clock\_id, int flags, const struct [timespec](#_CPPv48timespec "timespec") \*rqtp, struct [timespec](#_CPPv48timespec "timespec") \*rmtp)
:   High resolution sleep with specifiable clock.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/clock_nanosleep.html>

    备注

    clock\_id is ignored, as this function uses the FreeRTOS tick count as its clock.

    备注

    flags is ignored, if INCLUDE\_vTaskDelayUntil is 0\. i.e. the FreeRTOS function vTaskDelayUntil isn’t available.

    备注

    rmtp is also ignored, as signals are not implemented.

    Return values
    :   - **0** – \- Upon successful completion.
        - **EINVAL** – \- The rqtp argument specified a nanosecond value less than zero or greater than or equal to 1000 million.

<a id="_CPPv413clock_settime9clockid_tPK8timespec"></a>

<a id="_CPPv313clock_settime9clockid_tPK8timespec"></a> <a id="_CPPv213clock_settime9clockid_tPK8timespec"></a> <a id="clock_settime__clockid_t.timespecCP"></a> <a id="time_8h_1ab0dbabb3e47efe9483b81235fdd0c297"></a> int clock\_settime(clockid\_t clock\_id, const struct [timespec](#_CPPv48timespec "timespec") \*tp)
:   Sets the time for the specified clock.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/clock_settime.html>

    备注

    This function is currently unsupported, as FreeRTOS does not provide a function to modify the tick count.

    Return values
    :   **-1** – with errno set to EPERM.

<a id="_CPPv49nanosleepPK8timespecP8timespec"></a>

<a id="_CPPv39nanosleepPK8timespecP8timespec"></a> <a id="_CPPv29nanosleepPK8timespecP8timespec"></a> <a id="nanosleep__timespecCP.timespecP"></a> <a id="time_8h_1a9ce6a1ed91a601dee133c8b6cf8b721a"></a> int nanosleep(const struct [timespec](#_CPPv48timespec "timespec") \*rqtp, struct [timespec](#_CPPv48timespec "timespec") \*rmtp)
:   High resolution sleep.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/nanosleep.html>

    备注

    rmtp is ignored, as signals are not implemented.

    Return values
    :   - **0** – \- Upon successful completion.
        - **-1** – \- The rqtp argument is invalid OR the rqtp argument specified a nanosecond value less than zero or greater than or equal to 1000 million.

<a id="_CPPv412timer_create9clockid_tP8sigeventP7timer_t"></a>

<a id="_CPPv312timer_create9clockid_tP8sigeventP7timer_t"></a> <a id="_CPPv212timer_create9clockid_tP8sigeventP7timer_t"></a> <a id="timer_create__clockid_t.sigeventP.timer_tP"></a> <a id="time_8h_1aade0bf466f5cbd364bc9ba7a73510891"></a> int timer\_create(clockid\_t clockid, struct [sigevent](signal.md#_CPPv48sigevent "sigevent") \*evp, timer\_t \*timerid)
:   Create a per-process timer.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/timer_create.html>

    @sideeffect Possible errno values

    ENOTSUP \- If evp is NULL OR evp-\>sigen\_notify \=\= SIGEV\_SIGNAL.

    EAGAIN \- The system lacks sufficient signal queuing resources to honor the request.

    备注

    clock\_id is ignored, as this function used the FreeRTOS tick count as its clock.

    备注

    evp.sigev\_notify must be set to SIGEV\_THREAD, since signals are currently not supported.

    Return values
    :   - **0** – \- Upon successful completion, with location referenced by timerid updated.
        - **-1** – \- If an error occurs. errno is also set.

<a id="_CPPv412timer_delete7timer_t"></a>

<a id="_CPPv312timer_delete7timer_t"></a> <a id="_CPPv212timer_delete7timer_t"></a> <a id="timer_delete__timer_t"></a> <a id="time_8h_1ad114bb350d7d5d12cff3fd19bf533303"></a> int timer\_delete(timer\_t timerid)
:   Delete a per-process timer.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/timer_delete.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv416timer_getoverrun7timer_t"></a>

<a id="_CPPv316timer_getoverrun7timer_t"></a> <a id="_CPPv216timer_getoverrun7timer_t"></a> <a id="timer_getoverrun__timer_t"></a> <a id="time_8h_1ad779f0bc22f64bd3bd977221b0ce1b8f"></a> int timer\_getoverrun(timer\_t timerid)
:   Get the timer overrun count.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/timer_getoverrun.html>

    Return values
    :   **0** – \- Always return 0, since signals are not supported.

<a id="_CPPv413timer_gettime7timer_tP10itimerspec"></a>

<a id="_CPPv313timer_gettime7timer_tP10itimerspec"></a> <a id="_CPPv213timer_gettime7timer_tP10itimerspec"></a> <a id="timer_gettime__timer_t.itimerspecP"></a> <a id="time_8h_1a520e1913c35aa3352259dafa3259d140"></a> int timer\_gettime(timer\_t timerid, struct [itimerspec](#_CPPv410itimerspec "itimerspec") \*value)
:   Get the amount of time until the timer expires.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/timer_gettime.html>

    Return values
    :   **0** – \- Upon successful completion.

<a id="_CPPv413timer_settime7timer_tiPK10itimerspecP10itimerspec"></a>

<a id="_CPPv313timer_settime7timer_tiPK10itimerspecP10itimerspec"></a> <a id="_CPPv213timer_settime7timer_tiPK10itimerspecP10itimerspec"></a> <a id="timer_settime__timer_t.i.itimerspecCP.itimerspecP"></a> <a id="time_8h_1a32207b51f2effa8441f4c728fd8519c0"></a> int timer\_settime(timer\_t timerid, int flags, const struct [itimerspec](#_CPPv410itimerspec "itimerspec") \*value, struct [itimerspec](#_CPPv410itimerspec "itimerspec") \*ovalue)
:   Set the time until the next expiration of the timer.

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/timer_settime.html>

    @sideeffect Possible errno values

    EINVAL \- A value structure specified a nanosecond value less than zero or greater than or equal to 1000 million, AND the it\_value member of that structure did not specify zero seconds and nanoseconds.

    Return values
    :   - **0** – \- Upon successful completion.
        - **-1** – \- An error occurred, errno is also set.

<a id="structures"></a>

## Structures

<a id="_CPPv48timespec"></a>

<a id="_CPPv38timespec"></a> <a id="_CPPv28timespec"></a> <a id="timespec"></a> <a id="structtimespec"></a> struct timespec
:   represents an elapsed time

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N8timespec6tv_secE"></a>

    <a id="_CPPv3N8timespec6tv_secE"></a> <a id="_CPPv2N8timespec6tv_secE"></a> <a id="timespec::tv_sec__time_t"></a> <a id="structtimespec_1afc3302668d7cb5952f590da69fdd4955"></a> time\_t tv\_sec
    :   Seconds.

    <a id="_CPPv4N8timespec7tv_nsecE"></a>

    <a id="_CPPv3N8timespec7tv_nsecE"></a> <a id="_CPPv2N8timespec7tv_nsecE"></a> <a id="timespec::tv_nsec__l"></a> <a id="structtimespec_1ae3c7510dafa8cbcaede866ed13c99683"></a> long tv\_nsec
    :   Nanoseconds.

<a id="_CPPv410itimerspec"></a>

<a id="_CPPv310itimerspec"></a> <a id="_CPPv210itimerspec"></a> <a id="itimerspec"></a> <a id="structitimerspec"></a> struct itimerspec
:   timer

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N10itimerspec11it_intervalE"></a>

    <a id="_CPPv3N10itimerspec11it_intervalE"></a> <a id="_CPPv2N10itimerspec11it_intervalE"></a> <a id="itimerspec::it_interval__timespec"></a> <a id="structitimerspec_1a27cedae552e2b2fe0993c1b2c4ff1889"></a> struct [timespec](#_CPPv48timespec "timespec") it\_interval
    :   Timer period.

    <a id="_CPPv4N10itimerspec8it_valueE"></a>

    <a id="_CPPv3N10itimerspec8it_valueE"></a> <a id="_CPPv2N10itimerspec8it_valueE"></a> <a id="itimerspec::it_value__timespec"></a> <a id="structitimerspec_1a754dda918053251c24558b07571d6e8f"></a> struct [timespec](#_CPPv48timespec "timespec") it\_value
    :   Timer expiration.

<a id="macros"></a>

## Macros

<a id="c.MICROSECONDS_PER_SECOND"></a>

<a id="time_8h_1a8a708413d6171e7d86056793abe2cd1a"></a> MICROSECONDS\_PER\_SECOND
:   Microseconds per second.

<a id="c.NANOSECONDS_PER_SECOND"></a>

<a id="time_8h_1a5df38c677104658963501aa1e2a88e60"></a> NANOSECONDS\_PER\_SECOND
:   Nanoseconds per second.

<a id="c.NANOSECONDS_PER_TICK"></a>

<a id="time_8h_1a033850a105f65ce574fc0f7de437dd14"></a> NANOSECONDS\_PER\_TICK
:   Nanoseconds per FreeRTOS tick.

<a id="c.CLOCK_REALTIME"></a>

<a id="time_8h_1a922ce1ae64374c9410c8a999e25e82af"></a> CLOCK\_REALTIME
:   The identifier of the system-wide clock measuring real time.

<a id="c.CLOCK_MONOTONIC"></a>

<a id="time_8h_1a6fb83f5e91e704391ff796553d5e0f46"></a> CLOCK\_MONOTONIC
:   The identifier for the system-wide monotonic clock.

<a id="c.CLOCKS_PER_SEC"></a>

<a id="time_8h_1a3d9fc3c745d0880902fe3ea3d5d5f71e"></a> CLOCKS\_PER\_SEC

<a id="c.TIMER_ABSTIME"></a>

<a id="time_8h_1adde83d9ea51f12d4149f016eededde54"></a> TIMER\_ABSTIME
