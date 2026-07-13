# Uart Util


The Uart util provides a method to dump data processed by the component through free uart.


## API Reference


### Header File


- [bk_audio/audio_utils/uart_util.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_utils/uart_util.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_utils/uart_util.h")


### Functions

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") uart_util_create([uart_util_handle_t](#_CPPv418uart_util_handle_t "uart_util_handle_t") uart_util, [uart_id_t](../../../peripheral/bk_uart.md#_CPPv49uart_id_t "uart_id_t") id, uint32_t baud_rate)
:   Create a uart util.

    参数
    :   - **uart_util** – The uart util handle

        - **id** – **[in]** The uart id

        - **baud_rate** – **[in]** The baud rate

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") uart_util_destroy([uart_util_handle_t](#_CPPv418uart_util_handle_t "uart_util_handle_t") uart_util)
:   Destroy a uart util.

    参数
    :   **uart_util** – The uart util handle

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") uart_util_tx_data([uart_util_handle_t](#_CPPv418uart_util_handle_t "uart_util_handle_t") uart_util, void *data_buf, uint32_t len)
:   Transmit data via uart util.

    参数
    :   - **uart_util** – The uart util handle

        - **data_buf** – **[in]** The data buffer

        - **len** – **[in]** The data length

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed


### Structures

struct uart_util


### Type Definitions

typedef struct [uart_util](#_CPPv49uart_util "uart_util") *uart_util_handle_t
