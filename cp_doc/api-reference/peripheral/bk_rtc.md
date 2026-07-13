# RTC


BK7259 CP 侧 RTC API（`include/driver/aon_rtc.h`）。详细说明见
[RTC 开发指南](../../developer-guide/peripheral/bk_rtc.md "../../developer-guide/peripheral/bk_rtc.md")。


## RTC API Reference


### Header File


- [aon_rtc.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/aon_rtc.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/aon_rtc.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_aon_rtc_driver_init(void)
:   Init the AON_RTC driver.

    This API init the resoure common:


    - Init AON_RTC driver control memory

    - Register ISR to NVIC/INTC/PLIC…


    **Attention**
    :   1. This API should be called before any other AON_RTC APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_aon_rtc_driver_deinit(void)
:   Denit the AON_RTC driver.

    This API deinit the resoure common:


    - Deinit AON_RTC driver control memory

    - Deinit AON RTC HW:Disable AON RTC, unregister isr handler


    **Attention**
    :   1. This API should be called after any other AON_RTC APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_alarm_register(aon_rtc_id_t id, [alarm_info_t](#_CPPv412alarm_info_t "alarm_info_t") *alarm_info_p)
:   Register an alarm to AON_RTC id timer !!! NOTES: the callback function is in ISR, so can’t block too much time. F.E:can’t call sleep/suspend; !!! !!! NOTES: freertos forbid call free/malloc in ISR which include suspend and resume. !!! @id: register to which aon_rtc id.

    参数
    :   **alarm_info_p** – includes below info: name_p: the name of the registered alarm period_time: what’s the alarm time, milliseconds * AON_RTC_MS_TICK_CNT period_cnt: 0xFFFFFFF means always period until user unregister it, or means period how many times callback: if the alarm comes, will call this callback param_p: the param will be used for callback

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_alarm_unregister(aon_rtc_id_t id, uint8_t *name_p)
:   Unregister an alarm from AON_RTC id timer.


    **Attention**
    :   1. Please don’t unregister self in the alarm’s callback.

    参数
    :   - **id** – unregister the aon_rtc id alarm

        - **name_p** – the name of the registered alarm which will be unregistered.

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint64_t bk_aon_rtc_get_upper_val(aon_rtc_id_t id)
:   Get AON RTC upper value with 64 bits @id: register to which aon_rtc id.

    返回
    :   - AON RTC upper value with 64 bits

uint64_t bk_aon_rtc_get_max_value(aon_rtc_id_t id)
:   Get AON RTC configured max value with 64 bits @id: register to which aon_rtc id.

    返回
    :   - AON RTC configured max value with 64 bits

uint64_t bk_aon_rtc_get_current_tick(aon_rtc_id_t id)
:   Get AON RTC current tick with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: register to which aon_rtc id.

    返回
    :   - BK_OK: succeed

        - others: other errors.

void bk_aon_rtc_dump(aon_rtc_id_t id)
:   dump aon rtc debug info

    @id: which aon_rtc id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_rtc_gettimeofday(struct timeval *tv, void *ptz)
:   Get time of day.

    @tv: Define parameters according to “structure timeval”

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_rtc_settimeofday(const struct timeval *tv, const struct timezone *tz)
:   Set time of day.

    @tv: Define parameters according to “structure timeval” @tz: Define parameters according to “structure timezone”

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_rtc_get_deepsleep_duration_seconds(uint32_t *deepsleep_seconds)
:   Get Deepsleep duration seconds.

    @deepsleep_seconds: The incoming formal parameter is assigned the deepsleep time Unit : second

    返回
    :   - BK_OK: succeed

        - others: other errors.

float bk_rtc_get_ms_tick_count(void)
:   Get aon rtc ticks of per ms.

    返回
    :   - aon rtc ticks of per ms |- EXTERN 32K: 32.768 |- Default: 32.000

uint32_t bk_rtc_get_clock_freq(void)
:   Get aon rtc clock freq.

    返回
    :   - aon rtc clock freq |- EXTERN 32K: 32768 |- Default: 32000

void bk_rtc_update_base_time(void)
:   Update AON RTC base time reference.

    This API accumulates the elapsed time since the last base tick into the internal base time (s_time_base_us), and resets the base tick (s_time_base_tick) to the current RTC tick. It should be called before changing the RTC clock frequency or after sleep/wakeup to keep the monotonic time (bk_aon_rtc_get_us) continuous.

    返回
    :   NA

void bk_rtc_set_clock_freq(uint32_t clock_freq)
:   Set aon rtc ticks of per ms while dynamic swith clock.

    @ms_tick_cnt: aon rtc clock freq |- EXTERN 32K: 32768 |- Default: 32000

    返回
    :   NA

uint64_t bk_aon_rtc_get_us(void)
:   Get AON RTC current us with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: use AON_RTC_ID_1.

    返回
    :   - AON RTC current us with 64 bits with about +30us/-30us presision

uint64_t bk_aon_rtc_get_ms(void)
:   Get AON RTC current ms with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: use AON_RTC_ID_1.

    返回
    :   - AON RTC current us with 64 bits with about +30us/-30us presision

uint64_t rtc_tick_to_us(uint64_t tick)
:   Convert AON RTC tick to us.

    @tick: AON RTC tick

    返回
    :   - AON RTC tick to us

uint64_t rtc_us_to_tick(uint64_t us)
:   Convert AON RTC us to tick.

    @us: AON RTC us

    返回
    :   - AON RTC us to tick

uint8_t *bk_rtc_get_first_alarm_name(void)
:   Get the name of the first alarm node in the RTC alarm list.

    This function returns the name of the first alarm node (earliest expired time) in the RTC alarm list. The alarm list is sorted by expired_tick in ascending order. This is useful for identifying which application (e.g., “BK_BLE”, “BK_WIFI”) will wake up the system next.

    备注

    The returned pointer points to the internal alarm node structure. The caller should not modify the content, and the pointer may become invalid if the alarm is unregistered.

    返回
    :   - Pointer to the alarm name string (e.g., “BK_BLE”, “BK_WIFI”)

        - NULL if no alarm is registered or list is empty


## RTC API Typedefs


### Header File


- [aon_rtc_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/aon_rtc_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/aon_rtc_types.h")


### Structures

struct aon_rtc_int_config_t

struct _alarm_info_t

struct _alarm_node_t


### Macros

ALARM_NAME_MAX_LEN

ALARM_LOOP_FOREVER

AON_RTC_EXTERN_32K_CLOCK_FREQ

AON_RTC_DEFAULT_CLOCK_FREQ

AON_RTC_MS_TICK_CNT

AON_RTC_PRECISION_TICK

AON_RTC_ROUND_TICK

AON_RTC_MAX_ALARM_CNT

BK_ERR_AON_RTC_DRIVER_NOT_INIT
:   AON RTC interrupt service routine.

    AON_RTC driver not init


### Type Definitions

typedef uint32_t rtc_tick_t

typedef void (*aon_rtc_isr_t)(aon_rtc_id_t id, uint8_t *name_p, void *param)

typedef struct [_alarm_info_t](#_CPPv413_alarm_info_t "_alarm_info_t") alarm_info_t

typedef struct [_alarm_node_t](#_CPPv413_alarm_node_t "_alarm_node_t") alarm_node_t
