---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_jpegdec_sw.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="jpegapi"></a>

# JPEG软件解码API

<a id="id1"></a>

## 概述

> 本节主要介绍JPEG软件解码器的API及相关数据结构。软件解码器利用CPU来解码JPEG图像，提供灵活的解码方案。

- 有关JPEG解码的详细信息，请参阅：

  - [JPEG解码概述](../../developer-guide/video_codec/jpeg_decoding.md)
  - [JPEG软件解码指南](../../developer-guide/video_codec/jpeg_decoding_sw.md)
- 有关JPEG解码的示例工程，请参阅：

  - [JPEG解码示例工程](../../examples/projects/jpeg_decode_example.md)

<a id="api"></a>

## API参考

1. **bk\_software\_jpeg\_decode\_new**

创建一个新的软件JPEG解码器实例。

```
avdk_err_t bk_software_jpeg_decode_new(bk_jpeg_decode_sw_handle_t *handle, bk_jpeg_decode_sw_config_t *config);
```

- 参数:
  \- handle: 解码器句柄指针，用于存储创建的解码器实例
  \- config: 解码器配置参数，包括回调函数、输出格式等
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

2. **bk\_software\_jpeg\_decode\_on\_multi\_core\_new**

创建一个新的针对多核执行优化的软件JPEG解码器实例。

```
avdk_err_t bk_software_jpeg_decode_on_multi_core_new(bk_jpeg_decode_sw_handle_t *handle, bk_jpeg_decode_sw_config_t *config);
```

- 参数:
  \- handle: 解码器句柄指针，用于存储创建的解码器实例
  \- config: 解码器配置参数，包括回调函数、输出格式等
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

3. **bk\_jpeg\_decode\_sw\_open**

打开软件JPEG解码器。

```
avdk_err_t bk_jpeg_decode_sw_open(bk_jpeg_decode_sw_handle_t handle);
```

- 参数:
  \- handle: 软件解码器句柄，通过bk\_software\_jpeg\_decode\_new或bk\_software\_jpeg\_decode\_on\_multi\_core\_new获得
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

4. **bk\_jpeg\_decode\_sw\_close**

关闭软件JPEG解码器。

```
avdk_err_t bk_jpeg_decode_sw_close(bk_jpeg_decode_sw_handle_t handle);
```

- 参数:
  \- handle: 软件解码器句柄
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

5. **bk\_jpeg\_decode\_sw\_decode**

开始JPEG解码过程。

```
avdk_err_t bk_jpeg_decode_sw_decode(bk_jpeg_decode_sw_handle_t handle, frame_buffer_t *frame, frame_buffer_t *out_frame);
```

- 参数:
  \- handle: 软件解码器句柄
  \- frame: 输入JPEG帧缓冲区，包含编码的JPEG数据
  \- out\_frame: 输出解码帧缓冲区，用于存储解码后的图像
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

6. **bk\_jpeg\_decode\_sw\_decode\_async**

以异步方式开始JPEG解码过程。

```
avdk_err_t bk_jpeg_decode_sw_decode_async(bk_jpeg_decode_sw_handle_t handle, frame_buffer_t *frame);
```

- 参数:
  \- handle: 软件解码器句柄
  \- frame: 输入JPEG帧缓冲区，包含编码的JPEG数据
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

7. **bk\_jpeg\_decode\_sw\_delete**

删除软件JPEG解码器实例。

```
avdk_err_t bk_jpeg_decode_sw_delete(bk_jpeg_decode_sw_handle_t handle);
```

- 参数:
  \- handle: 软件解码器句柄
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

8. **bk\_jpeg\_decode\_sw\_set\_config**

设置软件JPEG解码器的输出帧配置。

```
avdk_err_t bk_jpeg_decode_sw_set_config(bk_jpeg_decode_sw_handle_t handle, bk_jpeg_decode_sw_out_frame_info_t *config);
```

- 参数:
  \- handle: 软件解码器句柄
  \- config: 要设置的输出帧配置参数
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

9. **bk\_jpeg\_decode\_sw\_get\_img\_info**

在解码前获取图像信息。

```
avdk_err_t bk_jpeg_decode_sw_get_img_info(bk_jpeg_decode_sw_handle_t handle, bk_jpeg_decode_img_info_t *info);
```

- 参数:
  \- handle: 软件解码器句柄
  \- info: 用于存储获取的图像信息的指针
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

10. **bk\_jpeg\_decode\_sw\_ioctl**

软件JPEG解码器的扩展控制接口。

```
avdk_err_t bk_jpeg_decode_sw_ioctl(bk_jpeg_decode_sw_handle_t handle, bk_jpeg_decode_sw_ioctl_cmd_t cmd, void *param);
```

- 参数:
  \- handle: 软件解码器句柄
  \- cmd: 命令码，指定要执行的操作
  \- param: 与操作相关的命令参数
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

11. **bk\_get\_jpeg\_data\_info**

获取JPEG图像数据信息的函数，可独立调用。

```
avdk_err_t bk_get_jpeg_data_info(bk_jpeg_decode_img_info_t *img_info);
```

- 参数:
  \- img\_info: \[输入\] 图像信息结构指针，解析后的数据信息也在img\_info结构体中，结构体中frame不能为空，且frame-\>frame和frame-\>length需要为有效数据
- 返回值:
  \- AVDK\_ERR\_OK: 成功
  \- 其他: 失败

<a id="id4"></a>

## API类型定义

1. **bk\_jpeg\_decode\_sw\_handle\_t**

软件JPEG解码器句柄类型，用于引用软件JPEG解码器实例。

```
typedef struct bk_jpeg_decode_sw *bk_jpeg_decode_sw_handle_t;
```

2. **bk\_jpeg\_decode\_sw\_config\_t**

软件JPEG解码器配置结构体。

```
typedef struct bk_jpeg_decode_sw_config
{
    bk_jpeg_decode_callback_t decode_cbs;  /*!< JPEG解码回调函数 */
    uint32_t core_id;                     /*!< 解码器将运行的CPU核心ID */
    bk_jpeg_decode_sw_out_format_t out_format; /*!< 输出图像格式 */
    bk_jpeg_decode_byte_order_t byte_order;  /*!< 解码数据的字节序 */
} bk_jpeg_decode_sw_config_t;
```

3. **bk\_jpeg\_decode\_sw\_out\_frame\_info\_t**

软件JPEG解码器输出帧信息结构体。

```
typedef struct bk_jpeg_decode_sw_out_frame_info
{
    bk_jpeg_decode_sw_out_format_t out_format; /*!< 输出图像格式 */
    bk_jpeg_decode_byte_order_t byte_order;  /*!< 解码数据的字节序 */
} bk_jpeg_decode_sw_out_frame_info_t;
```

4. **bk\_jpeg\_decode\_sw\_ioctl\_cmd\_t**

软件JPEG解码器扩展命令枚举。

```
typedef enum
{
    JPEG_DECODE_SW_IOCTL_CMD_BASE = 0,                  /*!< 软件解码器的基础命令起始值 */
} bk_jpeg_decode_sw_ioctl_cmd_t;
```

5. **bk\_jpeg\_decode\_sw\_out\_format\_t**

软件JPEG解码器输出格式枚举。

```
typedef enum
{
    JPEG_DECODE_SW_OUT_FORMAT_GRAY = 0,                 /*!< 灰度输出格式 */
    JPEG_DECODE_SW_OUT_FORMAT_RGB565 = 1,               /*!< RGB565输出格式（每像素16位） */
    JPEG_DECODE_SW_OUT_FORMAT_RGB888 = 2,               /*!< RGB888输出格式（每像素24位） */
    JPEG_DECODE_SW_OUT_FORMAT_YUYV = 3,                 /*!< YUYV交错格式（4:2:2） */
    JPEG_DECODE_SW_OUT_FORMAT_YUYV_ROTATE_90 = 4,       /*!< YUYV格式，顺时针旋转90度 */
    JPEG_DECODE_SW_OUT_FORMAT_YUYV_ROTATE_180 = 5,      /*!< YUYV格式，旋转180度 */
    JPEG_DECODE_SW_OUT_FORMAT_YUYV_ROTATE_270 = 6,      /*!< YUYV格式，顺时针旋转270度 */
    JPEG_DECODE_SW_OUT_FORMAT_VYUY = 7,                 /*!< VYUY交错格式（另一种4:2:2） */
    JPEG_DECODE_SW_OUT_FORMAT_VUYY = 8,                 /*!< VUYY交错格式（再一种4:2:2） */
} bk_jpeg_decode_sw_out_format_t;
```

6. **bk\_jpeg\_decode\_byte\_order\_t**

JPEG解码字节序枚举。

```
typedef enum{
    JPEG_DECODE_LITTLE_ENDIAN = 0,  /*!< 小端字节序（最低有效字节在前） */
    JPEG_DECODE_BIG_ENDIAN           /*!< 大端字节序（最高有效字节在前） */
} bk_jpeg_decode_byte_order_t;
```

7. **bk\_jpeg\_decode\_rotate\_info\_t**

JPEG解码旋转信息结构体。

```
typedef struct bk_jpeg_decode_rotate_info
{
    uint32_t rotate_angle;  /*!< 旋转角度 */
    uint8_t *rotate_buf;    /*!< 旋转缓冲区 */
} bk_jpeg_decode_rotate_info_t;
```

8. **bk\_jpeg\_decode\_out\_format\_info\_t**

JPEG解码输出格式命令结构体。

```
typedef struct bk_jpeg_decode_out_format_info
{
    bk_jpeg_decode_sw_out_format_t out_format;  /*!< 输出图像格式（RGB565, RGB888, YUYV等） */
} bk_jpeg_decode_out_format_info_t;
```

9. **bk\_jpeg\_decode\_byte\_order\_info\_t**

JPEG解码字节序命令结构体。

```
typedef struct bk_jpeg_decode_byte_order_info
{
    bk_jpeg_decode_byte_order_t byte_order;  /*!< 字节序（JPEG_DECODE_LITTLE_ENDIAN或JPEG_DECODE_BIG_ENDIAN） */
} bk_jpeg_decode_byte_order_info_t;
```

10. **jpeg\_decode\_status\_t**

JPEG解码器状态枚举。

```
typedef enum
{
    JPEG_DECODE_DISABLED = 0,  /*!< 解码器已禁用，无法执行解码操作 */
    JPEG_DECODE_ENABLED        /*!< 解码器已启用，准备执行解码操作 */
} jpeg_decode_status_t;
```

11. **jpeg\_img\_fmt\_t**

JPEG图像格式枚举。

```
typedef enum
{
    JPEG_FMT_ERR,           /*!< 无效或不支持的图像格式 */
    JPEG_FMT_YUV444,        /*!< YUV 4:4:4格式 - 完整色度分辨率，无子采样 */
    JPEG_FMT_YUV422,        /*!< YUV 4:2:2格式 - 水平色度子采样2:1 */
    JPEG_FMT_YUV420,        /*!< YUV 4:2:0格式 - 水平和垂直色度子采样2:1 */
    JPEG_FMT_YUV400,        /*!< YUV 4:0:0格式 - 灰度图像，仅亮度分量 */
} jpeg_img_fmt_t;
```

12. **bk\_jpeg\_decode\_img\_info\_t**

JPEG解码图像信息结构体。

```
typedef struct bk_jpeg_decode_img_info_t
{
    frame_buffer_t *frame;  /*!< 包含编码JPEG数据的帧缓冲区 */
    uint32_t width;         /*!< 输出: 图像宽度（像素） */
    uint32_t height;        /*!< 输出: 图像高度（像素） */
    jpeg_img_fmt_t format;  /*!< 输出: 图像格式（YUV444, YUV422, YUV420等） */
} bk_jpeg_decode_img_info_t;
```

13. **bk\_jpeg\_decode\_callback\_t**

JPEG解码回调函数结构体。

**回调函数使用注意事项：**

- 不建议在回调函数中执行阻塞或耗时操作（如长时间等待、休眠等），以免影响解码性能和系统响应性。
- 回调函数应仅执行轻量级操作，如设置标志位、发送消息/信号量等，将耗时操作移至其他任务中处理。

```
typedef struct {
    bk_err_t (*in_complete)(frame_buffer_t *in_frame); /*!< 输入数据解码完成回调 */
    frame_buffer_t *(*out_malloc)(uint32_t size); /*!< 分配输出缓冲区回调 */
    bk_err_t (*out_complete)(uint32_t format_type, uint32_t result, frame_buffer_t *out_frame); /*!< 输出数据处理完成回调 */
} bk_jpeg_decode_callback_t;
```

14. **bk\_jpeg\_decode\_sw\_t**

软件JPEG解码器操作结构体。

```
typedef struct bk_jpeg_decode_sw
{
    avdk_err_t (*open)(bk_jpeg_decode_sw_handle_t handle); /*!< 打开软件JPEG解码器 */
    avdk_err_t (*close)(bk_jpeg_decode_sw_handle_t handle); /*!< 关闭软件JPEG解码器 */
    avdk_err_t (*decode)(bk_jpeg_decode_sw_handle_t handle, frame_buffer_t *in_frame, frame_buffer_t *out_frame); /*!< 解码JPEG帧 */
    avdk_err_t (*decode_async)(bk_jpeg_decode_sw_handle_t handle, frame_buffer_t *in_frame); /*!< 异步解码JPEG帧 */
    avdk_err_t (*delete_sw)(bk_jpeg_decode_sw_handle_t handle); /*!< 删除软件JPEG解码器实例 */
    avdk_err_t (*set_config)(bk_jpeg_decode_sw_handle_t handle, bk_jpeg_decode_sw_out_frame_info_t *config); /*!< 设置解码图像的输出格式 */
    avdk_err_t (*get_img_info)(bk_jpeg_decode_sw_handle_t handle, bk_jpeg_decode_img_info_t *info); /*!< 解码前获取图像信息 */
    avdk_err_t (*ioctl)(bk_jpeg_decode_sw_handle_t handle, bk_jpeg_decode_sw_ioctl_cmd_t cmd, void *param); /*!< 附加功能的扩展接口 */
} bk_jpeg_decode_sw_t;
```
