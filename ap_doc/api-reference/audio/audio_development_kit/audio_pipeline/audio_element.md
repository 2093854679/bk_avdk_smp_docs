# Audio Element


Audio Element is used to set and control the behavior of audio functional elements.


## API Reference


### Header File


- [bk_audio/audio_pipeline/audio_element.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_element.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_element.h")


### Functions

[audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") audio_element_init([audio_element_cfg_t](#_CPPv419audio_element_cfg_t "audio_element_cfg_t") *config)
:   Initialize audio element with config.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   - audio_elemenent handle object

        - NULL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_deinit([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Destroy audio element handle object, stop, clear, deletel all.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_setdata([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, void *data)
:   Set context data to element handle object. It can be retrieved by calling `audio_element_getdata`.

    参数
    :   - **el** – **[in]** The audio element handle

        - **data** – **[in]** The data pointer

    返回
    :   - BK_OK

        - BK_FAIL

void *audio_element_getdata([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get context data from element handle object.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   data pointer

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_tag([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, const char *tag)
:   Set elemenet tag name, or clear if tag = NULL.

    参数
    :   - **el** – **[in]** The audio element handle

        - **tag** – **[in]** The tag name pointer

    返回
    :   - BK_OK

        - BK_FAIL

char *audio_element_get_tag([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get element tag name.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   Element tag name pointer

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_setinfo([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_element_info_t](#_CPPv420audio_element_info_t "audio_element_info_t") *info)
:   Set audio element infomation.

    参数
    :   - **el** – **[in]** The audio element handle

        - **info** – **[in]** The information pointer

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_getinfo([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_element_info_t](#_CPPv420audio_element_info_t "audio_element_info_t") *info)
:   Get audio element infomation.

    参数
    :   - **el** – **[in]** The audio element handle

        - **info** – **[inout]** The information pointer

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_uri([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, const char *uri)
:   Set audio element URI.

    参数
    :   - **el** – **[in]** The audio element handle

        - **uri** – **[in]** The uri pointer

    返回
    :   - BK_OK

        - BK_FAIL

char *audio_element_get_uri([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get audio element URI.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   URI pointer

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_run([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Start Audio Element. With this function, audio_element will start as freeRTOS task, and put the task into ‘PAUSED’ state. Note: Element does not actually start when this function returns.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_terminate([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Terminate Audio Element. With this function, audio_element will exit the task function. Note: this API only sends request. It does not actually terminate immediately when this function returns.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_terminate_with_ticks([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, TickType_t ticks_to_wait)
:   Terminate Audio Element with specific ticks for timeout. With this function, audio_element will exit the task function. Note: this API only sends request. It does not actually terminate immediately when this function returns.

    参数
    :   - **el** – **[in]** The audio element handle

        - **ticks_to_wait** – **[in]** The maximum amount of time to blocking

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_stop([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Request stop of the Audio Element. After receiving the stop request, the element will ignore the actions being performed (read/write, wait for the ringbuffer …) and close the task, reset the state variables. Note: this API only sends requests, Element does not actually stop when this function returns.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_wait_for_stop([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   After the `audio_element_stop` function is called, the Element task will perform some abort procedures. This function will be blocked (Time is DEFAULT_MAX_WAIT_TIME) until Element Task has done and exit.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK, Success

        - BK_FAIL, The state is not AEL_STATE_RUNNING

        - BK_ERR_ADK_TIMEOUT, Timeout

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_wait_for_stop_ms([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, TickType_t ticks_to_wait)
:   After the `audio_element_stop` function is called, the Element task will perform some abort procedures. The maximum amount of time should block waiting for Element task has stopped.

    参数
    :   - **el** – **[in]** The audio element handle

        - **ticks_to_wait** – **[in]** The maximum amount of time to wait for stop

    返回
    :   - BK_OK, Success

        - BK_FAIL, The state is not AEL_STATE_RUNNING

        - BK_ERR_ADK_TIMEOUT, Timeout

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_pause([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Request audio Element enter ‘PAUSE’ state. In this state, the task will wait for any event.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_resume([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, float wait_for_rb_threshold, TickType_t timeout)
:   Request audio Element enter ‘RUNNING’ state. In this state, the task listens to events and invokes the callback functions. At the same time it will wait until the size/total_size of the output ringbuffer is greater than or equal to `wait_for_rb_threshold`. If the timeout period has been exceeded and ringbuffer output has not yet reached `wait_for_rb_threshold` then the function will return.

    参数
    :   - **el** – **[in]** The audio element handle

        - **wait_for_rb_threshold** – **[in]** The wait for rb threshold (0 .. 1)

        - **timeout** – **[in]** The timeout

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_msg_set_listener([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_event_iface_handle_t](audio_event_iface.md#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener)
:   This function will add a `listener` to listen to all events from audio element `el`. Any event from el->external_event will be send to the `listener`.

    参数
    :   - **el** – **[in]** The audio element handle

        - **listener** – **[in]** The event will be listen to

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_event_callback([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [event_cb_func](#_CPPv413event_cb_func "event_cb_func") cb_func, void *ctx)
:   This function will add a `callback` to be called from audio element `el`. Any event to caller will cause to call callback function.

    参数
    :   - **el** – **[in]** The audio element handle

        - **cb_func** – **[in]** The callback function

        - **ctx** – **[in]** Caller context

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_msg_remove_listener([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_event_iface_handle_t](audio_event_iface.md#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener)
:   Remove listener out of el. No new events will be sent to the listener.

    参数
    :   - **el** – **[in]** The audio element handle

        - **listener** – **[in]** The listener

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_input_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_port_handle_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") port)
:   Set Element input ringbuffer.

    参数
    :   - **el** – **[in]** The audio element handle

        - **port** – **[in]** The audio port handle

    返回
    :   - BK_OK

        - BK_FAIL

[audio_port_handle_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") audio_element_get_input_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get Element input audio port.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   audio_port_handle_t

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_output_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_port_handle_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") port)
:   Set Element output ringbuffer.

    参数
    :   - **el** – **[in]** The audio element handle

        - **port** – **[in]** The audio port handle

    返回
    :   - BK_OK

        - BK_FAIL

[audio_port_handle_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") audio_element_get_output_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get Element output audio port.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   audio_port_handle_t

[audio_element_state_t](#_CPPv421audio_element_state_t "audio_element_state_t") audio_element_get_state([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get current Element state.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   audio_element_state_t

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_abort_input_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   If the element is requesting data from the input audio port, this function forces it to abort.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_abort_output_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   If the element is waiting to write data to the output audio port, this function forces it to abort.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_wait_for_buffer([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int size_expect, TickType_t timeout)
:   This function will wait until the sizeof the output ringbuffer is greater than or equal to `size_expect`. If the timeout period has been exceeded and ringbuffer output has not yet reached `size_expect` then the function will return `BK_FAIL`

    参数
    :   - **el** – **[in]** The audio element handle

        - **size_expect** – **[in]** The size expect

        - **timeout** – **[in]** The timeout

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_report_status([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_element_status_t](#_CPPv422audio_element_status_t "audio_element_status_t") status)
:   Element will sendout event (status) to event by this function.

    参数
    :   - **el** – **[in]** The audio element handle

        - **status** – **[in]** The status

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_report_info([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Element will sendout event (information) to event by this function.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_report_codec_fmt([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Element will sendout event (codec format) to event by this function.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_report_pos([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Element will sendout event with a duplicate information by this function.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

        - BK_ERR_ADK_NO_MEM

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_input_timeout([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, TickType_t timeout)
:   Set input read timeout (default is `portMAX_DELAY`).

    参数
    :   - **el** – **[in]** The audio element handle

        - **timeout** – **[in]** The timeout

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_output_timeout([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, TickType_t timeout)
:   Set output read timeout (default is `portMAX_DELAY`).

    参数
    :   - **el** – **[in]** The audio element handle

        - **timeout** – **[in]** The timeout

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_reset_input_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Reset input port.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_reset_output_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Reset output port.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

int audio_element_input([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, char *buffer, int wanted_size)
:   Call this function to provide Element input data. Depending on setup using ringbuffer or function callback, Element invokes read ringbuffer, or calls read callback funtion.

    参数
    :   - **el** – **[in]** The audio element handle

        - **buffer** – **[in]** The buffer pointer

        - **wanted_size** – **[in]** The wanted size

    返回
    :   - > 0 number of bytes produced

        - <=0 audio_element_err_t

int audio_element_output([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, char *buffer, int write_size)
:   Call this function to sendout Element output data. Depending on setup using ringbuffer or function callback, Element will invoke write to ringbuffer, or call write callback funtion.

    参数
    :   - **el** – **[in]** The audio element handle

        - **buffer** – **[in]** The buffer pointer

        - **write_size** – **[in]** The write size

    返回
    :   - > 0 number of bytes written

        - <=0 audio_element_err_t

QueueHandle_t audio_element_get_event_queue([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get External queue of Emitter. We can read any event that has been send out of Element from this `QueueHandle_t`.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   QueueHandle_t

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_port_done([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Set input port and output port have finished.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_reset_state([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Enforce ‘AEL_STATE_INIT’ state.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

int audio_element_get_output_ringbuf_size([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get Element output ringbuffer size.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - =0: Parameter NULL

        - >0: Size of ringbuffer

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_output_ringbuf_size([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int rb_size)
:   Set Element output ringbuffer size.

    参数
    :   - **el** – **[in]** The audio element handle

        - **rb_size** – **[in]** Size of the ringbuffer

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_get_output_framebuf_size([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int *node_size, int *node_num)
:   Get Element output port framebuffer size.

    参数
    :   - **el** – **[in]** The audio element handle

        - **node_size** – **[in]** Size of the framebuffer node

        - **node_num** – **[in]** Numbers of the framebuffer node

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_output_framebuf_size([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int node_size, int node_num)
:   Set Element output port framebuffer size.

    参数
    :   - **el** – **[in]** The audio element handle

        - **node_size** – **[in]** Size of the framebuffer node

        - **node_num** – **[in]** Numbers of the framebuffer node

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_multi_input([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, char *buffer, int wanted_size, int index, TickType_t ticks_to_wait)
:   Call this function to read data from multi input ringbuffer by given index.

    参数
    :   - **el** – **[in]** The audio element handle

        - **buffer** – **[inout]** The buffer pointer

        - **wanted_size** – **[in]** The wanted size

        - **index** – **[in]** The index of multi input ringbuffer, start from `0`, should be less than `NUMBER_OF_MULTI_RINGBUF`

        - **ticks_to_wait** – **[in]** Timeout of ringbuffer

    返回
    :   - >= 0: Size of input

        - < 0: Error

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_multi_output([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, char *buffer, int wanted_size, TickType_t ticks_to_wait)
:   Call this function write data by multi output ringbuffer.

    参数
    :   - **el** – **[in]** The audio element handle

        - **buffer** – **[in]** The buffer pointer

        - **wanted_size** – **[in]** The wanted size

        - **ticks_to_wait** – **[in]** Timeout of ringbuffer

    返回
    :   - >= 0: Size of output

        - < 0: Error

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_multi_input_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_port_handle_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") port, int index)
:   Set multi input port Element.

    参数
    :   - **el** – **[in]** The audio element handle

        - **port** – **[in]** The audio port handle

        - **index** – **[in]** Index of multi port, starts from `0`, should be less than `NUMBER_OF_MULTI_PORT`

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_multi_output_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_port_handle_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") port, int index)
:   Set multi output ringbuffer Element.

    参数
    :   - **el** – **[in]** The audio element handle

        - **port** – **[in]** The audio port handle

        - **index** – **[in]** Index of multi ringbuffer, starts from `0`, should be less than `NUMBER_OF_MULTI_PORT`

    返回
    :   - BK_OK

        - BK_ERR_ADK_INVALID_ARG

[audio_port_handle_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") audio_element_get_multi_input_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int index)
:   Get handle of multi input audio port Element by index.

    参数
    :   - **el** – **[in]** The audio element handle

        - **index** – **[in]** Index of multi audio port, starts from `0`, should be less than `NUMBER_OF_MULTI_PORT`

    返回
    :   - NULL Error

        - Others audio_port_handle_t

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_get_multi_input_max_port_num([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get max port number of multi input audio port Element.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - >= 0: Max port number of multi input audio port Element

        - < 0: Error

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_get_multi_output_max_port_num([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get max port number of multi output audio port Element.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - >= 0: Max port number of multi output audio port Element

        - < 0: Error

[audio_port_handle_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") audio_element_get_multi_output_port([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int index)
:   Get handle of multi output audio port Element by index.

    参数
    :   - **el** – **[in]** The audio element handle

        - **index** – **[in]** Index of multi audio port, starts from `0`, should be less than `NUMBER_OF_MULTI_PORT`

    返回
    :   - NULL Error

        - Others audio_port_handle_t

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_process_init([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Provides a way to call element’s `open`

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_process_deinit([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Provides a way to call element’s `close`

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_seek([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, void *in_data, int in_size, void *out_data, int *out_size)
:   Call element’s `seek`

    参数
    :   - **el** – **[in]** The audio element handle

        - **in_data** – **[in]** A pointer to in data

        - **in_size** – **[in]** The size of the `in_data`

        - **out_data** – **[out]** A pointer to the out data

        - **out_size** – **[out]** The size of the `out_data`

    返回
    :   - BK_OK

        - BK_FAIL

        - BK_ERR_ADK_NOT_SUPPORT

bool audio_element_is_stopping([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get Element stopping flag.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   element’s stopping flag

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_update_byte_pos([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int pos)
:   Update the byte position of element information.

    参数
    :   - **el** – **[in]** The audio element handle

        - **pos** – **[in]** The byte_pos accumulated by this value

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_byte_pos([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int pos)
:   Set the byte position of element information.

    参数
    :   - **el** – **[in]** The audio element handle

        - **pos** – **[in]** This value is assigned to byte_pos

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_update_total_bytes([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int total_bytes)
:   Update the total bytes of element information.

    参数
    :   - **el** – **[in]** The audio element handle

        - **total_bytes** – **[in]** The total_bytes accumulated by this value

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_total_bytes([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int total_bytes)
:   Set the total bytes of element information.

    参数
    :   - **el** – **[in]** The audio element handle

        - **total_bytes** – **[in]** This value is assigned to total_bytes

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_bps([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int bit_rate)
:   Set the bps of element information.

    参数
    :   - **el** – **[in]** The audio element handle

        - **bit_rate** – **[in]** This value is assigned to bps

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_codec_fmt([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int format)
:   Set the codec format of element information.

    参数
    :   - **el** – **[in]** The audio element handle

        - **format** – **[in]** This value is assigned to codec_fmt

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_music_info([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int sample_rates, int channels, int bits)
:   Set the sample_rate, channels, bits of element information.

    参数
    :   - **el** – **[in]** The audio element handle

        - **sample_rates** – **[in]** Sample_rates of music information

        - **channels** – **[in]** Channels of music information

        - **bits** – **[in]** Bits of music information

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_duration([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int duration)
:   Set the duration of element information.

    参数
    :   - **el** – **[in]** The audio element handle

        - **duration** – **[in]** This value is assigned to duration

    返回
    :   - BK_OK

        - BK_FAIL

[port_type_t](audio_port.md#_CPPv411port_type_t "port_type_t") audio_element_get_output_port_type([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get the type of element output port.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - 0 Error

        - Others port_type_t

[port_type_t](audio_port.md#_CPPv411port_type_t "port_type_t") audio_element_get_input_port_type([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get the type of element input port.

    参数
    :   **el** – **[in]** The audio element handle

    返回
    :   - 0 Error

        - Others port_type_t

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_output_port_type([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [port_type_t](audio_port.md#_CPPv411port_type_t "port_type_t") type)
:   Set the type of element output port.

    参数
    :   - **el** – **[in]** The audio element handle

        - **type** – **[in]** The audio port type

    返回
    :   - BK_OK

        - BK_FAIL

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_element_set_input_port_type([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [port_type_t](audio_port.md#_CPPv411port_type_t "port_type_t") type)
:   Set the type of element input port.

    参数
    :   - **el** – **[in]** The audio element handle

        - **type** – **[in]** The audio port type

    返回
    :   - BK_OK

        - BK_FAIL


### Structures

struct audio_element_info_t
:   Audio Element informations.

struct audio_element_cfg_t
:   Audio Element configurations. Each Element at startup will be a self-running task. These tasks will execute the callback open -> [loop: read -> process -> write] -> close. These callback functions are provided by the user corresponding to this configuration.


### Macros

AUDIO_ELEMENT_INFO_DEFAULT()

DEFAULT_ELEMENT_FRAMEBUF_SIZE

DEFAULT_ELEMENT_FRAMEBUF_NUM

DEFAULT_ELEMENT_RINGBUF_SIZE

DEFAULT_ELEMENT_BUFFER_LENGTH

DEFAULT_ELEMENT_STACK_SIZE

DEFAULT_ELEMENT_TASK_PRIO

DEFAULT_ELEMENT_TASK_CORE

DEFAULT_AUDIO_ELEMENT_CONFIG()


### Type Definitions

typedef struct audio_element *audio_element_handle_t

typedef [bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (*el_io_func)([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") self)

typedef int (*process_func)([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") self, char *el_buffer, int el_buf_len)

typedef [bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (*event_cb_func)([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio_event_iface_msg_t](audio_event_iface.md#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") *event, void *ctx)

typedef [bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (*ctrl_func)([audio_element_handle_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") self, void *in_data, int in_size, void *out_data, int *out_size)


### Enumerations

enum audio_element_err_t
:   *Values:*

    enumerator AEL_IO_OK

    enumerator AEL_IO_FAIL

    enumerator AEL_IO_DONE

    enumerator AEL_IO_ABORT

    enumerator AEL_IO_TIMEOUT

    enumerator AEL_PROCESS_FAIL

enum audio_element_state_t
:   Audio element state.


    *Values:*

    enumerator AEL_STATE_NONE

    enumerator AEL_STATE_INIT

    enumerator AEL_STATE_INITIALIZING

    enumerator AEL_STATE_RUNNING

    enumerator AEL_STATE_PAUSED

    enumerator AEL_STATE_STOPPED

    enumerator AEL_STATE_FINISHED

    enumerator AEL_STATE_ERROR

enum audio_element_msg_cmd_t
:   Audio element action command, process on dispatcher


    *Values:*

    enumerator AEL_MSG_CMD_NONE

    enumerator AEL_MSG_CMD_FINISH

    enumerator AEL_MSG_CMD_STOP

    enumerator AEL_MSG_CMD_PAUSE

    enumerator AEL_MSG_CMD_RESUME

    enumerator AEL_MSG_CMD_DESTROY

    enumerator AEL_MSG_CMD_REPORT_STATUS

    enumerator AEL_MSG_CMD_REPORT_MUSIC_INFO

    enumerator AEL_MSG_CMD_REPORT_CODEC_FMT

    enumerator AEL_MSG_CMD_REPORT_POSITION

enum audio_element_status_t
:   Audio element status report


    *Values:*

    enumerator AEL_STATUS_NONE

    enumerator AEL_STATUS_ERROR_OPEN

    enumerator AEL_STATUS_ERROR_INPUT

    enumerator AEL_STATUS_ERROR_PROCESS

    enumerator AEL_STATUS_ERROR_OUTPUT

    enumerator AEL_STATUS_ERROR_CLOSE

    enumerator AEL_STATUS_ERROR_TIMEOUT

    enumerator AEL_STATUS_ERROR_UNKNOWN

    enumerator AEL_STATUS_INPUT_DONE

    enumerator AEL_STATUS_INPUT_BUFFERING

    enumerator AEL_STATUS_OUTPUT_DONE

    enumerator AEL_STATUS_OUTPUT_BUFFERING

    enumerator AEL_STATUS_STATE_RUNNING

    enumerator AEL_STATUS_STATE_PAUSED

    enumerator AEL_STATUS_STATE_STOPPED

    enumerator AEL_STATUS_STATE_FINISHED

    enumerator AEL_STATUS_MOUNTED

    enumerator AEL_STATUS_UNMOUNTED
