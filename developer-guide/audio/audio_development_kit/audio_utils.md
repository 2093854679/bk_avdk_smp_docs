# **音频工具集**



## **1. 简介**

> 音频开发框架支持多种音频调试工具，详细列表如下：
>
> |  |  |
> | --- | --- |
> | 音频流 | 功能简介 |
> | count_util | 音频流速率统计工具 |
> | uart_util | uart dump音频流工具 |
> | vfs_util | VFS dump音频流工具 |


## **2. 音频流速率统计工具**

> count_util 主要用于统计组件处理的音频流的数据量，并计算得到速率，通过软件timer定时打印结果。
>
> 方便调试下述问题：
> :   - 音频卡顿：数据量偏小
>     - 播放无声：数据量为0
>
> 接口说明：
> :   - count_util_create：创建速率统计工具
>     - count_util_destroy：注销速率统计工具
>     - count_util_add_size：通知速率统计工具处理的数据量
>
> 详情请参考头文件：
> :   `bk_avdk_smp<源代码路径>/ap/include/components/bk_audio/audio_utils/count_util.h`

备注

1. streams中很多组件已经适配使用此工具，如：onboard_mic_stream、onboard_speaker_stream等，可供参考。


## **3. 串口dump音频流工具**

> uart_util 主要用于dump音频流数据，用于分析。
>
> 方便调试下述问题：
> :   - 音频异常：数据丢失、错误等
>     - pop音：数据丢失、错误等
>
> 接口说明：
> :   - uart_util_create：创建串口dump音频流工具
>     - uart_util_destroy：注销串口dump音频流工具
>     - uart_util_tx_data：通知串口dump音频流输出音频数据
>
> 详情请参考头文件：
> :   `bk_avdk_smp<源代码路径>/ap/include/components/bk_audio/audio_utils/uart_util.h`

备注

1. uart dump数据会占用cpu资源，可能会导致task调度异常，影响原本的音频应用功能。因此需要将波特率设置为2M，尽量dump较少的数据。
2. 部分组件已经适配使用此工具，如：aec_algorithm等，可供参考。


## **4. VFS dump音频流工具**

> vfs_util 主要用于dump音频流数据，用于分析。
>
> 方便调试下述问题：
> :   - 音频异常：数据丢失、错误等
>     - pop音：数据丢失、错误等
>
> 接口说明：
> :   - vfs_util_create：创建VFS dump音频流工具
>     - vfs_util_destroy：注销VFS dump音频流工具
>     - vfs_util_tx_data：通知VFS dump音频流输出音频数据
>
> 详情请参考头文件：
> :   `bk_avdk_smp<源代码路径>/ap/include/components/bk_audio/audio_utils/vfs_util.h`

备注

1. VFS工具默认不支持挂载操作，需要客户自行mount。
2. 部分组件已经适配使用此工具，如：aec_algorithm等，可供参考。
