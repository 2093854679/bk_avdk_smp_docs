---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_streams/array_stream.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="array-stream"></a>

# Array Stream

The array stream reads/writes audio data from/into array.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [array\_stream.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_streams/array_stream.h)

<a id="functions"></a>

### Functions

<a id="_CPPv417array_stream_initP18array_stream_cfg_t"></a>

<a id="_CPPv317array_stream_initP18array_stream_cfg_t"></a> <a id="_CPPv217array_stream_initP18array_stream_cfg_t"></a> <a id="array_stream_init__array_stream_cfg_tP"></a> <a id="array__stream_8h_1abd8b06006d57ac3d49886194b3a475c5"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") array\_stream\_init([array\_stream\_cfg\_t](#_CPPv418array_stream_cfg_t "array_stream_cfg_t") \*config)
:   Create a handle to an Audio Element to stream data from array to another Element or get data from other elements written to array, depending on the configuration the stream type, either AUDIO\_STREAM\_READER or AUDIO\_STREAM\_WRITER.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The Audio Element handle

        - Not NULL: success
        - NULL: failed

<a id="_CPPv421array_stream_set_data22audio_element_handle_tP7uint8_ti"></a>

<a id="_CPPv321array_stream_set_data22audio_element_handle_tP7uint8_ti"></a> <a id="_CPPv221array_stream_set_data22audio_element_handle_tP7uint8_ti"></a> <a id="array_stream_set_data__audio_element_handle_t.uint8_tP.i"></a> <a id="array__stream_8h_1afa376cce8f9fd5795d128d127172fd9b"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") array\_stream\_set\_data([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") array\_stream, uint8\_t \*array\_buf, int array\_size)
:   Set the array information for the array stream. This interface must be used to set the array and its length after the component is initialized and before it runs.

    参数
    :   - **array\_stream** – **\[in\]** The audio element handle of the array stream.
        - **array\_buf** – **\[in\]** Pointer to the array buffer.
        - **array\_size** – **\[in\]** Size of the array.

    返回
    :   Operation result

        - BK\_OK: Success
        - Other values: Failure

<a id="structures"></a>

### Structures

<a id="_CPPv418array_stream_cfg_t"></a>

<a id="_CPPv318array_stream_cfg_t"></a> <a id="_CPPv218array_stream_cfg_t"></a> <a id="array_stream_cfg_t"></a> <a id="structarray__stream__cfg__t"></a> struct array\_stream\_cfg\_t
:   ARRAY Stream configurations, if any entry is zero then the configuration will be set to default values.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18array_stream_cfg_t4typeE"></a>

    <a id="_CPPv3N18array_stream_cfg_t4typeE"></a> <a id="_CPPv2N18array_stream_cfg_t4typeE"></a> <a id="array_stream_cfg_t::type__audio_stream_type_t"></a> <a id="structarray__stream__cfg__t_1a43ed1a6dce6a6a0822677667c35485c6"></a> [audio\_stream\_type\_t](../audio_pipeline/audio_types.md#_CPPv419audio_stream_type_t "audio_stream_type_t") type
    :   Stream type

    <a id="_CPPv4N18array_stream_cfg_t10array_sizeE"></a>

    <a id="_CPPv3N18array_stream_cfg_t10array_sizeE"></a> <a id="_CPPv2N18array_stream_cfg_t10array_sizeE"></a> <a id="array_stream_cfg_t::array_size__uint32_t"></a> <a id="structarray__stream__cfg__t_1a74fa3945cc5c34de4ce4582e8d5b2134"></a> uint32\_t array\_size
    :   Array total size

    <a id="_CPPv4N18array_stream_cfg_t12array_offsetE"></a>

    <a id="_CPPv3N18array_stream_cfg_t12array_offsetE"></a> <a id="_CPPv2N18array_stream_cfg_t12array_offsetE"></a> <a id="array_stream_cfg_t::array_offset__uint32_t"></a> <a id="structarray__stream__cfg__t_1ae2afec3ac853125a9d662ea54c4397ef"></a> uint32\_t array\_offset
    :   Array offset

    <a id="_CPPv4N18array_stream_cfg_t6buf_szE"></a>

    <a id="_CPPv3N18array_stream_cfg_t6buf_szE"></a> <a id="_CPPv2N18array_stream_cfg_t6buf_szE"></a> <a id="array_stream_cfg_t::buf_sz__i"></a> <a id="structarray__stream__cfg__t_1ae3a77c509781cddad074febded47706b"></a> int buf\_sz
    :   Audio Element Buffer size

    <a id="_CPPv4N18array_stream_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N18array_stream_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N18array_stream_cfg_t14out_block_sizeE"></a> <a id="array_stream_cfg_t::out_block_size__i"></a> <a id="structarray__stream__cfg__t_1a0aa1c40199dc75551b61ef07054d87e3"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N18array_stream_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N18array_stream_cfg_t13out_block_numE"></a> <a id="_CPPv2N18array_stream_cfg_t13out_block_numE"></a> <a id="array_stream_cfg_t::out_block_num__i"></a> <a id="structarray__stream__cfg__t_1a3abb269426d4fd0103e6393966229159"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N18array_stream_cfg_t10task_stackE"></a>

    <a id="_CPPv3N18array_stream_cfg_t10task_stackE"></a> <a id="_CPPv2N18array_stream_cfg_t10task_stackE"></a> <a id="array_stream_cfg_t::task_stack__i"></a> <a id="structarray__stream__cfg__t_1a314b2c44885e2a7b90cca6815bf0eeb3"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N18array_stream_cfg_t9task_coreE"></a>

    <a id="_CPPv3N18array_stream_cfg_t9task_coreE"></a> <a id="_CPPv2N18array_stream_cfg_t9task_coreE"></a> <a id="array_stream_cfg_t::task_core__i"></a> <a id="structarray__stream__cfg__t_1aa6acc862d220dc2462006a2e4ae4132e"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N18array_stream_cfg_t9task_prioE"></a>

    <a id="_CPPv3N18array_stream_cfg_t9task_prioE"></a> <a id="_CPPv2N18array_stream_cfg_t9task_prioE"></a> <a id="array_stream_cfg_t::task_prio__i"></a> <a id="structarray__stream__cfg__t_1a5027b2e7a35e001ae7e18a24484e0a02"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.ARRAY_STREAM_BUF_SIZE"></a>

<a id="array__stream_8h_1a7f0771c700101448088d8038b1c8c694"></a> ARRAY\_STREAM\_BUF\_SIZE

<a id="c.ARRAY_STREAM_TASK_STACK"></a>

<a id="array__stream_8h_1af6a5babb44dbf30bf955cf252d6d9e81"></a> ARRAY\_STREAM\_TASK\_STACK

<a id="c.ARRAY_STREAM_TASK_CORE"></a>

<a id="array__stream_8h_1ae86d171ae83c434b4c99841ebc21fd4b"></a> ARRAY\_STREAM\_TASK\_CORE

<a id="c.ARRAY_STREAM_TASK_PRIO"></a>

<a id="array__stream_8h_1a1becf34a94b7b3757100e429f57ee20a"></a> ARRAY\_STREAM\_TASK\_PRIO

<a id="c.ARRAY_STREAM_OUT_BLOCK_SIZE"></a>

<a id="array__stream_8h_1a1eda429f8913b6179be6f0ef4179c1d4"></a> ARRAY\_STREAM\_OUT\_BLOCK\_SIZE

<a id="c.ARRAY_STREAM_OUT_BLOCK_NUM"></a>

<a id="array__stream_8h_1a1946faa42c6106544057824a4f9ffbc8"></a> ARRAY\_STREAM\_OUT\_BLOCK\_NUM

<a id="c.DEFAULT_ARRAY_STREAM_CONFIG"></a>

<a id="array__stream_8h_1a0d5dda676573641db09573bcbe4a2ce9"></a> DEFAULT\_ARRAY\_STREAM\_CONFIG()
