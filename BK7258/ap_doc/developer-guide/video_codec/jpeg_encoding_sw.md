---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/video_codec/jpeg_encoding_sw.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="jpeg"></a>

# JPEG软编码

<a id="id1"></a>

## 1、JPEG软编码流程

JPEG软编码主要流程如下：

1. 输入数据格式转换(该步骤可选，输入格式必须为YVYU422，如果不是该格式需要进行格式转换)；
2. 初始化/申请压缩数据buffer/图像输出buffer；
3. 填充编码头部信息；
4. 以16x8像素的block为单位进行DCT/量化/哈夫曼编码，压缩后的数据填入图像输出buffer；
5. 重复4，直至出现异常或编码结束；

<a id="id5"></a>
![jpeg_encode sw](../../../../../_assets/7e56286df799b65306e7-jpeg_encode_sw.png)


Figure 1\. jpeg soft encode process

<a id="id2"></a>

## 2、内存需求

JPEG软编码对线程依赖在3K以内，主要需要的buffer及用途如下：

1. 一块512bytes的内部buffer，用于存储16x8 block压缩数据；
2. 一块64k大小的图像输出buffer（该大小可根据需要调整使用malloc动态分配），用于输出压缩后的图像；

<a id="id3"></a>

## 3、JPEG软编码模块使用

1. 调用 jpeg\_sw\_encoder\_init ，初始化软编码模块,注册相关回调函数如：open/enc/deinit；
2. 调用 jpeg\_sw\_encoder.open ，完成软编码器内部参数初始化/内存申请；
3. 调用 jpeg\_sw\_encoder.enc ，执行软编码操作；
4. 调用 jpeg\_sw\_encoder.deinit ，关闭软编码模块，释放内部申请buffer；

函数参数请查看 [API Reference :](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multi_media/bk_jpegenc_sw.html)

<a id="id4"></a>

## 4、JPEG软编码例程

请参考 jpeg\_sw\_enc\_test.c

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
- [H264软解码](h264_decoding_sw.md)
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
