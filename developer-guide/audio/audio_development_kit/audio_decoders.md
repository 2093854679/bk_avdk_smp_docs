---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/audio/audio_development_kit/audio_decoders.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# **音频解码器**

<a id="id2"></a>

## **1\. 简介**

> 音频开发框架支持多种音频编码器，详细列表如下：
>
> |  |  |
> | --- | --- |
> | 音频流 | 功能简介 |
> | g711\_decoder | g711a/u解码器 |
> | mp3\_decoder | mp3解码器 |
> | aac\_decoder | aac解码器 |
> | g722\_decoder | g722解码器 |
> | wav\_decoder | wav解码器 |
> | opus\_decoder | opus解码器 |

<a id="g711a-u"></a>

## **2\. g711a/u解码器**

<a id="id3"></a>

### **2.1 功能配置**

> g711解码器支持对g711格式音频进行解码，读取g711音频，并解码成pcm格式输出到ringbuffer，通过 `g711_decoder_init` 接口初始化模块。
>
> g711\_decoder.h 中提供了默认配置： `DEFAULT_G711_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | dec\_mode | 解码模式：g711a/g711u |
> | buf\_sz | 解码的每帧音频数据的size（byte） |
> | out\_block\_size | 输出音频块的size（byte） |
> | out\_block\_num | 输出音频块的数量 |

备注

1. 解码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。

<a id="id4"></a>

### **2.2 宏配置**

> g711解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_G711\_DECODER | AP | bool | y |
>
> g711解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="casedemo"></a>

### **2.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/g711_decoder/g711_decoder_test.c`
>
> demo创建了一个音频pipeline，对固定的g711格式音频数据进行解码，并比较输出结果，进行自测试。

<a id="mp3"></a>

## **3\. mp3解码器**

<a id="id5"></a>

### **3.1 功能配置**

> mp3解码器支持对mp3格式音频进行编码，读取mp3音频，解码成pcm格式输出到ringbuffer，通过 `mp3_decoder_init` 接口初始化模块。
>
> mp3\_decoder.h 中提供了默认配置： `DEFAULT_MP3_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | main\_buff\_size | mp3解码的输入size（byte） |
> | out\_pcm\_buff\_size | mp3解码一帧输出pcm数据的size（byte） |
> | out\_block\_size | 输出音频块的size（byte） |
> | out\_block\_num | 输出音频块的数量 |

备注

1. `main_buff_size` 值的设置和输入mp3音频数据的声道数有关， 详情可参考： `mp3dec.h` 中宏定义 `MAINBUF_SIZE` 的说明。
2. `out_pcm_buff_size` 的值必须大于等于解码一帧mp3输出的pcm数据的size，否则解码时会内存越界。

<a id="id6"></a>

### **3.2 宏配置**

> mp3解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_MP3\_DECODER | AP | bool | y |
>
> mp3解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="id7"></a>

### **3.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/mp3_decoder/mp3_decoder_test.c`
>
> demo基于 `fatfs_stream` 、和 `mp3_decoder` 创建了一个音频pipeline，读取sdcard中的mp3音频数据进行mp3编码，并将解码后的pcm数据写回sdcard。

<a id="aac"></a>

## **4\. aac解码器**

<a id="id8"></a>

### **4.1 功能配置**

> aac解码器支持对aac格式音频进行编码，读取aac音频，解码成pcm格式输出到ringbuffer，通过 `aac_decoder_init` 接口初始化模块。
>
> aac\_decoder.h 中提供了默认配置： `DEFAULT_AAC_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | main\_buff\_size | aac解码的输入size（byte） |
> | out\_pcm\_buff\_size | aac解码一帧输出pcm数据的size（byte） |
> | out\_block\_size | 输出音频块的size（byte） |
> | out\_block\_num | 输出音频块的数量 |

备注

1. `main_buff_size` 值的设置和输入aac音频数据的声道数有关， 详情可参考： `aacdec.h` 中宏定义 `AAC_MAINBUF_SIZE` 的说明。
2. `out_pcm_buff_size` 的值必须大于等于解码一帧aac输出的pcm数据的size，否则解码时会内存越界。

<a id="id9"></a>

### **4.2 宏配置**

> aac解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_AAC\_DECODER | AP | bool | y |
>
> aac解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="id10"></a>

### **4.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/aac_decoder/aac_decoder_test.c`
>
> demo基于 `onboard_mic_stream` 、 `aac_encoder` 、 ``` aac_decoder``和 ``uart_stream ``` 创建了一个音频pipeline，对采集的板载mic音频数据进行aac编码和aac解码，最后通过uart输出经过编解码后的数据。

<a id="g722"></a>

## **5\. g722解码器**

<a id="id11"></a>

### **5.1 功能配置**

> g722解码器支持对g722格式音频进行解码，读取g722音频，并解码成pcm格式输出到ringbuffer，通过 `g722_decoder_init` 接口初始化模块。
>
> g722\_decoder.h 中提供了默认配置： `DEFAULT_G722_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | buf\_sz | 解码的每帧音频数据的size（byte） |
> | out\_block\_size | 输出音频块的size（byte） |
> | out\_block\_num | 输出音频块的数量 |
> | task\_stack | 解码任务的堆栈大小 |
> | task\_prio | 解码任务的优先级 |
> | task\_core | 解码任务运行的核编号 |
> | rate | 采样率 |
> | options | 解码选项（如G722\_SAMPLE\_RATE\_8000表示8kHz采样率） |

备注

1. 解码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。
2. 对于8kHz模式，输出PCM数据长度与输入相同；对于16kHz模式，输出PCM数据长度是输入的两倍。

<a id="id12"></a>

### **5.2 宏配置**

> g722解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_G722\_DECODER | AP | bool | y |
>
> g722解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="id13"></a>

### **5.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/g722_decoder/g722_decoder_test.c`
>
> demo创建了一个音频pipeline，对固定的g722格式音频数据进行解码，并比较输出结果，进行自测试。

<a id="wav"></a>

## **6\. wav解码器**

<a id="id14"></a>

### **6.1 功能配置**

> wav解码器支持对wav格式音频进行解码，读取wav音频，解码成pcm格式输出到ringbuffer，通过 `wav_decoder_init` 接口初始化模块。
>
> wav\_decoder.h 中提供了默认配置： `DEFAULT_WAV_DECODER_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | buf\_sz | 解码的每帧音频数据的size（byte） |
> | out\_block\_size | 输出音频块的size（byte） |
> | out\_block\_num | 输出音频块的数量 |
> | task\_stack | 解码任务的堆栈大小 |
> | task\_prio | 解码任务的优先级 |
> | task\_core | 解码任务运行的核编号 |

备注

1. 解码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。
2. wav解码器会自动解析wav文件头，获取音频的采样率、声道数和位深等信息。

<a id="id15"></a>

### **6.2 宏配置**

> wav解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_WAV\_DECODER | AP | bool | y |
>
> wav解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="id16"></a>

### **6.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/wav_decoder/wav_decoder_test.c`
>
> demo创建了一个音频pipeline，对wav格式音频文件进行解码，并验证解码后的pcm数据。

<a id="opus"></a>

## **7\. opus解码器**

<a id="id17"></a>

### **7.1 功能配置**

> opus解码器支持对opus格式音频进行解码，读取opus音频，并解码成pcm格式输出到ringbuffer，通过 `opus_dec_init` 接口初始化模块。
>
> opus\_dec.h 中提供了默认配置： `DEFAULT_OPUS_DEC_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | sample\_rate | 采样率：8000/12000/16000/24000/48000 |
> | channels | 声道数：1(单声道)/2(立体声) |
> | buf\_sz | 解码的每帧音频数据的size（byte） |
> | out\_block\_size | 输出音频块的size（byte） |
> | out\_block\_num | 输出音频块的数量 |
> | task\_stack | 解码器任务栈大小 |
> | task\_prio | 解码器任务优先级 |
> | task\_core | 解码器任务运行核心 |

备注

1. 解码输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。
2. opus解码器支持多种采样率和声道配置，具有优秀的音质和低延迟特性。
3. 支持动态码率调整，能够适应网络条件变化。

<a id="id18"></a>

### **7.2 宏配置**

> opus解码器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_OPUS\_DECODER | AP | bool | y |
>
> opus解码器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="id19"></a>

### **7.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_decoders/opus_dec/opus_dec_test.c`
>
> demo创建了一个音频pipeline，对opus格式音频数据进行解码，并验证解码后的pcm数据。
