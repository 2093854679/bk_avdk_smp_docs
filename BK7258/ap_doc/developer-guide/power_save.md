---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 低功耗与电源管理

本章节介绍BK7258的低功耗特性和电源管理功能，包括系统架构、睡眠模式配置、唤醒源设置、时钟管理等内容。

<a id="id2"></a>

## 基础概念

了解系统电源管理的基础架构和工作原理。

- [电源域说明](power_save/bk_power_domain.md)
- [时钟说明](power_save/bk_clock.md)
- [CPU主频说明](power_save/bk_cpu_frequency.md)
- [系统状态机说明](power_save/bk_fsm.md)
- [状态机切换说明](power_save/bk_fsm.md#id2)

<a id="id3"></a>

## 睡眠模式与唤醒源配置

配置系统进入不同睡眠模式（深度睡眠、低压睡眠）以及设置唤醒源。

- [设置GPIO作为唤醒源](power_save/bk_gpio_sleep.md)
- [设置RTC作为唤醒源](power_save/bk_rtc_sleep.md)
- [获取睡眠唤醒源](power_save/bk_wakeup_source.md)
- [WIFI低压保活](power_save/bk_wifi_alive.md)

<a id="id4"></a>

## 时钟源配置

配置和管理系统时钟源，优化功耗表现。

- [32k的时钟源说明和配置](power_save/bk_32k_source.md)
- [切换32k时钟源函数接口说明](power_save/bk_32k_source.md#id1)
- [使用外部32K时钟源](power_save/bk_use_extern32K.md)

<a id="id5"></a>

## 电源与性能管理

动态管理系统电源和性能，实现功耗与性能的平衡。

- [动态切换CPU主频](power_save/bk_cpu_vote_freq.md)
- [关闭多媒体模块](power_save/bk_close_multimedia.md)

<a id="id6"></a>

## 问题排查与优化

低功耗问题的分析方法和优化指南。

- [低功耗问题分析](power_save/bk_Lowpower_problem_analysis.md)
- [低功耗问题分析checklist](power_save/bk_lowpower_checklist.md)

## 模块导航

- [简介](../introduction.md)
- [H/W 参考手册](../hw-reference.md)
- [API 参考手册](../api-reference.md)
- [开发者指南](../developer-guide.md)
- [软件架构与分层](architecture.md)
- [系统安全](security.md)
- [电源域说明](power_save/bk_power_domain.md)
- [时钟说明](power_save/bk_clock.md)
- [CPU主频说明](power_save/bk_cpu_frequency.md)
- [系统状态机说明](power_save/bk_fsm.md)
- [状态机切换说明](power_save/bk_fsm.md)
- [设置GPIO作为唤醒源](power_save/bk_gpio_sleep.md)
- [设置RTC作为唤醒源](power_save/bk_rtc_sleep.md)
- [获取睡眠唤醒源](power_save/bk_wakeup_source.md)
- [WIFI低压保活](power_save/bk_wifi_alive.md)
- [32k的时钟源说明和配置](power_save/bk_32k_source.md)
- [切换32k时钟源函数接口说明](power_save/bk_32k_source.md)
- [使用外部32K时钟源](power_save/bk_use_extern32K.md)
- [动态切换CPU主频](power_save/bk_cpu_vote_freq.md)
- [关闭多媒体模块](power_save/bk_close_multimedia.md)
- [低功耗问题分析](power_save/bk_Lowpower_problem_analysis.md)
- [低功耗问题分析checklist](power_save/bk_lowpower_checklist.md)
- [设备管理框架](driver_model.md)
- [外设与驱动](peripheral.md)
- [出错与日志](error_log.md)
- [系统调试](debug_trace.md)
- [Wi-Fi](wifi.md)
- [Bluetooth](bluetooth.md)
- [HTTP](http.md)
- [Bootloader与Ota](bootloader_ota.md)
- [BK AT](at.md)
- [多媒体](multimedia.md)
- [显示](display.md)
- [视频编解码](video_codec.md)
- [音频](audio.md)
- [用例编写](examples.md)
- [文档系统](documentation.md)
- [摄像头](camera.md)
- [图像用户界面](gui.md)
- [多媒体网络传输](multimedia_network_transfer.md)
- [OS 相关参考](../os.md)
- [样例演示](../examples.md)
- [应用开发](../application.md)
- [开发与贡献代码流程](../process.md)
- [云平台](../cloud.md)
- [常见问题](../FAQ.md)
- [支持的外设](../support_peripherals.md)
