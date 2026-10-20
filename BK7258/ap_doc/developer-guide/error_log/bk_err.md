---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/error_log/bk_err.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 出错处理

及时发现与检测程序的错误是一个强健应用程序的基本要求。本节主要讲述 SDK API 错误码定义以及应用程序检测错误码方式。

<a id="id2"></a>

## 错误码定义

目前 SDK 中大多数 API 返回 bk\_err\_t 类型错误码，新增 API 将全部使用 bk\_err\_t 作为返回值（返回 void 除外）。

SDK 中错误码可分下面几类:

> - BK\_OK 表示成功，没有错误， 值为 0
> - 通用错误码，如 BK\_ERR\_NO\_MEM 表示内存不够，定义在 bk\_err.h 中
> - 模块错误码，使用 BK\_ERR\_MOD\_xxx 形式定义， 其中 MOD 产生该错误码的模块， 如 BK\_ERR\_WIFI\_STA\_NOT\_CONFIG 表示由 WiFi 产生的一个具体错误码

SDK 错误码两个特点:

> - 一般使用负数表示出错
> - 错误码在 SDK 全局唯一， 每个模块在 bk\_err.h 中定义一个错误码基地址，然后在 API 头文件中定义本模块特有的错误码

备注

第三方代码提供的 API 返回值不是 bk\_err\_t， 如 socket API 等。

<a id="id3"></a>

## 错误码返回

为了使应用程序尽可能精确的定义问题出错点，SDK API 返回错误码时会尽量精确。

一方面将同类别，但出错点不同的错误使用不同的错误码区分，另一方面，尽可能将底层具体错误返回到 API.

备注

在 SDK API 注释中，常常会看到错误码为 others 情形，这表示 API 所调用的底层代码或者其他模块函数所返回。

<a id="id4"></a>

## 出错检测宏

应用程序在使用 SDK API 时，建议使用 SDK 提供宏进行出错检测。

<a id="bk-log-on-err"></a>

### BK\_LOG\_ON\_ERR

当 API 返回不为 BK\_OK 时打出调用函数名称，行号及错误码，但不会从 API 调用函数返回。

<a id="bk-return-on-err"></a>

### BK\_RETURN\_ON\_ERR

当 API 返回不为 BK\_OK 时， 立即从 API 调用函数返回， 返回值为 API 返回的错误码。

<a id="bk-abort-on-err"></a>

### BK\_ABORT\_ON\_ERR

当 API 返回不为 BK\_OK 时， 调用 bk\_reboot() 重起系统。

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
- [系统日志](bk_log.md)
- [系统调试](../debug_trace.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [Bootloader与Ota](../bootloader_ota.md)
- [BK AT](../at.md)
- [多媒体](../multimedia.md)
- [显示](../display.md)
- [视频编解码](../video_codec.md)
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
