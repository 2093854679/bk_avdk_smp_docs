---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_cpu_frequency.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cpu"></a>

# CPU时钟源说明

CPU有以下时钟源：

- 26M
- DCO
- 320M
- 480M

备注：
CP主频最高可以达到240M（通过480M分频得到），AP主频最高可以达到480M。

<a id="id1"></a>

## CPU主频切换说明

- 可以根据业务需要动态的切频率来达到最优功耗,CPU主频切换相对来说比较复杂,SDK内部来实现。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [软件架构与分层](../architecture.md)
- [系统安全](../security.md)
- [低功耗与电源管理](../power_save.md)
- [AP侧bk_pm目录文件说明](bk_pm_directory.md)
- [低功耗整体架构](bk_lowpower_architecture.md)
- [系统状态机说明](bk_fsm.md)
- [状态机切换说明](bk_fsm.md)
- [睡眠模式说明](bk_sleep_mode.md)
- [如何动态切换CPU主频](bk_cpu_vote_freq.md)
- [AP侧电源域控制](bk_power_domain_ctrl.md)
- [AP侧配置GPIO和RTC唤醒说明](bk_ap_wakeup.md)
- [AP快速启动](bk_ap_fast_boot.md)
- [AP低功耗问题分析](bk_Lowpower_problem_analysis.md)
- [设备管理框架](../driver_model.md)
- [外设与驱动](../peripheral.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [CPU Hotplug](../cpu_hotplug.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [Bootloader与Ota](../bootloader_ota.md)
- [BK AT](../at.md)
- [多媒体](../multimedia.md)
- [显示](../display.md)
- [VPU](../vpu.md)
- [GPU](../gpu.md)
- [NPU](../npu.md)
- [音频](../audio.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [摄像头](../camera.md)
- [图像用户界面](../gui.md)
- [多媒体网络传输](../multimedia_network_transfer.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [项目示例](../../examples/projects.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
