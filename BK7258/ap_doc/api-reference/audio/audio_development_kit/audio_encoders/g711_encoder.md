---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_encoders/g711_encoder.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="g711-encoder"></a>

# G711 Encoder

Encode an audio data stream to G711 format.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [g711\_encoder.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_encoders/g711_encoder.h)

<a id="functions"></a>

### Functions

<a id="_CPPv417g711_encoder_initP18g711_encoder_cfg_t"></a>

<a id="_CPPv317g711_encoder_initP18g711_encoder_cfg_t"></a> <a id="_CPPv217g711_encoder_initP18g711_encoder_cfg_t"></a> <a id="g711_encoder_init__g711_encoder_cfg_tP"></a> <a id="g711__encoder_8h_1a3147b7fcdc9ca2d4d2c7a33fb2f7961a"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") g711\_encoder\_init([g711\_encoder\_cfg\_t](#_CPPv418g711_encoder_cfg_t "g711_encoder_cfg_t") \*config)
:   Create a G711 encoder of Audio Element to encode incoming data using G711 format.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The audio element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv418g711_encoder_cfg_t"></a>

<a id="_CPPv318g711_encoder_cfg_t"></a> <a id="_CPPv218g711_encoder_cfg_t"></a> <a id="g711_encoder_cfg_t"></a> <a id="structg711__encoder__cfg__t"></a> struct g711\_encoder\_cfg\_t
:   G711 Encoder configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18g711_encoder_cfg_t6buf_szE"></a>

    <a id="_CPPv3N18g711_encoder_cfg_t6buf_szE"></a> <a id="_CPPv2N18g711_encoder_cfg_t6buf_szE"></a> <a id="g711_encoder_cfg_t::buf_sz__i"></a> <a id="structg711__encoder__cfg__t_1a514837ab1f9b9fcfe43ee6b92c10a1f2"></a> int buf\_sz
    :   Element Buffer size

    <a id="_CPPv4N18g711_encoder_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N18g711_encoder_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N18g711_encoder_cfg_t14out_block_sizeE"></a> <a id="g711_encoder_cfg_t::out_block_size__i"></a> <a id="structg711__encoder__cfg__t_1a89c55db068c0f8187fb1af95edf2b496"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N18g711_encoder_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N18g711_encoder_cfg_t13out_block_numE"></a> <a id="_CPPv2N18g711_encoder_cfg_t13out_block_numE"></a> <a id="g711_encoder_cfg_t::out_block_num__i"></a> <a id="structg711__encoder__cfg__t_1ad695e74628c247fed4cdc98e5e0f0515"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N18g711_encoder_cfg_t10task_stackE"></a>

    <a id="_CPPv3N18g711_encoder_cfg_t10task_stackE"></a> <a id="_CPPv2N18g711_encoder_cfg_t10task_stackE"></a> <a id="g711_encoder_cfg_t::task_stack__i"></a> <a id="structg711__encoder__cfg__t_1a3a74b9d0ae476ce95dc2ddd4823fe137"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N18g711_encoder_cfg_t9task_coreE"></a>

    <a id="_CPPv3N18g711_encoder_cfg_t9task_coreE"></a> <a id="_CPPv2N18g711_encoder_cfg_t9task_coreE"></a> <a id="g711_encoder_cfg_t::task_core__i"></a> <a id="structg711__encoder__cfg__t_1a5d8073e0d5b6a6d9ebe921cca7765677"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N18g711_encoder_cfg_t9task_prioE"></a>

    <a id="_CPPv3N18g711_encoder_cfg_t9task_prioE"></a> <a id="_CPPv2N18g711_encoder_cfg_t9task_prioE"></a> <a id="g711_encoder_cfg_t::task_prio__i"></a> <a id="structg711__encoder__cfg__t_1aa3f8e82f5a4326253dc67a4341da1b81"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

    <a id="_CPPv4N18g711_encoder_cfg_t8enc_modeE"></a>

    <a id="_CPPv3N18g711_encoder_cfg_t8enc_modeE"></a> <a id="_CPPv2N18g711_encoder_cfg_t8enc_modeE"></a> <a id="g711_encoder_cfg_t::enc_mode__g711_encoder_mode_t"></a> <a id="structg711__encoder__cfg__t_1a30f38958ba6b04ea86822b2acb207d50"></a> [g711\_encoder\_mode\_t](#_CPPv419g711_encoder_mode_t "g711_encoder_mode_t") enc\_mode
    :   0: a-law 1: u-law

<a id="macros"></a>

### Macros

<a id="c.G711_ENCODER_TASK_STACK"></a>

<a id="g711__encoder_8h_1a5a4c9dd94fa12967f677cfbed4d2feed"></a> G711\_ENCODER\_TASK\_STACK

<a id="c.G711_ENCODER_TASK_CORE"></a>

<a id="g711__encoder_8h_1ad2be2e3d3d3210f91e8d85120f1f206c"></a> G711\_ENCODER\_TASK\_CORE

<a id="c.G711_ENCODER_TASK_PRIO"></a>

<a id="g711__encoder_8h_1a7f5f44d7b646ddbf77115f4bfdbbf9ba"></a> G711\_ENCODER\_TASK\_PRIO

<a id="c.G711_ENCODER_BUFFER_SIZE"></a>

<a id="g711__encoder_8h_1ac55ba044be1f8b7f265ba6a590179b50"></a> G711\_ENCODER\_BUFFER\_SIZE

<a id="c.G711_ENCODER_OUT_BLOCK_SIZE"></a>

<a id="g711__encoder_8h_1a34277d53cb5ad699c85afe400272056e"></a> G711\_ENCODER\_OUT\_BLOCK\_SIZE

<a id="c.G711_ENCODER_OUT_BLOCK_NUM"></a>

<a id="g711__encoder_8h_1a7f9f3c2a7a85a8cf739c4cfdd719ed9c"></a> G711\_ENCODER\_OUT\_BLOCK\_NUM

<a id="c.DEFAULT_G711_ENCODER_CONFIG"></a>

<a id="g711__encoder_8h_1a3f7762b01380eda139c8e32516fe63b5"></a> DEFAULT\_G711\_ENCODER\_CONFIG()

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv419g711_encoder_mode_t"></a>

<a id="_CPPv319g711_encoder_mode_t"></a> <a id="_CPPv219g711_encoder_mode_t"></a> <a id="g711__encoder_8h_1ab04152e1460b6dbbdf052b9db5aa5c4c"></a> enum g711\_encoder\_mode\_t
:   Enum of G711 Encoder enc\_mode.

    *Values:*

    <a id="_CPPv4N19g711_encoder_mode_t19G711_ENC_MODE_A_LOWE"></a>

    <a id="_CPPv3N19g711_encoder_mode_t19G711_ENC_MODE_A_LOWE"></a> <a id="_CPPv2N19g711_encoder_mode_t19G711_ENC_MODE_A_LOWE"></a> <a id="g711__encoder_8h_1ab04152e1460b6dbbdf052b9db5aa5c4ca469e55a9547d8f53b70222616acc394e"></a> enumerator G711\_ENC\_MODE\_A\_LOW

    <a id="_CPPv4N19g711_encoder_mode_t19G711_ENC_MODE_U_LOWE"></a>

    <a id="_CPPv3N19g711_encoder_mode_t19G711_ENC_MODE_U_LOWE"></a> <a id="_CPPv2N19g711_encoder_mode_t19G711_ENC_MODE_U_LOWE"></a> <a id="g711__encoder_8h_1ab04152e1460b6dbbdf052b9db5aa5c4ca9b4ca7fee411fb8b61819f18766226b0"></a> enumerator G711\_ENC\_MODE\_U\_LOW

    <a id="_CPPv4N19g711_encoder_mode_t17G711_ENC_MODE_MAXE"></a>

    <a id="_CPPv3N19g711_encoder_mode_t17G711_ENC_MODE_MAXE"></a> <a id="_CPPv2N19g711_encoder_mode_t17G711_ENC_MODE_MAXE"></a> <a id="g711__encoder_8h_1ab04152e1460b6dbbdf052b9db5aa5c4ca478f1a27f5d81f69707ff96316d8d63f"></a> enumerator G711\_ENC\_MODE\_MAX
    :   Invalid mode
