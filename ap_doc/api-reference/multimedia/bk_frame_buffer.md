---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/multimedia/bk_frame_buffer.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="frame-buffer"></a>

# frame\_buffer

<a id="id1"></a>

## 1\. 概述

Frame Buffer模块提供了视频帧缓冲区的内存管理功能，主要用于显示和编码场景。该模块具有以下核心特性：

1. 双堆内存管理 ：支持从PSRAM的DISPLAY堆和ENCODE堆分别分配内存，满足不同应用场景的需求
2. 安全内存分配 ：使用32字节内存对齐，确保内存访问的高效性和兼容性
3. CRC校验保护 ：为每个分配的缓冲区生成CRC-8校验值，防止内存重复释放和非法访问
4. 内存初始化 ：新分配的内存会用特定模式（0xFB）进行初始化，便于调试和问题排查
5. 错误处理 ：包含空指针检查、内存分配失败处理等安全机制

- 使用可以参考DVP示例工程是如何使用frame buffer相关API接口，实现图像的内存buffe管理：

  > - [ISP 示例工程](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/isp_example/index.html)

<a id="api"></a>

## 2\. API函数

- frame\_buffer\_display\_malloc() \- 从DISPLAY堆分配显示用帧缓冲区
- frame\_buffer\_display\_free() \- 释放显示用帧缓冲区
- frame\_buffer\_encode\_malloc() \- 从ENCODE堆分配编码用帧缓冲区
- frame\_buffer\_encode\_free() \- 释放编码用帧缓冲区

适用于视频显示系统、视频编码流水线等需要高效、安全内存管理的多媒体应用场景。

备注

- 该模块依赖于PSRAM模块，确保在使用前已经初始化。而PSRAM初始化分为两个部分，一个是PSRAM整个硬件模块的初始化，另一个是PSRAM的DISPLAY堆和ENCODE堆的初始化。
- 而DISPLAY堆和ENCODE堆的初始化是在PSRAM初始化的基础上进行的，确保在使用前已经初始化。
- PSRAM模块的初始化是基于投票的方式，因为使用PSRAM的模块不止多媒体，还可以将其作为Heap进行使用，投票接口参考：`bk_pm_module_vote_psram_ctrl`。
- 而DISPLAY堆和ENCODE堆的初始化是在上面PSRAM上电初始化后，调用提前注册的回调函数实现的，具体参考：`bk_psram_frame_buffer_init`。

<a id="id2"></a>

## 3\. 相关宏定义

以下宏定义了PSRAM内存区域的地址和大小配置，与链接脚本中的内存区域定义相对应：

- `PSRAM_ADDR` \- PSRAM内存基地址 (0x60000000)
- `PSRAM_MEM_SLAB_USER_SIZE` \- 用户堆内存大小配置 (CONFIG\_PSRAM\_MEM\_SLAB\_USER\_SIZE)
- `PSRAM_MEM_SLAB_AUDIO_SIZE` \- 音频堆内存大小配置 (CONFIG\_PSRAM\_MEM\_SLAB\_AUDIO\_SIZE)
- `PSRAM_MEM_SLAB_ENCODE_SIZE` \- 编码堆内存大小配置 (CONFIG\_PSRAM\_MEM\_SLAB\_ENCODE\_SIZE)
- `PSRAM_MEM_SLAB_DISPLAY_SIZE` \- 显示堆内存大小配置 (CONFIG\_PSRAM\_MEM\_SLAB\_DISPLAY\_SIZE)
- `psram_mem_slab` \- PSRAM内存映射结构体指针，用于访问各内存区域

对应的链接脚本内存区域定义：

- `PSRAM_SLAB_USER` \- 用户堆内存区域 (地址: CONFIG\_PSRAM\_MEM\_SLAB\_USER\_ADDR, 大小: CONFIG\_PSRAM\_MEM\_SLAB\_USER\_SIZE)
- `PSRAM_SLAB_AUDIO` \- 音频堆内存区域 (地址: CONFIG\_PSRAM\_MEM\_SLAB\_AUDIO\_ADDR, 大小: CONFIG\_PSRAM\_MEM\_SLAB\_AUDIO\_SIZE)
- `PSRAM_SLAB_ENCODE` \- 编码堆内存区域 (地址: CONFIG\_PSRAM\_MEM\_SLAB\_ENCODE\_ADDR, 大小: CONFIG\_PSRAM\_MEM\_SLAB\_ENCODE\_SIZE)
- `PSRAM_SLAB_DISPLAY` \- 显示堆内存区域 (地址: CONFIG\_PSRAM\_MEM\_SLAB\_DISPLAY\_ADDR, 大小: CONFIG\_PSRAM\_MEM\_SLAB\_DISPLAY\_SIZE)

这些宏和内存区域定义共同构成了PSRAM的内存管理框架，用于管理不同功能区域的内存分配。

<a id="id3"></a>

## 4\. 堆大小定义

以下宏定义了PSRAM内存区域的大小配置，与链接脚本中的内存区域定义相对应：

- `PSRAM_MEM_SLAB_USER_SIZE` \- 用户堆内存大小配置 (CONFIG\_PSRAM\_MEM\_SLAB\_USER\_SIZE)
- `PSRAM_MEM_SLAB_AUDIO_SIZE` \- 音频堆内存大小配置 (CONFIG\_PSRAM\_MEM\_SLAB\_AUDIO\_SIZE)
- `PSRAM_MEM_SLAB_ENCODE_SIZE` \- 编码堆内存大小配置 (CONFIG\_PSRAM\_MEM\_SLAB\_ENCODE\_SIZE)
- `PSRAM_MEM_SLAB_DISPLAY_SIZE` \- 显示堆内存大小配置 (CONFIG\_PSRAM\_MEM\_SLAB\_DISPLAY\_SIZE)

这些宏定义了PSRAM内存区域的大小，用于配置内存分配和管理。

备注

堆大小定义：如果需要修改不同的堆大小，只需要修改对应工程中的配置文件即可，参考app工程： `./projects/app/partitions/bk7259/ram_regions.csv`。

其中 `PSRAM_MEM_SLAB_USER_SIZE` 、 `PSRAM_MEM_SLAB_AUDIO_SIZE` 、 `PSRAM_MEM_SLAB_ENCODE_SIZE` 、 `PSRAM_MEM_SLAB_DISPLAY_SIZE` 对应内存区域的大小，单位为字节。

<a id="id4"></a>

## 5\. 相关数据结构

frame\_buffer\_t 结构体

frame\_buffer\_t是帧缓冲区管理中的核心数据结构，用于存储视频帧的元数据和实际帧数据：

```
typedef struct frame_buffer_t
{
    uint32_t flag;          // 标志位
    uint8_t *frame;         // 帧数据指针
    uint32_t size;          // 帧数据大小
    uint8_t frame_crc;      // 帧数据CRC校验值
    camera_type_t type;     // 摄像头类型
    pixel_format_t fmt;     // 像素格式
    uint8_t crc;            // 结构体CRC校验值
    uint32_t timestamp;     // 时间戳
    uint16_t width;         // 帧宽度
    uint16_t height;        // 帧高度
    uint32_t length;        // 帧长度
    uint32_t sequence;      // 序列号
    uint32_t h264_type;     // H264编码类型
} frame_buffer_t;
```

成员说明：

- **flag**: 状态标志位，用于标识帧缓冲区的各种状态
- **frame**: 指向实际帧数据的指针，存储视频帧的像素数据
- **size**: 帧数据的总大小（字节数）
- **frame\_crc**: 帧数据的CRC-8校验值，用于数据完整性验证
- **type**: 摄像头类型（camera\_type\_t枚举）
- **fmt**: 像素格式（pixel\_format\_t枚举），支持多种格式如：
  \- PIXEL\_FMT\_YUV420P, PIXEL\_FMT\_NV12, PIXEL\_FMT\_NV21
  \- PIXEL\_FMT\_RGB565, PIXEL\_FMT\_RGB888, PIXEL\_FMT\_ARGB8888
  \- PIXEL\_FMT\_GRAY, PIXEL\_FMT\_RAW, PIXEL\_FMT\_PNG
- **crc**: 结构体本身的CRC校验值，防止重复释放
- **timestamp**: 时间戳，记录帧的捕获或处理时间
- **width**: 帧的宽度（像素数）
- **height**: 帧的高度（像素数）
- **length**: 帧的实际数据长度
- **sequence**: 序列号，用于帧顺序追踪
- **h264\_type**: H264编码特定的类型信息

该结构体通过CRC校验机制确保内存安全，防止重复释放和非法访问。

以下结构体定义了PSRAM内存区域的结构体，用于访问各内存区域：

- `psram_mem_slab_t` \- PSRAM内存映射结构体，包含用户堆、音频堆、编码堆、显示堆的内存映射信息

这些结构体定义了PSRAM内存区域的布局和访问方式，用于管理不同功能区域的内存分配。

<a id="id5"></a>

## 6\. 相关函数接口

<a id="id6"></a>

### 6.1 显示缓冲区管理函数

**frame\_buffer\_display\_malloc**

```
frame_buffer_t *frame_buffer_display_malloc(uint32_t size);
```

**功能**: 从PSRAM的DISPLAY堆分配显示用帧缓冲区

**参数**:

> - size: 请求分配的帧数据大小（字节数）

**返回值**:

> - 成功: 指向分配的frame\_buffer\_t结构体的指针
> - 失败: NULL

**实现细节**:

```
- 从PSRAM_HEAP_YUV堆分配内存，大小为 `size + sizeof(frame_buffer_t) + 32`（32字节对齐预留）
- 使用`os_memset`清零frame_buffer_t结构体
- 计算32字节对齐的帧数据指针地址
- 设置flag为FB_ALLOCATED_PATTERN (0x8338)
- 计算前6个字节的CRC-8校验值并存储在frame_crc中
- 返回分配好的帧缓冲区指针
```

**frame\_buffer\_display\_free**

```
void frame_buffer_display_free(frame_buffer_t *frame);
```

**功能**: 释放显示用帧缓冲区

**参数**:

- frame: 要释放的帧缓冲区指针

**实现细节**:

> - 空指针检查，如果为NULL则记录错误日志
> - 检查flag是否为FB\_ALLOCATED\_PATTERN
> - 重新计算CRC校验值并与存储的frame\_crc比较
> - 如果校验通过，设置flag为FB\_FREE\_PATTERN (0xF00F)并释放内存
> - 如果校验失败，记录重复释放错误日志

<a id="id7"></a>

### 6.2 编码缓冲区管理函数

**frame\_buffer\_encode\_malloc**

```
frame_buffer_t *frame_buffer_encode_malloc(uint32_t size);
```

**功能**: 从PSRAM的ENCODE堆分配编码用帧缓冲区

**参数**:

> - size: 请求分配的帧数据大小（字节数）

**返回值**:

> - 成功: 指向分配的frame\_buffer\_t结构体的指针
> - 失败: NULL

**实现细节**:
1\. 从PSRAM\_HEAP\_ENCODE堆分配内存，大小计算与显示缓冲区相同
2\. 内存初始化和对齐处理与显示缓冲区相同
3\. 同样设置flag和CRC校验机制

**frame\_buffer\_encode\_free**

```
void frame_buffer_encode_free(frame_buffer_t *frame);
```

**功能**: 释放编码用帧缓冲区

**参数**:

> - frame: 要释放的帧缓冲区指针

**实现细节**:
1\. 释放逻辑与显示缓冲区完全相同
2\. 使用相同的安全检查和CRC验证机制

<a id="id8"></a>

### 6.3 关键特性

1. **内存对齐**: 所有帧数据指针都进行32字节对齐（ALIGN\_BITS\=5）
2. **安全分配**: 使用特定的分配模式(FB\_ALLOCATED\_PATTERN)标识有效缓冲区
3. **防重复释放**: 通过CRC-8校验防止内存重复释放
4. **错误处理**: 详细的错误日志记录，便于调试问题
5. **内存初始化**: 新分配的内存会进行清零初始化

<a id="id9"></a>

### 6.4 使用示例

```
// 分配显示缓冲区
frame_buffer_t *display_frame = frame_buffer_display_malloc(1920 * 1080 * 2);
if (display_frame) {
    // 使用帧缓冲区
    // ...
    // 释放缓冲区
    frame_buffer_display_free(display_frame);
}

// 分配编码缓冲区
frame_buffer_t *encode_frame = frame_buffer_encode_malloc(1280 * 720 * 1.5);
if (encode_frame) {
    // 使用帧缓冲区
    // ...
    // 释放缓冲区
    frame_buffer_encode_free(encode_frame);
}
```
