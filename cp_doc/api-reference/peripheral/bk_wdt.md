---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_wdt.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="watchdog"></a>

# Watchdog

<a id="aon-wdt-api-status"></a>

## AON\_WDT 兼容 API Status

| API | BK7259\_CP |
| --- | --- |
| [`bk_wdt_driver_init()`](#_CPPv418bk_wdt_driver_initv "bk_wdt_driver_init") | Y |
| [`bk_wdt_driver_deinit()`](#_CPPv420bk_wdt_driver_deinitv "bk_wdt_driver_deinit") | Y |
| [`bk_wdt_start()`](#_CPPv412bk_wdt_start8uint32_t "bk_wdt_start") | Y |
| [`bk_wdt_stop()`](#_CPPv411bk_wdt_stopv "bk_wdt_stop") | Y |
| [`bk_wdt_suspend()`](#_CPPv414bk_wdt_suspendv "bk_wdt_suspend") | Y |
| [`bk_wdt_resume()`](#_CPPv413bk_wdt_resumev "bk_wdt_resume") | Y |
| [`bk_wdt_feed()`](#_CPPv411bk_wdt_feedv "bk_wdt_feed") | Y |
| [`bk_wdt_get_feed_time()`](#_CPPv420bk_wdt_get_feed_timev "bk_wdt_get_feed_time") | Y |
| [`bk_wdt_set_feed_time()`](#_CPPv420bk_wdt_set_feed_time8uint32_t "bk_wdt_set_feed_time") | Y |
| [`bk_wdt_is_driver_inited()`](#_CPPv423bk_wdt_is_driver_initedv "bk_wdt_is_driver_inited") | Y |

<a id="id1"></a>

## AON\_WDT 专用 API Status

| API | BK7259\_CP |
| --- | --- |
| `bk_aon_wdt_get_period()` | Y |
| `bk_aon_wdt_set_period()` | Y |
| `bk_aon_wdt_stop()` | Y |
| `bk_aon_wdt_feed()` | Y |
| `bk_aon_wdt_get_feed_time()` | Y |
| `bk_aon_wdt_set_feed_time()` | Y |

<a id="wwdt-api-status"></a>

## `wwdt` API Status

| API | BK7259\_CP |
| --- | --- |
| `bk_wwdt_driver_init()` | Y |
| `bk_wwdt_driver_deinit()` | Y |
| `bk_wwdt_start()` | Y |
| `bk_wwdt_stop()` | Y |
| `bk_wwdt_feed()` | Y |
| `bk_wwdt_get_feed_time()` | Y |
| `bk_wwdt_set_feed_time()` | Y |
| `bk_wwdt_is_driver_inited()` | Y |
| `bk_wwdt_get_cpu_id()` | Y |

<a id="aon-wdt-api-reference"></a>

## AON\_WDT 兼容 API Reference

<a id="header-file"></a>

### Header File

- [wdt.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/wdt.h)

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

<a id="_CPPv414bk_wdt_suspendv"></a>

<a id="_CPPv314bk_wdt_suspendv"></a> <a id="_CPPv214bk_wdt_suspendv"></a> <a id="bk_wdt_suspend__void"></a> <a id="group__bk__api__wdt_1ga78ed834230fed7ebc9890331ed3a27c5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wdt\_suspend(void)
:   Suspend AON\_WDT before entering low power.

    This API closes AON\_WDT hardware and stops its periodic feed timer, while keeping retained software state for wakeup recovery.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv413bk_wdt_resumev"></a>

<a id="_CPPv313bk_wdt_resumev"></a> <a id="_CPPv213bk_wdt_resumev"></a> <a id="bk_wdt_resume__void"></a> <a id="group__bk__api__wdt_1ga0459d9917bfc557002f72b52bd22e9a8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wdt\_resume(void)
:   Resume AON\_WDT after exiting low power.

    This API restores AON\_WDT HAL state, periodic feed timer and PMU watchdog reset path, then restarts AON\_WDT with the retained timeout.

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

<a id="_CPPv410update_wdt8uint32_t"></a>

<a id="_CPPv310update_wdt8uint32_t"></a> <a id="_CPPv210update_wdt8uint32_t"></a> <a id="update_wdt__uint32_t"></a> <a id="group__bk__api__wdt_1gaf26ce90182c2cfe3113d4c4b70d6e00a"></a> void update\_wdt(uint32\_t val)

<a id="_CPPv414update_aon_wdt8uint32_t"></a>

<a id="_CPPv314update_aon_wdt8uint32_t"></a> <a id="_CPPv214update_aon_wdt8uint32_t"></a> <a id="update_aon_wdt__uint32_t"></a> <a id="group__bk__api__wdt_1gafda69aa4d711bdec9820a2da66144b9d"></a> void update\_aon\_wdt(uint32\_t val)

<a id="_CPPv49close_wdtv"></a>

<a id="_CPPv39close_wdtv"></a> <a id="_CPPv29close_wdtv"></a> <a id="close_wdt__void"></a> <a id="group__bk__api__wdt_1gaa99ddd4d02f8acdd58aefbbe1bfd98bc"></a> void close\_wdt(void)

<a id="_CPPv413close_aon_wdtv"></a>

<a id="_CPPv313close_aon_wdtv"></a> <a id="_CPPv213close_aon_wdtv"></a> <a id="close_aon_wdt__void"></a> <a id="group__bk__api__wdt_1gaac060fc49959431953761d294f765be2"></a> void close\_aon\_wdt(void)

<a id="aon-wdt-api-typedefs"></a>

## AON\_WDT 兼容 API Typedefs

<a id="id2"></a>

### Header File

- [wdt\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/wdt_types.h)

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

<a id="id3"></a>

### Header File

- [hal\_wdt\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_wdt_types.h)

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410wdt_unit_t"></a>

<a id="_CPPv310wdt_unit_t"></a> <a id="_CPPv210wdt_unit_t"></a> <a id="wdt_unit_t"></a> <a id="group__bk__api__wdt__defs_1gaa140a251e0a5f8ed59a6fb7795991ef0"></a> typedef uint8\_t wdt\_unit\_t
:   wdt uint id

<a id="aon-wdt-api"></a>

## AON\_WDT API 头文件

> - API 头文件：`cp/include/driver/aon_wdt.h`
> - 类型定义：`cp/include/driver/aon_wdt_types.h`

<a id="wwdt-api"></a>

## `wwdt` API 头文件

> - API 头文件：`cp/include/driver/wwdt.h`
> - 类型定义：`cp/include/driver/wwdt_types.h`、`cp/include/driver/hal/hal_wwdt_types.h`
