---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/gui/bk_draw_osd.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bk-draw-osd"></a>

# bk\_draw\_osd 开发者指南

<a id="id1"></a>

## 1、概述

`bk_draw_osd` 是 BK7259 SDK 提供的 **GPU OSD 叠加组件**，用于在 UVC / MIPI 等视频 pipeline 上叠加图标、文字等透明 UI 元素。

组件采用 pipeline 提交模型：不自建 VG-Lite 上下文，而是把 CPU 合成好的透明 sprite 注册给已经打开的视频链路 GPU（`bk_gpu_blit_set`），由 GPU 每帧对视频做 `SRC_OVER` alpha 融合。

- 组件源码：`ap/components/bk_draw_osd`
- 公共头文件：`ap/include/components/bk_draw_osd.h`、`bk_draw_osd_types.h`
- 参考示例：`projects/multimedia/draw_osd_example`
- 详细 API / 设计说明（示例工程内）：`draw_osd_example/docs/bk_draw_osd_usage_CN.md`、`bk_draw_osd_design_CN.md`

使用前需满足三条前提：

1. 视频 pipeline 已打开，且能拿到已 `vg_lite_init` 的 `bk_gpu_ctlr_handle_t`。
2. 每个 `bk_draw_osd_new()` 绑定一个 GPU 实例；UVC / MIPI 各持一个实例，互不干扰。
3. 对外渲染入口只有 3 个（`array`、`element`、`text`），内部分槽与提交对用户透明。

<a id="id2"></a>

## 2、组件功能简介

<a id="id3"></a>

### 2.1 分层结构

```
工程侧（blend_info 资产 + pipeline GPU handle）
        │
        ▼
bk_draw_osd.c          — 公共薄 wrapper（参数校验 + 转发）
        │
        ▼
bk_draw_osd_ctlr.c     — 控制器（资产表/显示列表/mutex/add-remove/自动聚簇分槽）
        │
        ▼
bk_osd_engine.c        — 合成引擎（PSRAM sprite 合成 + bk_gpu_blit_set 提交）
        │
        ▼
外部 pipeline GPU      — 每帧 SRC_OVER 叠加到视频帧
```

<a id="id4"></a>

### 2.2 主要能力

- 图标 \+ 文字：`BLEND_TYPE_IMAGE` （ARGB8888 字节流）与 `BLEND_TYPE_FONT` （emWin/bk\_font 字模）。
- 可选 LVGL 字库：经 `bk_draw_osd_text` 使用抗锯齿字体（组件内置最小化 LVGL 解码器，不依赖 `CONFIG_LVGL`）。
- 多区域 multi-blit：最多 ``` BK_GPU_BLIT_SLOT_MAX``（当前 4）个独立 sprite 槽位；``bk_draw_osd_array ``` 按元素位置自动聚簇分槽。
- 运行时更新：`add_or_update` 与 `remove` 修改显示列表，再 `array(NULL)` 重画生效。
- 融合时机可选：整帧末一次 blit（默认）或 flexa 逐块分散 blit（`BK_GPU_IOCTL_SET_OSD_BY_FLEXA`）。

<a id="id5"></a>

## 3、设计原理简述

<a id="id6"></a>

### 3.1 合成与提交

一次 OSD 更新在引擎内部走 `begin → put_icon/put_text → commit`：

1. 从 PSRAM 分配透明 ARGB8888 sprite（按元素包围盒裁剪，非整屏）。
2. CPU 把图标像素 / 字模 A8 alpha 着色写入 sprite。
3. `commit` 调用 `bk_gpu_blit_set(gpu, sprite, {alpha_blend=1, dst_x/y, src_format})` 注册给 pipeline GPU；sprite 所有权转交 GPU，由 `free` 回调释放。

同一 slot 内多个元素先合成到一张 sprite、一次 blit，GPU 成本与 OSD 裁剪后面积成正比，而非整帧分辨率。

<a id="vs-flexa"></a>

### 3.2 整帧融合 vs flexa 逐块融合

| 模式 | 语义 | 适用 |
| --- | --- | --- |
| ``` frame``（默认，``osd_by_flexa=false ```） | 整帧结束后对 OSD 覆盖区做一次 SRC\_OVER | 少量、集中元素（状态栏、时钟等），单帧总面积建议 ≤ \~40k px |
| ``` flexa``（``osd_by_flexa=true ```） | 在 `gpu_flex_process_line_block()` 里对与 OSD 相交的 flexa block 逐块 SRC\_OVER | 元素分散多角落，或整帧模式出现 `flexa waits frame start` 掉帧 |

设置方式（绑定 GPU 的属性，非 OSD API 参数）：

```
bool osd_by_flexa = false;
bk_gpu_ioctl(gpu, BK_GPU_IOCTL_SET_OSD_BY_FLEXA, &osd_by_flexa);
```

<a id="draw-path"></a>

### 3.3 与人脸框 draw\_path 的区别

人脸识别画框使用 `bk_gpu_draw_path_build()` 绘制矢量描边，在 flexa 逐块路径里与视频一起 rotate，与 OSD sprite blit 是独立通路。`osd_by_flexa` 只影响 OSD 叠加，不影响 draw\_path 画框。

<a id="id7"></a>

## 4、标准使用流程（4 步）

<a id="blend-info"></a>

### 4.1 准备 `blend_info[]` 资产

在工程 `assets/` 定义 `bk_blend_t` 与 ``` blend_info[]``（数组必须以 ``{.addr = NULL} ``` 结尾）。参考 `draw_osd_example/ap/assets/`。

```
const bk_blend_t img_wifi = {
    .blend_type = BLEND_TYPE_IMAGE,
    .name = "wifi", .width = 48, .height = 48,
    .xpos = 8, .ypos = 4,
    .image = { .format = ARGB8888, .data = wifi_argb8888, .data_len = 48 * 48 * 4 },
};

const blend_info_t blend_info[] = {
    { .name = "wifi",  .addr = &img_wifi,   .content = "" },
    { .name = "clock", .addr = &font_clock, .content = "12:34" },
    { .addr = NULL },
};
```

<a id="pipeline-gpu"></a>

### 4.2 创建实例（绑定 pipeline GPU）

```
bk_gpu_ctlr_handle_t gpu = mipi_pipeline_get_gpu_handle();  /* 或 display_get_gpu_handle() */
osd_ctlr_config_t cfg = {0};
cfg.gpu        = gpu;
cfg.panel_w    = 1080;
cfg.panel_h    = 1920;
cfg.src_format = BK_PIXEL_FORMAT_ABGR8888;   /* MIPI；UVC 用 ARGB8888 */
cfg.blend_assets = blend_assets;
cfg.blend_info   = blend_info;
bk_draw_osd_new(&s_osd, &cfg);
```

`panel_w` 与 `panel_h` 填旋转后显示坐标系宽高，用于裁剪与 blit 定位。

<a id="id8"></a>

### 4.3 渲染

```
bk_draw_osd_array(s_osd, NULL);   /* NULL 使用 new 时的默认列表 */
```

追加单个元素（可选）：

```
bk_draw_osd_element(s_osd, &(blend_info_t){ .addr = &font_clock, .content = "12:35" });
bk_draw_osd_text(s_osd, OSD_FONT_LVGL, &lv_font_montserrat_24, "12:35",
                 64, 8, 0xFFFFFF, 1);
```

<a id="id9"></a>

### 4.4 更新 / 清理 / 销毁

```
bk_draw_osd_add_or_update(s_osd, "clock", "12:35");
bk_draw_osd_array(s_osd, NULL);          /* 改列表后必须重画 */

bk_draw_osd_remove(s_osd, "wifi");
bk_draw_osd_array(s_osd, NULL);

bk_draw_osd_clear(s_osd);                /* 只撤 OSD，保留视频 */
bk_draw_osd_delete(s_osd); s_osd = NULL;
```

<a id="api"></a>

## 5、API 概览

| API | 说明 |
| --- | --- |
| `bk_draw_osd_new` | 创建实例，绑定 `cfg.gpu` 与默认列表 |
| `bk_draw_osd_array` | 主入口：渲染 ``` blend_info[]``（``NULL ``` 表示默认列表），自动聚簇分槽 |
| `bk_draw_osd_element` | 一次性渲染单个 `blend_info_t` 元素 |
| `bk_draw_osd_text` | 一次性渲染裸字体文本（LVGL / bk\_font） |
| `bk_draw_osd_add_or_update` 与 `remove` | 运行时增删动态列表项（需再 `array` 生效） |
| `bk_draw_osd_clear` 与 `delete` | 清除 blit / 释放实例 |
| `bk_draw_osd_ioctl` | 查询资产表与当前列表 |

关键配置结构 `osd_ctlr_config_t`：

```
typedef struct {
    bk_gpu_ctlr_handle_t gpu;
    uint16_t panel_w, panel_h;
    bk_pixel_format_t src_format;
    const blend_info_t *blend_assets;
    const blend_info_t *blend_info;
    bool draw_in_psram;
} osd_ctlr_config_t;
```

<a id="cli"></a>

## 6、参考工程与 CLI

<a id="id10"></a>

### 6.1 编译

在 SDK 根目录：

```
make bk7259 PROJECT=multimedia/draw_osd_example -j32
```

<a id="cli-ap-cp-ap-cmd"></a>

### 6.2 CLI 命令（AP 侧，从 CP 串口需加 `ap_cmd` 前缀）

```
ap_cmd osd <mipi|uvc> <frame|flexa|update|remove|clear|close> [参数]
```

| 子命令 | 说明 |
| --- | --- |
| `frame` 与 `flexa` | 显示 OSD 并选择融合时机（首次自动拉起 pipeline） |
| `update <name> <content>` | 更新图标/文本内容 |
| `remove <name>` | 移除元素 |
| `clear` | 只撤 OSD，保留视频 |
| `close` | 销毁 OSD 并关闭 pipeline |

MIPI 与 UVC 共用 GPU/显存，不能同时开启；切换前先 `close` 当前通路。

<a id="id11"></a>

## 7、移植清单

1. 工程 `CMakeLists.txt` 与 `defconfig` 增加 ``` bk_draw_osd``（依赖 ``bk_gpu ```）。
2. 准备 `assets/`：`bk_img.c`、`bk_font.c`、`blend_dsc.c`、`blend.h`。
3. 将 `mipi_pipeline_get_gpu_handle()` 与 `display_get_gpu_handle()` 替换为本工程 pipeline 的实际接口。
4. 按输出通路设置 ``` cfg.src_format``（MIPI=``ABGR8888 ```，UVC\=\`\`ARGB8888\`\`）。
5. 少量集中元素用默认 `frame`；分散或大面积 OSD 可切 `flexa`。
6. 准备好 `blend_info[]` 后调用 `bk_draw_osd_array` 即可，无需手动管理 slot。
7. 若用 LVGL 抗锯齿字库：字库 `.c` 改 `#include "bk_osd_lv_font.h"`，`lv_font_t` 里 `.get_glyph_dsc` 与 `.get_glyph_bitmap` 置 ``` NULL``（OSD 直接读 ``font->dsc ```）。

<a id="id12"></a>

## 8、注意事项

1. 必须先有 pipeline GPU：`cfg.gpu` 为 NULL 时 `new` 失败。
2. 颜色格式：MIPI 用 `ABGR8888`，否则红蓝反；指定颜色时 MIPI 下 `argb` 按 `0x00BBGGRR` 填写。
3. 资源生命周期：`blend_assets`、`blend_info`、图标、字模均不深拷贝，指针须在 handle 存活期有效。
4. 槽位上限：自动聚簇最多 ``` BK_GPU_BLIT_SLOT_MAX``（4）个 slot；``add_or_update ``` 与 `remove` 后须再 `array`。
5. MIPI 摄像头：需 1.8V VDDIO（`PM_AUXLDO_USER_DISPLAY`）与 `CONFIG_XTAL_FREQ=12000000`。
6. 掉帧排查：大面积整帧 OSD 出现 `flexa waits frame start` 时，尝试 `flexa` 模式或减小 OSD 裁剪面积。

<a id="id13"></a>

## 9、常见问题

| 现象 | 处理建议 |
| --- | --- |
| 改了内容不刷新 | `add_or_update` 与 `remove` 后忘记 `bk_draw_osd_array(h, NULL)` |
| 图标/文字红蓝反 | MIPI 设 `BK_PIXEL_FORMAT_ABGR8888`；文本颜色按 `0x00BBGGRR` |
| 切通路 OOM | 先 `osd <当前源> close` 再开另一路 |
| `flexa waits frame start` | OSD 总面积过大或过于分散；切 `flexa` 或压缩 OSD 区域 |
| LVGL 字库链接报错 | 字库 `.c` 改 `bk_osd_lv_font.h`，回调置 `NULL`；同固件链完整 LVGL 时可保留标准 `lv_font_get_*` 指针 |
