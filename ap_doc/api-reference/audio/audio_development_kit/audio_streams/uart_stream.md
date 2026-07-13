# UART Stream


The UART stream reads/writes audio data from/into UART.


## API Reference


### Header File


- [bk_audio/audio_streams/uart_stream.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/uart_stream.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/uart_stream.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") uart_stream_init([uart_stream_cfg_t](#_CPPv417uart_stream_cfg_t "uart_stream_cfg_t") *config)
:   Create a handle to an Audio Element to stream data to another Element.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The Audio Element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct uart_stream_cfg_t
:   Uart Stream configurations, if any entry is zero then the configuration will be set to default values.

    Public Members

    uint8_t uart_id
    :   Uart id

    uint32_t baud_rate
    :   uart baud rate

    [audio_stream_type_t](../audio_pipeline/audio_types.md#_CPPv419audio_stream_type_t "audio_stream_type_t") type
    :   Type of stream

    int out_block_size
    :   Size of output block

    int out_block_num
    :   Number of output block

    int buffer_len
    :   Size of read every time

    int task_stack
    :   Task stack size

    int task_core
    :   Task running in core (0 or 1)

    int task_prio
    :   Task priority (based on freeRTOS priority)


### Macros

UART_STREAM_UART_ID

UART_STREAM_BAUD_RATE

UART_STREAM_BLOCK_SIZE

UART_STREAM_BLOCK_NUM

UART_STREAM_BUFFER_LEN

UART_STREAM_TASK_STACK

UART_STREAM_TASK_CORE

UART_STREAM_TASK_PRIO

UART_STREAM_CFG_DEFAULT()

DEFAULT_UART_STREAM_CONFIG()
