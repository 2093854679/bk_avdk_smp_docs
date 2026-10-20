---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/vpu/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="vpu"></a>

# VPU 视频处理单元

<a id="id1"></a>

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

VPU 编解码均支持 **Frame 整帧模式** 和 **Flexa 低延迟分段模式**。两种模式在数据处理粒度、缓冲布局、延迟和下游对接方式上差异明显，请参阅 [Frame 与 Flexa 模式](vpu/flexa_frame.md)。

- [Frame 与 Flexa 模式](vpu/flexa_frame.md)
- [H.264 解码](vpu/h264_decode.md)
- [H.264 编码](vpu/h264_encode.md)
- [JPEG 解码](vpu/jpeg_decode.md)
- [JPEG 编码](vpu/jpeg_encode.md)

## 模块导航

- [简介](../introduction.md)
- [H/W 参考手册](../hw-reference.md)
- [API 参考手册](../api-reference.md)
- [开发者指南](../developer-guide.md)
- [软件架构与分层](architecture.md)
- [系统安全](security.md)
- [低功耗与电源管理](power_save.md)
- [设备管理框架](driver_model.md)
- [外设与驱动](peripheral.md)
- [出错与日志](error_log.md)
- [系统调试](debug_trace.md)
- [CPU Hotplug](cpu_hotplug.md)
- [Wi-Fi](wifi.md)
- [Bluetooth](bluetooth.md)
- [HTTP](http.md)
- [Bootloader与Ota](bootloader_ota.md)
- [BK AT](at.md)
- [多媒体](multimedia.md)
- [显示](display.md)
- [Frame 与 Flexa 模式](vpu/flexa_frame.md)
- [H.264 解码](vpu/h264_decode.md)
- [H.264 编码](vpu/h264_encode.md)
- [JPEG 解码](vpu/jpeg_decode.md)
- [JPEG 编码](vpu/jpeg_encode.md)
- [GPU](gpu.md)
- [NPU](npu.md)
- [音频](audio.md)
- [用例编写](examples.md)
- [文档系统](documentation.md)
- [摄像头](camera.md)
- [图像用户界面](gui.md)
- [多媒体网络传输](multimedia_network_transfer.md)
- [操作系统与内存管理](../os.md)
- [样例演示](../examples.md)
- [项目示例](../examples/projects.md)
- [应用开发](../application.md)
- [开发与贡献代码流程](../process.md)
- [云平台](../cloud.md)
- [常见问题](../FAQ.md)
- [支持的外设](../support_peripherals.md)
