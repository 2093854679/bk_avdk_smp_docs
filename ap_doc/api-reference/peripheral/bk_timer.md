# Timer



## Timer API Status

| API | BK7259_AP |
| --- | --- |
| [`bk_timer_driver_init()`](#_CPPv420bk_timer_driver_initv "bk_timer_driver_init") | Y |
| [`bk_timer_driver_deinit()`](#_CPPv422bk_timer_driver_deinitv "bk_timer_driver_deinit") | Y |
| [`bk_timer_start()`](#_CPPv414bk_timer_start10timer_id_t8uint32_t11timer_isr_t "bk_timer_start") | Y |
| [`bk_timer_stop()`](#_CPPv413bk_timer_stop10timer_id_t "bk_timer_stop") | Y |
| [`bk_timer_get_cnt()`](#_CPPv416bk_timer_get_cnt10timer_id_t "bk_timer_get_cnt") | Y |
| [`bk_timer_enable()`](#_CPPv415bk_timer_enable10timer_id_t "bk_timer_enable") | Y |
| [`bk_timer_disable()`](#_CPPv416bk_timer_disable10timer_id_t "bk_timer_disable") | Y |
| [`bk_timer_get_period()`](#_CPPv419bk_timer_get_period10timer_id_t "bk_timer_get_period") | Y |
| [`bk_timer_start_us()`](#_CPPv417bk_timer_start_us10timer_id_t8uint64_t11timer_isr_t "bk_timer_start_us") | Y |
| [`bk_timer_start_without_callback()`](#_CPPv431bk_timer_start_without_callback10timer_id_t8uint32_t "bk_timer_start_without_callback") | Y |
| [`bk_timer_get_enable_status()`](#_CPPv426bk_timer_get_enable_statusv "bk_timer_get_enable_status") | Y |
| [`bk_timer_is_interrupt_triggered()`](#_CPPv431bk_timer_is_interrupt_triggered10timer_id_t "bk_timer_is_interrupt_triggered") | Y |
| [`bk_timer_get_time()`](#_CPPv417bk_timer_get_time10timer_id_t8uint32_t8uint32_t18timer_value_unit_t "bk_timer_get_time") | Y |
| [`bk_timer_delay_with_callback()`](#_CPPv428bk_timer_delay_with_callback10timer_id_t8uint64_t11timer_isr_t "bk_timer_delay_with_callback") | Y |
| [`bk_timer_cancel()`](#_CPPv415bk_timer_cancel10timer_id_t "bk_timer_cancel") | Y |


## Timer API Reference


### Header File


- [timer.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/timer.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/timer.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_driver_init(void)
:   Init the timer driver.

    This API init the resoure common to all timer channels:


    - Init timer driver control memory

    This API should be called before any other timer APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_driver_deinit(void)
:   Deinit the timer driver.

    This API free all resource related to timer and power down all timer channels.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_start([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id, uint32_t time_ms, [timer_isr_t](#_CPPv411timer_isr_t "timer_isr_t") callback)
:   Start the timer.


    **Attention**
    :   1. timer2 has been used for time cali


    **Attention**
    :   2. timer3 has been used for clock, but bk7271 use timer1


    **Attention**
    :   3. bk7271 has used timer0(10ms)

    参数
    :   - **timer_id** – the timer ID to be started

        - **time_ms** – time delay value of the timer

        - **callback** – the timer call back function

    返回
    :   - BK_OK: succeed

        - BK_ERR_TIMER_NOT_INIT: timer driver not init

        - BK_ERR_TIMER_ID: timer id is invalid

        - BK_ERR_TIMER_IS_RUNNING: timer id is running

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_start_us([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id, uint64_t time_us, [timer_isr_t](#_CPPv411timer_isr_t "timer_isr_t") callback)
:   Start the timer.

    参数
    :   - **timer_id** – the timer ID to be started

        - **time_us** – time delay value of the timer, the unit is us

        - **callback** – the timer call back function

    返回
    :   - BK_OK: succeed

        - BK_ERR_TIMER_NOT_INIT: timer driver not init

        - BK_ERR_TIMER_ID: timer id is invalid

        - BK_ERR_TIMER_IS_RUNNING: timer id is running

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_start_without_callback([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id, uint32_t time_ms)
:   Start the timer without set callback.

    参数
    :   - **timer_id** – the timer ID to be started

        - **timer_ms** – time delay value of the timer

    返回
    :   - BK_OK: succeed

        - others: others errors

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_stop([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id)
:   Stop the timer.

    参数
    :   **timer_id** – the timer ID to be stoped

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_timer_get_cnt([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id)
:   Get the current counter value.


    **Attention**
    :   1. The caller need to make sure the parameter timer_id is correct!

    参数
    :   **timer_id** – the timer id

    返回
    :   counter value

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_enable([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id)
:   Enable the timer.

    参数
    :   **timer_id** – the timer ID

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_disable([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id)
:   Disable the timer.

    参数
    :   **timer_id** – the timer ID

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_timer_get_period([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id)
:   Get the counter value set by [bk_timer_start()](#group__bk__api__timer_1gafd8412ab7d4698fde8a944c39551c749 "#group__bk__api__timer_1gafd8412ab7d4698fde8a944c39551c749")

    参数
    :   **timer_id** – the timer id

    返回
    :   counter value set by [bk_timer_start()](#group__bk__api__timer_1gafd8412ab7d4698fde8a944c39551c749 "#group__bk__api__timer_1gafd8412ab7d4698fde8a944c39551c749")

uint32_t bk_timer_get_enable_status(void)
:   Get the timer enable status.

    参数
    :   **timer_id** – the timer id

    返回
    :   timer enable status

bool bk_timer_is_interrupt_triggered([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id)
:   Get whether the timer interrupt triggered.

    参数
    :   **timer_id** – the timer id

    返回
    :   the timer interrupt status

uint64_t bk_timer_get_time([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id, uint32_t div, uint32_t last_count, [timer_value_unit_t](#_CPPv418timer_value_unit_t "timer_value_unit_t") unit_type)
:   Get the timer count value in ms or us.

    参数
    :   - **timer_id** – the timer id

        - **div** – the divider of clock frequency

        - **last_count** – last count of the timer

        - **timer_value_unit_t** – the time unit, ms or us

    返回
    :   the timer value in micro seconds

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_delay_with_callback([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id, uint64_t time_us, [timer_isr_t](#_CPPv411timer_isr_t "timer_isr_t") callback)
:   This function set the delay based on the current running counter, which is different from bk_timer_start.

    参数
    :   - **timer_id** – the timer id

        - **time_us** – time delay value of the timer by us

        - **callback** – the timer delay call back function

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_timer_cancel([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id)
:   Cancel the timer delay task, reset timer and set ISR to NULL, it will not disable the timer, which is different from bk_timer_stop.

    参数
    :   **timer_id** – the timer id

    返回
    :   - BK_OK: succeed

        - others: other errors.


## Timer API Typedefs


### Header File


- [timer_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/timer_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/timer_types.h")


### Macros

BK_ERR_TIMER_ID
:   timer id is invalid

BK_ERR_TIMER_NOT_INIT
:   timer driver not init

BK_ERR_TIMER_IS_RUNNING
:   timer id is running

BK_ERR_TIMER_ID_ON_DEFCONFIG
:   timer id is error


### Type Definitions

typedef void (*timer_isr_t)([timer_id_t](#_CPPv410timer_id_t "timer_id_t") timer_id)
:   Timer interrupt service routine.


### Header File


- [hal/hal_timer_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_timer_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_timer_types.h")


### Macros

TIMER_CLOCK_FREQ_26M

TIMER_CLOCK_FREQ_32K


### Type Definitions

typedef uint8_t timer_unit_t
:   Timer uint id


### Enumerations

enum timer_src_clk_t
:   *Values:*

    enumerator TIMER_SCLK_CLK32
    :   TIMER source clock dco

    enumerator TIMER_SCLK_XTAL
    :   TIMER source clock xtal 26M

enum sys_sel_timer_t
:   *Values:*

    enumerator SYS_SEL_TIMER0

    enumerator SYS_SEL_TIMER1

enum timer_id_t
:   *Values:*

    enumerator TIMER_ID0
    :   TIMER id 0

    enumerator TIMER_ID1
    :   TIMER id 1

    enumerator TIMER_ID2
    :   TIMER id 2

    enumerator TIMER_ID3
    :   TIMER id 3

    enumerator TIMER_ID4
    :   TIMER id 4

    enumerator TIMER_ID5
    :   TIMER id 5

    enumerator TIMER_ID6
    :   TIMER id 6 - temporary NOT SUPPORTED on AP

    enumerator TIMER_ID7
    :   TIMER id 7 - temporary NOT SUPPORTED on AP

    enumerator TIMER_ID8
    :   TIMER id 8 - temporary NOT SUPPORTED on AP

    enumerator TIMER_ID9
    :   TIMER id 9 - temporary NOT SUPPORTED on AP

    enumerator TIMER_ID10
    :   TIMER id 10 - temporary NOT SUPPORTED on AP

    enumerator TIMER_ID11
    :   TIMER id 11 - temporary NOT SUPPORTED on AP

    enumerator TIMER_ID12
    :   TIMER id 12 - maps to TIMER-4 channel 0

    enumerator TIMER_ID13
    :   TIMER id 13 - maps to TIMER-4 channel 1

    enumerator TIMER_ID14
    :   TIMER id 14 - maps to TIMER-4 channel 2

    enumerator TIMER_ID15
    :   TIMER id 15 - maps to TIMER-5 channel 0

    enumerator TIMER_ID16
    :   TIMER id 16 - maps to TIMER-5 channel 1

    enumerator TIMER_ID17
    :   TIMER id 17 - maps to TIMER-5 channel 2

    enumerator TIMER_ID_MAX
    :   TIMER id max

enum timer_value_unit_t
:   *Values:*

    enumerator TIMER_UNIT_MS
    :   TIMER unit type is ms

    enumerator TIMER_UNIT_US
    :   TIMER unit type is us
