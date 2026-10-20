---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/voice_service/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="api"></a>

# 语音通话服务API

<a id="id1"></a>

## 概述

语音通话服务提供双向语音通话功能，支持常见的特性如AEC（声学回声消除）和编解码。

- 有关语音通话服务的开发指南，请参阅：

  - [语音通话服务开发指南](../../developer-guide/audio/voice_service.md)
- 有关语音通话服务的示例工程，请参阅：

  - [语音通话服务示例工程](../../examples/projects/voice_service_example.md)

<a id="id4"></a>

## API参考

1. **bk\_voice\_init**

创建一个语音通话句柄。

```
voice_handle_t bk_voice_init(voice_cfg_t *cfg);
```

- 参数:
  \- cfg: 语音通话配置
- 返回值:
  \- 非NULL: 成功，返回语音句柄
  \- NULL: 失败

2. **bk\_voice\_deinit**

销毁一个语音通话句柄。

```
bk_err_t bk_voice_deinit(voice_handle_t voice_handle);
```

- 参数:
  \- voice\_handle: 语音通话句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

3. **bk\_voice\_start**

启动语音通话。

```
bk_err_t bk_voice_start(voice_handle_t voice_handle);
```

- 参数:
  \- voice\_handle: 语音通话句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

4. **bk\_voice\_stop**

停止语音通话。

```
bk_err_t bk_voice_stop(voice_handle_t voice_handle);
```

- 参数:
  \- voice\_handle: 语音通话句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

5. **bk\_voice\_read\_mic\_data**

读取麦克风数据。

```
int bk_voice_read_mic_data(voice_handle_t voice_handle, char *buffer, uint32_t size);
```

- 参数:
  \- voice\_handle: 语音通话句柄
  \- buffer: 用于存储麦克风数据的缓冲区
  \- size: 缓冲区大小
- 返回值:
  \- 大于0: 成功读取的字节数
  \- 小于或等于0: 失败

6. **bk\_voice\_write\_spk\_data**

向扬声器写入数据。

```
int bk_voice_write_spk_data(voice_handle_t voice_handle, char *buffer, uint32_t size);
```

- 参数:
  \- voice\_handle: 语音通话句柄
  \- buffer: 包含要写入数据的缓冲区
  \- size: 要写入的数据大小
- 返回值:
  \- 大于0: 成功写入的字节数
  \- 小于或等于0: 失败

7. **bk\_voice\_event\_handle**

处理语音事件。

```
bk_err_t bk_voice_event_handle(voice_event_handle event_handle, vioce_evt_t event, void *param, void *args);
```

- 参数:
  \- event\_handle: 语音事件处理函数
  \- event: 语音事件类型
  \- param: 事件参数
  \- args: 附加参数
- 返回值:
  \- 0: 成功
  \- 非0: 失败

8. **bk\_voice\_get\_status**

获取语音通话的状态。

```
bk_err_t bk_voice_get_status(voice_handle_t voice_handle, voice_sta_t *status);
```

- 参数:
  \- voice\_handle: 语音通话句柄
  \- status: 用于存储语音状态的指针
- 返回值:
  \- 0: 成功
  \- 非0: 失败

9. **bk\_voice\_get\_spk\_element**

获取语音通话的扬声器元素句柄。

```
audio_element_handle_t bk_voice_get_spk_element(voice_handle_t voice_handle);
```

- 参数:
  \- voice\_handle: 语音通话句柄
- 返回值:
  \- 非NULL: 成功，返回扬声器元素句柄
  \- NULL: 失败

10. **bk\_voice\_cal\_vad\_buf\_size**

计算VAD（语音活动检测）缓冲区大小。

```
void bk_voice_cal_vad_buf_size(voice_cfg_t *cfg, voice_handle_t voice_handle);
```

- 参数:
  \- cfg: 语音配置
  \- voice\_handle: 语音通话句柄

<a id="id5"></a>

## 语音读取服务API

1. **bk\_voice\_read\_init**

创建一个语音读取句柄，用于从语音服务读取麦克风数据。

```
voice_read_handle_t bk_voice_read_init(voice_read_cfg_t *cfg);
```

- 参数:
  \- cfg: 语音读取配置
- 返回值:
  \- 非NULL: 成功，返回语音读取句柄
  \- NULL: 失败

2. **bk\_voice\_read\_deinit**

销毁一个语音读取句柄。

```
bk_err_t bk_voice_read_deinit(voice_read_handle_t voice_read_handle);
```

- 参数:
  \- voice\_read\_handle: 语音读取句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

3. **bk\_voice\_read\_start**

启动语音读取。

```
bk_err_t bk_voice_read_start(voice_read_handle_t voice_read_handle);
```

- 参数:
  \- voice\_read\_handle: 语音读取句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

4. **bk\_voice\_read\_stop**

停止语音读取。

```
bk_err_t bk_voice_read_stop(voice_read_handle_t voice_read_handle);
```

- 参数:
  \- voice\_read\_handle: 语音读取句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

<a id="id6"></a>

## 语音写入服务API

1. **bk\_voice\_write\_init**

创建一个语音写入句柄，用于向语音服务写入语音数据。

```
voice_write_handle_t bk_voice_write_init(voice_write_cfg_t *cfg);
```

- 参数:
  \- cfg: 语音写入配置
- 返回值:
  \- 非NULL: 成功，返回语音写入句柄
  \- NULL: 失败

2. **bk\_voice\_write\_deinit**

销毁一个语音写入句柄。

```
bk_err_t bk_voice_write_deinit(voice_write_handle_t voice_write_handle);
```

- 参数:
  \- voice\_write\_handle: 语音写入句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

3. **bk\_voice\_write\_start**

启动语音写入。

```
bk_err_t bk_voice_write_start(voice_write_handle_t voice_write_handle);
```

- 参数:
  \- voice\_write\_handle: 语音写入句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

4. **bk\_voice\_write\_stop**

停止语音写入。

```
bk_err_t bk_voice_write_stop(voice_write_handle_t voice_write_handle);
```

- 参数:
  \- voice\_write\_handle: 语音写入句柄
- 返回值:
  \- 0: 成功
  \- 非0: 失败

5. **bk\_voice\_write\_frame\_data**

向语音服务写入语音帧数据。

```
bk_err_t bk_voice_write_frame_data(voice_write_handle_t voice_write_handle, char *buffer, uint32_t len);
```

- 参数:
  \- voice\_write\_handle: 语音写入句柄
  \- buffer: 语音数据缓冲区
  \- len: 语音数据长度
- 返回值:
  \- 0: 成功
  \- 非0: 失败

<a id="id7"></a>

## API类型定义

1. **voice\_sta\_t**

语音服务状态枚举。

```
typedef enum
{
    VOICE_STA_NONE = 0,    /*!< 语音服务处于未定义状态 */
    VOICE_STA_IDLE,        /*!< 语音服务已初始化但未激活 */
    VOICE_STA_RUNNING,     /*!< 语音服务正在积极处理音频 */
    VOICE_STA_STOPPING,    /*!< 语音服务正在停止过程中 */
    VOICE_STA_STOPED,      /*!< 语音服务已停止 */
} voice_sta_t;
```

2. **voice\_evt\_t**

语音服务事件枚举。

```
typedef enum
{
    VOC_EVT_NONE = 0,              /*!< 无事件 */
    VOC_EVT_MIC_NOT_SUPPORT,       /*!< 麦克风类型不支持 */
    VOC_EVT_SPK_NOT_SUPPORT,       /*!< 扬声器类型不支持 */
    VOC_EVT_ERROR_UNKNOW,          /*!< 发生未知错误 */
    VOC_EVT_STOP,                  /*!< 语音服务停止事件 */
} voice_evt_t;
```

3. **voice\_event\_handle**

语音服务事件处理回调类型。

```
typedef bk_err_t (*voice_event_handle)(voice_evt_t evt, void *data, void *args);
```

- 参数:
  \- evt: 事件类型
  \- data: 事件数据
  \- args: 用户定义的参数
- 返回值:
  \- BK\_OK: 成功
  \- 其他值: 错误

4. **voice\_element\_init**

语音编解码器元素初始化回调函数类型，用于创建用户自定义的编码器或解码器元素。

```
typedef audio_element_handle_t (*voice_element_init)(void *args);
```

- 参数:
  \- args: 用户定义的参数
- 返回值:
  \- 非NULL: 成功，返回音频元素句柄
  \- NULL: 失败

5. **voice\_handle\_t**

语音服务句柄类型。

```
typedef struct voice *voice_handle_t;
```

6. **audio\_codec\_common\_t**

通用音频编解码器配置结构体。

```
typedef struct
{
    uint32_t    samp_rate;        /*!< 音频采样率（Hz） */
    uint32_t    bitrate;          /*!< 音频比特率（bps） */
    uint32_t    frame_in_size;    /*!< 输入帧大小（字节） */
    uint32_t    frame_out_size;   /*!< 输出帧大小（字节） */
    uint8_t     bits;             /*!< 每样本位数 */
    uint8_t     frame_in_ms;      /*!< 输入帧持续时间（毫秒） */
    uint8_t     vbr;              /*!< 可变比特率启用标志 */
    uint8_t     channels;         /*!< 音频通道数 */
} audio_codec_common_t;
```

7. **voice\_cfg\_t**

语音服务配置结构体。

```
typedef struct
{
    mic_type_t              mic_type;      /*!< 麦克风类型 */
    union
    {
        onboard_mic_stream_cfg_t            onboard_mic_cfg;          /*!< 板载麦克风配置 */
        onboard_dual_dmic_mic_stream_cfg_t  onboard_dual_dmic_mic_cfg; /*!< 板载双DMIC配置 */
        uac_mic_stream_cfg_t                uac_mic_cfg;              /*!< USB音频类麦克风配置 */
    } mic_cfg;                              /*!< 麦克风配置联合体 */

    bool                    aec_en;        /*!< 声学回声消除（AEC）启用标志 */
    union
    {
        aec_v3_algorithm_cfg_t aec_alg_cfg; /*!< AEC算法配置 */
        uint8_t                reserve;     /*!< 保留用于未来使用 */
    } aec_cfg;                              /*!< AEC配置联合体 */

    bool                    enc_en;        /*!< 音频编码器启用标志 */
    audio_enc_type_t        enc_type;      /*!< 音频编码器类型 */
    audio_codec_common_t    enc_common;    /*!< 通用编码器配置 */
    union
    {
        g711_encoder_cfg_t    g711_enc_cfg; /*!< G.711编码器配置 */
#if CONFIG_VOICE_SERVICE_AAC_ENCODER
        aac_encoder_cfg_t     aac_enc_cfg;  /*!< AAC编码器配置 */
#endif
#if CONFIG_VOICE_SERVICE_G722_ENCODER
        g722_encoder_cfg_t    g722_enc_cfg; /*!< G.722编码器配置 */
#endif
#if CONFIG_VOICE_SERVICE_OPUS_ENCODER
        opus_enc_cfg_t        opus_enc_cfg; /*!< Opus编码器配置 */
#endif
        uint8_t               pcm_enc_cfg;  /*!< PCM编码器配置占位符 */
    } enc_cfg;                              /*!< 编码器配置联合体 */

    uint32_t                read_pool_size;     /*!< 用于保存编码麦克风数据的池大小（字节） */
    uint32_t                write_pool_size;    /*!< 用于保存尚未解码的扬声器数据的池大小（字节） */

    bool                    dec_en;        /*!< 音频解码器启用标志 */
    audio_dec_type_t        dec_type;      /*!< 音频解码器类型 */
    audio_codec_common_t    dec_common;    /*!< 通用解码器配置 */
    union
    {
        g711_decoder_cfg_t    g711_dec_cfg; /*!< G.711解码器配置 */
#if CONFIG_VOICE_SERVICE_AAC_DECODER
        aac_decoder_cfg_t     aac_dec_cfg;  /*!< AAC解码器配置 */
#endif
#if CONFIG_VOICE_SERVICE_G722_DECODER
        g722_decoder_cfg_t    g722_dec_cfg; /*!< G.722解码器配置 */
#endif
#if CONFIG_VOICE_SERVICE_OPUS_DECODER
        opus_dec_cfg_t        opus_dec_cfg; /*!< Opus解码器配置 */
#endif
        uint8_t               pcm_dec_cfg;  /*!< PCM解码器配置占位符 */
    } dec_cfg;                              /*!< 解码器配置联合体 */

    spk_type_t              spk_type;      /*!< 扬声器类型 */
    union
    {
        onboard_speaker_stream_cfg_t    onboard_spk_cfg; /*!< 板载扬声器配置 */
        uac_speaker_stream_cfg_t        uac_spk_cfg;     /*!< USB音频类扬声器配置 */
    } spk_cfg;                              /*!< 扬声器配置联合体 */

#if CONFIG_VOICE_SERVICE_EQ
    bool                    eq_en;         /*!< 均衡器启用标志 */
    union
    {
        eq_algorithm_cfg_t  eq_alg_cfg;    /*!< 均衡器算法配置 */
    } eq_cfg;                               /*!< 均衡器配置联合体 */
#endif

    voice_event_handle      event_handle;  /*!< 语音事件处理回调函数 */
    void *                  args;          /*!< 事件处理函数的用户定义参数 */

    voice_element_init      voice_enc_init; /*!< 语音编码器元素初始化回调函数，当 enc_type=AUDIO_ENC_TYPE_USER 时使用此函数创建编码器元素 */
    void *                  enc_args;       /*!< 语音编码器初始化函数的用户定义配置参数 */
    voice_element_init      voice_dec_init; /*!< 语音解码器元素初始化回调函数，当 dec_type=AUDIO_DEC_TYPE_USER 时使用此函数创建解码器元素 */
    void *                  dec_args;       /*!< 语音解码器初始化函数的用户定义配置参数 */
} voice_cfg_t;
```

<a id="id8"></a>

## 典型配置宏定义

以下是语音服务提供的典型配置宏定义，可用于快速初始化语音服务：

1. **VOICE\_BY\_ONBOARD\_MIC\_SPK\_CFG\_DEFAULT()**

使用板载麦克风和扬声器，带AEC，8000Hz采样率和G.711a编解码器的默认配置。

配置详情：
:   - 输入：板载麦克风
    - 输出：板载扬声器
    - AEC：已启用
    - 麦克风采样率：8000Hz
    - 扬声器采样率：8000Hz
    - 编码器：G.711a
    - 解码器：G.711a
    - 均衡器：禁用

2. **DEFAULT\_VOICE\_BY\_ONBOARD\_MIC\_SPK\_AECV1\_G711A\_16000\_CONFIG()**

使用板载麦克风和扬声器，带AEC，16000Hz采样率和G.711a编解码器的默认配置。

配置详情：
:   - 输入：板载麦克风
    - 输出：板载扬声器
    - AEC：已启用
    - 麦克风采样率：16000Hz
    - 扬声器采样率：16000Hz
    - 编码器：G.711a
    - 解码器：G.711a
    - 均衡器：禁用

3. **VOICE\_BY\_UAC\_MIC\_SPK\_CFG\_DEFAULT()**

使用UAC麦克风和扬声器，带AEC，8000Hz采样率和G.711a编解码器的默认配置。

配置详情：
:   - 输入：UAC麦克风
    - 输出：UAC扬声器
    - AEC：已启用
    - 麦克风采样率：8000Hz
    - 扬声器采样率：8000Hz
    - 编码器：G.711a
    - 解码器：G.711a
    - 均衡器：禁用

4. **VOICE\_BY\_ONBOARD\_MIC\_SPK\_AAC\_CFG\_DEFAULT()**

使用板载麦克风/扬声器、AEC、8000Hz采样率和AAC编解码器的默认语音服务配置。

配置详情：
:   - 输入：板载麦克风
    - 输出：板载扬声器
    - AEC：已启用
    - 麦克风采样率：8000Hz
    - 扬声器采样率：8000Hz
    - 编码器：AAC
    - 解码器：AAC
    - 均衡器：禁用

5. **VOICE\_BY\_ONBOARD\_DUAL\_DMIC\_MIC\_SPK\_CFG\_DEFAULT()**

使用板载双DMIC麦克风/扬声器、AEC、16000Hz采样率和G.711a编解码器的默认语音服务配置。

配置详情：
:   - 输入：板载双DMIC麦克风
    - 输出：板载扬声器
    - AEC：已启用
    - 麦克风采样率：16000Hz
    - 扬声器采样率：16000Hz
    - 编码器：G.711a
    - 解码器：G.711a
    - 均衡器：禁用

6. **DEFAULT\_VOICE\_BY\_ONBOARD\_MIC\_SPK\_G722\_CONFIG()**

使用板载麦克风/扬声器、AEC、16000Hz采样率和G.722编解码器的默认语音服务配置。

配置详情：
:   - 输入：板载麦克风
    - 输出：板载扬声器
    - AEC：已启用
    - 麦克风采样率：16000Hz
    - 扬声器采样率：16000Hz
    - 编码器：G.722
    - 解码器：G.722
    - 均衡器：禁用

7. **VOICE\_BY\_ONBOARD\_MIC\_SPK\_EQ\_CFG\_DEFAULT()**

使用板载麦克风/扬声器、AEC、8000Hz采样率、G.711a编解码器并启用均衡器的默认语音服务配置。

配置详情：
:   - 输入：板载麦克风
    - 输出：板载扬声器
    - AEC：已启用
    - 麦克风采样率：8000Hz
    - 扬声器采样率：8000Hz
    - 编码器：G.711a
    - 解码器：G.711a
    - 均衡器：启用

8. **DEFAULT\_VOICE\_BY\_ONBOARD\_MIC\_SPK\_OPUS\_CONFIG()**

使用板载麦克风/扬声器、AEC、16000Hz采样率和OPUS编解码器的默认语音服务配置。

配置详情：
:   - 输入：板载麦克风
    - 输出：板载扬声器
    - AEC：已启用
    - 麦克风采样率：16000Hz
    - 扬声器采样率：16000Hz
    - 编码器：OPUS
    - 解码器：OPUS
    - 均衡器：禁用

<a id="id9"></a>

## 语音读取服务类型定义

1. **voice\_read\_handle\_t**

语音读取句柄类型。

```
typedef struct voice_read *voice_read_handle_t;
```

2. **voice\_read\_cfg\_t**

语音读取配置结构体。

```
typedef struct {
    voice_handle_t voice_handle;                                                    /*!< 语音句柄 */
    uint32_t max_read_size;                                                         /*!< 从语音句柄读取的最大数据大小，用于voice_read_callback */
    int (*voice_read_callback)(unsigned char *data, unsigned int len, void *args);  /*!< 当读取到有效数据时调用此回调 */
    void *args;                                                                     /*!< 回调的私有参数 */
    int task_stack;                                                                 /*!< 任务堆栈大小 */
    int task_core;                                                                  /*!< 任务运行的内核（0或1） */
    int task_prio;                                                                  /*!< 任务优先级（基于freeRTOS优先级） */
    audio_mem_type_t mem_type;                                                      /*!< 使用的内存类型，sram或psram */
} voice_read_cfg_t;
```

3. **VOICE\_READ\_TASK\_PRIO**

默认语音读取任务优先级。

```
#define VOICE_READ_TASK_PRIO    (BEKEN_DEFAULT_WORKER_PRIORITY - 1)
```

4. **VOICE\_READ\_CFG\_DEFAULT()**

默认语音读取配置宏。

```
#define VOICE_READ_CFG_DEFAULT() {                  \
    .voice_handle = NULL,                           \
    .max_read_size = 1920,                          \
    .voice_read_callback = NULL,                    \
    .args = NULL,                                   \
    .task_stack = 2048,                             \
    .task_core = 0,                                 \
    .task_prio = VOICE_READ_TASK_PRIO,              \
    .mem_type = AUDIO_MEM_TYPE_PSRAM,               \
}
```

<a id="id10"></a>

## 语音写入服务类型定义

1. **voice\_write\_handle\_t**

语音写入句柄类型。

```
typedef struct voice_write *voice_write_handle_t;
```

2. **voice\_write\_cfg\_t**

语音写入配置结构体。

```
typedef struct {
    voice_handle_t voice_handle;            /*!< 语音句柄 */
    uint32_t start_threshold;               /*!< 开始写入数据的阈值 */
    uint32_t pause_threshold;               /*!< 暂停写入数据的阈值 */
    int task_stack;                         /*!< 任务堆栈大小 */
    int task_core;                          /*!< 任务运行的内核（0或1） */
    int task_prio;                          /*!< 任务优先级（基于freeRTOS优先级） */
    audio_mem_type_t mem_type;              /*!< 使用的内存类型，sram、psram或音频堆 */
    audio_buf_type_t write_buf_type;        /*!< 使用的写入缓冲区类型，帧缓冲区或环形缓冲区 */
    int node_size;                          /*!< 帧缓冲区节点大小或环形缓冲区池大小 */
    int node_num;                           /*!< 帧缓冲区节点数或环形缓冲区的1 */
} voice_write_cfg_t;
```

3. **VOICE\_WRITE\_TASK\_PRIO**

默认语音写入任务优先级。

```
#define VOICE_WRITE_TASK_PRIO           (BEKEN_DEFAULT_WORKER_PRIORITY - 1)
```

4. **VOICE\_WRITE\_POOL\_SIZE**

默认语音写入池大小。

```
#define VOICE_WRITE_POOL_SIZE           (3200)
```

5. **VOICE\_WRITE\_START\_THRESHOLD**

默认语音写入开始阈值。

```
#define VOICE_WRITE_START_THRESHOLD     (1280)
```

6. **VOICE\_WRITE\_PAUSE\_THRESHOLD**

默认语音写入暂停阈值。

```
#define VOICE_WRITE_PAUSE_THRESHOLD     (0)
```

7. **VOICE\_WRITE\_CFG\_DEFAULT()**

默认语音写入配置宏。

```
#define VOICE_WRITE_CFG_DEFAULT() {                 \
    .voice_handle = NULL,                           \
    .start_threshold = VOICE_WRITE_START_THRESHOLD, \
    .pause_threshold = VOICE_WRITE_PAUSE_THRESHOLD, \
    .task_stack = 2048,                             \
    .task_core = 0,                                 \
    .task_prio = VOICE_READ_TASK_PRIO,              \
    .mem_type = AUDIO_MEM_TYPE_PSRAM,               \
    .write_buf_type = AUDIO_BUF_TYPE_RB,            \
    .node_size = VOICE_WRITE_POOL_SIZE,             \
    .node_num = 1,                                  \
}
```
