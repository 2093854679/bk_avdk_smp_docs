---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/audio/audio_development_kit/audio_algorithms.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# **音频算法**

<a id="id2"></a>

## **1\. 简介**

> 音频开发框架支持多种音频算法，详细列表如下：
>
> |  |  |
> | --- | --- |
> | 音频流 | 功能简介 |
> | aec\_algorithm | 回声消除 |
> | aec\_v3\_algorithm | 回声消除V3版本 |
> | agc\_algorithm | 自动增益控制 |
> | eq\_algorithm | 均衡器 |

<a id="aec"></a>

## **2\. AEC回声消除算法**

<a id="id3"></a>

### **2.1 功能配置**

> AEC回声消除算法支持mic中的回声进行消除，同时也支持NS降噪AGC增益控制。
>
> AEC回声消除支持硬回采和软回采两种工作模式：
> \- 硬回采：其中一路mic外接在板载speaker上用于采集回声，读取mic数据时同时读取mic信号和参考信号；
> \- 软回采：参考信号存储在ringbuffer中，将speaker数据写入audio dac播放前写入ringbuffer中备份，作为参考信号。
>
> 软回采较为复杂，且存在mic信号和ref参考信号对齐问题，效果没有硬回采好，建议采用硬回采的方案。
>
> 两种方案的数据流可参考下述头文件中的详细描述：
> :   `bk_avdk_smp<源代码路径>/ap/include/components/bk_audio/audio_algorithms/aec_algorithm.h`
>
> AEC算法按照配置的帧长度读取原始音频和参考信号，经过回声消除处理后，将结果输出到ringbuffer，通过 `aec_algorithm_init` 接口初始化模块。
>
> aec\_algorithm.h 中提供了默认配置： `DEFAULT_AEC_ALGORITHM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | aec\_cfg | aec参数配置 |
> | out\_block\_num | 输出音频块的数量 |

备注

1. 编码输出方式为ringbuffer，aec算法对帧的size有严格要求，通常为20ms数据，ringbuffer的size为 `size_20ms * out_block_num` 。
2. 建议将speaker输出接入其中一路mic输入，采用硬回采的工作模式。

<a id="id4"></a>

### **2.2 宏配置**

> aec回声消除宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_ADK\_AEC\_ALGORITHM | AP | bool | y |
>
> aec回声消除宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="casedemo"></a>

### **2.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_algorithms/aec_algorithm/aec_algorithm_test.c`
>
> 测试文件中提供了两种工作模式下的测试demo。

<a id="agc"></a>

## **3\. agc自动增益控制**

<a id="id5"></a>

### **3.1 功能配置**

> agc自动增益控制支持对pcm格式音频进行增益控制调节，按照配置读取原始音频，处理后输出到ringbuffer，通过 `agc_algorithm_init` 接口初始化模块。
>
> agc\_algorithm.h 中提供了默认配置： `DEFAULT_AGC_ALGORITHM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | agc\_cfg | agc参数配置 |
> | minLevel | 下限 |
> | maxLevel | 上限 |
> | fs | 采样率：8000/16000 |
> | out\_block\_size | 输出音频块的size（byte） |
> | out\_block\_num | 输出音频块的数量 |

<a id="id6"></a>

### **3.2 宏配置**

> agc自动增益控制宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_AGC\_ALGORITHM | AP | bool | y |
>
> agc自动增益控制依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="id7"></a>

### **3.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_algorithms/agc_algorithm/agc_algorithm_test.c`
>
> demo创建了一个音频pipeline，对测试音频数据进行agc算法处理，并输出处理结果。

<a id="aec-v3"></a>

## **4\. AEC V3回声消除算法**

<a id="id8"></a>

### **4.1 功能配置**

> AEC V3回声消除算法是AEC算法的升级版本，支持更先进的回声消除、降噪和自动增益控制功能。该算法支持硬回采和软回采两种工作模式，并集成了VAD（语音活动检测）功能。
>
> AEC V3算法按照配置的帧长度读取原始音频和参考信号，经过回声消除、降噪、自动增益控制处理后，将结果输出到ringbuffer，通过 `aec_v3_algorithm_init` 接口初始化模块。
>
> aec\_v3\_algorithm.h 中提供了默认配置： `DEFAULT_AEC_V3_ALGORITHM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | aec\_cfg.mode | 工作模式：HARDWARE/SOFTWARE |
> | aec\_cfg.fs | 采样率：8000/16000 |
> | aec\_cfg.delay\_points | 参考信号延迟点数 |
> | aec\_cfg.ec\_depth | 回声消除深度（1\~50） |
> | aec\_cfg.ns\_type | 降噪类型：NS\_CLOSE/NS\_AI/NS\_TRADITION |
> | aec\_cfg.ns\_level | 降噪级别（1\~8） |
> | vad\_cfg.vad\_enable | VAD功能使能 |
> | vad\_cfg.vad\_start\_threshold | VAD语音开始阈值 |
> | vad\_cfg.vad\_stop\_threshold | VAD语音结束阈值 |
> | out\_block\_size | 输出音频块大小 |
> | out\_block\_num | 输出音频块数量 |
> | dual\_ch | 双声道输入使能 |

备注

1. AEC V3算法对帧的size有严格要求，通常为20ms数据，ringbuffer的size为 `size_20ms * out_block_num` 。
2. 建议将speaker输出接入其中一路mic输入，采用硬回采的工作模式。
3. 支持双声道输入，可提供更好的降噪效果。

<a id="id9"></a>

### **4.2 宏配置**

> aec v3回声消除宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_AEC\_V3\_ALGORITHM | AP | bool | y |
>
> aec v3回声消除依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="id10"></a>

### **4.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_algorithms/aec_v3_algorithm/aec_v3_algorithm.c`
>
> 测试文件中提供了两种工作模式下的测试demo，包括硬回采和软回采模式。

<a id="eq"></a>

## **5\. EQ均衡器算法**

<a id="id11"></a>

### **5.1 功能配置**

> EQ均衡器算法支持对pcm格式音频进行均衡器处理，按照配置的滤波器参数对音频进行频域均衡调节，通过 `eq_algorithm_init` 接口初始化模块。
>
> eq\_algorithm.h 中提供了默认配置： `DEFAULT_EQ_ALGORITHM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | eq\_cal\_para.eq\_en | EQ功能使能 |
> | eq\_cal\_para.filters | 滤波器数量 |
> | eq\_cal\_para.globle\_gain | 全局增益 |
> | eq\_cal\_para.eq\_para\[\].a\[\] | 滤波器a系数 |
> | eq\_cal\_para.eq\_para\[\].b\[\] | 滤波器b系数 |
> | eq\_cal\_para.eq\_load.freq | 滤波器中心频率 |
> | eq\_cal\_para.eq\_load.gain | 滤波器增益 |
> | eq\_cal\_para.eq\_load.q\_val | 滤波器Q值 |
> | eq\_cal\_para.eq\_load.type | 滤波器类型 |
> | eq\_chl\_num | EQ声道数 |
> | eq\_frame\_size | EQ帧大小 |
> | out\_block\_num | 输出音频块数量 |

备注

1. EQ算法支持多段滤波器，可对音频进行精细的频域调节。
2. 支持高通、低通、带通、带阻等多种滤波器类型。
3. 可通过音频工具生成滤波器参数，实现自定义均衡效果。

<a id="id12"></a>

### **5.2 宏配置**

> eq均衡器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK\_EQ\_ALGORITHM | AP | bool | y |
>
> eq均衡器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG\_ADK | AP | bool | y |

<a id="id13"></a>

### **5.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_algorithms/eq_algorithm/eq_algorithm_test.c`
>
> demo创建了一个音频pipeline，对测试音频数据进行EQ算法处理，并输出处理结果。
