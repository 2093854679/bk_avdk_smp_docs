# SPI



## SPI API Status

| API | BK7259_AP |
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
| [`bk_spi_register_rx_isr()`](#_CPPv422bk_spi_register_rx_isr8spi_id_t9spi_isr_tPv "bk_spi_register_rx_isr") | Y |
| [`bk_spi_register_tx_finish_isr()`](#_CPPv429bk_spi_register_tx_finish_isr8spi_id_t9spi_isr_tPv "bk_spi_register_tx_finish_isr") | Y |
| [`bk_spi_write_bytes()`](#_CPPv418bk_spi_write_bytes8spi_id_tPKv8uint32_t "bk_spi_write_bytes") | Y |
| [`bk_spi_read_bytes()`](#_CPPv417bk_spi_read_bytes8spi_id_tPv8uint32_t "bk_spi_read_bytes") | Y |
| [`bk_spi_transmit()`](#_CPPv415bk_spi_transmit8spi_id_tPKv8uint32_tPv8uint32_t "bk_spi_transmit") | Y |
| `bk_spi_dma_write_bytes()` | Y |
| `bk_spi_dma_read_bytes()` | Y |
| `bk_spi_dma_transmit()` | Y |


## SPI UNIT Number

| Capability | BK7259_AP |
| --- | --- |
| UNIT Number | 3 |


## SPI Pin and GPIO Map

| SPI Pin | BK7259_AP |
| --- | --- |
| SPI0 SCK | 44 |
| SPI0 CSN | 45 |
| SPI0 MOSI | 46 |
| SPI0 MISO | 47 |
| SPI1 SCK | 2 |
| SPI1 CSN | 3 |
| SPI1 MOSI | 4 |
| SPI1 MISO | 5 |
| SPI2 SCK | 14 |
| SPI2 CSN | 15 |
| SPI2 MOSI | 16 |
| SPI2 MISO | 17 |


## SPI API Reference


### Header File


- [spi.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/spi.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/spi.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_driver_init(void)
:   Init the SPI driver.

    This API init the resoure common:


    - Init SPI driver control memory


    **Attention**
    :   1. This API should be called before any other SPI APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_driver_deinit(void)
:   Deinit the SPI driver.

    This API free all resource related to SPI and disable SPI.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_init([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, const [spi_config_t](#_CPPv412spi_config_t "spi_config_t") *config)
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
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: SPI config paramter is NULL

        - BK_ERR_SPI_NOT_INIT: SPI driver not init

        - BK_ERR_SPI_INVALID_ID: SPI id is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_deinit([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id)
:   Deinit the SPI id.

    This API deinit the SPI id:


    - Stop the SPI id

    - Disable the SPI id interrupt

    - Power down the SPI id

    参数
    :   **id** – SPI id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_set_mode([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, [spi_mode_t](#_CPPv410spi_mode_t "spi_mode_t") mode)
:   Set the SPI mode.

    参数
    :   - **id** – SPI id

        - **mode** – SPI mode

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_set_bit_width([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, [spi_bit_width_t](#_CPPv415spi_bit_width_t "spi_bit_width_t") bit_width)
:   Set the SPI bit width.

    参数
    :   - **id** – SPI id

        - **bit_width** – SPI bit width

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_set_wire_mode([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, [spi_wire_mode_t](#_CPPv415spi_wire_mode_t "spi_wire_mode_t") wire_mode)
:   Set the SPI wire mode.

    参数
    :   - **id** – SPI id

        - **wire_mode** – SPI wire mode

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_set_baud_rate([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, uint32_t baud_rate)
:   Set the SPI baud rate.

    参数
    :   - **id** – SPI id

        - **baud_rate** – SPI baud rate

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_set_bit_order([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, [spi_bit_order_t](#_CPPv415spi_bit_order_t "spi_bit_order_t") bit_order)
:   Set the SPI bit order.

    参数
    :   - **id** – SPI id

        - **bit_order** – SPI bit order

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_set_role([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, [spi_role_t](#_CPPv410spi_role_t "spi_role_t") role)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_clear_tx_fifo([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_clear_rx_fifo([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_clr_tx([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_clr_rx([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_register_rx_isr([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, [spi_isr_t](#_CPPv49spi_isr_t "spi_isr_t") isr, void *param)
:   Register the RX interrupt service routine for SPI id.

    参数
    :   - **id** – spi id

        - **isr** – SPI RX callback

        - **param** – SPI RX callback parameter

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_register_tx_finish_isr([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, [spi_isr_t](#_CPPv49spi_isr_t "spi_isr_t") isr, void *param)
:   Register the TX finish interrupt service routine for SPI id.

    参数
    :   - **id** – SPi id

        - **isr** – SPI TX finish callback

        - **param** – SPi TX callback parameter

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_write_bytes([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, const void *data, uint32_t size)
:   Send data to the SPI port from a given buffer and length.

    参数
    :   - **id** – spi id

        - **data** – data buffer address

        - **size** – data length to send

    返回
    :   - BK_OK: succeed

        - BK_ERR_SPI_NOT_INIT: SPI driver not init

        - BK_ERR_SPI_INVALID_ID: SPI id number is invalid

        - BK_ERR_SPI_ID_NOT_INIT: SPI id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_read_bytes([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, void *data, uint32_t size)
:   SPI read bytes from SPI buffer.

    参数
    :   - **id** – SPI id

        - **data** – pointer to the buffer

        - **size** – data length to read

    返回
    :   - BK_OK: succeed

        - BK_ERR_SPI_NOT_INIT: SPI driver not init

        - BK_ERR_SPI_INVALID_ID: SPI id number is invalid

        - BK_ERR_SPI_ID_NOT_INIT: SPI id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_transmit([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, const void *tx_data, uint32_t tx_size, void *rx_data, uint32_t rx_size)
:   SPI write and read bytes.

    参数
    :   - **id** – SPI id

        - **tx_data** – write data buffer address

        - **tx_size** – data length to read

        - **rx_data** – pointer to the receive buffer

        - **rx_size** – data length to read

        - **timeout_ms** – timeout ms, if set BEKEN_WAIT_FOREVER, read will wait forever

    返回
    :   - BK_OK: succeed

        - BK_ERR_SPI_NOT_INIT: SPI driver not init

        - BK_ERR_SPI_INVALID_ID: SPI id number is invalid

        - BK_ERR_SPI_ID_NOT_INIT: SPI id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_register_rx_finish_isr([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, [spi_isr_t](#_CPPv49spi_isr_t "spi_isr_t") isr, void *param)
:   Register the RX finish interrupt service routine for SPI id.

    参数
    :   - **id** – spi id

        - **isr** – SPI RX callback

        - **param** – SPI RX callback parameter

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_unregister_rx_isr([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id)
:   Unregister the RX interrupt service routine for SPI id.

    参数
    :   **id** – spi id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_unregister_rx_finish_isr([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id)
:   Unregister the RX finish interrupt service routine for SPI id.

    参数
    :   **id** – spi id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_unregister_tx_finish_isr([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id)
:   Unregister the TX finish interrupt service routine for SPI id.

    参数
    :   **id** – spi id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_write_bytes_async([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, const void *data, uint32_t size)
:   Send data to the SPI port from a given buffer and length in async mode.

    参数
    :   - **id** – spi id

        - **data** – data buffer address

        - **size** – data length to send

    返回
    :   - BK_OK: succeed

        - BK_ERR_SPI_NOT_INIT: SPI driver not init

        - BK_ERR_SPI_INVALID_ID: SPI id number is invalid

        - BK_ERR_SPI_ID_NOT_INIT: SPI id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spi_read_bytes_async([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, void *data, uint32_t size)
:   SPI read bytes from SPI buffer in async mode.

    参数
    :   - **id** – SPI id

        - **data** – pointer to the buffer

        - **size** – data length to read

    返回
    :   - BK_OK: succeed

        - BK_ERR_SPI_NOT_INIT: SPI driver not init

        - BK_ERR_SPI_INVALID_ID: SPI id number is invalid

        - BK_ERR_SPI_ID_NOT_INIT: SPI id not init

        - others: other errors.


## SPI API Typedefs


### Header File


- [spi_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/spi_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/spi_types.h")


### Structures

struct spi_int_config_t
:   Public Members

    [spi_id_t](#_CPPv48spi_id_t "spi_id_t") id
    :   SPI id

    icu_int_src_t int_src
    :   int source

    int_group_isr_t isr
    :   isr function

    [dma_dev_t](bk_dma.md#_CPPv49dma_dev_t "dma_dev_t") dma_dev
    :   dma device


### Type Definitions

typedef void (*spi_isr_t)([spi_id_t](#_CPPv48spi_id_t "spi_id_t") id, void *param)
:   SPI interrupt service routine


### Header File


- [hal/hal_spi_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_spi_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_spi_types.h")


### Structures

struct spi_config_t


### Macros

BK_ERR_SPI_NOT_INIT
:   SPI driver not init

BK_ERR_SPI_INVALID_ID
:   SPI id number is invalid

BK_ERR_SPI_ID_NOT_INIT
:   SPI ID not init

BK_ERR_SPI_RX_TIMEOUT
:   SPI receive data timeout

BK_ERR_SPI_TX_TIMEOUT
:   SPI send data timeout

BK_ERR_SPI_FIFO_WR_NOT_READY
:   SPI tx fifo write not ready

BK_ERR_SPI_FIFO_RD_NOT_READY
:   SPI rx fifo read not ready

BK_ERR_SPI_DUPLEX_SIZE_NOT_EQUAL
:   SPI duplex tx rx size not equal


### Type Definitions

typedef uint8_t spi_unit_t
:   spi uint id


### Enumerations

enum spi_id_t
:   *Values:*

    enumerator SPI_ID_0
    :   SPI id 1

    enumerator SPI_ID_MAX
    :   SPI id max

enum spi_role_t
:   *Values:*

    enumerator SPI_ROLE_SLAVE
    :   SPI as slave

    enumerator SPI_ROLE_MASTER
    :   SPI as master

enum spi_bit_width_t
:   *Values:*

    enumerator SPI_BIT_WIDTH_8BITS
    :   SPI bit width 8bits

    enumerator SPI_BIT_WIDTH_16BITS
    :   SPI bit width 16bits

enum spi_polarity_t
:   *Values:*

    enumerator SPI_POLARITY_LOW
    :   SPI clock polarity low

    enumerator SPI_POLARITY_HIGH
    :   SPI clock polarity high

enum spi_phase_t
:   *Values:*

    enumerator SPI_PHASE_1ST_EDGE
    :   SPI clock phase the first edge

    enumerator SPI_PHASE_2ND_EDGE
    :   SPI clock phase the second edge

enum spi_mode_t
:   *Values:*

    enumerator SPI_POL_MODE_0
    :   SPI mode 0

    enumerator SPI_POL_MODE_1
    :   SPI mode 1

    enumerator SPI_POL_MODE_2
    :   SPI mode 2

    enumerator SPI_POL_MODE_3
    :   SPI mode 3

enum spi_wire_mode_t
:   *Values:*

    enumerator SPI_4WIRE_MODE
    :   SPI four wire mode

    enumerator SPI_3WIRE_MODE
    :   SPI three wire mode

enum spi_bit_order_t
:   *Values:*

    enumerator SPI_MSB_FIRST
    :   SPI MSB first

    enumerator SPI_LSB_FIRST
    :   SPI LSB first

enum spi_fifo_int_level
:   *Values:*

    enumerator SPI_FIFO_INT_LEVEL_1
    :   SPI fifo int level 1

    enumerator SPI_FIFO_INT_LEVEL_16
    :   SPI fifo int level 16

    enumerator SPI_FIFO_INT_LEVEL_32
    :   SPI fifo int level 32

    enumerator SPI_FIFO_INT_LEVEL_48
    :   SPI fifo int level 48

enum spi_src_clk_t
:   *Values:*

    enumerator SPI_CLK_XTAL

    enumerator SPI_CLK_APLL

    enumerator SPI_CLK_60MHZ

    enumerator SPI_CLK_80MHZ

    enumerator SPI_CLK_160MHZ

    enumerator SPI_CLK_UNKNOW
