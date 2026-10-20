---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_draw_osd.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="draw-osd"></a>

# draw\_osd

<a id="id1"></a>

## 概述

DRAW\_OSD模块提供统一的OSD绘制接口

参考工程：

- 有关draw\_osd的详细信息，请参阅：

  - [draw\_osd开发指南](../../developer-guide/display/draw_osd.md)
- 有关draw\_osd的示例工程，请参阅：

  - [draw\_osd 示例项目](../../examples/projects/draw_osd_example.md)

<a id="draw-osd-api-reference"></a>

## DRAW\_OSD API Reference

<a id="header-file"></a>

### Header File

- [bk\_draw\_osd.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_draw_osd.h)

<a id="functions"></a>

### Functions

<a id="_CPPv417bk_draw_osd_array25bk_draw_osd_ctlr_handle_tP13osd_bg_info_tPK12blend_info_t"></a>

<a id="_CPPv317bk_draw_osd_array25bk_draw_osd_ctlr_handle_tP13osd_bg_info_tPK12blend_info_t"></a> <a id="_CPPv217bk_draw_osd_array25bk_draw_osd_ctlr_handle_tP13osd_bg_info_tPK12blend_info_t"></a> <a id="bk_draw_osd_array__bk_draw_osd_ctlr_handle_t.osd_bg_info_tP.blend_info_tCP"></a> <a id="bk__draw__osd_8h_1a6bb7a97a6bbcc20a599632365f54a146"></a> avdk\_err\_t bk\_draw\_osd\_array([bk\_draw\_osd\_ctlr\_handle\_t](#_CPPv425bk_draw_osd_ctlr_handle_t "bk_draw_osd_ctlr_handle_t") handle, [osd\_bg\_info\_t](#_CPPv413osd_bg_info_t "osd_bg_info_t") \*bg\_info, const [blend\_info\_t](#_CPPv412blend_info_t "blend_info_t") \*info)
:   draw osd array

    参数
    :   - **handle** – osd controller handle
        - **bg\_info** – osd background info
        - **info** – osd info

    返回
    :   avdk\_err\_t

<a id="_CPPv417bk_draw_osd_image25bk_draw_osd_ctlr_handle_tP13osd_bg_info_tPK12blend_info_t"></a>

<a id="_CPPv317bk_draw_osd_image25bk_draw_osd_ctlr_handle_tP13osd_bg_info_tPK12blend_info_t"></a> <a id="_CPPv217bk_draw_osd_image25bk_draw_osd_ctlr_handle_tP13osd_bg_info_tPK12blend_info_t"></a> <a id="bk_draw_osd_image__bk_draw_osd_ctlr_handle_t.osd_bg_info_tP.blend_info_tCP"></a> <a id="bk__draw__osd_8h_1aed5a50b256541c783c02e686db159dd8"></a> avdk\_err\_t bk\_draw\_osd\_image([bk\_draw\_osd\_ctlr\_handle\_t](#_CPPv425bk_draw_osd_ctlr_handle_t "bk_draw_osd_ctlr_handle_t") handle, [osd\_bg\_info\_t](#_CPPv413osd_bg_info_t "osd_bg_info_t") \*bg\_info, const [blend\_info\_t](#_CPPv412blend_info_t "blend_info_t") \*info)
:   draw osd image

    draw osd image

    参数
    :   - **handle** – osd controller handle
        - **bg\_info** – osd background info
        - **info** – osd info
        - **handle** – osd controller handle
        - **bg\_info** – osd background info
        - **info** – osd info

    返回
    :   avdk\_err\_t

    返回
    :   avdk\_err\_t

<a id="_CPPv416bk_draw_osd_font25bk_draw_osd_ctlr_handle_tP13osd_bg_info_tPK12blend_info_t"></a>

<a id="_CPPv316bk_draw_osd_font25bk_draw_osd_ctlr_handle_tP13osd_bg_info_tPK12blend_info_t"></a> <a id="_CPPv216bk_draw_osd_font25bk_draw_osd_ctlr_handle_tP13osd_bg_info_tPK12blend_info_t"></a> <a id="bk_draw_osd_font__bk_draw_osd_ctlr_handle_t.osd_bg_info_tP.blend_info_tCP"></a> <a id="bk__draw__osd_8h_1abb7522c4aeb525355e973aec014adf12"></a> avdk\_err\_t bk\_draw\_osd\_font([bk\_draw\_osd\_ctlr\_handle\_t](#_CPPv425bk_draw_osd_ctlr_handle_t "bk_draw_osd_ctlr_handle_t") handle, [osd\_bg\_info\_t](#_CPPv413osd_bg_info_t "osd_bg_info_t") \*bg\_info, const [blend\_info\_t](#_CPPv412blend_info_t "blend_info_t") \*info)
:   draw osd font

    参数
    :   - **handle** – osd controller handle
        - **bg\_info** – osd background info
        - **info** – osd info

    返回
    :   avdk\_err\_t

<a id="_CPPv425bk_draw_osd_add_or_updata25bk_draw_osd_ctlr_handle_tPKcPKc"></a>

<a id="_CPPv325bk_draw_osd_add_or_updata25bk_draw_osd_ctlr_handle_tPKcPKc"></a> <a id="_CPPv225bk_draw_osd_add_or_updata25bk_draw_osd_ctlr_handle_tPKcPKc"></a> <a id="bk_draw_osd_add_or_updata__bk_draw_osd_ctlr_handle_t.cCP.cCP"></a> <a id="bk__draw__osd_8h_1adf6faf866e71c265487df092dfb7b134"></a> avdk\_err\_t bk\_draw\_osd\_add\_or\_updata([bk\_draw\_osd\_ctlr\_handle\_t](#_CPPv425bk_draw_osd_ctlr_handle_t "bk_draw_osd_ctlr_handle_t") handle, const char \*name, const char \*content)
:   add or updata osd info

    参数
    :   - **handle** – osd controller handle
        - **name** – osd name
        - **content** – osd content

    返回
    :   avdk\_err\_t

<a id="_CPPv417bk_draw_osd_ioctl25bk_draw_osd_ctlr_handle_t8uint32_t8uint32_t8uint32_t8uint32_t"></a>

<a id="_CPPv317bk_draw_osd_ioctl25bk_draw_osd_ctlr_handle_t8uint32_t8uint32_t8uint32_t8uint32_t"></a> <a id="_CPPv217bk_draw_osd_ioctl25bk_draw_osd_ctlr_handle_t8uint32_t8uint32_t8uint32_t8uint32_t"></a> <a id="bk_draw_osd_ioctl__bk_draw_osd_ctlr_handle_t.uint32_t.uint32_t.uint32_t.uint32_t"></a> <a id="bk__draw__osd_8h_1aa2806886f053941da16c30ddeed811c3"></a> avdk\_err\_t bk\_draw\_osd\_ioctl([bk\_draw\_osd\_ctlr\_handle\_t](#_CPPv425bk_draw_osd_ctlr_handle_t "bk_draw_osd_ctlr_handle_t") handle, uint32\_t ioctl\_cmd, uint32\_t param1, uint32\_t param2, uint32\_t param3)
:   osd controller ioctl

    参数
    :   - **handle** – osd controller handle
        - **ioctl\_cmd** – ioctl command
        - **param1** – ioctl param1
        - **param2** – ioctl param2
        - **param3** – ioctl param3

    返回
    :   avdk\_err\_t

<a id="_CPPv418bk_draw_osd_delete25bk_draw_osd_ctlr_handle_t"></a>

<a id="_CPPv318bk_draw_osd_delete25bk_draw_osd_ctlr_handle_t"></a> <a id="_CPPv218bk_draw_osd_delete25bk_draw_osd_ctlr_handle_t"></a> <a id="bk_draw_osd_delete__bk_draw_osd_ctlr_handle_t"></a> <a id="bk__draw__osd_8h_1a9c6c4556668cb102b3bfa8691be47947"></a> avdk\_err\_t bk\_draw\_osd\_delete([bk\_draw\_osd\_ctlr\_handle\_t](#_CPPv425bk_draw_osd_ctlr_handle_t "bk_draw_osd_ctlr_handle_t") handle)
:   delete osd controller

    参数
    :   **handle** – osd controller handle

    返回
    :   avdk\_err\_t

<a id="_CPPv415bk_draw_osd_newP25bk_draw_osd_ctlr_handle_tP17osd_ctlr_config_t"></a>

<a id="_CPPv315bk_draw_osd_newP25bk_draw_osd_ctlr_handle_tP17osd_ctlr_config_t"></a> <a id="_CPPv215bk_draw_osd_newP25bk_draw_osd_ctlr_handle_tP17osd_ctlr_config_t"></a> <a id="bk_draw_osd_new__bk_draw_osd_ctlr_handle_tP.osd_ctlr_config_tP"></a> <a id="bk__draw__osd_8h_1a2d34c074b12042a2da698eb447c02eea"></a> avdk\_err\_t bk\_draw\_osd\_new([bk\_draw\_osd\_ctlr\_handle\_t](#_CPPv425bk_draw_osd_ctlr_handle_t "bk_draw_osd_ctlr_handle_t") \*handle, [osd\_ctlr\_config\_t](#_CPPv417osd_ctlr_config_t "osd_ctlr_config_t") \*config)
:   create osd controller

    参数
    :   - **handle** – osd controller handle
        - **config** – osd controller config

    返回
    :   avdk\_err\_t

<a id="_CPPv418bk_draw_osd_remove25bk_draw_osd_ctlr_handle_tPKc"></a>

<a id="_CPPv318bk_draw_osd_remove25bk_draw_osd_ctlr_handle_tPKc"></a> <a id="_CPPv218bk_draw_osd_remove25bk_draw_osd_ctlr_handle_tPKc"></a> <a id="bk_draw_osd_remove__bk_draw_osd_ctlr_handle_t.cCP"></a> <a id="bk__draw__osd_8h_1a39a4912b44246361f1ce9328df78e68e"></a> avdk\_err\_t bk\_draw\_osd\_remove([bk\_draw\_osd\_ctlr\_handle\_t](#_CPPv425bk_draw_osd_ctlr_handle_t "bk_draw_osd_ctlr_handle_t") handle, const char \*name)
:   remove osd info

    参数
    :   - **handle** – osd controller handle
        - **name** – osd name

    返回
    :   avdk\_err\_t

<a id="draw-osd-api-typedefs"></a>

## DRAW\_OSD API Typedefs

<a id="id4"></a>

### Header File

- [bk\_draw\_osd\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_draw_osd_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv413blend_image_t"></a>

<a id="_CPPv313blend_image_t"></a> <a id="_CPPv213blend_image_t"></a> <a id="blend_image_t"></a> <a id="structblend__image__t"></a> struct blend\_image\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13blend_image_t6formatE"></a>

    <a id="_CPPv3N13blend_image_t6formatE"></a> <a id="_CPPv2N13blend_image_t6formatE"></a> <a id="blend_image_t::format__uint8_t"></a> <a id="structblend__image__t_1a0d7e2c9879ed43a83274ba21008f091f"></a> uint8\_t format
    :   data\_format\_t, should be ARGB8888

    <a id="_CPPv4N13blend_image_t8data_lenE"></a>

    <a id="_CPPv3N13blend_image_t8data_lenE"></a> <a id="_CPPv2N13blend_image_t8data_lenE"></a> <a id="blend_image_t::data_len__uint32_t"></a> <a id="structblend__image__t_1aae09ae4318b656b1ce08d88a1e4e37b6"></a> uint32\_t data\_len
    :   ARGB8888 image size, should be: (xsize \* ysize \* 4\) (no used)

    <a id="_CPPv4N13blend_image_t4dataE"></a>

    <a id="_CPPv3N13blend_image_t4dataE"></a> <a id="_CPPv2N13blend_image_t4dataE"></a> <a id="blend_image_t::data__uint8_tCP"></a> <a id="structblend__image__t_1a329418268dfb9c3abf09662ef3b43272"></a> const uint8\_t \*data
    :   ARGB8888 image data

<a id="_CPPv412blend_font_t"></a>

<a id="_CPPv312blend_font_t"></a> <a id="_CPPv212blend_font_t"></a> <a id="blend_font_t"></a> <a id="structblend__font__t"></a> struct blend\_font\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12blend_font_t15font_digit_typeE"></a>

    <a id="_CPPv3N12blend_font_t15font_digit_typeE"></a> <a id="_CPPv2N12blend_font_t15font_digit_typeE"></a> <a id="blend_font_t::font_digit_type__gui_font_digit_structCP"></a> <a id="structblend__font__t_1aa10e78954f0c744ec100f76dcc93a65d"></a> const gui\_font\_digit\_struct \*font\_digit\_type
    :   character database

    <a id="_CPPv4N12blend_font_t5colorE"></a>

    <a id="_CPPv3N12blend_font_t5colorE"></a> <a id="_CPPv2N12blend_font_t5colorE"></a> <a id="blend_font_t::color__uint32_t"></a> <a id="structblend__font__t_1aa6a8d8227306f09c079b4e3404ca8390"></a> uint32\_t color
    :   font color value used by RGB565 date

<a id="_CPPv410bk_blend_t"></a>

<a id="_CPPv310bk_blend_t"></a> <a id="_CPPv210bk_blend_t"></a> <a id="bk_blend_t"></a> <a id="structbk__blend__t"></a> struct bk\_blend\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N10bk_blend_t7versionE"></a>

    <a id="_CPPv3N10bk_blend_t7versionE"></a> <a id="_CPPv2N10bk_blend_t7versionE"></a> <a id="bk_blend_t::version__uint8_t"></a> <a id="structbk__blend__t_1a3e4a511873dfa48f8f8b7db0d1210873"></a> uint8\_t version
    :   version

    <a id="_CPPv4N10bk_blend_t10blend_typeE"></a>

    <a id="_CPPv3N10bk_blend_t10blend_typeE"></a> <a id="_CPPv2N10bk_blend_t10blend_typeE"></a> <a id="bk_blend_t::blend_type__blend_type_t"></a> <a id="structbk__blend__t_1a3026fcd077a8af77c5ad4fa1d21d7492"></a> [blend\_type\_t](#_CPPv412blend_type_t "blend_type_t") blend\_type
    :   0: image, 1:font

    <a id="_CPPv4N10bk_blend_t4nameE"></a>

    <a id="_CPPv3N10bk_blend_t4nameE"></a> <a id="_CPPv2N10bk_blend_t4nameE"></a> <a id="bk_blend_t::name__cCA"></a> <a id="structbk__blend__t_1acdb970c96afd2c07f1239600796e301a"></a> const char name\[MAX\_BLEND\_NAME\_LEN\]
    :   image name like “wifi”,”clock”, “weather”

    <a id="_CPPv4N10bk_blend_t5widthE"></a>

    <a id="_CPPv3N10bk_blend_t5widthE"></a> <a id="_CPPv2N10bk_blend_t5widthE"></a> <a id="bk_blend_t::width__uint32_t"></a> <a id="structbk__blend__t_1a5ae39b2066e0109564def8bb6b96308d"></a> uint32\_t width
    :   icon width

    <a id="_CPPv4N10bk_blend_t6heightE"></a>

    <a id="_CPPv3N10bk_blend_t6heightE"></a> <a id="_CPPv2N10bk_blend_t6heightE"></a> <a id="bk_blend_t::height__uint32_t"></a> <a id="structbk__blend__t_1aa60b7e922a416e2fac2e6225c203d965"></a> uint32\_t height
    :   icon height

    <a id="_CPPv4N10bk_blend_t10icon_widthE"></a>

    <a id="_CPPv3N10bk_blend_t10icon_widthE"></a> <a id="_CPPv2N10bk_blend_t10icon_widthE"></a> <a id="bk_blend_t::icon_width__uint32_t"></a> <a id="structbk__blend__t_1a76aa0b482d0c61b60732a689583e325b"></a> uint32\_t icon\_width
    :   icon width

    <a id="_CPPv4N10bk_blend_t11icon_heightE"></a>

    <a id="_CPPv3N10bk_blend_t11icon_heightE"></a> <a id="_CPPv2N10bk_blend_t11icon_heightE"></a> <a id="bk_blend_t::icon_height__uint32_t"></a> <a id="structbk__blend__t_1a464414691fbc2b6d2c6f497312422e5f"></a> uint32\_t icon\_height
    :   icon height

    <a id="_CPPv4N10bk_blend_t8bg_widthE"></a>

    <a id="_CPPv3N10bk_blend_t8bg_widthE"></a> <a id="_CPPv2N10bk_blend_t8bg_widthE"></a> <a id="bk_blend_t::bg_width__uint32_t"></a> <a id="structbk__blend__t_1a782213be2ac28b0f423ecd1ef39c87de"></a> uint32\_t bg\_width
    :   background window width

    <a id="_CPPv4N10bk_blend_t9bg_heightE"></a>

    <a id="_CPPv3N10bk_blend_t9bg_heightE"></a> <a id="_CPPv2N10bk_blend_t9bg_heightE"></a> <a id="bk_blend_t::bg_height__uint32_t"></a> <a id="structbk__blend__t_1a30b1d1fe1492c8e5ae43d8437b9d7bad"></a> uint32\_t bg\_height
    :   background window height

    <a id="_CPPv4N10bk_blend_t4xposE"></a>

    <a id="_CPPv3N10bk_blend_t4xposE"></a> <a id="_CPPv2N10bk_blend_t4xposE"></a> <a id="bk_blend_t::xpos__uint16_t"></a> <a id="structbk__blend__t_1aff49bd49f7844074f8b88eef2dd36010"></a> uint16\_t xpos
    :   icon x pos based on background window

    <a id="_CPPv4N10bk_blend_t4yposE"></a>

    <a id="_CPPv3N10bk_blend_t4yposE"></a> <a id="_CPPv2N10bk_blend_t4yposE"></a> <a id="bk_blend_t::ypos__uint16_t"></a> <a id="structbk__blend__t_1a0689df1d2cb0fb1cdb4936b42039454b"></a> uint16\_t ypos
    :   icon y pos based on background window

<a id="_CPPv412blend_info_t"></a>

<a id="_CPPv312blend_info_t"></a> <a id="_CPPv212blend_info_t"></a> <a id="blend_info_t"></a> <a id="structblend__info__t"></a> struct blend\_info\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12blend_info_t4nameE"></a>

    <a id="_CPPv3N12blend_info_t4nameE"></a> <a id="_CPPv2N12blend_info_t4nameE"></a> <a id="blend_info_t::name__cA"></a> <a id="structblend__info__t_1addd3e12bf533251052cc5eaff6018151"></a> char name\[MAX\_BLEND\_NAME\_LEN\]
    :   name like “wifi”,”clock”, “weather”

    <a id="_CPPv4N12blend_info_t4addrE"></a>

    <a id="_CPPv3N12blend_info_t4addrE"></a> <a id="_CPPv2N12blend_info_t4addrE"></a> <a id="blend_info_t::addr__bk_blend_tCP"></a> <a id="structblend__info__t_1a6692d279d973a6166980bac6e5507c9a"></a> const [bk\_blend\_t](#_CPPv410bk_blend_t "bk_blend_t") \*addr
    :   the pointer, pointer to the struct

    <a id="_CPPv4N12blend_info_t7contentE"></a>

    <a id="_CPPv3N12blend_info_t7contentE"></a> <a id="_CPPv2N12blend_info_t7contentE"></a> <a id="blend_info_t::content__cA"></a> <a id="structblend__info__t_1ab87bee4d3e7e00873de6d478c816e5f0"></a> char content\[MAX\_BLEND\_CONTENT\_LEN\]
    :   content like “wifi0”, “12:00”,”v 1.0.0”

<a id="_CPPv415dynamic_array_t"></a>

<a id="_CPPv315dynamic_array_t"></a> <a id="_CPPv215dynamic_array_t"></a> <a id="dynamic_array_t"></a> <a id="structdynamic__array__t"></a> struct dynamic\_array\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15dynamic_array_t5entryE"></a>

    <a id="_CPPv3N15dynamic_array_t5entryE"></a> <a id="_CPPv2N15dynamic_array_t5entryE"></a> <a id="dynamic_array_t::entry__blend_info_tP"></a> <a id="structdynamic__array__t_1aaf045ec17b7cf415c3a14d489add19de"></a> [blend\_info\_t](#_CPPv412blend_info_t "blend_info_t") \*entry
    :   the pointer, pointer to the struct array

    <a id="_CPPv4N15dynamic_array_t4sizeE"></a>

    <a id="_CPPv3N15dynamic_array_t4sizeE"></a> <a id="_CPPv2N15dynamic_array_t4sizeE"></a> <a id="dynamic_array_t::size__s"></a> <a id="structdynamic__array__t_1ad2d268c07ac478739549ce242976f676"></a> size\_t size
    :   the size of the struct array

    <a id="_CPPv4N15dynamic_array_t8capacityE"></a>

    <a id="_CPPv3N15dynamic_array_t8capacityE"></a> <a id="_CPPv2N15dynamic_array_t8capacityE"></a> <a id="dynamic_array_t::capacity__s"></a> <a id="structdynamic__array__t_1ae9f388afdcf587c0d37db84beca7def4"></a> size\_t capacity
    :   the capacity of the struct array

<a id="_CPPv417osd_ctlr_config_t"></a>

<a id="_CPPv317osd_ctlr_config_t"></a> <a id="_CPPv217osd_ctlr_config_t"></a> <a id="osd_ctlr_config_t"></a> <a id="structosd__ctlr__config__t"></a> struct osd\_ctlr\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17osd_ctlr_config_t12blend_assetsE"></a>

    <a id="_CPPv3N17osd_ctlr_config_t12blend_assetsE"></a> <a id="_CPPv2N17osd_ctlr_config_t12blend_assetsE"></a> <a id="osd_ctlr_config_t::blend_assets__blend_info_tCP"></a> <a id="structosd__ctlr__config__t_1a11569d1a24fd21c07161c20286a8b5ae"></a> const [blend\_info\_t](#_CPPv412blend_info_t "blend_info_t") \*blend\_assets
    :   the pointer, pointer to the struct all blend assetsarray

    <a id="_CPPv4N17osd_ctlr_config_t10blend_infoE"></a>

    <a id="_CPPv3N17osd_ctlr_config_t10blend_infoE"></a> <a id="_CPPv2N17osd_ctlr_config_t10blend_infoE"></a> <a id="osd_ctlr_config_t::blend_info__blend_info_tCP"></a> <a id="structosd__ctlr__config__t_1a2712b57e00b2b1d7de1c68e6e21cee8c"></a> const [blend\_info\_t](#_CPPv412blend_info_t "blend_info_t") \*blend\_info
    :   the pointer, pointer to current blend info

    <a id="_CPPv4N17osd_ctlr_config_t13draw_in_psramE"></a>

    <a id="_CPPv3N17osd_ctlr_config_t13draw_in_psramE"></a> <a id="_CPPv2N17osd_ctlr_config_t13draw_in_psramE"></a> <a id="osd_ctlr_config_t::draw_in_psram__b"></a> <a id="structosd__ctlr__config__t_1aacdf71ffe8ec50cd83fb23a173010c8d"></a> bool draw\_in\_psram
    :   true: use PSRAM, false: use SRAM

<a id="_CPPv413osd_bg_info_t"></a>

<a id="_CPPv313osd_bg_info_t"></a> <a id="_CPPv213osd_bg_info_t"></a> <a id="osd_bg_info_t"></a> <a id="structosd__bg__info__t"></a> struct osd\_bg\_info\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13osd_bg_info_t5frameE"></a>

    <a id="_CPPv3N13osd_bg_info_t5frameE"></a> <a id="_CPPv2N13osd_bg_info_t5frameE"></a> <a id="osd_bg_info_t::frame__frame_buffer_tP"></a> <a id="structosd__bg__info__t_1a92b88d4a3c502806aa6dcf21d7800774"></a> frame\_buffer\_t \*frame
    :   the pointer, pointer to the struct frame buffer

    <a id="_CPPv4N13osd_bg_info_t5widthE"></a>

    <a id="_CPPv3N13osd_bg_info_t5widthE"></a> <a id="_CPPv2N13osd_bg_info_t5widthE"></a> <a id="osd_bg_info_t::width__uint16_t"></a> <a id="structosd__bg__info__t_1a27c9536fa2dbda094ba75b0b8e38fe21"></a> uint16\_t width
    :   osd draw visible width

    <a id="_CPPv4N13osd_bg_info_t6heightE"></a>

    <a id="_CPPv3N13osd_bg_info_t6heightE"></a> <a id="_CPPv2N13osd_bg_info_t6heightE"></a> <a id="osd_bg_info_t::height__uint16_t"></a> <a id="structosd__bg__info__t_1abb14c5bb30affd32a4c1041e73996c03"></a> uint16\_t height
    :   osd draw visible height

<a id="_CPPv416bk_draw_osd_ctlr"></a>

<a id="_CPPv316bk_draw_osd_ctlr"></a> <a id="_CPPv216bk_draw_osd_ctlr"></a> <a id="bk_draw_osd_ctlr"></a> <a id="structbk__draw__osd__ctlr"></a> struct bk\_draw\_osd\_ctlr

<a id="macros"></a>

### Macros

<a id="c.MAX_BLEND_NAME_LEN"></a>

<a id="bk__draw__osd__types_8h_1a7d18436b6301d0dc32d63f8a4080e046"></a> MAX\_BLEND\_NAME\_LEN

<a id="c.MAX_BLEND_CONTENT_LEN"></a>

<a id="bk__draw__osd__types_8h_1a07da951199913f59b3557415ac3858c3"></a> MAX\_BLEND\_CONTENT\_LEN

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv425bk_draw_osd_ctlr_handle_t"></a>

<a id="_CPPv325bk_draw_osd_ctlr_handle_t"></a> <a id="_CPPv225bk_draw_osd_ctlr_handle_t"></a> <a id="bk_draw_osd_ctlr_handle_t"></a> <a id="bk__draw__osd__types_8h_1a4a16836d5194a89c2bc7836d4da270c0"></a> typedef struct [bk\_draw\_osd\_ctlr](#_CPPv416bk_draw_osd_ctlr "bk_draw_osd_ctlr") \*bk\_draw\_osd\_ctlr\_handle\_t

<a id="_CPPv418bk_draw_osd_ctlr_t"></a>

<a id="_CPPv318bk_draw_osd_ctlr_t"></a> <a id="_CPPv218bk_draw_osd_ctlr_t"></a> <a id="bk_draw_osd_ctlr_t"></a> <a id="bk__draw__osd__types_8h_1a349c6500d10c42d2766f5195d3f70104"></a> typedef struct [bk\_draw\_osd\_ctlr](#_CPPv416bk_draw_osd_ctlr "bk_draw_osd_ctlr") bk\_draw\_osd\_ctlr\_t

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv415osd_ioctl_cmd_t"></a>

<a id="_CPPv315osd_ioctl_cmd_t"></a> <a id="_CPPv215osd_ioctl_cmd_t"></a> <a id="bk__draw__osd__types_8h_1a54b2e4561257d14a4adcdbfe3057f1a4"></a> enum osd\_ioctl\_cmd\_t
:   *Values:*

    <a id="_CPPv4N15osd_ioctl_cmd_t28OSD_CTLR_CMD_SET_PSRAM_USAGEE"></a>

    <a id="_CPPv3N15osd_ioctl_cmd_t28OSD_CTLR_CMD_SET_PSRAM_USAGEE"></a> <a id="_CPPv2N15osd_ioctl_cmd_t28OSD_CTLR_CMD_SET_PSRAM_USAGEE"></a> <a id="bk__draw__osd__types_8h_1a54b2e4561257d14a4adcdbfe3057f1a4a0b98c80815267b36fd6ee1028dc56c5a"></a> enumerator OSD\_CTLR\_CMD\_SET\_PSRAM\_USAGE
    :   set use psram

    <a id="_CPPv4N15osd_ioctl_cmd_t28OSD_CTLR_CMD_GET_PSRAM_USAGEE"></a>

    <a id="_CPPv3N15osd_ioctl_cmd_t28OSD_CTLR_CMD_GET_PSRAM_USAGEE"></a> <a id="_CPPv2N15osd_ioctl_cmd_t28OSD_CTLR_CMD_GET_PSRAM_USAGEE"></a> <a id="bk__draw__osd__types_8h_1a54b2e4561257d14a4adcdbfe3057f1a4a9c4bf6ba77ca909c81fa8df2bfde71ee"></a> enumerator OSD\_CTLR\_CMD\_GET\_PSRAM\_USAGE
    :   get psram usage status

    <a id="_CPPv4N15osd_ioctl_cmd_t27OSD_CTLR_CMD_GET_ALL_ASSETSE"></a>

    <a id="_CPPv3N15osd_ioctl_cmd_t27OSD_CTLR_CMD_GET_ALL_ASSETSE"></a> <a id="_CPPv2N15osd_ioctl_cmd_t27OSD_CTLR_CMD_GET_ALL_ASSETSE"></a> <a id="bk__draw__osd__types_8h_1a54b2e4561257d14a4adcdbfe3057f1a4aeb6edf28c521b12a3b1aaa1ace1c0759"></a> enumerator OSD\_CTLR\_CMD\_GET\_ALL\_ASSETS
    :   get all blend\_info

    <a id="_CPPv4N15osd_ioctl_cmd_t26OSD_CTLR_CMD_GET_DRAW_INFOE"></a>

    <a id="_CPPv3N15osd_ioctl_cmd_t26OSD_CTLR_CMD_GET_DRAW_INFOE"></a> <a id="_CPPv2N15osd_ioctl_cmd_t26OSD_CTLR_CMD_GET_DRAW_INFOE"></a> <a id="bk__draw__osd__types_8h_1a54b2e4561257d14a4adcdbfe3057f1a4a6b43f5ae0c4b1a9a1348fe43428f6df6"></a> enumerator OSD\_CTLR\_CMD\_GET\_DRAW\_INFO
    :   get current blend osd info

<a id="_CPPv412blend_type_t"></a>

<a id="_CPPv312blend_type_t"></a> <a id="_CPPv212blend_type_t"></a> <a id="bk__draw__osd__types_8h_1ada197263dd575617a809f29ec0bd790f"></a> enum blend\_type\_t
:   *Values:*

    <a id="_CPPv4N12blend_type_t16BLEND_TYPE_IMAGEE"></a>

    <a id="_CPPv3N12blend_type_t16BLEND_TYPE_IMAGEE"></a> <a id="_CPPv2N12blend_type_t16BLEND_TYPE_IMAGEE"></a> <a id="bk__draw__osd__types_8h_1ada197263dd575617a809f29ec0bd790fad601fca166e2de5ea39c73756ab5094f"></a> enumerator BLEND\_TYPE\_IMAGE
    :   image type

    <a id="_CPPv4N12blend_type_t15BLEND_TYPE_FONTE"></a>

    <a id="_CPPv3N12blend_type_t15BLEND_TYPE_FONTE"></a> <a id="_CPPv2N12blend_type_t15BLEND_TYPE_FONTE"></a> <a id="bk__draw__osd__types_8h_1ada197263dd575617a809f29ec0bd790fa80420db9eb65857fa916c9550a7a16ab"></a> enumerator BLEND\_TYPE\_FONT
    :   font type
