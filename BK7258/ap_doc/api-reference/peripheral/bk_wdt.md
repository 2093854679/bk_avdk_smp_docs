---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_wdt.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wdt"></a>

# WDT

<a id="wdt-api-status"></a>

## WDT API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_wdt_driver_init()`](#_CPPv418bk_wdt_driver_initv "bk_wdt_driver_init") | Y |
| [`bk_wdt_driver_deinit()`](#_CPPv420bk_wdt_driver_deinitv "bk_wdt_driver_deinit") | Y |
| [`bk_wdt_start()`](#_CPPv412bk_wdt_start8uint32_t "bk_wdt_start") | Y |
| [`bk_wdt_stop()`](#_CPPv411bk_wdt_stopv "bk_wdt_stop") | Y |
| [`bk_wdt_feed()`](#_CPPv411bk_wdt_feedv "bk_wdt_feed") | Y |

<a id="wdt-api-reference"></a>

## WDT API Reference

<a id="header-file"></a>

### Header File

- [wdt.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/wdt.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_wdt_driver_initv"></a>

<a id="_CPPv318bk_wdt_driver_initv"></a> <a id="_CPPv218bk_wdt_driver_initv"></a> <a id="bk_wdt_driver_init__void"></a> <a id="group__bk__api__wdt_1ga46dd3f450e6c227244235cc7012ad2b6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wdt\_driver\_init(void)
:   Init the WDT driver.

    This API init the resoure common:

    - Init WDT driver control memory

    **Attention**
    :   1\. This API should be called before any other WDT APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_wdt_driver_deinitv"></a>

<a id="_CPPv320bk_wdt_driver_deinitv"></a> <a id="_CPPv220bk_wdt_driver_deinitv"></a> <a id="bk_wdt_driver_deinit__void"></a> <a id="group__bk__api__wdt_1gaef1e9f40d792ed4fbc2b9ee218d24121"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wdt\_driver\_deinit(void)
:   Deinit the WDT driver.

    This API free all resource related to WDT and power down WDT.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv412bk_wdt_start8uint32_t"></a>

<a id="_CPPv312bk_wdt_start8uint32_t"></a> <a id="_CPPv212bk_wdt_start8uint32_t"></a> <a id="bk_wdt_start__uint32_t"></a> <a id="group__bk__api__wdt_1gacba87a8b4cb62a77f26255d57a27bde2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wdt\_start(uint32\_t timeout\_ms)
:   Start the WDT.

    This API start the WDT:

    - Power up the WDT
    - Init the watch dog timer period

    参数
    :   **timeout\_ms** – WDT period

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_WDT\_DRIVER\_NOT\_INIT: WDT driver not init
        - BK\_ERR\_WDT\_INVALID\_PERIOD: WDT invalid period
        - others: other errors.

<a id="_CPPv411bk_wdt_stopv"></a>

<a id="_CPPv311bk_wdt_stopv"></a> <a id="_CPPv211bk_wdt_stopv"></a> <a id="bk_wdt_stop__void"></a> <a id="group__bk__api__wdt_1ga708ae275d41039e36be9c67be3a2a60e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wdt\_stop(void)
:   Stop the WDT.

    This API stop the WDT:

    - Reset all configuration of WDT to default value
    - Power down the WDT

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_wdt_feedv"></a>

<a id="_CPPv311bk_wdt_feedv"></a> <a id="_CPPv211bk_wdt_feedv"></a> <a id="bk_wdt_feed__void"></a> <a id="group__bk__api__wdt_1ga087f22e39c2f4acad990e48e309cde0e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wdt\_feed(void)
:   Feed the WDT.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_wdt_get_feed_timev"></a>

<a id="_CPPv320bk_wdt_get_feed_timev"></a> <a id="_CPPv220bk_wdt_get_feed_timev"></a> <a id="bk_wdt_get_feed_time__void"></a> <a id="group__bk__api__wdt_1gadd4cd64af8d03cf6020c3a0c54a40c86"></a> uint32\_t bk\_wdt\_get\_feed\_time(void)
:   Get feed watchdog time.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_wdt_set_feed_time8uint32_t"></a>

<a id="_CPPv320bk_wdt_set_feed_time8uint32_t"></a> <a id="_CPPv220bk_wdt_set_feed_time8uint32_t"></a> <a id="bk_wdt_set_feed_time__uint32_t"></a> <a id="group__bk__api__wdt_1ga4714b269a8f2b72b8270a92ba74d6ea0"></a> void bk\_wdt\_set\_feed\_time(uint32\_t dw\_set\_time)
:   set feed watchdog time

    返回
    :   - NULL

<a id="_CPPv423bk_wdt_is_driver_initedv"></a>

<a id="_CPPv323bk_wdt_is_driver_initedv"></a> <a id="_CPPv223bk_wdt_is_driver_initedv"></a> <a id="bk_wdt_is_driver_inited__void"></a> <a id="group__bk__api__wdt_1ga0e51d42412ca6335145892bbdd34860e"></a> bool bk\_wdt\_is\_driver\_inited(void)
:   Get wdt driver init flag.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="wdt-api-typedefs"></a>

## WDT API Typedefs

<a id="id1"></a>

### Header File

- [wdt\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/wdt_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_WDT_DRIVER_NOT_INIT"></a>

<a id="group__bk__api__wdt__defs_1ga90b34b299bcd34ff2d43e6f4f4ba328f"></a> BK\_ERR\_WDT\_DRIVER\_NOT\_INIT
:   WDT driver not init

<a id="c.BK_ERR_WDT_NOT_INIT"></a>

<a id="group__bk__api__wdt__defs_1ga606fdda09a98a8b4688aadba6bae4e49"></a> BK\_ERR\_WDT\_NOT\_INIT
:   WDT not init

<a id="c.BK_ERR_WDT_INVALID_PERIOD"></a>

<a id="group__bk__api__wdt__defs_1gad9962715560c5c682e3d907d21f9d059"></a> BK\_ERR\_WDT\_INVALID\_PERIOD
:   WDT invalid period

<a id="c.BK_ERR_WDT_DEBUG_DISABLED"></a>

<a id="group__bk__api__wdt__defs_1gac293195ebd9717b1c66ae4ee0d702a67"></a> BK\_ERR\_WDT\_DEBUG\_DISABLED
:   WDT disabled via cmdline flag

<a id="id2"></a>

### Header File

- [hal\_wdt\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_wdt_types.h)

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410wdt_unit_t"></a>

<a id="_CPPv310wdt_unit_t"></a> <a id="_CPPv210wdt_unit_t"></a> <a id="wdt_unit_t"></a> <a id="group__bk__api__wdt__defs_1gaa140a251e0a5f8ed59a6fb7795991ef0"></a> typedef uint8\_t wdt\_unit\_t
:   wdt uint id
