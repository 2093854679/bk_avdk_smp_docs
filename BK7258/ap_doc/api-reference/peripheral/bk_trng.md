---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_trng.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="trng"></a>

# TRNG

<a id="trng-api-status"></a>

## TRNG API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_trng_driver_init()`](#_CPPv419bk_trng_driver_initv "bk_trng_driver_init") | Y |
| [`bk_trng_driver_deinit()`](#_CPPv421bk_trng_driver_deinitv "bk_trng_driver_deinit") | Y |
| [`bk_trng_start()`](#_CPPv413bk_trng_startv "bk_trng_start") | Y |
| [`bk_trng_stop()`](#_CPPv412bk_trng_stopv "bk_trng_stop") | Y |
| [`bk_rand()`](#_CPPv47bk_randv "bk_rand") | Y |

<a id="trng-api-reference"></a>

## TRNG API Reference

<a id="header-file"></a>

### Header File

- [trng.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/trng.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419bk_trng_driver_initv"></a>

<a id="_CPPv319bk_trng_driver_initv"></a> <a id="_CPPv219bk_trng_driver_initv"></a> <a id="bk_trng_driver_init__void"></a> <a id="group__bk__api__trng_1gaec35d5d2ae8c08534f48a7a6ba636640"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_trng\_driver\_init(void)
:   Init the TRNG driver.

    This API init the resoure common:

    - Init TRNG driver control memory

    **Attention**
    :   1\. This API should be called before any other TRNG APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_trng_driver_deinitv"></a>

<a id="_CPPv321bk_trng_driver_deinitv"></a> <a id="_CPPv221bk_trng_driver_deinitv"></a> <a id="bk_trng_driver_deinit__void"></a> <a id="group__bk__api__trng_1ga019e52775178c9a20580393f42be1150"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_trng\_driver\_deinit(void)
:   Deinit the TRNG driver.

    This API free all resource related to TRNG and disable TRNG.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv413bk_trng_startv"></a>

<a id="_CPPv313bk_trng_startv"></a> <a id="_CPPv213bk_trng_startv"></a> <a id="bk_trng_start__void"></a> <a id="group__bk__api__trng_1gae7833bfd29ae12a4e0403089e321b2af"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_trng\_start(void)
:   Start the TRNG.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_TRNG\_DRIVER\_NOT\_INIT: TRNG driver not init
        - others: other errors.

<a id="_CPPv412bk_trng_stopv"></a>

<a id="_CPPv312bk_trng_stopv"></a> <a id="_CPPv212bk_trng_stopv"></a> <a id="bk_trng_stop__void"></a> <a id="group__bk__api__trng_1ga24f28f63639d6913490dcdf20e0fb0c3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_trng\_stop(void)
:   Stop the TRNG.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_TRNG\_DRIVER\_NOT\_INIT: TRNG driver not init
        - others: other errors.

<a id="_CPPv47bk_randv"></a>

<a id="_CPPv37bk_randv"></a> <a id="_CPPv27bk_randv"></a> <a id="bk_rand__void"></a> <a id="group__bk__api__trng_1gadcb29cae0f63ca3cec69db05eb19b098"></a> int bk\_rand(void)
:   Get the random number.

    返回
    :   random number between 0 and RAND\_MAX

<a id="_CPPv412bk_fill_randPv6size_t"></a>

<a id="_CPPv312bk_fill_randPv6size_t"></a> <a id="_CPPv212bk_fill_randPv6size_t"></a> <a id="bk_fill_rand__voidP.s"></a> <a id="group__bk__api__trng_1gaba92e60484185b4667bf79e09e02c4f4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_fill\_rand(void \*buff, size\_t len)
:   Get the random number to buff.

    参数
    :   - **buff** – the buffer to store the random number
        - **len** – the byte length of the buffer

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="trng-api-typedefs"></a>

## TRNG API Typedefs

<a id="id1"></a>

### Header File

- [trng\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/trng_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_TRNG_DRIVER_NOT_INIT"></a>

<a id="group__bk__api__trng__defs_1ga39b00c34a8ac0590338733c01d78a939"></a> BK\_ERR\_TRNG\_DRIVER\_NOT\_INIT
:   TRNG driver not init

<a id="id2"></a>

### Header File

- [hal\_trng\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_trng_types.h)

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv411trng_unit_t"></a>

<a id="_CPPv311trng_unit_t"></a> <a id="_CPPv211trng_unit_t"></a> <a id="trng_unit_t"></a> <a id="group__bk__api__trng__defs_1ga3ece26559b63b292898a945aa7c9ea7e"></a> typedef uint8\_t trng\_unit\_t
:   trng uint id
