# JPEG 编码



## 1. 概述

JPEG 硬件编码基于 VCENC JPEG 通路，通过 `bk_jpeg_encode_*` 控制器将 NV12 图像编码为 JPEG 码流。


- 头文件：`ap/include/components/bk_encode/bk_jpeg_encode_ctlr.h`

- 示例工程：`projects/multimedia/jpeg_encode_example`


## 2. 支持能力


- NV12 输入静态 JPEG 编码

- Frame 整帧模式（`bk_jpeg_encode_frame_new`）

- 硬件 / 软件 Flexa 低延迟模式

- 质量档位 0~10（IOCTL 调节）

参见

Frame 与 Flexa 模式说明见 [Frame 与 Flexa 模式](flexa_frame.md "flexa_frame.md")。CLI `jpeg_encode frame` / `jpeg_encode flexa` 分别对应 Frame 与软件 Flexa。


## 3. 相关宏定义

| 宏名称 | 说明 |
| --- | --- |
| CONFIG_BK_ENCODER | 使能 VCENC 编码子系统 |
| CONFIG_BK_ENCODER_MJPEG_TASK_SIZE | JPEG 编码任务栈大小 |
| CONFIG_BK_ENCODER_MJPEG_MAX_OUTPUT_BUFFER | JPEG 最大输出缓冲区（字节） |


## 4. 调试说明


### 4.1 编译与烧录


```
cd <SDK_ROOT>
make bk7259 PROJECT=multimedia/jpeg_encode_example -j$(nproc)

```


### 4.2 CLI 命令


```
jpeg_encode help
jpeg_encode frame
jpeg_encode flexa

```


- 内置 256×128 NV12 平铺为 1920×1080 输入，10 帧，质量档 5

- `flexa` 为软件 Flexa 模式

- 成功标志：`[RESULT][PASS] bk_jpeg_encode_frame_test success` / `bk_jpeg_encode_sw_flexa_test success`

- 使能 `CONFIG_BK_ENCODER` 时上电自动运行 Frame + Flexa 自检


## 5. 使用流程


```
bk_jpeg_encode_ctlr_handle_t encoder = NULL;
bk_jpeg_encode_frame_config_t cfg = {0};
cfg.width = 256;
cfg.height = 128;
cfg.input_format = BK_PIXEL_FORMAT_NV12;
cfg.input_buf = nv12_phys_addr;
cfg.quality = 5;
cfg.outbuf_malloc = jpeg_outbuf_malloc;
cfg.outbuf_complete = jpeg_outbuf_complete;

bk_jpeg_encode_frame_new(&encoder, &cfg);
bk_jpeg_encode_init(encoder);
bk_jpeg_encode_open(encoder);

bk_jpeg_encode_input_t input = {
    .input_buf = nv12_phys_addr,
};
bk_jpeg_encode_frame(encoder, &input);

bk_jpeg_encode_close(encoder);
bk_jpeg_encode_deinit(encoder);
bk_jpeg_encode_delete(encoder);

```

Flexa 硬件路径：`bk_jpeg_encode_hw_flexa_new()`；软件 Flexa：`bk_jpeg_encode_sw_flexa_new()`。

质量调节：


```
uint8_t quality = 8;
bk_jpeg_encode_ioctl(encoder, BK_JPEG_ENCODE_IOCTL_SET_QUALITY, &quality);

```
