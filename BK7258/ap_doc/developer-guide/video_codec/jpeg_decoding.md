---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/video_codec/jpeg_decoding.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="jpeg"></a>

# JPEG 解码概述

<a id="id1"></a>

## 1、概述

> 本节主要说明JPEG解码器的整体架构、支持的功能以及使用方法。系统提供两种JPEG解码方案：硬件解码和软件解码，以满足不同场景下的需求。

- 有关JPEG解码的示例工程，请参阅：

  - [JPEG解码示例工程](../../examples/projects/jpeg_decode_example.md)
- 有关API参考，请参阅：

  - [JPEG硬解码 API](../../api-reference/multimedia/bk_jpegdec_hw.md)
  - [JPEG软解码 API](../../api-reference/multimedia/bk_jpegdec_sw.md)
- 有关JPEG解码的详细信息，请参阅：

  - [JPEG硬件解码指南](jpeg_decoding_hw.md)
  - [JPEG软件解码指南](jpeg_decoding_sw.md)

<a id="id6"></a>

## 2、JPEG解码架构

> JPEG解码器提供两种实现方式：
>
> 1. **硬件解码器**：使用专用硬件加速JPEG解码过程，具有高性能、低CPU占用的特点。
> 2. **软件解码器**：使用CPU实现JPEG解码过程，提供更灵活的解码选项和输出格式支持。
>
> 硬件解码器和软件解码器共享相似的接口设计，使用户可以方便地在两种模式之间切换。同时，两种解码器都支持相同的回调机制和基本的解码流程。

<a id="id7"></a>

## 3、支持的功能

两种JPEG解码器共有的功能：

> 1、支持标准JPEG格式解码；
>
> 2、支持获取图像信息（宽度、高度、格式等）；
>
> 3、支持回调机制处理解码完成事件；
>
> 4、支持扩展控制接口。

硬件解码器特有功能：

> 1、解码速度快；
>
> 2、不占用CPU资源；

软件解码器特有功能：

> 1、支持灰度、RGB565、RGB888、YUYV、VYUY、VUYY等多种输出格式；
>
> 2、支持大小端字节序配置；
>
> 3、支持多核优化执行；
>
> 4、提供丰富的图像旋转和格式转换选项；
>
> 5、支持YUV444、YUV422、YUV420多种格式的JPEG图像解码。

<a id="id8"></a>

## 4、文档结构

> 本JPEG解码文档集包含以下部分：
>
> 1. **JPEG解码概述** （当前页面）：提供JPEG解码的整体架构和功能介绍。
> 2. **JPEG硬件解码**：详细说明硬件解码器的使用方法、API和数据结构。
> 3. **JPEG软件解码**：详细说明软件解码器的使用方法、API和数据结构。

<a id="id9"></a>

## 5、相关头文件

> **共享头文件**：
>
> - `components/bk_jpeg_decode/bk_jpeg_decode_types.h` \- 定义JPEG解码通用类型、枚举和结构体
>
> **硬件解码头文件**：
>
> - `components/bk_jpeg_decode/bk_jpeg_decode_hw.h` \- 定义JPEG硬件解码API
> - `components/bk_jpeg_decode/bk_jpeg_decode_types_hw.h` \- 定义JPEG硬件解码特定类型
>
> **软件解码头文件**：
>
> - `components/bk_jpeg_decode/bk_jpeg_decode_sw.h` \- 定义JPEG软件解码API
> - `components/bk_jpeg_decode/bk_jpeg_decode_types_sw.h` \- 定义JPEG软件解码特定类型

<a id="id10"></a>

## 6、使用流程比较

> 硬件解码器和软件解码器的基本使用流程相似，但在具体实现和配置选项上有所不同。以下是两种解码器的主要使用流程对比：
>
> **硬件解码器使用流程**：
>
> 1. 创建硬件解码器实例（bk\_hardware\_jpeg\_decode\_new）
> 2. 打开硬件解码器（bk\_jpeg\_decode\_hw\_open）
> 3. 获取图像信息（bk\_jpeg\_decode\_hw\_get\_img\_info）
> 4. 配置硬件解码器（可选，bk\_jpeg\_decode\_hw\_set\_config）
> 5. 等待解码完成
> 6. 关闭硬件解码器（bk\_jpeg\_decode\_hw\_close）
> 7. 删除硬件解码器实例（bk\_jpeg\_decode\_hw\_delete）
>
> **软件解码器使用流程**：
>
> 1. 创建软件解码器实例（bk\_software\_jpeg\_decode\_new或bk\_software\_jpeg\_decode\_on\_multi\_core\_new）
> 2. 打开软件解码器（bk\_jpeg\_decode\_sw\_open）
> 3. 获取图像信息（bk\_jpeg\_decode\_sw\_get\_img\_info）
> 4. 设置输出帧配置（bk\_jpeg\_decode\_sw\_set\_config，可选，更改创建实例时传入的配置时调用）
> 5. 执行解码（同步或异步）
> 6. 等待解码完成
> 7. 关闭软件解码器（bk\_jpeg\_decode\_sw\_close）
> 8. 删除软件解码器实例（bk\_jpeg\_decode\_sw\_delete）

<a id="id11"></a>

## 7、JPEG解码器选择指南

> 如何选择适合的JPEG解码器？以下是一些选择指南：
>
> **选择硬件解码器的场景**：
>
> - 对性能要求高，需要快速解码大量JPEG图像
> - 解码分辨率适中，且对输出格式要求不复杂
> - 对CPU资源有其他高要求的任务需要运行
>
> **选择软件解码器的场景**：
>
> - 需要支持多种输出格式和特殊图像处理
> - 对解码质量有特殊要求
> - 需要处理一些非标准或特殊的JPEG格式
> - 系统资源充足，对功耗要求不严格
> - 解码分辨率不高，图像数量不大
> - 需要在多核处理器上优化性能
>
> 在某些应用场景下，也可以考虑混合使用两种解码器，例如在处理不同分辨率或不同格式的JPEG图像时，根据具体需求选择最适合的解码器。

<a id="id12"></a>

## 8、JPEG解码参考工程

> 完整的JPEG解码示例工程位于：
>
> `./projects/jpeg_decode_example`
>
> 该示例提供了详细的使用案例，包括硬件解码和软件解码的完整实现，以及错误处理、回调机制等功能演示。示例代码展示了如何在实际应用中使用JPEG解码器进行图像解码。

<a id="id13"></a>

## 9、更多信息

> - 有关JPEG硬件解码的详细信息，请参阅：`JPEG硬解码`
> - 有关JPEG软件解码的详细信息，请参阅：`JPEG软解码`
