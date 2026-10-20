---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_uart.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="uart"></a>

# UART

<a id="uart-api-status"></a>

## UART API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_uart_driver_init()`](#_CPPv419bk_uart_driver_initv "bk_uart_driver_init") | Y |
| [`bk_uart_driver_deinit()`](#_CPPv421bk_uart_driver_deinitv "bk_uart_driver_deinit") | Y |
| [`bk_uart_init()`](#_CPPv412bk_uart_init9uart_id_tPK13uart_config_t "bk_uart_init") | Y |
| [`bk_uart_deinit()`](#_CPPv414bk_uart_deinit9uart_id_t "bk_uart_deinit") | Y |
| [`bk_uart_set_baud_rate()`](#_CPPv421bk_uart_set_baud_rate9uart_id_t8uint32_t "bk_uart_set_baud_rate") | Y |
| [`bk_uart_set_data_bits()`](#_CPPv421bk_uart_set_data_bits9uart_id_t16uart_data_bits_t "bk_uart_set_data_bits") | Y |
| [`bk_uart_set_stop_bits()`](#_CPPv421bk_uart_set_stop_bits9uart_id_t16uart_stop_bits_t "bk_uart_set_stop_bits") | Y |
| [`bk_uart_set_parity()`](#_CPPv418bk_uart_set_parity9uart_id_t13uart_parity_t "bk_uart_set_parity") | Y |
| [`bk_uart_set_hw_flow_ctrl()`](#_CPPv424bk_uart_set_hw_flow_ctrl9uart_id_t7uint8_t "bk_uart_set_hw_flow_ctrl") | Y |
| [`bk_uart_set_rx_full_threshold()`](#_CPPv429bk_uart_set_rx_full_threshold9uart_id_t7uint8_t "bk_uart_set_rx_full_threshold") | Y |
| [`bk_uart_set_tx_empty_threshold()`](#_CPPv430bk_uart_set_tx_empty_threshold9uart_id_t7uint8_t "bk_uart_set_tx_empty_threshold") | Y |
| [`bk_uart_set_rx_timeout()`](#_CPPv422bk_uart_set_rx_timeout9uart_id_t26uart_rx_stop_detect_time_t "bk_uart_set_rx_timeout") | Y |
| [`bk_uart_disable_hw_flow_ctrl()`](#_CPPv428bk_uart_disable_hw_flow_ctrl9uart_id_t "bk_uart_disable_hw_flow_ctrl") | Y |
| [`bk_uart_enable_tx_interrupt()`](#_CPPv427bk_uart_enable_tx_interrupt9uart_id_t "bk_uart_enable_tx_interrupt") | Y |
| [`bk_uart_disable_tx_interrupt()`](#_CPPv428bk_uart_disable_tx_interrupt9uart_id_t "bk_uart_disable_tx_interrupt") | Y |
| [`bk_uart_enable_rx_interrupt()`](#_CPPv427bk_uart_enable_rx_interrupt9uart_id_t "bk_uart_enable_rx_interrupt") | Y |
| [`bk_uart_disable_rx_interrupt()`](#_CPPv428bk_uart_disable_rx_interrupt9uart_id_t "bk_uart_disable_rx_interrupt") | Y |
| [`bk_uart_register_rx_isr()`](#_CPPv423bk_uart_register_rx_isr9uart_id_t10uart_isr_tPv "bk_uart_register_rx_isr") | Y |
| [`bk_uart_register_tx_isr()`](#_CPPv423bk_uart_register_tx_isr9uart_id_t10uart_isr_tPv "bk_uart_register_tx_isr") | Y |
| [`bk_uart_write_bytes()`](#_CPPv419bk_uart_write_bytes9uart_id_tPKv8uint32_t "bk_uart_write_bytes") | Y |
| [`bk_uart_read_bytes()`](#_CPPv418bk_uart_read_bytes9uart_id_tPv8uint32_t8uint32_t "bk_uart_read_bytes") | Y |
| [`bk_uart_disable_rx()`](#_CPPv418bk_uart_disable_rx9uart_id_t "bk_uart_disable_rx") | Y |
| [`bk_uart_disable_tx()`](#_CPPv418bk_uart_disable_tx9uart_id_t "bk_uart_disable_tx") | Y |
| [`bk_uart_enable_sw_fifo()`](#_CPPv422bk_uart_enable_sw_fifo9uart_id_t "bk_uart_enable_sw_fifo") | Y |
| [`bk_uart_disable_sw_fifo()`](#_CPPv423bk_uart_disable_sw_fifo9uart_id_t "bk_uart_disable_sw_fifo") | Y |

<a id="uart-port-number"></a>

## UART Port Number

| Capability | BK7258\_AP |
| --- | --- |
| Port Number | 3 |

<a id="uart-pin-and-gpio-map"></a>

## UART Pin and GPIO Map

| UART Pin | BK7258\_AP |
| --- | --- |
| UART0 TX | 11 |
| UART0 RX | 10 |
| UART1 TX | 0 |
| UART1 RX | 1 |
| UART2 TX | 41 |
| UART2 RX | 40 |

<a id="uart-api-reference"></a>

## UART API Reference

<a id="header-file"></a>

### Header File

- [uart.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/uart.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419bk_uart_driver_initv"></a>

<a id="_CPPv319bk_uart_driver_initv"></a> <a id="_CPPv219bk_uart_driver_initv"></a> <a id="bk_uart_driver_init__void"></a> <a id="uart_8h_1abd92212cd1f5b55df632ec5fcc431779"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_driver\_init(void)
:   Init the UART driver.

    This API init the resoure common to all UART id:

    - Init UART driver control memory

    **Attention**
    :   1\. This API should be called before any other UART APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_uart_driver_deinitv"></a>

<a id="_CPPv321bk_uart_driver_deinitv"></a> <a id="_CPPv221bk_uart_driver_deinitv"></a> <a id="bk_uart_driver_deinit__void"></a> <a id="uart_8h_1a2b16b30a29fc09cf5be90835fddcb244"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_driver\_deinit(void)
:   Deinit the UART driver.

    This API free all resource related to UART and power down all UART id.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_uart_is_in_used9uart_id_t"></a>

<a id="_CPPv318bk_uart_is_in_used9uart_id_t"></a> <a id="_CPPv218bk_uart_is_in_used9uart_id_t"></a> <a id="bk_uart_is_in_used__uart_id_t"></a> <a id="uart_8h_1acc1baf45503e8d325a52a237c65aa08c"></a> int bk\_uart\_is\_in\_used([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Get the UART whether in used.

    参数
    :   **id** – UART id

    返回
    :   - 1: in used
        - 0: not in used

<a id="_CPPv425bk_uart_is_rx_dma_enabled9uart_id_t"></a>

<a id="_CPPv325bk_uart_is_rx_dma_enabled9uart_id_t"></a> <a id="_CPPv225bk_uart_is_rx_dma_enabled9uart_id_t"></a> <a id="bk_uart_is_rx_dma_enabled__uart_id_t"></a> <a id="uart_8h_1ab7ab10a79115adc7d4a8dd848c993202"></a> int bk\_uart\_is\_rx\_dma\_enabled([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Get the UART whether rx dma is enabled.

    参数
    :   **id** – UART id

    返回
    :   - 1: rx dma is enabled
        - 0: rx dma is disabled

<a id="_CPPv412bk_uart_init9uart_id_tPK13uart_config_t"></a>

<a id="_CPPv312bk_uart_init9uart_id_tPK13uart_config_t"></a> <a id="_CPPv212bk_uart_init9uart_id_tPK13uart_config_t"></a> <a id="bk_uart_init__uart_id_t.uart_config_tCP"></a> <a id="uart_8h_1aa366f9681fc381f97271d0e9ca3dd9d4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_init([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, const [uart\_config\_t](#_CPPv413uart_config_t "uart_config_t") \*config)
:   Init the UART id.

    This API init the UART id:

    - Power up the UART id
    - Configure the UART id clock
    - Map the UART id to dedicated GPIO port
    - Set the UART baud rate, data bits, parity, stop bits,flow ctrl and source clock
    - Start the UART id

    参数
    :   - **id** – UART id
        - **config** – UART parameter settings

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_UART\_NOT\_INIT: UART driver not init
        - BK\_ERR\_NULL\_PARAM: UART config parameter is NULL
        - BK\_ERR\_UART\_INVALID\_ID: UART id is invalid
        - BK\_ERR\_UART\_BAUD\_RATE\_NOT\_SUPPORT: UART baud rate is not support
        - others: other errors.

<a id="_CPPv414bk_uart_deinit9uart_id_t"></a>

<a id="_CPPv314bk_uart_deinit9uart_id_t"></a> <a id="_CPPv214bk_uart_deinit9uart_id_t"></a> <a id="bk_uart_deinit__uart_id_t"></a> <a id="uart_8h_1a96927d97c084e3c3e5d5f173aca2f5e0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_deinit([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Deinit the UART id.

    This API deinit the UART id:

    - Stop the UART id
    - Reset all configuration of UART id to default value
    - Disable the UART id interrupt
    - Power down the UART id

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_uart_set_baud_rate9uart_id_t8uint32_t"></a>

<a id="_CPPv321bk_uart_set_baud_rate9uart_id_t8uint32_t"></a> <a id="_CPPv221bk_uart_set_baud_rate9uart_id_t8uint32_t"></a> <a id="bk_uart_set_baud_rate__uart_id_t.uint32_t"></a> <a id="uart_8h_1adef7c82ff3defca050d3281eb1b00f32"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_baud\_rate([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, uint32\_t baud\_rate)
:   Set the UART baud rate.

    参数
    :   - **id** – UART id
        - **baud\_rate** – UART baud rate

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_uart_set_data_bits9uart_id_t16uart_data_bits_t"></a>

<a id="_CPPv321bk_uart_set_data_bits9uart_id_t16uart_data_bits_t"></a> <a id="_CPPv221bk_uart_set_data_bits9uart_id_t16uart_data_bits_t"></a> <a id="bk_uart_set_data_bits__uart_id_t.uart_data_bits_t"></a> <a id="uart_8h_1a67af278ec4b7f849105a35b675256130"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_data\_bits([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, [uart\_data\_bits\_t](#_CPPv416uart_data_bits_t "uart_data_bits_t") data\_bits)
:   Set the UART data bits.

    参数
    :   - **id** – UART id
        - **data\_bits** – UART data bits

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_uart_set_stop_bits9uart_id_t16uart_stop_bits_t"></a>

<a id="_CPPv321bk_uart_set_stop_bits9uart_id_t16uart_stop_bits_t"></a> <a id="_CPPv221bk_uart_set_stop_bits9uart_id_t16uart_stop_bits_t"></a> <a id="bk_uart_set_stop_bits__uart_id_t.uart_stop_bits_t"></a> <a id="uart_8h_1a24379d32c46e9dbd3f118f92cf2c33b4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_stop\_bits([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, [uart\_stop\_bits\_t](#_CPPv416uart_stop_bits_t "uart_stop_bits_t") stop\_bits)
:   Set the UART stop bits.

    参数
    :   - **id** – UART id
        - **stop\_bits** – UART stop bits

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_uart_set_parity9uart_id_t13uart_parity_t"></a>

<a id="_CPPv318bk_uart_set_parity9uart_id_t13uart_parity_t"></a> <a id="_CPPv218bk_uart_set_parity9uart_id_t13uart_parity_t"></a> <a id="bk_uart_set_parity__uart_id_t.uart_parity_t"></a> <a id="uart_8h_1a5b195b37d59daa3f35058c01cfb28525"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_parity([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, [uart\_parity\_t](#_CPPv413uart_parity_t "uart_parity_t") partiy)
:   Set the UART partiy.

    参数
    :   - **id** – UART id
        - **partiy** – UART partiy

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_uart_set_hw_flow_ctrl9uart_id_t7uint8_t"></a>

<a id="_CPPv324bk_uart_set_hw_flow_ctrl9uart_id_t7uint8_t"></a> <a id="_CPPv224bk_uart_set_hw_flow_ctrl9uart_id_t7uint8_t"></a> <a id="bk_uart_set_hw_flow_ctrl__uart_id_t.uint8_t"></a> <a id="uart_8h_1a83405465cbd6b6737ba394ccb9a6d8d3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_hw\_flow\_ctrl([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, uint8\_t rx\_threshold)
:   Set the UART hardware flow control.

    参数
    :   - **id** – UART id
        - **rx\_threshold** – Threshold of Hardware RX flow control

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv429bk_uart_set_rx_full_threshold9uart_id_t7uint8_t"></a>

<a id="_CPPv329bk_uart_set_rx_full_threshold9uart_id_t7uint8_t"></a> <a id="_CPPv229bk_uart_set_rx_full_threshold9uart_id_t7uint8_t"></a> <a id="bk_uart_set_rx_full_threshold__uart_id_t.uint8_t"></a> <a id="uart_8h_1a34cd98a7d1edafd54c3aa02fb41e4beb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_rx\_full\_threshold([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, uint8\_t threshold)
:   Set the UART threshold value for RX fifo full.

    参数
    :   - **id** – UART id
        - **threshold** – Threshold value above which RX fifo full interrupt is generated

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv430bk_uart_set_tx_empty_threshold9uart_id_t7uint8_t"></a>

<a id="_CPPv330bk_uart_set_tx_empty_threshold9uart_id_t7uint8_t"></a> <a id="_CPPv230bk_uart_set_tx_empty_threshold9uart_id_t7uint8_t"></a> <a id="bk_uart_set_tx_empty_threshold__uart_id_t.uint8_t"></a> <a id="uart_8h_1a6d2ac43d5689e6de9f211e0395d3a903"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_tx\_empty\_threshold([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, uint8\_t threshold)
:   Set the UART threshold value for TX fifo empty.

    参数
    :   - **id** – UART id
        - **threshold** – Threshold value below which TX fifo empty interrupt is generated

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_uart_set_rx_timeout9uart_id_t26uart_rx_stop_detect_time_t"></a>

<a id="_CPPv322bk_uart_set_rx_timeout9uart_id_t26uart_rx_stop_detect_time_t"></a> <a id="_CPPv222bk_uart_set_rx_timeout9uart_id_t26uart_rx_stop_detect_time_t"></a> <a id="bk_uart_set_rx_timeout__uart_id_t.uart_rx_stop_detect_time_t"></a> <a id="uart_8h_1ae707e4ec262e9d4db0c52d1f532ca3c1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_rx\_timeout([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, [uart\_rx\_stop\_detect\_time\_t](#_CPPv426uart_rx_stop_detect_time_t "uart_rx_stop_detect_time_t") timeout\_thresh)
:   Set the UART threshold timeout for receive data, unit is bit.

    UART finish receiving data when the periods is more than timeout threshold. If the time is expired, the UART\_RX\_STOP\_END interrupt is triggered.

    参数
    :   - **id** – UART id
        - **timeout\_thresh** – timeout threshold

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv428bk_uart_disable_hw_flow_ctrl9uart_id_t"></a>

<a id="_CPPv328bk_uart_disable_hw_flow_ctrl9uart_id_t"></a> <a id="_CPPv228bk_uart_disable_hw_flow_ctrl9uart_id_t"></a> <a id="bk_uart_disable_hw_flow_ctrl__uart_id_t"></a> <a id="uart_8h_1a5864162dea6439cbf077665c56e25944"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_disable\_hw\_flow\_ctrl([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable the UART hardware flow control.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_uart_enable_tx_interrupt9uart_id_t"></a>

<a id="_CPPv327bk_uart_enable_tx_interrupt9uart_id_t"></a> <a id="_CPPv227bk_uart_enable_tx_interrupt9uart_id_t"></a> <a id="bk_uart_enable_tx_interrupt__uart_id_t"></a> <a id="uart_8h_1a8f56a7d398f07681e458e85e81e648b7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_enable\_tx\_interrupt([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Enable TX interrupt of UART id.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv428bk_uart_disable_tx_interrupt9uart_id_t"></a>

<a id="_CPPv328bk_uart_disable_tx_interrupt9uart_id_t"></a> <a id="_CPPv228bk_uart_disable_tx_interrupt9uart_id_t"></a> <a id="bk_uart_disable_tx_interrupt__uart_id_t"></a> <a id="uart_8h_1ae03c2472fe40f3030c7ad514bc21077d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_disable\_tx\_interrupt([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable TX interrupt of UART id.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_uart_enable_rx_interrupt9uart_id_t"></a>

<a id="_CPPv327bk_uart_enable_rx_interrupt9uart_id_t"></a> <a id="_CPPv227bk_uart_enable_rx_interrupt9uart_id_t"></a> <a id="bk_uart_enable_rx_interrupt__uart_id_t"></a> <a id="uart_8h_1a1e451bf8b496a126e65daf7c44ac1d7d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_enable\_rx\_interrupt([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Enable RX interrupt of UART id.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv428bk_uart_disable_rx_interrupt9uart_id_t"></a>

<a id="_CPPv328bk_uart_disable_rx_interrupt9uart_id_t"></a> <a id="_CPPv228bk_uart_disable_rx_interrupt9uart_id_t"></a> <a id="bk_uart_disable_rx_interrupt__uart_id_t"></a> <a id="uart_8h_1abeeafeeda3af44fb807755ce56de631a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_disable\_rx\_interrupt([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable RX interrupt of UART id.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_uart_register_rx_isr9uart_id_t10uart_isr_tPv"></a>

<a id="_CPPv323bk_uart_register_rx_isr9uart_id_t10uart_isr_tPv"></a> <a id="_CPPv223bk_uart_register_rx_isr9uart_id_t10uart_isr_tPv"></a> <a id="bk_uart_register_rx_isr__uart_id_t.uart_isr_t.voidP"></a> <a id="uart_8h_1af6e8991d43d98c508a9ae5df41a25f5d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_register\_rx\_isr([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, [uart\_isr\_t](#_CPPv410uart_isr_t "uart_isr_t") isr, void \*param)
:   Register the RX interrupt service routine for UART id.

    参数
    :   - **id** – UART id
        - **isr** – UART RX callback
        - **param** – UART RX callback parameter

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_uart_register_tx_isr9uart_id_t10uart_isr_tPv"></a>

<a id="_CPPv323bk_uart_register_tx_isr9uart_id_t10uart_isr_tPv"></a> <a id="_CPPv223bk_uart_register_tx_isr9uart_id_t10uart_isr_tPv"></a> <a id="bk_uart_register_tx_isr__uart_id_t.uart_isr_t.voidP"></a> <a id="uart_8h_1a1df6660b23ed31501eb30a6f19d90613"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_register\_tx\_isr([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, [uart\_isr\_t](#_CPPv410uart_isr_t "uart_isr_t") isr, void \*param)
:   Register the TX interrupt service routine for UART id.

    参数
    :   - **id** – UART id
        - **isr** – UART TX callback
        - **param** – UART TX callback parameter

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_uart_write_bytes9uart_id_tPKv8uint32_t"></a>

<a id="_CPPv319bk_uart_write_bytes9uart_id_tPKv8uint32_t"></a> <a id="_CPPv219bk_uart_write_bytes9uart_id_tPKv8uint32_t"></a> <a id="bk_uart_write_bytes__uart_id_t.voidCP.uint32_t"></a> <a id="uart_8h_1a07223aab417c84faf5775a3a8dae91cc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_write\_bytes([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, const void \*data, uint32\_t size)
:   Send data to the UART port from a given buffer and length.

    参数
    :   - **id** – UART id
        - **data** – data buffer address
        - **size** – data length to send

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_uart_read_bytes9uart_id_tPv8uint32_t8uint32_t"></a>

<a id="_CPPv318bk_uart_read_bytes9uart_id_tPv8uint32_t8uint32_t"></a> <a id="_CPPv218bk_uart_read_bytes9uart_id_tPv8uint32_t8uint32_t"></a> <a id="bk_uart_read_bytes__uart_id_t.voidP.uint32_t.uint32_t"></a> <a id="uart_8h_1a88678d1509683ed85977ff29beeaf4b0"></a> int bk\_uart\_read\_bytes([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, void \*data, uint32\_t size, uint32\_t timeout\_ms)
:   UART read bytes from UART buffer.

    参数
    :   - **id** – UART id
        - **data** – pointer to the buffer
        - **size** – data length to read
        - **timeout\_ms** – timeout ms, if set BEKEN\_WAIT\_FOREVER, read will wait forever

    返回
    :   - BK\_ERR\_UART\_NOT\_INIT: UART driver not init
        - BK\_ERR\_UART\_INVALID\_ID: UART id number is invalid
        - BK\_ERR\_UART\_ID\_NOT\_INIT: UART id not init
        - BK\_ERR\_UART\_RX\_TIMEOUT: UART receive data timeout
        - others (\>\=0): The number of bytes read from UART FIFO

<a id="_CPPv418bk_uart_disable_rx9uart_id_t"></a>

<a id="_CPPv318bk_uart_disable_rx9uart_id_t"></a> <a id="_CPPv218bk_uart_disable_rx9uart_id_t"></a> <a id="bk_uart_disable_rx__uart_id_t"></a> <a id="uart_8h_1a4284d274c68eac6d19c5c53fd69dbac7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_disable\_rx([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable UART TX pin and set as GPIO.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_uart_disable_tx9uart_id_t"></a>

<a id="_CPPv318bk_uart_disable_tx9uart_id_t"></a> <a id="_CPPv218bk_uart_disable_tx9uart_id_t"></a> <a id="bk_uart_disable_tx__uart_id_t"></a> <a id="uart_8h_1a333655ff2c604a3cda4fa417061fada9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_disable\_tx([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable UART TX pin and set as GPIO.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_uart_set_enable_rx9uart_id_tb"></a>

<a id="_CPPv321bk_uart_set_enable_rx9uart_id_tb"></a> <a id="_CPPv221bk_uart_set_enable_rx9uart_id_tb"></a> <a id="bk_uart_set_enable_rx__uart_id_t.b"></a> <a id="uart_8h_1af7875e8bb3d86afd73d4184d07342e00"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_enable\_rx([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, bool enable)
:   Just set UART RX enable/disable, doesn’t set pin.

    参数
    :   - **id** – UART id
        - **enable** – true, enable, flase disable

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_uart_set_enable_tx9uart_id_tb"></a>

<a id="_CPPv321bk_uart_set_enable_tx9uart_id_tb"></a> <a id="_CPPv221bk_uart_set_enable_tx9uart_id_tb"></a> <a id="bk_uart_set_enable_tx__uart_id_t.b"></a> <a id="uart_8h_1a3114673fe7d05cc94a39f07d63e8e81e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_set\_enable\_tx([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, bool enable)
:   Just set UART TX enable/disable, doesn’t set pin.

    参数
    :   - **id** – UART id
        - **enable** – true, enable, flase disable

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_uart_enable_sw_fifo9uart_id_t"></a>

<a id="_CPPv322bk_uart_enable_sw_fifo9uart_id_t"></a> <a id="_CPPv222bk_uart_enable_sw_fifo9uart_id_t"></a> <a id="bk_uart_enable_sw_fifo__uart_id_t"></a> <a id="uart_8h_1a4b7066e88d2722ca2fa71d2c00d5f295"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_enable\_sw\_fifo([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Enable UART software fifo.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_uart_disable_sw_fifo9uart_id_t"></a>

<a id="_CPPv323bk_uart_disable_sw_fifo9uart_id_t"></a> <a id="_CPPv223bk_uart_disable_sw_fifo9uart_id_t"></a> <a id="bk_uart_disable_sw_fifo__uart_id_t"></a> <a id="uart_8h_1a1f32ea1ba2f648b9ef31ccd3cd2538b9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_disable\_sw\_fifo([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable UART software fifo.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_uart_take_rx_isr9uart_id_t10uart_isr_tPv"></a>

<a id="_CPPv319bk_uart_take_rx_isr9uart_id_t10uart_isr_tPv"></a> <a id="_CPPv219bk_uart_take_rx_isr9uart_id_t10uart_isr_tPv"></a> <a id="bk_uart_take_rx_isr__uart_id_t.uart_isr_t.voidP"></a> <a id="uart_8h_1a68bb06e73d9d94e83c611d5ab21ad5fe"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_take\_rx\_isr([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, [uart\_isr\_t](#_CPPv410uart_isr_t "uart_isr_t") isr, void \*param)
:   Register uart rx isr and disable software fifo.

    参数
    :   - **id** – UART id
        - **isr** – UART RX callback
        - **param** – UART RX callback parameter

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_uart_recover_rx_isr9uart_id_t"></a>

<a id="_CPPv322bk_uart_recover_rx_isr9uart_id_t"></a> <a id="_CPPv222bk_uart_recover_rx_isr9uart_id_t"></a> <a id="bk_uart_recover_rx_isr__uart_id_t"></a> <a id="uart_8h_1a61bcdf6565864f96a7a131a147d47de9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_recover\_rx\_isr([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Recover uart rx isr.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_uart_is_tx_over9uart_id_t"></a>

<a id="_CPPv318bk_uart_is_tx_over9uart_id_t"></a> <a id="_CPPv218bk_uart_is_tx_over9uart_id_t"></a> <a id="bk_uart_is_tx_over__uart_id_t"></a> <a id="uart_8h_1a862a267ce05b9190429415ef847bb5bb"></a> bool bk\_uart\_is\_tx\_over([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Get whether the uart tx over(tx fifo empty)

    参数
    :   **id** – UART id

    返回
    :   - true: uart tx over
        - false: uart tx not over

<a id="_CPPv417bk_uart_pm_backup9uart_id_t"></a>

<a id="_CPPv317bk_uart_pm_backup9uart_id_t"></a> <a id="_CPPv217bk_uart_pm_backup9uart_id_t"></a> <a id="bk_uart_pm_backup__uart_id_t"></a> <a id="uart_8h_1ad1f6fec53a9adea02c9a33b7b56c8845"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_pm\_backup([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Backup uart config.

    参数
    :   **id** – UART id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_uart_pm_restore9uart_id_t"></a>

<a id="_CPPv318bk_uart_pm_restore9uart_id_t"></a> <a id="_CPPv218bk_uart_pm_restore9uart_id_t"></a> <a id="bk_uart_pm_restore__uart_id_t"></a> <a id="uart_8h_1a1435b1bb676d6a54ef3e617395ae409b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_uart\_pm\_restore([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)

<a id="_CPPv420bk_uart_wait_tx_over9uart_id_t"></a>

<a id="_CPPv320bk_uart_wait_tx_over9uart_id_t"></a> <a id="_CPPv220bk_uart_wait_tx_over9uart_id_t"></a> <a id="bk_uart_wait_tx_over__uart_id_t"></a> <a id="uart_8h_1abdf30acdd176448fd7816790cbe88072"></a> void bk\_uart\_wait\_tx\_over([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Wait uart tx over.

    参数
    :   **id** – UART id

    返回
    :   - void

<a id="uart-api-typedefs"></a>

## UART API Typedefs

<a id="id1"></a>

### Header File

- [uart\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/uart_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_UART_NOT_INIT"></a>

<a id="uart__types_8h_1a24a6662e5c355133612fc466e01371dd"></a> BK\_ERR\_UART\_NOT\_INIT
:   UART driver not init

<a id="c.BK_ERR_UART_INVALID_ID"></a>

<a id="uart__types_8h_1a4758e0b9d603a74f3778e1b1a1850883"></a> BK\_ERR\_UART\_INVALID\_ID
:   UART id number is invalid

<a id="c.BK_ERR_UART_INVALID_SIZE"></a>

<a id="uart__types_8h_1af38ae1a0e6a9f3ab3e8ca88028b757a0"></a> BK\_ERR\_UART\_INVALID\_SIZE
:   UART read bytes length is more than fifo length

<a id="c.BK_ERR_UART_RX_TIMEOUT"></a>

<a id="uart__types_8h_1aa40c388acaff60ed4f08ed0df1a5c90b"></a> BK\_ERR\_UART\_RX\_TIMEOUT
:   UART receive data timeout

<a id="c.BK_ERR_UART_BAUD_RATE_NOT_SUPPORT"></a>

<a id="uart__types_8h_1a7cde4c77bbf4ffc06740c36d939b6a01"></a> BK\_ERR\_UART\_BAUD\_RATE\_NOT\_SUPPORT
:   UART baud rate not support

<a id="c.BK_ERR_UART_ID_NOT_INIT"></a>

<a id="uart__types_8h_1a39605dc2946f84bec7633e512be8f620"></a> BK\_ERR\_UART\_ID\_NOT\_INIT
:   UART id not init

<a id="c.BK_ERR_UART_MUTEX_INIT"></a>

<a id="uart__types_8h_1ad848664a57c4b65e090f63a0a828f8b1"></a> BK\_ERR\_UART\_MUTEX\_INIT
:   UART mutex init failed

<a id="c.BK_ERR_UART_CTS_TIMEOUT"></a>

<a id="uart__types_8h_1a231ef238119af863f68d02fbc8e35a12"></a> BK\_ERR\_UART\_CTS\_TIMEOUT
:   UART CTS timeout

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410uart_isr_t"></a>

<a id="_CPPv310uart_isr_t"></a> <a id="_CPPv210uart_isr_t"></a> <a id="uart_isr_t"></a> <a id="uart__types_8h_1a5ca58133e7286ec941c009abfc94c467"></a> typedef void (\*uart\_isr\_t)([uart\_id\_t](#_CPPv49uart_id_t "uart_id_t") id, void \*param)
:   UART interrupt service routine.

<a id="id2"></a>

### Header File

- [hal\_uart\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_uart_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv413uart_config_t"></a>

<a id="_CPPv313uart_config_t"></a> <a id="_CPPv213uart_config_t"></a> <a id="uart_config_t"></a> <a id="structuart__config__t"></a> struct uart\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13uart_config_t9baud_rateE"></a>

    <a id="_CPPv3N13uart_config_t9baud_rateE"></a> <a id="_CPPv2N13uart_config_t9baud_rateE"></a> <a id="uart_config_t::baud_rate__uint32_t"></a> <a id="structuart__config__t_1a988fe3be69cba628a241033f1b16f35e"></a> uint32\_t baud\_rate
    :   UART baud rate

    <a id="_CPPv4N13uart_config_t9data_bitsE"></a>

    <a id="_CPPv3N13uart_config_t9data_bitsE"></a> <a id="_CPPv2N13uart_config_t9data_bitsE"></a> <a id="uart_config_t::data_bits__uart_data_bits_t"></a> <a id="structuart__config__t_1ae568b92a4a64a148c136dd511a3aefe1"></a> [uart\_data\_bits\_t](#_CPPv416uart_data_bits_t "uart_data_bits_t") data\_bits
    :   UART data bits

    <a id="_CPPv4N13uart_config_t6parityE"></a>

    <a id="_CPPv3N13uart_config_t6parityE"></a> <a id="_CPPv2N13uart_config_t6parityE"></a> <a id="uart_config_t::parity__uart_parity_t"></a> <a id="structuart__config__t_1a157fe675a803f44325017b6b32a20824"></a> [uart\_parity\_t](#_CPPv413uart_parity_t "uart_parity_t") parity
    :   UART parity

    <a id="_CPPv4N13uart_config_t9stop_bitsE"></a>

    <a id="_CPPv3N13uart_config_t9stop_bitsE"></a> <a id="_CPPv2N13uart_config_t9stop_bitsE"></a> <a id="uart_config_t::stop_bits__uart_stop_bits_t"></a> <a id="structuart__config__t_1ac90c1cc43e3e84befa5f6e98d63bb2d8"></a> [uart\_stop\_bits\_t](#_CPPv416uart_stop_bits_t "uart_stop_bits_t") stop\_bits
    :   UART stop bits

    <a id="_CPPv4N13uart_config_t9flow_ctrlE"></a>

    <a id="_CPPv3N13uart_config_t9flow_ctrlE"></a> <a id="_CPPv2N13uart_config_t9flow_ctrlE"></a> <a id="uart_config_t::flow_ctrl__uart_flow_control_t"></a> <a id="structuart__config__t_1a31b20ef7c58a682bede999cd60013c91"></a> [uart\_flow\_control\_t](#_CPPv419uart_flow_control_t "uart_flow_control_t") flow\_ctrl
    :   UART flow control

    <a id="_CPPv4N13uart_config_t7src_clkE"></a>

    <a id="_CPPv3N13uart_config_t7src_clkE"></a> <a id="_CPPv2N13uart_config_t7src_clkE"></a> <a id="uart_config_t::src_clk__uart_src_clk_t"></a> <a id="structuart__config__t_1a88d4ee14d55d4c30db9fead53c33d0f3"></a> [uart\_src\_clk\_t](#_CPPv414uart_src_clk_t "uart_src_clk_t") src\_clk
    :   UART source clock

<a id="id3"></a>

### Macros

<a id="c.UART_BAUDRATE_3250000"></a>

<a id="hal__uart__types_8h_1a75c5b5ffad5076e37c00cb5e160d9f45"></a> UART\_BAUDRATE\_3250000

<a id="c.UART_BAUDRATE_2000000"></a>

<a id="hal__uart__types_8h_1acdf53f3f66fa76e39d6aea2d68593ed6"></a> UART\_BAUDRATE\_2000000

<a id="c.UART_BAUDRATE_921600"></a>

<a id="hal__uart__types_8h_1a04adc5a61ac8bca86e1ba1524f9ff7a5"></a> UART\_BAUDRATE\_921600

<a id="c.UART_BAUDRATE_460800"></a>

<a id="hal__uart__types_8h_1ad6bfe17a5c0f2881d5d524e4d7d85051"></a> UART\_BAUDRATE\_460800

<a id="c.UART_BAUDRATE_230400"></a>

<a id="hal__uart__types_8h_1a2c3b5462bda445df5ca24a1c756c9e76"></a> UART\_BAUDRATE\_230400

<a id="c.UART_BAUDRATE_115200"></a>

<a id="hal__uart__types_8h_1a7ba5033e1e1547d07d7683d0542c1f4a"></a> UART\_BAUDRATE\_115200

<a id="c.UART_BAUDRATE_3000"></a>

<a id="hal__uart__types_8h_1ac004f3bc6db3bdaea48e3989c28e66dd"></a> UART\_BAUDRATE\_3000

<a id="c.UART_BAUDRATE_19200"></a>

<a id="hal__uart__types_8h_1a61cfb7c7f0b8f41e5861a4cbd6b6ba64"></a> UART\_BAUDRATE\_19200

<a id="c.UART_BAUDRATE_9600"></a>

<a id="hal__uart__types_8h_1a4549807ebe0dd970e68e283921e80bb3"></a> UART\_BAUDRATE\_9600

<a id="c.UART_BAUD_RATE"></a>

<a id="hal__uart__types_8h_1a615aed21aa6825462b7c17b0c238ffe2"></a> UART\_BAUD\_RATE

<a id="c.UART_CLOCK_FREQ_10M"></a>

<a id="hal__uart__types_8h_1afa842e026584f7fa2891c1155e96a4f7"></a> UART\_CLOCK\_FREQ\_10M

<a id="c.UART_CLOCK_FREQ_48M"></a>

<a id="hal__uart__types_8h_1a69c14609deb77b34cba903b9f2e4f21a"></a> UART\_CLOCK\_FREQ\_48M

<a id="c.UART_CLOCK_FREQ_24M"></a>

<a id="hal__uart__types_8h_1ab5819d27f71651f9a90e10ea4baa8c6d"></a> UART\_CLOCK\_FREQ\_24M

<a id="c.UART_CLOCK_FREQ_26M"></a>

<a id="hal__uart__types_8h_1ac18fe2bcfe4c752908aaf20851a4e9c0"></a> UART\_CLOCK\_FREQ\_26M

<a id="c.UART_CLOCK_FREQ_52M"></a>

<a id="hal__uart__types_8h_1abc02d0341020b65d04ed434f86de17ac"></a> UART\_CLOCK\_FREQ\_52M

<a id="c.UART_CLOCK_FREQ_120M"></a>

<a id="hal__uart__types_8h_1ad1e7e072e674a9d0df7e6ad879a55962"></a> UART\_CLOCK\_FREQ\_120M

<a id="c.UART_CLOCK"></a>

<a id="hal__uart__types_8h_1a37ba45746e4dd0d1fbf6320bd4c0ce25"></a> UART\_CLOCK

<a id="c.UART_TX_FIFO_THRESHOLD"></a>

<a id="hal__uart__types_8h_1ab901fe232d5fbf5a4f8e0e7d84f3e511"></a> UART\_TX\_FIFO\_THRESHOLD

<a id="c.UART_RX_FIFO_THRESHOLD"></a>

<a id="hal__uart__types_8h_1a51e4a128056566eba14b19f4a51f3ff3"></a> UART\_RX\_FIFO\_THRESHOLD

<a id="id4"></a>

### Type Definitions

<a id="_CPPv411uart_unit_t"></a>

<a id="_CPPv311uart_unit_t"></a> <a id="_CPPv211uart_unit_t"></a> <a id="uart_unit_t"></a> <a id="hal__uart__types_8h_1aa716cc8ae3d9b93771de0989d28b7123"></a> typedef uint8\_t uart\_unit\_t
:   uart uint id

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv49uart_id_t"></a>

<a id="_CPPv39uart_id_t"></a> <a id="_CPPv29uart_id_t"></a> <a id="hal__uart__types_8h_1ada81ace00fa480969ed3a1938a6d9c43"></a> enum uart\_id\_t
:   *Values:*

    <a id="_CPPv4N9uart_id_t9UART_ID_0E"></a>

    <a id="_CPPv3N9uart_id_t9UART_ID_0E"></a> <a id="_CPPv2N9uart_id_t9UART_ID_0E"></a> <a id="hal__uart__types_8h_1ada81ace00fa480969ed3a1938a6d9c43ab58a70f5b9c0bc5a2bba9fbabce200a6"></a> enumerator UART\_ID\_0
    :   UART id 0

    <a id="_CPPv4N9uart_id_t9UART_ID_1E"></a>

    <a id="_CPPv3N9uart_id_t9UART_ID_1E"></a> <a id="_CPPv2N9uart_id_t9UART_ID_1E"></a> <a id="hal__uart__types_8h_1ada81ace00fa480969ed3a1938a6d9c43a8fb7a2c346bb0585ccbb713479ae2137"></a> enumerator UART\_ID\_1
    :   UART id 1

    <a id="_CPPv4N9uart_id_t9UART_ID_2E"></a>

    <a id="_CPPv3N9uart_id_t9UART_ID_2E"></a> <a id="_CPPv2N9uart_id_t9UART_ID_2E"></a> <a id="hal__uart__types_8h_1ada81ace00fa480969ed3a1938a6d9c43a430e093123da216f65b52edffbe47217"></a> enumerator UART\_ID\_2
    :   UART id 2

    <a id="_CPPv4N9uart_id_t11UART_ID_MAXE"></a>

    <a id="_CPPv3N9uart_id_t11UART_ID_MAXE"></a> <a id="_CPPv2N9uart_id_t11UART_ID_MAXE"></a> <a id="hal__uart__types_8h_1ada81ace00fa480969ed3a1938a6d9c43a355bd7de758b1eaf3743e220a9cb2de6"></a> enumerator UART\_ID\_MAX
    :   UART id max

<a id="_CPPv414uart_src_clk_t"></a>

<a id="_CPPv314uart_src_clk_t"></a> <a id="_CPPv214uart_src_clk_t"></a> <a id="hal__uart__types_8h_1acf2cbaebacc73389de21bc3d98430f7f"></a> enum uart\_src\_clk\_t
:   *Values:*

    <a id="_CPPv4N14uart_src_clk_t13UART_SCLK_DCOE"></a>

    <a id="_CPPv3N14uart_src_clk_t13UART_SCLK_DCOE"></a> <a id="_CPPv2N14uart_src_clk_t13UART_SCLK_DCOE"></a> <a id="hal__uart__types_8h_1acf2cbaebacc73389de21bc3d98430f7fab7306b088119ea25e916cd95bbec72e4"></a> enumerator UART\_SCLK\_DCO
    :   UART source clock dco

    <a id="_CPPv4N14uart_src_clk_t18UART_SCLK_XTAL_26ME"></a>

    <a id="_CPPv3N14uart_src_clk_t18UART_SCLK_XTAL_26ME"></a> <a id="_CPPv2N14uart_src_clk_t18UART_SCLK_XTAL_26ME"></a> <a id="hal__uart__types_8h_1acf2cbaebacc73389de21bc3d98430f7fab013ac68405a637967edb4c99767160a"></a> enumerator UART\_SCLK\_XTAL\_26M
    :   UART source clock xtal 26M

    <a id="_CPPv4N14uart_src_clk_t14UART_SCLK_APLLE"></a>

    <a id="_CPPv3N14uart_src_clk_t14UART_SCLK_APLLE"></a> <a id="_CPPv2N14uart_src_clk_t14UART_SCLK_APLLE"></a> <a id="hal__uart__types_8h_1acf2cbaebacc73389de21bc3d98430f7fa4cd4b057859b240f0c9ed142b4f6e279"></a> enumerator UART\_SCLK\_APLL
    :   UART source clock apll

<a id="_CPPv417uart_frame_mode_t"></a>

<a id="_CPPv317uart_frame_mode_t"></a> <a id="_CPPv217uart_frame_mode_t"></a> <a id="hal__uart__types_8h_1a489676c2fc74d962d8ee07b8e54466f5"></a> enum uart\_frame\_mode\_t
:   *Values:*

    <a id="_CPPv4N17uart_frame_mode_t14UART_MODE_UARTE"></a>

    <a id="_CPPv3N17uart_frame_mode_t14UART_MODE_UARTE"></a> <a id="_CPPv2N17uart_frame_mode_t14UART_MODE_UARTE"></a> <a id="hal__uart__types_8h_1a489676c2fc74d962d8ee07b8e54466f5a068436d1319f7158782d371df48a7651"></a> enumerator UART\_MODE\_UART
    :   UART frame mode uart

    <a id="_CPPv4N17uart_frame_mode_t14UART_MODE_IDRAE"></a>

    <a id="_CPPv3N17uart_frame_mode_t14UART_MODE_IDRAE"></a> <a id="_CPPv2N17uart_frame_mode_t14UART_MODE_IDRAE"></a> <a id="hal__uart__types_8h_1a489676c2fc74d962d8ee07b8e54466f5a26c4a800f3e505e242301bfcc0682a0b"></a> enumerator UART\_MODE\_IDRA
    :   UART frame mode idra

<a id="_CPPv416uart_data_bits_t"></a>

<a id="_CPPv316uart_data_bits_t"></a> <a id="_CPPv216uart_data_bits_t"></a> <a id="hal__uart__types_8h_1adc68b8fd9ded3990f84129df23fee798"></a> enum uart\_data\_bits\_t
:   *Values:*

    <a id="_CPPv4N16uart_data_bits_t16UART_DATA_5_BITSE"></a>

    <a id="_CPPv3N16uart_data_bits_t16UART_DATA_5_BITSE"></a> <a id="_CPPv2N16uart_data_bits_t16UART_DATA_5_BITSE"></a> <a id="hal__uart__types_8h_1adc68b8fd9ded3990f84129df23fee798a45437f3ff3941ae72e531dfb755456f4"></a> enumerator UART\_DATA\_5\_BITS
    :   UART data bits 5bits

    <a id="_CPPv4N16uart_data_bits_t16UART_DATA_6_BITSE"></a>

    <a id="_CPPv3N16uart_data_bits_t16UART_DATA_6_BITSE"></a> <a id="_CPPv2N16uart_data_bits_t16UART_DATA_6_BITSE"></a> <a id="hal__uart__types_8h_1adc68b8fd9ded3990f84129df23fee798a2f062e3e06c3560077fe86fef6b8d9cb"></a> enumerator UART\_DATA\_6\_BITS
    :   UART data bits 6bits

    <a id="_CPPv4N16uart_data_bits_t16UART_DATA_7_BITSE"></a>

    <a id="_CPPv3N16uart_data_bits_t16UART_DATA_7_BITSE"></a> <a id="_CPPv2N16uart_data_bits_t16UART_DATA_7_BITSE"></a> <a id="hal__uart__types_8h_1adc68b8fd9ded3990f84129df23fee798aa5bd9a1dad740644b4c60fe0a8f9addd"></a> enumerator UART\_DATA\_7\_BITS
    :   UART data bits 7bits

    <a id="_CPPv4N16uart_data_bits_t16UART_DATA_8_BITSE"></a>

    <a id="_CPPv3N16uart_data_bits_t16UART_DATA_8_BITSE"></a> <a id="_CPPv2N16uart_data_bits_t16UART_DATA_8_BITSE"></a> <a id="hal__uart__types_8h_1adc68b8fd9ded3990f84129df23fee798a92b996b63bd23267f72518c51a79936e"></a> enumerator UART\_DATA\_8\_BITS
    :   UART data bits 8bits

<a id="_CPPv413uart_parity_t"></a>

<a id="_CPPv313uart_parity_t"></a> <a id="_CPPv213uart_parity_t"></a> <a id="hal__uart__types_8h_1a6bcc37e31dd40c204b4ac6f6189e8878"></a> enum uart\_parity\_t
:   *Values:*

    <a id="_CPPv4N13uart_parity_t16UART_PARITY_NONEE"></a>

    <a id="_CPPv3N13uart_parity_t16UART_PARITY_NONEE"></a> <a id="_CPPv2N13uart_parity_t16UART_PARITY_NONEE"></a> <a id="hal__uart__types_8h_1a6bcc37e31dd40c204b4ac6f6189e8878aa80d2d8ea61454045ebe71d155e85b3d"></a> enumerator UART\_PARITY\_NONE
    :   UART parity none

    <a id="_CPPv4N13uart_parity_t15UART_PARITY_ODDE"></a>

    <a id="_CPPv3N13uart_parity_t15UART_PARITY_ODDE"></a> <a id="_CPPv2N13uart_parity_t15UART_PARITY_ODDE"></a> <a id="hal__uart__types_8h_1a6bcc37e31dd40c204b4ac6f6189e8878ad90cc425f5ba447773a44a75be6593e2"></a> enumerator UART\_PARITY\_ODD
    :   UART parity odd

    <a id="_CPPv4N13uart_parity_t16UART_PARITY_EVENE"></a>

    <a id="_CPPv3N13uart_parity_t16UART_PARITY_EVENE"></a> <a id="_CPPv2N13uart_parity_t16UART_PARITY_EVENE"></a> <a id="hal__uart__types_8h_1a6bcc37e31dd40c204b4ac6f6189e8878ad908a637b1dd23f93b149dd2d8bdfdb8"></a> enumerator UART\_PARITY\_EVEN
    :   UART parity even

<a id="_CPPv416uart_stop_bits_t"></a>

<a id="_CPPv316uart_stop_bits_t"></a> <a id="_CPPv216uart_stop_bits_t"></a> <a id="hal__uart__types_8h_1a6da57a73bbdbf830b845d4116f8341d7"></a> enum uart\_stop\_bits\_t
:   *Values:*

    <a id="_CPPv4N16uart_stop_bits_t16UART_STOP_BITS_1E"></a>

    <a id="_CPPv3N16uart_stop_bits_t16UART_STOP_BITS_1E"></a> <a id="_CPPv2N16uart_stop_bits_t16UART_STOP_BITS_1E"></a> <a id="hal__uart__types_8h_1a6da57a73bbdbf830b845d4116f8341d7a44b3bfbe90aebe2b23227f5c011f41cc"></a> enumerator UART\_STOP\_BITS\_1
    :   UART stop bits 1bit

    <a id="_CPPv4N16uart_stop_bits_t16UART_STOP_BITS_2E"></a>

    <a id="_CPPv3N16uart_stop_bits_t16UART_STOP_BITS_2E"></a> <a id="_CPPv2N16uart_stop_bits_t16UART_STOP_BITS_2E"></a> <a id="hal__uart__types_8h_1a6da57a73bbdbf830b845d4116f8341d7a00c73c92b3d624bc86cfa63636dd99b3"></a> enumerator UART\_STOP\_BITS\_2
    :   UART stop bits 2bits

<a id="_CPPv419uart_flow_control_t"></a>

<a id="_CPPv319uart_flow_control_t"></a> <a id="_CPPv219uart_flow_control_t"></a> <a id="hal__uart__types_8h_1a7882852eb00c56bff774f58d88e6d8f0"></a> enum uart\_flow\_control\_t
:   *Values:*

    <a id="_CPPv4N19uart_flow_control_t21UART_FLOWCTRL_DISABLEE"></a>

    <a id="_CPPv3N19uart_flow_control_t21UART_FLOWCTRL_DISABLEE"></a> <a id="_CPPv2N19uart_flow_control_t21UART_FLOWCTRL_DISABLEE"></a> <a id="hal__uart__types_8h_1a7882852eb00c56bff774f58d88e6d8f0a6c225e159e32fc457df6f6909aba9284"></a> enumerator UART\_FLOWCTRL\_DISABLE
    :   UART flow control disable

    <a id="_CPPv4N19uart_flow_control_t21UART_FLOWCTRL_CTS_RTSE"></a>

    <a id="_CPPv3N19uart_flow_control_t21UART_FLOWCTRL_CTS_RTSE"></a> <a id="_CPPv2N19uart_flow_control_t21UART_FLOWCTRL_CTS_RTSE"></a> <a id="hal__uart__types_8h_1a7882852eb00c56bff774f58d88e6d8f0a9087af14b51f567f338f3f2bf93b83a0"></a> enumerator UART\_FLOWCTRL\_CTS\_RTS
    :   UART flow control cts rts

<a id="_CPPv426uart_rx_stop_detect_time_t"></a>

<a id="_CPPv326uart_rx_stop_detect_time_t"></a> <a id="_CPPv226uart_rx_stop_detect_time_t"></a> <a id="hal__uart__types_8h_1a48e25f230a4b3015b1f11477d6f01b24"></a> enum uart\_rx\_stop\_detect\_time\_t
:   *Values:*

    <a id="_CPPv4N26uart_rx_stop_detect_time_t32UART_RX_STOP_DETECT_TIME_32_BITSE"></a>

    <a id="_CPPv3N26uart_rx_stop_detect_time_t32UART_RX_STOP_DETECT_TIME_32_BITSE"></a> <a id="_CPPv2N26uart_rx_stop_detect_time_t32UART_RX_STOP_DETECT_TIME_32_BITSE"></a> <a id="hal__uart__types_8h_1a48e25f230a4b3015b1f11477d6f01b24afe931b35b388d2c67fd4e123ef0ff915"></a> enumerator UART\_RX\_STOP\_DETECT\_TIME\_32\_BITS
    :   UART rx stop time 32 bits

    <a id="_CPPv4N26uart_rx_stop_detect_time_t32UART_RX_STOP_DETECT_TIME_64_BITSE"></a>

    <a id="_CPPv3N26uart_rx_stop_detect_time_t32UART_RX_STOP_DETECT_TIME_64_BITSE"></a> <a id="_CPPv2N26uart_rx_stop_detect_time_t32UART_RX_STOP_DETECT_TIME_64_BITSE"></a> <a id="hal__uart__types_8h_1a48e25f230a4b3015b1f11477d6f01b24abb3b5c70e38e3d10351bdea6f3094635"></a> enumerator UART\_RX\_STOP\_DETECT\_TIME\_64\_BITS
    :   UART rx stop time 64 bits

    <a id="_CPPv4N26uart_rx_stop_detect_time_t33UART_RX_STOP_DETECT_TIME_128_BITSE"></a>

    <a id="_CPPv3N26uart_rx_stop_detect_time_t33UART_RX_STOP_DETECT_TIME_128_BITSE"></a> <a id="_CPPv2N26uart_rx_stop_detect_time_t33UART_RX_STOP_DETECT_TIME_128_BITSE"></a> <a id="hal__uart__types_8h_1a48e25f230a4b3015b1f11477d6f01b24a5969550e328d569c1f5eae35e1888312"></a> enumerator UART\_RX\_STOP\_DETECT\_TIME\_128\_BITS
    :   UART rx stop time 128 bits

    <a id="_CPPv4N26uart_rx_stop_detect_time_t33UART_RX_STOP_DETECT_TIME_256_BITSE"></a>

    <a id="_CPPv3N26uart_rx_stop_detect_time_t33UART_RX_STOP_DETECT_TIME_256_BITSE"></a> <a id="_CPPv2N26uart_rx_stop_detect_time_t33UART_RX_STOP_DETECT_TIME_256_BITSE"></a> <a id="hal__uart__types_8h_1a48e25f230a4b3015b1f11477d6f01b24a764794ccb60bf90e5a1de974520f6040"></a> enumerator UART\_RX\_STOP\_DETECT\_TIME\_256\_BITS
    :   UART rx stop time 256 bits

<a id="_CPPv417uart_dma_enable_t"></a>

<a id="_CPPv317uart_dma_enable_t"></a> <a id="_CPPv217uart_dma_enable_t"></a> <a id="hal__uart__types_8h_1a00b94e115672de603c7e466ba50ec74f"></a> enum uart\_dma\_enable\_t
:   *Values:*

    <a id="_CPPv4N17uart_dma_enable_t16UART_DMA_DISABLEE"></a>

    <a id="_CPPv3N17uart_dma_enable_t16UART_DMA_DISABLEE"></a> <a id="_CPPv2N17uart_dma_enable_t16UART_DMA_DISABLEE"></a> <a id="hal__uart__types_8h_1a00b94e115672de603c7e466ba50ec74fa1b8df60eb38bbb0a887c9c167f473500"></a> enumerator UART\_DMA\_DISABLE

    <a id="_CPPv4N17uart_dma_enable_t15UART_DMA_ENABLEE"></a>

    <a id="_CPPv3N17uart_dma_enable_t15UART_DMA_ENABLEE"></a> <a id="_CPPv2N17uart_dma_enable_t15UART_DMA_ENABLEE"></a> <a id="hal__uart__types_8h_1a00b94e115672de603c7e466ba50ec74fa9726c6224c09fac87c81d71a192fc032"></a> enumerator UART\_DMA\_ENABLE
