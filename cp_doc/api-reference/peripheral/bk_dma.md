# DMA


BK7259 CP 侧 DMA API（`include/driver/dma.h`）。详细说明见
[DMA 开发指南](../../developer-guide/peripheral/bk_dma.md "../../developer-guide/peripheral/bk_dma.md")。


## DMA API Reference


### Header File


- [dma.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/dma.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/dma.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_driver_init(void)
:   Init the DMA driver.

    This API init the resoure common to all dma channels:


    - Init dma driver control memory

    This API should be called before any other dma APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_driver_deinit(void)
:   Deinit the DMA driver.

    This API free all resource related to dma and power down all dma channels.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[dma_id_t](#_CPPv48dma_id_t "dma_id_t") bk_dma_alloc(u16 user_id)
:   Allocate a DMA channel.

    This API should be called before any other dma channel APIs.


    **Attention**
    :   : This API can only be called in task context,


        - and can’t be called in context that interrupt is disabled.

    参数
    :   **user_id** – DMA channel applicant

    返回
    :   DMA channel id.


        - > DMA_ID_MAX: no free DMA channel.

[dma_id_t](#_CPPv48dma_id_t "dma_id_t") bk_fixed_dma_alloc(u16 user_id, [dma_id_t](#_CPPv48dma_id_t "dma_id_t") fixed_chnl_id)
:   Allocate a fixed DMA channel.Maybe some APP needs to have a fixed channel forever, then it can use this API.

    This API should be called before any other dma channel APIs.

    参数
    :   - **user_id** – DMA channel applicant

        - **fixed_chnl_id** – application wants to get which fixed channel

    返回
    :   DMA channel id.


        - > DMA_ID_MAX: if the fixed_chnl_id has been allocated, it will return DMA_ID_MAX which means error.

        - > fixed_chnl_id: the fixed_chnl_id is allocated suc.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_free(u16 user_id, [dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Free the DMA channel.


    **Attention**
    :   : This API can only be called in task context,


        - and can’t be called in context that interrupt is disabled.

    参数
    :   - **user_id** – DMA channel applicant, the same as in bk_dma_alloc.

        - **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_dma_user([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   get the user of DMA channel

    参数
    :   **id** – DMA channel

    返回
    :   DMA channel user_id.


        - u32: high u16 is the CPU_ID, low 16 bits is the applicant_id.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_init([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, const [dma_config_t](#_CPPv412dma_config_t "dma_config_t") *config)
:   Init the DMA channel.


    **Attention**
    :   1. the higher channel priority value, the higher the priority

    参数
    :   - **id** – DMA channel

        - **config** – DMA configuration

    返回
    :   - BK_OK: succeed

        - BK_ERR_DMA_NOT_INIT: DMA driver not init

        - BK_ERR_NULL_PARAM: config is NULL

        - BK_ERR_DMA_ID: invalid DMA channel

        - BK_ERR_DMA_INVALID_ADDR: invalid DMA address

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_deinit([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Deinit a DMA channel.

    This API deinit the DMA channel:


    - Stop the DMA channel

    - Reset all configuration of DMA channel to default value

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_start([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Start a DMA channel.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_stop([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Stop a DMA channel.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_write([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, const uint8_t *data, uint32_t size)
:   Transfer data from memory to peripheral.

    参数
    :   - **id** – DMA channel

        - **data** – DMA transfer data

        - **size** – data size

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_read([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, uint8_t *data, uint32_t size)
:   Transfer data from peripheral to memory.

    参数
    :   - **id** – DMA channel

        - **data** – DMA transfer data

        - **size** – data size

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_enable_finish_interrupt([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA finish intterrup.

    @NOTES before enable interrupt, please confirm have called bk_dma_register_isr.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_disable_finish_interrupt([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA finish intterrup.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_enable_half_finish_interrupt([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA half finish intterrup.

    @NOTES before enable interrupt, please confirm have called bk_dma_register_isr.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_disable_half_finish_interrupt([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA half finish intterrup.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_register_isr([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, [dma_isr_t](#_CPPv49dma_isr_t "dma_isr_t") half_finish_isr, [dma_isr_t](#_CPPv49dma_isr_t "dma_isr_t") finish_isr)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel

        - **half_finish_isr** – DMA half finish callback

        - **finish_isr** – DMA finish callback

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_register_bus_err_isr([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, [dma_isr_t](#_CPPv49dma_isr_t "dma_isr_t") bus_err_isr)
:   Register the interrupt service routine for DMA channel.

    This API regist dma error isr callback function.

    参数
    :   - **id** – DMA channel

        - **bus_err_isr** – DMA bus error callback

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_register_isr_arg([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, [dma_isr_arg_reg_t](#_CPPv417dma_isr_arg_reg_t "dma_isr_arg_reg_t") *dma_arg_isr)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel

        - **dma_arg_isr** – DMA half finish, finish, bus error callback and pointer variable

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_register_half_finish_isr_arg([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, [dma_isr_arg_t](#_CPPv413dma_isr_arg_t "dma_isr_arg_t") half_finish_isr, void *arg)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel

        - **dma_arg_isr** – DMA half finish callback and pointer variable

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_register_finish_isr_arg([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, [dma_isr_arg_t](#_CPPv413dma_isr_arg_t "dma_isr_arg_t") finish_isr, void *arg)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel

        - **dma_arg_isr** – DMA finish callback and pointer variable

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_register_bus_err_isr_arg([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, [dma_isr_arg_t](#_CPPv413dma_isr_arg_t "dma_isr_arg_t") bus_err_isr, void *arg)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel

        - **dma_arg_isr** – DMA bus error callback and pointer variable

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_dma_get_transfer_len_max([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   get DMA transfer max length in one round, default value is 65536 bytes.

    参数
    :   **id** – DMA channel

    返回
    :   - max len: how many bytes can be copy by DMA in one round.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_set_transfer_len([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, uint32_t tran_len)
:   Set DMA transfer length.

    参数
    :   - **id** – DMA channel

        - **tran_len** – DMA transfer length, the tran_len should be <= bk_dma_get_transfer_len_max() bytes.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_set_src_addr([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, uint32_t start_addr, uint32_t end_addr)
:   Set DMA source address.


    **Attention**
    :   1. address should be zero when there is no value, e.g. bk_dma_set_src_addr(1, 0x80210C, 0)

    参数
    :   - **id** – DMA channel

        - **start_addr** – DMA source start address

        - **end_addr** – DMA source end address

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_set_src_start_addr([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, uint32_t start_addr)
:   Set DMA source start address.

    参数
    :   - **id** – DMA channel

        - **start_addr** – DMA source start address

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_set_dest_addr([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, uint32_t start_addr, uint32_t end_addr)
:   Set DMA dest address.


    **Attention**
    :   1. address should be zero when there is no value, e.g. bk_dma_set_dest_addr(1, 0x80210C, 0)

    参数
    :   - **id** – DMA channel

        - **start_addr** – DMA dest start address

        - **end_addr** – DMA dest end address

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_set_dest_start_addr([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id, uint32_t start_addr)
:   Set DMA dest start address.

    参数
    :   - **id** – DMA channel

        - **start_addr** – DMA dest start address

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_enable_src_addr_increase([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA source address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_disable_src_addr_increase([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA source address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_enable_src_addr_loop([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA source address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_disable_src_addr_loop([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA source address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_enable_dest_addr_increase([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA dest address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_disable_dest_addr_increase([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA dest address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_enable_dest_addr_loop([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA dest address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_disable_dest_addr_loop([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA dest address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_dma_get_remain_len([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Get DMA transfer remain length.

    参数
    :   **id** – DMA channel

    返回
    :   DMA transfer remain length

uint32_t bk_dma_get_enable_status([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Gets the current DMA channel working status.

    参数
    :   **id** – DMA channel

    返回
    :   - 0: Channel idle state

        - others: Channel busy state.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_dma_flush_src_buffer([dma_id_t](#_CPPv48dma_id_t "dma_id_t") id)
:   flush reserved data in dma internal buffer I.E:If source data width is not 4bytes, and data size isn’t 4bytes align, but dest data width is 4bytes, then maybe 1~3 bytes data reserved in dma internal buffer, then the left 1~3 bytes data not copy to dest address.

    参数
    :   - **id** – DMA channel

        - **attr** – DMA privileged attr

    返回
    :   - 0: Channel idle state

        - others: Channel busy state.


## DMA API Typedefs


### Header File


- [dma_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/dma_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/dma_types.h")


### Structures

struct dma_isr_arg_reg_t


### Macros

BK_ERR_DMA_ID
:   DMA id is invalid

BK_ERR_DMA_NOT_INIT
:   DMA driver not init

BK_ERR_DMA_ID_NOT_INIT
:   DMA id not init

BK_ERR_DMA_ID_NOT_START
:   DMA id not start

BK_ERR_DMA_INVALID_ADDR
:   DMA addr is invalid

BK_ERR_DMA_ID_REINIT
:   DMA id has inited, if reinit,please de-init firstly

BK_ERR_DMA_TRANS_LEN
:   DMA trans len is invalid


### Type Definitions

typedef void (*dma_isr_t)([dma_id_t](#_CPPv48dma_id_t "dma_id_t") dma_id)
:   DMA interrupt service routine.

typedef void (*dma_isr_arg_t)([dma_id_t](#_CPPv48dma_id_t "dma_id_t") dma_id, void *arg)


### Header File


- [hal/hal_dma_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_dma_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_dma_types.h")


### Structures

struct dma_port_config_t
:   Public Members

    [dma_dev_t](#_CPPv49dma_dev_t "dma_dev_t") dev
    :   DMA device

    [dma_data_width_t](#_CPPv416dma_data_width_t "dma_data_width_t") width
    :   DMA data width

    [dma_addr_inc_t](#_CPPv414dma_addr_inc_t "dma_addr_inc_t") addr_inc_en
    :   enable/disable DMA address increase

    [dma_addr_loop_t](#_CPPv415dma_addr_loop_t "dma_addr_loop_t") addr_loop_en
    :   enable/disable DMA address loop

    uint32_t start_addr
    :   DMA start address

    uint32_t end_addr
    :   DMA end address

struct dma_config_t
:   Public Members

    [dma_work_mode_t](#_CPPv415dma_work_mode_t "dma_work_mode_t") mode
    :   DMA work mode

    [dma_chan_priority_t](#_CPPv419dma_chan_priority_t "dma_chan_priority_t") chan_prio
    :   DMA channel prioprity

    [dma_port_config_t](#_CPPv417dma_port_config_t "dma_port_config_t") src
    :   DMA source configuration

    [dma_port_config_t](#_CPPv417dma_port_config_t "dma_port_config_t") dst
    :   DMA dest configuration

    [dma_pixel_trans_type_t](#_CPPv422dma_pixel_trans_type_t "dma_pixel_trans_type_t") trans_type
    :   DMA TRANS TYPE

    uint32_t dest_wr_intlv
    :   DMA Destination Write operate interval.unit is cycle

    uint32_t src_rd_intlv
    :   DMA Source Read operate interval.unit is cycle


### Macros

BK_ERR_DMA_HAL_INVALID_ADDR


### Type Definitions

typedef uint8_t dma_unit_t
:   DMA uint id

typedef uint8_t dma_chan_priority_t
:   DMA channel priority:the value is higher then the priority is higher


### Enumerations

enum dma_int_id_t
:   CPU core for DMA Interrupt Differentiation Notification.

    @Enumeration option selection core notifies DMA to interrupt after completion of transport

    @Notification of terminal selection based on channel operation


    *Values:*

    enumerator DMA_INT_0
    :   DMA INT 0

    enumerator DMA_INT_1
    :   DMA INT 1

    enumerator DMA_INT_2
    :   DMA INT 2

    enumerator DMA_INT_3
    :   DMA INT 3

    enumerator DMA_INT_MAX
    :   DMA channel max

enum dma_dev_t
:   *Values:*

    enumerator DMA_DEV_DTCM
    :   DMA device DTCM

    enumerator DMA_DEV_LA
    :   DMA device LA

    enumerator DMA_DEV_HSSPI
    :   DMA device HSSPI

    enumerator DMA_DEV_AUDIO
    :   DMA device AUDIO

    enumerator DMA_DEV_AUDIO_RX
    :   DMA device AUDIO

    enumerator DMA_DEV_SDIO
    :   DMA device SDIO

    enumerator DMA_DEV_SDIO_RX
    :   DMA device SDIO

    enumerator DMA_DEV_UART1
    :   DMA device UART1

    enumerator DMA_DEV_UART1_RX
    :   DMA device UART1

    enumerator DMA_DEV_UART2
    :   DMA device UART2

    enumerator DMA_DEV_UART2_RX
    :   DMA device UART 2 RX

    enumerator DMA_DEV_UART3
    :   DMA device UART3

    enumerator DMA_DEV_UART3_RX
    :   DMA device UART3

    enumerator DMA_DEV_UART4
    :   DMA device UART4

    enumerator DMA_DEV_UART4_RX
    :   DMA device UART4

    enumerator DMA_DEV_I2S
    :   DMA device I2S

    enumerator DMA_DEV_I2S_CH1
    :   DMA device I2S

    enumerator DMA_DEV_I2S_CH2
    :   DMA device I2S

    enumerator DMA_DEV_I2S_RX
    :   DMA device I2S

    enumerator DMA_DEV_I2S_RX_CH1
    :   DMA device I2S

    enumerator DMA_DEV_I2S_RX_CH2
    :   DMA device I2S

    enumerator DMA_DEV_I2S1
    :   DMA device I2S

    enumerator DMA_DEV_I2S1_RX
    :   DMA device I2S

    enumerator DMA_DEV_I2S2
    :   DMA device I2S

    enumerator DMA_DEV_I2S2_RX
    :   DMA device I2S

    enumerator DMA_DEV_GSPI0
    :   DMA device GSPI1

    enumerator DMA_DEV_GSPI0_RX
    :   DMA device GSPI1

    enumerator DMA_DEV_GSPI1
    :   DMA device GSPI2

    enumerator DMA_DEV_GSPI1_RX
    :   DMA device GSPI2

    enumerator DMA_DEV_GSPI2
    :   DMA device GSPI3

    enumerator DMA_DEV_JPEG
    :   DMA device JPEG

    enumerator DMA_DEV_PSRAM_VIDEO
    :   DMA device PSRAM VIDEO

    enumerator DMA_DEV_PSRAM_AUDIO
    :   DMA device PSRAM AUDIO

    enumerator DMA_DEV_USB
    :   DMA device USB

    enumerator DMA_DEV_LCD_CMD
    :   DMA device LCD CMD

    enumerator DMA_DEV_LCD_DATA
    :   DMA device LCD DATA

    enumerator DMA_DEV_DISP_RX
    :   DMA device DISP RX

    enumerator DMA_DEV_SDMADC_RX
    :   DMA device SDMADC RX

    enumerator DMA_DEV_AHB_MEM
    :   DMA device AHB_MEM

    enumerator DMA_DEV_SPI0
    :   DMA device SPI 0

    enumerator DMA_DEV_SPI1
    :   DMA device SPI 1

    enumerator DMA_DEV_H264
    :   DMA device H264

    enumerator DMA_DEV_I2S0
    :   DMA device I2S0

    enumerator DMA_DEV_I2S0_RX
    :   DMA device I2S0 RX

    enumerator DMA_DEV_GSPI2_RX
    :   DMA device GSPI2 RX

    enumerator DMA_DEV_AUD_DMIC
    :   DMA device aud dmic

    enumerator DMA_DEV_AUD_MIC0
    :   DMA device aud mic0

    enumerator DMA_DEV_AUD_SPK0
    :   DMA device aud spk0

    enumerator DMA_DEV_AUD_SPK0_HINT
    :   DMA device aud spk0 hint

    enumerator DMA_DEV_I2S3
    :   DMA device I2S3

    enumerator DMA_DEV_I2S3_RX
    :   DMA device I2S3 RX

    enumerator DMA_DEV_SPDIF0
    :   DMA device SPDIF0

    enumerator DMA_DEV_SPDIF1
    :   DMA device SPDIF1

    enumerator DMA_DEV_SADC_RX
    :   DMA device SADC RX

    enumerator DMA_DEV_AUD_SPK0_CALL
    :   DMA device aud spk0 call

    enumerator DMA_DEV_AUD_MIC1
    :   DMA device aud mic1

    enumerator DMA_DEV_AUD_SPK1_A2DP
    :   DMA device aud spk1 a2dp

    enumerator DMA_DEV_AUD_SPK1_HINT
    :   DMA device aud spk1 hint dma

    enumerator DMA_DEV_AUD_SPK1_CALL
    :   DMA device aud spk1 call

    enumerator DMA_DEV_GSPI3
    :   DMA device GSPI3

    enumerator DMA_DEV_GSPI3_RX
    :   DMA device GSPI3 RX

    enumerator DMA_DEV_UART5
    :   DMA device UART5

    enumerator DMA_DEV_UART5_RX
    :   DMA device UART5 RX

    enumerator DMA_DEV_I2S4
    :   DMA device I2S4

    enumerator DMA_DEV_I2S4_RX
    :   DMA device I2S4 RX

    enumerator DMA_DEV_XDAC0
    :   DMA device XDAC0

    enumerator DMA_DEV_XDAC1
    :   DMA device XDAC1

    enumerator DMA_DEV_MAX

enum dma_data_width_t
:   *Values:*

    enumerator DMA_DATA_WIDTH_8BITS
    :   DMA data width 8bit

    enumerator DMA_DATA_WIDTH_16BITS
    :   DMA data width 16bit

    enumerator DMA_DATA_WIDTH_32BITS
    :   DMA data width 32bit

enum dma_work_mode_t
:   *Values:*

    enumerator DMA_WORK_MODE_SINGLE
    :   DMA work mode single_mode

    enumerator DMA_WORK_MODE_REPEAT
    :   DMA work mode repeat_mode (forever repeat until software clear dma_en)

enum dma_priority_mode_t
:   *Values:*

    enumerator DMA_PRIO_MODE_ROUND_ROBIN
    :   DMA priority mode round-robin(all dma priority are the same)

    enumerator DMA_PRIO_MODE_FIXED_PRIO
    :   DMA priority mode fixed prio(depend on chan_prio)

enum dma_addr_inc_t
:   *Values:*

    enumerator DMA_ADDR_INC_DISABLE
    :   DMA disable addrress increase

    enumerator DMA_ADDR_INC_ENABLE
    :   DMA enable addrress increase

enum dma_addr_loop_t
:   *Values:*

    enumerator DMA_ADDR_LOOP_DISABLE
    :   DMA disable addrress loop

    enumerator DMA_ADDR_LOOP_ENABLE
    :   DMA enable addrress loop

enum dma_sec_attr_t
:   *Values:*

    enumerator DMA_ATTR_NON_SEC
    :   DMA non-secure attr

    enumerator DMA_ATTR_SEC
    :   DMA secure attr

enum dma_burst_len_t
:   *Values:*

    enumerator BURST_LEN_SINGLE

    enumerator BURST_LEN_INC4

    enumerator BURST_LEN_INC8

    enumerator BURST_LEN_INC16

enum dma_pixel_trans_type_t
:   *Values:*

    enumerator DMA_TRANS_DEFAULT
    :   DMA TRANS DEFAULT

    enumerator DMA_TRANS_RGB_TO_YUV
    :   DMA TRANS RGB_TO_YUV

    enumerator DMA_TRANS_YUV_TO_RGB
    :   DMA TRANS YUV_TO_RGB

    enumerator DMA_TRANS_MAX

enum dma_id_t
:   *Values:*

    enumerator DMA_ID_0
    :   DMA channel 0

    enumerator DMA_ID_1
    :   DMA channel 1

    enumerator DMA_ID_2
    :   DMA channel 2

    enumerator DMA_ID_3
    :   DMA channel 3

    enumerator DMA_ID_4
    :   DMA channel 4

    enumerator DMA_ID_5
    :   DMA channel 5

    enumerator DMA_ID_6
    :   DMA channel 6

    enumerator DMA_ID_7
    :   DMA channel 7

    enumerator DMA_ID_8
    :   DMA channel 8

    enumerator DMA_ID_9
    :   DMA channel 9

    enumerator DMA_ID_10
    :   DMA channel 10

    enumerator DMA_ID_11
    :   DMA channel 11

    enumerator DMA_ID_12
    :   DMA channel 12

    enumerator DMA_ID_13
    :   DMA channel 13

    enumerator DMA_ID_14
    :   DMA channel 14

    enumerator DMA_ID_15
    :   DMA channel 15

    enumerator DMA_ID_MAX
    :   DMA channel max
