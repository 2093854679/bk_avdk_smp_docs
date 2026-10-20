---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_hpdma.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="hpdma"></a>

# HPDMA

BK7259 AP 侧 HPDMA API（`include/driver/hpdma.h`）。详细说明见
[HPDMA 开发指南](../../developer-guide/peripheral/bk_hpdma.md)。

<a id="hpdma-api-reference"></a>

## HPDMA API Reference

<a id="header-file"></a>

### Header File

- [hpdma.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hpdma.h)

<a id="functions"></a>

### Functions

<a id="_CPPv420bk_hpdma_driver_initv"></a>

<a id="_CPPv320bk_hpdma_driver_initv"></a> <a id="_CPPv220bk_hpdma_driver_initv"></a> <a id="bk_hpdma_driver_init__void"></a> <a id="hpdma_8h_1aa574e6bced62bfbb4fb92d93a2d67f86"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_driver\_init(void)
:   Init the DMA driver.

    This API init the resoure common to all dma channels:

    - Init dma driver control memory

    This API should be called before any other dma APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_hpdma_driver_deinitv"></a>

<a id="_CPPv322bk_hpdma_driver_deinitv"></a> <a id="_CPPv222bk_hpdma_driver_deinitv"></a> <a id="bk_hpdma_driver_deinit__void"></a> <a id="hpdma_8h_1adcf2e9a4e6f53d53b81abaf8d533b9c6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_driver\_deinit(void)
:   Deinit the DMA driver.

    This API free all resource related to dma and power down all dma channels.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv414bk_hpdma_alloc3u16"></a>

<a id="_CPPv314bk_hpdma_alloc3u16"></a> <a id="_CPPv214bk_hpdma_alloc3u16"></a> <a id="bk_hpdma_alloc__u16"></a> <a id="hpdma_8h_1aa78138181b91e7f2b9451519a3b25082"></a> [hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") bk\_hpdma\_alloc(u16 user\_id)
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

<a id="_CPPv420bk_fixed_hpdma_alloc3u1610hpdma_id_t"></a>

<a id="_CPPv320bk_fixed_hpdma_alloc3u1610hpdma_id_t"></a> <a id="_CPPv220bk_fixed_hpdma_alloc3u1610hpdma_id_t"></a> <a id="bk_fixed_hpdma_alloc__u16.hpdma_id_t"></a> <a id="hpdma_8h_1a791b2f30b9a04be93d3d266dc0df771f"></a> [hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") bk\_fixed\_hpdma\_alloc(u16 user\_id, [hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") fixed\_chnl\_id)
:   Allocate a fixed DMA channel.Maybe some APP needs to have a fixed channel forever, then it can use this API.

    This API should be called before any other dma channel APIs.

    **Attention**
    :   : This API is just for CONFIG\_GDMA\_HW\_V2PX And CONFIG\_GDMA\_HW\_V1PX doesn’t support it.

    参数
    :   - **user\_id** – DMA channel applicant
        - **fixed\_chnl\_id** – application wants to get which fixed channel

    返回
    :   DMA channel id.

        - \> DMA\_ID\_MAX: if the fixed\_chnl\_id has been allocated, it will return DMA\_ID\_MAX which means error.
        - \> fixed\_chnl\_id: the fixed\_chnl\_id is allocated suc.

<a id="_CPPv413bk_hpdma_free3u1610hpdma_id_t"></a>

<a id="_CPPv313bk_hpdma_free3u1610hpdma_id_t"></a> <a id="_CPPv213bk_hpdma_free3u1610hpdma_id_t"></a> <a id="bk_hpdma_free__u16.hpdma_id_t"></a> <a id="hpdma_8h_1a499b86d2ed3b0cb286345631fad0d6ec"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_free(u16 user\_id, [hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Free the DMA channel.

    **Attention**
    :   : This API can only be called in task context,

        - and can’t be called in context that interrupt is disabled.

    参数
    :   - **user\_id** – DMA channel applicant, the same as in bk\_hpdma\_alloc.
        - **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_hpdma_force_reclaim3u1610hpdma_id_t"></a>

<a id="_CPPv322bk_hpdma_force_reclaim3u1610hpdma_id_t"></a> <a id="_CPPv222bk_hpdma_force_reclaim3u1610hpdma_id_t"></a> <a id="bk_hpdma_force_reclaim__u16.hpdma_id_t"></a> <a id="hpdma_8h_1a2749d434c8a74094bee68e64f69a4c3b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_force\_reclaim(u16 user\_id, [hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") chnl\_id)
:   Force release a channel that bk\_hpdma\_free() refused to release (S0/C: HPDMA stability review escape hatch).

    bk\_hpdma\_free() now performs a defensive stop \+ wait-to-idle and leaves the channel reserved if the engine does not honour the stop within HPDMA\_MAX\_BUSY\_TIME us. This API is the only sanctioned way to recover that stuck channel for re-use. It performs a per-channel register reset (NOT a full controller soft\_reset), clears the channel’s ISR callbacks and finally releases the bitmap entry. Any data the engine had not yet committed is lost; callers must release their associated buffers AFTER the channel is reclaimed (or with full awareness of the data-loss risk).

    备注

    Task context only. Do NOT call from ISR or with interrupts disabled.

    参数
    :   - **user\_id** – Same applicant token passed to bk\_hpdma\_alloc().
        - **chnl\_id** – Channel id originally returned by bk\_hpdma\_alloc().

    返回
    :   - BK\_OK: channel reclaimed
        - BK\_ERR\_HPDMA\_NOT\_INIT / BK\_ERR\_HPDMA\_ID / BK\_ERR\_PARAM otherwise

<a id="_CPPv434bk_hpdma_recover_after_low_voltagev"></a>

<a id="_CPPv334bk_hpdma_recover_after_low_voltagev"></a> <a id="_CPPv234bk_hpdma_recover_after_low_voltagev"></a> <a id="bk_hpdma_recover_after_low_voltage__void"></a> <a id="hpdma_8h_1a4d877ba8ed99a0442b4104c248861f44"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_recover\_after\_low\_voltage(void)
:   Recover global HPDMA controller registers after low-voltage wakeup (S2: HPDMA stability review).

    The controller-wide registers (soft\_reset / secure\_attr / privileged\_attr / prio\_mode) are powered down with the rest of the chip during low-voltage sleep and read back as zero on wakeup. Call this once from the PM wakeup hook BEFORE any client invokes bk\_hpdma\_init() / bk\_hpdma\_start().

    备注

    Do not call from per-transfer paths; that was the historical bug.

    返回
    :   BK\_OK on success.

<a id="_CPPv413bk_hpdma_user10hpdma_id_t"></a>

<a id="_CPPv313bk_hpdma_user10hpdma_id_t"></a> <a id="_CPPv213bk_hpdma_user10hpdma_id_t"></a> <a id="bk_hpdma_user__hpdma_id_t"></a> <a id="hpdma_8h_1a49e97db9f471219652464d2fc5c7ed0d"></a> uint32\_t bk\_hpdma\_user([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   get the user of DMA channel

    参数
    :   **id** – DMA channel

    返回
    :   DMA channel user\_id.

        - u32: high u16 is the CPU\_ID, low 16 bits is the applicant\_id.

<a id="_CPPv413bk_hpdma_init10hpdma_id_tPK14hpdma_config_t"></a>

<a id="_CPPv313bk_hpdma_init10hpdma_id_tPK14hpdma_config_t"></a> <a id="_CPPv213bk_hpdma_init10hpdma_id_tPK14hpdma_config_t"></a> <a id="bk_hpdma_init__hpdma_id_t.hpdma_config_tCP"></a> <a id="hpdma_8h_1abf6c5ca78254f0e1166af4fdddee3333"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_init([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, const [hpdma\_config\_t](#_CPPv414hpdma_config_t "hpdma_config_t") \*config)
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

<a id="_CPPv415bk_hpdma_deinit10hpdma_id_t"></a>

<a id="_CPPv315bk_hpdma_deinit10hpdma_id_t"></a> <a id="_CPPv215bk_hpdma_deinit10hpdma_id_t"></a> <a id="bk_hpdma_deinit__hpdma_id_t"></a> <a id="hpdma_8h_1af714b806f17f73ff72ac9499b060bafd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_deinit([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Deinit a DMA channel.

    This API deinit the DMA channel:

    - Stop the DMA channel
    - Reset all configuration of DMA channel to default value

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv414bk_hpdma_start10hpdma_id_t"></a>

<a id="_CPPv314bk_hpdma_start10hpdma_id_t"></a> <a id="_CPPv214bk_hpdma_start10hpdma_id_t"></a> <a id="bk_hpdma_start__hpdma_id_t"></a> <a id="hpdma_8h_1a8f42403b69b3d7ba83ac48de011a6692"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_start([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Start a DMA channel.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv413bk_hpdma_stop10hpdma_id_t"></a>

<a id="_CPPv313bk_hpdma_stop10hpdma_id_t"></a> <a id="_CPPv213bk_hpdma_stop10hpdma_id_t"></a> <a id="bk_hpdma_stop__hpdma_id_t"></a> <a id="hpdma_8h_1a6cffff4d50100581c4079874f662d1a8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_stop([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Stop a DMA channel.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_hpdma_wait_to_idle10hpdma_id_t"></a>

<a id="_CPPv321bk_hpdma_wait_to_idle10hpdma_id_t"></a> <a id="_CPPv221bk_hpdma_wait_to_idle10hpdma_id_t"></a> <a id="bk_hpdma_wait_to_idle__hpdma_id_t"></a> <a id="hpdma_8h_1ae0d8e169a154eca9c138a6cb21a9acd7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_wait\_to\_idle([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Wait until the given DMA channel becomes idle (S1: hpdma stability).

    Polls the channel’s hardware enable bit (and for HPDMA\_WORK\_MODE\_REPEAT issues a stop first) up to HPDMA\_MAX\_BUSY\_TIME microseconds.

    Callers should invoke this before touching channel registers (e.g. changing the destination address / data width) or before tearing down DMA target buffers, to avoid the use-after-free / mid-transfer write hazards described in the HPDMA stability review.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: channel is idle
        - BK\_ERR\_HPDMA\_TIMEOUT: channel still busy after HPDMA\_MAX\_BUSY\_TIME us
        - other negative: parameter / not-initialized errors

<a id="_CPPv432bk_hpdma_enable_finish_interrupt10hpdma_id_t"></a>

<a id="_CPPv332bk_hpdma_enable_finish_interrupt10hpdma_id_t"></a> <a id="_CPPv232bk_hpdma_enable_finish_interrupt10hpdma_id_t"></a> <a id="bk_hpdma_enable_finish_interrupt__hpdma_id_t"></a> <a id="hpdma_8h_1a4017fdab7654d4f6e92b5e79207410b4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_enable\_finish\_interrupt([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA finish intterrup.

    @NOTES before enable interrupt, please confirm have called bk\_hpdma\_register\_isr.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv433bk_hpdma_disable_finish_interrupt10hpdma_id_t"></a>

<a id="_CPPv333bk_hpdma_disable_finish_interrupt10hpdma_id_t"></a> <a id="_CPPv233bk_hpdma_disable_finish_interrupt10hpdma_id_t"></a> <a id="bk_hpdma_disable_finish_interrupt__hpdma_id_t"></a> <a id="hpdma_8h_1ae08f1fb4afc058126020c1c693ef89a9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_disable\_finish\_interrupt([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA finish intterrup.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv437bk_hpdma_enable_half_finish_interrupt10hpdma_id_t"></a>

<a id="_CPPv337bk_hpdma_enable_half_finish_interrupt10hpdma_id_t"></a> <a id="_CPPv237bk_hpdma_enable_half_finish_interrupt10hpdma_id_t"></a> <a id="bk_hpdma_enable_half_finish_interrupt__hpdma_id_t"></a> <a id="hpdma_8h_1a660c48e1e7987bae6dd0ecbccb6e72db"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_enable\_half\_finish\_interrupt([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA half finish intterrup.

    @NOTES before enable interrupt, please confirm have called bk\_hpdma\_register\_isr.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv438bk_hpdma_disable_half_finish_interrupt10hpdma_id_t"></a>

<a id="_CPPv338bk_hpdma_disable_half_finish_interrupt10hpdma_id_t"></a> <a id="_CPPv238bk_hpdma_disable_half_finish_interrupt10hpdma_id_t"></a> <a id="bk_hpdma_disable_half_finish_interrupt__hpdma_id_t"></a> <a id="hpdma_8h_1a01b272ae4fca3d9150aba598fe07607b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_disable\_half\_finish\_interrupt([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA half finish intterrup.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv433bk_hpdma_enable_bus_err_interrupt10hpdma_id_t"></a>

<a id="_CPPv333bk_hpdma_enable_bus_err_interrupt10hpdma_id_t"></a> <a id="_CPPv233bk_hpdma_enable_bus_err_interrupt10hpdma_id_t"></a> <a id="bk_hpdma_enable_bus_err_interrupt__hpdma_id_t"></a> <a id="hpdma_8h_1ae6944f4637a3218c86596e427e0486c3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_enable\_bus\_err\_interrupt([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA bus error interrupt.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv434bk_hpdma_disable_bus_err_interrupt10hpdma_id_t"></a>

<a id="_CPPv334bk_hpdma_disable_bus_err_interrupt10hpdma_id_t"></a> <a id="_CPPv234bk_hpdma_disable_bus_err_interrupt10hpdma_id_t"></a> <a id="bk_hpdma_disable_bus_err_interrupt__hpdma_id_t"></a> <a id="hpdma_8h_1a1e7b787d649f228b07cddb1188fd9322"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_disable\_bus\_err\_interrupt([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA bus error interrupt.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_hpdma_register_isr10hpdma_id_t11hpdma_isr_tPv11hpdma_isr_tPv"></a>

<a id="_CPPv321bk_hpdma_register_isr10hpdma_id_t11hpdma_isr_tPv11hpdma_isr_tPv"></a> <a id="_CPPv221bk_hpdma_register_isr10hpdma_id_t11hpdma_isr_tPv11hpdma_isr_tPv"></a> <a id="bk_hpdma_register_isr__hpdma_id_t.hpdma_isr_t.voidP.hpdma_isr_t.voidP"></a> <a id="hpdma_8h_1aa90b7c9ad7954a549e0eacf883018136"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_register\_isr([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, [hpdma\_isr\_t](#_CPPv411hpdma_isr_t "hpdma_isr_t") half\_finish\_isr, void \*half\_finish\_data, [hpdma\_isr\_t](#_CPPv411hpdma_isr_t "hpdma_isr_t") finish\_isr, void \*finish\_data)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function with user data parameter.

    参数
    :   - **id** – DMA channel
        - **half\_finish\_isr** – DMA half finish callback
        - **half\_finish\_data** – User data for half finish callback (can be NULL)
        - **finish\_isr** – DMA finish callback
        - **finish\_data** – User data for finish callback (can be NULL)

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv429bk_hpdma_register_bus_err_isr10hpdma_id_t11hpdma_isr_tPv"></a>

<a id="_CPPv329bk_hpdma_register_bus_err_isr10hpdma_id_t11hpdma_isr_tPv"></a> <a id="_CPPv229bk_hpdma_register_bus_err_isr10hpdma_id_t11hpdma_isr_tPv"></a> <a id="bk_hpdma_register_bus_err_isr__hpdma_id_t.hpdma_isr_t.voidP"></a> <a id="hpdma_8h_1ac5723081f4597c2e8a42830ea4529360"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_register\_bus\_err\_isr([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, [hpdma\_isr\_t](#_CPPv411hpdma_isr_t "hpdma_isr_t") bus\_err\_isr, void \*user\_data)
:   Register the interrupt service routine for DMA channel.

    This API regist dma isr callback function with user data parameter.

    参数
    :   - **id** – DMA channel
        - **bus\_err\_isr** – DMA bus error callback
        - **user\_data** – User data for bus error callback (can be NULL)

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv430bk_hpdma_register_fifo_err_isr10hpdma_id_t11hpdma_isr_tPv"></a>

<a id="_CPPv330bk_hpdma_register_fifo_err_isr10hpdma_id_t11hpdma_isr_tPv"></a> <a id="_CPPv230bk_hpdma_register_fifo_err_isr10hpdma_id_t11hpdma_isr_tPv"></a> <a id="bk_hpdma_register_fifo_err_isr__hpdma_id_t.hpdma_isr_t.voidP"></a> <a id="hpdma_8h_1ac77456badc86cdfa5360f9cf84804ac4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_register\_fifo\_err\_isr([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, [hpdma\_isr\_t](#_CPPv411hpdma_isr_t "hpdma_isr_t") fifo\_err\_isr, void \*user\_data)
:   Register a callback for the fifo\_err interrupt class (P0: HPDMA review).

    fifo\_err is the 4th error class on Reg23/Reg28 (bit17 in status). It was previously not wired up; callers that enable it via bk\_hpdma\_enable\_fifo\_err\_interrupt() can use this to be notified after the ISR has halted the engine.

    参数
    :   - **id** – DMA channel
        - **fifo\_err\_isr** – Callback (NULL to clear)
        - **user\_data** – Opaque user pointer

    返回
    :   BK\_OK on success.

<a id="_CPPv434bk_hpdma_enable_fifo_err_interrupt10hpdma_id_t"></a>

<a id="_CPPv334bk_hpdma_enable_fifo_err_interrupt10hpdma_id_t"></a> <a id="_CPPv234bk_hpdma_enable_fifo_err_interrupt10hpdma_id_t"></a> <a id="bk_hpdma_enable_fifo_err_interrupt__hpdma_id_t"></a> <a id="hpdma_8h_1a1cf3856acb7f6da313de8efc99d41b54"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_enable\_fifo\_err\_interrupt([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable / disable the fifo\_err interrupt for a DMA channel (P0: HPDMA review).

<a id="_CPPv435bk_hpdma_disable_fifo_err_interrupt10hpdma_id_t"></a>

<a id="_CPPv335bk_hpdma_disable_fifo_err_interrupt10hpdma_id_t"></a> <a id="_CPPv235bk_hpdma_disable_fifo_err_interrupt10hpdma_id_t"></a> <a id="bk_hpdma_disable_fifo_err_interrupt__hpdma_id_t"></a> <a id="hpdma_8h_1afc3b8069f697990584e094f0111bff83"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_disable\_fifo\_err\_interrupt([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)

<a id="_CPPv427bk_hpdma_set_src_start_addr10hpdma_id_t8uint32_t"></a>

<a id="_CPPv327bk_hpdma_set_src_start_addr10hpdma_id_t8uint32_t"></a> <a id="_CPPv227bk_hpdma_set_src_start_addr10hpdma_id_t8uint32_t"></a> <a id="bk_hpdma_set_src_start_addr__hpdma_id_t.uint32_t"></a> <a id="hpdma_8h_1af6fe20378e54b425d04ae387f5661dae"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_set\_src\_start\_addr([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, uint32\_t start\_addr)
:   Set DMA source start address.

    参数
    :   - **id** – DMA channel
        - **start\_addr** – DMA source start address (pass the CPU-side 0x2C alias; the driver converts it to the HPDMA-visible 0x28 alias)

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv428bk_hpdma_set_dest_start_addr10hpdma_id_t8uint32_t"></a>

<a id="_CPPv328bk_hpdma_set_dest_start_addr10hpdma_id_t8uint32_t"></a> <a id="_CPPv228bk_hpdma_set_dest_start_addr10hpdma_id_t8uint32_t"></a> <a id="bk_hpdma_set_dest_start_addr__hpdma_id_t.uint32_t"></a> <a id="hpdma_8h_1a51c6f3d7b71ca63607aa7df43da475fc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_set\_dest\_start\_addr([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, uint32\_t start\_addr)
:   Set DMA dest start address.

    参数
    :   - **id** – DMA channel
        - **start\_addr** – DMA dest start address (pass the CPU-side 0x2C alias; the driver converts it to the HPDMA-visible 0x28 alias)

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv433bk_hpdma_enable_src_addr_increase10hpdma_id_t"></a>

<a id="_CPPv333bk_hpdma_enable_src_addr_increase10hpdma_id_t"></a> <a id="_CPPv233bk_hpdma_enable_src_addr_increase10hpdma_id_t"></a> <a id="bk_hpdma_enable_src_addr_increase__hpdma_id_t"></a> <a id="hpdma_8h_1a4933d7320c7d5fe045441f6d9d367003"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_enable\_src\_addr\_increase([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA source address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv434bk_hpdma_disable_src_addr_increase10hpdma_id_t"></a>

<a id="_CPPv334bk_hpdma_disable_src_addr_increase10hpdma_id_t"></a> <a id="_CPPv234bk_hpdma_disable_src_addr_increase10hpdma_id_t"></a> <a id="bk_hpdma_disable_src_addr_increase__hpdma_id_t"></a> <a id="hpdma_8h_1a9cf3ac131867be289d279b951818e408"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_disable\_src\_addr\_increase([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA source address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv429bk_hpdma_enable_src_addr_loop10hpdma_id_t"></a>

<a id="_CPPv329bk_hpdma_enable_src_addr_loop10hpdma_id_t"></a> <a id="_CPPv229bk_hpdma_enable_src_addr_loop10hpdma_id_t"></a> <a id="bk_hpdma_enable_src_addr_loop__hpdma_id_t"></a> <a id="hpdma_8h_1a5dc698dfcaf60b9e57d24b77cab663fb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_enable\_src\_addr\_loop([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA source address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv430bk_hpdma_disable_src_addr_loop10hpdma_id_t"></a>

<a id="_CPPv330bk_hpdma_disable_src_addr_loop10hpdma_id_t"></a> <a id="_CPPv230bk_hpdma_disable_src_addr_loop10hpdma_id_t"></a> <a id="bk_hpdma_disable_src_addr_loop__hpdma_id_t"></a> <a id="hpdma_8h_1ad72d9b9880117f8dd175946f50c9847f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_disable\_src\_addr\_loop([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA source address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv434bk_hpdma_enable_dest_addr_increase10hpdma_id_t"></a>

<a id="_CPPv334bk_hpdma_enable_dest_addr_increase10hpdma_id_t"></a> <a id="_CPPv234bk_hpdma_enable_dest_addr_increase10hpdma_id_t"></a> <a id="bk_hpdma_enable_dest_addr_increase__hpdma_id_t"></a> <a id="hpdma_8h_1a9439044c15201299aec1ce35fd5d45a9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_enable\_dest\_addr\_increase([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA dest address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv435bk_hpdma_disable_dest_addr_increase10hpdma_id_t"></a>

<a id="_CPPv335bk_hpdma_disable_dest_addr_increase10hpdma_id_t"></a> <a id="_CPPv235bk_hpdma_disable_dest_addr_increase10hpdma_id_t"></a> <a id="bk_hpdma_disable_dest_addr_increase__hpdma_id_t"></a> <a id="hpdma_8h_1aee23cea07a551344d6070eba8b0eaef6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_disable\_dest\_addr\_increase([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA dest address increase.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv430bk_hpdma_enable_dest_addr_loop10hpdma_id_t"></a>

<a id="_CPPv330bk_hpdma_enable_dest_addr_loop10hpdma_id_t"></a> <a id="_CPPv230bk_hpdma_enable_dest_addr_loop10hpdma_id_t"></a> <a id="bk_hpdma_enable_dest_addr_loop__hpdma_id_t"></a> <a id="hpdma_8h_1a77f9464556e6805088b86d68ad085b52"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_enable\_dest\_addr\_loop([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Enable DMA dest address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv431bk_hpdma_disable_dest_addr_loop10hpdma_id_t"></a>

<a id="_CPPv331bk_hpdma_disable_dest_addr_loop10hpdma_id_t"></a> <a id="_CPPv231bk_hpdma_disable_dest_addr_loop10hpdma_id_t"></a> <a id="bk_hpdma_disable_dest_addr_loop__hpdma_id_t"></a> <a id="hpdma_8h_1a2fdbdb1108a633563c0eb08cf0710e0a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_disable\_dest\_addr\_loop([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Disable DMA dest address loop.

    参数
    :   **id** – DMA channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_hpdma_get_remain_len10hpdma_id_t"></a>

<a id="_CPPv323bk_hpdma_get_remain_len10hpdma_id_t"></a> <a id="_CPPv223bk_hpdma_get_remain_len10hpdma_id_t"></a> <a id="bk_hpdma_get_remain_len__hpdma_id_t"></a> <a id="hpdma_8h_1adc981de4d1eb2b870bd9cd00c5b92f6f"></a> uint32\_t bk\_hpdma\_get\_remain\_len([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Get DMA transfer remain length.

    参数
    :   **id** – DMA channel

    返回
    :   DMA transfer remain length

<a id="_CPPv426bk_hpdma_get_enable_status10hpdma_id_t"></a>

<a id="_CPPv326bk_hpdma_get_enable_status10hpdma_id_t"></a> <a id="_CPPv226bk_hpdma_get_enable_status10hpdma_id_t"></a> <a id="bk_hpdma_get_enable_status__hpdma_id_t"></a> <a id="hpdma_8h_1a843f54379ccb94a3bbb91ab53df8a0d2"></a> uint32\_t bk\_hpdma\_get\_enable\_status([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Gets the current DMA channel working status.

    参数
    :   **id** – DMA channel

    返回
    :   - 0: Channel idle state
        - others: Channel busy state.

<a id="_CPPv425bk_hpdma_flush_src_buffer10hpdma_id_t"></a>

<a id="_CPPv325bk_hpdma_flush_src_buffer10hpdma_id_t"></a> <a id="_CPPv225bk_hpdma_flush_src_buffer10hpdma_id_t"></a> <a id="bk_hpdma_flush_src_buffer__hpdma_id_t"></a> <a id="hpdma_8h_1a9675684e6eda2821ae30000ebc750a7d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_flush\_src\_buffer([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   flush reserved data in dma internal buffer I.E:If source data width is not 4bytes, and data size isn’t 4bytes align, but dest data width is 4bytes, then maybe 1\~3 bytes data reserved in dma internal buffer, then the left 1\~3 bytes data not copy to dest address.

    参数
    :   - **id** – DMA channel
        - **attr** – DMA privileged attr

    返回
    :   - 0: Channel idle state
        - others: Channel busy state.

<a id="_CPPv425bk_hpdma_set_next_ll_addr10hpdma_id_t8uint32_t"></a>

<a id="_CPPv325bk_hpdma_set_next_ll_addr10hpdma_id_t8uint32_t"></a> <a id="_CPPv225bk_hpdma_set_next_ll_addr10hpdma_id_t8uint32_t"></a> <a id="bk_hpdma_set_next_ll_addr__hpdma_id_t.uint32_t"></a> <a id="hpdma_8h_1a02467ca6ecdb9d298cb80762aed0d440"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_set\_next\_ll\_addr([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, uint32\_t ll\_addr)
:   Set next linked list address.

    参数
    :   - **id** – DMA channel
        - **ll\_addr** – Linked list address (pass the CPU-side 0x2C alias; the driver converts it to the HPDMA-visible 0x28 alias)

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_hpdma_get_next_ll_addr10hpdma_id_t"></a>

<a id="_CPPv325bk_hpdma_get_next_ll_addr10hpdma_id_t"></a> <a id="_CPPv225bk_hpdma_get_next_ll_addr10hpdma_id_t"></a> <a id="bk_hpdma_get_next_ll_addr__hpdma_id_t"></a> <a id="hpdma_8h_1ae9c89f834449f07d09dacd293c37e63d"></a> uint32\_t bk\_hpdma\_get\_next\_ll\_addr([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id)
:   Get next linked list address.

    备注

    Returns the raw 0x28 peripheral alias from the hardware register; it is NOT converted back to 0x2C. Today it is only used for a done-check (compare against 0, which is alias-agnostic). If you need to compare it against a 0x2C pointer you hold, or subtract a base address, convert first with SOC\_SRAM\_CPU\_ADDR().

    参数
    :   **id** – DMA channel

    返回
    :   Next linked list address (0x28 peripheral alias)

<a id="_CPPv418bk_hpdma_link_init8uint32_t"></a>

<a id="_CPPv318bk_hpdma_link_init8uint32_t"></a> <a id="_CPPv218bk_hpdma_link_init8uint32_t"></a> <a id="bk_hpdma_link_init__uint32_t"></a> <a id="hpdma_8h_1a069eb747b8f8f164a7a126abc6269c35"></a> void \*bk\_hpdma\_link\_init(uint32\_t link\_cnt)
:   Initialize linked list descriptor table.

    This API allocates and initializes a descriptor table for linked list DMA transfers.

    备注

    The next\_desc\_addr chain pointers between descriptors are converted 0x2C-\>0x28 by this API. After you get the returned desc\_table, only fill it via bk\_hpdma\_link\_set\_desc(); do NOT write the [hpdma\_descriptor\_t](#structhpdma__descriptor__t) fields directly (see the SRAM address-alias contract at the top of this file).

    参数
    :   **link\_cnt** – Number of descriptors in the linked list

    返回
    :   - Pointer to the first descriptor (16-byte aligned) on success
        - NULL on failure (memory allocation failed)

<a id="_CPPv420bk_hpdma_link_deinitPv"></a>

<a id="_CPPv320bk_hpdma_link_deinitPv"></a> <a id="_CPPv220bk_hpdma_link_deinitPv"></a> <a id="bk_hpdma_link_deinit__voidP"></a> <a id="hpdma_8h_1a9574bf5f86a2ccac1e1fbaadbeaa0223"></a> void bk\_hpdma\_link\_deinit(void \*desc\_table)
:   Deinitialize linked list descriptor table.

    This API frees the memory allocated for the descriptor table.

    参数
    :   **desc\_table** – Descriptor table pointer returned by bk\_hpdma\_link\_init

<a id="_CPPv422bk_hpdma_link_set_descPv8uint32_tPK19hpdma_link_config_t"></a>

<a id="_CPPv322bk_hpdma_link_set_descPv8uint32_tPK19hpdma_link_config_t"></a> <a id="_CPPv222bk_hpdma_link_set_descPv8uint32_tPK19hpdma_link_config_t"></a> <a id="bk_hpdma_link_set_desc__voidP.uint32_t.hpdma_link_config_tCP"></a> <a id="hpdma_8h_1a2a7dd5c8adc0cf466e29d5d0d9ae9f44"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_link\_set\_desc(void \*desc\_table, uint32\_t index, const [hpdma\_link\_config\_t](#_CPPv419hpdma_link_config_t "hpdma_link_config_t") \*config)
:   Set a single descriptor in the linked list.

    This API configures a descriptor at the specified index for DMA transfer. Supports both 1D and 2D transfers.

    备注

    config src\_addr/dst\_addr take the CPU-side 0x2C alias; this API applies the 0x2C-\>0x28 conversion when writing the descriptor. This is the only supported entry point for building linked-list descriptors \- do not bypass it and write the descriptor struct directly (see the SRAM address-alias contract at the top of this file).

    参数
    :   - **desc\_table** – Descriptor table pointer
        - **index** – Descriptor index
        - **config** – Transfer configuration (for 1D: set ysize\=1, step\=0)

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: invalid parameters
        - BK\_ERR\_PARAM: invalid parameters

<a id="_CPPv423bk_hpdma_link_set_descsPvPK19hpdma_link_config_t8uint32_t"></a>

<a id="_CPPv323bk_hpdma_link_set_descsPvPK19hpdma_link_config_t8uint32_t"></a> <a id="_CPPv223bk_hpdma_link_set_descsPvPK19hpdma_link_config_t8uint32_t"></a> <a id="bk_hpdma_link_set_descs__voidP.hpdma_link_config_tCP.uint32_t"></a> <a id="hpdma_8h_1a58d418d73307ee4c123545132f829d2b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_link\_set\_descs(void \*desc\_table, const [hpdma\_link\_config\_t](#_CPPv419hpdma_link_config_t "hpdma_link_config_t") \*configs, uint32\_t link\_cnt)
:   Set multiple descriptors in the linked list.

    This API configures multiple descriptors for DMA transfer. Supports both 1D and 2D transfers.

    参数
    :   - **desc\_table** – Descriptor table pointer
        - **configs** – Configuration array (for 1D: set ysize\=1, step\=0)
        - **link\_cnt** – Number of descriptors to configure

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: invalid parameters
        - others: other errors

<a id="_CPPv422bk_hpdma_link_transfer10hpdma_id_tPv"></a>

<a id="_CPPv322bk_hpdma_link_transfer10hpdma_id_tPv"></a> <a id="_CPPv222bk_hpdma_link_transfer10hpdma_id_tPv"></a> <a id="bk_hpdma_link_transfer__hpdma_id_t.voidP"></a> <a id="hpdma_8h_1a7d030e5a392058cf9a7f9bf0e9f7c6a9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_link\_transfer([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") id, void \*desc\_table)
:   Execute linked list transfer (Asynchronous)

    This API configures the DMA channel and starts the transfer. The DMA channel ID must be allocated by the application layer using bk\_hpdma\_alloc(). The function returns after the transfer is started (not necessarily completed).

    参数
    :   - **id** – DMA channel ID (allocated by application layer using bk\_hpdma\_alloc())
        - **desc\_table** – Descriptor table pointer

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: invalid descriptor table
        - BK\_ERR\_HPDMA\_ID: invalid DMA channel ID
        - others: other errors

<a id="_CPPv415bk_hpdma_memcpyPvPKv8uint32_t"></a>

<a id="_CPPv315bk_hpdma_memcpyPvPKv8uint32_t"></a> <a id="_CPPv215bk_hpdma_memcpyPvPKv8uint32_t"></a> <a id="bk_hpdma_memcpy__voidP.voidCP.uint32_t"></a> <a id="hpdma_8h_1ab29dd88a21f89d5cbfbaa0a4641171c5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_memcpy(void \*out, const void \*in, uint32\_t len)
:   Memory copy using HPDMA.

    This API performs a memory copy operation using HPDMA. It automatically allocates a DMA channel, performs the transfer, and frees the channel.

    Length is no longer limited to the 16-bit single-shot size: transfers larger than HPDMA\_SINGLE\_MAX\_XFER (0xF000 bytes) are automatically split into a linked list of chunks and kicked as a single chain.

    When called from task context (scheduler running, not suspended), completion is awaited on a semaphore posted by the finish interrupt, so the CPU is yielded instead of busy-waiting. In non-blockable contexts (ISR / critical section) it falls back to a bounded busy-poll. If the DMA path fails for any reason, it transparently falls back to a CPU copy so the data is always correct.

    参数
    :   - **out** – Destination address
        - **in** – Source address
        - **len** – Number of bytes to copy

    返回
    :   - BK\_OK: succeed (including successful CPU fallback)
        - BK\_ERR\_NULL\_PARAM: out or in is NULL
        - others: other errors

<a id="_CPPv420bk_hpdma_memcpy_linkPvPKv8uint32_t10hpdma_id_t"></a>

<a id="_CPPv320bk_hpdma_memcpy_linkPvPKv8uint32_t10hpdma_id_t"></a> <a id="_CPPv220bk_hpdma_memcpy_linkPvPKv8uint32_t10hpdma_id_t"></a> <a id="bk_hpdma_memcpy_link__voidP.voidCP.uint32_t.hpdma_id_t"></a> <a id="hpdma_8h_1a50f546a7f46a7f61d49dbba0a8b17bcc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_hpdma\_memcpy\_link(void \*out, const void \*in, uint32\_t len, [hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") cpy\_chnl)
:   Memory copy using HPDMA on a caller-owned channel.

    Same behaviour as bk\_hpdma\_memcpy() (arbitrary length via linked-list split, interrupt/semaphore completion with busy-poll fallback) but on a channel the caller has already allocated with bk\_hpdma\_alloc(). The channel is NOT freed by this call. No CPU fallback is performed; the DMA error is returned so the caller can decide how to recover.

    参数
    :   - **out** – Destination address
        - **in** – Source address
        - **len** – Number of bytes to copy
        - **cpy\_chnl** – DMA channel allocated by the caller

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: out or in is NULL
        - BK\_ERR\_HPDMA\_ID: invalid channel id
        - others: other errors

<a id="hpdma-api-typedefs"></a>

## HPDMA API Typedefs

<a id="id1"></a>

### Header File

- [hpdma\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hpdma_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv416hpdma_isr_info_t"></a>

<a id="_CPPv316hpdma_isr_info_t"></a> <a id="_CPPv216hpdma_isr_info_t"></a> <a id="hpdma_isr_info_t"></a> <a id="structhpdma__isr__info__t"></a> struct hpdma\_isr\_info\_t
:   DMA interrupt service routine with user data.

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_HPDMA_ID"></a>

<a id="group__bk__api__hpdma__defs_1ga1ad03227a02018e294b4d8cf3ab92566"></a> BK\_ERR\_HPDMA\_ID
:   HPDMA id is invalid

<a id="c.BK_ERR_HPDMA_NOT_INIT"></a>

<a id="group__bk__api__hpdma__defs_1ga44f54fd62396878d1498a441c0ac7135"></a> BK\_ERR\_HPDMA\_NOT\_INIT
:   HPDMA driver not init

<a id="c.BK_ERR_HPDMA_ID_NOT_INIT"></a>

<a id="group__bk__api__hpdma__defs_1ga8ab62e75b13c7a2599743d4953211231"></a> BK\_ERR\_HPDMA\_ID\_NOT\_INIT
:   HPDMA id not init

<a id="c.BK_ERR_HPDMA_ID_NOT_START"></a>

<a id="group__bk__api__hpdma__defs_1gac25a5977a93b5bc733c6254bfee46d7b"></a> BK\_ERR\_HPDMA\_ID\_NOT\_START
:   HPDMA id not start

<a id="c.BK_ERR_HPDMA_INVALID_ADDR"></a>

<a id="group__bk__api__hpdma__defs_1ga0990cbe1df724c3c925b823a6507c893"></a> BK\_ERR\_HPDMA\_INVALID\_ADDR
:   HPDMA addr is invalid

<a id="c.BK_ERR_HPDMA_ID_REINIT"></a>

<a id="group__bk__api__hpdma__defs_1ga1aaf11a9dd124adcd49ea5dcd1b32629"></a> BK\_ERR\_HPDMA\_ID\_REINIT
:   HPDMA id has inited, if reinit,please de-init firstly

<a id="c.BK_ERR_HPDMA_TRANS_LEN"></a>

<a id="group__bk__api__hpdma__defs_1gad6eae9e8d4187dfb9002235176ed6e15"></a> BK\_ERR\_HPDMA\_TRANS\_LEN
:   HPDMA trans len is invalid

<a id="c.BK_ERR_HPDMA_TIMEOUT"></a>

<a id="group__bk__api__hpdma__defs_1gaa61467b07eda3b0ac54bc29dfb3e76de"></a> BK\_ERR\_HPDMA\_TIMEOUT
:   HPDMA wait-to-idle timeout (channel still busy)

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv411hpdma_isr_t"></a>

<a id="_CPPv311hpdma_isr_t"></a> <a id="_CPPv211hpdma_isr_t"></a> <a id="hpdma_isr_t"></a> <a id="group__bk__api__hpdma__defs_1gab030f660e75033fdac576ed287c14dcb"></a> typedef void (\*hpdma\_isr\_t)([hpdma\_id\_t](#_CPPv410hpdma_id_t "hpdma_id_t") hpdma\_id, void \*user\_data)
:   DMA interrupt service routine.

<a id="id2"></a>

### Header File

- [hal\_hpdma\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_hpdma_types.h)

<a id="id3"></a>

### Structures

<a id="_CPPv419hpdma_port_config_t"></a>

<a id="_CPPv319hpdma_port_config_t"></a> <a id="_CPPv219hpdma_port_config_t"></a> <a id="hpdma_port_config_t"></a> <a id="structhpdma__port__config__t"></a> struct hpdma\_port\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19hpdma_port_config_t3devE"></a>

    <a id="_CPPv3N19hpdma_port_config_t3devE"></a> <a id="_CPPv2N19hpdma_port_config_t3devE"></a> <a id="hpdma_port_config_t::dev__hpdma_dev_t"></a> <a id="group__bk__api__dma__enum_1ga52b720c8f7013f1a157fe901a3a8bb01"></a> [hpdma\_dev\_t](#_CPPv411hpdma_dev_t "hpdma_dev_t") dev
    :   DMA device

    <a id="_CPPv4N19hpdma_port_config_t5widthE"></a>

    <a id="_CPPv3N19hpdma_port_config_t5widthE"></a> <a id="_CPPv2N19hpdma_port_config_t5widthE"></a> <a id="hpdma_port_config_t::width__hpdma_data_width_t"></a> <a id="group__bk__api__dma__enum_1gaa265bc52f025abd23bcc7e447042559e"></a> [hpdma\_data\_width\_t](#_CPPv418hpdma_data_width_t "hpdma_data_width_t") width
    :   DMA data width

    <a id="_CPPv4N19hpdma_port_config_t11addr_inc_enE"></a>

    <a id="_CPPv3N19hpdma_port_config_t11addr_inc_enE"></a> <a id="_CPPv2N19hpdma_port_config_t11addr_inc_enE"></a> <a id="hpdma_port_config_t::addr_inc_en__hpdma_addr_inc_t"></a> <a id="group__bk__api__dma__enum_1ga37d2ef9bc958024dbcd2220b49ab7f50"></a> [hpdma\_addr\_inc\_t](#_CPPv416hpdma_addr_inc_t "hpdma_addr_inc_t") addr\_inc\_en
    :   enable/disable DMA address increase

    <a id="_CPPv4N19hpdma_port_config_t12addr_loop_enE"></a>

    <a id="_CPPv3N19hpdma_port_config_t12addr_loop_enE"></a> <a id="_CPPv2N19hpdma_port_config_t12addr_loop_enE"></a> <a id="hpdma_port_config_t::addr_loop_en__hpdma_addr_loop_t"></a> <a id="group__bk__api__dma__enum_1gadbfe45eca39587e798a0e1d6cb536b44"></a> [hpdma\_addr\_loop\_t](#_CPPv417hpdma_addr_loop_t "hpdma_addr_loop_t") addr\_loop\_en
    :   enable/disable DMA address loop

    <a id="_CPPv4N19hpdma_port_config_t10start_addrE"></a>

    <a id="_CPPv3N19hpdma_port_config_t10start_addrE"></a> <a id="_CPPv2N19hpdma_port_config_t10start_addrE"></a> <a id="hpdma_port_config_t::start_addr__uint32_t"></a> <a id="group__bk__api__dma__enum_1ga459f53926185992bbacc036b060c7939"></a> uint32\_t start\_addr
    :   DMA start address

    <a id="_CPPv4N19hpdma_port_config_t5xsizeE"></a>

    <a id="_CPPv3N19hpdma_port_config_t5xsizeE"></a> <a id="_CPPv2N19hpdma_port_config_t5xsizeE"></a> <a id="hpdma_port_config_t::xsize__uint16_t"></a> <a id="group__bk__api__dma__enum_1ga4d72b514f98a57032f8660420459ad58"></a> uint16\_t xsize
    :   X-direction length (Reg20: src\_xsize\[15:0\] or dest\_xsize\[31:16\]) (number of bytes per row)

    <a id="_CPPv4N19hpdma_port_config_t5ysizeE"></a>

    <a id="_CPPv3N19hpdma_port_config_t5ysizeE"></a> <a id="_CPPv2N19hpdma_port_config_t5ysizeE"></a> <a id="hpdma_port_config_t::ysize__uint16_t"></a> <a id="group__bk__api__dma__enum_1ga7629847009b187f2a6a9b21b879dd320"></a> uint16\_t ysize
    :   Y-direction length (Reg22: src\_ysize\[15:0\] or dest\_ysize\[31:16\]) (number of rows, 1 means 1 row)

    <a id="_CPPv4N19hpdma_port_config_t4stepE"></a>

    <a id="_CPPv3N19hpdma_port_config_t4stepE"></a> <a id="_CPPv2N19hpdma_port_config_t4stepE"></a> <a id="hpdma_port_config_t::step__uint16_t"></a> <a id="group__bk__api__dma__enum_1gaaee92c3b3f84dfe8d6be72d98c80824a"></a> uint16\_t step
    :   Address step between adjacent data (Reg29: src\_step\[14:0\] or dest\_step\[29:15\])

<a id="_CPPv414hpdma_config_t"></a>

<a id="_CPPv314hpdma_config_t"></a> <a id="_CPPv214hpdma_config_t"></a> <a id="hpdma_config_t"></a> <a id="structhpdma__config__t"></a> struct hpdma\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14hpdma_config_t4modeE"></a>

    <a id="_CPPv3N14hpdma_config_t4modeE"></a> <a id="_CPPv2N14hpdma_config_t4modeE"></a> <a id="hpdma_config_t::mode__hpdma_work_mode_t"></a> <a id="group__bk__api__dma__enum_1gac24df156fd192a3a96416717db654d0e"></a> [hpdma\_work\_mode\_t](#_CPPv417hpdma_work_mode_t "hpdma_work_mode_t") mode
    :   DMA work mode

    <a id="_CPPv4N14hpdma_config_t9chan_prioE"></a>

    <a id="_CPPv3N14hpdma_config_t9chan_prioE"></a> <a id="_CPPv2N14hpdma_config_t9chan_prioE"></a> <a id="hpdma_config_t::chan_prio__hpdma_chan_priority_t"></a> <a id="group__bk__api__dma__enum_1ga15bf93ec7439bd5775c21d1e55030a5d"></a> [hpdma\_chan\_priority\_t](#_CPPv421hpdma_chan_priority_t "hpdma_chan_priority_t") chan\_prio
    :   DMA channel prioprity

    <a id="_CPPv4N14hpdma_config_t3srcE"></a>

    <a id="_CPPv3N14hpdma_config_t3srcE"></a> <a id="_CPPv2N14hpdma_config_t3srcE"></a> <a id="hpdma_config_t::src__hpdma_port_config_t"></a> <a id="group__bk__api__dma__enum_1gae7cf05614043b84870224d77e823aa34"></a> [hpdma\_port\_config\_t](#_CPPv419hpdma_port_config_t "hpdma_port_config_t") src
    :   DMA source configuration

    <a id="_CPPv4N14hpdma_config_t3dstE"></a>

    <a id="_CPPv3N14hpdma_config_t3dstE"></a> <a id="_CPPv2N14hpdma_config_t3dstE"></a> <a id="hpdma_config_t::dst__hpdma_port_config_t"></a> <a id="group__bk__api__dma__enum_1ga96f7aa4cdcf94b66cdb60e6f0a67bc1e"></a> [hpdma\_port\_config\_t](#_CPPv419hpdma_port_config_t "hpdma_port_config_t") dst
    :   DMA dest configuration

    <a id="_CPPv4N14hpdma_config_t10trans_typeE"></a>

    <a id="_CPPv3N14hpdma_config_t10trans_typeE"></a> <a id="_CPPv2N14hpdma_config_t10trans_typeE"></a> <a id="hpdma_config_t::trans_type__hpdma_pixel_trans_type_t"></a> <a id="group__bk__api__dma__enum_1gadf2c40ca572c72d60c1af4b65f469314"></a> [hpdma\_pixel\_trans\_type\_t](#_CPPv424hpdma_pixel_trans_type_t "hpdma_pixel_trans_type_t") trans\_type
    :   DMA TRANS TYPE

<a id="_CPPv418hpdma_descriptor_t"></a>

<a id="_CPPv318hpdma_descriptor_t"></a> <a id="_CPPv218hpdma_descriptor_t"></a> <a id="hpdma_descriptor_t"></a> <a id="structhpdma__descriptor__t"></a> struct hpdma\_descriptor\_t

<a id="_CPPv419hpdma_link_config_t"></a>

<a id="_CPPv319hpdma_link_config_t"></a> <a id="_CPPv219hpdma_link_config_t"></a> <a id="hpdma_link_config_t"></a> <a id="structhpdma__link__config__t"></a> struct hpdma\_link\_config\_t

<a id="id4"></a>

### Macros

<a id="c.BK_ERR_HPDMA_HAL_INVALID_ALIGN"></a>

<a id="hal__hpdma__types_8h_1a1bd2f4e2f48076dbbb66c952a6921013"></a> BK\_ERR\_HPDMA\_HAL\_INVALID\_ALIGN
:   HPDMA loop window is not 128-bit aligned

<a id="c.BK_ERR_HPDMA_HAL_INVALID_YSIZE"></a>

<a id="hal__hpdma__types_8h_1a800bd2e79701b02d1fc9dc4588fc5aa8"></a> BK\_ERR\_HPDMA\_HAL\_INVALID\_YSIZE
:   HPDMA ysize must be 0 when addr loop is enabled

<a id="id5"></a>

### Type Definitions

<a id="_CPPv412hpdma_unit_t"></a>

<a id="_CPPv312hpdma_unit_t"></a> <a id="_CPPv212hpdma_unit_t"></a> <a id="hpdma_unit_t"></a> <a id="group__bk__api__dma__defs_1gacb91d71ef775d43e3fbf0f87821bdfa2"></a> typedef uint8\_t hpdma\_unit\_t
:   DMA uint id

<a id="_CPPv421hpdma_chan_priority_t"></a>

<a id="_CPPv321hpdma_chan_priority_t"></a> <a id="_CPPv221hpdma_chan_priority_t"></a> <a id="hpdma_chan_priority_t"></a> <a id="group__bk__api__dma__defs_1ga22646a62886c326885c3a3d5a6de754b"></a> typedef uint8\_t hpdma\_chan\_priority\_t
:   DMA channel priority:the value is higher then the priority is higher

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv414hpdma_int_id_t"></a>

<a id="_CPPv314hpdma_int_id_t"></a> <a id="_CPPv214hpdma_int_id_t"></a> <a id="group__bk__api__dma__enum_1gaa21bff5404d51a3cac091b2c02bc12cf"></a> enum hpdma\_int\_id\_t
:   CPU core for DMA Interrupt Differentiation Notification.

    @Enumeration option selection core notifies DMA to interrupt after completion of transport

    @Notification of terminal selection based on channel operation

    *Values:*

    <a id="_CPPv4N14hpdma_int_id_t11HPDMA_INT_0E"></a>

    <a id="_CPPv3N14hpdma_int_id_t11HPDMA_INT_0E"></a> <a id="_CPPv2N14hpdma_int_id_t11HPDMA_INT_0E"></a> <a id="group__bk__api__dma__enum_1ggaa21bff5404d51a3cac091b2c02bc12cfa1e2bce86b381ad781ce3568745b8b96e"></a> enumerator HPDMA\_INT\_0
    :   DMA INT 0 AP cpu core 0

    <a id="_CPPv4N14hpdma_int_id_t11HPDMA_INT_1E"></a>

    <a id="_CPPv3N14hpdma_int_id_t11HPDMA_INT_1E"></a> <a id="_CPPv2N14hpdma_int_id_t11HPDMA_INT_1E"></a> <a id="group__bk__api__dma__enum_1ggaa21bff5404d51a3cac091b2c02bc12cfab0923032c6f9b13697ce422af9116bc3"></a> enumerator HPDMA\_INT\_1
    :   DMA INT 1 AP cpu core 1

    <a id="_CPPv4N14hpdma_int_id_t11HPDMA_INT_2E"></a>

    <a id="_CPPv3N14hpdma_int_id_t11HPDMA_INT_2E"></a> <a id="_CPPv2N14hpdma_int_id_t11HPDMA_INT_2E"></a> <a id="group__bk__api__dma__enum_1ggaa21bff5404d51a3cac091b2c02bc12cfa81f2acc3a552479737ee22e4abee5ddf"></a> enumerator HPDMA\_INT\_2
    :   DMA INT 2 CP

    <a id="_CPPv4N14hpdma_int_id_t11HPDMA_INT_3E"></a>

    <a id="_CPPv3N14hpdma_int_id_t11HPDMA_INT_3E"></a> <a id="_CPPv2N14hpdma_int_id_t11HPDMA_INT_3E"></a> <a id="group__bk__api__dma__enum_1ggaa21bff5404d51a3cac091b2c02bc12cfad50d4ca4f096d2737884d419bf7d4cf6"></a> enumerator HPDMA\_INT\_3
    :   DMA INT 3 NA

    <a id="_CPPv4N14hpdma_int_id_t11HPDMA_INT_4E"></a>

    <a id="_CPPv3N14hpdma_int_id_t11HPDMA_INT_4E"></a> <a id="_CPPv2N14hpdma_int_id_t11HPDMA_INT_4E"></a> <a id="group__bk__api__dma__enum_1ggaa21bff5404d51a3cac091b2c02bc12cfae8e5b26e14f33ddc645973700e2418e5"></a> enumerator HPDMA\_INT\_4
    :   DMA INT 4 NA

    <a id="_CPPv4N14hpdma_int_id_t13HPDMA_INT_MAXE"></a>

    <a id="_CPPv3N14hpdma_int_id_t13HPDMA_INT_MAXE"></a> <a id="_CPPv2N14hpdma_int_id_t13HPDMA_INT_MAXE"></a> <a id="group__bk__api__dma__enum_1ggaa21bff5404d51a3cac091b2c02bc12cfa955fe4b9b30409358d805d28257a42b2"></a> enumerator HPDMA\_INT\_MAX
    :   DMA channel max

<a id="_CPPv411hpdma_dev_t"></a>

<a id="_CPPv311hpdma_dev_t"></a> <a id="_CPPv211hpdma_dev_t"></a> <a id="group__bk__api__dma__enum_1gaffcbc2366592ba38e78ac43f9312e5f7"></a> enum hpdma\_dev\_t
:   *Values:*

    <a id="_CPPv4N11hpdma_dev_t14HPDMA_DEV_DTCME"></a>

    <a id="_CPPv3N11hpdma_dev_t14HPDMA_DEV_DTCME"></a> <a id="_CPPv2N11hpdma_dev_t14HPDMA_DEV_DTCME"></a> <a id="group__bk__api__dma__enum_1ggaffcbc2366592ba38e78ac43f9312e5f7a11a8b83d431b0f9b8db09d551223cf22"></a> enumerator HPDMA\_DEV\_DTCM
    :   DMA device DTCM

    <a id="_CPPv4N11hpdma_dev_t15HPDMA_DEV_UART5E"></a>

    <a id="_CPPv3N11hpdma_dev_t15HPDMA_DEV_UART5E"></a> <a id="_CPPv2N11hpdma_dev_t15HPDMA_DEV_UART5E"></a> <a id="group__bk__api__dma__enum_1ggaffcbc2366592ba38e78ac43f9312e5f7a7a38dab4b8f9d2ef3a21aa71d9d80622"></a> enumerator HPDMA\_DEV\_UART5
    :   DMA device UART5

    <a id="_CPPv4N11hpdma_dev_t13HPDMA_DEV_MAXE"></a>

    <a id="_CPPv3N11hpdma_dev_t13HPDMA_DEV_MAXE"></a> <a id="_CPPv2N11hpdma_dev_t13HPDMA_DEV_MAXE"></a> <a id="group__bk__api__dma__enum_1ggaffcbc2366592ba38e78ac43f9312e5f7a5c56130e856951d125b869caff072008"></a> enumerator HPDMA\_DEV\_MAX

<a id="_CPPv418hpdma_data_width_t"></a>

<a id="_CPPv318hpdma_data_width_t"></a> <a id="_CPPv218hpdma_data_width_t"></a> <a id="group__bk__api__dma__enum_1ga5437420e55e576645862019b58a7a0a0"></a> enum hpdma\_data\_width\_t
:   *Values:*

    <a id="_CPPv4N18hpdma_data_width_t22HPDMA_DATA_WIDTH_8BITSE"></a>

    <a id="_CPPv3N18hpdma_data_width_t22HPDMA_DATA_WIDTH_8BITSE"></a> <a id="_CPPv2N18hpdma_data_width_t22HPDMA_DATA_WIDTH_8BITSE"></a> <a id="group__bk__api__dma__enum_1gga5437420e55e576645862019b58a7a0a0a730229f83177444ae27ad142f5843353"></a> enumerator HPDMA\_DATA\_WIDTH\_8BITS
    :   DMA data width 8bit

    <a id="_CPPv4N18hpdma_data_width_t23HPDMA_DATA_WIDTH_16BITSE"></a>

    <a id="_CPPv3N18hpdma_data_width_t23HPDMA_DATA_WIDTH_16BITSE"></a> <a id="_CPPv2N18hpdma_data_width_t23HPDMA_DATA_WIDTH_16BITSE"></a> <a id="group__bk__api__dma__enum_1gga5437420e55e576645862019b58a7a0a0a5c4722de6bde6f1acab3faad9d1673da"></a> enumerator HPDMA\_DATA\_WIDTH\_16BITS
    :   DMA data width 16bit

    <a id="_CPPv4N18hpdma_data_width_t23HPDMA_DATA_WIDTH_32BITSE"></a>

    <a id="_CPPv3N18hpdma_data_width_t23HPDMA_DATA_WIDTH_32BITSE"></a> <a id="_CPPv2N18hpdma_data_width_t23HPDMA_DATA_WIDTH_32BITSE"></a> <a id="group__bk__api__dma__enum_1gga5437420e55e576645862019b58a7a0a0a5578474b363aba3dabbd3fce38818f93"></a> enumerator HPDMA\_DATA\_WIDTH\_32BITS
    :   DMA data width 32bit

    <a id="_CPPv4N18hpdma_data_width_t23HPDMA_DATA_WIDTH_64BITSE"></a>

    <a id="_CPPv3N18hpdma_data_width_t23HPDMA_DATA_WIDTH_64BITSE"></a> <a id="_CPPv2N18hpdma_data_width_t23HPDMA_DATA_WIDTH_64BITSE"></a> <a id="group__bk__api__dma__enum_1gga5437420e55e576645862019b58a7a0a0afdaf5771c6b143e15b9ba00b80362d3d"></a> enumerator HPDMA\_DATA\_WIDTH\_64BITS
    :   DMA data width 32bit

    <a id="_CPPv4N18hpdma_data_width_t24HPDMA_DATA_WIDTH_128BITSE"></a>

    <a id="_CPPv3N18hpdma_data_width_t24HPDMA_DATA_WIDTH_128BITSE"></a> <a id="_CPPv2N18hpdma_data_width_t24HPDMA_DATA_WIDTH_128BITSE"></a> <a id="group__bk__api__dma__enum_1gga5437420e55e576645862019b58a7a0a0aff00f857c96b971ecc88b8e59c21a28d"></a> enumerator HPDMA\_DATA\_WIDTH\_128BITS
    :   DMA data width 32bit

<a id="_CPPv417hpdma_work_mode_t"></a>

<a id="_CPPv317hpdma_work_mode_t"></a> <a id="_CPPv217hpdma_work_mode_t"></a> <a id="group__bk__api__dma__enum_1ga6d3592925beedfb15dd3b42c60e385ef"></a> enum hpdma\_work\_mode\_t
:   *Values:*

    <a id="_CPPv4N17hpdma_work_mode_t22HPDMA_WORK_MODE_SINGLEE"></a>

    <a id="_CPPv3N17hpdma_work_mode_t22HPDMA_WORK_MODE_SINGLEE"></a> <a id="_CPPv2N17hpdma_work_mode_t22HPDMA_WORK_MODE_SINGLEE"></a> <a id="group__bk__api__dma__enum_1gga6d3592925beedfb15dd3b42c60e385efafe4b36209ccea5e58565922ffe031949"></a> enumerator HPDMA\_WORK\_MODE\_SINGLE
    :   DMA work mode single\_mode

    <a id="_CPPv4N17hpdma_work_mode_t22HPDMA_WORK_MODE_REPEATE"></a>

    <a id="_CPPv3N17hpdma_work_mode_t22HPDMA_WORK_MODE_REPEATE"></a> <a id="_CPPv2N17hpdma_work_mode_t22HPDMA_WORK_MODE_REPEATE"></a> <a id="group__bk__api__dma__enum_1gga6d3592925beedfb15dd3b42c60e385efaf834c2b8d3d2deec7f75e71c211a73b4"></a> enumerator HPDMA\_WORK\_MODE\_REPEAT
    :   DMA work mode repeat\_mode (forever repeat until software clear dma\_en)

<a id="_CPPv421hpdma_priority_mode_t"></a>

<a id="_CPPv321hpdma_priority_mode_t"></a> <a id="_CPPv221hpdma_priority_mode_t"></a> <a id="group__bk__api__dma__enum_1ga6c20e2d6207f6ffc8a66055bc4ffe405"></a> enum hpdma\_priority\_mode\_t
:   *Values:*

    <a id="_CPPv4N21hpdma_priority_mode_t27HPDMA_PRIO_MODE_ROUND_ROBINE"></a>

    <a id="_CPPv3N21hpdma_priority_mode_t27HPDMA_PRIO_MODE_ROUND_ROBINE"></a> <a id="_CPPv2N21hpdma_priority_mode_t27HPDMA_PRIO_MODE_ROUND_ROBINE"></a> <a id="group__bk__api__dma__enum_1gga6c20e2d6207f6ffc8a66055bc4ffe405af9a25b279cdde7619793dc47e7709555"></a> enumerator HPDMA\_PRIO\_MODE\_ROUND\_ROBIN
    :   DMA priority mode round-robin(all dma priority are the same)

    <a id="_CPPv4N21hpdma_priority_mode_t26HPDMA_PRIO_MODE_FIXED_PRIOE"></a>

    <a id="_CPPv3N21hpdma_priority_mode_t26HPDMA_PRIO_MODE_FIXED_PRIOE"></a> <a id="_CPPv2N21hpdma_priority_mode_t26HPDMA_PRIO_MODE_FIXED_PRIOE"></a> <a id="group__bk__api__dma__enum_1gga6c20e2d6207f6ffc8a66055bc4ffe405a6150043d02b7d691788aacbc6f7817d2"></a> enumerator HPDMA\_PRIO\_MODE\_FIXED\_PRIO
    :   DMA priority mode fixed prio(depend on chan\_prio)

<a id="_CPPv416hpdma_addr_inc_t"></a>

<a id="_CPPv316hpdma_addr_inc_t"></a> <a id="_CPPv216hpdma_addr_inc_t"></a> <a id="group__bk__api__dma__enum_1gaab1272b4e2ea174ab32a261c4d504377"></a> enum hpdma\_addr\_inc\_t
:   *Values:*

    <a id="_CPPv4N16hpdma_addr_inc_t22HPDMA_ADDR_INC_DISABLEE"></a>

    <a id="_CPPv3N16hpdma_addr_inc_t22HPDMA_ADDR_INC_DISABLEE"></a> <a id="_CPPv2N16hpdma_addr_inc_t22HPDMA_ADDR_INC_DISABLEE"></a> <a id="group__bk__api__dma__enum_1ggaab1272b4e2ea174ab32a261c4d504377a3d0c54785337f815f21f0bccc077d051"></a> enumerator HPDMA\_ADDR\_INC\_DISABLE
    :   DMA disable addrress increase

    <a id="_CPPv4N16hpdma_addr_inc_t21HPDMA_ADDR_INC_ENABLEE"></a>

    <a id="_CPPv3N16hpdma_addr_inc_t21HPDMA_ADDR_INC_ENABLEE"></a> <a id="_CPPv2N16hpdma_addr_inc_t21HPDMA_ADDR_INC_ENABLEE"></a> <a id="group__bk__api__dma__enum_1ggaab1272b4e2ea174ab32a261c4d504377a43d4023d90e81bdab43eecfc3b65d825"></a> enumerator HPDMA\_ADDR\_INC\_ENABLE
    :   DMA enable addrress increase

<a id="_CPPv417hpdma_addr_loop_t"></a>

<a id="_CPPv317hpdma_addr_loop_t"></a> <a id="_CPPv217hpdma_addr_loop_t"></a> <a id="group__bk__api__dma__enum_1gac89c1cbc264214ac691f60ee85631e71"></a> enum hpdma\_addr\_loop\_t
:   *Values:*

    <a id="_CPPv4N17hpdma_addr_loop_t23HPDMA_ADDR_LOOP_DISABLEE"></a>

    <a id="_CPPv3N17hpdma_addr_loop_t23HPDMA_ADDR_LOOP_DISABLEE"></a> <a id="_CPPv2N17hpdma_addr_loop_t23HPDMA_ADDR_LOOP_DISABLEE"></a> <a id="group__bk__api__dma__enum_1ggac89c1cbc264214ac691f60ee85631e71af015dacf9536c862c9302e57493be67e"></a> enumerator HPDMA\_ADDR\_LOOP\_DISABLE
    :   DMA disable addrress loop

    <a id="_CPPv4N17hpdma_addr_loop_t22HPDMA_ADDR_LOOP_ENABLEE"></a>

    <a id="_CPPv3N17hpdma_addr_loop_t22HPDMA_ADDR_LOOP_ENABLEE"></a> <a id="_CPPv2N17hpdma_addr_loop_t22HPDMA_ADDR_LOOP_ENABLEE"></a> <a id="group__bk__api__dma__enum_1ggac89c1cbc264214ac691f60ee85631e71a19739c83fb91566e1d8e3f13519a1d00"></a> enumerator HPDMA\_ADDR\_LOOP\_ENABLE
    :   DMA enable addrress loop

<a id="_CPPv416hpdma_sec_attr_t"></a>

<a id="_CPPv316hpdma_sec_attr_t"></a> <a id="_CPPv216hpdma_sec_attr_t"></a> <a id="group__bk__api__dma__enum_1ga37cfb6fd102df857038d5cfc02a6a33e"></a> enum hpdma\_sec\_attr\_t
:   *Values:*

    <a id="_CPPv4N16hpdma_sec_attr_t18HPDMA_ATTR_NON_SECE"></a>

    <a id="_CPPv3N16hpdma_sec_attr_t18HPDMA_ATTR_NON_SECE"></a> <a id="_CPPv2N16hpdma_sec_attr_t18HPDMA_ATTR_NON_SECE"></a> <a id="group__bk__api__dma__enum_1gga37cfb6fd102df857038d5cfc02a6a33ea24f16473ca1d1591ab5ab43595654433"></a> enumerator HPDMA\_ATTR\_NON\_SEC
    :   DMA non-secure attr

    <a id="_CPPv4N16hpdma_sec_attr_t14HPDMA_ATTR_SECE"></a>

    <a id="_CPPv3N16hpdma_sec_attr_t14HPDMA_ATTR_SECE"></a> <a id="_CPPv2N16hpdma_sec_attr_t14HPDMA_ATTR_SECE"></a> <a id="group__bk__api__dma__enum_1gga37cfb6fd102df857038d5cfc02a6a33ea8ee49cd7aa331789495096550e103546"></a> enumerator HPDMA\_ATTR\_SEC
    :   DMA secure attr

<a id="_CPPv417hpdma_burst_len_t"></a>

<a id="_CPPv317hpdma_burst_len_t"></a> <a id="_CPPv217hpdma_burst_len_t"></a> <a id="group__bk__api__dma__enum_1ga2a78478af182c838666ed1a98b10cbb3"></a> enum hpdma\_burst\_len\_t
:   *Values:*

    <a id="_CPPv4N17hpdma_burst_len_t22HPDMA_BURST_LEN_SINGLEE"></a>

    <a id="_CPPv3N17hpdma_burst_len_t22HPDMA_BURST_LEN_SINGLEE"></a> <a id="_CPPv2N17hpdma_burst_len_t22HPDMA_BURST_LEN_SINGLEE"></a> <a id="group__bk__api__dma__enum_1gga2a78478af182c838666ed1a98b10cbb3a1ed5590e2fa572ecf86037483e61231b"></a> enumerator HPDMA\_BURST\_LEN\_SINGLE

    <a id="_CPPv4N17hpdma_burst_len_t20HPDMA_BURST_LEN_INC4E"></a>

    <a id="_CPPv3N17hpdma_burst_len_t20HPDMA_BURST_LEN_INC4E"></a> <a id="_CPPv2N17hpdma_burst_len_t20HPDMA_BURST_LEN_INC4E"></a> <a id="group__bk__api__dma__enum_1gga2a78478af182c838666ed1a98b10cbb3ad19672ca777f6dcfe34d547fe6ca9b1b"></a> enumerator HPDMA\_BURST\_LEN\_INC4

    <a id="_CPPv4N17hpdma_burst_len_t20HPDMA_BURST_LEN_INC8E"></a>

    <a id="_CPPv3N17hpdma_burst_len_t20HPDMA_BURST_LEN_INC8E"></a> <a id="_CPPv2N17hpdma_burst_len_t20HPDMA_BURST_LEN_INC8E"></a> <a id="group__bk__api__dma__enum_1gga2a78478af182c838666ed1a98b10cbb3a1d34f9d8cf16d20924c948d1980a01fd"></a> enumerator HPDMA\_BURST\_LEN\_INC8

    <a id="_CPPv4N17hpdma_burst_len_t21HPDMA_BURST_LEN_INC16E"></a>

    <a id="_CPPv3N17hpdma_burst_len_t21HPDMA_BURST_LEN_INC16E"></a> <a id="_CPPv2N17hpdma_burst_len_t21HPDMA_BURST_LEN_INC16E"></a> <a id="group__bk__api__dma__enum_1gga2a78478af182c838666ed1a98b10cbb3a653a7b8c65cbbac32435bf8c96e74016"></a> enumerator HPDMA\_BURST\_LEN\_INC16

<a id="_CPPv424hpdma_pixel_trans_type_t"></a>

<a id="_CPPv324hpdma_pixel_trans_type_t"></a> <a id="_CPPv224hpdma_pixel_trans_type_t"></a> <a id="group__bk__api__dma__enum_1ga895a6980e150eeb44217a4fca327dbc8"></a> enum hpdma\_pixel\_trans\_type\_t
:   *Values:*

    <a id="_CPPv4N24hpdma_pixel_trans_type_t19HPDMA_TRANS_DEFAULTE"></a>

    <a id="_CPPv3N24hpdma_pixel_trans_type_t19HPDMA_TRANS_DEFAULTE"></a> <a id="_CPPv2N24hpdma_pixel_trans_type_t19HPDMA_TRANS_DEFAULTE"></a> <a id="group__bk__api__dma__enum_1gga895a6980e150eeb44217a4fca327dbc8a6897f02737127e7f9bba1aad01defd36"></a> enumerator HPDMA\_TRANS\_DEFAULT
    :   DMA TRANS DEFAULT

    <a id="_CPPv4N24hpdma_pixel_trans_type_t22HPDMA_TRANS_YUV_TO_RGBE"></a>

    <a id="_CPPv3N24hpdma_pixel_trans_type_t22HPDMA_TRANS_YUV_TO_RGBE"></a> <a id="_CPPv2N24hpdma_pixel_trans_type_t22HPDMA_TRANS_YUV_TO_RGBE"></a> <a id="group__bk__api__dma__enum_1gga895a6980e150eeb44217a4fca327dbc8a1557e11c3a2e3c85872761be37b495ba"></a> enumerator HPDMA\_TRANS\_YUV\_TO\_RGB
    :   DMA TRANS YUV\_TO\_RGB

    <a id="_CPPv4N24hpdma_pixel_trans_type_t15HPDMA_TRANS_MAXE"></a>

    <a id="_CPPv3N24hpdma_pixel_trans_type_t15HPDMA_TRANS_MAXE"></a> <a id="_CPPv2N24hpdma_pixel_trans_type_t15HPDMA_TRANS_MAXE"></a> <a id="group__bk__api__dma__enum_1gga895a6980e150eeb44217a4fca327dbc8aea3ae80b68a9a851e805a094e6149ad6"></a> enumerator HPDMA\_TRANS\_MAX

<a id="_CPPv410hpdma_id_t"></a>

<a id="_CPPv310hpdma_id_t"></a> <a id="_CPPv210hpdma_id_t"></a> <a id="group__bk__api__dma__enum_1ga5a833477e1e542c1a0f275bddd03f08f"></a> enum hpdma\_id\_t
:   *Values:*

    <a id="_CPPv4N10hpdma_id_t10HPDMA_ID_0E"></a>

    <a id="_CPPv3N10hpdma_id_t10HPDMA_ID_0E"></a> <a id="_CPPv2N10hpdma_id_t10HPDMA_ID_0E"></a> <a id="group__bk__api__dma__enum_1gga5a833477e1e542c1a0f275bddd03f08fa85830a313643cd5f2b8e828383357f9c"></a> enumerator HPDMA\_ID\_0
    :   DMA channel 0

    <a id="_CPPv4N10hpdma_id_t10HPDMA_ID_1E"></a>

    <a id="_CPPv3N10hpdma_id_t10HPDMA_ID_1E"></a> <a id="_CPPv2N10hpdma_id_t10HPDMA_ID_1E"></a> <a id="group__bk__api__dma__enum_1gga5a833477e1e542c1a0f275bddd03f08fa9797f87b2bcbaa9bd2dadfbde7cb6e98"></a> enumerator HPDMA\_ID\_1
    :   DMA channel 1

    <a id="_CPPv4N10hpdma_id_t10HPDMA_ID_2E"></a>

    <a id="_CPPv3N10hpdma_id_t10HPDMA_ID_2E"></a> <a id="_CPPv2N10hpdma_id_t10HPDMA_ID_2E"></a> <a id="group__bk__api__dma__enum_1gga5a833477e1e542c1a0f275bddd03f08fa447ec88e92d7f66cbe9669479ba60ae6"></a> enumerator HPDMA\_ID\_2
    :   DMA channel 2

    <a id="_CPPv4N10hpdma_id_t10HPDMA_ID_3E"></a>

    <a id="_CPPv3N10hpdma_id_t10HPDMA_ID_3E"></a> <a id="_CPPv2N10hpdma_id_t10HPDMA_ID_3E"></a> <a id="group__bk__api__dma__enum_1gga5a833477e1e542c1a0f275bddd03f08fa9211b1c1fe2340d2b57fb345cb00ffca"></a> enumerator HPDMA\_ID\_3
    :   DMA channel 3

    <a id="_CPPv4N10hpdma_id_t12HPDMA_ID_MAXE"></a>

    <a id="_CPPv3N10hpdma_id_t12HPDMA_ID_MAXE"></a> <a id="_CPPv2N10hpdma_id_t12HPDMA_ID_MAXE"></a> <a id="group__bk__api__dma__enum_1gga5a833477e1e542c1a0f275bddd03f08fadb369ff92eaa10aa8d2281b77f24e511"></a> enumerator HPDMA\_ID\_MAX
    :   DMA channel max
