---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/video_codec/h264_decoding_sw.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="h264"></a>

# H264软解码

<a id="id1"></a>

## 1、H264解码

> H264解码部分在手机端实现，本文使用ffmpeg库进行解码。

<a id="ffmpeg"></a>

## 2、ffmpeg官网地址

> <https://ffmpeg.org/>

<a id="id2"></a>

## 3、解码流程图

<a id="id4"></a>
![fill specific color](../../../../../_assets/8ddf3ff7a309aab83d0b-ffmpeg_h264_decode_flow.png)


Figure 1\. decode\_flow

<a id="id3"></a>

## 4、流程说明

1. 注册解码器: `avcodec_register_all`

   用于注册所有已编译的编解码器
2. 查找解码器: `avcodec_find_decoder`

   根据指定的解码器ID查找对应的解码器,h264解码器对应ID为：AV\_CODEC\_ID\_H264
3. 初始化解析器: `av_parser_init`

   初始化解析器上下文。解析器在处理数据流之前，可以用于预处理输入数据，例如找到帧边界、提取关键信息等。
4. 分配解码器上下文: `avcodec_alloc_context3`

   分配一个 AVCodecContext 结构体，并设置默认值。AVCodecContext 结构体是 FFmpeg 中用于存储编解码器的上下文信息的数据结构。
5. 打开解码器: `avcodec_open2`

   打开编解码器并初始化其上下文（AVCodecContext）。在解码器上下文初始化之后，通过这个函数可以打开解码器，以便开始进行解码操作。
6. 接收数据

   每次开始解码之前，先判断数据是否以sps帧开始，直到查找到sps开始的数据，才开始进行解码，否则丢弃数据，不进行解码。
7. 发送数据给解析器: `av_parser_parse2`

   解析输入的媒体数据流，通常用于找到帧的边界
8. 发送数据给解码器: `avcodec_send_packet`

   用于向解码器发送数据包以进行解码。它将输入的数据包发送到解码器上下文进行解码。
9. 接收解码以后的数据帧: `avcodec_receive_frame`

   用于从解码器接收解码后的帧。在使用 `avcodec_send_packet` 函数发送数据包进行解码后，可以使用 `avcodec_receive_frame` 来获取解码器解码出的图像帧。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [软件架构与分层](../architecture.md)
- [系统安全](../security.md)
- [低功耗与电源管理](../power_save.md)
- [设备管理框架](../driver_model.md)
- [外设与驱动](../peripheral.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [Bootloader与Ota](../bootloader_ota.md)
- [BK AT](../at.md)
- [多媒体](../multimedia.md)
- [显示](../display.md)
- [视频编解码](../video_codec.md)
- [JPEG解码](jpeg_decoding.md)
- [JPEG硬解码](jpeg_decoding_hw.md)
- [JPEG软解码](jpeg_decoding_sw.md)
- [JPEG硬编码](jpeg_encoding_hw.md)
- [JPEG软编码](jpeg_encoding_sw.md)
- [H264硬编码](h264_encoding_hw.md)
- [VIDEO_PIPELINE](video_pipeline.md)
- [音频](../audio.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [摄像头](../camera.md)
- [图像用户界面](../gui.md)
- [多媒体网络传输](../multimedia_network_transfer.md)
- [OS 相关参考](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
