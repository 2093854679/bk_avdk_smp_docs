# **音频解码器**



## **1. 简介**

> 音频开发框架支持多种音频编码器，详细列表如下：
>
> |  |  |
> | --- | --- |
> | 音频流 | 功能简介 |
> | g711_decoder | g711a/u解码器 |
> | mp3_decoder | mp3解码器 |
> | aac_decoder | aac解码器 |
> | g722_decoder | g722解码器 |
> | wav_decoder | wav解码器 |
> | opus_decoder | opus解码器 |


## **2. g711a/u解码器**


### **2.1 功能配置**

> g711解码器支持对g711格式音频进行解码，读取g711音频，并解码成pcm格式输出到ringbuffer，通过 `g711_decoder_init` 接口初始化模块。
>
> g711_decoder.h 中提供了默认配置： `DEFAULT_G711_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | dec_mode | 解码模式：g711a/g711u |
> | buf_sz | 解码的每帧音频数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. 解码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。


### **2.2 宏配置**

> g711解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_G711_DECODER | AP | bool | y |
>
> g711解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **2.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/g711_decoder/g711_decoder_test.c`
>
> demo创建了一个音频pipeline，对固定的g711格式音频数据进行解码，并比较输出结果，进行自测试。


## **3. mp3解码器**


### **3.1 功能配置**

> mp3解码器支持对mp3格式音频进行编码，读取mp3音频，解码成pcm格式输出到ringbuffer，通过 `mp3_decoder_init` 接口初始化模块。
>
> mp3_decoder.h 中提供了默认配置： `DEFAULT_MP3_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | main_buff_size | mp3解码的输入size（byte） |
> | out_pcm_buff_size | mp3解码一帧输出pcm数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. `main_buff_size` 值的设置和输入mp3音频数据的声道数有关， 详情可参考： `mp3dec.h` 中宏定义 `MAINBUF_SIZE` 的说明。
2. `out_pcm_buff_size` 的值必须大于等于解码一帧mp3输出的pcm数据的size，否则解码时会内存越界。


### **3.2 宏配置**

> mp3解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_MP3_DECODER | AP | bool | y |
>
> mp3解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **3.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/mp3_decoder/mp3_decoder_test.c`
>
> demo基于 `fatfs_stream` 、和 `mp3_decoder` 创建了一个音频pipeline，读取sdcard中的mp3音频数据进行mp3编码，并将解码后的pcm数据写回sdcard。


## **4. aac解码器**


### **4.1 功能配置**

> aac解码器支持对aac格式音频进行编码，读取aac音频，解码成pcm格式输出到ringbuffer，通过 `aac_decoder_init` 接口初始化模块。
>
> aac_decoder.h 中提供了默认配置： `DEFAULT_AAC_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | main_buff_size | aac解码的输入size（byte） |
> | out_pcm_buff_size | aac解码一帧输出pcm数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. `main_buff_size` 值的设置和输入aac音频数据的声道数有关， 详情可参考： `aacdec.h` 中宏定义 `AAC_MAINBUF_SIZE` 的说明。
2. `out_pcm_buff_size` 的值必须大于等于解码一帧aac输出的pcm数据的size，否则解码时会内存越界。


### **4.2 宏配置**

> aac解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_AAC_DECODER | AP | bool | y |
>
> aac解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **4.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/aac_decoder/aac_decoder_test.c`
>
> demo基于 `onboard_mic_stream` 、 `aac_encoder` 、 ``` aac_decoder``和 ``uart_stream ``` 创建了一个音频pipeline，对采集的板载mic音频数据进行aac编码和aac解码，最后通过uart输出经过编解码后的数据。


## **5. g722解码器**


### **5.1 功能配置**

> g722解码器支持对g722格式音频进行解码，读取g722音频，并解码成pcm格式输出到ringbuffer，通过 `g722_decoder_init` 接口初始化模块。
>
> g722_decoder.h 中提供了默认配置： `DEFAULT_G722_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | buf_sz | 解码的每帧音频数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |
> | task_stack | 解码任务的堆栈大小 |
> | task_prio | 解码任务的优先级 |
> | task_core | 解码任务运行的核编号 |
> | rate | 采样率 |
> | options | 解码选项（如G722_SAMPLE_RATE_8000表示8kHz采样率） |

备注

1. 解码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。
2. 对于8kHz模式，输出PCM数据长度与输入相同；对于16kHz模式，输出PCM数据长度是输入的两倍。


### **5.2 宏配置**

> g722解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_G722_DECODER | AP | bool | y |
>
> g722解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **5.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/g722_decoder/g722_decoder_test.c`
>
> demo创建了一个音频pipeline，对固定的g722格式音频数据进行解码，并比较输出结果，进行自测试。


## **6. wav解码器**


### **6.1 功能配置**

> wav解码器支持对wav格式音频进行解码，读取wav音频，解码成pcm格式输出到ringbuffer，通过 `wav_decoder_init` 接口初始化模块。
>
> wav_decoder.h 中提供了默认配置： `DEFAULT_WAV_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | buf_sz | 解码的每帧音频数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |
> | task_stack | 解码任务的堆栈大小 |
> | task_prio | 解码任务的优先级 |
> | task_core | 解码任务运行的核编号 |

备注

1. 解码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。
2. wav解码器会自动解析wav文件头，获取音频的采样率、声道数和位深等信息。


### **6.2 宏配置**

> wav解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_WAV_DECODER | AP | bool | y |
>
> wav解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **6.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/wav_decoder/wav_decoder_test.c`
>
> demo创建了一个音频pipeline，对wav格式音频文件进行解码，并验证解码后的pcm数据。


## **7. opus解码器**


### **7.1 功能配置**

> opus解码器支持对opus格式音频进行解码，读取opus音频，并解码成pcm格式输出到ringbuffer，通过 `opus_dec_init` 接口初始化模块。
>
> opus_dec.h 中提供了默认配置： `DEFAULT_OPUS_DEC_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | sample_rate | 采样率：8000/12000/16000/24000/48000 |
> | channels | 声道数：1(单声道)/2(立体声) |
> | buf_sz | 解码的每帧音频数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |
> | task_stack | 解码器任务栈大小 |
> | task_prio | 解码器任务优先级 |
> | task_core | 解码器任务运行核心 |

备注

1. 解码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。
2. opus解码器支持多种采样率和声道配置，具有优秀的音质和低延迟特性。
3. 支持动态码率调整，能够适应网络条件变化。


### **7.2 宏配置**

> opus解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_OPUS_DECODER | AP | bool | y |
>
> opus解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **7.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/opus_dec/opus_dec_test.c`
>
> demo创建了一个音频pipeline，对opus格式音频数据进行解码，并验证解码后的pcm数据。
