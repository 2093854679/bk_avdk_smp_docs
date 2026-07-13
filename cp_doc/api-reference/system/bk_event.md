# 事件机制


Armino 事件模块提供发布/订阅式通知（如 Wi-Fi 连接状态、IP 获取等）。头文件为
`components/bk_event/bk_event.h`；Wi-Fi 相关事件说明见
[Wi-Fi 事件](../../developer-guide/wifi/bk_event.md "../../developer-guide/wifi/bk_event.md")。


## Header File


- [event.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/event.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/event.h")


## Functions

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") bk_event_register_cb([event_module_t](#_CPPv414event_module_t "event_module_t") event_module_id, int event_id, [event_cb_t](#_CPPv410event_cb_t "event_cb_t") event_cb, void *event_cb_arg)
:   Register event callback.

    参数
    :   - **event_module_id** – the module ID of the event to register the callback for

        - **event_id** – the id of the event to register the callback for

        - **event_cb** – the callback which gets called when the event is dispatched

        - **event_cb_arg** – data, aside from event data, that is passed to the handler when it is called

    返回
    :   - BK_OK: succeed

        - BK_ERR_EVENT_NOT_INIT: the event module is not initialized

        - BK_ERR_EVENT_MOD_OR_ID: the event module ID or event ID is invalid

        - BK_ERR_EVENT_NO_MEM: out of memory

        - BK_ERR_EVENT_INIT_SEM: failed to init the internal event semaphore

        - BK_ERR_EVENT_POST_QUEUE: failed to post the event to event queue

        - BK_ERR_EVENT_CB_EXIST: the event callback already unregistered

        - Others: Fail

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") bk_event_unregister_cb([event_module_t](#_CPPv414event_module_t "event_module_t") event_module_id, int event_id, [event_cb_t](#_CPPv410event_cb_t "event_cb_t") event_cb)
:   Unregister a callback.

    This function can be used to unregister a callback so that it no longer gets called during dispatch.

    参数
    :   - **event_module_id** – the ID of the module with which to unregister the callback

        - **event_id** – the ID of the event with which to unregister the callback

        - **event_cb** – the callback to be unregistered

    返回
    :   - BK_OK: Success

        - BK_ERR_EVENT_NOT_INIT: the event module is not initialized

        - BK_ERR_EVENT_MOD_OR_ID: the event module ID or event ID is invalid

        - BK_ERR_EVENT_NO_MEM: out of memory

        - BK_ERR_EVENT_INIT_SEM: failed to init the internal event semaphore

        - BK_ERR_EVENT_POST_QUEUE: failed to post the event to event queue

        - BK_ERR_EVENT_NO_CB: the event callback already unregistered

        - Others: Fail

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") bk_event_post([event_module_t](#_CPPv414event_module_t "event_module_t") event_module_id, int event_id, void *event_data, size_t event_data_size, uint32_t timeout)
:   Posts an event to the event task.

    参数
    :   - **event_module_id** – The ID of the module that generates the event

        - **event_id** – the event id that identifies the event

        - **event_data** – the data, specific to the event occurence, that gets passed to the callback

        - **event_data_size** – the size of the event data

        - **timeout** – number of milliseconds to block on a full event queue

    返回
    :   - BK_OK: Success

        - BK_ERR_EVENT_NOT_INIT: the event module is not initialized

        - BK_ERR_EVENT_MOD_OR_ID: the event module ID or event ID is not invalid

        - BK_ERR_EVENT_NO_MEM: out of memory

        - BK_ERR_EVENT_INIT_SEM: failed to init the internal event semaphore

        - BK_ERR_EVENT_POST_QUEUE: failed to post the event to event queue

        - Others: Fail

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") bk_event_init(void)
:   Init the event module.

    This API initializes the event queue and create the event task.

    This API should be called before any event API is called, generally it should be called before WiFi/BLE is initialized.

    返回
    :   - BK_OK: succeed

        - BK_ERR_EVENT_CREATE_QUEUE: failed to create event queue

        - BK_ERR_EVENT_CREATE_TASK: failed to create event task

        - Others: Fail

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") bk_event_deinit(void)
:   Deinit the event module.

    This API destroy the event queue and delete the event task.

    返回
    :   - BK_OK: succeed

        - BK_ERR_NO_MEM: out of memory

        - Others: Fail

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") bk_event_dump(void)
:   Dump all registered event callback.


    **Attention**
    :   This API is for debug only

    返回
    :   - BK_OK: succeed

        - BK_ERR_NO_MEM: out of memory

        - Others: Fail


## Macros

BK_ERR_EVENT_MOD
:   Event module is not supported

BK_ERR_EVENT_ID
:   Event ID is not supported

BK_ERR_EVENT_MOD_OR_ID
:   Event ID or Module is invalid

BK_ERR_EVENT_CB_EXIST
:   Event cb already registered

BK_ERR_EVENT_NO_CB
:   No event cb is registered

BK_ERR_EVENT_CREATE_QUEUE
:   Failed to create event message queue

BK_ERR_EVENT_CREATE_MUTEX
:   Failed to create event mutex

BK_ERR_EVENT_CREATE_TASK
:   Failed to create event task

BK_ERR_EVENT_NULL_MSG
:   Event message is NULL

BK_ERR_EVENT_INIT_SEM
:   Failed to init RTOS semaphore

BK_ERR_EVENT_NOT_INIT
:   Event module not init

BK_ERR_EVENT_POST_QUEUE
:   Failed to post event request to event queue

BK_ERR_EVENT_UNKNOWN_MSG
:   Not supported event message

EVENT_ID_ALL
:   All events in a event module


## Type Definitions

typedef [bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") (*event_cb_t)(void *arg, [event_module_t](#_CPPv414event_module_t "event_module_t") event_module, int event_id, void *event_data)
:   Event callback.

    The event callback get called when related event dispatched.

typedef [bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") (*event_callback_t)(void *arg, [event_module_t](#_CPPv414event_module_t "event_module_t") event_module, int event_id, void *event_data)


## Enumerations

enum event_module_t
:   *Values:*

    enumerator EVENT_MOD_WIFI_INTERNAL
    :   WiFi internal event

    enumerator EVENT_MOD_WIFI
    :   WiFi public event

    enumerator EVENT_MOD_NETIF
    :   Netif event

    enumerator EVENT_MOD_COUNT
    :   Event module count
