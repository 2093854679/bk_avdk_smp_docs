# G722 Decoder


Decode an audio data stream provided in G722 format.


## API Reference


### Header File


- [bk_audio/audio_decoders/g722_decoder.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_decoders/g722_decoder.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_decoders/g722_decoder.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") g722_decoder_init([g722_decoder_cfg_t](#_CPPv418g722_decoder_cfg_t "g722_decoder_cfg_t") *config)
:   Create a G722 decoder of Audio Element to decode incoming data using G722 format.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The audio element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct g722_decoder_cfg_t
:   G722 Decoder configurations.


### Macros

G722_DECODER_TASK_STACK

G722_DECODER_TASK_CORE

G722_DECODER_TASK_PRIO

G722_DECODER_BUFFER_SIZE

G722_DECODER_OUT_BLOCK_SIZE

G722_DECODER_OUT_BLOCK_NUM

DEFAULT_G722_DECODER_CONFIG()


### Enumerations

enum g722_decoder_rate_t
:   Enum of G722 Decoder rate.


    *Values:*

    enumerator G722_DEC_RATE_48000

    enumerator G722_DEC_RATE_56000

    enumerator G722_DEC_RATE_64000

enum g722_decoder_option_t
:   Enum of G722 Decoder options.


    *Values:*

    enumerator G722_DEC_OPTION_NONE

    enumerator G722_DEC_OPTION_8K_SAMPLE

    enumerator G722_DEC_OPTION_PACKED
