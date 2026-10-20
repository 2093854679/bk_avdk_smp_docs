---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/cli/touch/touch.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="touch-cli"></a>

# TOUCH Cli

<a id="id1"></a>

## 1、功能概述

> 为了便于验证TOUCH的功能，为此设计了一系列cli CMD，主要包括单通道工作模式和多通道扫描的工作模式，当前cli命令是否生效由宏 `CLI_CFG_TOUCH` 决定，宏控制位置在：`components\bk_cli\cli_config.h` 文件中，该宏是否生效由内部宏 `CONFIG_TOUCH_TEST` 决定。

<a id="id2"></a>

## 2、代码路径

> 路径：`components\demos\peripheral\touch\touch_demo.c`

<a id="cli"></a>

## 3、cli命令简介

支持的命令如下:

> 1.touch\_single\_channel\_calib\_mode\_test
> :   - 功能说明
>       :   用来测试touch单通道的功能。
>     - 命令格式
>       :   touch\_single\_channel\_calib\_mode\_test param1 param2
>
>           | Param | value |
>           | --- | --- |
>           | param1 | touch channel id  选择：0 \- 15 |
>           | param2 | Sensitivity level selection  选择: 0 / 1 / 2 / 3 |
>     - 测试用例
>       :   测试touch通道2：`touch_single_channel_calib_mode_test 2 1`
>
> 2.touch\_multi\_channel\_scan\_mode\_test
> :   - 功能说明
>       :   用来测试touch多个通道扫描工作的功能。
>     - 命令格式
>       :   touch\_multi\_channel\_scan\_mode\_test param1 param2
>
>           | Param | value |
>           | --- | --- |
>           | param1 | start / stop  start：开始  stop ：停止 |
>           | param2 | Sensitivity level selection  选择: 0 / 1 / 2 / 3 |
>     - 测试用例
>       :   测试所有通道：`touch_multi_channel_scan_mode_test start 1`
