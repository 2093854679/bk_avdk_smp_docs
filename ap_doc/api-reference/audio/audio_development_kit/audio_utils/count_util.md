# Count Util


The Count util provides a method to count the amount of data processed by the component. It prints the processed data volume periodically using a timer for debugging purposes.


## API Reference


### Header File


- [bk_audio/audio_utils/count_util.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_utils/count_util.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_utils/count_util.h")


### Functions

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") count_util_destroy([count_util_t](#_CPPv412count_util_t "count_util_t") *count_util)
:   Destroy a count util.

    参数
    :   **count_util** – **[in]** The count util handle

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") count_util_create([count_util_t](#_CPPv412count_util_t "count_util_t") *count_util, uint32_t interval, char *tag)
:   Create a count util.

    参数
    :   - **count_util** – **[in]** The count util handle

        - **interval** – **[in]** The timer interval(ms)

        - **tag** – **[in]** The printf tag

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed

void count_util_add_size([count_util_t](#_CPPv412count_util_t "count_util_t") *count_util, int32_t size)
:   Add data size to count util.

    参数
    :   - **count_util** – **[in]** The count util handle

        - **size** – **[in]** The data size(bytes)

    返回
    :   None

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") count_util_multi_destroy([count_util_multi_t](#_CPPv418count_util_multi_t "count_util_multi_t") *count_util)
:   Destroy a multi-parameter count util.

    参数
    :   **count_util** – **[in]** The multi-parameter count util handle

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") count_util_multi_create([count_util_multi_t](#_CPPv418count_util_multi_t "count_util_multi_t") *count_util, uint32_t interval, char **tags, uint32_t param_count)
:   Create a multi-parameter count util.

    备注

    The tags array should contain param_count strings

    参数
    :   - **count_util** – **[in]** The multi-parameter count util handle

        - **interval** – **[in]** The timer interval(ms)

        - **tags** – **[in]** The array of parameter tags

        - **param_count** – **[in]** The number of parameters

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed

void count_util_multi_add_size([count_util_multi_t](#_CPPv418count_util_multi_t "count_util_multi_t") *count_util, uint32_t param_index, int32_t size)
:   Add data size to specific parameter in multi-parameter count util.

    参数
    :   - **count_util** – **[in]** The multi-parameter count util handle

        - **param_index** – **[in]** The parameter index (0 to param_count-1)

        - **size** – **[in]** The data size(bytes)

    返回
    :   None


### Structures

struct count_util_t
:   Public Members

    [beken_timer_t](../../../system/os.md#_CPPv413beken_timer_t "beken_timer_t") timer
    :   freertos timer

    uint32_t timer_interval
    :   timer interval(ms)

    uint32_t data_size
    :   total data size(bytes)

    char tag[20]
    :   printf tag

struct count_util_param_t
:   Multi-parameter item structure for count util.

    Public Members

    char tag[20]
    :   parameter tag

    uint32_t data_size
    :   total data size(bytes)

struct count_util_multi_t
:   Multi-parameter count util structure.

    Public Members

    [beken_timer_t](../../../system/os.md#_CPPv413beken_timer_t "beken_timer_t") timer
    :   freertos timer

    uint32_t timer_interval
    :   timer interval(ms)

    [count_util_param_t](#_CPPv418count_util_param_t "count_util_param_t") *params
    :   parameters array

    uint32_t param_count
    :   number of parameters
