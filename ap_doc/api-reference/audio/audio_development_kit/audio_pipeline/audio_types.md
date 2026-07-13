# Audio Types


The Audio Types provides the audio data type.


## API Reference


### Header File


- [bk_audio/audio_pipeline/audio_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_pipeline/audio_types.h")


### Enumerations

enum audio_stream_type_t
:   *Values:*

    enumerator AUDIO_STREAM_NONE

    enumerator AUDIO_STREAM_READER

    enumerator AUDIO_STREAM_WRITER

enum bk_codec_type_t
:   *Values:*

    enumerator BK_CODEC_TYPE_UNKNOW

    enumerator BK_CODEC_TYPE_PCM

    enumerator BK_CODEC_TYPE_WAV

    enumerator BK_CODEC_TYPE_MP3

    enumerator BK_CODEC_TYPE_AAC

    enumerator BK_CODEC_TYPE_OPUS

    enumerator BK_CODEC_TYPE_FLAC

    enumerator BK_CODEC_TYPE_ADPCM

    enumerator BK_CODEC_TYPE_G722

    enumerator BK_CODEC_TYPE_SBC

    enumerator BK_CODEC_TYPE_UNSUPPORT

enum mic_type_t
:   *Values:*

    enumerator MIC_TYPE_INVALID

    enumerator MIC_TYPE_ONBOARD

    enumerator MIC_TYPE_UAC

    enumerator MIC_TYPE_ONBOARD_DUAL_DMIC_MIC

enum audio_strm_type_t
:   *Values:*

    enumerator AUDIO_STRM_TYPE_INVALID

    enumerator AUDIO_STRM_TYPE_ONBOARD_MIC

    enumerator AUDIO_STRM_TYPE_UAC_MIC

    enumerator AUDIO_STRM_TYPE_ONBOARD_SPEAKER

    enumerator AUDIO_STRM_TYPE_UAC_SPEAKER

    enumerator AUDIO_STRM_TYPE_ARRAY

    enumerator AUDIO_STRM_TYPE_VFS

    enumerator AUDIO_STRM_TYPE_RAW

    enumerator AUDIO_STRM_TYPE_UART

    enumerator AUDIO_STRM_TYPE_I2S

    enumerator AUDIO_STRM_TYPE_MAX

enum spk_type_t
:   *Values:*

    enumerator SPK_TYPE_INVALID

    enumerator SPK_TYPE_ONBOARD

    enumerator SPK_TYPE_UAC

    enumerator SPK_TYPE_I2S

enum audio_enc_type_t
:   *Values:*

    enumerator AUDIO_ENC_TYPE_INVALID

    enumerator AUDIO_ENC_TYPE_PCM

    enumerator AUDIO_ENC_TYPE_G711A

    enumerator AUDIO_ENC_TYPE_G711U

    enumerator AUDIO_ENC_TYPE_AAC

    enumerator AUDIO_ENC_TYPE_ADPCM

    enumerator AUDIO_ENC_TYPE_LC3

    enumerator AUDIO_ENC_TYPE_OPUS

    enumerator AUDIO_ENC_TYPE_G722

    enumerator AUDIO_ENC_TYPE_USER
    :   User private encoding type

enum audio_dec_type_t
:   *Values:*

    enumerator AUDIO_DEC_TYPE_INVALID

    enumerator AUDIO_DEC_TYPE_PCM

    enumerator AUDIO_DEC_TYPE_G711A

    enumerator AUDIO_DEC_TYPE_G711U

    enumerator AUDIO_DEC_TYPE_AAC

    enumerator AUDIO_DEC_TYPE_ADPCM

    enumerator AUDIO_DEC_TYPE_LC3

    enumerator AUDIO_DEC_TYPE_MP3

    enumerator AUDIO_DEC_TYPE_OPUS

    enumerator AUDIO_DEC_TYPE_G722

    enumerator AUDIO_DEC_TYPE_WAV

    enumerator AUDIO_DEC_TYPE_AMR

    enumerator AUDIO_DEC_TYPE_USER
    :   User private decoding type

enum audio_mem_type_t
:   *Values:*

    enumerator AUDIO_MEM_TYPE_SRAM

    enumerator AUDIO_MEM_TYPE_PSRAM

    enumerator AUDIO_MEM_TYPE_AUDIO_HEAP

enum audio_buf_type_t
:   *Values:*

    enumerator AUDIO_BUF_TYPE_RB

    enumerator AUDIO_BUF_TYPE_FB
