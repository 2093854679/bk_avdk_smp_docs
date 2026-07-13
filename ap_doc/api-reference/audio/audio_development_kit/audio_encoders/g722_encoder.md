# G722 Encoder


Encode an audio data stream to G722 format.


## API Reference


### Header File


- [bk_audio/audio_encoders/g722_encoder.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_encoders/g722_encoder.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_encoders/g722_encoder.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") g722_encoder_init([g722_encoder_cfg_t](#_CPPv418g722_encoder_cfg_t "g722_encoder_cfg_t") *config)
:   Create a G722 encoder of Audio Element to encode incoming data using G722 format.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The audio element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct g722_encoder_cfg_t
:   G722 Encoder configurations.


### Macros

G722_ENCODER_TASK_STACK

G722_ENCODER_TASK_CORE

G722_ENCODER_TASK_PRIO

G722_ENCODER_BUFFER_SIZE

G722_ENCODER_OUT_BLOCK_SIZE

G722_ENCODER_OUT_BLOCK_NUM

DEFAULT_G722_ENCODER_CONFIG()


### Enumerations

enum g722_encoder_rate_t
:   Enum of G722 Encoder bit rate.


    *Values:*

    enumerator G722_ENC_RATE_48000

    enumerator G722_ENC_RATE_56000

    enumerator G722_ENC_RATE_64000

    enumerator G722_ENC_RATE_MAX
    :   Invalid rate
