# 摄像头



## 概述

BK7259 多媒体方案支持三类摄像头输入接口，均通过统一的 `bk_camera` 框架管理：

| 接口类型 | 典型应用场景 | 示例工程 |
| --- | --- | --- |
| MIPI CSI | 高分辨率 Sensor + ISP 图像处理 | `isp_example` |
| DVP (并行) | 低成本 Sensor，直连 JPEG/H264 硬件编码 | `isp_example` / 方案工程 |
| UVC (USB) | 外接 USB 摄像头，即插即用 | `uvc_example` / `uvc_display_example` |


**相关 API 与示例：**


- [Camera API](camera/../../api-reference/multimedia/bk_camera.md "../../api-reference/multimedia/bk_camera.md")

- [图像内存管理](camera/../../api-reference/multimedia/bk_frame_buffer.md "../../api-reference/multimedia/bk_frame_buffer.md")


- [ISP 图像信号处理](camera/isp.md "isp.md")

- [MIPI CSI 摄像头](camera/mipi_csi.md "mipi_csi.md")

- [DVP 摄像头](camera/dvp.md "dvp.md")

- [UVC 摄像头](camera/uvc.md "uvc.md")
