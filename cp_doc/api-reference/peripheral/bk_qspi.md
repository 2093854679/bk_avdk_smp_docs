---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# QSPI


BK7259 CP 侧 QSPI API（`include/driver/qspi.h`）。


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
:   Public Members

    [qspi_src_clk_t](#_CPPv414qspi_src_clk_t "qspi_src_clk_t") src_clk
    :   QSPI source clock

    uint32_t src_clk_div
    :   QSPI source clock divide number

    uint32_t clk_div
    :   QSPI controller clock divide number

struct qspi_cmd_t
:   Public Members

    [qspi_work_mode](#_CPPv414qspi_work_mode "qspi_work_mode") work_mode
    :   QSPI work mode

    [qspi_op_t](#_CPPv49qspi_op_t "qspi_op_t") op
    :   QSPI operation

    uint32_t cmd
    :   QSPI command

    uint32_t addr
    :   QSPI address

    uint32_t addr_len
    :   QSPI address length

    [qspi_wire_mode_t](#_CPPv416qspi_wire_mode_t "qspi_wire_mode_t") addr_wire_mode
    :   QSPI address wire mode

    uint32_t dummy_cycle
    :   QSPI dummy cycle

    uint32_t dummy_mode
    :   QSPI dummy mode, means the offset to insert dummy clock

    uint32_t data_len
    :   QSPI data length

    [qspi_wire_mode_t](#_CPPv416qspi_wire_mode_t "qspi_wire_mode_t") data_wire_mode
    :   QSPI data wire mode

    [qspi_device_t](#_CPPv413qspi_device_t "qspi_device_t") device
    :   QSPI slave device


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

    enumerator QSPI_SCLK_320M
    :   QSPI source clock 320M

    enumerator QSPI_SCLK_480M
    :   QSPI source clock 480M

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
