# semaphore接口介绍

> - 需要包含头文件#include <posix/semaphore.h>;
> - 定义了系统信号量相关的接口



## Header File


- [semaphore.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/semaphore.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/semaphore.h")


## Functions

int sem_destroy([sem_t](#_CPPv45sem_t "sem_t") *sem)
:   Destroy an unnamed semaphore.

    参见

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_destroy.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_destroy.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_destroy.html")

    备注

    Semaphore is destroyed regardless of whether there is any thread currently blocked on this semaphore.

    Return values
    :   **0** – - upon successful completion

int sem_getvalue([sem_t](#_CPPv45sem_t "sem_t") *sem, int *sval)
:   Get the value of a semaphore.

    参见

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_getvalue.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_getvalue.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_getvalue.html")

    备注

    If sem is locked, then the object to which sval points is set to zero.

    Return values
    :   **0** – - Upon successful completion

int sem_init([sem_t](#_CPPv45sem_t "sem_t") *sem, int pshared, unsigned value)
:   Initialize an unnamed semaphore.

    @sideeffect Possible errno values

    EINVAL - The value argument exceeds {SEM_VALUE_MAX}.

    ENOSPC - A resource required to initialize the semaphore has been exhausted.

    参见

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_init.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_init.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_init.html")

    备注

    pshared is ignored. Semaphores will always be considered “shared”.

    Return values
    :   - **0** – - upon successful completion

        - **-1** – - otherwise. System error variable errno is also set in this case.

int sem_post([sem_t](#_CPPv45sem_t "sem_t") *sem)
:   Unlock a semaphore.

    参见

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_post.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_post.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_post.html")

    Return values
    :   **0** – - upon successful completion

int sem_timedwait([sem_t](#_CPPv45sem_t "sem_t") *sem, const struct [timespec](time.md#_CPPv48timespec "timespec") *abstime)
:   Lock a semaphore with timeout.

    @sideeffect Possible errno values

    EINVAL - parameter specified a nanoseconds field value less than zero or greater than or equal to 1000 million

    ETIMEDOUT - The semaphore could not be locked before the specified timeout expired.

    参见

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_timedwait.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_timedwait.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_timedwait.html")

    备注

    Deadlock detection is not implemented.

    Return values
    :   - **0** – - upon successful completion

        - **-1** – - otherwise. System error variable errno is also set in this case.

int sem_trywait([sem_t](#_CPPv45sem_t "sem_t") *sem)
:   Lock a semaphore if available.

    @sideeffect Possible errno values

    EAGAIN - The semaphore was already locked, so it cannot be immediately locked by the

    [sem_trywait()](#semaphore_8h_1a4de7a9a334b01b6373b017aaefa07cf0 "#semaphore_8h_1a4de7a9a334b01b6373b017aaefa07cf0") operation.

    参见

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_trywait.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_trywait.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_trywait.html")

    Return values
    :   - **0** – - upon successful completion

        - **-1** – - otherwise. System error variable errno is also set in this case.

int sem_wait([sem_t](#_CPPv45sem_t "sem_t") *sem)
:   Lock a semaphore.

    参见

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_wait.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_wait.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sem_wait.html")

    备注

    Deadlock detection is not implemented.

    Return values
    :   - **0** – - upon successful completion

        - **-1** – - otherwise. System error variable errno is also set in this case.


## Type Definitions

typedef PosixSemType_t sem_t
:   Semaphore type.
