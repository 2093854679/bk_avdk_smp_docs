---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/test/cpu_perf_test/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cpu-sram"></a>

# CPU 与 SRAM 性能测试工程

<a id="id1"></a>

## 工程概述

`test/cpu_perf_test` 是 BK7259 工程测试项目，使用处理器周期计数器测量 SRAM 和 PSRAM 的读写耗时。

`CONFIG_CPU_PERF_TEST` 选项会注册 `cpu_perf_test` CLI 命令。该命令测试由 `partitions/bk7259/ram_regions.csv` 生成的区域，并可在启用 SMP 时选择 AP 执行核。

<a id="id2"></a>

## 工程目录

- `ap/ap_main.c`：AP 应用入口
- `cp/cp_main.c`：CP 初始化和 AP 启动逻辑
- SDK `ap/components/bk_cli/cli_cpu_perf.c`：公共 CPU 性能测试 CLI 实现
- `ap/config/bk7259_ap/defconfig`：AP 性能测试配置
- `cp/config/bk7259/defconfig`：CP SMP 性能测试配置
- `bk7259_ap_bsp.ld`：AP 测试链接布局
- `partitions/bk7259/ram_regions.csv`：SRAM 和 PSRAM 测试区域定义

<a id="id3"></a>

## 编译

在 SDK 根目录执行：

```
make bk7259 PROJECT=test/cpu_perf_test
```

<a id="id4"></a>

## 运行

烧录 AP 和 CP 镜像，连接串口并复位开发板。在 AP CLI 中执行以下命令，可在当前核上测试全部配置区域：

```
cpu_perf_test
```

启用 SMP 时，可指定 AP 核索引 `0` 或 `1`，并可继续指定一个或多个区域 ID：

```
cpu_perf_test 0
cpu_perf_test 1 0 3
```

区域 ID 按 SDK `ap/components/bk_cli/cli_cpu_perf.c` 中的编译顺序排列：`SRAM2_TEST`、`SRAM5_TEST`、`SRAM6_TEST`、`PSRAM0_TEST` 和 `PSRAM1_TEST`。输出会显示读写周期数和参与测试的字数。

<a id="id5"></a>

## 测试注意事项

该命令会向每个选中区域的前 32 KiB 范围内写入测试数据，并在测量期间临时关闭本地中断。请仅使用工程自带的内存布局运行，且不要同时运行无关应用负载。

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
- [平台测试工程](platform.md)
- [RAM 测试工程](ram_test.md)
- [tflite micro](../tflite_micro.md)
- [Wi-Fi 项目示例](../wifi.md)
- [应用开发](../../../application.md)
- [开发与贡献代码流程](../../../process.md)
- [云平台](../../../cloud.md)
- [常见问题](../../../FAQ.md)
- [支持的外设](../../../support_peripherals.md)
