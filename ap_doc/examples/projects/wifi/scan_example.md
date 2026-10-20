---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/wifi/scan_example/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="scan-example"></a>

# scan\_example

<a id="id1"></a>

## 1\. 概述

演示 `bk_wifi_scan_start` 与 `EVENT_WIFI_SCAN_DONE` 处理，打印扫描结果。

- 源码：`ap/ap_main.c`
- 开发者指南：Wi-Fi 扫描 \<../../../../developer-guide/wifi/bk\_wifi.html\>\_（「Armino Wi-Fi 扫描」章节）

<a id="id2"></a>

## 2\. 编译

```
make bk7259 PROJECT=wifi/scan_example
```

<a id="id3"></a>

## 3\. 运行

AP UART：

```
scan
```

CP UART：

```
ap_cmd scan
```

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
- [tflite micro](../tflite_micro.md)
- [Wi-Fi 项目示例](../wifi.md)
- [sta_example](sta_example.md)
- [softap_example](softap_example.md)
- [iperf](iperf.md)
- [p2p](p2p.md)
- [bridge](bridge.md)
- [rlk_demo](rlk_demo.md)
- [通用编译](../wifi.md)
- [相关文档](../wifi.md)
- [应用开发](../../../application.md)
- [开发与贡献代码流程](../../../process.md)
- [云平台](../../../cloud.md)
- [常见问题](../../../FAQ.md)
- [支持的外设](../../../support_peripherals.md)
