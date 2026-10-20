---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_decoders/g722_decoder.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="g722-decoder"></a>

# G722 Decoder

Decode an audio data stream provided in G722 format.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [g722\_decoder.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_decoders/g722_decoder.h)

<a id="functions"></a>

### Functions

<a id="_CPPv417g722_decoder_initP18g722_decoder_cfg_t"></a>

<a id="_CPPv317g722_decoder_initP18g722_decoder_cfg_t"></a> <a id="_CPPv217g722_decoder_initP18g722_decoder_cfg_t"></a> <a id="g722_decoder_init__g722_decoder_cfg_tP"></a> <a id="g722__decoder_8h_1affc36d3e6fb7688c61895d0a96bbf32d"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") g722\_decoder\_init([g722\_decoder\_cfg\_t](#_CPPv418g722_decoder_cfg_t "g722_decoder_cfg_t") \*config)
:   Create a G722 decoder of Audio Element to decode incoming data using G722 format.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The audio element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv418g722_decoder_cfg_t"></a>

<a id="_CPPv318g722_decoder_cfg_t"></a> <a id="_CPPv218g722_decoder_cfg_t"></a> <a id="g722_decoder_cfg_t"></a> <a id="structg722__decoder__cfg__t"></a> struct g722\_decoder\_cfg\_t
:   G722 Decoder configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18g722_decoder_cfg_t6buf_szE"></a>

    <a id="_CPPv3N18g722_decoder_cfg_t6buf_szE"></a> <a id="_CPPv2N18g722_decoder_cfg_t6buf_szE"></a> <a id="g722_decoder_cfg_t::buf_sz__i"></a> <a id="structg722__decoder__cfg__t_1a5eaedc50d54cefc424d3c2672dae4c24"></a> int buf\_sz
    :   Element Buffer size

    <a id="_CPPv4N18g722_decoder_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N18g722_decoder_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N18g722_decoder_cfg_t14out_block_sizeE"></a> <a id="g722_decoder_cfg_t::out_block_size__i"></a> <a id="structg722__decoder__cfg__t_1ae7ba968e8552db4a565782d9d358005a"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N18g722_decoder_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N18g722_decoder_cfg_t13out_block_numE"></a> <a id="_CPPv2N18g722_decoder_cfg_t13out_block_numE"></a> <a id="g722_decoder_cfg_t::out_block_num__i"></a> <a id="structg722__decoder__cfg__t_1a882e27e0be9d33fc24745475bb9f7076"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N18g722_decoder_cfg_t10task_stackE"></a>

    <a id="_CPPv3N18g722_decoder_cfg_t10task_stackE"></a> <a id="_CPPv2N18g722_decoder_cfg_t10task_stackE"></a> <a id="g722_decoder_cfg_t::task_stack__i"></a> <a id="structg722__decoder__cfg__t_1a93a00e1a7f5c81e0fb25e3377edff21f"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N18g722_decoder_cfg_t9task_coreE"></a>

    <a id="_CPPv3N18g722_decoder_cfg_t9task_coreE"></a> <a id="_CPPv2N18g722_decoder_cfg_t9task_coreE"></a> <a id="g722_decoder_cfg_t::task_core__i"></a> <a id="structg722__decoder__cfg__t_1a19489e0f39eb0bfecfa29790ae6e28c9"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N18g722_decoder_cfg_t9task_prioE"></a>

    <a id="_CPPv3N18g722_decoder_cfg_t9task_prioE"></a> <a id="_CPPv2N18g722_decoder_cfg_t9task_prioE"></a> <a id="g722_decoder_cfg_t::task_prio__i"></a> <a id="structg722__decoder__cfg__t_1ac032dce42ab2266b2d04d25f5b9f2783"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

    <a id="_CPPv4N18g722_decoder_cfg_t4rateE"></a>

    <a id="_CPPv3N18g722_decoder_cfg_t4rateE"></a> <a id="_CPPv2N18g722_decoder_cfg_t4rateE"></a> <a id="g722_decoder_cfg_t::rate__g722_decoder_rate_t"></a> <a id="structg722__decoder__cfg__t_1a9ddb057e027f1018bdb3eb857132f79e"></a> [g722\_decoder\_rate\_t](#_CPPv419g722_decoder_rate_t "g722_decoder_rate_t") rate
    :   Bit rate

    <a id="_CPPv4N18g722_decoder_cfg_t7optionsE"></a>

    <a id="_CPPv3N18g722_decoder_cfg_t7optionsE"></a> <a id="_CPPv2N18g722_decoder_cfg_t7optionsE"></a> <a id="g722_decoder_cfg_t::options__i"></a> <a id="structg722__decoder__cfg__t_1a637d97826c8ba4b153b2a31c92242021"></a> int options
    :   Decoder options

<a id="macros"></a>

### Macros

<a id="c.G722_DECODER_TASK_STACK"></a>

<a id="g722__decoder_8h_1acb5ebf79a80fe0d664926c7644570405"></a> G722\_DECODER\_TASK\_STACK

<a id="c.G722_DECODER_TASK_CORE"></a>

<a id="g722__decoder_8h_1a3a1242c48ef96d5700fe688f70f3380a"></a> G722\_DECODER\_TASK\_CORE

<a id="c.G722_DECODER_TASK_PRIO"></a>

<a id="g722__decoder_8h_1af47469d3f8c74ac80881de72e61201a7"></a> G722\_DECODER\_TASK\_PRIO

<a id="c.G722_DECODER_BUFFER_SIZE"></a>

<a id="g722__decoder_8h_1affb9a3287387fc67f7153e39e7bd00b5"></a> G722\_DECODER\_BUFFER\_SIZE

<a id="c.G722_DECODER_OUT_BLOCK_SIZE"></a>

<a id="g722__decoder_8h_1ac2eff82aab8ae015593cc04d5b7f9cfa"></a> G722\_DECODER\_OUT\_BLOCK\_SIZE

<a id="c.G722_DECODER_OUT_BLOCK_NUM"></a>

<a id="g722__decoder_8h_1a18a7d2425993fcec432f0aecfe6a8a6e"></a> G722\_DECODER\_OUT\_BLOCK\_NUM

<a id="c.DEFAULT_G722_DECODER_CONFIG"></a>

<a id="g722__decoder_8h_1a3700238d4d7adcceb3faca3bef8fd067"></a> DEFAULT\_G722\_DECODER\_CONFIG()

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv419g722_decoder_rate_t"></a>

<a id="_CPPv319g722_decoder_rate_t"></a> <a id="_CPPv219g722_decoder_rate_t"></a> <a id="g722__decoder_8h_1a2ec8846c496c28dd592331f07f6239ae"></a> enum g722\_decoder\_rate\_t
:   Enum of G722 Decoder rate.

    *Values:*

    <a id="_CPPv4N19g722_decoder_rate_t19G722_DEC_RATE_48000E"></a>

    <a id="_CPPv3N19g722_decoder_rate_t19G722_DEC_RATE_48000E"></a> <a id="_CPPv2N19g722_decoder_rate_t19G722_DEC_RATE_48000E"></a> <a id="g722__decoder_8h_1a2ec8846c496c28dd592331f07f6239aea448adfdb1996bc86d801cb822cb8c47c"></a> enumerator G722\_DEC\_RATE\_48000

    <a id="_CPPv4N19g722_decoder_rate_t19G722_DEC_RATE_56000E"></a>

    <a id="_CPPv3N19g722_decoder_rate_t19G722_DEC_RATE_56000E"></a> <a id="_CPPv2N19g722_decoder_rate_t19G722_DEC_RATE_56000E"></a> <a id="g722__decoder_8h_1a2ec8846c496c28dd592331f07f6239aeaa94be350fa8abf1e1f5b91b86bd79631"></a> enumerator G722\_DEC\_RATE\_56000

    <a id="_CPPv4N19g722_decoder_rate_t19G722_DEC_RATE_64000E"></a>

    <a id="_CPPv3N19g722_decoder_rate_t19G722_DEC_RATE_64000E"></a> <a id="_CPPv2N19g722_decoder_rate_t19G722_DEC_RATE_64000E"></a> <a id="g722__decoder_8h_1a2ec8846c496c28dd592331f07f6239aea08479cd0d8d944bd19fb9de77ed9bdaa"></a> enumerator G722\_DEC\_RATE\_64000

<a id="_CPPv421g722_decoder_option_t"></a>

<a id="_CPPv321g722_decoder_option_t"></a> <a id="_CPPv221g722_decoder_option_t"></a> <a id="g722__decoder_8h_1ab9eeb21f4fab3d4e73f35ee337f09d46"></a> enum g722\_decoder\_option\_t
:   Enum of G722 Decoder options.

    *Values:*

    <a id="_CPPv4N21g722_decoder_option_t20G722_DEC_OPTION_NONEE"></a>

    <a id="_CPPv3N21g722_decoder_option_t20G722_DEC_OPTION_NONEE"></a> <a id="_CPPv2N21g722_decoder_option_t20G722_DEC_OPTION_NONEE"></a> <a id="g722__decoder_8h_1ab9eeb21f4fab3d4e73f35ee337f09d46a924c9c5807a93f2782a13a53a260de54"></a> enumerator G722\_DEC\_OPTION\_NONE

    <a id="_CPPv4N21g722_decoder_option_t25G722_DEC_OPTION_8K_SAMPLEE"></a>

    <a id="_CPPv3N21g722_decoder_option_t25G722_DEC_OPTION_8K_SAMPLEE"></a> <a id="_CPPv2N21g722_decoder_option_t25G722_DEC_OPTION_8K_SAMPLEE"></a> <a id="g722__decoder_8h_1ab9eeb21f4fab3d4e73f35ee337f09d46a4a27915e42e5f737eae2955c563c3a9f"></a> enumerator G722\_DEC\_OPTION\_8K\_SAMPLE

    <a id="_CPPv4N21g722_decoder_option_t22G722_DEC_OPTION_PACKEDE"></a>

    <a id="_CPPv3N21g722_decoder_option_t22G722_DEC_OPTION_PACKEDE"></a> <a id="_CPPv2N21g722_decoder_option_t22G722_DEC_OPTION_PACKEDE"></a> <a id="g722__decoder_8h_1ab9eeb21f4fab3d4e73f35ee337f09d46a270e503e41b5350aefc7629f3860aadc"></a> enumerator G722\_DEC\_OPTION\_PACKED
