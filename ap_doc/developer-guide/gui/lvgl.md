---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/gui/lvgl.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="lvgl"></a>

# LVGL开发者指南

<a id="id1"></a>

## 1、概述

LVGL（Light and Versatile Graphics Library）是一个面向嵌入式设备的开源 GUI 图形库，提供按钮、列表、滑条、图表、图片、字体、动画、输入设备等常用界面能力。LVGL 官方网站为 <https://lvgl.io> 。

BK7259 SDK 已集成 LVGL 适配层，源码位于 `ap/components/lvgl`。当前支持两套版本：

- `lvgl_v8`：LVGL V8.3.9，适合维护已有 V8 项目。
- `lvgl_v9`：LVGL V9.3.0，适合新项目优先使用。

开发者通常不需要自己移植 `lv_init()`、tick、显示刷新线程和输入设备框架。应用侧需要完成的是：选择 LVGL 版本，初始化显示硬件，配置 `lv_vnd_config_t`，创建 UI 页面，然后启动 SDK 提供的 LVGL vendor 线程。

<a id="id2"></a>

## 2、快速上手

<a id="id3"></a>

### 2.1 先运行参考工程

建议新手先跑通 `widgets_v9`，确认屏幕、触摸、DPU、frame buffer 和 LVGL vendor 适配层都能正常工作。

参考工程位于 SDK 根目录下的 `projects/lvgl`，不是 `ap/projects`。

| 工程 | LVGL版本 | 默认显示配置 | 适用场景 |
| --- | --- | --- | --- |
| `projects/lvgl/widgets_v9` | V9.3.0 | MIPI DSI，1080x1920，ARGB8888，DPU解压 | 新项目优先参考 |
| `projects/lvgl/widgets_v8` | V8.3.9 | MIPI DSI，1080x1920，RGB565 | 维护或验证 V8 项目 |

在 SDK 根目录执行：

```
make bk7259 PROJECT=lvgl/widgets_v9
```

如使用 Docker 编译环境，可执行：

```
./dbuild.sh make bk7259 PROJECT=lvgl/widgets_v9
```

编译、烧录并复位开发板后，屏幕应显示 LVGL 官方 Widgets Demo。若黑屏或触摸无响应，应先排查 LCD 型号、分辨率、背光 GPIO、reset GPIO、TP GPIO/I2C 配置是否与硬件一致。

<a id="id4"></a>

### 2.2 了解最小开发路径

基于参考工程开发自己的 UI，一般按以下步骤进行：

1. 复制或新建一个工程目录，优先参考 `projects/lvgl/widgets_v9`。
2. 在工程 `ap/config/bk7259_ap/defconfig` 中打开 LVGL、显示、DPU、frame buffer、LCD 和 TP 配置。
3. 在 `ap/ap_main.c` 中适配自己的 LCD panel、分辨率、背光和触摸配置。
4. 保留 `lv_vendor_init()`、`drv_tp_open()`、`lv_vendor_start()` 等启动流程。
5. 将 `lv_demo_widgets()` 替换为自己的 UI 创建函数。
6. 新增图片、字体、页面源码后，把对应 `.c` 文件加入工程 `ap/CMakeLists.txt`。

<a id="id5"></a>

## 3、关键目录

| 路径 | 说明 |
| --- | --- |
| `ap/components/lvgl/Kconfig` | LVGL 版本、任务栈、frame buffer 数量、GPU 绘制等 Kconfig 配置。 |
| `ap/components/lvgl/common/lv_vendor.h` | SDK LVGL vendor 适配层对应用暴露的主要接口和 `lv_vnd_config_t`。 |
| `ap/components/lvgl/common/lv_vendor.c` | LVGL 初始化、线程、锁、tick、frame buffer 队列等实现。 |
| `ap/components/lvgl/lvgl_v8` | LVGL V8.3.9 源码和 porting。 |
| `ap/components/lvgl/lvgl_v9` | LVGL V9.3.0 源码和 porting。 |
| `projects/lvgl/widgets_v9/ap/ap_main.c` | 推荐参考的 LVGL V9 显示与 UI 启动流程。 |
| `projects/lvgl/widgets_v9/ap/lv_conf_custom.h` | 工程级 LVGL 功能裁剪和字体配置覆盖。 |
| `projects/lvgl/widgets_v9/ap/assets` | Widgets Demo 使用的 C 数组图片资源。 |

<a id="id6"></a>

## 4、工程配置

<a id="id7"></a>

### 4.1 选择 LVGL 版本

在工程 `defconfig` 中打开 LVGL，并选择一个版本：

```
CONFIG_LVGL=y
CONFIG_LVGL_V9=y
# CONFIG_LVGL_V8 is not set
```

如果维护 V8 工程，则选择：

```
CONFIG_LVGL=y
CONFIG_LVGL_V8=y
# CONFIG_LVGL_V9 is not set
```

注意

V8 和 V9 的 API 存在差异，UI 代码不要混用。新项目建议优先使用 `widgets_v9` 作为模板。

<a id="id8"></a>

### 4.2 打开显示和触摸依赖

以 `widgets_v9` 为例，常见关键配置如下：

| 配置项 | 作用 |
| --- | --- |
| `CONFIG_BK_DISPLAY=y` | 启用 SDK display 框架。 |
| `CONFIG_DPU_DRIVER=y` | 启用 DPU 显示控制器。 |
| `CONFIG_DSI_DRIVER=y`、`CONFIG_MIPI_DSI=y` | 启用 MIPI DSI 显示总线。 |
| `CONFIG_FRAME_BUFFER=y` | 启用 frame buffer 分配与管理。 |
| `CONFIG_LCD_HX8399C_MIPI_1080x1920=y` | 启用参考工程默认 LCD 驱动，实际项目应替换为自己的 LCD。 |
| `CONFIG_TP=y` | 启用触摸。 |
| `CONFIG_TP_RST_PIN`、`CONFIG_TP_INT_PIN`、`CONFIG_TP_I2C_SDA_PIN`、`CONFIG_TP_I2C_SCL_PIN` | 配置触摸 reset、interrupt 和 I2C 引脚。 |

<a id="id9"></a>

### 4.3 调整 LVGL 任务参数

`ap/components/lvgl/Kconfig` 中提供以下常用参数：

| 配置项 | 说明 |
| --- | --- |
| `CONFIG_LVGL_TASK_PRIORITY` | LVGL vendor 线程优先级，默认 4。 |
| `CONFIG_LVGL_TASK_STACK_SIZE` | LVGL vendor 线程栈大小，默认 8192。复杂页面、较多字体或 GPU 绘制可适当增大。 |
| `CONFIG_LVGL_FRAME_BUFFER_NUM` | 显示 frame buffer 数量，默认 2。direct/full 模式只能配置为 2。 |
| `CONFIG_LVGL_TASK_SLEEP_TIME_CUSTOMIZE` | 是否自定义 LVGL 线程休眠时间。 |
| `CONFIG_LV_USE_PERF_MONITOR` | 显示 LVGL 性能监视信息。 |
| `CONFIG_LV_USE_DRAW_VG_LITE` | LVGL V9 使用 VG-Lite GPU 绘制能力。 |
| `CONFIG_LVGL_USE_GPU_ROTATE` | 启用 GPU 旋转相关支持。 |

<a id="lv-conf-custom-h"></a>

### 4.4 lv\_conf\_custom.h配置机制

LVGL 本身大量功能通过 `LV_USE_xxx`、`LV_FONT_xxx`、`LV_COLOR_xxx` 等宏裁剪，这些宏最终由 LVGL 的 `lv_conf.h` 生效。BK7259 SDK 在 LVGL 组件中增加了工程级覆盖机制：如果当前方案工程存在 `ap/lv_conf_custom.h`，构建系统会自动为 LVGL 组件设置 `LV_CONF_PATH`，让 LVGL 编译时使用这个工程级配置文件。

这个机制的目的是把“SDK 默认配置”和“产品工程差异配置”分开：

- `ap/components/lvgl` 下的默认 `lv_conf.h` 由 SDK 维护，作为公共基线。
- 方案工程自己的 `ap/lv_conf_custom.h` 用来覆盖本工程需要打开或关闭的 LVGL 功能。
- 新增字体、demo、图片解码、复杂控件、文件系统驱动等 LVGL 宏时，优先改工程目录下的 `lv_conf_custom.h`。
- 不建议直接修改 `ap/components/lvgl` 组件内的公共配置，否则会影响其它工程，也不利于后续 SDK 升级合并。

参考工程 `projects/lvgl/widgets_v9/ap/lv_conf_custom.h` 的写法如下：

```
#ifndef PROJECT_LV_CONF_CUSTOM_H
#define PROJECT_LV_CONF_CUSTOM_H

#include "lv_conf.h"

#undef LV_USE_DEMO_WIDGETS
#define LV_USE_DEMO_WIDGETS 1

#undef LV_FONT_MONTSERRAT_24
#define LV_FONT_MONTSERRAT_24 1

#endif /* PROJECT_LV_CONF_CUSTOM_H */
```

使用时要注意两点：

1. 先 `#include "lv_conf.h"`，继承 SDK 默认配置。
2. 对需要变更的宏先 `#undef` 再 `#define`，只覆盖本工程真正需要修改的选项。

如果某个 LVGL 控件编译时报错提示 “Enable it in lv\_conf.h”，在 BK7259 工程中通常应理解为：到当前工程的 `ap/lv_conf_custom.h` 中打开对应宏。例如使用官方 Widgets Demo 需要打开 `LV_USE_DEMO_WIDGETS`，使用某个字号需要打开对应 `LV_FONT_MONTSERRAT_xx`。

注意

`defconfig` 负责打开 SDK 组件级能力，例如 `CONFIG_LVGL`、`CONFIG_LVGL_V9`、`CONFIG_BK_DISPLAY`；`lv_conf_custom.h` 负责打开 LVGL 库内部能力，例如 demo、控件、字体、主题、图片解码等。两者作用不同，开发时不要混淆。

<a id="id10"></a>

## 5、LVGL启动流程

参考 `projects/lvgl/widgets_v9/ap/ap_main.c`，应用启动流程如下：

1. `bk_init()` 初始化系统。
2. `media_service_init()` 初始化多媒体服务。
3. `bk_frame_buffer_init()` 初始化 frame buffer。
4. 创建显示总线，例如 `bk_display_dsi_bus_new()`。
5. 创建 LCD panel，例如 `bk_lcd_mipi_panel_new()`。
6. 创建 DPU 显示控制器，例如 `bk_display_dpu_ctlr_new()`。
7. 调用 `bk_display_init()` 和 `bk_display_open()` 初始化并打开显示。
8. 打开 LCD 背光。
9. 配置 `lv_vnd_config_t`。
10. 申请 `CONFIG_LVGL_FRAME_BUFFER_NUM` 个显示 frame buffer。
11. 调用 `lv_vendor_init()` 初始化 LVGL vendor 适配层。
12. 如果启用触摸，调用 `drv_tp_open()`。
13. 加锁创建 UI 页面。
14. 调用 `lv_vendor_start()` 启动 LVGL vendor 线程。

典型代码结构如下：

```
static void app_lvgl_flush_cb(void *args, void *frame_buffer, int (*cb)(void *args))
{
    bk_display_flush(args, frame_buffer, cb);
}

static bk_err_t app_lvgl_init(void)
{
    lv_vnd_config_t config = {0};

    /* 1. Create display bus, LCD panel and DPU controller first. */
    bk_display_dsi_bus_new(&disp_ctx.dis_bus_handle, NULL);
    bk_lcd_mipi_panel_new(disp_ctx.dis_bus_handle,
                          &panel_config,
                          &lcd_device_hx8399c_mipi_1080x1920,
                          &disp_ctx.panel_handle);
    bk_display_dpu_ctlr_new(&disp_ctx.dpu_ctlr_handle,
                            disp_ctx.panel_handle,
                            &dpu_config);
    bk_display_init(disp_ctx.dpu_ctlr_handle);
    bk_display_open(disp_ctx.dpu_ctlr_handle);

    /* 2. Configure LVGL vendor layer. */
    config.width = 1080;
    config.height = 1920;
    config.render_mode = RENDER_PARTIAL_MODE;
    config.rotation = ROTATE_NONE;
    config.disp_width = config.width;
    config.disp_height = config.height;
    config.args = disp_ctx.dpu_ctlr_handle;
    config.flush_cb = app_lvgl_flush_cb;

    for (int i = 0; i < CONFIG_LVGL_FRAME_BUFFER_NUM; i++) {
        config.frame_buffer[i] =
            bk_frame_buffer_malloc(MEM_SLAB_HEAP_UNCODED,
                                   config.disp_width * config.disp_height * sizeof(bk_color_t));
    }

    lv_vendor_init(&config);

#if CONFIG_TP
    drv_tp_open(config.width, config.height, TP_MIRROR_NONE);
#endif

    lv_vendor_disp_lock();
    my_ui_create();
    lv_vendor_disp_unlock();

    lv_vendor_start();
    return BK_OK;
}
```

注意

显示控制器必须先创建并打开，再调用 `lv_vendor_init()`。当前 `lv_vnd_config_t` 不再使用旧文档中的 `handle` 字段，而是通过 `args` 保存显示控制器句柄，通过 `flush_cb` 完成显示刷新。

<a id="lv-vnd-config-t"></a>

## 6、lv\_vnd\_config\_t说明

`lv_vnd_config_t` 定义在 `ap/components/lvgl/common/lv_vendor.h`。应用侧最常配置以下字段：

| 字段 | 说明 |
| --- | --- |
| `width`、`height` | LVGL 逻辑分辨率，应与 UI 设计和触摸坐标匹配。 |
| `render_mode` | 渲染模式。常用 `RENDER_PARTIAL_MODE`，内存占用较低，适合大多数应用。 |
| `rotation` | 显示旋转角度，类型为 `rott_angle_t`。 |
| `args` | 传给 `flush_cb` 的用户参数，通常保存 DPU/display 控制器句柄。 |
| `flush_cb` | LVGL flush 回调，通常封装 `bk_display_flush(args, frame_buffer, cb)`。 |
| `frame_buffer[]` | 显示 frame buffer 数组，数量由 `CONFIG_LVGL_FRAME_BUFFER_NUM` 决定。 |
| `draw_pixel_size` | partial mode 下绘制 buffer 大小。V8 单位为像素，V9 单位为字节；不配置时使用默认值。 |
| `draw_buf_2_1`、`draw_buf_2_2` | 自定义 LVGL draw buffer。一般无需配置。 |
| `output_compress` | partial mode 下的压缩输出开关，通常配合 DPU 解压和 GPU 使用。 |
| `disp_width`、`disp_height` | 实际显示 buffer 宽高。普通场景可等于 `width`、`height`；压缩输出时可能需要按对齐要求放大。 |

渲染模式选择建议：

- `RENDER_PARTIAL_MODE`：推荐默认使用。LVGL 分块绘制，内存占用较低。
- `RENDER_DIRECT_MODE`：使用屏幕大小 buffer，适合特定性能优化场景，`CONFIG_LVGL_FRAME_BUFFER_NUM` 必须配置为 2。
- `RENDER_FULL_MODE`：每次重绘整屏，性能和内存压力较大，一般不建议使用。

<a id="ui"></a>

## 7、创建自己的UI

<a id="demo"></a>

### 7.1 替换官方Demo

参考工程默认在 `lv_vendor_start()` 前调用 `lv_demo_widgets()`。开发自己的应用时，将它替换为自己的页面创建函数即可：

```
lv_vendor_disp_lock();
my_ui_create();
lv_vendor_disp_unlock();

lv_vendor_start();
```

`my_ui_create()` 中可以直接使用 LVGL API 创建控件：

```
void my_ui_create(void)
{
    lv_obj_t *screen = lv_screen_active();

    lv_obj_t *label = lv_label_create(screen);
    lv_label_set_text(label, "Hello BK7259 LVGL");
    lv_obj_center(label);

    lv_obj_t *button = lv_button_create(screen);
    lv_obj_align(button, LV_ALIGN_BOTTOM_MID, 0, -40);
}
```

<a id="id11"></a>

### 7.2 线程安全要求

LVGL 不是线程安全的。除 LVGL vendor 线程自身调用外，其他 task 中只要调用 LVGL API 创建、删除或修改 UI，都必须加锁：

```
lv_vendor_disp_lock();
/* LVGL API calls */
lv_vendor_disp_unlock();
```

如果缺少锁，常见现象包括随机死机、对象访问异常、显示刷新过程中崩溃。

<a id="id12"></a>

### 7.3 页面组织建议

小型应用可以从一个 `ui_main.c` 开始；页面增多后建议拆成：

```
ap/
├── ui/
│   ├── ui_main.c
│   ├── ui_home.c
│   ├── ui_settings.c
│   └── ui_assets.h
├── assets/
│   ├── img_logo.c
│   └── img_icon_wifi.c
└── ap_main.c
```

新增源码后，需要在工程 `ap/CMakeLists.txt` 中加入对应文件，否则会出现链接错误。

<a id="id13"></a>

## 8、适配显示硬件

如果参考工程不能直接点亮自己的屏，优先修改显示硬件，而不是修改 LVGL 控件代码。

常见需要同步修改的位置：

| 修改项 | 说明 |
| --- | --- |
| LCD 头文件 | 例如将 `lcd_mipi_hx8399c_1080x1920.h` 替换为实际屏驱动头文件。 |
| LCD device 对象 | 替换 `bk_lcd_mipi_panel_new()` 中传入的 `lcd_device_xxx`。 |
| 分辨率 | 同步修改 `width`、`height`、DPU `disp_w`、`disp_h` 等参数。 |
| LCD reset GPIO | 修改 `bk_lcd_panel_config_t.reset_pin`。 |
| 背光 GPIO | 修改背光 GPIO 初始化和输出逻辑。 |
| LCD Kconfig | 在 `defconfig` 中打开实际 LCD 驱动对应的 `CONFIG_LCD_xxx`。 |
| TP Kconfig | 修改触摸 IC 和 TP GPIO/I2C 配置。 |

备注

黑屏、花屏、触摸偏移通常不是 LVGL 控件问题。先确认 LCD 驱动、时序、像素格式、分辨率、背光和触摸坐标方向正确。

<a id="id14"></a>

## 9、资源、字体和配置

<a id="id15"></a>

### 9.1 图片资源

最简单可靠的方式是把图片转换为 LVGL C 数组资源，放入工程 `ap/assets`，并加入 `ap/CMakeLists.txt`。参考 `widgets_v9/ap/assets` 中的 `img_lvgl_logo.c` 等文件。

使用步骤：

1. 使用 LVGL 图片转换工具生成 `.c` 图片资源。
2. 将资源文件放入 `ap/assets`。
3. 在 `ap/CMakeLists.txt` 的源码列表中加入资源文件。
4. 在 UI 代码中使用 `LV_IMAGE_DECLARE(img_xxx)` 声明后创建图片对象。

示例：

```
LV_IMAGE_DECLARE(img_logo);

lv_obj_t *image = lv_image_create(lv_screen_active());
lv_image_set_src(image, &img_logo);
lv_obj_center(image);
```

<a id="id16"></a>

### 9.2 字体

字体相关宏属于 LVGL 库内部裁剪项，应在工程级 `ap/lv_conf_custom.h` 中配置。该文件会先包含 SDK 默认 `lv_conf.h`，再通过 `#undef`/`#define` 覆盖本工程需要的字体、demo 或控件开关。

参考工程通过 `lv_conf_custom.h` 打开 Montserrat 字体和官方 demo，例如：

```
#include "lv_conf.h"

#undef LV_USE_DEMO_WIDGETS
#define LV_USE_DEMO_WIDGETS 1

#undef LV_FONT_MONTSERRAT_24
#define LV_FONT_MONTSERRAT_24 1

#undef LV_FONT_MONTSERRAT_20
#define LV_FONT_MONTSERRAT_20 1

#undef LV_FONT_MONTSERRAT_16
#define LV_FONT_MONTSERRAT_16 1
```

字体越多、字号越多，代码体积和内存压力越大。中文字体或矢量字体需要结合项目资源方案单独评估。

<a id="id17"></a>

### 9.3 LVGL文件系统

SDK 中提供了 LVGL 文件系统适配代码，位于 `ap/components/lvgl/common/vfs`。如果 UI 需要从文件系统加载图片、字体或其他资源，需要同时确认：

- 工程已启用 VFS 和目标文件系统。
- 分区表中有足够空间保存资源。
- 资源已按项目要求烧录或挂载。
- LVGL 文件路径使用了适配层支持的盘符和路径格式。

文件系统资源方案和烧录方式与具体产品分区有关，建议在项目分区确定后再接入。

<a id="v8v9"></a>

## 10、V8与V9差异

| 对比项 | `widgets_v8` | `widgets_v9` |
| --- | --- | --- |
| LVGL版本 | V8.3.9 | V9.3.0 |
| Kconfig | `CONFIG_LVGL_V8=y` | `CONFIG_LVGL_V9=y` |
| 默认像素格式 | `BK_PIXEL_FORMAT_RGB565` | `BK_PIXEL_FORMAT_ARGB8888` |
| DPU解压 | 默认关闭 | 默认开启 |
| 压缩输出 | 默认关闭 | 默认开启 `output_compress` |
| 推荐场景 | 维护已有 V8 项目 | 新项目优先使用 |

迁移 V8 UI 到 V9 时，不建议直接复制后强行编译。应先用 `widgets_v9` 跑通底层显示和触摸，再按 LVGL V9 API 逐个页面迁移。

<a id="id18"></a>

## 11、常见问题

<a id="id19"></a>

### 11.1 编译找不到LVGL符号

检查：

- 是否打开 `CONFIG_LVGL=y` 并选择了 `CONFIG_LVGL_V8` 或 `CONFIG_LVGL_V9`。
- UI 代码使用的 API 是否匹配当前 LVGL 版本。
- 新增 `.c` 文件或图片资源是否加入 `ap/CMakeLists.txt`。
- `lv_conf_custom.h` 是否打开了用到的 demo、控件、字体或图片解码选项。

<a id="id20"></a>

### 11.2 屏幕黑屏

优先检查：

- LCD 型号和 `lcd_device_xxx` 是否匹配。
- DSI/RGB/SPI 接口、时序、分辨率和像素格式是否正确。
- 背光 GPIO 是否输出有效电平。
- LCD reset GPIO 是否正确。
- `bk_display_init()`、`bk_display_open()` 是否执行成功。
- frame buffer 是否申请成功。

<a id="id21"></a>

### 11.3 触摸无响应或坐标错误

检查：

- `CONFIG_TP=y` 是否开启。
- TP reset、interrupt、I2C SDA/SCL GPIO 是否匹配硬件。
- 当前触摸 IC 驱动是否打开。
- `drv_tp_open(width, height, mirror)` 的宽高和镜像参数是否与屏幕方向一致。

<a id="id22"></a>

### 11.4 UI运行一段时间后死机

常见原因：

- 在其他 task 中调用 LVGL API 时没有使用 `lv_vendor_disp_lock()` 和 `lv_vendor_disp_unlock()`。
- 页面复杂、字体较多或启用 GPU 绘制后，`CONFIG_LVGL_TASK_STACK_SIZE` 偏小。
- frame buffer 或图片资源内存申请失败后未处理错误。
- V8/V9 API 混用导致对象或事件回调行为异常。

<a id="id23"></a>

### 11.5 显示刷新性能不足

可按顺序排查：

- 优先使用 `RENDER_PARTIAL_MODE`。
- 如果使用 direct/full mode，`CONFIG_LVGL_FRAME_BUFFER_NUM` 配置为 2。
- 避免频繁整屏重绘，减少高频动画和大面积透明叠加。
- 需要性能监控时打开 `CONFIG_LV_USE_PERF_MONITOR`。
- V9 项目可评估 `CONFIG_LV_USE_DRAW_VG_LITE` 和 `output_compress`，但要同步确认 DPU 解压和内存对齐要求。
