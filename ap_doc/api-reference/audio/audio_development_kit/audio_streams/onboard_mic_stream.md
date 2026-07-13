# Onboard MIC Stream


The onboard mic stream reads audio data from onboard mic.


## API Reference


### Header File


- [bk_audio/audio_streams/onboard_mic_stream.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/onboard_mic_stream.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/onboard_mic_stream.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_mic_stream_init([onboard_mic_stream_cfg_t](#_CPPv424onboard_mic_stream_cfg_t "onboard_mic_stream_cfg_t") *config)
:   Create a handle to an Audio Element to stream data to another Element.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The Audio Element handle


        - Not NULL: success

        - NULL: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_mic_stream_set_digital_gain([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_mic_stream, uint8_t gain)
:   Updata onboard mic stream digital gain.

    参数
    :   - **onboard_mic_stream** – **[in]** element handle

        - **gain** – **[in]** mic digital gain, range: 0x00 ~ 0x3f(-45db ~ 18db, 0x2d: 0db)

    返回
    :   Result


        - BK_OK: success

        - other: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_mic_stream_get_digital_gain([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_mic_stream, uint8_t *gain)
:   Get onboard mic stream digital gain.

    参数
    :   - **onboard_mic_stream** – **[in]** element handle

        - **gain** – **[inout]** mic digital gain

    返回
    :   Result


        - BK_OK: success

        - other: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_mic_stream_set_analog_gain([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_mic_stream, uint8_t gain)
:   Update onboard mic stream analog gain.

    参数
    :   - **onboard_mic_stream** – **[in]** element handle

        - **gain** – **[in]** mic analog gain, range: 0x00 ~ 0x3f

    返回
    :   Result


        - BK_OK: success

        - other: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_mic_stream_get_analog_gain([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_mic_stream, uint8_t *gain)
:   Get onboard mic stream analog gain.

    参数
    :   - **onboard_mic_stream** – **[in]** element handle

        - **gain** – **[inout]** mic analog gain

    返回
    :   Result


        - BK_OK: success

        - other: failed


### Structures

struct adc_cfg_t
:   ADC mode configurations, if any entry is zero then the configuration will be set to default values.

    Public Members

    uint8_t chl_num
    :   mic channel number

    uint8_t bits
    :   Bit wide (16 or 24 bits)

    uint32_t sample_rate
    :   mic sample rate

    int32_t dig_gain
    :   audio adc digital gain: value range: 0x00 ~ 0x3f(-45db ~ 18db, 0x2d: 0db), suggest: 0x2d

    int32_t ana_gain
    :   audio adc analog gain: value range: , suggest:

    aud_adc_mode_t mode
    :   mic interface mode: signal_ended/differen

    aud_clk_t clk_src
    :   audio clock: XTAL(26MHz)/APLL

struct onboard_mic_stream_cfg_t
:   Onboard MIC Stream configurations, if any entry is zero then the configuration will be set to default values.

    Public Members

    [adc_cfg_t](#_CPPv49adc_cfg_t "adc_cfg_t") adc_cfg
    :   ADC mode configuration

    uint32_t frame_size
    :   the length of one frame (bytes)

    int out_block_size
    :   Size of output block

    int out_block_num
    :   Number of output block

    int multi_out_port_num
    :   The number of multiple output audio port

    int task_stack
    :   Task stack size

    int task_core
    :   Task running in core (0 or 1)

    int task_prio
    :   Task priority (based on freeRTOS priority)


### Macros

ONBOARD_MIC_STREAM_TASK_STACK

ONBOARD_MIC_STREAM_TASK_CORE

ONBOARD_MIC_STREAM_TASK_PRIO

ONBOARD_MIC_ADC_STREAM_CFG_DEFAULT()

DEFAULT_ONBOARD_MIC_ADC_STREAM_CONFIG()
