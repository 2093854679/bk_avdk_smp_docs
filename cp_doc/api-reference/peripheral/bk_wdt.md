# Watchdog



## AON_WDT 兼容 API Status

| API | BK7259_CP |
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


## AON_WDT 专用 API Status

| API | BK7259_CP |
| --- | --- |
| `bk_aon_wdt_get_period()` | Y |
| `bk_aon_wdt_set_period()` | Y |
| `bk_aon_wdt_stop()` | Y |
| `bk_aon_wdt_feed()` | Y |
| `bk_aon_wdt_get_feed_time()` | Y |
| `bk_aon_wdt_set_feed_time()` | Y |


## `wwdt` API Status

| API | BK7259_CP |
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


## AON_WDT 兼容 API Reference


### Header File


- [wdt.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/wdt.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/wdt.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_wdt_driver_init(void)
:   Init the WDT driver.

    This API init the resoure common:


    - Init WDT driver control memory


    **Attention**
    :   1. This API should be called before any other WDT APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_wdt_driver_deinit(void)
:   Deinit the WDT driver.

    This API free all resource related to WDT and power down WDT.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_wdt_start(uint32_t timeout_ms)
:   Start the WDT.

    This API start the WDT:


    - Power up the WDT

    - Init the watch dog timer period

    参数
    :   **timeout_ms** – WDT period

    返回
    :   - BK_OK: succeed

        - BK_ERR_WDT_DRIVER_NOT_INIT: WDT driver not init

        - BK_ERR_WDT_INVALID_PERIOD: WDT invalid period

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_wdt_stop(void)
:   Stop the WDT.

    This API stop the WDT:


    - Reset all configuration of WDT to default value

    - Power down the WDT

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_wdt_suspend(void)
:   Suspend AON_WDT before entering low power.

    This API closes AON_WDT hardware and stops its periodic feed timer, while keeping retained software state for wakeup recovery.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_wdt_resume(void)
:   Resume AON_WDT after exiting low power.

    This API restores AON_WDT HAL state, periodic feed timer and PMU watchdog reset path, then restarts AON_WDT with the retained timeout.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_wdt_feed(void)
:   Feed the WDT.

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_wdt_get_feed_time(void)
:   Get feed watchdog time.

    返回
    :   - BK_OK: succeed

        - others: other errors.

void bk_wdt_set_feed_time(uint32_t dw_set_time)
:   set feed watchdog time

    返回
    :   - NULL

bool bk_wdt_is_driver_inited(void)
:   Get wdt driver init flag.

    返回
    :   - BK_OK: succeed

        - others: other errors.


## AON_WDT 兼容 API Typedefs


### Header File


- [wdt_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/wdt_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/wdt_types.h")


### Macros

BK_ERR_WDT_DRIVER_NOT_INIT
:   WDT driver not init

BK_ERR_WDT_NOT_INIT
:   WDT not init

BK_ERR_WDT_INVALID_PERIOD
:   WDT invalid period

BK_ERR_WDT_DEBUG_DISABLED
:   WDT disabled via cmdline flag


### Header File


- [hal/hal_wdt_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_wdt_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_wdt_types.h")


### Type Definitions

typedef uint8_t wdt_unit_t
:   wdt uint id


## AON_WDT API 头文件

> - API 头文件：`cp/include/driver/aon_wdt.h`
> - 类型定义：`cp/include/driver/aon_wdt_types.h`


## `wwdt` API 头文件

> - API 头文件：`cp/include/driver/wwdt.h`
> - 类型定义：`cp/include/driver/wwdt_types.h`、`cp/include/driver/hal/hal_wwdt_types.h`
