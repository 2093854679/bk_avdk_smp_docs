---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/bk_use_extern32K.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="k"></a>

# 使用外部32K

<a id="id1"></a>

## 开启外部32K时钟源方法

- 确保硬件已经焊接了外部32K时钟源
- 在middleware/soc/bk72xx/bk7258.defconfig中设置CONFIG\_EXTERN\_32K\=y

重要

当本地工程应用于其他项目时，为避免定义外部32K影响该工程，请新建工程，将CONFIG\_EXTERN\_32K定义在根目录下projects的新建工程的config/bk72xx.config中。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [软件架构与分层](../architecture.md)
- [系统安全](../security.md)
- [低功耗与电源管理](../power_save.md)
- [电源域说明](bk_power_domain.md)
- [时钟说明](bk_clock.md)
- [CPU主频说明](bk_cpu_frequency.md)
- [系统状态机说明](bk_fsm.md)
- [状态机切换说明](bk_fsm.md)
- [设置GPIO作为唤醒源，系统进入深度睡眠和低压睡眠说明](bk_gpio_sleep.md)
- [设置RTC作为唤醒源，系统进入深度睡眠和低压睡眠说明](bk_rtc_sleep.md)
- [设置TOUCH作为唤醒源，系统进入深度睡眠和低压睡眠说明](bk_touch_sleep.md)
- [32k的时钟源说明和配置](bk_32k_source.md)
- [切换32k时钟源函数接口说明](bk_32k_source.md)
- [设置WIFI低压保活说明](bk_wifi_alive.md)
- [如何动态切换CPU主频](bk_cpu_vote_freq.md)
- [如何启动和关闭CPU1](bk_vote_boot_cp1.md)
- [关闭多媒体模块接口参考](bk_close_multimedia.md)
- [低功耗问题分析](bk_Lowpower_problem_analysis.md)
- [低功耗问题分析checklist](bk_lowpower_checklist.md)
- [设备管理框架](../driver_model.md)
- [外设与驱动](../peripheral.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [OS 相关参考](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
