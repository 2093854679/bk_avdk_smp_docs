---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/projects/app/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 默认应用工程

<a id="id2"></a>

## 工程概述

`app` 是 BK7258 的默认应用工程，提供标准的 AP/CP 启动流程和通用 SDK 开发、功能验证配置。

- CP 完成系统初始化并投票拉起 CP1，启动 SMP。
- AP 完成应用环境初始化。
- 可通过工程配置选择 SMP、IPC 和 BLE 配网测试代码。
- 默认配置启用常用的 Wi-Fi、蓝牙、存储、文件系统、安全和网络功能。
- 支持 BK7258 和 BK7257 两个编译目标。

<a id="id3"></a>

## 工程目录

- `ap/ap_main.c`：AP 应用入口和可选测试初始化
- `cp/cp_main.c`：CP 应用入口和 CP1 启动逻辑
- `ap/config/bk7258_ap/config`：AP 工程配置
- `ap/config/bk7258_ap/no_cli.config`：关闭 CLI 的替代配置
- `cp/config/bk7258/config`：CP 工程配置
- `partitions/bk7258/auto_partitions.csv`：Flash 分区表
- `partitions/bk7258/ram_regions.csv`：SRAM/PSRAM 区域划分

<a id="id4"></a>

## 编译

在 SDK 根目录执行：

```
make bk7258 PROJECT=app
```

`app` 是默认工程，因此也可以执行：

```
make bk7258
```

编译 BK7257 目标：

```
make bk7257 PROJECT=app
```

如需使用关闭 CLI 的替代配置，执行：

```
make bk7258 PROJECT=app BK_CONFIG_FILE=no_cli
```

<a id="id5"></a>

## 运行

烧录生成的 AP 和 CP 镜像，连接对应串口并复位开发板。可通过已启用的 SDK CLI 命令验证配置中的功能，发往 AP 的命令需加 `ap_cmd` 前缀。

如需修改工程选项，请更新 AP 或 CP 的 `config`，也可以在重新编译前运行 `make bk7258_ap_menuconfig PROJECT=app` 或 `make bk7258_cp_menuconfig PROJECT=app`。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [OS 相关参考](../../os.md)
- [样例演示](../../examples.md)
- [命令](../cli.md)
- [外设](../peripheral.md)
- [平台](../platform.md)
- [工程](../projects.md)
- [AP Powerdown Keepalive 示例工程](ap_powerdown_keepalive.md)
- [A/B OTA 应用工程](app_ab.md)
- [语音识别服务示例工程](asr_service_example.md)
- [音频播放器示例工程](audio_player_example.md)
- [bluetooth](bluetooth.md)
- [DMA2D Example](dma2d_example.md)
- [BK7258 门铃 ASR 示例工程](doorbell_asr.md)
- [Draw OSD 示例](draw_osd_example.md)
- [DVP示例工程](dvp_example.md)
- [Encoder示例工程](encoder_example.md)
- [1. 工程概述](encoder_example.md)
- [2. 目录结构](encoder_example.md)
- [3. CLI命令使用](encoder_example.md)
- [4. 编译和运行](encoder_example.md)
- [5 注意事项](encoder_example.md)
- [以太网示例工程](eth_example.md)
- [JPEG解码示例工程](jpeg_decode_example.md)
- [lvgl](lvgl.md)
- [lwIP PSRAM 示例工程](lwip_psram_example.md)
- [MCU LCD Display示例项目](mcu_lcd_example.md)
- [播放器服务示例工程](player_service_example.md)
- [AP 低压掉电示例项目](pm_ap_powerdown.md)
- [QSPI LCD Display示例项目](qspi_lcd_example.md)
- [RGB Display示例项目](rgb_lcd_example.md)
- [安全启动 XIP OTA 工程](secureboot_xip.md)
- [安全启动 XIP OTA 工程（关闭 Flash AES）](secureboot_xip_no_encrypt.md)
- [SPI LCD Display示例项目](spi_lcd_example.md)
- [SRAM Lite 工程](sram_lite.md)
- [test](test.md)
- [UVC双流示例工程](uvc_dualstream_example.md)
- [UVC示例工程](uvc_example.md)
- [Video Pipeline 示例项目](video_pipeline_example.md)
- [视频录制与播放示例工程（video_player_example）](video_player_example.md)
- [语音服务示例工程](voice_service_example.md)
- [wifi](wifi.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
