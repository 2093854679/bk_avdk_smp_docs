# RTC



## RTC API Status

| API | BK7259_AP |
| --- | --- |
| [`bk_rtc_gettimeofday()`](#_CPPv419bk_rtc_gettimeofdayP7timevalPv "bk_rtc_gettimeofday") | Y |
| [`bk_rtc_settimeofday()`](#_CPPv419bk_rtc_settimeofdayPK7timevalPK8timezone "bk_rtc_settimeofday") | Y |
| [`bk_aon_rtc_get_current_tick()`](#_CPPv427bk_aon_rtc_get_current_tick12aon_rtc_id_t "bk_aon_rtc_get_current_tick") | Y |
| [`bk_rtc_get_ms_tick_count()`](#_CPPv424bk_rtc_get_ms_tick_countv "bk_rtc_get_ms_tick_count") | Y |
| [`bk_aon_rtc_get_us()`](#_CPPv417bk_aon_rtc_get_usv "bk_aon_rtc_get_us") | Y |
| [`bk_aon_rtc_get_ms()`](#_CPPv417bk_aon_rtc_get_msv "bk_aon_rtc_get_ms") | Y |


## RTC API Reference


### Header File


- [aon_rtc.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/aon_rtc.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/aon_rtc.h")


### Functions

uint64_t bk_aon_rtc_get_current_tick(aon_rtc_id_t id)
:   Get AON RTC current tick with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: register to which aon_rtc id.

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

float bk_rtc_get_ms_tick_count(void)
:   Get aon rtc ticks of per ms.

    返回
    :   - aon rtc ticks of per ms |- EXTERN 32K: 32.768 |- Default: 32.000

uint32_t bk_rtc_get_clock_freq(void)
:   Get aon rtc clock freq.

    返回
    :   - aon rtc clock freq |- EXTERN 32K: 32768 |- Default: 32000

uint64_t bk_aon_rtc_get_us(void)
:   Get AON RTC current us with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: use AON_RTC_ID_1.

    返回
    :   - AON RTC current us with 64 bits with about +30us/-30us presision

uint64_t bk_aon_rtc_get_ms(void)
:   Get AON RTC current ms with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: use AON_RTC_ID_1.

    返回
    :   - AON RTC current us with 64 bits with about +30us/-30us presision


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
