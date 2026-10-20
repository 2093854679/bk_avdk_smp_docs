---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7258/zh_CN/v3.1.1/developer-guide/memory_resource/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: SMP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 内存资源

<a id="id2"></a>

## 内存概述

> - BK7258芯片整体有4M/8M/16M psram, 640K sram, CPU0、CPU1、CPU2各有独立的16k dtcm和16k itcm
> - 内存资源配置方法, 具体请参考 [RAM资源分区配置](config_tools/bk_config_ram_regions.md#bk-config-ram-regions)

<a id="sram"></a>

## SRAM概述

> - BK7258芯片当前为SMP架构, 包括AP和CP两个部分, 有640K sram。
> - 可以通过ram\_regions.csv中配置AP和CP的SRAM, 通过AP\_RAM和CP\_RAM项即可配置SRAM资源分配。

<a id="psram"></a>

## PSRAM概述

> 请参考 [PSRAM 使用指南](../ap_doc/developer-guide/peripheral/bk_psram.md)

## 模块导航

- [快速入门](../get-started.md)
- [开发者指南](../developer-guide.md)
- [AP(SMP)+CP架构](architecture.md)
- [配置工具](config_tools.md)
- [中断管理](interrupt.md)
- [多核通讯](multicore_communication.md)
- [外设资源](peripheral_resource.md)
- [以太网](ethernet.md)
- [构建系统](build_config.md)
- [新建工程介绍](create_new_project_rule.md)
