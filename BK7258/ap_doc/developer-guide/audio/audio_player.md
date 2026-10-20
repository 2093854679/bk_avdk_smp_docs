---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/audio/audio_player/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# **音频播放器**

<a id="id2"></a>

## **1\. 简介**

> 音频播放器组件是针对FreeRTOS系统设计实现的轻量级音频播放器。
>
> 支持播放列表管理，可以添加、删除音频文件，支持播放列表的清空操作。
>
> 支持多种播放模式，如：单曲播放、顺序播放、单曲循环、列表循环、随机播放等。
>
> 支持丰富的播放控制功能，如：播放、停止、暂停、恢复、上一首、下一首、跳转等。
>
> 支持音量调节功能，音量范围为0-100。
>
> 支持事件回调机制，可以通过注册事件回调函数，获取播放器的状态变化，如：歌曲开始、歌曲完成、歌曲失败、暂停、恢复、播放进度更新等。
>
> 支持播放本地 VFS 文件系统中的音频文件，也支持播放网络音频流。
>
> 媒体元数据解析器、解码器、输入源、输出源均通过注册方式由客户按需添加；内置插件涵盖常见格式（如 MP3、WAV、AAC、OPUS、M4A、M3U8、TS）及文件源、网络源、HLS 源、板载扬声器输出、文件输出等，客户也可实现自定义插件并注册。

- 有关音频播放器的API参考，请参阅：

  - [音频播放器API参考](../../api-reference/audio/audio_player.md)
- 有关音频播放器的示例工程，请参阅：

  - [音频播放器示例工程](../../examples/projects/audio_player_example.md)

重要

1. 此音频播放器和播放器服务组件是独立的两个组件，互不依赖，播放器服务组件主要用于播放提示音，不支持播放多种类型的音乐及播放列表管理。
2. 音频播放器适配的是VFS文件系统，内部不会执行文件系统的挂载和卸载操作，播放本地音乐文件时前需要客户先挂载文件系统。

<a id="id4"></a>

## **2\. 宏配置**

> 基本功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_AUDIO\_PLAYER | AP | bool | y |
>
> 内存配置（二选一）：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_AUDIO\_PLAYER\_USE\_SRAM | AP | bool | y/n |
> | CONFIG\_AUDIO\_PLAYER\_USE\_PSRAM | AP | bool | y/n |

备注

1. 宏配置中 value 含义： `y` 表示必须打开， `y/n` 表示根据实际需求选择是否开启。
2. 内存配置必须二选一：使用 `CONFIG_AUDIO_PLAYER_USE_SRAM` 或 `CONFIG_AUDIO_PLAYER_USE_PSRAM`，PSRAM 配置依赖于 `CONFIG_PSRAM`。

<a id="id5"></a>

## **3\. 内置插件**

> 组件已提供以下内置插件，客户可通过对应的插件头文件中的接口 `bk_audio_player_get_*_ops()` 获取操作表，再调用 `bk_audio_player_register_*` 注册到播放器实例。
>
> 元数据解析器（用于 `bk_audio_player_register_metadata_parser`）：
>
> | 格式 | 获取操作表接口 |
> | --- | --- |
> | AAC | `bk_audio_player_get_aac_metadata_parser_ops()` |
> | AMR | `bk_audio_player_get_amr_metadata_parser_ops()` |
> | FLAC | `bk_audio_player_get_flac_metadata_parser_ops()` |
> | M4A | `bk_audio_player_get_m4a_metadata_parser_ops()` |
> | MP3 | `bk_audio_player_get_mp3_metadata_parser_ops()` |
> | OGG | `bk_audio_player_get_ogg_metadata_parser_ops()` |
> | Opus | `bk_audio_player_get_opus_metadata_parser_ops()` |
> | WAV | `bk_audio_player_get_wav_metadata_parser_ops()` |
>
> 解码器（用于 `bk_audio_player_register_decoder`）：
>
> | 格式 | 获取操作表接口 |
> | --- | --- |
> | AAC | `bk_audio_player_get_aac_decoder_ops()` |
> | AMR | `bk_audio_player_get_amr_decoder_ops()` |
> | FLAC | `bk_audio_player_get_flac_decoder_ops()` |
> | M4A | `bk_audio_player_get_m4a_decoder_ops()` |
> | MP3 | `bk_audio_player_get_mp3_decoder_ops()` |
> | OGG | `bk_audio_player_get_ogg_decoder_ops()` |
> | Opus | `bk_audio_player_get_opus_decoder_ops()` |
> | MPEG-TS | `bk_audio_player_get_ts_decoder_ops()` |
> | WAV | `bk_audio_player_get_wav_decoder_ops()` |
>
> 输入源（用于 `bk_audio_player_register_source`）：
>
> | 类型 | 获取操作表接口 |
> | --- | --- |
> | 本地文件 | `bk_audio_player_get_file_source_ops()` |
> | HLS 流 | `bk_audio_player_get_hls_source_ops()` |
> | 网络源 | `bk_audio_player_get_net_source_ops()` |

重要

1. **本地文件**：依赖 VFS，需开 `CONFIG_VFS`。
2. **HLS 流** 和 **网络源**：依赖网络客户端，需开 `CONFIG_WEBCLIENT`。

> 输出源（用于 `bk_audio_player_register_sink`）：
>
> | 类型 | 获取操作表接口 |
> | --- | --- |
> | 文件输出 | `bk_audio_player_get_file_sink_ops()` |
> | 板载扬声器 | `bk_audio_player_get_onboard_speaker_sink_ops()` |

重要

1. **文件输出**：依赖 VFS，需开 `CONFIG_VFS`。
2. **板载扬声器**：依赖 ADK 原始流与板载扬声器流，需开 `CONFIG_ADK_RAW_STREAM`、`CONFIG_ADK_ONBOARD_SPEAKER_STREAM`。
3. PA的控制需要在输出源实现中自行适配（例如在板载扬声器 sink 或自定义 sink 内控制 PA 使能/静音引脚）。
4. 默认提供的板载扬声器 sink 未打开 PA 控制，如需支持 PA 控制，需要客户自行修改适配，（此sink是基于onboard\_speaker\_stream实现的, `onboard_speaker_stream_cfg_t` 提供了PA控制相关的配置项）。

<a id="id6"></a>

## **4\. 使用示例**

> 以典型的应用场景：播放SD卡中的音频文件列表为示例说明音频播放器组件使用流程。

<a id="id7"></a>

### 初始化音频播放器

初始化音频播放器的流程如下：
:   1. 定义事件回调函数，用于处理播放器的状态变化事件。
    2. 创建播放器实例，传入配置（含事件回调等）。
    3. 按需注册元数据解析器、解码器、输入源、输出源（使用内置插件或自定义实现）。
    4. 设置播放模式（可选）。
    5. 设置音量（可选）。

以下为代码示例

```
/* 1. 定义事件回调函数 */
void player_event_handler(audio_player_event_type_t event, void *extra_info, void *args)
{
    switch (event)
    {
        case AUDIO_PLAYER_EVENT_SONG_START:
            LOGI("Song start playing\n");
            break;
        case AUDIO_PLAYER_EVENT_SONG_FINISH:
            LOGI("Song finish playing\n");
            break;
        case AUDIO_PLAYER_EVENT_SONG_FAILURE:
            LOGE("Song play failure\n");
            break;
        case AUDIO_PLAYER_EVENT_SONG_PAUSE:
            LOGI("Song paused\n");
            break;
        case AUDIO_PLAYER_EVENT_SONG_RESUME:
            LOGI("Song resumed\n");
            break;
        case AUDIO_PLAYER_EVENT_SONG_TICK:
            // Handle playback progress update
            break;
        case AUDIO_PLAYER_EVENT_SEEK_COMPLETE:
        {
            audio_player_seek_result_t *result = (audio_player_seek_result_t *)extra_info;
            if (result && result->status == AUDIO_PLAYER_OK)
            {
                LOGI("Seek success, target=%d\n", result->second);
            }
            else
            {
                LOGE("Seek failed\n");
            }
            break;
        }
        default:
            break;
    }
}

/* 2. 创建播放器实例，获取 handle */
bk_audio_player_handle_t player_handle = NULL;
bk_audio_player_cfg_t cfg = DEFAULT_AUDIO_PLAYER_CONFIG();
cfg.event_handler = player_event_handler;
cfg.args = NULL;  /* 用户自定义参数，可以为NULL */

int ret = bk_audio_player_new(&player_handle, &cfg);
if (ret != AUDIO_PLAYER_OK || player_handle == NULL)
{
    LOGE("audio player new fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 3. 按需注册插件：元数据解析器、解码器、输入源、输出源（本示例以播放本地 MP3/WAV 并输出到板载扬声器为例） */
ret = bk_audio_player_register_metadata_parser(player_handle, bk_audio_player_get_mp3_metadata_parser_ops());
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("register mp3 metadata parser fail\n");
    return BK_FAIL;
}

ret = bk_audio_player_register_metadata_parser(player_handle, bk_audio_player_get_wav_metadata_parser_ops());
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("register wav metadata parser fail\n");
    return BK_FAIL;
}

ret = bk_audio_player_register_decoder(player_handle, bk_audio_player_get_mp3_decoder_ops());
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("register mp3 decoder fail\n");
    return BK_FAIL;
}

ret = bk_audio_player_register_decoder(player_handle, bk_audio_player_get_wav_decoder_ops());
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("register wav decoder fail\n");
    return BK_FAIL;
}

ret = bk_audio_player_register_source(player_handle, bk_audio_player_get_file_source_ops());
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("register file source fail\n");
    return BK_FAIL;
}

ret = bk_audio_player_register_sink(player_handle, bk_audio_player_get_onboard_speaker_sink_ops());
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("register onboard speaker sink fail\n");
    return BK_FAIL;
}

/* 4. 设置播放模式（可选） */
ret = bk_audio_player_set_play_mode(player_handle, AUDIO_PLAYER_MODE_SEQUENCE_LOOP);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("set play mode fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 5. 设置音量（可选） */
ret = bk_audio_player_set_volume(player_handle, 80);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("set volume fail, ret=%d\n", ret);
    return BK_FAIL;
}
```

备注

1. `AUDIO_PLAYER_EVENT_SEEK_COMPLETE` 事件的 `extra_info` 指向 `audio_player_seek_result_t`，可通过其中的 `second` 与 `status` 判断定位结果。
2. 其他事件的 `extra_info` 视具体实现可能为 `NULL`，使用前请做好判空。
3. 插件注册：上述示例仅注册了 MP3/WAV 的元数据解析器与解码器、文件源、板载扬声器输出，若需播放其他输入源、输出源、格式的数据，可再注册相应的插件。

<a id="id8"></a>

### 添加音频文件到播放列表

详细流程如下：
:   1. 调用添加音乐接口，将音频文件添加到播放列表。
    2. 可以多次调用添加接口，添加多个音频文件。

以下为代码示例

```
/* 添加音频文件到播放列表 */
ret = bk_audio_player_add_music(player_handle, "song1", "/sd0/music/song1.mp3");
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("add music fail, ret=%d\n", ret);
    return BK_FAIL;
}

ret = bk_audio_player_add_music(player_handle, "song2", "/sd0/music/song2.wav");
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("add music fail, ret=%d\n", ret);
    return BK_FAIL;
}

ret = bk_audio_player_add_music(player_handle, "song3", "/sd0/music/song3.mp3");
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("add music fail, ret=%d\n", ret);
    return BK_FAIL;
}
```

备注

1. 音频文件路径支持VFS文件系统路径，如SD卡路径、Flash文件系统路径等。
2. 音频文件名称由用户自定义，用于标识播放列表中的音频文件。

<a id="id9"></a>

### 开始播放

详细流程如下：
:   1. 调用播放接口，开始播放播放列表中的音频文件。
    2. 播放器会根据当前设置的播放模式进行播放。

以下为代码示例

```
/* 开始播放 */
ret = bk_audio_player_start(player_handle);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("player start fail, ret=%d\n", ret);
    return BK_FAIL;
}
```

<a id="id10"></a>

### 播放控制

播放器提供了丰富的播放控制功能：

以下为代码示例

```
/* 暂停播放 */
ret = bk_audio_player_pause(player_handle);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("player pause fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 恢复播放 */
ret = bk_audio_player_resume(player_handle);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("player resume fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 播放上一首 */
ret = bk_audio_player_prev(player_handle);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("player prev fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 播放下一首 */
ret = bk_audio_player_next(player_handle);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("player next fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 跳转到指定歌曲（例如跳转到第2首，索引从0开始） */
ret = bk_audio_player_jumpto(player_handle, 1);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("player jumpto fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 定位到当前歌曲的第60秒（仅本地文件支持） */
ret = bk_audio_player_seek(player_handle, 60);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("player seek fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 停止播放 */
ret = bk_audio_player_stop(player_handle);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("player stop fail, ret=%d\n", ret);
    return BK_FAIL;
}
```

备注

1. `bk_audio_player_seek` 仅支持本地音频文件，对网络流或 HLS 源会返回错误。
2. 定位操作为异步执行，完成后会触发 `AUDIO_PLAYER_EVENT_SEEK_COMPLETE`，可通过 `audio_player_seek_result_t` 判断结果。

<a id="id11"></a>

### 播放列表管理

播放器支持动态管理播放列表：

以下为代码示例

```
/* 通过名称删除音乐 */
ret = bk_audio_player_del_music_by_name(player_handle, "song1");
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("delete music by name fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 通过URI删除音乐 */
ret = bk_audio_player_del_music_by_uri(player_handle, "/sd0/music/song2.wav");
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("delete music by uri fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 清空播放列表 */
ret = bk_audio_player_clear_music_list(player_handle);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("clear music list fail, ret=%d\n", ret);
    return BK_FAIL;
}
```

备注

1. 删除正在播放的歌曲会自动切换到下一首歌曲。
2. 清空播放列表会停止当前的播放。

<a id="id12"></a>

### 提取音频元数据

> 在播放前可以通过 `bk_audio_player_get_metadata_from_file()` 获取音频文件的基础信息（标题、艺术家、比特率、时长等），便于在 UI 或业务流程中展示。使用当前实例已注册的元数据解析器解析文件。

以下为代码示例

```
audio_metadata_t metadata;
memset(&metadata, 0, sizeof(metadata));

if (bk_audio_player_get_metadata_from_file(player_handle, "/sd0/music/song1.mp3", &metadata) == 0)
{
    LOGI("title=%s, artist=%s, duration=%.1fs\n",
         metadata.title, metadata.artist, metadata.duration);
}
else
{
    LOGE("parse metadata fail\n");
}
```

备注

1. 该接口只支持本地文件路径（VFS 文件系统），不支持网络流或 HTTP URI。
2. 返回值为0表示成功，-1/-2/-3/-4分别表示打开失败、格式不支持、参数无效与读文件失败。

<a id="id13"></a>

### 音量调节

播放器支持音量调节功能：

以下为代码示例

```
/* 设置音量为50 */
ret = bk_audio_player_set_volume(player_handle, 50);
if (ret != AUDIO_PLAYER_OK)
{
    LOGE("set volume fail, ret=%d\n", ret);
    return BK_FAIL;
}

/* 获取当前音量 */
int volume = bk_audio_player_get_volume(player_handle);
LOGI("current volume: %d\n", volume);
```

备注

1. 音量范围为0-100，0表示静音，100表示最大音量。

<a id="id14"></a>

### 去初始化音频播放器

去初始化音频播放器的流程如下：
:   1. 停止播放（如果正在播放）。
    2. 调用去初始化接口，释放播放器资源。

以下为代码示例

```
/* 1. 停止播放（如果正在播放） */
bk_audio_player_stop(player_handle);

/* 2. 销毁播放器实例 */
bk_audio_player_delete(player_handle);
player_handle = NULL;
```
