---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_video_player.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="api"></a>

# 视频文件播放器 API

<a id="id1"></a>

## 概述

本节介绍视频文件播放器（Video Player）的 API 与核心数据结构。播放器支持 AVI/MP4 等容器解析，并支持 MJPEG/H264 等视频流与 PCM/AAC 等音频流（依赖已使能的 parser/decoder）。

- 有关 Video Player 的详细信息，请参阅：

  - [视频文件播放指南](../../developer-guide/multimedia/video_file_playback.md)
- 有关 Video Player 的示例工程，请参阅：

  - [Video Player 示例工程](../../examples/projects/video_player_example.md)

<a id="id3"></a>

## 相关头文件

- `ap/include/components/bk_video_player/bk_video_player_engine.h`
- `ap/include/components/bk_video_player/bk_video_player_playlist.h`
- `ap/include/components/bk_video_player/bk_video_player_types.h`

<a id="api-engine"></a>

## API 参考（Engine）

1. **bk\_video\_player\_engine\_new**

创建播放器 Engine 实例。

```
avdk_err_t bk_video_player_engine_new(bk_video_player_engine_handle_t *handle, bk_video_player_config_t *config);
```

- 参数:
  \- handle: \[输出\] Engine 句柄
  \- config: \[输入\] 播放器配置（回调、buffer 配置、输出格式等）
- 返回值:
  \- AVDK\_ERR\_OK: 成功
  \- 其他: 失败

2. **bk\_video\_player\_engine\_delete**

删除 Engine 实例并释放资源。

```
avdk_err_t bk_video_player_engine_delete(bk_video_player_engine_handle_t handle);
```

3. **bk\_video\_player\_engine\_open / bk\_video\_player\_engine\_close**

打开/关闭 Engine。

```
avdk_err_t bk_video_player_engine_open(bk_video_player_engine_handle_t handle);
avdk_err_t bk_video_player_engine_close(bk_video_player_engine_handle_t handle);
```

4. **bk\_video\_player\_engine\_set\_file\_path**

设置媒体文件路径（在 play 之前调用）。

```
avdk_err_t bk_video_player_engine_set_file_path(bk_video_player_engine_handle_t handle, const char *file_path);
```

5. **bk\_video\_player\_engine\_play / bk\_video\_player\_engine\_stop**

开始/停止播放。

```
avdk_err_t bk_video_player_engine_play(bk_video_player_engine_handle_t handle);
avdk_err_t bk_video_player_engine_stop(bk_video_player_engine_handle_t handle);
```

6. **bk\_video\_player\_engine\_set\_pause**

设置暂停状态。

```
avdk_err_t bk_video_player_engine_set_pause(bk_video_player_engine_handle_t handle, bool pause);
```

7. **bk\_video\_player\_engine\_seek**

跳转到指定时间（毫秒）。

```
avdk_err_t bk_video_player_engine_seek(bk_video_player_engine_handle_t handle, uint64_t time_ms);
```

8. **bk\_video\_player\_engine\_fast\_forward / bk\_video\_player\_engine\_rewind**

快进/快退（按指定时长跳转，毫秒）。

```
avdk_err_t bk_video_player_engine_fast_forward(bk_video_player_engine_handle_t handle, uint32_t time_ms);
avdk_err_t bk_video_player_engine_rewind(bk_video_player_engine_handle_t handle, uint32_t time_ms);
```

9. **bk\_video\_player\_engine\_play\_file**

从头播放指定文件（内部执行 stop -\> set\_file\_path -\> play 的常用序列）。

```
avdk_err_t bk_video_player_engine_play_file(bk_video_player_engine_handle_t handle, const char *file_path);
```

10. **bk\_video\_player\_engine\_set\_volume / volume\_up / volume\_down**

设置/调整音量（0-100）。

```
avdk_err_t bk_video_player_engine_set_volume(bk_video_player_engine_handle_t handle, uint8_t volume);
avdk_err_t bk_video_player_engine_volume_up(bk_video_player_engine_handle_t handle, uint8_t step);
avdk_err_t bk_video_player_engine_volume_down(bk_video_player_engine_handle_t handle, uint8_t step);
```

备注

上述音量接口依赖 `bk_video_player_config_t.audio.audio_set_volume_cb`。若未提供，将返回不支持错误码。

11. **bk\_video\_player\_engine\_set\_mute**

设置静音状态。

```
avdk_err_t bk_video_player_engine_set_mute(bk_video_player_engine_handle_t handle, bool mute);
```

12. **bk\_video\_player\_engine\_register\_\*（decoder/parser 注册）**

注册音频解码器、视频解码器、容器解析器。

```
avdk_err_t bk_video_player_engine_register_audio_decoder(bk_video_player_engine_handle_t handle,
                                                         const video_player_audio_decoder_ops_t *decoder_ops);
avdk_err_t bk_video_player_engine_register_video_decoder(bk_video_player_engine_handle_t handle,
                                                         video_player_video_decoder_ops_t *decoder_ops);
avdk_err_t bk_video_player_engine_register_container_parser(bk_video_player_engine_handle_t handle,
                                                            video_player_container_parser_ops_t *parser_ops);
```

13. **bk\_video\_player\_engine\_get\_current\_time / get\_status / get\_media\_info**

查询当前播放时间、播放状态与媒体信息。

```
avdk_err_t bk_video_player_engine_get_current_time(bk_video_player_engine_handle_t handle, uint64_t *time_ms);
avdk_err_t bk_video_player_engine_get_status(bk_video_player_engine_handle_t handle, video_player_status_t *status);
avdk_err_t bk_video_player_engine_get_media_info(bk_video_player_engine_handle_t handle,
                                                 const char *file_path,
                                                 video_player_media_info_t *media_info);
```

备注

`get_media_info` 的 `file_path` 传 NULL 时，查询当前已打开文件（缓存）的媒体信息。

重要

`get_media_info` 的文件探测/解析依赖已注册的容器解析器（`register_container_parser`）。在未注册解析器的情况下，播放器无法选择合适的解析器来打开文件并解析媒体信息。

<a id="api-playlist"></a>

## API 参考（Playlist）

Playlist API 用于播放列表管理与切歌控制，典型接口如下（原型见头文件）：

- 创建/销毁：`bk_video_player_playlist_new` / `bk_video_player_playlist_delete`
- 打开/关闭：`bk_video_player_playlist_open` / `bk_video_player_playlist_close`
- 列表管理：`add_file` / `remove_file` / `clear` / `get_file_count` / `get_current_file`
- 播放控制：`play_file` / `stop` / `set_pause` / `seek` / `fast_forward` / `rewind`
- 切歌与策略：`play_next` / `play_prev` / `play_at_index` / `set_play_mode`
- 音量与静音：`set_volume` / `volume_up` / `volume_down` / `set_mute`
- 解码器/解析器注册：`register_audio_decoder` / `register_video_decoder` / `register_container_parser`
- 状态查询：`get_current_time` / `get_status` / `get_media_info`

<a id="playlist"></a>

## 播放模式（Playlist）

Playlist 提供播放模式（play mode），用于定义到达文件尾（EOF）后的处理策略：

```
typedef enum
{
    BK_VIDEO_PLAYER_PLAYLIST_PLAY_MODE_STOP = 0, // Stop playback (default)
    BK_VIDEO_PLAYER_PLAYLIST_PLAY_MODE_REPEAT,   // Repeat current file
    BK_VIDEO_PLAYER_PLAYLIST_PLAY_MODE_LOOP,     // Loop playlist (wrap to first when reaching the end)
} bk_video_player_playlist_play_mode_t;

avdk_err_t bk_video_player_playlist_set_play_mode(bk_video_player_playlist_handle_t handle,
                                                  bk_video_player_playlist_play_mode_t mode);
```

<a id="id4"></a>

## API 类型定义（节选）

1. **video\_player\_status\_t**

播放状态枚举。

```
typedef enum
{
    VIDEO_PLAYER_STATUS_NONE = 0,
    VIDEO_PLAYER_STATUS_OPENED,
    VIDEO_PLAYER_STATUS_CLOSED,
    VIDEO_PLAYER_STATUS_PLAYING,
    VIDEO_PLAYER_STATUS_PAUSED,
    VIDEO_PLAYER_STATUS_STOPPED,
    VIDEO_PLAYER_STATUS_FINISHED,
} video_player_status_t;
```

2. **video\_player\_media\_info\_t**

媒体信息（音视频参数 \+ 文件/容器信息）。

```
typedef struct
{
    video_player_video_params_t video;
    video_player_audio_params_t audio;
    uint64_t duration_ms;
    uint64_t file_size_bytes;
} video_player_media_info_t;
```

3. **bk\_video\_player\_config\_t**

播放器配置（包含音频/视频 buffer 配置与回调等）。上层应按实际输出链路实现必要回调，并保证回调快速返回。
