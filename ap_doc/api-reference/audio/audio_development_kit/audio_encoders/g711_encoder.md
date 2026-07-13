# G711 Encoder


Encode an audio data stream to G711 format.


## API Reference


### Header File


- [bk_audio/audio_encoders/g711_encoder.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_encoders/g711_encoder.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_encoders/g711_encoder.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") g711_encoder_init([g711_encoder_cfg_t](#_CPPv418g711_encoder_cfg_t "g711_encoder_cfg_t") *config)
:   Create a G711 encoder of Audio Element to encode incoming data using G711 format.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The audio element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct g711_encoder_cfg_t
:   G711 Encoder configurations.


### Macros

G711_ENCODER_TASK_STACK

G711_ENCODER_TASK_CORE

G711_ENCODER_TASK_PRIO

G711_ENCODER_BUFFER_SIZE

G711_ENCODER_OUT_BLOCK_SIZE

G711_ENCODER_OUT_BLOCK_NUM

DEFAULT_G711_ENCODER_CONFIG()


### Enumerations

enum g711_encoder_mode_t
:   Enum of G711 Encoder enc_mode.


    *Values:*

    enumerator G711_ENC_MODE_A_LOW

    enumerator G711_ENC_MODE_U_LOW

    enumerator G711_ENC_MODE_MAX
    :   Invalid mode
