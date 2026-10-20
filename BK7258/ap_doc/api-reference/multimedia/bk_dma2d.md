---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_dma2d.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="dma2d"></a>

# dma2d

<a id="id1"></a>

## 概述

DMA2D模块提供统一的DMA2D接口

参考工程：

- 有关dma2d的详细信息，请参阅：

  - [dma2d开发指南](../../developer-guide/display/dma2d.md)
- 有关dma2d的示例工程，请参阅：

  - [dma2d 示例项目](../../examples/projects/dma2d_example.md)

<a id="dma2d-api-reference"></a>

## DMA2D API Reference

<a id="header-file"></a>

### Header File

- [bk\_dma2d.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_dma2d.h)

<a id="functions"></a>

### Functions

<a id="_CPPv413bk_dma2d_open22bk_dma2d_ctlr_handle_t"></a>

<a id="_CPPv313bk_dma2d_open22bk_dma2d_ctlr_handle_t"></a> <a id="_CPPv213bk_dma2d_open22bk_dma2d_ctlr_handle_t"></a> <a id="bk_dma2d_open__bk_dma2d_ctlr_handle_t"></a> <a id="bk__dma2d_8h_1ad913e3acbee3d7c47268e4aaa37b4fb1"></a> avdk\_err\_t bk\_dma2d\_open([bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") handle)
:   Open a DMA2D controller handle.

    参数
    :   **handle** – Handle to open

    返回
    :   AVDK\_ERR\_OK if successful, otherwise error code

<a id="_CPPv414bk_dma2d_close22bk_dma2d_ctlr_handle_t"></a>

<a id="_CPPv314bk_dma2d_close22bk_dma2d_ctlr_handle_t"></a> <a id="_CPPv214bk_dma2d_close22bk_dma2d_ctlr_handle_t"></a> <a id="bk_dma2d_close__bk_dma2d_ctlr_handle_t"></a> <a id="bk__dma2d_8h_1a33ae64ae5134610f9c3322b8092f4cb0"></a> avdk\_err\_t bk\_dma2d\_close([bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") handle)
:   Close a DMA2D controller handle.

    参数
    :   **handle** – Handle to close

    返回
    :   AVDK\_ERR\_OK if successful, otherwise error code

<a id="_CPPv415bk_dma2d_delete22bk_dma2d_ctlr_handle_t"></a>

<a id="_CPPv315bk_dma2d_delete22bk_dma2d_ctlr_handle_t"></a> <a id="_CPPv215bk_dma2d_delete22bk_dma2d_ctlr_handle_t"></a> <a id="bk_dma2d_delete__bk_dma2d_ctlr_handle_t"></a> <a id="bk__dma2d_8h_1a0767064a01b4a9759858e946eb348afe"></a> avdk\_err\_t bk\_dma2d\_delete([bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") handle)
:   Delete a DMA2D controller handle.

    参数
    :   **handle** – Handle to delete

    返回
    :   AVDK\_ERR\_OK if successful, otherwise error code

<a id="_CPPv413bk_dma2d_fill22bk_dma2d_ctlr_handle_tP19dma2d_fill_config_t"></a>

<a id="_CPPv313bk_dma2d_fill22bk_dma2d_ctlr_handle_tP19dma2d_fill_config_t"></a> <a id="_CPPv213bk_dma2d_fill22bk_dma2d_ctlr_handle_tP19dma2d_fill_config_t"></a> <a id="bk_dma2d_fill__bk_dma2d_ctlr_handle_t.dma2d_fill_config_tP"></a> <a id="bk__dma2d_8h_1a922864386fbdb1680d394a649937a6bf"></a> avdk\_err\_t bk\_dma2d\_fill([bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") handle, [dma2d\_fill\_config\_t](#_CPPv419dma2d_fill_config_t "dma2d_fill_config_t") \*config)
:   Perform fill operation using DMA2D.

    参数
    :   - **handle** – DMA2D controller handle
        - **config** – Fill configuration

    返回
    :   AVDK\_ERR\_OK if successful, otherwise error code

<a id="_CPPv415bk_dma2d_memcpy22bk_dma2d_ctlr_handle_tP21dma2d_memcpy_config_t"></a>

<a id="_CPPv315bk_dma2d_memcpy22bk_dma2d_ctlr_handle_tP21dma2d_memcpy_config_t"></a> <a id="_CPPv215bk_dma2d_memcpy22bk_dma2d_ctlr_handle_tP21dma2d_memcpy_config_t"></a> <a id="bk_dma2d_memcpy__bk_dma2d_ctlr_handle_t.dma2d_memcpy_config_tP"></a> <a id="bk__dma2d_8h_1a6fbaa312bde6a7aed96e9d1bb18d557e"></a> avdk\_err\_t bk\_dma2d\_memcpy([bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") handle, [dma2d\_memcpy\_config\_t](#_CPPv421dma2d_memcpy_config_t "dma2d_memcpy_config_t") \*config)
:   Perform memory copy operation using DMA2D.

    参数
    :   - **handle** – DMA2D controller handle
        - **config** – Memory copy configuration

    返回
    :   AVDK\_ERR\_OK if successful, otherwise error code

<a id="_CPPv425bk_dma2d_pixel_conversion22bk_dma2d_ctlr_handle_tP25dma2d_pfc_memcpy_config_t"></a>

<a id="_CPPv325bk_dma2d_pixel_conversion22bk_dma2d_ctlr_handle_tP25dma2d_pfc_memcpy_config_t"></a> <a id="_CPPv225bk_dma2d_pixel_conversion22bk_dma2d_ctlr_handle_tP25dma2d_pfc_memcpy_config_t"></a> <a id="bk_dma2d_pixel_conversion__bk_dma2d_ctlr_handle_t.dma2d_pfc_memcpy_config_tP"></a> <a id="bk__dma2d_8h_1a001fc35f28726038a2993d69b86f5095"></a> avdk\_err\_t bk\_dma2d\_pixel\_conversion([bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") handle, [dma2d\_pfc\_memcpy\_config\_t](#_CPPv425dma2d_pfc_memcpy_config_t "dma2d_pfc_memcpy_config_t") \*config)
:   Perform pixel format conversion operation using DMA2D.

    参数
    :   - **handle** – DMA2D controller handle
        - **config** – Pixel conversion configuration

    返回
    :   AVDK\_ERR\_OK if successful, otherwise error code

<a id="_CPPv414bk_dma2d_blend22bk_dma2d_ctlr_handle_tP20dma2d_blend_config_t"></a>

<a id="_CPPv314bk_dma2d_blend22bk_dma2d_ctlr_handle_tP20dma2d_blend_config_t"></a> <a id="_CPPv214bk_dma2d_blend22bk_dma2d_ctlr_handle_tP20dma2d_blend_config_t"></a> <a id="bk_dma2d_blend__bk_dma2d_ctlr_handle_t.dma2d_blend_config_tP"></a> <a id="bk__dma2d_8h_1ac705af7d4395752e1c19b8e4ff76908f"></a> avdk\_err\_t bk\_dma2d\_blend([bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") handle, [dma2d\_blend\_config\_t](#_CPPv420dma2d_blend_config_t "dma2d_blend_config_t") \*config)
:   Perform blend operation using DMA2D.

    参数
    :   - **handle** – DMA2D controller handle
        - **config** – Blend configuration

    返回
    :   AVDK\_ERR\_OK if successful, otherwise error code

<a id="_CPPv414bk_dma2d_ioctl22bk_dma2d_ctlr_handle_t8uint32_t8uint32_t8uint32_t8uint32_t"></a>

<a id="_CPPv314bk_dma2d_ioctl22bk_dma2d_ctlr_handle_t8uint32_t8uint32_t8uint32_t8uint32_t"></a> <a id="_CPPv214bk_dma2d_ioctl22bk_dma2d_ctlr_handle_t8uint32_t8uint32_t8uint32_t8uint32_t"></a> <a id="bk_dma2d_ioctl__bk_dma2d_ctlr_handle_t.uint32_t.uint32_t.uint32_t.uint32_t"></a> <a id="bk__dma2d_8h_1aac2043c283d31c87ad4d0dea097b1ddd"></a> avdk\_err\_t bk\_dma2d\_ioctl([bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") handle, uint32\_t ioctl\_cmd, uint32\_t param1, uint32\_t param2, uint32\_t param3)
:   Control IO operations of DMA2D controller.

    参数
    :   - **handle** – DMA2D controller handle
        - **ioctl\_cmd** – IO control command
        - **param1** – Command parameter 1
        - **param2** – Command parameter 2
        - **param3** – Command parameter 3

    返回
    :   AVDK\_ERR\_OK if successful, otherwise error code

<a id="_CPPv412bk_dma2d_newP22bk_dma2d_ctlr_handle_t"></a>

<a id="_CPPv312bk_dma2d_newP22bk_dma2d_ctlr_handle_t"></a> <a id="_CPPv212bk_dma2d_newP22bk_dma2d_ctlr_handle_t"></a> <a id="bk_dma2d_new__bk_dma2d_ctlr_handle_tP"></a> <a id="bk__dma2d_8h_1a280465eac8163e68dac56c191f8600c1"></a> avdk\_err\_t bk\_dma2d\_new([bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") \*handle)
:   Create a DMA2D controller handle.

    参数
    :   **handle** – Handle to create

    返回
    :   AVDK\_ERR\_OK if successful, otherwise error code

<a id="_CPPv419bk_dma2d_handle_getv"></a>

<a id="_CPPv319bk_dma2d_handle_getv"></a> <a id="_CPPv219bk_dma2d_handle_getv"></a> <a id="bk_dma2d_handle_get__void"></a> <a id="bk__dma2d_8h_1abd2b2c2173c34c2782a0e26650212274"></a> [bk\_dma2d\_ctlr\_handle\_t](#_CPPv422bk_dma2d_ctlr_handle_t "bk_dma2d_ctlr_handle_t") bk\_dma2d\_handle\_get(void)
:   get dma2d handle

    返回
    :   bk\_dma2d\_ctlr\_handle\_t handle

<a id="dma2d-api-typedefs"></a>

## DMA2D API Typedefs

<a id="id4"></a>

### Header File

- [bk\_dma2d\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_dma2d_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv419dma2d_fill_config_t"></a>

<a id="_CPPv319dma2d_fill_config_t"></a> <a id="_CPPv219dma2d_fill_config_t"></a> <a id="dma2d_fill_config_t"></a> <a id="structdma2d__fill__config__t"></a> struct dma2d\_fill\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19dma2d_fill_config_t4fillE"></a>

    <a id="_CPPv3N19dma2d_fill_config_t4fillE"></a> <a id="_CPPv2N19dma2d_fill_config_t4fillE"></a> <a id="dma2d_fill_config_t::fill__dma2d_fill_t"></a> <a id="structdma2d__fill__config__t_1a83d3f299a065a3d143d464bf6b008727"></a> [dma2d\_fill\_t](#_CPPv412dma2d_fill_t "dma2d_fill_t") fill
    :   dma2d fill config

    <a id="_CPPv4N19dma2d_fill_config_t20transfer_complete_cbE"></a>

    <a id="_CPPv3N19dma2d_fill_config_t20transfer_complete_cbE"></a> <a id="_CPPv2N19dma2d_fill_config_t20transfer_complete_cbE"></a> <a id="structdma2d__fill__config__t_1ab09fac2ab2dc5acbf10352628766f2e5"></a> void (\*transfer\_complete\_cb)([dma2d\_trans\_status\_t](#_CPPv420dma2d_trans_status_t "dma2d_trans_status_t") status, void \*user\_data)
    :   dma2d transfer complete callback

    <a id="_CPPv4N19dma2d_fill_config_t7is_syncE"></a>

    <a id="_CPPv3N19dma2d_fill_config_t7is_syncE"></a> <a id="_CPPv2N19dma2d_fill_config_t7is_syncE"></a> <a id="dma2d_fill_config_t::is_sync__b"></a> <a id="structdma2d__fill__config__t_1aecb29cd6fc2aae44c573defebe575dd2"></a> bool is\_sync
    :   true: dma2d config valid immediately or wait for dma2d execute finish if current in use, false: dma2d config valid after dma2d execute finish if dma2d current is in use

<a id="_CPPv421dma2d_memcpy_config_t"></a>

<a id="_CPPv321dma2d_memcpy_config_t"></a> <a id="_CPPv221dma2d_memcpy_config_t"></a> <a id="dma2d_memcpy_config_t"></a> <a id="structdma2d__memcpy__config__t"></a> struct dma2d\_memcpy\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21dma2d_memcpy_config_t6memcpyE"></a>

    <a id="_CPPv3N21dma2d_memcpy_config_t6memcpyE"></a> <a id="_CPPv2N21dma2d_memcpy_config_t6memcpyE"></a> <a id="dma2d_memcpy_config_t::memcpy__dma2d_memcpy_pfc_t"></a> <a id="structdma2d__memcpy__config__t_1af0c9513c55c39eefc7bc1b4baf4215da"></a> [dma2d\_memcpy\_pfc\_t](#_CPPv418dma2d_memcpy_pfc_t "dma2d_memcpy_pfc_t") memcpy
    :   dma2d memcpy config

    <a id="_CPPv4N21dma2d_memcpy_config_t20transfer_complete_cbE"></a>

    <a id="_CPPv3N21dma2d_memcpy_config_t20transfer_complete_cbE"></a> <a id="_CPPv2N21dma2d_memcpy_config_t20transfer_complete_cbE"></a> <a id="structdma2d__memcpy__config__t_1a342dffb3f875fe3e37b5980511c8c228"></a> void (\*transfer\_complete\_cb)([dma2d\_trans\_status\_t](#_CPPv420dma2d_trans_status_t "dma2d_trans_status_t") status, void \*user\_data)
    :   dma2d transfer complete callback

    <a id="_CPPv4N21dma2d_memcpy_config_t7is_syncE"></a>

    <a id="_CPPv3N21dma2d_memcpy_config_t7is_syncE"></a> <a id="_CPPv2N21dma2d_memcpy_config_t7is_syncE"></a> <a id="dma2d_memcpy_config_t::is_sync__b"></a> <a id="structdma2d__memcpy__config__t_1ab3c67a43bc7cdcee538ef74eaf8e70b4"></a> bool is\_sync
    :   true: dma2d config valid immediately or wait for dma2d execute finish if current in use, false: dma2d config valid after dma2d execute finish if dma2d current is in use

<a id="_CPPv425dma2d_pfc_memcpy_config_t"></a>

<a id="_CPPv325dma2d_pfc_memcpy_config_t"></a> <a id="_CPPv225dma2d_pfc_memcpy_config_t"></a> <a id="dma2d_pfc_memcpy_config_t"></a> <a id="structdma2d__pfc__memcpy__config__t"></a> struct dma2d\_pfc\_memcpy\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N25dma2d_pfc_memcpy_config_t3pfcE"></a>

    <a id="_CPPv3N25dma2d_pfc_memcpy_config_t3pfcE"></a> <a id="_CPPv2N25dma2d_pfc_memcpy_config_t3pfcE"></a> <a id="dma2d_pfc_memcpy_config_t::pfc__dma2d_memcpy_pfc_t"></a> <a id="structdma2d__pfc__memcpy__config__t_1a56b57b7c60ef40490a68a089b6446150"></a> [dma2d\_memcpy\_pfc\_t](#_CPPv418dma2d_memcpy_pfc_t "dma2d_memcpy_pfc_t") pfc
    :   dma2d pfc memcpy config

    <a id="_CPPv4N25dma2d_pfc_memcpy_config_t20transfer_complete_cbE"></a>

    <a id="_CPPv3N25dma2d_pfc_memcpy_config_t20transfer_complete_cbE"></a> <a id="_CPPv2N25dma2d_pfc_memcpy_config_t20transfer_complete_cbE"></a> <a id="structdma2d__pfc__memcpy__config__t_1abee83b510d34f2546a504b6ac8e4a1b5"></a> void (\*transfer\_complete\_cb)([dma2d\_trans\_status\_t](#_CPPv420dma2d_trans_status_t "dma2d_trans_status_t") status, void \*user\_data)
    :   dma2d transfer complete callback

    <a id="_CPPv4N25dma2d_pfc_memcpy_config_t7is_syncE"></a>

    <a id="_CPPv3N25dma2d_pfc_memcpy_config_t7is_syncE"></a> <a id="_CPPv2N25dma2d_pfc_memcpy_config_t7is_syncE"></a> <a id="dma2d_pfc_memcpy_config_t::is_sync__b"></a> <a id="structdma2d__pfc__memcpy__config__t_1ac2b4bd4335e4400b8f9d4205278086fb"></a> bool is\_sync
    :   true: dma2d config valid immediately or wait for dma2d execute finish if current in use, false: dma2d config valid after dma2d execute finish if dma2d current is in use

<a id="_CPPv420dma2d_blend_config_t"></a>

<a id="_CPPv320dma2d_blend_config_t"></a> <a id="_CPPv220dma2d_blend_config_t"></a> <a id="dma2d_blend_config_t"></a> <a id="structdma2d__blend__config__t"></a> struct dma2d\_blend\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20dma2d_blend_config_t5blendE"></a>

    <a id="_CPPv3N20dma2d_blend_config_t5blendE"></a> <a id="_CPPv2N20dma2d_blend_config_t5blendE"></a> <a id="dma2d_blend_config_t::blend__dma2d_offset_blend_t"></a> <a id="structdma2d__blend__config__t_1ac894725ff182c54653f25536c97b4589"></a> [dma2d\_offset\_blend\_t](#_CPPv420dma2d_offset_blend_t "dma2d_offset_blend_t") blend
    :   dma2d blend config

    <a id="_CPPv4N20dma2d_blend_config_t20transfer_complete_cbE"></a>

    <a id="_CPPv3N20dma2d_blend_config_t20transfer_complete_cbE"></a> <a id="_CPPv2N20dma2d_blend_config_t20transfer_complete_cbE"></a> <a id="structdma2d__blend__config__t_1a5142a59192484a3ae90ddcd8d97a39b0"></a> void (\*transfer\_complete\_cb)([dma2d\_trans\_status\_t](#_CPPv420dma2d_trans_status_t "dma2d_trans_status_t") status, void \*user\_data)
    :   dma2d transfer complete callback

    <a id="_CPPv4N20dma2d_blend_config_t7is_syncE"></a>

    <a id="_CPPv3N20dma2d_blend_config_t7is_syncE"></a> <a id="_CPPv2N20dma2d_blend_config_t7is_syncE"></a> <a id="dma2d_blend_config_t::is_sync__b"></a> <a id="structdma2d__blend__config__t_1ade86dec6c1360be33f31e07481bf7c7a"></a> bool is\_sync
    :   true: dma2d config valid immediately or wait for dma2d execute finish if current in use, false: dma2d config valid after dma2d execute finish if dma2d current is in use

<a id="_CPPv413bk_dma2d_ctlr"></a>

<a id="_CPPv313bk_dma2d_ctlr"></a> <a id="_CPPv213bk_dma2d_ctlr"></a> <a id="bk_dma2d_ctlr"></a> <a id="structbk__dma2d__ctlr"></a> struct bk\_dma2d\_ctlr

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv422bk_dma2d_ctlr_handle_t"></a>

<a id="_CPPv322bk_dma2d_ctlr_handle_t"></a> <a id="_CPPv222bk_dma2d_ctlr_handle_t"></a> <a id="bk_dma2d_ctlr_handle_t"></a> <a id="bk__dma2d__types_8h_1ac02119f9d8d4be30a619a8e9da3d0e3d"></a> typedef struct [bk\_dma2d\_ctlr](#_CPPv413bk_dma2d_ctlr "bk_dma2d_ctlr") \*bk\_dma2d\_ctlr\_handle\_t

<a id="_CPPv415bk_dma2d_ctlr_t"></a>

<a id="_CPPv315bk_dma2d_ctlr_t"></a> <a id="_CPPv215bk_dma2d_ctlr_t"></a> <a id="bk_dma2d_ctlr_t"></a> <a id="bk__dma2d__types_8h_1a4528fefc0edded952925e333d596e9e5"></a> typedef struct [bk\_dma2d\_ctlr](#_CPPv413bk_dma2d_ctlr "bk_dma2d_ctlr") bk\_dma2d\_ctlr\_t

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv420dma2d_trans_status_t"></a>

<a id="_CPPv320dma2d_trans_status_t"></a> <a id="_CPPv220dma2d_trans_status_t"></a> <a id="bk__dma2d__types_8h_1aacf2c370826d7ec8e9265c0b49cc2c04"></a> enum dma2d\_trans\_status\_t
:   *Values:*

    <a id="_CPPv4N20dma2d_trans_status_t23DMA2D_TRANSFER_COMPLETEE"></a>

    <a id="_CPPv3N20dma2d_trans_status_t23DMA2D_TRANSFER_COMPLETEE"></a> <a id="_CPPv2N20dma2d_trans_status_t23DMA2D_TRANSFER_COMPLETEE"></a> <a id="bk__dma2d__types_8h_1aacf2c370826d7ec8e9265c0b49cc2c04a3e5e40309359e6d137b3b881849ee22b"></a> enumerator DMA2D\_TRANSFER\_COMPLETE

    <a id="_CPPv4N20dma2d_trans_status_t20DMA2D_TRANSFER_ERRORE"></a>

    <a id="_CPPv3N20dma2d_trans_status_t20DMA2D_TRANSFER_ERRORE"></a> <a id="_CPPv2N20dma2d_trans_status_t20DMA2D_TRANSFER_ERRORE"></a> <a id="bk__dma2d__types_8h_1aacf2c370826d7ec8e9265c0b49cc2c04af9071d483dca6477e430444867181c7a"></a> enumerator DMA2D\_TRANSFER\_ERROR

    <a id="_CPPv4N20dma2d_trans_status_t18DMA2D_CONFIG_ERRORE"></a>

    <a id="_CPPv3N20dma2d_trans_status_t18DMA2D_CONFIG_ERRORE"></a> <a id="_CPPv2N20dma2d_trans_status_t18DMA2D_CONFIG_ERRORE"></a> <a id="bk__dma2d__types_8h_1aacf2c370826d7ec8e9265c0b49cc2c04a91f57ce130bd1426dbf6cadd99e94de1"></a> enumerator DMA2D\_CONFIG\_ERROR

<a id="_CPPv415dma2d_ioctl_cmd"></a>

<a id="_CPPv315dma2d_ioctl_cmd"></a> <a id="_CPPv215dma2d_ioctl_cmd"></a> <a id="bk__dma2d__types_8h_1a9ca8cedb8221747b70e84d6f8da069b5"></a> enum dma2d\_ioctl\_cmd
:   *Values:*

    <a id="_CPPv4N15dma2d_ioctl_cmd23DMA2D_IOCTL_SET_SWRESRTE"></a>

    <a id="_CPPv3N15dma2d_ioctl_cmd23DMA2D_IOCTL_SET_SWRESRTE"></a> <a id="_CPPv2N15dma2d_ioctl_cmd23DMA2D_IOCTL_SET_SWRESRTE"></a> <a id="bk__dma2d__types_8h_1a9ca8cedb8221747b70e84d6f8da069b5ad6184f7267a4ad0281342a30c80eb6b6"></a> enumerator DMA2D\_IOCTL\_SET\_SWRESRT
    :   Set software reset

    <a id="_CPPv4N15dma2d_ioctl_cmd19DMA2D_IOCTL_SUSPENDE"></a>

    <a id="_CPPv3N15dma2d_ioctl_cmd19DMA2D_IOCTL_SUSPENDE"></a> <a id="_CPPv2N15dma2d_ioctl_cmd19DMA2D_IOCTL_SUSPENDE"></a> <a id="bk__dma2d__types_8h_1a9ca8cedb8221747b70e84d6f8da069b5a8ce1830f990bea96e4b904026c5af57f"></a> enumerator DMA2D\_IOCTL\_SUSPEND
    :   Suspend DMA2D

    <a id="_CPPv4N15dma2d_ioctl_cmd18DMA2D_IOCTL_RESUMEE"></a>

    <a id="_CPPv3N15dma2d_ioctl_cmd18DMA2D_IOCTL_RESUMEE"></a> <a id="_CPPv2N15dma2d_ioctl_cmd18DMA2D_IOCTL_RESUMEE"></a> <a id="bk__dma2d__types_8h_1a9ca8cedb8221747b70e84d6f8da069b5aabbeebb30df430831456edd88caaea65"></a> enumerator DMA2D\_IOCTL\_RESUME
    :   Resume DMA2D

    <a id="_CPPv4N15dma2d_ioctl_cmd23DMA2D_IOCTL_TRANS_ABORTE"></a>

    <a id="_CPPv3N15dma2d_ioctl_cmd23DMA2D_IOCTL_TRANS_ABORTE"></a> <a id="_CPPv2N15dma2d_ioctl_cmd23DMA2D_IOCTL_TRANS_ABORTE"></a> <a id="bk__dma2d__types_8h_1a9ca8cedb8221747b70e84d6f8da069b5a1b5bcbba57d265095ac3a48f3cca241d"></a> enumerator DMA2D\_IOCTL\_TRANS\_ABORT
    :   Abort DMA2D transfer

<a id="id5"></a>

### Header File

- [dma2d\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/dma2d_types.h)

<a id="id6"></a>

### Structures

<a id="_CPPv412dma2d_init_t"></a>

<a id="_CPPv312dma2d_init_t"></a> <a id="_CPPv212dma2d_init_t"></a> <a id="dma2d_init_t"></a> <a id="structdma2d__init__t"></a> struct dma2d\_init\_t
:   DMA2D Init structure definition.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12dma2d_init_t4modeE"></a>

    <a id="_CPPv3N12dma2d_init_t4modeE"></a> <a id="_CPPv2N12dma2d_init_t4modeE"></a> <a id="dma2d_init_t::mode__dma2d_mode_t"></a> <a id="structdma2d__init__t_1a305eaea157b708df4f192e805b2e7592"></a> [dma2d\_mode\_t](#_CPPv412dma2d_mode_t "dma2d_mode_t") mode
    :   Configures the DMA2D transfer mode.his parameter can be one value of DMA2D\_Mode.

    <a id="_CPPv4N12dma2d_init_t10color_modeE"></a>

    <a id="_CPPv3N12dma2d_init_t10color_modeE"></a> <a id="_CPPv2N12dma2d_init_t10color_modeE"></a> <a id="dma2d_init_t::color_mode__uint32_t"></a> <a id="structdma2d__init__t_1a7999d8ed0c3c81849245aa88d44d44fa"></a> uint32\_t color\_mode
    :   Configures the color format of the output image. This parameter can be one value of DMA2D\_Output\_Color\_Mode.

    <a id="_CPPv4N12dma2d_init_t13output_offsetE"></a>

    <a id="_CPPv3N12dma2d_init_t13output_offsetE"></a> <a id="_CPPv2N12dma2d_init_t13output_offsetE"></a> <a id="dma2d_init_t::output_offset__uint32_t"></a> <a id="structdma2d__init__t_1ad40b010301ac57cfef31d0eaf9f0c5b4"></a> uint32\_t output\_offset
    :   Specifies the Offset value. This parameter must be a number between Min\_Data \= 0x0000 and Max\_Data \= 0x3FFF.

    <a id="_CPPv4N12dma2d_init_t14alpha_invertedE"></a>

    <a id="_CPPv3N12dma2d_init_t14alpha_invertedE"></a> <a id="_CPPv2N12dma2d_init_t14alpha_invertedE"></a> <a id="dma2d_init_t::alpha_inverted__uint32_t"></a> <a id="structdma2d__init__t_1a653738cfd9d725f10de91ed59ec0f365"></a> uint32\_t alpha\_inverted
    :   Select regular or inverted alpha value for the output pixel format converter. This parameter can be one value of DMA2D\_Alpha\_Inverted.

    <a id="_CPPv4N12dma2d_init_t16line_offset_modeE"></a>

    <a id="_CPPv3N12dma2d_init_t16line_offset_modeE"></a> <a id="_CPPv2N12dma2d_init_t16line_offset_modeE"></a> <a id="dma2d_init_t::line_offset_mode__uint32_t"></a> <a id="structdma2d__init__t_1ad7d9613c2e8686ad86d4de2dddd22c10"></a> uint32\_t line\_offset\_mode
    :   Configures how is expressed the line offset for the foreground, background and output. This parameter can be one value of DMA2D\_Line\_Offset\_Mode.

    <a id="_CPPv4N12dma2d_init_t13red_blue_swapE"></a>

    <a id="_CPPv3N12dma2d_init_t13red_blue_swapE"></a> <a id="_CPPv2N12dma2d_init_t13red_blue_swapE"></a> <a id="dma2d_init_t::red_blue_swap__uint8_t"></a> <a id="structdma2d__init__t_1a4eb523949fe135e16c5063fcb9f1ff7e"></a> uint8\_t red\_blue\_swap
    :   Select regular mode (RGB or ARGB) or swap mode (BGR or ABGR) for the output pixel format converter. This parameter can be one value of DMA2D\_RB\_Swap.

    <a id="_CPPv4N12dma2d_init_t24out_byte_by_byte_reverseE"></a>

    <a id="_CPPv3N12dma2d_init_t24out_byte_by_byte_reverseE"></a> <a id="_CPPv2N12dma2d_init_t24out_byte_by_byte_reverseE"></a> <a id="dma2d_init_t::out_byte_by_byte_reverse__uint8_t"></a> <a id="structdma2d__init__t_1a9836ae01620b0bf98d8af1a61b4e8154"></a> uint8\_t out\_byte\_by\_byte\_reverse
    :   DMA2D\_BYTE\_REVERSE or DMA2D\_NO\_REVERSE , normally for 32bit color of yuv format

    <a id="_CPPv4N12dma2d_init_t13trans_abilityE"></a>

    <a id="_CPPv3N12dma2d_init_t13trans_abilityE"></a> <a id="_CPPv2N12dma2d_init_t13trans_abilityE"></a> <a id="dma2d_init_t::trans_ability__dma2d_trans_ability_t"></a> <a id="structdma2d__init__t_1a70f63adfbabfb0a7273a94a4da2b3723"></a> [dma2d\_trans\_ability\_t](#_CPPv421dma2d_trans_ability_t "dma2d_trans_ability_t") trans\_ability
    :   set defult MAX\_TRANS\_256BYTES

<a id="_CPPv417dma2d_layer_cfg_t"></a>

<a id="_CPPv317dma2d_layer_cfg_t"></a> <a id="_CPPv217dma2d_layer_cfg_t"></a> <a id="dma2d_layer_cfg_t"></a> <a id="structdma2d__layer__cfg__t"></a> struct dma2d\_layer\_cfg\_t
:   DMA2D Layer structure definition

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17dma2d_layer_cfg_t12input_offsetE"></a>

    <a id="_CPPv3N17dma2d_layer_cfg_t12input_offsetE"></a> <a id="_CPPv2N17dma2d_layer_cfg_t12input_offsetE"></a> <a id="dma2d_layer_cfg_t::input_offset__uint32_t"></a> <a id="structdma2d__layer__cfg__t_1acbeffa0425574bbba06ac27760093af3"></a> uint32\_t input\_offset
    :   Configures the DMA2D foreground or background offset. This parameter must be a number between Min\_Data \= 0x0000 and Max\_Data \= 0x3FFF.

    <a id="_CPPv4N17dma2d_layer_cfg_t16input_color_modeE"></a>

    <a id="_CPPv3N17dma2d_layer_cfg_t16input_color_modeE"></a> <a id="_CPPv2N17dma2d_layer_cfg_t16input_color_modeE"></a> <a id="dma2d_layer_cfg_t::input_color_mode__uint32_t"></a> <a id="structdma2d__layer__cfg__t_1a90430c0e8335983abef91117b0ac151d"></a> uint32\_t input\_color\_mode
    :   Configures the DMA2D foreground or background color mode. This parameter can be one value of DMA2D\_Input\_Color\_Mode.

    <a id="_CPPv4N17dma2d_layer_cfg_t10alpha_modeE"></a>

    <a id="_CPPv3N17dma2d_layer_cfg_t10alpha_modeE"></a> <a id="_CPPv2N17dma2d_layer_cfg_t10alpha_modeE"></a> <a id="dma2d_layer_cfg_t::alpha_mode__uint32_t"></a> <a id="structdma2d__layer__cfg__t_1a2aa8ff3a0501d97a4e84d3230774c734"></a> uint32\_t alpha\_mode
    :   Configures the DMA2D foreground or background alpha mode.This parameter can be one value of DMA2D\_Alpha\_Mode.

    <a id="_CPPv4N17dma2d_layer_cfg_t11input_colorE"></a>

    <a id="_CPPv3N17dma2d_layer_cfg_t11input_colorE"></a> <a id="_CPPv2N17dma2d_layer_cfg_t11input_colorE"></a> <a id="dma2d_layer_cfg_t::input_color__uint32_t"></a> <a id="structdma2d__layer__cfg__t_1a92892df93cc6e80d1eeacc7d14c72f1f"></a> uint32\_t input\_color
    :   Specifies color value in case of A8 or A4 color mode.

        备注

        In case of A8 or A4 color mode (ARGB), this parameter must be a number between Min\_Data \= 0x00000000 and Max\_Data \= 0xFFFFFF where

        - Inputcolor\[16:23\] is the red value RED\[0:7\]
        - Inputcolor\[8:15\] is the green value GREEN\[0:7\]
        - Inputcolor\[0:7\] is the blue value BLUE\[0:7\].

    <a id="_CPPv4N17dma2d_layer_cfg_t14alpha_invertedE"></a>

    <a id="_CPPv3N17dma2d_layer_cfg_t14alpha_invertedE"></a> <a id="_CPPv2N17dma2d_layer_cfg_t14alpha_invertedE"></a> <a id="dma2d_layer_cfg_t::alpha_inverted__uint32_t"></a> <a id="structdma2d__layer__cfg__t_1ad3dbdf64bd2c2efab11344de7b57501b"></a> uint32\_t alpha\_inverted
    :   Select regular or inverted alpha value.This parameter can be one value of DMA2D\_Alpha\_Inverted.

    <a id="_CPPv4N17dma2d_layer_cfg_t13red_blue_swapE"></a>

    <a id="_CPPv3N17dma2d_layer_cfg_t13red_blue_swapE"></a> <a id="_CPPv2N17dma2d_layer_cfg_t13red_blue_swapE"></a> <a id="dma2d_layer_cfg_t::red_blue_swap__uint32_t"></a> <a id="structdma2d__layer__cfg__t_1a29a8d404754a57d864f813e83b6bc36d"></a> uint32\_t red\_blue\_swap
    :   Select regular mode (RGB or ARGB) or swap mode (BGR or ABGR). This parameter can be one value of DMA2D\_RB\_Swap.

    <a id="_CPPv4N17dma2d_layer_cfg_t18input_data_reverseE"></a>

    <a id="_CPPv3N17dma2d_layer_cfg_t18input_data_reverseE"></a> <a id="_CPPv2N17dma2d_layer_cfg_t18input_data_reverseE"></a> <a id="dma2d_layer_cfg_t::input_data_reverse__data_reverse_t"></a> <a id="structdma2d__layer__cfg__t_1acfd5795487962a3f03890e054668769c"></a> [data\_reverse\_t](#_CPPv414data_reverse_t "data_reverse_t") input\_data\_reverse
    :   input formart for yuv format, reverse data byte by byte or halfword by halfword.

<a id="_CPPv414dma2d_config_t"></a>

<a id="_CPPv314dma2d_config_t"></a> <a id="_CPPv214dma2d_config_t"></a> <a id="dma2d_config_t"></a> <a id="structdma2d__config__t"></a> struct dma2d\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14dma2d_config_t4initE"></a>

    <a id="_CPPv3N14dma2d_config_t4initE"></a> <a id="_CPPv2N14dma2d_config_t4initE"></a> <a id="dma2d_config_t::init__dma2d_init_t"></a> <a id="structdma2d__config__t_1a8d2526741d849cf17fbde00a609b9c5b"></a> [dma2d\_init\_t](#_CPPv412dma2d_init_t "dma2d_init_t") init
    :   dma2d init config, is the value of struct [dma2d\_init\_t](#structdma2d__init__t)

    <a id="_CPPv4N14dma2d_config_t9layer_cfgE"></a>

    <a id="_CPPv3N14dma2d_config_t9layer_cfgE"></a> <a id="_CPPv2N14dma2d_config_t9layer_cfgE"></a> <a id="dma2d_config_t::layer_cfg__dma2d_layer_cfg_tA"></a> <a id="structdma2d__config__t_1ad42aae62c7c3aa32311858a1cc336313"></a> [dma2d\_layer\_cfg\_t](#_CPPv417dma2d_layer_cfg_t "dma2d_layer_cfg_t") layer\_cfg\[MAX\_DMA2D\_LAYER\]
    :   dma2d layer config, is the value of struct [dma2d\_layer\_cfg\_t](#structdma2d__layer__cfg__t) the param MAX\_DMA2D\_LAYER is select from DMA2D\_BACKGROUND\_LAYER and DMA2D\_FOREGROUND\_LAYER

<a id="_CPPv413dma2d_blend_t"></a>

<a id="_CPPv313dma2d_blend_t"></a> <a id="_CPPv213dma2d_blend_t"></a> <a id="dma2d_blend_t"></a> <a id="structdma2d__blend__t"></a> struct dma2d\_blend\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13dma2d_blend_t8pfg_addrE"></a>

    <a id="_CPPv3N13dma2d_blend_t8pfg_addrE"></a> <a id="_CPPv2N13dma2d_blend_t8pfg_addrE"></a> <a id="dma2d_blend_t::pfg_addr__voidP"></a> <a id="structdma2d__blend__t_1a40428df5fc3579cdac34b57f2c1e3516"></a> void \*pfg\_addr
    :   The source memory Buffer address for the foreground layer..

    <a id="_CPPv4N13dma2d_blend_t8pbg_addrE"></a>

    <a id="_CPPv3N13dma2d_blend_t8pbg_addrE"></a> <a id="_CPPv2N13dma2d_blend_t8pbg_addrE"></a> <a id="dma2d_blend_t::pbg_addr__voidP"></a> <a id="structdma2d__blend__t_1a979684d78195e03570dc2e13c027d500"></a> void \*pbg\_addr
    :   he source memory Buffer address for the background layer…

    <a id="_CPPv4N13dma2d_blend_t9pdst_addrE"></a>

    <a id="_CPPv3N13dma2d_blend_t9pdst_addrE"></a> <a id="_CPPv2N13dma2d_blend_t9pdst_addrE"></a> <a id="dma2d_blend_t::pdst_addr__voidP"></a> <a id="structdma2d__blend__t_1ae6ec5ddf3a1ddbbcc03edc924f190634"></a> void \*pdst\_addr
    :   The output memory Buffer address ..

    <a id="_CPPv4N13dma2d_blend_t13fg_color_modeE"></a>

    <a id="_CPPv3N13dma2d_blend_t13fg_color_modeE"></a> <a id="_CPPv2N13dma2d_blend_t13fg_color_modeE"></a> <a id="dma2d_blend_t::fg_color_mode__input_color_mode_t"></a> <a id="structdma2d__blend__t_1a0f7943b68abf2b7f5ffa41acd2c7ccf4"></a> [input\_color\_mode\_t](#_CPPv418input_color_mode_t "input_color_mode_t") fg\_color\_mode
    :   fg color mode..

    <a id="_CPPv4N13dma2d_blend_t13bg_color_modeE"></a>

    <a id="_CPPv3N13dma2d_blend_t13bg_color_modeE"></a> <a id="_CPPv2N13dma2d_blend_t13bg_color_modeE"></a> <a id="dma2d_blend_t::bg_color_mode__input_color_mode_t"></a> <a id="structdma2d__blend__t_1a4f9f536e20feefe324477f240530985c"></a> [input\_color\_mode\_t](#_CPPv418input_color_mode_t "input_color_mode_t") bg\_color\_mode
    :   bg color mode..

    <a id="_CPPv4N13dma2d_blend_t14dst_color_modeE"></a>

    <a id="_CPPv3N13dma2d_blend_t14dst_color_modeE"></a> <a id="_CPPv2N13dma2d_blend_t14dst_color_modeE"></a> <a id="dma2d_blend_t::dst_color_mode__out_color_mode_t"></a> <a id="structdma2d__blend__t_1a87718b3144cc420d3bd40a956d955ba8"></a> [out\_color\_mode\_t](#_CPPv416out_color_mode_t "out_color_mode_t") dst\_color\_mode
    :   out color mode..

    <a id="_CPPv4N13dma2d_blend_t10fg_offlineE"></a>

    <a id="_CPPv3N13dma2d_blend_t10fg_offlineE"></a> <a id="_CPPv2N13dma2d_blend_t10fg_offlineE"></a> <a id="dma2d_blend_t::fg_offline__uint32_t"></a> <a id="structdma2d__blend__t_1a6e432d08771985457aa95d1d2751aa1c"></a> uint32\_t fg\_offline
    :   for partical copy this is to calculate start addr based on fg frame addr, uint by pixel

    <a id="_CPPv4N13dma2d_blend_t10bg_offlineE"></a>

    <a id="_CPPv3N13dma2d_blend_t10bg_offlineE"></a> <a id="_CPPv2N13dma2d_blend_t10bg_offlineE"></a> <a id="dma2d_blend_t::bg_offline__uint32_t"></a> <a id="structdma2d__blend__t_1a3a5de1915539514f16e812027939c671"></a> uint32\_t bg\_offline
    :   for partical copy this is to calculate start addr based on bg frame addr, uint by pixel

    <a id="_CPPv4N13dma2d_blend_t12dest_offlineE"></a>

    <a id="_CPPv3N13dma2d_blend_t12dest_offlineE"></a> <a id="_CPPv2N13dma2d_blend_t12dest_offlineE"></a> <a id="dma2d_blend_t::dest_offline__uint32_t"></a> <a id="structdma2d__blend__t_1a4f64b255fb9705122450df2740f501db"></a> uint32\_t dest\_offline
    :   for partical copy this is to calculate output addr based on dst frame addr, uint by pixel

    <a id="_CPPv4N13dma2d_blend_t5xsizeE"></a>

    <a id="_CPPv3N13dma2d_blend_t5xsizeE"></a> <a id="_CPPv2N13dma2d_blend_t5xsizeE"></a> <a id="dma2d_blend_t::xsize__uint32_t"></a> <a id="structdma2d__blend__t_1a2bc738b9d20ee205062bd323dc664b2e"></a> uint32\_t xsize
    :   dma2d blend x size..

    <a id="_CPPv4N13dma2d_blend_t5ysizeE"></a>

    <a id="_CPPv3N13dma2d_blend_t5ysizeE"></a> <a id="_CPPv2N13dma2d_blend_t5ysizeE"></a> <a id="dma2d_blend_t::ysize__uint32_t"></a> <a id="structdma2d__blend__t_1a44112872960b69f563d151db8f861757"></a> uint32\_t ysize
    :   dma2d blend y size..

    <a id="_CPPv4N13dma2d_blend_t14fg_alpha_valueE"></a>

    <a id="_CPPv3N13dma2d_blend_t14fg_alpha_valueE"></a> <a id="_CPPv2N13dma2d_blend_t14fg_alpha_valueE"></a> <a id="dma2d_blend_t::fg_alpha_value__uint8_t"></a> <a id="structdma2d__blend__t_1aefe2f2421dbb08bcab13cd5f0cd7e040"></a> uint8\_t fg\_alpha\_value
    :   config fg alpha..

    <a id="_CPPv4N13dma2d_blend_t14bg_alpha_valueE"></a>

    <a id="_CPPv3N13dma2d_blend_t14bg_alpha_valueE"></a> <a id="_CPPv2N13dma2d_blend_t14bg_alpha_valueE"></a> <a id="dma2d_blend_t::bg_alpha_value__uint8_t"></a> <a id="structdma2d__blend__t_1a412da2cc9c57f814c82b47d8faa51d7e"></a> uint8\_t bg\_alpha\_value
    :   config bg alpha.

    <a id="_CPPv4N13dma2d_blend_t13red_bule_swapE"></a>

    <a id="_CPPv3N13dma2d_blend_t13red_bule_swapE"></a> <a id="_CPPv2N13dma2d_blend_t13red_bule_swapE"></a> <a id="dma2d_blend_t::red_bule_swap__red_blue_swap_t"></a> <a id="structdma2d__blend__t_1ab37bec59e303f9af8e5d71d1ca0d3403"></a> [red\_blue\_swap\_t](#_CPPv415red_blue_swap_t "red_blue_swap_t") red\_bule\_swap
    :   DMA2D\_RB\_SWAP or DMA2D\_RB\_REGULAR

<a id="_CPPv420dma2d_offset_blend_t"></a>

<a id="_CPPv320dma2d_offset_blend_t"></a> <a id="_CPPv220dma2d_offset_blend_t"></a> <a id="dma2d_offset_blend_t"></a> <a id="structdma2d__offset__blend__t"></a> struct dma2d\_offset\_blend\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20dma2d_offset_blend_t8pfg_addrE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t8pfg_addrE"></a> <a id="_CPPv2N20dma2d_offset_blend_t8pfg_addrE"></a> <a id="dma2d_offset_blend_t::pfg_addr__voidP"></a> <a id="structdma2d__offset__blend__t_1a39daa18202b925b12f6a69adc7074fd6"></a> void \*pfg\_addr
    :   The source memory Buffer address for the foreground layer..

    <a id="_CPPv4N20dma2d_offset_blend_t8pbg_addrE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t8pbg_addrE"></a> <a id="_CPPv2N20dma2d_offset_blend_t8pbg_addrE"></a> <a id="dma2d_offset_blend_t::pbg_addr__voidP"></a> <a id="structdma2d__offset__blend__t_1ae3c4e6c6850ac8c390a710c3409934e3"></a> void \*pbg\_addr
    :   he source memory Buffer address for the background layer…

    <a id="_CPPv4N20dma2d_offset_blend_t9pdst_addrE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t9pdst_addrE"></a> <a id="_CPPv2N20dma2d_offset_blend_t9pdst_addrE"></a> <a id="dma2d_offset_blend_t::pdst_addr__voidP"></a> <a id="structdma2d__offset__blend__t_1a61689cf9a484a18c2e6b58d3692513bc"></a> void \*pdst\_addr
    :   The output memory Buffer address ..

    <a id="_CPPv4N20dma2d_offset_blend_t13fg_color_modeE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t13fg_color_modeE"></a> <a id="_CPPv2N20dma2d_offset_blend_t13fg_color_modeE"></a> <a id="dma2d_offset_blend_t::fg_color_mode__input_color_mode_t"></a> <a id="structdma2d__offset__blend__t_1a828b5531dbfb457cb0757e9dfa84627b"></a> [input\_color\_mode\_t](#_CPPv418input_color_mode_t "input_color_mode_t") fg\_color\_mode
    :   fg color mode..

    <a id="_CPPv4N20dma2d_offset_blend_t13bg_color_modeE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t13bg_color_modeE"></a> <a id="_CPPv2N20dma2d_offset_blend_t13bg_color_modeE"></a> <a id="dma2d_offset_blend_t::bg_color_mode__input_color_mode_t"></a> <a id="structdma2d__offset__blend__t_1a6c58a929f52e6f10105cdc56f17d8a2c"></a> [input\_color\_mode\_t](#_CPPv418input_color_mode_t "input_color_mode_t") bg\_color\_mode
    :   bg color mode..

    <a id="_CPPv4N20dma2d_offset_blend_t14dst_color_modeE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t14dst_color_modeE"></a> <a id="_CPPv2N20dma2d_offset_blend_t14dst_color_modeE"></a> <a id="dma2d_offset_blend_t::dst_color_mode__out_color_mode_t"></a> <a id="structdma2d__offset__blend__t_1af2fea9200f8821a0b148083260928c0b"></a> [out\_color\_mode\_t](#_CPPv416out_color_mode_t "out_color_mode_t") dst\_color\_mode
    :   out color mode..

    <a id="_CPPv4N20dma2d_offset_blend_t13fg_frame_xposE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t13fg_frame_xposE"></a> <a id="_CPPv2N20dma2d_offset_blend_t13fg_frame_xposE"></a> <a id="dma2d_offset_blend_t::fg_frame_xpos__uint16_t"></a> <a id="structdma2d__offset__blend__t_1ad8a4195e3b359c081643163ba20d90d9"></a> uint16\_t fg\_frame\_xpos
    :   src img start copy/pfc x pos

    <a id="_CPPv4N20dma2d_offset_blend_t13fg_frame_yposE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t13fg_frame_yposE"></a> <a id="_CPPv2N20dma2d_offset_blend_t13fg_frame_yposE"></a> <a id="dma2d_offset_blend_t::fg_frame_ypos__uint16_t"></a> <a id="structdma2d__offset__blend__t_1a52324c4aeca5df18c92acb813fb65abd"></a> uint16\_t fg\_frame\_ypos
    :   src img start copy/pfc y pos

    <a id="_CPPv4N20dma2d_offset_blend_t13bg_frame_xposE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t13bg_frame_xposE"></a> <a id="_CPPv2N20dma2d_offset_blend_t13bg_frame_xposE"></a> <a id="dma2d_offset_blend_t::bg_frame_xpos__uint16_t"></a> <a id="structdma2d__offset__blend__t_1a7fd46974d7a34c55ed1efda98d7cff9e"></a> uint16\_t bg\_frame\_xpos
    :   dma2d fill x pos based on frame\_xsize

    <a id="_CPPv4N20dma2d_offset_blend_t13bg_frame_yposE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t13bg_frame_yposE"></a> <a id="_CPPv2N20dma2d_offset_blend_t13bg_frame_yposE"></a> <a id="dma2d_offset_blend_t::bg_frame_ypos__uint16_t"></a> <a id="structdma2d__offset__blend__t_1a9501a4c359ad85f9f5da9c66f8cac416"></a> uint16\_t bg\_frame\_ypos
    :   dma2d fill y pos based on frame\_ysize

    <a id="_CPPv4N20dma2d_offset_blend_t14dst_frame_xposE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t14dst_frame_xposE"></a> <a id="_CPPv2N20dma2d_offset_blend_t14dst_frame_xposE"></a> <a id="dma2d_offset_blend_t::dst_frame_xpos__uint16_t"></a> <a id="structdma2d__offset__blend__t_1a708d1cb89d7fffc43f2d94456ed216c8"></a> uint16\_t dst\_frame\_xpos
    :   dma2d fill x pos based on frame\_xsize

    <a id="_CPPv4N20dma2d_offset_blend_t14dst_frame_yposE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t14dst_frame_yposE"></a> <a id="_CPPv2N20dma2d_offset_blend_t14dst_frame_yposE"></a> <a id="dma2d_offset_blend_t::dst_frame_ypos__uint16_t"></a> <a id="structdma2d__offset__blend__t_1adc7f37d91c60012c95fbd37c93339084"></a> uint16\_t dst\_frame\_ypos
    :   dma2d fill y pos based on frame\_ysize

    <a id="_CPPv4N20dma2d_offset_blend_t14fg_frame_widthE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t14fg_frame_widthE"></a> <a id="_CPPv2N20dma2d_offset_blend_t14fg_frame_widthE"></a> <a id="dma2d_offset_blend_t::fg_frame_width__uint16_t"></a> <a id="structdma2d__offset__blend__t_1a327a5d1381e939b033c98f835e678bc9"></a> uint16\_t fg\_frame\_width
    :   src image width

    <a id="_CPPv4N20dma2d_offset_blend_t15fg_frame_heightE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t15fg_frame_heightE"></a> <a id="_CPPv2N20dma2d_offset_blend_t15fg_frame_heightE"></a> <a id="dma2d_offset_blend_t::fg_frame_height__uint16_t"></a> <a id="structdma2d__offset__blend__t_1a5ce93fbca83adc9e81af65958ce0c722"></a> uint16\_t fg\_frame\_height
    :   src image height

    <a id="_CPPv4N20dma2d_offset_blend_t14bg_frame_widthE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t14bg_frame_widthE"></a> <a id="_CPPv2N20dma2d_offset_blend_t14bg_frame_widthE"></a> <a id="dma2d_offset_blend_t::bg_frame_width__uint16_t"></a> <a id="structdma2d__offset__blend__t_1a2acc70ca0399fd69fc0d68fbf49f9592"></a> uint16\_t bg\_frame\_width
    :   src image width

    <a id="_CPPv4N20dma2d_offset_blend_t15bg_frame_heightE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t15bg_frame_heightE"></a> <a id="_CPPv2N20dma2d_offset_blend_t15bg_frame_heightE"></a> <a id="dma2d_offset_blend_t::bg_frame_height__uint16_t"></a> <a id="structdma2d__offset__blend__t_1aaae0b284f5b72c95952f02c98f635823"></a> uint16\_t bg\_frame\_height
    :   src image height

    <a id="_CPPv4N20dma2d_offset_blend_t15dst_frame_widthE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t15dst_frame_widthE"></a> <a id="_CPPv2N20dma2d_offset_blend_t15dst_frame_widthE"></a> <a id="dma2d_offset_blend_t::dst_frame_width__uint16_t"></a> <a id="structdma2d__offset__blend__t_1aeeb37a8a1ea691ae7648430b46cc9c34"></a> uint16\_t dst\_frame\_width
    :   src image width

    <a id="_CPPv4N20dma2d_offset_blend_t16dst_frame_heightE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t16dst_frame_heightE"></a> <a id="_CPPv2N20dma2d_offset_blend_t16dst_frame_heightE"></a> <a id="dma2d_offset_blend_t::dst_frame_height__uint16_t"></a> <a id="structdma2d__offset__blend__t_1af034edeb962df3f017cd376d43bd6442"></a> uint16\_t dst\_frame\_height
    :   src image height

    <a id="_CPPv4N20dma2d_offset_blend_t11dma2d_widthE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t11dma2d_widthE"></a> <a id="_CPPv2N20dma2d_offset_blend_t11dma2d_widthE"></a> <a id="dma2d_offset_blend_t::dma2d_width__uint32_t"></a> <a id="structdma2d__offset__blend__t_1ad5abd61bd58f7d0838b3cd78c9d16efb"></a> uint32\_t dma2d\_width
    :   dma2d blend x size..

    <a id="_CPPv4N20dma2d_offset_blend_t12dma2d_heightE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t12dma2d_heightE"></a> <a id="_CPPv2N20dma2d_offset_blend_t12dma2d_heightE"></a> <a id="dma2d_offset_blend_t::dma2d_height__uint32_t"></a> <a id="structdma2d__offset__blend__t_1a99abba7157e37cbd4f30de0caf3cde96"></a> uint32\_t dma2d\_height
    :   dma2d blend y size..

    <a id="_CPPv4N20dma2d_offset_blend_t14fg_alpha_valueE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t14fg_alpha_valueE"></a> <a id="_CPPv2N20dma2d_offset_blend_t14fg_alpha_valueE"></a> <a id="dma2d_offset_blend_t::fg_alpha_value__uint8_t"></a> <a id="structdma2d__offset__blend__t_1a05f6ef2dabbd5079f3969a06427dd534"></a> uint8\_t fg\_alpha\_value
    :   config fg alpha..

    <a id="_CPPv4N20dma2d_offset_blend_t14bg_alpha_valueE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t14bg_alpha_valueE"></a> <a id="_CPPv2N20dma2d_offset_blend_t14bg_alpha_valueE"></a> <a id="dma2d_offset_blend_t::bg_alpha_value__uint8_t"></a> <a id="structdma2d__offset__blend__t_1a3dedf0e7365edbf4f9f08016b916820a"></a> uint8\_t bg\_alpha\_value
    :   config bg alpha.

    <a id="_CPPv4N20dma2d_offset_blend_t16fg_red_blue_swapE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t16fg_red_blue_swapE"></a> <a id="_CPPv2N20dma2d_offset_blend_t16fg_red_blue_swapE"></a> <a id="dma2d_offset_blend_t::fg_red_blue_swap__red_blue_swap_t"></a> <a id="structdma2d__offset__blend__t_1a2148ac0e2471ef49abe01bda37f0da99"></a> [red\_blue\_swap\_t](#_CPPv415red_blue_swap_t "red_blue_swap_t") fg\_red\_blue\_swap
    :   fg img red blue swap, select DMA2D\_RB\_SWAP or DMA2D\_RB\_REGULAR

    <a id="_CPPv4N20dma2d_offset_blend_t16bg_red_blue_swapE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t16bg_red_blue_swapE"></a> <a id="_CPPv2N20dma2d_offset_blend_t16bg_red_blue_swapE"></a> <a id="dma2d_offset_blend_t::bg_red_blue_swap__red_blue_swap_t"></a> <a id="structdma2d__offset__blend__t_1a4605f3cd633966c8353fc4c904e2e192"></a> [red\_blue\_swap\_t](#_CPPv415red_blue_swap_t "red_blue_swap_t") bg\_red\_blue\_swap
    :   bg img red blue swap, select DMA2D\_RB\_SWAP or DMA2D\_RB\_REGULAR

    <a id="_CPPv4N20dma2d_offset_blend_t17dst_red_blue_swapE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t17dst_red_blue_swapE"></a> <a id="_CPPv2N20dma2d_offset_blend_t17dst_red_blue_swapE"></a> <a id="dma2d_offset_blend_t::dst_red_blue_swap__red_blue_swap_t"></a> <a id="structdma2d__offset__blend__t_1a11759d0630c43b117ded5077c2abb597"></a> [red\_blue\_swap\_t](#_CPPv415red_blue_swap_t "red_blue_swap_t") dst\_red\_blue\_swap
    :   dst img red blue swap, select DMA2D\_RB\_SWAP or DMA2D\_RB\_REGULAR

    <a id="_CPPv4N20dma2d_offset_blend_t18input_data_reverseE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t18input_data_reverseE"></a> <a id="_CPPv2N20dma2d_offset_blend_t18input_data_reverseE"></a> <a id="dma2d_offset_blend_t::input_data_reverse__data_reverse_t"></a> <a id="structdma2d__offset__blend__t_1ac54a9fa1e30a221b309e2931852e4831"></a> [data\_reverse\_t](#_CPPv414data_reverse_t "data_reverse_t") input\_data\_reverse
    :   NO\_REVERSE, BYTE\_BY\_BYTE\_REVERSE or HFWORD\_BY\_HFWORD\_REVERSE

    <a id="_CPPv4N20dma2d_offset_blend_t24out_byte_by_byte_reverseE"></a>

    <a id="_CPPv3N20dma2d_offset_blend_t24out_byte_by_byte_reverseE"></a> <a id="_CPPv2N20dma2d_offset_blend_t24out_byte_by_byte_reverseE"></a> <a id="dma2d_offset_blend_t::out_byte_by_byte_reverse__data_reverse_t"></a> <a id="structdma2d__offset__blend__t_1a05b661c298e2cb36b0d9cddf9b0b7e07"></a> [data\_reverse\_t](#_CPPv414data_reverse_t "data_reverse_t") out\_byte\_by\_byte\_reverse
    :   NO\_REVERSE, BYTE\_BY\_BYTE\_REVERSE or HFWORD\_BY\_HFWORD\_REVERSE

<a id="_CPPv418dma2d_memcpy_pfc_t"></a>

<a id="_CPPv318dma2d_memcpy_pfc_t"></a> <a id="_CPPv218dma2d_memcpy_pfc_t"></a> <a id="dma2d_memcpy_pfc_t"></a> <a id="structdma2d__memcpy__pfc__t"></a> struct dma2d\_memcpy\_pfc\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18dma2d_memcpy_pfc_t10input_addrE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t10input_addrE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t10input_addrE"></a> <a id="dma2d_memcpy_pfc_t::input_addr__voidP"></a> <a id="structdma2d__memcpy__pfc__t_1a9b5ca498b096335601eeecaac8836b0e"></a> void \*input\_addr
    :   The image memcpy or pixel convert src addr

    <a id="_CPPv4N18dma2d_memcpy_pfc_t15src_frame_widthE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t15src_frame_widthE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t15src_frame_widthE"></a> <a id="dma2d_memcpy_pfc_t::src_frame_width__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1a530f5910445d72c58d9e3b04f87a3212"></a> uint16\_t src\_frame\_width
    :   memcpy or pfc src image width

    <a id="_CPPv4N18dma2d_memcpy_pfc_t16src_frame_heightE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t16src_frame_heightE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t16src_frame_heightE"></a> <a id="dma2d_memcpy_pfc_t::src_frame_height__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1ad02d84ae9983f3609ee543eb34992764"></a> uint16\_t src\_frame\_height
    :   imemcpy or pfc src image height

    <a id="_CPPv4N18dma2d_memcpy_pfc_t14src_frame_xposE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t14src_frame_xposE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t14src_frame_xposE"></a> <a id="dma2d_memcpy_pfc_t::src_frame_xpos__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1abb9b5dd4965174e1dfddb39a9012dcdd"></a> uint16\_t src\_frame\_xpos
    :   src img start copy/pfc x pos

    <a id="_CPPv4N18dma2d_memcpy_pfc_t14src_frame_yposE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t14src_frame_yposE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t14src_frame_yposE"></a> <a id="dma2d_memcpy_pfc_t::src_frame_ypos__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1aa1f03c54eac7ff802e2b911cfb1ebbc5"></a> uint16\_t src\_frame\_ypos
    :   src img start copy/pfc y pos

    <a id="_CPPv4N18dma2d_memcpy_pfc_t16input_color_modeE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t16input_color_modeE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t16input_color_modeE"></a> <a id="dma2d_memcpy_pfc_t::input_color_mode__input_color_mode_t"></a> <a id="structdma2d__memcpy__pfc__t_1a38258522b3e6c3f315cd330682ad79e8"></a> [input\_color\_mode\_t](#_CPPv418input_color_mode_t "input_color_mode_t") input\_color\_mode
    :   The pixel convert src color mode

    <a id="_CPPv4N18dma2d_memcpy_pfc_t18input_data_reverseE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t18input_data_reverseE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t18input_data_reverseE"></a> <a id="dma2d_memcpy_pfc_t::input_data_reverse__data_reverse_t"></a> <a id="structdma2d__memcpy__pfc__t_1a63f41e99cc44f7a35c9ce7b080e2fe5d"></a> [data\_reverse\_t](#_CPPv414data_reverse_t "data_reverse_t") input\_data\_reverse
    :   NO\_REVERSE, BYTE\_BY\_BYTE\_REVERSE or HFWORD\_BY\_HFWORD\_REVERSE

    <a id="_CPPv4N18dma2d_memcpy_pfc_t19input_red_blue_swapE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t19input_red_blue_swapE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t19input_red_blue_swapE"></a> <a id="dma2d_memcpy_pfc_t::input_red_blue_swap__red_blue_swap_t"></a> <a id="structdma2d__memcpy__pfc__t_1af316c5ebd5296dc8c84428b848adbde4"></a> [red\_blue\_swap\_t](#_CPPv415red_blue_swap_t "red_blue_swap_t") input\_red\_blue\_swap
    :   src img red blue swap, select DMA2D\_RB\_SWAP or DMA2D\_RB\_REGULAR

    <a id="_CPPv4N18dma2d_memcpy_pfc_t11output_addrE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t11output_addrE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t11output_addrE"></a> <a id="dma2d_memcpy_pfc_t::output_addr__voidP"></a> <a id="structdma2d__memcpy__pfc__t_1a13abb87f52ce444b5f92eb1db8c8f7ae"></a> void \*output\_addr
    :   The mage memcpy or pixel convert dst addr

    <a id="_CPPv4N18dma2d_memcpy_pfc_t15dst_frame_widthE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t15dst_frame_widthE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t15dst_frame_widthE"></a> <a id="dma2d_memcpy_pfc_t::dst_frame_width__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1ab61e60a1f301572b54d5239e8c032aeb"></a> uint16\_t dst\_frame\_width
    :   memcpy to dst image, the dst image width

    <a id="_CPPv4N18dma2d_memcpy_pfc_t16dst_frame_heightE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t16dst_frame_heightE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t16dst_frame_heightE"></a> <a id="dma2d_memcpy_pfc_t::dst_frame_height__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1ac038660fa40681437bc5d0eb4e20abc8"></a> uint16\_t dst\_frame\_height
    :   memcpy to dst image, the dst image height

    <a id="_CPPv4N18dma2d_memcpy_pfc_t14dst_frame_xposE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t14dst_frame_xposE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t14dst_frame_xposE"></a> <a id="dma2d_memcpy_pfc_t::dst_frame_xpos__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1ac7dc3c3bef0d499fb741d41fa94e18fb"></a> uint16\_t dst\_frame\_xpos
    :   dma2d fill x pos based on frame\_xsize

    <a id="_CPPv4N18dma2d_memcpy_pfc_t14dst_frame_yposE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t14dst_frame_yposE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t14dst_frame_yposE"></a> <a id="dma2d_memcpy_pfc_t::dst_frame_ypos__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1a56abbebd99f154f4947c486bf5f67473"></a> uint16\_t dst\_frame\_ypos
    :   dma2d fill y pos based on frame\_ysize

    <a id="_CPPv4N18dma2d_memcpy_pfc_t17output_color_modeE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t17output_color_modeE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t17output_color_modeE"></a> <a id="dma2d_memcpy_pfc_t::output_color_mode__out_color_mode_t"></a> <a id="structdma2d__memcpy__pfc__t_1ab814d8d2e65d2a2f0eb5bb43ffd13297"></a> [out\_color\_mode\_t](#_CPPv416out_color_mode_t "out_color_mode_t") output\_color\_mode
    :   The pixel convert dst color mode

    <a id="_CPPv4N18dma2d_memcpy_pfc_t20output_red_blue_swapE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t20output_red_blue_swapE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t20output_red_blue_swapE"></a> <a id="dma2d_memcpy_pfc_t::output_red_blue_swap__red_blue_swap_t"></a> <a id="structdma2d__memcpy__pfc__t_1a02fa23d715acdef2b905dd47b560c8a4"></a> [red\_blue\_swap\_t](#_CPPv415red_blue_swap_t "red_blue_swap_t") output\_red\_blue\_swap
    :   src img red blue swap, select DMA2D\_RB\_SWAP or DMA2D\_RB\_REGULAR

    <a id="_CPPv4N18dma2d_memcpy_pfc_t11dma2d_widthE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t11dma2d_widthE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t11dma2d_widthE"></a> <a id="dma2d_memcpy_pfc_t::dma2d_width__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1a65e4988c40cd64d6ce4f7b5038d2caf6"></a> uint16\_t dma2d\_width
    :   dma2d memcpy or pfc width

    <a id="_CPPv4N18dma2d_memcpy_pfc_t12dma2d_heightE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t12dma2d_heightE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t12dma2d_heightE"></a> <a id="dma2d_memcpy_pfc_t::dma2d_height__uint16_t"></a> <a id="structdma2d__memcpy__pfc__t_1acd3323719be6727c9c28b4b2023e4877"></a> uint16\_t dma2d\_height
    :   dma2d memcpy or pfc height

    <a id="_CPPv4N18dma2d_memcpy_pfc_t11input_alphaE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t11input_alphaE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t11input_alphaE"></a> <a id="dma2d_memcpy_pfc_t::input_alpha__uint8_t"></a> <a id="structdma2d__memcpy__pfc__t_1a56964ee3380b218c05c95ee75f6c8086"></a> uint8\_t input\_alpha
    :   src data alpha, depend on alpha\_mode , only used in pfc

    <a id="_CPPv4N18dma2d_memcpy_pfc_t12output_alphaE"></a>

    <a id="_CPPv3N18dma2d_memcpy_pfc_t12output_alphaE"></a> <a id="_CPPv2N18dma2d_memcpy_pfc_t12output_alphaE"></a> <a id="dma2d_memcpy_pfc_t::output_alpha__uint8_t"></a> <a id="structdma2d__memcpy__pfc__t_1a4a93f2abc75732490ec5b2cb35383e9e"></a> uint8\_t output\_alpha
    :   dst data alpha,depend on alpha\_mode , only used in pfc

<a id="_CPPv412dma2d_fill_t"></a>

<a id="_CPPv312dma2d_fill_t"></a> <a id="_CPPv212dma2d_fill_t"></a> <a id="dma2d_fill_t"></a> <a id="structdma2d__fill__t"></a> struct dma2d\_fill\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12dma2d_fill_t9frameaddrE"></a>

    <a id="_CPPv3N12dma2d_fill_t9frameaddrE"></a> <a id="_CPPv2N12dma2d_fill_t9frameaddrE"></a> <a id="dma2d_fill_t::frameaddr__voidP"></a> <a id="structdma2d__fill__t_1a6d17b2ee3a1bd5ae940098ddae878229"></a> void \*frameaddr
    :   dma2d fill frame baseaddr , normally LCD start frame addr

    <a id="_CPPv4N12dma2d_fill_t11frame_xsizeE"></a>

    <a id="_CPPv3N12dma2d_fill_t11frame_xsizeE"></a> <a id="_CPPv2N12dma2d_fill_t11frame_xsizeE"></a> <a id="dma2d_fill_t::frame_xsize__uint16_t"></a> <a id="structdma2d__fill__t_1aba8b9601b06aa4dcee80794564275b05"></a> uint16\_t frame\_xsize
    :   img/lcd x size

    <a id="_CPPv4N12dma2d_fill_t11frame_ysizeE"></a>

    <a id="_CPPv3N12dma2d_fill_t11frame_ysizeE"></a> <a id="_CPPv2N12dma2d_fill_t11frame_ysizeE"></a> <a id="dma2d_fill_t::frame_ysize__uint16_t"></a> <a id="structdma2d__fill__t_1a52168c4de9e2b10bf21c5b8b6c48864a"></a> uint16\_t frame\_ysize
    :   img/lcd y size

    <a id="_CPPv4N12dma2d_fill_t4xposE"></a>

    <a id="_CPPv3N12dma2d_fill_t4xposE"></a> <a id="_CPPv2N12dma2d_fill_t4xposE"></a> <a id="dma2d_fill_t::xpos__uint16_t"></a> <a id="structdma2d__fill__t_1a40ebf60e15548b9e0ea216cb357237bc"></a> uint16\_t xpos
    :   dma2d fill x pos based on frame\_xsize

    <a id="_CPPv4N12dma2d_fill_t4yposE"></a>

    <a id="_CPPv3N12dma2d_fill_t4yposE"></a> <a id="_CPPv2N12dma2d_fill_t4yposE"></a> <a id="dma2d_fill_t::ypos__uint16_t"></a> <a id="structdma2d__fill__t_1a66336b49301c678071cd60f5f1d69a8c"></a> uint16\_t ypos
    :   dma2d fill y pos based on frame\_ysize

    <a id="_CPPv4N12dma2d_fill_t5widthE"></a>

    <a id="_CPPv3N12dma2d_fill_t5widthE"></a> <a id="_CPPv2N12dma2d_fill_t5widthE"></a> <a id="dma2d_fill_t::width__uint16_t"></a> <a id="structdma2d__fill__t_1a0153840d36aa4c6d9bf2282d97bf6617"></a> uint16\_t width
    :   dma2d fill width

    <a id="_CPPv4N12dma2d_fill_t6heightE"></a>

    <a id="_CPPv3N12dma2d_fill_t6heightE"></a> <a id="_CPPv2N12dma2d_fill_t6heightE"></a> <a id="dma2d_fill_t::height__uint16_t"></a> <a id="structdma2d__fill__t_1a6fbef130ccc7198ac9767a3787a73b00"></a> uint16\_t height
    :   dma2d fill height

    <a id="_CPPv4N12dma2d_fill_t5colorE"></a>

    <a id="_CPPv3N12dma2d_fill_t5colorE"></a> <a id="_CPPv2N12dma2d_fill_t5colorE"></a> <a id="dma2d_fill_t::color__uint32_t"></a> <a id="structdma2d__fill__t_1ae2e444bedb25c6be8f48020d5f73207b"></a> uint32\_t color
    :   dma2d fill color , if YUV datat fill , should fill RGB888 color data

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_DMA2D_NOT_INIT"></a>

<a id="dma2d__types_8h_1a51a646536850bff5b450f8cdc74c281f"></a> BK\_ERR\_DMA2D\_NOT\_INIT
:   dma2d macos define

    LCD driver not init

<a id="c.USE_HAL_DMA2D_REGISTER_CALLBACKS"></a>

<a id="dma2d__types_8h_1ad3fd64734f71ef9c872f38dd0d0b8cb0"></a> USE\_HAL\_DMA2D\_REGISTER\_CALLBACKS
:   if use int type isr register, set this value 1\. always use with API @refs bk\_dma2d\_register\_int\_callback\_isr

<a id="c.COLOR_BLACK"></a>

<a id="dma2d__types_8h_1aba2a7fe77a7501e5844370eec0185207"></a> COLOR\_BLACK

<a id="c.COLOR_NAVY"></a>

<a id="dma2d__types_8h_1ac353684a9f431de76b1ea9443265d917"></a> COLOR\_NAVY

<a id="c.COLOR_DARKGREEN"></a>

<a id="dma2d__types_8h_1a60f33bc1f24aede8bbf12d47f90f982e"></a> COLOR\_DARKGREEN

<a id="c.COLOR_DARKCYAN"></a>

<a id="dma2d__types_8h_1acf2525b31291a9f1e17788dc0ac2e4e2"></a> COLOR\_DARKCYAN

<a id="c.COLOR_MAROON"></a>

<a id="dma2d__types_8h_1abc11c9ea14211945d71a0bea2e05c597"></a> COLOR\_MAROON

<a id="c.COLOR_PURPLE"></a>

<a id="dma2d__types_8h_1a361bd41194ac13caf9169f3f689dc179"></a> COLOR\_PURPLE

<a id="c.COLOR_OLIVE"></a>

<a id="dma2d__types_8h_1a3d28ef5dfbf3f7af50d52bff322a6c01"></a> COLOR\_OLIVE

<a id="c.COLOR_LIGHTGREY"></a>

<a id="dma2d__types_8h_1a2b8184cd58de122a35084154c001aef0"></a> COLOR\_LIGHTGREY

<a id="c.COLOR_DARKGREY"></a>

<a id="dma2d__types_8h_1a4ebd2c7b809dfb04565bd99ff6029c08"></a> COLOR\_DARKGREY

<a id="c.COLOR_BLUE"></a>

<a id="dma2d__types_8h_1a23c70d699a5a775bc2e1ebeb8603f630"></a> COLOR\_BLUE

<a id="c.COLOR_GREEN"></a>

<a id="dma2d__types_8h_1afc9149f5de51bd9ac4f5ebbfa153f018"></a> COLOR\_GREEN

<a id="c.COLOR_CYAN"></a>

<a id="dma2d__types_8h_1a82573859711fce56f1aa0a76b18a9b18"></a> COLOR\_CYAN

<a id="c.COLOR_RED"></a>

<a id="dma2d__types_8h_1ad86358bf19927183dd7b4ae215a29731"></a> COLOR\_RED

<a id="c.COLOR_MAGENTA"></a>

<a id="dma2d__types_8h_1a8deb0beccea721b35bdb1b4f7264fe75"></a> COLOR\_MAGENTA

<a id="c.COLOR_YELLOW"></a>

<a id="dma2d__types_8h_1a4534b577b74a58b0f4b7be027af664e0"></a> COLOR\_YELLOW

<a id="c.COLOR_WHITE"></a>

<a id="dma2d__types_8h_1a9b44987ffdc2af19b635206b94334b69"></a> COLOR\_WHITE

<a id="c.COLOR_ORANGE"></a>

<a id="dma2d__types_8h_1aef75f616b9a3fdb10d38395dfb996873"></a> COLOR\_ORANGE

<a id="c.COLOR_GREENYELLOW"></a>

<a id="dma2d__types_8h_1af44aaf067cf7d36a10185c238e54e43c"></a> COLOR\_GREENYELLOW

<a id="c.COLOR_PINK"></a>

<a id="dma2d__types_8h_1adc400e6efc54843fb9400270bbc61368"></a> COLOR\_PINK

<a id="c.COLOR_SILVER"></a>

<a id="dma2d__types_8h_1a222ba410c8d99aaacadef5ecd4d7952e"></a> COLOR\_SILVER

<a id="c.COLOR_GRAY"></a>

<a id="dma2d__types_8h_1a3aaf3b0287d26dfb6ecb3b1c46e950c8"></a> COLOR\_GRAY

<a id="c.COLOR_LIME"></a>

<a id="dma2d__types_8h_1aa817719ae6665a0e4e0862eb45ea2a0d"></a> COLOR\_LIME

<a id="c.COLOR_TEAL"></a>

<a id="dma2d__types_8h_1a4b267232e4d63357f019b51df51eaef2"></a> COLOR\_TEAL

<a id="c.COLOR_FUCHSIA"></a>

<a id="dma2d__types_8h_1afd03a600e34232de72c0dac0792d3770"></a> COLOR\_FUCHSIA

<a id="c.COLOR_ESP_BKGD"></a>

<a id="dma2d__types_8h_1af53f8b0bdde13070b950a94e3d114527"></a> COLOR\_ESP\_BKGD

<a id="c.DMA2D_OCOLR_BLUE_1"></a>

<a id="dma2d__types_8h_1a164c96762ec6cbaac2bff45dd84b97cf"></a> DMA2D\_OCOLR\_BLUE\_1
:   define Mode\_ARGB8888/RGB888 Blue Value

<a id="c.DMA2D_OCOLR_GREEN_1"></a>

<a id="dma2d__types_8h_1a8545d0dcde8b511d0ec64eb0c338fe2c"></a> DMA2D\_OCOLR\_GREEN\_1
:   define Mode\_ARGB8888/RGB888 Green Value

<a id="c.DMA2D_OCOLR_RED_1"></a>

<a id="dma2d__types_8h_1ad3928724c5937ffda60f29f272dda4fc"></a> DMA2D\_OCOLR\_RED\_1
:   define Mode\_ARGB8888/RGB888 Red Value

<a id="c.DMA2D_OCOLR_YELLOW_1"></a>

<a id="dma2d__types_8h_1ad2a37df334a031ee85dacdf336e1ce68"></a> DMA2D\_OCOLR\_YELLOW\_1
:   define Mode\_ARGB8888/RGB888 yellow Value

<a id="c.DMA2D_OCOLR_ALPHA_1"></a>

<a id="dma2d__types_8h_1aaada795f8e861c5a220054e78c31c512"></a> DMA2D\_OCOLR\_ALPHA\_1
:   define Mode\_ARGB8888/RGB888Alpha Channel Value

<a id="c.DMA2D_OCOLR_BLUE_3"></a>

<a id="dma2d__types_8h_1a0aa0634e409fb6d9fc68ecf9533c8d9c"></a> DMA2D\_OCOLR\_BLUE\_3
:   define Mode\_ARGB1555 Blue Value

<a id="c.DMA2D_OCOLR_GREEN_3"></a>

<a id="dma2d__types_8h_1acf4c97dc43e39e09956c2f4d8e092d17"></a> DMA2D\_OCOLR\_GREEN\_3
:   define Mode\_ARGB1555Green Value

<a id="c.DMA2D_OCOLR_RED_3"></a>

<a id="dma2d__types_8h_1aea63157a41a08d213f6cb8395373b385"></a> DMA2D\_OCOLR\_RED\_3
:   define Mode\_ARGB1555 Red Value

<a id="c.DMA2D_OCOLR_ALPHA_3"></a>

<a id="dma2d__types_8h_1abc0bf21946366343cedce1a2e9b07259"></a> DMA2D\_OCOLR\_ALPHA\_3
:   define Mode\_ARGB1555 Alpha Channel Value

<a id="c.DMA2D_OCOLR_BLUE_4"></a>

<a id="dma2d__types_8h_1add2439915c875a33bf9119382276cb89"></a> DMA2D\_OCOLR\_BLUE\_4
:   define Mode\_ARGB4444 Blue Value

<a id="c.DMA2D_OCOLR_GREEN_4"></a>

<a id="dma2d__types_8h_1a801078def8b64717b6fa0688483e3b78"></a> DMA2D\_OCOLR\_GREEN\_4
:   define Mode\_ARGB4444 Green Value

<a id="c.DMA2D_OCOLR_RED_4"></a>

<a id="dma2d__types_8h_1a3dd8ba291eeaec6bdf282570dc94699f"></a> DMA2D\_OCOLR\_RED\_4
:   define Mode\_ARGB4444 Red Value

<a id="c.DMA2D_OCOLR_ALPHA_4"></a>

<a id="dma2d__types_8h_1ab0b00eb37c77d6852cfbb731b603a9d5"></a> DMA2D\_OCOLR\_ALPHA\_4
:   define Mode\_ARGB4444 Alpha Channel Value

<a id="c.DMA2D_BACKGROUND_LAYER"></a>

<a id="dma2d__types_8h_1a62a5bfb546997e74c4171bcda44e70c5"></a> DMA2D\_BACKGROUND\_LAYER
:   DMA2D Background Layer (layer 0\)

<a id="c.DMA2D_FOREGROUND_LAYER"></a>

<a id="dma2d__types_8h_1a1a0116b4054c07eb00609bfdb2b06716"></a> DMA2D\_FOREGROUND\_LAYER
:   DMA2D Foreground Layer (layer 1\)

<a id="c.MAX_DMA2D_LAYER"></a>

<a id="dma2d__types_8h_1a1f76fcd25373b98c2ddd245de4a9c7bd"></a> MAX\_DMA2D\_LAYER
:   DMA2D maximum number of layers

<a id="c.DMA2D_REGULAR_ALPHA"></a>

<a id="dma2d__types_8h_1a727afc37b9c65346f5bb0bcdfedbb0be"></a> DMA2D\_REGULAR\_ALPHA
:   No modification of the alpha channel value

<a id="c.DMA2D_INVERTED_ALPHA"></a>

<a id="dma2d__types_8h_1aafd4c3a0adaf2f8a925c3059ead37f7c"></a> DMA2D\_INVERTED\_ALPHA
:   Invert the alpha channel value

<a id="c.DMA2D_NO_REVERSE"></a>

<a id="dma2d__types_8h_1a1ab50a0a62ff833b33ee035980275677"></a> DMA2D\_NO\_REVERSE
:   dma2d in/out put data in order not flip

<a id="c.DMA2D_BYTE_REVERSE"></a>

<a id="dma2d__types_8h_1ab38287212f2740e7ae666f19de75290f"></a> DMA2D\_BYTE\_REVERSE
:   input/output data reerse byte by byte for 32 bits color of YUV

<a id="c.DMA2D_HFWORD_REVERSE"></a>

<a id="dma2d__types_8h_1ad87026afd1f4d6ad57be770afc873fdc"></a> DMA2D\_HFWORD\_REVERSE
:   input/output data reerse half-word by half-word for 32 bits color of YUV

<a id="id7"></a>

### Type Definitions

<a id="_CPPv411dma2d_isr_t"></a>

<a id="_CPPv311dma2d_isr_t"></a> <a id="_CPPv211dma2d_isr_t"></a> <a id="dma2d_isr_t"></a> <a id="dma2d__types_8h_1a8b4f049df14c01ddc5c67948d779d549"></a> typedef void (\*dma2d\_isr\_t)(void \*args)

<a id="id8"></a>

### Enumerations

<a id="_CPPv413dm2d_isr_id_t"></a>

<a id="_CPPv313dm2d_isr_id_t"></a> <a id="_CPPv213dm2d_isr_id_t"></a> <a id="dma2d__types_8h_1abc05d8f28e027bd19161486b543bdbca"></a> enum dm2d\_isr\_id\_t
:   if USE\_HAL\_DMA2D\_REGISTER\_CALLBACKS \= 1, define int isr register id

    *Values:*

    <a id="_CPPv4N13dm2d_isr_id_t19DMA2D_CFG_ERROR_ISRE"></a>

    <a id="_CPPv3N13dm2d_isr_id_t19DMA2D_CFG_ERROR_ISRE"></a> <a id="_CPPv2N13dm2d_isr_id_t19DMA2D_CFG_ERROR_ISRE"></a> <a id="dma2d__types_8h_1abc05d8f28e027bd19161486b543bdbcaa2ade09af47d1b4080af5e6d94c1c360b"></a> enumerator DMA2D\_CFG\_ERROR\_ISR

    <a id="_CPPv4N13dm2d_isr_id_t29DMA2D_CLUT_TRANS_COMPLETE_ISRE"></a>

    <a id="_CPPv3N13dm2d_isr_id_t29DMA2D_CLUT_TRANS_COMPLETE_ISRE"></a> <a id="_CPPv2N13dm2d_isr_id_t29DMA2D_CLUT_TRANS_COMPLETE_ISRE"></a> <a id="dma2d__types_8h_1abc05d8f28e027bd19161486b543bdbcaa1ee51bce10ad0196ad8eeceb16324f0c"></a> enumerator DMA2D\_CLUT\_TRANS\_COMPLETE\_ISR

    <a id="_CPPv4N13dm2d_isr_id_t26DMA2D_CLUT_TRANS_ERROR_ISRE"></a>

    <a id="_CPPv3N13dm2d_isr_id_t26DMA2D_CLUT_TRANS_ERROR_ISRE"></a> <a id="_CPPv2N13dm2d_isr_id_t26DMA2D_CLUT_TRANS_ERROR_ISRE"></a> <a id="dma2d__types_8h_1abc05d8f28e027bd19161486b543bdbcaa3abda4ecd3cff1b2c82cd58ec6598b79"></a> enumerator DMA2D\_CLUT\_TRANS\_ERROR\_ISR

    <a id="_CPPv4N13dm2d_isr_id_t24DMA2D_WARTERMARK_INT_ISRE"></a>

    <a id="_CPPv3N13dm2d_isr_id_t24DMA2D_WARTERMARK_INT_ISRE"></a> <a id="_CPPv2N13dm2d_isr_id_t24DMA2D_WARTERMARK_INT_ISRE"></a> <a id="dma2d__types_8h_1abc05d8f28e027bd19161486b543bdbcaa890946575e171c1825bf94a0b45d2947"></a> enumerator DMA2D\_WARTERMARK\_INT\_ISR

    <a id="_CPPv4N13dm2d_isr_id_t24DMA2D_TRANS_COMPLETE_ISRE"></a>

    <a id="_CPPv3N13dm2d_isr_id_t24DMA2D_TRANS_COMPLETE_ISRE"></a> <a id="_CPPv2N13dm2d_isr_id_t24DMA2D_TRANS_COMPLETE_ISRE"></a> <a id="dma2d__types_8h_1abc05d8f28e027bd19161486b543bdbcaae3ee8176e5b7e0c25c2073d1bd5a1c92"></a> enumerator DMA2D\_TRANS\_COMPLETE\_ISR

    <a id="_CPPv4N13dm2d_isr_id_t21DMA2D_TRANS_ERROR_ISRE"></a>

    <a id="_CPPv3N13dm2d_isr_id_t21DMA2D_TRANS_ERROR_ISRE"></a> <a id="_CPPv2N13dm2d_isr_id_t21DMA2D_TRANS_ERROR_ISRE"></a> <a id="dma2d__types_8h_1abc05d8f28e027bd19161486b543bdbcaa83cf266c2c127cf8b2fbbd52dfcde596"></a> enumerator DMA2D\_TRANS\_ERROR\_ISR

    <a id="_CPPv4N13dm2d_isr_id_t13DMA2D_ISR_NUME"></a>

    <a id="_CPPv3N13dm2d_isr_id_t13DMA2D_ISR_NUME"></a> <a id="_CPPv2N13dm2d_isr_id_t13DMA2D_ISR_NUME"></a> <a id="dma2d__types_8h_1abc05d8f28e027bd19161486b543bdbcaad78200b0a6cdf1eb597415a5048814b5"></a> enumerator DMA2D\_ISR\_NUM

<a id="_CPPv412dma2d_mode_t"></a>

<a id="_CPPv312dma2d_mode_t"></a> <a id="_CPPv212dma2d_mode_t"></a> <a id="dma2d__types_8h_1a2281f69de0c11a61edada2a9aed202b5"></a> enum dma2d\_mode\_t
:   DMA2D enum defines.

    DMA2D\_Mode

    *Values:*

    <a id="_CPPv4N12dma2d_mode_t9DMA2D_M2ME"></a>

    <a id="_CPPv3N12dma2d_mode_t9DMA2D_M2ME"></a> <a id="_CPPv2N12dma2d_mode_t9DMA2D_M2ME"></a> <a id="dma2d__types_8h_1a2281f69de0c11a61edada2a9aed202b5ab4c23b4221ad43235a0251e1c0ace8b4"></a> enumerator DMA2D\_M2M
    :   DMA2D memory to memory transfer mode

    <a id="_CPPv4N12dma2d_mode_t13DMA2D_M2M_PFCE"></a>

    <a id="_CPPv3N12dma2d_mode_t13DMA2D_M2M_PFCE"></a> <a id="_CPPv2N12dma2d_mode_t13DMA2D_M2M_PFCE"></a> <a id="dma2d__types_8h_1a2281f69de0c11a61edada2a9aed202b5af455e3664ff46d21b0140517b5117e09"></a> enumerator DMA2D\_M2M\_PFC
    :   DMA2D memory to memory with pixel format conversion transfer mode

    <a id="_CPPv4N12dma2d_mode_t15DMA2D_M2M_BLENDE"></a>

    <a id="_CPPv3N12dma2d_mode_t15DMA2D_M2M_BLENDE"></a> <a id="_CPPv2N12dma2d_mode_t15DMA2D_M2M_BLENDE"></a> <a id="dma2d__types_8h_1a2281f69de0c11a61edada2a9aed202b5aefeff04036abac70f74b476e4be9db39"></a> enumerator DMA2D\_M2M\_BLEND
    :   DMA2D memory to memory with blending transfer mode

    <a id="_CPPv4N12dma2d_mode_t9DMA2D_R2ME"></a>

    <a id="_CPPv3N12dma2d_mode_t9DMA2D_R2ME"></a> <a id="_CPPv2N12dma2d_mode_t9DMA2D_R2ME"></a> <a id="dma2d__types_8h_1a2281f69de0c11a61edada2a9aed202b5a224cd974482f6059b0d53952b09d8b81"></a> enumerator DMA2D\_R2M
    :   DMA2D register to memory transfer mode

    <a id="_CPPv4N12dma2d_mode_t18DMA2D_M2M_BLEND_FGE"></a>

    <a id="_CPPv3N12dma2d_mode_t18DMA2D_M2M_BLEND_FGE"></a> <a id="_CPPv2N12dma2d_mode_t18DMA2D_M2M_BLEND_FGE"></a> <a id="dma2d__types_8h_1a2281f69de0c11a61edada2a9aed202b5a25316c91e294f4769f6f0ff1a83c79b6"></a> enumerator DMA2D\_M2M\_BLEND\_FG
    :   DMA2D memory to memory with blending transfer mode and fixed color FG

    <a id="_CPPv4N12dma2d_mode_t18DMA2D_M2M_BLEND_BGE"></a>

    <a id="_CPPv3N12dma2d_mode_t18DMA2D_M2M_BLEND_BGE"></a> <a id="_CPPv2N12dma2d_mode_t18DMA2D_M2M_BLEND_BGE"></a> <a id="dma2d__types_8h_1a2281f69de0c11a61edada2a9aed202b5adb4f2ca3726d9535653efbb3d950ef8d"></a> enumerator DMA2D\_M2M\_BLEND\_BG
    :   DMA2D memory to memory with blending transfer mode and fixed color BG

<a id="_CPPv414data_reverse_t"></a>

<a id="_CPPv314data_reverse_t"></a> <a id="_CPPv214data_reverse_t"></a> <a id="dma2d__types_8h_1a63b4399011f34b19aa43d1bc62673bbc"></a> enum data\_reverse\_t
:   *Values:*

    <a id="_CPPv4N14data_reverse_t10NO_REVERSEE"></a>

    <a id="_CPPv3N14data_reverse_t10NO_REVERSEE"></a> <a id="_CPPv2N14data_reverse_t10NO_REVERSEE"></a> <a id="dma2d__types_8h_1a63b4399011f34b19aa43d1bc62673bbcad9e8b8eb800a7a9f3282273f61987e00"></a> enumerator NO\_REVERSE
    :   in output 32bit color(yuv) formart, not reverse data byte by byte

    <a id="_CPPv4N14data_reverse_t20BYTE_BY_BYTE_REVERSEE"></a>

    <a id="_CPPv3N14data_reverse_t20BYTE_BY_BYTE_REVERSEE"></a> <a id="_CPPv2N14data_reverse_t20BYTE_BY_BYTE_REVERSEE"></a> <a id="dma2d__types_8h_1a63b4399011f34b19aa43d1bc62673bbca8f0362fa635f2a631203bb306220964c"></a> enumerator BYTE\_BY\_BYTE\_REVERSE
    :   in output 32bit color(yuv) formart, reverse data byte by byte

    <a id="_CPPv4N14data_reverse_t24HFWORD_BY_HFWORD_REVERSEE"></a>

    <a id="_CPPv3N14data_reverse_t24HFWORD_BY_HFWORD_REVERSEE"></a> <a id="_CPPv2N14data_reverse_t24HFWORD_BY_HFWORD_REVERSEE"></a> <a id="dma2d__types_8h_1a63b4399011f34b19aa43d1bc62673bbcafa57674ca40c7d7d625f806288223897"></a> enumerator HFWORD\_BY\_HFWORD\_REVERSE
    :   in output 32bit color(yuv) formart, reverse data byte by byte

<a id="_CPPv416out_color_mode_t"></a>

<a id="_CPPv316out_color_mode_t"></a> <a id="_CPPv216out_color_mode_t"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7"></a> enum out\_color\_mode\_t
:   DMA2D\_Output\_Color\_Mode , used for fillfmt / memcpy dst fmt/ blend output fmt

    *Values:*

    <a id="_CPPv4N16out_color_mode_t21DMA2D_OUTPUT_ARGB8888E"></a>

    <a id="_CPPv3N16out_color_mode_t21DMA2D_OUTPUT_ARGB8888E"></a> <a id="_CPPv2N16out_color_mode_t21DMA2D_OUTPUT_ARGB8888E"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7a8c8e4c059ec93d76aeba77b3ab2e1263"></a> enumerator DMA2D\_OUTPUT\_ARGB8888
    :   ARGB8888 DMA2D color mode

    <a id="_CPPv4N16out_color_mode_t19DMA2D_OUTPUT_RGB888E"></a>

    <a id="_CPPv3N16out_color_mode_t19DMA2D_OUTPUT_RGB888E"></a> <a id="_CPPv2N16out_color_mode_t19DMA2D_OUTPUT_RGB888E"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7ac4640719178927386325412a7e652ab6"></a> enumerator DMA2D\_OUTPUT\_RGB888
    :   RGB888 DMA2D color mode

    <a id="_CPPv4N16out_color_mode_t19DMA2D_OUTPUT_RGB565E"></a>

    <a id="_CPPv3N16out_color_mode_t19DMA2D_OUTPUT_RGB565E"></a> <a id="_CPPv2N16out_color_mode_t19DMA2D_OUTPUT_RGB565E"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7a3f88fe21358f8521c73193e01f9ea5ba"></a> enumerator DMA2D\_OUTPUT\_RGB565
    :   RGB565 DMA2D color mode

    <a id="_CPPv4N16out_color_mode_t21DMA2D_OUTPUT_ARGB1555E"></a>

    <a id="_CPPv3N16out_color_mode_t21DMA2D_OUTPUT_ARGB1555E"></a> <a id="_CPPv2N16out_color_mode_t21DMA2D_OUTPUT_ARGB1555E"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7a269775fb36b22a74db22dfc6365369bf"></a> enumerator DMA2D\_OUTPUT\_ARGB1555
    :   ARGB1555 DMA2D color mode

    <a id="_CPPv4N16out_color_mode_t21DMA2D_OUTPUT_ARGB4444E"></a>

    <a id="_CPPv3N16out_color_mode_t21DMA2D_OUTPUT_ARGB4444E"></a> <a id="_CPPv2N16out_color_mode_t21DMA2D_OUTPUT_ARGB4444E"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7acfab7422b5ad7376de6cb31e0db66b83"></a> enumerator DMA2D\_OUTPUT\_ARGB4444
    :   ARGB4444 DMA2D color mode

    <a id="_CPPv4N16out_color_mode_t17DMA2D_OUTPUT_YUYVE"></a>

    <a id="_CPPv3N16out_color_mode_t17DMA2D_OUTPUT_YUYVE"></a> <a id="_CPPv2N16out_color_mode_t17DMA2D_OUTPUT_YUYVE"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7abc8aed5ee408a33fb1cf4846a687aebb"></a> enumerator DMA2D\_OUTPUT\_YUYV

    <a id="_CPPv4N16out_color_mode_t17DMA2D_OUTPUT_UYVYE"></a>

    <a id="_CPPv3N16out_color_mode_t17DMA2D_OUTPUT_UYVYE"></a> <a id="_CPPv2N16out_color_mode_t17DMA2D_OUTPUT_UYVYE"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7a81824a044650bb18458823e2c9b156da"></a> enumerator DMA2D\_OUTPUT\_UYVY

    <a id="_CPPv4N16out_color_mode_t17DMA2D_OUTPUT_YYUVE"></a>

    <a id="_CPPv3N16out_color_mode_t17DMA2D_OUTPUT_YYUVE"></a> <a id="_CPPv2N16out_color_mode_t17DMA2D_OUTPUT_YYUVE"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7aad17c4da4ac18bcb6ccfb24abfd9412a"></a> enumerator DMA2D\_OUTPUT\_YYUV

    <a id="_CPPv4N16out_color_mode_t17DMA2D_OUTPUT_UVYYE"></a>

    <a id="_CPPv3N16out_color_mode_t17DMA2D_OUTPUT_UVYYE"></a> <a id="_CPPv2N16out_color_mode_t17DMA2D_OUTPUT_UVYYE"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7ab1607b8c1c605f37226b6541d1cf0511"></a> enumerator DMA2D\_OUTPUT\_UVYY

    <a id="_CPPv4N16out_color_mode_t17DMA2D_OUTPUT_VUYYE"></a>

    <a id="_CPPv3N16out_color_mode_t17DMA2D_OUTPUT_VUYYE"></a> <a id="_CPPv2N16out_color_mode_t17DMA2D_OUTPUT_VUYYE"></a> <a id="dma2d__types_8h_1a12dfb66554675f98f5a8c9223f5390d7ad962ea705561b4f2ba2a938e0fc2fb3e"></a> enumerator DMA2D\_OUTPUT\_VUYY

<a id="_CPPv418input_color_mode_t"></a>

<a id="_CPPv318input_color_mode_t"></a> <a id="_CPPv218input_color_mode_t"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793e"></a> enum input\_color\_mode\_t
:   DMA2D\_Input\_Color\_Mode, the members in order

    *Values:*

    <a id="_CPPv4N18input_color_mode_t20DMA2D_INPUT_ARGB8888E"></a>

    <a id="_CPPv3N18input_color_mode_t20DMA2D_INPUT_ARGB8888E"></a> <a id="_CPPv2N18input_color_mode_t20DMA2D_INPUT_ARGB8888E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea21ac464db71c078c0fec407396240e9d"></a> enumerator DMA2D\_INPUT\_ARGB8888
    :   ARGB8888 DMA2D color mode

    <a id="_CPPv4N18input_color_mode_t18DMA2D_INPUT_RGB888E"></a>

    <a id="_CPPv3N18input_color_mode_t18DMA2D_INPUT_RGB888E"></a> <a id="_CPPv2N18input_color_mode_t18DMA2D_INPUT_RGB888E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea6de0d3b45bb036eff87dfdfea70b6a56"></a> enumerator DMA2D\_INPUT\_RGB888
    :   RGB888 DMA2D color mode

    <a id="_CPPv4N18input_color_mode_t18DMA2D_INPUT_RGB565E"></a>

    <a id="_CPPv3N18input_color_mode_t18DMA2D_INPUT_RGB565E"></a> <a id="_CPPv2N18input_color_mode_t18DMA2D_INPUT_RGB565E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea9c5aad132a779d4d25c793c9b5284a5f"></a> enumerator DMA2D\_INPUT\_RGB565
    :   RGB565 DMA2D color mode

    <a id="_CPPv4N18input_color_mode_t20DMA2D_INPUT_ARGB1555E"></a>

    <a id="_CPPv3N18input_color_mode_t20DMA2D_INPUT_ARGB1555E"></a> <a id="_CPPv2N18input_color_mode_t20DMA2D_INPUT_ARGB1555E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ead26602d4750419bf0a4386e102311cf5"></a> enumerator DMA2D\_INPUT\_ARGB1555
    :   ARGB1555 DMA2D color mode

    <a id="_CPPv4N18input_color_mode_t20DMA2D_INPUT_ARGB4444E"></a>

    <a id="_CPPv3N18input_color_mode_t20DMA2D_INPUT_ARGB4444E"></a> <a id="_CPPv2N18input_color_mode_t20DMA2D_INPUT_ARGB4444E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea6845c5d28916eb38d7f1fc91875a2cbb"></a> enumerator DMA2D\_INPUT\_ARGB4444
    :   ARGB4444 DMA2D color mode

    <a id="_CPPv4N18input_color_mode_t14DMA2D_INPUT_L8E"></a>

    <a id="_CPPv3N18input_color_mode_t14DMA2D_INPUT_L8E"></a> <a id="_CPPv2N18input_color_mode_t14DMA2D_INPUT_L8E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea96791c6736d6ac30ac876fbe5e315eb6"></a> enumerator DMA2D\_INPUT\_L8

    <a id="_CPPv4N18input_color_mode_t16DMA2D_INPUT_AL44E"></a>

    <a id="_CPPv3N18input_color_mode_t16DMA2D_INPUT_AL44E"></a> <a id="_CPPv2N18input_color_mode_t16DMA2D_INPUT_AL44E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea537a233ec5470dc2ad69bde0415fabbc"></a> enumerator DMA2D\_INPUT\_AL44

    <a id="_CPPv4N18input_color_mode_t16DMA2D_INPUT_AL88E"></a>

    <a id="_CPPv3N18input_color_mode_t16DMA2D_INPUT_AL88E"></a> <a id="_CPPv2N18input_color_mode_t16DMA2D_INPUT_AL88E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea51cc30807bb6a1ee1ad2152e412083df"></a> enumerator DMA2D\_INPUT\_AL88

    <a id="_CPPv4N18input_color_mode_t14DMA2D_INPUT_L4E"></a>

    <a id="_CPPv3N18input_color_mode_t14DMA2D_INPUT_L4E"></a> <a id="_CPPv2N18input_color_mode_t14DMA2D_INPUT_L4E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea9db488b5acf1f7d10935c98177fbacad"></a> enumerator DMA2D\_INPUT\_L4

    <a id="_CPPv4N18input_color_mode_t14DMA2D_INPUT_A8E"></a>

    <a id="_CPPv3N18input_color_mode_t14DMA2D_INPUT_A8E"></a> <a id="_CPPv2N18input_color_mode_t14DMA2D_INPUT_A8E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea05c690235d572fddddc39fb2ec4e68f7"></a> enumerator DMA2D\_INPUT\_A8

    <a id="_CPPv4N18input_color_mode_t14DMA2D_INPUT_A4E"></a>

    <a id="_CPPv3N18input_color_mode_t14DMA2D_INPUT_A4E"></a> <a id="_CPPv2N18input_color_mode_t14DMA2D_INPUT_A4E"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea8f1993a03f955f004b175ac365fc8e50"></a> enumerator DMA2D\_INPUT\_A4

    <a id="_CPPv4N18input_color_mode_t16DMA2D_INPUT_YUYVE"></a>

    <a id="_CPPv3N18input_color_mode_t16DMA2D_INPUT_YUYVE"></a> <a id="_CPPv2N18input_color_mode_t16DMA2D_INPUT_YUYVE"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793eae017f4ff93c1f84317b4b6ea29f0003f"></a> enumerator DMA2D\_INPUT\_YUYV

    <a id="_CPPv4N18input_color_mode_t16DMA2D_INPUT_UYVYE"></a>

    <a id="_CPPv3N18input_color_mode_t16DMA2D_INPUT_UYVYE"></a> <a id="_CPPv2N18input_color_mode_t16DMA2D_INPUT_UYVYE"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea97dbfacd1e38f45159dd6f84edbff8b2"></a> enumerator DMA2D\_INPUT\_UYVY

    <a id="_CPPv4N18input_color_mode_t16DMA2D_INPUT_YYUVE"></a>

    <a id="_CPPv3N18input_color_mode_t16DMA2D_INPUT_YYUVE"></a> <a id="_CPPv2N18input_color_mode_t16DMA2D_INPUT_YYUVE"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea59c002ac655a3ed8555dcfec29f3a123"></a> enumerator DMA2D\_INPUT\_YYUV

    <a id="_CPPv4N18input_color_mode_t16DMA2D_INPUT_UVYYE"></a>

    <a id="_CPPv3N18input_color_mode_t16DMA2D_INPUT_UVYYE"></a> <a id="_CPPv2N18input_color_mode_t16DMA2D_INPUT_UVYYE"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793ea041524ed01e9cb09a8c6edff468b691b"></a> enumerator DMA2D\_INPUT\_UVYY

    <a id="_CPPv4N18input_color_mode_t16DMA2D_INPUT_VUYYE"></a>

    <a id="_CPPv3N18input_color_mode_t16DMA2D_INPUT_VUYYE"></a> <a id="_CPPv2N18input_color_mode_t16DMA2D_INPUT_VUYYE"></a> <a id="dma2d__types_8h_1a441ff49e3cfa3f19468412bea504793eabe67fe2d4e84b075a7d9b198571d0712"></a> enumerator DMA2D\_INPUT\_VUYY

<a id="_CPPv416dma2d_int_type_t"></a>

<a id="_CPPv316dma2d_int_type_t"></a> <a id="_CPPv216dma2d_int_type_t"></a> <a id="dma2d__types_8h_1a33c1eda950ec92bfc1b91cf3669e5762"></a> enum dma2d\_int\_type\_t
:   dma2d int type

    *Values:*

    <a id="_CPPv4N16dma2d_int_type_t15DMA2D_CFG_ERRORE"></a>

    <a id="_CPPv3N16dma2d_int_type_t15DMA2D_CFG_ERRORE"></a> <a id="_CPPv2N16dma2d_int_type_t15DMA2D_CFG_ERRORE"></a> <a id="dma2d__types_8h_1a33c1eda950ec92bfc1b91cf3669e5762a34e43318f2c7f4a8d627121c482ab1ec"></a> enumerator DMA2D\_CFG\_ERROR

    <a id="_CPPv4N16dma2d_int_type_t25DMA2D_CLUT_TRANS_COMPLETEE"></a>

    <a id="_CPPv3N16dma2d_int_type_t25DMA2D_CLUT_TRANS_COMPLETEE"></a> <a id="_CPPv2N16dma2d_int_type_t25DMA2D_CLUT_TRANS_COMPLETEE"></a> <a id="dma2d__types_8h_1a33c1eda950ec92bfc1b91cf3669e5762a7a063a54163156e5d69bbd2f541b8130"></a> enumerator DMA2D\_CLUT\_TRANS\_COMPLETE

    <a id="_CPPv4N16dma2d_int_type_t22DMA2D_CLUT_TRANS_ERRORE"></a>

    <a id="_CPPv3N16dma2d_int_type_t22DMA2D_CLUT_TRANS_ERRORE"></a> <a id="_CPPv2N16dma2d_int_type_t22DMA2D_CLUT_TRANS_ERRORE"></a> <a id="dma2d__types_8h_1a33c1eda950ec92bfc1b91cf3669e5762a8219ce7cc6e314e4f189cccbe09c44ff"></a> enumerator DMA2D\_CLUT\_TRANS\_ERROR

    <a id="_CPPv4N16dma2d_int_type_t20DMA2D_WARTERMARK_INTE"></a>

    <a id="_CPPv3N16dma2d_int_type_t20DMA2D_WARTERMARK_INTE"></a> <a id="_CPPv2N16dma2d_int_type_t20DMA2D_WARTERMARK_INTE"></a> <a id="dma2d__types_8h_1a33c1eda950ec92bfc1b91cf3669e5762a7b9dbb6138ec3e83e5f6bbe38b35fa76"></a> enumerator DMA2D\_WARTERMARK\_INT

    <a id="_CPPv4N16dma2d_int_type_t20DMA2D_TRANS_COMPLETEE"></a>

    <a id="_CPPv3N16dma2d_int_type_t20DMA2D_TRANS_COMPLETEE"></a> <a id="_CPPv2N16dma2d_int_type_t20DMA2D_TRANS_COMPLETEE"></a> <a id="dma2d__types_8h_1a33c1eda950ec92bfc1b91cf3669e5762a78650903c721e01829672ee824cc6157"></a> enumerator DMA2D\_TRANS\_COMPLETE

    <a id="_CPPv4N16dma2d_int_type_t17DMA2D_TRANS_ERRORE"></a>

    <a id="_CPPv3N16dma2d_int_type_t17DMA2D_TRANS_ERRORE"></a> <a id="_CPPv2N16dma2d_int_type_t17DMA2D_TRANS_ERRORE"></a> <a id="dma2d__types_8h_1a33c1eda950ec92bfc1b91cf3669e5762ace29072fa5692d0d883aada80f51be62"></a> enumerator DMA2D\_TRANS\_ERROR

    <a id="_CPPv4N16dma2d_int_type_t13DMA2D_ALL_INIE"></a>

    <a id="_CPPv3N16dma2d_int_type_t13DMA2D_ALL_INIE"></a> <a id="_CPPv2N16dma2d_int_type_t13DMA2D_ALL_INIE"></a> <a id="dma2d__types_8h_1a33c1eda950ec92bfc1b91cf3669e5762a318bdccd4e36d8990c94db36a5e2f254"></a> enumerator DMA2D\_ALL\_INI

<a id="_CPPv418dma2d_int_status_t"></a>

<a id="_CPPv318dma2d_int_status_t"></a> <a id="_CPPv218dma2d_int_status_t"></a> <a id="dma2d__types_8h_1a9447b8aeb2f86e30825a8f37565046ac"></a> enum dma2d\_int\_status\_t
:   dma2d int status

    *Values:*

    <a id="_CPPv4N18dma2d_int_status_t24DMA2D_TRANS_ERROR_STATUSE"></a>

    <a id="_CPPv3N18dma2d_int_status_t24DMA2D_TRANS_ERROR_STATUSE"></a> <a id="_CPPv2N18dma2d_int_status_t24DMA2D_TRANS_ERROR_STATUSE"></a> <a id="dma2d__types_8h_1a9447b8aeb2f86e30825a8f37565046aca383e4f485e63621f28745587f56625ac"></a> enumerator DMA2D\_TRANS\_ERROR\_STATUS

    <a id="_CPPv4N18dma2d_int_status_t27DMA2D_TRANS_COMPLETE_STATUSE"></a>

    <a id="_CPPv3N18dma2d_int_status_t27DMA2D_TRANS_COMPLETE_STATUSE"></a> <a id="_CPPv2N18dma2d_int_status_t27DMA2D_TRANS_COMPLETE_STATUSE"></a> <a id="dma2d__types_8h_1a9447b8aeb2f86e30825a8f37565046aca7b80f49b4d1095e325a76b45129124df"></a> enumerator DMA2D\_TRANS\_COMPLETE\_STATUS

    <a id="_CPPv4N18dma2d_int_status_t27DMA2D_WARTERMARK_INT_STATUSE"></a>

    <a id="_CPPv3N18dma2d_int_status_t27DMA2D_WARTERMARK_INT_STATUSE"></a> <a id="_CPPv2N18dma2d_int_status_t27DMA2D_WARTERMARK_INT_STATUSE"></a> <a id="dma2d__types_8h_1a9447b8aeb2f86e30825a8f37565046acacfe9e7092b029622687e02fa8b8e0ed6"></a> enumerator DMA2D\_WARTERMARK\_INT\_STATUS

    <a id="_CPPv4N18dma2d_int_status_t29DMA2D_CLUT_TRANS_ERROR_STATUSE"></a>

    <a id="_CPPv3N18dma2d_int_status_t29DMA2D_CLUT_TRANS_ERROR_STATUSE"></a> <a id="_CPPv2N18dma2d_int_status_t29DMA2D_CLUT_TRANS_ERROR_STATUSE"></a> <a id="dma2d__types_8h_1a9447b8aeb2f86e30825a8f37565046aca3e184134b1353ea3040065d4f9f25ac9"></a> enumerator DMA2D\_CLUT\_TRANS\_ERROR\_STATUS

    <a id="_CPPv4N18dma2d_int_status_t31DMA2D_CLUT_TRANS_COMPLETE_STATUE"></a>

    <a id="_CPPv3N18dma2d_int_status_t31DMA2D_CLUT_TRANS_COMPLETE_STATUE"></a> <a id="_CPPv2N18dma2d_int_status_t31DMA2D_CLUT_TRANS_COMPLETE_STATUE"></a> <a id="dma2d__types_8h_1a9447b8aeb2f86e30825a8f37565046aca9a646cda23e22e215a07d0a39750f3b0"></a> enumerator DMA2D\_CLUT\_TRANS\_COMPLETE\_STATU

    <a id="_CPPv4N18dma2d_int_status_t22DMA2D_CFG_ERROR_STATUSE"></a>

    <a id="_CPPv3N18dma2d_int_status_t22DMA2D_CFG_ERROR_STATUSE"></a> <a id="_CPPv2N18dma2d_int_status_t22DMA2D_CFG_ERROR_STATUSE"></a> <a id="dma2d__types_8h_1a9447b8aeb2f86e30825a8f37565046aca13f702c1c99f5e315695a9e98e030e3b"></a> enumerator DMA2D\_CFG\_ERROR\_STATUS

<a id="_CPPv421dma2d_trans_ability_t"></a>

<a id="_CPPv321dma2d_trans_ability_t"></a> <a id="_CPPv221dma2d_trans_ability_t"></a> <a id="dma2d__types_8h_1afa43bff619ad5dd629d5037302e1ff74"></a> enum dma2d\_trans\_ability\_t
:   *Values:*

    <a id="_CPPv4N21dma2d_trans_ability_t18MAX_TRANS_256BYTESE"></a>

    <a id="_CPPv3N21dma2d_trans_ability_t18MAX_TRANS_256BYTESE"></a> <a id="_CPPv2N21dma2d_trans_ability_t18MAX_TRANS_256BYTESE"></a> <a id="dma2d__types_8h_1afa43bff619ad5dd629d5037302e1ff74a4a34310917509c731191fa261f9f0da6"></a> enumerator MAX\_TRANS\_256BYTES

    <a id="_CPPv4N21dma2d_trans_ability_t14TRANS_128BYTESE"></a>

    <a id="_CPPv3N21dma2d_trans_ability_t14TRANS_128BYTESE"></a> <a id="_CPPv2N21dma2d_trans_ability_t14TRANS_128BYTESE"></a> <a id="dma2d__types_8h_1afa43bff619ad5dd629d5037302e1ff74a49b046d70041dc5036be0b23e70c2f46"></a> enumerator TRANS\_128BYTES

    <a id="_CPPv4N21dma2d_trans_ability_t13TRANS_64BYTESE"></a>

    <a id="_CPPv3N21dma2d_trans_ability_t13TRANS_64BYTESE"></a> <a id="_CPPv2N21dma2d_trans_ability_t13TRANS_64BYTESE"></a> <a id="dma2d__types_8h_1afa43bff619ad5dd629d5037302e1ff74a1baa4ef777ac4fc68537c11a224b97db"></a> enumerator TRANS\_64BYTES

    <a id="_CPPv4N21dma2d_trans_ability_t13TRANS_32BYTESE"></a>

    <a id="_CPPv3N21dma2d_trans_ability_t13TRANS_32BYTESE"></a> <a id="_CPPv2N21dma2d_trans_ability_t13TRANS_32BYTESE"></a> <a id="dma2d__types_8h_1afa43bff619ad5dd629d5037302e1ff74ac8ca6f77c11d1541c84ad00da7bcfcc5"></a> enumerator TRANS\_32BYTES

    <a id="_CPPv4N21dma2d_trans_ability_t13TRANS_16BYTESE"></a>

    <a id="_CPPv3N21dma2d_trans_ability_t13TRANS_16BYTESE"></a> <a id="_CPPv2N21dma2d_trans_ability_t13TRANS_16BYTESE"></a> <a id="dma2d__types_8h_1afa43bff619ad5dd629d5037302e1ff74ab57858b729a2a795fbbf523bd1d818cf"></a> enumerator TRANS\_16BYTES

<a id="_CPPv418blend_alpha_mode_t"></a>

<a id="_CPPv318blend_alpha_mode_t"></a> <a id="_CPPv218blend_alpha_mode_t"></a> <a id="dma2d__types_8h_1a174a9a6be32e0178d2ffbbdaab931834"></a> enum blend\_alpha\_mode\_t
:   *Values:*

    <a id="_CPPv4N18blend_alpha_mode_t20DMA2D_NO_MODIF_ALPHAE"></a>

    <a id="_CPPv3N18blend_alpha_mode_t20DMA2D_NO_MODIF_ALPHAE"></a> <a id="_CPPv2N18blend_alpha_mode_t20DMA2D_NO_MODIF_ALPHAE"></a> <a id="dma2d__types_8h_1a174a9a6be32e0178d2ffbbdaab931834a944e897f7c45ab32facc01d4375620cd"></a> enumerator DMA2D\_NO\_MODIF\_ALPHA

    <a id="_CPPv4N18blend_alpha_mode_t19DMA2D_REPLACE_ALPHAE"></a>

    <a id="_CPPv3N18blend_alpha_mode_t19DMA2D_REPLACE_ALPHAE"></a> <a id="_CPPv2N18blend_alpha_mode_t19DMA2D_REPLACE_ALPHAE"></a> <a id="dma2d__types_8h_1a174a9a6be32e0178d2ffbbdaab931834ab4278df22f0b7c1af037a778f8e0a190"></a> enumerator DMA2D\_REPLACE\_ALPHA

    <a id="_CPPv4N18blend_alpha_mode_t19DMA2D_COMBINE_ALPHAE"></a>

    <a id="_CPPv3N18blend_alpha_mode_t19DMA2D_COMBINE_ALPHAE"></a> <a id="_CPPv2N18blend_alpha_mode_t19DMA2D_COMBINE_ALPHAE"></a> <a id="dma2d__types_8h_1a174a9a6be32e0178d2ffbbdaab931834ae7704f5083ad09f46ff4f6de512e5c9a"></a> enumerator DMA2D\_COMBINE\_ALPHA

<a id="_CPPv415red_blue_swap_t"></a>

<a id="_CPPv315red_blue_swap_t"></a> <a id="_CPPv215red_blue_swap_t"></a> <a id="dma2d__types_8h_1ab9f0f0496be7caf3178f4bce151ef8b9"></a> enum red\_blue\_swap\_t
:   *Values:*

    <a id="_CPPv4N15red_blue_swap_t16DMA2D_RB_REGULARE"></a>

    <a id="_CPPv3N15red_blue_swap_t16DMA2D_RB_REGULARE"></a> <a id="_CPPv2N15red_blue_swap_t16DMA2D_RB_REGULARE"></a> <a id="dma2d__types_8h_1ab9f0f0496be7caf3178f4bce151ef8b9a681cedec1b226d7dd13a5380ef8f9bd1"></a> enumerator DMA2D\_RB\_REGULAR
    :   Select regular mode (RGB or ARGB)

    <a id="_CPPv4N15red_blue_swap_t13DMA2D_RB_SWAPE"></a>

    <a id="_CPPv3N15red_blue_swap_t13DMA2D_RB_SWAPE"></a> <a id="_CPPv2N15red_blue_swap_t13DMA2D_RB_SWAPE"></a> <a id="dma2d__types_8h_1ab9f0f0496be7caf3178f4bce151ef8b9a8c41084cb63c180c67254046c6d16931"></a> enumerator DMA2D\_RB\_SWAP
    :   Select swap mode (BGR or ABGR) \* \= 0

<a id="_CPPv413color_bytes_t"></a>

<a id="_CPPv313color_bytes_t"></a> <a id="_CPPv213color_bytes_t"></a> <a id="dma2d__types_8h_1adab734214366b31d83036a2d3549af05"></a> enum color\_bytes\_t
:   *Values:*

    <a id="_CPPv4N13color_bytes_t9TWO_BYTESE"></a>

    <a id="_CPPv3N13color_bytes_t9TWO_BYTESE"></a> <a id="_CPPv2N13color_bytes_t9TWO_BYTESE"></a> <a id="dma2d__types_8h_1adab734214366b31d83036a2d3549af05a3528c04355484cbd4eccb72eedbc39b4"></a> enumerator TWO\_BYTES

    <a id="_CPPv4N13color_bytes_t11THREE_BYTESE"></a>

    <a id="_CPPv3N13color_bytes_t11THREE_BYTESE"></a> <a id="_CPPv2N13color_bytes_t11THREE_BYTESE"></a> <a id="dma2d__types_8h_1adab734214366b31d83036a2d3549af05ada1aada2f7100abc69c7af969eee4653"></a> enumerator THREE\_BYTES

    <a id="_CPPv4N13color_bytes_t10FOUR_BYTESE"></a>

    <a id="_CPPv3N13color_bytes_t10FOUR_BYTESE"></a> <a id="_CPPv2N13color_bytes_t10FOUR_BYTESE"></a> <a id="dma2d__types_8h_1adab734214366b31d83036a2d3549af05a8fad8c5fadaf09d2c403930df2a71896"></a> enumerator FOUR\_BYTES
