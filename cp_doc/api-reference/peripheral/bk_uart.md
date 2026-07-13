# UART



## UART API Status

| API | BK7259_CP |
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


## UART Port Number

| Capability | BK7259_CP |
| --- | --- |
| Port Number | 3 |


## UART Pin and GPIO Map

| UART Pin | BK7259_CP |
| --- | --- |
| UART0 TX | 11 |
| UART0 RX | 10 |
| UART1 TX | 0 |
| UART1 RX | 1 |
| UART2 TX | 41 |
| UART2 RX | 40 |


## UART API Reference


### Header File


- [uart.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/uart.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/uart.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_driver_init(void)
:   Init the UART driver.

    This API init the resoure common to all UART id:


    - Init UART driver control memory


    **Attention**
    :   1. This API should be called before any other UART APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_driver_deinit(void)
:   Deinit the UART driver.

    This API free all resource related to UART and power down all UART id.

    返回
    :   - BK_OK: succeed

        - others: other errors.

int bk_uart_is_in_used([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Get the UART whether in used.

    参数
    :   **id** – UART id

    返回
    :   - 1: in used

        - 0: not in used

int bk_uart_is_rx_dma_enabled([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Get the UART whether rx dma is enabled.

    参数
    :   **id** – UART id

    返回
    :   - 1: rx dma is enabled

        - 0: rx dma is disabled

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_init([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, const [uart_config_t](#_CPPv413uart_config_t "uart_config_t") *config)
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
    :   - BK_OK: succeed

        - BK_ERR_UART_NOT_INIT: UART driver not init

        - BK_ERR_NULL_PARAM: UART config parameter is NULL

        - BK_ERR_UART_INVALID_ID: UART id is invalid

        - BK_ERR_UART_BAUD_RATE_NOT_SUPPORT: UART baud rate is not support

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_deinit([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Deinit the UART id.

    This API deinit the UART id:


    - Stop the UART id

    - Reset all configuration of UART id to default value

    - Disable the UART id interrupt

    - Power down the UART id

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_baud_rate([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, uint32_t baud_rate)
:   Set the UART baud rate.

    参数
    :   - **id** – UART id

        - **baud_rate** – UART baud rate

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_data_bits([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, [uart_data_bits_t](#_CPPv416uart_data_bits_t "uart_data_bits_t") data_bits)
:   Set the UART data bits.

    参数
    :   - **id** – UART id

        - **data_bits** – UART data bits

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_stop_bits([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, [uart_stop_bits_t](#_CPPv416uart_stop_bits_t "uart_stop_bits_t") stop_bits)
:   Set the UART stop bits.

    参数
    :   - **id** – UART id

        - **stop_bits** – UART stop bits

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_parity([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, [uart_parity_t](#_CPPv413uart_parity_t "uart_parity_t") partiy)
:   Set the UART partiy.

    参数
    :   - **id** – UART id

        - **partiy** – UART partiy

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_hw_flow_ctrl([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, uint8_t rx_threshold)
:   Set the UART hardware flow control.

    参数
    :   - **id** – UART id

        - **rx_threshold** – Threshold of Hardware RX flow control

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_rx_full_threshold([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, uint8_t threshold)
:   Set the UART threshold value for RX fifo full.

    参数
    :   - **id** – UART id

        - **threshold** – Threshold value above which RX fifo full interrupt is generated

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_tx_empty_threshold([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, uint8_t threshold)
:   Set the UART threshold value for TX fifo empty.

    参数
    :   - **id** – UART id

        - **threshold** – Threshold value below which TX fifo empty interrupt is generated

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_rx_timeout([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, [uart_rx_stop_detect_time_t](#_CPPv426uart_rx_stop_detect_time_t "uart_rx_stop_detect_time_t") timeout_thresh)
:   Set the UART threshold timeout for receive data, unit is bit.

    UART finish receiving data when the periods is more than timeout threshold. If the time is expired, the UART_RX_STOP_END interrupt is triggered.

    参数
    :   - **id** – UART id

        - **timeout_thresh** – timeout threshold

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_disable_hw_flow_ctrl([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable the UART hardware flow control.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_enable_tx_interrupt([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Enable TX interrupt of UART id.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_disable_tx_interrupt([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable TX interrupt of UART id.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_enable_rx_interrupt([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Enable RX interrupt of UART id.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_disable_rx_interrupt([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable RX interrupt of UART id.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_register_rx_isr([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, [uart_isr_t](#_CPPv410uart_isr_t "uart_isr_t") isr, void *param)
:   Register the RX interrupt service routine for UART id.

    参数
    :   - **id** – UART id

        - **isr** – UART RX callback

        - **param** – UART RX callback parameter

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_register_tx_isr([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, [uart_isr_t](#_CPPv410uart_isr_t "uart_isr_t") isr, void *param)
:   Register the TX interrupt service routine for UART id.

    参数
    :   - **id** – UART id

        - **isr** – UART TX callback

        - **param** – UART TX callback parameter

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_write_bytes([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, const void *data, uint32_t size)
:   Send data to the UART port from a given buffer and length.

    参数
    :   - **id** – UART id

        - **data** – data buffer address

        - **size** – data length to send

    返回
    :   - BK_OK: succeed

        - others: other errors.

int bk_uart_read_bytes([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, void *data, uint32_t size, uint32_t timeout_ms)
:   UART read bytes from UART buffer.

    参数
    :   - **id** – UART id

        - **data** – pointer to the buffer

        - **size** – data length to read

        - **timeout_ms** – timeout ms, if set BEKEN_WAIT_FOREVER, read will wait forever

    返回
    :   - BK_ERR_UART_NOT_INIT: UART driver not init

        - BK_ERR_UART_INVALID_ID: UART id number is invalid

        - BK_ERR_UART_ID_NOT_INIT: UART id not init

        - BK_ERR_UART_RX_TIMEOUT: UART receive data timeout

        - others (>=0): The number of bytes read from UART FIFO

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_disable_rx([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable UART TX pin and set as GPIO.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_disable_tx([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable UART TX pin and set as GPIO.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_enable_rx([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, bool enable)
:   Just set UART RX enable/disable, doesn’t set pin.

    参数
    :   - **id** – UART id

        - **enable** – true, enable, flase disable

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_set_enable_tx([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, bool enable)
:   Just set UART TX enable/disable, doesn’t set pin.

    参数
    :   - **id** – UART id

        - **enable** – true, enable, flase disable

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_enable_sw_fifo([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Enable UART software fifo.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_disable_sw_fifo([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Disable UART software fifo.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_uart_get_ate_detect_gpio(void)
:   Get the gpio pin when in ate detect.

    返回
    :   the ate detect gpio pin

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_take_rx_isr([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, [uart_isr_t](#_CPPv410uart_isr_t "uart_isr_t") isr, void *param)
:   Register uart rx isr and disable software fifo.

    参数
    :   - **id** – UART id

        - **isr** – UART RX callback

        - **param** – UART RX callback parameter

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_recover_rx_isr([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Recover uart rx isr.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

bool bk_uart_is_tx_over([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Get whether the uart tx over(tx fifo empty)

    参数
    :   **id** – UART id

    返回
    :   - true: uart tx over

        - false: uart tx not over

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_pm_backup([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Backup uart config.

    参数
    :   **id** – UART id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_uart_pm_restore([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)

void bk_uart_wait_tx_over([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id)
:   Wait uart tx over.

    参数
    :   **id** – UART id

    返回
    :   - void


## UART API Typedefs


### Header File


- [uart_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/uart_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/uart_types.h")


### Macros

BK_ERR_UART_NOT_INIT
:   UART driver not init

BK_ERR_UART_INVALID_ID
:   UART id number is invalid

BK_ERR_UART_INVALID_SIZE
:   UART read bytes length is more than fifo length

BK_ERR_UART_RX_TIMEOUT
:   UART receive data timeout

BK_ERR_UART_BAUD_RATE_NOT_SUPPORT
:   UART baud rate not support

BK_ERR_UART_ID_NOT_INIT
:   UART id not init

BK_ERR_UART_MUTEX_INIT
:   UART mutex init failed


### Type Definitions

typedef void (*uart_isr_t)([uart_id_t](#_CPPv49uart_id_t "uart_id_t") id, void *param)
:   UART interrupt service routine.


### Header File


- [hal/hal_uart_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_uart_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_uart_types.h")


### Structures

struct uart_config_t
:   Public Members

    uint32_t baud_rate
    :   UART baud rate

    [uart_data_bits_t](#_CPPv416uart_data_bits_t "uart_data_bits_t") data_bits
    :   UART data bits

    [uart_parity_t](#_CPPv413uart_parity_t "uart_parity_t") parity
    :   UART parity

    [uart_stop_bits_t](#_CPPv416uart_stop_bits_t "uart_stop_bits_t") stop_bits
    :   UART stop bits

    [uart_flow_control_t](#_CPPv419uart_flow_control_t "uart_flow_control_t") flow_ctrl
    :   UART flow control

    [uart_src_clk_t](#_CPPv414uart_src_clk_t "uart_src_clk_t") src_clk
    :   UART source clock


### Macros

UART_BAUDRATE_3250000

UART_BAUDRATE_2000000

UART_BAUDRATE_921600

UART_BAUDRATE_460800

UART_BAUDRATE_230400

UART_BAUDRATE_115200

UART_BAUDRATE_3000

UART_BAUDRATE_19200

UART_BAUDRATE_9600

UART_BAUD_RATE

UART_CLOCK_FREQ_10M

UART_CLOCK_FREQ_48M

UART_CLOCK_FREQ_24M

UART_CLOCK_FREQ_26M

UART_CLOCK_FREQ_52M

UART_CLOCK_FREQ_120M

UART_CLOCK_FREQ_80M

UART_CLOCK

UART_TX_FIFO_THRESHOLD

UART_RX_FIFO_THRESHOLD


### Type Definitions

typedef uint8_t uart_unit_t
:   uart uint id


### Enumerations

enum uart_id_t
:   *Values:*

    enumerator UART_ID_0
    :   UART id 0

    enumerator UART_ID_1
    :   UART id 1

    enumerator UART_ID_2
    :   UART id 2

    enumerator UART_ID_3
    :   UART id 3

    enumerator UART_ID_4
    :   UART id 4

    enumerator UART_ID_5
    :   UART id 5

    enumerator UART_ID_MAX
    :   UART id max

enum uart_src_clk_t
:   *Values:*

    enumerator UART_SCLK_DCO
    :   UART source clock dco

    enumerator UART_SCLK_XTAL_26M
    :   UART source clock xtal 26M

    enumerator UART_SCLK_APLL
    :   UART source clock apll

    enumerator UART_SCLK_80M
    :   UART source clock 80M

enum uart_frame_mode_t
:   *Values:*

    enumerator UART_MODE_UART
    :   UART frame mode uart

    enumerator UART_MODE_IDRA
    :   UART frame mode idra

enum uart_data_bits_t
:   *Values:*

    enumerator UART_DATA_5_BITS
    :   UART data bits 5bits

    enumerator UART_DATA_6_BITS
    :   UART data bits 6bits

    enumerator UART_DATA_7_BITS
    :   UART data bits 7bits

    enumerator UART_DATA_8_BITS
    :   UART data bits 8bits

enum uart_parity_t
:   *Values:*

    enumerator UART_PARITY_NONE
    :   UART parity none

    enumerator UART_PARITY_ODD
    :   UART parity odd

    enumerator UART_PARITY_EVEN
    :   UART parity even

enum uart_stop_bits_t
:   *Values:*

    enumerator UART_STOP_BITS_1
    :   UART stop bits 1bit

    enumerator UART_STOP_BITS_2
    :   UART stop bits 2bits

enum uart_flow_control_t
:   *Values:*

    enumerator UART_FLOWCTRL_DISABLE
    :   UART flow control disable

    enumerator UART_FLOWCTRL_CTS_RTS
    :   UART flow control cts rts

enum uart_rx_stop_detect_time_t
:   *Values:*

    enumerator UART_RX_STOP_DETECT_TIME_32_BITS
    :   UART rx stop time 32 bits

    enumerator UART_RX_STOP_DETECT_TIME_64_BITS
    :   UART rx stop time 64 bits

    enumerator UART_RX_STOP_DETECT_TIME_128_BITS
    :   UART rx stop time 128 bits

    enumerator UART_RX_STOP_DETECT_TIME_256_BITS
    :   UART rx stop time 256 bits

enum uart_dma_enable_t
:   *Values:*

    enumerator UART_DMA_DISABLE

    enumerator UART_DMA_ENABLE
