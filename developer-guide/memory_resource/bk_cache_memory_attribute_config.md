---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/memory_resource/bk_cache_memory_attribute_config.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bk7259-cache"></a>

<a id="bk-cache-memory-attribute-config"></a>

# BK7259 Cache 配置与内存属性说明

<a id="id1"></a>

## 1\. 当前策略概述

BK7259 采用 AP \+ CP 双系统架构。当前推荐的 cache 与内存属性策略是：

> - **SRAM 默认 non-cacheable**：AP/CP 运行时 SRAM、共享 SRAM 窗口以及 AP HSRAM heap
>   默认不经过 cache，适合承载系统关键数据和对确定性要求较高的数据。
> - **普通 PSRAM heap 默认 non-cacheable**：客户通过 `psram_malloc` 申请的 AP PSRAM
>   默认不经过 cache，适合网络、音频、视频、显示、AI 等普通业务 buffer。
> - **PSRAM task 相关内部分配使用 cacheable PSRAM**：当工程启用 PSRAM task 时，
>   OS 内部使用 `AP_PSRAM_CACHE_HEAP` 分配 PSRAM task 相关内存，以提升 CPU 访问性能；
>   fast boot 场景下 TCB 仍保留在 default heap。
> - **L2 cache 默认开启，L1 D-cache 默认关闭**：当前方案通过开启 L2 cache 保留
>   cacheable task stack 的性能收益，并由硬件维护 AP SMP CPU 间的一致性；普通模块数据
>   默认 non-cacheable，因此 `CONFIG_CACHE_MAINTENANCE` 默认关闭，客户业务通常不需要手动
>   clean/invalidate buffer。
> - **系统级 cache 操作由平台维护**：boot、MPU/cache 初始化、低功耗和 CPU hotplug 等场景由
>   SDK 平台层处理，客户应用无需直接参与。

该策略的目标是在保留 AP SMP 任务栈性能的同时，让大部分业务内存保持 non-cacheable，
减少跨 CPU、DMA 和外设 master 之间的 cache 一致性负担。

<a id="cp"></a>

## 2\. CP 侧内存规划

CP 侧主要承载通信、协议栈和低功耗常驻控制逻辑。当前设计优先使用 SRAM，默认不使用
PSRAM，以减少 PSRAM 常开带来的功耗开销；`CP_PSRAM_HEAP` 仅作为备用扩展资源：

| 区域 | cache 属性 | 用途 |
| --- | --- | --- |
| `CP_RAM` | non-cacheable | CP 运行时 RAM，承载 CP 侧代码、数据、默认 heap、任务栈和系统上下文。 |
| `SWAP` | non-cacheable | AP/CP 固定共享 SRAM 窗口，用于 mailbox、IPC 控制面等小型共享数据。 |
| `CP_PSRAM_HEAP` | non-cacheable | CP 备用 PSRAM heap，仅在 SRAM 不足且业务允许 PSRAM 常开时使用，具体大小由工程 `ram_regions.csv` 配置。 |

CP 侧客户代码通常不需要关注 cache maintenance。若确需使用 CP PSRAM，应结合低功耗策略评估
PSRAM 常开功耗和掉电风险，不建议把必须长期保持的任务上下文或关键控制状态放在可能掉电的
PSRAM 中。

<a id="ap"></a>

## 3\. AP 侧内存规划

AP 侧承载主要应用、多媒体、AI 和 UI 业务。AP 内存规划同时使用 SRAM、HSRAM 和 PSRAM：

| 区域 | cache 属性 | 用途 |
| --- | --- | --- |
| `AP_RAM` | non-cacheable | AP 运行时 RAM，承载 AP 侧代码、数据、默认 heap、TCB、kernel object 和中断上下文。 |
| `AP_HSRAM_HEAP` | non-cacheable | AP 专用高速 SRAM heap，通过 `hsram_malloc` 申请，适合对访问延迟敏感的 buffer。 |
| `AP_PSRAM_HEAP` | non-cacheable | AP 默认 PSRAM heap，通过 `psram_malloc` / `psram_zalloc` 申请，适合普通业务大块内存。 |
| `AP_PSRAM_CACHE_HEAP` | L2 write-back cacheable | AP cacheable PSRAM heap，仅由 OS task 创建路径用于 PSRAM task 相关分配。 |
| `AP_PSRAM_CODE_SECTION` | cacheable | AP PSRAM 代码段或执行相关区域，具体是否使用由工程链接配置决定。 |

客户应用申请普通数据 buffer 时，优先使用 `os_malloc`、`psram_malloc` 或 `hsram_malloc`。
`psram_cache_malloc` 不作为客户业务 buffer 接口使用，它由 OS task 创建流程内部使用。

<a id="id2"></a>

## 4\. 任务栈与普通数据的区别

BK7259 当前方案将 task stack 和普通业务数据分开处理：

| 类型 | 推荐内存 | 说明 |
| --- | --- | --- |
| 普通业务数据 | `AP_RAM` / `AP_HSRAM_HEAP` / `AP_PSRAM_HEAP` | 默认 non-cacheable，适合被 CPU、DMA、显示、音视频、AI 等模块访问。 |
| AP task stack | `AP_RAM` 或 `AP_PSRAM_CACHE_HEAP` | SRAM task stack 默认 non-cacheable；PSRAM task stack 由 OS 内部分配到 cacheable heap。 |
| TCB / kernel object | `AP_RAM` / 默认 heap / `AP_PSRAM_CACHE_HEAP` | fast boot 场景下 PSRAM task 的 TCB 保留在 default heap；非 fast boot 场景下， PSRAM task 相关内部分配使用 cacheable heap。 |

当工程开启 `CONFIG_TASK_STACK_IN_PSRAM` 后，PSRAM task 相关内存的 cacheable 属性由
SDK 内部处理。客户应用只需要按正常方式创建任务，不需要直接申请
`AP_PSRAM_CACHE_HEAP`。

<a id="id3"></a>

### 栈内变量使用限制

警告

开启 PSRAM task stack 后，AP task stack 位于 cacheable PSRAM。客户应用 **禁止**
将栈上的局部变量、局部数组或结构体作为 DMA、CP、GPU、NPU、Wi-Fi、BT、display、
audio/video codec 等第三方 master 的数据 buffer 使用，也 **禁止** 把栈地址保存给
异步流程在函数返回后继续访问。

需要与第三方 master 共享的数据，应使用默认 non-cacheable heap 或对应模块提供的专用
buffer 申请接口。栈内变量只适合当前 CPU 同步访问，不适合作为跨 master、异步或硬件访问的数据载体。

<a id="id4"></a>

## 5\. 关键配置项

| 配置项 | 说明 |
| --- | --- |
| `CONFIG_L2_CACHE_ENABLE` | 控制 L2 cache 能力。当前方案保留 L2，用于 PSRAM task stack 等 AP 内部高频访问场景。 |
| `CONFIG_DCACHE` | 控制 AP L1 D-cache。当前 AP 产品配置通常不开 L1 D-cache，应以工程 defconfig 为准。 |
| `CONFIG_CACHE_MAINTENANCE` | 控制业务 per-buffer cache clean/invalidate API 是否默认启用。当前方案下默认关闭。 |
| `CONFIG_TASK_STACK_IN_PSRAM` | 控制任务栈是否允许放入 PSRAM。启用后，PSRAM task 相关内存由 OS 内部分配到 `AP_PSRAM_CACHE_HEAP`；fast boot 场景下 TCB 仍保留在 default heap。 |

需要注意，关闭 `CONFIG_CACHE_MAINTENANCE` 不等于关闭平台内部所有 cache 操作。启动、
低功耗、MPU/cache 初始化以及 CPU hotplug 所需的系统级 cache 处理仍由 SDK 保留。

<a id="id5"></a>

## 6\. 客户使用建议

客户开发应用或组件时，建议按以下方式选择内存：

| 场景 | 建议 |
| --- | --- |
| 小块控制数据、状态机、普通对象 | 使用 `os_malloc` 或默认 heap。 |
| AP 侧大块业务 buffer | 使用 `psram_malloc`；该内存默认 non-cacheable，通常不需要手动维护 cache。 |
| 对访问延迟敏感的 AP buffer | 使用 `hsram_malloc`，具体可用空间取决于工程 `AP_HSRAM_HEAP` 配置。 |
| DMA、GPU、NPU、Wi-Fi、BT、display、audio/video codec 共享 buffer | 使用默认 non-cacheable 内存，避免业务层处理 cache 一致性。 |
| 任务栈 | 通过 SDK 的任务创建接口创建；不要将栈上变量作为第三方 master 的共享 buffer。 |
| PSRAM task 创建失败或内存不足 | 优先检查 `AP_PSRAM_CACHE_HEAP` 是否预留不足；根据任务数量和 stack size 调整 工程 `ram_regions.csv` 后 clean 编译。 |

普通客户应用不需要新增 `flush_dcache` 或手动调用 per-buffer clean/invalidate。若产品需要
自定义 cacheable 共享 buffer，应结合内存来源、访问 master、生命周期和低功耗策略进行专项设计。

若开启 `CONFIG_TASK_STACK_IN_PSRAM` 后出现任务创建失败、返回内存不足，或日志显示
PSRAM task 分配失败，应重点检查 `AP_PSRAM_CACHE_HEAP` 的大小。该区域承载
PSRAM task 相关内部分配，大小应覆盖同时存在的 PSRAM 任务栈峰值，并预留一定余量；
非 fast boot 场景还需考虑对应 TCB 等任务内部对象开销。调整方式是在
工程 `partitions/bk7259/ram_regions.csv` 中增大 `AP_PSRAM_CACHE_HEAP`；如果总 PSRAM
预算固定，需要相应压缩 `AP_PSRAM_HEAP`、`AP_PSRAM_CODE_SECTION` 或其它可调整区域，
同时保持相同 cache 属性的 PSRAM 分区尽量连续，避免超过 MPU region 数量限制。修改后建议
执行 clean 编译并通过 `memshow` 等命令确认各 heap 剩余空间。

<a id="cache"></a>

## 7\. 系统级 cache 操作说明

以下 cache 操作属于平台内部行为，客户应用通常不需要直接调用：

> - boot 阶段的 cache invalidate/flush，用于进入应用前清理 cache 状态。
> - MPU 或 cache enable/disable 前后的同步操作，用于保证内存属性切换安全。
> - 低功耗进出时的 cache 状态处理，用于配合 SRAM/PSRAM 保持或恢复。
> - CPU3 hotplug offline 前的 cache writeback，用于保证 cacheable task 内存或系统上下文在
>   CPU 下线前写回到可见内存。

这些系统级操作不受 `CONFIG_CACHE_MAINTENANCE` 控制。`CONFIG_CACHE_MAINTENANCE` 只用于
控制客户业务是否默认启用 per-buffer cache maintenance API。
