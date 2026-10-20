---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_interrupt.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="interrupt-control-unit"></a>

# Interrupt Control Unit

Beken chip supports interrupt service function registe for user.

<a id="interrupt-api-status"></a>

## Interrupt API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_int_isr_register()`](#_CPPv419bk_int_isr_register13icu_int_src_t15int_group_isr_tPv "bk_int_isr_register") | Y |
| [`bk_int_isr_unregister()`](#_CPPv421bk_int_isr_unregister13icu_int_src_t "bk_int_isr_unregister") | Y |
| [`bk_int_set_priority()`](#_CPPv419bk_int_set_priority13icu_int_src_t8uint32_t "bk_int_set_priority") | Y |
| [`bk_int_set_group()`](#_CPPv416bk_int_set_groupv "bk_int_set_group") | Y |
| `bk_get_int_statis()` | Y |
| `bk_dump_int_statis()` | Y |

<a id="interrupt-api-reference"></a>

## Interrupt API Reference

<a id="header-file"></a>

### Header File

- [int.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/int.h)

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

<a id="_CPPv319bk_int_isr_register13icu_int_src_t15int_group_isr_tPv"></a> <a id="_CPPv219bk_int_isr_register13icu_int_src_t15int_group_isr_tPv"></a> <a id="bk_int_isr_register__icu_int_src_t.int_group_isr_t.voidP"></a> <a id="group__bk__api__icu_1gab1929863601295d456177900afef5299"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_int\_isr\_register([icu\_int\_src\_t](#_CPPv413icu_int_src_t "icu_int_src_t") dev, int\_group\_isr\_t isr, void \*arg)
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

<a id="_CPPv321bk_int_isr_unregister13icu_int_src_t"></a> <a id="_CPPv221bk_int_isr_unregister13icu_int_src_t"></a> <a id="bk_int_isr_unregister__icu_int_src_t"></a> <a id="group__bk__api__icu_1ga0d78f93b9b48af2d17e5416e4462e824"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_int\_isr\_unregister([icu\_int\_src\_t](#_CPPv413icu_int_src_t "icu_int_src_t") src)
:   unregister interrupt service handler

    参数
    :   **dev** – interrupt source device

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_INT\_DEVICE\_NONE:no int device
        - others: other errors.

<a id="_CPPv419bk_int_set_priority13icu_int_src_t8uint32_t"></a>

<a id="_CPPv319bk_int_set_priority13icu_int_src_t8uint32_t"></a> <a id="_CPPv219bk_int_set_priority13icu_int_src_t8uint32_t"></a> <a id="bk_int_set_priority__icu_int_src_t.uint32_t"></a> <a id="group__bk__api__icu_1ga4a608665a47286894f417e7ac3617dd8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_int\_set\_priority([icu\_int\_src\_t](#_CPPv413icu_int_src_t "icu_int_src_t") src, uint32\_t int\_priority)
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

- [int\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/int_types.h)

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

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv413icu_int_src_t"></a>

<a id="_CPPv313icu_int_src_t"></a> <a id="_CPPv213icu_int_src_t"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8b"></a> enum icu\_int\_src\_t
:   *Values:*

    <a id="_CPPv4N13icu_int_src_t13INT_SRC_UART0E"></a>

    <a id="_CPPv3N13icu_int_src_t13INT_SRC_UART0E"></a> <a id="_CPPv2N13icu_int_src_t13INT_SRC_UART0E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baf818169e4a39b9c8c67502fe7e45f0df"></a> enumerator INT\_SRC\_UART0

    <a id="_CPPv4N13icu_int_src_t13INT_SRC_UART1E"></a>

    <a id="_CPPv3N13icu_int_src_t13INT_SRC_UART1E"></a> <a id="_CPPv2N13icu_int_src_t13INT_SRC_UART1E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baed79fbb60003097867bafec78cc20e5f"></a> enumerator INT\_SRC\_UART1

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_I2C0E"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_I2C0E"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_I2C0E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bacffc385e3df72516ef3389c6b14552d0"></a> enumerator INT\_SRC\_I2C0

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_IRDAE"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_IRDAE"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_IRDAE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baa8973f07fa8d3ef2ca5bc2056cd3fc88"></a> enumerator INT\_SRC\_IRDA

    <a id="_CPPv4N13icu_int_src_t11INT_SRC_I2SE"></a>

    <a id="_CPPv3N13icu_int_src_t11INT_SRC_I2SE"></a> <a id="_CPPv2N13icu_int_src_t11INT_SRC_I2SE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba8ec4f9fd916cf39db10c0b058b39b87a"></a> enumerator INT\_SRC\_I2S

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_I2C1E"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_I2C1E"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_I2C1E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baf7bfdbc161fb4724e080ae6dbed4f704"></a> enumerator INT\_SRC\_I2C1

    <a id="_CPPv4N13icu_int_src_t11INT_SRC_SPIE"></a>

    <a id="_CPPv3N13icu_int_src_t11INT_SRC_SPIE"></a> <a id="_CPPv2N13icu_int_src_t11INT_SRC_SPIE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba628fa04e6d232b6af770f4fcbf349a64"></a> enumerator INT\_SRC\_SPI

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_GPIOE"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_GPIOE"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_GPIOE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bab3d57806551a3ea6166b73e0723ae975"></a> enumerator INT\_SRC\_GPIO

    <a id="_CPPv4N13icu_int_src_t13INT_SRC_TIMERE"></a>

    <a id="_CPPv3N13icu_int_src_t13INT_SRC_TIMERE"></a> <a id="_CPPv2N13icu_int_src_t13INT_SRC_TIMERE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba38a6ee2e7cdc1c5c7b8b7a689be1a9c7"></a> enumerator INT\_SRC\_TIMER

    <a id="_CPPv4N13icu_int_src_t11INT_SRC_PWME"></a>

    <a id="_CPPv3N13icu_int_src_t11INT_SRC_PWME"></a> <a id="_CPPv2N13icu_int_src_t11INT_SRC_PWME"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baef9c0d432a51ddf660b64c0c9243ced9"></a> enumerator INT\_SRC\_PWM

    <a id="_CPPv4N13icu_int_src_t13INT_SRC_AUDIOE"></a>

    <a id="_CPPv3N13icu_int_src_t13INT_SRC_AUDIOE"></a> <a id="_CPPv2N13icu_int_src_t13INT_SRC_AUDIOE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba989d36a574864c2e055cc89e613b7625"></a> enumerator INT\_SRC\_AUDIO

    <a id="_CPPv4N13icu_int_src_t14INT_SRC_SARADCE"></a>

    <a id="_CPPv3N13icu_int_src_t14INT_SRC_SARADCE"></a> <a id="_CPPv2N13icu_int_src_t14INT_SRC_SARADCE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bac2daa4ead630b1cde62032f1db088618"></a> enumerator INT\_SRC\_SARADC

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_SDIOE"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_SDIOE"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_SDIOE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba926832b728e894fa494143fb3966732d"></a> enumerator INT\_SRC\_SDIO

    <a id="_CPPv4N13icu_int_src_t11INT_SRC_USBE"></a>

    <a id="_CPPv3N13icu_int_src_t11INT_SRC_USBE"></a> <a id="_CPPv2N13icu_int_src_t11INT_SRC_USBE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba483a24b60244b993c12624ac16012f2f"></a> enumerator INT\_SRC\_USB

    <a id="_CPPv4N13icu_int_src_t11INT_SRC_FFTE"></a>

    <a id="_CPPv3N13icu_int_src_t11INT_SRC_FFTE"></a> <a id="_CPPv2N13icu_int_src_t11INT_SRC_FFTE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba6a486a4a1bad84a45a606eab52d60943"></a> enumerator INT\_SRC\_FFT

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_GDMAE"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_GDMAE"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_GDMAE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baa49a9542596419132dfe90d615537e9d"></a> enumerator INT\_SRC\_GDMA

    <a id="_CPPv4N13icu_int_src_t13INT_SRC_MODEME"></a>

    <a id="_CPPv3N13icu_int_src_t13INT_SRC_MODEME"></a> <a id="_CPPv2N13icu_int_src_t13INT_SRC_MODEME"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bac9ff348d0c1a0f58552091d54d9747f0"></a> enumerator INT\_SRC\_MODEM

    <a id="_CPPv4N13icu_int_src_t22INT_SRC_MAC_TXRX_TIMERE"></a>

    <a id="_CPPv3N13icu_int_src_t22INT_SRC_MAC_TXRX_TIMERE"></a> <a id="_CPPv2N13icu_int_src_t22INT_SRC_MAC_TXRX_TIMERE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8badf69b8169b8458b0495c4e469ad75379"></a> enumerator INT\_SRC\_MAC\_TXRX\_TIMER

    <a id="_CPPv4N13icu_int_src_t21INT_SRC_MAC_TXRX_MISCE"></a>

    <a id="_CPPv3N13icu_int_src_t21INT_SRC_MAC_TXRX_MISCE"></a> <a id="_CPPv2N13icu_int_src_t21INT_SRC_MAC_TXRX_MISCE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bac320fda4a1a7862d68be0a6a1b62cf68"></a> enumerator INT\_SRC\_MAC\_TXRX\_MISC

    <a id="_CPPv4N13icu_int_src_t22INT_SRC_MAC_RX_TRIGGERE"></a>

    <a id="_CPPv3N13icu_int_src_t22INT_SRC_MAC_RX_TRIGGERE"></a> <a id="_CPPv2N13icu_int_src_t22INT_SRC_MAC_RX_TRIGGERE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baf42644a7696b0db1c67a74a810159876"></a> enumerator INT\_SRC\_MAC\_RX\_TRIGGER

    <a id="_CPPv4N13icu_int_src_t22INT_SRC_MAC_TX_TRIGGERE"></a>

    <a id="_CPPv3N13icu_int_src_t22INT_SRC_MAC_TX_TRIGGERE"></a> <a id="_CPPv2N13icu_int_src_t22INT_SRC_MAC_TX_TRIGGERE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba96d038c52039189fda0104a2836e2f99"></a> enumerator INT\_SRC\_MAC\_TX\_TRIGGER

    <a id="_CPPv4N13icu_int_src_t24INT_SRC_MAC_PROT_TRIGGERE"></a>

    <a id="_CPPv3N13icu_int_src_t24INT_SRC_MAC_PROT_TRIGGERE"></a> <a id="_CPPv2N13icu_int_src_t24INT_SRC_MAC_PROT_TRIGGERE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bad6ca1d3ecb6db1fa2f0b4f8ac0f8f3d0"></a> enumerator INT\_SRC\_MAC\_PROT\_TRIGGER

    <a id="_CPPv4N13icu_int_src_t19INT_SRC_MAC_GENERALE"></a>

    <a id="_CPPv3N13icu_int_src_t19INT_SRC_MAC_GENERALE"></a> <a id="_CPPv2N13icu_int_src_t19INT_SRC_MAC_GENERALE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bad551c34be50e57f72dcb74a5805ca270"></a> enumerator INT\_SRC\_MAC\_GENERAL

    <a id="_CPPv4N13icu_int_src_t16INT_SRC_SDIO_DMAE"></a>

    <a id="_CPPv3N13icu_int_src_t16INT_SRC_SDIO_DMAE"></a> <a id="_CPPv2N13icu_int_src_t16INT_SRC_SDIO_DMAE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bad2580a924f6cb8dec005e214953a8044"></a> enumerator INT\_SRC\_SDIO\_DMA

    <a id="_CPPv4N13icu_int_src_t22INT_SRC_USB_PLUG_INOUTE"></a>

    <a id="_CPPv3N13icu_int_src_t22INT_SRC_USB_PLUG_INOUTE"></a> <a id="_CPPv2N13icu_int_src_t22INT_SRC_USB_PLUG_INOUTE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba8470fe35387a3ca9744d2f9bb86139c2"></a> enumerator INT\_SRC\_USB\_PLUG\_INOUT

    <a id="_CPPv4N13icu_int_src_t16INT_SRC_SECURITYE"></a>

    <a id="_CPPv3N13icu_int_src_t16INT_SRC_SECURITYE"></a> <a id="_CPPv2N13icu_int_src_t16INT_SRC_SECURITYE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bab925d493b608c35489a7ed71adfd6194"></a> enumerator INT\_SRC\_SECURITY

    <a id="_CPPv4N13icu_int_src_t18INT_SRC_MAC_WAKEUPE"></a>

    <a id="_CPPv3N13icu_int_src_t18INT_SRC_MAC_WAKEUPE"></a> <a id="_CPPv2N13icu_int_src_t18INT_SRC_MAC_WAKEUPE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba5881228a1fa1c7bd7b5f89322f8e24e8"></a> enumerator INT\_SRC\_MAC\_WAKEUP

    <a id="_CPPv4N13icu_int_src_t19INT_SRC_HSSPI_SLAVEE"></a>

    <a id="_CPPv3N13icu_int_src_t19INT_SRC_HSSPI_SLAVEE"></a> <a id="_CPPv2N13icu_int_src_t19INT_SRC_HSSPI_SLAVEE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba9251e58778ff2360fe9ffd1691e07178"></a> enumerator INT\_SRC\_HSSPI\_SLAVE

    <a id="_CPPv4N13icu_int_src_t18INT_SRC_PLL_UNLOCKE"></a>

    <a id="_CPPv3N13icu_int_src_t18INT_SRC_PLL_UNLOCKE"></a> <a id="_CPPv2N13icu_int_src_t18INT_SRC_PLL_UNLOCKE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8badd2dcb87a32ae0da0b1295cd2c817710"></a> enumerator INT\_SRC\_PLL\_UNLOCK

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_JPEGE"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_JPEGE"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_JPEGE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba5f35fca8a76f6b61de7a6d1bc5430c93"></a> enumerator INT\_SRC\_JPEG

    <a id="_CPPv4N13icu_int_src_t11INT_SRC_BLEE"></a>

    <a id="_CPPv3N13icu_int_src_t11INT_SRC_BLEE"></a> <a id="_CPPv2N13icu_int_src_t11INT_SRC_BLEE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba170d7dccdc49506df11150506a1b29db"></a> enumerator INT\_SRC\_BLE

    <a id="_CPPv4N13icu_int_src_t13INT_SRC_PSRAME"></a>

    <a id="_CPPv3N13icu_int_src_t13INT_SRC_PSRAME"></a> <a id="_CPPv2N13icu_int_src_t13INT_SRC_PSRAME"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba069ff0c1a6d33bc34f58895190177ca4"></a> enumerator INT\_SRC\_PSRAM

    <a id="_CPPv4N13icu_int_src_t10INT_SRC_LAE"></a>

    <a id="_CPPv3N13icu_int_src_t10INT_SRC_LAE"></a> <a id="_CPPv2N13icu_int_src_t10INT_SRC_LAE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba23cb031fc3c32a89f46c75b2b2f05c2e"></a> enumerator INT\_SRC\_LA

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_BTDME"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_BTDME"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_BTDME"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba0ef7ca7ecfe5adfc31bcd6270a262ec5"></a> enumerator INT\_SRC\_BTDM

    <a id="_CPPv4N13icu_int_src_t10INT_SRC_BTE"></a>

    <a id="_CPPv3N13icu_int_src_t10INT_SRC_BTE"></a> <a id="_CPPv2N13icu_int_src_t10INT_SRC_BTE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bacf69c0a258698b411ce408ae9c51eb6c"></a> enumerator INT\_SRC\_BT

    <a id="_CPPv4N13icu_int_src_t13INT_SRC_UART2E"></a>

    <a id="_CPPv3N13icu_int_src_t13INT_SRC_UART2E"></a> <a id="_CPPv2N13icu_int_src_t13INT_SRC_UART2E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bad43f5da31fbdcf7f9f9397e058b6fbcf"></a> enumerator INT\_SRC\_UART2

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_I2C2E"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_I2C2E"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_I2C2E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bafa6c6841b875e804d66d27874a92d711"></a> enumerator INT\_SRC\_I2C2

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_SPI2E"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_SPI2E"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_SPI2E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba5e816cd12648c46509f8643b56ccbd6f"></a> enumerator INT\_SRC\_SPI2

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_SPI3E"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_SPI3E"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_SPI3E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba9121c4ec237c136fbcdb9531aec09bc5"></a> enumerator INT\_SRC\_SPI3

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_PWM2E"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_PWM2E"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_PWM2E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bac21b6a880a0e331e0749f93fedd08eaf"></a> enumerator INT\_SRC\_PWM2

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_USB2E"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_USB2E"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_USB2E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba16271e46a4961848ee68d5507b9c62f9"></a> enumerator INT\_SRC\_USB2

    <a id="_CPPv4N13icu_int_src_t16INT_SRC_MAILBOX0E"></a>

    <a id="_CPPv3N13icu_int_src_t16INT_SRC_MAILBOX0E"></a> <a id="_CPPv2N13icu_int_src_t16INT_SRC_MAILBOX0E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba6cac44bed2ade3d8f2ea8e58544b889b"></a> enumerator INT\_SRC\_MAILBOX0

    <a id="_CPPv4N13icu_int_src_t16INT_SRC_MAILBOX1E"></a>

    <a id="_CPPv3N13icu_int_src_t16INT_SRC_MAILBOX1E"></a> <a id="_CPPv2N13icu_int_src_t16INT_SRC_MAILBOX1E"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baf2f4e300092a3f4db568a08fcf9f28ca"></a> enumerator INT\_SRC\_MAILBOX1

    <a id="_CPPv4N13icu_int_src_t14INT_SRC_BT_WDTE"></a>

    <a id="_CPPv3N13icu_int_src_t14INT_SRC_BT_WDTE"></a> <a id="_CPPv2N13icu_int_src_t14INT_SRC_BT_WDTE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8badcd1fb4a03a3d35c780f9ad4fbc71945"></a> enumerator INT\_SRC\_BT\_WDT

    <a id="_CPPv4N13icu_int_src_t15INT_SRC_DSP_WDTE"></a>

    <a id="_CPPv3N13icu_int_src_t15INT_SRC_DSP_WDTE"></a> <a id="_CPPv2N13icu_int_src_t15INT_SRC_DSP_WDTE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bafd4fcd0253334dc67227d27803642909"></a> enumerator INT\_SRC\_DSP\_WDT

    <a id="_CPPv4N13icu_int_src_t11INT_SRC_RTCE"></a>

    <a id="_CPPv3N13icu_int_src_t11INT_SRC_RTCE"></a> <a id="_CPPv2N13icu_int_src_t11INT_SRC_RTCE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba01dc958c68dff8b95be176923bacd130"></a> enumerator INT\_SRC\_RTC

    <a id="_CPPv4N13icu_int_src_t13INT_SRC_TOUCHE"></a>

    <a id="_CPPv3N13icu_int_src_t13INT_SRC_TOUCHE"></a> <a id="_CPPv2N13icu_int_src_t13INT_SRC_TOUCHE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baef32ed221271315c7ed8c9f9410792a4"></a> enumerator INT\_SRC\_TOUCH

    <a id="_CPPv4N13icu_int_src_t11INT_SRC_CECE"></a>

    <a id="_CPPv3N13icu_int_src_t11INT_SRC_CECE"></a> <a id="_CPPv2N13icu_int_src_t11INT_SRC_CECE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8bad7dea9323e0732c9975865e95b02e207"></a> enumerator INT\_SRC\_CEC

    <a id="_CPPv4N13icu_int_src_t16INT_SRC_MODEM_RCE"></a>

    <a id="_CPPv3N13icu_int_src_t16INT_SRC_MODEM_RCE"></a> <a id="_CPPv2N13icu_int_src_t16INT_SRC_MODEM_RCE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba2eacf20832c04b6e7ab68defa82c3c8b"></a> enumerator INT\_SRC\_MODEM\_RC

    <a id="_CPPv4N13icu_int_src_t15INT_SRC_MAC_HSUE"></a>

    <a id="_CPPv3N13icu_int_src_t15INT_SRC_MAC_HSUE"></a> <a id="_CPPv2N13icu_int_src_t15INT_SRC_MAC_HSUE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8baecd4b45e152c609cdbe1c74740774834"></a> enumerator INT\_SRC\_MAC\_HSU

    <a id="_CPPv4N13icu_int_src_t12INT_SRC_NONEE"></a>

    <a id="_CPPv3N13icu_int_src_t12INT_SRC_NONEE"></a> <a id="_CPPv2N13icu_int_src_t12INT_SRC_NONEE"></a> <a id="int__types_8h_1a260745bc02479944f2dd03630e14ce8ba23551ab375db75f1048d3b773e0ca62a"></a> enumerator INT\_SRC\_NONE
