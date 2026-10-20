---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/audio/audio_development_kit/audio_utils/vfs_util.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="vfs-util"></a>

# VFS Util

The VFS util provides a method to dump data processed by the component through VFS (sdcard, flash…).

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [vfs\_util.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bk_audio/audio_utils/vfs_util.h)

<a id="functions"></a>

### Functions

<a id="_CPPv415vfs_util_create17vfs_util_handle_tPc"></a>

<a id="_CPPv315vfs_util_create17vfs_util_handle_tPc"></a> <a id="_CPPv215vfs_util_create17vfs_util_handle_tPc"></a> <a id="vfs_util_create__vfs_util_handle_t.cP"></a> <a id="vfs__util_8h_1ad56c781644d2136865cd5a5829968cb0"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") vfs\_util\_create([vfs\_util\_handle\_t](#_CPPv417vfs_util_handle_t "vfs_util_handle_t") vfs\_util, char \*name)
:   Create a vfs util.

    参数
    :   - **vfs\_util** – The vfs util handle
        - **name** – **\[in\]** The vfs name, such as “/sd0/mic.pcm”

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="_CPPv416vfs_util_destroy17vfs_util_handle_t"></a>

<a id="_CPPv316vfs_util_destroy17vfs_util_handle_t"></a> <a id="_CPPv216vfs_util_destroy17vfs_util_handle_t"></a> <a id="vfs_util_destroy__vfs_util_handle_t"></a> <a id="vfs__util_8h_1a40b68cb23080e46eff5f403acac00145"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") vfs\_util\_destroy([vfs\_util\_handle\_t](#_CPPv417vfs_util_handle_t "vfs_util_handle_t") vfs\_util)
:   Destroy a vfs util.

    参数
    :   **vfs\_util** – The vfs util handle, created by vfs\_util\_create

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="_CPPv416vfs_util_tx_data17vfs_util_handle_tPv8uint32_t"></a>

<a id="_CPPv316vfs_util_tx_data17vfs_util_handle_tPv8uint32_t"></a> <a id="_CPPv216vfs_util_tx_data17vfs_util_handle_tPv8uint32_t"></a> <a id="vfs_util_tx_data__vfs_util_handle_t.voidP.uint32_t"></a> <a id="vfs__util_8h_1a2ae4ff9fb67bd6ae2fb8e4b90b4adaef"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") vfs\_util\_tx\_data([vfs\_util\_handle\_t](#_CPPv417vfs_util_handle_t "vfs_util_handle_t") vfs\_util, void \*data\_buf, uint32\_t len)
:   Transmit data via vfs util.

    参数
    :   - **vfs\_util** – The vfs util handle, created by vfs\_util\_create
        - **data\_buf** – **\[in\]** The data buffer
        - **len** – **\[in\]** The data length

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="structures"></a>

### Structures

<a id="_CPPv48vfs_util"></a>

<a id="_CPPv38vfs_util"></a> <a id="_CPPv28vfs_util"></a> <a id="vfs_util"></a> <a id="structvfs__util"></a> struct vfs\_util

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv417vfs_util_handle_t"></a>

<a id="_CPPv317vfs_util_handle_t"></a> <a id="_CPPv217vfs_util_handle_t"></a> <a id="vfs_util_handle_t"></a> <a id="vfs__util_8h_1a657c710c6423f8fed4072a3affbf1492"></a> typedef struct [vfs\_util](#_CPPv48vfs_util "vfs_util") \*vfs\_util\_handle\_t
