---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/projects/spi_lcd_example/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="spi-lcd-display"></a>

# SPI LCD Display示例项目

<a id="id1"></a>

## 功能概述

- 实现display模块刷屏功能
- 支持输入数据源RGB565和RGB888数据格式

<a id="id2"></a>

## 主要组件

- `bk_display`: display组件
- `lcd_spi_gc9d01`: 屏幕组件

<a id="cli"></a>

## CLI命令使用

```
spi_lcd_display open   # 打开lcd显示
spi_lcd_display close  # 关闭lcd显示
```

参数说明：
\* `none`: 无参数

<a id="id3"></a>

## 日志输出

- 设备打开/关闭状态
- 错误信息

<a id="id4"></a>

## 测试示例

<a id="id5"></a>

### 测试环境

- 开发板：Armino开发板
- 外设：gc9d01 spi lcd

<a id="spi-lcd-example"></a>

### spi\_lcd\_example 固件编译

- 编译命令：

```
make bk7258 PROJECT=spi_lcd_example
```

<a id="case-1-lcd"></a>

### 测试CASE 1 \- LCD打开出图测试

- CASE命令:

```
lcd_display open
```

- CASE预期结果：

```
成功
```

- CASE成功标准：

```
屏幕显示红色纯色
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

<a id="case-2-lcd"></a>

### 测试CASE 2 \- LCD关闭测试

- CASE命令:

```
lcd_display close
```

- CASE预期结果：

```
屏幕关闭显示
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

<a id="id6"></a>

## 注意事项

<a id="id7"></a>

## 正常打印日志
