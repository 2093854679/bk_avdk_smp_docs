---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/bootloader_ota/bootloader_and_ota/bk_l_bootloader.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="l-bootloader"></a>

# 二．l\_bootloader简介

l\_bootloader：主要是uart下载功能，流程图如上图2所示。

- 1.在romcode执行完成之后会跳转到flash的0x0地址执行；
- 2.此时会判断uart rx\_buf中有是否有数据，如果有数据，抢占到uart总线进入数据下载状态，下载完成之后会reboot；
- 3.如果此时uart rx\_buf中没有数据，会循环检测一定次数后会跳转到指定地址（此为逻辑地址）处执行up\_boot。
- 4.系统正常启动后运行在app业务中，uart接收到下载握手信息后会主动reboot进入l\_bootloader下载程序，用户也可以取消此功能。

## 模块导航

- [简介](../../../introduction.md)
- [H/W 参考手册](../../../hw-reference.md)
- [API 参考手册](../../../api-reference.md)
- [开发者指南](../../../developer-guide.md)
- [软件架构与分层](../../architecture.md)
- [系统安全](../../security.md)
- [低功耗与电源管理](../../power_save.md)
- [设备管理框架](../../driver_model.md)
- [外设与驱动](../../peripheral.md)
- [出错与日志](../../error_log.md)
- [系统调试](../../debug_trace.md)
- [Wi-Fi](../../wifi.md)
- [Bluetooth](../../bluetooth.md)
- [HTTP](../../http.md)
- [Bootloader与Ota](../../bootloader_ota.md)
- [bootloader和常规ota](../bootloader_and_ota.md)
- [Bootloader简介](bk_bootloader_brief_introduction.md)
- [UP_bootloader和ota介绍](bk_up_bootloader_and_ota.md)
- [Bootloader镜像生成介绍](bk_bootloader_image_generate.md)
- [ota升级固件介绍](bk_ota_upgrade_image.md)
- [Bootloader镜像更新说明](bk_bootloader_imag_update.md)
- [ab位置无关升级](../ab_position_independent_ota.md)
- [BLE_OTA](../ble_ota.md)
- [BK AT](../../at.md)
- [多媒体](../../multimedia.md)
- [显示](../../display.md)
- [视频编解码](../../video_codec.md)
- [音频](../../audio.md)
- [用例编写](../../examples.md)
- [文档系统](../../documentation.md)
- [摄像头](../../camera.md)
- [图像用户界面](../../gui.md)
- [多媒体网络传输](../../multimedia_network_transfer.md)
- [OS 相关参考](../../../os.md)
- [样例演示](../../../examples.md)
- [应用开发](../../../application.md)
- [开发与贡献代码流程](../../../process.md)
- [云平台](../../../cloud.md)
- [常见问题](../../../FAQ.md)
- [支持的外设](../../../support_peripherals.md)
