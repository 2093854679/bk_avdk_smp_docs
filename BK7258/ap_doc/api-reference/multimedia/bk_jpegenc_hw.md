---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_jpegenc_hw.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="jpeg-enc"></a>

# JPEG\_ENC

<a id="jpeg-enc-api-status"></a>

## JPEG\_ENC API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_jpeg_enc_driver_init()`](#_CPPv423bk_jpeg_enc_driver_initv "bk_jpeg_enc_driver_init") | Y |
| [`bk_jpeg_enc_driver_deinit()`](#_CPPv425bk_jpeg_enc_driver_deinitv "bk_jpeg_enc_driver_deinit") | Y |
| [`bk_jpeg_enc_init()`](#_CPPv416bk_jpeg_enc_initPK13jpeg_config_t "bk_jpeg_enc_init") | Y |
| [`bk_jpeg_enc_deinit()`](#_CPPv418bk_jpeg_enc_deinitv "bk_jpeg_enc_deinit") | Y |
| [`bk_jpeg_enc_start()`](#_CPPv417bk_jpeg_enc_start10yuv_mode_t "bk_jpeg_enc_start") | Y |
| [`bk_jpeg_enc_stop()`](#_CPPv416bk_jpeg_enc_stop10yuv_mode_t "bk_jpeg_enc_stop") | Y |
| [`bk_jpeg_enc_yuv_fmt_sel()`](#_CPPv423bk_jpeg_enc_yuv_fmt_sel12yuv_format_t "bk_jpeg_enc_yuv_fmt_sel") | N |
| [`bk_jpeg_enc_get_frame_size()`](#_CPPv426bk_jpeg_enc_get_frame_sizev "bk_jpeg_enc_get_frame_size") | Y |
| [`bk_jpeg_enc_register_isr()`](#_CPPv424bk_jpeg_enc_register_isr15jpeg_isr_type_t10jpeg_isr_tPv "bk_jpeg_enc_register_isr") | Y |
| [`bk_jpeg_enc_unregister_isr()`](#_CPPv426bk_jpeg_enc_unregister_isr15jpeg_isr_type_t "bk_jpeg_enc_unregister_isr") | Y |
| [`bk_jpeg_enc_get_fifo_addr()`](#_CPPv425bk_jpeg_enc_get_fifo_addrP8uint32_t "bk_jpeg_enc_get_fifo_addr") | Y |
| [`bk_jpeg_enc_set_auxs()`](#_CPPv420bk_jpeg_enc_set_auxs8uint32_t8uint32_t "bk_jpeg_enc_set_auxs") | N |
| [`bk_jpeg_enc_partial_display_init()`](#_CPPv432bk_jpeg_enc_partial_display_initPK28jpeg_partial_offset_config_t "bk_jpeg_enc_partial_display_init") | N |
| [`bk_jpeg_enc_partial_display_deinit()`](#_CPPv434bk_jpeg_enc_partial_display_deinitv "bk_jpeg_enc_partial_display_deinit") | N |
| [`bk_jpeg_set_em_base_addr()`](#_CPPv424bk_jpeg_set_em_base_addrP7uint8_t "bk_jpeg_set_em_base_addr") | N |
| [`bk_jpeg_get_em_base_addr()`](#_CPPv424bk_jpeg_get_em_base_addrv "bk_jpeg_get_em_base_addr") | N |
| [`bk_jpeg_enc_encode_config()`](#_CPPv425bk_jpeg_enc_encode_config7uint8_t8uint32_t8uint32_t "bk_jpeg_enc_encode_config") | Y |
| [`bk_jpeg_enc_mode_switch()`](#_CPPv423bk_jpeg_enc_mode_switchP13jpeg_config_t "bk_jpeg_enc_mode_switch") | N |
| [`bk_jpeg_enc_set_mclk_div()`](#_CPPv424bk_jpeg_enc_set_mclk_div10mclk_div_t "bk_jpeg_enc_set_mclk_div") | N |
| [`bk_jpeg_enc_soft_reset()`](#_CPPv422bk_jpeg_enc_soft_resetv "bk_jpeg_enc_soft_reset") | Y |

<a id="jpeg-enc-marco-defined-and-config"></a>

## JPEG\_ENC Marco defined and config

| Marco name | illustrate |
| --- | --- |
| CONFIG\_JPEGENC\_HW | enable JPEG\_ENC module or not |

备注

CONFIG\_JPEGENC\_HW depends on CONFIG\_YUV\_BUF, JPEG module can not work alone. Those api only for reference, user can not use them directly. Please referecnce doorbell project.

<a id="jpeg-enc-api-reference"></a>

## JPEG\_ENC API Reference

<a id="header-file"></a>

### Header File

- [jpeg\_enc.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/jpeg_enc.h)

<a id="functions"></a>

### Functions

<a id="_CPPv423bk_jpeg_enc_driver_initv"></a>

<a id="_CPPv323bk_jpeg_enc_driver_initv"></a> <a id="_CPPv223bk_jpeg_enc_driver_initv"></a> <a id="bk_jpeg_enc_driver_init__void"></a> <a id="jpeg__enc_8h_1aa627d0d3312f723f3a348dd53f05a63a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_driver\_init(void)
:   Init the jpeg encode driver.

    This API init the resoure common:

    - Init jpegenc driver control memory
    - register jpegenc isr

    **Attention**
    :   1\. This API should be called before any other jpeg APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_jpeg_enc_driver_deinitv"></a>

<a id="_CPPv325bk_jpeg_enc_driver_deinitv"></a> <a id="_CPPv225bk_jpeg_enc_driver_deinitv"></a> <a id="bk_jpeg_enc_driver_deinit__void"></a> <a id="jpeg__enc_8h_1a8a6e76226601221ff4b3f6f02e272929"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_driver\_deinit(void)
:   Deinit the jpegenc driver.

    This API free all resource related to jpegenc and disable jpegenc.

    **Attention**
    :   1\. This API will power down video when soc is bk7256XX

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_jpeg_enc_initPK13jpeg_config_t"></a>

<a id="_CPPv316bk_jpeg_enc_initPK13jpeg_config_t"></a> <a id="_CPPv216bk_jpeg_enc_initPK13jpeg_config_t"></a> <a id="bk_jpeg_enc_init__jpeg_config_tCP"></a> <a id="jpeg__enc_8h_1a20ba8dee0b17571ec977683d0911185e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_init(const [jpeg\_config\_t](#_CPPv413jpeg_config_t "jpeg_config_t") \*config)
:   Init the jpeg encode.

    This API init the jpegenc

    - Configure clock and Power up the jpegenc
    - Enable Jpegenc interrupt
    - Map the jpegenc to dedicated GPIO port(MCLK and PCLK)
    - Set the jpegenc parameters
    - Enable jpeg encode module

    Usage example:

    ```
     jpeg_config_t init_config = {
                         .rx_buf = xxx, // the address point to mem for receiving jpeg data
                         .yuv_mode = 0,
                         .sys_clk_div = 3, // jpeg_clk = 480 / (1+3) =120MHz
                         .mclk_div = 0, // MCLK=jpeg_clk/4 = 30MHz
                         .rx_buf_len = xxx, // the length of receive jpeg data
                         .node_len = xxx, // dma transfer length
                         .x_pixel = 80, // jpeg image resolution of width: 80 * 8 = 640
                         .y_pixel = 60, // jpeg image resolution of height: 60 * 8 = 480
                         .dma_rx_finish_handler = cb, // dma transfer finish callback
                     };
     BK_LOG_ON_ERR(bk_jpeg_init(&init_config);
    ```

    **Attention**
    :   1\. only work for imaging transfer

    参数
    :   **config** – jpeg encode parameter settings

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: jpegenc config paramter is NULL
        - BK\_ERR\_JPEG\_NOT\_INIT: jpegenc driver not init
        - others: other errors.

<a id="_CPPv418bk_jpeg_enc_deinitv"></a>

<a id="_CPPv318bk_jpeg_enc_deinitv"></a> <a id="_CPPv218bk_jpeg_enc_deinitv"></a> <a id="bk_jpeg_enc_deinit__void"></a> <a id="jpeg__enc_8h_1ab6a0d8537992e1373514cc3363b6c249"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_deinit(void)
:   Deinit the jpeg.

    This API stop jpeg encode, close jpeg gpio, power off jpeg module at last.

    **Attention**
    :   1\. only work for imaging transfer

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv417bk_jpeg_enc_start10yuv_mode_t"></a>

<a id="_CPPv317bk_jpeg_enc_start10yuv_mode_t"></a> <a id="_CPPv217bk_jpeg_enc_start10yuv_mode_t"></a> <a id="bk_jpeg_enc_start__yuv_mode_t"></a> <a id="jpeg__enc_8h_1afeb0ad85c0db0da97a15792dd43e4e4d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_start(yuv\_mode\_t mode)
:   set jpegenc start

    This API will set jpegenc work start.

    **Attention**
    :   1\. if work in jpegenc mode, this api can enable jpegenc mode

    **Attention**
    :   2\. if work in yuv mode, this api can enable yuv\_mode.

    参数
    :   **mode** – 0/1:jpeg encode mode/yuv mode

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_jpeg_enc_stop10yuv_mode_t"></a>

<a id="_CPPv316bk_jpeg_enc_stop10yuv_mode_t"></a> <a id="_CPPv216bk_jpeg_enc_stop10yuv_mode_t"></a> <a id="bk_jpeg_enc_stop__yuv_mode_t"></a> <a id="jpeg__enc_8h_1af18d33bbfb845f653d1e45f9b47c4f5b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_stop(yuv\_mode\_t mode)
:   set jpegenc stop

    This API will set jpegenc work stop.

    **Attention**
    :   1\. if work in jpegenc mode, this api can disable jpegenc mode

    **Attention**
    :   2\. if work in yuv mode, this api can disable yuv\_mode.

    参数
    :   **mode** – 0/1:jpeg encode mode/yuv mode

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_jpeg_enc_yuv_fmt_sel12yuv_format_t"></a>

<a id="_CPPv323bk_jpeg_enc_yuv_fmt_sel12yuv_format_t"></a> <a id="_CPPv223bk_jpeg_enc_yuv_fmt_sel12yuv_format_t"></a> <a id="bk_jpeg_enc_yuv_fmt_sel__yuv_format_t"></a> <a id="jpeg__enc_8h_1a75e181e60c1536ca6ed473782a9a2428"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_yuv\_fmt\_sel(yuv\_format\_t fmt)
:   yuv format select

    This API will set yuv output format.

    **Attention**
    :   1\. this function only used when jpeg at yuv mode

    参数
    :   **value** – 0:yuyv, 1:uyvy, 2:yyuv, 3:uvyy

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_jpeg_enc_get_frame_sizev"></a>

<a id="_CPPv326bk_jpeg_enc_get_frame_sizev"></a> <a id="_CPPv226bk_jpeg_enc_get_frame_sizev"></a> <a id="bk_jpeg_enc_get_frame_size__void"></a> <a id="jpeg__enc_8h_1ac47ca42ba05cf3a44ecb2cf9e3d6c29d"></a> uint32\_t bk\_jpeg\_enc\_get\_frame\_size(void)
:   get a frame size output from jpegenc module, uint byte

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_jpeg_enc_register_isr15jpeg_isr_type_t10jpeg_isr_tPv"></a>

<a id="_CPPv324bk_jpeg_enc_register_isr15jpeg_isr_type_t10jpeg_isr_tPv"></a> <a id="_CPPv224bk_jpeg_enc_register_isr15jpeg_isr_type_t10jpeg_isr_tPv"></a> <a id="bk_jpeg_enc_register_isr__jpeg_isr_type_t.jpeg_isr_t.voidP"></a> <a id="jpeg__enc_8h_1af39149f90bba9122e2ca890ab0c71891"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_register\_isr([jpeg\_isr\_type\_t](#_CPPv415jpeg_isr_type_t "jpeg_isr_type_t") type\_id, [jpeg\_isr\_t](#_CPPv410jpeg_isr_t "jpeg_isr_t") isr, void \*param)
:   register frame end isr

    This API will register jpeg encode isr function, need user defined.The isr function will execute when the isr be triggered.

    参数
    :   - **type\_id** – the type of the isr

          - JPEG\_EOY: (eoy)when jpeg encode work in yuv mode, once a complete frame have been transfer by jpeg encode module, the isr will trigger.
          - JPEG\_HEAD\_OUTPUT: jpeg encode output head the isrt will be triggered, work in jpeg encode mode.
          - START\_OFFRAME: (sof) when jpeg encode module start reveice a frame the isr will be triggered.
          - JPEG\_EOF: (eof) when jpeg encode module receive a complete frame the isr will be triggered, this only effect in jpeg encode mode.
          - JPEG\_VSYNC\_NEGEDGE: (vng) when jpeg encode module receive a vsync negedge the isr will be triggered.
        - **isr** – isr\_func
        - **param** – other value(default set NULL)

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_jpeg_enc_unregister_isr15jpeg_isr_type_t"></a>

<a id="_CPPv326bk_jpeg_enc_unregister_isr15jpeg_isr_type_t"></a> <a id="_CPPv226bk_jpeg_enc_unregister_isr15jpeg_isr_type_t"></a> <a id="bk_jpeg_enc_unregister_isr__jpeg_isr_type_t"></a> <a id="jpeg__enc_8h_1ae0209be234aaeafdf8622ab5d712da1d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_unregister\_isr([jpeg\_isr\_type\_t](#_CPPv415jpeg_isr_type_t "jpeg_isr_type_t") type\_id)
:   unregister frame end isr

    This API will unregister jpeg encode isr function, need user unregister, when deinit jpeg module

    参数
    :   **type\_id** – the type of the isr

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_jpeg_enc_get_fifo_addrP8uint32_t"></a>

<a id="_CPPv325bk_jpeg_enc_get_fifo_addrP8uint32_t"></a> <a id="_CPPv225bk_jpeg_enc_get_fifo_addrP8uint32_t"></a> <a id="bk_jpeg_enc_get_fifo_addr__uint32_tP"></a> <a id="jpeg__enc_8h_1accbcc8d4eb52e62607fef7369887e9c4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_get\_fifo\_addr(uint32\_t \*fifo\_addr)
:   get jpeg enc fifo addr

    This API will get jpeg encode fifo addr in param

    **Attention**
    :   1\. only work in jpeg encode mode is effective

    参数
    :   **fifo\_addr** – fifo addr

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_jpeg_enc_set_auxs8uint32_t8uint32_t"></a>

<a id="_CPPv320bk_jpeg_enc_set_auxs8uint32_t8uint32_t"></a> <a id="_CPPv220bk_jpeg_enc_set_auxs8uint32_t8uint32_t"></a> <a id="bk_jpeg_enc_set_auxs__uint32_t.uint32_t"></a> <a id="jpeg__enc_8h_1ae273638b25edd14a671fd92d744c814f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_set\_auxs(uint32\_t cksel, uint32\_t ckdiv)
:   set mclk output

    This API will use for camera config

    @attenation 1\. this api only used for bk7256xx\_mp chip, and when use this api, this api ‘bk\_jpeg\_enc\_mclk\_enable’ will not useful

    参数
    :   - **cksel** – 0-3:0:DCO/1:APLL/2:320M/3:480M,use 2 or 3
        - **ckdiv** – 0-15, div \= 1/(ckdiv\+1)

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv432bk_jpeg_enc_partial_display_initPK28jpeg_partial_offset_config_t"></a>

<a id="_CPPv332bk_jpeg_enc_partial_display_initPK28jpeg_partial_offset_config_t"></a> <a id="_CPPv232bk_jpeg_enc_partial_display_initPK28jpeg_partial_offset_config_t"></a> <a id="bk_jpeg_enc_partial_display_init__jpeg_partial_offset_config_tCP"></a> <a id="jpeg__enc_8h_1a3dc1fdd103c565e86468eb070809339b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_partial\_display\_init(const [jpeg\_partial\_offset\_config\_t](#_CPPv428jpeg_partial_offset_config_t "jpeg_partial_offset_config_t") \*offset\_config)
:   partial display init

    This API will use for partial display configure of jpeg encode

    参数
    :   **offset\_config** – x\_pixel left/right offset and y\_pixel left/right offset configure

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv434bk_jpeg_enc_partial_display_deinitv"></a>

<a id="_CPPv334bk_jpeg_enc_partial_display_deinitv"></a> <a id="_CPPv234bk_jpeg_enc_partial_display_deinitv"></a> <a id="bk_jpeg_enc_partial_display_deinit__void"></a> <a id="jpeg__enc_8h_1a89041c6211b312d6fb412476e0e8aa99"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_partial\_display\_deinit(void)
:   partial display deinit

    This API will use for partial display deinit

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_jpeg_set_em_base_addrP7uint8_t"></a>

<a id="_CPPv324bk_jpeg_set_em_base_addrP7uint8_t"></a> <a id="_CPPv224bk_jpeg_set_em_base_addrP7uint8_t"></a> <a id="bk_jpeg_set_em_base_addr__uint8_tP"></a> <a id="jpeg__enc_8h_1a5bd17d8d578305434d40bf2b5522d1d8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_set\_em\_base\_addr(uint8\_t \*address)
:   jpeg em base set

    This API will use for jpeg em base address, 64KB memory align.

    参数
    :   **address** – set a mem used for jpeg encode

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_jpeg_get_em_base_addrv"></a>

<a id="_CPPv324bk_jpeg_get_em_base_addrv"></a> <a id="_CPPv224bk_jpeg_get_em_base_addrv"></a> <a id="bk_jpeg_get_em_base_addr__void"></a> <a id="jpeg__enc_8h_1a44aefaf185c04803d8d14371c485dc18"></a> uint32\_t bk\_jpeg\_get\_em\_base\_addr(void)
:   jpeg em base get

    This API will use for get jpeg em base address.

    返回
    :   - jpeg em base

<a id="_CPPv425bk_jpeg_enc_encode_config7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv325bk_jpeg_enc_encode_config7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv225bk_jpeg_enc_encode_config7uint8_t8uint32_t8uint32_t"></a> <a id="bk_jpeg_enc_encode_config__uint8_t.uint32_t.uint32_t"></a> <a id="jpeg__enc_8h_1a81cd08aa14fc8e5562f88853601f9984"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_encode\_config(uint8\_t enable, uint32\_t up\_size, uint32\_t low\_size)
:   jpeg encode enable encode auto contrl

    This API will use for enable/disable for auto encode size. only valid in jpeh encode mode

    @attenation 1\. this api only called in jpeg\_eof\_isr function, and only bk\_jpeg\_enc\_enable\_encode\_auto\_ctrl have been set enable

    参数
    :   - **up\_size** – the jpeg image upper limit, unit byte
        - **low\_size** – the jpeg image lower limit, unit byte

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv429bk_jpeg_enc_get_encode_configP8uint32_tP8uint32_t"></a>

<a id="_CPPv329bk_jpeg_enc_get_encode_configP8uint32_tP8uint32_t"></a> <a id="_CPPv229bk_jpeg_enc_get_encode_configP8uint32_tP8uint32_t"></a> <a id="bk_jpeg_enc_get_encode_config__uint32_tP.uint32_tP"></a> <a id="jpeg__enc_8h_1aacc6a7d9fa1c2f59a4663c4bb5fe797b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_get\_encode\_config(uint32\_t \*up\_size, uint32\_t \*low\_size)
:   get jpeg encode config

    This API will use for get jpeg encode config

    参数
    :   - **up\_size** – the jpeg image upper limit, unit byte
        - **low\_size** – the jpeg image lower limit, unit byte

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_jpeg_enc_mode_switchP13jpeg_config_t"></a>

<a id="_CPPv323bk_jpeg_enc_mode_switchP13jpeg_config_t"></a> <a id="_CPPv223bk_jpeg_enc_mode_switchP13jpeg_config_t"></a> <a id="bk_jpeg_enc_mode_switch__jpeg_config_tP"></a> <a id="jpeg__enc_8h_1a4b839f6fd75aebdac1358cea7eadcac6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_mode\_switch([jpeg\_config\_t](#_CPPv413jpeg_config_t "jpeg_config_t") \*config)
:   jpeg encode mode and yuv mode switch

    This API will use for switch jpeg mode

    @attenation 1\. this api must called in jpeg\_eof isr or yuv\_eof isr

    参数
    :   **config** – jpeg encode config or jpeg yuv config

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_jpeg_enc_set_mclk_div10mclk_div_t"></a>

<a id="_CPPv324bk_jpeg_enc_set_mclk_div10mclk_div_t"></a> <a id="_CPPv224bk_jpeg_enc_set_mclk_div10mclk_div_t"></a> <a id="bk_jpeg_enc_set_mclk_div__mclk_div_t"></a> <a id="jpeg__enc_8h_1acafd541ecd8a13d7c90df58f7d6df489"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_set\_mclk\_div(mclk\_div\_t div)

<a id="_CPPv422bk_jpeg_enc_soft_resetv"></a>

<a id="_CPPv322bk_jpeg_enc_soft_resetv"></a> <a id="_CPPv222bk_jpeg_enc_soft_resetv"></a> <a id="bk_jpeg_enc_soft_reset__void"></a> <a id="jpeg__enc_8h_1a1f9f1643910ea24bd61dc8dae8d621ba"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_soft\_reset(void)
:   jpeg encode module softreset

    This API will use for resetting jpeg encode module

    @attenation 1\. this api only used in bk7236xx

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv429bk_jpeg_enc_global_soft_reset7uint8_t"></a>

<a id="_CPPv329bk_jpeg_enc_global_soft_reset7uint8_t"></a> <a id="_CPPv229bk_jpeg_enc_global_soft_reset7uint8_t"></a> <a id="bk_jpeg_enc_global_soft_reset__uint8_t"></a> <a id="jpeg__enc_8h_1a1cfaccbfd55f1b148f336376170b81ed"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_jpeg\_enc\_global\_soft\_reset(uint8\_t enable)
:   jpeg encode module global softreset

    This API will use for resetting jpeg encode module

    @attenation 1\. this api only used in bk7236xx @attenation 2\. this api must be called twice to complete the reset: first enable(1), then disable(0)

    参数
    :   **enable** – 0:disable, 1:enable

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="jpeg-enc-api-typedefs"></a>

## JPEG\_ENC API Typedefs

<a id="id1"></a>

### Header File

- [jpeg\_enc\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/jpeg_enc_types.h)

<a id="macros"></a>

### Macros

<a id="c.Y_PIXEL_272"></a>

<a id="jpeg__enc__types_8h_1a522404482babcb4eaf5194f358da79ff"></a> Y\_PIXEL\_272
:   JPEGENC APIs Version 1.0.

    image resolution for hight: Y \* 8 \= 272

<a id="c.Y_PIXEL_320"></a>

<a id="jpeg__enc__types_8h_1ab0d71e31f0a16373ed2a009f2ffba484"></a> Y\_PIXEL\_320
:   image resolution for hight: Y \* 8 \= 320

<a id="c.X_PIXEL_480"></a>

<a id="jpeg__enc__types_8h_1a6d819fd957585002ae577656335ceb4d"></a> X\_PIXEL\_480
:   image resolution for width: X \* 8 \= 480

<a id="c.Y_PIXEL_480"></a>

<a id="jpeg__enc__types_8h_1ab3f397fb7ef0d4146c3eb8969be9fe97"></a> Y\_PIXEL\_480
:   image resolution for hight: Y \* 8 \= 480

<a id="c.X_PIXEL_640"></a>

<a id="jpeg__enc__types_8h_1a4f02881b00a2a0e8c216cb1eaec25f28"></a> X\_PIXEL\_640
:   image resolution for hight: X \* 8 \= 640

<a id="c.Y_PIXEL_240"></a>

<a id="jpeg__enc__types_8h_1ab4d9548ba28b2774a13e9c469f1f0f73"></a> Y\_PIXEL\_240
:   image resolution for hight: Y \* 8 \= 240

<a id="c.X_PIXEL_320"></a>

<a id="jpeg__enc__types_8h_1a949fd6364e8ce0227ce8f42217aefb03"></a> X\_PIXEL\_320
:   image resolution for hight: X \* 8 \= 320

<a id="c.Y_PIXEL_600"></a>

<a id="jpeg__enc__types_8h_1a3821b9a80a3f1fac681b46f53fc3398e"></a> Y\_PIXEL\_600
:   image resolution for hight: Y \* 8 \= 600

<a id="c.X_PIXEL_800"></a>

<a id="jpeg__enc__types_8h_1a9d01a40e7e75283f258fda84bda80130"></a> X\_PIXEL\_800
:   image resolution for hight: X \* 8 \= 800

<a id="c.Y_PIXEL_720"></a>

<a id="jpeg__enc__types_8h_1aea7342a2701602b4c2b8cb72a830dccc"></a> Y\_PIXEL\_720
:   image resolution for hight: Y \* 8 \= 720

<a id="c.X_PIXEL_1280"></a>

<a id="jpeg__enc__types_8h_1ad26437aad7c4d19fab25865b65e8a635"></a> X\_PIXEL\_1280
:   image resolution for hight: X \* 8 \= 1280

<a id="c.X_PIXEL_1600"></a>

<a id="jpeg__enc__types_8h_1a1bdb08449f697917a8b4877a1aaee026"></a> X\_PIXEL\_1600
:   image resolution for hight: X \* 8 \= 1600

<a id="c.Y_PIXEL_1200"></a>

<a id="jpeg__enc__types_8h_1a12ea013e007311ec2fff1afebd3d79a4"></a> Y\_PIXEL\_1200
:   image resolution for hight: Y \* 8 \= 1200

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410jpeg_isr_t"></a>

<a id="_CPPv310jpeg_isr_t"></a> <a id="_CPPv210jpeg_isr_t"></a> <a id="jpeg_isr_t"></a> <a id="jpeg__enc__types_8h_1acbd42c0f8bb94d8c5e8a98bffc30ee76"></a> typedef void (\*jpeg\_isr\_t)([jpeg\_unit\_t](#_CPPv411jpeg_unit_t "jpeg_unit_t") id, void \*param)
:   jpeg isr callback relay jpeg driver

    Param id
    :   only 0 useful, set 0 default

    Param param
    :   NULL default

<a id="id2"></a>

### Header File

- [hal\_jpeg\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_jpeg_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv413jpeg_config_t"></a>

<a id="_CPPv313jpeg_config_t"></a> <a id="_CPPv213jpeg_config_t"></a> <a id="jpeg_config_t"></a> <a id="structjpeg__config__t"></a> struct jpeg\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13jpeg_config_t6rx_bufE"></a>

    <a id="_CPPv3N13jpeg_config_t6rx_bufE"></a> <a id="_CPPv2N13jpeg_config_t6rx_bufE"></a> <a id="jpeg_config_t::rx_buf__uint8_tP"></a> <a id="structjpeg__config__t_1a5dec70fa63193130ffb81b7c65160b1e"></a> uint8\_t \*rx\_buf
    :   the address of receiving jpeg data

    <a id="_CPPv4N13jpeg_config_t4modeE"></a>

    <a id="_CPPv3N13jpeg_config_t4modeE"></a> <a id="_CPPv2N13jpeg_config_t4modeE"></a> <a id="jpeg_config_t::mode__yuv_mode_t"></a> <a id="structjpeg__config__t_1a35cfed1f938383a389982f5a85335412"></a> yuv\_mode\_t mode
    :   jpeg module work mode:0/1:jpegencoder/yuv

    <a id="_CPPv4N13jpeg_config_t3clkE"></a>

    <a id="_CPPv3N13jpeg_config_t3clkE"></a> <a id="_CPPv2N13jpeg_config_t3clkE"></a> <a id="jpeg_config_t::clk__mclk_freq_t"></a> <a id="structjpeg__config__t_1a3d4b1f2c6864f8d55d5037c736aed0cf"></a> mclk\_freq\_t clk
    :   jpeg module work clk config

    <a id="_CPPv4N13jpeg_config_t5vsyncE"></a>

    <a id="_CPPv3N13jpeg_config_t5vsyncE"></a> <a id="_CPPv2N13jpeg_config_t5vsyncE"></a> <a id="jpeg_config_t::vsync__sync_level_t"></a> <a id="structjpeg__config__t_1a6e7f4bf07cdd0c8b3a2b21ab84dfa937"></a> sync\_level\_t vsync
    :   sensor vsync active level

    <a id="_CPPv4N13jpeg_config_t5hsyncE"></a>

    <a id="_CPPv3N13jpeg_config_t5hsyncE"></a> <a id="_CPPv2N13jpeg_config_t5hsyncE"></a> <a id="jpeg_config_t::hsync__sync_level_t"></a> <a id="structjpeg__config__t_1a7e7e59d3cd66cf2a0ef578166e3922c0"></a> sync\_level\_t hsync
    :   sensor hsync active level

    <a id="_CPPv4N13jpeg_config_t10sensor_fmtE"></a>

    <a id="_CPPv3N13jpeg_config_t10sensor_fmtE"></a> <a id="_CPPv2N13jpeg_config_t10sensor_fmtE"></a> <a id="jpeg_config_t::sensor_fmt__yuv_format_t"></a> <a id="structjpeg__config__t_1a4e8166bcb77a3d5a16801df6bbae5f8b"></a> yuv\_format\_t sensor\_fmt
    :   sensor input data format

    <a id="_CPPv4N13jpeg_config_t10rx_buf_lenE"></a>

    <a id="_CPPv3N13jpeg_config_t10rx_buf_lenE"></a> <a id="_CPPv2N13jpeg_config_t10rx_buf_lenE"></a> <a id="jpeg_config_t::rx_buf_len__uint32_t"></a> <a id="structjpeg__config__t_1aa7fa1a0021ba3ecbd789818cf194164f"></a> uint32\_t rx\_buf\_len
    :   the length for receiving jpeg data

    <a id="_CPPv4N13jpeg_config_t8node_lenE"></a>

    <a id="_CPPv3N13jpeg_config_t8node_lenE"></a> <a id="_CPPv2N13jpeg_config_t8node_lenE"></a> <a id="jpeg_config_t::node_len__uint32_t"></a> <a id="structjpeg__config__t_1a23acfe32680938b7117f380ae207860e"></a> uint32\_t node\_len
    :   dma transfer length

    <a id="_CPPv4N13jpeg_config_t7x_pixelE"></a>

    <a id="_CPPv3N13jpeg_config_t7x_pixelE"></a> <a id="_CPPv2N13jpeg_config_t7x_pixelE"></a> <a id="jpeg_config_t::x_pixel__uint32_t"></a> <a id="structjpeg__config__t_1a902b0b398e4c116c8413dde299f609ee"></a> uint32\_t x\_pixel
    :   jpeg encode image resolution for width

    <a id="_CPPv4N13jpeg_config_t7y_pixelE"></a>

    <a id="_CPPv3N13jpeg_config_t7y_pixelE"></a> <a id="_CPPv2N13jpeg_config_t7y_pixelE"></a> <a id="jpeg_config_t::y_pixel__uint32_t"></a> <a id="structjpeg__config__t_1a8abdf0714669b504b952dd1148672527"></a> uint32\_t y\_pixel
    :   jpeg encode image resolution for height

<a id="_CPPv428jpeg_partial_offset_config_t"></a>

<a id="_CPPv328jpeg_partial_offset_config_t"></a> <a id="_CPPv228jpeg_partial_offset_config_t"></a> <a id="jpeg_partial_offset_config_t"></a> <a id="structjpeg__partial__offset__config__t"></a> struct jpeg\_partial\_offset\_config\_t

<a id="id3"></a>

### Macros

<a id="c.JPEG_CRC_SIZE"></a>

<a id="hal__jpeg__types_8h_1a95a3d2c26176fe54b6d1010d6f6aff83"></a> JPEG\_CRC\_SIZE

<a id="c.BK_ERR_JPEG_NOT_INIT"></a>

<a id="hal__jpeg__types_8h_1a3369b528dc5491f109b9b4a0c068ffb4"></a> BK\_ERR\_JPEG\_NOT\_INIT
:   JPEG driver not init

<a id="id4"></a>

### Type Definitions

<a id="_CPPv411jpeg_unit_t"></a>

<a id="_CPPv311jpeg_unit_t"></a> <a id="_CPPv211jpeg_unit_t"></a> <a id="jpeg_unit_t"></a> <a id="hal__jpeg__types_8h_1ade3f08334d7148b6071b77376c846354"></a> typedef uint8\_t jpeg\_unit\_t
:   jpeg uint id

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv415jpeg_isr_type_t"></a>

<a id="_CPPv315jpeg_isr_type_t"></a> <a id="_CPPv215jpeg_isr_type_t"></a> <a id="hal__jpeg__types_8h_1ad64e59977e7197df24b45e2f298a4c49"></a> enum jpeg\_isr\_type\_t
:   *Values:*

    <a id="_CPPv4N15jpeg_isr_type_t8JPEG_EOYE"></a>

    <a id="_CPPv3N15jpeg_isr_type_t8JPEG_EOYE"></a> <a id="_CPPv2N15jpeg_isr_type_t8JPEG_EOYE"></a> <a id="hal__jpeg__types_8h_1ad64e59977e7197df24b45e2f298a4c49a9282c5772e4cf378081856f88499ff2f"></a> enumerator JPEG\_EOY
    :   when work at yuv mode, transfer a complete frame will trigger this isr

    <a id="_CPPv4N15jpeg_isr_type_t16JPEG_HEAD_OUTPUTE"></a>

    <a id="_CPPv3N15jpeg_isr_type_t16JPEG_HEAD_OUTPUTE"></a> <a id="_CPPv2N15jpeg_isr_type_t16JPEG_HEAD_OUTPUTE"></a> <a id="hal__jpeg__types_8h_1ad64e59977e7197df24b45e2f298a4c49af3a6ca507bda37dd545aa1c3bbac93d2"></a> enumerator JPEG\_HEAD\_OUTPUT
    :   when work at jpeg encode mode, the head output complete will trigger this isr

    <a id="_CPPv4N15jpeg_isr_type_t8JPEG_SOFE"></a>

    <a id="_CPPv3N15jpeg_isr_type_t8JPEG_SOFE"></a> <a id="_CPPv2N15jpeg_isr_type_t8JPEG_SOFE"></a> <a id="hal__jpeg__types_8h_1ad64e59977e7197df24b45e2f298a4c49a30b66c3cb623fda9087c912cff8afb46"></a> enumerator JPEG\_SOF
    :   when work at jpeg encode mode, detect vsync rising edge after few cycle will trigger this isr

    <a id="_CPPv4N15jpeg_isr_type_t8JPEG_EOFE"></a>

    <a id="_CPPv3N15jpeg_isr_type_t8JPEG_EOFE"></a> <a id="_CPPv2N15jpeg_isr_type_t8JPEG_EOFE"></a> <a id="hal__jpeg__types_8h_1ad64e59977e7197df24b45e2f298a4c49ad16eaa1eeda82d4d5e7aed0524d5c2e5"></a> enumerator JPEG\_EOF
    :   when work at jpeg encode mode, transfer a complete frame will trigger this isr

    <a id="_CPPv4N15jpeg_isr_type_t18JPEG_VSYNC_NEGEDGEE"></a>

    <a id="_CPPv3N15jpeg_isr_type_t18JPEG_VSYNC_NEGEDGEE"></a> <a id="_CPPv2N15jpeg_isr_type_t18JPEG_VSYNC_NEGEDGEE"></a> <a id="hal__jpeg__types_8h_1ad64e59977e7197df24b45e2f298a4c49a84733c8dba6eb3fbed299f93f6f461a4"></a> enumerator JPEG\_VSYNC\_NEGEDGE
    :   when detect vsync negedge will trigger this isr

    <a id="_CPPv4N15jpeg_isr_type_t15JPEG_LINE_CLEARE"></a>

    <a id="_CPPv3N15jpeg_isr_type_t15JPEG_LINE_CLEARE"></a> <a id="_CPPv2N15jpeg_isr_type_t15JPEG_LINE_CLEARE"></a> <a id="hal__jpeg__types_8h_1ad64e59977e7197df24b45e2f298a4c49aeff6176d725b4991fa67b42403ccc6a1"></a> enumerator JPEG\_LINE\_CLEAR
    :   when used encode yuv data by 8line every time will trigger this isr

    <a id="_CPPv4N15jpeg_isr_type_t14JPEG_FRAME_ERRE"></a>

    <a id="_CPPv3N15jpeg_isr_type_t14JPEG_FRAME_ERRE"></a> <a id="_CPPv2N15jpeg_isr_type_t14JPEG_FRAME_ERRE"></a> <a id="hal__jpeg__types_8h_1ad64e59977e7197df24b45e2f298a4c49af200c15ef96c2a5dd8d07627dba128d1"></a> enumerator JPEG\_FRAME\_ERR
    :   when detect jpeg encode error, will trigger this isr

    <a id="_CPPv4N15jpeg_isr_type_t12JPEG_ISR_MAXE"></a>

    <a id="_CPPv3N15jpeg_isr_type_t12JPEG_ISR_MAXE"></a> <a id="_CPPv2N15jpeg_isr_type_t12JPEG_ISR_MAXE"></a> <a id="hal__jpeg__types_8h_1ad64e59977e7197df24b45e2f298a4c49af992cf48375fdf16cf100114c5017e32"></a> enumerator JPEG\_ISR\_MAX
