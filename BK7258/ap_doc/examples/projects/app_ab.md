---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/projects/app_ab/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="a-b-ota"></a>

# A/B OTA 应用工程

<a id="id1"></a>

## 工程概述

`app_ab` 是 BK7258 位置无关 A/B OTA 升级参考工程。应用启动过程沿用标准 AP/CP 流程，工程配置和分区文件用于启用 A/B 镜像打包与升级。

主要特性：

- A/B OTA 和 HTTP OTA 支持
- 位置无关应用镜像
- OTA 镜像 Hash 校验
- 备用应用区 `s_app` 和 OTA 完成状态数据 `ota_fina_executive`

<a id="id2"></a>

## 工程目录

- `ap/ap_main.c`：AP 应用入口
- `cp/cp_main.c`：CP 应用入口和 CP1 启动逻辑
- `ap/config/bk7258_ap/config`：包含 A/B OTA 选项的 AP 配置
- `cp/config/bk7258/config`：CP 配置
- `partitions/bk7258/auto_partitions.csv`：A/B Flash 分区表
- `partitions/bk7258/ab_position_independent.csv`：位置无关镜像配置
- `partitions/bk7258/ota_rbl.config`：OTA 包配置

<a id="id3"></a>

## 编译

在 SDK 根目录执行：

```
make bk7258 PROJECT=app_ab
```

<a id="id4"></a>

## 运行与验证

1. 编译工程并烧录生成的初始镜像。
2. 按 SDK 打包流程使用生成的 A/B OTA 产物制作升级包。
3. 通过已启用的 OTA 接口启动升级，升级内容写入 `s_app`。
4. 复位开发板，确认系统启动到更新后的镜像。

分区表和 OTA 包配置共同构成升级约束。修改镜像大小或启用更多功能前，应先检查这些文件。

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
- [默认应用工程](app.md)
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
