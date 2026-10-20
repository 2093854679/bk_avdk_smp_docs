---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/camera/mipi_csi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="mipi-csi"></a>

# MIPI CSI 摄像头

<a id="id1"></a>

## 1\. 概述

MIPI CSI 摄像头通过 MIPI CSI-2 接口连接 Sensor，数据经 ISP（Image Signal Processor）处理后输出 NV12/YUV 等格式，适用于高分辨率预览、编码及 AI 推理场景。

数据通路：**Sensor → MIPI CSI → ISP → 应用层（显示 / 编码 / NN）**

- 示例工程：`projects/multimedia/isp_example`
- API 参考：[Camera API](../../api-reference/multimedia/bk_camera.md)

<a id="id2"></a>

## 2\. 支持外设

<a id="sensor"></a>

### 2.1 已适配 Sensor

参考文件路径：`ap/components/bk_peripheral/src/csi`

| 型号 | 最大分辨率 | 默认分辨率 |
| --- | --- | --- |
| GC2053 | 1920×1080 | 1920×1080 |
| GC4653 | 1280×720 | 1280×720 |
| OV2775 | 1280×720 | 1280×720 |
| F58 | 1920×1080 | 1920×1080 |
| CV2005 | 1920×1080 | 1920×1080 |
| SC3336 | 2304×1296 | 2304×1296 |
| SC4336 | 2560×1440 | 2560×1440 |

备注

各 Sensor 实际支持的分辨率与帧率以 `bk_camera_sensor_query_support_formats()` 查询结果为准。

<a id="gpio"></a>

### 2.2 硬件接口与 GPIO

BK7259 默认 MIPI CSI 引脚配置（参考 `ap/include/components/bk_camera_configs.h` 及 `isp_example`）：

| 信号 | 默认 GPIO | 说明 |
| --- | --- | --- |
| I2C SCL | GPIO\_69 | Sensor 寄存器配置 |
| I2C SDA | GPIO\_70 | Sensor 寄存器配置 |
| XCLK (MCLK) | GPIO\_59 | Sensor 工作时钟（CLK\_AUXS\_CIS） |
| RESET | GPIO\_71 | Sensor 复位，可按硬件修改 |
| PWDN | 0xFF（未使用） | 按硬件原理图配置 |

备注

MIPI Sensor 需要额外开启 AuxLDO 供电（1.8V iovdd \+ 1.2V dvdd），可通过 `app_mipi_camera_power_enable()` 控制，详见方案工程 `multimedia_device_service`。

<a id="id3"></a>

### 2.3 相关宏定义

| 宏名称 | 说明 |
| --- | --- |
| CONFIG\_ISP | 使能 ISP 模块 |
| CONFIG\_MIPI\_CSI | 使能 MIPI CSI 控制器 |
| CONFIG\_BK\_CAMERA | 使能 Camera 框架 |
| CONFIG\_CSI\_CAMERA | 使能 CSI Camera 子系统 |
| CONFIG\_CSI\_GC2053 等 | 使能对应 Sensor 驱动（见 Kconfig） |

<a id="id4"></a>

## 3\. 调试说明

<a id="id5"></a>

### 3.1 编译与烧录

在 SDK 根目录编译 `isp_example` 工程：

```
cd <SDK_ROOT>
make bk7259 PROJECT=multimedia/isp_example -j$(nproc)
```

烧录后在串口终端执行 CLI 命令进行调试。

<a id="cli"></a>

### 3.2 CLI 命令

**检测 Sensor：**

```
isp detect
```

预期输出：在 MIPI CSI 端口检测到 Sensor，并打印支持的分辨率与帧率列表。

**打开 MIPI 采集（MP 主通道，Frame 模式）：**

```
isp open mipi mp <sensor_w> <sensor_h> <fps> <out_w> <out_h> frame [output_fmt]
```

常用示例（GC2053 默认 1920×1080@20fps，输出 NV12）：

```
isp open mipi mp 1920 1080 20 1920 1080 frame
isp open mipi mp 1920 1080 20 1280 720 frame
```

**打开 SP 副通道（画中画 / 缩略图）：**

```
isp open mipi sp 1920 1080 20 640 480 frame
```

**关闭通道：**

```
isp close mp
isp close sp
```

**读取一帧（调试用）：**

```
isp read mp
```

<a id="id6"></a>

### 3.3 常见问题排查

| 现象 | 排查建议 |
| --- | --- |
| `isp detect` 无 Sensor | 检查 AuxLDO 供电、RESET/XCLK GPIO、I2C 引脚与 Sensor 型号宏 |
| 打开失败（分辨率不支持） | 用 `isp detect` 确认 Sensor 支持的分辨率，勿使用放大输出 |
| 图像异常 / 无帧中断 | 确认 `CONFIG_ISP`、`CONFIG_MIPI_CSI` 已开启；检查 MCLK |
| I2C 通信失败 | 确认 I2C 引脚未被其他外设占用；检查 Sensor I2C 地址 |
| CV2005 有效画面上方叠加大片粉红色矩形框 | Sensor 供电电压不对。CV2005 要求 IOVDD 接 2.8V、DVDD 接 1.8V；BK7259 开发板 可通过 MIPI Sensor 接口下的跳线帽选择：CSI\_IOVDD 接 2.8V、CSI\_DVDD 接 1.8V |

更完整的测试用例见工程内 `projects/multimedia/isp_example/ISP_TEST_CASES.md`。

<a id="id7"></a>

## 4\. 适配新 Sensor

1. 在 `ap/components/bk_peripheral/src/csi/` 下参考 `csi_gc2053.c` 添加驱动文件，实现初始化表、分辨率表及 ISP 校准参数。
2. 在 `csi/Kconfig` 和 `csi/config.cmake` 中注册新 Sensor 宏。
3. 使用 `BK_CAMERA_SENSOR_DETECT_SECTION(xxx_detect, CSI_CAMERA_PORT)` 注册自动检测函数。
4. 在 menuconfig 中开启 `CONFIG_CSI_CAMERA` 及对应 Sensor 宏后重新编译。

Sensor 寄存器表需向模组厂商索取；ISP 校准参数（`xxx_calib.h`）需根据 Sensor 特性配置。

<a id="id8"></a>

## 5\. 使用流程概要

MIPI CSI 典型初始化流程：

1. 开启 MIPI Sensor 电源（AuxLDO）
2. 创建并 enable Camera Bus（`CSI_CAM_BUS_I2C1_8BIT_2000TIMEOUT()`）
3. 自动检测 Sensor（`bk_camera_sensor_auto_detect()`，端口 `CSI_CAMERA_PORT`）
4. 创建 ISP Camera 控制器并初始化端口（`bk_isp_camera_dev_init()` / `bk_isp_camera_port_init()`）
5. 打开 MP/SP 通道（`bk_isp_camera_channel_open()`）
6. 读取帧或送入显示/编码模块

详细 API 说明请参阅 [Camera API](../../api-reference/multimedia/bk_camera.md) 及 `isp_example` 源码 `isp_func_test.c`。
