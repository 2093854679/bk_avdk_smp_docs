---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/audio_development_kit/audio_pipeline/audio_element.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="audio-element"></a>

# Audio Element

Audio Element is used to set and control the behavior of audio functional elements.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [audio\_element.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_audio/audio_pipeline/audio_element.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418audio_element_initP19audio_element_cfg_t"></a>

<a id="_CPPv318audio_element_initP19audio_element_cfg_t"></a> <a id="_CPPv218audio_element_initP19audio_element_cfg_t"></a> <a id="audio_element_init__audio_element_cfg_tP"></a> <a id="audio__element_8h_1a4d35b5d7fda2ea71a0612ebf462903cd"></a> [audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") audio\_element\_init([audio\_element\_cfg\_t](#_CPPv419audio_element_cfg_t "audio_element_cfg_t") \*config)
:   Initialize audio element with config.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   - audio\_elemenent handle object
        - NULL

<a id="_CPPv420audio_element_deinit22audio_element_handle_t"></a>

<a id="_CPPv320audio_element_deinit22audio_element_handle_t"></a> <a id="_CPPv220audio_element_deinit22audio_element_handle_t"></a> <a id="audio_element_deinit__audio_element_handle_t"></a> <a id="audio__element_8h_1aa67f7e14e8153382510fc61110b8706f"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_deinit([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Destroy audio element handle object, stop, clear, deletel all.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv421audio_element_setdata22audio_element_handle_tPv"></a>

<a id="_CPPv321audio_element_setdata22audio_element_handle_tPv"></a> <a id="_CPPv221audio_element_setdata22audio_element_handle_tPv"></a> <a id="audio_element_setdata__audio_element_handle_t.voidP"></a> <a id="audio__element_8h_1afb94b67db363a1cd87aa464d8189edb4"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_setdata([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, void \*data)
:   Set context data to element handle object. It can be retrieved by calling `audio_element_getdata`.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **data** – **\[in\]** The data pointer

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv421audio_element_getdata22audio_element_handle_t"></a>

<a id="_CPPv321audio_element_getdata22audio_element_handle_t"></a> <a id="_CPPv221audio_element_getdata22audio_element_handle_t"></a> <a id="audio_element_getdata__audio_element_handle_t"></a> <a id="audio__element_8h_1a0f8de39fd5edc5f64c3e59241d341340"></a> void \*audio\_element\_getdata([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get context data from element handle object.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   data pointer

<a id="_CPPv421audio_element_set_tag22audio_element_handle_tPKc"></a>

<a id="_CPPv321audio_element_set_tag22audio_element_handle_tPKc"></a> <a id="_CPPv221audio_element_set_tag22audio_element_handle_tPKc"></a> <a id="audio_element_set_tag__audio_element_handle_t.cCP"></a> <a id="audio__element_8h_1ac90530e20bdbe1b9dd490dc4ff88aec3"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_tag([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, const char \*tag)
:   Set elemenet tag name, or clear if tag \= NULL.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **tag** – **\[in\]** The tag name pointer

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv421audio_element_get_tag22audio_element_handle_t"></a>

<a id="_CPPv321audio_element_get_tag22audio_element_handle_t"></a> <a id="_CPPv221audio_element_get_tag22audio_element_handle_t"></a> <a id="audio_element_get_tag__audio_element_handle_t"></a> <a id="audio__element_8h_1aea4a7bfbd7a9a1e5ddf9547c5e909669"></a> char \*audio\_element\_get\_tag([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get element tag name.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   Element tag name pointer

<a id="_CPPv423audio_element_obs_begin22audio_element_handle_t"></a>

<a id="_CPPv323audio_element_obs_begin22audio_element_handle_t"></a> <a id="_CPPv223audio_element_obs_begin22audio_element_handle_t"></a> <a id="audio_element_obs_begin__audio_element_handle_t"></a> <a id="audio__element_8h_1a51d6af18e5912667375333c203901993"></a> void audio\_element\_obs\_begin([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Start process-cost observation for the current element.

    ```
            The caller should place this after blocking input/wait operations
            and before the non-blocking component work to keep timing
            comparable across elements.
    ```

    参数
    :   **el** – **\[in\]** The audio element handle

<a id="_CPPv421audio_element_obs_end22audio_element_handle_ti8uint32_t"></a>

<a id="_CPPv321audio_element_obs_end22audio_element_handle_ti8uint32_t"></a> <a id="_CPPv221audio_element_obs_end22audio_element_handle_ti8uint32_t"></a> <a id="audio_element_obs_end__audio_element_handle_t.i.uint32_t"></a> <a id="audio__element_8h_1ae70398d1d4f213ad3af0d634a41d132c"></a> void audio\_element\_obs\_end([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int ret, uint32\_t frame\_size)
:   Finish process-cost observation for the current element.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **ret** – **\[in\]** The element process return value or input size
        - **frame\_size** – **\[in\]** The expected frame size

<a id="_CPPv421audio_element_setinfo22audio_element_handle_tP20audio_element_info_t"></a>

<a id="_CPPv321audio_element_setinfo22audio_element_handle_tP20audio_element_info_t"></a> <a id="_CPPv221audio_element_setinfo22audio_element_handle_tP20audio_element_info_t"></a> <a id="audio_element_setinfo__audio_element_handle_t.audio_element_info_tP"></a> <a id="audio__element_8h_1a529406a2505c9e36c32b79ebfce29084"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_setinfo([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_element\_info\_t](#_CPPv420audio_element_info_t "audio_element_info_t") \*info)
:   Set audio element infomation.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **info** – **\[in\]** The information pointer

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv421audio_element_getinfo22audio_element_handle_tP20audio_element_info_t"></a>

<a id="_CPPv321audio_element_getinfo22audio_element_handle_tP20audio_element_info_t"></a> <a id="_CPPv221audio_element_getinfo22audio_element_handle_tP20audio_element_info_t"></a> <a id="audio_element_getinfo__audio_element_handle_t.audio_element_info_tP"></a> <a id="audio__element_8h_1a5fb11d0d151e1efdc21ccb10047487d7"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_getinfo([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_element\_info\_t](#_CPPv420audio_element_info_t "audio_element_info_t") \*info)
:   Get audio element infomation.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **info** – **\[inout\]** The information pointer

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv429audio_element_set_uplink_caps22audio_element_handle_tPK17aud_uplink_caps_t"></a>

<a id="_CPPv329audio_element_set_uplink_caps22audio_element_handle_tPK17aud_uplink_caps_t"></a> <a id="_CPPv229audio_element_set_uplink_caps22audio_element_handle_tPK17aud_uplink_caps_t"></a> <a id="audio_element_set_uplink_caps__audio_element_handle_t.aud_uplink_caps_tCP"></a> <a id="audio__element_8h_1ac9ab6468564738ea7c463acb1a835749"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_uplink\_caps([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, const aud\_uplink\_caps\_t \*caps)
:   Publish this element’s uplink capture caps (producer side, e.g. mic). The pipeline forwards the effective caps downstream at link time so a consumer (e.g. AEC) can derive the interleaved lane layout without any hand-set lane geometry. Purely additive; elements that never call this are unaffected.

<a id="_CPPv429audio_element_get_uplink_caps22audio_element_handle_tP17aud_uplink_caps_t"></a>

<a id="_CPPv329audio_element_get_uplink_caps22audio_element_handle_tP17aud_uplink_caps_t"></a> <a id="_CPPv229audio_element_get_uplink_caps22audio_element_handle_tP17aud_uplink_caps_t"></a> <a id="audio_element_get_uplink_caps__audio_element_handle_t.aud_uplink_caps_tP"></a> <a id="audio__element_8h_1aaf5d295b9fe82555a66f624b06f27c30"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_get\_uplink\_caps([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, aud\_uplink\_caps\_t \*caps)
:   Get this element’s EFFECTIVE uplink caps: its own published caps if valid, otherwise the caps forwarded from upstream (pass-through). Used by the pipeline to propagate caps across intermediate elements (e.g. a resampler that does not change channel geometry).

<a id="_CPPv435audio_element_set_input_uplink_caps22audio_element_handle_tPK17aud_uplink_caps_t"></a>

<a id="_CPPv335audio_element_set_input_uplink_caps22audio_element_handle_tPK17aud_uplink_caps_t"></a> <a id="_CPPv235audio_element_set_input_uplink_caps22audio_element_handle_tPK17aud_uplink_caps_t"></a> <a id="audio_element_set_input_uplink_caps__audio_element_handle_t.aud_uplink_caps_tCP"></a> <a id="audio__element_8h_1a5c548c7eadf3a83cd16cbdcee5130645"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_input\_uplink\_caps([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, const aud\_uplink\_caps\_t \*caps)
:   Set the uplink caps forwarded from upstream (called by the pipeline at link time). Consumers read these via audio\_element\_get\_input\_uplink\_caps().

<a id="_CPPv435audio_element_get_input_uplink_caps22audio_element_handle_tP17aud_uplink_caps_t"></a>

<a id="_CPPv335audio_element_get_input_uplink_caps22audio_element_handle_tP17aud_uplink_caps_t"></a> <a id="_CPPv235audio_element_get_input_uplink_caps22audio_element_handle_tP17aud_uplink_caps_t"></a> <a id="audio_element_get_input_uplink_caps__audio_element_handle_t.aud_uplink_caps_tP"></a> <a id="audio__element_8h_1ae6852d7940ce685722f6f4bb5773573f"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_get\_input\_uplink\_caps([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, aud\_uplink\_caps\_t \*caps)
:   Get the uplink caps forwarded from upstream (consumer side, e.g. AEC). caps-\>valid is 0 when no producer upstream published any.

<a id="_CPPv421audio_element_set_uri22audio_element_handle_tPKc"></a>

<a id="_CPPv321audio_element_set_uri22audio_element_handle_tPKc"></a> <a id="_CPPv221audio_element_set_uri22audio_element_handle_tPKc"></a> <a id="audio_element_set_uri__audio_element_handle_t.cCP"></a> <a id="audio__element_8h_1a8b0d1e418a7079282a87d7464a314789"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_uri([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, const char \*uri)
:   Set audio element URI.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **uri** – **\[in\]** The uri pointer

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv421audio_element_get_uri22audio_element_handle_t"></a>

<a id="_CPPv321audio_element_get_uri22audio_element_handle_t"></a> <a id="_CPPv221audio_element_get_uri22audio_element_handle_t"></a> <a id="audio_element_get_uri__audio_element_handle_t"></a> <a id="audio__element_8h_1a5218276785e9c884d646b637dcc40d10"></a> char \*audio\_element\_get\_uri([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get audio element URI.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   URI pointer

<a id="_CPPv417audio_element_run22audio_element_handle_t"></a>

<a id="_CPPv317audio_element_run22audio_element_handle_t"></a> <a id="_CPPv217audio_element_run22audio_element_handle_t"></a> <a id="audio_element_run__audio_element_handle_t"></a> <a id="audio__element_8h_1aaaf9ad0b468b90133fa4bc5fe43673cc"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_run([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Start Audio Element. With this function, audio\_element will start as freeRTOS task, and put the task into ‘PAUSED’ state. Note: Element does not actually start when this function returns.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv423audio_element_terminate22audio_element_handle_t"></a>

<a id="_CPPv323audio_element_terminate22audio_element_handle_t"></a> <a id="_CPPv223audio_element_terminate22audio_element_handle_t"></a> <a id="audio_element_terminate__audio_element_handle_t"></a> <a id="audio__element_8h_1abecac1c83bebd768a2d9878ad77bf6b2"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_terminate([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Terminate Audio Element. With this function, audio\_element will exit the task function. Note: this API only sends request. It does not actually terminate immediately when this function returns.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv434audio_element_terminate_with_ticks22audio_element_handle_t10TickType_t"></a>

<a id="_CPPv334audio_element_terminate_with_ticks22audio_element_handle_t10TickType_t"></a> <a id="_CPPv234audio_element_terminate_with_ticks22audio_element_handle_t10TickType_t"></a> <a id="audio_element_terminate_with_ticks__audio_element_handle_t.TickType_t"></a> <a id="audio__element_8h_1ab802da1f540851fae09eaa6ed74c7d4f"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_terminate\_with\_ticks([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, TickType\_t ticks\_to\_wait)
:   Terminate Audio Element with specific ticks for timeout. With this function, audio\_element will exit the task function. Note: this API only sends request. It does not actually terminate immediately when this function returns.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **ticks\_to\_wait** – **\[in\]** The maximum amount of time to blocking

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv418audio_element_stop22audio_element_handle_t"></a>

<a id="_CPPv318audio_element_stop22audio_element_handle_t"></a> <a id="_CPPv218audio_element_stop22audio_element_handle_t"></a> <a id="audio_element_stop__audio_element_handle_t"></a> <a id="audio__element_8h_1a89b1068f0daa32fc74bb8a3ebb19091e"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_stop([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Request stop of the Audio Element. After receiving the stop request, the element will ignore the actions being performed (read/write, wait for the ringbuffer …) and close the task, reset the state variables. Note: this API only sends requests, Element does not actually stop when this function returns.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv427audio_element_wait_for_stop22audio_element_handle_t"></a>

<a id="_CPPv327audio_element_wait_for_stop22audio_element_handle_t"></a> <a id="_CPPv227audio_element_wait_for_stop22audio_element_handle_t"></a> <a id="audio_element_wait_for_stop__audio_element_handle_t"></a> <a id="audio__element_8h_1aab5019fc1de719f26ee56e42e09d42c0"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_wait\_for\_stop([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   After the `audio_element_stop` function is called, the Element task will perform some abort procedures. This function will be blocked (Time is DEFAULT\_MAX\_WAIT\_TIME) until Element Task has done and exit.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK, Success
        - BK\_FAIL, The state is not AEL\_STATE\_RUNNING
        - BK\_ERR\_ADK\_TIMEOUT, Timeout

<a id="_CPPv430audio_element_wait_for_stop_ms22audio_element_handle_t10TickType_t"></a>

<a id="_CPPv330audio_element_wait_for_stop_ms22audio_element_handle_t10TickType_t"></a> <a id="_CPPv230audio_element_wait_for_stop_ms22audio_element_handle_t10TickType_t"></a> <a id="audio_element_wait_for_stop_ms__audio_element_handle_t.TickType_t"></a> <a id="audio__element_8h_1a1ad69193cb86ce11f7d06b6c37eafd27"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_wait\_for\_stop\_ms([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, TickType\_t ticks\_to\_wait)
:   After the `audio_element_stop` function is called, the Element task will perform some abort procedures. The maximum amount of time should block waiting for Element task has stopped.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **ticks\_to\_wait** – **\[in\]** The maximum amount of time to wait for stop

    返回
    :   - BK\_OK, Success
        - BK\_FAIL, The state is not AEL\_STATE\_RUNNING
        - BK\_ERR\_ADK\_TIMEOUT, Timeout

<a id="_CPPv419audio_element_pause22audio_element_handle_t"></a>

<a id="_CPPv319audio_element_pause22audio_element_handle_t"></a> <a id="_CPPv219audio_element_pause22audio_element_handle_t"></a> <a id="audio_element_pause__audio_element_handle_t"></a> <a id="audio__element_8h_1af48abb143ddc68162255708f98307c69"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_pause([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Request audio Element enter ‘PAUSE’ state. In this state, the task will wait for any event.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv420audio_element_resume22audio_element_handle_tf10TickType_t"></a>

<a id="_CPPv320audio_element_resume22audio_element_handle_tf10TickType_t"></a> <a id="_CPPv220audio_element_resume22audio_element_handle_tf10TickType_t"></a> <a id="audio_element_resume__audio_element_handle_t.float.TickType_t"></a> <a id="audio__element_8h_1ae1344df5c045932a99062e3ec2f0530c"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_resume([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, float wait\_for\_rb\_threshold, TickType\_t timeout)
:   Request audio Element enter ‘RUNNING’ state. In this state, the task listens to events and invokes the callback functions. At the same time it will wait until the size/total\_size of the output ringbuffer is greater than or equal to `wait_for_rb_threshold`. If the timeout period has been exceeded and ringbuffer output has not yet reached `wait_for_rb_threshold` then the function will return.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **wait\_for\_rb\_threshold** – **\[in\]** The wait for rb threshold (0 .. 1\)
        - **timeout** – **\[in\]** The timeout

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv430audio_element_msg_set_listener22audio_element_handle_t26audio_event_iface_handle_t"></a>

<a id="_CPPv330audio_element_msg_set_listener22audio_element_handle_t26audio_event_iface_handle_t"></a> <a id="_CPPv230audio_element_msg_set_listener22audio_element_handle_t26audio_event_iface_handle_t"></a> <a id="audio_element_msg_set_listener__audio_element_handle_t.audio_event_iface_handle_t"></a> <a id="audio__element_8h_1a0bcc6696003c244719fcac058d8d1788"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_msg\_set\_listener([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_event\_iface\_handle\_t](audio_event_iface.md#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener)
:   This function will add a `listener` to listen to all events from audio element `el`. Any event from el-\>external\_event will be send to the `listener`.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **listener** – **\[in\]** The event will be listen to

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv432audio_element_set_event_callback22audio_element_handle_t13event_cb_funcPv"></a>

<a id="_CPPv332audio_element_set_event_callback22audio_element_handle_t13event_cb_funcPv"></a> <a id="_CPPv232audio_element_set_event_callback22audio_element_handle_t13event_cb_funcPv"></a> <a id="audio_element_set_event_callback__audio_element_handle_t.event_cb_func.voidP"></a> <a id="audio__element_8h_1a41650aae6b24dd583d44ae5727b9f784"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_event\_callback([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [event\_cb\_func](#_CPPv413event_cb_func "event_cb_func") cb\_func, void \*ctx)
:   This function will add a `callback` to be called from audio element `el`. Any event to caller will cause to call callback function.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **cb\_func** – **\[in\]** The callback function
        - **ctx** – **\[in\]** Caller context

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv433audio_element_msg_remove_listener22audio_element_handle_t26audio_event_iface_handle_t"></a>

<a id="_CPPv333audio_element_msg_remove_listener22audio_element_handle_t26audio_event_iface_handle_t"></a> <a id="_CPPv233audio_element_msg_remove_listener22audio_element_handle_t26audio_event_iface_handle_t"></a> <a id="audio_element_msg_remove_listener__audio_element_handle_t.audio_event_iface_handle_t"></a> <a id="audio__element_8h_1a9a44fe668a6b2cee6558d5e66d701185"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_msg\_remove\_listener([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_event\_iface\_handle\_t](audio_event_iface.md#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") listener)
:   Remove listener out of el. No new events will be sent to the listener.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **listener** – **\[in\]** The listener

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv428audio_element_set_input_port22audio_element_handle_t19audio_port_handle_t"></a>

<a id="_CPPv328audio_element_set_input_port22audio_element_handle_t19audio_port_handle_t"></a> <a id="_CPPv228audio_element_set_input_port22audio_element_handle_t19audio_port_handle_t"></a> <a id="audio_element_set_input_port__audio_element_handle_t.audio_port_handle_t"></a> <a id="audio__element_8h_1a62057f8af54598c0bb888b164c4d0474"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_input\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_port\_handle\_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") port)
:   Set Element input ringbuffer.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **port** – **\[in\]** The audio port handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv428audio_element_get_input_port22audio_element_handle_t"></a>

<a id="_CPPv328audio_element_get_input_port22audio_element_handle_t"></a> <a id="_CPPv228audio_element_get_input_port22audio_element_handle_t"></a> <a id="audio_element_get_input_port__audio_element_handle_t"></a> <a id="audio__element_8h_1a3785d0873f1d9b0b683d155bf1efc7a0"></a> [audio\_port\_handle\_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") audio\_element\_get\_input\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get Element input audio port.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   audio\_port\_handle\_t

<a id="_CPPv429audio_element_set_output_port22audio_element_handle_t19audio_port_handle_t"></a>

<a id="_CPPv329audio_element_set_output_port22audio_element_handle_t19audio_port_handle_t"></a> <a id="_CPPv229audio_element_set_output_port22audio_element_handle_t19audio_port_handle_t"></a> <a id="audio_element_set_output_port__audio_element_handle_t.audio_port_handle_t"></a> <a id="audio__element_8h_1ae6801d98410dd63040a704cfab96a19c"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_output\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_port\_handle\_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") port)
:   Set Element output ringbuffer.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **port** – **\[in\]** The audio port handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv429audio_element_get_output_port22audio_element_handle_t"></a>

<a id="_CPPv329audio_element_get_output_port22audio_element_handle_t"></a> <a id="_CPPv229audio_element_get_output_port22audio_element_handle_t"></a> <a id="audio_element_get_output_port__audio_element_handle_t"></a> <a id="audio__element_8h_1a2bd648ef1715a162df303907d336f8c3"></a> [audio\_port\_handle\_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") audio\_element\_get\_output\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get Element output audio port.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   audio\_port\_handle\_t

<a id="_CPPv423audio_element_get_state22audio_element_handle_t"></a>

<a id="_CPPv323audio_element_get_state22audio_element_handle_t"></a> <a id="_CPPv223audio_element_get_state22audio_element_handle_t"></a> <a id="audio_element_get_state__audio_element_handle_t"></a> <a id="audio__element_8h_1aa55ec43d7dd725c69a51fe176e3b8a8f"></a> [audio\_element\_state\_t](#_CPPv421audio_element_state_t "audio_element_state_t") audio\_element\_get\_state([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get current Element state.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   audio\_element\_state\_t

<a id="_CPPv430audio_element_abort_input_port22audio_element_handle_t"></a>

<a id="_CPPv330audio_element_abort_input_port22audio_element_handle_t"></a> <a id="_CPPv230audio_element_abort_input_port22audio_element_handle_t"></a> <a id="audio_element_abort_input_port__audio_element_handle_t"></a> <a id="audio__element_8h_1a4e90d9897e0811cdfd71275a73f2921b"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_abort\_input\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   If the element is requesting data from the input audio port, this function forces it to abort.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv431audio_element_abort_output_port22audio_element_handle_t"></a>

<a id="_CPPv331audio_element_abort_output_port22audio_element_handle_t"></a> <a id="_CPPv231audio_element_abort_output_port22audio_element_handle_t"></a> <a id="audio_element_abort_output_port__audio_element_handle_t"></a> <a id="audio__element_8h_1a86bb52d548c7d8c0be41ecd171e420e3"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_abort\_output\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   If the element is waiting to write data to the output audio port, this function forces it to abort.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv429audio_element_wait_for_buffer22audio_element_handle_ti10TickType_t"></a>

<a id="_CPPv329audio_element_wait_for_buffer22audio_element_handle_ti10TickType_t"></a> <a id="_CPPv229audio_element_wait_for_buffer22audio_element_handle_ti10TickType_t"></a> <a id="audio_element_wait_for_buffer__audio_element_handle_t.i.TickType_t"></a> <a id="audio__element_8h_1a4fe95892a8f714bd5c617e8767d6dbe1"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_wait\_for\_buffer([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int size\_expect, TickType\_t timeout)
:   This function will wait until the sizeof the output ringbuffer is greater than or equal to `size_expect`. If the timeout period has been exceeded and ringbuffer output has not yet reached `size_expect` then the function will return `BK_FAIL`

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **size\_expect** – **\[in\]** The size expect
        - **timeout** – **\[in\]** The timeout

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv427audio_element_report_status22audio_element_handle_t22audio_element_status_t"></a>

<a id="_CPPv327audio_element_report_status22audio_element_handle_t22audio_element_status_t"></a> <a id="_CPPv227audio_element_report_status22audio_element_handle_t22audio_element_status_t"></a> <a id="audio_element_report_status__audio_element_handle_t.audio_element_status_t"></a> <a id="audio__element_8h_1aa3d0ef2e488b60a72e6900dbb85f877e"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_report\_status([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_element\_status\_t](#_CPPv422audio_element_status_t "audio_element_status_t") status)
:   Element will sendout event (status) to event by this function.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **status** – **\[in\]** The status

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv425audio_element_report_info22audio_element_handle_t"></a>

<a id="_CPPv325audio_element_report_info22audio_element_handle_t"></a> <a id="_CPPv225audio_element_report_info22audio_element_handle_t"></a> <a id="audio_element_report_info__audio_element_handle_t"></a> <a id="audio__element_8h_1aab124cccfa742be632dd33809a409bbe"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_report\_info([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Element will sendout event (information) to event by this function.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv430audio_element_report_codec_fmt22audio_element_handle_t"></a>

<a id="_CPPv330audio_element_report_codec_fmt22audio_element_handle_t"></a> <a id="_CPPv230audio_element_report_codec_fmt22audio_element_handle_t"></a> <a id="audio_element_report_codec_fmt__audio_element_handle_t"></a> <a id="audio__element_8h_1a24d87134c95a35ed1ef19108cc19a25d"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_report\_codec\_fmt([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Element will sendout event (codec format) to event by this function.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv424audio_element_report_pos22audio_element_handle_t"></a>

<a id="_CPPv324audio_element_report_pos22audio_element_handle_t"></a> <a id="_CPPv224audio_element_report_pos22audio_element_handle_t"></a> <a id="audio_element_report_pos__audio_element_handle_t"></a> <a id="audio__element_8h_1a40e5805e6efdddcd928a2fad53bcf4de"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_report\_pos([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Element will sendout event with a duplicate information by this function.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL
        - BK\_ERR\_ADK\_NO\_MEM

<a id="_CPPv431audio_element_set_input_timeout22audio_element_handle_t10TickType_t"></a>

<a id="_CPPv331audio_element_set_input_timeout22audio_element_handle_t10TickType_t"></a> <a id="_CPPv231audio_element_set_input_timeout22audio_element_handle_t10TickType_t"></a> <a id="audio_element_set_input_timeout__audio_element_handle_t.TickType_t"></a> <a id="audio__element_8h_1a4e8608782e6a908b3ebeb861dd6c4678"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_input\_timeout([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, TickType\_t timeout)
:   Set input read timeout (default is `portMAX_DELAY`).

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **timeout** – **\[in\]** The timeout

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv432audio_element_set_output_timeout22audio_element_handle_t10TickType_t"></a>

<a id="_CPPv332audio_element_set_output_timeout22audio_element_handle_t10TickType_t"></a> <a id="_CPPv232audio_element_set_output_timeout22audio_element_handle_t10TickType_t"></a> <a id="audio_element_set_output_timeout__audio_element_handle_t.TickType_t"></a> <a id="audio__element_8h_1a5c8e818f7ee9636537fdf9910a393026"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_output\_timeout([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, TickType\_t timeout)
:   Set output read timeout (default is `portMAX_DELAY`).

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **timeout** – **\[in\]** The timeout

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv430audio_element_reset_input_port22audio_element_handle_t"></a>

<a id="_CPPv330audio_element_reset_input_port22audio_element_handle_t"></a> <a id="_CPPv230audio_element_reset_input_port22audio_element_handle_t"></a> <a id="audio_element_reset_input_port__audio_element_handle_t"></a> <a id="audio__element_8h_1a613f426b62fc03e5446108dd788386b9"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_reset\_input\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Reset input port.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv431audio_element_reset_output_port22audio_element_handle_t"></a>

<a id="_CPPv331audio_element_reset_output_port22audio_element_handle_t"></a> <a id="_CPPv231audio_element_reset_output_port22audio_element_handle_t"></a> <a id="audio_element_reset_output_port__audio_element_handle_t"></a> <a id="audio__element_8h_1ae3527bfa035d2c90f615442808907a0f"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_reset\_output\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Reset output port.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv419audio_element_input22audio_element_handle_tPci"></a>

<a id="_CPPv319audio_element_input22audio_element_handle_tPci"></a> <a id="_CPPv219audio_element_input22audio_element_handle_tPci"></a> <a id="audio_element_input__audio_element_handle_t.cP.i"></a> <a id="audio__element_8h_1a4f689be8acfc1eac3afde2071dac9289"></a> int audio\_element\_input([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, char \*buffer, int wanted\_size)
:   Call this function to provide Element input data. Depending on setup using ringbuffer or function callback, Element invokes read ringbuffer, or calls read callback funtion.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **buffer** – **\[in\]** The buffer pointer
        - **wanted\_size** – **\[in\]** The wanted size

    返回
    :   - \> 0 number of bytes produced
        - \<\=0 audio\_element\_err\_t

<a id="_CPPv420audio_element_output22audio_element_handle_tPci"></a>

<a id="_CPPv320audio_element_output22audio_element_handle_tPci"></a> <a id="_CPPv220audio_element_output22audio_element_handle_tPci"></a> <a id="audio_element_output__audio_element_handle_t.cP.i"></a> <a id="audio__element_8h_1afee05b260be67f3720f6f3e464e2aceb"></a> int audio\_element\_output([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, char \*buffer, int write\_size)
:   Call this function to sendout Element output data. Depending on setup using ringbuffer or function callback, Element will invoke write to ringbuffer, or call write callback funtion.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **buffer** – **\[in\]** The buffer pointer
        - **write\_size** – **\[in\]** The write size

    返回
    :   - \> 0 number of bytes written
        - \<\=0 audio\_element\_err\_t

<a id="_CPPv429audio_element_get_event_queue22audio_element_handle_t"></a>

<a id="_CPPv329audio_element_get_event_queue22audio_element_handle_t"></a> <a id="_CPPv229audio_element_get_event_queue22audio_element_handle_t"></a> <a id="audio_element_get_event_queue__audio_element_handle_t"></a> <a id="audio__element_8h_1ad52cec8231a405504417cdae5e1a7094"></a> QueueHandle\_t audio\_element\_get\_event\_queue([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get External queue of Emitter. We can read any event that has been send out of Element from this `QueueHandle_t`.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   QueueHandle\_t

<a id="_CPPv427audio_element_set_port_done22audio_element_handle_t"></a>

<a id="_CPPv327audio_element_set_port_done22audio_element_handle_t"></a> <a id="_CPPv227audio_element_set_port_done22audio_element_handle_t"></a> <a id="audio_element_set_port_done__audio_element_handle_t"></a> <a id="audio__element_8h_1a8faebe7ff9dbb2bb76b2873196f783f0"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_port\_done([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Set input port and output port have finished.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv425audio_element_reset_state22audio_element_handle_t"></a>

<a id="_CPPv325audio_element_reset_state22audio_element_handle_t"></a> <a id="_CPPv225audio_element_reset_state22audio_element_handle_t"></a> <a id="audio_element_reset_state__audio_element_handle_t"></a> <a id="audio__element_8h_1a0afbd9370f36ec76437617007de1a93a"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_reset\_state([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Enforce ‘AEL\_STATE\_INIT’ state.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv437audio_element_get_output_ringbuf_size22audio_element_handle_t"></a>

<a id="_CPPv337audio_element_get_output_ringbuf_size22audio_element_handle_t"></a> <a id="_CPPv237audio_element_get_output_ringbuf_size22audio_element_handle_t"></a> <a id="audio_element_get_output_ringbuf_size__audio_element_handle_t"></a> <a id="audio__element_8h_1a3a30e8803634782ecb38cc9127c6d48e"></a> int audio\_element\_get\_output\_ringbuf\_size([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get Element output ringbuffer size.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - \=0: Parameter NULL
        - \>0: Size of ringbuffer

<a id="_CPPv437audio_element_set_output_ringbuf_size22audio_element_handle_ti"></a>

<a id="_CPPv337audio_element_set_output_ringbuf_size22audio_element_handle_ti"></a> <a id="_CPPv237audio_element_set_output_ringbuf_size22audio_element_handle_ti"></a> <a id="audio_element_set_output_ringbuf_size__audio_element_handle_t.i"></a> <a id="audio__element_8h_1ae514ff4739c0e0cb7909338d8fbd283b"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_output\_ringbuf\_size([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int rb\_size)
:   Set Element output ringbuffer size.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **rb\_size** – **\[in\]** Size of the ringbuffer

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv438audio_element_get_output_framebuf_size22audio_element_handle_tPiPi"></a>

<a id="_CPPv338audio_element_get_output_framebuf_size22audio_element_handle_tPiPi"></a> <a id="_CPPv238audio_element_get_output_framebuf_size22audio_element_handle_tPiPi"></a> <a id="audio_element_get_output_framebuf_size__audio_element_handle_t.iP.iP"></a> <a id="audio__element_8h_1acffe1163226e46aac8b7232bb8cd37d2"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_get\_output\_framebuf\_size([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int \*node\_size, int \*node\_num)
:   Get Element output port framebuffer size.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **node\_size** – **\[in\]** Size of the framebuffer node
        - **node\_num** – **\[in\]** Numbers of the framebuffer node

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv438audio_element_set_output_framebuf_size22audio_element_handle_tii"></a>

<a id="_CPPv338audio_element_set_output_framebuf_size22audio_element_handle_tii"></a> <a id="_CPPv238audio_element_set_output_framebuf_size22audio_element_handle_tii"></a> <a id="audio_element_set_output_framebuf_size__audio_element_handle_t.i.i"></a> <a id="audio__element_8h_1a56f5d46c37be908b72c8b6d899881940"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_output\_framebuf\_size([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int node\_size, int node\_num)
:   Set Element output port framebuffer size.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **node\_size** – **\[in\]** Size of the framebuffer node
        - **node\_num** – **\[in\]** Numbers of the framebuffer node

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv425audio_element_multi_input22audio_element_handle_tPcii10TickType_t"></a>

<a id="_CPPv325audio_element_multi_input22audio_element_handle_tPcii10TickType_t"></a> <a id="_CPPv225audio_element_multi_input22audio_element_handle_tPcii10TickType_t"></a> <a id="audio_element_multi_input__audio_element_handle_t.cP.i.i.TickType_t"></a> <a id="audio__element_8h_1aa30577809fc4a5ced999c97ff6e0375b"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_multi\_input([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, char \*buffer, int wanted\_size, int index, TickType\_t ticks\_to\_wait)
:   Call this function to read data from multi input ringbuffer by given index.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **buffer** – **\[inout\]** The buffer pointer
        - **wanted\_size** – **\[in\]** The wanted size
        - **index** – **\[in\]** The index of multi input ringbuffer, start from `0`, should be less than `NUMBER_OF_MULTI_RINGBUF`
        - **ticks\_to\_wait** – **\[in\]** Timeout of ringbuffer

    返回
    :   - \>\= 0: Size of input
        - \< 0: Error

<a id="_CPPv426audio_element_multi_output22audio_element_handle_tPci10TickType_t"></a>

<a id="_CPPv326audio_element_multi_output22audio_element_handle_tPci10TickType_t"></a> <a id="_CPPv226audio_element_multi_output22audio_element_handle_tPci10TickType_t"></a> <a id="audio_element_multi_output__audio_element_handle_t.cP.i.TickType_t"></a> <a id="audio__element_8h_1a492fbd1066270ab79f18d70c0731eb7e"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_multi\_output([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, char \*buffer, int wanted\_size, TickType\_t ticks\_to\_wait)
:   Call this function write data by multi output ringbuffer.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **buffer** – **\[in\]** The buffer pointer
        - **wanted\_size** – **\[in\]** The wanted size
        - **ticks\_to\_wait** – **\[in\]** Timeout of ringbuffer

    返回
    :   - \>\= 0: Size of output
        - \< 0: Error

<a id="_CPPv434audio_element_set_multi_input_port22audio_element_handle_t19audio_port_handle_ti"></a>

<a id="_CPPv334audio_element_set_multi_input_port22audio_element_handle_t19audio_port_handle_ti"></a> <a id="_CPPv234audio_element_set_multi_input_port22audio_element_handle_t19audio_port_handle_ti"></a> <a id="audio_element_set_multi_input_port__audio_element_handle_t.audio_port_handle_t.i"></a> <a id="audio__element_8h_1aaca572551a23b449ca65154d02cf1146"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_multi\_input\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_port\_handle\_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") port, int index)
:   Set multi input port Element.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **port** – **\[in\]** The audio port handle
        - **index** – **\[in\]** Index of multi port, starts from `0`, should be less than `NUMBER_OF_MULTI_PORT`

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv435audio_element_set_multi_output_port22audio_element_handle_t19audio_port_handle_ti"></a>

<a id="_CPPv335audio_element_set_multi_output_port22audio_element_handle_t19audio_port_handle_ti"></a> <a id="_CPPv235audio_element_set_multi_output_port22audio_element_handle_t19audio_port_handle_ti"></a> <a id="audio_element_set_multi_output_port__audio_element_handle_t.audio_port_handle_t.i"></a> <a id="audio__element_8h_1ad0bad6960b3d6ee94669c8960ece66ce"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_multi\_output\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_port\_handle\_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") port, int index)
:   Set multi output ringbuffer Element.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **port** – **\[in\]** The audio port handle
        - **index** – **\[in\]** Index of multi ringbuffer, starts from `0`, should be less than `NUMBER_OF_MULTI_PORT`

    返回
    :   - BK\_OK
        - BK\_ERR\_ADK\_INVALID\_ARG

<a id="_CPPv434audio_element_get_multi_input_port22audio_element_handle_ti"></a>

<a id="_CPPv334audio_element_get_multi_input_port22audio_element_handle_ti"></a> <a id="_CPPv234audio_element_get_multi_input_port22audio_element_handle_ti"></a> <a id="audio_element_get_multi_input_port__audio_element_handle_t.i"></a> <a id="audio__element_8h_1af52bec4adbf563ee57d915f02abc05d5"></a> [audio\_port\_handle\_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") audio\_element\_get\_multi\_input\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int index)
:   Get handle of multi input audio port Element by index.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **index** – **\[in\]** Index of multi audio port, starts from `0`, should be less than `NUMBER_OF_MULTI_PORT`

    返回
    :   - NULL Error
        - Others audio\_port\_handle\_t

<a id="_CPPv442audio_element_get_multi_input_max_port_num22audio_element_handle_t"></a>

<a id="_CPPv342audio_element_get_multi_input_max_port_num22audio_element_handle_t"></a> <a id="_CPPv242audio_element_get_multi_input_max_port_num22audio_element_handle_t"></a> <a id="audio_element_get_multi_input_max_port_num__audio_element_handle_t"></a> <a id="audio__element_8h_1a616977061e0b68c0718df8d9e8bf222b"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_get\_multi\_input\_max\_port\_num([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get max port number of multi input audio port Element.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - \>\= 0: Max port number of multi input audio port Element
        - \< 0: Error

<a id="_CPPv443audio_element_get_multi_output_max_port_num22audio_element_handle_t"></a>

<a id="_CPPv343audio_element_get_multi_output_max_port_num22audio_element_handle_t"></a> <a id="_CPPv243audio_element_get_multi_output_max_port_num22audio_element_handle_t"></a> <a id="audio_element_get_multi_output_max_port_num__audio_element_handle_t"></a> <a id="audio__element_8h_1a47f42ba9b045963c2db267216d6cfb8a"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_get\_multi\_output\_max\_port\_num([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get max port number of multi output audio port Element.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - \>\= 0: Max port number of multi output audio port Element
        - \< 0: Error

<a id="_CPPv435audio_element_get_multi_output_port22audio_element_handle_ti"></a>

<a id="_CPPv335audio_element_get_multi_output_port22audio_element_handle_ti"></a> <a id="_CPPv235audio_element_get_multi_output_port22audio_element_handle_ti"></a> <a id="audio_element_get_multi_output_port__audio_element_handle_t.i"></a> <a id="audio__element_8h_1aee385fe284185e039ec6ef452770f4cf"></a> [audio\_port\_handle\_t](audio_port.md#_CPPv419audio_port_handle_t "audio_port_handle_t") audio\_element\_get\_multi\_output\_port([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int index)
:   Get handle of multi output audio port Element by index.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **index** – **\[in\]** Index of multi audio port, starts from `0`, should be less than `NUMBER_OF_MULTI_PORT`

    返回
    :   - NULL Error
        - Others audio\_port\_handle\_t

<a id="_CPPv426audio_element_process_init22audio_element_handle_t"></a>

<a id="_CPPv326audio_element_process_init22audio_element_handle_t"></a> <a id="_CPPv226audio_element_process_init22audio_element_handle_t"></a> <a id="audio_element_process_init__audio_element_handle_t"></a> <a id="audio__element_8h_1a1f1525bd41702d7a67d82773c0c83da6"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_process\_init([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Provides a way to call element’s `open`

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv428audio_element_process_deinit22audio_element_handle_t"></a>

<a id="_CPPv328audio_element_process_deinit22audio_element_handle_t"></a> <a id="_CPPv228audio_element_process_deinit22audio_element_handle_t"></a> <a id="audio_element_process_deinit__audio_element_handle_t"></a> <a id="audio__element_8h_1ada8eb2a00a066c910b5954e6f50912de"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_process\_deinit([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Provides a way to call element’s `close`

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv418audio_element_seek22audio_element_handle_tPviPvPi"></a>

<a id="_CPPv318audio_element_seek22audio_element_handle_tPviPvPi"></a> <a id="_CPPv218audio_element_seek22audio_element_handle_tPviPvPi"></a> <a id="audio_element_seek__audio_element_handle_t.voidP.i.voidP.iP"></a> <a id="audio__element_8h_1ad8b0c717ab210417789be2905c453b43"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_seek([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, void \*in\_data, int in\_size, void \*out\_data, int \*out\_size)
:   Call element’s `seek`

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **in\_data** – **\[in\]** A pointer to in data
        - **in\_size** – **\[in\]** The size of the `in_data`
        - **out\_data** – **\[out\]** A pointer to the out data
        - **out\_size** – **\[out\]** The size of the `out_data`

    返回
    :   - BK\_OK
        - BK\_FAIL
        - BK\_ERR\_ADK\_NOT\_SUPPORT

<a id="_CPPv425audio_element_is_stopping22audio_element_handle_t"></a>

<a id="_CPPv325audio_element_is_stopping22audio_element_handle_t"></a> <a id="_CPPv225audio_element_is_stopping22audio_element_handle_t"></a> <a id="audio_element_is_stopping__audio_element_handle_t"></a> <a id="audio__element_8h_1a1bf4cdb7fb5ca06f24025f284ea1bf0e"></a> bool audio\_element\_is\_stopping([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get Element stopping flag.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   element’s stopping flag

<a id="_CPPv429audio_element_update_byte_pos22audio_element_handle_ti"></a>

<a id="_CPPv329audio_element_update_byte_pos22audio_element_handle_ti"></a> <a id="_CPPv229audio_element_update_byte_pos22audio_element_handle_ti"></a> <a id="audio_element_update_byte_pos__audio_element_handle_t.i"></a> <a id="audio__element_8h_1aebbd7e86947e7ca5bbe1b8245af9c33a"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_update\_byte\_pos([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int pos)
:   Update the byte position of element information.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **pos** – **\[in\]** The byte\_pos accumulated by this value

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv426audio_element_set_byte_pos22audio_element_handle_ti"></a>

<a id="_CPPv326audio_element_set_byte_pos22audio_element_handle_ti"></a> <a id="_CPPv226audio_element_set_byte_pos22audio_element_handle_ti"></a> <a id="audio_element_set_byte_pos__audio_element_handle_t.i"></a> <a id="audio__element_8h_1a77b4902422289e0786c3f12107b78d54"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_byte\_pos([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int pos)
:   Set the byte position of element information.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **pos** – **\[in\]** This value is assigned to byte\_pos

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv432audio_element_update_total_bytes22audio_element_handle_ti"></a>

<a id="_CPPv332audio_element_update_total_bytes22audio_element_handle_ti"></a> <a id="_CPPv232audio_element_update_total_bytes22audio_element_handle_ti"></a> <a id="audio_element_update_total_bytes__audio_element_handle_t.i"></a> <a id="audio__element_8h_1af6727fedf07537fec7452c03512c3278"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_update\_total\_bytes([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int total\_bytes)
:   Update the total bytes of element information.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **total\_bytes** – **\[in\]** The total\_bytes accumulated by this value

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv429audio_element_set_total_bytes22audio_element_handle_ti"></a>

<a id="_CPPv329audio_element_set_total_bytes22audio_element_handle_ti"></a> <a id="_CPPv229audio_element_set_total_bytes22audio_element_handle_ti"></a> <a id="audio_element_set_total_bytes__audio_element_handle_t.i"></a> <a id="audio__element_8h_1ad2e5d1b0ae14d9ed3ab96edc984bac44"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_total\_bytes([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int total\_bytes)
:   Set the total bytes of element information.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **total\_bytes** – **\[in\]** This value is assigned to total\_bytes

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv421audio_element_set_bps22audio_element_handle_ti"></a>

<a id="_CPPv321audio_element_set_bps22audio_element_handle_ti"></a> <a id="_CPPv221audio_element_set_bps22audio_element_handle_ti"></a> <a id="audio_element_set_bps__audio_element_handle_t.i"></a> <a id="audio__element_8h_1ae1cc81de6715138d8bf82b0258af3060"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_bps([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int bit\_rate)
:   Set the bps of element information.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **bit\_rate** – **\[in\]** This value is assigned to bps

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv427audio_element_set_codec_fmt22audio_element_handle_ti"></a>

<a id="_CPPv327audio_element_set_codec_fmt22audio_element_handle_ti"></a> <a id="_CPPv227audio_element_set_codec_fmt22audio_element_handle_ti"></a> <a id="audio_element_set_codec_fmt__audio_element_handle_t.i"></a> <a id="audio__element_8h_1a299fe6cb3704028301608f75e47643cd"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_codec\_fmt([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int format)
:   Set the codec format of element information.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **format** – **\[in\]** This value is assigned to codec\_fmt

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv428audio_element_set_music_info22audio_element_handle_tiii"></a>

<a id="_CPPv328audio_element_set_music_info22audio_element_handle_tiii"></a> <a id="_CPPv228audio_element_set_music_info22audio_element_handle_tiii"></a> <a id="audio_element_set_music_info__audio_element_handle_t.i.i.i"></a> <a id="audio__element_8h_1aa93b7562162ea119d81eec2efb4889da"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_music\_info([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int sample\_rates, int channels, int bits)
:   Set the sample\_rate, channels, bits of element information.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **sample\_rates** – **\[in\]** Sample\_rates of music information
        - **channels** – **\[in\]** Channels of music information
        - **bits** – **\[in\]** Bits of music information

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv426audio_element_set_duration22audio_element_handle_ti"></a>

<a id="_CPPv326audio_element_set_duration22audio_element_handle_ti"></a> <a id="_CPPv226audio_element_set_duration22audio_element_handle_ti"></a> <a id="audio_element_set_duration__audio_element_handle_t.i"></a> <a id="audio__element_8h_1a306a34c9518a13da074794df94bf4318"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_duration([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, int duration)
:   Set the duration of element information.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **duration** – **\[in\]** This value is assigned to duration

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv434audio_element_get_output_port_type22audio_element_handle_t"></a>

<a id="_CPPv334audio_element_get_output_port_type22audio_element_handle_t"></a> <a id="_CPPv234audio_element_get_output_port_type22audio_element_handle_t"></a> <a id="audio_element_get_output_port_type__audio_element_handle_t"></a> <a id="audio__element_8h_1af06c6e88c4975be91977ad7614f8dddc"></a> [port\_type\_t](audio_port.md#_CPPv411port_type_t "port_type_t") audio\_element\_get\_output\_port\_type([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get the type of element output port.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - 0 Error
        - Others port\_type\_t

<a id="_CPPv433audio_element_get_input_port_type22audio_element_handle_t"></a>

<a id="_CPPv333audio_element_get_input_port_type22audio_element_handle_t"></a> <a id="_CPPv233audio_element_get_input_port_type22audio_element_handle_t"></a> <a id="audio_element_get_input_port_type__audio_element_handle_t"></a> <a id="audio__element_8h_1a5082aaae0e0c431f341e109be1374d86"></a> [port\_type\_t](audio_port.md#_CPPv411port_type_t "port_type_t") audio\_element\_get\_input\_port\_type([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Get the type of element input port.

    参数
    :   **el** – **\[in\]** The audio element handle

    返回
    :   - 0 Error
        - Others port\_type\_t

<a id="_CPPv434audio_element_set_output_port_type22audio_element_handle_t11port_type_t"></a>

<a id="_CPPv334audio_element_set_output_port_type22audio_element_handle_t11port_type_t"></a> <a id="_CPPv234audio_element_set_output_port_type22audio_element_handle_t11port_type_t"></a> <a id="audio_element_set_output_port_type__audio_element_handle_t.port_type_t"></a> <a id="audio__element_8h_1a6d51501e019916379aea606396e185f1"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_output\_port\_type([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [port\_type\_t](audio_port.md#_CPPv411port_type_t "port_type_t") type)
:   Set the type of element output port.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **type** – **\[in\]** The audio port type

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="_CPPv433audio_element_set_input_port_type22audio_element_handle_t11port_type_t"></a>

<a id="_CPPv333audio_element_set_input_port_type22audio_element_handle_t11port_type_t"></a> <a id="_CPPv233audio_element_set_input_port_type22audio_element_handle_t11port_type_t"></a> <a id="audio_element_set_input_port_type__audio_element_handle_t.port_type_t"></a> <a id="audio__element_8h_1a089d220c2ed74a6d5da00e32a0d88673"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_element\_set\_input\_port\_type([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [port\_type\_t](audio_port.md#_CPPv411port_type_t "port_type_t") type)
:   Set the type of element input port.

    参数
    :   - **el** – **\[in\]** The audio element handle
        - **type** – **\[in\]** The audio port type

    返回
    :   - BK\_OK
        - BK\_FAIL

<a id="structures"></a>

### Structures

<a id="_CPPv420audio_element_info_t"></a>

<a id="_CPPv320audio_element_info_t"></a> <a id="_CPPv220audio_element_info_t"></a> <a id="audio_element_info_t"></a> <a id="structaudio__element__info__t"></a> struct audio\_element\_info\_t
:   Audio Element informations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20audio_element_info_t12sample_ratesE"></a>

    <a id="_CPPv3N20audio_element_info_t12sample_ratesE"></a> <a id="_CPPv2N20audio_element_info_t12sample_ratesE"></a> <a id="audio_element_info_t::sample_rates__i"></a> <a id="structaudio__element__info__t_1a5c21cadd134f042f9425aff26e4a374c"></a> int sample\_rates
    :   Sample rates in Hz

    <a id="_CPPv4N20audio_element_info_t8channelsE"></a>

    <a id="_CPPv3N20audio_element_info_t8channelsE"></a> <a id="_CPPv2N20audio_element_info_t8channelsE"></a> <a id="audio_element_info_t::channels__i"></a> <a id="structaudio__element__info__t_1a10b9bdfbf5b249cfec76fe01fc9ad19d"></a> int channels
    :   Number of audio channel, mono is 1, stereo is 2

    <a id="_CPPv4N20audio_element_info_t4bitsE"></a>

    <a id="_CPPv3N20audio_element_info_t4bitsE"></a> <a id="_CPPv2N20audio_element_info_t4bitsE"></a> <a id="audio_element_info_t::bits__i"></a> <a id="structaudio__element__info__t_1a3757725a1d181f9879c9fa8650bdb6aa"></a> int bits
    :   Bit wide (8, 16, 24, 32 bits)

    <a id="_CPPv4N20audio_element_info_t3bpsE"></a>

    <a id="_CPPv3N20audio_element_info_t3bpsE"></a> <a id="_CPPv2N20audio_element_info_t3bpsE"></a> <a id="audio_element_info_t::bps__i"></a> <a id="structaudio__element__info__t_1a76f1a9c0541288243d0175286b85065d"></a> int bps
    :   Bit per second

    <a id="_CPPv4N20audio_element_info_t8byte_posE"></a>

    <a id="_CPPv3N20audio_element_info_t8byte_posE"></a> <a id="_CPPv2N20audio_element_info_t8byte_posE"></a> <a id="audio_element_info_t::byte_pos__int64_t"></a> <a id="structaudio__element__info__t_1acd41b1a35453327bacdfa60255db1524"></a> int64\_t byte\_pos
    :   The current position (in bytes) being processed for an element

    <a id="_CPPv4N20audio_element_info_t11total_bytesE"></a>

    <a id="_CPPv3N20audio_element_info_t11total_bytesE"></a> <a id="_CPPv2N20audio_element_info_t11total_bytesE"></a> <a id="audio_element_info_t::total_bytes__int64_t"></a> <a id="structaudio__element__info__t_1a1b875c96a4f8827e9a0e2a5256b88e7e"></a> int64\_t total\_bytes
    :   The total bytes for an element

    <a id="_CPPv4N20audio_element_info_t8durationE"></a>

    <a id="_CPPv3N20audio_element_info_t8durationE"></a> <a id="_CPPv2N20audio_element_info_t8durationE"></a> <a id="audio_element_info_t::duration__i"></a> <a id="structaudio__element__info__t_1a74a4c4d62fa646ee7d7192a63ac3d4b7"></a> int duration
    :   The duration for an element (optional)

    <a id="_CPPv4N20audio_element_info_t3uriE"></a>

    <a id="_CPPv3N20audio_element_info_t3uriE"></a> <a id="_CPPv2N20audio_element_info_t3uriE"></a> <a id="audio_element_info_t::uri__cP"></a> <a id="structaudio__element__info__t_1a92a193da6cc928824a39b2004ef3a0a4"></a> char \*uri
    :   URI (optional)

    <a id="_CPPv4N20audio_element_info_t9codec_fmtE"></a>

    <a id="_CPPv3N20audio_element_info_t9codec_fmtE"></a> <a id="_CPPv2N20audio_element_info_t9codec_fmtE"></a> <a id="audio_element_info_t::codec_fmt__bk_codec_type_t"></a> <a id="structaudio__element__info__t_1a11c91b1055bdd3b8cf9e18df8b458665"></a> [bk\_codec\_type\_t](audio_types.md#_CPPv415bk_codec_type_t "bk_codec_type_t") codec\_fmt
    :   Music format (optional)

<a id="_CPPv419audio_element_cfg_t"></a>

<a id="_CPPv319audio_element_cfg_t"></a> <a id="_CPPv219audio_element_cfg_t"></a> <a id="audio_element_cfg_t"></a> <a id="structaudio__element__cfg__t"></a> struct audio\_element\_cfg\_t
:   Audio Element configurations. Each Element at startup will be a self-running task. These tasks will execute the callback open -\> \[loop: read -\> process -\> write\] -\> close. These callback functions are provided by the user corresponding to this configuration.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19audio_element_cfg_t4openE"></a>

    <a id="_CPPv3N19audio_element_cfg_t4openE"></a> <a id="_CPPv2N19audio_element_cfg_t4openE"></a> <a id="audio_element_cfg_t::open__el_io_func"></a> <a id="structaudio__element__cfg__t_1a49c984ab88c930ba11e10bd6997efe33"></a> [el\_io\_func](#_CPPv410el_io_func "el_io_func") open
    :   Open callback function

    <a id="_CPPv4N19audio_element_cfg_t4seekE"></a>

    <a id="_CPPv3N19audio_element_cfg_t4seekE"></a> <a id="_CPPv2N19audio_element_cfg_t4seekE"></a> <a id="audio_element_cfg_t::seek__ctrl_func"></a> <a id="structaudio__element__cfg__t_1a9990c579aee319af474d42ded8fa58bc"></a> [ctrl\_func](#_CPPv49ctrl_func "ctrl_func") seek
    :   Seek callback function

    <a id="_CPPv4N19audio_element_cfg_t7processE"></a>

    <a id="_CPPv3N19audio_element_cfg_t7processE"></a> <a id="_CPPv2N19audio_element_cfg_t7processE"></a> <a id="audio_element_cfg_t::process__process_func"></a> <a id="structaudio__element__cfg__t_1a80be675c488535f6e6d1ce478eaef292"></a> [process\_func](#_CPPv412process_func "process_func") process
    :   Process callback function

    <a id="_CPPv4N19audio_element_cfg_t5closeE"></a>

    <a id="_CPPv3N19audio_element_cfg_t5closeE"></a> <a id="_CPPv2N19audio_element_cfg_t5closeE"></a> <a id="audio_element_cfg_t::close__el_io_func"></a> <a id="structaudio__element__cfg__t_1a3a8a908a333cd63d7d100bbc07d92c78"></a> [el\_io\_func](#_CPPv410el_io_func "el_io_func") close
    :   Close callback function

    <a id="_CPPv4N19audio_element_cfg_t7destroyE"></a>

    <a id="_CPPv3N19audio_element_cfg_t7destroyE"></a> <a id="_CPPv2N19audio_element_cfg_t7destroyE"></a> <a id="audio_element_cfg_t::destroy__el_io_func"></a> <a id="structaudio__element__cfg__t_1ae5a38b303215f33825d5cb68a4e33933"></a> [el\_io\_func](#_CPPv410el_io_func "el_io_func") destroy
    :   Destroy callback function

    <a id="_CPPv4N19audio_element_cfg_t4readE"></a>

    <a id="_CPPv3N19audio_element_cfg_t4readE"></a> <a id="_CPPv2N19audio_element_cfg_t4readE"></a> <a id="audio_element_cfg_t::read__port_stream_func"></a> <a id="structaudio__element__cfg__t_1a7215884d44f2092a93d72a4217efade7"></a> [port\_stream\_func](audio_port.md#_CPPv416port_stream_func "port_stream_func") read
    :   Read callback function

    <a id="_CPPv4N19audio_element_cfg_t5writeE"></a>

    <a id="_CPPv3N19audio_element_cfg_t5writeE"></a> <a id="_CPPv2N19audio_element_cfg_t5writeE"></a> <a id="audio_element_cfg_t::write__port_stream_func"></a> <a id="structaudio__element__cfg__t_1a55937f68fd7546b5ce3d7a854865893e"></a> [port\_stream\_func](audio_port.md#_CPPv416port_stream_func "port_stream_func") write
    :   Write callback function

    <a id="_CPPv4N19audio_element_cfg_t10buffer_lenE"></a>

    <a id="_CPPv3N19audio_element_cfg_t10buffer_lenE"></a> <a id="_CPPv2N19audio_element_cfg_t10buffer_lenE"></a> <a id="audio_element_cfg_t::buffer_len__i"></a> <a id="structaudio__element__cfg__t_1a2a6fd89c7de9d9c7d7d7595471b3c3b2"></a> int buffer\_len
    :   Buffer length use for an Element

    <a id="_CPPv4N19audio_element_cfg_t10task_stackE"></a>

    <a id="_CPPv3N19audio_element_cfg_t10task_stackE"></a> <a id="_CPPv2N19audio_element_cfg_t10task_stackE"></a> <a id="audio_element_cfg_t::task_stack__i"></a> <a id="structaudio__element__cfg__t_1a2b547f4e1687bbff0287e0cd4777b568"></a> int task\_stack
    :   Element task stack

    <a id="_CPPv4N19audio_element_cfg_t9task_prioE"></a>

    <a id="_CPPv3N19audio_element_cfg_t9task_prioE"></a> <a id="_CPPv2N19audio_element_cfg_t9task_prioE"></a> <a id="audio_element_cfg_t::task_prio__i"></a> <a id="structaudio__element__cfg__t_1a23922b38f48c7e19d1a711299222a5a2"></a> int task\_prio
    :   Element task priority (based on freeRTOS priority)

    <a id="_CPPv4N19audio_element_cfg_t9task_coreE"></a>

    <a id="_CPPv3N19audio_element_cfg_t9task_coreE"></a> <a id="_CPPv2N19audio_element_cfg_t9task_coreE"></a> <a id="audio_element_cfg_t::task_core__i"></a> <a id="structaudio__element__cfg__t_1a8c0f29eca058fc05b3571099fa54773b"></a> int task\_core
    :   Element task running in core (0 or 1\)

    <a id="_CPPv4N19audio_element_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N19audio_element_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N19audio_element_cfg_t14out_block_sizeE"></a> <a id="audio_element_cfg_t::out_block_size__i"></a> <a id="structaudio__element__cfg__t_1a68a89d7a1bf4dd69d7b820c743539605"></a> int out\_block\_size
    :   Output block size

    <a id="_CPPv4N19audio_element_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N19audio_element_cfg_t13out_block_numE"></a> <a id="_CPPv2N19audio_element_cfg_t13out_block_numE"></a> <a id="audio_element_cfg_t::out_block_num__i"></a> <a id="structaudio__element__cfg__t_1abd2af415d1372f5467184d1f6282c8f7"></a> int out\_block\_num
    :   Output block numbers

    <a id="_CPPv4N19audio_element_cfg_t4dataE"></a>

    <a id="_CPPv3N19audio_element_cfg_t4dataE"></a> <a id="_CPPv2N19audio_element_cfg_t4dataE"></a> <a id="audio_element_cfg_t::data__voidP"></a> <a id="structaudio__element__cfg__t_1a85062f80d6991e3dcab5a5dbfbddbf84"></a> void \*data
    :   User context

    <a id="_CPPv4N19audio_element_cfg_t3tagE"></a>

    <a id="_CPPv3N19audio_element_cfg_t3tagE"></a> <a id="_CPPv2N19audio_element_cfg_t3tagE"></a> <a id="audio_element_cfg_t::tag__cCP"></a> <a id="structaudio__element__cfg__t_1a7caf2e51b245cc4eeab4f8893a0cf397"></a> const char \*tag
    :   Element tag

    <a id="_CPPv4N19audio_element_cfg_t17multi_in_port_numE"></a>

    <a id="_CPPv3N19audio_element_cfg_t17multi_in_port_numE"></a> <a id="_CPPv2N19audio_element_cfg_t17multi_in_port_numE"></a> <a id="audio_element_cfg_t::multi_in_port_num__i"></a> <a id="structaudio__element__cfg__t_1a340674f566a34fc225ed2c2b26de9ef8"></a> int multi\_in\_port\_num
    :   The number of multiple input audio port

    <a id="_CPPv4N19audio_element_cfg_t18multi_out_port_numE"></a>

    <a id="_CPPv3N19audio_element_cfg_t18multi_out_port_numE"></a> <a id="_CPPv2N19audio_element_cfg_t18multi_out_port_numE"></a> <a id="audio_element_cfg_t::multi_out_port_num__i"></a> <a id="structaudio__element__cfg__t_1a54fb34a0ae55f505612a5f549ff3003a"></a> int multi\_out\_port\_num
    :   The number of multiple output audio port

    <a id="_CPPv4N19audio_element_cfg_t7in_typeE"></a>

    <a id="_CPPv3N19audio_element_cfg_t7in_typeE"></a> <a id="_CPPv2N19audio_element_cfg_t7in_typeE"></a> <a id="audio_element_cfg_t::in_type__port_type_t"></a> <a id="structaudio__element__cfg__t_1acde6a9113064ab54e8c501b6ce3e267e"></a> [port\_type\_t](audio_port.md#_CPPv411port_type_t "port_type_t") in\_type
    :   The type of input audio port

    <a id="_CPPv4N19audio_element_cfg_t8out_typeE"></a>

    <a id="_CPPv3N19audio_element_cfg_t8out_typeE"></a> <a id="_CPPv2N19audio_element_cfg_t8out_typeE"></a> <a id="audio_element_cfg_t::out_type__port_type_t"></a> <a id="structaudio__element__cfg__t_1a742378afc55c8002f3bc4d812b722d86"></a> [port\_type\_t](audio_port.md#_CPPv411port_type_t "port_type_t") out\_type
    :   The type of output audio port

<a id="macros"></a>

### Macros

<a id="c.AUDIO_ELEMENT_INFO_DEFAULT"></a>

<a id="audio__element_8h_1a907908d72e94ab2057cd4dbe3779bb08"></a> AUDIO\_ELEMENT\_INFO\_DEFAULT()

<a id="c.DEFAULT_ELEMENT_FRAMEBUF_SIZE"></a>

<a id="audio__element_8h_1a1cd807efa162cbe2b192a2f20acd07d3"></a> DEFAULT\_ELEMENT\_FRAMEBUF\_SIZE

<a id="c.DEFAULT_ELEMENT_FRAMEBUF_NUM"></a>

<a id="audio__element_8h_1acaf7697317f2aea8e6658aea80b32639"></a> DEFAULT\_ELEMENT\_FRAMEBUF\_NUM

<a id="c.DEFAULT_ELEMENT_RINGBUF_SIZE"></a>

<a id="audio__element_8h_1a4c71b530590e6d796e1b66707635b144"></a> DEFAULT\_ELEMENT\_RINGBUF\_SIZE

<a id="c.DEFAULT_ELEMENT_BUFFER_LENGTH"></a>

<a id="audio__element_8h_1a16a344d79d3c0db589744591786ac022"></a> DEFAULT\_ELEMENT\_BUFFER\_LENGTH

<a id="c.DEFAULT_ELEMENT_STACK_SIZE"></a>

<a id="audio__element_8h_1a424dcfa53c3d0966cb89a8d8e7a30a3e"></a> DEFAULT\_ELEMENT\_STACK\_SIZE

<a id="c.DEFAULT_ELEMENT_TASK_PRIO"></a>

<a id="audio__element_8h_1aea5c3724a404fa54a45f89ab77be8eba"></a> DEFAULT\_ELEMENT\_TASK\_PRIO

<a id="c.DEFAULT_ELEMENT_TASK_CORE"></a>

<a id="audio__element_8h_1a68d37173745a9e0d2ebf9b7236e7d422"></a> DEFAULT\_ELEMENT\_TASK\_CORE

<a id="c.DEFAULT_AUDIO_ELEMENT_CONFIG"></a>

<a id="audio__element_8h_1a53424c774bc44d7e39bd2f60a49d1296"></a> DEFAULT\_AUDIO\_ELEMENT\_CONFIG()

<a id="c.AUDIO_ELEMENT_OBS_BEGIN"></a>

<a id="audio__element_8h_1a25624b0860eab1934a2d1dbd95054ca3"></a> AUDIO\_ELEMENT\_OBS\_BEGIN(el)

<a id="c.AUDIO_ELEMENT_OBS_END"></a>

<a id="audio__element_8h_1abfd2a6137afb3128144d0f57467c95b7"></a> AUDIO\_ELEMENT\_OBS\_END(el, ret, frame\_size)

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv422audio_element_handle_t"></a>

<a id="_CPPv322audio_element_handle_t"></a> <a id="_CPPv222audio_element_handle_t"></a> <a id="audio_element_handle_t"></a> <a id="audio__element_8h_1a218b540a03fc367d453e38e939ee588a"></a> typedef struct audio\_element \*audio\_element\_handle\_t

<a id="_CPPv410el_io_func"></a>

<a id="_CPPv310el_io_func"></a> <a id="_CPPv210el_io_func"></a> <a id="el_io_func"></a> <a id="audio__element_8h_1a8642ebe3b6adf844fc44d288ab189459"></a> typedef [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*el\_io\_func)([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") self)

<a id="_CPPv412process_func"></a>

<a id="_CPPv312process_func"></a> <a id="_CPPv212process_func"></a> <a id="process_func"></a> <a id="audio__element_8h_1a51f3587eecebb990e8aac74b25db52dd"></a> typedef int (\*process\_func)([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") self, char \*el\_buffer, int el\_buf\_len)

<a id="_CPPv413event_cb_func"></a>

<a id="_CPPv313event_cb_func"></a> <a id="_CPPv213event_cb_func"></a> <a id="event_cb_func"></a> <a id="audio__element_8h_1af7dffecdc4f6c5c09d52dd135a3317ee"></a> typedef [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*event\_cb\_func)([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") el, [audio\_event\_iface\_msg\_t](audio_event_iface.md#_CPPv423audio_event_iface_msg_t "audio_event_iface_msg_t") \*event, void \*ctx)

<a id="_CPPv49ctrl_func"></a>

<a id="_CPPv39ctrl_func"></a> <a id="_CPPv29ctrl_func"></a> <a id="ctrl_func"></a> <a id="audio__element_8h_1a1660dd4321f003a831e07fcd2ec6334f"></a> typedef [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*ctrl\_func)([audio\_element\_handle\_t](#_CPPv422audio_element_handle_t "audio_element_handle_t") self, void \*in\_data, int in\_size, void \*out\_data, int \*out\_size)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv419audio_element_err_t"></a>

<a id="_CPPv319audio_element_err_t"></a> <a id="_CPPv219audio_element_err_t"></a> <a id="audio__element_8h_1ac19df25e390d7ec39430f878c3095760"></a> enum audio\_element\_err\_t
:   *Values:*

    <a id="_CPPv4N19audio_element_err_t9AEL_IO_OKE"></a>

    <a id="_CPPv3N19audio_element_err_t9AEL_IO_OKE"></a> <a id="_CPPv2N19audio_element_err_t9AEL_IO_OKE"></a> <a id="audio__element_8h_1ac19df25e390d7ec39430f878c3095760a2bd73dc6905ac919d80c7e7b296d3863"></a> enumerator AEL\_IO\_OK

    <a id="_CPPv4N19audio_element_err_t11AEL_IO_FAILE"></a>

    <a id="_CPPv3N19audio_element_err_t11AEL_IO_FAILE"></a> <a id="_CPPv2N19audio_element_err_t11AEL_IO_FAILE"></a> <a id="audio__element_8h_1ac19df25e390d7ec39430f878c3095760ab297fc083a349ad42ea734997d490d6b"></a> enumerator AEL\_IO\_FAIL

    <a id="_CPPv4N19audio_element_err_t11AEL_IO_DONEE"></a>

    <a id="_CPPv3N19audio_element_err_t11AEL_IO_DONEE"></a> <a id="_CPPv2N19audio_element_err_t11AEL_IO_DONEE"></a> <a id="audio__element_8h_1ac19df25e390d7ec39430f878c3095760aa9f3a7c28a452a5fb0d12c1a5aa3a372"></a> enumerator AEL\_IO\_DONE

    <a id="_CPPv4N19audio_element_err_t12AEL_IO_ABORTE"></a>

    <a id="_CPPv3N19audio_element_err_t12AEL_IO_ABORTE"></a> <a id="_CPPv2N19audio_element_err_t12AEL_IO_ABORTE"></a> <a id="audio__element_8h_1ac19df25e390d7ec39430f878c3095760abf705e9076089ce5b2f40f4d007c9abc"></a> enumerator AEL\_IO\_ABORT

    <a id="_CPPv4N19audio_element_err_t14AEL_IO_TIMEOUTE"></a>

    <a id="_CPPv3N19audio_element_err_t14AEL_IO_TIMEOUTE"></a> <a id="_CPPv2N19audio_element_err_t14AEL_IO_TIMEOUTE"></a> <a id="audio__element_8h_1ac19df25e390d7ec39430f878c3095760a16832c044b1123de4fb838081117f6af"></a> enumerator AEL\_IO\_TIMEOUT

    <a id="_CPPv4N19audio_element_err_t16AEL_PROCESS_FAILE"></a>

    <a id="_CPPv3N19audio_element_err_t16AEL_PROCESS_FAILE"></a> <a id="_CPPv2N19audio_element_err_t16AEL_PROCESS_FAILE"></a> <a id="audio__element_8h_1ac19df25e390d7ec39430f878c3095760a4cbcf5a591874aba05f3e658e2ce1b13"></a> enumerator AEL\_PROCESS\_FAIL

<a id="_CPPv421audio_element_state_t"></a>

<a id="_CPPv321audio_element_state_t"></a> <a id="_CPPv221audio_element_state_t"></a> <a id="audio__element_8h_1addd4ddfd855c0bfc262ceb744f8a24cb"></a> enum audio\_element\_state\_t
:   Audio element state.

    *Values:*

    <a id="_CPPv4N21audio_element_state_t14AEL_STATE_NONEE"></a>

    <a id="_CPPv3N21audio_element_state_t14AEL_STATE_NONEE"></a> <a id="_CPPv2N21audio_element_state_t14AEL_STATE_NONEE"></a> <a id="audio__element_8h_1addd4ddfd855c0bfc262ceb744f8a24cba6952895ac2f150f6b829c831e241fe26"></a> enumerator AEL\_STATE\_NONE

    <a id="_CPPv4N21audio_element_state_t14AEL_STATE_INITE"></a>

    <a id="_CPPv3N21audio_element_state_t14AEL_STATE_INITE"></a> <a id="_CPPv2N21audio_element_state_t14AEL_STATE_INITE"></a> <a id="audio__element_8h_1addd4ddfd855c0bfc262ceb744f8a24cba60bb573ebe8eb0f8a433a7410eea209f"></a> enumerator AEL\_STATE\_INIT

    <a id="_CPPv4N21audio_element_state_t22AEL_STATE_INITIALIZINGE"></a>

    <a id="_CPPv3N21audio_element_state_t22AEL_STATE_INITIALIZINGE"></a> <a id="_CPPv2N21audio_element_state_t22AEL_STATE_INITIALIZINGE"></a> <a id="audio__element_8h_1addd4ddfd855c0bfc262ceb744f8a24cba04bfc559c15d95752423c8f437716d37"></a> enumerator AEL\_STATE\_INITIALIZING

    <a id="_CPPv4N21audio_element_state_t17AEL_STATE_RUNNINGE"></a>

    <a id="_CPPv3N21audio_element_state_t17AEL_STATE_RUNNINGE"></a> <a id="_CPPv2N21audio_element_state_t17AEL_STATE_RUNNINGE"></a> <a id="audio__element_8h_1addd4ddfd855c0bfc262ceb744f8a24cbaa7e4ec732460cb818f1ff74563b765bd"></a> enumerator AEL\_STATE\_RUNNING

    <a id="_CPPv4N21audio_element_state_t16AEL_STATE_PAUSEDE"></a>

    <a id="_CPPv3N21audio_element_state_t16AEL_STATE_PAUSEDE"></a> <a id="_CPPv2N21audio_element_state_t16AEL_STATE_PAUSEDE"></a> <a id="audio__element_8h_1addd4ddfd855c0bfc262ceb744f8a24cba8c5f8babdb16f82d9865699eff5402da"></a> enumerator AEL\_STATE\_PAUSED

    <a id="_CPPv4N21audio_element_state_t17AEL_STATE_STOPPEDE"></a>

    <a id="_CPPv3N21audio_element_state_t17AEL_STATE_STOPPEDE"></a> <a id="_CPPv2N21audio_element_state_t17AEL_STATE_STOPPEDE"></a> <a id="audio__element_8h_1addd4ddfd855c0bfc262ceb744f8a24cba4ca4aaeea714386cc06fa13c04cbc4e7"></a> enumerator AEL\_STATE\_STOPPED

    <a id="_CPPv4N21audio_element_state_t18AEL_STATE_FINISHEDE"></a>

    <a id="_CPPv3N21audio_element_state_t18AEL_STATE_FINISHEDE"></a> <a id="_CPPv2N21audio_element_state_t18AEL_STATE_FINISHEDE"></a> <a id="audio__element_8h_1addd4ddfd855c0bfc262ceb744f8a24cbab5f01883b0aaa2a68a3a95bfba51538e"></a> enumerator AEL\_STATE\_FINISHED

    <a id="_CPPv4N21audio_element_state_t15AEL_STATE_ERRORE"></a>

    <a id="_CPPv3N21audio_element_state_t15AEL_STATE_ERRORE"></a> <a id="_CPPv2N21audio_element_state_t15AEL_STATE_ERRORE"></a> <a id="audio__element_8h_1addd4ddfd855c0bfc262ceb744f8a24cba51de61e79f1ff175aad5ff9df6daf699"></a> enumerator AEL\_STATE\_ERROR

<a id="_CPPv423audio_element_msg_cmd_t"></a>

<a id="_CPPv323audio_element_msg_cmd_t"></a> <a id="_CPPv223audio_element_msg_cmd_t"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9f"></a> enum audio\_element\_msg\_cmd\_t
:   Audio element action command, process on dispatcher

    *Values:*

    <a id="_CPPv4N23audio_element_msg_cmd_t16AEL_MSG_CMD_NONEE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t16AEL_MSG_CMD_NONEE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t16AEL_MSG_CMD_NONEE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9fafbed18a17abc03691dbafe7b6744aa8a"></a> enumerator AEL\_MSG\_CMD\_NONE

    <a id="_CPPv4N23audio_element_msg_cmd_t18AEL_MSG_CMD_FINISHE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t18AEL_MSG_CMD_FINISHE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t18AEL_MSG_CMD_FINISHE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9fa13bf2609b8ea5d008ec47f1972756cdd"></a> enumerator AEL\_MSG\_CMD\_FINISH

    <a id="_CPPv4N23audio_element_msg_cmd_t16AEL_MSG_CMD_STOPE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t16AEL_MSG_CMD_STOPE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t16AEL_MSG_CMD_STOPE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9fa49d7c909061e9441d0f04e5a8d35c5c0"></a> enumerator AEL\_MSG\_CMD\_STOP

    <a id="_CPPv4N23audio_element_msg_cmd_t17AEL_MSG_CMD_PAUSEE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t17AEL_MSG_CMD_PAUSEE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t17AEL_MSG_CMD_PAUSEE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9faa57c2464380c80c262fd87c5fd33741e"></a> enumerator AEL\_MSG\_CMD\_PAUSE

    <a id="_CPPv4N23audio_element_msg_cmd_t18AEL_MSG_CMD_RESUMEE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t18AEL_MSG_CMD_RESUMEE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t18AEL_MSG_CMD_RESUMEE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9fa25e2ccbb0ffad6c27be3d601faeb233a"></a> enumerator AEL\_MSG\_CMD\_RESUME

    <a id="_CPPv4N23audio_element_msg_cmd_t19AEL_MSG_CMD_DESTROYE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t19AEL_MSG_CMD_DESTROYE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t19AEL_MSG_CMD_DESTROYE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9fa13b0ccc23d4bcaa1b1df4859f75e1ebe"></a> enumerator AEL\_MSG\_CMD\_DESTROY

    <a id="_CPPv4N23audio_element_msg_cmd_t25AEL_MSG_CMD_REPORT_STATUSE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t25AEL_MSG_CMD_REPORT_STATUSE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t25AEL_MSG_CMD_REPORT_STATUSE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9fa6ff819e53918fa161f50b612f0cef410"></a> enumerator AEL\_MSG\_CMD\_REPORT\_STATUS

    <a id="_CPPv4N23audio_element_msg_cmd_t29AEL_MSG_CMD_REPORT_MUSIC_INFOE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t29AEL_MSG_CMD_REPORT_MUSIC_INFOE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t29AEL_MSG_CMD_REPORT_MUSIC_INFOE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9fad1097dfac1500cf61076b9170a7fae3c"></a> enumerator AEL\_MSG\_CMD\_REPORT\_MUSIC\_INFO

    <a id="_CPPv4N23audio_element_msg_cmd_t28AEL_MSG_CMD_REPORT_CODEC_FMTE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t28AEL_MSG_CMD_REPORT_CODEC_FMTE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t28AEL_MSG_CMD_REPORT_CODEC_FMTE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9fa9f0616a3b0d24f3943bae555a6298b35"></a> enumerator AEL\_MSG\_CMD\_REPORT\_CODEC\_FMT

    <a id="_CPPv4N23audio_element_msg_cmd_t27AEL_MSG_CMD_REPORT_POSITIONE"></a>

    <a id="_CPPv3N23audio_element_msg_cmd_t27AEL_MSG_CMD_REPORT_POSITIONE"></a> <a id="_CPPv2N23audio_element_msg_cmd_t27AEL_MSG_CMD_REPORT_POSITIONE"></a> <a id="audio__element_8h_1a92e08c79b0cb1de38c99389794384b9fa393f95c6c14667e519ea66b2cb50fcef"></a> enumerator AEL\_MSG\_CMD\_REPORT\_POSITION

<a id="_CPPv422audio_element_status_t"></a>

<a id="_CPPv322audio_element_status_t"></a> <a id="_CPPv222audio_element_status_t"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690"></a> enum audio\_element\_status\_t
:   Audio element status report

    *Values:*

    <a id="_CPPv4N22audio_element_status_t15AEL_STATUS_NONEE"></a>

    <a id="_CPPv3N22audio_element_status_t15AEL_STATUS_NONEE"></a> <a id="_CPPv2N22audio_element_status_t15AEL_STATUS_NONEE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690ae2da2423c934c2b3fe9411edf5e6f7f6"></a> enumerator AEL\_STATUS\_NONE

    <a id="_CPPv4N22audio_element_status_t21AEL_STATUS_ERROR_OPENE"></a>

    <a id="_CPPv3N22audio_element_status_t21AEL_STATUS_ERROR_OPENE"></a> <a id="_CPPv2N22audio_element_status_t21AEL_STATUS_ERROR_OPENE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690ace01676223546b72fb2130eab0018499"></a> enumerator AEL\_STATUS\_ERROR\_OPEN

    <a id="_CPPv4N22audio_element_status_t22AEL_STATUS_ERROR_INPUTE"></a>

    <a id="_CPPv3N22audio_element_status_t22AEL_STATUS_ERROR_INPUTE"></a> <a id="_CPPv2N22audio_element_status_t22AEL_STATUS_ERROR_INPUTE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690a32d0a33418feaa84714f7aa86966e2ca"></a> enumerator AEL\_STATUS\_ERROR\_INPUT

    <a id="_CPPv4N22audio_element_status_t24AEL_STATUS_ERROR_PROCESSE"></a>

    <a id="_CPPv3N22audio_element_status_t24AEL_STATUS_ERROR_PROCESSE"></a> <a id="_CPPv2N22audio_element_status_t24AEL_STATUS_ERROR_PROCESSE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690a4a9740f82985d673dc71bdb0d7ce0ec2"></a> enumerator AEL\_STATUS\_ERROR\_PROCESS

    <a id="_CPPv4N22audio_element_status_t23AEL_STATUS_ERROR_OUTPUTE"></a>

    <a id="_CPPv3N22audio_element_status_t23AEL_STATUS_ERROR_OUTPUTE"></a> <a id="_CPPv2N22audio_element_status_t23AEL_STATUS_ERROR_OUTPUTE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690af02949a970a32a97d4579bfe87f93eff"></a> enumerator AEL\_STATUS\_ERROR\_OUTPUT

    <a id="_CPPv4N22audio_element_status_t22AEL_STATUS_ERROR_CLOSEE"></a>

    <a id="_CPPv3N22audio_element_status_t22AEL_STATUS_ERROR_CLOSEE"></a> <a id="_CPPv2N22audio_element_status_t22AEL_STATUS_ERROR_CLOSEE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690ad1a2a052884cfbe57abc58e5fb3128fe"></a> enumerator AEL\_STATUS\_ERROR\_CLOSE

    <a id="_CPPv4N22audio_element_status_t24AEL_STATUS_ERROR_TIMEOUTE"></a>

    <a id="_CPPv3N22audio_element_status_t24AEL_STATUS_ERROR_TIMEOUTE"></a> <a id="_CPPv2N22audio_element_status_t24AEL_STATUS_ERROR_TIMEOUTE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690aebd9d0298a8cb69cb0c335252affbda7"></a> enumerator AEL\_STATUS\_ERROR\_TIMEOUT

    <a id="_CPPv4N22audio_element_status_t24AEL_STATUS_ERROR_UNKNOWNE"></a>

    <a id="_CPPv3N22audio_element_status_t24AEL_STATUS_ERROR_UNKNOWNE"></a> <a id="_CPPv2N22audio_element_status_t24AEL_STATUS_ERROR_UNKNOWNE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690a5fee3aa451d80359b4a839d4defe9d87"></a> enumerator AEL\_STATUS\_ERROR\_UNKNOWN

    <a id="_CPPv4N22audio_element_status_t21AEL_STATUS_INPUT_DONEE"></a>

    <a id="_CPPv3N22audio_element_status_t21AEL_STATUS_INPUT_DONEE"></a> <a id="_CPPv2N22audio_element_status_t21AEL_STATUS_INPUT_DONEE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690a4aad5e189d7cd896759571a34e5585c0"></a> enumerator AEL\_STATUS\_INPUT\_DONE

    <a id="_CPPv4N22audio_element_status_t26AEL_STATUS_INPUT_BUFFERINGE"></a>

    <a id="_CPPv3N22audio_element_status_t26AEL_STATUS_INPUT_BUFFERINGE"></a> <a id="_CPPv2N22audio_element_status_t26AEL_STATUS_INPUT_BUFFERINGE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690a8fcc4465e8b7cd8b2ca15531148939ee"></a> enumerator AEL\_STATUS\_INPUT\_BUFFERING

    <a id="_CPPv4N22audio_element_status_t22AEL_STATUS_OUTPUT_DONEE"></a>

    <a id="_CPPv3N22audio_element_status_t22AEL_STATUS_OUTPUT_DONEE"></a> <a id="_CPPv2N22audio_element_status_t22AEL_STATUS_OUTPUT_DONEE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690a65705f8fcd5046db2863e2ddb08f6db4"></a> enumerator AEL\_STATUS\_OUTPUT\_DONE

    <a id="_CPPv4N22audio_element_status_t27AEL_STATUS_OUTPUT_BUFFERINGE"></a>

    <a id="_CPPv3N22audio_element_status_t27AEL_STATUS_OUTPUT_BUFFERINGE"></a> <a id="_CPPv2N22audio_element_status_t27AEL_STATUS_OUTPUT_BUFFERINGE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690af563b82aedc3789705d003abd24149e8"></a> enumerator AEL\_STATUS\_OUTPUT\_BUFFERING

    <a id="_CPPv4N22audio_element_status_t24AEL_STATUS_STATE_RUNNINGE"></a>

    <a id="_CPPv3N22audio_element_status_t24AEL_STATUS_STATE_RUNNINGE"></a> <a id="_CPPv2N22audio_element_status_t24AEL_STATUS_STATE_RUNNINGE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690a199f7aeeedc426307250714cc15f5a87"></a> enumerator AEL\_STATUS\_STATE\_RUNNING

    <a id="_CPPv4N22audio_element_status_t23AEL_STATUS_STATE_PAUSEDE"></a>

    <a id="_CPPv3N22audio_element_status_t23AEL_STATUS_STATE_PAUSEDE"></a> <a id="_CPPv2N22audio_element_status_t23AEL_STATUS_STATE_PAUSEDE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690abb4257fb63813953df83a1f0e84318ea"></a> enumerator AEL\_STATUS\_STATE\_PAUSED

    <a id="_CPPv4N22audio_element_status_t24AEL_STATUS_STATE_STOPPEDE"></a>

    <a id="_CPPv3N22audio_element_status_t24AEL_STATUS_STATE_STOPPEDE"></a> <a id="_CPPv2N22audio_element_status_t24AEL_STATUS_STATE_STOPPEDE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690aae9916a40f6b93d2bb1cf41bc6316484"></a> enumerator AEL\_STATUS\_STATE\_STOPPED

    <a id="_CPPv4N22audio_element_status_t25AEL_STATUS_STATE_FINISHEDE"></a>

    <a id="_CPPv3N22audio_element_status_t25AEL_STATUS_STATE_FINISHEDE"></a> <a id="_CPPv2N22audio_element_status_t25AEL_STATUS_STATE_FINISHEDE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690acefa911ef6d638010e4f7d567155740f"></a> enumerator AEL\_STATUS\_STATE\_FINISHED

    <a id="_CPPv4N22audio_element_status_t18AEL_STATUS_MOUNTEDE"></a>

    <a id="_CPPv3N22audio_element_status_t18AEL_STATUS_MOUNTEDE"></a> <a id="_CPPv2N22audio_element_status_t18AEL_STATUS_MOUNTEDE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690a62c65c26ac94007365b9e794d715ae11"></a> enumerator AEL\_STATUS\_MOUNTED

    <a id="_CPPv4N22audio_element_status_t20AEL_STATUS_UNMOUNTEDE"></a>

    <a id="_CPPv3N22audio_element_status_t20AEL_STATUS_UNMOUNTEDE"></a> <a id="_CPPv2N22audio_element_status_t20AEL_STATUS_UNMOUNTEDE"></a> <a id="audio__element_8h_1a9b9cf68b7e82bd6a5238affa4b1a0690a1d6f6abee33b6fa08425e6638c2fb9af"></a> enumerator AEL\_STATUS\_UNMOUNTED
