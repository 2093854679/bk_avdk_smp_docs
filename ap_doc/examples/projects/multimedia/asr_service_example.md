---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/multimedia/asr_service_example/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="asr"></a>

# ASR 服务示例工程

<a id="id1"></a>

## 1\. 项目概述

本工程演示 BK7259 上基于 ADK 的语音识别（ASR）服务。识别引擎使用 BEKEN KWS（TFLite Micro \+ NPU），支持以下两种工作方式：

- `startwithmic`：ASR 服务直接打开板载或 UAC 麦克风采集并识别。
- `startnomic`：通过 Voice Service 获取音频流并交给 ASR 服务识别。

<a id="id2"></a>

## 2\. 硬件与串口

- BK7259 开发板。
- 板载麦克风或 UAC 麦克风。
- 串口终端连接 CP UART，默认波特率为 115200。
- ASR CLI 运行在 AP，需在 CP 串口命令前添加 `ap_cmd`。

<a id="id3"></a>

## 3\. 代码结构

```
asr_service_example/
├── ap/
│   ├── ap_main.c
│   ├── asr_service_test/
│   └── config/bk7259_ap/defconfig
├── cp/
│   ├── cp_main.c
│   └── config/bk7259/defconfig
└── partitions/bk7259/
```

<a id="id4"></a>

## 4\. 编译与烧录

在 SDK 根目录执行：

```
make bk7259 PROJECT=multimedia/asr_service_example
```

生成的固件位于：

```
build/bk7259/asr_service_example/package/all-app.bin
```

按照 BK7259 常规烧录流程将固件烧录到开发板。

<a id="cli"></a>

## 5\. CLI 命令

命令格式：

```
ap_cmd asr_service {startwithmic|startnomic|stop} [onboard|uac] [8000|16000] [aec_en]
```

常用示例：

```
# 板载麦克风，16 kHz
ap_cmd asr_service startwithmic onboard 16000

# 板载麦克风并启用 AEC
ap_cmd asr_service startwithmic onboard 16000 1

# 通过 Voice Service 获取音频流
ap_cmd asr_service startnomic onboard 16000 1

# 停止识别
ap_cmd asr_service stop
```

`aec_en` 可取 `0`、`1` 或 `aec`。UAC 麦克风路径不启用 AEC。输入采样率为 8 kHz 时，服务会重采样到 ASR 引擎使用的 16 kHz。

命令执行成功返回 `CMDRSP:OK`。识别到关键词后，串口会输出对应命令 ID。

<a id="id5"></a>

## 6\. 关键配置

主要配置位于 `ap/config/bk7259_ap/defconfig`：

- `CONFIG_ASR_SERVICE`
- `CONFIG_BEKEN_KWS`
- `CONFIG_TFLITE_MICRO`
- `CONFIG_NPU`
- `CONFIG_VOICE_SERVICE`
