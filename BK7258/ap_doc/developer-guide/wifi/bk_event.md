---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/wifi/bk_event.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 事件机制

事件机制用于向用户通知 SDK 产生的异步事件，如 WiFi 掉线等。

<a id="id2"></a>

## 实现概述

SDK 中事件机制主要是通过一个专门的事件任务来实现， 事件任务将 bk\_event\_register\_cb() 注册的
回调函数以链表形式管理起来，当 bk\_event\_register\_cb() 调用时， 事件任务在链表中增加一个结点，
当 bk\_event\_unregister\_cb() 调用时， 事件任务将链表中回调函数结点删除并释放内存， 当事件发生时，
事件任务依次调用该事件下所有回调函数。

为节省内存， Event Task 的栈大小默认为 2048 字节，可通过在 SDK 配置
文件中定义 CFG\_EVENT\_TASK\_STACK\_SIZE 来修改默认大小。

<a id="id3"></a>

## 回调函数实现注意事项

回调函数实现时应该遵守下列原则：

> - 回调函数中不应该有阻塞操作，如果回调函数被阻塞可能会影响其他事件处理
> - 回调函数调用深度尽量不要太深，否则可能会导致事件任务栈溢出
> - 回调函数中传入的数据指针在回调函数返回之后会被释放，因此，如果回调函数返回后应用程序还要访问这些数据，
>   需要在回函数中将事件数据拷贝一份

<a id="id4"></a>

## 回调函数调用顺序

当某个事件发生时， 以 EVENT\_WIFI\_STA\_CONNECTED 发生为例， 事件任务调用回调用函数的顺序如下：

> - 如果有模块关注 EVENT\_WIFI\_MOD 下所有事件，即 bk\_event\_register\_cb 时 event\_id 参数为 EVENT\_ID\_ALL，
>   依次调用注册为 EVENT\_ID\_ALL 的所有回调函数， 调用顺序为先注册先调用。
> - 依次调用 EVENT\_WIFI\_STA\_CONNECTED 事件下所有回调函数, 调用顺序为先注册先调用。

重要

一般来说，应用程序不应该对同一个事件下不同回调函数调用顺序作任何假设。

<a id="api"></a>

## API 使用举例

假设应用程序想关注 EVENT\_WIFI\_STA\_CONNECTED, 其中 user\_cb() 为用户定义的回调函数， s\_user\_cb\_arg 为回调函数用户参数，
则注册方式如下:

```
BK_LOG_ON_ERR(bk_event_register_cb(EVENT_MOD_WIFI, EVENT_WIFI_STA_CONNECTED,
            user_cb, s_user_cb_arg));
```

当 EVENT\_WIFI\_STA\_CONNECTED 产生时， 事件任务会调用 user\_cb， 并且首个参数为 s\_user\_cb\_arg。

如果应用程序想关注 WiFi 模块产生的多个或者全部事件， 除了可以按上述逐个注册回调函数之外，还可以使用下述方式注册一个回调函数处理所有
WiFi 事件:

```
BK_LOG_ON_ERR(bk_event_register_cb(EVENT_MOD_WIFI, EVENT_ID_ALL,
            user_cb, s_user_cb_arg));
```

备注

当应用不需要关注某个事件时，建议调用 bk\_event\_unregister\_cb 删除回调函数结点；特别是当回调函数指针或者用户参数不再有效时，
务必调用 bk\_event\_unregister\_cb()，以免非法回调函数调用或者参数访问造成错误。
