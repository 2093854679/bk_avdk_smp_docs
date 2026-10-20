---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_psram.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="psram"></a>

# PSRAM 使用指南

<a id="id1"></a>

## 概述

PSRAM（Pseudo Static RAM，伪静态随机存取存储器）是一种兼具 SRAM 接口简单性与 DRAM 容量优势的存储器类型。
通过内部 DRAM 技术 \+ 自动刷新控制，PSRAM 向主控提供与 SRAM 接口兼容的易用体验，且具备更高容量性价比，适用于图像/音频/缓存等大容量应用场景。

<a id="id2"></a>

## PSRAM 适用场景

PSRAM 特别适合以下应用场景：

- 图像缓存（摄像头帧缓存、图像预处理）
- 音频数据处理（语音识别、语音缓存）
- 联网应用缓存（TCP/IP 缓冲区、OTA 数据）
- 堆内存扩展（task 创建、运行时内存分配）

<a id="psram-bk7259"></a>

## 我们的 PSRAM 支持情况（BK7259）

- BK7259 芯片内置 **两块** 合封 PSRAM（PSRAM0 / PSRAM1，均封装在芯片内部）；相比之下 BK7258 仅内置 1 块 PSRAM。
- 地址空间：PSRAM0 基址 `0x60000000`，PSRAM1 基址 `0x64000000`；分区与容量以工程 `ram_regions.csv` 为准。
- 自动识别型号与容量：支持 4MB / 8MB / 16MB 等型号，驱动在启动时会根据 PSRAM ID 自动检测并配置初始化参数，编译时使用的大小需要在 `ram_regions.csv` 中配置。
- 初始化完成后，系统自动映射有效地址空间，供开发者使用
- 注意：尽管驱动能自动识别容量，但用户访问地址仍需确保不超出对应 PSRAM 实例的有效大小

<a id="id3"></a>

## PSRAM 使用方法

<a id="heap"></a>

### 作为 Heap 使用

- 在 `ram_regions.csv` 中通过 `AP_PSRAM_HEAP`、`AP_PSRAM_CACHE_HEAP`
  和 `CP_PSRAM_HEAP` 配置各内存池大小，并开启 `CONFIG_PSRAM_AS_SYS_MEMORY`。
- 动态内存接口：

  ```
  void *psram_malloc(size_t size);
  void *psram_zalloc(size_t size);
  void  psram_free(void *p);
  ```

  `psram_malloc` / `psram_zalloc` 从普通 `AP_PSRAM_HEAP` 分配。当前 AP
  推荐配置下，该内存默认 non-cacheable，适合普通业务 buffer。`AP_PSRAM_CACHE_HEAP`
  仅用于 OS 内部的 PSRAM task 相关分配，不作为客户业务 buffer 接口。
- 低功耗场景：未释放 Heap 内存会影响进入低功耗，可用 bk\_psram\_heap\_get\_used\_state() 查询当前状态。
- PSRAM 上的 Task 创建接口:

  ```
  bk_err_t rtos_create_psram_thread(beken_thread_t *thread, uint8_t priority, const char *name, beken_thread_function_t function, uint32_t stack_size, beken_thread_arg_t arg);
  bk_err_t rtos_delete_thread(beken_thread_t *thread);
  ```

  如果 PSRAM 上创建任务失败或返回内存不足，通常需要检查 `AP_PSRAM_CACHE_HEAP` 是否
  满足当前工程的 PSRAM task 内部分配峰值需求。非 fast boot 场景还需考虑 TCB 等任务内部
  对象开销。可在工程 `partitions/bk7259/ram_regions.csv` 中增大
  `AP_PSRAM_CACHE_HEAP`，必要时从普通 `AP_PSRAM_HEAP`、`AP_PSRAM_CODE_SECTION` 或其它
  可调整区域中回收空间。修改后建议 clean 编译，并通过 `memshow` 确认剩余空间。

<a id="id4"></a>

### 作为 多媒体静态内存 使用

- 多媒体模块（AP）独占部分 PSRAM 空间
- 使用专用接口申请/释放：

```
void *bk_psram_frame_buffer_malloc(psram_heap_type_t type, uint32_t size);
void  bk_psram_frame_buffer_free(void* mem_ptr);
```

<a id="id5"></a>

## PSRAM 使用说明

- PSRAM 可被 AP 与 CP共同访问，但访问时需要避免资源冲突，确保互斥管理
- AP 普通动态内存使用 psram\_malloc() / psram\_free()；该内存默认 non-cacheable，
  适合普通业务 buffer 和常见 CP/DMA 共享场景
- 一部分 PSRAM 空间可用于扩展堆内存，提升系统动态内存灵活性

<a id="id6"></a>

## PSRAM的类型

> BK7259支持三种类型的PSRAM，具体配置如下：
>
> |  |  |
> | --- | --- |
> | name | size(Mbyte) |
> | W955D8MKY\_5J | 4 |
> | APS6408L\_O | 8 |
> | APS128XXO\_OB9 | 16 |

<a id="id7"></a>

## PSRAM的划分

> PSRAM主要分为两部分，一部分是多媒体当作数据内存进行使用，另一部分当作不同CPU的heap空间进行使用，需要参考下面的宏定义去使能配置：
>
> |  |  |  |
> | --- | --- | --- |
> | marco | value | implication |
> | CONFIG\_PSRAM | Y | 使能PSRAM模块 |
> | CONFIG\_PSRAM\_AS\_SYS\_MEMORY | Y | 使能PSRAM作为Heap |
> | CONFIG\_USE\_PSRAM\_HEAP\_AT\_SRAM\_OOM | Y | 使能sram申请不到内存，从psram申请 |
>
> > - 功能开关CONFIG\_PSRAM\_AS\_SYS\_MEMORY依赖CONFIG\_PSRAM和CONFIG\_FREERTOS\_V10

备注

注意：
系统默认从PSRAM的起始地址(0x60000000)开始的头部区域给多媒体使用。
某个核上是否需要将psram作为heap，是由 `CONFIG_PSRAM_AS_SYS_MEMORY` 控制。
ram\_regions.csv仅作为划分资源分区，是否使用特定的分区由相应的宏进行控制，
但AP侧未开启 `CONFIG_PSRAM_AS_SYS_MEMORY` 则此分区未被使用。

<a id="id8"></a>

## PSRAM在多媒体上的划分

> > PSRAM在多媒体上使用，根据功能被划分为四个模块，参考结构体：`psram_heap_type_t`，位置：`ap/include/driver/media_types.h`.
> >
> > 各个模块使用的内存是由结构体：`psram_mem_slab_mapping` ，定义的，参考路径：`ap/components/media_utils/src/frame_buffer_mapping.h`。
> > 各个模块分配的内存大小在ram\_regions.csv中配置，默认配置如下所示：
>
> |  |  |  |
> | --- | --- | --- |
> | marco | value(byte) | implication |
> | CONFIG\_PSRAM\_MEM\_SLAB\_USER\_SIZE | 102400 | user defined mem block |
> | CONFIG\_PSRAM\_MEM\_SLAB\_AUDIO\_SIZE | 102400 | audio module mem block |
> | CONFIG\_PSRAM\_MEM\_SLAB\_ENCODE\_SIZE | 1433600 | encode image mem block |
> | CONFIG\_PSRAM\_MEM\_SLAB\_DISPLAY\_SIZE | 5701632 | undecode image mem block |

备注

注意：上面宏定义的值是默认定义的，使用时可以根据自身需求，动态调整，直接在对应project中ram\_regions.csv中进行修改即可。

<a id="id9"></a>

## 各个模块内存调整

> > 根据上节所述，psram被划分为四个模块，不同的模块存储的数据类型不同，可在ram\_regions.csv中配置地址空间，具体如下：
> >
> > - UASER：分配给用户使用，编译时生成 `CONFIG_PSRAM_MEM_SLAB_UASER_SIZE` 和 `CONFIG_PSRAM_MEM_SLAB_UASER_SIZE`；
> > - AUDIO：分配给audio使用，存储的是音频数据，编译时生成 `CONFIG_PSRAM_MEM_SLAB_AUDIO_SIZE` 和 `CONFIG_PSRAM_MEM_SLAB_AUDIO_SIZE`；
> > - ENCODE：分配给编码使用，存储的是完整的JPEG图像或者H264图像，编译时生成 `CONFIG_PSRAM_MEM_SLAB_ENCODE_SIZE` 和 `CONFIG_PSRAM_MEM_SLAB_ENCODE_SIZE`；
> > - DISPLAY：分配给显示使用，存储的是显示的数据类型，如YUV、RGB565、RGB888等，编译时生成 `CONFIG_PSRAM_MEM_SLAB_DISPLAY_SIZE` 和 `CONFIG_PSRAM_MEM_SLAB_DISPLAY_SIZE`；
> >
> > 根据上面不同的模块功能，以及大小，存储的数据量也不一样，比如ENCODE模块可以存储不止一帧的JPEG图像或H264图像，
> > 系统还定义了一帧图像的大小的宏，参考文件：`./bk_idk/middleware/driver/camera/Kconfig`:
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | marco | value(byte) | implication | range |
> | CONFIG\_JPEG\_FRAME\_SIZE | 153600 | a jpeg frame max size | \[0, 204800\] |
> | CONFIG\_H264\_FRAME\_SIZE | 65536 | a h264 frame max size | \[0, 204800\] |
>
> > 上面的大小需要根据自身需求需要调整，比如需要存储1280X720的JPEG图像，150K的空间可能不够，需要改成200K(204800)，甚至更大，根据实际使用情况调整。
> > 同样针对H264数据，有时候需要调整H264的压缩率，以达到更清楚的画质，默认的64K可能不够，需要继续调大，所以也需要根据实际情况做调整。
> >
> > 根据上面的定义的大小，不同块存储的个数可以计算出来，假设DISPLAY模块使用的RGB565，且分辨率为：800X480，那么一帧图像的大小为：800\*480\*2\=768000，
> > 可存储的个数为：CONFIG\_PSRAM\_MEM\_SLAB\_DISPLAY\_SIZE/768000\=7，表示最大存7帧800X480的RGB565图像；
> >
> > 假设ENCODE模块都用来存储JPEG图像，最多存储数量：CONFIG\_PSRAM\_MEM\_SLAB\_ENCODE\_SIZE/CONFIG\_JPEG\_FRAME\_SIZE\=9；但实际情况会同时存储JPEG和H264数据，代码中定义了
> > 各个图像模块最大的存储个数，参考： `ap/components/multimedia/include/frame_buffer.h`。

```
#define FRAME_LIST_NODE_MAX         6
#define COMM_FRAME_LIST_MAX_NODE    (FRAME_LIST_NODE_MAX - 2)
#if (!CONFIG_MEDIA_PSRAM_SIZE_4M)
#define H26X_FRAME_LIST_MAX_NODE    FRAME_LIST_NODE_MAX
#else
#define H26X_FRAME_LIST_MAX_NODE    (FRAME_LIST_NODE_MAX - 2)
#endif
#define YUV_FRAME_LIST_MAX_NODE     (FRAME_LIST_NODE_MAX - 3)

      上面的数量可以调整，只要保证总的数据量不超过各自模块的size即可。
```

<a id="id10"></a>

## 多媒体上PSRAM使用

> > 因为多媒体的功能都在CPU1上使用，所以针对PSRAM的使用，只能在CPU1上直接调用，系统CPU1启动后会自动给多媒体整个PSRAM进行初始化，用户不需要去自己调用实现。
> > 当CPU1掉电时，多媒体不再使用PSRAM，不需要额外调用注销的接口去释放相应的内存。
>
> - 内存初始化接口:
>
>   ```
>   bk_psram_frame_buffer_init
>   ```
> - 内存申请和释放接口:
>
>   ```
>   void *bk_psram_frame_buffer_malloc(psram_heap_type_t type, uint32_t size);
>   void bk_psram_frame_buffer_free(void* mem_ptr);
>   ```

备注

客户使用时，建议使用系统的 `psram_malloc` / `psram_free` 接口，
不建议直接使用上面的多媒体模块私有接口。

<a id="psram-heap-cache"></a>

## PSRAM heap 的 Cache 属性

BK7259 已在 MPU 中按 `ram_regions.csv` 自动划分 PSRAM 属性，无需应用修改
`mpu_cfg.c`：

- `AP_PSRAM_HEAP` 和 `AP_PSRAM_DATA_SECTION` 为 non-cacheable。
- `AP_PSRAM_CACHE_HEAP` 为 L2 write-back cacheable，仅用于 PSRAM task 相关内部分配。
- `AP_PSRAM_CODE_SECTION` 为 L1/L2 cacheable。

普通业务 buffer 默认使用 non-cacheable 的 `AP_PSRAM_HEAP`，通常不需要业务层手动
clean/invalidate。不要将 `AP_PSRAM_CACHE_HEAP` 或栈上局部变量作为 DMA、CP、GPU、
NPU、Wi-Fi、BT、display、audio/video codec 等第三方 master 的数据 buffer。

<a id="id11"></a>

## PSRAM使用注意事项与动态行为

<a id="id12"></a>

### PSRAM与低功耗管理的关系

- Heap 初始化 / 多媒体静态使用时 投票上电
- 资源释放后 投票下电，系统自动管理，无需手动干预

<a id="id13"></a>

### PSRAM空间划分规则

- 默认 PSRAM\_DATA\_ADDR(0x60000000) 到 DISPLAY分区结束为多媒体静态区
- 避免各个分区重叠

<a id="id14"></a>

### 不同容量对工程配置影响

- 不同工程场景需合理配置 PSRAM 空间
- 若配置超出硬件容量，编译阶段 自动报错提示

<a id="dump"></a>

### Dump 行为说明

- 系统默认 Dump Heap 区内容
- 多媒体静态区需手动接口查看，不自动 Dump
