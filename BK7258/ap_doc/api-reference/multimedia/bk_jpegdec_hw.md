---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_jpegdec_hw.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="jpegapi"></a>

# JPEG硬件解码API

<a id="id1"></a>

## 概述

> 本节主要介绍JPEG硬件解码器的API及相关数据结构。硬件解码器利用专用硬件加速JPEG图像解码过程，提供更高的解码性能。

- 有关JPEG解码的详细信息，请参阅：

  - [JPEG解码概述](../../developer-guide/video_codec/jpeg_decoding.md)
  - [JPEG硬件解码指南](../../developer-guide/video_codec/jpeg_decoding_hw.md)
- 有关JPEG解码的示例工程，请参阅：

  - [JPEG解码示例工程](../../examples/projects/jpeg_decode_example.md)

<a id="api"></a>

## API参考

1. **bk\_hardware\_jpeg\_decode\_new**

创建一个新的硬件JPEG解码器实例。

```
avdk_err_t bk_hardware_jpeg_decode_new(bk_jpeg_decode_hw_handle_t *handle, bk_jpeg_decode_hw_config_t *config);
```

- 参数:
  \- handle: 解码器句柄指针，用于存储创建的解码器实例
  \- config: 解码器配置参数，包括回调函数等
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

1.1. **bk\_hardware\_jpeg\_decode\_opt\_new**

创建一个新的硬件优化JPEG解码器实例。

```
avdk_err_t bk_hardware_jpeg_decode_opt_new(bk_jpeg_decode_hw_handle_t *handle, bk_jpeg_decode_hw_opt_config_t *config);
```

- 参数:
  \- handle: 解码器句柄指针，用于存储创建的解码器实例
  \- config: 优化解码器配置参数，包括回调函数、SRAM缓冲区、块大小等
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

备注

此优化解码器支持使用SRAM缓冲区分块解码图像，可降低峰值内存使用并提高解码效率。

2. **bk\_jpeg\_decode\_hw\_open**

打开硬件JPEG解码器。

```
avdk_err_t bk_jpeg_decode_hw_open(bk_jpeg_decode_hw_handle_t handle);
```

- 参数:
  \- handle: 硬件解码器句柄
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

3. **bk\_jpeg\_decode\_hw\_close**

关闭硬件JPEG解码器。

```
avdk_err_t bk_jpeg_decode_hw_close(bk_jpeg_decode_hw_handle_t handle);
```

- 参数:
  \- handle: 硬件解码器句柄
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

4. **bk\_jpeg\_decode\_hw\_decode**

开始JPEG同步解码过程。

```
avdk_err_t bk_jpeg_decode_hw_decode(bk_jpeg_decode_hw_handle_t handle, frame_buffer_t *frame, frame_buffer_t *out_frame);
```

- 参数:
  \- handle: 硬件解码器句柄
  \- frame: 输入JPEG帧缓冲区，包含编码的JPEG数据
  \- out\_frame: 输出解码帧缓冲区，用于存储解码后的图像
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

5. **bk\_jpeg\_decode\_hw\_decode\_async**

开始JPEG异步解码过程。

```
avdk_err_t bk_jpeg_decode_hw_decode_async(bk_jpeg_decode_hw_handle_t handle, frame_buffer_t *frame);
```

- 参数:
  \- handle: 硬件解码器句柄
  \- frame: 输入JPEG帧缓冲区，包含编码的JPEG数据
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

6. **bk\_jpeg\_decode\_hw\_delete**

删除硬件JPEG解码器实例。

```
avdk_err_t bk_jpeg_decode_hw_delete(bk_jpeg_decode_hw_handle_t handle);
```

- 参数:
  \- handle: 硬件解码器句柄
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

7. **bk\_jpeg\_decode\_hw\_get\_img\_info**

在解码前获取图像信息。

```
avdk_err_t bk_jpeg_decode_hw_get_img_info(bk_jpeg_decode_hw_handle_t handle, bk_jpeg_decode_img_info_t *info);
```

- 参数:
  \- handle: 硬件解码器句柄
  \- info: 用于存储获取的图像信息的指针
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

8. **bk\_jpeg\_decode\_hw\_ioctl**

硬件JPEG解码器的扩展控制接口。

```
avdk_err_t bk_jpeg_decode_hw_ioctl(bk_jpeg_decode_hw_handle_t handle, bk_jpeg_decode_hw_ioctl_cmd_t cmd, void *param);
```

- 参数:
  \- handle: 硬件解码器句柄
  \- cmd: 命令码，指定要执行的操作
  \- param: 与操作相关的命令参数
- 返回值:
  \- BK\_OK: 成功
  \- 其他: 失败（错误码表示具体失败原因）

9. **bk\_get\_jpeg\_data\_info**

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

1. **bk\_jpeg\_decode\_hw\_handle\_t**

硬件JPEG解码器句柄类型，用于引用硬件JPEG解码器实例。

```
typedef struct bk_jpeg_decode_hw *bk_jpeg_decode_hw_handle_t;
```

2. **bk\_jpeg\_decode\_hw\_config\_t**

硬件JPEG解码器配置结构体。

```
typedef struct bk_jpeg_decode_hw_config
{
    bk_jpeg_decode_callback_t decode_cbs;  /*!< JPEG解码回调函数 */
} bk_jpeg_decode_hw_config_t;
```

2.1. **bk\_jpeg\_decode\_hw\_opt\_config\_t**

硬件优化JPEG解码器配置结构体。

```
typedef struct bk_jpeg_decode_hw_opt_config
{
    bk_jpeg_decode_callback_t decode_cbs;  /*!< JPEG解码回调函数 */
    uint8_t *sram_buffer;                  /*!< SRAM缓冲区，用于优化解码（NULL表示自动分配）
                                                缓冲区大小应为：image_max_width * lines_per_block * 2 (YUYV格式每像素2字节)
                                                如使用乒乓模式：image_max_width * lines_per_block * 2 * 2 */
    uint32_t image_max_width;              /*!< 图像最大宽度 */
    uint8_t is_pingpong;                   /*!< 是否使用乒乓模式 */
    bk_jpeg_decode_opt_lines_per_block_t lines_per_block;               /*!< 每个块解码的行数 */
    bk_jpeg_decode_opt_copy_method_t copy_method;  /*!< 数据传输的复制方法 */
} bk_jpeg_decode_hw_opt_config_t;
```

2.2. **bk\_jpeg\_decode\_opt\_copy\_method\_t**

SRAM到PSRAM传输的复制方法枚举。

```
typedef enum
{
    JPEG_DECODE_OPT_COPY_METHOD_MEMCPY = 0,  /*!< 使用os_memcpy进行数据传输 */
    JPEG_DECODE_OPT_COPY_METHOD_DMA,         /*!< 使用DMA进行数据传输（更快） */
} bk_jpeg_decode_opt_copy_method_t;
```

2.3. **bk\_jpeg\_decode\_opt\_lines\_per\_block\_t**

每个块解码的行数枚举。

```
typedef enum
{
    JPEG_DECODE_OPT_LINES_PER_BLOCK_8 = 8,   /*!< 每个块解码8行 */
    JPEG_DECODE_OPT_LINES_PER_BLOCK_16 = 16,  /*!< 每个块解码16行 */
} bk_jpeg_decode_opt_lines_per_block_t;
```

3. **bk\_jpeg\_decode\_hw\_ioctl\_cmd\_t**

硬件JPEG解码器扩展命令枚举。

```
typedef enum
{
    JPEG_DECODE_HW_IOCTL_CMD_BASE = 0,                  /*!< 硬件解码器的基础命令起始值 */
} bk_jpeg_decode_hw_ioctl_cmd_t;
```

4. **jpeg\_decode\_status\_t**

JPEG解码器状态枚举。

```
typedef enum
{
    JPEG_DECODE_DISABLED = 0,  /*!< 解码器已禁用，无法执行解码操作 */
    JPEG_DECODE_ENABLED        /*!< 解码器已启用，准备执行解码操作 */
} jpeg_decode_status_t;
```

5. **jpeg\_img\_fmt\_t**

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

6. **bk\_jpeg\_decode\_img\_info\_t**

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

7. **bk\_jpeg\_decode\_callback\_t**

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
