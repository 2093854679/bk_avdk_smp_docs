---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_decoders/aac_decoder.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="aac-decoder"></a>

# AAC Decoder

Decode an audio data stream provided in AAC format.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [aac\_decoder.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_decoders/aac_decoder.h)

<a id="functions"></a>

### Functions

<a id="_CPPv416aac_decoder_initP17aac_decoder_cfg_t"></a>

<a id="_CPPv316aac_decoder_initP17aac_decoder_cfg_t"></a> <a id="_CPPv216aac_decoder_initP17aac_decoder_cfg_t"></a> <a id="aac_decoder_init__aac_decoder_cfg_tP"></a> <a id="aac__decoder_8h_1a48ee07d8dc3cb84eea406c9ce36af98d"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") aac\_decoder\_init([aac\_decoder\_cfg\_t](#_CPPv417aac_decoder_cfg_t "aac_decoder_cfg_t") \*config)
:   Create a AAC decoder of Audio Element to decode incoming data using AAC format.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The audio element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv417aac_decoder_cfg_t"></a>

<a id="_CPPv317aac_decoder_cfg_t"></a> <a id="_CPPv217aac_decoder_cfg_t"></a> <a id="aac_decoder_cfg_t"></a> <a id="structaac__decoder__cfg__t"></a> struct aac\_decoder\_cfg\_t
:   AAC Decoder configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17aac_decoder_cfg_t14main_buff_sizeE"></a>

    <a id="_CPPv3N17aac_decoder_cfg_t14main_buff_sizeE"></a> <a id="_CPPv2N17aac_decoder_cfg_t14main_buff_sizeE"></a> <a id="aac_decoder_cfg_t::main_buff_size__uint32_t"></a> <a id="structaac__decoder__cfg__t_1a7d5dbcd949283fd0e5330894f819986b"></a> uint32\_t main\_buff\_size
    :   mainbuff size

    <a id="_CPPv4N17aac_decoder_cfg_t17out_pcm_buff_sizeE"></a>

    <a id="_CPPv3N17aac_decoder_cfg_t17out_pcm_buff_sizeE"></a> <a id="_CPPv2N17aac_decoder_cfg_t17out_pcm_buff_sizeE"></a> <a id="aac_decoder_cfg_t::out_pcm_buff_size__uint32_t"></a> <a id="structaac__decoder__cfg__t_1a682b9e3d8bca4872bcea1eb7433b023e"></a> uint32\_t out\_pcm\_buff\_size
    :   out pcm buffer size

    <a id="_CPPv4N17aac_decoder_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N17aac_decoder_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N17aac_decoder_cfg_t14out_block_sizeE"></a> <a id="aac_decoder_cfg_t::out_block_size__i"></a> <a id="structaac__decoder__cfg__t_1a8fd05e96f011a8c249ae7accf306d07d"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N17aac_decoder_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N17aac_decoder_cfg_t13out_block_numE"></a> <a id="_CPPv2N17aac_decoder_cfg_t13out_block_numE"></a> <a id="aac_decoder_cfg_t::out_block_num__i"></a> <a id="structaac__decoder__cfg__t_1a43c6edcfff24693c535c1753888f2e64"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N17aac_decoder_cfg_t10task_stackE"></a>

    <a id="_CPPv3N17aac_decoder_cfg_t10task_stackE"></a> <a id="_CPPv2N17aac_decoder_cfg_t10task_stackE"></a> <a id="aac_decoder_cfg_t::task_stack__i"></a> <a id="structaac__decoder__cfg__t_1abf7202f5d71dc04b0db9a3a2f33177b7"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N17aac_decoder_cfg_t9task_coreE"></a>

    <a id="_CPPv3N17aac_decoder_cfg_t9task_coreE"></a> <a id="_CPPv2N17aac_decoder_cfg_t9task_coreE"></a> <a id="aac_decoder_cfg_t::task_core__i"></a> <a id="structaac__decoder__cfg__t_1a598861136499b80ab07ed9f606606248"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N17aac_decoder_cfg_t9task_prioE"></a>

    <a id="_CPPv3N17aac_decoder_cfg_t9task_prioE"></a> <a id="_CPPv2N17aac_decoder_cfg_t9task_prioE"></a> <a id="aac_decoder_cfg_t::task_prio__i"></a> <a id="structaac__decoder__cfg__t_1a965f7fa315a6b12dfb44ed5efbccdf15"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.AAC_DECODER_MAIN_BUFF_SIZE"></a>

<a id="aac__decoder_8h_1a37855138d4773c2f5df8e92b2eee90e5"></a> AAC\_DECODER\_MAIN\_BUFF\_SIZE

<a id="c.AAC_DECODER_OUT_PCM_BUFF_SIZE"></a>

<a id="aac__decoder_8h_1af7b0749a15b8f3e489bd83d5a006cbe6"></a> AAC\_DECODER\_OUT\_PCM\_BUFF\_SIZE

<a id="c.AAC_DECODER_OUT_BLOCK_NUM"></a>

<a id="aac__decoder_8h_1a0b49e048353fe6040886d65253a1c7d4"></a> AAC\_DECODER\_OUT\_BLOCK\_NUM

<a id="c.AAC_DECODER_TASK_STACK"></a>

<a id="aac__decoder_8h_1a467bd131c1d771c75329fce09052da40"></a> AAC\_DECODER\_TASK\_STACK

<a id="c.AAC_DECODER_TASK_CORE"></a>

<a id="aac__decoder_8h_1a36e897db19033434d787b0706e03a142"></a> AAC\_DECODER\_TASK\_CORE

<a id="c.AAC_DECODER_TASK_PRIO"></a>

<a id="aac__decoder_8h_1a9527a7e873269fbf7f57ea88cf9760d8"></a> AAC\_DECODER\_TASK\_PRIO

<a id="c.DEFAULT_AAC_DECODER_CONFIG"></a>

<a id="aac__decoder_8h_1a6e675c25ab9bfef6f6721c0f3efba5bc"></a> DEFAULT\_AAC\_DECODER\_CONFIG()
