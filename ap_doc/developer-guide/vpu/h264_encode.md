---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/vpu/h264_encode.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="h-264"></a>

# H.264 编码

<a id="id1"></a>

## 1\. 概述

H.264 硬件编码基于 VCENC IP，通过 `bk_h264_encode_*` 控制器将 NV12/YUV 输入编码为 H.264 码流。

- 头文件：`ap/include/components/bk_encode/bk_h264_encode_ctlr.h`
- 示例工程：`projects/multimedia/h264_encode_example`

<a id="id2"></a>

## 2\. 支持能力

- H.264 硬件编码（VCENC 后端）
- Frame 整帧模式（`bk_h264_encode_frame_new`）
- 硬件 / 软件 Flexa 低延迟模式
- GOP 与码率控制配置
- 强制 IDR：`bk_h264_encode_force_idr()`
- 硬件 OSD：`bk_h264_encode_set_osd()`，以及空心矩形便捷接口
  `bk_h264_encode_set_osd_bitmap_boxes()` /
  `bk_h264_encode_set_osd_argb8888_boxes()` （见第 6 节）

参见

Frame 与 Flexa 模式说明见 [Frame 与 Flexa 模式](flexa_frame.md)。CLI `vcenc_h264e` 为 Frame，`vcenc_h264e_flexa` 为软件 Flexa。

<a id="id3"></a>

## 3\. 相关宏定义

| 宏名称 | 说明 |
| --- | --- |
| CONFIG\_BK\_ENCODER | 使能 VCENC 编码子系统 |
| CONFIG\_BK\_ENCODER\_H264\_TASK\_SIZE | H.264 编码任务栈大小 |
| CONFIG\_BK\_ENCODER\_H264\_MAX\_OUTPUT\_BUFFER | 最大输出缓冲区（字节） |
| CONFIG\_ENCODER\_H264\_CLK\_240M | 使用 240MHz H.264 编码时钟 |

<a id="id4"></a>

## 4\. 调试说明

<a id="id5"></a>

### 4.1 编译与烧录

```
cd <SDK_ROOT>
make bk7259 PROJECT=multimedia/h264_encode_example -j$(nproc)
```

<a id="cli"></a>

### 4.2 CLI 命令

```
h264_encode help
h264_encode vcenc_h264e
h264_encode vcenc_h264e_flexa
```

- `vcenc_h264e`：整帧模式，256×128 NV12 输入，编码 30 帧，GOP\=15
- `vcenc_h264e_flexa`：软件 Flexa 模式
- 成功标志：`[RESULT][PASS] ...`
- 使能 `CONFIG_BK_ENCODER` 时上电自动运行编码自检

<a id="id6"></a>

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

<a id="id7"></a>

## 5\. 使用流程

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

<a id="osd"></a>

## 6\. OSD 空心矩形

编码器在编码前支持硬件 OSD 叠加。除直接传入像素 buffer 的
`bk_h264_encode_set_osd()` 外，还提供两套便捷接口，用于在指定 overlay
槽位上批量绘制空心矩形：

| API | 说明 |
| --- | --- |
| `bk_h264_encode_set_osd_bitmap_boxes()` | 单色 BITMAP（1bpp）空心矩形批处理 |
| `bk_h264_encode_set_osd_argb8888_boxes()` | 多色 ARGB8888 空心矩形批处理 |

实现会根据本批所有矩形的轴对齐包围盒（union bbox）分配一块画布，栅格化边框后
安装到 `boxes->index` 对应的 overlay 槽位；后续编码帧自动叠加。传入
`count == 0` 或 `boxes == NULL` 可清除该槽位。

源码：`ap/components/bk_vpu/bk_encoder/common/h264_encode_osd.c`

<a id="id8"></a>

### 6.1 OSD 限制

以下限制对 `bk_h264_encode_set_osd()` 与空心矩形便捷接口均适用（未注明处为通用约束）。
编码器须已 `open` 后才能设置 OSD。

| 限制项 | 说明 |
| --- | --- |
| Overlay 槽位 | `index` 范围 `0..7`，共 8 路 |
| 空心矩形数量 | 单次调用 `count` 上限 `64`；`width` / `height` / `thickness` 均须非 0 |
| 必须落在帧内 | 矩形或 OSD 区域不得超出编码帧宽高 |
| 几何最大值 | `x` / `y` / `width` / `height` 均不得超过 `65535` |
| 坐标对齐 | `x` / `y` 须 2 像素对齐（便捷接口内部会对画布自动对齐） |
| BITMAP 尺寸对齐 | `set_osd` 时 BITMAP 的 `width` / `height` 须 8 像素对齐 |
| NV12 尺寸对齐 | `set_osd` 时 NV12 的 `width` / `height` 须为偶数 |
| Buffer 地址对齐 | `set_osd` 的 `buffer` 须 4 字节对齐；且 `buffer_free` 非空 |
| CTB 不重叠 | 不同槽位的 OSD 区域不得落在同一硬件 CTB（`64x16`）内，否则设置失败 |
| BITMAP 颜色 | 空心矩形 BITMAP 接口整批仅一种前景色（取 `boxes[0].color`） |
| ARGB 透明度 | `0xAARRGGBB` 中若 `A == 0`，实现强制为不透明 `0xFF` |
| 画质建议 | 框线起始点、宽高、线宽建议为 16 的倍数，避免高 QP 时马赛克（见 6.5） |

重要

CTB 不重叠是硬件约束：两路 OSD 即使像素矩形不相交，只要覆盖同一 `64x16`
CTB 块也会失败。多槽位布局时请拉开间距或合并到同一槽位（如一批 boxes）。

<a id="bitmap"></a>

### 6.2 BITMAP 单色矩形

```
avdk_err_t bk_h264_encode_set_osd_bitmap_boxes(
    bk_h264_encode_ctlr_handle_t handle,
    bk_h264_encode_osd_bitmap_boxes_t *boxes);
```

- 整批矩形共用一种前景色，取自 `boxes->boxes[0].color`
  （RGB888 `0x00RRGGBB`，内部转为 YUV）；后续 box 的 `color` 会被忽略。
- `alpha` 为全局透明度；传 `0` 时按 `255` 处理。
- 槽位与数量等限制见 6.1。

<a id="argb8888"></a>

### 6.3 ARGB8888 多色矩形

```
avdk_err_t bk_h264_encode_set_osd_argb8888_boxes(
    bk_h264_encode_ctlr_handle_t handle,
    bk_h264_encode_osd_argb8888_boxes_t *boxes);
```

- 每个 box 可使用独立颜色，格式 `0xAARRGGBB`；若 `A == 0`，
  实现会强制为不透明 `0xFF` （方便直接传 RGB888）。
- 非边框像素保持透明（A\=0），硬件按 per-pixel alpha 混合。
- 槽位与数量等限制见 6.1。

<a id="id9"></a>

### 6.4 内存占用

画布覆盖本批所有矩形的轴对齐包围盒，并对齐后按格式分配 buffer（来自 UNCODED /
PSRAM 侧 frame buffer 堆，由编码器持有，直到被替换或清除）。

| 格式 | 对齐规则 | 占用公式 |
| --- | --- | --- |
| BITMAP (1bpp) | x/y 向下对齐 2；width/height 向上对齐 8 | `(canvas_w / 8) * canvas_h` |
| ARGB8888 (32bpp) | x/y/width/height 均对齐 2 | `canvas_w * canvas_h * 4` |

示例（单个 `100x80` 矩形）：

- BITMAP：画布 `104x80` → `1040` 字节
- ARGB8888：画布 `100x80` → `32000` 字节

重要

相同画布尺寸下，ARGB8888 内存约为 BITMAP 的 32 倍（32 bpp vs 1 bpp）。
单色场景优先使用 `bk_h264_encode_set_osd_bitmap_boxes()`。

<a id="id10"></a>

### 6.5 几何约束（避免马赛克）

H.264 按宏块编码。空心矩形的细线若未与宏块边界对齐，在 QP 偏大时容易在
框线附近出现马赛克块。

备注

建议每个矩形的起始点 `(x, y)`、宽高 `(width, height)` 以及
线条宽度 `thickness` 均为 16 的倍数。不满足时功能仍可用，但高 QP
下画质更容易劣化。

<a id="id11"></a>

### 6.6 使用示例

```
/* BITMAP：单色空心框，几何按 16 对齐 */
static const bk_h264_encode_osd_bitmap_box_t boxes[] = {
    { .x = 32, .y = 32, .width = 240, .height = 160, .thickness = 16,
      .color = 0x00FF0000 },
};
bk_h264_encode_osd_bitmap_boxes_t cfg = {
    .index = 0,
    .alpha = 255,
    .count = 1,
    .boxes = boxes,
};
bk_h264_encode_set_osd_bitmap_boxes(enc, &cfg);

/* ARGB8888：多色空心框 */
static const bk_h264_encode_osd_argb8888_box_t argb_boxes[] = {
    { .x = 32,  .y = 32,  .width = 240, .height = 160, .thickness = 16,
      .color = 0xFFFF0000 }, /* 红 */
    { .x = 352, .y = 112, .width = 192, .height = 144, .thickness = 16,
      .color = 0xFF00FF00 }, /* 绿 */
};
bk_h264_encode_osd_argb8888_boxes_t argb_cfg = {
    .index = 0,
    .count = 2,
    .boxes = argb_boxes,
};
bk_h264_encode_set_osd_argb8888_boxes(enc, &argb_cfg);

/* 清除槽位 0 */
bk_h264_encode_osd_bitmap_boxes_t clear = {
    .index = 0, .count = 0, .boxes = NULL,
};
bk_h264_encode_set_osd_bitmap_boxes(enc, &clear);
```

<a id="api"></a>

## 7\. API 说明

公开接口声明于 `bk_h264_encode_ctlr.h`。本节补充文档中此前未展开的接口；
空心矩形 OSD 见第 6 节，生命周期示例见第 5 节。

<a id="id12"></a>

### 7.1 创建接口

| API | 说明 |
| --- | --- |
| `bk_h264_encode_frame_new` | 创建 Frame 整帧编码器 |
| `bk_h264_encode_hw_flexa_new` | 创建硬件 Flexa 编码器 |
| `bk_h264_encode_sw_flexa_new` | 创建软件 Flexa 编码器 |

三种 `*_new` 均需提供 `outbuf_malloc` / `outbuf_complete` 回调。
Frame / Flexa 差异见 [Frame 与 Flexa 模式](flexa_frame.md)。

<a id="id13"></a>

### 7.2 生命周期

| API | 说明 |
| --- | --- |
| `bk_h264_encode_init` | 初始化编码器资源 |
| `bk_h264_encode_open` | 打开编码器，准备开始编码 |
| `bk_h264_encode_start` | 启动/触发一次编码 |
| `bk_h264_encode_close` | 关闭编码器；释放已安装的 OSD buffer |
| `bk_h264_encode_deinit` | 反初始化 |
| `bk_h264_encode_delete` | 销毁控制器，释放句柄 |

推荐顺序：`*_new` → `init` → `open` → （运行期配置 / `start`）→
`close` → `deinit` → `delete`。

<a id="idr-gop"></a>

### 7.3 强制 IDR 与 GOP

```
avdk_err_t bk_h264_encode_force_idr(bk_h264_encode_ctlr_handle_t handle);

avdk_err_t bk_h264_encode_set_gop_frame_count(bk_h264_encode_ctlr_handle_t handle,
                                              uint32_t gop_frame_count);
avdk_err_t bk_h264_encode_get_gop_frame_count(bk_h264_encode_ctlr_handle_t handle,
                                              uint32_t *gop_frame_count);
```

- `force_idr`：下一帧强制编码为 IDR。
- `set_gop_frame_count` / `get_gop_frame_count`：运行中设置/读取 GOP 帧数。

```
bk_h264_encode_force_idr(encoder);
bk_h264_encode_set_gop_frame_count(encoder, 15);

uint32_t gop = 0;
bk_h264_encode_get_gop_frame_count(encoder, &gop);
```

<a id="id14"></a>

### 7.4 码率控制

```
avdk_err_t bk_h264_encode_set_rate_ctrl(bk_h264_encode_ctlr_handle_t handle,
                                        bk_h264_encode_rate_ctrl_t *rate_ctrl);
avdk_err_t bk_h264_encode_get_rate_ctrl(bk_h264_encode_ctlr_handle_t handle,
                                        bk_h264_encode_rate_ctrl_t *rate_ctrl);
```

`bk_h264_encode_rate_ctrl_t` 字段：

| 字段 | 说明 |
| --- | --- |
| `bitrate` | 非 0：码率模式（bps）；0：固定 QP 模式 |
| `qp_min_i` | 码率模式下 I 帧最小 QP；固定模式下为 I 帧固定 QP |
| `qp_max_i` | 码率模式下 I 帧最大 QP；0 表示保持内部默认；固定模式下忽略 |
| `qp_min_p` | 码率模式下 P 帧最小 QP；固定模式下为 P 帧固定 QP |
| `qp_max_p` | 码率模式下 P 帧最大 QP；0 表示保持内部默认；固定模式下忽略 |

```
bk_h264_encode_rate_ctrl_t rc = {
    .bitrate = 2000000,
    .qp_min_i = 20, .qp_max_i = 40,
    .qp_min_p = 22, .qp_max_p = 42,
};
bk_h264_encode_set_rate_ctrl(encoder, &rc);

bk_h264_encode_rate_ctrl_t cur;
bk_h264_encode_get_rate_ctrl(encoder, &cur);
```

<a id="osd-buffer"></a>

### 7.5 自定义 OSD buffer

空心矩形便捷接口见第 6 节。若需自行绘制任意 OSD 内容，使用：

```
avdk_err_t bk_h264_encode_set_osd(bk_h264_encode_ctlr_handle_t handle,
                                  bk_h264_encode_osd_t *osd);
```

- 调用方分配并填充 `osd->buffer`，通过 `osd->buffer_free` 将所有权交给编码器；
  成功后调用方不得再修改该 buffer。
- `format` 支持 `ARGB8888` / `NV12` / `BITMAP`。
- `BITMAP` 时需填写 `bitmap_y/u/v` 前景色；`alpha` 对 NV12/BITMAP 生效，
  ARGB8888 使用像素内 alpha。
- `buffer == NULL` 可清除该槽位；更新同一槽位时旧 buffer 经原 `buffer_free` 释放；
  `close` 时释放全部已安装 OSD。
- 对齐、槽位、CTB 不重叠等硬性限制见 6.1。

```
bk_h264_encode_osd_t osd = {
    .index = 0,
    .buffer = my_bitmap,
    .format = BK_H264_ENCODE_OVERLAY_FORMAT_BITMAP,
    .alpha = 255,
    .x = 32, .y = 32, .width = 128, .height = 64,
    .bitmap_y = 76, .bitmap_u = 84, .bitmap_v = 255, /* 示例：红色 YUV */
    .buffer_free = my_osd_free,
    .free_arg = NULL,
};
bk_h264_encode_set_osd(encoder, &osd);
```
