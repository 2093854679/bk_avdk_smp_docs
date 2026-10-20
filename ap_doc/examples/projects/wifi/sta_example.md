---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/wifi/sta_example/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="sta-example"></a>

# sta\_example

<a id="id1"></a>

## 1\. 概述

演示 AP 核 STA 模式连接：注册 Wi-Fi / Netif 事件，配置 SSID 密码后调用 `bk_wifi_sta_start`，在 `EVENT_NETIF_GOT_IP4` 后可进行 socket 通信。

- 源码：`ap/ap_main.c`
- 开发者指南：Wi-Fi 快速入门 \<../../../../developer-guide/wifi/bk\_wifi\_get\_started.html\>\_、[Wi-Fi 模式与 CLI](../../../developer-guide/wifi/bk_wifi_mode.md)

<a id="id2"></a>

## 2\. 编译与烧录

```
make bk7259 PROJECT=wifi/sta_example
```

烧录 AP \+ CP 完整镜像。

<a id="id3"></a>

## 3\. 运行

修改 `ap/ap_main.c` 中 `WIFI_STA_EXAMPLE_SSID` / `WIFI_STA_EXAMPLE_PASSWORD`，或在 AP UART 使用 CLI：

```
sta your_ssid your_password
```

CP UART 转发 AP CLI：

```
ap_cmd sta your_ssid your_password
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
- [scan_example](scan_example.md)
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
