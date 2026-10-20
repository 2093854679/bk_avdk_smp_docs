---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/audio_development_kit/audio_streams/raw_stream.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="raw-stream"></a>

# Raw Stream

The raw stream reads/writes audio data from/into audio port.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [raw\_stream.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_audio/audio_streams/raw_stream.h)

<a id="functions"></a>

### Functions

<a id="_CPPv415raw_stream_initP16raw_stream_cfg_t"></a>

<a id="_CPPv315raw_stream_initP16raw_stream_cfg_t"></a> <a id="_CPPv215raw_stream_initP16raw_stream_cfg_t"></a> <a id="raw_stream_init__raw_stream_cfg_tP"></a> <a id="raw__stream_8h_1a9cc338f81b18b7183be78da4ab619e2a"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") raw\_stream\_init([raw\_stream\_cfg\_t](#_CPPv416raw_stream_cfg_t "raw_stream_cfg_t") \*cfg)
:   Initialize RAW stream.

    参数
    :   **cfg** – The RAW Stream configuration

    返回
    :   The audio element handle

<a id="_CPPv415raw_stream_read22audio_element_handle_tPci"></a>

<a id="_CPPv315raw_stream_read22audio_element_handle_tPci"></a> <a id="_CPPv215raw_stream_read22audio_element_handle_tPci"></a> <a id="raw_stream_read__audio_element_handle_t.cP.i"></a> <a id="raw__stream_8h_1aa6e50c5c182caf1b4677a1df7d642b1d"></a> int raw\_stream\_read([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") pipeline, char \*buffer, int buf\_size)
:   Read data from Stream.

    参数
    :   - **pipeline** – The audio pipeline handle
        - **buffer** – The buffer
        - **buf\_size** – Maximum number of bytes to be read.

    返回
    :   Number of bytes actually read.

<a id="_CPPv416raw_stream_write22audio_element_handle_tPci"></a>

<a id="_CPPv316raw_stream_write22audio_element_handle_tPci"></a> <a id="_CPPv216raw_stream_write22audio_element_handle_tPci"></a> <a id="raw_stream_write__audio_element_handle_t.cP.i"></a> <a id="raw__stream_8h_1a2350a09a02f4790465ff188c4df6243e"></a> int raw\_stream\_write([audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") pipeline, char \*buffer, int buf\_size)
:   Write data to Stream.

    参数
    :   - **pipeline** – The audio pipeline handle
        - **buffer** – The buffer
        - **buf\_size** – Number of bytes to write

    返回
    :   Number of bytes written

<a id="structures"></a>

### Structures

<a id="_CPPv416raw_stream_cfg_t"></a>

<a id="_CPPv316raw_stream_cfg_t"></a> <a id="_CPPv216raw_stream_cfg_t"></a> <a id="raw_stream_cfg_t"></a> <a id="structraw__stream__cfg__t"></a> struct raw\_stream\_cfg\_t
:   RAW stream configuration.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16raw_stream_cfg_t4typeE"></a>

    <a id="_CPPv3N16raw_stream_cfg_t4typeE"></a> <a id="_CPPv2N16raw_stream_cfg_t4typeE"></a> <a id="raw_stream_cfg_t::type__audio_stream_type_t"></a> <a id="structraw__stream__cfg__t_1a05be3c8c013109a3f62dd578e6efc44f"></a> [audio\_stream\_type\_t](../audio_pipeline/audio_types.md#_CPPv419audio_stream_type_t "audio_stream_type_t") type
    :   Type of stream

    <a id="_CPPv4N16raw_stream_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N16raw_stream_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N16raw_stream_cfg_t14out_block_sizeE"></a> <a id="raw_stream_cfg_t::out_block_size__i"></a> <a id="structraw__stream__cfg__t_1aae25ca27b4a716b60cb59170d437bd06"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N16raw_stream_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N16raw_stream_cfg_t13out_block_numE"></a> <a id="_CPPv2N16raw_stream_cfg_t13out_block_numE"></a> <a id="raw_stream_cfg_t::out_block_num__i"></a> <a id="structraw__stream__cfg__t_1af9eb840db06bf2e91a8f92782c02f1dc"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N16raw_stream_cfg_t16output_port_typeE"></a>

    <a id="_CPPv3N16raw_stream_cfg_t16output_port_typeE"></a> <a id="_CPPv2N16raw_stream_cfg_t16output_port_typeE"></a> <a id="raw_stream_cfg_t::output_port_type__port_type_t"></a> <a id="structraw__stream__cfg__t_1a9407b61bd1a1fa86075cc1e4fe302d15"></a> [port\_type\_t](../audio_pipeline/audio_port.md#_CPPv411port_type_t "port_type_t") output\_port\_type
    :   Output port type

<a id="macros"></a>

### Macros

<a id="c.RAW_STREAM_OUT_BLOCK_SIZE"></a>

<a id="raw__stream_8h_1acaca0d6ffc1a6d25673bcd7ec7e7b9dc"></a> RAW\_STREAM\_OUT\_BLOCK\_SIZE

<a id="c.RAW_STREAM_OUT_BLOCK_NUM"></a>

<a id="raw__stream_8h_1ae830e08f219b6f82c9724a5c19668ae9"></a> RAW\_STREAM\_OUT\_BLOCK\_NUM

<a id="c.RAW_STREAM_CFG_DEFAULT"></a>

<a id="raw__stream_8h_1acfa26f0885776f745f09ad91e61e2ada"></a> RAW\_STREAM\_CFG\_DEFAULT()

<a id="c.DEFAULT_RAW_STREAM_CONFIG"></a>

<a id="raw__stream_8h_1a65fc409fa03ddbd91ace118c390062ef"></a> DEFAULT\_RAW\_STREAM\_CONFIG()
