---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/display/dma2d.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="dma2d"></a>

# DMA2D使用指南

<a id="id1"></a>

## 概述

<a id="id2"></a>

## DMA2D组件功能特点

DMA2D（Direct Memory Access 2D）模块提供了硬件加速的2D图形操作功能，包括：

- 内存填充（Fill）：使用指定颜色填充矩形区域
- 内存拷贝（Memcpy）：可以带偏移的内存拷贝
- 像素格式转换（PFC Memcpy）：可以带偏移的，带格式转换的内存拷贝
- 混合操作（Blend）：图像混合操作
- 组件接口支持同步和异步操作模式

关于配置中的参数.is\_sync true/false 表示是否同步操作，true表示同步操作，调用该接口功能实现后退出。false表示异步操作，调用该接口后立即返回，功能实现需要在DMA2D task中完成。

- 支持多个场景分时复用，由于DMA2D硬件模块只有一个，所以在多个场景使用时创建的handle为同一个，用户也可以使用提供的get handle接口后获取。拿到handle后，可以在多个场景下调用memcopy，blend等API，组件内部会做场景切换保护。

- 有关DMA2D的示例工程，请参阅：

  - [DMA2D示例工程](../../examples/projects/dma2d_example.md)
- 有关DMA2D接口文档，请参阅：

  - [DMA2D API](../../api-reference/multimedia/bk_dma2d.md)

注意

- DMA2D的填充数据像素格式选择out\_color\_mode\_t成员
- DMA2D的内存拷贝的数据格式选择out\_color\_mode\_t成员
- DMA2D像素转换的源数据像素格式为input\_color\_mode\_t，输出像素格式为out\_color\_mode\_t
- DMA2D的融合前景/背景的输入格式为input\_color\_mode\_t，输出格式为out\_color\_mode\_t
- 如果输入输出格式输入错误，可能导致数据异常或DMA2D工作异常

DMA2D输入输出支持的像素格式如下：

输入像素格式：

```
/** DMA2D_Input_Color_Mode*/
typedef enum {
        DMA2D_INPUT_ARGB8888 = 0, /**< ARGB8888 DMA2D color mode */
        DMA2D_INPUT_RGB888,  /**< RGB888 DMA2D color mode   */
        DMA2D_INPUT_RGB565,   /**< RGB565 DMA2D color mode   */
        DMA2D_INPUT_ARGB1555,   /**< ARGB1555 DMA2D color mode */
        DMA2D_INPUT_ARGB4444,   /**< ARGB4444 DMA2D color mode */
        DMA2D_INPUT_L8 = 5,
        DMA2D_INPUT_AL44,
        DMA2D_INPUT_AL88,
        DMA2D_INPUT_L4,
        DMA2D_INPUT_A8,
        DMA2D_INPUT_A4,
} input_color_mode_t;
```

输出像素格式：

```
/** DMA2D_Output_Color_Mode */
typedef enum {
        DMA2D_OUTPUT_ARGB8888 = 0, /**< ARGB8888 DMA2D color mode */
        DMA2D_OUTPUT_RGB888,       /**< RGB888 DMA2D color mode   */
        DMA2D_OUTPUT_RGB565,       /**< RGB565 DMA2D color mode   */
        DMA2D_OUTPUT_ARGB1555,     /**< ARGB1555 DMA2D color mode */
        DMA2D_OUTPUT_ARGB4444,     /**< ARGB4444 DMA2D color mode */
} out_color_mode_t;
```

<a id="api"></a>

## API调用流程概览

DMA2D的典型使用流程如下：

```
┌─────────────────────────────────────────────────────────────┐
│                    DMA2D API 调用流程                         │
└─────────────────────────────────────────────────────────────┘

1. bk_dma2d_new()        ──→  创建DMA2D控制器实例
                               └─ 分配资源，初始化句柄

2. bk_dma2d_open()       ──→  打开DMA2D控制器
                               └─ 启动硬件，使能时钟

3. DMA2D操作（可多次调用）
   │
   ├─ bk_dma2d_fill()          填充操作
   ├─ bk_dma2d_memcpy()        内存拷贝
   ├─ bk_dma2d_pixel_conversion()  像素格式转换
   └─ bk_dma2d_blend()         图层混合

4. bk_dma2d_close()      ──→  关闭DMA2D控制器
                               └─ 停止硬件，关闭时钟

5. bk_dma2d_delete()     ──→  删除DMA2D控制器实例
                               └─ 释放资源，清空句柄
```

注意

- 必须按照上述顺序调用API
- 在执行DMA2D操作前，必须先创建并打开控制器
- 操作完成后，建议及时关闭和删除控制器以释放资源
- 支持创建多个控制器实例，但它们共享同一个硬件模块

<a id="id4"></a>

## 完整使用示例

以下是一个完整的DMA2D使用示例，展示了从创建到删除的全过程：

```
#include <components/bk_dma2d/bk_dma2d.h>
#include <components/bk_dma2d/bk_dma2d_types.h>

#define TAG "dma2d_demo"

avdk_err_t dma2d_demo(void)
{
    avdk_err_t ret = AVDK_ERR_OK;
    bk_dma2d_ctlr_handle_t dma2d_handle = NULL;

    // 步骤1: 创建DMA2D控制器
    ret = bk_dma2d_new(&dma2d_handle);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_dma2d_new failed: %d\n", ret);
        return ret;
    }
    LOGI("DMA2D controller created successfully\n");

    // 步骤2: 打开DMA2D控制器
    ret = bk_dma2d_open(dma2d_handle);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_dma2d_open failed: %d\n", ret);
        bk_dma2d_delete(dma2d_handle);
        return ret;
    }
    LOGI("DMA2D controller opened successfully\n");

    // 步骤3: 执行DMA2D操作（这里以填充为例）
    // ... 执行fill/memcpy/blend等操作 ...

    // 步骤4: 关闭DMA2D控制器
    ret = bk_dma2d_close(dma2d_handle);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_dma2d_close failed: %d\n", ret);
    }
    LOGI("DMA2D controller closed successfully\n");

    // 步骤5: 删除DMA2D控制器
    ret = bk_dma2d_delete(dma2d_handle);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_dma2d_delete failed: %d\n", ret);
        return ret;
    }
    dma2d_handle = NULL;
    LOGI("DMA2D controller deleted successfully\n");

    return AVDK_ERR_OK;
}
```

<a id="id5"></a>

## API详细说明

<a id="bk-dma2d-new-dma2d"></a>

### 1\. bk\_dma2d\_new \- 创建DMA2D控制器

**功能描述:**

创建一个DMA2D控制器实例，分配必要的资源并初始化句柄。此函数可以被多次调用以创建多个实例，但所有实例共享同一个DMA2D硬件模块。

**函数原型:**

```
avdk_err_t bk_dma2d_new(bk_dma2d_ctlr_handle_t *handle);
```

**参数说明:**

- handle: \[输出\] 指向DMA2D控制器句柄的指针，函数成功后会将创建的句柄存储到此地址

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_NOMEM: 内存分配失败
- AVDK\_ERR\_INVAL: 参数无效（handle为NULL）

**使用注意:**

- 必须在调用其他DMA2D API之前调用此函数
- 创建成功后，handle会指向一个有效的控制器实例
- 如果创建失败，handle的值不会被修改
- 支持多实例，但建议在单个场景中只创建一个实例

**示例代码:**

```
bk_dma2d_ctlr_handle_t dma2d_handle = NULL;

// 创建DMA2D控制器
avdk_err_t ret = bk_dma2d_new(&dma2d_handle);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to create DMA2D controller: %d\n", ret);
    return ret;
}
LOGI("DMA2D controller created: %p\n", dma2d_handle);
```

<a id="bk-dma2d-open-dma2d"></a>

### 2\. bk\_dma2d\_open \- 打开DMA2D控制器

**功能描述:**

打开已创建的DMA2D控制器，启动硬件模块并使能相关时钟。只有在打开控制器后，才能执行DMA2D的各种操作（填充、拷贝、混合等）。

**函数原型:**

```
avdk_err_t bk_dma2d_open(bk_dma2d_ctlr_handle_t handle);
```

**参数说明:**

- handle: \[输入\] DMA2D控制器句柄（由bk\_dma2d\_new创建）

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效（handle为NULL）
- AVDK\_ERR\_DMA2D: DMA2D硬件初始化失败

**使用注意:**

- 必须在bk\_dma2d\_new之后调用
- 同一个handle不应该重复调用open，除非之前已经调用了close
- 打开失败后，建议调用bk\_dma2d\_delete释放资源
- 多个实例可以同时处于打开状态，组件内部会进行互斥保护

**示例代码:**

```
// 打开DMA2D控制器
ret = bk_dma2d_open(dma2d_handle);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to open DMA2D controller: %d\n", ret);
    bk_dma2d_delete(dma2d_handle);
    return ret;
}
LOGI("DMA2D controller opened successfully\n");
```

<a id="bk-dma2d-close-dma2d"></a>

### 3\. bk\_dma2d\_close \- 关闭DMA2D控制器

**功能描述:**

关闭已打开的DMA2D控制器，停止硬件模块并关闭相关时钟。关闭后如果需要再次使用，需要重新调用bk\_dma2d\_open。

**函数原型:**

```
avdk_err_t bk_dma2d_close(bk_dma2d_ctlr_handle_t handle);
```

**参数说明:**

- handle: \[输入\] DMA2D控制器句柄

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效（handle为NULL）

**使用注意:**

- 在不需要使用DMA2D功能时应该调用此函数以节省功耗
- 关闭前应确保所有DMA2D操作都已完成
- 异步操作应等待完成回调后再关闭
- 关闭后handle仍然有效，可以再次调用open
- 建议在关闭后调用delete释放资源

**示例代码:**

```
// 关闭DMA2D控制器
ret = bk_dma2d_close(dma2d_handle);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to close DMA2D controller: %d\n", ret);
    return ret;
}
LOGI("DMA2D controller closed successfully\n");
```

<a id="bk-dma2d-delete-dma2d"></a>

### 4\. bk\_dma2d\_delete \- 删除DMA2D控制器

**功能描述:**

删除DMA2D控制器实例，释放所有分配的资源。删除后handle将失效，不能再使用。

**函数原型:**

```
avdk_err_t bk_dma2d_delete(bk_dma2d_ctlr_handle_t handle);
```

**参数说明:**

- handle: \[输入\] DMA2D控制器句柄

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效（handle为NULL）

**使用注意:**

- 必须在bk\_dma2d\_close之后调用，否则可能导致资源泄漏
- 删除后应将handle设置为NULL，避免误用
- 如果控制器仍处于打开状态，会自动关闭后再删除
- 删除后handle指向的内存将被释放

**示例代码:**

```
// 删除DMA2D控制器
ret = bk_dma2d_delete(dma2d_handle);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to delete DMA2D controller: %d\n", ret);
    return ret;
}
dma2d_handle = NULL;
LOGI("DMA2D controller deleted successfully\n");
```

<a id="id6"></a>

## DMA2D功能操作

以下章节介绍DMA2D的各种功能操作API，包括填充、内存拷贝、像素格式转换和图层混合。
所有这些操作都需要在打开控制器后才能执行。

<a id="bk-dma2d-fill"></a>

### 5\. 内存填充操作 \- bk\_dma2d\_fill

**功能描述:**

使用指定颜色填充矩形区域。支持多种像素格式，可以填充整个帧或部分区域。

**函数原型:**

```
avdk_err_t bk_dma2d_fill(bk_dma2d_ctlr_handle_t handle, const dma2d_fill_config_t *config);
```

**参数说明:**

- handle: \[输入\] DMA2D控制器句柄
- config: \[输入\] 填充配置参数结构体指针

config结构体链接参考：[dma2d\_fill\_config\_t](../../api-reference/multimedia/bk_dma2d.md)

**配置结构体成员说明:**

- fill.frameaddr: 帧缓冲区起始地址
- fill.color: 填充颜色值（格式由color\_format决定）
- fill.color\_format: 填充颜色格式（out\_color\_mode\_t）
- fill.pixel\_byte: 每个像素的字节数（2/3/4）
- fill.frame\_xsize: 帧的宽度（像素）
- fill.frame\_ysize: 帧的高度（像素）
- fill.xpos: 填充区域的X坐标（基于帧起始地址）
- fill.ypos: 填充区域的Y坐标（基于帧起始地址）
- fill.width: 填充区域的宽度（像素）
- fill.height: 填充区域的高度（像素）
- transfer\_complete\_cb: 填充完成回调函数
- is\_sync: 是否同步操作（true\=同步，false\=异步）
- user\_data: 用户自定义数据，在回调中返回

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效
- AVDK\_ERR\_DMA2D: DMA2D操作失败

**使用注意:**

- 必须先调用bk\_dma2d\_open打开控制器
- 填充坐标(xpos, ypos)和尺寸(width, height)不能超出帧边界
- 同步模式下函数会阻塞直到填充完成
- 异步模式下立即返回，通过回调通知完成
- 填充颜色格式必须与pixel\_byte匹配

**示例代码:**

```
// 填充配置
dma2d_fill_config_t fill_config = {0};
fill_config.fill.frameaddr = dma2d_frame->frame;    // 帧起始地址
fill_config.fill.color = color;                      // 填充颜色
fill_config.fill.color_format = color_format;       // 填充颜色格式
fill_config.fill.pixel_byte = pixel_byte;           // 填充颜色字节数
fill_config.fill.frame_xsize = frame_width;         // 帧宽度
fill_config.fill.frame_ysize = frame_height;        // 帧高度
fill_config.fill.xpos = xpos;                        // 填充区域X坐标,基于帧起始地址（0，0）
fill_config.fill.ypos = ypos;                        // 填充区域Y坐标,基于帧起始地址（0，0）
fill_config.fill.width = fill_width;                // 填充区域宽度
fill_config.fill.height = fill_height;              // 填充区域高度
fill_config.transfer_complete_cb = bk_dma2d_fill_complete_cb;    // 填充完成回调
fill_config.is_sync = true;                          // 是否同步操作
fill_config.user_data = NULL;                        // 用户数据

// 执行填充操作
ret = bk_dma2d_fill(dma2d_handle, &fill_config);
if (ret != AVDK_ERR_OK) {
    // 错误处理
}
```

填充效果以及示意图卡如下：

<a id="id9"></a>
![../../_images/dma2d_fill_config.png](../../../../../_assets/84559638196f857a88df-dma2d_fill_config.png)


Figure 2\. dma2d color fill config

填充数据格式可选择：

```
/** DMA2D_Output_Color_Mode */
typedef enum {
        DMA2D_OUTPUT_ARGB8888 = 0, /**< ARGB8888 DMA2D color mode */
        DMA2D_OUTPUT_RGB888,       /**< RGB888 DMA2D color mode   */
        DMA2D_OUTPUT_RGB565,       /**< RGB565 DMA2D color mode   */
        DMA2D_OUTPUT_ARGB1555,     /**< ARGB1555 DMA2D color mode */
        DMA2D_OUTPUT_ARGB4444,     /**< ARGB4444 DMA2D color mode */
} out_color_mode_t;
```

<a id="bk-dma2d-memcpy"></a>

### 6\. 内存拷贝操作 \- bk\_dma2d\_memcpy

**功能描述:**

将图像数据从源地址拷贝到目标地址，支持带偏移的拷贝。可以拷贝整个帧或部分区域，输入输出格式必须相同。

**函数原型:**

```
avdk_err_t bk_dma2d_memcpy(bk_dma2d_ctlr_handle_t handle, const dma2d_memcpy_config_t *config);
```

**参数说明:**

- handle: \[输入\] DMA2D控制器句柄
- config: \[输入\] 内存拷贝配置参数结构体指针

config结构体链接参考：[dma2d\_memcpy\_config\_t](../../api-reference/multimedia/bk_dma2d.md)

**配置结构体成员说明:**

源帧配置:

- memcpy.input\_addr: 源帧缓冲区起始地址
- memcpy.src\_frame\_width: 源帧的宽度（像素）
- memcpy.src\_frame\_height: 源帧的高度（像素）
- memcpy.src\_frame\_xpos: 拷贝区域在源帧中的X坐标
- memcpy.src\_frame\_ypos: 拷贝区域在源帧中的Y坐标
- memcpy.input\_color\_mode: 源数据颜色格式（input\_color\_mode\_t）
- memcpy.src\_pixel\_byte: 源数据每像素字节数

目标帧配置:

- memcpy.output\_addr: 目标帧缓冲区起始地址
- memcpy.dst\_frame\_width: 目标帧的宽度（像素）
- memcpy.dst\_frame\_height: 目标帧的高度（像素）
- memcpy.dst\_frame\_xpos: 拷贝区域在目标帧中的X坐标
- memcpy.dst\_frame\_ypos: 拷贝区域在目标帧中的Y坐标
- memcpy.output\_color\_mode: 目标数据颜色格式（out\_color\_mode\_t）
- memcpy.dst\_pixel\_byte: 目标数据每像素字节数

拷贝区域配置:

- memcpy.dma2d\_width: 要拷贝的区域宽度（像素）
- memcpy.dma2d\_height: 要拷贝的区域高度（像素）

回调配置:

- transfer\_complete\_cb: 拷贝完成回调函数
- is\_sync: 是否同步操作（true\=同步，false\=异步）
- user\_data: 用户自定义数据

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效
- AVDK\_ERR\_DMA2D: DMA2D操作失败

**使用注意:**

- 输入和输出颜色格式必须相同
- 拷贝区域不能超出源帧和目标帧的边界
- 异步模式建议使用信号量等待完成
- 支持源和目标地址相同（原地操作）

**示例代码:**

```
// 内存拷贝配置
dma2d_memcpy_config_t memcpy_config = {0};
frame_buffer_t *src_frame = frame_buffer_display_malloc(src_width * src_height * pixel_byte);
AVDK_RETURN_ON_FALSE(src_frame, AVDK_ERR_NOMEM, TAG, "frame_buffer_display_malloc failed! \n");

frame_buffer_t *dst_frame = frame_buffer_display_malloc(dst_width * dst_height * pixel_byte);
if (!dst_frame) {
    LOGE("frame_buffer_display_malloc failed! \n");
    frame_buffer_display_free(src_frame);
    return AVDK_ERR_NOMEM;
}

// 初始化源数据和目标数据
memcopy_src_data_pre((uint8_t *)src_frame->frame, color, pixel_byte, src_width, src_height);
os_memset((void *)dst_frame->frame, 0, dst_width * dst_height * pixel_byte);

// src frame config
memcpy_config.memcpy.input_addr = (char *)src_frame->frame;
memcpy_config.memcpy.src_frame_width = src_width;
memcpy_config.memcpy.src_frame_height = src_height;
memcpy_config.memcpy.src_frame_xpos = src_frame_xpos;
memcpy_config.memcpy.src_frame_ypos = src_frame_ypos;
memcpy_config.memcpy.input_color_mode = color_format;
memcpy_config.memcpy.src_pixel_byte = pixel_byte;

// dst frame config
memcpy_config.memcpy.output_addr = (char *)dst_frame->frame;
memcpy_config.memcpy.dst_frame_width = dst_width;
memcpy_config.memcpy.dst_frame_height = dst_height;
memcpy_config.memcpy.dst_frame_xpos = dst_frame_xpos;
memcpy_config.memcpy.dst_frame_ypos = dst_frame_ypos;
memcpy_config.memcpy.output_color_mode = output_color_mode;
memcpy_config.memcpy.dst_pixel_byte = pixel_byte;

// dma2d memcpy config
memcpy_config.memcpy.dma2d_width = dma2d_width;
memcpy_config.memcpy.dma2d_height = dma2d_height;

// memcpy complete cb
memcpy_config.transfer_complete_cb = bk_dma2d_memcpy_complete_cb;
memcpy_config.is_sync = false;
memcpy_config.user_data = NULL;

// 执行内存拷贝
ret = bk_dma2d_memcpy(dma2d_handle, &memcpy_config);
if (ret != AVDK_ERR_OK) {
    // 错误处理
    frame_buffer_display_free(src_frame);
    frame_buffer_display_free(dst_frame);
    return ret;
}

// 释放资源
frame_buffer_display_free(src_frame);
frame_buffer_display_free(dst_frame);
```

源图片目标图片，带偏移的内存拷贝示意图可以参考：

<a id="id10"></a>
![../../_images/dma2d_memcpy.jpg](../../../../../_assets/f2c0853b13127ce2cb6a-dma2d_memcpy.jpg)


Figure 3\. dma2d memcpy config by pos

<a id="bk-dma2d-pixel-conversion"></a>

### 7\. 像素格式转换操作 \- bk\_dma2d\_pixel\_conversion

**功能描述:**

在拷贝图像数据的同时进行像素格式转换。配置参数与内存拷贝类似，但支持输入和输出使用不同的颜色格式。

**函数原型:**

```
avdk_err_t bk_dma2d_pixel_conversion(bk_dma2d_ctlr_handle_t handle, const dma2d_pfc_memcpy_config_t *config);
```

**参数说明:**

- handle: \[输入\] DMA2D控制器句柄
- config: \[输入\] 像素格式转换配置参数结构体指针

config结构体链接参考：[dma2d\_pfc\_memcpy\_config\_t](../../api-reference/multimedia/bk_dma2d.md)

**配置结构体成员说明:**

配置参数与bk\_dma2d\_memcpy相同，区别在于：

- pfc.input\_color\_mode: 源数据颜色格式，可与输出格式不同
- pfc.output\_color\_mode: 目标数据颜色格式，可与输入格式不同
- pfc.src\_pixel\_byte: 源像素字节数，根据输入格式确定
- pfc.dst\_pixel\_byte: 目标像素字节数，根据输出格式确定

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效
- AVDK\_ERR\_DMA2D: DMA2D操作失败

**使用注意:**

- 支持的输入格式：ARGB8888, RGB888, RGB565, ARGB1555, ARGB4444, L8, AL44, AL88, L4, A8, A4
- 支持的输出格式：ARGB8888, RGB888, RGB565, ARGB1555, ARGB4444
- 输入输出格式错误可能导致数据异常或硬件工作异常
- 格式转换可能会损失或增加颜色信息（如RGB565转RGB888）

**示例代码:**

```
// 像素格式转换配置
dma2d_pfc_memcpy_config_t pfc_config = {0};
frame_buffer_t *src_frame = frame_buffer_display_malloc(src_width * src_height * src_pixel_byte);
AVDK_RETURN_ON_FALSE(src_frame, AVDK_ERR_NOMEM, TAG, "frame_buffer_display_malloc failed! \n");

frame_buffer_t *dst_frame = frame_buffer_display_malloc(dst_width * dst_height * dst_pixel_byte);
if (!dst_frame) {
    LOGE("frame_buffer_display_malloc failed! \n");
    frame_buffer_display_free(src_frame);
    return AVDK_ERR_NOMEM;
}

// 初始化源数据和目标数据
os_memset((void *)dst_frame->frame, 0, dst_width * dst_height * dst_pixel_byte);

// src frame config
pfc_config.pfc.input_addr = (char *)src_frame->frame;
pfc_config.pfc.src_frame_width = src_width;
pfc_config.pfc.src_frame_height = src_height;
pfc_config.pfc.src_frame_xpos = src_frame_xpos;
pfc_config.pfc.src_frame_ypos = src_frame_ypos;
pfc_config.pfc.input_color_mode = input_color_mode;
pfc_config.pfc.src_pixel_byte = src_pixel_byte;

// dst frame config
pfc_config.pfc.output_addr = (char *)dst_frame->frame;
pfc_config.pfc.dst_frame_width = dst_width;
pfc_config.pfc.dst_frame_height = dst_height;
pfc_config.pfc.dst_frame_xpos = dst_frame_xpos;
pfc_config.pfc.dst_frame_ypos = dst_frame_ypos;
pfc_config.pfc.output_color_mode = output_color_mode;
pfc_config.pfc.dst_pixel_byte = dst_pixel_byte;

// dma2d memcpy config
pfc_config.pfc.dma2d_width = dma2d_width;
pfc_config.pfc.dma2d_height = dma2d_height;

// memcpy complete cb
pfc_config.transfer_complete_cb = bk_dma2d_pfc_complete_cb;
pfc_config.is_sync = true;
pfc_config.user_data = NULL;

// 执行像素格式转换
ret = bk_dma2d_pixel_conversion(dma2d_handle, &pfc_config);
if (ret != AVDK_ERR_OK) {
    LOGE("bk_dma2d_pixel_conversion failed! \n");
    frame_buffer_display_free(src_frame);
    frame_buffer_display_free(dst_frame);
    return ret;
}

// 释放资源
frame_buffer_display_free(src_frame);
frame_buffer_display_free(dst_frame);
```

<a id="bk-dma2d-blend"></a>

### 8\. 图层混合操作 \- bk\_dma2d\_blend

**功能描述:**

将前景和背景两个图层进行混合。DMA2D的图层混合是硬件实现，通过配置前景、背景以及输出的图片格式、透明度、数据地址、混合坐标等参数实现图片的融合。

**函数原型:**

```
avdk_err_t bk_dma2d_blend(bk_dma2d_ctlr_handle_t handle, const dma2d_blend_config_t *config);
```

**参数说明:**

- handle: \[输入\] DMA2D控制器句柄
- config: \[输入\] 混合配置参数结构体指针

config结构体链接参考：[dma2d\_blend\_config\_t](../../api-reference/multimedia/bk_dma2d.md)

**配置结构体成员说明:**

前景配置:

- blend.pfg\_addr: 前景图层缓冲区地址
- blend.fg\_frame\_width: 前景图层宽度
- blend.fg\_frame\_height: 前景图层高度
- blend.fg\_frame\_xpos: 前景拷贝区域X坐标
- blend.fg\_frame\_ypos: 前景拷贝区域Y坐标
- blend.fg\_color\_mode: 前景颜色格式（input\_color\_mode\_t）
- blend.fg\_pixel\_byte: 前景每像素字节数
- blend.fg\_alpha\_value: 前景透明度值（0x00-0xFF）
- blend.fg\_alpha\_mode: 前景Alpha模式（DMA2D\_NO\_MODIF\_ALPHA/DMA2D\_REPLACE\_ALPHA/DMA2D\_COMBINE\_ALPHA）
- blend.fg\_red\_blue\_swap: 前景红蓝交换（DMA2D\_RB\_REGULAR/DMA2D\_RB\_SWAP）

背景配置:

- blend.pbg\_addr: 背景图层缓冲区地址
- blend.bg\_frame\_width: 背景图层宽度
- blend.bg\_frame\_height: 背景图层高度
- blend.bg\_frame\_xpos: 背景混合区域X坐标
- blend.bg\_frame\_ypos: 背景混合区域Y坐标
- blend.bg\_color\_mode: 背景颜色格式（input\_color\_mode\_t）
- blend.bg\_pixel\_byte: 背景每像素字节数
- blend.bg\_alpha\_mode: 背景Alpha模式
- blend.bg\_red\_blue\_swap: 背景红蓝交换

输出配置:

- blend.pdst\_addr: 输出缓冲区地址
- blend.dst\_frame\_width: 输出帧宽度
- blend.dst\_frame\_height: 输出帧高度
- blend.dst\_frame\_xpos: 输出位置X坐标
- blend.dst\_frame\_ypos: 输出位置Y坐标
- blend.dst\_color\_mode: 输出颜色格式（out\_color\_mode\_t）
- blend.dst\_pixel\_byte: 输出每像素字节数
- blend.dst\_red\_blue\_swap: 输出红蓝交换

混合区域配置:

- blend.dma2d\_width: 混合区域宽度
- blend.dma2d\_height: 混合区域高度

回调配置:

- transfer\_complete\_cb: 混合完成回调函数
- is\_sync: 是否同步操作
- user\_data: 用户自定义数据

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效
- AVDK\_ERR\_DMA2D: DMA2D操作失败

**使用注意:**

- Alpha模式说明：
  \- DMA2D\_NO\_MODIF\_ALPHA: 保持原图的透明度，alpha\_value不生效
  \- DMA2D\_REPLACE\_ALPHA: 替换原图的透明度为alpha\_value
  \- DMA2D\_COMBINE\_ALPHA: 透明度 \= (原透明度 × alpha\_value) / 0xFF
- 输出地址可以与前景或背景地址相同（原地混合），但需确保内存大小足够
- 混合坐标必须在各自帧的边界内
- 前景通常使用包含Alpha通道的格式（如ARGB8888）

**示例代码:**

```
dma2d_blend_config_t blend_config = {0};

// fg config - 前景配置
blend_config.blend.pfg_addr = (char *)fg_frame->frame;
blend_config.blend.fg_frame_width = fg_width;
blend_config.blend.fg_frame_height = fg_height;
blend_config.blend.fg_frame_xpos = fg_frame_xpos;
blend_config.blend.fg_frame_ypos = fg_frame_ypos;
blend_config.blend.fg_color_mode = input_fg_mode;
blend_config.blend.fg_pixel_byte = fg_pixel_byte;

// bg config - 背景配置
blend_config.blend.pbg_addr = (char *)bg_frame->frame;
blend_config.blend.bg_frame_width = bg_width;
blend_config.blend.bg_frame_height = bg_height;
blend_config.blend.bg_frame_xpos = bg_frame_xpos;
blend_config.blend.bg_frame_ypos = bg_frame_ypos;
blend_config.blend.bg_color_mode = input_bg_mode;
blend_config.blend.bg_pixel_byte = bg_pixel_byte;

// dst config - 输出配置
blend_config.blend.pdst_addr = (char *)dst_frame->frame;
blend_config.blend.dst_frame_width = dst_width;
blend_config.blend.dst_frame_height = dst_height;
blend_config.blend.dst_frame_xpos = dst_frame_xpos;
blend_config.blend.dst_frame_ypos = dst_frame_ypos;
blend_config.blend.dst_color_mode = output_mode;
blend_config.blend.dst_pixel_byte = dst_pixel_byte;

// dma2d blend size config - 混合尺寸配置
blend_config.blend.dma2d_width = dma2d_width;
blend_config.blend.dma2d_height = dma2d_height;

// alpha config - 透明度配置
blend_config.blend.fg_alpha_value = fg_alpha_value;
blend_config.blend.fg_alpha_mode = DMA2D_NO_MODIF_ALPHA;
blend_config.blend.bg_alpha_mode = DMA2D_NO_MODIF_ALPHA;

// color swap config - 颜色交换配置
blend_config.blend.fg_red_blue_swap = DMA2D_RB_SWAP;
blend_config.blend.bg_red_blue_swap = DMA2D_RB_REGULAR;
blend_config.blend.dst_red_blue_swap = DMA2D_RB_REGULAR;

// callback config - 回调配置
blend_config.transfer_complete_cb = bk_dma2d_blend_complete_cb;
blend_config.is_sync = true;
blend_config.user_data = NULL;

// 执行混合操作
ret = bk_dma2d_blend(dma2d_handle, &blend_config);
if (ret != AVDK_ERR_OK) {
    LOGE("bk_dma2d_blend failed! \n");
    return ret;
}
```

其中：

fg\_alpha\_value为不透明度，0为完全透明， 0xff为完全不透明。
fg\_alpha\_value值是否有效以及如何取值 取决于前景或背景的alpha\_mode。
如果alpha\_mode为：

```
1) DMA2D_NO_MODIF_ALPHA：即保持原图片的透明度，不管input_alpha 值设置为多少都不生效。
2) DMA2D_REPLACE_ALPHA：替换原图的alpha(透明度)，图片的透明度替换成alpha_value的值。
3) DMA2D_COMBINE_ALPHA：图片的透明度为(原有的透明度 * input_alpha)/0xFF.
即如果源图片中某些像素的alpha为0(完全透明)，配置input_alpha后，该像素的alpha仍为0,常用于保持原图的透明效果。
```

配置示意图如下：

<a id="id11"></a>
![../../_images/dma2d_blend.jpg](../../../../../_assets/d4cc74b9bc2184ec7fa3-dma2d_blend.jpg)


Figure 4\. dma2d blend config by pos

**关于输出地址复用:**

如果输出的图像所占用的内存大小不超过前景或背景的内存大小, 输出的地址可以和前景背景共用，例如:

- 前景DMA2D\_INPUT\_RGB888（3字节）, 背景DMA2D\_INPUT\_ARGB8888（4字节）,输出DMA2D\_OUTPUT\_ARGB8888（4字节），那么输出的地址可以设置为背景地址
- 反之, 如果前景DMA2D\_INPUT\_RGB888（3字节）, 背景DMA2D\_INPUT\_RGB565（2字节）,输出DMA2D\_OUTPUT\_RGB888（3字节）, 则输出地址不能与背景复用

<a id="id7"></a>

## 使用建议和注意事项

**API调用顺序:**

1. 必须按照 new -\> open -\> 操作 -\> close -\> delete 的顺序调用API
2. 在执行任何DMA2D操作前，必须先成功调用bk\_dma2d\_new和bk\_dma2d\_open
3. 不要在未打开控制器的情况下调用操作API（fill/memcpy/pfc/blend）

**内存和资源管理:**

1. 操作完成后应及时调用bk\_dma2d\_close关闭控制器以节省功耗
2. 不再使用时应调用bk\_dma2d\_delete释放资源
3. 异步操作模式下，需要在传输完成回调函数中释放显示帧的内存
4. 删除控制器后，应将handle设置为NULL避免误用

**参数配置:**

1. 确保配置参数中的宽度和高度在有效范围内，不要超出硬件限制
2. 配置的坐标点均是基于原图片的像素坐标，不要超过帧的边界
3. 像素格式必须正确配置，否则可能导致数据异常或硬件工作异常
4. 填充、拷贝、混合区域的(xpos \+ width)不能超过frame\_width
5. 填充、拷贝、混合区域的(ypos \+ height)不能超过frame\_height

**同步与异步:**

1. 同步模式（is\_sync\=true）会阻塞直到操作完成，适合简单场景
2. 异步模式（is\_sync\=false）立即返回，需要通过回调或信号量等待完成
3. 异步模式下应确保回调函数简洁高效，避免长时间阻塞
4. 异步操作完成前不要释放相关的缓冲区

**多实例使用:**

1. 支持创建多个DMA2D控制器实例用于不同场景
2. 所有实例共享同一个DMA2D硬件模块
3. 组件内部会进行互斥保护，确保硬件访问安全
4. 可以使用bk\_dma2d\_get\_handle()获取已创建的句柄

**性能优化:**

1. 对于频繁使用的场景，保持控制器打开状态而不是反复open/close
2. 尽量使用硬件支持的原生格式，避免不必要的格式转换
3. 大数据量操作建议使用异步模式，避免阻塞主线程
4. 混合操作时，输出地址可以复用背景地址以节省内存（需满足大小条件）

<a id="id8"></a>

## DMA2D API函数列表

**控制器生命周期管理:**

- bk\_dma2d\_new: 创建DMA2D控制器实例
- bk\_dma2d\_open: 打开DMA2D控制器，启动硬件
- bk\_dma2d\_close: 关闭DMA2D控制器，停止硬件
- bk\_dma2d\_delete: 删除DMA2D控制器实例，释放资源
- bk\_dma2d\_get\_handle: 获取已创建的DMA2D控制器句柄

**DMA2D功能操作:**

- bk\_dma2d\_fill: 使用指定颜色填充矩形区域
- bk\_dma2d\_memcpy: 带偏移的内存拷贝操作
- bk\_dma2d\_pixel\_conversion: 像素格式转换操作
- bk\_dma2d\_blend: 前景背景图层混合操作

**其他功能:**

- bk\_dma2d\_ioctl: DMA2D控制操作（软复位等）
