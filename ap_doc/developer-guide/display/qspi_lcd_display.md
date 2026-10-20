---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/display/qspi_lcd_display.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="qspi-lcd-display"></a>

# qspi\_lcd\_display

<a id="id1"></a>

## 概述

Display 模块为不同 LCD 接口提供统一的控制器生命周期。QSPI LCD 使用 `bk_display_qspi_panel_t` 屏描述结构，并通过 QSPI LCD 驱动发送寄存器初始化命令和原始像素帧。

本节说明 BK7259 当前 QSPI LCD 通路的使用方式。QSPI 控制器基础说明见 [QSPI 使用指南](../peripheral/bk_qspi.md)。
API 细节请参考 [Display API](../../api-reference/multimedia/bk_display.md)，可运行示例请参考 `projects/multimedia/qspi_lcd_example`。

<a id="id2"></a>

## 配置项

工程中需要使能 QSPI LCD 通路和具体屏驱动：

- `CONFIG_BK_DISPLAY`：使能 Display 组件。
- `CONFIG_FRAME_BUFFER`：使能帧缓冲区分配接口。
- `CONFIG_BK_PERIPHERAL`：编译 LCD panel 描述。
- `CONFIG_QSPI` 和 `CONFIG_QSPI_LINE_MODE=4`：使能 QSPI 四线模式。
- `CONFIG_LCD_QSPI`：使能 QSPI LCD 驱动。
- `CONFIG_LCD_QSPI_<PANEL>`：使能具体 QSPI panel，例如 `CONFIG_LCD_QSPI_SPD2010`。
- `CONFIG_LCD_QSPI_TE`：当屏和板级硬件连接 TE 引脚时使能 TE 支持。
- `CONFIG_LCD_QSPI_COLOR_DEPTH_BYTE`：输出像素字节数，用于 panel 的 `frame_len`。

背光和电源 GPIO 与具体板级设计相关。SDK 示例使用 GPIO7 作为背光控制脚，实际应用应按硬件设计在打开显示前后自行配置。

<a id="panel"></a>

## Panel 描述

QSPI 屏使用 `bk_display_qspi_panel_t` 描述，并提供 `lcd_qspi_t` 总线配置：

```
static uint8_t spd2010_cmd[] = {0x32, 0x00, 0x2c, 0x00};

static const lcd_qspi_t lcd_qspi_spd2010_config = {
    .clk = LCD_QSPI_48M,
    .refresh_method = LCD_QSPI_REFRESH_BY_FRAME,
    .reg_write_cmd = 0x02,
    .reg_read_cmd = 0x0B,
    .pixel_write_config.cmd = spd2010_cmd,
    .pixel_write_config.cmd_len = sizeof(spd2010_cmd),
    .init_cmd = spd2010_init_cmds,
    .device_init_cmd_len = sizeof(spd2010_init_cmds) / sizeof(lcd_qspi_init_cmd_t),
    .refresh_config = {0},
    .frame_len = 412 * 412 * CONFIG_LCD_QSPI_COLOR_DEPTH_BYTE,
};

const bk_display_qspi_panel_t lcd_device_spd2010 = {
    .name = "spd2010",
    .width = 412,
    .height = 412,
    .qspi = &lcd_qspi_spd2010_config,
};

BK_LCD_PANEL_DEVICE_SECTION(lcd_device_spd2010,
                            "spd2010_qspi_412x412",
                            BK_LCD_PANEL_BUS_QSPI);
```

新增 QSPI 屏时，可参考 `ap/components/bk_peripheral/src/lcd/qspi/` 下已有文件。至少需要确认寄存器读写命令、像素写命令、初始化命令表、像素时钟、刷新模式、有效宽高和 `frame_len`。

<a id="qspi-panel"></a>

### 适配新 QSPI panel

新增一个 QSPI LCD sensor/panel 时，推荐按现有 `lcd_qspi_spd2010.c`、`lcd_qspi_co5300.c` 等文件复制改造。QSPI 屏除了初始化表，还要特别确认寄存器读写命令、像素写命令和 dummy clock 配置是否与屏厂资料一致。

1. 准备屏厂资料

   从屏厂获取初始化寄存器表、分辨率、像素格式、QSPI 最大时钟、reset/TE/背光连接方式、寄存器写命令、寄存器读命令、RAM write 或 pixel write 命令序列，以及读寄存器需要插入的 dummy clock。若屏支持 RGB565，通常 `CONFIG_LCD_QSPI_COLOR_DEPTH_BYTE` 配置为 `2`，同时初始化表中的像素格式寄存器也要设置为 RGB565。
2. 新增 panel 源文件

   在 `ap/components/bk_peripheral/src/lcd/qspi/` 下新增 `lcd_qspi_<name>.c`，并包含下面几个部分：

   - `static const lcd_qspi_init_cmd_t <name>_init_cmds[]`：按屏厂初始化表填写寄存器命令。sleep out、display on 等命令后的延时可参考已有文件中的延时写法。
   - `static uint8_t <name>_cmd[]`：填写整屏写像素时发送的命令序列，例如 SPD2010 使用 `{0x32, 0x00, 0x2c, 0x00}`。
   - `static const lcd_qspi_t lcd_qspi_<name>_config`：填写 `clk`、`refresh_method`、`reg_write_cmd`、`reg_read_cmd`、`reg_read_config`、`pixel_write_config`、`init_cmd`、`device_init_cmd_len` 和 `frame_len`。首版建议先使用保守时钟，点亮稳定后再逐步提高。
   - `const bk_display_qspi_panel_t lcd_device_<name>`：填写 `name`、`width`、`height` 和 `qspi` 指针。

   注册时必须使用 QSPI bus 类型：

   ```
   BK_LCD_PANEL_DEVICE_SECTION(lcd_device_<name>,
                               "<name>_qspi_<width>x<height>",
                               BK_LCD_PANEL_BUS_QSPI);
   ```
3. 增加编译开关

   修改 `ap/components/bk_peripheral/src/lcd/qspi/Kconfig`，新增 `CONFIG_LCD_QSPI_<NAME>`，通常需要 `depends on LCD_QSPI`；再修改 `ap/components/bk_peripheral/src/lcd/qspi/config.cmake`，在该配置打开时把 `lcd_qspi_<name>.c` 加入 `QSPI_LCD_DEVICE_FILES`。
4. 工程中启用新 panel

   在方案工程配置中打开 `CONFIG_BK_DISPLAY`、`CONFIG_FRAME_BUFFER`、`CONFIG_BK_PERIPHERAL`、`CONFIG_QSPI`、`CONFIG_QSPI_LINE_MODE=4`、`CONFIG_LCD_QSPI` 和 `CONFIG_LCD_QSPI_<NAME>`。应用侧将 `extern const bk_display_qspi_panel_t lcd_device_spd2010` 替换为新符号 `lcd_device_<name>`，并按板级原理图配置 `qspi_id`、`reset_pin`、`te_pin`、背光和电源 GPIO。
5. 首屏调试顺序

   先确认 reset、背光和电源时序，再确认 QSPI 四线模式、时钟、初始化命令和 pixel write 命令是否有波形输出。若有背光但黑屏，重点检查 `0x11` sleep out、`0x29` display on、寄存器写命令、RAM write 命令序列和窗口范围；若花屏或颜色异常，重点检查 `CONFIG_LCD_QSPI_COLOR_DEPTH_BYTE`、像素格式寄存器、RGB/BGR 方向寄存器、`frame_len` 和 `refresh_method`。

<a id="id3"></a>

## 代码流程

<a id="id4"></a>

### 1\. 创建控制器

使用 `bk_display_qspi_ctlr_new()` 创建 QSPI display 控制器。`lcd_panel` 必须指向有效的 QSPI `bk_display_qspi_panel_t` 描述，且其 `qspi` 成员不能为空。

```
extern const bk_display_qspi_panel_t lcd_device_spd2010;

static bk_display_ctlr_handle_t lcd_display_handle = NULL;
static bk_display_qspi_ctlr_config_t qspi_ctlr_config = {
    .lcd_panel = &lcd_device_spd2010,
    .qspi_id = 0,
    .reset_pin = GPIO_40,
    .te_pin = GPIO_41,
};

avdk_err_t ret = bk_display_qspi_ctlr_new(&lcd_display_handle, &qspi_ctlr_config);
```

`te_pin` 仅在使能 TE 并且硬件已连接 TE 引脚时使用。如果方案不使用 TE，应在板级配置中保持该引脚未使用，并避免开启依赖 TE 的行为。

<a id="id5"></a>

### 2\. 初始化并打开

调用 `bk_display_open()` 前需要先调用 `bk_display_init()`。初始化阶段会配置 QSPI LCD 通路，open 后控制器进入可刷帧状态。

```
ret = bk_display_init(lcd_display_handle);
if (ret != AVDK_ERR_OK) {
    goto fail;
}

ret = bk_display_open(lcd_display_handle);
if (ret != AVDK_ERR_OK) {
    goto fail;
}
```

<a id="id6"></a>

### 3\. 刷新帧

QSPI 控制器的 `bk_display_flush()` 参数是与 panel 配置匹配的原始像素 buffer。buffer 大小可按 `lcd_panel->qspi->frame_len` 或 `width * height * CONFIG_LCD_QSPI_COLOR_DEPTH_BYTE` 分配。

```
uint32_t frame_size = qspi_ctlr_config.lcd_panel->qspi->frame_len;
uint8_t *disp_frame = bk_frame_buffer_malloc(MEM_SLAB_HEAP_CODED, frame_size);

ret = bk_display_flush(lcd_display_handle, disp_frame, display_frame_free_cb);
if (ret != AVDK_ERR_OK) {
    display_frame_free_cb(disp_frame);
}
```

可选回调会在控制器不再使用该帧时被调用。如果使用固定复用 buffer，回调可以为空实现；如果每帧单独分配，应在回调中释放。

<a id="id7"></a>

### 4\. 关闭和删除

使用 `bk_display_close()` 停止输出。如果后续还要重新初始化，可调用 `bk_display_deinit()`；如果需要释放句柄，调用 `bk_display_delete()`。`bk_display_delete()` 会在控制器仍处于 active 状态时隐式反初始化。

```
bk_display_close(lcd_display_handle);
bk_display_deinit(lcd_display_handle);
bk_display_delete(lcd_display_handle);
lcd_display_handle = NULL;
```

<a id="id8"></a>

## 注意事项

1. 使用当前 API 名称：`bk_display_qspi_ctlr_new()`、`bk_display_init()`、`bk_display_open()`、`bk_display_flush()`、`bk_display_close()`、`bk_display_deinit()` 和 `bk_display_delete()`。
2. `lcd_panel` 为必填项。向 `bk_display_qspi_ctlr_new()` 传入 SPI/RGB/DSI panel 会返回 `AVDK_ERR_INVAL`。
3. QSPI LCD 刷帧数据是原始像素数据，不是 `frame_buffer_t` 包装结构。
4. 在 flush 回调执行前，或者控制器仍在使用 frame 前，应用需要保证 frame buffer 有效。
5. `CONFIG_LCD_QSPI_COLOR_DEPTH_BYTE` 需要与 panel 像素格式和帧大小匹配。
