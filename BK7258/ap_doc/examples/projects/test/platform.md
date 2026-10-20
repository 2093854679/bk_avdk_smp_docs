---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/projects/test/platform/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 平台测试工程

<a id="id2"></a>

## 工程概述

`test/platform` 是 BK7258 平台驱动集成和回归测试工程。工程配置启用了常用外设和安全功能的 SDK CLI 测试。

当前配置覆盖：

- CP 侧看门狗、ADC/SADC、Flash、GPIO、PSRAM、PUF、Touch 和 UART 测试
- AP 侧 PWM、UART、I2C、SPI、Flash、GPIO、SARADC 和密码算法测试，并使能完整 mbedTLS
- 通过 CP 串口转发到 AP 的测试命令

<a id="id3"></a>

## 工程目录

- `ap/ap_main.c`：AP 初始化和可选 SMP 测试初始化
- `cp/cp_main.c`：CP 初始化和 CP1 启动逻辑
- `ap/config/bk7258_ap/config`：已启用的 AP 驱动测试功能
- `cp/config/bk7258/config`：已启用的 CP 驱动测试功能
- `.it.csv`：集成测试命令和预期输出，共 649 条用例
- `partitions/bk7258/`：测试分区和 RAM 区域定义

<a id="id4"></a>

## 编译

在 SDK 根目录执行：

```
make bk7258 PROJECT=test/platform
```

<a id="id5"></a>

## 运行

烧录生成的 AP 和 CP 镜像，连接测试所需的外设线路和串口，然后复位开发板。从 `.it.csv` 中选择适用命令执行，并将串口输出与预期结果进行比较。不带前缀的命令在 CP 串口直接执行，带 `ap_cmd` 前缀的命令由 CP 转发到 AP。

示例命令：

```
wdt_driver init
sadc 1 config 1 64 64 1
flash_test R 0x3da000 0x1000
ap_cmd pwm_driver init
ap_cmd uart_driver init
ap_cmd mbedtls_selftest
```

<a id="id6"></a>

## 测试注意事项

部分用例需要外部接线或两块开发板（`.it.csv` 第三列的设备号为 `2` 的共 140 条，涉及 UART 收发与 SPI 主从对测）。Flash 测试会擦写 `0x3da000` 起的地址，看门狗重启测试会主动复位设备。在保存有重要数据的开发板上运行前，请先检查对应的 `.it.csv` 用例。

## 模块导航

- [简介](../../../introduction.md)
- [H/W 参考手册](../../../hw-reference.md)
- [API 参考手册](../../../api-reference.md)
- [开发者指南](../../../developer-guide.md)
- [OS 相关参考](../../../os.md)
- [样例演示](../../../examples.md)
- [命令](../../cli.md)
- [外设](../../peripheral.md)
- [平台](../../platform.md)
- [工程](../../projects.md)
- [AP Powerdown Keepalive 示例工程](../ap_powerdown_keepalive.md)
- [默认应用工程](../app.md)
- [A/B OTA 应用工程](../app_ab.md)
- [语音识别服务示例工程](../asr_service_example.md)
- [音频播放器示例工程](../audio_player_example.md)
- [bluetooth](../bluetooth.md)
- [DMA2D Example](../dma2d_example.md)
- [BK7258 门铃 ASR 示例工程](../doorbell_asr.md)
- [Draw OSD 示例](../draw_osd_example.md)
- [DVP示例工程](../dvp_example.md)
- [Encoder示例工程](../encoder_example.md)
- [1. 工程概述](../encoder_example.md)
- [2. 目录结构](../encoder_example.md)
- [3. CLI命令使用](../encoder_example.md)
- [4. 编译和运行](../encoder_example.md)
- [5 注意事项](../encoder_example.md)
- [以太网示例工程](../eth_example.md)
- [JPEG解码示例工程](../jpeg_decode_example.md)
- [lvgl](../lvgl.md)
- [lwIP PSRAM 示例工程](../lwip_psram_example.md)
- [MCU LCD Display示例项目](../mcu_lcd_example.md)
- [播放器服务示例工程](../player_service_example.md)
- [AP 低压掉电示例项目](../pm_ap_powerdown.md)
- [QSPI LCD Display示例项目](../qspi_lcd_example.md)
- [RGB Display示例项目](../rgb_lcd_example.md)
- [安全启动 XIP OTA 工程](../secureboot_xip.md)
- [安全启动 XIP OTA 工程（关闭 Flash AES）](../secureboot_xip_no_encrypt.md)
- [SPI LCD Display示例项目](../spi_lcd_example.md)
- [SRAM Lite 工程](../sram_lite.md)
- [test](../test.md)
- [UVC双流示例工程](../uvc_dualstream_example.md)
- [UVC示例工程](../uvc_example.md)
- [Video Pipeline 示例项目](../video_pipeline_example.md)
- [视频录制与播放示例工程（video_player_example）](../video_player_example.md)
- [语音服务示例工程](../voice_service_example.md)
- [wifi](../wifi.md)
- [应用开发](../../../application.md)
- [开发与贡献代码流程](../../../process.md)
- [云平台](../../../cloud.md)
- [常见问题](../../../FAQ.md)
- [支持的外设](../../../support_peripherals.md)
