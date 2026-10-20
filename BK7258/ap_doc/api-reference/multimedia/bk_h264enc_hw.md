---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_h264enc_hw.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="h264-enc"></a>

# H264\_ENC

<a id="h264-enc-api-status"></a>

## H264\_ENC API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_h264_driver_init()`](#_CPPv419bk_h264_driver_initv "bk_h264_driver_init") | Y |
| [`bk_h264_driver_deinit()`](#_CPPv421bk_h264_driver_deinitv "bk_h264_driver_deinit") | Y |
| [`bk_h264_init()`](#_CPPv412bk_h264_init8uint16_t8uint16_t "bk_h264_init") | Y |
| [`bk_h264_deinit()`](#_CPPv414bk_h264_deinitv "bk_h264_deinit") | Y |
| [`bk_h264_set_base_config()`](#_CPPv423bk_h264_set_base_configP21h264_compress_ratio_t "bk_h264_set_base_config") | Y |
| [`bk_h264_get_h264_base_config()`](#_CPPv428bk_h264_get_h264_base_configP18h264_base_config_t "bk_h264_get_h264_base_config") | Y |
| [`bk_h264_set_pframe_num()`](#_CPPv422bk_h264_set_pframe_num8uint32_t "bk_h264_set_pframe_num") | Y |
| [`bk_h264_get_pframe_num()`](#_CPPv422bk_h264_get_pframe_numv "bk_h264_get_pframe_num") | Y |
| [`bk_h264_set_qp()`](#_CPPv414bk_h264_set_qpP9h264_qp_t "bk_h264_set_qp") | Y |
| [`bk_h264_set_quality()`](#_CPPv419bk_h264_set_quality8uint32_t8uint32_t "bk_h264_set_quality") | Y |
| [`bk_h264_encode_enable()`](#_CPPv421bk_h264_encode_enablev "bk_h264_encode_enable") | Y |
| [`bk_h264_encode_disable()`](#_CPPv422bk_h264_encode_disablev "bk_h264_encode_disable") | Y |
| [`bk_h264_soft_reset()`](#_CPPv418bk_h264_soft_resetv "bk_h264_soft_reset") | Y |
| [`bk_h264_config_reset()`](#_CPPv420bk_h264_config_resetv "bk_h264_config_reset") | Y |
| [`bk_h264_get_fifo_addr()`](#_CPPv421bk_h264_get_fifo_addrP8uint32_t "bk_h264_get_fifo_addr") | Y |
| [`bk_h264_register_isr()`](#_CPPv420bk_h264_register_isr15h264_isr_type_t10h264_isr_tPv "bk_h264_register_isr") | Y |
| [`bk_h264_unregister_isr()`](#_CPPv422bk_h264_unregister_isr15h264_isr_type_t "bk_h264_unregister_isr") | Y |
| [`bk_h264_get_encode_count()`](#_CPPv424bk_h264_get_encode_countv "bk_h264_get_encode_count") | Y |
| [`bk_h264_enc_lcd_dma_cpy()`](#_CPPv423bk_h264_enc_lcd_dma_cpyPvPKv8uint32_t8dma_id_t "bk_h264_enc_lcd_dma_cpy") | Y |
| [`bk_h264_updata_encode_fps()`](#_CPPv425bk_h264_updata_encode_fps8uint32_t "bk_h264_updata_encode_fps") | Y |

<a id="h264-enc-marco-defined-and-config"></a>

## H264\_ENC Marco defined and config

| Marco name | illustrate |
| --- | --- |
| CONFIG\_H264 | enable H264\_ENC module or not |

备注

CONFIG\_H264 depends on CONFIG\_YUV\_BUF, H264 module can not work alone. Those api only for reference, user can not use them directly. Please referecnce doorbell project.

<a id="h264-enc-api-reference"></a>

## H264\_ENC API Reference

<a id="header-file"></a>

### Header File

- [h264.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/h264.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419bk_h264_driver_initv"></a>

<a id="_CPPv319bk_h264_driver_initv"></a> <a id="_CPPv219bk_h264_driver_initv"></a> <a id="bk_h264_driver_init__void"></a> <a id="h264_8h_1ab27a7cce86e01f88bac18c30ceff38da"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_driver\_init(void)
:   init h264 driver

    This API use to init h264 driver register and register system isr

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_h264_driver_deinitv"></a>

<a id="_CPPv321bk_h264_driver_deinitv"></a> <a id="_CPPv221bk_h264_driver_deinitv"></a> <a id="bk_h264_driver_deinit__void"></a> <a id="h264_8h_1a32cdc7dfa0a225b83c3ed0fbc703e87d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_driver\_deinit(void)
:   deinit h264 driver

    This API use to deinit h264 driver register and deregister system isr

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv412bk_h264_init8uint16_t8uint16_t"></a>

<a id="_CPPv312bk_h264_init8uint16_t8uint16_t"></a> <a id="_CPPv212bk_h264_init8uint16_t8uint16_t"></a> <a id="bk_h264_init__uint16_t.uint16_t"></a> <a id="h264_8h_1a6b6ed2e1b9f187782c3ce2154cf845e4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_init(uint16\_t width, uint16\_t height)
:   Init the h264 encoder.

    This API init the h264 encoder

    - vote cpu to 480MHz
    - vote video power on
    - set h264 clk enable
    - enable h264 system isr
    - according image resolution, config release register

    参数
    :   - **width** – input image width
        - **height** – input image height

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv414bk_h264_deinitv"></a>

<a id="_CPPv314bk_h264_deinitv"></a> <a id="_CPPv214bk_h264_deinitv"></a> <a id="bk_h264_deinit__void"></a> <a id="h264_8h_1a251c9c7ad9ca630879bf64f31c7c3372"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_deinit(void)
:   Deinitialize the H264 module.

    This API deinitialize the H264 module

    - vote cpu to default
    - vote video power off
    - disable h264 clk
    - disable h264 system isr

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv423bk_h264_set_base_configP21h264_compress_ratio_t"></a>

<a id="_CPPv323bk_h264_set_base_configP21h264_compress_ratio_t"></a> <a id="_CPPv223bk_h264_set_base_configP21h264_compress_ratio_t"></a> <a id="bk_h264_set_base_config__h264_compress_ratio_tP"></a> <a id="h264_8h_1a69052b84690d27a2fbd710428a9b564c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_set\_base\_config([h264\_compress\_ratio\_t](#_CPPv421h264_compress_ratio_t "h264_compress_ratio_t") \*config)
:   config h264 encode ratio

    This API modify h264 register to config encode ratio, you can call anytime

    参数
    :   **config** – compress ratio config

        - profile\_idc: profile idc
        - p\_frame\_cnt: p frame count
        - qp: qp
        - num\_imb\_bits: num imb bits
        - num\_pmb\_bits: num pmb bits

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv428bk_h264_get_h264_base_configP18h264_base_config_t"></a>

<a id="_CPPv328bk_h264_get_h264_base_configP18h264_base_config_t"></a> <a id="_CPPv228bk_h264_get_h264_base_configP18h264_base_config_t"></a> <a id="bk_h264_get_h264_base_config__h264_base_config_tP"></a> <a id="h264_8h_1ab79e0c2874712332a11a5adeecb219f7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_get\_h264\_base\_config([h264\_base\_config\_t](#_CPPv418h264_base_config_t "h264_base_config_t") \*config)
:   get h264 encode base config

    This API get h264 encode base config, you can call anytime

    参数
    :   **config** – h264 base config

        - profile\_idc: profile idc
        - p\_frame\_cnt: p frame count
        - qp: qp
        - num\_imb\_bits: num imb bits
        - num\_pmb\_bits: num pmb bits

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv422bk_h264_set_pframe_num8uint32_t"></a>

<a id="_CPPv322bk_h264_set_pframe_num8uint32_t"></a> <a id="_CPPv222bk_h264_set_pframe_num8uint32_t"></a> <a id="bk_h264_set_pframe_num__uint32_t"></a> <a id="h264_8h_1a5b068db2511801648ffca09e65b1f548"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_set\_pframe\_num(uint32\_t pframe\_number)
:   set h264 encode p frame count

    This API can set h264 encode p frame count

    **Attention**
    :   if you use h264 pipeline, suggest modify it by CONFIG\_H264\_P\_FRAME\_CNT

    参数
    :   **pframe\_number** – p frame number

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv422bk_h264_get_pframe_numv"></a>

<a id="_CPPv322bk_h264_get_pframe_numv"></a> <a id="_CPPv222bk_h264_get_pframe_numv"></a> <a id="bk_h264_get_pframe_num__void"></a> <a id="h264_8h_1a3a9ce94d13858d25fe0015f7f8ef502c"></a> uint32\_t bk\_h264\_get\_pframe\_num(void)
:   get h264 encode p frame count

    This API get h264 encode p frame count

    返回
    :   - p frame number

<a id="_CPPv414bk_h264_set_qpP9h264_qp_t"></a>

<a id="_CPPv314bk_h264_set_qpP9h264_qp_t"></a> <a id="_CPPv214bk_h264_set_qpP9h264_qp_t"></a> <a id="bk_h264_set_qp__h264_qp_tP"></a> <a id="h264_8h_1a294be58137fa23c950388e71ef1a96c3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_set\_qp([h264\_qp\_t](#_CPPv49h264_qp_t "h264_qp_t") \*qp)
:   set h264 encode qp

    This API can set h264 encode qp

    参数
    :   **qp** – qp config

        - qp: qp
        - num\_imb\_bits: num imb bits
        - num\_pmb\_bits: num pmb bits

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv419bk_h264_set_quality8uint32_t8uint32_t"></a>

<a id="_CPPv319bk_h264_set_quality8uint32_t8uint32_t"></a> <a id="_CPPv219bk_h264_set_quality8uint32_t8uint32_t"></a> <a id="bk_h264_set_quality__uint32_t.uint32_t"></a> <a id="h264_8h_1a4a3c77340359ef7739031465fc7faa52"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_set\_quality(uint32\_t imb\_bits, uint32\_t pmb\_bits)
:   set h264 encode qp

    This API can set h264 encode qp

    参数
    :   - **imb\_bits** – imb bits
        - **pmb\_bits** – pmb bits

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv421bk_h264_encode_enablev"></a>

<a id="_CPPv321bk_h264_encode_enablev"></a> <a id="_CPPv221bk_h264_encode_enablev"></a> <a id="bk_h264_encode_enable__void"></a> <a id="h264_8h_1aff868fec5fb3b9c9ae0ff54fbd7eec8a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_encode\_enable(void)
:   enable h264 encode

    This API enable h264 encode

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv422bk_h264_encode_disablev"></a>

<a id="_CPPv322bk_h264_encode_disablev"></a> <a id="_CPPv222bk_h264_encode_disablev"></a> <a id="bk_h264_encode_disable__void"></a> <a id="h264_8h_1ad553c0b9e1cee1879c1d88f00eeebf12"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_encode\_disable(void)
:   disable h264 encode

    This API disable h264 encode

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv418bk_h264_soft_resetv"></a>

<a id="_CPPv318bk_h264_soft_resetv"></a> <a id="_CPPv218bk_h264_soft_resetv"></a> <a id="bk_h264_soft_reset__void"></a> <a id="h264_8h_1a6b2a0b2e7b7652521d74423d550fdb59"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_soft\_reset(void)
:   soft reset h264

    This API soft reset h264, you can call this to reset encode logical, can regenrate idr frame

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv420bk_h264_config_resetv"></a>

<a id="_CPPv320bk_h264_config_resetv"></a> <a id="_CPPv220bk_h264_config_resetv"></a> <a id="bk_h264_config_reset__void"></a> <a id="h264_8h_1aa7785cd138baa730eb61af892b84324b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_config\_reset(void)
:   config reset h264 driver

    This API config reset h264 driver, reset all register to init status

    **Attention**
    :   this api will reconfig h264 all register

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv421bk_h264_get_fifo_addrP8uint32_t"></a>

<a id="_CPPv321bk_h264_get_fifo_addrP8uint32_t"></a> <a id="_CPPv221bk_h264_get_fifo_addrP8uint32_t"></a> <a id="bk_h264_get_fifo_addr__uint32_tP"></a> <a id="h264_8h_1a4286468830b43f19c937a37b3f8dd1b7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_get\_fifo\_addr(uint32\_t \*fifo\_addr)
:   get h264 encode fifo addr

    This API get h264 encode fifo addr

    参数
    :   **fifo\_addr** – h264 encode fifo addr

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv420bk_h264_register_isr15h264_isr_type_t10h264_isr_tPv"></a>

<a id="_CPPv320bk_h264_register_isr15h264_isr_type_t10h264_isr_tPv"></a> <a id="_CPPv220bk_h264_register_isr15h264_isr_type_t10h264_isr_tPv"></a> <a id="bk_h264_register_isr__h264_isr_type_t.h264_isr_t.voidP"></a> <a id="h264_8h_1a060b705d5cfb564f12cacf2fab632826"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_register\_isr([h264\_isr\_type\_t](#_CPPv415h264_isr_type_t "h264_isr_type_t") type\_id, [h264\_isr\_t](#_CPPv410h264_isr_t "h264_isr_t") isr, void \*param)
:   register h264 isr

    This API register h264 isr

    参数
    :   - **type\_id** – isr type
        - **isr** – isr callback function
        - **param** – isr param

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv422bk_h264_unregister_isr15h264_isr_type_t"></a>

<a id="_CPPv322bk_h264_unregister_isr15h264_isr_type_t"></a> <a id="_CPPv222bk_h264_unregister_isr15h264_isr_type_t"></a> <a id="bk_h264_unregister_isr__h264_isr_type_t"></a> <a id="h264_8h_1ad8cfcd7c1c9bf4b72981ab769e554cc7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_unregister\_isr([h264\_isr\_type\_t](#_CPPv415h264_isr_type_t "h264_isr_type_t") type\_id)
:   unregister h264 isr

    This API unregister h264 isr

    参数
    :   **type\_id** – isr type

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv424bk_h264_get_encode_countv"></a>

<a id="_CPPv324bk_h264_get_encode_countv"></a> <a id="_CPPv224bk_h264_get_encode_countv"></a> <a id="bk_h264_get_encode_count__void"></a> <a id="h264_8h_1a4906a55aaacac83d1cf1b5fb00aa3c47"></a> uint32\_t bk\_h264\_get\_encode\_count(void)
:   get h264 encode count

    This API get h264 encode count

    **Attention**
    :   output unit is word(4 bytes)

    返回
    :   - encode count

<a id="_CPPv423bk_h264_enc_lcd_dma_cpyPvPKv8uint32_t8dma_id_t"></a>

<a id="_CPPv323bk_h264_enc_lcd_dma_cpyPvPKv8uint32_t8dma_id_t"></a> <a id="_CPPv223bk_h264_enc_lcd_dma_cpyPvPKv8uint32_t8dma_id_t"></a> <a id="bk_h264_enc_lcd_dma_cpy__voidP.voidCP.uint32_t.dma_id_t"></a> <a id="h264_8h_1a25af08cdf2ea83c58594dcca11636ad4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_enc\_lcd\_dma\_cpy(void \*out, const void \*in, uint32\_t len, [dma\_id\_t](../peripheral/bk_dma.md#_CPPv48dma_id_t "dma_id_t") cpy\_chnl)
:   h264 encode lcd dma copy

    This API h264 encode lcd dma copy

    参数
    :   - **out** – output addr
        - **in** – input addr
        - **len** – copy len
        - **cpy\_chnl** – dma channel

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv425bk_h264_updata_encode_fps8uint32_t"></a>

<a id="_CPPv325bk_h264_updata_encode_fps8uint32_t"></a> <a id="_CPPv225bk_h264_updata_encode_fps8uint32_t"></a> <a id="bk_h264_updata_encode_fps__uint32_t"></a> <a id="h264_8h_1a0defb614b9173d65a59694feac700c2a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_updata\_encode\_fps(uint32\_t fps)
:   h264 updata encode fps

    This API h264 updata encode fps, this fps will release h264 decode fps

    参数
    :   **fps** – fps

    返回
    :   - BK\_OK: Success
        - others: Other errors

<a id="_CPPv425bk_h264_global_soft_reset7uint8_t"></a>

<a id="_CPPv325bk_h264_global_soft_reset7uint8_t"></a> <a id="_CPPv225bk_h264_global_soft_reset7uint8_t"></a> <a id="bk_h264_global_soft_reset__uint8_t"></a> <a id="h264_8h_1a9a4ef933e6d03719f9d132a5eee7c9a6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_h264\_global\_soft\_reset(uint8\_t enable)
:   h264 module global softreset

    This API will use for resetting h264 module

    @attenation this api must be called twice to complete the reset: first enable(1), then disable(0)

    参数
    :   **enable** – 0:disable, 1:enable

    返回
    :   - BK\_OK: Success
        - others: Other errors.

<a id="h264-enc-api-typedefs"></a>

## H264\_ENC API Typedefs

<a id="id1"></a>

### Header File

- [h264\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/h264_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv418h264_base_config_t"></a>

<a id="_CPPv318h264_base_config_t"></a> <a id="_CPPv218h264_base_config_t"></a> <a id="h264_base_config_t"></a> <a id="structh264__base__config__t"></a> struct h264\_base\_config\_t

<a id="_CPPv421h264_compress_ratio_t"></a>

<a id="_CPPv321h264_compress_ratio_t"></a> <a id="_CPPv221h264_compress_ratio_t"></a> <a id="h264_compress_ratio_t"></a> <a id="structh264__compress__ratio__t"></a> struct h264\_compress\_ratio\_t

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_H264_DRIVER_NOT_INIT"></a>

<a id="h264__types_8h_1a38ab4344a91d556895b8cba7f545d565"></a> BK\_ERR\_H264\_DRIVER\_NOT\_INIT

<a id="c.BK_ERR_H264_ISR_INVALID_ID"></a>

<a id="h264__types_8h_1af58d1c9b6bdd74c8780e8d0bcdd223ee"></a> BK\_ERR\_H264\_ISR\_INVALID\_ID

<a id="c.BK_ERR_H264_INVALID_RESOLUTION_TYPE"></a>

<a id="h264__types_8h_1a38762a2215cde5f64128386fafd612af"></a> BK\_ERR\_H264\_INVALID\_RESOLUTION\_TYPE

<a id="c.BK_ERR_H264_INVALID_PFRAME_NUMBER"></a>

<a id="h264__types_8h_1a1fd7134c1fe38786c3ed8d9c4697a6b6"></a> BK\_ERR\_H264\_INVALID\_PFRAME\_NUMBER

<a id="c.BK_ERR_H264_INVALID_QP"></a>

<a id="h264__types_8h_1ab616d7dbb1f6bcda53bb3a66779b5541"></a> BK\_ERR\_H264\_INVALID\_QP

<a id="c.BK_ERR_H264_INVALID_IMB_BITS"></a>

<a id="h264__types_8h_1ab51457426c2bb99348f9396abb2b10ec"></a> BK\_ERR\_H264\_INVALID\_IMB\_BITS

<a id="c.BK_ERR_H264_INVALID_PMB_BITS"></a>

<a id="h264__types_8h_1aa5fb3e27ef9e9db4e47d6b18324ee0fd"></a> BK\_ERR\_H264\_INVALID\_PMB\_BITS

<a id="c.BK_ERR_H264_INVALID_CONFIG_PARAM"></a>

<a id="h264__types_8h_1ab5f297968c9fa52d6f99b99de71a456a"></a> BK\_ERR\_H264\_INVALID\_CONFIG\_PARAM

<a id="c.BK_ERR_H264_INVALID_PIXEL_HEIGHT"></a>

<a id="h264__types_8h_1a957a5d56d7ee82f2df6284eafd877624"></a> BK\_ERR\_H264\_INVALID\_PIXEL\_HEIGHT

<a id="c.INT_SKIP_FRAME"></a>

<a id="h264__types_8h_1af927e6dd578659155cf18ecd00d9c5de"></a> INT\_SKIP\_FRAME

<a id="c.INT_FINAL_OUT"></a>

<a id="h264__types_8h_1a3a1adbb8d97d99bdcbe3a66bd8e568a0"></a> INT\_FINAL\_OUT

<a id="c.INT_LINE_DONE"></a>

<a id="h264__types_8h_1a90d9d6e6e82661b708540bcc8d17504a"></a> INT\_LINE\_DONE

<a id="c.H264_CLK_SEL_480M"></a>

<a id="h264__types_8h_1a4ec51c4097ee0086b14c682259663d3f"></a> H264\_CLK\_SEL\_480M

<a id="c.H264_AHB_CLK_DIV"></a>

<a id="h264__types_8h_1ad42a0c2396748af3c8898593c44f3bfa"></a> H264\_AHB\_CLK\_DIV

<a id="c.H264_AHB_CLK_SEL"></a>

<a id="h264__types_8h_1a5468e34219390f4bc2c0406464621168"></a> H264\_AHB\_CLK\_SEL

<a id="c.H264_INT_ENABLE"></a>

<a id="h264__types_8h_1ac23a65dde0fdc8019cb6645089c2d8c5"></a> H264\_INT\_ENABLE

<a id="c.H264_INT_DISABLE"></a>

<a id="h264__types_8h_1a630c0cce4f9e4a8b5235c2ba777a9daa"></a> H264\_INT\_DISABLE

<a id="c.MAX_QP"></a>

<a id="h264__types_8h_1a36731cc1007cd643f55b66d1f573d659"></a> MAX\_QP

<a id="c.MIN_QP"></a>

<a id="h264__types_8h_1adeb82eed4379b9031106339f3db02e8e"></a> MIN\_QP

<a id="c.MAX_PFRAME"></a>

<a id="h264__types_8h_1a865ccd290d0204d08c564fe4375da8ee"></a> MAX\_PFRAME

<a id="c.MIN_PFRAME"></a>

<a id="h264__types_8h_1a229a0f1411d01f2e79bd7b0e87a2a9a4"></a> MIN\_PFRAME

<a id="c.MAX_IFRAME_BITS"></a>

<a id="h264__types_8h_1af8eb27660f9ab8e1b3945cce3b1f93a6"></a> MAX\_IFRAME\_BITS

<a id="c.MAX_PFRAME_BITS"></a>

<a id="h264__types_8h_1aaab38631d2a138f13328b9f6cf4d4791"></a> MAX\_PFRAME\_BITS

<a id="c.MIN_FRAME_BITS"></a>

<a id="h264__types_8h_1aed824fcd42ee4e383f97b2c518607d59"></a> MIN\_FRAME\_BITS

<a id="c.DEFAULT_SKIP_MODE"></a>

<a id="h264__types_8h_1a1b85be457e8ce705d2df6ba3de9f0231"></a> DEFAULT\_SKIP\_MODE

<a id="c.H264_GOP_FRAME_CNT"></a>

<a id="h264__types_8h_1ab216a3671de961413232cd1bb8ad9dc1"></a> H264\_GOP\_FRAME\_CNT

<a id="c.H265_GOP_FRAME_CNT"></a>

<a id="h264__types_8h_1aae2c914729a9461f81d1bbb41a83758b"></a> H265\_GOP\_FRAME\_CNT

<a id="c.H264_COMPRESS_RATIO_DEFAULT_CONFIG"></a>

<a id="h264__types_8h_1ac0b79871fe346f190c59a8b0b21f9951"></a> H264\_COMPRESS\_RATIO\_DEFAULT\_CONFIG()
:   H264 compress ratio default config.

    This is the default configuration for the H264 compress ratio. The init\_qp/i\_min\_qp/i\_max\_qp/p\_min\_qp/p\_max\_qp range is \[15, 51\]. The imb\_bits/pmb\_bits range is \[50, 4095\].

    返回
    :   [h264\_compress\_ratio\_t](#structh264__compress__ratio__t)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv415h264_isr_type_t"></a>

<a id="_CPPv315h264_isr_type_t"></a> <a id="_CPPv215h264_isr_type_t"></a> <a id="h264__types_8h_1a2ab5824260e4ad814b96b5e48b706231"></a> enum h264\_isr\_type\_t
:   *Values:*

    <a id="_CPPv4N15h264_isr_type_t15H264_SKIP_FRAMEE"></a>

    <a id="_CPPv3N15h264_isr_type_t15H264_SKIP_FRAMEE"></a> <a id="_CPPv2N15h264_isr_type_t15H264_SKIP_FRAMEE"></a> <a id="h264__types_8h_1a2ab5824260e4ad814b96b5e48b706231a8a5068c32beb7ccda172f2a23ce2c89b"></a> enumerator H264\_SKIP\_FRAME

    <a id="_CPPv4N15h264_isr_type_t14H264_FINAL_OUTE"></a>

    <a id="_CPPv3N15h264_isr_type_t14H264_FINAL_OUTE"></a> <a id="_CPPv2N15h264_isr_type_t14H264_FINAL_OUTE"></a> <a id="h264__types_8h_1a2ab5824260e4ad814b96b5e48b706231a20fe684b48d6ecc6d14bbbfb5dffbafe"></a> enumerator H264\_FINAL\_OUT

    <a id="_CPPv4N15h264_isr_type_t14H264_LINE_DONEE"></a>

    <a id="_CPPv3N15h264_isr_type_t14H264_LINE_DONEE"></a> <a id="_CPPv2N15h264_isr_type_t14H264_LINE_DONEE"></a> <a id="h264__types_8h_1a2ab5824260e4ad814b96b5e48b706231a958bc458b9f3df7750178d10d5521f4e"></a> enumerator H264\_LINE\_DONE

    <a id="_CPPv4N15h264_isr_type_t12H264_ISR_MAXE"></a>

    <a id="_CPPv3N15h264_isr_type_t12H264_ISR_MAXE"></a> <a id="_CPPv2N15h264_isr_type_t12H264_ISR_MAXE"></a> <a id="h264__types_8h_1a2ab5824260e4ad814b96b5e48b706231a3b4f5753c68e6c44f9820f208d2dd407"></a> enumerator H264\_ISR\_MAX

<a id="_CPPv411h264_type_t"></a>

<a id="_CPPv311h264_type_t"></a> <a id="_CPPv211h264_type_t"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696"></a> enum h264\_type\_t
:   *Values:*

    <a id="_CPPv4N11h264_type_t20H264_NAL_UNSPECIFIEDE"></a>

    <a id="_CPPv3N11h264_type_t20H264_NAL_UNSPECIFIEDE"></a> <a id="_CPPv2N11h264_type_t20H264_NAL_UNSPECIFIEDE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696ad69024b6c7524d77d95dc9797b794932"></a> enumerator H264\_NAL\_UNSPECIFIED

    <a id="_CPPv4N11h264_type_t14H264_NAL_SLICEE"></a>

    <a id="_CPPv3N11h264_type_t14H264_NAL_SLICEE"></a> <a id="_CPPv2N11h264_type_t14H264_NAL_SLICEE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a9f5ecee4fcf069f90853d39dda680dfe"></a> enumerator H264\_NAL\_SLICE

    <a id="_CPPv4N11h264_type_t12H264_NAL_DPAE"></a>

    <a id="_CPPv3N11h264_type_t12H264_NAL_DPAE"></a> <a id="_CPPv2N11h264_type_t12H264_NAL_DPAE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a4e192fc076ebbc228544ef98f785846c"></a> enumerator H264\_NAL\_DPA

    <a id="_CPPv4N11h264_type_t12H264_NAL_DPBE"></a>

    <a id="_CPPv3N11h264_type_t12H264_NAL_DPBE"></a> <a id="_CPPv2N11h264_type_t12H264_NAL_DPBE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a0d5a11e9da42ef24f0a0ce53251331a3"></a> enumerator H264\_NAL\_DPB

    <a id="_CPPv4N11h264_type_t12H264_NAL_DPCE"></a>

    <a id="_CPPv3N11h264_type_t12H264_NAL_DPCE"></a> <a id="_CPPv2N11h264_type_t12H264_NAL_DPCE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a6da3a75493af0fa1ded8a72d4a6e4a55"></a> enumerator H264\_NAL\_DPC

    <a id="_CPPv4N11h264_type_t18H264_NAL_IDR_SLICEE"></a>

    <a id="_CPPv3N11h264_type_t18H264_NAL_IDR_SLICEE"></a> <a id="_CPPv2N11h264_type_t18H264_NAL_IDR_SLICEE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696afecaaa64bb1dfd9df3d21e7253ecb973"></a> enumerator H264\_NAL\_IDR\_SLICE

    <a id="_CPPv4N11h264_type_t12H264_NAL_SEIE"></a>

    <a id="_CPPv3N11h264_type_t12H264_NAL_SEIE"></a> <a id="_CPPv2N11h264_type_t12H264_NAL_SEIE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696ae3091622b1b99e74d09b16673e98b1d0"></a> enumerator H264\_NAL\_SEI

    <a id="_CPPv4N11h264_type_t12H264_NAL_SPSE"></a>

    <a id="_CPPv3N11h264_type_t12H264_NAL_SPSE"></a> <a id="_CPPv2N11h264_type_t12H264_NAL_SPSE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a9b569b7bafbb864fe260d3b84ad78387"></a> enumerator H264\_NAL\_SPS

    <a id="_CPPv4N11h264_type_t12H264_NAL_PPSE"></a>

    <a id="_CPPv3N11h264_type_t12H264_NAL_PPSE"></a> <a id="_CPPv2N11h264_type_t12H264_NAL_PPSE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a7e20eaba3c2969ad80d2e9a791cf1be0"></a> enumerator H264\_NAL\_PPS

    <a id="_CPPv4N11h264_type_t12H264_NAL_AUDE"></a>

    <a id="_CPPv3N11h264_type_t12H264_NAL_AUDE"></a> <a id="_CPPv2N11h264_type_t12H264_NAL_AUDE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696af6a508f5b414bc605a853f180be5f4bf"></a> enumerator H264\_NAL\_AUD

    <a id="_CPPv4N11h264_type_t21H264_NAL_END_SEQUENCEE"></a>

    <a id="_CPPv3N11h264_type_t21H264_NAL_END_SEQUENCEE"></a> <a id="_CPPv2N11h264_type_t21H264_NAL_END_SEQUENCEE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a1516f589b293cf637e30ef73d1572fb6"></a> enumerator H264\_NAL\_END\_SEQUENCE

    <a id="_CPPv4N11h264_type_t19H264_NAL_END_STREAME"></a>

    <a id="_CPPv3N11h264_type_t19H264_NAL_END_STREAME"></a> <a id="_CPPv2N11h264_type_t19H264_NAL_END_STREAME"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a03570c256f96c6d3d8abb7f44d4b9481"></a> enumerator H264\_NAL\_END\_STREAM

    <a id="_CPPv4N11h264_type_t20H264_NAL_FILLER_DATAE"></a>

    <a id="_CPPv3N11h264_type_t20H264_NAL_FILLER_DATAE"></a> <a id="_CPPv2N11h264_type_t20H264_NAL_FILLER_DATAE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696ad912e6a24ef4a096a45428913268f271"></a> enumerator H264\_NAL\_FILLER\_DATA

    <a id="_CPPv4N11h264_type_t16H264_NAL_SPS_EXTE"></a>

    <a id="_CPPv3N11h264_type_t16H264_NAL_SPS_EXTE"></a> <a id="_CPPv2N11h264_type_t16H264_NAL_SPS_EXTE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696ade05c1f88ff7c052a167864087c0dcd0"></a> enumerator H264\_NAL\_SPS\_EXT

    <a id="_CPPv4N11h264_type_t15H264_NAL_PREFIXE"></a>

    <a id="_CPPv3N11h264_type_t15H264_NAL_PREFIXE"></a> <a id="_CPPv2N11h264_type_t15H264_NAL_PREFIXE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a96a295c10d901b5a254ed03b4bd058f6"></a> enumerator H264\_NAL\_PREFIX

    <a id="_CPPv4N11h264_type_t16H264_NAL_SUB_SPSE"></a>

    <a id="_CPPv3N11h264_type_t16H264_NAL_SUB_SPSE"></a> <a id="_CPPv2N11h264_type_t16H264_NAL_SUB_SPSE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a91e44f24f4faef8fc245fe01e9d23574"></a> enumerator H264\_NAL\_SUB\_SPS

    <a id="_CPPv4N11h264_type_t12H264_NAL_DPSE"></a>

    <a id="_CPPv3N11h264_type_t12H264_NAL_DPSE"></a> <a id="_CPPv2N11h264_type_t12H264_NAL_DPSE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696aa95bce8a2088f301f6557b6a8f9fcf67"></a> enumerator H264\_NAL\_DPS

    <a id="_CPPv4N11h264_type_t19H264_NAL_RESERVED17E"></a>

    <a id="_CPPv3N11h264_type_t19H264_NAL_RESERVED17E"></a> <a id="_CPPv2N11h264_type_t19H264_NAL_RESERVED17E"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a6d3646f16aeb517e144b7d19ce487abf"></a> enumerator H264\_NAL\_RESERVED17

    <a id="_CPPv4N11h264_type_t19H264_NAL_RESERVED18E"></a>

    <a id="_CPPv3N11h264_type_t19H264_NAL_RESERVED18E"></a> <a id="_CPPv2N11h264_type_t19H264_NAL_RESERVED18E"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696afa0da81bdb782752463b35a81146049c"></a> enumerator H264\_NAL\_RESERVED18

    <a id="_CPPv4N11h264_type_t24H264_NAL_AUXILIARY_SLICEE"></a>

    <a id="_CPPv3N11h264_type_t24H264_NAL_AUXILIARY_SLICEE"></a> <a id="_CPPv2N11h264_type_t24H264_NAL_AUXILIARY_SLICEE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a22991b3104f543aea8b43d4b5310c54c"></a> enumerator H264\_NAL\_AUXILIARY\_SLICE

    <a id="_CPPv4N11h264_type_t20H264_NAL_EXTEN_SLICEE"></a>

    <a id="_CPPv3N11h264_type_t20H264_NAL_EXTEN_SLICEE"></a> <a id="_CPPv2N11h264_type_t20H264_NAL_EXTEN_SLICEE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696ae6707891e89b5e9c78e4c98d2f295bb3"></a> enumerator H264\_NAL\_EXTEN\_SLICE

    <a id="_CPPv4N11h264_type_t26H264_NAL_DEPTH_EXTEN_SLICEE"></a>

    <a id="_CPPv3N11h264_type_t26H264_NAL_DEPTH_EXTEN_SLICEE"></a> <a id="_CPPv2N11h264_type_t26H264_NAL_DEPTH_EXTEN_SLICEE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a7dd7f82ddc2442d495eff578d52dc22d"></a> enumerator H264\_NAL\_DEPTH\_EXTEN\_SLICE

    <a id="_CPPv4N11h264_type_t16H264_NAL_B_FRAMEE"></a>

    <a id="_CPPv3N11h264_type_t16H264_NAL_B_FRAMEE"></a> <a id="_CPPv2N11h264_type_t16H264_NAL_B_FRAMEE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a8491d6e2f8914bcdc94ecefa1d72e15a"></a> enumerator H264\_NAL\_B\_FRAME

    <a id="_CPPv4N11h264_type_t16H264_NAL_P_FRAMEE"></a>

    <a id="_CPPv3N11h264_type_t16H264_NAL_P_FRAMEE"></a> <a id="_CPPv2N11h264_type_t16H264_NAL_P_FRAMEE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a8e2f3f03e0cb38c091c604b13158ae06"></a> enumerator H264\_NAL\_P\_FRAME

    <a id="_CPPv4N11h264_type_t16H264_NAL_I_FRAMEE"></a>

    <a id="_CPPv3N11h264_type_t16H264_NAL_I_FRAMEE"></a> <a id="_CPPv2N11h264_type_t16H264_NAL_I_FRAMEE"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a8e63f952ac48a3c0e2358d0503e5a3e6"></a> enumerator H264\_NAL\_I\_FRAME

    <a id="_CPPv4N11h264_type_t22H264_NAL_UNSPECIFIED25E"></a>

    <a id="_CPPv3N11h264_type_t22H264_NAL_UNSPECIFIED25E"></a> <a id="_CPPv2N11h264_type_t22H264_NAL_UNSPECIFIED25E"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696ae1e6d825c93d0c1a8937bc4dd4cdf883"></a> enumerator H264\_NAL\_UNSPECIFIED25

    <a id="_CPPv4N11h264_type_t22H264_NAL_UNSPECIFIED26E"></a>

    <a id="_CPPv3N11h264_type_t22H264_NAL_UNSPECIFIED26E"></a> <a id="_CPPv2N11h264_type_t22H264_NAL_UNSPECIFIED26E"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a9f0021a74fe6dd15569278d32b26a01a"></a> enumerator H264\_NAL\_UNSPECIFIED26

    <a id="_CPPv4N11h264_type_t22H264_NAL_UNSPECIFIED27E"></a>

    <a id="_CPPv3N11h264_type_t22H264_NAL_UNSPECIFIED27E"></a> <a id="_CPPv2N11h264_type_t22H264_NAL_UNSPECIFIED27E"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a4d7b8fb3a9454c3885d105983e4a16ad"></a> enumerator H264\_NAL\_UNSPECIFIED27

    <a id="_CPPv4N11h264_type_t22H264_NAL_UNSPECIFIED28E"></a>

    <a id="_CPPv3N11h264_type_t22H264_NAL_UNSPECIFIED28E"></a> <a id="_CPPv2N11h264_type_t22H264_NAL_UNSPECIFIED28E"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a2f564c534f2dc4f698eb20b21aab2a62"></a> enumerator H264\_NAL\_UNSPECIFIED28

    <a id="_CPPv4N11h264_type_t22H264_NAL_UNSPECIFIED29E"></a>

    <a id="_CPPv3N11h264_type_t22H264_NAL_UNSPECIFIED29E"></a> <a id="_CPPv2N11h264_type_t22H264_NAL_UNSPECIFIED29E"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a2554ebeafbe7a2981e760f155e024559"></a> enumerator H264\_NAL\_UNSPECIFIED29

    <a id="_CPPv4N11h264_type_t22H264_NAL_UNSPECIFIED30E"></a>

    <a id="_CPPv3N11h264_type_t22H264_NAL_UNSPECIFIED30E"></a> <a id="_CPPv2N11h264_type_t22H264_NAL_UNSPECIFIED30E"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a1471cb6f908dbd0cac619ae71ec4b528"></a> enumerator H264\_NAL\_UNSPECIFIED30

    <a id="_CPPv4N11h264_type_t22H264_NAL_UNSPECIFIED31E"></a>

    <a id="_CPPv3N11h264_type_t22H264_NAL_UNSPECIFIED31E"></a> <a id="_CPPv2N11h264_type_t22H264_NAL_UNSPECIFIED31E"></a> <a id="h264__types_8h_1a9d17c373ecefa73b990fb26ec4f28696a0ccd8cac803c8682e4da17925f381957"></a> enumerator H264\_NAL\_UNSPECIFIED31

<a id="id2"></a>

### Header File

- [hal\_h264\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_h264_types.h)

<a id="id3"></a>

### Structures

<a id="_CPPv413h264_config_t"></a>

<a id="_CPPv313h264_config_t"></a> <a id="_CPPv213h264_config_t"></a> <a id="h264_config_t"></a> <a id="structh264__config__t"></a> struct h264\_config\_t

<a id="_CPPv49h264_qp_t"></a>

<a id="_CPPv39h264_qp_t"></a> <a id="_CPPv29h264_qp_t"></a> <a id="h264_qp_t"></a> <a id="structh264__qp__t"></a> struct h264\_qp\_t

<a id="_CPPv417h264_dma_config_t"></a>

<a id="_CPPv317h264_dma_config_t"></a> <a id="_CPPv217h264_dma_config_t"></a> <a id="h264_dma_config_t"></a> <a id="structh264__dma__config__t"></a> struct h264\_dma\_config\_t

<a id="id4"></a>

### Macros

<a id="c.PBITS_FACT1"></a>

<a id="hal__h264__types_8h_1a2288bcf8d7468859fc3543b2a2d5d26e"></a> PBITS\_FACT1

<a id="c.PBITS_FACT2"></a>

<a id="hal__h264__types_8h_1a05288eb6115d1f19a8f0894d5f66a4de"></a> PBITS\_FACT2

<a id="c.PBITS_FACT3"></a>

<a id="hal__h264__types_8h_1a5fb84b461e825db588b5089646aa4174"></a> PBITS\_FACT3

<a id="c.PBITS_FACT4"></a>

<a id="hal__h264__types_8h_1a3e937beb0cb6a6b0e1b58dc3c023a936"></a> PBITS\_FACT4

<a id="c.PBITS_FACT5"></a>

<a id="hal__h264__types_8h_1a34d5623222d6aef5495c1189bcad3577"></a> PBITS\_FACT5

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv411h264_unit_t"></a>

<a id="_CPPv311h264_unit_t"></a> <a id="_CPPv211h264_unit_t"></a> <a id="h264_unit_t"></a> <a id="hal__h264__types_8h_1a59173ddd9d5d3d3ab1c65e6df93ca544"></a> typedef uint8\_t h264\_unit\_t

<a id="_CPPv410h264_isr_t"></a>

<a id="_CPPv310h264_isr_t"></a> <a id="_CPPv210h264_isr_t"></a> <a id="h264_isr_t"></a> <a id="hal__h264__types_8h_1af9e58276addf20b37dc9d470cf90c226"></a> typedef void (\*h264\_isr\_t)([h264\_unit\_t](#_CPPv411h264_unit_t "h264_unit_t") id, void \*param)
