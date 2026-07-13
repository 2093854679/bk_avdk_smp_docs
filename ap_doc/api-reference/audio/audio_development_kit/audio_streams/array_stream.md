# Array Stream


The array stream reads/writes audio data from/into array.


## API Reference


### Header File


- [bk_audio/audio_streams/array_stream.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/array_stream.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/array_stream.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") array_stream_init([array_stream_cfg_t](#_CPPv418array_stream_cfg_t "array_stream_cfg_t") *config)
:   Create a handle to an Audio Element to stream data from array to another Element or get data from other elements written to array, depending on the configuration the stream type, either AUDIO_STREAM_READER or AUDIO_STREAM_WRITER.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The Audio Element handle


        - Not NULL: success

        - NULL: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") array_stream_set_data([audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") array_stream, uint8_t *array_buf, int array_size)
:   Set the array information for the array stream. This interface must be used to set the array and its length after the component is initialized and before it runs.

    参数
    :   - **array_stream** – **[in]** The audio element handle of the array stream.

        - **array_buf** – **[in]** Pointer to the array buffer.

        - **array_size** – **[in]** Size of the array.

    返回
    :   Operation result


        - BK_OK: Success

        - Other values: Failure


### Structures

struct array_stream_cfg_t
:   ARRAY Stream configurations, if any entry is zero then the configuration will be set to default values.

    Public Members

    [audio_stream_type_t](../audio_pipeline/audio_types.md#_CPPv419audio_stream_type_t "audio_stream_type_t") type
    :   Stream type

    uint32_t array_size
    :   Array total size

    uint32_t array_offset
    :   Array offset

    int buf_sz
    :   Audio Element Buffer size

    int out_block_size
    :   Size of output block

    int out_block_num
    :   Number of output block

    int task_stack
    :   Task stack size

    int task_core
    :   Task running in core (0 or 1)

    int task_prio
    :   Task priority (based on freeRTOS priority)


### Macros

ARRAY_STREAM_BUF_SIZE

ARRAY_STREAM_TASK_STACK

ARRAY_STREAM_TASK_CORE

ARRAY_STREAM_TASK_PRIO

ARRAY_STREAM_OUT_BLOCK_SIZE

ARRAY_STREAM_OUT_BLOCK_NUM

DEFAULT_ARRAY_STREAM_CONFIG()
