---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/camera/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 摄像头

<a id="id2"></a>

## 概述

BK7259 多媒体方案支持三类摄像头输入接口，均通过统一的 `bk_camera` 框架管理：

| 接口类型 | 典型应用场景 | 示例工程 |
| --- | --- | --- |
| MIPI CSI | 高分辨率 Sensor \+ ISP 图像处理 | `isp_example` |
| DVP (并行) | 低成本 Sensor，直连 JPEG/H264 硬件编码 | `isp_example` / 方案工程 |
| UVC (USB) | 外接 USB 摄像头，即插即用 | `uvc_example` / `uvc_display_example` |

**相关 API 与示例：**

- [Camera API](../api-reference/multimedia/bk_camera.md)
- [图像内存管理](../api-reference/multimedia/bk_frame_buffer.md)

- [ISP 图像信号处理](camera/isp.md)
- [MIPI CSI 摄像头](camera/mipi_csi.md)
- [DVP 摄像头](camera/dvp.md)
- [UVC 摄像头](camera/uvc.md)

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
- [VPU](vpu.md)
- [GPU](gpu.md)
- [NPU](npu.md)
- [音频](audio.md)
- [用例编写](examples.md)
- [文档系统](documentation.md)
- [ISP 图像信号处理](camera/isp.md)
- [MIPI CSI 摄像头](camera/mipi_csi.md)
- [DVP 摄像头](camera/dvp.md)
- [UVC 摄像头](camera/uvc.md)
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
