---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_touch.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="touch"></a>

# TOUCH

BK7259 AP 侧 Touch API（`include/driver/touch.h`）。

重要

The TOUCH API v1.0 is the lastest and stable TOUCH APIs. All new applications should use TOUCH API v1.0.

<a id="touch-user-guide"></a>

## Touch User Guide

Touch module have three different types of working modes, which are automatic calibrattion mode, manul calibration mode and scan mode. The scan mode must work based on the automatic calibration mode or manul mode.
When the touch channel has been calibrated, then set multi channels that neet to scan and enable the scan mode. The automatic calibration mode and manul calibration mode are used as follows:

<a id="id2"></a>
![Touch User Guide Flow](../../../../_assets/deb5e674f755684cbe00-touch_user_guide_flow.png)


Touch User Guide Flow

<a id="touch-apis"></a>

## Touch APIs

> - [`bk_touch_gpio_init()`](#_CPPv418bk_touch_gpio_init15touch_channel_t "bk_touch_gpio_init") \- init the touch gpio pin
> - [`bk_touch_enable()`](#_CPPv415bk_touch_enable15touch_channel_t "bk_touch_enable") \- enable the touch module funtion
> - [`bk_touch_disable()`](#_CPPv416bk_touch_disablev "bk_touch_disable") \- enable the touch module funtion
> - [`bk_touch_config()`](#_CPPv415bk_touch_configPK14touch_config_t "bk_touch_config") \- config the touch parameters to enable touch work
> - [`bk_touch_calibration_start()`](#_CPPv426bk_touch_calibration_startv "bk_touch_calibration_start") \- start calibrating the touch channel
> - [`bk_touch_scan_mode_enable()`](#_CPPv425bk_touch_scan_mode_enable8uint32_t "bk_touch_scan_mode_enable") \- enable or disable scan mode of touch module
> - [`bk_touch_manul_mode_enable()`](#_CPPv426bk_touch_manul_mode_enable8uint32_t "bk_touch_manul_mode_enable") \- enable manul mode of touch module
> - [`bk_touch_manul_mode_disable()`](#_CPPv427bk_touch_manul_mode_disablev "bk_touch_manul_mode_disable") \- disable manul mode of touch module
> - [`bk_touch_scan_mode_multi_channl_set()`](#_CPPv435bk_touch_scan_mode_multi_channl_set15touch_channel_t "bk_touch_scan_mode_multi_channl_set") \- set multi channels that need to scan
> - [`bk_touch_int_enable()`](#_CPPv419bk_touch_int_enable15touch_channel_t8uint32_t "bk_touch_int_enable") \- enable or disable touch interrupt
> - [`bk_touch_get_calib_value()`](#_CPPv424bk_touch_get_calib_valuev "bk_touch_get_calib_value") \- get the calibration value of touch channel
> - [`bk_touch_get_touch_status()`](#_CPPv425bk_touch_get_touch_statusv "bk_touch_get_touch_status") \- get the status of touch channel
> - [`bk_touch_register_touch_isr()`](#_CPPv427bk_touch_register_touch_isr15touch_channel_t11touch_isr_tPv "bk_touch_register_touch_isr") \- register touch isr

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [touch.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/touch.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_touch_gpio_init15touch_channel_t"></a>

<a id="_CPPv318bk_touch_gpio_init15touch_channel_t"></a> <a id="_CPPv218bk_touch_gpio_init15touch_channel_t"></a> <a id="bk_touch_gpio_init__touch_channel_t"></a> <a id="group__touch_1ga0e791e1ca6c28adb26a30ff0af94290b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_gpio\_init([touch\_channel\_t](#_CPPv415touch_channel_t "touch_channel_t") touch\_id)
:   Init the touch gpio pin.

    This API init the GPIO pin corresponding to touch channel:

    - Unmap gpio pin function
    - Change gpio pin function to touch
    - Configure gpio to be high impedance

    This API should be called before any other TOUCH APIs.

    参数
    :   **\-** – touch\_id: touch channel, channel 0 \~ channel 15

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_touch_enable15touch_channel_t"></a>

<a id="_CPPv315bk_touch_enable15touch_channel_t"></a> <a id="_CPPv215bk_touch_enable15touch_channel_t"></a> <a id="bk_touch_enable__touch_channel_t"></a> <a id="group__touch_1ga113fd3f1cac7261c242d7d0307d7df32"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_enable([touch\_channel\_t](#_CPPv415touch_channel_t "touch_channel_t") touch\_id)
:   enable touch function

    This API enable the touch function:

    - Select the touch channel
    - Power on the touch module

    参数
    :   **\-** – touch\_id: touch channel, channel 0 \~ channel 15

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_touch_disablev"></a>

<a id="_CPPv316bk_touch_disablev"></a> <a id="_CPPv216bk_touch_disablev"></a> <a id="bk_touch_disable__void"></a> <a id="group__touch_1ga13784f5ab840e56eaa68bfa13a41ab9a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_disable(void)
:   disable touch function

    This API disable the touch function:

    - Power down the touch module

    参数
    :   **\-** – None

    返回
    :   - BK\_OK: succeed

<a id="_CPPv415bk_touch_configPK14touch_config_t"></a>

<a id="_CPPv315bk_touch_configPK14touch_config_t"></a> <a id="_CPPv215bk_touch_configPK14touch_config_t"></a> <a id="bk_touch_config__touch_config_tCP"></a> <a id="group__touch_1ga9b981d172ace27d67c5a3ccbd66c979b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_config(const [touch\_config\_t](#_CPPv414touch_config_t "touch_config_t") \*touch\_config)
:   config touch function

    This API config the touch function:

    - Set touch sensitivity level, the smaller the value, the more sensitive. The range of level value from 0 to 3
    - Set touch detect threshold, the range of value from 0 to 7\.
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
    :   **\-** – touch\_config: the config of touch work mode

    返回
    :   - BK\_OK: succeed

<a id="_CPPv426bk_touch_calibration_startv"></a>

<a id="_CPPv326bk_touch_calibration_startv"></a> <a id="_CPPv226bk_touch_calibration_startv"></a> <a id="bk_touch_calibration_start__void"></a> <a id="group__touch_1ga4559fc1d2c2077887d2eb93815bd9b76"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_calibration\_start(void)
:   start calibrating touch channel

    This API start calibrating the touch channel that selected.

    参数
    :   **\-** – None

    返回
    :   - BK\_OK: succeed

<a id="_CPPv425bk_touch_scan_mode_enable8uint32_t"></a>

<a id="_CPPv325bk_touch_scan_mode_enable8uint32_t"></a> <a id="_CPPv225bk_touch_scan_mode_enable8uint32_t"></a> <a id="bk_touch_scan_mode_enable__uint32_t"></a> <a id="group__touch_1ga840f53e61ffd4a082c9bfe2d9b747a3e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_scan\_mode\_enable(uint32\_t enable)
:   enable/disable scan mode of touch channel

    This API enable or disable the scan mode of touch channel.

    参数
    :   **\-** – enable: enable —— 1; disable —— 0;

    返回
    :   - BK\_OK: succeed

<a id="_CPPv424bk_touch_adc_mode_enable8uint32_t"></a>

<a id="_CPPv324bk_touch_adc_mode_enable8uint32_t"></a> <a id="_CPPv224bk_touch_adc_mode_enable8uint32_t"></a> <a id="bk_touch_adc_mode_enable__uint32_t"></a> <a id="group__touch_1ga2f84beb3d20bb4bc644b5e8bf4c32c68"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_adc\_mode\_enable(uint32\_t enable)
:   enable/disable adc mode of touch channel

    This API enable or disable the adc mode of touch channel.

    参数
    :   **\-** – enable: enable —— 1; disable —— 0;

    返回
    :   - BK\_OK: succeed

<a id="_CPPv426bk_touch_manul_mode_enable8uint32_t"></a>

<a id="_CPPv326bk_touch_manul_mode_enable8uint32_t"></a> <a id="_CPPv226bk_touch_manul_mode_enable8uint32_t"></a> <a id="bk_touch_manul_mode_enable__uint32_t"></a> <a id="group__touch_1gadb5190a6ca208a3c1c776b6fb1f53f2b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_manul\_mode\_enable(uint32\_t calib\_value)
:   enable manul calibration mode of touch channel

    This API enable the manul calibration mode of touch channel:

    - set the calibration value of manul mode;
    - enable the manul calibretion mode;

    参数
    :   **\-** – calib\_value: calibration value of manul mode, the max value is 0x1FF;

    返回
    :   - BK\_OK: succeed

<a id="_CPPv427bk_touch_manul_mode_disablev"></a>

<a id="_CPPv327bk_touch_manul_mode_disablev"></a> <a id="_CPPv227bk_touch_manul_mode_disablev"></a> <a id="bk_touch_manul_mode_disable__void"></a> <a id="group__touch_1gaa2f1be4c68e609a82a98318a434ebdbb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_manul\_mode\_disable(void)
:   disable manul calibration mode of touch channel

    This API disable the manul calibration mode of touch channel

    参数
    :   **\-** – None

    返回
    :   - BK\_OK: succeed

<a id="_CPPv435bk_touch_scan_mode_multi_channl_set15touch_channel_t"></a>

<a id="_CPPv335bk_touch_scan_mode_multi_channl_set15touch_channel_t"></a> <a id="_CPPv235bk_touch_scan_mode_multi_channl_set15touch_channel_t"></a> <a id="bk_touch_scan_mode_multi_channl_set__touch_channel_t"></a> <a id="group__touch_1ga07d84a582f53293476df335c8f5868a0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_scan\_mode\_multi\_channl\_set([touch\_channel\_t](#_CPPv415touch_channel_t "touch_channel_t") touch\_id)
:   set multi channels that need to scan

    This API set multi channels that need to scan

    参数
    :   **\-** – touch\_id: the multi channels that need to scan. See the enum of touch\_channel\_t.

    返回
    :   - BK\_OK: succeed

<a id="_CPPv419bk_touch_int_enable15touch_channel_t8uint32_t"></a>

<a id="_CPPv319bk_touch_int_enable15touch_channel_t8uint32_t"></a> <a id="_CPPv219bk_touch_int_enable15touch_channel_t8uint32_t"></a> <a id="bk_touch_int_enable__touch_channel_t.uint32_t"></a> <a id="group__touch_1gaa81bf40ba0e9d3e2b24639f8cea2cff0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_int\_enable([touch\_channel\_t](#_CPPv415touch_channel_t "touch_channel_t") touch\_id, uint32\_t enable)
:   enable/disable touch channel interrupt

    This API enable or disable the touch channel interrupt:

    - register the interrupt service handle;
    - enable or disable the touch interrupt;

    参数
    :   **\-** – touch\_id: touch channel, channel 0 \~ channel 15;

        - enable: enable —— 1; disable —— 0;

    返回
    :   - BK\_OK: succeed

<a id="_CPPv424bk_touch_get_calib_valuev"></a>

<a id="_CPPv324bk_touch_get_calib_valuev"></a> <a id="_CPPv224bk_touch_get_calib_valuev"></a> <a id="bk_touch_get_calib_value__void"></a> <a id="group__touch_1gaf15c226b74f4f6c5357c14f9a2075116"></a> uint32\_t bk\_touch\_get\_calib\_value(void)
:   get the calibration value of touch channel

    This API get the calibration value of touch channel.

    参数
    :   **\-** – None

    返回
    :   - calib\_value: the max value is 0x1FF.

<a id="_CPPv425bk_touch_get_touch_statusv"></a>

<a id="_CPPv325bk_touch_get_touch_statusv"></a> <a id="_CPPv225bk_touch_get_touch_statusv"></a> <a id="bk_touch_get_touch_status__void"></a> <a id="group__touch_1ga27de024da4ace7ad53c1e7d7b7386fc8"></a> uint32\_t bk\_touch\_get\_touch\_status(void)
:   get the status of touch channel

    This API get the status of touch channel:

    参数
    :   **\-** – None

    返回
    :   - touch\_status: the touch status of every channel. One bit corresponding to one channel. 1 —— the channel is touched; 0 —— the channel is idle.

<a id="_CPPv426bk_touch_digital_tube_initv"></a>

<a id="_CPPv326bk_touch_digital_tube_initv"></a> <a id="_CPPv226bk_touch_digital_tube_initv"></a> <a id="bk_touch_digital_tube_init__void"></a> <a id="group__touch_1gac92341ad92a77043e51a0ef0b8766869"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_digital\_tube\_init(void)
:   init the digital tube of touch

    This API init the digital tube:

    参数
    :   **\-** – None

    返回
    :   - BK\_OK: succeed

<a id="_CPPv429bk_touch_digital_tube_display7uint8_t"></a>

<a id="_CPPv329bk_touch_digital_tube_display7uint8_t"></a> <a id="_CPPv229bk_touch_digital_tube_display7uint8_t"></a> <a id="bk_touch_digital_tube_display__uint8_t"></a> <a id="group__touch_1ga5a0f92ae2e742c3117eda8cb98339753"></a> void bk\_touch\_digital\_tube\_display(uint8\_t disp\_value)
:   display the value in the digital tube

    This API display the value in the digital tube

    参数
    :   **\-** – disp\_value: the value need to display;

    返回
    :   - None

<a id="_CPPv427bk_touch_wakeup_channel_set15touch_channel_t"></a>

<a id="_CPPv327bk_touch_wakeup_channel_set15touch_channel_t"></a> <a id="_CPPv227bk_touch_wakeup_channel_set15touch_channel_t"></a> <a id="bk_touch_wakeup_channel_set__touch_channel_t"></a> <a id="group__touch_1gae935d968be98d15262b00fd9caf8cc30"></a> void bk\_touch\_wakeup\_channel\_set([touch\_channel\_t](#_CPPv415touch_channel_t "touch_channel_t") channel)
:   get the touch channel for low voltage and deepsleep wake up

    This API get the touch channel for low voltage and deepsleep wake up

    参数
    :   **\-** – channel: touch channel, channel 0 \~ channel 15\. See the enum of touch\_channel\_t.

    返回
    :   - None

<a id="_CPPv427bk_touch_wakeup_channel_getv"></a>

<a id="_CPPv327bk_touch_wakeup_channel_getv"></a> <a id="_CPPv227bk_touch_wakeup_channel_getv"></a> <a id="bk_touch_wakeup_channel_get__void"></a> <a id="group__touch_1gafcacacc0fbce7d0c81ad10845d61abf6"></a> uint32\_t bk\_touch\_wakeup\_channel\_get(void)
:   set the touch channel for low voltage and deepsleep wake up

    This API set the touch channel for low voltage and deepsleep wake up

    参数
    :   **\-** – None

    返回
    :   - s\_touch\_wakeup\_channel: the channel number of touch

<a id="_CPPv416bk_touch_pm_initv"></a>

<a id="_CPPv316bk_touch_pm_initv"></a> <a id="_CPPv216bk_touch_pm_initv"></a> <a id="bk_touch_pm_init__void"></a> <a id="group__touch_1ga78a2d9d3761bf7676e4e05517bd70269"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_pm\_init(void)
:   Register touch low voltage and deepsleep config.

    This API register touch low voltage and deepsleep config

    参数
    :   **\-** – None

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_touch_register_touch_isr15touch_channel_t11touch_isr_tPv"></a>

<a id="_CPPv327bk_touch_register_touch_isr15touch_channel_t11touch_isr_tPv"></a> <a id="_CPPv227bk_touch_register_touch_isr15touch_channel_t11touch_isr_tPv"></a> <a id="bk_touch_register_touch_isr__touch_channel_t.touch_isr_t.voidP"></a> <a id="group__touch_1gad74e9c383d2fe4137cf17736c056ae04"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_touch\_register\_touch\_isr([touch\_channel\_t](#_CPPv415touch_channel_t "touch_channel_t") touch\_id, [touch\_isr\_t](#_CPPv411touch_isr_t "touch_isr_t") isr, void \*param)
:   Register touch isr.

    This API register touch isr

    参数
    :   **\-** – touch\_id: touch channel, channel 0 \~ channel 15;

        - isr: touch isr callback;
        - param: touch isr callback parameter;

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="api-typedefs"></a>

## API Typedefs

<a id="id1"></a>

### Header File

- [touch\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/touch_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv418touch_int_config_t"></a>

<a id="_CPPv318touch_int_config_t"></a> <a id="_CPPv218touch_int_config_t"></a> <a id="touch_int_config_t"></a> <a id="structtouch__int__config__t"></a> struct touch\_int\_config\_t

<a id="_CPPv414touch_config_t"></a>

<a id="_CPPv314touch_config_t"></a> <a id="_CPPv214touch_config_t"></a> <a id="touch_config_t"></a> <a id="structtouch__config__t"></a> struct touch\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14touch_config_t17sensitivity_levelE"></a>

    <a id="_CPPv3N14touch_config_t17sensitivity_levelE"></a> <a id="_CPPv2N14touch_config_t17sensitivity_levelE"></a> <a id="touch_config_t::sensitivity_level__touch_sensitivity_level_t"></a> <a id="structtouch__config__t_1a39a6c62c2380639dd4b562da9fa0f805"></a> [touch\_sensitivity\_level\_t](#_CPPv425touch_sensitivity_level_t "touch_sensitivity_level_t") sensitivity\_level
    :   sensitivity\_level

    <a id="_CPPv4N14touch_config_t16detect_thresholdE"></a>

    <a id="_CPPv3N14touch_config_t16detect_thresholdE"></a> <a id="_CPPv2N14touch_config_t16detect_thresholdE"></a> <a id="touch_config_t::detect_threshold__touch_detect_threshold_t"></a> <a id="structtouch__config__t_1a54555905435914e1e91d6f76196bda42"></a> [touch\_detect\_threshold\_t](#_CPPv424touch_detect_threshold_t "touch_detect_threshold_t") detect\_threshold
    :   detect\_threshold

    <a id="_CPPv4N14touch_config_t12detect_rangeE"></a>

    <a id="_CPPv3N14touch_config_t12detect_rangeE"></a> <a id="_CPPv2N14touch_config_t12detect_rangeE"></a> <a id="touch_config_t::detect_range__touch_detect_range_t"></a> <a id="structtouch__config__t_1a007b423fe10419c865ced779682bb65d"></a> [touch\_detect\_range\_t](#_CPPv420touch_detect_range_t "touch_detect_range_t") detect\_range
    :   detect\_range

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_TOUCH_ID"></a>

<a id="touch__types_8h_1ab38bccd6d83c227922aab76170149ced"></a> BK\_ERR\_TOUCH\_ID

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv411touch_isr_t"></a>

<a id="_CPPv311touch_isr_t"></a> <a id="_CPPv211touch_isr_t"></a> <a id="touch_isr_t"></a> <a id="touch__types_8h_1acfbbc7d6681a1e32c4c7570ddb132d95"></a> typedef void (\*touch\_isr\_t)(void \*param)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv415touch_channel_t"></a>

<a id="_CPPv315touch_channel_t"></a> <a id="_CPPv215touch_channel_t"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74f"></a> enum touch\_channel\_t
:   *Values:*

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_0E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_0E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_0E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fad93388e3fea32fefbf67004db8aeae61"></a> enumerator BK\_TOUCH\_0
    :   touch channel 0

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_1E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_1E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_1E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa57a7aa93e1da7fa9bbed316ca3aa940b"></a> enumerator BK\_TOUCH\_1
    :   touch channel 1

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_2E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_2E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_2E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fab30cd7b899e9196ab2cd988b2c161696"></a> enumerator BK\_TOUCH\_2
    :   touch channel 2

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_3E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_3E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_3E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74faa2854deeda376f5ae105e3062cf309f6"></a> enumerator BK\_TOUCH\_3
    :   touch channel 3

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_4E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_4E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_4E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa17354881c972ef6723d208f7ba47c0b6"></a> enumerator BK\_TOUCH\_4
    :   touch channel 4

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_5E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_5E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_5E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa5575887e7b5a9e2e64189b834996255e"></a> enumerator BK\_TOUCH\_5
    :   touch channel 5

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_6E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_6E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_6E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fae383160039414bde7afd15637f54cde1"></a> enumerator BK\_TOUCH\_6
    :   touch channel 6

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_7E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_7E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_7E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa4135c03990581de6821594155407a81f"></a> enumerator BK\_TOUCH\_7
    :   touch channel 7

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_8E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_8E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_8E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa75d0eb57a69ddb5f400690fb037ab571"></a> enumerator BK\_TOUCH\_8
    :   touch channel 8

    <a id="_CPPv4N15touch_channel_t10BK_TOUCH_9E"></a>

    <a id="_CPPv3N15touch_channel_t10BK_TOUCH_9E"></a> <a id="_CPPv2N15touch_channel_t10BK_TOUCH_9E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa94cac367698a7f3085c437b20687d2f9"></a> enumerator BK\_TOUCH\_9
    :   touch channel 9

    <a id="_CPPv4N15touch_channel_t11BK_TOUCH_10E"></a>

    <a id="_CPPv3N15touch_channel_t11BK_TOUCH_10E"></a> <a id="_CPPv2N15touch_channel_t11BK_TOUCH_10E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fac61dcc0945b50376aee57d8b6986e172"></a> enumerator BK\_TOUCH\_10
    :   touch channel 10

    <a id="_CPPv4N15touch_channel_t11BK_TOUCH_11E"></a>

    <a id="_CPPv3N15touch_channel_t11BK_TOUCH_11E"></a> <a id="_CPPv2N15touch_channel_t11BK_TOUCH_11E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa040c74b26152248f97074d7d0decc592"></a> enumerator BK\_TOUCH\_11
    :   touch channel 11

    <a id="_CPPv4N15touch_channel_t11BK_TOUCH_12E"></a>

    <a id="_CPPv3N15touch_channel_t11BK_TOUCH_12E"></a> <a id="_CPPv2N15touch_channel_t11BK_TOUCH_12E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa56b6eab888096942c74b4e442f311478"></a> enumerator BK\_TOUCH\_12
    :   touch channel 12

    <a id="_CPPv4N15touch_channel_t11BK_TOUCH_13E"></a>

    <a id="_CPPv3N15touch_channel_t11BK_TOUCH_13E"></a> <a id="_CPPv2N15touch_channel_t11BK_TOUCH_13E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa4b0da4b09b5324bbc005625e3f7bcf3b"></a> enumerator BK\_TOUCH\_13
    :   touch channel 13

    <a id="_CPPv4N15touch_channel_t11BK_TOUCH_14E"></a>

    <a id="_CPPv3N15touch_channel_t11BK_TOUCH_14E"></a> <a id="_CPPv2N15touch_channel_t11BK_TOUCH_14E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa1980be9ee396a7371508d4df6562de35"></a> enumerator BK\_TOUCH\_14
    :   touch channel 14

    <a id="_CPPv4N15touch_channel_t11BK_TOUCH_15E"></a>

    <a id="_CPPv3N15touch_channel_t11BK_TOUCH_15E"></a> <a id="_CPPv2N15touch_channel_t11BK_TOUCH_15E"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa6fbe87f5faa4173e893adbb116fb4d9f"></a> enumerator BK\_TOUCH\_15
    :   touch channel 15

    <a id="_CPPv4N15touch_channel_t12BK_TOUCH_MAXE"></a>

    <a id="_CPPv3N15touch_channel_t12BK_TOUCH_MAXE"></a> <a id="_CPPv2N15touch_channel_t12BK_TOUCH_MAXE"></a> <a id="touch__types_8h_1a181ca1ffa9cce000a1a79788a892a74fa5f4f01ff6ffd23888e3cd97dce0664e3"></a> enumerator BK\_TOUCH\_MAX

<a id="_CPPv425touch_sensitivity_level_t"></a>

<a id="_CPPv325touch_sensitivity_level_t"></a> <a id="_CPPv225touch_sensitivity_level_t"></a> <a id="touch__types_8h_1ac1334156b5661cb871beb2f279ac9377"></a> enum touch\_sensitivity\_level\_t
:   *Values:*

    <a id="_CPPv4N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_0E"></a>

    <a id="_CPPv3N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_0E"></a> <a id="_CPPv2N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_0E"></a> <a id="touch__types_8h_1ac1334156b5661cb871beb2f279ac9377a1eedd07d3227669af98c584104bd77b6"></a> enumerator TOUCH\_SENSITIVITY\_LEVLE\_0

    <a id="_CPPv4N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_1E"></a>

    <a id="_CPPv3N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_1E"></a> <a id="_CPPv2N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_1E"></a> <a id="touch__types_8h_1ac1334156b5661cb871beb2f279ac9377ad1a0d6f845ed4fb9903cbf738d6759fc"></a> enumerator TOUCH\_SENSITIVITY\_LEVLE\_1

    <a id="_CPPv4N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_2E"></a>

    <a id="_CPPv3N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_2E"></a> <a id="_CPPv2N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_2E"></a> <a id="touch__types_8h_1ac1334156b5661cb871beb2f279ac9377a3407caf7b398a88d038bc3c0980f912b"></a> enumerator TOUCH\_SENSITIVITY\_LEVLE\_2

    <a id="_CPPv4N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_3E"></a>

    <a id="_CPPv3N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_3E"></a> <a id="_CPPv2N25touch_sensitivity_level_t25TOUCH_SENSITIVITY_LEVLE_3E"></a> <a id="touch__types_8h_1ac1334156b5661cb871beb2f279ac9377a37dbc917dbeedc4970cf43df149f97f4"></a> enumerator TOUCH\_SENSITIVITY\_LEVLE\_3

<a id="_CPPv424touch_detect_threshold_t"></a>

<a id="_CPPv324touch_detect_threshold_t"></a> <a id="_CPPv224touch_detect_threshold_t"></a> <a id="touch__types_8h_1a169e10069335f4f0b1e65a3d99e1fd16"></a> enum touch\_detect\_threshold\_t
:   *Values:*

    <a id="_CPPv4N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_0E"></a>

    <a id="_CPPv3N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_0E"></a> <a id="_CPPv2N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_0E"></a> <a id="touch__types_8h_1a169e10069335f4f0b1e65a3d99e1fd16ae092b4bd3cc6f4c9045c71059c98879e"></a> enumerator TOUCH\_DETECT\_THRESHOLD\_0

    <a id="_CPPv4N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_1E"></a>

    <a id="_CPPv3N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_1E"></a> <a id="_CPPv2N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_1E"></a> <a id="touch__types_8h_1a169e10069335f4f0b1e65a3d99e1fd16aca4073f9250f056fe7d4458db09a3976"></a> enumerator TOUCH\_DETECT\_THRESHOLD\_1

    <a id="_CPPv4N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_2E"></a>

    <a id="_CPPv3N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_2E"></a> <a id="_CPPv2N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_2E"></a> <a id="touch__types_8h_1a169e10069335f4f0b1e65a3d99e1fd16af2cae4cc3e77b2de4256cb7e01ecf671"></a> enumerator TOUCH\_DETECT\_THRESHOLD\_2

    <a id="_CPPv4N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_3E"></a>

    <a id="_CPPv3N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_3E"></a> <a id="_CPPv2N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_3E"></a> <a id="touch__types_8h_1a169e10069335f4f0b1e65a3d99e1fd16a98ca34f103f59615e1471ba7f713a884"></a> enumerator TOUCH\_DETECT\_THRESHOLD\_3

    <a id="_CPPv4N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_4E"></a>

    <a id="_CPPv3N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_4E"></a> <a id="_CPPv2N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_4E"></a> <a id="touch__types_8h_1a169e10069335f4f0b1e65a3d99e1fd16a21f342ff57488fdb1ffd563855b4f22f"></a> enumerator TOUCH\_DETECT\_THRESHOLD\_4

    <a id="_CPPv4N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_5E"></a>

    <a id="_CPPv3N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_5E"></a> <a id="_CPPv2N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_5E"></a> <a id="touch__types_8h_1a169e10069335f4f0b1e65a3d99e1fd16a9a308c472f61f2b5c56b21b4280180ec"></a> enumerator TOUCH\_DETECT\_THRESHOLD\_5

    <a id="_CPPv4N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_6E"></a>

    <a id="_CPPv3N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_6E"></a> <a id="_CPPv2N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_6E"></a> <a id="touch__types_8h_1a169e10069335f4f0b1e65a3d99e1fd16a589bbd0507967dad87015b3071fa90e8"></a> enumerator TOUCH\_DETECT\_THRESHOLD\_6

    <a id="_CPPv4N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_7E"></a>

    <a id="_CPPv3N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_7E"></a> <a id="_CPPv2N24touch_detect_threshold_t24TOUCH_DETECT_THRESHOLD_7E"></a> <a id="touch__types_8h_1a169e10069335f4f0b1e65a3d99e1fd16adee4f067c8af45c30aafc13a5fce6424"></a> enumerator TOUCH\_DETECT\_THRESHOLD\_7

<a id="_CPPv420touch_detect_range_t"></a>

<a id="_CPPv320touch_detect_range_t"></a> <a id="_CPPv220touch_detect_range_t"></a> <a id="touch__types_8h_1a4c1f3b73e584bd18fdaaa092c98373dd"></a> enum touch\_detect\_range\_t
:   *Values:*

    <a id="_CPPv4N20touch_detect_range_t22TOUCH_DETECT_RANGE_8PFE"></a>

    <a id="_CPPv3N20touch_detect_range_t22TOUCH_DETECT_RANGE_8PFE"></a> <a id="_CPPv2N20touch_detect_range_t22TOUCH_DETECT_RANGE_8PFE"></a> <a id="touch__types_8h_1a4c1f3b73e584bd18fdaaa092c98373dda0a7e7a6727b898e2d6a2612b52e658d1"></a> enumerator TOUCH\_DETECT\_RANGE\_8PF
    :   8PF

    <a id="_CPPv4N20touch_detect_range_t23TOUCH_DETECT_RANGE_12PFE"></a>

    <a id="_CPPv3N20touch_detect_range_t23TOUCH_DETECT_RANGE_12PFE"></a> <a id="_CPPv2N20touch_detect_range_t23TOUCH_DETECT_RANGE_12PFE"></a> <a id="touch__types_8h_1a4c1f3b73e584bd18fdaaa092c98373dda8178b2913ced27fd01745e510f3e9608"></a> enumerator TOUCH\_DETECT\_RANGE\_12PF
    :   12PF

    <a id="_CPPv4N20touch_detect_range_t23TOUCH_DETECT_RANGE_19PFE"></a>

    <a id="_CPPv3N20touch_detect_range_t23TOUCH_DETECT_RANGE_19PFE"></a> <a id="_CPPv2N20touch_detect_range_t23TOUCH_DETECT_RANGE_19PFE"></a> <a id="touch__types_8h_1a4c1f3b73e584bd18fdaaa092c98373dda0bb1b931fb3ed29697a33f3274fc994a"></a> enumerator TOUCH\_DETECT\_RANGE\_19PF
    :   19PF

    <a id="_CPPv4N20touch_detect_range_t23TOUCH_DETECT_RANGE_27PFE"></a>

    <a id="_CPPv3N20touch_detect_range_t23TOUCH_DETECT_RANGE_27PFE"></a> <a id="_CPPv2N20touch_detect_range_t23TOUCH_DETECT_RANGE_27PFE"></a> <a id="touch__types_8h_1a4c1f3b73e584bd18fdaaa092c98373dda7b8eb1e6fcab8186f522975faff0ebc3"></a> enumerator TOUCH\_DETECT\_RANGE\_27PF
    :   27PF
