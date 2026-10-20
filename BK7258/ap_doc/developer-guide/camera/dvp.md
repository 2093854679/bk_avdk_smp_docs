---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/camera/dvp.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="dvp"></a>

# DVP

<a id="id1"></a>

## 1\. 概述

> 本节主要说明DVP的使用和适配方法，以及相关的宏定义。

- 有关DVP CAMERA的示例工程，请参阅：

  - [DVP CAMERA示例工程](../../examples/projects/dvp_example.md)
- 有关DVP CAMERA的API参考，请参阅：

  - [DVP CAMERA API](../../api-reference/multimedia/bk_camera.md)
- 有关图像内存申请释放的相关API，请参阅：

  - [图像内存管理](../../api-reference/multimedia/bk_frame_buffer.md)

<a id="id3"></a>

## 2\. 支持的功能

> 1、支持最大分辨率1280X720输入（输出）；
>
> 2、只支持Sensor输出标准YUV422数据格式(大端模式)：YUYV/UYVY/YYUV/UVYY；
>
> 3、默认VSYNC/HSYNC输入高有效，且支持翻转
>
> 4、支持直接输出YUV422数据到BUFF；
>
> 5、支持直接输出JPEG编码数据，或YUV422\&JPEG数据分别到BUFF；
>
> 6、支持直接输出H264编码数据，或YUV422\&H264数据分别到BUFF；
>
> 7、支持动态调节编码码率（JPEG或H264）;
>
> 8、支持H264编码任意时刻重新生成IDR帧
>
> 9、支持Sensor数据接收错误检测
>
> 用户需要根据自己的应用方案，通过配置参数的方式，打开对应的功能

<a id="id4"></a>

## 3\. 相关宏定义

> | Marco name | info |
> | --- | --- |
> | CONFIG\_DVP\_CAMERA | enable dvp sensor function or not |
> | CONFIG\_DVP\_CAMERA\_I2C\_ID | config dvp sensor communicate i2c id |
> | CONFIG\_DVP\_CTRL\_POWER\_GPIO\_ID | config the gpio id of control dvp vdd |
> | CONFIG\_JPEG\_FRAME\_SIZE | config a jpeg frame size |
> | CONFIG\_H264\_FRAME\_SIZE | config a h264 frame size |
> | CONFIG\_DVP\_GC0308 | enable gc0308 sensor function or not |
> | CONFIG\_DVP\_HM1055 | enable hm1055 sensor function or not |
> | CONFIG\_DVP\_OV2640 | enable ov2640 sensor function or not |
> | CONFIG\_DVP\_SC101 | enable sc101 sensor function or not |
> | CONFIG\_DVP\_GC0328C | enable gc0328c sensor function or not |
> | CONFIG\_DVP\_GC2145 | enable gc2145 sensor function or not |

备注

上面的sensor宏是已经适配好了，用户可以直接使用。都默认开启的，其他宏需要用户在编译时自己开启。但是会依赖CONFIG\_DVP\_CAMERA宏，所以需要用户在编译时自己开启。

<a id="id5"></a>

## 4\. 适配新摄像头

> 1.适配新的sensor用户需要在自己的工程下添加sensor的配置文件，具体可以参考 `./ap/components/bk_peripheral/src/dvp/dvp_gc2145.c` 的实现方式。实现如下结构体的内容。需要根据sensor的实际情况，填充结构体中的内容。
>
> 2.sensor输出指定分辨率和帧率的方式是通过设置sensor的寄存器实现的，方案中是配置三个表实现，分别是：
> \- 初始化表：用于初始化sensor的寄存器。
> \- 帧率表：用于设置sensor的帧率。
> \- 分辨率表：用于设置sensor的分辨率。
>
> 相关表内容的配置需要sensor厂商给出
>
> 3.按照上面的说明配置好相关参数后，需要将sensor的检测函数注册到系统中，具体可以参考 `./projects/dvp_example/ap/dvp_test/src/dvp_gc0001_test.c` 的实现方式。注册如下结构体的内容。
>
> ```
> const dvp_sensor_config_t *gc0001_detect_sensor(void)
> {
>     LOGI("%s\n", __func__);
>     if (gc0001_detect())
>     {
>         return &dvp_sensor_gc0001;
>     }
>
>     return NULL;
> }
>
> BK_CAMERA_SENSOR_DETECT_SECTION(gc0001_detect_sensor);
> ```
>
> 4.在完成上述步骤后，需要将添加的sensor配置文件添加到编译系统中，参考 `./projects/dvp_example/ap/CMakeLists.txt` 的实现方式。
>
> ```
> set(GLOBAL_FUNCTION_SYMBOLS "")
>
> list(APPEND srcs
>     # other srcs
>     dvp_test/src/dvp_gc0001_test.c
> )
>
> list(APPEND GLOBAL_FUNCTION_SYMBOLS "gc0001_detect_sensor")
>
> foreach(symbol ${GLOBAL_FUNCTION_SYMBOLS})
>     target_link_libraries(${COMPONENT_LIB} INTERFACE "-u ${symbol}")
> endforeach()
> ```
>
> 5.在完成上述步骤后，编译完成后会将添加的sensor检测方式注册到段中。用户在启动时会自动检测sensor，如果检测到sensor，会调用sensor的检测函数。
>
> 6.sensor的检测方法段默认会在ld文件中注册，但是有些工程可能有自己的ld文件，不采用SDK默认的ld文件，那么就需要在ld文件中添加如下内容：
>
> ```
> .sensor_detect :
> {
> __camera_sensor_detect_array_start = .;
> KEEP(*(.camera_sensor_detect_function_list.*))
> __camera_sensor_detect_array_end = .;
> } > FLASH
> ```
>
> 7.Sensor的配置结构体如下：\`\`
>
> ```
> /**
> * @brief DVP传感器配置结构体
> * @details DVP传感器的配置参数和函数指针
> */
> typedef struct
> {
>     char *name;                     /**< 传感器名称 */
>     media_ppi_t def_ppi;            /**< 传感器默认分辨率 */
>     frame_fps_t def_fps;            /**< 传感器默认帧率 */
>     mclk_freq_t  clk;               /**< 配置帧率和分辨率时的传感器工作时钟 */
>     pixel_format_t fmt;             /**< 传感器输入数据格式 */
>     sync_level_t vsync;             /**< 传感器垂直同步信号有效电平 */
>     sync_level_t hsync;             /**< 传感器水平同步信号有效电平 */
>     uint16_t id;                    /**< 传感器类型 (sensor_id_t) */
>     uint16_t address;               /**< 传感器通过I2C写入寄存器的地址 */
>     uint16_t fps_cap;               /**< 传感器支持的帧率 */
>     uint16_t ppi_cap;               /**< 传感器支持的分辨率 */
>
>     /**
>     * @brief 自动检测使用的DVP传感器
>     * @return 检测到传感器返回true，否则返回false
>     */
>     bool (*detect)(void);
>
>     /**
>     * @brief 初始化DVP传感器
>     * @return 成功返回0，失败返回错误码
>     */
>     int (*init)(void);
>
>     /**
>     * @brief 设置传感器的分辨率
>     * @param ppi 要设置的分辨率
>     * @return 成功返回0，失败返回错误码
>     */
>     int (*set_ppi)(media_ppi_t ppi);
>
>     /**
>     * @brief 设置传感器的帧率
>     * @param fps 要设置的帧率
>     * @return 成功返回0，失败返回错误码
>     */
>     int (*set_fps)(frame_fps_t fps);
>
>     /**
>     * @brief 传感器断电或重置
>     * @return 成功返回0，失败返回错误码
>     */
>     int (*power_down)(void);
>
>     /**
>     * @brief 读取传感器寄存器
>     * @param reg 寄存器地址
>     * @param val 存储寄存器值的指针
>     * @return 成功返回0，失败返回错误码
>     */
>     int (*read_register)(uint32_t reg, uint32_t *val);
>
>     /**
>     * @brief 写入传感器寄存器
>     * @param reg 寄存器地址
>     * @param val 要写入的寄存器值
>     * @return 成功返回0，失败返回错误码
>     */
>     int (*write_register)(uint32_t reg, uint32_t val);
> } dvp_sensor_config_t;
> ```
>
> 一些参数的说明：
> \* clk: 摄像头输入时钟，默认是24MHz，需要根据摄像头规格配置；
> \* fmt: 摄像头输出数据格式，目前只支持YUV420，需要与摄像头输出顺序同步，默认是YUYV；
> \* vsync: 摄像头输出vsync有效电平，有些摄像头在vsync低电平时输出有效数据，需要与摄像头vsync输出电平同步，默认是高电平有效；
> \* hsync: 摄像头输出hsync有效电平，有些摄像头在hsync低电平时输出有效数据，需要与摄像头hsync输出电平同步，默认是高电平有效；
> \* address: 摄像头寄存器地址，需要根据摄像头规格配置；
> \* fps\_cap: 摄像头支持的帧率表，需要配置对应的寄存器实现；
> \* ppi\_cap: 摄像头支持的分辨率表，需要配置对应的寄存器实现；
> \* id: 摄像头类型，需要根据摄像头规格配置；
> \* address: 摄像头寄存器地址，需要根据摄像头规格配置；
> \* fps\_cap: 摄像头支持的帧率表，需要配置对应的寄存器实现；
> \* ppi\_cap: 摄像头支持的分辨率表，需要配置对应的寄存器实现；

<a id="id6"></a>

## 5\. DVP摄像头的使用流程

<a id="id7"></a>

### 5.1 DVP上电

> 在对dvp sensor使用之前需要对DVP进行上电操作，对于BK7258平台，需要配置 `CONFIG_DVP_CTRL_POWER_GPIO_ID` 为DVP的VDD引脚，
> 默认控制引脚为GPIO\_28，将该引脚配置为输出模式，并且将其电平设置为高电平。

```
/**
* @brief DVP摄像头上电
*/
{
    #define GPIO_INVALID_ID           (0xFF)
    #ifdef CONFIG_DVP_CTRL_POWER_GPIO_ID
    #define DVP_POWER_GPIO_ID CONFIG_DVP_CTRL_POWER_GPIO_ID
    #else
    #define DVP_POWER_GPIO_ID GPIO_INVALID_ID
    #endif

    if (DVP_POWER_GPIO_ID != GPIO_INVALID_ID)
    {
        GPIO_UP(DVP_POWER_GPIO_ID);
    }
}
```

<a id="id8"></a>

### 5.2 创建DVP摄像头控制器

> 调用如下接口创建DVP摄像头控制器：

```
avdk_err_t bk_camera_dvp_ctlr_new(bk_camera_ctlr_handle_t *handle, bk_dvp_ctlr_config_t *config);
```

描述：
:   创建DVP摄像头控制器，返回控制器句柄。

    传入的配置包含两个部分：

    第一部分：bk\_dvp\_config\_t，包含DVP摄像头IO映射，I2C的配置，需要输出的分辨率帧率配置，需要输出的图像格式配置等。

    第二部分：bk\_dvp\_callback\_t，通过此回调函数申请存放目标数据的空间，以及返回图像数据给用户，用户自行管理目标数据。

备注

1.在DVP的回调函数中不能有任何的阻塞操作，也不能执行长时间的操作，否则会导致硬件中断被延时，进而导致图像异常。在下面的创建DVP摄像头控制器中会给出具体的示例，实例中回调函数只进行了简单的帧缓冲区申请释放操作，用户可以参考实现。
2.如果工作在编码模式下，会默认根据分辨率大下申请内存给硬件模块使用，在open的时候配置下去，在delete的时候释放掉。如果需要不重复申请释放这块内存，建议不做delete控制器的操作。

参数：
:   handle：DVP摄像头控制器句柄。

    config：DVP摄像头控制器配置参数。

    相关数据结构：`bk_dvp_ctlr_config_t`, `bk_dvp_config_t`, `bk_dvp_callback_t`。

    参考路径：`ap/include/components/dvp_camera_types.h`。

    bk\_dvp\_config\_t支持如下默认配置：

```
/**
 * @brief DVP摄像头640x480分辨率30 FPS MJPEG格式配置
 * @details 常用DVP摄像头设置的预定义配置宏
 */

/* 宏定义中各参数说明：
 * i2c_config.id - I2C控制器ID
 * i2c_config.scl_pin - I2C时钟引脚
 * i2c_config.sda_pin - I2C数据引脚
 * i2c_config.baud_rate - I2C波特率(100kHz)
 * i2c_config.flags - I2C标志位(无特殊配置)
 * reset_pin - 复位引脚(0xFF表示未使用)
 * pwdn_pin - 电源关闭引脚(0xFF表示未使用)
 * io_config.data_width - 数据位宽度(8位)
 * io_config.data_pin - 数据引脚数组
 * io_config.vsync_pin - 垂直同步引脚
 * io_config.hsync_pin - 水平同步引脚
 * io_config.xclk_pin - 外部时钟引脚
 * io_config.pclk_pin - 像素时钟引脚
 * clk_source - 时钟源(24MHz)
 * width - 图像宽度(像素)
 * height - 图像高度(像素)
 * fps - 帧率(帧/秒)
 * img_format - 图像格式(MJPEG)
 * user_data - 用户数据指针(无)
 */
#define BK_DVP_864X480_30FPS_MJPEG_CONFIG()\
{\
    .i2c_config = {\
        .id = 1,\
        .scl_pin = 0,\
        .sda_pin = 1,\
        .baud_rate = 100000,\
        .flags = 0,\
    },\
    .reset_pin = 0xFF,\
    .pwdn_pin = 0xFF,\
    .io_config = {\
        .data_width = SENSOR_BITS_WIDTH_8BIT,\
        .data_pin = {32, 33, 34, 35, 36, 37, 38, 39},\
        .vsync_pin = 31,\
        .hsync_pin = 30,\
        .xclk_pin = 27,\
        .pclk_pin = 29,\
    },\
    .clk_source = MCLK_24M,\
    .width = 640,\
    .height = 480,\
    .fps = 30,\
    .img_format = IMAGE_MJPEG,\
    .user_data = NULL,\
}

// 建议用户针对申请的帧，根据图像格式选择自己维护的链表中空闲的节点，与下面complete的操作维护两个链表，一个是free链表，一个是ready链表。
// 每次申请时从free链表中取出一个节点，申请完成后将节点加入到ready链表中，需要使用时从ready链表中取出，使用后直接释放到free链表中。
// 具体可以参考： ``./projects/dvp_example/dvp_test/src/dvp_frame_list.c``
/**
 * @brief 根据图像格式分配不同类型的帧缓冲区并初始化帧结构成员
 *
 * @param format 图像格式(YUV或其他格式如MJPEG/H264等)
 * @param size 要分配的缓冲区大小(字节)
 * @return 成功返回帧缓冲区指针，失败返回NULL
 */
static frame_buffer_t *dvp_frame_malloc(image_format_t format, uint32_t size)
{
    // 从DVP帧队列中申请帧缓冲区
    frame_buffer_t *frame = dvp_frame_queue_malloc(format, size);

    if (frame)
    {
        frame->sequence = 0;
        frame->length = 0;
        frame->timestamp = 0;
        frame->size = size;
    }

    return frame;
}


/**
 * @brief 通知DVP摄像头数据处理完成，释放帧缓冲区
 *
 * @param format 图像格式(YUV或其他格式如MJPEG/H264等)
 * @param frame 指向帧缓冲区的指针，包含要释放的帧数据
 * @param result 处理结果，0表示成功，非0表示失败，成功时可以存入用户自己维护的链表，失败时建议直接释放
 */
static void dvp_frame_complete(image_format_t format, frame_buffer_t *frame, int result)
{
    if (frame->sequence % 30 == 0)
    {
        LOGD("%s: seq:%d, length:%d, format:%s, h264_type:%x, result:%d\n", __func__, frame->sequence,
            frame->length, (format == IMAGE_MJPEG) ? "mjpeg" : (format == IMAGE_H264) ? "h264" : "YUV", frame->h264_type, result);
    }

    if (result != AVDK_ERR_OK)
    {
        // 图像有问题，直接释放帧缓冲区，加入到free链表中
        dvp_frame_queue_free(format, frame);
    }
    else
    {
        // 图像正常，加入到ready链表中，等待用户使用
        dvp_frame_queue_complete(format, frame);
    }
}

static const bk_dvp_callback_t dvp_cbs = {
    .malloc = dvp_frame_malloc,
    .complete = dvp_frame_complete,
};

// create dvp controller
{
    bk_dvp_ctlr_config_t dvp_ctrl_config = {
        .config = BK_DVP_864X480_30FPS_MJPEG_CONFIG(),
        .cbs = &dvp_cbs,
    };

    // you can change the config here
    //dvp_ctrl_config.config.img_format = output_format;
    //dvp_ctrl_config.config.width = ppi >> 16;
    //dvp_ctrl_config.config.height = ppi & 0xFFFF;
    // new
    ret = bk_camera_dvp_ctlr_new(&s_dvp_handle, &dvp_ctrl_config);
}
```

<a id="id9"></a>

### 5.3 打开DVP摄像头

> 调用如下接口打开DVP摄像头：

```
avdk_err_t bk_camera_open(bk_camera_ctlr_handle_t handle);
```

描述：
:   打开DVP摄像头控制器，返回错误码。

    打开DVP摄像头后，上面注册的回调函数会不停的申请数据空间用以存储。

    打开DVP摄像头后，会开始采集数据，且会调用上面注册的回调函数，将采集到的数据返回给用户，用户需要关注frame是否有效，选择使用还是释放。

参数：
:   handle：DVP摄像头控制器句柄。

<a id="dvp-ioctl"></a>

### 5.4 DVP Ioctl

> 调用如下接口进行DVP的IOCTL操作：

```
avdk_err_t bk_camera_ioctl(bk_camera_ctlr_handle_t handle, uint32_t cmd, void *arg)
```

描述：
:   DVP的IOCTL操作，支持的命令如下：
    \- DVP\_IOCTL\_CMD\_H264\_IDR\_RESET：重新生产IDR帧，必须确保DVP的工作模式是H264\_MODE或H264\_YUV\_MODE模式，才能生效。
    \- DVP\_IOCTL\_CMD\_SENSOR\_WRITE\_REGISTER：写入传感器寄存器。
    \- DVP\_IOCTL\_CMD\_SENSOR\_READ\_REGISTER：读取传感器寄存器。

参数：
:   handle：DVP摄像头控制器句柄。

    cmd：命令码，支持的命令如上所示。

    arg：参数，用户传入参数，根据命令不同，参数不同。

<a id="id10"></a>

### 5.5 关闭DVP摄像头

> 调用如下接口关闭DVP摄像头：

```
avdk_err_t bk_camera_close(bk_camera_ctlr_handle_t handle);
```

描述：
:   关闭DVP摄像头控制器。

    关闭DVP摄像头后，上面注册的回调函数会停止申请数据空间，也会停止采集数据。

参数：
:   handle：DVP摄像头控制器句柄。

<a id="id11"></a>

### 5.6 注销DVP摄像头控制器

> 调用如下接口注销DVP摄像头控制器：

```
avdk_err_t bk_camera_delete(bk_camera_ctlr_handle_t handle);
```

描述：
:   注销DVP摄像头控制器。

    释放控制器申请的内存空间，只有当dvp成功关闭时才允许被调用。

参数：
:   handle：DVP摄像头控制器句柄。

<a id="dvp-power-off"></a>

### 5.7 DVP Power Off

> 将控制DVP LDO的GPIO拉低即可关闭DVP摄像头电源。

```
{
    // power off dvp camera
    if (DVP_POWER_GPIO_ID != GPIO_INVALID_ID)
    {
        GPIO_DOWN(DVP_POWER_GPIO_ID);
    }
}
```

<a id="id12"></a>

## 6\. DVP支持方案

因为DVP支持输出各种格式的数据，所以需要用户根据自己的需求，选择合适的输出格式。

1.DVP直接输出YUV图像，联合显示模块进行显示。
2.DVP直接输出MJPEG图像，再联合WiFi模块进行图传。
3.DVP直接输出H264图像，再联合WiFi模块进行图传。
4.DVP直接输出MJPEG\&YUV图像，再联合WiFi模块进行图传，联合显示模块进行显示。
5.DVP直接输出H264\&YUV图像，再联合WiFi模块进行图传，联合显示模块进行显示。
