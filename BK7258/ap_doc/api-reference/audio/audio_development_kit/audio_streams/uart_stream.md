---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_streams/uart_stream.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="uart-stream"></a>

# UART Stream

The UART stream reads/writes audio data from/into UART.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [uart\_stream.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_streams/uart_stream.h)

<a id="functions"></a>

### Functions

<a id="_CPPv416uart_stream_initP17uart_stream_cfg_t"></a>

<a id="_CPPv316uart_stream_initP17uart_stream_cfg_t"></a> <a id="_CPPv216uart_stream_initP17uart_stream_cfg_t"></a> <a id="uart_stream_init__uart_stream_cfg_tP"></a> <a id="uart__stream_8h_1a8b207c6af6e1a19e6f37c188e2f7b6ac"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") uart\_stream\_init([uart\_stream\_cfg\_t](#_CPPv417uart_stream_cfg_t "uart_stream_cfg_t") \*config)
:   Create a handle to an Audio Element to stream data to another Element.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The Audio Element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv417uart_stream_cfg_t"></a>

<a id="_CPPv317uart_stream_cfg_t"></a> <a id="_CPPv217uart_stream_cfg_t"></a> <a id="uart_stream_cfg_t"></a> <a id="structuart__stream__cfg__t"></a> struct uart\_stream\_cfg\_t
:   Uart Stream configurations, if any entry is zero then the configuration will be set to default values.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17uart_stream_cfg_t7uart_idE"></a>

    <a id="_CPPv3N17uart_stream_cfg_t7uart_idE"></a> <a id="_CPPv2N17uart_stream_cfg_t7uart_idE"></a> <a id="uart_stream_cfg_t::uart_id__uint8_t"></a> <a id="structuart__stream__cfg__t_1a5435fa70b7bd56e13d9c1a3f0f0b85e2"></a> uint8\_t uart\_id
    :   Uart id

    <a id="_CPPv4N17uart_stream_cfg_t9baud_rateE"></a>

    <a id="_CPPv3N17uart_stream_cfg_t9baud_rateE"></a> <a id="_CPPv2N17uart_stream_cfg_t9baud_rateE"></a> <a id="uart_stream_cfg_t::baud_rate__uint32_t"></a> <a id="structuart__stream__cfg__t_1a37e009403a41da5ce5ac24b8011f0320"></a> uint32\_t baud\_rate
    :   uart baud rate

    <a id="_CPPv4N17uart_stream_cfg_t4typeE"></a>

    <a id="_CPPv3N17uart_stream_cfg_t4typeE"></a> <a id="_CPPv2N17uart_stream_cfg_t4typeE"></a> <a id="uart_stream_cfg_t::type__audio_stream_type_t"></a> <a id="structuart__stream__cfg__t_1aaa616a34b016c5c6bfc3f559bd106b66"></a> [audio\_stream\_type\_t](../audio_pipeline/audio_types.md#_CPPv419audio_stream_type_t "audio_stream_type_t") type
    :   Type of stream

    <a id="_CPPv4N17uart_stream_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N17uart_stream_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N17uart_stream_cfg_t14out_block_sizeE"></a> <a id="uart_stream_cfg_t::out_block_size__i"></a> <a id="structuart__stream__cfg__t_1ae4c29ff0e9a197199b6b8e2935795cba"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N17uart_stream_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N17uart_stream_cfg_t13out_block_numE"></a> <a id="_CPPv2N17uart_stream_cfg_t13out_block_numE"></a> <a id="uart_stream_cfg_t::out_block_num__i"></a> <a id="structuart__stream__cfg__t_1a95d220f900d83e7467fdf343777228bd"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N17uart_stream_cfg_t10buffer_lenE"></a>

    <a id="_CPPv3N17uart_stream_cfg_t10buffer_lenE"></a> <a id="_CPPv2N17uart_stream_cfg_t10buffer_lenE"></a> <a id="uart_stream_cfg_t::buffer_len__i"></a> <a id="structuart__stream__cfg__t_1a488f66419c6c16673444ae3eafc48e32"></a> int buffer\_len
    :   Size of read every time

    <a id="_CPPv4N17uart_stream_cfg_t10task_stackE"></a>

    <a id="_CPPv3N17uart_stream_cfg_t10task_stackE"></a> <a id="_CPPv2N17uart_stream_cfg_t10task_stackE"></a> <a id="uart_stream_cfg_t::task_stack__i"></a> <a id="structuart__stream__cfg__t_1a0c14c6e9d380f7c13d0a49571d92b889"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N17uart_stream_cfg_t9task_coreE"></a>

    <a id="_CPPv3N17uart_stream_cfg_t9task_coreE"></a> <a id="_CPPv2N17uart_stream_cfg_t9task_coreE"></a> <a id="uart_stream_cfg_t::task_core__i"></a> <a id="structuart__stream__cfg__t_1a918ffac7a2fcd9a40b478bd749189996"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N17uart_stream_cfg_t9task_prioE"></a>

    <a id="_CPPv3N17uart_stream_cfg_t9task_prioE"></a> <a id="_CPPv2N17uart_stream_cfg_t9task_prioE"></a> <a id="uart_stream_cfg_t::task_prio__i"></a> <a id="structuart__stream__cfg__t_1afb5c32409ae878373d52d172f54fbecb"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.UART_STREAM_UART_ID"></a>

<a id="uart__stream_8h_1a14c157fc7a624d771cd5d13cd65c429e"></a> UART\_STREAM\_UART\_ID

<a id="c.UART_STREAM_BAUD_RATE"></a>

<a id="uart__stream_8h_1a3d2a2e5f6404c34bb80540d0b4fadb06"></a> UART\_STREAM\_BAUD\_RATE

<a id="c.UART_STREAM_BLOCK_SIZE"></a>

<a id="uart__stream_8h_1a8abac174bf5cdd6ec99c052cf157034b"></a> UART\_STREAM\_BLOCK\_SIZE

<a id="c.UART_STREAM_BLOCK_NUM"></a>

<a id="uart__stream_8h_1a845c032f80f25d5b932b8028337856b3"></a> UART\_STREAM\_BLOCK\_NUM

<a id="c.UART_STREAM_BUFFER_LEN"></a>

<a id="uart__stream_8h_1ae28c065ca02e598850fca136ba86999b"></a> UART\_STREAM\_BUFFER\_LEN

<a id="c.UART_STREAM_TASK_STACK"></a>

<a id="uart__stream_8h_1a888ce89feac9be1804425c4ae1daedc2"></a> UART\_STREAM\_TASK\_STACK

<a id="c.UART_STREAM_TASK_CORE"></a>

<a id="uart__stream_8h_1a64f3bac80fcb4269c80b9811cc078e68"></a> UART\_STREAM\_TASK\_CORE

<a id="c.UART_STREAM_TASK_PRIO"></a>

<a id="uart__stream_8h_1abfee61a2067b1fc3be58793e5ee45362"></a> UART\_STREAM\_TASK\_PRIO

<a id="c.UART_STREAM_CFG_DEFAULT"></a>

<a id="uart__stream_8h_1a2bcc000b2ff028ef9b85fc88e0e265b3"></a> UART\_STREAM\_CFG\_DEFAULT()

<a id="c.DEFAULT_UART_STREAM_CONFIG"></a>

<a id="uart__stream_8h_1a76f72155d0b8bf4b1b8e14372a97e989"></a> DEFAULT\_UART\_STREAM\_CONFIG()
