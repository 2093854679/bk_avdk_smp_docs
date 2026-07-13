# WAV Decoder


Decode an audio data stream provided in WAV format.


## API Reference


### Header File


- [bk_audio/audio_decoders/wav_decoder.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_decoders/wav_decoder.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_decoders/wav_decoder.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") wav_decoder_init([wav_decoder_cfg_t](#_CPPv417wav_decoder_cfg_t "wav_decoder_cfg_t") *config)
:   Create a WAV decoder of Audio Element to decode incoming data using WAV format.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The audio element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct wav_decoder_cfg_t
:   WAV Decoder configurations.

    Public Members

    int buf_sz
    :   Element Buffer size

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

WAV_DECODER_TASK_STACK

WAV_DECODER_TASK_CORE

WAV_DECODER_TASK_PRIO

WAV_DECODER_BUFFER_SIZE

WAV_DECODER_OUT_BLOCK_SIZE

WAV_DECODER_OUT_BLOCK_NUM

DEFAULT_WAV_DECODER_CONFIG()
