---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/video_codec/jpeg_encoding_hw.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="jpeg"></a>

# JPEG硬件编码

<a id="id1"></a>

## 1、功能概述

> JPEG编码主要用于将YUV422的数据通过硬件编码，输出JPEG图像数据，并且压缩图像数据量。当前JPEG功能主要用在DVP摄像头，DVP摄像头输出YUV422数据给芯片，芯片压缩成JPEG图像。也支持将外部YUV422数据，压缩成JPEG图像。由于BK7258有一个专门处理YUV数据的模块YUV\_BUF，JPEG模块也需要依赖它。另外也支持非DVP摄像头数据，压缩成JPEG图像。

<a id="id2"></a>

## 2、开发资料

> 当前avdk提供了两套编码接口，一套是YUV数据来源于DVP摄像头，另一套是YUV数据来源于外部传感器。分别参考文件路径： ``` ./ap/include/components/bk_camera_ctlr.h``和 ``./ap/include/components/bk_jpeg_encode_ctlr.h ```。
>
> 参考使用示例： `./projects/dvp_example/README_CN.md` 和 `./projects/encoder_example/README_CN.md`。

<a id="id3"></a>

## 3、接口说明

> 1. DVP摄像头控制器接口：
>    :   bk\_camera\_dvp\_ctlr\_new：创建DVP摄像头控制器
>        bk\_camera\_open：打开DVP摄像头控制器
>        bk\_camera\_close：关闭DVP摄像头控制器
>        bk\_camera\_delete：删除DVP摄像头控制器
>        bk\_camera\_ioctl：DVP摄像头控制器IO控制
> 2. JPEG编码控制器接口：
>    :   bk\_jpeg\_encode\_ctlr\_new：创建JPEG编码控制器
>        bk\_jpeg\_encode\_open：打开JPEG编码控制器
>        bk\_jpeg\_encode\_close：关闭JPEG编码控制器
>        bk\_jpeg\_encode\_delete：删除JPEG编码控制器
>        bk\_jpeg\_encode\_ioctl：JPEG编码控制器IO控制
> 3. 调整压缩率的接口：
>
>    > bk\_jpeg\_enc\_encode\_config：设置JPEG编码配置
>    > bk\_jpeg\_enc\_get\_encode\_config：获取JPEG编码配置

<a id="id4"></a>

## 4、驱动代码

DVP摄像头驱动代码路径： `./ap/components/bk_dvp`.

JPEG编码驱动代码路径： `./ap/middleware/driver/jpeg_enc`.

YUV\_BUF驱动代码路径： `./ap/middleware/driver/yuv_buf`.

<a id="id5"></a>

## 5、注意事项

1. 在编码过程中，当输出一帧图像的大小超过up\_size，会进一步压缩，使得数据量不超过up\_size且不小于low\_size。
2. 在编码过程中，当输出一帧图像的大小小于low\_size，会进一步压缩，使得数据量不超过up\_size且不小于low\_size。
3. 不同的分辨率配置的默认输出图像范围是不一样的，比如640X480，默认是范围是20KB到35KB。
4. 如果需要调整压缩率，建议先通过接口获取默认的压缩率，然后根据实际需求进行调整。
5. 虽然默认可以配置一些边界值，比如最大值为65535KB，但是不建议使用，因为可能会导致图像质量下降。建议一般配置压缩率为20倍左右。比如640X480，原始YUV图像为600KB，压缩率为20倍，则输出图像为30KB。
