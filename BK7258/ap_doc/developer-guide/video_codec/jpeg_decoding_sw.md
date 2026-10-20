---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/video_codec/jpeg_decoding_sw.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="jpeg"></a>

# JPEG 软件解码

<a id="id1"></a>

## 1、概述

> 本节主要说明JPEG软件解码器的使用方法、API介绍及相关的数据结构。软件解码器使用CPU实现JPEG图像的解码过程，提供更灵活的解码选项和输出格式支持。

- 有关JPEG解码的示例工程，请参阅：

  - [JPEG解码示例工程](../../examples/projects/jpeg_decode_example.md)
- 有关API参考，请参阅：

  - [JPEG软解码 API](../../api-reference/multimedia/bk_jpegdec_sw.md)

<a id="id3"></a>

## 2、支持的功能

> 1、支持JPEG标准格式解码；
>
> 2、支持获取图像信息（宽度、高度、格式等）；
>
> 3、支持回调机制处理解码完成事件；
>
> 4、支持多种输出格式（RGB565、RGB888、YUYV等）；
>
> 5、支持图像旋转功能（在YUYV格式下支持90度、180度、270度旋转）；
>
> 6、支持大小端字节序配置；
>
> 7、支持多核优化执行；
>
> 8、支持同步和异步解码模式；
>
> 9、支持扩展控制接口。

警告

软件解码的旋转功能仅在输出格式为YUYV时支持。

重要

**回调函数使用注意事项：**

1）回调函数中不建议执行阻塞操作（如长时间等待、sleep等），以避免影响解码性能和系统响应；

2）例外情况：在解码任务中获取图像时，允许在回调函数中进行必要的阻塞等待；

3）建议在回调函数中仅进行轻量级操作，如设置标志位、发送消息/信号量等，将耗时操作放到其他任务中执行。

<a id="id4"></a>

## 3、相关头文件

> - `components/bk_jpeg_decode/bk_jpeg_decode_sw.h`
> - `components/bk_jpeg_decode/bk_jpeg_decode_types_sw.h`
> - `components/bk_jpeg_decode/bk_jpeg_decode_types.h`

<a id="id5"></a>

## 4、配置选项

<a id="id6"></a>

### 4.1 线程栈大小配置

软件JPEG解码器的线程栈大小可以通过Kconfig进行配置：

> - **CONFIG\_SW\_JPEG\_DECODE\_TASK\_STACK\_SIZE**: 软件JPEG解码任务的线程栈大小（字节）
>
>   - 默认值：1024 字节
>   - 配置路径：menuconfig -\> JPEG Decoder -\> Software JPEG decode task stack size
>   - 说明：根据实际解码场景和内存资源调整栈大小，如遇到栈溢出可适当增大此值

<a id="id7"></a>

## 5、JPEG解码参考工程

> 该示例的完整路径: `./projects/jpeg_decode_example`
>
> 该示例主要展示了如何使用JPEG解码器，包括硬件解码和软件解码。
>
> 该示例的主要流程如下：
> 1\. 创建并打开JPEG解码器（硬件或软件）。
> 2\. 获取图像信息。
> 3\. 执行解码操作。
> 4\. 关闭并删除JPEG解码器。

<a id="id8"></a>

## 6、使用示例

> 以下是使用JPEG软件解码器的简单示例代码：

```
#include "components/bk_jpeg_decode/bk_jpeg_decode_sw.h"
#include "frame_buffer.h"

static bk_jpeg_decode_sw_handle_t sw_decoder = NULL;
static beken_semaphore_t decode_complete_semaphore = NULL;

// 解码完成回调函数
bk_err_t decode_complete_callback(uint32_t format_type, uint32_t result, frame_buffer_t *out_frame)
{
    if (result == BK_OK)
    {
        LOGD("JPEG decode success!\n");
    }
    else
    {
        LOGE("JPEG decode failed! Result: %d\n", result);
    }

    if (decode_complete_semaphore != NULL)
    {
        rtos_set_semaphore(&decode_complete_semaphore);
    }

    return BK_OK;
}

// JPEG软件解码示例函数
bk_err_t jpeg_sw_decode_example(uint8_t *jpeg_data, uint32_t jpeg_length)
{
    bk_err_t ret = BK_OK;
    frame_buffer_t *in_frame = NULL;
    frame_buffer_t *out_frame = NULL;
    bk_jpeg_decode_img_info_t img_info = {0};

    // 1. 初始化配置
    bk_jpeg_decode_sw_config_t config = {
        .decode_cbs = {
            .out_complete = decode_complete_callback,
        },
        .core_id = 0,
        .out_format = JPEG_DECODE_SW_OUT_FORMAT_YUYV,
        .byte_order = JPEG_DECODE_LITTLE_ENDIAN,
    };

    // 2. 创建并打开解码器（标准版本）
    // 对于多核优化版本，可以使用：bk_software_jpeg_decode_on_multi_core_new
    ret = bk_software_jpeg_decode_new(&sw_decoder, &config);
    if (ret != BK_OK) {
        LOGE("Create software decoder failed!\n");
        return ret;
    }

    ret = bk_jpeg_decode_sw_open(sw_decoder);
    if (ret != BK_OK) {
        LOGE("Open software decoder failed!\n");
        bk_jpeg_decode_sw_delete(sw_decoder);
        return ret;
    }

    // 初始化信号量用于同步
    ret = rtos_init_semaphore(&decode_complete_semaphore, 1);
    if (ret != BK_OK) {
        LOGE("Init semaphore failed!\n");
        bk_jpeg_decode_sw_close(sw_decoder);
        bk_jpeg_decode_sw_delete(sw_decoder);
        return ret;
    }

    // 3. 分配并填充输入缓冲区
    in_frame = frame_buffer_encode_malloc(jpeg_length);
    if (in_frame == NULL) {
        LOGE("Allocate input buffer failed!\n");
        ret = BK_FAIL;
        goto exit;
    }
    in_frame->length = jpeg_length;
    in_frame->size = jpeg_length;
    os_memcpy(in_frame->frame, jpeg_data, jpeg_length);

    // 4. 获取图像信息
    img_info.frame = in_frame;
    ret = bk_jpeg_decode_sw_get_img_info(sw_decoder, &img_info);
    if (ret != BK_OK) {
        LOGE("Get image info failed!\n");
        goto exit;
    }
    LOGD("Image info: %dx%d, format: %d\n", img_info.width, img_info.height, img_info.format);

    // 5. 分配输出缓冲区
    out_frame = frame_buffer_display_malloc(img_info.width * img_info.height * 2);
    if (out_frame == NULL) {
        LOGE("Allocate output buffer failed!\n");
        ret = BK_FAIL;
        goto exit;
    }
    out_frame->width = img_info.width;
    out_frame->height = img_info.height;
    out_frame->fmt = PIXEL_FMT_YUYV;

    // 6. 设置输出格式（软件解码器特有功能）
    bk_jpeg_decode_sw_out_frame_info_t out_config = {
        .out_format = JPEG_DECODE_SW_OUT_FORMAT_YUYV,
        .byte_order = JPEG_DECODE_LITTLE_ENDIAN,
    };
    ret = bk_jpeg_decode_sw_set_config(sw_decoder, &out_config);
    if (ret != BK_OK) {
        LOGE("Set output config failed!\n");
        goto exit;
    }

    // 7. 执行解码（同步方式）
    ret = bk_jpeg_decode_sw_decode(sw_decoder, in_frame, out_frame);
    // 对于异步方式，可以使用：bk_jpeg_decode_sw_decode_async

    if (ret != BK_OK) {
        LOGE("Start decode failed!\n");
        goto exit;
    }

    // 等待解码完成
    ret = rtos_get_semaphore(&decode_complete_semaphore, 2000); // 软件解码可能需要更长时间
    if (ret != BK_OK) {
        LOGE("Decode timeout!\n");
        goto exit;
    }

    LOGI("JPEG software decode example completed successfully!\n");

exit:
    // 8. 释放资源
    if (in_frame != NULL) {
        frame_buffer_encode_free(in_frame);
    }
    if (out_frame != NULL) {
        frame_buffer_display_free(out_frame);
    }
    if (decode_complete_semaphore != NULL) {
        rtos_deinit_semaphore(&decode_complete_semaphore);
    }
    if (sw_decoder != NULL) {
        bk_jpeg_decode_sw_close(sw_decoder);
        bk_jpeg_decode_sw_delete(sw_decoder);
    }

    return ret;
}
```

**多核优化版本示例**

以下是使用多核优化的JPEG软件解码器示例：

```
// JPEG多核优化软件解码示例函数
bk_err_t jpeg_sw_multi_core_decode_example(uint8_t *jpeg_data, uint32_t jpeg_length)
{
    bk_err_t ret = BK_OK;
    frame_buffer_t *in_frame = NULL;
    frame_buffer_t *out_frame = NULL;
    bk_jpeg_decode_img_info_t img_info = {0};

    // 1. 初始化配置
    bk_jpeg_decode_sw_config_t config = {
        .decode_cbs = {
            .out_complete = decode_complete_callback,
        },
        .core_id = JPEG_DECODE_CORE_ID_1,  // 使用核心1
        .out_format = JPEG_DECODE_SW_OUT_FORMAT_YUYV,
        .byte_order = JPEG_DECODE_LITTLE_ENDIAN,
    };

    // 2. 创建并打开多核优化解码器
    ret = bk_software_jpeg_decode_on_multi_core_new(&sw_decoder, &config);
    if (ret != BK_OK) {
        LOGE("Create multi-core decoder failed!\n");
        return ret;
    }

    // 后续步骤与标准软件解码器类似
    // ...

    return ret;
}
```
