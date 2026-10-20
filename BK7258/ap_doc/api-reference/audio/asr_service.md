---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/asr_service/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="api"></a>

# 语音识别服务API

<a id="id1"></a>

## 概述

语音识别服务提供完整的语音识别处理框架，支持Wanson ASR引擎，并提供灵活的集成方式。该服务支持音频数据采集、处理、识别等功能，同时支持AEC和重采样。

- 有关语音识别服务的开发指南，请参阅：

  - [语音识别服务开发指南](../../developer-guide/audio/asr_service.md)
- 有关语音识别服务的示例工程，请参阅：

  - [语音识别服务示例工程](../../examples/projects/asr_service_example.md)

<a id="id4"></a>

## API参考

1. **bk\_asr\_create**

创建ASR服务句柄。

```
asr_handle_t bk_asr_create(asr_cfg_t *cfg);
```

- 参数:

  > - cfg: ASR配置参数，包含采样率、AEC配置等
- 返回值:

  > - 非NULL: 成功，返回ASR句柄
  > - NULL: 失败，通常因参数非法或内存分配失败

2. **bk\_asr\_init**

初始化ASR服务（ASR不直接使用麦克风，而是接收来自其他音频服务的音频数据作为输入）。

```
bk_err_t bk_asr_init(asr_cfg_t *cfg, asr_handle_t asr_handle);
```

- 参数:

  > - cfg: ASR配置参数
  > - asr\_handle: ASR句柄，由bk\_asr\_create创建
- 返回值:

  - 0: 成功
  - 非0: 失败

3. **bk\_asr\_init\_with\_mic**

使用麦克风初始化ASR服务（ASR服务可独立运行，不依赖其他音频服务）。

```
bk_err_t bk_asr_init_with_mic(asr_cfg_t *cfg, asr_handle_t asr_handle);
```

- 参数:

  > - cfg: ASR配置参数
  > - asr\_handle: ASR句柄，由bk\_asr\_create创建
- 返回值:

  > - 0: 成功
  > - 非0: 失败

4. **bk\_asr\_deinit**

反初始化ASR服务。

```
bk_err_t bk_asr_deinit(asr_handle_t asr_handle);
```

- 参数:

  > - asr\_handle: ASR句柄
- 返回值:

  > - 0: 成功
  > - 非0: 失败

5. **bk\_asr\_start**

启动ASR服务。

```
bk_err_t bk_asr_start(asr_handle_t asr_handle);
```

- 参数:

  > - asr\_handle: ASR句柄
- 返回值:

  > - 0: 成功
  > - 非0: 失败

6. **bk\_asr\_stop**

停止ASR服务。

```
bk_err_t bk_asr_stop(asr_handle_t asr_handle);
```

- 参数:

  > - asr\_handle: ASR句柄
- 返回值:

  > - 0: 成功
  > - 非0: 失败

7. **bk\_aud\_asr\_read\_mic\_data**

读取麦克风数据。

```
int bk_aud_asr_read_mic_data(asr_handle_t asr_handle, char *buffer, uint32_t size);
```

- 参数:

  > - asr\_handle: ASR句柄
  > - buffer: 用于存储麦克风数据的缓冲区
  > - size: 缓冲区大小
- 返回值:

  > - 大于0: 成功读取的字节数
  > - 小于或等于0: 失败

8. **bk\_aud\_asr\_init**

初始化音频ASR服务。

```
bk_err_t bk_aud_asr_init(aud_asr_cfg_t *cfg);
```

- 参数:

  > - cfg: 音频ASR配置参数
- 返回值:

  > - 0: 成功
  > - 非0: 失败

9. **bk\_aud\_asr\_deinit**

反初始化音频ASR服务。

```
bk_err_t bk_aud_asr_deinit(aud_asr_handle_t aud_asr_handle);
```

- 参数:

  > - aud\_asr\_handle: 音频ASR句柄
- 返回值:

  > - 0: 成功
  > - 非0: 失败

10. **bk\_aud\_asr\_start**

启动音频ASR服务。

```
bk_err_t bk_aud_asr_start(aud_asr_handle_t aud_asr_handle);
```

- 参数:

  > - aud\_asr\_handle: 音频ASR句柄
- 返回值:

  > - 0: 成功
  > - 非0: 失败

11. **bk\_aud\_asr\_stop**

停止音频ASR服务。

```
bk_err_t bk_aud_asr_stop(aud_asr_handle_t aud_asr_handle);
```

- 参数:

  > - aud\_asr\_handle: 音频ASR句柄
- 返回值:

  > - 0: 成功
  > - 非0: 失败

<a id="asr"></a>

## ASR引擎接口函数说明

Wanson ASR引擎交互的核心函数接口，具体说明如下：

1. **ASR初始化接口**

```
int bk_wanson_asr_common_init(void);
```

- 功能：初始化Wanson ASR引擎
- 返回值：

  > - 0：成功
  > - 非0：失败
- 说明：在使用ASR服务前必须先调用此函数初始化引擎

2. **ASR反初始化接口**

```
void bk_wanson_asr_common_deinit(void);
```

- 功能：反初始化Wanson ASR引擎，释放资源
- 说明：不再使用ASR服务时应调用此函数释放资源

3. **ASR识别接口**

```
int bk_wanson_asr_recog(void *read_buf, uint32_t read_size, void *p1, void *p2);
```

- 功能：处理音频数据并进行语音识别
- 参数：

  > - read\_buf：音频数据缓冲区
  > - read\_size：音频数据大小
  > - p1/p2：额外参数
- 返回值：

  > - 0：成功
  > - 非0：失败
- 说明：此函数会对输入的音频数据进行处理，识别结果通过回调函数返回

备注

1. 这些接口函数必须在ASR服务启动（bk\_asr\_start）之前在外部由用户代码进行初始化.
2. 接口函数的实现将通过 aud\_asr\_cfg\_t 结构体中的函数指针传递给ASR服务.
3. 如果用户需要使用自定义ASR引擎，但仍希望使用SDK提供的ASR处理流程，需要：

> - 替换相应的ASR库及相关文件
> - 根据上述函数接口格式实现对应的回调函数，包括结果处理回调

<a id="id5"></a>

## 数据结构

1. **asr\_cfg\_t**

ASR配置结构体。

```
typedef struct
{
   mic_type_t mic_type;                             /* 麦克风类型 */
   union
   {
      onboard_mic_stream_cfg_t    onboard_mic_cfg; /* 板载麦克风配置 */
      uac_mic_stream_cfg_t        uac_mic_cfg;     /* UAC麦克风配置 */
   } mic_cfg;
   uint32_t read_pool_size;                        /* 读取池大小 */
   bool asr_en;
   bool asr_rsp_en;
   bool aec_en;                                   /* AEC功能使能标志 */
   uint32_t asr_sample_rate;
   union
   {
      rsp_algorithm_cfg_t rsp_alg_cfg;            /* 重采样算法配置 */
      uint32_t reserved;
   }rsp_cfg;
   union
   {
      aec_v3_algorithm_cfg_t aec_alg_cfg;        /* AEC算法配置 */
      uint32_t reserved2;
   }aec_cfg;
   asr_event_handle event_handle;                /* ASR事件处理回调函数 */
   void * args;                                  /* 用户自定义参数 */
}  asr_cfg_t;
```

2. **aud\_asr\_cfg\_t**

音频ASR配置结构体。

```
typedef struct {
    asr_handle_t asr_handle;                            /* ASR句柄 */
    void *args;                                         /* 回调的私有参数 */
    int task_stack;                                     /* 任务栈大小 */
    int task_core;                                      /* 任务运行核心(0或1) */
    int task_prio;                                      /* 任务优先级 */
    audio_mem_type_t mem_type;                          /* 使用的内存类型 */
    uint32_t max_read_size;                             /* 从ASR句柄读取的最大数据大小 */
    void (*aud_asr_result_handle)(uint32_t param);      /* ASR结果处理回调（用户自定义） */
    int (*aud_asr_init)(void);                          /* ASR初始化回调 */
    int (*aud_asr_recog)(void *read_buf, uint32_t read_size, void *p1, void *p2); /* ASR识别回调 */
    void (*aud_asr_deinit)(void);                       /* ASR反初始化回调 */
} aud_asr_cfg_t;
```

3. **struct asr**

ASR服务结构体。

```
struct asr
{
   audio_element_handle_t  mic_str;            /* MIC元素 */
   mic_type_t              mic_type;           /* 板载麦克风或UAC麦克风 */
   bool                    asr_en;             /* ASR使能标志 */
   bool                    asr_rsp_en;         /* ASR源是否需要重采样 */
   bool                    aec_en;             /* AEC使能标志 */
   audio_pipeline_handle_t asr_pipeline;       /* ASR音频管道 */
   audio_element_handle_t  asr_raw_read;       /* 原始音频读取元素 */
   audio_element_handle_t  asr_rsp;            /* ASR重采样元素 */
   audio_element_handle_t  aec_alg;            /* AEC算法句柄 */
   audio_port_handle_t     aec_alg_ref_rb;     /* AEC参考环形缓冲区 */
   audio_port_handle_t     asr_in_rb;          /* ASR输入环形缓冲区 */
   audio_event_iface_handle_t asr_evt;         /* 音频事件接口 */

   asr_sta_t             status;               /* ASR句柄状态 */
   asr_event_handle      event_handle;         /* ASR事件处理回调 */
   void *                args;                 /* 事件处理函数参数 */

   beken_thread_t          listener_task_hdl;  /* 监听器任务句柄 */
   beken_queue_t           listener_msg_que;   /* 监听器消息队列 */
   beken_semaphore_t       listener_sem;       /* 监听器信号量 */
   bool                    listener_is_running; /* 监听器运行状态 */
};
```

备注

1. asr服务结构体中的字段均为内部使用，用户无需直接访问。
2. asr服务的状态和事件处理回调函数由SDK内部管理，用户无需手动调用。
3. 如果asr服务的mic输入源依赖与其他音频服务组件, 那么mic\_str需要在从源服务组件中获取，可以参考asr\_service\_example工程。

4. **asr\_sta\_t**

ASR状态枚举。

```
typedef enum {
    ASR_STA_NONE = 0,      /* 初始状态 */
    ASR_STA_IDLE,          /* 空闲状态 */
    ASR_STA_RUNNING,       /* 运行状态 */
    ASR_STA_STOPPING,      /* 停止中状态 */
    ASR_STA_STOPED         /* 已停止状态 */
} asr_sta_t;
```

5. **asr\_evt\_t**

ASR事件枚举。

```
typedef enum {
    ASR_EVT_START = 0,         /* 启动事件 */
    ASR_EVT_STOP,              /* 停止事件 */
    ASR_EVT_MIC_NOT_SUPPORT,   /* 麦克风不支持事件 */
    ASR_EVT_ERROR_UNKNOW       /* 未知错误事件 */
} asr_evt_t;
```

6. **asr\_event\_handle**

ASR事件处理回调函数类型。

```
typedef bk_err_t (*asr_event_handle)(asr_evt_t event, void *param, void *args);
```
