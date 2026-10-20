---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_spi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="spi"></a>

# SPI

<a id="spi-api-status"></a>

## SPI API Status

| API | BK7259\_AP |
| --- | --- |
| [`bk_spi_driver_init()`](#_CPPv418bk_spi_driver_initv "bk_spi_driver_init") | Y |
| [`bk_spi_driver_deinit()`](#_CPPv420bk_spi_driver_deinitv "bk_spi_driver_deinit") | Y |
| [`bk_spi_init()`](#_CPPv411bk_spi_init8spi_id_tPK12spi_config_t "bk_spi_init") | Y |
| [`bk_spi_deinit()`](#_CPPv413bk_spi_deinit8spi_id_t "bk_spi_deinit") | Y |
| [`bk_spi_set_mode()`](#_CPPv415bk_spi_set_mode8spi_id_t10spi_mode_t "bk_spi_set_mode") | Y |
| [`bk_spi_set_bit_width()`](#_CPPv420bk_spi_set_bit_width8spi_id_t15spi_bit_width_t "bk_spi_set_bit_width") | Y |
| [`bk_spi_set_wire_mode()`](#_CPPv420bk_spi_set_wire_mode8spi_id_t15spi_wire_mode_t "bk_spi_set_wire_mode") | Y |
| [`bk_spi_set_baud_rate()`](#_CPPv420bk_spi_set_baud_rate8spi_id_t8uint32_t "bk_spi_set_baud_rate") | Y |
| [`bk_spi_set_bit_order()`](#_CPPv420bk_spi_set_bit_order8spi_id_t15spi_bit_order_t "bk_spi_set_bit_order") | Y |
| [`bk_spi_set_role()`](#_CPPv415bk_spi_set_role8spi_id_t10spi_role_t "bk_spi_set_role") | Y |
| [`bk_spi_clear_tx_fifo()`](#_CPPv420bk_spi_clear_tx_fifo8spi_id_t "bk_spi_clear_tx_fifo") | Y |
| [`bk_spi_clear_rx_fifo()`](#_CPPv420bk_spi_clear_rx_fifo8spi_id_t "bk_spi_clear_rx_fifo") | Y |
| [`bk_spi_clr_tx()`](#_CPPv413bk_spi_clr_tx8spi_id_t "bk_spi_clr_tx") | Y |
| [`bk_spi_clr_rx()`](#_CPPv413bk_spi_clr_rx8spi_id_t "bk_spi_clr_rx") | Y |
| [`bk_spi_register_rx_isr()`](#_CPPv422bk_spi_register_rx_isr8spi_id_t9spi_isr_tPv "bk_spi_register_rx_isr") | Y |
| [`bk_spi_register_tx_finish_isr()`](#_CPPv429bk_spi_register_tx_finish_isr8spi_id_t9spi_isr_tPv "bk_spi_register_tx_finish_isr") | Y |
| [`bk_spi_register_rx_finish_isr()`](#_CPPv429bk_spi_register_rx_finish_isr8spi_id_t9spi_isr_tPv "bk_spi_register_rx_finish_isr") | Y |
| [`bk_spi_unregister_rx_isr()`](#_CPPv424bk_spi_unregister_rx_isr8spi_id_t "bk_spi_unregister_rx_isr") | Y |
| [`bk_spi_unregister_tx_finish_isr()`](#_CPPv431bk_spi_unregister_tx_finish_isr8spi_id_t "bk_spi_unregister_tx_finish_isr") | Y |
| [`bk_spi_unregister_rx_finish_isr()`](#_CPPv431bk_spi_unregister_rx_finish_isr8spi_id_t "bk_spi_unregister_rx_finish_isr") | Y |
| [`bk_spi_write_bytes()`](#_CPPv418bk_spi_write_bytes8spi_id_tPKv8uint32_t "bk_spi_write_bytes") | Y |
| [`bk_spi_read_bytes()`](#_CPPv417bk_spi_read_bytes8spi_id_tPv8uint32_t "bk_spi_read_bytes") | Y |
| [`bk_spi_write_bytes_async()`](#_CPPv424bk_spi_write_bytes_async8spi_id_tPKv8uint32_t "bk_spi_write_bytes_async") | Y |
| [`bk_spi_read_bytes_async()`](#_CPPv423bk_spi_read_bytes_async8spi_id_tPv8uint32_t "bk_spi_read_bytes_async") | Y |
| `bk_spi_dma_write_bytes()` | Y |
| `bk_spi_dma_read_bytes()` | Y |
| `bk_spi_dma_duplex_init()` | Y |
| `bk_spi_dma_duplex_deinit()` | Y |
| `bk_spi_dma_duplex_xfer()` | Y |

<a id="spi-unit-number"></a>

## SPI UNIT Number

| Capability | BK7259\_AP | 说明 |
| --- | --- | --- |
| UNIT Number | 1\~4 | 由 CONFIG\_SOC\_SPI\_UNIT\_NUM 配置，默认 2 |

<a id="spi-gpio"></a>

## SPI GPIO 映射说明

BK7259 AP 的 SPI0\~SPI3 引脚均为灵活映射，无固定 GPIO 编号。用户须在工程
projects/\<工程\>/config/bk7259\_ap/usr\_gpio\_cfg.h 的 GPIO\_DEFAULT\_DEV\_CONFIG 中，
将所需 pad 配置为 GPIO\_DEV\_SPIx 的 SCK、CSN、MOSI、MISO（x \= 0\~3）。

bk\_spi\_init 通过 gpio\_dev\_map\_by\_func 查找上述配置表完成引脚映射。
可选 pad 范围及 IO Matrix 约束见 ap/middleware/soc/bk7259\_ap/soc/gpio\_map.h 中
GPIO\_DEV\_TO\_IOMX\_CODE\_MAP；配置方法见 [GPIO 使用指南](../../developer-guide/peripheral/bk_gpio.md)。

SPI 功能与 GPIO 设备枚举对应关系：

| SPI 单元 | GPIO 设备枚举 |
| --- | --- |
| SPI0 | GPIO\_DEV\_SPI0\_SCK、CSN、MOSI、MISO |
| SPI1 | GPIO\_DEV\_SPI1\_SCK、CSN、MOSI、MISO |
| SPI2 | GPIO\_DEV\_SPI2\_SCK、CSN、MOSI、MISO |
| SPI3 | GPIO\_DEV\_SPI3\_SCK、CSN、MOSI、MISO |

<a id="spi-api-reference"></a>

## SPI API Reference

<a id="header-file"></a>

### Header File

- [spi.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/spi.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_spi_driver_initv"></a>

<a id="_CPPv318bk_spi_driver_initv"></a> <a id="_CPPv218bk_spi_driver_initv"></a> <a id="bk_spi_driver_init__void"></a> <a id="spi_8h_1aad9a9d4f974fa3cbc151d753a36bf944"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_driver\_init(void)
:   Init the SPI driver.

    This API init the resoure common:

    - Init SPI driver control memory

    **Attention**
    :   1\. This API should be called before any other SPI APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_spi_driver_deinitv"></a>

<a id="_CPPv320bk_spi_driver_deinitv"></a> <a id="_CPPv220bk_spi_driver_deinitv"></a> <a id="bk_spi_driver_deinit__void"></a> <a id="spi_8h_1a67161f339fa790324b07af5c3b3d3abb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_driver\_deinit(void)
:   Deinit the SPI driver.

    This API free all resource related to SPI and disable SPI.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_spi_init8spi_id_tPK12spi_config_t"></a>

<a id="_CPPv311bk_spi_init8spi_id_tPK12spi_config_t"></a> <a id="_CPPv211bk_spi_init8spi_id_tPK12spi_config_t"></a> <a id="bk_spi_init__spi_id_t.spi_config_tCP"></a> <a id="spi_8h_1a15e4e8c43d7a750b9fc092443fc1f8c2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_init([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, const [spi\_config\_t](#_CPPv412spi_config_t "spi_config_t") \*config)
:   Init the SPI id.

    This API init the SPI id:

    - Power up the SPI id
    - Configure the SPI id clock
    - Map the SPI id to dedicated GPIO port
    - Set the SPI parameters
    - Start the SPI id

    参数
    :   - **id** – SPI id
        - **config** – SPI parameter settings

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: SPI config paramter is NULL
        - BK\_ERR\_SPI\_NOT\_INIT: SPI driver not init
        - BK\_ERR\_SPI\_INVALID\_ID: SPI id is invalid
        - others: other errors.

<a id="_CPPv413bk_spi_deinit8spi_id_t"></a>

<a id="_CPPv313bk_spi_deinit8spi_id_t"></a> <a id="_CPPv213bk_spi_deinit8spi_id_t"></a> <a id="bk_spi_deinit__spi_id_t"></a> <a id="spi_8h_1a96f60bcf20308e16506aa164a1ec292b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_deinit([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id)
:   Deinit the SPI id.

    This API deinit the SPI id:

    - Stop the SPI id
    - Disable the SPI id interrupt
    - Power down the SPI id

    参数
    :   **id** – SPI id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_spi_set_mode8spi_id_t10spi_mode_t"></a>

<a id="_CPPv315bk_spi_set_mode8spi_id_t10spi_mode_t"></a> <a id="_CPPv215bk_spi_set_mode8spi_id_t10spi_mode_t"></a> <a id="bk_spi_set_mode__spi_id_t.spi_mode_t"></a> <a id="spi_8h_1a021d0b93196974058152ef5e7903dfa6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_set\_mode([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, [spi\_mode\_t](#_CPPv410spi_mode_t "spi_mode_t") mode)
:   Set the SPI mode.

    参数
    :   - **id** – SPI id
        - **mode** – SPI mode

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_spi_set_bit_width8spi_id_t15spi_bit_width_t"></a>

<a id="_CPPv320bk_spi_set_bit_width8spi_id_t15spi_bit_width_t"></a> <a id="_CPPv220bk_spi_set_bit_width8spi_id_t15spi_bit_width_t"></a> <a id="bk_spi_set_bit_width__spi_id_t.spi_bit_width_t"></a> <a id="spi_8h_1ae69150917075354cb9322704454b9776"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_set\_bit\_width([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, [spi\_bit\_width\_t](#_CPPv415spi_bit_width_t "spi_bit_width_t") bit\_width)
:   Set the SPI bit width.

    参数
    :   - **id** – SPI id
        - **bit\_width** – SPI bit width

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_spi_set_wire_mode8spi_id_t15spi_wire_mode_t"></a>

<a id="_CPPv320bk_spi_set_wire_mode8spi_id_t15spi_wire_mode_t"></a> <a id="_CPPv220bk_spi_set_wire_mode8spi_id_t15spi_wire_mode_t"></a> <a id="bk_spi_set_wire_mode__spi_id_t.spi_wire_mode_t"></a> <a id="spi_8h_1a5e341b3b8a32bd848cd4aa0cf5e7e32b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_set\_wire\_mode([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, [spi\_wire\_mode\_t](#_CPPv415spi_wire_mode_t "spi_wire_mode_t") wire\_mode)
:   Set the SPI wire mode.

    参数
    :   - **id** – SPI id
        - **wire\_mode** – SPI wire mode

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_spi_set_baud_rate8spi_id_t8uint32_t"></a>

<a id="_CPPv320bk_spi_set_baud_rate8spi_id_t8uint32_t"></a> <a id="_CPPv220bk_spi_set_baud_rate8spi_id_t8uint32_t"></a> <a id="bk_spi_set_baud_rate__spi_id_t.uint32_t"></a> <a id="spi_8h_1a52b2528e02599fc4d60739b1f182c7c3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_set\_baud\_rate([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, uint32\_t baud\_rate)
:   Set the SPI baud rate.

    参数
    :   - **id** – SPI id
        - **baud\_rate** – SPI baud rate

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_spi_set_bit_order8spi_id_t15spi_bit_order_t"></a>

<a id="_CPPv320bk_spi_set_bit_order8spi_id_t15spi_bit_order_t"></a> <a id="_CPPv220bk_spi_set_bit_order8spi_id_t15spi_bit_order_t"></a> <a id="bk_spi_set_bit_order__spi_id_t.spi_bit_order_t"></a> <a id="spi_8h_1a5bc86c748258f55346b29da30911cfa0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_set\_bit\_order([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, [spi\_bit\_order\_t](#_CPPv415spi_bit_order_t "spi_bit_order_t") bit\_order)
:   Set the SPI bit order.

    参数
    :   - **id** – SPI id
        - **bit\_order** – SPI bit order

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_spi_set_role8spi_id_t10spi_role_t"></a>

<a id="_CPPv315bk_spi_set_role8spi_id_t10spi_role_t"></a> <a id="_CPPv215bk_spi_set_role8spi_id_t10spi_role_t"></a> <a id="bk_spi_set_role__spi_id_t.spi_role_t"></a> <a id="spi_8h_1a1de563596ba5a3378e2fa4d6933d61e8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_set\_role([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, [spi\_role\_t](#_CPPv410spi_role_t "spi_role_t") role)

<a id="_CPPv420bk_spi_clear_tx_fifo8spi_id_t"></a>

<a id="_CPPv320bk_spi_clear_tx_fifo8spi_id_t"></a> <a id="_CPPv220bk_spi_clear_tx_fifo8spi_id_t"></a> <a id="bk_spi_clear_tx_fifo__spi_id_t"></a> <a id="spi_8h_1a7efdcbba3ea1ee46ef083a2794a0e279"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_clear\_tx\_fifo([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id)

<a id="_CPPv420bk_spi_clear_rx_fifo8spi_id_t"></a>

<a id="_CPPv320bk_spi_clear_rx_fifo8spi_id_t"></a> <a id="_CPPv220bk_spi_clear_rx_fifo8spi_id_t"></a> <a id="bk_spi_clear_rx_fifo__spi_id_t"></a> <a id="spi_8h_1a0e69b882517af2abbd7edecea6860247"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_clear\_rx\_fifo([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id)

<a id="_CPPv413bk_spi_clr_tx8spi_id_t"></a>

<a id="_CPPv313bk_spi_clr_tx8spi_id_t"></a> <a id="_CPPv213bk_spi_clr_tx8spi_id_t"></a> <a id="bk_spi_clr_tx__spi_id_t"></a> <a id="spi_8h_1a9f105ba203ec4294f490215a580f1333"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_clr\_tx([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id)

<a id="_CPPv413bk_spi_clr_rx8spi_id_t"></a>

<a id="_CPPv313bk_spi_clr_rx8spi_id_t"></a> <a id="_CPPv213bk_spi_clr_rx8spi_id_t"></a> <a id="bk_spi_clr_rx__spi_id_t"></a> <a id="spi_8h_1a420177067b57e736b4ee671a57d78f1c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_clr\_rx([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id)

<a id="_CPPv422bk_spi_register_rx_isr8spi_id_t9spi_isr_tPv"></a>

<a id="_CPPv322bk_spi_register_rx_isr8spi_id_t9spi_isr_tPv"></a> <a id="_CPPv222bk_spi_register_rx_isr8spi_id_t9spi_isr_tPv"></a> <a id="bk_spi_register_rx_isr__spi_id_t.spi_isr_t.voidP"></a> <a id="spi_8h_1a2d6ebb7fc822810d52250fc02a5ebb15"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_register\_rx\_isr([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, [spi\_isr\_t](#_CPPv49spi_isr_t "spi_isr_t") isr, void \*param)
:   Register the RX interrupt service routine for SPI id.

    参数
    :   - **id** – spi id
        - **isr** – SPI RX callback
        - **param** – SPI RX callback parameter

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv429bk_spi_register_tx_finish_isr8spi_id_t9spi_isr_tPv"></a>

<a id="_CPPv329bk_spi_register_tx_finish_isr8spi_id_t9spi_isr_tPv"></a> <a id="_CPPv229bk_spi_register_tx_finish_isr8spi_id_t9spi_isr_tPv"></a> <a id="bk_spi_register_tx_finish_isr__spi_id_t.spi_isr_t.voidP"></a> <a id="spi_8h_1ac400893791227c0a66ab1539e63117ca"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_register\_tx\_finish\_isr([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, [spi\_isr\_t](#_CPPv49spi_isr_t "spi_isr_t") isr, void \*param)
:   Register the TX finish interrupt service routine for SPI id.

    参数
    :   - **id** – SPi id
        - **isr** – SPI TX finish callback
        - **param** – SPi TX callback parameter

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_spi_write_bytes8spi_id_tPKv8uint32_t"></a>

<a id="_CPPv318bk_spi_write_bytes8spi_id_tPKv8uint32_t"></a> <a id="_CPPv218bk_spi_write_bytes8spi_id_tPKv8uint32_t"></a> <a id="bk_spi_write_bytes__spi_id_t.voidCP.uint32_t"></a> <a id="spi_8h_1a2a3305509c196126c835e783da00da13"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_write\_bytes([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, const void \*data, uint32\_t size)
:   Send data to the SPI port from a given buffer and length.

    参数
    :   - **id** – spi id
        - **data** – data buffer address
        - **size** – data length to send

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_SPI\_NOT\_INIT: SPI driver not init
        - BK\_ERR\_SPI\_INVALID\_ID: SPI id number is invalid
        - BK\_ERR\_SPI\_ID\_NOT\_INIT: SPI id not init
        - others: other errors.

<a id="_CPPv417bk_spi_read_bytes8spi_id_tPv8uint32_t"></a>

<a id="_CPPv317bk_spi_read_bytes8spi_id_tPv8uint32_t"></a> <a id="_CPPv217bk_spi_read_bytes8spi_id_tPv8uint32_t"></a> <a id="bk_spi_read_bytes__spi_id_t.voidP.uint32_t"></a> <a id="spi_8h_1a9bf07de51a574ac446771552f811f617"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_read\_bytes([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, void \*data, uint32\_t size)
:   SPI read bytes from SPI buffer.

    参数
    :   - **id** – SPI id
        - **data** – pointer to the buffer
        - **size** – data length to read

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_SPI\_NOT\_INIT: SPI driver not init
        - BK\_ERR\_SPI\_INVALID\_ID: SPI id number is invalid
        - BK\_ERR\_SPI\_ID\_NOT\_INIT: SPI id not init
        - others: other errors.

<a id="_CPPv429bk_spi_register_rx_finish_isr8spi_id_t9spi_isr_tPv"></a>

<a id="_CPPv329bk_spi_register_rx_finish_isr8spi_id_t9spi_isr_tPv"></a> <a id="_CPPv229bk_spi_register_rx_finish_isr8spi_id_t9spi_isr_tPv"></a> <a id="bk_spi_register_rx_finish_isr__spi_id_t.spi_isr_t.voidP"></a> <a id="spi_8h_1a089e304f198c8a694909be1212c8e6cd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_register\_rx\_finish\_isr([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, [spi\_isr\_t](#_CPPv49spi_isr_t "spi_isr_t") isr, void \*param)
:   Register the RX finish interrupt service routine for SPI id.

    参数
    :   - **id** – spi id
        - **isr** – SPI RX callback
        - **param** – SPI RX callback parameter

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_spi_unregister_rx_isr8spi_id_t"></a>

<a id="_CPPv324bk_spi_unregister_rx_isr8spi_id_t"></a> <a id="_CPPv224bk_spi_unregister_rx_isr8spi_id_t"></a> <a id="bk_spi_unregister_rx_isr__spi_id_t"></a> <a id="spi_8h_1aa99792f0ad7b80ca1ed797e96c5d0e2b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_unregister\_rx\_isr([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id)
:   Unregister the RX interrupt service routine for SPI id.

    参数
    :   **id** – spi id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv431bk_spi_unregister_rx_finish_isr8spi_id_t"></a>

<a id="_CPPv331bk_spi_unregister_rx_finish_isr8spi_id_t"></a> <a id="_CPPv231bk_spi_unregister_rx_finish_isr8spi_id_t"></a> <a id="bk_spi_unregister_rx_finish_isr__spi_id_t"></a> <a id="spi_8h_1a66ff6c686208061a5e2f2a740e69f3f7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_unregister\_rx\_finish\_isr([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id)
:   Unregister the RX finish interrupt service routine for SPI id.

    参数
    :   **id** – spi id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv431bk_spi_unregister_tx_finish_isr8spi_id_t"></a>

<a id="_CPPv331bk_spi_unregister_tx_finish_isr8spi_id_t"></a> <a id="_CPPv231bk_spi_unregister_tx_finish_isr8spi_id_t"></a> <a id="bk_spi_unregister_tx_finish_isr__spi_id_t"></a> <a id="spi_8h_1ae9e27ca8feedea37bfb07998ec8033f5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_unregister\_tx\_finish\_isr([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id)
:   Unregister the TX finish interrupt service routine for SPI id.

    参数
    :   **id** – spi id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_spi_write_bytes_async8spi_id_tPKv8uint32_t"></a>

<a id="_CPPv324bk_spi_write_bytes_async8spi_id_tPKv8uint32_t"></a> <a id="_CPPv224bk_spi_write_bytes_async8spi_id_tPKv8uint32_t"></a> <a id="bk_spi_write_bytes_async__spi_id_t.voidCP.uint32_t"></a> <a id="spi_8h_1a9b8323f2507542d3c683494d21cdccb6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_write\_bytes\_async([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, const void \*data, uint32\_t size)
:   Send data to the SPI port from a given buffer and length in async mode.

    参数
    :   - **id** – spi id
        - **data** – data buffer address
        - **size** – data length to send

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_SPI\_NOT\_INIT: SPI driver not init
        - BK\_ERR\_SPI\_INVALID\_ID: SPI id number is invalid
        - BK\_ERR\_SPI\_ID\_NOT\_INIT: SPI id not init
        - others: other errors.

<a id="_CPPv423bk_spi_read_bytes_async8spi_id_tPv8uint32_t"></a>

<a id="_CPPv323bk_spi_read_bytes_async8spi_id_tPv8uint32_t"></a> <a id="_CPPv223bk_spi_read_bytes_async8spi_id_tPv8uint32_t"></a> <a id="bk_spi_read_bytes_async__spi_id_t.voidP.uint32_t"></a> <a id="spi_8h_1affaf6dc6b2e8d571f6d4682c8295afbd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spi\_read\_bytes\_async([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, void \*data, uint32\_t size)
:   SPI read bytes from SPI buffer in async mode.

    参数
    :   - **id** – SPI id
        - **data** – pointer to the buffer
        - **size** – data length to read

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_SPI\_NOT\_INIT: SPI driver not init
        - BK\_ERR\_SPI\_INVALID\_ID: SPI id number is invalid
        - BK\_ERR\_SPI\_ID\_NOT\_INIT: SPI id not init
        - others: other errors.

<a id="spi-api-typedefs"></a>

## SPI API Typedefs

<a id="id1"></a>

### Header File

- [spi\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/spi_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv416spi_int_config_t"></a>

<a id="_CPPv316spi_int_config_t"></a> <a id="_CPPv216spi_int_config_t"></a> <a id="spi_int_config_t"></a> <a id="structspi__int__config__t"></a> struct spi\_int\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16spi_int_config_t2idE"></a>

    <a id="_CPPv3N16spi_int_config_t2idE"></a> <a id="_CPPv2N16spi_int_config_t2idE"></a> <a id="spi_int_config_t::id__spi_id_t"></a> <a id="structspi__int__config__t_1a458a0fc19ac160765e12211430e6cff4"></a> [spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id
    :   SPI id

    <a id="_CPPv4N16spi_int_config_t7int_srcE"></a>

    <a id="_CPPv3N16spi_int_config_t7int_srcE"></a> <a id="_CPPv2N16spi_int_config_t7int_srcE"></a> <a id="spi_int_config_t::int_src__icu_int_src_t"></a> <a id="structspi__int__config__t_1af5cd1fd17607ee1994c6f9a7f546b202"></a> icu\_int\_src\_t int\_src
    :   int source

    <a id="_CPPv4N16spi_int_config_t3isrE"></a>

    <a id="_CPPv3N16spi_int_config_t3isrE"></a> <a id="_CPPv2N16spi_int_config_t3isrE"></a> <a id="spi_int_config_t::isr__int_group_isr_t"></a> <a id="structspi__int__config__t_1a0b2f498796b9421290626b3ab7f0e484"></a> int\_group\_isr\_t isr
    :   isr function

    <a id="_CPPv4N16spi_int_config_t7dma_devE"></a>

    <a id="_CPPv3N16spi_int_config_t7dma_devE"></a> <a id="_CPPv2N16spi_int_config_t7dma_devE"></a> <a id="spi_int_config_t::dma_dev__dma_dev_t"></a> <a id="structspi__int__config__t_1ac8676eaeab41989a74021a08d1770914"></a> [dma\_dev\_t](bk_dma.md#_CPPv49dma_dev_t "dma_dev_t") dma\_dev
    :   dma device

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv49spi_isr_t"></a>

<a id="_CPPv39spi_isr_t"></a> <a id="_CPPv29spi_isr_t"></a> <a id="spi_isr_t"></a> <a id="spi__types_8h_1a84722bffdb26e610d877276d939c7445"></a> typedef void (\*spi\_isr\_t)([spi\_id\_t](#_CPPv48spi_id_t "spi_id_t") id, void \*param)
:   SPI interrupt service routine

<a id="id2"></a>

### Header File

- [hal\_spi\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_spi_types.h)

<a id="id3"></a>

### Structures

<a id="_CPPv412spi_config_t"></a>

<a id="_CPPv312spi_config_t"></a> <a id="_CPPv212spi_config_t"></a> <a id="spi_config_t"></a> <a id="structspi__config__t"></a> struct spi\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12spi_config_t4roleE"></a>

    <a id="_CPPv3N12spi_config_t4roleE"></a> <a id="_CPPv2N12spi_config_t4roleE"></a> <a id="spi_config_t::role__spi_role_t"></a> <a id="structspi__config__t_1ab17d6132e5c2d6397c047b5df4ad1b5a"></a> [spi\_role\_t](#_CPPv410spi_role_t "spi_role_t") role
    :   SPI as master or slave

    <a id="_CPPv4N12spi_config_t9bit_widthE"></a>

    <a id="_CPPv3N12spi_config_t9bit_widthE"></a> <a id="_CPPv2N12spi_config_t9bit_widthE"></a> <a id="spi_config_t::bit_width__spi_bit_width_t"></a> <a id="structspi__config__t_1ad4f0da0e51d42849f8bb3bfe084e5974"></a> [spi\_bit\_width\_t](#_CPPv415spi_bit_width_t "spi_bit_width_t") bit\_width
    :   SPI data bit witdth

    <a id="_CPPv4N12spi_config_t8polarityE"></a>

    <a id="_CPPv3N12spi_config_t8polarityE"></a> <a id="_CPPv2N12spi_config_t8polarityE"></a> <a id="spi_config_t::polarity__spi_polarity_t"></a> <a id="structspi__config__t_1a7784d2c35bebaebbe69abd934c132aff"></a> [spi\_polarity\_t](#_CPPv414spi_polarity_t "spi_polarity_t") polarity
    :   SPI clock polarity

    <a id="_CPPv4N12spi_config_t5phaseE"></a>

    <a id="_CPPv3N12spi_config_t5phaseE"></a> <a id="_CPPv2N12spi_config_t5phaseE"></a> <a id="spi_config_t::phase__spi_phase_t"></a> <a id="structspi__config__t_1a64f71c737b7dd7e8a09c26bef1007d8a"></a> [spi\_phase\_t](#_CPPv411spi_phase_t "spi_phase_t") phase
    :   SPI clock phase

    <a id="_CPPv4N12spi_config_t9wire_modeE"></a>

    <a id="_CPPv3N12spi_config_t9wire_modeE"></a> <a id="_CPPv2N12spi_config_t9wire_modeE"></a> <a id="spi_config_t::wire_mode__spi_wire_mode_t"></a> <a id="structspi__config__t_1a78731212ddc1f57aaf1a24e30676c736"></a> [spi\_wire\_mode\_t](#_CPPv415spi_wire_mode_t "spi_wire_mode_t") wire\_mode
    :   SPI wire mode

    <a id="_CPPv4N12spi_config_t9baud_rateE"></a>

    <a id="_CPPv3N12spi_config_t9baud_rateE"></a> <a id="_CPPv2N12spi_config_t9baud_rateE"></a> <a id="spi_config_t::baud_rate__uint32_t"></a> <a id="structspi__config__t_1a3e13ccc08ecf811ba2471f5eb3cc7baa"></a> uint32\_t baud\_rate
    :   SPI transmit and receive SCK clock

    <a id="_CPPv4N12spi_config_t9bit_orderE"></a>

    <a id="_CPPv3N12spi_config_t9bit_orderE"></a> <a id="_CPPv2N12spi_config_t9bit_orderE"></a> <a id="spi_config_t::bit_order__spi_bit_order_t"></a> <a id="structspi__config__t_1a4f468aeffd3bbbcab1e5a71e3c1d70e8"></a> [spi\_bit\_order\_t](#_CPPv415spi_bit_order_t "spi_bit_order_t") bit\_order
    :   SPI bit order, MSB/LSB

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_SPI_NOT_INIT"></a>

<a id="hal__spi__types_8h_1a6bd8c56e1ae88cbe9c47f1130a4bdaf9"></a> BK\_ERR\_SPI\_NOT\_INIT
:   SPI driver not init

<a id="c.BK_ERR_SPI_INVALID_ID"></a>

<a id="hal__spi__types_8h_1a6ef61f7feaa6e2a8cf57ca5b8e3f2e31"></a> BK\_ERR\_SPI\_INVALID\_ID
:   SPI id number is invalid

<a id="c.BK_ERR_SPI_ID_NOT_INIT"></a>

<a id="hal__spi__types_8h_1a7d0d35d82ab9ee558e26bc0516acc767"></a> BK\_ERR\_SPI\_ID\_NOT\_INIT
:   SPI ID not init

<a id="c.BK_ERR_SPI_RX_TIMEOUT"></a>

<a id="hal__spi__types_8h_1ae4f98544f91a26c4129a01f00808e5d1"></a> BK\_ERR\_SPI\_RX\_TIMEOUT
:   SPI receive data timeout

<a id="c.BK_ERR_SPI_TX_TIMEOUT"></a>

<a id="hal__spi__types_8h_1adb1eaae6c7a53ec4f19153a4c3232f73"></a> BK\_ERR\_SPI\_TX\_TIMEOUT
:   SPI send data timeout

<a id="c.BK_ERR_SPI_FIFO_WR_NOT_READY"></a>

<a id="hal__spi__types_8h_1ac89bc76196dd24abd664335595547ee6"></a> BK\_ERR\_SPI\_FIFO\_WR\_NOT\_READY
:   SPI tx fifo write not ready

<a id="c.BK_ERR_SPI_FIFO_RD_NOT_READY"></a>

<a id="hal__spi__types_8h_1abf570710c0e4005f5155308f55b02bc3"></a> BK\_ERR\_SPI\_FIFO\_RD\_NOT\_READY
:   SPI rx fifo read not ready

<a id="c.BK_ERR_SPI_DUPLEX_SIZE_NOT_EQUAL"></a>

<a id="hal__spi__types_8h_1a0e48f989594cbe68e89c87983db2b190"></a> BK\_ERR\_SPI\_DUPLEX\_SIZE\_NOT\_EQUAL
:   SPI duplex tx rx size not equal

<a id="id4"></a>

### Type Definitions

<a id="_CPPv410spi_unit_t"></a>

<a id="_CPPv310spi_unit_t"></a> <a id="_CPPv210spi_unit_t"></a> <a id="spi_unit_t"></a> <a id="hal__spi__types_8h_1afd978c45b793d1b3efd624b7bca28b62"></a> typedef uint8\_t spi\_unit\_t
:   spi uint id

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv48spi_id_t"></a>

<a id="_CPPv38spi_id_t"></a> <a id="_CPPv28spi_id_t"></a> <a id="hal__spi__types_8h_1a1e48d9e4c4dd025d1cf4448227410237"></a> enum spi\_id\_t
:   *Values:*

    <a id="_CPPv4N8spi_id_t8SPI_ID_0E"></a>

    <a id="_CPPv3N8spi_id_t8SPI_ID_0E"></a> <a id="_CPPv2N8spi_id_t8SPI_ID_0E"></a> <a id="hal__spi__types_8h_1a1e48d9e4c4dd025d1cf4448227410237a682de5adb4e7035be8d5049ddc83a050"></a> enumerator SPI\_ID\_0
    :   SPI id 1

    <a id="_CPPv4N8spi_id_t10SPI_ID_MAXE"></a>

    <a id="_CPPv3N8spi_id_t10SPI_ID_MAXE"></a> <a id="_CPPv2N8spi_id_t10SPI_ID_MAXE"></a> <a id="hal__spi__types_8h_1a1e48d9e4c4dd025d1cf4448227410237afebf52f10dbbe467ffad98700434f5a9"></a> enumerator SPI\_ID\_MAX
    :   SPI id max

<a id="_CPPv410spi_role_t"></a>

<a id="_CPPv310spi_role_t"></a> <a id="_CPPv210spi_role_t"></a> <a id="hal__spi__types_8h_1a8ca86a080ece72454562cf2caa8ce479"></a> enum spi\_role\_t
:   *Values:*

    <a id="_CPPv4N10spi_role_t14SPI_ROLE_SLAVEE"></a>

    <a id="_CPPv3N10spi_role_t14SPI_ROLE_SLAVEE"></a> <a id="_CPPv2N10spi_role_t14SPI_ROLE_SLAVEE"></a> <a id="hal__spi__types_8h_1a8ca86a080ece72454562cf2caa8ce479a09c1f921b6707d02a9bd1e41817767a5"></a> enumerator SPI\_ROLE\_SLAVE
    :   SPI as slave

    <a id="_CPPv4N10spi_role_t15SPI_ROLE_MASTERE"></a>

    <a id="_CPPv3N10spi_role_t15SPI_ROLE_MASTERE"></a> <a id="_CPPv2N10spi_role_t15SPI_ROLE_MASTERE"></a> <a id="hal__spi__types_8h_1a8ca86a080ece72454562cf2caa8ce479a1f8bc6aa1f8e48dca00f24d45a7a2977"></a> enumerator SPI\_ROLE\_MASTER
    :   SPI as master

<a id="_CPPv415spi_bit_width_t"></a>

<a id="_CPPv315spi_bit_width_t"></a> <a id="_CPPv215spi_bit_width_t"></a> <a id="hal__spi__types_8h_1a6ba4a8eef274a5b227fc2ab6ee61f8fd"></a> enum spi\_bit\_width\_t
:   *Values:*

    <a id="_CPPv4N15spi_bit_width_t19SPI_BIT_WIDTH_8BITSE"></a>

    <a id="_CPPv3N15spi_bit_width_t19SPI_BIT_WIDTH_8BITSE"></a> <a id="_CPPv2N15spi_bit_width_t19SPI_BIT_WIDTH_8BITSE"></a> <a id="hal__spi__types_8h_1a6ba4a8eef274a5b227fc2ab6ee61f8fdac22a8f948ed5f02adbf53ee8a900dc17"></a> enumerator SPI\_BIT\_WIDTH\_8BITS
    :   SPI bit width 8bits

    <a id="_CPPv4N15spi_bit_width_t20SPI_BIT_WIDTH_16BITSE"></a>

    <a id="_CPPv3N15spi_bit_width_t20SPI_BIT_WIDTH_16BITSE"></a> <a id="_CPPv2N15spi_bit_width_t20SPI_BIT_WIDTH_16BITSE"></a> <a id="hal__spi__types_8h_1a6ba4a8eef274a5b227fc2ab6ee61f8fda9300dbbd48850f9d4d2d8345cff08626"></a> enumerator SPI\_BIT\_WIDTH\_16BITS
    :   SPI bit width 16bits

<a id="_CPPv414spi_polarity_t"></a>

<a id="_CPPv314spi_polarity_t"></a> <a id="_CPPv214spi_polarity_t"></a> <a id="hal__spi__types_8h_1a4b5160f7a5de37103d330f973a6cbb1d"></a> enum spi\_polarity\_t
:   *Values:*

    <a id="_CPPv4N14spi_polarity_t16SPI_POLARITY_LOWE"></a>

    <a id="_CPPv3N14spi_polarity_t16SPI_POLARITY_LOWE"></a> <a id="_CPPv2N14spi_polarity_t16SPI_POLARITY_LOWE"></a> <a id="hal__spi__types_8h_1a4b5160f7a5de37103d330f973a6cbb1da93259fc05082fc5a641ea2680fcb4e14"></a> enumerator SPI\_POLARITY\_LOW
    :   SPI clock polarity low

    <a id="_CPPv4N14spi_polarity_t17SPI_POLARITY_HIGHE"></a>

    <a id="_CPPv3N14spi_polarity_t17SPI_POLARITY_HIGHE"></a> <a id="_CPPv2N14spi_polarity_t17SPI_POLARITY_HIGHE"></a> <a id="hal__spi__types_8h_1a4b5160f7a5de37103d330f973a6cbb1da45314886358ce09bd4a9a92f90e992b5"></a> enumerator SPI\_POLARITY\_HIGH
    :   SPI clock polarity high

<a id="_CPPv411spi_phase_t"></a>

<a id="_CPPv311spi_phase_t"></a> <a id="_CPPv211spi_phase_t"></a> <a id="hal__spi__types_8h_1ad7236911b86b72663f2e0c3eba26c51f"></a> enum spi\_phase\_t
:   *Values:*

    <a id="_CPPv4N11spi_phase_t18SPI_PHASE_1ST_EDGEE"></a>

    <a id="_CPPv3N11spi_phase_t18SPI_PHASE_1ST_EDGEE"></a> <a id="_CPPv2N11spi_phase_t18SPI_PHASE_1ST_EDGEE"></a> <a id="hal__spi__types_8h_1ad7236911b86b72663f2e0c3eba26c51fa6a998f6ca65d253267f76862df2caad8"></a> enumerator SPI\_PHASE\_1ST\_EDGE
    :   SPI clock phase the first edge

    <a id="_CPPv4N11spi_phase_t18SPI_PHASE_2ND_EDGEE"></a>

    <a id="_CPPv3N11spi_phase_t18SPI_PHASE_2ND_EDGEE"></a> <a id="_CPPv2N11spi_phase_t18SPI_PHASE_2ND_EDGEE"></a> <a id="hal__spi__types_8h_1ad7236911b86b72663f2e0c3eba26c51fa518eaf6ae281baaf14e742009a5806f0"></a> enumerator SPI\_PHASE\_2ND\_EDGE
    :   SPI clock phase the second edge

<a id="_CPPv410spi_mode_t"></a>

<a id="_CPPv310spi_mode_t"></a> <a id="_CPPv210spi_mode_t"></a> <a id="hal__spi__types_8h_1ac4b206a51636d91c5cffcbcee458c3cb"></a> enum spi\_mode\_t
:   *Values:*

    <a id="_CPPv4N10spi_mode_t14SPI_POL_MODE_0E"></a>

    <a id="_CPPv3N10spi_mode_t14SPI_POL_MODE_0E"></a> <a id="_CPPv2N10spi_mode_t14SPI_POL_MODE_0E"></a> <a id="hal__spi__types_8h_1ac4b206a51636d91c5cffcbcee458c3cba1b3fd53d2cd84a110e693e93a7c13821"></a> enumerator SPI\_POL\_MODE\_0
    :   SPI mode 0

    <a id="_CPPv4N10spi_mode_t14SPI_POL_MODE_1E"></a>

    <a id="_CPPv3N10spi_mode_t14SPI_POL_MODE_1E"></a> <a id="_CPPv2N10spi_mode_t14SPI_POL_MODE_1E"></a> <a id="hal__spi__types_8h_1ac4b206a51636d91c5cffcbcee458c3cba0dda16d1e9914651ac35d9b1751d4d9f"></a> enumerator SPI\_POL\_MODE\_1
    :   SPI mode 1

    <a id="_CPPv4N10spi_mode_t14SPI_POL_MODE_2E"></a>

    <a id="_CPPv3N10spi_mode_t14SPI_POL_MODE_2E"></a> <a id="_CPPv2N10spi_mode_t14SPI_POL_MODE_2E"></a> <a id="hal__spi__types_8h_1ac4b206a51636d91c5cffcbcee458c3cbaa58356405a11c176f967204d3a7d5b25"></a> enumerator SPI\_POL\_MODE\_2
    :   SPI mode 2

    <a id="_CPPv4N10spi_mode_t14SPI_POL_MODE_3E"></a>

    <a id="_CPPv3N10spi_mode_t14SPI_POL_MODE_3E"></a> <a id="_CPPv2N10spi_mode_t14SPI_POL_MODE_3E"></a> <a id="hal__spi__types_8h_1ac4b206a51636d91c5cffcbcee458c3cba2a86c236cb98726b3f1295103d0dafc5"></a> enumerator SPI\_POL\_MODE\_3
    :   SPI mode 3

<a id="_CPPv415spi_wire_mode_t"></a>

<a id="_CPPv315spi_wire_mode_t"></a> <a id="_CPPv215spi_wire_mode_t"></a> <a id="hal__spi__types_8h_1ac1b09dab3e6dffc16cbb5243b737c8e1"></a> enum spi\_wire\_mode\_t
:   *Values:*

    <a id="_CPPv4N15spi_wire_mode_t14SPI_4WIRE_MODEE"></a>

    <a id="_CPPv3N15spi_wire_mode_t14SPI_4WIRE_MODEE"></a> <a id="_CPPv2N15spi_wire_mode_t14SPI_4WIRE_MODEE"></a> <a id="hal__spi__types_8h_1ac1b09dab3e6dffc16cbb5243b737c8e1a9b77a68d98cde0380fdad756c0538c6a"></a> enumerator SPI\_4WIRE\_MODE
    :   SPI four wire mode

    <a id="_CPPv4N15spi_wire_mode_t14SPI_3WIRE_MODEE"></a>

    <a id="_CPPv3N15spi_wire_mode_t14SPI_3WIRE_MODEE"></a> <a id="_CPPv2N15spi_wire_mode_t14SPI_3WIRE_MODEE"></a> <a id="hal__spi__types_8h_1ac1b09dab3e6dffc16cbb5243b737c8e1ab1f434fba6c742beb626fda478c69062"></a> enumerator SPI\_3WIRE\_MODE
    :   SPI three wire mode

<a id="_CPPv415spi_bit_order_t"></a>

<a id="_CPPv315spi_bit_order_t"></a> <a id="_CPPv215spi_bit_order_t"></a> <a id="hal__spi__types_8h_1a90f5b39d4872c0c09255af5dcea6cd3e"></a> enum spi\_bit\_order\_t
:   *Values:*

    <a id="_CPPv4N15spi_bit_order_t13SPI_MSB_FIRSTE"></a>

    <a id="_CPPv3N15spi_bit_order_t13SPI_MSB_FIRSTE"></a> <a id="_CPPv2N15spi_bit_order_t13SPI_MSB_FIRSTE"></a> <a id="hal__spi__types_8h_1a90f5b39d4872c0c09255af5dcea6cd3ea8912f763c0e7854e08dfbe61b7a57cc6"></a> enumerator SPI\_MSB\_FIRST
    :   SPI MSB first

    <a id="_CPPv4N15spi_bit_order_t13SPI_LSB_FIRSTE"></a>

    <a id="_CPPv3N15spi_bit_order_t13SPI_LSB_FIRSTE"></a> <a id="_CPPv2N15spi_bit_order_t13SPI_LSB_FIRSTE"></a> <a id="hal__spi__types_8h_1a90f5b39d4872c0c09255af5dcea6cd3ea5a6abe145caf9794d5a70e5472ee988f"></a> enumerator SPI\_LSB\_FIRST
    :   SPI LSB first

<a id="_CPPv418spi_fifo_int_level"></a>

<a id="_CPPv318spi_fifo_int_level"></a> <a id="_CPPv218spi_fifo_int_level"></a> <a id="hal__spi__types_8h_1aab00dc2f8bd12bcde6866023d1fb58f8"></a> enum spi\_fifo\_int\_level
:   *Values:*

    <a id="_CPPv4N18spi_fifo_int_level20SPI_FIFO_INT_LEVEL_1E"></a>

    <a id="_CPPv3N18spi_fifo_int_level20SPI_FIFO_INT_LEVEL_1E"></a> <a id="_CPPv2N18spi_fifo_int_level20SPI_FIFO_INT_LEVEL_1E"></a> <a id="hal__spi__types_8h_1aab00dc2f8bd12bcde6866023d1fb58f8adeac05478caff029c05921d03a7e9f68"></a> enumerator SPI\_FIFO\_INT\_LEVEL\_1
    :   SPI fifo int level 1

    <a id="_CPPv4N18spi_fifo_int_level21SPI_FIFO_INT_LEVEL_16E"></a>

    <a id="_CPPv3N18spi_fifo_int_level21SPI_FIFO_INT_LEVEL_16E"></a> <a id="_CPPv2N18spi_fifo_int_level21SPI_FIFO_INT_LEVEL_16E"></a> <a id="hal__spi__types_8h_1aab00dc2f8bd12bcde6866023d1fb58f8a4c08aecc69adf20951dee4a1368529fc"></a> enumerator SPI\_FIFO\_INT\_LEVEL\_16
    :   SPI fifo int level 16

    <a id="_CPPv4N18spi_fifo_int_level21SPI_FIFO_INT_LEVEL_32E"></a>

    <a id="_CPPv3N18spi_fifo_int_level21SPI_FIFO_INT_LEVEL_32E"></a> <a id="_CPPv2N18spi_fifo_int_level21SPI_FIFO_INT_LEVEL_32E"></a> <a id="hal__spi__types_8h_1aab00dc2f8bd12bcde6866023d1fb58f8aa49a8a652e103387140493442dc30374"></a> enumerator SPI\_FIFO\_INT\_LEVEL\_32
    :   SPI fifo int level 32

    <a id="_CPPv4N18spi_fifo_int_level21SPI_FIFO_INT_LEVEL_48E"></a>

    <a id="_CPPv3N18spi_fifo_int_level21SPI_FIFO_INT_LEVEL_48E"></a> <a id="_CPPv2N18spi_fifo_int_level21SPI_FIFO_INT_LEVEL_48E"></a> <a id="hal__spi__types_8h_1aab00dc2f8bd12bcde6866023d1fb58f8a096fa0beeeeca242f37246064f7a82d6"></a> enumerator SPI\_FIFO\_INT\_LEVEL\_48
    :   SPI fifo int level 48

<a id="_CPPv413spi_src_clk_t"></a>

<a id="_CPPv313spi_src_clk_t"></a> <a id="_CPPv213spi_src_clk_t"></a> <a id="hal__spi__types_8h_1a42807162f5dadf69c41df77f2829b088"></a> enum spi\_src\_clk\_t
:   *Values:*

    <a id="_CPPv4N13spi_src_clk_t12SPI_CLK_XTALE"></a>

    <a id="_CPPv3N13spi_src_clk_t12SPI_CLK_XTALE"></a> <a id="_CPPv2N13spi_src_clk_t12SPI_CLK_XTALE"></a> <a id="hal__spi__types_8h_1a42807162f5dadf69c41df77f2829b088a0622ad1364222b7b1019484730020f7f"></a> enumerator SPI\_CLK\_XTAL

    <a id="_CPPv4N13spi_src_clk_t12SPI_CLK_APLLE"></a>

    <a id="_CPPv3N13spi_src_clk_t12SPI_CLK_APLLE"></a> <a id="_CPPv2N13spi_src_clk_t12SPI_CLK_APLLE"></a> <a id="hal__spi__types_8h_1a42807162f5dadf69c41df77f2829b088a86f3749fcf684f076095271e5a6c9eb9"></a> enumerator SPI\_CLK\_APLL

    <a id="_CPPv4N13spi_src_clk_t13SPI_CLK_60MHZE"></a>

    <a id="_CPPv3N13spi_src_clk_t13SPI_CLK_60MHZE"></a> <a id="_CPPv2N13spi_src_clk_t13SPI_CLK_60MHZE"></a> <a id="hal__spi__types_8h_1a42807162f5dadf69c41df77f2829b088ac19a54fa51bcccd79bddbe697639fc1f"></a> enumerator SPI\_CLK\_60MHZ

    <a id="_CPPv4N13spi_src_clk_t13SPI_CLK_80MHZE"></a>

    <a id="_CPPv3N13spi_src_clk_t13SPI_CLK_80MHZE"></a> <a id="_CPPv2N13spi_src_clk_t13SPI_CLK_80MHZE"></a> <a id="hal__spi__types_8h_1a42807162f5dadf69c41df77f2829b088adac4a6a0fdd6f67a58f40963b65284a7"></a> enumerator SPI\_CLK\_80MHZ

    <a id="_CPPv4N13spi_src_clk_t14SPI_CLK_160MHZE"></a>

    <a id="_CPPv3N13spi_src_clk_t14SPI_CLK_160MHZE"></a> <a id="_CPPv2N13spi_src_clk_t14SPI_CLK_160MHZE"></a> <a id="hal__spi__types_8h_1a42807162f5dadf69c41df77f2829b088a2d4feeba623791b8fbb807836182939c"></a> enumerator SPI\_CLK\_160MHZ

    <a id="_CPPv4N13spi_src_clk_t14SPI_CLK_UNKNOWE"></a>

    <a id="_CPPv3N13spi_src_clk_t14SPI_CLK_UNKNOWE"></a> <a id="_CPPv2N13spi_src_clk_t14SPI_CLK_UNKNOWE"></a> <a id="hal__spi__types_8h_1a42807162f5dadf69c41df77f2829b088a0a4242cd413ea9eb41583f6d6cef277e"></a> enumerator SPI\_CLK\_UNKNOW
