---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_pipeline/audio_pipeline.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="audio-pipeline"></a>

# Audio Pipeline

Audio Pipeline is used to manage audio pipeline.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [audio\_pipeline.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_pipeline/audio_pipeline.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419audio_pipeline_initP20audio_pipeline_cfg_t"></a>

<a id="_CPPv319audio_pipeline_initP20audio_pipeline_cfg_t"></a> <a id="_CPPv219audio_pipeline_initP20audio_pipeline_cfg_t"></a> <a id="audio_pipeline_init__audio_pipeline_cfg_tP"></a> <a id="audio__pipeline_8h_1a62b7aab96fde12fb24119b87001c636a"></a> [audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") audio\_pipeline\_init([audio\_pipeline\_cfg\_t](#_CPPv420audio_pipeline_cfg_t "audio_pipeline_cfg_t") \*config)
:   Initialize audio\_pipeline\_handle\_t object audio\_pipeline is responsible for controlling the audio data stream and connecting the audio elements with the ringbuffer It will connect and start the audio element in order, responsible for retrieving the data from the previous element and passing it to the element after it. Also get events from each element, process events or pass it to a higher layer.

    参数
    :   **config** – The configuration \- audio\_pipeline\_cfg\_t

    返回
    :   - audio\_pipeline\_handle\_t on success
        - NULL when any errors

<a id="_CPPv421audio_pipeline_deinit23audio_pipeline_handle_t"></a>

<a id="_CPPv321audio_pipeline_deinit23audio_pipeline_handle_t"></a> <a id="_CPPv221audio_pipeline_deinit23audio_pipeline_handle_t"></a> <a id="audio_pipeline_deinit__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1aaa3360abdaa7ca381e159f05cb18c2ed"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_deinit([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   This function removes all of the element’s links in audio\_pipeline, cancels the registration of all events, invokes the destroy functions of the registered elements, and frees the memory allocated by the init function. Briefly, frees all memory.

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   BK\_OK

<a id="_CPPv423audio_pipeline_register23audio_pipeline_handle_t22audio_element_handle_tPKc"></a>

<a id="_CPPv323audio_pipeline_register23audio_pipeline_handle_t22audio_element_handle_tPKc"></a> <a id="_CPPv223audio_pipeline_register23audio_pipeline_handle_t22audio_element_handle_tPKc"></a> <a id="audio_pipeline_register__audio_pipeline_handle_t.audio_element_handle_t.cCP"></a> <a id="audio__pipeline_8h_1a1a3868f2eb14893f8e186dd50cffeb14"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_register([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline, [audio\_element\_handle\_t](audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") el, const char \*name)
:   Registering an element for audio\_pipeline, each element can be registered multiple times, but `name` (as String) must be unique in audio\_pipeline, which is used to identify the element for link creation mentioned in the `audio_pipeline_link`

    备注

    Because of stop pipeline or pause pipeline depend much on register order. Please register element strictly in the following order: input element first, process middle, output element last.

    参数
    :   - **pipeline** – **\[in\]** The Audio Pipeline Handle
        - **el** – **\[in\]** The Audio Element Handle
        - **name** – **\[in\]** The name identifier of the audio\_element in this audio\_pipeline

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv425audio_pipeline_unregister23audio_pipeline_handle_t22audio_element_handle_t"></a>

<a id="_CPPv325audio_pipeline_unregister23audio_pipeline_handle_t22audio_element_handle_t"></a> <a id="_CPPv225audio_pipeline_unregister23audio_pipeline_handle_t22audio_element_handle_t"></a> <a id="audio_pipeline_unregister__audio_pipeline_handle_t.audio_element_handle_t"></a> <a id="audio__pipeline_8h_1a303d62fcb0921b3772073507c077e432"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_unregister([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline, [audio\_element\_handle\_t](audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") el)
:   Unregister the audio\_element in audio\_pipeline, remove it from the list.

    参数
    :   - **pipeline** – **\[in\]** The Audio Pipeline Handle
        - **el** – **\[in\]** The Audio Element Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv418audio_pipeline_run23audio_pipeline_handle_t"></a>

<a id="_CPPv318audio_pipeline_run23audio_pipeline_handle_t"></a> <a id="_CPPv218audio_pipeline_run23audio_pipeline_handle_t"></a> <a id="audio_pipeline_run__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1ae952eb9e805b15e502b42d297490a2ff"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_run([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   Start Audio Pipeline.

    ```
          With this function audio_pipeline will create tasks for all elements,
          that have been linked using the linking functions.
    ```

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv424audio_pipeline_terminate23audio_pipeline_handle_t"></a>

<a id="_CPPv324audio_pipeline_terminate23audio_pipeline_handle_t"></a> <a id="_CPPv224audio_pipeline_terminate23audio_pipeline_handle_t"></a> <a id="audio_pipeline_terminate__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1a7582e4224466c7a74668fd1b0b5896e6"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_terminate([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   Stop Audio Pipeline.

    ```
          With this function audio_pipeline will destroy tasks of all elements,
          that have been linked using the linking functions.
    ```

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv421audio_pipeline_resume23audio_pipeline_handle_t"></a>

<a id="_CPPv321audio_pipeline_resume23audio_pipeline_handle_t"></a> <a id="_CPPv221audio_pipeline_resume23audio_pipeline_handle_t"></a> <a id="audio_pipeline_resume__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1aa3eee2032686f551d882bd4d4fafdc33"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_resume([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   This function will set all the elements to the `RUNNING` state and process the audio data as an inherent feature of audio\_pipeline.

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv420audio_pipeline_pause23audio_pipeline_handle_t"></a>

<a id="_CPPv320audio_pipeline_pause23audio_pipeline_handle_t"></a> <a id="_CPPv220audio_pipeline_pause23audio_pipeline_handle_t"></a> <a id="audio_pipeline_pause__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1a2bd49dc014feba938a04e29a4f12f486"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_pause([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   This function will set all the elements to the `PAUSED` state. Everything remains the same except the data processing is stopped.

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv419audio_pipeline_stop23audio_pipeline_handle_t"></a>

<a id="_CPPv319audio_pipeline_stop23audio_pipeline_handle_t"></a> <a id="_CPPv219audio_pipeline_stop23audio_pipeline_handle_t"></a> <a id="audio_pipeline_stop__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1a6f5671206ed52957bd1368629f4c2dd6"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_stop([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   Stop all of the linked elements. Used with `audio_pipeline_wait_for_stop` to keep in sync. The link state of the elements in the pipeline is kept, events are still registered. The stopped audio\_pipeline restart by `audio_pipeline_resume`.

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv428audio_pipeline_wait_for_stop23audio_pipeline_handle_t"></a>

<a id="_CPPv328audio_pipeline_wait_for_stop23audio_pipeline_handle_t"></a> <a id="_CPPv228audio_pipeline_wait_for_stop23audio_pipeline_handle_t"></a> <a id="audio_pipeline_wait_for_stop__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1ab0e01311a4e7382382b2412807190b81"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_wait\_for\_stop([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   The `audio_pipeline_stop` function sends requests to the elements and exits. But they need time to get rid of time-blocking tasks. This function will wait `portMAX_DELAY` until all the Elements in the pipeline actually stop.

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv419audio_pipeline_link23audio_pipeline_handle_tA_PKci"></a>

<a id="_CPPv319audio_pipeline_link23audio_pipeline_handle_tA_PKci"></a> <a id="_CPPv219audio_pipeline_link23audio_pipeline_handle_tA_PKci"></a> <a id="audio_pipeline_link__audio_pipeline_handle_t.cCPA.i"></a> <a id="audio__pipeline_8h_1aea5260ede1f21f637ab6a3d3c3205753"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_link([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline, const char \*link\_tag\[\], int link\_num)
:   The audio\_element added to audio\_pipeline will be unconnected before it is called by this function. Based on element’s `name` already registered by `audio_pipeline_register`, the path of the data will be linked in the order of the link\_tag. Element at index 0 is first, and index `link_num -1` is final. As well as audio\_pipeline will subscribe all element’s events.

    参数
    :   - **pipeline** – **\[in\]** The Audio Pipeline Handle
        - **link\_tag** – Array of element `name` was registered by `audio_pipeline_register`
        - **link\_num** – **\[in\]** Total number of elements of the `link_tag` array

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv421audio_pipeline_unlink23audio_pipeline_handle_t"></a>

<a id="_CPPv321audio_pipeline_unlink23audio_pipeline_handle_t"></a> <a id="_CPPv221audio_pipeline_unlink23audio_pipeline_handle_t"></a> <a id="audio_pipeline_unlink__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1a56377c0c4db488fbcd1f4759d7895612"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_unlink([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   Removes the connection of the elements, as well as unsubscribe events.

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv428audio_pipeline_get_el_by_tag23audio_pipeline_handle_tPKc"></a>

<a id="_CPPv328audio_pipeline_get_el_by_tag23audio_pipeline_handle_tPKc"></a> <a id="_CPPv228audio_pipeline_get_el_by_tag23audio_pipeline_handle_tPKc"></a> <a id="audio_pipeline_get_el_by_tag__audio_pipeline_handle_t.cCP"></a> <a id="audio__pipeline_8h_1a5255443578b6ab13dcd8c8c8c96ece6b"></a> [audio\_element\_handle\_t](audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") audio\_pipeline\_get\_el\_by\_tag([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline, const char \*tag)
:   Find un-kept element from registered pipeline by tag.

    参数
    :   - **pipeline** – **\[in\]** The Audio Pipeline Handle
        - **tag** – **\[in\]** A char pointer

    返回
    :   - NULL when any errors
        - Others on success

<a id="_CPPv430audio_pipeline_remove_listener23audio_pipeline_handle_t"></a>

<a id="_CPPv330audio_pipeline_remove_listener23audio_pipeline_handle_t"></a> <a id="_CPPv230audio_pipeline_remove_listener23audio_pipeline_handle_t"></a> <a id="audio_pipeline_remove_listener__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1afa430980c69135c960a127828bf153fd"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_remove\_listener([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   Remove event listener from this audio\_pipeline.

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv427audio_pipeline_set_listener23audio_pipeline_handle_t26audio_event_iface_handle_t"></a>

<a id="_CPPv327audio_pipeline_set_listener23audio_pipeline_handle_t26audio_event_iface_handle_t"></a> <a id="_CPPv227audio_pipeline_set_listener23audio_pipeline_handle_t26audio_event_iface_handle_t"></a> <a id="audio_pipeline_set_listener__audio_pipeline_handle_t.audio_event_iface_handle_t"></a> <a id="audio__pipeline_8h_1adf3992e4625e87005e1392994dcdf57b"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_set\_listener([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline, [audio\_event\_iface\_handle\_t](audio_event_iface.md#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") evt)
:   Set event listner for this audio\_pipeline, any event from this pipeline can be listen to by `evt`

    参数
    :   - **pipeline** – **\[in\]** The Audio Pipeline Handle
        - **evt** – **\[in\]** The Event Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv430audio_pipeline_get_event_iface23audio_pipeline_handle_t"></a>

<a id="_CPPv330audio_pipeline_get_event_iface23audio_pipeline_handle_t"></a> <a id="_CPPv230audio_pipeline_get_event_iface23audio_pipeline_handle_t"></a> <a id="audio_pipeline_get_event_iface__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1ac5a6fd5191e7704a9e560767a48da8f4"></a> [audio\_event\_iface\_handle\_t](audio_event_iface.md#_CPPv426audio_event_iface_handle_t "audio_event_iface_handle_t") audio\_pipeline\_get\_event\_iface([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   Get the event iface using by this pipeline.

    参数
    :   **pipeline** – **\[in\]** The pipeline

    返回
    :   The Event Handle

<a id="_CPPv432audio_pipeline_reset_items_state23audio_pipeline_handle_t"></a>

<a id="_CPPv332audio_pipeline_reset_items_state23audio_pipeline_handle_t"></a> <a id="_CPPv232audio_pipeline_reset_items_state23audio_pipeline_handle_t"></a> <a id="audio_pipeline_reset_items_state__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1ab4ab6f2112fefbea56cd86dcbb378589"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_reset\_items\_state([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   Reset pipeline element items state to `AEL_STATUS_NONE`

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv425audio_pipeline_reset_port23audio_pipeline_handle_t"></a>

<a id="_CPPv325audio_pipeline_reset_port23audio_pipeline_handle_t"></a> <a id="_CPPv225audio_pipeline_reset_port23audio_pipeline_handle_t"></a> <a id="audio_pipeline_reset_port__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1aa2c91ccb95c554eb5888163c8f95e198"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_reset\_port([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   Reset pipeline element port.

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv429audio_pipeline_reset_elements23audio_pipeline_handle_t"></a>

<a id="_CPPv329audio_pipeline_reset_elements23audio_pipeline_handle_t"></a> <a id="_CPPv229audio_pipeline_reset_elements23audio_pipeline_handle_t"></a> <a id="audio_pipeline_reset_elements__audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1a3f9fffb4f6369326a68e0ebd576c42c0"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_reset\_elements([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline)
:   Reset Pipeline linked elements state.

    参数
    :   **pipeline** – **\[in\]** The Audio Pipeline Handle

    返回
    :   - BK\_OK on success
        - BK\_FAIL when any errors

<a id="_CPPv427audio_pipeline_change_state23audio_pipeline_handle_t21audio_element_state_t"></a>

<a id="_CPPv327audio_pipeline_change_state23audio_pipeline_handle_t21audio_element_state_t"></a> <a id="_CPPv227audio_pipeline_change_state23audio_pipeline_handle_t21audio_element_state_t"></a> <a id="audio_pipeline_change_state__audio_pipeline_handle_t.audio_element_state_t"></a> <a id="audio__pipeline_8h_1a2bae0cc537ac6407ad42cb655819339a"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_pipeline\_change\_state([audio\_pipeline\_handle\_t](#_CPPv423audio_pipeline_handle_t "audio_pipeline_handle_t") pipeline, [audio\_element\_state\_t](audio_element.md#_CPPv421audio_element_state_t "audio_element_state_t") new\_state)
:   Set the pipeline state.

    参数
    :   - **pipeline** – **\[in\]** The Audio Pipeline Handle
        - **new\_state** – **\[in\]** The new state will be set

    返回
    :   - BK\_OK All linked elements state are same.
        - BK\_FAIL Error.

<a id="structures"></a>

### Structures

<a id="_CPPv418audio_pipeline_cfg"></a>

<a id="_CPPv318audio_pipeline_cfg"></a> <a id="_CPPv218audio_pipeline_cfg"></a> <a id="audio_pipeline_cfg"></a> <a id="structaudio__pipeline__cfg"></a> struct audio\_pipeline\_cfg
:   Audio Pipeline configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18audio_pipeline_cfg7rb_sizeE"></a>

    <a id="_CPPv3N18audio_pipeline_cfg7rb_sizeE"></a> <a id="_CPPv2N18audio_pipeline_cfg7rb_sizeE"></a> <a id="audio_pipeline_cfg::rb_size__i"></a> <a id="structaudio__pipeline__cfg_1a073883da7713037f8f93e4a27effb711"></a> int rb\_size
    :   Audio Pipeline ringbuffer size

<a id="macros"></a>

### Macros

<a id="c.DEFAULT_PIPELINE_RINGBUF_SIZE"></a>

<a id="audio__pipeline_8h_1ad905b97722100c3302bef186d22b4f21"></a> DEFAULT\_PIPELINE\_RINGBUF\_SIZE

<a id="c.DEFAULT_AUDIO_PIPELINE_CONFIG"></a>

<a id="audio__pipeline_8h_1ac93198c449d316d6e7b6bd5585accbf5"></a> DEFAULT\_AUDIO\_PIPELINE\_CONFIG()

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv423audio_pipeline_handle_t"></a>

<a id="_CPPv323audio_pipeline_handle_t"></a> <a id="_CPPv223audio_pipeline_handle_t"></a> <a id="audio_pipeline_handle_t"></a> <a id="audio__pipeline_8h_1a6ea571efc6c16934f91453ffbf6a4d10"></a> typedef struct audio\_pipeline \*audio\_pipeline\_handle\_t

<a id="_CPPv420audio_pipeline_cfg_t"></a>

<a id="_CPPv320audio_pipeline_cfg_t"></a> <a id="_CPPv220audio_pipeline_cfg_t"></a> <a id="audio_pipeline_cfg_t"></a> <a id="audio__pipeline_8h_1a2473cd303bae7af0f06701b6e0fbc519"></a> typedef struct [audio\_pipeline\_cfg](#_CPPv418audio_pipeline_cfg "audio_pipeline_cfg") audio\_pipeline\_cfg\_t
:   Audio Pipeline configurations.
