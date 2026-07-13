# QSPI



## QSPI API Reference


### Header File


- [qspi.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/qspi.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/qspi.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_driver_init(void)
:   Init the QSPI driver.

    This API init the resoure common:


    - Init QSPI driver control memory


    **Attention**
    :   1. This API should be called before any other QSPI APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_driver_deinit(void)
:   Deinit the QSPI driver.

    This API free all resource related to QSPI and disable QSPI.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_init([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id, const [qspi_config_t](#_CPPv413qspi_config_t "qspi_config_t") *config)
:   Init the QSPI.

    This API init the QSPI:


    - Power up the QSPI

    - Configure the QSPI clock

    - Map the QSPI to dedicated GPIO port

    - Enabel QSPI interrupt

    参数
    :   **config** – QSPI parameter settings

    返回
    :   - BK_OK: succeed

        - BK_ERR_QSPI_NOT_INIT: QSPI driver not init

        - BK_ERR_NULL_PARAM: QSPI config parameter is NULL

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_init_by_freq([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32_t clk_hz)
:   Init the QSPI by target SCK frequency (convenience wrapper)

    This API picks the source clock and dividers whose resulting SCK is closest to clk_hz (SCK = src_clock / (1 + src_clk_div)), fills a [qspi_config_t](#structqspi__config__t "#structqspi__config__t") and then calls bk_qspi_init(). The application only needs to provide the QSPI id and the desired clock in Hz, without caring about the source clock selection or divider details.

    参数
    :   - **id** – QSPI id

        - **clk_hz** – target SCK frequency in Hz (max 80000000)

    返回
    :   - BK_OK: succeed

        - BK_ERR_QSPI_NOT_INIT: QSPI driver not init

        - others: forwarded from bk_qspi_init

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_deinit([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   Deinit the QSPI.

    This API deinit the QSPI:


    - Disable the QSPI interrupt

    - Power down the QSPI

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_command([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id, const [qspi_cmd_t](#_CPPv410qspi_cmd_t "qspi_cmd_t") *cmd)
:   Init the QSPI command.

    参数
    :   **cmd** – QSPI device command

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_write([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id, const void *data, uint32_t size)
:   QSPI indirect mode write.

    参数
    :   - **base_addr** – QSPI write address

        - **data** – QSPI write data

        - **size** – the size of QSPI write data

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_read([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id, void *data, uint32_t size)
:   QSPI indirect mode read.

    参数
    :   - **base_addr** – QSPI read address

        - **data** – QSPI read data

        - **size** – the size of QSPI read data

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_register_tx_isr([qspi_isr_t](#_CPPv410qspi_isr_t "qspi_isr_t") isr, void *param)
:   Register the TX interrupt service routine for QSPI.

    参数
    :   - **isr** – QSPI TX callback

        - **param** – QSPI TX callback parameter

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_register_rx_isr([qspi_isr_t](#_CPPv410qspi_isr_t "qspi_isr_t") isr, void *param)
:   Register the RX interrupt service routine for QSPI.

    参数
    :   - **isr** – QSPI RX callback

        - **param** – QSPI RX callback parameter

    返回
    :   - BK_OK: succeed

        - others: other errors.


## QSPI PSRAM API Reference


### Header File


- [qspi_psram.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/qspi_psram.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/qspi_psram.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_init([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   Init the QSPI psram.

    返回
    :   - BK_OK: succeed

        - BK_ERR_QSPI_NOT_INIT: QSPI driver not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_deinit([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   Deinit the QSPI psram.

    返回
    :   - BK_OK: succeed

        - BK_ERR_QSPI_NOT_INIT: QSPI driver not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_enter_quad_mode([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram enter quad mode.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_exit_quad_mode([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram exit quad mode.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_quad_write([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram init quad write.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_single_write([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram init single write.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_quad_read([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram init quad read.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_single_read([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram init single read.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_write([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32_t base_addr, const void *data, uint32_t size)
:   QSPI psram write data.

    参数
    :   - **base_addr** – QSPI write address

        - **data** – QSPI write data

        - **size** – the size of QSPI write data

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_qspi_psram_read([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32_t base_addr, void *data, uint32_t size)
:   QSPI psram read data.

    参数
    :   - **base_addr** – QSPI read address

        - **data** – QSPI read data

        - **size** – the size of QSPI read data

    返回
    :   - BK_OK: succeed

        - others: other errors.


## QSPI API Typedefs


### Header File


- [qspi_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/qspi_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/qspi_types.h")


### Structures

struct qspi_driver_t

struct qspi_callback_t


### Type Definitions

typedef void (*qspi_isr_t)([qspi_id_t](#_CPPv49qspi_id_t "qspi_id_t") id, void *param)
:   QSPI interrupt service routine.


### Header File


- [hal/hal_qspi_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_qspi_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_qspi_types.h")


### Structures

struct qspi_config_t

struct qspi_cmd_t


### Macros

BK_ERR_QSPI_NOT_INIT
:   QSPI driver not init

BK_ERR_QSPI_ID_NOT_INIT
:   QSPI id not init

QSPI_FIFO_LEN_MAX


### Type Definitions

typedef uint8_t qspi_unit_t
:   QSPI uint id


### Enumerations

enum qspi_id_t
:   *Values:*

    enumerator QSPI_ID_0
    :   QSPI id 1

    enumerator QSPI_ID_MAX
    :   QSPI id max

enum qspi_op_t
:   *Values:*

    enumerator QSPI_READ
    :   QSPI read operation

    enumerator QSPI_WRITE
    :   QSPI write operation

enum qspi_src_clk_t
:   *Values:*

    enumerator QSPI_SCLK_160M
    :   QSPI source clock 160M

    enumerator QSPI_SCLK_240M
    :   QSPI source clock 240M

enum qspi_work_mode
:   *Values:*

    enumerator MEMORY_MAPPED_MODE

    enumerator INDIRECT_MODE

enum qspi_wire_mode_t
:   *Values:*

    enumerator QSPI_1WIRE
    :   QSPI 1_wire mode, standard SPI

    enumerator QSPI_2WIRE
    :   QSPI 2_wire mode, DUAL SPI

    enumerator QSPI_4WIRE
    :   QSPI 4_wire mode, QUAD SPI

    enumerator QSPI_CMD_DISABLE
    :   QSPI command disable flag

enum qspi_device_t
:   *Values:*

    enumerator QSPI_PSRAM
    :   QSPI PSRAM

    enumerator QSPI_FLASH
    :   QSPI FLASH

    enumerator QSPI_OLED
    :   QSPI OLED
