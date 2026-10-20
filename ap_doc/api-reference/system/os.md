---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/system/os.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="os-api"></a>

# OS API

> - OS抽象层主要为了适配Armino平台不同的操作系统
> - 对于不同的操作系统，OS抽象层对外提供一套统一的接口
> - 目前Armino平台OS抽象层支持的操作系统有FreeRTOS.

备注

BK7259 为 CP\+AP 双核方案；两侧 `include/os/mem.h` 能力略有差异（AP 额外提供 HSRAM 堆与 UAF 调试接口）。内存 API 索引见 [内存 API](mem.md)，详细说明见 [内存接口](../../os/bk_mem.md)。

<a id="header-file"></a>

## Header File

- [os.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/os/os.h)

<a id="functions"></a>

## Functions

<a id="_CPPv419rtos_enter_criticalv"></a>

<a id="_CPPv319rtos_enter_criticalv"></a> <a id="_CPPv219rtos_enter_criticalv"></a> <a id="rtos_enter_critical__void"></a> <a id="group__os__apis_1gaeacef1c26de12d966fc8ceb8b7609684"></a> uint32\_t rtos\_enter\_critical(void)
:   Enter a critical session, all interrupts are disabled.

    返回
    :   irq flags

<a id="_CPPv418rtos_exit_critical8uint32_t"></a>

<a id="_CPPv318rtos_exit_critical8uint32_t"></a> <a id="_CPPv218rtos_exit_critical8uint32_t"></a> <a id="rtos_exit_critical__uint32_t"></a> <a id="group__os__apis_1ga86a055f9dacf9d74a3fac15a4409278a"></a> void rtos\_exit\_critical(uint32\_t flags)
:   Exit a critical session, all interrupts are enabled.

    参数
    :   **flags** – : irq flags

    返回
    :   none

<a id="_CPPv426rtos_enter_global_criticalv"></a>

<a id="_CPPv326rtos_enter_global_criticalv"></a> <a id="_CPPv226rtos_enter_global_criticalv"></a> <a id="rtos_enter_global_critical__void"></a> <a id="group__os__apis_1ga8d62aaad5f505c336449c3678ef32d8a"></a> uint32\_t rtos\_enter\_global\_critical(void)
:   Enter a critical session, all interrupts are disabled.

    返回
    :   irq flags

<a id="_CPPv425rtos_exit_global_critical8uint32_t"></a>

<a id="_CPPv325rtos_exit_global_critical8uint32_t"></a> <a id="_CPPv225rtos_exit_global_critical8uint32_t"></a> <a id="rtos_exit_global_critical__uint32_t"></a> <a id="group__os__apis_1gaac870ba48494f3fe156fd9010ba103c1"></a> void rtos\_exit\_global\_critical(uint32\_t flags)
:   Exit a critical session, all interrupts are enabled.

    参数
    :   **flags** – : irq flags

    返回
    :   none

<a id="_CPPv419beken_time_get_timeP12beken_time_t"></a>

<a id="_CPPv319beken_time_get_timeP12beken_time_t"></a> <a id="_CPPv219beken_time_get_timeP12beken_time_t"></a> <a id="beken_time_get_time__beken_time_tP"></a> <a id="group__os__apis_1ga165bb49a3ac9e7972363bff50b61feec"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") beken\_time\_get\_time([beken\_time\_t](#_CPPv412beken_time_t "beken_time_t") \*time\_ptr)
:   Get system time value in milliseconds.

    参数
    :   **time\_ptr** – : the pointer of time value in milliseconds

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv423rtos_create_sram_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a>

<a id="_CPPv323rtos_create_sram_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a> <a id="_CPPv223rtos_create_sram_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a> <a id="rtos_create_sram_thread__beken_thread_tP.uint8_t.cCP.beken_thread_function_t.uint32_t.beken_thread_arg_t"></a> <a id="group__BEKEN__RTOS__Thread_1ga00c582cb284bb4626dffa0e93d9b30b0"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_create\_sram\_thread([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread, uint8\_t priority, const char \*name, [beken\_thread\_function\_t](#_CPPv423beken_thread_function_t "beken_thread_function_t") function, uint32\_t stack\_size, [beken\_thread\_arg\_t](#_CPPv418beken_thread_arg_t "beken_thread_arg_t") arg)
:   Creates and starts a new thread.

    参数
    :   - **thread** – : Pointer to variable that will receive the thread handle (can be null)
        - **priority** – : A priority number.
        - **name** – : a text name for the thread (can be null)
        - **function** – : the main thread function
        - **stack\_size** – : stack size for this thread
        - **arg** – : argument which will be passed to thread function

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv424rtos_create_psram_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a>

<a id="_CPPv324rtos_create_psram_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a> <a id="_CPPv224rtos_create_psram_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a> <a id="rtos_create_psram_thread__beken_thread_tP.uint8_t.cCP.beken_thread_function_t.uint32_t.beken_thread_arg_t"></a> <a id="group__BEKEN__RTOS__Thread_1gac821b45dbd3d64b5bc9b2ac45b3a45ee"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_create\_psram\_thread([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread, uint8\_t priority, const char \*name, [beken\_thread\_function\_t](#_CPPv423beken_thread_function_t "beken_thread_function_t") function, uint32\_t stack\_size, [beken\_thread\_arg\_t](#_CPPv418beken_thread_arg_t "beken_thread_arg_t") arg)
:   Creates and starts a new thread on psram and not specify core.

    参数
    :   - **thread** – : Pointer to variable that will receive the thread handle (can be null)
        - **priority** – : A priority number.
        - **name** – : a text name for the thread (can be null)
        - **function** – : the main thread function
        - **stack\_size** – : stack size for this thread
        - **arg** – : argument which will be passed to thread function

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv424rtos_create_hsram_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a>

<a id="_CPPv324rtos_create_hsram_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a> <a id="_CPPv224rtos_create_hsram_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a> <a id="rtos_create_hsram_thread__beken_thread_tP.uint8_t.cCP.beken_thread_function_t.uint32_t.beken_thread_arg_t"></a> <a id="group__BEKEN__RTOS__Thread_1ga010f750513f0143adaaf397c3ca2a64d"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_create\_hsram\_thread([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread, uint8\_t priority, const char \*name, [beken\_thread\_function\_t](#_CPPv423beken_thread_function_t "beken_thread_function_t") function, uint32\_t stack\_size, [beken\_thread\_arg\_t](#_CPPv418beken_thread_arg_t "beken_thread_arg_t") arg)
:   Creates and starts a new thread on hsram and not specify core.

    参数
    :   - **thread** – : Pointer to variable that will receive the thread handle (can be null)
        - **priority** – : A priority number.
        - **name** – : a text name for the thread (can be null)
        - **function** – : the main thread function
        - **stack\_size** – : stack size for this thread
        - **arg** – : argument which will be passed to thread function

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv418rtos_create_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a>

<a id="_CPPv318rtos_create_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a> <a id="_CPPv218rtos_create_threadP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_t"></a> <a id="rtos_create_thread__beken_thread_tP.uint8_t.cCP.beken_thread_function_t.uint32_t.beken_thread_arg_t"></a> <a id="group__BEKEN__RTOS__Thread_1ga62d6448183997b762248f27d377f417b"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_create\_thread([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread, uint8\_t priority, const char \*name, [beken\_thread\_function\_t](#_CPPv423beken_thread_function_t "beken_thread_function_t") function, uint32\_t stack\_size, [beken\_thread\_arg\_t](#_CPPv418beken_thread_arg_t "beken_thread_arg_t") arg)
:   Creates and starts a new thread,the task will be dynamically created in sram(default)

    参数
    :   - **thread** – : Pointer to variable that will receive the thread handle (can be null)
        - **priority** – : A priority number. The adaptation layer uniformly managers priorities. For the application layer,the lower the configured number,the higher the task priority.Currently supports ten priority levels from 0 to 9\. recommended that the application layer use priorities from 6 to 8\.
        - **name** – : a text name for the thread (can be null)
        - **function** – : the main thread function
        - **stack\_size** – : stack size for this thread,size is in bytes,for example if the stack\_size is defined as 2048,then 2048bytes will be allocated for stack storage.
        - **arg** – : argument which will be passed to thread function

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv425rtos_create_thread_staticP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_tPCvPCv8uint32_t"></a>

<a id="_CPPv325rtos_create_thread_staticP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_tPCvPCv8uint32_t"></a> <a id="_CPPv225rtos_create_thread_staticP14beken_thread_t7uint8_tPKc23beken_thread_function_t8uint32_t18beken_thread_arg_tPCvPCv8uint32_t"></a> <a id="rtos_create_thread_static__beken_thread_tP.uint8_t.cCP.beken_thread_function_t.uint32_t.beken_thread_arg_t.voidPC.voidPC.uint32_t"></a> <a id="group__BEKEN__RTOS__Thread_1ga4be8e92cb2fb18082cfef9d62fa329be"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_create\_thread\_static([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread, uint8\_t priority, const char \*name, [beken\_thread\_function\_t](#_CPPv423beken_thread_function_t "beken_thread_function_t") function, uint32\_t stack\_size, [beken\_thread\_arg\_t](#_CPPv418beken_thread_arg_t "beken_thread_arg_t") arg, void \*const TaskStackBuffer, void \*const TaskTCBBuffer, uint32\_t core\_id)
:   Creates and starts a new thread,the task will be static created in sram(default)

    参数
    :   - **thread** – : Pointer to variable that will receive the thread handle (can be null)
        - **priority** – : A priority number. The adaptation layer uniformly managers priorities. For the application layer,the lower the configured number,the higher the task priority.Currently supports ten priority levels from 0 to 9\. recommended that the application layer use priorities from 6 to 8\.
        - **name** – : a text name for the thread (can be null)
        - **function** – : the main thread function
        - **stack\_size** – : stack size for this thread,size is in bytes,for example if the stack\_size is defined as 2048,then 2048bytes will be allocated for stack storage.
        - **arg** – : argument which will be passed to thread function
        - **TaskStackBuffer** – : Must point to a variable of type StaticTask\_t, which will then be used to hold the task’s data structures,
        - **TaskTCBBuffer** – : Must point to a variable of type StaticTask\_t, which will then be used to hold the task’s data structures,
        - **core\_id** – : Specify which core a task is bound to,the value can be 0/1 or 0xFFFFFFFF

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv418rtos_delete_threadP14beken_thread_t"></a>

<a id="_CPPv318rtos_delete_threadP14beken_thread_t"></a> <a id="_CPPv218rtos_delete_threadP14beken_thread_t"></a> <a id="rtos_delete_thread__beken_thread_tP"></a> <a id="group__BEKEN__RTOS__Thread_1ga18301a4b6b57170e6c371f914de04dee"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_delete\_thread([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread)
:   Deletes a terminated thread.

    备注

    If you want to delete the task itself,do not call this API when the interrupts is disables(may cause the system to enter a deadlock or abnormal status))

    参数
    :   **thread** – : the handle of the thread to delete, , NULL is the current thread

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv419rtos_suspend_threadP14beken_thread_t"></a>

<a id="_CPPv319rtos_suspend_threadP14beken_thread_t"></a> <a id="_CPPv219rtos_suspend_threadP14beken_thread_t"></a> <a id="rtos_suspend_thread__beken_thread_tP"></a> <a id="group__BEKEN__RTOS__Thread_1ga39d257a6b9a0d7220f5c7c4abc2319a2"></a> void rtos\_suspend\_thread([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread)
:   Suspend a thread.

    备注

    If you want to suspend the task itself,do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **thread** – : the handle of the thread to suspend, NULL is the current thread

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv423rtos_suspend_all_threadv"></a>

<a id="_CPPv323rtos_suspend_all_threadv"></a> <a id="_CPPv223rtos_suspend_all_threadv"></a> <a id="rtos_suspend_all_thread__void"></a> <a id="group__BEKEN__RTOS__Thread_1gaf9de078556736b02b6d5a48ffd1645b0"></a> void rtos\_suspend\_all\_thread(void)
:   Suspend all other thread.

    参数
    :   **none** –

    返回
    :   none

<a id="_CPPv418rtos_resume_threadP14beken_thread_t"></a>

<a id="_CPPv318rtos_resume_threadP14beken_thread_t"></a> <a id="_CPPv218rtos_resume_threadP14beken_thread_t"></a> <a id="rtos_resume_thread__beken_thread_tP"></a> <a id="group__BEKEN__RTOS__Thread_1ga2299f295fc24bdf6489c9dea5b2cfb29"></a> void rtos\_resume\_thread([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread)
:   resume a thread

    备注

    If you want to resume the task not itself,do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **thread** – : the handle of the thread to resume, NULL is the current thread

    返回
    :   none

<a id="_CPPv422rtos_resume_all_threadv"></a>

<a id="_CPPv322rtos_resume_all_threadv"></a> <a id="_CPPv222rtos_resume_all_threadv"></a> <a id="rtos_resume_all_thread__void"></a> <a id="group__BEKEN__RTOS__Thread_1ga836630ce5e4118b8ce9b41cbaf83d1e1"></a> void rtos\_resume\_all\_thread(void)
:   Rresume all other thread.

    参数
    :   **none** –

    返回
    :   none

<a id="_CPPv416rtos_thread_joinP14beken_thread_t"></a>

<a id="_CPPv316rtos_thread_joinP14beken_thread_t"></a> <a id="_CPPv216rtos_thread_joinP14beken_thread_t"></a> <a id="rtos_thread_join__beken_thread_tP"></a> <a id="group__BEKEN__RTOS__Thread_1ga211577220405875be68c12375f68d521"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_thread\_join([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread)
:   Sleeps until another thread has terminated.

    @Details Causes the current thread to sleep until the specified other thread has terminated. If the processor is heavily loaded with higher priority tasks, this thread may not wake until significantly after the thread termination.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **thread** – : the handle of the other thread which will terminate

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv423rtos_thread_force_awakeP14beken_thread_t"></a>

<a id="_CPPv323rtos_thread_force_awakeP14beken_thread_t"></a> <a id="_CPPv223rtos_thread_force_awakeP14beken_thread_t"></a> <a id="rtos_thread_force_awake__beken_thread_tP"></a> <a id="group__BEKEN__RTOS__Thread_1ga3aa4305e105bda539aeec74941841fc9"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_thread\_force\_awake([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread)
:   Forcibly wakes another thread.

    @Details Causes the specified thread to wake from suspension. This will usually cause an error or timeout in that thread, since the task it was waiting on is not complete.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **thread** – : the handle of the other thread which will be removed from the block state.

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv422rtos_is_current_threadP14beken_thread_t"></a>

<a id="_CPPv322rtos_is_current_threadP14beken_thread_t"></a> <a id="_CPPv222rtos_is_current_threadP14beken_thread_t"></a> <a id="rtos_is_current_thread__beken_thread_tP"></a> <a id="group__BEKEN__RTOS__Thread_1ga69ef5324d432af3a5cd86890e0713c68"></a> bool rtos\_is\_current\_thread([beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*thread)
:   Checks if a thread is the current thread.

    @Details Checks if a specified thread is the currently running thread

    参数
    :   **thread** – : the handle of the other thread against which the current thread will be compared

    返回
    :   true : specified thread is the current thread

    返回
    :   false : specified thread is not currently running

<a id="_CPPv423rtos_get_current_threadv"></a>

<a id="_CPPv323rtos_get_current_threadv"></a> <a id="_CPPv223rtos_get_current_threadv"></a> <a id="rtos_get_current_thread__void"></a> <a id="group__BEKEN__RTOS__Thread_1ga498e82f9a6bf29d7e01e3c82dc77211f"></a> [beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") \*rtos\_get\_current\_thread(void)
:   Get current thread handler.

    返回
    :   Current RTOS thread handler

<a id="_CPPv417rtos_thread_sleep8uint32_t"></a>

<a id="_CPPv317rtos_thread_sleep8uint32_t"></a> <a id="_CPPv217rtos_thread_sleep8uint32_t"></a> <a id="rtos_thread_sleep__uint32_t"></a> <a id="group__BEKEN__RTOS__Thread_1ga0dce8fe06a964183ee06dec3bf9f9c66"></a> void rtos\_thread\_sleep(uint32\_t seconds)
:   Suspend current thread for a specific time.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **seconds** – : A time interval (Unit: seconds)

    返回
    :   None.

<a id="_CPPv418rtos_thread_msleep8uint32_t"></a>

<a id="_CPPv318rtos_thread_msleep8uint32_t"></a> <a id="_CPPv218rtos_thread_msleep8uint32_t"></a> <a id="rtos_thread_msleep__uint32_t"></a> <a id="group__BEKEN__RTOS__Thread_1gabfe4fd01275cd0ace4db76db37f31789"></a> void rtos\_thread\_msleep(uint32\_t milliseconds)
:   Suspend current thread for a specific time.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **milliseconds** – : A time interval (Unit: millisecond)

    返回
    :   None.

<a id="_CPPv423rtos_delay_milliseconds8uint32_t"></a>

<a id="_CPPv323rtos_delay_milliseconds8uint32_t"></a> <a id="_CPPv223rtos_delay_milliseconds8uint32_t"></a> <a id="rtos_delay_milliseconds__uint32_t"></a> <a id="group__BEKEN__RTOS__Thread_1ga4dd2e0920daaa295c5ee9a9c373a1e42"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_delay\_milliseconds(uint32\_t num\_ms)
:   Suspend current thread for a specific time.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **num\_ms** – : A time interval (Unit: millisecond)

    返回
    :   kNoErr.

<a id="_CPPv424rtos_print_thread_statusPci"></a>

<a id="_CPPv324rtos_print_thread_statusPci"></a> <a id="_CPPv224rtos_print_thread_statusPci"></a> <a id="rtos_print_thread_status__cP.i"></a> <a id="group__BEKEN__RTOS__Thread_1gaeacb8f75e0e27c9c4d697637fb2274d6"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_print\_thread\_status(char \*buffer, int length)
:   Print Thread status into buffer.

    参数
    :   - **buffer, point** – to buffer to store thread status
        - **length, length** – of the buffer

    返回
    :   none

<a id="_CPPv419rtos_init_semaphoreP17beken_semaphore_ti"></a>

<a id="_CPPv319rtos_init_semaphoreP17beken_semaphore_ti"></a> <a id="_CPPv219rtos_init_semaphoreP17beken_semaphore_ti"></a> <a id="rtos_init_semaphore__beken_semaphore_tP.i"></a> <a id="group__BEKEN__RTOS__SEM_1gab8c99e1fa5c54d1759c538ca78de93a5"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_init\_semaphore([beken\_semaphore\_t](#_CPPv417beken_semaphore_t "beken_semaphore_t") \*semaphore, int max\_count)
:   Initialises a counting semaphore and set count to 0\.

    参数
    :   - **semaphore** – : a pointer to the semaphore handle to be initialised
        - **max\_count** – : the max count number of this semaphore

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv422rtos_init_semaphore_exP17beken_semaphore_tii"></a>

<a id="_CPPv322rtos_init_semaphore_exP17beken_semaphore_tii"></a> <a id="_CPPv222rtos_init_semaphore_exP17beken_semaphore_tii"></a> <a id="rtos_init_semaphore_ex__beken_semaphore_tP.i.i"></a> <a id="group__BEKEN__RTOS__SEM_1ga540ee9ef7c02d2292384c16d1a54efdf"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_init\_semaphore\_ex([beken\_semaphore\_t](#_CPPv417beken_semaphore_t "beken_semaphore_t") \*semaphore, int max\_count, int init\_count)
:   Initialises a counting semaphore and set count to init count.

    参数
    :   - **semaphore** – : a pointer to the semaphore handle to be initialised
        - **max\_count** – : the max count number of this semaphore
        - **init\_count** – : the init count number of this semaphore

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv418rtos_set_semaphoreP17beken_semaphore_t"></a>

<a id="_CPPv318rtos_set_semaphoreP17beken_semaphore_t"></a> <a id="_CPPv218rtos_set_semaphoreP17beken_semaphore_t"></a> <a id="rtos_set_semaphore__beken_semaphore_tP"></a> <a id="group__BEKEN__RTOS__SEM_1ga4e132dc329ec2d651aa543928f6a5313"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_set\_semaphore([beken\_semaphore\_t](#_CPPv417beken_semaphore_t "beken_semaphore_t") \*semaphore)
:   Set (post/put/increment) a semaphore.

    备注

    This API can be called in task context and interrupt context.

    参数
    :   **semaphore** – : a pointer to the semaphore handle to be set

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv418rtos_get_semaphoreP17beken_semaphore_t8uint32_t"></a>

<a id="_CPPv318rtos_get_semaphoreP17beken_semaphore_t8uint32_t"></a> <a id="_CPPv218rtos_get_semaphoreP17beken_semaphore_t8uint32_t"></a> <a id="rtos_get_semaphore__beken_semaphore_tP.uint32_t"></a> <a id="group__BEKEN__RTOS__SEM_1ga63d52a0c91ce0aa6793cd1fdc9690e5a"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_get\_semaphore([beken\_semaphore\_t](#_CPPv417beken_semaphore_t "beken_semaphore_t") \*semaphore, uint32\_t timeout\_ms)
:   Get (wait/decrement) a semaphore.

    @Details Attempts to get (wait/decrement) a semaphore. If semaphore is at zero already, then the calling thread will be suspended until another thread sets the semaphore with [rtos\_set\_semaphore](#group__BEKEN__RTOS__SEM_1ga4e132dc329ec2d651aa543928f6a5313)

    备注

    Do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   - **semaphore** – : a pointer to the semaphore handle
        - **timeout\_ms** – the number of milliseconds to wait before returning

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv424rtos_get_semaphore_countP17beken_semaphore_t"></a>

<a id="_CPPv324rtos_get_semaphore_countP17beken_semaphore_t"></a> <a id="_CPPv224rtos_get_semaphore_countP17beken_semaphore_t"></a> <a id="rtos_get_semaphore_count__beken_semaphore_tP"></a> <a id="group__BEKEN__RTOS__SEM_1ga1c32e98b96790742a806a3bc03f1537e"></a> int rtos\_get\_semaphore\_count([beken\_semaphore\_t](#_CPPv417beken_semaphore_t "beken_semaphore_t") \*semaphore)
:   get current semaphore count

    参数
    :   **semaphore** – : a pointer to the semaphore handle to be set

    返回
    :   kNoErr : current semaphore count

<a id="_CPPv421rtos_deinit_semaphoreP17beken_semaphore_t"></a>

<a id="_CPPv321rtos_deinit_semaphoreP17beken_semaphore_t"></a> <a id="_CPPv221rtos_deinit_semaphoreP17beken_semaphore_t"></a> <a id="rtos_deinit_semaphore__beken_semaphore_tP"></a> <a id="group__BEKEN__RTOS__SEM_1gacd99f32c53360ed9016baa8a3a0db6ec"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_deinit\_semaphore([beken\_semaphore\_t](#_CPPv417beken_semaphore_t "beken_semaphore_t") \*semaphore)
:   De-initialise a semaphore.

    @Details Deletes a semaphore created with [rtos\_init\_semaphore](#group__BEKEN__RTOS__SEM_1gab8c99e1fa5c54d1759c538ca78de93a5)

    参数
    :   **semaphore** – : a pointer to the semaphore handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv415rtos_init_mutexP13beken_mutex_t"></a>

<a id="_CPPv315rtos_init_mutexP13beken_mutex_t"></a> <a id="_CPPv215rtos_init_mutexP13beken_mutex_t"></a> <a id="rtos_init_mutex__beken_mutex_tP"></a> <a id="group__BEKEN__RTOS__MUTEX_1ga206c1b0aebb6431a6407373e921b2486"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_init\_mutex([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex)
:   Initialises a mutex.

    @Details A mutex is different to a semaphore in that a thread that already holds the lock on the mutex can request the lock again (nested) without causing it to be suspended.

    参数
    :   **mutex** – : a pointer to the mutex handle to be initialised

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv418rtos_trylock_mutexP13beken_mutex_t"></a>

<a id="_CPPv318rtos_trylock_mutexP13beken_mutex_t"></a> <a id="_CPPv218rtos_trylock_mutexP13beken_mutex_t"></a> <a id="rtos_trylock_mutex__beken_mutex_tP"></a> <a id="group__BEKEN__RTOS__MUTEX_1gae833c0f1d8a543f0c2d674cfd6ddc87e"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_trylock\_mutex([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex)
:   Obtains the lock on a mutex.

    @Details Attempts to obtain the lock on a mutex. If the lock is already held by another thead, the calling thread will not be suspended until the mutex lock is released by the other thread.

    参数
    :   **mutex** – : a pointer to the mutex handle to be locked

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv415rtos_lock_mutexP13beken_mutex_t"></a>

<a id="_CPPv315rtos_lock_mutexP13beken_mutex_t"></a> <a id="_CPPv215rtos_lock_mutexP13beken_mutex_t"></a> <a id="rtos_lock_mutex__beken_mutex_tP"></a> <a id="group__BEKEN__RTOS__MUTEX_1gabcf759b17d613da44cf49dbf227bc5c0"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_lock\_mutex([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex)
:   Obtains the lock on a mutex.

    @Details Attempts to obtain the lock on a mutex. If the lock is already held by another thead, the calling thread will be suspended until the mutex lock is released by the other thread.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **mutex** – : a pointer to the mutex handle to be locked

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv423rtos_lock_mutex_timeoutP13beken_mutex_t8uint32_t"></a>

<a id="_CPPv323rtos_lock_mutex_timeoutP13beken_mutex_t8uint32_t"></a> <a id="_CPPv223rtos_lock_mutex_timeoutP13beken_mutex_t8uint32_t"></a> <a id="rtos_lock_mutex_timeout__beken_mutex_tP.uint32_t"></a> <a id="group__BEKEN__RTOS__MUTEX_1ga174da9f6c1610cbcfa5dc2e9821e5a03"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_lock\_mutex\_timeout([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex, uint32\_t timeout\_ms)
:   Obtains the lock on a mutex.

    @Details Attempts to obtain the lock on a mutex. If the lock is already held by another thead, the calling thread will be suspended until the mutex lock is released by the other thread or timeout.

    参数
    :   - **mutex** – : a pointer to the mutex handle to be locked
        - **timeout\_ms** – : timeout for get lock

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv417rtos_unlock_mutexP13beken_mutex_t"></a>

<a id="_CPPv317rtos_unlock_mutexP13beken_mutex_t"></a> <a id="_CPPv217rtos_unlock_mutexP13beken_mutex_t"></a> <a id="rtos_unlock_mutex__beken_mutex_tP"></a> <a id="group__BEKEN__RTOS__MUTEX_1ga340cb91499d5b2e03fd173efde2e581b"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_unlock\_mutex([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex)
:   Releases the lock on a mutex.

    @Details Releases a currently held lock on a mutex. If another thread is waiting on the mutex lock, then it will be resumed.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **mutex** – : a pointer to the mutex handle to be unlocked

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv417rtos_deinit_mutexP13beken_mutex_t"></a>

<a id="_CPPv317rtos_deinit_mutexP13beken_mutex_t"></a> <a id="_CPPv217rtos_deinit_mutexP13beken_mutex_t"></a> <a id="rtos_deinit_mutex__beken_mutex_tP"></a> <a id="group__BEKEN__RTOS__MUTEX_1ga45dc67ce2e7d3b37f824a5e6cbf94a62"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_deinit\_mutex([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex)
:   De-initialise a mutex.

    @Details Deletes a mutex created with [rtos\_init\_mutex](#group__BEKEN__RTOS__MUTEX_1ga206c1b0aebb6431a6407373e921b2486)

    参数
    :   **mutex** – : a pointer to the mutex handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv425rtos_init_recursive_mutexP13beken_mutex_t"></a>

<a id="_CPPv325rtos_init_recursive_mutexP13beken_mutex_t"></a> <a id="_CPPv225rtos_init_recursive_mutexP13beken_mutex_t"></a> <a id="rtos_init_recursive_mutex__beken_mutex_tP"></a> <a id="group__BEKEN__RTOS__MUTEX_1ga4904afaad1caa400f69a692093c4832f"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_init\_recursive\_mutex([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex)
:   Creates a new recursive mutex type semaphore instance.

    参数
    :   **mutex** – : a pointer to the new recursive mutex handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv425rtos_lock_recursive_mutexP13beken_mutex_t"></a>

<a id="_CPPv325rtos_lock_recursive_mutexP13beken_mutex_t"></a> <a id="_CPPv225rtos_lock_recursive_mutexP13beken_mutex_t"></a> <a id="rtos_lock_recursive_mutex__beken_mutex_tP"></a> <a id="group__BEKEN__RTOS__MUTEX_1ga648170ef217288abaf1859c784aeee61"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_lock\_recursive\_mutex([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex)
:   Obtains the lock on a recursive mutex (A mutex used recursively can be ‘taken’ repeatedly by the owner)

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **mutex** – : a pointer to the new recursive mutex handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv427rtos_unlock_recursive_mutexP13beken_mutex_t"></a>

<a id="_CPPv327rtos_unlock_recursive_mutexP13beken_mutex_t"></a> <a id="_CPPv227rtos_unlock_recursive_mutexP13beken_mutex_t"></a> <a id="rtos_unlock_recursive_mutex__beken_mutex_tP"></a> <a id="group__BEKEN__RTOS__MUTEX_1gaa188f26ada3f88508a919867ac52cc35"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_unlock\_recursive\_mutex([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex)
:   Releases the lock on a recursive mutex (A mutex used recursively can be ‘taken’ repeatedly by the owner)

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **mutex** – : a pointer to the new recursive mutex handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv427rtos_deinit_recursive_mutexP13beken_mutex_t"></a>

<a id="_CPPv327rtos_deinit_recursive_mutexP13beken_mutex_t"></a> <a id="_CPPv227rtos_deinit_recursive_mutexP13beken_mutex_t"></a> <a id="rtos_deinit_recursive_mutex__beken_mutex_tP"></a> <a id="group__BEKEN__RTOS__MUTEX_1gaeca047c6d6c7eadd42c70dba539c5785"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_deinit\_recursive\_mutex([beken\_mutex\_t](#_CPPv413beken_mutex_t "beken_mutex_t") \*mutex)
:   De-initialise a recursive mutex.

    @Details Deletes a mutex created with [rtos\_init\_recursive\_mutex](#group__BEKEN__RTOS__MUTEX_1ga4904afaad1caa400f69a692093c4832f)

    参数
    :   **mutex** – : a pointer to the recursive mutex handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv415rtos_init_queueP13beken_queue_tPKc8uint32_t8uint32_t"></a>

<a id="_CPPv315rtos_init_queueP13beken_queue_tPKc8uint32_t8uint32_t"></a> <a id="_CPPv215rtos_init_queueP13beken_queue_tPKc8uint32_t8uint32_t"></a> <a id="rtos_init_queue__beken_queue_tP.cCP.uint32_t.uint32_t"></a> <a id="group__BEKEN__RTOS__QUEUE_1gaac5e20b73f7298368b26eb5de85483c3"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_init\_queue([beken\_queue\_t](#_CPPv413beken_queue_t "beken_queue_t") \*queue, const char \*name, uint32\_t message\_size, uint32\_t number\_of\_messages)
:   Initialises a FIFO queue.

    参数
    :   - **queue** – : a pointer to the queue handle to be initialised
        - **name** – : a text string name for the queue (NULL is allowed)
        - **message\_size** – : size in bytes of objects that will be held in the queue
        - **number\_of\_messages** – : depth of the queue \- i.e. max number of objects in the queue

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv418rtos_push_to_queueP13beken_queue_tPv8uint32_t"></a>

<a id="_CPPv318rtos_push_to_queueP13beken_queue_tPv8uint32_t"></a> <a id="_CPPv218rtos_push_to_queueP13beken_queue_tPv8uint32_t"></a> <a id="rtos_push_to_queue__beken_queue_tP.voidP.uint32_t"></a> <a id="group__BEKEN__RTOS__QUEUE_1gaf4fe8d00c18ccf386b9b841e60e174d3"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_push\_to\_queue([beken\_queue\_t](#_CPPv413beken_queue_t "beken_queue_t") \*queue, void \*message, uint32\_t timeout\_ms)
:   Post an item to the back of a queue. The item is queued by copy, not by reference.

    备注

    This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   - **queue** – : a pointer to the queue handle
        - **message** – : the object to be added to the queue. Size is assumed to be the size specified in [rtos\_init\_queue](#group__BEKEN__RTOS__QUEUE_1gaac5e20b73f7298368b26eb5de85483c3)
        - **timeout\_ms** – the number of milliseconds to wait before returning

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error or timeout occurred

<a id="_CPPv424rtos_push_to_queue_frontP13beken_queue_tPv8uint32_t"></a>

<a id="_CPPv324rtos_push_to_queue_frontP13beken_queue_tPv8uint32_t"></a> <a id="_CPPv224rtos_push_to_queue_frontP13beken_queue_tPv8uint32_t"></a> <a id="rtos_push_to_queue_front__beken_queue_tP.voidP.uint32_t"></a> <a id="group__BEKEN__RTOS__QUEUE_1gad4e54e98bfb2f7100bcbb8cd767655fb"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_push\_to\_queue\_front([beken\_queue\_t](#_CPPv413beken_queue_t "beken_queue_t") \*queue, void \*message, uint32\_t timeout\_ms)
:   Post an item to the front of a queue. The item is queued by copy, not by reference.

    备注

    This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   - **queue** – : a pointer to the queue handle
        - **message** – : the object to be added to the queue. Size is assumed to be the size specified in [rtos\_init\_queue](#group__BEKEN__RTOS__QUEUE_1gaac5e20b73f7298368b26eb5de85483c3)
        - **timeout\_ms** – the number of milliseconds to wait before returning

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error or timeout occurred

<a id="_CPPv419rtos_pop_from_queueP13beken_queue_tPv8uint32_t"></a>

<a id="_CPPv319rtos_pop_from_queueP13beken_queue_tPv8uint32_t"></a> <a id="_CPPv219rtos_pop_from_queueP13beken_queue_tPv8uint32_t"></a> <a id="rtos_pop_from_queue__beken_queue_tP.voidP.uint32_t"></a> <a id="group__BEKEN__RTOS__QUEUE_1gaaa843981ac613eaccbb0231e5b50b024"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_pop\_from\_queue([beken\_queue\_t](#_CPPv413beken_queue_t "beken_queue_t") \*queue, void \*message, uint32\_t timeout\_ms)
:   Pops an object off a queue.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   - **queue** – : a pointer to the queue handle
        - **message** – : pointer to a buffer that will receive the object being popped off the queue. Size is assumed to be the size specified in [rtos\_init\_queue](#group__BEKEN__RTOS__QUEUE_1gaac5e20b73f7298368b26eb5de85483c3) , hence you must ensure the buffer is long enough or memory corruption will result
        - **timeout\_ms** – the number of milliseconds to wait before returning

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error or timeout occurred

<a id="_CPPv417rtos_deinit_queueP13beken_queue_t"></a>

<a id="_CPPv317rtos_deinit_queueP13beken_queue_t"></a> <a id="_CPPv217rtos_deinit_queueP13beken_queue_t"></a> <a id="rtos_deinit_queue__beken_queue_tP"></a> <a id="group__BEKEN__RTOS__QUEUE_1gad50078690271f44ce66f45ce5819c3af"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_deinit\_queue([beken\_queue\_t](#_CPPv413beken_queue_t "beken_queue_t") \*queue)
:   De-initialise a queue created with [rtos\_init\_queue](#group__BEKEN__RTOS__QUEUE_1gaac5e20b73f7298368b26eb5de85483c3).

    参数
    :   **queue** – : a pointer to the queue handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv419rtos_is_queue_emptyP13beken_queue_t"></a>

<a id="_CPPv319rtos_is_queue_emptyP13beken_queue_t"></a> <a id="_CPPv219rtos_is_queue_emptyP13beken_queue_t"></a> <a id="rtos_is_queue_empty__beken_queue_tP"></a> <a id="group__BEKEN__RTOS__QUEUE_1ga155f5f3c6903f355804d166877b93d0a"></a> bool rtos\_is\_queue\_empty([beken\_queue\_t](#_CPPv413beken_queue_t "beken_queue_t") \*queue)
:   Check if a queue is empty.

    参数
    :   **queue** – : a pointer to the queue handle

    返回
    :   true : queue is empty.

    返回
    :   false : queue is not empty.

<a id="_CPPv418rtos_is_queue_fullP13beken_queue_t"></a>

<a id="_CPPv318rtos_is_queue_fullP13beken_queue_t"></a> <a id="_CPPv218rtos_is_queue_fullP13beken_queue_t"></a> <a id="rtos_is_queue_full__beken_queue_tP"></a> <a id="group__BEKEN__RTOS__QUEUE_1ga45be84b6fdeee61a3400ebb1f7a787aa"></a> bool rtos\_is\_queue\_full([beken\_queue\_t](#_CPPv413beken_queue_t "beken_queue_t") \*queue)
:   Check if a queue is full.

    参数
    :   **queue** – : a pointer to the queue handle

    返回
    :   true : queue is full.

    返回
    :   false : queue is not full.

<a id="_CPPv416rtos_reset_queueP13beken_queue_t"></a>

<a id="_CPPv316rtos_reset_queueP13beken_queue_t"></a> <a id="_CPPv216rtos_reset_queueP13beken_queue_t"></a> <a id="rtos_reset_queue__beken_queue_tP"></a> <a id="group__BEKEN__RTOS__QUEUE_1ga246957b12563fb6516c56aeeb98fbfc1"></a> bool rtos\_reset\_queue([beken\_queue\_t](#_CPPv413beken_queue_t "beken_queue_t") \*queue)
:   Reset queue.

    参数
    :   **queue** – : a pointer to the queue handle

    返回
    :   true : reset ok.

    返回
    :   false : reset fail.

<a id="_CPPv421rtos_init_event_flagsP13beken_event_t"></a>

<a id="_CPPv321rtos_init_event_flagsP13beken_event_t"></a> <a id="_CPPv221rtos_init_event_flagsP13beken_event_t"></a> <a id="rtos_init_event_flags__beken_event_tP"></a> <a id="group__BEKEN__RTOS__EVENT_1gac306ea13a38248022cfca5893c0cc57c"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_init\_event\_flags([beken\_event\_t](#_CPPv413beken_event_t "beken_event_t") \*event\_flags)
:   Create a new event group

    参数
    :   **event\_flags** – : pointer to a event handle which will be initialised

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv425rtos_wait_for_event_flagsP13beken_event_t8uint32_t12beken_bool_t31beken_event_flags_wait_option_t8uint32_t"></a>

<a id="_CPPv325rtos_wait_for_event_flagsP13beken_event_t8uint32_t12beken_bool_t31beken_event_flags_wait_option_t8uint32_t"></a> <a id="_CPPv225rtos_wait_for_event_flagsP13beken_event_t8uint32_t12beken_bool_t31beken_event_flags_wait_option_t8uint32_t"></a> <a id="rtos_wait_for_event_flags__beken_event_tP.uint32_t.beken_bool_t.beken_event_flags_wait_option_t.uint32_t"></a> <a id="group__BEKEN__RTOS__EVENT_1gae6cf9960174db036b0bdf7d1a0284345"></a> [beken\_event\_flags\_t](#_CPPv419beken_event_flags_t "beken_event_flags_t") rtos\_wait\_for\_event\_flags([beken\_event\_t](#_CPPv413beken_event_t "beken_event_t") \*event\_flags, uint32\_t flags\_to\_wait\_for, [beken\_bool\_t](#_CPPv412beken_bool_t "beken_bool_t") clear\_set\_flags, [beken\_event\_flags\_wait\_option\_t](#_CPPv431beken_event_flags_wait_option_t "beken_event_flags_wait_option_t") wait\_option, uint32\_t timeout\_ms)
:   block to wait for one or more bits to be set within a previously created event group.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   - **event\_flags** – : pointer to a event handle which will be initialised
        - **flags\_to\_wait\_for** – : A bitwise value that indicates the bit or bits to test inside the event group. For example, to wait for bit 0 and/or bit 2 set flags\_to\_wait\_for to 0x05. To wait for bits 0 and/or bit 1 and/or bit 2 set flags\_to\_wait\_for to 0x07. Etc.
        - **clear\_set\_flags** – : If clear\_set\_flags is set to pdTRUE then any bits within flags\_to\_wait\_for that are set within the event group will be cleared before returns
        - **wait\_option** – : If it is set to WAIT\_FOR\_ALL\_EVENTS then will return when either all the bits in flags\_to\_wait\_for are set or the specified block time expires. If it is set to WAIT\_FOR\_ANY\_EVENT then will return when any one of the bits set in flags\_to\_wait\_for is set or the specified block time expires. The block time is specified by the timeout\_ms parameter.
        - **timeout\_ms** – : the time period between function calls in milliseconds

    返回
    :   The value of the event group at the time either the bits being waited for became set, or the block time expired.

<a id="_CPPv420rtos_set_event_flagsP13beken_event_t8uint32_t"></a>

<a id="_CPPv320rtos_set_event_flagsP13beken_event_t8uint32_t"></a> <a id="_CPPv220rtos_set_event_flagsP13beken_event_t8uint32_t"></a> <a id="rtos_set_event_flags__beken_event_tP.uint32_t"></a> <a id="group__BEKEN__RTOS__EVENT_1gad1af45220486f36d4100703da8f04f03"></a> void rtos\_set\_event\_flags([beken\_event\_t](#_CPPv413beken_event_t "beken_event_t") \*event\_flags, uint32\_t flags\_to\_set)
:   Set bits within an event group.

    备注

    This API can be called in task context and interrupt context.

    参数
    :   - **event\_flags** – : pointer to a event handle which will be initialised
        - **flags\_to\_set** –

          : A bitwise value that indicates the bit or bits to set. For example, to set bit 3 only, set flags\_to\_set to 0x08.

          To set bit 3 and bit 0 set flags\_to\_set to 0x09.

<a id="_CPPv422rtos_clear_event_flagsP13beken_event_t8uint32_t"></a>

<a id="_CPPv322rtos_clear_event_flagsP13beken_event_t8uint32_t"></a> <a id="_CPPv222rtos_clear_event_flagsP13beken_event_t8uint32_t"></a> <a id="rtos_clear_event_flags__beken_event_tP.uint32_t"></a> <a id="group__BEKEN__RTOS__EVENT_1gaa76fc93d48742c21e43f98f48b8db4cd"></a> [beken\_event\_flags\_t](#_CPPv419beken_event_flags_t "beken_event_flags_t") rtos\_clear\_event\_flags([beken\_event\_t](#_CPPv413beken_event_t "beken_event_t") \*event\_flags, uint32\_t flags\_to\_clear)
:   Clear bits within an event group.

    备注

    This API can be called in task context and interrupt context.

    参数
    :   - **event\_flags** – : pointer to a event handle which will be initialised
        - **flags\_to\_clear** – :A bitwise value that indicates the bit or bits to clear in the event group. For example, to clear bit 3 only, set flags\_to\_clear to 0x08. To clear bit 3 and bit 0 set flags\_to\_clear to 0x09.

    返回
    :   The value of the event group before the specified bits were cleared

<a id="_CPPv421rtos_sync_event_flagsP13beken_event_t8uint32_t8uint32_t8uint32_t"></a>

<a id="_CPPv321rtos_sync_event_flagsP13beken_event_t8uint32_t8uint32_t8uint32_t"></a> <a id="_CPPv221rtos_sync_event_flagsP13beken_event_t8uint32_t8uint32_t8uint32_t"></a> <a id="rtos_sync_event_flags__beken_event_tP.uint32_t.uint32_t.uint32_t"></a> <a id="group__BEKEN__RTOS__EVENT_1ga8bfaa6f5b6eb7ca404b3dd290a2ffb5a"></a> [beken\_event\_flags\_t](#_CPPv419beken_event_flags_t "beken_event_flags_t") rtos\_sync\_event\_flags([beken\_event\_t](#_CPPv413beken_event_t "beken_event_t") \*event\_flags, uint32\_t flags\_to\_set, uint32\_t flags\_to\_wait\_for, uint32\_t timeout\_ms)
:   Atomically set bits within an event group, then wait for a combination of bits to be set within the same event group. This functionality is typically used to synchronise multiple tasks, where each task has to wait for the other tasks to reach a synchronisation point before proceeding.

    备注

    do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   - **event\_flags** – : pointer to a event handle which will be initialised
        - **flags\_to\_set** – : The bits to set in the event group before determining if, and possibly waiting for, all the bits specified by the timeout\_ms parameter are set.
        - **flags\_to\_wait\_for** – : A bitwise value that indicates the bit or bits to test inside the event group. For example, to wait for bit 0 and bit 2 flags\_to\_wait\_for to 0x05. To wait for bits 0 and bit 1 and bit 2 set flags\_to\_wait\_for to 0x07. Etc.
        - **timeout\_ms** – : the time period between function calls in milliseconds

    返回
    :   The value of the event group at the time either the bits being waited for became set, or the block time expired.

<a id="_CPPv423rtos_deinit_event_flagsP13beken_event_t"></a>

<a id="_CPPv323rtos_deinit_event_flagsP13beken_event_t"></a> <a id="_CPPv223rtos_deinit_event_flagsP13beken_event_t"></a> <a id="rtos_deinit_event_flags__beken_event_tP"></a> <a id="group__BEKEN__RTOS__EVENT_1ga78173fa38b8d8d87431e47f827178e03"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_deinit\_event\_flags([beken\_event\_t](#_CPPv413beken_event_t "beken_event_t") \*event\_flags)
:   Delete an event group that was previously created by a call to [rtos\_init\_event\_flags()](#group__BEKEN__RTOS__EVENT_1gac306ea13a38248022cfca5893c0cc57c). Tasks that are blocked on the event group will be unblocked and obtain 0 as the event group’s value.

    参数
    :   **event\_flags** – : pointer to a event handle which will be initialised

    返回
    :   kNoErr : on success.

    返回
    :   kParamErr : if an error occurred

<a id="_CPPv413rtos_get_timev"></a>

<a id="_CPPv313rtos_get_timev"></a> <a id="_CPPv213rtos_get_timev"></a> <a id="rtos_get_time__void"></a> <a id="group__BEKEN__RTOS__TIMER_1gaf03416446210651ff9a910caa55f0161"></a> uint32\_t rtos\_get\_time(void)
:   Gets time in miiliseconds since RTOS start.

    备注

    : Since this is only 32 bits, it will roll over every 49 days, 17 hours.

    返回
    :   Time in milliseconds since RTOS started.

<a id="_CPPv417beken_ms_per_tickv"></a>

<a id="_CPPv317beken_ms_per_tickv"></a> <a id="_CPPv217beken_ms_per_tickv"></a> <a id="beken_ms_per_tick__void"></a> <a id="group__BEKEN__RTOS__TIMER_1ga23c0017105e1257e26074724a28a8329"></a> uint32\_t beken\_ms\_per\_tick(void)
:   Gets time in miiliseconds since RTOS start.

    备注

    : Since this is only 32 bits, it will roll over every 49 days, 17 hours.

    返回
    :   Time in milliseconds since RTOS started.

<a id="_CPPv415rtos_init_timerP13beken_timer_t8uint32_t15timer_handler_tPv"></a>

<a id="_CPPv315rtos_init_timerP13beken_timer_t8uint32_t15timer_handler_tPv"></a> <a id="_CPPv215rtos_init_timerP13beken_timer_t8uint32_t15timer_handler_tPv"></a> <a id="rtos_init_timer__beken_timer_tP.uint32_t.timer_handler_t.voidP"></a> <a id="group__BEKEN__RTOS__TIMER_1ga977f803c06c250aff5299b621dd444de"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_init\_timer([beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") \*timer, uint32\_t time\_ms, [timer\_handler\_t](#_CPPv415timer_handler_t "timer_handler_t") function, void \*arg)
:   Initialize a RTOS periodic timer.

    备注

    Timer does not start running until beken\_start\_timer is called and the timer will execute periodically

    参数
    :   - **timer** – : a pointer to the timer handle to be initialised
        - **time\_ms** – : Timer period in milliseconds
        - **function** – : the callback handler function that is called each time the timer expires
        - **arg** – : an argument that will be passed to the callback function

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv416rtos_start_timerP13beken_timer_t"></a>

<a id="_CPPv316rtos_start_timerP13beken_timer_t"></a> <a id="_CPPv216rtos_start_timerP13beken_timer_t"></a> <a id="rtos_start_timer__beken_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1gaec7a35eff26a31a6e861f783bee466ce"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_start\_timer([beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") \*timer)
:   Starts a RTOS periodic timer.

    备注

    Timer must have been previously initialised with [rtos\_init\_timer](#group__BEKEN__RTOS__TIMER_1ga977f803c06c250aff5299b621dd444de) This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   **timer** – : a pointer to the timer handle to start

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv415rtos_stop_timerP13beken_timer_t"></a>

<a id="_CPPv315rtos_stop_timerP13beken_timer_t"></a> <a id="_CPPv215rtos_stop_timerP13beken_timer_t"></a> <a id="rtos_stop_timer__beken_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1ga33b56fb5008be9260b603b22bba201c1"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_stop\_timer([beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") \*timer)
:   Stops a running RTOS periodic timer.

    备注

    Timer must have been previously started with [rtos\_init\_timer](#group__BEKEN__RTOS__TIMER_1ga977f803c06c250aff5299b621dd444de). This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   **timer** – : a pointer to the timer handle to stop

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv417rtos_reload_timerP13beken_timer_t"></a>

<a id="_CPPv317rtos_reload_timerP13beken_timer_t"></a> <a id="_CPPv217rtos_reload_timerP13beken_timer_t"></a> <a id="rtos_reload_timer__beken_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1gaaf92084b94397ae5cf34edf349c2ab07"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_reload\_timer([beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") \*timer)
:   Reloads a RTOS periodic timer that has expired.

    备注

    This is usually called in the timer callback handler, to reschedule the timer for the next period. This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   **timer** – : a pointer to the timer handle to reload

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv417rtos_deinit_timerP13beken_timer_t"></a>

<a id="_CPPv317rtos_deinit_timerP13beken_timer_t"></a> <a id="_CPPv217rtos_deinit_timerP13beken_timer_t"></a> <a id="rtos_deinit_timer__beken_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1ga99100dd7f4342dc7f2545b21b6567fe8"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_deinit\_timer([beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") \*timer)
:   De-initialise a RTOS periodic timer.

    备注

    Deletes a RTOS timer created with [rtos\_init\_timer](#group__BEKEN__RTOS__TIMER_1ga977f803c06c250aff5299b621dd444de). do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv418rtos_is_timer_initP13beken_timer_t"></a>

<a id="_CPPv318rtos_is_timer_initP13beken_timer_t"></a> <a id="_CPPv218rtos_is_timer_initP13beken_timer_t"></a> <a id="rtos_is_timer_init__beken_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1ga24e8e8b833e339d685356e42a4f7942d"></a> bool rtos\_is\_timer\_init([beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") \*timer)
:   Check if an RTOS periodic timer is init.

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   true : if init.

    返回
    :   false : if not init

<a id="_CPPv421rtos_is_timer_runningP13beken_timer_t"></a>

<a id="_CPPv321rtos_is_timer_runningP13beken_timer_t"></a> <a id="_CPPv221rtos_is_timer_runningP13beken_timer_t"></a> <a id="rtos_is_timer_running__beken_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1gaca5ad2aaec6bfa60ae4739a08c463084"></a> bool rtos\_is\_timer\_running([beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") \*timer)
:   Check if an RTOS periodic timer is running.

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   true : if running.

    返回
    :   false : if not running

<a id="_CPPv423rtos_init_oneshot_timerP14beken2_timer_t8uint32_t16timer_2handler_tPvPv"></a>

<a id="_CPPv323rtos_init_oneshot_timerP14beken2_timer_t8uint32_t16timer_2handler_tPvPv"></a> <a id="_CPPv223rtos_init_oneshot_timerP14beken2_timer_t8uint32_t16timer_2handler_tPvPv"></a> <a id="rtos_init_oneshot_timer__beken2_timer_tP.uint32_t.timer_2handler_t.voidP.voidP"></a> <a id="group__BEKEN__RTOS__TIMER_1gad0584724261ba4d9b4835bdcbc3b7203"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_init\_oneshot\_timer([beken2\_timer\_t](#_CPPv414beken2_timer_t "beken2_timer_t") \*timer, uint32\_t time\_ms, [timer\_2handler\_t](#_CPPv416timer_2handler_t "timer_2handler_t") function, void \*larg, void \*rarg)
:   Initialize a RTOS oneshot timer.

    备注

    Timer does not start running until [rtos\_start\_oneshot\_timer](#group__BEKEN__RTOS__TIMER_1gaeaaae9363d21adfd6e4dc1bf0135c72a) is called and the timer will only execute once

    参数
    :   - **timer** – : a pointer to the timer handle to be initialised
        - **time\_ms** – : Timer period in milliseconds
        - **function** – : the callback handler function that is called each time the timer expires
        - **larg** – : an argument that will be passed to the callback function
        - **rarg** – : an argument that will be passed to the callback function

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv425rtos_deinit_oneshot_timerP14beken2_timer_t"></a>

<a id="_CPPv325rtos_deinit_oneshot_timerP14beken2_timer_t"></a> <a id="_CPPv225rtos_deinit_oneshot_timerP14beken2_timer_t"></a> <a id="rtos_deinit_oneshot_timer__beken2_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1ga0dc913cfe482ea4ae34ad229a9ce25da"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_deinit\_oneshot\_timer([beken2\_timer\_t](#_CPPv414beken2_timer_t "beken2_timer_t") \*timer)
:   De-initialise a RTOS rtos\_init\_oneshot\_timer timer.

    备注

    Deletes a RTOS timer created with [rtos\_init\_oneshot\_timer](#group__BEKEN__RTOS__TIMER_1gad0584724261ba4d9b4835bdcbc3b7203). do not call this API when interrupts are disabled (may cause the system to enter a deadlock or abnormal status)

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv424rtos_start_oneshot_timerP14beken2_timer_t"></a>

<a id="_CPPv324rtos_start_oneshot_timerP14beken2_timer_t"></a> <a id="_CPPv224rtos_start_oneshot_timerP14beken2_timer_t"></a> <a id="rtos_start_oneshot_timer__beken2_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1gaeaaae9363d21adfd6e4dc1bf0135c72a"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_start\_oneshot\_timer([beken2\_timer\_t](#_CPPv414beken2_timer_t "beken2_timer_t") \*timer)
:   start a RTOS oneshot timer

    备注

    Timer must have been previously started with [rtos\_init\_oneshot\_timer](#group__BEKEN__RTOS__TIMER_1gad0584724261ba4d9b4835bdcbc3b7203). This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv423rtos_stop_oneshot_timerP14beken2_timer_t"></a>

<a id="_CPPv323rtos_stop_oneshot_timerP14beken2_timer_t"></a> <a id="_CPPv223rtos_stop_oneshot_timerP14beken2_timer_t"></a> <a id="rtos_stop_oneshot_timer__beken2_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1ga2cec3aa98fc55950f5344e80adefadb7"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_stop\_oneshot\_timer([beken2\_timer\_t](#_CPPv414beken2_timer_t "beken2_timer_t") \*timer)
:   stop a RTOS oneshot timer

    备注

    Timer must have been previously started with [rtos\_init\_oneshot\_timer](#group__BEKEN__RTOS__TIMER_1gad0584724261ba4d9b4835bdcbc3b7203). This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv429rtos_is_oneshot_timer_runningP14beken2_timer_t"></a>

<a id="_CPPv329rtos_is_oneshot_timer_runningP14beken2_timer_t"></a> <a id="_CPPv229rtos_is_oneshot_timer_runningP14beken2_timer_t"></a> <a id="rtos_is_oneshot_timer_running__beken2_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1gaddf8d7846580e4c3aaeb73f0c87c414b"></a> bool rtos\_is\_oneshot\_timer\_running([beken2\_timer\_t](#_CPPv414beken2_timer_t "beken2_timer_t") \*timer)
:   Check if an RTOS oneshot timer is running.

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   true : if running.

    返回
    :   false : if not running

<a id="_CPPv426rtos_is_oneshot_timer_initP14beken2_timer_t"></a>

<a id="_CPPv326rtos_is_oneshot_timer_initP14beken2_timer_t"></a> <a id="_CPPv226rtos_is_oneshot_timer_initP14beken2_timer_t"></a> <a id="rtos_is_oneshot_timer_init__beken2_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1ga30455192b80aea587c7a5a37cca41c05"></a> bool rtos\_is\_oneshot\_timer\_init([beken2\_timer\_t](#_CPPv414beken2_timer_t "beken2_timer_t") \*timer)
:   Check if an RTOS oneshot timer is initialised.

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   true : if initialised

    返回
    :   false : if not initialised

<a id="_CPPv425rtos_oneshot_reload_timerP14beken2_timer_t"></a>

<a id="_CPPv325rtos_oneshot_reload_timerP14beken2_timer_t"></a> <a id="_CPPv225rtos_oneshot_reload_timerP14beken2_timer_t"></a> <a id="rtos_oneshot_reload_timer__beken2_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1ga1e85d81bdaa964ebda0db01993103d68"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_oneshot\_reload\_timer([beken2\_timer\_t](#_CPPv414beken2_timer_t "beken2_timer_t") \*timer)
:   re-starts a oneshot timer

    备注

    Timer must have been previously started with [rtos\_init\_oneshot\_timer](#group__BEKEN__RTOS__TIMER_1gad0584724261ba4d9b4835bdcbc3b7203). This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv418rtos_change_periodP13beken_timer_t8uint32_t"></a>

<a id="_CPPv318rtos_change_periodP13beken_timer_t8uint32_t"></a> <a id="_CPPv218rtos_change_periodP13beken_timer_t8uint32_t"></a> <a id="rtos_change_period__beken_timer_tP.uint32_t"></a> <a id="group__BEKEN__RTOS__TIMER_1ga924e60d3e44e584d4440e1356dd724c4"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_change\_period([beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") \*timer, uint32\_t time\_ms)
:   changes the period of a oneshot timer

    备注

    Timer must have been previously started with [rtos\_init\_oneshot\_timer](#group__BEKEN__RTOS__TIMER_1gad0584724261ba4d9b4835bdcbc3b7203). This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv428rtos_oneshot_reload_timer_exP14beken2_timer_t8uint32_t16timer_2handler_tPvPv"></a>

<a id="_CPPv328rtos_oneshot_reload_timer_exP14beken2_timer_t8uint32_t16timer_2handler_tPvPv"></a> <a id="_CPPv228rtos_oneshot_reload_timer_exP14beken2_timer_t8uint32_t16timer_2handler_tPvPv"></a> <a id="rtos_oneshot_reload_timer_ex__beken2_timer_tP.uint32_t.timer_2handler_t.voidP.voidP"></a> <a id="group__BEKEN__RTOS__TIMER_1gacd1fd95242797989f32ab800e8c0696c"></a> [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") rtos\_oneshot\_reload\_timer\_ex([beken2\_timer\_t](#_CPPv414beken2_timer_t "beken2_timer_t") \*timer, uint32\_t time\_ms, [timer\_2handler\_t](#_CPPv416timer_2handler_t "timer_2handler_t") function, void \*larg, void \*rarg)
:   changes the period of a oneshot timer then re-start it

    备注

    Timer must have been previously started with [rtos\_init\_oneshot\_timer](#group__BEKEN__RTOS__TIMER_1gad0584724261ba4d9b4835bdcbc3b7203). This API can be called in task context and interrupt context. However when calling this API in task context,the interrupt cannot be turned off(may cause the system to enter a deadlock or abnormal status)

    参数
    :   - **timer** – : a pointer to the RTOS timer handle
        - **time\_ms** – : Timer period in milliseconds
        - **function** – : the callback handler function that is called each time the timer expires
        - **larg** – : an argument that will be passed to the callback function
        - **rarg** – : an argument that will be passed to the callback function

    返回
    :   kNoErr : on success.

    返回
    :   kGeneralErr : if an error occurred

<a id="_CPPv426rtos_get_timer_expiry_timeP13beken_timer_t"></a>

<a id="_CPPv326rtos_get_timer_expiry_timeP13beken_timer_t"></a> <a id="_CPPv226rtos_get_timer_expiry_timeP13beken_timer_t"></a> <a id="rtos_get_timer_expiry_time__beken_timer_tP"></a> <a id="group__BEKEN__RTOS__TIMER_1ga28703fcc45fb5e36314d4595a39576e4"></a> uint32\_t rtos\_get\_timer\_expiry\_time([beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") \*timer)
:   Returns the time in ticks at which the timer will expire.

    参数
    :   **timer** – : a pointer to the RTOS timer handle

    返回
    :   If the timer is running then the time in ticks at which the timer will next expire is returned. If the timer is not running then the return value is undefined.

<a id="_CPPv420rtos_start_schedulerv"></a>

<a id="_CPPv320rtos_start_schedulerv"></a> <a id="_CPPv220rtos_start_schedulerv"></a> <a id="rtos_start_scheduler__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gac343e700239fe05a50f3b107a185d737"></a> void rtos\_start\_scheduler(void)
:   Starts the real time kernel tick processing. After calling the kernel has control over which tasks are executed and when.

<a id="_CPPv425rtos_is_scheduler_startedv"></a>

<a id="_CPPv325rtos_is_scheduler_startedv"></a> <a id="_CPPv225rtos_is_scheduler_startedv"></a> <a id="rtos_is_scheduler_started__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gab309102020c44fe7241a0074830adf11"></a> bool rtos\_is\_scheduler\_started(void)
:   check if the rtos scheduler is running or not

<a id="_CPPv413rtos_get_namev"></a>

<a id="_CPPv313rtos_get_namev"></a> <a id="_CPPv213rtos_get_namev"></a> <a id="rtos_get_name__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga9f3137c561965bae599fc4493146e38c"></a> char \*rtos\_get\_name(void)
:   get the name of the currently used OS

<a id="_CPPv416rtos_get_versionv"></a>

<a id="_CPPv316rtos_get_versionv"></a> <a id="_CPPv216rtos_get_versionv"></a> <a id="rtos_get_version__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga09e470bf819aa927311a648ba9630ce0"></a> char \*rtos\_get\_version(void)
:   get the version of the currently used OS

<a id="_CPPv424rtos_get_total_heap_sizev"></a>

<a id="_CPPv324rtos_get_total_heap_sizev"></a> <a id="_CPPv224rtos_get_total_heap_sizev"></a> <a id="rtos_get_total_heap_size__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gaa723114ac74e2cb593c81db3fd3e0f3e"></a> size\_t rtos\_get\_total\_heap\_size(void)
:   get the total heap size

    返回
    :   the amount of total heap space available on the system

<a id="_CPPv423rtos_get_free_heap_sizev"></a>

<a id="_CPPv323rtos_get_free_heap_sizev"></a> <a id="_CPPv223rtos_get_free_heap_sizev"></a> <a id="rtos_get_free_heap_size__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gaf4261e2bbd703465004b6bc0f05bf508"></a> size\_t rtos\_get\_free\_heap\_size(void)
:   get the free heap size

    返回
    :   the amount of left heap space available on the system

<a id="_CPPv431rtos_get_minimum_free_heap_sizev"></a>

<a id="_CPPv331rtos_get_minimum_free_heap_sizev"></a> <a id="_CPPv231rtos_get_minimum_free_heap_sizev"></a> <a id="rtos_get_minimum_free_heap_size__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga7b21d594c1adebc1829f8b4ee6d0e883"></a> size\_t rtos\_get\_minimum\_free\_heap\_size(void)
:   get the minimum heap size

    返回
    :   the minimum value remaining during the system heap space usage

<a id="_CPPv430rtos_get_psram_total_heap_sizev"></a>

<a id="_CPPv330rtos_get_psram_total_heap_sizev"></a> <a id="_CPPv230rtos_get_psram_total_heap_sizev"></a> <a id="rtos_get_psram_total_heap_size__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gadda1e17aec544bc8cd25d0e1150a42e4"></a> size\_t rtos\_get\_psram\_total\_heap\_size(void)
:   get the total heap size in psram

    返回
    :   the amount of total heap space in psram

<a id="_CPPv429rtos_get_psram_free_heap_sizev"></a>

<a id="_CPPv329rtos_get_psram_free_heap_sizev"></a> <a id="_CPPv229rtos_get_psram_free_heap_sizev"></a> <a id="rtos_get_psram_free_heap_size__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gacf223f3a18b87f461b5c96df8d36d2af"></a> size\_t rtos\_get\_psram\_free\_heap\_size(void)
:   get the free heap size

    返回
    :   the amount of left heap space in psram

<a id="_CPPv437rtos_get_psram_minimum_free_heap_sizev"></a>

<a id="_CPPv337rtos_get_psram_minimum_free_heap_sizev"></a> <a id="_CPPv237rtos_get_psram_minimum_free_heap_sizev"></a> <a id="rtos_get_psram_minimum_free_heap_size__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gac4e43f0c3ee88775e1eb9b54cb702f0d"></a> size\_t rtos\_get\_psram\_minimum\_free\_heap\_size(void)
:   get the minimum heap size in psram

    返回
    :   the minimum value remaining in psram during the system heap space usage

<a id="_CPPv430rtos_get_hsram_total_heap_sizev"></a>

<a id="_CPPv330rtos_get_hsram_total_heap_sizev"></a> <a id="_CPPv230rtos_get_hsram_total_heap_sizev"></a> <a id="rtos_get_hsram_total_heap_size__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga40f4911e1da1d85df6663543cb233e0b"></a> size\_t rtos\_get\_hsram\_total\_heap\_size(void)
:   get the total heap size in hsram

    返回
    :   the amount of total heap space in hsram

<a id="_CPPv429rtos_get_hsram_free_heap_sizev"></a>

<a id="_CPPv329rtos_get_hsram_free_heap_sizev"></a> <a id="_CPPv229rtos_get_hsram_free_heap_sizev"></a> <a id="rtos_get_hsram_free_heap_size__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga7e130625ae67e41fd839109abdea65bc"></a> size\_t rtos\_get\_hsram\_free\_heap\_size(void)
:   get the free heap size in hsram

    返回
    :   the amount of left heap space in hsram

<a id="_CPPv437rtos_get_hsram_minimum_free_heap_sizev"></a>

<a id="_CPPv337rtos_get_hsram_minimum_free_heap_sizev"></a> <a id="_CPPv237rtos_get_hsram_minimum_free_heap_sizev"></a> <a id="rtos_get_hsram_minimum_free_heap_size__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gaa7c4ee355873e24ad541fdb3d22c512e"></a> size\_t rtos\_get\_hsram\_minimum\_free\_heap\_size(void)
:   get the minimum heap size in hsram

    返回
    :   the minimum value remaining in hsram during the system heap space usage

<a id="_CPPv419rtos_get_tick_countv"></a>

<a id="_CPPv319rtos_get_tick_countv"></a> <a id="_CPPv219rtos_get_tick_countv"></a> <a id="rtos_get_tick_count__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga76820a7d902e6af0ee9251d561834a32"></a> uint32\_t rtos\_get\_tick\_count(void)
:   get the os tick count

    返回
    :   The count of ticks since vTaskStartScheduler was called.

<a id="_CPPv416rtos_disable_intv"></a>

<a id="_CPPv316rtos_disable_intv"></a> <a id="_CPPv216rtos_disable_intv"></a> <a id="rtos_disable_int__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga99e8c6b5c91918fe9cfe5d1bed847761"></a> uint32\_t rtos\_disable\_int(void)
:   disable interrupts and return the current interrupt status

    备注

    disable interrupt support nesting

    返回
    :   the current interrupt status

<a id="_CPPv415rtos_enable_int8uint32_t"></a>

<a id="_CPPv315rtos_enable_int8uint32_t"></a> <a id="_CPPv215rtos_enable_int8uint32_t"></a> <a id="rtos_enable_int__uint32_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gaaa0099eff47f618846327600529b3499"></a> void rtos\_enable\_int(uint32\_t int\_level)
:   enable previously disabled interrupts

    备注

    this API needs to be used with [rtos\_disable\_int](#group__BEKEN__RTOS__SYSTEM_1ga99e8c6b5c91918fe9cfe5d1bed847761)

    参数
    :   **int\_level** – : saved interrupt status

    返回
    :   the current interrupt status

<a id="_CPPv417rtos_before_sleepv"></a>

<a id="_CPPv317rtos_before_sleepv"></a> <a id="_CPPv217rtos_before_sleepv"></a> <a id="rtos_before_sleep__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga337ed4402ef197934731b221521c5263"></a> uint32\_t rtos\_before\_sleep(void)
:   disable interrupts and return the current interrupt status

    备注

    disable interrupt support nesting. This API has the same functionality as [rtos\_disable\_int](#group__BEKEN__RTOS__SYSTEM_1ga99e8c6b5c91918fe9cfe5d1bed847761)

    返回
    :   the current interrupt status

<a id="_CPPv416rtos_after_sleep8uint32_t"></a>

<a id="_CPPv316rtos_after_sleep8uint32_t"></a> <a id="_CPPv216rtos_after_sleep8uint32_t"></a> <a id="rtos_after_sleep__uint32_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gae45d666c1f28d9532e04e480b6077d1c"></a> void rtos\_after\_sleep(uint32\_t int\_level)
:   enable previously disabled interrupts

    备注

    This API has the same functionality as [rtos\_enable\_int](#group__BEKEN__RTOS__SYSTEM_1gaaa0099eff47f618846327600529b3499)

    参数
    :   **int\_level** – : saved interrupt status

    返回
    :   the current interrupt status

<a id="_CPPv428rtos_is_in_interrupt_contextv"></a>

<a id="_CPPv328rtos_is_in_interrupt_contextv"></a> <a id="_CPPv228rtos_is_in_interrupt_contextv"></a> <a id="rtos_is_in_interrupt_context__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga8a975ad6dabc46dcb7067127f20fdcca"></a> bool rtos\_is\_in\_interrupt\_context(void)
:   Check if system in interrupt context.

    返回
    :   true : if in interrupt context

    返回
    :   false : if not in interrupt context

<a id="_CPPv423rtos_local_irq_disabledv"></a>

<a id="_CPPv323rtos_local_irq_disabledv"></a> <a id="_CPPv223rtos_local_irq_disabledv"></a> <a id="rtos_local_irq_disabled__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gab9d2bcbbf77973d15b9dce710a68095e"></a> bool rtos\_local\_irq\_disabled(void)
:   Check if local irq is disabled.

    返回
    :   true : if irq is disabled

    返回
    :   false : if irq is not disabled

<a id="_CPPv427rtos_is_scheduler_suspendedv"></a>

<a id="_CPPv327rtos_is_scheduler_suspendedv"></a> <a id="_CPPv227rtos_is_scheduler_suspendedv"></a> <a id="rtos_is_scheduler_suspended__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gaffda4f59b06ac3d3f2b6115cd1b70c40"></a> bool rtos\_is\_scheduler\_suspended(void)
:   Check if the current scheduler is in suspended state.

    返回
    :   true : the scheduler is in suspended state

    返回
    :   false : the scheduler is not in suspended state

<a id="_CPPv418rtos_setup_systick8uint32_t"></a>

<a id="_CPPv318rtos_setup_systick8uint32_t"></a> <a id="_CPPv218rtos_setup_systick8uint32_t"></a> <a id="rtos_setup_systick__uint32_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gab1a2d4e3673f0e2fc796d92880286582"></a> void rtos\_setup\_systick(uint32\_t cpu\_clock\_hz)
:   setup rtos systick

    参数
    :   **cpu\_clock\_hz** – : the cpu clock frequency

<a id="_CPPv413rtos_shutdownv"></a>

<a id="_CPPv313rtos_shutdownv"></a> <a id="_CPPv213rtos_shutdownv"></a> <a id="rtos_shutdown__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga7349127da1198d8abe3863010a0a482b"></a> void rtos\_shutdown(void)
:   disable interrupts and the run in an infinite loop

<a id="_CPPv416rtos_get_core_idv"></a>

<a id="_CPPv316rtos_get_core_idv"></a> <a id="_CPPv216rtos_get_core_idv"></a> <a id="rtos_get_core_id__void"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga414917cbf2ce93d6af012ebc4970d19b"></a> static inline uint32\_t rtos\_get\_core\_id(void)

<a id="structures"></a>

## Structures

<a id="_CPPv413beken_timer_t"></a>

<a id="_CPPv313beken_timer_t"></a> <a id="_CPPv213beken_timer_t"></a> <a id="beken_timer_t"></a> <a id="structbeken__timer__t"></a> struct beken\_timer\_t
:   OS timer handle struct type.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13beken_timer_t6handleE"></a>

    <a id="_CPPv3N13beken_timer_t6handleE"></a> <a id="_CPPv2N13beken_timer_t6handleE"></a> <a id="beken_timer_t::handle__voidP"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga12fe24abf24aea489271e1184c6a5809"></a> void \*handle
    :   OS timer handle pointer

    <a id="_CPPv4N13beken_timer_t8functionE"></a>

    <a id="_CPPv3N13beken_timer_t8functionE"></a> <a id="_CPPv2N13beken_timer_t8functionE"></a> <a id="beken_timer_t::function__timer_handler_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga7d2a649b91c90554fe1330ef5a643342"></a> [timer\_handler\_t](#_CPPv415timer_handler_t "timer_handler_t") function
    :   OS timer handle callback function

    <a id="_CPPv4N13beken_timer_t3argE"></a>

    <a id="_CPPv3N13beken_timer_t3argE"></a> <a id="_CPPv2N13beken_timer_t3argE"></a> <a id="beken_timer_t::arg__voidP"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga1049cfabfdaf7a3c80d26d7c20c8c095"></a> void \*arg
    :   OS timer handle callback argument

    <a id="_CPPv4N13beken_timer_t9stop_flagE"></a>

    <a id="_CPPv3N13beken_timer_t9stop_flagE"></a> <a id="_CPPv2N13beken_timer_t9stop_flagE"></a> <a id="beken_timer_t::stop_flag__uint32_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gab5261a5e6c79a12631925f9425f39021"></a> uint32\_t stop\_flag
    :   stop flag

    <a id="_CPPv4N13beken_timer_t11deinit_flagE"></a>

    <a id="_CPPv3N13beken_timer_t11deinit_flagE"></a> <a id="_CPPv2N13beken_timer_t11deinit_flagE"></a> <a id="beken_timer_t::deinit_flag__uint32_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga9fd34dae43fe6377f63db089b836e01d"></a> uint32\_t deinit\_flag
    :   deinit flag

<a id="_CPPv421beken_worker_thread_t"></a>

<a id="_CPPv321beken_worker_thread_t"></a> <a id="_CPPv221beken_worker_thread_t"></a> <a id="beken_worker_thread_t"></a> <a id="structbeken__worker__thread__t"></a> struct beken\_worker\_thread\_t
:   OS worker thread handle struct type.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21beken_worker_thread_t6threadE"></a>

    <a id="_CPPv3N21beken_worker_thread_t6threadE"></a> <a id="_CPPv2N21beken_worker_thread_t6threadE"></a> <a id="beken_worker_thread_t::thread__beken_thread_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga94146b3ee131d211bc51481433c79238"></a> [beken\_thread\_t](#_CPPv414beken_thread_t "beken_thread_t") thread
    :   OS thread handle

    <a id="_CPPv4N21beken_worker_thread_t11event_queueE"></a>

    <a id="_CPPv3N21beken_worker_thread_t11event_queueE"></a> <a id="_CPPv2N21beken_worker_thread_t11event_queueE"></a> <a id="beken_worker_thread_t::event_queue__beken_queue_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gaa8955f86b8c426b85b6ad029c9e51bd9"></a> [beken\_queue\_t](#_CPPv413beken_queue_t "beken_queue_t") event\_queue
    :   OS event queue

<a id="_CPPv419beken_timed_event_t"></a>

<a id="_CPPv319beken_timed_event_t"></a> <a id="_CPPv219beken_timed_event_t"></a> <a id="beken_timed_event_t"></a> <a id="structbeken__timed__event__t"></a> struct beken\_timed\_event\_t
:   OS timer event struct type.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19beken_timed_event_t8functionE"></a>

    <a id="_CPPv3N19beken_timed_event_t8functionE"></a> <a id="_CPPv2N19beken_timed_event_t8functionE"></a> <a id="beken_timed_event_t::function__event_handler_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gaf3f572c5168b661e71ccebe9051155e5"></a> [event\_handler\_t](#_CPPv415event_handler_t "event_handler_t") function
    :   OS event callback function

    <a id="_CPPv4N19beken_timed_event_t3argE"></a>

    <a id="_CPPv3N19beken_timed_event_t3argE"></a> <a id="_CPPv2N19beken_timed_event_t3argE"></a> <a id="beken_timed_event_t::arg__voidP"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga96e60248d73993bd208ed6f00c63cd1a"></a> void \*arg
    :   OS event callback argument

    <a id="_CPPv4N19beken_timed_event_t5timerE"></a>

    <a id="_CPPv3N19beken_timed_event_t5timerE"></a> <a id="_CPPv2N19beken_timed_event_t5timerE"></a> <a id="beken_timed_event_t::timer__beken_timer_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga578014269b25a33473eec63c7fce0774"></a> [beken\_timer\_t](#_CPPv413beken_timer_t "beken_timer_t") timer
    :   OS timer handle

    <a id="_CPPv4N19beken_timed_event_t6threadE"></a>

    <a id="_CPPv3N19beken_timed_event_t6threadE"></a> <a id="_CPPv2N19beken_timed_event_t6threadE"></a> <a id="beken_timed_event_t::thread__beken_worker_thread_tP"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gafa80c540e315df841a2026d6fb422b87"></a> [beken\_worker\_thread\_t](#_CPPv421beken_worker_thread_t "beken_worker_thread_t") \*thread
    :   OS work thread handle

<a id="_CPPv414beken2_timer_t"></a>

<a id="_CPPv314beken2_timer_t"></a> <a id="_CPPv214beken2_timer_t"></a> <a id="beken2_timer_t"></a> <a id="structbeken2__timer__t"></a> struct beken2\_timer\_t
:   OS timer handle struct type.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14beken2_timer_t6handleE"></a>

    <a id="_CPPv3N14beken2_timer_t6handleE"></a> <a id="_CPPv2N14beken2_timer_t6handleE"></a> <a id="beken2_timer_t::handle__voidP"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga7cc4dabb683b80271f2f7da5bce1bf14"></a> void \*handle
    :   OS timer handle pointer

    <a id="_CPPv4N14beken2_timer_t8functionE"></a>

    <a id="_CPPv3N14beken2_timer_t8functionE"></a> <a id="_CPPv2N14beken2_timer_t8functionE"></a> <a id="beken2_timer_t::function__timer_2handler_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gaa96785acb49768b6a14aa71d94b29e67"></a> [timer\_2handler\_t](#_CPPv416timer_2handler_t "timer_2handler_t") function
    :   OS timer handle callback function

    <a id="_CPPv4N14beken2_timer_t8left_argE"></a>

    <a id="_CPPv3N14beken2_timer_t8left_argE"></a> <a id="_CPPv2N14beken2_timer_t8left_argE"></a> <a id="beken2_timer_t::left_arg__voidP"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gac223f06841ffee96b441c3e708bc9342"></a> void \*left\_arg
    :   OS timer handle callback first argument

    <a id="_CPPv4N14beken2_timer_t9right_argE"></a>

    <a id="_CPPv3N14beken2_timer_t9right_argE"></a> <a id="_CPPv2N14beken2_timer_t9right_argE"></a> <a id="beken2_timer_t::right_arg__voidP"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gad6c58f04ff37ecdb144304812be16eb3"></a> void \*right\_arg
    :   OS timer handle callback second argument

    <a id="_CPPv4N14beken2_timer_t11beken_magicE"></a>

    <a id="_CPPv3N14beken2_timer_t11beken_magicE"></a> <a id="_CPPv2N14beken2_timer_t11beken_magicE"></a> <a id="beken2_timer_t::beken_magic__uint32_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gaebda675499e1aa39fde6fb17299b6ee0"></a> uint32\_t beken\_magic
    :   OS timer magic word

    <a id="_CPPv4N14beken2_timer_t9stop_flagE"></a>

    <a id="_CPPv3N14beken2_timer_t9stop_flagE"></a> <a id="_CPPv2N14beken2_timer_t9stop_flagE"></a> <a id="beken2_timer_t::stop_flag__uint32_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1gab267e3493f3470456e52d9de4f590ea2"></a> uint32\_t stop\_flag
    :   stop flag

    <a id="_CPPv4N14beken2_timer_t11deinit_flagE"></a>

    <a id="_CPPv3N14beken2_timer_t11deinit_flagE"></a> <a id="_CPPv2N14beken2_timer_t11deinit_flagE"></a> <a id="beken2_timer_t::deinit_flag__uint32_t"></a> <a id="group__BEKEN__RTOS__SYSTEM_1ga40f55c970b884e2b7bd9178df3007a49"></a> uint32\_t deinit\_flag
    :   deinit flag

<a id="macros"></a>

## Macros

<a id="c.RTOS_TAG"></a>

<a id="group__os__defines_1ga47f510aaf7457227d26f5d74242ef5ae"></a> RTOS\_TAG
:   OS log tag

<a id="c.RTOS_LOGI"></a>

<a id="group__os__defines_1ga1020d1c4f554e825bce53880f0cb179e"></a> RTOS\_LOGI(...)
:   Output OS Info log

<a id="c.RTOS_LOGW"></a>

<a id="group__os__defines_1gaa485e65eb3e5ffe9b7c5a7d2d931b6f2"></a> RTOS\_LOGW(...)
:   Output OS Warning log

<a id="c.RTOS_LOGE"></a>

<a id="group__os__defines_1ga9a78e5df49eeb2fc159264e18b3ee320"></a> RTOS\_LOGE(...)
:   Output OS Error log

<a id="c.RTOS_LOGD"></a>

<a id="group__os__defines_1ga4d992e457e193ab32ff1e3eafd930733"></a> RTOS\_LOGD(...)
:   Output OS Debug log

<a id="c.RTOS_LOGV"></a>

<a id="group__os__defines_1ga32b984372bcd004baa0414af25408b8c"></a> RTOS\_LOGV(...)
:   Output OS Verbose log

<a id="c.GLOBAL_INT_STOP"></a>

<a id="group__os__defines_1ga77a6612437e667b2dcd137a6b7f09c07"></a> GLOBAL\_INT\_STOP
:   os stop interrupt

<a id="c.GLOBAL_INT_DECLARATION"></a>

<a id="group__os__defines_1ga90288a8d7fab075f0bb896f79199a179"></a> GLOBAL\_INT\_DECLARATION()
:   os declaration interrupt status

<a id="c.GLOBAL_INT_DISABLE"></a>

<a id="group__os__defines_1gaf2dc82b4be76ae6c4c54d167412d643a"></a> GLOBAL\_INT\_DISABLE()
:   os read interrupt status and disable interrupt

<a id="c.GLOBAL_INT_RESTORE"></a>

<a id="group__os__defines_1gaafb58c366b3a81872748702d26f51c06"></a> GLOBAL\_INT\_RESTORE()
:   os restore interrupt status

<a id="c.RTOS_SUCCESS"></a>

<a id="group__os__defines_1gaa4192a67fef34ce34bcd83467e2b99a5"></a> RTOS\_SUCCESS
:   Return Success

<a id="c.RTOS_FAILURE"></a>

<a id="group__os__defines_1ga8c7a95d4c6ac7775ba48d9b3590eed06"></a> RTOS\_FAILURE
:   Return Failure

<a id="c.BEKEN_DEFAULT_WORKER_PRIORITY"></a>

<a id="group__os__defines_1ga6edba4eb2f1e1361a1e5bdd019a26ebf"></a> BEKEN\_DEFAULT\_WORKER\_PRIORITY
:   Default Worker Priority

<a id="c.BEKEN_APPLICATION_PRIORITY"></a>

<a id="group__os__defines_1ga0d00a202c61b5703cf69c2df77d99410"></a> BEKEN\_APPLICATION\_PRIORITY
:   Application Task Priority

<a id="c.NanosecondsPerSecond"></a>

<a id="group__os__defines_1gae7a936a25488398860ffa6fadf8de1a8"></a> NanosecondsPerSecond
:   Nanoseconds Per Second

<a id="c.MicrosecondsPerSecond"></a>

<a id="group__os__defines_1ga1b9feedf58bb26b841c8c95a1819a655"></a> MicrosecondsPerSecond
:   Microseconds Per Second

<a id="c.MillisecondsPerSecond"></a>

<a id="group__os__defines_1ga13f80e6e861611819b9a77297b7cec27"></a> MillisecondsPerSecond
:   Milliseconds Per Second

<a id="c.BEKEN_NEVER_TIMEOUT"></a>

<a id="group__os__defines_1gabed08d8cb8b1bea237404021f557fca3"></a> BEKEN\_NEVER\_TIMEOUT
:   Never Timeout

<a id="c.BEKEN_WAIT_FOREVER"></a>

<a id="group__os__defines_1ga5d97509ba4ef69628c839900f1aa1335"></a> BEKEN\_WAIT\_FOREVER
:   Wait Forever

<a id="c.BEKEN_NO_WAIT"></a>

<a id="group__os__defines_1ga46798109388453040704d7f0f2bf539b"></a> BEKEN\_NO\_WAIT
:   No Wait

<a id="c.NANOSECONDS"></a>

<a id="group__os__defines_1gae6ae95d0a02b44dfed6affb30634412a"></a> NANOSECONDS
:   Nanoseconds Per Milliseconds

<a id="c.MICROSECONDS"></a>

<a id="group__os__defines_1ga8f3b4ac82ea98ed2bfcd2285f2861a7a"></a> MICROSECONDS
:   Microseconds Per Milliseconds

<a id="c.MILLISECONDS"></a>

<a id="group__os__defines_1ga523f92e3a3a17c1f64110375785270ee"></a> MILLISECONDS
:   One Milliseconds

<a id="c.SECONDS"></a>

<a id="group__os__defines_1ga48fcf4f2eeef6769d588168d4ac2ab0e"></a> SECONDS
:   Milliseconds Per Second

<a id="c.MINUTES"></a>

<a id="group__os__defines_1ga84be9dcfa5a172ee83121620d15c8e29"></a> MINUTES
:   Milliseconds Per MINUTES

<a id="c.HOURS"></a>

<a id="group__os__defines_1ga212d0f839f6f7ca43ccde311f93d5892"></a> HOURS
:   Milliseconds Per HOURS

<a id="c.DAYS"></a>

<a id="group__os__defines_1gaa6aa2a2fb8f4380e680d5ecb81a7d319"></a> DAYS
:   Milliseconds Per DAYS

<a id="c.BEKEN_MAGIC_WORD"></a>

<a id="group__os__defines_1ga578346b2f5902e7440cd34128eb92496"></a> BEKEN\_MAGIC\_WORD
:   Beken Magic word

<a id="c.os_printf"></a>

<a id="os_8h_1a751d204d0c7e166a527475d79e803454"></a> os\_printf
:   OS printf, will be replace with RTOS\_LOGI later

<a id="c.os_null_printf"></a>

<a id="os_8h_1a48e21dbc387e8f6c01fc651e2cafe020"></a> os\_null\_printf
:   OS drop print string

<a id="c.rtos_init_semaphore_adv"></a>

<a id="os_8h_1a9edb01b01fe72cfc50b3706b7a7d1fc7"></a> rtos\_init\_semaphore\_adv
:   To be replace with rtos\_init\_semaphore\_ex

<a id="c.rtos_get_sema_count"></a>

<a id="os_8h_1aa40ecd776a947f4a6214d22772d0b735"></a> rtos\_get\_sema\_count
:   To be replace with rtos\_get\_semaphore\_count

<a id="c.CPU0_CORE_ID"></a>

<a id="group__BEKEN__RTOS__SYSTEM_1gafda82da2489598483dcef6ebda798531"></a> CPU0\_CORE\_ID

<a id="c.CPU1_CORE_ID"></a>

<a id="group__BEKEN__RTOS__SYSTEM_1gacb4d169f97698ce339c0efa0efb945b9"></a> CPU1\_CORE\_ID

<a id="c.CPU2_CORE_ID"></a>

<a id="group__BEKEN__RTOS__SYSTEM_1gaf5cdfca375bbf7e6fd501a5ee2a0fa48"></a> CPU2\_CORE\_ID

<a id="c.CPU3_CORE_ID"></a>

<a id="group__BEKEN__RTOS__SYSTEM_1gaf5bc2bde3e536e4303b8b9c010820cae"></a> CPU3\_CORE\_ID

<a id="c.portGET_CORE_ID"></a>

<a id="group__BEKEN__RTOS__SYSTEM_1gaf56cac3afabd5c354d28d1a9d22321cd"></a> portGET\_CORE\_ID()

<a id="type-definitions"></a>

## Type Definitions

<a id="_CPPv48bk_err_t"></a>

<a id="_CPPv38bk_err_t"></a> <a id="_CPPv28bk_err_t"></a> <a id="bk_err_t"></a> <a id="group__os__defines_1gaf44cdf0336aafb9cb2f7496f15f00a92"></a> typedef int bk\_err\_t
:   Return error code

<a id="_CPPv418beken_thread_arg_t"></a>

<a id="_CPPv318beken_thread_arg_t"></a> <a id="_CPPv218beken_thread_arg_t"></a> <a id="beken_thread_arg_t"></a> <a id="group__os__defines_1ga7b68adecdf88fec131f64670bcdf9d50"></a> typedef void \*beken\_thread\_arg\_t
:   Thread argument pointer type

<a id="_CPPv412beken_bool_t"></a>

<a id="_CPPv312beken_bool_t"></a> <a id="_CPPv212beken_bool_t"></a> <a id="beken_bool_t"></a> <a id="group__os__defines_1ga66afa86cb763bcc991283bfcfa3319d9"></a> typedef uint8\_t beken\_bool\_t
:   Bool type

<a id="_CPPv412beken_time_t"></a>

<a id="_CPPv312beken_time_t"></a> <a id="_CPPv212beken_time_t"></a> <a id="beken_time_t"></a> <a id="group__os__defines_1ga84d0409fd54c623c000dbd11984929a1"></a> typedef uint32\_t beken\_time\_t
:   Time value in milliseconds

<a id="_CPPv416beken_utc_time_t"></a>

<a id="_CPPv316beken_utc_time_t"></a> <a id="_CPPv216beken_utc_time_t"></a> <a id="beken_utc_time_t"></a> <a id="group__os__defines_1ga5292a0e6802c62d25cca886415af461a"></a> typedef uint32\_t beken\_utc\_time\_t
:   UTC Time in seconds

<a id="_CPPv419beken_utc_time_ms_t"></a>

<a id="_CPPv319beken_utc_time_ms_t"></a> <a id="_CPPv219beken_utc_time_ms_t"></a> <a id="beken_utc_time_ms_t"></a> <a id="group__os__defines_1ga553b9d25eff3344d06c147421de3d0b1"></a> typedef uint64\_t beken\_utc\_time\_ms\_t
:   UTC Time in milliseconds

<a id="_CPPv419beken_event_flags_t"></a>

<a id="_CPPv319beken_event_flags_t"></a> <a id="_CPPv219beken_event_flags_t"></a> <a id="beken_event_flags_t"></a> <a id="group__os__defines_1gaa76ad942e2d9a6fb3bf2c6c6c26a0994"></a> typedef uint32\_t beken\_event\_flags\_t
:   Event flag type

<a id="_CPPv417beken_semaphore_t"></a>

<a id="_CPPv317beken_semaphore_t"></a> <a id="_CPPv217beken_semaphore_t"></a> <a id="beken_semaphore_t"></a> <a id="group__os__defines_1ga26e2c92f7995168fc9d18816eb906035"></a> typedef void \*beken\_semaphore\_t
:   OS Semaphore handle pointer

<a id="_CPPv413beken_mutex_t"></a>

<a id="_CPPv313beken_mutex_t"></a> <a id="_CPPv213beken_mutex_t"></a> <a id="beken_mutex_t"></a> <a id="group__os__defines_1gab4743cb7776376b6a9604c7367829454"></a> typedef void \*beken\_mutex\_t
:   OS Mutex handle pointer

<a id="_CPPv414beken_thread_t"></a>

<a id="_CPPv314beken_thread_t"></a> <a id="_CPPv214beken_thread_t"></a> <a id="beken_thread_t"></a> <a id="group__os__defines_1gab6dce24aab1945e522e613a15ae533d9"></a> typedef void \*beken\_thread\_t
:   OS Thread handle pointer

<a id="_CPPv413beken_queue_t"></a>

<a id="_CPPv313beken_queue_t"></a> <a id="_CPPv213beken_queue_t"></a> <a id="beken_queue_t"></a> <a id="group__os__defines_1ga9d26c0386e03f4b1832fda3b7d56af5a"></a> typedef void \*beken\_queue\_t
:   OS Queue handle pointer

<a id="_CPPv413beken_event_t"></a>

<a id="_CPPv313beken_event_t"></a> <a id="_CPPv213beken_event_t"></a> <a id="beken_event_t"></a> <a id="group__os__defines_1ga99c038de095b4b5142a8863a6a5896c2"></a> typedef void \*beken\_event\_t
:   OS Event handle pointer

<a id="_CPPv415timer_handler_t"></a>

<a id="_CPPv315timer_handler_t"></a> <a id="_CPPv215timer_handler_t"></a> <a id="timer_handler_t"></a> <a id="group__os__defines_1ga6b46be086e6bf9ab555a04177ad47953"></a> typedef void (\*timer\_handler\_t)(void\*)
:   timer callback function type with one parameter

<a id="_CPPv416timer_2handler_t"></a>

<a id="_CPPv316timer_2handler_t"></a> <a id="_CPPv216timer_2handler_t"></a> <a id="timer_2handler_t"></a> <a id="group__os__defines_1gab7d12040bc02ac53af6123ab02f67c27"></a> typedef void (\*timer\_2handler\_t)(void \*Larg, void \*Rarg)
:   timer callback function type with two parameters

<a id="_CPPv415event_handler_t"></a>

<a id="_CPPv315event_handler_t"></a> <a id="_CPPv215event_handler_t"></a> <a id="event_handler_t"></a> <a id="group__os__defines_1gaabd70961549830cb36e06cf8ce8ffc1c"></a> typedef [bk\_err\_t](#_CPPv48bk_err_t "bk_err_t") (\*event\_handler\_t)(void \*arg)
:   event callback function type with one parameter

<a id="_CPPv423beken_thread_function_t"></a>

<a id="_CPPv323beken_thread_function_t"></a> <a id="_CPPv223beken_thread_function_t"></a> <a id="beken_thread_function_t"></a> <a id="group__os__defines_1ga524d59438407f94061e6bf969128f0f9"></a> typedef void (\*beken\_thread\_function\_t)([beken\_thread\_arg\_t](#_CPPv418beken_thread_arg_t "beken_thread_arg_t") arg)
:   OS Thread entry function type.

<a id="enumerations"></a>

## Enumerations

<a id="_CPPv431beken_event_flags_wait_option_t"></a>

<a id="_CPPv331beken_event_flags_wait_option_t"></a> <a id="_CPPv231beken_event_flags_wait_option_t"></a> <a id="group__os__defines_1ga537519574455314eee0adc96793e9086"></a> enum beken\_event\_flags\_wait\_option\_t
:   OS Event wait options.

    *Values:*

    <a id="_CPPv4N31beken_event_flags_wait_option_t18WAIT_FOR_ANY_EVENTE"></a>

    <a id="_CPPv3N31beken_event_flags_wait_option_t18WAIT_FOR_ANY_EVENTE"></a> <a id="_CPPv2N31beken_event_flags_wait_option_t18WAIT_FOR_ANY_EVENTE"></a> <a id="group__os__defines_1gga537519574455314eee0adc96793e9086a8c3165534f07880b25884c46107b8a1c"></a> enumerator WAIT\_FOR\_ANY\_EVENT
    :   Wait for any event

    <a id="_CPPv4N31beken_event_flags_wait_option_t19WAIT_FOR_ALL_EVENTSE"></a>

    <a id="_CPPv3N31beken_event_flags_wait_option_t19WAIT_FOR_ALL_EVENTSE"></a> <a id="_CPPv2N31beken_event_flags_wait_option_t19WAIT_FOR_ALL_EVENTSE"></a> <a id="group__os__defines_1gga537519574455314eee0adc96793e9086a3081a759548332d16875ae346c5714f4"></a> enumerator WAIT\_FOR\_ALL\_EVENTS
    :   Wait for all event
