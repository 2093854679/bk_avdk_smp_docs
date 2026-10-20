---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/api-reference/system/posix/semaphore.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="semaphore"></a>

# semaphore接口介绍

> - 需要包含头文件#include \<posix/semaphore.h\>;
> - 定义了系统信号量相关的接口

<a id="header-file"></a>

## Header File

- [semaphore.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/_header_files/include/posix/semaphore.h)

<a id="functions"></a>

## Functions

<a id="_CPPv411sem_destroyP5sem_t"></a>

<a id="_CPPv311sem_destroyP5sem_t"></a> <a id="_CPPv211sem_destroyP5sem_t"></a> <a id="sem_destroy__sem_tP"></a> <a id="semaphore_8h_1a6bc9a7dd941a9b5e319715b767af5682"></a> int sem\_destroy([sem\_t](#_CPPv45sem_t "sem_t") \*sem)
:   Destroy an unnamed semaphore.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_destroy.html>

    备注

    Semaphore is destroyed regardless of whether there is any thread currently blocked on this semaphore.

    Return values
    :   **0** – \- upon successful completion

<a id="_CPPv412sem_getvalueP5sem_tPi"></a>

<a id="_CPPv312sem_getvalueP5sem_tPi"></a> <a id="_CPPv212sem_getvalueP5sem_tPi"></a> <a id="sem_getvalue__sem_tP.iP"></a> <a id="semaphore_8h_1a9755d3b56c40d2aec3d55b00c8f7cae8"></a> int sem\_getvalue([sem\_t](#_CPPv45sem_t "sem_t") \*sem, int \*sval)
:   Get the value of a semaphore.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_getvalue.html>

    备注

    If sem is locked, then the object to which sval points is set to zero.

    Return values
    :   **0** – \- Upon successful completion

<a id="_CPPv48sem_initP5sem_tij"></a>

<a id="_CPPv38sem_initP5sem_tij"></a> <a id="_CPPv28sem_initP5sem_tij"></a> <a id="sem_init__sem_tP.i.unsigned"></a> <a id="semaphore_8h_1a8437c38b02b5858b66f2df30f4f26435"></a> int sem\_init([sem\_t](#_CPPv45sem_t "sem_t") \*sem, int pshared, unsigned value)
:   Initialize an unnamed semaphore.

    @sideeffect Possible errno values

    EINVAL \- The value argument exceeds {SEM\_VALUE\_MAX}.

    ENOSPC \- A resource required to initialize the semaphore has been exhausted.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_init.html>

    备注

    pshared is ignored. Semaphores will always be considered “shared”.

    Return values
    :   - **0** – \- upon successful completion
        - **-1** – \- otherwise. System error variable errno is also set in this case.

<a id="_CPPv48sem_postP5sem_t"></a>

<a id="_CPPv38sem_postP5sem_t"></a> <a id="_CPPv28sem_postP5sem_t"></a> <a id="sem_post__sem_tP"></a> <a id="semaphore_8h_1a015dce85cab8477c679cc47968958247"></a> int sem\_post([sem\_t](#_CPPv45sem_t "sem_t") \*sem)
:   Unlock a semaphore.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_post.html>

    Return values
    :   **0** – \- upon successful completion

<a id="_CPPv413sem_timedwaitP5sem_tPK8timespec"></a>

<a id="_CPPv313sem_timedwaitP5sem_tPK8timespec"></a> <a id="_CPPv213sem_timedwaitP5sem_tPK8timespec"></a> <a id="sem_timedwait__sem_tP.timespecCP"></a> <a id="semaphore_8h_1a9fa286fcc7ddce4e32fa449f34a494c6"></a> int sem\_timedwait([sem\_t](#_CPPv45sem_t "sem_t") \*sem, const struct [timespec](time.md#_CPPv48timespec "timespec") \*abstime)
:   Lock a semaphore with timeout.

    @sideeffect Possible errno values

    EINVAL \- parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million

    ETIMEDOUT \- The semaphore could not be locked before the specified timeout expired.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_timedwait.html>

    备注

    Deadlock detection is not implemented.

    Return values
    :   - **0** – \- upon successful completion
        - **-1** – \- otherwise. System error variable errno is also set in this case.

<a id="_CPPv411sem_trywaitP5sem_t"></a>

<a id="_CPPv311sem_trywaitP5sem_t"></a> <a id="_CPPv211sem_trywaitP5sem_t"></a> <a id="sem_trywait__sem_tP"></a> <a id="semaphore_8h_1a4de7a9a334b01b6373b017aaefa07cf0"></a> int sem\_trywait([sem\_t](#_CPPv45sem_t "sem_t") \*sem)
:   Lock a semaphore if available.

    @sideeffect Possible errno values

    EAGAIN \- The semaphore was already locked, so it cannot be immediately locked by the

    [sem\_trywait()](#semaphore_8h_1a4de7a9a334b01b6373b017aaefa07cf0) operation.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_trywait.html>

    Return values
    :   - **0** – \- upon successful completion
        - **-1** – \- otherwise. System error variable errno is also set in this case.

<a id="_CPPv48sem_waitP5sem_t"></a>

<a id="_CPPv38sem_waitP5sem_t"></a> <a id="_CPPv28sem_waitP5sem_t"></a> <a id="sem_wait__sem_tP"></a> <a id="semaphore_8h_1aad70020dca2241a2b78e272ca033271b"></a> int sem\_wait([sem\_t](#_CPPv45sem_t "sem_t") \*sem)
:   Lock a semaphore.

    参见

    <http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_wait.html>

    备注

    Deadlock detection is not implemented.

    Return values
    :   - **0** – \- upon successful completion
        - **-1** – \- otherwise. System error variable errno is also set in this case.

<a id="type-definitions"></a>

## Type Definitions

<a id="_CPPv45sem_t"></a>

<a id="_CPPv35sem_t"></a> <a id="_CPPv25sem_t"></a> <a id="sem_t"></a> <a id="semaphore_8h_1acdcd24391f60977a34f32015c2edadaa"></a> typedef PosixSemType\_t sem\_t
:   Semaphore type.
