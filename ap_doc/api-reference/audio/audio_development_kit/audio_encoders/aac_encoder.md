# AAC Encoder


Encode an audio data stream to AAC format.


## API Reference


### Header File


- [bk_audio/audio_encoders/aac_encoder.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_encoders/aac_encoder.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_encoders/aac_encoder.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") aac_encoder_init([aac_encoder_cfg_t](#_CPPv417aac_encoder_cfg_t "aac_encoder_cfg_t") *config)
:   Create a AAC encoder of Audio Element to encode incoming data using AAC format.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The audio element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct aac_encoder_cfg_t
:   AAC Encoder configurations.

    Public Members

    uint8_t chl_num
    :   channel number

    uint32_t samp_rate
    :   sample rate

    uint8_t bits
    :   Bit wide (8, 16, 24, 32 bits)

    uint32_t modules
    :   modules, refer to “encModules” parameter description of “aacEncOpen” spi in aacenc_lib.h

    uint8_t aot
    :   Audio object type, refer to “AACENC_AOT” parameter description in aacenc_lib.h

    uint32_t bitrate
    :   encoder bitrate, refer to “AACENC_BITRATE” parameter description in aacenc_lib.h

    uint8_t bitrate_mode
    :   Bitrate mode, refer to “AACENC_BITRATEMODE” parameter description in aacenc_lib.h

    int8_t sbr_mode
    :   sbr mode, refer to “AACENC_SBR_MODE” parameter description in aacenc_lib.h

    uint32_t granule_length
    :   audio frame length in samples, refer to “AACENC_GRANULE_LENGTH” parameter description in aacenc_lib.h

    uint8_t chl_order
    :   Input audio data channel ordering scheme, refer to “AACENC_CHANNELORDER” parameter description in aacenc_lib.h

    uint8_t afterburner_en
    :   afterburner feature enable, refer to “AACENC_AFTERBURNER” parameter description in aacenc_lib.h

    uint8_t transport_type
    :   Transport type, refer to “AACENC_TRANSMUX” parameter description in aacenc_lib.h

    int buffer_len
    :   Buffer length use for aac Element

    uint32_t in_pool_len
    :   input data pool size(byte), save data if the valid data in pool is less than one frame

    uint32_t out_buffer_len
    :   one frame data size(byte) of output aac data, less than one frame size

    int out_block_size
    :   Size of output block, at least larger than the size of one frame of output aac data

    int out_block_num
    :   Number of output block

    int task_stack
    :   Task stack size

    int task_core
    :   Task running in core (0 or 1)

    int task_prio
    :   Task priority (based on freeRTOS priority)


### Macros

AAC_ENCODER_CHL_NUM

AAC_ENCODER_SAMP_RATE

AAC_ENCODER_BITS

AAC_ENCODER_MODULES

AAC_ENCODER_AOT

AAC_ENCODER_BITRATE

AAC_ENCODER_BITRATE_MODE

AAC_ENCODER_SBR_MODE

AAC_ENCODER_GRANULE_LENGTH

AAC_ENCODER_CHL_ORDER

AAC_ENCODER_AFTERBURNER_EN

AAC_ENCODER_TRANSPORT_TYPE

AAC_ENCODER_BUFFER_LEN

AAC_ENCODER_IN_POOL_LEN

AAC_ENCODER_OUT_BUFFER_LEN

AAC_ENCODER_OUT_BLOCK_SIZE

AAC_ENCODER_OUT_BLOCK_NUM

AAC_ENCODER_TASK_STACK

AAC_ENCODER_TASK_CORE

AAC_ENCODER_TASK_PRIO

DEFAULT_AAC_ENCODER_CONFIG()
