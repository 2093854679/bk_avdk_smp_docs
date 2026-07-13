# **音频流**



## **1. 简介**

> 音频开发框架支持多种音频流，详细列表如下：
>
> |  |  |
> | --- | --- |
> | 音频流 | 功能简介 |
> | onboard_mic_stream | 板载麦克采集音频 |
> | onboard_speaker_stream | 板载喇叭播放音频 |
> | uac_mic_stream | uac麦克采集音频 |
> | uac_speaker_stream | uac喇叭播放音频 |
> | vfs_stream | 文件系统读写音频 |
> | uart_stream | uart读写音频 |
> | raw_stream | 原始音频流读写 |
> | array_stream | 数组音频流读写 |


## **2. 板载mic流**


### **2.1 功能配置**

> 板载mic流支持采集板载模拟mic音频，按照配置的帧长度采集音频并输出到ringbuffer，通过 `onboard_mic_stream_init` 接口初始化模块。
>
> onboard_mic_stream.h 中提供了默认配置： `DEFAULT_ONBOARD_MIC_ADC_STREAM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | adc_cfg | 模拟mic参数配置（包含声道数、位宽、采样率、增益等） |
> | frame_size | 每帧音频数据的size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. 板载mic流输出方式为ringbuffer，ringbuffer的size为 `out_block_size * out_block_num` 。
2. 模拟mic的数字增益 `dig_gain` 的取值范围为： `0x00 ~ 0x3f` ,对应的增益设置为 `-45db ~ 18db` ，其中 `0x2d 为 0db` 。
3. 模块还提供了其他的功能接口，如数字增益设置、数字增益获取等，详情请参考头文件： `onboard_mic_stream.h` 中对接口的详细说明。


### **2.2 宏配置**

> 板载mic流宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_ONBOARD_MIC_STREAM | AP | bool | y |
>
> 板载mic流依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_AUDIO_ADC | AP | bool | y |
> | CONFIG_ADK | AP | bool | y |


### **2.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_streams/onboard_mic_stream/onboard_mic_stream_test.c`
>
> demo基于 `onboard_mic_stream` 和 `uart_stream` 模块创建了一个音频pipeline，采集模拟mic音频，并输出至uart串口，通过uart工具可以将uart输出的音频保存，在pc上验证。


## **3. 板载speaker流**


### **3.1 功能配置**

> 板载speaker流支持板载speaker播放，按照配置的帧长度从audio port读取音频并播放，通过 `onboard_speaker_stream_init` 接口初始化模块。
>
> onboard_speaker_stream.h 中提供了默认配置： `DEFAULT_ONBOARD_SPEAKER_STREAM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | chl_num | 喇叭声道数 |
> | sample_rate | 采样率 |
> | dig_gain | 数字增益，取值范围：0x00 ~ 0x3f(-45db ~ 18db，0x2d: 0db)，建议：0x2d |
> | ana_gain | 模拟增益，取值范围：0x00 ~ 0x3f(-15db ~ 0db，1db/step)，建议：0x0A |
> | work_mode | 喇叭工作模式：差分(AUD_DAC_WORK_MODE_DIFFEN)或单端(AUD_DAC_WORK_MODE_SIGNAL) |
> | bits | 音频位宽（only support 16 bits） |
> | clk_src | 音频时钟源：XTAL(26MHz)/APLL |
> | multi_in_port_num | 多路输入的端口数量（一般不需要多路输入，配置为0） |
> | multi_out_port_num | 多路输出的端口数量（一般不需要多路输出，配置为0） |
> | frame_size | 喇叭播放的每帧数据的size（byte），建议配置为20ms的数据量 |
> | pool_length | 缓存池子的size（byte） |
> | pool_play_thold | 缓存池播放的阈值（当池子中的数据量大于阈值就开始播放） |
> | pool_pause_thold | 缓存池暂停的阈值（当池子中的数据量小于阈值就暂停播放） |
> | pa_ctrl_en | 控制PA使能开关 |
> | pa_ctrl_gpio | 控制PA的GPIO编号 |
> | pa_on_level | 打开PA的GPIO电平，0：低电平，1：高电平 |
> | pa_on_delay | 使能audio dac后，延迟多久(ms)打开PA。[dac初始化 -> 延迟 -> pa打开] |
> | pa_off_delay | 关闭PA后，延迟多久(ms)禁用audio dac。[静音 -> pa关闭 -> 延迟 -> dac去初始化] |

备注

1. 模拟speaker的数字增益 `dig_gain` 的取值范围为： `0x00 ~ 0x3f` ,对应的增益设置为 `-45db ~ 18db` ，其中 `0x2d 为 0db` 。
2. 模拟speaker的模拟增益 `ana_gain` 的取值范围为： `0x00 ~ 0x3f` ,对应的增益设置为 `-15db ~ 0db, 1db/step` ，在满足幅度要求的情况下，模拟增益设置的越小底噪抑制效果越好。
3. 当 `multi_out_port_num` 大于0，且配置了输出的端口时，模块会在播放数据的同时，将speaker数据输出到配置的端口。
4. 模块支持通过内部缓存池控制播放和暂停，避免播放时持续卡顿（暂不支持，还在开发中）。
5. 模块支持多播放源切换功能，当 `multi_in_port_num` 大于0，且配置了输入的端口时，模块会根据多音源的优先级配置动态切换端口读取音频数据播放。
6. 当 `pa_ctrl_en` 设置为 `true` 时，模块会通过GPIO控制PA的开启和关闭，需要配置 `pa_ctrl_gpio` 、 `pa_on_level` 、 `pa_on_delay` 和 `pa_off_delay` 参数。
7. 模块还提供了其他的功能接口，如数字增益设置/获取、模拟增益设置/获取、静音控制等，详情请参考头文件： `onboard_speaker_stream.h` 中对接口的详细说明。


### **3.2 宏配置**

> 板载speaker流宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_ONBOARD_SPEAKER_STREAM | AP | bool | y |
>
> 板载speaker流依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_AUDIO_DAC | AP | bool | y |
> | CONFIG_ADK | AP | bool | y |
>
> 可选功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_ONBOARD_SPEAKER_STREAM_SUPPORT_MULTIPLE_SOURCE | AP | bool | y |

备注

1. 当模块需要动态切换播放多路音频时，需要配置 `CONFIG_ADK_ONBOARD_SPEAKER_STREAM_SUPPORT_MULTIPLE_SOURCE` 为 `y` ， 默认情况下无需打开。


### **3.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_streams/onboard_speaker_stream/onboard_speaker_stream_test.c`
>
> demo创建了一个音频pipeline，通过板载speaker循环播放数组中的提示音。


### **3.4 多播放源动态切换功能说明**

> 多播放源动态切换功能会根据配置的多路数据源的优先级，优先读取高优先级且存在有效数据的播放源数据进行播放。

重要

使用多播放源动态切换功能时需要进行以下配置：

1. 配置 `CONFIG_ADK_ONBOARD_SPEAKER_STREAM_SUPPORT_MULTIPLE_SOURCE` 为 `y` ， 打开多播放源动态切换功能。
2. 根据播放源的数量配置模块的初始化参数 `multi_in_port_num` 。
3. 准备好播放源，并通过接口 `onboard_speaker_stream_set_input_port_info` 将播放源绑定到指定的port端口。


## **4. uac mic流**


### **4.1 功能配置**

> uac mic流支持获取uac mic音频，按照配置的帧长度采集音频并输出到ringbuffer，通过 `uac_mic_stream_init` 接口初始化模块。
>
> uac_mic_stream.h 中提供了默认配置： `DEFAULT_UAC_MIC_STREAM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | port_index | usb hub端口 |
> | format | 音频格式（通常都是AUDIO_FORMAT_PCM格式，直接获取pcm音频） |
> | chl_num | 声道数 |
> | bits | 音频数据位宽 |
> | sanple_rate | 采样率 |
> | frame_size | 从usb驱动获取每帧数据的size（byte） |
> | auto_connect | 异常断开重连（热插拔）配置 |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. 如果没有打开usb hub功能，则 port_index 必须配置为 `USB_HUB_PORT_1` 。
2. 通过设置 `auto_connect = true` 可以支持热插拔功能。


### **4.2 宏配置**

> uac mic流宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_UAC_MIC_STREAM | AP | bool | y |
>
> uac mic流依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_USBH_UAC | AP | bool | y |
> | CONFIG_ADK | AP | bool | y |


### **4.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_streams/uac_mic_stream/uac_mic_stream_test.c`
>
> demo基于 `uac_mic_stream` 和 `uart_stream` 模块创建了一个音频pipeline，获取uac mic音频，并输出至uart串口，通过uart工具可以将uart输出的音频保存，在pc上验证。


## **5. uac speaker流**


### **5.1 功能配置**

> uac speaker流支持uac speaker播放，按照配置的帧长度从audio port读取音频并播放，通过 `uac_speaker_stream_init` 接口初始化模块。
>
> uac_speaker_stream.h 中提供了默认配置： `DEFAULT_UAC_SPEAKER_STREAM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | port_index | usb hub端口 |
> | format | 音频格式（通常都是AUDIO_FORMAT_PCM格式，直接获取pcm音频） |
> | chl_num | 喇叭声道数 |
> | bits | 音频位宽 |
> | sample_rate | 采样率 |
> | multi_out_port_num | 多路输出的端口数量（一般不需要多路输出，配置为0） |
> | frame_size | 喇叭播放的每帧数据的size（byte） |
> | volume | 音量 |
> | auto_connect | 异常断开重连（热插拔）配置 |
> | pool_length | 缓存池子的size（byte） |
> | pool_play_thold | 缓存池播放的阈值（当池子中的数据量大于阈值就开始播放） |
> | pool_pause_thold | 缓存池暂停的阈值（当池子中的数据量小于阈值就暂停播放） |

备注

1. 如果没有打开usb hub功能，则 port_index 必须配置为 `USB_HUB_PORT_1` 。
2. 通过设置 `auto_connect = true` 可以支持热插拔功能。
3. 当 `multi_out_port_num` 大于0，且配置了输出的端口时，模块会在播放数据的同时，将speaker数据输出到配置的端口。
4. 模块支持通过内部缓存池控制播放和暂停，避免播放时持续卡顿（暂不支持，还在开发中）。


### **5.2 宏配置**

> uac speaker流宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_UAC_SPEAKER_STREAM | AP | bool | y |
>
> uac speaker流依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_USBH_UAC | AP | bool | y |
> | CONFIG_ADK | AP | bool | y |


### **5.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_streams/uac_speaker_stream/uac_speaker_stream_test.c`
>
> demo基于 `uac_speaker_stream` 和 `raw_stream` 创建了一个音频pipeline，通过uac speaker循环播放正弦信号。


## **6. vfs流**


### **6.1 功能配置**

> vfs流支持VFS文件系统读写音频文件，按照配置的帧长度操作文件系统读写音频数据，通过 `vfs_stream_init` 接口初始化模块。
>
> 通过 `audio_element_set_uri` 接口设置操作的文件名。
>
> 当从文件中读取音频时，将读取的音频数据输出到ringbuffer中；当向文件写入音频时，将接收的音频数据写入文件。
>
> vfs_stream.h 中提供了默认配置： `DEFAULT_VFS_STREAM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | type | 配置文件操作类型：读文件或者写文件 |
> | bus_sz | 配置每次读写操作的最大数据包size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. `out_block_size` 和 `out_block_num` 仅在读文件时有效，用来配置输出缓存ringbuffer的size。
2. 此组件不支持文件系统的挂载操作，在使用前，需要客户在应用层执行mount操作。


### **6.2 宏配置**

> vfs流宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_VFS_STREAM | AP | bool | y |
>
> vfs流依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_VFS | AP | bool | y |
> | CONFIG_ADK | AP | bool | y |


### **6.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_streams/vfs_stream/vfs_stream_test.c`
>
> demo创建了一个pipeline，通过vfs stream实现文件复制功能。测试用例包括内存泄漏测试和文件读写测试，通过创建vfs_stream reader/writer元素组成pipeline，实现从/sd0/aec_mic.pcm读取数据并写入/sd0/aec_mic_bk.pcm。


## **7. raw流**


### **7.1 功能配置**

> raw流是一种特殊的组件，用于读写audio port端口缓存中的原始数据。通过在pipeline的头部或者尾部串接raw流，可以实现pipeline数据的读写操作。
>
> 通过 `raw_stream_init` 接口初始化模块。
>
> 通过 `raw_stream_read` 读取上一级组件输出到audio port中的数据。
>
> 通过 `raw_stream_write` 将数据写入下一级组件输入的audio port中。
>
> raw_stream.h 中提供了默认配置： `DEFAULT_RAW_STREAM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | type | 配置操作类型：读/写 |
> | bus_sz | 配置每次读写操作的最大数据包size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. `out_block_size` 和 `out_block_num` 仅在操作类型就write时有效，用来配置输出缓存ringbuffer的size。


### **7.2 宏配置**

> raw流宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_RAW_STREAM | AP | bool | y |
>
> raw流依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **7.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_streams/raw_stream/raw_stream_test.c`
>
> demo创建了两个pipeline，分别是record_pipeline和play_pipeline。
>
> record_pipeline 由 onboard_mic_stream 和 raw_stream 顺序构成，其中raw_stream类型为read，实现mic数据的读取。
>
> play_pipeline 由 raw_stream 和 onboard_mic_stream 顺序构成，其中raw_stream类型为write，实现speaker数据的写入。
>
> 此外demo还创建了一个user app，user app 调用raw_stream_read接口从record_pipeline读取音频数据，然后通过调用raw_stream_write接口将读取的数据写入play_pipeline播放。实现板载音频的自回环测试功能。


## **8. uart流**


### **8.1 功能配置**

> uart流支持通过uart读写音频，按照配置的帧长度操作文件系统读写音频数据，通过 `uart_stream_init` 接口初始化模块。
>
> 当从uart接收音频时，将接收的音频数据输出到ringbuffer中。
>
> uart_stream.h 中提供了默认配置： `DEFAULT_UART_STREAM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | uart_id | 配置使用的uart号 |
> | baud_rate | 配置波特率 |
> | type | 配置操作类型：读/写 |
> | buffer_len | 配置每次读写操作的数据包size（byte） |
> | out_block_size | 输出音频块的size（byte） |
> | out_block_num | 输出音频块的数量 |

备注

1. `out_block_size` 和 `out_block_num` 仅在读时有效，用来配置输出缓存ringbuffer的size。


### **8.2 宏配置**

> uart流宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_UART_STREAM | AP | bool | y |
>
> uart流依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **8.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_streams/uart_stream/uart_stream_test.c`
>
> demo基于 `onboard_mic_stream` 和 `uart_stream` 模块创建了一个音频pipeline，采集模拟mic音频，并输出至uart串口，通过uart工具可以将uart输出的音频保存，在pc上验证。


## **9. array流**


### **9.1 功能配置**

> array流支持数组音频流读写，通过数组 buffer 进行音频数据的输入和输出，通过 `array_stream_init` 接口初始化模块。
>
> 使用前需要通过 `array_stream_set_data` 接口设置数组 buffer 和其大小。
>
> array_stream.h 中提供了默认配置： `DEFAULT_ARRAY_STREAM_CONFIG()` 供参考。
>
> 重要的参数配置说明如下：
>
> |  |  |
> | --- | --- |
> | 参数 | 说明 |
> | type | 流类型：AUDIO_STREAM_READER 或 AUDIO_STREAM_WRITER |
> | array_size | 数组总大小 |
> | array_offset | 数组偏移量 |
> | buf_sz | 音频元素缓冲区大小 |
> | out_block_size | 输出块大小 |
> | out_block_num | 输出块数量 |
> | task_stack | 任务栈大小 |
> | task_core | 任务运行核心（0或1） |
> | task_prio | 任务优先级（基于freeRTOS优先级） |

备注

1. 当 type 配置为 AUDIO_STREAM_READER 时，array流会从数组中读取音频数据并输出到下一级组件。
2. 当 type 配置为 AUDIO_STREAM_WRITER 时，array流会接收上一级组件的音频数据并写入到数组中。
3. 在调用 array_stream_init 之后、启动流之前，必须调用 array_stream_set_data 设置数组 buffer 和大小。


### **9.2 宏配置**

> array流宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK_ARRAY_STREAM | AP | bool | y |
>
> array流依赖功能宏配置：
>
> |  |  |  |  |
> | --- | --- | --- | --- |
> | Kconfig | CPU | Format | Value |
> | CONFIG_ADK | AP | bool | y |


### **9.3 测试case及参考demo**

> 组件提供了模块测试case和使用参考demo：
> :   `bk_avdk_smp<源代码路径>/ap/components/bk_audio/audio_streams/array_stream/array_stream_test.c`
>
> demo创建了一个音频pipeline，通过array_stream实现音频数据的读写测试。
