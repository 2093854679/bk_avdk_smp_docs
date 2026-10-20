---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_pipeline/audio_thread.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="audio-thread"></a>

# Audio Thread

The Audio Thread provides the thread management interface.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [audio\_thread.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_pipeline/audio_thread.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419audio_create_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_ti"></a>

<a id="_CPPv319audio_create_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_ti"></a> <a id="_CPPv219audio_create_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_ti"></a> <a id="audio_create_thread__beken_thread_tP.uint8_t.cCP.beken_thread_function_t.uint32_t.beken_thread_arg_t.i"></a> <a id="audio__thread_8h_1a877b875f98bcd981076c2e10a7458911"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio\_create\_thread([beken\_thread\_t](../../../system/os.md#_CPPv414beken_thread_t "beken_thread_t") \*thread, uint8\_t priority, const char \*name, [beken\_thread\_function\_t](../../../system/os.md#_CPPv423beken_thread_function_t "beken_thread_function_t") function, uint32\_t stack\_size, [beken\_thread\_arg\_t](../../../system/os.md#_CPPv418beken_thread_arg_t "beken_thread_arg_t") arg, int core\_id)
:   Create audio thread to the specified core.

    ```
         Create audio thread to the core 0 when cpu work in smp system, if the specified core is not support.
         Create audio thread to the running core when cpu work in amp system, not depends on the specified core.
    ```

    参数
    :   - **thread** – **\[out\]** Pointer to variable that will receive the thread handle (can be null)
        - **priority** – **\[in\]** A priority number.
        - **name** – **\[in\]** a text name for the thread (can be null)
        - **function** – **\[in\]** the main thread function
        - **stack\_size** – **\[in\]** stack size for this thread
        - **arg** – **\[in\]** argument which will be passed to thread function
        - **core\_id** – **\[in\]** the core of the task running

    返回
    :   - kNoErr success.
        - kGeneralErr fail
