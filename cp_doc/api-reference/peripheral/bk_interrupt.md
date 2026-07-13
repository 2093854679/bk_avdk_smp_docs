# Interrupt Control Unit


BK7259 CP 侧中断管理 API（`include/driver/int.h`）。详细说明见
[ICU 开发指南](../../developer-guide/peripheral/bk_interrupt.md "../../developer-guide/peripheral/bk_interrupt.md")。


## Interrupt API Reference


### Header File


- [int.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/int.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/int.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_icu_driver_init(void)
:   Init the ICU driver.

    This API init the icu modules :


    - Init ICU driver control memory, enable fiq and irq

    This API should be called before any other ICU APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_icu_driver_deinit(void)
:   deinit the ICU driver

    This API deinit the icu module

    This API disable all devices’ intterrupts

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_int_isr_register(icu_int_src_t dev, int_group_isr_t isr, void *arg)
:   register interrupt service handler


    **Attention**
    :   1. If this is called, the default interrupt handler is replaced by the new handler, the caller is fully responsible for handling the interrupt, such as, read the interrupt status, clear the interrupt status and processing the interrupt etc.

    参数
    :   - **dev** – interrupt source device

        - **isr** – int service function

    返回
    :   - BK_OK: succeed

        - BK_ERR_NO_MEM: no memoery

        - BK_ERR_INT_DEVICE_NONE: no int device

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_int_isr_unregister(icu_int_src_t src)
:   unregister interrupt service handler

    参数
    :   **dev** – interrupt source device

    返回
    :   - BK_OK: succeed

        - BK_ERR_INT_DEVICE_NONE:no int device

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_int_set_priority(icu_int_src_t src, uint32_t int_priority)
:   set/change interrupt priority

    Every interrupt source has a two-level priority, the group priority and the priority. The interrupt source has higher group priority will be schedule first. The interrupt sources has higher priority will be schedule first if they has the same group priority.

    This API is used to configure the pririty.

    参数
    :   - **dev** – interrupt source device

        - **isr** – int service function

    返回
    :   - BK_OK: succeed

        - BK_ERR_NOT_SUPPORT :not support

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_int_clear_pending(icu_int_src_t src)
:   Clear pending state of an interrupt source in NVIC.

    参数
    :   **src** – interrupt source device

    返回
    :   - BK_OK: succeed

        - BK_ERR_INT_DEVICE_NONE: interrupt source is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_int_set_group(void)
:   set the interrupt group priority

    Every interrupt source has a two-level priority, the group priority and the priority. The interrupt source has higher group priority will be schedule first. The interrupt sources has higher priority will be schedule first if they has the same group priority.

    This API is used to configure the group priority of the interrupt source.


    **Attention**
    :   1. For ARM9, it has two group priorities which are mapped to ARM9 FIQ and IRQ. Currently all interrupt source are statically mapped to the group priority and can’t change by this API. We may support it in future.

    返回
    :   - BK_OK: succeed

        - BK_ERR_NOT_SUPPORT :not support

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_int_register_mac_ps_callback([int_mac_ps_callback_t](#_CPPv421int_mac_ps_callback_t "int_mac_ps_callback_t") mac_ps_cb)
:   Register callback for mac ps.

    参数
    :   **mac_ps_cb** – mac ps callback

    返回
    :   - BK_OK: succeed

        - others: other errors.


## Interrupt API Typedefs


### Header File


- [int_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/int_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/int_types.h")


### Macros

BK_ERR_INT_DEVICE_NONE
:   icu device number is invalid

BK_ERR_INT_NOT_EXIST
:   icu device number is invalid


### Type Definitions

typedef void (*int_mac_ps_callback_t)(uint32_t status)
