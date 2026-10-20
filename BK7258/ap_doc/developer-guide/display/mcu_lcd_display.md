---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/display/mcu_lcd_display.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="mcu-lcd-display"></a>

# mcu\_lcd\_display

<a id="id1"></a>

## 概述

display API接口是对不同接口的屏幕驱动的抽象，客户根据不同的屏幕类型使用对应的接口创建handle。

display hardwarefeature：

1. 支持不同的屏幕类型，如RGB LCD（RGB565,RGB888）、MCU LCD(8线,16线)等。
2. 支持像素转换功能，即输入数据可以和lcd支持的输出数据格式不同，比如可以提供YUYV数据刷屏。
   :   - YUYV到RGB565/RGB888/RGB666的转换
       - RGB565到RGB888的转换
       - RGB888到RGB565的转换
       - RGB565到RGB666的转换
       - RGB888到RGB666的转换
3. RGB565格式使用的GPIO为高位有效， 即R3-R7为高位，G2-G7为高位，B3-B7为高位。

本节主要说明display模块如何驱动MCU LCD，包括其API调用，参数说明以及注意事项。

- 有关RGB LCD显示的示例工程，请参阅：

  - [MCU LCD显示示例工程](../../examples/projects/mcu_lcd_example.md)
- 有关API参考，请参阅：

  - [MCU LCD显示 API](../../api-reference/multimedia/bk_display.md)

<a id="id2"></a>

## 开发介绍

<a id="ldo"></a>

### 1\. 关于电源LDO控制

BK7258 开发板SDK中默认的LCD LDO控制引脚是GPIO13,如果客户的IO不一致，需要在方案中主动调用GPIO驱动配置。

<a id="id3"></a>

### 2\. 关于背光只支持

LCD背光控制引脚，需要在方案中调用GPIO驱动配置。

<a id="lcd"></a>

### 3\. 关于lcd设备

BK7258 开发板SDK中默认的LCD RGB设备是st7796s,如果客户的设备不一致，需要在方案中添加device设备。

关于devices设备应该如何添加请参考：
\- [LCD设备添加指南](lcd_devices.md)

<a id="mcu-816"></a>

### 3\. 关于mcu输出格式（8线16线）配置

MCU接口支持数据线是8线（D0-7）和16线（D0-15）的接口配置，但是对不同的像素格式RGB565/666/888有限制，如下：

> - 8线支持RGB565， RGB888输出：out\_fmt \= PIXEL\_FMT\_RGB565，out\_fmt \= PIXEL\_FMT\_RGB888；
> - 16线只支持RGB666输出：out\_fmt \= PIXEL\_FMT\_RGB666
> - 16线只支持RGB888输出:out\_fmt \= PIXEL\_FMT\_RGB888\_16BIT

如何配置MCU屏的输出格式是在lcd\_device中的lcd\_device\_t中配置out\_fmt。
下面的配置即：Display模块的输入数据源是YUYV数据，MCU接口是8线RGB565，display模块内部将YUYV数据转换为RGB565，输出给MCU LCD。

代码示例

```
const lcd_device_t lcd_device_st7796s =
{
    .id = LCD_DEVICE_ST7796S,
    .name = "st7796s",
    .type = LCD_TYPE_MCU8080,
    .width = 320,
    .height = 480,
    .mcu = &lcd_mcu,
    .src_fmt = PIXEL_FMT_YUYV,
    .out_fmt = PIXEL_FMT_RGB565,
    .lcd_init = lcd_st7796s_init,
    .lcd_off = st7796s_lcd_off,
};
```

<a id="api"></a>

## API调用流程概览

MCU LCD Display的典型使用流程如下：

```
┌─────────────────────────────────────────────────────────────┐
│              MCU LCD Display API 调用流程                     │
└─────────────────────────────────────────────────────────────┘

1. 硬件准备        ──→  配置LCD LDO和背光GPIO
                       └─ 使能电源和背光控制

2. bk_display_mcu_new()  ──→  创建MCU LCD控制器实例
                              └─ 配置LCD设备和TE引脚

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
- MCU LCD使用8线或16线数据总线，需要根据设备配置
- 帧释放回调函数必须正确实现

<a id="id5"></a>

## 完整使用示例

以下是一个完整的MCU LCD使用示例：

```
#include <components/bk_display/bk_display.h>
#include <components/bk_display/bk_display_types.h>
#include <driver/gpio.h>

#define TAG "mcu_lcd_demo"
#define BL_PIN GPIO_7
#define LCD_LDO_PIN GPIO_13

// 帧数据释放回调
static avdk_err_t display_frame_free_cb(void *frame)
{
    frame_buffer_display_free((frame_buffer_t *)frame);
    return AVDK_ERR_OK;
}

avdk_err_t mcu_lcd_demo(void)
{
    avdk_err_t ret = AVDK_ERR_OK;
    bk_display_ctlr_handle_t lcd_display_handle = NULL;
    const lcd_device_t *lcd_device = &lcd_device_st7796s;

    // 步骤1: 配置LDO和背光
    gpio_dev_unmap(LCD_LDO_PIN);
    bk_gpio_enable_output(LCD_LDO_PIN);
    bk_gpio_set_output_high(LCD_LDO_PIN);

    gpio_dev_unmap(BL_PIN);
    bk_gpio_enable_output(BL_PIN);
    bk_gpio_set_output_high(BL_PIN);

    // 步骤2: 创建MCU LCD控制器
    bk_display_mcu_ctlr_config_t lcd_config = {0};
    lcd_config.lcd_device = lcd_device;
    lcd_config.te_pin = GPIO_INVALID_PIN;  // 不使用TE功能

    ret = bk_display_mcu_new(&lcd_display_handle, &lcd_config);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_display_mcu_new failed: %d\n", ret);
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
    bk_gpio_set_output_low(LCD_LDO_PIN);

    return AVDK_ERR_OK;
}
```

<a id="id6"></a>

## API详细说明

<a id="bk-display-mcu-new-mcu-lcd"></a>

### 1\. bk\_display\_mcu\_new \- 创建MCU LCD控制器

**功能描述:**

创建MCU LCD显示控制器实例，配置LCD设备和TE（Tearing Effect）引脚。

**函数原型:**

```
avdk_err_t bk_display_mcu_new(bk_display_ctlr_handle_t *handle,
                              const bk_display_mcu_ctlr_config_t *config);
```

**参数说明:**

- handle: \[输出\] 指向显示控制器句柄的指针，成功后存储创建的句柄
- config: \[输入\] MCU LCD控制器配置参数结构体指针

**配置结构体成员说明:**

- lcd\_device: LCD设备指针，包含分辨率、接口类型等信息（必填）
- te\_pin: Tearing Effect信号引脚（如不需要设为GPIO\_INVALID\_PIN）

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_NOMEM: 内存分配失败
- AVDK\_ERR\_INVAL: 参数无效（handle或config为NULL，或lcd\_device为NULL）

**使用注意:**

- lcd\_device参数必须传入有效的设备指针
- TE功能用于同步显示，避免撕裂效果，如果LCD不支持可设为-1
- LCD设备需要提前定义，参考：[LCD设备添加指南](lcd_devices.md)
- MCU LCD支持8线和16线数据总线

**示例代码:**

```
#include <components/bk_display/bk_display.h>
#include <components/bk_display/bk_display_types.h>

bk_display_ctlr_handle_t lcd_display_handle = NULL;
const lcd_device_t *lcd_device = &lcd_device_st7796s;  // 使用ST7796S设备

// 创建MCU LCD控制器配置
bk_display_mcu_ctlr_config_t lcd_config = {0};
lcd_config.lcd_device = lcd_device;
lcd_config.te_pin = GPIO_INVALID_PIN;  // 不使用TE功能

// 创建控制器
avdk_err_t ret = bk_display_mcu_new(&lcd_display_handle, &lcd_config);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to create MCU LCD controller: %d\n", ret);
    return ret;
}
LOGI("MCU LCD controller created: %p\n", lcd_display_handle);
```

<a id="bk-display-open-lcd"></a>

### 2\. bk\_display\_open \- 打开LCD显示控制器

**功能描述:**

打开LCD显示控制器，初始化显示硬件、使能时钟并调用LCD设备的初始化函数。

*此API在RGB LCD和MCU LCD中通用*

```
avdk_err_t bk_display_open(bk_display_ctlr_handle_t handle);
```

详细说明请参考：[RGB LCD Display \- bk\_display\_open](rgb_lcd_display.md#bk-display-open-lcd)

<a id="bk-display-flush-lcd"></a>

### 3\. bk\_display\_flush \- 刷新LCD显示

**功能描述:**

将帧数据发送到LCD显示屏进行显示。MCU LCD支持RGB565、RGB888、RGB666、YUYV格式的源数据。

*此API在RGB LCD和MCU LCD中通用，但MCU LCD有特殊的数据总线配置*

```
avdk_err_t bk_display_flush(bk_display_ctlr_handle_t handle, void *frame, avdk_err_t (*free_cb)(void *));
```

**MCU LCD特殊说明:**

MCU接口支持8线（D0-D7）和16线（D0-D15）数据总线，对不同像素格式有限制：

- **8线总线**: 支持RGB565、RGB888输出
- **16线总线**: 支持RGB666、RGB888输出

输出格式在lcd\_device的out\_fmt中配置：

```
const lcd_device_t lcd_device_st7796s = {
    .type = LCD_TYPE_MCU8080,
    .width = 320,
    .height = 480,
    .out_fmt = PIXEL_FMT_RGB565,  // 8线总线RGB565输出
    // ...
};
```

详细说明请参考：[RGB LCD Display \- bk\_display\_flush](rgb_lcd_display.md#bk-display-flush-lcd)

<a id="bk-display-close-lcd"></a>

### 4\. bk\_display\_close \- 关闭LCD显示控制器

**功能描述:**

关闭LCD显示控制器，停止显示硬件并关闭相关时钟。

*此API在RGB LCD和MCU LCD中通用*

```
avdk_err_t bk_display_close(bk_display_ctlr_handle_t handle);
```

详细说明请参考：[RGB LCD Display \- bk\_display\_close](rgb_lcd_display.md#bk-display-close-lcd)

<a id="bk-display-delete-lcd"></a>

### 5\. bk\_display\_delete \- 删除LCD控制器

**功能描述:**

删除LCD控制器实例，释放所有分配的资源。

*此API在RGB LCD和MCU LCD中通用*

```
avdk_err_t bk_display_delete(bk_display_ctlr_handle_t handle);
```

详细说明请参考：[RGB LCD Display \- bk\_display\_delete](rgb_lcd_display.md#bk-display-delete-lcd)

<a id="id8"></a>

## 使用建议和注意事项

**MCU LCD数据总线配置:**

1. **8线数据总线（D0-D7）:**
   \- 支持RGB565输出: out\_fmt \= PIXEL\_FMT\_RGB565
   \- 支持RGB888输出: out\_fmt \= PIXEL\_FMT\_RGB888
2. **16线数据总线（D0-D15）:**
   \- 支持RGB666输出: out\_fmt \= PIXEL\_FMT\_RGB666
   \- 支持RGB888输出: out\_fmt \= PIXEL\_FMT\_RGB888\_16BIT
3. 输出格式在lcd\_device\_t结构体的out\_fmt成员中配置

**帧数据格式:**

1. 支持的源数据格式：RGB565、RGB888、YUYV
2. Display模块会自动进行格式转换（源格式-\>MCU输出格式）
3. 源数据通过frame-\>fmt指定，每次刷屏都可以动态改变
4. 输出格式通过lcd\_device-\>out\_fmt固定配置

**API调用顺序和其他注意事项:**

与RGB LCD相同，详细请参考：[RGB LCD Display \- 使用建议和注意事项](rgb_lcd_display.md#id9)

**MCU LCD特有注意事项:**

1. MCU LCD初始化命令需要根据屏厂提供的规格书配置
2. 数据总线宽度（8线/16线）需要与硬件连接匹配
3. 输出格式需要与数据总线宽度匹配，否则显示异常
4. TE功能可选，用于避免显示撕裂
5. 刷屏速度通常低于RGB LCD，取决于时钟频率和数据总线宽度

<a id="display-api"></a>

## Display API函数列表

**控制器生命周期管理:**

- bk\_display\_mcu\_new: 创建MCU LCD控制器实例（MCU专用）
- bk\_display\_open: 打开显示控制器，初始化硬件（通用）
- bk\_display\_close: 关闭显示控制器，停止硬件（通用）
- bk\_display\_delete: 删除控制器实例，释放资源（通用）

**显示操作:**

- bk\_display\_flush: 刷新显示内容到LCD屏幕（通用）

**其他功能:**

- bk\_display\_set\_yuv\_mode: 设置YUV数据模式（通用）
- bk\_display\_ioctl: Display控制操作（通用）
