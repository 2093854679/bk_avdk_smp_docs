# VFS Util


The VFS util provides a method to dump data processed by the component through VFS (sdcard, flash…).


## API Reference


### Header File


- [bk_audio/audio_utils/vfs_util.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_utils/vfs_util.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_audio/audio_utils/vfs_util.h")


### Functions

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") vfs_util_create([vfs_util_handle_t](#_CPPv417vfs_util_handle_t "vfs_util_handle_t") vfs_util, char *name)
:   Create a vfs util.

    参数
    :   - **vfs_util** – The vfs util handle

        - **name** – **[in]** The vfs name, such as “/sd0/mic.pcm”

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") vfs_util_destroy([vfs_util_handle_t](#_CPPv417vfs_util_handle_t "vfs_util_handle_t") vfs_util)
:   Destroy a vfs util.

    参数
    :   **vfs_util** – The vfs util handle, created by vfs_util_create

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed

[bk_err_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") vfs_util_tx_data([vfs_util_handle_t](#_CPPv417vfs_util_handle_t "vfs_util_handle_t") vfs_util, void *data_buf, uint32_t len)
:   Transmit data via vfs util.

    参数
    :   - **vfs_util** – The vfs util handle, created by vfs_util_create

        - **data_buf** – **[in]** The data buffer

        - **len** – **[in]** The data length

    返回
    :   The result


        - BK_OK: success

        - BK_ERR: failed


### Structures

struct vfs_util


### Type Definitions

typedef struct [vfs_util](#_CPPv48vfs_util "vfs_util") *vfs_util_handle_t
