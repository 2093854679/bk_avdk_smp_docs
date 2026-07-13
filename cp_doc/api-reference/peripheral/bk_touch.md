# TOUCH


BK7259 CP 侧 Touch API（`include/driver/touch.h`）。


## Touch API Reference


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

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_mode_select_set(uint32_t mode)
:   set touch calibration interface mode (SPI or digital)

    This API selects the calibration readback interface mode via ana_reg34.modsel_spi. Set to 0 for digital mode (default); set to 1 for SPI mode.

    参数
    :   **-** – mode: 0 — digital mode; 1 — SPI mode

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_set_test_mode(uint8_t period, uint8_t number)
:   set touch detection test period and test number

    This API configures the touch detection test parameters via ana_reg33. test_period controls the detection window length; test_number controls how many consecutive detections are required to confirm a touch event.

    参数
    :   **-** – period: test period value (ana_reg33.test_period, bit[7:4])


        - number: test number value (ana_reg33.test_number, bit[3:0])

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_set_calib_mode(uint8_t period, uint8_t number)
:   set touch calibration charge length period and calibration number

    This API configures the calibration timing parameters via ana_reg34. cl_period sets the charge length period; cal_number sets the number of calibration cycles averaged to produce the final calibration result.

    参数
    :   **-** – period: charge length period (ana_reg34.cl_period, bit[31:23])


        - number: calibration cycle count (ana_reg34.cal_number, bit[22:19])

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_power_down(uint32_t enable)
:   power down or power on the touch analog front-end

    This API controls the pwd_td bit (sys.reg60 bit31) to power on or power off the touch analog circuit. Must be set to 0 (power on) before initiating any calibration or detection operation.

    参数
    :   **-** – enable: 1 — power down (disable touch analog); 0 — power on

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_detect_range_set(uint32_t crg)
:   set the touch sensor capacitance detect range (crg)

    This API sets the detect range field crg (sys.reg60 bit[21:20]) which selects the reference capacitor range for calibration: 0 — 8 pF, 1 — 12 pF, 2 — 19 pF, 3 — 27 pF. During multi-range calibration, crg is incremented until cap_out < 0x1F0.

    参数
    :   **-** – crg: detect range index (0–3); see touch_detect_range_t for named values

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_gain_s_set(uint32_t value)
:   set the touch sensor analog gain (gain_s)

    This API sets the gain_s field (sys.reg60 bit[29:26]) which controls the amplifier gain of the touch analog front-end. Recommended optimal value: 1.

    参数
    :   **-** – value: gain value (0–15)

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_vrefs_set(uint32_t value)
:   set the touch sensor reference voltage (vrefs)

    This API sets the vrefs field (sys.reg60 bit[25:22]) which selects the internal reference voltage level used for touch detection comparison. Recommended optimal value: 2.

    参数
    :   **-** – value: reference voltage selection (0–15)

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_cal_vth_set(uint32_t value)
:   set the touch calibration voltage threshold (cal_vth)

    This API sets the cal_vth field (sys.reg60 bit[19:17]) which controls the voltage threshold used during hardware auto-calibration. Recommended optimal value: 2.

    参数
    :   **-** – value: calibration voltage threshold (0–7)

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_cal_auto_set(uint32_t enable)
:   enable or disable touch automatic calibration mode

    This API controls the en_cal_auto bit (sys.reg61 bit30). When enabled, the hardware triggers calibration automatically at a fixed interval. Must be set to 0 before using force calibration (en_cal_force).

    参数
    :   **-** – enable: 1 — enable auto calibration; 0 — disable

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_cal_done_clr(uint32_t value)
:   clear the touch calibration done flag

    This API writes to cal_done_clr (sys.reg61 bit28) to reset the hardware calibration completion flag before starting a new calibration sequence. Should be set to 1 prior to triggering en_cal_force.

    参数
    :   **-** – value: write 1 to clear the calibration done status

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_rstb_dig_set(uint32_t value)
:   set the touch digital reset signal (rstb_dig)

    This API controls the rstb_dig bit (sys.reg60 bit8) which holds the touch digital logic in reset when set to 1. Must be cleared to 0 before initiating calibration or detection.

    参数
    :   **-** – value: 1 — assert reset; 0 — release reset

    返回
    :   - BK_OK: succeed

uint32_t bk_touch_rstb_dig_get(void)
:   get the current value of the touch digital reset signal (rstb_dig)

    This API reads the rstb_dig bit (sys.reg60 bit8).

    参数
    :   **-** – None

    返回
    :   - 0: reset not asserted (normal operation)

        - 1: reset asserted

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_touch_ldoen_set(uint32_t value)
:   set the touch analog LDO enable signal (ldoen)

    This API controls the ldoen bit (sys.reg60 bit5) which enables the internal LDO powering the touch analog front-end. Must be cleared to 0 before calibration to ensure the LDO is in the correct initial state.

    参数
    :   **-** – value: 1 — enable LDO; 0 — disable LDO

    返回
    :   - BK_OK: succeed

uint32_t bk_touch_ldoen_get(void)
:   get the current value of the touch analog LDO enable signal (ldoen)

    This API reads the ldoen bit (sys.reg60 bit5).

    参数
    :   **-** – None

    返回
    :   - 0: LDO disabled

        - 1: LDO enabled

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


## Touch API Typedefs


### Header File


- [touch_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/touch_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/touch_types.h")


### Structures

struct touch_int_config_t

struct touch_config_t
:   Public Members

    [touch_sensitivity_level_t](#_CPPv425touch_sensitivity_level_t "touch_sensitivity_level_t") sensitivity_level
    :   sensitivity_level

    [touch_detect_threshold_t](#_CPPv424touch_detect_threshold_t "touch_detect_threshold_t") detect_threshold
    :   detect_threshold

    [touch_detect_range_t](#_CPPv420touch_detect_range_t "touch_detect_range_t") detect_range
    :   detect_range


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
