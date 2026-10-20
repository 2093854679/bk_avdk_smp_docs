---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/audio_development_kit/audio_streams/onboard_mic_stream.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="onboard-mic-stream"></a>

# Onboard MIC Stream

The onboard mic stream reads audio data from onboard mic.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [onboard\_mic\_stream.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_audio/audio_streams/onboard_mic_stream.h)

<a id="functions"></a>

### Functions

<a id="_CPPv423onboard_mic_stream_initP24onboard_mic_stream_cfg_t"></a>

<a id="_CPPv323onboard_mic_stream_initP24onboard_mic_stream_cfg_t"></a> <a id="_CPPv223onboard_mic_stream_initP24onboard_mic_stream_cfg_t"></a> <a id="onboard_mic_stream_init__onboard_mic_stream_cfg_tP"></a> <a id="onboard__mic__stream_8h_1aefeaff005e6211ac5f5decb5e7969730"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_mic\_stream\_init([onboard\_mic\_stream\_cfg\_t](#_CPPv424onboard_mic_stream_cfg_t "onboard_mic_stream_cfg_t") \*config)
:   Create a handle to an Audio Element to stream data to another Element.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The Audio Element handle

        - Not NULL: success
        - NULL: failed

<a id="_CPPv435onboard_mic_stream_set_digital_gain22audio_element_handle_t7uint8_t"></a>

<a id="_CPPv335onboard_mic_stream_set_digital_gain22audio_element_handle_t7uint8_t"></a> <a id="_CPPv235onboard_mic_stream_set_digital_gain22audio_element_handle_t7uint8_t"></a> <a id="onboard_mic_stream_set_digital_gain__audio_element_handle_t.uint8_t"></a> <a id="onboard__mic__stream_8h_1ae2479ec88e13b4e3e4ec76abb8e601b9"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_mic\_stream\_set\_digital\_gain([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_mic\_stream, uint8\_t gain)
:   Updata onboard mic stream digital gain.

    参数
    :   - **onboard\_mic\_stream** – **\[in\]** element handle
        - **gain** – **\[in\]** mic digital gain, range: 0x00 \~ 0x3f(-45db \~ 18db, 0x2d: 0db)

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="_CPPv435onboard_mic_stream_get_digital_gain22audio_element_handle_tP7uint8_t"></a>

<a id="_CPPv335onboard_mic_stream_get_digital_gain22audio_element_handle_tP7uint8_t"></a> <a id="_CPPv235onboard_mic_stream_get_digital_gain22audio_element_handle_tP7uint8_t"></a> <a id="onboard_mic_stream_get_digital_gain__audio_element_handle_t.uint8_tP"></a> <a id="onboard__mic__stream_8h_1a65c08d32d1d9e4756b9c0bcd2734ed2e"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_mic\_stream\_get\_digital\_gain([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_mic\_stream, uint8\_t \*gain)
:   Get onboard mic stream digital gain.

    参数
    :   - **onboard\_mic\_stream** – **\[in\]** element handle
        - **gain** – **\[inout\]** mic digital gain

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="_CPPv434onboard_mic_stream_set_analog_gain22audio_element_handle_t7uint8_t"></a>

<a id="_CPPv334onboard_mic_stream_set_analog_gain22audio_element_handle_t7uint8_t"></a> <a id="_CPPv234onboard_mic_stream_set_analog_gain22audio_element_handle_t7uint8_t"></a> <a id="onboard_mic_stream_set_analog_gain__audio_element_handle_t.uint8_t"></a> <a id="onboard__mic__stream_8h_1a3c15f390b1b65fb833428cfa2220ba4d"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_mic\_stream\_set\_analog\_gain([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_mic\_stream, uint8\_t gain)
:   Update onboard mic stream analog gain.

    参数
    :   - **onboard\_mic\_stream** – **\[in\]** element handle
        - **gain** – **\[in\]** mic analog gain, range: 0x00 \~ 0x3f

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="_CPPv434onboard_mic_stream_get_analog_gain22audio_element_handle_tP7uint8_t"></a>

<a id="_CPPv334onboard_mic_stream_get_analog_gain22audio_element_handle_tP7uint8_t"></a> <a id="_CPPv234onboard_mic_stream_get_analog_gain22audio_element_handle_tP7uint8_t"></a> <a id="onboard_mic_stream_get_analog_gain__audio_element_handle_t.uint8_tP"></a> <a id="onboard__mic__stream_8h_1ad606a64cc13408adccabdaeff70c747f"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") onboard\_mic\_stream\_get\_analog\_gain([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") onboard\_mic\_stream, uint8\_t \*gain)
:   Get onboard mic stream analog gain.

    参数
    :   - **onboard\_mic\_stream** – **\[in\]** element handle
        - **gain** – **\[inout\]** mic analog gain

    返回
    :   Result

        - BK\_OK: success
        - other: failed

<a id="structures"></a>

### Structures

<a id="_CPPv49adc_cfg_t"></a>

<a id="_CPPv39adc_cfg_t"></a> <a id="_CPPv29adc_cfg_t"></a> <a id="adc_cfg_t"></a> <a id="structadc__cfg__t"></a> struct adc\_cfg\_t
:   ADC mode configurations, if any entry is zero then the configuration will be set to default values.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N9adc_cfg_t7chl_numE"></a>

    <a id="_CPPv3N9adc_cfg_t7chl_numE"></a> <a id="_CPPv2N9adc_cfg_t7chl_numE"></a> <a id="adc_cfg_t::chl_num__uint8_t"></a> <a id="structadc__cfg__t_1a3f0561d534a37702c924c3d1ed05a52c"></a> uint8\_t chl\_num
    :   mic channel number

    <a id="_CPPv4N9adc_cfg_t4bitsE"></a>

    <a id="_CPPv3N9adc_cfg_t4bitsE"></a> <a id="_CPPv2N9adc_cfg_t4bitsE"></a> <a id="adc_cfg_t::bits__uint8_t"></a> <a id="structadc__cfg__t_1ae4db6825eaf32f049c8504f8b35cb147"></a> uint8\_t bits
    :   Bit wide (16 or 24 bits)

    <a id="_CPPv4N9adc_cfg_t11sample_rateE"></a>

    <a id="_CPPv3N9adc_cfg_t11sample_rateE"></a> <a id="_CPPv2N9adc_cfg_t11sample_rateE"></a> <a id="adc_cfg_t::sample_rate__uint32_t"></a> <a id="structadc__cfg__t_1aa06f47f8052ff634230eaf8cf91ede65"></a> uint32\_t sample\_rate
    :   mic sample rate

    <a id="_CPPv4N9adc_cfg_t8dig_gainE"></a>

    <a id="_CPPv3N9adc_cfg_t8dig_gainE"></a> <a id="_CPPv2N9adc_cfg_t8dig_gainE"></a> <a id="adc_cfg_t::dig_gain__int32_t"></a> <a id="structadc__cfg__t_1ac87de8b4a64a370954633112282d6f5e"></a> int32\_t dig\_gain
    :   audio adc digital gain: value range: 0x00 \~ 0x3f(-45db \~ 18db, 0x2d: 0db), suggest: 0x2d

    <a id="_CPPv4N9adc_cfg_t8ana_gainE"></a>

    <a id="_CPPv3N9adc_cfg_t8ana_gainE"></a> <a id="_CPPv2N9adc_cfg_t8ana_gainE"></a> <a id="adc_cfg_t::ana_gain__int32_t"></a> <a id="structadc__cfg__t_1a4e298981e10ebb5ba360065b6300a4b3"></a> int32\_t ana\_gain
    :   audio adc analog gain: value range: , suggest:

    <a id="_CPPv4N9adc_cfg_t4modeE"></a>

    <a id="_CPPv3N9adc_cfg_t4modeE"></a> <a id="_CPPv2N9adc_cfg_t4modeE"></a> <a id="adc_cfg_t::mode__aud_adc_mode_t"></a> <a id="structadc__cfg__t_1a74fe0d1eb7cfc35711a628e22fe14154"></a> aud\_adc\_mode\_t mode
    :   mic interface mode: signal\_ended/differen

    <a id="_CPPv4N9adc_cfg_t7clk_srcE"></a>

    <a id="_CPPv3N9adc_cfg_t7clk_srcE"></a> <a id="_CPPv2N9adc_cfg_t7clk_srcE"></a> <a id="adc_cfg_t::clk_src__aud_clk_t"></a> <a id="structadc__cfg__t_1a00ec810419de39ac1dd18504ae565a79"></a> aud\_clk\_t clk\_src
    :   audio clock: XTAL(26MHz)/APLL

<a id="_CPPv424onboard_mic_stream_cfg_t"></a>

<a id="_CPPv324onboard_mic_stream_cfg_t"></a> <a id="_CPPv224onboard_mic_stream_cfg_t"></a> <a id="onboard_mic_stream_cfg_t"></a> <a id="structonboard__mic__stream__cfg__t"></a> struct onboard\_mic\_stream\_cfg\_t
:   Onboard MIC Stream configurations, if any entry is zero then the configuration will be set to default values.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N24onboard_mic_stream_cfg_t7adc_cfgE"></a>

    <a id="_CPPv3N24onboard_mic_stream_cfg_t7adc_cfgE"></a> <a id="_CPPv2N24onboard_mic_stream_cfg_t7adc_cfgE"></a> <a id="onboard_mic_stream_cfg_t::adc_cfg__adc_cfg_t"></a> <a id="structonboard__mic__stream__cfg__t_1a957141cde208abdea1cf20242d2bca6b"></a> [adc\_cfg\_t](#_CPPv49adc_cfg_t "adc_cfg_t") adc\_cfg
    :   ADC mode configuration

    <a id="_CPPv4N24onboard_mic_stream_cfg_t10frame_sizeE"></a>

    <a id="_CPPv3N24onboard_mic_stream_cfg_t10frame_sizeE"></a> <a id="_CPPv2N24onboard_mic_stream_cfg_t10frame_sizeE"></a> <a id="onboard_mic_stream_cfg_t::frame_size__uint32_t"></a> <a id="structonboard__mic__stream__cfg__t_1a1339105f3f36ed3454a6e35718e96751"></a> uint32\_t frame\_size
    :   the length of one frame (bytes)

    <a id="_CPPv4N24onboard_mic_stream_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N24onboard_mic_stream_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N24onboard_mic_stream_cfg_t14out_block_sizeE"></a> <a id="onboard_mic_stream_cfg_t::out_block_size__i"></a> <a id="structonboard__mic__stream__cfg__t_1a360cb97f4f19b850cbf0173c7743e6b2"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N24onboard_mic_stream_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N24onboard_mic_stream_cfg_t13out_block_numE"></a> <a id="_CPPv2N24onboard_mic_stream_cfg_t13out_block_numE"></a> <a id="onboard_mic_stream_cfg_t::out_block_num__i"></a> <a id="structonboard__mic__stream__cfg__t_1a6f54602ffd2ebb2e9df0d7d518b6b624"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N24onboard_mic_stream_cfg_t18multi_out_port_numE"></a>

    <a id="_CPPv3N24onboard_mic_stream_cfg_t18multi_out_port_numE"></a> <a id="_CPPv2N24onboard_mic_stream_cfg_t18multi_out_port_numE"></a> <a id="onboard_mic_stream_cfg_t::multi_out_port_num__i"></a> <a id="structonboard__mic__stream__cfg__t_1a303edd29977e4797d2f62e8b8bd55654"></a> int multi\_out\_port\_num
    :   The number of multiple output audio port

    <a id="_CPPv4N24onboard_mic_stream_cfg_t10task_stackE"></a>

    <a id="_CPPv3N24onboard_mic_stream_cfg_t10task_stackE"></a> <a id="_CPPv2N24onboard_mic_stream_cfg_t10task_stackE"></a> <a id="onboard_mic_stream_cfg_t::task_stack__i"></a> <a id="structonboard__mic__stream__cfg__t_1afc518993275d283068770621c38c0eda"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N24onboard_mic_stream_cfg_t9task_coreE"></a>

    <a id="_CPPv3N24onboard_mic_stream_cfg_t9task_coreE"></a> <a id="_CPPv2N24onboard_mic_stream_cfg_t9task_coreE"></a> <a id="onboard_mic_stream_cfg_t::task_core__i"></a> <a id="structonboard__mic__stream__cfg__t_1ae411f97ee61680496ed6aa5b11c446c9"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N24onboard_mic_stream_cfg_t9task_prioE"></a>

    <a id="_CPPv3N24onboard_mic_stream_cfg_t9task_prioE"></a> <a id="_CPPv2N24onboard_mic_stream_cfg_t9task_prioE"></a> <a id="onboard_mic_stream_cfg_t::task_prio__i"></a> <a id="structonboard__mic__stream__cfg__t_1a9702ed64648c33e332b5f1169586b179"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.ONBOARD_MIC_STREAM_TASK_STACK"></a>

<a id="onboard__mic__stream_8h_1a4502a057cc4fbc38a597229a8de78e43"></a> ONBOARD\_MIC\_STREAM\_TASK\_STACK

<a id="c.ONBOARD_MIC_STREAM_TASK_CORE"></a>

<a id="onboard__mic__stream_8h_1a6e31c104afc069dea88b7650caf08e79"></a> ONBOARD\_MIC\_STREAM\_TASK\_CORE

<a id="c.ONBOARD_MIC_STREAM_TASK_PRIO"></a>

<a id="onboard__mic__stream_8h_1ad62528c659f919ba4e6c8f9c09bbfb8d"></a> ONBOARD\_MIC\_STREAM\_TASK\_PRIO

<a id="c.ONBOARD_MIC_ADC_STREAM_CFG_DEFAULT"></a>

<a id="onboard__mic__stream_8h_1a428f72543a2e1db27b205594b6e6c4e5"></a> ONBOARD\_MIC\_ADC\_STREAM\_CFG\_DEFAULT()

<a id="c.DEFAULT_ONBOARD_MIC_ADC_STREAM_CONFIG"></a>

<a id="onboard__mic__stream_8h_1a7abeabfc8617ee405acb69a92492aec1"></a> DEFAULT\_ONBOARD\_MIC\_ADC\_STREAM\_CONFIG()
