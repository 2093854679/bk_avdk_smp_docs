---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_pipeline/audio_types.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="audio-types"></a>

# Audio Types

The Audio Types provides the audio data type.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [audio\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_pipeline/audio_types.h)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv419audio_stream_type_t"></a>

<a id="_CPPv319audio_stream_type_t"></a> <a id="_CPPv219audio_stream_type_t"></a> <a id="audio__types_8h_1a617edfb76567ff93543b9ee637a07d5c"></a> enum audio\_stream\_type\_t
:   *Values:*

    <a id="_CPPv4N19audio_stream_type_t17AUDIO_STREAM_NONEE"></a>

    <a id="_CPPv3N19audio_stream_type_t17AUDIO_STREAM_NONEE"></a> <a id="_CPPv2N19audio_stream_type_t17AUDIO_STREAM_NONEE"></a> <a id="audio__types_8h_1a617edfb76567ff93543b9ee637a07d5cabd15139e5fc6c3978f3a9e932eb22735"></a> enumerator AUDIO\_STREAM\_NONE

    <a id="_CPPv4N19audio_stream_type_t19AUDIO_STREAM_READERE"></a>

    <a id="_CPPv3N19audio_stream_type_t19AUDIO_STREAM_READERE"></a> <a id="_CPPv2N19audio_stream_type_t19AUDIO_STREAM_READERE"></a> <a id="audio__types_8h_1a617edfb76567ff93543b9ee637a07d5ca5ddb25cab5a03a9e1b61a5bc3494a979"></a> enumerator AUDIO\_STREAM\_READER

    <a id="_CPPv4N19audio_stream_type_t19AUDIO_STREAM_WRITERE"></a>

    <a id="_CPPv3N19audio_stream_type_t19AUDIO_STREAM_WRITERE"></a> <a id="_CPPv2N19audio_stream_type_t19AUDIO_STREAM_WRITERE"></a> <a id="audio__types_8h_1a617edfb76567ff93543b9ee637a07d5cae518220e6d1dac80a4ff731d7143b7a8"></a> enumerator AUDIO\_STREAM\_WRITER

<a id="_CPPv415bk_codec_type_t"></a>

<a id="_CPPv315bk_codec_type_t"></a> <a id="_CPPv215bk_codec_type_t"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4a"></a> enum bk\_codec\_type\_t
:   *Values:*

    <a id="_CPPv4N15bk_codec_type_t20BK_CODEC_TYPE_UNKNOWE"></a>

    <a id="_CPPv3N15bk_codec_type_t20BK_CODEC_TYPE_UNKNOWE"></a> <a id="_CPPv2N15bk_codec_type_t20BK_CODEC_TYPE_UNKNOWE"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aaba2b277e49312dcdde84283e79f3b4bc"></a> enumerator BK\_CODEC\_TYPE\_UNKNOW

    <a id="_CPPv4N15bk_codec_type_t17BK_CODEC_TYPE_PCME"></a>

    <a id="_CPPv3N15bk_codec_type_t17BK_CODEC_TYPE_PCME"></a> <a id="_CPPv2N15bk_codec_type_t17BK_CODEC_TYPE_PCME"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aa7074043c1551872e9b5f94514b4a164b"></a> enumerator BK\_CODEC\_TYPE\_PCM

    <a id="_CPPv4N15bk_codec_type_t17BK_CODEC_TYPE_WAVE"></a>

    <a id="_CPPv3N15bk_codec_type_t17BK_CODEC_TYPE_WAVE"></a> <a id="_CPPv2N15bk_codec_type_t17BK_CODEC_TYPE_WAVE"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aa5c9565621bdbba0b3d601d9c8426ed93"></a> enumerator BK\_CODEC\_TYPE\_WAV

    <a id="_CPPv4N15bk_codec_type_t17BK_CODEC_TYPE_MP3E"></a>

    <a id="_CPPv3N15bk_codec_type_t17BK_CODEC_TYPE_MP3E"></a> <a id="_CPPv2N15bk_codec_type_t17BK_CODEC_TYPE_MP3E"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aabd5152edcfd0c0a042f3e526d9badf10"></a> enumerator BK\_CODEC\_TYPE\_MP3

    <a id="_CPPv4N15bk_codec_type_t17BK_CODEC_TYPE_AACE"></a>

    <a id="_CPPv3N15bk_codec_type_t17BK_CODEC_TYPE_AACE"></a> <a id="_CPPv2N15bk_codec_type_t17BK_CODEC_TYPE_AACE"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aa3e9e2aa0913cc5733d7137051300bc48"></a> enumerator BK\_CODEC\_TYPE\_AAC

    <a id="_CPPv4N15bk_codec_type_t18BK_CODEC_TYPE_OPUSE"></a>

    <a id="_CPPv3N15bk_codec_type_t18BK_CODEC_TYPE_OPUSE"></a> <a id="_CPPv2N15bk_codec_type_t18BK_CODEC_TYPE_OPUSE"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aa12436a7d5551b98f86a9fbf2439ae2fd"></a> enumerator BK\_CODEC\_TYPE\_OPUS

    <a id="_CPPv4N15bk_codec_type_t18BK_CODEC_TYPE_FLACE"></a>

    <a id="_CPPv3N15bk_codec_type_t18BK_CODEC_TYPE_FLACE"></a> <a id="_CPPv2N15bk_codec_type_t18BK_CODEC_TYPE_FLACE"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aa7919711eb065a37d02658ba2a736a44c"></a> enumerator BK\_CODEC\_TYPE\_FLAC

    <a id="_CPPv4N15bk_codec_type_t19BK_CODEC_TYPE_ADPCME"></a>

    <a id="_CPPv3N15bk_codec_type_t19BK_CODEC_TYPE_ADPCME"></a> <a id="_CPPv2N15bk_codec_type_t19BK_CODEC_TYPE_ADPCME"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aa6b561115593de6993e5e0979db026c6a"></a> enumerator BK\_CODEC\_TYPE\_ADPCM

    <a id="_CPPv4N15bk_codec_type_t18BK_CODEC_TYPE_G722E"></a>

    <a id="_CPPv3N15bk_codec_type_t18BK_CODEC_TYPE_G722E"></a> <a id="_CPPv2N15bk_codec_type_t18BK_CODEC_TYPE_G722E"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aa282a3a75d11f733980013663cd08358a"></a> enumerator BK\_CODEC\_TYPE\_G722

    <a id="_CPPv4N15bk_codec_type_t17BK_CODEC_TYPE_SBCE"></a>

    <a id="_CPPv3N15bk_codec_type_t17BK_CODEC_TYPE_SBCE"></a> <a id="_CPPv2N15bk_codec_type_t17BK_CODEC_TYPE_SBCE"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aaa9ed6c269c964b240b2134520a283e69"></a> enumerator BK\_CODEC\_TYPE\_SBC

    <a id="_CPPv4N15bk_codec_type_t23BK_CODEC_TYPE_UNSUPPORTE"></a>

    <a id="_CPPv3N15bk_codec_type_t23BK_CODEC_TYPE_UNSUPPORTE"></a> <a id="_CPPv2N15bk_codec_type_t23BK_CODEC_TYPE_UNSUPPORTE"></a> <a id="audio__types_8h_1a9fc32acde4837c4a3558b5f6c8174c4aab796ffd8173fac419b00c5bf6da65343"></a> enumerator BK\_CODEC\_TYPE\_UNSUPPORT

<a id="_CPPv410mic_type_t"></a>

<a id="_CPPv310mic_type_t"></a> <a id="_CPPv210mic_type_t"></a> <a id="audio__types_8h_1a6d648d01036864ab8f609f505f2bf5d6"></a> enum mic\_type\_t
:   *Values:*

    <a id="_CPPv4N10mic_type_t16MIC_TYPE_INVALIDE"></a>

    <a id="_CPPv3N10mic_type_t16MIC_TYPE_INVALIDE"></a> <a id="_CPPv2N10mic_type_t16MIC_TYPE_INVALIDE"></a> <a id="audio__types_8h_1a6d648d01036864ab8f609f505f2bf5d6abe9e572af3dade825255aadb2ce2c2e9"></a> enumerator MIC\_TYPE\_INVALID

    <a id="_CPPv4N10mic_type_t16MIC_TYPE_ONBOARDE"></a>

    <a id="_CPPv3N10mic_type_t16MIC_TYPE_ONBOARDE"></a> <a id="_CPPv2N10mic_type_t16MIC_TYPE_ONBOARDE"></a> <a id="audio__types_8h_1a6d648d01036864ab8f609f505f2bf5d6ad3a5d867c4f424c6014e70a7fa82c67e"></a> enumerator MIC\_TYPE\_ONBOARD

    <a id="_CPPv4N10mic_type_t12MIC_TYPE_UACE"></a>

    <a id="_CPPv3N10mic_type_t12MIC_TYPE_UACE"></a> <a id="_CPPv2N10mic_type_t12MIC_TYPE_UACE"></a> <a id="audio__types_8h_1a6d648d01036864ab8f609f505f2bf5d6ae8c64d52514550079dc659ed4b250ccc"></a> enumerator MIC\_TYPE\_UAC

    <a id="_CPPv4N10mic_type_t30MIC_TYPE_ONBOARD_DUAL_DMIC_MICE"></a>

    <a id="_CPPv3N10mic_type_t30MIC_TYPE_ONBOARD_DUAL_DMIC_MICE"></a> <a id="_CPPv2N10mic_type_t30MIC_TYPE_ONBOARD_DUAL_DMIC_MICE"></a> <a id="audio__types_8h_1a6d648d01036864ab8f609f505f2bf5d6a41a35b2297f872eb8e524a9988ee8144"></a> enumerator MIC\_TYPE\_ONBOARD\_DUAL\_DMIC\_MIC

<a id="_CPPv417audio_strm_type_t"></a>

<a id="_CPPv317audio_strm_type_t"></a> <a id="_CPPv217audio_strm_type_t"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4"></a> enum audio\_strm\_type\_t
:   *Values:*

    <a id="_CPPv4N17audio_strm_type_t23AUDIO_STRM_TYPE_INVALIDE"></a>

    <a id="_CPPv3N17audio_strm_type_t23AUDIO_STRM_TYPE_INVALIDE"></a> <a id="_CPPv2N17audio_strm_type_t23AUDIO_STRM_TYPE_INVALIDE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4a7fa823cbb020bb892ef117ccc145318a"></a> enumerator AUDIO\_STRM\_TYPE\_INVALID

    <a id="_CPPv4N17audio_strm_type_t27AUDIO_STRM_TYPE_ONBOARD_MICE"></a>

    <a id="_CPPv3N17audio_strm_type_t27AUDIO_STRM_TYPE_ONBOARD_MICE"></a> <a id="_CPPv2N17audio_strm_type_t27AUDIO_STRM_TYPE_ONBOARD_MICE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4afcb17b94e3a011d841e3adbb1d9cb43f"></a> enumerator AUDIO\_STRM\_TYPE\_ONBOARD\_MIC

    <a id="_CPPv4N17audio_strm_type_t23AUDIO_STRM_TYPE_UAC_MICE"></a>

    <a id="_CPPv3N17audio_strm_type_t23AUDIO_STRM_TYPE_UAC_MICE"></a> <a id="_CPPv2N17audio_strm_type_t23AUDIO_STRM_TYPE_UAC_MICE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4a7eab20ef2b5362c0e1582e5f7c46dc58"></a> enumerator AUDIO\_STRM\_TYPE\_UAC\_MIC

    <a id="_CPPv4N17audio_strm_type_t31AUDIO_STRM_TYPE_ONBOARD_SPEAKERE"></a>

    <a id="_CPPv3N17audio_strm_type_t31AUDIO_STRM_TYPE_ONBOARD_SPEAKERE"></a> <a id="_CPPv2N17audio_strm_type_t31AUDIO_STRM_TYPE_ONBOARD_SPEAKERE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4a325525442df97aff589a45e3b5e0ae92"></a> enumerator AUDIO\_STRM\_TYPE\_ONBOARD\_SPEAKER

    <a id="_CPPv4N17audio_strm_type_t27AUDIO_STRM_TYPE_UAC_SPEAKERE"></a>

    <a id="_CPPv3N17audio_strm_type_t27AUDIO_STRM_TYPE_UAC_SPEAKERE"></a> <a id="_CPPv2N17audio_strm_type_t27AUDIO_STRM_TYPE_UAC_SPEAKERE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4a929e9b530b9ab305b3096a68540040de"></a> enumerator AUDIO\_STRM\_TYPE\_UAC\_SPEAKER

    <a id="_CPPv4N17audio_strm_type_t21AUDIO_STRM_TYPE_ARRAYE"></a>

    <a id="_CPPv3N17audio_strm_type_t21AUDIO_STRM_TYPE_ARRAYE"></a> <a id="_CPPv2N17audio_strm_type_t21AUDIO_STRM_TYPE_ARRAYE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4a3f5500b6f28ab8c618aece8f70aa93be"></a> enumerator AUDIO\_STRM\_TYPE\_ARRAY

    <a id="_CPPv4N17audio_strm_type_t19AUDIO_STRM_TYPE_VFSE"></a>

    <a id="_CPPv3N17audio_strm_type_t19AUDIO_STRM_TYPE_VFSE"></a> <a id="_CPPv2N17audio_strm_type_t19AUDIO_STRM_TYPE_VFSE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4adc0316ce3928468a2a54de32023105d8"></a> enumerator AUDIO\_STRM\_TYPE\_VFS

    <a id="_CPPv4N17audio_strm_type_t19AUDIO_STRM_TYPE_RAWE"></a>

    <a id="_CPPv3N17audio_strm_type_t19AUDIO_STRM_TYPE_RAWE"></a> <a id="_CPPv2N17audio_strm_type_t19AUDIO_STRM_TYPE_RAWE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4a63cbd2348622dab9c3937fd9ed992daf"></a> enumerator AUDIO\_STRM\_TYPE\_RAW

    <a id="_CPPv4N17audio_strm_type_t20AUDIO_STRM_TYPE_UARTE"></a>

    <a id="_CPPv3N17audio_strm_type_t20AUDIO_STRM_TYPE_UARTE"></a> <a id="_CPPv2N17audio_strm_type_t20AUDIO_STRM_TYPE_UARTE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4a53fee537bf00764b97c34a8c0e854fbb"></a> enumerator AUDIO\_STRM\_TYPE\_UART

    <a id="_CPPv4N17audio_strm_type_t19AUDIO_STRM_TYPE_I2SE"></a>

    <a id="_CPPv3N17audio_strm_type_t19AUDIO_STRM_TYPE_I2SE"></a> <a id="_CPPv2N17audio_strm_type_t19AUDIO_STRM_TYPE_I2SE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4af04c9dd15497fd9c8632cd48dbadf850"></a> enumerator AUDIO\_STRM\_TYPE\_I2S

    <a id="_CPPv4N17audio_strm_type_t19AUDIO_STRM_TYPE_MAXE"></a>

    <a id="_CPPv3N17audio_strm_type_t19AUDIO_STRM_TYPE_MAXE"></a> <a id="_CPPv2N17audio_strm_type_t19AUDIO_STRM_TYPE_MAXE"></a> <a id="audio__types_8h_1a3016ec97fae6e92fef085cd99c15afc4a6bb1a29184de16ce20b07e76dd6b4b92"></a> enumerator AUDIO\_STRM\_TYPE\_MAX

<a id="_CPPv410spk_type_t"></a>

<a id="_CPPv310spk_type_t"></a> <a id="_CPPv210spk_type_t"></a> <a id="audio__types_8h_1af6bbf93ded8f50f9a9e229a8ed40bbca"></a> enum spk\_type\_t
:   *Values:*

    <a id="_CPPv4N10spk_type_t16SPK_TYPE_INVALIDE"></a>

    <a id="_CPPv3N10spk_type_t16SPK_TYPE_INVALIDE"></a> <a id="_CPPv2N10spk_type_t16SPK_TYPE_INVALIDE"></a> <a id="audio__types_8h_1af6bbf93ded8f50f9a9e229a8ed40bbcaab2a3335602a2ae8753a7304d6610d1d1"></a> enumerator SPK\_TYPE\_INVALID

    <a id="_CPPv4N10spk_type_t16SPK_TYPE_ONBOARDE"></a>

    <a id="_CPPv3N10spk_type_t16SPK_TYPE_ONBOARDE"></a> <a id="_CPPv2N10spk_type_t16SPK_TYPE_ONBOARDE"></a> <a id="audio__types_8h_1af6bbf93ded8f50f9a9e229a8ed40bbcaa9e2de4ec27b2b0e8dfc318332f6b7b9a"></a> enumerator SPK\_TYPE\_ONBOARD

    <a id="_CPPv4N10spk_type_t12SPK_TYPE_UACE"></a>

    <a id="_CPPv3N10spk_type_t12SPK_TYPE_UACE"></a> <a id="_CPPv2N10spk_type_t12SPK_TYPE_UACE"></a> <a id="audio__types_8h_1af6bbf93ded8f50f9a9e229a8ed40bbcaaf677ba6d270d377d6d8110fda9f8a502"></a> enumerator SPK\_TYPE\_UAC

    <a id="_CPPv4N10spk_type_t12SPK_TYPE_I2SE"></a>

    <a id="_CPPv3N10spk_type_t12SPK_TYPE_I2SE"></a> <a id="_CPPv2N10spk_type_t12SPK_TYPE_I2SE"></a> <a id="audio__types_8h_1af6bbf93ded8f50f9a9e229a8ed40bbcaa9aefa4543acc960e3925cebeda9dbe2c"></a> enumerator SPK\_TYPE\_I2S

<a id="_CPPv416audio_enc_type_t"></a>

<a id="_CPPv316audio_enc_type_t"></a> <a id="_CPPv216audio_enc_type_t"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2"></a> enum audio\_enc\_type\_t
:   *Values:*

    <a id="_CPPv4N16audio_enc_type_t22AUDIO_ENC_TYPE_INVALIDE"></a>

    <a id="_CPPv3N16audio_enc_type_t22AUDIO_ENC_TYPE_INVALIDE"></a> <a id="_CPPv2N16audio_enc_type_t22AUDIO_ENC_TYPE_INVALIDE"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2a2d7379ec84199ead8fbd189e71dba043"></a> enumerator AUDIO\_ENC\_TYPE\_INVALID

    <a id="_CPPv4N16audio_enc_type_t18AUDIO_ENC_TYPE_PCME"></a>

    <a id="_CPPv3N16audio_enc_type_t18AUDIO_ENC_TYPE_PCME"></a> <a id="_CPPv2N16audio_enc_type_t18AUDIO_ENC_TYPE_PCME"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2a83314e8e01e3868f5979c46a5457748f"></a> enumerator AUDIO\_ENC\_TYPE\_PCM

    <a id="_CPPv4N16audio_enc_type_t20AUDIO_ENC_TYPE_G711AE"></a>

    <a id="_CPPv3N16audio_enc_type_t20AUDIO_ENC_TYPE_G711AE"></a> <a id="_CPPv2N16audio_enc_type_t20AUDIO_ENC_TYPE_G711AE"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2af5549be7a49c5928555509f7d8c3e97b"></a> enumerator AUDIO\_ENC\_TYPE\_G711A

    <a id="_CPPv4N16audio_enc_type_t20AUDIO_ENC_TYPE_G711UE"></a>

    <a id="_CPPv3N16audio_enc_type_t20AUDIO_ENC_TYPE_G711UE"></a> <a id="_CPPv2N16audio_enc_type_t20AUDIO_ENC_TYPE_G711UE"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2a0296288f4f91a8c42152ad50cc245d57"></a> enumerator AUDIO\_ENC\_TYPE\_G711U

    <a id="_CPPv4N16audio_enc_type_t18AUDIO_ENC_TYPE_AACE"></a>

    <a id="_CPPv3N16audio_enc_type_t18AUDIO_ENC_TYPE_AACE"></a> <a id="_CPPv2N16audio_enc_type_t18AUDIO_ENC_TYPE_AACE"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2a7134c7714555e431edbe080f5228e000"></a> enumerator AUDIO\_ENC\_TYPE\_AAC

    <a id="_CPPv4N16audio_enc_type_t20AUDIO_ENC_TYPE_ADPCME"></a>

    <a id="_CPPv3N16audio_enc_type_t20AUDIO_ENC_TYPE_ADPCME"></a> <a id="_CPPv2N16audio_enc_type_t20AUDIO_ENC_TYPE_ADPCME"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2af7beea99254f9cb5ce67498759c0c17d"></a> enumerator AUDIO\_ENC\_TYPE\_ADPCM

    <a id="_CPPv4N16audio_enc_type_t18AUDIO_ENC_TYPE_LC3E"></a>

    <a id="_CPPv3N16audio_enc_type_t18AUDIO_ENC_TYPE_LC3E"></a> <a id="_CPPv2N16audio_enc_type_t18AUDIO_ENC_TYPE_LC3E"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2a046bb8f87d647affd55ef352e117188e"></a> enumerator AUDIO\_ENC\_TYPE\_LC3

    <a id="_CPPv4N16audio_enc_type_t19AUDIO_ENC_TYPE_OPUSE"></a>

    <a id="_CPPv3N16audio_enc_type_t19AUDIO_ENC_TYPE_OPUSE"></a> <a id="_CPPv2N16audio_enc_type_t19AUDIO_ENC_TYPE_OPUSE"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2a4b5e057a43e555ee0e769d144471e2e9"></a> enumerator AUDIO\_ENC\_TYPE\_OPUS

    <a id="_CPPv4N16audio_enc_type_t19AUDIO_ENC_TYPE_G722E"></a>

    <a id="_CPPv3N16audio_enc_type_t19AUDIO_ENC_TYPE_G722E"></a> <a id="_CPPv2N16audio_enc_type_t19AUDIO_ENC_TYPE_G722E"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2a573e4fc236a3be45ad1a3be98c3f4f41"></a> enumerator AUDIO\_ENC\_TYPE\_G722

    <a id="_CPPv4N16audio_enc_type_t19AUDIO_ENC_TYPE_USERE"></a>

    <a id="_CPPv3N16audio_enc_type_t19AUDIO_ENC_TYPE_USERE"></a> <a id="_CPPv2N16audio_enc_type_t19AUDIO_ENC_TYPE_USERE"></a> <a id="audio__types_8h_1a592d5ae4293d8618ecfdebbf681f67b2a0ff9ce5e7272bcb9c5bf772718c5f820"></a> enumerator AUDIO\_ENC\_TYPE\_USER
    :   User private encoding type

<a id="_CPPv416audio_dec_type_t"></a>

<a id="_CPPv316audio_dec_type_t"></a> <a id="_CPPv216audio_dec_type_t"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344"></a> enum audio\_dec\_type\_t
:   *Values:*

    <a id="_CPPv4N16audio_dec_type_t22AUDIO_DEC_TYPE_INVALIDE"></a>

    <a id="_CPPv3N16audio_dec_type_t22AUDIO_DEC_TYPE_INVALIDE"></a> <a id="_CPPv2N16audio_dec_type_t22AUDIO_DEC_TYPE_INVALIDE"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344a7c90fe7c7bd7bbd23141057166ba9de5"></a> enumerator AUDIO\_DEC\_TYPE\_INVALID

    <a id="_CPPv4N16audio_dec_type_t18AUDIO_DEC_TYPE_PCME"></a>

    <a id="_CPPv3N16audio_dec_type_t18AUDIO_DEC_TYPE_PCME"></a> <a id="_CPPv2N16audio_dec_type_t18AUDIO_DEC_TYPE_PCME"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344ad1addc1e051ff9f2009bf6499cc90b1a"></a> enumerator AUDIO\_DEC\_TYPE\_PCM

    <a id="_CPPv4N16audio_dec_type_t20AUDIO_DEC_TYPE_G711AE"></a>

    <a id="_CPPv3N16audio_dec_type_t20AUDIO_DEC_TYPE_G711AE"></a> <a id="_CPPv2N16audio_dec_type_t20AUDIO_DEC_TYPE_G711AE"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344af628b278f6beb440cc3a4ff9fc356526"></a> enumerator AUDIO\_DEC\_TYPE\_G711A

    <a id="_CPPv4N16audio_dec_type_t20AUDIO_DEC_TYPE_G711UE"></a>

    <a id="_CPPv3N16audio_dec_type_t20AUDIO_DEC_TYPE_G711UE"></a> <a id="_CPPv2N16audio_dec_type_t20AUDIO_DEC_TYPE_G711UE"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344aac35813cd8f486212927e61030778f7c"></a> enumerator AUDIO\_DEC\_TYPE\_G711U

    <a id="_CPPv4N16audio_dec_type_t18AUDIO_DEC_TYPE_AACE"></a>

    <a id="_CPPv3N16audio_dec_type_t18AUDIO_DEC_TYPE_AACE"></a> <a id="_CPPv2N16audio_dec_type_t18AUDIO_DEC_TYPE_AACE"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344ab341c3c351eed4c373127bf8f82ab3b5"></a> enumerator AUDIO\_DEC\_TYPE\_AAC

    <a id="_CPPv4N16audio_dec_type_t20AUDIO_DEC_TYPE_ADPCME"></a>

    <a id="_CPPv3N16audio_dec_type_t20AUDIO_DEC_TYPE_ADPCME"></a> <a id="_CPPv2N16audio_dec_type_t20AUDIO_DEC_TYPE_ADPCME"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344a97b1256762ea35547c186ac6ac85c585"></a> enumerator AUDIO\_DEC\_TYPE\_ADPCM

    <a id="_CPPv4N16audio_dec_type_t18AUDIO_DEC_TYPE_LC3E"></a>

    <a id="_CPPv3N16audio_dec_type_t18AUDIO_DEC_TYPE_LC3E"></a> <a id="_CPPv2N16audio_dec_type_t18AUDIO_DEC_TYPE_LC3E"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344a22d5a7a1d4e9ea1f7019003ab211e203"></a> enumerator AUDIO\_DEC\_TYPE\_LC3

    <a id="_CPPv4N16audio_dec_type_t18AUDIO_DEC_TYPE_MP3E"></a>

    <a id="_CPPv3N16audio_dec_type_t18AUDIO_DEC_TYPE_MP3E"></a> <a id="_CPPv2N16audio_dec_type_t18AUDIO_DEC_TYPE_MP3E"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344a7c69a27fe4938dfbd0c375b894ec186d"></a> enumerator AUDIO\_DEC\_TYPE\_MP3

    <a id="_CPPv4N16audio_dec_type_t19AUDIO_DEC_TYPE_OPUSE"></a>

    <a id="_CPPv3N16audio_dec_type_t19AUDIO_DEC_TYPE_OPUSE"></a> <a id="_CPPv2N16audio_dec_type_t19AUDIO_DEC_TYPE_OPUSE"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344a8f1441967236c2d838b11e50e894e978"></a> enumerator AUDIO\_DEC\_TYPE\_OPUS

    <a id="_CPPv4N16audio_dec_type_t19AUDIO_DEC_TYPE_G722E"></a>

    <a id="_CPPv3N16audio_dec_type_t19AUDIO_DEC_TYPE_G722E"></a> <a id="_CPPv2N16audio_dec_type_t19AUDIO_DEC_TYPE_G722E"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344a49ee6ee84b8eab7736dec260dc6e0f75"></a> enumerator AUDIO\_DEC\_TYPE\_G722

    <a id="_CPPv4N16audio_dec_type_t18AUDIO_DEC_TYPE_WAVE"></a>

    <a id="_CPPv3N16audio_dec_type_t18AUDIO_DEC_TYPE_WAVE"></a> <a id="_CPPv2N16audio_dec_type_t18AUDIO_DEC_TYPE_WAVE"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344a871968cac46b1e63fdcfa5bf6c3849d8"></a> enumerator AUDIO\_DEC\_TYPE\_WAV

    <a id="_CPPv4N16audio_dec_type_t18AUDIO_DEC_TYPE_AMRE"></a>

    <a id="_CPPv3N16audio_dec_type_t18AUDIO_DEC_TYPE_AMRE"></a> <a id="_CPPv2N16audio_dec_type_t18AUDIO_DEC_TYPE_AMRE"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344a4ddb3fcc626cc154065faee6ea54215c"></a> enumerator AUDIO\_DEC\_TYPE\_AMR

    <a id="_CPPv4N16audio_dec_type_t19AUDIO_DEC_TYPE_USERE"></a>

    <a id="_CPPv3N16audio_dec_type_t19AUDIO_DEC_TYPE_USERE"></a> <a id="_CPPv2N16audio_dec_type_t19AUDIO_DEC_TYPE_USERE"></a> <a id="audio__types_8h_1ac78cb96b8bd3c06c5034c2c790be4344ab7ebb21342a09eb2126fed1905459943"></a> enumerator AUDIO\_DEC\_TYPE\_USER
    :   User private decoding type

<a id="_CPPv416audio_mem_type_t"></a>

<a id="_CPPv316audio_mem_type_t"></a> <a id="_CPPv216audio_mem_type_t"></a> <a id="audio__types_8h_1a1e020ad24f53f897b5fe9621576d2cbd"></a> enum audio\_mem\_type\_t
:   *Values:*

    <a id="_CPPv4N16audio_mem_type_t19AUDIO_MEM_TYPE_SRAME"></a>

    <a id="_CPPv3N16audio_mem_type_t19AUDIO_MEM_TYPE_SRAME"></a> <a id="_CPPv2N16audio_mem_type_t19AUDIO_MEM_TYPE_SRAME"></a> <a id="audio__types_8h_1a1e020ad24f53f897b5fe9621576d2cbda781892a84785a0b55fe58a5aa55048b2"></a> enumerator AUDIO\_MEM\_TYPE\_SRAM

    <a id="_CPPv4N16audio_mem_type_t20AUDIO_MEM_TYPE_PSRAME"></a>

    <a id="_CPPv3N16audio_mem_type_t20AUDIO_MEM_TYPE_PSRAME"></a> <a id="_CPPv2N16audio_mem_type_t20AUDIO_MEM_TYPE_PSRAME"></a> <a id="audio__types_8h_1a1e020ad24f53f897b5fe9621576d2cbda99268afdcb618aa0ffb33e1044e64f73"></a> enumerator AUDIO\_MEM\_TYPE\_PSRAM

    <a id="_CPPv4N16audio_mem_type_t25AUDIO_MEM_TYPE_AUDIO_HEAPE"></a>

    <a id="_CPPv3N16audio_mem_type_t25AUDIO_MEM_TYPE_AUDIO_HEAPE"></a> <a id="_CPPv2N16audio_mem_type_t25AUDIO_MEM_TYPE_AUDIO_HEAPE"></a> <a id="audio__types_8h_1a1e020ad24f53f897b5fe9621576d2cbdad43b016311c6c53a8053e48693d63748"></a> enumerator AUDIO\_MEM\_TYPE\_AUDIO\_HEAP

<a id="_CPPv416audio_buf_type_t"></a>

<a id="_CPPv316audio_buf_type_t"></a> <a id="_CPPv216audio_buf_type_t"></a> <a id="audio__types_8h_1a5a7a63612a1b170b2b5b6a184b5634d0"></a> enum audio\_buf\_type\_t
:   *Values:*

    <a id="_CPPv4N16audio_buf_type_t17AUDIO_BUF_TYPE_RBE"></a>

    <a id="_CPPv3N16audio_buf_type_t17AUDIO_BUF_TYPE_RBE"></a> <a id="_CPPv2N16audio_buf_type_t17AUDIO_BUF_TYPE_RBE"></a> <a id="audio__types_8h_1a5a7a63612a1b170b2b5b6a184b5634d0a46140d62bc5554c29e4384a9f55794e0"></a> enumerator AUDIO\_BUF\_TYPE\_RB

    <a id="_CPPv4N16audio_buf_type_t17AUDIO_BUF_TYPE_FBE"></a>

    <a id="_CPPv3N16audio_buf_type_t17AUDIO_BUF_TYPE_FBE"></a> <a id="_CPPv2N16audio_buf_type_t17AUDIO_BUF_TYPE_FBE"></a> <a id="audio__types_8h_1a5a7a63612a1b170b2b5b6a184b5634d0ac5e5618cfb879821174458c9a545e3dc"></a> enumerator AUDIO\_BUF\_TYPE\_FB
