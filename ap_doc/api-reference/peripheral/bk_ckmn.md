# CKMN


BK7259 AP 侧 CKMN（Clock Monitor）API（`include/driver/ckmn.h`）。


## CKMN API Reference


### Header File


- [ckmn.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/ckmn.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/ckmn.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_driver_init(void)
:   Init the CKMN driver.

    This API init the resoure common:


    - Init CKMN driver control memory


    **Attention**
    :   1. This API should be called before any other CKMN APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_driver_deinit(void)
:   Deinit the CKMN driver.

    This API free all resource related to CKMN and disable CKMN.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_register_isr([ckmn_int_type_t](#_CPPv415ckmn_int_type_t "ckmn_int_type_t") int_type, [ckmn_isr_t](#_CPPv410ckmn_isr_t "ckmn_isr_t") int_isr)
:   Register the interrupt service routine for CKMN.

    This API regist ckmn isr callback function.

    参数
    :   - **int_type** – register interrupt type

        - **int_isr** – ckmn callback

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_unregister_isr([ckmn_int_type_t](#_CPPv415ckmn_int_type_t "ckmn_int_type_t") int_type)
:   Unregister the interrupt service routine for CKMN.

    This API regist ckmn isr callback function.

    参数
    :   **int_type** – register interrupt type

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_soft_reset(void)
:   ckmn soft reset

    This API reset ckmn module

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_set_rc32k_count(uint32_t count)
:   Set the number of counts for RC32K accuracy statistics.

    This API 26m digital clock measurement 32k analog clock.

    参数
    :   **count** – number of clock cycles

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_get_rc32k_count(void)
:   Get the number of counts for RC32K accuracy statistics.

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - count number of clock cycles

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_ckest_enable(void)
:   enable RC32K accuracy statistics

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_ckest_disable(void)
:   disable RC32K accuracy statistics

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_get_rc26m_count(void)
:   get ther number of mappings of RC32K accuracy statistics in the 26m domain

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - ther number of mappings

double bk_ckmn_driver_get_rc32k_freq(void)
:   Get calibrated 32k clock frequency.

    This API 26m digital clock measurement 32k analog clock.

    返回
    :   - alibrated 32k clock frequency value.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_driver_get_rc32k_ppm(void)
:   Get calibrated 32k clock ppm.

    This API tells the current clock ppm of rc32k.

    返回
    :   - alibrated 32k clock ppm value.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_driver_rc32k_prog(uint32_t count)
:   Perform 32k frequency calibration.

    This API 26m digital clock measurement 32k analog clock.

    参数
    :   **count** – number of clock cycles

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_set_26m_target([ckmn_acc_t](#_CPPv410ckmn_acc_t "ckmn_acc_t") target)
:   Set 26m clock accuracy related targets.

    This API auto clock switching.

    参数
    :   **target** – accuracy percentage

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_enable_autosw_26m(void)
:   enable 26m clock auto switching

    This API auto clock switching..

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_disable_autosw_26m(void)
:   disable 26m clock auto switching

    This API auto clock switching..

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_enable_corr_26m(void)
:   enable 26m clock accuracy detection and enable interrupt

    This API auto clock switching..

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_disable_corr_26m(void)
:   disable 26m clock accuracy detection and disable interrupt

    This API auto clock switching..

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_set_32k_target([ckmn_acc_t](#_CPPv410ckmn_acc_t "ckmn_acc_t") target)
:   Set 32k clock accuracy related targets.

    This API auto clock switching.

    参数
    :   **target** – accuracy percentage

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_enable_autosw_32k(void)
:   enable 32k clock auto switching

    This API auto clock switching..

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_disable_autosw_32k(void)
:   disable 32k clock auto switching

    This API auto clock switching..

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_enable_corr_32k(void)
:   enable 32k clock accuracy detection and enable interrupt

    This API clock accuracy detection..

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_disable_corr_32k(void)
:   disable 32k clock accuracy detection and disable interrupt

    This API clock accuracy detection..

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_cor26m_intr_enable(void)
:   enable 26m clock auto switching interrupt

    This API clock accuracy detection interrupt

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_cor26m_intr_disable(void)
:   disable 26m clock auto switching interrupt

    This API clock accuracy detection interrupt

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_cor32k_intr_enable(void)
:   enable 32k clock auto switching interrupt

    This API clock accuracy detection interrupt

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_cor32k_intr_disable(void)
:   disable 32k clock auto switching interrupt

    This API clock accuracy detection interrupt

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_get_intr_status(void)
:   Get all interrput status.

    This API clock accuracy detection interrupt

    返回
    :   - all interrupt value

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_get_ckest_intr_status(void)
:   Get chest interrput status.

    This API clock accuracy detection interrupt

    返回
    :   - chest interrupt value

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_get_cor26m_intr_status(void)
:   Get cor26m interrput status.

    This API clock accuracy detection interrupt

    返回
    :   - cor26m interrupt value

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_get_cor32k_intr_status(void)
:   Get 32k interrput status.

    This API clock accuracy detection interrupt

    返回
    :   - 32k interrupt value

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_clear_ckest_intr_status(void)
:   clear ckest interrput status

    This API clock accuracy detection interrupt

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_clear_cor26m_intr_status(void)
:   clear cor26m interrput status

    This API clock accuracy detection interrupt

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ckmn_clear_cor32k_intr_status(void)
:   clear cor32k interrput status

    This API clock accuracy detection interrupt

    返回
    :   - BK_OK: succeed

        - others: other errors.


## CKMN API Typedefs


### Header File


- [ckmn_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/ckmn_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/ckmn_types.h")


### Macros

BK_ERR_CKMN_DRIVER_NOT_INIT
:   CKMN driver not init

BK_ERR_CKMN_INT_TYPE
:   CKMN unknow int type

BK_ERR_CKMN_CKEST_BUSY
:   CKMN skest is busy


### Type Definitions

typedef void (*ckmn_isr_t)(void)
:   DMA interrupt service routine.


### Enumerations

enum ckmn_int_type_t
:   *Values:*

    enumerator CKMN_INT_CKEST

    enumerator CKMN_INT_26M

    enumerator CKMN_INT_32K

    enumerator CKMN_INT_MAX


### Header File


- [hal/hal_ckmn_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_ckmn_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_ckmn_types.h")


### Enumerations

enum ckmn_acc_t
:   *Values:*

    enumerator CKMN_TARGET_1PER

    enumerator CKMN_TARGET_4PER

    enumerator CKMN_TARGET_16PER

    enumerator CKMN_TARGET_50PER
