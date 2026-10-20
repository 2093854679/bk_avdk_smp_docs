---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/projects/mcu_lcd_example/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="mcu-lcd-display"></a>

# MCU LCD Display示例项目

<a id="id1"></a>

## 功能概述

- 实现display模块刷屏功能
- 支持输入数据源RGB565,RGB888和YUYV数据格式
- 有关display应用开发，请参阅：

  - [Display 开发指南](../../developer-guide/display/rgb_lcd_display.md)
- 有关lcd device添加请参阅：

  - [LCD设备添加指南](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/developer-guide/display/lcd_devices.html)
- 有关API参考，请参阅：

  - [Display API](../../api-reference/multimedia/bk_display.md)

<a id="id2"></a>

## 测试环境

> - 硬件配置：
>   :   - 核心板，**BK7258\_QFN88\_9X9\_V3.2**
>       - PSRAM 8M/16M
>       - lcd 转接小板
>       - RGB接口的LCD，demo中使用的为st7796s 320\*480的屏幕

警告

请使用参考外设，进行demo工程的熟悉和学习。如果外设规格不一样，代码可能需要重新配置。

<a id="id3"></a>

## 2\. 功能说明

- 提供命令行接口进行解码测试
- 提供了单独API接口场景和API组合功能测试

<a id="id4"></a>

## 3\. 编译与运行

<a id="id5"></a>

### 3.1 编译方法

使用以下命令编译项目：

```
make bk7258 PROJECT=rgb_lcd_example
```

<a id="id6"></a>

### 3.2 运行方法

编译完成后，将生成的固件烧录到开发板上，然后通过串口终端使用以下命令测试显示功能：

命令执行成功打印：”CMDRSP:OK”

命令执行失败打印：”CMDRSP:ERROR”

<a id="api"></a>

#### 3.2.1 API测试命令

1. 创建display实例:

```
lcd_display_api init
```

2. 初始化硬件display模块：

```
lcd_display_api open
```

3. 数据刷屏：

```
lcd_display_api flush
```

4. 关闭硬件display模块：

```
lcd_display_api close
```

5. 删除显示实例：

```
lcd_display_api delete
```

<a id="id7"></a>

#### 3.2.2 功能测试

1. 刷屏测试

```
lcd_display open
```

- CASE成功标准：

```
屏幕显示几张随机颜色后，稳定最后的颜色刷屏显示
```

- CASE成功日志：

```
ap0:media_se:D(104282):h264:0[0], dec:0[0], lcd:58[149], lcd_fps:3[8], lvgl:0[0]
ap0:media_se:D(104282):wifi:0[0, 0kbps, 0ms, 0-0], jpg:0KB[0Kbps], h264:0KB[0Kbps]

ap0:rgb_main:D(104805):bk_display_flush frame success!
CMDRSP:OK
```

- CASE失败标准：

```
屏幕没有显示刷屏
```

- CASE失败日志：

```
CMDRSP:ERROR
```

2. 关闭刷屏测试

```
lcd_display close
```

- CASE成功标准：

```
屏幕关闭显示
```

- CASE成功日志：

```
bk_display_delete success!
CMDRSP:OK
```

- CASE失败标准：

```
屏幕没有关闭显示
```

- CASE失败日志：

```
CMDRSP:ERROR
```

<a id="id8"></a>

## 注意事项

1. 屏幕不亮请注意检查背光IO是否打开
