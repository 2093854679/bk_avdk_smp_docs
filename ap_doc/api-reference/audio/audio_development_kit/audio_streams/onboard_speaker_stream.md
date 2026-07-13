# Onboard Speaker Stream


The onboard speaker stream writes audio data to onboard speaker.


## API Reference


### Header File


- [bk_audio/audio_streams/onboard_speaker_stream.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/onboard_speaker_stream.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/onboard_speaker_stream.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_speaker_stream_init([onboard_speaker_stream_cfg_t](#_CPPv428onboard_speaker_stream_cfg_t "onboard_speaker_stream_cfg_t") *config)
:   Create a handle to an Audio Element to stream data from another Element to play.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The Audio Element handle


        - Not NULL: success

        - NULL: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_speaker_stream_set_param([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_speaker_stream, int rate, int bits, int ch)
:   Updata onboard speaker stream include sample rate, bits and channel number on running.

    参数
    :   - **onboard_speaker_stream** – **[in]** element handle

        - **rate** – **[in]** sample rate

        - **bits** – **[in]** sample bit

        - **ch** – **[in]** channel number

    返回
    :   Result


        - BK_OK: success

        - other: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_speaker_stream_set_digital_gain([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_speaker_stream, uint8_t gain)
:   Updata onboard speaker stream digital gain.

    参数
    :   - **onboard_speaker_stream** – **[in]** element handle

        - **gain** – **[in]** speaker digital gain, range: 0x00 ~ 0x3f(-45db ~ 18db, 0x2d: 0db)

    返回
    :   Result


        - BK_OK: success

        - other: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_speaker_stream_get_digital_gain([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_speaker_stream, uint8_t *gain)
:   Get onboard speaker stream digital gain.

    参数
    :   - **onboard_speaker_stream** – **[in]** element handle

        - **gain** – **[inout]** speaker digital gain

    返回
    :   Result


        - BK_OK: success

        - other: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_speaker_stream_dac_mute_en([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_speaker_stream, uint8_t value)
:   Control onboard audio dac mute.

    参数
    :   - **onboard_speaker_stream** – **[in]** element handle

        - **value** – **[in]** mute value (1: mute, 0: unmute)

    返回
    :   Result


        - BK_OK: success

        - other: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_speaker_stream_set_analog_gain([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_speaker_stream, uint8_t gain)
:   Update onboard speaker stream analog gain.

    参数
    :   - **onboard_speaker_stream** – **[in]** element handle

        - **gain** – **[in]** speaker analog gain, range: 0x00 ~ 0x3f

    返回
    :   Result


        - BK_OK: success

        - other: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard_speaker_stream_get_analog_gain([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard_speaker_stream, uint8_t *gain)
:   Get onboard speaker stream analog gain.

    参数
    :   - **onboard_speaker_stream** – **[in]** element handle

        - **gain** – **[inout]** speaker analog gain

    返回
    :   Result


        - BK_OK: success

        - other: failed


### Structures

struct onboard_speaker_stream_cfg_t
:   Onboard Speaker Stream configurations, if any entry is zero then the configuration will be set to default values.

    Public Members

    uint8_t chl_num
    :   speaker channel number

    uint32_t sample_rate
    :   speaker sample rate

    int32_t dig_gain
    :   audio dac digital gain: value range: 0x00 ~ 0x3f(-45db ~ 18db, 0x2d: 0db), suggest: 0x2d

    int32_t ana_gain
    :   audio dac analog gain: value range: 0x00 ~ 0x3f(-15db ~ 0db, 1db/step), suggest: 0x0A

    aud_dac_work_mode_t work_mode
    :   audio dac mode: signal_ended/differen

    uint8_t bits
    :   Bit wide (8, 16, 24, 32 bits)

    aud_clk_t clk_src
    :   audio clock: XTAL(26MHz)/APLL

    int multi_in_port_num
    :   The number of multiple input audio port

    int multi_out_port_num
    :   The number of multiple output audio port

    uint32_t frame_size
    :   the length of one frame speaker data dma carried (suggest 20ms data)

    uint32_t pool_length
    :   speaker data pool size, the unit is byte

    uint32_t pool_play_thold
    :   the play threshold of pool, the unit is byte

    uint32_t pool_pause_thold
    :   the pause threshold of pool, the unit is byte

    bool pa_ctrl_en
    :   control pa enable

    uint16_t pa_ctrl_gpio
    :   the gpio id of control pa

    uint8_t pa_on_level
    :   the gpio level of turn on pa, 0: low level, 1: high level

    uint32_t pa_on_delay
    :   the delay time(ms) of turn on pa after enable audio dac. [dac init -> delay -> pa turn on]

    uint32_t pa_off_delay
    :   the delay time(ms) of disable audio dac after turn off pa. [mute -> pa turn off -> delay -> dac deinit]

    int task_stack
    :   Task stack size

    int task_core
    :   Task running in core (0 or 1)

    int task_prio
    :   Task priority (based on freeRTOS priority)


### Macros

ONBOARD_SPEAKER_STREAM_TASK_STACK

ONBOARD_SPEAKER_STREAM_TASK_CORE

ONBOARD_SPEAKER_STREAM_TASK_PRIO

ONBOARD_SPEAKER_STREAM_CFG_DEFAULT()

DEFAULT_ONBOARD_SPEAKER_STREAM_CONFIG()
