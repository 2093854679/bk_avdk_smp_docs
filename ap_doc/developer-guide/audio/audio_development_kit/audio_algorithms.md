# **音频算法**



## **1. 简介**

> 音频开发框架支持多种音频算法，详细列表如下：
>
> |  |  |
> | --- | --- |
> | 音频流 | 功能简介 |
> | aec_algorithm | 回声消除 |
> | aec_v3_algorithm | 回声消除V3版本 |
> | agc_algorithm | 自动增益控制 |
> | eq_algorithm | 均衡器 |


## **2. AEC回声消除算法**


### **2.1 功能配置**

> AEC回声消除算法支持mic中的回声进行消除，同时也支持NS降噪AGC增益控制。
>
> AEC回声消除支持硬回采和软回采两种工作模式：
> - 硬回采：其中一路mic外接在板载speaker上用于采集回声，读取mic数据时同时读取mic信号和参考信号；
> - 软回采：参考信号存储在ringbuffer中，将speaker数据写入audio dac播放前写入ringbuffer中备份，作为参考信号。
>
> 软回采较为复杂，且存在mic信号和ref参考信号对齐问题，效果没有硬回采好，建议采用硬回采的方案。
>
> 两种方案的数据流可参考下述头文件中的详细描述：
> :   `bk_avdk_smp<源代码路径>/ap/include/components/bk_audio/audio_algorithms/aec_algorithm.h`
>
> AEC算法按照配置的帧长度读取原始音频和参考信号，经过回声消除处理后，将结果输出到ringbuffer，通过 `aec_algorithm_init` 接口初始化模块。
>
> aec_algorithm.h 中提供了默认配置： `DEFAULT_AEC_ALGORITHM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | aec_cfg | aec参数配置 |
> | out_block_num | 输出音频块的数量 |

备注

1. 编码输出方式为ringbuffer，aec算法对帧的size有严格要求，通常为20ms数据，ringbuffer的size为 `size_20ms * out_block_num` 。
2. 建议将speaker输出接入其中一路mic输入，采用硬回采的工作模式。


### **2.2 宏配置**

> aec回声消除宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_ADK_AEC_ALGORITHM | AP | bool | y |
>
> aec回声消除宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **2.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_algorithms/aec_algorithm/aec_algorithm_test.c`
>
> 测试文件中提供了两种工作模式下的测试demo。


## **3. agc自动增益控制**


### **3.1 功能配置**

> agc自动增益控制支持对pcm格式音频进行增益控制调节，按照配置读取原始音频，处理后输出到ringbuffer，通过 `agc_algorithm_init` 接口初始化模块。
>
> agc_algorithm.h 中提供了默认配置： `DEFAULT_AGC_ALGORITHM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | agc_cfg | agc参数配置 |
> | minLevel | 下限 |
> | maxLevel | 上限 |
> | fs | 采样率：8000/16000 |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |


### **3.2 宏配置**

> agc自动增益控制宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_AGC_ALGORITHM | AP | bool | y |
>
> agc自动增益控制依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **3.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_algorithms/agc_algorithm/agc_algorithm_test.c`
>
> demo创建了一个音频pipeline，对测试音频数据进行agc算法处理，并输出处理结果。


## **4. AEC V3回声消除算法**


### **4.1 功能配置**

> AEC V3回声消除算法是AEC算法的升级版本，支持更先进的回声消除、降噪和自动增益控制功能。该算法支持硬回采和软回采两种工作模式，并集成了VAD（语音活动检测）功能。
>
> AEC V3算法按照配置的帧长度读取原始音频和参考信号，经过回声消除、降噪、自动增益控制处理后，将结果输出到ringbuffer，通过 `aec_v3_algorithm_init` 接口初始化模块。
>
> aec_v3_algorithm.h 中提供了默认配置： `DEFAULT_AEC_V3_ALGORITHM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | aec_cfg.mode | 工作模式：HARDWARE/SOFTWARE |
> | aec_cfg.fs | 采样率：8000/16000 |
> | aec_cfg.delay_points | 参考信号延迟点数 |
> | aec_cfg.ec_depth | 回声消除深度（1~50） |
> | aec_cfg.ns_type | 降噪类型：NS_CLOSE/NS_AI/NS_TRADITION |
> | aec_cfg.ns_level | 降噪级别（1~8） |
> | vad_cfg.vad_enable | VAD功能使能 |
> | vad_cfg.vad_start_threshold | VAD语音开始阈值 |
> | vad_cfg.vad_stop_threshold | VAD语音结束阈值 |
> | out_block_size | 输出音频块大小 |
> | out_block_num | 输出音频块数量 |
> | dual_ch | 双声道输入使能 |

备注

1. AEC V3算法对帧的size有严格要求，通常为20ms数据，ringbuffer的size为 `size_20ms * out_block_num` 。
2. 建议将speaker输出接入其中一路mic输入，采用硬回采的工作模式。
3. 支持双声道输入，可提供更好的降噪效果。


### **4.2 宏配置**

> aec v3回声消除宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_AEC_V3_ALGORITHM | AP | bool | y |
>
> aec v3回声消除依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **4.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_algorithms/aec_v3_algorithm/aec_v3_algorithm.c`
>
> 测试文件中提供了两种工作模式下的测试demo，包括硬回采和软回采模式。


## **5. EQ均衡器算法**


### **5.1 功能配置**

> EQ均衡器算法支持对pcm格式音频进行均衡器处理，按照配置的滤波器参数对音频进行频域均衡调节，通过 `eq_algorithm_init` 接口初始化模块。
>
> eq_algorithm.h 中提供了默认配置： `DEFAULT_EQ_ALGORITHM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | eq_cal_para.eq_en | EQ功能使能 |
> | eq_cal_para.filters | 滤波器数量 |
> | eq_cal_para.globle_gain | 全局增益 |
> | eq_cal_para.eq_para[].a[] | 滤波器a系数 |
> | eq_cal_para.eq_para[].b[] | 滤波器b系数 |
> | eq_cal_para.eq_load.freq | 滤波器中心频率 |
> | eq_cal_para.eq_load.gain | 滤波器增益 |
> | eq_cal_para.eq_load.q_val | 滤波器Q值 |
> | eq_cal_para.eq_load.type | 滤波器类型 |
> | eq_chl_num | EQ声道数 |
> | eq_frame_size | EQ帧大小 |
> | out_block_num | 输出音频块数量 |

备注

1. EQ算法支持多段滤波器，可对音频进行精细的频域调节。
2. 支持高通、低通、带通、带阻等多种滤波器类型。
3. 可通过音频工具生成滤波器参数，实现自定义均衡效果。


### **5.2 宏配置**

> eq均衡器宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_EQ_ALGORITHM | AP | bool | y |
>
> eq均衡器依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **5.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_algorithms/eq_algorithm/eq_algorithm_test.c`
>
> demo创建了一个音频pipeline，对测试音频数据进行EQ算法处理，并输出处理结果。
