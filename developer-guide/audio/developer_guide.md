---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/audio/developer_guide/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# **音频应用开发指南**

<a id="id2"></a>

## **1\. 简介**

> 本文档是音频应用开发的 `必读文档` 。
>
> 为方便客户使用音频功能，避免直接调用驱动接口开发，降低音频应用的开发难度， `<source code>/ap/components/` 路径下已经提供了一些常见的音频功能组件，例如：录音、播放、语音通话等。
>
> 同时为了满足客户多元化的音频应用需求，也提供了音频开发框架，该框架基于pipeline结构设计，将常见的音频功能封装成一个个独立的功能子模块，客户可以基于该框架，直接调用子功能模块开发自己的音频应用。

## 模块导航

- [快速入门](../../get-started.md)
- [开发者指南](../../developer-guide.md)
- [AP(SMP)+CP架构](../architecture.md)
- [系统启动流程](../system_boot.md)
- [音频](../audio.md)
- [音频开发框架](audio_development_kit.md)
- [语音通话](voice_service.md)
- [播放器服务](player_service.md)
- [语音识别服务](asr_service.md)
- [配置工具](../config_tools.md)
- [内存资源](../memory_resource.md)
- [中断管理](../interrupt.md)
- [多核通讯](../multicore_communication.md)
- [外设资源](../peripheral_resource.md)
- [构建系统](../build_config.md)
- [新建工程介绍](../create_new_project_rule.md)
