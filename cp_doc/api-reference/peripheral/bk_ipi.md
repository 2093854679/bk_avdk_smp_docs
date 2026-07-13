# IPI


BK7259 CP 侧 IPI（处理器间中断）API（`include/driver/ipi_driver.h`）。详细说明见
[IPI 开发指南](../../developer-guide/peripheral/bk_ipi.md "../../developer-guide/peripheral/bk_ipi.md")。


## IPI API Reference


### Header File


- [ipi_driver.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/ipi_driver.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/ipi_driver.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ipi_driver_init(void)
:   Initialize IPI driver and register ISR.

    返回
    :   BK_OK on success, BK_FAIL on failure

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ipi_driver_deinit(void)
:   Deinitialize IPI driver.

    返回
    :   BK_OK on success, BK_FAIL on failure

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ipi_send_domain([ipi_core_id_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core_id, [ipi_domain_t](#_CPPv412ipi_domain_t "ipi_domain_t") domain, uint8_t event, uint16_t payload)
:   Send an encoded domain IPI interrupt to target core/channel.

    The current CPU ID is encoded as the source field.

    参数
    :   - **core_id** – Target IPI core/channel ID

        - **domain** – Domain identifier, see ipi_domain_t

        - **event** – Domain-specific event ID

        - **payload** – Domain-specific compact payload

    返回
    :   BK_OK on success, BK_FAIL on failure

uint32_t bk_ipi_get_status([ipi_core_id_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core_id)
:   Get pending status for one IPI core/channel.

    参数
    :   **core_id** – IPI core/channel ID to query

    返回
    :   1 if pending, 0 if clear/invalid/not initialized

uint32_t bk_ipi_get_all_status(void)
:   Get pending status bitmap for all IPI cores/channels.

    返回
    :   Bitmask where bit0..bit4 correspond to IPI_CP_CORE0..IPI_DSP_CORE

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ipi_clear([ipi_core_id_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core_id)
:   Clear pending IPI interrupt for the specified core/channel.

    参数
    :   **core_id** – IPI core/channel ID to clear

    返回
    :   BK_OK on success, BK_FAIL on failure

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ipi_enable([ipi_core_id_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core_id)
:   Enable IPI interrupt for the specified core/channel.

    参数
    :   **core_id** – IPI core/channel ID to enable

    返回
    :   BK_OK on success, BK_FAIL on failure

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ipi_disable([ipi_core_id_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core_id)
:   Disable IPI interrupt for the specified core/channel.

    参数
    :   **core_id** – IPI core/channel ID to disable

    返回
    :   BK_OK on success, BK_FAIL on failure

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ipi_register_domain_callback([ipi_domain_t](#_CPPv412ipi_domain_t "ipi_domain_t") domain, [ipi_domain_callback_t](#_CPPv421ipi_domain_callback_t "ipi_domain_callback_t") callback, void *param)
:   Register a shared domain callback.

    Only one owner can register each domain. Use domain callbacks for shared IPI use cases such as heartbeat and SMP kicks, so multiple users do not overwrite each other.

    参数
    :   - **domain** – Domain identifier, see ipi_domain_t

        - **callback** – Callback function

        - **param** – User argument passed back to callback

    返回
    :   BK_OK on success, BK_FAIL on failure

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ipi_unregister_domain_callback([ipi_domain_t](#_CPPv412ipi_domain_t "ipi_domain_t") domain)
:   Unregister a shared domain callback.

    参数
    :   **domain** – Domain identifier, see ipi_domain_t

    返回
    :   BK_OK on success, BK_FAIL on failure

uint32_t bk_ipi_get_device_status(void)
:   Get IPI device status register value.

    返回
    :   Device status register value, or 0 if not initialized


### Macros

IPI_VALUE_PAYLOAD_MASK

IPI_VALUE_EVENT_MASK

IPI_VALUE_DOMAIN_MASK

IPI_VALUE_SRC_MASK

IPI_VALUE_EVENT_POS

IPI_VALUE_DOMAIN_POS

IPI_VALUE_SRC_POS

IPI_VALUE_MAKE(src, domain, event, payload)

IPI_VALUE_GET_SRC(value)

IPI_VALUE_GET_DOMAIN(value)

IPI_VALUE_GET_EVENT(value)

IPI_VALUE_GET_PAYLOAD(value)


### Type Definitions

typedef void (*ipi_domain_callback_t)([ipi_core_id_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core_id, uint32_t value, uint8_t src_cpu, uint8_t event, uint16_t payload, void *param)
:   Domain-level IPI callback.

    IPI is a doorbell, not a FIFO. Domain users should keep durable state in shared memory/bitmaps and use the IPI value only as a compact notification.


### Enumerations

enum ipi_core_id_t
:   *Values:*

    enumerator IPI_CP_CORE0

    enumerator IPI_CP_CORE1

    enumerator IPI_AP_CORE0

    enumerator IPI_AP_CORE1

    enumerator IPI_DSP_CORE

    enumerator IPI_CORE_MAX

enum ipi_domain_t
:   Software domains multiplexed over one target-core IPI channel.

    The IPI hardware provides one pending/value register per target core, not a FIFO or a set of independent logical channels. Domain encoding lets the common IPI ISR dispatch one hardware interrupt source to multiple software users without those users overwriting each other’s per-core callback.

    Encoded domain IPI values use this layout: bits 30..27: source CPU ID bits 26..24: software domain bits 23..16: domain-specific event ID bits 15..0 : domain-specific compact payload

    Domain 0 is reserved as an invalid domain, so every public IPI user must use an explicitly assigned domain. HEARTBEAT is for AP/CP liveness notifications, SMP is for cross-core scheduler/OS kicks, USB is reserved for USB/RISC-V bridge notifications, and TEST is kept for CLI/debug traffic.


    *Values:*

    enumerator IPI_DOMAIN_RESERVED

    enumerator IPI_DOMAIN_HEARTBEAT

    enumerator IPI_DOMAIN_SMP

    enumerator IPI_DOMAIN_USB

    enumerator IPI_DOMAIN_CP_HANG_DEBUG

    enumerator IPI_DOMAIN_TEST

    enumerator IPI_DOMAIN_MAX
