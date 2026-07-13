# VFS Stream


The VFS stream reads/writes audio data from/into VFS.


## API Reference


### Header File


- [bk_audio/audio_streams/vfs_stream.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/vfs_stream.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/vfs_stream.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") vfs_stream_init([vfs_stream_cfg_t](#_CPPv416vfs_stream_cfg_t "vfs_stream_cfg_t") *config)
:   Create a handle to an Audio Element to stream data from vfs file system to another Element or get data from other elements written to vfs file system, depending on the configuration the stream type, either AUDIO_STREAM_READER or AUDIO_STREAM_WRITER.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The Audio Element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct vfs_stream_cfg_t
:   VFS Stream configurations, if any entry is zero then the configuration will be set to default values.

    Public Members

    [audio_stream_type_t](../audio_pipeline/audio_types.md#_CPPv419audio_stream_type_t "audio_stream_type_t") type
    :   Stream type

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

VFS_STREAM_BUF_SIZE

VFS_STREAM_TASK_STACK

VFS_STREAM_TASK_CORE

VFS_STREAM_TASK_PRIO

VFS_STREAM_OUT_BLOCK_SIZE

VFS_STREAM_OUT_BLOCK_NUM

DEFAULT_VFS_STREAM_CONFIG()
