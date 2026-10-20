---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/video_codec/video_pipeline.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="video-pipeline"></a>

# Video Pipeline

<a id="id1"></a>

## 1、概述

> 本节主要说明Video Pipeline模块的使用方法、API介绍及相关的数据结构。Video Pipeline模块提供了视频编解码和图像旋转等功能的统一管理接口，简化了多模块协同工作的复杂度。

- 有关Video Pipeline的示例工程，请参阅：

  - [Video Pipeline示例工程](../../examples/projects/video_pipeline_example.md)
- 有关Video Pipeline的API参考，请参阅：

  - [Video Pipeline API](../../api-reference/multimedia/bk_video_pipeline.md)
- H264编码图像效果修改，请参阅：

  - [H264硬编码 开发指南](h264_encoding_hw.md)

<a id="id3"></a>

## 2、Video Pipeline基础信息

<a id="id4"></a>

### 2.1 支持的功能

> - 支持H.264视频编码功能；
> - 支持图像旋转功能（硬件旋转和软件旋转）；
> - 支持多种旋转角度（90度、180度、270度等）；
> - 支持模块状态查询；
> - 支持回调机制处理编解码完成事件；
> - 支持JPEG解码集成；
> - 支持扩展控制接口。

警告

1）该模块在在DVP摄像头时不会调用，默认在UVC摄像头时调用，也可以单独用于解码jpeg图像，在回调中控制输出图像；

2）该模块在硬解码时，给到H264模块的数据是旋转前的数据，在软解码时，给到H264模块的数据是旋转后的数据；

3）该模块在硬解码时，90度和270度是支持硬件旋转的，如果需要旋转180度，只能使用软件旋转，软件旋转速度慢于硬件旋转；

4）旋转参数需要保证一致；
旋转模块的旋转参数是video\_pipeline\_config.decode\_cfg.rotate\_angle，
H264模块的旋转参数是video\_pipeline\_config.h264e\_cfg.sw\_rotate\_angle，
否则会出现硬解码和软解码摄像头屏幕显示不一致；

5）经过硬件旋转后的数据格式为RGB565，如果需要进行其他处理或显示，需要配置为RGB565格式；
软件旋转后的数据格式为YUYV格式；，如果需要进行其他处理或显示，需要配置为YUYV格式；

<a id="id5"></a>

### 2.2 相关头文件

> - `components/bk_video_pipeline/bk_video_pipeline.h`
> - `components/bk_video_pipeline/bk_video_pipeline_types.h`

<a id="id6"></a>

### 2.3 参考工程

> 该示例的完整路径: `./projects/video_pipeline_example`
>
> 该示例主要展示了如何使用Video Pipeline模块，包括H.264编码和图像旋转功能的使用及其组合使用。
>
> 该示例的主要流程如下：
>
> > - 1. 创建Video Pipeline实例。
> > - 2. 配置并打开相应功能模块（H.264编码器或旋转模块,详见下面的使用示例中参数配置）。
> > - 3. 执行相应操作（编码或旋转）。
> > - 4. 查询模块状态（可选）。
> > - 5. 关闭相应功能模块。
> > - 6. 删除Video Pipeline实例。

<a id="id7"></a>

### 2.4 内存占用

video pipeline模块最多需要（DECODE\_MAX\_PIPELINE\_LINE\_SIZE \+ ROTATE\_MAX\_PIPELINE\_LINE\_SIZE）大小的内存，
用于存储解码后的图像和旋转后的图像，具体大小见 `mux_pipeline.h` 中宏配置，默认解码 864\*480 的图像，需要 0X1B000 的大小的内存；

通过宏 `CONFIG_BT_REUSE_MEDIA_MEMORY` 可以配置在多媒体运行时，能否使用蓝牙的内存来进行处理，如果该宏配置为Y，
则需要在video pipeline模块调用 `bk_video_pipeline_open_h264e` 和\`\`bk\_video\_pipeline\_open\_rotate\`\` 前将蓝牙关闭，否则会出现异常dump；

如果 `CONFIG_BT_REUSE_MEDIA_MEMORY` 配置为N，则video pipeline模块会在打开对应模块时自动申请的内存来进行处理，且后续不再释放；
避免因重复申请释放出现内存碎片化后，无法申请到足够大的内存；
如果解码的图像宽度超过864，需要更改 `IMAGE_MAX_WIDTH` 宏配置；

警告

后续有需求可以在video pipeline模块关闭后调用接口 `uvc_pipeline_deinit` 和 `deinit_all_buffer` 来释放相关内存占用；

<a id="id8"></a>

## 3、常见应用场景

常见场景主要是UVC摄像头硬解码，UVC摄像头软解码和DVP摄像头解码；

DVP摄像头场景下不建议使用该模块；

UVC摄像头硬解码和UVC摄像头软解码是在内部在获取到第一帧图像后，获取到图像信息，内部根据图像信息选择使用硬解码还是软解码；
硬解码和软解码图像输出格式不一致，使用时需要注意。

<a id="uvc"></a>

### 3.1 UVC 摄像头硬件解码

<a id="id9"></a>

#### 3.1.1 图像输入

UVC摄像头硬解码图像数输入需要为YUV422格式，图像宽度需要为32的整数倍，高度需要为16的整数倍；

<a id="id10"></a>

#### 3.1.2 图像输出

UVC硬解码场景下，推荐配置硬件旋转，输出图像格式为RGB565，硬件旋转不支持180度旋转，如需要180度旋转，请配置软件旋转，输出图像格式为YUYV；

警告

1. 如果需要输出YUYV格式，请配置软件旋转，软件旋转支持0，90，180，270度旋转；
2. 如果需要输出RGB88格式，请关闭宏 `CONFIG_SW_ROTATE_TO_YUYV_AND_DMA2D_TO_YUYV_NOT_RGB888` （RGB888输出不支持旋转0度）

<a id="id11"></a>

#### 3.1.3 H264编码图像输出

H264编码后的数据通过 `h264e_cbs` 中的 `complete` 函数回调输出，回调中包含编码结果和frame\_buffer\_t类型的指针，
编码成功后数据可以进行其他处理，如存储到文件、发送到网络等，编码失败时需要释放frame\_buffer\_t类型的指针；

frame\_buffer\_t结构体中可以通过 `frame_buffer_t.h264_type` 可以获取到当前图像的类型；
:   - 如果 `frame_buffer_t.h264_type` 为 `H264_TYPE_I` ，则为I帧；
    - 如果 `frame_buffer_t.h264_type` 为 `H264_TYPE_P` ，则为P帧；
    - I帧输出间隔通过宏 `CONFIG_H264_P_FRAME_CNT` 配置，默认值为29，即每30帧输出一个I帧；

H264编码效果修改方法见文档： [H264硬编码 开发指南](h264_encoding_hw.md)

<a id="id13"></a>

### 3.2 UVC 摄像头软件解码

<a id="id14"></a>

#### 3.1.1 图像输入

UVC摄像头硬解码图像数输入需要为YUV420格式，图像宽度需要为2的整数倍，高度没有限制;

输出格式为YUYV，YUYV格式中，两个Y分量共用一组UV，因此Y的数量需要2的倍数；

<a id="id15"></a>

#### 3.1.2 图像输出

UVC摄像头数据解码数据为YUYV格式，解码后数据已经旋转了，不需要再经过旋转模块；

<a id="id16"></a>

#### 3.1.3 H264编码图像输出

H264编码后的数据通过 `h264e_cbs` 中的 `complete` 函数回调输出，回调中包含编码结果和frame\_buffer\_t类型的指针，
编码成功后数据可以进行其他处理，如存储到文件、发送到网络等，编码失败时需要释放frame\_buffer\_t类型的指针；

frame\_buffer\_t结构体中可以通过 `frame_buffer_t.h264_type` 可以获取到当前图像的类型;
:   - 如果 `frame_buffer_t.h264_type` 为 `H264_TYPE_I` ，则为I帧；
    - 如果 `frame_buffer_t.h264_type` 为 `H264_TYPE_P` ，则为P帧；
    - I帧输出间隔通过宏 `CONFIG_H264_P_FRAME_CNT` 配置，默认值为29，即每30帧输出一个I帧；

H264编码效果修改方法见文档： [H264硬编码 开发指南](h264_encoding_hw.md)

警告

软解码时，给到H264模块的数据是经过了旋转的，因此显示和硬解码时的图像旋转角度不一致，需要根据实际情况进行调整；

<a id="dvp"></a>

### 3.3 DVP 摄像头

DVP场景下不建议使用该模块，因为video pipeline模块需要整帧的jpeg图像，而DVP可以直接输出YUV格式的数据，可以直接给到H264模块和显示模块；

<a id="id18"></a>

## 4、模块参数配置和函数调用

下面详细描述了模块的参数配置和函数调用；

<a id="id19"></a>

### 4.1 初始化模块

<a id="id20"></a>

#### 4.1.1 初始化参数配置

初始化时，需要传入 `jpeg_cbs` 和 `decode_cbs` ，结构体均不可以为空；

`jpeg_cbs` 在解码时使用，硬解码/软解码均会使用该结构体中的 `malloc` 函数获取一帧图像进行解码，在解码完成后调用该结构体中的 `complete` 函数释放该图像；

`decode_cbs` 在旋转和软解码时使用，
:   - 旋转前使用结构体中 `malloc` 申请一帧frame存储解码后的数据，旋转完成后，通过 `complete` 函数释放，释放失败尝试使用 `free` 直接释放；
    - 软解码时先使用结构体中 `malloc` 申请一帧frame用于解码，解码完成后，通过 `complete` 函数释放；

`decode_cbs` 中 `complete` 函数在解码结束时返回，解码成功时，frame可以用于显示等操作，解码失败时，该frame应该直接释放；

```
//全局的video pipeline句柄
static bk_video_pipeline_handle_t g_video_pipeline_handle = NULL;

// JPEG回调函数，解码完成时调用，用于释放解码前的图像帧，可以在该处添加自定义的处理逻辑
static bk_err_t jpeg_complete(bk_err_t result, frame_buffer_t *out_frame)
{
    frame_buffer_encode_free(out_frame);
    return BK_OK;
}

// JPEG读取函数，内部解码前获取一帧图像用于解码，需要根据实际情况修改
static frame_buffer_t *jpeg_read(uint32_t timeout_ms)
{
    //TODO 从JPEG缓存中获取一帧图像数据，需要根据实际情况修改
    frame_buffer_t *frame = frame_buffer_encode_malloc(jpeg_data_length);
    if (frame == NULL) {
        LOGE("jpeg_read malloc failed\r\n");
        return NULL;
    }
    // 复制JPEG数据到frame_buffer_t结构体中
    os_memcpy(frame->frame, jpeg_data, jpeg_data_length);
    frame->width = 864;
    frame->height = 480;
    frame->fmt = PIXEL_FMT_JPEG;
    frame->length = jpeg_data_length;
    return frame;
}
// JPEG解码配置，需要根据实际情况修改
static const jpeg_callback_t jpeg_cbs = {
    .read = jpeg_read,
    .complete = jpeg_complete,
};

// 显示frame的释放函数，需要根据实际情况修改
static bk_err_t display_frame_free_cb(void *frame)
{
    frame_buffer_display_free((frame_buffer_t *)frame);
    return BK_OK;
}
//解码完成回调函数， 当解码完成时调用，format_type为解码完成的格式类型，result为解码结果，out_frame为解码后的图像帧，
// 可以在该处添加自定义的处理逻辑，例如显示图像、保存图像等
static bk_err_t decode_complete(uint32_t format_type, uint32_t result, frame_buffer_t *out_frame)
{
    bk_err_t ret = BK_FAIL;
    if (result != BK_OK)
    {
        //解码失败时，直接释放对应的buffer
        display_frame_free_cb(out_frame);
        return BK_OK;
    }
    if (format_type == HW_DEC_END)
    {
        LOGI("Decode complete with result: %d\n", result);
        //TODO 给到显示模块进行显示
        display_frame_free_cb(out_frame);
        return BK_OK;
    }
    else if (format_type == SW_DEC_END)
    {
        //TODO 给到显示模块进行显示
        display_frame_free_cb(out_frame);
    }
    return ret;
}

// 解码后的frame申请函数，需要根据实际情况修改
static frame_buffer_t *decode_malloc(uint32_t size)
{
    return frame_buffer_encode_malloc(size);
}
// 解码后的frame释放函数，需要根据实际情况修改
static bk_err_t decode_free(frame_buffer_t *frame)
{
    frame_buffer_encode_free(frame);
    return BK_OK;
}
// 解码回调结构体，需要根据实际情况修改
static const decode_callback_t decode_cbs = {
    .malloc = decode_malloc,
    .free = decode_free,
    .complete = decode_complete,
};
```

<a id="id21"></a>

#### 4.1.2 初始化函数配置

```
bk_err_t ret = BK_FAIL;
bk_video_pipeline_config_t video_pipeline_config = {0};

if (g_video_pipeline_handle == NULL) {
    video_pipeline_config.jpeg_cbs = &jpeg_cbs; // 配置JPEG回调函数,用于获取一帧JPEG图像和释放图像
    video_pipeline_config.decode_cbs = &decode_cbs; // 配置解码回调函数，用于申请存放解码后的图像，释放图像，以及通知上层解码图像的状态
    //创建一个新的video pipeline实例
    ret = bk_video_pipeline_new(&g_video_pipeline_handle, &video_pipeline_config);
    if (ret != BK_OK) {
        LOGE("bk_video_pipeline_new failed, ret: %d\n", ret);
        return ret;
    }
}
```

<a id="id22"></a>

### 4.2 打开旋转功能

<a id="id23"></a>

#### 4.2.1 旋转功能参数配置

旋转功能主要参数为旋转模式和旋转角度，
:   - 旋转模式包括硬件旋转和软件旋转两种模式；
    - 旋转角度使用 `media_rotate_t` 枚举类型，可配置 ROTATE\_NONE、ROTATE\_90、ROTATE\_180、ROTATE\_270。

该参数在软解码时不生效，软解码时，旋转角度在 `bk_video_pipeline_h264e_config_t` 中配置。

备注

旋转角度参数必须使用 `media_rotate_t` 枚举类型，不能使用数字（如 0、90、180、270）。

无特殊需求，推荐使用硬件旋转，因为硬件旋转速度快，不会影响解码性能。

硬件旋转不支持180度旋转，如需要180度旋转，请配置软件旋转，输出图像格式为YUYV；

警告

1. 如果需要输出YUYV格式，请配置软件旋转，软件旋转支持0，90，180，270度旋转；
2. 如果需要输出RGB88格式，请关闭宏 `CONFIG_SW_ROTATE_TO_YUYV_AND_DMA2D_TO_YUYV_NOT_RGB888` （RGB888输出不支持旋转0度）

```
bk_video_pipeline_decode_config_t video_pipeline_decode_config = {0};
// 配置硬件旋转
video_pipeline_decode_config.rotate_mode = HW_ROTATE; // 硬件旋转模式
video_pipeline_decode_config.rotate_angle = ROTATE_90; // 90度旋转（使用media_rotate_t枚举类型）
```

<a id="id24"></a>

#### 4.2.2 旋转功能函数配置

```
// 打开旋转功能
ret = bk_video_pipeline_open_rotate(g_video_pipeline_handle, &video_pipeline_decode_config);
if (ret != BK_OK) {
    LOGE("bk_video_pipeline_open_rotate failed, ret: %d\n", ret);
    return ret;
}
```

<a id="h-264"></a>

### 4.3 打开H.264编码功能

<a id="id25"></a>

#### 4.3.1 H264编码功能参数配置

回调函数

```
// H.264编码回调函数
static frame_buffer_t *h264e_frame_malloc(uint32_t size)
{
    return frame_buffer_encode_malloc(size);
}

static void h264e_frame_complete(frame_buffer_t *frame, int result)
{
    if (result != AVDK_ERR_OK) {
        LOGI("H264 encode failed with result: %d\n", result);
        frame_buffer_encode_free(frame);
    } else {
        LOGI("H264 encode success, frame size: %d\n", frame->length);
        //TODO 编码后的frame处理
        frame_buffer_encode_free(frame);
    }
}

static const bk_h264e_callback_t h264e_cbs = {
    .malloc = h264e_frame_malloc,
    .complete = h264e_frame_complete,
};
```

参数配置

```
bk_video_pipeline_h264e_config_t video_pipeline_h264e_config = {0};

// 配置video pipeline H.264编码器
video_pipeline_h264e_config.width = 864; // 编码分辨率宽度，单位px
video_pipeline_h264e_config.height = 480; // 编码分辨率，单位px
video_pipeline_h264e_config.fps = FPS30; // 编码帧率，单位fps
video_pipeline_h264e_config.sw_rotate_angle = ROTATE_NONE; // 软件旋转角度（使用media_rotate_t枚举类型），ROTATE_NONE为不旋转，支持ROTATE_NONE、ROTATE_90、ROTATE_180、ROTATE_270
// 配置video pipeline H.264编码器回调函数
video_pipeline_h264e_config.h264e_cb = &h264e_cbs;
```

<a id="id26"></a>

#### 4.3.2 H264编码功能函数配置

```
// 打开H.264编码器
ret = bk_video_pipeline_open_h264e(g_video_pipeline_handle, &video_pipeline_h264e_config);
if (ret != BK_OK) {
    LOGE("bk_video_pipeline_open_h264e failed, ret: %d\n", ret);
    return ret;
}
```

<a id="id27"></a>

### 4.4 关闭旋转功能

```
// 关闭旋转功能
ret = bk_video_pipeline_close_rotate(g_video_pipeline_handle);
if (ret != BK_OK) {
    LOGE("bk_video_pipeline_close_rotate failed, ret: %d\n", ret);
    return ret;
}
```

<a id="id28"></a>

### 4.5 关闭H.264编码功能

```
// 关闭H.264编码器
ret = bk_video_pipeline_close_h264e(g_video_pipeline_handle);
if (ret != BK_OK) {
    LOGE("bk_video_pipeline_close_h264e failed, ret: %d\n", ret);
    return ret;
}
```

<a id="id29"></a>

### 4.6 获取模块状态

```
// 获取H.264编码器状态
ret = bk_video_pipeline_get_module_status(g_video_pipeline_handle, VIDEO_PIPELINE_MODULE_H264E, &h264e_state);
// 获取旋转模块状态
ret = bk_video_pipeline_get_module_status(g_video_pipeline_handle, VIDEO_PIPELINE_MODULE_ROTATE, &rotate_state);
```

<a id="id30"></a>

### 4.7 重置解码状态

该函数仅在摄像头切换时调用，为了让内部模块再次获取jpeg图像时，判断使用硬解码流程还是软解码流程；

```
// 重置解码状态
ret = bk_video_pipeline_reset_decode(g_video_pipeline_handle);
if (ret != BK_OK) {
    LOGE("bk_video_pipeline_reset_decode failed, ret: %d\n", ret);
    return ret;
}
```

<a id="id31"></a>

### 4.8 清理资源

```
if (g_video_pipeline_handle != NULL) {
    //删除内部资源
    bk_video_pipeline_delete(g_video_pipeline_handle);
    //将外部的全局指针设为NULL
    g_video_pipeline_handle = NULL;
}
```
