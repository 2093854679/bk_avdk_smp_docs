# CAN



## CAN API Status

| API | BK7259_AP |
| --- | --- |
| [`bk_can_init()`](#_CPPv411bk_can_initP9can_dev_t "bk_can_init") | Y |
| [`bk_can_driver_init()`](#_CPPv418bk_can_driver_initv "bk_can_driver_init") | Y |
| [`bk_can_driver_deinit()`](#_CPPv420bk_can_driver_deinitv "bk_can_driver_deinit") | Y |
| [`bk_can_deinit()`](#_CPPv413bk_can_deinitv "bk_can_deinit") | Y |
| [`bk_can_send()`](#_CPPv411bk_can_sendP11can_frame_s8uint32_t "bk_can_send") | Y |
| [`bk_can_acc_filter_set()`](#_CPPv421bk_can_acc_filter_setP20can_acc_filter_cmd_s "bk_can_acc_filter_set") | Y |
| [`bk_can_register_isr_callback()`](#_CPPv428bk_can_register_isr_callbackP18can_callback_des_tP18can_callback_des_t "bk_can_register_isr_callback") | Y |
| [`bk_can_register_err_callback()`](#_CPPv428bk_can_register_err_callbackP18can_callback_des_t "bk_can_register_err_callback") | Y |
| [`can_driver_bit_rate_config()`](#_CPPv426can_driver_bit_rate_config14can_bit_rate_e14can_bit_rate_e "can_driver_bit_rate_config") | Y |


## CAN API Reference


### Header File


- [can.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/can.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/can.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_can_init([can_dev_t](#_CPPv49can_dev_t "can_dev_t") *can)
:   The CAN config.

    参数
    :   **can** – **[in]** structure of parameters

    返回
    :   bk_err_t error code

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_can_driver_init(void)
:   CAN software module init.

    返回
    :   bk_err_t error code

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_can_driver_deinit(void)
:   CAN software module deinit.

    返回
    :   bk_err_t error code

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_can_deinit(void)
:   free the CAN config

    返回
    :   bk_err_t error code

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_can_receive(uint8_t *data, uint32_t expect_size, uint32_t *recv_size, uint32_t timeout)
:   CAN receive frames.

    备注

    Pop out the data from software fifo

    参数
    :   - **data** – **[in]** buffer to store data in

        - **expect_size** – **[in]** size of data expect to get

        - **recv_size** – **[in]** size of data actually get

        - **timeout** – **[in]** max wait time to achieve the expect size

    返回
    :   bk_err_t error code

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_can_send_ptb([can_frame_s](#_CPPv411can_frame_s "can_frame_s") *frame)
:   CAN send frame through primary transmit buffer.

    备注

    Put in fifo one message that would be transmitted at the next possible positon

    参数
    :   **frame** – **[in]** One frame for transmission

    返回
    :   bk_err_t error code

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_can_send([can_frame_s](#_CPPv411can_frame_s "can_frame_s") *frame, uint32_t timeout)
:   CAN send frame through secondary transmit buffer.

    备注

    Put in fifo frames that would be sent out together Data in fifo would be conbined to reach the longest legal length Data share the same arbitration parameter

    参数
    :   - **frame** – **[in]** One frame for transmission

        - **timeout** – **[in]** max wait time to send out all data

    返回
    :   bk_err_t error code

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_can_acc_filter_set([can_acc_filter_cmd_s](#_CPPv420can_acc_filter_cmd_s "can_acc_filter_cmd_s") *cmd)
:   CAN acceptance filter set.

    备注

    Only filter 0 accpet all messages by default Disabled bits result in accepting the message

    参数
    :   **cmd** – **[in]** structure of parameter

    返回
    :   bk_err_t error code

void bk_can_register_isr_callback([can_callback_des_t](#_CPPv418can_callback_des_t "can_callback_des_t") *rx_cb, [can_callback_des_t](#_CPPv418can_callback_des_t "can_callback_des_t") *tx_cb)
:   CAN register callback.

    备注

    Register to send and receive completed interrupt callback funcitons. The callback funciton is called in the interrupt. Pay attention to the operation.

    参数
    :   - **rx_cb** – **[in]** Receive callback functions and parameters

        - **tx_cb** – **[in]** Send callback functions and parameters

void bk_can_register_err_callback([can_callback_des_t](#_CPPv418can_callback_des_t "can_callback_des_t") *err_cb)
:   CAN register callback.

    备注

    Register to Error interrupt callback funcitons. The callback funciton is called in the interrupt. Pay attention to the operation.

    参数
    :   **err_cb** – **[in]** Error callback functions and parameters

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") can_driver_bit_rate_config([can_bit_rate_e](#_CPPv414can_bit_rate_e "can_bit_rate_e") s_speed, [can_bit_rate_e](#_CPPv414can_bit_rate_e "can_bit_rate_e") f_speed)
:   Adjusting the Baud Rate.

    备注

    Berfore sending data, the baud rate can be adjusted Pay attention to the protocol used to prevent speed mismatch.

    参数
    :   - **s_speed** – **[in]** CAN2.0 Baud rate

        - **f_speed** – **[in]** CAN FD Baud rate


## CAN API Typedefs


### Header File


- [can_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/can_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/can_types.h")


### Structures

struct can_gpio_map_t

struct can_gpio_t

struct can_fifo_t

struct can_env_t

struct can_config_t

struct can_dev_t


### Macros

BK_ERR_CAN_NOT_INIT
:   CAN driver not init

BK_ERR_CAN_INT_TYPE
:   CAN interrupte type error

BK_ERR_CAN_BIT_ERROR
:   CAN bit error

BK_ERR_CAN_CHK_ERROR
:   CAN checksum error

BK_ERR_CAN_TIMEOUT_ERROR
:   CAN timeout error

BK_ERR_CAN_PARITY_ERROR
:   CAN identifier parity error

BK_ERR_CAN_HAL_INVALID_ADDR
:   CAN invalid addr

BK_ERR_CAN_HAL_INVALID_ARG
:   CAN invalid arg


### Enumerations

enum can_status_e
:   *Values:*

    enumerator CAN_STATUS_CLOSED

    enumerator CAN_STATUS_IDLE

    enumerator CAN_STATUS_OPENED


### Header File


- [hal/hal_can_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_can_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_can_types.h")


### Structures

struct can_core_br_tab_s

struct can_speed_t

struct can_acc_filter_cmd_s

struct can_frame_tag_t

struct can_frame_s

struct can_callback_des_t

struct can_hal_t


### Macros

RX_INT_FLAG_GROUP

TX_INT_FLAG_GROUP

ERR_INT_FLAG_GROUP

TT_INT_FLAG_GROUP

MEM_INT_FLAG_GROUP

SAFE_INT_FLAG_GROUP

OTHER_INT_FLAG_GROUP

CC_RAM_MEMTYPE

CC_RAM_TYPE

CC_RAM_ECC

CC_RAM_ES

CC_RBUF_SLOTS

CC_STB_ENABLE

CC_STB_SLOTS

CC_STB_PRIO

CC_ACF_NUMBER

CC_CAN_FD

CC_UPWARD_COMPATIBILITY

CC_TTCAN

CC_CIA603

CC_SAFETY_ENABLE

CAN_20_MAX_PAYLOAD

CAN_FD_MAX_PAYLOAD

MAX_ACF_NUM

FDF_CAN_20

FDF_CAN_FD

CAN_STAND_ID_MASK

CAN_EXT_ID_MASK

POS_TTSEN

TTSEN_MASK

RSTAT_EMPTY

RSTAT_AFWL

RSTAT_NOFULL

RSTAT_FULL

BUF_REG_NUM


### Type Definitions

typedef void (*can_callback)(void *param)

typedef uint32_t (*can_fifo_f)(uint8_t *buf, uint32_t len)

typedef uint32_t (*can_size_f)(void)


### Enumerations

enum can_channel_t
:   *Values:*

    enumerator CAN_CHAN_0
    :   can gpio44/gpio45/gpuo46

    enumerator CAN_CHAN_MAX

enum can_bit_rate_e
:   *Values:*

    enumerator CAN_BR_125K

    enumerator CAN_BR_250K

    enumerator CAN_BR_500K

    enumerator CAN_BR_800K

    enumerator CAN_BR_1M

    enumerator CAN_BR_2M

    enumerator CAN_BR_4M

    enumerator CAN_BR_5M

enum can_ctrl_cmd_e
:   *Values:*

    enumerator CMD_CAN_MODUILE_INIT

    enumerator CMD_CAN_SET_RX_CALLBACK

    enumerator CMD_CAN_SET_TX_CALLBACK

    enumerator CMD_CAN_RESET_REQ

    enumerator CMD_CAN_ACC_FILTER_SET

    enumerator CMD_CAN_SET_TX_FIFO

    enumerator CMD_CAN_GET_TX_SIZE

    enumerator CMD_CAN_SET_RX_FIFO

    enumerator CMD_CAN_FD_BOSCH_MODE

    enumerator CMD_CAN_GET_RX_FRAME_TAG

    enumerator CMD_CAN_SET_TX_FRAME_TAG

    enumerator CMD_CAN_PTB_INBUF

    enumerator CMD_CAN_TRANS_SWITCH

    enumerator CMD_CAN_STB_INBUF

    enumerator CMD_CAN_SET_ERR_CALLBACK

    enumerator CMD_CAN_BUSOFF_CLR

    enumerator CMD_CAN_GET_KOER

enum drv_switch_e
:   *Values:*

    enumerator DRIVER_DISABLE

    enumerator DRIVER_ENABLE

enum can_err_int_e
:   *Values:*

    enumerator CAN_ERRINT_BUS

    enumerator CAN_ERRINT_ARB_LOST

    enumerator CAN_ERRINT_PASSIVE

    enumerator CAN_ERRINT_WARN_LIM

enum can_protocol_e
:   *Values:*

    enumerator CAN_PROTO_20

    enumerator CAN_PROTO_FD

enum can_form_e
:   *Values:*

    enumerator CAN_FORM_STD

    enumerator CAN_FORM_EXT

enum can_frame_e
:   *Values:*

    enumerator CAN_FRAME_DATA

    enumerator CAN_FRAME_REMT

enum can_brate_e
:   *Values:*

    enumerator CAN_BIT_RATE_SLOW

    enumerator CAN_BIT_RATE_FAST

enum can_acc_mask_ide_e
:   *Values:*

    enumerator CAN_ACCEPT_BOTH

    enumerator CAN_ACCEPT_STANDARD

    enumerator CAN_ACCEPT_EXTENDED

enum can_loc_reset_c
:   *Values:*

    enumerator CAN_RESET_REQ_EN

    enumerator CAN_RESET_REQ_NO

enum can_trans_switch_c
:   *Values:*

    enumerator CAN_TPE

    enumerator CAN_TPA

    enumerator CAN_TSONE

    enumerator CAN_TSALL

    enumerator CAN_TSA

enum can_koer_code_e
:   *Values:*

    enumerator CAN_KOER_NO

    enumerator CAN_KOER_BIT

    enumerator CAN_KOER_FORM

    enumerator CAN_KOER_STUFF

    enumerator CAN_KOER_ACK

    enumerator CAN_KOER_CRC

    enumerator CAN_KOER_OTHER

    enumerator CAN_KOER_NOUSE
