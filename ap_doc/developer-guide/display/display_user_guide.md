# BK7259 Display 组件使用文档


本文面向**应用开发者**，介绍如何用 `bk_display` 组件把 LCD 屏点亮、持续刷帧、
并在运行期切换像素格式。一篇覆盖从 bring-up 到接口详解；新增/移植屏见
[如何新增 MIPI DSI Panel（BK7259）](how_to_add_mipi_panel.md "how_to_add_mipi_panel.md") 与 [如何新增 RGB Panel（BK7259）](how_to_add_rgb_panel.md "how_to_add_rgb_panel.md")，当前支持的屏型号见
[支持的 LCD 设备](supported_lcd_devices.md "supported_lcd_devices.md")。

本页目录


- [1. 概述](#id2 "#id2")

- [2. 核心概念与架构](#id3 "#id3")


  - [2.1 三个句柄：总线 → 屏 → 控制器](#id4 "#id4")

  - [2.2 控制器状态机](#id5 "#id5")

- [3. 快速开始](#id6 "#id6")


  - [3.1 五步法（通用骨架）](#id7 "#id7")

  - [3.2 最小 MIPI 示例](#mipi "#mipi")

  - [3.3 最小 RGB 示例](#rgb "#rgb")

- [4. 使用流程详解](#id8 "#id8")


  - [4.1 选择总线 / 路径](#id9 "#id9")

  - [4.2 打开（bring-up）顺序](#bring-up "#bring-up")

  - [4.3 刷帧 flush 与帧 buffer](#flush-buffer "#flush-buffer")

  - [4.4 关闭与销毁（teardown ladder）](#teardown-ladder "#teardown-ladder")

  - [4.5 上电 / 下电顺序](#id10 "#id10")

- [5. 接口详解](#id11 "#id11")


  - [5.1 总线 Bus API](#bus-api "#bus-api")

  - [5.2 屏 Panel API](#panel-api "#panel-api")

  - [5.3 显示控制器 Display Controller API](#display-controller-api "#display-controller-api")

  - [5.4 关键数据类型](#id12 "#id12")

- [6. 进阶用法](#id13 "#id13")


  - [6.1 运行期切换像素格式](#id14 "#id14")

  - [6.2 运行期发送屏命令（读 ID / 二次初始化）](#id "#id")

  - [6.3 生产级集成参考](#id15 "#id15")

- [7. 线程模型与并发](#id16 "#id16")

- [8. 电源与时钟须知](#id17 "#id17")

- [9. 错误码约定](#id18 "#id18")

- [10. 常见问题 FAQ](#faq "#faq")

- [相关文档](#id19 "#id19")


## [1. 概述](#id20 "#id20")

`bk_display` 是统一的 LCD 显示组件，对上层应用屏蔽不同屏的总线差异，支持四类总线：


- **MIPI-DSI**：高速串行屏，像素由 DPU 直推 DSI host

- **并口 RGB**：24-bit 并行像素 + SW SPI 配置通道

- **QSPI**：四线 SPI 屏（见 [qspi_lcd_display](qspi_lcd_display.md "qspi_lcd_display.md")）

- **SPI**：硬件 SPI 屏（见 [spi_lcd_display](spi_lcd_display.md "spi_lcd_display.md")）

只需包含一个伞头即可拉入全部 API（总线 / 屏 / 显示控制器）：


```
#include <components/bk_display.h>

```

核心能力：bring-up 一条显示通路、提交帧（flush）、运行期切像素格式、运行期下发屏命令
（读 ID / 补发初始化命令）。


## [2. 核心概念与架构](#id21 "#id21")


### [2.1 三个句柄：总线 → 屏 → 控制器](#id22 "#id22")

一条显示通路由三个相互正交的句柄串起来：


```
┌────────────────────────────┐
│ bk_display_bus_handle_t    │  物理通道（DSI / SW SPI / HW SPI）
└──────────────┬─────────────┘
               │
┌──────────────┴─────────────┐
│ bk_avdk_lcd_panel_handle_t │  一块屏的实例（绑定 bus + reset 引脚 + 描述符）
└──────────────┬─────────────┘
               │
┌──────────────┴─────────────┐
│ bk_display_ctlr_handle_t   │  DPU + 视频层 + flush 队列
└────────────────────────────┘

```

三者职责：

| 句柄 | 抽象 | 职责 |
| --- | --- | --- |
| `bk_display_bus_handle_t` | 物理通道 | 承载像素和/或命令：DSI 走 DCS、SW SPI 走 bit-bang 配置、HW SPI 走 DMA 帧流 |
| `bk_avdk_lcd_panel_handle_t` | 屏实例 | 绑定屏描述符（timing / init_cmds / reset 时序）+ bus + reset 引脚 |
| `bk_display_ctlr_handle_t` | 显示通路 | 配置 DPU、编排状态机、提交 flush、运行期 ioctl |

时序 / 像素时钟 / 时钟源都缓存在 panel 句柄里，由控制器内部读取，
应用层的 `dpu_config` **只填 video 层**。


### [2.2 控制器状态机](#id23 "#id23")

显示控制器是一个显式状态机，flush 只在 ACTIVE 态可用：


```
dpu_ctlr_new()        ┌──────────┐
──────────────────►   │  DEINIT  │  (句柄已建，HW 未编程)
                      └────┬─────┘
         bk_display_init() │  ▲ bk_display_deinit()
                           ▼  │
                      ┌──────────┐
                      │  INITED  │  (DPU 已编程，等 open)
                      └────┬─────┘
         bk_display_open() │  ▲ bk_display_close()
                           ▼  │
                      ┌──────────┐    bk_display_flush() / bk_display_ioctl()
                      │  ACTIVE  │◄── (持续刷帧 / 运行期重配)
                      └────┬─────┘
         bk_display_close()│
                           ▼
                      ┌──────────┐
                      │  CLOSED  │  (静默，可再次 open)
                      └──────────┘

销毁：bk_display_delete()（会自动先 deinit，保证无泄漏）

```

要点：


- `init` / `deinit` 受内部 mutex 保护，状态合法性集中校验。

- `deinit` 会等所有 inflight flush 落盘后才撕 DPU。

- 在 INITED 态首次 flush 会被**自动提升到 ACTIVE 并打 WARN**——不要依赖该行为，
  正经流程显式调 `bk_display_open`。

- `delete` 会自动调一次 `deinit`，句柄释放路径无泄漏。


## [3. 快速开始](#id24 "#id24")


### [3.1 五步法（通用骨架）](#id25 "#id25")

无论 MIPI 还是 RGB，bring-up 都是这五步（按顺序）：


```
/* 1. 板级电源：VDDIO 1.8V（背光暂不点） */
app_display_power_enable(true);                  /* 或自己投票 PM_AUXLDO_USER_DISPLAY */

/* 2. 总线（MIPI 传 NULL 即可；RGB 用 bk_display_spi_bus_new + cfg） */
bk_display_dsi_bus_new(&bus, NULL);

/* 3. 屏：只填 reset_pin；RST 有效电平 / 时序在描述符里；无需手动 reset/init */
bk_lcd_panel_config_t pcfg = { .reset_pin = GPIO_60 };
bk_lcd_mipi_panel_new(bus, &pcfg, panel_desc, &panel);

/* 4. 显示控制器（DPU）：第 2 参传 panel 句柄；dpu_cfg 只填 video 层 */
bk_display_dpu_config_t dpu_cfg = {
    .video.enable     = true,
    .video.format     = BK_PIXEL_FORMAT_RGB565,
    .video.decompress = false,
};
bk_display_dpu_ctlr_new(&ctlr, panel, &dpu_cfg);
bk_display_init(ctlr);                           /* 内部驱动 panel reset + init_cmds */
bk_display_open(ctlr);

/* 5. 背光（最后才点亮，避免花屏） */
bk_gpio_set_output_high(BACKLIGHT_PIN);

```

之后即可 `bk_display_flush(ctlr, frame, free_cb)` 持续推帧。下电按相反顺序：
背光 → `close` → `deinit` → `delete` ctlr → `delete` panel → `delete` bus → 断 VDDIO。


### [3.2 最小 MIPI 示例](#id26 "#id26")

参考 `projects/multimedia/mipi_lcd_example/`（`ap/src/lcd_example_mipi.c`）：


```
avdk_err_t lcd_example_dsi_open(display_ctx_t *ctx, const char *name, bk_pixel_format_t fmt)
{
    bk_display_dpu_config_t dpu = {0};
    dpu.video.enable     = true;
    dpu.video.decompress = (fmt == BK_PIXEL_FORMAT_ARGB8888);
    dpu.video.format     = fmt;

    const bk_lcd_panel_config_t pcfg = { .reset_pin = GPIO_60 };

    bk_lodoen_enable(true);                                  /* VDDIO 1.8V */
    bk_display_dsi_bus_new(&ctx->dis_bus_handle, NULL);      /* DSI 总线 */

    /* 按名字在链接段里查屏描述符 */
    const bk_display_dsi_panel_t *panel = bk_lcd_find_mipi_panel_by_name(name);
    if (!panel) return AVDK_ERR_UNSUPPORTED;

    bk_lcd_mipi_panel_new(ctx->dis_bus_handle, &pcfg, panel, &ctx->panel_handle);
    bk_display_dpu_ctlr_new(&ctx->dpu_ctlr_handle, ctx->panel_handle, &dpu);
    bk_display_init(ctx->dpu_ctlr_handle);                   /* 内部 reset + init_cmds */
    bk_display_open(ctx->dpu_ctlr_handle);

    ctx->width  = panel->timing.h_size;
    ctx->height = panel->timing.v_size;
    ctx->format = fmt;
    return AVDK_ERR_OK;
}

```

普通 MIPI 屏**无需**调用 `bk_display_bus_set_clock_src`：DSI 总线默认
`DPU_CLK_SRC_DPHY_DPLL`，panel init 时若 PLL 求解失败会自动回落 `SYSCLK`。


### [3.3 最小 RGB 示例](#id27 "#id27")

参考 `projects/multimedia/rgb_lcd_example/`（`ap/src/lcd_example_rgb.c`）。
RGB 屏的像素走 24-bit 并口，寄存器初始化走 SW SPI 配置通道：


```
avdk_err_t lcd_example_rgb_open(display_ctx_t *ctx, const char *name, bk_pixel_format_t fmt)
{
    bk_display_dpu_config_t dpu = {
        .video.enable     = true,
        .video.decompress = (fmt == BK_PIXEL_FORMAT_ARGB8888),
        .video.format     = fmt,
    };

    bk_display_spi_bus_config_t bus_cfg = {
        .clk_pin = GPIO_8,
        .csx_pin = GPIO_28,
        .sda_pin = GPIO_9,
    };
    bk_lcd_panel_config_t panel_config = { .reset_pin = GPIO_6 };

    const bk_display_rgb_panel_t *panel = bk_lcd_find_rgb_panel_by_name(name);
    if (!panel) return AVDK_ERR_UNSUPPORTED;

    /* 关键：从描述符复制 cmd_width 给 bus（决定 9-bit / 4-byte 包协议） */
    bus_cfg.cmd_width = panel->spi_cmd_16bit ? 16 : 8;

    bk_display_spi_bus_new(&ctx->spi_bus_handle, &bus_cfg);
    bk_lcd_rgb_panel_new(ctx->spi_bus_handle, &panel_config, panel, &ctx->panel_handle);

    bk_display_dpu_ctlr_new(&ctx->dpu_ctlr_handle, ctx->panel_handle, &dpu);
    bk_display_init(ctx->dpu_ctlr_handle);                /* 内部派发 SPI 寄存器序列 */
    bk_display_open(ctx->dpu_ctlr_handle);

    bk_gpio_set_output_high(GPIO_7);                      /* 背光 */
    return AVDK_ERR_OK;
}

```


## [4. 使用流程详解](#id28 "#id28")


### [4.1 选择总线 / 路径](#id29 "#id29")

| 屏类型 | bus_new | panel_new | 时钟源（内部自动） | 像素流向 |
| --- | --- | --- | --- | --- |
| MIPI-DSI 普通屏 | `bk_display_dsi_bus_new(&bus, NULL)` | `bk_lcd_mipi_panel_new` | `DPHY_DPLL`（PLL 不满足自动回落 `SYSCLK`） | DPU → DSI host |
| LT8912B HDMI 桥 | `bk_display_dsi_bus_new` + `bk_lcd_lt8912b_set_io_pins()` | `bk_lcd_mipi_panel_new` | 同上 | DPU → DSI host → HDMI 桥 |
| 并口 RGB | `bk_display_spi_bus_new(&bus, cfg)` | `bk_lcd_rgb_panel_new` | `SYSCLK`（固定） | DPU → 24-bit RGB pinmux |
| 硬件 SPI 屏 | 不单独创建 bus | `bk_display_spi_ctlr_new` | n/a | HW SPI LCD DMA 帧流 |

提示：RGB 屏的 “SPI bus” 只是**配置通道**（GPIO bit-bang 写寄存器），像素走并口
RGB，不要和硬件 SPI LCD 刷帧通路混淆。硬件 SPI 屏详见 [spi_lcd_display](spi_lcd_display.md "spi_lcd_display.md")。


### [4.2 打开（bring-up）顺序](#id30 "#id30")

bring-up 完整顺序为：VDDIO 上电 → `bus_new` → `panel_new` →
`dpu_ctlr_new` → `init` → `open` → 背光。其中 `bk_display_init()`
内部会驱动屏的 reset 波形并下发 `init_cmds`，应用层**不需要**手动 reset/init。


### [4.3 刷帧 flush 与帧 buffer](#id31 "#id31")


```
while (ctx->enable) {
    void *frame = bk_frame_buffer_malloc(MEM_SLAB_HEAP_UNCODED, frame_size);
    fill_frame(frame, ctx->width, ctx->height, ...);
    if (bk_display_flush(ctx->dpu_ctlr_handle, frame, display_frame_free) != AVDK_ERR_OK)
        bk_frame_buffer_free(frame);
    rtos_delay_milliseconds(500);
}

```


- 帧 buffer 必须用 `bk_frame_buffer_malloc(MEM_SLAB_HEAP_UNCODED, size)` 分配，
  否则 DPU DMA 找不到合法物理地址。

- `flush` 成功后**帧所有权移交 DPU**：不要在调用后立即释放；DPU 刷完会通过
  `flush_free_cb_t` 回调，回调里调 `bk_frame_buffer_free(frame)`。


### [4.4 关闭与销毁（teardown ladder）](#id32 "#id32")

按相反顺序逐级释放，且**先撕 ctlr/panel/bus，再断 VDDIO**（否则屏的 IO 引脚会
看到悬空电压）：


```
背光关
→ if opened : bk_display_close(ctlr)
→ if inited : bk_display_deinit(ctlr)
→             bk_display_delete(ctlr)   (ctlr = NULL)
→ bk_lcd_panel_delete(panel)            (panel = NULL)
→ bk_display_bus_delete(bus)            (bus   = NULL)
→ app_display_power_enable(false)       (最后再降 VDDIO)

```

生产代码建议用 `ctlr_inited` / `ctlr_opened` 标志位，使 bring-up 任意一步失败都能
精确回滚（见 §6.3）。


### [4.5 上电 / 下电顺序](#id33 "#id33")


- 上电：**VDDIO → bus_new → panel reset/init → ctlr open → 背光**

- 下电：**背光 → close → deinit → delete ctlr/panel/bus → VDDIO**


## [5. 接口详解](#id34 "#id34")

签名以 `<components/bk_display.h>` 系列头为准。返回码约定见 §9。


### [5.1 总线 Bus API](#id35 "#id35")


**bk_display_dsi_bus_new**


```
avdk_err_t bk_display_dsi_bus_new(bk_display_bus_handle_t *handle,
                                  bk_display_dsi_bus_config_t *config);

```


- 作用：创建 MIPI-DSI 总线，内部完成 MIPI 子域上电、D-PHY 模拟轨投票、`mipi_dsi_init()`。

- 参数：`handle` 输出总线句柄；`config` 可为 `NULL`（预留）。

- 返回：`AVDK_ERR_OK` / `AVDK_ERR_INVAL`（handle 为 NULL）/ `AVDK_ERR_NO_MEM`。

- 调用时机：VDDIO 上电之后；与 `bk_lcd_mipi_panel_new` 配套。


**bk_display_spi_bus_new**


```
avdk_err_t bk_display_spi_bus_new(bk_display_bus_handle_t *handle,
                                  bk_display_spi_bus_config_t *config);

```


- 作用：创建 GPIO bit-bang SPI 配置通道，用于 RGB 屏寄存器初始化；硬件 SPI LCD
  刷帧通路由 `bk_display_spi_ctlr_new()` 和 `bk_display_spi_ctlr_config_t` 管理，
  不经过该 bus API。

- 参数：需 `clk_pin` / `csx_pin` / `sda_pin` / `cmd_width`；其中
  `cmd_width = panel->spi_cmd_16bit ? 16 : 8`。

- 返回：`AVDK_ERR_OK` / `AVDK_ERR_INVAL`（参数非法）。


**bk_display_bus_delete**


```
avdk_err_t bk_display_bus_delete(bk_display_bus_handle_t handle);

```


- 作用：销毁总线并释放其占用的所有资源（含电源投票）。


**bk_display_bus_set_clock_src**


```
avdk_err_t bk_display_bus_set_clock_src(bk_display_bus_handle_t handle, dpu_clk_src_t clk_src);

```


- 作用：**可选**。强制指定 MIPI-DSI 的 DPU 寄存器时钟源。

- 调用时机：在 `bk_display_dsi_bus_new` 之后、`bk_lcd_mipi_panel_new` 之前。
  不调用时 DSI 默认 `DPU_CLK_SRC_DPHY_DPLL` 并在 PLL 不满足时自动回落 `SYSCLK`。

- 返回：`AVDK_ERR_OK` / `AVDK_ERR_UNSUPPORTED`（SPI 总线无时钟源概念）。


**bk_display_bus_tx_param / bk_display_bus_rx_param**


```
bk_err_t bk_display_bus_tx_param(bk_display_bus_handle_t h, int cmd, const void *p, size_t n);
bk_err_t bk_display_bus_rx_param(bk_display_bus_handle_t h, int cmd,       void *p, size_t n);

```


- 作用：直接在总线命令通道上收发命令（裸接口）。一般用 §5.2 的 panel 版本即可。

- 约束：`tx_param` 支持 DSI 与 SW SPI；`rx_param` 仅 DSI 支持；HW SPI 均不支持。


### [5.2 屏 Panel API](#id36 "#id36")


**bk_lcd_mipi_panel_new / bk_lcd_rgb_panel_new**


```
bk_err_t bk_lcd_mipi_panel_new(bk_display_bus_handle_t bus,
                               const bk_lcd_panel_config_t *panel_config,
                               const bk_display_dsi_panel_t *desc,
                               bk_avdk_lcd_panel_handle_t *out);
bk_err_t bk_lcd_rgb_panel_new (bk_display_bus_handle_t bus,
                               const bk_lcd_panel_config_t *panel_config,
                               const bk_display_rgb_panel_t *desc,
                               bk_avdk_lcd_panel_handle_t *out);

```


- 作用：在指定总线上创建一块屏实例。

- 参数：`panel_config` 现**只有** `reset_pin`（RST 有效电平 / 时序 / reset / init
  钩子都在 `desc` 描述符里）；`desc` 为屏描述符（可用查表接口按名字获取）。

- 返回：`BK_OK` / `BK_ERR_NULL_PARAM` / `BK_ERR_NO_MEM`。


**bk_lcd_panel_delete**


```
bk_err_t bk_lcd_panel_delete(bk_avdk_lcd_panel_handle_t panel);

```


- 作用：释放屏句柄（不释放其所属总线）。


**bk_lcd_panel_read_id**


```
bk_err_t bk_lcd_panel_read_id(bk_avdk_lcd_panel_handle_t panel, uint32_t *id);

```


- 作用：按描述符的 `read_id_regs` 读屏 ID。

- 约束：须在 `bk_display_init()` 之后调用；`read_id_regs` 为 NULL 时返回 `BK_ERR_NOT_SUPPORT`。


**bk_lcd_panel_tx_param / bk_lcd_panel_rx_param**


```
bk_err_t bk_lcd_panel_tx_param(bk_avdk_lcd_panel_handle_t panel, int cmd, const void *param, size_t size);
bk_err_t bk_lcd_panel_rx_param(bk_avdk_lcd_panel_handle_t panel, int cmd,       void *param, size_t size);

```


- 作用：运行期向屏发送单条命令 / 读回参数（详见 §6.2）。`panel` 内部转发到自己的 bus，
  调用方无需持有 bus 句柄。

- 约束：`tx_param` 支持 MIPI DSI 与 SW SPI；`rx_param` 仅 MIPI DSI 支持。


**查表接口（链接段自动注册）**


```
uint32_t bk_lcd_get_mipi_panel_list(const bk_display_dsi_panel_t **out, uint32_t max);
uint32_t bk_lcd_get_rgb_panel_list (const bk_display_rgb_panel_t **out, uint32_t max);
const bk_display_dsi_panel_t *bk_lcd_find_mipi_panel_by_name(const char *name);
const bk_display_rgb_panel_t *bk_lcd_find_rgb_panel_by_name (const char *name);

```


- 作用：枚举 / 按名字查找当前固件里注册的屏描述符（受 Kconfig 选择影响）。

备注

屏的 reset / init **没有**独立 public 入口——bring-up 时由 `bk_display_init()`
内部隐式驱动描述符的 `.reset` / `.init`。默认实现
`bk_lcd_mipi_default_reset` / `bk_lcd_mipi_default_init` /
`bk_lcd_rgb_default_reset` / `bk_lcd_rgb_default_init` 可直接填进描述符，
详见 [如何新增 MIPI DSI Panel（BK7259）](how_to_add_mipi_panel.md "how_to_add_mipi_panel.md") / [如何新增 RGB Panel（BK7259）](how_to_add_rgb_panel.md "how_to_add_rgb_panel.md")。


### [5.3 显示控制器 Display Controller API](#id37 "#id37")


**bk_display_dpu_ctlr_new**


```
avdk_err_t bk_display_dpu_ctlr_new(bk_display_ctlr_handle_t *h,
                                   bk_avdk_lcd_panel_handle_t panel,
                                   const bk_display_dpu_config_t *cfg);

```


- 作用：创建 DPU 显示控制器（状态 = DEINIT）。

- 参数：`panel` 为已创建的屏句柄；`cfg` 只填 video 层（timing / 像素时钟 / 时钟源由
  控制器从 panel 句柄内部读取）。

- 返回：`AVDK_ERR_OK` / `AVDK_ERR_INVAL` / `AVDK_ERR_NO_MEM`。


**bk_display_init / open / close / deinit / delete**


```
avdk_err_t bk_display_init  (bk_display_ctlr_handle_t h);   /* DEINIT → INITED，内部驱动 reset+init_cmds */
avdk_err_t bk_display_open  (bk_display_ctlr_handle_t h);   /* INITED/CLOSED → ACTIVE */
avdk_err_t bk_display_close (bk_display_ctlr_handle_t h);   /* ACTIVE → CLOSED */
avdk_err_t bk_display_deinit(bk_display_ctlr_handle_t h);   /* → DEINIT，等 inflight flush 落盘 */
avdk_err_t bk_display_delete(bk_display_ctlr_handle_t h);   /* 释放句柄（自动先 deinit） */

```


- 约束：状态机见 §2.2；`flush` 只在 ACTIVE 态可用。


**bk_display_flush**


```
avdk_err_t bk_display_flush(bk_display_ctlr_handle_t h, void *frame, flush_free_cb_t cb);

```


- 作用：提交一帧刷新。`cb` 在该帧不再被使用时回调（用于释放帧 buffer）。

- 约束：见 §4.3，帧所有权在调用后移交 DPU。


**bk_display_ioctl / bk_display_pixel_format_set**


```
avdk_err_t bk_display_ioctl(bk_display_ctlr_handle_t h, bk_display_ioctl_cmd_t cmd, void *arg);
avdk_err_t bk_display_pixel_format_set(bk_display_ctlr_handle_t h,
                                       const bk_display_pixel_format_config_t *cfg);

```


- 作用：运行期控制。当前命令 `BK_DISPLAY_IOCTL_DPU_PIXEL_FORMAT` 用于切像素格式，
  `arg` 为 `bk_display_pixel_format_config_t*`；`bk_display_pixel_format_set` 是其便捷封装。

- 约束：仅 ACTIVE 态可用，且切换前须停掉 flush（见 §6.1）。


### [5.4 关键数据类型](#id38 "#id38")


```
/* 屏配置：现在只有 reset_pin */
struct bk_lcd_panel_config_t {
    int8_t reset_pin;            /* LCD reset GPIO，-1 表示禁用 */
};

/* DPU 控制器配置：只填 video 层 */
typedef struct {
    dpu_video_layer_config_t video;   /* enable / format / decompress ... */
} bk_display_dpu_config_t;

/* 运行期切像素格式 */
typedef struct {
    bk_pixel_format_t format;
    bool decompress;
} bk_display_pixel_format_config_t;

```


**显示时序 bk_display_timing_t**（在 `<driver/dpu_types.h>`，由屏描述符提供，应用层不直接填）：

| 字段 | 说明 |
| --- | --- |
| `h_size` / `v_size` | 显示分辨率 |
| `hsync_pulse_width` / `hsync_back_porch` / `hsync_front_porch` | 行同步 / 后沿 / 前沿（像素数） |
| `vsync_pulse_width` / `vsync_back_porch` / `vsync_front_porch` | 帧同步 / 后沿 / 前沿（行数） |

`bk_display_timing_t` **不含像素时钟字段**：MIPI 由 `fps` + 总像素数自动算，RGB 用
描述符的 `pixel_clock_hz`。


**像素格式 bk_pixel_format_t**（在 `<common/avdk_pixel_types.h>`）：

| 值 | 字节/像素 | 备注 |
| --- | --- | --- |
| `BK_PIXEL_FORMAT_RGB565` | 2 | 最常用 |
| `BK_PIXEL_FORMAT_RGB888` | 3 | 不带 alpha |
| `BK_PIXEL_FORMAT_ARGB8888` | 4（decompress 时 2） | `decompress=true` 时输入为 RLE，内部解压成 ARGB |
| `BK_PIXEL_FORMAT_NV12` | 1.5 | 视频常用，Y 平面 + UV 交错平面 |


## [6. 进阶用法](#id39 "#id39")


### [6.1 运行期切换像素格式](#id40 "#id40")

不断电即可切像素格式 / 切是否开 decompress。**必须先停 flush 再 ioctl**，否则旧格式
inflight 帧会撞上新 DPU layer 配置：


```
void cli_mipi_lcd_switch_format(const bk_display_pixel_format_config_t *cfg)
{
    lcd_example_flush_thread_stop(&ctx);                  /* 1) 先停刷帧 */

    if (bk_display_ioctl(ctx.dpu_ctlr_handle,
                         BK_DISPLAY_IOCTL_DPU_PIXEL_FORMAT, (void *)cfg) != AVDK_ERR_OK) {
        lcd_example_flush_thread_start(&ctx);             /* 2) 失败回滚 */
        return;
    }

    ctx.format     = cfg->format;                         /* 3) 同步本地状态 */
    ctx.decompress = cfg->decompress;
    lcd_example_flush_thread_start(&ctx);                 /* 4) 重启刷帧 */
}

```

`bk_display_pixel_format_set(handle, &cfg)` 与上面的 ioctl 等价。


### [6.2 运行期发送屏命令（读 ID / 二次初始化）](#id41 "#id41")

调试常见需求：屏不亮时读 ID 确认通信，或初始化后再补几条命令。


```
#include <components/bk_lcd_panel.h>

/* 读屏 ID（按描述符 read_id_regs / read_id_bytes 自动解析） */
uint32_t id = 0;
bk_lcd_panel_read_id(panel, &id);

/* 发任意 DCS 命令（write） */
uint8_t param[2] = {0x55, 0xAA};
bk_lcd_panel_tx_param(panel, 0x29 /* DISPON */, NULL, 0);
bk_lcd_panel_tx_param(panel, 0xC0, param, 2);

/* 读回参数（仅 MIPI bus 支持） */
uint8_t dstat[3] = {0};
bk_lcd_panel_rx_param(panel, 0x09 /* RDDPM */, dstat, 3);

```

约束：`tx_param` 支持 MIPI DSI 与 SW SPI，HW SPI 不支持；`rx_param` 仅 MIPI DSI 支持；
`read_id` / `rx_param` 须在 `bk_display_init()` 之后调用。


### [6.3 生产级集成参考](#id42 "#id42")

`projects/common_components/multimedia_device_service/src/app_display.c`
展示了产品级用法，相比示例工程多了：


- 全局 `display_ctx_t` + 互斥锁保护并发 bring-up/teardown/flush。

- `app_display_power_enable()` 独占管理 VDDIO（`PM_AUXLDO_USER_DISPLAY`）。

- `ctlr_inited` / `ctlr_opened` 标志 + 完整 teardown ladder：任意一步失败都能精确回滚。

- 背光在最后一刻打开；LT8912B 桥仅需额外用 `bk_lcd_lt8912b_set_io_pins()` 转发其私有
  I2C 引脚，时钟源仍走默认。


## [7. 线程模型与并发](#id43 "#id43")


- **单 flush 流**：同一个 ctlr 句柄不要并发 flush。示例工程用一个专用刷帧线程；
  生产代码用顶层互斥包住刷帧。

- **bring-up / tear-down 期间**不要让其他线程并发 flush。

- **ioctl 必须在 flush 停下来时调**（见 §6.1）。

- `bk_display_flush` 内部加锁并维护 inflight 计数；把帧交给它之后**所有权归 DPU**，
  回调返回前不要碰该帧。

- `bk_display_deinit` 内部会等所有 inflight flush 落盘后再撕 DPU，可放心调用。

- DSI / SW-SPI 总线与 panel ops 本身无锁，期望应用层串行调用 `tx_param` / `rx_param`。


## [8. 电源与时钟须知](#id44 "#id44")


**电源**


- `PM_AUXLDO_USER_DISPLAY` 只允许两处投票：

  1. 应用层 —— 面板 VDDIO 1.8V（如 `app_display_power_enable` / `bk_lodoen_enable`）。
  2. `bk_display_dsi_bus.c` 内部 —— DSI D-PHY 模拟轨 2.8V / 3V（应用层不要碰）。

- 中间层（组件 / panel-common）**严禁**直接投票面板供电。

- 上电顺序：**VDDIO → bus_new → panel reset/init → ctlr open → 背光**；下电反序。


**时钟源**

时钟源由总线 / panel-common 内部选定并写入 panel 句柄，控制器直接读取，`dpu_config`
不含 `clk_src` 字段：


- 普通 MIPI 屏：默认 `DPU_CLK_SRC_DPHY_DPLL`；panel init 时若 PLL 求解失败自动回落
  `DPU_CLK_SRC_SYSCLK`。

- RGB 屏：固定 `DPU_CLK_SRC_SYSCLK`。

应用层通常无需干预；如需强制指定，在 `bk_display_dsi_bus_new` 之后、`bk_lcd_mipi_panel_new`
之前调用 `bk_display_bus_set_clock_src(bus, clk_src)`。


## [9. 错误码约定](#id45 "#id45")


- `bk_display_*` 一族返回 `avdk_err_t`（`AVDK_ERR_OK` / `_INVAL` / `_NO_MEM` /
  `_UNSUPPORTED` / `_GENERIC` / `_BUSY` …）。

- `bk_lcd_panel_*` 一族返回 `bk_err_t`（`BK_OK` / `BK_ERR_NULL_PARAM` /
  `BK_ERR_NOT_SUPPORT` / `BK_ERR_NO_MEM`）。

- `bk_display_bus_*` 公有派发：`flush` / `delete` / `set_clock_src` 返回 `avdk_err_t`；
  `tx_param` / `rx_param` 返回 `bk_err_t`。

- 用伞头 `<components/bk_display.h>` 后两套类型都可见；不要假定 0 == 成功，永远显式比较
  `AVDK_ERR_OK` / `BK_OK`。


## [10. 常见问题 FAQ](#id46 "#id46")


**Q1：调 bk_display_flush 返回 AVDK_ERR_GENERIC，日志 “display is not active”**

状态机问题：忘了 `bk_display_open`，或在 `close` / `deinit` 之后又 flush。INITED 态
首次 flush 会被自动提升到 ACTIVE 并打 WARN——不要依赖，正经流程显式 open。


**Q2：屏完全不亮，也没报错**

1. 用 `bk_lcd_panel_read_id` 确认屏能通信（须在 `bk_display_init()` 之后调）。读不到 →
   检查 VDDIO、reset 引脚、bus 配置。
2. ID 对但黑屏 → 检查屏描述符 timing / 像素时钟、背光 GPIO。
3. 闪屏 / 颜色错乱 → 检查 `dpu_cfg.video.format` 与帧 buffer 实际格式是否一致、
   `decompress` 是否与帧编码匹配。


**Q3：bk_lcd_mipi_panel_new 返回 BK_ERR_NULL_PARAM**

多半是描述符没找到（按名字查时拼错），或忘了在 menuconfig 勾选对应屏的 Kconfig 选项导致描述符
没编进固件。用 `bk_lcd_get_mipi_panel_list()` 可验证当前 build 包含哪些屏。


**Q4：bk_display_spi_bus_new 返回 AVDK_ERR_INVAL**

检查 `clk_pin` / `csx_pin` / `sda_pin` 都非 0，且 `cmd_width` 为 8 或 16
（应当 = `panel->spi_cmd_16bit ? 16 : 8`）。


**Q5：运行期切像素格式后屏花了**

没遵循 §6.1：必须先停 flush 线程，ioctl 成功后再启线程，并同步本地 width/height/format 状态。


**Q6：deinit 后再次 bk_display_dsi_bus_new 报 mipi_dsi 初始化失败**

关闭路径不完整：必须 `bk_display_delete(ctlr)` → `bk_lcd_panel_delete(panel)` →
`bk_display_bus_delete(bus)`。漏任一步都会让 PMU / D-PHY 投票计数错乱。


**Q7：能否不建 bus 直接 flush？**

不能。flush 把帧推进 DPU，DPU 通过 bus 把像素送出——必须先把整条链 bring-up 完整。


## [相关文档](#id47 "#id47")


- 支持的 LCD 设备：[支持的 LCD 设备](supported_lcd_devices.md "supported_lcd_devices.md")

- 新增 MIPI panel：[如何新增 MIPI DSI Panel（BK7259）](how_to_add_mipi_panel.md "how_to_add_mipi_panel.md")

- 新增 RGB panel：[如何新增 RGB Panel（BK7259）](how_to_add_rgb_panel.md "how_to_add_rgb_panel.md")

- QSPI 屏：[qspi_lcd_display](qspi_lcd_display.md "qspi_lcd_display.md")；SPI 屏：[spi_lcd_display](spi_lcd_display.md "spi_lcd_display.md")

- 接口速查（Doxygen 自动生成）：`api-reference/multimedia/bk_display`

参考工程：

| 工程路径 | 用途 |
| --- | --- |
| `projects/multimedia/mipi_lcd_example/` | 最小 MIPI demo + CLI 控制 + 运行期 ioctl |
| `projects/multimedia/rgb_lcd_example/` | RGB SW SPI demo |
| `projects/common_components/multimedia_device_service/src/app_display.c` | 生产质量的 MIPI bring-up / teardown |
| `projects/multimedia/doorbell/` | `multimedia_device_service` 的实际使用方 |
