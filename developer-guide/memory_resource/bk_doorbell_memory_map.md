---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/memory_resource/bk_doorbell_memory_map.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bk7259-doorbell"></a>

# BK7259 Doorbell 内存架构

备注

本页将 `projects/multimedia/doorbell` 的项目级内存映射设计文档
集成到官方 BK7259 文档树中。文中的地址与边界来自当前 doorbell
构建输出、AP/CP 链接脚本、启动代码以及 SoC 寄存器头文件。

<a id="id1"></a>

## 范围说明

本页从以下五个角度描述当前 BK7259 `doorbell` 的内存架构：

- AP 与 CP 子系统拓扑
- 当前生成的 Flash 分区
- 当前生成的 SRAM 与 PSRAM 区域
- shared-memory 与 DMA 约束
- 启动流程与当前安全边界

本文中的数值属于当前 `doorbell` 工程基线，不应直接视为所有
BK7259 产品的固定规则。

<a id="id2"></a>

## 架构摘要

当前 BK7259 SMP 代码库采用 AP \+ CP 拆分：

- CP 是运行在 CPU0 与 CPU1 上的 SMP 子系统，并独立生成镜像
- AP 是运行在 CPU2 与 CPU3 上的 SMP 子系统，并独立生成镜像
- 两个子系统都从 `Reset_Handler_Core0` 进入，并在 primary core
  完成初始化后拉起本地 secondary core
- AP 与 CP 之间通过 mailbox IPC 和固定 `SWAP` SRAM 窗口交换控制
  数据

这里同时存在两套 core ID 视角：

- `portGET_CORE_ID()` 表示单个 SMP 镜像内部的逻辑 core ID，取值
  从 `0` 和 `1` 开始
- `rtos_get_core_id()` 返回 SoC 级物理 CPU ID，用于区分
  CPU0/CPU1/CPU2/CPU3

<a id="flash"></a>

## 当前 Flash 布局

当前生成的物理分区表如下：

| 区域 | 偏移 | 大小 | 用途 |
| --- | --- | --- | --- |
| `primary_cp_app` | `0x00000000` | `1224K` | CP 固件镜像 |
| `primary_ap_app` | `0x00132000` | `1700K` | AP 固件镜像 |
| `ota` | `0x002DB000` | `1360K` | OTA 暂存镜像 |
| `usr_config` | `0x0042F000` | `60K` | 用户配置区 |
| `easyflash` | `0x0043E000` | `8K` | CP KV 与日志区 |
| `easyflash_ap` | `0x00440000` | `8K` | AP KV 与日志区 |
| `sys_rf` | `0x007FE000` | `4K` | RF 数据 |
| `sys_net` | `0x007FF000` | `4K` | 网络数据 |

设计要点：

- CP 与 AP 继续保持独立可执行镜像
- OTA 规划应以生成后的分区输出为准，而不是只看链接器看到的代码段
- 当前布局仍保留了未来安全分区或产品变种所需的 Flash 余量

<a id="sram"></a>

## 当前 SRAM 布局

`ram_regions.h` 当前导出的 `doorbell` SRAM 划分如下：

| 区域 | 地址 | 大小 | 角色 |
| --- | --- | --- | --- |
| `CP_RAM` | `0x28000000` | `0x0005F000` | CP 运行时 RAM |
| `SWAP` | `0x2805F000` | `0x00001000` | 固定 AP/CP 共享 SRAM 窗口 |
| `AP_HSRAM_HEAP` | `0x28100000` | `0x00080000` | AP 辅助 heap |
| `AP_RAM` | `0x28180000` | `0x00060000` | AP 运行时 RAM |

同时，SoC 头文件还定义了 `0x28000000` 到 `0x281DFFFF` 的固定
SRAM bank 视图，并通过 `SOC_S_NS_ADDR_DIFF` 提供 Secure /
Non-Secure 地址别名。因此在做 TrustZone 内存审查时，必须显式区分
Secure、Non-Secure 与未来 NSC 的布局要求。

<a id="id3"></a>

## 模块 SRAM 静态占用参考

下表基于当前 `doorbell` 构建输出
`build/bk7259/doorbell/*/size_map_total.csv` 统计，口径为链接后
`ram = data + bss` 的静态 SRAM 占用。该表适合给客户评估各功能模块
在 CP/AP 两侧的基础 SRAM 需求；不包含运行时 heap、任务栈、DMA buffer、
网络包池、图像帧缓存、音频环形缓冲等动态内存。

| 模块 | CP SRAM | AP SRAM | 合计 | 统计范围 |
| --- | --- | --- | --- | --- |
| Wi-Fi | `55.9 KiB` | `0.6 KiB` | `56.5 KiB` | `libwifi`、`bk_wifi`、`wpa_supplicant`、`bk_phy`、 `controller_if`、`bk_coex`、AP `bk_wifi_driver` |
| BLE | `49.0 KiB` | `12.0 KiB` | `61.0 KiB` | CP BLE controller、AP BLE host、`bk_bluetooth`、`bt` |
| LwIP | `83.5 KiB` | `84.3 KiB` | `167.8 KiB` | `lwip_intf_v2_1` |
| GPU | `0 KiB` | `16.5 KiB` | `16.5 KiB` | `vg_lite_gpu`、`bk_gpu` |
| DPU | `0 KiB` | `0.6 KiB` | `0.6 KiB` | `libdpu` |
| ISP / Camera / Display / Video | `0 KiB` | `5.8 KiB` | `5.8 KiB` | `libisp`、`bk_camera`、`bk_display`、`bk_encoder`、 `bk_decoder`、`media_service`、`avdk_driver`、`vcenc`、 `vcdec`、`bk_uvc` |
| Audio / Voice | `0 KiB` | `4.3 KiB` | `4.3 KiB` | `audio_utils`、`audio_pipeline`、`voice_service`、 `aec_v3_algorithm`、`rsp_algorithm`、audio streams、 `resample`、`audio_osi` |
| USB | `0 KiB` | `6.9 KiB` | `6.9 KiB` | `bk_usb` |
| AI / ASR / KWS | `0 KiB` | `11.7 KiB` | `11.7 KiB` | `bk_tflite_micro`、`tensorflow-microlite`、`bk_asr_service`、 `kws_model` |

客户进行整机 SRAM 预算时，应在上述静态占用之外，再叠加实际业务配置下
的 task stack、heap watermark、Wi-Fi/LwIP 包池、camera/display frame
buffer、audio buffer 和 DMA 对齐预留。

<a id="shared-memory"></a>

## Shared Memory 与同步模型

AP 与 CP 两侧的链接脚本都定义了相同的共享内存契约：

- `SWAP` 起始地址为 `0x2805F000`，总大小为 `4K`
- `.shared_memory` 必须固定为 `1024` 字节
- `.swap_data` 使用 `SWAP` 剩余空间

推荐的使用方式如下：

- `.shared_memory` 只放紧凑型控制元数据
- camera、display、audio、network 等大负载数据不要放入 `SWAP`
- 共享分配器和共享对象必须使用 spinlock 保护
- shared-memory 元数据发布时应使用 `DMB` 保证顺序
- 修改 MPU 或执行属性后，如需架构级完成，应补充 `DSB/ISB`

<a id="psram"></a>

## 当前 PSRAM 布局

当前 PSRAM carve-out 的角色划分如下，实际地址和大小以工程构建生成的
`ram_regions.h` 为准：

| 区域 | cache 属性 | 角色 |
| --- | --- | --- |
| `CP_PSRAM_HEAP` | non-cacheable | CP 备用 heap 扩展，当前默认不使用 PSRAM 以节省功耗 |
| `AP_PSRAM_DATA_SECTION` | non-cacheable | AP 显式 PSRAM data 与 BSS |
| `AP_PSRAM_HEAP` | non-cacheable | AP 普通动态 heap，通过 `psram_malloc` / `psram_zalloc` 申请 |
| `AP_PSRAM_CACHE_HEAP` | L2 write-back cacheable | AP PSRAM task 相关内部分配，由 OS task 创建路径内部使用 |
| `AP_PSRAM_CODE_SECTION` | cacheable | AP 显式 PSRAM code 与 rodata |

对于当前 `doorbell` 基线：

- AP 主要将 PSRAM 用于动态运行时数据，而不是把所有代码都放入 PSRAM
- 普通 `AP_PSRAM_HEAP` 默认 non-cacheable，适合作为 camera、display、audio、
  network 等模块的大块业务 buffer 来源
- `AP_PSRAM_CACHE_HEAP` 仅用于 PSRAM task 相关内部分配，不作为客户业务 buffer 接口
- CP 默认优先使用 SRAM；如确需使用 `CP_PSRAM_HEAP`，应限制在临时或已经过明确审查的场景
- 解释 PSRAM 地址时，需要同时考虑 uncoded/data alias、coded alias
  以及子系统实际配置的 MPU 属性

<a id="dma-cache"></a>

## DMA 与 Cache 策略

Doorbell 是典型的 DMA 高负载工程，因为 camera、display、USB、
audio 与 network 路径都需要搬运大块 buffer。

建议遵循以下规则：

- 不要假设所有 PSRAM buffer 都天然 DMA-safe
- 对时延敏感的 DMA，优先使用驱动管理的 SRAM 或 HSRAM buffer
- 普通业务 buffer 优先从默认 non-cacheable 的 `AP_PSRAM_HEAP` 分配，通常不需要业务层
  cache clean / invalidate
- 不要将 `AP_PSRAM_CACHE_HEAP` 或栈上局部变量作为 DMA、CP、GPU、NPU、Wi-Fi、BT、
  display、audio/video codec 等第三方 master 的数据 buffer
- 固定 `SWAP` 控制区中不能放大块 DMA 负载

<a id="id4"></a>

## 启动流程与安全边界

当前启动路径可按以下顺序理解：

1. Reset 进入 ROM 或 bootloader 流程。
2. CP 与 AP 镜像分别从独立 Flash 分区中选出。
3. 每个镜像都从 `Reset_Handler_Core0` 进入。
4. 镜像先完成数据搬运和零初始化。
5. primary core 为本子系统配置 MPU 与 cache 策略。
6. primary core 初始化公共资源，并释放本地 secondary core。
7. 子系统分别进入各自的 RTOS 启动路径。

当前安全边界的结论如下：

- BK7259 头文件已经提供 Secure 与 Non-Secure 地址别名
- AP 与 CP 启动路径都会配置 MPU 区域
- 当前分区表尚未导出独立的 NSC 分区
- 量产签收前仍需要单独发布 Secure、Non-Secure 与 NSC 映射

<a id="id5"></a>

## 验证清单

- 检查生成的 `partitions.csv` 与最终打包镜像是否一致
- 检查生成的 `ram_regions.h` 是否仍满足 AP/CP 链接脚本约束
- 检查 `.shared_memory` 是否仍然固定为 `1024` 字节
- 检查 CP 与 AP 的 Flash 增长是否仍落在生成分区范围内
- 检查真实 video、audio、network 负载下的 PSRAM watermark
- 检查 DMA buffer 是否只落在已审查区域，并配套 cache 维护
