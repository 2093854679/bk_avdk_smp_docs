---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/audio_development_kit/audio_streams/uac_speaker_stream.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="uac-speaker-stream"></a>

# UAC Speaker Stream

The UAC speaker stream writes audio data to UAC speaker.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [uac\_speaker\_stream.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_audio/audio_streams/uac_speaker_stream.h)

<a id="functions"></a>

### Functions

<a id="_CPPv423uac_speaker_stream_initP24uac_speaker_stream_cfg_t"></a>

<a id="_CPPv323uac_speaker_stream_initP24uac_speaker_stream_cfg_t"></a> <a id="_CPPv223uac_speaker_stream_initP24uac_speaker_stream_cfg_t"></a> <a id="uac_speaker_stream_init__uac_speaker_stream_cfg_tP"></a> <a id="uac__speaker__stream_8h_1a34c4f1ce35d11d19a11078a9d9ceeca2"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") uac\_speaker\_stream\_init([uac\_speaker\_stream\_cfg\_t](#_CPPv424uac_speaker_stream_cfg_t "uac_speaker_stream_cfg_t") \*config)
:   Create a handle to an Audio Element to stream data to another Element.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The Audio Element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv424uac_speaker_stream_cfg_t"></a>

<a id="_CPPv324uac_speaker_stream_cfg_t"></a> <a id="_CPPv224uac_speaker_stream_cfg_t"></a> <a id="uac_speaker_stream_cfg_t"></a> <a id="structuac__speaker__stream__cfg__t"></a> struct uac\_speaker\_stream\_cfg\_t
:   UAC Speaker Stream configurations, if any entry is zero then the configuration will be set to default values.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N24uac_speaker_stream_cfg_t10port_indexE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t10port_indexE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t10port_indexE"></a> <a id="uac_speaker_stream_cfg_t::port_index__E_USB_HUB_PORT_INDEX"></a> <a id="structuac__speaker__stream__cfg__t_1a549959b5083ffefa70f935d25dcca719"></a> [E\_USB\_HUB\_PORT\_INDEX](../../../peripheral/bk_usb.md#_CPPv420E_USB_HUB_PORT_INDEX "E_USB_HUB_PORT_INDEX") port\_index
    :   usb hub port index

    <a id="_CPPv4N24uac_speaker_stream_cfg_t6formatE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t6formatE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t6formatE"></a> <a id="uac_speaker_stream_cfg_t::format__uint16_t"></a> <a id="structuac__speaker__stream__cfg__t_1a8e9e04224c26c8a73688de0c21c5c679"></a> uint16\_t format
    :   uac speaker data format

    <a id="_CPPv4N24uac_speaker_stream_cfg_t7chl_numE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t7chl_numE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t7chl_numE"></a> <a id="uac_speaker_stream_cfg_t::chl_num__uint8_t"></a> <a id="structuac__speaker__stream__cfg__t_1a8b1879b678e194e2746bb27034a2312b"></a> uint8\_t chl\_num
    :   speaker channel number

    <a id="_CPPv4N24uac_speaker_stream_cfg_t4bitsE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t4bitsE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t4bitsE"></a> <a id="uac_speaker_stream_cfg_t::bits__uint8_t"></a> <a id="structuac__speaker__stream__cfg__t_1acfa9f471f6fc93675dda7845cb84bfaf"></a> uint8\_t bits
    :   Bit wide (8, 16 bits)

    <a id="_CPPv4N24uac_speaker_stream_cfg_t9samp_rateE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t9samp_rateE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t9samp_rateE"></a> <a id="uac_speaker_stream_cfg_t::samp_rate__uint32_t"></a> <a id="structuac__speaker__stream__cfg__t_1a55eed160b8332ee22189a87e9c0f5048"></a> uint32\_t samp\_rate
    :   speaker sample rate

    <a id="_CPPv4N24uac_speaker_stream_cfg_t10frame_sizeE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t10frame_sizeE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t10frame_sizeE"></a> <a id="uac_speaker_stream_cfg_t::frame_size__uint32_t"></a> <a id="structuac__speaker__stream__cfg__t_1a8dcc5bdb69b79ffa19fa04e4c85e28f9"></a> uint32\_t frame\_size
    :   size of one frame speaker data

    <a id="_CPPv4N24uac_speaker_stream_cfg_t6volumeE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t6volumeE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t6volumeE"></a> <a id="uac_speaker_stream_cfg_t::volume__uint32_t"></a> <a id="structuac__speaker__stream__cfg__t_1acdfd45319b552fb5e6d44b5792f08036"></a> uint32\_t volume
    :   speaker dac gain

    <a id="_CPPv4N24uac_speaker_stream_cfg_t12auto_connectE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t12auto_connectE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t12auto_connectE"></a> <a id="uac_speaker_stream_cfg_t::auto_connect__b"></a> <a id="structuac__speaker__stream__cfg__t_1a289ad547bc0b2667bf24feab57ce2210"></a> bool auto\_connect
    :   Automatic connect enable

    <a id="_CPPv4N24uac_speaker_stream_cfg_t18multi_out_port_numE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t18multi_out_port_numE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t18multi_out_port_numE"></a> <a id="uac_speaker_stream_cfg_t::multi_out_port_num__i"></a> <a id="structuac__speaker__stream__cfg__t_1ab05b3e1ebce2752e2f5aff01e1acc827"></a> int multi\_out\_port\_num
    :   The number of multiple output audio port

    <a id="_CPPv4N24uac_speaker_stream_cfg_t9pool_sizeE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t9pool_sizeE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t9pool_sizeE"></a> <a id="uac_speaker_stream_cfg_t::pool_size__uint32_t"></a> <a id="structuac__speaker__stream__cfg__t_1af6b70af78de95b4550d116b9f27e77bb"></a> uint32\_t pool\_size
    :   speaker data pool size, the unit is byte

    <a id="_CPPv4N24uac_speaker_stream_cfg_t15pool_play_tholdE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t15pool_play_tholdE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t15pool_play_tholdE"></a> <a id="uac_speaker_stream_cfg_t::pool_play_thold__uint32_t"></a> <a id="structuac__speaker__stream__cfg__t_1a803bbff57b6c8e1fc8cc8d15c6abcab2"></a> uint32\_t pool\_play\_thold
    :   the play threshold of pool, the unit is byte

    <a id="_CPPv4N24uac_speaker_stream_cfg_t16pool_pause_tholdE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t16pool_pause_tholdE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t16pool_pause_tholdE"></a> <a id="uac_speaker_stream_cfg_t::pool_pause_thold__uint32_t"></a> <a id="structuac__speaker__stream__cfg__t_1a7cc3a359bdc5f19d6dc24aecca61c102"></a> uint32\_t pool\_pause\_thold
    :   the pause threshold of pool, the unit is byte

    <a id="_CPPv4N24uac_speaker_stream_cfg_t10task_stackE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t10task_stackE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t10task_stackE"></a> <a id="uac_speaker_stream_cfg_t::task_stack__i"></a> <a id="structuac__speaker__stream__cfg__t_1abf1e6486a85ed2bceebca39caa2b11ea"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N24uac_speaker_stream_cfg_t9task_coreE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t9task_coreE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t9task_coreE"></a> <a id="uac_speaker_stream_cfg_t::task_core__i"></a> <a id="structuac__speaker__stream__cfg__t_1aec8b31747d7a8f6038787f0c5993740e"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N24uac_speaker_stream_cfg_t9task_prioE"></a>

    <a id="_CPPv3N24uac_speaker_stream_cfg_t9task_prioE"></a> <a id="_CPPv2N24uac_speaker_stream_cfg_t9task_prioE"></a> <a id="uac_speaker_stream_cfg_t::task_prio__i"></a> <a id="structuac__speaker__stream__cfg__t_1a630545f125f317e075e1af4d5ab61c48"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.UAC_SPEAKER_STREAM_TASK_STACK"></a>

<a id="uac__speaker__stream_8h_1a36b1d6fec4eb7ad9e11d5d361f976bfc"></a> UAC\_SPEAKER\_STREAM\_TASK\_STACK

<a id="c.UAC_SPEAKER_STREAM_TASK_CORE"></a>

<a id="uac__speaker__stream_8h_1aba97c50ecb6f26eab7300d229ff86d02"></a> UAC\_SPEAKER\_STREAM\_TASK\_CORE

<a id="c.UAC_SPEAKER_STREAM_TASK_PRIO"></a>

<a id="uac__speaker__stream_8h_1a3e613119447e06dfe18c69e40d49bc96"></a> UAC\_SPEAKER\_STREAM\_TASK\_PRIO

<a id="c.UAC_SPEAKER_STREAM_CFG_DEFAULT"></a>

<a id="uac__speaker__stream_8h_1a8993972df25677cd23f5b039d9b39565"></a> UAC\_SPEAKER\_STREAM\_CFG\_DEFAULT()

<a id="c.DEFAULT_UAC_SPEAKER_STREAM_CONFIG"></a>

<a id="uac__speaker__stream_8h_1ad9b2617ef6f43edbde43e43841af9542"></a> DEFAULT\_UAC\_SPEAKER\_STREAM\_CONFIG()
