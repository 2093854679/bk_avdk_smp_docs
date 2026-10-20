---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/sram_lite/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="sram-lite"></a>

# SRAM Lite 工程

<a id="id1"></a>

## 工程概述

`sram_lite` 是用于资源受限构建验证的轻量级 AP/CP 应用骨架。工程仅保留应用入口和组件注册文件，不包含工程专用分区表或 `defconfig`。

因此，本工程会继承所选 SoC 的默认配置。应用入口还包含可选的 SMP、IPC 和 BLE 配网测试初始化，仅在启用对应配置时参与编译。

<a id="id2"></a>

## 工程目录

- `ap/ap_main.c`：AP 初始化和可选测试代码
- `cp/cp_main.c`：CP 初始化和 AP 上电投票
- `ap/CMakeLists.txt`：AP 源文件和私有组件依赖
- `cp/CMakeLists.txt`：CP 源文件注册
- `CMakeLists.txt`：顶层工程定义

<a id="id3"></a>

## 编译

针对当前 SDK 版本，在 SDK 根目录执行：

```
make bk7259 PROJECT=sram_lite
```

<a id="id4"></a>

## 运行

烧录生成的 AP 和 CP 镜像，连接对应串口并复位开发板，确认两侧应用入口均能完成初始化。

由于本工程继承 SoC 默认配置，启用其他组件前请先检查最终生效的配置和内存布局。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [项目示例](../projects.md)
- [私有 2.4GHz（BK24G）收发示例工程](24g.md)
- [AP 仿真启动工程](ap_emuboot.md)
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
- [test](test.md)
- [tflite micro](tflite_micro.md)
- [Wi-Fi 项目示例](wifi.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
