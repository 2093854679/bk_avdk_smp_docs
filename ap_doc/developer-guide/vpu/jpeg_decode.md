# JPEG 解码



## 1. 概述

JPEG 硬件解码基于 VCDec JPEG 通路，通过 `bk_jpeg_decode_*` 控制器完成 JPEG 图像解码。


- 头文件：`ap/include/components/bk_decode/bk_jpeg_decode_ctlr.h`

- 示例工程：`projects/multimedia/jpeg_decode_example`


## 2. 支持能力


- 标准 JPEG 格式解码

- Frame 整帧模式（`bk_jpeg_decode_frame_ctlr_new`）

- Flexa 低延迟分段模式（`bk_jpeg_decode_flexa_ctlr_new`）

- 图像信息查询（`bk_jpeg_decode_get_img_info`）

- 支持与 GPU / H264E 端口绑核（bond）

参见

Frame 与 Flexa 模式说明见 [Frame 与 Flexa 模式](flexa_frame.md "flexa_frame.md")。CLI `vcdec_jpegd` 为 Frame，`vcdec_jpegd_flexa` 为 Flexa。


## 3. 相关宏定义

| 宏名称 | 说明 |
| --- | --- |
| CONFIG_BK_DECODER | 使能 VCDec（JPEG 解码依赖此宏） |


## 4. 调试说明


### 4.1 编译与烧录


```
cd <SDK_ROOT>
make bk7259 PROJECT=multimedia/jpeg_decode_example -j$(nproc)

```


### 4.2 CLI 命令


```
jpeg_decode help
jpeg_decode jpegd
jpeg_decode jpegd_flexa
jpeg_decode vcdec_jpegd          # 需 CONFIG_BK_DECODER
jpeg_decode vcdec_jpegd_flexa

```


- `jpegd` / `jpegd_flexa`：平台 JPEG 解码示例

- `vcdec_jpegd` / `vcdec_jpegd_flexa`：VCDec JPEG 通路（`vcdec_jpeg_test.c`）

- 使能 `CONFIG_BK_DECODER` 时上电自检：依次运行 Flexa 和整帧模式

警告

硬解码输出为 YUYV 格式；图像宽度须为 16 的倍数，高度须为 8 的倍数。


## 5. 使用流程


```
bk_jpeg_decode_ctlr_handle_t decoder = NULL;
bk_jpeg_decode_frame_config_t cfg = DEFAULT_JPEG_DECODE_FRAME_CONFIG;
cfg.out_width = 176;
cfg.out_height = 144;
cfg.out_format = BK_PIXEL_FORMAT_YUYV;

bk_jpeg_decode_frame_ctlr_new(&decoder, &cfg);
bk_jpeg_decode_init(decoder);
bk_jpeg_decode_open(decoder);

bk_jpeg_decode_input_t input = {
    .stream = jpeg_data,
    .stream_len = jpeg_len,
    .out_buffer = yuv_buf,
    .out_buffer_size = yuv_size,
};
bk_jpeg_decode_frame(decoder, &input);

bk_jpeg_decode_close(decoder);
bk_jpeg_decode_deinit(decoder);
bk_jpeg_decode_delete(decoder);

```

Flexa 模式使用 `bk_jpeg_decode_flexa_ctlr_new()`，配置宏 `DEFAULT_JPEG_DECODE_FLEXA_CONFIG`。
