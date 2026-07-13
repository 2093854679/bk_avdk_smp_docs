# 如何新增 RGB Panel（BK7259）


面向 **新增 RGB 屏驱动** 的开发者。MIPI 屏见同目录
:   [如何新增 MIPI DSI Panel（BK7259）](how_to_add_mipi_panel.md "how_to_add_mipi_panel.md") 。 整个过程：**1 个 .c 文件 + 1 个
    Kconfig 入口 + 1 个 cmake 入口 + 应用层引用 1 个符号**。 无需修改
    `bk_display` / 链接脚本 / 寄存器。

目录

1. [BK7259 RGB 屏的两条通道](#1-bk7259-rgb-屏的两条通道 "#1-bk7259-rgb-屏的两条通道")
2. [总流程](#2-总流程 "#2-总流程")
3. [Step 1：从 datasheet 收集字段](#3-step-1从-datasheet-收集字段 "#3-step-1从-datasheet-收集字段")
4. [Step 2：新建 panel 驱动文件](#4-step-2新建-panel-驱动文件 "#4-step-2新建-panel-驱动文件")
5. [Step 3：Kconfig 声明](#5-step-3kconfig-声明 "#5-step-3kconfig-声明")
6. [Step 4：config.cmake 加入构建](#6-step-4configcmake-加入构建 "#6-step-4configcmake-加入构建")
7. [Step 5：工程启用 + 应用层使用](#7-step-5工程启用--应用层使用 "#7-step-5工程启用--应用层使用")
8. [描述符字段速查表](#8-描述符字段速查表 "#8-描述符字段速查表")
9. [init_cmds 编写规则（含 9-bit vs 4-byte 包
   SPI）](#9-init_cmds-编写规则含-9-bit-vs-4-byte-包-spi "#9-init_cmds-编写规则含-9-bit-vs-4-byte-包-spi")
10. [custom_reset / reset_timing](#10-custom_reset--reset_timing "#10-custom_reset--reset_timing")
11. [现有 panel 一览](#11-现有-panel-一览 "#11-现有-panel-一览")
12. [应用代码模板](#12-应用代码模板 "#12-应用代码模板")
13. [验证清单 & FAQ](#13-验证清单--faq "#13-验证清单--faq")

1. BK7259 RGB 屏的两条通道

| 通道 | 用途 | 物理形式 |
| --- | --- | --- |
| **像素通道**（24-bit RGB） | 持续输出像素数据 | 24 根 RGB 数据线 + HSYNC/VSYNC/DE/PCLK，由 DPU 直接驱动 |
| **配置通道**（SW SPI，bit-bang） | 上电时下发屏厂初始化命令 | CSX / SDA / CLK + RESET，4 根 GPIO 软件位敲 |

像素通道随 DPU bring-up 自动 pinmux；配置通道的 3 根 SPI GPIO 由你在
`bk_display_spi_bus_config_t` 中传入，RESET 引脚由 `bk_lcd_panel_config_t`
传入。

> **没有** `bk_display_rgb_bus_new()` 这个 API。RGB 屏的配置通道复用
> SPI 总线后端，作为 GPIO bit-bang 配置通道，仅承担寄存器写。

2. 总流程


```
1) ap/components/bk_peripheral/src/lcd/rgb/lcd_rgb_<vendor>_<WxH>.c
     填 bk_display_rgb_panel_t + 用 BK_LCD_PANEL_DEVICE_SECTION 注册
2) rgb/Kconfig         加 CONFIG_LCD_<NAME>
3) rgb/config.cmake    条件加入源文件
4) 工程 defconfig      CONFIG_LCD_<NAME>=y
5) 应用层              extern 该 panel，喂给 bk_lcd_rgb_panel_new()

```

参考工程：`projects/multimedia/rgb_lcd_example/`。

3. Step 1：从 datasheet 收集字段

| 项 | 写入字段 |
| --- | --- |
| 分辨率 W×H | `timing.h_size` / `timing.v_size` |
| PCLK 频率（典型 20–60 MHz） | `pixel_clock_hz`（用宏 `BK_RGB_PIXEL_CLK_HZ(mhz)`，如 `BK_RGB_PIXEL_CLK_HZ(30)`） |
| H 时序 (脉宽/后沿/前沿) | `timing.hsync_pulse_width` / `hsync_back_porch` / `hsync_front_porch` |
| V 时序 (脉宽/后沿/前沿) | `timing.vsync_pulse_width` / `vsync_back_porch` / `vsync_front_porch` |
| 配置 SPI 协议 | `spi_cmd_16bit`（**0 = 9-bit SPI；1 = 4-byte 包**，见 §9） |
| 初始化命令序列 | `init_cmds` |
| ID 寄存器（可选） | `read_id_regs` / `read_id_bytes` / `id` |

帧率估算：


```
fps = pixel_clock_hz
       ÷ (h_size + h_pulse + h_back + h_front)
       ÷ (v_size + v_pulse + v_back + v_front)

```

例：`BK_RGB_PIXEL_CLK_HZ(30), 480×854, ΣH=576/ΣV=904` →
`30M / 576 / 904 ≈ 57 Hz`。

> 与 MIPI 屏不同，**RGB 屏的 ``pixel_clock_hz``
> 必填**，否则像素时钟不对会撕裂/闪屏。

4. Step 2：新建 panel 驱动文件

路径规范：


```
ap/components/bk_peripheral/src/lcd/rgb/lcd_rgb_<vendor>_<WxH>.c

```


```
// Copyright 2020-2021 Beken

/**

 * @file lcd_rgb_<vendor>_<WxH>.c

 * @brief <Vendor> RGB Panel Driver (<W>x<H>)

 */

#include <components/bk_lcd_panel.h>
#include <common/avdk_pixel_types.h>

#if CONFIG_LCD_<VENDOR_TAG>

/* 1) 初始化命令序列（走 SW SPI 配置通道；按 datasheet 顺序逐条填入） */
static const lcd_rgb_spi_init_cmd_t <vendor>_rgb_<WxH>_init_cmds[] = {
    {0xFF, (const uint8_t []){0x77,0x01,0x00,0x00,0x13}, 5},
    {0xEF, (const uint8_t []){0x08}, 1},
    /* ... 厂家配置命令省略 ... */

    {0x3A, (const uint8_t []){0x55}, 1},          /* Pixel Format: 0x55 = RGB565 */
    {0x36, (const uint8_t []){0x10}, 1},          /* MADCTL */

    /* delay：cmd=0x00, data[0]=毫秒数, data_len=0xFF */
    {0x11, NULL, 0},                              /* SLPOUT */
    {0x00, (const uint8_t []){120}, 0xFF},       /* delay 120ms */
    {0x29, NULL, 0},                              /* DISPON */

    {0x00, NULL, 0}                               /* 结束标记，必填 */
};

/* 2) ID 寄存器列表（可选） */
static const uint8_t <vendor>_rgb_<WxH>_read_id_regs[] = {0xA1, 0};

/* 3) Panel 描述符 */
const bk_display_rgb_panel_t lcd_device_<vendor>_rgb_<WxH> = {
    .id            = 0x9903,
    .name          = "<vendor>_rgb_<WxH>",
    .pixel_clock_hz = BK_RGB_PIXEL_CLK_HZ(30),    /* DPI PCLK，必填；30 = 30MHz */
    .timing = {
        .h_size            = 480,
        .v_size            = 854,
        .hsync_pulse_width = 2,
        .vsync_pulse_width = 2,
        .hsync_back_porch  = 46,
        .hsync_front_porch = 48,
        .vsync_back_porch  = 24,
        .vsync_front_porch = 24,
    },
    .init_cmds     = <vendor>_rgb_<WxH>_init_cmds,
    .spi_cmd_16bit = 0,                           /* 0 = 9-bit SPI；1 = 4-byte 包，见 §9 */
    .read_id_regs  = <vendor>_rgb_<WxH>_read_id_regs,
    .read_id_bytes = 2,
    .reset_active_level = false,                  /* RST 有效电平：false=低有效 */
    /* .reset_timing = {...}   <-- 可选，回落到 BK_DISPLAY_RESET_*_MS_RGB_DEFAULT */
    .reset         = bk_lcd_rgb_default_reset,    /* 默认 GPIO H/L/H；NULL=跳过；自定义见 §10 */
    .init          = bk_lcd_rgb_default_init,     /* 默认下发 init_cmds；NULL=跳过 */
};

/* 4) 段注册（必须）：第 3 参数用 BK_LCD_PANEL_BUS_RGB */
BK_LCD_PANEL_DEVICE_SECTION(lcd_device_<vendor>_rgb_<WxH>,
                            "<vendor>_rgb_<WxH>",
                            BK_LCD_PANEL_BUS_RGB);

#endif /* CONFIG_LCD_<VENDOR_TAG> */

```


## 命名规范（强烈建议）

| 项 | 模式 |
| --- | --- |
| 文件名 | `lcd_rgb_<vendor>_<WxH>.c` |
| `init_cmds` 数组 | `<vendor>_rgb_<WxH>_init_cmds` |
| `read_id_regs` 数组 | `<vendor>_rgb_<WxH>_read_id_regs` |
| 描述符符号 | `lcd_device_<vendor>_rgb_<WxH>` 或 `<vendor>_rgb_panel`（现有混用） |
| 段注册 name | `"<vendor>_rgb_<WxH>"` |
| Kconfig 项 | `CONFIG_LCD_<VENDOR>`（参考现有命名约定，多为 IC 名） |

5. Step 3：Kconfig 声明

文件：`ap/components/bk_peripheral/src/lcd/rgb/Kconfig`


```
config LCD_<VENDOR_TAG>
    depends on LCD_RGB
    bool "Enable LCD_<VENDOR_TAG> API"
    default n

```

`depends on LCD_RGB` 必填。

6. Step 4：config.cmake 加入构建

文件：`ap/components/bk_peripheral/src/lcd/rgb/config.cmake`


```
if (CONFIG_LCD_<VENDOR_TAG>)
    list(APPEND RGB_LCD_DEVICE_FILES ${RGB_LCD_PATH}/lcd_rgb_<vendor>_<WxH>.c)
endif()

```

7. Step 5：工程启用 + 应用层使用


## 7.1 启用

工程 defconfig 中加：


```
CONFIG_LCD_<VENDOR_TAG>=y

```

或在 build 目录 `make menuconfig` → BK_PERIPHERAL → RGB LCD 勾选。


## 7.2 应用层引用


**方式 A：固定单屏 — 直接 extern**


```
extern const bk_display_rgb_panel_t lcd_device_<vendor>_rgb_<WxH>;
const bk_display_rgb_panel_t *panel = &lcd_device_<vendor>_rgb_<WxH>;

```


**方式 B：CLI/可换屏 — 段注册按 name 查找**


```
const bk_display_rgb_panel_t *panel =
    bk_lcd_find_rgb_panel_by_name("<vendor>_rgb_<WxH>");

```

或枚举：


```
const bk_display_rgb_panel_t *list[8];
uint32_t n = bk_lcd_get_rgb_panel_list(list, 8);

```

完整 bring-up 链见 §12。

8. 描述符字段速查表

`bk_display_rgb_panel_t`（声明于
`<components/bk_lcd_panel_types.h>`，包含在
`<components/bk_lcd_panel.h>` 中）：

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `id` | `uint32_t` | 推荐 | IC ID，调试 `bk_lcd_panel_read_id()` 校验 |
| `name` | `const char *` | **必填** | CLI/段查找标识；建议 `<vendor>_rgb_<WxH>` |
| `pixel_clock_hz` | `uint32_t` | **必填** | DPI PCLK（Hz），用宏 `BK_RGB_PIXEL_CLK_HZ(mhz)`；硬件取最接近的 PLL/分频 |
| `timing.h_size` / `.v_size` | `uint16_t` | **必填** | 水平/垂直有效像素 |
| `timing.hsync_*` | `uint16_t` | **必填** | hsync 脉宽/后沿/前沿（单位 pclk） |
| `timing.vsync_*` | `uint16_t` | **必填** | vsync 脉宽/后沿/前沿（单位 line） |
| `init_cmds` | `const lcd_rgb_spi_init_cmd_t *` | **必填** | 命令序列，**必须**以 `{0x00, NULL, 0}` 结尾 |
| `spi_cmd_16bit` | `uint8_t` | **必填** | 配置 SPI 协议选择：`0` = 9-bit SPI；`1` = 4-byte 包，详见 §9 |
| `read_id_regs` | `const uint8_t *` | 可选 | ID 寄存器地址数组，以 `0` 结尾 |
| `read_id_bytes` | `uint8_t` | 与 `read_id_regs` 配套 | 1~3 |
| `reset_active_level` | `bool` | 推荐 | RST 有效电平：`true` = 高有效，`false` = 低有效 |
| `reset_timing` | `bk_display_reset_timing_t` | 可选 | 三段（`idle_ms`/`active_ms`/`release_ms`），回落到 `BK_DISPLAY_RESET_*_MS_RGB_DEFAULT` |
| `reset` | `bk_err_t (*)(bk_avdk_lcd_panel_t *)` | 推荐 | reset 钩子；填 `bk_lcd_rgb_default_reset` 走通用 H/L/H，`NULL` 跳过，或自定义，见 §10 |
| `init` | `bk_err_t (*)(bk_avdk_lcd_panel_t *)` | 推荐 | init 钩子；填 `bk_lcd_rgb_default_init` 通过 SW SPI 派发 `init_cmds`，`NULL` 跳过 |

`bk_lcd_panel_config_t`（`bk_lcd_rgb_panel_new()` 第 2
参，声明于 `<components/bk_lcd_panel_types.h>`）：

| 字段 | 说明 |
| --- | --- |
| `reset_pin` | RESET GPIO（`int8_t`，`-1` 禁用） |

该结构现在**只有** `reset_pin`。RST 有效电平 `reset_active_level`
已移到 panel 描述符；历史的 `clk_pin` / `csx_pin` / `sda_pin` /
`vendor_config` / `rgb_ele_order` / `data_endian` / `bits_per_pixel`
等字段已**全部移除**。配置 SPI 的 3 根 GPIO 改由
`bk_display_spi_bus_config_t` 传，见 §12 模板。

RGB 屏的 `.init` 默认用 `bk_lcd_rgb_default_init` 通过 SW SPI 派发
`init_cmds`，一般无需自定义。

9. `init_cmds` 编写规则（含 9-bit vs 4-byte 包 SPI）

`lcd_rgb_spi_init_cmd_t`：


```
typedef struct {
    uint16_t      cmd;       /* 9-bit 模式用低 8 位；4-byte 模式用完整 16 位 */
    const void   *data;      /* 9-bit: const uint8_t *；4-byte: const uint16_t *；无参 NULL */
    uint8_t       data_len;  /* 参数个数；0xFF 时表示 delay */
} lcd_rgb_spi_init_cmd_t;

```


## 9.1 4 种合法形式

| 形式 | 写法（9-bit / `spi_cmd_16bit=0`） | 含义 |
| --- | --- | --- |
| 带参命令 | `{0x36, (const uint8_t []){0x10}, 1}` | 命令 0x36 + 1 字节参数 |
| 无参命令 | `{0x11, NULL, 0}` | SLPOUT |
| 延迟 N ms | `{0x00, (const uint8_t []){N}, 0xFF}` | 不发任何命令，等 N 毫秒 |
| 结束标记（必填） | `{0x00, NULL, 0}` |  |


## 9.2 9-bit SPI（`spi_cmd_16bit = 0`）

适用：ST7701S / ST7701SN / GC9503V / AML01 / ST7282 / HX8282 / H050IWV /
MD0430R / MD0700R …

线上波形：`[D/C bit] [byte]`，bit-bang。 `cmd` 字段写低 8
位，`data` 用 `const uint8_t[]`：


```
{0xFF, (const uint8_t []){0x77,0x01,0x00,0x00,0x13}, 5},
{0x3A, (const uint8_t []){0x55}, 1},

```


## 9.3 4-byte 包 SPI（`spi_cmd_16bit = 1`）

适用：NT35510 / NT35512。

线上格式按完整 16-bit 命令字 + 16-bit data，`cmd` 写完整 16 位（如
`0xF000`）， `data` 用 `const uint16_t[]`，多数寄存器是单字 1
word：


```
{0xF000, (const void *)(const uint16_t []){0x0055}, 1},
{0xF001, (const void *)(const uint16_t []){0x00AA}, 1},
{0xB600, (const void *)(const uint16_t []){0x0034}, 1},

```

delay 形式两种模式相同：`{0x00, (const uint8_t []){N}, 0xFF}`。


## 9.4 常见误用


- ❌ `{0x11, (const uint8_t []){120}, 0xFF}`——驱动不会解析”命令 +
  延时”复合形式；拆成两条：

  ```
  {0x11, NULL, 0},
  {0x00, (const uint8_t []){120}, 0xFF},
  ```

- ❌ delay 的 `data` 不能是 `NULL`；`cmd` 必须是 `0x00`

- ❌ 普通命令的 `data_len` 不能等于 `0xFF`（会被当 delay）

- ❌ 4-byte 模式忘了把 `data` 改成 `uint16_t[]`——驱动会按 16-bit
  单元读

10. `custom_reset` / `reset_timing`


## 10.1 优先用 `reset_timing` 调时序

通用 reset 波形分三段：IDLE → ACTIVE → RELEASE。RGB 默认值（ms）：

| 段 | 宏 | 默认 |
| --- | --- | --- |
| `idle_ms` | `BK_DISPLAY_RESET_IDLE_MS_RGB_DEFAULT` | 10 |
| `active_ms` | `BK_DISPLAY_RESET_ACTIVE_MS_RGB_DEFAULT` | 120 |
| `release_ms` | `BK_DISPLAY_RESET_RELEASE_MS_RGB_DEFAULT` | 60 |

要改时序，填 `reset_timing` 即可（零字段保持默认）：


```
.reset_timing = {
    .active_ms  = 200,   /* 加长 reset 脉冲 */
    .release_ms = 100,
},

```


## 10.2 仅在波形不是 H/L/H 三段时才写 `custom_reset`


```
/* 赋给描述符的 .reset 字段；签名只有 panel 一个参数 */
static bk_err_t my_reset(bk_avdk_lcd_panel_t *panel)
{
    bk_gpio_set_output_high(MY_RST_PIN);
    rtos_delay_milliseconds(50);
    bk_gpio_set_output_low (MY_RST_PIN);
    rtos_delay_milliseconds(20);
    bk_gpio_set_output_high(MY_RST_PIN);
    rtos_delay_milliseconds(200);
    return BK_OK;
}

```

自定义 `.reset` 非 NULL 时**完全替换**默认波形，`reset_timing`
被旁路。

11. 现有 panel 一览

| 文件 | IC | 分辨率 | PCLK | `spi_cmd_16bit` | Kconfig |
| --- | --- | --- | --- | --- | --- |
| `lcd_rgb_aml01_720x1280.c` | AML01 | 720×1280 | 60M | 0 | `LCD_AML01` |
| `lcd_rgb_gc9503v_480x800.c` | GC9503V | 480×800 |  | 0 | `LCD_GC9503V` |
| `lcd_rgb_h050iwv_800x480.c` | H050IWV | 800×480 |  | 0 | `LCD_H050IWV` |
| `lcd_rgb_hx8282_1024x600.c` | HX8282 | 1024×600 |  | 0 | `LCD_HX8282` |
| `lcd_rgb_md0430r_800x480.c` | MD0430R | 800×480 |  | 0 | `LCD_MD0430R` |
| `lcd_rgb_md0700r_1024x600.c` | MD0700R | 1024×600 |  | 0 | `LCD_MD0700R` |
| `lcd_rgb_nt35510_480x854.c` | NT35510 | 480×854 | 20M | **1** | `LCD_NT35510` |
| `lcd_rgb_nt35512_480x800.c` | NT35512 | 480×800 |  | **1** | `LCD_NT35512` |
| `lcd_rgb_st7282_480x272.c` | ST7282 | 480×272 |  | 0 | `LCD_ST7282` |
| `lcd_rgb_st7701s_480x480.c` | ST7701S | 480×480 |  | 0 | `LCD_ST7701S` |
| `lcd_rgb_st7701sn_480x854.c` | ST7701SN | 480×854 | 30M | 0 | `LCD_ST7701SN` |

建议挑分辨率/IC 最接近的现有文件做模板。

12. 应用代码模板

完整工程参考
`projects/multimedia/rgb_lcd_example/ap/src/lcd_example_rgb.c`。
单文件最小化版本：


```
#include <components/bk_display.h>   /* 伞头：bus + panel + display ctlr */

extern const bk_display_rgb_panel_t lcd_device_<vendor>_rgb_<WxH>;

static bk_display_bus_handle_t    s_spi_bus;
static bk_avdk_lcd_panel_handle_t s_panel;
static bk_display_ctlr_handle_t   s_ctlr;

int my_rgb_lcd_open(void)
{
    const bk_display_rgb_panel_t *panel = &lcd_device_<vendor>_rgb_<WxH>;

    /* 1) 建配置通道（SW SPI bit-bang）。cmd_width 必须按 panel 选择：

     *      panel->spi_cmd_16bit == 0 -> cmd_width = 8  (9-bit SPI)

     *      panel->spi_cmd_16bit == 1 -> cmd_width = 16 (4-byte 包)        */
    bk_display_spi_bus_config_t cfg = {
        .clk_pin   = GPIO_8,
        .csx_pin   = GPIO_28,
        .sda_pin   = GPIO_9,
        .cmd_width = panel->spi_cmd_16bit ? 16 : 8,   /* 必须按 panel 选择 */
    };
    bk_display_spi_bus_new(&s_spi_bus, &cfg);

    /* 2) 建 panel（reset/init 由 bk_display_init() 内部驱动，无需手动调） */
    bk_lcd_panel_config_t panel_config = {
        .reset_pin = GPIO_6,                    /* RST 有效电平在 panel 描述符里 */
    };
    bk_lcd_rgb_panel_new(s_spi_bus, &panel_config, panel, &s_panel);

    /* 3) DPU；timing / 像素时钟由控制器从 panel 句柄自取，dpu_cfg 只填 video 层 */
    bk_display_dpu_config_t dpu_cfg = {
        .video.enable     = true,
        .video.format     = BK_PIXEL_FORMAT_RGB565,
        .video.decompress = false,
    };
    bk_display_dpu_ctlr_new(&s_ctlr, s_panel, &dpu_cfg);   /* 3 参：含 panel 句柄 */
    bk_display_init(s_ctlr);                                /* 内部跑 .reset/.init */
    bk_display_open(s_ctlr);

    /* 4) 板上背光 GPIO 放最后（按板子接线） */
    return 0;
}

int my_rgb_lcd_close(void)
{
    /* 严格逆序 */
    bk_display_close (s_ctlr);
    bk_display_deinit(s_ctlr);
    bk_display_delete(s_ctlr);        s_ctlr    = NULL;
    bk_lcd_panel_delete(s_panel);     s_panel   = NULL;
    bk_display_bus_delete(s_spi_bus); s_spi_bus = NULL;
    return 0;
}

```

13. 验证清单 & FAQ


## 13.1 验证顺序

1. 编译通过；`bk_lcd_get_rgb_panel_list()` 中能看到你的 `name`
2. 示波器看 PCLK：`bk_display_open()` 后稳定时钟（约
   `pixel_clock_hz` 对应频率）
3. 示波器看 RESET：`bk_display_init()` 内部驱动 reset 后波形
   idle→active→release 三段
4. 逻辑分析仪看配置 SPI（CSX/SDA/CLK）：`bk_display_init()` 内部派发的
   全部命令流正常
5. `bk_display_open()` 后送纯色帧整屏稳定无横纹
6. 渐变图无条纹/撕裂；R/G/B 顺序正确（错位见 §13.2）
7. 100 次 open/close 不死机不漏内存


## 13.2 常见问题速查

| 现象 | 排查首项 | 排查次项 |
| --- | --- | --- |
| 整屏黑、电流正常 | RESET 时序 / init 命令是否真的下发（抓 SPI） | RGB 像素脚 pinmux：PCLK 是否在跳 |
| 整屏黑、电流异常 | 屏 VCC / 背光 LDO | 板上 LDO 使能 |
| 整屏白底/雪花 | DPI clock 太高或 porch 偏小 | 降 `pixel_clock_hz` 或重算 porch |
| 规则横纹 | h porch 偏小，DPU FIFO underflow | 加大 porch；确认 DPU QoS=3 |
| 规则竖纹/抖动 | PCLK 极性与屏采样沿不一致 | 屏 datasheet 看 PCLK 极性（本平台不开放反相，找驱动同事） |
| R/B 互换 | 屏 BGR/RGB 寄存器没设对 | 检查 `init_cmds` 中 0x36 (MADCTL) |
| `read_id` 全 0 / 全 F | 屏 VCC / 配置 SPI 引脚错 | 万用表测 CSX/SDA/CLK 是否到屏脚 |
| init 全发完屏没反应 | `spi_cmd_16bit` 选错（屏要 4-byte 包但填了 0） | 抓 SPI 看实际命令字宽 |
| 4-byte 模式参数花掉 | `data` 数组类型仍是 `uint8_t[]` | 改成 `(const void *)(const uint16_t []){...}` |
| 中间某条命令后屏挂 | 该命令前缺 delay | 该命令前插 `{0x00, (const uint8_t []){N}, 0xFF}` |
| 撕裂 | flush 频率高于 panel 实际帧率 | 降 flush 频率或 `pixel_clock_hz` 降一档 |
| 切像素格式后花屏 | 切换瞬间仍有 inflight flush | 切换前停 flush 线程 → ioctl → 再启 |
| close 后再 open 卡死 | `bk_display_bus_delete` 是否漏 | RGB 像素脚 pinmux 未释放 |
| menuconfig 看不到新 panel | Kconfig `depends on LCD_RGB` 是否漏 | `config LCD_xxx` 名字拼错 |
| 段注册取不到 panel | `BK_LCD_PANEL_DEVICE_SECTION` 是否漏 | 第 3 参须为 `BK_LCD_PANEL_BUS_RGB` |
| 编译时找不到结构体 | 头文件应为 `<components/bk_lcd_panel.h>` | `#if CONFIG_LCD_xxx` 与 Kconfig 名一致 |

参考


- 模板源文件：`ap/components/bk_peripheral/src/lcd/rgb/lcd_rgb_st7701sn_480x854.c`

- 4-byte
  包参考：`ap/components/bk_peripheral/src/lcd/rgb/lcd_rgb_nt35510_480x854.c`

- 通用驱动：`ap/components/bk_display/src/panel/lcd_rgb_panel_common.c`

- 公有 API：`<components/bk_display.h>`（伞头）/
  `<components/bk_display_bus.h>` / `<components/bk_lcd_panel.h>`

- 公有类型：`<components/bk_lcd_panel_types.h>`

- 应用样例：`projects/multimedia/rgb_lcd_example/ap/src/lcd_example_rgb.c`
