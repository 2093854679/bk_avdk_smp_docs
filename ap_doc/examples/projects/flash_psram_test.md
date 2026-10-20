---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/flash_psram_test/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="flash-psram"></a>

# Flash / PSRAM 硬件验证工程

<a id="id1"></a>

## 工程概述

`flash_psram_test` 基于 `test/ram_test`，用于 **新 Flash / 新 PSRAM 导入时的硬件验证** 。

工程默认：

- Flash： **16M** （`CONFIG_FLASH_CAPACITY_16M=y`，`auto_partitions_16M.csv`，RF/NET 在 `0xFFE000`/`0xFFF000` ）
- PSRAM： **32M / 颗** （`CONFIG_PSRAM_CAPACITY_32M=y`，`ram_regions_32M.csv`，高 16MB 为 `PSRAM0_TEST_HIGH` / `PSRAM1_TEST_HIGH` ）

产物目录：`build/bk7259/flash_psram_test_16M_psram32M/`。

AP 使用单核 FreeRTOS 跑 RAM 测试，CP 负责系统初始化并启动 AP。CP 打开 `CONFIG_FLASH_TEST`。

<a id="id2"></a>

## 编译

```
make bk7259 PROJECT=flash_psram_test
```

<a id="id3"></a>

## 运行

```
flash_test ID
psram_test start
psram_test stop
sram_test_all
sram_bus_bench all 32768 10
```

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
