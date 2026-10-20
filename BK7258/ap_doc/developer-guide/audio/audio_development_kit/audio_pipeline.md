---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/audio/audio_development_kit/audio_pipeline.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# **框架**

<a id="id2"></a>

## **1\. 简介**

> 此音频开发框架基于pipeline结构设计，将最小单元的音频功能抽象为一个类，基于该类可以实例化一个个功能独立，彼此解耦的音频子功能模块。通过pipeline的方式将需要的音频子功能模块串联组合即可实现想要的音频功能应用。
>
> 基于ADK开发的音频应用整体框架如下图所示：

<a id="id5"></a>
![Audio Application Architecture](../../../../../../_assets/df739c783898be9b7d3a-audio_application_architecture.png)


Figure Audio Application Architecture

> 整个应用框架主要分为两层： `Audio App` 音频应用层和 `Audio Development Kit` 音频开发框架层。
>
> > - `Audio App` 层属于基于ADK开发的多媒体应用层，例如：音频播放器、录音机、语音通话等。客户的应用开发工作主要集中在这一层。
> > - `Audio Development Kit` 层包含 `Audio Pipeline` 管道架构和 `Audio Element` 功能模块。SDK发布时会适配常用的功能模块，所以通常情况下客户不需要修改这一层的代码。
>
> 如果现有的功能模块无法满足客户的需求，客户也可以基于模块类，并参考其他已有的功能模块自行适配新的功能模块。

<a id="id3"></a>

## **2\. 音频开发框架**

> 如上图所示，`Audio Pipeline` 管道架构是整个音频开发框架的核心，负责音频组件的串联控制、消息调度，并向上层应用提供API，客户仅需要了解API接口的使用，不需要对其进行开发。
>
> `Audio Element` 功能模块根据根据组件功能划分主要有以下几类：
> :   - Streams：流组件，主要负责音频流数据的输入输出，如mic、speaker、sdcard等。
>     - Encoders：编码器组件，主要负责音频数据流的编码，如g711a、g711u、adpcm、aac等。
>     - Decoders：解码器组件，主要负责音频数据流的解码，如g711a、g711u、adpcm、mp3、opus、aac等。
>     - Algorithms：算法组件，主要负责音频数据流的算法处理，如AEC、ns等。
>
> 功能组件通过 `Audio Port` 接口模块进行串联组成pipeline。 `Audio Port` 模块主要负责模块间数据的传输和缓存，支持以下几种方式：
> :   - callback：通过模块初始化注册的callback输入输出数据。
>     - ringbuffer：通过ringbuffer读写数据（copy数据到模块内部的buffer使用），ringbuffer的size由模块初始化时配置的输出size决定。
>     - framebuffer：通过framebuffer读写数据，framebuffer的配置由模块初始化时配置的输出size决定。

<a id="id4"></a>

## **3\. 音频应用示例**

> 如下图所示，常见的音频上下行应用都可以通过pipeline架构来实现。
>
> 例如录音到文件的功能，基于onboard\_mic\_stream和vfs\_stream组件构建一个record Pipeline即可实现。

<a id="id6"></a>
![Audio Uplink Examples](../../../../../../_assets/9084b3c77b82b67798a8-audio_uplink_examples.png)


Figure Audio Uplink Examples

<a id="id7"></a>
![Audio Downlink Examples](../../../../../../_assets/44894f06b4c691a4d500-audio_downlink_examples.png)


Figure Audio Downlink Examples
