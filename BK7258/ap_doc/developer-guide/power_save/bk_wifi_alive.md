---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/bk_wifi_alive.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wifi"></a>

# 设置WIFI低压保活说明

<a id="id1"></a>

## WIFI-调用函数和调用顺序说明

- 1. 当使用BT配置完网络，不要使用BT时，可以把它，这样可以达到更低的功耗
  > bk\_bluetooth\_deinit();
  >
  > 关闭BT
- 2.bk\_wifi\_send\_listen\_interval\_req(10);

  > 设置DTIM10(1:DTIM1)
- 3. demo\_sta\_app\_init(“a”, “b”);
  > 连接路由器（a:路由器的名字;b:路由器的密码）
- 4. bk\_pm\_module\_vote\_sleep\_ctrl(PM\_SLEEP\_MODULE\_NAME\_APP,0x1,0x0);
  > 向系统中投应用程序的票。

(备注：一定需要设备连接上路由器，拿到IP地址，才调用以上函数bk\_pm\_module\_vote\_sleep\_ctrl()投APP的票，不然移动设备不能网络唤醒测试设备)

备注

- 1. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入低压和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。
- 2. 当系统中BT或WIFI模块没有上电时，系统会自动给这两个模块投上sleep的票。
- 3. 追求最优功耗时，当系统开启音频，视频，LCD后，进入低压睡眠前需要把启音频，视频，LCD先关闭，再进入睡眠。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [软件架构与分层](../architecture.md)
- [系统安全](../security.md)
- [低功耗与电源管理](../power_save.md)
- [基础概念](../power_save.md)
- [睡眠模式与唤醒源配置](../power_save.md)
- [设置GPIO作为唤醒源](bk_gpio_sleep.md)
- [设置RTC作为唤醒源](bk_rtc_sleep.md)
- [获取睡眠唤醒源](bk_wakeup_source.md)
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
