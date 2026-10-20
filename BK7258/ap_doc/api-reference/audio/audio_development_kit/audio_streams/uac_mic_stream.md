---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_streams/uac_mic_stream.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="uac-mic-stream"></a>

# UAC Mic Stream

The UAC MIC stream reads audio data from UAC mic.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [uac\_mic\_stream.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_streams/uac_mic_stream.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419uac_mic_stream_initP20uac_mic_stream_cfg_t"></a>

<a id="_CPPv319uac_mic_stream_initP20uac_mic_stream_cfg_t"></a> <a id="_CPPv219uac_mic_stream_initP20uac_mic_stream_cfg_t"></a> <a id="uac_mic_stream_init__uac_mic_stream_cfg_tP"></a> <a id="uac__mic__stream_8h_1ae6294bca1c1c6dbf8af575d787875a5f"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") uac\_mic\_stream\_init([uac\_mic\_stream\_cfg\_t](#_CPPv420uac_mic_stream_cfg_t "uac_mic_stream_cfg_t") \*config)
:   Create a handle to an Audio Element to stream data to another Element.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The Audio Element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv420uac_mic_stream_cfg_t"></a>

<a id="_CPPv320uac_mic_stream_cfg_t"></a> <a id="_CPPv220uac_mic_stream_cfg_t"></a> <a id="uac_mic_stream_cfg_t"></a> <a id="structuac__mic__stream__cfg__t"></a> struct uac\_mic\_stream\_cfg\_t
:   UAC MIC Stream configurations, if any entry is zero then the configuration will be set to default values.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20uac_mic_stream_cfg_t10port_indexE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t10port_indexE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t10port_indexE"></a> <a id="uac_mic_stream_cfg_t::port_index__E_USB_HUB_PORT_INDEX"></a> <a id="structuac__mic__stream__cfg__t_1ace0dc693ceee1d1992e70236e8b91d7c"></a> [E\_USB\_HUB\_PORT\_INDEX](../../../peripheral/bk_usb.md#_CPPv420E_USB_HUB_PORT_INDEX "E_USB_HUB_PORT_INDEX") port\_index
    :   usb hub port index

    <a id="_CPPv4N20uac_mic_stream_cfg_t6formatE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t6formatE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t6formatE"></a> <a id="uac_mic_stream_cfg_t::format__uint16_t"></a> <a id="structuac__mic__stream__cfg__t_1a8061713ad7ed21490735285118badd2b"></a> uint16\_t format
    :   uac mic data format

    <a id="_CPPv4N20uac_mic_stream_cfg_t7chl_numE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t7chl_numE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t7chl_numE"></a> <a id="uac_mic_stream_cfg_t::chl_num__uint8_t"></a> <a id="structuac__mic__stream__cfg__t_1ae15bc0c5d925e22626c8f8946b98a9f0"></a> uint8\_t chl\_num
    :   mic channel number

    <a id="_CPPv4N20uac_mic_stream_cfg_t4bitsE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t4bitsE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t4bitsE"></a> <a id="uac_mic_stream_cfg_t::bits__uint8_t"></a> <a id="structuac__mic__stream__cfg__t_1a1c0dfd34bbd1e0ed85608e2ff11eb535"></a> uint8\_t bits
    :   Bit wide (8, 16 bits)

    <a id="_CPPv4N20uac_mic_stream_cfg_t9samp_rateE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t9samp_rateE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t9samp_rateE"></a> <a id="uac_mic_stream_cfg_t::samp_rate__uint32_t"></a> <a id="structuac__mic__stream__cfg__t_1a7e51290e6df6cbab9ad86c28fb5e2650"></a> uint32\_t samp\_rate
    :   mic sample rate

    <a id="_CPPv4N20uac_mic_stream_cfg_t10frame_sizeE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t10frame_sizeE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t10frame_sizeE"></a> <a id="uac_mic_stream_cfg_t::frame_size__uint32_t"></a> <a id="structuac__mic__stream__cfg__t_1af5438c4fcbef01549f2c6a3762f7abe4"></a> uint32\_t frame\_size
    :   size of one frame mic data

    <a id="_CPPv4N20uac_mic_stream_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t14out_block_sizeE"></a> <a id="uac_mic_stream_cfg_t::out_block_size__i"></a> <a id="structuac__mic__stream__cfg__t_1ab4b54ce7f3886a2008e85e757e760b3a"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N20uac_mic_stream_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t13out_block_numE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t13out_block_numE"></a> <a id="uac_mic_stream_cfg_t::out_block_num__i"></a> <a id="structuac__mic__stream__cfg__t_1a361e3d33d5cff0071120e823124cbad8"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N20uac_mic_stream_cfg_t12auto_connectE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t12auto_connectE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t12auto_connectE"></a> <a id="uac_mic_stream_cfg_t::auto_connect__b"></a> <a id="structuac__mic__stream__cfg__t_1aea565bdf905c0b62da483d5afd9179c9"></a> bool auto\_connect
    :   Automatic connect enable

    <a id="_CPPv4N20uac_mic_stream_cfg_t18multi_out_port_numE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t18multi_out_port_numE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t18multi_out_port_numE"></a> <a id="uac_mic_stream_cfg_t::multi_out_port_num__i"></a> <a id="structuac__mic__stream__cfg__t_1a389a08794549c6ad296941a9b90879da"></a> int multi\_out\_port\_num
    :   The number of multiple output audio port

    <a id="_CPPv4N20uac_mic_stream_cfg_t10task_stackE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t10task_stackE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t10task_stackE"></a> <a id="uac_mic_stream_cfg_t::task_stack__i"></a> <a id="structuac__mic__stream__cfg__t_1a20633edf55b87c5029fdb465c5ad26a3"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N20uac_mic_stream_cfg_t9task_coreE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t9task_coreE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t9task_coreE"></a> <a id="uac_mic_stream_cfg_t::task_core__i"></a> <a id="structuac__mic__stream__cfg__t_1a18b3ea183689013e2d9dcfcc2e9e4b1b"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N20uac_mic_stream_cfg_t9task_prioE"></a>

    <a id="_CPPv3N20uac_mic_stream_cfg_t9task_prioE"></a> <a id="_CPPv2N20uac_mic_stream_cfg_t9task_prioE"></a> <a id="uac_mic_stream_cfg_t::task_prio__i"></a> <a id="structuac__mic__stream__cfg__t_1acc719b31e3639c6645990df516dcb7a6"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.UAC_MIC_STREAM_TASK_STACK"></a>

<a id="uac__mic__stream_8h_1a32c010ab29cd69a0a2ae0929d7b27749"></a> UAC\_MIC\_STREAM\_TASK\_STACK

<a id="c.UAC_MIC_STREAM_TASK_CORE"></a>

<a id="uac__mic__stream_8h_1a0f8632eb233591a3273b909638438f9c"></a> UAC\_MIC\_STREAM\_TASK\_CORE

<a id="c.UAC_MIC_STREAM_TASK_PRIO"></a>

<a id="uac__mic__stream_8h_1af42c8465cc6f0bcb47d43d558da6ff32"></a> UAC\_MIC\_STREAM\_TASK\_PRIO

<a id="c.UAC_MIC_STREAM_CFG_DEFAULT"></a>

<a id="uac__mic__stream_8h_1af43b655b87f21dc3ed7bb8728ec8be82"></a> UAC\_MIC\_STREAM\_CFG\_DEFAULT()

<a id="c.DEFAULT_UAC_MIC_STREAM_CONFIG"></a>

<a id="uac__mic__stream_8h_1ae95bc2d4f3685b6b9d75ec3c93744daf"></a> DEFAULT\_UAC\_MIC\_STREAM\_CONFIG()
