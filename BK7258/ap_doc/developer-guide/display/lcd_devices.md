---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/display/lcd_devices.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="lcd-devices"></a>

# lcd\_devices

<a id="id1"></a>

## 概述

本节主要讲解新增RGB接口和MCU接口的lcd device

<a id="rgb"></a>

## 增加RGB接口屏幕

<a id="lcd-rgb-name-c"></a>

### 1:新增lcd\_rgb\_name.c

在用户在开发目录下新增lcd\_rgb\_name.c

<a id="lcd-rgb-t"></a>

### 2：实现lcd\_rgb\_t结构体

针对RGB屏幕需要根据lcd spec 设置clk, data\_out\_clk\_edge, hsync/vsync proch等参数。
注意参数的范围也要满足spec的要求，也要满足display模块限定的范围。

display模块设置的时钟clk，信号线proch，以及数据输出在时钟的上升沿下降沿的范围如下：

```
/** rgb lcd clk select, infulence pfs, user should select according to lcd device spec*/
typedef enum {
    LCD_80M,
    LCD_64M,
    LCD_60M,
    LCD_54M,
    LCD_45M, //45.7M
    LCD_40M,
    LCD_35M, //35.5
    LCD_32M,
    LCD_30M,
    LCD_26M, //26.6M
    LCD_24M, //24.6M
    LCD_22M, //22.85M
    LCD_20M,
    LCD_17M, //17.1M
    LCD_15M,
    LCD_12M,
    LCD_10M,
    LCD_9M,  //9.2M
    LCD_8M,
    LCD_7M   //7.5M
} lcd_clk_t;

/** rgb data output in clk rising or falling */
typedef enum {
    POSEDGE_OUTPUT = 0,    /**< output in clk falling*/
    NEGEDGE_OUTPUT,        /**< output in clk rising*/
} rgb_out_clk_edge_t;

/** rgb interface config param */
typedef struct
{
    lcd_clk_t clk;                         /**< config lcd clk */
    rgb_out_clk_edge_t data_out_clk_edge;  /**< rgb data output in clk edge, should refer lcd device spec*/

    uint16_t hsync_back_porch;            /**< rang 0~0x3FF (0~1023), should refer lcd device spec*/
    uint16_t hsync_front_porch;           /**< rang 0~0x3FF (0~1023), should refer lcd device spec*/
    uint16_t vsync_back_porch;            /**< rang 0~0xFF (0~255), should refer lcd device spec*/
    uint16_t vsync_front_porch;           /**< rang 0~0xFF (0~255), should refer lcd device spec*/
    uint8_t hsync_pulse_width;            /**< rang 0~0x3F (0~7), should refer lcd device spec*/
    uint8_t vsync_pulse_width;            /**< rang 0~0x3F (0~7), should refer lcd device spec*/
} lcd_rgb_t;
```

实现如下：

```
static const lcd_rgb_t lcd_rgb =
{
    .clk = LCD_30M,
    .data_out_clk_edge = NEGEDGE_OUTPUT,

    .hsync_pulse_width = 2,
    .vsync_pulse_width = 2,
    .hsync_back_porch = 46,
    .hsync_front_porch = 48,
    .vsync_back_porch = 24,
    .vsync_front_porch = 24,
};
```

- 有关结构体参考，请参阅：

  - [lcd\_rgb\_t](../../api-reference/multimedia/bk_display.md#_CPPv49lcd_rgb_t)

spec中提供的参数一般如图，具体需要看每个屏幕的spec：

<a id="id8"></a>
![RealtimeVideo_app](../../../../../_assets/7472bdb6ae4d4ff1faee-st7282_lcd_sync.png)


Figure. rgb sync params config

<a id="id3"></a>

### 3：实现屏幕初始化等功能函数

屏幕的初始化代码函数一般是屏幕厂商提供，需要SPI接口给LCD发送初始化命令.
一般为GPIO模拟SPI，所以需要在创建display handle时传入spi io，目前SDK中已适配了8-bit和16-bit的命令格式。

```
static void lcd_st7701sn_config(const bk_lcd_spi_handle_t *spi_handle)
{
#define Delay rtos_delay_milliseconds
#define SPI_WriteComm(data) spi_handle->write_cmd(spi_handle, data)
#define SPI_WriteData(data) spi_handle->write_data(spi_handle, data)

    bk_gpio_set_output_low(spi_handle->io.rst);
    Delay(10);
    bk_gpio_set_output_high(spi_handle->io.rst);
    Delay(120);

    SPI_WriteComm(0x11);
    Delay(10);

    SPI_WriteComm(0xFF);
    SPI_WriteData(0x77);
    SPI_WriteData(0x01);
    .......

    SPI_WriteComm(0x29);
}
static bk_err_t lcd_st7701sn_off(const void *handle)
{
    if (!handle)
    {
        return BK_FAIL;
    }
    ((bk_lcd_spi_handle_t *)handle)->write_cmd((bk_lcd_spi_handle_t *)handle, 0x28);
    return BK_OK;
}
static bk_err_t lcd_st7701sn_init(const void *handle)
{
    if (!handle)
    {
        return BK_FAIL;
    }
    lcd_st7701sn_config((bk_lcd_spi_handle_t *)handle);
    BK_LOGD(NULL, "lcd_st7701sn: init.\r\n");
    return BK_OK;
}
```

16-bit命令api如下：

```
#define SPI_WriteComm(data) spi_handle->write_hf_word_data(spi_handle, data)
#define SPI_WriteData(data) spi_handle->write_hf_word_cmd(spi_handle, data)
```

<a id="lcd-device-t"></a>

### 4：实现lcd\_device\_t结构体

> - 针对不同的屏幕类型，需要实现不同的lcd\_device\_t结构体，结构体中包含屏幕的名称、类型、分辨率, 输出格式、初始化函数、关闭函数等。
> - 因为display支持像素转换功能，即输入数据可以和lcd支持的输出数据格式不同，所以可以通过 `src_fmt` 和 `out_fmt` 来区分： `src_fmt` 用于指定输入给display模块的数据格式， `out_fmt` 为display输出到LCD的格式。
> - 实践中（参考 `lcd_rgb_st7701sn.c` ）， `src_fmt` 通常在刷屏时通过调用 `bk_display_flush` 动态指定，而不是固定在 `lcd_device_t` 中。因此， `lcd_device_t` 中的 `src_fmt` 为可选项，示例中不再固定配置； `out_fmt` 根据屏幕接口能力固定配置。

```
bg_frame->fmt = PIXEL_FMT_RGB565_LE;  /**< 每次刷屏配置源数据的输入格式，可以动态改变 */
bg_frame->width = bg_frame_width;     /**< 源数据的宽度 */
bg_frame->height = bg_frame_height;   /**< 源数据的高度 */
bk_display_flush(lcd_display_handle, bg_frame, display_frame_free_cb);
```

```
const lcd_device_t lcd_device_custom_st7701sn =
{
    .name = "custom_lcd_st7701sn",  /**< lcd 名称, 用于打印debug查看 */
    .type = LCD_TYPE_RGB,             /**< lcd 接口类型 */
    .width = 480,                     /**< lcd 分辨率宽度 */
    .height = 854,                    /**< lcd 分辨率高度 */
    .rgb = &lcd_rgb,                  /**< lcd rgb 参数 */
    .out_fmt = PIXEL_FMT_RGB888,      /**< lcd 输出格式（固定） */
    .lcd_init = lcd_st7701sn_init,    /**< lcd 初始化函数 */
    .lcd_off = lcd_st7701sn_off,      /**< lcd 关闭函数 */
};
```

备注

刷屏时请根据源数据格式设置\`bg\_frame-\>fmt\`并调用\`bk\_display\_flush\`，无需在\`lcd\_device\_t\`中固定\`src\_fmt\`。

- 有关结构体参考，请参阅：

  - [lcd\_device\_t](../../api-reference/multimedia/bk_display.md#_CPPv412lcd_device_t)

<a id="mcu"></a>

### 增加MCU接口屏幕

<a id="lcd-mcu-name-c"></a>

### 1: 新增lcd\_mcu\_name.c

在用户在开发目录下新增lcd\_mcu\_name.c

<a id="id5"></a>

### 2: 实现屏幕初始化等功能函数

```
static bk_err_t lcd_st7796s_init(const void *handle)
{
    if (!handle) {
        return BK_FAIL;
    }
    // MCU LCD初始化序列
    bk_lcd_i80_handle_t *i80_handle = (bk_lcd_i80_handle_t *)handle;

    rtos_delay_milliseconds(131);
    i80_handle->write_cmd(i80_handle, 0, SLEEP_OUT, NULL);
    rtos_delay_milliseconds(120);
    // ... 更多初始化命令
    return BK_OK;
}
```

<a id="lcd-mcu-t"></a>

### 3: 实现lcd\_mcu\_t结构体

lcd\_mcu\_t结构体用于配置lcd的clk、set\_display\_area、start\_transfer、continue\_transfer等函数指针。
客户一般需要实现start\_transfer和continue\_transfer，如果这两个函数为NULL，则display默认会使用0x2C进行刷屏。
如果不为NULL， 那么display就调用客户实现的start\_transfer和continue\_transfer函数。

```
static const lcd_mcu_t lcd_mcu =
{
    .clk = LCD_40M,                                 /**< lcd clk */
    .start_transfer = lcd_st7796s_start_transfer,   /**< lcd start transfer */
    .continue_transfer = lcd_st7796s_continue_transfer,/**< lcd continue transfer */
};
```

<a id="id6"></a>

### 4: 实现lcd\_device\_t结构体

```
const lcd_device_t lcd_device_custom_st7796s =
{
    .name = "custom_lcd_st7796s",      /**< lcd 名称 */
    .type = LCD_TYPE_MCU8080,              /**< lcd 接口类型 */
    .width = 320,                       /**< lcd 分辨率宽度 */
    .height = 480,                      /**< lcd 分辨率高度 */
    .mcu = &lcd_mcu,                   /**< lcd mcu 参数 */
    .lcd_init = lcd_st7796s_init,      /**< lcd 初始化函数 */
    .lcd_off = st7796s_lcd_off,        /**< lcd 关闭函数 */
};
```

备注

MCU 接口同样建议在刷屏时通过 bg\_frame-\>fmt 指定源数据格式，不在 lcd\_device\_t 固定 src\_fmt；out\_fmt 如需固定请根据面板支持情况配置，但在本示例中省略以保持与参考实现一致。

<a id="id7"></a>

## 注意事项

1. RGB屏幕参数需要同时满足LCD规格书和display模块的要求
2. 初始化函数需要与屏厂确认为正确的初始化序列
3. 设备名称需要唯一，避免调试误导
4. 输出格式需要与实际屏幕支持的格式匹配
5. 时钟频率设置需要根据屏幕规格和性能要求调整
