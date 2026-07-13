# UVC 摄像头



## 1. 概述

UVC（USB Video Class）摄像头通过 USB Host 接口连接，支持 MJPEG、H264/H265、YUV 等多种码流输出，无需适配 Sensor 寄存器，即插即用。


- 示例工程：`projects/multimedia/uvc_example` （采集调试）、`projects/multimedia/uvc_display_example` （UVC MJPEG 显示流水线，`pipeline open`）

- API 参考：[UVC CAMERA API](../../api-reference/multimedia/bk_camera.md "../../api-reference/multimedia/bk_camera.md")

- 图像内存管理：[图像内存管理](../../api-reference/multimedia/bk_frame_buffer.md "../../api-reference/multimedia/bk_frame_buffer.md")

- USB 底层说明：[USB Host UVC+UAC](../peripheral/usb/bk_usbh_uvc_uac.md "../peripheral/usb/bk_usbh_uvc_uac.md")


## 2. 支持外设


### 2.1 已验证 UVC 设备

以下设备已在平台调试验证（VID/PID 标识）：

| 设备标识 (VID&PID) | 支持分辨率-帧率 |
| --- | --- |
| USB\VID_0C45&PID_64AB&REV_0822 | 1280×720-15, 800×480-15, 640×480-15, 480×320-15 |
| USB\VID_13D3&PID_78AB&REV_0826 | 640×480-15 |
| USB\VID_13D3&PID_78AB&REV_0829 | 1280×720-10, 640×480-30, 480×800-30, 480×320-30, 320×240-30 |
| USB\VID_0C45&PID_64AB&REV_0811 | 640×480-25 |
| USB\VID_1871&PID_FF50&REV_0100 | 640×480-15, 480×320-15, 352×288-15, 320×240-15 |
| USB\VID_0C45&PID_64AB&REV_1202 | 640×480-25, 480×320-30, 320×240-30 |
| USB\VID_0C45&PID_64A0&REV_0100 | 800×480-15, 640×480-15, 480×320-15, 352×288-15 |
| USB\VID_13D3&PID_784B&REV_1001 | 640×480-15 |
| USB\VID_05A3&PID_9230&REV_0909 | 1280×720-25, 640×480-15, 480×800-25 |
| USB\VID_0C45&PID_636B&REV_0100 | 800×480-25, 640×320-25, 480×320-25 |
| USB\VID_174F&PID_2459&REV_0008 | 1280×720-30, 960×540-30 |
| USB\VID_0C45&PID_1915&REV_0100 | 1280×720-5, 800×600-15, 640×480-15 等 |
| USB\VID_8088&PID_0001&REV_0000 | 1280×720-10, 640×480-10 等 |
| USB\VID_4C4A&PID_4C55&REV_0100 | 1280×720-10, 640×480-10 等 |
| USB\VID_1E45&PID_8022&REV_1601 | 1280×720-30, 848×480-30, 640×480-30 等 |
| USB\VID_0FFE&PID_0001&REV_0200 | 720×1280-15, 480×800-15 等 |
| USB\VID_0C45&PID_64AB&REV_0525 | 1280×720-10, 1024×600-15, 864×480-15 等 |

备注

未在列表中的 UVC 设备通常也可工作，但需确认其描述符中的分辨率与帧率在软件支持范围内。


### 2.2 硬件要求


- USB 控制器：BK7259 内置 Mentor MUSB MHDRC HS USB 2.0 OTG

- 工作电压：5.0V（通过 `CONFIG_USB_VBAT_CONTROL_GPIO_ID` 控制 VBUS）

- 多设备：支持 USB Hub，最多 4 路 UVC 同时输出（`CONFIG_USBHOST_HUB_MAX_EHPORTS`）


## 3. 调试说明


### 3.1 编译与烧录


```
cd <SDK_ROOT>
make bk7259 PROJECT=multimedia/uvc_example -j$(nproc)

```


### 3.2 CLI 命令


**打开 UVC 摄像头：**


```
uvc open <port> <width> <height> <h264|h265|mjpeg|yuv>

```

示例：


```
uvc open 1 640 480 mjpeg
uvc open 1 1280 720 h264

```


**关闭 UVC 摄像头：**


```
uvc close <port>

```


### 3.3 常见问题排查

| 现象 | 排查建议 |
| --- | --- |
| 枚举失败 / 无设备 | 检查 VBUS 供电 GPIO、USB 线缆、`CONFIG_USBH_UVC` 宏 |
| 打开超时 | 先注册连接回调再上电；检查 `bk_usbh_hub_port_check_device` |
| 图像卡顿 / 丢帧 | 增大 `CONFIG_UVC_URB_NUM`；回调中禁止阻塞操作 |
| 栈溢出 | 增大 `CONFIG_UVC_PROCESS_TASK_STACK_SIZE` |
| 分辨率不支持 | 用 USB 描述符确认摄像头支持的分辨率，勿超出 `USBH_VIDEO_FRAME_MAX_NUM` |


## 4. 支持的功能

> 1、支持最大支持4个UVC同时输出，由宏UVC_PORT_MAX（CONFIG_USBHOST_HUB_MAX_EHPORTS）配置；
>
> 2、支持双码流，即单个摄像头同时输出两种类型的码流；
>
> 3、默认支持最多8个分辨率，如摄像头支持更多分辨率，需要软件作相应改动，修改宏：USBH_VIDEO_FRAME_MAX_NUM；
>
> 用户需要根据自己的应用方案，通过配置参数的方式，打开对应的功能


## 5. 相关宏定义

> | Marco name | info |
> | --- | --- |
> | CONFIG_USB | enable usb or not |
> | CONFIG_USB_HOST | enable usb host or not |
> | CONFIG_USB_HUB_MULTIPLE_DEVICES | config usb hub support multiple device |
> | CONFIG_USBHOST_HUB_MAX_EHPORTS | config support max ep, default 4 |
> | CONFIG_USBHOST_HUB_PORT_SUPPORT_MAX_DEVICE | config support max devices, default 5 |
> | CONFIG_USBHOST_HUB_PORT_1_VBAT_CONTROL_GPIO_ID | gpio control hub power, default 0 |
> | CONFIG_USBH_MSC | enable usb hub MSC or not |
> | CONFIG_USBH_UVC | enable usb hub uvc or not |
> | CONFIG_USBH_UAC | enable usb hub uvc or not |
> | CONFIG_USB_CAMERA | enable usb camera or not |
> | CONFIG_USB_VBAT_CONTROL_GPIO_ID | gpio control hub power, default 0x1C |
> | CONFIG_USB_DMA_ENABLE | enable usb dma copy data or not |
> | CONFIG_UVC_CHECK_BULK_JPEG_HEADER | enable BULK JPEG header check or not |
> | CONFIG_UVC_URB_NUM | Config URB number, default 8 |
> | CONFIG_UVC_NUM_PACKET_PER_URB | Config URB number packet per urb, default 8 |
> | CONFIG_UVC_PROCESS_TASK_STACK_SIZE | UVC process task stack size, default 1024 |
> | CONFIG_UVC_STREAM_TASK_STACK_SIZE | UVC stream task stack size, default 1536 |

备注

1. 以上宏定义为UVC的宏定义，用户可以根据实际情况进行配置。尤其是CONFIG_UVC_PROCESS_TASK_STACK_SIZE和CONFIG_UVC_STREAM_TASK_STACK_SIZE，需要根据实际情况进行配置。
2. CONFIG_UVC_URB_NUM和CONFIG_UVC_NUM_PACKET_PER_URB，需要根据使用UVC的摄像头数量进行配置。理论上urb的数量应该至少是使用UVC的摄像头数量的两倍。
3. UVC 处理任务中会调用 `bk_uvc_callback_t` 的 `frame_malloc` / `frame_complete` 回调，回调中禁止阻塞或长时间操作，否则会导致图像异常。详见下文第 6 节示例。


## 6. UVC 摄像头使用流程

参考工程：`projects/multimedia/uvc_example/ap/src/uvc_test.c`

当前 UVC API 位于 `ap/include/components/bk_uvc_camera.h`，主要接口：

| API | 说明 |
| --- | --- |
| `bk_uvc_ctrl_new` | 创建 UVC 控制器，注册回调 |
| `bk_uvc_init` | 初始化控制器硬件资源 |
| `bk_uvc_open` | 按配置打开 UVC 设备并开始采集 |
| `bk_uvc_close` | 关闭设备、停止采集 |
| `bk_uvc_deinit` | 释放控制器资源 |
| `bk_uvc_delete` | 销毁控制器实例 |
| `bk_uvc_suspend` | 低功耗挂起 |
| `bk_uvc_resume` | 从挂起恢复 |


### 6.1 高层封装（推荐）

示例工程提供 `uvc_camera_turn_on()` / `uvc_camera_turn_off()` 封装完整流程：


```
// 打开（内部依次：上电 → 检查端口 → new → init → open）
bk_cam_uvc_config_t config = MEDIA_UVC_MJPEG_864X480_30FPS_CONFIG();
config.port = 1;
config.width = 640;
config.height = 480;
config.format = BK_IMAGE_FORMAT_MJPEG;
handle = uvc_camera_turn_on(&config);

// 关闭（内部依次：close → deinit → delete → 下电）
uvc_camera_turn_off(handle);

```


### 6.2 分步调用


```
static const bk_uvc_callback_t uvc_camera_cbs = {
    .frame_malloc = uvc_camera_frame_malloc,
    .frame_complete = uvc_camera_frame_complete,
    .state_change_cb = uvc_event_callback,
    .user_data = &s_uvc_handle,
};

// 1. 上电并等待设备连接
uvc_camera_power_on(4000);

// 2. 检查端口是否支持目标分辨率/格式
uvc_checkout_port_info(&config);

// 3. 创建 → 初始化 → 打开
bk_uvc_ctrl_new(&handle, &uvc_camera_cbs);
bk_uvc_init(handle);
bk_uvc_open(handle, &config);

// 4. 关闭 → 反初始化 → 销毁 → 下电
bk_uvc_close(handle);
bk_uvc_deinit(handle);
bk_uvc_delete(handle);
uvc_camera_power_off();

```


### 6.3 电源管理

上电（`uvc_camera_power_on`）流程：

1. 注册 `bk_usbh_hub_port_register_connect_callback()` 连接回调
2. 对所有端口调用 `bk_usbh_hub_multiple_devices_power_on(USB_HOST_MODE, port, USB_UVC_DEVICE)`
3. 对 H26x 码流同样上电 `USB_UVC_H26X_DEVICE`
4. 调用 `bk_usbh_hub_port_check_device()` 检查是否已连接；未连接则等待信号量超时

下电（`uvc_camera_power_off`）流程：

1. 确认所有端口 handle 已关闭
2. 注销连接回调
3. 调用 `bk_usbh_hub_multiple_devices_power_down()` 关闭 `USB_UVC_DEVICE` 和 `USB_UVC_H26X_DEVICE`


### 6.4 回调函数

`bk_uvc_callback_t` 结构（`ap/include/components/bk_uvc_camera_types.h`）：


- `frame_malloc`：申请帧缓冲区，**禁止阻塞**

- `frame_complete`：一帧处理完成回调，**禁止阻塞**

- `state_change_cb`：设备连接/断开状态变化（`uvc_state_t`）

- `user_data`：用户自定义数据

示例工程中帧缓冲区通过 `bk_frame_buffer_malloc()` 申请，完成后 `bk_frame_buffer_free()` 释放。


### 6.5 分步调试 CLI

除 `uvc open/close` 外，还提供 `uvc_api` 子命令分步调试各 API：


```
uvc_api power_on
uvc_api new
uvc_api init
uvc_api open 1 640 480 mjpeg
uvc_api close
uvc_api deinit
uvc_api delete
uvc_api power_off
uvc_api suspend
uvc_api resume

```

默认配置宏：


```
#define MEDIA_UVC_MJPEG_864X480_30FPS_CONFIG() { \
    .format = BK_IMAGE_FORMAT_MJPEG, \
    .width = 864, .height = 480, .fps = 30, \
    .port = 1, .drop_num = 0, \
}

```


## 7. UVC 应用方案

1. UVC直接输出MJPEG图像，通过联合JPEG解码器进行解码，将MJPEG图像转换为YUV格式，再联合LCD显示器进行显示，且UVC输出的MJPEG联合WiFi模块，进行图传。
2. UVC直接输出MJPEG图像，通过联合JPEG解码器进行解码，将MJPEG图像转换为YUV格式，再通过联合H264编码器进行编码成H.264格式，再联合LCD显示器对解码后的图像进行显示，联合WiFi模块对编码的H.264图像进行图传。可以参考doobell方案。
3. UVC直接输出双码流H264&MJPEG图像（一个端口输出两种格式，或者两个端口分别输出H264和MJPEG），联合JPEG解码器进行解码，将MJPEG图像转换为YUV格式，再联合LCD显示器对解码后的图像进行显示，联合WiFi模块对UVC输出的H264图像进行图传。
