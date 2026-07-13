# GPU 图形加速



## 1. 概述

BK7259 内置 `vg_lite` GPU。在 AVDK 多媒体框架中，应用通常通过 `bk_gpu` 控制器将 GPU 处理接入 Camera、解码器、显示、DPU 或 AI 链路。该控制器负责 Flexa 分行输入、帧内存回调、输出帧通知、旋转、缩放、压缩、路径绘制和图像叠加（blit）。

如果应用需要直接管理 buffer、矩阵、path、渐变或 mask layer，也可以直接调用底层 `vg_lite` 接口。控制器 API 细节请参考 [GPU API Reference](../api-reference/multimedia/bk_gpu.md "../api-reference/multimedia/bk_gpu.md")。

| 能力 | 典型接口 | 典型场景 |
| --- | --- | --- |
| Flexa 分行处理 | `bk_gpu_*` + `BK_GPU_IOCTL_*` | H.264 解码、Camera 或 ISP 分段送入 GPU |
| 缩放 / 旋转 / 压缩 | `bk_gpu_ctlr_config_t` | 生成显示或 DPU 使用的 ARGB 帧 |
| 路径绘制 | `bk_gpu_draw_path_build` / `vg_lite_draw` | 绘制描边、叠加层或简单矢量图形 |
| 图像叠加 | `bk_gpu_blit_set` / `vg_lite_blit` | 将另一幅图像叠加到输出帧 |

组件路径：


- 控制器：`ap/components/bk_gpu/`

- 公共头文件：`ap/include/components/bk_gpu*.h`

- GPU 原生接口头文件：`ap/include/modules/vg_lite_gpu/`

- 参考示例：`projects/multimedia/h264d_gpu_display_example/`


## 2. 配置项

通过 `CONFIG_VG_LITE_GPU` 使能 GPU 组件，该选项依赖 `FREERTOS_FPU_ENABLE`。GPU 驱动还使用以下 Kconfig 配置：


- `CONFIG_VG_LITE_GPU_BASE_ADDRESS`：GPU 硬件基地址。

- `CONFIG_VG_LITE_GPU_CONTIGUOUS_MEM_SZ`：为 GPU 命令和工作 buffer 保留的连续内存大小。

- `CONFIG_VG_LITE_GPU_COMMAND_BUFFER_SIZE`：命令 buffer 大小。

当前默认 `bk_gpu` 控制器要求使用 Flexa 模式。`bk_gpu_init()` 会检查 Flexa 配置、帧内存回调和 GPU 连续内存，并在这些配置满足要求后初始化 `vg_lite`。


## 3. 典型 Flexa 链路

常见实时视频链路如下：


```
H.264D / Camera / ISP
         │
         ▼
Flexa 分段环形缓冲
         │  bk_flexa_bond_* 同步读写指针
         ▼
       GPU
         │
         ▼
压缩 ARGB 帧，送往 DPU / 显示 / 下游模块

```

在该模式下，上游模块将小段行数据写入 HSRAM，GPU 在整帧落入 PSRAM 前即可开始消费。该方式与 VPU Flexa 链路类似，适合视频播放、实时预览等对整帧内存带宽敏感的场景。

典型控制器流程如下：

1. 配置 `bk_gpu_ctlr_config_t`，填入源/目标尺寸、像素格式、旋转、缩放、压缩、Flexa 参数和帧回调。
2. 调用 `bk_gpu_ctlr_new()` 创建控制器。
3. 调用 `bk_gpu_init()` 和 `bk_gpu_open()`。
4. 当上游模块也工作在 Flexa 模式时，注册 Flexa Bond。
5. 根据需要配置路径绘制或 blit 叠加。
6. 退出时按 `bk_gpu_close()`、`bk_gpu_deinit()`、`bk_gpu_delete()` 释放资源。


## 4. 关键参数

`src_width` / `src_height`
:   源图像尺寸。Flexa 链路中应与上游分段流尺寸保持一致。

`dst_width` / `dst_height`
:   输出图像尺寸。当目标尺寸与源尺寸不一致时，需要将 `scale` 设置为 `true`。

`src_format` / `dst_format`
:   像素格式。典型视频链路常使用 NV12 输入、ARGB8888 输出。

`rotate_degree`
:   旋转角度。控制器 blit 路径支持 `0`、`90`、`180`、`270`。

`compress`
:   是否启用压缩输出，常用于将 ARGB 帧送往 DPU 或显示链路前的压缩。

`flexa` / `flexa_lines` / `flexa_buff_cnt`
:   使能 Flexa 模式，并描述每次交换的行数和缓冲区数量。该配置需要与 Flexa Bond 对端保持一致。

`frame_malloc` / `frame_free` / `frame_done`
:   输出帧分配、释放和完成回调。控制器关闭前，这些回调必须一直有效。

`tess_width` / `tess_height`
:   传入 `vg_lite_init()` 的 tessellation 缓冲区尺寸。矢量 path 绘制需要先对 path 数据进行 tessellation，因此使用矢量绘制时需要配置该尺寸。如果应用只使用缩放、旋转、压缩或 blit 等图像处理能力，不使用矢量 path 绘制，则这两个字段可以直接设置为 `0`。


## 5. 路径绘制与图像叠加

应用需要通过控制器叠加简单矢量图形时，可使用 `bk_gpu_draw_path_build()`。该接口配置 command 数据、path 数据、alpha 和颜色。更复杂的矢量能力可直接使用 `vg_lite` path 相关接口。

应用需要在 GPU 输出帧上叠加另一幅图像时，可使用 `bk_gpu_blit_set()`。blit 配置包含源裁剪区域、目标位置、源格式、旋转角度和释放回调。释放回调应保持有效，因为清除或替换叠加图像时，控制器会通过该回调释放已保存的 blit 帧。


## 6. 开发注意事项


- 构建 Flexa 解码到显示链路时，可从 `h264d_gpu_display_example` 开始。该示例包含 H.264 解码、Flexa Bond、GPU 处理、帧池分配以及可选 DPU/显示输出。

- 源和目标 buffer 地址需要保证 GPU 可访问。直接调用 `vg_lite` 时，提交命令后还需要按场景调用 `vg_lite_flush()` 或 `vg_lite_finish()`。

- 如果输出帧分配失败，优先检查 `CONFIG_VG_LITE_GPU_CONTIGUOUS_MEM_SZ` 和帧池大小。

- 链路调试时，先确认宽高、像素格式和旋转配置正确，再逐步开启叠加或 path 绘制等额外能力。
