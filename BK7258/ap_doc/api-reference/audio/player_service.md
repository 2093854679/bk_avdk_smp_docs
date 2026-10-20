---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/player_service/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="api"></a>

# 播放器服务API

<a id="id1"></a>

## 概述

播放器服务提供音频播放功能，支持播放来自各种源（如数组、VFS（虚拟文件系统）和URL）的音频数据。它还支持各种音频格式的不同音频解码器。

- 有关播放器服务的开发指南，请参阅：

  - [播放器服务开发指南](../../developer-guide/audio/player_service.md)
- 有关播放器服务的示例工程，请参阅：

  - [播放器服务示例工程](../../examples/projects/player_service_example.md)

<a id="id4"></a>

## API参考

1. **bk\_player\_create**

创建一个播放器句柄。支持创建直接播放的播放器和不直接播放的播放器（解码后的PCM数据可以输出到其他组件进行播放）。

```
bk_player_handle_t bk_player_create(bk_player_cfg_t *cfg);
```

- 参数:
  \- cfg: 播放器配置
- 返回值:
  \- 非NULL: 成功，返回播放器句柄
  \- NULL: 失败

2. **bk\_player\_destroy**

销毁一个播放器句柄。

```
bk_err_t bk_player_destroy(bk_player_handle_t player_handle);
```

- 参数:
  \- player\_handle: 播放器句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

3. **bk\_player\_start**

启动播放器。

```
bk_err_t bk_player_start(bk_player_handle_t player_handle);
```

- 参数:
  \- player\_handle: 播放器句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

4. **bk\_player\_stop**

停止播放器。

```
bk_err_t bk_player_stop(bk_player_handle_t player_handle);
```

- 参数:
  \- player\_handle: 播放器句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

5. **bk\_player\_set\_uri**

设置播放器的URI。

```
bk_err_t bk_player_set_uri(bk_player_handle_t player_handle, player_uri_info_t *uri_info);
```

- 参数:
  \- player\_handle: 播放器句柄
  \- uri\_info: URI信息
- 返回值:
  \- 0: 成功
  \- 非0: 失败

6. **bk\_player\_get\_state**

获取播放器的状态。

```
bk_err_t bk_player_get_state(bk_player_handle_t player_handle, bk_player_state_t *state);
```

- 参数:
  \- player\_handle: 播放器句柄
  \- state: 用于存储播放器状态的指针
- 返回值:
  \- 0: 成功
  \- 非0: 失败

7. **bk\_player\_set\_decode\_type**

设置播放器的解码类型。

```
bk_err_t bk_player_set_decode_type(bk_player_handle_t player_handle, audio_dec_type_t dec_type);
```

- 参数:
  \- player\_handle: 播放器句柄
  \- dec\_type: 解码类型
- 返回值:
  \- 0: 成功
  \- 非0: 失败

8. **bk\_player\_set\_output\_port**

设置播放器的输出端口。当创建的播放器不直接播放数据时，使用此接口设置输出端口。当播放器正在播放数据时，请勿使用此接口设置输出端口。

```
bk_err_t bk_player_set_output_port(bk_player_handle_t player_handle, audio_port_handle_t port);
```

- 参数:
  \- player\_handle: 播放器句柄
  \- port: 输出端口句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

<a id="id5"></a>

## API类型定义

1. **bk\_player\_state\_t**

播放器服务状态枚举。

```
typedef enum
{
    PLAYER_STATE_NONE = 0,    /*!< 播放器服务处于未定义状态 */
    PLAYER_STATE_IDLE,        /*!< 播放器服务已初始化但未激活 */
    PLAYER_STATE_STOPED,      /*!< 播放器服务已停止 */
    PLAYER_STATE_PLAYING,     /*!< 播放器服务正在积极播放音频 */
    PLAYER_STATE_PAUSED,      /*!< 播放器服务已暂停 */
} bk_player_state_t;
```

2. **bk\_player\_event\_t**

播放器服务事件枚举。

```
typedef enum
{
    PLAYER_EVENT_START = 0,   /*!< 播放器服务开始事件 */
    PLAYER_EVENT_STOP,        /*!< 播放器服务停止事件 */
    PLAYER_EVENT_FAILURE,     /*!< 播放器服务失败事件 */
    PLAYER_EVENT_PAUSE,       /*!< 播放器服务暂停事件 */
    PLAYER_EVENT_RESUME,      /*!< 播放器服务恢复事件 */
    PLAYER_EVENT_FINISH,      /*!< 播放器服务完成事件 */

    PLAYER_EVENT_MUSIC_INFO,  /*!< 播放器服务音乐信息事件 */
} bk_player_event_t;
```

3. **player\_uri\_type\_t**

播放器URI类型枚举。

```
typedef enum
{
    PLAYER_URI_TYPE_ARRAY = 0,  /*!< 数组流源类型 */
    PLAYER_URI_TYPE_VFS,        /*!< VFS（虚拟文件系统）源类型 */
    PLAYER_URI_TYPE_URL,        /*!< URL源类型 */
} player_uri_type_t;
```

4. **player\_uri\_info\_t**

播放器URI信息结构。

```
typedef struct
{
    player_uri_type_t uri_type; /*!< URI类型 */
    char *uri;                  /*!< URI字符串 */
    uint32_t total_len;         /*!< 音频数据总长度 */
} player_uri_info_t;
```

5. **bk\_player\_handle\_t**

播放器句柄类型。

```
typedef struct player *bk_player_handle_t;
```

6. **player\_event\_handle\_cb**

播放器事件处理回调类型。

```
typedef int (*player_event_handle_cb)(int event, void *data, void *args);
```

- 参数:
  \- event: 事件类型
  \- data: 事件数据
  \- args: 用户定义的参数
- 返回值:
  \- 0: 成功
  \- 其他值: 失败

7. **bk\_player\_cfg\_t**

播放器服务配置结构。

```
typedef struct
{
    spk_type_t                          spk_type;           /*!< 扬声器类型 */

    union
    {
        onboard_speaker_stream_cfg_t    onboard_spk_cfg;    /*!< 板载扬声器配置 */
        uac_speaker_stream_cfg_t        uac_spk_cfg;        /*!< USB音频类扬声器配置 */
        uint8_t                         reserve;            /*!< 保留用于未来使用 */
    } spk_cfg;                                              /*!< 扬声器配置联合体 */

    player_event_handle_cb              event_handle;       /*!< 播放器事件处理回调函数 */
    void *                              args;               /*!< 事件处理函数的用户定义参数 */
} bk_player_cfg_t;
```

8. **DEFAULT\_PLAYER\_NOT\_PLAYBACK\_CONFIG()**

不带播放功能的默认播放器配置宏。

此配置创建一个读取和解码音频数据到PCM数据，但不播放PCM数据的播放器。

```
#define DEFAULT_PLAYER_NOT_PLAYBACK_CONFIG() {                  \
    .spk_type = SPK_TYPE_INVALID,                               \
    .spk_cfg.reserve = 0,                                       \
    .event_handle = NULL,                                       \
    .args = NULL,                                               \
}
```

9. **DEFAULT\_PLAYER\_WITH\_PLAYBACK\_CONFIG()**

带播放功能的默认播放器配置宏。

此配置创建一个使用板载扬声器播放音频的播放器，采用默认设置读取、解码并播放音频数据。

```
#define DEFAULT_PLAYER_WITH_PLAYBACK_CONFIG() {                 \
    .spk_type = SPK_TYPE_ONBOARD,                               \
    .spk_cfg.onboard_spk_cfg = {                                \
        .chl_num = 1,                                           \
        .sample_rate = 8000,                                    \
        .dig_gain = 0x2d,                                       \
        .ana_gain = 0x07,                                       \
        .work_mode = AUD_DAC_WORK_MODE_DIFFEN,                  \
        .bits = 16,                                             \
        .clk_src = AUD_CLK_XTAL,                                \
        .multi_out_port_num = 1,                                \
        .frame_size = 320,                                      \
        .pool_length = 0,                                       \
        .pool_play_thold = 0,                                   \
        .pool_pause_thold = 0,                                  \
        .task_stack = ONBOARD_SPEAKER_STREAM_TASK_STACK,        \
        .task_core = ONBOARD_SPEAKER_STREAM_TASK_CORE,          \
        .task_prio = ONBOARD_SPEAKER_STREAM_TASK_PRIO,          \
    },                                                          \
    .event_handle = NULL,                                       \
    .args = NULL,                                               \
}
```
