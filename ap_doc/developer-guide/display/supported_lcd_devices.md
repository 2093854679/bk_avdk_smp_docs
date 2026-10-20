---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/display/supported_lcd_devices.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="lcd"></a>

# 支持的 LCD 设备

本页汇总 BK7259 当前已在 `ap/components/bk_peripheral/src/lcd` 下注册的 LCD 屏，
按总线类型分组。型号/分辨率/源文件以代码库为准；新增屏的方法见
[如何新增 MIPI DSI Panel（BK7259）](how_to_add_mipi_panel.md) 与 [如何新增 RGB Panel（BK7259）](how_to_add_rgb_panel.md)。

备注

BK7259 **不支持** Intel 8080 / MCU 并口 LCD 总线，仅支持 MIPI-DSI、并口 RGB、
QSPI、SPI 四类。

<a id="mipi-dsi"></a>

## MIPI-DSI 屏

源目录 `ap/components/bk_peripheral/src/lcd/dsi`，详细新增/时序说明见
[如何新增 MIPI DSI Panel（BK7259）](how_to_add_mipi_panel.md)。

| 型号 | 分辨率 | 源文件 |
| --- | --- | --- |
| ER68576B | 720×1280 | `lcd_mipi_er68576b_720x1280.c` |
| FL7703NP | 720×1280 | `lcd_mipi_fl7703np_720x1280.c` |
| GC9702 | 720×1280 | `lcd_mipi_gc9702_720x1280.c` |
| HX8394F | 720×1280 | `lcd_mipi_hx8394f_720x1280.c` |
| HX8399C | 1080×1920 | `lcd_mipi_hx8399c_1080x1920.c` |
| JD9522Z | 1080×1920 | `lcd_mipi_jd9522z_1080x1920.c` |
| JD9855 | 320×385 | `lcd_mipi_jd9855_320x385.c` |
| ST7701S | 412×960 | `lcd_mipi_st7701s_412x960.c` |
| ST7701SN | 360×640 | `lcd_mipi_st7701sn_360x640.c` |
| ST7701SN | 480×640 | `lcd_mipi_st7701sn_480x640.c` |
| ST7701SN | 480×854 | `lcd_mipi_st7701sn_480x854.c` |
| LT8912B（MIPI→HDMI 桥） | 由 HDMI 时序决定（Kconfig 选择） | `lcd_mipi_lt8912b_bridge.c` |

<a id="rgb"></a>

## 并口 RGB 屏

源目录 `ap/components/bk_peripheral/src/lcd/rgb`，详细新增/时序说明见
[如何新增 RGB Panel（BK7259）](how_to_add_rgb_panel.md)。像素走 24-bit 并口 RGB，寄存器初始化走 SW SPI
配置通道。

| 型号 | 分辨率 | 源文件 |
| --- | --- | --- |
| AML01 | 720×1280 | `lcd_rgb_aml01_720x1280.c` |
| GC9503V | 480×800 | `lcd_rgb_gc9503v_480x800.c` |
| H050IWV | 800×480 | `lcd_rgb_h050iwv_800x480.c` |
| HX8282 | 1024×600 | `lcd_rgb_hx8282_1024x600.c` |
| MD0430R | 800×480 | `lcd_rgb_md0430r_800x480.c` |
| MD0700R | 1024×600 | `lcd_rgb_md0700r_1024x600.c` |
| NT35510 | 480×854 | `lcd_rgb_nt35510_480x854.c` |
| NT35512 | 480×800 | `lcd_rgb_nt35512_480x800.c` |
| ST7282 | 480×272 | `lcd_rgb_st7282_480x272.c` |
| ST7701S | 480×480 | `lcd_rgb_st7701s_480x480.c` |
| ST7701SN | 480×854 | `lcd_rgb_st7701sn_480x854.c` |

<a id="qspi"></a>

## QSPI 屏

源目录 `ap/components/bk_peripheral/src/lcd/qspi`，使用方法见
[qspi\_lcd\_display](qspi_lcd_display.md)。

| 型号 | 分辨率 | 源文件 |
| --- | --- | --- |
| CO5300 | 410×502 | `lcd_qspi_co5300.c` |
| GC9C01 | 360×360 | `lcd_qspi_gc9c01.c` |
| JD9853A | 240×320 | `lcd_qspi_jd9853a.c` |
| JD9855 | 360×360 | `lcd_qspi_jd9855.c` |
| JD9855 (K18XJ15) | 360×360 | `lcd_qspi_jd9855_k18xj15.c` |
| SH8601A | 454×454 | `lcd_qspi_sh8601a.c` |
| SPD2010 | 412×412 | `lcd_qspi_spd2010.c` |
| ST77903 (H0165Y008T) | 400×400 | `lcd_qspi_st77903_h0165y008t.c` |
| ST77903 (SAT61478M) | 360×480 | `lcd_qspi_st77903_sat61478m.c` |
| ST77903 (WX20114) | 400×400 | `lcd_qspi_st77903_wx20114.c` |
| ST77916 | 360×360 | `lcd_qspi_st77916.c` |

<a id="spi"></a>

## SPI 屏

源目录 `ap/components/bk_peripheral/src/lcd/spi`，使用方法见
[spi\_lcd\_display](spi_lcd_display.md)。

| 型号 | 分辨率 | 源文件 |
| --- | --- | --- |
| GC9D01 | 160×160 | `lcd_spi_gc9d01.c` |
| JD9853 | 240×296 | `lcd_spi_jd9853.c` |
| ST7789V2 | 240×320 | `lcd_spi_st7789v2.c` |
| ST7796U | 320×480 | `lcd_spi_st7796u.c` |
