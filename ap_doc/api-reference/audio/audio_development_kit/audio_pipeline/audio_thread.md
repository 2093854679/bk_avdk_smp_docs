# Audio Thread


The Audio Thread provides the thread management interface.


## API Reference


### Header File


- [bk_audio/audio_pipeline/audio_thread.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_thread.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_thread.h")


### Functions

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") audio_create_thread([beken_thread_t](../../../system/os.md#_CPPv414beken_thread_t "beken_thread_t") *thread, uint8_t priority, const char *name, [beken_thread_function_t](../../../system/os.md#_CPPv423beken_thread_function_t "beken_thread_function_t") function, uint32_t stack_size, [beken_thread_arg_t](../../../system/os.md#_CPPv418beken_thread_arg_t "beken_thread_arg_t") arg, int core_id)
:   Create audio thread to the specified core.

    ```
         Create audio thread to the core 0 when cpu work in smp system, if the specified core is not support.
         Create audio thread to the running core when cpu work in amp system, not depends on the specified core.
    ```

    参数
    :   - **thread** – **[out]** Pointer to variable that will receive the thread handle (can be null)

        - **priority** – **[in]** A priority number.

        - **name** – **[in]** a text name for the thread (can be null)

        - **function** – **[in]** the main thread function

        - **stack_size** – **[in]** stack size for this thread

        - **arg** – **[in]** argument which will be passed to thread function

        - **core_id** – **[in]** the core of the task running

    返回
    :   - kNoErr success.

        - kGeneralErr fail
