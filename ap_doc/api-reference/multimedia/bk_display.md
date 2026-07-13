# display



## 概述

Display模块提供统一的显示控制器管理接口

参考工程：


- 有关display的详细信息，请参阅：


  - [display 使用文档](../../developer-guide/display/display_user_guide.md "../../developer-guide/display/display_user_guide.md")

  - [支持的 LCD 设备](../../developer-guide/display/supported_lcd_devices.md "../../developer-guide/display/supported_lcd_devices.md")

  - [新增 MIPI panel](../../developer-guide/display/how_to_add_mipi_panel.md "../../developer-guide/display/how_to_add_mipi_panel.md")

  - [新增 RGB panel](../../developer-guide/display/how_to_add_rgb_panel.md "../../developer-guide/display/how_to_add_rgb_panel.md")

  - [qspi display开发指南](../../developer-guide/display/qspi_lcd_display.md "../../developer-guide/display/qspi_lcd_display.md")

  - [spi display开发指南](../../developer-guide/display/spi_lcd_display.md "../../developer-guide/display/spi_lcd_display.md")

- 有关display的示例工程，请参阅：


  - [rgb display 示例项目](../../examples/projects/multimedia/rgb_lcd_example.md "../../examples/projects/multimedia/rgb_lcd_example.md")

  - qspi display 示例项目：`projects/multimedia/qspi_lcd_example`

  - spi display 示例项目：`projects/multimedia/spi_lcd_example`

Display 组件采用 **总线（bus）→ 屏（panel）→ 显示控制器（ctlr）** 三域句柄模型，
对应三个公有头文件：


- `<components/bk_display.h>`：伞头，拉入下面三套 API

- `<components/bk_display_bus.h>`：总线 API + 配置类型

- `<components/bk_lcd_panel.h>` / `<components/bk_lcd_panel_types.h>`：panel API + 描述符类型

典型 bring-up 顺序与详细用法见
[display 使用文档](../../developer-guide/display/display_user_guide.md "../../developer-guide/display/display_user_guide.md") 。


## DISPLAY API Reference


### 显示控制器（display controller）


```
/* 创建 DPU 显示控制器；panel 为 bk_lcd_*_panel_new() 得到的句柄，

 * config 只填 video 层（timing/像素时钟/时钟源由控制器从 panel 句柄内部读取）。 */
avdk_err_t bk_display_dpu_ctlr_new(bk_display_ctlr_handle_t *handle,
                                   bk_avdk_lcd_panel_handle_t panel,
                                   const bk_display_dpu_config_t *config);

/* 创建 SPI 显示控制器（HW SPI LCD 帧通路）；

 * config 为 SPI 显示控制器配置，会被拷贝进控制器内部。 */
avdk_err_t bk_display_spi_ctlr_new(bk_display_ctlr_handle_t *handle,
                                   bk_display_spi_ctlr_config_t *config);

/* 创建 QSPI 显示控制器（HW QSPI LCD 帧通路）；config 为 QSPI 控制器配置，

 * 会被拷贝进控制器内部，flush 的 frame 需指向原始像素数据。 */
avdk_err_t bk_display_qspi_ctlr_new(bk_display_ctlr_handle_t *handle,
                                    bk_display_qspi_ctlr_config_t *config);

avdk_err_t bk_display_init  (bk_display_ctlr_handle_t handle);  /* 内部驱动 panel reset + init_cmds */
avdk_err_t bk_display_open  (bk_display_ctlr_handle_t handle);
avdk_err_t bk_display_flush (bk_display_ctlr_handle_t handle, void *frame, flush_free_cb_t cb);
avdk_err_t bk_display_ioctl (bk_display_ctlr_handle_t handle, bk_display_ioctl_cmd_t cmd, void *arg);
avdk_err_t bk_display_pixel_format_set(bk_display_ctlr_handle_t handle,
                                       const bk_display_pixel_format_config_t *config);
avdk_err_t bk_display_close (bk_display_ctlr_handle_t handle);
avdk_err_t bk_display_deinit(bk_display_ctlr_handle_t handle);
avdk_err_t bk_display_delete(bk_display_ctlr_handle_t handle);

```


### 总线（bus）


```
avdk_err_t bk_display_dsi_bus_new(bk_display_bus_handle_t *handle, bk_display_dsi_bus_config_t *config);
avdk_err_t bk_display_spi_bus_new(bk_display_bus_handle_t *handle, bk_display_spi_bus_config_t *config);
avdk_err_t bk_display_bus_delete (bk_display_bus_handle_t handle);

/* 可选：在 dsi_bus_new 之后、mipi_panel_new 之前强制指定时钟源 */
avdk_err_t bk_display_bus_set_clock_src(bk_display_bus_handle_t handle, dpu_clk_src_t clk_src);

bk_err_t   bk_display_bus_tx_param(bk_display_bus_handle_t h, int cmd, const void *p, size_t n);
bk_err_t   bk_display_bus_rx_param(bk_display_bus_handle_t h, int cmd,       void *p, size_t n);

```


### 屏（panel）


```
/* panel_config 只携带 reset_pin；RST 有效电平/时序/reset/init 钩子都在 panel 描述符里 */
bk_err_t bk_lcd_mipi_panel_new(bk_display_bus_handle_t bus,
                               const bk_lcd_panel_config_t *panel_config,
                               const bk_display_dsi_panel_t *panel_desc,
                               bk_avdk_lcd_panel_handle_t *ret_panel);
bk_err_t bk_lcd_rgb_panel_new (bk_display_bus_handle_t bus,
                               const bk_lcd_panel_config_t *panel_config,
                               const bk_display_rgb_panel_t *panel_desc,
                               bk_avdk_lcd_panel_handle_t *ret_panel);

bk_err_t bk_lcd_panel_delete   (bk_avdk_lcd_panel_handle_t panel);
bk_err_t bk_lcd_panel_read_id  (bk_avdk_lcd_panel_handle_t panel, uint32_t *id);
bk_err_t bk_lcd_panel_tx_param (bk_avdk_lcd_panel_handle_t panel, int cmd, const void *param, size_t size);
bk_err_t bk_lcd_panel_rx_param (bk_avdk_lcd_panel_handle_t panel, int cmd,       void *param, size_t size);

/* 填进描述符 .reset / .init 的默认实现 */
bk_err_t bk_lcd_mipi_default_reset(bk_avdk_lcd_panel_t *panel);
bk_err_t bk_lcd_mipi_default_init (bk_avdk_lcd_panel_t *panel);
bk_err_t bk_lcd_rgb_default_reset (bk_avdk_lcd_panel_t *panel);
bk_err_t bk_lcd_rgb_default_init  (bk_avdk_lcd_panel_t *panel);

/* 链接段注册表查询 */
uint32_t bk_lcd_get_mipi_panel_list(const bk_display_dsi_panel_t **panels, uint32_t max_count);
uint32_t bk_lcd_get_rgb_panel_list (const bk_display_rgb_panel_t **panels, uint32_t max_count);
uint32_t bk_lcd_get_spi_panel_list (const bk_display_spi_panel_t **panels, uint32_t max_count);
uint32_t bk_lcd_get_qspi_panel_list(const bk_display_qspi_panel_t **panels, uint32_t max_count);
const bk_display_dsi_panel_t *bk_lcd_find_mipi_panel_by_name(const char *name);
const bk_display_rgb_panel_t *bk_lcd_find_rgb_panel_by_name (const char *name);
const bk_display_spi_panel_t *bk_lcd_find_spi_panel_by_name (const char *name);
const bk_display_qspi_panel_t *bk_lcd_find_qspi_panel_by_name(const char *name);

```


## DISPLAY Typedefs


```
/* 不透明句柄 */
typedef struct bk_display_ctlr_t  *bk_display_ctlr_handle_t;
typedef struct bk_display_bus_ctlr_t *bk_display_bus_handle_t;
typedef struct bk_avdk_lcd_panel_t   *bk_avdk_lcd_panel_handle_t;

/* panel new 第 2 参：现在只有 reset_pin */
struct bk_lcd_panel_config_t {
    int8_t reset_pin;            /* LCD reset GPIO，-1 表示禁用 */
};

/* DPU 控制器配置：只填 video 层；timing / 像素时钟 / 时钟源都不在这里，

 * 由控制器从 panel 句柄内部读取。dpu_video_layer_config_t 见 <driver/dpu_types.h>。 */
typedef struct {
    dpu_video_layer_config_t video;
} bk_display_dpu_config_t;

/* 运行期切像素格式（ioctl 参数 / pixel_format_set 参数） */
typedef struct {
    bk_pixel_format_t format;
    bool decompress;
} bk_display_pixel_format_config_t;

```

更多类型（`bk_display_dsi_panel_t` / `bk_display_rgb_panel_t` /
`bk_display_spi_panel_t` / `bk_display_qspi_panel_t` /
`bk_display_spi_ctlr_config_t` / `bk_display_qspi_ctlr_config_t` /
`bk_display_reset_timing_t` / `lcd_mipi_init_cmd_t` /
`lcd_rgb_spi_init_cmd_t` 等）见 `<components/bk_lcd_panel_types.h>` 和
`<components/bk_display.h>`，
字段说明见
[新增 MIPI panel](../../developer-guide/display/how_to_add_mipi_panel.md "../../developer-guide/display/how_to_add_mipi_panel.md") /
[新增 RGB panel](../../developer-guide/display/how_to_add_rgb_panel.md "../../developer-guide/display/how_to_add_rgb_panel.md") /
[QSPI display开发指南](../../developer-guide/display/qspi_lcd_display.md "../../developer-guide/display/qspi_lcd_display.md") /
[SPI display开发指南](../../developer-guide/display/spi_lcd_display.md "../../developer-guide/display/spi_lcd_display.md") 。
