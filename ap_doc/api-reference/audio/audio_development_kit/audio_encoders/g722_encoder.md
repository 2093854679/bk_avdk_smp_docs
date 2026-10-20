---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/audio_development_kit/audio_encoders/g722_encoder.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="g722-encoder"></a>

# G722 Encoder

Encode an audio data stream to G722 format.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [g722\_encoder.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_audio/audio_encoders/g722_encoder.h)

<a id="functions"></a>

### Functions

<a id="_CPPv417g722_encoder_initP18g722_encoder_cfg_t"></a>

<a id="_CPPv317g722_encoder_initP18g722_encoder_cfg_t"></a> <a id="_CPPv217g722_encoder_initP18g722_encoder_cfg_t"></a> <a id="g722_encoder_init__g722_encoder_cfg_tP"></a> <a id="g722__encoder_8h_1a6d119fd8e68387d27e6f6f6b1d4bc9b9"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") g722\_encoder\_init([g722\_encoder\_cfg\_t](#_CPPv418g722_encoder_cfg_t "g722_encoder_cfg_t") \*config)
:   Create a G722 encoder of Audio Element to encode incoming data using G722 format.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The audio element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv418g722_encoder_cfg_t"></a>

<a id="_CPPv318g722_encoder_cfg_t"></a> <a id="_CPPv218g722_encoder_cfg_t"></a> <a id="g722_encoder_cfg_t"></a> <a id="structg722__encoder__cfg__t"></a> struct g722\_encoder\_cfg\_t
:   G722 Encoder configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18g722_encoder_cfg_t6buf_szE"></a>

    <a id="_CPPv3N18g722_encoder_cfg_t6buf_szE"></a> <a id="_CPPv2N18g722_encoder_cfg_t6buf_szE"></a> <a id="g722_encoder_cfg_t::buf_sz__i"></a> <a id="structg722__encoder__cfg__t_1a84e9906b9369cf8e7146b7870e0eac56"></a> int buf\_sz
    :   Element Buffer size

    <a id="_CPPv4N18g722_encoder_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N18g722_encoder_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N18g722_encoder_cfg_t14out_block_sizeE"></a> <a id="g722_encoder_cfg_t::out_block_size__i"></a> <a id="structg722__encoder__cfg__t_1a01aa9fd2eb331490da27a6effc682bdf"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N18g722_encoder_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N18g722_encoder_cfg_t13out_block_numE"></a> <a id="_CPPv2N18g722_encoder_cfg_t13out_block_numE"></a> <a id="g722_encoder_cfg_t::out_block_num__i"></a> <a id="structg722__encoder__cfg__t_1ae55191eef15882f88fd985fb86f916f9"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N18g722_encoder_cfg_t10task_stackE"></a>

    <a id="_CPPv3N18g722_encoder_cfg_t10task_stackE"></a> <a id="_CPPv2N18g722_encoder_cfg_t10task_stackE"></a> <a id="g722_encoder_cfg_t::task_stack__i"></a> <a id="structg722__encoder__cfg__t_1a70891175134e138a8d2dacbef622b2b7"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N18g722_encoder_cfg_t9task_coreE"></a>

    <a id="_CPPv3N18g722_encoder_cfg_t9task_coreE"></a> <a id="_CPPv2N18g722_encoder_cfg_t9task_coreE"></a> <a id="g722_encoder_cfg_t::task_core__i"></a> <a id="structg722__encoder__cfg__t_1a07aed3d4fff799344cd1b529fe8744ef"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N18g722_encoder_cfg_t9task_prioE"></a>

    <a id="_CPPv3N18g722_encoder_cfg_t9task_prioE"></a> <a id="_CPPv2N18g722_encoder_cfg_t9task_prioE"></a> <a id="g722_encoder_cfg_t::task_prio__i"></a> <a id="structg722__encoder__cfg__t_1ab0cf972cdde34753c9fb25a39e32be2f"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

    <a id="_CPPv4N18g722_encoder_cfg_t8enc_rateE"></a>

    <a id="_CPPv3N18g722_encoder_cfg_t8enc_rateE"></a> <a id="_CPPv2N18g722_encoder_cfg_t8enc_rateE"></a> <a id="g722_encoder_cfg_t::enc_rate__g722_encoder_rate_t"></a> <a id="structg722__encoder__cfg__t_1a0484e0a96adf236b87cd39638b3baab2"></a> [g722\_encoder\_rate\_t](#_CPPv419g722_encoder_rate_t "g722_encoder_rate_t") enc\_rate
    :   0: 48kbps 1: 56kbps 2: 64kbps

    <a id="_CPPv4N18g722_encoder_cfg_t7optionsE"></a>

    <a id="_CPPv3N18g722_encoder_cfg_t7optionsE"></a> <a id="_CPPv2N18g722_encoder_cfg_t7optionsE"></a> <a id="g722_encoder_cfg_t::options__i"></a> <a id="structg722__encoder__cfg__t_1a739e8b0c4d9a8de633c26f50b431a024"></a> int options
    :   G722 options, combination of G722\_SAMPLE\_RATE\_8000 and G722\_PACKED

<a id="macros"></a>

### Macros

<a id="c.G722_ENCODER_TASK_STACK"></a>

<a id="g722__encoder_8h_1a1af1e3cce3e4ddc95f23cbcb75540dda"></a> G722\_ENCODER\_TASK\_STACK

<a id="c.G722_ENCODER_TASK_CORE"></a>

<a id="g722__encoder_8h_1a59e1c6b1d37a31debc631f56b531aaa2"></a> G722\_ENCODER\_TASK\_CORE

<a id="c.G722_ENCODER_TASK_PRIO"></a>

<a id="g722__encoder_8h_1a6d62fb34cdaaf4f18bad0e174f6e1b5e"></a> G722\_ENCODER\_TASK\_PRIO

<a id="c.G722_ENCODER_BUFFER_SIZE"></a>

<a id="g722__encoder_8h_1accf53d5a0e77060b76ee2becfa413c58"></a> G722\_ENCODER\_BUFFER\_SIZE

<a id="c.G722_ENCODER_OUT_BLOCK_SIZE"></a>

<a id="g722__encoder_8h_1a7f7f3af67872e7149e6538e57b604965"></a> G722\_ENCODER\_OUT\_BLOCK\_SIZE

<a id="c.G722_ENCODER_OUT_BLOCK_NUM"></a>

<a id="g722__encoder_8h_1a44d50c69dfb75d29d7351a10e08b4e37"></a> G722\_ENCODER\_OUT\_BLOCK\_NUM

<a id="c.DEFAULT_G722_ENCODER_CONFIG"></a>

<a id="g722__encoder_8h_1a6f08511fe64dd17db371afa75fb70a34"></a> DEFAULT\_G722\_ENCODER\_CONFIG()

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv419g722_encoder_rate_t"></a>

<a id="_CPPv319g722_encoder_rate_t"></a> <a id="_CPPv219g722_encoder_rate_t"></a> <a id="g722__encoder_8h_1a9f3a07148d048b154b982969cf66333d"></a> enum g722\_encoder\_rate\_t
:   Enum of G722 Encoder bit rate.

    *Values:*

    <a id="_CPPv4N19g722_encoder_rate_t19G722_ENC_RATE_48000E"></a>

    <a id="_CPPv3N19g722_encoder_rate_t19G722_ENC_RATE_48000E"></a> <a id="_CPPv2N19g722_encoder_rate_t19G722_ENC_RATE_48000E"></a> <a id="g722__encoder_8h_1a9f3a07148d048b154b982969cf66333da6fa2d1ead67380e9c0ec6d360a356004"></a> enumerator G722\_ENC\_RATE\_48000

    <a id="_CPPv4N19g722_encoder_rate_t19G722_ENC_RATE_56000E"></a>

    <a id="_CPPv3N19g722_encoder_rate_t19G722_ENC_RATE_56000E"></a> <a id="_CPPv2N19g722_encoder_rate_t19G722_ENC_RATE_56000E"></a> <a id="g722__encoder_8h_1a9f3a07148d048b154b982969cf66333da08f0d9c283b720f7f1f5999887174c4b"></a> enumerator G722\_ENC\_RATE\_56000

    <a id="_CPPv4N19g722_encoder_rate_t19G722_ENC_RATE_64000E"></a>

    <a id="_CPPv3N19g722_encoder_rate_t19G722_ENC_RATE_64000E"></a> <a id="_CPPv2N19g722_encoder_rate_t19G722_ENC_RATE_64000E"></a> <a id="g722__encoder_8h_1a9f3a07148d048b154b982969cf66333da1d1597aac815b64d2a92bf9a98c8a573"></a> enumerator G722\_ENC\_RATE\_64000

    <a id="_CPPv4N19g722_encoder_rate_t17G722_ENC_RATE_MAXE"></a>

    <a id="_CPPv3N19g722_encoder_rate_t17G722_ENC_RATE_MAXE"></a> <a id="_CPPv2N19g722_encoder_rate_t17G722_ENC_RATE_MAXE"></a> <a id="g722__encoder_8h_1a9f3a07148d048b154b982969cf66333da2a8977f645ffffc634dff4c5913594f7"></a> enumerator G722\_ENC\_RATE\_MAX
    :   Invalid rate
