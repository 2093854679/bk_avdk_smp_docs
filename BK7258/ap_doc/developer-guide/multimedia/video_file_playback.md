---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/multimedia/video_file_playback.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 视频文件播放

<a id="id2"></a>

## 1、概述

本节介绍 BK7258 平台上“视频文件播放（Video Player）”的使用方式，包括支持的容器/编码格式、关键配置项、典型播放链路，以及示例工程的使用说明。

- 有关视频文件播放的示例工程，请参阅：

  - [Video Player 示例工程](../../examples/projects/video_player_example.md)
- 有关 Video Player 的 API 参考，请参阅：

  - [Video Player API](../../api-reference/multimedia/bk_video_player.md)

播放器主要提供两类接口：

- **Engine 接口**：面向单文件播放控制（播放/停止/暂停/seek/快进快退等）
- **Playlist 接口**：在 Engine 的基础上提供播放列表、切歌与 EOF 策略等能力

<a id="id3"></a>

## 2、支持的功能

- **容器格式**：AVI、MP4（按 Kconfig 选择对应 parser）
- **视频格式**：MJPEG、H264（按解码器支持情况）
- **音频格式**：PCM、AAC 等（按解码器支持情况）
- **播放控制**：play/stop/pause/resume、seek、快进快退、音量/静音（需上层提供控制回调）
- **信息查询**：获取媒体信息（时长、文件大小、音视频参数等）

<a id="id4"></a>

## 3、相关头文件

- `ap/include/components/bk_video_player/bk_video_player_engine.h`
- `ap/include/components/bk_video_player/bk_video_player_playlist.h`
- `ap/include/components/bk_video_player/bk_video_player_types.h`

<a id="kconfig"></a>

## 4、配置选项（Kconfig）

播放器 Kconfig 位于：

- `ap/components/bk_video_player/Kconfig`

常用配置项（部分）：

- **CONFIG\_AVI\_PLAYER**：使能播放器组件
- **CONFIG\_BK\_VIDEO\_PLAYER\_ENABLE\_AVI\_PARSER**：使能 AVI 容器解析
- **CONFIG\_BK\_VIDEO\_PLAYER\_ENABLE\_MP4\_PARSER**：使能 MP4 容器解析
- **CONFIG\_BK\_VIDEO\_PLAYER\_ENABLE\_AAC\_DECODER**：使能 AAC 音频解码
- **CONFIG\_BK\_VIDEO\_PLAYER\_ENABLE\_HW\_JPEG\_DECODER**：使能硬件 JPEG（MJPEG）视频解码
- **CONFIG\_BK\_VIDEO\_PLAYER\_ENABLE\_SW\_JPEG\_DECODER**：使能软件 JPEG（MJPEG）视频解码

线程与栈大小（默认值见 Kconfig）：

- **CONFIG\_BK\_VIDEO\_PLAYER\_VIDEO\_PARSE\_THREAD\_STACK\_SIZE** （vp\_video\_parse）
- **CONFIG\_BK\_VIDEO\_PLAYER\_AUDIO\_PARSE\_THREAD\_STACK\_SIZE** （vp\_audio\_parse）
- **CONFIG\_BK\_VIDEO\_PLAYER\_VIDEO\_DECODE\_THREAD\_STACK\_SIZE** （video\_decode）
- **CONFIG\_BK\_VIDEO\_PLAYER\_AUDIO\_DECODE\_THREAD\_STACK\_SIZE** （audio\_decode）
- **CONFIG\_BK\_VIDEO\_PLAYER\_EVENT\_THREAD\_STACK\_SIZE** （vp\_evt）

备注

播放链路包含解复用、解码、显示/音频输出等模块，建议使用 PSRAM 并预留足够 heap。若出现卡顿/花屏/音画不同步，可从降低分辨率、减少 pipeline buffer 数量、调大关键线程栈、降低日志等级等方向排查。

<a id="id5"></a>

## 5、典型播放链路

播放器的典型链路如下：

<a id="id7"></a>
[![Video player pipeline](../../../../../_assets/39b5e9c7ae4dadded3bf-video_player.png)](../../../../../_assets/39b5e9c7ae4dadded3bf-video_player.png)


视频文件播放典型链路（Video Player pipeline）

- **Container parser**：从文件中读取音视频包（encoded packets）
- **Decoder**：将 encoded packets 解码为音频 PCM 或视频帧
- **Output**：
  \- 视频：上层在 `video.decode_complete_cb` 中拿到解码输出并显示（LCD/OSD 等）
  \- 音频：上层在 `audio.decode_complete_cb` 中拿到解码输出并送入音频输出链路

上层需要提供必要的 buffer 分配/释放回调，以便播放器在不同阶段申请与回收 buffer。

<a id="api-engine"></a>

## 6、API 使用流程（Engine）

Engine 接口的典型流程如下：

1. 准备 `bk_video_player_config_t`，填入：
   \- 音频/视频 pipeline buffer 数量
   \- 音频/视频 buffer 分配与释放回调
   \- 解码完成回调（decode\_complete\_cb）
   \- 可选：音量/静音控制回调、播放完成回调等
2. `bk_video_player_engine_new()` 创建实例
3. 注册 parser/decoder：`bk_video_player_engine_register_*()`
   \- 必须在 `play` 前完成注册，否则播放器内部没有可用的容器解析器/解码器，无法解析媒体并完成播放。
   \- 媒体解析（如 `get_media_info` / CLI 的 `info`）同样依赖已注册的容器解析器；未注册解析器时将无法完成文件探测与解析。
4. `bk_video_player_engine_open()`
5. `bk_video_player_engine_set_file_path()`
6. `bk_video_player_engine_play()`
7. `bk_video_player_engine_stop()` / `bk_video_player_engine_set_pause()` / `bk_video_player_engine_seek()` 等控制
8. `bk_video_player_engine_close()`
9. `bk_video_player_engine_delete()`

重要

- `bk_video_player_engine_set_volume()` 依赖上层提供 `audio_set_volume_cb`，否则会返回不支持错误码。
- 播放完成回调是异步触发，回调中不建议做长时间阻塞操作。

<a id="api-playlist"></a>

## 7、API 使用流程（Playlist）

Playlist 接口在 Engine 基础上增加了播放列表与播放模式（play mode）：

1. `bk_video_player_playlist_new()` 创建实例
2. `bk_video_player_playlist_open()`
3. 通过 `bk_video_player_playlist_add_file()` 添加播放列表
4. 使用 `bk_video_player_playlist_play_file()` / `play_next()` / `play_prev()` 等控制播放
5. `bk_video_player_playlist_set_play_mode()` 配置播放模式（stop/repeat/loop）
6. `bk_video_player_playlist_close()` \+ `bk_video_player_playlist_delete()`

<a id="id6"></a>

## 8、示例工程

示例工程路径：

- `projects/video_player_example`

该示例提供 `video_play_engine` 与 `video_play_playlist` CLI 命令，用于验证播放器链路。

<a id="engine"></a>

## 9、使用示例（Engine）

以下示例仅展示 Engine 的基本调用顺序。实际工程中通常需要结合显示与音频输出模块实现回调。

```
#include "components/bk_video_player/bk_video_player_engine.h"
#include "bk_video_player_mp4_parser.h"
#include "bk_video_player_avi_parser.h"
#include "bk_video_player_hw_jpeg_decoder.h"
#include "bk_video_player_sw_jpeg_decoder.h"
#include "bk_video_player_aac_decoder.h"

static avdk_err_t audio_buf_alloc(void *user_data, video_player_buffer_t *buffer)
{
    (void)user_data;
    if (buffer == NULL) {
        return AVDK_ERR_INVALID_PARAM;
    }
    buffer->data = os_malloc(buffer->length);
    if (buffer->data == NULL) {
        return AVDK_ERR_NO_MEMORY;
    }
    return AVDK_ERR_OK;
}

static void audio_buf_free(void *user_data, video_player_buffer_t *buffer)
{
    (void)user_data;
    if (buffer && buffer->data) {
        os_free(buffer->data);
        buffer->data = NULL;
    }
}

static avdk_err_t video_buf_alloc(void *user_data, video_player_buffer_t *buffer)
{
    (void)user_data;
    if (buffer == NULL) {
        return AVDK_ERR_INVALID_PARAM;
    }
    buffer->data = os_malloc(buffer->length);
    if (buffer->data == NULL) {
        return AVDK_ERR_NO_MEMORY;
    }
    return AVDK_ERR_OK;
}

static void video_buf_free(void *user_data, video_player_buffer_t *buffer)
{
    (void)user_data;
    if (buffer && buffer->data) {
        os_free(buffer->data);
        buffer->data = NULL;
    }
}

static void on_audio_decoded(void *user_data, const video_player_audio_packet_meta_t *meta, video_player_buffer_t *buffer)
{
    (void)user_data;
    (void)meta;
    // Send decoded PCM to audio output, then free the buffer.
    audio_buf_free(NULL, buffer);
}

static void on_video_decoded(void *user_data, const video_player_video_frame_meta_t *meta, video_player_buffer_t *buffer)
{
    (void)user_data;
    (void)meta;
    // Display the decoded frame, then free the buffer.
    video_buf_free(NULL, buffer);
}

avdk_err_t video_file_playback_example(void)
{
    bk_video_player_engine_handle_t engine = NULL;
    bk_video_player_config_t cfg = {0};
    avdk_err_t ret = AVDK_ERR_OK;

    cfg.user_data = NULL;

    cfg.audio.parser_to_decode_buffer_count = 4;
    cfg.audio.decode_to_output_buffer_count = 4;
    cfg.audio.buffer_alloc_cb = audio_buf_alloc;
    cfg.audio.buffer_free_cb = audio_buf_free;
    cfg.audio.decode_complete_cb = on_audio_decoded;

    cfg.video.parser_to_decode_buffer_count = 4;
    cfg.video.decode_to_output_buffer_count = 4;
    cfg.video.buffer_alloc_cb = video_buf_alloc;
    cfg.video.buffer_free_cb = video_buf_free;
    cfg.video.decode_complete_cb = on_video_decoded;
    cfg.video.output_format = PIXEL_FMT_YUYV;

    ret = bk_video_player_engine_new(&engine, &cfg);
    if (ret != AVDK_ERR_OK) {
        return ret;
    }

    // Register parsers/decoders before media probing (info/get_media_info) or playback.
#if CONFIG_BK_VIDEO_PLAYER_ENABLE_MP4_PARSER
    ret = bk_video_player_engine_register_container_parser(engine, bk_video_player_get_mp4_parser_ops());
    if (ret != AVDK_ERR_OK) {
        bk_video_player_engine_delete(engine);
        return ret;
    }
#endif
#if CONFIG_BK_VIDEO_PLAYER_ENABLE_AVI_PARSER
    ret = bk_video_player_engine_register_container_parser(engine, bk_video_player_get_avi_parser_ops());
    if (ret != AVDK_ERR_OK) {
        bk_video_player_engine_delete(engine);
        return ret;
    }
#endif
#if CONFIG_BK_VIDEO_PLAYER_ENABLE_HW_JPEG_DECODER
    ret = bk_video_player_engine_register_video_decoder(engine, bk_video_player_get_hw_jpeg_decoder_ops());
    if (ret != AVDK_ERR_OK) {
        bk_video_player_engine_delete(engine);
        return ret;
    }
#endif
#if CONFIG_BK_VIDEO_PLAYER_ENABLE_SW_JPEG_DECODER
    ret = bk_video_player_engine_register_video_decoder(engine, bk_video_player_get_sw_jpeg_decoder_ops());
    if (ret != AVDK_ERR_OK) {
        bk_video_player_engine_delete(engine);
        return ret;
    }
#endif
#if CONFIG_BK_VIDEO_PLAYER_ENABLE_AAC_DECODER
    ret = bk_video_player_engine_register_audio_decoder(engine, bk_video_player_get_aac_audio_decoder_ops());
    if (ret != AVDK_ERR_OK) {
        bk_video_player_engine_delete(engine);
        return ret;
    }
#endif

    ret = bk_video_player_engine_open(engine);
    if (ret != AVDK_ERR_OK) {
        bk_video_player_engine_delete(engine);
        return ret;
    }

    ret = bk_video_player_engine_set_file_path(engine, "/sd0/record.mp4");
    if (ret == AVDK_ERR_OK) {
        ret = bk_video_player_engine_play(engine);
    }

    // Stop playback when needed.
    if (ret == AVDK_ERR_OK) {
        (void)bk_video_player_engine_stop(engine);
    }

    (void)bk_video_player_engine_close(engine);
    (void)bk_video_player_engine_delete(engine);
    return ret;
}
```
