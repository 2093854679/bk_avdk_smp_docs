# signal接口介绍

> - 需要包含头文件#include <posix/signal.h>;
> - 定义了系统信号相关的接口



## Header File


- [signal.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/signal.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/signal.h")


## Unions

union sigval
:   *#include <signal.h>*

    Signal value.

    Public Members

    int sival_int
    :   Integer signal value.

    void *sival_ptr
    :   Pointer signal value.


## Structures

struct sigevent
:   Signal event structure.

    Public Members

    int sigev_notify
    :   Notification type. A value of SIGEV_SIGNAL is not supported.

    int sigev_signo
    :   Signal number. This member is ignored.

    union [sigval](#_CPPv46sigval "sigval") sigev_value
    :   Signal value. Only the sival_ptr member is used.

    void (*sigev_notify_function)(union [sigval](#_CPPv46sigval "sigval"))
    :   Notification function.

    pthread_attr_t *sigev_notify_attributes
    :   Notification attributes.


## Macros

SIGEV_NONE
:   No asynchronous notification is delivered when the event of interest occurs.

SIGEV_SIGNAL
:   A queued signal, with an application-defined value, is generated when the event of interest occurs. Not supported.

SIGEV_THREAD
:   A notification function is called to perform notification.
