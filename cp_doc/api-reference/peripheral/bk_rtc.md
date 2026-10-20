---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_rtc.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# RTC

BK7259 CP 侧 RTC API（`include/driver/aon_rtc.h`）。详细说明见
[RTC 开发指南](../../developer-guide/peripheral/bk_rtc.md)。

<a id="rtc-api-reference"></a>

## RTC API Reference

<a id="header-file"></a>

### Header File

- [aon\_rtc.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/aon_rtc.h)

<a id="functions"></a>

### Functions

<a id="_CPPv422bk_aon_rtc_driver_initv"></a>

<a id="_CPPv322bk_aon_rtc_driver_initv"></a> <a id="_CPPv222bk_aon_rtc_driver_initv"></a> <a id="bk_aon_rtc_driver_init__void"></a> <a id="aon__rtc_8h_1a5fc38f976b0aceff5e01ded6abe70300"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_aon\_rtc\_driver\_init(void)
:   Init the AON\_RTC driver.

    This API init the resoure common:

    - Init AON\_RTC driver control memory
    - Register ISR to NVIC/INTC/PLIC…

    **Attention**
    :   1\. This API should be called before any other AON\_RTC APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_aon_rtc_driver_deinitv"></a>

<a id="_CPPv324bk_aon_rtc_driver_deinitv"></a> <a id="_CPPv224bk_aon_rtc_driver_deinitv"></a> <a id="bk_aon_rtc_driver_deinit__void"></a> <a id="aon__rtc_8h_1a4ca8242e06cc18735590cdcd2e6918b3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_aon\_rtc\_driver\_deinit(void)
:   Denit the AON\_RTC driver.

    This API deinit the resoure common:

    - Deinit AON\_RTC driver control memory
    - Deinit AON RTC HW:Disable AON RTC, unregister isr handler

    **Attention**
    :   1\. This API should be called after any other AON\_RTC APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv417bk_alarm_register12aon_rtc_id_tP12alarm_info_t"></a>

<a id="_CPPv317bk_alarm_register12aon_rtc_id_tP12alarm_info_t"></a> <a id="_CPPv217bk_alarm_register12aon_rtc_id_tP12alarm_info_t"></a> <a id="bk_alarm_register__aon_rtc_id_t.alarm_info_tP"></a> <a id="aon__rtc_8h_1af2df335081a80cda45fa393252ed04b6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_alarm\_register(aon\_rtc\_id\_t id, [alarm\_info\_t](#_CPPv412alarm_info_t "alarm_info_t") \*alarm\_info\_p)
:   Register an alarm to AON\_RTC id timer !!! NOTES: the callback function is in ISR, so can’t block too much time. F.E:can’t call sleep/suspend; !!! !!! NOTES: freertos forbid call free/malloc in ISR which include suspend and resume. !!! @id: register to which aon\_rtc id.

    参数
    :   **alarm\_info\_p** – includes below info: name\_p: the name of the registered alarm period\_time: what’s the alarm time, milliseconds \* AON\_RTC\_MS\_TICK\_CNT period\_cnt: 0xFFFFFFF means always period until user unregister it, or means period how many times callback: if the alarm comes, will call this callback param\_p: the param will be used for callback

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_alarm_unregister12aon_rtc_id_tP7uint8_t"></a>

<a id="_CPPv319bk_alarm_unregister12aon_rtc_id_tP7uint8_t"></a> <a id="_CPPv219bk_alarm_unregister12aon_rtc_id_tP7uint8_t"></a> <a id="bk_alarm_unregister__aon_rtc_id_t.uint8_tP"></a> <a id="aon__rtc_8h_1aad4393d92ed740318416fbe4cbba7b30"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_alarm\_unregister(aon\_rtc\_id\_t id, uint8\_t \*name\_p)
:   Unregister an alarm from AON\_RTC id timer.

    **Attention**
    :   1\. Please don’t unregister self in the alarm’s callback.

    参数
    :   - **id** – unregister the aon\_rtc id alarm
        - **name\_p** – the name of the registered alarm which will be unregistered.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_alarm_is_registered12aon_rtc_id_tPK7uint8_t"></a>

<a id="_CPPv322bk_alarm_is_registered12aon_rtc_id_tPK7uint8_t"></a> <a id="_CPPv222bk_alarm_is_registered12aon_rtc_id_tPK7uint8_t"></a> <a id="bk_alarm_is_registered__aon_rtc_id_t.uint8_tCP"></a> <a id="aon__rtc_8h_1ab177efa86a78b6e4434e53baa8b68d48"></a> bool bk\_alarm\_is\_registered(aon\_rtc\_id\_t id, const uint8\_t \*name\_p)
:   Check whether an alarm with the given name is still registered.

    参数
    :   - **id** – aon\_rtc id
        - **name\_p** – alarm name to look up

    返回
    :   - true: the named alarm is present in the AON RTC alarm list
        - false: not registered / invalid args

<a id="_CPPv424bk_aon_rtc_get_upper_val12aon_rtc_id_t"></a>

<a id="_CPPv324bk_aon_rtc_get_upper_val12aon_rtc_id_t"></a> <a id="_CPPv224bk_aon_rtc_get_upper_val12aon_rtc_id_t"></a> <a id="bk_aon_rtc_get_upper_val__aon_rtc_id_t"></a> <a id="aon__rtc_8h_1a0f401f855c5f88cb872eba5d609bdcf8"></a> uint64\_t bk\_aon\_rtc\_get\_upper\_val(aon\_rtc\_id\_t id)
:   Get AON RTC upper value with 64 bits @id: register to which aon\_rtc id.

    返回
    :   - AON RTC upper value with 64 bits

<a id="_CPPv424bk_aon_rtc_get_max_value12aon_rtc_id_t"></a>

<a id="_CPPv324bk_aon_rtc_get_max_value12aon_rtc_id_t"></a> <a id="_CPPv224bk_aon_rtc_get_max_value12aon_rtc_id_t"></a> <a id="bk_aon_rtc_get_max_value__aon_rtc_id_t"></a> <a id="aon__rtc_8h_1af75d5635271928541e4e6fd41691e2cd"></a> uint64\_t bk\_aon\_rtc\_get\_max\_value(aon\_rtc\_id\_t id)
:   Get AON RTC configured max value with 64 bits @id: register to which aon\_rtc id.

    返回
    :   - AON RTC configured max value with 64 bits

<a id="_CPPv427bk_aon_rtc_get_current_tick12aon_rtc_id_t"></a>

<a id="_CPPv327bk_aon_rtc_get_current_tick12aon_rtc_id_t"></a> <a id="_CPPv227bk_aon_rtc_get_current_tick12aon_rtc_id_t"></a> <a id="bk_aon_rtc_get_current_tick__aon_rtc_id_t"></a> <a id="aon__rtc_8h_1ad78f51f23028ddf6e57afd436a6c37e3"></a> uint64\_t bk\_aon\_rtc\_get\_current\_tick(aon\_rtc\_id\_t id)
:   Get AON RTC current tick with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: register to which aon\_rtc id.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_aon_rtc_dump12aon_rtc_id_t"></a>

<a id="_CPPv315bk_aon_rtc_dump12aon_rtc_id_t"></a> <a id="_CPPv215bk_aon_rtc_dump12aon_rtc_id_t"></a> <a id="bk_aon_rtc_dump__aon_rtc_id_t"></a> <a id="aon__rtc_8h_1a25466f4c6fe69595f093a6c84bb764e5"></a> void bk\_aon\_rtc\_dump(aon\_rtc\_id\_t id)
:   dump aon rtc debug info

    @id: which aon\_rtc id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_rtc_gettimeofdayP7timevalPv"></a>

<a id="_CPPv319bk_rtc_gettimeofdayP7timevalPv"></a> <a id="_CPPv219bk_rtc_gettimeofdayP7timevalPv"></a> <a id="bk_rtc_gettimeofday__timevalP.voidP"></a> <a id="aon__rtc_8h_1adbecb84d09322cff55d91ef0f235acbd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rtc\_gettimeofday(struct timeval \*tv, void \*ptz)
:   Get time of day.

    @tv: Define parameters according to “structure timeval”

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_rtc_settimeofdayPK7timevalPK8timezone"></a>

<a id="_CPPv319bk_rtc_settimeofdayPK7timevalPK8timezone"></a> <a id="_CPPv219bk_rtc_settimeofdayPK7timevalPK8timezone"></a> <a id="bk_rtc_settimeofday__timevalCP.timezoneCP"></a> <a id="aon__rtc_8h_1ae67595427a328bc4e1a73fbfbbaf090c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rtc\_settimeofday(const struct timeval \*tv, const struct timezone \*tz)
:   Set time of day.

    @tv: Define parameters according to “structure timeval” @tz: Define parameters according to “structure timezone”

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv437bk_rtc_get_deepsleep_duration_secondsP8uint32_t"></a>

<a id="_CPPv337bk_rtc_get_deepsleep_duration_secondsP8uint32_t"></a> <a id="_CPPv237bk_rtc_get_deepsleep_duration_secondsP8uint32_t"></a> <a id="bk_rtc_get_deepsleep_duration_seconds__uint32_tP"></a> <a id="aon__rtc_8h_1a80cdcea79b819ccc5a8cd1711f5f7d49"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rtc\_get\_deepsleep\_duration\_seconds(uint32\_t \*deepsleep\_seconds)
:   Get Deepsleep duration seconds.

    @deepsleep\_seconds: The incoming formal parameter is assigned the deepsleep time Unit : second

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_rtc_get_ms_tick_countv"></a>

<a id="_CPPv324bk_rtc_get_ms_tick_countv"></a> <a id="_CPPv224bk_rtc_get_ms_tick_countv"></a> <a id="bk_rtc_get_ms_tick_count__void"></a> <a id="aon__rtc_8h_1ac75eeae14d8a4707d0519ba25127c3df"></a> float bk\_rtc\_get\_ms\_tick\_count(void)
:   Get aon rtc ticks of per ms.

    返回
    :   - aon rtc ticks of per ms \|- EXTERN 32K: 32.768 \|- Default: 32.000

<a id="_CPPv421bk_rtc_get_clock_freqv"></a>

<a id="_CPPv321bk_rtc_get_clock_freqv"></a> <a id="_CPPv221bk_rtc_get_clock_freqv"></a> <a id="bk_rtc_get_clock_freq__void"></a> <a id="aon__rtc_8h_1a097316049402475f172ac05e8d6b0043"></a> uint32\_t bk\_rtc\_get\_clock\_freq(void)
:   Get aon rtc clock freq.

    返回
    :   - aon rtc clock freq \|- EXTERN 32K: 32768 \|- Default: 32000

<a id="_CPPv423bk_rtc_update_base_timev"></a>

<a id="_CPPv323bk_rtc_update_base_timev"></a> <a id="_CPPv223bk_rtc_update_base_timev"></a> <a id="bk_rtc_update_base_time__void"></a> <a id="aon__rtc_8h_1a1ae96681b0654d8dbabd272a1b63e578"></a> void bk\_rtc\_update\_base\_time(void)
:   Update AON RTC base time reference.

    This API accumulates the elapsed time since the last base tick into the internal base time (s\_time\_base\_us), and resets the base tick (s\_time\_base\_tick) to the current RTC tick. It should be called before changing the RTC clock frequency or after sleep/wakeup to keep the monotonic time (bk\_aon\_rtc\_get\_us) continuous.

    返回
    :   NA

<a id="_CPPv421bk_rtc_set_clock_freq8uint32_t"></a>

<a id="_CPPv321bk_rtc_set_clock_freq8uint32_t"></a> <a id="_CPPv221bk_rtc_set_clock_freq8uint32_t"></a> <a id="bk_rtc_set_clock_freq__uint32_t"></a> <a id="aon__rtc_8h_1af47feb73e4f9553cf8712d112c63f0d0"></a> void bk\_rtc\_set\_clock\_freq(uint32\_t clock\_freq)
:   Set aon rtc ticks of per ms while dynamic swith clock.

    @ms\_tick\_cnt: aon rtc clock freq \|- EXTERN 32K: 32768 \|- Default: 32000

    返回
    :   NA

<a id="_CPPv417bk_aon_rtc_get_usv"></a>

<a id="_CPPv317bk_aon_rtc_get_usv"></a> <a id="_CPPv217bk_aon_rtc_get_usv"></a> <a id="bk_aon_rtc_get_us__void"></a> <a id="aon__rtc_8h_1adbe1a91c0f9b7c8507ceaadd7f50c9d4"></a> uint64\_t bk\_aon\_rtc\_get\_us(void)
:   Get AON RTC current us with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: use AON\_RTC\_ID\_1.

    返回
    :   - AON RTC current us with 64 bits with about \+30us/-30us presision

<a id="_CPPv417bk_aon_rtc_get_msv"></a>

<a id="_CPPv317bk_aon_rtc_get_msv"></a> <a id="_CPPv217bk_aon_rtc_get_msv"></a> <a id="bk_aon_rtc_get_ms__void"></a> <a id="aon__rtc_8h_1a86380baa629425ae8e5b4c40d57d36c9"></a> uint64\_t bk\_aon\_rtc\_get\_ms(void)
:   Get AON RTC current ms with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: use AON\_RTC\_ID\_1.

    返回
    :   - AON RTC current us with 64 bits with about \+30us/-30us presision

<a id="_CPPv414rtc_tick_to_us8uint64_t"></a>

<a id="_CPPv314rtc_tick_to_us8uint64_t"></a> <a id="_CPPv214rtc_tick_to_us8uint64_t"></a> <a id="rtc_tick_to_us__uint64_t"></a> <a id="aon__rtc_8h_1a7014913b23413a5ea53154bdfb4cd45e"></a> uint64\_t rtc\_tick\_to\_us(uint64\_t tick)
:   Convert AON RTC tick to us.

    @tick: AON RTC tick

    返回
    :   - AON RTC tick to us

<a id="_CPPv414rtc_us_to_tick8uint64_t"></a>

<a id="_CPPv314rtc_us_to_tick8uint64_t"></a> <a id="_CPPv214rtc_us_to_tick8uint64_t"></a> <a id="rtc_us_to_tick__uint64_t"></a> <a id="aon__rtc_8h_1a23e271acd307c902baefd7f66c11831a"></a> uint64\_t rtc\_us\_to\_tick(uint64\_t us)
:   Convert AON RTC us to tick.

    @us: AON RTC us

    返回
    :   - AON RTC us to tick

<a id="_CPPv427bk_rtc_get_first_alarm_namev"></a>

<a id="_CPPv327bk_rtc_get_first_alarm_namev"></a> <a id="_CPPv227bk_rtc_get_first_alarm_namev"></a> <a id="bk_rtc_get_first_alarm_name__void"></a> <a id="aon__rtc_8h_1ae35331ddcad7916793b7772ec40a0045"></a> uint8\_t \*bk\_rtc\_get\_first\_alarm\_name(void)
:   Get the name of the first alarm node in the RTC alarm list.

    This function returns the name of the first alarm node (earliest expired time) in the RTC alarm list. The alarm list is sorted by expired\_tick in ascending order. This is useful for identifying which application (e.g., “BK\_BLE”, “BK\_WIFI”) will wake up the system next.

    备注

    The returned pointer points to the internal alarm node structure. The caller should not modify the content, and the pointer may become invalid if the alarm is unregistered.

    返回
    :   - Pointer to the alarm name string (e.g., “BK\_BLE”, “BK\_WIFI”)
        - NULL if no alarm is registered or list is empty

<a id="rtc-api-typedefs"></a>

## RTC API Typedefs

<a id="id1"></a>

### Header File

- [aon\_rtc\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/aon_rtc_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv420aon_rtc_int_config_t"></a>

<a id="_CPPv320aon_rtc_int_config_t"></a> <a id="_CPPv220aon_rtc_int_config_t"></a> <a id="aon_rtc_int_config_t"></a> <a id="structaon__rtc__int__config__t"></a> struct aon\_rtc\_int\_config\_t

<a id="_CPPv413_alarm_info_t"></a>

<a id="_CPPv313_alarm_info_t"></a> <a id="_CPPv213_alarm_info_t"></a> <a id="_alarm_info_t"></a> <a id="struct__alarm__info__t"></a> struct \_alarm\_info\_t

<a id="_CPPv413_alarm_node_t"></a>

<a id="_CPPv313_alarm_node_t"></a> <a id="_CPPv213_alarm_node_t"></a> <a id="_alarm_node_t"></a> <a id="struct__alarm__node__t"></a> struct \_alarm\_node\_t

<a id="macros"></a>

### Macros

<a id="c.ALARM_NAME_MAX_LEN"></a>

<a id="aon__rtc__types_8h_1aa11cc044348edde38dd9c2da24fba732"></a> ALARM\_NAME\_MAX\_LEN

<a id="c.ALARM_LOOP_FOREVER"></a>

<a id="aon__rtc__types_8h_1aaaa4a0fec3f68b49fcbde3c7266cc990"></a> ALARM\_LOOP\_FOREVER

<a id="c.AON_RTC_EXTERN_32K_CLOCK_FREQ"></a>

<a id="aon__rtc__types_8h_1a48341c9e5a2970975e77953137996b9b"></a> AON\_RTC\_EXTERN\_32K\_CLOCK\_FREQ

<a id="c.AON_RTC_DEFAULT_CLOCK_FREQ"></a>

<a id="aon__rtc__types_8h_1a502db0ba2d94046a4363d067610c76ba"></a> AON\_RTC\_DEFAULT\_CLOCK\_FREQ

<a id="c.AON_RTC_MS_TICK_CNT"></a>

<a id="aon__rtc__types_8h_1ab6ab502f7490c1c7545f10cf0836b8d5"></a> AON\_RTC\_MS\_TICK\_CNT

<a id="c.AON_RTC_PRECISION_TICK"></a>

<a id="aon__rtc__types_8h_1a613f977200578269726650b191a12672"></a> AON\_RTC\_PRECISION\_TICK

<a id="c.AON_RTC_ROUND_TICK"></a>

<a id="aon__rtc__types_8h_1a9c1ebca01b0b6e1489eddefd8d153c8a"></a> AON\_RTC\_ROUND\_TICK

<a id="c.AON_RTC_MAX_ALARM_CNT"></a>

<a id="aon__rtc__types_8h_1adc72fe8fbea0cb3a38b95328947f7d59"></a> AON\_RTC\_MAX\_ALARM\_CNT

<a id="c.BK_ERR_AON_RTC_DRIVER_NOT_INIT"></a>

<a id="aon__rtc__types_8h_1a44be16af913fa2cd3d2790681bef2b65"></a> BK\_ERR\_AON\_RTC\_DRIVER\_NOT\_INIT
:   AON RTC interrupt service routine.

    AON\_RTC driver not init

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410rtc_tick_t"></a>

<a id="_CPPv310rtc_tick_t"></a> <a id="_CPPv210rtc_tick_t"></a> <a id="rtc_tick_t"></a> <a id="aon__rtc__types_8h_1a18aa35d8718b700b1bb8e4ccf8671999"></a> typedef uint32\_t rtc\_tick\_t

<a id="_CPPv413aon_rtc_isr_t"></a>

<a id="_CPPv313aon_rtc_isr_t"></a> <a id="_CPPv213aon_rtc_isr_t"></a> <a id="aon_rtc_isr_t"></a> <a id="aon__rtc__types_8h_1a7a9a2ad8dac6c4613e961b259215dd4e"></a> typedef void (\*aon\_rtc\_isr\_t)(aon\_rtc\_id\_t id, uint8\_t \*name\_p, void \*param)

<a id="_CPPv412alarm_info_t"></a>

<a id="_CPPv312alarm_info_t"></a> <a id="_CPPv212alarm_info_t"></a> <a id="alarm_info_t"></a> <a id="aon__rtc__types_8h_1a9a0db404beb94a2e6c4332519a59792e"></a> typedef struct [\_alarm\_info\_t](#_CPPv413_alarm_info_t "_alarm_info_t") alarm\_info\_t

<a id="_CPPv412alarm_node_t"></a>

<a id="_CPPv312alarm_node_t"></a> <a id="_CPPv212alarm_node_t"></a> <a id="alarm_node_t"></a> <a id="aon__rtc__types_8h_1aa7afd3b7bbe4796a18c74e26759fa322"></a> typedef struct [\_alarm\_node\_t](#_CPPv413_alarm_node_t "_alarm_node_t") alarm\_node\_t
