---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/test/platform/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 平台测试工程

<a id="id2"></a>

## 工程概述

`test/platform` 是 BK7259 平台驱动集成和回归测试工程。工程配置启用了常用外设和安全功能的 SDK CLI 测试。

当前配置覆盖：

- CP 侧看门狗和 ADC 测试
- AP 侧 PWM、UART、I2C、SPI、Flash、GPIO、ADC 和密码算法测试
- 通过 CP 串口转发到 AP 的测试命令

<a id="id3"></a>

## 工程目录

- `ap/ap_main.c`：AP 初始化和可选 IPC 测试初始化
- `cp/cp_main.c`：CP 初始化和 AP 启动逻辑
- `ap/config/bk7259_ap/defconfig`：已启用的 AP 驱动测试功能
- `cp/config/bk7259/defconfig`：已启用的 CP 驱动测试功能
- `.it.csv`：集成测试命令和预期输出
- `partitions/bk7259/`：测试分区和 RAM 区域定义

<a id="id4"></a>

## 编译

在 SDK 根目录执行：

```
make bk7259 PROJECT=test/platform
```

<a id="id5"></a>

## 运行

烧录生成的 AP 和 CP 镜像，连接测试所需的外设线路和串口，然后复位开发板。从 `.it.csv` 中选择适用命令执行，并将串口输出与预期结果进行比较。

示例命令：

```
wdt_driver init
ap_cmd pwm_driver init
ap_cmd uart_driver init
ap_cmd mbedtls_selftest
```

<a id="id6"></a>

## 测试注意事项

部分用例需要外部接线或两块开发板。Flash 测试会擦写命令指定的地址，看门狗重启测试会主动复位设备。在保存有重要数据的开发板上运行前，请先检查对应的 `.it.csv` 用例。

## 模块导航

- [简介](../../../introduction.md)
- [H/W 参考手册](../../../hw-reference.md)
- [API 参考手册](../../../api-reference.md)
- [开发者指南](../../../developer-guide.md)
- [操作系统与内存管理](../../../os.md)
- [样例演示](../../../examples.md)
- [项目示例](../../projects.md)
- [私有 2.4GHz（BK24G）收发示例工程](../24g.md)
- [AP 仿真启动工程](../ap_emuboot.md)
- [AP Powerdown Keepalive 示例工程](../ap_powerdown_keepalive.md)
- [默认应用工程](../app.md)
- [A/B OTA 应用工程](../app_ab.md)
- [bluetooth](../bluetooth.md)
- [Flash / PSRAM 硬件验证工程](../flash_psram_test.md)
- [KVS AWS Sample 示例工程](../kvs_aws_sample.md)
- [lvgl](../lvgl.md)
- [lwIP PSRAM 示例工程](../lwip_psram_example.md)
- [multimedia](../multimedia.md)
- [pm](../pm.md)
- [安全启动 Overwrite OTA 工程](../secureboot_overwrite.md)
- [安全启动 Overwrite OTA 工程（关闭 Flash AES）](../secureboot_overwrite_no_en.md)
- [安全启动 XIP OTA 工程](../secureboot_xip.md)
- [SRAM Lite 工程](../sram_lite.md)
- [test](../test.md)
- [CPU 与 SRAM 性能测试工程](cpu_perf_test.md)
- [RAM 测试工程](ram_test.md)
- [tflite micro](../tflite_micro.md)
- [Wi-Fi 项目示例](../wifi.md)
- [应用开发](../../../application.md)
- [开发与贡献代码流程](../../../process.md)
- [云平台](../../../cloud.md)
- [常见问题](../../../FAQ.md)
- [支持的外设](../../../support_peripherals.md)
