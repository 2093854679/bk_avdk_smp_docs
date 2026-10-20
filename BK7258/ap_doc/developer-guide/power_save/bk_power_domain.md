---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/bk_power_domain.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 电源域说明

<a id="id2"></a>

## 电源域说明

<a id="id3"></a>

### 初识电源域

整个开发板分为三类电源域：
:   - 板级的电源域
    - 模拟部分电源域
    - 数字部分电源域

---

数字部分分为两个大的电源域：
:   - Aon电源域
    - Digital Core电源域

<a id="digital-core"></a>

### Digital Core电源域

Digital Core电源域下各个业务模块有自己单独的电源域。各个业务可以根据自己的工作场景来决定上电还是下电，这样功耗控制很灵活，不同的产品形态达到最优功耗。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [软件架构与分层](../architecture.md)
- [系统安全](../security.md)
- [低功耗与电源管理](../power_save.md)
- [基础概念](../power_save.md)
- [时钟说明](bk_clock.md)
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
