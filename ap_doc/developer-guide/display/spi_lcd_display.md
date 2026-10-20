---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/display/spi_lcd_display.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="spi-lcd-display"></a>

# spi\_lcd\_display

<a id="id1"></a>

## 概述

Display 模块为不同 LCD 接口提供统一的控制器生命周期。SPI LCD 使用硬件 SPI LCD 刷帧通路和 `bk_display_spi_panel_t` 屏描述结构。

本节说明 BK7259 当前 SPI LCD 通路的使用方式。API 细节请参考 [Display API](../../api-reference/multimedia/bk_display.md)，可运行示例请参考 `projects/multimedia/spi_lcd_example`。

<a id="id2"></a>

## 配置项

工程中需要使能 SPI LCD 通路和具体屏驱动：

- `CONFIG_BK_DISPLAY`：使能 Display 组件。
- `CONFIG_FRAME_BUFFER`：使能帧缓冲区分配接口。
- `CONFIG_BK_PERIPHERAL`：编译 LCD panel 描述。
- `CONFIG_LCD_SPI`：使能硬件 SPI LCD 驱动。
- `CONFIG_LCD_SPI_<PANEL>`：使能具体 SPI panel，例如 `CONFIG_LCD_SPI_JD9853`。
- `CONFIG_LCD_SPI_COLOR_DEPTH_BYTE`：输出像素字节数，用于 panel 帧大小。
- `CONFIG_QSPI` 和 `CONFIG_QSPI_LINE_MODE=1` 可能也需要按板级 LCD SPI 驱动配置开启。

背光和电源 GPIO 与具体板级设计相关，需要应用自行配置；display 控制器只管理配置中传入的 LCD SPI 刷帧通路、reset/DC/TE 引脚。

<a id="panel"></a>

## Panel 描述

SPI 屏使用 `bk_display_spi_panel_t` 描述，并提供 `lcd_spi_t` 总线配置：

```
static const lcd_spi_t lcd_spi_jd9853_config = {
    .clk = LCD_QSPI_60M,
    .init_cmd = jd9853_init_cmds,
    .device_init_cmd_len = sizeof(jd9853_init_cmds) / sizeof(lcd_qspi_init_cmd_t),
    .frame_len = 240 * 296 * CONFIG_LCD_SPI_COLOR_DEPTH_BYTE,
};

const bk_display_spi_panel_t lcd_device_jd9853 = {
    .name = "jd9853",
    .width = 240,
    .height = 296,
    .spi = &lcd_spi_jd9853_config,
};

BK_LCD_PANEL_DEVICE_SECTION(lcd_device_jd9853,
                            "jd9853_spi_240x296",
                            BK_LCD_PANEL_BUS_SPI);
```

SPI panel 通路复用 `lcd_qspi_init_cmd_t` 作为寄存器初始化命令记录。新增 SPI 屏时，可参考 `ap/components/bk_peripheral/src/lcd/spi/` 下已有文件，并确认初始化命令、时钟、有效宽高、色深和 `frame_len`。

<a id="spi-panel"></a>

### 适配新 SPI panel

新增一个 SPI LCD sensor/panel 时，推荐按现有 `lcd_spi_jd9853.c`、`lcd_spi_st7789v2.c` 等文件复制改造，优先跑通最小点屏链路，再补充背光、TE、方向和色彩调试。

1. 准备屏厂资料

   从屏厂获取初始化寄存器表、分辨率、像素格式、SPI 最大时钟、reset 时序、DC/TE/背光连接方式，以及整屏刷新的 RAM write 命令和窗口设置命令。若屏支持 RGB565，通常 `CONFIG_LCD_SPI_COLOR_DEPTH_BYTE` 配置为 `2`，同时初始化表中的像素格式寄存器也要设置为 RGB565。
2. 新增 panel 源文件

   在 `ap/components/bk_peripheral/src/lcd/spi/` 下新增 `lcd_spi_<name>.c`，并包含下面三个部分：

   - `static const lcd_qspi_init_cmd_t <name>_init_cmds[]`：按屏厂初始化表填写寄存器命令。复位、sleep out、display on 之间的延时可参考已有文件中的延时写法。
   - `static const lcd_spi_t lcd_spi_<name>_config`：填写 `clk`、`init_cmd`、`device_init_cmd_len` 和 `frame_len`。首版建议先使用保守时钟，点亮稳定后再逐步提高。
   - `const bk_display_spi_panel_t lcd_device_<name>`：填写 `name`、`width`、`height` 和 `spi` 指针。

   注册时必须使用 SPI bus 类型：

   ```
   BK_LCD_PANEL_DEVICE_SECTION(lcd_device_<name>,
                               "<name>_spi_<width>x<height>",
                               BK_LCD_PANEL_BUS_SPI);
   ```
3. 增加编译开关

   修改 `ap/components/bk_peripheral/src/lcd/spi/Kconfig`，新增 `CONFIG_LCD_SPI_<NAME>`；再修改 `ap/components/bk_peripheral/src/lcd/spi/config.cmake`，在该配置打开时把 `lcd_spi_<name>.c` 加入 `SPI_LCD_DEVICE_FILES`。
4. 工程中启用新 panel

   在方案工程配置中打开 `CONFIG_BK_DISPLAY`、`CONFIG_FRAME_BUFFER`、`CONFIG_BK_PERIPHERAL`、`CONFIG_LCD_SPI` 和 `CONFIG_LCD_SPI_<NAME>`。应用侧将 `extern const bk_display_spi_panel_t lcd_device_jd9853` 替换为新符号 `lcd_device_<name>`，并按板级原理图配置 `spi_id`、`dc_pin`、`reset_pin`、`te_pin`、背光和电源 GPIO。
5. 首屏调试顺序

   先确认 reset、背光和电源时序，再确认 SPI 时钟、DC 引脚和初始化命令是否有波形输出。若有背光但黑屏，重点检查 `0x11` sleep out、`0x29` display on、像素格式寄存器、窗口范围和 RAM write 命令；若花屏或颜色异常，重点检查 `CONFIG_LCD_SPI_COLOR_DEPTH_BYTE`、`0x3A` 像素格式、RGB/BGR 方向寄存器和 `frame_len`。

<a id="id3"></a>

## 代码流程

<a id="id4"></a>

### 1\. 创建控制器

使用 `bk_display_spi_ctlr_new()` 创建 SPI display 控制器。`lcd_panel` 必须指向有效的 SPI `bk_display_spi_panel_t` 描述，且其 `spi` 成员不能为空。

```
extern const bk_display_spi_panel_t lcd_device_jd9853;

static bk_display_ctlr_handle_t lcd_display_handle = NULL;
static bk_display_spi_ctlr_config_t spi_ctlr_config = {
    .lcd_panel = &lcd_device_jd9853,
    .spi_id = 0,
    .dc_pin = GPIO_25,
    .reset_pin = GPIO_26,
    .te_pin = 0,
};

avdk_err_t ret = bk_display_spi_ctlr_new(&lcd_display_handle, &spi_ctlr_config);
```

`dc_pin` 是数据/命令选择引脚，`reset_pin` 用于屏复位。`te_pin` 仅在屏和板级硬件连接 TE 引脚时预留使用。

<a id="id5"></a>

### 2\. 初始化并打开

调用 `bk_display_open()` 前需要先调用 `bk_display_init()`。初始化阶段会配置 SPI LCD 驱动和 panel，open 后控制器进入可刷帧状态。

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

SPI 控制器的 `bk_display_flush()` 参数是与 panel 宽高和色深匹配的原始像素 buffer。示例工程按 RGB565 输出分配 `width * height * 2` 字节。

```
uint32_t frame_len = spi_ctlr_config.lcd_panel->width *
                     spi_ctlr_config.lcd_panel->height *
                     CONFIG_LCD_SPI_COLOR_DEPTH_BYTE;
void *disp_frame = bk_frame_buffer_malloc(MEM_SLAB_HEAP_CODED, frame_len);

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

1. 使用当前 API 名称：`bk_display_spi_ctlr_new()`、`bk_display_init()`、`bk_display_open()`、`bk_display_flush()`、`bk_display_close()`、`bk_display_deinit()` 和 `bk_display_delete()`。
2. `bk_display_spi_ctlr_new()` 使用 `bk_display_spi_ctlr_config_t`。软件 SPI bus 配置用于命令通道，不用于该 SPI LCD display 控制器。
3. `lcd_panel` 为必填项。向 `bk_display_spi_ctlr_new()` 传入 QSPI/RGB/DSI panel 会返回 `AVDK_ERR_INVAL`。
4. SPI LCD 刷帧数据是原始像素数据，不是 `frame_buffer_t` 包装结构。
5. 在 flush 回调执行前，或者控制器仍在使用 frame 前，应用需要保证 frame buffer 有效。
