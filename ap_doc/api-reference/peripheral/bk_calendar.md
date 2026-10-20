---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_calendar.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="calendar"></a>

# Calendar

BK7259 AP 侧 Calendar API（`include/driver/calendar.h`）。用于日历/闹钟计时，与 RTC 模块 `aon_rtc.h` 为不同外设。

<a id="calendar-api-reference"></a>

## Calendar API Reference

<a id="header-file"></a>

### Header File

- [calendar.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/calendar.h)

<a id="functions"></a>

### Functions

<a id="_CPPv423bk_calendar_driver_initv"></a>

<a id="_CPPv323bk_calendar_driver_initv"></a> <a id="_CPPv223bk_calendar_driver_initv"></a> <a id="bk_calendar_driver_init__void"></a> <a id="calendar_8h_1a757ed7eb4a8e1fe0bf68b66579f5b6b3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_calendar\_driver\_init(void)
:   Init the calendar driver.

    This API init the resoure common:

    - Init calendar driver control memory

    **Attention**
    :   1\. This API should be called before any other calendar APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_calendar_driver_deinitv"></a>

<a id="_CPPv325bk_calendar_driver_deinitv"></a> <a id="_CPPv225bk_calendar_driver_deinitv"></a> <a id="bk_calendar_driver_deinit__void"></a> <a id="calendar_8h_1a6e7229324532549fba4524aa771e700e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_calendar\_driver\_deinit(void)
:   Deinit the calendar driver.

    This API free all resource related to calendar and disable calendar.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_calendar_set_init_value8uint32_t"></a>

<a id="_CPPv326bk_calendar_set_init_value8uint32_t"></a> <a id="_CPPv226bk_calendar_set_init_value8uint32_t"></a> <a id="bk_calendar_set_init_value__uint32_t"></a> <a id="calendar_8h_1a41ee2962e12f62854d9700bd4655fea9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_calendar\_set\_init\_value(uint32\_t init\_val)
:   Set the calendar init value.

    参数
    :   **init\_val** – calendar init value

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_calendar_get_time_usv"></a>

<a id="_CPPv323bk_calendar_get_time_usv"></a> <a id="_CPPv223bk_calendar_get_time_usv"></a> <a id="bk_calendar_get_time_us__void"></a> <a id="calendar_8h_1a69d01af599b246ab734cb9906c8ad79d"></a> uint64\_t bk\_calendar\_get\_time\_us(void)
:   Get the calendar time us.

    返回
    :   the calendar time us

<a id="calendar-api-typedefs"></a>

## Calendar API Typedefs

<a id="id1"></a>

### Header File

- [calendar\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/calendar_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_CALENDAR_NOT_INIT"></a>

<a id="calendar__types_8h_1a57e296e30e4df89fa15ac814ff34a9c4"></a> BK\_ERR\_CALENDAR\_NOT\_INIT
:   calendar driver not init

<a id="id2"></a>

### Header File

- [hal\_calendar\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_calendar_types.h)

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv415calendar_unit_t"></a>

<a id="_CPPv315calendar_unit_t"></a> <a id="_CPPv215calendar_unit_t"></a> <a id="calendar_unit_t"></a> <a id="hal__calendar__types_8h_1a08f9429d5e5fc55a3d3db71b5879e4a7"></a> typedef uint8\_t calendar\_unit\_t
:   calendar uint id
