---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/system/bk_event.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 事件机制

Armino 事件模块提供发布/订阅式通知（如 Wi-Fi 连接状态、IP 获取等）。头文件为
`components/bk_event/bk_event.h`。

<a id="header-file"></a>

## Header File

- [event.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/event.h)

<a id="functions"></a>

## Functions

<a id="_CPPv420bk_event_register_cb14event_module_ti10event_cb_tPv"></a>

<a id="_CPPv320bk_event_register_cb14event_module_ti10event_cb_tPv"></a> <a id="_CPPv220bk_event_register_cb14event_module_ti10event_cb_tPv"></a> <a id="bk_event_register_cb__event_module_t.i.event_cb_t.voidP"></a> <a id="group__bk__api__event_1ga924219508b0e699883253b002130a2cc"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") bk\_event\_register\_cb([event\_module\_t](#_CPPv414event_module_t "event_module_t") event\_module\_id, int event\_id, [event\_cb\_t](#_CPPv410event_cb_t "event_cb_t") event\_cb, void \*event\_cb\_arg)
:   Register event callback.

    参数
    :   - **event\_module\_id** – the module ID of the event to register the callback for
        - **event\_id** – the id of the event to register the callback for
        - **event\_cb** – the callback which gets called when the event is dispatched
        - **event\_cb\_arg** – data, aside from event data, that is passed to the handler when it is called

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_EVENT\_NOT\_INIT: the event module is not initialized
        - BK\_ERR\_EVENT\_MOD\_OR\_ID: the event module ID or event ID is invalid
        - BK\_ERR\_EVENT\_NO\_MEM: out of memory
        - BK\_ERR\_EVENT\_INIT\_SEM: failed to init the internal event semaphore
        - BK\_ERR\_EVENT\_POST\_QUEUE: failed to post the event to event queue
        - BK\_ERR\_EVENT\_CB\_EXIST: the event callback already unregistered
        - Others: Fail

<a id="_CPPv422bk_event_unregister_cb14event_module_ti10event_cb_t"></a>

<a id="_CPPv322bk_event_unregister_cb14event_module_ti10event_cb_t"></a> <a id="_CPPv222bk_event_unregister_cb14event_module_ti10event_cb_t"></a> <a id="bk_event_unregister_cb__event_module_t.i.event_cb_t"></a> <a id="group__bk__api__event_1ga409d470b9874382bec24c670f4196cd2"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") bk\_event\_unregister\_cb([event\_module\_t](#_CPPv414event_module_t "event_module_t") event\_module\_id, int event\_id, [event\_cb\_t](#_CPPv410event_cb_t "event_cb_t") event\_cb)
:   Unregister a callback.

    This function can be used to unregister a callback so that it no longer gets called during dispatch.

    参数
    :   - **event\_module\_id** – the ID of the module with which to unregister the callback
        - **event\_id** – the ID of the event with which to unregister the callback
        - **event\_cb** – the callback to be unregistered

    返回
    :   - BK\_OK: Success
        - BK\_ERR\_EVENT\_NOT\_INIT: the event module is not initialized
        - BK\_ERR\_EVENT\_MOD\_OR\_ID: the event module ID or event ID is invalid
        - BK\_ERR\_EVENT\_NO\_MEM: out of memory
        - BK\_ERR\_EVENT\_INIT\_SEM: failed to init the internal event semaphore
        - BK\_ERR\_EVENT\_POST\_QUEUE: failed to post the event to event queue
        - BK\_ERR\_EVENT\_NO\_CB: the event callback already unregistered
        - Others: Fail

<a id="_CPPv413bk_event_post14event_module_tiPv6size_t8uint32_t"></a>

<a id="_CPPv313bk_event_post14event_module_tiPv6size_t8uint32_t"></a> <a id="_CPPv213bk_event_post14event_module_tiPv6size_t8uint32_t"></a> <a id="bk_event_post__event_module_t.i.voidP.s.uint32_t"></a> <a id="group__bk__api__event_1gaceaf3193a5e139af0e08493d1e3dcd68"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") bk\_event\_post([event\_module\_t](#_CPPv414event_module_t "event_module_t") event\_module\_id, int event\_id, void \*event\_data, size\_t event\_data\_size, uint32\_t timeout)
:   Posts an event to the event task.

    参数
    :   - **event\_module\_id** – The ID of the module that generates the event
        - **event\_id** – the event id that identifies the event
        - **event\_data** – the data, specific to the event occurence, that gets passed to the callback
        - **event\_data\_size** – the size of the event data
        - **timeout** – number of milliseconds to block on a full event queue

    返回
    :   - BK\_OK: Success
        - BK\_ERR\_EVENT\_NOT\_INIT: the event module is not initialized
        - BK\_ERR\_EVENT\_MOD\_OR\_ID: the event module ID or event ID is not invalid
        - BK\_ERR\_EVENT\_NO\_MEM: out of memory
        - BK\_ERR\_EVENT\_INIT\_SEM: failed to init the internal event semaphore
        - BK\_ERR\_EVENT\_POST\_QUEUE: failed to post the event to event queue
        - Others: Fail

<a id="_CPPv413bk_event_initv"></a>

<a id="_CPPv313bk_event_initv"></a> <a id="_CPPv213bk_event_initv"></a> <a id="bk_event_init__void"></a> <a id="group__bk__api__event_1gac988164aac6d75a79059485f1a7392eb"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") bk\_event\_init(void)
:   Init the event module.

    This API initializes the event queue and create the event task.

    This API should be called before any event API is called, generally it should be called before WiFi/BLE is initialized.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_EVENT\_CREATE\_QUEUE: failed to create event queue
        - BK\_ERR\_EVENT\_CREATE\_TASK: failed to create event task
        - Others: Fail

<a id="_CPPv415bk_event_deinitv"></a>

<a id="_CPPv315bk_event_deinitv"></a> <a id="_CPPv215bk_event_deinitv"></a> <a id="bk_event_deinit__void"></a> <a id="group__bk__api__event_1ga36721bd2596fbd4af8ea9ad9df6b4571"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") bk\_event\_deinit(void)
:   Deinit the event module.

    This API destroy the event queue and delete the event task.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NO\_MEM: out of memory
        - Others: Fail

<a id="_CPPv413bk_event_dumpv"></a>

<a id="_CPPv313bk_event_dumpv"></a> <a id="_CPPv213bk_event_dumpv"></a> <a id="bk_event_dump__void"></a> <a id="group__bk__api__event_1ga84e3620311900f1b8097594db4d24711"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") bk\_event\_dump(void)
:   Dump all registered event callback.

    **Attention**
    :   This API is for debug only

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NO\_MEM: out of memory
        - Others: Fail

<a id="macros"></a>

## Macros

<a id="c.BK_ERR_EVENT_MOD"></a>

<a id="group__bk__api__event__typedef_1gaa94cbf3a7b3954ef9f66437819c3bc01"></a> BK\_ERR\_EVENT\_MOD
:   Event module is not supported

<a id="c.BK_ERR_EVENT_ID"></a>

<a id="group__bk__api__event__typedef_1ga6cf66d73f4e29fe5a73879d3e2180e34"></a> BK\_ERR\_EVENT\_ID
:   Event ID is not supported

<a id="c.BK_ERR_EVENT_MOD_OR_ID"></a>

<a id="group__bk__api__event__typedef_1ga946e3aa6276880ddcc6ad119a2d0ae2f"></a> BK\_ERR\_EVENT\_MOD\_OR\_ID
:   Event ID or Module is invalid

<a id="c.BK_ERR_EVENT_CB_EXIST"></a>

<a id="group__bk__api__event__typedef_1ga0b29b449117ff6e4000bc249c0cbc5b0"></a> BK\_ERR\_EVENT\_CB\_EXIST
:   Event cb already registered

<a id="c.BK_ERR_EVENT_NO_CB"></a>

<a id="group__bk__api__event__typedef_1ga24110f9b3449cac26af9ac7b8b5dfd78"></a> BK\_ERR\_EVENT\_NO\_CB
:   No event cb is registered

<a id="c.BK_ERR_EVENT_CREATE_QUEUE"></a>

<a id="group__bk__api__event__typedef_1ga19c5fbeeddc77ad08e50a309dd8136d3"></a> BK\_ERR\_EVENT\_CREATE\_QUEUE
:   Failed to create event message queue

<a id="c.BK_ERR_EVENT_CREATE_MUTEX"></a>

<a id="group__bk__api__event__typedef_1ga8bdb2acd8eb72cea51dc73c490b0631a"></a> BK\_ERR\_EVENT\_CREATE\_MUTEX
:   Failed to create event mutex

<a id="c.BK_ERR_EVENT_CREATE_TASK"></a>

<a id="group__bk__api__event__typedef_1ga218b66ba20f66c858588de8bc186cad9"></a> BK\_ERR\_EVENT\_CREATE\_TASK
:   Failed to create event task

<a id="c.BK_ERR_EVENT_NULL_MSG"></a>

<a id="group__bk__api__event__typedef_1ga7416b3fc4028b3f21555066776000d7b"></a> BK\_ERR\_EVENT\_NULL\_MSG
:   Event message is NULL

<a id="c.BK_ERR_EVENT_INIT_SEM"></a>

<a id="group__bk__api__event__typedef_1gaa104c9d8df395f0c2a0bb79efe2d540e"></a> BK\_ERR\_EVENT\_INIT\_SEM
:   Failed to init RTOS semaphore

<a id="c.BK_ERR_EVENT_NOT_INIT"></a>

<a id="group__bk__api__event__typedef_1gad82459fc4ea4d023a5d85754a6fbb93c"></a> BK\_ERR\_EVENT\_NOT\_INIT
:   Event module not init

<a id="c.BK_ERR_EVENT_POST_QUEUE"></a>

<a id="group__bk__api__event__typedef_1ga95cb8ca89fb80391101d51ce6134fd13"></a> BK\_ERR\_EVENT\_POST\_QUEUE
:   Failed to post event request to event queue

<a id="c.BK_ERR_EVENT_UNKNOWN_MSG"></a>

<a id="group__bk__api__event__typedef_1ga3570e54b98c2b6ea8c62a3bae0864393"></a> BK\_ERR\_EVENT\_UNKNOWN\_MSG
:   Not supported event message

<a id="c.EVENT_ID_ALL"></a>

<a id="group__bk__api__event__typedef_1ga8b11c538f7663d160d373b4cb05e84c9"></a> EVENT\_ID\_ALL
:   All events in a event module

<a id="type-definitions"></a>

## Type Definitions

<a id="_CPPv410event_cb_t"></a>

<a id="_CPPv310event_cb_t"></a> <a id="_CPPv210event_cb_t"></a> <a id="event_cb_t"></a> <a id="group__bk__api__event_1gaf154e2918f312a2725066db02a706995"></a> typedef [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") (\*event\_cb\_t)(void \*arg, [event\_module\_t](#_CPPv414event_module_t "event_module_t") event\_module, int event\_id, void \*event\_data)
:   Event callback.

    The event callback get called when related event dispatched.

<a id="_CPPv416event_callback_t"></a>

<a id="_CPPv316event_callback_t"></a> <a id="_CPPv216event_callback_t"></a> <a id="event_callback_t"></a> <a id="event_8h_1a123bd8657acf50447f3f522b2a03fb98"></a> typedef [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") (\*event\_callback\_t)(void \*arg, [event\_module\_t](#_CPPv414event_module_t "event_module_t") event\_module, int event\_id, void \*event\_data)

<a id="enumerations"></a>

## Enumerations

<a id="_CPPv414event_module_t"></a>

<a id="_CPPv314event_module_t"></a> <a id="_CPPv214event_module_t"></a> <a id="group__bk__api__event__typedef_1ga8e1aa07a2a4e5fb9275943d957c3480d"></a> enum event\_module\_t
:   *Values:*

    <a id="_CPPv4N14event_module_t23EVENT_MOD_WIFI_INTERNALE"></a>

    <a id="_CPPv3N14event_module_t23EVENT_MOD_WIFI_INTERNALE"></a> <a id="_CPPv2N14event_module_t23EVENT_MOD_WIFI_INTERNALE"></a> <a id="group__bk__api__event__typedef_1gga8e1aa07a2a4e5fb9275943d957c3480daaf9e85b985f1a2d903efed120b2c916d"></a> enumerator EVENT\_MOD\_WIFI\_INTERNAL
    :   WiFi internal event

    <a id="_CPPv4N14event_module_t14EVENT_MOD_WIFIE"></a>

    <a id="_CPPv3N14event_module_t14EVENT_MOD_WIFIE"></a> <a id="_CPPv2N14event_module_t14EVENT_MOD_WIFIE"></a> <a id="group__bk__api__event__typedef_1gga8e1aa07a2a4e5fb9275943d957c3480da30f802bde1eb6fbcaa74c8b62d1b9996"></a> enumerator EVENT\_MOD\_WIFI
    :   WiFi public event

    <a id="_CPPv4N14event_module_t15EVENT_MOD_NETIFE"></a>

    <a id="_CPPv3N14event_module_t15EVENT_MOD_NETIFE"></a> <a id="_CPPv2N14event_module_t15EVENT_MOD_NETIFE"></a> <a id="group__bk__api__event__typedef_1gga8e1aa07a2a4e5fb9275943d957c3480dafe4941ad73fe079ab6ecd1b440b52905"></a> enumerator EVENT\_MOD\_NETIF
    :   Netif event

    <a id="_CPPv4N14event_module_t15EVENT_MOD_COUNTE"></a>

    <a id="_CPPv3N14event_module_t15EVENT_MOD_COUNTE"></a> <a id="_CPPv2N14event_module_t15EVENT_MOD_COUNTE"></a> <a id="group__bk__api__event__typedef_1gga8e1aa07a2a4e5fb9275943d957c3480da0dc252fb2939ee45848b52a880cbb3fb"></a> enumerator EVENT\_MOD\_COUNT
    :   Event module count
