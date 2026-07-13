# MP3 Decoder


Decode an audio data stream provided in MP3 format.


## API Reference


### Header File


- [bk_audio/audio_decoders/mp3_decoder.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_decoders/mp3_decoder.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_decoders/mp3_decoder.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") mp3_decoder_init([mp3_decoder_cfg_t](#_CPPv417mp3_decoder_cfg_t "mp3_decoder_cfg_t") *config)
:   Create a MP3 decoder of Audio Element to decode incoming data using MP3 format.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The audio element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct mp3_decoder_cfg_t
:   MP3 Decoder configurations.

    Public Members

    uint32_t main_buff_size
    :   mainbuff size

    uint32_t out_pcm_buff_size
    :   out pcm buffer size

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

MP3_DECODER_TASK_STACK

MP3_DECODER_TASK_CORE

MP3_DECODER_TASK_PRIO

MP3_DECODER_MAIN_BUFF_SIZE

MP3_DECODER_OUT_PCM_BUFF_SIZE

DEFAULT_MP3_DECODER_CONFIG()
