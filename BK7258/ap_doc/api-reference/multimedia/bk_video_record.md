---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_video_record.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="api"></a>

# 视频文件录制 API

<a id="id1"></a>

## 概述

本节介绍视频文件录制（Video Record）的 API 与核心数据结构。录制模块通过上层回调获取视频帧与音频数据，并封装为 AVI/MP4 文件写入存储介质。

- 有关 Video Record 的详细信息，请参阅：

  - [视频文件录制指南](../../developer-guide/multimedia/video_file_recording.md)
- 有关 Video Record 的示例工程，请参阅：

  - [Video Record 示例工程](../../examples/projects/video_player_example.md)

<a id="id3"></a>

## 相关头文件

- `ap/include/components/bk_video_recorder.h`
- `ap/include/components/bk_video_recorder_types.h`

<a id="id4"></a>

## API 参考

1. **bk\_video\_recorder\_new**

创建录制实例。

```
avdk_err_t bk_video_recorder_new(bk_video_record_handle_t *handle, bk_video_record_config_t *config);
```

- 参数:
  \- handle: \[输出\] 录制器句柄
  \- config: \[输入\] 录制配置（格式参数与回调等）
- 返回值:
  \- AVDK\_ERR\_OK: 成功
  \- 其他: 失败

2. **bk\_video\_recorder\_open / bk\_video\_recorder\_close**

打开/关闭录制器。

```
avdk_err_t bk_video_recorder_open(bk_video_record_handle_t handler);
avdk_err_t bk_video_recorder_close(bk_video_record_handle_t handler);
```

3. **bk\_video\_recorder\_start / bk\_video\_recorder\_stop**

开始/停止录制。

```
avdk_err_t bk_video_recorder_start(bk_video_record_handle_t handler, char *file_path, uint32_t record_type);
avdk_err_t bk_video_recorder_stop(bk_video_record_handle_t handler);
```

- 参数（start）:
  \- file\_path: 输出文件路径（由上层提供，需为有效可写路径）
  \- record\_type: 容器类型（如 `VIDEO_RECORD_TYPE_AVI` / `VIDEO_RECORD_TYPE_MP4`）

重要

若直接使用 `mp4lib` / `avilib` 进行录制（非 `bk_video_recorder` 模块），请在调用 `MP4_close()` / `AVI_close()` 前传入实际录制时长（毫秒）以修正帧率：

- `MP4_update_video_frame_rate_by_duration(mp4, duration_ms)`
- `AVI_update_video_frame_rate_by_duration(avi, duration_ms)`

4. **bk\_video\_recorder\_ioctl**

扩展控制接口。

```
avdk_err_t bk_video_recorder_ioctl(bk_video_record_handle_t handler, bk_video_record_ioctl_cmd_t cmd, void *param);
```

5. **bk\_video\_recorder\_delete**

删除录制实例并释放资源。

```
avdk_err_t bk_video_recorder_delete(bk_video_record_handle_t handler);
```

<a id="id5"></a>

## API 类型定义（节选）

1. **record\_type（容器类型）**

```
#define VIDEO_RECORD_TYPE_AVI    0
#define VIDEO_RECORD_TYPE_MP4    1
```

2. **record\_format（视频格式）**

```
#define VIDEO_RECORD_FORMAT_H264 0
#define VIDEO_RECORD_FORMAT_MJPEG 1
#define VIDEO_RECORD_FORMAT_YUV  2
```

3. **bk\_video\_record\_config\_t**

录制配置结构体（包含音视频参数与数据回调）。

```
typedef struct bk_video_record_config
{
    uint32_t record_type;
    uint32_t record_format;
    uint32_t record_quality;
    uint32_t record_bitrate;
    uint32_t record_framerate;
    uint32_t video_width;
    uint32_t video_height;
    uint32_t audio_channels;
    uint32_t audio_rate;
    uint32_t audio_bits;
    uint32_t audio_format;
    video_record_get_frame_cb_t get_frame_cb;
    video_record_get_audio_cb_t get_audio_cb;
    video_record_release_frame_cb_t release_frame_cb;
    video_record_release_audio_cb_t release_audio_cb;
    void *user_data;
} bk_video_record_config_t;
```

重要

- `get_frame_cb` / `get_audio_cb` 返回的缓冲区在写入完成前必须保持有效。
- 写入完成后，模块会调用 `release_frame_cb` / `release_audio_cb` 归还缓冲区。
- 回调中应避免长时间阻塞，以免影响录制实时性与丢帧概率。
