---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/bootloader_ota/ble_ota/bk_ble_ota_overview.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ble-ota"></a>

# BLE\_OTA概述

<a id="id1"></a>

## 一.BLE\_OTA概述

BLE\_OTA是一种蓝牙低功耗设备的无线升级技术。它允许设备在不需要物理连接的情况下升级固件，提高了设备的可维护性和可升级性，通常用于蓝牙低功耗设备，如可穿戴设备、智能家居设备等

<a id="id2"></a>

## 1.1.BLE\_OTA升级步骤

- 1.设备发现：设备端开启BLE广播，并提供其 OTA 升级服务的信息；
- 2.连接建立：OTA 升级服务端（通常是移动设备或计算机）连接到 BLE 设备；
- 3.升级包传输：OTA 升级服务端将新的固件传输到 BLE 设备；
- 4.升级执行：BLE 设备接收并执行升级包，更新其固件。

<a id="id3"></a>

## 1.2.BLE\_OTA升级的优、缺点

- 1.无需物理连接，方便升级；
- 2.降低维护成本；
- 3.提高设备的可升级性和可维护性；
- 4.下载速度较慢。

<a id="id4"></a>

## 1.3.术语与缩写解释

- APP：应用程序(Application)；
- BLE：蓝牙低功耗（Bluetooth Low Energy）；
- OTA：空中升级（Over-The-Air）；
- APK：安卓应用包Android Package Kit）；
- CRC：循环冗余校验（Cyclic Redundancy Check）

## 模块导航

- [简介](../../../introduction.md)
- [H/W 参考手册](../../../hw-reference.md)
- [API 参考手册](../../../api-reference.md)
- [开发者指南](../../../developer-guide.md)
- [软件架构与分层](../../architecture.md)
- [系统安全](../../security.md)
- [低功耗与电源管理](../../power_save.md)
- [设备管理框架](../../driver_model.md)
- [外设与驱动](../../peripheral.md)
- [出错与日志](../../error_log.md)
- [系统调试](../../debug_trace.md)
- [CPU Hotplug](../../cpu_hotplug.md)
- [Wi-Fi](../../wifi.md)
- [Bluetooth](../../bluetooth.md)
- [HTTP](../../http.md)
- [Bootloader与Ota](../../bootloader_ota.md)
- [方案对照](../../bootloader_ota.md)
- [四套方案阶段对照](../../bootloader_ota.md)
- [公共框架](../bk_ota_framework.md)
- [安全 Overwrite 方案](../bk_ota_secure_overwrite.md)
- [安全 XIP A/B 方案](../bk_ota_secure_xip.md)
- [非安全非 AB 方案](../bk_ota_nosecure.md)
- [非安全 AB 方案](../bk_ota_nosecure_ab.md)
- [BLE_OTA](../ble_ota.md)
- [BK AT](../../at.md)
- [多媒体](../../multimedia.md)
- [显示](../../display.md)
- [VPU](../../vpu.md)
- [GPU](../../gpu.md)
- [NPU](../../npu.md)
- [音频](../../audio.md)
- [用例编写](../../examples.md)
- [文档系统](../../documentation.md)
- [摄像头](../../camera.md)
- [图像用户界面](../../gui.md)
- [多媒体网络传输](../../multimedia_network_transfer.md)
- [操作系统与内存管理](../../../os.md)
- [样例演示](../../../examples.md)
- [项目示例](../../../examples/projects.md)
- [应用开发](../../../application.md)
- [开发与贡献代码流程](../../../process.md)
- [云平台](../../../cloud.md)
- [常见问题](../../../FAQ.md)
- [支持的外设](../../../support_peripherals.md)
