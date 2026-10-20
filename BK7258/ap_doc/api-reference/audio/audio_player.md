---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_player/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="api"></a>

# 音频播放器API

<a id="id1"></a>

## 概述

音频播放器组件提供轻量级的音频播放功能，支持播放列表管理、播放控制、音量调节等功能，并通过事件回调上报播放状态。适用于需要管理多个音频文件播放的应用场景。

- 有关音频播放器的开发指南，请参阅：

  - [音频播放器开发指南](../../developer-guide/audio/audio_player.md)
- 有关音频播放器的示例工程，请参阅：

  - [音频播放器示例工程](../../examples/projects/audio_player_example.md)

<a id="id4"></a>

## API参考

1. **bk\_audio\_player\_new**

创建音频播放器实例。

```
int bk_audio_player_new(bk_audio_player_handle_t *handle, bk_audio_player_cfg_t *cfg);
```

- 参数:
  \- handle: 成功时返回新实例的 handle（输出参数）
  \- cfg: 音频播放器配置，参见 bk\_audio\_player\_cfg\_t 结构体
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_ERR: 失败
  \- AUDIO\_PLAYER\_NO\_MEM: 内存不足
  \- AUDIO\_PLAYER\_INVALID: 参数无效

2. **bk\_audio\_player\_delete**

销毁音频播放器实例并释放资源。

```
int bk_audio_player_delete(bk_audio_player_handle_t handle);
```

- 参数:
  \- handle: 由 bk\_audio\_player\_new 返回的实例 handle
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_INVALID: 参数无效（如 handle 为 NULL）

3. **bk\_audio\_player\_set\_play\_mode**

设置播放模式。

```
int bk_audio_player_set_play_mode(bk_audio_player_handle_t handle, audio_player_mode_t mode);
```

- 参数:
  \- handle: 实例 handle
  \- mode: 播放模式，参见 audio\_player\_mode\_t 枚举
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_INVALID: 参数无效

4. **bk\_audio\_player\_set\_volume**

设置音量。

```
int bk_audio_player_set_volume(bk_audio_player_handle_t handle, int volume);
```

- 参数:
  \- handle: 实例 handle
  \- volume: 音量等级，范围 0-100
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_INVALID: 参数无效

5. **bk\_audio\_player\_get\_volume**

获取当前音量。

```
int bk_audio_player_get_volume(bk_audio_player_handle_t handle);
```

- 参数:
  \- handle: 实例 handle
- 返回值:
  \- 当前音量等级（0-100）

6. **bk\_audio\_player\_clear\_music\_list**

清空播放列表。

```
int bk_audio_player_clear_music_list(bk_audio_player_handle_t handle);
```

- 参数:
  \- handle: 实例 handle
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_ERR: 失败

7. **bk\_audio\_player\_add\_music**

添加音乐到播放列表。

```
int bk_audio_player_add_music(bk_audio_player_handle_t handle, char *name, char *uri);
```

- 参数:
  \- handle: 实例 handle
  \- name: 音乐名称
  \- uri: 音乐 URI（URL 或文件路径）
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_ERR: 失败

8. **bk\_audio\_player\_del\_music\_by\_name**

通过名称从播放列表中删除音乐。

```
int bk_audio_player_del_music_by_name(bk_audio_player_handle_t handle, char *name);
```

- 参数:
  \- handle: 实例 handle
  \- name: 音乐名称
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_ERR: 失败

9. **bk\_audio\_player\_del\_music\_by\_uri**

通过 URI 从播放列表中删除音乐。

```
int bk_audio_player_del_music_by_uri(bk_audio_player_handle_t handle, char *uri);
```

- 参数:
  \- handle: 实例 handle
  \- uri: 音乐 URI（URL 或文件路径）
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_ERR: 失败

10. **bk\_audio\_player\_start**

开始播放。

```
int bk_audio_player_start(bk_audio_player_handle_t handle);
```

- 参数:
  \- handle: 实例 handle
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_ERR: 失败
  \- AUDIO\_PLAYER\_NOT\_INIT: 播放器未初始化

11. **bk\_audio\_player\_stop**

停止播放。

```
int bk_audio_player_stop(bk_audio_player_handle_t handle);
```

- 参数:
  \- handle: 实例 handle
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_ERR: 失败
  \- AUDIO\_PLAYER\_NOT\_INIT: 播放器未初始化

12. **bk\_audio\_player\_pause**

暂停播放。

```
int bk_audio_player_pause(bk_audio_player_handle_t handle);
```

- 参数:
  \- handle: 实例 handle
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_ERR: 失败
  \- AUDIO\_PLAYER\_NOT\_INIT: 播放器未初始化

13. **bk\_audio\_player\_resume**

恢复播放。

```
int bk_audio_player_resume(bk_audio_player_handle_t handle);
```

- 参数:
  \- handle: 实例 handle
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_ERR: 失败
  \- AUDIO\_PLAYER\_NOT\_INIT: 播放器未初始化

14. **bk\_audio\_player\_prev**

播放上一首歌曲。

```
int bk_audio_player_prev(bk_audio_player_handle_t handle);
```

- 参数:
  \- handle: 实例 handle
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_INVALID: 没有可用的上一首歌曲
  \- AUDIO\_PLAYER\_NOT\_INIT: 播放器未初始化

15. **bk\_audio\_player\_next**

播放下一首歌曲。

```
int bk_audio_player_next(bk_audio_player_handle_t handle);
```

- 参数:
  \- handle: 实例 handle
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_INVALID: 没有可用的下一首歌曲
  \- AUDIO\_PLAYER\_NOT\_INIT: 播放器未初始化

16. **bk\_audio\_player\_jumpto**

跳转到播放列表中的指定歌曲。

```
int bk_audio_player_jumpto(bk_audio_player_handle_t handle, int idx);
```

- 参数:
  \- handle: 实例 handle
  \- idx: 播放列表中的歌曲索引
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功
  \- AUDIO\_PLAYER\_INVALID: 索引无效
  \- AUDIO\_PLAYER\_NOT\_INIT: 播放器未初始化

17. **bk\_audio\_player\_seek**

将当前曲目跳转到指定播放位置，仅在播放本地音频文件时生效。

```
int bk_audio_player_seek(bk_audio_player_handle_t handle, int second);
```

- 参数:
  \- handle: 实例 handle
  \- second: 目标播放位置（秒），小于 0 时将被视为 0
- 返回值:
  \- AUDIO\_PLAYER\_OK: 成功（已受理定位请求）
  \- AUDIO\_PLAYER\_NOT\_INIT: 播放器未初始化

18. **bk\_audio\_player\_get\_metadata\_from\_file**

从指定音频文件中提取元数据（如标题、艺术家、比特率、时长等），并填充到 audio\_metadata\_t 结构体中。使用当前实例已注册的元数据解析器。

```
int bk_audio_player_get_metadata_from_file(bk_audio_player_handle_t handle, const char *filepath, audio_metadata_t *metadata);
```

- 参数:
  \- handle: 实例 handle
  \- filepath: 音频文件的完整路径
  \- metadata: 输出参数，指向待填充的元数据结构体
- 返回值:
  \- 0: 成功
  \- -1: 打开文件失败
  \- -2: 文件格式不支持
  \- -3: 参数无效
  \- -4: 读取文件失败

19. **bk\_audio\_player\_register\_metadata\_parser**

注册自定义元数据解析器。可用于支持新的音频格式，提供的 ops 在实例生命周期内须保持有效。

```
int bk_audio_player_register_metadata_parser(bk_audio_player_handle_t handle, const bk_audio_player_metadata_parser_ops_t *ops);
```

- 参数:
  \- handle: 实例 handle
  \- ops: 元数据解析器操作表，参见 bk\_audio\_player\_metadata\_parser\_ops\_t
- 返回值:
  \- AUDIO\_PLAYER\_OK: 注册成功
  \- AUDIO\_PLAYER\_ERR: 参数无效或内部未初始化

20. **bk\_audio\_player\_register\_source**

注册自定义音频源（如新网络协议或存储后端）。提供的 ops 在实例生命周期内须保持有效。

```
int bk_audio_player_register_source(bk_audio_player_handle_t handle, const bk_audio_player_source_ops_t *ops);
```

- 参数:
  \- handle: 实例 handle
  \- ops: 源操作表，参见 bk\_audio\_player\_source\_ops\_t
- 返回值:
  \- AUDIO\_PLAYER\_OK: 注册成功
  \- AUDIO\_PLAYER\_ERR: 参数无效或内部未初始化

21. **bk\_audio\_player\_register\_decoder**

注册自定义解码器，以支持更多音频格式。提供的 ops 在实例生命周期内须保持有效。

```
int bk_audio_player_register_decoder(bk_audio_player_handle_t handle, const bk_audio_player_decoder_ops_t *ops);
```

- 参数:
  \- handle: 实例 handle
  \- ops: 解码器操作表，参见 bk\_audio\_player\_decoder\_ops\_t
- 返回值:
  \- AUDIO\_PLAYER\_OK: 注册成功
  \- AUDIO\_PLAYER\_ERR: 参数无效或内部未初始化

22. **bk\_audio\_player\_register\_sink**

注册自定义输出（如新设备或文件/流写入）。提供的 ops 在实例生命周期内须保持有效。

```
int bk_audio_player_register_sink(bk_audio_player_handle_t handle, const bk_audio_player_sink_ops_t *ops);
```

- 参数:
  \- handle: 实例 handle
  \- ops: 输出操作表，参见 bk\_audio\_player\_sink\_ops\_t
- 返回值:
  \- AUDIO\_PLAYER\_OK: 注册成功
  \- AUDIO\_PLAYER\_ERR: 参数无效或内部未初始化

<a id="id5"></a>

## 内置解码器插件

以下接口返回各格式解码器的操作表，可用于 bk\_audio\_player\_register\_decoder() 注册。

- **bk\_audio\_player\_get\_aac\_decoder\_ops**：获取 AAC 解码器操作表
- **bk\_audio\_player\_get\_amr\_decoder\_ops**：获取 AMR 解码器操作表
- **bk\_audio\_player\_get\_flac\_decoder\_ops**：获取 FLAC 解码器操作表
- **bk\_audio\_player\_get\_m4a\_decoder\_ops**：获取 M4A 解码器操作表
- **bk\_audio\_player\_get\_mp3\_decoder\_ops**：获取 MP3 解码器操作表
- **bk\_audio\_player\_get\_ogg\_decoder\_ops**：获取 OGG 解码器操作表
- **bk\_audio\_player\_get\_opus\_decoder\_ops**：获取 Opus 解码器操作表
- **bk\_audio\_player\_get\_ts\_decoder\_ops**：获取 MPEG-TS 解码器操作表
- **bk\_audio\_player\_get\_wav\_decoder\_ops**：获取 WAV 解码器操作表

<a id="id6"></a>

## 内置元数据解析器插件

以下接口返回各格式元数据解析器的操作表，可用于 bk\_audio\_player\_register\_metadata\_parser() 注册。

- **bk\_audio\_player\_get\_aac\_metadata\_parser\_ops**：获取 AAC 元数据解析器操作表
- **bk\_audio\_player\_get\_amr\_metadata\_parser\_ops**：获取 AMR 元数据解析器操作表
- **bk\_audio\_player\_get\_flac\_metadata\_parser\_ops**：获取 FLAC 元数据解析器操作表
- **bk\_audio\_player\_get\_m4a\_metadata\_parser\_ops**：获取 M4A 元数据解析器操作表
- **bk\_audio\_player\_get\_mp3\_metadata\_parser\_ops**：获取 MP3 元数据解析器操作表
- **bk\_audio\_player\_get\_ogg\_metadata\_parser\_ops**：获取 OGG 元数据解析器操作表
- **bk\_audio\_player\_get\_opus\_metadata\_parser\_ops**：获取 Opus 元数据解析器操作表
- **bk\_audio\_player\_get\_wav\_metadata\_parser\_ops**：获取 WAV 元数据解析器操作表

<a id="id7"></a>

## 内置源插件

以下接口返回各音频源的操作表，可用于 bk\_audio\_player\_register\_source() 注册。

- **bk\_audio\_player\_get\_file\_source\_ops**：获取本地文件源操作表
- **bk\_audio\_player\_get\_hls\_source\_ops**：获取 HLS 流源操作表
- **bk\_audio\_player\_get\_net\_source\_ops**：获取网络源操作表

<a id="sink"></a>

## 内置输出插件（Sink）

以下接口返回各音频输出的操作表，可用于 bk\_audio\_player\_register\_sink() 注册。

- **bk\_audio\_player\_get\_file\_sink\_ops**：获取文件输出操作表
- **bk\_audio\_player\_get\_onboard\_speaker\_sink\_ops**：获取板载扬声器输出操作表

<a id="id8"></a>

## API类型定义

1. **audio\_player\_error\_code\_t**

音频播放器错误码枚举。

```
typedef enum
{
    AUDIO_PLAYER_OK = 0,              /*！< 操作成功 */
    AUDIO_PLAYER_ERR = -100,          /*！< 通用错误 */
    AUDIO_PLAYER_NOT_INIT,            /*！< 播放器未初始化 */
    AUDIO_PLAYER_NO_MEM,              /*！< 内存不足 */
    AUDIO_PLAYER_PROGRESS,            /*！< 操作进行中 */
    AUDIO_PLAYER_INVALID,             /*！< 参数无效 */
    AUDIO_PLAYER_TIMEOUT = -200,      /*！< 操作超时 */
} audio_player_error_code_t;
```

2. **audio\_player\_mode\_t**

音频播放器播放模式枚举。

```
typedef enum
{
    AUDIO_PLAYER_MODE_ONE_SONG = 0,        /*！< 播放单曲 */
    AUDIO_PLAYER_MODE_SEQUENCE,            /*！< 顺序播放 */
    AUDIO_PLAYER_MODE_ONE_SONG_LOOP,       /*！< 单曲循环 */
    AUDIO_PLAYER_MODE_SEQUENCE_LOOP,       /*！< 列表循环 */
    AUDIO_PLAYER_MODE_RANDOM               /*！< 随机播放 */
} audio_player_mode_t;
```

3. **audio\_player\_event\_type\_t**

音频播放器事件类型枚举。

```
typedef enum
{
    AUDIO_PLAYER_EVENT_SONG_START,           /*！< 歌曲开始播放 */
    AUDIO_PLAYER_EVENT_SONG_FINISH,          /*！< 歌曲播放完成 */
    AUDIO_PLAYER_EVENT_SONG_FAILURE,         /*！< 歌曲播放失败 */
    AUDIO_PLAYER_EVENT_SONG_PAUSE,           /*！< 歌曲已暂停 */
    AUDIO_PLAYER_EVENT_SONG_RESUME,          /*！< 歌曲已恢复 */
    AUDIO_PLAYER_EVENT_SONG_TICK,            /*！< 歌曲播放进度更新 */
    AUDIO_PLAYER_EVENT_SEEK_COMPLETE,        /*！< 定位操作完成 */
    AUDIO_PLAYER_EVENT_LAST,                 /*！< 事件枚举结束标记 */
} audio_player_event_type_t;
```

4. **audio\_player\_event\_handler\_func**

事件处理回调函数类型。

```
typedef void (*audio_player_event_handler_func)(audio_player_event_type_t event, void *extra_info, void *args);
```

- 参数:
  \- event: 事件类型，参见 audio\_player\_event\_type\_t 枚举
  \- extra\_info: 事件的额外信息
  \- args: 用户自定义参数
- 返回值:
  \- 无

5. **audio\_player\_seek\_result\_t**

AUDIO\_PLAYER\_EVENT\_SEEK\_COMPLETE 事件携带的结构体负载，描述目标秒数以及实际执行结果。

```
typedef struct
{
    int second;     /*！< 请求定位的时间（秒） */
    int status;     /*！< 结果码，AUDIO_PLAYER_OK 表示成功 */
} audio_player_seek_result_t;
```

- 成员:
  \- second: 用户请求的目标播放位置
  \- status: 执行结果码

6. **bk\_audio\_player\_cfg\_t**

音频播放器配置结构体，包含内部任务栈、优先级及事件回调等。

```
typedef struct
{
    uint32_t                         task_stack;     /*!< 内部任务栈大小（字节），0 表示使用默认值 */
    int                              task_prio;      /*!< 内部任务优先级（遵循 RTOS 约定） */
    audio_player_event_handler_func  event_handler;  /*!< 事件处理回调函数 */
    void *                           args;           /*!< 事件处理函数的用户自定义参数 */
} bk_audio_player_cfg_t;
```

- 成员:
  \- task\_stack: 内部任务栈大小（字节），0 表示使用 AUDIO\_PLAYER\_DEFAULT\_TASK\_STACK
  \- task\_prio: 内部任务优先级，如 BEKEN\_DEFAULT\_WORKER\_PRIORITY
  \- event\_handler: 事件处理回调函数，可以为 NULL
  \- args: 传递给事件处理函数的用户自定义参数，可以为 NULL

7. **DEFAULT\_AUDIO\_PLAYER\_CONFIG()**

默认音频播放器配置宏，使用默认任务栈、优先级及空事件回调。

```
#define DEFAULT_AUDIO_PLAYER_CONFIG() {             \
    .task_stack = AUDIO_PLAYER_DEFAULT_TASK_STACK,  \
    .task_prio = BEKEN_DEFAULT_WORKER_PRIORITY,     \
    .event_handler = NULL,                          \
    .args = NULL,                                   \
}
```

使用示例：

```
bk_audio_player_handle_t handle = NULL;
bk_audio_player_cfg_t cfg = DEFAULT_AUDIO_PLAYER_CONFIG();
bk_audio_player_new(&handle, &cfg);
```

8. **AUDIO\_PLAYER\_MODE\_DEFAULT**

默认播放模式宏定义。

```
#define AUDIO_PLAYER_MODE_DEFAULT   AUDIO_PLAYER_MODE_SEQUENCE_LOOP
```

默认播放模式为列表循环播放。
