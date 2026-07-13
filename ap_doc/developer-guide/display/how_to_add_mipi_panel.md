# 如何新增 MIPI DSI Panel（BK7259）


面向 **新增 MIPI 屏驱动** 的开发者。RGB 屏见同目录
:   [如何新增 RGB Panel（BK7259）](how_to_add_rgb_panel.md "how_to_add_rgb_panel.md") 。 整个过程：**1 个 .c 文件 + 1 个
    Kconfig 入口 + 1 个 cmake 入口 + 应用层引用 1 个符号**。 无需修改
    `bk_display` / 链接脚本 / 寄存器。

目录

1. [总流程](#1-总流程 "#1-总流程")
2. [Step 1：从 datasheet 收集字段](#2-step-1从-datasheet-收集字段 "#2-step-1从-datasheet-收集字段")
3. [Step 2：新建 panel 驱动文件](#3-step-2新建-panel-驱动文件 "#3-step-2新建-panel-驱动文件")
4. [Step 3：Kconfig 声明](#4-step-3kconfig-声明 "#4-step-3kconfig-声明")
5. [Step 4：config.cmake 加入构建](#5-step-4configcmake-加入构建 "#5-step-4configcmake-加入构建")
6. [Step 5：工程启用 + 应用层使用](#6-step-5工程启用--应用层使用 "#6-step-5工程启用--应用层使用")
7. [描述符字段速查表](#7-描述符字段速查表 "#7-描述符字段速查表")
8. [init_cmds 编写规则](#8-init_cmds-编写规则 "#8-init_cmds-编写规则")
9. [custom_reset / custom_init /
   reset_timing](#9-custom_reset--custom_init--reset_timing "#9-custom_reset--custom_init--reset_timing")
10. [桥接芯片（LT8912B）说明](#10-桥接芯片lt8912b说明 "#10-桥接芯片lt8912b说明")
11. [现有 panel 一览](#11-现有-panel-一览 "#11-现有-panel-一览")
12. [应用代码模板](#12-应用代码模板 "#12-应用代码模板")
13. [验证清单 & FAQ](#13-验证清单--faq "#13-验证清单--faq")

1. 总流程


```
1) ap/components/bk_peripheral/src/lcd/dsi/lcd_mipi_<vendor>_<WxH>.c
     填 bk_display_dsi_panel_t + 用 BK_LCD_PANEL_DEVICE_SECTION 注册
2) dsi/Kconfig         加 CONFIG_LCD_<VENDOR>_MIPI_<WxH>
3) dsi/config.cmake    条件加入源文件
4) 工程 defconfig      CONFIG_LCD_<VENDOR>_MIPI_<WxH>=y
5) 应用层              extern 该 panel 描述符，喂给 bk_lcd_mipi_panel_new()

```

参考工程：`projects/multimedia/doorbell/`、`projects/multimedia/mipi_lcd_example/`。

2. Step 1：从 datasheet 收集字段

| 项 | 写入字段 |
| --- | --- |
| 分辨率 W×H | `timing.h_size` / `timing.v_size` |
| 帧率 | `fps` |
| MIPI lane 数 | `n_lanes`（`DSI_ACTIVE_LANES_1` ~ `_4`） |
| H 时序 (脉宽/后沿/前沿) | `timing.hsync_pulse_width` / `hsync_back_porch` / `hsync_front_porch` |
| V 时序 (脉宽/后沿/前沿) | `timing.vsync_pulse_width` / `vsync_back_porch` / `vsync_front_porch` |
| 初始化命令序列 | `init_cmds` |
| ID 寄存器（可选） | `read_id_regs` / `read_id_bytes` / `id` |

经验估算：


- DPI 像素时钟 ≈
  `(h_size + h_porch_sum) × (v_size + v_porch_sum) × fps`

- DSI 单 lane bit-rate ≈
  `DPI clock × bits_per_pixel / n_lanes`，必须落在屏 spec 范围内

> **DSI 屏不需要填任何像素时钟字段**——DPI 时钟由 fps +
> 总像素数自动算；RGB 屏才需在描述符里填 `pixel_clock_hz`。

3. Step 2：新建 panel 驱动文件

路径规范：


```
ap/components/bk_peripheral/src/lcd/dsi/lcd_mipi_<vendor>_<WxH>.c

```


```
// Copyright 2020-2021 Beken

/**

 * @file lcd_mipi_<vendor>_<WxH>.c

 * @brief <Vendor> MIPI DSI Panel Driver (<W>x<H>)

 */

#include <components/bk_lcd_panel.h>
#include <driver/mipi_dsi_types.h>
#include <common/avdk_pixel_types.h>

#if CONFIG_LCD_<VENDOR>_MIPI_<WxH>

/* 1) 初始化命令序列（按 datasheet 顺序逐条填入） */
static const lcd_mipi_init_cmd_t <vendor>_mipi_<WxH>_init_cmds[] = {
    {0xFF, (const uint8_t []){0x77,0x01,0x00,0x00,0x13}, 5},
    {0xEF, (const uint8_t []){0x08}, 1},
    /* ... 厂家配置命令省略 ... */

    /* delay：cmd=0x00, data[0]=毫秒数, data_len=0xFF */
    {0x00, (const uint8_t []){120}, 0xFF},

    {0x11, NULL, 0},                          /* SLPOUT（无参） */
    {0x00, (const uint8_t []){120}, 0xFF},   /* delay 120ms */
    {0x29, NULL, 0},                          /* DISPON（无参） */

    {0x00, NULL, 0}                           /* 结束标记，必填 */
};

/* 2) ID 寄存器列表（可选；不填则 bk_lcd_panel_read_id() 不可用） */
static const uint8_t <vendor>_mipi_<WxH>_read_id_regs[] = {0xA1, 0};

/* 3) Panel 描述符 */
const bk_display_dsi_panel_t lcd_device_<vendor>_mipi_<WxH> = {
    .id            = 0x9903,
    .name          = "<vendor>_mipi_<WxH>",
    .n_lanes       = DSI_ACTIVE_LANES_2,
    .fps           = 30,
    .timing = {
        .h_size            = PIXEL_480,
        .v_size            = PIXEL_640,
        .hsync_pulse_width = 5,
        .vsync_pulse_width = 5,
        .hsync_back_porch  = 30,
        .hsync_front_porch = 30,
        .vsync_back_porch  = 20,
        .vsync_front_porch = 20,
    },
    .init_cmds     = <vendor>_mipi_<WxH>_init_cmds,
    .read_id_regs  = <vendor>_mipi_<WxH>_read_id_regs,
    .read_id_bytes = 2,
    .reset_active_level = false,              /* RST 有效电平：false=低有效 */
    /* .reset_timing = {...}   <-- 可选，零字段回落到 BK_DISPLAY_RESET_*_MS_DEFAULT */
    .reset         = bk_lcd_mipi_default_reset, /* 默认 GPIO H/L/H；NULL=跳过；自定义见 §9 */
    .init          = bk_lcd_mipi_default_init,  /* 默认下发 init_cmds；NULL=跳过；桥接 IC 见 §9/§10 */
};

/* 4) 段注册（必须）：第 3 参数用 BK_LCD_PANEL_BUS_DSI */
BK_LCD_PANEL_DEVICE_SECTION(lcd_device_<vendor>_mipi_<WxH>,
                            "<vendor>_mipi_<WxH>",
                            BK_LCD_PANEL_BUS_DSI);

#endif /* CONFIG_LCD_<VENDOR>_MIPI_<WxH> */

```


## 命名规范（强烈建议）

| 项 | 模式 |
| --- | --- |
| 文件名 | `lcd_mipi_<vendor>_<WxH>.c` |
| `init_cmds` 数组 | `<vendor>_mipi_<WxH>_init_cmds` |
| `read_id_regs` 数组 | `<vendor>_mipi_<WxH>_read_id_regs` |
| 描述符符号 | `lcd_device_<vendor>_mipi_<WxH>` |
| 段注册 name | `"<vendor>_mipi_<WxH>"` |
| Kconfig 项 | `CONFIG_LCD_<VENDOR>_MIPI_<WxH>` |

4. Step 3：Kconfig 声明

文件：`ap/components/bk_peripheral/src/lcd/dsi/Kconfig`


```
config LCD_<VENDOR>_MIPI_<WxH>
    depends on LCD_DSI
    bool "Enable LCD_<VENDOR>_MIPI_<WxH> API"
    default n

```

`depends on LCD_DSI` 必填，否则 menuconfig 中看不到。

5. Step 4：config.cmake 加入构建

文件：`ap/components/bk_peripheral/src/lcd/dsi/config.cmake`


```
if (CONFIG_LCD_<VENDOR>_MIPI_<WxH>)
    list(APPEND DSI_LCD_DEVICE_FILES ${DSI_LCD_PATH}/lcd_mipi_<vendor>_<WxH>.c)
endif()

```

6. Step 5：工程启用 + 应用层使用


## 6.1 启用

工程 defconfig 中加：


```
CONFIG_LCD_<VENDOR>_MIPI_<WxH>=y

```

或在 build 目录 `make menuconfig` → BK_PERIPHERAL → DSI LCD 勾选。


## 6.2 应用层引用


**方式 A：固定单屏 — 直接 extern**


```
extern const bk_display_dsi_panel_t lcd_device_<vendor>_mipi_<WxH>;
const bk_display_dsi_panel_t *panel = &lcd_device_<vendor>_mipi_<WxH>;

```


**方式 B：CLI/可换屏 — 段注册按 name 查找**


```
const bk_display_dsi_panel_t *panel =
    bk_lcd_find_mipi_panel_by_name("<vendor>_mipi_<WxH>");

```

或枚举：


```
const bk_display_dsi_panel_t *list[16];
uint32_t n = bk_lcd_get_mipi_panel_list(list, 16);

```

完整 bring-up 链见 §12。

7. 描述符字段速查表

`bk_display_dsi_panel_t`（声明于
`<components/bk_lcd_panel_types.h>`，包含在
`<components/bk_lcd_panel.h>` 中）：

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `id` | `uint32_t` | 推荐 | IC ID，调试用 `bk_lcd_panel_read_id()` 校验 |
| `name` | `const char *` | **必填** | CLI / 日志 / 段查找标识；建议 `<vendor>_mipi_<WxH>` |
| `n_lanes` | `uint8_t` | **必填** | `DSI_ACTIVE_LANES_1` ~ `_4` |
| `fps` | `uint8_t` | **必填** | 期望帧率，与 timing 一起决定 PHY bit-rate |
| `timing.h_size` / `.v_size` | `uint16_t` | **必填** | 水平/垂直有效像素，可用 `PIXEL_480` / `PIXEL_854` 等宏 |
| `timing.hsync_*` | `uint16_t` | **必填** | hsync 脉宽/后沿/前沿（单位 pclk） |
| `timing.vsync_*` | `uint16_t` | **必填** | vsync 脉宽/后沿/前沿（单位 line） |
| `init_cmds` | `const lcd_mipi_init_cmd_t *` | **必填** | 命令序列，**必须**以 `{0x00, NULL, 0}` 结尾 |
| `read_id_regs` | `const uint8_t *` | 可选 | ID 寄存器地址数组，以 `0` 结尾 |
| `read_id_bytes` | `uint8_t` | 与 `read_id_regs` 配套 | 1~3 字节 |
| `reset_active_level` | `bool` | 推荐 | RST 有效电平：`true` = 高有效，`false` = 低有效 |
| `reset_timing` | `bk_display_reset_timing_t` | 可选 | 三段（`idle_ms`/`active_ms`/`release_ms`），零字段回落到 `BK_DISPLAY_RESET_*_MS_DEFAULT` |
| `reset` | `bk_err_t (*)(bk_avdk_lcd_panel_t *)` | 推荐 | reset 钩子；填 `bk_lcd_mipi_default_reset` 走通用 H/L/H，`NULL` 跳过，或自定义，见 §9 |
| `init` | `bk_err_t (*)(bk_avdk_lcd_panel_t *)` | 推荐 | init 钩子；填 `bk_lcd_mipi_default_init` 下发 `init_cmds`，`NULL` 跳过，或自定义（桥接 IC），见 §9/§10 |

`bk_lcd_panel_config_t`（`bk_lcd_mipi_panel_new()` 第 2
参，声明于 `<components/bk_lcd_panel_types.h>`）：

| 字段 | 说明 |
| --- | --- |
| `reset_pin` | RESET GPIO（`int8_t`，`-1` 表示禁用） |

该结构现在**只有** `reset_pin`。RST 有效电平 `reset_active_level`
已移到 panel 描述符；历史的 `vendor_config` / `clk_src` / `clk_pin` /
`csx_pin` / `sda_pin` / `bits_per_pixel` 等字段已**全部移除**。

8. `init_cmds` 编写规则

`lcd_mipi_init_cmd_t`：


```
typedef struct {
    uint8_t       cmd;       /* DCS / MCS 命令字 */
    const void   *data;      /* 参数指针，无参传 NULL */
    uint8_t       data_len;  /* 参数长度（字节）；0xFF 时表示这是 delay */
} lcd_mipi_init_cmd_t;

```


## 4 种合法形式

| 形式 | 写法 |
| --- | --- |
| 带参命令 | `{0x36, (const uint8_t []){0x10}, 1}` |
| 无参命令 | `{0x11, NULL, 0}` |
| 延迟 N ms | `{0x00, (const uint8_t []){N}, 0xFF}` |
| 结束标记（必填） | `{0x00, NULL, 0}` |


## 常见误用


- ❌ `{0x11, (const uint8_t []){120}, 0xFF}`——驱动不会解析”命令 +
  延时”复合形式；拆成两条：

  ```
  {0x11, NULL, 0},
  {0x00, (const uint8_t []){120}, 0xFF},
  ```

- ❌ delay 的 `data` 不能是 `NULL`；`cmd` 必须是 `0x00`

- ❌ 普通命令的 `data_len` 不能等于 `0xFF`（会被当 delay）

9. `custom_reset` / `custom_init` / `reset_timing`


## 9.1 panel-common 的执行顺序

这里说的 `custom_reset` / `custom_init` 就是 panel 描述符里的
`.reset` / `.init` 函数指针字段，由 `bk_display_init()` 内部依次驱动，

**应用层无需手动调用**：


```
bk_display_init(ctlr) 内部依次执行：
    descriptor.reset:
        .reset != NULL ?  调用 .reset()（默认 bk_lcd_mipi_default_reset 跑 reset_timing H/L/H 波形）
                   NULL : 跳过 reset
    set_clock (依据 panel timing/fps/n_lanes)
    descriptor.init:
        .init  != NULL ?  调用 .init()（默认 bk_lcd_mipi_default_init 逐条派发 init_cmds[]）
                   NULL : 跳过 init

```

> **重要**：自定义 `.init` **替换** init_cmds
> 派发流程，而**不是**追加在其后。桥接芯片把整个 bring-up 写在
> `.init` 里时，`init_cmds` 通常留 NULL 或不被使用。


## 9.2 何时用 `reset_timing`

只想换默认 reset 时序、不想写函数：填 `reset_timing`：


```
.reset_timing = {
    .idle_ms    = 5,    /* 默认 BK_DISPLAY_RESET_IDLE_MS_DEFAULT=10 */
    .active_ms  = 20,   /* 默认 BK_DISPLAY_RESET_ACTIVE_MS_DEFAULT=10 */
    .release_ms = 200,  /* 默认 BK_DISPLAY_RESET_RELEASE_MS_DEFAULT=120 */
},

```

任意字段填 0 都使用默认值。


## 9.3 何时用 `custom_reset`

仅当 reset 波形不是 H/L/H 三段（例如双脉冲、需要异步 IO 控制）时：


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


## 9.4 何时用 `custom_init`

仅当 panel/桥接 IC 不通过 DSI DCS 完成 bring-up 时（如 LT8912B 走 I2C
配桥接寄存器）。`.init` 签名为 `bk_err_t (*)(bk_avdk_lcd_panel_t *panel)`，
可在函数内通过 `bk_lcd_panel_tx_param()` 等接口下发命令。

10. 桥接芯片（LT8912B）说明

LT8912B（MIPI-DSI → HDMI 桥）作为参考实现位于
`lcd_mipi_lt8912b_bridge.c`：


- 描述符 `lcd_device_lt8912b_mipi`，由 Kconfig
  选择具体分辨率（`LCD_LT8912B_RES_*`）

- 桥侧用 software I2C 配置，**SCL/SDA 不走 panel 描述符**，由
  Kconfig `CONFIG_LCD_LT8912B_PIN_SCL` / `_PIN_SDA`
  决定，应用层通过 `bk_lcd_lt8912b_set_io_pins()` 覆盖

- DPU 时钟源走 `DPU_CLK_SRC_SYSCLK`（旧 PHY 表）；普通 MIPI 屏走
  `DPU_CLK_SRC_DPHY_DPLL`

应用层片段（节选自 `app_display.c`）：


```
#if CONFIG_LCD_LT8912B_MIPI_BRIDGE
if (config->mipi.panel == &lcd_device_lt8912b_mipi) {
    bk_lcd_lt8912b_io_pins_t pins = {
        .scl_pin = config->mipi.pin_scl,
        .sda_pin = config->mipi.pin_sda,
    };
    bk_lcd_lt8912b_set_io_pins(&pins);
    /* LT8912B 桥走 SYSCLK：在 dsi_bus_new 之后、mipi_panel_new 之前调用 */
    bk_display_bus_set_clock_src(bus, DPU_CLK_SRC_SYSCLK);
}
#endif

```

桥接 IC 编写新模板时遵循同一思路：bridge 自带 I2C/SPI
通道在驱动文件内自包含初始化，外部仅通过统一的 panel 描述符 + 可选的”set
io pins”接口配置。

11. 现有 panel 一览

| 文件 | IC | 分辨率 | n_lanes | fps | Kconfig |
| --- | --- | --- | --- | --- | --- |
| `lcd_mipi_hx8394f_720x1280.c` | HX8394F | 720×1280 | 4 |  | `LCD_HX8394F_MIPI_720x1280` |
| `lcd_mipi_hx8399c_1080x1920.c` | HX8399C | 1080×1920 | 4 |  | `LCD_HX8399C_MIPI_1080x1920` |
| `lcd_mipi_fl7703np_720x1280.c` | FL7703NP | 720×1280 | 4 |  | `LCD_FL7703NP_MIPI_720x1280` |
| `lcd_mipi_gc9702_720x1280.c` | GC9702 | 720×1280 | 4 |  | `LCD_GC9702_MIPI_720x1280` |
| `lcd_mipi_jd9522z_1080x1920.c` | JD9522Z | 1080×1920 | 4 |  | `LCD_JD9522Z_MIPI_1080x1920` |
| `lcd_mipi_jd9855_360x390.c` | JD9855 | 360×390 | 1 | 60 | `LCD_JD9855_MIPI_360x390` |
| `lcd_mipi_st7701s_412x960.c` | ST7701S | 412×960 | 2 |  | `LCD_ST7701S_MIPI_412x960` |
| `lcd_mipi_st7701sn_360x640.c` | ST7701SN | 360×640 | 2 |  | `LCD_ST7701SN_MIPI_360x640` |
| `lcd_mipi_st7701sn_480x640.c` | ST7701SN | 480×640 | 1 | 30 | `LCD_ST7701SN_MIPI_480x640` |
| `lcd_mipi_st7701sn_480x854.c` | ST7701SN | 480×854 | 2 | 30 | `LCD_ST7701SN_MIPI_480x854` |
| `lcd_mipi_lt8912b_bridge.c` | LT8912B (MIPI→HDMI 桥) | 由 Kconfig 决定 | 2 |  | `LCD_LT8912B_MIPI_BRIDGE` |

建议挑分辨率/lane 数最接近的现有文件作模板。

12. 应用代码模板

完整产品代码参考
`projects/common_components/multimedia_device_service/src/app_display.c`。
单文件最小化版本：


```
#include <components/bk_display.h>   /* 伞头：bus + panel + display ctlr */

extern const bk_display_dsi_panel_t lcd_device_<vendor>_mipi_<WxH>;

static bk_display_bus_handle_t    s_bus;
static bk_avdk_lcd_panel_handle_t s_panel;
static bk_display_ctlr_handle_t   s_ctlr;

int my_mipi_lcd_open(void)
{
    /* 0) MIPI 屏需先投票 1.8V VDDIO（AUXLDO, PM_AUXLDO_USER_DISPLAY），此处略 */

    /* 1) 建 DSI 总线（config 传 NULL 即可） */
    bk_display_dsi_bus_new(&s_bus, NULL);

    /* 2) 时钟源可选：普通 MIPI 屏默认 DPU_CLK_SRC_DPHY_DPLL，PLL 不满足时

     *    自动回落 SYSCLK，无需调用；仅 LT8912B 等桥接 IC 才在 bus_new 之后、

     *    panel_new 之前显式设 SYSCLK：

     *    bk_display_bus_set_clock_src(s_bus, DPU_CLK_SRC_SYSCLK); */

    /* 3) 建 panel（reset/init 由 bk_display_init() 内部驱动，无需手动调） */
    bk_lcd_panel_config_t panel_config = {
        .reset_pin = GPIO_60,                /* RST 有效电平在 panel 描述符里 */
    };
    bk_lcd_mipi_panel_new(s_bus, &panel_config,
                          &lcd_device_<vendor>_mipi_<WxH>,
                          &s_panel);

    /* 4) 建 DPU 控制器；timing / 像素时钟由控制器从 panel 句柄自取，

     *    dpu_cfg 只填 video 层 */
    bk_display_dpu_config_t dpu_cfg = {
        .video.enable     = true,
        .video.format     = BK_PIXEL_FORMAT_RGB565,
        .video.decompress = false,
    };
    bk_display_dpu_ctlr_new(&s_ctlr, s_panel, &dpu_cfg);   /* 3 参：含 panel 句柄 */
    bk_display_init(s_ctlr);                                /* 内部跑 .reset/.init */
    bk_display_open(s_ctlr);

    /* 5) 板上背光 GPIO 放最后（按板子接线） */
    return 0;
}

int my_mipi_lcd_close(void)
{
    /* 严格逆序 */
    bk_display_close (s_ctlr);
    bk_display_deinit(s_ctlr);
    bk_display_delete(s_ctlr);    s_ctlr  = NULL;
    bk_lcd_panel_delete(s_panel); s_panel = NULL;
    bk_display_bus_delete(s_bus); s_bus   = NULL;
    /* 最后再降 1.8V VDDIO */
    return 0;
}

```


## 运行期调试命令通道


```
/* 重新发 DISPON / SLPOUT，或在亮屏后切 MADCTL */
bk_lcd_panel_tx_param(s_panel, 0x11, NULL, 0);        /* SLPOUT */
rtos_delay_milliseconds(120);
bk_lcd_panel_tx_param(s_panel, 0x29, NULL, 0);        /* DISPON */

/* 读 display status */
uint8_t dstat[4] = {0};
bk_lcd_panel_rx_param(s_panel, 0x09, dstat, sizeof(dstat));

```

13. 验证清单 & FAQ


## 13.1 验证顺序

1. 编译通过；`bk_lcd_get_mipi_panel_list()` 中能看到你的 `name`
2. 示波器看 RESET 引脚：`bk_display_init()` 内部驱动 reset 后波形为
   idle→active→release 三段
3. `bk_display_init()` 返回 `BK_OK`（内部已派发 `init_cmds`）
4. （若填了 `read_id_regs`）`bk_lcd_panel_read_id()` 与
   `panel.id` 一致
5. `bk_display_open()` 后送纯色帧整屏稳定无横纹
6. 渐变图无条纹/撕裂/颜色错位
7. 切像素格式（RGB565 / RGB888 / NV12 / ARGB8888）正常
8. 100 次 open/close 不死机不漏内存


## 13.2 常见问题速查

| 现象 | 排查首项 | 排查次项 |
| --- | --- | --- |
| 整屏黑、电流正常 | RESET 时序 / init 命令是否真的下发 | `n_lanes` 是否与屏一致 |
| 整屏黑、电流异常 | 屏 VDDIO / 背光 LDO | PMU AUXLDO 2.8V/3V 投票是否成功 |
| `read_id` 返回 0 / 0xFF | 屏 VCC 是否上电 | `read_id_regs` 配错 / `read_id_bytes` 错 |
| 闪屏 / 帧率不稳 | DSI lane bit-rate 偏离 spec | 调 `fps` 或 `n_lanes` 重算 |
| 整屏黄/绿条带 | DPU FIFO underflow（PSRAM 带宽） | 确认 DPU QoS=3；高带宽模块是否并发 |
| 撕裂 | flush 频率高于实际帧率 | 降 flush 频率或 fps |
| 切像素格式后花屏 | 切换瞬间仍有 inflight flush | 切换前先停 flush 线程 → ioctl → 再启 |
| close 后再 open 卡死 | `bk_display_bus_delete` 是否漏 | 同一 handle 不要重复 new |
| LT8912B 无信号 | `bk_lcd_lt8912b_set_io_pins()` 是否调用 | 是否用 `bk_display_bus_set_clock_src()` 切到 `SYSCLK` |
| menuconfig 看不到新 panel | Kconfig `depends on LCD_DSI` 是否漏 | `config LCD_xxx` 名字拼错 |
| 段注册取不到 panel | `BK_LCD_PANEL_DEVICE_SECTION` 是否漏 | 第 3 参须为 `BK_LCD_PANEL_BUS_DSI` |
| 编译时找不到结构体 | 头文件应为 `<components/bk_lcd_panel.h>` | `#if CONFIG_LCD_xxx` 与 Kconfig 名一致 |

参考


- 模板源文件：`ap/components/bk_peripheral/src/lcd/dsi/lcd_mipi_st7701sn_480x854.c`

- 通用驱动：`ap/components/bk_display/src/panel/lcd_mipi_panel_common.c`

- 公有 API：`<components/bk_display.h>`（伞头）/
  `<components/bk_display_bus.h>` / `<components/bk_lcd_panel.h>`

- 公有类型：`<components/bk_lcd_panel_types.h>`

- 应用样例：`projects/common_components/multimedia_device_service/src/app_display.c`、`projects/multimedia/mipi_lcd_example/`

- 桥接参考：`ap/components/bk_peripheral/src/lcd/dsi/lcd_mipi_lt8912b_bridge.c`
