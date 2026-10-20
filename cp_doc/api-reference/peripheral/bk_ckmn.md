---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_ckmn.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ckmn"></a>

# CKMN

BK7259 CP 侧 CKMN（Clock Monitor）API（`include/driver/ckmn.h`）。

<a id="ckmn-api-reference"></a>

## CKMN API Reference

<a id="header-file"></a>

### Header File

- [ckmn.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/ckmn.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419bk_ckmn_driver_initv"></a>

<a id="_CPPv319bk_ckmn_driver_initv"></a> <a id="_CPPv219bk_ckmn_driver_initv"></a> <a id="bk_ckmn_driver_init__void"></a> <a id="group__bk__api__ckmn_1gab0e65dd9eedc9abad87e7641196a83da"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_driver\_init(void)
:   Init the CKMN driver.

    This API init the resoure common:

    - Init CKMN driver control memory

    **Attention**
    :   1\. This API should be called before any other CKMN APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_ckmn_driver_deinitv"></a>

<a id="_CPPv321bk_ckmn_driver_deinitv"></a> <a id="_CPPv221bk_ckmn_driver_deinitv"></a> <a id="bk_ckmn_driver_deinit__void"></a> <a id="group__bk__api__ckmn_1gadcca9953aaf429989a419b21f62b0ff8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_driver\_deinit(void)
:   Deinit the CKMN driver.

    This API free all resource related to CKMN and disable CKMN.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_ckmn_register_isr15ckmn_int_type_t10ckmn_isr_t"></a>

<a id="_CPPv320bk_ckmn_register_isr15ckmn_int_type_t10ckmn_isr_t"></a> <a id="_CPPv220bk_ckmn_register_isr15ckmn_int_type_t10ckmn_isr_t"></a> <a id="bk_ckmn_register_isr__ckmn_int_type_t.ckmn_isr_t"></a> <a id="group__bk__api__ckmn_1ga1a5617e93579ef614d4d06e50946bc61"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_register\_isr([ckmn\_int\_type\_t](#_CPPv415ckmn_int_type_t "ckmn_int_type_t") int\_type, [ckmn\_isr\_t](#_CPPv410ckmn_isr_t "ckmn_isr_t") int\_isr)
:   Register the interrupt service routine for CKMN.

    This API regist ckmn isr callback function.

    参数
    :   - **int\_type** – register interrupt type
        - **int\_isr** – ckmn callback

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_ckmn_unregister_isr15ckmn_int_type_t"></a>

<a id="_CPPv322bk_ckmn_unregister_isr15ckmn_int_type_t"></a> <a id="_CPPv222bk_ckmn_unregister_isr15ckmn_int_type_t"></a> <a id="bk_ckmn_unregister_isr__ckmn_int_type_t"></a> <a id="group__bk__api__ckmn_1ga215ccc329b9c46380a84dcc88ecbc654"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_unregister\_isr([ckmn\_int\_type\_t](#_CPPv415ckmn_int_type_t "ckmn_int_type_t") int\_type)
:   Unregister the interrupt service routine for CKMN.

    This API regist ckmn isr callback function.

    参数
    :   **int\_type** – register interrupt type

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_ckmn_soft_resetv"></a>

<a id="_CPPv318bk_ckmn_soft_resetv"></a> <a id="_CPPv218bk_ckmn_soft_resetv"></a> <a id="bk_ckmn_soft_reset__void"></a> <a id="group__bk__api__ckmn_1ga906e44d789be3f351e14c66d4ae5632c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_soft\_reset(void)
:   ckmn soft reset

    This API reset ckmn module

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_ckmn_sleep_regs_backupv"></a>

<a id="_CPPv325bk_ckmn_sleep_regs_backupv"></a> <a id="_CPPv225bk_ckmn_sleep_regs_backupv"></a> <a id="bk_ckmn_sleep_regs_backup__void"></a> <a id="group__bk__api__ckmn_1ga11ad5dcbd9311219ed7dc264bc8f1952"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_sleep\_regs\_backup(void)
:   Backup CKMN registers before sleep.

    This API saves CKMN R/W configuration registers before low voltage sleep.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_ckmn_sleep_regs_restorev"></a>

<a id="_CPPv326bk_ckmn_sleep_regs_restorev"></a> <a id="_CPPv226bk_ckmn_sleep_regs_restorev"></a> <a id="bk_ckmn_sleep_regs_restore__void"></a> <a id="group__bk__api__ckmn_1gaa48a76f093db17904b4c2daddee2ec9d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_sleep\_regs\_restore(void)
:   Restore CKMN registers after wakeup.

    This API reinitializes CKMN interrupt/HAL state and restores CKMN R/W configuration registers saved before sleep.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv428bk_ckmn_power_down_for_sleepv"></a>

<a id="_CPPv328bk_ckmn_power_down_for_sleepv"></a> <a id="_CPPv228bk_ckmn_power_down_for_sleepv"></a> <a id="bk_ckmn_power_down_for_sleep__void"></a> <a id="group__bk__api__ckmn_1gaec67a988eece0c1bace0d0dd409002b0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_power\_down\_for\_sleep(void)
:   Power down CKMN before low voltage sleep.

    Disable ckest/correction and clear CKMN control registers to minimize AON leakage during sleep.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv429bk_ckmn_sleep_regs_get_backupP8uint32_tP8uint32_tP8uint32_t"></a>

<a id="_CPPv329bk_ckmn_sleep_regs_get_backupP8uint32_tP8uint32_tP8uint32_t"></a> <a id="_CPPv229bk_ckmn_sleep_regs_get_backupP8uint32_tP8uint32_tP8uint32_t"></a> <a id="bk_ckmn_sleep_regs_get_backup__uint32_tP.uint32_tP.uint32_tP"></a> <a id="group__bk__api__ckmn_1ga58159bae8bd843568093684ea152cdbb"></a> void bk\_ckmn\_sleep\_regs\_get\_backup(uint32\_t \*global\_ctrl, uint32\_t \*rc32k\_ctrl, uint32\_t \*corr\_cfg)
:   Get last CKMN sleep backup register values.

    参数
    :   - **global\_ctrl** – saved CKMN\_CTRL
        - **rc32k\_ctrl** – saved CKMN\_RC32K\_CTRL
        - **corr\_cfg** – saved CKMN\_CORR\_CFG

<a id="_CPPv423bk_ckmn_set_rc32k_count8uint32_t"></a>

<a id="_CPPv323bk_ckmn_set_rc32k_count8uint32_t"></a> <a id="_CPPv223bk_ckmn_set_rc32k_count8uint32_t"></a> <a id="bk_ckmn_set_rc32k_count__uint32_t"></a> <a id="group__bk__api__ckmn_1gac098c6f42c79760cf6829bf1f61afb78"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_set\_rc32k\_count(uint32\_t count)
:   Set the number of counts for RC32K accuracy statistics.

    This API 26m digital clock measurement 32k analog clock.

    参数
    :   **count** – number of clock cycles

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_ckmn_get_rc32k_countv"></a>

<a id="_CPPv323bk_ckmn_get_rc32k_countv"></a> <a id="_CPPv223bk_ckmn_get_rc32k_countv"></a> <a id="bk_ckmn_get_rc32k_count__void"></a> <a id="group__bk__api__ckmn_1gadf5955e49cc683de46c4b0d9d7a609cb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_get\_rc32k\_count(void)
:   Get the number of counts for RC32K accuracy statistics.

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - count number of clock cycles

<a id="_CPPv420bk_ckmn_ckest_enablev"></a>

<a id="_CPPv320bk_ckmn_ckest_enablev"></a> <a id="_CPPv220bk_ckmn_ckest_enablev"></a> <a id="bk_ckmn_ckest_enable__void"></a> <a id="group__bk__api__ckmn_1ga2895f5402053b7b66fc48cd3431f6b7d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_ckest\_enable(void)
:   enable RC32K accuracy statistics

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_ckmn_ckest_disablev"></a>

<a id="_CPPv321bk_ckmn_ckest_disablev"></a> <a id="_CPPv221bk_ckmn_ckest_disablev"></a> <a id="bk_ckmn_ckest_disable__void"></a> <a id="group__bk__api__ckmn_1gac3979a395380beb1512fee3b5835655e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_ckest\_disable(void)
:   disable RC32K accuracy statistics

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_ckmn_ckest_check_busyv"></a>

<a id="_CPPv324bk_ckmn_ckest_check_busyv"></a> <a id="_CPPv224bk_ckmn_ckest_check_busyv"></a> <a id="bk_ckmn_ckest_check_busy__void"></a> <a id="group__bk__api__ckmn_1ga76c9c8f6c632eb7d86eb25484a4f6da4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_ckest\_check\_busy(void)
:   check if ckest is busy

    This API checks if chest is on measurement.

    返回
    :   - BK\_OK: ckest is ready
        - others: ckest is busy.

<a id="_CPPv423bk_ckmn_get_rc26m_countv"></a>

<a id="_CPPv323bk_ckmn_get_rc26m_countv"></a> <a id="_CPPv223bk_ckmn_get_rc26m_countv"></a> <a id="bk_ckmn_get_rc26m_count__void"></a> <a id="group__bk__api__ckmn_1ga8738375aff3682c07899dfe697e7bc73"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_get\_rc26m\_count(void)
:   get ther number of mappings of RC32K accuracy statistics in the 26m domain

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - ther number of mappings

<a id="_CPPv429bk_ckmn_driver_get_rc32k_freqv"></a>

<a id="_CPPv329bk_ckmn_driver_get_rc32k_freqv"></a> <a id="_CPPv229bk_ckmn_driver_get_rc32k_freqv"></a> <a id="bk_ckmn_driver_get_rc32k_freq__void"></a> <a id="group__bk__api__ckmn_1ga58359f917e192ad0413dd90af67d19b8"></a> double bk\_ckmn\_driver\_get\_rc32k\_freq(void)
:   Get calibrated 32k clock frequency.

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - alibrated 32k clock frequency value.

<a id="_CPPv428bk_ckmn_driver_get_rc32k_ppmv"></a>

<a id="_CPPv328bk_ckmn_driver_get_rc32k_ppmv"></a> <a id="_CPPv228bk_ckmn_driver_get_rc32k_ppmv"></a> <a id="bk_ckmn_driver_get_rc32k_ppm__void"></a> <a id="group__bk__api__ckmn_1ga32a4258eb33e95a13f49f6abb595d12b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_driver\_get\_rc32k\_ppm(void)
:   Get calibrated 32k clock ppm.

    This API tells the current clock ppm of rc32k.

    返回
    :   - alibrated 32k clock ppm value.

<a id="_CPPv425bk_ckmn_driver_rc32k_prog8uint32_t"></a>

<a id="_CPPv325bk_ckmn_driver_rc32k_prog8uint32_t"></a> <a id="_CPPv225bk_ckmn_driver_rc32k_prog8uint32_t"></a> <a id="bk_ckmn_driver_rc32k_prog__uint32_t"></a> <a id="group__bk__api__ckmn_1ga6bfd17aa5432b0a2f580ff2fa7b4c5c4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_driver\_rc32k\_prog(uint32\_t count)
:   Perform 32k frequency calibration.

    This API 26m digital clock measurement 32k analog clock.

    参数
    :   **count** – number of clock cycles

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_ckmn_set_26m_target10ckmn_acc_t"></a>

<a id="_CPPv322bk_ckmn_set_26m_target10ckmn_acc_t"></a> <a id="_CPPv222bk_ckmn_set_26m_target10ckmn_acc_t"></a> <a id="bk_ckmn_set_26m_target__ckmn_acc_t"></a> <a id="group__bk__api__ckmn_1ga7e244f71c37a587a9e2c23ca76b33b6d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_set\_26m\_target([ckmn\_acc\_t](#_CPPv410ckmn_acc_t "ckmn_acc_t") target)
:   Set 26m clock accuracy related targets.

    This API auto clock switching.

    参数
    :   **target** – accuracy percentage

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_ckmn_enable_autosw_26mv"></a>

<a id="_CPPv325bk_ckmn_enable_autosw_26mv"></a> <a id="_CPPv225bk_ckmn_enable_autosw_26mv"></a> <a id="bk_ckmn_enable_autosw_26m__void"></a> <a id="group__bk__api__ckmn_1ga18a841fb12b8643c8a6be9f7f85bc517"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_enable\_autosw\_26m(void)
:   enable 26m clock auto switching

    This API auto clock switching..

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_ckmn_disable_autosw_26mv"></a>

<a id="_CPPv326bk_ckmn_disable_autosw_26mv"></a> <a id="_CPPv226bk_ckmn_disable_autosw_26mv"></a> <a id="bk_ckmn_disable_autosw_26m__void"></a> <a id="group__bk__api__ckmn_1ga9e5c3f291d905681851db6b2510129a5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_disable\_autosw\_26m(void)
:   disable 26m clock auto switching

    This API auto clock switching..

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_ckmn_enable_corr_26mv"></a>

<a id="_CPPv323bk_ckmn_enable_corr_26mv"></a> <a id="_CPPv223bk_ckmn_enable_corr_26mv"></a> <a id="bk_ckmn_enable_corr_26m__void"></a> <a id="group__bk__api__ckmn_1ga69d9b11f5c54df58803767c03383fdcc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_enable\_corr\_26m(void)
:   enable 26m clock accuracy detection and enable interrupt

    This API auto clock switching..

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_ckmn_disable_corr_26mv"></a>

<a id="_CPPv324bk_ckmn_disable_corr_26mv"></a> <a id="_CPPv224bk_ckmn_disable_corr_26mv"></a> <a id="bk_ckmn_disable_corr_26m__void"></a> <a id="group__bk__api__ckmn_1gadb25f82f87792553e8caeeca6e62f500"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_disable\_corr\_26m(void)
:   disable 26m clock accuracy detection and disable interrupt

    This API auto clock switching..

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_ckmn_set_32k_target10ckmn_acc_t"></a>

<a id="_CPPv322bk_ckmn_set_32k_target10ckmn_acc_t"></a> <a id="_CPPv222bk_ckmn_set_32k_target10ckmn_acc_t"></a> <a id="bk_ckmn_set_32k_target__ckmn_acc_t"></a> <a id="group__bk__api__ckmn_1gaa5363fb908ea29af4dd4c323eb76f6f1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_set\_32k\_target([ckmn\_acc\_t](#_CPPv410ckmn_acc_t "ckmn_acc_t") target)
:   Set 32k clock accuracy related targets.

    This API auto clock switching.

    参数
    :   **target** – accuracy percentage

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_ckmn_enable_autosw_32kv"></a>

<a id="_CPPv325bk_ckmn_enable_autosw_32kv"></a> <a id="_CPPv225bk_ckmn_enable_autosw_32kv"></a> <a id="bk_ckmn_enable_autosw_32k__void"></a> <a id="group__bk__api__ckmn_1ga81c87045a268fa4a7579ce5548925559"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_enable\_autosw\_32k(void)
:   enable 32k clock auto switching

    This API auto clock switching..

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_ckmn_disable_autosw_32kv"></a>

<a id="_CPPv326bk_ckmn_disable_autosw_32kv"></a> <a id="_CPPv226bk_ckmn_disable_autosw_32kv"></a> <a id="bk_ckmn_disable_autosw_32k__void"></a> <a id="group__bk__api__ckmn_1gafa76fe7b2ab0ad26aca7f65c7f8b6706"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_disable\_autosw\_32k(void)
:   disable 32k clock auto switching

    This API auto clock switching..

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_ckmn_enable_corr_32kv"></a>

<a id="_CPPv323bk_ckmn_enable_corr_32kv"></a> <a id="_CPPv223bk_ckmn_enable_corr_32kv"></a> <a id="bk_ckmn_enable_corr_32k__void"></a> <a id="group__bk__api__ckmn_1gab4fb00415942d7905b1414cc46008ba4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_enable\_corr\_32k(void)
:   enable 32k clock accuracy detection and enable interrupt

    This API clock accuracy detection..

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_ckmn_disable_corr_32kv"></a>

<a id="_CPPv324bk_ckmn_disable_corr_32kv"></a> <a id="_CPPv224bk_ckmn_disable_corr_32kv"></a> <a id="bk_ckmn_disable_corr_32k__void"></a> <a id="group__bk__api__ckmn_1gaa319839b09c8391796318b77420b584f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_disable\_corr\_32k(void)
:   disable 32k clock accuracy detection and disable interrupt

    This API clock accuracy detection..

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_ckmn_cor26m_intr_enablev"></a>

<a id="_CPPv326bk_ckmn_cor26m_intr_enablev"></a> <a id="_CPPv226bk_ckmn_cor26m_intr_enablev"></a> <a id="bk_ckmn_cor26m_intr_enable__void"></a> <a id="group__bk__api__ckmn_1ga72baad81d84c5a82864bc3a007b695ce"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_cor26m\_intr\_enable(void)
:   enable 26m clock auto switching interrupt

    This API clock accuracy detection interrupt

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_ckmn_cor26m_intr_disablev"></a>

<a id="_CPPv327bk_ckmn_cor26m_intr_disablev"></a> <a id="_CPPv227bk_ckmn_cor26m_intr_disablev"></a> <a id="bk_ckmn_cor26m_intr_disable__void"></a> <a id="group__bk__api__ckmn_1gacde0927122a48ed8549a79018921188a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_cor26m\_intr\_disable(void)
:   disable 26m clock auto switching interrupt

    This API clock accuracy detection interrupt

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_ckmn_cor32k_intr_enablev"></a>

<a id="_CPPv326bk_ckmn_cor32k_intr_enablev"></a> <a id="_CPPv226bk_ckmn_cor32k_intr_enablev"></a> <a id="bk_ckmn_cor32k_intr_enable__void"></a> <a id="group__bk__api__ckmn_1gacd40b5193d7d63423305cc3139eded17"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_cor32k\_intr\_enable(void)
:   enable 32k clock auto switching interrupt

    This API clock accuracy detection interrupt

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_ckmn_cor32k_intr_disablev"></a>

<a id="_CPPv327bk_ckmn_cor32k_intr_disablev"></a> <a id="_CPPv227bk_ckmn_cor32k_intr_disablev"></a> <a id="bk_ckmn_cor32k_intr_disable__void"></a> <a id="group__bk__api__ckmn_1ga1028f5a1c9af7f73af5b29b5fd1b42c8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_cor32k\_intr\_disable(void)
:   disable 32k clock auto switching interrupt

    This API clock accuracy detection interrupt

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_ckmn_get_intr_statusv"></a>

<a id="_CPPv323bk_ckmn_get_intr_statusv"></a> <a id="_CPPv223bk_ckmn_get_intr_statusv"></a> <a id="bk_ckmn_get_intr_status__void"></a> <a id="group__bk__api__ckmn_1ga9dd87078e74adee8f83e14709af8754e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_get\_intr\_status(void)
:   Get all interrput status.

    This API clock accuracy detection interrupt

    返回
    :   - all interrupt value

<a id="_CPPv429bk_ckmn_get_ckest_intr_statusv"></a>

<a id="_CPPv329bk_ckmn_get_ckest_intr_statusv"></a> <a id="_CPPv229bk_ckmn_get_ckest_intr_statusv"></a> <a id="bk_ckmn_get_ckest_intr_status__void"></a> <a id="group__bk__api__ckmn_1gaca9c74989ad7151496053f4d53bac5a7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_get\_ckest\_intr\_status(void)
:   Get chest interrput status.

    This API clock accuracy detection interrupt

    返回
    :   - chest interrupt value

<a id="_CPPv430bk_ckmn_get_cor26m_intr_statusv"></a>

<a id="_CPPv330bk_ckmn_get_cor26m_intr_statusv"></a> <a id="_CPPv230bk_ckmn_get_cor26m_intr_statusv"></a> <a id="bk_ckmn_get_cor26m_intr_status__void"></a> <a id="group__bk__api__ckmn_1ga5a6319aa49c151395856f8b526198d4f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_get\_cor26m\_intr\_status(void)
:   Get cor26m interrput status.

    This API clock accuracy detection interrupt

    返回
    :   - cor26m interrupt value

<a id="_CPPv430bk_ckmn_get_cor32k_intr_statusv"></a>

<a id="_CPPv330bk_ckmn_get_cor32k_intr_statusv"></a> <a id="_CPPv230bk_ckmn_get_cor32k_intr_statusv"></a> <a id="bk_ckmn_get_cor32k_intr_status__void"></a> <a id="group__bk__api__ckmn_1ga01e86266072adc2af4188c2cead01ef8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_get\_cor32k\_intr\_status(void)
:   Get 32k interrput status.

    This API clock accuracy detection interrupt

    返回
    :   - 32k interrupt value

<a id="_CPPv431bk_ckmn_clear_ckest_intr_statusv"></a>

<a id="_CPPv331bk_ckmn_clear_ckest_intr_statusv"></a> <a id="_CPPv231bk_ckmn_clear_ckest_intr_statusv"></a> <a id="bk_ckmn_clear_ckest_intr_status__void"></a> <a id="group__bk__api__ckmn_1ga77ec01c75a86357cf0f94ab93f52b2a6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_clear\_ckest\_intr\_status(void)
:   clear ckest interrput status

    This API clock accuracy detection interrupt

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv432bk_ckmn_clear_cor26m_intr_statusv"></a>

<a id="_CPPv332bk_ckmn_clear_cor26m_intr_statusv"></a> <a id="_CPPv232bk_ckmn_clear_cor26m_intr_statusv"></a> <a id="bk_ckmn_clear_cor26m_intr_status__void"></a> <a id="group__bk__api__ckmn_1ga5b04856641b70422be6962194d76c2bd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_clear\_cor26m\_intr\_status(void)
:   clear cor26m interrput status

    This API clock accuracy detection interrupt

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv432bk_ckmn_clear_cor32k_intr_statusv"></a>

<a id="_CPPv332bk_ckmn_clear_cor32k_intr_statusv"></a> <a id="_CPPv232bk_ckmn_clear_cor32k_intr_statusv"></a> <a id="bk_ckmn_clear_cor32k_intr_status__void"></a> <a id="group__bk__api__ckmn_1ga9af9c10332a37576685761053d926466"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ckmn\_clear\_cor32k\_intr\_status(void)
:   clear cor32k interrput status

    This API clock accuracy detection interrupt

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv413bk_ckmn_startv"></a>

<a id="_CPPv313bk_ckmn_startv"></a> <a id="_CPPv213bk_ckmn_startv"></a> <a id="bk_ckmn_start__void"></a> <a id="group__bk__api__ckmn_1ga709ec535229d0accf52e3754f5c30e6e"></a> void bk\_ckmn\_start(void)
:   Start the clock monitor (init \+ set 26M/32K targets \+ enable autosw).

    Convenience wrapper used by the TF-M secure firmware. Implemented for BK7259 in the TF-M platform shim (beken/bk7259/sys\_drv\_int\_shim.c).

<a id="ckmn-api-typedefs"></a>

## CKMN API Typedefs

<a id="id1"></a>

### Header File

- [ckmn\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/ckmn_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_CKMN_DRIVER_NOT_INIT"></a>

<a id="group__bk__api__ckmn__defs_1gaaa381f5da12e9c3159cddbeaf8965717"></a> BK\_ERR\_CKMN\_DRIVER\_NOT\_INIT
:   CKMN driver not init

<a id="c.BK_ERR_CKMN_INT_TYPE"></a>

<a id="group__bk__api__ckmn__defs_1gae1b2a1490a60849710a7b9498887da46"></a> BK\_ERR\_CKMN\_INT\_TYPE
:   CKMN unknow int type

<a id="c.BK_ERR_CKMN_CKEST_BUSY"></a>

<a id="group__bk__api__ckmn__defs_1ga3dc181c2bfb8b278d608c13963275476"></a> BK\_ERR\_CKMN\_CKEST\_BUSY
:   CKMN skest is busy

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410ckmn_isr_t"></a>

<a id="_CPPv310ckmn_isr_t"></a> <a id="_CPPv210ckmn_isr_t"></a> <a id="ckmn_isr_t"></a> <a id="group__bk__api__ckmn__defs_1ga434cde774d2df3a11bf095eaa8c39b73"></a> typedef void (\*ckmn\_isr\_t)(void)
:   DMA interrupt service routine.

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv415ckmn_int_type_t"></a>

<a id="_CPPv315ckmn_int_type_t"></a> <a id="_CPPv215ckmn_int_type_t"></a> <a id="group__bk__api__ckmn__defs_1ga219e13175d3daae3ad0340608e08e966"></a> enum ckmn\_int\_type\_t
:   *Values:*

    <a id="_CPPv4N15ckmn_int_type_t14CKMN_INT_CKESTE"></a>

    <a id="_CPPv3N15ckmn_int_type_t14CKMN_INT_CKESTE"></a> <a id="_CPPv2N15ckmn_int_type_t14CKMN_INT_CKESTE"></a> <a id="group__bk__api__ckmn__defs_1gga219e13175d3daae3ad0340608e08e966a0f9aa5a443562e9638569834ab1b367e"></a> enumerator CKMN\_INT\_CKEST

    <a id="_CPPv4N15ckmn_int_type_t12CKMN_INT_26ME"></a>

    <a id="_CPPv3N15ckmn_int_type_t12CKMN_INT_26ME"></a> <a id="_CPPv2N15ckmn_int_type_t12CKMN_INT_26ME"></a> <a id="group__bk__api__ckmn__defs_1gga219e13175d3daae3ad0340608e08e966a2161f653fba5c383131f2caabfed0235"></a> enumerator CKMN\_INT\_26M

    <a id="_CPPv4N15ckmn_int_type_t12CKMN_INT_32KE"></a>

    <a id="_CPPv3N15ckmn_int_type_t12CKMN_INT_32KE"></a> <a id="_CPPv2N15ckmn_int_type_t12CKMN_INT_32KE"></a> <a id="group__bk__api__ckmn__defs_1gga219e13175d3daae3ad0340608e08e966a89be53c7ed0a398bded256038e26502c"></a> enumerator CKMN\_INT\_32K

    <a id="_CPPv4N15ckmn_int_type_t12CKMN_INT_MAXE"></a>

    <a id="_CPPv3N15ckmn_int_type_t12CKMN_INT_MAXE"></a> <a id="_CPPv2N15ckmn_int_type_t12CKMN_INT_MAXE"></a> <a id="group__bk__api__ckmn__defs_1gga219e13175d3daae3ad0340608e08e966a91a69526ed9a83ef3c482566e049399a"></a> enumerator CKMN\_INT\_MAX

<a id="id2"></a>

### Header File

- [hal\_ckmn\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_ckmn_types.h)

<a id="id3"></a>

### Enumerations

<a id="_CPPv410ckmn_acc_t"></a>

<a id="_CPPv310ckmn_acc_t"></a> <a id="_CPPv210ckmn_acc_t"></a> <a id="hal__ckmn__types_8h_1a0c49c1296c8bfa3dba62b62203347d9d"></a> enum ckmn\_acc\_t
:   *Values:*

    <a id="_CPPv4N10ckmn_acc_t16CKMN_TARGET_1PERE"></a>

    <a id="_CPPv3N10ckmn_acc_t16CKMN_TARGET_1PERE"></a> <a id="_CPPv2N10ckmn_acc_t16CKMN_TARGET_1PERE"></a> <a id="hal__ckmn__types_8h_1a0c49c1296c8bfa3dba62b62203347d9dab95ff7a3cd5ffdd48d535692c622eada"></a> enumerator CKMN\_TARGET\_1PER

    <a id="_CPPv4N10ckmn_acc_t16CKMN_TARGET_4PERE"></a>

    <a id="_CPPv3N10ckmn_acc_t16CKMN_TARGET_4PERE"></a> <a id="_CPPv2N10ckmn_acc_t16CKMN_TARGET_4PERE"></a> <a id="hal__ckmn__types_8h_1a0c49c1296c8bfa3dba62b62203347d9dac423b9ea0b29e6c05a726c1dd9bc742b"></a> enumerator CKMN\_TARGET\_4PER

    <a id="_CPPv4N10ckmn_acc_t17CKMN_TARGET_16PERE"></a>

    <a id="_CPPv3N10ckmn_acc_t17CKMN_TARGET_16PERE"></a> <a id="_CPPv2N10ckmn_acc_t17CKMN_TARGET_16PERE"></a> <a id="hal__ckmn__types_8h_1a0c49c1296c8bfa3dba62b62203347d9da4fd3342b85bb908efc95b2e58084a362"></a> enumerator CKMN\_TARGET\_16PER

    <a id="_CPPv4N10ckmn_acc_t17CKMN_TARGET_50PERE"></a>

    <a id="_CPPv3N10ckmn_acc_t17CKMN_TARGET_50PERE"></a> <a id="_CPPv2N10ckmn_acc_t17CKMN_TARGET_50PERE"></a> <a id="hal__ckmn__types_8h_1a0c49c1296c8bfa3dba62b62203347d9da34ca7779becf774333de3f6c8461ebcf"></a> enumerator CKMN\_TARGET\_50PER
