---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/app_ab/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="a-b-ota"></a>

# A/B OTA 应用工程

<a id="id1"></a>

## 工程概述

`app_ab` 是 BK7259 位置无关 A/B OTA 升级参考工程。应用启动过程沿用标准 AP/CP 流程，工程配置和分区文件用于启用 A/B 镜像打包与升级。

主要特性：

- A/B OTA 和 HTTP OTA 支持
- 位置无关应用镜像
- OTA 镜像 Hash 校验
- 备用应用区 `s_app` 和 OTA 完成状态数据

<a id="id2"></a>

## 工程目录

- `ap/ap_main.c`：AP 应用入口
- `cp/cp_main.c`：CP 应用入口和 AP 启动逻辑
- `ap/config/bk7259_ap/defconfig`：包含 A/B OTA 选项的 AP 配置
- `cp/config/bk7259/defconfig`：CP 配置
- `partitions/bk7259/auto_partitions.csv`：A/B Flash 分区表
- `partitions/bk7259/ab_position_independent.csv`：位置无关镜像配置
- `partitions/bk7259/ota_rbl.config`：OTA 包配置

<a id="id3"></a>

## 编译

在 SDK 根目录执行：

```
make bk7259 PROJECT=app_ab
```

<a id="id4"></a>

## 运行与验证

1. 编译工程并烧录生成的初始镜像。
2. 按 SDK 打包流程使用生成的 A/B OTA 产物制作升级包。
3. 通过已启用的 OTA 接口启动升级。
4. 复位开发板，确认系统启动到更新后的镜像。

分区表和 OTA 包配置共同构成升级约束。修改镜像大小或启用更多功能前，应先检查这些文件。

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
