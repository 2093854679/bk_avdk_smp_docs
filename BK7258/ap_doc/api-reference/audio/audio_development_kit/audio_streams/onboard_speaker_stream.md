---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_streams/onboard_speaker_stream.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="onboard-speaker-stream"></a>

# Onboard Speaker Stream

The onboard speaker stream writes audio data to onboard speaker.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [onboard\_speaker\_stream.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_streams/onboard_speaker_stream.h)

<a id="functions"></a>

### Functions

<a id="_CPPv427onboard_speaker_stream_initP28onboard_speaker_stream_cfg_t"></a>

<a id="_CPPv327onboard_speaker_stream_initP28onboard_speaker_stream_cfg_t"></a> <a id="_CPPv227onboard_speaker_stream_initP28onboard_speaker_stream_cfg_t"></a> <a id="onboard_speaker_stream_init__onboard_speaker_stream_cfg_tP"></a> <a id="onboard__speaker__stream_8h_1a289b2c865e638184ed529cf87f98edde"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_speaker\_stream\_init([onboard\_speaker\_stream\_cfg\_t](#_CPPv428onboard_speaker_stream_cfg_t "onboard_speaker_stream_cfg_t") \*config)
:   Create a handle to an Audio Element to stream data from another Element to play.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The Audio Element handle

        - Not NULL: success
        - NULL: failed

<a id="_CPPv432onboard_speaker_stream_set_param22audio_element_handle_tiii"></a>

<a id="_CPPv332onboard_speaker_stream_set_param22audio_element_handle_tiii"></a> <a id="_CPPv232onboard_speaker_stream_set_param22audio_element_handle_tiii"></a> <a id="onboard_speaker_stream_set_param__audio_element_handle_t.i.i.i"></a> <a id="onboard__speaker__stream_8h_1a6be400e8e209504aca5c9463d3443184"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_speaker\_stream\_set\_param([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_speaker\_stream, int rate, int bits, int ch)
:   Updata onboard speaker stream include sample rate, bits and channel number on running.

    参数
    :   - **onboard\_speaker\_stream** – **\[in\]** element handle
        - **rate** – **\[in\]** sample rate
        - **bits** – **\[in\]** sample bit
        - **ch** – **\[in\]** channel number

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="_CPPv439onboard_speaker_stream_set_digital_gain22audio_element_handle_t7uint8_t"></a>

<a id="_CPPv339onboard_speaker_stream_set_digital_gain22audio_element_handle_t7uint8_t"></a> <a id="_CPPv239onboard_speaker_stream_set_digital_gain22audio_element_handle_t7uint8_t"></a> <a id="onboard_speaker_stream_set_digital_gain__audio_element_handle_t.uint8_t"></a> <a id="onboard__speaker__stream_8h_1a24222f600e0c3069d5370c2de38d2ae0"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_speaker\_stream\_set\_digital\_gain([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_speaker\_stream, uint8\_t gain)
:   Updata onboard speaker stream digital gain.

    参数
    :   - **onboard\_speaker\_stream** – **\[in\]** element handle
        - **gain** – **\[in\]** speaker digital gain, range: 0x00 \~ 0x3f(-45db \~ 18db, 0x2d: 0db)

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="_CPPv439onboard_speaker_stream_get_digital_gain22audio_element_handle_tP7uint8_t"></a>

<a id="_CPPv339onboard_speaker_stream_get_digital_gain22audio_element_handle_tP7uint8_t"></a> <a id="_CPPv239onboard_speaker_stream_get_digital_gain22audio_element_handle_tP7uint8_t"></a> <a id="onboard_speaker_stream_get_digital_gain__audio_element_handle_t.uint8_tP"></a> <a id="onboard__speaker__stream_8h_1a3212c04b5b016fdbdab060fb314f282d"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_speaker\_stream\_get\_digital\_gain([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_speaker\_stream, uint8\_t \*gain)
:   Get onboard speaker stream digital gain.

    参数
    :   - **onboard\_speaker\_stream** – **\[in\]** element handle
        - **gain** – **\[inout\]** speaker digital gain

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="_CPPv434onboard_speaker_stream_dac_mute_en22audio_element_handle_t7uint8_t"></a>

<a id="_CPPv334onboard_speaker_stream_dac_mute_en22audio_element_handle_t7uint8_t"></a> <a id="_CPPv234onboard_speaker_stream_dac_mute_en22audio_element_handle_t7uint8_t"></a> <a id="onboard_speaker_stream_dac_mute_en__audio_element_handle_t.uint8_t"></a> <a id="onboard__speaker__stream_8h_1aca03be168725dcfde2553300aa095a92"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_speaker\_stream\_dac\_mute\_en([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_speaker\_stream, uint8\_t value)
:   Control onboard audio dac mute.

    参数
    :   - **onboard\_speaker\_stream** – **\[in\]** element handle
        - **value** – **\[in\]** mute value (1: mute, 0: unmute)

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="_CPPv438onboard_speaker_stream_set_analog_gain22audio_element_handle_t7uint8_t"></a>

<a id="_CPPv338onboard_speaker_stream_set_analog_gain22audio_element_handle_t7uint8_t"></a> <a id="_CPPv238onboard_speaker_stream_set_analog_gain22audio_element_handle_t7uint8_t"></a> <a id="onboard_speaker_stream_set_analog_gain__audio_element_handle_t.uint8_t"></a> <a id="onboard__speaker__stream_8h_1a80036ee64d03cd71b0a3945422ef6dda"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_speaker\_stream\_set\_analog\_gain([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_speaker\_stream, uint8\_t gain)
:   Update onboard speaker stream analog gain.

    参数
    :   - **onboard\_speaker\_stream** – **\[in\]** element handle
        - **gain** – **\[in\]** speaker analog gain, range: 0x00 \~ 0x3f

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="_CPPv438onboard_speaker_stream_get_analog_gain22audio_element_handle_tP7uint8_t"></a>

<a id="_CPPv338onboard_speaker_stream_get_analog_gain22audio_element_handle_tP7uint8_t"></a> <a id="_CPPv238onboard_speaker_stream_get_analog_gain22audio_element_handle_tP7uint8_t"></a> <a id="onboard_speaker_stream_get_analog_gain__audio_element_handle_t.uint8_tP"></a> <a id="onboard__speaker__stream_8h_1afa63a59ecf6da1c38fe594721cbc70ab"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_speaker\_stream\_get\_analog\_gain([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_speaker\_stream, uint8\_t \*gain)
:   Get onboard speaker stream analog gain.

    参数
    :   - **onboard\_speaker\_stream** – **\[in\]** element handle
        - **gain** – **\[inout\]** speaker analog gain

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="_CPPv448onboard_speaker_stream_set_input_port_data_valid22audio_element_handle_t7uint8_tb"></a>

<a id="_CPPv348onboard_speaker_stream_set_input_port_data_valid22audio_element_handle_t7uint8_tb"></a> <a id="_CPPv248onboard_speaker_stream_set_input_port_data_valid22audio_element_handle_t7uint8_tb"></a> <a id="onboard_speaker_stream_set_input_port_data_valid__audio_element_handle_t.uint8_t.b"></a> <a id="onboard__speaker__stream_8h_1a0fa3860cd9078ce82533a2abe8b79476"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_speaker\_stream\_set\_input\_port\_data\_valid([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_speaker\_stream, uint8\_t port\_id, bool valid)
:   Set input port data validity. When port data is valid, the data from the port can be used for playback. When port data is invalid, the data from the port will be replaced with silence packets.

    参数
    :   - **onboard\_speaker\_stream** – **\[in\]** element handle
        - **port\_id** – **\[in\]** port id (0: element-\>in, \>\=1: element-\>multi\_in)
        - **valid** – **\[in\]** port data validity (true: valid, false: invalid)

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="structures"></a>

### Structures

<a id="_CPPv428onboard_speaker_stream_cfg_t"></a>

<a id="_CPPv328onboard_speaker_stream_cfg_t"></a> <a id="_CPPv228onboard_speaker_stream_cfg_t"></a> <a id="onboard_speaker_stream_cfg_t"></a> <a id="structonboard__speaker__stream__cfg__t"></a> struct onboard\_speaker\_stream\_cfg\_t
:   Onboard Speaker Stream configurations, if any entry is zero then the configuration will be set to default values.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t7chl_numE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t7chl_numE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t7chl_numE"></a> <a id="onboard_speaker_stream_cfg_t::chl_num__uint8_t"></a> <a id="structonboard__speaker__stream__cfg__t_1abd12516f2140c5163fc97413ced5e66c"></a> uint8\_t chl\_num
    :   speaker channel number

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t11sample_rateE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t11sample_rateE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t11sample_rateE"></a> <a id="onboard_speaker_stream_cfg_t::sample_rate__uint32_t"></a> <a id="structonboard__speaker__stream__cfg__t_1a87f79c08b71894f867671d85d524b749"></a> uint32\_t sample\_rate
    :   speaker sample rate

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t8dig_gainE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t8dig_gainE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t8dig_gainE"></a> <a id="onboard_speaker_stream_cfg_t::dig_gain__int32_t"></a> <a id="structonboard__speaker__stream__cfg__t_1aa9e0c408b397b0404faf416b26b5dcf8"></a> int32\_t dig\_gain
    :   audio dac digital gain: value range: 0x00 \~ 0x3f(-45db \~ 18db, 0x2d: 0db), suggest: 0x2d

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t8ana_gainE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t8ana_gainE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t8ana_gainE"></a> <a id="onboard_speaker_stream_cfg_t::ana_gain__int32_t"></a> <a id="structonboard__speaker__stream__cfg__t_1ad45ac3fa62e23291dbd666db5af6c111"></a> int32\_t ana\_gain
    :   audio dac analog gain: value range: 0x00 \~ 0x3f(-15db \~ 0db, 1db/step), suggest: 0x0A

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t9work_modeE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t9work_modeE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t9work_modeE"></a> <a id="onboard_speaker_stream_cfg_t::work_mode__aud_dac_work_mode_t"></a> <a id="structonboard__speaker__stream__cfg__t_1a0a854cfb97b02b9347ec2856119aa56e"></a> aud\_dac\_work\_mode\_t work\_mode
    :   audio dac mode: signal\_ended/differen

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t4bitsE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t4bitsE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t4bitsE"></a> <a id="onboard_speaker_stream_cfg_t::bits__uint8_t"></a> <a id="structonboard__speaker__stream__cfg__t_1a2fb4f90448ad08deaba90536ad1fedec"></a> uint8\_t bits
    :   Bit wide (8, 16, 24, 32 bits)

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t7clk_srcE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t7clk_srcE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t7clk_srcE"></a> <a id="onboard_speaker_stream_cfg_t::clk_src__aud_clk_t"></a> <a id="structonboard__speaker__stream__cfg__t_1afeffdada5b46582e95def3d0c379c365"></a> aud\_clk\_t clk\_src
    :   audio clock: XTAL(26MHz)/APLL

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t17multi_in_port_numE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t17multi_in_port_numE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t17multi_in_port_numE"></a> <a id="onboard_speaker_stream_cfg_t::multi_in_port_num__i"></a> <a id="structonboard__speaker__stream__cfg__t_1a86961d2330796d2a602ee036e54d045d"></a> int multi\_in\_port\_num
    :   The number of multiple input audio port

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t18multi_out_port_numE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t18multi_out_port_numE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t18multi_out_port_numE"></a> <a id="onboard_speaker_stream_cfg_t::multi_out_port_num__i"></a> <a id="structonboard__speaker__stream__cfg__t_1a6535df02f05a2df6e4ac348a75d9c347"></a> int multi\_out\_port\_num
    :   The number of multiple output audio port

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t10frame_sizeE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t10frame_sizeE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t10frame_sizeE"></a> <a id="onboard_speaker_stream_cfg_t::frame_size__uint32_t"></a> <a id="structonboard__speaker__stream__cfg__t_1ad9b60b2e1830ccd8bee406ee5b928036"></a> uint32\_t frame\_size
    :   the length of one frame speaker data dma carried (suggest 20ms data)

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t11pool_lengthE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t11pool_lengthE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t11pool_lengthE"></a> <a id="onboard_speaker_stream_cfg_t::pool_length__uint32_t"></a> <a id="structonboard__speaker__stream__cfg__t_1aa526b518679a4e596b655bfc96ec29e3"></a> uint32\_t pool\_length
    :   speaker data pool size, the unit is byte

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t15pool_play_tholdE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t15pool_play_tholdE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t15pool_play_tholdE"></a> <a id="onboard_speaker_stream_cfg_t::pool_play_thold__uint32_t"></a> <a id="structonboard__speaker__stream__cfg__t_1ac9e51901a95a4961d537be03a7495497"></a> uint32\_t pool\_play\_thold
    :   the play threshold of pool, the unit is byte

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t16pool_pause_tholdE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t16pool_pause_tholdE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t16pool_pause_tholdE"></a> <a id="onboard_speaker_stream_cfg_t::pool_pause_thold__uint32_t"></a> <a id="structonboard__speaker__stream__cfg__t_1af5386d496c321582e108359b478e0ff2"></a> uint32\_t pool\_pause\_thold
    :   the pause threshold of pool, the unit is byte

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t10pa_ctrl_enE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t10pa_ctrl_enE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t10pa_ctrl_enE"></a> <a id="onboard_speaker_stream_cfg_t::pa_ctrl_en__b"></a> <a id="structonboard__speaker__stream__cfg__t_1a790e72d95bef2a209ae926418b1bccce"></a> bool pa\_ctrl\_en
    :   control pa enable

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t12pa_ctrl_gpioE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t12pa_ctrl_gpioE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t12pa_ctrl_gpioE"></a> <a id="onboard_speaker_stream_cfg_t::pa_ctrl_gpio__uint16_t"></a> <a id="structonboard__speaker__stream__cfg__t_1a33041dd04e97c857bf986e3c251cc834"></a> uint16\_t pa\_ctrl\_gpio
    :   the gpio id of control pa

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t11pa_on_levelE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t11pa_on_levelE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t11pa_on_levelE"></a> <a id="onboard_speaker_stream_cfg_t::pa_on_level__uint8_t"></a> <a id="structonboard__speaker__stream__cfg__t_1af18f8dacb10b9d86226780265e979ee9"></a> uint8\_t pa\_on\_level
    :   the gpio level of turn on pa, 0: low level, 1: high level

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t11pa_on_delayE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t11pa_on_delayE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t11pa_on_delayE"></a> <a id="onboard_speaker_stream_cfg_t::pa_on_delay__uint32_t"></a> <a id="structonboard__speaker__stream__cfg__t_1a942473260735aaf98facebe7da3a614f"></a> uint32\_t pa\_on\_delay
    :   the delay time(ms) of turn on pa after enable audio dac. \[dac init -\> delay -\> pa turn on\]

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t12pa_off_delayE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t12pa_off_delayE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t12pa_off_delayE"></a> <a id="onboard_speaker_stream_cfg_t::pa_off_delay__uint32_t"></a> <a id="structonboard__speaker__stream__cfg__t_1a06aa7f90906c6959010d31a5a39ad3e1"></a> uint32\_t pa\_off\_delay
    :   the delay time(ms) of disable audio dac after turn off pa. \[mute -\> pa turn off -\> delay -\> dac deinit\]

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t10task_stackE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t10task_stackE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t10task_stackE"></a> <a id="onboard_speaker_stream_cfg_t::task_stack__i"></a> <a id="structonboard__speaker__stream__cfg__t_1a8d716857fa534110dc0390603f4cc290"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t9task_coreE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t9task_coreE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t9task_coreE"></a> <a id="onboard_speaker_stream_cfg_t::task_core__i"></a> <a id="structonboard__speaker__stream__cfg__t_1ac0178c670adf7dc2d832cc0e3329a241"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N28onboard_speaker_stream_cfg_t9task_prioE"></a>

    <a id="_CPPv3N28onboard_speaker_stream_cfg_t9task_prioE"></a> <a id="_CPPv2N28onboard_speaker_stream_cfg_t9task_prioE"></a> <a id="onboard_speaker_stream_cfg_t::task_prio__i"></a> <a id="structonboard__speaker__stream__cfg__t_1a45f6abc710a89e6444ca8606d2bd8e3e"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.ONBOARD_SPEAKER_STREAM_TASK_STACK"></a>

<a id="onboard__speaker__stream_8h_1aef211acb4db9ad867492cf634f6e290b"></a> ONBOARD\_SPEAKER\_STREAM\_TASK\_STACK

<a id="c.ONBOARD_SPEAKER_STREAM_TASK_CORE"></a>

<a id="onboard__speaker__stream_8h_1ad0693e13105947f655ab8b63269c7053"></a> ONBOARD\_SPEAKER\_STREAM\_TASK\_CORE

<a id="c.ONBOARD_SPEAKER_STREAM_TASK_PRIO"></a>

<a id="onboard__speaker__stream_8h_1a076c71952016b5f59cd37db6b48fd45e"></a> ONBOARD\_SPEAKER\_STREAM\_TASK\_PRIO

<a id="c.ONBOARD_SPEAKER_STREAM_CFG_DEFAULT"></a>

<a id="onboard__speaker__stream_8h_1ae65c36d0fbeaacde0d598c0030454323"></a> ONBOARD\_SPEAKER\_STREAM\_CFG\_DEFAULT()

<a id="c.DEFAULT_ONBOARD_SPEAKER_STREAM_CONFIG"></a>

<a id="onboard__speaker__stream_8h_1a1442c9d8d345624feb0aa5f489d36e18"></a> DEFAULT\_ONBOARD\_SPEAKER\_STREAM\_CONFIG()
