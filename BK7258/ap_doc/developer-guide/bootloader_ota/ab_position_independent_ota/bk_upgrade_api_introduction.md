---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/bootloader_ota/ab_position_independent_ota/bk_upgrade_api_introduction.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ab"></a>

# AB分区位置无关的升级性格接口介绍

- 1 获取当前的执行分区；

  > uint8 bk\_ota\_get\_current\_partition(void);
  >
  > 备注
  >
  > 返回值简介：
  > 0： means current execute A partition.
  > 1： means current execute B partition.
- 2 当app镜像下载成功之后，客户需要调用该接口，返回将升级的的分区；

  > void bk\_ota\_register\_temp\_partition\_callback(callback\_func cb);
  >
  > 备注
  >
  > 返回值简介：
  > 3： means temporary execute A partition.
  > 4： means temporary execute B partition.
- 3 当执行完升级重启之后，客户需要在app中，确认当前的升级分区ok.

  > void bk\_ota\_double\_check\_for\_execution(void);
- 4 当前发布的SDK版本中，上述（2，3）为方便自测试，已实现（被CONFIG\_OTA\_UPDATE\_DEFAULT\_PARTITION控制），客户需要在（projects/customization/config\_ab/config/bk7258/config）将CONFIG\_OTA\_UPDATE\_DEFAULT\_PARTITION 这个宏定义关闭。
- app下载镜像成功之后，需要客户返回需要临时执行的分区；见下图1

<a id="id1"></a>
![ab_position_indes_api_introduction](../../../../../../_assets/c8d4fb681b08a3667465-ab_position_indes_api_introduction.png)


图1 临时执行分区的接口

- app升级镜像成功之后，需要客户在app中确认当前升级分区ok，调用bk\_ota\_double\_check\_for\_execution；（参考components/bk\_init见下图2）

<a id="id2"></a>
![ab_position_indes_api_introduction2](../../../../../../_assets/5bec7358f327a7642a2d-ab_position_indes_api_introduction2.png)


图2 确认执行分区的接口

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
- [ab位置无关升级](../ab_position_independent_ota.md)
- [AB分区位置无关ota概述](bk_ab_position_independent_ota_overview.md)
- [AB分区位置无关升级原理](bk_upgrade_principle_introduction.md)
- [AB分区位置无关工程介绍](bk_ab_position_independent_project_introduction.md)
- [AB分区位置无关的编译命令介绍](bk_compile_command_introduction.md)
- [AB分区位置无关的升级镜像路径](bk_upgrade_image_route_introduction.md)
- [AB分区位置无关的优势](bk_upgrade_advantage_introduction.md)
- [AB分区位置无关的升级流程介绍](bk_upgrade_process_introduction.md)
- [AB分区位置无关的hash功能验证流程介绍](bk_hash_process_introduction.md)
- [AB的bootloader镜像更新介绍](bk_ab_bootloader_imag_update_introduction.md)
- [增加AB分区功能或建立AB工程的介绍](bk_introduce_ab_functionality_or_establishing_ab_project.md)
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
