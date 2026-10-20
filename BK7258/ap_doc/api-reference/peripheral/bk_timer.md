---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_timer.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="timer"></a>

# Timer

<a id="timer-api-status"></a>

## Timer API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_timer_driver_init()`](#_CPPv420bk_timer_driver_initv "bk_timer_driver_init") | Y |
| [`bk_timer_driver_deinit()`](#_CPPv422bk_timer_driver_deinitv "bk_timer_driver_deinit") | Y |
| [`bk_timer_start()`](#_CPPv414bk_timer_start10timer_id_t8uint32_t11timer_isr_t "bk_timer_start") | Y |
| [`bk_timer_stop()`](#_CPPv413bk_timer_stop10timer_id_t "bk_timer_stop") | Y |
| [`bk_timer_get_cnt()`](#_CPPv416bk_timer_get_cnt10timer_id_t "bk_timer_get_cnt") | Y |
| [`bk_timer_enable()`](#_CPPv415bk_timer_enable10timer_id_t "bk_timer_enable") | Y |
| [`bk_timer_disable()`](#_CPPv416bk_timer_disable10timer_id_t "bk_timer_disable") | Y |
| [`bk_timer_get_period()`](#_CPPv419bk_timer_get_period10timer_id_t "bk_timer_get_period") | Y |

<a id="timer-api-reference"></a>

## Timer API Reference

<a id="header-file"></a>

### Header File

- [timer.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/timer.h)

<a id="functions"></a>

### Functions

<a id="_CPPv420bk_timer_driver_initv"></a>

<a id="_CPPv320bk_timer_driver_initv"></a> <a id="_CPPv220bk_timer_driver_initv"></a> <a id="bk_timer_driver_init__void"></a> <a id="group__bk__api__timer_1ga85bd981349ef22cd84c49f9294d01b5c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_timer\_driver\_init(void)
:   Init the timer driver.

    This API init the resoure common to all timer channels:

    - Init timer driver control memory

    This API should be called before any other timer APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_timer_driver_deinitv"></a>

<a id="_CPPv322bk_timer_driver_deinitv"></a> <a id="_CPPv222bk_timer_driver_deinitv"></a> <a id="bk_timer_driver_deinit__void"></a> <a id="group__bk__api__timer_1gaf157cc3319382ffa0ea1e6d41954f754"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_timer\_driver\_deinit(void)
:   Deinit the timer driver.

    This API free all resource related to timer and power down all timer channels.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv414bk_timer_start10timer_id_t8uint32_t11timer_isr_t"></a>

<a id="_CPPv314bk_timer_start10timer_id_t8uint32_t11timer_isr_t"></a> <a id="_CPPv214bk_timer_start10timer_id_t8uint32_t11timer_isr_t"></a> <a id="bk_timer_start__timer_id_t.uint32_t.timer_isr_t"></a> <a id="group__bk__api__timer_1gafd8412ab7d4698fde8a944c39551c749"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_timer\_start([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id, uint32\_t time\_ms, [timer\_isr\_t](#_CPPv411timer_isr_t "timer_isr_t") callback)
:   Start the timer.

    **Attention**
    :   1\. timer2 has been used for time cali

    **Attention**
    :   2\. timer3 has been used for clock, but bk7271 use timer1

    **Attention**
    :   3\. bk7271 has used timer0(10ms)

    参数
    :   - **timer\_id** – the timer ID to be started
        - **time\_ms** – time delay value of the timer
        - **callback** – the timer call back function

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_TIMER\_NOT\_INIT: timer driver not init
        - BK\_ERR\_TIMER\_ID: timer id is invalid
        - BK\_ERR\_TIMER\_IS\_RUNNING: timer id is running
        - others: other errors.

<a id="_CPPv431bk_timer_start_without_callback10timer_id_t8uint32_t"></a>

<a id="_CPPv331bk_timer_start_without_callback10timer_id_t8uint32_t"></a> <a id="_CPPv231bk_timer_start_without_callback10timer_id_t8uint32_t"></a> <a id="bk_timer_start_without_callback__timer_id_t.uint32_t"></a> <a id="group__bk__api__timer_1gaa61d429e98b4ff5ea3b98ba6b69c3906"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_timer\_start\_without\_callback([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id, uint32\_t time\_ms)
:   Start the timer without set callback.

    参数
    :   - **timer\_id** – the timer ID to be started
        - **timer\_ms** – time delay value of the timer

    返回
    :   - BK\_OK: succeed
        - others: others errors

<a id="_CPPv413bk_timer_stop10timer_id_t"></a>

<a id="_CPPv313bk_timer_stop10timer_id_t"></a> <a id="_CPPv213bk_timer_stop10timer_id_t"></a> <a id="bk_timer_stop__timer_id_t"></a> <a id="group__bk__api__timer_1gadaae0ec3110d731c676e99fb283e4aad"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_timer\_stop([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id)
:   Stop the timer.

    参数
    :   **timer\_id** – the timer ID to be stoped

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_timer_get_cnt10timer_id_t"></a>

<a id="_CPPv316bk_timer_get_cnt10timer_id_t"></a> <a id="_CPPv216bk_timer_get_cnt10timer_id_t"></a> <a id="bk_timer_get_cnt__timer_id_t"></a> <a id="group__bk__api__timer_1gabd8124fff09cc32cc910d152860780b1"></a> uint32\_t bk\_timer\_get\_cnt([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id)
:   Get the current counter value.

    **Attention**
    :   1\. The caller need to make sure the parameter timer\_id is correct!

    参数
    :   **timer\_id** – the timer id

    返回
    :   counter value

<a id="_CPPv415bk_timer_enable10timer_id_t"></a>

<a id="_CPPv315bk_timer_enable10timer_id_t"></a> <a id="_CPPv215bk_timer_enable10timer_id_t"></a> <a id="bk_timer_enable__timer_id_t"></a> <a id="group__bk__api__timer_1ga1cafbfb77178d9581ab30da9b8ba5fc2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_timer\_enable([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id)
:   Enable the timer.

    参数
    :   **timer\_id** – the timer ID

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_timer_disable10timer_id_t"></a>

<a id="_CPPv316bk_timer_disable10timer_id_t"></a> <a id="_CPPv216bk_timer_disable10timer_id_t"></a> <a id="bk_timer_disable__timer_id_t"></a> <a id="group__bk__api__timer_1ga8ffcd2f11b3b6fa47b7c8571a93dc6b1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_timer\_disable([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id)
:   Disable the timer.

    参数
    :   **timer\_id** – the timer ID

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_timer_get_period10timer_id_t"></a>

<a id="_CPPv319bk_timer_get_period10timer_id_t"></a> <a id="_CPPv219bk_timer_get_period10timer_id_t"></a> <a id="bk_timer_get_period__timer_id_t"></a> <a id="group__bk__api__timer_1ga08a99e27adc0bc6adc6eefd58775e303"></a> uint32\_t bk\_timer\_get\_period([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id)
:   Get the counter value set by [bk\_timer\_start()](#group__bk__api__timer_1gafd8412ab7d4698fde8a944c39551c749)

    参数
    :   **timer\_id** – the timer id

    返回
    :   counter value set by [bk\_timer\_start()](#group__bk__api__timer_1gafd8412ab7d4698fde8a944c39551c749)

<a id="_CPPv426bk_timer_get_enable_statusv"></a>

<a id="_CPPv326bk_timer_get_enable_statusv"></a> <a id="_CPPv226bk_timer_get_enable_statusv"></a> <a id="bk_timer_get_enable_status__void"></a> <a id="group__bk__api__timer_1gaabb4bb91bec05d153d3fc95eca955318"></a> uint32\_t bk\_timer\_get\_enable\_status(void)
:   Get the timer enable status.

    参数
    :   **timer\_id** – the timer id

    返回
    :   timer enable status

<a id="_CPPv431bk_timer_is_interrupt_triggered10timer_id_t"></a>

<a id="_CPPv331bk_timer_is_interrupt_triggered10timer_id_t"></a> <a id="_CPPv231bk_timer_is_interrupt_triggered10timer_id_t"></a> <a id="bk_timer_is_interrupt_triggered__timer_id_t"></a> <a id="group__bk__api__timer_1ga5fae4d8291837dc9e57935d68a1ab59f"></a> bool bk\_timer\_is\_interrupt\_triggered([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id)
:   Get whether the timer interrupt triggered.

    参数
    :   **timer\_id** – the timer id

    返回
    :   the timer interrupt status

<a id="_CPPv417bk_timer_get_time10timer_id_t8uint32_t8uint32_t18timer_value_unit_t"></a>

<a id="_CPPv317bk_timer_get_time10timer_id_t8uint32_t8uint32_t18timer_value_unit_t"></a> <a id="_CPPv217bk_timer_get_time10timer_id_t8uint32_t8uint32_t18timer_value_unit_t"></a> <a id="bk_timer_get_time__timer_id_t.uint32_t.uint32_t.timer_value_unit_t"></a> <a id="group__bk__api__timer_1gae781ccdb3ed2d4ddf4799aa6798b7488"></a> uint64\_t bk\_timer\_get\_time([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id, uint32\_t div, uint32\_t last\_count, [timer\_value\_unit\_t](#_CPPv418timer_value_unit_t "timer_value_unit_t") unit\_type)
:   Get the timer count value in ms or us.

    参数
    :   - **timer\_id** – the timer id
        - **div** – the divider of clock frequency
        - **last\_count** – last count of the timer
        - **timer\_value\_unit\_t** – the time unit, ms or us

    返回
    :   the timer value in micro seconds

<a id="_CPPv428bk_timer_delay_with_callback10timer_id_t8uint64_t11timer_isr_t"></a>

<a id="_CPPv328bk_timer_delay_with_callback10timer_id_t8uint64_t11timer_isr_t"></a> <a id="_CPPv228bk_timer_delay_with_callback10timer_id_t8uint64_t11timer_isr_t"></a> <a id="bk_timer_delay_with_callback__timer_id_t.uint64_t.timer_isr_t"></a> <a id="group__bk__api__timer_1ga11d4757ff403a9822d487b1496dc37e2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_timer\_delay\_with\_callback([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id, uint64\_t time\_us, [timer\_isr\_t](#_CPPv411timer_isr_t "timer_isr_t") callback)
:   This function set the delay based on the current running counter, which is different from bk\_timer\_start.

    参数
    :   - **timer\_id** – the timer id
        - **time\_us** – time delay value of the timer by us
        - **callback** – the timer delay call back function

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_timer_cancel10timer_id_t"></a>

<a id="_CPPv315bk_timer_cancel10timer_id_t"></a> <a id="_CPPv215bk_timer_cancel10timer_id_t"></a> <a id="bk_timer_cancel__timer_id_t"></a> <a id="group__bk__api__timer_1ga35899d640247db8b288b88a4c5450215"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_timer\_cancel([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id)
:   Cancel the timer delay task, reset timer and set ISR to NULL, it will not disable the timer, which is different from bk\_timer\_stop.

    参数
    :   **timer\_id** – the timer id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="timer-api-typedefs"></a>

## Timer API Typedefs

<a id="id1"></a>

### Header File

- [timer\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/timer_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_TIMER_ID"></a>

<a id="group__bk__api__timer__defs_1gab5cb019470c99c8d58693ce1710ec4ef"></a> BK\_ERR\_TIMER\_ID
:   timer id is invalid

<a id="c.BK_ERR_TIMER_NOT_INIT"></a>

<a id="group__bk__api__timer__defs_1ga95f9e4fadd7189673ff5d91b9476e68c"></a> BK\_ERR\_TIMER\_NOT\_INIT
:   timer driver not init

<a id="c.BK_ERR_TIMER_IS_RUNNING"></a>

<a id="group__bk__api__timer__defs_1ga09c4f7abc18ca9e91341214dcafed574"></a> BK\_ERR\_TIMER\_IS\_RUNNING
:   timer id is running

<a id="c.BK_ERR_TIMER_ID_ON_DEFCONFIG"></a>

<a id="group__bk__api__timer__defs_1gae248ddc4847453e6db8e6064df54b02a"></a> BK\_ERR\_TIMER\_ID\_ON\_DEFCONFIG
:   timer id is error

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv411timer_isr_t"></a>

<a id="_CPPv311timer_isr_t"></a> <a id="_CPPv211timer_isr_t"></a> <a id="timer_isr_t"></a> <a id="group__bk__api__timer__defs_1ga15d86f598bb4a932c1448ce605cebe48"></a> typedef void (\*timer\_isr\_t)([timer\_id\_t](#_CPPv410timer_id_t "timer_id_t") timer\_id)
:   Timer interrupt service routine.

<a id="id2"></a>

### Header File

- [hal\_timer\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_timer_types.h)

<a id="id3"></a>

### Macros

<a id="c.TIMER_CLOCK_FREQ_26M"></a>

<a id="hal__timer__types_8h_1a0f47980c1b53487c95a308151f723f1d"></a> TIMER\_CLOCK\_FREQ\_26M

<a id="c.TIMER_CLOCK_FREQ_32K"></a>

<a id="hal__timer__types_8h_1a1447f7c8836c64fca681e45f49c66abf"></a> TIMER\_CLOCK\_FREQ\_32K

<a id="id4"></a>

### Type Definitions

<a id="_CPPv412timer_unit_t"></a>

<a id="_CPPv312timer_unit_t"></a> <a id="_CPPv212timer_unit_t"></a> <a id="timer_unit_t"></a> <a id="group__bk__api__timer__defs_1ga9ea4f7d7ca6233288d38ab12e2ac3ddf"></a> typedef uint8\_t timer\_unit\_t
:   Timer uint id

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv415timer_src_clk_t"></a>

<a id="_CPPv315timer_src_clk_t"></a> <a id="_CPPv215timer_src_clk_t"></a> <a id="hal__timer__types_8h_1a98f253510f3d206027f6bafe9ac7f351"></a> enum timer\_src\_clk\_t
:   *Values:*

    <a id="_CPPv4N15timer_src_clk_t16TIMER_SCLK_CLK32E"></a>

    <a id="_CPPv3N15timer_src_clk_t16TIMER_SCLK_CLK32E"></a> <a id="_CPPv2N15timer_src_clk_t16TIMER_SCLK_CLK32E"></a> <a id="hal__timer__types_8h_1a98f253510f3d206027f6bafe9ac7f351ac5617ca493006a827bcf4988c1e632e6"></a> enumerator TIMER\_SCLK\_CLK32
    :   TIMER source clock dco

    <a id="_CPPv4N15timer_src_clk_t15TIMER_SCLK_XTALE"></a>

    <a id="_CPPv3N15timer_src_clk_t15TIMER_SCLK_XTALE"></a> <a id="_CPPv2N15timer_src_clk_t15TIMER_SCLK_XTALE"></a> <a id="hal__timer__types_8h_1a98f253510f3d206027f6bafe9ac7f351a3486fba0120c1bc84cbccff0fe9895af"></a> enumerator TIMER\_SCLK\_XTAL
    :   TIMER source clock xtal 26M

<a id="_CPPv415sys_sel_timer_t"></a>

<a id="_CPPv315sys_sel_timer_t"></a> <a id="_CPPv215sys_sel_timer_t"></a> <a id="hal__timer__types_8h_1a6c468aff1a14758ccf63bb8b8e692c32"></a> enum sys\_sel\_timer\_t
:   *Values:*

    <a id="_CPPv4N15sys_sel_timer_t14SYS_SEL_TIMER0E"></a>

    <a id="_CPPv3N15sys_sel_timer_t14SYS_SEL_TIMER0E"></a> <a id="_CPPv2N15sys_sel_timer_t14SYS_SEL_TIMER0E"></a> <a id="hal__timer__types_8h_1a6c468aff1a14758ccf63bb8b8e692c32aaaba2a4c85ec3cd7318a115ec56e30d5"></a> enumerator SYS\_SEL\_TIMER0

    <a id="_CPPv4N15sys_sel_timer_t14SYS_SEL_TIMER1E"></a>

    <a id="_CPPv3N15sys_sel_timer_t14SYS_SEL_TIMER1E"></a> <a id="_CPPv2N15sys_sel_timer_t14SYS_SEL_TIMER1E"></a> <a id="hal__timer__types_8h_1a6c468aff1a14758ccf63bb8b8e692c32a01a540006307c3b078fb8561f3367c8a"></a> enumerator SYS\_SEL\_TIMER1

<a id="_CPPv410timer_id_t"></a>

<a id="_CPPv310timer_id_t"></a> <a id="_CPPv210timer_id_t"></a> <a id="group__bk__api__timer__defs_1gab46c323c4f73f2150385fead53055392"></a> enum timer\_id\_t
:   *Values:*

    <a id="_CPPv4N10timer_id_t9TIMER_ID0E"></a>

    <a id="_CPPv3N10timer_id_t9TIMER_ID0E"></a> <a id="_CPPv2N10timer_id_t9TIMER_ID0E"></a> <a id="group__bk__api__timer__defs_1ggab46c323c4f73f2150385fead53055392ac028ff0e64e607f8143c49015fc04a12"></a> enumerator TIMER\_ID0
    :   TIMER id 0

    <a id="_CPPv4N10timer_id_t9TIMER_ID1E"></a>

    <a id="_CPPv3N10timer_id_t9TIMER_ID1E"></a> <a id="_CPPv2N10timer_id_t9TIMER_ID1E"></a> <a id="group__bk__api__timer__defs_1ggab46c323c4f73f2150385fead53055392aa9d4a52b9406b34e8ec29ce17cc7ef9a"></a> enumerator TIMER\_ID1
    :   TIMER id 1

    <a id="_CPPv4N10timer_id_t9TIMER_ID2E"></a>

    <a id="_CPPv3N10timer_id_t9TIMER_ID2E"></a> <a id="_CPPv2N10timer_id_t9TIMER_ID2E"></a> <a id="group__bk__api__timer__defs_1ggab46c323c4f73f2150385fead53055392a0abef5a9d41f90d330f1579f659fc4a8"></a> enumerator TIMER\_ID2
    :   TIMER id 2

    <a id="_CPPv4N10timer_id_t9TIMER_ID3E"></a>

    <a id="_CPPv3N10timer_id_t9TIMER_ID3E"></a> <a id="_CPPv2N10timer_id_t9TIMER_ID3E"></a> <a id="group__bk__api__timer__defs_1ggab46c323c4f73f2150385fead53055392a925e8eb05cb1f84b541187886d9e1609"></a> enumerator TIMER\_ID3
    :   TIMER id 3

    <a id="_CPPv4N10timer_id_t9TIMER_ID4E"></a>

    <a id="_CPPv3N10timer_id_t9TIMER_ID4E"></a> <a id="_CPPv2N10timer_id_t9TIMER_ID4E"></a> <a id="group__bk__api__timer__defs_1ggab46c323c4f73f2150385fead53055392aedcdd456084d75309b0ade9f91158691"></a> enumerator TIMER\_ID4
    :   TIMER id 4

    <a id="_CPPv4N10timer_id_t9TIMER_ID5E"></a>

    <a id="_CPPv3N10timer_id_t9TIMER_ID5E"></a> <a id="_CPPv2N10timer_id_t9TIMER_ID5E"></a> <a id="group__bk__api__timer__defs_1ggab46c323c4f73f2150385fead53055392a85479f2a53e08919fd5b53d9e6251e9e"></a> enumerator TIMER\_ID5
    :   TIMER id 5

    <a id="_CPPv4N10timer_id_t12TIMER_ID_MAXE"></a>

    <a id="_CPPv3N10timer_id_t12TIMER_ID_MAXE"></a> <a id="_CPPv2N10timer_id_t12TIMER_ID_MAXE"></a> <a id="group__bk__api__timer__defs_1ggab46c323c4f73f2150385fead53055392aacb7163f3ddbcdee2a162c6a6872dce3"></a> enumerator TIMER\_ID\_MAX
    :   TIMER id max

<a id="_CPPv418timer_value_unit_t"></a>

<a id="_CPPv318timer_value_unit_t"></a> <a id="_CPPv218timer_value_unit_t"></a> <a id="group__bk__api__timer__defs_1ga4074d5804ca53e570d0d4bd10c68e01e"></a> enum timer\_value\_unit\_t
:   *Values:*

    <a id="_CPPv4N18timer_value_unit_t13TIMER_UNIT_MSE"></a>

    <a id="_CPPv3N18timer_value_unit_t13TIMER_UNIT_MSE"></a> <a id="_CPPv2N18timer_value_unit_t13TIMER_UNIT_MSE"></a> <a id="group__bk__api__timer__defs_1gga4074d5804ca53e570d0d4bd10c68e01ea9e8a17f50fbbd953d0eac0b3abc030e6"></a> enumerator TIMER\_UNIT\_MS
    :   TIMER unit type is ms

    <a id="_CPPv4N18timer_value_unit_t13TIMER_UNIT_USE"></a>

    <a id="_CPPv3N18timer_value_unit_t13TIMER_UNIT_USE"></a> <a id="_CPPv2N18timer_value_unit_t13TIMER_UNIT_USE"></a> <a id="group__bk__api__timer__defs_1gga4074d5804ca53e570d0d4bd10c68e01ea89163cb239b84628e06d5551f0804adc"></a> enumerator TIMER\_UNIT\_US
    :   TIMER unit type is us
