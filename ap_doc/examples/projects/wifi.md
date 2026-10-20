---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/wifi/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wi-fi"></a>

# Wi-Fi 项目示例

BK7259 SMP SDK 在 `projects/wifi/` 下提供 Wi-Fi 参考工程，应用逻辑均在 **AP 核** 编写；CP 核为 Wi-Fi 控制器。

- [sta\_example](wifi/sta_example.md)
- [scan\_example](wifi/scan_example.md)
- [softap\_example](wifi/softap_example.md)
- [iperf](wifi/iperf.md)
- [p2p](wifi/p2p.md)
- [bridge](wifi/bridge.md)
- [rlk\_demo](wifi/rlk_demo.md)

<a id="id1"></a>

## 通用编译

在 SDK 根目录:

```
make bk7259 PROJECT=wifi/<工程名>
```

固件输出：`build/bk7259/wifi/<工程名>/`

<a id="id2"></a>

## 相关文档

- [Wi-Fi 快速入门](../../developer-guide/wifi/bk_wifi_get_started.md)
- [Wi-Fi 开发者指南](../../developer-guide/wifi.md)
- [Wi-Fi API](../../api-reference/wifi/bk_wifi.md)

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
- [SRAM Lite 工程](sram_lite.md)
- [test](test.md)
- [tflite micro](tflite_micro.md)
- [sta_example](wifi/sta_example.md)
- [scan_example](wifi/scan_example.md)
- [softap_example](wifi/softap_example.md)
- [iperf](wifi/iperf.md)
- [p2p](wifi/p2p.md)
- [bridge](wifi/bridge.md)
- [rlk_demo](wifi/rlk_demo.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
