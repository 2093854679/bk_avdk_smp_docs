---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/display/rgb_lcd_display.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rgb-lcd-display"></a>

# rgb\_lcd\_display

<a id="id1"></a>

## 概述

display接口是对不同接口的屏幕驱动的抽象，客户根据不同的屏幕类型使用对应的接口创建handle。

display hardwarefeature：

1. 支持不同的屏幕类型，如RGB LCD（RGB565,RGB888）、MCU LCD(8线,16线)等。
2. 支持像素转换功能，即输入数据可以和lcd支持的输出数据格式不同，比如可以提供YUYV数据刷屏。
   :   - YUYV到RGB565/RGB888/RGB666的转换
       - RGB565到RGB888的转换
       - RGB888到RGB565的转换
       - RGB565到RGB666的转换
       - RGB888到RGB666的转换
3. RGB565格式使用的GPIO为高位有效， 即R3-R7为高位，G2-G7为高位，B3-B7为高位。

本节主要说明display模块如何驱动RGB LCD，包括其API调用，参数说明以及注意事项。

- 有关RGB LCD显示的示例工程，请参阅：

  - [RGB LCD显示示例工程](../../examples/projects/rgb_lcd_example.md)
- 有关API参考，请参阅：

  - [RGB LCD显示接口](../../api-reference/multimedia/bk_display.md)

<a id="id3"></a>

## 开发介绍

<a id="ldo"></a>

### 1\. 关于电源LDO控制

BK7258 开发板SDK中默认的LCD LDO控制引脚是GPIO13,如果客户的IO不一致，需要在方案中主动调用GPIO驱动配置。

<a id="id4"></a>

### 2\. 关于背光

LCD背光控制引脚，需要在方案中调用GPIO驱动配置。

<a id="lcd"></a>

### 3\. 关于lcd设备

BK7258 开发板SDK中默认的LCD RGB设备是ST7701SN,如果客户的设备不一致，需要在方案中添加device设备。

关于devices设备应该如何添加请参考：
\- [LCD设备添加指南](lcd_devices.md)

如果LCD 屏幕需要使用SPI初始化屏幕，需要在创建handle时传入正确的SPI IO引脚， 如果不需要IO初始化，IO传入GPIO\_INVALID\_PIN（-1）。

<a id="api"></a>

## API调用流程概览

RGB LCD Display的典型使用流程如下：

```
┌─────────────────────────────────────────────────────────────┐
│              RGB LCD Display API 调用流程                     │
└─────────────────────────────────────────────────────────────┘

1. 硬件准备        ──→  配置LCD LDO和背光GPIO
                       └─ 使能电源和背光控制

2. bk_display_rgb_new()  ──→  创建RGB LCD控制器实例
                              └─ 配置LCD设备和SPI IO引脚

3. bk_display_open()     ──→  打开显示控制器
                              └─ 初始化LCD硬件

4. bk_display_flush()    ──→  刷新显示（可多次调用）
                              └─ 将帧数据发送到LCD

5. bk_display_close()    ──→  关闭显示控制器
                              └─ 停止硬件，关闭时钟

6. bk_display_delete()   ──→  删除控制器实例
                              └─ 释放资源
```

注意

- 必须按照上述顺序调用API
- 刷新显示前必须先创建并打开控制器
- 操作完成后应及时关闭背光和电源
- 帧释放回调函数必须正确实现，否则会导致内存泄漏

<a id="id6"></a>

## 完整使用示例

以下是一个完整的RGB LCD使用示例，展示了从创建到删除的全过程：

```
#include <components/bk_display/bk_display.h>
#include <components/bk_display/bk_display_types.h>
#include <driver/gpio.h>

#define TAG "lcd_demo"
#define BL_PIN GPIO_7
#define LCD_LDO_PIN GPIO_13

// 帧数据释放回调
static avdk_err_t display_frame_free_cb(void *frame)
{
    frame_buffer_display_free((frame_buffer_t *)frame);
    return AVDK_ERR_OK;
}

avdk_err_t rgb_lcd_demo(void)
{
    avdk_err_t ret = AVDK_ERR_OK;
    bk_display_ctlr_handle_t lcd_display_handle = NULL;
    const lcd_device_t *lcd_device = &lcd_device_st7701sn;

    // 由于LCD和SD卡共用ldo引脚，需要调用平台提供的投票API投票LCD电源
    // 如果客户的板子不需要投票，直接调用GPIO驱动即可
    bk_pm_module_vote_ctrl_external_ldo(GPIO_CTRL_LDO_MODULE_LCD, lcd_ldo_io, GPIO_OUTPUT_STATE_HIGH);

    gpio_dev_unmap(BL_PIN);
    bk_gpio_enable_output(BL_PIN);
    bk_gpio_set_output_high(BL_PIN);

    // 步骤2: 创建RGB LCD控制器
    bk_display_rgb_ctlr_config_t lcd_config = {
        .lcd_device = lcd_device,
        .clk_pin = GPIO_0,
        .cs_pin = GPIO_12,
        .sda_pin = GPIO_1,
        .rst_pin = GPIO_6
    };

    ret = bk_display_rgb_new(&lcd_display_handle, &lcd_config);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_display_rgb_new failed: %d\n", ret);
        return ret;
    }

    // 步骤3: 打开显示控制器
    ret = bk_display_open(lcd_display_handle);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_display_open failed: %d\n", ret);
        bk_display_delete(lcd_display_handle);
        return ret;
    }

    // 步骤4: 分配并刷新显示
    uint32_t frame_size = lcd_device->width * lcd_device->height * 2;
    frame_buffer_t *disp_frame = frame_buffer_display_malloc(frame_size);
    if (disp_frame) {
        disp_frame->fmt = PIXEL_FMT_RGB565;
        disp_frame->width = lcd_device->width;
        disp_frame->height = lcd_device->height;

        ret = bk_display_flush(lcd_display_handle, disp_frame, display_frame_free_cb);
        if (ret != AVDK_ERR_OK) {
            frame_buffer_display_free(disp_frame);
        }
    }

    // 步骤5: 关闭显示
    bk_display_close(lcd_display_handle);

    // 步骤6: 删除控制器
    bk_display_delete(lcd_display_handle);
    lcd_display_handle = NULL;

    // 关闭背光和LDO
    bk_gpio_set_output_low(BL_PIN);
    //关闭LDO
    bk_pm_module_vote_ctrl_external_ldo(GPIO_CTRL_LDO_MODULE_LCD, lcd_ldo_io, GPIO_OUTPUT_STATE_LOW);

    return AVDK_ERR_OK;
}
```

<a id="id7"></a>

## API详细说明

<a id="bk-display-rgb-new-rgb-lcd"></a>

### 1\. bk\_display\_rgb\_new \- 创建RGB LCD控制器

**功能描述:**

创建RGB LCD显示控制器实例，配置LCD设备和SPI初始化引脚。

**函数原型:**

```
avdk_err_t bk_display_rgb_new(bk_display_ctlr_handle_t *handle,
                              const bk_display_rgb_ctlr_config_t *config);
```

**参数说明:**

- handle: \[输出\] 指向显示控制器句柄的指针，成功后存储创建的句柄
- config: \[输入\] RGB LCD控制器配置参数结构体指针

**配置结构体成员说明:**

- lcd\_device: LCD设备指针，包含分辨率、接口类型等信息（必填）
- clk\_pin: SPI时钟引脚，用于LCD初始化（如不需要设为GPIO\_INVALID\_PIN）
- cs\_pin: SPI片选引脚（如不需要设为GPIO\_INVALID\_PIN）
- sda\_pin: SPI数据引脚（如不需要设为GPIO\_INVALID\_PIN）
- rst\_pin: 复位引脚（如不需要设为GPIO\_INVALID\_PIN）

配置结构体参考：[bk\_display\_rgb\_ctlr\_config\_t](../../api-reference/multimedia/bk_display.md#_CPPv428bk_display_rgb_ctlr_config_t)

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_NOMEM: 内存分配失败
- AVDK\_ERR\_INVAL: 参数无效（handle或config为NULL，或lcd\_device为NULL）

**使用注意:**

- lcd\_device参数必须传入有效的设备指针
- 如果LCD不需要SPI初始化，将SPI引脚设置为GPIO\_INVALID\_PIN（-1）
- LCD设备需要提前定义，参考：[LCD设备添加指南](lcd_devices.md)
- 创建成功后，不要立即刷屏，需要先调用bk\_display\_open

**示例代码:**

```
#include <components/bk_display/bk_display.h>
#include <components/bk_display/bk_display_types.h>

bk_display_ctlr_handle_t lcd_display_handle = NULL;
const lcd_device_t *lcd_device = &lcd_device_st7701sn;  // 使用ST7701SN设备

// 创建RGB LCD控制器配置
bk_display_rgb_ctlr_config_t lcd_config = {0};
lcd_config.lcd_device = lcd_device;
lcd_config.clk_pin = GPIO_0;    // SPI时钟引脚
lcd_config.cs_pin = GPIO_12;    // 片选引脚
lcd_config.sda_pin = GPIO_1;    // 数据引脚
lcd_config.rst_pin = GPIO_6;    // 复位引脚

// 创建控制器
avdk_err_t ret = bk_display_rgb_new(&lcd_display_handle, &lcd_config);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to create RGB LCD controller: %d\n", ret);
    return ret;
}
LOGI("RGB LCD controller created: %p\n", lcd_display_handle);
```

<a id="bk-display-open-lcd"></a>

### 2\. bk\_display\_open \- 打开LCD显示控制器

**功能描述:**

打开LCD显示控制器，初始化显示硬件、使能时钟并调用LCD设备的初始化函数。

**函数原型:**

```
avdk_err_t bk_display_open(bk_display_ctlr_handle_t handle);
```

**参数说明:**

- handle: \[输入\] Display控制器句柄（由bk\_display\_rgb\_new创建）

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效（handle为NULL）
- AVDK\_ERR\_DISPLAY: 显示硬件初始化失败

**使用注意:**

- 必须在bk\_display\_rgb\_new之后调用
- 打开前应先配置好LCD LDO和背光GPIO
- 打开失败后建议调用bk\_display\_delete释放资源
- 打开成功后才能调用bk\_display\_flush刷屏

**示例代码:**

```
// 打开LCD LDO（如果客户的板子是直接拉高GPIO，直接调用GPIO驱动即可）
gpio_dev_unmap(GPIO_13);
BK_LOG_ON_ERR(bk_gpio_enable_output(GPIO_13));
BK_LOG_ON_ERR(bk_gpio_pull_up(GPIO_13));
bk_gpio_set_output_high(GPIO_13);

// 打开背光（使用GPIO或PWM控制）
gpio_dev_unmap(GPIO_7);
BK_LOG_ON_ERR(bk_gpio_enable_output(GPIO_7));
BK_LOG_ON_ERR(bk_gpio_pull_up(GPIO_7));
bk_gpio_set_output_high(GPIO_7);

// 打开显示控制器
ret = bk_display_open(lcd_display_handle);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to open display controller: %d\n", ret);
    bk_display_delete(lcd_display_handle);
    return ret;
}
LOGI("Display controller opened successfully\n");
```

<a id="bk-display-flush-lcd"></a>

### 3\. bk\_display\_flush \- 刷新LCD显示

**功能描述:**

将帧数据发送到LCD显示屏进行显示。支持多种像素格式，并可以进行自动格式转换。

**函数原型:**

```
avdk_err_t bk_display_flush(bk_display_ctlr_handle_t handle,
                            void *frame,
                            avdk_err_t (*free_cb)(void *));
```

**参数说明:**

- handle: \[输入\] Display控制器句柄
- frame: \[输入\] 要显示的帧数据指针（frame\_buffer\_t类型）
- free\_cb: \[输入\] 帧数据释放回调函数

**帧结构体成员说明:**

- frame-\>fmt: 源数据格式（PIXEL\_FMT\_RGB565/RGB888/RGB666/YUYV）
- frame-\>width: 源数据宽度（像素）
- frame-\>height: 源数据高度（像素）
- frame-\>frame: 实际的图像数据缓冲区

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效（handle、frame或free\_cb为NULL）
- AVDK\_ERR\_DISPLAY: 显示操作失败

**使用注意:**

- 必须在bk\_display\_open之后调用
- frame和free\_cb都不能为NULL
- 支持的源数据格式：PIXEL\_FMT\_RGB565、PIXEL\_FMT\_RGB888、PIXEL\_FMT\_RGB666、PIXEL\_FMT\_YUYV
- Display模块会自动进行格式转换（源格式-\>LCD输出格式）
- 如果源数据分辨率大于LCD分辨率，会自动裁剪中间区域显示
- 如果源数据分辨率小于LCD分辨率，显示会异常
- 帧释放时机：下一帧刷新时释放前一帧，或在close时释放最后一帧
- 回调函数中必须正确释放帧内存，否则会内存泄漏

**示例代码:**

```
// 帧数据释放回调函数
static avdk_err_t display_frame_free_cb(void *frame)
{
    frame_buffer_display_free((frame_buffer_t *)frame);
    return AVDK_ERR_OK;
}

// 分配显示帧缓冲区，根据屏幕分辨率和像素格式计算帧数据大小
uint32_t frame_size = lcd_device->width * lcd_device->height * 2;  // RGB565格式

frame_buffer_t *disp_frame = frame_buffer_display_malloc(frame_size);
if (!disp_frame) {
    LOGE("Failed to allocate frame buffer\n");
    return AVDK_ERR_NOMEM;
}

// 配置帧参数
disp_frame->fmt = PIXEL_FMT_RGB565;      // 提供刷屏的源数据格式
disp_frame->width = lcd_device->width;   // 源数据像素宽度
disp_frame->height = lcd_device->height; // 源数据像素高度

// 填充图像数据（示例使用随机颜色，用户可根据需求自定义）
lcd_fill_rand_color(frame_size, disp_frame->frame);

// 刷新显示
ret = bk_display_flush(lcd_display_handle, disp_frame, display_frame_free_cb);
if (ret != AVDK_ERR_OK) {
    LOGE("bk_display_flush failed: %d\n", ret);
    // 错误时需要手动释放帧
    display_frame_free_cb(disp_frame);
    return ret;
}
LOGI("Display flushed successfully\n");
```

<a id="bk-display-close-lcd"></a>

### 4\. bk\_display\_close \- 关闭LCD显示控制器

**功能描述:**

关闭LCD显示控制器，停止显示硬件并关闭相关时钟。关闭时会调用最后一帧的释放回调。

**函数原型:**

```
avdk_err_t bk_display_close(bk_display_ctlr_handle_t handle);
```

**参数说明:**

- handle: \[输入\] Display控制器句柄

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效（handle为NULL）

**使用注意:**

- 关闭前会自动调用最后一帧的free\_cb释放回调
- 关闭后handle仍然有效，可以再次调用open
- 建议关闭后同时关闭背光和LDO以节省功耗
- 不再使用时应调用delete释放资源

**示例代码:**

```
// 关闭显示控制器
ret = bk_display_close(lcd_display_handle);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to close display controller: %d\n", ret);
    return ret;
}
LOGI("Display controller closed successfully\n");

// 关闭背光（拉低GPIO或关闭PWM控制）
bk_gpio_set_output_low(GPIO_7);

// 关闭LCD LDO
bk_gpio_set_output_low(GPIO_13);
```

<a id="bk-display-delete-lcd"></a>

### 5\. bk\_display\_delete \- 删除LCD控制器

**功能描述:**

删除LCD控制器实例，释放所有分配的资源。删除后handle将失效，不能再使用。

**函数原型:**

```
avdk_err_t bk_display_delete(bk_display_ctlr_handle_t handle);
```

**参数说明:**

- handle: \[输入\] Display控制器句柄

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效（handle为NULL）

**使用注意:**

- 删除前建议先调用bk\_display\_close
- 如果控制器仍处于打开状态，会自动关闭后再删除
- 删除后应将handle设置为NULL，避免误用
- 删除时会释放所有相关资源

**示例代码:**

```
// 删除显示控制器
ret = bk_display_delete(lcd_display_handle);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to delete display controller: %d\n", ret);
    return ret;
}
lcd_display_handle = NULL;
LOGI("Display controller deleted successfully\n");
```

<a id="id9"></a>

## 使用建议和注意事项

**API调用顺序:**

1. 必须按照 硬件准备 -\> new -\> open -\> flush -\> close -\> delete 的顺序
2. 刷新显示前必须先成功创建并打开控制器
3. 不要在未打开控制器的情况下调用flush

**硬件配置:**

1. LCD LDO引脚（默认GPIO13）需要在open前拉高
2. 背光引脚（项目相关）需要在open前或后使能
3. 如果硬件配置不同，需要修改GPIO引脚定义
4. SPI初始化引脚（clk/cs/sda/rst）根据LCD设备需求配置
5. 不需要SPI初始化的LCD，将引脚设置为GPIO\_INVALID\_PIN（-1）

**帧数据管理:**

1. 帧缓冲区大小 \= width × height × pixel\_byte
2. RGB565格式：pixel\_byte \= 2
3. RGB888格式：pixel\_byte \= 3
4. 帧释放回调函数free\_cb不能为NULL，必须正确实现
5. 回调中必须释放帧内存，否则会导致内存泄漏
6. 多帧显示时，前一帧在下一帧刷新时释放
7. 单帧显示时，在close时释放

**像素格式:**

1. 支持的源数据格式：RGB565、RGB888、RGB666、YUYV
2. Display模块会自动将源格式转换为LCD输出格式
3. YUYV转RGB565/RGB888/RGB666
4. RGB565转RGB888
5. RGB888转RGB565
6. RGB565转RGB666
7. RGB888转RGB666

**分辨率处理:**

1. 源数据分辨率必须 \>\= LCD分辨率
2. 源数据分辨率大于LCD时，自动裁剪中间区域显示
3. 源数据分辨率小于LCD时，显示会异常（不支持）
4. 建议源数据分辨率与LCD分辨率一致

**性能优化:**

1. 对于频繁刷屏的场景，保持控制器打开状态
2. 使用DMA传输可以提高刷屏效率
3. 选择合适的像素格式以平衡内存和显示质量
4. 避免不必要的格式转换以提升性能

**LCD设备:**

1. 使用前需要定义LCD设备（lcd\_device\_t）
2. 设备定义包括：名称、类型、分辨率、RGB参数、初始化函数等
3. 设备添加参考：[LCD设备添加指南](lcd_devices.md)
4. SDK默认支持ST7701SN设备，其他设备需要自行添加

<a id="display-api"></a>

## Display API函数列表

**控制器生命周期管理:**

- bk\_display\_rgb\_new: 创建RGB LCD控制器实例
- bk\_display\_open: 打开显示控制器，初始化硬件
- bk\_display\_close: 关闭显示控制器，停止硬件
- bk\_display\_delete: 删除控制器实例，释放资源

**显示操作:**

- bk\_display\_flush: 刷新显示内容到LCD屏幕

**其他功能:**

- bk\_display\_set\_yuv\_mode: 设置YUV数据模式
- bk\_display\_ioctl: Display控制操作
