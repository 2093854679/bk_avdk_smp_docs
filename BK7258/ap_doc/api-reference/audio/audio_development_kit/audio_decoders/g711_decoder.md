---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_decoders/g711_decoder.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="g711-decoder"></a>

# G711 Decoder

Decode an audio data stream provided in G711 format.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [g711\_decoder.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_decoders/g711_decoder.h)

<a id="functions"></a>

### Functions

<a id="_CPPv417g711_decoder_initP18g711_decoder_cfg_t"></a>

<a id="_CPPv317g711_decoder_initP18g711_decoder_cfg_t"></a> <a id="_CPPv217g711_decoder_initP18g711_decoder_cfg_t"></a> <a id="g711_decoder_init__g711_decoder_cfg_tP"></a> <a id="g711__decoder_8h_1a7098aa0f181b68997d53ad7a8fab14f1"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") g711\_decoder\_init([g711\_decoder\_cfg\_t](#_CPPv418g711_decoder_cfg_t "g711_decoder_cfg_t") \*config)
:   Create a G711 decoder of Audio Element to decode incoming data using G711 format.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The audio element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv418g711_decoder_cfg_t"></a>

<a id="_CPPv318g711_decoder_cfg_t"></a> <a id="_CPPv218g711_decoder_cfg_t"></a> <a id="g711_decoder_cfg_t"></a> <a id="structg711__decoder__cfg__t"></a> struct g711\_decoder\_cfg\_t
:   G711 Decoder configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18g711_decoder_cfg_t6buf_szE"></a>

    <a id="_CPPv3N18g711_decoder_cfg_t6buf_szE"></a> <a id="_CPPv2N18g711_decoder_cfg_t6buf_szE"></a> <a id="g711_decoder_cfg_t::buf_sz__i"></a> <a id="structg711__decoder__cfg__t_1aaeb860d058155385f1351acf357baa96"></a> int buf\_sz
    :   Element Buffer size

    <a id="_CPPv4N18g711_decoder_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N18g711_decoder_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N18g711_decoder_cfg_t14out_block_sizeE"></a> <a id="g711_decoder_cfg_t::out_block_size__i"></a> <a id="structg711__decoder__cfg__t_1ad0b3d40873c8c5f0dc3e415541ae0669"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N18g711_decoder_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N18g711_decoder_cfg_t13out_block_numE"></a> <a id="_CPPv2N18g711_decoder_cfg_t13out_block_numE"></a> <a id="g711_decoder_cfg_t::out_block_num__i"></a> <a id="structg711__decoder__cfg__t_1ad477f1767208d4f590fd81dee2ecedf1"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N18g711_decoder_cfg_t10task_stackE"></a>

    <a id="_CPPv3N18g711_decoder_cfg_t10task_stackE"></a> <a id="_CPPv2N18g711_decoder_cfg_t10task_stackE"></a> <a id="g711_decoder_cfg_t::task_stack__i"></a> <a id="structg711__decoder__cfg__t_1aeeb8bfae0673a282960fb71836a9958e"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N18g711_decoder_cfg_t9task_coreE"></a>

    <a id="_CPPv3N18g711_decoder_cfg_t9task_coreE"></a> <a id="_CPPv2N18g711_decoder_cfg_t9task_coreE"></a> <a id="g711_decoder_cfg_t::task_core__i"></a> <a id="structg711__decoder__cfg__t_1aefa6b1fb684d5816fb0be151d5b76ae0"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N18g711_decoder_cfg_t9task_prioE"></a>

    <a id="_CPPv3N18g711_decoder_cfg_t9task_prioE"></a> <a id="_CPPv2N18g711_decoder_cfg_t9task_prioE"></a> <a id="g711_decoder_cfg_t::task_prio__i"></a> <a id="structg711__decoder__cfg__t_1a5d019f54a3abbf367a0f50d4bdc6c48d"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

    <a id="_CPPv4N18g711_decoder_cfg_t8dec_modeE"></a>

    <a id="_CPPv3N18g711_decoder_cfg_t8dec_modeE"></a> <a id="_CPPv2N18g711_decoder_cfg_t8dec_modeE"></a> <a id="g711_decoder_cfg_t::dec_mode__g711_decoder_mode_t"></a> <a id="structg711__decoder__cfg__t_1ae979a22df73fae8e8963c2de52b23ab7"></a> [g711\_decoder\_mode\_t](#_CPPv419g711_decoder_mode_t "g711_decoder_mode_t") dec\_mode
    :   0: a-law 1: u-law

<a id="macros"></a>

### Macros

<a id="c.G711_DECODER_TASK_STACK"></a>

<a id="g711__decoder_8h_1a2f910df891ecc761a0845d3114b00874"></a> G711\_DECODER\_TASK\_STACK

<a id="c.G711_DECODER_TASK_CORE"></a>

<a id="g711__decoder_8h_1a34c86e756fe638db771cb015c602fc50"></a> G711\_DECODER\_TASK\_CORE

<a id="c.G711_DECODER_TASK_PRIO"></a>

<a id="g711__decoder_8h_1ad4263016a1620d33db498a07d395297c"></a> G711\_DECODER\_TASK\_PRIO

<a id="c.G711_DECODER_BUFFER_SIZE"></a>

<a id="g711__decoder_8h_1af27ce7decbf87335a63cb8677f46ad00"></a> G711\_DECODER\_BUFFER\_SIZE

<a id="c.G711_DECODER_OUT_BLOCK_SIZE"></a>

<a id="g711__decoder_8h_1abd895bd13c897326a35da77ad85f5b31"></a> G711\_DECODER\_OUT\_BLOCK\_SIZE

<a id="c.G711_DECODER_OUT_BLOCK_NUM"></a>

<a id="g711__decoder_8h_1a4118ad39a8a581ebedae54bee085ed33"></a> G711\_DECODER\_OUT\_BLOCK\_NUM

<a id="c.DEFAULT_G711_DECODER_CONFIG"></a>

<a id="g711__decoder_8h_1af6e6d598e088339d20d63902388a4b16"></a> DEFAULT\_G711\_DECODER\_CONFIG()

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv419g711_decoder_mode_t"></a>

<a id="_CPPv319g711_decoder_mode_t"></a> <a id="_CPPv219g711_decoder_mode_t"></a> <a id="g711__decoder_8h_1a5c259214c460559de7d3791b210e2c0a"></a> enum g711\_decoder\_mode\_t
:   Enum of G711 Decoder dec\_mode.

    *Values:*

    <a id="_CPPv4N19g711_decoder_mode_t19G711_DEC_MODE_A_LOWE"></a>

    <a id="_CPPv3N19g711_decoder_mode_t19G711_DEC_MODE_A_LOWE"></a> <a id="_CPPv2N19g711_decoder_mode_t19G711_DEC_MODE_A_LOWE"></a> <a id="g711__decoder_8h_1a5c259214c460559de7d3791b210e2c0aa7f34e96a7754e9e7da69fb60b4f4d9d0"></a> enumerator G711\_DEC\_MODE\_A\_LOW

    <a id="_CPPv4N19g711_decoder_mode_t19G711_DEC_MODE_U_LOWE"></a>

    <a id="_CPPv3N19g711_decoder_mode_t19G711_DEC_MODE_U_LOWE"></a> <a id="_CPPv2N19g711_decoder_mode_t19G711_DEC_MODE_U_LOWE"></a> <a id="g711__decoder_8h_1a5c259214c460559de7d3791b210e2c0aadfd34fdb35c8c60b9424ba4f64e74d9e"></a> enumerator G711\_DEC\_MODE\_U\_LOW

    <a id="_CPPv4N19g711_decoder_mode_t17G711_DEC_MODE_MAXE"></a>

    <a id="_CPPv3N19g711_decoder_mode_t17G711_DEC_MODE_MAXE"></a> <a id="_CPPv2N19g711_decoder_mode_t17G711_DEC_MODE_MAXE"></a> <a id="g711__decoder_8h_1a5c259214c460559de7d3791b210e2c0aa261ca8d7aac81d0bb2da7dac78618a51"></a> enumerator G711\_DEC\_MODE\_MAX
    :   Invalid mode
