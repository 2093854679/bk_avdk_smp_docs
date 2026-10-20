---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/camera/uvc.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="uvc"></a>

# UVC

<a id="id1"></a>

## 1\. 概述

> 本节主要说明UVC的工作流程，以及客户如何使用UVC摄像头。

- 有关UVC CAMERA的示例工程，请参阅：

  - [UVC CAMERA示例工程](../../examples/projects/uvc_example.md)
- 有关UVC CAMERA的API参考，请参阅：

  - [UVC CAMERA API](../../api-reference/multimedia/bk_camera.md)
- 有关图像内存申请释放的相关API，请参阅：

  - [图像内存管理](../../api-reference/multimedia/bk_frame_buffer.md)

<a id="id3"></a>

## 2\. 支持的功能

> 1、支持最大支持4个UVC同时输出，由宏UVC\_PORT\_MAX（CONFIG\_USBHOST\_HUB\_MAX\_EHPORTS）配置；
>
> 2、支持双码流，即单个摄像头同时输出两种类型的码流；
>
> 3、默认支持最多8个分辨率，如摄像头支持更多分辨率，需要软件作相应改动，修改宏：USBH\_VIDEO\_FRAME\_MAX\_NUM；
>
> 用户需要根据自己的应用方案，通过配置参数的方式，打开对应的功能

<a id="id4"></a>

## 3\. 相关宏定义

> | Marco name | info |
> | --- | --- |
> | CONFIG\_USB | enable usb or not |
> | CONFIG\_USB\_HOST | enable usb host or not |
> | CONFIG\_USB\_HUB\_MULTIPLE\_DEVICES | config usb hub support multiple device |
> | CONFIG\_USBHOST\_HUB\_MAX\_EHPORTS | config support max ep, default 4 |
> | CONFIG\_USBHOST\_HUB\_PORT\_SUPPORT\_MAX\_DEVICE | config support max devices, default 5 |
> | CONFIG\_USBHOST\_HUB\_PORT\_1\_VBAT\_CONTROL\_GPIO\_ID | gpio control hub power, default 0 |
> | CONFIG\_USBH\_MSC | enable usb hub MSC or not |
> | CONFIG\_USBH\_UVC | enable usb hub uvc or not |
> | CONFIG\_USBH\_UAC | enable usb hub uvc or not |
> | CONFIG\_USB\_CAMERA | enable usb camera or not |
> | CONFIG\_USB\_VBAT\_CONTROL\_GPIO\_ID | gpio control hub power, default 0x1C |
> | CONFIG\_USB\_DMA\_ENABLE | enable usb dma copy data or not |
> | CONFIG\_UVC\_CHECK\_BULK\_JPEG\_HEADER | enable BULK JPEG header check or not |
> | CONFIG\_UVC\_URB\_NUM | Config URB number, default 8 |
> | CONFIG\_UVC\_NUM\_PACKET\_PER\_URB | Config URB number packet per urb, default 8 |
> | CONFIG\_UVC\_PROCESS\_TASK\_STACK\_SIZE | UVC process task stack size, default 1024 |
> | CONFIG\_UVC\_STREAM\_TASK\_STACK\_SIZE | UVC stream task stack size, default 1536 |

备注

1. 以上宏定义为UVC的宏定义，用户可以根据实际情况进行配置。尤其是CONFIG\_UVC\_PROCESS\_TASK\_STACK\_SIZE和CONFIG\_UVC\_STREAM\_TASK\_STACK\_SIZE，需要根据实际情况进行配置。
2. CONFIG\_UVC\_URB\_NUM和CONFIG\_UVC\_NUM\_PACKET\_PER\_URB，需要根据使用UVC的摄像头数量进行配置。理论上urb的数量应该至少是使用UVC的摄像头数量的两倍。
3. UVC\_PROCESS\_TASK中会调用bk\_uvc\_callback\_t中的malloc/complete回调函数，回调函数如果太深就会导致栈溢出，且回调函数里面不能有任何的阻塞操作，也不能执行长时间的操作，否则会导致UVC\_PROCESS\_TASK阻塞，进而导致图像异常。在下面的创建UVC摄像头控制器中会给出具体的示例，实例中回调函数只进行了简单的帧缓冲区申请释放操作，用户需要根据实际情况进行配置。

<a id="id5"></a>

## 4\. UVC摄像头的使用流程

1. 启动UVC电源
2. 创建UVC摄像头控制器
3. 打开UVC摄像头
4. 关闭UVC摄像头
5. 删除UVC摄像头
6. 挂起UVC摄像头
7. 恢复UVC摄像头
8. 关闭UVC电源

<a id="id6"></a>

### 4.1 启动UVC电源

> 调用如下接口启动UVC电源：

```
// power on
bk_err_t bk_usbh_hub_multiple_devices_power_on(E_USB_MODE mode, E_USB_HUB_PORT_INDEX port_index, E_USB_DEVICE_T class_dev_index);
```

描述：
\- 启动UVC电源，返回错误码。

参数：
:   mode：USB模式，默认为USB\_MODE\_HOST。

    port\_index：USB端口索引，默认为1，最大值由宏UVC\_PORT\_MAX控制。

    class\_dev\_index：USB设备索引，支持USB\_UVC\_DEVICE和USB\_UVC\_H26X\_DEVICE。

    USB\_UVC\_DEVICE：UVC摄像头设备；

    USB\_UVC\_H26X\_DEVICE：UVC H26X摄像头设备；

备注

一般需要根据摄像头输出的格式确定，如果需要输出MJPEG，则使用USB\_UVC\_DEVICE，如果需要输出H26X(264/265)，则使用USB\_UVC\_H26X\_DEVICE。
一般建议都开或者都关，不区分输出格式。

具体上电流程可参考如下：

```
/**
 * @brief UVC连接成功回调函数
 * @details 当UVC设备上电后成功连接时会触发此回调函数。
 *          它会存储端口信息并触发连接信号量。
 * @param port_info USB集线器端口信息结构指针
 * @param arg 用户参数指针（uvc_test_info_t结构）
 */
static void uvc_connect_successful_callback(bk_usb_hub_port_info *port_info, void *arg)
{
    LOGI("%s, %d\n", __func__, __LINE__);
    uvc_test_info_t *info = (uvc_test_info_t *)arg;
    if (info == NULL)
        return;
    rtos_lock_mutex(&info->uvc_mutex);
    info->port_info[port_info->port_index - 1] = port_info;
    rtos_set_semaphore(&info->uvc_connect_semaphore);
    rtos_unlock_mutex(&info->uvc_mutex);
}

/**
 * @brief UVC断开连接回调函数
 * @details 当UVC设备断开连接时会触发此回调函数。
 *          它会清除端口信息。
 * @param port_info USB集线器端口信息结构指针
 * @param arg 用户参数指针（uvc_test_info_t结构）
 */
static void uvc_disconnect_callback(bk_usb_hub_port_info *port_info, void *arg)
{
    LOGI("%s, %d\n", __func__, __LINE__);
    uvc_test_info_t *info = (uvc_test_info_t *)arg;
    if (info == NULL)
        return;
    rtos_lock_mutex(&info->uvc_mutex);
    info->port_info[port_info->port_index - 1] = NULL;
    rtos_unlock_mutex(&info->uvc_mutex);
}

/**
 * @brief UVC摄像头设备上电函数
 * @details 此函数会在所有端口上电UVC摄像头设备。
 *          它会注册连接和断开回调函数。
 * @param device USB设备类型（USB_UVC_DEVICE或USB_UVC_H26X_DEVICE）
 * @return avdk_err_t 错误码（AVDK_ERR_OK如果成功）
 */
static avdk_err_t uvc_camera_device_power_on(E_USB_DEVICE_T device)
{
    avdk_err_t ret = AVDK_ERR_OK;
    // 给每个端口注册连接和断开回调函数，并给对应端口的UVC设备上电
    for (uint8_t port = 1; port <= UVC_PORT_MAX; port++)
    {
        bk_usbh_hub_port_register_connect_callback(port, device, uvc_connect_successful_callback, uvc_test_info);
        bk_usbh_hub_port_register_disconnect_callback(port, device, uvc_disconnect_callback, uvc_test_info);
        bk_usbh_hub_multiple_devices_power_on(USB_HOST_MODE, port, device);
    }

    // 检查UVC端口是否已经连接成功
    for (uint8_t port = 1; port <= UVC_PORT_MAX; port++)
    {
        ret = bk_usbh_hub_port_check_device(port, device, &uvc_test_info->port_info[port - 1]);
        if (ret == AVDK_ERR_OK)
        {
            break;
        }
    }

    return ret;
}

/**
 * @brief UVC摄像头设备上电处理函数
 * @details 此函数会上电UVC摄像头设备并等待连接成功回调。
 * @param info UVC测试信息结构指针
 * @param timeout 超时时间（单位：毫秒）
 * @return avdk_err_t 错误码（AVDK_ERR_OK如果成功）
 */
static avdk_err_t uvc_camera_power_on_handle(uvc_test_info_t *info, uint32_t timeout)
{
    // 上电UVC摄像头设备，并等待连接成功回调
    avdk_err_t ret = AVDK_ERR_OK;

    /*USB_UVC_H26X_DEVICE: for h26x stream, this can not execute*/
    ret = uvc_camera_device_power_on(USB_UVC_H26X_DEVICE);
    /*USB_UVC_DEVICE: for mjpeg stream*/

    ret = uvc_camera_device_power_on(USB_UVC_DEVICE);

    // 如果未检测到已经连接成功，等待连接成功回调
    if (ret != AVDK_ERR_OK)
    {
        ret = rtos_get_semaphore(&info->uvc_connect_semaphore, timeout);
        if (ret != AVDK_ERR_OK)
        {
            LOGE("%s, %d, timeout:%d\n", __func__, __LINE__, timeout);
        }
    }

    return ret;
}

// 用户基本调用流程
{
    avdk_err_t ret = AVDK_ERR_OK;
    ret = uvc_camera_power_on_handle(uvc_test_info, 4000);
    if (ret != AVDK_ERR_OK)
    {
        LOGE("%s, %d: uvc_camera_power_on_handle failed\n", __func__, __LINE__);
        ret = uvc_camera_power_off_handle(uvc_test_info);
        if (ret != AVDK_ERR_OK)
        {
            LOGE("%s, %d: uvc_camera_power_off_handle failed\n", __func__, __LINE__);
        }
        goto exit;
    }

    ...
}
```

描述：
:   使用UVC之前需要先给UVC上电。

    上电之前需要先注册回调函数（连接成功/连接断开）。

    备份/删除端口信息port\_info，建议使用互斥锁添加保护，以防止在使用端口信息的过程中，突然断开，使port\_info失效，导致访问异常指针问题。

    上电完成后，先检查是否已经成功连接，因为当UAC在UVC之前打开时，注册的连接成功回调不会被触发。导致信号量不会被置上。

    如果没有连接成功，等待连接成功回调，超时时间用户自行配置，当连接成功后，才进行后续操作。

    如果连接超时，建议直接关闭电源，以达到低功耗的目的。

<a id="id7"></a>

### 4.2 创建UVC摄像头控制器

> 当上电完成，且成功枚举到UVC设备后，调用如下接口创建UVC摄像头控制器：

```
avdk_err_t bk_camera_uvc_ctlr_new(bk_camera_ctlr_handle_t *handle, bk_uvc_ctlr_config_t *config);
```

描述：
:   创建UVC摄像头控制器，返回控制器句柄。

    传入的配置包含两个部分：

    第一部分：bk\_uvc\_config\_t，包含UVC需要输出的分辨率帧率配置，需要输出的图像格式配置等。

    第二部分：bk\_uvc\_callback\_t，通过此回调函数申请存放目标数据的空间，以及返回图像数据给用户，用户自行管理目标数据。

参数：
:   handle：UVC摄像头控制器句柄。

    config：UVC摄像头控制器配置参数。

相关数据结构：`bk_uvc_ctlr_config_t`, `bk_cam_uvc_config_t`, `bk_uvc_callback_t`。
参考路径：`ap/include/components/uvc_camera_types.h`。
bk\_cam\_uvc\_config\_t支持如下默认配置：

```
/**
* @brief 默认UVC配置（864x480分辨率，30 FPS，MJPEG格式）
*
* 提供UVC摄像头初始化的标准配置，包含：
* - 单流模式
* - 端口1
* - 不丢帧：支持配置丢弃摄像头启动时输出的图像数据，避免启动时图像数据异常。
* - 分辨率：864x480像素
* - 帧率：30 FPS
* - 图像格式：MJPEG
* - 无用户参数
*/
#define BK_UVC_864X480_30FPS_MJPEG_CONFIG() \
{\
    .type = UVC_SINGLE_STREAM, \
    .port = 1, \
    .drop_num = 0, \
    .img_format = IMAGE_MJPEG, \
    .width = 864, \
    .height = 480, \
    .fps = 30, \
    .arg = NULL, \
}

// 注册申请存储目标数据的回调函数。
// 建议用户针对申请的帧，根据图像格式选择自己维护的链表中空闲的节点，与下面complete的操作维护两个链表，一个是free链表，一个是ready链表。
// 每次申请时从free链表中取出一个节点，申请完成后将节点加入到ready链表中，需要使用时从ready链表中取出，使用后直接释放到free链表中。
// 具体可以参考： ``./projects/dvp_example/dvp_test/src/dvp_frame_list.c``, 实现自己的链表。
/**
 * @brief UVC帧缓冲区分配函数
 * @details 根据图像格式分配相应的帧缓冲区，并初始化帧缓冲区的基本属性
 * @param format 图像格式，支持IMAGE_YUV/IMAGE_MJPEG/IMAGE_H264等格式
 * @param size 需要分配的缓冲区大小（字节）
 * @return 成功时返回分配的帧缓冲区指针，失败时返回NULL
 */
static frame_buffer_t *uvc_frame_malloc(image_format_t format, uint32_t size)
{
    frame_buffer_t *frame = NULL;
    if (format == IMAGE_YUV)
    {
        // 用户添加自己的操作，如从free链表中取出一个节点（此处测试直接申请一块buf，没有通过链表进行管理）
        // frame = frame_buffer_display_malloc(size);
    }
    else
    {
        // 用户添加自己的操作，如从free链表中取出一个节点（此处测试直接申请一块buf，没有通过链表进行管理）
        // frame = frame_buffer_encode_malloc(size);
    }

    if (frame)
    {
        frame->sequence = 0;
        frame->length = 0;
        frame->timestamp = 0;
        frame->size = size;
    }

    return frame;
}


// 注册回调函数，用于处理UVC图像数据的完成回调。
/**
 * @brief UVC帧缓冲区完成回调函数
 * @details 当UVC摄像头输出一帧图像数据后，会调用此回调函数通知应用层图像数据已完成。
 * @param port 图像数据所属的UVC端口号
 * @param frame 指向包含图像数据的帧缓冲区结构体指针
 * @param result 图像数据处理结果，0表示成功，其他值表示失败，成功的帧可以被推到用户的链表中进行管理，失败的帧直接释放
 */
static void uvc_frame_complete(uint8_t port, image_format_t format, frame_buffer_t *frame, int result)
{
    if (frame->sequence % 30 == 0)
    {
        LOGD("%s: port:%d, seq:%d, length:%d, format:%s, h264_type:%x, result:%d\n", __func__, port, frame->sequence,
            frame->length, (format == IMAGE_MJPEG) ? "mjpeg" : "h264", frame->h264_type, result);
    }

    if (format == IMAGE_YUV)
    {
        // 用户添加自己的操作，如添加到ready链表中（此处测试直接释放buf，没有检查图像是否正确，没有通过链表进行管理）
        //frame_buffer_display_free(frame);
    }
    else
    {
        // 用户添加自己的操作，如添加到ready链表中（此处测试直接释放buf，没有检查图像是否正确，没有通过链表进行管理）
        //frame_buffer_encode_free(frame);
    }
}

/**
 * @brief UVC事件回调函数
 * @details 当UVC设备发生事件时会调用此回调函数，目前主要用于打印事件代码
 * @param port_info 端口信息结构体指针，包含UVC设备连接的端口信息
 * @param arg 用户自定义参数，可以在创建UVC控制器时传入
 * @param code 事件代码，表示发生的UVC事件类型，具体事件代码请参考bk_camera_uvc_event_code_t
 */
static void uvc_event_callback(bk_usb_hub_port_info *port_info,void *arg, uvc_error_code_t code)
{
    LOGD("uvc_event_callback: %d", code);
}

static const bk_uvc_callback_t uvc_cbs = {
    .malloc = uvc_frame_malloc,
    .complete = uvc_frame_complete,
    .uvc_event_callback = uvc_event_callback,
};

/**
* @brief 根据用户配置检查UVC端口信息，客户可自定义选择是否做检查
*
* 此函数根据提供的用户配置检查UVC端口信息。
* 它会根据支持的UVC格式验证端口、格式、宽度和高度。
*
* @param info UVC测试信息结构体指针
* @param user_config 用户配置结构体指针
* @return avdk_err_t 表示操作成功或失败的错误码
*/
static avdk_err_t uvc_checkout_port_info(uvc_test_info_t *info, bk_cam_uvc_config_t *user_config)
{
    if (info == NULL)
    {
        LOGE("%s: info is NULL\n", __func__);
        return AVDK_ERR_INVAL;
    }

    if (user_config == NULL)
    {
        LOGE("%s: config is NULL\n", __func__);
        return AVDK_ERR_INVAL;
    }

    LOGD("%s, %d, port:%d, format:%d, W*H:%d*%d\r\n", __func__, __LINE__, user_config->port, user_config->img_format,
        user_config->width, user_config->height);

    avdk_err_t ret = AVDK_ERR_OK;
    switch (user_config->img_format)
    {
        case IMAGE_YUV:
            ret = uvc_checkout_port_info_yuv(info, user_config);
            break;

        case IMAGE_MJPEG:
            ret = uvc_checkout_port_info_mjpeg(info, user_config);
            break;

        case IMAGE_H264:
            ret = uvc_checkout_port_info_h264(info, user_config);
            break;

        case IMAGE_H265:
            ret = uvc_checkout_port_info_h265(info, user_config);
            break;

        default:
            LOGE("%s, please check usb output format:%d\r\n", __func__, user_config->img_format);
            ret = AVDK_ERR_UNSUPPORTED;
            break;
    }

    return ret;
}


// 创建UVC摄像头控制器示例代码
{
    bk_uvc_ctlr_config_t uvc_ctlr_config = {
        .config = BK_UVC_864X480_30FPS_MJPEG_CONFIG(),
        .cbs = &uvc_cbs,
    };

    // 通过传入参数修改默认配置
    uvc_ctlr_config.config.img_format = output_format;
    uvc_ctlr_config.config.width = ppi >> 16;
    uvc_ctlr_config.config.height = ppi & 0xFFFF;
    uvc_ctlr_config.config.user_data = test_info;
    if (argc > 2)
    {
        // 通过传入参数配置port端口
        port = os_strtoul(argv[2], NULL, 10);
        if (port > UVC_PORT_MAX || port == 0)
        {
            LOGE("%s, %d: invalid port %d\n", __func__, __LINE__, port);
            goto exit;
        }
        uvc_ctlr_config.config.port = port;
    }

    // 可以检查用户配置是否与端口信息匹配
    ret = uvc_checkout_user_info(test_info, &uvc_ctlr_config.config);
    if (ret != AVDK_ERR_OK)
    {
        LOGE("%s, %d: uvc_checkout_user_info failed, ret:%d\n", __func__, __LINE__, ret);
        goto exit;
    }

    // create new
    ret = bk_camera_uvc_ctlr_new(&test_info->handle[port - 1], &uvc_ctlr_config);
}
```

描述：
:   检查UVC端口信息。

    检查用户输出的配置，此端口是否支持。

    检查的过程中，建议使用互斥锁添加保护，保证线程安全。

    检查也可以不做，只有保证分辨率输入正常，才不会影响到后面打开UVC。

<a id="id8"></a>

### 4.3 打开UVC摄像头

> 调用如下接口打开UVC摄像头：

```
avdk_err_t bk_camera_open(bk_camera_ctlr_handle_t handle);
```

描述：
:   打开UVC摄像头，返回错误码。

    打开UVC摄像头后，上面注册的回调函数会不停的申请数据空间用以存储。

    打开UVC摄像头后，会开始采集数据，且会调用上面注册的回调函数，将采集到的数据返回给用户，用户需要关注frame是否有效，选择使用还是释放。

    如果出现问题，会调用上面注册的回调函数uvc\_event\_callback，返回错误码。

    打开UVC摄像头后，用户注册的连接成功/断开回调函数不再生效，所有的状态信息，包括连接/断开的状态通过uvc\_event\_callback返回给用户。

参数：
:   handle：UVC摄像头控制器句柄。

<a id="id9"></a>

### 4.4 关闭UVC摄像头

> 调用如下接口关闭UVC摄像头：

```
avdk_err_t bk_camera_close(bk_camera_ctlr_handle_t handle);
```

描述：
:   关闭UVC摄像头，返回错误码。

    关闭UVC摄像头后，上面注册的回调函数会停止申请数据空间，且不会再调用上面注册的回调函数。

    关闭UVC摄像头后，会停止采集数据。

参数：
:   handle：UVC摄像头控制器句柄。

<a id="id10"></a>

### 4.5 注销UVC摄像头

> 调用如下接口注销UVC摄像头：

```
avdk_err_t bk_camera_delete(bk_camera_ctlr_handle_t handle);
```

描述：
:   注销UVC摄像头，返回错误码。

    注销UVC摄像头后，释放UVC摄像头控制器的资源。

参数：
:   handle：UVC摄像头控制器句柄。

<a id="id11"></a>

### 4.6 暂停所有UVC摄像头

> 调用如下接口暂停UVC摄像头：

```
avdk_err_t bk_camera_suspend(bk_camera_ctlr_handle_t handle);
```

描述：
:   暂停UVC摄像头，返回错误码。

    暂停UVC摄像头后，上面注册的回调函数会停止申请数据空间，且不会再调用上面注册的回调函数。

    暂停UVC摄像头后，会停止采集数据。

    这里UVC暂停，UVC依旧会继续采集数据，只是采集的数据不做处理了，所有没有有效帧数据输出。

参数：
:   handle：UVC摄像头控制器句柄。

<a id="id12"></a>

### 4.7 恢复所有UVC摄像头

> 调用如下接口恢复UVC摄像头：

```
avdk_err_t bk_camera_resume(bk_camera_ctlr_handle_t handle);
```

描述：
:   恢复UVC摄像头，返回错误码。

    恢复UVC摄像头后，上面注册的回调函数会继续申请数据空间，且会继续调用上面注册的回调函数。

    恢复UVC摄像头后，会继续采集数据。

参数：
:   handle：UVC摄像头控制器句柄。

<a id="id13"></a>

### 4.8 UVC关闭电源

> 调用如下接口关闭UVC摄像头的电源：

```
bk_err_t bk_usbh_hub_multiple_devices_power_down(USB_HOST_MODE, port, device);
```

描述：
:   关闭UVC摄像头的电源，返回错误码。

参数：
:   port：USB端口号。

    device：USB设备号,默认是USB\_UVC\_DEVICE, 还支持USB\_UVC\_H26X\_DEVICE。

    参考下面掉电逻辑：

```
/*
 * uvc_camera_device_power_off - 关闭UVC摄像头设备电源
 * @device: USB设备类型（USB_UVC_DEVICE或USB_UVC_H26X_DEVICE）
 *
 * 此函数通过遍历所有UVC端口、注销连接和断开连接回调函数，并调用底层API来关闭指定的UVC摄像头设备电源。
 *
 * 该函数通常在UVC系统关闭时调用，以确保所有连接的设备都能正确断电。
 */
static void uvc_camera_device_power_off(E_USB_DEVICE_T device)
{
    // Iterate through all possible UVC ports
    for (uint8_t port = 1; port <= UVC_PORT_MAX; port++)
    {
        // Unregister the connection callback for this port and device
        bk_usbh_hub_port_register_connect_callback(port, device, NULL, NULL);
        // Unregister the disconnection callback for this port and device
        bk_usbh_hub_port_register_disconnect_callback(port, device, NULL, NULL);
        // Power down the specified device on this port
        bk_usbh_hub_multiple_devices_power_down(USB_HOST_MODE, port, device);
    }
}


/**
 * @brief UVC摄像头设备断电处理函数
 * @details 此函数在UVC系统关闭时调用，用于确保所有已连接的UVC设备正确断电。
 *          它会先检查所有UVC端口是否已关闭，然后释放信号量、关闭设备电源并清除端口信息。
 * @param info UVC测试信息结构体指针
 * @return 成功时返回AVDK_ERR_OK，失败时返回AVDK_ERR_GENERIC
 */
static avdk_err_t uvc_camera_power_off_handle(uvc_test_info_t *info)
{
    // Before power-off, check if all ports are closed
    avdk_err_t ret = AVDK_ERR_GENERIC;
    if (info == NULL)
    {
        LOGE("%s, %d: info is NULL\n", __func__, __LINE__);
        return ret;
    }
    uint8_t all_closed = true;
    for (uint8_t port = 1; port <= UVC_PORT_MAX; port++)
    {
        if (info->handle[port - 1] != NULL)
        {
            all_closed = false;
            LOGW("%s, %d: port %d not closed\n", __func__, __LINE__, port);
        }
    }

    if (all_closed)
    {
        rtos_get_semaphore(&info->uvc_connect_semaphore, BEKEN_NO_WAIT);
        uvc_camera_device_power_off(USB_UVC_H26X_DEVICE);
        uvc_camera_device_power_off(USB_UVC_DEVICE);
        os_memset(info->port_info, 0, sizeof(bk_usb_hub_port_info *) * UVC_PORT_MAX);
        ret = AVDK_ERR_OK;
    }

    return ret;
}

// power off
{
    ...

    ret = uvc_camera_power_off_handle(uvc_test_info);

    ...
}
```

描述：
:   掉电之前确保所有端口都已经关闭。

    关闭UVC摄像头的电源，返回错误码。

参数：
:   port：USB端口号。

    device：USB设备号,默认是USB\_UVC\_DEVICE, 还支持USB\_UVC\_H26X\_DEVICE。

<a id="id14"></a>

## 5\. UVC支持方案

1. UVC直接输出MJPEG图像，通过联合JPEG解码器进行解码，将MJPEG图像转换为YUV格式，再联合LCD显示器进行显示，且UVC输出的MJPEG联合WiFi模块，进行图传。
2. UVC直接输出MJPEG图像，通过联合JPEG解码器进行解码，将MJPEG图像转换为YUV格式，再通过联合H264编码器进行编码成H.264格式，再联合LCD显示器对解码后的图像进行显示，联合WiFi模块对编码的H.264图像进行图传。可以参考doobell方案。
3. UVC直接输出双码流H264\&MJPEG图像（一个端口输出两种格式，或者两个端口分别输出H264和MJPEG），联合JPEG解码器进行解码，将MJPEG图像转换为YUV格式，再联合LCD显示器对解码后的图像进行显示，联合WiFi模块对UVC输出的H264图像进行图传。
