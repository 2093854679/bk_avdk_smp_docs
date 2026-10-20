---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/gui/lvgl.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="lvgl"></a>

# LVGL

<a id="id1"></a>

## 1、概述

> LVGL(Light and Versatile Graphics Library，轻量级多功能图形库)是一种免费、开源且低消耗的嵌入式图形库，具有丰富且强大的模块化图像组件，可以为任何MCU、MPU及显示类型创建美观的界面，且支持多种输入设备，已成为当前热门的图形用户界面库。
>
> LVGL官方网站地址：<https://lvgl.io> 。
>
> SDK提供了LVGL V8.3.9和LVGL V9.3.0两种版本的源码适配，代码路径：`...\ap\components\lvgl\...`，可通过设置宏 `CONFIG_LVGL_V8` 和 `CONFIG_LVGL_V9` 进行选择版本。

<a id="id2"></a>

## 2、参考工程

> SDK提供了多种类型和用途的LVGL demo参考工程，参考工程的代码路径：`..\projects\lvgl\...`，
> 编译命令：`make bk7258 PROJECT=lvgl/xxx`。
>
> | 工程名 | LCD分辨率 | 数据格式 | 工程说明 |
> | --- | --- | --- | --- |
> | 86box | 480\*480 | RGB565 | 86盒子演示 |
> | benchmark\_v9 | 480\*480 | RGB565 | LVGL官方demo（LVGL V9.3.0） |
> | freetype\_font | 400\*400 | RGB565 | 矢量字体演示（QSPI LCD） |
> | widgets | 480\*480 | RGB565 | LVGL官方demo（LVGL V8.3.9） |
> | widgets\_v9 | 800\*480 | RGB565 | LVGL官方demo（LVGL V9.3.0） |

<a id="id3"></a>

## 3、开发流程

> SDK在对LVGL源码进行适配时已经做好了相应的适配工作，开发者无需再次创建LVGL启动线程，且已适配好输入设备、显示以及文件系统等功能，具体开发流程可按如下进行：

1. 根据所选择LCD屏的数据接口类型以及硬件引脚定义，配置LCD的相关参数，不同接口的屏所配置的LCD参数不一致，具体可以参考display模块。

```
// RGB LCD参数配置
bk_display_rgb_ctlr_config_t rgb_ctlr_config = {
    .lcd_device = &lcd_device_st7701s,
    .clk_pin = GPIO_0,
    .cs_pin = GPIO_12,
    .sda_pin = GPIO_1,
    .rst_pin = GPIO_6,
};
```

2. 创建LCD显示控制器，配置LVGL的参数，调用 `lv_vendor_init()` 初始化LVGL。

```
lv_vnd_config_t lv_vnd_config = {0};

lv_vnd_config.width = rgb_ctlr_config.lcd_device->width;
lv_vnd_config.height = rgb_ctlr_config.lcd_device->height;
lv_vnd_config.render_mode = RENDER_PARTIAL_MODE;
lv_vnd_config.rotation = ROTATE_NONE;
for (int i = 0; i < CONFIG_LVGL_FRAME_BUFFER_NUM; i++) {
    lv_vnd_config.frame_buffer[i] = frame_buffer_display_malloc(lv_vnd_config.width * lv_vnd_config.height * sizeof(bk_color_t));
    if (lv_vnd_config.frame_buffer[i] == NULL) {
        LOGE("lv_frame_buffer[%d] malloc failed\r\n", i);
        return BK_FAIL;
    }
}

bk_display_rgb_new(&lv_vnd_config.handle, &rgb_ctlr_config);
lv_vendor_init(&lv_vnd_config);
```

注意

LCD控制器的handle需要传入lv\_vnd\_config\_t结构体中，方便lvgl刷新显示时获取到LCD控制器handle，所以创建LCD控制器需要在 `lv_vendor_init()` 函数之前进行调用。

3. 打开LCD显示控制器及对应的LCD背光，若存在触摸功能则打开TP功能。

```
bk_display_open(lv_vnd_config.handle);
lcd_backlight_open(GPIO_7);

#if (CONFIG_TP)
    drv_tp_open(lv_vnd_config.width, lv_vnd_config.height, TP_MIRROR_NONE);
#endif
```

4. 调用LVGL提供的组件接口设计所需的UI界面，调用 `lv_vendor_start()` 的接口启动LVGL线程开始调度。

```
lv_vendor_disp_lock();
hor_page_load_main();
lv_vendor_disp_unlock();

lv_vendor_start();
```

注意

1、LVGL是非线程安全的，若UI设计是在不同task中执行，需要添加 `lv_vendor_disp_lock()` 和 `lv_vendor_disp_unlock()` 两个函数进行保护，防止出现异常死机。

2、当设计的UI使用较多的组件功能，尤其是freetype矢量字体功能时，若出现了异常死机，可能是由于LVGL的线程栈空间不足。

<a id="id4"></a>

## 4、参数配置说明

```
typedef struct {
    lv_coord_t width;               /**< Horizontal resolution.*/
    lv_coord_t height;              /**< Vertical resolution.*/
    lvgl_render_mode_t render_mode; /**< Partial mode use sram as draw buffer, other mode use psram as draw_buffer. */
    media_rotate_t rotation;        /**< 0: 0 degree, 1: 90 degree, 2: 180 degree, 3: 270 degree. */
    bk_display_ctlr_handle_t handle;

    /**< The following parameters do not need to be configured by default. */
    uint32_t draw_pixel_size;       /**< v8 size is in pixel, v9 size is in byte. */
    void *draw_buf_2_1;             /**< LVGL draw buffer 1. */
    void *draw_buf_2_2;             /**< LVGL draw buffer 2. Not used by default and only is used when requires high performance. It will cost more memory. */
    frame_buffer_t *frame_buffer[CONFIG_LVGL_FRAME_BUFFER_NUM];    /**< LVGL frame buffer */
} lv_vnd_config_t;
```

LVGL的配置参数主要在上述结构体中定义，但是开发者只需要配置其中的六个参数，其余参数无需配置，具体如下：

> | 参数 | 说明 |
> | --- | --- |
> | width | LVGL的水平坐标 |
> | height | LVGL的垂直坐标 |
> | render\_mode | 渲染模式，见 `lvgl_render_mode_t` 枚举，默认使用partial模式，该模式性能最 佳，使用十分之一屏幕大小的sram作为绘制buffer，然后在disp\_flush()函数中将其 缓存到display buffer中，直至一帧图像完成后发送给屏进行显示。 其余模式使用psram内存，直接整帧绘制并进行显示，其中full mode性能最低，不建 议使用该模式。 |
> | rotation | 旋转角度，见 `media_rotate_t` 枚举。 |
> | handle | LCD控制器handle，在lvgl初始化之前创建好LCD显示控制器并传入。 |
> | frame\_buffer | LVGL显示buffer，数量可通过 `CONFIG_LVGL_FRAME_BUFFER_NUM` 配置，默认为2。 |

<a id="id5"></a>

## 5、开发说明

> | 目录 | 说明 |
> | --- | --- |
> | 图片解码显示 | 在lv\_conf.h文件中打开 `LV_USE_PNG`、`LV_USE_SJPG` 和 `LV_USE_GIF`， 对于大分辨率图像，还需打开 `LV_PNG_USE_PSRAM`、`LV_SJPG_USE_PSRAM` 和 `LV_GIF_USE_PSRAM` 宏来使用psram进行解码。 |
> | 文件系统 | LVGL中适配了LITTLEFS和FATFS两种文件系统，统一使用vfs的接口调用，可在工程中 配置 `CONFIG_VFS`，再依据所需文件系统类型打开对应的宏（`CONFIG_FATFS` 或 `CONFIG_LITTLEFS`），此外，需要主动调用 `lv_vendor_fs_init()` 和 `lv_vendor_fs_deinit()` 进行mount和unmount。 |
> | img\_utility | SDK中提供了img\_utility功能，可通过设置 `CONFIG_LV_IMG_UTILITY_CUSTOMIZE` 使能，主要是提供预先解码到PSRAM的方式来提高解码的速度，且JPEG图片提供了使用 硬件解码的适配。 |
> | freetype字库 | 将字体打包成bin文件烧录到user分区地址，并在工程中设置 `CONFIG_LV_USE_FREETYPE` 来打开LVGL功能。 |
> | 调整工程分区大小 | 只需修改工程中partitions/bk7258文件夹下的 `auto_partitions.csv` 文件分区 ，注意对齐要求，重新编译前需要先make clean。 |
> | 资源文件打包工具 | 根据选择的文件系统类型，使用对应的打包工具进行生成，工具可咨询FAE获取。 |
