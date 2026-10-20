---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/examples/cli/saradc/saradc.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="saradc-cli"></a>

# SARADC CLI

<a id="id1"></a>

## 1 功能概述

SDK 提供 SARADC CLI 命令，用于验证驱动初始化、通道配置、连续采样、
多通道采样和采样时钟等功能。

<a id="id2"></a>

## 2 代码路径

SARADC V1.2 CLI 测试代码路径：

`cp/middleware/driver/saradc/v1_2/adc_test.c`

<a id="id3"></a>

## 3 宏配置

启用以下配置：

> - `CONFIG_SARADC`
> - `CONFIG_DRIVER_TEST`
> - `CONFIG_SARADC_TEST`

<a id="cli"></a>

## 4 CLI 命令

主要命令如下：

| 命令 | 格式 | 功能 |
| --- | --- | --- |
| `sadc_driver` | `sadc_driver init|deinit` | 初始化或反初始化 SARADC 驱动 |
| `sadc` | `sadc <channel> <subcommand> [parameters]` | 配置通道、读取数据或查询校准电压 |
| `sadc_cont` | `sadc_cont start|read|stop [parameters]` | 验证连续采样 |
| `sadc_multi` | `sadc_multi config|read [channel]` | 验证多通道采样 |
| `sadc_rate` | `sadc_rate <channel> <clock>` | 验证指定采样时钟 |

例如，初始化驱动并读取 ADC3 的校准电压值：

```
sadc_driver init
sadc 3 config 3 1 13000000 3 0
sadc 3 get_value
```

备注

可用子命令受固件配置影响，请以当前固件的 `help` 输出为准。

## 模块导航

- [简介](../../../introduction.md)
- [H/W 参考手册](../../../hw-reference.md)
- [API 参考手册](../../../api-reference.md)
- [开发者指南](../../../developer-guide.md)
- [操作系统与内存管理](../../../os.md)
- [样例演示](../../../examples.md)
- [命令](../../cli.md)
- [触摸](../touch.md)
- [外设](../../peripheral.md)
- [平台](../../platform.md)
- [VND_CAL](../../vnd_cal/vnd_cal.md)
- [应用开发](../../../application.md)
- [开发与贡献代码流程](../../../process.md)
- [云平台](../../../cloud.md)
