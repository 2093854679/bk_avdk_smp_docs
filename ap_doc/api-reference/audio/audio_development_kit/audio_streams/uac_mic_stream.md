# UAC Mic Stream


The UAC MIC stream reads audio data from UAC mic.


## API Reference


### Header File


- [bk_audio/audio_streams/uac_mic_stream.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/uac_mic_stream.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_streams/uac_mic_stream.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") uac_mic_stream_init([uac_mic_stream_cfg_t](#_CPPv420uac_mic_stream_cfg_t "uac_mic_stream_cfg_t") *config)
:   Create a handle to an Audio Element to stream data to another Element.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The Audio Element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct uac_mic_stream_cfg_t
:   UAC MIC Stream configurations, if any entry is zero then the configuration will be set to default values.

    Public Members

    [E_USB_HUB_PORT_INDEX](../../../peripheral/bk_usb.md#_CPPv420E_USB_HUB_PORT_INDEX "E_USB_HUB_PORT_INDEX") port_index
    :   usb hub port index

    uint16_t format
    :   uac mic data format

    uint8_t chl_num
    :   mic channel number

    uint8_t bits
    :   Bit wide (8, 16 bits)

    uint32_t samp_rate
    :   mic sample rate

    uint32_t frame_size
    :   size of one frame mic data

    int out_block_size
    :   Size of output block

    int out_block_num
    :   Number of output block

    bool auto_connect
    :   Automatic connect enable

    int multi_out_port_num
    :   The number of multiple output audio port

    int task_stack
    :   Task stack size

    int task_core
    :   Task running in core (0 or 1)

    int task_prio
    :   Task priority (based on freeRTOS priority)


### Macros

UAC_MIC_STREAM_TASK_STACK

UAC_MIC_STREAM_TASK_CORE

UAC_MIC_STREAM_TASK_PRIO

UAC_MIC_STREAM_CFG_DEFAULT()

DEFAULT_UAC_MIC_STREAM_CONFIG()
