---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/bootloader_ota/bootloader_and_ota/bk_ota_upgrade_image.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bootloaderinfo"></a>

# 五.Bootloader升级固件相关info

- 1.升级固件制作有两种方式：

  - 1）方式一：通过工具手动生成；
  - 2）方式二：由编译打包的时候自动化生成；（首选方式二）
- 2.升级固件路径为：

重要

在bk\_avdk\_smp/build/bk7258/app/package/app\_pack.rbl

- 3.打开Everything-1.4.1.935.x64-Setup.exe，工具-\>选项-\>HTTP服务器，绑定本机ip。使用浏览器打开本机的ip地址，找到本地的升级文件 \*.rbl，拷贝url出来，用于cli命令。

> <a id="id1"></a>
> ![bootlaoder_everthing](../../../../../../_assets/6c15beb0b16c25c057a4-bootlaoder_everthing.png)
>
>
> 图6 Everything工具页面

- 4.使用串口发送cli命令，例如：
  cpu1 http\_ota <http://192.168.21.101/D%3A/E/build/app_pack.rbl>

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
- [L_bootloader介绍](bk_l_bootloader.md)
- [UP_bootloader和ota介绍](bk_up_bootloader_and_ota.md)
- [Bootloader镜像生成介绍](bk_bootloader_image_generate.md)
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
