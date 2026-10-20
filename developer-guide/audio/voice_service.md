---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/audio/voice_service/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# **语音通话服务**

<a id="id2"></a>

## **1\. 简介**

> 语音通话服务组件是基于ADK语音开发框架设计实现的。
>
> 支持aec回声消除功能。
>
> 支持多种数据格式，如：G711A/U、pcm、AAC、G722等。由于组件是基于语音开发框架设计，客户如需其他数据格式，可自行适配。
>
> 支持板载模拟mic、uac mic、板载模拟speaker和uac speaker。
>
> 支持设置speaker数据缓存池子，避免因网络卡顿、读写较慢等原因导致的播放卡顿问题。

- 有关语音通话服务的API参考，请参阅：

  - [语音通话服务API参考](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/voice_service/index.html)
- 有关语音通话服务的示例工程，请参阅：

  - [语音通话服务示例工程](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/examples/projects/voice_service_example/index.html)

<a id="id4"></a>

## **2\. 软件框架**

> 软件框架如下图所示（图示资源待补充）：
>
> - Figure Voice Service Architecture
>
> 语音通话服务由三个服务构成：voice\_service、voice\_read\_service和voice\_write\_service。
>
> voice\_service为语音通话服务组件的核心功能。内部创建了两个pipeline，分别是 `record_pipeline` 和 `play_pipeline` :
>
> > - `record_pipeline` 为上行录音pipeline，负责mic数据的采集、aec回声消除和音频编码。
> > - `play_pipeline` 为下行播放pipeline，负责speaker数据的解码和播放。
>
> voice\_read\_service为mic数据读服务，通过注册mic数据回调接口，可实现mic数据的主动上报，为推流模式。
>
> voice\_write\_service为speaker数据写服务，支持内部创建一个缓存池，实现对speaker数据的缓存播放。

备注

1. 直接使用voice\_service提供的api接口也可以实现语音通话功能，但是此服务提供给的读取mic数据的接口 `bk_voice_read_mic_data` 和写speaker数据的接口 `bk_voice_write_spk_data` 都为阻塞调用接口，工作模式为拉流模式。
2. `onboard_speaker_stream` 模块提供了音量设置接口，可通过 `bk_voice_get_spk_element` 接口获取speaker元素句柄，然后通过 `audio_element_set_digital_gain` 和 `audio_element_set_analog_gain` 接口设置音量。
3. BK7259 在板载通话场景中使用 `onboard_mic_stream/v2.0` 与 `onboard_speaker_stream/v2.0` 实现，不使用 `onboard_mic_stream/v1.0`、`onboard_speaker_stream/v1.0`，也不使用 `onboard_dual_dmic_mic_stream` 目录下实现。

重要

组件支持用户自定义的音频编解码器，详细步骤如下：
:   1. 用户可以根据需要参考音频开发框架下其他的编解码器实现，开发自定义的音频编解码器;
    2. 配置 `voice_cfg_t.enc_type=AUDIO_ENC_TYPE_USER`, 和 `voice_cfg_t.dec_type=AUDIO_DEC_TYPE_USER`;
    3. 配置 `voice_cfg_t.voice_enc_init` , `voice_cfg_t.voice_dec_init` , `voice_cfg_t.enc_args` 和 `voice_cfg_t.dec_args` ，将自定义的音频编解码器创建注册到语音通话组件中。

<a id="id5"></a>

## **3\. 宏配置**

> 功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_VOICE\_SERVICE | AP | bool | y |
> | CONFIG\_VOICE\_READ\_SERVICE | AP | bool | y |
> | CONFIG\_VOICE\_WRITE\_SERVICE | AP | bool | y |
>
> 依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |
> | CONFIG\_ADK\_RAW\_STREAM | AP | bool | y |
> | CONFIG\_ADK\_ONBOARD\_MIC\_STREAM | AP | bool | y |
> | CONFIG\_ADK\_ONBOARD\_SPEAKER\_STREAM | AP | bool | y |
> | CONFIG\_ADK\_G711\_ENCODER | AP | bool | y |
> | CONFIG\_ADK\_G711\_DECODER | AP | bool | y |
> | CONFIG\_ADK\_AEC\_V3\_ALGORITHM | AP | bool | y |

备注

1. 组件默认支持板载模拟mic、板载模拟speaker、AEC回声消除、G711A/U编解码功能，依赖的宏配置仅列举了默认依赖。
2. 如果需要支持AAC编解码、G722编解码、uac mic、uac speaker等功能，参考音频开发框架中的组件模块说明，打开对应的功能宏以及对应的组件功能宏即可。

<a id="casedemo"></a>

## **4\. 测试case及参考demo**

> 组件提供了模块测试case和参考使用demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_voice_service/cli/`
>
> demo基于语音通话组件，读取mic数据，并将数据写入speaker播放，实现自回环测试。

备注

1. `bk_avdk_smp<源代码路径>/ap/include/components/bk_voice_service_types.h` 提供了常用方案的默认配置参考，可参阅语音通话服务的API文档。

<a id="id6"></a>

## **5\. 使用示例**

> 以典型的应用场景：板载语音通话（8K采样率，支持G711A编解码、AEC回声消除）为示例说明语音通话组件使用流程。

<a id="id7"></a>

### 打开语音通话

打开语音通话的流程如下：
:   1. 初始化语音通话组件。
    2. 初始化语音通话组件的mic数据读服务。
    3. 初始化语音通话组件的speaker数据写服务。
    4. 启动语音通话组件。
    5. 启动语音通话组件的mic数据读服务。
    6. 启动语音通话组件的speaker数据写服务。

以下为代码示例

```
/* init voice service */
voice_cfg_t voice_cfg = DEFAULT_VOICE_BY_ONBOARD_MIC_SPK_CONFIG();
voice_handle_t voice_handle = bk_voice_init(&voice_cfg);
if (!voice_handle)
{
    LOGE("voice init fail\n");
    return BK_FAIL;
}

/* init voice read service */
voice_read_cfg_t voice_read_cfg = VOICE_READ_CFG_DEFAULT();
voice_read_cfg.voice_handle = voice_handle;
voice_read_cfg.max_read_size = 1280;
voice_read_cfg.voice_read_callback = doorbell_udp_voice_send_callback;  //doorbell_udp_voice_send_callback mic data caalback
voice_read_handle_t voice_read_handle = bk_voice_read_init(&voice_read_cfg);
if (!voice_read_handle)
{
    LOGE("voice read init fail\n");
    return BK_FAIL;
}

/* init voice write service */
voice_write_cfg_t voice_write_cfg = VOICE_WRITE_CFG_DEFAULT();
voice_write_cfg.voice_handle = voice_handle;
voice_write_handle_t voice_write_handle = bk_voice_write_init(&voice_write_cfg);
if (!voice_write_handle)
{
    LOGE("voice write init fail\n");
    return BK_FAIL;
}

/* start voice service */
if (BK_OK != bk_voice_start(voice_handle))
{
    LOGE("voice start fail\n");
    return BK_FAIL;
}

/* start voice read service */
if (BK_OK != bk_voice_read_start(voice_read_handle))
{
    LOGE("voice read start fail\n");
    return BK_FAIL;
}

/* start voice write service */
if (BK_OK != bk_voice_write_start(voice_write_handle))
{
    LOGE("voice write start fail\n");
    return BK_FAIL;
}
```

<a id="id8"></a>

### 关闭语音通话

关闭语音通话的流程如下：
:   1. 停止语音通话组件的mic数据读服务。
    2. 停止语音通话组件的speaker数据写服务。
    3. 停止语音通话组件。
    4. 释放语音通话组件的mic数据读服务。
    5. 释放语音通话组件的speaker数据写服务。
    6. 释放语音通话组件。

以下为代码示例

```
/* stop voice read service */
bk_voice_read_stop(voice_read_handle);

/* stop voice write service */
bk_voice_write_stop(voice_write_handle);

/* stop voice service */
bk_voice_stop(voice_handle);

/* deinit voice read service */
bk_voice_read_deinit(voice_read_handle);

/* deinit voice write service */
bk_voice_write_deinit(voice_write_handle);

/* deinit voice service */
bk_voice_deinit(voice_handle);
```
