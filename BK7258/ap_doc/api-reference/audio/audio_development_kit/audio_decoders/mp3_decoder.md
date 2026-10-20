---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_decoders/mp3_decoder.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="mp3-decoder"></a>

# MP3 Decoder

Decode an audio data stream provided in MP3 format.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [mp3\_decoder.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_decoders/mp3_decoder.h)

<a id="functions"></a>

### Functions

<a id="_CPPv416mp3_decoder_initP17mp3_decoder_cfg_t"></a>

<a id="_CPPv316mp3_decoder_initP17mp3_decoder_cfg_t"></a> <a id="_CPPv216mp3_decoder_initP17mp3_decoder_cfg_t"></a> <a id="mp3_decoder_init__mp3_decoder_cfg_tP"></a> <a id="mp3__decoder_8h_1a3ecb5c28f9435c373dd7e025dd225516"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") mp3\_decoder\_init([mp3\_decoder\_cfg\_t](#_CPPv417mp3_decoder_cfg_t "mp3_decoder_cfg_t") \*config)
:   Create a MP3 decoder of Audio Element to decode incoming data using MP3 format.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The audio element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv417mp3_decoder_cfg_t"></a>

<a id="_CPPv317mp3_decoder_cfg_t"></a> <a id="_CPPv217mp3_decoder_cfg_t"></a> <a id="mp3_decoder_cfg_t"></a> <a id="structmp3__decoder__cfg__t"></a> struct mp3\_decoder\_cfg\_t
:   MP3 Decoder configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17mp3_decoder_cfg_t14main_buff_sizeE"></a>

    <a id="_CPPv3N17mp3_decoder_cfg_t14main_buff_sizeE"></a> <a id="_CPPv2N17mp3_decoder_cfg_t14main_buff_sizeE"></a> <a id="mp3_decoder_cfg_t::main_buff_size__uint32_t"></a> <a id="structmp3__decoder__cfg__t_1a0ecbee04b2a902676385d2dfc7a559c9"></a> uint32\_t main\_buff\_size
    :   mainbuff size

    <a id="_CPPv4N17mp3_decoder_cfg_t17out_pcm_buff_sizeE"></a>

    <a id="_CPPv3N17mp3_decoder_cfg_t17out_pcm_buff_sizeE"></a> <a id="_CPPv2N17mp3_decoder_cfg_t17out_pcm_buff_sizeE"></a> <a id="mp3_decoder_cfg_t::out_pcm_buff_size__uint32_t"></a> <a id="structmp3__decoder__cfg__t_1a580672ef273b362d7b1676538e6b0874"></a> uint32\_t out\_pcm\_buff\_size
    :   out pcm buffer size

    <a id="_CPPv4N17mp3_decoder_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N17mp3_decoder_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N17mp3_decoder_cfg_t14out_block_sizeE"></a> <a id="mp3_decoder_cfg_t::out_block_size__i"></a> <a id="structmp3__decoder__cfg__t_1affb2d283a7b91d533edc4b16e5534b61"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N17mp3_decoder_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N17mp3_decoder_cfg_t13out_block_numE"></a> <a id="_CPPv2N17mp3_decoder_cfg_t13out_block_numE"></a> <a id="mp3_decoder_cfg_t::out_block_num__i"></a> <a id="structmp3__decoder__cfg__t_1a39b1a3aaf4571ddfdc33c880a09732ca"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N17mp3_decoder_cfg_t10task_stackE"></a>

    <a id="_CPPv3N17mp3_decoder_cfg_t10task_stackE"></a> <a id="_CPPv2N17mp3_decoder_cfg_t10task_stackE"></a> <a id="mp3_decoder_cfg_t::task_stack__i"></a> <a id="structmp3__decoder__cfg__t_1a3dd6ec64203e8a5517b375e2a7641676"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N17mp3_decoder_cfg_t9task_coreE"></a>

    <a id="_CPPv3N17mp3_decoder_cfg_t9task_coreE"></a> <a id="_CPPv2N17mp3_decoder_cfg_t9task_coreE"></a> <a id="mp3_decoder_cfg_t::task_core__i"></a> <a id="structmp3__decoder__cfg__t_1a10a66349ec239851eb80235f1a066c5b"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N17mp3_decoder_cfg_t9task_prioE"></a>

    <a id="_CPPv3N17mp3_decoder_cfg_t9task_prioE"></a> <a id="_CPPv2N17mp3_decoder_cfg_t9task_prioE"></a> <a id="mp3_decoder_cfg_t::task_prio__i"></a> <a id="structmp3__decoder__cfg__t_1ad38533f9aa3b3aba2531f2d61981da31"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.MP3_DECODER_TASK_STACK"></a>

<a id="mp3__decoder_8h_1a0ebc2062ef1cffdc6a8eb57fcfc15d82"></a> MP3\_DECODER\_TASK\_STACK

<a id="c.MP3_DECODER_TASK_CORE"></a>

<a id="mp3__decoder_8h_1ae6ad7f5abddaba7de35b5f8bdc7eb234"></a> MP3\_DECODER\_TASK\_CORE

<a id="c.MP3_DECODER_TASK_PRIO"></a>

<a id="mp3__decoder_8h_1aa5e784a7e4814b82d030ffc1adcc5ea9"></a> MP3\_DECODER\_TASK\_PRIO

<a id="c.MP3_DECODER_MAIN_BUFF_SIZE"></a>

<a id="mp3__decoder_8h_1ad39d543a6f7420d66ad5839866561a25"></a> MP3\_DECODER\_MAIN\_BUFF\_SIZE

<a id="c.MP3_DECODER_OUT_PCM_BUFF_SIZE"></a>

<a id="mp3__decoder_8h_1a7c96904eaab114f0c05e6aac2e4d9d77"></a> MP3\_DECODER\_OUT\_PCM\_BUFF\_SIZE

<a id="c.DEFAULT_MP3_DECODER_CONFIG"></a>

<a id="mp3__decoder_8h_1a627d1d5e06f4efcdb436028d87d32532"></a> DEFAULT\_MP3\_DECODER\_CONFIG()
