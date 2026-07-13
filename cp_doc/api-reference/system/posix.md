# POSIX APIs



## POSIX APIs 介绍

> - 目前Armino平台posix接口仅支持FreeRTOS V10.4操作系统，默认关闭;
> - 若打开使用，需要打开CONFIG_FREERTOS_POSIX配置开关

备注


- 在使用FreeRTOS的posix功能的时候，在引用posix相关头文件之前，需要先引用FreeRTOS_POSIX.h头文件；

- 可以在components/bk_rtos/freertos/posix/freertos_impl/include/portable/bk/FreeRTOS_POSIX_portable.h中自定义相关配置。


- [unistd接口](posix/unistd.md "unistd.md")

- [utils接口](posix/utils.md "utils.md")

- [errno接口](posix/errno.md "errno.md")

- [fcntl接口](posix/fcntl.md "fcntl.md")

- [signal接口](posix/signal.md "signal.md")

- [mqueue接口](posix/mqueue.md "mqueue.md")

- [pthread接口](posix/pthread.md "pthread.md")

- [sched接口](posix/sched.md "sched.md")

- [semaphore接口](posix/semaphore.md "semaphore.md")

- [time接口](posix/time.md "time.md")
