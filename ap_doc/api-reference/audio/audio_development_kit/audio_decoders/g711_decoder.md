# G711 Decoder


Decode an audio data stream provided in G711 format.


## API Reference


### Header File


- [bk_audio/audio_decoders/g711_decoder.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_decoders/g711_decoder.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_decoders/g711_decoder.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") g711_decoder_init([g711_decoder_cfg_t](#_CPPv418g711_decoder_cfg_t "g711_decoder_cfg_t") *config)
:   Create a G711 decoder of Audio Element to decode incoming data using G711 format.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The audio element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct g711_decoder_cfg_t
:   G711 Decoder configurations.


### Macros

G711_DECODER_TASK_STACK

G711_DECODER_TASK_CORE

G711_DECODER_TASK_PRIO

G711_DECODER_BUFFER_SIZE

G711_DECODER_OUT_BLOCK_SIZE

G711_DECODER_OUT_BLOCK_NUM

DEFAULT_G711_DECODER_CONFIG()


### Enumerations

enum g711_decoder_mode_t
:   Enum of G711 Decoder dec_mode.


    *Values:*

    enumerator G711_DEC_MODE_A_LOW

    enumerator G711_DEC_MODE_U_LOW

    enumerator G711_DEC_MODE_MAX
    :   Invalid mode
