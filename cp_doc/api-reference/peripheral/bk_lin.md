# LIN


BK7259 CP 侧 LIN API（`include/driver/lin.h`）。


## LIN API Reference


### Header File


- [lin.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/lin.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/lin.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_gpio_init([lin_channel_t](#_CPPv413lin_channel_t "lin_channel_t") chn)
:   Select the LIN gpio.

    This API adaptation hardware link channel

    参数
    :   **chn** – gpio channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_cfg([lin_config_t](#_CPPv412lin_config_t "lin_config_t") *cfg)
:   the LIN config

    This API lin configure interface

    参数
    :   **cfg** – basic configuration information

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_driver_init(void)
:   Init the LIN driver.

    This API init the resoure common:


    - Init LIN driver control memory


    **Attention**
    :   1. This API should be called before any other LIN APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_driver_deinit(void)
:   Deinit the LIN driver.

    This API free all resource related to LIN and disable LIN.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_interrupt_enable(void)
:   Enable LIN interrupt.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_interrupt_disable(void)
:   Disable LIN interrupt.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_register_isr([lin_int_type_t](#_CPPv414lin_int_type_t "lin_int_type_t") type, [lin_isr_t](#_CPPv49lin_isr_t "lin_isr_t") isr, void *arg)
:   Register the interrupt service routine for LIN.

    This API register lin isr callback function.

    参数
    :   - **type** – register interrupt type

        - **isr** – lin callback

        - **arg** – lin callback arg

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_dev([lin_dev_t](#_CPPv49lin_dev_t "lin_dev_t") dev)
:   Set this device as master or slave.

    参数
    :   **lin_dev_t** – device type

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_get_dev(void)
:   Get this device as master or slave.

    参数
    :   **lin_dev_t** – device type

    返回
    :   - 0: slave

        - 1: master

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_ident(uint32_t ident)
:   Set this device ident.

    This interface will set the id and transmission direction of the data frame

    参数
    :   **ident** – bit3 for master indicates whether this frame is a sending or receving bit [4] is direction :0 recv,1 send bit[3:0] is id number

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_get_ident(void)
:   get this device ident

    get identifer and transmittion direction

    返回
    :   - bit [4] is direction :0 recv,1 send bit[3:0] is id number

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_rate(double rate)
:   Set this device bit rate (master only)

    This interface will set data rate between 1 Kbit/s and 20 Kbit/s (for master) automatic bit rate detection (for slave)

    参数
    :   **rate** – data rate

    返回
    :   - BK_OK: succeed

        - others: other errors.

double bk_lin_get_rate(void)
:   Get this device bit rate (master only)

    get data rate

    返回
    :   - data rate value

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_data_length([lin_data_len_t](#_CPPv414lin_data_len_t "lin_data_len_t") len)
:   Set the transmission data length.

    the max data length is 8bytes

    参数
    :   **len** – data length

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_get_data_length(void)
:   Get the transmission data length.

    the max data length is 8bytes

    返回
    :   - data length value.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_enh_check([lin_checksum_t](#_CPPv414lin_checksum_t "lin_checksum_t") check)
:   Set the checksum type.

    参数
    :   **checksum** – type:0 classic checksum,1 enhanced checksum

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_get_enh_check(void)
:   Get the checksum type.

    返回
    :   - checksum value.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_bus_inactivity_time([lin_bus_inactivity_time_t](#_CPPv425lin_bus_inactivity_time_t "lin_bus_inactivity_time_t") time)
:   Set bus inactivity time(slave only),.

    This API will generate an bus idle timeout interrupt when it detectes no bus activity for a set time.

    参数
    :   **time** – set timeout, 0:4s, 1:6s, 2:8s, 3:10s

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_get_bus_inactivity_time(void)
:   Get bus inactivity time(slave only),.

    返回
    :   - bus inactivity enum

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_wup_repeat_time([lin_wup_repeat_time_t](#_CPPv421lin_wup_repeat_time_t "lin_wup_repeat_time_t") time)
:   Set wake up repeat time(slave only),.

    The time for repeating of wake up because of no reaction on the bus

    参数
    :   **time** – set time, 0:180ms, 1:200ms, 2:220ms, 3:240ms

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_get_wup_repeat_time(void)
:   Get wake up repeat time(slave only),.

    返回
    :   - repeat time enum

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_transmit([lin_trans_t](#_CPPv411lin_trans_t "lin_trans_t") trans)
:   Set transmit operation,.

    The API determines whether the current frame is transmit frame or a receive frame for the LIN node.

    参数
    :   **trans** – 1 - transmit operation, 0 - receive operation

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_get_transmit(void)
:   get transmit operation,

    参数
    :   **trans** – 1 - transmit operation, 0 - receive operation

    返回
    :   - 1: transmit operation,

        - 0: receive operation,

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_send(uint8_t *buf, uint32_t len)
:   load buf to the data bytes

    参数
    :   - **buf** – source data buffer

        - **len** – data length,max 8 bytes

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_recv(uint8_t *buf, uint32_t len)
:   load data bytes to buf,

    参数
    :   - **buf** – destination data buffer

        - **len** – data length,max 8 bytes

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_tx([lin_id_t](#_CPPv48lin_id_t "lin_id_t") id, uint8_t *tx, uint32_t len)
:   Send data based on specified id,.

    参数
    :   - **id** – target id of sending data

        - **tx** – send data buffer

        - **len** – data length,max 8 bytes

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_rx([lin_id_t](#_CPPv48lin_id_t "lin_id_t") id, uint8_t *rx, uint32_t len, uint32_t timeout)
:   Recevie data based on specified id.

    This interface has blocking function. using freeROTS task notification mechanism

    The API recevie data max 8 bytes

    参数
    :   - **id** – target id to recevie data

        - **rx** – recevie data buffer

        - **len** – data length,max 8 bytes

        - **timeout** – The maximum amount of time that the task should wait in the Blocked state for a notification to be received.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_start_req(void)
:   Set start transmission request,.

    The API is celled to start the LIN transmission after loading identifier, data length and data buffer

    master only,slaver reserved

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_get_start_req(void)
:   Get start transmission request status,.

    The API is celled to start the LIN transmission after loading identifier, data length and data buffer

    master only,slaver reserved

    返回
    :   - 0: The transmission is finished or an error is occurred

        - 1: Transmitting.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_sleep(void)
:   Set sleep mode,.

    The API is used by LIN to determine whether the LIN bus is in sleep mode or not

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_get_sleep(void)
:   Get sleep mode,.

    返回
    :   - 1: sleep

        - 0: wakeup

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_lin_set_wakeup(void)
:   Set wakeup request,.

    The API terminate the sleep mode of LIN bus by sending a wakeup signal

    返回
    :   - BK_OK: succeed

        - others: other errors.


## LIN API Typedefs


### Header File


- [lin_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/lin_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/lin_types.h")


### Structures

struct lin_callback_t

struct lin_gpio_map_t

struct lin_gpio_t

struct lin_buf_t

struct lin_config_t
:   Public Members

    [lin_bus_inactivity_time_t](#_CPPv425lin_bus_inactivity_time_t "lin_bus_inactivity_time_t") bus_inactiv_time
    :   master only

    [lin_wup_repeat_time_t](#_CPPv421lin_wup_repeat_time_t "lin_wup_repeat_time_t") wup_repeat_time
    :   slave only


### Macros

BK_ERR_LIN_NOT_INIT
:   LIN driver not init

BK_ERR_LIN_INT_TYPE
:   LIN interrupte type error

BK_ERR_LIN_BIT_ERROR
:   LIN bit error

BK_ERR_LIN_CHK_ERROR
:   LIN checksum error

BK_ERR_LIN_TIMEOUT_ERROR
:   LIN timeout error

BK_ERR_LIN_PARITY_ERROR
:   LIN identifier parity error

BK_ERR_LIN_HAL_INVALID_ADDR
:   LIN invalid addr

BK_ERR_LIN_HAL_INVALID_ARG
:   LIN invalid arg


### Type Definitions

typedef void (*lin_isr_t)(void *arg)


### Enumerations

enum lin_int_type_t
:   *Values:*

    enumerator LIN_INT_COMPLETE

    enumerator LIN_INT_WAKEUP

    enumerator LIN_INT_IDLE_TIMEOUT

    enumerator LIN_INT_ABORTED

    enumerator LIN_INT_DATA_REQ

    enumerator LIN_INT_BIT_ERR

    enumerator LIN_INT_CHK_ERR

    enumerator LIN_INT_TIMEOUT_ERR

    enumerator LIN_INT_PARITY_ERR

    enumerator LIN_INT_MAX

enum lin_trans_t
:   *Values:*

    enumerator LIN_RECV

    enumerator LIN_SEND

enum lin_en_t
:   *Values:*

    enumerator LIN_DISABLE

    enumerator LIN_ENABLE

enum lin_bus_inactivity_time_t
:   *Values:*

    enumerator LIN_BUS_INACTIVITY_4S

    enumerator LIN_BUS_INACTIVITY_6S

    enumerator LIN_BUS_INACTIVITY_8S

    enumerator LIN_BUS_INACTIVITY_10S

enum lin_wup_repeat_time_t
:   *Values:*

    enumerator LIN_WUP_REPEAT_180MS

    enumerator LIN_WUP_REPEAT_200MS

    enumerator LIN_WUP_REPEAT_220MS

    enumerator LIN_WUP_REPEAT_240MS

enum lin_id_t
:   *Values:*

    enumerator LIN_IDENT_MIN

    enumerator LIN_IDENT0

    enumerator LIN_IDENT1

    enumerator LIN_IDENT2

    enumerator LIN_IDENT3

    enumerator LIN_IDENT4

    enumerator LIN_IDENT5

    enumerator LIN_IDENT6

    enumerator LIN_IDENT7

    enumerator LIN_IDENT8

    enumerator LIN_IDENT9

    enumerator LIN_IDENT10

    enumerator LIN_IDENT11

    enumerator LIN_IDENT12

    enumerator LIN_IDENT13

    enumerator LIN_IDENT14

    enumerator LIN_IDENT15

    enumerator LIN_IDENT_MAX

enum lin_checksum_t
:   *Values:*

    enumerator LIN_CLASSIC

    enumerator LIN_ENHANCED

enum lin_data_len_t
:   *Values:*

    enumerator LIN_DATA_LEN_MIN

    enumerator LIN_DATA_LEN_1BYTES

    enumerator LIN_DATA_LEN_2BYTES

    enumerator LIN_DATA_LEN_3BYTES

    enumerator LIN_DATA_LEN_4BYTES

    enumerator LIN_DATA_LEN_5BYTES

    enumerator LIN_DATA_LEN_6BYTES

    enumerator LIN_DATA_LEN_7BYTES

    enumerator LIN_DATA_LEN_8BYTES

    enumerator LIN_DATA_LEN_MAX


### Header File


- [hal/hal_lin_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_lin_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_lin_types.h")


### Macros

LIN_RATE_20KBIT

LIN_CLK_26M

LIN_BAUD_RATE_MIN

LIN_BAUD_RATE_MAX


### Enumerations

enum lin_dev_t
:   *Values:*

    enumerator LIN_SLAVE

    enumerator LIN_MASTER

enum lin_channel_t
:   *Values:*

    enumerator LIN_CHAN_0
    :   lin gpio0/gpio1/gpuo2

    enumerator LIN_CHAN_1
    :   lin gpio30/gpio31/gpuo42

    enumerator LIN_CHAN_2
    :   lin gpio40/gpio41/gpuo42

    enumerator LIN_CHAN_MAX
