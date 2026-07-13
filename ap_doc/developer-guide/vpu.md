# VPU 视频处理单元



## 概述

BK7259 内置 VeriSilicon VPU（Video Processing Unit），通过 `bk_decoder` / `bk_encoder` 组件对外提供硬件 H.264 / JPEG 编解码能力。应用层统一使用 `bk_h264_*` / `bk_jpeg_*` 控制器 API。

| 能力 | 控制器 API | 示例工程 |
| --- | --- | --- |
| H.264 硬件解码 | `bk_h264_decode_*` | `multimedia/h264d_gpu_display_example` |
| H.264 硬件编码 | `bk_h264_encode_*` | `multimedia/h264_encode_example` |
| JPEG 硬件解码 | `bk_jpeg_decode_*` | `multimedia/jpeg_decode_example` |
| JPEG 硬件编码 | `bk_jpeg_encode_*` | `multimedia/jpeg_encode_example` |

组件路径：


- 解码器：`ap/components/bk_vpu/bk_decoder/`

- 编码器：`ap/components/bk_vpu/bk_encoder/`

- 头文件：`ap/include/components/bk_decode/`、`ap/include/components/bk_encode/`

通用使能宏：


- `CONFIG_BK_DECODER`：使能 VCDec 解码子系统（H.264 / JPEG 解码）

- `CONFIG_BK_ENCODER`：使能 VCENC 编码子系统（H.264 / JPEG 编码）

备注

VPU 编解码均支持 **Frame 整帧模式** 和 **Flexa 低延迟分段模式**。两种模式在数据处理粒度、缓冲布局、延迟和下游对接方式上差异明显，请参阅 [Frame 与 Flexa 模式](vpu/flexa_frame.md "flexa_frame.md")。


- [Frame 与 Flexa 模式](vpu/flexa_frame.md "flexa_frame.md")

- [H.264 解码](vpu/h264_decode.md "h264_decode.md")

- [H.264 编码](vpu/h264_encode.md "h264_encode.md")

- [JPEG 解码](vpu/jpeg_decode.md "jpeg_decode.md")

- [JPEG 编码](vpu/jpeg_encode.md "jpeg_encode.md")
