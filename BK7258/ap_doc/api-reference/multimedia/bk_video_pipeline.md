---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_video_pipeline.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="video-pipeline-api"></a>

# VIDEO PIPELINE API

<a id="id1"></a>

## 概述

> 本节主要介绍Video Pipeline的API及相关数据结构。
> Video Pipeline是管理视频数据流的组件，提供统一接口来处理H264编码和图像旋转等功能，简化多模块协同工作的复杂性。

- 有关Video Pipeline的详细信息，请参阅：

  - [Video Pipeline 开发指南](../../developer-guide/video_codec/video_pipeline.md)
- 有关Video Pipeline的示例工程，请参阅：

  - [Video Pipeline 示例项目](../../examples/projects/video_pipeline_example.md)

<a id="api"></a>

## API参考

1. **bk\_video\_pipeline\_new**

创建并初始化一个新的Video Pipeline实例。

```
avdk_err_t bk_video_pipeline_new(bk_video_pipeline_handle_t *handle, bk_video_pipeline_config_t *config);
```

- 参数:
  \- handle\[out\]: 用于存储创建的Pipeline实例的句柄指针
  \- config\[in\]: Video Pipeline配置参数
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

2. **bk\_video\_pipeline\_open\_h264e**

打开并配置Video Pipeline中的H.264编码器模块。

```
avdk_err_t bk_video_pipeline_open_h264e(bk_video_pipeline_handle_t handle, bk_video_pipeline_h264e_config_t *config);
```

- 参数:
  \- handle\[in\]: Video Pipeline句柄
  \- config\[in\]: 用于H.264编码的Video Pipeline配置参数
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

3. **bk\_video\_pipeline\_close\_h264e**

关闭Video Pipeline中的H.264编码器模块。

```
avdk_err_t bk_video_pipeline_close_h264e(bk_video_pipeline_handle_t handle);
```

- 参数:
  \- handle\[in\]: Video Pipeline句柄
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

4. **bk\_video\_pipeline\_open\_rotate**

打开并配置Video Pipeline中的图像旋转模块。

```
avdk_err_t bk_video_pipeline_open_rotate(bk_video_pipeline_handle_t handle, bk_video_pipeline_decode_config_t *config);
```

- 参数:
  \- handle\[in\]: Video Pipeline句柄
  \- config\[in\]: 用于图像旋转的Video Pipeline配置参数
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

5. **bk\_video\_pipeline\_close\_rotate**

关闭Video Pipeline中的图像旋转模块。

```
avdk_err_t bk_video_pipeline_close_rotate(bk_video_pipeline_handle_t handle);
```

- 参数:
  \- handle\[in\]: Video Pipeline句柄
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

6. **bk\_video\_pipeline\_get\_module\_status**

获取Video Pipeline中指定模块的启用状态。

```
avdk_err_t bk_video_pipeline_get_module_status(bk_video_pipeline_handle_t handler, video_pipeline_module_t module, video_pipeline_module_status_t *status);
```

- 参数:
  \- handler\[in\]: Video Pipeline句柄
  \- module\[in\]: 要查询的模块（H264E或ROTATE）
  \- status\[out\]: 用于存储模块状态的指针
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

7. **bk\_video\_pipeline\_reset\_decode**

重置Video Pipeline中的解码模块以重新检测图像格式。

此函数在切换摄像头时用于内部重新获取图像格式。

```
avdk_err_t bk_video_pipeline_reset_decode(bk_video_pipeline_handle_t handler);
```

- 参数:
  \- handler\[in\]: Video Pipeline句柄
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

8. **bk\_video\_pipeline\_delete**

删除并释放与Video Pipeline实例关联的资源。

```
avdk_err_t bk_video_pipeline_delete(bk_video_pipeline_handle_t handle);
```

- 参数:
  \- handle\[in\]: Video Pipeline句柄
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

9. **bk\_video\_pipeline\_ioctl**

Video Pipeline的扩展接口，用于附加功能，如获取编码器状态等。

```
avdk_err_t bk_video_pipeline_ioctl(bk_video_pipeline_handle_t handle, video_pipeline_ioctl_cmd_t cmd, void *param);
```

- 参数:
  \- handle\[in\]: Video Pipeline句柄
  \- cmd\[in\]: 命令码（在video\_pipeline\_ioctl\_cmd\_t中定义）
  \- param\[in,out\]: 命令参数
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

<a id="id3"></a>

## API类型定义

1. **BK\_H264\_ENCODE\_864X480\_30FPS\_CONFIG**

864x480分辨率、30FPS的默认H.264编码配置宏。

此宏提供了H.264编码的默认配置，包括：
\- 分辨率：864x480
\- 帧率：30 FPS
\- 软件解码旋转角度：默认:ROTATE\_NONE 可选值:(ROTATE\_NONE, ROTATE\_90, ROTATE\_180, ROTATE\_270)

```
#define BK_H264_ENCODE_864X480_30FPS_CONFIG() \n{
    .width = 864, \
    .height = 480, \
    .fps = FPS30, \
    .sw_rotate_angle = ROTATE_NONE, \
}
```

2. **bk\_video\_pipeline\_handle\_t**

Video Pipeline句柄类型，用于引用Video Pipeline实例。

```
typedef struct bk_video_pipeline *bk_video_pipeline_handle_t;
```

3. **bk\_video\_pipeline\_config\_t**

Video Pipeline配置结构体。
该结构体定义了Video Pipeline的主要配置参数。

```
typedef struct bk_video_pipeline_config
{
    const jpeg_callback_t *jpeg_cbs; /*!< JPEG解码回调函数 */
    const decode_callback_t *decode_cbs; /*!< 图像编解码回调函数 */
} bk_video_pipeline_config_t;
```

4. **bk\_video\_pipeline\_h264e\_config\_t**

Video Pipeline H.264编码器配置结构体。
该结构体定义了Video Pipeline中H.264编码器的配置参数。

**注意：** sw\_rotate\_angle 参数使用 media\_rotate\_t 枚举类型，而非数字。

```
typedef struct bk_video_pipeline_h264e_config
{
    uint16_t width;                      /**< 视频帧宽度 */
    uint16_t height;                     /**< 视频帧高度 */
    uint32_t fps;                        /**< 帧率 */
    media_rotate_t sw_rotate_angle;      /**< 软件旋转角度 (media_rotate_t类型) */
    const bk_h264e_callback_t *h264e_cb; /*!< H.264编码器回调函数 */
} bk_video_pipeline_h264e_config_t;
```

5. **bk\_video\_pipeline\_decode\_config\_t**

Video Pipeline解码配置结构体。
该结构体定义了Video Pipeline中解码模块的配置参数。

**注意：** rotate\_angle 参数使用 media\_rotate\_t 枚举类型，而非数字。

```
typedef struct bk_video_pipeline_decode_config
{
    media_rotate_mode_t rotate_mode;   /*!< 旋转模式 (SW_ROTATE: 软件旋转, HW_ROTATE: 硬件旋转) */
    media_rotate_t rotate_angle;       /*!< 旋转角度 (media_rotate_t类型) */
} bk_video_pipeline_decode_config_t;
```

6. **bk\_video\_pipeline\_t**

Video Pipeline操作结构体。
该结构体定义了Video Pipeline实例可用的操作。

```
typedef struct bk_video_pipeline
{
    avdk_err_t (*open_h264e)(bk_video_pipeline_handle_t handle, bk_video_pipeline_h264e_config_t *config); /*!< 打开H.264编码器 */
    avdk_err_t (*close_h264e)(bk_video_pipeline_handle_t handle); /*!< 关闭H.264编码器 */
    avdk_err_t (*open_rotate)(bk_video_pipeline_handle_t handle, bk_video_pipeline_decode_config_t *config); /*!< 打开图像旋转模块 */
    avdk_err_t (*close_rotate)(bk_video_pipeline_handle_t handle); /*!< 关闭图像旋转模块 */
    avdk_err_t (*encode_h264e)(bk_video_pipeline_handle_t handle, frame_buffer_t *frame); /*!< 使用H.264编码器编码帧 */
    avdk_err_t (*reset_decode)(bk_video_pipeline_handle_t handle); /*!< 重置解码模块，此函数在切换摄像头时用于内部重新获取图像格式 */
    avdk_err_t (*get_module_status)(bk_video_pipeline_handle_t handle, video_pipeline_module_t module, video_pipeline_module_status_t *status); /*!< 获取模块启用状态 */
    avdk_err_t (*delete_video_pipeline)(bk_video_pipeline_handle_t handle); /*!< 删除Video Pipeline实例 */
    avdk_err_t (*ioctl)(bk_video_pipeline_handle_t handle, video_pipeline_ioctl_cmd_t cmd, void *param); /*!< 扩展接口用于附加功能 */
} bk_video_pipeline_t;
```

7. **media\_rotate\_t**

媒体旋转角度枚举。
该枚举定义了图像的旋转角度。

**重要说明：**

- **内部统一使用 media\_rotate\_t 结构体**：所有解码和编码模块内部统一使用 media\_rotate\_t 枚举类型表示旋转角度。
- **外部数据转换**：如果外部传入的是数字数据（如 0, 90, 180, 270），需要先转换为 media\_rotate\_t 枚举值（ROTATE\_NONE, ROTATE\_90, ROTATE\_180, ROTATE\_270），再传入内部函数。

```
typedef enum {
    ROTATE_NONE = 0,  /*!< 不旋转 */
    ROTATE_90,        /*!< 旋转90度 */
    ROTATE_180,       /*!< 旋转180度 (暂不支持，保留用于未来扩展) */
    ROTATE_270,       /*!< 旋转270度 */
} media_rotate_t;
```

8. **dec\_end\_type\_t**

解码器结束类型枚举。
该枚举定义了解码器的结束操作类型。

```
typedef enum
{
    HW_DEC_END = 0,  /*!< 硬件解码结束 */
    SW_DEC_END,      /*!< 软件解码结束 */
} dec_end_type_t;
```

9. **h264e\_state\_t**

H.264编码器工作状态枚举。
该枚举定义了H.264编码器的工作状态。

```
typedef enum
{
    H264E_STATE_IDLE = 0,      /*!< 编码器空闲状态 */
    H264E_STATE_ENCODING       /*!< 编码器编码状态 */
} h264e_state_t;
```

10. **video\_pipeline\_module\_t**

Video Pipeline模块类型枚举。
该枚举定义了Video Pipeline中的不同模块类型。

```
typedef enum
{
    VIDEO_PIPELINE_MODULE_H264E = 0,   /*!< H.264编码器模块 */
    VIDEO_PIPELINE_MODULE_ROTATE,      /*!< 图像旋转模块 */
} video_pipeline_module_t;
```

11. **video\_pipeline\_module\_status\_t**

Video Pipeline模块状态枚举。
该枚举定义了Video Pipeline中模块的启用状态。

```
typedef enum
{
    VIDEO_PIPELINE_MODULE_DISABLED = 0,  /*!< 模块禁用状态 */
    VIDEO_PIPELINE_MODULE_ENABLED        /*!< 模块启用状态 */
} video_pipeline_module_status_t;
```

12. **video\_pipeline\_ioctl\_cmd\_t**

Pipeline扩展命令枚举。
该枚举定义了Video Pipeline的扩展命令。

```
typedef enum
{
    VIDEO_PIPELINE_IOCTL_CMD_BASE = 0,                  /*!< 基础命令起始值 */
} video_pipeline_ioctl_cmd_t;
```

13. **bk\_h264e\_callback\_t**

H.264编码器回调结构体。
该结构体定义了H.264编码操作的回调函数，包括内存分配和完成通知。

**回调函数使用注意事项：**

- 不建议在回调函数中执行阻塞或耗时操作（如长时间等待、休眠等），以免影响编码性能和系统响应性。
- 回调函数应仅执行轻量级操作，如设置标志位、发送消息/信号量等，将耗时操作移至其他任务中处理。

```
typedef struct
{
    /**
     * @brief 为帧缓冲区分配内存
     * @param size 要分配的内存大小
     * @return 指向分配的帧缓冲区的指针
     */
    frame_buffer_t *(*malloc)(uint32_t size);

    /**
     * @brief 帧编码完成回调
     * @param frame 指向帧缓冲区的指针
     * @param result 编码操作的结果
     */
    void (*complete)(frame_buffer_t *frame, bk_err_t result);
} bk_h264e_callback_t;
```

14. **jpeg\_callback\_t**

JPEG解码回调结构体。
该结构体定义了JPEG解码操作的回调函数。

**回调函数使用注意事项：**

- 不建议在回调函数中执行阻塞或耗时操作（如长时间等待、休眠等），以免影响解码性能和系统响应性。
- 回调函数应仅执行轻量级操作，如设置标志位、发送消息/信号量等，将耗时操作移至其他任务中处理。
- **例外：** `read()` 回调函数可以在内部进行短暂的阻塞等待来获取准备好的JPEG缓冲区。

```
typedef struct {
    frame_buffer_t *(*read)(uint32_t timeout_ms);    /*!< 读取/获取准备好的JPEG缓冲区的回调，允许短暂的阻塞等待 */
    bk_err_t (*complete)(bk_err_t result, frame_buffer_t *out_frame); /*!< 解码完成时的回调 */
} jpeg_callback_t;
```

15. **decode\_callback\_t**

图像编解码回调结构体。
该结构体定义了图像编解码操作的回调函数。

**回调函数使用注意事项：**

- 不建议在回调函数中执行阻塞或耗时操作（如长时间等待、休眠等），以免影响解码性能和系统响应性。
- 回调函数应仅执行轻量级操作，如设置标志位、发送消息/信号量等，将耗时操作移至其他任务中处理。

```
typedef struct {
    frame_buffer_t *(*malloc)(uint32_t size);    /*!< 分配帧缓冲区的回调 */
    bk_err_t (*free)(frame_buffer_t *frame);     /*!< 释放帧缓冲区的回调 */
    bk_err_t (*complete)(dec_end_type_t format_type, bk_err_t result, frame_buffer_t *out_frame); /*!< 处理完成时的回调 */
} decode_callback_t;
```
