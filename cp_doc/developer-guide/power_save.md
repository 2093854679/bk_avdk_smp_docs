---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 低功耗与电源管理

整体架构与状态模型

- [低功耗整体架构](power_save/bk_lowpower_architecture.md)
- [系统状态机说明](power_save/bk_fsm.md)
- [状态机切换说明](power_save/bk_fsm.md#id3)
- [睡眠模式说明](power_save/bk_sleep_mode.md)

电源、时钟与性能配置

- [电源域说明](power_save/bk_power_domain.md)
- [时钟说明](power_save/bk_clock.md)
- [32k的时钟源说明和配置](power_save/bk_32k_source.md)
- [切换32k时钟源函数接口说明](power_save/bk_32k_source.md#id1)
- [使用外部32K时钟源](power_save/bk_use_extern32K.md)
- [CPU主频说明](power_save/bk_cpu_frequency.md)
- [如何动态切换CPU主频](power_save/bk_cpu_vote_freq.md)
- [低功耗工程配置说明](power_save/bk_lowpower_project_config.md)
- [CP快速启动](power_save/bk_cp_fast_boot.md)
- [AP快速启动配置说明](power_save/bk_ap_fast_boot_config.md)

睡眠进入与唤醒源

- [设置GPIO作为唤醒源，系统进入深度、超深度睡眠和睡眠模式说明](power_save/bk_gpio_sleep.md)
- [设置RTC作为唤醒源，系统进入深度、超深度睡眠和睡眠模式说明](power_save/bk_rtc_sleep.md)
- [设置TOUCH作为唤醒源，系统进入深度睡眠和睡眠模式说明](power_save/bk_touch_sleep.md)

保活、AP与多媒体控制

- [设置WIFI睡眠模式保活说明](power_save/bk_wifi_alive.md)
- [蓝牙睡眠模式使用说明](power_save/bk_bluetooth_sleep_mode.md)
- [AP侧配置GPIO和RTC唤醒说明](power_save/bk_ap_wakeup.md)
- [如何启动和关闭AP](power_save/bk_vote_boot_ap.md)
- [CP侧AP上下电回调使用说明](power_save/bk_ap_ctrl_callback.md)
- [关闭多媒体模块接口参考](power_save/bk_close_multimedia.md)

调试与问题分析

- [低功耗问题分析](power_save/bk_Lowpower_problem_analysis.md)
- [低功耗问题分析checklist](power_save/bk_lowpower_checklist.md)
