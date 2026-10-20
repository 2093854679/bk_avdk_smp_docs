---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_camera.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="camera"></a>

# Camera

<a id="id1"></a>

## 概述

Camera模块提供统一的摄像头控制器管理接口，支持多种摄像头设备的操作和控制。

- 有关CAMERA的使用详细信息，请参阅：

  - [DVP CAMERA使用指南](../../developer-guide/camera/dvp.md)
  - [UVC CAMERA使用指南](../../developer-guide/camera/uvc.md)
- 有关CAMERA使用的示例工程，请参阅：

  - [DVP CAMERA使用示例工程](../../examples/projects/dvp_example.md)
  - [UVC CAMERA使用示例工程](../../examples/projects/uvc_example.md)

主要功能特性：

- **设备管理**: 支持摄像头控制器的打开、关闭和删除操作
- **流控制**: 提供暂停和恢复视频流输出的功能
- **IO控制**: 通过统一的ioctl接口支持多种控制命令
- **错误处理**: 完善的参数校验和错误码返回机制

核心API函数：

- `bk_camera_uvc_ctlr_new()` \- 创建UVC摄像头控制器
- `bk_camera_dvp_ctlr_new()` \- 创建DVP摄像头控制器
- `bk_camera_open()` \- 打开摄像头控制器
- `bk_camera_close()` \- 关闭摄像头控制器
- `bk_camera_delete()` \- 删除摄像头控制器
- `bk_camera_suspend()` \- 暂停视频流输出
- `bk_camera_resume()` \- 恢复视频流输出
- `bk_camera_ioctl()` \- 摄像头IO控制

该模块采用统一的控制器句柄接口设计，通过函数指针调用具体的硬件驱动实现，为上层应用提供简洁一致的摄像头操作接口。所有函数均包含完善的参数校验，确保系统稳定性和安全性。

<a id="id4"></a>

## 调用流程

> - bk\_camera\_dvp\_ctlr\_new 或 bk\_camera\_uvc\_ctlr\_new : 创建相机控制器
> - bk\_camera\_open ： 打开相机
> - bk\_camera\_ioctl： 通过进行特定控制（DVP特有）
> - bk\_camera\_close ： 关闭相机
> - bk\_camera\_delete ： 删除控制器

注意事项：
:   1. DVP和UVC控制器创建后都需要通过通用接口进行操作
    2. DVP的IO控制命令丰富，UVC目前IO控制功能有限
    3. UVC不包含电源控制，需要用户自己控制，具体参考用例

<a id="id5"></a>

## 摄像头控制器接口

> 接口说明：

1. **bk\_camera\_uvc\_ctlr\_new**

```
/**
* @brief 创建一个新的UVC摄像头控制器
*
* 此函数用于创建并初始化一个新的UVC摄像头控制器。
*
* @param handle 用于存储创建的控制器句柄的指针
* @param config 指向UVC控制器配置的指针
* @return AVDK错误码
*/
avdk_err_t bk_camera_uvc_ctlr_new(bk_camera_ctlr_handle_t *handle, bk_uvc_ctlr_config_t *config);
```

2. **bk\_camera\_dvp\_ctlr\_new**

```
/**
* @brief 创建一个新的DVP摄像头控制器
*
* 此函数用于创建并初始化一个新的DVP摄像头控制器。
*
* @param handle 用于存储创建的控制器句柄的指针
* @param config 指向DVP控制器配置的指针
* @return AVDK错误码
*/
avdk_err_t bk_camera_dvp_ctlr_new(bk_camera_ctlr_handle_t *handle, bk_dvp_ctlr_config_t *config);
```

3. **bk\_camera\_open**

```
/**
* @brief 打开摄像头控制器
*
* 此函数用于打开与给定控制器句柄关联的摄像头。
*
* @param handle 摄像头控制器句柄
* @return AVDK错误码
*/
avdk_err_t bk_camera_open(bk_camera_ctlr_handle_t handle);
```

4. **bk\_camera\_close**

```
/**
* @brief 关闭摄像头控制器
*
* 此函数用于关闭与给定控制器句柄关联的摄像头。
*
* @param handle 摄像头控制器句柄
* @return AVDK错误码
*/
avdk_err_t bk_camera_close(bk_camera_ctlr_handle_t handle);
```

5. **bk\_camera\_suspend**

```
/**
* @brief 挂起摄像头控制器
*
* 此函数用于挂起与给定控制器句柄关联的摄像头。
*
* @param handle 摄像头控制器句柄
* @return AVDK错误码
*/
avdk_err_t bk_camera_suspend(bk_camera_ctlr_handle_t handle);
```

6. **bk\_camera\_resume**

```
/**
* @brief 恢复摄像头控制器
*
* 此函数用于恢复与给定控制器句柄关联的摄像头。
*
* @param handle 摄像头控制器句柄
* @return AVDK错误码
*/
avdk_err_t bk_camera_resume(bk_camera_ctlr_handle_t handle);
```

7. **bk\_camera\_ioctl**

```
/**
* @brief 在摄像头控制器上执行IOCTL操作
*
* 此函数用于在摄像头上执行设备特定的IOCTL操作。
*
* @param handle 摄像头控制器句柄
* @param cmd 要执行的命令
* @param arg 命令的参数
* @return AVDK错误码
*/
avdk_err_t bk_camera_ioctl(bk_camera_ctlr_handle_t handle, uint32_t cmd, void *arg);

/**
* @brief 删除摄像头控制器
*
* 此函数用于删除并清理给定的摄像头控制器。
*
* @param handle 摄像头控制器句柄
* @return AVDK错误码
*/
avdk_err_t bk_camera_delete(bk_camera_ctlr_handle_t handle);
```

<a id="id6"></a>

## 摄像头控制器数据结构

> 下面是摄像头控制器的数据结构：

1. **bk\_dvp\_ctlr\_config\_t**

```
/**
* @brief DVP相机配置结构体
* @details DVP相机的完整配置参数
*/
typedef struct
{
    bk_dvp_i2c_config_t i2c_config; /**< I2C配置 */
    uint8_t reset_pin;                /**< 复位IO引脚 */
    uint8_t pwdn_pin;                 /**< 断电IO引脚 */
    bk_dvp_io_config_t io_config;   /**< IO配置 */
    mclk_freq_t clk_source;         /**< 传感器核心输入时钟 */
    uint16_t img_format;            /**< 图像格式 */
    uint16_t width;                 /**< 图像宽度 */
    uint16_t height;                /**< 图像高度 */
    uint32_t fps;                   /**< 帧率 */
    void *user_data;                /**< 用户数据指针 */
} bk_dvp_config_t;

/**
* @brief DVP相机回调函数
* @details DVP相机操作的回调函数集合
*/
typedef struct
{
    /**
    * @brief 分配帧缓冲区
    * @param format 图像格式
    * @param size 缓冲区大小
    * @return 指向已分配帧缓冲区的指针
    */
    frame_buffer_t *(*malloc)(image_format_t format, uint32_t size);

    /**
    * @brief 帧完成回调
    * @param format 图像格式
    * @param frame 指向帧缓冲区的指针
    * @param result 操作结果
    */
    void (*complete)(image_format_t format, frame_buffer_t *frame, int result);
} bk_dvp_callback_t;

/**
* @brief DVP摄像头控制器配置结构
*
* 此结构用于存储DVP（数字视频端口）摄像头控制器的配置信息。
*/
typedef struct
{
    bk_dvp_config_t config;      /**< DVP配置参数 */
    const bk_dvp_callback_t *cbs;  /**< DVP回调函数 */
} bk_dvp_ctlr_config_t;
```

2. **bk\_uvc\_ctlr\_config\_t**

```
/**
* @brief UVC相机配置结构体
*
* 包含UVC相机初始化和运行所需的所有配置参数。设置新UVC相机时使用此结构体。
*/
typedef struct
{
    uvc_stream_type_t type;    /**< 流类型（单流或双流） */
    uint8_t port;              /**< 相机端口号（从1开始索引） */
    uint8_t drop_num;          /**< UVC流启动时丢弃的帧数 */
    image_format_t img_format; /**< 图像格式（如MJPEG、YUV、H264） */
    uint16_t width;            /**< 帧宽度（像素） */
    uint16_t height;           /**< 帧高度（像素） */
    uint32_t fps;              /**< 每秒帧数（帧率） */
    void *user_data;           /**< 传递给uvc_event_callback的用户定义参数 */
} bk_cam_uvc_config_t;

/**
* @brief UVC回调函数结构体
*
* 包含各种UVC事件和操作的函数指针。
* 这些回调函数允许应用程序响应UVC事件并管理帧缓冲区的分配和处理。
*/
typedef struct
{
    /**
    * @brief 帧缓冲区分配回调
    *
    * 此函数用于分配帧缓冲区内存。
    *
    * @param format 帧的图像格式（如MJPEG、YUV）
    * @param size 要分配的内存大小（字节）
    * @return 指向分配的帧缓冲区的指针，失败则返回NULL
    */
    frame_buffer_t *(*malloc)(image_format_t format, uint32_t size);

    /**
    * @brief 帧处理完成回调
    *
    * 此函数在帧处理完成时被调用。
    *
    * @param port 相机端口号
    * @param format 处理后帧的图像格式
    * @param frame 包含处理后数据的帧缓冲区指针
    * @param result 帧处理操作的结果
    */
    void (*complete)(uint8_t port, image_format_t format, frame_buffer_t *frame, int result);

    /**
    * @brief UVC事件回调
    *
    * 此函数在UVC状态发生变化时被调用。
    *
    * @param port_info USB集线器端口信息指针
    * @param arg 传递给回调的用户定义参数
    * @param code 指示事件类型的UVC错误代码
    */
    void (*uvc_event_callback)(bk_usb_hub_port_info *port_info, void *arg, uvc_error_code_t code);
} bk_uvc_callback_t;

/**
* @brief UVC摄像头控制器配置结构
*
* 此结构用于存储UVC（USB视频类）摄像头控制器的配置信息。
*/
typedef struct
{
    bk_cam_uvc_config_t config;  /**< UVC配置参数 */
    const bk_uvc_callback_t *cbs;  /**< UVC回调函数 */
} bk_uvc_ctlr_config_t;
```

3. **bk\_camera\_ctlr\_handle\_t**

```
/**
* @brief 摄像头控制器句柄类型
*
* 这是一个指向摄像头控制器实例的不透明句柄。
*/
typedef struct bk_camera_ctlr *bk_camera_ctlr_handle_t;

/**
* @brief 摄像头控制器结构
*
* 此结构定义了摄像头控制器的接口，提供了各种摄像头操作的函数指针。
*/
typedef struct bk_camera_ctlr bk_camera_ctlr_t;

/**
* @brief 摄像头控制器接口
*
* 此结构包含定义摄像头控制器可用操作的函数指针。
*/
struct bk_camera_ctlr
{
    /**
    * @brief 打开摄像头
    * @param controller 指向摄像头控制器的指针
    * @return AVDK错误码
    */
    avdk_err_t (*open)(bk_camera_ctlr_t *controller);

    /**
    * @brief 关闭摄像头
    * @param controller 指向摄像头控制器的指针
    * @return AVDK错误码
    */
    avdk_err_t (*close)(bk_camera_ctlr_t *controller);

    /**
    * @brief 挂起摄像头
    * @param controller 指向摄像头控制器的指针
    * @return AVDK错误码
    */
    avdk_err_t (*suspend)(bk_camera_ctlr_t *controller);

    /**
    * @brief 恢复摄像头
    * @param controller 指向摄像头控制器的指针
    * @return AVDK错误码
    */
    avdk_err_t (*resume)(bk_camera_ctlr_t *controller);

    /**
    * @brief 删除摄像头控制器
    * @param controller 指向摄像头控制器的指针
    * @return AVDK错误码
    */
    avdk_err_t (*del)(bk_camera_ctlr_t *controller);

    /**
    * @brief 摄像头IOCTL操作
    * @param controller 指向摄像头控制器的指针
    * @param cmd 要执行的命令
    * @param arg 命令的参数
    * @return AVDK错误码
    */
    avdk_err_t (*ioctlr)(bk_camera_ctlr_t *controller, uint32_t cmd, void *arg);
} ;
```

<a id="id7"></a>

## 摄像头相关的数据结构

<a id="header-file"></a>

### Header File

- [uvc\_camera\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/uvc_camera_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv419uvc_separate_info_t"></a>

<a id="_CPPv319uvc_separate_info_t"></a> <a id="_CPPv219uvc_separate_info_t"></a> <a id="uvc_separate_info_t"></a> <a id="structuvc__separate__info__t"></a> struct uvc\_separate\_info\_t
:   UVC Data Separation Information Structure.

    Used to track the valid data after separating H.264/JPEG from raw data stream. This structure holds information about the location and length of valid data within a UVC data packet.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19uvc_separate_info_t8data_lenE"></a>

    <a id="_CPPv3N19uvc_separate_info_t8data_lenE"></a> <a id="_CPPv2N19uvc_separate_info_t8data_lenE"></a> <a id="uvc_separate_info_t::data_len__uint32_t"></a> <a id="structuvc__separate__info__t_1a7d8999bf51d41d24c6a5a4401bfa3d61"></a> uint32\_t data\_len
    :   Length of the valid data in bytes

    <a id="_CPPv4N19uvc_separate_info_t8data_offE"></a>

    <a id="_CPPv3N19uvc_separate_info_t8data_offE"></a> <a id="_CPPv2N19uvc_separate_info_t8data_offE"></a> <a id="uvc_separate_info_t::data_off__uint8_tP"></a> <a id="structuvc__separate__info__t_1a2c3fdff04b434e24da64b66cc53dbd03"></a> uint8\_t \*data\_off
    :   Pointer to the start of valid data within the packet

<a id="_CPPv417bk_uvc_callback_t"></a>

<a id="_CPPv317bk_uvc_callback_t"></a> <a id="_CPPv217bk_uvc_callback_t"></a> <a id="bk_uvc_callback_t"></a> <a id="structbk__uvc__callback__t"></a> struct bk\_uvc\_callback\_t
:   UVC Callback Functions Structure.

    Contains function pointers for various UVC events and operations. These callbacks allow the application to respond to UVC events and manage frame buffer allocation and processing.

    **Attention**
    :   In the callback functions, no blocking operations or long operations should be performed, otherwise the hardware interrupt will be delayed, leading to abnormal image data.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_uvc_callback_t6mallocE"></a>

    <a id="_CPPv3N17bk_uvc_callback_t6mallocE"></a> <a id="_CPPv2N17bk_uvc_callback_t6mallocE"></a> <a id="structbk__uvc__callback__t_1ace38b634d5e4ec56f8308c9c17330e70"></a> frame\_buffer\_t \*(\*malloc)(image\_format\_t format, uint32\_t size)
    :   Frame buffer allocation callback.

        This function is called to allocate memory for a frame buffer.

        Param format
        :   Image format of the frame (e.g., MJPEG, YUV)

        Param size
        :   Size of memory to allocate in bytes

        Return
        :   Pointer to allocated frame buffer, or NULL on failure

    <a id="_CPPv4N17bk_uvc_callback_t8completeE"></a>

    <a id="_CPPv3N17bk_uvc_callback_t8completeE"></a> <a id="_CPPv2N17bk_uvc_callback_t8completeE"></a> <a id="structbk__uvc__callback__t_1ab99e683afb988613e7907ef2f11fa8f4"></a> void (\*complete)(uint8\_t port, image\_format\_t format, frame\_buffer\_t \*frame, int result)
    :   Frame processing completion callback.

        This function is called when frame processing is complete.

        Param port
        :   Camera port number

        Param format
        :   Image format of the processed frame

        Param frame
        :   Pointer to the frame buffer containing the processed data

        Param result
        :   Result of the frame processing operation

    <a id="_CPPv4N17bk_uvc_callback_t18uvc_event_callbackE"></a>

    <a id="_CPPv3N17bk_uvc_callback_t18uvc_event_callbackE"></a> <a id="_CPPv2N17bk_uvc_callback_t18uvc_event_callbackE"></a> <a id="structbk__uvc__callback__t_1ae233139a121e2b4780ef7c3bdbb84047"></a> void (\*uvc\_event\_callback)([bk\_usb\_hub\_port\_info](../peripheral/bk_usb.md#_CPPv420bk_usb_hub_port_info "bk_usb_hub_port_info") \*port\_info, void \*arg, [uvc\_error\_code\_t](#_CPPv416uvc_error_code_t "uvc_error_code_t") code)
    :   UVC event callback.

        This function is called when UVC state changes occur.

        Param port\_info
        :   Pointer to USB hub port information

        Param arg
        :   User-defined argument passed to the callback

        Param code
        :   UVC error code indicating the type of event

<a id="_CPPv419bk_cam_uvc_config_t"></a>

<a id="_CPPv319bk_cam_uvc_config_t"></a> <a id="_CPPv219bk_cam_uvc_config_t"></a> <a id="bk_cam_uvc_config_t"></a> <a id="structbk__cam__uvc__config__t"></a> struct bk\_cam\_uvc\_config\_t
:   UVC Camera Configuration Structure.

    Contains all configuration parameters needed for UVC camera initialization and operation. This structure is used when setting up a new UVC camera.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_cam_uvc_config_t4typeE"></a>

    <a id="_CPPv3N19bk_cam_uvc_config_t4typeE"></a> <a id="_CPPv2N19bk_cam_uvc_config_t4typeE"></a> <a id="bk_cam_uvc_config_t::type__uvc_stream_type_t"></a> <a id="structbk__cam__uvc__config__t_1abdf928bdf1eac3806b759dd17ac62295"></a> [uvc\_stream\_type\_t](#_CPPv417uvc_stream_type_t "uvc_stream_type_t") type
    :   Stream type (single or double stream)

    <a id="_CPPv4N19bk_cam_uvc_config_t4portE"></a>

    <a id="_CPPv3N19bk_cam_uvc_config_t4portE"></a> <a id="_CPPv2N19bk_cam_uvc_config_t4portE"></a> <a id="bk_cam_uvc_config_t::port__uint8_t"></a> <a id="structbk__cam__uvc__config__t_1a8236a1318d7f483121685ad23ff67f7e"></a> uint8\_t port
    :   Camera port number (1-based indexing)

    <a id="_CPPv4N19bk_cam_uvc_config_t8drop_numE"></a>

    <a id="_CPPv3N19bk_cam_uvc_config_t8drop_numE"></a> <a id="_CPPv2N19bk_cam_uvc_config_t8drop_numE"></a> <a id="bk_cam_uvc_config_t::drop_num__uint8_t"></a> <a id="structbk__cam__uvc__config__t_1ad98a33aede4dec5510f3746bdb8b9522"></a> uint8\_t drop\_num
    :   Number of frames to drop when UVC stream starts

    <a id="_CPPv4N19bk_cam_uvc_config_t10img_formatE"></a>

    <a id="_CPPv3N19bk_cam_uvc_config_t10img_formatE"></a> <a id="_CPPv2N19bk_cam_uvc_config_t10img_formatE"></a> <a id="bk_cam_uvc_config_t::img_format__image_format_t"></a> <a id="structbk__cam__uvc__config__t_1a4ca494e62d1dd630c80c732f55ef26e6"></a> image\_format\_t img\_format
    :   Image format (e.g., MJPEG, YUV, H264)

    <a id="_CPPv4N19bk_cam_uvc_config_t5widthE"></a>

    <a id="_CPPv3N19bk_cam_uvc_config_t5widthE"></a> <a id="_CPPv2N19bk_cam_uvc_config_t5widthE"></a> <a id="bk_cam_uvc_config_t::width__uint16_t"></a> <a id="structbk__cam__uvc__config__t_1ae9f5fa39057c6bb337f7f8f8f62313e0"></a> uint16\_t width
    :   Frame width in pixels

    <a id="_CPPv4N19bk_cam_uvc_config_t6heightE"></a>

    <a id="_CPPv3N19bk_cam_uvc_config_t6heightE"></a> <a id="_CPPv2N19bk_cam_uvc_config_t6heightE"></a> <a id="bk_cam_uvc_config_t::height__uint16_t"></a> <a id="structbk__cam__uvc__config__t_1a1d90c8ee8b0a798aeaf633d14973b027"></a> uint16\_t height
    :   Frame height in pixels

    <a id="_CPPv4N19bk_cam_uvc_config_t3fpsE"></a>

    <a id="_CPPv3N19bk_cam_uvc_config_t3fpsE"></a> <a id="_CPPv2N19bk_cam_uvc_config_t3fpsE"></a> <a id="bk_cam_uvc_config_t::fps__uint32_t"></a> <a id="structbk__cam__uvc__config__t_1af94256413270c353310f5fa951866560"></a> uint32\_t fps
    :   Frames per second (frame rate)

    <a id="_CPPv4N19bk_cam_uvc_config_t9user_dataE"></a>

    <a id="_CPPv3N19bk_cam_uvc_config_t9user_dataE"></a> <a id="_CPPv2N19bk_cam_uvc_config_t9user_dataE"></a> <a id="bk_cam_uvc_config_t::user_data__voidP"></a> <a id="structbk__cam__uvc__config__t_1a9d986507b68136dfaa0db1146e01f90f"></a> void \*user\_data
    :   User-defined argument to pass to uvc\_event\_callback

<a id="_CPPv421uvc_separate_config_t"></a>

<a id="_CPPv321uvc_separate_config_t"></a> <a id="_CPPv221uvc_separate_config_t"></a> <a id="uvc_separate_config_t"></a> <a id="structuvc__separate__config__t"></a> struct uvc\_separate\_config\_t
:   UVC Packet Separation Configuration Structure.

    Contains configuration for handling UVC packet separation and processing. This structure defines callbacks for packet processing operations.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21uvc_separate_config_t2idE"></a>

    <a id="_CPPv3N21uvc_separate_config_t2idE"></a> <a id="_CPPv2N21uvc_separate_config_t2idE"></a> <a id="uvc_separate_config_t::id__uint8_t"></a> <a id="structuvc__separate__config__t_1aaec91165c7ea2218fab6d5dd75a07b5e"></a> uint8\_t id
    :   Camera port ID

    <a id="_CPPv4N21uvc_separate_config_t22uvc_separate_packet_cbE"></a>

    <a id="_CPPv3N21uvc_separate_config_t22uvc_separate_packet_cbE"></a> <a id="_CPPv2N21uvc_separate_config_t22uvc_separate_packet_cbE"></a> <a id="structuvc__separate__config__t_1a876bd6d9e09c28ce27ab7d51102bcf8b"></a> void (\*uvc\_separate\_packet\_cb)(uint8\_t \*data, uint32\_t length, [uvc\_separate\_info\_t](#_CPPv419uvc_separate_info_t "uvc_separate_info_t") \*sepatate\_info)
    :   UVC packet separation callback.

        This function is called to separate UVC packets from the raw data stream.

        Param data
        :   Pointer to the raw data

        Param length
        :   Length of the raw data in bytes

        Param sepatate\_info
        :   Pointer to structure that will receive separation results

    <a id="_CPPv4N21uvc_separate_config_t18uvc_init_packet_cbE"></a>

    <a id="_CPPv3N21uvc_separate_config_t18uvc_init_packet_cbE"></a> <a id="_CPPv2N21uvc_separate_config_t18uvc_init_packet_cbE"></a> <a id="structuvc__separate__config__t_1a4e513b75b6524e13d0a97721eaf6195f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*uvc\_init\_packet\_cb)([bk\_cam\_uvc\_config\_t](#_CPPv419bk_cam_uvc_config_t "bk_cam_uvc_config_t") \*device, uint8\_t init, const [bk\_uvc\_callback\_t](#_CPPv417bk_uvc_callback_t "bk_uvc_callback_t") \*cb)
    :   UVC packet initialization callback.

        This function is called to initialize UVC packet processing.

        Param device
        :   Pointer to UVC camera configuration

        Param init
        :   Initialization flag (1 for init, 0 for deinit)

        Param cb
        :   Pointer to UVC callback functions

        Return
        :   BK\_ERR\_NONE on success, error code on failure

    <a id="_CPPv4N21uvc_separate_config_t17uvc_eof_packet_cbE"></a>

    <a id="_CPPv3N21uvc_separate_config_t17uvc_eof_packet_cbE"></a> <a id="_CPPv2N21uvc_separate_config_t17uvc_eof_packet_cbE"></a> <a id="structuvc__separate__config__t_1a6941fb589a9521b17bf5327b81cf0596"></a> void (\*uvc\_eof\_packet\_cb)([bk\_cam\_uvc\_config\_t](#_CPPv419bk_cam_uvc_config_t "bk_cam_uvc_config_t") \*device)
    :   UVC end-of-frame packet callback.

        This function is called when an end-of-frame packet is received.

        Param device
        :   Pointer to UVC camera configuration

<a id="macros"></a>

### Macros

<a id="c.UVC_PORT_MAX"></a>

<a id="uvc__camera__types_8h_1a78750ec6a8cd9598fa8c901a778e5145"></a> UVC\_PORT\_MAX
:   Maximum number of UVC ports.

    This macro defines the maximum number of UVC ports supported, based on the USB host hub maximum external ports configuration.

<a id="c.BK_UVC_864X480_30FPS_MJPEG_CONFIG"></a>

<a id="uvc__camera__types_8h_1a9ae4d6c58e41381d1097b4410696c47a"></a> BK\_UVC\_864X480\_30FPS\_MJPEG\_CONFIG()
:   Default UVC Configuration for 864x480 Resolution at 30 FPS with MJPEG Format.

    Provides a standard configuration for UVC camera initialization with:

    - Resolution: 864x480 pixels
    - Frame rate: 30 FPS
    - Image format: MJPEG
    - Single stream mode
    - Port 1
    - No frame dropping
    - No user argument

<a id="c.BK_UVC_1920X1080_30FPS_H26X_CONFIG"></a>

<a id="uvc__camera__types_8h_1a67a30c10158ee9d0eb9d751dc17a7bc2"></a> BK\_UVC\_1920X1080\_30FPS\_H26X\_CONFIG()

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv416uvc_error_code_t"></a>

<a id="_CPPv316uvc_error_code_t"></a> <a id="_CPPv216uvc_error_code_t"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8"></a> enum uvc\_error\_code\_t
:   UVC Error Codes.

    Defines the different types of UVC error codes that can occur during device operation.

    *Values:*

    <a id="_CPPv4N16uvc_error_code_t14BK_UVC_CONNECTE"></a>

    <a id="_CPPv3N16uvc_error_code_t14BK_UVC_CONNECTE"></a> <a id="_CPPv2N16uvc_error_code_t14BK_UVC_CONNECTE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8a42aefc160e711cfac6d48ad83e88553e"></a> enumerator BK\_UVC\_CONNECT
    :   UVC device connected successfully

    <a id="_CPPv4N16uvc_error_code_t19BK_UVC_CONFIG_ERRORE"></a>

    <a id="_CPPv3N16uvc_error_code_t19BK_UVC_CONFIG_ERRORE"></a> <a id="_CPPv2N16uvc_error_code_t19BK_UVC_CONFIG_ERRORE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8ad2fa548cc0ce85b30db15069fdd360ec"></a> enumerator BK\_UVC\_CONFIG\_ERROR
    :   UVC configuration error occurred

    <a id="_CPPv4N16uvc_error_code_t16BK_UVC_NO_MEMORYE"></a>

    <a id="_CPPv3N16uvc_error_code_t16BK_UVC_NO_MEMORYE"></a> <a id="_CPPv2N16uvc_error_code_t16BK_UVC_NO_MEMORYE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8af8c129af9c848cd3ec687ff5f27e05e0"></a> enumerator BK\_UVC\_NO\_MEMORY
    :   Insufficient memory for UVC operations

    <a id="_CPPv4N16uvc_error_code_t18BK_UVC_NO_RESOURCEE"></a>

    <a id="_CPPv3N16uvc_error_code_t18BK_UVC_NO_RESOURCEE"></a> <a id="_CPPv2N16uvc_error_code_t18BK_UVC_NO_RESOURCEE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8ac79bbe006da3ee664d70bd938c80f357"></a> enumerator BK\_UVC\_NO\_RESOURCE
    :   No available resources for UVC

    <a id="_CPPv4N16uvc_error_code_t16BK_UVC_PPI_ERRORE"></a>

    <a id="_CPPv3N16uvc_error_code_t16BK_UVC_PPI_ERRORE"></a> <a id="_CPPv2N16uvc_error_code_t16BK_UVC_PPI_ERRORE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8a31f676acb80efdf6e97da3f4cae59a3b"></a> enumerator BK\_UVC\_PPI\_ERROR
    :   PPI (Parallel Peripheral Interface) error

    <a id="_CPPv4N16uvc_error_code_t17BK_UVC_DISCONNECTE"></a>

    <a id="_CPPv3N16uvc_error_code_t17BK_UVC_DISCONNECTE"></a> <a id="_CPPv2N16uvc_error_code_t17BK_UVC_DISCONNECTE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8a640cc0e67c2da5c79e1d071f477c9beb"></a> enumerator BK\_UVC\_DISCONNECT
    :   UVC device disconnected

    <a id="_CPPv4N16uvc_error_code_t16BK_UVC_NO_RESPONE"></a>

    <a id="_CPPv3N16uvc_error_code_t16BK_UVC_NO_RESPONE"></a> <a id="_CPPv2N16uvc_error_code_t16BK_UVC_NO_RESPONE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8ac04567ab1374a826438b301c2d13117c"></a> enumerator BK\_UVC\_NO\_RESPON
    :   UVC device not responding

    <a id="_CPPv4N16uvc_error_code_t16BK_UVC_DMA_ERRORE"></a>

    <a id="_CPPv3N16uvc_error_code_t16BK_UVC_DMA_ERRORE"></a> <a id="_CPPv2N16uvc_error_code_t16BK_UVC_DMA_ERRORE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8a06bc360658e2874c9467d707107b11de"></a> enumerator BK\_UVC\_DMA\_ERROR
    :   DMA (Direct Memory Access) error

    <a id="_CPPv4N16uvc_error_code_t17BK_UVC_NOT_PERMITE"></a>

    <a id="_CPPv3N16uvc_error_code_t17BK_UVC_NOT_PERMITE"></a> <a id="_CPPv2N16uvc_error_code_t17BK_UVC_NOT_PERMITE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8aa9aadf31c3fdc82a4998d4dee47b7dfe"></a> enumerator BK\_UVC\_NOT\_PERMIT
    :   Operation not permitted

    <a id="_CPPv4N16uvc_error_code_t18BK_UVC_POWER_ERRORE"></a>

    <a id="_CPPv3N16uvc_error_code_t18BK_UVC_POWER_ERRORE"></a> <a id="_CPPv2N16uvc_error_code_t18BK_UVC_POWER_ERRORE"></a> <a id="uvc__camera__types_8h_1abc3b91a89bf053206b9705cfcf41e0a8afb9d4dee4b517dd8b5cccad28b4434a3"></a> enumerator BK\_UVC\_POWER\_ERROR
    :   Power supply error

<a id="_CPPv418uvc_stream_state_t"></a>

<a id="_CPPv318uvc_stream_state_t"></a> <a id="_CPPv218uvc_stream_state_t"></a> <a id="uvc__camera__types_8h_1af6ddee731d325dfa3a6a4419b0d9e88f"></a> enum uvc\_stream\_state\_t
:   UVC Stream States.

    Represents the different operational states of a UVC data stream.

    *Values:*

    <a id="_CPPv4N18uvc_stream_state_t24UVC_STREAM_STATE_RUNNINGE"></a>

    <a id="_CPPv3N18uvc_stream_state_t24UVC_STREAM_STATE_RUNNINGE"></a> <a id="_CPPv2N18uvc_stream_state_t24UVC_STREAM_STATE_RUNNINGE"></a> <a id="uvc__camera__types_8h_1af6ddee731d325dfa3a6a4419b0d9e88fa54f703bff668a899a5660e44159669f0"></a> enumerator UVC\_STREAM\_STATE\_RUNNING
    :   Stream is running normally

    <a id="_CPPv4N18uvc_stream_state_t23UVC_STREAM_STATE_RESUMEE"></a>

    <a id="_CPPv3N18uvc_stream_state_t23UVC_STREAM_STATE_RESUMEE"></a> <a id="_CPPv2N18uvc_stream_state_t23UVC_STREAM_STATE_RESUMEE"></a> <a id="uvc__camera__types_8h_1af6ddee731d325dfa3a6a4419b0d9e88fa2c068b13a8774655d226efe11ca92d7a"></a> enumerator UVC\_STREAM\_STATE\_RESUME
    :   Stream is resumed from a suspended state

    <a id="_CPPv4N18uvc_stream_state_t24UVC_STREAM_STATE_SUSPENDE"></a>

    <a id="_CPPv3N18uvc_stream_state_t24UVC_STREAM_STATE_SUSPENDE"></a> <a id="_CPPv2N18uvc_stream_state_t24UVC_STREAM_STATE_SUSPENDE"></a> <a id="uvc__camera__types_8h_1af6ddee731d325dfa3a6a4419b0d9e88faade6daf4be322271c61730c15b907ead"></a> enumerator UVC\_STREAM\_STATE\_SUSPEND
    :   Stream is temporarily suspended

<a id="_CPPv417uvc_stream_type_t"></a>

<a id="_CPPv317uvc_stream_type_t"></a> <a id="_CPPv217uvc_stream_type_t"></a> <a id="uvc__camera__types_8h_1a0689293210e13efa1792227a8f6e3cf9"></a> enum uvc\_stream\_type\_t
:   UVC Stream Types.

    Defines the streaming modes for UVC data transmission.

    *Values:*

    <a id="_CPPv4N17uvc_stream_type_t17UVC_SINGLE_STREAME"></a>

    <a id="_CPPv3N17uvc_stream_type_t17UVC_SINGLE_STREAME"></a> <a id="_CPPv2N17uvc_stream_type_t17UVC_SINGLE_STREAME"></a> <a id="uvc__camera__types_8h_1a0689293210e13efa1792227a8f6e3cf9af91055f03dc4fbadeed49d073d1e4d51"></a> enumerator UVC\_SINGLE\_STREAM
    :   Single stream mode \- one data stream

    <a id="_CPPv4N17uvc_stream_type_t17UVC_DOUBLE_STREAME"></a>

    <a id="_CPPv3N17uvc_stream_type_t17UVC_DOUBLE_STREAME"></a> <a id="_CPPv2N17uvc_stream_type_t17UVC_DOUBLE_STREAME"></a> <a id="uvc__camera__types_8h_1a0689293210e13efa1792227a8f6e3cf9a42dd4c8acfe91feb7ac8381287fc2205"></a> enumerator UVC\_DOUBLE\_STREAM
    :   Double stream mode \- two simultaneous data streams

<a id="id8"></a>

### Header File

- [dvp\_camera\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/dvp_camera_types.h)

<a id="id9"></a>

### Structures

<a id="_CPPv418bk_dvp_io_config_t"></a>

<a id="_CPPv318bk_dvp_io_config_t"></a> <a id="_CPPv218bk_dvp_io_config_t"></a> <a id="bk_dvp_io_config_t"></a> <a id="structbk__dvp__io__config__t"></a> struct bk\_dvp\_io\_config\_t
:   DVP IO configuration structure.

    Configuration parameters for DVP interface IO pins

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_dvp_io_config_t10data_widthE"></a>

    <a id="_CPPv3N18bk_dvp_io_config_t10data_widthE"></a> <a id="_CPPv2N18bk_dvp_io_config_t10data_widthE"></a> <a id="bk_dvp_io_config_t::data_width__sensor_bits_width_t"></a> <a id="structbk__dvp__io__config__t_1a7012a6fd2fb741819656489ee3e3a332"></a> [sensor\_bits\_width\_t](#_CPPv419sensor_bits_width_t "sensor_bits_width_t") data\_width
    :   Data bus width

    <a id="_CPPv4N18bk_dvp_io_config_t8data_pinE"></a>

    <a id="_CPPv3N18bk_dvp_io_config_t8data_pinE"></a> <a id="_CPPv2N18bk_dvp_io_config_t8data_pinE"></a> <a id="bk_dvp_io_config_t::data_pin__uint8_tA"></a> <a id="structbk__dvp__io__config__t_1aeb33941049069eca925c08d9f0a41944"></a> uint8\_t data\_pin\[16\]
    :   Data IO pins (up to 16 pins)

    <a id="_CPPv4N18bk_dvp_io_config_t9vsync_pinE"></a>

    <a id="_CPPv3N18bk_dvp_io_config_t9vsync_pinE"></a> <a id="_CPPv2N18bk_dvp_io_config_t9vsync_pinE"></a> <a id="bk_dvp_io_config_t::vsync_pin__uint8_t"></a> <a id="structbk__dvp__io__config__t_1a7c0f2eae8ec267b2d154ad22caa8bdfc"></a> uint8\_t vsync\_pin
    :   Vertical sync IO pin

    <a id="_CPPv4N18bk_dvp_io_config_t9hsync_pinE"></a>

    <a id="_CPPv3N18bk_dvp_io_config_t9hsync_pinE"></a> <a id="_CPPv2N18bk_dvp_io_config_t9hsync_pinE"></a> <a id="bk_dvp_io_config_t::hsync_pin__uint8_t"></a> <a id="structbk__dvp__io__config__t_1aa9ffa5f5366d9ee9bb068a9843e2280d"></a> uint8\_t hsync\_pin
    :   Horizontal sync IO pin

    <a id="_CPPv4N18bk_dvp_io_config_t8xclk_pinE"></a>

    <a id="_CPPv3N18bk_dvp_io_config_t8xclk_pinE"></a> <a id="_CPPv2N18bk_dvp_io_config_t8xclk_pinE"></a> <a id="bk_dvp_io_config_t::xclk_pin__uint8_t"></a> <a id="structbk__dvp__io__config__t_1a755e51cc30145246b054a4ddec5100f4"></a> uint8\_t xclk\_pin
    :   Core input clock to sensor

    <a id="_CPPv4N18bk_dvp_io_config_t8pclk_pinE"></a>

    <a id="_CPPv3N18bk_dvp_io_config_t8pclk_pinE"></a> <a id="_CPPv2N18bk_dvp_io_config_t8pclk_pinE"></a> <a id="bk_dvp_io_config_t::pclk_pin__uint8_t"></a> <a id="structbk__dvp__io__config__t_1ac9352301f91cd76a7e5eb9a9e3bfa3c8"></a> uint8\_t pclk\_pin
    :   Sensor output clock to core

<a id="_CPPv419bk_dvp_i2c_config_t"></a>

<a id="_CPPv319bk_dvp_i2c_config_t"></a> <a id="_CPPv219bk_dvp_i2c_config_t"></a> <a id="bk_dvp_i2c_config_t"></a> <a id="structbk__dvp__i2c__config__t"></a> struct bk\_dvp\_i2c\_config\_t
:   DVP I2C configuration structure.

    Configuration parameters for I2C interface used by DVP sensor

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_dvp_i2c_config_t2idE"></a>

    <a id="_CPPv3N19bk_dvp_i2c_config_t2idE"></a> <a id="_CPPv2N19bk_dvp_i2c_config_t2idE"></a> <a id="bk_dvp_i2c_config_t::id__uint8_t"></a> <a id="structbk__dvp__i2c__config__t_1a6527558bcf74be11adb6b8f9a35e511c"></a> uint8\_t id
    :   I2C bus ID

    <a id="_CPPv4N19bk_dvp_i2c_config_t7scl_pinE"></a>

    <a id="_CPPv3N19bk_dvp_i2c_config_t7scl_pinE"></a> <a id="_CPPv2N19bk_dvp_i2c_config_t7scl_pinE"></a> <a id="bk_dvp_i2c_config_t::scl_pin__uint8_t"></a> <a id="structbk__dvp__i2c__config__t_1a444cc90bdb55b8195520bcf40fddde3c"></a> uint8\_t scl\_pin
    :   I2C clock line IO pin

    <a id="_CPPv4N19bk_dvp_i2c_config_t7sda_pinE"></a>

    <a id="_CPPv3N19bk_dvp_i2c_config_t7sda_pinE"></a> <a id="_CPPv2N19bk_dvp_i2c_config_t7sda_pinE"></a> <a id="bk_dvp_i2c_config_t::sda_pin__uint8_t"></a> <a id="structbk__dvp__i2c__config__t_1a795eef330d99bf30c1cc4706d5edf404"></a> uint8\_t sda\_pin
    :   I2C data line IO pin

    <a id="_CPPv4N19bk_dvp_i2c_config_t9baud_rateE"></a>

    <a id="_CPPv3N19bk_dvp_i2c_config_t9baud_rateE"></a> <a id="_CPPv2N19bk_dvp_i2c_config_t9baud_rateE"></a> <a id="bk_dvp_i2c_config_t::baud_rate__uint32_t"></a> <a id="structbk__dvp__i2c__config__t_1a135d215fd8672d1842c540b10689c88c"></a> uint32\_t baud\_rate
    :   I2C bus baud rate

    <a id="_CPPv4N19bk_dvp_i2c_config_t5flagsE"></a>

    <a id="_CPPv3N19bk_dvp_i2c_config_t5flagsE"></a> <a id="_CPPv2N19bk_dvp_i2c_config_t5flagsE"></a> <a id="bk_dvp_i2c_config_t::flags__uint32_t"></a> <a id="structbk__dvp__i2c__config__t_1a23ad49efec979e935199f62151c4ef12"></a> uint32\_t flags
    :   I2C configuration flags

<a id="_CPPv415bk_dvp_config_t"></a>

<a id="_CPPv315bk_dvp_config_t"></a> <a id="_CPPv215bk_dvp_config_t"></a> <a id="bk_dvp_config_t"></a> <a id="structbk__dvp__config__t"></a> struct bk\_dvp\_config\_t
:   DVP camera configuration structure.

    Complete configuration parameters for DVP camera

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15bk_dvp_config_t10i2c_configE"></a>

    <a id="_CPPv3N15bk_dvp_config_t10i2c_configE"></a> <a id="_CPPv2N15bk_dvp_config_t10i2c_configE"></a> <a id="bk_dvp_config_t::i2c_config__bk_dvp_i2c_config_t"></a> <a id="structbk__dvp__config__t_1ac93591b757a7bb6c3974064fab695722"></a> [bk\_dvp\_i2c\_config\_t](#_CPPv419bk_dvp_i2c_config_t "bk_dvp_i2c_config_t") i2c\_config
    :   I2C configuration

    <a id="_CPPv4N15bk_dvp_config_t9reset_pinE"></a>

    <a id="_CPPv3N15bk_dvp_config_t9reset_pinE"></a> <a id="_CPPv2N15bk_dvp_config_t9reset_pinE"></a> <a id="bk_dvp_config_t::reset_pin__uint8_t"></a> <a id="structbk__dvp__config__t_1ab84d4a26062d47a0135e328a13bd0c90"></a> uint8\_t reset\_pin
    :   Reset IO pin

    <a id="_CPPv4N15bk_dvp_config_t8pwdn_pinE"></a>

    <a id="_CPPv3N15bk_dvp_config_t8pwdn_pinE"></a> <a id="_CPPv2N15bk_dvp_config_t8pwdn_pinE"></a> <a id="bk_dvp_config_t::pwdn_pin__uint8_t"></a> <a id="structbk__dvp__config__t_1a35cc742799f837e7af3a5c1e156b4764"></a> uint8\_t pwdn\_pin
    :   Power down IO pin

    <a id="_CPPv4N15bk_dvp_config_t9io_configE"></a>

    <a id="_CPPv3N15bk_dvp_config_t9io_configE"></a> <a id="_CPPv2N15bk_dvp_config_t9io_configE"></a> <a id="bk_dvp_config_t::io_config__bk_dvp_io_config_t"></a> <a id="structbk__dvp__config__t_1a88c344b8a35b7bc61dcbece2d4b385bc"></a> [bk\_dvp\_io\_config\_t](#_CPPv418bk_dvp_io_config_t "bk_dvp_io_config_t") io\_config
    :   IO configuration

    <a id="_CPPv4N15bk_dvp_config_t10clk_sourceE"></a>

    <a id="_CPPv3N15bk_dvp_config_t10clk_sourceE"></a> <a id="_CPPv2N15bk_dvp_config_t10clk_sourceE"></a> <a id="bk_dvp_config_t::clk_source__mclk_freq_t"></a> <a id="structbk__dvp__config__t_1a79657c68d8c6b872b846d10ce92040b1"></a> mclk\_freq\_t clk\_source
    :   Core input clock to sensor

    <a id="_CPPv4N15bk_dvp_config_t10img_formatE"></a>

    <a id="_CPPv3N15bk_dvp_config_t10img_formatE"></a> <a id="_CPPv2N15bk_dvp_config_t10img_formatE"></a> <a id="bk_dvp_config_t::img_format__uint16_t"></a> <a id="structbk__dvp__config__t_1abe90068e2fcad4a799507c2cfd7d04e8"></a> uint16\_t img\_format
    :   Image format

    <a id="_CPPv4N15bk_dvp_config_t5widthE"></a>

    <a id="_CPPv3N15bk_dvp_config_t5widthE"></a> <a id="_CPPv2N15bk_dvp_config_t5widthE"></a> <a id="bk_dvp_config_t::width__uint16_t"></a> <a id="structbk__dvp__config__t_1a30e0edb24350f6350d3cace2d2a3114e"></a> uint16\_t width
    :   Image width

    <a id="_CPPv4N15bk_dvp_config_t6heightE"></a>

    <a id="_CPPv3N15bk_dvp_config_t6heightE"></a> <a id="_CPPv2N15bk_dvp_config_t6heightE"></a> <a id="bk_dvp_config_t::height__uint16_t"></a> <a id="structbk__dvp__config__t_1a2004316330740bdb9fa3bf7864ca4b76"></a> uint16\_t height
    :   Image height

    <a id="_CPPv4N15bk_dvp_config_t3fpsE"></a>

    <a id="_CPPv3N15bk_dvp_config_t3fpsE"></a> <a id="_CPPv2N15bk_dvp_config_t3fpsE"></a> <a id="bk_dvp_config_t::fps__uint32_t"></a> <a id="structbk__dvp__config__t_1aba642a11b9d17385817a206eba5d3928"></a> uint32\_t fps
    :   Frames per second

    <a id="_CPPv4N15bk_dvp_config_t9user_dataE"></a>

    <a id="_CPPv3N15bk_dvp_config_t9user_dataE"></a> <a id="_CPPv2N15bk_dvp_config_t9user_dataE"></a> <a id="bk_dvp_config_t::user_data__voidP"></a> <a id="structbk__dvp__config__t_1a164d59cd748395660dcc818a2e602204"></a> void \*user\_data
    :   User data pointer

<a id="_CPPv417bk_dvp_callback_t"></a>

<a id="_CPPv317bk_dvp_callback_t"></a> <a id="_CPPv217bk_dvp_callback_t"></a> <a id="bk_dvp_callback_t"></a> <a id="structbk__dvp__callback__t"></a> struct bk\_dvp\_callback\_t
:   DVP camera callback functions.

    Callback functions for DVP camera operations

    **Attention**
    :   In the callback functions, no blocking operations or long operations should be performed, otherwise the hardware interrupt will be delayed, leading to abnormal image data.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_dvp_callback_t6mallocE"></a>

    <a id="_CPPv3N17bk_dvp_callback_t6mallocE"></a> <a id="_CPPv2N17bk_dvp_callback_t6mallocE"></a> <a id="structbk__dvp__callback__t_1a7719ea475527d46a373d11bfb8c86270"></a> frame\_buffer\_t \*(\*malloc)(image\_format\_t format, uint32\_t size)
    :   Allocate frame buffer.

        Param format
        :   Image format

        Param size
        :   Buffer size

        Return
        :   Pointer to allocated frame buffer

    <a id="_CPPv4N17bk_dvp_callback_t8completeE"></a>

    <a id="_CPPv3N17bk_dvp_callback_t8completeE"></a> <a id="_CPPv2N17bk_dvp_callback_t8completeE"></a> <a id="structbk__dvp__callback__t_1a52988ef67fa23c446bdd49697300d94d"></a> void (\*complete)(image\_format\_t format, frame\_buffer\_t \*frame, int result)
    :   Frame completion callback.

        Param format
        :   Image format

        Param frame
        :   Pointer to frame buffer

        Param result
        :   Operation result

<a id="_CPPv420dvp_sensor_reg_val_t"></a>

<a id="_CPPv320dvp_sensor_reg_val_t"></a> <a id="_CPPv220dvp_sensor_reg_val_t"></a> <a id="dvp_sensor_reg_val_t"></a> <a id="structdvp__sensor__reg__val__t"></a> struct dvp\_sensor\_reg\_val\_t
:   DVP sensor register value structure.

    Structure to hold sensor register address and value pairs

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20dvp_sensor_reg_val_t3regE"></a>

    <a id="_CPPv3N20dvp_sensor_reg_val_t3regE"></a> <a id="_CPPv2N20dvp_sensor_reg_val_t3regE"></a> <a id="dvp_sensor_reg_val_t::reg__uint32_t"></a> <a id="structdvp__sensor__reg__val__t_1aa63c7a240aef5401a677006bf717a433"></a> uint32\_t reg
    :   Register address

    <a id="_CPPv4N20dvp_sensor_reg_val_t3valE"></a>

    <a id="_CPPv3N20dvp_sensor_reg_val_t3valE"></a> <a id="_CPPv2N20dvp_sensor_reg_val_t3valE"></a> <a id="dvp_sensor_reg_val_t::val__uint32_t"></a> <a id="structdvp__sensor__reg__val__t_1a2e3de1d5e361594959cdfb6e690071fb"></a> uint32\_t val
    :   Register value

<a id="_CPPv419dvp_sensor_config_t"></a>

<a id="_CPPv319dvp_sensor_config_t"></a> <a id="_CPPv219dvp_sensor_config_t"></a> <a id="dvp_sensor_config_t"></a> <a id="structdvp__sensor__config__t"></a> struct dvp\_sensor\_config\_t
:   DVP sensor configuration structure.

    Configuration parameters and function pointers for DVP sensor

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19dvp_sensor_config_t4nameE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t4nameE"></a> <a id="_CPPv2N19dvp_sensor_config_t4nameE"></a> <a id="dvp_sensor_config_t::name__cP"></a> <a id="structdvp__sensor__config__t_1ab7b2b20c53aa87375e3495562f7ee647"></a> char \*name
    :   Sensor name

    <a id="_CPPv4N19dvp_sensor_config_t7def_ppiE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7def_ppiE"></a> <a id="_CPPv2N19dvp_sensor_config_t7def_ppiE"></a> <a id="dvp_sensor_config_t::def_ppi__media_ppi_t"></a> <a id="structdvp__sensor__config__t_1a54a5669482eb1d3cdaebaf1097736df2"></a> media\_ppi\_t def\_ppi
    :   Sensor default resolution

    <a id="_CPPv4N19dvp_sensor_config_t7def_fpsE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7def_fpsE"></a> <a id="_CPPv2N19dvp_sensor_config_t7def_fpsE"></a> <a id="dvp_sensor_config_t::def_fps__frame_fps_t"></a> <a id="structdvp__sensor__config__t_1a72c34312c76b198a36efa2f3b9eb5f7f"></a> frame\_fps\_t def\_fps
    :   Sensor default FPS

    <a id="_CPPv4N19dvp_sensor_config_t3clkE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t3clkE"></a> <a id="_CPPv2N19dvp_sensor_config_t3clkE"></a> <a id="dvp_sensor_config_t::clk__mclk_freq_t"></a> <a id="structdvp__sensor__config__t_1acc75e0d6e90b402ebb4c2efd2953f7a6"></a> mclk\_freq\_t clk
    :   Sensor working clock for configured FPS and PPI

    <a id="_CPPv4N19dvp_sensor_config_t3fmtE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t3fmtE"></a> <a id="_CPPv2N19dvp_sensor_config_t3fmtE"></a> <a id="dvp_sensor_config_t::fmt__pixel_format_t"></a> <a id="structdvp__sensor__config__t_1a65ff8277a9ec25ac485ff358abd8fe8d"></a> pixel\_format\_t fmt
    :   Sensor input data format

    <a id="_CPPv4N19dvp_sensor_config_t5vsyncE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t5vsyncE"></a> <a id="_CPPv2N19dvp_sensor_config_t5vsyncE"></a> <a id="dvp_sensor_config_t::vsync__sync_level_t"></a> <a id="structdvp__sensor__config__t_1a362a51d84e5c4a755e1744181bdd041c"></a> sync\_level\_t vsync
    :   Sensor VSYNC active level

    <a id="_CPPv4N19dvp_sensor_config_t5hsyncE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t5hsyncE"></a> <a id="_CPPv2N19dvp_sensor_config_t5hsyncE"></a> <a id="dvp_sensor_config_t::hsync__sync_level_t"></a> <a id="structdvp__sensor__config__t_1af62377e7f34b990ea6d6a0a7a35b7358"></a> sync\_level\_t hsync
    :   Sensor HSYNC active level

    <a id="_CPPv4N19dvp_sensor_config_t2idE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t2idE"></a> <a id="_CPPv2N19dvp_sensor_config_t2idE"></a> <a id="dvp_sensor_config_t::id__uint16_t"></a> <a id="structdvp__sensor__config__t_1a54479b78007648b61b3c87e8172e7f49"></a> uint16\_t id
    :   Sensor type (sensor\_id\_t)

    <a id="_CPPv4N19dvp_sensor_config_t7addressE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7addressE"></a> <a id="_CPPv2N19dvp_sensor_config_t7addressE"></a> <a id="dvp_sensor_config_t::address__uint16_t"></a> <a id="structdvp__sensor__config__t_1af605f3525eae060dc9559b75c49a07f6"></a> uint16\_t address
    :   Sensor write register address by I2C

    <a id="_CPPv4N19dvp_sensor_config_t7fps_capE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7fps_capE"></a> <a id="_CPPv2N19dvp_sensor_config_t7fps_capE"></a> <a id="dvp_sensor_config_t::fps_cap__uint16_t"></a> <a id="structdvp__sensor__config__t_1a031ad0f5bdd0cd7af41cf2a5054103a8"></a> uint16\_t fps\_cap
    :   Sensor supported FPS

    <a id="_CPPv4N19dvp_sensor_config_t7ppi_capE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7ppi_capE"></a> <a id="_CPPv2N19dvp_sensor_config_t7ppi_capE"></a> <a id="dvp_sensor_config_t::ppi_cap__uint16_t"></a> <a id="structdvp__sensor__config__t_1a1f3132bf13682e13e1138adb139fdeba"></a> uint16\_t ppi\_cap
    :   Sensor supported resolutions

    <a id="_CPPv4N19dvp_sensor_config_t6detectE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t6detectE"></a> <a id="_CPPv2N19dvp_sensor_config_t6detectE"></a> <a id="structdvp__sensor__config__t_1aebd73324267e31f955404ec1f5afa0f7"></a> bool (\*detect)(void)
    :   Auto-detect used DVP sensor.

        Return
        :   true if sensor detected, false otherwise

    <a id="_CPPv4N19dvp_sensor_config_t4initE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t4initE"></a> <a id="_CPPv2N19dvp_sensor_config_t4initE"></a> <a id="structdvp__sensor__config__t_1ad3ffee59ad42f2f49c95bc5ca266ec3a"></a> int (\*init)(void)
    :   Initialize DVP sensor.

        Return
        :   0 on success, error code on failure

    <a id="_CPPv4N19dvp_sensor_config_t7set_ppiE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7set_ppiE"></a> <a id="_CPPv2N19dvp_sensor_config_t7set_ppiE"></a> <a id="structdvp__sensor__config__t_1a95009b91ad5fec8fd7818b3ba778a201"></a> int (\*set\_ppi)(media\_ppi\_t ppi)
    :   Set resolution of sensor.

        Param ppi
        :   Resolution to set

        Return
        :   0 on success, error code on failure

    <a id="_CPPv4N19dvp_sensor_config_t7set_fpsE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7set_fpsE"></a> <a id="_CPPv2N19dvp_sensor_config_t7set_fpsE"></a> <a id="structdvp__sensor__config__t_1a47812c1d994d7a2952f9c3de71c4f932"></a> int (\*set\_fps)(frame\_fps\_t fps)
    :   Set FPS of sensor.

        Param fps
        :   FPS to set

        Return
        :   0 on success, error code on failure

    <a id="_CPPv4N19dvp_sensor_config_t10power_downE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t10power_downE"></a> <a id="_CPPv2N19dvp_sensor_config_t10power_downE"></a> <a id="structdvp__sensor__config__t_1af8bcb71c496ecda44014603cf429d4c7"></a> int (\*power\_down)(void)
    :   Power down or reset sensor.

        Return
        :   0 on success, error code on failure

    <a id="_CPPv4N19dvp_sensor_config_t13read_registerE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t13read_registerE"></a> <a id="_CPPv2N19dvp_sensor_config_t13read_registerE"></a> <a id="structdvp__sensor__config__t_1abb6a92e4019bfa83fb945d7423a07869"></a> int (\*read\_register)(uint32\_t reg, uint32\_t \*val)
    :   Read sensor register.

        Param reg
        :   Register address

        Param val
        :   Pointer to store register value

        Return
        :   0 on success, error code on failure

    <a id="_CPPv4N19dvp_sensor_config_t14write_registerE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t14write_registerE"></a> <a id="_CPPv2N19dvp_sensor_config_t14write_registerE"></a> <a id="structdvp__sensor__config__t_1a3547e4ac7a86ee8ff15d9032f8f70d60"></a> int (\*write\_register)(uint32\_t reg, uint32\_t val)
    :   Write sensor register.

        Param reg
        :   Register address

        Param val
        :   Register value to write

        Return
        :   0 on success, error code on failure

<a id="_CPPv424dvp_sensor_detect_func_t"></a>

<a id="_CPPv324dvp_sensor_detect_func_t"></a> <a id="_CPPv224dvp_sensor_detect_func_t"></a> <a id="dvp_sensor_detect_func_t"></a> <a id="structdvp__sensor__detect__func__t"></a> struct dvp\_sensor\_detect\_func\_t
:   Camera sensor detection function structure.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N24dvp_sensor_detect_func_t6detectE"></a>

    <a id="_CPPv3N24dvp_sensor_detect_func_t6detectE"></a> <a id="_CPPv2N24dvp_sensor_detect_func_t6detectE"></a> <a id="structdvp__sensor__detect__func__t_1aa6bc22e7ed01c5fa81ad3168064cb9db"></a> const [dvp\_sensor\_config\_t](#_CPPv419dvp_sensor_config_t "dvp_sensor_config_t") \*(\*detect)(void)
    :   Detection function pointer

<a id="id10"></a>

### Macros

<a id="c.H264_SELF_DEFINE_SEI_SIZE"></a>

<a id="dvp__camera__types_8h_1a3f09d49dd57ef7f5359bf830bcdaa5d4"></a> H264\_SELF\_DEFINE\_SEI\_SIZE
:   Size of H.264 self-defined SEI data.

<a id="c._SECTION_ATTR_IMPL"></a>

<a id="dvp__camera__types_8h_1aa2981b422d41df7c27b71b901b070d5d"></a> \_SECTION\_ATTR\_IMPL(SECTION, COUNTER)
:   Section attribute macro implementation.

    参数
    :   - **SECTION** – Section name
        - **COUNTER** – Counter

<a id="c._CPIMTER_STRINGIFY"></a>

<a id="dvp__camera__types_8h_1a5374f0a0faba2ecaef934e0159f44a92"></a> \_CPIMTER\_STRINGIFY(COUNTER)
:   Stringify macro.

    参数
    :   - **COUNTER** – Counter

<a id="c.BK_CAMERA_SENSOR_DETECT_SECTION"></a>

<a id="dvp__camera__types_8h_1a9cff9b388e24b9ec31d7da02b8f3682f"></a> BK\_CAMERA\_SENSOR\_DETECT\_SECTION(f)
:   Camera sensor detection function section registration macro.

    This macro registers a sensor detection function into a dedicated section, enabling the system to automatically discover and run detection routines.

    参数
    :   - **f** – Detection function name

<a id="c.GC_QVGA_USE_SUBSAMPLE"></a>

<a id="dvp__camera__types_8h_1a66644ee9010a9ef92e185f533bc53add"></a> GC\_QVGA\_USE\_SUBSAMPLE
:   Flag for QVGA subsample usage.

<a id="c.BK_DVP_864X480_30FPS_MJPEG_CONFIG"></a>

<a id="dvp__camera__types_8h_1a4d631b1a04652cc954ec957632cd6aa5"></a> BK\_DVP\_864X480\_30FPS\_MJPEG\_CONFIG()
:   DVP camera configuration for 864x480 resolution at 30 FPS with MJPEG format.

    Predefined configuration macro for common DVP camera settings

<a id="id11"></a>

### Enumerations

<a id="_CPPv411sensor_id_t"></a>

<a id="_CPPv311sensor_id_t"></a> <a id="_CPPv211sensor_id_t"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6"></a> enum sensor\_id\_t
:   DVP sensor ID types.

    Enumeration of supported DVP sensor IDs

    *Values:*

    <a id="_CPPv4N11sensor_id_t9ID_UNKNOWE"></a>

    <a id="_CPPv3N11sensor_id_t9ID_UNKNOWE"></a> <a id="_CPPv2N11sensor_id_t9ID_UNKNOWE"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6aa522e5582aa8f0d9c6e142840443a523"></a> enumerator ID\_UNKNOW
    :   Unknown sensor ID

    <a id="_CPPv4N11sensor_id_t10ID_PAS6329E"></a>

    <a id="_CPPv3N11sensor_id_t10ID_PAS6329E"></a> <a id="_CPPv2N11sensor_id_t10ID_PAS6329E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a9bee58f985939f499c9d6cd3fe368d8e"></a> enumerator ID\_PAS6329
    :   PAS6329 sensor

    <a id="_CPPv4N11sensor_id_t9ID_OV7670E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_OV7670E"></a> <a id="_CPPv2N11sensor_id_t9ID_OV7670E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a4bff123c4ea8676da98770abdcb36c78"></a> enumerator ID\_OV7670
    :   OV7670 sensor

    <a id="_CPPv4N11sensor_id_t10ID_PAS6375E"></a>

    <a id="_CPPv3N11sensor_id_t10ID_PAS6375E"></a> <a id="_CPPv2N11sensor_id_t10ID_PAS6375E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6acfa56a6897a4e4a0313c06658a5da75c"></a> enumerator ID\_PAS6375
    :   PAS6375 sensor

    <a id="_CPPv4N11sensor_id_t10ID_GC0328CE"></a>

    <a id="_CPPv3N11sensor_id_t10ID_GC0328CE"></a> <a id="_CPPv2N11sensor_id_t10ID_GC0328CE"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a467d8e3d0b85197644f4e57f2e9bfd97"></a> enumerator ID\_GC0328C
    :   GC0328C sensor

    <a id="_CPPv4N11sensor_id_t9ID_BF2013E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_BF2013E"></a> <a id="_CPPv2N11sensor_id_t9ID_BF2013E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a828081741d1e90ce4a84ed13e28a111d"></a> enumerator ID\_BF2013
    :   BF2013 sensor

    <a id="_CPPv4N11sensor_id_t10ID_GC0308CE"></a>

    <a id="_CPPv3N11sensor_id_t10ID_GC0308CE"></a> <a id="_CPPv2N11sensor_id_t10ID_GC0308CE"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a1f60ec9fc31cf2140d8267273df0eef5"></a> enumerator ID\_GC0308C
    :   GC0308C sensor

    <a id="_CPPv4N11sensor_id_t9ID_HM1055E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_HM1055E"></a> <a id="_CPPv2N11sensor_id_t9ID_HM1055E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a310b28e1516bcc5d04869f1a85d32751"></a> enumerator ID\_HM1055
    :   HM1055 sensor

    <a id="_CPPv4N11sensor_id_t9ID_GC2145E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_GC2145E"></a> <a id="_CPPv2N11sensor_id_t9ID_GC2145E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a3fc0969905257087061c006548ad7b31"></a> enumerator ID\_GC2145
    :   GC2145 sensor

    <a id="_CPPv4N11sensor_id_t9ID_OV2640E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_OV2640E"></a> <a id="_CPPv2N11sensor_id_t9ID_OV2640E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6aa1f46e481e0e295c2a116c83e74a8275"></a> enumerator ID\_OV2640
    :   OV2640 sensor

    <a id="_CPPv4N11sensor_id_t9ID_GC0308E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_GC0308E"></a> <a id="_CPPv2N11sensor_id_t9ID_GC0308E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a59ebd0e84e50168cccc19ad6a2b808b3"></a> enumerator ID\_GC0308
    :   GC0308 sensor

    <a id="_CPPv4N11sensor_id_t10ID_TVP5150E"></a>

    <a id="_CPPv3N11sensor_id_t10ID_TVP5150E"></a> <a id="_CPPv2N11sensor_id_t10ID_TVP5150E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6afd325c5527ebb4b555f61ef252ce4ae8"></a> enumerator ID\_TVP5150
    :   TVP5150 sensor

    <a id="_CPPv4N11sensor_id_t8ID_SC101E"></a>

    <a id="_CPPv3N11sensor_id_t8ID_SC101E"></a> <a id="_CPPv2N11sensor_id_t8ID_SC101E"></a> <a id="dvp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a309ebd04930981b6a2fd3461a74367dc"></a> enumerator ID\_SC101
    :   SC101 sensor

<a id="_CPPv419sensor_bits_width_t"></a>

<a id="_CPPv319sensor_bits_width_t"></a> <a id="_CPPv219sensor_bits_width_t"></a> <a id="dvp__camera__types_8h_1a2e88e0bdcd75535c41cc70a73f121b4c"></a> enum sensor\_bits\_width\_t
:   Sensor data bit width types.

    Enumeration of supported data bit widths for DVP sensors

    *Values:*

    <a id="_CPPv4N19sensor_bits_width_t22SENSOR_BITS_WIDTH_8BITE"></a>

    <a id="_CPPv3N19sensor_bits_width_t22SENSOR_BITS_WIDTH_8BITE"></a> <a id="_CPPv2N19sensor_bits_width_t22SENSOR_BITS_WIDTH_8BITE"></a> <a id="dvp__camera__types_8h_1a2e88e0bdcd75535c41cc70a73f121b4ca627b071f865b79b8ed696402b7c05705"></a> enumerator SENSOR\_BITS\_WIDTH\_8BIT
    :   8-bit data width

    <a id="_CPPv4N19sensor_bits_width_t23SENSOR_BITS_WIDTH_10BITE"></a>

    <a id="_CPPv3N19sensor_bits_width_t23SENSOR_BITS_WIDTH_10BITE"></a> <a id="_CPPv2N19sensor_bits_width_t23SENSOR_BITS_WIDTH_10BITE"></a> <a id="dvp__camera__types_8h_1a2e88e0bdcd75535c41cc70a73f121b4cad427b19865d6676b692aaf7bd9388d96"></a> enumerator SENSOR\_BITS\_WIDTH\_10BIT
    :   10-bit data width

    <a id="_CPPv4N19sensor_bits_width_t23SENSOR_BITS_WIDTH_12BITE"></a>

    <a id="_CPPv3N19sensor_bits_width_t23SENSOR_BITS_WIDTH_12BITE"></a> <a id="_CPPv2N19sensor_bits_width_t23SENSOR_BITS_WIDTH_12BITE"></a> <a id="dvp__camera__types_8h_1a2e88e0bdcd75535c41cc70a73f121b4ca365ac02e3ca1f1b2d6b42c3237238fe7"></a> enumerator SENSOR\_BITS\_WIDTH\_12BIT
    :   12-bit data width

    <a id="_CPPv4N19sensor_bits_width_t23SENSOR_BITS_WIDTH_16BITE"></a>

    <a id="_CPPv3N19sensor_bits_width_t23SENSOR_BITS_WIDTH_16BITE"></a> <a id="_CPPv2N19sensor_bits_width_t23SENSOR_BITS_WIDTH_16BITE"></a> <a id="dvp__camera__types_8h_1a2e88e0bdcd75535c41cc70a73f121b4ca0c17a4343a81af61733f915ccd3de6ed"></a> enumerator SENSOR\_BITS\_WIDTH\_16BIT
    :   16-bit data width

<a id="_CPPv415dvp_ioctl_cmd_t"></a>

<a id="_CPPv315dvp_ioctl_cmd_t"></a> <a id="_CPPv215dvp_ioctl_cmd_t"></a> <a id="dvp__camera__types_8h_1a92f33c5d70242366bb168901fa9d5bbc"></a> enum dvp\_ioctl\_cmd\_t
:   *Values:*

    <a id="_CPPv4N15dvp_ioctl_cmd_t28DVP_IOCTL_CMD_H264_IDR_RESETE"></a>

    <a id="_CPPv3N15dvp_ioctl_cmd_t28DVP_IOCTL_CMD_H264_IDR_RESETE"></a> <a id="_CPPv2N15dvp_ioctl_cmd_t28DVP_IOCTL_CMD_H264_IDR_RESETE"></a> <a id="dvp__camera__types_8h_1a92f33c5d70242366bb168901fa9d5bbca7a6e824e6e1628598107e094bb7c9f17"></a> enumerator DVP\_IOCTL\_CMD\_H264\_IDR\_RESET
    :   Regenerate idr frame

    <a id="_CPPv4N15dvp_ioctl_cmd_t35DVP_IOCTL_CMD_SENSOR_WRITE_REGISTERE"></a>

    <a id="_CPPv3N15dvp_ioctl_cmd_t35DVP_IOCTL_CMD_SENSOR_WRITE_REGISTERE"></a> <a id="_CPPv2N15dvp_ioctl_cmd_t35DVP_IOCTL_CMD_SENSOR_WRITE_REGISTERE"></a> <a id="dvp__camera__types_8h_1a92f33c5d70242366bb168901fa9d5bbca4e01595c35b777c5f8d70c404f63976d"></a> enumerator DVP\_IOCTL\_CMD\_SENSOR\_WRITE\_REGISTER

    <a id="_CPPv4N15dvp_ioctl_cmd_t34DVP_IOCTL_CMD_SENSOR_READ_REGISTERE"></a>

    <a id="_CPPv3N15dvp_ioctl_cmd_t34DVP_IOCTL_CMD_SENSOR_READ_REGISTERE"></a> <a id="_CPPv2N15dvp_ioctl_cmd_t34DVP_IOCTL_CMD_SENSOR_READ_REGISTERE"></a> <a id="dvp__camera__types_8h_1a92f33c5d70242366bb168901fa9d5bbca601db09c948740b78cce5d3b6b44d1e2"></a> enumerator DVP\_IOCTL\_CMD\_SENSOR\_READ\_REGISTER
    :   Read sensor register
