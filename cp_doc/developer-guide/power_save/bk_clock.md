---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_clock.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
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
- [低功耗整体架构](bk_lowpower_architecture.md)
- [系统状态机说明](bk_fsm.md)
- [状态机切换说明](bk_fsm.md)
- [睡眠模式说明](bk_sleep_mode.md)
- [电源域说明](bk_power_domain.md)
- [32k的时钟源说明和配置](bk_32k_source.md)
- [切换32k时钟源函数接口说明](bk_32k_source.md)
- [使用外部32K时钟源](bk_use_extern32K.md)
- [CPU主频说明](bk_cpu_frequency.md)
- [如何动态切换CPU主频](bk_cpu_vote_freq.md)
- [低功耗工程配置说明](bk_lowpower_project_config.md)
- [CP快速启动](bk_cp_fast_boot.md)
- [AP快速启动配置说明](bk_ap_fast_boot_config.md)
- [设置GPIO作为唤醒源，系统进入深度、超深度睡眠和睡眠模式说明](bk_gpio_sleep.md)
- [设置RTC作为唤醒源，系统进入深度、超深度睡眠和睡眠模式说明](bk_rtc_sleep.md)
- [设置TOUCH作为唤醒源，系统进入深度睡眠和睡眠模式说明](bk_touch_sleep.md)
- [设置WIFI睡眠模式保活说明](bk_wifi_alive.md)
- [蓝牙睡眠模式使用说明](bk_bluetooth_sleep_mode.md)
- [AP侧配置GPIO和RTC唤醒说明](bk_ap_wakeup.md)
- [如何启动和关闭AP](bk_vote_boot_ap.md)
- [CP侧AP上下电回调使用说明](bk_ap_ctrl_callback.md)
- [关闭多媒体模块接口参考](bk_close_multimedia.md)
- [低功耗问题分析](bk_Lowpower_problem_analysis.md)
- [低功耗问题分析checklist](bk_lowpower_checklist.md)
- [设备管理框架](../driver_model.md)
- [外设与驱动](../peripheral.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [CPU Hotplug](../cpu_hotplug.md)
- [Wi-Fi](../wifi.md)
- [HTTP](../http.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
