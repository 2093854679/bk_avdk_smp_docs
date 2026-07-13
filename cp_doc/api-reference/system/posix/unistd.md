# unistd接口介绍

> - 需要包含头文件#include <posix/unistd.h>;
> - 定义了系统sleep相关的接口



## Header File


- [unistd.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/unistd.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/unistd.h")


## Functions

unsigned sleep(unsigned seconds)
:   Suspend execution for an interval of time.

    [http://pubs.opengroup.org/onlinepubs/9699919799/functions/sleep.html](http://pubs.opengroup.org/onlinepubs/9699919799/functions/sleep.html "http://pubs.opengroup.org/onlinepubs/9699919799/functions/sleep.html")

    备注

    Return value of a positive number is not yet supported.

    参数
    :   **seconds** – **[in]** The number of seconds to suspend execution.

    Return values
    :   **0** – - Upon successful completion.

int usleep(useconds_t usec)
:   Suspend execution for microsecond intervals.

    This is a useful, non-POSIX function.

    参数
    :   **usec** – **[in]** The number of microseconds to suspend execution.

    Return values
    :   **0** – - Upon successful completion.
