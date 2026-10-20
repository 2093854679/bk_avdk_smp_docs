---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/system/posix/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="posix-apis"></a>

# POSIX APIs

<a id="id1"></a>

## POSIX APIs 介绍

> - 目前Armino平台posix接口仅支持FreeRTOS V10.4操作系统，默认关闭;
> - 若打开使用，需要打开CONFIG\_FREERTOS\_POSIX配置开关

备注

- 在使用FreeRTOS的posix功能的时候，在引用posix相关头文件之前，需要先引用FreeRTOS\_POSIX.h头文件；
- 可以在components/bk\_rtos/freertos/posix/freertos\_impl/include/portable/bk/FreeRTOS\_POSIX\_portable.h中自定义相关配置。

- [unistd接口](posix/unistd.md)
- [utils接口](posix/utils.md)
- [errno接口](posix/errno.md)
- [fcntl接口](posix/fcntl.md)
- [signal接口](posix/signal.md)
- [mqueue接口](posix/mqueue.md)
- [pthread接口](posix/pthread.md)
- [sched接口](posix/sched.md)
- [semaphore接口](posix/semaphore.md)
- [time接口](posix/time.md)

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [外设](../peripheral.md)
- [系统](../system.md)
- [操作系统](os.md)
- [内存](mem.md)
- [事件机制](bk_event.md)
- [多核 Mailbox](logic_mailbox.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
