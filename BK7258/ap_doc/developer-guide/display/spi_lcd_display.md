---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/display/spi_lcd_display.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="spi-lcd-display"></a>

# spi\_lcd\_display

<a id="id1"></a>

## 概述

display函数是对不同接口的屏幕驱动的抽象，客户根据不同的屏幕类型使用对应的接口创建handle。
接口说明参考bk\_display.h。

本节主要说明display模块如何驱动SPI LCD，包括其API调用，参数说明以及注意事项。

<a id="id2"></a>

## 开发介绍

<a id="id3"></a>

### 1\. 关于背光

BK7258 SDK中默认的LCD背光控制引脚是GPIO7，如果客户的IO不一致，需要在方案中主动配置。此外，背光控制是由用户自行控制的，可按照SDK工程中的背光接口自行封装打开和关闭接口。

<a id="lcd"></a>

### 2\. 关于lcd设备

BK7258 SDK中已添加一些SPI LCD的设备，如果客户的设备不一致，需要在方案中添加新的device设备，可参考下面章节说明。

<a id="id4"></a>

## 代码流程

<a id="id5"></a>

### 1\. 创建LCD控制器

介绍参数:
\- `handle`: 输出参数，存储创建的display控制器句柄
\- `config`: 控制器配置参数，包含LCD设备信息和GPIO引脚配置

示例代码:

```
bk_display_spi_ctlr_config_t spi_ctlr_config = {
    .lcd_device = &lcd_device_st7796u,
    .spi_id = 0,
    .dc_pin = GPIO_8,
    .reset_pin = GPIO_40,
    .te_pin = 0,
};

static bk_display_ctlr_handle_t lcd_display_handle = NULL;
avdk_err_t ret = bk_display_spi_new(&lcd_display_handle, &spi_ctlr_config);
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
static const lcd_qspi_init_cmd_t gc9d01_init_cmds[] =
{
    {0xFE, {0x00}, 0},
    {0xEF, {0x00}, 0},
    {0x80, {0xFF}, 1},
    {0x81, {0xFF}, 1},
    {0x82, {0xFF}, 1},
    {0x83, {0xFF}, 1},
    {0x84, {0xFF}, 1},
    {0x85, {0xFF}, 1},
    {0x86, {0xFF}, 1},
    {0x87, {0xFF}, 1},
    {0x88, {0xFF}, 1},
    {0x89, {0xFF}, 1},
    {0x8A, {0xFF}, 1},
    {0x8B, {0xFF}, 1},
    {0x8C, {0xFF}, 1},
    {0x8D, {0xFF}, 1},
    {0x8E, {0xFF}, 1},
    {0x8F, {0xFF}, 1},
    {0x3A, {0x05}, 1},
    {0xEC, {0x01}, 1},
    {0x74, {0x02, 0x0E, 0x00, 0x00, 0x00, 0x00, 0x00}, 7},
    {0x98, {0x3E, 0x99, 0x3E}, 3},
    {0XB5, {0x0D, 0x0D}, 2},
    {0x60, {0x38, 0x0F, 0x79, 0x67}, 4},
    {0x61, {0x38, 0x11, 0x79, 0x67}, 4},
    {0x64, {0x38, 0x17, 0x71, 0x5F, 0x79, 0x67}, 6},
    {0x65, {0x38, 0x13, 0x71, 0x5B, 0x79, 0x67}, 6},
    {0x6A, {0x00, 0x00}, 2},
    {0x6C, {0x22, 0x02, 0x22, 0x02, 0x22, 0x22, 0x50}, 7},
    {0x6E, {0x03, 0x03, 0x01, 0x01, 0x00, 0x00, 0x0F, 0x0F, 0x0D, 0x0D, 0x0B, 0x0B, 0x09, 0x09, 0x00, 0x00, 0x00, 0x00, 0x0A, 0x0A, 0x0C, 0x0C, 0x0E, 0x0E, 0x10, 0x10, 0x00, 0x00, 0x02, 0x02, 0x04, 0x04}, 32},
    {0xBF, {0x01}, 1},
    {0xF9, {0x40}, 1},
    {0x9B, {0x3B}, 1},
    {0x93, {0x33, 0x7F, 0x00}, 3},
    {0x7E, {0x30}, 1},
    {0x70, {0x0D, 0x02, 0x08, 0x0D, 0x02, 0x08}, 6},
    {0x71, {0x0D, 0x02, 0x08}, 3},
    {0X91, {0x0E, 0x09}, 2},
    {0xC3, {0x18}, 1},
    {0xC4, {0x18}, 1},
    {0xC9, {0x3C}, 1},
    {0xF0, {0x13, 0x15, 0x04, 0x05, 0x01, 0x38}, 6},
    {0xF2, {0x13, 0x15, 0x04, 0x05, 0x01, 0x34}, 6},
    {0xF1, {0x4B, 0xB8, 0x7B, 0x34, 0x35, 0xEF}, 6},
    {0xF3, {0x47, 0xB4, 0x72, 0x34, 0x35, 0xDA}, 6},
    {0x36, {0x00}, 1},
    {0x34, {0x00}, 0},
    {0x11, {0x00}, 0},
    {0x00, {0x78}, 0xFF},
    {0x29, {0x00}, 0},
};

static const lcd_spi_t lcd_spi_gc9d01_config =
{
    .clk = LCD_QSPI_60M,
    .init_cmd = gc9d01_init_cmds,
    .device_init_cmd_len = sizeof(gc9d01_init_cmds) / sizeof (lcd_qspi_init_cmd_t),
    .frame_len = (PPI_160X160 >> 16) * (PPI_160X160 & 0xFFFF) * 2,
};

const lcd_device_t lcd_device_gc9d01 =
{
    .id = LCD_DEVICE_GC9D01,
    .name = "gc9d01",
    .type = LCD_TYPE_SPI,
    .ppi = PPI_160X160,
    .spi = &lcd_spi_gc9d01_config,
    .init = NULL,
    .lcd_off = NULL,
};
```

<a id="id10"></a>

## 参考工程

- SPI LCD示例: `./projects/spi_lcd_example`

<a id="id11"></a>

## 注意事项

1. 确保在调用flush之前已经成功创建和打开了display控制器
2. 帧数据释放回调函数必须正确实现，否则会导致内存泄漏
3. 不同的LCD设备需要配置正确的GPIO引脚
4. 帧缓冲区大小应根据实际显示分辨率和像素格式计算
5. 操作完成后应及时关闭和删除控制器释放资源
