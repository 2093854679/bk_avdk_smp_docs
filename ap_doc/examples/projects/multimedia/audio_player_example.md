---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/multimedia/audio_player_example/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 音频播放器示例工程

<a id="id2"></a>

## 1\. 项目概述

本工程演示 BK7259 `bk_audio_player` 组件的基本使用方法。播放器运行在 AP， 支持文件、网络和 HLS 音频源，支持 MP3、WAV、AAC 和 TS 解码，并通过板载 扬声器输出。

<a id="id3"></a>

## 2\. 硬件与串口

- BK7259 开发板及板载扬声器。
- 播放本地文件时需要 SD 卡，文件系统挂载点为 `/sd0`。
- 播放网络或 HLS 音频时需要可用网络。
- 串口终端连接 CP UART，默认波特率为 115200。
- 播放器 CLI 运行在 AP，需在 CP 串口命令前添加 `ap_cmd`。

<a id="id4"></a>

## 3\. 代码结构

```
audio_player_example/
├── ap/
│   ├── ap_main.c
│   ├── audio_player_test/
│   │   └── cli_audio_player.c
│   └── config/bk7259_ap/defconfig
├── cp/
│   ├── cp_main.c
│   └── config/bk7259/defconfig
└── partitions/bk7259/
```

<a id="id5"></a>

## 4\. 编译与烧录

```
make bk7259 PROJECT=multimedia/audio_player_example
```

固件输出路径：

```
build/bk7259/audio_player_example/package/all-app.bin
```

编译完成后，按照 BK7259 常规流程烧录固件。

<a id="cli"></a>

## 5\. CLI 命令

命令格式为 `ap_cmd audio_player <subcommand> [parameters]`。

| 子命令 | 参数 | 功能 |
| --- | --- | --- |
| `init` / `deinit` | 无 | 创建或销毁播放器 |
| `add` | `<name> <uri>` | 添加播放项 |
| `rm` | `<uri>` | 按 URI 删除播放项 |
| `clear` / `dump` | 无 | 清空或打印播放列表 |
| `mode` | `<mode>` | 设置播放模式 |
| `volume` | `[value]` | 设置或读取音量 |
| `start` / `stop` | 无 | 开始或停止播放 |
| `pause` / `resume` | 无 | 暂停或恢复播放 |
| `prev` / `next` | 无 | 切换上一首或下一首 |
| `jump` | `<id>` | 跳转到指定播放项 |
| `sd_mount` / `sd_unmount` | 无 | 挂载或卸载 SD 卡 |
| `sd_scan` | 无 | 扫描 `/sd0` 并添加媒体文件 |

SD 卡播放示例：

```
ap_cmd audio_player init
ap_cmd audio_player sd_mount
ap_cmd audio_player sd_scan
ap_cmd audio_player dump
ap_cmd audio_player start
```

直接添加文件或网络 URI：

```
ap_cmd audio_player init
ap_cmd audio_player add local /sd0/test.mp3
ap_cmd audio_player add network http://example.com/test.mp3
ap_cmd audio_player start
```

命令成功返回 `CMDRSP:OK`，失败返回 `CMDRSP:ERROR`。

<a id="id6"></a>

## 6\. 关键配置

主要配置位于 `ap/config/bk7259_ap/defconfig`：

- `CONFIG_MEDIA_SERVICE`
- `CONFIG_AUDIO_PLAYER`
- `CONFIG_SDCARD`
- `CONFIG_FATFS`
- `CONFIG_VFS`
- `CONFIG_WEBCLIENT`
