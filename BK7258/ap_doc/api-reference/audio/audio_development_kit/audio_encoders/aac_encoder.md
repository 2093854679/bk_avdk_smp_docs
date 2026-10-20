---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_encoders/aac_encoder.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="aac-encoder"></a>

# AAC Encoder

Encode an audio data stream to AAC format.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [aac\_encoder.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_encoders/aac_encoder.h)

<a id="functions"></a>

### Functions

<a id="_CPPv416aac_encoder_initP17aac_encoder_cfg_t"></a>

<a id="_CPPv316aac_encoder_initP17aac_encoder_cfg_t"></a> <a id="_CPPv216aac_encoder_initP17aac_encoder_cfg_t"></a> <a id="aac_encoder_init__aac_encoder_cfg_tP"></a> <a id="aac__encoder_8h_1aa2d3623049eb051c65d7889fbf103ec0"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") aac\_encoder\_init([aac\_encoder\_cfg\_t](#_CPPv417aac_encoder_cfg_t "aac_encoder_cfg_t") \*config)
:   Create a AAC encoder of Audio Element to encode incoming data using AAC format.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The audio element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv417aac_encoder_cfg_t"></a>

<a id="_CPPv317aac_encoder_cfg_t"></a> <a id="_CPPv217aac_encoder_cfg_t"></a> <a id="aac_encoder_cfg_t"></a> <a id="structaac__encoder__cfg__t"></a> struct aac\_encoder\_cfg\_t
:   AAC Encoder configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17aac_encoder_cfg_t7chl_numE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t7chl_numE"></a> <a id="_CPPv2N17aac_encoder_cfg_t7chl_numE"></a> <a id="aac_encoder_cfg_t::chl_num__uint8_t"></a> <a id="structaac__encoder__cfg__t_1aad5d6ff5647724d3a8e0e8404a8800c0"></a> uint8\_t chl\_num
    :   channel number

    <a id="_CPPv4N17aac_encoder_cfg_t9samp_rateE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t9samp_rateE"></a> <a id="_CPPv2N17aac_encoder_cfg_t9samp_rateE"></a> <a id="aac_encoder_cfg_t::samp_rate__uint32_t"></a> <a id="structaac__encoder__cfg__t_1a2f322a48d5b2922592058e88520a7b27"></a> uint32\_t samp\_rate
    :   sample rate

    <a id="_CPPv4N17aac_encoder_cfg_t4bitsE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t4bitsE"></a> <a id="_CPPv2N17aac_encoder_cfg_t4bitsE"></a> <a id="aac_encoder_cfg_t::bits__uint8_t"></a> <a id="structaac__encoder__cfg__t_1aad6587a0b8f44f45ed9f638a40b5fe6c"></a> uint8\_t bits
    :   Bit wide (8, 16, 24, 32 bits)

    <a id="_CPPv4N17aac_encoder_cfg_t7modulesE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t7modulesE"></a> <a id="_CPPv2N17aac_encoder_cfg_t7modulesE"></a> <a id="aac_encoder_cfg_t::modules__uint32_t"></a> <a id="structaac__encoder__cfg__t_1a2d0193b131df15cc80c6cde0b08fcd3d"></a> uint32\_t modules
    :   modules, refer to “encModules” parameter description of “aacEncOpen” spi in aacenc\_lib.h

    <a id="_CPPv4N17aac_encoder_cfg_t3aotE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t3aotE"></a> <a id="_CPPv2N17aac_encoder_cfg_t3aotE"></a> <a id="aac_encoder_cfg_t::aot__uint8_t"></a> <a id="structaac__encoder__cfg__t_1a19b54ac7f27a9642e3d625ae9d0db22f"></a> uint8\_t aot
    :   Audio object type, refer to “AACENC\_AOT” parameter description in aacenc\_lib.h

    <a id="_CPPv4N17aac_encoder_cfg_t7bitrateE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t7bitrateE"></a> <a id="_CPPv2N17aac_encoder_cfg_t7bitrateE"></a> <a id="aac_encoder_cfg_t::bitrate__uint32_t"></a> <a id="structaac__encoder__cfg__t_1aa20cc459a80bf8694e39814ea60e43b1"></a> uint32\_t bitrate
    :   encoder bitrate, refer to “AACENC\_BITRATE” parameter description in aacenc\_lib.h

    <a id="_CPPv4N17aac_encoder_cfg_t12bitrate_modeE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t12bitrate_modeE"></a> <a id="_CPPv2N17aac_encoder_cfg_t12bitrate_modeE"></a> <a id="aac_encoder_cfg_t::bitrate_mode__uint8_t"></a> <a id="structaac__encoder__cfg__t_1a8efc523a6070f32f1cde4bd27e0ae2ab"></a> uint8\_t bitrate\_mode
    :   Bitrate mode, refer to “AACENC\_BITRATEMODE” parameter description in aacenc\_lib.h

    <a id="_CPPv4N17aac_encoder_cfg_t8sbr_modeE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t8sbr_modeE"></a> <a id="_CPPv2N17aac_encoder_cfg_t8sbr_modeE"></a> <a id="aac_encoder_cfg_t::sbr_mode__int8_t"></a> <a id="structaac__encoder__cfg__t_1a9c9542cc5e8e5809f4271b0f774b3b6f"></a> int8\_t sbr\_mode
    :   sbr mode, refer to “AACENC\_SBR\_MODE” parameter description in aacenc\_lib.h

    <a id="_CPPv4N17aac_encoder_cfg_t14granule_lengthE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t14granule_lengthE"></a> <a id="_CPPv2N17aac_encoder_cfg_t14granule_lengthE"></a> <a id="aac_encoder_cfg_t::granule_length__uint32_t"></a> <a id="structaac__encoder__cfg__t_1aa6c00d8a3f6e719284baa2c805ab8e76"></a> uint32\_t granule\_length
    :   audio frame length in samples, refer to “AACENC\_GRANULE\_LENGTH” parameter description in aacenc\_lib.h

    <a id="_CPPv4N17aac_encoder_cfg_t9chl_orderE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t9chl_orderE"></a> <a id="_CPPv2N17aac_encoder_cfg_t9chl_orderE"></a> <a id="aac_encoder_cfg_t::chl_order__uint8_t"></a> <a id="structaac__encoder__cfg__t_1a1b9809fc2f9e3c55a48b43ac88f33105"></a> uint8\_t chl\_order
    :   Input audio data channel ordering scheme, refer to “AACENC\_CHANNELORDER” parameter description in aacenc\_lib.h

    <a id="_CPPv4N17aac_encoder_cfg_t14afterburner_enE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t14afterburner_enE"></a> <a id="_CPPv2N17aac_encoder_cfg_t14afterburner_enE"></a> <a id="aac_encoder_cfg_t::afterburner_en__uint8_t"></a> <a id="structaac__encoder__cfg__t_1a4568df9b62a11b8ce552ac7b38f723fd"></a> uint8\_t afterburner\_en
    :   afterburner feature enable, refer to “AACENC\_AFTERBURNER” parameter description in aacenc\_lib.h

    <a id="_CPPv4N17aac_encoder_cfg_t14transport_typeE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t14transport_typeE"></a> <a id="_CPPv2N17aac_encoder_cfg_t14transport_typeE"></a> <a id="aac_encoder_cfg_t::transport_type__uint8_t"></a> <a id="structaac__encoder__cfg__t_1af9c568f7d9836ee9674a3fca8ea9f8de"></a> uint8\_t transport\_type
    :   Transport type, refer to “AACENC\_TRANSMUX” parameter description in aacenc\_lib.h

    <a id="_CPPv4N17aac_encoder_cfg_t10buffer_lenE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t10buffer_lenE"></a> <a id="_CPPv2N17aac_encoder_cfg_t10buffer_lenE"></a> <a id="aac_encoder_cfg_t::buffer_len__i"></a> <a id="structaac__encoder__cfg__t_1a35c4763e44ccb81e748482be9e77ab9f"></a> int buffer\_len
    :   Buffer length use for aac Element

    <a id="_CPPv4N17aac_encoder_cfg_t11in_pool_lenE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t11in_pool_lenE"></a> <a id="_CPPv2N17aac_encoder_cfg_t11in_pool_lenE"></a> <a id="aac_encoder_cfg_t::in_pool_len__uint32_t"></a> <a id="structaac__encoder__cfg__t_1a8030e209692e14570086a53ab48cc4e7"></a> uint32\_t in\_pool\_len
    :   input data pool size(byte), save data if the valid data in pool is less than one frame

    <a id="_CPPv4N17aac_encoder_cfg_t14out_buffer_lenE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t14out_buffer_lenE"></a> <a id="_CPPv2N17aac_encoder_cfg_t14out_buffer_lenE"></a> <a id="aac_encoder_cfg_t::out_buffer_len__uint32_t"></a> <a id="structaac__encoder__cfg__t_1a0a3825f08522c49e2b184fa154832130"></a> uint32\_t out\_buffer\_len
    :   one frame data size(byte) of output aac data, less than one frame size

    <a id="_CPPv4N17aac_encoder_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N17aac_encoder_cfg_t14out_block_sizeE"></a> <a id="aac_encoder_cfg_t::out_block_size__i"></a> <a id="structaac__encoder__cfg__t_1a24c9efa1984c1db976d893b364421e97"></a> int out\_block\_size
    :   Size of output block, at least larger than the size of one frame of output aac data

    <a id="_CPPv4N17aac_encoder_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t13out_block_numE"></a> <a id="_CPPv2N17aac_encoder_cfg_t13out_block_numE"></a> <a id="aac_encoder_cfg_t::out_block_num__i"></a> <a id="structaac__encoder__cfg__t_1aa013d5da95d4e4287406d887c15ebcf0"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N17aac_encoder_cfg_t10task_stackE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t10task_stackE"></a> <a id="_CPPv2N17aac_encoder_cfg_t10task_stackE"></a> <a id="aac_encoder_cfg_t::task_stack__i"></a> <a id="structaac__encoder__cfg__t_1a754d632488269d0b8a195883316dad5b"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N17aac_encoder_cfg_t9task_coreE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t9task_coreE"></a> <a id="_CPPv2N17aac_encoder_cfg_t9task_coreE"></a> <a id="aac_encoder_cfg_t::task_core__i"></a> <a id="structaac__encoder__cfg__t_1a39645c33168300ba7afb6aaabe9d30b9"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N17aac_encoder_cfg_t9task_prioE"></a>

    <a id="_CPPv3N17aac_encoder_cfg_t9task_prioE"></a> <a id="_CPPv2N17aac_encoder_cfg_t9task_prioE"></a> <a id="aac_encoder_cfg_t::task_prio__i"></a> <a id="structaac__encoder__cfg__t_1aff03972c54afa12044773cf6f19b2103"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.AAC_ENCODER_CHL_NUM"></a>

<a id="aac__encoder_8h_1a4e4bed2ff57ac2151de7a3b380af42f4"></a> AAC\_ENCODER\_CHL\_NUM

<a id="c.AAC_ENCODER_SAMP_RATE"></a>

<a id="aac__encoder_8h_1a8f2072d769be60fe00ed517e57282536"></a> AAC\_ENCODER\_SAMP\_RATE

<a id="c.AAC_ENCODER_BITS"></a>

<a id="aac__encoder_8h_1a47e91e7e18ee22df362810329d491a10"></a> AAC\_ENCODER\_BITS

<a id="c.AAC_ENCODER_MODULES"></a>

<a id="aac__encoder_8h_1ae2d134d651b19122ab9028b579e4e67b"></a> AAC\_ENCODER\_MODULES

<a id="c.AAC_ENCODER_AOT"></a>

<a id="aac__encoder_8h_1ae8fb59cdf242e731a8fc96c058b0f59f"></a> AAC\_ENCODER\_AOT

<a id="c.AAC_ENCODER_BITRATE"></a>

<a id="aac__encoder_8h_1a90fdc0777d03ca565506c7325b1f8a5e"></a> AAC\_ENCODER\_BITRATE

<a id="c.AAC_ENCODER_BITRATE_MODE"></a>

<a id="aac__encoder_8h_1a68856e7d3eeaec815b1a42c5d96f2959"></a> AAC\_ENCODER\_BITRATE\_MODE

<a id="c.AAC_ENCODER_SBR_MODE"></a>

<a id="aac__encoder_8h_1af5a6385c6a4ab3c13a4cc58bce54c1af"></a> AAC\_ENCODER\_SBR\_MODE

<a id="c.AAC_ENCODER_GRANULE_LENGTH"></a>

<a id="aac__encoder_8h_1a098d07df9af292c5c298379d77deda96"></a> AAC\_ENCODER\_GRANULE\_LENGTH

<a id="c.AAC_ENCODER_CHL_ORDER"></a>

<a id="aac__encoder_8h_1a6b9fb2eb2a7e11aa1f3ec0aba8e3fb43"></a> AAC\_ENCODER\_CHL\_ORDER

<a id="c.AAC_ENCODER_AFTERBURNER_EN"></a>

<a id="aac__encoder_8h_1a5c4937503ccb50cad441f6db7773b372"></a> AAC\_ENCODER\_AFTERBURNER\_EN

<a id="c.AAC_ENCODER_TRANSPORT_TYPE"></a>

<a id="aac__encoder_8h_1ad450d2ff642bdb8905c87482dc02cd62"></a> AAC\_ENCODER\_TRANSPORT\_TYPE

<a id="c.AAC_ENCODER_BUFFER_LEN"></a>

<a id="aac__encoder_8h_1a1a7098f653e42ae11be7e6edd0270681"></a> AAC\_ENCODER\_BUFFER\_LEN

<a id="c.AAC_ENCODER_IN_POOL_LEN"></a>

<a id="aac__encoder_8h_1af33f9b7c5bcca31b41b77ea41ccc1dd4"></a> AAC\_ENCODER\_IN\_POOL\_LEN

<a id="c.AAC_ENCODER_OUT_BUFFER_LEN"></a>

<a id="aac__encoder_8h_1ad509a174bd74bdff127075d7de836a91"></a> AAC\_ENCODER\_OUT\_BUFFER\_LEN

<a id="c.AAC_ENCODER_OUT_BLOCK_SIZE"></a>

<a id="aac__encoder_8h_1a0226074385ddeb95f2c86bf97789d765"></a> AAC\_ENCODER\_OUT\_BLOCK\_SIZE

<a id="c.AAC_ENCODER_OUT_BLOCK_NUM"></a>

<a id="aac__encoder_8h_1a8c713b0258d86cf1b4bb89ad9ffd414d"></a> AAC\_ENCODER\_OUT\_BLOCK\_NUM

<a id="c.AAC_ENCODER_TASK_STACK"></a>

<a id="aac__encoder_8h_1a560d636608abd9f4a19a3091a81084e6"></a> AAC\_ENCODER\_TASK\_STACK

<a id="c.AAC_ENCODER_TASK_CORE"></a>

<a id="aac__encoder_8h_1a80fee873ba8c4e74201d7a4955444385"></a> AAC\_ENCODER\_TASK\_CORE

<a id="c.AAC_ENCODER_TASK_PRIO"></a>

<a id="aac__encoder_8h_1af5541131a2fc7d78cad526371c5b0e57"></a> AAC\_ENCODER\_TASK\_PRIO

<a id="c.DEFAULT_AAC_ENCODER_CONFIG"></a>

<a id="aac__encoder_8h_1a5d77334bba2e14677ffa2175bc53f5a0"></a> DEFAULT\_AAC\_ENCODER\_CONFIG()
