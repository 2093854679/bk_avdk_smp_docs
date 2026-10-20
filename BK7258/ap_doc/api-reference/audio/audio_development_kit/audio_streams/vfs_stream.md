---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_streams/vfs_stream.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="vfs-stream"></a>

# VFS Stream

The VFS stream reads/writes audio data from/into VFS.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [vfs\_stream.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_streams/vfs_stream.h)

<a id="functions"></a>

### Functions

<a id="_CPPv415vfs_stream_initP16vfs_stream_cfg_t"></a>

<a id="_CPPv315vfs_stream_initP16vfs_stream_cfg_t"></a> <a id="_CPPv215vfs_stream_initP16vfs_stream_cfg_t"></a> <a id="vfs_stream_init__vfs_stream_cfg_tP"></a> <a id="vfs__stream_8h_1a75a7b14e9a1b80b3ff0360032b7b3bd4"></a> [audio\_element\_handle\_t](../audio_pipeline/audio_element.md#_CPPv422audio_element_handle_t "audio_element_handle_t") vfs\_stream\_init([vfs\_stream\_cfg\_t](#_CPPv416vfs_stream_cfg_t "vfs_stream_cfg_t") \*config)
:   Create a handle to an Audio Element to stream data from vfs file system to another Element or get data from other elements written to vfs file system, depending on the configuration the stream type, either AUDIO\_STREAM\_READER or AUDIO\_STREAM\_WRITER.

    参数
    :   **config** – **\[in\]** The configuration

    返回
    :   The Audio Element handle

        - Not NULL: success
        - NULL: failed

<a id="structures"></a>

### Structures

<a id="_CPPv416vfs_stream_cfg_t"></a>

<a id="_CPPv316vfs_stream_cfg_t"></a> <a id="_CPPv216vfs_stream_cfg_t"></a> <a id="vfs_stream_cfg_t"></a> <a id="structvfs__stream__cfg__t"></a> struct vfs\_stream\_cfg\_t
:   VFS Stream configurations, if any entry is zero then the configuration will be set to default values.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16vfs_stream_cfg_t4typeE"></a>

    <a id="_CPPv3N16vfs_stream_cfg_t4typeE"></a> <a id="_CPPv2N16vfs_stream_cfg_t4typeE"></a> <a id="vfs_stream_cfg_t::type__audio_stream_type_t"></a> <a id="structvfs__stream__cfg__t_1ada0edfbc5a81f1428f48576c47412442"></a> [audio\_stream\_type\_t](../audio_pipeline/audio_types.md#_CPPv419audio_stream_type_t "audio_stream_type_t") type
    :   Stream type

    <a id="_CPPv4N16vfs_stream_cfg_t6buf_szE"></a>

    <a id="_CPPv3N16vfs_stream_cfg_t6buf_szE"></a> <a id="_CPPv2N16vfs_stream_cfg_t6buf_szE"></a> <a id="vfs_stream_cfg_t::buf_sz__i"></a> <a id="structvfs__stream__cfg__t_1aff6fbdfb49b66a4435881221df979d1d"></a> int buf\_sz
    :   Audio Element Buffer size

    <a id="_CPPv4N16vfs_stream_cfg_t14out_block_sizeE"></a>

    <a id="_CPPv3N16vfs_stream_cfg_t14out_block_sizeE"></a> <a id="_CPPv2N16vfs_stream_cfg_t14out_block_sizeE"></a> <a id="vfs_stream_cfg_t::out_block_size__i"></a> <a id="structvfs__stream__cfg__t_1a707dd9392cf067221486119ebf09c0ec"></a> int out\_block\_size
    :   Size of output block

    <a id="_CPPv4N16vfs_stream_cfg_t13out_block_numE"></a>

    <a id="_CPPv3N16vfs_stream_cfg_t13out_block_numE"></a> <a id="_CPPv2N16vfs_stream_cfg_t13out_block_numE"></a> <a id="vfs_stream_cfg_t::out_block_num__i"></a> <a id="structvfs__stream__cfg__t_1a54d98a530e7611abdf51f4e9a7b5bc9c"></a> int out\_block\_num
    :   Number of output block

    <a id="_CPPv4N16vfs_stream_cfg_t10task_stackE"></a>

    <a id="_CPPv3N16vfs_stream_cfg_t10task_stackE"></a> <a id="_CPPv2N16vfs_stream_cfg_t10task_stackE"></a> <a id="vfs_stream_cfg_t::task_stack__i"></a> <a id="structvfs__stream__cfg__t_1acdd97d1f827e79fde563e25acc38f783"></a> int task\_stack
    :   Task stack size

    <a id="_CPPv4N16vfs_stream_cfg_t9task_coreE"></a>

    <a id="_CPPv3N16vfs_stream_cfg_t9task_coreE"></a> <a id="_CPPv2N16vfs_stream_cfg_t9task_coreE"></a> <a id="vfs_stream_cfg_t::task_core__i"></a> <a id="structvfs__stream__cfg__t_1a501f6a1c27a283a3b53ffc0a77dcb54b"></a> int task\_core
    :   Task running in core (0 or 1\)

    <a id="_CPPv4N16vfs_stream_cfg_t9task_prioE"></a>

    <a id="_CPPv3N16vfs_stream_cfg_t9task_prioE"></a> <a id="_CPPv2N16vfs_stream_cfg_t9task_prioE"></a> <a id="vfs_stream_cfg_t::task_prio__i"></a> <a id="structvfs__stream__cfg__t_1abec8bbb3c1bd58e1340820e506ceb8c5"></a> int task\_prio
    :   Task priority (based on freeRTOS priority)

<a id="macros"></a>

### Macros

<a id="c.VFS_STREAM_BUF_SIZE"></a>

<a id="vfs__stream_8h_1a7cb919103f108b1121d16dcd6112a2f3"></a> VFS\_STREAM\_BUF\_SIZE

<a id="c.VFS_STREAM_TASK_STACK"></a>

<a id="vfs__stream_8h_1aed8a1c4528acf2b7e3f2b19da6030f7d"></a> VFS\_STREAM\_TASK\_STACK

<a id="c.VFS_STREAM_TASK_CORE"></a>

<a id="vfs__stream_8h_1a80b9a7f80a74212d7975999f4b558d7a"></a> VFS\_STREAM\_TASK\_CORE

<a id="c.VFS_STREAM_TASK_PRIO"></a>

<a id="vfs__stream_8h_1a52f225fd48df8f09b0b7e711354cd5d6"></a> VFS\_STREAM\_TASK\_PRIO

<a id="c.VFS_STREAM_OUT_BLOCK_SIZE"></a>

<a id="vfs__stream_8h_1a4109e5641e5b0b7741854f59770265f5"></a> VFS\_STREAM\_OUT\_BLOCK\_SIZE

<a id="c.VFS_STREAM_OUT_BLOCK_NUM"></a>

<a id="vfs__stream_8h_1aeceb0c328b8d5a0270c8a2d85be0299e"></a> VFS\_STREAM\_OUT\_BLOCK\_NUM

<a id="c.DEFAULT_VFS_STREAM_CONFIG"></a>

<a id="vfs__stream_8h_1a4b5ba76f1c3aafb0c887bcdf01b93d75"></a> DEFAULT\_VFS\_STREAM\_CONFIG()
