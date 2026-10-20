---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/vpu/h264_decode.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="h-264"></a>

# H.264 解码

<a id="id1"></a>

## 1\. 概述

H.264 硬件解码基于 VCDec IP，通过 `bk_h264_decode_*` 控制器将 H.264 码流解码为 NV12/YUV 等像素格式，可与 GPU、DPU 显示链路配合。

- 头文件：`ap/include/components/bk_decode/bk_h264_decode_ctlr.h`
- 示例工程：`projects/multimedia/h264d_gpu_display_example`

<a id="id2"></a>

## 2\. 支持能力

- Baseline / Main Profile H.264 码流解码
- Frame 整帧模式（`bk_h264_decode_frame_ctlr_new`）
- Frame 零拷贝整帧模式（`bk_h264_decode_frame_zerocopy_ctlr_new`）
- Flexa 分段低延迟模式（`bk_h264_decode_flexa_ctlr_new`）
- 输出格式可配置（默认 NV12）
- 支持通过 IOCTL 与 GPU / H264E 端口绑核（bond）

备注

仅 **Frame 零拷贝整帧模式** 支持含 B 帧（Main Profile IBBP）的码流；Frame 整帧模式与
Flexa 模式为非 B 控制器，只能解码不含 B 帧的码流（如 1 IDR \+ P 帧）。Frame 零拷贝整帧
模式的使用方法见下文 [6\. Frame 零拷贝整帧模式](#frame-zerocopy-mode)。

参见

Frame 与 Flexa 模式的工作原理、对比及选型，请参阅 [Frame 与 Flexa 模式](flexa_frame.md)。

<a id="id3"></a>

## 3\. 相关宏定义

| 宏名称 | 说明 |
| --- | --- |
| CONFIG\_BK\_DECODER | 使能 VCDec 解码子系统 |
| CONFIG\_BK\_DECODER\_TASK\_PRIO | 解码任务优先级 |
| CONFIG\_BK\_DECODER\_TASK\_SIZE | 解码任务栈大小 |

<a id="id4"></a>

## 4\. 调试说明

<a id="id5"></a>

### 4.1 编译与烧录

```
cd <SDK_ROOT>
make bk7259 PROJECT=multimedia/h264d_gpu_display_example -j$(nproc)
```

<a id="cli"></a>

### 4.2 CLI 命令

```
h264d_gpu_display help
h264d_gpu_display start [loops]
h264d_gpu_display stop
h264d_gpu_display isp_open
h264d_gpu_display isp_close
```

- `start [loops]`：启动 H.264 解码 \+ GPU 显示；`loops=0` 持续循环
- 成功标志：`[RESULT][PASS] decoded_frames=...`
- 使能 `CONFIG_BK_DECODER` 时上电自动运行一次 boot demo

<a id="id6"></a>

### 4.3 常见问题

| 现象 | 排查建议 |
| --- | --- |
| 解码失败 | 确认 `CONFIG_BK_DECODER` 已开启；检查码流是否含 SPS/PPS |
| 输出尺寸不对 | 检查 `out_width/out_height` 与码流分辨率匹配 |
| GPU 显示花屏 | 确认输出格式为 NV12；宽高偶数对齐 |

<a id="id7"></a>

## 5\. 使用流程

参考 `h264d_gpu_display_demo.c`：

```
bk_h264_decode_ctlr_handle_t decoder = NULL;
bk_h264_decode_flexa_config_t dec_cfg = DEFAULT_H264_DECODE_FLEXA_CONFIG;
dec_cfg.out_width = 720;
dec_cfg.out_height = 1280;
dec_cfg.out_format = BK_PIXEL_FORMAT_NV12;

bk_h264_decode_flexa_ctlr_new(&decoder, &dec_cfg);
bk_h264_decode_init(decoder);
bk_h264_decode_open(decoder);

bk_h264_decode_input_t input = {
    .stream = h264_data,
    .stream_len = h264_len,
    .out_buffer = yuv_buf,
    .out_buffer_size = yuv_size,
};
bk_h264_decode_frame(decoder, &input);

bk_h264_decode_info_t info;
bk_h264_decode_get_info(decoder, &info);

bk_h264_decode_close(decoder);
bk_h264_decode_deinit(decoder);
bk_h264_decode_delete(decoder);
```

Frame 模式将 `bk_h264_decode_flexa_ctlr_new` 替换为 `bk_h264_decode_frame_ctlr_new`，配置使用 `DEFAULT_H264_DECODE_FRAME_CONFIG`。

<a id="frame"></a>

<a id="frame-zerocopy-mode"></a>

## 6\. Frame 零拷贝整帧模式

Frame 整帧模式与 Flexa 模式均为 **非 B** 控制器；要解码含 B 帧的 Main Profile（IBBP）码流，
必须使用 Frame 零拷贝整帧模式控制器 `bk_h264_decode_frame_zerocopy_ctlr_new`。

该控制器内部维护一个零拷贝帧池：同一块物理缓冲同时充当 **解码目标 / DPB 参考 / 显示输出**，
省去参考帧备份（reference backup）与输出拷贝，并支持按 **POC（picture order count）** 做
B 帧显示重排。

与 Frame 模式的差异：

- 创建接口为 `bk_h264_decode_frame_zerocopy_ctlr_new`，使用 **专用** 配置结构体
  `bk_h264_decode_frame_zerocopy_config_t` / `DEFAULT_H264_DECODE_FRAME_ZEROCOPY_CONFIG`
  （与 Frame 整帧模式的 `bk_h264_decode_frame_config_t` 相互解耦）；其中 `disp_depth`
  表示应用层在编解码 DPB 之外可同时持有的额外显示 slot 数，取值 1..4，`0` 表示取控制器
  默认值（2）。
- `bk_h264_decode_frame()` 仍是每次送入 **一个 access unit**，但 `bk_h264_decode_input_t`
  的 `out_buffer` / `out_buffer_size` 被忽略（解码结果不再拷贝到应用缓冲）。
- 解码帧按 **显示（POC）顺序** 通过 `BK_H264_DECODE_IOCTL_DEQUEUE` 取出；用完后必须且仅需
  通过 `BK_H264_DECODE_IOCTL_RELEASE` 归还 **一次**。
- 码流结束（EOS）时用 `BK_H264_DECODE_IOCTL_FLUSH` 冲刷出尾部因重排而滞留的图像。
- B 帧重排在内部完成，顺序 dequeue 得到的就是正确的播放顺序。

```
bk_h264_decode_ctlr_handle_t decoder = NULL;
bk_h264_decode_frame_zerocopy_config_t dec_cfg = DEFAULT_H264_DECODE_FRAME_ZEROCOPY_CONFIG;
dec_cfg.out_width = 1280;
dec_cfg.out_height = 720;
dec_cfg.out_format = BK_PIXEL_FORMAT_NV12;
dec_cfg.disp_depth = 0; /* 0 = 使用默认值 2 */

bk_h264_decode_frame_zerocopy_ctlr_new(&decoder, &dec_cfg);
bk_h264_decode_init(decoder);
bk_h264_decode_open(decoder);

/* 送入一个 AU（out_buffer 被忽略） */
bk_h264_decode_input_t input = {
    .stream = au_data,
    .stream_len = au_len,
};
bk_h264_decode_frame(decoder, &input);

/* 按显示顺序取帧 */
bk_h264_decode_dequeue_t deq = { .timeout_ms = 100 };
while (bk_h264_decode_ioctl(decoder, BK_H264_DECODE_IOCTL_DEQUEUE, &deq) == BK_OK) {
    /* 使用 deq.frame.data / width / height / poc ... */
    bk_h264_decode_ioctl(decoder, BK_H264_DECODE_IOCTL_RELEASE, &deq.frame);
}

/* EOS：冲刷尾部重排帧后再取一次 */
bk_h264_decode_ioctl(decoder, BK_H264_DECODE_IOCTL_FLUSH, NULL);

bk_h264_decode_close(decoder);
bk_h264_decode_deinit(decoder);
bk_h264_decode_delete(decoder);
```

示例工程 `projects/multimedia/h264_decode_example` 的 `vcdec_h264d_frame_zerocopy` 用例
演示了该控制器解码 B 帧码流（`1280x720_ibbp`）的完整流程。
