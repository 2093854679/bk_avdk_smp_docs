---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/audio_development_kit/audio_algorithms/aec_algorithm.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="aec-algorithm"></a>

# AEC Algorithm

Process the data collected by the microphone and eliminate the echo in the data.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [aec\_algorithm.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_audio/audio_algorithms/aec_algorithm.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418aec_algorithm_initP19aec_algorithm_cfg_t"></a>

<a id="_CPPv318aec_algorithm_initP19aec_algorithm_cfg_t"></a> <a id="_CPPv218aec_algorithm_initP19aec_algorithm_cfg_t"></a> <a id="aec_algorithm_init__aec_algorithm_cfg_tP"></a> <a id="aec__algorithm_8h_1aec383982e8c95e6ea2c0058038761576"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") aec\_algorithm\_init([aec\_algorithm\_cfg\_t](#_CPPv419aec_algorithm_cfg_t "aec_algorithm_cfg_t") \*config)
:   Create a Aec algorithm of Audio Element to echo cancellation.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The audio element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv49aec_cfg_t"></a>

<a id="_CPPv39aec_cfg_t"></a> <a id="_CPPv29aec_cfg_t"></a> <a id="aec_cfg_t"></a> <a id="structaec__cfg__t"></a> struct aec\_cfg\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N9aec_cfg_t4modeE"></a>

    <a id="_CPPv3N9aec_cfg_t4modeE"></a> <a id="_CPPv2N9aec_cfg_t4modeE"></a> <a id="aec_cfg_t::mode__aec_mode_t"></a> <a id="structaec__cfg__t_1a737e8bdf2cc72649a09b526e35cbd925"></a> [aec\_mode\_t](#_CPPv410aec_mode_t "aec_mode_t") mode
    :   aec work mode: hardware mode or software mode

    <a id="_CPPv4N9aec_cfg_t2fsE"></a>

    <a id="_CPPv3N9aec_cfg_t2fsE"></a> <a id="_CPPv2N9aec_cfg_t2fsE"></a> <a id="aec_cfg_t::fs__uint32_t"></a> <a id="structaec__cfg__t_1a1a04b7dc10d3681c2a8fc785110777b6"></a> uint32\_t fs
    :   Sample rate (8000 or 16000\)

    <a id="_CPPv4N9aec_cfg_t12delay_pointsE"></a>

    <a id="_CPPv3N9aec_cfg_t12delay_pointsE"></a> <a id="_CPPv2N9aec_cfg_t12delay_pointsE"></a> <a id="aec_cfg_t::delay_points__uint32_t"></a> <a id="structaec__cfg__t_1a0d17d5b9c9034f3968b66a160b5f289c"></a> uint32\_t delay\_points
    :   Delay sampling points between reference signal and source signal

    <a id="_CPPv4N9aec_cfg_t8ec_depthE"></a>

    <a id="_CPPv3N9aec_cfg_t8ec_depthE"></a> <a id="_CPPv2N9aec_cfg_t8ec_depthE"></a> <a id="aec_cfg_t::ec_depth__uint32_t"></a> <a id="structaec__cfg__t_1af3948ee291967341ee6d2e58c0b0a80d"></a> uint32\_t ec\_depth
    :   recommended value range: 1\~50, the greater the echo, the greater the value setting

    <a id="_CPPv4N9aec_cfg_t7TxRxThrE"></a>

    <a id="_CPPv3N9aec_cfg_t7TxRxThrE"></a> <a id="_CPPv2N9aec_cfg_t7TxRxThrE"></a> <a id="aec_cfg_t::TxRxThr__uint32_t"></a> <a id="structaec__cfg__t_1ad9fd9149a53b4ef4cef70436c2f528e1"></a> uint32\_t TxRxThr
    :   the max amplitude of rx audio data

    <a id="_CPPv4N9aec_cfg_t7TxRxFlrE"></a>

    <a id="_CPPv3N9aec_cfg_t7TxRxFlrE"></a> <a id="_CPPv2N9aec_cfg_t7TxRxFlrE"></a> <a id="aec_cfg_t::TxRxFlr__uint32_t"></a> <a id="structaec__cfg__t_1a4e07bbe0c5213749f60bb6047855e81c"></a> uint32\_t TxRxFlr
    :   the min amplitude of rx audio data

    <a id="_CPPv4N9aec_cfg_t9ref_scaleE"></a>

    <a id="_CPPv3N9aec_cfg_t9ref_scaleE"></a> <a id="_CPPv2N9aec_cfg_t9ref_scaleE"></a> <a id="aec_cfg_t::ref_scale__uint8_t"></a> <a id="structaec__cfg__t_1a7117438aa4f0a44692fdd5b59d1e7fb4"></a> uint8\_t ref\_scale
    :   value range:0,1,2, the greater the signal amplitude, the greater the setting

    <a id="_CPPv4N9aec_cfg_t8ns_levelE"></a>

    <a id="_CPPv3N9aec_cfg_t8ns_levelE"></a> <a id="_CPPv2N9aec_cfg_t8ns_levelE"></a> <a id="aec_cfg_t::ns_level__uint8_t"></a> <a id="structaec__cfg__t_1a1713120c19e8d68d27b44f57815feab3"></a> uint8\_t ns\_level
    :   recommended value range: 1\~8, the lower the noise, the lower the level

    <a id="_CPPv4N9aec_cfg_t7ns_paraE"></a>

    <a id="_CPPv3N9aec_cfg_t7ns_paraE"></a> <a id="_CPPv2N9aec_cfg_t7ns_paraE"></a> <a id="aec_cfg_t::ns_para__uint8_t"></a> <a id="structaec__cfg__t_1a0ef23789cafd55959e0c0dd1f21785f1"></a> uint8\_t ns\_para
    :   value range:0,1,2, the lower the noise, the lower the level, the default valude is recommended

<a id="_CPPv419aec_algorithm_cfg_t"></a>

<a id="_CPPv319aec_algorithm_cfg_t"></a> <a id="_CPPv219aec_algorithm_cfg_t"></a> <a id="aec_algorithm_cfg_t"></a> <a id="structaec__algorithm__cfg__t"></a> struct aec\_algorithm\_cfg\_t
:   AEC algorithm configurations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19aec_algorithm_cfg_t10task_stackE"></a>

    <a id="_CPPv3N19aec_algorithm_cfg_t10task_stackE"></a> <a id="_CPPv2N19aec_algorithm_cfg_t10task_stackE"></a> <a id="aec_algorithm_cfg_t::task_stack__i"></a> <a id="structaec__algorithm__cfg__t_1a53eefa61558bcfe04f49d0f45c8dff91"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N19aec_algorithm_cfg_t9task_coreE"></a>

    <a id="_CPPv3N19aec_algorithm_cfg_t9task_coreE"></a> <a id="_CPPv2N19aec_algorithm_cfg_t9task_coreE"></a> <a id="aec_algorithm_cfg_t::task_core__i"></a> <a id="structaec__algorithm__cfg__t_1a3680a25a0d62b6ed2d5ea68c1d266b77"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N19aec_algorithm_cfg_t9task_prioE"></a>

    <a id="_CPPv3N19aec_algorithm_cfg_t9task_prioE"></a> <a id="_CPPv2N19aec_algorithm_cfg_t9task_prioE"></a> <a id="aec_algorithm_cfg_t::task_prio__i"></a> <a id="structaec__algorithm__cfg__t_1a2cb701523f8b83e2c60512a8ca4145a1"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

    <a id="_CPPv4N19aec_algorithm_cfg_t7aec_cfgE"></a>

    <a id="_CPPv3N19aec_algorithm_cfg_t7aec_cfgE"></a> <a id="_CPPv2N19aec_algorithm_cfg_t7aec_cfgE"></a> <a id="aec_algorithm_cfg_t::aec_cfg__aec_cfg_t"></a> <a id="structaec__algorithm__cfg__t_1a49361c4e0567e8b37b20b1e5d947b538"></a> [aec\_cfg\_t](#_CPPv49aec_cfg_t "aec_cfg_t") aec\_cfg
    :   aec config

    <a id="_CPPv4N19aec_algorithm_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N19aec_algorithm_cfg_t13out_block_numE"></a> <a id="_CPPv2N19aec_algorithm_cfg_t13out_block_numE"></a> <a id="aec_algorithm_cfg_t::out_block_num__i"></a> <a id="structaec__algorithm__cfg__t_1aea84a54c546a0ae5b291d4f33938f032"></a> int out\_block\_num
    :   Number of output block, the size of block is frame size of 20ms audio data

    <a id="_CPPv4N19aec_algorithm_cfg_t18multi_out_port_numE"></a>

    <a id="_CPPv3N19aec_algorithm_cfg_t18multi_out_port_numE"></a> <a id="_CPPv2N19aec_algorithm_cfg_t18multi_out_port_numE"></a> <a id="aec_algorithm_cfg_t::multi_out_port_num__i"></a> <a id="structaec__algorithm__cfg__t_1a57cb044f2d6240dc33c58e831354d1ef"></a> int multi\_out\_port\_num
    :   The number of multiple output audio port

<a id="macros"></a>

### Macros

<a id="c.AEC_DELAY_SAMPLE_POINTS_MAX"></a>

<a id="aec__algorithm_8h_1a051646955a19ae9b9ba0ab229a8b01fd"></a> AEC\_DELAY\_SAMPLE\_POINTS\_MAX

<a id="c.AEC_ALGORITHM_TASK_STACK"></a>

<a id="aec__algorithm_8h_1a53b109c172bcc6c4a8cceb991ad199f7"></a> AEC\_ALGORITHM\_TASK\_STACK

<a id="c.AEC_ALGORITHM_TASK_CORE"></a>

<a id="aec__algorithm_8h_1a3715e60aa0f4afeb201cc78713d71de3"></a> AEC\_ALGORITHM\_TASK\_CORE

<a id="c.AEC_ALGORITHM_TASK_PRIO"></a>

<a id="aec__algorithm_8h_1adc917df89c3cef675b0f1af7c02c1316"></a> AEC\_ALGORITHM\_TASK\_PRIO

<a id="c.AEC_ALGORITHM_OUT_BLOCK_NUM"></a>

<a id="aec__algorithm_8h_1aeb4dea34045e9a4109ee87c3553df667"></a> AEC\_ALGORITHM\_OUT\_BLOCK\_NUM

<a id="c.AEC_ALGORITHM_FS"></a>

<a id="aec__algorithm_8h_1a72e292e74c7f3cb8e1713a8535f3bbf3"></a> AEC\_ALGORITHM\_FS

<a id="c.AEC_DELAY_POINTS"></a>

<a id="aec__algorithm_8h_1ad336e3d37ad94913e0de24a7cdb37002"></a> AEC\_DELAY\_POINTS

<a id="c.AEC_ALGORITHM_EC_DEPTH"></a>

<a id="aec__algorithm_8h_1ae6782489e5d8fbaa06226e809c8259f5"></a> AEC\_ALGORITHM\_EC\_DEPTH

<a id="c.AEC_ALGORITHM_TXRXTHR"></a>

<a id="aec__algorithm_8h_1a23ee03e3ae6d06662b5439aba9efc560"></a> AEC\_ALGORITHM\_TXRXTHR

<a id="c.AEC_ALGORITHM_TXRXFLR"></a>

<a id="aec__algorithm_8h_1a6157cccb6e462462907f7b3f8718497b"></a> AEC\_ALGORITHM\_TXRXFLR

<a id="c.AEC_ALGORITHM_REF_SCALE"></a>

<a id="aec__algorithm_8h_1a3a0d90e01e8c318e5e0aa01a7eaf04a6"></a> AEC\_ALGORITHM\_REF\_SCALE

<a id="c.AEC_ALGORITHM_NS_LEVEL"></a>

<a id="aec__algorithm_8h_1a1e5a1d3f4dfb9acd0acc5d069aea3917"></a> AEC\_ALGORITHM\_NS\_LEVEL

<a id="c.AEC_ALGORITHM_NS_PARA"></a>

<a id="aec__algorithm_8h_1a06c8a28ab18fcc31fadd8507b4dfe1a5"></a> AEC\_ALGORITHM\_NS\_PARA

<a id="c.DEFAULT_AEC_ALGORITHM_CONFIG"></a>

<a id="aec__algorithm_8h_1a7ba701c027f8f341d7ec45f7ae07226f"></a> DEFAULT\_AEC\_ALGORITHM\_CONFIG()

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv410aec_mode_t"></a>

<a id="_CPPv310aec_mode_t"></a> <a id="_CPPv210aec_mode_t"></a> <a id="aec__algorithm_8h_1aa6193163470c4d1f0b6323ffd822fba2"></a> enum aec\_mode\_t
:   *Values:*

    <a id="_CPPv4N10aec_mode_t17AEC_MODE_HARDWAREE"></a>

    <a id="_CPPv3N10aec_mode_t17AEC_MODE_HARDWAREE"></a> <a id="_CPPv2N10aec_mode_t17AEC_MODE_HARDWAREE"></a> <a id="aec__algorithm_8h_1aa6193163470c4d1f0b6323ffd822fba2a17dbfc65754cdcd930a0284718fcf32e"></a> enumerator AEC\_MODE\_HARDWARE
    :   hardware mode: Hardware mode get source and reference signal through audio adc L and R channel. Audio adc L channel connect to mic, and collect source signal. Audio adc R channel connect to speaker, and collect reference signal.

    <a id="_CPPv4N10aec_mode_t17AEC_MODE_SOFTWAREE"></a>

    <a id="_CPPv3N10aec_mode_t17AEC_MODE_SOFTWAREE"></a> <a id="_CPPv2N10aec_mode_t17AEC_MODE_SOFTWAREE"></a> <a id="aec__algorithm_8h_1aa6193163470c4d1f0b6323ffd822fba2a473319a225612778dc1eb4e6bfddf13b"></a> enumerator AEC\_MODE\_SOFTWARE
    :   software mode: Software mode get source and reference signal through audio adc L and software writting. Audio adc L channel connect to mic, and collect source signal. Software write speaker data to input ringbuffer to support reference signal.
