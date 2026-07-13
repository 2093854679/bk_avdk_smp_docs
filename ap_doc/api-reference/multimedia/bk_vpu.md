# VPU（视频编解码）



## 概述

BK7259 **VPU** 硬件 H.264 / JPEG 编解码通过 `bk_decoder` / `bk_encoder` 组件的统一控制器 API 对外提供。


- 开发者指南：[VPU 开发者指南](../../developer-guide/vpu.md "../../developer-guide/vpu.md")

- Frame 与 Flexa：[Frame 与 Flexa 模式](../../developer-guide/vpu/flexa_frame.md "../../developer-guide/vpu/flexa_frame.md")

示例工程：

| 能力 | 工程 |
| --- | --- |
| H.264 解码 | `multimedia/h264d_gpu_display_example` |
| H.264 编码 | `multimedia/h264_encode_example` |
| JPEG 解码 | `multimedia/jpeg_decode_example` |
| JPEG 编码 | `multimedia/jpeg_encode_example` |

Kconfig 选项：`CONFIG_BK_DECODER` 与 `CONFIG_BK_ENCODER`。


## H.264 解码

头文件：`ap/include/components/bk_decode/bk_h264_decode_ctlr.h`

创建接口（三选一）：


- `bk_h264_decode_frame_ctlr_new` — Frame 整帧模式（非 B）

- `bk_h264_decode_frame_zerocopy_ctlr_new` — Frame 零拷贝整帧模式

- `bk_h264_decode_flexa_ctlr_new` — Flexa 分段模式（非 B）

生命周期：


```

*_ctlr_new → bk_h264_decode_init → bk_h264_decode_open
→ bk_h264_decode_frame（每帧/每 AU）
→ bk_h264_decode_close → bk_h264_decode_deinit → bk_h264_decode_delete

```

其他接口：


- `bk_h264_decode_ioctl` — Bond、中止、读指针（`BK_H264_DECODE_IOCTL_REGISTER_BOND` 等）

- `bk_h264_decode_get_info` — 码流/帧信息

输入结构：``` bk_h264_decode_input_t``（``stream ```、`stream_len`、`out_buffer`、`out_buffer_size`）。

Frame 零拷贝整帧模式（`bk_h264_decode_frame_zerocopy_ctlr_new`）：


- 唯一能解码含 B 帧（Main Profile IBBP）码流的控制器，内部帧池实现零拷贝，并按 POC 做显示重排。

- 使用专用配置 ``` bk_h264_decode_frame_zerocopy_config_t``（与 ``bk_h264_decode_frame_config_t ``` 解耦）；`disp_depth` 为应用层可额外持有的显示 slot 数（1..4，`0` 取默认 2）。

- 输入的 `out_buffer` / `out_buffer_size` 被忽略；解码帧改为通过 IOCTL 交付：


  - ``` BK_H264_DECODE_IOCTL_DEQUEUE``（``bk_h264_decode_dequeue_t* ```）— 按显示顺序取一帧

  - ``` BK_H264_DECODE_IOCTL_RELEASE``（``bk_h264_decode_out_frame_t* ```）— 归还一帧（每帧仅一次）

  - ``` BK_H264_DECODE_IOCTL_FLUSH``（``NULL ```）— EOS 时冲刷尾部重排帧


## H.264 编码

头文件：`ap/include/components/bk_encode/bk_h264_encode_ctlr.h`

创建接口（三选一）：


- `bk_h264_encode_frame_new` — Frame 模式

- `bk_h264_encode_hw_flexa_new` — 硬件 Flexa

- `bk_h264_encode_sw_flexa_new` — 软件 Flexa

生命周期：


```

*_new → bk_h264_encode_init → bk_h264_encode_open → bk_h264_encode_start
→ bk_h264_encode_close → bk_h264_encode_deinit → bk_h264_encode_delete

```

码率 / GOP：


- `bk_h264_encode_set_rate_ctrl` / `bk_h264_encode_get_rate_ctrl`

- `bk_h264_encode_set_gop_frame_count` / `bk_h264_encode_get_gop_frame_count`

- `bk_h264_encode_force_idr`

- `bk_h264_encode_ioctl` — Flexa 行通知、Bond、调试

输出通过配置中的 `outbuf_malloc` / `outbuf_complete` 回调交付。


## JPEG 解码

头文件：`ap/include/components/bk_decode/bk_jpeg_decode_ctlr.h`

创建接口：


- `bk_jpeg_decode_frame_ctlr_new` — Frame 模式

- `bk_jpeg_decode_flexa_ctlr_new` — Flexa 模式

生命周期：


```

*_ctlr_new → bk_jpeg_decode_init → bk_jpeg_decode_open
→ bk_jpeg_decode_frame
→ bk_jpeg_decode_close → bk_jpeg_decode_deinit → bk_jpeg_decode_delete

```

其他：


- `bk_jpeg_decode_ioctl` — Bond、读指针、图像信息

- `bk_jpeg_decode_get_img_info` — 不解码完整图像，仅解析 JPEG 头


## JPEG 编码

头文件：`ap/include/components/bk_encode/bk_jpeg_encode_ctlr.h`

创建接口：


- `bk_jpeg_encode_frame_new` — Frame 模式

- `bk_jpeg_encode_hw_flexa_new` — 硬件 Flexa

- `bk_jpeg_encode_sw_flexa_new` — 软件 Flexa

生命周期：


```

*_new → bk_jpeg_encode_init → bk_jpeg_encode_open
→ bk_jpeg_encode_frame
→ bk_jpeg_encode_close → bk_jpeg_encode_deinit → bk_jpeg_encode_delete

```


- `bk_jpeg_encode_ioctl` — 质量（`BK_JPEG_ENCODE_IOCTL_SET_QUALITY`）、Flexa 行通知


## Flexa Bond

Flexa 流水线通过 `bk_flexa_bond` 系列 API 将解码/编码端口与 GPU、H264E、ISP 等绑核。

类型定义：`ap/components/media_service/include/bk_flexa_bond_types.h`

通过编解码控制器的 `ioctl` 接口 `REGISTER_BOND` 命令注册。

参考 `h264d_gpu_display_demo.c` 中的 `bk_flexa_h264d_gpu_bond_start`。


## API Reference


### H.264 Decode


#### Header File


- [bk_h264_decode_ctlr.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_h264_decode_ctlr.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_h264_decode_ctlr.h")


#### Functions

avdk_err_t bk_h264_decode_flexa_ctlr_new([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") *handle, [bk_h264_decode_flexa_config_t](#_CPPv429bk_h264_decode_flexa_config_t "bk_h264_decode_flexa_config_t") *config)
:   Create a Flexa-mode H.264 decoder controller.

    参数
    :   - **handle** – Output pointer that receives the decoder handle

        - **config** – Flexa decoder configuration

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_frame_ctlr_new([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") *handle, [bk_h264_decode_frame_config_t](#_CPPv429bk_h264_decode_frame_config_t "bk_h264_decode_frame_config_t") *config)
:   Create a frame-mode H.264 decoder controller.

    参数
    :   - **handle** – Output pointer that receives the decoder handle

        - **config** – Frame decoder configuration

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_frame_zerocopy_ctlr_new([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") *handle, [bk_h264_decode_frame_zerocopy_config_t](#_CPPv438bk_h264_decode_frame_zerocopy_config_t "bk_h264_decode_frame_zerocopy_config_t") *config)
:   Create a zero-copy / B-frame capable whole-frame H.264 decoder controller.

    Like bk_h264_decode_frame_ctlr_new() it decodes one access unit per bk_h264_decode_frame() call, but it owns an internal zero-copy frame pool: one physical buffer serves as decode target / DPB reference / display output, eliminating the reference-backup and output copies and enabling B-frame decoding with POC-based display reordering. The per-frame output buffer in [bk_h264_decode_input_t](#structbk__h264__decode__input__t "#structbk__h264__decode__input__t") is ignored; decoded frames are pulled in display order via BK_H264_DECODE_IOCTL_DEQUEUE and returned via BK_H264_DECODE_IOCTL_RELEASE, with BK_H264_DECODE_IOCTL_FLUSH emitting trailing reordered pictures at EOS.

    参数
    :   - **handle** – Output pointer that receives the decoder handle

        - **config** – Zero-copy frame decoder configuration (disp_depth applies here)

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_init([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Initialize the H.264 decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_deinit([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Deinitialize the H.264 decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_open([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Open the H.264 decoder for decoding.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_close([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Close the H.264 decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_frame([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle, [bk_h264_decode_input_t](#_CPPv422bk_h264_decode_input_t "bk_h264_decode_input_t") *input)
:   Decode one H.264 access unit or frame.

    参数
    :   - **handle** – Decoder handle

        - **input** – Input bitstream and output buffer descriptors

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_ioctl([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle, [bk_h264_decode_ioctl_cmd_t](#_CPPv426bk_h264_decode_ioctl_cmd_t "bk_h264_decode_ioctl_cmd_t") cmd, void *arg)
:   Issue an IOCTL command on the H.264 decoder.

    参数
    :   - **handle** – Decoder handle

        - **cmd** – IOCTL command

        - **arg** – Command-specific argument

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_delete([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Delete the H.264 decoder controller.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_h264_decode_get_info([bk_h264_decode_ctlr_handle_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle, [bk_h264_decode_info_t](#_CPPv421bk_h264_decode_info_t "bk_h264_decode_info_t") *info)
:   Get decoded stream or frame metadata.

    参数
    :   - **handle** – Decoder handle

        - **info** – Output structure for stream/frame info

    返回
    :   AVDK error code


### H.264 Decode Types


#### Header File


- [bk_h264_decode_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_h264_decode_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_h264_decode_types.h")


#### Structures

struct bk_h264_decode_port_rd_t

struct bk_h264_decode_frame_config_t

struct bk_h264_decode_frame_zerocopy_config_t

struct bk_h264_decode_flexa_config_t

struct bk_h264_decode_input_t

struct bk_h264_decode_out_frame_t

struct bk_h264_decode_dequeue_t

struct bk_h264_decode_ctlr_t


#### Macros

BK_H264_DECODE_RD_PORT_MAX

DEFAULT_H264_DECODE_FLEXA_CONFIG

DEFAULT_H264_DECODE_FRAME_CONFIG

DEFAULT_H264_DECODE_FRAME_ZEROCOPY_CONFIG


#### Type Definitions

typedef void (*bk_h264_decode_frame_done_cb)(int status, void *args)

typedef void (*bk_h264_decode_flexa_done_cb)(uint32_t wr_ptr, void *args)

typedef vcdec_h264_frame_type_t bk_h264_decode_frame_type_t

typedef vcdec_h264_info_t bk_h264_decode_info_t

typedef struct [bk_h264_decode_ctlr_t](#_CPPv421bk_h264_decode_ctlr_t "bk_h264_decode_ctlr_t") *bk_h264_decode_ctlr_handle_t


#### Enumerations

enum bk_h264_decode_ioctl_cmd_t
:   *Values:*

    enumerator BK_H264_DECODE_IOCTL_GET_INFO

    enumerator BK_H264_DECODE_IOCTL_ABORT

    enumerator BK_H264_DECODE_IOCTL_PORT_SET_RD_PTR

    enumerator BK_H264_DECODE_IOCTL_REGISTER_BOND

    enumerator BK_H264_DECODE_IOCTL_UNREGISTER_BOND

    enumerator BK_H264_DECODE_IOCTL_FLEXA_NOTIFY_PORT_DONE

    enumerator BK_H264_DECODE_IOCTL_RESET

    enumerator BK_H264_DECODE_IOCTL_DEQUEUE

    enumerator BK_H264_DECODE_IOCTL_RELEASE

    enumerator BK_H264_DECODE_IOCTL_FLUSH

enum bk_h264_decode_rd_port_id_t
:   *Values:*

    enumerator BK_H264_DECODE_RD_PORT_GPU

    enumerator BK_H264_DECODE_RD_PORT_H264E


### H.264 Encode


#### Header File


- [bk_h264_encode_ctlr.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_h264_encode_ctlr.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_h264_encode_ctlr.h")


#### Functions

avdk_err_t bk_h264_encode_hw_flexa_new([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") *handle, [bk_h264_encode_hw_flexa_config_t](#_CPPv432bk_h264_encode_hw_flexa_config_t "bk_h264_encode_hw_flexa_config_t") *config)
:   Create a new hardware flexa encoder.

    参数
    :   - **handle** – Encoder handle

        - **config** – Hardware flexa configuration

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_sw_flexa_new([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") *handle, [bk_h264_encode_sw_flexa_config_t](#_CPPv432bk_h264_encode_sw_flexa_config_t "bk_h264_encode_sw_flexa_config_t") *config)
:   Create a new software flexa encoder.

    参数
    :   - **handle** – Encoder handle

        - **config** – Software flexa configuration

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_frame_new([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") *handle, [bk_h264_encode_frame_config_t](#_CPPv429bk_h264_encode_frame_config_t "bk_h264_encode_frame_config_t") *config)
:   Create a new frame encoder.

    参数
    :   - **handle** – Encoder handle

        - **config** – Frame configuration

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_init([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Initialize encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_deinit([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Deinitialize encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_open([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Open encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_close([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Close encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_start([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Execute encoding.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_ioctl([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, [bk_h264_encode_ioctl_cmd_t](#_CPPv426bk_h264_encode_ioctl_cmd_t "bk_h264_encode_ioctl_cmd_t") cmd, void *arg)
:   Control interface.

    参数
    :   - **handle** – Encoder handle

        - **cmd** – Command

        - **arg** – Argument

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_force_idr([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Force IDR frame generation.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_set_gop_frame_count([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, uint32_t gop_frame_count)
:   Configure GOP frame count.

    参数
    :   - **handle** – Encoder handle

        - **gop_frame_count** – Number of frames in one GOP

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_get_gop_frame_count([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, uint32_t *gop_frame_count)
:   Get GOP frame count.

    参数
    :   - **handle** – Encoder handle

        - **gop_frame_count** – Output GOP frame count

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_set_rate_ctrl([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, [bk_h264_encode_rate_ctrl_t](#_CPPv426bk_h264_encode_rate_ctrl_t "bk_h264_encode_rate_ctrl_t") *rate_ctrl)
:   Configure rate control.

    参数
    :   - **handle** – Encoder handle

        - **rate_ctrl** – Rate control config

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_get_rate_ctrl([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, [bk_h264_encode_rate_ctrl_t](#_CPPv426bk_h264_encode_rate_ctrl_t "bk_h264_encode_rate_ctrl_t") *rate_ctrl)
:   Get rate control config.

    参数
    :   - **handle** – Encoder handle

        - **rate_ctrl** – Output rate control config

    返回
    :   AVSDK error code

avdk_err_t bk_h264_encode_delete([bk_h264_encode_ctlr_handle_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Delete encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code


### H.264 Encode Types


#### Header File


- [bk_h264_encode_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_h264_encode_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_h264_encode_types.h")


#### Structures

struct bk_h264_encode_rate_ctrl_t

struct bk_h264_encode_outbuf_info_t

struct bk_h264_encode_frame_config_t

struct bk_h264_encode_hw_flexa_config_t

struct bk_h264_encode_sw_flexa_config_t

struct bk_h264_encode_ctlr_t


#### Type Definitions

typedef struct [bk_h264_encode_ctlr_t](#_CPPv421bk_h264_encode_ctlr_t "bk_h264_encode_ctlr_t") *bk_h264_encode_ctlr_handle_t


#### Enumerations

enum flexa_stream_id_t
:   *Values:*

    enumerator FLEXA_STREAM_ID_Y

    enumerator FLEXA_STREAM_ID_CB

    enumerator FLEXA_STREAM_ID_CR

enum bk_h264_encode_ioctl_cmd_t
:   *Values:*

    enumerator BK_H264_ENCODE_IOCTL_DEBUG_START

    enumerator BK_H264_ENCODE_IOCTL_DEBUG_STOP

    enumerator BK_H264_ENCODE_IOCTL_SET_GOP_FRAME_COUNT

    enumerator BK_H264_ENCODE_IOCTL_GET_GOP_FRAME_COUNT

    enumerator BK_H264_ENCODE_IOCTL_SET_FLEXA_LINES_READY

    enumerator BK_H264_ENCODE_IOCTL_SET_FRAME_READY

    enumerator BK_H264_ENCODE_IOCTL_REGISTER_BOND

    enumerator BK_H264_ENCODE_IOCTL_UNREGISTER_BOND

    enumerator BK_H264_ENCODE_IOCTL_STOP_ENCODE

    enumerator BK_H264_ENCODE_IOCTL_SET_RATE_CTRL

    enumerator BK_H264_ENCODE_IOCTL_GET_RATE_CTRL

enum bk_h264_encode_flexa_mode_t
:   *Values:*

    enumerator BK_H264_ENCODE_FLEXA_MODE_NONE

    enumerator BK_H264_ENCODE_FLEXA_MODE_SOFTWARE

    enumerator BK_H264_ENCODE_FLEXA_MODE_HARDWARE


### JPEG Decode


#### Header File


- [bk_jpeg_decode_ctlr.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_jpeg_decode_ctlr.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_jpeg_decode_ctlr.h")


#### Functions

avdk_err_t bk_jpeg_decode_flexa_ctlr_new([bk_jpeg_decode_ctlr_handle_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") *handle, [bk_jpeg_decode_flexa_config_t](#_CPPv429bk_jpeg_decode_flexa_config_t "bk_jpeg_decode_flexa_config_t") *config)
:   Create a Flexa-mode JPEG decoder controller.

    参数
    :   - **handle** – Output pointer that receives the decoder handle

        - **config** – Flexa decoder configuration

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_decode_frame_ctlr_new([bk_jpeg_decode_ctlr_handle_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") *handle, [bk_jpeg_decode_frame_config_t](#_CPPv429bk_jpeg_decode_frame_config_t "bk_jpeg_decode_frame_config_t") *config)
:   Create a frame-mode JPEG decoder controller.

    参数
    :   - **handle** – Output pointer that receives the decoder handle

        - **config** – Frame decoder configuration

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_decode_init([bk_jpeg_decode_ctlr_handle_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Initialize the JPEG decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_decode_deinit([bk_jpeg_decode_ctlr_handle_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Deinitialize the JPEG decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_decode_open([bk_jpeg_decode_ctlr_handle_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Open the JPEG decoder for decoding.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_decode_close([bk_jpeg_decode_ctlr_handle_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Close the JPEG decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_decode_frame([bk_jpeg_decode_ctlr_handle_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle, [bk_jpeg_decode_input_t](#_CPPv422bk_jpeg_decode_input_t "bk_jpeg_decode_input_t") *input)
:   Decode one JPEG image.

    参数
    :   - **handle** – Decoder handle

        - **input** – Input bitstream and output buffer descriptors

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_decode_ioctl([bk_jpeg_decode_ctlr_handle_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle, [bk_jpeg_decode_ioctl_cmd_t](#_CPPv426bk_jpeg_decode_ioctl_cmd_t "bk_jpeg_decode_ioctl_cmd_t") cmd, void *arg)
:   Issue an IOCTL command on the JPEG decoder.

    参数
    :   - **handle** – Decoder handle

        - **cmd** – IOCTL command

        - **arg** – Command-specific argument

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_decode_delete([bk_jpeg_decode_ctlr_handle_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Delete the JPEG decoder controller.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_decode_get_img_info([bk_jpeg_decode_img_info_t](#_CPPv425bk_jpeg_decode_img_info_t "bk_jpeg_decode_img_info_t") *img_info)
:   Parse JPEG header and get image information without full decode.

    参数
    :   **img_info** – Input/output image info structure (contains JPEG bitstream pointer)

    返回
    :   AVDK error code


### JPEG Decode Types


#### Header File


- [bk_jpeg_decode_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_jpeg_decode_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_jpeg_decode_types.h")


#### Structures

struct bk_jpeg_decode_port_rd_t
:   this is for bond

struct bk_jpeg_decode_frame_config_t

struct bk_jpeg_decode_flexa_config_t

struct bk_jpeg_decode_input_t

struct bk_jpeg_decode_img_info

struct bk_jpeg_decode_ctlr_t


#### Macros

BK_JPEG_DECODE_RD_PORT_MAX

DEFAULT_JPEG_DECODE_FLEXA_CONFIG

DEFAULT_JPEG_DECODE_FRAME_CONFIG


#### Type Definitions

typedef void (*bk_jpeg_decode_frame_done_cb)(int status, void *args)
:   JPEG decode result callback: (status, args).

typedef void (*bk_jpeg_decode_flexa_done_cb)(uint32_t wr_ptr, void *args)
:   Flexa done callback: (wr_ptr, args).

typedef struct [bk_jpeg_decode_img_info](#_CPPv423bk_jpeg_decode_img_info "bk_jpeg_decode_img_info") bk_jpeg_decode_img_info_t

typedef struct [bk_jpeg_decode_ctlr_t](#_CPPv421bk_jpeg_decode_ctlr_t "bk_jpeg_decode_ctlr_t") *bk_jpeg_decode_ctlr_handle_t


#### Enumerations

enum bk_jpeg_decode_ioctl_cmd_t
:   *Values:*

    enumerator BK_JPEG_DECODE_IOCTL_GET_INFO
    :   Get image info see bk_jpeg_decode_img_info_t

    enumerator BK_JPEG_DECODE_IOCTL_ABORT
    :   Abort decode

    enumerator BK_JPEG_DECODE_IOCTL_PORT_SET_RD_PTR
    :   Set read pointer see [bk_jpeg_decode_port_rd_t](#structbk__jpeg__decode__port__rd__t "#structbk__jpeg__decode__port__rd__t")

    enumerator BK_JPEG_DECODE_IOCTL_REGISTER_BOND
    :   Register bond should be ptr for the bond

    enumerator BK_JPEG_DECODE_IOCTL_UNREGISTER_BOND
    :   Unregister bond should be ptr for the bond

    enumerator BK_JPEG_DECODE_IOCTL_FLEXA_NOTIFY_PORT_DONE
    :   Notify port done should be ptr for the port

enum bk_jpeg_decode_rd_port_id_t
:   *Values:*

    enumerator BK_JPEG_DECODE_RD_PORT_GPU

    enumerator BK_JPEG_DECODE_RD_PORT_H264E

enum bk_jpeg_decode_flexa_mode_t
:   *Values:*

    enumerator BK_JPEG_DECODE_FLEXA_MODE_NONE

    enumerator BK_JPEG_DECODE_FLEXA_MODE_FLEXA

enum bk_jpeg_decode_img_fmt_t
:   *Values:*

    enumerator BK_JPEG_DECODE_IMG_FMT_ERR
    :   Invalid or unsupported image format

    enumerator BK_JPEG_DECODE_IMG_FMT_YUV444
    :   YUV 4:4:4 format - full chroma resolution, no subsampling

    enumerator BK_JPEG_DECODE_IMG_FMT_YUV422
    :   YUV 4:2:2 format - horizontal chroma subsampling by 2:1

    enumerator BK_JPEG_DECODE_IMG_FMT_YUV420
    :   YUV 4:2:0 format - horizontal and vertical chroma subsampling by 2:1

    enumerator BK_JPEG_DECODE_IMG_FMT_YUV400
    :   YUV 4:0:0 format - grayscale image with only luma component

    enumerator BK_JPEG_DECODE_IMG_FMT_MAX


### JPEG Encode


#### Header File


- [bk_jpeg_encode_ctlr.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_jpeg_encode_ctlr.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_jpeg_encode_ctlr.h")


#### Functions

avdk_err_t bk_jpeg_encode_frame_new([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") *handle, [bk_jpeg_encode_frame_config_t](#_CPPv429bk_jpeg_encode_frame_config_t "bk_jpeg_encode_frame_config_t") *config)
:   Create frame-mode JPEG encoder (VCENC JPEG path).

    参数
    :   - **handle** – Output pointer that receives the encoder handle

        - **config** – Frame encoder configuration

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_encode_hw_flexa_new([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") *handle, [bk_jpeg_encode_hw_flexa_config_t](#_CPPv432bk_jpeg_encode_hw_flexa_config_t "bk_jpeg_encode_hw_flexa_config_t") *config)
:   Create hardware-Flexa JPEG encoder (VCENC JPEG low-latency HW sync path).

    参数
    :   - **handle** – Output pointer that receives the encoder handle

        - **config** – Hardware Flexa encoder configuration

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_encode_sw_flexa_new([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") *handle, [bk_jpeg_encode_sw_flexa_config_t](#_CPPv432bk_jpeg_encode_sw_flexa_config_t "bk_jpeg_encode_sw_flexa_config_t") *config)
:   Create software-Flexa JPEG encoder (VCENC JPEG low-latency SW sync path).

    参数
    :   - **handle** – Output pointer that receives the encoder handle

        - **config** – Software Flexa encoder configuration

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_encode_init([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Initialize the JPEG encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_encode_deinit([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Deinitialize the JPEG encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_encode_open([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Open the JPEG encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_encode_close([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Close the JPEG encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_encode_frame([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle, [bk_jpeg_encode_input_t](#_CPPv422bk_jpeg_encode_input_t "bk_jpeg_encode_input_t") *input)
:   Encode one JPEG frame.

    参数
    :   - **handle** – Encoder handle

        - **input** – Input pixel buffer and output descriptors

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_encode_ioctl([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle, [bk_jpeg_encode_ioctl_cmd_t](#_CPPv426bk_jpeg_encode_ioctl_cmd_t "bk_jpeg_encode_ioctl_cmd_t") cmd, void *arg)
:   Issue an IOCTL command on the JPEG encoder.

    参数
    :   - **handle** – Encoder handle

        - **cmd** – IOCTL command (e.g. quality setting)

        - **arg** – Command-specific argument

    返回
    :   AVDK error code

avdk_err_t bk_jpeg_encode_delete([bk_jpeg_encode_ctlr_handle_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Delete the JPEG encoder controller.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code


### JPEG Encode Types


#### Header File


- [bk_jpeg_encode_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_jpeg_encode_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_jpeg_encode_types.h")


#### Structures

struct bk_jpeg_encode_outbuf_info_t

struct bk_jpeg_encode_frame_config_t

struct bk_jpeg_encode_hw_flexa_config_t

struct bk_jpeg_encode_sw_flexa_config_t

struct bk_jpeg_encode_input_t

struct bk_jpeg_encode_ctlr_t


#### Macros

DEFAULT_JPEG_ENCODE_FRAME_CONFIG

DEFAULT_JPEG_ENCODE_HW_FLEXA_CONFIG

DEFAULT_JPEG_ENCODE_SW_FLEXA_CONFIG


#### Type Definitions

typedef void (*bk_jpeg_encode_flexa_done_cb)(uint32_t rd_blocks, void *args)

typedef struct [bk_jpeg_encode_ctlr_t](#_CPPv421bk_jpeg_encode_ctlr_t "bk_jpeg_encode_ctlr_t") *bk_jpeg_encode_ctlr_handle_t


#### Enumerations

enum bk_jpeg_encode_ioctl_cmd_t
:   *Values:*

    enumerator BK_JPEG_ENCODE_IOCTL_SET_QUALITY
    :   arg: uint8_t * quality 0..10

    enumerator BK_JPEG_ENCODE_IOCTL_SET_FLEXA_LINES_READY
    :   Software Flexa: arg is block count cast to void *

    enumerator BK_JPEG_ENCODE_IOCTL_SET_FRAME_READY
    :   Software Flexa: notify one frame input is ready

    enumerator BK_JPEG_ENCODE_IOCTL_REGISTER_BOND
    :   arg: bk_flexa_bond_t *

    enumerator BK_JPEG_ENCODE_IOCTL_UNREGISTER_BOND
    :   arg: bk_flexa_bond_t *

    enumerator BK_JPEG_ENCODE_IOCTL_STOP_ENCODE
    :   stop current Flexa encode

enum bk_jpeg_encode_flexa_mode_t
:   *Values:*

    enumerator BK_JPEG_ENCODE_FLEXA_MODE_NONE

    enumerator BK_JPEG_ENCODE_FLEXA_MODE_SOFTWARE

    enumerator BK_JPEG_ENCODE_FLEXA_MODE_HARDWARE
