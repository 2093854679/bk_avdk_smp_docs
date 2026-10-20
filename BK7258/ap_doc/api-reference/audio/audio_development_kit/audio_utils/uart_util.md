---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_utils/uart_util.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="uart-util"></a>

# Uart Util

The Uart util provides a method to dump data processed by the component through free uart.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [uart\_util.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_utils/uart_util.h)

<a id="functions"></a>

### Functions

<a id="_CPPv416uart_util_create18uart_util_handle_t9uart_id_t8uint32_t"></a>

<a id="_CPPv316uart_util_create18uart_util_handle_t9uart_id_t8uint32_t"></a> <a id="_CPPv216uart_util_create18uart_util_handle_t9uart_id_t8uint32_t"></a> <a id="uart_util_create__uart_util_handle_t.uart_id_t.uint32_t"></a> <a id="uart__util_8h_1a2d27b545d21a2d3e1ec3ab6d80257f5f"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") uart\_util\_create([uart\_util\_handle\_t](#_CPPv418uart_util_handle_t "uart_util_handle_t") uart\_util, [uart\_id\_t](../../../peripheral/bk_uart.md#_CPPv49uart_id_t "uart_id_t") id, uint32\_t baud\_rate)
:   Create a uart util.

    参数
    :   - **uart\_util** – The uart util handle
        - **id** – **\[in\]** The uart id
        - **baud\_rate** – **\[in\]** The baud rate

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="_CPPv417uart_util_destroy18uart_util_handle_t"></a>

<a id="_CPPv317uart_util_destroy18uart_util_handle_t"></a> <a id="_CPPv217uart_util_destroy18uart_util_handle_t"></a> <a id="uart_util_destroy__uart_util_handle_t"></a> <a id="uart__util_8h_1a54a61059bc4b213ebd0ec6a5767d65f3"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") uart\_util\_destroy([uart\_util\_handle\_t](#_CPPv418uart_util_handle_t "uart_util_handle_t") uart\_util)
:   Destroy a uart util.

    参数
    :   **uart\_util** – The uart util handle

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="_CPPv417uart_util_tx_data18uart_util_handle_tPv8uint32_t"></a>

<a id="_CPPv317uart_util_tx_data18uart_util_handle_tPv8uint32_t"></a> <a id="_CPPv217uart_util_tx_data18uart_util_handle_tPv8uint32_t"></a> <a id="uart_util_tx_data__uart_util_handle_t.voidP.uint32_t"></a> <a id="uart__util_8h_1aefc64383b4b417dd2ad3f777918e2088"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") uart\_util\_tx\_data([uart\_util\_handle\_t](#_CPPv418uart_util_handle_t "uart_util_handle_t") uart\_util, void \*data\_buf, uint32\_t len)
:   Transmit data via uart util.

    参数
    :   - **uart\_util** – The uart util handle
        - **data\_buf** – **\[in\]** The data buffer
        - **len** – **\[in\]** The data length

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="structures"></a>

### Structures

<a id="_CPPv49uart_util"></a>

<a id="_CPPv39uart_util"></a> <a id="_CPPv29uart_util"></a> <a id="uart_util"></a> <a id="structuart__util"></a> struct uart\_util

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv418uart_util_handle_t"></a>

<a id="_CPPv318uart_util_handle_t"></a> <a id="_CPPv218uart_util_handle_t"></a> <a id="uart_util_handle_t"></a> <a id="uart__util_8h_1a1b9ca2fd6bc459620024880e1e00bc18"></a> typedef struct [uart\_util](#_CPPv49uart_util "uart_util") \*uart\_util\_handle\_t
