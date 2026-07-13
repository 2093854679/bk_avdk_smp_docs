# sched接口介绍

> - 需要包含头文件#include <posix/sched.h>;
> - 定义了系统调度相关的接口



## Header File


- [sched.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/sched.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/sched.h")


## Functions

int sched_get_priority_max(int policy)
:   Get priority limit (max).

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_get_priority_max.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_get_priority_max.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_get_priority_max.html")

    备注

    policy is ignored.

    返回
    :   the maximum priority value (0-based) system configuration allows.

        e.g. if configMAX_PRIORITIES == 7, this function returns (configMAX_PRIORITIES - 1). configMAX_PRIORITIES is configured in application FreeRTOSConfig.h file.

int sched_get_priority_min(int policy)
:   Get priority limit (min).

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_get_priority_min.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_get_priority_min.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_get_priority_min.html")

    备注

    policy is ignored.

int sched_yield(void)
:   Yield the processor.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_yield.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_yield.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sched_yield.html")

    Return values
    :   **0** – - Upon successful completion


## Structures

struct sched_param
:   Scheduling parameters required for implementation of each supported scheduling policy.

    Public Members

    int sched_priority
    :   Process or thread execution scheduling priority.


## Macros

SCHED_OTHER
:   Another scheduling policy.
