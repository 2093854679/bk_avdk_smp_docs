# TOUCH


BK7259 AP 侧 Touch API（`include/driver/touch.h`）。

重要

The TOUCH API v1.0 is the lastest and stable TOUCH APIs. All new applications should use TOUCH API v1.0.


## Touch User Guide

Touch module have three different types of working modes, which are automatic calibrattion mode, manul calibration mode and scan mode. The scan mode must work based on the automatic calibration mode or manul mode.
When the touch channel has been calibrated, then set multi channels that neet to scan and enable the scan mode. The automatic calibration mode and manul calibration mode are used as follows:

![Touch User Guide Flow](../../_images/touch_user_guide_flow.png)

Touch User Guide Flow


## Touch APIs

> - [`bk_touch_gpio_init()`](#_CPPv418bk_touch_gpio_init15touch_channel_t "bk_touch_gpio_init") - init the touch gpio pin
> - [`bk_touch_enable()`](#_CPPv415bk_touch_enable15touch_channel_t "bk_touch_enable") - enable the touch module funtion
> - [`bk_touch_disable()`](#_CPPv416bk_touch_disablev "bk_touch_disable") - enable the touch module funtion
> - [`bk_touch_config()`](#_CPPv415bk_touch_configPK14touch_config_t "bk_touch_config") - config the touch parameters to enable touch work
> - [`bk_touch_calibration_start()`](#_CPPv426bk_touch_calibration_startv "bk_touch_calibration_start") - start calibrating the touch channel
> - [`bk_touch_scan_mode_enable()`](#_CPPv425bk_touch_scan_mode_enable8uint32_t "bk_touch_scan_mode_enable") - enable or disable scan mode of touch module
> - [`bk_touch_manul_mode_enable()`](#_CPPv426bk_touch_manul_mode_enable8uint32_t "bk_touch_manul_mode_enable") - enable manul mode of touch module
> - [`bk_touch_manul_mode_disable()`](#_CPPv427bk_touch_manul_mode_disablev "bk_touch_manul_mode_disable") - disable manul mode of touch module
> - [`bk_touch_scan_mode_multi_channl_set()`](#_CPPv435bk_touch_scan_mode_multi_channl_set15touch_channel_t "bk_touch_scan_mode_multi_channl_set") - set multi channels that need to scan
> - [`bk_touch_int_enable()`](#_CPPv419bk_touch_int_enable15touch_channel_t8uint32_t "bk_touch_int_enable") - enable or disable touch interrupt
> - [`bk_touch_get_calib_value()`](#_CPPv424bk_touch_get_calib_valuev "bk_touch_get_calib_value") - get the calibration value of touch channel
> - [`bk_touch_get_touch_status()`](#_CPPv425bk_touch_get_touch_statusv "bk_touch_get_touch_status") - get the status of touch channel
> - [`bk_touch_register_touch_isr()`](#_CPPv427bk_touch_register_touch_isr15touch_channel_t11touch_isr_tPv "bk_touch_register_touch_isr") - register touch isr


## API Reference


### Header File


- [touch.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/touch.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/touch.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_gpio_init([touch_channel_t](#_CPPv415touch_channel_t "touch_channel_t") touch_id)
:   Init the touch gpio pin.

    This API init the GPIO pin corresponding to touch channel:


    - Unmap gpio pin function

    - Change gpio pin function to touch

    - Configure gpio to be high impedance

    This API should be called before any other TOUCH APIs.

    参数
    :   **-** – touch_id: touch channel, channel 0 ~ channel 15

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_enable([touch_channel_t](#_CPPv415touch_channel_t "touch_channel_t") touch_id)
:   enable touch function

    This API enable the touch function:


    - Select the touch channel

    - Power on the touch module

    参数
    :   **-** – touch_id: touch channel, channel 0 ~ channel 15

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_disable(void)
:   disable touch function

    This API disable the touch function:


    - Power down the touch module

    参数
    :   **-** – None

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_config(const [touch_config_t](#_CPPv414touch_config_t "touch_config_t") *touch_config)
:   config touch function

    This API config the touch function:


    - Set touch sensitivity level, the smaller the value, the more sensitive. The range of level value from 0 to 3

    - Set touch detect threshold, the range of value from 0 to 7.

    - Set touch detect range, 8pF/12pF/19pF/27pF

    Usage example:

    ```
    touch_config_t touch_config;
    touch_config.sensitivity_level = TOUCH_SENSITIVITY_LEVLE_3;
    touch_config.detect_threshold = TOUCH_DETECT_THRESHOLD_6;
    touch_config.detect_range = TOUCH_DETECT_RANGE_27PF;
    bk_touch_config(&touch_config);
    ```

    参数
    :   **-** – touch_config: the config of touch work mode

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_calibration_start(void)
:   start calibrating touch channel

    This API start calibrating the touch channel that selected.

    参数
    :   **-** – None

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_scan_mode_enable(uint32_t enable)
:   enable/disable scan mode of touch channel

    This API enable or disable the scan mode of touch channel.

    参数
    :   **-** – enable: enable —— 1; disable —— 0;

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_adc_mode_enable(uint32_t enable)
:   enable/disable adc mode of touch channel

    This API enable or disable the adc mode of touch channel.

    参数
    :   **-** – enable: enable —— 1; disable —— 0;

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_manul_mode_enable(uint32_t calib_value)
:   enable manul calibration mode of touch channel

    This API enable the manul calibration mode of touch channel:


    - set the calibration value of manul mode;

    - enable the manul calibretion mode;

    参数
    :   **-** – calib_value: calibration value of manul mode, the max value is 0x1FF;

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_manul_mode_disable(void)
:   disable manul calibration mode of touch channel

    This API disable the manul calibration mode of touch channel

    参数
    :   **-** – None

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_scan_mode_multi_channl_set([touch_channel_t](#_CPPv415touch_channel_t "touch_channel_t") touch_id)
:   set multi channels that need to scan

    This API set multi channels that need to scan

    参数
    :   **-** – touch_id: the multi channels that need to scan. See the enum of touch_channel_t.

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_int_enable([touch_channel_t](#_CPPv415touch_channel_t "touch_channel_t") touch_id, uint32_t enable)
:   enable/disable touch channel interrupt

    This API enable or disable the touch channel interrupt:


    - register the interrupt service handle;

    - enable or disable the touch interrupt;

    参数
    :   **-** – touch_id: touch channel, channel 0 ~ channel 15;


        - enable: enable —— 1; disable —— 0;

    返回
    :   - BK_OK: succeed

uint32_t bk_touch_get_calib_value(void)
:   get the calibration value of touch channel

    This API get the calibration value of touch channel.

    参数
    :   **-** – None

    返回
    :   - calib_value: the max value is 0x1FF.

uint32_t bk_touch_get_touch_status(void)
:   get the status of touch channel

    This API get the status of touch channel:

    参数
    :   **-** – None

    返回
    :   - touch_status: the touch status of every channel. One bit corresponding to one channel. 1 —— the channel is touched; 0 —— the channel is idle.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_digital_tube_init(void)
:   init the digital tube of touch

    This API init the digital tube:

    参数
    :   **-** – None

    返回
    :   - BK_OK: succeed

void bk_touch_digital_tube_display(uint8_t disp_value)
:   display the value in the digital tube

    This API display the value in the digital tube

    参数
    :   **-** – disp_value: the value need to display;

    返回
    :   - None

void bk_touch_wakeup_channel_set([touch_channel_t](#_CPPv415touch_channel_t "touch_channel_t") channel)
:   get the touch channel for low voltage and deepsleep wake up

    This API get the touch channel for low voltage and deepsleep wake up

    参数
    :   **-** – channel: touch channel, channel 0 ~ channel 15. See the enum of touch_channel_t.

    返回
    :   - None

uint32_t bk_touch_wakeup_channel_get(void)
:   set the touch channel for low voltage and deepsleep wake up

    This API set the touch channel for low voltage and deepsleep wake up

    参数
    :   **-** – None

    返回
    :   - s_touch_wakeup_channel: the channel number of touch

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_pm_init(void)
:   Register touch low voltage and deepsleep config.

    This API register touch low voltage and deepsleep config

    参数
    :   **-** – None

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_register_touch_isr([touch_channel_t](#_CPPv415touch_channel_t "touch_channel_t") touch_id, [touch_isr_t](#_CPPv411touch_isr_t "touch_isr_t") isr, void *param)
:   Register touch isr.

    This API register touch isr

    参数
    :   **-** – touch_id: touch channel, channel 0 ~ channel 15;


        - isr: touch isr callback;

        - param: touch isr callback parameter;

    返回
    :   - BK_OK: succeed

        - others: other errors.


## API Typedefs


### Header File


- [touch_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/touch_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/touch_types.h")


### Structures

struct touch_int_config_t

struct touch_config_t


### Macros

BK_ERR_TOUCH_ID


### Type Definitions

typedef void (*touch_isr_t)(void *param)


### Enumerations

enum touch_channel_t
:   *Values:*

    enumerator BK_TOUCH_0
    :   touch channel 0

    enumerator BK_TOUCH_1
    :   touch channel 1

    enumerator BK_TOUCH_2
    :   touch channel 2

    enumerator BK_TOUCH_3
    :   touch channel 3

    enumerator BK_TOUCH_4
    :   touch channel 4

    enumerator BK_TOUCH_5
    :   touch channel 5

    enumerator BK_TOUCH_6
    :   touch channel 6

    enumerator BK_TOUCH_7
    :   touch channel 7

    enumerator BK_TOUCH_8
    :   touch channel 8

    enumerator BK_TOUCH_9
    :   touch channel 9

    enumerator BK_TOUCH_10
    :   touch channel 10

    enumerator BK_TOUCH_11
    :   touch channel 11

    enumerator BK_TOUCH_12
    :   touch channel 12

    enumerator BK_TOUCH_13
    :   touch channel 13

    enumerator BK_TOUCH_14
    :   touch channel 14

    enumerator BK_TOUCH_15
    :   touch channel 15

    enumerator BK_TOUCH_MAX

enum touch_sensitivity_level_t
:   *Values:*

    enumerator TOUCH_SENSITIVITY_LEVLE_0

    enumerator TOUCH_SENSITIVITY_LEVLE_1

    enumerator TOUCH_SENSITIVITY_LEVLE_2

    enumerator TOUCH_SENSITIVITY_LEVLE_3

enum touch_detect_threshold_t
:   *Values:*

    enumerator TOUCH_DETECT_THRESHOLD_0

    enumerator TOUCH_DETECT_THRESHOLD_1

    enumerator TOUCH_DETECT_THRESHOLD_2

    enumerator TOUCH_DETECT_THRESHOLD_3

    enumerator TOUCH_DETECT_THRESHOLD_4

    enumerator TOUCH_DETECT_THRESHOLD_5

    enumerator TOUCH_DETECT_THRESHOLD_6

    enumerator TOUCH_DETECT_THRESHOLD_7

enum touch_detect_range_t
:   *Values:*

    enumerator TOUCH_DETECT_RANGE_8PF
    :   8PF

    enumerator TOUCH_DETECT_RANGE_12PF
    :   12PF

    enumerator TOUCH_DETECT_RANGE_19PF
    :   19PF

    enumerator TOUCH_DETECT_RANGE_27PF
    :   27PF
