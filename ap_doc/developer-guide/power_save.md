---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap"></a>

# AP侧低功耗配置说明

BK7259低功耗采用CP主控、AP配合的架构。低功耗状态机、睡眠投票、唤醒源管理、电源域和AP上下电控制主体在CP侧；AP侧主要负责音频、视频、LCD、多媒体等业务模块的关闭/恢复，以及在需要由AP应用发起低功耗流程时完成GPIO、RTC唤醒和AP关闭投票等配置。

本目录是AP侧低功耗配置入口，重点说明AP侧需要关注的目录文件、配置流程和调试方法。若需要了解CP侧完整低功耗架构、状态机和底层唤醒源实现，请参考CP侧低功耗文档目录：

> - CP侧低功耗章节已同步到本目录，可从下方目录进入；CP侧源码目录为 `cp/docs/bk7259/zh_CN/developer-guide/power_save/index.rst`。

AP侧低功耗入口

- [AP侧bk\_pm目录文件说明](power_save/bk_pm_directory.md)
- [低功耗整体架构](power_save/bk_lowpower_architecture.md)
- [系统状态机说明](power_save/bk_fsm.md)
- [状态机切换说明](power_save/bk_fsm.md#id3)
- [睡眠模式说明](power_save/bk_sleep_mode.md)
- [CPU主频说明](power_save/bk_cpu_frequency.md)
- [如何动态切换CPU主频](power_save/bk_cpu_vote_freq.md)
- [AP侧电源域控制](power_save/bk_power_domain_ctrl.md)
- [AP侧配置GPIO和RTC唤醒说明](power_save/bk_ap_wakeup.md)
- [AP快速启动](power_save/bk_ap_fast_boot.md)
- [AP低功耗问题分析](power_save/bk_Lowpower_problem_analysis.md)

## 模块导航

- [简介](../introduction.md)
- [H/W 参考手册](../hw-reference.md)
- [API 参考手册](../api-reference.md)
- [开发者指南](../developer-guide.md)
- [软件架构与分层](architecture.md)
- [系统安全](security.md)
- [AP侧bk_pm目录文件说明](power_save/bk_pm_directory.md)
- [低功耗整体架构](power_save/bk_lowpower_architecture.md)
- [系统状态机说明](power_save/bk_fsm.md)
- [状态机切换说明](power_save/bk_fsm.md)
- [睡眠模式说明](power_save/bk_sleep_mode.md)
- [CPU主频说明](power_save/bk_cpu_frequency.md)
- [如何动态切换CPU主频](power_save/bk_cpu_vote_freq.md)
- [AP侧电源域控制](power_save/bk_power_domain_ctrl.md)
- [AP侧配置GPIO和RTC唤醒说明](power_save/bk_ap_wakeup.md)
- [AP快速启动](power_save/bk_ap_fast_boot.md)
- [AP低功耗问题分析](power_save/bk_Lowpower_problem_analysis.md)
- [设备管理框架](driver_model.md)
- [外设与驱动](peripheral.md)
- [出错与日志](error_log.md)
- [系统调试](debug_trace.md)
- [CPU Hotplug](cpu_hotplug.md)
- [Wi-Fi](wifi.md)
- [Bluetooth](bluetooth.md)
- [HTTP](http.md)
- [Bootloader与Ota](bootloader_ota.md)
- [BK AT](at.md)
- [多媒体](multimedia.md)
- [显示](display.md)
- [VPU](vpu.md)
- [GPU](gpu.md)
- [NPU](npu.md)
- [音频](audio.md)
- [用例编写](examples.md)
- [文档系统](documentation.md)
- [摄像头](camera.md)
- [图像用户界面](gui.md)
- [多媒体网络传输](multimedia_network_transfer.md)
- [操作系统与内存管理](../os.md)
- [样例演示](../examples.md)
- [项目示例](../examples/projects.md)
- [应用开发](../application.md)
- [开发与贡献代码流程](../process.md)
- [云平台](../cloud.md)
- [常见问题](../FAQ.md)
- [支持的外设](../support_peripherals.md)
