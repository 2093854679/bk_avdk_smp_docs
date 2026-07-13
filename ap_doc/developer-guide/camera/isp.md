# ISP 图像信号处理



## 1. 概述

ISP（Image Signal Processor，图像信号处理器）是 MIPI CSI / DVP Sensor 采集通路中的图像处理核心。
Sensor 输出的原始数据（RAW / BT656 / BT601）经 ISP 完成去坏点、黑电平、去马赛克、自动曝光（AE）、
自动白平衡（AWB）、色彩校正、降噪、缩放等处理后，输出 NV12/YUV 等可直接用于显示、编码或 AI 推理的图像格式。

BK7259 的 ISP 由 `bk_camera` 组件中的 **ISP Camera 控制器**
（`bk_isp_camera_*` 系列接口）统一封装，向上层提供与接口类型（CSI / DVP）无关的采集 API。

数据通路：**Sensor → MIPI CSI / DVP → ISP → MP / SP 双通道 → 应用层（显示 / 编码 / NN）**


- 示例工程：`projects/multimedia/isp_example`

- 组件路径：`ap/components/bk_camera`

- API 参考：[Camera API](../../api-reference/multimedia/bk_camera.md "../../api-reference/multimedia/bk_camera.md")


## 2. 架构与组件结构

ISP Camera 控制器是对底层 ISP 驱动的面向对象封装：上层通过统一的 `bk_camera_ctlr_t` 操作表
（`dev_init` / `port_init` / `channel_open` / `open` / `read` / `close` 等函数指针）
调用 ISP，无需直接操作底层 ISP 寄存器。

`bk_camera` 组件中与 ISP 相关的主要源码：


- `src/bk_isp_camera.c` —— ISP Camera 公共 API 入口，转发到控制器操作表

- `src/isp/bk_camera_isp_ctlr_default.c` —— 默认 ISP 控制器实现（dev/port/channel/open/read 等）

- `include/isp_camera_ctlr.h` —— 控制器内部状态机（`CAM_FSM_INIT` / `CAM_FSM_ENABLE`）

- `src/utils/isp_camera_utils.c` —— ISP 像素格式 / 分辨率 / 属性转换辅助函数

- `src/isp_frame/` —— ispFrame 帧抓取会话（JSON-RPC，可选）

对外头文件：


- `ap/include/components/bk_isp_camera.h` —— ISP Camera 采集 API

- `ap/include/components/bk_camera_isp_ctlr.h` —— ISP 控制器配置类型与 `bk_camera_isp_ctlr_new()`

- `ap/include/components/bk_isp_camera_types.h` —— 通道配置、ISR 类型、Sensor ID 等公共类型


## 3. 双通道（MP / SP）

ISP 硬件提供两个输出端口（`ISP_PORT_CNT = 2`），在 `bk_camera` 中以通道（channel）形式暴露：


- **MP（Main Port，主通道）** —— 主码流：全分辨率预览 / 编码

- **SP（Sub Port，副通道）** —— 子码流：缩略图 / 画中画 / AI 推理小图

两个通道可独立配置分辨率、像素格式与工作模式，并可同时输出，实现“一路高分辨率编码 + 一路小图推理”的常见组合。


## 4. 关键配置类型


### 4.1 控制器配置 `bk_isp_camera_ctlr_config_t`

定义于 `bk_camera_isp_ctlr.h`，描述 ISP 输入侧（Sensor → ISP）的属性：


- `port_id` —— ISP 端口号

- `width` / `height` —— 输入图像宽 / 高

- `input_type` —— 输入源类型：`BK_ISP_INPUT_TYPE_CSI_SENSOR` / `BK_ISP_INPUT_TYPE_DVP_SENSOR`

- `isp_mode` —— 时序模式：`BK_ISP_MODE_BT656` / `BK_ISP_MODE_BT601` / `BK_ISP_MODE_RAW`

- `hdr_mode` —— HDR 模式（见 4.3）

- `input_pixel_fmt` —— 输入像素格式（`bk_pixel_format_t`）

- `clk` —— Sensor / ISP 工作时钟

- `input_rect` / `input_crop` —— 输入区域与裁剪区域

- `fps` —— 帧率

- `sensor_object` —— 关联的 Sensor 对象指针


### 4.2 通道配置 `bk_isp_camera_channel_config_t`

定义于 `bk_isp_camera_types.h`，描述 ISP 输出侧（ISP → 通道）的属性：


- `buf_cnt` —— 帧缓冲数量

- `port_id` —— 端口号（对应 MP / SP）

- `enable_flexa` —— 是否使能 Flexa：0 - 关闭，1 - 开启

- `work_mode` —— 工作模式：0 - Frame 帧模式，1 - SFW Flexa 模式

- `width` / `height` —— 输出图像宽 / 高

- `format` —— 输出像素格式

备注


**Frame 模式**：ISP 输出完整帧到帧缓冲，应用层主动读取，适合编码 / 抓帧 / 推理。

**Flexa（SFW）模式**：与编码模块流水线直连，由硬件按行推进，降低时延与内存占用；该模式下不支持
`bk_isp_camera_read()` 主动读帧。


### 4.3 HDR 模式


- `BK_ISP_HDR_MODE_LINEAR` —— 线性模式（非 HDR），默认

- `BK_ISP_HDR_MODE_ISP_STICH` —— ISP 端多帧合成 HDR

- `BK_ISP_HDR_MODE_SENSOR_STICH` —— Sensor 端合成 HDR（ISP 接收已合成数据）


## 5. 相关宏定义

| 宏名称 | 说明 |
| --- | --- |
| CONFIG_BK_CAMERA | 使能 Camera 框架（`bk_camera`） |
| CONFIG_ISP | 使能 ISP 模块 |
| CONFIG_MIPI_CSI | 使能 MIPI CSI 控制器（CSI 输入） |
| CONFIG_CSI_CAMERA | 使能 CSI Camera 子系统 |
| CONFIG_ISP_FRAME_SESSION | 使能 ispFrame 帧抓取会话（依赖网络传输模块） |


## 6. API 调用流程

ISP Camera 典型生命周期（参考 `isp_example` 的 `isp_func_test.c`）：


```
bk_isp_camera_ctlr_handle_t handle = NULL;

/* 1. 创建 ISP 控制器 */
bk_camera_isp_ctlr_new(&handle);

/* 2. 初始化 ISP 设备（时钟、ISP 核） */
bk_isp_camera_dev_init(handle);

/* 3. 配置输入端口（Sensor → ISP），传入 bk_isp_camera_ctlr_config_t */
bk_isp_camera_port_init(handle, &ctlr_config);

/* 4. 打开输出通道（MP / SP），传入 bk_isp_camera_channel_config_t */
bk_isp_camera_channel_open(handle, channel, &chnl_config);

/* 5. 注册帧中断回调，开始出图 */
bk_isp_camera_register_isr_callback(handle, ISR_TYPE_FRAME_COMPLETE, cb, arg);
bk_isp_camera_open(handle, parameter);

/* 6. Frame 模式下主动读取一帧 */
bk_isp_camera_read(handle, id, frame, size, timeout);

/* 7. 反初始化与释放 */
bk_isp_camera_close(handle);
bk_isp_camera_channel_close(handle, channel);
bk_isp_camera_deinit(handle);
bk_isp_camera_delete(handle);

```

核心 API 一览：


- 创建 / 销毁：`bk_camera_isp_ctlr_new` / `bk_isp_camera_delete`

- 设备与端口：`bk_isp_camera_dev_init` / `bk_isp_camera_port_init` / `bk_isp_camera_port_change` / `bk_isp_camera_deinit`

- 通道：`bk_isp_camera_channel_open` / `bk_isp_camera_channel_close` / `bk_isp_camera_channel_state_get`

- 数据流：`bk_isp_camera_open` / `bk_isp_camera_close` / `bk_isp_camera_read`

- 中断：`bk_isp_camera_register_isr_callback` / `bk_isp_camera_deregister_isr_callback`

- 其他：``` bk_isp_camera_ctlr_ioctl``（如 ``BK_CAM_IOCTL_SOFTRESET ``` 软复位）


### 6.1 中断回调类型

| ISR 类型 | 触发时机 |
| --- | --- |
| `ISR_TYPE_16LINE_DONE` | 每完成 16 行输出（适合行级流水 / 低时延） |
| `ISR_TYPE_FRAME_COMPLETE` | 完成一整帧输出 |

回调原型：`void (*bk_camera_isr_t)(uint32_t seqence, uint32_t line, uint8_t chnl, uint8_t error, void *param)`。


## 7. 调试说明


### 7.1 编译与烧录

在 SDK 根目录编译 `isp_example` 工程：


```
cd <SDK_ROOT>
make bk7259 PROJECT=multimedia/isp_example -j$(nproc)

```

烧录后在串口终端执行 CLI 命令进行调试。


### 7.2 CLI 命令


**检测 Sensor：**


```
isp detect

```


**打开采集通道**（`mipi` / `dvp` 选择输入，`mp` / `sp` 选择通道，`frame` / `flexa` 选择工作模式）：


```
isp open <mipi|dvp> <mp|sp> <sensor_w> <sensor_h> <fps> <out_w> <out_h> <frame|flexa> [output_fmt]

```

常用示例：


```
isp open mipi mp 1920 1080 20 1920 1080 frame
isp open mipi sp 1920 1080 20 640 480 frame
isp open dvp  mp 1280 720  30 1280 720  frame

```


**关闭通道 / 读取一帧：**


```
isp close mp
isp close sp
isp read mp

```

更完整的测试用例见工程内 `projects/multimedia/isp_example/ISP_TEST_CASES.md`。


### 7.3 常见问题排查


- **ISP 初始化失败** —— 确认 `CONFIG_BK_CAMERA` 与 `CONFIG_ISP` 已开启。

- **图像异常 / 偏色** —— 检查 `isp_mode` 与 Sensor 输出时序是否匹配；确认 ISP 校准参数与 Sensor 对应。

- **打开失败（分辨率不支持）** —— 用 `isp detect` 确认 Sensor 支持的分辨率，输出分辨率不应放大超过输入。

- **Flexa 模式读帧失败** —— Flexa（SFW）模式与编码流水线直连，不支持 `bk_isp_camera_read()`，改用 Frame 模式。

- **无帧中断** —— 确认已 `register_isr_callback` 并调用 `bk_isp_camera_open`；检查 MCLK。


## 8. ispFrame 帧抓取会话（可选）

当开启 ``` CONFIG_ISP_FRAME_SESSION``（依赖 ``BK_NTWK_TRANSFER ``` 网络传输模块）时，`bk_camera` 提供
`src/isp_frame/` 下的帧抓取会话：通过 JSON-RPC 控制（方法与 H264E 一致），VIDEO 通道按 NV12/YUV
推送图像帧，便于在 PC 端实时抓取 ISP 原始/处理后图像，用于调试与画质评估。


## 9. 参考资料


- [Camera API](../../api-reference/multimedia/bk_camera.md "../../api-reference/multimedia/bk_camera.md")

- [MIPI CSI 摄像头](mipi_csi.md "mipi_csi.md")

- [DVP 摄像头](dvp.md "dvp.md")

- 示例工程源码：``` projects/multimedia/isp_example``（``ap/src/isp_func_test.c ```）

- 组件源码：`ap/components/bk_camera`
