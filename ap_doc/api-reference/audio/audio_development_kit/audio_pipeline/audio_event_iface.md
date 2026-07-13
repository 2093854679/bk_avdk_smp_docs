# Audio Event Interface


Audio Event Interface is used to handle audio event message.


## API Reference


### Header File


- [bk_audio/audio_pipeline/audio_event_iface.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_event_iface.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_event_iface.h")


### Functions

[audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") audio_event_iface_init([audio_event_iface_cfg_t](#_CPPv423audio_event_iface_cfg_t "audio_event_iface_cfg_t") *config)
:   Initialize audio event.

    参数
    :   **config** – The configurations

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_destroy([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Cleanup event, it doesn’t free evt pointer.

    参数
    :   **evt** – The event

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_set_listener([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener)
:   Add audio event `evt` to the listener, then we can listen `evt` event from `listen`

    参数
    :   - **listener** – The event can listen another event

        - **evt** – The event to be added to

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_remove_listener([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener, [audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Remove audio event `evt` from the listener.

    参数
    :   - **listener** – The event listener

        - **evt** – The event to be removed from

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_set_cmd_waiting_timeout([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, TickType_t wait_time)
:   Set current queue wait time for the event.

    参数
    :   - **evt** – The event

        - **wait_time** – **[in]** The wait time

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_waiting_cmd_msg([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Waiting internal queue message.

    参数
    :   **evt** – The event

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_cmd([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio_event_iface_msg_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") *msg)
:   Trigger an event for internal queue with a message.

    参数
    :   - **evt** – The event

        - **msg** – The message

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_cmd_from_isr([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio_event_iface_msg_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") *msg)
:   It’s same with `audio_event_iface_cmd`, but can send a message from ISR.

    参数
    :   - **evt** – **[in]** The event

        - **msg** – The message

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_sendout([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio_event_iface_msg_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") *msg)
:   Trigger and event out with a message.

    参数
    :   - **evt** – The event

        - **msg** – The message

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_discard([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Discard all ongoing event message.

    参数
    :   **evt** – The event

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_listen([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio_event_iface_msg_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") *msg, TickType_t wait_time)
:   Listening and invoke callback function if there are any event are comming.

    参数
    :   - **evt** – The event

        - **msg** – The message

        - **wait_time** – The wait time

    返回
    :   - BK_OK

        - BK_FAIL

QueueHandle_t audio_event_iface_get_queue_handle([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Get External queue handle of Emmitter.

    参数
    :   **evt** – **[in]** The external queue

    返回
    :   External QueueHandle_t

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_read([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio_event_iface_msg_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") *msg, TickType_t wait_time)
:   Read the event from all the registered event emitters in the queue set of the interface.

    参数
    :   - **evt** – **[in]** The event interface

        - **msg** – **[out]** The pointer to structure in which event is to be received

        - **wait_time** – **[in]** Timeout for receiving event

    返回
    :   - BK_OK On successful receiving of event

        - BK_FAIL In case of a timeout or invalid parameter passed

QueueHandle_t audio_event_iface_get_msg_queue_handle([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Get Internal queue handle of Emmitter.

    参数
    :   **evt** – **[in]** The Internal queue

    返回
    :   Internal QueueHandle_t

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_event_iface_set_msg_listener([audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio_event_iface_handle_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener)
:   Add audio internal event `evt` to the listener, then we can listen `evt` event from `listen`

    参数
    :   - **listener** – The event can listen another event

        - **evt** – The event to be added to

    返回
    :   - BK_OK

        - BK_FAIL


### Structures

struct audio_event_iface_msg_t
:   Event message

    Public Members

    int cmd
    :   Command id

    void *data
    :   Data pointer

    int data_len
    :   Data length

    void *source
    :   Source event

    bool need_free_data
    :   Need to free data pointer after the event has been processed

struct audio_event_iface_cfg_t
:   Event interface configurations

    Public Members

    int internal_queue_size
    :   It’s optional, Queue size for event `internal_queue`

    int external_queue_size
    :   It’s optional, Queue size for event `external_queue`

    int queue_set_size
    :   It’s optional, QueueSet size for event `queue_set`

    [on_event_iface_func](#_CPPv419on_event_iface_func "on_event_iface_func") on_cmd
    :   Function callback for listener when any event arrived

    void *context
    :   Context will pass to callback function

    TickType_t wait_time
    :   Timeout to check for event queue

    int type
    :   it will pass to [audio_event_iface_msg_t](#structaudio__event__iface__msg__t "#structaudio__event__iface__msg__t") source_type (To know where it came from)


### Macros

DEFAULT_AUDIO_EVENT_IFACE_SIZE

AUDIO_EVENT_IFACE_DEFAULT_CFG()


### Type Definitions

typedef [bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (*on_event_iface_func)([audio_event_iface_msg_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t")*, void*)

typedef struct audio_event_iface *audio_event_iface_handle_t
