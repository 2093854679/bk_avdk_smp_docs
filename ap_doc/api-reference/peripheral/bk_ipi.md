---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_ipi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ipi"></a>

# IPI

BK7259 AP 侧 IPI（处理器间中断）API（`include/driver/ipi_driver.h`）。详细说明见
[IPI 开发指南](../../developer-guide/peripheral/bk_ipi.md)。

<a id="ipi-api-reference"></a>

## IPI API Reference

<a id="header-file"></a>

### Header File

- [ipi\_driver.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/ipi_driver.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_ipi_driver_initv"></a>

<a id="_CPPv318bk_ipi_driver_initv"></a> <a id="_CPPv218bk_ipi_driver_initv"></a> <a id="bk_ipi_driver_init__void"></a> <a id="ipi__driver_8h_1abfa70cab9836792eb4f83cf6236dcab5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ipi\_driver\_init(void)
:   Initialize IPI driver and register ISR.

<a id="_CPPv420bk_ipi_driver_deinitv"></a>

<a id="_CPPv320bk_ipi_driver_deinitv"></a> <a id="_CPPv220bk_ipi_driver_deinitv"></a> <a id="bk_ipi_driver_deinit__void"></a> <a id="ipi__driver_8h_1a8e22a4dc19c7d42506af9fd5b7f36c11"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ipi\_driver\_deinit(void)
:   Deinitialize IPI driver.

<a id="_CPPv418bk_ipi_send_domain13ipi_core_id_t12ipi_domain_t7uint8_t8uint16_t"></a>

<a id="_CPPv318bk_ipi_send_domain13ipi_core_id_t12ipi_domain_t7uint8_t8uint16_t"></a> <a id="_CPPv218bk_ipi_send_domain13ipi_core_id_t12ipi_domain_t7uint8_t8uint16_t"></a> <a id="bk_ipi_send_domain__ipi_core_id_t.ipi_domain_t.uint8_t.uint16_t"></a> <a id="ipi__driver_8h_1a56aafca43306305297a9edc7bcd62ce1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ipi\_send\_domain([ipi\_core\_id\_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core\_id, [ipi\_domain\_t](#_CPPv412ipi_domain_t "ipi_domain_t") domain, uint8\_t event, uint16\_t payload)
:   Send an encoded domain IPI interrupt to target core/channel.

<a id="_CPPv417bk_ipi_get_status13ipi_core_id_t"></a>

<a id="_CPPv317bk_ipi_get_status13ipi_core_id_t"></a> <a id="_CPPv217bk_ipi_get_status13ipi_core_id_t"></a> <a id="bk_ipi_get_status__ipi_core_id_t"></a> <a id="ipi__driver_8h_1a5b294e61d9b575c133b780b99e63681f"></a> uint32\_t bk\_ipi\_get\_status([ipi\_core\_id\_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core\_id)
:   Get pending status for one IPI core/channel.

<a id="_CPPv421bk_ipi_get_all_statusv"></a>

<a id="_CPPv321bk_ipi_get_all_statusv"></a> <a id="_CPPv221bk_ipi_get_all_statusv"></a> <a id="bk_ipi_get_all_status__void"></a> <a id="ipi__driver_8h_1a1458ef82e4ba4c65b4b79c7f8236a836"></a> uint32\_t bk\_ipi\_get\_all\_status(void)
:   Get pending status bitmap for all IPI cores/channels.

<a id="_CPPv412bk_ipi_clear13ipi_core_id_t"></a>

<a id="_CPPv312bk_ipi_clear13ipi_core_id_t"></a> <a id="_CPPv212bk_ipi_clear13ipi_core_id_t"></a> <a id="bk_ipi_clear__ipi_core_id_t"></a> <a id="ipi__driver_8h_1a461a0620c0c1632165a49f6af4a03c8b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ipi\_clear([ipi\_core\_id\_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core\_id)
:   Clear pending IPI interrupt for the specified core/channel.

<a id="_CPPv413bk_ipi_enable13ipi_core_id_t"></a>

<a id="_CPPv313bk_ipi_enable13ipi_core_id_t"></a> <a id="_CPPv213bk_ipi_enable13ipi_core_id_t"></a> <a id="bk_ipi_enable__ipi_core_id_t"></a> <a id="ipi__driver_8h_1ab40f47ed72fedf807a00b4767a085fbb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ipi\_enable([ipi\_core\_id\_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core\_id)
:   Enable IPI interrupt for the specified core/channel.

<a id="_CPPv414bk_ipi_disable13ipi_core_id_t"></a>

<a id="_CPPv314bk_ipi_disable13ipi_core_id_t"></a> <a id="_CPPv214bk_ipi_disable13ipi_core_id_t"></a> <a id="bk_ipi_disable__ipi_core_id_t"></a> <a id="ipi__driver_8h_1a2ae0cad38e8c73c4f2cbbf48cb863014"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ipi\_disable([ipi\_core\_id\_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core\_id)
:   Disable IPI interrupt for the specified core/channel.

<a id="_CPPv431bk_ipi_register_domain_callback12ipi_domain_t21ipi_domain_callback_tPv"></a>

<a id="_CPPv331bk_ipi_register_domain_callback12ipi_domain_t21ipi_domain_callback_tPv"></a> <a id="_CPPv231bk_ipi_register_domain_callback12ipi_domain_t21ipi_domain_callback_tPv"></a> <a id="bk_ipi_register_domain_callback__ipi_domain_t.ipi_domain_callback_t.voidP"></a> <a id="ipi__driver_8h_1ad26e655425538bb9af13db4abc488007"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ipi\_register\_domain\_callback([ipi\_domain\_t](#_CPPv412ipi_domain_t "ipi_domain_t") domain, [ipi\_domain\_callback\_t](#_CPPv421ipi_domain_callback_t "ipi_domain_callback_t") callback, void \*param)
:   Register a shared domain callback.

<a id="_CPPv433bk_ipi_unregister_domain_callback12ipi_domain_t"></a>

<a id="_CPPv333bk_ipi_unregister_domain_callback12ipi_domain_t"></a> <a id="_CPPv233bk_ipi_unregister_domain_callback12ipi_domain_t"></a> <a id="bk_ipi_unregister_domain_callback__ipi_domain_t"></a> <a id="ipi__driver_8h_1ac648eddbcea9537c737f910f3eca170d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ipi\_unregister\_domain\_callback([ipi\_domain\_t](#_CPPv412ipi_domain_t "ipi_domain_t") domain)
:   Unregister a shared domain callback.

<a id="_CPPv424bk_ipi_get_device_statusv"></a>

<a id="_CPPv324bk_ipi_get_device_statusv"></a> <a id="_CPPv224bk_ipi_get_device_statusv"></a> <a id="bk_ipi_get_device_status__void"></a> <a id="ipi__driver_8h_1acac350a2a1403892a520e20d09f2dbda"></a> uint32\_t bk\_ipi\_get\_device\_status(void)
:   Get IPI device status register value.

<a id="macros"></a>

### Macros

<a id="c.IPI_VALUE_PAYLOAD_MASK"></a>

<a id="ipi__driver_8h_1a1ed8516ccd2683276f3a7bba24cce6dd"></a> IPI\_VALUE\_PAYLOAD\_MASK

<a id="c.IPI_VALUE_EVENT_MASK"></a>

<a id="ipi__driver_8h_1ad75c53cb849f8eaa5f1ff7f479720fe2"></a> IPI\_VALUE\_EVENT\_MASK

<a id="c.IPI_VALUE_DOMAIN_MASK"></a>

<a id="ipi__driver_8h_1a444f9248556cc83c3bb6c6824dc59b86"></a> IPI\_VALUE\_DOMAIN\_MASK

<a id="c.IPI_VALUE_SRC_MASK"></a>

<a id="ipi__driver_8h_1aa9798fe8e7765e8878a2c4330c7d8381"></a> IPI\_VALUE\_SRC\_MASK

<a id="c.IPI_VALUE_EVENT_POS"></a>

<a id="ipi__driver_8h_1ac9f4304c18d1e0b673724d9826db4858"></a> IPI\_VALUE\_EVENT\_POS

<a id="c.IPI_VALUE_DOMAIN_POS"></a>

<a id="ipi__driver_8h_1a131a08abf9f33d2708319b201a5df386"></a> IPI\_VALUE\_DOMAIN\_POS

<a id="c.IPI_VALUE_SRC_POS"></a>

<a id="ipi__driver_8h_1abbfee2d0a90c619791600772a301151a"></a> IPI\_VALUE\_SRC\_POS

<a id="c.IPI_VALUE_MAKE"></a>

<a id="ipi__driver_8h_1aa28a74615fcd7134e138ca759c1e0054"></a> IPI\_VALUE\_MAKE(src, domain, event, payload)

<a id="c.IPI_VALUE_GET_SRC"></a>

<a id="ipi__driver_8h_1ae96fb8055d2410bcf43fb198b4ff9b70"></a> IPI\_VALUE\_GET\_SRC(value)

<a id="c.IPI_VALUE_GET_DOMAIN"></a>

<a id="ipi__driver_8h_1afd7bd17273065cef092fc7693e252290"></a> IPI\_VALUE\_GET\_DOMAIN(value)

<a id="c.IPI_VALUE_GET_EVENT"></a>

<a id="ipi__driver_8h_1a5aaf63626b2fa7a6d27ac1ce0e7b1477"></a> IPI\_VALUE\_GET\_EVENT(value)

<a id="c.IPI_VALUE_GET_PAYLOAD"></a>

<a id="ipi__driver_8h_1a98f2ec52e7392ee29fd16a243bd400ef"></a> IPI\_VALUE\_GET\_PAYLOAD(value)

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv421ipi_domain_callback_t"></a>

<a id="_CPPv321ipi_domain_callback_t"></a> <a id="_CPPv221ipi_domain_callback_t"></a> <a id="ipi_domain_callback_t"></a> <a id="ipi__driver_8h_1ab176cd4b93003e6b15d8312ccdac73cf"></a> typedef void (\*ipi\_domain\_callback\_t)([ipi\_core\_id\_t](#_CPPv413ipi_core_id_t "ipi_core_id_t") core\_id, uint32\_t value, uint8\_t src\_cpu, uint8\_t event, uint16\_t payload, void \*param)
:   Domain-level IPI callback.

    IPI is a doorbell, not a FIFO. Domain users should keep durable state in shared memory/bitmaps and use the IPI value only as a compact notification.

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv413ipi_core_id_t"></a>

<a id="_CPPv313ipi_core_id_t"></a> <a id="_CPPv213ipi_core_id_t"></a> <a id="ipi__driver_8h_1a5ab309d664e83e2b5b42b129fafa054c"></a> enum ipi\_core\_id\_t
:   *Values:*

    <a id="_CPPv4N13ipi_core_id_t12IPI_CP_CORE0E"></a>

    <a id="_CPPv3N13ipi_core_id_t12IPI_CP_CORE0E"></a> <a id="_CPPv2N13ipi_core_id_t12IPI_CP_CORE0E"></a> <a id="ipi__driver_8h_1a5ab309d664e83e2b5b42b129fafa054caf090bdfe6e3c7bdb0ca54c175ca4be0f"></a> enumerator IPI\_CP\_CORE0

    <a id="_CPPv4N13ipi_core_id_t12IPI_CP_CORE1E"></a>

    <a id="_CPPv3N13ipi_core_id_t12IPI_CP_CORE1E"></a> <a id="_CPPv2N13ipi_core_id_t12IPI_CP_CORE1E"></a> <a id="ipi__driver_8h_1a5ab309d664e83e2b5b42b129fafa054ca1e320e6c02a62a1b7d7573ddd14a9189"></a> enumerator IPI\_CP\_CORE1

    <a id="_CPPv4N13ipi_core_id_t12IPI_AP_CORE0E"></a>

    <a id="_CPPv3N13ipi_core_id_t12IPI_AP_CORE0E"></a> <a id="_CPPv2N13ipi_core_id_t12IPI_AP_CORE0E"></a> <a id="ipi__driver_8h_1a5ab309d664e83e2b5b42b129fafa054cabcdd3884d0559b4ef89568053cd2e4dc"></a> enumerator IPI\_AP\_CORE0

    <a id="_CPPv4N13ipi_core_id_t12IPI_AP_CORE1E"></a>

    <a id="_CPPv3N13ipi_core_id_t12IPI_AP_CORE1E"></a> <a id="_CPPv2N13ipi_core_id_t12IPI_AP_CORE1E"></a> <a id="ipi__driver_8h_1a5ab309d664e83e2b5b42b129fafa054ca9baf160190379f7d2349ba58b2bfa0d7"></a> enumerator IPI\_AP\_CORE1

    <a id="_CPPv4N13ipi_core_id_t12IPI_DSP_COREE"></a>

    <a id="_CPPv3N13ipi_core_id_t12IPI_DSP_COREE"></a> <a id="_CPPv2N13ipi_core_id_t12IPI_DSP_COREE"></a> <a id="ipi__driver_8h_1a5ab309d664e83e2b5b42b129fafa054ca25efbb452acc4c797049f1a11d94d614"></a> enumerator IPI\_DSP\_CORE

    <a id="_CPPv4N13ipi_core_id_t12IPI_CORE_MAXE"></a>

    <a id="_CPPv3N13ipi_core_id_t12IPI_CORE_MAXE"></a> <a id="_CPPv2N13ipi_core_id_t12IPI_CORE_MAXE"></a> <a id="ipi__driver_8h_1a5ab309d664e83e2b5b42b129fafa054cacbf291ed7a5ddb139d86d4893b8caffb"></a> enumerator IPI\_CORE\_MAX

<a id="_CPPv412ipi_domain_t"></a>

<a id="_CPPv312ipi_domain_t"></a> <a id="_CPPv212ipi_domain_t"></a> <a id="ipi__driver_8h_1ade6d680a5f1cc540192c643851b918ef"></a> enum ipi\_domain\_t
:   Software domains multiplexed over one target-core IPI channel.

    The IPI hardware provides one pending/value register per target core, not a FIFO or a set of independent logical channels. Domain encoding lets the common IPI ISR dispatch one hardware interrupt source to multiple software users without those users overwriting each other’s per-core callback.

    Encoded domain IPI values use this layout: bits 30..27: source CPU ID bits 26..24: software domain bits 23..16: domain-specific event ID bits 15..0 : domain-specific compact payload

    Domain 0 is reserved as an invalid domain, so every public IPI user must use an explicitly assigned domain. HEARTBEAT is for AP/CP liveness notifications, SMP is for cross-core scheduler/OS kicks, USB is reserved for USB/RISC-V bridge notifications, and TEST is kept for CLI/debug traffic.

    *Values:*

    <a id="_CPPv4N12ipi_domain_t19IPI_DOMAIN_RESERVEDE"></a>

    <a id="_CPPv3N12ipi_domain_t19IPI_DOMAIN_RESERVEDE"></a> <a id="_CPPv2N12ipi_domain_t19IPI_DOMAIN_RESERVEDE"></a> <a id="ipi__driver_8h_1ade6d680a5f1cc540192c643851b918efa021132b0fbb48dff1df0dd80f79d00d4"></a> enumerator IPI\_DOMAIN\_RESERVED

    <a id="_CPPv4N12ipi_domain_t20IPI_DOMAIN_HEARTBEATE"></a>

    <a id="_CPPv3N12ipi_domain_t20IPI_DOMAIN_HEARTBEATE"></a> <a id="_CPPv2N12ipi_domain_t20IPI_DOMAIN_HEARTBEATE"></a> <a id="ipi__driver_8h_1ade6d680a5f1cc540192c643851b918efa3796e67fb246db88682f682ccaa8a6c4"></a> enumerator IPI\_DOMAIN\_HEARTBEAT

    <a id="_CPPv4N12ipi_domain_t14IPI_DOMAIN_SMPE"></a>

    <a id="_CPPv3N12ipi_domain_t14IPI_DOMAIN_SMPE"></a> <a id="_CPPv2N12ipi_domain_t14IPI_DOMAIN_SMPE"></a> <a id="ipi__driver_8h_1ade6d680a5f1cc540192c643851b918efa9eb7d718ab1da6e0f9c2a7c3c084f21f"></a> enumerator IPI\_DOMAIN\_SMP

    <a id="_CPPv4N12ipi_domain_t14IPI_DOMAIN_USBE"></a>

    <a id="_CPPv3N12ipi_domain_t14IPI_DOMAIN_USBE"></a> <a id="_CPPv2N12ipi_domain_t14IPI_DOMAIN_USBE"></a> <a id="ipi__driver_8h_1ade6d680a5f1cc540192c643851b918efad714fefa2bbc6dd4ad0dc9646ace461a"></a> enumerator IPI\_DOMAIN\_USB

    <a id="_CPPv4N12ipi_domain_t24IPI_DOMAIN_CP_HANG_DEBUGE"></a>

    <a id="_CPPv3N12ipi_domain_t24IPI_DOMAIN_CP_HANG_DEBUGE"></a> <a id="_CPPv2N12ipi_domain_t24IPI_DOMAIN_CP_HANG_DEBUGE"></a> <a id="ipi__driver_8h_1ade6d680a5f1cc540192c643851b918efad461f5d96b5ada59761e32f0cb220726"></a> enumerator IPI\_DOMAIN\_CP\_HANG\_DEBUG

    <a id="_CPPv4N12ipi_domain_t15IPI_DOMAIN_TESTE"></a>

    <a id="_CPPv3N12ipi_domain_t15IPI_DOMAIN_TESTE"></a> <a id="_CPPv2N12ipi_domain_t15IPI_DOMAIN_TESTE"></a> <a id="ipi__driver_8h_1ade6d680a5f1cc540192c643851b918efaaf4b89ce55deef87cf60c838debcb595"></a> enumerator IPI\_DOMAIN\_TEST

    <a id="_CPPv4N12ipi_domain_t14IPI_DOMAIN_MAXE"></a>

    <a id="_CPPv3N12ipi_domain_t14IPI_DOMAIN_MAXE"></a> <a id="_CPPv2N12ipi_domain_t14IPI_DOMAIN_MAXE"></a> <a id="ipi__driver_8h_1ade6d680a5f1cc540192c643851b918efa46e940aca79cdee780a4889dba4d9738"></a> enumerator IPI\_DOMAIN\_MAX
