# Raw Stream


The raw stream reads/writes audio data from/into audio port.


## API Reference


### Header File


- [bk_audio/audio_streams/raw_stream.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/raw_stream.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/raw_stream.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") raw_stream_init([raw_stream_cfg_t](#_CPPv416raw_stream_cfg_t "raw_stream_cfg_t") *cfg)
:   Initialize RAW stream.

    参数
    :   **cfg** – The RAW Stream configuration

    返回
    :   The audio element handle

int raw_stream_read([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") pipeline, char *buffer, int buf_size)
:   Read data from Stream.

    参数
    :   - **pipeline** – The audio pipeline handle

        - **buffer** – The buffer

        - **buf_size** – Maximum number of bytes to be read.

    返回
    :   Number of bytes actually read.

int raw_stream_write([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") pipeline, char *buffer, int buf_size)
:   Write data to Stream.

    参数
    :   - **pipeline** – The audio pipeline handle

        - **buffer** – The buffer

        - **buf_size** – Number of bytes to write

    返回
    :   Number of bytes written


### Structures

struct raw_stream_cfg_t
:   RAW stream configuration.

    Public Members

    [audio_stream_type_t](../audio_pipeline/audio_types.md#_CPPv419audio_stream_type_t "audio_stream_type_t") type
    :   Type of stream

    int out_block_size
    :   Size of output block

    int out_block_num
    :   Number of output block

    [port_type_t](../audio_pipeline/audio_port.md#_CPPv411port_type_t "port_type_t") output_port_type
    :   Output port type


### Macros

RAW_STREAM_OUT_BLOCK_SIZE

RAW_STREAM_OUT_BLOCK_NUM

RAW_STREAM_CFG_DEFAULT()

DEFAULT_RAW_STREAM_CONFIG()
