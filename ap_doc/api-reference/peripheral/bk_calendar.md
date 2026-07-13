# Calendar


BK7259 AP 侧 Calendar API（`include/driver/calendar.h`）。用于日历/闹钟计时，与 RTC 模块 `aon_rtc.h` 为不同外设。


## Calendar API Reference


### Header File


- [calendar.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/calendar.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/calendar.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_calendar_driver_init(void)
:   Init the calendar driver.

    This API init the resoure common:


    - Init calendar driver control memory


    **Attention**
    :   1. This API should be called before any other calendar APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_calendar_driver_deinit(void)
:   Deinit the calendar driver.

    This API free all resource related to calendar and disable calendar.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_calendar_set_init_value(uint32_t init_val)
:   Set the calendar init value.

    参数
    :   **init_val** – calendar init value

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint64_t bk_calendar_get_time_us(void)
:   Get the calendar time us.

    返回
    :   the calendar time us


## Calendar API Typedefs


### Header File


- [calendar_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/calendar_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/calendar_types.h")


### Macros

BK_ERR_CALENDAR_NOT_INIT
:   calendar driver not init


### Header File


- [hal/hal_calendar_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_calendar_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_calendar_types.h")


### Type Definitions

typedef uint8_t calendar_unit_t
:   calendar uint id
