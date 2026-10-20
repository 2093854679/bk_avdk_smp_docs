---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/multimedia/video_file_recording.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 视频文件录制

<a id="id2"></a>

## 1、概述

本节介绍 BK7258 平台上“视频文件录制（Video Record）”的典型使用方式，包括支持的容器/编码格式、关键配置项、典型数据流，以及示例工程的使用说明。

该录制模块通过上层回调获取视频帧/音频数据，并将数据封装为文件（AVI/MP4）写入存储介质（如 SD 卡）。

- 有关视频文件录制的示例工程，请参阅：

  - [Video Record 示例工程](../../examples/projects/video_player_example.md)
- 有关 Video Record 的 API 参考，请参阅：

  - [Video Record API](../../api-reference/multimedia/bk_video_record.md)

<a id="id3"></a>

## 2、支持的功能

- **容器格式**：AVI、MP4
- **视频**：MJPEG、H264、YUV（与实际输入与配置相关）
- **音频**：PCM（默认）、AAC、G711A/G711U、G722、MP3（示例工程支持通过关键字启用，MP3 当前无编码器）
- **文件存储**：依赖 VFS/文件系统（示例工程使用 SD 卡挂载点 `/sd0`）

重要

当录制音频格式选择 `g722` 时，当前录制链路要求按 **16 kHz PCM** 进行编码（即 AVI 头 `SamplesPerSec=16000`）。
若以 8 kHz 方式生成 G722 码流，录制文件在解析/播放时音频会出现异常。

备注

**G711A/G711U（A-law/u-law）录制说明**

- **推荐采样率**：8 kHz（窄带语音场景）
- **位宽**：8-bit（容器头 `BitsPerSample=8`）
- **示例工程关键字**：
  \- `g711a` / `alaw` / `G711A` / `ALAW`
  \- `g711u` / `ulaw` / `G711U` / `ULAW`

重要

**支持但未验证的格式说明**

录制/封装链路中存在部分音频格式的代码路径支持，但示例工程未对端到端“录制 -\> 解析 -\> 播放”进行验证，使用前请自行验证：

- **MP3**：示例工程当前不提供 MP3 编码器（CLI 会提示不支持），仅封装路径可能具备兼容处理。

<a id="id4"></a>

## 3、相关头文件

- `ap/include/components/bk_video_recorder.h`
- `ap/include/components/bk_video_recorder_types.h`
- `ap/include/modules/avilib.h`
- `ap/include/modules/mp4lib.h`

备注

**avilib/mp4lib 接口（直接使用容器库）**

若直接使用容器库进行录制，请在关闭文件前传入实际录制时长（毫秒）以修正帧率：

```
void AVI_update_video_frame_rate_by_duration(avi_t *AVI, uint32_t duration_ms);
void MP4_update_video_frame_rate_by_duration(mp4_t *mp4, uint32_t duration_ms);
```

<a id="kconfig"></a>

## 4、配置选项（Kconfig）

<a id="id5"></a>

### 4.1 组件使能

录制模块的 Kconfig 配置位于：

- `ap/components/bk_video_record/Kconfig`

常用配置项：

- **CONFIG\_VIDEO\_RECORD**：使能视频录制模块
- **CONFIG\_VIDEO\_RECORD\_TASK\_STACK\_SIZE**：录制任务栈大小（字节），默认 2048

备注

录制过程中会涉及摄像头采集、音频采集、编码与文件写入等链路，资源占用与实时性要求较高。若出现丢帧/卡顿，可优先检查任务栈大小、heap/PSRAM 余量、SD 卡写入性能以及日志等级。

<a id="id6"></a>

## 5、典型数据流

录制模块的典型数据流如下：

- **视频路径**：Camera/DVP -\>（编码或打包前的帧）-\> `get_frame_cb` -\> Video record -\> 容器封装 -\> 文件写入
- **音频路径**：Mic/ADC/I2S -\>（编码前的 PCM/AAC 输入）-\> `get_audio_cb` -\> Video record -\> 容器封装 -\> 文件写入

上层需要实现回调并保证：

- 回调返回的缓冲区在写入完成前保持有效
- 写入完成后，通过 `release_frame_cb` / `release_audio_cb` 释放或归还缓冲区

<a id="api"></a>

## 6、API 使用流程

录制 API 的典型调用顺序如下：

1. `bk_video_recorder_new()` 创建录制实例并传入 `bk_video_record_config_t` （包含回调与参数）
2. `bk_video_recorder_open()` 打开录制器
3. `bk_video_recorder_start()` 开始录制（设置文件路径与容器类型）
4. 录制过程中，模块会周期性调用上层回调获取视频帧/音频数据并写入文件
5. `bk_video_recorder_stop()` 停止录制
6. `bk_video_recorder_close()` 关闭录制器
7. `bk_video_recorder_delete()` 删除实例并释放资源

重要

- 上层回调中应避免长时间阻塞操作，以免影响录制实时性。
- 当队列满或内存不足时，录制链路可能丢帧或写入失败。建议在系统设计时预留足够的缓冲与存储写入带宽。

<a id="id7"></a>

## 7、示例工程

示例工程路径：

- `projects/video_player_example`

该示例提供 `video_record` CLI 命令，可将 DVP 摄像头视频与麦克风音频录制到 SD 卡文件。

<a id="id8"></a>

## 8、使用示例

以下示例仅展示“创建-打开-开始-停止-关闭-删除”的基本流程。上层需要按实际视频/音频数据来源实现回调。

```
#include "components/bk_video_recorder.h"

// Return 0 on success, negative on error.
static int get_frame_cb(void *user_data, video_record_frame_data_t *frame_data)
{
    (void)user_data;
    (void)frame_data;
    // Fill frame_data->data/frame_data->length/pts... according to your capture pipeline.
    return -1;
}

static void release_frame_cb(void *user_data, video_record_frame_data_t *frame_data)
{
    (void)user_data;
    (void)frame_data;
    // Release or return the frame buffer to the pool.
}

static int get_audio_cb(void *user_data, video_record_audio_data_t *audio_data)
{
    (void)user_data;
    (void)audio_data;
    // Fill audio_data->data/audio_data->length/pts... according to your audio pipeline.
    return -1;
}

static void release_audio_cb(void *user_data, video_record_audio_data_t *audio_data)
{
    (void)user_data;
    (void)audio_data;
    // Release or return the audio buffer to the pool.
}

avdk_err_t video_file_record_example(void)
{
    bk_video_record_handle_t record = NULL;
    bk_video_record_config_t cfg = {0};
    avdk_err_t ret = AVDK_ERR_OK;

    cfg.record_type = VIDEO_RECORD_TYPE_AVI;
    cfg.record_format = VIDEO_RECORD_FORMAT_MJPEG;
    cfg.video_width = 480;
    cfg.video_height = 320;
    cfg.audio_channels = 1;
    cfg.audio_rate = 16000;
    cfg.audio_bits = 16;
    cfg.audio_format = VIDEO_RECORD_AUDIO_FORMAT_PCM;
    cfg.get_frame_cb = get_frame_cb;
    cfg.get_audio_cb = get_audio_cb;
    cfg.release_frame_cb = release_frame_cb;
    cfg.release_audio_cb = release_audio_cb;
    cfg.user_data = NULL;

    ret = bk_video_recorder_new(&record, &cfg);
    if (ret != AVDK_ERR_OK) {
        return ret;
    }

    ret = bk_video_recorder_open(record);
    if (ret != AVDK_ERR_OK) {
        bk_video_recorder_delete(record);
        return ret;
    }

    ret = bk_video_recorder_start(record, "/sd0/record.avi", VIDEO_RECORD_TYPE_AVI);
    if (ret != AVDK_ERR_OK) {
        bk_video_recorder_close(record);
        bk_video_recorder_delete(record);
        return ret;
    }

    // Recording is running. Stop it when needed.
    // If using mp4lib/avilib directly, update real fps before closing.
    // Example (AVI):
    // uint32_t duration_ms = ...; // actual recording duration in ms
    // AVI_update_video_frame_rate_by_duration(avi, duration_ms);
    ret = bk_video_recorder_stop(record);
    if (ret != AVDK_ERR_OK) {
        // Best-effort cleanup.
    }

    bk_video_recorder_close(record);
    bk_video_recorder_delete(record);
    return AVDK_ERR_OK;
}
```
