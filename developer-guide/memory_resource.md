---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/memory_resource/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 内存资源

<a id="id2"></a>

## 内存概述

BK7259 SMP 代码库的内存规划需要同时理解 **SoC 地址映射**、**工程生成的 RAM/Flash 分区** 以及 **AP/CP 独立链接** 三方面的结果。

| 类型 | 说明 |
| --- | --- |
| Flash | 存放 CP/AP 独立镜像、OTA、KV（EasyFlash）等；由分区表生成，详见 [分区表配置](create_new_project_rule/bk_configure_partition_Table.md) |
| SRAM | 片上主 RAM，bank 覆盖 `0x28000000`–`0x281DFFFF`；通过 `SOC_S_NS_ADDR_DIFF` 提供 Secure/Non-Secure 别名 |
| HSRAM | 从 SRAM 划出的 **AP 专用辅助堆** （`AP_HSRAM_HEAP`）；独立 `hsram_malloc` 池，详见下文 |
| PSRAM | 片外扩展内存，可划分 heap/slab/section；低功耗场景可能掉电，使用约束见下文 |
| SWAP 共享窗口 | AP/CP 固定共享 SRAM（链接脚本 `.shared_memory` 为 1024 字节），用于 Mailbox/IPC 控制面 |

架构层面的资源划分与调试入口见 [AP(SMP)\+CP 架构](architecture.md) 中「资源划分」与「系统调试」章节。

<a id="sram"></a>

## SRAM 概述

> - BK7259 采用 AP \+ CP 架构，两侧 **独立编译、独立链接**，各自生成 `ram_regions.h` 与链接脚本。
> - 典型 SRAM 区域（doorbell 工程）包括 `CP_RAM`、`SWAP`、`AP_HSRAM_HEAP`、`AP_RAM`；实际地址与大小以工程构建输出为准。
> - AP 与 CP 链接脚本均将 `SWAP` 绑定到 `CONFIG_SWAP_ADDR`，并要求 `.shared_memory` 固定 **1024** 字节。
> - 调整 AP/CP SRAM 归属：修改工程 `ram_regions.csv` 后重新生成，详见 [RAM资源分区配置](config_tools/bk_config_ram_regions.md#bk-config-ram-regions)。

当前 doorbell 基线 SRAM 布局（摘录）：

| 区域 | 地址（示例） | 大小（示例） | 角色 |
| --- | --- | --- | --- |
| `CP_RAM` | `0x28000000` | `0x5F000` | CP 运行时 RAM |
| `SWAP` | `0x2805F000` | `0x1000` | AP/CP 共享窗口 |
| `AP_HSRAM_HEAP` | `0x28100000` | `0x80000` | AP HSRAM 辅助堆 （见下文 HSRAM 概述） |
| `AP_RAM` | `0x28180000` | `0x60000` | AP 运行时 RAM |

<a id="hsram"></a>

## HSRAM 概述

HSRAM （High-Speed SRAM）在 BK7259 工程中指从片上 **SRAM 地址空间** 划出的 **AP 专用辅助堆区域**。
链接与配置项名通常为 `AP_HSRAM_HEAP`，构建后生成 `CONFIG_AP_HSRAM_HEAP_ADDR` / `CONFIG_AP_HSRAM_HEAP_SIZE`。

它与 `AP_RAM`、`CP_RAM` 同属 SRAM bank，但作为\*\*独立堆\*\*管理：`hsram_malloc` 只从该区域分配，不会与 AP 默认 heap （`os_malloc`）互相回落。

> - **仅 AP 侧**：CP 无 HSRAM 堆；区域在 `ram_regions.csv` 中由 AP 工程声明
> - **分配接口**：`hsram_malloc` / `hsram_zalloc` / `hsram_free`；任务栈可选用 `rtos_create_hsram_thread`
> - **典型用途**：多媒体 Flexa 行缓冲、编解码/GPU/ISP/ASR 等与 DMA 协作、对延迟敏感的 buffer
> - **与 PSRAM 区别**：仍在片上 SRAM，访问延迟低于 PSRAM；是否参与低功耗掉电需结合工程 PM 策略评估

若工程未配置 `AP_HSRAM_HEAP`，则 `hsram_malloc` 与 `rtos_create_hsram_thread` 不可用。
API 与调试说明见 AP 文档「操作系统与内存管理」中的 `bk_mem` 章节。

<a id="psram"></a>

## PSRAM 概述

> - PSRAM 通常划分为 CP heap、AP heap、多媒体 slab（audio/encode/display 等）及 AP section 段，具体条目在 `ram_regions.csv` 中配置。
> - CP 侧：PSRAM 仅适合动态申请后及时释放的场景（如动态 Log）；不应将长期运行的 task、queue 或代码放入可能掉电的 PSRAM。
> - AP 侧：多媒体、大 buffer 的主要承载区；需同时评估 DMA 可见性、cache 同步与低功耗掉电策略。
> - 驱动与 API 细节请参考 AP 文档中的 PSRAM 使用指南（`ap_doc` 外设章节 `bk_psram`）。

<a id="id3"></a>

## 配置与排查

| 主题 | 参考 |
| --- | --- |
| RAM 区域生成 | [RAM资源分区配置](config_tools/bk_config_ram_regions.md#bk-config-ram-regions) |
| 自动分区 / Flash 布局 | [分区表配置](create_new_project_rule/bk_configure_partition_Table.md)、[自动分区](config_tools/bk_config_auto_partitions.md#bk-config-auto-partitions) |
| 运行时查看 | CP 执行 memshow；AP 执行 ap\_cmd memshow（参见架构文档调试章节） |
| 模块静态占用 | Doorbell 示例中的 `size_map_total.csv` 统计，见下文专章 |

<a id="cache"></a>

## Cache 与内存属性

以下页面说明 BK7259 当前推荐的 SRAM/PSRAM cache 属性、系统级 cache 操作边界、
业务 per-buffer cache maintenance 开关以及模块迁移约束：

- [BK7259 Cache 配置与内存属性说明](memory_resource/bk_cache_memory_attribute_config.md)

<a id="doorbell"></a>

## Doorbell 示例

以下页面给出 **doorbell** 工程的 Flash/SRAM/PSRAM 完整布局、共享内存约束、DMA 边界与模块静态占用参考：

- [BK7259 Doorbell 内存架构](memory_resource/bk_doorbell_memory_map.md)
