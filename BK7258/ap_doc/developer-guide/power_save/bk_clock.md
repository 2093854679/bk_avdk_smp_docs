---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/bk_clock.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 时钟说明

系统时钟源，有以下几种：

- ROSC
- DCO
- XTAL-32k
- XTAL-26M
- AUPLL
- DPLL

备注：XTAL是指外部时钟：

- XTAL-32k：外部的32k；
- XTAL-26M: 外部的26M；

系统默认带外部的26M，外部的32K可以根据项目需要来考虑是否接上。

<a id="id2"></a>

## 时钟配置说明

32k的时钟源，有以下几种：

- rosc

优缺点：
功耗低，但是时钟精度相对来说不好，最优功耗时可以选用它。

- 外部26M分频出的时钟

优缺点：精度好，功耗相对高

- 外部32k时钟

优缺点：精度好，功耗相对外部26M分频的时钟低,但是得额外增加一个外部32K晶体

因此可以根据不同的业务和场景，选用不同的32k时钟

<a id="dpll"></a>

## DPLL使用介绍

<a id="dpll26m"></a>

### DPLL是通过外部26M时钟倍频上去

- WIFI在执行业务的工作时钟是DPLL
- BT在执行业务的工作时钟是DPLL
- 可以根据业务需要，使用不同的DPLL分频时钟来节省功耗

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [软件架构与分层](../architecture.md)
- [系统安全](../security.md)
- [低功耗与电源管理](../power_save.md)
- [基础概念](../power_save.md)
- [电源域说明](bk_power_domain.md)
- [CPU主频说明](bk_cpu_frequency.md)
- [系统状态机说明](bk_fsm.md)
- [状态机切换说明](bk_fsm.md)
- [睡眠模式与唤醒源配置](../power_save.md)
- [时钟源配置](../power_save.md)
- [电源与性能管理](../power_save.md)
- [问题排查与优化](../power_save.md)
- [设备管理框架](../driver_model.md)
- [外设与驱动](../peripheral.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [Bootloader与Ota](../bootloader_ota.md)
- [BK AT](../at.md)
- [多媒体](../multimedia.md)
- [显示](../display.md)
- [视频编解码](../video_codec.md)
- [音频](../audio.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [摄像头](../camera.md)
- [图像用户界面](../gui.md)
- [多媒体网络传输](../multimedia_network_transfer.md)
- [OS 相关参考](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
