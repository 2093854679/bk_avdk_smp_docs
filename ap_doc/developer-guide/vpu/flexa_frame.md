# Frame 与 Flexa 模式



## 1. 概述

BK7259 VPU 的 H.264 / JPEG 编解码均提供两种工作模式：


- **Frame 模式（整帧模式）**：以完整一帧图像/码流为处理单元，输入就绪后一次性送入硬件，整帧处理完成后再交付上层。

- **Flexa 模式（分段低延迟模式）**：以 **16 像素行（1 个宏块行，MB row）** 为最小分段单位，按段写入环形缓冲区；下游模块可在整帧尚未完成时即开始消费，从而降低端到端延迟并减少 PSRAM 整帧搬运。

两种模式对应不同的控制器创建接口（`*_frame_*` vs `*_flexa_*` / `*_hw_flexa_*` / `*_sw_flexa_*`），**不能混用**。


## 2. 工作原理


### 2.1 Frame 模式


```
[完整输入] ──► VPU 编/解码 ──► [完整输出缓冲区]
                  │
                  └── 整帧完成后回调 frame_done_cb

```

特点：


- 输入、输出均为整帧缓冲区（如 1080x1920 NV12 约 3.1 MB）。

- 调用 `decode_frame` / `encode` 后，通常阻塞或等待 `frame_done_cb` 才表示本帧结束。

- 实现简单，适合单步调试、离线文件处理、抓图/存文件等场景。

- 高分辨率下整帧读写 PSRAM 带宽开销大，实时预览/播放容易成为瓶颈。


### 2.2 Flexa 模式


```
[码流/输入] ──► VPU ──► 分段环形缓冲（HSRAM，segment 为单位）
                          │
                          ├── flexa_done_cb（每写出一段触发）
                          └── frame_done_cb（整帧结束）
                          │
                          ▼
                下游通过 Bond 按段读取（GPU / H264E / DPU …）

```

特点：


- 使用 **环形分段缓冲** 而非整帧落地。环高（像素行数）= `16 × segment_height × segment_number`。
  `segment_height` 单位为宏块行数（MB row），`segment_number` 为环中分段个数。
  典型配置 `segment_height=1, segment_number=2` → 环高 32 行，仅数十 KB 级 HSRAM。

- 每写出一段触发 `flexa_done_cb`；整帧完成仍触发 `frame_done_cb`。

- 通过 **Flexa Bond**（``bk_flexa_bond_*``）将 VPU 输出流与 GPU、H264E、ISP 等输入流绑核，实现 **流水线并行**。

- 参考 `h264d_gpu_display_example`：H.264 解码仅写 16 行 NV12 分段到 HSRAM，GPU 经 Bond 按段读取并合成压缩 ARGB，避免整帧 NV12 落 PSRAM，显著提升播放帧率。


## 3. 模式对比

| 对比项 | Frame 模式 | Flexa 模式 |
| --- | --- | --- |
| 处理粒度 | 整帧 | 16 行（MB row）分段 |
| 典型缓冲 | 整帧 PSRAM/PSRAM slab | HSRAM 环形分段缓冲 |
| 端到端延迟 | 较高（须等整帧完成） | 较低（下游可提前消费） |
| 内存/带宽 | 整帧读写，高分辨率开销大 | 分段小缓冲，适合实时流水线 |
| 下游对接 | 应用自行取整帧缓冲 | 需 Bond 或手动维护读指针（`PORT_SET_RD_PTR`） |
| 回调 | `frame_done_cb` | `flexa_done_cb` and `frame_done_cb` |
| 典型场景 | 自检、存文件、单帧抓拍 | 实时预览、视频播放、Camera→编码/显示链路 |


## 4. Flexa 编码子类型（仅编码侧）

H.264 / JPEG **编码** 的 Flexa 还分为：

| 类型 | 说明 |
| --- | --- |
| 硬件 Flexa | `bk_*_encode_hw_flexa_new`；ISP/Camera 经 SBI 流（`FLEXA_STREAM_ID_Y/CB/CR`）向编码器送数据 |
| 软件 Flexa | `bk_*_encode_sw_flexa_new`；IOCTL `SET_FLEXA_LINES_READY` / `SET_FRAME_READY` 通知行就绪 |

解码侧仅有一种 Flexa 控制器（`*_flexa_ctlr_new`），分段输出由硬件写入环缓，由 Bond 或回调通知下游。


## 5. Flexa Bond

Bond 用于在两个 Flexa 端口之间同步读写指针，避免应用层手工拷贝整帧。


- 类型定义：`ap/components/media_service/include/bk_flexa_bond_types.h`

- 支持的绑核类型（`bk_flexa_bond_kind_t`）：`H264D`、`GPU`、`H264E`、`ISP`、`MJPEGD`、`MJPEGE`

- 注册方式：`BK_*_DECODE_IOCTL_REGISTER_BOND` / `BK_*_ENCODE_IOCTL_REGISTER_BOND`

- 示例：``` bk_flexa_h264d_gpu_bond_start()``（``h264d_gpu_display_demo.c ```）、``` bk_flexa_mjpegd_gpu_bond_start()``（``uvc_display_example ```）


## 6. API 与示例对照

| 能力 | Frame 创建接口 | Flexa 创建接口 | 示例 CLI |
| --- | --- | --- | --- |
| H.264 解码 | `bk_h264_decode_frame_ctlr_new` | `bk_h264_decode_flexa_ctlr_new` | `h264d_gpu_display start` （Flexa+GPU） |
| H.264 编码 | `bk_h264_encode_frame_new` | `bk_h264_encode_hw/sw_flexa_new` | `h264_encode vcenc_h264e` / `vcenc_h264e_flexa` |
| JPEG 解码 | `bk_jpeg_decode_frame_ctlr_new` | `bk_jpeg_decode_flexa_ctlr_new` | `jpeg_decode vcdec_jpegd` / `vcdec_jpegd_flexa`； `uvc_display_example` `pipeline open` |
| JPEG 编码 | `bk_jpeg_encode_frame_new` | `bk_jpeg_encode_hw/sw_flexa_new` | `jpeg_encode frame` （Frame） |

配置宏：解码使用 `DEFAULT_H264_DECODE_FRAME_CONFIG` / `DEFAULT_H264_DECODE_FLEXA_CONFIG`、
`DEFAULT_JPEG_DECODE_FRAME_CONFIG` / `DEFAULT_JPEG_DECODE_FLEXA_CONFIG`。
Flexa 配置比 Frame 多出 `segment_height`、`segment_number` 及 `flexa_done_cb`。

备注

H.264 **解码** 除上表的 Frame / Flexa 外，还提供第三种整帧控制器

``` bk_h264_decode_frame_zerocopy_ctlr_new``（Frame 零拷贝整帧模式）：它是唯一能解码含 B 帧
（Main Profile IBBP）码流的控制器，复用 Frame 配置，并通过 ``DEQUEUE ``` / `RELEASE` /
`FLUSH` IOCTL 按 POC 顺序交付重排后的帧。详见 [H.264 解码](h264_decode.md "h264_decode.md")。


## 7. 选型建议


- **优先 Frame**：功能验证、单元测试、对延迟不敏感的一次性编解码、上层已有完整帧缓冲。

- **优先 Flexa**：Camera/ISP 实时预览、H.264 硬解 + GPU/DPU 显示、编码器与采集流水线绑核、1080p 及以上实时场景。

- Flexa 需额外规划：环缓大小（`segment_height` × `segment_number`）、Bond 对象生命周期、`flexa_done_cb` 与下游读指针同步；调试可从对应 example 的 Frame CLI 入手，确认功能后再切 Flexa 流水线。
