---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_wifi_alive.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wifi"></a>

# 设置WIFI睡眠模式保活说明

<a id="id1"></a>

## WIFI-调用函数和调用顺序说明

- 1. 当使用BT配置完网络且后续不再使用BT时，可以关闭BT以降低功耗。
  > bk\_bluetooth\_deinit();
  >
  > 关闭BT
- 2. 连接路由器，等待STA拿到IP地址。
  > demo\_sta\_app\_init(“a”, “b”);
  >
  > 连接路由器（a:路由器的名字；b:路由器的密码）
- 3. bk\_wifi\_send\_listen\_interval\_req(10);
  > 设置监听间隔为10个DTIM周期（1表示DTIM1）。监听间隔越大，功耗越低，但广播包丢失风险也会增加，需要按业务场景选择。
- 4. bk\_pm\_sleep\_mode\_set(PM\_MODE\_LOW\_VOLTAGE);
  > 设置睡眠模式，进入睡眠模式。
- 5. bk\_pm\_module\_vote\_sleep\_ctrl(PM\_SLEEP\_MODULE\_NAME\_APP,0x1,0x0);
  > 向系统中投应用程序的票。

(备注：一定需要设备连接上路由器并拿到IP地址后，才调用 `bk_pm_module_vote_sleep_ctrl()` 投APP的票，否则移动设备不能通过网络唤醒测试设备。)

备注

- 1. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入睡眠模式和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。
- 2. 当前代码不会因为BT或WIFI未上电而自动替应用投对应的sleep票；需要进入睡眠模式时，应以 `pm_debug 8` 输出的 `not_sleeped` 字段确认仍未满足的票。
- 3. WIFI模块投 `PM_SLEEP_MODULE_NAME_WIFIP_MAC` sleep票时，SDK内部会设置MAC唤醒源，应用程序不需要再调用 `bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_WIFI, ...)`。
- 4. 追求最优功耗时，当系统开启音频，视频，LCD，CPU1，CPU2后，进入睡眠模式前需要把音频，视频，LCD，CPU1,CPU2先关闭，再进入睡眠。

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
- [时钟说明](bk_clock.md)
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
