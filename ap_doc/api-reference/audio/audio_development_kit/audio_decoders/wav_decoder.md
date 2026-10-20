---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/audio_development_kit/audio_decoders/wav_decoder.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wav-decoder"></a>

# WAV Decoder

Decode an audio data stream provided in WAV format.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [wav\_decoder.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_audio/audio_decoders/wav_decoder.h)

<a id="functions"></a>

### Functions

<a id="_CPPv416wav_decoder_initP17wav_decoder_cfg_t"></a>

<a id="_CPPv316wav_decoder_initP17wav_decoder_cfg_t"></a> <a id="_CPPv216wav_decoder_initP17wav_decoder_cfg_t"></a> <a id="wav_decoder_init__wav_decoder_cfg_tP"></a> <a id="wav__decoder_8h_1a4bb646e5682a0e399e1671e110c67313"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") wav\_decoder\_init([wav\_decoder\_cfg\_t](#_CPPv417wav_decoder_cfg_t "wav_decoder_cfg_t") \*config)
:   Create a WAV decoder of Audio Element to decode incoming data using WAV format.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The audio element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv417wav_decoder_cfg_t"></a>

<a id="_CPPv317wav_decoder_cfg_t"></a> <a id="_CPPv217wav_decoder_cfg_t"></a> <a id="wav_decoder_cfg_t"></a> <a id="structwav__decoder__cfg__t"></a> struct wav\_decoder\_cfg\_t
:   WAV Decoder configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17wav_decoder_cfg_t6buf_szE"></a>

    <a id="_CPPv3N17wav_decoder_cfg_t6buf_szE"></a> <a id="_CPPv2N17wav_decoder_cfg_t6buf_szE"></a> <a id="wav_decoder_cfg_t::buf_sz__i"></a> <a id="structwav__decoder__cfg__t_1a05f1f0fe62e4d1e7d584a2624d3b82df"></a> int buf\_sz
    :   Element Buffer size

    <a id="_CPPv4N17wav_decoder_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N17wav_decoder_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N17wav_decoder_cfg_t14out_block_sizeE"></a> <a id="wav_decoder_cfg_t::out_block_size__i"></a> <a id="structwav__decoder__cfg__t_1ac8562ce7e14dde4e1c05632870043f67"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N17wav_decoder_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N17wav_decoder_cfg_t13out_block_numE"></a> <a id="_CPPv2N17wav_decoder_cfg_t13out_block_numE"></a> <a id="wav_decoder_cfg_t::out_block_num__i"></a> <a id="structwav__decoder__cfg__t_1a3d24c1e83f5703be206f8e69f29a4566"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N17wav_decoder_cfg_t10task_stackE"></a>

    <a id="_CPPv3N17wav_decoder_cfg_t10task_stackE"></a> <a id="_CPPv2N17wav_decoder_cfg_t10task_stackE"></a> <a id="wav_decoder_cfg_t::task_stack__i"></a> <a id="structwav__decoder__cfg__t_1a4d872d1a932c2339fc3dc96814ba43f1"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N17wav_decoder_cfg_t9task_coreE"></a>

    <a id="_CPPv3N17wav_decoder_cfg_t9task_coreE"></a> <a id="_CPPv2N17wav_decoder_cfg_t9task_coreE"></a> <a id="wav_decoder_cfg_t::task_core__i"></a> <a id="structwav__decoder__cfg__t_1abdd29d6e2f846e24a51bab154bc3b4fc"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N17wav_decoder_cfg_t9task_prioE"></a>

    <a id="_CPPv3N17wav_decoder_cfg_t9task_prioE"></a> <a id="_CPPv2N17wav_decoder_cfg_t9task_prioE"></a> <a id="wav_decoder_cfg_t::task_prio__i"></a> <a id="structwav__decoder__cfg__t_1acaff8633555d6a05589b9806af2a4f21"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.WAV_DECODER_TASK_STACK"></a>

<a id="wav__decoder_8h_1a64b9cb328d7c9a751ab61496cb79c9ff"></a> WAV\_DECODER\_TASK\_STACK

<a id="c.WAV_DECODER_TASK_CORE"></a>

<a id="wav__decoder_8h_1a14553d9038884d937005a3fe5abd7232"></a> WAV\_DECODER\_TASK\_CORE

<a id="c.WAV_DECODER_TASK_PRIO"></a>

<a id="wav__decoder_8h_1a12ef7dce3820a96ce20bac5e6f9e5249"></a> WAV\_DECODER\_TASK\_PRIO

<a id="c.WAV_DECODER_BUFFER_SIZE"></a>

<a id="wav__decoder_8h_1a2a819059de6dec23de04487a3b669333"></a> WAV\_DECODER\_BUFFER\_SIZE

<a id="c.WAV_DECODER_OUT_BLOCK_SIZE"></a>

<a id="wav__decoder_8h_1a41a524b89733ff12b93d0889829da185"></a> WAV\_DECODER\_OUT\_BLOCK\_SIZE

<a id="c.WAV_DECODER_OUT_BLOCK_NUM"></a>

<a id="wav__decoder_8h_1a21f8df65cad4bfe4dba6352f905205c4"></a> WAV\_DECODER\_OUT\_BLOCK\_NUM

<a id="c.DEFAULT_WAV_DECODER_CONFIG"></a>

<a id="wav__decoder_8h_1a2d1f75f955126c02368d2ceb876436b1"></a> DEFAULT\_WAV\_DECODER\_CONFIG()
