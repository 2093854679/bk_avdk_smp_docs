---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/projects/dma2d_example/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="dma2d-example"></a>

# DMA2D Example

<a id="id1"></a>

## 概述

本示例展示了BK7258平台中DMA2D控制器的使用方法。它提供了二维图形操作功能，如用指定颜色填充区域、内存复制、像素格式转换和混合两个图像层。

<a id="id2"></a>

## 支持的功能

> - **填充（Fill）**: 用指定颜色填充矩形区域
> - **内存复制（Memory Copy）**: 将图像数据从源地址复制到目标地址
> - **像素格式转换（PFC）**: 在不同像素格式之间转换（RGB565、RGB888、ARGB8888）
> - **混合（Blending）**: 混合前景和背景图层，可调节透明度

- DMA2D的功能在开发者指南中有详细介绍，请参阅：

  - [DMA2D开发指南](../../developer-guide/display/dma2d.md)
- 有关API参考，请参阅：

  - [DMA2D API](../../api-reference/multimedia/bk_dma2d.md)

<a id="id3"></a>

## 组件

> - **bk\_dma2d**: DMA2D控制器驱动
> - **frame\_buffer**: 帧缓冲管理
> - **cli**: 用于测试的命令行接口

<a id="id4"></a>

## 测试环境

> - 硬件配置：
>   :   - 核心板，**BK7258\_QFN88\_9X9\_V3.2**
>       - PSRAM 8M/16M
>       - lcd 转接小板
>       - RGB接口的LCD，demo中使用的为st7701sn 480\*854的屏幕

警告

请使用参考外设，进行demo工程的熟悉和学习。如果外设规格不一样，代码可能需要重新配置。

<a id="id5"></a>

## 项目结构

```
dma2d_example/
├── ap/
│   ├── dma2d/
│   │   ├── src/
│   │   │   ├── dma2d_cli.c           # CLI命令行接口实现
│   │   │   ├── dma2d_fill_test.c     # 填充功能测试代码
│   │   │   ├── dma2d_memcpy_test.c   # 内存拷贝功能测试代码
│   │   │   ├── dma2d_pfc_test.c      # 像素格式转换功能测试代码
│   │   │   ├── dma2d_blend_test.c    # 混合功能测试代码
│   │   │   └── blend_assets/         # 混合测试用的图片资源
│   │   └── include/
│   │       └── dma2d_test.h          # 测试接口头文件
│   ├── ap_main.c                     # AP核心主程序
│   └── config/                       # 配置文件
├── cp/                               # CP核心相关代码
├── partitions/                       # 分区配置
├── README_CN.md                      # 中文说明文档
├── README.md                         # 英文说明文档
└── CMakeLists.txt                    # 构建配置文件
```

<a id="id6"></a>

## 编译与运行

使用以下命令编译项目：

```
make bk7258 PROJECT=dma2d_example
```

编译完成后，将生成的固件烧录到开发板上，然后通过串口终端使用以下命令测试显示功能：

命令执行成功打印：`CMDRSP:OK`

命令执行失败打印：`CMDRSP:ERROR`

<a id="id7"></a>

## 命令行接口

本示例提供了命令行接口用于测试不同的DMA2D操作。以下是可用的命令：

<a id="id8"></a>

### 基本命令

```
# 创建DMA2D控制器实例1，并初始化LCD显示
> dma2d open module1

# 关闭DMA2D控制器，释放资源并删除DMA2D实例1
> dma2d close module1

# 创建DMA2D控制器实例2，创建多个实例是为了在多个场景下同时使用DMA2D
> dma2d open module2

# 关闭DMA2D控制器，释放资源并删除DMA2D实例2
> dma2d close module2
```

**说明：**
\* 第一次执行 `dma2d open` 命令时，会同时初始化LCD显示控制器
\* 当所有DMA2D实例都关闭后，LCD显示控制器也会自动关闭
\* 多个实例共享同一个DMA2D硬件模块，组件内部会进行场景切换保护

<a id="id9"></a>

### 填充命令

```
# 用指定颜色填充矩形区域
# 格式: dma2d fill <格式> <颜色> <帧宽度> <帧高度> <x坐标> <y坐标> <填充宽度> <填充高度>
# <格式>: RGB565, RGB888, ARGB8888
# <颜色>: 十六进制颜色值（不带0x前缀）

# 示例1：使用RGB565格式，填充红色到480x854的帧
> dma2d fill RGB565 F800 480 854 0 0 480 854

# 示例2：部分填充，在(100,100)位置填充200x200的绿色区域
> dma2d fill RGB565 07E0 480 854 100 100 200 200

# 使用module2实例进行填充
> dma2d fill_module2 RGB565 F800 480 854 0 0 480 854
```

**说明：**
\* 填充操作是同步执行的（`is_sync = true`）
\* 填充完成后会自动刷新到LCD显示
\* 帧缓冲区从显示内存池分配，使用完成后自动释放

<a id="id10"></a>

### 内存拷贝命令

```
# 从源地址拷贝图像数据到目标地址（支持带偏移的拷贝）
# 格式: dma2d memcpy <格式> <颜色> <源宽度> <源高度> <目标宽度> <目标高度>
#                    <源x坐标> <源y坐标> <目标x坐标> <目标y坐标> <拷贝宽度> <拷贝高度>

# 示例1：完整拷贝32x48的图像
> dma2d memcpy RGB565 F800 32 48 32 48 0 0 0 0 32 48

# 示例2：部分拷贝，从源图(10,10)拷贝20x20到目标图(5,5)位置
> dma2d memcpy RGB565 F800 100 100 100 100 10 10 5 5 20 20

# 使用module2实例进行拷贝
> dma2d memcpy_module2 RGB565 F800 32 48 32 48 0 0 0 0 32 48
```

**说明：**
\* 内存拷贝操作是异步执行的（`is_sync = false`），使用信号量进行同步
\* 拷贝完成后会自动进行数据校验
\* 支持相同格式的内存拷贝，输入输出格式需一致

<a id="id11"></a>

### 像素格式转换命令

```
# 在拷贝的同时进行像素格式转换
# 格式: dma2d pfc <输入格式> <输出格式> <颜色> <源宽度> <源高度> <目标宽度> <目标高度>
#                  <源x坐标> <源y坐标> <目标x坐标> <目标y坐标> <宽度> <高度>

# 示例1：从RGB565转换为RGB888
> dma2d pfc RGB565 RGB888 F800 32 48 32 48 0 0 0 0 32 48

# 示例2：从RGB888转换为ARGB8888
> dma2d pfc RGB888 ARGB8888 FF0000 100 100 100 100 0 0 0 0 100 100

# 使用module2实例进行格式转换
> dma2d pfc_module2 RGB565 RGB888 F800 32 48 32 48 0 0 0 0 32 48
```

**说明：**
\* 像素格式转换操作是同步执行的（`is_sync = true`）
\* 支持的输入格式：ARGB8888, RGB888, RGB565, ARGB1555, ARGB4444等
\* 支持的输出格式：ARGB8888, RGB888, RGB565, ARGB1555, ARGB4444
\* 转换时支持带偏移的拷贝

<a id="id12"></a>

### 混合命令

```
# 混合前景和背景图层，支持透明度控制
# 格式: dma2d blend <背景格式> <背景颜色> <背景宽度> <背景高度> <是否同步>
# 注意：此命令使用内置的图片资源（云朵、WiFi信号、电池图标）进行混合测试

# 示例1：同步混合（0表示同步）
> dma2d blend RGB565 07E0 480 854 0

# 示例2：异步混合（1表示异步）
> dma2d blend RGB565 07E0 480 854 1

# 使用module2实例进行混合
> dma2d blend_module2 RGB565 07E0 480 854 0
```

**说明：**
\* 混合操作使用内置的图片资源（img\_cloudy\_to\_sunny、img\_wifi\_rssi0、img\_battery1）
\* 前景图片固定为ARGB8888格式，包含透明度信息
\* 支持红蓝颜色交换配置（`fg_red_blue_swap = DMA2D_RB_SWAP`）
\* 混合完成后会自动刷新到LCD显示
\* 透明度模式使用 `DMA2D_NO_MODIF_ALPHA`，保持原图透明度

<a id="id13"></a>

## 实现细节

<a id="id14"></a>

### 多实例管理

- 项目支持创建多个DMA2D控制器实例（module1和module2）
- 多个实例实际共享同一个DMA2D硬件模块
- 组件内部会进行互斥保护，确保多场景使用的安全性
- 可以通过 `bk_dma2d_get_handle()` 获取已创建的句柄

<a id="id15"></a>

### 内存管理

- 所有帧缓冲区通过 `frame_buffer_display_malloc()` 从显示内存池分配
- 使用完成后通过 `frame_buffer_display_free()` 释放
- 对于显示的帧，使用回调函数 `display_frame_free_cb` 自动释放

<a id="id16"></a>

### 同步与异步

- **同步模式** (`is_sync = true`)：API调用会阻塞直到操作完成
  \- 填充操作（fill）使用同步模式
  \- 像素格式转换（pfc）使用同步模式
- **异步模式** (`is_sync = false`)：API调用立即返回，操作在后台完成
  \- 内存拷贝（memcpy）使用异步模式，通过信号量等待完成

<a id="id17"></a>

### 错误处理

- 使用 `AVDK_RETURN_ON_FALSE` 和 `AVDK_RETURN_ON_ERROR` 宏进行错误检查
- 失败时会打印详细的错误信息
- 确保资源正确释放，避免内存泄漏

<a id="id18"></a>

## 注意事项

- 执行操作前必须先使用 `dma2d open` 命令打开DMA2D控制器
- 操作完成后建议使用 `dma2d close` 命令关闭控制器释放资源
- 示例使用从显示内存池分配的帧缓冲区，确保PSRAM配置正确（8M/16M）
- LCD配置针对st7701sn 480x854屏幕，使用其他屏幕需修改配置
- 填充、混合操作使用同步模式，会阻塞直到完成
- 内存拷贝操作使用异步模式，通过信号量进行同步
- 确保配置的坐标和尺寸不超出帧的边界，否则可能导致异常
- 像素格式必须正确配置，否则可能导致数据异常或硬件工作异常
