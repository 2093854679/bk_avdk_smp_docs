---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/bootloader_ota/ab_position_independent_ota/bk_ab_bootloader_imag_update_introduction.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bootloader-bin"></a>

# Bootloader.bin的镜像更新说明

- 1.为了优化bootloader.bin镜像的版本发布，从tag:v2.0.1.8版本开始：bootloader镜像的打包路径发生改变，由原先的默认路径middleware/boards/更改为bk\_avdk\_smp/cp/components/bk\_libs目录下。

  重要

  自从tag:v2.0.1.10之后的版本，已实现全自动插入bootloader.bin中的分区表，无需再手动修改bootloader中分区表。

  - 1.以bk\_avdk\_smp中app\_ab工程为例修改分区步骤如下：
    :   - 1.当通过修改bk\_avdk\_smp/projects/app\_ab/partitions/bk7258/auto\_partitions.csv文件来修改分区；
        - 2.直接make bk7258 PROJECT \= app\_ab即可；
        - 3.无需手动修改bk\_avdk\_smp/cp/components/bk\_libs/bk7258/bootloader/normal\_bootloader/bootloader.bin；

  重要

  bootloader镜像的打包路径发生改变，由原先的默认路径middleware/boards/更改为bk\_avdk\_smp/cp/components/bk\_libs目录下。

  - 1.以7258的app\_ab工程为例：
    :   - bootloader现路径为：bk\_avdk\_smp/cp/components/bk\_libs/bk7258/bootloader/ab\_bootloader/bootloader.bin；
- 2.若升级过程中出现问题，请联系我们FAE支持。

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
- [AB分区位置无关的相关接口介绍](bk_upgrade_api_introduction.md)
- [AB分区位置无关的hash功能验证流程介绍](bk_hash_process_introduction.md)
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
