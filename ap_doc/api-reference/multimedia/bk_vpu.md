---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/multimedia/bk_vpu.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="vpu"></a>

# VPU（视频编解码）

<a id="id1"></a>

## 概述

BK7259 **VPU** 硬件 H.264 / JPEG 编解码通过 `bk_decoder` / `bk_encoder` 组件的统一控制器 API 对外提供。

- 开发者指南：[VPU 开发者指南](../../developer-guide/vpu.md)
- Frame 与 Flexa：[Frame 与 Flexa 模式](../../developer-guide/vpu/flexa_frame.md)

示例工程：

| 能力 | 工程 |
| --- | --- |
| H.264 解码 | `multimedia/h264d_gpu_display_example` |
| H.264 编码 | `multimedia/h264_encode_example` |
| JPEG 解码 | `multimedia/jpeg_decode_example` |
| JPEG 编码 | `multimedia/jpeg_encode_example` |

Kconfig 选项：`CONFIG_BK_DECODER` 与 `CONFIG_BK_ENCODER`。

<a id="h-264"></a>

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

<a id="id3"></a>

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

<a id="jpeg"></a>

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

<a id="id4"></a>

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

<a id="flexa-bond"></a>

## Flexa Bond

Flexa 流水线通过 `bk_flexa_bond` 系列 API 将解码/编码端口与 GPU、H264E、ISP 等绑核。

类型定义：`ap/components/media_service/include/bk_flexa_bond_types.h`

通过编解码控制器的 `ioctl` 接口 `REGISTER_BOND` 命令注册。

参考 `h264d_gpu_display_demo.c` 中的 `bk_flexa_h264d_gpu_bond_start`。

<a id="api-reference"></a>

## API Reference

<a id="h-264-decode"></a>

### H.264 Decode

<a id="header-file"></a>

#### Header File

- [bk\_h264\_decode\_ctlr.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_decode/bk_h264_decode_ctlr.h)

<a id="functions"></a>

#### Functions

<a id="_CPPv429bk_h264_decode_flexa_ctlr_newP28bk_h264_decode_ctlr_handle_tP29bk_h264_decode_flexa_config_t"></a>

<a id="_CPPv329bk_h264_decode_flexa_ctlr_newP28bk_h264_decode_ctlr_handle_tP29bk_h264_decode_flexa_config_t"></a> <a id="_CPPv229bk_h264_decode_flexa_ctlr_newP28bk_h264_decode_ctlr_handle_tP29bk_h264_decode_flexa_config_t"></a> <a id="bk_h264_decode_flexa_ctlr_new__bk_h264_decode_ctlr_handle_tP.bk_h264_decode_flexa_config_tP"></a> <a id="bk__h264__decode__ctlr_8h_1a70cfe4db1fa363353c9695cc88705fb3"></a> avdk\_err\_t bk\_h264\_decode\_flexa\_ctlr\_new([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") \*handle, [bk\_h264\_decode\_flexa\_config\_t](#_CPPv429bk_h264_decode_flexa_config_t "bk_h264_decode_flexa_config_t") \*config)
:   Create a Flexa-mode H.264 decoder controller.

    参数
    :   - **handle** – Output pointer that receives the decoder handle
        - **config** – Flexa decoder configuration

    返回
    :   AVDK error code

<a id="_CPPv429bk_h264_decode_frame_ctlr_newP28bk_h264_decode_ctlr_handle_tP29bk_h264_decode_frame_config_t"></a>

<a id="_CPPv329bk_h264_decode_frame_ctlr_newP28bk_h264_decode_ctlr_handle_tP29bk_h264_decode_frame_config_t"></a> <a id="_CPPv229bk_h264_decode_frame_ctlr_newP28bk_h264_decode_ctlr_handle_tP29bk_h264_decode_frame_config_t"></a> <a id="bk_h264_decode_frame_ctlr_new__bk_h264_decode_ctlr_handle_tP.bk_h264_decode_frame_config_tP"></a> <a id="bk__h264__decode__ctlr_8h_1ac3071ede2e68d8a4851dba4b5a39ea83"></a> avdk\_err\_t bk\_h264\_decode\_frame\_ctlr\_new([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") \*handle, [bk\_h264\_decode\_frame\_config\_t](#_CPPv429bk_h264_decode_frame_config_t "bk_h264_decode_frame_config_t") \*config)
:   Create a frame-mode H.264 decoder controller.

    参数
    :   - **handle** – Output pointer that receives the decoder handle
        - **config** – Frame decoder configuration

    返回
    :   AVDK error code

<a id="_CPPv438bk_h264_decode_frame_zerocopy_ctlr_newP28bk_h264_decode_ctlr_handle_tP38bk_h264_decode_frame_zerocopy_config_t"></a>

<a id="_CPPv338bk_h264_decode_frame_zerocopy_ctlr_newP28bk_h264_decode_ctlr_handle_tP38bk_h264_decode_frame_zerocopy_config_t"></a> <a id="_CPPv238bk_h264_decode_frame_zerocopy_ctlr_newP28bk_h264_decode_ctlr_handle_tP38bk_h264_decode_frame_zerocopy_config_t"></a> <a id="bk_h264_decode_frame_zerocopy_ctlr_new__bk_h264_decode_ctlr_handle_tP.bk_h264_decode_frame_zerocopy_config_tP"></a> <a id="bk__h264__decode__ctlr_8h_1a63d67b636d36510a231a186d251bd5e3"></a> avdk\_err\_t bk\_h264\_decode\_frame\_zerocopy\_ctlr\_new([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") \*handle, [bk\_h264\_decode\_frame\_zerocopy\_config\_t](#_CPPv438bk_h264_decode_frame_zerocopy_config_t "bk_h264_decode_frame_zerocopy_config_t") \*config)
:   Create a zero-copy / B-frame capable whole-frame H.264 decoder controller.

    Like bk\_h264\_decode\_frame\_ctlr\_new() it decodes one access unit per bk\_h264\_decode\_frame() call, but it owns an internal zero-copy frame pool: one physical buffer serves as decode target / DPB reference / display output, eliminating the reference-backup and output copies and enabling B-frame decoding with POC-based display reordering. The per-frame output buffer in [bk\_h264\_decode\_input\_t](#structbk__h264__decode__input__t) is ignored; decoded frames are pulled in display order via BK\_H264\_DECODE\_IOCTL\_DEQUEUE and returned via BK\_H264\_DECODE\_IOCTL\_RELEASE, with BK\_H264\_DECODE\_IOCTL\_FLUSH emitting trailing reordered pictures at EOS.

    参数
    :   - **handle** – Output pointer that receives the decoder handle
        - **config** – Zero-copy frame decoder configuration (disp\_depth applies here)

    返回
    :   AVDK error code

<a id="_CPPv419bk_h264_decode_init28bk_h264_decode_ctlr_handle_t"></a>

<a id="_CPPv319bk_h264_decode_init28bk_h264_decode_ctlr_handle_t"></a> <a id="_CPPv219bk_h264_decode_init28bk_h264_decode_ctlr_handle_t"></a> <a id="bk_h264_decode_init__bk_h264_decode_ctlr_handle_t"></a> <a id="bk__h264__decode__ctlr_8h_1a9e7e83de31bbc7f35e7d03efb8abf3aa"></a> avdk\_err\_t bk\_h264\_decode\_init([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Initialize the H.264 decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv421bk_h264_decode_deinit28bk_h264_decode_ctlr_handle_t"></a>

<a id="_CPPv321bk_h264_decode_deinit28bk_h264_decode_ctlr_handle_t"></a> <a id="_CPPv221bk_h264_decode_deinit28bk_h264_decode_ctlr_handle_t"></a> <a id="bk_h264_decode_deinit__bk_h264_decode_ctlr_handle_t"></a> <a id="bk__h264__decode__ctlr_8h_1a590a8757ac057ac48730e6fdaea8731a"></a> avdk\_err\_t bk\_h264\_decode\_deinit([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Deinitialize the H.264 decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv419bk_h264_decode_open28bk_h264_decode_ctlr_handle_t"></a>

<a id="_CPPv319bk_h264_decode_open28bk_h264_decode_ctlr_handle_t"></a> <a id="_CPPv219bk_h264_decode_open28bk_h264_decode_ctlr_handle_t"></a> <a id="bk_h264_decode_open__bk_h264_decode_ctlr_handle_t"></a> <a id="bk__h264__decode__ctlr_8h_1a374255e3205bed25cdd7282bcfc0dfae"></a> avdk\_err\_t bk\_h264\_decode\_open([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Open the H.264 decoder for decoding.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv420bk_h264_decode_close28bk_h264_decode_ctlr_handle_t"></a>

<a id="_CPPv320bk_h264_decode_close28bk_h264_decode_ctlr_handle_t"></a> <a id="_CPPv220bk_h264_decode_close28bk_h264_decode_ctlr_handle_t"></a> <a id="bk_h264_decode_close__bk_h264_decode_ctlr_handle_t"></a> <a id="bk__h264__decode__ctlr_8h_1a72b7eb82222400301d447018bb1ba13d"></a> avdk\_err\_t bk\_h264\_decode\_close([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Close the H.264 decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv420bk_h264_decode_frame28bk_h264_decode_ctlr_handle_tP22bk_h264_decode_input_t"></a>

<a id="_CPPv320bk_h264_decode_frame28bk_h264_decode_ctlr_handle_tP22bk_h264_decode_input_t"></a> <a id="_CPPv220bk_h264_decode_frame28bk_h264_decode_ctlr_handle_tP22bk_h264_decode_input_t"></a> <a id="bk_h264_decode_frame__bk_h264_decode_ctlr_handle_t.bk_h264_decode_input_tP"></a> <a id="bk__h264__decode__ctlr_8h_1a57e77a164bf41aaa14fc4c35302ade2a"></a> avdk\_err\_t bk\_h264\_decode\_frame([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle, [bk\_h264\_decode\_input\_t](#_CPPv422bk_h264_decode_input_t "bk_h264_decode_input_t") \*input)
:   Decode one H.264 access unit or frame.

    参数
    :   - **handle** – Decoder handle
        - **input** – Input bitstream and output buffer descriptors

    返回
    :   AVDK error code

<a id="_CPPv420bk_h264_decode_ioctl28bk_h264_decode_ctlr_handle_t26bk_h264_decode_ioctl_cmd_tPv"></a>

<a id="_CPPv320bk_h264_decode_ioctl28bk_h264_decode_ctlr_handle_t26bk_h264_decode_ioctl_cmd_tPv"></a> <a id="_CPPv220bk_h264_decode_ioctl28bk_h264_decode_ctlr_handle_t26bk_h264_decode_ioctl_cmd_tPv"></a> <a id="bk_h264_decode_ioctl__bk_h264_decode_ctlr_handle_t.bk_h264_decode_ioctl_cmd_t.voidP"></a> <a id="bk__h264__decode__ctlr_8h_1a189a7b01d2603c765094e4b6600009c5"></a> avdk\_err\_t bk\_h264\_decode\_ioctl([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle, [bk\_h264\_decode\_ioctl\_cmd\_t](#_CPPv426bk_h264_decode_ioctl_cmd_t "bk_h264_decode_ioctl_cmd_t") cmd, void \*arg)
:   Issue an IOCTL command on the H.264 decoder.

    参数
    :   - **handle** – Decoder handle
        - **cmd** – IOCTL command
        - **arg** – Command-specific argument

    返回
    :   AVDK error code

<a id="_CPPv421bk_h264_decode_delete28bk_h264_decode_ctlr_handle_t"></a>

<a id="_CPPv321bk_h264_decode_delete28bk_h264_decode_ctlr_handle_t"></a> <a id="_CPPv221bk_h264_decode_delete28bk_h264_decode_ctlr_handle_t"></a> <a id="bk_h264_decode_delete__bk_h264_decode_ctlr_handle_t"></a> <a id="bk__h264__decode__ctlr_8h_1a000531c1b8ffae3d7d439e54c2402012"></a> avdk\_err\_t bk\_h264\_decode\_delete([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle)
:   Delete the H.264 decoder controller.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv423bk_h264_decode_get_info28bk_h264_decode_ctlr_handle_tP21bk_h264_decode_info_t"></a>

<a id="_CPPv323bk_h264_decode_get_info28bk_h264_decode_ctlr_handle_tP21bk_h264_decode_info_t"></a> <a id="_CPPv223bk_h264_decode_get_info28bk_h264_decode_ctlr_handle_tP21bk_h264_decode_info_t"></a> <a id="bk_h264_decode_get_info__bk_h264_decode_ctlr_handle_t.bk_h264_decode_info_tP"></a> <a id="bk__h264__decode__ctlr_8h_1a2ea1bd7074197fc0745079486b31ad56"></a> avdk\_err\_t bk\_h264\_decode\_get\_info([bk\_h264\_decode\_ctlr\_handle\_t](#_CPPv428bk_h264_decode_ctlr_handle_t "bk_h264_decode_ctlr_handle_t") handle, [bk\_h264\_decode\_info\_t](#_CPPv421bk_h264_decode_info_t "bk_h264_decode_info_t") \*info)
:   Get decoded stream or frame metadata.

    参数
    :   - **handle** – Decoder handle
        - **info** – Output structure for stream/frame info

    返回
    :   AVDK error code

<a id="h-264-decode-types"></a>

### H.264 Decode Types

<a id="id5"></a>

#### Header File

- [bk\_h264\_decode\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_decode/bk_h264_decode_types.h)

<a id="structures"></a>

#### Structures

<a id="_CPPv424bk_h264_decode_port_rd_t"></a>

<a id="_CPPv324bk_h264_decode_port_rd_t"></a> <a id="_CPPv224bk_h264_decode_port_rd_t"></a> <a id="bk_h264_decode_port_rd_t"></a> <a id="structbk__h264__decode__port__rd__t"></a> struct bk\_h264\_decode\_port\_rd\_t

<a id="_CPPv427bk_h264_decode_osd_config_t"></a>

<a id="_CPPv327bk_h264_decode_osd_config_t"></a> <a id="_CPPv227bk_h264_decode_osd_config_t"></a> <a id="bk_h264_decode_osd_config_t"></a> <a id="structbk__h264__decode__osd__config__t"></a> struct bk\_h264\_decode\_osd\_config\_t

<a id="_CPPv420bk_h264_decode_osd_t"></a>

<a id="_CPPv320bk_h264_decode_osd_t"></a> <a id="_CPPv220bk_h264_decode_osd_t"></a> <a id="bk_h264_decode_osd_t"></a> <a id="structbk__h264__decode__osd__t"></a> struct bk\_h264\_decode\_osd\_t

<a id="_CPPv429bk_h264_decode_frame_config_t"></a>

<a id="_CPPv329bk_h264_decode_frame_config_t"></a> <a id="_CPPv229bk_h264_decode_frame_config_t"></a> <a id="bk_h264_decode_frame_config_t"></a> <a id="structbk__h264__decode__frame__config__t"></a> struct bk\_h264\_decode\_frame\_config\_t

<a id="_CPPv438bk_h264_decode_frame_zerocopy_config_t"></a>

<a id="_CPPv338bk_h264_decode_frame_zerocopy_config_t"></a> <a id="_CPPv238bk_h264_decode_frame_zerocopy_config_t"></a> <a id="bk_h264_decode_frame_zerocopy_config_t"></a> <a id="structbk__h264__decode__frame__zerocopy__config__t"></a> struct bk\_h264\_decode\_frame\_zerocopy\_config\_t

<a id="_CPPv429bk_h264_decode_flexa_config_t"></a>

<a id="_CPPv329bk_h264_decode_flexa_config_t"></a> <a id="_CPPv229bk_h264_decode_flexa_config_t"></a> <a id="bk_h264_decode_flexa_config_t"></a> <a id="structbk__h264__decode__flexa__config__t"></a> struct bk\_h264\_decode\_flexa\_config\_t

<a id="_CPPv422bk_h264_decode_input_t"></a>

<a id="_CPPv322bk_h264_decode_input_t"></a> <a id="_CPPv222bk_h264_decode_input_t"></a> <a id="bk_h264_decode_input_t"></a> <a id="structbk__h264__decode__input__t"></a> struct bk\_h264\_decode\_input\_t

<a id="_CPPv426bk_h264_decode_out_frame_t"></a>

<a id="_CPPv326bk_h264_decode_out_frame_t"></a> <a id="_CPPv226bk_h264_decode_out_frame_t"></a> <a id="bk_h264_decode_out_frame_t"></a> <a id="structbk__h264__decode__out__frame__t"></a> struct bk\_h264\_decode\_out\_frame\_t

<a id="_CPPv424bk_h264_decode_dequeue_t"></a>

<a id="_CPPv324bk_h264_decode_dequeue_t"></a> <a id="_CPPv224bk_h264_decode_dequeue_t"></a> <a id="bk_h264_decode_dequeue_t"></a> <a id="structbk__h264__decode__dequeue__t"></a> struct bk\_h264\_decode\_dequeue\_t

<a id="_CPPv421bk_h264_decode_ctlr_t"></a>

<a id="_CPPv321bk_h264_decode_ctlr_t"></a> <a id="_CPPv221bk_h264_decode_ctlr_t"></a> <a id="bk_h264_decode_ctlr_t"></a> <a id="structbk__h264__decode__ctlr__t"></a> struct bk\_h264\_decode\_ctlr\_t

<a id="macros"></a>

#### Macros

<a id="c.BK_H264_DECODE_RD_PORT_MAX"></a>

<a id="bk__h264__decode__types_8h_1a9e1e384e51f1b07ff365573de7a335f9"></a> BK\_H264\_DECODE\_RD\_PORT\_MAX

<a id="c.DEFAULT_H264_DECODE_FLEXA_CONFIG"></a>

<a id="bk__h264__decode__types_8h_1a64c87252fb1ca938042817e6060ae39b"></a> DEFAULT\_H264\_DECODE\_FLEXA\_CONFIG

<a id="c.DEFAULT_H264_DECODE_FRAME_CONFIG"></a>

<a id="bk__h264__decode__types_8h_1a70b387283fd50b68abe40c1098d34080"></a> DEFAULT\_H264\_DECODE\_FRAME\_CONFIG

<a id="c.DEFAULT_H264_DECODE_FRAME_ZEROCOPY_CONFIG"></a>

<a id="bk__h264__decode__types_8h_1afc39938a2259495deef3d54410c8ecc1"></a> DEFAULT\_H264\_DECODE\_FRAME\_ZEROCOPY\_CONFIG

<a id="type-definitions"></a>

#### Type Definitions

<a id="_CPPv428bk_h264_decode_frame_done_cb"></a>

<a id="_CPPv328bk_h264_decode_frame_done_cb"></a> <a id="_CPPv228bk_h264_decode_frame_done_cb"></a> <a id="bk_h264_decode_frame_done_cb"></a> <a id="bk__h264__decode__types_8h_1a926448b6ca1bd2b5c151ea26c71007a5"></a> typedef void (\*bk\_h264\_decode\_frame\_done\_cb)(int status, void \*args)

<a id="_CPPv428bk_h264_decode_flexa_done_cb"></a>

<a id="_CPPv328bk_h264_decode_flexa_done_cb"></a> <a id="_CPPv228bk_h264_decode_flexa_done_cb"></a> <a id="bk_h264_decode_flexa_done_cb"></a> <a id="bk__h264__decode__types_8h_1a6deb7414239b464aa43977f5fc7f8604"></a> typedef void (\*bk\_h264\_decode\_flexa\_done\_cb)(uint32\_t wr\_ptr, void \*args)

<a id="_CPPv428bk_h264_decode_osd_update_cb"></a>

<a id="_CPPv328bk_h264_decode_osd_update_cb"></a> <a id="_CPPv228bk_h264_decode_osd_update_cb"></a> <a id="bk_h264_decode_osd_update_cb"></a> <a id="bk__h264__decode__types_8h_1af28afc9b36e952002ea56051ed0ac098"></a> typedef void (\*bk\_h264\_decode\_osd\_update\_cb)([bk\_h264\_decode\_osd\_config\_t](#_CPPv427bk_h264_decode_osd_config_t "bk_h264_decode_osd_config_t") \*osd)

<a id="_CPPv427bk_h264_decode_frame_type_t"></a>

<a id="_CPPv327bk_h264_decode_frame_type_t"></a> <a id="_CPPv227bk_h264_decode_frame_type_t"></a> <a id="bk_h264_decode_frame_type_t"></a> <a id="bk__h264__decode__types_8h_1ae936422242af5dcf0b0f500f1ff63631"></a> typedef vcdec\_h264\_frame\_type\_t bk\_h264\_decode\_frame\_type\_t

<a id="_CPPv421bk_h264_decode_info_t"></a>

<a id="_CPPv321bk_h264_decode_info_t"></a> <a id="_CPPv221bk_h264_decode_info_t"></a> <a id="bk_h264_decode_info_t"></a> <a id="bk__h264__decode__types_8h_1a9351f3d252d7fd8618a507d6ec55b02b"></a> typedef vcdec\_h264\_info\_t bk\_h264\_decode\_info\_t

<a id="_CPPv428bk_h264_decode_ctlr_handle_t"></a>

<a id="_CPPv328bk_h264_decode_ctlr_handle_t"></a> <a id="_CPPv228bk_h264_decode_ctlr_handle_t"></a> <a id="bk_h264_decode_ctlr_handle_t"></a> <a id="bk__h264__decode__types_8h_1a27f6f0613a3084f999db526567fb47c5"></a> typedef struct [bk\_h264\_decode\_ctlr\_t](#_CPPv421bk_h264_decode_ctlr_t "bk_h264_decode_ctlr_t") \*bk\_h264\_decode\_ctlr\_handle\_t

<a id="bk__h264__decode__types_8h_1af6bedb37c2920ce156649daf6eebfc55"></a> typedef struct [bk\_h264\_decode\_ctlr\_t](#_CPPv421bk_h264_decode_ctlr_t "bk_h264_decode_ctlr_t") bk\_h264\_decode\_ctlr\_t

<a id="enumerations"></a>

#### Enumerations

<a id="_CPPv426bk_h264_decode_ioctl_cmd_t"></a>

<a id="_CPPv326bk_h264_decode_ioctl_cmd_t"></a> <a id="_CPPv226bk_h264_decode_ioctl_cmd_t"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcf"></a> enum bk\_h264\_decode\_ioctl\_cmd\_t
:   *Values:*

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t29BK_H264_DECODE_IOCTL_GET_INFOE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t29BK_H264_DECODE_IOCTL_GET_INFOE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t29BK_H264_DECODE_IOCTL_GET_INFOE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfadbe701557596cfdc5b3648bccd5c4c25"></a> enumerator BK\_H264\_DECODE\_IOCTL\_GET\_INFO

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t26BK_H264_DECODE_IOCTL_ABORTE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t26BK_H264_DECODE_IOCTL_ABORTE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t26BK_H264_DECODE_IOCTL_ABORTE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfa176c8083724b50fa3716789d9379072f"></a> enumerator BK\_H264\_DECODE\_IOCTL\_ABORT

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t36BK_H264_DECODE_IOCTL_PORT_SET_RD_PTRE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t36BK_H264_DECODE_IOCTL_PORT_SET_RD_PTRE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t36BK_H264_DECODE_IOCTL_PORT_SET_RD_PTRE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfa4293118d802f3d76b13d1f0008199c63"></a> enumerator BK\_H264\_DECODE\_IOCTL\_PORT\_SET\_RD\_PTR

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t34BK_H264_DECODE_IOCTL_REGISTER_BONDE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t34BK_H264_DECODE_IOCTL_REGISTER_BONDE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t34BK_H264_DECODE_IOCTL_REGISTER_BONDE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfaae0911393635206d1cbe245db72cc196"></a> enumerator BK\_H264\_DECODE\_IOCTL\_REGISTER\_BOND

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t36BK_H264_DECODE_IOCTL_UNREGISTER_BONDE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t36BK_H264_DECODE_IOCTL_UNREGISTER_BONDE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t36BK_H264_DECODE_IOCTL_UNREGISTER_BONDE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfa31b6b6dd0a377a1e51196f43816fe99b"></a> enumerator BK\_H264\_DECODE\_IOCTL\_UNREGISTER\_BOND

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t43BK_H264_DECODE_IOCTL_FLEXA_NOTIFY_PORT_DONEE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t43BK_H264_DECODE_IOCTL_FLEXA_NOTIFY_PORT_DONEE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t43BK_H264_DECODE_IOCTL_FLEXA_NOTIFY_PORT_DONEE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfa12e89f2bfa91f075ea0c600fe74e7334"></a> enumerator BK\_H264\_DECODE\_IOCTL\_FLEXA\_NOTIFY\_PORT\_DONE

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t26BK_H264_DECODE_IOCTL_RESETE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t26BK_H264_DECODE_IOCTL_RESETE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t26BK_H264_DECODE_IOCTL_RESETE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfaff5787b84ba35eab1e255cd0a272d75d"></a> enumerator BK\_H264\_DECODE\_IOCTL\_RESET

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t28BK_H264_DECODE_IOCTL_SET_OSDE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t28BK_H264_DECODE_IOCTL_SET_OSDE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t28BK_H264_DECODE_IOCTL_SET_OSDE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfaa5c85adeb25b6d9fbfc7d984620c2f95"></a> enumerator BK\_H264\_DECODE\_IOCTL\_SET\_OSD

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t36BK_H264_DECODE_IOCTL_SET_RECON_COVERE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t36BK_H264_DECODE_IOCTL_SET_RECON_COVERE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t36BK_H264_DECODE_IOCTL_SET_RECON_COVERE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfa14a4ba122b547876c6d6944f3cd1fb8e"></a> enumerator BK\_H264\_DECODE\_IOCTL\_SET\_RECON\_COVER

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t28BK_H264_DECODE_IOCTL_DEQUEUEE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t28BK_H264_DECODE_IOCTL_DEQUEUEE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t28BK_H264_DECODE_IOCTL_DEQUEUEE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfae9dc49ee266e0214ed00f98fb981de4a"></a> enumerator BK\_H264\_DECODE\_IOCTL\_DEQUEUE

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t28BK_H264_DECODE_IOCTL_RELEASEE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t28BK_H264_DECODE_IOCTL_RELEASEE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t28BK_H264_DECODE_IOCTL_RELEASEE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfa8c9517cc01d8759120f6452ba6083e2d"></a> enumerator BK\_H264\_DECODE\_IOCTL\_RELEASE

    <a id="_CPPv4N26bk_h264_decode_ioctl_cmd_t26BK_H264_DECODE_IOCTL_FLUSHE"></a>

    <a id="_CPPv3N26bk_h264_decode_ioctl_cmd_t26BK_H264_DECODE_IOCTL_FLUSHE"></a> <a id="_CPPv2N26bk_h264_decode_ioctl_cmd_t26BK_H264_DECODE_IOCTL_FLUSHE"></a> <a id="bk__h264__decode__types_8h_1a7dd55a2a1c7a692ac9bbd46679aa1bcfa33342d72dbd84e0b2cc57afefaecb7a7"></a> enumerator BK\_H264\_DECODE\_IOCTL\_FLUSH

<a id="_CPPv427bk_h264_decode_rd_port_id_t"></a>

<a id="_CPPv327bk_h264_decode_rd_port_id_t"></a> <a id="_CPPv227bk_h264_decode_rd_port_id_t"></a> <a id="bk__h264__decode__types_8h_1a7c1c4eefefacf8963df130684a0d9954"></a> enum bk\_h264\_decode\_rd\_port\_id\_t
:   *Values:*

    <a id="_CPPv4N27bk_h264_decode_rd_port_id_t26BK_H264_DECODE_RD_PORT_GPUE"></a>

    <a id="_CPPv3N27bk_h264_decode_rd_port_id_t26BK_H264_DECODE_RD_PORT_GPUE"></a> <a id="_CPPv2N27bk_h264_decode_rd_port_id_t26BK_H264_DECODE_RD_PORT_GPUE"></a> <a id="bk__h264__decode__types_8h_1a7c1c4eefefacf8963df130684a0d9954a58500f5739689429ff16f623960e25af"></a> enumerator BK\_H264\_DECODE\_RD\_PORT\_GPU

    <a id="_CPPv4N27bk_h264_decode_rd_port_id_t28BK_H264_DECODE_RD_PORT_H264EE"></a>

    <a id="_CPPv3N27bk_h264_decode_rd_port_id_t28BK_H264_DECODE_RD_PORT_H264EE"></a> <a id="_CPPv2N27bk_h264_decode_rd_port_id_t28BK_H264_DECODE_RD_PORT_H264EE"></a> <a id="bk__h264__decode__types_8h_1a7c1c4eefefacf8963df130684a0d9954a2435d5beedf578b9d1fe17c45400cb8f"></a> enumerator BK\_H264\_DECODE\_RD\_PORT\_H264E

<a id="h-264-encode"></a>

### H.264 Encode

<a id="id6"></a>

#### Header File

- [bk\_h264\_encode\_ctlr.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_encode/bk_h264_encode_ctlr.h)

<a id="id7"></a>

#### Functions

<a id="_CPPv427bk_h264_encode_hw_flexa_newP28bk_h264_encode_ctlr_handle_tP32bk_h264_encode_hw_flexa_config_t"></a>

<a id="_CPPv327bk_h264_encode_hw_flexa_newP28bk_h264_encode_ctlr_handle_tP32bk_h264_encode_hw_flexa_config_t"></a> <a id="_CPPv227bk_h264_encode_hw_flexa_newP28bk_h264_encode_ctlr_handle_tP32bk_h264_encode_hw_flexa_config_t"></a> <a id="bk_h264_encode_hw_flexa_new__bk_h264_encode_ctlr_handle_tP.bk_h264_encode_hw_flexa_config_tP"></a> <a id="bk__h264__encode__ctlr_8h_1ab16ca1e6ded94571da471d2ed7a1395a"></a> avdk\_err\_t bk\_h264\_encode\_hw\_flexa\_new([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") \*handle, [bk\_h264\_encode\_hw\_flexa\_config\_t](#_CPPv432bk_h264_encode_hw_flexa_config_t "bk_h264_encode_hw_flexa_config_t") \*config)
:   Create a new hardware flexa encoder.

    参数
    :   - **handle** – Encoder handle
        - **config** – Hardware flexa configuration

    返回
    :   AVSDK error code

<a id="_CPPv427bk_h264_encode_sw_flexa_newP28bk_h264_encode_ctlr_handle_tP32bk_h264_encode_sw_flexa_config_t"></a>

<a id="_CPPv327bk_h264_encode_sw_flexa_newP28bk_h264_encode_ctlr_handle_tP32bk_h264_encode_sw_flexa_config_t"></a> <a id="_CPPv227bk_h264_encode_sw_flexa_newP28bk_h264_encode_ctlr_handle_tP32bk_h264_encode_sw_flexa_config_t"></a> <a id="bk_h264_encode_sw_flexa_new__bk_h264_encode_ctlr_handle_tP.bk_h264_encode_sw_flexa_config_tP"></a> <a id="bk__h264__encode__ctlr_8h_1a10f1ead7038310bb78c674539d885372"></a> avdk\_err\_t bk\_h264\_encode\_sw\_flexa\_new([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") \*handle, [bk\_h264\_encode\_sw\_flexa\_config\_t](#_CPPv432bk_h264_encode_sw_flexa_config_t "bk_h264_encode_sw_flexa_config_t") \*config)
:   Create a new software flexa encoder.

    参数
    :   - **handle** – Encoder handle
        - **config** – Software flexa configuration

    返回
    :   AVSDK error code

<a id="_CPPv424bk_h264_encode_frame_newP28bk_h264_encode_ctlr_handle_tP29bk_h264_encode_frame_config_t"></a>

<a id="_CPPv324bk_h264_encode_frame_newP28bk_h264_encode_ctlr_handle_tP29bk_h264_encode_frame_config_t"></a> <a id="_CPPv224bk_h264_encode_frame_newP28bk_h264_encode_ctlr_handle_tP29bk_h264_encode_frame_config_t"></a> <a id="bk_h264_encode_frame_new__bk_h264_encode_ctlr_handle_tP.bk_h264_encode_frame_config_tP"></a> <a id="bk__h264__encode__ctlr_8h_1ab147113771592ad364891a602c68fc10"></a> avdk\_err\_t bk\_h264\_encode\_frame\_new([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") \*handle, [bk\_h264\_encode\_frame\_config\_t](#_CPPv429bk_h264_encode_frame_config_t "bk_h264_encode_frame_config_t") \*config)
:   Create a new frame encoder.

    参数
    :   - **handle** – Encoder handle
        - **config** – Frame configuration

    返回
    :   AVSDK error code

<a id="_CPPv419bk_h264_encode_init28bk_h264_encode_ctlr_handle_t"></a>

<a id="_CPPv319bk_h264_encode_init28bk_h264_encode_ctlr_handle_t"></a> <a id="_CPPv219bk_h264_encode_init28bk_h264_encode_ctlr_handle_t"></a> <a id="bk_h264_encode_init__bk_h264_encode_ctlr_handle_t"></a> <a id="bk__h264__encode__ctlr_8h_1a3e2c3185dbe2e55ac66079d3ac8061c6"></a> avdk\_err\_t bk\_h264\_encode\_init([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Initialize encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

<a id="_CPPv421bk_h264_encode_deinit28bk_h264_encode_ctlr_handle_t"></a>

<a id="_CPPv321bk_h264_encode_deinit28bk_h264_encode_ctlr_handle_t"></a> <a id="_CPPv221bk_h264_encode_deinit28bk_h264_encode_ctlr_handle_t"></a> <a id="bk_h264_encode_deinit__bk_h264_encode_ctlr_handle_t"></a> <a id="bk__h264__encode__ctlr_8h_1a0d1cc1ea4f21b03380c1c92e5add48d9"></a> avdk\_err\_t bk\_h264\_encode\_deinit([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Deinitialize encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

<a id="_CPPv419bk_h264_encode_open28bk_h264_encode_ctlr_handle_t"></a>

<a id="_CPPv319bk_h264_encode_open28bk_h264_encode_ctlr_handle_t"></a> <a id="_CPPv219bk_h264_encode_open28bk_h264_encode_ctlr_handle_t"></a> <a id="bk_h264_encode_open__bk_h264_encode_ctlr_handle_t"></a> <a id="bk__h264__encode__ctlr_8h_1a0635bb8a9da2ffbc0521303041dae242"></a> avdk\_err\_t bk\_h264\_encode\_open([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Open encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

<a id="_CPPv420bk_h264_encode_close28bk_h264_encode_ctlr_handle_t"></a>

<a id="_CPPv320bk_h264_encode_close28bk_h264_encode_ctlr_handle_t"></a> <a id="_CPPv220bk_h264_encode_close28bk_h264_encode_ctlr_handle_t"></a> <a id="bk_h264_encode_close__bk_h264_encode_ctlr_handle_t"></a> <a id="bk__h264__encode__ctlr_8h_1a2d53f7549e2e3fedb495a52c4025a859"></a> avdk\_err\_t bk\_h264\_encode\_close([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Close encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

<a id="_CPPv420bk_h264_encode_start28bk_h264_encode_ctlr_handle_t"></a>

<a id="_CPPv320bk_h264_encode_start28bk_h264_encode_ctlr_handle_t"></a> <a id="_CPPv220bk_h264_encode_start28bk_h264_encode_ctlr_handle_t"></a> <a id="bk_h264_encode_start__bk_h264_encode_ctlr_handle_t"></a> <a id="bk__h264__encode__ctlr_8h_1a9912a3e111f443821e88ed696921d87a"></a> avdk\_err\_t bk\_h264\_encode\_start([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Execute encoding.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

<a id="_CPPv420bk_h264_encode_ioctl28bk_h264_encode_ctlr_handle_t26bk_h264_encode_ioctl_cmd_tPv"></a>

<a id="_CPPv320bk_h264_encode_ioctl28bk_h264_encode_ctlr_handle_t26bk_h264_encode_ioctl_cmd_tPv"></a> <a id="_CPPv220bk_h264_encode_ioctl28bk_h264_encode_ctlr_handle_t26bk_h264_encode_ioctl_cmd_tPv"></a> <a id="bk_h264_encode_ioctl__bk_h264_encode_ctlr_handle_t.bk_h264_encode_ioctl_cmd_t.voidP"></a> <a id="bk__h264__encode__ctlr_8h_1aabf3ca3a686c34ae6b7f63650018de11"></a> avdk\_err\_t bk\_h264\_encode\_ioctl([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, [bk\_h264\_encode\_ioctl\_cmd\_t](#_CPPv426bk_h264_encode_ioctl_cmd_t "bk_h264_encode_ioctl_cmd_t") cmd, void \*arg)
:   Control interface.

    参数
    :   - **handle** – Encoder handle
        - **cmd** – Command
        - **arg** – Argument

    返回
    :   AVSDK error code

<a id="_CPPv424bk_h264_encode_force_idr28bk_h264_encode_ctlr_handle_t"></a>

<a id="_CPPv324bk_h264_encode_force_idr28bk_h264_encode_ctlr_handle_t"></a> <a id="_CPPv224bk_h264_encode_force_idr28bk_h264_encode_ctlr_handle_t"></a> <a id="bk_h264_encode_force_idr__bk_h264_encode_ctlr_handle_t"></a> <a id="bk__h264__encode__ctlr_8h_1a391a99a6ab87aa6c388fe442f1e92a43"></a> avdk\_err\_t bk\_h264\_encode\_force\_idr([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Force IDR frame generation.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

<a id="_CPPv434bk_h264_encode_set_gop_frame_count28bk_h264_encode_ctlr_handle_t8uint32_t"></a>

<a id="_CPPv334bk_h264_encode_set_gop_frame_count28bk_h264_encode_ctlr_handle_t8uint32_t"></a> <a id="_CPPv234bk_h264_encode_set_gop_frame_count28bk_h264_encode_ctlr_handle_t8uint32_t"></a> <a id="bk_h264_encode_set_gop_frame_count__bk_h264_encode_ctlr_handle_t.uint32_t"></a> <a id="bk__h264__encode__ctlr_8h_1ae2deb8a6f31e951248326952e5ca4eb3"></a> avdk\_err\_t bk\_h264\_encode\_set\_gop\_frame\_count([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, uint32\_t gop\_frame\_count)
:   Configure GOP frame count.

    参数
    :   - **handle** – Encoder handle
        - **gop\_frame\_count** – Number of frames in one GOP

    返回
    :   AVSDK error code

<a id="_CPPv434bk_h264_encode_get_gop_frame_count28bk_h264_encode_ctlr_handle_tP8uint32_t"></a>

<a id="_CPPv334bk_h264_encode_get_gop_frame_count28bk_h264_encode_ctlr_handle_tP8uint32_t"></a> <a id="_CPPv234bk_h264_encode_get_gop_frame_count28bk_h264_encode_ctlr_handle_tP8uint32_t"></a> <a id="bk_h264_encode_get_gop_frame_count__bk_h264_encode_ctlr_handle_t.uint32_tP"></a> <a id="bk__h264__encode__ctlr_8h_1a6c7e63cdff9704fc8d9f4299645a01f8"></a> avdk\_err\_t bk\_h264\_encode\_get\_gop\_frame\_count([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, uint32\_t \*gop\_frame\_count)
:   Get GOP frame count.

    参数
    :   - **handle** – Encoder handle
        - **gop\_frame\_count** – Output GOP frame count

    返回
    :   AVSDK error code

<a id="_CPPv428bk_h264_encode_set_rate_ctrl28bk_h264_encode_ctlr_handle_tP26bk_h264_encode_rate_ctrl_t"></a>

<a id="_CPPv328bk_h264_encode_set_rate_ctrl28bk_h264_encode_ctlr_handle_tP26bk_h264_encode_rate_ctrl_t"></a> <a id="_CPPv228bk_h264_encode_set_rate_ctrl28bk_h264_encode_ctlr_handle_tP26bk_h264_encode_rate_ctrl_t"></a> <a id="bk_h264_encode_set_rate_ctrl__bk_h264_encode_ctlr_handle_t.bk_h264_encode_rate_ctrl_tP"></a> <a id="bk__h264__encode__ctlr_8h_1ad39b0abf2c34ff78a3eb94e5e14dd90b"></a> avdk\_err\_t bk\_h264\_encode\_set\_rate\_ctrl([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, [bk\_h264\_encode\_rate\_ctrl\_t](#_CPPv426bk_h264_encode_rate_ctrl_t "bk_h264_encode_rate_ctrl_t") \*rate\_ctrl)
:   Configure rate control.

    参数
    :   - **handle** – Encoder handle
        - **rate\_ctrl** – Rate control config

    返回
    :   AVSDK error code

<a id="_CPPv428bk_h264_encode_get_rate_ctrl28bk_h264_encode_ctlr_handle_tP26bk_h264_encode_rate_ctrl_t"></a>

<a id="_CPPv328bk_h264_encode_get_rate_ctrl28bk_h264_encode_ctlr_handle_tP26bk_h264_encode_rate_ctrl_t"></a> <a id="_CPPv228bk_h264_encode_get_rate_ctrl28bk_h264_encode_ctlr_handle_tP26bk_h264_encode_rate_ctrl_t"></a> <a id="bk_h264_encode_get_rate_ctrl__bk_h264_encode_ctlr_handle_t.bk_h264_encode_rate_ctrl_tP"></a> <a id="bk__h264__encode__ctlr_8h_1ae7ac08777006c49fbde2b9110785bab9"></a> avdk\_err\_t bk\_h264\_encode\_get\_rate\_ctrl([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, [bk\_h264\_encode\_rate\_ctrl\_t](#_CPPv426bk_h264_encode_rate_ctrl_t "bk_h264_encode_rate_ctrl_t") \*rate\_ctrl)
:   Get rate control config.

    参数
    :   - **handle** – Encoder handle
        - **rate\_ctrl** – Output rate control config

    返回
    :   AVSDK error code

<a id="_CPPv422bk_h264_encode_set_osd28bk_h264_encode_ctlr_handle_tP20bk_h264_encode_osd_t"></a>

<a id="_CPPv322bk_h264_encode_set_osd28bk_h264_encode_ctlr_handle_tP20bk_h264_encode_osd_t"></a> <a id="_CPPv222bk_h264_encode_set_osd28bk_h264_encode_ctlr_handle_tP20bk_h264_encode_osd_t"></a> <a id="bk_h264_encode_set_osd__bk_h264_encode_ctlr_handle_t.bk_h264_encode_osd_tP"></a> <a id="bk__h264__encode__ctlr_8h_1ab2c8d90d086c0927d2ba49003dc4ea43"></a> avdk\_err\_t bk\_h264\_encode\_set\_osd([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, [bk\_h264\_encode\_osd\_t](#_CPPv420bk_h264_encode_osd_t "bk_h264_encode_osd_t") \*osd)
:   Configure hardware OSD overlay with externally owned buffer.

    The caller allocates and fills `osd->buffer`, then passes ownership to the encoder via `osd->buffer_free`. After a successful call the caller must not modify the buffer. When a slot receives a new buffer pointer, the previous buffer is released through its registered free callback. All active OSD buffers are released automatically when the encoder is closed.

    参数
    :   - **handle** – Encoder handle
        - **osd** – OSD overlay config (buffer\_free required when buffer !\= NULL)

    返回
    :   AVSDK error code

<a id="_CPPv435bk_h264_encode_set_osd_bitmap_boxes28bk_h264_encode_ctlr_handle_tP33bk_h264_encode_osd_bitmap_boxes_t"></a>

<a id="_CPPv335bk_h264_encode_set_osd_bitmap_boxes28bk_h264_encode_ctlr_handle_tP33bk_h264_encode_osd_bitmap_boxes_t"></a> <a id="_CPPv235bk_h264_encode_set_osd_bitmap_boxes28bk_h264_encode_ctlr_handle_tP33bk_h264_encode_osd_bitmap_boxes_t"></a> <a id="bk_h264_encode_set_osd_bitmap_boxes__bk_h264_encode_ctlr_handle_t.bk_h264_encode_osd_bitmap_boxes_tP"></a> <a id="bk__h264__encode__ctlr_8h_1a2d10b3562243076972a4a0e73041b88d"></a> avdk\_err\_t bk\_h264\_encode\_set\_osd\_bitmap\_boxes([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, [bk\_h264\_encode\_osd\_bitmap\_boxes\_t](#_CPPv433bk_h264_encode_osd_bitmap_boxes_t "bk_h264_encode_osd_bitmap_boxes_t") \*boxes)
:   Draw hollow rectangles as a mono-color BITMAP OSD overlay.

    Internally allocates one BITMAP (1bpp) covering the union of all boxes, rasterizes borders, and installs it on `boxes->index`. Subsequent encode frames overlay automatically.

    Color limitation: BITMAP OSD supports only one foreground color per call. The color is taken from boxes-\>boxes\[0\].color (RGB888 → YUV); additional per-box colors are ignored. Pass count\=\=0 / boxes\=\=NULL to clear the slot.

    Buffer size (PSRAM / UNCODED heap, owned by encoder until replaced/cleared): canvas \= axis-aligned union of all boxes, then x/y rounded down to 2 px, width/height rounded up to 8 px; size \= (canvas\_w / 8\) \* canvas\_h bytes (1 bit/pixel). Example: one 100x80 box → canvas 104x80 → 1040 bytes.

    Geometry tip (avoid encode mosaic): keep each box’s start (x,y), size (width,height), and border thickness as multiples of 16\. Otherwise, the encoder may introduce mosaic artifacts around the lines.

    参数
    :   - **handle** – Encoder handle
        - **boxes** – BITMAP rectangle batch descriptor

    返回
    :   AVSDK error code

<a id="_CPPv437bk_h264_encode_set_osd_argb8888_boxes28bk_h264_encode_ctlr_handle_tP35bk_h264_encode_osd_argb8888_boxes_t"></a>

<a id="_CPPv337bk_h264_encode_set_osd_argb8888_boxes28bk_h264_encode_ctlr_handle_tP35bk_h264_encode_osd_argb8888_boxes_t"></a> <a id="_CPPv237bk_h264_encode_set_osd_argb8888_boxes28bk_h264_encode_ctlr_handle_tP35bk_h264_encode_osd_argb8888_boxes_t"></a> <a id="bk_h264_encode_set_osd_argb8888_boxes__bk_h264_encode_ctlr_handle_t.bk_h264_encode_osd_argb8888_boxes_tP"></a> <a id="bk__h264__encode__ctlr_8h_1a8876c9b45c9a0d285e16335b4061c720"></a> avdk\_err\_t bk\_h264\_encode\_set\_osd\_argb8888\_boxes([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle, [bk\_h264\_encode\_osd\_argb8888\_boxes\_t](#_CPPv435bk_h264_encode_osd_argb8888_boxes_t "bk_h264_encode_osd_argb8888_boxes_t") \*boxes)
:   Draw hollow rectangles as a multi-color ARGB8888 OSD overlay.

    Internally allocates one ARGB8888 buffer covering the union of all boxes, rasterizes borders with per-box ARGB color (alpha blend enabled by HW), and installs it on `boxes->index`. Non-border pixels are transparent. Subsequent encode frames overlay automatically.

    Each box may use a different color. Color format is 0xAARRGGBB; if A\=\=0 the implementation forces opaque 0xFF. Pass count\=\=0 / boxes\=\=NULL to clear.

    Buffer size (PSRAM / UNCODED heap, owned by encoder until replaced/cleared): canvas \= axis-aligned union of all boxes, then x/y/width/height all rounded to 2 px; size \= canvas\_w \* canvas\_h \* 4 bytes (32 bit/pixel). Example: one 100x80 box → canvas 100x80 → 32000 bytes.

    Size note: ARGB8888 needs 32x the memory of BITMAP for the same canvas (32 bpp vs 1 bpp). Prefer bk\_h264\_encode\_set\_osd\_bitmap\_boxes() when a single color is enough.

    Geometry tip (avoid encode mosaic): keep each box’s start (x,y), size (width,height), and border thickness as multiples of 16\. Otherwise, the encoder may introduce mosaic artifacts around the lines.

    参数
    :   - **handle** – Encoder handle
        - **boxes** – ARGB8888 rectangle batch descriptor

    返回
    :   AVSDK error code

<a id="_CPPv421bk_h264_encode_delete28bk_h264_encode_ctlr_handle_t"></a>

<a id="_CPPv321bk_h264_encode_delete28bk_h264_encode_ctlr_handle_t"></a> <a id="_CPPv221bk_h264_encode_delete28bk_h264_encode_ctlr_handle_t"></a> <a id="bk_h264_encode_delete__bk_h264_encode_ctlr_handle_t"></a> <a id="bk__h264__encode__ctlr_8h_1a345abeb8ca352e519fe51f11878c729c"></a> avdk\_err\_t bk\_h264\_encode\_delete([bk\_h264\_encode\_ctlr\_handle\_t](#_CPPv428bk_h264_encode_ctlr_handle_t "bk_h264_encode_ctlr_handle_t") handle)
:   Delete encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVSDK error code

<a id="h-264-encode-types"></a>

### H.264 Encode Types

<a id="id8"></a>

#### Header File

- [bk\_h264\_encode\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_encode/bk_h264_encode_types.h)

<a id="id9"></a>

#### Structures

<a id="_CPPv422bk_h264_encode_input_t"></a>

<a id="_CPPv322bk_h264_encode_input_t"></a> <a id="_CPPv222bk_h264_encode_input_t"></a> <a id="bk_h264_encode_input_t"></a> <a id="structbk__h264__encode__input__t"></a> struct bk\_h264\_encode\_input\_t
:   Per-frame input descriptor for frame-mode zero-copy encoding.

    Used with BK\_H264\_ENCODE\_IOCTL\_SET\_INPUT\_BUF. The input must be contiguous NV12; the encoder derives the chroma-plane address from the luma address and configured frame dimensions.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_h264_encode_input_t9input_bufE"></a>

    <a id="_CPPv3N22bk_h264_encode_input_t9input_bufE"></a> <a id="_CPPv2N22bk_h264_encode_input_t9input_bufE"></a> <a id="bk_h264_encode_input_t::input_buf__uint32_t"></a> <a id="structbk__h264__encode__input__t_1a453addec6a49daf77310de19fea49141"></a> uint32\_t input\_buf
    :   Luma (Y) plane base address of the frame to encode.

    <a id="_CPPv4N22bk_h264_encode_input_t10input_sizeE"></a>

    <a id="_CPPv3N22bk_h264_encode_input_t10input_sizeE"></a> <a id="_CPPv2N22bk_h264_encode_input_t10input_sizeE"></a> <a id="bk_h264_encode_input_t::input_size__uint32_t"></a> <a id="structbk__h264__encode__input__t_1aa6bbd050b253f3acf734bfe9fdf51853"></a> uint32\_t input\_size
    :   Input frame size in bytes (or line count, per controller).

<a id="_CPPv428bk_h264_encode_stream_info_t"></a>

<a id="_CPPv328bk_h264_encode_stream_info_t"></a> <a id="_CPPv228bk_h264_encode_stream_info_t"></a> <a id="bk_h264_encode_stream_info_t"></a> <a id="structbk__h264__encode__stream__info__t"></a> struct bk\_h264\_encode\_stream\_info\_t
:   Per-frame encoder statistics used by adaptive pre-processing (e.g. NDR).

    Filled by BK\_H264\_ENCODE\_IOCTL\_GET\_STREAM\_INFO.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N28bk_h264_encode_stream_info_t13intra_cu8_numE"></a>

    <a id="_CPPv3N28bk_h264_encode_stream_info_t13intra_cu8_numE"></a> <a id="_CPPv2N28bk_h264_encode_stream_info_t13intra_cu8_numE"></a> <a id="bk_h264_encode_stream_info_t::intra_cu8_num__uint32_t"></a> <a id="structbk__h264__encode__stream__info__t_1a950e8f8e31dbd65157b31293c7cd163c"></a> uint32\_t intra\_cu8\_num
    :   Number of intra-coded 8x8 CUs in the last frame (motion proxy).

    <a id="_CPPv4N28bk_h264_encode_stream_info_t7rd_costE"></a>

    <a id="_CPPv3N28bk_h264_encode_stream_info_t7rd_costE"></a> <a id="_CPPv2N28bk_h264_encode_stream_info_t7rd_costE"></a> <a id="bk_h264_encode_stream_info_t::rd_cost__uint32_t"></a> <a id="structbk__h264__encode__stream__info__t_1abbf694a9f80bd0142529e11a00cf8e5b"></a> uint32\_t rd\_cost
    :   Aggregate rate-distortion cost of the last frame.

<a id="_CPPv420bk_h264_encode_osd_t"></a>

<a id="_CPPv320bk_h264_encode_osd_t"></a> <a id="_CPPv220bk_h264_encode_osd_t"></a> <a id="bk_h264_encode_osd_t"></a> <a id="structbk__h264__encode__osd__t"></a> struct bk\_h264\_encode\_osd\_t

<a id="_CPPv431bk_h264_encode_osd_bitmap_box_t"></a>

<a id="_CPPv331bk_h264_encode_osd_bitmap_box_t"></a> <a id="_CPPv231bk_h264_encode_osd_bitmap_box_t"></a> <a id="bk_h264_encode_osd_bitmap_box_t"></a> <a id="structbk__h264__encode__osd__bitmap__box__t"></a> struct bk\_h264\_encode\_osd\_bitmap\_box\_t
:   One hollow rectangle for mono-color BITMAP OSD overlay.

    Only one color is supported per call: `color` of boxes\[0\] is converted to BITMAP foreground YUV and applied to all boxes in the batch. Per-box colors after the first entry are ignored (a warning may be logged).

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N31bk_h264_encode_osd_bitmap_box_t1xE"></a>

    <a id="_CPPv3N31bk_h264_encode_osd_bitmap_box_t1xE"></a> <a id="_CPPv2N31bk_h264_encode_osd_bitmap_box_t1xE"></a> <a id="bk_h264_encode_osd_bitmap_box_t::x__uint32_t"></a> <a id="structbk__h264__encode__osd__bitmap__box__t_1a98a7a23298283c0cb5afd3085489a5b8"></a> uint32\_t x
    :   Top-left X in frame coordinates.

    <a id="_CPPv4N31bk_h264_encode_osd_bitmap_box_t1yE"></a>

    <a id="_CPPv3N31bk_h264_encode_osd_bitmap_box_t1yE"></a> <a id="_CPPv2N31bk_h264_encode_osd_bitmap_box_t1yE"></a> <a id="bk_h264_encode_osd_bitmap_box_t::y__uint32_t"></a> <a id="structbk__h264__encode__osd__bitmap__box__t_1a1f7fb73bafdee32f2bc627be70cade66"></a> uint32\_t y
    :   Top-left Y in frame coordinates.

    <a id="_CPPv4N31bk_h264_encode_osd_bitmap_box_t5widthE"></a>

    <a id="_CPPv3N31bk_h264_encode_osd_bitmap_box_t5widthE"></a> <a id="_CPPv2N31bk_h264_encode_osd_bitmap_box_t5widthE"></a> <a id="bk_h264_encode_osd_bitmap_box_t::width__uint32_t"></a> <a id="structbk__h264__encode__osd__bitmap__box__t_1a4edebcb8dd257903421dff276c9d9688"></a> uint32\_t width
    :   Box width in pixels.

    <a id="_CPPv4N31bk_h264_encode_osd_bitmap_box_t6heightE"></a>

    <a id="_CPPv3N31bk_h264_encode_osd_bitmap_box_t6heightE"></a> <a id="_CPPv2N31bk_h264_encode_osd_bitmap_box_t6heightE"></a> <a id="bk_h264_encode_osd_bitmap_box_t::height__uint32_t"></a> <a id="structbk__h264__encode__osd__bitmap__box__t_1aeefd210dc1ba762dfe3ff354d42a7a9a"></a> uint32\_t height
    :   Box height in pixels.

    <a id="_CPPv4N31bk_h264_encode_osd_bitmap_box_t9thicknessE"></a>

    <a id="_CPPv3N31bk_h264_encode_osd_bitmap_box_t9thicknessE"></a> <a id="_CPPv2N31bk_h264_encode_osd_bitmap_box_t9thicknessE"></a> <a id="bk_h264_encode_osd_bitmap_box_t::thickness__uint32_t"></a> <a id="structbk__h264__encode__osd__bitmap__box__t_1aaf372bb48c1ba3cc1a145f91559911c1"></a> uint32\_t thickness
    :   Border thickness in pixels (min 1).

    <a id="_CPPv4N31bk_h264_encode_osd_bitmap_box_t5colorE"></a>

    <a id="_CPPv3N31bk_h264_encode_osd_bitmap_box_t5colorE"></a> <a id="_CPPv2N31bk_h264_encode_osd_bitmap_box_t5colorE"></a> <a id="bk_h264_encode_osd_bitmap_box_t::color__uint32_t"></a> <a id="structbk__h264__encode__osd__bitmap__box__t_1a92777bc612e7695b3540556152980e1b"></a> uint32\_t color
    :   RGB888 0x00RRGGBB; only boxes\[0\].color is used.

<a id="_CPPv433bk_h264_encode_osd_bitmap_boxes_t"></a>

<a id="_CPPv333bk_h264_encode_osd_bitmap_boxes_t"></a> <a id="_CPPv233bk_h264_encode_osd_bitmap_boxes_t"></a> <a id="bk_h264_encode_osd_bitmap_boxes_t"></a> <a id="structbk__h264__encode__osd__bitmap__boxes__t"></a> struct bk\_h264\_encode\_osd\_bitmap\_boxes\_t
:   Batch hollow-rectangle request rendered as a mono-color BITMAP OSD.

    Encoder builds one BITMAP buffer covering the union of all boxes and installs it on `index`. Only one color is supported (from boxes\[0\].color). Pass `count` \=\= 0 or `boxes` \=\= NULL to clear the slot. On success the encoder owns the buffer; later encode frames overlay it automatically.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N33bk_h264_encode_osd_bitmap_boxes_t5indexE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_bitmap_boxes_t5indexE"></a> <a id="_CPPv2N33bk_h264_encode_osd_bitmap_boxes_t5indexE"></a> <a id="bk_h264_encode_osd_bitmap_boxes_t::index__uint32_t"></a> <a id="structbk__h264__encode__osd__bitmap__boxes__t_1af67df99b3410c08186bccbcdfeb49bca"></a> uint32\_t index
    :   Overlay slot index, 0..7.

    <a id="_CPPv4N33bk_h264_encode_osd_bitmap_boxes_t5alphaE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_bitmap_boxes_t5alphaE"></a> <a id="_CPPv2N33bk_h264_encode_osd_bitmap_boxes_t5alphaE"></a> <a id="bk_h264_encode_osd_bitmap_boxes_t::alpha__uint8_t"></a> <a id="structbk__h264__encode__osd__bitmap__boxes__t_1a517bbb64b1461d8d10c2c88eda3f7f9f"></a> uint8\_t alpha
    :   Global alpha; 0 means 255\.

    <a id="_CPPv4N33bk_h264_encode_osd_bitmap_boxes_t5countE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_bitmap_boxes_t5countE"></a> <a id="_CPPv2N33bk_h264_encode_osd_bitmap_boxes_t5countE"></a> <a id="bk_h264_encode_osd_bitmap_boxes_t::count__uint32_t"></a> <a id="structbk__h264__encode__osd__bitmap__boxes__t_1a3d3716c96e161ead5512d0b0d4fd7297"></a> uint32\_t count
    :   Number of boxes in `boxes`.

    <a id="_CPPv4N33bk_h264_encode_osd_bitmap_boxes_t5boxesE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_bitmap_boxes_t5boxesE"></a> <a id="_CPPv2N33bk_h264_encode_osd_bitmap_boxes_t5boxesE"></a> <a id="bk_h264_encode_osd_bitmap_boxes_t::boxes__bk_h264_encode_osd_bitmap_box_tCP"></a> <a id="structbk__h264__encode__osd__bitmap__boxes__t_1ac6a8f8951de7cda427a0f16c2c6e028c"></a> const [bk\_h264\_encode\_osd\_bitmap\_box\_t](#_CPPv431bk_h264_encode_osd_bitmap_box_t "bk_h264_encode_osd_bitmap_box_t") \*boxes
    :   Box array; NULL when clearing.

<a id="_CPPv433bk_h264_encode_osd_argb8888_box_t"></a>

<a id="_CPPv333bk_h264_encode_osd_argb8888_box_t"></a> <a id="_CPPv233bk_h264_encode_osd_argb8888_box_t"></a> <a id="bk_h264_encode_osd_argb8888_box_t"></a> <a id="structbk__h264__encode__osd__argb8888__box__t"></a> struct bk\_h264\_encode\_osd\_argb8888\_box\_t
:   One hollow rectangle for multi-color ARGB8888 OSD overlay.

    Each box keeps its own `color` (including per-pixel alpha). A\=\=0 is treated as fully opaque (0xFF) for convenience when callers pass RGB888-only values.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N33bk_h264_encode_osd_argb8888_box_t1xE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_argb8888_box_t1xE"></a> <a id="_CPPv2N33bk_h264_encode_osd_argb8888_box_t1xE"></a> <a id="bk_h264_encode_osd_argb8888_box_t::x__uint32_t"></a> <a id="structbk__h264__encode__osd__argb8888__box__t_1a6d560ba3ebe3311c96f7cc9964b5c966"></a> uint32\_t x
    :   Top-left X in frame coordinates.

    <a id="_CPPv4N33bk_h264_encode_osd_argb8888_box_t1yE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_argb8888_box_t1yE"></a> <a id="_CPPv2N33bk_h264_encode_osd_argb8888_box_t1yE"></a> <a id="bk_h264_encode_osd_argb8888_box_t::y__uint32_t"></a> <a id="structbk__h264__encode__osd__argb8888__box__t_1ac630c3a61c3c4aa7d0cf9c24248d85d7"></a> uint32\_t y
    :   Top-left Y in frame coordinates.

    <a id="_CPPv4N33bk_h264_encode_osd_argb8888_box_t5widthE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_argb8888_box_t5widthE"></a> <a id="_CPPv2N33bk_h264_encode_osd_argb8888_box_t5widthE"></a> <a id="bk_h264_encode_osd_argb8888_box_t::width__uint32_t"></a> <a id="structbk__h264__encode__osd__argb8888__box__t_1a4a1bc2dd8e4dcb5f07656a10f4a8bbdd"></a> uint32\_t width
    :   Box width in pixels.

    <a id="_CPPv4N33bk_h264_encode_osd_argb8888_box_t6heightE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_argb8888_box_t6heightE"></a> <a id="_CPPv2N33bk_h264_encode_osd_argb8888_box_t6heightE"></a> <a id="bk_h264_encode_osd_argb8888_box_t::height__uint32_t"></a> <a id="structbk__h264__encode__osd__argb8888__box__t_1a68eaaa3a5d95c26f20c59761f1e9bb3d"></a> uint32\_t height
    :   Box height in pixels.

    <a id="_CPPv4N33bk_h264_encode_osd_argb8888_box_t9thicknessE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_argb8888_box_t9thicknessE"></a> <a id="_CPPv2N33bk_h264_encode_osd_argb8888_box_t9thicknessE"></a> <a id="bk_h264_encode_osd_argb8888_box_t::thickness__uint32_t"></a> <a id="structbk__h264__encode__osd__argb8888__box__t_1a5ca6a8aaab0de9761b6190bb8c301f9a"></a> uint32\_t thickness
    :   Border thickness in pixels (min 1).

    <a id="_CPPv4N33bk_h264_encode_osd_argb8888_box_t5colorE"></a>

    <a id="_CPPv3N33bk_h264_encode_osd_argb8888_box_t5colorE"></a> <a id="_CPPv2N33bk_h264_encode_osd_argb8888_box_t5colorE"></a> <a id="bk_h264_encode_osd_argb8888_box_t::color__uint32_t"></a> <a id="structbk__h264__encode__osd__argb8888__box__t_1afa01bd26b3139c38f443b1276e6456a3"></a> uint32\_t color
    :   ARGB8888 0xAARRGGBB; A\=\=0 means opaque.

<a id="_CPPv435bk_h264_encode_osd_argb8888_boxes_t"></a>

<a id="_CPPv335bk_h264_encode_osd_argb8888_boxes_t"></a> <a id="_CPPv235bk_h264_encode_osd_argb8888_boxes_t"></a> <a id="bk_h264_encode_osd_argb8888_boxes_t"></a> <a id="structbk__h264__encode__osd__argb8888__boxes__t"></a> struct bk\_h264\_encode\_osd\_argb8888\_boxes\_t
:   Batch hollow-rectangle request rendered as an ARGB8888 OSD.

    Encoder builds one ARGB8888 buffer covering the union of all boxes. Non-border pixels stay transparent (A\=0). Each box may use a different color/alpha. Pass `count` \=\= 0 or `boxes` \=\= NULL to clear the slot.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N35bk_h264_encode_osd_argb8888_boxes_t5indexE"></a>

    <a id="_CPPv3N35bk_h264_encode_osd_argb8888_boxes_t5indexE"></a> <a id="_CPPv2N35bk_h264_encode_osd_argb8888_boxes_t5indexE"></a> <a id="bk_h264_encode_osd_argb8888_boxes_t::index__uint32_t"></a> <a id="structbk__h264__encode__osd__argb8888__boxes__t_1ac0d23e92594def5c32c240801a4c59a4"></a> uint32\_t index
    :   Overlay slot index, 0..7.

    <a id="_CPPv4N35bk_h264_encode_osd_argb8888_boxes_t5countE"></a>

    <a id="_CPPv3N35bk_h264_encode_osd_argb8888_boxes_t5countE"></a> <a id="_CPPv2N35bk_h264_encode_osd_argb8888_boxes_t5countE"></a> <a id="bk_h264_encode_osd_argb8888_boxes_t::count__uint32_t"></a> <a id="structbk__h264__encode__osd__argb8888__boxes__t_1a0af30f1d9146cb0db700aa16f4e63af8"></a> uint32\_t count
    :   Number of boxes in `boxes`.

    <a id="_CPPv4N35bk_h264_encode_osd_argb8888_boxes_t5boxesE"></a>

    <a id="_CPPv3N35bk_h264_encode_osd_argb8888_boxes_t5boxesE"></a> <a id="_CPPv2N35bk_h264_encode_osd_argb8888_boxes_t5boxesE"></a> <a id="bk_h264_encode_osd_argb8888_boxes_t::boxes__bk_h264_encode_osd_argb8888_box_tCP"></a> <a id="structbk__h264__encode__osd__argb8888__boxes__t_1a1e1894d0623399c270a782d162b566af"></a> const [bk\_h264\_encode\_osd\_argb8888\_box\_t](#_CPPv433bk_h264_encode_osd_argb8888_box_t "bk_h264_encode_osd_argb8888_box_t") \*boxes
    :   Box array; NULL when clearing.

<a id="_CPPv426bk_h264_encode_rate_ctrl_t"></a>

<a id="_CPPv326bk_h264_encode_rate_ctrl_t"></a> <a id="_CPPv226bk_h264_encode_rate_ctrl_t"></a> <a id="bk_h264_encode_rate_ctrl_t"></a> <a id="structbk__h264__encode__rate__ctrl__t"></a> struct bk\_h264\_encode\_rate\_ctrl\_t

<a id="_CPPv428bk_h264_encode_outbuf_info_t"></a>

<a id="_CPPv328bk_h264_encode_outbuf_info_t"></a> <a id="_CPPv228bk_h264_encode_outbuf_info_t"></a> <a id="bk_h264_encode_outbuf_info_t"></a> <a id="structbk__h264__encode__outbuf__info__t"></a> struct bk\_h264\_encode\_outbuf\_info\_t

<a id="_CPPv429bk_h264_encode_frame_config_t"></a>

<a id="_CPPv329bk_h264_encode_frame_config_t"></a> <a id="_CPPv229bk_h264_encode_frame_config_t"></a> <a id="bk_h264_encode_frame_config_t"></a> <a id="structbk__h264__encode__frame__config__t"></a> struct bk\_h264\_encode\_frame\_config\_t

<a id="_CPPv432bk_h264_encode_hw_flexa_config_t"></a>

<a id="_CPPv332bk_h264_encode_hw_flexa_config_t"></a> <a id="_CPPv232bk_h264_encode_hw_flexa_config_t"></a> <a id="bk_h264_encode_hw_flexa_config_t"></a> <a id="structbk__h264__encode__hw__flexa__config__t"></a> struct bk\_h264\_encode\_hw\_flexa\_config\_t

<a id="_CPPv432bk_h264_encode_sw_flexa_config_t"></a>

<a id="_CPPv332bk_h264_encode_sw_flexa_config_t"></a> <a id="_CPPv232bk_h264_encode_sw_flexa_config_t"></a> <a id="bk_h264_encode_sw_flexa_config_t"></a> <a id="structbk__h264__encode__sw__flexa__config__t"></a> struct bk\_h264\_encode\_sw\_flexa\_config\_t

<a id="_CPPv421bk_h264_encode_ctlr_t"></a>

<a id="_CPPv321bk_h264_encode_ctlr_t"></a> <a id="_CPPv221bk_h264_encode_ctlr_t"></a> <a id="bk_h264_encode_ctlr_t"></a> <a id="structbk__h264__encode__ctlr__t"></a> struct bk\_h264\_encode\_ctlr\_t

<a id="id10"></a>

#### Type Definitions

<a id="_CPPv435bk_h264_encode_osd_buffer_free_cb_t"></a>

<a id="_CPPv335bk_h264_encode_osd_buffer_free_cb_t"></a> <a id="_CPPv235bk_h264_encode_osd_buffer_free_cb_t"></a> <a id="bk_h264_encode_osd_buffer_free_cb_t"></a> <a id="bk__h264__encode__types_8h_1a1fb4cbe90031902031f002729774eaee"></a> typedef void (\*bk\_h264\_encode\_osd\_buffer\_free\_cb\_t)(void \*buffer, void \*free\_arg)

<a id="_CPPv428bk_h264_encode_ctlr_handle_t"></a>

<a id="_CPPv328bk_h264_encode_ctlr_handle_t"></a> <a id="_CPPv228bk_h264_encode_ctlr_handle_t"></a> <a id="bk_h264_encode_ctlr_handle_t"></a> <a id="bk__h264__encode__types_8h_1aebf17d52c51c0e386e2889845aa2749c"></a> typedef struct [bk\_h264\_encode\_ctlr\_t](#_CPPv421bk_h264_encode_ctlr_t "bk_h264_encode_ctlr_t") \*bk\_h264\_encode\_ctlr\_handle\_t

<a id="bk__h264__encode__types_8h_1af72938e81bb4ecbc6aa8bdfdc4888af1"></a> typedef struct [bk\_h264\_encode\_ctlr\_t](#_CPPv421bk_h264_encode_ctlr_t "bk_h264_encode_ctlr_t") bk\_h264\_encode\_ctlr\_t

<a id="id11"></a>

#### Enumerations

<a id="_CPPv417flexa_stream_id_t"></a>

<a id="_CPPv317flexa_stream_id_t"></a> <a id="_CPPv217flexa_stream_id_t"></a> <a id="bk__h264__encode__types_8h_1a4fd4fef95b6bb4c35678ab964082bb48"></a> enum flexa\_stream\_id\_t
:   *Values:*

    <a id="_CPPv4N17flexa_stream_id_t17FLEXA_STREAM_ID_YE"></a>

    <a id="_CPPv3N17flexa_stream_id_t17FLEXA_STREAM_ID_YE"></a> <a id="_CPPv2N17flexa_stream_id_t17FLEXA_STREAM_ID_YE"></a> <a id="bk__h264__encode__types_8h_1a4fd4fef95b6bb4c35678ab964082bb48a78d3929c2acc0c062653acc8cdd3e973"></a> enumerator FLEXA\_STREAM\_ID\_Y

    <a id="_CPPv4N17flexa_stream_id_t18FLEXA_STREAM_ID_CBE"></a>

    <a id="_CPPv3N17flexa_stream_id_t18FLEXA_STREAM_ID_CBE"></a> <a id="_CPPv2N17flexa_stream_id_t18FLEXA_STREAM_ID_CBE"></a> <a id="bk__h264__encode__types_8h_1a4fd4fef95b6bb4c35678ab964082bb48acb4758b19d7d61e687aebd4a4c3575fc"></a> enumerator FLEXA\_STREAM\_ID\_CB

    <a id="_CPPv4N17flexa_stream_id_t18FLEXA_STREAM_ID_CRE"></a>

    <a id="_CPPv3N17flexa_stream_id_t18FLEXA_STREAM_ID_CRE"></a> <a id="_CPPv2N17flexa_stream_id_t18FLEXA_STREAM_ID_CRE"></a> <a id="bk__h264__encode__types_8h_1a4fd4fef95b6bb4c35678ab964082bb48a50c4709efd99d6256c7ff5d1c73b1567"></a> enumerator FLEXA\_STREAM\_ID\_CR

<a id="_CPPv426bk_h264_encode_ioctl_cmd_t"></a>

<a id="_CPPv326bk_h264_encode_ioctl_cmd_t"></a> <a id="_CPPv226bk_h264_encode_ioctl_cmd_t"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3f"></a> enum bk\_h264\_encode\_ioctl\_cmd\_t
:   *Values:*

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t32BK_H264_ENCODE_IOCTL_DEBUG_STARTE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t32BK_H264_ENCODE_IOCTL_DEBUG_STARTE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t32BK_H264_ENCODE_IOCTL_DEBUG_STARTE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3faadc43a2bacd6004f18bc30df5b6de678"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_DEBUG\_START

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t31BK_H264_ENCODE_IOCTL_DEBUG_STOPE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t31BK_H264_ENCODE_IOCTL_DEBUG_STOPE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t31BK_H264_ENCODE_IOCTL_DEBUG_STOPE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa8e74468156253993dd48b1b19fc4c40b"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_DEBUG\_STOP

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t40BK_H264_ENCODE_IOCTL_SET_GOP_FRAME_COUNTE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t40BK_H264_ENCODE_IOCTL_SET_GOP_FRAME_COUNTE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t40BK_H264_ENCODE_IOCTL_SET_GOP_FRAME_COUNTE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa9c904483e4c044c20358dcdbc494633d"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_GOP\_FRAME\_COUNT

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t40BK_H264_ENCODE_IOCTL_GET_GOP_FRAME_COUNTE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t40BK_H264_ENCODE_IOCTL_GET_GOP_FRAME_COUNTE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t40BK_H264_ENCODE_IOCTL_GET_GOP_FRAME_COUNTE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa8a9a4998b7d8e78a0f96a0776aa617f2"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_GET\_GOP\_FRAME\_COUNT

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t42BK_H264_ENCODE_IOCTL_SET_FLEXA_LINES_READYE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t42BK_H264_ENCODE_IOCTL_SET_FLEXA_LINES_READYE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t42BK_H264_ENCODE_IOCTL_SET_FLEXA_LINES_READYE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa9c99e56c0a677489cd1e04f085df9b66"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_FLEXA\_LINES\_READY

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t36BK_H264_ENCODE_IOCTL_SET_FRAME_READYE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t36BK_H264_ENCODE_IOCTL_SET_FRAME_READYE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t36BK_H264_ENCODE_IOCTL_SET_FRAME_READYE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa533a78025efd5793196d0646a401a8d9"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_FRAME\_READY

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_REGISTER_BONDE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_REGISTER_BONDE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_REGISTER_BONDE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa05254e1edcbfeea1f0f60b518803df03"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_REGISTER\_BOND

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t36BK_H264_ENCODE_IOCTL_UNREGISTER_BONDE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t36BK_H264_ENCODE_IOCTL_UNREGISTER_BONDE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t36BK_H264_ENCODE_IOCTL_UNREGISTER_BONDE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa1cee9b8a978a1f3b046481762eea4ab7"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_UNREGISTER\_BOND

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t32BK_H264_ENCODE_IOCTL_STOP_ENCODEE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t32BK_H264_ENCODE_IOCTL_STOP_ENCODEE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t32BK_H264_ENCODE_IOCTL_STOP_ENCODEE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa5b1b43566dd92f443f2fc8ca03cba9cb"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_STOP\_ENCODE

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_SET_RATE_CTRLE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_SET_RATE_CTRLE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_SET_RATE_CTRLE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3faa25ffc4f37625b9ba03d99945d74171e"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_RATE\_CTRL

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_GET_RATE_CTRLE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_GET_RATE_CTRLE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_GET_RATE_CTRLE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa1294994a1a01c57d84d6214be41c60d1"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_GET\_RATE\_CTRL

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t28BK_H264_ENCODE_IOCTL_SET_OSDE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t28BK_H264_ENCODE_IOCTL_SET_OSDE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t28BK_H264_ENCODE_IOCTL_SET_OSDE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3faf149c0925aa26649e2e45e88e9dae187"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_OSD

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t41BK_H264_ENCODE_IOCTL_SET_OSD_BITMAP_BOXESE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t41BK_H264_ENCODE_IOCTL_SET_OSD_BITMAP_BOXESE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t41BK_H264_ENCODE_IOCTL_SET_OSD_BITMAP_BOXESE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa7e8b00a24e07fbd39ae91f506f575dd0"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_OSD\_BITMAP\_BOXES

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t43BK_H264_ENCODE_IOCTL_SET_OSD_ARGB8888_BOXESE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t43BK_H264_ENCODE_IOCTL_SET_OSD_ARGB8888_BOXESE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t43BK_H264_ENCODE_IOCTL_SET_OSD_ARGB8888_BOXESE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3faab16f9c3cce2695285ed4e21259b7f9b"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_OSD\_ARGB8888\_BOXES

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_SET_INPUT_BUFE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_SET_INPUT_BUFE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t34BK_H264_ENCODE_IOCTL_SET_INPUT_BUFE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa9ca3632db2565758fbd618477a6f6c38"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_INPUT\_BUF

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t36BK_H264_ENCODE_IOCTL_GET_STREAM_INFOE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t36BK_H264_ENCODE_IOCTL_GET_STREAM_INFOE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t36BK_H264_ENCODE_IOCTL_GET_STREAM_INFOE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa2909d83f08d7ae9d2c4dd5d17381987d"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_GET\_STREAM\_INFO

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t35BK_H264_ENCODE_IOCTL_SET_FRAME_RATEE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t35BK_H264_ENCODE_IOCTL_SET_FRAME_RATEE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t35BK_H264_ENCODE_IOCTL_SET_FRAME_RATEE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fae930f613155571e20fca26219a750b02"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_FRAME\_RATE

    <a id="_CPPv4N26bk_h264_encode_ioctl_cmd_t42BK_H264_ENCODE_IOCTL_SET_RC_QP_DELTA_RANGEE"></a>

    <a id="_CPPv3N26bk_h264_encode_ioctl_cmd_t42BK_H264_ENCODE_IOCTL_SET_RC_QP_DELTA_RANGEE"></a> <a id="_CPPv2N26bk_h264_encode_ioctl_cmd_t42BK_H264_ENCODE_IOCTL_SET_RC_QP_DELTA_RANGEE"></a> <a id="bk__h264__encode__types_8h_1a6b0350c6a587dcb94c4d24c2fcd51d3fa62dd851792d71b022554cd6d3e7a8961"></a> enumerator BK\_H264\_ENCODE\_IOCTL\_SET\_RC\_QP\_DELTA\_RANGE

<a id="_CPPv431bk_h264_encode_overlay_format_t"></a>

<a id="_CPPv331bk_h264_encode_overlay_format_t"></a> <a id="_CPPv231bk_h264_encode_overlay_format_t"></a> <a id="bk__h264__encode__types_8h_1a0938018efc2fffa8e31023251a36163f"></a> enum bk\_h264\_encode\_overlay\_format\_t
:   *Values:*

    <a id="_CPPv4N31bk_h264_encode_overlay_format_t38BK_H264_ENCODE_OVERLAY_FORMAT_ARGB8888E"></a>

    <a id="_CPPv3N31bk_h264_encode_overlay_format_t38BK_H264_ENCODE_OVERLAY_FORMAT_ARGB8888E"></a> <a id="_CPPv2N31bk_h264_encode_overlay_format_t38BK_H264_ENCODE_OVERLAY_FORMAT_ARGB8888E"></a> <a id="bk__h264__encode__types_8h_1a0938018efc2fffa8e31023251a36163fa5d6d0ff5afa6375e61ced0bfd6f0cc3a"></a> enumerator BK\_H264\_ENCODE\_OVERLAY\_FORMAT\_ARGB8888

    <a id="_CPPv4N31bk_h264_encode_overlay_format_t34BK_H264_ENCODE_OVERLAY_FORMAT_NV12E"></a>

    <a id="_CPPv3N31bk_h264_encode_overlay_format_t34BK_H264_ENCODE_OVERLAY_FORMAT_NV12E"></a> <a id="_CPPv2N31bk_h264_encode_overlay_format_t34BK_H264_ENCODE_OVERLAY_FORMAT_NV12E"></a> <a id="bk__h264__encode__types_8h_1a0938018efc2fffa8e31023251a36163fa5032da78f9f51f133c5a507a6b60812c"></a> enumerator BK\_H264\_ENCODE\_OVERLAY\_FORMAT\_NV12

    <a id="_CPPv4N31bk_h264_encode_overlay_format_t36BK_H264_ENCODE_OVERLAY_FORMAT_BITMAPE"></a>

    <a id="_CPPv3N31bk_h264_encode_overlay_format_t36BK_H264_ENCODE_OVERLAY_FORMAT_BITMAPE"></a> <a id="_CPPv2N31bk_h264_encode_overlay_format_t36BK_H264_ENCODE_OVERLAY_FORMAT_BITMAPE"></a> <a id="bk__h264__encode__types_8h_1a0938018efc2fffa8e31023251a36163fa0c196c7dc81d65250e9345c9f88077f7"></a> enumerator BK\_H264\_ENCODE\_OVERLAY\_FORMAT\_BITMAP

<a id="_CPPv427bk_h264_encode_flexa_mode_t"></a>

<a id="_CPPv327bk_h264_encode_flexa_mode_t"></a> <a id="_CPPv227bk_h264_encode_flexa_mode_t"></a> <a id="bk__h264__encode__types_8h_1a807ede8960d48a477852bf2893676e8b"></a> enum bk\_h264\_encode\_flexa\_mode\_t
:   *Values:*

    <a id="_CPPv4N27bk_h264_encode_flexa_mode_t30BK_H264_ENCODE_FLEXA_MODE_NONEE"></a>

    <a id="_CPPv3N27bk_h264_encode_flexa_mode_t30BK_H264_ENCODE_FLEXA_MODE_NONEE"></a> <a id="_CPPv2N27bk_h264_encode_flexa_mode_t30BK_H264_ENCODE_FLEXA_MODE_NONEE"></a> <a id="bk__h264__encode__types_8h_1a807ede8960d48a477852bf2893676e8ba0bfd53b0095b112b3cdc86dc4ab3b592"></a> enumerator BK\_H264\_ENCODE\_FLEXA\_MODE\_NONE

    <a id="_CPPv4N27bk_h264_encode_flexa_mode_t34BK_H264_ENCODE_FLEXA_MODE_SOFTWAREE"></a>

    <a id="_CPPv3N27bk_h264_encode_flexa_mode_t34BK_H264_ENCODE_FLEXA_MODE_SOFTWAREE"></a> <a id="_CPPv2N27bk_h264_encode_flexa_mode_t34BK_H264_ENCODE_FLEXA_MODE_SOFTWAREE"></a> <a id="bk__h264__encode__types_8h_1a807ede8960d48a477852bf2893676e8ba945ac635b52734489026e50b5eb9a7ad"></a> enumerator BK\_H264\_ENCODE\_FLEXA\_MODE\_SOFTWARE

    <a id="_CPPv4N27bk_h264_encode_flexa_mode_t34BK_H264_ENCODE_FLEXA_MODE_HARDWAREE"></a>

    <a id="_CPPv3N27bk_h264_encode_flexa_mode_t34BK_H264_ENCODE_FLEXA_MODE_HARDWAREE"></a> <a id="_CPPv2N27bk_h264_encode_flexa_mode_t34BK_H264_ENCODE_FLEXA_MODE_HARDWAREE"></a> <a id="bk__h264__encode__types_8h_1a807ede8960d48a477852bf2893676e8ba09ebe89683f73aae5ec38ba307fd0031"></a> enumerator BK\_H264\_ENCODE\_FLEXA\_MODE\_HARDWARE

<a id="jpeg-decode"></a>

### JPEG Decode

<a id="id12"></a>

#### Header File

- [bk\_jpeg\_decode\_ctlr.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_decode/bk_jpeg_decode_ctlr.h)

<a id="id13"></a>

#### Functions

<a id="_CPPv429bk_jpeg_decode_flexa_ctlr_newP28bk_jpeg_decode_ctlr_handle_tP29bk_jpeg_decode_flexa_config_t"></a>

<a id="_CPPv329bk_jpeg_decode_flexa_ctlr_newP28bk_jpeg_decode_ctlr_handle_tP29bk_jpeg_decode_flexa_config_t"></a> <a id="_CPPv229bk_jpeg_decode_flexa_ctlr_newP28bk_jpeg_decode_ctlr_handle_tP29bk_jpeg_decode_flexa_config_t"></a> <a id="bk_jpeg_decode_flexa_ctlr_new__bk_jpeg_decode_ctlr_handle_tP.bk_jpeg_decode_flexa_config_tP"></a> <a id="bk__jpeg__decode__ctlr_8h_1a1cc5fe0ec0aa347ddb54bd3b3c6e8597"></a> avdk\_err\_t bk\_jpeg\_decode\_flexa\_ctlr\_new([bk\_jpeg\_decode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") \*handle, [bk\_jpeg\_decode\_flexa\_config\_t](#_CPPv429bk_jpeg_decode_flexa_config_t "bk_jpeg_decode_flexa_config_t") \*config)
:   Create a Flexa-mode JPEG decoder controller.

    参数
    :   - **handle** – Output pointer that receives the decoder handle
        - **config** – Flexa decoder configuration

    返回
    :   AVDK error code

<a id="_CPPv429bk_jpeg_decode_frame_ctlr_newP28bk_jpeg_decode_ctlr_handle_tP29bk_jpeg_decode_frame_config_t"></a>

<a id="_CPPv329bk_jpeg_decode_frame_ctlr_newP28bk_jpeg_decode_ctlr_handle_tP29bk_jpeg_decode_frame_config_t"></a> <a id="_CPPv229bk_jpeg_decode_frame_ctlr_newP28bk_jpeg_decode_ctlr_handle_tP29bk_jpeg_decode_frame_config_t"></a> <a id="bk_jpeg_decode_frame_ctlr_new__bk_jpeg_decode_ctlr_handle_tP.bk_jpeg_decode_frame_config_tP"></a> <a id="bk__jpeg__decode__ctlr_8h_1a5dd43ee7872bbd405b7cf07d477768eb"></a> avdk\_err\_t bk\_jpeg\_decode\_frame\_ctlr\_new([bk\_jpeg\_decode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") \*handle, [bk\_jpeg\_decode\_frame\_config\_t](#_CPPv429bk_jpeg_decode_frame_config_t "bk_jpeg_decode_frame_config_t") \*config)
:   Create a frame-mode JPEG decoder controller.

    参数
    :   - **handle** – Output pointer that receives the decoder handle
        - **config** – Frame decoder configuration

    返回
    :   AVDK error code

<a id="_CPPv419bk_jpeg_decode_init28bk_jpeg_decode_ctlr_handle_t"></a>

<a id="_CPPv319bk_jpeg_decode_init28bk_jpeg_decode_ctlr_handle_t"></a> <a id="_CPPv219bk_jpeg_decode_init28bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk_jpeg_decode_init__bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk__jpeg__decode__ctlr_8h_1ae0be893099df3a5750656804afbeb119"></a> avdk\_err\_t bk\_jpeg\_decode\_init([bk\_jpeg\_decode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Initialize the JPEG decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv421bk_jpeg_decode_deinit28bk_jpeg_decode_ctlr_handle_t"></a>

<a id="_CPPv321bk_jpeg_decode_deinit28bk_jpeg_decode_ctlr_handle_t"></a> <a id="_CPPv221bk_jpeg_decode_deinit28bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk_jpeg_decode_deinit__bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk__jpeg__decode__ctlr_8h_1af77d515f938c0ef9765cf7a487bd49fe"></a> avdk\_err\_t bk\_jpeg\_decode\_deinit([bk\_jpeg\_decode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Deinitialize the JPEG decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv419bk_jpeg_decode_open28bk_jpeg_decode_ctlr_handle_t"></a>

<a id="_CPPv319bk_jpeg_decode_open28bk_jpeg_decode_ctlr_handle_t"></a> <a id="_CPPv219bk_jpeg_decode_open28bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk_jpeg_decode_open__bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk__jpeg__decode__ctlr_8h_1aa74c2d5b212c6aab287828e1ee57d12a"></a> avdk\_err\_t bk\_jpeg\_decode\_open([bk\_jpeg\_decode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Open the JPEG decoder for decoding.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv420bk_jpeg_decode_close28bk_jpeg_decode_ctlr_handle_t"></a>

<a id="_CPPv320bk_jpeg_decode_close28bk_jpeg_decode_ctlr_handle_t"></a> <a id="_CPPv220bk_jpeg_decode_close28bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk_jpeg_decode_close__bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk__jpeg__decode__ctlr_8h_1a83fd85b8c15f9c7ddc53ad29c67ab858"></a> avdk\_err\_t bk\_jpeg\_decode\_close([bk\_jpeg\_decode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Close the JPEG decoder.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv420bk_jpeg_decode_frame28bk_jpeg_decode_ctlr_handle_tP22bk_jpeg_decode_input_t"></a>

<a id="_CPPv320bk_jpeg_decode_frame28bk_jpeg_decode_ctlr_handle_tP22bk_jpeg_decode_input_t"></a> <a id="_CPPv220bk_jpeg_decode_frame28bk_jpeg_decode_ctlr_handle_tP22bk_jpeg_decode_input_t"></a> <a id="bk_jpeg_decode_frame__bk_jpeg_decode_ctlr_handle_t.bk_jpeg_decode_input_tP"></a> <a id="bk__jpeg__decode__ctlr_8h_1a41a43dc4045aa3e98985fdd867612754"></a> avdk\_err\_t bk\_jpeg\_decode\_frame([bk\_jpeg\_decode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle, [bk\_jpeg\_decode\_input\_t](#_CPPv422bk_jpeg_decode_input_t "bk_jpeg_decode_input_t") \*input)
:   Decode one JPEG image.

    参数
    :   - **handle** – Decoder handle
        - **input** – Input bitstream and output buffer descriptors

    返回
    :   AVDK error code

<a id="_CPPv420bk_jpeg_decode_ioctl28bk_jpeg_decode_ctlr_handle_t26bk_jpeg_decode_ioctl_cmd_tPv"></a>

<a id="_CPPv320bk_jpeg_decode_ioctl28bk_jpeg_decode_ctlr_handle_t26bk_jpeg_decode_ioctl_cmd_tPv"></a> <a id="_CPPv220bk_jpeg_decode_ioctl28bk_jpeg_decode_ctlr_handle_t26bk_jpeg_decode_ioctl_cmd_tPv"></a> <a id="bk_jpeg_decode_ioctl__bk_jpeg_decode_ctlr_handle_t.bk_jpeg_decode_ioctl_cmd_t.voidP"></a> <a id="bk__jpeg__decode__ctlr_8h_1a728855de5e04160f4eaa9e050a593e13"></a> avdk\_err\_t bk\_jpeg\_decode\_ioctl([bk\_jpeg\_decode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle, [bk\_jpeg\_decode\_ioctl\_cmd\_t](#_CPPv426bk_jpeg_decode_ioctl_cmd_t "bk_jpeg_decode_ioctl_cmd_t") cmd, void \*arg)
:   Issue an IOCTL command on the JPEG decoder.

    参数
    :   - **handle** – Decoder handle
        - **cmd** – IOCTL command
        - **arg** – Command-specific argument

    返回
    :   AVDK error code

<a id="_CPPv421bk_jpeg_decode_delete28bk_jpeg_decode_ctlr_handle_t"></a>

<a id="_CPPv321bk_jpeg_decode_delete28bk_jpeg_decode_ctlr_handle_t"></a> <a id="_CPPv221bk_jpeg_decode_delete28bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk_jpeg_decode_delete__bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk__jpeg__decode__ctlr_8h_1acef5aa8148d05051498cd8c16733c4ae"></a> avdk\_err\_t bk\_jpeg\_decode\_delete([bk\_jpeg\_decode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_decode_ctlr_handle_t "bk_jpeg_decode_ctlr_handle_t") handle)
:   Delete the JPEG decoder controller.

    参数
    :   **handle** – Decoder handle

    返回
    :   AVDK error code

<a id="_CPPv427bk_jpeg_decode_get_img_infoP25bk_jpeg_decode_img_info_t"></a>

<a id="_CPPv327bk_jpeg_decode_get_img_infoP25bk_jpeg_decode_img_info_t"></a> <a id="_CPPv227bk_jpeg_decode_get_img_infoP25bk_jpeg_decode_img_info_t"></a> <a id="bk_jpeg_decode_get_img_info__bk_jpeg_decode_img_info_tP"></a> <a id="bk__jpeg__decode__ctlr_8h_1aa38665fb2674791a26713f9d940f0896"></a> avdk\_err\_t bk\_jpeg\_decode\_get\_img\_info([bk\_jpeg\_decode\_img\_info\_t](#_CPPv425bk_jpeg_decode_img_info_t "bk_jpeg_decode_img_info_t") \*img\_info)
:   Parse JPEG header and get image information without full decode.

    参数
    :   **img\_info** – Input/output image info structure (contains JPEG bitstream pointer)

    返回
    :   AVDK error code

<a id="jpeg-decode-types"></a>

### JPEG Decode Types

<a id="id14"></a>

#### Header File

- [bk\_jpeg\_decode\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_decode/bk_jpeg_decode_types.h)

<a id="id15"></a>

#### Structures

<a id="_CPPv424bk_jpeg_decode_port_rd_t"></a>

<a id="_CPPv324bk_jpeg_decode_port_rd_t"></a> <a id="_CPPv224bk_jpeg_decode_port_rd_t"></a> <a id="bk_jpeg_decode_port_rd_t"></a> <a id="structbk__jpeg__decode__port__rd__t"></a> struct bk\_jpeg\_decode\_port\_rd\_t
:   this is for bond

<a id="_CPPv429bk_jpeg_decode_frame_config_t"></a>

<a id="_CPPv329bk_jpeg_decode_frame_config_t"></a> <a id="_CPPv229bk_jpeg_decode_frame_config_t"></a> <a id="bk_jpeg_decode_frame_config_t"></a> <a id="structbk__jpeg__decode__frame__config__t"></a> struct bk\_jpeg\_decode\_frame\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N29bk_jpeg_decode_frame_config_t10timeout_msE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_frame_config_t10timeout_msE"></a> <a id="_CPPv2N29bk_jpeg_decode_frame_config_t10timeout_msE"></a> <a id="bk_jpeg_decode_frame_config_t::timeout_ms__uint32_t"></a> <a id="structbk__jpeg__decode__frame__config__t_1abda0ebc987003b894880f370e4bcdd83"></a> uint32\_t timeout\_ms
    :   timeout in milliseconds

    <a id="_CPPv4N29bk_jpeg_decode_frame_config_t9out_widthE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_frame_config_t9out_widthE"></a> <a id="_CPPv2N29bk_jpeg_decode_frame_config_t9out_widthE"></a> <a id="bk_jpeg_decode_frame_config_t::out_width__uint16_t"></a> <a id="structbk__jpeg__decode__frame__config__t_1a0a0059cd10d7e013cc0f329b270c5bed"></a> uint16\_t out\_width
    :   output width

    <a id="_CPPv4N29bk_jpeg_decode_frame_config_t10out_heightE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_frame_config_t10out_heightE"></a> <a id="_CPPv2N29bk_jpeg_decode_frame_config_t10out_heightE"></a> <a id="bk_jpeg_decode_frame_config_t::out_height__uint16_t"></a> <a id="structbk__jpeg__decode__frame__config__t_1aa779f9f0a831a5e0da0ba7911c237fb5"></a> uint16\_t out\_height
    :   output height

    <a id="_CPPv4N29bk_jpeg_decode_frame_config_t10out_formatE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_frame_config_t10out_formatE"></a> <a id="_CPPv2N29bk_jpeg_decode_frame_config_t10out_formatE"></a> <a id="bk_jpeg_decode_frame_config_t::out_format__uint32_t"></a> <a id="structbk__jpeg__decode__frame__config__t_1a50798e18221debbbf243c8ed1ca148f8"></a> uint32\_t out\_format
    :   output format

    <a id="_CPPv4N29bk_jpeg_decode_frame_config_t13frame_done_cbE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_frame_config_t13frame_done_cbE"></a> <a id="_CPPv2N29bk_jpeg_decode_frame_config_t13frame_done_cbE"></a> <a id="bk_jpeg_decode_frame_config_t::frame_done_cb__bk_jpeg_decode_frame_done_cb"></a> <a id="structbk__jpeg__decode__frame__config__t_1aec083e21b87f6465d6c890678616bbaf"></a> [bk\_jpeg\_decode\_frame\_done\_cb](#_CPPv428bk_jpeg_decode_frame_done_cb "bk_jpeg_decode_frame_done_cb") frame\_done\_cb
    :   frame done callback

    <a id="_CPPv4N29bk_jpeg_decode_frame_config_t15frame_done_argsE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_frame_config_t15frame_done_argsE"></a> <a id="_CPPv2N29bk_jpeg_decode_frame_config_t15frame_done_argsE"></a> <a id="bk_jpeg_decode_frame_config_t::frame_done_args__voidP"></a> <a id="structbk__jpeg__decode__frame__config__t_1a98e8b9cc6d2ab3a93e1bf66fa71a62a9"></a> void \*frame\_done\_args
    :   frame done arguments

<a id="_CPPv429bk_jpeg_decode_flexa_config_t"></a>

<a id="_CPPv329bk_jpeg_decode_flexa_config_t"></a> <a id="_CPPv229bk_jpeg_decode_flexa_config_t"></a> <a id="bk_jpeg_decode_flexa_config_t"></a> <a id="structbk__jpeg__decode__flexa__config__t"></a> struct bk\_jpeg\_decode\_flexa\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t10timeout_msE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t10timeout_msE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t10timeout_msE"></a> <a id="bk_jpeg_decode_flexa_config_t::timeout_ms__uint32_t"></a> <a id="structbk__jpeg__decode__flexa__config__t_1a3305bee4ef7c4bebbfccf3fb3598959f"></a> uint32\_t timeout\_ms
    :   timeout in milliseconds

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t9out_widthE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t9out_widthE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t9out_widthE"></a> <a id="bk_jpeg_decode_flexa_config_t::out_width__uint16_t"></a> <a id="structbk__jpeg__decode__flexa__config__t_1aa5069b6aa35fe7d1cf7328f2f8947dc3"></a> uint16\_t out\_width
    :   output width

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t10out_heightE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t10out_heightE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t10out_heightE"></a> <a id="bk_jpeg_decode_flexa_config_t::out_height__uint16_t"></a> <a id="structbk__jpeg__decode__flexa__config__t_1aff4439c1380fe9e697612c75dd3f198f"></a> uint16\_t out\_height
    :   output height

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t10out_formatE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t10out_formatE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t10out_formatE"></a> <a id="bk_jpeg_decode_flexa_config_t::out_format__uint32_t"></a> <a id="structbk__jpeg__decode__flexa__config__t_1a15a8baf95d54255ed83ed9f31d960d80"></a> uint32\_t out\_format
    :   output format

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t14segment_heightE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t14segment_heightE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t14segment_heightE"></a> <a id="bk_jpeg_decode_flexa_config_t::segment_height__uint16_t"></a> <a id="structbk__jpeg__decode__flexa__config__t_1a1f744339e3210c952d7c7d854406348f"></a> uint16\_t segment\_height
    :   segment height

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t14segment_numberE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t14segment_numberE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t14segment_numberE"></a> <a id="bk_jpeg_decode_flexa_config_t::segment_number__uint8_t"></a> <a id="structbk__jpeg__decode__flexa__config__t_1a6802463d0ce3d4efab4803cd0417db75"></a> uint8\_t segment\_number
    :   segment number

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t13frame_done_cbE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t13frame_done_cbE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t13frame_done_cbE"></a> <a id="bk_jpeg_decode_flexa_config_t::frame_done_cb__bk_jpeg_decode_frame_done_cb"></a> <a id="structbk__jpeg__decode__flexa__config__t_1a0a9807822b1763a84749ccae23772e60"></a> [bk\_jpeg\_decode\_frame\_done\_cb](#_CPPv428bk_jpeg_decode_frame_done_cb "bk_jpeg_decode_frame_done_cb") frame\_done\_cb
    :   frame done callback

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t15frame_done_argsE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t15frame_done_argsE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t15frame_done_argsE"></a> <a id="bk_jpeg_decode_flexa_config_t::frame_done_args__voidP"></a> <a id="structbk__jpeg__decode__flexa__config__t_1a7cc9282788e4bce651e769177c00aa07"></a> void \*frame\_done\_args
    :   frame done arguments

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t13flexa_done_cbE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t13flexa_done_cbE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t13flexa_done_cbE"></a> <a id="bk_jpeg_decode_flexa_config_t::flexa_done_cb__bk_jpeg_decode_flexa_done_cb"></a> <a id="structbk__jpeg__decode__flexa__config__t_1acd50caae8c211e2daae6d67628c012c8"></a> [bk\_jpeg\_decode\_flexa\_done\_cb](#_CPPv428bk_jpeg_decode_flexa_done_cb "bk_jpeg_decode_flexa_done_cb") flexa\_done\_cb
    :   flexa done callback

    <a id="_CPPv4N29bk_jpeg_decode_flexa_config_t15flexa_done_argsE"></a>

    <a id="_CPPv3N29bk_jpeg_decode_flexa_config_t15flexa_done_argsE"></a> <a id="_CPPv2N29bk_jpeg_decode_flexa_config_t15flexa_done_argsE"></a> <a id="bk_jpeg_decode_flexa_config_t::flexa_done_args__voidP"></a> <a id="structbk__jpeg__decode__flexa__config__t_1a2b7890a975f0dfcfa31e350fe86fa0fa"></a> void \*flexa\_done\_args
    :   flexa done arguments

<a id="_CPPv422bk_jpeg_decode_input_t"></a>

<a id="_CPPv322bk_jpeg_decode_input_t"></a> <a id="_CPPv222bk_jpeg_decode_input_t"></a> <a id="bk_jpeg_decode_input_t"></a> <a id="structbk__jpeg__decode__input__t"></a> struct bk\_jpeg\_decode\_input\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_jpeg_decode_input_t6streamE"></a>

    <a id="_CPPv3N22bk_jpeg_decode_input_t6streamE"></a> <a id="_CPPv2N22bk_jpeg_decode_input_t6streamE"></a> <a id="bk_jpeg_decode_input_t::stream__uint8_tP"></a> <a id="structbk__jpeg__decode__input__t_1a0648b4585b16f4f33bf8c06110ae37e6"></a> uint8\_t \*stream
    :   input stream

    <a id="_CPPv4N22bk_jpeg_decode_input_t10stream_lenE"></a>

    <a id="_CPPv3N22bk_jpeg_decode_input_t10stream_lenE"></a> <a id="_CPPv2N22bk_jpeg_decode_input_t10stream_lenE"></a> <a id="bk_jpeg_decode_input_t::stream_len__uint32_t"></a> <a id="structbk__jpeg__decode__input__t_1a9ac3f29545e6dd73255267ac3f78c939"></a> uint32\_t stream\_len
    :   input stream length

    <a id="_CPPv4N22bk_jpeg_decode_input_t10out_bufferE"></a>

    <a id="_CPPv3N22bk_jpeg_decode_input_t10out_bufferE"></a> <a id="_CPPv2N22bk_jpeg_decode_input_t10out_bufferE"></a> <a id="bk_jpeg_decode_input_t::out_buffer__uint8_tP"></a> <a id="structbk__jpeg__decode__input__t_1ac3e2d9460bcd15957b8e515687f72ff2"></a> uint8\_t \*out\_buffer
    :   output buffer

    <a id="_CPPv4N22bk_jpeg_decode_input_t15out_buffer_sizeE"></a>

    <a id="_CPPv3N22bk_jpeg_decode_input_t15out_buffer_sizeE"></a> <a id="_CPPv2N22bk_jpeg_decode_input_t15out_buffer_sizeE"></a> <a id="bk_jpeg_decode_input_t::out_buffer_size__uint32_t"></a> <a id="structbk__jpeg__decode__input__t_1af68a29ceca42ff7096b1df2eff4eb0c6"></a> uint32\_t out\_buffer\_size
    :   output buffer size

<a id="_CPPv423bk_jpeg_decode_img_info"></a>

<a id="_CPPv323bk_jpeg_decode_img_info"></a> <a id="_CPPv223bk_jpeg_decode_img_info"></a> <a id="bk_jpeg_decode_img_info"></a> <a id="structbk__jpeg__decode__img__info"></a> struct bk\_jpeg\_decode\_img\_info
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23bk_jpeg_decode_img_info12input_streamE"></a>

    <a id="_CPPv3N23bk_jpeg_decode_img_info12input_streamE"></a> <a id="_CPPv2N23bk_jpeg_decode_img_info12input_streamE"></a> <a id="bk_jpeg_decode_img_info::input_stream__uint8_tP"></a> <a id="structbk__jpeg__decode__img__info_1a3465763a1c0435cf45e40d8c521884b9"></a> uint8\_t \*input\_stream
    :   Input: JPEG stream buffer

    <a id="_CPPv4N23bk_jpeg_decode_img_info19input_stream_lengthE"></a>

    <a id="_CPPv3N23bk_jpeg_decode_img_info19input_stream_lengthE"></a> <a id="_CPPv2N23bk_jpeg_decode_img_info19input_stream_lengthE"></a> <a id="bk_jpeg_decode_img_info::input_stream_length__uint32_t"></a> <a id="structbk__jpeg__decode__img__info_1a37cb1055f14795b6d8eb01168f4b487e"></a> uint32\_t input\_stream\_length
    :   Input: JPEG stream length

    <a id="_CPPv4N23bk_jpeg_decode_img_info5widthE"></a>

    <a id="_CPPv3N23bk_jpeg_decode_img_info5widthE"></a> <a id="_CPPv2N23bk_jpeg_decode_img_info5widthE"></a> <a id="bk_jpeg_decode_img_info::width__uint32_t"></a> <a id="structbk__jpeg__decode__img__info_1a0edac5a5ea4a5862cfec5af23d5157b2"></a> uint32\_t width
    :   Output: Image width in pixels

    <a id="_CPPv4N23bk_jpeg_decode_img_info6heightE"></a>

    <a id="_CPPv3N23bk_jpeg_decode_img_info6heightE"></a> <a id="_CPPv2N23bk_jpeg_decode_img_info6heightE"></a> <a id="bk_jpeg_decode_img_info::height__uint32_t"></a> <a id="structbk__jpeg__decode__img__info_1a57f583e2b61cb2486822cf68c2804996"></a> uint32\_t height
    :   Output: Image height in pixels

    <a id="_CPPv4N23bk_jpeg_decode_img_info6formatE"></a>

    <a id="_CPPv3N23bk_jpeg_decode_img_info6formatE"></a> <a id="_CPPv2N23bk_jpeg_decode_img_info6formatE"></a> <a id="bk_jpeg_decode_img_info::format__bk_jpeg_decode_img_fmt_t"></a> <a id="structbk__jpeg__decode__img__info_1a63849e05157b55bd5f1cf1e072d09853"></a> [bk\_jpeg\_decode\_img\_fmt\_t](#_CPPv424bk_jpeg_decode_img_fmt_t "bk_jpeg_decode_img_fmt_t") format
    :   Output: Image format (see bk\_jpeg\_decode\_img\_fmt\_t)

<a id="_CPPv421bk_jpeg_decode_ctlr_t"></a>

<a id="_CPPv321bk_jpeg_decode_ctlr_t"></a> <a id="_CPPv221bk_jpeg_decode_ctlr_t"></a> <a id="bk_jpeg_decode_ctlr_t"></a> <a id="structbk__jpeg__decode__ctlr__t"></a> struct bk\_jpeg\_decode\_ctlr\_t

<a id="id16"></a>

#### Macros

<a id="c.BK_JPEG_DECODE_RD_PORT_MAX"></a>

<a id="bk__jpeg__decode__types_8h_1a687e34f8394b5239bb25d4356c9abda6"></a> BK\_JPEG\_DECODE\_RD\_PORT\_MAX

<a id="c.DEFAULT_JPEG_DECODE_FLEXA_CONFIG"></a>

<a id="bk__jpeg__decode__types_8h_1a1c07a5820fff6522c99f3e98a374db8d"></a> DEFAULT\_JPEG\_DECODE\_FLEXA\_CONFIG

<a id="c.DEFAULT_JPEG_DECODE_FRAME_CONFIG"></a>

<a id="bk__jpeg__decode__types_8h_1ac338ac2d4cb222f77673a3fe46480c5f"></a> DEFAULT\_JPEG\_DECODE\_FRAME\_CONFIG

<a id="id17"></a>

#### Type Definitions

<a id="_CPPv428bk_jpeg_decode_frame_done_cb"></a>

<a id="_CPPv328bk_jpeg_decode_frame_done_cb"></a> <a id="_CPPv228bk_jpeg_decode_frame_done_cb"></a> <a id="bk_jpeg_decode_frame_done_cb"></a> <a id="bk__jpeg__decode__types_8h_1acb52f8b4c534fc0d08d0f443ee32bb9b"></a> typedef void (\*bk\_jpeg\_decode\_frame\_done\_cb)(int status, void \*args)
:   JPEG decode result callback: (status, args).

<a id="_CPPv428bk_jpeg_decode_flexa_done_cb"></a>

<a id="_CPPv328bk_jpeg_decode_flexa_done_cb"></a> <a id="_CPPv228bk_jpeg_decode_flexa_done_cb"></a> <a id="bk_jpeg_decode_flexa_done_cb"></a> <a id="bk__jpeg__decode__types_8h_1a67081c3125fb23a5d8e7ce7ce99d038c"></a> typedef void (\*bk\_jpeg\_decode\_flexa\_done\_cb)(uint32\_t wr\_ptr, void \*args)
:   Flexa done callback: (wr\_ptr, args).

<a id="_CPPv425bk_jpeg_decode_img_info_t"></a>

<a id="_CPPv325bk_jpeg_decode_img_info_t"></a> <a id="_CPPv225bk_jpeg_decode_img_info_t"></a> <a id="bk_jpeg_decode_img_info_t"></a> <a id="bk__jpeg__decode__types_8h_1ab03eb01de1b36445b95158295fe742c7"></a> typedef struct [bk\_jpeg\_decode\_img\_info](#_CPPv423bk_jpeg_decode_img_info "bk_jpeg_decode_img_info") bk\_jpeg\_decode\_img\_info\_t

<a id="_CPPv428bk_jpeg_decode_ctlr_handle_t"></a>

<a id="_CPPv328bk_jpeg_decode_ctlr_handle_t"></a> <a id="_CPPv228bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk_jpeg_decode_ctlr_handle_t"></a> <a id="bk__jpeg__decode__types_8h_1a748c13e9cc36e8fd5dd1e7570ccb5964"></a> typedef struct [bk\_jpeg\_decode\_ctlr\_t](#_CPPv421bk_jpeg_decode_ctlr_t "bk_jpeg_decode_ctlr_t") \*bk\_jpeg\_decode\_ctlr\_handle\_t

<a id="bk__jpeg__decode__types_8h_1ab737c724c4005ddd7a81bf8fc0506240"></a> typedef struct [bk\_jpeg\_decode\_ctlr\_t](#_CPPv421bk_jpeg_decode_ctlr_t "bk_jpeg_decode_ctlr_t") bk\_jpeg\_decode\_ctlr\_t

<a id="id18"></a>

#### Enumerations

<a id="_CPPv426bk_jpeg_decode_ioctl_cmd_t"></a>

<a id="_CPPv326bk_jpeg_decode_ioctl_cmd_t"></a> <a id="_CPPv226bk_jpeg_decode_ioctl_cmd_t"></a> <a id="bk__jpeg__decode__types_8h_1a755fa72608f92ef5e64e1012ff60c959"></a> enum bk\_jpeg\_decode\_ioctl\_cmd\_t
:   *Values:*

    <a id="_CPPv4N26bk_jpeg_decode_ioctl_cmd_t29BK_JPEG_DECODE_IOCTL_GET_INFOE"></a>

    <a id="_CPPv3N26bk_jpeg_decode_ioctl_cmd_t29BK_JPEG_DECODE_IOCTL_GET_INFOE"></a> <a id="_CPPv2N26bk_jpeg_decode_ioctl_cmd_t29BK_JPEG_DECODE_IOCTL_GET_INFOE"></a> <a id="bk__jpeg__decode__types_8h_1a755fa72608f92ef5e64e1012ff60c959ac5ed331daa050e187ea62b63bb4ff823"></a> enumerator BK\_JPEG\_DECODE\_IOCTL\_GET\_INFO
    :   Get image info see bk\_jpeg\_decode\_img\_info\_t

    <a id="_CPPv4N26bk_jpeg_decode_ioctl_cmd_t26BK_JPEG_DECODE_IOCTL_ABORTE"></a>

    <a id="_CPPv3N26bk_jpeg_decode_ioctl_cmd_t26BK_JPEG_DECODE_IOCTL_ABORTE"></a> <a id="_CPPv2N26bk_jpeg_decode_ioctl_cmd_t26BK_JPEG_DECODE_IOCTL_ABORTE"></a> <a id="bk__jpeg__decode__types_8h_1a755fa72608f92ef5e64e1012ff60c959a5382a37955e4235d27db854e1a7f28ee"></a> enumerator BK\_JPEG\_DECODE\_IOCTL\_ABORT
    :   Abort decode

    <a id="_CPPv4N26bk_jpeg_decode_ioctl_cmd_t36BK_JPEG_DECODE_IOCTL_PORT_SET_RD_PTRE"></a>

    <a id="_CPPv3N26bk_jpeg_decode_ioctl_cmd_t36BK_JPEG_DECODE_IOCTL_PORT_SET_RD_PTRE"></a> <a id="_CPPv2N26bk_jpeg_decode_ioctl_cmd_t36BK_JPEG_DECODE_IOCTL_PORT_SET_RD_PTRE"></a> <a id="bk__jpeg__decode__types_8h_1a755fa72608f92ef5e64e1012ff60c959afd8fc8acb4a2ea70bf2f44f3fbb1b412"></a> enumerator BK\_JPEG\_DECODE\_IOCTL\_PORT\_SET\_RD\_PTR
    :   Set read pointer see [bk\_jpeg\_decode\_port\_rd\_t](#structbk__jpeg__decode__port__rd__t)

    <a id="_CPPv4N26bk_jpeg_decode_ioctl_cmd_t34BK_JPEG_DECODE_IOCTL_REGISTER_BONDE"></a>

    <a id="_CPPv3N26bk_jpeg_decode_ioctl_cmd_t34BK_JPEG_DECODE_IOCTL_REGISTER_BONDE"></a> <a id="_CPPv2N26bk_jpeg_decode_ioctl_cmd_t34BK_JPEG_DECODE_IOCTL_REGISTER_BONDE"></a> <a id="bk__jpeg__decode__types_8h_1a755fa72608f92ef5e64e1012ff60c959ac652122872285a301d171c2fecc3c6a1"></a> enumerator BK\_JPEG\_DECODE\_IOCTL\_REGISTER\_BOND
    :   Register bond should be ptr for the bond

    <a id="_CPPv4N26bk_jpeg_decode_ioctl_cmd_t36BK_JPEG_DECODE_IOCTL_UNREGISTER_BONDE"></a>

    <a id="_CPPv3N26bk_jpeg_decode_ioctl_cmd_t36BK_JPEG_DECODE_IOCTL_UNREGISTER_BONDE"></a> <a id="_CPPv2N26bk_jpeg_decode_ioctl_cmd_t36BK_JPEG_DECODE_IOCTL_UNREGISTER_BONDE"></a> <a id="bk__jpeg__decode__types_8h_1a755fa72608f92ef5e64e1012ff60c959aba97179b83f15797a1584a0079d3557e"></a> enumerator BK\_JPEG\_DECODE\_IOCTL\_UNREGISTER\_BOND
    :   Unregister bond should be ptr for the bond

    <a id="_CPPv4N26bk_jpeg_decode_ioctl_cmd_t43BK_JPEG_DECODE_IOCTL_FLEXA_NOTIFY_PORT_DONEE"></a>

    <a id="_CPPv3N26bk_jpeg_decode_ioctl_cmd_t43BK_JPEG_DECODE_IOCTL_FLEXA_NOTIFY_PORT_DONEE"></a> <a id="_CPPv2N26bk_jpeg_decode_ioctl_cmd_t43BK_JPEG_DECODE_IOCTL_FLEXA_NOTIFY_PORT_DONEE"></a> <a id="bk__jpeg__decode__types_8h_1a755fa72608f92ef5e64e1012ff60c959adb84ed84fac0e5a98e0600d741b58ef8"></a> enumerator BK\_JPEG\_DECODE\_IOCTL\_FLEXA\_NOTIFY\_PORT\_DONE
    :   Notify port done should be ptr for the port

<a id="_CPPv427bk_jpeg_decode_rd_port_id_t"></a>

<a id="_CPPv327bk_jpeg_decode_rd_port_id_t"></a> <a id="_CPPv227bk_jpeg_decode_rd_port_id_t"></a> <a id="bk__jpeg__decode__types_8h_1a7d73f1f255d5ffebc1a0572fd927a0da"></a> enum bk\_jpeg\_decode\_rd\_port\_id\_t
:   *Values:*

    <a id="_CPPv4N27bk_jpeg_decode_rd_port_id_t26BK_JPEG_DECODE_RD_PORT_GPUE"></a>

    <a id="_CPPv3N27bk_jpeg_decode_rd_port_id_t26BK_JPEG_DECODE_RD_PORT_GPUE"></a> <a id="_CPPv2N27bk_jpeg_decode_rd_port_id_t26BK_JPEG_DECODE_RD_PORT_GPUE"></a> <a id="bk__jpeg__decode__types_8h_1a7d73f1f255d5ffebc1a0572fd927a0daaecdaa0e5fd6ef56f626bf92d46275db7"></a> enumerator BK\_JPEG\_DECODE\_RD\_PORT\_GPU

    <a id="_CPPv4N27bk_jpeg_decode_rd_port_id_t28BK_JPEG_DECODE_RD_PORT_H264EE"></a>

    <a id="_CPPv3N27bk_jpeg_decode_rd_port_id_t28BK_JPEG_DECODE_RD_PORT_H264EE"></a> <a id="_CPPv2N27bk_jpeg_decode_rd_port_id_t28BK_JPEG_DECODE_RD_PORT_H264EE"></a> <a id="bk__jpeg__decode__types_8h_1a7d73f1f255d5ffebc1a0572fd927a0daa58333ca61988dde4f6572edf3260c8c1"></a> enumerator BK\_JPEG\_DECODE\_RD\_PORT\_H264E

<a id="_CPPv427bk_jpeg_decode_flexa_mode_t"></a>

<a id="_CPPv327bk_jpeg_decode_flexa_mode_t"></a> <a id="_CPPv227bk_jpeg_decode_flexa_mode_t"></a> <a id="bk__jpeg__decode__types_8h_1acc3a5d0973c98140b30df0ffce6ad275"></a> enum bk\_jpeg\_decode\_flexa\_mode\_t
:   *Values:*

    <a id="_CPPv4N27bk_jpeg_decode_flexa_mode_t30BK_JPEG_DECODE_FLEXA_MODE_NONEE"></a>

    <a id="_CPPv3N27bk_jpeg_decode_flexa_mode_t30BK_JPEG_DECODE_FLEXA_MODE_NONEE"></a> <a id="_CPPv2N27bk_jpeg_decode_flexa_mode_t30BK_JPEG_DECODE_FLEXA_MODE_NONEE"></a> <a id="bk__jpeg__decode__types_8h_1acc3a5d0973c98140b30df0ffce6ad275abdfa896221e324ec83fbf21c57324224"></a> enumerator BK\_JPEG\_DECODE\_FLEXA\_MODE\_NONE

    <a id="_CPPv4N27bk_jpeg_decode_flexa_mode_t31BK_JPEG_DECODE_FLEXA_MODE_FLEXAE"></a>

    <a id="_CPPv3N27bk_jpeg_decode_flexa_mode_t31BK_JPEG_DECODE_FLEXA_MODE_FLEXAE"></a> <a id="_CPPv2N27bk_jpeg_decode_flexa_mode_t31BK_JPEG_DECODE_FLEXA_MODE_FLEXAE"></a> <a id="bk__jpeg__decode__types_8h_1acc3a5d0973c98140b30df0ffce6ad275a0d0e7ec7c783fc2c61aaf0d1f1aa9347"></a> enumerator BK\_JPEG\_DECODE\_FLEXA\_MODE\_FLEXA

<a id="_CPPv424bk_jpeg_decode_img_fmt_t"></a>

<a id="_CPPv324bk_jpeg_decode_img_fmt_t"></a> <a id="_CPPv224bk_jpeg_decode_img_fmt_t"></a> <a id="bk__jpeg__decode__types_8h_1a8bf485d192c1ff73949575aef4a88f60"></a> enum bk\_jpeg\_decode\_img\_fmt\_t
:   *Values:*

    <a id="_CPPv4N24bk_jpeg_decode_img_fmt_t26BK_JPEG_DECODE_IMG_FMT_ERRE"></a>

    <a id="_CPPv3N24bk_jpeg_decode_img_fmt_t26BK_JPEG_DECODE_IMG_FMT_ERRE"></a> <a id="_CPPv2N24bk_jpeg_decode_img_fmt_t26BK_JPEG_DECODE_IMG_FMT_ERRE"></a> <a id="bk__jpeg__decode__types_8h_1a8bf485d192c1ff73949575aef4a88f60a6cd948971c3cc639e1dc409af50382d8"></a> enumerator BK\_JPEG\_DECODE\_IMG\_FMT\_ERR
    :   Invalid or unsupported image format

    <a id="_CPPv4N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV444E"></a>

    <a id="_CPPv3N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV444E"></a> <a id="_CPPv2N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV444E"></a> <a id="bk__jpeg__decode__types_8h_1a8bf485d192c1ff73949575aef4a88f60a613b813a6349b7c40df1ffc178c420d7"></a> enumerator BK\_JPEG\_DECODE\_IMG\_FMT\_YUV444
    :   YUV 4:4:4 format \- full chroma resolution, no subsampling

    <a id="_CPPv4N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV422E"></a>

    <a id="_CPPv3N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV422E"></a> <a id="_CPPv2N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV422E"></a> <a id="bk__jpeg__decode__types_8h_1a8bf485d192c1ff73949575aef4a88f60a8185b24799ad14e6c1c9e920d8bfac53"></a> enumerator BK\_JPEG\_DECODE\_IMG\_FMT\_YUV422
    :   YUV 4:2:2 format \- horizontal chroma subsampling by 2:1

    <a id="_CPPv4N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV420E"></a>

    <a id="_CPPv3N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV420E"></a> <a id="_CPPv2N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV420E"></a> <a id="bk__jpeg__decode__types_8h_1a8bf485d192c1ff73949575aef4a88f60abe8e8cdf7edddc280cd1ed2f14ac74a3"></a> enumerator BK\_JPEG\_DECODE\_IMG\_FMT\_YUV420
    :   YUV 4:2:0 format \- horizontal and vertical chroma subsampling by 2:1

    <a id="_CPPv4N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV400E"></a>

    <a id="_CPPv3N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV400E"></a> <a id="_CPPv2N24bk_jpeg_decode_img_fmt_t29BK_JPEG_DECODE_IMG_FMT_YUV400E"></a> <a id="bk__jpeg__decode__types_8h_1a8bf485d192c1ff73949575aef4a88f60a3ab3ab71cd2d97e7ca2ca8bbdd2e23d4"></a> enumerator BK\_JPEG\_DECODE\_IMG\_FMT\_YUV400
    :   YUV 4:0:0 format \- grayscale image with only luma component

    <a id="_CPPv4N24bk_jpeg_decode_img_fmt_t26BK_JPEG_DECODE_IMG_FMT_MAXE"></a>

    <a id="_CPPv3N24bk_jpeg_decode_img_fmt_t26BK_JPEG_DECODE_IMG_FMT_MAXE"></a> <a id="_CPPv2N24bk_jpeg_decode_img_fmt_t26BK_JPEG_DECODE_IMG_FMT_MAXE"></a> <a id="bk__jpeg__decode__types_8h_1a8bf485d192c1ff73949575aef4a88f60af71f0f4050de2544ff8a485d83292957"></a> enumerator BK\_JPEG\_DECODE\_IMG\_FMT\_MAX

<a id="jpeg-encode"></a>

### JPEG Encode

<a id="id19"></a>

#### Header File

- [bk\_jpeg\_encode\_ctlr.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_encode/bk_jpeg_encode_ctlr.h)

<a id="id20"></a>

#### Functions

<a id="_CPPv424bk_jpeg_encode_frame_newP28bk_jpeg_encode_ctlr_handle_tP29bk_jpeg_encode_frame_config_t"></a>

<a id="_CPPv324bk_jpeg_encode_frame_newP28bk_jpeg_encode_ctlr_handle_tP29bk_jpeg_encode_frame_config_t"></a> <a id="_CPPv224bk_jpeg_encode_frame_newP28bk_jpeg_encode_ctlr_handle_tP29bk_jpeg_encode_frame_config_t"></a> <a id="bk_jpeg_encode_frame_new__bk_jpeg_encode_ctlr_handle_tP.bk_jpeg_encode_frame_config_tP"></a> <a id="bk__jpeg__encode__ctlr_8h_1a85a2153204ab2263c47b249b1319d894"></a> avdk\_err\_t bk\_jpeg\_encode\_frame\_new([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") \*handle, [bk\_jpeg\_encode\_frame\_config\_t](#_CPPv429bk_jpeg_encode_frame_config_t "bk_jpeg_encode_frame_config_t") \*config)
:   Create frame-mode JPEG encoder (VCENC JPEG path).

    参数
    :   - **handle** – Output pointer that receives the encoder handle
        - **config** – Frame encoder configuration

    返回
    :   AVDK error code

<a id="_CPPv427bk_jpeg_encode_sw_frame_newP28bk_jpeg_encode_ctlr_handle_tP32bk_jpeg_encode_sw_frame_config_t"></a>

<a id="_CPPv327bk_jpeg_encode_sw_frame_newP28bk_jpeg_encode_ctlr_handle_tP32bk_jpeg_encode_sw_frame_config_t"></a> <a id="_CPPv227bk_jpeg_encode_sw_frame_newP28bk_jpeg_encode_ctlr_handle_tP32bk_jpeg_encode_sw_frame_config_t"></a> <a id="bk_jpeg_encode_sw_frame_new__bk_jpeg_encode_ctlr_handle_tP.bk_jpeg_encode_sw_frame_config_tP"></a> <a id="bk__jpeg__encode__ctlr_8h_1afb33ba38a48686c3bcedf3d86c2fedb7"></a> avdk\_err\_t bk\_jpeg\_encode\_sw\_frame\_new([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") \*handle, [bk\_jpeg\_encode\_sw\_frame\_config\_t](#_CPPv432bk_jpeg_encode_sw_frame_config_t "bk_jpeg_encode_sw_frame_config_t") \*config)
:   Create software frame-mode JPEG encoder.

    参数
    :   - **handle** – Output pointer that receives the encoder handle
        - **config** – Software frame encoder configuration

    返回
    :   AVDK error code

<a id="_CPPv427bk_jpeg_encode_hw_flexa_newP28bk_jpeg_encode_ctlr_handle_tP32bk_jpeg_encode_hw_flexa_config_t"></a>

<a id="_CPPv327bk_jpeg_encode_hw_flexa_newP28bk_jpeg_encode_ctlr_handle_tP32bk_jpeg_encode_hw_flexa_config_t"></a> <a id="_CPPv227bk_jpeg_encode_hw_flexa_newP28bk_jpeg_encode_ctlr_handle_tP32bk_jpeg_encode_hw_flexa_config_t"></a> <a id="bk_jpeg_encode_hw_flexa_new__bk_jpeg_encode_ctlr_handle_tP.bk_jpeg_encode_hw_flexa_config_tP"></a> <a id="bk__jpeg__encode__ctlr_8h_1adf6f2aa159eb0d4d597f4857c1a68b19"></a> avdk\_err\_t bk\_jpeg\_encode\_hw\_flexa\_new([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") \*handle, [bk\_jpeg\_encode\_hw\_flexa\_config\_t](#_CPPv432bk_jpeg_encode_hw_flexa_config_t "bk_jpeg_encode_hw_flexa_config_t") \*config)
:   Create hardware-Flexa JPEG encoder (VCENC JPEG low-latency HW sync path).

    参数
    :   - **handle** – Output pointer that receives the encoder handle
        - **config** – Hardware Flexa encoder configuration

    返回
    :   AVDK error code

<a id="_CPPv427bk_jpeg_encode_sw_flexa_newP28bk_jpeg_encode_ctlr_handle_tP32bk_jpeg_encode_sw_flexa_config_t"></a>

<a id="_CPPv327bk_jpeg_encode_sw_flexa_newP28bk_jpeg_encode_ctlr_handle_tP32bk_jpeg_encode_sw_flexa_config_t"></a> <a id="_CPPv227bk_jpeg_encode_sw_flexa_newP28bk_jpeg_encode_ctlr_handle_tP32bk_jpeg_encode_sw_flexa_config_t"></a> <a id="bk_jpeg_encode_sw_flexa_new__bk_jpeg_encode_ctlr_handle_tP.bk_jpeg_encode_sw_flexa_config_tP"></a> <a id="bk__jpeg__encode__ctlr_8h_1a54917645ae191db2738498011f38a1ce"></a> avdk\_err\_t bk\_jpeg\_encode\_sw\_flexa\_new([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") \*handle, [bk\_jpeg\_encode\_sw\_flexa\_config\_t](#_CPPv432bk_jpeg_encode_sw_flexa_config_t "bk_jpeg_encode_sw_flexa_config_t") \*config)
:   Create software-Flexa JPEG encoder (VCENC JPEG low-latency SW sync path).

    参数
    :   - **handle** – Output pointer that receives the encoder handle
        - **config** – Software Flexa encoder configuration

    返回
    :   AVDK error code

<a id="_CPPv419bk_jpeg_encode_init28bk_jpeg_encode_ctlr_handle_t"></a>

<a id="_CPPv319bk_jpeg_encode_init28bk_jpeg_encode_ctlr_handle_t"></a> <a id="_CPPv219bk_jpeg_encode_init28bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk_jpeg_encode_init__bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk__jpeg__encode__ctlr_8h_1aae676884feba8f45c76481a24dafc7bd"></a> avdk\_err\_t bk\_jpeg\_encode\_init([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Initialize the JPEG encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code

<a id="_CPPv421bk_jpeg_encode_deinit28bk_jpeg_encode_ctlr_handle_t"></a>

<a id="_CPPv321bk_jpeg_encode_deinit28bk_jpeg_encode_ctlr_handle_t"></a> <a id="_CPPv221bk_jpeg_encode_deinit28bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk_jpeg_encode_deinit__bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk__jpeg__encode__ctlr_8h_1a51e3d6d55f8acb826f29495edd229153"></a> avdk\_err\_t bk\_jpeg\_encode\_deinit([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Deinitialize the JPEG encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code

<a id="_CPPv419bk_jpeg_encode_open28bk_jpeg_encode_ctlr_handle_t"></a>

<a id="_CPPv319bk_jpeg_encode_open28bk_jpeg_encode_ctlr_handle_t"></a> <a id="_CPPv219bk_jpeg_encode_open28bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk_jpeg_encode_open__bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk__jpeg__encode__ctlr_8h_1a62f68da2e38be2559a489e5575670fc1"></a> avdk\_err\_t bk\_jpeg\_encode\_open([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Open the JPEG encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code

<a id="_CPPv420bk_jpeg_encode_close28bk_jpeg_encode_ctlr_handle_t"></a>

<a id="_CPPv320bk_jpeg_encode_close28bk_jpeg_encode_ctlr_handle_t"></a> <a id="_CPPv220bk_jpeg_encode_close28bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk_jpeg_encode_close__bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk__jpeg__encode__ctlr_8h_1af320165856d1cba977ca8136a84b29c4"></a> avdk\_err\_t bk\_jpeg\_encode\_close([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Close the JPEG encoder.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code

<a id="_CPPv420bk_jpeg_encode_frame28bk_jpeg_encode_ctlr_handle_tP22bk_jpeg_encode_input_t"></a>

<a id="_CPPv320bk_jpeg_encode_frame28bk_jpeg_encode_ctlr_handle_tP22bk_jpeg_encode_input_t"></a> <a id="_CPPv220bk_jpeg_encode_frame28bk_jpeg_encode_ctlr_handle_tP22bk_jpeg_encode_input_t"></a> <a id="bk_jpeg_encode_frame__bk_jpeg_encode_ctlr_handle_t.bk_jpeg_encode_input_tP"></a> <a id="bk__jpeg__encode__ctlr_8h_1a921388e72cd4b73207f1c1ac3824054a"></a> avdk\_err\_t bk\_jpeg\_encode\_frame([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle, [bk\_jpeg\_encode\_input\_t](#_CPPv422bk_jpeg_encode_input_t "bk_jpeg_encode_input_t") \*input)
:   Encode one JPEG frame.

    参数
    :   - **handle** – Encoder handle
        - **input** – Input pixel buffer and output descriptors

    返回
    :   AVDK error code

<a id="_CPPv420bk_jpeg_encode_ioctl28bk_jpeg_encode_ctlr_handle_t26bk_jpeg_encode_ioctl_cmd_tPv"></a>

<a id="_CPPv320bk_jpeg_encode_ioctl28bk_jpeg_encode_ctlr_handle_t26bk_jpeg_encode_ioctl_cmd_tPv"></a> <a id="_CPPv220bk_jpeg_encode_ioctl28bk_jpeg_encode_ctlr_handle_t26bk_jpeg_encode_ioctl_cmd_tPv"></a> <a id="bk_jpeg_encode_ioctl__bk_jpeg_encode_ctlr_handle_t.bk_jpeg_encode_ioctl_cmd_t.voidP"></a> <a id="bk__jpeg__encode__ctlr_8h_1a09a00890365466b1005a50ad98f0ff82"></a> avdk\_err\_t bk\_jpeg\_encode\_ioctl([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle, [bk\_jpeg\_encode\_ioctl\_cmd\_t](#_CPPv426bk_jpeg_encode_ioctl_cmd_t "bk_jpeg_encode_ioctl_cmd_t") cmd, void \*arg)
:   Issue an IOCTL command on the JPEG encoder.

    参数
    :   - **handle** – Encoder handle
        - **cmd** – IOCTL command (e.g. quality setting)
        - **arg** – Command-specific argument

    返回
    :   AVDK error code

<a id="_CPPv421bk_jpeg_encode_delete28bk_jpeg_encode_ctlr_handle_t"></a>

<a id="_CPPv321bk_jpeg_encode_delete28bk_jpeg_encode_ctlr_handle_t"></a> <a id="_CPPv221bk_jpeg_encode_delete28bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk_jpeg_encode_delete__bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk__jpeg__encode__ctlr_8h_1a5bdc83259495abb4f2a7833e55a17c38"></a> avdk\_err\_t bk\_jpeg\_encode\_delete([bk\_jpeg\_encode\_ctlr\_handle\_t](#_CPPv428bk_jpeg_encode_ctlr_handle_t "bk_jpeg_encode_ctlr_handle_t") handle)
:   Delete the JPEG encoder controller.

    参数
    :   **handle** – Encoder handle

    返回
    :   AVDK error code

<a id="jpeg-encode-types"></a>

### JPEG Encode Types

<a id="id21"></a>

#### Header File

- [bk\_jpeg\_encode\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_encode/bk_jpeg_encode_types.h)

<a id="id22"></a>

#### Structures

<a id="_CPPv428bk_jpeg_encode_outbuf_info_t"></a>

<a id="_CPPv328bk_jpeg_encode_outbuf_info_t"></a> <a id="_CPPv228bk_jpeg_encode_outbuf_info_t"></a> <a id="bk_jpeg_encode_outbuf_info_t"></a> <a id="structbk__jpeg__encode__outbuf__info__t"></a> struct bk\_jpeg\_encode\_outbuf\_info\_t

<a id="_CPPv429bk_jpeg_encode_frame_config_t"></a>

<a id="_CPPv329bk_jpeg_encode_frame_config_t"></a> <a id="_CPPv229bk_jpeg_encode_frame_config_t"></a> <a id="bk_jpeg_encode_frame_config_t"></a> <a id="structbk__jpeg__encode__frame__config__t"></a> struct bk\_jpeg\_encode\_frame\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N29bk_jpeg_encode_frame_config_t12input_formatE"></a>

    <a id="_CPPv3N29bk_jpeg_encode_frame_config_t12input_formatE"></a> <a id="_CPPv2N29bk_jpeg_encode_frame_config_t12input_formatE"></a> <a id="bk_jpeg_encode_frame_config_t::input_format__uint32_t"></a> <a id="structbk__jpeg__encode__frame__config__t_1a36787ca191806d4fa26c062855e15aa5"></a> uint32\_t input\_format
    :   e.g. BK\_PIXEL\_FORMAT\_NV12

    <a id="_CPPv4N29bk_jpeg_encode_frame_config_t9input_bufE"></a>

    <a id="_CPPv3N29bk_jpeg_encode_frame_config_t9input_bufE"></a> <a id="_CPPv2N29bk_jpeg_encode_frame_config_t9input_bufE"></a> <a id="bk_jpeg_encode_frame_config_t::input_buf__uint32_t"></a> <a id="structbk__jpeg__encode__frame__config__t_1a3c668d96d1c2665bb57dea6cee126d52"></a> uint32\_t input\_buf
    :   NV12 luma base (physical/bus address as used by VCENC)

    <a id="_CPPv4N29bk_jpeg_encode_frame_config_t10input_sizeE"></a>

    <a id="_CPPv3N29bk_jpeg_encode_frame_config_t10input_sizeE"></a> <a id="_CPPv2N29bk_jpeg_encode_frame_config_t10input_sizeE"></a> <a id="bk_jpeg_encode_frame_config_t::input_size__uint32_t"></a> <a id="structbk__jpeg__encode__frame__config__t_1a3414501dad00fe6e8672d40b649fa11a"></a> uint32\_t input\_size
    :   reserved; line count for flexa-like paths (unused for JPEG frame mode)

    <a id="_CPPv4N29bk_jpeg_encode_frame_config_t7qualityE"></a>

    <a id="_CPPv3N29bk_jpeg_encode_frame_config_t7qualityE"></a> <a id="_CPPv2N29bk_jpeg_encode_frame_config_t7qualityE"></a> <a id="bk_jpeg_encode_frame_config_t::quality__uint8_t"></a> <a id="structbk__jpeg__encode__frame__config__t_1ac8fae81feaa591f76db913820dce5b48"></a> uint8\_t quality
    :   0..10

<a id="_CPPv432bk_jpeg_encode_sw_frame_config_t"></a>

<a id="_CPPv332bk_jpeg_encode_sw_frame_config_t"></a> <a id="_CPPv232bk_jpeg_encode_sw_frame_config_t"></a> <a id="bk_jpeg_encode_sw_frame_config_t"></a> <a id="structbk__jpeg__encode__sw__frame__config__t"></a> struct bk\_jpeg\_encode\_sw\_frame\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N32bk_jpeg_encode_sw_frame_config_t12input_formatE"></a>

    <a id="_CPPv3N32bk_jpeg_encode_sw_frame_config_t12input_formatE"></a> <a id="_CPPv2N32bk_jpeg_encode_sw_frame_config_t12input_formatE"></a> <a id="bk_jpeg_encode_sw_frame_config_t::input_format__uint32_t"></a> <a id="structbk__jpeg__encode__sw__frame__config__t_1af2d0839485fb48ce29802d4a57472d8c"></a> uint32\_t input\_format
    :   e.g. BK\_PIXEL\_FORMAT\_YUYV

    <a id="_CPPv4N32bk_jpeg_encode_sw_frame_config_t9input_bufE"></a>

    <a id="_CPPv3N32bk_jpeg_encode_sw_frame_config_t9input_bufE"></a> <a id="_CPPv2N32bk_jpeg_encode_sw_frame_config_t9input_bufE"></a> <a id="bk_jpeg_encode_sw_frame_config_t::input_buf__uint32_t"></a> <a id="structbk__jpeg__encode__sw__frame__config__t_1ab4d3d9e011fa8d91ba1987b980e33952"></a> uint32\_t input\_buf
    :   YUYV input base address

<a id="_CPPv432bk_jpeg_encode_hw_flexa_config_t"></a>

<a id="_CPPv332bk_jpeg_encode_hw_flexa_config_t"></a> <a id="_CPPv232bk_jpeg_encode_hw_flexa_config_t"></a> <a id="bk_jpeg_encode_hw_flexa_config_t"></a> <a id="structbk__jpeg__encode__hw__flexa__config__t"></a> struct bk\_jpeg\_encode\_hw\_flexa\_config\_t

<a id="_CPPv432bk_jpeg_encode_sw_flexa_config_t"></a>

<a id="_CPPv332bk_jpeg_encode_sw_flexa_config_t"></a> <a id="_CPPv232bk_jpeg_encode_sw_flexa_config_t"></a> <a id="bk_jpeg_encode_sw_flexa_config_t"></a> <a id="structbk__jpeg__encode__sw__flexa__config__t"></a> struct bk\_jpeg\_encode\_sw\_flexa\_config\_t

<a id="_CPPv422bk_jpeg_encode_input_t"></a>

<a id="_CPPv322bk_jpeg_encode_input_t"></a> <a id="_CPPv222bk_jpeg_encode_input_t"></a> <a id="bk_jpeg_encode_input_t"></a> <a id="structbk__jpeg__encode__input__t"></a> struct bk\_jpeg\_encode\_input\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_jpeg_encode_input_t7pic_bufE"></a>

    <a id="_CPPv3N22bk_jpeg_encode_input_t7pic_bufE"></a> <a id="_CPPv2N22bk_jpeg_encode_input_t7pic_bufE"></a> <a id="bk_jpeg_encode_input_t::pic_buf__uint32_t"></a> <a id="structbk__jpeg__encode__input__t_1a3e34abbba9ba5b75ddb732ce6fb38272"></a> uint32\_t pic\_buf
    :   override input base for this frame

    <a id="_CPPv4N22bk_jpeg_encode_input_t9pic_linesE"></a>

    <a id="_CPPv3N22bk_jpeg_encode_input_t9pic_linesE"></a> <a id="_CPPv2N22bk_jpeg_encode_input_t9pic_linesE"></a> <a id="bk_jpeg_encode_input_t::pic_lines__uint32_t"></a> <a id="structbk__jpeg__encode__input__t_1aaf1263d46b5406730fea4f02f6e138b5"></a> uint32\_t pic\_lines
    :   unused

    <a id="_CPPv4N22bk_jpeg_encode_input_t7out_bufE"></a>

    <a id="_CPPv3N22bk_jpeg_encode_input_t7out_bufE"></a> <a id="_CPPv2N22bk_jpeg_encode_input_t7out_bufE"></a> <a id="bk_jpeg_encode_input_t::out_buf__uint32_t"></a> <a id="structbk__jpeg__encode__input__t_1ae4496766773a2272ccda0eec12e693fc"></a> uint32\_t out\_buf
    :   optional; 0 \= allocate via outbuf\_malloc

    <a id="_CPPv4N22bk_jpeg_encode_input_t8out_sizeE"></a>

    <a id="_CPPv3N22bk_jpeg_encode_input_t8out_sizeE"></a> <a id="_CPPv2N22bk_jpeg_encode_input_t8out_sizeE"></a> <a id="bk_jpeg_encode_input_t::out_size__uint32_t"></a> <a id="structbk__jpeg__encode__input__t_1a29c178d29e70ed12b113c1ff7048b0da"></a> uint32\_t out\_size
    :   optional output capacity when out\_buf non-zero

<a id="_CPPv421bk_jpeg_encode_ctlr_t"></a>

<a id="_CPPv321bk_jpeg_encode_ctlr_t"></a> <a id="_CPPv221bk_jpeg_encode_ctlr_t"></a> <a id="bk_jpeg_encode_ctlr_t"></a> <a id="structbk__jpeg__encode__ctlr__t"></a> struct bk\_jpeg\_encode\_ctlr\_t

<a id="id23"></a>

#### Macros

<a id="c.DEFAULT_JPEG_ENCODE_FRAME_CONFIG"></a>

<a id="bk__jpeg__encode__types_8h_1ace161eb6f124394adb607eb32f335b80"></a> DEFAULT\_JPEG\_ENCODE\_FRAME\_CONFIG

<a id="c.DEFAULT_JPEG_ENCODE_SW_FRAME_CONFIG"></a>

<a id="bk__jpeg__encode__types_8h_1ade502e9a171a0689aaeed0277a32b3cf"></a> DEFAULT\_JPEG\_ENCODE\_SW\_FRAME\_CONFIG

<a id="c.DEFAULT_JPEG_ENCODE_HW_FLEXA_CONFIG"></a>

<a id="bk__jpeg__encode__types_8h_1a5dd01b43aa8723830117c2d8ae504bd5"></a> DEFAULT\_JPEG\_ENCODE\_HW\_FLEXA\_CONFIG

<a id="c.DEFAULT_JPEG_ENCODE_SW_FLEXA_CONFIG"></a>

<a id="bk__jpeg__encode__types_8h_1ab61580d6a408cdb8bf06d8fdba5ef82d"></a> DEFAULT\_JPEG\_ENCODE\_SW\_FLEXA\_CONFIG

<a id="id24"></a>

#### Type Definitions

<a id="_CPPv428bk_jpeg_encode_flexa_done_cb"></a>

<a id="_CPPv328bk_jpeg_encode_flexa_done_cb"></a> <a id="_CPPv228bk_jpeg_encode_flexa_done_cb"></a> <a id="bk_jpeg_encode_flexa_done_cb"></a> <a id="bk__jpeg__encode__types_8h_1a4d26a6ef903ebbd1bf001f3547daaf44"></a> typedef void (\*bk\_jpeg\_encode\_flexa\_done\_cb)(uint32\_t rd\_blocks, void \*args)

<a id="_CPPv428bk_jpeg_encode_ctlr_handle_t"></a>

<a id="_CPPv328bk_jpeg_encode_ctlr_handle_t"></a> <a id="_CPPv228bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk_jpeg_encode_ctlr_handle_t"></a> <a id="bk__jpeg__encode__types_8h_1a761cffd42888804c081574c8d91a1030"></a> typedef struct [bk\_jpeg\_encode\_ctlr\_t](#_CPPv421bk_jpeg_encode_ctlr_t "bk_jpeg_encode_ctlr_t") \*bk\_jpeg\_encode\_ctlr\_handle\_t

<a id="bk__jpeg__encode__types_8h_1a1230245532ba2324923f5114aca027b1"></a> typedef struct [bk\_jpeg\_encode\_ctlr\_t](#_CPPv421bk_jpeg_encode_ctlr_t "bk_jpeg_encode_ctlr_t") bk\_jpeg\_encode\_ctlr\_t

<a id="id25"></a>

#### Enumerations

<a id="_CPPv426bk_jpeg_encode_ioctl_cmd_t"></a>

<a id="_CPPv326bk_jpeg_encode_ioctl_cmd_t"></a> <a id="_CPPv226bk_jpeg_encode_ioctl_cmd_t"></a> <a id="bk__jpeg__encode__types_8h_1a1fa2fd3dca6503f897f1ac83959dfbbc"></a> enum bk\_jpeg\_encode\_ioctl\_cmd\_t
:   *Values:*

    <a id="_CPPv4N26bk_jpeg_encode_ioctl_cmd_t32BK_JPEG_ENCODE_IOCTL_SET_QUALITYE"></a>

    <a id="_CPPv3N26bk_jpeg_encode_ioctl_cmd_t32BK_JPEG_ENCODE_IOCTL_SET_QUALITYE"></a> <a id="_CPPv2N26bk_jpeg_encode_ioctl_cmd_t32BK_JPEG_ENCODE_IOCTL_SET_QUALITYE"></a> <a id="bk__jpeg__encode__types_8h_1a1fa2fd3dca6503f897f1ac83959dfbbca5edd33f3fed80c779247c2ba88b0bec7"></a> enumerator BK\_JPEG\_ENCODE\_IOCTL\_SET\_QUALITY
    :   arg: uint8\_t \* quality 0..10

    <a id="_CPPv4N26bk_jpeg_encode_ioctl_cmd_t42BK_JPEG_ENCODE_IOCTL_SET_FLEXA_LINES_READYE"></a>

    <a id="_CPPv3N26bk_jpeg_encode_ioctl_cmd_t42BK_JPEG_ENCODE_IOCTL_SET_FLEXA_LINES_READYE"></a> <a id="_CPPv2N26bk_jpeg_encode_ioctl_cmd_t42BK_JPEG_ENCODE_IOCTL_SET_FLEXA_LINES_READYE"></a> <a id="bk__jpeg__encode__types_8h_1a1fa2fd3dca6503f897f1ac83959dfbbca13dbc71493f0b0b3ae792674b5fee20b"></a> enumerator BK\_JPEG\_ENCODE\_IOCTL\_SET\_FLEXA\_LINES\_READY
    :   Software Flexa: arg is block count cast to void \*

    <a id="_CPPv4N26bk_jpeg_encode_ioctl_cmd_t36BK_JPEG_ENCODE_IOCTL_SET_FRAME_READYE"></a>

    <a id="_CPPv3N26bk_jpeg_encode_ioctl_cmd_t36BK_JPEG_ENCODE_IOCTL_SET_FRAME_READYE"></a> <a id="_CPPv2N26bk_jpeg_encode_ioctl_cmd_t36BK_JPEG_ENCODE_IOCTL_SET_FRAME_READYE"></a> <a id="bk__jpeg__encode__types_8h_1a1fa2fd3dca6503f897f1ac83959dfbbca53ce9dc2bf9e08a2932335194d2326cf"></a> enumerator BK\_JPEG\_ENCODE\_IOCTL\_SET\_FRAME\_READY
    :   Software Flexa: notify one frame input is ready

    <a id="_CPPv4N26bk_jpeg_encode_ioctl_cmd_t34BK_JPEG_ENCODE_IOCTL_REGISTER_BONDE"></a>

    <a id="_CPPv3N26bk_jpeg_encode_ioctl_cmd_t34BK_JPEG_ENCODE_IOCTL_REGISTER_BONDE"></a> <a id="_CPPv2N26bk_jpeg_encode_ioctl_cmd_t34BK_JPEG_ENCODE_IOCTL_REGISTER_BONDE"></a> <a id="bk__jpeg__encode__types_8h_1a1fa2fd3dca6503f897f1ac83959dfbbca9f9e1135a0f7bf825a10f1c5ca3e9142"></a> enumerator BK\_JPEG\_ENCODE\_IOCTL\_REGISTER\_BOND
    :   arg: bk\_flexa\_bond\_t \*

    <a id="_CPPv4N26bk_jpeg_encode_ioctl_cmd_t36BK_JPEG_ENCODE_IOCTL_UNREGISTER_BONDE"></a>

    <a id="_CPPv3N26bk_jpeg_encode_ioctl_cmd_t36BK_JPEG_ENCODE_IOCTL_UNREGISTER_BONDE"></a> <a id="_CPPv2N26bk_jpeg_encode_ioctl_cmd_t36BK_JPEG_ENCODE_IOCTL_UNREGISTER_BONDE"></a> <a id="bk__jpeg__encode__types_8h_1a1fa2fd3dca6503f897f1ac83959dfbbca7d1eda0a7cd4562282bc7b72403ca4dd"></a> enumerator BK\_JPEG\_ENCODE\_IOCTL\_UNREGISTER\_BOND
    :   arg: bk\_flexa\_bond\_t \*

    <a id="_CPPv4N26bk_jpeg_encode_ioctl_cmd_t32BK_JPEG_ENCODE_IOCTL_STOP_ENCODEE"></a>

    <a id="_CPPv3N26bk_jpeg_encode_ioctl_cmd_t32BK_JPEG_ENCODE_IOCTL_STOP_ENCODEE"></a> <a id="_CPPv2N26bk_jpeg_encode_ioctl_cmd_t32BK_JPEG_ENCODE_IOCTL_STOP_ENCODEE"></a> <a id="bk__jpeg__encode__types_8h_1a1fa2fd3dca6503f897f1ac83959dfbbca9ea189ee9b361eecc5ae5a88df667c36"></a> enumerator BK\_JPEG\_ENCODE\_IOCTL\_STOP\_ENCODE
    :   stop current Flexa encode

<a id="_CPPv427bk_jpeg_encode_flexa_mode_t"></a>

<a id="_CPPv327bk_jpeg_encode_flexa_mode_t"></a> <a id="_CPPv227bk_jpeg_encode_flexa_mode_t"></a> <a id="bk__jpeg__encode__types_8h_1a91c396e157af5a306755c3be95d5d083"></a> enum bk\_jpeg\_encode\_flexa\_mode\_t
:   *Values:*

    <a id="_CPPv4N27bk_jpeg_encode_flexa_mode_t30BK_JPEG_ENCODE_FLEXA_MODE_NONEE"></a>

    <a id="_CPPv3N27bk_jpeg_encode_flexa_mode_t30BK_JPEG_ENCODE_FLEXA_MODE_NONEE"></a> <a id="_CPPv2N27bk_jpeg_encode_flexa_mode_t30BK_JPEG_ENCODE_FLEXA_MODE_NONEE"></a> <a id="bk__jpeg__encode__types_8h_1a91c396e157af5a306755c3be95d5d083afc1ef6634b80c1039c371b289da04a14"></a> enumerator BK\_JPEG\_ENCODE\_FLEXA\_MODE\_NONE

    <a id="_CPPv4N27bk_jpeg_encode_flexa_mode_t34BK_JPEG_ENCODE_FLEXA_MODE_SOFTWAREE"></a>

    <a id="_CPPv3N27bk_jpeg_encode_flexa_mode_t34BK_JPEG_ENCODE_FLEXA_MODE_SOFTWAREE"></a> <a id="_CPPv2N27bk_jpeg_encode_flexa_mode_t34BK_JPEG_ENCODE_FLEXA_MODE_SOFTWAREE"></a> <a id="bk__jpeg__encode__types_8h_1a91c396e157af5a306755c3be95d5d083a66979bf467fd1d32080a5b57a777d4d9"></a> enumerator BK\_JPEG\_ENCODE\_FLEXA\_MODE\_SOFTWARE

    <a id="_CPPv4N27bk_jpeg_encode_flexa_mode_t34BK_JPEG_ENCODE_FLEXA_MODE_HARDWAREE"></a>

    <a id="_CPPv3N27bk_jpeg_encode_flexa_mode_t34BK_JPEG_ENCODE_FLEXA_MODE_HARDWAREE"></a> <a id="_CPPv2N27bk_jpeg_encode_flexa_mode_t34BK_JPEG_ENCODE_FLEXA_MODE_HARDWAREE"></a> <a id="bk__jpeg__encode__types_8h_1a91c396e157af5a306755c3be95d5d083a789271709033f4f2480b1e0799838b36"></a> enumerator BK\_JPEG\_ENCODE\_FLEXA\_MODE\_HARDWARE
