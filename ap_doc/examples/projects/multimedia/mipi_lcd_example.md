---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/multimedia/mipi_lcd_example/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="mipi-lcd"></a>

# MIPI LCD 示例工程

<a id="id1"></a>

## 1\. 项目概述

本项目用于演示 Beken 平台上的 MIPI DSI 接口 LCD 显示流程。基于 `bk_display_*` 控制器接口，演示显示初始化、帧刷新线程以及像素格式运行时切换。

当前工程提供：

- 上电自动运行的 ARGB8888 显示自检：`mipi_lcd_display_argb8888_test`
- 像素格式运行时切换测试：`mipi_lcd_switch_format` （CLI / `ap_cmd` ）
- 辅助调试命令：`mipi_lcd open | close | switch ...`
- `.it.csv` 集成测试入口

<a id="id2"></a>

### 1.1 测试环境

- 硬件配置：

  > - 核心板， **BK7259\_QF128\_12.3X12.3\_V4.0**
  > - PSRAM 32M
- 默认 MIPI 屏：`hx8399c_mipi_1080x1920` （分辨率 1080x1920）

  > - 上电默认格式：`ARGB8888` （压缩数据）
  > - 支持格式：`RGB565` / `RGB888` / `NV12` / `ARGB8888` （压缩）

警告

请使用参考外设，进行 demo 工程的熟悉和学习。如果外设规格不一样，代码可能需要重新配置。

<a id="id3"></a>

## 2\. 目录结构

项目采用 AP-CP 双核架构，主要源代码位于 AP 目录下。项目结构如下：

```
mipi_lcd_example/
├── CMakeLists.txt        # 项目级 CMake 构建文件
├── Makefile              # Make 构建文件
├── README.md             # 项目说明文档（英文）
├── README_CN.md          # 项目说明文档（中文）
├── app.rst               # 工程说明
├── .it.csv               # 集成测试用例
├── ap/                   # AP 端代码
│   ├── CMakeLists.txt    # AP 端 CMake 构建文件
│   ├── ap_main.c         # AP 主入口、CLI 命令注册、上电 case
│   ├── config/           # AP 配置目录
│   ├── include/
│   │   ├── lcd_example.h # 接口声明
│   │   └── lcd_image.h   # 内置 ARGB8888 压缩图源
│   └── src/
│       └── lcd_example_mipi.c # MIPI 显示开关、刷新线程、两个 IT case
├── cp/                   # CP 端代码
├── partitions/           # 分区配置
└── pj_config.mk          # 项目配置
```

<a id="id4"></a>

## 3\. 功能说明

<a id="id5"></a>

### 3.1 主要功能

- 上电后自动运行 ARGB8888 显示 case
- 提供 `mipi_lcd_switch_format` CLI 命令验证像素格式运行时切换
- 提供 `mipi_lcd` 辅助命令手动开关屏与切换格式
- 使用直接 `malloc -> 填充 -> flush -> 延时` 的刷新线程（无队列）
- 每个 case 显示固定时长后自动关闭，保证用例相互独立
- 提供统一 `[RESULT][PASS]` / `[RESULT][FAIL]` 结果日志

<a id="id6"></a>

### 3.2 测试用例说明

<a id="case-1-argb8888-mipi-lcd-display-argb8888-test"></a>

#### Case 1：上电 ARGB8888 显示（`mipi_lcd_display_argb8888_test` ）

1. 上电时 `main()` 自动调用 `mipi_lcd_argb8888_test()`
2. 以 `ARGB8888` （压缩）打开屏并启动刷新线程
3. 持续刷新约 20s（`MIPI_LCD_CASE_DURATION_MS` ）
4. 自动关闭显示，打印： `[RESULT][PASS] mipi_lcd_display_argb8888_test success`

<a id="case-2-mipi-lcd-switch-format"></a>

#### Case 2：像素格式运行时切换（`mipi_lcd_switch_format` ）

1. 由 CLI / `ap_cmd mipi_lcd_switch_format` 触发
2. 通过 `bk_display_ioctl` 运行时切换格式，顺序为： `RGB565 -> RGB888 -> ARGB8888 -> RGB565`，每档显示约 5s（`MIPI_LCD_SWITCH_STEP_MS`，合计约 20s）
3. 切换完成后自动关闭显示，打印： `[RESULT][PASS]mipi_lcd_switch_format success`

> 说明：`ARGB8888` 按压缩数据处理（`decompress=true` ）。

<a id="id7"></a>

## 4\. 编译与运行

<a id="id8"></a>

### 4.1 编译方法

使用以下命令编译项目：

```
make bk7259 PROJECT=multimedia/mipi_lcd_example
```

<a id="id9"></a>

### 4.2 运行方法

编译完成后，将生成的固件烧录到开发板上。上电后 `main()` 会自动运行 Case 1（ARGB8888 显示）。也可以通过串口终端手动触发以下命令：

命令执行成功打印：”CMDRSP:OK”

命令执行失败打印：”CMDRSP:ERROR”

<a id="cli"></a>

#### 4.2.1 当前 CLI 命令

```
mipi_lcd_switch_format
mipi_lcd open
mipi_lcd close
mipi_lcd switch rgb565|rgb888|nv12|argb8888
```

- `mipi_lcd_switch_format`：依次切换 `RGB565 / RGB888 / ARGB8888` 验证切换 API（IT case）
- `mipi_lcd open` / `close`：手动开 / 关屏
- `mipi_lcd switch <fmt>`：手动切换单个格式（调试用）
- `CMDRSP:OK` 只表示测试线程创建成功，最终是否通过请看 `[RESULT]` 日志

<a id="id10"></a>

## 5\. 测试示例

<a id="argb8888"></a>

### 5.1 上电 ARGB8888 显示测试

设备上电（或发送 `reboot` ）后自动运行，预期最终日志：

```
[RESULT][PASS] mipi_lcd_display_argb8888_test success
```

<a id="id11"></a>

### 5.2 像素格式切换测试

```
ap_cmd mipi_lcd_switch_format
```

预期最终日志：

```
[RESULT][PASS]mipi_lcd_switch_format success
```

<a id="id12"></a>

### 5.3 集成测试命令

`.it.csv` 包含：

```
reboot                           -> [RESULT][PASS] mipi_lcd_display_argb8888_test success
ap_cmd mipi_lcd_switch_format    -> [RESULT][PASS]mipi_lcd_switch_format success
```

<a id="id13"></a>

## 6\. 配置选项

<a id="id14"></a>

### 6.1 显示配置

当前 MIPI 测试使用以下固定配置：

- 默认屏：`hx8399c_mipi_1080x1920`
- 分辨率：`1080 x 1920`
- 上电格式：`BK_PIXEL_FORMAT_ARGB8888` （压缩）
- 支持格式：`RGB565` / `RGB888` / `NV12` / `ARGB8888` （压缩）
- 上电显示保持时长：`MIPI_LCD_CASE_DURATION_MS = 20s`
- 切换每档时长：`MIPI_LCD_SWITCH_STEP_MS = 5s`

<a id="id15"></a>

## 7\. 注意事项

1. 两个 case 互相独立，case 运行结束会自动关闭显示并释放资源；后启动的 case 会抢占前一个。
2. CLI 命令只负责创建测试线程，最终结果以 `[RESULT][PASS]` 或 `[RESULT][FAIL]` 为准。
3. 格式切换通过 `bk_display_ioctl` 运行时完成，期间会先停止刷新线程，切换后再重启刷新。
4. `ARGB8888` 按压缩数据处理，对应的内置图源位于 `ap/include/lcd_image.h`。
5. 帧缓冲资源有限，请避免同时占用过多缓冲区。
