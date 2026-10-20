---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/display/qspi_lcd_display.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="qspi-lcd-display"></a>

# qspi\_lcd\_display

<a id="id1"></a>

## 概述

display函数是对不同接口的屏幕驱动的抽象，客户根据不同的屏幕类型使用对应的接口创建handle。
接口说明参考bk\_display.h。

本节主要说明display模块如何驱动QSPI LCD，包括其API调用，参数说明以及注意事项。

<a id="id2"></a>

## 开发介绍

<a id="id3"></a>

### 1\. 关于背光

BK7258 SDK中默认的LCD背光控制引脚是GPIO7，如果客户的IO不一致，需要在方案中主动配置。此外，背光控制是由用户自行控制的，可按照SDK工程中的背光接口自行封装打开和关闭接口。

<a id="lcd"></a>

### 2\. 关于lcd设备

BK7258 SDK中已添加一些QSPI LCD的设备，如果客户的设备不一致，需要在方案中添加新的device设备，可参考下面章节说明。

<a id="id4"></a>

## 代码流程

<a id="id5"></a>

### 1\. 创建LCD控制器

介绍参数:
\- `handle`: 输出参数，存储创建的display控制器句柄
\- `config`: 控制器配置参数，包含LCD设备信息和GPIO引脚配置

示例代码:

```
bk_display_qspi_ctlr_config_t qspi_ctlr_config = {
    .lcd_device = &lcd_device_st77903_h0165y008t,
    .qspi_id = 0,
    .reset_pin = GPIO_40,
    .te_pin = 0,
};

static bk_display_ctlr_handle_t lcd_display_handle = NULL;
avdk_err_t ret = bk_display_qspi_new(&lcd_display_handle, &qspi_ctlr_config);
if (ret != AVDK_ERR_OK) {
    // 错误处理
}
```

注意

如果TE功能未使用，可将te\_pin设置为任意值。
lcd\_device是传入的lcd设备指针，用于获取屏幕的分辨率、接口类型等信息，该参数必须传入。

<a id="id6"></a>

### 2\. 打开LCD显示

介绍参数:
\- `handle`: display控制器句柄

描述：
打开LCD显示，初始化显示控制器。

示例代码:

```
// 打开背光
lcd_backlight_open(GPIO_7);

// 打开显示控制器
ret = bk_display_open(lcd_display_handle);
if (ret != AVDK_ERR_OK) {
    // 错误处理
}
```

注意

由于硬件环境不同，背光需要用户自己配置

<a id="id7"></a>

### 3\. 刷新LCD显示

介绍参数:
\- `handle`: display控制器句柄
\- `frame`: 要显示的帧数据指针
\- `free_t`: 帧数据释放回调函数

描述：
刷新LCD显示内容，将帧数据发送到显示屏。

示例代码:

```
// 帧数据释放回调函数
static avdk_err_t display_frame_free_cb(void *frame)
{
    frame_buffer_display_free((frame_buffer_t *)frame);
    return AVDK_ERR_OK;
}

// 刷新显示
ret = bk_display_flush(lcd_display_handle, (void *)disp_frame, display_frame_free_cb);
if (ret != AVDK_ERR_OK) {
    // 错误处理，需要手动释放帧
    display_frame_free_cb(disp_frame);
}
```

注意

1：display\_frame\_free\_cb是刷新显示时的帧数据释放回调函数，用于释放刷新完成后的帧数据。
如果客户不需要释放frame, 可以将free\_t设置为NULL。
2：刷屏的源数据格式支持RGB数据，具体的RGB格式可参考LCD的spec说明。

<a id="id8"></a>

### 4\. 关闭LCD显示

介绍参数:
\- `handle`: display控制器句柄

描述：
关闭LCD显示，停止显示控制器。

示例代码:

```
// 关闭显示控制器
ret = bk_display_close(lcd_display_handle);
if (ret != AVDK_ERR_OK) {
    // 错误处理
}

// 关闭背光
lcd_backlight_close(GPIO_7);
```

<a id="id9"></a>

### 5\. 删除LCD控制器

介绍参数:
\- `handle`: display控制器句柄

描述：
删除LCD控制器，释放相关资源。

示例代码:

```
// 删除显示控制器
ret = bk_display_delete(lcd_display_handle);
if (ret != AVDK_ERR_OK) {
    // 错误处理
}
lcd_display_handle = NULL; // 重置句柄
```

<a id="lcd-device"></a>

### 6\. 新增lcd device

```
#define LCD_QSPI_GC9C01_REGISTER_WRITE_COMMAND        0x02
#define LCD_QSPI_GC9C01_REGISTER_READ_COMMAND         0x03

static const lcd_qspi_init_cmd_t gc9c01_init_cmds[] =
{
    {0xfe, {0x00}, 0},
    {0xef, {0x00}, 0},
    {0x80, {0x11}, 1},
    {0x81, {0x70}, 1},
    {0x82, {0x09}, 1},
    {0x83, {0x03}, 1},
    {0x84, {0x70}, 1},
    {0x89, {0x10}, 1},
    {0x8a, {0x4f}, 1},
    {0x8b, {0x08}, 1},
    {0x8c, {0x59}, 1},
    {0x8d, {0x51}, 1},
    {0x36, {0x40}, 1},//RGB, 0x48 - BGR
    {0x3a, {0x05}, 1},
    {0xec, {0x87}, 1},
    {0x74, {0x01, 0x80, 0x00, 0x00, 0x00, 0x00}, 6},
    {0x98, {0x3e}, 1},
    {0x99, {0x3e}, 1},
    {0xc3, {0x3a}, 1},
    {0xc4, {0x16}, 1},
    {0xa1, {0x01, 0x04}, 2},
    {0xa2, {0x01, 0x04}, 2},
    {0xcb, {0x02}, 1},
    {0x7c, {0xB6, 0x26}, 2},
    {0xac, {0x24}, 1},
    {0xf6, {0x80}, 1},
    {0xb5, {0x09, 0x09}, 2},
    {0xb6, {0x00, 0x40}, 2},
    {0x60, {0x38, 0x0B, 0x5B, 0x56}, 4},
    {0x63, {0x3A, 0xE0, 0x5B, 0x56}, 4},
    {0x64, {0x38, 0x0D, 0x72, 0xDD, 0x5B, 0x56}, 6},
    {0x66, {0x38, 0x11, 0x72, 0xE1, 0x5B, 0x56}, 6},
    {0x68, {0x3B, 0x08, 0x08, 0x00, 0x08, 0x29, 0x5B}, 7},
    {0x6E, {0x00, 0x00, 0x00, 0x07, 0x01, 0x13, 0x11, 0x0B, 0x09, 0x16, 0x15, 0x1D, 0x1E, 0x00, 0x00, 0x00,
            0x00, 0x00, 0x00, 0x1E, 0x1D, 0x15, 0x16, 0x0A, 0x0C, 0x12, 0x14, 0x02, 0x08, 0x00, 0x00, 0x00}, 32},
    {0xBE, {0x11}, 1},
    {0x6C, {0xCC, 0x0C, 0xCC, 0x84, 0xCC, 0x04, 0x50}, 7},
    {0x7d, {0x72}, 1},
    {0x7e, {0x38}, 1},
    {0x70, {0x02, 0x03, 0x09, 0x05, 0x0C, 0x06, 0x09, 0x05, 0x0C, 0x06}, 10},
    {0x90, {0x06, 0x06, 0x05, 0x06}, 4},
    {0x93, {0x45, 0xFF, 0x00}, 3},
    {0xF0, {0x46, 0x0B, 0x0F, 0x0A, 0x10, 0x3F}, 6},
    {0xF1, {0x52, 0x9A, 0x4F, 0x36, 0x37, 0xFF}, 6},
    {0xF2, {0x46, 0x0B, 0x0F, 0x0A, 0x10, 0x3F}, 6},
    {0xF3, {0x52, 0x9A, 0x4F, 0x36, 0x37, 0xFF}, 6},
    {0XFB, {0X00, 0x00}, 2},
    {0xb4, {0x0A}, 1},
    {0x35, {0x00}, 1},
    {0x44, {0x00, 0x01}, 2},
    {0xa3, {0x4F}, 1}, //TE,0x21-25ms,0x24-23ms,0x28-22ms,0x2f-20ms,0x3f-19ms,0x4f-17ms
    {0x78, {0x01, 0x80}, 2},
    {0x11, {0x00}, 0},
    {0x00, {0xC8}, 0xFF},
    {0xfe, {0x00}, 0},
    {0xee, {0x00}, 0},
    {0x29, {0x00}, 0},
};

static uint8_t gc9c01_cmd[4] = {0x32, 0x00, 0x2c, 0x00};

static const lcd_qspi_t lcd_qspi_gc9c01_config =
{
    .clk = LCD_QSPI_48M,
    .refresh_method = LCD_QSPI_REFRESH_BY_FRAME,
    .reg_write_cmd = LCD_QSPI_GC9C01_REGISTER_WRITE_COMMAND,
    .reg_read_cmd = LCD_QSPI_GC9C01_REGISTER_READ_COMMAND,
    .reg_read_config.dummy_clk = 0,
    .reg_read_config.dummy_mode = LCD_QSPI_NO_INSERT_DUMMMY_CLK,
    .pixel_write_config.cmd = gc9c01_cmd,
    .pixel_write_config.cmd_len = sizeof(gc9c01_cmd),
    .init_cmd = gc9c01_init_cmds,
    .device_init_cmd_len = sizeof(gc9c01_init_cmds) / sizeof(lcd_qspi_init_cmd_t),
    .refresh_config = {0},
#if (CONFIG_LCD_QSPI_COLOR_DEPTH_BYTE == 3)
    .frame_len = (PPI_360X360 >> 16) * (PPI_360X360 & 0xFFFF) * 3,
#else
    .frame_len = (PPI_360X360 >> 16) * (PPI_360X360 & 0xFFFF) * 2,
#endif
};

const lcd_device_t lcd_device_gc9c01 =
{
    .id = LCD_DEVICE_GC9C01,
    .name = "gc9c01",
    .type = LCD_TYPE_QSPI,
    .ppi = PPI_360X360,
    .qspi = &lcd_qspi_gc9c01_config,
    .init = NULL,
    .lcd_off = NULL,
};
```

<a id="id10"></a>

## 参考工程

- QSPI LCD示例: `./projects/qspi_lcd_example`

<a id="id11"></a>

## 注意事项

1. 确保在调用flush之前已经成功创建和打开了display控制器
2. 帧数据释放回调函数必须正确实现，否则会导致内存泄漏
3. 不同的LCD设备需要配置正确的GPIO引脚
4. 帧缓冲区大小应根据实际显示分辨率和像素格式计算
5. 操作完成后应及时关闭和删除控制器释放资源
