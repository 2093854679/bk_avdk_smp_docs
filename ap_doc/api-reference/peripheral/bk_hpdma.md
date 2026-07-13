# HPDMA


BK7259 AP 侧 HPDMA API（`include/driver/hpdma.h`）。详细说明见
[HPDMA 开发指南](../../developer-guide/peripheral/bk_hpdma.md "../../developer-guide/peripheral/bk_hpdma.md")。


## HPDMA API Reference


### Header File


- [hpdma.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hpdma.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hpdma.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_driver_init(void)
:   Init the DMA driver.

    This API init the resoure common to all dma channels:


    - Init dma driver control memory

    This API should be called before any other dma APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_driver_deinit(void)
:   Deinit the DMA driver.

    This API free all resource related to dma and power down all dma channels.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") bk_hpdma_alloc(u16 user_id)
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

[hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") bk_fixed_hpdma_alloc(u16 user_id, [hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") fixed_chnl_id)
:   Allocate a fixed DMA channel.Maybe some APP needs to have a fixed channel forever, then it can use this API.

    This API should be called before any other dma channel APIs.


    **Attention**
    :   : This API is just for CONFIG_GDMA_HW_V2PX And CONFIG_GDMA_HW_V1PX doesn’t support it.

    参数
    :   - **user_id** – DMA channel applicant

        - **fixed_chnl_id** – application wants to get which fixed channel

    返回
    :   DMA channel id.


        - > DMA_ID_MAX: if the fixed_chnl_id has been allocated, it will return DMA_ID_MAX which means error.

        - > fixed_chnl_id: the fixed_chnl_id is allocated suc.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_free(u16 user_id, [hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Free the DMA channel.


    **Attention**
    :   : This API can only be called in task context,


        - and can’t be called in context that interrupt is disabled.

    参数
    :   - **user_id** – DMA channel applicant, the same as in bk_hpdma_alloc.

        - **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_force_reclaim(u16 user_id, [hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") chnl_id)
:   Force release a channel that bk_hpdma_free() refused to release (S0/C: HPDMA stability review escape hatch).

    bk_hpdma_free() now performs a defensive stop + wait-to-idle and leaves the channel reserved if the engine does not honour the stop within HPDMA_MAX_BUSY_TIME us. This API is the only sanctioned way to recover that stuck channel for re-use. It performs a per-channel register reset (NOT a full controller soft_reset), clears the channel’s ISR callbacks and finally releases the bitmap entry. Any data the engine had not yet committed is lost; callers must release their associated buffers AFTER the channel is reclaimed (or with full awareness of the data-loss risk).

    备注

    Task context only. Do NOT call from ISR or with interrupts disabled.

    参数
    :   - **user_id** – Same applicant token passed to bk_hpdma_alloc().

        - **chnl_id** – Channel id originally returned by bk_hpdma_alloc().

    返回
    :   - BK_OK: channel reclaimed

        - BK_ERR_HPDMA_NOT_INIT / BK_ERR_HPDMA_ID / BK_ERR_PARAM otherwise

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_recover_after_low_voltage(void)
:   Recover global HPDMA controller registers after low-voltage wakeup (S2: HPDMA stability review).

    The controller-wide registers (soft_reset / secure_attr / privileged_attr / prio_mode) are powered down with the rest of the chip during low-voltage sleep and read back as zero on wakeup. Call this once from the PM wakeup hook BEFORE any client invokes bk_hpdma_init() / bk_hpdma_start().

    备注

    Do not call from per-transfer paths; that was the historical bug.

    返回
    :   BK_OK on success.

uint32_t bk_hpdma_user([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   get the user of DMA channel

    参数
    :   **id** – DMA channel

    返回
    :   DMA channel user_id.


        - u32: high u16 is the CPU_ID, low 16 bits is the applicant_id.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_init([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, const [hpdma_config_t](#_CPPv414hpdma_config_t "hpdma_config_t") *config)
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

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_deinit([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Deinit a DMA channel.

    This API deinit the DMA channel:


    - Stop the DMA channel

    - Reset all configuration of DMA channel to default value

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_start([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Start a DMA channel.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_stop([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Stop a DMA channel.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_wait_to_idle([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Wait until the given DMA channel becomes idle (S1: hpdma stability).

    Polls the channel’s hardware enable bit (and for HPDMA_WORK_MODE_REPEAT issues a stop first) up to HPDMA_MAX_BUSY_TIME microseconds.

    Callers should invoke this before touching channel registers (e.g. changing the destination address / data width) or before tearing down DMA target buffers, to avoid the use-after-free / mid-transfer write hazards described in the HPDMA stability review.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: channel is idle

        - BK_ERR_HPDMA_TIMEOUT: channel still busy after HPDMA_MAX_BUSY_TIME us

        - other negative: parameter / not-initialized errors

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_enable_finish_interrupt([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA finish intterrup.

    @NOTES before enable interrupt, please confirm have called bk_hpdma_register_isr.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_disable_finish_interrupt([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA finish intterrup.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_enable_half_finish_interrupt([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA half finish intterrup.

    @NOTES before enable interrupt, please confirm have called bk_hpdma_register_isr.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_disable_half_finish_interrupt([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA half finish intterrup.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_enable_bus_err_interrupt([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA bus error interrupt.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_disable_bus_err_interrupt([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA bus error interrupt.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_register_isr([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, [hpdma_isr_t](#_CPPv411hpdma_isr_t "hpdma_isr_t") half_finish_isr, void *half_finish_data, [hpdma_isr_t](#_CPPv411hpdma_isr_t "hpdma_isr_t") finish_isr, void *finish_data)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function with user data parameter.

    参数
    :   - **id** – DMA channel

        - **half_finish_isr** – DMA half finish callback

        - **half_finish_data** – User data for half finish callback (can be NULL)

        - **finish_isr** – DMA finish callback

        - **finish_data** – User data for finish callback (can be NULL)

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_register_bus_err_isr([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, [hpdma_isr_t](#_CPPv411hpdma_isr_t "hpdma_isr_t") bus_err_isr, void *user_data)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function with user data parameter.

    参数
    :   - **id** – DMA channel

        - **bus_err_isr** – DMA bus error callback

        - **user_data** – User data for bus error callback (can be NULL)

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_register_fifo_err_isr([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, [hpdma_isr_t](#_CPPv411hpdma_isr_t "hpdma_isr_t") fifo_err_isr, void *user_data)
:   Register a callback for the fifo_err interrupt class (P0: HPDMA review).

    fifo_err is the 4th error class on Reg23/Reg28 (bit17 in status). It was previously not wired up; callers that enable it via bk_hpdma_enable_fifo_err_interrupt() can use this to be notified after the ISR has halted the engine.

    参数
    :   - **id** – DMA channel

        - **fifo_err_isr** – Callback (NULL to clear)

        - **user_data** – Opaque user pointer

    返回
    :   BK_OK on success.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_enable_fifo_err_interrupt([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable / disable the fifo_err interrupt for a DMA channel (P0: HPDMA review).

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_disable_fifo_err_interrupt([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_set_src_start_addr([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, uint32_t start_addr)
:   Set DMA source start address.

    参数
    :   - **id** – DMA channel

        - **start_addr** – DMA source start address (pass the CPU-side 0x2C alias; the driver converts it to the HPDMA-visible 0x28 alias)

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_set_dest_start_addr([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, uint32_t start_addr)
:   Set DMA dest start address.

    参数
    :   - **id** – DMA channel

        - **start_addr** – DMA dest start address (pass the CPU-side 0x2C alias; the driver converts it to the HPDMA-visible 0x28 alias)

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_enable_src_addr_increase([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA source address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_disable_src_addr_increase([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA source address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_enable_src_addr_loop([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA source address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_disable_src_addr_loop([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA source address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_enable_dest_addr_increase([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA dest address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_disable_dest_addr_increase([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA dest address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_enable_dest_addr_loop([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA dest address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_disable_dest_addr_loop([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA dest address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_hpdma_get_remain_len([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Get DMA transfer remain length.

    参数
    :   **id** – DMA channel

    返回
    :   DMA transfer remain length

uint32_t bk_hpdma_get_enable_status([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Gets the current DMA channel working status.

    参数
    :   **id** – DMA channel

    返回
    :   - 0: Channel idle state

        - others: Channel busy state.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_flush_src_buffer([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   flush reserved data in dma internal buffer I.E:If source data width is not 4bytes, and data size isn’t 4bytes align, but dest data width is 4bytes, then maybe 1~3 bytes data reserved in dma internal buffer, then the left 1~3 bytes data not copy to dest address.

    参数
    :   - **id** – DMA channel

        - **attr** – DMA privileged attr

    返回
    :   - 0: Channel idle state

        - others: Channel busy state.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_set_next_ll_addr([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, uint32_t ll_addr)
:   Set next linked list address.

    参数
    :   - **id** – DMA channel

        - **ll_addr** – Linked list address (pass the CPU-side 0x2C alias; the driver converts it to the HPDMA-visible 0x28 alias)

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_hpdma_get_next_ll_addr([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Get next linked list address.

    备注

    Returns the raw 0x28 peripheral alias from the hardware register; it is NOT converted back to 0x2C. Today it is only used for a done-check (compare against 0, which is alias-agnostic). If you need to compare it against a 0x2C pointer you hold, or subtract a base address, convert first with SOC_SRAM_CPU_ADDR().

    参数
    :   **id** – DMA channel

    返回
    :   Next linked list address (0x28 peripheral alias)

void *bk_hpdma_link_init(uint32_t link_cnt)
:   Initialize linked list descriptor table.

    This API allocates and initializes a descriptor table for linked list DMA transfers.

    备注

    The next_desc_addr chain pointers between descriptors are converted 0x2C->0x28 by this API. After you get the returned desc_table, only fill it via bk_hpdma_link_set_desc(); do NOT write the [hpdma_descriptor_t](#structhpdma__descriptor__t "#structhpdma__descriptor__t") fields directly (see the SRAM address-alias contract at the top of this file).

    参数
    :   **link_cnt** – Number of descriptors in the linked list

    返回
    :   - Pointer to the first descriptor (16-byte aligned) on success

        - NULL on failure (memory allocation failed)

void bk_hpdma_link_deinit(void *desc_table)
:   Deinitialize linked list descriptor table.

    This API frees the memory allocated for the descriptor table.

    参数
    :   **desc_table** – Descriptor table pointer returned by bk_hpdma_link_init

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_link_set_desc(void *desc_table, uint32_t index, const [hpdma_link_config_t](#_CPPv419hpdma_link_config_t "hpdma_link_config_t") *config)
:   Set a single descriptor in the linked list.

    This API configures a descriptor at the specified index for DMA transfer. Supports both 1D and 2D transfers.

    备注

    config src_addr/dst_addr take the CPU-side 0x2C alias; this API applies the 0x2C->0x28 conversion when writing the descriptor. This is the only supported entry point for building linked-list descriptors - do not bypass it and write the descriptor struct directly (see the SRAM address-alias contract at the top of this file).

    参数
    :   - **desc_table** – Descriptor table pointer

        - **index** – Descriptor index

        - **config** – Transfer configuration (for 1D: set ysize=1, step=0)

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: invalid parameters

        - BK_ERR_PARAM: invalid parameters

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_link_set_descs(void *desc_table, const [hpdma_link_config_t](#_CPPv419hpdma_link_config_t "hpdma_link_config_t") *configs, uint32_t link_cnt)
:   Set multiple descriptors in the linked list.

    This API configures multiple descriptors for DMA transfer. Supports both 1D and 2D transfers.

    参数
    :   - **desc_table** – Descriptor table pointer

        - **configs** – Configuration array (for 1D: set ysize=1, step=0)

        - **link_cnt** – Number of descriptors to configure

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: invalid parameters

        - others: other errors

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_link_transfer([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, void *desc_table)
:   Execute linked list transfer (Asynchronous)

    This API configures the DMA channel and starts the transfer. The DMA channel ID must be allocated by the application layer using bk_hpdma_alloc(). The function returns after the transfer is started (not necessarily completed).

    参数
    :   - **id** – DMA channel ID (allocated by application layer using bk_hpdma_alloc())

        - **desc_table** – Descriptor table pointer

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: invalid descriptor table

        - BK_ERR_HPDMA_ID: invalid DMA channel ID

        - others: other errors

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_memcpy(void *out, const void *in, uint32_t len)
:   Memory copy using HPDMA.

    This API performs a memory copy operation using HPDMA. It automatically allocates a DMA channel, performs the transfer, and frees the channel.

    Length is no longer limited to the 16-bit single-shot size: transfers larger than HPDMA_SINGLE_MAX_XFER (0xF000 bytes) are automatically split into a linked list of chunks and kicked as a single chain.

    When called from task context (scheduler running, not suspended), completion is awaited on a semaphore posted by the finish interrupt, so the CPU is yielded instead of busy-waiting. In non-blockable contexts (ISR / critical section) it falls back to a bounded busy-poll. If the DMA path fails for any reason, it transparently falls back to a CPU copy so the data is always correct.

    参数
    :   - **out** – Destination address

        - **in** – Source address

        - **len** – Number of bytes to copy

    返回
    :   - BK_OK: succeed (including successful CPU fallback)

        - BK_ERR_NULL_PARAM: out or in is NULL

        - others: other errors

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_hpdma_memcpy_link(void *out, const void *in, uint32_t len, [hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") cpy_chnl)
:   Memory copy using HPDMA on a caller-owned channel.

    Same behaviour as bk_hpdma_memcpy() (arbitrary length via linked-list split, interrupt/semaphore completion with busy-poll fallback) but on a channel the caller has already allocated with bk_hpdma_alloc(). The channel is NOT freed by this call. No CPU fallback is performed; the DMA error is returned so the caller can decide how to recover.

    参数
    :   - **out** – Destination address

        - **in** – Source address

        - **len** – Number of bytes to copy

        - **cpy_chnl** – DMA channel allocated by the caller

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: out or in is NULL

        - BK_ERR_HPDMA_ID: invalid channel id

        - others: other errors


## HPDMA API Typedefs


### Header File


- [hpdma_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hpdma_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hpdma_types.h")


### Structures

struct hpdma_isr_info_t
:   DMA interrupt service routine with user data.


### Macros

BK_ERR_HPDMA_ID
:   HPDMA id is invalid

BK_ERR_HPDMA_NOT_INIT
:   HPDMA driver not init

BK_ERR_HPDMA_ID_NOT_INIT
:   HPDMA id not init

BK_ERR_HPDMA_ID_NOT_START
:   HPDMA id not start

BK_ERR_HPDMA_INVALID_ADDR
:   HPDMA addr is invalid

BK_ERR_HPDMA_ID_REINIT
:   HPDMA id has inited, if reinit,please de-init firstly

BK_ERR_HPDMA_TRANS_LEN
:   HPDMA trans len is invalid

BK_ERR_HPDMA_TIMEOUT
:   HPDMA wait-to-idle timeout (channel still busy)


### Type Definitions

typedef void (*hpdma_isr_t)([hpdma_id_t](#_CPPv410hpdma_id_t "hpdma_id_t") hpdma_id, void *user_data)
:   DMA interrupt service routine.


### Header File


- [hal/hal_hpdma_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_hpdma_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_hpdma_types.h")


### Structures

struct hpdma_port_config_t

struct hpdma_config_t

struct hpdma_descriptor_t

struct hpdma_link_config_t


### Macros

BK_ERR_HPDMA_HAL_INVALID_ALIGN
:   HPDMA loop window is not 128-bit aligned

BK_ERR_HPDMA_HAL_INVALID_YSIZE
:   HPDMA ysize must be 0 when addr loop is enabled


### Type Definitions

typedef uint8_t hpdma_unit_t
:   DMA uint id

typedef uint8_t hpdma_chan_priority_t
:   DMA channel priority:the value is higher then the priority is higher


### Enumerations

enum hpdma_int_id_t
:   CPU core for DMA Interrupt Differentiation Notification.

    @Enumeration option selection core notifies DMA to interrupt after completion of transport

    @Notification of terminal selection based on channel operation


    *Values:*

    enumerator HPDMA_INT_0
    :   DMA INT 0 m55 cpu core 0

    enumerator HPDMA_INT_1
    :   DMA INT 1 m55 cpu core 1

    enumerator HPDMA_INT_2
    :   DMA INT 2 m52

    enumerator HPDMA_INT_3
    :   DMA INT 3 NA

    enumerator HPDMA_INT_4
    :   DMA INT 4 NA

    enumerator HPDMA_INT_MAX
    :   DMA channel max

enum hpdma_dev_t
:   *Values:*

    enumerator HPDMA_DEV_DTCM
    :   DMA device DTCM

    enumerator HPDMA_DEV_UART5
    :   DMA device UART5

    enumerator HPDMA_DEV_MAX

enum hpdma_data_width_t
:   *Values:*

    enumerator HPDMA_DATA_WIDTH_8BITS
    :   DMA data width 8bit

    enumerator HPDMA_DATA_WIDTH_16BITS
    :   DMA data width 16bit

    enumerator HPDMA_DATA_WIDTH_32BITS
    :   DMA data width 32bit

    enumerator HPDMA_DATA_WIDTH_64BITS
    :   DMA data width 32bit

    enumerator HPDMA_DATA_WIDTH_128BITS
    :   DMA data width 32bit

enum hpdma_work_mode_t
:   *Values:*

    enumerator HPDMA_WORK_MODE_SINGLE
    :   DMA work mode single_mode

    enumerator HPDMA_WORK_MODE_REPEAT
    :   DMA work mode repeat_mode (forever repeat until software clear dma_en)

enum hpdma_priority_mode_t
:   *Values:*

    enumerator HPDMA_PRIO_MODE_ROUND_ROBIN
    :   DMA priority mode round-robin(all dma priority are the same)

    enumerator HPDMA_PRIO_MODE_FIXED_PRIO
    :   DMA priority mode fixed prio(depend on chan_prio)

enum hpdma_addr_inc_t
:   *Values:*

    enumerator HPDMA_ADDR_INC_DISABLE
    :   DMA disable addrress increase

    enumerator HPDMA_ADDR_INC_ENABLE
    :   DMA enable addrress increase

enum hpdma_addr_loop_t
:   *Values:*

    enumerator HPDMA_ADDR_LOOP_DISABLE
    :   DMA disable addrress loop

    enumerator HPDMA_ADDR_LOOP_ENABLE
    :   DMA enable addrress loop

enum hpdma_sec_attr_t
:   *Values:*

    enumerator HPDMA_ATTR_NON_SEC
    :   DMA non-secure attr

    enumerator HPDMA_ATTR_SEC
    :   DMA secure attr

enum hpdma_burst_len_t
:   *Values:*

    enumerator HPDMA_BURST_LEN_SINGLE

    enumerator HPDMA_BURST_LEN_INC4

    enumerator HPDMA_BURST_LEN_INC8

    enumerator HPDMA_BURST_LEN_INC16

enum hpdma_pixel_trans_type_t
:   *Values:*

    enumerator HPDMA_TRANS_DEFAULT
    :   DMA TRANS DEFAULT

    enumerator HPDMA_TRANS_YUV_TO_RGB
    :   DMA TRANS YUV_TO_RGB

    enumerator HPDMA_TRANS_MAX

enum hpdma_id_t
:   *Values:*

    enumerator HPDMA_ID_0
    :   DMA channel 0

    enumerator HPDMA_ID_1
    :   DMA channel 1

    enumerator HPDMA_ID_2
    :   DMA channel 2

    enumerator HPDMA_ID_3
    :   DMA channel 3

    enumerator HPDMA_ID_MAX
    :   DMA channel max
