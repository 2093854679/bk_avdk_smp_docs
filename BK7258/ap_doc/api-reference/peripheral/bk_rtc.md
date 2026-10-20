---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_rtc.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# RTC

<a id="rtc-api-status"></a>

## RTC API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_rtc_gettimeofday()`](#_CPPv419bk_rtc_gettimeofdayP7timevalPv "bk_rtc_gettimeofday") | Y |
| [`bk_rtc_settimeofday()`](#_CPPv419bk_rtc_settimeofdayPK7timevalPK8timezone "bk_rtc_settimeofday") | Y |
| [`bk_aon_rtc_get_current_tick()`](#_CPPv427bk_aon_rtc_get_current_tick12aon_rtc_id_t "bk_aon_rtc_get_current_tick") | Y |
| [`bk_rtc_get_ms_tick_count()`](#_CPPv424bk_rtc_get_ms_tick_countv "bk_rtc_get_ms_tick_count") | Y |
| [`bk_aon_rtc_get_us()`](#_CPPv417bk_aon_rtc_get_usv "bk_aon_rtc_get_us") | Y |
| [`bk_aon_rtc_get_ms()`](#_CPPv417bk_aon_rtc_get_msv "bk_aon_rtc_get_ms") | Y |

<a id="rtc-api-reference"></a>

## RTC API Reference

<a id="header-file"></a>

### Header File

- [aon\_rtc.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/aon_rtc.h)

<a id="functions"></a>

### Functions

<a id="_CPPv427bk_aon_rtc_get_current_tick12aon_rtc_id_t"></a>

<a id="_CPPv327bk_aon_rtc_get_current_tick12aon_rtc_id_t"></a> <a id="_CPPv227bk_aon_rtc_get_current_tick12aon_rtc_id_t"></a> <a id="bk_aon_rtc_get_current_tick__aon_rtc_id_t"></a> <a id="aon__rtc_8h_1ad78f51f23028ddf6e57afd436a6c37e3"></a> uint64\_t bk\_aon\_rtc\_get\_current\_tick(aon\_rtc\_id\_t id)
:   Get AON RTC current tick with 64 bits AON RTC uses 32 Bits counter with 32K clock, the max time is about 36.4 hours. The 32K clock really frequency is 32768 HZ(External 32K XTL) or 32000 HZ(Internel ROSC). Set upper interrupt as the 0xFFFFFFFF ticks as one round. @id: register to which aon\_rtc id.

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

<a id="rtc-api-typedefs"></a>

## RTC API Typedefs

<a id="id1"></a>

### Header File

- [aon\_rtc\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/aon_rtc_types.h)

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
