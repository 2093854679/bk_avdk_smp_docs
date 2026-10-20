---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/ap_emuboot/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap"></a>

# AP 仿真启动工程

<a id="id1"></a>

## 工程概述

`ap_emuboot` 是用于验证 AP 仿真启动配置的 BK7259 精简工程。工程关闭了大部分通信和外设功能，以较小配置验证启动流程。

启用 `CONFIG_AP_EMUBOOT` 后，CP 会在系统早期初始化阶段启动 AP，而不是在常规 CP 应用入口中启动。AP 与 CP 通过系统软件寄存器协调 Flash 初始化，随后 AP 入口执行工程特定的 Flash 时钟配置并调用 `bk_init()`。

<a id="id2"></a>

## 工程目录

- `ap/ap_main.c`：AP 早期时钟配置和应用入口
- `cp/cp_main.c`：精简 CP 应用入口；AP 已在更早的系统初始化阶段启动
- `ap/config/bk7259_ap/defconfig`：精简的 AP 仿真启动配置
- `cp/config/bk7259/defconfig`：精简的 CP 仿真启动配置
- `bk7259_ap_bsp.ld`：AP 链接布局
- `bk7259_bsp.ld`：CP 链接布局
- `partitions/bk7259/`：工程分区和 RAM 区域定义

<a id="id3"></a>

## 编译

在 SDK 根目录执行：

```
make bk7259 PROJECT=ap_emuboot
```

<a id="id4"></a>

## 运行

使用仿真启动测试环境烧录生成的镜像，连接 AP 和 CP 串口并复位目标板，确认两侧均能正常完成 `bk_init()`，且无启动异常。

本工程有意关闭了较多 SDK 默认功能。启用其他功能前，请先检查可用的 Flash 和 RAM 布局。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [项目示例](../projects.md)
- [私有 2.4GHz（BK24G）收发示例工程](24g.md)
- [AP Powerdown Keepalive 示例工程](ap_powerdown_keepalive.md)
- [默认应用工程](app.md)
- [A/B OTA 应用工程](app_ab.md)
- [bluetooth](bluetooth.md)
- [Flash / PSRAM 硬件验证工程](flash_psram_test.md)
- [KVS AWS Sample 示例工程](kvs_aws_sample.md)
- [lvgl](lvgl.md)
- [lwIP PSRAM 示例工程](lwip_psram_example.md)
- [multimedia](multimedia.md)
- [pm](pm.md)
- [安全启动 Overwrite OTA 工程](secureboot_overwrite.md)
- [安全启动 Overwrite OTA 工程（关闭 Flash AES）](secureboot_overwrite_no_en.md)
- [安全启动 XIP OTA 工程](secureboot_xip.md)
- [SRAM Lite 工程](sram_lite.md)
- [test](test.md)
- [tflite micro](tflite_micro.md)
- [Wi-Fi 项目示例](wifi.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
