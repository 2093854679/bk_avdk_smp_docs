---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_interrupt.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="interrupt-control-unit"></a>

# Interrupt Control Unit

BK7259 CP 侧中断管理 API（`include/driver/int.h`）。详细说明见
[ICU 开发指南](../../developer-guide/peripheral/bk_interrupt.md)。

<a id="interrupt-api-reference"></a>

## Interrupt API Reference

<a id="header-file"></a>

### Header File

- [int.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/int.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_icu_driver_initv"></a>

<a id="_CPPv318bk_icu_driver_initv"></a> <a id="_CPPv218bk_icu_driver_initv"></a> <a id="bk_icu_driver_init__void"></a> <a id="group__bk__api__icu_1gaa3be47dd1dbe66234a91ddbdf145ed9a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_icu\_driver\_init(void)
:   Init the ICU driver.

    This API init the icu modules :

    - Init ICU driver control memory, enable fiq and irq

    This API should be called before any other ICU APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_icu_driver_deinitv"></a>

<a id="_CPPv320bk_icu_driver_deinitv"></a> <a id="_CPPv220bk_icu_driver_deinitv"></a> <a id="bk_icu_driver_deinit__void"></a> <a id="group__bk__api__icu_1gaeab9ff66b565fc0fe76c8d2f916c1a7b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_icu\_driver\_deinit(void)
:   deinit the ICU driver

    This API deinit the icu module

    This API disable all devices’ intterrupts

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_int_isr_register13icu_int_src_t15int_group_isr_tPv"></a>

<a id="_CPPv319bk_int_isr_register13icu_int_src_t15int_group_isr_tPv"></a> <a id="_CPPv219bk_int_isr_register13icu_int_src_t15int_group_isr_tPv"></a> <a id="bk_int_isr_register__icu_int_src_t.int_group_isr_t.voidP"></a> <a id="group__bk__api__icu_1gab1929863601295d456177900afef5299"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_int\_isr\_register(icu\_int\_src\_t dev, int\_group\_isr\_t isr, void \*arg)
:   register interrupt service handler

    **Attention**
    :   1\. If this is called, the default interrupt handler is replaced by the new handler, the caller is fully responsible for handling the interrupt, such as, read the interrupt status, clear the interrupt status and processing the interrupt etc.

    参数
    :   - **dev** – interrupt source device
        - **isr** – int service function

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NO\_MEM: no memoery
        - BK\_ERR\_INT\_DEVICE\_NONE: no int device
        - others: other errors.

<a id="_CPPv421bk_int_isr_unregister13icu_int_src_t"></a>

<a id="_CPPv321bk_int_isr_unregister13icu_int_src_t"></a> <a id="_CPPv221bk_int_isr_unregister13icu_int_src_t"></a> <a id="bk_int_isr_unregister__icu_int_src_t"></a> <a id="group__bk__api__icu_1ga0d78f93b9b48af2d17e5416e4462e824"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_int\_isr\_unregister(icu\_int\_src\_t src)
:   unregister interrupt service handler

    参数
    :   **dev** – interrupt source device

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_INT\_DEVICE\_NONE:no int device
        - others: other errors.

<a id="_CPPv419bk_int_set_priority13icu_int_src_t8uint32_t"></a>

<a id="_CPPv319bk_int_set_priority13icu_int_src_t8uint32_t"></a> <a id="_CPPv219bk_int_set_priority13icu_int_src_t8uint32_t"></a> <a id="bk_int_set_priority__icu_int_src_t.uint32_t"></a> <a id="group__bk__api__icu_1ga4a608665a47286894f417e7ac3617dd8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_int\_set\_priority(icu\_int\_src\_t src, uint32\_t int\_priority)
:   set/change interrupt priority

    Every interrupt source has a two-level priority, the group priority and the priority. The interrupt source has higher group priority will be schedule first. The interrupt sources has higher priority will be schedule first if they has the same group priority.

    This API is used to configure the pririty.

    参数
    :   - **dev** – interrupt source device
        - **isr** – int service function

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NOT\_SUPPORT :not support
        - others: other errors.

<a id="_CPPv420bk_int_clear_pending13icu_int_src_t"></a>

<a id="_CPPv320bk_int_clear_pending13icu_int_src_t"></a> <a id="_CPPv220bk_int_clear_pending13icu_int_src_t"></a> <a id="bk_int_clear_pending__icu_int_src_t"></a> <a id="group__bk__api__icu_1ga3d4182aae7cd0046ec328a9065d82017"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_int\_clear\_pending(icu\_int\_src\_t src)
:   Clear pending state of an interrupt source in NVIC.

    参数
    :   **src** – interrupt source device

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_INT\_DEVICE\_NONE: interrupt source is invalid
        - others: other errors.

<a id="_CPPv416bk_int_set_groupv"></a>

<a id="_CPPv316bk_int_set_groupv"></a> <a id="_CPPv216bk_int_set_groupv"></a> <a id="bk_int_set_group__void"></a> <a id="group__bk__api__icu_1gaf86a1407937c4edd536a3a96bd1a2815"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_int\_set\_group(void)
:   set the interrupt group priority

    Every interrupt source has a two-level priority, the group priority and the priority. The interrupt source has higher group priority will be schedule first. The interrupt sources has higher priority will be schedule first if they has the same group priority.

    This API is used to configure the group priority of the interrupt source.

    **Attention**
    :   1\. For ARM9, it has two group priorities which are mapped to ARM9 FIQ and IRQ. Currently all interrupt source are statically mapped to the group priority and can’t change by this API. We may support it in future.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NOT\_SUPPORT :not support
        - others: other errors.

<a id="_CPPv431bk_int_register_mac_ps_callback21int_mac_ps_callback_t"></a>

<a id="_CPPv331bk_int_register_mac_ps_callback21int_mac_ps_callback_t"></a> <a id="_CPPv231bk_int_register_mac_ps_callback21int_mac_ps_callback_t"></a> <a id="bk_int_register_mac_ps_callback__int_mac_ps_callback_t"></a> <a id="group__bk__api__icu_1ga69744f540cc958b374614aa39b805d50"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_int\_register\_mac\_ps\_callback([int\_mac\_ps\_callback\_t](#_CPPv421int_mac_ps_callback_t "int_mac_ps_callback_t") mac\_ps\_cb)
:   Register callback for mac ps.

    参数
    :   **mac\_ps\_cb** – mac ps callback

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="interrupt-api-typedefs"></a>

## Interrupt API Typedefs

<a id="id1"></a>

### Header File

- [int\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/int_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_INT_DEVICE_NONE"></a>

<a id="int__types_8h_1a2f4e71dd2a76888988c1bb58fea97535"></a> BK\_ERR\_INT\_DEVICE\_NONE
:   icu device number is invalid

<a id="c.BK_ERR_INT_NOT_EXIST"></a>

<a id="int__types_8h_1aad2ee438dda7b43b647c6c1169300d15"></a> BK\_ERR\_INT\_NOT\_EXIST
:   icu device number is invalid

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv421int_mac_ps_callback_t"></a>

<a id="_CPPv321int_mac_ps_callback_t"></a> <a id="_CPPv221int_mac_ps_callback_t"></a> <a id="int_mac_ps_callback_t"></a> <a id="int__types_8h_1a7dc91072bff9ec5d4610e065443715bc"></a> typedef void (\*int\_mac\_ps\_callback\_t)(uint32\_t status)
