---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/bootloader_ota/ab_position_independent_ota/bk_introduce_ab_functionality_or_establishing_ab_project.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="abab"></a>

# 增加AB分区功能或建立AB工程的介绍

> 一、在新工程中增加AB功能或新建AB工程的修改主要分为以下几点：
>
> - 1、首先，规划AB分区的分区表，增加AB功能相关的宏配置，以及修改ab\_position\_independent.csv的值，确保开启AB功能；
> - 2、最后，配置pj\_config.mk文件（配置bootloader的路径以及自动化编译所需的参数）
> - 3、具体步骤见下述描述。
>
> 二、新增AB分区功能具体步骤如下，以bk\_avdk\_smp/projects/app\_ab 工程为例（可当作example）：
>
> - 1、AB分区的分区表、宏配置如下：
>   :   - 1）需要有ota\_rbl.config ，该配置文件是制作AB升级固件时所需的配置；（可直接复制该文件，且该文件位置放置在auto\_partitions.csv同级目录文件下）；
>       - 2）然后需要有ab\_position\_independent.csv，该配置文件用于开启AB功能时所需（可直接复制该.csv文件）;
>       - 3）配置分区表，以auto\_partitions.csv为例：
>         :   - a)primary\_cp\_app、primary\_ap\_app的size均需为68k的倍数；
>             - b)所需s\_app的大小等于两个app分区和的大小；（若app只有一个，则s\_app的大小等于该app的大小）；
>             - c)所需ota\_fina\_executive分区，该分区为存储AB分区升级时的flag；
>       - 4）将该bk\_avdk\_smp/projects/app\_ab/ap/config/bk7258\_ap/config文件中的配置宏，拷贝到对应过程中的配置文件中；
>
> <a id="id1"></a>
> ![ab_config](../../../../../../_assets/f442e8ab366a564afa2f-ab_config.png)
>
>
> 图1 AB分区config配置
>
> <a id="id2"></a>
> ![ab_partition](../../../../../../_assets/f04a8016075469a5446e-ab_partition.png)
>
>
> 图2 AB的auto\_partitions.csv配置

备注

- 1.app、app1的size均需为68k的倍数；
- 2.s\_app的大小等于这两个app分区和的大小;

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
- [AB的bootloader镜像更新介绍](bk_ab_bootloader_imag_update_introduction.md)
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
