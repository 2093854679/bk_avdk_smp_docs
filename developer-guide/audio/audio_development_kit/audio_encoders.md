# **音频编码器**



## **1. 简介**

> 音频开发框架支持多种音频编码器，详细列表如下：
>
> |  |  |
> | --- | --- |
> | 音频流 | 功能简介 |
> | g711_encoder | g711a/u编码器 |
> | aac_encoder | aac编码器 |
> | g722_encoder | g722编码器 |
> | opus_encoder | opus编码器 |


## **2. g711a/u编码器**


### **2.1 功能配置**

> g711编码器支持对pcm格式音频进行g711编码，按照配置的帧长度读取原始音频，并编码成G711a/u格式输出到ringbuffer，通过 `g711_encoder_init` 接口初始化模块。
>
> g711_encoder.h 中提供了默认配置： `DEFAULT_G711_ENCODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | enc_mode | 编码模式：g711a/g711u |
> | buf_sz | 编码的每帧音频数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. 编码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。


### **2.2 宏配置**

> g711编码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_G711_ENCODER | AP | bool | y |
>
> g711编码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **2.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_encoders/g711_encoder/g711_encoder_test.c`
>
> demo创建了一个音频pipeline，对固定的pcm格式音频数据进行编码，并比较输出结果，进行自测试。


## **3. aac编码器**


### **3.1 功能配置**

> aac编码器支持对pcm格式音频进行aac编码，按照配置读取原始音频，并编码成aac格式输出到framebuffer，通过 `aac_encoder_init` 接口初始化模块。
>
> aac_encoder.h 中提供了默认配置： `DEFAULT_AAC_ENCODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | chl_num | 声道数 |
> | samp_rate | 采样率 |
> | bits | 声道数 |
> | modules | 编码模式（参考 `aacenc_lib.h` 中 `aacEncOpen` 接口对 `encModules` 参数的描述） |
> | aot | 音频对象类型（参考 `aacenc_lib.h` 中对 `AACENC_AOT` 参数的描述） |
> | bitrate | 编码码率（参考 `aacenc_lib.h` 中对 `AACENC_BITRATE` 参数的描述） |
> | bitrate_mode | 码率模式（参考 `aacenc_lib.h` 中对 `AACENC_BITRATEMODE` 参数的描述） |
> | sbr_mode | sbr模式（参考 `aacenc_lib.h` 中对 `AACENC_SBR_MODE` 参数的描述） |
> | granule_length | 音频帧包含采样点数（参考 `aacenc_lib.h` 中对 `AACENC_GRANULE_LENGTH` 参数的描述） |
> | chl_order | 输入音频声道顺序（参考 `aacenc_lib.h` 中对 `AACENC_CHANNELORDER` 参数的描述） |
> | afterburner_en | afterburner特性使能（参考 `aacenc_lib.h` 中对 `AACENC_AFTERBURNER` 参数的描述） |
> | transport_type | 传输类型（参考 `aacenc_lib.h` 中对 `AACENC_TRANSMUX` 参数的描述） |
> | buffer_len | 编码器内部编码输出buffer |
> | in_pool_len | 输入待编码的pcm音频缓存池size（byte） |
> | out_buffer_len | 编码一帧输出的aac数据最大size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. 编码输出方式为framebuffer，framebuffer的frame size为 `out_block_size` frame number 为 `out_block_num` 。


### **3.2 宏配置**

> aac编码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_AAC_ENCODER | AP | bool | y |
>
> aac编码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **3.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_encoders/aac_encoder/aac_encoder_test.c`
>
> demo基于 `onboard_mic_stream` 、 `aac_encoder` 和 `uart_stream` 创建了一个音频pipeline，对采集的板载mic音频数据进行aac编码，并通过uart输出编码后的数据。


## **4. g722编码器**


### **4.1 功能配置**

> g722编码器支持对pcm格式音频进行g722编码，按照配置的帧长度读取原始音频，并编码成G722格式输出到ringbuffer，通过 `g722_encoder_init` 接口初始化模块。
>
> g722_encoder.h 中提供了默认配置： `DEFAULT_G722_ENCODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | enc_rate | 编码速率：48000/56000/64000 bps |
> | buf_sz | 编码的每帧音频数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |
> | task_stack | 编码器任务栈大小 |
> | task_prio | 编码器任务优先级 |
> | task_core | 编码器任务运行核心 |

备注

1. 编码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。
2. 支持的编码速率有三种：48000 bps、56000 bps和64000 bps，对应不同的压缩比。


### **4.2 宏配置**

> g722编码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_G722_ENCODER | AP | bool | y |
>
> g722编码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **4.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_encoders/g722_encoder/g722_encoder_test.c`
>
> demo创建了一个音频pipeline，对固定的pcm格式音频数据进行编码，并验证编码结果的正确性。


## **5. opus编码器**


### **5.1 功能配置**

> opus编码器支持对pcm格式音频进行opus编码，按照配置的帧长度读取原始音频，并编码成opus格式输出到ringbuffer，通过 `opus_enc_init` 接口初始化模块。
>
> opus_enc.h 中提供了默认配置： `DEFAULT_OPUS_ENC_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | enc_mode | 编码模式：VOIP/AUDIO/RESTRICTED_LOWDELAY |
> | sample_rate | 采样率：8000/12000/16000/24000/48000 |
> | channels | 声道数：1(单声道)/2(立体声) |
> | bitrate | 编码码率（bps） |
> | frame_samples_per_channel | 每声道帧采样点数 |
> | buf_sz | 编码的每帧音频数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |
> | task_stack | 编码器任务栈大小 |
> | task_prio | 编码器任务优先级 |
> | task_core | 编码器任务运行核心 |

备注

1. 编码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。
2. opus编码器支持多种采样率和声道配置，具有优秀的压缩比和音质。
3. 支持VBR（可变码率）和CBR（固定码率）编码模式。


### **5.2 宏配置**

> opus编码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_OPUS_ENCODER | AP | bool | y |
>
> opus编码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **5.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_encoders/opus_enc/opus_enc_test.c`
>
> demo创建了一个音频pipeline，对固定的pcm格式音频数据进行opus编码，并验证编码结果的正确性。
