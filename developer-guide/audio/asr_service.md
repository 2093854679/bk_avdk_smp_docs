---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/audio/asr_service/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# **语音识别服务**

<a id="id2"></a>

## **1\. 简介**

> 语音识别服务组件是基于ADK语音开发框架设计实现的，提供语音识别(ASR)功能。
>
> 支持 BEKEN\_KWS（TFLite-Micro \+ NPU）及 Wanson 等 ASR 引擎。
>
> 支持音频数据重采样功能，可根据不同ASR引擎的需求进行采样率转换。
>
> 支持板载麦克风、UAC设备或通过其他语音服务获取音频数据等多种输入模式。

备注

1. 用户可以使用统一的API接口来配置和控制ASR服务，无需关注具体的ASR引擎实现。

- 有关语音识别服务的API参考，请参阅：

  - [语音识别服务API参考](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/asr_service/index.html)
- 有关语音识别服务的示例工程，请参阅：

  - [语音识别服务示例工程](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/examples/projects/asr_service_example/index.html)

<a id="id4"></a>

## **2\. 软件框架**

> 语音识别服务主要功能包括：
>
> > - 音频数据采集：支持直接从麦克风采集(如Figure1)或从语音服务获取音频数据(如Figure2)。
> > - 音频数据处理：提供重采样功能，确保音频数据符合ASR引擎的输入要求。
> > - 语音识别：将处理后的音频数据送入ASR引擎进行语音识别。
>
> 软件框架如下图所示（图示资源待补充）：
>
> - Figure1 ASR Service Architecture
> - Figure2 ASR Service Architecture

备注

1. 当前软件版本语音识别服务例举了两种工作模式：直接使用麦克风进行录音识别，或通过语音服务获取音频数据进行识别。用户可根据实际应用场景,对asr的工作模式进行其他配置。
2. 不同的ASR引擎可能对音频数据的格式和采样率有特定要求，可通过配置进行适配；BEKEN\_KWS / Wanson 通常要求 16 位 PCM、采样率 16000Hz。

<a id="id5"></a>

## **3\. 宏配置**

> 功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ASR\_SERVICE | AP | bool | y |
>
> 依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |
> | CONFIG\_ADK\_RAW\_STREAM | AP | bool | y |
> | CONFIG\_ADK\_ONBOARD\_MIC\_STREAM | AP | bool | y |
> | CONFIG\_BEKEN\_KWS | AP | bool | y |
> | CONFIG\_TFLITE\_MICRO | AP | bool | y |
> | CONFIG\_NPU | AP | bool | y |

备注

1. 如果需要支持AEC及重采样等功能，参考音频开发框架中的组件模块说明，打开对应的功能宏以及对应的组件功能宏即可。

<a id="id6"></a>

## **4\. 示例说明**

> 具体示例可参见asr\_service\_example工程。

<a id="id7"></a>

## **6\. 常见问题**

> **Q: 采样率如何选择？**
>
> A: 根据使用的ASR引擎要求选择合适的采样率，通常为8kHz或16kHz。
>
> **Q: 如何处理ASR识别结果？**
>
> A: 通过注册回调函数接收ASR识别结果，具体可参考API文档中的回调函数设置方法。
