---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/display/draw_osd.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="draw-osd"></a>

# draw\_osd

<a id="id1"></a>

## 概述

DRAW\_OSD（On-Screen Display）模块用于在视频或图像上叠加显示文字、图标等OSD元素。
该模块支持图像和字体两种类型的叠加显示，可以动态添加、更新和删除OSD元素。

- 有关OSD显示的示例工程，请参阅：

  - [OSD显示示例工程](../../examples/projects/draw_osd_example.md)
- 有关API参考，请参阅：

  - [OSD显示 API](../../api-reference/multimedia/bk_draw_osd.md)

<a id="id2"></a>

## 开发介绍

OSD控制器是一个用于管理OSD元素的句柄，通过它可以创建、绘制、更新和删除OSD元素。

支持两种融合类型：
:   - 图像混合（BLEND\_TYPE\_IMAGE）：只支持ARGB8888格式的图像
    - 字体混合（BLEND\_TYPE\_FONT）:支持字体工具FontCvt.exe生成的字库

OSD控制器API支持以下接口配置：
:   - 混合资源数组：直接显示预定义的OSD资源数组，包括图标和字体
    - 当前混合信息：当前显示的OSD内容，单独显示一个图标或字体
    - PSRAM使用：是否在PSRAM中绘制

其中资源数组可以使用UI工具生成，具体步骤可以参考：
UI工具的使用请参考:
\<[https://docs.bekencorp.com/arminodoc/bk\_app/ui\_designer/zh\_CN/latest/index.html](../../../../../bk_toolkit/uidesigner/index.md)\>\`\_

<a id="api"></a>

## API调用流程概览

OSD的典型使用流程如下：

```
┌─────────────────────────────────────────────────────────────┐
│                   OSD API 调用流程                            │
└─────────────────────────────────────────────────────────────┘

1. 资源准备         ──→  使用UI工具生成字体和图标资源
                        └─ 生成bk_font.c、bk_img.c、bk_dsc.c、blend.h

2. bk_draw_osd_new()  ──→  创建OSD控制器实例
                        └─ 配置资源数组和绘制参数

3. OSD绘制操作（可多次调用）
   │
   ├─ bk_draw_osd_array()    绘制整个OSD数组
   ├─ bk_draw_osd_image()    绘制单个图像
   └─ bk_draw_osd_font()     绘制单个字体

4. OSD内容管理（可选）
   │
   ├─ bk_draw_osd_add_or_updata()  添加或更新OSD内容
   └─ bk_draw_osd_remove()         删除OSD内容

5. bk_draw_osd_delete()  ──→  删除OSD控制器实例
                           └─ 释放资源
```

注意

- OSD元素必须在创建控制器后才能绘制
- 更新或删除OSD内容后需要重新调用绘制函数才能生效
- 所有OSD元素的名称（name）必须唯一
- 操作完成后应及时删除控制器释放资源

<a id="id3"></a>

## 完整使用示例

以下是一个完整的OSD使用示例，展示了从创建到删除的全过程：

```
#include <components/bk_draw_osd/bk_draw_osd.h>
#include <components/bk_draw_osd/bk_draw_osd_types.h>
#include "blend.h"  // UI工具生成的资源头文件

#define TAG "osd_demo"

avdk_err_t osd_demo(frame_buffer_t *display_frame)
{
    avdk_err_t ret = AVDK_ERR_OK;
    bk_draw_osd_ctlr_handle_t osd_handle = NULL;

    // 步骤1: 创建OSD控制器
    osd_ctlr_config_t osd_config = {
        .blend_assets = blend_assets,  // 总资源数组
        .blend_info = blend_info,      // 默认绘制的资源
        .draw_in_psram = false         // 在SRAM中绘制
    };

    ret = bk_draw_osd_new(&osd_handle, &osd_config);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_draw_osd_new failed: %d\n", ret);
        return ret;
    }
    LOGI("OSD controller created successfully\n");

    // 步骤2: 准备背景信息
    osd_bg_info_t bg_info = {
        .frame = display_frame,  // 显示帧缓冲区
        .width = 854,            // 可见宽度
        .height = 480            // 可见高度
    };

    // 步骤3: 绘制OSD数组
    ret = bk_draw_osd_array(osd_handle, &bg_info, blend_info);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_draw_osd_array failed: %d\n", ret);
        bk_draw_osd_delete(osd_handle);
        return ret;
    }
    LOGI("OSD array drawn successfully\n");

    // 步骤4: 更新OSD内容（可选）
    ret = bk_draw_osd_add_or_updata(osd_handle, "clock", "15:30");
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_draw_osd_add_or_updata failed: %d\n", ret);
    }

    // 重新绘制以应用更新
    ret = bk_draw_osd_array(osd_handle, &bg_info, NULL);

    // 步骤5: 删除OSD控制器
    ret = bk_draw_osd_delete(osd_handle);
    if (ret != AVDK_ERR_OK) {
        LOGE("bk_draw_osd_delete failed: %d\n", ret);
        return ret;
    }
    osd_handle = NULL;
    LOGI("OSD controller deleted successfully\n");

    return AVDK_ERR_OK;
}
```

<a id="id4"></a>

## API详细说明

<a id="id5"></a>

## 代码流程

<a id="id6"></a>

### 1\. 资源准备

通过UI工具生成的文件夹内包含4个文件：

- bk\_font.c 字库资源
- bk\_img.c 图片资源
- bk\_dsc.c 资源数组
- blend.h 头文件

其中bk\_dsc.c文件中包含了资源数组blend\_assets，该数组定义了OSD显示的资源，包括字体和图片。

> - name是融合字体或图标的标签，表示同一类的统合，其位置是相同的。
> - content是融合内容，是可以修改的，比如字符串内容、图片内容等。

```
//总资源
const blend_info_t blend_assets[] =
{
    {.name = "clock", .addr = &font_clock, .content = "12:30"},  //融合标签为clock,字符串内容为12：00
    {.name = "date",  .addr = &font_dates, .content = "2025年2月26日周三"},
    {.name = "ver",   .addr = &font_ver, .content = "v 1.0.0"},
    {.name = "wifi", .addr = &img_wifi_rssi0, .content = "wifi0"},//融合标签为wifi, 融合内容为wifi0
    {.name = "wifi", .addr = &img_wifi_rssi1, .content = "wifi1"},
    {.name = "wifi", .addr = &img_wifi_rssi2, .content = "wifi2"},
    {.name = "wifi", .addr = &img_wifi_rssi3, .content = "wifi3"},
    {.name = "wifi", .addr = &img_wifi_rssi4, .content = "wifi4"},
    {.name = "battery", .addr = &img_battery1, .content = "battery1"},
    {.name = "weather", .addr = &img_cloudy_to_sunny, .content = "cloudy_to_sunny"},
    {.addr = NULL},    //必须且只有最后一个元素为NULL
};
//默认融合的资源
const blend_info_t blend_info[] =
{
    {.name = "clock", .addr = &font_clock, .content = ""},
    {.name = "ver",   .addr = &font_ver, .content = "v 1.0.0"},
    {.name = "wifi", .addr = &img_wifi_rssi0, .content = "wifi0"},
    {.name = "weather", .addr = &img_cloudy_to_sunny, .content = "cloudy_to_sunny"},
    {.addr = NULL},   //必须且只有最后一个元素为NULL
};
```

字体和图标的结构体定义示例如下， 下面的参数均是根据UI图标绘制界面自动生成。

```
GUI_CONST_STORAGE bk_blend_t font_clock =
{
    .version = 0,                          //融合软件版本
    .blend_type = BLEND_TYPE_FONT,          //融合类型
    .name = "clock",                        //融合名称（一类的标签）
    .width = CLOCK_LOGO_W,                  //融合字符串宽度
    .height = CLOCK_LOGO_H,                  //融合字符串高度
    .xpos = 0,                               //融合字符串x坐标(基于画布背景)
    .ypos = 0,                               //融合字符串y坐标(基于画布背景)
    .font =
    {
        .font_digit_type = font_digit_Roboto53, //字体类型
        .color = FONT_COLOR,                    //字体颜色
    },
};

GUI_CONST_STORAGE bk_blend_t img_wifi_rssi0 =
{
    .version = 0,                            //融合软件版本
    .blend_type = BLEND_TYPE_IMAGE,          //融合类型
    .name = "wifi",                          //融合名称（一类的标签）
    .width = WIFI_WIDTH,                     //融合图像宽度
    .height = WIFI_HEIGHT,                   //融合图像高度
    .xpos = WIFI_XPOS,                       //融合图像x坐标(基于画布背景)
    .ypos = WIFI_YPOS,                       //融合图像y坐标(基于画布背景)
    .image =
    {
        .format = ARGB8888,                      //融合图像格式
        .data_len = WIFI_WIDTH * WIFI_HEIGHT * 4, //融合图像数据长度
        .data = wifi_0_argb8888                  //融合图像数据
    },
};
```

<a id="bk-draw-osd-new-osd"></a>

### 2\. bk\_draw\_osd\_new \- 创建OSD控制器

**功能描述:**

创建OSD控制器实例，初始化资源并分配绘制所需的内存。控制器会根据资源数组中最大图标的尺寸自动分配缓冲区（width × height × 4字节）。

**函数原型:**

```
avdk_err_t bk_draw_osd_new(bk_draw_osd_ctlr_handle_t *handle, const osd_ctlr_config_t *config);
```

**参数说明:**

- handle: \[输出\] 指向OSD控制器句柄的指针，成功后存储创建的句柄
- config: \[输入\] OSD控制器配置参数结构体指针

**配置结构体成员说明:**

- blend\_assets: 混合资源总数组，包含所有可用的字体和图标资源
- blend\_info: 默认要绘制的资源数组，可以为NULL
- draw\_in\_psram: 是否在PSRAM中分配绘制缓冲区（true\=PSRAM，false\=SRAM）

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_NOMEM: 内存分配失败
- AVDK\_ERR\_INVAL: 参数无效（handle或config为NULL）

**使用注意:**

- blend\_assets必须以{.addr \= NULL}结尾
- 如果blend\_info为NULL，则不会自动绘制任何内容
- PSRAM绘制适合大尺寸OSD元素，SRAM绘制速度更快
- 创建时会自动分配最大OSD元素尺寸的缓冲区
- 缓冲区大小 \= max(width) × max(height) × 4字节（ARGB8888）

**示例代码:**

```
#include <components/bk_draw_osd/bk_draw_osd.h>
#include <components/bk_draw_osd/bk_draw_osd_types.h>

bk_draw_osd_ctlr_handle_t osd_handle = NULL;

// 创建OSD控制器配置
osd_ctlr_config_t osd_config = {
    .blend_assets = blend_assets,  // 总资源数组
    .blend_info = blend_info,      // 默认绘制的资源（可为NULL）
    .draw_in_psram = false         // 在SRAM中绘制
};

// 创建OSD控制器
avdk_err_t ret = bk_draw_osd_new(&osd_handle, &osd_config);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to create OSD controller: %d\n", ret);
    return ret;
}
LOGI("OSD controller created: %p\n", osd_handle);
```

<a id="bk-draw-osd-array-osd"></a>

### 3\. bk\_draw\_osd\_array \- 绘制OSD数组

**功能描述:**

在背景帧上绘制整个OSD资源数组。此函数会遍历资源数组中的所有元素，逐个绘制到背景帧上。

**函数原型:**

```
avdk_err_t bk_draw_osd_array(bk_draw_osd_ctlr_handle_t handle,
                             const osd_bg_info_t *bg_info,
                             const blend_info_t *info);
```

**参数说明:**

- handle: \[输入\] OSD控制器句柄
- bg\_info: \[输入\] 背景信息结构体指针
- info: \[输入\] 要绘制的混合信息数组，如果为NULL则使用创建时配置的blend\_info

**背景信息结构体成员说明:**

- frame: 显示帧缓冲区指针（frame\_buffer\_t类型）
- width: 可见宽度，即画布的背景宽度
- height: 可见高度，即画布的背景高度

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效
- AVDK\_ERR\_DRAW\_OSD: OSD绘制失败

**使用注意:**

- bg\_info不能为NULL
- bg\_info-\>frame必须是有效的帧缓冲区指针
- info数组必须以{.addr \= NULL}结尾
- 如果info为NULL，使用创建时的blend\_info
- OSD元素坐标不能超出背景帧边界
- 绘制会直接修改背景帧的内容

**示例代码:**

```
// 分配背景帧缓冲区
uint16_t bg_frame_width = 480;
uint16_t bg_frame_height = 854;
uint32_t len = bg_frame_width * bg_frame_height * 2;  // RGB565格式
frame_buffer_t *bg_frame = frame_buffer_display_malloc(len);
AVDK_RETURN_ON_FALSE(bg_frame, AVDK_ERR_NOMEM, TAG, "frame_buffer_display_malloc failed!\n");

// 配置背景帧参数
bg_frame->fmt = PIXEL_FMT_RGB565_LE;
bg_frame->width = bg_frame_width;
bg_frame->height = bg_frame_height;

// 准备背景信息
osd_bg_info_t bg_info = {
    .frame = bg_frame,       // 显示帧缓冲区
    .width = bg_frame_width, // 可见宽度
    .height = bg_frame_height // 可见高度
};

// 绘制OSD数组（使用blend_assets）
ret = bk_draw_osd_array(osd_handle, &bg_info, blend_assets);
if (ret != AVDK_ERR_OK) {
    LOGE("bk_draw_osd_array failed: %d\n", ret);
    frame_buffer_display_free(bg_frame);
    return ret;
}
LOGI("OSD array drawn successfully\n");
```

<a id="bk-draw-osd-image-osd"></a>

### 4\. bk\_draw\_osd\_image \- 绘制单个OSD图像

**功能描述:**

在背景帧上绘制单个图像OSD元素。用于需要单独绘制某个图标的场景。

**函数原型:**

```
avdk_err_t bk_draw_osd_image(bk_draw_osd_ctlr_handle_t handle,
                             const osd_bg_info_t *bg_info,
                             const blend_info_t *info);
```

**参数说明:**

- handle: \[输入\] OSD控制器句柄
- bg\_info: \[输入\] 背景信息结构体指针
- info: \[输入\] 要绘制的图像混合信息

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效
- AVDK\_ERR\_DRAW\_OSD: OSD绘制失败

**使用注意:**

- info指向的资源必须是图像类型（BLEND\_TYPE\_IMAGE）
- 图像必须是ARGB8888格式
- 图像坐标和尺寸不能超出背景帧边界

**示例代码:**

```
// 准备背景信息
osd_bg_info_t bg_info = {
    .frame = display_frame,  // 显示帧缓冲区
    .width = 854,            // 可见宽度
    .height = 480            // 可见高度
};

// 绘制wifi图标（从资源数组中选择）
const blend_info_t wifi_info = {
    .name = "wifi",
    .addr = &img_wifi_rssi0,
    .content = "wifi0"
};

ret = bk_draw_osd_image(osd_handle, &bg_info, &wifi_info);
if (ret != AVDK_ERR_OK) {
    LOGE("bk_draw_osd_image failed: %d\n", ret);
    return ret;
}
```

<a id="bk-draw-osd-font-osd"></a>

### 5\. bk\_draw\_osd\_font \- 绘制单个OSD字体

**功能描述:**

在背景帧上绘制单个字体OSD元素。用于需要单独绘制文字的场景，如时钟、日期等动态文字。

**函数原型:**

```
avdk_err_t bk_draw_osd_font(bk_draw_osd_ctlr_handle_t handle,
                            const osd_bg_info_t *bg_info,
                            const blend_info_t *info);
```

**参数说明:**

- handle: \[输入\] OSD控制器句柄
- bg\_info: \[输入\] 背景信息结构体指针
- info: \[输入\] 要绘制的字体混合信息

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效
- AVDK\_ERR\_DRAW\_OSD: OSD绘制失败

**使用注意:**

- info指向的资源必须是字体类型（BLEND\_TYPE\_FONT）
- content字段必须包含要显示的文字内容
- 字体必须使用FontCvt.exe工具生成
- 字体坐标和尺寸不能超出背景帧边界

**示例代码:**

```
// 准备背景信息
osd_bg_info_t bg_info = {
    .frame = display_frame,  // 显示帧缓冲区
    .width = 854,            // 可见宽度
    .height = 480            // 可见高度
};

// 绘制时钟字体
const blend_info_t clock_info = {
    .name = "clock",
    .addr = &font_clock,
    .content = "12:30"
};

ret = bk_draw_osd_font(osd_handle, &bg_info, &clock_info);
if (ret != AVDK_ERR_OK) {
    LOGE("bk_draw_osd_font failed: %d\n", ret);
    return ret;
}
```

<a id="bk-draw-osd-add-or-updata-osd"></a>

### 6\. bk\_draw\_osd\_add\_or\_updata \- 添加或更新OSD内容

**功能描述:**

向OSD资源数组中添加新内容或更新现有内容。此函数只是修改内存中的资源数组，需要重新调用绘制函数才能显示。

**函数原型:**

```
avdk_err_t bk_draw_osd_add_or_updata(bk_draw_osd_ctlr_handle_t handle,
                                     const char *name,
                                     const char *content);
```

**参数说明:**

- handle: \[输入\] OSD控制器句柄
- name: \[输入\] OSD元素名称标签
- content: \[输入\] 新的内容字符串

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效
- AVDK\_ERR\_NOTFOUND: 未找到指定名称的OSD元素

**使用注意:**

- name必须在blend\_assets数组中存在
- content会替换该name对应的所有元素的内容
- 对于字体类型，content是要显示的文字
- 对于图像类型，content是用于选择资源的标识
- 调用后必须重新调用bk\_draw\_osd\_array才能看到更新效果

**示例代码:**

```
// 更新时钟内容
ret = bk_draw_osd_add_or_updata(osd_handle, "clock", "13:45");
if (ret != AVDK_ERR_OK) {
    LOGE("bk_draw_osd_add_or_updata failed: %d\n", ret);
    return ret;
}

// 更新wifi图标
ret = bk_draw_osd_add_or_updata(osd_handle, "wifi", "wifi3");
if (ret != AVDK_ERR_OK) {
    LOGE("bk_draw_osd_add_or_updata failed: %d\n", ret);
    return ret;
}

// 重新绘制以应用更新
ret = bk_draw_osd_array(osd_handle, &bg_info, NULL);
```

<a id="bk-draw-osd-remove-osd"></a>

### 7\. bk\_draw\_osd\_remove \- 删除OSD内容

**功能描述:**

从OSD资源数组中删除指定名称的所有元素。此函数只是修改内存中的资源数组，需要重新调用绘制函数才能生效。

**函数原型:**

```
avdk_err_t bk_draw_osd_remove(bk_draw_osd_ctlr_handle_t handle, const char *name);
```

**参数说明:**

- handle: \[输入\] OSD控制器句柄
- name: \[输入\] 要删除的OSD元素名称

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效
- AVDK\_ERR\_NOTFOUND: 未找到指定名称的OSD元素

**使用注意:**

- 会删除所有具有该name的OSD元素
- 调用后必须重新调用bk\_draw\_osd\_array才能看到删除效果
- 删除后该name的所有内容都不会再显示

**示例代码:**

```
// 删除时钟显示
ret = bk_draw_osd_remove(osd_handle, "clock");
if (ret != AVDK_ERR_OK) {
    LOGE("bk_draw_osd_remove failed: %d\n", ret);
    return ret;
}

// 删除wifi图标
ret = bk_draw_osd_remove(osd_handle, "wifi");
if (ret != AVDK_ERR_OK) {
    LOGE("bk_draw_osd_remove failed: %d\n", ret);
    return ret;
}

// 重新绘制以应用删除
ret = bk_draw_osd_array(osd_handle, &bg_info, NULL);
```

<a id="bk-draw-osd-delete-osd"></a>

### 8\. bk\_draw\_osd\_delete \- 删除OSD控制器

**功能描述:**

删除OSD控制器实例，释放所有分配的资源和缓冲区。删除后handle将失效，不能再使用。

**函数原型:**

```
avdk_err_t bk_draw_osd_delete(bk_draw_osd_ctlr_handle_t handle);
```

**参数说明:**

- handle: \[输入\] OSD控制器句柄

**返回值:**

- AVDK\_ERR\_OK: 成功
- AVDK\_ERR\_INVAL: 参数无效（handle为NULL）

**使用注意:**

- 删除后应将handle设置为NULL，避免误用
- 删除时会自动释放创建时分配的绘制缓冲区
- 不再使用OSD时应及时删除以释放资源

**示例代码:**

```
// 删除OSD控制器
ret = bk_draw_osd_delete(osd_handle);
if (ret != AVDK_ERR_OK) {
    LOGE("Failed to delete OSD controller: %d\n", ret);
    return ret;
}
osd_handle = NULL;
LOGI("OSD controller deleted successfully\n");
```

<a id="id7"></a>

## 使用建议和注意事项

**资源配置:**

1. 资源数组必须以\`{.addr \= NULL}\`结尾作为结束标志
2. OSD元素的name（名称标签）用于标识同一类元素，可以有多个相同name的元素
3. OSD元素的content必须唯一，用于区分同name下的不同资源
4. 图像混合只支持ARGB8888格式的图像数据
5. 字体混合需要使用FontCvt.exe工具生成正确的字体库
6. UI工具的使用请参考: [https://docs.bekencorp.com/arminodoc/bk\_app/ui\_designer/zh\_CN/latest/index.html](../../../../../bk_toolkit/uidesigner/index.md)

**坐标和尺寸:**

1. 所有OSD元素的坐标(xpos, ypos)都是相对于背景帧的原点(0,0)
2. OSD元素的(xpos \+ width)不能超过背景帧的width
3. OSD元素的(ypos \+ height)不能超过背景帧的height
4. 坐标超出边界会导致绘制失败或显示异常

**内存管理:**

1. 创建OSD控制器时会自动分配绘制缓冲区
2. 缓冲区大小由资源数组中最大的OSD元素决定
3. PSRAM绘制适合大尺寸OSD，SRAM绘制速度更快但内存有限
4. 不再使用时应及时调用bk\_draw\_osd\_delete释放资源

**动态更新:**

1. 调用bk\_draw\_osd\_add\_or\_updata或bk\_draw\_osd\_remove只修改内存数组
2. 修改后必须重新调用bk\_draw\_osd\_array才能应用到显示
3. 更新content时会查找匹配的name和content，找到后替换
4. 删除name时会删除所有具有该name的元素

**性能优化:**

1. 如果OSD内容不频繁变化，可以复用同一个背景帧
2. 对于动态内容（如时钟），只更新变化的部分而不是重绘全部
3. 大量OSD元素建议使用PSRAM绘制，避免SRAM不足
4. 绘制顺序会影响层叠效果，后绘制的元素会覆盖先绘制的

**与DMA2D配合使用:**

1. OSD绘制内部使用DMA2D进行图像混合
2. 需要确保DMA2D硬件资源可用
3. 图像格式必须正确，否则DMA2D操作可能失败
4. OSD控制器与DMA2D控制器可以共存

<a id="id8"></a>

## OSD API函数列表

**控制器管理:**

- bk\_draw\_osd\_new: 创建OSD控制器实例
- bk\_draw\_osd\_delete: 删除OSD控制器实例，释放资源

**OSD绘制操作:**

- bk\_draw\_osd\_array: 绘制整个OSD资源数组
- bk\_draw\_osd\_image: 绘制单个图像OSD元素
- bk\_draw\_osd\_font: 绘制单个字体OSD元素

**OSD内容管理:**

- bk\_draw\_osd\_add\_or\_updata: 添加或更新OSD元素内容
- bk\_draw\_osd\_remove: 删除指定名称的OSD元素
