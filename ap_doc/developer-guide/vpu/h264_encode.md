# H.264 编码



## 1. 概述

H.264 硬件编码基于 VCENC IP，通过 `bk_h264_encode_*` 控制器将 NV12/YUV 输入编码为 H.264 码流。


- 头文件：`ap/include/components/bk_encode/bk_h264_encode_ctlr.h`

- 示例工程：`projects/multimedia/h264_encode_example`


## 2. 支持能力


- H.264 硬件编码（VCENC 后端）

- Frame 整帧模式（`bk_h264_encode_frame_new`）

- 硬件 / 软件 Flexa 低延迟模式

- GOP 与码率控制配置

- 强制 IDR：`bk_h264_encode_force_idr()`

参见

Frame 与 Flexa 模式说明见 [Frame 与 Flexa 模式](flexa_frame.md "flexa_frame.md")。CLI `vcenc_h264e` 为 Frame，`vcenc_h264e_flexa` 为软件 Flexa。


## 3. 相关宏定义

| 宏名称 | 说明 |
| --- | --- |
| CONFIG_BK_ENCODER | 使能 VCENC 编码子系统 |
| CONFIG_BK_ENCODER_H264_TASK_SIZE | H.264 编码任务栈大小 |
| CONFIG_BK_ENCODER_H264_MAX_OUTPUT_BUFFER | 最大输出缓冲区（字节） |
| CONFIG_ENCODER_H264_CLK_240M | 使用 240MHz H.264 编码时钟 |


## 4. 调试说明


### 4.1 编译与烧录


```
cd <SDK_ROOT>
make bk7259 PROJECT=multimedia/h264_encode_example -j$(nproc)

```


### 4.2 CLI 命令


```
h264_encode help
h264_encode vcenc_h264e
h264_encode vcenc_h264e_flexa

```


- `vcenc_h264e`：整帧模式，256×128 NV12 输入，编码 30 帧，GOP=15

- `vcenc_h264e_flexa`：软件 Flexa 模式

- 成功标志：`[RESULT][PASS] ...`

- 使能 `CONFIG_BK_ENCODER` 时上电自动运行编码自检


### 4.3 码率与画质调节

通过 `bk_h264_encode_set_rate_ctrl()` 配置码率控制：


```
bk_h264_encode_rate_ctrl_t rc = {
    .bitrate = 2000000,   // 非零：码率模式；0：固定 QP 模式
    .qp_min_i = 20, .qp_max_i = 40,
    .qp_min_p = 22, .qp_max_p = 42,
};
bk_h264_encode_set_rate_ctrl(encoder, &rc);

```


## 5. 使用流程


```
bk_h264_encode_ctlr_handle_t encoder = NULL;
bk_h264_encode_frame_config_t cfg = {0};
cfg.width = 256;
cfg.height = 128;
cfg.gop_frame_count = 15;
cfg.input_format = BK_PIXEL_FORMAT_NV12;
cfg.outbuf_malloc = h264_outbuf_malloc;
cfg.outbuf_complete = h264_outbuf_complete;

bk_h264_encode_frame_new(&encoder, &cfg);
bk_h264_encode_init(encoder);
bk_h264_encode_open(encoder);
bk_h264_encode_start(encoder);

bk_h264_encode_force_idr(encoder);          // 可选
bk_h264_encode_set_gop_frame_count(encoder, 15);

bk_h264_encode_close(encoder);
bk_h264_encode_deinit(encoder);
bk_h264_encode_delete(encoder);

```

Flexa 硬件路径：`bk_h264_encode_hw_flexa_new()`；软件 Flexa：`bk_h264_encode_sw_flexa_new()`。
