---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/multimedia/bk_camera.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="camera"></a>

# Camera

<a id="id1"></a>

## 概述

BK7259 Camera 模块提供两条主要采集路径：

- **ISP 路径** — MIPI CSI / DVP Sensor，经 `bk_camera_bus` \+ `bk_camera_sensor` \+ `bk_isp_camera_*`
- **UVC 路径** — USB 摄像头，经 `bk_uvc_*`

使用指南与 CLI 调试：

- [摄像头总览](../../developer-guide/camera.md)
- [ISP 图像信号处理](../../developer-guide/camera/isp.md)
- [MIPI CSI](../../developer-guide/camera/mipi_csi.md)
- [DVP](../../developer-guide/camera/dvp.md)
- [UVC](../../developer-guide/camera/uvc.md)

示例工程：

- [isp\_example](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/isp_example/index.html) — MIPI / DVP / ISP
- [uvc\_example](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/uvc_example/index.html) — UVC 采集
- [uvc\_display\_example](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/uvc_display_example/index.html) — UVC 显示流水线

头文件：

- `ap/include/components/bk_camera_bus.h`
- `ap/include/components/bk_camera_sensor.h`
- `ap/include/components/bk_camera_isp_ctlr.h`
- `ap/include/components/bk_isp_camera.h`
- `ap/include/components/bk_uvc_camera.h`

备注

旧 API `bk_camera_dvp_ctlr_new` / `bk_camera_uvc_ctlr_new` **已移除**，请使用下方 ISP / UVC 控制器接口。

<a id="isp-camera"></a>

## ISP Camera 路径

典型调用流程（参考 `isp_func_test.c`）：

1. `bk_camera_bus_new` / `bk_camera_bus_enable`
2. `bk_camera_sensor_auto_detect`，DVP 或 CSI 端口
3. `bk_camera_isp_ctlr_new`
4. `bk_isp_camera_dev_init`，`bk_isp_camera_port_init`，`bk_isp_camera_channel_open`
5. `bk_isp_camera_open` 开始出图；ISR 通过 `bk_isp_camera_register_isr_callback` 注册
6. `bk_isp_camera_close`，`bk_isp_camera_channel_close`，`bk_isp_camera_deinit`，`bk_isp_camera_delete`

<a id="api"></a>

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

<a id="uvc-camera"></a>

## UVC Camera 路径

典型调用流程（参考 `uvc_test.c`）：

1. USB Host 上电（应用 / Hub 驱动）
2. `bk_uvc_ctrl_new` — 注册 `bk_uvc_callback_t` 回调
3. `bk_uvc_init`，`bk_uvc_open`，传入 `bk_cam_uvc_config_t`
4. 在 `frame_complete` 回调中处理帧
5. `bk_uvc_close`，`bk_uvc_deinit`，`bk_uvc_delete`

可选：`bk_uvc_suspend` / `bk_uvc_resume` / `bk_uvc_ioctl`。

<a id="id3"></a>

### 核心 API

- `bk_uvc_ctrl_new` / `bk_uvc_delete`
- `bk_uvc_init` / `bk_uvc_deinit`
- `bk_uvc_open` / `bk_uvc_close`
- `bk_uvc_suspend` / `bk_uvc_resume`
- `bk_uvc_ioctl`
- `bk_uvc_register_separate_packet_callback` — 双端点 MJPEG\+H264 设备

主要类型：`bk_cam_uvc_config_t`、`bk_uvc_callback_t`、`bk_uvc_ctlr_handle_t`。

`bk_cam_uvc_config_t` 字段：`format`、`width`、`height`、`fps`、`port`、`skip_frames`。

<a id="id4"></a>

## 相关内存

帧缓冲使用 `bk_frame_buffer_*`，参见 [frame\_buffer](bk_frame_buffer.md)。

<a id="api-reference"></a>

## API Reference

<a id="camera-bus"></a>

### Camera Bus

<a id="header-file"></a>

#### Header File

- [bk\_camera\_bus.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_camera_bus.h)

<a id="functions"></a>

#### Functions

<a id="_CPPv417bk_camera_bus_newP22bk_camera_bus_config_t"></a>

<a id="_CPPv317bk_camera_bus_newP22bk_camera_bus_config_t"></a> <a id="_CPPv217bk_camera_bus_newP22bk_camera_bus_config_t"></a> <a id="bk_camera_bus_new__bk_camera_bus_config_tP"></a> <a id="bk__camera__bus_8h_1aee861af4a37e1f713aa279d976ec90b8"></a> [bk\_camera\_bus\_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") \*bk\_camera\_bus\_new([bk\_camera\_bus\_config\_t](#_CPPv422bk_camera_bus_config_t "bk_camera_bus_config_t") \*config)
:   Create a camera I2C bus instance.

    参数
    :   **config** – Bus configuration (pins, I2C ID, sensor address, etc.)

    返回
    :   Pointer to the bus instance, or NULL on failure

<a id="_CPPv420bk_camera_bus_enableP15bk_camera_bus_t"></a>

<a id="_CPPv320bk_camera_bus_enableP15bk_camera_bus_t"></a> <a id="_CPPv220bk_camera_bus_enableP15bk_camera_bus_t"></a> <a id="bk_camera_bus_enable__bk_camera_bus_tP"></a> <a id="bk__camera__bus_8h_1a2cca7c69831f1513df809f5e51bbc9fc"></a> avdk\_err\_t bk\_camera\_bus\_enable([bk\_camera\_bus\_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") \*bus)
:   Enable the camera I2C bus.

    参数
    :   **bus** – Bus instance from bk\_camera\_bus\_new

    返回
    :   AVDK error code

<a id="_CPPv421bk_camera_bus_disableP15bk_camera_bus_t"></a>

<a id="_CPPv321bk_camera_bus_disableP15bk_camera_bus_t"></a> <a id="_CPPv221bk_camera_bus_disableP15bk_camera_bus_t"></a> <a id="bk_camera_bus_disable__bk_camera_bus_tP"></a> <a id="bk__camera__bus_8h_1a304c4946af9910e043b7ada4f2b6576d"></a> avdk\_err\_t bk\_camera\_bus\_disable([bk\_camera\_bus\_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") \*bus)
:   Disable the camera I2C bus.

    参数
    :   **bus** – Bus instance

    返回
    :   AVDK error code

<a id="_CPPv420bk_camera_bus_deleteP15bk_camera_bus_t"></a>

<a id="_CPPv320bk_camera_bus_deleteP15bk_camera_bus_t"></a> <a id="_CPPv220bk_camera_bus_deleteP15bk_camera_bus_t"></a> <a id="bk_camera_bus_delete__bk_camera_bus_tP"></a> <a id="bk__camera__bus_8h_1a915c65a4cf98c8aea7c5b636426fe1cd"></a> avdk\_err\_t bk\_camera\_bus\_delete([bk\_camera\_bus\_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") \*bus)
:   Delete the camera I2C bus instance.

    参数
    :   **bus** – Bus instance

    返回
    :   AVDK error code

<a id="_CPPv417bk_camera_bus_getv"></a>

<a id="_CPPv317bk_camera_bus_getv"></a> <a id="_CPPv217bk_camera_bus_getv"></a> <a id="bk_camera_bus_get__void"></a> <a id="bk__camera__bus_8h_1ac3123744affd3fc9a208ad0b7ae18924"></a> [bk\_camera\_bus\_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") \*bk\_camera\_bus\_get(void)
:   Get the global camera bus instance.

    返回
    :   Pointer to the bus instance, or NULL if not created

<a id="structures"></a>

#### Structures

<a id="_CPPv419bk_camera_bus_ops_t"></a>

<a id="_CPPv319bk_camera_bus_ops_t"></a> <a id="_CPPv219bk_camera_bus_ops_t"></a> <a id="bk_camera_bus_ops_t"></a> <a id="structbk__camera__bus__ops__t"></a> struct bk\_camera\_bus\_ops\_t

<a id="_CPPv422bk_camera_bus_config_t"></a>

<a id="_CPPv322bk_camera_bus_config_t"></a> <a id="_CPPv222bk_camera_bus_config_t"></a> <a id="bk_camera_bus_config_t"></a> <a id="structbk__camera__bus__config__t"></a> struct bk\_camera\_bus\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_camera_bus_config_t8pin_xclkE"></a>

    <a id="_CPPv3N22bk_camera_bus_config_t8pin_xclkE"></a> <a id="_CPPv2N22bk_camera_bus_config_t8pin_xclkE"></a> <a id="bk_camera_bus_config_t::pin_xclk__uint8_t"></a> <a id="structbk__camera__bus__config__t_1aebd4e619c06ddfb84daa91bd2c0e357a"></a> uint8\_t pin\_xclk
    :   Sensor MCLK GPIO; BK\_CAMERA\_PIN\_INVALID \= no SoC MCLK

<a id="_CPPv415bk_camera_bus_t"></a>

<a id="_CPPv315bk_camera_bus_t"></a> <a id="_CPPv215bk_camera_bus_t"></a> <a id="bk_camera_bus_t"></a> <a id="structbk__camera__bus__t"></a> struct bk\_camera\_bus\_t

<a id="macros"></a>

#### Macros

<a id="c.BK_CAMERA_PIN_INVALID"></a>

<a id="bk__camera__bus_8h_1a6173b64a0f2372b2f54c536b4c88a252"></a> BK\_CAMERA\_PIN\_INVALID

<a id="type-definitions"></a>

#### Type Definitions

<a id="bk__camera__bus_8h_1a3108cae64de6634867fef6b92afb7116"></a> typedef struct [bk\_camera\_bus\_ops\_t](#_CPPv419bk_camera_bus_ops_t "bk_camera_bus_ops_t") bk\_camera\_bus\_ops\_t

<a id="bk__camera__bus_8h_1a9e9ff70a09419dca188cc9291be6a42c"></a> typedef struct [bk\_camera\_bus\_config\_t](#_CPPv422bk_camera_bus_config_t "bk_camera_bus_config_t") bk\_camera\_bus\_config\_t

<a id="bk__camera__bus_8h_1ace07788967d179c91f04def002885102"></a> typedef struct [bk\_camera\_bus\_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") bk\_camera\_bus\_t

<a id="enumerations"></a>

#### Enumerations

<a id="_CPPv416bk_camera_port_t"></a>

<a id="_CPPv316bk_camera_port_t"></a> <a id="_CPPv216bk_camera_port_t"></a> <a id="bk__camera__bus_8h_1a8762ad4694ff878ae30de88f2dc5378f"></a> enum bk\_camera\_port\_t
:   *Values:*

    <a id="_CPPv4N16bk_camera_port_t15DVP_CAMERA_PORTE"></a>

    <a id="_CPPv3N16bk_camera_port_t15DVP_CAMERA_PORTE"></a> <a id="_CPPv2N16bk_camera_port_t15DVP_CAMERA_PORTE"></a> <a id="bk__camera__bus_8h_1a8762ad4694ff878ae30de88f2dc5378fa9a4c37cf6cd601df33746c0b0467623c"></a> enumerator DVP\_CAMERA\_PORT
    :   dvp port

    <a id="_CPPv4N16bk_camera_port_t15CSI_CAMERA_PORTE"></a>

    <a id="_CPPv3N16bk_camera_port_t15CSI_CAMERA_PORTE"></a> <a id="_CPPv2N16bk_camera_port_t15CSI_CAMERA_PORTE"></a> <a id="bk__camera__bus_8h_1a8762ad4694ff878ae30de88f2dc5378fae74289f74b13fe689010d4b59a1bea9e"></a> enumerator CSI\_CAMERA\_PORT
    :   csi port

<a id="camera-sensor"></a>

### Camera Sensor

<a id="id5"></a>

#### Header File

- [bk\_camera\_sensor.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_camera_sensor.h)

<a id="id6"></a>

#### Functions

<a id="_CPPv421bk_camera_sensor_init25bk_camera_sensor_handle_t"></a>

<a id="_CPPv321bk_camera_sensor_init25bk_camera_sensor_handle_t"></a> <a id="_CPPv221bk_camera_sensor_init25bk_camera_sensor_handle_t"></a> <a id="bk_camera_sensor_init__bk_camera_sensor_handle_t"></a> <a id="bk__camera__sensor_8h_1a9f2fedef048d6e6bd956a0ea27b50ef9"></a> avdk\_err\_t bk\_camera\_sensor\_init([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle)
:   Initialize the camera sensor.

    参数
    :   **handle** – Sensor handle

    返回
    :   Error code

<a id="_CPPv434bk_camera_sensor_get_sensor_object25bk_camera_sensor_handle_t"></a>

<a id="_CPPv334bk_camera_sensor_get_sensor_object25bk_camera_sensor_handle_t"></a> <a id="_CPPv234bk_camera_sensor_get_sensor_object25bk_camera_sensor_handle_t"></a> <a id="bk_camera_sensor_get_sensor_object__bk_camera_sensor_handle_t"></a> <a id="bk__camera__sensor_8h_1a3667bb4fb059ff926cd5498c5be0bb9a"></a> void \*bk\_camera\_sensor\_get\_sensor\_object([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle)
:   Get pointer to the sensor object.

    参数
    :   **handle** – Sensor handle

    返回
    :   Pointer to the sensor object

<a id="_CPPv431bk_camera_sensor_get_sensor_cfg25bk_camera_sensor_handle_t"></a>

<a id="_CPPv331bk_camera_sensor_get_sensor_cfg25bk_camera_sensor_handle_t"></a> <a id="_CPPv231bk_camera_sensor_get_sensor_cfg25bk_camera_sensor_handle_t"></a> <a id="bk_camera_sensor_get_sensor_cfg__bk_camera_sensor_handle_t"></a> <a id="bk__camera__sensor_8h_1a946df9e85a68a456de2f37b387928fbb"></a> void \*bk\_camera\_sensor\_get\_sensor\_cfg([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle)
:   Get pointer to the sensor configuration.

    参数
    :   **handle** – Sensor handle

    返回
    :   Pointer to the sensor configuration

<a id="_CPPv427bk_camera_sensor_set_format25bk_camera_sensor_handle_tP25bk_camera_sensor_format_t"></a>

<a id="_CPPv327bk_camera_sensor_set_format25bk_camera_sensor_handle_tP25bk_camera_sensor_format_t"></a> <a id="_CPPv227bk_camera_sensor_set_format25bk_camera_sensor_handle_tP25bk_camera_sensor_format_t"></a> <a id="bk_camera_sensor_set_format__bk_camera_sensor_handle_t.bk_camera_sensor_format_tP"></a> <a id="bk__camera__sensor_8h_1a3101c7d18efa047adbf43ac66ea66c31"></a> avdk\_err\_t bk\_camera\_sensor\_set\_format([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle, [bk\_camera\_sensor\_format\_t](#_CPPv425bk_camera_sensor_format_t "bk_camera_sensor_format_t") \*format)
:   Set sensor format.

    参数
    :   - **handle** – Sensor handle
        - **format** – Format configuration

    返回
    :   Error code

<a id="_CPPv428bk_camera_sensor_set_hmirror25bk_camera_sensor_handle_tb"></a>

<a id="_CPPv328bk_camera_sensor_set_hmirror25bk_camera_sensor_handle_tb"></a> <a id="_CPPv228bk_camera_sensor_set_hmirror25bk_camera_sensor_handle_tb"></a> <a id="bk_camera_sensor_set_hmirror__bk_camera_sensor_handle_t.b"></a> <a id="bk__camera__sensor_8h_1ac2846f94c97e23f62eb680a471c761ac"></a> avdk\_err\_t bk\_camera\_sensor\_set\_hmirror([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle, bool enable)
:   Set horizontal mirror on the sensor output.

    返回
    :   AVDK\_ERR\_OK on success, AVDK\_ERR\_UNSUPPORTED if the sensor has no hook.

<a id="_CPPv426bk_camera_sensor_set_vflip25bk_camera_sensor_handle_tb"></a>

<a id="_CPPv326bk_camera_sensor_set_vflip25bk_camera_sensor_handle_tb"></a> <a id="_CPPv226bk_camera_sensor_set_vflip25bk_camera_sensor_handle_tb"></a> <a id="bk_camera_sensor_set_vflip__bk_camera_sensor_handle_t.b"></a> <a id="bk__camera__sensor_8h_1a02aed8b9186e2dee0a438ac5490ddc01"></a> avdk\_err\_t bk\_camera\_sensor\_set\_vflip([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle, bool enable)
:   Set vertical flip on the sensor output.

    返回
    :   AVDK\_ERR\_OK on success, AVDK\_ERR\_UNSUPPORTED if the sensor has no hook.

<a id="_CPPv438bk_camera_sensor_query_support_formats25bk_camera_sensor_handle_tP31bk_camera_sensor_format_array_t"></a>

<a id="_CPPv338bk_camera_sensor_query_support_formats25bk_camera_sensor_handle_tP31bk_camera_sensor_format_array_t"></a> <a id="_CPPv238bk_camera_sensor_query_support_formats25bk_camera_sensor_handle_tP31bk_camera_sensor_format_array_t"></a> <a id="bk_camera_sensor_query_support_formats__bk_camera_sensor_handle_t.bk_camera_sensor_format_array_tP"></a> <a id="bk__camera__sensor_8h_1a1ce53e35f239a0f3084a2fab20b35d2c"></a> avdk\_err\_t bk\_camera\_sensor\_query\_support\_formats([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle, [bk\_camera\_sensor\_format\_array\_t](#_CPPv431bk_camera_sensor_format_array_t "bk_camera_sensor_format_array_t") \*format\_array)
:   Query supported sensor formats.

    参数
    :   - **handle** – Sensor handle
        - **format\_array** – Output parameter for the format array

    返回
    :   Error code

<a id="_CPPv422bk_camera_sensor_ioctl25bk_camera_sensor_handle_t8uint32_tPv"></a>

<a id="_CPPv322bk_camera_sensor_ioctl25bk_camera_sensor_handle_t8uint32_tPv"></a> <a id="_CPPv222bk_camera_sensor_ioctl25bk_camera_sensor_handle_t8uint32_tPv"></a> <a id="bk_camera_sensor_ioctl__bk_camera_sensor_handle_t.uint32_t.voidP"></a> <a id="bk__camera__sensor_8h_1a4a4c6273a12cbe386196fa41c28dd297"></a> avdk\_err\_t bk\_camera\_sensor\_ioctl([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle, uint32\_t cmd, void \*arg)
:   Issue a sensor-specific IOCTL command.

    参数
    :   - **handle** – Sensor handle
        - **cmd** – Command code, see ::bk\_camera\_sensor\_ioctl\_cmd\_t
        - **arg** – Command-specific argument

    返回
    :   Error code

<a id="_CPPv428bk_camera_sensor_auto_detectP25bk_camera_sensor_config_t16bk_camera_port_t"></a>

<a id="_CPPv328bk_camera_sensor_auto_detectP25bk_camera_sensor_config_t16bk_camera_port_t"></a> <a id="_CPPv228bk_camera_sensor_auto_detectP25bk_camera_sensor_config_t16bk_camera_port_t"></a> <a id="bk_camera_sensor_auto_detect__bk_camera_sensor_config_tP.bk_camera_port_t"></a> <a id="bk__camera__sensor_8h_1a3c03779191660277c5f03cf58fa07a9f"></a> [bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") bk\_camera\_sensor\_auto\_detect([bk\_camera\_sensor\_config\_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") \*config, [bk\_camera\_port\_t](#_CPPv416bk_camera_port_t "bk_camera_port_t") port)
:   Auto-detect the camera sensor.

    参数
    :   - **config** – Sensor configuration
        - **port** – Camera port

    返回
    :   Sensor handle, or NULL on failure

<a id="_CPPv424bk_camera_sensor_destroy25bk_camera_sensor_handle_t"></a>

<a id="_CPPv324bk_camera_sensor_destroy25bk_camera_sensor_handle_t"></a> <a id="_CPPv224bk_camera_sensor_destroy25bk_camera_sensor_handle_t"></a> <a id="bk_camera_sensor_destroy__bk_camera_sensor_handle_t"></a> <a id="bk__camera__sensor_8h_1a8f99beb7fdd49be3f12f9a85d6c84d29"></a> void bk\_camera\_sensor\_destroy([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") handle)
:   Release heap allocated by auto-detect ([bk\_camera\_csi\_sensor\_t](#structbk__camera__csi__sensor__t) / [bk\_camera\_dvp\_sensor\_t](#structbk__camera__dvp__sensor__t) wrapper).

    参数
    :   **handle** – Handle from bk\_camera\_sensor\_auto\_detect or equivalent; NULL is a no-op.

<a id="id7"></a>

#### Structures

<a id="_CPPv425bk_camera_sensor_config_t"></a>

<a id="_CPPv325bk_camera_sensor_config_t"></a> <a id="_CPPv225bk_camera_sensor_config_t"></a> <a id="bk_camera_sensor_config_t"></a> <a id="structbk__camera__sensor__config__t"></a> struct bk\_camera\_sensor\_config\_t
:   Camera sensor configuration structure.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N25bk_camera_sensor_config_t9pin_resetE"></a>

    <a id="_CPPv3N25bk_camera_sensor_config_t9pin_resetE"></a> <a id="_CPPv2N25bk_camera_sensor_config_t9pin_resetE"></a> <a id="bk_camera_sensor_config_t::pin_reset__uint8_t"></a> <a id="structbk__camera__sensor__config__t_1aa319f1387e21b4ca6918cb742dc1b2ab"></a> uint8\_t pin\_reset
    :   Reset pin number

    <a id="_CPPv4N25bk_camera_sensor_config_t8pin_pwdnE"></a>

    <a id="_CPPv3N25bk_camera_sensor_config_t8pin_pwdnE"></a> <a id="_CPPv2N25bk_camera_sensor_config_t8pin_pwdnE"></a> <a id="bk_camera_sensor_config_t::pin_pwdn__uint8_t"></a> <a id="structbk__camera__sensor__config__t_1a7fb7f3df71d2161f87779322d24d994c"></a> uint8\_t pin\_pwdn
    :   Power-down pin number

    <a id="_CPPv4N25bk_camera_sensor_config_t3busE"></a>

    <a id="_CPPv3N25bk_camera_sensor_config_t3busE"></a> <a id="_CPPv2N25bk_camera_sensor_config_t3busE"></a> <a id="bk_camera_sensor_config_t::bus__bk_camera_bus_tP"></a> <a id="structbk__camera__sensor__config__t_1a0c85e89b2231bb34ae349090ea32e279"></a> [bk\_camera\_bus\_t](#_CPPv415bk_camera_bus_t "bk_camera_bus_t") \*bus
    :   Pointer to camera bus interface

<a id="_CPPv425bk_camera_sensor_format_t"></a>

<a id="_CPPv325bk_camera_sensor_format_t"></a> <a id="_CPPv225bk_camera_sensor_format_t"></a> <a id="bk_camera_sensor_format_t"></a> <a id="structbk__camera__sensor__format__t"></a> struct bk\_camera\_sensor\_format\_t
:   Camera sensor format configuration structure.

    Each entry describes one operating mode that the sensor natively supports. `output_pixel_fmt` declares the raw Bayer/pixel format the sensor emits in this mode (e.g. RGGB8 for DVP sensors, RGGB10 for MIPI raw sensors). It is a property of the sensor/mode itself, not an application-time choice, so device drivers must populate it inside their `xxx_format_array[]`.

    On the downstream side, applications should copy this value into `bk_isp_camera_ctlr_config_t.input_pixel_fmt` (sensor output \=\= ISP input) after locating the matched mode via `bk_camera_sensor_query_support_formats()`.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N25bk_camera_sensor_format_t5widthE"></a>

    <a id="_CPPv3N25bk_camera_sensor_format_t5widthE"></a> <a id="_CPPv2N25bk_camera_sensor_format_t5widthE"></a> <a id="bk_camera_sensor_format_t::width__uint16_t"></a> <a id="structbk__camera__sensor__format__t_1a8853157b43f4be0953712c49569e3571"></a> uint16\_t width
    :   Image width (pixels)

    <a id="_CPPv4N25bk_camera_sensor_format_t6heightE"></a>

    <a id="_CPPv3N25bk_camera_sensor_format_t6heightE"></a> <a id="_CPPv2N25bk_camera_sensor_format_t6heightE"></a> <a id="bk_camera_sensor_format_t::height__uint16_t"></a> <a id="structbk__camera__sensor__format__t_1af615e3a32806fc4cd12ea7606096efe2"></a> uint16\_t height
    :   Image height (pixels)

    <a id="_CPPv4N25bk_camera_sensor_format_t3fpsE"></a>

    <a id="_CPPv3N25bk_camera_sensor_format_t3fpsE"></a> <a id="_CPPv2N25bk_camera_sensor_format_t3fpsE"></a> <a id="bk_camera_sensor_format_t::fps__uint16_t"></a> <a id="structbk__camera__sensor__format__t_1a9822743ab6c068792c8fbe491a41071b"></a> uint16\_t fps
    :   Frame rate (frames/second)

    <a id="_CPPv4N25bk_camera_sensor_format_t4xclkE"></a>

    <a id="_CPPv3N25bk_camera_sensor_format_t4xclkE"></a> <a id="_CPPv2N25bk_camera_sensor_format_t4xclkE"></a> <a id="bk_camera_sensor_format_t::xclk__uint32_t"></a> <a id="structbk__camera__sensor__format__t_1a5fdc96e079b63e6e7d69b86e14c7f46e"></a> uint32\_t xclk
    :   External clock frequency (Hz)

    <a id="_CPPv4N25bk_camera_sensor_format_t16output_pixel_fmtE"></a>

    <a id="_CPPv3N25bk_camera_sensor_format_t16output_pixel_fmtE"></a> <a id="_CPPv2N25bk_camera_sensor_format_t16output_pixel_fmtE"></a> <a id="bk_camera_sensor_format_t::output_pixel_fmt__bk_pixel_format_t"></a> <a id="structbk__camera__sensor__format__t_1a41414abc8b25636449d3f4b282b4840a"></a> bk\_pixel\_format\_t output\_pixel\_fmt
    :   Sensor output pixel format (e.g. RGGB8 / RGGB10)

<a id="_CPPv431bk_camera_sensor_format_array_t"></a>

<a id="_CPPv331bk_camera_sensor_format_array_t"></a> <a id="_CPPv231bk_camera_sensor_format_array_t"></a> <a id="bk_camera_sensor_format_array_t"></a> <a id="structbk__camera__sensor__format__array__t"></a> struct bk\_camera\_sensor\_format\_array\_t
:   Supported format array structure for camera sensor.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N31bk_camera_sensor_format_array_t4sizeE"></a>

    <a id="_CPPv3N31bk_camera_sensor_format_array_t4sizeE"></a> <a id="_CPPv2N31bk_camera_sensor_format_array_t4sizeE"></a> <a id="bk_camera_sensor_format_array_t::size__uint32_t"></a> <a id="structbk__camera__sensor__format__array__t_1acdbb7b1bb7af1bfbc5213678d00824ee"></a> uint32\_t size
    :   Size of the format array

    <a id="_CPPv4N31bk_camera_sensor_format_array_t12format_arrayE"></a>

    <a id="_CPPv3N31bk_camera_sensor_format_array_t12format_arrayE"></a> <a id="_CPPv2N31bk_camera_sensor_format_array_t12format_arrayE"></a> <a id="bk_camera_sensor_format_array_t::format_array__bk_camera_sensor_format_tCP"></a> <a id="structbk__camera__sensor__format__array__t_1acef8422f81ad9eb1cca179b5a32acbe6"></a> const [bk\_camera\_sensor\_format\_t](#_CPPv425bk_camera_sensor_format_t "bk_camera_sensor_format_t") \*format\_array
    :   Pointer to the format array

<a id="_CPPv432bk_camera_sensor_init_exposure_t"></a>

<a id="_CPPv332bk_camera_sensor_init_exposure_t"></a> <a id="_CPPv232bk_camera_sensor_init_exposure_t"></a> <a id="bk_camera_sensor_init_exposure_t"></a> <a id="structbk__camera__sensor__init__exposure__t"></a> struct bk\_camera\_sensor\_init\_exposure\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N32bk_camera_sensor_init_exposure_t8exposureE"></a>

    <a id="_CPPv3N32bk_camera_sensor_init_exposure_t8exposureE"></a> <a id="_CPPv2N32bk_camera_sensor_init_exposure_t8exposureE"></a> <a id="bk_camera_sensor_init_exposure_t::exposure__uint32_t"></a> <a id="structbk__camera__sensor__init__exposure__t_1a469e314d28ee9ab43d60b2baf513aa79"></a> uint32\_t exposure
    :   Composite AE exposure: intLine \* again \* dgain / ISP\_SNS\_GAIN\_ACCU

<a id="_CPPv423bk_camera_sensor_ctlr_t"></a>

<a id="_CPPv323bk_camera_sensor_ctlr_t"></a> <a id="_CPPv223bk_camera_sensor_ctlr_t"></a> <a id="bk_camera_sensor_ctlr_t"></a> <a id="structbk__camera__sensor__ctlr__t"></a> struct bk\_camera\_sensor\_ctlr\_t
:   Camera sensor controller operations structure.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t4initE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t4initE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t4initE"></a> <a id="structbk__camera__sensor__ctlr__t_1aebf9cb5f252636bd508ad0418206c1f7"></a> int (\*init)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller)
    :   Initialize CSI sensor

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t10set_formatE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t10set_formatE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t10set_formatE"></a> <a id="structbk__camera__sensor__ctlr__t_1ac59374e5d5e9d4c0e57ee4d7ac89fbee"></a> int (\*set\_format)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, [bk\_camera\_sensor\_format\_t](#_CPPv425bk_camera_sensor_format_t "bk_camera_sensor_format_t") \*format)
    :   Set sensor resolution

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t10power_downE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t10power_downE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t10power_downE"></a> <a id="structbk__camera__sensor__ctlr__t_1ac16ba3ea302fe3d9156f6c632c4c4231"></a> int (\*power\_down)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller)
    :   Power down or reset the sensor

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t8reg_ctrlE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t8reg_ctrlE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t8reg_ctrlE"></a> <a id="structbk__camera__sensor__ctlr__t_1aca2d22e2b082e6eb4861a6f9206ae478"></a> int (\*reg\_ctrl)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, uint8\_t cmd, uint16\_t addr, uint8\_t val)
    :   Register control function

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t11set_hmirrorE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t11set_hmirrorE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t11set_hmirrorE"></a> <a id="structbk__camera__sensor__ctlr__t_1afb879fb3ebaa131547a229e708e5a596"></a> avdk\_err\_t (\*set\_hmirror)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, bool enable)
    :   Horizontal mirror

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t9set_vflipE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t9set_vflipE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t9set_vflipE"></a> <a id="structbk__camera__sensor__ctlr__t_1a39179cdb75004c5024ac91edd27b589f"></a> avdk\_err\_t (\*set\_vflip)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, bool enable)
    :   Vertical flip

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t17get_sensor_objectE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t17get_sensor_objectE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t17get_sensor_objectE"></a> <a id="structbk__camera__sensor__ctlr__t_1a5d4a028bb938cc4925138ec4bb05699f"></a> void \*(\*get\_sensor\_object)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller)
    :   Get pointer to sensor object

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t14get_sensor_cfgE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t14get_sensor_cfgE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t14get_sensor_cfgE"></a> <a id="structbk__camera__sensor__ctlr__t_1a4dcb8cf881437bafae5d0ac14ab5552b"></a> void \*(\*get\_sensor\_cfg)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller)
    :   Get pointer to sensor configuration

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t21query_support_formatsE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t21query_support_formatsE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t21query_support_formatsE"></a> <a id="structbk__camera__sensor__ctlr__t_1a8b8c875c3cd57b91b4937e3484e99eb8"></a> avdk\_err\_t (\*query\_support\_formats)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, [bk\_camera\_sensor\_format\_array\_t](#_CPPv431bk_camera_sensor_format_array_t "bk_camera_sensor_format_array_t") \*format\_array)
    :   Query supported formats

    <a id="_CPPv4N23bk_camera_sensor_ctlr_t5ioctlE"></a>

    <a id="_CPPv3N23bk_camera_sensor_ctlr_t5ioctlE"></a> <a id="_CPPv2N23bk_camera_sensor_ctlr_t5ioctlE"></a> <a id="structbk__camera__sensor__ctlr__t_1afdee359f7f89eda554753573aca734a8"></a> avdk\_err\_t (\*ioctl)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, uint32\_t cmd, void \*arg)
    :   Sensor specific IOCTL

<a id="_CPPv427bk_camera_csi_sensor_data_t"></a>

<a id="_CPPv327bk_camera_csi_sensor_data_t"></a> <a id="_CPPv227bk_camera_csi_sensor_data_t"></a> <a id="bk_camera_csi_sensor_data_t"></a> <a id="structbk__camera__csi__sensor__data__t"></a> struct bk\_camera\_csi\_sensor\_data\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N27bk_camera_csi_sensor_data_t12private_dataE"></a>

    <a id="_CPPv3N27bk_camera_csi_sensor_data_t12private_dataE"></a> <a id="_CPPv2N27bk_camera_csi_sensor_data_t12private_dataE"></a> <a id="bk_camera_csi_sensor_data_t::private_data__voidP"></a> <a id="structbk__camera__csi__sensor__data__t_1a93cb8e488b4523b76651dfe7e3a6687d"></a> void \*private\_data
    :   Sensor-specific runtime context owned by this wrapper

<a id="_CPPv422bk_camera_csi_sensor_t"></a>

<a id="_CPPv322bk_camera_csi_sensor_t"></a> <a id="_CPPv222bk_camera_csi_sensor_t"></a> <a id="bk_camera_csi_sensor_t"></a> <a id="structbk__camera__csi__sensor__t"></a> struct bk\_camera\_csi\_sensor\_t
:   CSI camera sensor structure.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_camera_csi_sensor_t12isp_pub_attrE"></a>

    <a id="_CPPv3N22bk_camera_csi_sensor_t12isp_pub_attrE"></a> <a id="_CPPv2N22bk_camera_csi_sensor_t12isp_pub_attrE"></a> <a id="bk_camera_csi_sensor_t::isp_pub_attr__voidCP"></a> <a id="structbk__camera__csi__sensor__t_1a1881aab057374691066a1c17a534003f"></a> const void \*isp\_pub\_attr
    :   Pointer to ISP public attributes

    <a id="_CPPv4N22bk_camera_csi_sensor_t13sensor_configE"></a>

    <a id="_CPPv3N22bk_camera_csi_sensor_t13sensor_configE"></a> <a id="_CPPv2N22bk_camera_csi_sensor_t13sensor_configE"></a> <a id="bk_camera_csi_sensor_t::sensor_config__voidCP"></a> <a id="structbk__camera__csi__sensor__t_1ab0e06fe979fa71589b3ec29fae0d1989"></a> const void \*sensor\_config
    :   Pointer to sensor-specific configuration

    <a id="_CPPv4N22bk_camera_csi_sensor_t6configE"></a>

    <a id="_CPPv3N22bk_camera_csi_sensor_t6configE"></a> <a id="_CPPv2N22bk_camera_csi_sensor_t6configE"></a> <a id="bk_camera_csi_sensor_t::config__bk_camera_sensor_config_t"></a> <a id="structbk__camera__csi__sensor__t_1a5b14c9853d119ab2c8422155489747ad"></a> [bk\_camera\_sensor\_config\_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") config
    :   Sensor configuration

    <a id="_CPPv4N22bk_camera_csi_sensor_t3opsE"></a>

    <a id="_CPPv3N22bk_camera_csi_sensor_t3opsE"></a> <a id="_CPPv2N22bk_camera_csi_sensor_t3opsE"></a> <a id="bk_camera_csi_sensor_t::ops__bk_camera_sensor_ctlr_t"></a> <a id="structbk__camera__csi__sensor__t_1a1dd262131e6854a4aa501b19f9c3fdbe"></a> [bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") ops
    :   Sensor controller operations

    <a id="_CPPv4N22bk_camera_csi_sensor_t4dataE"></a>

    <a id="_CPPv3N22bk_camera_csi_sensor_t4dataE"></a> <a id="_CPPv2N22bk_camera_csi_sensor_t4dataE"></a> <a id="bk_camera_csi_sensor_t::data__bk_camera_csi_sensor_data_t"></a> <a id="structbk__camera__csi__sensor__t_1ad38d6caccfff920af39579668e964e69"></a> [bk\_camera\_csi\_sensor\_data\_t](#_CPPv427bk_camera_csi_sensor_data_t "bk_camera_csi_sensor_data_t") data
    :   Sensor data

<a id="_CPPv422bk_camera_dvp_sensor_t"></a>

<a id="_CPPv322bk_camera_dvp_sensor_t"></a> <a id="_CPPv222bk_camera_dvp_sensor_t"></a> <a id="bk_camera_dvp_sensor_t"></a> <a id="structbk__camera__dvp__sensor__t"></a> struct bk\_camera\_dvp\_sensor\_t
:   DVP camera sensor structure.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_camera_dvp_sensor_t12isp_pub_attrE"></a>

    <a id="_CPPv3N22bk_camera_dvp_sensor_t12isp_pub_attrE"></a> <a id="_CPPv2N22bk_camera_dvp_sensor_t12isp_pub_attrE"></a> <a id="bk_camera_dvp_sensor_t::isp_pub_attr__voidCP"></a> <a id="structbk__camera__dvp__sensor__t_1a706967243bcf635e3ca3d2b4cf4ed793"></a> const void \*isp\_pub\_attr
    :   Pointer to ISP public attributes

    <a id="_CPPv4N22bk_camera_dvp_sensor_t13sensor_configE"></a>

    <a id="_CPPv3N22bk_camera_dvp_sensor_t13sensor_configE"></a> <a id="_CPPv2N22bk_camera_dvp_sensor_t13sensor_configE"></a> <a id="bk_camera_dvp_sensor_t::sensor_config__voidCP"></a> <a id="structbk__camera__dvp__sensor__t_1ad241fe805b7a07cc21a3516a6d11930a"></a> const void \*sensor\_config
    :   Pointer to sensor-specific configuration

    <a id="_CPPv4N22bk_camera_dvp_sensor_t6configE"></a>

    <a id="_CPPv3N22bk_camera_dvp_sensor_t6configE"></a> <a id="_CPPv2N22bk_camera_dvp_sensor_t6configE"></a> <a id="bk_camera_dvp_sensor_t::config__bk_camera_sensor_config_t"></a> <a id="structbk__camera__dvp__sensor__t_1a05bda61b8091282580617b967c8a9c34"></a> [bk\_camera\_sensor\_config\_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") config
    :   Sensor configuration

    <a id="_CPPv4N22bk_camera_dvp_sensor_t3opsE"></a>

    <a id="_CPPv3N22bk_camera_dvp_sensor_t3opsE"></a> <a id="_CPPv2N22bk_camera_dvp_sensor_t3opsE"></a> <a id="bk_camera_dvp_sensor_t::ops__bk_camera_sensor_ctlr_t"></a> <a id="structbk__camera__dvp__sensor__t_1aec5e6614c2e1bb74afdb0894944d8f29"></a> [bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") ops
    :   Sensor controller operations

<a id="_CPPv430bk_camera_sensor_detect_func_t"></a>

<a id="_CPPv330bk_camera_sensor_detect_func_t"></a> <a id="_CPPv230bk_camera_sensor_detect_func_t"></a> <a id="bk_camera_sensor_detect_func_t"></a> <a id="structbk__camera__sensor__detect__func__t"></a> struct bk\_camera\_sensor\_detect\_func\_t
:   Camera sensor detection function structure.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N30bk_camera_sensor_detect_func_t4portE"></a>

    <a id="_CPPv3N30bk_camera_sensor_detect_func_t4portE"></a> <a id="_CPPv2N30bk_camera_sensor_detect_func_t4portE"></a> <a id="bk_camera_sensor_detect_func_t::port__bk_camera_port_t"></a> <a id="structbk__camera__sensor__detect__func__t_1a4ae89ce45d7f4ad3dd684b82cae8f19d"></a> [bk\_camera\_port\_t](#_CPPv416bk_camera_port_t "bk_camera_port_t") port
    :   Camera port

    <a id="_CPPv4N30bk_camera_sensor_detect_func_t6detectE"></a>

    <a id="_CPPv3N30bk_camera_sensor_detect_func_t6detectE"></a> <a id="_CPPv2N30bk_camera_sensor_detect_func_t6detectE"></a> <a id="structbk__camera__sensor__detect__func__t_1a8716b12ba66aa768ce34175a38ccbc2e"></a> avdk\_err\_t (\*detect)([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") \*handle, [bk\_camera\_sensor\_config\_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") \*config)
    :   Detection function pointer

<a id="id8"></a>

#### Macros

<a id="c._SECTION_ATTR_IMPL"></a>

<a id="bk__camera__sensor_8h_1aa2981b422d41df7c27b71b901b070d5d"></a> \_SECTION\_ATTR\_IMPL(SECTION, COUNTER)
:   Section attribute macro implementation.

    参数
    :   - **SECTION** – Section name
        - **COUNTER** – Counter

<a id="c._CPIMTER_STRINGIFY"></a>

<a id="bk__camera__sensor_8h_1a5374f0a0faba2ecaef934e0159f44a92"></a> \_CPIMTER\_STRINGIFY(COUNTER)
:   Stringify macro.

    参数
    :   - **COUNTER** – Counter

<a id="c.BK_CAMERA_SENSOR_DETECT_SECTION"></a>

<a id="bk__camera__sensor_8h_1aa6db172bfcde5297cf20ef01f36efed0"></a> BK\_CAMERA\_SENSOR\_DETECT\_SECTION(f, p)
:   Camera sensor detection function section registration macro.

    This macro registers a sensor detection function into a dedicated section, enabling the system to automatically discover and run detection routines.

    参数
    :   - **f** – Detection function name
        - **p** – Port type

<a id="id9"></a>

#### Type Definitions

<a id="_CPPv425bk_camera_sensor_handle_t"></a>

<a id="_CPPv325bk_camera_sensor_handle_t"></a> <a id="_CPPv225bk_camera_sensor_handle_t"></a> <a id="bk_camera_sensor_handle_t"></a> <a id="bk__camera__sensor_8h_1ac27eeea19d5264778457a9468525e215"></a> typedef struct [bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*bk\_camera\_sensor\_handle\_t

<a id="bk__camera__sensor_8h_1a09e48ae33136bb815aff734abedbc935"></a> typedef struct [bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") bk\_camera\_sensor\_ctlr\_t

<a id="id10"></a>

#### Enumerations

<a id="_CPPv428bk_camera_sensor_ioctl_cmd_t"></a>

<a id="_CPPv328bk_camera_sensor_ioctl_cmd_t"></a> <a id="_CPPv228bk_camera_sensor_ioctl_cmd_t"></a> <a id="bk__camera__sensor_8h_1acd7171513713a8b9db8fc06d260e3fc0"></a> enum bk\_camera\_sensor\_ioctl\_cmd\_t
:   Camera sensor IOCTL commands.

    *Values:*

    <a id="_CPPv4N28bk_camera_sensor_ioctl_cmd_t30BK_CAMERA_SENSOR_IOCTL_UNKNOWNE"></a>

    <a id="_CPPv3N28bk_camera_sensor_ioctl_cmd_t30BK_CAMERA_SENSOR_IOCTL_UNKNOWNE"></a> <a id="_CPPv2N28bk_camera_sensor_ioctl_cmd_t30BK_CAMERA_SENSOR_IOCTL_UNKNOWNE"></a> <a id="bk__camera__sensor_8h_1acd7171513713a8b9db8fc06d260e3fc0ac69c7f220abb7f6ccf38f316c6a0966c"></a> enumerator BK\_CAMERA\_SENSOR\_IOCTL\_UNKNOWN

    <a id="_CPPv4N28bk_camera_sensor_ioctl_cmd_t40BK_CAMERA_SENSOR_IOCTL_GET_DEFAULT_CPROCE"></a>

    <a id="_CPPv3N28bk_camera_sensor_ioctl_cmd_t40BK_CAMERA_SENSOR_IOCTL_GET_DEFAULT_CPROCE"></a> <a id="_CPPv2N28bk_camera_sensor_ioctl_cmd_t40BK_CAMERA_SENSOR_IOCTL_GET_DEFAULT_CPROCE"></a> <a id="bk__camera__sensor_8h_1acd7171513713a8b9db8fc06d260e3fc0ad1b63eecb3be8d9b30709c37b8ccf397"></a> enumerator BK\_CAMERA\_SENSOR\_IOCTL\_GET\_DEFAULT\_CPROC
    :   Get default CPROC from calib; arg \= bk\_isp\_cproc\_attr\_t \*

    <a id="_CPPv4N28bk_camera_sensor_ioctl_cmd_t40BK_CAMERA_SENSOR_IOCTL_SET_INIT_EXPOSUREE"></a>

    <a id="_CPPv3N28bk_camera_sensor_ioctl_cmd_t40BK_CAMERA_SENSOR_IOCTL_SET_INIT_EXPOSUREE"></a> <a id="_CPPv2N28bk_camera_sensor_ioctl_cmd_t40BK_CAMERA_SENSOR_IOCTL_SET_INIT_EXPOSUREE"></a> <a id="bk__camera__sensor_8h_1acd7171513713a8b9db8fc06d260e3fc0a2b0d6c2adb33d8eba6fd91f79d8f7716"></a> enumerator BK\_CAMERA\_SENSOR\_IOCTL\_SET\_INIT\_EXPOSURE
    :   Set initial Sensor exposure; arg \= [bk\_camera\_sensor\_init\_exposure\_t](#structbk__camera__sensor__init__exposure__t) \*

<a id="isp-controller"></a>

### ISP Controller

<a id="id11"></a>

#### Header File

- [bk\_camera\_isp\_ctlr.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_camera_isp_ctlr.h)

<a id="id12"></a>

#### Functions

<a id="_CPPv422bk_camera_isp_ctlr_newP27bk_isp_camera_ctlr_handle_t"></a>

<a id="_CPPv322bk_camera_isp_ctlr_newP27bk_isp_camera_ctlr_handle_t"></a> <a id="_CPPv222bk_camera_isp_ctlr_newP27bk_isp_camera_ctlr_handle_t"></a> <a id="bk_camera_isp_ctlr_new__bk_isp_camera_ctlr_handle_tP"></a> <a id="bk__camera__isp__ctlr_8h_1ae0e76d248f70899f37a2dfd266e4c4b2"></a> avdk\_err\_t bk\_camera\_isp\_ctlr\_new(bk\_isp\_camera\_ctlr\_handle\_t \*handle)
:   Create a new ISP camera controller instance.

    参数
    :   **handle** – Output pointer that receives the controller handle

    返回
    :   AVDK error code

<a id="_CPPv424bk_camera_isp_vc_mux_newP29bk_isp_camera_vc_mux_handle_t27bk_isp_camera_ctlr_handle_t"></a>

<a id="_CPPv324bk_camera_isp_vc_mux_newP29bk_isp_camera_vc_mux_handle_t27bk_isp_camera_ctlr_handle_t"></a> <a id="_CPPv224bk_camera_isp_vc_mux_newP29bk_isp_camera_vc_mux_handle_t27bk_isp_camera_ctlr_handle_t"></a> <a id="bk_camera_isp_vc_mux_new__bk_isp_camera_vc_mux_handle_tP.bk_isp_camera_ctlr_handle_t"></a> <a id="bk__camera__isp__ctlr_8h_1ad97ed309812f26587a44356667c19f69"></a> avdk\_err\_t bk\_camera\_isp\_vc\_mux\_new(bk\_isp\_camera\_vc\_mux\_handle\_t \*handle, bk\_isp\_camera\_ctlr\_handle\_t camera)
:   Create an ISP camera VC mux controller attached to an existing camera controller.

    参数
    :   - **handle** – Output VC mux handle
        - **camera** – ISP camera controller handle from bk\_camera\_isp\_ctlr\_new

    返回
    :   AVDK error code

<a id="id13"></a>

#### Structures

<a id="_CPPv427bk_isp_camera_ctlr_config_t"></a>

<a id="_CPPv327bk_isp_camera_ctlr_config_t"></a> <a id="_CPPv227bk_isp_camera_ctlr_config_t"></a> <a id="bk_isp_camera_ctlr_config_t"></a> <a id="structbk__isp__camera__ctlr__config__t"></a> struct bk\_isp\_camera\_ctlr\_config\_t

<a id="_CPPv422isp_channel_read_ctx_t"></a>

<a id="_CPPv322isp_channel_read_ctx_t"></a> <a id="_CPPv222isp_channel_read_ctx_t"></a> <a id="isp_channel_read_ctx_t"></a> <a id="structisp__channel__read__ctx__t"></a> struct isp\_channel\_read\_ctx\_t

<a id="_CPPv420bk_camera_isp_ctlr_t"></a>

<a id="_CPPv320bk_camera_isp_ctlr_t"></a> <a id="_CPPv220bk_camera_isp_ctlr_t"></a> <a id="bk_camera_isp_ctlr_t"></a> <a id="structbk__camera__isp__ctlr__t"></a> struct bk\_camera\_isp\_ctlr\_t

<a id="id14"></a>

#### Macros

<a id="c.BK_ISP_INPUT_TYPE_CSI_SENSOR"></a>

<a id="bk__camera__isp__ctlr_8h_1aac955423323795f9e0671b9e9b376f9f"></a> BK\_ISP\_INPUT\_TYPE\_CSI\_SENSOR

<a id="c.BK_ISP_INPUT_TYPE_DVP_SENSOR"></a>

<a id="bk__camera__isp__ctlr_8h_1a72d55d262c90555e586e1410f7323ebe"></a> BK\_ISP\_INPUT\_TYPE\_DVP\_SENSOR

<a id="c.BK_ISP_MODE_BT656"></a>

<a id="bk__camera__isp__ctlr_8h_1ab668ed6203e2aeda6ba1ad11be27e563"></a> BK\_ISP\_MODE\_BT656

<a id="c.BK_ISP_MODE_BT601"></a>

<a id="bk__camera__isp__ctlr_8h_1ae1544c485b10b05723c2560ef92cffd2"></a> BK\_ISP\_MODE\_BT601

<a id="c.BK_ISP_MODE_RAW"></a>

<a id="bk__camera__isp__ctlr_8h_1a5dbc85339f49fae66cc06a7a1602625c"></a> BK\_ISP\_MODE\_RAW

<a id="c.BK_ISP_HDR_MODE_LINEAR"></a>

<a id="bk__camera__isp__ctlr_8h_1a54a907864f20cd6ffd64f37b1fb86230"></a> BK\_ISP\_HDR\_MODE\_LINEAR

<a id="c.BK_ISP_HDR_MODE_ISP_STICH"></a>

<a id="bk__camera__isp__ctlr_8h_1a8c59de4aaaa1e03f1b99942ad7580914"></a> BK\_ISP\_HDR\_MODE\_ISP\_STICH

<a id="c.BK_ISP_HDR_MODE_SENSOR_STICH"></a>

<a id="bk__camera__isp__ctlr_8h_1a19e38c40b7483d2fa470c1320457688e"></a> BK\_ISP\_HDR\_MODE\_SENSOR\_STICH

<a id="c.ISP_CHANNEL_INSTANCE_MAX"></a>

<a id="bk__camera__isp__ctlr_8h_1a83082541bc4bb21137955a64c1b3bf05"></a> ISP\_CHANNEL\_INSTANCE\_MAX

<a id="id15"></a>

#### Type Definitions

<a id="_CPPv419bk_isp_input_type_t"></a>

<a id="_CPPv319bk_isp_input_type_t"></a> <a id="_CPPv219bk_isp_input_type_t"></a> <a id="bk_isp_input_type_t"></a> <a id="bk__camera__isp__ctlr_8h_1aec1c59f5af10d00b51e226e6e4128c9c"></a> typedef uint16\_t bk\_isp\_input\_type\_t

<a id="_CPPv413bk_isp_mode_t"></a>

<a id="_CPPv313bk_isp_mode_t"></a> <a id="_CPPv213bk_isp_mode_t"></a> <a id="bk_isp_mode_t"></a> <a id="bk__camera__isp__ctlr_8h_1aeebec4609d710df19cdfe7e6c126a1f8"></a> typedef uint16\_t bk\_isp\_mode\_t

<a id="_CPPv417bk_isp_hdr_mode_t"></a>

<a id="_CPPv317bk_isp_hdr_mode_t"></a> <a id="_CPPv217bk_isp_hdr_mode_t"></a> <a id="bk_isp_hdr_mode_t"></a> <a id="bk__camera__isp__ctlr_8h_1af2f93080840f6527d93563f118f598ec"></a> typedef uint16\_t bk\_isp\_hdr\_mode\_t

<a id="id16"></a>

### ISP Camera

<a id="id17"></a>

#### Header File

- [bk\_isp\_camera.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_isp_camera.h)

<a id="id18"></a>

#### Functions

<a id="_CPPv422bk_isp_camera_dev_init27bk_isp_camera_ctlr_handle_t"></a>

<a id="_CPPv322bk_isp_camera_dev_init27bk_isp_camera_ctlr_handle_t"></a> <a id="_CPPv222bk_isp_camera_dev_init27bk_isp_camera_ctlr_handle_t"></a> <a id="bk_isp_camera_dev_init__bk_isp_camera_ctlr_handle_t"></a> <a id="bk__isp__camera_8h_1aa7ecf4342e05275a63da219143030176"></a> avdk\_err\_t bk\_isp\_camera\_dev\_init(bk\_isp\_camera\_ctlr\_handle\_t handle)
:   Initialize ISP camera controller device-level resources.

    参数
    :   **handle** – ISP camera controller handle from bk\_camera\_isp\_ctlr\_new

    返回
    :   AVDK error code

<a id="_CPPv423bk_isp_camera_port_init27bk_isp_camera_ctlr_handle_tPv"></a>

<a id="_CPPv323bk_isp_camera_port_init27bk_isp_camera_ctlr_handle_tPv"></a> <a id="_CPPv223bk_isp_camera_port_init27bk_isp_camera_ctlr_handle_tPv"></a> <a id="bk_isp_camera_port_init__bk_isp_camera_ctlr_handle_t.voidP"></a> <a id="bk__isp__camera_8h_1a5db3f24371d54ffb09161d021ea2be03"></a> avdk\_err\_t bk\_isp\_camera\_port\_init(bk\_isp\_camera\_ctlr\_handle\_t handle, void \*config)
:   Configure the active ISP port (DVP or CSI)

    参数
    :   - **handle** – ISP camera controller handle
        - **config** – Pointer to [bk\_isp\_camera\_ctlr\_config\_t](#structbk__isp__camera__ctlr__config__t)

    返回
    :   AVDK error code

<a id="_CPPv425bk_isp_camera_port_select27bk_isp_camera_ctlr_handle_t7uint8_t"></a>

<a id="_CPPv325bk_isp_camera_port_select27bk_isp_camera_ctlr_handle_t7uint8_t"></a> <a id="_CPPv225bk_isp_camera_port_select27bk_isp_camera_ctlr_handle_t7uint8_t"></a> <a id="bk_isp_camera_port_select__bk_isp_camera_ctlr_handle_t.uint8_t"></a> <a id="bk__isp__camera_8h_1a1e3ca6885975be4cb323f1d5e48d5ea1"></a> avdk\_err\_t bk\_isp\_camera\_port\_select(bk\_isp\_camera\_ctlr\_handle\_t handle, uint8\_t port\_id)

<a id="_CPPv425bk_isp_camera_port_change27bk_isp_camera_ctlr_handle_t"></a>

<a id="_CPPv325bk_isp_camera_port_change27bk_isp_camera_ctlr_handle_t"></a> <a id="_CPPv225bk_isp_camera_port_change27bk_isp_camera_ctlr_handle_t"></a> <a id="bk_isp_camera_port_change__bk_isp_camera_ctlr_handle_t"></a> <a id="bk__isp__camera_8h_1a4534200983f80cbe6b1d3e64f34ac84e"></a> avdk\_err\_t bk\_isp\_camera\_port\_change(bk\_isp\_camera\_ctlr\_handle\_t handle)
:   Switch or update the active ISP port configuration.

    参数
    :   **handle** – ISP camera controller handle

    返回
    :   AVDK error code

<a id="_CPPv420bk_isp_camera_deinit27bk_isp_camera_ctlr_handle_t"></a>

<a id="_CPPv320bk_isp_camera_deinit27bk_isp_camera_ctlr_handle_t"></a> <a id="_CPPv220bk_isp_camera_deinit27bk_isp_camera_ctlr_handle_t"></a> <a id="bk_isp_camera_deinit__bk_isp_camera_ctlr_handle_t"></a> <a id="bk__isp__camera_8h_1a9543dea460aca1977cb51991f113f7d0"></a> avdk\_err\_t bk\_isp\_camera\_deinit(bk\_isp\_camera\_ctlr\_handle\_t handle)
:   Deinitialize ISP camera controller and release device-level resources.

    参数
    :   **handle** – ISP camera controller handle

    返回
    :   AVDK error code

<a id="_CPPv418bk_isp_camera_open27bk_isp_camera_ctlr_handle_tPv"></a>

<a id="_CPPv318bk_isp_camera_open27bk_isp_camera_ctlr_handle_tPv"></a> <a id="_CPPv218bk_isp_camera_open27bk_isp_camera_ctlr_handle_tPv"></a> <a id="bk_isp_camera_open__bk_isp_camera_ctlr_handle_t.voidP"></a> <a id="bk__isp__camera_8h_1ab86588e0182dc4805c6cc1be53d1fa5c"></a> avdk\_err\_t bk\_isp\_camera\_open(bk\_isp\_camera\_ctlr\_handle\_t handle, void \*parameter)
:   Start ISP camera streaming.

    参数
    :   - **handle** – ISP camera controller handle
        - **parameter** – Optional open parameters (implementation-specific, may be NULL)

    返回
    :   AVDK error code

<a id="_CPPv419bk_isp_camera_close27bk_isp_camera_ctlr_handle_t"></a>

<a id="_CPPv319bk_isp_camera_close27bk_isp_camera_ctlr_handle_t"></a> <a id="_CPPv219bk_isp_camera_close27bk_isp_camera_ctlr_handle_t"></a> <a id="bk_isp_camera_close__bk_isp_camera_ctlr_handle_t"></a> <a id="bk__isp__camera_8h_1a9d42160858c0a463db3528d3ab51f2ec"></a> avdk\_err\_t bk\_isp\_camera\_close(bk\_isp\_camera\_ctlr\_handle\_t handle)
:   Stop ISP camera streaming.

    参数
    :   **handle** – ISP camera controller handle

    返回
    :   AVDK error code

<a id="_CPPv418bk_isp_camera_read27bk_isp_camera_ctlr_handle_t8uint16_tP7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv318bk_isp_camera_read27bk_isp_camera_ctlr_handle_t8uint16_tP7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv218bk_isp_camera_read27bk_isp_camera_ctlr_handle_t8uint16_tP7uint8_t8uint32_t8uint32_t"></a> <a id="bk_isp_camera_read__bk_isp_camera_ctlr_handle_t.uint16_t.uint8_tP.uint32_t.uint32_t"></a> <a id="bk__isp__camera_8h_1adf992df3de7049e856b97264c47e790e"></a> avdk\_err\_t bk\_isp\_camera\_read(bk\_isp\_camera\_ctlr\_handle\_t handle, uint16\_t id, uint8\_t \*frame, uint32\_t size, uint32\_t timeout)
:   Read one frame from the specified channel.

    参数
    :   - **handle** – ISP camera controller handle
        - **id** – Channel identifier
        - **frame** – Output buffer for frame data
        - **size** – Size of the output buffer in bytes
        - **timeout** – Read timeout in milliseconds

    返回
    :   AVDK error code

<a id="_CPPv429bk_isp_camera_multi_port_read27bk_isp_camera_ctlr_handle_tPK23multi_port_read_param_tP24multi_port_read_result_t"></a>

<a id="_CPPv329bk_isp_camera_multi_port_read27bk_isp_camera_ctlr_handle_tPK23multi_port_read_param_tP24multi_port_read_result_t"></a> <a id="_CPPv229bk_isp_camera_multi_port_read27bk_isp_camera_ctlr_handle_tPK23multi_port_read_param_tP24multi_port_read_result_t"></a> <a id="bk_isp_camera_multi_port_read__bk_isp_camera_ctlr_handle_t.multi_port_read_param_tCP.multi_port_read_result_tP"></a> <a id="bk__isp__camera_8h_1ad6616c2d158ac09dcd428a740bba9cef"></a> avdk\_err\_t bk\_isp\_camera\_multi\_port\_read(bk\_isp\_camera\_ctlr\_handle\_t handle, const multi\_port\_read\_param\_t \*param, multi\_port\_read\_result\_t \*result)

<a id="_CPPv426bk_isp_camera_vc_mux_start29bk_isp_camera_vc_mux_handle_tP29bk_isp_camera_vc_mux_config_t"></a>

<a id="_CPPv326bk_isp_camera_vc_mux_start29bk_isp_camera_vc_mux_handle_tP29bk_isp_camera_vc_mux_config_t"></a> <a id="_CPPv226bk_isp_camera_vc_mux_start29bk_isp_camera_vc_mux_handle_tP29bk_isp_camera_vc_mux_config_t"></a> <a id="bk_isp_camera_vc_mux_start__bk_isp_camera_vc_mux_handle_t.bk_isp_camera_vc_mux_config_tP"></a> <a id="bk__isp__camera_8h_1ae18049a085d4cf3d0c039293a00c3ece"></a> avdk\_err\_t bk\_isp\_camera\_vc\_mux\_start(bk\_isp\_camera\_vc\_mux\_handle\_t handle, bk\_isp\_camera\_vc\_mux\_config\_t \*config)

<a id="_CPPv425bk_isp_camera_vc_mux_stop29bk_isp_camera_vc_mux_handle_t"></a>

<a id="_CPPv325bk_isp_camera_vc_mux_stop29bk_isp_camera_vc_mux_handle_t"></a> <a id="_CPPv225bk_isp_camera_vc_mux_stop29bk_isp_camera_vc_mux_handle_t"></a> <a id="bk_isp_camera_vc_mux_stop__bk_isp_camera_vc_mux_handle_t"></a> <a id="bk__isp__camera_8h_1a8073b3021c4048dd08df5565541d5803"></a> avdk\_err\_t bk\_isp\_camera\_vc\_mux\_stop(bk\_isp\_camera\_vc\_mux\_handle\_t handle)

<a id="_CPPv430bk_isp_camera_vc_mux_vc_enable29bk_isp_camera_vc_mux_handle_t7uint8_t7uint8_t"></a>

<a id="_CPPv330bk_isp_camera_vc_mux_vc_enable29bk_isp_camera_vc_mux_handle_t7uint8_t7uint8_t"></a> <a id="_CPPv230bk_isp_camera_vc_mux_vc_enable29bk_isp_camera_vc_mux_handle_t7uint8_t7uint8_t"></a> <a id="bk_isp_camera_vc_mux_vc_enable__bk_isp_camera_vc_mux_handle_t.uint8_t.uint8_t"></a> <a id="bk__isp__camera_8h_1ac7f6579ab33549c79dabf7d5e63cbb49"></a> avdk\_err\_t bk\_isp\_camera\_vc\_mux\_vc\_enable(bk\_isp\_camera\_vc\_mux\_handle\_t handle, uint8\_t vc, uint8\_t discard\_frames)

<a id="_CPPv431bk_isp_camera_vc_mux_vc_disable29bk_isp_camera_vc_mux_handle_t7uint8_t"></a>

<a id="_CPPv331bk_isp_camera_vc_mux_vc_disable29bk_isp_camera_vc_mux_handle_t7uint8_t"></a> <a id="_CPPv231bk_isp_camera_vc_mux_vc_disable29bk_isp_camera_vc_mux_handle_t7uint8_t"></a> <a id="bk_isp_camera_vc_mux_vc_disable__bk_isp_camera_vc_mux_handle_t.uint8_t"></a> <a id="bk__isp__camera_8h_1a8201da2d743fbc55ce95e53dfe958da7"></a> avdk\_err\_t bk\_isp\_camera\_vc\_mux\_vc\_disable(bk\_isp\_camera\_vc\_mux\_handle\_t handle, uint8\_t vc)

<a id="_CPPv425bk_isp_camera_vc_mux_peek29bk_isp_camera_vc_mux_handle_tP32bk_isp_camera_vc_mux_frame_ref_t"></a>

<a id="_CPPv325bk_isp_camera_vc_mux_peek29bk_isp_camera_vc_mux_handle_tP32bk_isp_camera_vc_mux_frame_ref_t"></a> <a id="_CPPv225bk_isp_camera_vc_mux_peek29bk_isp_camera_vc_mux_handle_tP32bk_isp_camera_vc_mux_frame_ref_t"></a> <a id="bk_isp_camera_vc_mux_peek__bk_isp_camera_vc_mux_handle_t.bk_isp_camera_vc_mux_frame_ref_tP"></a> <a id="bk__isp__camera_8h_1a06507b16097c4b5594c64e78235dad4b"></a> avdk\_err\_t bk\_isp\_camera\_vc\_mux\_peek(bk\_isp\_camera\_vc\_mux\_handle\_t handle, bk\_isp\_camera\_vc\_mux\_frame\_ref\_t \*frame)

<a id="_CPPv428bk_isp_camera_vc_mux_release29bk_isp_camera_vc_mux_handle_tP32bk_isp_camera_vc_mux_frame_ref_t"></a>

<a id="_CPPv328bk_isp_camera_vc_mux_release29bk_isp_camera_vc_mux_handle_tP32bk_isp_camera_vc_mux_frame_ref_t"></a> <a id="_CPPv228bk_isp_camera_vc_mux_release29bk_isp_camera_vc_mux_handle_tP32bk_isp_camera_vc_mux_frame_ref_t"></a> <a id="bk_isp_camera_vc_mux_release__bk_isp_camera_vc_mux_handle_t.bk_isp_camera_vc_mux_frame_ref_tP"></a> <a id="bk__isp__camera_8h_1af6e81f60d2a0e1abaf5ae0914f753738"></a> avdk\_err\_t bk\_isp\_camera\_vc\_mux\_release(bk\_isp\_camera\_vc\_mux\_handle\_t handle, bk\_isp\_camera\_vc\_mux\_frame\_ref\_t \*frame)

<a id="_CPPv427bk_isp_camera_vc_mux_delete29bk_isp_camera_vc_mux_handle_t"></a>

<a id="_CPPv327bk_isp_camera_vc_mux_delete29bk_isp_camera_vc_mux_handle_t"></a> <a id="_CPPv227bk_isp_camera_vc_mux_delete29bk_isp_camera_vc_mux_handle_t"></a> <a id="bk_isp_camera_vc_mux_delete__bk_isp_camera_vc_mux_handle_t"></a> <a id="bk__isp__camera_8h_1a5fe902ba3ce5c3e5aecb27a328f2c4ff"></a> avdk\_err\_t bk\_isp\_camera\_vc\_mux\_delete(bk\_isp\_camera\_vc\_mux\_handle\_t handle)
:   Destroy the ISP camera VC mux controller instance.

    参数
    :   **handle** – VC mux handle from bk\_camera\_isp\_vc\_mux\_new

    返回
    :   AVDK error code

<a id="_CPPv435bk_isp_camera_register_isr_callback27bk_isp_camera_ctlr_handle_t20bk_camera_isr_type_t15bk_camera_isr_tPv"></a>

<a id="_CPPv335bk_isp_camera_register_isr_callback27bk_isp_camera_ctlr_handle_t20bk_camera_isr_type_t15bk_camera_isr_tPv"></a> <a id="_CPPv235bk_isp_camera_register_isr_callback27bk_isp_camera_ctlr_handle_t20bk_camera_isr_type_t15bk_camera_isr_tPv"></a> <a id="bk_isp_camera_register_isr_callback__bk_isp_camera_ctlr_handle_t.bk_camera_isr_type_t.bk_camera_isr_t.voidP"></a> <a id="bk__isp__camera_8h_1a2563123a97563669935805aa7723b479"></a> avdk\_err\_t bk\_isp\_camera\_register\_isr\_callback(bk\_isp\_camera\_ctlr\_handle\_t handle, bk\_camera\_isr\_type\_t type, bk\_camera\_isr\_t cb, void \*arg)
:   Register an ISP interrupt callback.

    参数
    :   - **handle** – ISP camera controller handle
        - **type** – ISR event type
        - **cb** – Callback function
        - **arg** – User argument passed to the callback

    返回
    :   AVDK error code

<a id="_CPPv437bk_isp_camera_deregister_isr_callback27bk_isp_camera_ctlr_handle_t20bk_camera_isr_type_tPv"></a>

<a id="_CPPv337bk_isp_camera_deregister_isr_callback27bk_isp_camera_ctlr_handle_t20bk_camera_isr_type_tPv"></a> <a id="_CPPv237bk_isp_camera_deregister_isr_callback27bk_isp_camera_ctlr_handle_t20bk_camera_isr_type_tPv"></a> <a id="bk_isp_camera_deregister_isr_callback__bk_isp_camera_ctlr_handle_t.bk_camera_isr_type_t.voidP"></a> <a id="bk__isp__camera_8h_1aa30c35b45f4b1a991d28f943c4d6bff3"></a> avdk\_err\_t bk\_isp\_camera\_deregister\_isr\_callback(bk\_isp\_camera\_ctlr\_handle\_t handle, bk\_camera\_isr\_type\_t type, void \*arg)
:   Deregister an ISP interrupt callback.

    参数
    :   - **handle** – ISP camera controller handle
        - **type** – ISR event type
        - **arg** – User argument that was registered with the callback

    返回
    :   AVDK error code

<a id="_CPPv424bk_isp_camera_ctlr_ioctl27bk_isp_camera_ctlr_handle_t24bk_cam_interface_ioctl_tPv"></a>

<a id="_CPPv324bk_isp_camera_ctlr_ioctl27bk_isp_camera_ctlr_handle_t24bk_cam_interface_ioctl_tPv"></a> <a id="_CPPv224bk_isp_camera_ctlr_ioctl27bk_isp_camera_ctlr_handle_t24bk_cam_interface_ioctl_tPv"></a> <a id="bk_isp_camera_ctlr_ioctl__bk_isp_camera_ctlr_handle_t.bk_cam_interface_ioctl_t.voidP"></a> <a id="bk__isp__camera_8h_1ac475bf9ab1dd3e1e7e20256e8c6ea21b"></a> avdk\_err\_t bk\_isp\_camera\_ctlr\_ioctl(bk\_isp\_camera\_ctlr\_handle\_t handle, bk\_cam\_interface\_ioctl\_t ioctl, void \*arg)
:   Issue an IOCTL command on the ISP camera controller.

    White balance (BK\_CAM\_IOCTL\_GET/SET\_WB) and exposure (BK\_CAM\_IOCTL\_GET/SET\_EXPOSURE) notes:

    - Call them only after bk\_isp\_camera\_port\_init(). That step loads the sensor tuning data, which overwrites the whole WB and exposure attribute set, so anything set earlier is silently lost. Re-apply after a port re-init.
    - Both act on the currently selected logical ISP port; use BK\_CAM\_IOCTL\_SELECT\_ISP\_PORT first on multi-port setups.
    - Prefer get-modify-set so unrelated fields keep their current value.
    - Manual values take effect on the next 3A interrupt while streaming, so expect a delay of one to three frames.
    - Out-of-range gains and exposure times are clamped by the ISP firmware with a warning rather than rejected; read back if the exact value matters.
    - On a dual MIPI logical port setup, BK\_CAM\_IOCTL\_RESTORE\_ISP\_PORT\_CONTEXT forces AE back to auto, so manual exposure must be re-applied after a port switch. White balance is unaffected.

    参数
    :   - **handle** – ISP camera controller handle
        - **ioctl** – IOCTL command identifier
        - **arg** – Command-specific argument

    返回
    :   AVDK error code

<a id="_CPPv420bk_isp_camera_delete27bk_isp_camera_ctlr_handle_t"></a>

<a id="_CPPv320bk_isp_camera_delete27bk_isp_camera_ctlr_handle_t"></a> <a id="_CPPv220bk_isp_camera_delete27bk_isp_camera_ctlr_handle_t"></a> <a id="bk_isp_camera_delete__bk_isp_camera_ctlr_handle_t"></a> <a id="bk__isp__camera_8h_1a042966be319611f295a5195d37b400bf"></a> avdk\_err\_t bk\_isp\_camera\_delete(bk\_isp\_camera\_ctlr\_handle\_t handle)
:   Destroy the ISP camera controller instance.

    参数
    :   **handle** – ISP camera controller handle

    返回
    :   AVDK error code

<a id="_CPPv426bk_isp_camera_channel_open27bk_isp_camera_ctlr_handle_t7uint8_tP30bk_isp_camera_channel_config_t"></a>

<a id="_CPPv326bk_isp_camera_channel_open27bk_isp_camera_ctlr_handle_t7uint8_tP30bk_isp_camera_channel_config_t"></a> <a id="_CPPv226bk_isp_camera_channel_open27bk_isp_camera_ctlr_handle_t7uint8_tP30bk_isp_camera_channel_config_t"></a> <a id="bk_isp_camera_channel_open__bk_isp_camera_ctlr_handle_t.uint8_t.bk_isp_camera_channel_config_tP"></a> <a id="bk__isp__camera_8h_1a522ca8480283926b2e036345fc6b51f0"></a> avdk\_err\_t bk\_isp\_camera\_channel\_open(bk\_isp\_camera\_ctlr\_handle\_t handle, uint8\_t channel, [bk\_isp\_camera\_channel\_config\_t](#_CPPv430bk_isp_camera_channel_config_t "bk_isp_camera_channel_config_t") \*config)
:   Open an ISP output channel.

    参数
    :   - **handle** – ISP camera controller handle
        - **channel** – Channel index
        - **config** – Channel configuration

    返回
    :   AVDK error code

<a id="_CPPv427bk_isp_camera_channel_close27bk_isp_camera_ctlr_handle_t7uint8_t"></a>

<a id="_CPPv327bk_isp_camera_channel_close27bk_isp_camera_ctlr_handle_t7uint8_t"></a> <a id="_CPPv227bk_isp_camera_channel_close27bk_isp_camera_ctlr_handle_t7uint8_t"></a> <a id="bk_isp_camera_channel_close__bk_isp_camera_ctlr_handle_t.uint8_t"></a> <a id="bk__isp__camera_8h_1afe8b94513905cd814091bcb037876a03"></a> avdk\_err\_t bk\_isp\_camera\_channel\_close(bk\_isp\_camera\_ctlr\_handle\_t handle, uint8\_t channel)
:   Close an ISP output channel.

    参数
    :   - **handle** – ISP camera controller handle
        - **channel** – Channel index

    返回
    :   AVDK error code

<a id="_CPPv431bk_isp_camera_channel_state_get27bk_isp_camera_ctlr_handle_t7uint8_t"></a>

<a id="_CPPv331bk_isp_camera_channel_state_get27bk_isp_camera_ctlr_handle_t7uint8_t"></a> <a id="_CPPv231bk_isp_camera_channel_state_get27bk_isp_camera_ctlr_handle_t7uint8_t"></a> <a id="bk_isp_camera_channel_state_get__bk_isp_camera_ctlr_handle_t.uint8_t"></a> <a id="bk__isp__camera_8h_1a81f2e54517d1ee81c5d193a261e65fe0"></a> bk\_isp\_camera\_channel\_state\_t bk\_isp\_camera\_channel\_state\_get(bk\_isp\_camera\_ctlr\_handle\_t handle, uint8\_t channel)
:   Get the state of an ISP output channel.

    参数
    :   - **handle** – ISP camera controller handle
        - **channel** – Channel index

    返回
    :   Channel state

<a id="isp-camera-types"></a>

### ISP Camera Types

<a id="_CPPv430bk_isp_camera_channel_config_t"></a>

<a id="_CPPv330bk_isp_camera_channel_config_t"></a> <a id="_CPPv230bk_isp_camera_channel_config_t"></a> <a id="bk_isp_camera_channel_config_t"></a> <a id="structbk__isp__camera__channel__config__t"></a> struct bk\_isp\_camera\_channel\_config\_t
:   Camera ISP instance configuration structure.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N30bk_isp_camera_channel_config_t7buf_cntE"></a>

    <a id="_CPPv3N30bk_isp_camera_channel_config_t7buf_cntE"></a> <a id="_CPPv2N30bk_isp_camera_channel_config_t7buf_cntE"></a> <a id="bk_isp_camera_channel_config_t::buf_cnt__uint8_t"></a> <a id="structbk__isp__camera__channel__config__t_1a149168dc97618839eee2a3cf8be95564"></a> uint8\_t buf\_cnt
    :   Number of frame buffers

    <a id="_CPPv4N30bk_isp_camera_channel_config_t7port_idE"></a>

    <a id="_CPPv3N30bk_isp_camera_channel_config_t7port_idE"></a> <a id="_CPPv2N30bk_isp_camera_channel_config_t7port_idE"></a> <a id="bk_isp_camera_channel_config_t::port_id__uint8_t"></a> <a id="structbk__isp__camera__channel__config__t_1ae74152a2ae763791921d62618431d524"></a> uint8\_t port\_id
    :   Port identifier

    <a id="_CPPv4N30bk_isp_camera_channel_config_t12enable_flexaE"></a>

    <a id="_CPPv3N30bk_isp_camera_channel_config_t12enable_flexaE"></a> <a id="_CPPv2N30bk_isp_camera_channel_config_t12enable_flexaE"></a> <a id="bk_isp_camera_channel_config_t::enable_flexa__uint8_t"></a> <a id="structbk__isp__camera__channel__config__t_1ad5c7113e3be25973f125b16c6789e746"></a> uint8\_t enable\_flexa
    :   Enable Flexa: 0 \- disable, 1 \- enable

    <a id="_CPPv4N30bk_isp_camera_channel_config_t9work_modeE"></a>

    <a id="_CPPv3N30bk_isp_camera_channel_config_t9work_modeE"></a> <a id="_CPPv2N30bk_isp_camera_channel_config_t9work_modeE"></a> <a id="bk_isp_camera_channel_config_t::work_mode__uint8_t"></a> <a id="structbk__isp__camera__channel__config__t_1ad3f2d2ef39573ec22a64b755385714b8"></a> uint8\_t work\_mode
    :   Operating mode: 0 \- frame mode, 1 \- SFW Flexa mode

    <a id="_CPPv4N30bk_isp_camera_channel_config_t5widthE"></a>

    <a id="_CPPv3N30bk_isp_camera_channel_config_t5widthE"></a> <a id="_CPPv2N30bk_isp_camera_channel_config_t5widthE"></a> <a id="bk_isp_camera_channel_config_t::width__uint16_t"></a> <a id="structbk__isp__camera__channel__config__t_1adb7692ba9ad9816a08a4db8248d7fb2c"></a> uint16\_t width
    :   Frame width in pixels

    <a id="_CPPv4N30bk_isp_camera_channel_config_t6heightE"></a>

    <a id="_CPPv3N30bk_isp_camera_channel_config_t6heightE"></a> <a id="_CPPv2N30bk_isp_camera_channel_config_t6heightE"></a> <a id="bk_isp_camera_channel_config_t::height__uint16_t"></a> <a id="structbk__isp__camera__channel__config__t_1aeb7b7ea7bc1c3ce2230b09a002e37d75"></a> uint16\_t height
    :   Frame height in pixels

    <a id="_CPPv4N30bk_isp_camera_channel_config_t6formatE"></a>

    <a id="_CPPv3N30bk_isp_camera_channel_config_t6formatE"></a> <a id="_CPPv2N30bk_isp_camera_channel_config_t6formatE"></a> <a id="bk_isp_camera_channel_config_t::format__uint16_t"></a> <a id="structbk__isp__camera__channel__config__t_1a3f965f27f2b2e68f972eab714f8572d6"></a> uint16\_t format
    :   Pixel format

<a id="_CPPv416bk_camera_ctlr_t"></a>

<a id="_CPPv316bk_camera_ctlr_t"></a> <a id="_CPPv216bk_camera_ctlr_t"></a> <a id="bk_camera_ctlr_t"></a> <a id="structbk__camera__ctlr__t"></a> struct bk\_camera\_ctlr\_t
:   Camera controller operation table.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16bk_camera_ctlr_t8dev_initE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t8dev_initE"></a> <a id="_CPPv2N16bk_camera_ctlr_t8dev_initE"></a> <a id="structbk__camera__ctlr__t_1a1794fdeebe6ba84d0e9944844e139151"></a> avdk\_err\_t (\*dev\_init)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller)
    :   Initialize controller level resources (clock, GPIO, etc.)

    <a id="_CPPv4N16bk_camera_ctlr_t9port_initE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t9port_initE"></a> <a id="_CPPv2N16bk_camera_ctlr_t9port_initE"></a> <a id="structbk__camera__ctlr__t_1a170b1df6ab0a90862bd1dd39f8a82c3f"></a> avdk\_err\_t (\*port\_init)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, void \*config)
    :   Configure a physical port according to the supplied configuration

    <a id="_CPPv4N16bk_camera_ctlr_t11port_selectE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t11port_selectE"></a> <a id="_CPPv2N16bk_camera_ctlr_t11port_selectE"></a> <a id="structbk__camera__ctlr__t_1a934411e4e9db78d2123bffb9f3cbe7df"></a> avdk\_err\_t (\*port\_select)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, uint8\_t port\_id)
    :   Select an initialized logical ISP port

    <a id="_CPPv4N16bk_camera_ctlr_t11port_changeE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t11port_changeE"></a> <a id="_CPPv2N16bk_camera_ctlr_t11port_changeE"></a> <a id="structbk__camera__ctlr__t_1a50f895efe03d88013a752904f0005b53"></a> avdk\_err\_t (\*port\_change)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller)
    :   Switch the active port or update link configuration dynamically

    <a id="_CPPv4N16bk_camera_ctlr_t4openE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t4openE"></a> <a id="_CPPv2N16bk_camera_ctlr_t4openE"></a> <a id="structbk__camera__ctlr__t_1a8a5bf1bbcd30960ee3c2fb319b7cfe03"></a> avdk\_err\_t (\*open)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, void \*parameter)
    :   Open the controller for streaming with the specified parameters

    <a id="_CPPv4N16bk_camera_ctlr_t4readE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t4readE"></a> <a id="_CPPv2N16bk_camera_ctlr_t4readE"></a> <a id="structbk__camera__ctlr__t_1aabf10c5acd42a2380801eafcb04032e2"></a> avdk\_err\_t (\*read)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, uint16\_t id, uint8\_t \*frame, uint32\_t size, uint32\_t timeout)
    :   Read a frame

    <a id="_CPPv4N16bk_camera_ctlr_t15multi_port_readE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t15multi_port_readE"></a> <a id="_CPPv2N16bk_camera_ctlr_t15multi_port_readE"></a> <a id="structbk__camera__ctlr__t_1a3d2f42df6ad4da5c5f6198fd69a614c8"></a> avdk\_err\_t (\*multi\_port\_read)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, const multi\_port\_read\_param\_t \*param, multi\_port\_read\_result\_t \*result)
    :   Read a frame and return its logical ISP port

    <a id="_CPPv4N16bk_camera_ctlr_t5closeE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t5closeE"></a> <a id="_CPPv2N16bk_camera_ctlr_t5closeE"></a> <a id="structbk__camera__ctlr__t_1aa58dd129c1660677853120795a3f5e09"></a> avdk\_err\_t (\*close)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller)
    :   Stop streaming and release transient resources

    <a id="_CPPv4N16bk_camera_ctlr_t6deinitE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t6deinitE"></a> <a id="_CPPv2N16bk_camera_ctlr_t6deinitE"></a> <a id="structbk__camera__ctlr__t_1a4cb9a9602ffe69ba5dac1f52d6e07816"></a> avdk\_err\_t (\*deinit)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller)
    :   Deinitialize controller level resources

    <a id="_CPPv4N16bk_camera_ctlr_t7suspendE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t7suspendE"></a> <a id="_CPPv2N16bk_camera_ctlr_t7suspendE"></a> <a id="structbk__camera__ctlr__t_1a8f20704edf0c45e48d87d62c1c26753c"></a> avdk\_err\_t (\*suspend)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller)
    :   Suspend the controller for low-power operation

    <a id="_CPPv4N16bk_camera_ctlr_t6resumeE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t6resumeE"></a> <a id="_CPPv2N16bk_camera_ctlr_t6resumeE"></a> <a id="structbk__camera__ctlr__t_1ab2a6a36c507ff671a0333ad95fc5677a"></a> avdk\_err\_t (\*resume)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller)
    :   Resume the controller after suspension

    <a id="_CPPv4N16bk_camera_ctlr_t5ioctlE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t5ioctlE"></a> <a id="_CPPv2N16bk_camera_ctlr_t5ioctlE"></a> <a id="structbk__camera__ctlr__t_1afb6a0a8a37fd9c9c3fc440eda53087d4"></a> avdk\_err\_t (\*ioctl)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, bk\_cam\_interface\_ioctl\_t ioctl, void \*arg)
    :   Issue controller specific IOCTL commands

    <a id="_CPPv4N16bk_camera_ctlr_t3delE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t3delE"></a> <a id="_CPPv2N16bk_camera_ctlr_t3delE"></a> <a id="structbk__camera__ctlr__t_1a981e4dfd8a51684d63de2b1eba64675c"></a> avdk\_err\_t (\*del)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller)
    :   Destroy the controller object and free memory

    <a id="_CPPv4N16bk_camera_ctlr_t21register_isr_callbackE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t21register_isr_callbackE"></a> <a id="_CPPv2N16bk_camera_ctlr_t21register_isr_callbackE"></a> <a id="structbk__camera__ctlr__t_1a89636770d3413b9fd9f2228623e477e2"></a> avdk\_err\_t (\*register\_isr\_callback)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, bk\_camera\_isr\_type\_t type, bk\_camera\_isr\_t cb, void \*arg)
    :   Register ISP interrupt service routine callback

    <a id="_CPPv4N16bk_camera_ctlr_t23deregister_isr_callbackE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t23deregister_isr_callbackE"></a> <a id="_CPPv2N16bk_camera_ctlr_t23deregister_isr_callbackE"></a> <a id="structbk__camera__ctlr__t_1a089f63fbc73bd560850433351d9bb0bc"></a> avdk\_err\_t (\*deregister\_isr\_callback)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, bk\_camera\_isr\_type\_t type, void \*arg)
    :   Deregister ISP interrupt service routine callback

    <a id="_CPPv4N16bk_camera_ctlr_t12channel_openE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t12channel_openE"></a> <a id="_CPPv2N16bk_camera_ctlr_t12channel_openE"></a> <a id="structbk__camera__ctlr__t_1a3e066036cad18443757d9bd911bfbfe8"></a> avdk\_err\_t (\*channel\_open)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, uint8\_t channel, [bk\_isp\_camera\_channel\_config\_t](#_CPPv430bk_isp_camera_channel_config_t "bk_isp_camera_channel_config_t") \*config)
    :   Open a channel

    <a id="_CPPv4N16bk_camera_ctlr_t13channel_closeE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t13channel_closeE"></a> <a id="_CPPv2N16bk_camera_ctlr_t13channel_closeE"></a> <a id="structbk__camera__ctlr__t_1a97556d4b4cb18eb5f8682c935bd86727"></a> avdk\_err\_t (\*channel\_close)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, uint8\_t channel)
    :   Close a channel

    <a id="_CPPv4N16bk_camera_ctlr_t17channel_state_getE"></a>

    <a id="_CPPv3N16bk_camera_ctlr_t17channel_state_getE"></a> <a id="_CPPv2N16bk_camera_ctlr_t17channel_state_getE"></a> <a id="structbk__camera__ctlr__t_1a7785dca730a568334d5abe80bcd21c82"></a> bk\_isp\_camera\_channel\_state\_t (\*channel\_state\_get)([bk\_camera\_ctlr\_t](#_CPPv416bk_camera_ctlr_t "bk_camera_ctlr_t") \*controller, uint8\_t channel)
    :   Get a channel state

<a id="_CPPv411sensor_id_t"></a>

<a id="_CPPv311sensor_id_t"></a> <a id="_CPPv211sensor_id_t"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6"></a> enum sensor\_id\_t
:   Enumeration of sensor identifiers.

    *Values:*

    <a id="_CPPv4N11sensor_id_t9ID_UNKNOWE"></a>

    <a id="_CPPv3N11sensor_id_t9ID_UNKNOWE"></a> <a id="_CPPv2N11sensor_id_t9ID_UNKNOWE"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6aa522e5582aa8f0d9c6e142840443a523"></a> enumerator ID\_UNKNOW
    :   Unknown sensor

    <a id="_CPPv4N11sensor_id_t10ID_PAS6329E"></a>

    <a id="_CPPv3N11sensor_id_t10ID_PAS6329E"></a> <a id="_CPPv2N11sensor_id_t10ID_PAS6329E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a9bee58f985939f499c9d6cd3fe368d8e"></a> enumerator ID\_PAS6329
    :   PAS6329 sensor

    <a id="_CPPv4N11sensor_id_t9ID_OV7670E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_OV7670E"></a> <a id="_CPPv2N11sensor_id_t9ID_OV7670E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a4bff123c4ea8676da98770abdcb36c78"></a> enumerator ID\_OV7670
    :   OV7670 sensor

    <a id="_CPPv4N11sensor_id_t10ID_PAS6375E"></a>

    <a id="_CPPv3N11sensor_id_t10ID_PAS6375E"></a> <a id="_CPPv2N11sensor_id_t10ID_PAS6375E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6acfa56a6897a4e4a0313c06658a5da75c"></a> enumerator ID\_PAS6375
    :   PAS6375 sensor

    <a id="_CPPv4N11sensor_id_t10ID_GC0328CE"></a>

    <a id="_CPPv3N11sensor_id_t10ID_GC0328CE"></a> <a id="_CPPv2N11sensor_id_t10ID_GC0328CE"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a467d8e3d0b85197644f4e57f2e9bfd97"></a> enumerator ID\_GC0328C
    :   GC0328C sensor

    <a id="_CPPv4N11sensor_id_t9ID_BF2013E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_BF2013E"></a> <a id="_CPPv2N11sensor_id_t9ID_BF2013E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a828081741d1e90ce4a84ed13e28a111d"></a> enumerator ID\_BF2013
    :   BF2013 sensor

    <a id="_CPPv4N11sensor_id_t10ID_GC0308CE"></a>

    <a id="_CPPv3N11sensor_id_t10ID_GC0308CE"></a> <a id="_CPPv2N11sensor_id_t10ID_GC0308CE"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a1f60ec9fc31cf2140d8267273df0eef5"></a> enumerator ID\_GC0308C
    :   GC0308C sensor

    <a id="_CPPv4N11sensor_id_t9ID_HM1055E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_HM1055E"></a> <a id="_CPPv2N11sensor_id_t9ID_HM1055E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a310b28e1516bcc5d04869f1a85d32751"></a> enumerator ID\_HM1055
    :   HM1055 sensor

    <a id="_CPPv4N11sensor_id_t9ID_GC2145E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_GC2145E"></a> <a id="_CPPv2N11sensor_id_t9ID_GC2145E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a3fc0969905257087061c006548ad7b31"></a> enumerator ID\_GC2145
    :   GC2145 sensor

    <a id="_CPPv4N11sensor_id_t9ID_OV2640E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_OV2640E"></a> <a id="_CPPv2N11sensor_id_t9ID_OV2640E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6aa1f46e481e0e295c2a116c83e74a8275"></a> enumerator ID\_OV2640
    :   OV2640 sensor

    <a id="_CPPv4N11sensor_id_t9ID_GC0308E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_GC0308E"></a> <a id="_CPPv2N11sensor_id_t9ID_GC0308E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a59ebd0e84e50168cccc19ad6a2b808b3"></a> enumerator ID\_GC0308
    :   GC0308 sensor

    <a id="_CPPv4N11sensor_id_t10ID_TVP5150E"></a>

    <a id="_CPPv3N11sensor_id_t10ID_TVP5150E"></a> <a id="_CPPv2N11sensor_id_t10ID_TVP5150E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6afd325c5527ebb4b555f61ef252ce4ae8"></a> enumerator ID\_TVP5150
    :   TVP5150 sensor

    <a id="_CPPv4N11sensor_id_t8ID_SC101E"></a>

    <a id="_CPPv3N11sensor_id_t8ID_SC101E"></a> <a id="_CPPv2N11sensor_id_t8ID_SC101E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a309ebd04930981b6a2fd3461a74367dc"></a> enumerator ID\_SC101
    :   SC101 sensor

    <a id="_CPPv4N11sensor_id_t9ID_GC2053E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_GC2053E"></a> <a id="_CPPv2N11sensor_id_t9ID_GC2053E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a634b1791e2afed4b7261092bc0c8f974"></a> enumerator ID\_GC2053
    :   GC2053 sensor

    <a id="_CPPv4N11sensor_id_t9ID_GC4653E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_GC4653E"></a> <a id="_CPPv2N11sensor_id_t9ID_GC4653E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a336cfeabf802818b0878af323e013f7e"></a> enumerator ID\_GC4653
    :   GC4653 sensor

    <a id="_CPPv4N11sensor_id_t9ID_OV2775E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_OV2775E"></a> <a id="_CPPv2N11sensor_id_t9ID_OV2775E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a779c4f64d917f16897d53930feb50451"></a> enumerator ID\_OV2775
    :   OV2775 sensor

    <a id="_CPPv4N11sensor_id_t10ID_GC2053DE"></a>

    <a id="_CPPv3N11sensor_id_t10ID_GC2053DE"></a> <a id="_CPPv2N11sensor_id_t10ID_GC2053DE"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a776670dde9eb4e26b0f2554c69e20112"></a> enumerator ID\_GC2053D
    :   GC2053D sensor

    <a id="_CPPv4N11sensor_id_t9ID_CV2002E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_CV2002E"></a> <a id="_CPPv2N11sensor_id_t9ID_CV2002E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6ada2d30eb7d2e50f2a9efd4a7a7eb774b"></a> enumerator ID\_CV2002
    :   CV2002 sensor

    <a id="_CPPv4N11sensor_id_t9ID_CV2005E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_CV2005E"></a> <a id="_CPPv2N11sensor_id_t9ID_CV2005E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a42c9971357774b25fe4fa0814a480eb4"></a> enumerator ID\_CV2005
    :   CV2005 sensor

    <a id="_CPPv4N11sensor_id_t9ID_CV2008E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_CV2008E"></a> <a id="_CPPv2N11sensor_id_t9ID_CV2008E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a1241bd6159174ccc0a9eba35784eecc0"></a> enumerator ID\_CV2008
    :   CV2008 sensor

    <a id="_CPPv4N11sensor_id_t9ID_GC20C3E"></a>

    <a id="_CPPv3N11sensor_id_t9ID_GC20C3E"></a> <a id="_CPPv2N11sensor_id_t9ID_GC20C3E"></a> <a id="bk__isp__camera__types_8h_1a1e2efa0d9103cfa0fa5e77f4b65701f6a8f4551862ea23606ccdd9209f2d4e767"></a> enumerator ID\_GC20C3
    :   GC20C3 sensor

<a id="dvp-camera-types"></a>

### DVP Camera Types

<a id="id19"></a>

#### Header File

- [bk\_dvp\_camera\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_dvp_camera_types.h)

<a id="id20"></a>

#### Structures

<a id="_CPPv419dvp_sensor_config_t"></a>

<a id="_CPPv319dvp_sensor_config_t"></a> <a id="_CPPv219dvp_sensor_config_t"></a> <a id="dvp_sensor_config_t"></a> <a id="structdvp__sensor__config__t"></a> struct dvp\_sensor\_config\_t
:   dvp sensor configure

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19dvp_sensor_config_t4nameE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t4nameE"></a> <a id="_CPPv2N19dvp_sensor_config_t4nameE"></a> <a id="dvp_sensor_config_t::name__cP"></a> <a id="structdvp__sensor__config__t_1ab7b2b20c53aa87375e3495562f7ee647"></a> char \*name
    :   sensor name

    <a id="_CPPv4N19dvp_sensor_config_t3clkE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t3clkE"></a> <a id="_CPPv2N19dvp_sensor_config_t3clkE"></a> <a id="dvp_sensor_config_t::clk__mclk_freq_t"></a> <a id="structdvp__sensor__config__t_1acc75e0d6e90b402ebb4c2efd2953f7a6"></a> mclk\_freq\_t clk
    :   sensor work clk in config fps and ppi

    <a id="_CPPv4N19dvp_sensor_config_t5vsyncE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t5vsyncE"></a> <a id="_CPPv2N19dvp_sensor_config_t5vsyncE"></a> <a id="dvp_sensor_config_t::vsync__sync_level_t"></a> <a id="structdvp__sensor__config__t_1a362a51d84e5c4a755e1744181bdd041c"></a> sync\_level\_t vsync
    :   sensor vsync active level

    <a id="_CPPv4N19dvp_sensor_config_t5hsyncE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t5hsyncE"></a> <a id="_CPPv2N19dvp_sensor_config_t5hsyncE"></a> <a id="dvp_sensor_config_t::hsync__sync_level_t"></a> <a id="structdvp__sensor__config__t_1af62377e7f34b990ea6d6a0a7a35b7358"></a> sync\_level\_t hsync
    :   sensor hsync active level

    <a id="_CPPv4N19dvp_sensor_config_t2idE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t2idE"></a> <a id="_CPPv2N19dvp_sensor_config_t2idE"></a> <a id="dvp_sensor_config_t::id__uint16_t"></a> <a id="structdvp__sensor__config__t_1a54479b78007648b61b3c87e8172e7f49"></a> uint16\_t id
    :   sensor type, sensor\_id\_t

    <a id="_CPPv4N19dvp_sensor_config_t7addressE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7addressE"></a> <a id="_CPPv2N19dvp_sensor_config_t7addressE"></a> <a id="dvp_sensor_config_t::address__uint16_t"></a> <a id="structdvp__sensor__config__t_1af605f3525eae060dc9559b75c49a07f6"></a> uint16\_t address
    :   sensor write register address by i2c

    <a id="_CPPv4N19dvp_sensor_config_t6detectE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t6detectE"></a> <a id="_CPPv2N19dvp_sensor_config_t6detectE"></a> <a id="structdvp__sensor__config__t_1a26f77996a07a74e4d2c1f55f9cb9b70d"></a> avdk\_err\_t (\*detect)([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") \*handle, [bk\_camera\_sensor\_config\_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") \*config)
    :   auto detect used dvp sensor

    <a id="_CPPv4N19dvp_sensor_config_t4initE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t4initE"></a> <a id="_CPPv2N19dvp_sensor_config_t4initE"></a> <a id="structdvp__sensor__config__t_1a559ee260c17ab796f9a487e61e763b6e"></a> avdk\_err\_t (\*init)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller)
    :   init dvp sensor

    <a id="_CPPv4N19dvp_sensor_config_t7set_ppiE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7set_ppiE"></a> <a id="_CPPv2N19dvp_sensor_config_t7set_ppiE"></a> <a id="structdvp__sensor__config__t_1a65022fba835b0a96086e9742580df079"></a> avdk\_err\_t (\*set\_ppi)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, uint16\_t width, uint16\_t height)
    :   set resolution of sensor

    <a id="_CPPv4N19dvp_sensor_config_t7set_fpsE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t7set_fpsE"></a> <a id="_CPPv2N19dvp_sensor_config_t7set_fpsE"></a> <a id="structdvp__sensor__config__t_1a1b91db50e94c57206e110f927aa7e955"></a> avdk\_err\_t (\*set\_fps)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, uint16\_t fps)
    :   set fps of sensor

    <a id="_CPPv4N19dvp_sensor_config_t10power_downE"></a>

    <a id="_CPPv3N19dvp_sensor_config_t10power_downE"></a> <a id="_CPPv2N19dvp_sensor_config_t10power_downE"></a> <a id="structdvp__sensor__config__t_1af24b705d486d3387b61f1c9de7bcfa4a"></a> avdk\_err\_t (\*power\_down)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller)
    :   power down or reset of sensor

<a id="_CPPv415bk_dvp_config_t"></a>

<a id="_CPPv315bk_dvp_config_t"></a> <a id="_CPPv215bk_dvp_config_t"></a> <a id="bk_dvp_config_t"></a> <a id="structbk__dvp__config__t"></a> struct bk\_dvp\_config\_t

<a id="_CPPv417bk_dvp_callback_t"></a>

<a id="_CPPv317bk_dvp_callback_t"></a> <a id="_CPPv217bk_dvp_callback_t"></a> <a id="bk_dvp_callback_t"></a> <a id="structbk__dvp__callback__t"></a> struct bk\_dvp\_callback\_t

<a id="csi-camera-types"></a>

### CSI Camera Types

<a id="id21"></a>

#### Header File

- [bk\_csi\_camera\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_csi_camera_types.h)

<a id="id22"></a>

#### Structures

<a id="_CPPv419csi_sensor_config_t"></a>

<a id="_CPPv319csi_sensor_config_t"></a> <a id="_CPPv219csi_sensor_config_t"></a> <a id="csi_sensor_config_t"></a> <a id="structcsi__sensor__config__t"></a> struct csi\_sensor\_config\_t
:   csi sensor configure

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19csi_sensor_config_t4nameE"></a>

    <a id="_CPPv3N19csi_sensor_config_t4nameE"></a> <a id="_CPPv2N19csi_sensor_config_t4nameE"></a> <a id="csi_sensor_config_t::name__cP"></a> <a id="structcsi__sensor__config__t_1a4a477f677814ea53f457ec6079478173"></a> char \*name
    :   sensor name

    <a id="_CPPv4N19csi_sensor_config_t3clkE"></a>

    <a id="_CPPv3N19csi_sensor_config_t3clkE"></a> <a id="_CPPv2N19csi_sensor_config_t3clkE"></a> <a id="csi_sensor_config_t::clk__mclk_freq_t"></a> <a id="structcsi__sensor__config__t_1a3dbdcc48aeae57a007ea074d6043d5b8"></a> mclk\_freq\_t clk
    :   sensor work clk in config fps and ppi

    <a id="_CPPv4N19csi_sensor_config_t5vsyncE"></a>

    <a id="_CPPv3N19csi_sensor_config_t5vsyncE"></a> <a id="_CPPv2N19csi_sensor_config_t5vsyncE"></a> <a id="csi_sensor_config_t::vsync__sync_level_t"></a> <a id="structcsi__sensor__config__t_1aaae6fcc0c988808a1a17dc78fb5c7b02"></a> sync\_level\_t vsync
    :   sensor vsync active level

    <a id="_CPPv4N19csi_sensor_config_t5hsyncE"></a>

    <a id="_CPPv3N19csi_sensor_config_t5hsyncE"></a> <a id="_CPPv2N19csi_sensor_config_t5hsyncE"></a> <a id="csi_sensor_config_t::hsync__sync_level_t"></a> <a id="structcsi__sensor__config__t_1a7d6cf67f28ff5591111de5cb7050cad1"></a> sync\_level\_t hsync
    :   sensor hsync active level

    <a id="_CPPv4N19csi_sensor_config_t2idE"></a>

    <a id="_CPPv3N19csi_sensor_config_t2idE"></a> <a id="_CPPv2N19csi_sensor_config_t2idE"></a> <a id="csi_sensor_config_t::id__uint16_t"></a> <a id="structcsi__sensor__config__t_1a5d97830ab260807c1432a8bd1126f8ce"></a> uint16\_t id
    :   sensor type, sensor\_id\_t

    <a id="_CPPv4N19csi_sensor_config_t7addressE"></a>

    <a id="_CPPv3N19csi_sensor_config_t7addressE"></a> <a id="_CPPv2N19csi_sensor_config_t7addressE"></a> <a id="csi_sensor_config_t::address__uint16_t"></a> <a id="structcsi__sensor__config__t_1ac6c647666b252041273df86874a9e2a2"></a> uint16\_t address
    :   sensor write register address by i2c

    <a id="_CPPv4N19csi_sensor_config_t6detectE"></a>

    <a id="_CPPv3N19csi_sensor_config_t6detectE"></a> <a id="_CPPv2N19csi_sensor_config_t6detectE"></a> <a id="structcsi__sensor__config__t_1ad50e00014a362603e68e2c3053d547cf"></a> avdk\_err\_t (\*detect)([bk\_camera\_sensor\_handle\_t](#_CPPv425bk_camera_sensor_handle_t "bk_camera_sensor_handle_t") \*handle, [bk\_camera\_sensor\_config\_t](#_CPPv425bk_camera_sensor_config_t "bk_camera_sensor_config_t") \*config)
    :   auto detect used csi sensor

    <a id="_CPPv4N19csi_sensor_config_t4initE"></a>

    <a id="_CPPv3N19csi_sensor_config_t4initE"></a> <a id="_CPPv2N19csi_sensor_config_t4initE"></a> <a id="structcsi__sensor__config__t_1a2bfb9e62e3decb5e5652d3145c38def9"></a> avdk\_err\_t (\*init)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller)
    :   init csi sensor

    <a id="_CPPv4N19csi_sensor_config_t7set_ppiE"></a>

    <a id="_CPPv3N19csi_sensor_config_t7set_ppiE"></a> <a id="_CPPv2N19csi_sensor_config_t7set_ppiE"></a> <a id="structcsi__sensor__config__t_1aebb4c28753377172e443050c4184f464"></a> avdk\_err\_t (\*set\_ppi)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, uint16\_t width, uint16\_t height)
    :   set resolution of sensor

    <a id="_CPPv4N19csi_sensor_config_t7set_fpsE"></a>

    <a id="_CPPv3N19csi_sensor_config_t7set_fpsE"></a> <a id="_CPPv2N19csi_sensor_config_t7set_fpsE"></a> <a id="structcsi__sensor__config__t_1a9b67a6f8ee6a6330b20bc214735d8635"></a> avdk\_err\_t (\*set\_fps)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller, uint16\_t fps)
    :   set fps of sensor

    <a id="_CPPv4N19csi_sensor_config_t10power_downE"></a>

    <a id="_CPPv3N19csi_sensor_config_t10power_downE"></a> <a id="_CPPv2N19csi_sensor_config_t10power_downE"></a> <a id="structcsi__sensor__config__t_1a9b34bdce32f8128b91da2e442dfd7960"></a> avdk\_err\_t (\*power\_down)([bk\_camera\_sensor\_ctlr\_t](#_CPPv423bk_camera_sensor_ctlr_t "bk_camera_sensor_ctlr_t") \*controller)
    :   power down or reset of sensor

<a id="_CPPv415bk_csi_config_t"></a>

<a id="_CPPv315bk_csi_config_t"></a> <a id="_CPPv215bk_csi_config_t"></a> <a id="bk_csi_config_t"></a> <a id="structbk__csi__config__t"></a> struct bk\_csi\_config\_t

<a id="_CPPv417bk_csi_callback_t"></a>

<a id="_CPPv317bk_csi_callback_t"></a> <a id="_CPPv217bk_csi_callback_t"></a> <a id="bk_csi_callback_t"></a> <a id="structbk__csi__callback__t"></a> struct bk\_csi\_callback\_t

<a id="id23"></a>

### UVC Camera

<a id="id24"></a>

#### Header File

- [bk\_uvc\_camera.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_uvc_camera.h)

<a id="id25"></a>

#### Functions

<a id="_CPPv415bk_uvc_ctrl_newP20bk_uvc_ctlr_handle_tPK17bk_uvc_callback_t"></a>

<a id="_CPPv315bk_uvc_ctrl_newP20bk_uvc_ctlr_handle_tPK17bk_uvc_callback_t"></a> <a id="_CPPv215bk_uvc_ctrl_newP20bk_uvc_ctlr_handle_tPK17bk_uvc_callback_t"></a> <a id="bk_uvc_ctrl_new__bk_uvc_ctlr_handle_tP.bk_uvc_callback_tCP"></a> <a id="bk__uvc__camera_8h_1af7f46683ec4c4c63a4091473817f9acb"></a> avdk\_err\_t bk\_uvc\_ctrl\_new([bk\_uvc\_ctlr\_handle\_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") \*handle, const [bk\_uvc\_callback\_t](#_CPPv417bk_uvc_callback_t "bk_uvc_callback_t") \*callbacks)
:   Create a new UVC controller instance.

    Allocates and initialises an abstract controller object. Callbacks are stored internally and invoked when frames are allocated, released, or when the UVC device changes state.

    参数
    :   - **handle** – **\[out\]** Pointer that receives the newly created controller handle
        - **callbacks** – **\[in\]** Application provided callback hooks (frame allocation, completion, state changes)

    返回
    :   - AVDK\_ERR\_OK: controller created successfully
        - others: other errors.

<a id="_CPPv411bk_uvc_init20bk_uvc_ctlr_handle_t"></a>

<a id="_CPPv311bk_uvc_init20bk_uvc_ctlr_handle_t"></a> <a id="_CPPv211bk_uvc_init20bk_uvc_ctlr_handle_t"></a> <a id="bk_uvc_init__bk_uvc_ctlr_handle_t"></a> <a id="bk__uvc__camera_8h_1aa5d6c5d7b5a3c1828732c7da7969f062"></a> avdk\_err\_t bk\_uvc\_init([bk\_uvc\_ctlr\_handle\_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Initialize the UVC controller hardware and resources.

    Must be called before opening a device. The controller configures clocks, endpoints and any other hardware level state needed to communicate with a UVC camera.

    参数
    :   **handle** – Controller handle obtained from bk\_uvc\_ctrl\_new

    返回
    :   - AVDK\_ERR\_OK: initialization success
        - others: other errors.

<a id="_CPPv413bk_uvc_deinit20bk_uvc_ctlr_handle_t"></a>

<a id="_CPPv313bk_uvc_deinit20bk_uvc_ctlr_handle_t"></a> <a id="_CPPv213bk_uvc_deinit20bk_uvc_ctlr_handle_t"></a> <a id="bk_uvc_deinit__bk_uvc_ctlr_handle_t"></a> <a id="bk__uvc__camera_8h_1a149fd3e818b834d9c353c8bf03d18b0f"></a> avdk\_err\_t bk\_uvc\_deinit([bk\_uvc\_ctlr\_handle\_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Deinitialize the UVC controller and release resources.

    Reverses bk\_uvc\_init by powering down hardware resources and freeing controller level allocations. The controller can be initialised again after this call.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK\_ERR\_OK: deinitialisation success
        - others: other errors.

<a id="_CPPv411bk_uvc_open20bk_uvc_ctlr_handle_tP19bk_cam_uvc_config_t"></a>

<a id="_CPPv311bk_uvc_open20bk_uvc_ctlr_handle_tP19bk_cam_uvc_config_t"></a> <a id="_CPPv211bk_uvc_open20bk_uvc_ctlr_handle_tP19bk_cam_uvc_config_t"></a> <a id="bk_uvc_open__bk_uvc_ctlr_handle_t.bk_cam_uvc_config_tP"></a> <a id="bk__uvc__camera_8h_1a2c841e0ad0067960c0efc40494639ca4"></a> avdk\_err\_t bk\_uvc\_open([bk\_uvc\_ctlr\_handle\_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle, [bk\_cam\_uvc\_config\_t](#_CPPv419bk_cam_uvc_config_t "bk_cam_uvc_config_t") \*config)
:   Open a UVC device using the provided configuration.

    Applies stream parameters such as image format, resolution and frame rate, then arms the controller to start receiving data from the device.

    参数
    :   - **handle** – Controller handle
        - **config** – Runtime configuration describing format, resolution, FPS, etc.

    返回
    :   - AVDK\_ERR\_OK: device opened successfully
        - others: other errors.

<a id="_CPPv412bk_uvc_close20bk_uvc_ctlr_handle_t"></a>

<a id="_CPPv312bk_uvc_close20bk_uvc_ctlr_handle_t"></a> <a id="_CPPv212bk_uvc_close20bk_uvc_ctlr_handle_t"></a> <a id="bk_uvc_close__bk_uvc_ctlr_handle_t"></a> <a id="bk__uvc__camera_8h_1a57430281fde5e7092fda5c6b599ad66c"></a> avdk\_err\_t bk\_uvc\_close([bk\_uvc\_ctlr\_handle\_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Close the currently opened UVC device.

    Stops streaming, flushes pending transfers and releases device specific resources. After calling close, the controller can be opened again with a new configuration.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK\_ERR\_OK: device closed successfully
        - others: other errors.

<a id="_CPPv414bk_uvc_suspend20bk_uvc_ctlr_handle_t"></a>

<a id="_CPPv314bk_uvc_suspend20bk_uvc_ctlr_handle_t"></a> <a id="_CPPv214bk_uvc_suspend20bk_uvc_ctlr_handle_t"></a> <a id="bk_uvc_suspend__bk_uvc_ctlr_handle_t"></a> <a id="bk__uvc__camera_8h_1ae3478915d46cb014b262425779e273c7"></a> avdk\_err\_t bk\_uvc\_suspend([bk\_uvc\_ctlr\_handle\_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Suspend the UVC controller (used for low-power management)

    Places the controller in a low-power state. Streaming must be stopped prior to suspension.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK\_ERR\_OK: controller suspended successfully
        - others: other errors.

<a id="_CPPv413bk_uvc_resume20bk_uvc_ctlr_handle_t"></a>

<a id="_CPPv313bk_uvc_resume20bk_uvc_ctlr_handle_t"></a> <a id="_CPPv213bk_uvc_resume20bk_uvc_ctlr_handle_t"></a> <a id="bk_uvc_resume__bk_uvc_ctlr_handle_t"></a> <a id="bk__uvc__camera_8h_1a70c6b6aba415e3b16b78357988cbd895"></a> avdk\_err\_t bk\_uvc\_resume([bk\_uvc\_ctlr\_handle\_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Resume the UVC controller after a suspend operation.

    Restores controller state saved during suspend so that streaming can be restarted.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK\_ERR\_OK: controller resumed successfully
        - others: other errors.

<a id="_CPPv412bk_uvc_ioctl20bk_uvc_ctlr_handle_t8uint32_tPv"></a>

<a id="_CPPv312bk_uvc_ioctl20bk_uvc_ctlr_handle_t8uint32_tPv"></a> <a id="_CPPv212bk_uvc_ioctl20bk_uvc_ctlr_handle_t8uint32_tPv"></a> <a id="bk_uvc_ioctl__bk_uvc_ctlr_handle_t.uint32_t.voidP"></a> <a id="bk__uvc__camera_8h_1a97762cc532110c6d912eee423e7e017a"></a> avdk\_err\_t bk\_uvc\_ioctl([bk\_uvc\_ctlr\_handle\_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle, uint32\_t event, void \*arg)
:   Issue a controller-specific IOCTL command.

    Provides access to extended control paths that are not covered by the standard open/close/suspend/resume APIs.

    参数
    :   - **handle** – Controller handle
        - **event** – IOCTL command identifier
        - **arg** – Optional argument pointer associated with the command

    返回
    :   - AVDK\_ERR\_OK: IOCTL executed successfully
        - others: other errors.

<a id="_CPPv413bk_uvc_delete20bk_uvc_ctlr_handle_t"></a>

<a id="_CPPv313bk_uvc_delete20bk_uvc_ctlr_handle_t"></a> <a id="_CPPv213bk_uvc_delete20bk_uvc_ctlr_handle_t"></a> <a id="bk_uvc_delete__bk_uvc_ctlr_handle_t"></a> <a id="bk__uvc__camera_8h_1ad822ba1669835b07af49db65ce4a00f6"></a> avdk\_err\_t bk\_uvc\_delete([bk\_uvc\_ctlr\_handle\_t](#_CPPv420bk_uvc_ctlr_handle_t "bk_uvc_ctlr_handle_t") handle)
:   Destroy a controller instance created by bk\_uvc\_ctrl\_new.

    This API releases the handle and any residual resources created by the controller constructor.

    参数
    :   **handle** – Controller handle

    返回
    :   - AVDK\_ERR\_OK: deletion success
        - others: other errors.

<a id="_CPPv440bk_uvc_register_separate_packet_callbackP21uvc_separate_config_t"></a>

<a id="_CPPv340bk_uvc_register_separate_packet_callbackP21uvc_separate_config_t"></a> <a id="_CPPv240bk_uvc_register_separate_packet_callbackP21uvc_separate_config_t"></a> <a id="bk_uvc_register_separate_packet_callback__uvc_separate_config_tP"></a> <a id="bk__uvc__camera_8h_1a15f909a4106852a4a40d6f5cf8cac618"></a> avdk\_err\_t bk\_uvc\_register\_separate\_packet\_callback([uvc\_separate\_config\_t](#_CPPv421uvc_separate_config_t "uvc_separate_config_t") \*cb)
:   register separate packet cb

    This API will register separate packet data, some uvc device a endpoint will output mjpeg and h264 data meantime, need register this callback

    参数
    :   **cb** – @attation 1\. this api called before bk\_uvc\_init, not all uvc need register

    返回
    :   - AVDK\_ERR\_OK: set success
        - others: other errors.

<a id="uvc-camera-types"></a>

### UVC Camera Types

<a id="id26"></a>

#### Header File

- [bk\_uvc\_camera\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_uvc_camera_types.h)

<a id="id27"></a>

#### Structures

<a id="_CPPv427bk_uvc_skip_frames_config_t"></a>

<a id="_CPPv327bk_uvc_skip_frames_config_t"></a> <a id="_CPPv227bk_uvc_skip_frames_config_t"></a> <a id="bk_uvc_skip_frames_config_t"></a> <a id="structbk__uvc__skip__frames__config__t"></a> struct bk\_uvc\_skip\_frames\_config\_t
:   Skip-frames config for BK\_UVC\_IOCTL\_SET\_SKIP\_FRAMES.

    Issue after bk\_uvc\_init and before bk\_uvc\_open for the target port.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N27bk_uvc_skip_frames_config_t4portE"></a>

    <a id="_CPPv3N27bk_uvc_skip_frames_config_t4portE"></a> <a id="_CPPv2N27bk_uvc_skip_frames_config_t4portE"></a> <a id="bk_uvc_skip_frames_config_t::port__uint8_t"></a> <a id="structbk__uvc__skip__frames__config__t_1a479a574018be2ec5bfc63228703164d8"></a> uint8\_t port
    :   UVC port id (1-based)

    <a id="_CPPv4N27bk_uvc_skip_frames_config_t5countE"></a>

    <a id="_CPPv3N27bk_uvc_skip_frames_config_t5countE"></a> <a id="_CPPv2N27bk_uvc_skip_frames_config_t5countE"></a> <a id="bk_uvc_skip_frames_config_t::count__uint8_t"></a> <a id="structbk__uvc__skip__frames__config__t_1ab27fa72aa06b053f659599bd94e9dbab"></a> uint8\_t count
    :   Drop first N frames after open (AE warmup), 0 \= disabled

<a id="_CPPv419uvc_separate_info_t"></a>

<a id="_CPPv319uvc_separate_info_t"></a> <a id="_CPPv219uvc_separate_info_t"></a> <a id="uvc_separate_info_t"></a> <a id="structuvc__separate__info__t"></a> struct uvc\_separate\_info\_t
:   Auxiliary information returned by a frame separation callback.

    When a JPEG or H.26x frame spans multiple packets, the separation callback can report how much valid data remains to be processed.

    - data\_len: number of valid bytes observed in the current packet.
    - data\_off: pointer to the first valid byte within the packet buffer.

<a id="_CPPv419bk_cam_uvc_config_t"></a>

<a id="_CPPv319bk_cam_uvc_config_t"></a> <a id="_CPPv219bk_cam_uvc_config_t"></a> <a id="bk_cam_uvc_config_t"></a> <a id="structbk__cam__uvc__config__t"></a> struct bk\_cam\_uvc\_config\_t
:   UVC camera runtime configuration parameters.

<a id="_CPPv417bk_uvc_callback_t"></a>

<a id="_CPPv317bk_uvc_callback_t"></a> <a id="_CPPv217bk_uvc_callback_t"></a> <a id="bk_uvc_callback_t"></a> <a id="structbk__uvc__callback__t"></a> struct bk\_uvc\_callback\_t
:   Callback hooks provided by the application to the UVC controller.

<a id="_CPPv411bk_uvc_ctlr"></a>

<a id="_CPPv311bk_uvc_ctlr"></a> <a id="_CPPv211bk_uvc_ctlr"></a> <a id="bk_uvc_ctlr"></a> <a id="structbk__uvc__ctlr"></a> struct bk\_uvc\_ctlr
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N11bk_uvc_ctlr4initE"></a>

    <a id="_CPPv3N11bk_uvc_ctlr4initE"></a> <a id="_CPPv2N11bk_uvc_ctlr4initE"></a> <a id="structbk__uvc__ctlr_1a3fe4da69b3930634ac5a72747b0a56da"></a> avdk\_err\_t (\*init)([bk\_uvc\_ctlr\_t](#_CPPv413bk_uvc_ctlr_t "bk_uvc_ctlr_t") \*controller)
    :   Initialize the controller and allocate resources

    <a id="_CPPv4N11bk_uvc_ctlr6deinitE"></a>

    <a id="_CPPv3N11bk_uvc_ctlr6deinitE"></a> <a id="_CPPv2N11bk_uvc_ctlr6deinitE"></a> <a id="structbk__uvc__ctlr_1ab2df566088f35ece4e336ce293aa3c12"></a> avdk\_err\_t (\*deinit)([bk\_uvc\_ctlr\_t](#_CPPv413bk_uvc_ctlr_t "bk_uvc_ctlr_t") \*controller)
    :   Deinitialize the controller

    <a id="_CPPv4N11bk_uvc_ctlr4openE"></a>

    <a id="_CPPv3N11bk_uvc_ctlr4openE"></a> <a id="_CPPv2N11bk_uvc_ctlr4openE"></a> <a id="structbk__uvc__ctlr_1a492654f86c10041cf441f7d100b8dfd2"></a> avdk\_err\_t (\*open)([bk\_uvc\_ctlr\_t](#_CPPv413bk_uvc_ctlr_t "bk_uvc_ctlr_t") \*controller, [bk\_cam\_uvc\_config\_t](#_CPPv419bk_cam_uvc_config_t "bk_cam_uvc_config_t") \*config)
    :   Open a UVC device with the supplied configuration

    <a id="_CPPv4N11bk_uvc_ctlr5closeE"></a>

    <a id="_CPPv3N11bk_uvc_ctlr5closeE"></a> <a id="_CPPv2N11bk_uvc_ctlr5closeE"></a> <a id="structbk__uvc__ctlr_1a68a9819229e62a9559173b0116635bb5"></a> avdk\_err\_t (\*close)([bk\_uvc\_ctlr\_t](#_CPPv413bk_uvc_ctlr_t "bk_uvc_ctlr_t") \*controller)
    :   Close the active UVC device

    <a id="_CPPv4N11bk_uvc_ctlr7suspendE"></a>

    <a id="_CPPv3N11bk_uvc_ctlr7suspendE"></a> <a id="_CPPv2N11bk_uvc_ctlr7suspendE"></a> <a id="structbk__uvc__ctlr_1a052119d1a8ffc718bc61a1ad079adfa7"></a> avdk\_err\_t (\*suspend)([bk\_uvc\_ctlr\_t](#_CPPv413bk_uvc_ctlr_t "bk_uvc_ctlr_t") \*controller)
    :   Suspend the controller for power saving

    <a id="_CPPv4N11bk_uvc_ctlr6resumeE"></a>

    <a id="_CPPv3N11bk_uvc_ctlr6resumeE"></a> <a id="_CPPv2N11bk_uvc_ctlr6resumeE"></a> <a id="structbk__uvc__ctlr_1ab11a16bf5bc156b5e2608985db1e5abe"></a> avdk\_err\_t (\*resume)([bk\_uvc\_ctlr\_t](#_CPPv413bk_uvc_ctlr_t "bk_uvc_ctlr_t") \*controller)
    :   Resume controller operation after suspend

    <a id="_CPPv4N11bk_uvc_ctlr5ioctlE"></a>

    <a id="_CPPv3N11bk_uvc_ctlr5ioctlE"></a> <a id="_CPPv2N11bk_uvc_ctlr5ioctlE"></a> <a id="structbk__uvc__ctlr_1ab90325cef19d2649b83079be869bcd3b"></a> avdk\_err\_t (\*ioctl)([bk\_uvc\_ctlr\_t](#_CPPv413bk_uvc_ctlr_t "bk_uvc_ctlr_t") \*controller, [bk\_uvc\_ioctl\_cmd\_t](#_CPPv418bk_uvc_ioctl_cmd_t "bk_uvc_ioctl_cmd_t") event, void \*arg)
    :   Issue controller specific IOCTL command

    <a id="_CPPv4N11bk_uvc_ctlr3delE"></a>

    <a id="_CPPv3N11bk_uvc_ctlr3delE"></a> <a id="_CPPv2N11bk_uvc_ctlr3delE"></a> <a id="structbk__uvc__ctlr_1af762d467a8250d3f156a9ba2b61dc628"></a> avdk\_err\_t (\*del)([bk\_uvc\_ctlr\_t](#_CPPv413bk_uvc_ctlr_t "bk_uvc_ctlr_t") \*controller)
    :   Delete the controller instance

<a id="_CPPv421uvc_separate_config_t"></a>

<a id="_CPPv321uvc_separate_config_t"></a> <a id="_CPPv221uvc_separate_config_t"></a> <a id="uvc_separate_config_t"></a> <a id="structuvc__separate__config__t"></a> struct uvc\_separate\_config\_t
:   Per-device callbacks used to separate and process UVC payloads.

<a id="id28"></a>

#### Macros

<a id="c.UVC_PORT_MAX"></a>

<a id="bk__uvc__camera__types_8h_1a78750ec6a8cd9598fa8c901a778e5145"></a> UVC\_PORT\_MAX
:   Maximum number of UVC ports.

    This macro defines the maximum number of UVC ports supported, based on the USB host hub maximum external ports configuration.

<a id="c.MEDIA_UVC_MJPEG_864X480_30FPS_CONFIG"></a>

<a id="bk__uvc__camera__types_8h_1ab9ff3cb43a522f3b34c76f6682eafcd0"></a> MEDIA\_UVC\_MJPEG\_864X480\_30FPS\_CONFIG()

<a id="id29"></a>

#### Type Definitions

<a id="_CPPv420bk_uvc_ctlr_handle_t"></a>

<a id="_CPPv320bk_uvc_ctlr_handle_t"></a> <a id="_CPPv220bk_uvc_ctlr_handle_t"></a> <a id="bk_uvc_ctlr_handle_t"></a> <a id="bk__uvc__camera__types_8h_1a04101be8e9dab1e42fb1b68f25c57cf2"></a> typedef struct [bk\_uvc\_ctlr](#_CPPv411bk_uvc_ctlr "bk_uvc_ctlr") \*bk\_uvc\_ctlr\_handle\_t

<a id="_CPPv413bk_uvc_ctlr_t"></a>

<a id="_CPPv313bk_uvc_ctlr_t"></a> <a id="_CPPv213bk_uvc_ctlr_t"></a> <a id="bk_uvc_ctlr_t"></a> <a id="bk__uvc__camera__types_8h_1af994e7718c15ca364d40d3adf022c58c"></a> typedef struct [bk\_uvc\_ctlr](#_CPPv411bk_uvc_ctlr "bk_uvc_ctlr") bk\_uvc\_ctlr\_t

<a id="id30"></a>

#### Enumerations

<a id="_CPPv411uvc_state_t"></a>

<a id="_CPPv311uvc_state_t"></a> <a id="_CPPv211uvc_state_t"></a> <a id="bk__uvc__camera__types_8h_1afeafc7afde389eb278e73e40b1ac9a9c"></a> enum uvc\_state\_t
:   Enumeration of UVC connection states.

    *Values:*

    <a id="_CPPv4N11uvc_state_t13UVC_CONNECTEDE"></a>

    <a id="_CPPv3N11uvc_state_t13UVC_CONNECTEDE"></a> <a id="_CPPv2N11uvc_state_t13UVC_CONNECTEDE"></a> <a id="bk__uvc__camera__types_8h_1afeafc7afde389eb278e73e40b1ac9a9caf5af4d81cece0fd60cfc110907a809af"></a> enumerator UVC\_CONNECTED
    :   Device is connected and streaming capable

    <a id="_CPPv4N11uvc_state_t16UVC_DISCONNECTEDE"></a>

    <a id="_CPPv3N11uvc_state_t16UVC_DISCONNECTEDE"></a> <a id="_CPPv2N11uvc_state_t16UVC_DISCONNECTEDE"></a> <a id="bk__uvc__camera__types_8h_1afeafc7afde389eb278e73e40b1ac9a9cadfdeca0fbe0c9b889358be9ada674d65"></a> enumerator UVC\_DISCONNECTED
    :   Device has been disconnected

<a id="_CPPv418bk_uvc_ioctl_cmd_t"></a>

<a id="_CPPv318bk_uvc_ioctl_cmd_t"></a> <a id="_CPPv218bk_uvc_ioctl_cmd_t"></a> <a id="bk__uvc__camera__types_8h_1afd4c15343306dcc48abb4a1fe791a723"></a> enum bk\_uvc\_ioctl\_cmd\_t
:   *Values:*

    <a id="_CPPv4N18bk_uvc_ioctl_cmd_t20BK_UVC_IOCTL_UNKNOWNE"></a>

    <a id="_CPPv3N18bk_uvc_ioctl_cmd_t20BK_UVC_IOCTL_UNKNOWNE"></a> <a id="_CPPv2N18bk_uvc_ioctl_cmd_t20BK_UVC_IOCTL_UNKNOWNE"></a> <a id="bk__uvc__camera__types_8h_1afd4c15343306dcc48abb4a1fe791a723a985a165552e9dfb041f769d2485e8911"></a> enumerator BK\_UVC\_IOCTL\_UNKNOWN

    <a id="_CPPv4N18bk_uvc_ioctl_cmd_t28BK_UVC_IOCTL_SET_SKIP_FRAMESE"></a>

    <a id="_CPPv3N18bk_uvc_ioctl_cmd_t28BK_UVC_IOCTL_SET_SKIP_FRAMESE"></a> <a id="_CPPv2N18bk_uvc_ioctl_cmd_t28BK_UVC_IOCTL_SET_SKIP_FRAMESE"></a> <a id="bk__uvc__camera__types_8h_1afd4c15343306dcc48abb4a1fe791a723aa0917db543719d0d186483ba84280c11"></a> enumerator BK\_UVC\_IOCTL\_SET\_SKIP\_FRAMES
    :   Set skip\_frames for a port before bk\_uvc\_open; arg \= [bk\_uvc\_skip\_frames\_config\_t](#structbk__uvc__skip__frames__config__t) \*
