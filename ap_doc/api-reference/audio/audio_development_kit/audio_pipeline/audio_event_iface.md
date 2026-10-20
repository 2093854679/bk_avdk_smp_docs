---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/audio_development_kit/audio_pipeline/audio_event_iface.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="audio-event-interface"></a>

# Audio Event Interface

Audio Event Interface is used to handle audio event message.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [audio\_event\_iface.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_audio/audio_pipeline/audio_event_iface.h)

<a id="functions"></a>

### Functions

<a id="_CPPv422audio_event_iface_initP23audio_event_iface_cfg_t"></a>

<a id="_CPPv322audio_event_iface_initP23audio_event_iface_cfg_t"></a> <a id="_CPPv222audio_event_iface_initP23audio_event_iface_cfg_t"></a> <a id="audio_event_iface_init__audio_event_iface_cfg_tP"></a> <a id="audio__event__iface_8h_1a204519041f15d3e59eaa3bd0717e04c3"></a> [audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") audio\_event\_iface\_init([audio\_event\_iface\_cfg\_t](#_CPPv423audio_event_iface_cfg_t "audio_event_iface_cfg_t") \*config)
:   Initialize audio event.

    参数
    :   **config** – The configurations

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv425audio_event_iface_destroy26audio_event_iface_handle_t"></a>

<a id="_CPPv325audio_event_iface_destroy26audio_event_iface_handle_t"></a> <a id="_CPPv225audio_event_iface_destroy26audio_event_iface_handle_t"></a> <a id="audio_event_iface_destroy__audio_event_iface_handle_t"></a> <a id="audio__event__iface_8h_1a5331439ed1201dfd1fde470b7d648256"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_destroy([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Cleanup event, it doesn’t free evt pointer.

    参数
    :   **evt** – The event

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv430audio_event_iface_set_listener26audio_event_iface_handle_t26audio_event_iface_handle_t"></a>

<a id="_CPPv330audio_event_iface_set_listener26audio_event_iface_handle_t26audio_event_iface_handle_t"></a> <a id="_CPPv230audio_event_iface_set_listener26audio_event_iface_handle_t26audio_event_iface_handle_t"></a> <a id="audio_event_iface_set_listener__audio_event_iface_handle_t.audio_event_iface_handle_t"></a> <a id="audio__event__iface_8h_1aae9cc3608ba4b76d270582d6b6a2d4c6"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_set\_listener([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener)
:   Add audio event `evt` to the listener, then we can listen `evt` event from `listen`

    参数
    :   - **listener** – The event can listen another event
        - **evt** – The event to be added to

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv433audio_event_iface_remove_listener26audio_event_iface_handle_t26audio_event_iface_handle_t"></a>

<a id="_CPPv333audio_event_iface_remove_listener26audio_event_iface_handle_t26audio_event_iface_handle_t"></a> <a id="_CPPv233audio_event_iface_remove_listener26audio_event_iface_handle_t26audio_event_iface_handle_t"></a> <a id="audio_event_iface_remove_listener__audio_event_iface_handle_t.audio_event_iface_handle_t"></a> <a id="audio__event__iface_8h_1a59621bead4ff364f9c77613daa2dddfd"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_remove\_listener([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener, [audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Remove audio event `evt` from the listener.

    参数
    :   - **listener** – The event listener
        - **evt** – The event to be removed from

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv441audio_event_iface_set_cmd_waiting_timeout26audio_event_iface_handle_t10TickType_t"></a>

<a id="_CPPv341audio_event_iface_set_cmd_waiting_timeout26audio_event_iface_handle_t10TickType_t"></a> <a id="_CPPv241audio_event_iface_set_cmd_waiting_timeout26audio_event_iface_handle_t10TickType_t"></a> <a id="audio_event_iface_set_cmd_waiting_timeout__audio_event_iface_handle_t.TickType_t"></a> <a id="audio__event__iface_8h_1a3ca03d7179fae49fd5fec322f34028bd"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_set\_cmd\_waiting\_timeout([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, TickType\_t wait\_time)
:   Set current queue wait time for the event.

    参数
    :   - **evt** – The event
        - **wait\_time** – **\[in\]** The wait time

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv433audio_event_iface_waiting_cmd_msg26audio_event_iface_handle_t"></a>

<a id="_CPPv333audio_event_iface_waiting_cmd_msg26audio_event_iface_handle_t"></a> <a id="_CPPv233audio_event_iface_waiting_cmd_msg26audio_event_iface_handle_t"></a> <a id="audio_event_iface_waiting_cmd_msg__audio_event_iface_handle_t"></a> <a id="audio__event__iface_8h_1a94d81dc067f5b48f1493f0f2a3ba9878"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_waiting\_cmd\_msg([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Waiting internal queue message.

    参数
    :   **evt** – The event

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv421audio_event_iface_cmd26audio_event_iface_handle_tP23audio_event_iface_msg_t"></a>

<a id="_CPPv321audio_event_iface_cmd26audio_event_iface_handle_tP23audio_event_iface_msg_t"></a> <a id="_CPPv221audio_event_iface_cmd26audio_event_iface_handle_tP23audio_event_iface_msg_t"></a> <a id="audio_event_iface_cmd__audio_event_iface_handle_t.audio_event_iface_msg_tP"></a> <a id="audio__event__iface_8h_1adca5dc9185138b9d3dbf2d19d253afa3"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_cmd([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio\_event\_iface\_msg\_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") \*msg)
:   Trigger an event for internal queue with a message.

    参数
    :   - **evt** – The event
        - **msg** – The message

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv430audio_event_iface_cmd_from_isr26audio_event_iface_handle_tP23audio_event_iface_msg_t"></a>

<a id="_CPPv330audio_event_iface_cmd_from_isr26audio_event_iface_handle_tP23audio_event_iface_msg_t"></a> <a id="_CPPv230audio_event_iface_cmd_from_isr26audio_event_iface_handle_tP23audio_event_iface_msg_t"></a> <a id="audio_event_iface_cmd_from_isr__audio_event_iface_handle_t.audio_event_iface_msg_tP"></a> <a id="audio__event__iface_8h_1a11ab2284aabee013449bc364c742e9ee"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_cmd\_from\_isr([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio\_event\_iface\_msg\_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") \*msg)
:   It’s same with `audio_event_iface_cmd`, but can send a message from ISR.

    参数
    :   - **evt** – **\[in\]** The event
        - **msg** – The message

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv425audio_event_iface_sendout26audio_event_iface_handle_tP23audio_event_iface_msg_t"></a>

<a id="_CPPv325audio_event_iface_sendout26audio_event_iface_handle_tP23audio_event_iface_msg_t"></a> <a id="_CPPv225audio_event_iface_sendout26audio_event_iface_handle_tP23audio_event_iface_msg_t"></a> <a id="audio_event_iface_sendout__audio_event_iface_handle_t.audio_event_iface_msg_tP"></a> <a id="audio__event__iface_8h_1a6f4aa3ad37a94b3e3fd31d9de6f057f3"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_sendout([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio\_event\_iface\_msg\_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") \*msg)
:   Trigger and event out with a message.

    参数
    :   - **evt** – The event
        - **msg** – The message

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv425audio_event_iface_discard26audio_event_iface_handle_t"></a>

<a id="_CPPv325audio_event_iface_discard26audio_event_iface_handle_t"></a> <a id="_CPPv225audio_event_iface_discard26audio_event_iface_handle_t"></a> <a id="audio_event_iface_discard__audio_event_iface_handle_t"></a> <a id="audio__event__iface_8h_1a0125995df984f58fd59e34bc9b5d61fa"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_discard([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Discard all ongoing event message.

    参数
    :   **evt** – The event

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv424audio_event_iface_listen26audio_event_iface_handle_tP23audio_event_iface_msg_t10TickType_t"></a>

<a id="_CPPv324audio_event_iface_listen26audio_event_iface_handle_tP23audio_event_iface_msg_t10TickType_t"></a> <a id="_CPPv224audio_event_iface_listen26audio_event_iface_handle_tP23audio_event_iface_msg_t10TickType_t"></a> <a id="audio_event_iface_listen__audio_event_iface_handle_t.audio_event_iface_msg_tP.TickType_t"></a> <a id="audio__event__iface_8h_1a7688ea86113af8822686cb7756b951a9"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_listen([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio\_event\_iface\_msg\_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") \*msg, TickType\_t wait\_time)
:   Listening and invoke callback function if there are any event are comming.

    参数
    :   - **evt** – The event
        - **msg** – The message
        - **wait\_time** – The wait time

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv434audio_event_iface_get_queue_handle26audio_event_iface_handle_t"></a>

<a id="_CPPv334audio_event_iface_get_queue_handle26audio_event_iface_handle_t"></a> <a id="_CPPv234audio_event_iface_get_queue_handle26audio_event_iface_handle_t"></a> <a id="audio_event_iface_get_queue_handle__audio_event_iface_handle_t"></a> <a id="audio__event__iface_8h_1ae326709c2573aab90fd3df8e96f78626"></a> QueueHandle\_t audio\_event\_iface\_get\_queue\_handle([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Get External queue handle of Emmitter.

    参数
    :   **evt** – **\[in\]** The external queue

    返回
    :   External QueueHandle\_t

<a id="_CPPv422audio_event_iface_read26audio_event_iface_handle_tP23audio_event_iface_msg_t10TickType_t"></a>

<a id="_CPPv322audio_event_iface_read26audio_event_iface_handle_tP23audio_event_iface_msg_t10TickType_t"></a> <a id="_CPPv222audio_event_iface_read26audio_event_iface_handle_tP23audio_event_iface_msg_t10TickType_t"></a> <a id="audio_event_iface_read__audio_event_iface_handle_t.audio_event_iface_msg_tP.TickType_t"></a> <a id="audio__event__iface_8h_1aa6f9c048acd8bd721e3be7ced8647213"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_read([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio\_event\_iface\_msg\_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") \*msg, TickType\_t wait\_time)
:   Read the event from all the registered event emitters in the queue set of the interface.

    参数
    :   - **evt** – **\[in\]** The event interface
        - **msg** – **\[out\]** The pointer to structure in which event is to be received
        - **wait\_time** – **\[in\]** Timeout for receiving event

    返回
    :   - BK\_OK On successful receiving of event
        - BK\_FAIL In case of a timeout or invalid parameter passed

<a id="_CPPv438audio_event_iface_get_msg_queue_handle26audio_event_iface_handle_t"></a>

<a id="_CPPv338audio_event_iface_get_msg_queue_handle26audio_event_iface_handle_t"></a> <a id="_CPPv238audio_event_iface_get_msg_queue_handle26audio_event_iface_handle_t"></a> <a id="audio_event_iface_get_msg_queue_handle__audio_event_iface_handle_t"></a> <a id="audio__event__iface_8h_1a8e449a80d2cfcb7eae7dbb35bb351288"></a> QueueHandle\_t audio\_event\_iface\_get\_msg\_queue\_handle([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Get Internal queue handle of Emmitter.

    参数
    :   **evt** – **\[in\]** The Internal queue

    返回
    :   Internal QueueHandle\_t

<a id="_CPPv434audio_event_iface_set_msg_listener26audio_event_iface_handle_t26audio_event_iface_handle_t"></a>

<a id="_CPPv334audio_event_iface_set_msg_listener26audio_event_iface_handle_t26audio_event_iface_handle_t"></a> <a id="_CPPv234audio_event_iface_set_msg_listener26audio_event_iface_handle_t26audio_event_iface_handle_t"></a> <a id="audio_event_iface_set_msg_listener__audio_event_iface_handle_t.audio_event_iface_handle_t"></a> <a id="audio__event__iface_8h_1a23c8ea91abedf0cca6b9800e8c5cf56a"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_event\_iface\_set\_msg\_listener([audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt, [audio\_event\_iface\_handle\_t](#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener)
:   Add audio internal event `evt` to the listener, then we can listen `evt` event from `listen`

    参数
    :   - **listener** – The event can listen another event
        - **evt** – The event to be added to

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="structures"></a>

### Structures

<a id="_CPPv423audio_event_iface_msg_t"></a>

<a id="_CPPv323audio_event_iface_msg_t"></a> <a id="_CPPv223audio_event_iface_msg_t"></a> <a id="audio_event_iface_msg_t"></a> <a id="structaudio__event__iface__msg__t"></a> struct audio\_event\_iface\_msg\_t
:   Event message

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23audio_event_iface_msg_t3cmdE"></a>

    <a id="_CPPv3N23audio_event_iface_msg_t3cmdE"></a> <a id="_CPPv2N23audio_event_iface_msg_t3cmdE"></a> <a id="audio_event_iface_msg_t::cmd__i"></a> <a id="structaudio__event__iface__msg__t_1a0523ae66028673b400f5bac491bf80c3"></a> int cmd
    :   Command id

    <a id="_CPPv4N23audio_event_iface_msg_t4dataE"></a>

    <a id="_CPPv3N23audio_event_iface_msg_t4dataE"></a> <a id="_CPPv2N23audio_event_iface_msg_t4dataE"></a> <a id="audio_event_iface_msg_t::data__voidP"></a> <a id="structaudio__event__iface__msg__t_1ab8ca9b2d7ff49a623191f5a1b5964e0f"></a> void \*data
    :   Data pointer

    <a id="_CPPv4N23audio_event_iface_msg_t8data_lenE"></a>

    <a id="_CPPv3N23audio_event_iface_msg_t8data_lenE"></a> <a id="_CPPv2N23audio_event_iface_msg_t8data_lenE"></a> <a id="audio_event_iface_msg_t::data_len__i"></a> <a id="structaudio__event__iface__msg__t_1af46a8049925453478825a39db62b1616"></a> int data\_len
    :   Data length

    <a id="_CPPv4N23audio_event_iface_msg_t6sourceE"></a>

    <a id="_CPPv3N23audio_event_iface_msg_t6sourceE"></a> <a id="_CPPv2N23audio_event_iface_msg_t6sourceE"></a> <a id="audio_event_iface_msg_t::source__voidP"></a> <a id="structaudio__event__iface__msg__t_1ae7df003a7a88e188909533b735bfc9d7"></a> void \*source
    :   Source event

    <a id="_CPPv4N23audio_event_iface_msg_t14need_free_dataE"></a>

    <a id="_CPPv3N23audio_event_iface_msg_t14need_free_dataE"></a> <a id="_CPPv2N23audio_event_iface_msg_t14need_free_dataE"></a> <a id="audio_event_iface_msg_t::need_free_data__b"></a> <a id="structaudio__event__iface__msg__t_1ac0ebce6aa06cb5987903d84b411ffba5"></a> bool need\_free\_data
    :   Need to free data pointer after the event has been processed

<a id="_CPPv423audio_event_iface_cfg_t"></a>

<a id="_CPPv323audio_event_iface_cfg_t"></a> <a id="_CPPv223audio_event_iface_cfg_t"></a> <a id="audio_event_iface_cfg_t"></a> <a id="structaudio__event__iface__cfg__t"></a> struct audio\_event\_iface\_cfg\_t
:   Event interface configurations

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23audio_event_iface_cfg_t19internal_queue_sizeE"></a>

    <a id="_CPPv3N23audio_event_iface_cfg_t19internal_queue_sizeE"></a> <a id="_CPPv2N23audio_event_iface_cfg_t19internal_queue_sizeE"></a> <a id="audio_event_iface_cfg_t::internal_queue_size__i"></a> <a id="structaudio__event__iface__cfg__t_1abd2144b15c964b6036efceadcdf84b21"></a> int internal\_queue\_size
    :   It’s optional, Queue size for event `internal_queue`

    <a id="_CPPv4N23audio_event_iface_cfg_t19external_queue_sizeE"></a>

    <a id="_CPPv3N23audio_event_iface_cfg_t19external_queue_sizeE"></a> <a id="_CPPv2N23audio_event_iface_cfg_t19external_queue_sizeE"></a> <a id="audio_event_iface_cfg_t::external_queue_size__i"></a> <a id="structaudio__event__iface__cfg__t_1a50623ecf764045f0ce31aba9e4bda61f"></a> int external\_queue\_size
    :   It’s optional, Queue size for event `external_queue`

    <a id="_CPPv4N23audio_event_iface_cfg_t14queue_set_sizeE"></a>

    <a id="_CPPv3N23audio_event_iface_cfg_t14queue_set_sizeE"></a> <a id="_CPPv2N23audio_event_iface_cfg_t14queue_set_sizeE"></a> <a id="audio_event_iface_cfg_t::queue_set_size__i"></a> <a id="structaudio__event__iface__cfg__t_1a5a9c62a141fbd18db51256af961890d1"></a> int queue\_set\_size
    :   It’s optional, QueueSet size for event `queue_set`

    <a id="_CPPv4N23audio_event_iface_cfg_t6on_cmdE"></a>

    <a id="_CPPv3N23audio_event_iface_cfg_t6on_cmdE"></a> <a id="_CPPv2N23audio_event_iface_cfg_t6on_cmdE"></a> <a id="audio_event_iface_cfg_t::on_cmd__on_event_iface_func"></a> <a id="structaudio__event__iface__cfg__t_1a62bded4b59e902e7b909eb0f0e0ea013"></a> [on\_event\_iface\_func](#_CPPv419on_event_iface_func "on_event_iface_func") on\_cmd
    :   Function callback for listener when any event arrived

    <a id="_CPPv4N23audio_event_iface_cfg_t7contextE"></a>

    <a id="_CPPv3N23audio_event_iface_cfg_t7contextE"></a> <a id="_CPPv2N23audio_event_iface_cfg_t7contextE"></a> <a id="audio_event_iface_cfg_t::context__voidP"></a> <a id="structaudio__event__iface__cfg__t_1a3dbeaed964357ca0bd33fa8061dca515"></a> void \*context
    :   Context will pass to callback function

    <a id="_CPPv4N23audio_event_iface_cfg_t9wait_timeE"></a>

    <a id="_CPPv3N23audio_event_iface_cfg_t9wait_timeE"></a> <a id="_CPPv2N23audio_event_iface_cfg_t9wait_timeE"></a> <a id="audio_event_iface_cfg_t::wait_time__TickType_t"></a> <a id="structaudio__event__iface__cfg__t_1a3ef2c11d763a24e2bd4c7f3b08a68665"></a> TickType\_t wait\_time
    :   Timeout to check for event queue

    <a id="_CPPv4N23audio_event_iface_cfg_t4typeE"></a>

    <a id="_CPPv3N23audio_event_iface_cfg_t4typeE"></a> <a id="_CPPv2N23audio_event_iface_cfg_t4typeE"></a> <a id="audio_event_iface_cfg_t::type__i"></a> <a id="structaudio__event__iface__cfg__t_1a984d496c2ed3b6b0ede9cf8d21315f9e"></a> int type
    :   it will pass to [audio\_event\_iface\_msg\_t](#structaudio__event__iface__msg__t) source\_type (To know where it came from)

<a id="macros"></a>

### Macros

<a id="c.DEFAULT_AUDIO_EVENT_IFACE_SIZE"></a>

<a id="audio__event__iface_8h_1af3d925ed76eabdf59767746954505402"></a> DEFAULT\_AUDIO\_EVENT\_IFACE\_SIZE

<a id="c.AUDIO_EVENT_IFACE_DEFAULT_CFG"></a>

<a id="audio__event__iface_8h_1a5f5f92dd3caffe1fff396475f30d43ef"></a> AUDIO\_EVENT\_IFACE\_DEFAULT\_CFG()

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv419on_event_iface_func"></a>

<a id="_CPPv319on_event_iface_func"></a> <a id="_CPPv219on_event_iface_func"></a> <a id="on_event_iface_func"></a> <a id="audio__event__iface_8h_1a6be21d17572cea0f9e558f4d937a014d"></a> typedef [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*on\_event\_iface\_func)([audio\_event\_iface\_msg\_t](#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t")\*, void\*)

<a id="_CPPv426audio_event_iface_handle_t"></a>

<a id="_CPPv326audio_event_iface_handle_t"></a> <a id="_CPPv226audio_event_iface_handle_t"></a> <a id="audio_event_iface_handle_t"></a> <a id="audio__event__iface_8h_1a9b289023c46eadafb660a7ffa4c34b14"></a> typedef struct audio\_event\_iface \*audio\_event\_iface\_handle\_t
