---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/camera/dvp.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="dvp"></a>

# DVP 摄像头

<a id="id1"></a>

## 1\. 概述

DVP（Digital Video Port）为并行摄像头接口，Sensor 通过 PCLK/HSYNC/VSYNC 及 8bit 数据线输出 YUV422 原始数据，可经硬件 JPEG/H264 编码器直接编码，也可经 ISP 处理后输出。

- 示例工程：`projects/multimedia/isp_example`
- API 参考：[Camera API](../../api-reference/multimedia/bk_camera.md)
- 图像内存管理：[图像内存管理](../../api-reference/multimedia/bk_frame_buffer.md)

<a id="id3"></a>

## 2\. 支持外设

<a id="sensor"></a>

### 2.1 已适配 Sensor

参考文件路径：`ap/components/bk_peripheral/src/dvp`

| 型号 | 最大分辨率 |
| --- | --- |
| GC0308 | 640×480 |
| GC0328C | 640×480 |
| GC2145 | 1280×720 |
| HM1055 | 1280×720 |
| OV2640 | 1280×720 |
| SC101 | 1280×720 |

<a id="gpio"></a>

### 2.2 硬件接口与 GPIO

BK7259 DVP 引脚为固定映射（参见 `gpio_map.h` 及 `usr_gpio_cfg.h` 中 JPEG-DVP 功能表）：

| 信号 | GPIO | 说明 |
| --- | --- | --- |
| MCLK (XCLK) | GPIO\_27 | Sensor 工作时钟（JPEG\_MCLK） |
| PCLK | GPIO\_29 | 像素时钟（JPEG\_PCLK） |
| HSYNC | GPIO\_30 | 行同步（JPEG\_HSYNC） |
| VSYNC | GPIO\_31 | 场同步（JPEG\_VSYNC） |
| DATA\[7:0\] | GPIO\_32\~39 | 8bit 并行数据（JPEG\_PXDATA0\~7） |
| I2C SCL | GPIO\_0 | Sensor 寄存器配置 |
| I2C SDA | GPIO\_1 | Sensor 寄存器配置 |
| RESET | GPIO\_13 | Sensor 复位（可按硬件修改） |
| 电源控制 | 可配置 GPIO | DVP VDD GPIO（见 CONFIG\_DVP\_CTRL\_POWER\_GPIO\_ID） |

备注

DVP 引脚属于芯片固定功能映射，不可随意更改到其他 GPIO。若需修改 I2C 或控制引脚，请在工程配置中覆盖默认值。

<a id="id4"></a>

## 3\. 调试说明

<a id="isp"></a>

### 3.1 ISP 模式调试（推荐）

使用 `isp_example` 工程，通过 CLI 验证 DVP Sensor 与 ISP 通路：

```
cd <SDK_ROOT>
make bk7259 PROJECT=multimedia/isp_example -j$(nproc)
```

串口命令：

```
isp detect
isp open dvp mp 1280 720 30 1280 720 frame
isp close mp
```

默认 DVP Sensor 参数为 1280×720@30fps。更多用例见 `projects/multimedia/isp_example/ISP_TEST_CASES.md`。

<a id="api"></a>

### 3.2 API 分步调试

除 `isp` 高层命令外，`isp_example` 还提供 `isp_api` 子命令用于分步调用 ISP Camera API（详见工程源码 `isp_func_test.c`）。调试要点：

- 确认 `CONFIG_DVP_CAMERA`、`CONFIG_ISP` 及对应 Sensor 宏已开启
- 上电前拉高电源控制 GPIO（`CONFIG_DVP_CTRL_POWER_GPIO_ID`）
- 先用 `isp detect` 确认 DVP 端口 Sensor 已被检测到
- 通过日志确认 `bk_camera_sensor_auto_detect()` 返回非 NULL

<a id="id5"></a>

### 3.3 常见问题排查

| 现象 | 排查建议 |
| --- | --- |
| Sensor 检测失败 | 检查 I2C 引脚、电源 GPIO、RESET 时序及 Sensor 宏配置 |
| 图像花屏 / 偏色 | 确认 YUV 顺序（YUYV/UYVY 等）与 Sensor 输出一致 |
| 无帧输出 | 检查 MCLK 是否输出、VSYNC/HSYNC 极性配置是否正确 |
| 编码帧损坏 | 回调中避免长时间处理；检查帧缓冲区大小是否足够 |

<a id="id6"></a>

## 4\. 支持的功能

> 1、支持最大分辨率1280X720输入（输出）；
>
> 2、只支持Sensor输出标准YUV422数据格式(大端模式)：YUYV/UYVY/YYUV/UVYY；
>
> 3、默认VSYNC/HSYNC输入高有效，且支持翻转
>
> 4、支持直接输出YUV422数据到BUFF；
>
> 5、支持直接输出JPEG编码数据，或YUV422\&JPEG数据分别到BUFF；
>
> 6、支持直接输出H264编码数据，或YUV422\&H264数据分别到BUFF；
>
> 7、支持动态调节编码码率（JPEG或H264）;
>
> 8、支持H264编码任意时刻重新生成IDR帧
>
> 9、支持Sensor数据接收错误检测
>
> 用户需要根据自己的应用方案，通过配置参数的方式，打开对应的功能

<a id="id7"></a>

## 5\. 相关宏定义

> | Marco name | info |
> | --- | --- |
> | CONFIG\_DVP\_CAMERA | enable dvp sensor function or not |
> | CONFIG\_DVP\_CAMERA\_I2C\_ID | config dvp sensor communicate i2c id |
> | CONFIG\_DVP\_CTRL\_POWER\_GPIO\_ID | config the gpio id of control dvp vdd |
> | CONFIG\_JPEG\_FRAME\_SIZE | config a jpeg frame size |
> | CONFIG\_H264\_FRAME\_SIZE | config a h264 frame size |
> | CONFIG\_DVP\_GC0308 | enable gc0308 sensor function or not |
> | CONFIG\_DVP\_HM1055 | enable hm1055 sensor function or not |
> | CONFIG\_DVP\_OV2640 | enable ov2640 sensor function or not |
> | CONFIG\_DVP\_SC101 | enable sc101 sensor function or not |
> | CONFIG\_DVP\_GC0328C | enable gc0328c sensor function or not |
> | CONFIG\_DVP\_GC2145 | enable gc2145 sensor function or not |

备注

上面的sensor宏是已经适配好了，用户可以直接使用。都默认开启的，其他宏需要用户在编译时自己开启。但是会依赖CONFIG\_DVP\_CAMERA宏，所以需要用户在编译时自己开启。

<a id="id8"></a>

## 6\. 适配新 Sensor

1. 在 `ap/components/bk_peripheral/src/dvp/` 下参考 `dvp_gc2145.c` 添加驱动，实现寄存器初始化表及 `bk_camera_dvp_sensor_t` 操作函数集。
2. Sensor 分辨率/帧率通过寄存器表配置，通常包含初始化表、帧率表、分辨率表（需向模组厂商索取）。
3. 使用检测注册宏将驱动加入自动发现列表：

```
avdk_err_t gc2145_detect(bk_camera_sensor_handle_t *handle,
                         bk_camera_sensor_config_t *config);
BK_CAMERA_SENSOR_DETECT_SECTION(gc2145_detect, DVP_CAMERA_PORT);
```

4. 在 `dvp/Kconfig` 和 `dvp/config.cmake` 中注册新 Sensor 宏，menuconfig 开启后重新编译。
5. 检测函数段默认由链接脚本 `.camera_sensor_detect_function_list` 收集，自定义 ld 文件时需保留该段。

<a id="id9"></a>

## 7\. 使用流程（ISP 模式）

当前 DVP 采集通过 ISP 框架实现，参考 `projects/multimedia/isp_example/ap/src/isp_func_test.c` 中 `isp_init_dvp_camera()`。

<a id="id10"></a>

### 7.1 初始化流程

```
创建 Bus → 使能 Bus → 自动检测 Sensor → 创建 ISP 控制器
→ dev_init → port_init → channel_open → 读帧/显示
```

<a id="id11"></a>

### 7.2 关键代码示例

```
// 1. 创建并使能 Camera Bus
bk_camera_bus_config_t bus_config = (bk_camera_bus_config_t)DVP_CAM_BUS_I2C1_8BIT_2000TIMEOUT();
bk_camera_sensor_config_t sensor_config = {
    .pin_reset = GPIO_13,
    .pin_pwdn = 0xFF,
    .pin_xclk = GPIO_27,
};
bus = bk_camera_bus_new(&bus_config);
bk_camera_bus_enable(bus);

// 2. 自动检测 DVP Sensor
sensor_config.bus = bus;
sensor_handle = bk_camera_sensor_auto_detect(&sensor_config, DVP_CAMERA_PORT);

// 3. 配置 ISP 端口
bk_isp_camera_ctlr_config_t isp_cfg = CAM_DVP_DEFAULT_RAW8_CONFIG(width, height, fps);
isp_cfg.sensor_object = bk_camera_sensor_get_sensor_object(sensor_handle);
bk_camera_isp_ctlr_new(&camera_ctlr_handle);
bk_isp_camera_dev_init(camera_ctlr_handle);
bk_isp_camera_port_init(camera_ctlr_handle, &isp_cfg);

// 4. 打开 MP 通道
bk_isp_camera_channel_config_t ch_cfg = CAM_MP_NV12_RB_INSTANCE_CONFIG(out_w, out_h);
bk_isp_camera_channel_open(camera_ctlr_handle, ISP_MP_CHN_ID, &ch_cfg);
```

<a id="id12"></a>

### 7.3 关闭与释放

```
bk_isp_camera_channel_close(camera_ctlr_handle, ISP_MP_CHN_ID);
bk_isp_camera_deinit(camera_ctlr_handle);
bk_isp_camera_delete(camera_ctlr_handle);
bk_camera_sensor_destroy(sensor_handle);
bk_camera_bus_disable(bus);
bk_camera_bus_delete(bus);
```

相关头文件：

- `ap/include/components/bk_camera_sensor.h`
- `ap/include/components/bk_camera_bus.h`
- `ap/include/components/bk_camera_configs.h`
- `ap/include/components/bk_isp_camera.h`

<a id="id13"></a>

## 8\. DVP 应用方案

因为DVP支持输出各种格式的数据，所以需要用户根据自己的需求，选择合适的输出格式。

1.DVP直接输出YUV图像，联合显示模块进行显示。
2.DVP直接输出MJPEG图像，再联合WiFi模块进行图传。
3.DVP直接输出H264图像，再联合WiFi模块进行图传。
4.DVP直接输出MJPEG\&YUV图像，再联合WiFi模块进行图传，联合显示模块进行显示。
5.DVP直接输出H264\&YUV图像，再联合WiFi模块进行图传，联合显示模块进行显示。
