---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_dma.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="dma"></a>

# DMA

<a id="dma-api-status"></a>

## DMA API Status

| API | BK7259\_AP |
| --- | --- |
| [`bk_dma_driver_init()`](#_CPPv418bk_dma_driver_initv "bk_dma_driver_init") | Y |
| [`bk_dma_driver_deinit()`](#_CPPv420bk_dma_driver_deinitv "bk_dma_driver_deinit") | Y |
| [`bk_dma_alloc()`](#_CPPv412bk_dma_alloc3u16 "bk_dma_alloc") | Y |
| [`bk_fixed_dma_alloc()`](#_CPPv418bk_fixed_dma_alloc3u168dma_id_t "bk_fixed_dma_alloc") | Y |
| [`bk_dma_free()`](#_CPPv411bk_dma_free3u168dma_id_t "bk_dma_free") | Y |
| [`bk_dma_user()`](#_CPPv411bk_dma_user8dma_id_t "bk_dma_user") | Y |
| [`bk_dma_init()`](#_CPPv411bk_dma_init8dma_id_tPK12dma_config_t "bk_dma_init") | Y |
| [`bk_dma_deinit()`](#_CPPv413bk_dma_deinit8dma_id_t "bk_dma_deinit") | Y |
| [`bk_dma_start()`](#_CPPv412bk_dma_start8dma_id_t "bk_dma_start") | Y |
| [`bk_dma_stop()`](#_CPPv411bk_dma_stop8dma_id_t "bk_dma_stop") | Y |
| [`bk_dma_write()`](#_CPPv412bk_dma_write8dma_id_tPK7uint8_t8uint32_t "bk_dma_write") | Y |
| [`bk_dma_read()`](#_CPPv411bk_dma_read8dma_id_tP7uint8_t8uint32_t "bk_dma_read") | Y |
| [`bk_dma_enable_finish_interrupt()`](#_CPPv430bk_dma_enable_finish_interrupt8dma_id_t "bk_dma_enable_finish_interrupt") | Y |
| [`bk_dma_disable_finish_interrupt()`](#_CPPv431bk_dma_disable_finish_interrupt8dma_id_t "bk_dma_disable_finish_interrupt") | Y |
| [`bk_dma_enable_half_finish_interrupt()`](#_CPPv435bk_dma_enable_half_finish_interrupt8dma_id_t "bk_dma_enable_half_finish_interrupt") | Y |
| [`bk_dma_disable_half_finish_interrupt()`](#_CPPv436bk_dma_disable_half_finish_interrupt8dma_id_t "bk_dma_disable_half_finish_interrupt") | Y |
| [`bk_dma_register_isr()`](#_CPPv419bk_dma_register_isr8dma_id_t9dma_isr_t9dma_isr_t "bk_dma_register_isr") | Y |
| [`bk_dma_register_bus_err_isr()`](#_CPPv427bk_dma_register_bus_err_isr8dma_id_t9dma_isr_t "bk_dma_register_bus_err_isr") | Y |
| [`bk_dma_set_src_addr()`](#_CPPv419bk_dma_set_src_addr8dma_id_t8uint32_t8uint32_t "bk_dma_set_src_addr") | Y |
| [`bk_dma_set_dest_addr()`](#_CPPv420bk_dma_set_dest_addr8dma_id_t8uint32_t8uint32_t "bk_dma_set_dest_addr") | Y |
| [`bk_dma_set_dest_start_addr()`](#_CPPv426bk_dma_set_dest_start_addr8dma_id_t8uint32_t "bk_dma_set_dest_start_addr") | Y |
| [`bk_dma_set_transfer_len()`](#_CPPv423bk_dma_set_transfer_len8dma_id_t8uint32_t "bk_dma_set_transfer_len") | Y |
| [`bk_dma_get_remain_len()`](#_CPPv421bk_dma_get_remain_len8dma_id_t "bk_dma_get_remain_len") | Y |
| [`bk_dma_enable_src_addr_increase()`](#_CPPv431bk_dma_enable_src_addr_increase8dma_id_t "bk_dma_enable_src_addr_increase") | Y |
| [`bk_dma_disable_src_addr_increase()`](#_CPPv432bk_dma_disable_src_addr_increase8dma_id_t "bk_dma_disable_src_addr_increase") | Y |
| [`bk_dma_enable_src_addr_loop()`](#_CPPv427bk_dma_enable_src_addr_loop8dma_id_t "bk_dma_enable_src_addr_loop") | Y |
| [`bk_dma_disable_src_addr_loop()`](#_CPPv428bk_dma_disable_src_addr_loop8dma_id_t "bk_dma_disable_src_addr_loop") | Y |
| [`bk_dma_enable_dest_addr_increase()`](#_CPPv432bk_dma_enable_dest_addr_increase8dma_id_t "bk_dma_enable_dest_addr_increase") | Y |
| [`bk_dma_disable_dest_addr_increase()`](#_CPPv433bk_dma_disable_dest_addr_increase8dma_id_t "bk_dma_disable_dest_addr_increase") | Y |
| [`bk_dma_enable_dest_addr_loop()`](#_CPPv428bk_dma_enable_dest_addr_loop8dma_id_t "bk_dma_enable_dest_addr_loop") | Y |
| [`bk_dma_disable_dest_addr_loop()`](#_CPPv429bk_dma_disable_dest_addr_loop8dma_id_t "bk_dma_disable_dest_addr_loop") | Y |
| [`bk_dma_get_enable_status()`](#_CPPv424bk_dma_get_enable_status8dma_id_t "bk_dma_get_enable_status") | Y |
| [`bk_dma_flush_src_buffer()`](#_CPPv423bk_dma_flush_src_buffer8dma_id_t "bk_dma_flush_src_buffer") | Y |

<a id="dma-channel-number"></a>

## DMA Channel Number

| Capability | BK7259\_AP |
| --- | --- |
| Channel Number | 16 |

<a id="dma-api-reference"></a>

## DMA API Reference

<a id="header-file"></a>

### Header File

- [dma.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/dma.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_dma_driver_initv"></a>

<a id="_CPPv318bk_dma_driver_initv"></a> <a id="_CPPv218bk_dma_driver_initv"></a> <a id="bk_dma_driver_init__void"></a> <a id="dma_8h_1a73b2d9b8bc2ffc0f58ecc31155baaf7a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_driver\_init(void)
:   Init the DMA driver.

    This API init the resoure common to all dma channels:

    - Init dma driver control memory

    This API should be called before any other dma APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_dma_driver_deinitv"></a>

<a id="_CPPv320bk_dma_driver_deinitv"></a> <a id="_CPPv220bk_dma_driver_deinitv"></a> <a id="bk_dma_driver_deinit__void"></a> <a id="dma_8h_1a80d12069cb2caa4e4a7fe22b3db2d8f9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_driver\_deinit(void)
:   Deinit the DMA driver.

    This API free all resource related to dma and power down all dma channels.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv412bk_dma_alloc3u16"></a>

<a id="_CPPv312bk_dma_alloc3u16"></a> <a id="_CPPv212bk_dma_alloc3u16"></a> <a id="bk_dma_alloc__u16"></a> <a id="dma_8h_1abde0b892831794141d591546265049c2"></a> [dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") bk\_dma\_alloc(u16 user\_id)
:   Allocate a DMA channel.

    This API should be called before any other dma channel APIs.

    **Attention**
    :   : This API can only be called in task context,

        - and can’t be called in context that interrupt is disabled.

    参数
    :   **user\_id** – DMA channel applicant

    返回
    :   DMA channel id.

        - \> DMA\_ID\_MAX: no free DMA channel.

<a id="_CPPv418bk_fixed_dma_alloc3u168dma_id_t"></a>

<a id="_CPPv318bk_fixed_dma_alloc3u168dma_id_t"></a> <a id="_CPPv218bk_fixed_dma_alloc3u168dma_id_t"></a> <a id="bk_fixed_dma_alloc__u16.dma_id_t"></a> <a id="dma_8h_1a95e2e52c12c839bee2dc131e59c396e5"></a> [dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") bk\_fixed\_dma\_alloc(u16 user\_id, [dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") fixed\_chnl\_id)
:   Allocate a fixed DMA channel.Maybe some APP needs to have a fixed channel forever, then it can use this API.

    This API should be called before any other dma channel APIs.

    参数
    :   - **user\_id** – DMA channel applicant
        - **fixed\_chnl\_id** – application wants to get which fixed channel

    返回
    :   DMA channel id.

        - \> DMA\_ID\_MAX: if the fixed\_chnl\_id has been allocated, it will return DMA\_ID\_MAX which means error.
        - \> fixed\_chnl\_id: the fixed\_chnl\_id is allocated suc.

<a id="_CPPv411bk_dma_free3u168dma_id_t"></a>

<a id="_CPPv311bk_dma_free3u168dma_id_t"></a> <a id="_CPPv211bk_dma_free3u168dma_id_t"></a> <a id="bk_dma_free__u16.dma_id_t"></a> <a id="dma_8h_1a853b26fe303ecb50e2036b3e45de7ece"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_free(u16 user\_id, [dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Free the DMA channel.

    **Attention**
    :   : This API can only be called in task context,

        - and can’t be called in context that interrupt is disabled.

    参数
    :   - **user\_id** – DMA channel applicant, the same as in bk\_dma\_alloc.
        - **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_dma_user8dma_id_t"></a>

<a id="_CPPv311bk_dma_user8dma_id_t"></a> <a id="_CPPv211bk_dma_user8dma_id_t"></a> <a id="bk_dma_user__dma_id_t"></a> <a id="dma_8h_1a0d03bf702fe84f0bab68fbce3195569d"></a> uint32\_t bk\_dma\_user([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   get the user of DMA channel

    参数
    :   **id** – DMA channel

    返回
    :   DMA channel user\_id.

        - u32: high u16 is the CPU\_ID, low 16 bits is the applicant\_id.

<a id="_CPPv411bk_dma_init8dma_id_tPK12dma_config_t"></a>

<a id="_CPPv311bk_dma_init8dma_id_tPK12dma_config_t"></a> <a id="_CPPv211bk_dma_init8dma_id_tPK12dma_config_t"></a> <a id="bk_dma_init__dma_id_t.dma_config_tCP"></a> <a id="dma_8h_1a376d9a3e80dae84a1152e997115f960f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_init([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, const [dma\_config\_t](#_CPPv412dma_config_t "dma_config_t") \*config)
:   Init the DMA channel.

    **Attention**
    :   1\. the higher channel priority value, the higher the priority

    参数
    :   - **id** – DMA channel
        - **config** – DMA configuration

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_DMA\_NOT\_INIT: DMA driver not init
        - BK\_ERR\_NULL\_PARAM: config is NULL
        - BK\_ERR\_DMA\_ID: invalid DMA channel
        - BK\_ERR\_DMA\_INVALID\_ADDR: invalid DMA address
        - others: other errors.

<a id="_CPPv413bk_dma_deinit8dma_id_t"></a>

<a id="_CPPv313bk_dma_deinit8dma_id_t"></a> <a id="_CPPv213bk_dma_deinit8dma_id_t"></a> <a id="bk_dma_deinit__dma_id_t"></a> <a id="dma_8h_1a0c8faae79624cbc99e9c55fc881925c9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_deinit([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Deinit a DMA channel.

    This API deinit the DMA channel:

    - Stop the DMA channel
    - Reset all configuration of DMA channel to default value

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv412bk_dma_start8dma_id_t"></a>

<a id="_CPPv312bk_dma_start8dma_id_t"></a> <a id="_CPPv212bk_dma_start8dma_id_t"></a> <a id="bk_dma_start__dma_id_t"></a> <a id="dma_8h_1aa6a1606f8ff5984db237fc8b34db5cde"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_start([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Start a DMA channel.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_dma_stop8dma_id_t"></a>

<a id="_CPPv311bk_dma_stop8dma_id_t"></a> <a id="_CPPv211bk_dma_stop8dma_id_t"></a> <a id="bk_dma_stop__dma_id_t"></a> <a id="dma_8h_1a5ccb3ecdcbd33fa05782cc1166ef60cf"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_stop([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Stop a DMA channel.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv412bk_dma_write8dma_id_tPK7uint8_t8uint32_t"></a>

<a id="_CPPv312bk_dma_write8dma_id_tPK7uint8_t8uint32_t"></a> <a id="_CPPv212bk_dma_write8dma_id_tPK7uint8_t8uint32_t"></a> <a id="bk_dma_write__dma_id_t.uint8_tCP.uint32_t"></a> <a id="dma_8h_1a3ad2cce0dec4040397e056c8531a933b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_write([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, const uint8\_t \*data, uint32\_t size)
:   Transfer data from memory to peripheral.

    参数
    :   - **id** – DMA channel
        - **data** – DMA transfer data
        - **size** – data size

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_dma_read8dma_id_tP7uint8_t8uint32_t"></a>

<a id="_CPPv311bk_dma_read8dma_id_tP7uint8_t8uint32_t"></a> <a id="_CPPv211bk_dma_read8dma_id_tP7uint8_t8uint32_t"></a> <a id="bk_dma_read__dma_id_t.uint8_tP.uint32_t"></a> <a id="dma_8h_1add6ed3b997cf88979d806fb43088b8d5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_read([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, uint8\_t \*data, uint32\_t size)
:   Transfer data from peripheral to memory.

    参数
    :   - **id** – DMA channel
        - **data** – DMA transfer data
        - **size** – data size

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv430bk_dma_enable_finish_interrupt8dma_id_t"></a>

<a id="_CPPv330bk_dma_enable_finish_interrupt8dma_id_t"></a> <a id="_CPPv230bk_dma_enable_finish_interrupt8dma_id_t"></a> <a id="bk_dma_enable_finish_interrupt__dma_id_t"></a> <a id="dma_8h_1a4daac7f221a2dcf83eeafc6fbfcd72a7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_enable\_finish\_interrupt([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA finish intterrup.

    @NOTES before enable interrupt, please confirm have called bk\_dma\_register\_isr.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv431bk_dma_disable_finish_interrupt8dma_id_t"></a>

<a id="_CPPv331bk_dma_disable_finish_interrupt8dma_id_t"></a> <a id="_CPPv231bk_dma_disable_finish_interrupt8dma_id_t"></a> <a id="bk_dma_disable_finish_interrupt__dma_id_t"></a> <a id="dma_8h_1a3b3ac562a3a82c5459ba24c7cc6a07d1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_disable\_finish\_interrupt([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA finish intterrup.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv435bk_dma_enable_half_finish_interrupt8dma_id_t"></a>

<a id="_CPPv335bk_dma_enable_half_finish_interrupt8dma_id_t"></a> <a id="_CPPv235bk_dma_enable_half_finish_interrupt8dma_id_t"></a> <a id="bk_dma_enable_half_finish_interrupt__dma_id_t"></a> <a id="dma_8h_1a4f2e0ba07755655b91dcf5697a8ace86"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_enable\_half\_finish\_interrupt([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA half finish intterrup.

    @NOTES before enable interrupt, please confirm have called bk\_dma\_register\_isr.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv436bk_dma_disable_half_finish_interrupt8dma_id_t"></a>

<a id="_CPPv336bk_dma_disable_half_finish_interrupt8dma_id_t"></a> <a id="_CPPv236bk_dma_disable_half_finish_interrupt8dma_id_t"></a> <a id="bk_dma_disable_half_finish_interrupt__dma_id_t"></a> <a id="dma_8h_1ab45d98b1e096263d5bd3dd74386b9062"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_disable\_half\_finish\_interrupt([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA half finish intterrup.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_dma_register_isr8dma_id_t9dma_isr_t9dma_isr_t"></a>

<a id="_CPPv319bk_dma_register_isr8dma_id_t9dma_isr_t9dma_isr_t"></a> <a id="_CPPv219bk_dma_register_isr8dma_id_t9dma_isr_t9dma_isr_t"></a> <a id="bk_dma_register_isr__dma_id_t.dma_isr_t.dma_isr_t"></a> <a id="dma_8h_1a20e473bb6de815ce031aa24647992074"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_register\_isr([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, [dma\_isr\_t](#_CPPv49dma_isr_t "dma_isr_t") half\_finish\_isr, [dma\_isr\_t](#_CPPv49dma_isr_t "dma_isr_t") finish\_isr)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel
        - **half\_finish\_isr** – DMA half finish callback
        - **finish\_isr** – DMA finish callback

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_dma_register_bus_err_isr8dma_id_t9dma_isr_t"></a>

<a id="_CPPv327bk_dma_register_bus_err_isr8dma_id_t9dma_isr_t"></a> <a id="_CPPv227bk_dma_register_bus_err_isr8dma_id_t9dma_isr_t"></a> <a id="bk_dma_register_bus_err_isr__dma_id_t.dma_isr_t"></a> <a id="dma_8h_1afb6c6560e7f2c50cdd6fa235498f0c7e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_register\_bus\_err\_isr([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, [dma\_isr\_t](#_CPPv49dma_isr_t "dma_isr_t") bus\_err\_isr)
:   Register the interrupt service routine for DMA channel.

    This API regist dma error isr callback function.

    参数
    :   - **id** – DMA channel
        - **bus\_err\_isr** – DMA bus error callback

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_dma_register_isr_arg8dma_id_tP17dma_isr_arg_reg_t"></a>

<a id="_CPPv323bk_dma_register_isr_arg8dma_id_tP17dma_isr_arg_reg_t"></a> <a id="_CPPv223bk_dma_register_isr_arg8dma_id_tP17dma_isr_arg_reg_t"></a> <a id="bk_dma_register_isr_arg__dma_id_t.dma_isr_arg_reg_tP"></a> <a id="dma_8h_1a6e2867f50db500d8bf57814b36149c5e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_register\_isr\_arg([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, [dma\_isr\_arg\_reg\_t](#_CPPv417dma_isr_arg_reg_t "dma_isr_arg_reg_t") \*dma\_arg\_isr)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel
        - **dma\_arg\_isr** – DMA half finish, finish, bus error callback and pointer variable

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv435bk_dma_register_half_finish_isr_arg8dma_id_t13dma_isr_arg_tPv"></a>

<a id="_CPPv335bk_dma_register_half_finish_isr_arg8dma_id_t13dma_isr_arg_tPv"></a> <a id="_CPPv235bk_dma_register_half_finish_isr_arg8dma_id_t13dma_isr_arg_tPv"></a> <a id="bk_dma_register_half_finish_isr_arg__dma_id_t.dma_isr_arg_t.voidP"></a> <a id="dma_8h_1a7777072470c82183f955daf672a71171"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_register\_half\_finish\_isr\_arg([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, [dma\_isr\_arg\_t](#_CPPv413dma_isr_arg_t "dma_isr_arg_t") half\_finish\_isr, void \*arg)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel
        - **dma\_arg\_isr** – DMA half finish callback and pointer variable

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv430bk_dma_register_finish_isr_arg8dma_id_t13dma_isr_arg_tPv"></a>

<a id="_CPPv330bk_dma_register_finish_isr_arg8dma_id_t13dma_isr_arg_tPv"></a> <a id="_CPPv230bk_dma_register_finish_isr_arg8dma_id_t13dma_isr_arg_tPv"></a> <a id="bk_dma_register_finish_isr_arg__dma_id_t.dma_isr_arg_t.voidP"></a> <a id="dma_8h_1add64feae4b3939608da154e11aa3bf78"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_register\_finish\_isr\_arg([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, [dma\_isr\_arg\_t](#_CPPv413dma_isr_arg_t "dma_isr_arg_t") finish\_isr, void \*arg)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel
        - **dma\_arg\_isr** – DMA finish callback and pointer variable

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv431bk_dma_register_bus_err_isr_arg8dma_id_t13dma_isr_arg_tPv"></a>

<a id="_CPPv331bk_dma_register_bus_err_isr_arg8dma_id_t13dma_isr_arg_tPv"></a> <a id="_CPPv231bk_dma_register_bus_err_isr_arg8dma_id_t13dma_isr_arg_tPv"></a> <a id="bk_dma_register_bus_err_isr_arg__dma_id_t.dma_isr_arg_t.voidP"></a> <a id="dma_8h_1a62e8caa102c82fb2c242e1b52248176e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_register\_bus\_err\_isr\_arg([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, [dma\_isr\_arg\_t](#_CPPv413dma_isr_arg_t "dma_isr_arg_t") bus\_err\_isr, void \*arg)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function.

    参数
    :   - **id** – DMA channel
        - **dma\_arg\_isr** – DMA bus error callback and pointer variable

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_dma_get_transfer_len_max8dma_id_t"></a>

<a id="_CPPv327bk_dma_get_transfer_len_max8dma_id_t"></a> <a id="_CPPv227bk_dma_get_transfer_len_max8dma_id_t"></a> <a id="bk_dma_get_transfer_len_max__dma_id_t"></a> <a id="dma_8h_1ae16b21c969d4252fb6308e848553b6f9"></a> uint32\_t bk\_dma\_get\_transfer\_len\_max([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   get DMA transfer max length in one round, default value is 65536 bytes.

    参数
    :   **id** – DMA channel

    返回
    :   - max len: how many bytes can be copy by DMA in one round.

<a id="_CPPv423bk_dma_set_transfer_len8dma_id_t8uint32_t"></a>

<a id="_CPPv323bk_dma_set_transfer_len8dma_id_t8uint32_t"></a> <a id="_CPPv223bk_dma_set_transfer_len8dma_id_t8uint32_t"></a> <a id="bk_dma_set_transfer_len__dma_id_t.uint32_t"></a> <a id="dma_8h_1a118e528f09d01587dcfcbe59c0b667fe"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_set\_transfer\_len([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, uint32\_t tran\_len)
:   Set DMA transfer length.

    参数
    :   - **id** – DMA channel
        - **tran\_len** – DMA transfer length, the tran\_len should be \<\= bk\_dma\_get\_transfer\_len\_max() bytes.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_dma_set_src_addr8dma_id_t8uint32_t8uint32_t"></a>

<a id="_CPPv319bk_dma_set_src_addr8dma_id_t8uint32_t8uint32_t"></a> <a id="_CPPv219bk_dma_set_src_addr8dma_id_t8uint32_t8uint32_t"></a> <a id="bk_dma_set_src_addr__dma_id_t.uint32_t.uint32_t"></a> <a id="dma_8h_1a0f5a03f0f26e3f9ad7919049e9790da3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_set\_src\_addr([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, uint32\_t start\_addr, uint32\_t end\_addr)
:   Set DMA source address.

    **Attention**
    :   1\. address should be zero when there is no value, e.g. bk\_dma\_set\_src\_addr(1, 0x80210C, 0\)

    参数
    :   - **id** – DMA channel
        - **start\_addr** – DMA source start address
        - **end\_addr** – DMA source end address

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_dma_set_src_start_addr8dma_id_t8uint32_t"></a>

<a id="_CPPv325bk_dma_set_src_start_addr8dma_id_t8uint32_t"></a> <a id="_CPPv225bk_dma_set_src_start_addr8dma_id_t8uint32_t"></a> <a id="bk_dma_set_src_start_addr__dma_id_t.uint32_t"></a> <a id="dma_8h_1a7290d18c07625b277dfac24de7771512"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_set\_src\_start\_addr([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, uint32\_t start\_addr)
:   Set DMA source start address.

    参数
    :   - **id** – DMA channel
        - **start\_addr** – DMA source start address

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_dma_set_dest_addr8dma_id_t8uint32_t8uint32_t"></a>

<a id="_CPPv320bk_dma_set_dest_addr8dma_id_t8uint32_t8uint32_t"></a> <a id="_CPPv220bk_dma_set_dest_addr8dma_id_t8uint32_t8uint32_t"></a> <a id="bk_dma_set_dest_addr__dma_id_t.uint32_t.uint32_t"></a> <a id="dma_8h_1a298de6f08997dea0576e81eae1c2c102"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_set\_dest\_addr([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, uint32\_t start\_addr, uint32\_t end\_addr)
:   Set DMA dest address.

    **Attention**
    :   1\. address should be zero when there is no value, e.g. bk\_dma\_set\_dest\_addr(1, 0x80210C, 0\)

    参数
    :   - **id** – DMA channel
        - **start\_addr** – DMA dest start address
        - **end\_addr** – DMA dest end address

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_dma_set_dest_start_addr8dma_id_t8uint32_t"></a>

<a id="_CPPv326bk_dma_set_dest_start_addr8dma_id_t8uint32_t"></a> <a id="_CPPv226bk_dma_set_dest_start_addr8dma_id_t8uint32_t"></a> <a id="bk_dma_set_dest_start_addr__dma_id_t.uint32_t"></a> <a id="dma_8h_1afa31ad5ed8f44ca27dc1d0506843cb48"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_set\_dest\_start\_addr([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id, uint32\_t start\_addr)
:   Set DMA dest start address.

    参数
    :   - **id** – DMA channel
        - **start\_addr** – DMA dest start address

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv431bk_dma_enable_src_addr_increase8dma_id_t"></a>

<a id="_CPPv331bk_dma_enable_src_addr_increase8dma_id_t"></a> <a id="_CPPv231bk_dma_enable_src_addr_increase8dma_id_t"></a> <a id="bk_dma_enable_src_addr_increase__dma_id_t"></a> <a id="dma_8h_1a9fdce512c415977373bde7e6962e3ff1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_enable\_src\_addr\_increase([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA source address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv432bk_dma_disable_src_addr_increase8dma_id_t"></a>

<a id="_CPPv332bk_dma_disable_src_addr_increase8dma_id_t"></a> <a id="_CPPv232bk_dma_disable_src_addr_increase8dma_id_t"></a> <a id="bk_dma_disable_src_addr_increase__dma_id_t"></a> <a id="dma_8h_1a42e084adc21c26df39807376f438e0a1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_disable\_src\_addr\_increase([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA source address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_dma_enable_src_addr_loop8dma_id_t"></a>

<a id="_CPPv327bk_dma_enable_src_addr_loop8dma_id_t"></a> <a id="_CPPv227bk_dma_enable_src_addr_loop8dma_id_t"></a> <a id="bk_dma_enable_src_addr_loop__dma_id_t"></a> <a id="dma_8h_1a4dc7e313f407ecbe1f7a811ef5e6cda1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_enable\_src\_addr\_loop([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA source address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv428bk_dma_disable_src_addr_loop8dma_id_t"></a>

<a id="_CPPv328bk_dma_disable_src_addr_loop8dma_id_t"></a> <a id="_CPPv228bk_dma_disable_src_addr_loop8dma_id_t"></a> <a id="bk_dma_disable_src_addr_loop__dma_id_t"></a> <a id="dma_8h_1a91f403004c4097936bcd1fdde183525b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_disable\_src\_addr\_loop([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA source address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv432bk_dma_enable_dest_addr_increase8dma_id_t"></a>

<a id="_CPPv332bk_dma_enable_dest_addr_increase8dma_id_t"></a> <a id="_CPPv232bk_dma_enable_dest_addr_increase8dma_id_t"></a> <a id="bk_dma_enable_dest_addr_increase__dma_id_t"></a> <a id="dma_8h_1a5c717db94762a6f1bfbdb8511701c29a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_enable\_dest\_addr\_increase([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA dest address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv433bk_dma_disable_dest_addr_increase8dma_id_t"></a>

<a id="_CPPv333bk_dma_disable_dest_addr_increase8dma_id_t"></a> <a id="_CPPv233bk_dma_disable_dest_addr_increase8dma_id_t"></a> <a id="bk_dma_disable_dest_addr_increase__dma_id_t"></a> <a id="dma_8h_1a587ad797d2627e4475dc66c2082e59b2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_disable\_dest\_addr\_increase([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA dest address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv428bk_dma_enable_dest_addr_loop8dma_id_t"></a>

<a id="_CPPv328bk_dma_enable_dest_addr_loop8dma_id_t"></a> <a id="_CPPv228bk_dma_enable_dest_addr_loop8dma_id_t"></a> <a id="bk_dma_enable_dest_addr_loop__dma_id_t"></a> <a id="dma_8h_1af2fbaaf1f18d9842680d3510e6c01fa4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_enable\_dest\_addr\_loop([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Enable DMA dest address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv429bk_dma_disable_dest_addr_loop8dma_id_t"></a>

<a id="_CPPv329bk_dma_disable_dest_addr_loop8dma_id_t"></a> <a id="_CPPv229bk_dma_disable_dest_addr_loop8dma_id_t"></a> <a id="bk_dma_disable_dest_addr_loop__dma_id_t"></a> <a id="dma_8h_1a1e34578a5f3c89961476d1ab1dcaced5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_disable\_dest\_addr\_loop([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Disable DMA dest address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_dma_get_remain_len8dma_id_t"></a>

<a id="_CPPv321bk_dma_get_remain_len8dma_id_t"></a> <a id="_CPPv221bk_dma_get_remain_len8dma_id_t"></a> <a id="bk_dma_get_remain_len__dma_id_t"></a> <a id="dma_8h_1aceadc57e8f0f338e7832832a096102e5"></a> uint32\_t bk\_dma\_get\_remain\_len([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Get DMA transfer remain length.

    参数
    :   **id** – DMA channel

    返回
    :   DMA transfer remain length

<a id="_CPPv424bk_dma_get_enable_status8dma_id_t"></a>

<a id="_CPPv324bk_dma_get_enable_status8dma_id_t"></a> <a id="_CPPv224bk_dma_get_enable_status8dma_id_t"></a> <a id="bk_dma_get_enable_status__dma_id_t"></a> <a id="dma_8h_1a084d1d2afb3976ea82fbeee12868f4ed"></a> uint32\_t bk\_dma\_get\_enable\_status([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   Gets the current DMA channel working status.

    参数
    :   **id** – DMA channel

    返回
    :   - 0: Channel idle state
        - others: Channel busy state.

<a id="_CPPv423bk_dma_check_chn_statusv"></a>

<a id="_CPPv323bk_dma_check_chn_statusv"></a> <a id="_CPPv223bk_dma_check_chn_statusv"></a> <a id="bk_dma_check_chn_status__void"></a> <a id="dma_8h_1a6b69693f5ee1cac53331717b17ef813e"></a> uint32\_t bk\_dma\_check\_chn\_status(void)
:   Get the working status of all DMA channels.

    参数
    :   **NULL** –

    返回
    :   - 0: All channels are in an idle state
        - others: Channel busy state, one bit per channel.

<a id="_CPPv423bk_dma_flush_src_buffer8dma_id_t"></a>

<a id="_CPPv323bk_dma_flush_src_buffer8dma_id_t"></a> <a id="_CPPv223bk_dma_flush_src_buffer8dma_id_t"></a> <a id="bk_dma_flush_src_buffer__dma_id_t"></a> <a id="dma_8h_1a7e95b713bd0f87f2316278acb8cedef0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_dma\_flush\_src\_buffer([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") id)
:   flush reserved data in dma internal buffer I.E:If source data width is not 4bytes, and data size isn’t 4bytes align, but dest data width is 4bytes, then maybe 1\~3 bytes data reserved in dma internal buffer, then the left 1\~3 bytes data not copy to dest address.

    参数
    :   - **id** – DMA channel
        - **attr** – DMA privileged attr

    返回
    :   - 0: Channel idle state
        - others: Channel busy state.

<a id="dma-api-typedefs"></a>

## DMA API Typedefs

<a id="id1"></a>

### Header File

- [dma\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/dma_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv417dma_isr_arg_reg_t"></a>

<a id="_CPPv317dma_isr_arg_reg_t"></a> <a id="_CPPv217dma_isr_arg_reg_t"></a> <a id="dma_isr_arg_reg_t"></a> <a id="structdma__isr__arg__reg__t"></a> struct dma\_isr\_arg\_reg\_t

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_DMA_ID"></a>

<a id="group__bk__api__dma__defs_1gabde540598cd0e94bfedc7810a232134d"></a> BK\_ERR\_DMA\_ID
:   DMA id is invalid

<a id="c.BK_ERR_DMA_NOT_INIT"></a>

<a id="group__bk__api__dma__defs_1ga741468df8c6769fd7c5ba37d26ee559b"></a> BK\_ERR\_DMA\_NOT\_INIT
:   DMA driver not init

<a id="c.BK_ERR_DMA_ID_NOT_INIT"></a>

<a id="group__bk__api__dma__defs_1ga6c03555b8a404d8ce02cb12859bb7c07"></a> BK\_ERR\_DMA\_ID\_NOT\_INIT
:   DMA id not init

<a id="c.BK_ERR_DMA_ID_NOT_START"></a>

<a id="group__bk__api__dma__defs_1ga23e4008047e33ed2793dbb9eca37dbe6"></a> BK\_ERR\_DMA\_ID\_NOT\_START
:   DMA id not start

<a id="c.BK_ERR_DMA_INVALID_ADDR"></a>

<a id="group__bk__api__dma__defs_1gaded3d1be577b4a639e303e48dd36fb6d"></a> BK\_ERR\_DMA\_INVALID\_ADDR
:   DMA addr is invalid

<a id="c.BK_ERR_DMA_ID_REINIT"></a>

<a id="group__bk__api__dma__defs_1gaec3985c2a3490fb8a36ad06f01554a68"></a> BK\_ERR\_DMA\_ID\_REINIT
:   DMA id has inited, if reinit,please de-init firstly

<a id="c.BK_ERR_DMA_TRANS_LEN"></a>

<a id="group__bk__api__dma__defs_1ga8cc20ca2a5567bc6463007909485cd32"></a> BK\_ERR\_DMA\_TRANS\_LEN
:   DMA trans len is invalid

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv49dma_isr_t"></a>

<a id="_CPPv39dma_isr_t"></a> <a id="_CPPv29dma_isr_t"></a> <a id="dma_isr_t"></a> <a id="group__bk__api__dma__defs_1gaf563ac76d128050addca3a5dbb85442c"></a> typedef void (\*dma\_isr\_t)([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") dma\_id)
:   DMA interrupt service routine.

<a id="_CPPv413dma_isr_arg_t"></a>

<a id="_CPPv313dma_isr_arg_t"></a> <a id="_CPPv213dma_isr_arg_t"></a> <a id="dma_isr_arg_t"></a> <a id="group__bk__api__dma__defs_1gadc156f97276356ead152cb7847d0bca0"></a> typedef void (\*dma\_isr\_arg\_t)([dma\_id\_t](#_CPPv48dma_id_t "dma_id_t") dma\_id, void \*arg)

<a id="id2"></a>

### Header File

- [hal\_dma\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_dma_types.h)

<a id="id3"></a>

### Structures

<a id="_CPPv417dma_port_config_t"></a>

<a id="_CPPv317dma_port_config_t"></a> <a id="_CPPv217dma_port_config_t"></a> <a id="dma_port_config_t"></a> <a id="structdma__port__config__t"></a> struct dma\_port\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17dma_port_config_t3devE"></a>

    <a id="_CPPv3N17dma_port_config_t3devE"></a> <a id="_CPPv2N17dma_port_config_t3devE"></a> <a id="dma_port_config_t::dev__dma_dev_t"></a> <a id="group__bk__api__dma__enum_1ga2d151c40ad4b09e9f4044e7019cff511"></a> [dma\_dev\_t](#_CPPv49dma_dev_t "dma_dev_t") dev
    :   DMA device

    <a id="_CPPv4N17dma_port_config_t5widthE"></a>

    <a id="_CPPv3N17dma_port_config_t5widthE"></a> <a id="_CPPv2N17dma_port_config_t5widthE"></a> <a id="dma_port_config_t::width__dma_data_width_t"></a> <a id="group__bk__api__dma__enum_1ga74f9720cda31abcfedcfcbcf993dc004"></a> [dma\_data\_width\_t](#_CPPv416dma_data_width_t "dma_data_width_t") width
    :   DMA data width

    <a id="_CPPv4N17dma_port_config_t11addr_inc_enE"></a>

    <a id="_CPPv3N17dma_port_config_t11addr_inc_enE"></a> <a id="_CPPv2N17dma_port_config_t11addr_inc_enE"></a> <a id="dma_port_config_t::addr_inc_en__dma_addr_inc_t"></a> <a id="group__bk__api__dma__enum_1ga399d6c0777cc51a860ab10eb5032872d"></a> [dma\_addr\_inc\_t](#_CPPv414dma_addr_inc_t "dma_addr_inc_t") addr\_inc\_en
    :   enable/disable DMA address increase

    <a id="_CPPv4N17dma_port_config_t12addr_loop_enE"></a>

    <a id="_CPPv3N17dma_port_config_t12addr_loop_enE"></a> <a id="_CPPv2N17dma_port_config_t12addr_loop_enE"></a> <a id="dma_port_config_t::addr_loop_en__dma_addr_loop_t"></a> <a id="group__bk__api__dma__enum_1ga3a3f759e6f7906aea488a5378e258d95"></a> [dma\_addr\_loop\_t](#_CPPv415dma_addr_loop_t "dma_addr_loop_t") addr\_loop\_en
    :   enable/disable DMA address loop

    <a id="_CPPv4N17dma_port_config_t10start_addrE"></a>

    <a id="_CPPv3N17dma_port_config_t10start_addrE"></a> <a id="_CPPv2N17dma_port_config_t10start_addrE"></a> <a id="dma_port_config_t::start_addr__uint32_t"></a> <a id="group__bk__api__dma__enum_1gaa393df69843b1cf3b5bc14fa7c460170"></a> uint32\_t start\_addr
    :   DMA start address

    <a id="_CPPv4N17dma_port_config_t8end_addrE"></a>

    <a id="_CPPv3N17dma_port_config_t8end_addrE"></a> <a id="_CPPv2N17dma_port_config_t8end_addrE"></a> <a id="dma_port_config_t::end_addr__uint32_t"></a> <a id="group__bk__api__dma__enum_1gad2e5d521a99c5554058c38687e506357"></a> uint32\_t end\_addr
    :   DMA end address

<a id="_CPPv412dma_config_t"></a>

<a id="_CPPv312dma_config_t"></a> <a id="_CPPv212dma_config_t"></a> <a id="dma_config_t"></a> <a id="structdma__config__t"></a> struct dma\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12dma_config_t4modeE"></a>

    <a id="_CPPv3N12dma_config_t4modeE"></a> <a id="_CPPv2N12dma_config_t4modeE"></a> <a id="dma_config_t::mode__dma_work_mode_t"></a> <a id="group__bk__api__dma__enum_1ga4b299469e6677532bdd027cef59741bf"></a> [dma\_work\_mode\_t](#_CPPv415dma_work_mode_t "dma_work_mode_t") mode
    :   DMA work mode

    <a id="_CPPv4N12dma_config_t9chan_prioE"></a>

    <a id="_CPPv3N12dma_config_t9chan_prioE"></a> <a id="_CPPv2N12dma_config_t9chan_prioE"></a> <a id="dma_config_t::chan_prio__dma_chan_priority_t"></a> <a id="group__bk__api__dma__enum_1ga80e788c71475fb8ee741dd456012c028"></a> [dma\_chan\_priority\_t](#_CPPv419dma_chan_priority_t "dma_chan_priority_t") chan\_prio
    :   DMA channel prioprity

    <a id="_CPPv4N12dma_config_t3srcE"></a>

    <a id="_CPPv3N12dma_config_t3srcE"></a> <a id="_CPPv2N12dma_config_t3srcE"></a> <a id="dma_config_t::src__dma_port_config_t"></a> <a id="group__bk__api__dma__enum_1gad828944ee7a7ab0e929b7a80b3caf260"></a> [dma\_port\_config\_t](#_CPPv417dma_port_config_t "dma_port_config_t") src
    :   DMA source configuration

    <a id="_CPPv4N12dma_config_t3dstE"></a>

    <a id="_CPPv3N12dma_config_t3dstE"></a> <a id="_CPPv2N12dma_config_t3dstE"></a> <a id="dma_config_t::dst__dma_port_config_t"></a> <a id="group__bk__api__dma__enum_1ga89edcc05c0952f53efb5cf68a2aa4669"></a> [dma\_port\_config\_t](#_CPPv417dma_port_config_t "dma_port_config_t") dst
    :   DMA dest configuration

    <a id="_CPPv4N12dma_config_t10trans_typeE"></a>

    <a id="_CPPv3N12dma_config_t10trans_typeE"></a> <a id="_CPPv2N12dma_config_t10trans_typeE"></a> <a id="dma_config_t::trans_type__dma_pixel_trans_type_t"></a> <a id="group__bk__api__dma__enum_1ga81f448cbbd53d604b5992824d5024408"></a> [dma\_pixel\_trans\_type\_t](#_CPPv422dma_pixel_trans_type_t "dma_pixel_trans_type_t") trans\_type
    :   DMA TRANS TYPE

    <a id="_CPPv4N12dma_config_t13dest_wr_intlvE"></a>

    <a id="_CPPv3N12dma_config_t13dest_wr_intlvE"></a> <a id="_CPPv2N12dma_config_t13dest_wr_intlvE"></a> <a id="dma_config_t::dest_wr_intlv__uint32_t"></a> <a id="group__bk__api__dma__enum_1gab9aec1ee68129cf4c6732cc54065332b"></a> uint32\_t dest\_wr\_intlv
    :   DMA Destination Write operate interval.unit is cycle

    <a id="_CPPv4N12dma_config_t12src_rd_intlvE"></a>

    <a id="_CPPv3N12dma_config_t12src_rd_intlvE"></a> <a id="_CPPv2N12dma_config_t12src_rd_intlvE"></a> <a id="dma_config_t::src_rd_intlv__uint32_t"></a> <a id="group__bk__api__dma__enum_1ga2cee5e02c91aa930d576bc440eefca3d"></a> uint32\_t src\_rd\_intlv
    :   DMA Source Read operate interval.unit is cycle

<a id="id4"></a>

### Macros

<a id="c.BK_ERR_DMA_HAL_INVALID_ADDR"></a>

<a id="hal__dma__types_8h_1acf2d38c9e2f04288b5af01b22ba054d1"></a> BK\_ERR\_DMA\_HAL\_INVALID\_ADDR

<a id="id5"></a>

### Type Definitions

<a id="_CPPv410dma_unit_t"></a>

<a id="_CPPv310dma_unit_t"></a> <a id="_CPPv210dma_unit_t"></a> <a id="dma_unit_t"></a> <a id="group__bk__api__dma__defs_1ga6f1d4fb862ac3fcc87d007f9ccb93529"></a> typedef uint8\_t dma\_unit\_t
:   DMA uint id

<a id="_CPPv419dma_chan_priority_t"></a>

<a id="_CPPv319dma_chan_priority_t"></a> <a id="_CPPv219dma_chan_priority_t"></a> <a id="dma_chan_priority_t"></a> <a id="group__bk__api__dma__defs_1gaadc06af6c251d6f37f93f7c207a45a3b"></a> typedef uint8\_t dma\_chan\_priority\_t
:   DMA channel priority:the value is higher then the priority is higher

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv412dma_int_id_t"></a>

<a id="_CPPv312dma_int_id_t"></a> <a id="_CPPv212dma_int_id_t"></a> <a id="group__bk__api__dma__enum_1ga44c44475b6aaa58dac44d169c7041dd7"></a> enum dma\_int\_id\_t
:   CPU core for DMA Interrupt Differentiation Notification.

    @Enumeration option selection core notifies DMA to interrupt after completion of transport

    @Notification of terminal selection based on channel operation

    *Values:*

    <a id="_CPPv4N12dma_int_id_t9DMA_INT_0E"></a>

    <a id="_CPPv3N12dma_int_id_t9DMA_INT_0E"></a> <a id="_CPPv2N12dma_int_id_t9DMA_INT_0E"></a> <a id="group__bk__api__dma__enum_1gga44c44475b6aaa58dac44d169c7041dd7a382ea13e85da049e9e2f22f22793de9d"></a> enumerator DMA\_INT\_0
    :   DMA INT 0

    <a id="_CPPv4N12dma_int_id_t9DMA_INT_1E"></a>

    <a id="_CPPv3N12dma_int_id_t9DMA_INT_1E"></a> <a id="_CPPv2N12dma_int_id_t9DMA_INT_1E"></a> <a id="group__bk__api__dma__enum_1gga44c44475b6aaa58dac44d169c7041dd7a81f6b30c1dd00627598a6cefedc28ea7"></a> enumerator DMA\_INT\_1
    :   DMA INT 1

    <a id="_CPPv4N12dma_int_id_t9DMA_INT_2E"></a>

    <a id="_CPPv3N12dma_int_id_t9DMA_INT_2E"></a> <a id="_CPPv2N12dma_int_id_t9DMA_INT_2E"></a> <a id="group__bk__api__dma__enum_1gga44c44475b6aaa58dac44d169c7041dd7a112eabae14d5cf804a5884a306368088"></a> enumerator DMA\_INT\_2
    :   DMA INT 2

    <a id="_CPPv4N12dma_int_id_t9DMA_INT_3E"></a>

    <a id="_CPPv3N12dma_int_id_t9DMA_INT_3E"></a> <a id="_CPPv2N12dma_int_id_t9DMA_INT_3E"></a> <a id="group__bk__api__dma__enum_1gga44c44475b6aaa58dac44d169c7041dd7ad1adccb91c8363982d23076f5e23a073"></a> enumerator DMA\_INT\_3
    :   DMA INT 3

    <a id="_CPPv4N12dma_int_id_t11DMA_INT_MAXE"></a>

    <a id="_CPPv3N12dma_int_id_t11DMA_INT_MAXE"></a> <a id="_CPPv2N12dma_int_id_t11DMA_INT_MAXE"></a> <a id="group__bk__api__dma__enum_1gga44c44475b6aaa58dac44d169c7041dd7a9463bdac144c2ff9fa5680d566b0d82e"></a> enumerator DMA\_INT\_MAX
    :   DMA channel max

<a id="_CPPv49dma_dev_t"></a>

<a id="_CPPv39dma_dev_t"></a> <a id="_CPPv29dma_dev_t"></a> <a id="group__bk__api__dma__enum_1ga5db3db1227343b84183a0e7a23b8a201"></a> enum dma\_dev\_t
:   *Values:*

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_DTCME"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_DTCME"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_DTCME"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a1fb04c4ac69108a2df864cb08fb1aa14"></a> enumerator DMA\_DEV\_DTCM
    :   DMA device DTCM

    <a id="_CPPv4N9dma_dev_t10DMA_DEV_LAE"></a>

    <a id="_CPPv3N9dma_dev_t10DMA_DEV_LAE"></a> <a id="_CPPv2N9dma_dev_t10DMA_DEV_LAE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a04adbe1dc4d4aabf2335094342efc3be"></a> enumerator DMA\_DEV\_LA
    :   DMA device LA

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_HSSPIE"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_HSSPIE"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_HSSPIE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201aeaae41175c4698a578033ede15fed2a7"></a> enumerator DMA\_DEV\_HSSPI
    :   DMA device HSSPI

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_AUDIOE"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_AUDIOE"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_AUDIOE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a4bafdcc4810cc7dc2343a946d603ddde"></a> enumerator DMA\_DEV\_AUDIO
    :   DMA device AUDIO

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_AUDIO_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_AUDIO_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_AUDIO_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201aadf199b6cc71e91f1ee098641473dce9"></a> enumerator DMA\_DEV\_AUDIO\_RX
    :   DMA device AUDIO

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_SDIOE"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_SDIOE"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_SDIOE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a9f0883486d0fe51500939cdcf86a1483"></a> enumerator DMA\_DEV\_SDIO
    :   DMA device SDIO

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_SDIO_RXE"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_SDIO_RXE"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_SDIO_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a491863a778d1d2a63f240bccd8e29454"></a> enumerator DMA\_DEV\_SDIO\_RX
    :   DMA device SDIO

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_UART1E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_UART1E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_UART1E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a5d46f98edc85e9d5826f603a1bc9bbf5"></a> enumerator DMA\_DEV\_UART1
    :   DMA device UART1

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_UART1_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_UART1_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_UART1_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ac2f1c54025d432013f24990e6352dd42"></a> enumerator DMA\_DEV\_UART1\_RX
    :   DMA device UART1

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_UART2E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_UART2E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_UART2E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a5fa15268090977c92fcae8e914200c1d"></a> enumerator DMA\_DEV\_UART2
    :   DMA device UART2

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_UART2_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_UART2_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_UART2_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ad11aa7b46d06ac916eeb8c54df23f452"></a> enumerator DMA\_DEV\_UART2\_RX
    :   DMA device UART 2 RX

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_UART3E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_UART3E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_UART3E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ab3f407285f7a9eba95c4fa8986299ee8"></a> enumerator DMA\_DEV\_UART3
    :   DMA device UART3

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_UART3_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_UART3_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_UART3_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a42cf16e078a8f661d0ec144de0f7f9ae"></a> enumerator DMA\_DEV\_UART3\_RX
    :   DMA device UART3

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_UART4E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_UART4E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_UART4E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a473a322a089318b0ddbfd44e7a959d89"></a> enumerator DMA\_DEV\_UART4
    :   DMA device UART4

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_UART4_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_UART4_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_UART4_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a44fade7d3f8af5ea20f283f8ae1f417c"></a> enumerator DMA\_DEV\_UART4\_RX
    :   DMA device UART4

    <a id="_CPPv4N9dma_dev_t11DMA_DEV_I2SE"></a>

    <a id="_CPPv3N9dma_dev_t11DMA_DEV_I2SE"></a> <a id="_CPPv2N9dma_dev_t11DMA_DEV_I2SE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a251ea21a08b82bb25c664571057d9a86"></a> enumerator DMA\_DEV\_I2S
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_I2S_CH1E"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_I2S_CH1E"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_I2S_CH1E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a30658119315e9a864c00971acf1822fa"></a> enumerator DMA\_DEV\_I2S\_CH1
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_I2S_CH2E"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_I2S_CH2E"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_I2S_CH2E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a091e7a4d4d41e06262f8e5e30fdd3fb1"></a> enumerator DMA\_DEV\_I2S\_CH2
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t14DMA_DEV_I2S_RXE"></a>

    <a id="_CPPv3N9dma_dev_t14DMA_DEV_I2S_RXE"></a> <a id="_CPPv2N9dma_dev_t14DMA_DEV_I2S_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a305f4798db60cdeb01984ea71b1988e9"></a> enumerator DMA\_DEV\_I2S\_RX
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t18DMA_DEV_I2S_RX_CH1E"></a>

    <a id="_CPPv3N9dma_dev_t18DMA_DEV_I2S_RX_CH1E"></a> <a id="_CPPv2N9dma_dev_t18DMA_DEV_I2S_RX_CH1E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ac0366b3dcec7e4c55ca94e305d190ce7"></a> enumerator DMA\_DEV\_I2S\_RX\_CH1
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t18DMA_DEV_I2S_RX_CH2E"></a>

    <a id="_CPPv3N9dma_dev_t18DMA_DEV_I2S_RX_CH2E"></a> <a id="_CPPv2N9dma_dev_t18DMA_DEV_I2S_RX_CH2E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a194dc6c975a06940f0512332383fdeed"></a> enumerator DMA\_DEV\_I2S\_RX\_CH2
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_I2S1E"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_I2S1E"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_I2S1E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201aefc9a8b46813ee348e3b1a57c34009da"></a> enumerator DMA\_DEV\_I2S1
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_I2S1_RXE"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_I2S1_RXE"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_I2S1_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a5ad7ad3012c390e3b6a81bb934c502c1"></a> enumerator DMA\_DEV\_I2S1\_RX
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_I2S2E"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_I2S2E"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_I2S2E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a020f911672b44285f526f25dff9cb277"></a> enumerator DMA\_DEV\_I2S2
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_I2S2_RXE"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_I2S2_RXE"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_I2S2_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a7b96421d4bc6d7b0090255c38fd520a7"></a> enumerator DMA\_DEV\_I2S2\_RX
    :   DMA device I2S

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_GSPI0E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_GSPI0E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_GSPI0E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a13d4a0352ad78dc9c1ccee1e8e6211fe"></a> enumerator DMA\_DEV\_GSPI0
    :   DMA device GSPI1

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_GSPI0_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_GSPI0_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_GSPI0_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a6448c10153cf8dadc29c57b1a871db24"></a> enumerator DMA\_DEV\_GSPI0\_RX
    :   DMA device GSPI1

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_GSPI1E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_GSPI1E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_GSPI1E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ad400d2caada58660ebb578d5b369e748"></a> enumerator DMA\_DEV\_GSPI1
    :   DMA device GSPI2

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_GSPI1_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_GSPI1_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_GSPI1_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ae66e2b08d0eb6cb370a22c1783cd0f7f"></a> enumerator DMA\_DEV\_GSPI1\_RX
    :   DMA device GSPI2

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_GSPI2E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_GSPI2E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_GSPI2E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a201996415d2483fc51a5ade071eca51d"></a> enumerator DMA\_DEV\_GSPI2
    :   DMA device GSPI3

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_JPEGE"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_JPEGE"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_JPEGE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a82c54825d6f5ca9a99e573157e2cd067"></a> enumerator DMA\_DEV\_JPEG
    :   DMA device JPEG

    <a id="_CPPv4N9dma_dev_t19DMA_DEV_PSRAM_VIDEOE"></a>

    <a id="_CPPv3N9dma_dev_t19DMA_DEV_PSRAM_VIDEOE"></a> <a id="_CPPv2N9dma_dev_t19DMA_DEV_PSRAM_VIDEOE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201adbf67df65af5a58d5dc38cf0925da998"></a> enumerator DMA\_DEV\_PSRAM\_VIDEO
    :   DMA device PSRAM VIDEO

    <a id="_CPPv4N9dma_dev_t19DMA_DEV_PSRAM_AUDIOE"></a>

    <a id="_CPPv3N9dma_dev_t19DMA_DEV_PSRAM_AUDIOE"></a> <a id="_CPPv2N9dma_dev_t19DMA_DEV_PSRAM_AUDIOE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201aff375f3b8a53da6d151a218a14095377"></a> enumerator DMA\_DEV\_PSRAM\_AUDIO
    :   DMA device PSRAM AUDIO

    <a id="_CPPv4N9dma_dev_t11DMA_DEV_USBE"></a>

    <a id="_CPPv3N9dma_dev_t11DMA_DEV_USBE"></a> <a id="_CPPv2N9dma_dev_t11DMA_DEV_USBE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a0eb2f8d85228990b1ed57ef5291f6363"></a> enumerator DMA\_DEV\_USB
    :   DMA device USB

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_LCD_CMDE"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_LCD_CMDE"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_LCD_CMDE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ac5e77b5bad142e7ff89d888884e63f4d"></a> enumerator DMA\_DEV\_LCD\_CMD
    :   DMA device LCD CMD

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_LCD_DATAE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_LCD_DATAE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_LCD_DATAE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ad768520e3058851f793438fcb9785cd0"></a> enumerator DMA\_DEV\_LCD\_DATA
    :   DMA device LCD DATA

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_DISP_RXE"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_DISP_RXE"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_DISP_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a6edc9450fb0a3794446a570980d907ed"></a> enumerator DMA\_DEV\_DISP\_RX
    :   DMA device DISP RX

    <a id="_CPPv4N9dma_dev_t17DMA_DEV_SDMADC_RXE"></a>

    <a id="_CPPv3N9dma_dev_t17DMA_DEV_SDMADC_RXE"></a> <a id="_CPPv2N9dma_dev_t17DMA_DEV_SDMADC_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201af7b8f849275cae13dd747f5524911fc4"></a> enumerator DMA\_DEV\_SDMADC\_RX
    :   DMA device SDMADC RX

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_AHB_MEME"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_AHB_MEME"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_AHB_MEME"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a03624a29a56229959c89b1d3c35c2d18"></a> enumerator DMA\_DEV\_AHB\_MEM
    :   DMA device AHB\_MEM

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_SPI0E"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_SPI0E"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_SPI0E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201abda33cd5ef8874da3a97d3b885b1ed6f"></a> enumerator DMA\_DEV\_SPI0
    :   DMA device SPI 0

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_SPI1E"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_SPI1E"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_SPI1E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a4c1cfb6715f898c29aa99b4e4f7da892"></a> enumerator DMA\_DEV\_SPI1
    :   DMA device SPI 1

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_H264E"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_H264E"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_H264E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201adf8639d87473a73f7e4ded8b1c6e10d4"></a> enumerator DMA\_DEV\_H264
    :   DMA device H264

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_I2S0E"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_I2S0E"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_I2S0E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a0d3208774812fcba7f223c11b5d0b9f1"></a> enumerator DMA\_DEV\_I2S0
    :   DMA device I2S0

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_I2S0_RXE"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_I2S0_RXE"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_I2S0_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a63fcb433e946c4251aaef92fdbf1998a"></a> enumerator DMA\_DEV\_I2S0\_RX
    :   DMA device I2S0 RX

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_GSPI2_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_GSPI2_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_GSPI2_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ab088c2e74ce0fa07e7addd49ad89cae7"></a> enumerator DMA\_DEV\_GSPI2\_RX
    :   DMA device GSPI2 RX

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_AUD_DMICE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_AUD_DMICE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_AUD_DMICE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a34364e33bff5f03054785ac6553b3219"></a> enumerator DMA\_DEV\_AUD\_DMIC
    :   DMA device aud dmic

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_AUD_MIC0E"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_AUD_MIC0E"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_AUD_MIC0E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ac9e66cfc7bc2b7803d909220303d4792"></a> enumerator DMA\_DEV\_AUD\_MIC0
    :   DMA device aud mic0

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_AUD_SPK0E"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_AUD_SPK0E"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_AUD_SPK0E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a538b16aca33ea6c42f97df870fbbcfdd"></a> enumerator DMA\_DEV\_AUD\_SPK0
    :   DMA device aud spk0

    <a id="_CPPv4N9dma_dev_t21DMA_DEV_AUD_SPK0_HINTE"></a>

    <a id="_CPPv3N9dma_dev_t21DMA_DEV_AUD_SPK0_HINTE"></a> <a id="_CPPv2N9dma_dev_t21DMA_DEV_AUD_SPK0_HINTE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a900db74f336159412247ba05974a248a"></a> enumerator DMA\_DEV\_AUD\_SPK0\_HINT
    :   DMA device aud spk0 hint

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_I2S3E"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_I2S3E"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_I2S3E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201aec7592798511aa90fe9516550605da7c"></a> enumerator DMA\_DEV\_I2S3
    :   DMA device I2S3

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_I2S3_RXE"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_I2S3_RXE"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_I2S3_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a224b51fa6af4e4b6a6a837578e26335c"></a> enumerator DMA\_DEV\_I2S3\_RX
    :   DMA device I2S3 RX

    <a id="_CPPv4N9dma_dev_t14DMA_DEV_SPDIF0E"></a>

    <a id="_CPPv3N9dma_dev_t14DMA_DEV_SPDIF0E"></a> <a id="_CPPv2N9dma_dev_t14DMA_DEV_SPDIF0E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ad9eea1bd62f3c5658fc2033934d367d2"></a> enumerator DMA\_DEV\_SPDIF0
    :   DMA device SPDIF0

    <a id="_CPPv4N9dma_dev_t14DMA_DEV_SPDIF1E"></a>

    <a id="_CPPv3N9dma_dev_t14DMA_DEV_SPDIF1E"></a> <a id="_CPPv2N9dma_dev_t14DMA_DEV_SPDIF1E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a6dea6ea2936c49836ba6cdb355bace88"></a> enumerator DMA\_DEV\_SPDIF1
    :   DMA device SPDIF1

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_SADC_RXE"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_SADC_RXE"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_SADC_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ae6591b00a98e8756864bf92e54fbd9f7"></a> enumerator DMA\_DEV\_SADC\_RX
    :   DMA device SADC RX

    <a id="_CPPv4N9dma_dev_t21DMA_DEV_AUD_SPK0_CALLE"></a>

    <a id="_CPPv3N9dma_dev_t21DMA_DEV_AUD_SPK0_CALLE"></a> <a id="_CPPv2N9dma_dev_t21DMA_DEV_AUD_SPK0_CALLE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a887a9dce716fd8ca1224eed758d62397"></a> enumerator DMA\_DEV\_AUD\_SPK0\_CALL
    :   DMA device aud spk0 call

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_AUD_MIC1E"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_AUD_MIC1E"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_AUD_MIC1E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201af88e48abae448dcc9181c850a61bcc14"></a> enumerator DMA\_DEV\_AUD\_MIC1
    :   DMA device aud mic1

    <a id="_CPPv4N9dma_dev_t21DMA_DEV_AUD_SPK1_A2DPE"></a>

    <a id="_CPPv3N9dma_dev_t21DMA_DEV_AUD_SPK1_A2DPE"></a> <a id="_CPPv2N9dma_dev_t21DMA_DEV_AUD_SPK1_A2DPE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201abf958d2e3148d135ef9eac67e1c46d39"></a> enumerator DMA\_DEV\_AUD\_SPK1\_A2DP
    :   DMA device aud spk1 a2dp

    <a id="_CPPv4N9dma_dev_t21DMA_DEV_AUD_SPK1_HINTE"></a>

    <a id="_CPPv3N9dma_dev_t21DMA_DEV_AUD_SPK1_HINTE"></a> <a id="_CPPv2N9dma_dev_t21DMA_DEV_AUD_SPK1_HINTE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a8e72ba882b0ad234737c1e2b92e7b2d4"></a> enumerator DMA\_DEV\_AUD\_SPK1\_HINT
    :   DMA device aud spk1 hint dma

    <a id="_CPPv4N9dma_dev_t21DMA_DEV_AUD_SPK1_CALLE"></a>

    <a id="_CPPv3N9dma_dev_t21DMA_DEV_AUD_SPK1_CALLE"></a> <a id="_CPPv2N9dma_dev_t21DMA_DEV_AUD_SPK1_CALLE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201adc04bcee2c1a48027ac95c4211f2c1e4"></a> enumerator DMA\_DEV\_AUD\_SPK1\_CALL
    :   DMA device aud spk1 call

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_GSPI3E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_GSPI3E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_GSPI3E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a6ec8a850cf1ce7abc43ac20c7f3b875b"></a> enumerator DMA\_DEV\_GSPI3
    :   DMA device GSPI3

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_GSPI3_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_GSPI3_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_GSPI3_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201afc384957ff6d652d6734724d74d44534"></a> enumerator DMA\_DEV\_GSPI3\_RX
    :   DMA device GSPI3 RX

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_UART5E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_UART5E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_UART5E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a2ac14b846279eefe236ae3a8003ab817"></a> enumerator DMA\_DEV\_UART5
    :   DMA device UART5

    <a id="_CPPv4N9dma_dev_t16DMA_DEV_UART5_RXE"></a>

    <a id="_CPPv3N9dma_dev_t16DMA_DEV_UART5_RXE"></a> <a id="_CPPv2N9dma_dev_t16DMA_DEV_UART5_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a858aef1d5e8902f56867d416651ce3a1"></a> enumerator DMA\_DEV\_UART5\_RX
    :   DMA device UART5 RX

    <a id="_CPPv4N9dma_dev_t12DMA_DEV_I2S4E"></a>

    <a id="_CPPv3N9dma_dev_t12DMA_DEV_I2S4E"></a> <a id="_CPPv2N9dma_dev_t12DMA_DEV_I2S4E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ad0352c6aaba9694b7986b689c0839b6b"></a> enumerator DMA\_DEV\_I2S4
    :   DMA device I2S4

    <a id="_CPPv4N9dma_dev_t15DMA_DEV_I2S4_RXE"></a>

    <a id="_CPPv3N9dma_dev_t15DMA_DEV_I2S4_RXE"></a> <a id="_CPPv2N9dma_dev_t15DMA_DEV_I2S4_RXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201abe9d065f6e849c0aabf1dcc527a1b42c"></a> enumerator DMA\_DEV\_I2S4\_RX
    :   DMA device I2S4 RX

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_XDAC0E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_XDAC0E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_XDAC0E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a86e1e27ba519036cb42e8bbca35c6736"></a> enumerator DMA\_DEV\_XDAC0
    :   DMA device XDAC0

    <a id="_CPPv4N9dma_dev_t13DMA_DEV_XDAC1E"></a>

    <a id="_CPPv3N9dma_dev_t13DMA_DEV_XDAC1E"></a> <a id="_CPPv2N9dma_dev_t13DMA_DEV_XDAC1E"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201a416619ce17d1cfbc280ebeb74c5163c9"></a> enumerator DMA\_DEV\_XDAC1
    :   DMA device XDAC1

    <a id="_CPPv4N9dma_dev_t11DMA_DEV_MAXE"></a>

    <a id="_CPPv3N9dma_dev_t11DMA_DEV_MAXE"></a> <a id="_CPPv2N9dma_dev_t11DMA_DEV_MAXE"></a> <a id="group__bk__api__dma__enum_1gga5db3db1227343b84183a0e7a23b8a201ad05b335c92b7d9ab8de2d40746e4f4d7"></a> enumerator DMA\_DEV\_MAX

<a id="_CPPv416dma_data_width_t"></a>

<a id="_CPPv316dma_data_width_t"></a> <a id="_CPPv216dma_data_width_t"></a> <a id="group__bk__api__dma__enum_1ga0d10903c1db6a2aa72777609ce3e7ec3"></a> enum dma\_data\_width\_t
:   *Values:*

    <a id="_CPPv4N16dma_data_width_t20DMA_DATA_WIDTH_8BITSE"></a>

    <a id="_CPPv3N16dma_data_width_t20DMA_DATA_WIDTH_8BITSE"></a> <a id="_CPPv2N16dma_data_width_t20DMA_DATA_WIDTH_8BITSE"></a> <a id="group__bk__api__dma__enum_1gga0d10903c1db6a2aa72777609ce3e7ec3af59a00997dae0d323eb065ba570a6b1c"></a> enumerator DMA\_DATA\_WIDTH\_8BITS
    :   DMA data width 8bit

    <a id="_CPPv4N16dma_data_width_t21DMA_DATA_WIDTH_16BITSE"></a>

    <a id="_CPPv3N16dma_data_width_t21DMA_DATA_WIDTH_16BITSE"></a> <a id="_CPPv2N16dma_data_width_t21DMA_DATA_WIDTH_16BITSE"></a> <a id="group__bk__api__dma__enum_1gga0d10903c1db6a2aa72777609ce3e7ec3a7d1a5b1dc2a3fe126d1b3c12b167e3c6"></a> enumerator DMA\_DATA\_WIDTH\_16BITS
    :   DMA data width 16bit

    <a id="_CPPv4N16dma_data_width_t21DMA_DATA_WIDTH_32BITSE"></a>

    <a id="_CPPv3N16dma_data_width_t21DMA_DATA_WIDTH_32BITSE"></a> <a id="_CPPv2N16dma_data_width_t21DMA_DATA_WIDTH_32BITSE"></a> <a id="group__bk__api__dma__enum_1gga0d10903c1db6a2aa72777609ce3e7ec3a6f7f1e6a0a7120d090d3245b1810cb48"></a> enumerator DMA\_DATA\_WIDTH\_32BITS
    :   DMA data width 32bit

<a id="_CPPv415dma_work_mode_t"></a>

<a id="_CPPv315dma_work_mode_t"></a> <a id="_CPPv215dma_work_mode_t"></a> <a id="group__bk__api__dma__enum_1gadf0a042a977a7b6cb1182b27a69f6e5a"></a> enum dma\_work\_mode\_t
:   *Values:*

    <a id="_CPPv4N15dma_work_mode_t20DMA_WORK_MODE_SINGLEE"></a>

    <a id="_CPPv3N15dma_work_mode_t20DMA_WORK_MODE_SINGLEE"></a> <a id="_CPPv2N15dma_work_mode_t20DMA_WORK_MODE_SINGLEE"></a> <a id="group__bk__api__dma__enum_1ggadf0a042a977a7b6cb1182b27a69f6e5aa689227c60f69f3fdbf35088d9d5eaee6"></a> enumerator DMA\_WORK\_MODE\_SINGLE
    :   DMA work mode single\_mode

    <a id="_CPPv4N15dma_work_mode_t20DMA_WORK_MODE_REPEATE"></a>

    <a id="_CPPv3N15dma_work_mode_t20DMA_WORK_MODE_REPEATE"></a> <a id="_CPPv2N15dma_work_mode_t20DMA_WORK_MODE_REPEATE"></a> <a id="group__bk__api__dma__enum_1ggadf0a042a977a7b6cb1182b27a69f6e5aa347d56b77767b0f7d40b088fb1e505ca"></a> enumerator DMA\_WORK\_MODE\_REPEAT
    :   DMA work mode repeat\_mode (forever repeat until software clear dma\_en)

<a id="_CPPv419dma_priority_mode_t"></a>

<a id="_CPPv319dma_priority_mode_t"></a> <a id="_CPPv219dma_priority_mode_t"></a> <a id="group__bk__api__dma__enum_1ga3f709436c5bb916cc06db28edd8ff38b"></a> enum dma\_priority\_mode\_t
:   *Values:*

    <a id="_CPPv4N19dma_priority_mode_t25DMA_PRIO_MODE_ROUND_ROBINE"></a>

    <a id="_CPPv3N19dma_priority_mode_t25DMA_PRIO_MODE_ROUND_ROBINE"></a> <a id="_CPPv2N19dma_priority_mode_t25DMA_PRIO_MODE_ROUND_ROBINE"></a> <a id="group__bk__api__dma__enum_1gga3f709436c5bb916cc06db28edd8ff38ba3b8a094398ea507916e919ec03acc9e5"></a> enumerator DMA\_PRIO\_MODE\_ROUND\_ROBIN
    :   DMA priority mode round-robin(all dma priority are the same)

    <a id="_CPPv4N19dma_priority_mode_t24DMA_PRIO_MODE_FIXED_PRIOE"></a>

    <a id="_CPPv3N19dma_priority_mode_t24DMA_PRIO_MODE_FIXED_PRIOE"></a> <a id="_CPPv2N19dma_priority_mode_t24DMA_PRIO_MODE_FIXED_PRIOE"></a> <a id="group__bk__api__dma__enum_1gga3f709436c5bb916cc06db28edd8ff38bab7b37c50974b38f3a265c13c0af8e39d"></a> enumerator DMA\_PRIO\_MODE\_FIXED\_PRIO
    :   DMA priority mode fixed prio(depend on chan\_prio)

<a id="_CPPv414dma_addr_inc_t"></a>

<a id="_CPPv314dma_addr_inc_t"></a> <a id="_CPPv214dma_addr_inc_t"></a> <a id="group__bk__api__dma__enum_1ga8c6b1247ff694f5ae35b930b4ebe7000"></a> enum dma\_addr\_inc\_t
:   *Values:*

    <a id="_CPPv4N14dma_addr_inc_t20DMA_ADDR_INC_DISABLEE"></a>

    <a id="_CPPv3N14dma_addr_inc_t20DMA_ADDR_INC_DISABLEE"></a> <a id="_CPPv2N14dma_addr_inc_t20DMA_ADDR_INC_DISABLEE"></a> <a id="group__bk__api__dma__enum_1gga8c6b1247ff694f5ae35b930b4ebe7000aef9d774754ca442742d3feb412fd2eff"></a> enumerator DMA\_ADDR\_INC\_DISABLE
    :   DMA disable addrress increase

    <a id="_CPPv4N14dma_addr_inc_t19DMA_ADDR_INC_ENABLEE"></a>

    <a id="_CPPv3N14dma_addr_inc_t19DMA_ADDR_INC_ENABLEE"></a> <a id="_CPPv2N14dma_addr_inc_t19DMA_ADDR_INC_ENABLEE"></a> <a id="group__bk__api__dma__enum_1gga8c6b1247ff694f5ae35b930b4ebe7000adaa89687ea6bb5f80a1df831ef7c32f2"></a> enumerator DMA\_ADDR\_INC\_ENABLE
    :   DMA enable addrress increase

<a id="_CPPv415dma_addr_loop_t"></a>

<a id="_CPPv315dma_addr_loop_t"></a> <a id="_CPPv215dma_addr_loop_t"></a> <a id="group__bk__api__dma__enum_1gab84ff94868250c8de57f55b0adb5f13d"></a> enum dma\_addr\_loop\_t
:   *Values:*

    <a id="_CPPv4N15dma_addr_loop_t21DMA_ADDR_LOOP_DISABLEE"></a>

    <a id="_CPPv3N15dma_addr_loop_t21DMA_ADDR_LOOP_DISABLEE"></a> <a id="_CPPv2N15dma_addr_loop_t21DMA_ADDR_LOOP_DISABLEE"></a> <a id="group__bk__api__dma__enum_1ggab84ff94868250c8de57f55b0adb5f13da00816b3e1a2691d03d1eca2530a4474b"></a> enumerator DMA\_ADDR\_LOOP\_DISABLE
    :   DMA disable addrress loop

    <a id="_CPPv4N15dma_addr_loop_t20DMA_ADDR_LOOP_ENABLEE"></a>

    <a id="_CPPv3N15dma_addr_loop_t20DMA_ADDR_LOOP_ENABLEE"></a> <a id="_CPPv2N15dma_addr_loop_t20DMA_ADDR_LOOP_ENABLEE"></a> <a id="group__bk__api__dma__enum_1ggab84ff94868250c8de57f55b0adb5f13da130e4aa06e88ea19f9964c6b11605a34"></a> enumerator DMA\_ADDR\_LOOP\_ENABLE
    :   DMA enable addrress loop

<a id="_CPPv414dma_sec_attr_t"></a>

<a id="_CPPv314dma_sec_attr_t"></a> <a id="_CPPv214dma_sec_attr_t"></a> <a id="group__bk__api__dma__enum_1ga871f164b1f92a88b368c85b9e0c4b44b"></a> enum dma\_sec\_attr\_t
:   *Values:*

    <a id="_CPPv4N14dma_sec_attr_t16DMA_ATTR_NON_SECE"></a>

    <a id="_CPPv3N14dma_sec_attr_t16DMA_ATTR_NON_SECE"></a> <a id="_CPPv2N14dma_sec_attr_t16DMA_ATTR_NON_SECE"></a> <a id="group__bk__api__dma__enum_1gga871f164b1f92a88b368c85b9e0c4b44bafab47a66d2ad6a9543b67c0f9eade509"></a> enumerator DMA\_ATTR\_NON\_SEC
    :   DMA non-secure attr

    <a id="_CPPv4N14dma_sec_attr_t12DMA_ATTR_SECE"></a>

    <a id="_CPPv3N14dma_sec_attr_t12DMA_ATTR_SECE"></a> <a id="_CPPv2N14dma_sec_attr_t12DMA_ATTR_SECE"></a> <a id="group__bk__api__dma__enum_1gga871f164b1f92a88b368c85b9e0c4b44bad8e0dd9bd614351989edda54bbfd9b2d"></a> enumerator DMA\_ATTR\_SEC
    :   DMA secure attr

<a id="_CPPv415dma_burst_len_t"></a>

<a id="_CPPv315dma_burst_len_t"></a> <a id="_CPPv215dma_burst_len_t"></a> <a id="group__bk__api__dma__enum_1ga7e30282623413274949c8976690211b2"></a> enum dma\_burst\_len\_t
:   *Values:*

    <a id="_CPPv4N15dma_burst_len_t16BURST_LEN_SINGLEE"></a>

    <a id="_CPPv3N15dma_burst_len_t16BURST_LEN_SINGLEE"></a> <a id="_CPPv2N15dma_burst_len_t16BURST_LEN_SINGLEE"></a> <a id="group__bk__api__dma__enum_1gga7e30282623413274949c8976690211b2a035fb27d91a5ffaf7e9a269929345a76"></a> enumerator BURST\_LEN\_SINGLE

    <a id="_CPPv4N15dma_burst_len_t14BURST_LEN_INC4E"></a>

    <a id="_CPPv3N15dma_burst_len_t14BURST_LEN_INC4E"></a> <a id="_CPPv2N15dma_burst_len_t14BURST_LEN_INC4E"></a> <a id="group__bk__api__dma__enum_1gga7e30282623413274949c8976690211b2a17081dcdc4a6e3a9559c53faec2b0823"></a> enumerator BURST\_LEN\_INC4

    <a id="_CPPv4N15dma_burst_len_t14BURST_LEN_INC8E"></a>

    <a id="_CPPv3N15dma_burst_len_t14BURST_LEN_INC8E"></a> <a id="_CPPv2N15dma_burst_len_t14BURST_LEN_INC8E"></a> <a id="group__bk__api__dma__enum_1gga7e30282623413274949c8976690211b2a66917a96793ab3afb37319c2c3aa541c"></a> enumerator BURST\_LEN\_INC8

    <a id="_CPPv4N15dma_burst_len_t15BURST_LEN_INC16E"></a>

    <a id="_CPPv3N15dma_burst_len_t15BURST_LEN_INC16E"></a> <a id="_CPPv2N15dma_burst_len_t15BURST_LEN_INC16E"></a> <a id="group__bk__api__dma__enum_1gga7e30282623413274949c8976690211b2a0452b7fc2eee70f2434adf4886e928f5"></a> enumerator BURST\_LEN\_INC16

<a id="_CPPv422dma_pixel_trans_type_t"></a>

<a id="_CPPv322dma_pixel_trans_type_t"></a> <a id="_CPPv222dma_pixel_trans_type_t"></a> <a id="group__bk__api__dma__enum_1gaf89131405cad30f656dda47fc46e7744"></a> enum dma\_pixel\_trans\_type\_t
:   *Values:*

    <a id="_CPPv4N22dma_pixel_trans_type_t17DMA_TRANS_DEFAULTE"></a>

    <a id="_CPPv3N22dma_pixel_trans_type_t17DMA_TRANS_DEFAULTE"></a> <a id="_CPPv2N22dma_pixel_trans_type_t17DMA_TRANS_DEFAULTE"></a> <a id="group__bk__api__dma__enum_1ggaf89131405cad30f656dda47fc46e7744af219c73a61f4982b8ba5212a7ae8da22"></a> enumerator DMA\_TRANS\_DEFAULT
    :   DMA TRANS DEFAULT

    <a id="_CPPv4N22dma_pixel_trans_type_t20DMA_TRANS_RGB_TO_YUVE"></a>

    <a id="_CPPv3N22dma_pixel_trans_type_t20DMA_TRANS_RGB_TO_YUVE"></a> <a id="_CPPv2N22dma_pixel_trans_type_t20DMA_TRANS_RGB_TO_YUVE"></a> <a id="group__bk__api__dma__enum_1ggaf89131405cad30f656dda47fc46e7744afc2a7eda2d5164316f0ecdf84b3f0990"></a> enumerator DMA\_TRANS\_RGB\_TO\_YUV
    :   DMA TRANS RGB\_TO\_YUV

    <a id="_CPPv4N22dma_pixel_trans_type_t20DMA_TRANS_YUV_TO_RGBE"></a>

    <a id="_CPPv3N22dma_pixel_trans_type_t20DMA_TRANS_YUV_TO_RGBE"></a> <a id="_CPPv2N22dma_pixel_trans_type_t20DMA_TRANS_YUV_TO_RGBE"></a> <a id="group__bk__api__dma__enum_1ggaf89131405cad30f656dda47fc46e7744a311092354c382ec1c3382d61b1da2416"></a> enumerator DMA\_TRANS\_YUV\_TO\_RGB
    :   DMA TRANS YUV\_TO\_RGB

    <a id="_CPPv4N22dma_pixel_trans_type_t13DMA_TRANS_MAXE"></a>

    <a id="_CPPv3N22dma_pixel_trans_type_t13DMA_TRANS_MAXE"></a> <a id="_CPPv2N22dma_pixel_trans_type_t13DMA_TRANS_MAXE"></a> <a id="group__bk__api__dma__enum_1ggaf89131405cad30f656dda47fc46e7744ac9e2399f25d96880392ef78c457d4670"></a> enumerator DMA\_TRANS\_MAX

<a id="_CPPv48dma_id_t"></a>

<a id="_CPPv38dma_id_t"></a> <a id="_CPPv28dma_id_t"></a> <a id="group__bk__api__dma__enum_1ga1f892e2d7321ac9b35e128d1f5bcf3ce"></a> enum dma\_id\_t
:   *Values:*

    <a id="_CPPv4N8dma_id_t8DMA_ID_0E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_0E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_0E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3ceacfd9baf12033254804a0660b47e79384"></a> enumerator DMA\_ID\_0
    :   DMA channel 0

    <a id="_CPPv4N8dma_id_t8DMA_ID_1E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_1E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_1E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3ceaadf251cbf97fcb24fbd2feb8067b6350"></a> enumerator DMA\_ID\_1
    :   DMA channel 1

    <a id="_CPPv4N8dma_id_t8DMA_ID_2E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_2E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_2E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea3e2379b9d20087a6ebbb4e9357d951eb"></a> enumerator DMA\_ID\_2
    :   DMA channel 2

    <a id="_CPPv4N8dma_id_t8DMA_ID_3E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_3E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_3E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea1fdb95b79089d24a8faa18c356082113"></a> enumerator DMA\_ID\_3
    :   DMA channel 3

    <a id="_CPPv4N8dma_id_t8DMA_ID_4E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_4E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_4E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea37c329e58c519e8b5b3aa41606359e05"></a> enumerator DMA\_ID\_4
    :   DMA channel 4

    <a id="_CPPv4N8dma_id_t8DMA_ID_5E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_5E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_5E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea262c5b67a04c6014abeadec285045238"></a> enumerator DMA\_ID\_5
    :   DMA channel 5

    <a id="_CPPv4N8dma_id_t8DMA_ID_6E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_6E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_6E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea911f0e6ef54c18039f2f3277a7cc47b3"></a> enumerator DMA\_ID\_6
    :   DMA channel 6

    <a id="_CPPv4N8dma_id_t8DMA_ID_7E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_7E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_7E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea606928df3ad95aacaed07c2a75cb2599"></a> enumerator DMA\_ID\_7
    :   DMA channel 7

    <a id="_CPPv4N8dma_id_t8DMA_ID_8E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_8E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_8E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3ceaefdae9ba1356541a2915f0f0ab302414"></a> enumerator DMA\_ID\_8
    :   DMA channel 8

    <a id="_CPPv4N8dma_id_t8DMA_ID_9E"></a>

    <a id="_CPPv3N8dma_id_t8DMA_ID_9E"></a> <a id="_CPPv2N8dma_id_t8DMA_ID_9E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea775f00dae874d27bb6196b8a3fe4982a"></a> enumerator DMA\_ID\_9
    :   DMA channel 9

    <a id="_CPPv4N8dma_id_t9DMA_ID_10E"></a>

    <a id="_CPPv3N8dma_id_t9DMA_ID_10E"></a> <a id="_CPPv2N8dma_id_t9DMA_ID_10E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3ceae33a6529fae7662d2d7c413ddf660a5a"></a> enumerator DMA\_ID\_10
    :   DMA channel 10

    <a id="_CPPv4N8dma_id_t9DMA_ID_11E"></a>

    <a id="_CPPv3N8dma_id_t9DMA_ID_11E"></a> <a id="_CPPv2N8dma_id_t9DMA_ID_11E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3ceaf094751b036998043e6e059eeb9f0d76"></a> enumerator DMA\_ID\_11
    :   DMA channel 11

    <a id="_CPPv4N8dma_id_t9DMA_ID_12E"></a>

    <a id="_CPPv3N8dma_id_t9DMA_ID_12E"></a> <a id="_CPPv2N8dma_id_t9DMA_ID_12E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea2f21c504e35c17aba53503d4f19b1579"></a> enumerator DMA\_ID\_12
    :   DMA channel 12

    <a id="_CPPv4N8dma_id_t9DMA_ID_13E"></a>

    <a id="_CPPv3N8dma_id_t9DMA_ID_13E"></a> <a id="_CPPv2N8dma_id_t9DMA_ID_13E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cead8fa070011ffa6e90f2d0b6f7a9aeb1c"></a> enumerator DMA\_ID\_13
    :   DMA channel 13

    <a id="_CPPv4N8dma_id_t9DMA_ID_14E"></a>

    <a id="_CPPv3N8dma_id_t9DMA_ID_14E"></a> <a id="_CPPv2N8dma_id_t9DMA_ID_14E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea11bd33e1ee967c15e8e4eb347fe7943d"></a> enumerator DMA\_ID\_14
    :   DMA channel 14

    <a id="_CPPv4N8dma_id_t9DMA_ID_15E"></a>

    <a id="_CPPv3N8dma_id_t9DMA_ID_15E"></a> <a id="_CPPv2N8dma_id_t9DMA_ID_15E"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea63dfcc4b7121d9c9b125531c8348bf38"></a> enumerator DMA\_ID\_15
    :   DMA channel 15

    <a id="_CPPv4N8dma_id_t10DMA_ID_MAXE"></a>

    <a id="_CPPv3N8dma_id_t10DMA_ID_MAXE"></a> <a id="_CPPv2N8dma_id_t10DMA_ID_MAXE"></a> <a id="group__bk__api__dma__enum_1gga1f892e2d7321ac9b35e128d1f5bcf3cea964387cd6173e1ed55c333eeaa0b051d"></a> enumerator DMA\_ID\_MAX
    :   DMA channel max
