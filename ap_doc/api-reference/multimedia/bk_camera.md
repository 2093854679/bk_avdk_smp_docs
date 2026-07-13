# Camera



## 概述

BK7259 Camera 模块提供两条主要采集路径：


- **ISP 路径** — MIPI CSI / DVP Sensor，经 `bk_camera_bus` + `bk_camera_sensor` + `bk_isp_camera_*`

- **UVC 路径** — USB 摄像头，经 `bk_uvc_*`

使用指南与 CLI 调试：


- [摄像头总览](../../developer-guide/camera.md "../../developer-guide/camera.md")

- [ISP 图像信号处理](../../developer-guide/camera/isp.md "../../developer-guide/camera/isp.md")

- [MIPI CSI](../../developer-guide/camera/mipi_csi.md "../../developer-guide/camera/mipi_csi.md")

- [DVP](../../developer-guide/camera/dvp.md "../../developer-guide/camera/dvp.md")

- [UVC](../../developer-guide/camera/uvc.md "../../developer-guide/camera/uvc.md")

示例工程：


- [isp_example](../../examples/projects/multimedia/isp_example.md "../../examples/projects/multimedia/isp_example.md") — MIPI / DVP / ISP

- [uvc_example](../../examples/projects/multimedia/uvc_example.md "../../examples/projects/multimedia/uvc_example.md") — UVC 采集

- [uvc_display_example](../../examples/projects/multimedia/uvc_display_example.md "../../examples/projects/multimedia/uvc_display_example.md") — UVC 显示流水线

头文件：


- `ap/include/components/bk_camera_bus.h`

- `ap/include/components/bk_camera_sensor.h`

- `ap/include/components/bk_camera_isp_ctlr.h`

- `ap/include/components/bk_isp_camera.h`

- `ap/include/components/bk_uvc_camera.h`

备注

旧 API `bk_camera_dvp_ctlr_new` / `bk_camera_uvc_ctlr_new` **已移除**，请使用下方 ISP / UVC 控制器接口。


## ISP Camera 路径

典型调用流程（参考 `isp_func_test.c`）：

1. `bk_camera_bus_new` / `bk_camera_bus_enable`
2. `bk_camera_sensor_auto_detect`，DVP 或 CSI 端口
3. `bk_camera_isp_ctlr_new`
4. `bk_isp_camera_dev_init`，`bk_isp_camera_port_init`，`bk_isp_camera_channel_open`
5. `bk_isp_camera_open` 开始出图；ISR 通过 `bk_isp_camera_register_isr_callback` 注册
6. `bk_isp_camera_close`，`bk_isp_camera_channel_close`，`bk_isp_camera_deinit`，`bk_isp_camera_delete`


### 核心 API


**Camera 总线（I2C）**


- `bk_camera_bus_new` / `bk_camera_bus_enable` / `bk_camera_bus_disable` / `bk_camera_bus_delete`

- `bk_camera_bus_get`


**Sensor**


- `bk_camera_sensor_auto_detect` — 探测 DVP `DVP_CAMERA_PORT` 或 CSI `CSI_CAMERA_PORT`

- `bk_camera_sensor_init` / `bk_camera_sensor_set_format` / `bk_camera_sensor_query_support_formats`

- `bk_camera_sensor_destroy`


**ISP 控制器**


- `bk_camera_isp_ctlr_new`

- `bk_isp_camera_dev_init` / `bk_isp_camera_port_init` / `bk_isp_camera_port_change`

- `bk_isp_camera_channel_open` / `bk_isp_camera_channel_close` / `bk_isp_camera_channel_state_get`

- `bk_isp_camera_open` / `bk_isp_camera_close` / `bk_isp_camera_read`

- `bk_isp_camera_register_isr_callback` / `bk_isp_camera_deregister_isr_callback`

- `bk_isp_camera_ctlr_ioctl` / `bk_isp_camera_delete`

主要类型：`bk_camera_sensor_config_t`、`bk_isp_camera_ctlr_config_t`、`bk_isp_camera_channel_config_t`。


## UVC Camera 路径

典型调用流程（参考 `uvc_test.c`）：

1. USB Host 上电（应用 / Hub 驱动）
2. `bk_uvc_ctrl_new` — 注册 `bk_uvc_callback_t` 回调
3. `bk_uvc_init`，`bk_uvc_open`，传入 `bk_cam_uvc_config_t`
4. 在 `frame_complete` 回调中处理帧
5. `bk_uvc_close`，`bk_uvc_deinit`，`bk_uvc_delete`

可选：`bk_uvc_suspend` / `bk_uvc_resume` / `bk_uvc_ioctl`。


### 核心 API


- `bk_uvc_ctrl_new` / `bk_uvc_delete`

- `bk_uvc_init` / `bk_uvc_deinit`

- `bk_uvc_open` / `bk_uvc_close`

- `bk_uvc_suspend` / `bk_uvc_resume`

- `bk_uvc_ioctl`

- `bk_uvc_register_separate_packet_callback` — 双端点 MJPEG+H264 设备

主要类型：`bk_cam_uvc_config_t`、`bk_uvc_callback_t`、`bk_uvc_ctlr_handle_t`。

`bk_cam_uvc_config_t` 字段：`format`、`width`、`height`、`fps`、`port`、`drop_num`。


## 相关内存

帧缓冲使用 `bk_frame_buffer_*`，参见 [frame_buffer](bk_frame_buffer.md "bk_frame_buffer.md")。


## API Reference


### Camera Bus


#### Header File


- [bk_camera_bus.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_camera_bus.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_camera_bus.h")


#### Functions

[bk_camera_bus_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") *bk_camera_bus_new([bk_camera_bus_config_t](#_CPPv422bk_camera_bus_config_t "bk_camera_bus_config_t") *config)
:   Create a camera I2C bus instance.

    参数
    :   **config** – Bus configuration (pins, I2C ID, sensor address, etc.)

    返回
    :   Pointer to the bus instance, or NULL on failure

avdk_err_t bk_camera_bus_enable([bk_camera_bus_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") *bus)
:   Enable the camera I2C bus.

    参数
    :   **bus** – Bus instance from bk_camera_bus_new

    返回
    :   AVDK error code

avdk_err_t bk_camera_bus_disable([bk_camera_bus_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") *bus)
:   Disable the camera I2C bus.

    参数
    :   **bus** – Bus instance

    返回
    :   AVDK error code

avdk_err_t bk_camera_bus_delete([bk_camera_bus_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") *bus)
:   Delete the camera I2C bus instance.

    参数
    :   **bus** – Bus instance

    返回
    :   AVDK error code

[bk_camera_bus_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") *bk_camera_bus_get(void)
:   Get the global camera bus instance.

    返回
    :   Pointer to the bus instance, or NULL if not created


#### Structures

struct bk_camera_bus_ops_t

struct bk_camera_bus_config_t

struct bk_camera_bus_t


#### Enumerations

enum bk_camera_port_t
:   *Values:*

    enumerator DVP_CAMERA_PORT
    :   dvp port

    enumerator CSI_CAMERA_PORT
    :   csi port


### Camera Sensor


#### Header File


- [bk_camera_sensor.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_camera_sensor.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_camera_sensor.h")


#### Functions

avdk_err_t bk_camera_sensor_init([bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle)
:   Initialize the camera sensor.

    参数
    :   **handle** – Sensor handle

    返回
    :   Error code

void *bk_camera_sensor_get_sensor_object([bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle)
:   Get pointer to the sensor object.

    参数
    :   **handle** – Sensor handle

    返回
    :   Pointer to the sensor object

void *bk_camera_sensor_get_sensor_cfg([bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle)
:   Get pointer to the sensor configuration.

    参数
    :   **handle** – Sensor handle

    返回
    :   Pointer to the sensor configuration

avdk_err_t bk_camera_sensor_set_format([bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle, [bk_camera_sensor_format_t](#_CPPv425bk_camera_sensor_format_t "bk_camera_sensor_format_t") *format)
:   Set sensor format.

    参数
    :   - **handle** – Sensor handle

        - **format** – Format configuration

    返回
    :   Error code

avdk_err_t bk_camera_sensor_query_support_formats([bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle, [bk_camera_sensor_format_array_t](#_CPPv431bk_camera_sensor_format_array_t "bk_camera_sensor_format_array_t") *format_array)
:   Query supported sensor formats.

    参数
    :   - **handle** – Sensor handle

        - **format_array** – Output parameter for the format array

    返回
    :   Error code

[bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") bk_camera_sensor_auto_detect([bk_camera_sensor_config_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") *config, [bk_camera_port_t](#_CPPv416bk_camera_port_t "bk_camera_port_t") port)
:   Auto-detect the camera sensor.

    参数
    :   - **config** – Sensor configuration

        - **port** – Camera port

    返回
    :   Sensor handle, or NULL on failure

void bk_camera_sensor_destroy([bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle)
:   Release heap allocated by auto-detect ([bk_camera_csi_sensor_t](#structbk__camera__csi__sensor__t "#structbk__camera__csi__sensor__t") / [bk_camera_dvp_sensor_t](#structbk__camera__dvp__sensor__t "#structbk__camera__dvp__sensor__t") wrapper).

    参数
    :   **handle** – Handle from bk_camera_sensor_auto_detect or equivalent; NULL is a no-op.


#### Structures

struct bk_camera_sensor_config_t
:   Camera sensor configuration structure.

    Public Members

    uint8_t pin_reset
    :   Reset pin number

    uint8_t pin_pwdn
    :   Power-down pin number

    uint8_t pin_xclk
    :   Clock pin number

    [bk_camera_bus_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") *bus
    :   Pointer to camera bus interface

struct bk_camera_sensor_format_t
:   Camera sensor format configuration structure.

    Each entry describes one operating mode that the sensor natively supports. `output_pixel_fmt` declares the raw Bayer/pixel format the sensor emits in this mode (e.g. RGGB8 for DVP sensors, RGGB10 for MIPI raw sensors). It is a property of the sensor/mode itself, not an application-time choice, so device drivers must populate it inside their `xxx_format_array[]`.

    On the downstream side, applications should copy this value into `bk_isp_camera_ctlr_config_t.input_pixel_fmt` (sensor output == ISP input) after locating the matched mode via `bk_camera_sensor_query_support_formats()`.

    Public Members

    uint16_t width
    :   Image width (pixels)

    uint16_t height
    :   Image height (pixels)

    uint16_t fps
    :   Frame rate (frames/second)

    uint32_t xclk
    :   External clock frequency (Hz)

    bk_pixel_format_t output_pixel_fmt
    :   Sensor output pixel format (e.g. RGGB8 / RGGB10)

struct bk_camera_sensor_format_array_t
:   Supported format array structure for camera sensor.

    Public Members

    uint32_t size
    :   Size of the format array

    const [bk_camera_sensor_format_t](#_CPPv425bk_camera_sensor_format_t "bk_camera_sensor_format_t") *format_array
    :   Pointer to the format array

struct bk_camera_sensor_ctlr_t
:   Camera sensor controller operations structure.

    Public Members

    int (*init)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller)
    :   Initialize CSI sensor

    int (*set_format)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller, [bk_camera_sensor_format_t](#_CPPv425bk_camera_sensor_format_t "bk_camera_sensor_format_t") *format)
    :   Set sensor resolution

    int (*power_down)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller)
    :   Power down or reset the sensor

    int (*reg_ctrl)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller, uint8_t cmd, uint16_t addr, uint8_t val)
    :   Register control function

    void *(*get_sensor_object)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller)
    :   Get pointer to sensor object

    void *(*get_sensor_cfg)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller)
    :   Get pointer to sensor configuration

    avdk_err_t (*query_support_formats)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller, [bk_camera_sensor_format_array_t](#_CPPv431bk_camera_sensor_format_array_t "bk_camera_sensor_format_array_t") *format_array)
    :   Query supported formats

struct bk_camera_csi_sensor_t
:   CSI camera sensor structure.

    Public Members

    const void *isp_pub_attr
    :   Pointer to ISP public attributes

    const void *sensor_config
    :   Pointer to sensor-specific configuration

    [bk_camera_sensor_config_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") config
    :   Sensor configuration

    [bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") ops
    :   Sensor controller operations

struct bk_camera_dvp_sensor_t
:   DVP camera sensor structure.

    Public Members

    const void *isp_pub_attr
    :   Pointer to ISP public attributes

    const void *sensor_config
    :   Pointer to sensor-specific configuration

    [bk_camera_sensor_config_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") config
    :   Sensor configuration

    [bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") ops
    :   Sensor controller operations

struct bk_camera_sensor_detect_func_t
:   Camera sensor detection function structure.

    Public Members

    [bk_camera_port_t](#_CPPv416bk_camera_port_t "bk_camera_port_t") port
    :   Camera port

    avdk_err_t (*detect)([bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") *handle, [bk_camera_sensor_config_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") *config)
    :   Detection function pointer


#### Macros

_SECTION_ATTR_IMPL(SECTION, COUNTER)
:   Section attribute macro implementation.

    参数
    :   - **SECTION** – Section name

        - **COUNTER** – Counter

_CPIMTER_STRINGIFY(COUNTER)
:   Stringify macro.

    参数
    :   - **COUNTER** – Counter

BK_CAMERA_SENSOR_DETECT_SECTION(f, p)
:   Camera sensor detection function section registration macro.

    This macro registers a sensor detection function into a dedicated section, enabling the system to automatically discover and run detection routines.

    参数
    :   - **f** – Detection function name

        - **p** – Port type


#### Type Definitions

typedef struct [bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *bk_camera_sensor_handle_t


### ISP Controller


#### Header File


- [bk_camera_isp_ctlr.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_camera_isp_ctlr.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_camera_isp_ctlr.h")


#### Functions

avdk_err_t bk_camera_isp_ctlr_new(bk_isp_camera_ctlr_handle_t *handle)
:   Create a new ISP camera controller instance.

    参数
    :   **handle** – Output pointer that receives the controller handle

    返回
    :   AVDK error code


#### Structures

struct bk_isp_camera_ctlr_config_t

struct bk_camera_isp_ctlr_t


#### Macros

BK_ISP_INPUT_TYPE_CSI_SENSOR

BK_ISP_INPUT_TYPE_DVP_SENSOR

BK_ISP_MODE_BT656

BK_ISP_MODE_BT601

BK_ISP_MODE_RAW

BK_ISP_HDR_MODE_LINEAR

BK_ISP_HDR_MODE_ISP_STICH

BK_ISP_HDR_MODE_SENSOR_STICH

ISP_CHANNEL_INSTANCE_MAX


#### Type Definitions

typedef uint16_t bk_isp_input_type_t

typedef uint16_t bk_isp_mode_t

typedef uint16_t bk_isp_hdr_mode_t


### ISP Camera


#### Header File


- [bk_isp_camera.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_isp_camera.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_isp_camera.h")


#### Functions

avdk_err_t bk_isp_camera_dev_init(bk_isp_camera_ctlr_handle_t handle)
:   Initialize ISP camera controller device-level resources.

    参数
    :   **handle** – ISP camera controller handle from bk_camera_isp_ctlr_new

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_port_init(bk_isp_camera_ctlr_handle_t handle, void *config)
:   Configure the active ISP port (DVP or CSI)

    参数
    :   - **handle** – ISP camera controller handle

        - **config** – Pointer to [bk_isp_camera_ctlr_config_t](#structbk__isp__camera__ctlr__config__t "#structbk__isp__camera__ctlr__config__t")

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_port_change(bk_isp_camera_ctlr_handle_t handle)
:   Switch or update the active ISP port configuration.

    参数
    :   **handle** – ISP camera controller handle

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_deinit(bk_isp_camera_ctlr_handle_t handle)
:   Deinitialize ISP camera controller and release device-level resources.

    参数
    :   **handle** – ISP camera controller handle

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_open(bk_isp_camera_ctlr_handle_t handle, void *parameter)
:   Start ISP camera streaming.

    参数
    :   - **handle** – ISP camera controller handle

        - **parameter** – Optional open parameters (implementation-specific, may be NULL)

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_close(bk_isp_camera_ctlr_handle_t handle)
:   Stop ISP camera streaming.

    参数
    :   **handle** – ISP camera controller handle

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_read(bk_isp_camera_ctlr_handle_t handle, uint16_t id, uint8_t *frame, uint32_t size, uint32_t timeout)
:   Read one frame from the specified channel.

    参数
    :   - **handle** – ISP camera controller handle

        - **id** – Channel identifier

        - **frame** – Output buffer for frame data

        - **size** – Size of the output buffer in bytes

        - **timeout** – Read timeout in milliseconds

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_register_isr_callback(bk_isp_camera_ctlr_handle_t handle, bk_camera_isr_type_t type, bk_camera_isr_t cb, void *arg)
:   Register an ISP interrupt callback.

    参数
    :   - **handle** – ISP camera controller handle

        - **type** – ISR event type

        - **cb** – Callback function

        - **arg** – User argument passed to the callback

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_deregister_isr_callback(bk_isp_camera_ctlr_handle_t handle, bk_camera_isr_type_t type, void *arg)
:   Deregister an ISP interrupt callback.

    参数
    :   - **handle** – ISP camera controller handle

        - **type** – ISR event type

        - **arg** – User argument that was registered with the callback

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_ctlr_ioctl(bk_isp_camera_ctlr_handle_t handle, bk_cam_interface_ioctl_t ioctl, void *arg)
:   Issue an IOCTL command on the ISP camera controller.

    参数
    :   - **handle** – ISP camera controller handle

        - **ioctl** – IOCTL command identifier

        - **arg** – Command-specific argument

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_delete(bk_isp_camera_ctlr_handle_t handle)
:   Destroy the ISP camera controller instance.

    参数
    :   **handle** – ISP camera controller handle

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_channel_open(bk_isp_camera_ctlr_handle_t handle, uint8_t channel, [bk_isp_camera_channel_config_t](#_CPPv430bk_isp_camera_channel_config_t "bk_isp_camera_channel_config_t") *config)
:   Open an ISP output channel.

    参数
    :   - **handle** – ISP camera controller handle

        - **channel** – Channel index

        - **config** – Channel configuration

    返回
    :   AVDK error code

avdk_err_t bk_isp_camera_channel_close(bk_isp_camera_ctlr_handle_t handle, uint8_t channel)
:   Close an ISP output channel.

    参数
    :   - **handle** – ISP camera controller handle

        - **channel** – Channel index

    返回
    :   AVDK error code

bk_isp_camera_channel_state_t bk_isp_camera_channel_state_get(bk_isp_camera_ctlr_handle_t handle, uint8_t channel)
:   Get the state of an ISP output channel.

    参数
    :   - **handle** – ISP camera controller handle

        - **channel** – Channel index

    返回
    :   Channel state


### ISP Camera Types

struct bk_isp_camera_channel_config_t
:   Camera ISP instance configuration structure.

    Public Members

    uint8_t buf_cnt
    :   Number of frame buffers

    uint8_t port_id
    :   Port identifier

    uint8_t enable_flexa
    :   Enable Flexa: 0 - disable, 1 - enable

    uint8_t work_mode
    :   Operating mode: 0 - frame mode, 1 - SFW Flexa mode

    uint16_t width
    :   Frame width in pixels

    uint16_t height
    :   Frame height in pixels

    uint16_t format
    :   Pixel format

struct bk_camera_ctlr_t
:   Camera controller operation table.

    Public Members

    avdk_err_t (*dev_init)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller)
    :   Initialize controller level resources (clock, GPIO, etc.)

    avdk_err_t (*port_init)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller, void *config)
    :   Configure a physical port according to the supplied configuration

    avdk_err_t (*port_change)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller)
    :   Switch the active port or update link configuration dynamically

    avdk_err_t (*open)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller, void *parameter)
    :   Open the controller for streaming with the specified parameters

    avdk_err_t (*read)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller, uint16_t id, uint8_t *frame, uint32_t size, uint32_t timeout)
    :   Read a frame

    avdk_err_t (*close)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller)
    :   Stop streaming and release transient resources

    avdk_err_t (*deinit)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller)
    :   Deinitialize controller level resources

    avdk_err_t (*suspend)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller)
    :   Suspend the controller for low-power operation

    avdk_err_t (*resume)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller)
    :   Resume the controller after suspension

    avdk_err_t (*ioctl)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller, bk_cam_interface_ioctl_t ioctl, void *arg)
    :   Issue controller specific IOCTL commands

    avdk_err_t (*del)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller)
    :   Destroy the controller object and free memory

    avdk_err_t (*register_isr_callback)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller, bk_camera_isr_type_t type, bk_camera_isr_t cb, void *arg)
    :   Register ISP interrupt service routine callback

    avdk_err_t (*deregister_isr_callback)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller, bk_camera_isr_type_t type, void *arg)
    :   Deregister ISP interrupt service routine callback

    avdk_err_t (*channel_open)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller, uint8_t channel, [bk_isp_camera_channel_config_t](#_CPPv430bk_isp_camera_channel_config_t "bk_isp_camera_channel_config_t") *config)
    :   Open a channel

    avdk_err_t (*channel_close)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller, uint8_t channel)
    :   Close a channel

    bk_isp_camera_channel_state_t (*channel_state_get)([bk_camera_ctlr_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") *controller, uint8_t channel)
    :   Get a channel state

enum sensor_id_t
:   Enumeration of sensor identifiers.


    *Values:*

    enumerator ID_UNKNOW
    :   Unknown sensor

    enumerator ID_PAS6329
    :   PAS6329 sensor

    enumerator ID_OV7670
    :   OV7670 sensor

    enumerator ID_PAS6375
    :   PAS6375 sensor

    enumerator ID_GC0328C
    :   GC0328C sensor

    enumerator ID_BF2013
    :   BF2013 sensor

    enumerator ID_GC0308C
    :   GC0308C sensor

    enumerator ID_HM1055
    :   HM1055 sensor

    enumerator ID_GC2145
    :   GC2145 sensor

    enumerator ID_OV2640
    :   OV2640 sensor

    enumerator ID_GC0308
    :   GC0308 sensor

    enumerator ID_TVP5150
    :   TVP5150 sensor

    enumerator ID_SC101
    :   SC101 sensor

    enumerator ID_GC2053
    :   GC2053 sensor

    enumerator ID_GC4653
    :   GC4653 sensor

    enumerator ID_OV2775
    :   OV2775 sensor

    enumerator ID_GC2053D
    :   GC2053D sensor


### DVP Camera Types


#### Header File


- [bk_dvp_camera_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_dvp_camera_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_dvp_camera_types.h")


#### Structures

struct dvp_sensor_config_t
:   dvp sensor configure

    Public Members

    char *name
    :   sensor name

    mclk_freq_t clk
    :   sensor work clk in config fps and ppi

    sync_level_t vsync
    :   sensor vsync active level

    sync_level_t hsync
    :   sensor hsync active level

    uint16_t id
    :   sensor type, sensor_id_t

    uint16_t address
    :   sensor write register address by i2c

    avdk_err_t (*detect)([bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") *handle, [bk_camera_sensor_config_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") *config)
    :   auto detect used dvp sensor

    avdk_err_t (*init)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller)
    :   init dvp sensor

    avdk_err_t (*set_ppi)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller, uint16_t width, uint16_t height)
    :   set resolution of sensor

    avdk_err_t (*set_fps)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller, uint16_t fps)
    :   set fps of sensor

    avdk_err_t (*power_down)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller)
    :   power down or reset of sensor

struct bk_dvp_config_t

struct bk_dvp_callback_t


### CSI Camera Types


#### Header File


- [bk_csi_camera_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_csi_camera_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_csi_camera_types.h")


#### Structures

struct csi_sensor_config_t
:   csi sensor configure

    Public Members

    char *name
    :   sensor name

    mclk_freq_t clk
    :   sensor work clk in config fps and ppi

    sync_level_t vsync
    :   sensor vsync active level

    sync_level_t hsync
    :   sensor hsync active level

    uint16_t id
    :   sensor type, sensor_id_t

    uint16_t address
    :   sensor write register address by i2c

    avdk_err_t (*detect)([bk_camera_sensor_handle_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") *handle, [bk_camera_sensor_config_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") *config)
    :   auto detect used csi sensor

    avdk_err_t (*init)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller)
    :   init csi sensor

    avdk_err_t (*set_ppi)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller, uint16_t width, uint16_t height)
    :   set resolution of sensor

    avdk_err_t (*set_fps)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller, uint16_t fps)
    :   set fps of sensor

    avdk_err_t (*power_down)([bk_camera_sensor_ctlr_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") *controller)
    :   power down or reset of sensor

struct bk_csi_config_t

struct bk_csi_callback_t


### UVC Camera


#### Header File


- [bk_uvc_camera.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_uvc_camera.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_uvc_camera.h")


#### Functions

avdk_err_t bk_uvc_ctrl_new([bk_uvc_ctlr_handle_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") *handle, const [bk_uvc_callback_t](#_CPPv417bk_uvc_callback_t "bk_uvc_callback_t") *callbacks)
:   Create a new UVC controller instance.

    Allocates and initialises an abstract controller object. Callbacks are stored internally and invoked when frames are allocated, released, or when the UVC device changes state.

    参数
    :   - **handle** – **[out]** Pointer that receives the newly created controller handle

        - **callbacks** – **[in]** Application provided callback hooks (frame allocation, completion, state changes)

    返回
    :   - AVDK_ERR_OK: controller created successfully

        - others: other errors.

avdk_err_t bk_uvc_init([bk_uvc_ctlr_handle_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Initialize the UVC controller hardware and resources.

    Must be called before opening a device. The controller configures clocks, endpoints and any other hardware level state needed to communicate with a UVC camera.

    参数
    :   **handle** – Controller handle obtained from bk_uvc_ctrl_new

    返回
    :   - AVDK_ERR_OK: initialization success

        - others: other errors.

avdk_err_t bk_uvc_deinit([bk_uvc_ctlr_handle_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Deinitialize the UVC controller and release resources.

    Reverses bk_uvc_init by powering down hardware resources and freeing controller level allocations. The controller can be initialised again after this call.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK_ERR_OK: deinitialisation success

        - others: other errors.

avdk_err_t bk_uvc_open([bk_uvc_ctlr_handle_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle, [bk_cam_uvc_config_t](#_CPPv419bk_cam_uvc_config_t "bk_cam_uvc_config_t") *config)
:   Open a UVC device using the provided configuration.

    Applies stream parameters such as image format, resolution and frame rate, then arms the controller to start receiving data from the device.

    参数
    :   - **handle** – Controller handle

        - **config** – Runtime configuration describing format, resolution, FPS, etc.

    返回
    :   - AVDK_ERR_OK: device opened successfully

        - others: other errors.

avdk_err_t bk_uvc_close([bk_uvc_ctlr_handle_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Close the currently opened UVC device.

    Stops streaming, flushes pending transfers and releases device specific resources. After calling close, the controller can be opened again with a new configuration.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK_ERR_OK: device closed successfully

        - others: other errors.

avdk_err_t bk_uvc_suspend([bk_uvc_ctlr_handle_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Suspend the UVC controller (used for low-power management)

    Places the controller in a low-power state. Streaming must be stopped prior to suspension.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK_ERR_OK: controller suspended successfully

        - others: other errors.

avdk_err_t bk_uvc_resume([bk_uvc_ctlr_handle_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Resume the UVC controller after a suspend operation.

    Restores controller state saved during suspend so that streaming can be restarted.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK_ERR_OK: controller resumed successfully

        - others: other errors.

avdk_err_t bk_uvc_ioctl([bk_uvc_ctlr_handle_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle, uint32_t event, void *arg)
:   Issue a controller-specific IOCTL command.

    Provides access to extended control paths that are not covered by the standard open/close/suspend/resume APIs.

    参数
    :   - **handle** – Controller handle

        - **event** – IOCTL command identifier

        - **arg** – Optional argument pointer associated with the command

    返回
    :   - AVDK_ERR_OK: IOCTL executed successfully

        - others: other errors.

avdk_err_t bk_uvc_delete([bk_uvc_ctlr_handle_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Destroy a controller instance created by bk_uvc_ctrl_new.

    This API releases the handle and any residual resources created by the controller constructor.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK_ERR_OK: deletion success

        - others: other errors.

avdk_err_t bk_uvc_register_separate_packet_callback([uvc_separate_config_t](#_CPPv421uvc_separate_config_t "uvc_separate_config_t") *cb)
:   register separate packet cb

    This API will register separate packet data, some uvc device a endpoint will output mjpeg and h264 data meantime, need register this callback

    参数
    :   **cb** – @attation 1. this api called before bk_uvc_init, not all uvc need register

    返回
    :   - AVDK_ERR_OK: set success

        - others: other errors.


### UVC Camera Types


#### Header File


- [bk_uvc_camera_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_uvc_camera_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_uvc_camera_types.h")


#### Structures

struct uvc_separate_info_t
:   Auxiliary information returned by a frame separation callback.

    When a JPEG or H.26x frame spans multiple packets, the separation callback can report how much valid data remains to be processed.


    - data_len: number of valid bytes observed in the current packet.

    - data_off: pointer to the first valid byte within the packet buffer.

struct bk_cam_uvc_config_t
:   UVC camera runtime configuration parameters.

struct bk_uvc_callback_t
:   Callback hooks provided by the application to the UVC controller.

struct bk_uvc_ctlr

struct uvc_separate_config_t
:   Per-device callbacks used to separate and process UVC payloads.


#### Macros

UVC_PORT_MAX
:   Maximum number of UVC ports.

    This macro defines the maximum number of UVC ports supported, based on the USB host hub maximum external ports configuration.

MEDIA_UVC_MJPEG_864X480_30FPS_CONFIG()


#### Type Definitions

typedef struct [bk_uvc_ctlr](#_CPPv411bk_uvc_ctlr "bk_uvc_ctlr") *bk_uvc_ctlr_handle_t

typedef struct [bk_uvc_ctlr](#_CPPv411bk_uvc_ctlr "bk_uvc_ctlr") bk_uvc_ctlr_t


#### Enumerations

enum uvc_state_t
:   Enumeration of UVC connection states.


    *Values:*

    enumerator UVC_CONNECTED
    :   Device is connected and streaming capable

    enumerator UVC_DISCONNECTED
    :   Device has been disconnected
