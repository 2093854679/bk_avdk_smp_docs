# AEC Algorithm


Process the data collected by the microphone and eliminate the echo in the data.


## API Reference


### Header File


- [bk_audio/audio_algorithms/aec_algorithm.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_algorithms/aec_algorithm.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_algorithms/aec_algorithm.h")


### Functions

[audio_element_handle_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") aec_algorithm_init([aec_algorithm_cfg_t](#_CPPv419aec_algorithm_cfg_t "aec_algorithm_cfg_t") *config)
:   Create a Aec algorithm of Audio Element to echo cancellation.

    参数
    :   **config** – **[in]** The configuration

    返回
    :   The audio element handle


        - Not NULL: success

        - NULL: failed


### Structures

struct aec_cfg_t

struct aec_algorithm_cfg_t
:   AEC algorithm configurations.


### Macros

AEC_DELAY_SAMPLE_POINTS_MAX

AEC_ALGORITHM_TASK_STACK

AEC_ALGORITHM_TASK_CORE

AEC_ALGORITHM_TASK_PRIO

AEC_ALGORITHM_OUT_BLOCK_NUM

AEC_ALGORITHM_FS

AEC_DELAY_POINTS

AEC_ALGORITHM_EC_DEPTH

AEC_ALGORITHM_TXRXTHR

AEC_ALGORITHM_TXRXFLR

AEC_ALGORITHM_REF_SCALE

AEC_ALGORITHM_NS_LEVEL

AEC_ALGORITHM_NS_PARA

DEFAULT_AEC_ALGORITHM_CONFIG()


### Enumerations

enum aec_mode_t
:   *Values:*

    enumerator AEC_MODE_HARDWARE
    :   hardware mode: Hardware mode get source and reference signal through audio adc L and R channel. Audio adc L channel connect to mic, and collect source signal. Audio adc R channel connect to speaker, and collect reference signal.

    enumerator AEC_MODE_SOFTWARE
    :   software mode: Software mode get source and reference signal through audio adc L and software writting. Audio adc L channel connect to mic, and collect source signal. Software write speaker data to input ringbuffer to support reference signal.
