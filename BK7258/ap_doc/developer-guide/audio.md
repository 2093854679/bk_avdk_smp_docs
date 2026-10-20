---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/audio/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 音频应用开发

> **音频相关功能组件列表及其功能说明**
>
> | 组件名 | 功能说明 | 状态 |
> | --- | --- | --- |
> | bk\_audio\_player | 针对FreeRTOS系统设计的简易音频播放器：   1. 支持多种音频格式播放（MP3、WAV、AAC等） 2. 支持网络和本地歌曲 3. 支持播放列表的管理 4. 支持播放控制（播放、暂停、停止、上/下一曲等） | 维护中 |
> | audio\_algorithm | 音频算法库的测试组件，后续移至算法库的测试工程中， 不建议客户使用 | 废弃 |
> | audio\_codec | 音频编解码算法库测试组件，后续移至音频编解码库的 测试工程中，不建议客户使用 | 废弃 |
> | audio\_play | 基于audio驱动实现的pcm流播放组件，不建议客户使用 | 不推荐 |
> | audio\_record | 基于audio驱动实现的pcm流录音组件，不建议客户使用 | 不推荐 |
> | bk\_asr\_service | 语音识别服务组件，用于离线命令词识别功能 | 维护中 |
> | bk\_voice\_service | 语音通话服务组件，用于双向语音通话 | 维护中 |
> | bk\_player\_service | 播放器服务组件，用于提示音播放 | 维护中 |
> | bk\_audio | 音频开发框架，用于音频应用的开发 | 维护中 |

- [音频开发指南](audio/developer_guide.md)
  - [**1\. 简介**](audio/developer_guide.md#id2)
- [音频开发框架](audio/audio_development_kit.md)
  - [框架](audio/audio_development_kit/audio_pipeline.md)
  - [音频流](audio/audio_development_kit/audio_streams.md)
  - [算法](audio/audio_development_kit/audio_algorithms.md)
  - [编码器](audio/audio_development_kit/audio_encoders.md)
  - [解码器](audio/audio_development_kit/audio_decoders.md)
  - [工具集](audio/audio_development_kit/audio_utils.md)
- [语音通话](audio/voice_service.md)
  - [**1\. 简介**](audio/voice_service.md#id2)
  - [**2\. 软件框架**](audio/voice_service.md#id4)
  - [**3\. 宏配置**](audio/voice_service.md#id5)
  - [**4\. 测试case及参考demo**](audio/voice_service.md#casedemo)
  - [**5\. 使用示例**](audio/voice_service.md#id6)
- [播放器服务](audio/player_service.md)
  - [**1\. 简介**](audio/player_service.md#id2)
  - [**2\. 软件框架**](audio/player_service.md#id4)
  - [**2\. 宏配置**](audio/player_service.md#id5)
  - [**3\. 测试case及参考demo**](audio/player_service.md#casedemo)
  - [**4\. 典型示例**](audio/player_service.md#id6)
  - [**5\. 插播示例**](audio/player_service.md#id9)
- [音频播放器](audio/audio_player.md)
  - [**1\. 简介**](audio/audio_player.md#id2)
  - [**2\. 宏配置**](audio/audio_player.md#id4)
  - [**3\. 内置插件**](audio/audio_player.md#id5)
  - [**4\. 使用示例**](audio/audio_player.md#id6)
- [语音识别服务](audio/asr_service.md)
  - [**1\. 简介**](audio/asr_service.md#id2)
  - [**2\. 软件框架**](audio/asr_service.md#id4)
  - [**3\. 宏配置**](audio/asr_service.md#id5)
  - [**4\. 示例说明**](audio/asr_service.md#id6)
  - [**6\. 常见问题**](audio/asr_service.md#id7)
