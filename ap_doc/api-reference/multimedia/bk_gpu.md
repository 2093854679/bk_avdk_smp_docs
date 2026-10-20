---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/multimedia/bk_gpu.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="gpu"></a>

# GPU

<a id="id1"></a>

## 1\. 概述

BK GPU 模块基于 `vg_lite` GPU 能力，提供面向多媒体链路的图像处理接口。当前接口主要用于 Flexa 分行处理场景，可对输入图像执行缩放、旋转、压缩输出、图形路径绘制以及图像叠加（blit）等操作。

从接口层次上看，`bk_gpu` 提供面向 AVDK 多媒体业务的控制器封装，负责串联 Flexa、帧内存回调、输出帧通知以及常用的绘制/叠加配置；`vg_lite` 则是底层 GPU 原生图形接口，提供 buffer 管理、blit、path 绘制、矩阵变换、渐变、mask layer、Flexa 控制等更细粒度能力。因此本文前半部分先说明 `bk_gpu` 封装接口，第 6 章再补充 `vg_lite` 原生接口的能力分类和直接调用场景，便于需要绕过封装或扩展图形能力的应用参考。

典型使用流程如下：

1. 配置 `bk_gpu_ctlr_config_t`，指定输入/输出尺寸、像素格式、旋转角度、Flexa 参数和帧内存回调。
2. 调用 `bk_gpu_ctlr_new()` 创建 GPU 控制器句柄。
3. 调用 `bk_gpu_init()` 初始化 GPU 资源。
4. 调用 `bk_gpu_open()` 启动 GPU Flexa 处理线程。
5. 根据业务需要调用 `bk_gpu_draw_path_build()`、`bk_gpu_draw_path_clear()`、`bk_gpu_blit_set()`、`bk_gpu_blit_clear()` 或 `bk_gpu_ioctl()`。
6. 退出时按 `bk_gpu_close()`、`bk_gpu_deinit()`、`bk_gpu_delete()` 的顺序释放资源。

备注

当前默认控制器要求 `bk_gpu_ctlr_config_t.flexa` 设置为 `true`。`bk_gpu_init()` 和 `bk_gpu_open()` 依赖 Flexa 配置、帧内存分配回调以及 GPU 连续内存，配置不完整时会返回错误。

<a id="id2"></a>

## 2\. 头文件

使用 BK GPU API 时需要包含以下头文件：

```
#include <components/bk_gpu.h>
#include <components/bk_gpu_ctlr.h>
#include <components/bk_gpu_types.h>
```

<a id="id3"></a>

## 3\. 数据类型

<a id="bk-gpu-ctlr-handle-t"></a>

### 3.1 bk\_gpu\_ctlr\_handle\_t

```
typedef struct bk_gpu_ctlr_t *bk_gpu_ctlr_handle_t;
```

GPU 控制器句柄。应用通过 `bk_gpu_ctlr_new()` 获取该句柄，并在后续 API 中传入。

<a id="bk-gpu-ctlr-config-t"></a>

### 3.2 bk\_gpu\_ctlr\_config\_t

```
typedef struct
{
    uint16_t tess_width;
    uint16_t tess_height;
    uint16_t src_width;
    uint16_t src_height;
    uint16_t dst_width;
    uint16_t dst_height;
    bk_pixel_format_t src_format;
    bk_pixel_format_t dst_format;
    uint16_t rotate_degree;
    uint8_t *src_buffer;
    bool scale;
    bool compress;
    bool flexa;
    uint8_t flexa_lines;
    uint8_t flexa_buff_cnt;
    void *(*frame_malloc)(uint32_t size);
    avdk_err_t (*frame_free)(void *ptr);
    void (*flexa_line_done)(uint32_t done_lines, void *args);
    void *flexa_line_done_args;
    void (*frame_done)(void *frame, uint32_t frame_size, void *args);
    void *frame_done_args;
} bk_gpu_ctlr_config_t;
```

成员说明：

- `tess_width` / `tess_height`：GPU tessellation 缓冲区尺寸，用于 `vg_lite_init()`。矢量 path 绘制需要该缓冲区完成路径 tessellation。如果应用不使用矢量绘制，只使用缩放、旋转、压缩或 blit 等图像处理能力，则这两个字段可以设置为 `0`。
- `src_width` / `src_height`：源图像宽高。
- `dst_width` / `dst_height`：目标图像宽高。
- `src_format` / `dst_format`：源图像和目标图像像素格式，类型为 `bk_pixel_format_t`。
- `rotate_degree`：旋转角度。blit 接口当前支持 `0`、`90`、`180`、`270`。
- `src_buffer`：Flexa 源图像缓冲区地址。
- `scale`：是否启用缩放。
- `compress`：是否启用压缩输出。
- `flexa`：是否启用 Flexa 模式。默认控制器要求该字段为 `true`。
- `flexa_lines`：Flexa 每次处理的行数。
- `flexa_buff_cnt`：Flexa 缓冲区数量。
- `frame_malloc`：目标帧内存分配回调。
- `frame_free`：目标帧内存释放回调。
- `flexa_line_done`：Flexa 分行完成回调，可为空。
- `flexa_line_done_args`：传递给 `flexa_line_done` 的用户参数。
- `frame_done`：一帧处理完成回调，输出帧地址和帧大小由该回调接收。
- `frame_done_args`：传递给 `frame_done` 的用户参数。

<a id="bk-gpu-blit-config-t"></a>

### 3.3 bk\_gpu\_blit\_config\_t

```
typedef struct
{
    uint16_t src_x;
    uint16_t src_y;
    uint16_t src_width;
    uint16_t src_height;
    bk_pixel_format_t src_format;
    uint16_t dst_x;
    uint16_t dst_y;
    uint16_t rotate_degree;
    void *args;
    void (*free)(void *frame, void *args);
} bk_gpu_blit_config_t;
```

用于配置待叠加图像的位置、尺寸、格式和释放回调。

- `src_x` / `src_y`：源图像裁剪区域左上角坐标。
- `src_width` / `src_height`：源图像裁剪区域宽高。
- `src_format`：源图像像素格式。
- `dst_x` / `dst_y`：叠加到目标图像上的目标坐标。
- `rotate_degree`：叠加图像旋转角度，支持 `0`、`90`、`180`、`270`。
- `args`：传递给 `free` 回调的用户参数。
- `free`：blit 缓冲区释放回调。调用 `bk_gpu_blit_clear()` 或内部替换 blit 缓冲区时会使用该回调释放已保存的帧。

<a id="bk-gpu-draw-path-set-t"></a>

### 3.4 bk\_gpu\_draw\_path\_set\_t

```
typedef struct
{
    uint8_t *cmd;
    void *data;
    uint32_t size;
    uint8_t alpha;
    uint32_t color;
} bk_gpu_draw_path_set_t;
```

用于配置 `vg_lite` 路径绘制数据。

- `cmd`：路径命令缓冲区。
- `data`：路径坐标数据缓冲区。
- `size`：路径命令数量。
- `alpha`：透明度字段，预留给上层配置。
- `color`：路径颜色，格式为 ARGB8888。

<a id="bk-gpu-ioctl-cmd-t"></a>

### 3.5 bk\_gpu\_ioctl\_cmd\_t

```
typedef enum
{
    BK_GPU_IOCTL_SET_FLEXA_LINES_READY,
    BK_GPU_IOCTL_SET_NOTIFY,
    BK_GPU_IOCTL_REGISTER_BOND,
    BK_GPU_IOCTL_UNREGISTER_BOND,
    BK_GPU_IOCTL_FLEXA_ADDR_MAPPING,
    BK_GPU_IOCTL_FLEXA_ADDR_UNMAPPING,
    BK_GPU_IOCTL_LOCK,
    BK_GPU_IOCTL_UNLOCK,
} bk_gpu_ioctl_cmd_t;
```

IOCTL 命令说明：

- `BK_GPU_IOCTL_SET_FLEXA_LINES_READY`：通知 GPU 指定行数的 Flexa 数据已经就绪。
- `BK_GPU_IOCTL_SET_NOTIFY`：通知 GPU 重新开始 Flexa 处理。
- `BK_GPU_IOCTL_REGISTER_BOND`：注册 Flexa bond 对象，参数为 `bk_flexa_bond_t *`。
- `BK_GPU_IOCTL_UNREGISTER_BOND`：注销 Flexa bond 对象，参数为 `bk_flexa_bond_t *`。
- `BK_GPU_IOCTL_FLEXA_ADDR_MAPPING`：配置 Flexa 源地址映射，参数为源缓冲区地址。
- `BK_GPU_IOCTL_FLEXA_ADDR_UNMAPPING`：取消 Flexa 地址映射。
- `BK_GPU_IOCTL_LOCK`：锁定 GPU 互斥锁。
- `BK_GPU_IOCTL_UNLOCK`：解锁 GPU 互斥锁。

<a id="id4"></a>

## 4\. 宏定义

<a id="draw-rectangle-path-build"></a>

### 4.1 DRAW\_RECTANGLE\_PATH\_BUILD

```
DRAW_RECTANGLE_PATH_BUILD(_pcmd, _pdat, _xmin, _ymin, _xmax, _ymax)
```

用于向路径命令缓冲区和坐标数据缓冲区写入一个矩形路径。该宏会依次写入 `MOVE`、多段 `LINE` 和 `CLOSE` 命令，并写入矩形四个顶点坐标。常用于目标检测框、手势框等矩形标记绘制。

<a id="api"></a>

## 5\. API 函数

<a id="bk-gpu-ctlr-new"></a>

### 5.1 bk\_gpu\_ctlr\_new

```
avdk_err_t bk_gpu_ctlr_new(bk_gpu_ctlr_handle_t *handle,
                           bk_gpu_ctlr_config_t *config);
```

**功能**：创建 GPU 控制器实例。

**参数**：

- `handle`：输出参数，返回 GPU 控制器句柄。
- `config`：GPU 控制器配置。

**返回值**：

- `AVDK_ERR_OK`：创建成功。
- `AVDK_ERR_INVAL`：参数为空。
- `AVDK_ERR_NOMEM`：内存分配失败。

<a id="bk-gpu-init"></a>

### 5.2 bk\_gpu\_init

```
avdk_err_t bk_gpu_init(bk_gpu_ctlr_handle_t handle);
```

**功能**：初始化 GPU 控制器和底层 GPU 资源。

**参数**：

- `handle`：GPU 控制器句柄。

**返回值**：

- `AVDK_ERR_OK`：初始化成功。
- `AVDK_ERR_INVAL`：句柄无效或 Flexa 未启用。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作。
- `AVDK_ERR_NOMEM`：GPU 连续内存申请失败。

<a id="bk-gpu-deinit"></a>

### 5.3 bk\_gpu\_deinit

```
avdk_err_t bk_gpu_deinit(bk_gpu_ctlr_handle_t handle);
```

**功能**：反初始化 GPU 控制器，释放 `bk_gpu_init()` 阶段初始化的资源。

**参数**：

- `handle`：GPU 控制器句柄。

**返回值**：

- `AVDK_ERR_OK`：反初始化成功。
- `AVDK_ERR_INVAL`：句柄无效或 Flexa 未启用。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作。

<a id="bk-gpu-open"></a>

### 5.4 bk\_gpu\_open

```
avdk_err_t bk_gpu_open(bk_gpu_ctlr_handle_t handle);
```

**功能**：启动 GPU 处理流程。默认控制器会初始化 Flexa 数据结构、分配输出帧缓冲区，并创建 GPU 处理线程。

**参数**：

- `handle`：GPU 控制器句柄。

**返回值**：

- `AVDK_ERR_OK`：启动成功，或者控制器已经处于打开状态。
- `AVDK_ERR_INVAL`：句柄无效或 Flexa 未启用。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作。
- `AVDK_ERR_NOMEM`：帧缓冲区分配失败。

<a id="bk-gpu-close"></a>

### 5.5 bk\_gpu\_close

```
avdk_err_t bk_gpu_close(bk_gpu_ctlr_handle_t handle);
```

**功能**：停止 GPU 处理流程，退出处理线程并释放运行期资源。

**参数**：

- `handle`：GPU 控制器句柄。

**返回值**：

- `AVDK_ERR_OK`：关闭成功，或者控制器已经处于关闭状态。
- `AVDK_ERR_INVAL`：句柄无效或 Flexa 未启用。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作。

<a id="bk-gpu-ioctl"></a>

### 5.6 bk\_gpu\_ioctl

```
avdk_err_t bk_gpu_ioctl(bk_gpu_ctlr_handle_t handle,
                        uint32_t cmd,
                        void *args);
```

**功能**：向 GPU 控制器发送控制命令。

**参数**：

- `handle`：GPU 控制器句柄。
- `cmd`：控制命令，参考 `bk_gpu_ioctl_cmd_t`。
- `args`：命令参数，不同命令的参数含义不同。

**返回值**：

- `AVDK_ERR_OK`：命令执行成功。
- `AVDK_ERR_INVAL`：句柄无效或参数无效。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作或命令不支持。

<a id="bk-gpu-delete"></a>

### 5.7 bk\_gpu\_delete

```
avdk_err_t bk_gpu_delete(bk_gpu_ctlr_handle_t handle);
```

**功能**：删除 GPU 控制器实例。调用前应先完成 `bk_gpu_close()` 和 `bk_gpu_deinit()`。

**参数**：

- `handle`：GPU 控制器句柄。

**返回值**：

- `AVDK_ERR_OK`：删除成功。
- `AVDK_ERR_INVAL`：句柄无效。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作。

<a id="bk-gpu-draw-path-build"></a>

### 5.8 bk\_gpu\_draw\_path\_build

```
avdk_err_t bk_gpu_draw_path_build(bk_gpu_ctlr_handle_t handle,
                                  bk_gpu_draw_path_set_t *path_set);
```

**功能**：设置 GPU 绘制路径。默认控制器会根据 `path_set` 创建 `vg_lite` stroke path，并在后续输出帧上绘制。

**参数**：

- `handle`：GPU 控制器句柄。
- `path_set`：路径配置。

**返回值**：

- `AVDK_ERR_OK`：设置成功。
- `AVDK_ERR_INVAL`：句柄无效。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作。

<a id="bk-gpu-draw-path-clear"></a>

### 5.9 bk\_gpu\_draw\_path\_clear

```
avdk_err_t bk_gpu_draw_path_clear(bk_gpu_ctlr_handle_t handle);
```

**功能**：清除当前 GPU 绘制路径，停止路径绘制。

**参数**：

- `handle`：GPU 控制器句柄。

**返回值**：

- `AVDK_ERR_OK`：清除成功。
- `AVDK_ERR_INVAL`：句柄无效。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作。

<a id="bk-gpu-blit-set"></a>

### 5.10 bk\_gpu\_blit\_set

```
avdk_err_t bk_gpu_blit_set(bk_gpu_ctlr_handle_t handle,
                           void *src_buffer,
                           bk_gpu_blit_config_t *blit_config);
```

**功能**：设置待叠加图像。默认控制器会保存 `src_buffer` 和 `blit_config`，并在 GPU 输出帧上进行 blit 处理。

**参数**：

- `handle`：GPU 控制器句柄。
- `src_buffer`：待叠加图像缓冲区。
- `blit_config`：叠加配置。

**返回值**：

- `AVDK_ERR_OK`：设置成功。
- `AVDK_ERR_INVAL`：句柄无效、配置为空或旋转角度不支持。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作。

备注

`blit_config->free` 应提供有效释放函数。调用 `bk_gpu_blit_clear()` 或替换内部 blit 缓冲区时，默认控制器会通过该回调释放已保存的 blit 帧。

<a id="bk-gpu-blit-clear"></a>

### 5.11 bk\_gpu\_blit\_clear

```
avdk_err_t bk_gpu_blit_clear(bk_gpu_ctlr_handle_t handle);
```

**功能**：清除当前 blit 配置，并释放默认控制器保存的 blit 缓冲区。

**参数**：

- `handle`：GPU 控制器句柄。

**返回值**：

- `AVDK_ERR_OK`：清除成功。
- `AVDK_ERR_INVAL`：句柄无效。
- `AVDK_ERR_UNSUPPORTED`：控制器未实现该操作。

<a id="vg-lite-api"></a>

## 6\. VG Lite API 说明

`vg_lite.h` 位于 `ap/include/modules/vg_lite_gpu/vg_lite.h`，提供更底层的 GPU 图形加速接口。`bk_gpu` 默认控制器内部会调用其中的初始化、路径绘制、矩阵变换和 Flexa 接口；应用也可以在需要直接操作 `vg_lite_buffer_t`、`vg_lite_path_t` 或矩阵时使用这些接口。

备注

`vg_lite` 是底层 GPU 驱动接口。直接调用时需要保证 GPU 已正确初始化，输入/输出 buffer 可被 GPU 访问，并在提交命令后按需要调用 `vg_lite_flush()` 或 `vg_lite_finish()`。

<a id="id5"></a>

### 6.1 核心数据结构

- `vg_lite_buffer_t`：图像或渲染目标 buffer 描述结构，包含宽高、stride、像素格式、CPU 地址、GPU 地址、内存池、YUV 信息、压缩模式、透明度模式等字段。
- `vg_lite_path_t`：路径绘制对象，包含 bounding box、坐标格式、path 数据、stroke 参数和 path 类型等字段。
- `vg_lite_matrix_t`：3x3 变换矩阵，用于 blit、draw、gradient 等接口的平移、缩放、旋转和透视变换。
- `vg_lite_rectangle_t`：矩形区域描述，常用于 clear、blit rect、copy image、masklayer 等接口。
- `vg_lite_linear_gradient_t`、`vg_lite_ext_linear_gradient_t`、`vg_lite_radial_gradient_t`：渐变填充对象，用于路径渐变绘制。

<a id="id6"></a>

### 6.2 初始化与同步接口

- `vg_lite_set_buffer()`：设置 GPU 使用的连续内存 buffer。
- `vg_lite_init()`：初始化 VGLite 上下文，需要传入 tessellation buffer 的宽高。
- `vg_lite_close()`：销毁 VGLite 上下文并释放相关资源。
- `vg_lite_get_info()`：获取 VGLite 驱动信息。
- `vg_lite_get_product_info()`：获取 GPU 芯片名称、ID 和版本信息。
- `vg_lite_query_feature()`：查询指定 GPU 特性是否支持。
- `vg_lite_flush()`：提交命令 buffer，但不等待 GPU 完成。
- `vg_lite_finish()`：提交命令 buffer 并等待 GPU 完成。
- `vg_lite_get_register()`：读取指定 GPU 寄存器值，主要用于调试。
- `vg_lite_frame_delimiter()`：设置当前帧结束标记，并等待 GPU 完成当前帧。

<a id="buffer"></a>

### 6.3 Buffer 管理接口

- `vg_lite_allocate()`：从 GPU 可访问内存中分配 `vg_lite_buffer_t`。
- `vg_lite_free()`：释放由 `vg_lite_allocate()` 分配的 buffer。
- `vg_lite_allocate_with_data()`：使用已有图像数据创建 GPU 可访问 buffer。
- `vg_lite_free_without_free_data()`：释放 `vg_lite_allocate_with_data()` 创建的 buffer 描述，不释放外部数据。
- `vg_lite_upload_buffer()`：将 RGB 或 YUV 数据上传到已分配的 buffer。
- `vg_lite_map()`：将外部 buffer 映射到 GPU 可访问地址空间。
- `vg_lite_unmap()`：取消 buffer 映射。
- `vg_lite_flush_mapped_buffer()`：刷新已映射 buffer 的 cache。
- `vg_lite_get_mem_size()`：查询可用连续 video memory 大小。
- `vg_lite_set_memory_pool()`：设置不同类型 buffer 的内存池。

<a id="id7"></a>

### 6.4 图像处理接口

- `vg_lite_clear()`：用指定颜色填充目标 buffer 或其中的矩形区域。
- `vg_lite_blit()`：将源图像按矩阵变换、混合模式、颜色混合和滤波方式拷贝到目标 buffer。
- `vg_lite_blit_rect()`：仅拷贝源图像的指定矩形区域，并支持矩阵变换、混合和滤波。
- `vg_lite_blit2()`：将两个源图像按各自矩阵变换后混合到目标 buffer。
- `vg_lite_copy_image()`：无变换、无混合地拷贝源图像矩形区域到目标 buffer。
- `vg_lite_set_CLUT()`：设置索引图像使用的颜色查找表，颜色格式为 ARGB。
- `vg_lite_source_global_alpha()`：设置源图像全局 alpha。
- `vg_lite_dest_global_alpha()`：设置目标图像全局 alpha。
- `vg_lite_set_color_key()`：设置 color key。
- `vg_lite_enable_dither()` / `vg_lite_disable_dither()`：开启或关闭抖动功能。

<a id="id8"></a>

### 6.5 路径绘制接口

- `vg_lite_init_path()`：初始化路径对象，配置坐标格式、质量、path 数据长度和 bounding box。
- `vg_lite_init_arc_path()`：初始化弧线路径对象。
- `vg_lite_get_path_length()`：根据 path opcode 数组计算命令 buffer 所需大小。
- `vg_lite_append_path()`：根据 opcode 和坐标数据生成 path 命令。
- `vg_lite_upload_path()`：将 path 上传到 GPU 内存，便于 GPU 直接访问。
- `vg_lite_draw()`：将 path 按指定填充规则、矩阵、混合模式和颜色绘制到目标 buffer。
- `vg_lite_draw_pattern()`：使用图像 pattern 填充 path。
- `vg_lite_set_stroke()`：设置 stroke path 的端点样式、连接样式、线宽、虚线和颜色。
- `vg_lite_update_stroke()`：更新 stroke path 数据。
- `vg_lite_set_path_type()`：设置 path 类型，例如 fill path 或 stroke path。
- `vg_lite_clear_path()`：清除 path 对象属性并释放内部 path 资源。
- `vg_lite_split_path()`：开启或关闭特定 VG core 的 path split workaround。

<a id="id9"></a>

### 6.6 渐变绘制接口

- `vg_lite_init_grad()` / `vg_lite_clear_grad()`：初始化或清除线性渐变对象。
- `vg_lite_set_grad()`：设置普通线性渐变的颜色和 stop。
- `vg_lite_update_grad()`：更新普通线性渐变对象。
- `vg_lite_get_grad_matrix()`：获取普通线性渐变矩阵。
- `vg_lite_draw_grad()`：使用普通线性渐变绘制 path。
- `vg_lite_set_linear_grad()`、`vg_lite_update_linear_grad()`、`vg_lite_clear_linear_grad()`：设置、更新和清除扩展线性渐变。
- `vg_lite_get_linear_grad_matrix()`：获取扩展线性渐变矩阵。
- `vg_lite_draw_linear_grad()`：使用扩展线性渐变绘制 path。
- `vg_lite_set_radial_grad()`、`vg_lite_update_radial_grad()`、`vg_lite_clear_radial_grad()`：设置、更新和清除径向渐变。
- `vg_lite_get_radial_grad_matrix()`：获取径向渐变矩阵。
- `vg_lite_draw_radial_grad()`：使用径向渐变绘制 path。

<a id="id10"></a>

### 6.7 矩阵与裁剪接口

- `vg_lite_identity()`：加载单位矩阵。
- `vg_lite_translate()`：对矩阵追加平移变换。
- `vg_lite_scale()`：对矩阵追加缩放变换。
- `vg_lite_rotate()`：对矩阵追加旋转变换。
- `vg_lite_get_transform_matrix()`：根据四个源坐标和四个目标坐标生成 3x3 变换矩阵。
- `vg_lite_set_scissor()`：设置并启用渲染目标裁剪矩形，传入 `-1,-1,-1,-1` 可关闭裁剪。
- `vg_lite_scissor_rects()`：在 mask layer 上设置多个裁剪矩形。
- `vg_lite_enable_scissor()` / `vg_lite_disable_scissor()`：开启或关闭裁剪矩形功能。

<a id="mask-layer-flexa"></a>

### 6.8 像素效果、Mask Layer 与 Flexa 接口

- `vg_lite_set_pixel_matrix()`：设置 ARGB 像素通道变换矩阵。
- `vg_lite_gaussian_filter()`：设置 3x3 高斯滤波权重。
- `vg_lite_set_mirror()`：设置镜像方向。
- `vg_lite_set_gamma()`：设置 gamma 转换。
- `vg_lite_enable_color_transform()` / `vg_lite_disable_color_transform()`：开启或关闭颜色变换。
- `vg_lite_set_color_transform()`：设置每个颜色通道的 scale 和 bias。
- `vg_lite_enable_masklayer()` / `vg_lite_disable_masklayer()`：开启或关闭 mask layer 功能。
- `vg_lite_create_masklayer()`、`vg_lite_set_masklayer()`、`vg_lite_destroy_masklayer()`：创建、设置和销毁 mask layer。
- `vg_lite_fill_masklayer()`：填充 mask layer 的指定矩形区域。
- `vg_lite_blend_masklayer()`：按指定操作混合两个 mask layer。
- `vg_lite_render_masklayer()`：将 path 渲染到 mask layer。
- `vg_lite_flexa_set_stream()`：设置 Flexa stream ID。
- `vg_lite_flexa_bg_buffer()`：设置 Flexa 背景 buffer 及分段参数。
- `vg_lite_flexa_enable()` / `vg_lite_flexa_disable()`：开启或关闭 Flexa。
- `vg_lite_flexa_stop_frame()`：设置最后一帧后的 Flexa 停止标记。

<a id="id11"></a>

### 6.9 调试接口

- `vg_lite_dump_command_buffer()`：dump 当前 command buffer，便于调试 GPU 命令。
- `vg_lite_dump_png()`：将 `vg_lite_buffer_t` 图像 dump 为 PNG 文件，当前主要用于 Linux 调试环境。
- `vg_lite_get_parameter()`：读取 VGLite 参数数组。

<a id="id12"></a>

## 7\. 使用示例

```
bk_gpu_ctlr_config_t gpu_cfg = {0};

gpu_cfg.tess_width = 128;
gpu_cfg.tess_height = 128;
gpu_cfg.src_width = src_width;
gpu_cfg.src_height = src_height;
gpu_cfg.dst_width = dst_width;
gpu_cfg.dst_height = dst_height;
gpu_cfg.src_format = BK_PIXEL_FORMAT_NV12;
gpu_cfg.dst_format = BK_PIXEL_FORMAT_RGB565;
gpu_cfg.rotate_degree = 0;
gpu_cfg.src_buffer = src_buffer;
gpu_cfg.scale = true;
gpu_cfg.compress = false;
gpu_cfg.flexa = true;
gpu_cfg.flexa_lines = 16;
gpu_cfg.flexa_buff_cnt = 2;
gpu_cfg.frame_malloc = frame_malloc;
gpu_cfg.frame_free = frame_free;
gpu_cfg.frame_done = frame_done;

bk_gpu_ctlr_handle_t gpu = NULL;
avdk_err_t ret = bk_gpu_ctlr_new(&gpu, &gpu_cfg);
if (ret != AVDK_ERR_OK) {
    return ret;
}

ret = bk_gpu_init(gpu);
if (ret != AVDK_ERR_OK) {
    bk_gpu_delete(gpu);
    return ret;
}

ret = bk_gpu_open(gpu);
if (ret != AVDK_ERR_OK) {
    bk_gpu_deinit(gpu);
    bk_gpu_delete(gpu);
    return ret;
}

/* GPU is running. Configure draw path, blit, or ioctl here. */

bk_gpu_close(gpu);
bk_gpu_deinit(gpu);
bk_gpu_delete(gpu);
```
