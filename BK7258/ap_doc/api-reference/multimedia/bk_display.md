---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/multimedia/bk_display.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="display"></a>

# display

<a id="id1"></a>

## 概述

Display模块提供统一的显示控制器管理接口

参考工程：

- 有关display的详细信息，请参阅：

  - [rgb display开发指南](../../developer-guide/display/rgb_lcd_display.md)
  - [mcu display开发指南](../../developer-guide/display/mcu_lcd_display.md)
  - [qspi display开发指南](../../developer-guide/display/qspi_lcd_display.md)
  - [spi display开发指南](../../developer-guide/display/spi_lcd_display.md)
- 有关display的示例工程，请参阅：

  - [rgb display 示例项目](../../examples/projects/rgb_lcd_example.md)
  - [mcu display 示例项目](../../examples/projects/mcu_lcd_example.md)
  - [qspi display 示例项目](../../examples/projects/qspi_lcd_example.md)
  - [spi display 示例项目](../../examples/projects/spi_lcd_example.md)

<a id="display-api-reference"></a>

## DISPLAY API Reference

<a id="header-file"></a>

### Header File

- [bk\_display.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_display.h)

<a id="functions"></a>

### Functions

<a id="_CPPv415bk_display_open24bk_display_ctlr_handle_t"></a>

<a id="_CPPv315bk_display_open24bk_display_ctlr_handle_t"></a> <a id="_CPPv215bk_display_open24bk_display_ctlr_handle_t"></a> <a id="bk_display_open__bk_display_ctlr_handle_t"></a> <a id="bk__display_8h_1a030b071e195b635be7cfe2d4b211ba92"></a> avdk\_err\_t bk\_display\_open([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") handle)
:   Open display controller.

    参数
    :   **handle** – Display controller handle

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv416bk_display_close24bk_display_ctlr_handle_t"></a>

<a id="_CPPv316bk_display_close24bk_display_ctlr_handle_t"></a> <a id="_CPPv216bk_display_close24bk_display_ctlr_handle_t"></a> <a id="bk_display_close__bk_display_ctlr_handle_t"></a> <a id="bk__display_8h_1ae41fa37af8c496b422640aab221cc458"></a> avdk\_err\_t bk\_display\_close([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") handle)
:   Close display controller.

    参数
    :   **handle** – Display controller handle

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv417bk_display_delete24bk_display_ctlr_handle_t"></a>

<a id="_CPPv317bk_display_delete24bk_display_ctlr_handle_t"></a> <a id="_CPPv217bk_display_delete24bk_display_ctlr_handle_t"></a> <a id="bk_display_delete__bk_display_ctlr_handle_t"></a> <a id="bk__display_8h_1a7db92effb0103419b63e0059d00826a8"></a> avdk\_err\_t bk\_display\_delete([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") handle)
:   Delete display controller.

    参数
    :   **handle** – Display controller handle

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv416bk_display_flush24bk_display_ctlr_handle_tP14frame_buffer_tPF8bk_err_tPvE"></a>

<a id="_CPPv316bk_display_flush24bk_display_ctlr_handle_tP14frame_buffer_tPF8bk_err_tPvE"></a> <a id="_CPPv216bk_display_flush24bk_display_ctlr_handle_tP14frame_buffer_tPF8bk_err_tPvE"></a> <a id="bk__display_8h_1a7e66e10833f93930e3a445097d573437"></a> avdk\_err\_t bk\_display\_flush([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") handle, frame\_buffer\_t \*frame, [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*free\_t)(void \*args))
:   Flush display content.

    参数
    :   - **handle** – Display controller handle
        - **frame** – Frame data to be displayed
        - **free\_t** – Frame data release callback function

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv416bk_display_ioctl24bk_display_ctlr_handle_t8uint32_tPv"></a>

<a id="_CPPv316bk_display_ioctl24bk_display_ctlr_handle_t8uint32_tPv"></a> <a id="_CPPv216bk_display_ioctl24bk_display_ctlr_handle_t8uint32_tPv"></a> <a id="bk_display_ioctl__bk_display_ctlr_handle_t.uint32_t.voidP"></a> <a id="bk__display_8h_1a5f2e2581074c2c080e658fc6e097af0f"></a> avdk\_err\_t bk\_display\_ioctl([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") handle, uint32\_t cmd, void \*arg)
:   Control IO operations of display controller.

    参数
    :   - **handle** – Display controller handle
        - **cmd** – IO control command
        - **param** – Command data

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv418bk_display_mcu_newP24bk_display_ctlr_handle_tP28bk_display_mcu_ctlr_config_t"></a>

<a id="_CPPv318bk_display_mcu_newP24bk_display_ctlr_handle_tP28bk_display_mcu_ctlr_config_t"></a> <a id="_CPPv218bk_display_mcu_newP24bk_display_ctlr_handle_tP28bk_display_mcu_ctlr_config_t"></a> <a id="bk_display_mcu_new__bk_display_ctlr_handle_tP.bk_display_mcu_ctlr_config_tP"></a> <a id="bk__display_8h_1af05a22323deac641e378d993b7b57b5f"></a> avdk\_err\_t bk\_display\_mcu\_new([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") \*handle, [bk\_display\_mcu\_ctlr\_config\_t](#_CPPv428bk_display_mcu_ctlr_config_t "bk_display_mcu_ctlr_config_t") \*config)
:   Create MCU display controller.

    参数
    :   - **handle** – Output parameter, used to store the created display controller handle
        - **config** – MCU display controller configuration parameters

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv418bk_display_rgb_newP24bk_display_ctlr_handle_tP28bk_display_rgb_ctlr_config_t"></a>

<a id="_CPPv318bk_display_rgb_newP24bk_display_ctlr_handle_tP28bk_display_rgb_ctlr_config_t"></a> <a id="_CPPv218bk_display_rgb_newP24bk_display_ctlr_handle_tP28bk_display_rgb_ctlr_config_t"></a> <a id="bk_display_rgb_new__bk_display_ctlr_handle_tP.bk_display_rgb_ctlr_config_tP"></a> <a id="bk__display_8h_1a9b78c167ad9a7b183618c791bce20531"></a> avdk\_err\_t bk\_display\_rgb\_new([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") \*handle, [bk\_display\_rgb\_ctlr\_config\_t](#_CPPv428bk_display_rgb_ctlr_config_t "bk_display_rgb_ctlr_config_t") \*config)
:   Create RGB display controller.

    参数
    :   - **handle** – Output parameter, used to store the created display controller handle
        - **config** – RGB display controller configuration parameters

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv418bk_display_spi_newP24bk_display_ctlr_handle_tP28bk_display_spi_ctlr_config_t"></a>

<a id="_CPPv318bk_display_spi_newP24bk_display_ctlr_handle_tP28bk_display_spi_ctlr_config_t"></a> <a id="_CPPv218bk_display_spi_newP24bk_display_ctlr_handle_tP28bk_display_spi_ctlr_config_t"></a> <a id="bk_display_spi_new__bk_display_ctlr_handle_tP.bk_display_spi_ctlr_config_tP"></a> <a id="bk__display_8h_1a7738ec0636fd77a2a0df718cbfafc761"></a> avdk\_err\_t bk\_display\_spi\_new([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") \*handle, [bk\_display\_spi\_ctlr\_config\_t](#_CPPv428bk_display_spi_ctlr_config_t "bk_display_spi_ctlr_config_t") \*config)
:   Create SPI display controller.

    参数
    :   - **handle** – Output parameter, used to store the created display controller handle
        - **config** – SPI display controller configuration parameters

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv419bk_display_qspi_newP24bk_display_ctlr_handle_tP29bk_display_qspi_ctlr_config_t"></a>

<a id="_CPPv319bk_display_qspi_newP24bk_display_ctlr_handle_tP29bk_display_qspi_ctlr_config_t"></a> <a id="_CPPv219bk_display_qspi_newP24bk_display_ctlr_handle_tP29bk_display_qspi_ctlr_config_t"></a> <a id="bk_display_qspi_new__bk_display_ctlr_handle_tP.bk_display_qspi_ctlr_config_tP"></a> <a id="bk__display_8h_1a2f9f554c7c0ad8d5534b901792883cd7"></a> avdk\_err\_t bk\_display\_qspi\_new([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") \*handle, [bk\_display\_qspi\_ctlr\_config\_t](#_CPPv429bk_display_qspi_ctlr_config_t "bk_display_qspi_ctlr_config_t") \*config)
:   Create QSPI display controller.

    参数
    :   - **handle** – Output parameter, used to store the created display controller handle
        - **config** – QSPI display controller configuration parameters

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv424bk_display_dual_qspi_newP24bk_display_ctlr_handle_tP34bk_display_dual_qspi_ctlr_config_t"></a>

<a id="_CPPv324bk_display_dual_qspi_newP24bk_display_ctlr_handle_tP34bk_display_dual_qspi_ctlr_config_t"></a> <a id="_CPPv224bk_display_dual_qspi_newP24bk_display_ctlr_handle_tP34bk_display_dual_qspi_ctlr_config_t"></a> <a id="bk_display_dual_qspi_new__bk_display_ctlr_handle_tP.bk_display_dual_qspi_ctlr_config_tP"></a> <a id="bk__display_8h_1ad20233c01a5d4c9b946a9284900185cb"></a> avdk\_err\_t bk\_display\_dual\_qspi\_new([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") \*handle, [bk\_display\_dual\_qspi\_ctlr\_config\_t](#_CPPv434bk_display_dual_qspi_ctlr_config_t "bk_display_dual_qspi_ctlr_config_t") \*config)
:   Create Dual QSPI display controller.

    参数
    :   - **handle** – Output parameter, used to store the created display controller handle
        - **config** – Dual QSPI display controller configuration parameters

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="_CPPv423bk_display_dual_spi_newP24bk_display_ctlr_handle_tP33bk_display_dual_spi_ctlr_config_t"></a>

<a id="_CPPv323bk_display_dual_spi_newP24bk_display_ctlr_handle_tP33bk_display_dual_spi_ctlr_config_t"></a> <a id="_CPPv223bk_display_dual_spi_newP24bk_display_ctlr_handle_tP33bk_display_dual_spi_ctlr_config_t"></a> <a id="bk_display_dual_spi_new__bk_display_ctlr_handle_tP.bk_display_dual_spi_ctlr_config_tP"></a> <a id="bk__display_8h_1ad3463269089c3e43ed603673a499f684"></a> avdk\_err\_t bk\_display\_dual\_spi\_new([bk\_display\_ctlr\_handle\_t](#_CPPv424bk_display_ctlr_handle_t "bk_display_ctlr_handle_t") \*handle, [bk\_display\_dual\_spi\_ctlr\_config\_t](#_CPPv433bk_display_dual_spi_ctlr_config_t "bk_display_dual_spi_ctlr_config_t") \*config)
:   Create Dual SPI display controller.

    参数
    :   - **handle** – Output parameter, used to store the created display controller handle
        - **config** – Dual SPI display controller configuration parameters

    返回
    :   Operation result, AVDK\_ERR\_OK indicates success

<a id="display-typedefs"></a>

## DISPLAY Typedefs

<a id="id6"></a>

### Header File

- [bk\_display\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_display_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv428bk_display_rgb_ctlr_config_t"></a>

<a id="_CPPv328bk_display_rgb_ctlr_config_t"></a> <a id="_CPPv228bk_display_rgb_ctlr_config_t"></a> <a id="bk_display_rgb_ctlr_config_t"></a> <a id="structbk__display__rgb__ctlr__config__t"></a> struct bk\_display\_rgb\_ctlr\_config\_t
:   RGB display controller configuration structure.

    Used to configure LCD display controller with RGB interface, including device name, LCD device information and SPI IO configuration

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N28bk_display_rgb_ctlr_config_t10lcd_deviceE"></a>

    <a id="_CPPv3N28bk_display_rgb_ctlr_config_t10lcd_deviceE"></a> <a id="_CPPv2N28bk_display_rgb_ctlr_config_t10lcd_deviceE"></a> <a id="bk_display_rgb_ctlr_config_t::lcd_device__lcd_device_tCP"></a> <a id="structbk__display__rgb__ctlr__config__t_1a7513cda15b1f76a6298f13dee120aacd"></a> const [lcd\_device\_t](#_CPPv412lcd_device_t "lcd_device_t") \*lcd\_device
    :   LCD device configuration structure pointer, containing display parameters and initialization commands

    <a id="_CPPv4N28bk_display_rgb_ctlr_config_t7clk_pinE"></a>

    <a id="_CPPv3N28bk_display_rgb_ctlr_config_t7clk_pinE"></a> <a id="_CPPv2N28bk_display_rgb_ctlr_config_t7clk_pinE"></a> <a id="bk_display_rgb_ctlr_config_t::clk_pin__int8_t"></a> <a id="structbk__display__rgb__ctlr__config__t_1ad01357e243d5ad2faeb030e112e6c84d"></a> int8\_t clk\_pin
    :   spi clk io pin

    <a id="_CPPv4N28bk_display_rgb_ctlr_config_t6cs_pinE"></a>

    <a id="_CPPv3N28bk_display_rgb_ctlr_config_t6cs_pinE"></a> <a id="_CPPv2N28bk_display_rgb_ctlr_config_t6cs_pinE"></a> <a id="bk_display_rgb_ctlr_config_t::cs_pin__int8_t"></a> <a id="structbk__display__rgb__ctlr__config__t_1ab028584bf66e37c6bcfc9d8833536842"></a> int8\_t cs\_pin
    :   cs io pin

    <a id="_CPPv4N28bk_display_rgb_ctlr_config_t7sda_pinE"></a>

    <a id="_CPPv3N28bk_display_rgb_ctlr_config_t7sda_pinE"></a> <a id="_CPPv2N28bk_display_rgb_ctlr_config_t7sda_pinE"></a> <a id="bk_display_rgb_ctlr_config_t::sda_pin__int8_t"></a> <a id="structbk__display__rgb__ctlr__config__t_1aefcea544e7ae7b14fa4749a1333721bd"></a> int8\_t sda\_pin
    :   sda io pin

    <a id="_CPPv4N28bk_display_rgb_ctlr_config_t7rst_pinE"></a>

    <a id="_CPPv3N28bk_display_rgb_ctlr_config_t7rst_pinE"></a> <a id="_CPPv2N28bk_display_rgb_ctlr_config_t7rst_pinE"></a> <a id="bk_display_rgb_ctlr_config_t::rst_pin__int8_t"></a> <a id="structbk__display__rgb__ctlr__config__t_1aa4b6e9f5a4049cd56fe92e4607e415ea"></a> int8\_t rst\_pin
    :   lcd reset io pin

<a id="_CPPv428bk_display_mcu_ctlr_config_t"></a>

<a id="_CPPv328bk_display_mcu_ctlr_config_t"></a> <a id="_CPPv228bk_display_mcu_ctlr_config_t"></a> <a id="bk_display_mcu_ctlr_config_t"></a> <a id="structbk__display__mcu__ctlr__config__t"></a> struct bk\_display\_mcu\_ctlr\_config\_t
:   MCU display controller configuration structure.

    Used to configure LCD display controller with MCU interface, including device name and LCD device information

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N28bk_display_mcu_ctlr_config_t10lcd_deviceE"></a>

    <a id="_CPPv3N28bk_display_mcu_ctlr_config_t10lcd_deviceE"></a> <a id="_CPPv2N28bk_display_mcu_ctlr_config_t10lcd_deviceE"></a> <a id="bk_display_mcu_ctlr_config_t::lcd_device__lcd_device_tCP"></a> <a id="structbk__display__mcu__ctlr__config__t_1a60e49c593c389d2a1b7b5439bfbcbf9c"></a> const [lcd\_device\_t](#_CPPv412lcd_device_t "lcd_device_t") \*lcd\_device
    :   LCD device configuration structure pointer, containing display parameters and initialization commands

    <a id="_CPPv4N28bk_display_mcu_ctlr_config_t6te_pinE"></a>

    <a id="_CPPv3N28bk_display_mcu_ctlr_config_t6te_pinE"></a> <a id="_CPPv2N28bk_display_mcu_ctlr_config_t6te_pinE"></a> <a id="bk_display_mcu_ctlr_config_t::te_pin__int8_t"></a> <a id="structbk__display__mcu__ctlr__config__t_1a6e60091360417880bcb320fd477e283c"></a> int8\_t te\_pin
    :   lcd te io pin

<a id="_CPPv429bk_display_qspi_ctlr_config_t"></a>

<a id="_CPPv329bk_display_qspi_ctlr_config_t"></a> <a id="_CPPv229bk_display_qspi_ctlr_config_t"></a> <a id="bk_display_qspi_ctlr_config_t"></a> <a id="structbk__display__qspi__ctlr__config__t"></a> struct bk\_display\_qspi\_ctlr\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N29bk_display_qspi_ctlr_config_t10lcd_deviceE"></a>

    <a id="_CPPv3N29bk_display_qspi_ctlr_config_t10lcd_deviceE"></a> <a id="_CPPv2N29bk_display_qspi_ctlr_config_t10lcd_deviceE"></a> <a id="bk_display_qspi_ctlr_config_t::lcd_device__lcd_device_tCP"></a> <a id="structbk__display__qspi__ctlr__config__t_1a315acab5cad037ea9dc61026b8a55acb"></a> const [lcd\_device\_t](#_CPPv412lcd_device_t "lcd_device_t") \*lcd\_device
    :   LCD device configuration structure pointer, containing display parameters and initialization commands

    <a id="_CPPv4N29bk_display_qspi_ctlr_config_t7qspi_idE"></a>

    <a id="_CPPv3N29bk_display_qspi_ctlr_config_t7qspi_idE"></a> <a id="_CPPv2N29bk_display_qspi_ctlr_config_t7qspi_idE"></a> <a id="bk_display_qspi_ctlr_config_t::qspi_id__uint8_t"></a> <a id="structbk__display__qspi__ctlr__config__t_1a3d62325bef34c188f6ef40d77bcfaf0e"></a> uint8\_t qspi\_id
    :   qspi\_id

    <a id="_CPPv4N29bk_display_qspi_ctlr_config_t9reset_pinE"></a>

    <a id="_CPPv3N29bk_display_qspi_ctlr_config_t9reset_pinE"></a> <a id="_CPPv2N29bk_display_qspi_ctlr_config_t9reset_pinE"></a> <a id="bk_display_qspi_ctlr_config_t::reset_pin__uint8_t"></a> <a id="structbk__display__qspi__ctlr__config__t_1abc0c0f9645add058c5ca12ac59f76ecf"></a> uint8\_t reset\_pin
    :   qspi reset io pin

    <a id="_CPPv4N29bk_display_qspi_ctlr_config_t6te_pinE"></a>

    <a id="_CPPv3N29bk_display_qspi_ctlr_config_t6te_pinE"></a> <a id="_CPPv2N29bk_display_qspi_ctlr_config_t6te_pinE"></a> <a id="bk_display_qspi_ctlr_config_t::te_pin__uint8_t"></a> <a id="structbk__display__qspi__ctlr__config__t_1a6de12fc07a11d26526f4aaae5cc61835"></a> uint8\_t te\_pin
    :   qspi te io pin

<a id="_CPPv428bk_display_spi_ctlr_config_t"></a>

<a id="_CPPv328bk_display_spi_ctlr_config_t"></a> <a id="_CPPv228bk_display_spi_ctlr_config_t"></a> <a id="bk_display_spi_ctlr_config_t"></a> <a id="structbk__display__spi__ctlr__config__t"></a> struct bk\_display\_spi\_ctlr\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N28bk_display_spi_ctlr_config_t10lcd_deviceE"></a>

    <a id="_CPPv3N28bk_display_spi_ctlr_config_t10lcd_deviceE"></a> <a id="_CPPv2N28bk_display_spi_ctlr_config_t10lcd_deviceE"></a> <a id="bk_display_spi_ctlr_config_t::lcd_device__lcd_device_tCP"></a> <a id="structbk__display__spi__ctlr__config__t_1ae7d6580f78524d850e4aeb5a3b749eda"></a> const [lcd\_device\_t](#_CPPv412lcd_device_t "lcd_device_t") \*lcd\_device
    :   LCD device configuration structure pointer, containing display parameters and initialization commands

    <a id="_CPPv4N28bk_display_spi_ctlr_config_t6spi_idE"></a>

    <a id="_CPPv3N28bk_display_spi_ctlr_config_t6spi_idE"></a> <a id="_CPPv2N28bk_display_spi_ctlr_config_t6spi_idE"></a> <a id="bk_display_spi_ctlr_config_t::spi_id__uint8_t"></a> <a id="structbk__display__spi__ctlr__config__t_1af1ff86f43d86ddb8b778ec5b8108f7ea"></a> uint8\_t spi\_id
    :   spi\_id

    <a id="_CPPv4N28bk_display_spi_ctlr_config_t6dc_pinE"></a>

    <a id="_CPPv3N28bk_display_spi_ctlr_config_t6dc_pinE"></a> <a id="_CPPv2N28bk_display_spi_ctlr_config_t6dc_pinE"></a> <a id="bk_display_spi_ctlr_config_t::dc_pin__uint8_t"></a> <a id="structbk__display__spi__ctlr__config__t_1a2c51202072c4823430f74d347a12cbce"></a> uint8\_t dc\_pin
    :   spi dc io pin

    <a id="_CPPv4N28bk_display_spi_ctlr_config_t9reset_pinE"></a>

    <a id="_CPPv3N28bk_display_spi_ctlr_config_t9reset_pinE"></a> <a id="_CPPv2N28bk_display_spi_ctlr_config_t9reset_pinE"></a> <a id="bk_display_spi_ctlr_config_t::reset_pin__uint8_t"></a> <a id="structbk__display__spi__ctlr__config__t_1a65f7c11fc2854c8d3aabff554370ef03"></a> uint8\_t reset\_pin
    :   spi reset io pin

    <a id="_CPPv4N28bk_display_spi_ctlr_config_t6te_pinE"></a>

    <a id="_CPPv3N28bk_display_spi_ctlr_config_t6te_pinE"></a> <a id="_CPPv2N28bk_display_spi_ctlr_config_t6te_pinE"></a> <a id="bk_display_spi_ctlr_config_t::te_pin__uint8_t"></a> <a id="structbk__display__spi__ctlr__config__t_1a15f6295cff1fc5e795a8ac20b8043b3a"></a> uint8\_t te\_pin
    :   spi te io pin

<a id="_CPPv434bk_display_dual_qspi_ctlr_config_t"></a>

<a id="_CPPv334bk_display_dual_qspi_ctlr_config_t"></a> <a id="_CPPv234bk_display_dual_qspi_ctlr_config_t"></a> <a id="bk_display_dual_qspi_ctlr_config_t"></a> <a id="structbk__display__dual__qspi__ctlr__config__t"></a> struct bk\_display\_dual\_qspi\_ctlr\_config\_t

<a id="_CPPv433bk_display_dual_spi_ctlr_config_t"></a>

<a id="_CPPv333bk_display_dual_spi_ctlr_config_t"></a> <a id="_CPPv233bk_display_dual_spi_ctlr_config_t"></a> <a id="bk_display_dual_spi_ctlr_config_t"></a> <a id="structbk__display__dual__spi__ctlr__config__t"></a> struct bk\_display\_dual\_spi\_ctlr\_config\_t

<a id="_CPPv415bk_display_ctlr"></a>

<a id="_CPPv315bk_display_ctlr"></a> <a id="_CPPv215bk_display_ctlr"></a> <a id="bk_display_ctlr"></a> <a id="structbk__display__ctlr"></a> struct bk\_display\_ctlr

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv424bk_display_ctlr_handle_t"></a>

<a id="_CPPv324bk_display_ctlr_handle_t"></a> <a id="_CPPv224bk_display_ctlr_handle_t"></a> <a id="bk_display_ctlr_handle_t"></a> <a id="bk__display__types_8h_1a5ca217fdd4ebb825b229b61ab0af030c"></a> typedef struct [bk\_display\_ctlr](#_CPPv415bk_display_ctlr "bk_display_ctlr") \*bk\_display\_ctlr\_handle\_t
:   Display controller interface structure.

    Defines the interface functions that the display controller must implement, including open, close, flush, delete and IO control

<a id="_CPPv417bk_display_ctlr_t"></a>

<a id="_CPPv317bk_display_ctlr_t"></a> <a id="_CPPv217bk_display_ctlr_t"></a> <a id="bk_display_ctlr_t"></a> <a id="bk__display__types_8h_1a7d66b177abd1f4645e34388693928766"></a> typedef struct [bk\_display\_ctlr](#_CPPv415bk_display_ctlr "bk_display_ctlr") bk\_display\_ctlr\_t

<a id="id7"></a>

### Header File

- [lcd\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/lcd_types.h)

<a id="id8"></a>

### Functions

<a id="_CPPv423lcd_i80_bus_io_registerPv"></a>

<a id="_CPPv323lcd_i80_bus_io_registerPv"></a> <a id="_CPPv223lcd_i80_bus_io_registerPv"></a> <a id="lcd_i80_bus_io_register__voidP"></a> <a id="lcd__types_8h_1a709487706d90d7964fe1d8ee933a4c20"></a> [bk\_lcd\_i80\_handle\_t](#_CPPv419bk_lcd_i80_handle_t "bk_lcd_i80_handle_t") \*lcd\_i80\_bus\_io\_register(void \*io)

<a id="id9"></a>

### Structures

<a id="_CPPv49lcd_rgb_t"></a>

<a id="_CPPv39lcd_rgb_t"></a> <a id="_CPPv29lcd_rgb_t"></a> <a id="lcd_rgb_t"></a> <a id="structlcd__rgb__t"></a> struct lcd\_rgb\_t
:   rgb interface config param

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N9lcd_rgb_t3clkE"></a>

    <a id="_CPPv3N9lcd_rgb_t3clkE"></a> <a id="_CPPv2N9lcd_rgb_t3clkE"></a> <a id="lcd_rgb_t::clk__lcd_clk_t"></a> <a id="structlcd__rgb__t_1af836dffc8079a7f484f9bbb9e72379e7"></a> [lcd\_clk\_t](#_CPPv49lcd_clk_t "lcd_clk_t") clk
    :   config lcd clk

    <a id="_CPPv4N9lcd_rgb_t17data_out_clk_edgeE"></a>

    <a id="_CPPv3N9lcd_rgb_t17data_out_clk_edgeE"></a> <a id="_CPPv2N9lcd_rgb_t17data_out_clk_edgeE"></a> <a id="lcd_rgb_t::data_out_clk_edge__rgb_out_clk_edge_t"></a> <a id="structlcd__rgb__t_1a6376610d3bf354f4e9e7dd5e886cda4a"></a> [rgb\_out\_clk\_edge\_t](#_CPPv418rgb_out_clk_edge_t "rgb_out_clk_edge_t") data\_out\_clk\_edge
    :   rgb data output in clk edge, should refer lcd device spec

    <a id="_CPPv4N9lcd_rgb_t16hsync_back_porchE"></a>

    <a id="_CPPv3N9lcd_rgb_t16hsync_back_porchE"></a> <a id="_CPPv2N9lcd_rgb_t16hsync_back_porchE"></a> <a id="lcd_rgb_t::hsync_back_porch__uint16_t"></a> <a id="structlcd__rgb__t_1ac9d4a37676b80c717efcf95769f73202"></a> uint16\_t hsync\_back\_porch
    :   rang 0\~0x3FF (0\~1023), should refer lcd device spec

    <a id="_CPPv4N9lcd_rgb_t17hsync_front_porchE"></a>

    <a id="_CPPv3N9lcd_rgb_t17hsync_front_porchE"></a> <a id="_CPPv2N9lcd_rgb_t17hsync_front_porchE"></a> <a id="lcd_rgb_t::hsync_front_porch__uint16_t"></a> <a id="structlcd__rgb__t_1a4f124c59d970ca95b1c200188b95c57d"></a> uint16\_t hsync\_front\_porch
    :   rang 0\~0x3FF (0\~1023), should refer lcd device spec

    <a id="_CPPv4N9lcd_rgb_t16vsync_back_porchE"></a>

    <a id="_CPPv3N9lcd_rgb_t16vsync_back_porchE"></a> <a id="_CPPv2N9lcd_rgb_t16vsync_back_porchE"></a> <a id="lcd_rgb_t::vsync_back_porch__uint16_t"></a> <a id="structlcd__rgb__t_1a9c54c00c91d44285c214ed62918bc6fe"></a> uint16\_t vsync\_back\_porch
    :   rang 0\~0xFF (0\~255), should refer lcd device spec

    <a id="_CPPv4N9lcd_rgb_t17vsync_front_porchE"></a>

    <a id="_CPPv3N9lcd_rgb_t17vsync_front_porchE"></a> <a id="_CPPv2N9lcd_rgb_t17vsync_front_porchE"></a> <a id="lcd_rgb_t::vsync_front_porch__uint16_t"></a> <a id="structlcd__rgb__t_1abaded1c38f9c42ba6d9f337f20b84164"></a> uint16\_t vsync\_front\_porch
    :   rang 0\~0xFF (0\~255), should refer lcd device spec

    <a id="_CPPv4N9lcd_rgb_t17hsync_pulse_widthE"></a>

    <a id="_CPPv3N9lcd_rgb_t17hsync_pulse_widthE"></a> <a id="_CPPv2N9lcd_rgb_t17hsync_pulse_widthE"></a> <a id="lcd_rgb_t::hsync_pulse_width__uint8_t"></a> <a id="structlcd__rgb__t_1a6daa82777c10336129700f5b1f5571bd"></a> uint8\_t hsync\_pulse\_width
    :   rang 0\~0x3F (0\~7), should refer lcd device spec

    <a id="_CPPv4N9lcd_rgb_t17vsync_pulse_widthE"></a>

    <a id="_CPPv3N9lcd_rgb_t17vsync_pulse_widthE"></a> <a id="_CPPv2N9lcd_rgb_t17vsync_pulse_widthE"></a> <a id="lcd_rgb_t::vsync_pulse_width__uint8_t"></a> <a id="structlcd__rgb__t_1ab6b4ac49b710ca21d139760dcfd02b10"></a> uint8\_t vsync\_pulse\_width
    :   rang 0\~0x3F (0\~7), should refer lcd device spec

<a id="_CPPv49lcd_mcu_t"></a>

<a id="_CPPv39lcd_mcu_t"></a> <a id="_CPPv29lcd_mcu_t"></a> <a id="lcd_mcu_t"></a> <a id="structlcd__mcu__t"></a> struct lcd\_mcu\_t
:   mcu interface config param

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N9lcd_mcu_t3clkE"></a>

    <a id="_CPPv3N9lcd_mcu_t3clkE"></a> <a id="_CPPv2N9lcd_mcu_t3clkE"></a> <a id="lcd_mcu_t::clk__lcd_clk_t"></a> <a id="structlcd__mcu__t_1a160d778e6342e8fad3f54ef82ef7b68e"></a> [lcd\_clk\_t](#_CPPv49lcd_clk_t "lcd_clk_t") clk
    :   config lcd clk

<a id="_CPPv410lcd_qspi_t"></a>

<a id="_CPPv310lcd_qspi_t"></a> <a id="_CPPv210lcd_qspi_t"></a> <a id="lcd_qspi_t"></a> <a id="structlcd__qspi__t"></a> struct lcd\_qspi\_t
:   qspi interface config param

<a id="_CPPv49lcd_spi_t"></a>

<a id="_CPPv39lcd_spi_t"></a> <a id="_CPPv29lcd_spi_t"></a> <a id="lcd_spi_t"></a> <a id="structlcd__spi__t"></a> struct lcd\_spi\_t
:   spi interface config param

<a id="_CPPv412lcd_device_t"></a>

<a id="_CPPv312lcd_device_t"></a> <a id="_CPPv212lcd_device_t"></a> <a id="lcd_device_t"></a> <a id="structlcd__device__t"></a> struct lcd\_device\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12lcd_device_t2idE"></a>

    <a id="_CPPv3N12lcd_device_t2idE"></a> <a id="_CPPv2N12lcd_device_t2idE"></a> <a id="lcd_device_t::id__i"></a> <a id="structlcd__device__t_1aaf2cada3fe7617a421006e8f5e0626c4"></a> int id
    :   lcd device type, user can add if you want to add another lcd device

    <a id="_CPPv4N12lcd_device_t4nameE"></a>

    <a id="_CPPv3N12lcd_device_t4nameE"></a> <a id="_CPPv2N12lcd_device_t4nameE"></a> <a id="lcd_device_t::name__cP"></a> <a id="structlcd__device__t_1a0716f79f1dd6160e43b60071c2fb0fed"></a> char \*name
    :   lcd device name

    <a id="_CPPv4N12lcd_device_t4typeE"></a>

    <a id="_CPPv3N12lcd_device_t4typeE"></a> <a id="_CPPv2N12lcd_device_t4typeE"></a> <a id="lcd_device_t::type__uint8_t"></a> <a id="structlcd__device__t_1a0b97d8b71f48a46dcb35a831b85dd967"></a> uint8\_t type
    :   lcd device hw interface

    <a id="_CPPv4N12lcd_device_t5widthE"></a>

    <a id="_CPPv3N12lcd_device_t5widthE"></a> <a id="_CPPv2N12lcd_device_t5widthE"></a> <a id="lcd_device_t::width__uint16_t"></a> <a id="structlcd__device__t_1a26e072fc3cb47641233f8ce48b256dbb"></a> uint16\_t width
    :   lcd device width

    <a id="_CPPv4N12lcd_device_t6heightE"></a>

    <a id="_CPPv3N12lcd_device_t6heightE"></a> <a id="_CPPv2N12lcd_device_t6heightE"></a> <a id="lcd_device_t::height__uint16_t"></a> <a id="structlcd__device__t_1ad7796f477cda3337d01ef59aa7e0a237"></a> uint16\_t height
    :   lcd device height

    <a id="_CPPv4N12lcd_device_t7src_fmtE"></a>

    <a id="_CPPv3N12lcd_device_t7src_fmtE"></a> <a id="_CPPv2N12lcd_device_t7src_fmtE"></a> <a id="lcd_device_t::src_fmt__uint8_t"></a> <a id="structlcd__device__t_1a6840462df57bdf8242449de39b15b32c"></a> uint8\_t src\_fmt
    :   source data format: input to display module data format(rgb565/rgb888/yuv)

    <a id="_CPPv4N12lcd_device_t7out_fmtE"></a>

    <a id="_CPPv3N12lcd_device_t7out_fmtE"></a> <a id="_CPPv2N12lcd_device_t7out_fmtE"></a> <a id="lcd_device_t::out_fmt__uint8_t"></a> <a id="structlcd__device__t_1a024df12ee857ad9147c9854c2898e39f"></a> uint8\_t out\_fmt
    :   display module output data format(rgb565/rgb666/rgb888), input to lcd device, Color\_depth, 24bit/pixel:RGB888,18bit/pixel:RGB666,16bit/pixel:RGB565

    <a id="_CPPv4N12lcd_device_t3rgbE"></a>

    <a id="_CPPv3N12lcd_device_t3rgbE"></a> <a id="_CPPv2N12lcd_device_t3rgbE"></a> <a id="lcd_device_t::rgb__lcd_rgb_tCP"></a> <a id="structlcd__device__t_1a54bf0e055bf00eb1e66436d4bd09a6a1"></a> const [lcd\_rgb\_t](#_CPPv49lcd_rgb_t "lcd_rgb_t") \*rgb
    :   RGB interface lcd device config

    <a id="_CPPv4N12lcd_device_t3mcuE"></a>

    <a id="_CPPv3N12lcd_device_t3mcuE"></a> <a id="_CPPv2N12lcd_device_t3mcuE"></a> <a id="lcd_device_t::mcu__lcd_mcu_tCP"></a> <a id="structlcd__device__t_1abad62e6438452bdf022ae391a7a8ec22"></a> const [lcd\_mcu\_t](#_CPPv49lcd_mcu_t "lcd_mcu_t") \*mcu
    :   MCU interface lcd device config

    <a id="_CPPv4N12lcd_device_t4qspiE"></a>

    <a id="_CPPv3N12lcd_device_t4qspiE"></a> <a id="_CPPv2N12lcd_device_t4qspiE"></a> <a id="lcd_device_t::qspi__lcd_qspi_tCP"></a> <a id="structlcd__device__t_1a61ca212f4bbe75f92b7483fd682b06e7"></a> const [lcd\_qspi\_t](#_CPPv410lcd_qspi_t "lcd_qspi_t") \*qspi
    :   QSPI interface lcd device config

    <a id="_CPPv4N12lcd_device_t3spiE"></a>

    <a id="_CPPv3N12lcd_device_t3spiE"></a> <a id="_CPPv2N12lcd_device_t3spiE"></a> <a id="lcd_device_t::spi__lcd_spi_tCP"></a> <a id="structlcd__device__t_1ae9980b548cd1be02299aba94e57f9dc4"></a> const [lcd\_spi\_t](#_CPPv49lcd_spi_t "lcd_spi_t") \*spi
    :   SPI interface lcd device config

    <a id="_CPPv4N12lcd_device_t4initE"></a>

    <a id="_CPPv3N12lcd_device_t4initE"></a> <a id="_CPPv2N12lcd_device_t4initE"></a> <a id="structlcd__device__t_1a214e6443e8290fff225b1308b27ae764"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*init)(const void \*handle)
    :   lcd device initial function by handle

    <a id="_CPPv4N12lcd_device_t3offE"></a>

    <a id="_CPPv3N12lcd_device_t3offE"></a> <a id="_CPPv2N12lcd_device_t3offE"></a> <a id="structlcd__device__t_1aed011456a757741db1fc99fa2e9552fa"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*off)(const void \*handle)
    :   lcd off by handle

<a id="_CPPv418lcd_display_area_t"></a>

<a id="_CPPv318lcd_display_area_t"></a> <a id="_CPPv218lcd_display_area_t"></a> <a id="lcd_display_area_t"></a> <a id="structlcd__display__area__t"></a> struct lcd\_display\_area\_t

<a id="_CPPv417bk_lcd_i80_handle"></a>

<a id="_CPPv317bk_lcd_i80_handle"></a> <a id="_CPPv217bk_lcd_i80_handle"></a> <a id="bk_lcd_i80_handle"></a> <a id="structbk__lcd__i80__handle"></a> struct bk\_lcd\_i80\_handle

<a id="macros"></a>

### Macros

<a id="c.USE_LCD_REGISTER_CALLBACKS"></a>

<a id="lcd__types_8h_1a17da68dea3768aa8086fafa2133695cc"></a> USE\_LCD\_REGISTER\_CALLBACKS

<a id="id10"></a>

### Type Definitions

<a id="_CPPv49lcd_isr_t"></a>

<a id="_CPPv39lcd_isr_t"></a> <a id="_CPPv29lcd_isr_t"></a> <a id="lcd_isr_t"></a> <a id="lcd__types_8h_1a0ec134e818738e4ff50d85a6ae626bb6"></a> typedef void (\*lcd\_isr\_t)(void \*args)

<a id="_CPPv419bk_lcd_i80_handle_t"></a>

<a id="_CPPv319bk_lcd_i80_handle_t"></a> <a id="_CPPv219bk_lcd_i80_handle_t"></a> <a id="bk_lcd_i80_handle_t"></a> <a id="lcd__types_8h_1a01b1f9a514e7efdf5b9ee19e5459bffd"></a> typedef struct [bk\_lcd\_i80\_handle](#_CPPv417bk_lcd_i80_handle "bk_lcd_i80_handle") bk\_lcd\_i80\_handle\_t

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv415lcd_device_id_t"></a>

<a id="_CPPv315lcd_device_id_t"></a> <a id="_CPPv215lcd_device_id_t"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ce"></a> enum lcd\_device\_id\_t
:   *Values:*

    <a id="_CPPv4N15lcd_device_id_t17LCD_DEVICE_UNKNOWE"></a>

    <a id="_CPPv3N15lcd_device_id_t17LCD_DEVICE_UNKNOWE"></a> <a id="_CPPv2N15lcd_device_id_t17LCD_DEVICE_UNKNOWE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceac8710938e1091c0a603fac3ce915356e"></a> enumerator LCD\_DEVICE\_UNKNOW

    <a id="_CPPv4N15lcd_device_id_t17LCD_DEVICE_ST7282E"></a>

    <a id="_CPPv3N15lcd_device_id_t17LCD_DEVICE_ST7282E"></a> <a id="_CPPv2N15lcd_device_id_t17LCD_DEVICE_ST7282E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea7574ff30a446118a9f0456850b05abc6"></a> enumerator LCD\_DEVICE\_ST7282
    :   480X270 RGB

    <a id="_CPPv4N15lcd_device_id_t17LCD_DEVICE_HX8282E"></a>

    <a id="_CPPv3N15lcd_device_id_t17LCD_DEVICE_HX8282E"></a> <a id="_CPPv2N15lcd_device_id_t17LCD_DEVICE_HX8282E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceaf3a82abe4fe462cb469e330e45f05f7c"></a> enumerator LCD\_DEVICE\_HX8282
    :   1024X600 RGB

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_GC9503VE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_GC9503VE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_GC9503VE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea553dfd0dd3d872a813e791b92027a384"></a> enumerator LCD\_DEVICE\_GC9503V
    :   480X800 RGB

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_NT35510E"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_NT35510E"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_NT35510E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea2c361b1aecc3b18d32c64f068009e76d"></a> enumerator LCD\_DEVICE\_NT35510
    :   480X854 RGB

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_H050IWVE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_H050IWVE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_H050IWVE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceaeac8b66a1b1a716cfc7f0e43fa8d20e0"></a> enumerator LCD\_DEVICE\_H050IWV
    :   800X480 RGB

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_MD0430RE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_MD0430RE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_MD0430RE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea21467a5195bfa0ce300d5688e7f6b63c"></a> enumerator LCD\_DEVICE\_MD0430R
    :   800X480 RGB

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_MD0700RE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_MD0700RE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_MD0700RE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cead8bcbfdc1a08f0805a9b8b3728fe5b0b"></a> enumerator LCD\_DEVICE\_MD0700R
    :   1024X600 RGB

    <a id="_CPPv4N15lcd_device_id_t21LCD_DEVICE_ST7701S_LYE"></a>

    <a id="_CPPv3N15lcd_device_id_t21LCD_DEVICE_ST7701S_LYE"></a> <a id="_CPPv2N15lcd_device_id_t21LCD_DEVICE_ST7701S_LYE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea34780a69556d7ef3ae9267f77d250519"></a> enumerator LCD\_DEVICE\_ST7701S\_LY
    :   480X480 RGB

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_ST7701SE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_ST7701SE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_ST7701SE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceaa67ac66b9b32fcea2e6c4fa6f8c62a16"></a> enumerator LCD\_DEVICE\_ST7701S
    :   480X480 RGB

    <a id="_CPPv4N15lcd_device_id_t19LCD_DEVICE_ST7701SNE"></a>

    <a id="_CPPv3N15lcd_device_id_t19LCD_DEVICE_ST7701SNE"></a> <a id="_CPPv2N15lcd_device_id_t19LCD_DEVICE_ST7701SNE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea771ffd47c9f261bc8a03b4d2abb0dd13"></a> enumerator LCD\_DEVICE\_ST7701SN
    :   480X480 RGB

    <a id="_CPPv4N15lcd_device_id_t16LCD_DEVICE_AML01E"></a>

    <a id="_CPPv3N15lcd_device_id_t16LCD_DEVICE_AML01E"></a> <a id="_CPPv2N15lcd_device_id_t16LCD_DEVICE_AML01E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceae92d9e37f83a4aa9c3130bf7c9141321"></a> enumerator LCD\_DEVICE\_AML01
    :   720X1280 RGB

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_ST7796SE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_ST7796SE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_ST7796SE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea598c1bb50724f94841de83d16266b01b"></a> enumerator LCD\_DEVICE\_ST7796S
    :   320X480 MCU

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_NT35512E"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_NT35512E"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_NT35512E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea0865e8af0f57b7bcac7f4df3d6162d5f"></a> enumerator LCD\_DEVICE\_NT35512
    :   480X800 MCU

    <a id="_CPPv4N15lcd_device_id_t22LCD_DEVICE_NT35510_MCUE"></a>

    <a id="_CPPv3N15lcd_device_id_t22LCD_DEVICE_NT35510_MCUE"></a> <a id="_CPPv2N15lcd_device_id_t22LCD_DEVICE_NT35510_MCUE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea197885af012f5ab8e811428af702d908"></a> enumerator LCD\_DEVICE\_NT35510\_MCU
    :   480X800 MCU

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_ST7789VE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_ST7789VE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_ST7789VE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cead7f77e867120d3888b0530b2c0899d0d"></a> enumerator LCD\_DEVICE\_ST7789V
    :   170X320 MCU

    <a id="_CPPv4N15lcd_device_id_t19LCD_DEVICE_ST7789T3E"></a>

    <a id="_CPPv3N15lcd_device_id_t19LCD_DEVICE_ST7789T3E"></a> <a id="_CPPv2N15lcd_device_id_t19LCD_DEVICE_ST7789T3E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea136b6994bb5c82aeb341190172b08968"></a> enumerator LCD\_DEVICE\_ST7789T3
    :   240X320 MCU

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_SH8601AE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_SH8601AE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_SH8601AE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceafa5ce1e69e16a9912941b462adfd5644"></a> enumerator LCD\_DEVICE\_SH8601A
    :   454X454 QSPI

    <a id="_CPPv4N15lcd_device_id_t26LCD_DEVICE_ST77903_WX20114E"></a>

    <a id="_CPPv3N15lcd_device_id_t26LCD_DEVICE_ST77903_WX20114E"></a> <a id="_CPPv2N15lcd_device_id_t26LCD_DEVICE_ST77903_WX20114E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea0bfe7b9a9e92bb3763b616975883ca1e"></a> enumerator LCD\_DEVICE\_ST77903\_WX20114
    :   400X400 QSPI

    <a id="_CPPv4N15lcd_device_id_t28LCD_DEVICE_ST77903_SAT61478ME"></a>

    <a id="_CPPv3N15lcd_device_id_t28LCD_DEVICE_ST77903_SAT61478ME"></a> <a id="_CPPv2N15lcd_device_id_t28LCD_DEVICE_ST77903_SAT61478ME"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea526d4f70fb8ba8f35684558aa6289e88"></a> enumerator LCD\_DEVICE\_ST77903\_SAT61478M
    :   400X400 QSPI

    <a id="_CPPv4N15lcd_device_id_t29LCD_DEVICE_ST77903_H0165Y008TE"></a>

    <a id="_CPPv3N15lcd_device_id_t29LCD_DEVICE_ST77903_H0165Y008TE"></a> <a id="_CPPv2N15lcd_device_id_t29LCD_DEVICE_ST77903_H0165Y008TE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceac3314ab051c3b9da7f8e9a0e258b8ed0"></a> enumerator LCD\_DEVICE\_ST77903\_H0165Y008T
    :   360X480 QSPI

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_SPD2010E"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_SPD2010E"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_SPD2010E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea04ef1efb95afbb38b5e3a9c4f4f825ec"></a> enumerator LCD\_DEVICE\_SPD2010
    :   412X412 QSPI

    <a id="_CPPv4N15lcd_device_id_t17LCD_DEVICE_GC9C01E"></a>

    <a id="_CPPv3N15lcd_device_id_t17LCD_DEVICE_GC9C01E"></a> <a id="_CPPv2N15lcd_device_id_t17LCD_DEVICE_GC9C01E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceae949573444e9b5b74ca2bd633aae07ad"></a> enumerator LCD\_DEVICE\_GC9C01
    :   360X360 QSPI

    <a id="_CPPv4N15lcd_device_id_t17LCD_DEVICE_JD9855E"></a>

    <a id="_CPPv3N15lcd_device_id_t17LCD_DEVICE_JD9855E"></a> <a id="_CPPv2N15lcd_device_id_t17LCD_DEVICE_JD9855E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea2dbe562fe8dc82a08f355aa169d75d46"></a> enumerator LCD\_DEVICE\_JD9855
    :   360X360 QSPI

    <a id="_CPPv4N15lcd_device_id_t25LCD_DEVICE_JD9855_K18XJ15E"></a>

    <a id="_CPPv3N15lcd_device_id_t25LCD_DEVICE_JD9855_K18XJ15E"></a> <a id="_CPPv2N15lcd_device_id_t25LCD_DEVICE_JD9855_K18XJ15E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea71b16ace2de5be807e0e2334642583f7"></a> enumerator LCD\_DEVICE\_JD9855\_K18XJ15
    :   360X360 QSPI

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_ST77916E"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_ST77916E"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_ST77916E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3cea4fa2ae30876848ed0b97e6b7cfc084c2"></a> enumerator LCD\_DEVICE\_ST77916
    :   360X360 QSPI

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_JD9853AE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_JD9853AE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_JD9853AE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceaa05ea1f0937c5c7b72f7339af8858707"></a> enumerator LCD\_DEVICE\_JD9853A
    :   240X320 QSPI

    <a id="_CPPv4N15lcd_device_id_t18LCD_DEVICE_ST7796UE"></a>

    <a id="_CPPv3N15lcd_device_id_t18LCD_DEVICE_ST7796UE"></a> <a id="_CPPv2N15lcd_device_id_t18LCD_DEVICE_ST7796UE"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceaac7c5c4aad7d61f023cd6c3fb2a490e4"></a> enumerator LCD\_DEVICE\_ST7796U
    :   320X480 SPI

    <a id="_CPPv4N15lcd_device_id_t17LCD_DEVICE_GC9D01E"></a>

    <a id="_CPPv3N15lcd_device_id_t17LCD_DEVICE_GC9D01E"></a> <a id="_CPPv2N15lcd_device_id_t17LCD_DEVICE_GC9D01E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceafdc4e632d121ef77d158e1627853c737"></a> enumerator LCD\_DEVICE\_GC9D01
    :   160X160 SPI

    <a id="_CPPv4N15lcd_device_id_t19LCD_DEVICE_ST7789V2E"></a>

    <a id="_CPPv3N15lcd_device_id_t19LCD_DEVICE_ST7789V2E"></a> <a id="_CPPv2N15lcd_device_id_t19LCD_DEVICE_ST7789V2E"></a> <a id="lcd__types_8h_1a37e8eb517a35d12737857d17c5c3f3ceaba431e9af802fd6048387fef8786a9f0"></a> enumerator LCD\_DEVICE\_ST7789V2
    :   240X320 SPI

<a id="_CPPv410lcd_type_t"></a>

<a id="_CPPv310lcd_type_t"></a> <a id="_CPPv210lcd_type_t"></a> <a id="lcd__types_8h_1af4b71961185e1fa00ee5962123a349ae"></a> enum lcd\_type\_t
:   *Values:*

    <a id="_CPPv4N10lcd_type_t12LCD_TYPE_RGBE"></a>

    <a id="_CPPv3N10lcd_type_t12LCD_TYPE_RGBE"></a> <a id="_CPPv2N10lcd_type_t12LCD_TYPE_RGBE"></a> <a id="lcd__types_8h_1af4b71961185e1fa00ee5962123a349aea659c7a589916a748ffcf4ed245476425"></a> enumerator LCD\_TYPE\_RGB
    :   lcd hardware interface is parallel RGB interface

    <a id="_CPPv4N10lcd_type_t15LCD_TYPE_RGB565E"></a>

    <a id="_CPPv3N10lcd_type_t15LCD_TYPE_RGB565E"></a> <a id="_CPPv2N10lcd_type_t15LCD_TYPE_RGB565E"></a> <a id="lcd__types_8h_1af4b71961185e1fa00ee5962123a349aea58f49d69ae81d4124f7ce76cae70557f"></a> enumerator LCD\_TYPE\_RGB565
    :   lcd device output data hardware interface is RGB565 format

    <a id="_CPPv4N10lcd_type_t16LCD_TYPE_MCU8080E"></a>

    <a id="_CPPv3N10lcd_type_t16LCD_TYPE_MCU8080E"></a> <a id="_CPPv2N10lcd_type_t16LCD_TYPE_MCU8080E"></a> <a id="lcd__types_8h_1af4b71961185e1fa00ee5962123a349aea402c4ac8e222467f5e1b0fd05231d165"></a> enumerator LCD\_TYPE\_MCU8080
    :   lcd device output data hardware interface is MCU 8BIT format

    <a id="_CPPv4N10lcd_type_t13LCD_TYPE_QSPIE"></a>

    <a id="_CPPv3N10lcd_type_t13LCD_TYPE_QSPIE"></a> <a id="_CPPv2N10lcd_type_t13LCD_TYPE_QSPIE"></a> <a id="lcd__types_8h_1af4b71961185e1fa00ee5962123a349aeaf618168b284c75855cc6cf7e8a631247"></a> enumerator LCD\_TYPE\_QSPI
    :   lcd device hardware interface is QSPI interface

    <a id="_CPPv4N10lcd_type_t12LCD_TYPE_SPIE"></a>

    <a id="_CPPv3N10lcd_type_t12LCD_TYPE_SPIE"></a> <a id="_CPPv2N10lcd_type_t12LCD_TYPE_SPIE"></a> <a id="lcd__types_8h_1af4b71961185e1fa00ee5962123a349aea127ede10049ef527c1429050eba13f09"></a> enumerator LCD\_TYPE\_SPI
    :   lcd device hardware interface is SPI interface

<a id="_CPPv414lcd_int_type_t"></a>

<a id="_CPPv314lcd_int_type_t"></a> <a id="_CPPv214lcd_int_type_t"></a> <a id="lcd__types_8h_1a28f44ddb3274b941067b3e958614328b"></a> enum lcd\_int\_type\_t
:   *Values:*

    <a id="_CPPv4N14lcd_int_type_t14RGB_OUTPUT_EOFE"></a>

    <a id="_CPPv3N14lcd_int_type_t14RGB_OUTPUT_EOFE"></a> <a id="_CPPv2N14lcd_int_type_t14RGB_OUTPUT_EOFE"></a> <a id="lcd__types_8h_1a28f44ddb3274b941067b3e958614328ba115f811dd33a03546139c3f478f79fe9"></a> enumerator RGB\_OUTPUT\_EOF
    :   reg end of frame int status

    <a id="_CPPv4N14lcd_int_type_t14RGB_OUTPUT_SOFE"></a>

    <a id="_CPPv3N14lcd_int_type_t14RGB_OUTPUT_SOFE"></a> <a id="_CPPv2N14lcd_int_type_t14RGB_OUTPUT_SOFE"></a> <a id="lcd__types_8h_1a28f44ddb3274b941067b3e958614328bac24da633a70504b462ee0137cc60b3c7"></a> enumerator RGB\_OUTPUT\_SOF
    :   reg display output start of frame status

    <a id="_CPPv4N14lcd_int_type_t16I8080_OUTPUT_SOFE"></a>

    <a id="_CPPv3N14lcd_int_type_t16I8080_OUTPUT_SOFE"></a> <a id="_CPPv2N14lcd_int_type_t16I8080_OUTPUT_SOFE"></a> <a id="lcd__types_8h_1a28f44ddb3274b941067b3e958614328bafa88660b5cef16a11250153649d7b927"></a> enumerator I8080\_OUTPUT\_SOF
    :   8080 display output start of frame status

    <a id="_CPPv4N14lcd_int_type_t16I8080_OUTPUT_EOFE"></a>

    <a id="_CPPv3N14lcd_int_type_t16I8080_OUTPUT_EOFE"></a> <a id="_CPPv2N14lcd_int_type_t16I8080_OUTPUT_EOFE"></a> <a id="lcd__types_8h_1a28f44ddb3274b941067b3e958614328ba5a580bf2cfac1f0ca1f7aaa844f651c8"></a> enumerator I8080\_OUTPUT\_EOF
    :   8080 display output end of frame status

    <a id="_CPPv4N14lcd_int_type_t6DE_INTE"></a>

    <a id="_CPPv3N14lcd_int_type_t6DE_INTE"></a> <a id="_CPPv2N14lcd_int_type_t6DE_INTE"></a> <a id="lcd__types_8h_1a28f44ddb3274b941067b3e958614328ba924fe07dd502fe3cedbc05a08d9e3b96"></a> enumerator DE\_INT

    <a id="_CPPv4N14lcd_int_type_t18FRAME_INTERVAL_INTE"></a>

    <a id="_CPPv3N14lcd_int_type_t18FRAME_INTERVAL_INTE"></a> <a id="_CPPv2N14lcd_int_type_t18FRAME_INTERVAL_INTE"></a> <a id="lcd__types_8h_1a28f44ddb3274b941067b3e958614328ba42df9fd700394cd75f0793c144082af1"></a> enumerator FRAME\_INTERVAL\_INT

<a id="_CPPv418frame_delay_unit_t"></a>

<a id="_CPPv318frame_delay_unit_t"></a> <a id="_CPPv218frame_delay_unit_t"></a> <a id="lcd__types_8h_1aa171577dddd7f62b713731c6c9e29541"></a> enum frame\_delay\_unit\_t
:   *Values:*

    <a id="_CPPv4N18frame_delay_unit_t9DCLK_UNITE"></a>

    <a id="_CPPv3N18frame_delay_unit_t9DCLK_UNITE"></a> <a id="_CPPv2N18frame_delay_unit_t9DCLK_UNITE"></a> <a id="lcd__types_8h_1aa171577dddd7f62b713731c6c9e29541ac228e2b3cbcf9f9b887c5f1c03fe491a"></a> enumerator DCLK\_UNIT

    <a id="_CPPv4N18frame_delay_unit_t10HSYNC_UNITE"></a>

    <a id="_CPPv3N18frame_delay_unit_t10HSYNC_UNITE"></a> <a id="_CPPv2N18frame_delay_unit_t10HSYNC_UNITE"></a> <a id="lcd__types_8h_1aa171577dddd7f62b713731c6c9e29541a54273794e21b28566b85066353ad94c8"></a> enumerator HSYNC\_UNIT

    <a id="_CPPv4N18frame_delay_unit_t10VSYNC_UNITE"></a>

    <a id="_CPPv3N18frame_delay_unit_t10VSYNC_UNITE"></a> <a id="_CPPv2N18frame_delay_unit_t10VSYNC_UNITE"></a> <a id="lcd__types_8h_1aa171577dddd7f62b713731c6c9e29541a9a4fbc4f833fc81c6b3dda8fbd3845e6"></a> enumerator VSYNC\_UNIT

    <a id="_CPPv4N18frame_delay_unit_t4NONEE"></a>

    <a id="_CPPv3N18frame_delay_unit_t4NONEE"></a> <a id="_CPPv2N18frame_delay_unit_t4NONEE"></a> <a id="lcd__types_8h_1aa171577dddd7f62b713731c6c9e29541ac157bdf0b85a40d2619cbc8bc1ae5fe2"></a> enumerator NONE

<a id="_CPPv49lcd_clk_t"></a>

<a id="_CPPv39lcd_clk_t"></a> <a id="_CPPv29lcd_clk_t"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94c"></a> enum lcd\_clk\_t
:   rgb lcd clk select, infulence pfs, user should select according to lcd device spec

    *Values:*

    <a id="_CPPv4N9lcd_clk_t7LCD_80ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_80ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_80ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94cab97fb30150141ea72edb5f9215cc7861"></a> enumerator LCD\_80M

    <a id="_CPPv4N9lcd_clk_t7LCD_60ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_60ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_60ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94cab1aee5d1dbb15720fc5ccf14120b87ff"></a> enumerator LCD\_60M

    <a id="_CPPv4N9lcd_clk_t7LCD_54ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_54ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_54ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94cae3d96ee8a2728755ccf7f16ff78aa863"></a> enumerator LCD\_54M

    <a id="_CPPv4N9lcd_clk_t7LCD_40ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_40ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_40ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94cafa7a466e8f78d5a69fa3e1a601387b03"></a> enumerator LCD\_40M

    <a id="_CPPv4N9lcd_clk_t7LCD_32ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_32ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_32ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94ca7eb44b642493f447e151e6626e862b1e"></a> enumerator LCD\_32M

    <a id="_CPPv4N9lcd_clk_t7LCD_30ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_30ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_30ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94ca63321aa0b04d8e106b6410008283138c"></a> enumerator LCD\_30M

    <a id="_CPPv4N9lcd_clk_t7LCD_26ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_26ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_26ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94cabe590184b02fe4e435e26d15fb1d513e"></a> enumerator LCD\_26M

    <a id="_CPPv4N9lcd_clk_t7LCD_22ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_22ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_22ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94cac802d0da88ee4907021eae9f40da9938"></a> enumerator LCD\_22M

    <a id="_CPPv4N9lcd_clk_t7LCD_20ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_20ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_20ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94ca1d773daa19c63d9fab3cdf9a51592ac4"></a> enumerator LCD\_20M

    <a id="_CPPv4N9lcd_clk_t7LCD_17ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_17ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_17ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94caa52dbce4cfd12b9d6add5311ad38058b"></a> enumerator LCD\_17M

    <a id="_CPPv4N9lcd_clk_t7LCD_15ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_15ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_15ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94ca68679ed24b5eaf49401f2ee5ae6c9148"></a> enumerator LCD\_15M

    <a id="_CPPv4N9lcd_clk_t7LCD_12ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_12ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_12ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94ca0e52477003dc52e87641450bfe80c4ab"></a> enumerator LCD\_12M

    <a id="_CPPv4N9lcd_clk_t7LCD_10ME"></a>

    <a id="_CPPv3N9lcd_clk_t7LCD_10ME"></a> <a id="_CPPv2N9lcd_clk_t7LCD_10ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94cafb13e6644df84ded5e6a84a52261a8a6"></a> enumerator LCD\_10M

    <a id="_CPPv4N9lcd_clk_t6LCD_9ME"></a>

    <a id="_CPPv3N9lcd_clk_t6LCD_9ME"></a> <a id="_CPPv2N9lcd_clk_t6LCD_9ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94cac1ecfba5a09b23cec472172abafc41b1"></a> enumerator LCD\_9M

    <a id="_CPPv4N9lcd_clk_t6LCD_8ME"></a>

    <a id="_CPPv3N9lcd_clk_t6LCD_8ME"></a> <a id="_CPPv2N9lcd_clk_t6LCD_8ME"></a> <a id="lcd__types_8h_1a2a759d8f610763ee03ee3bee67b3e94ca2165418b3d183b1e333224e72599f321"></a> enumerator LCD\_8M

<a id="_CPPv414lcd_qspi_clk_t"></a>

<a id="_CPPv314lcd_qspi_clk_t"></a> <a id="_CPPv214lcd_qspi_clk_t"></a> <a id="lcd__types_8h_1a771a804dae215a78f525dedc780e5ba9"></a> enum lcd\_qspi\_clk\_t
:   *Values:*

    <a id="_CPPv4N14lcd_qspi_clk_t12LCD_QSPI_80ME"></a>

    <a id="_CPPv3N14lcd_qspi_clk_t12LCD_QSPI_80ME"></a> <a id="_CPPv2N14lcd_qspi_clk_t12LCD_QSPI_80ME"></a> <a id="lcd__types_8h_1a771a804dae215a78f525dedc780e5ba9a7171fe84c1d1ba3b17d168601b102e17"></a> enumerator LCD\_QSPI\_80M

    <a id="_CPPv4N14lcd_qspi_clk_t12LCD_QSPI_64ME"></a>

    <a id="_CPPv3N14lcd_qspi_clk_t12LCD_QSPI_64ME"></a> <a id="_CPPv2N14lcd_qspi_clk_t12LCD_QSPI_64ME"></a> <a id="lcd__types_8h_1a771a804dae215a78f525dedc780e5ba9a6fc5b285649ce48d3d7670b813e7bbbf"></a> enumerator LCD\_QSPI\_64M

    <a id="_CPPv4N14lcd_qspi_clk_t12LCD_QSPI_60ME"></a>

    <a id="_CPPv3N14lcd_qspi_clk_t12LCD_QSPI_60ME"></a> <a id="_CPPv2N14lcd_qspi_clk_t12LCD_QSPI_60ME"></a> <a id="lcd__types_8h_1a771a804dae215a78f525dedc780e5ba9a223c0ade308316e45e99bc673a72ef77"></a> enumerator LCD\_QSPI\_60M

    <a id="_CPPv4N14lcd_qspi_clk_t12LCD_QSPI_53ME"></a>

    <a id="_CPPv3N14lcd_qspi_clk_t12LCD_QSPI_53ME"></a> <a id="_CPPv2N14lcd_qspi_clk_t12LCD_QSPI_53ME"></a> <a id="lcd__types_8h_1a771a804dae215a78f525dedc780e5ba9af7eac094cd3b2854f60c1fbe3fd55c78"></a> enumerator LCD\_QSPI\_53M

    <a id="_CPPv4N14lcd_qspi_clk_t12LCD_QSPI_48ME"></a>

    <a id="_CPPv3N14lcd_qspi_clk_t12LCD_QSPI_48ME"></a> <a id="_CPPv2N14lcd_qspi_clk_t12LCD_QSPI_48ME"></a> <a id="lcd__types_8h_1a771a804dae215a78f525dedc780e5ba9aa83051548449c3a875a315595086364f"></a> enumerator LCD\_QSPI\_48M

    <a id="_CPPv4N14lcd_qspi_clk_t12LCD_QSPI_40ME"></a>

    <a id="_CPPv3N14lcd_qspi_clk_t12LCD_QSPI_40ME"></a> <a id="_CPPv2N14lcd_qspi_clk_t12LCD_QSPI_40ME"></a> <a id="lcd__types_8h_1a771a804dae215a78f525dedc780e5ba9a751e939647a9e0f6115f0e99811387e1"></a> enumerator LCD\_QSPI\_40M

    <a id="_CPPv4N14lcd_qspi_clk_t12LCD_QSPI_32ME"></a>

    <a id="_CPPv3N14lcd_qspi_clk_t12LCD_QSPI_32ME"></a> <a id="_CPPv2N14lcd_qspi_clk_t12LCD_QSPI_32ME"></a> <a id="lcd__types_8h_1a771a804dae215a78f525dedc780e5ba9a1e746f2f289e20af77f0036fbea50a39"></a> enumerator LCD\_QSPI\_32M

    <a id="_CPPv4N14lcd_qspi_clk_t12LCD_QSPI_30ME"></a>

    <a id="_CPPv3N14lcd_qspi_clk_t12LCD_QSPI_30ME"></a> <a id="_CPPv2N14lcd_qspi_clk_t12LCD_QSPI_30ME"></a> <a id="lcd__types_8h_1a771a804dae215a78f525dedc780e5ba9a2259644616f95000b38737fcb31c6b76"></a> enumerator LCD\_QSPI\_30M

<a id="_CPPv418rgb_out_clk_edge_t"></a>

<a id="_CPPv318rgb_out_clk_edge_t"></a> <a id="_CPPv218rgb_out_clk_edge_t"></a> <a id="lcd__types_8h_1aa5f0b3766c01d0133b2cb106c31f5177"></a> enum rgb\_out\_clk\_edge\_t
:   rgb data output in clk rising or falling

    *Values:*

    <a id="_CPPv4N18rgb_out_clk_edge_t14POSEDGE_OUTPUTE"></a>

    <a id="_CPPv3N18rgb_out_clk_edge_t14POSEDGE_OUTPUTE"></a> <a id="_CPPv2N18rgb_out_clk_edge_t14POSEDGE_OUTPUTE"></a> <a id="lcd__types_8h_1aa5f0b3766c01d0133b2cb106c31f5177a005de0101234af3f0d8c3dafb47e773a"></a> enumerator POSEDGE\_OUTPUT
    :   output in clk falling

    <a id="_CPPv4N18rgb_out_clk_edge_t14NEGEDGE_OUTPUTE"></a>

    <a id="_CPPv3N18rgb_out_clk_edge_t14NEGEDGE_OUTPUTE"></a> <a id="_CPPv2N18rgb_out_clk_edge_t14NEGEDGE_OUTPUTE"></a> <a id="lcd__types_8h_1aa5f0b3766c01d0133b2cb106c31f5177ac1a22fd926be61d730c8d8531a32a328"></a> enumerator NEGEDGE\_OUTPUT
    :   output in clk rising

<a id="_CPPv413data_format_t"></a>

<a id="_CPPv313data_format_t"></a> <a id="_CPPv213data_format_t"></a> <a id="lcd__types_8h_1a5bf8652e0ba6d33572895efc752f5b8c"></a> enum data\_format\_t
:   *Values:*

    <a id="_CPPv4N13data_format_t8ARGB8888E"></a>

    <a id="_CPPv3N13data_format_t8ARGB8888E"></a> <a id="_CPPv2N13data_format_t8ARGB8888E"></a> <a id="lcd__types_8h_1a5bf8652e0ba6d33572895efc752f5b8caf540c373a71dee269827b0d12026de80"></a> enumerator ARGB8888
    :   ARGB8888 DMA2D color mode

    <a id="_CPPv4N13data_format_t6RGB888E"></a>

    <a id="_CPPv3N13data_format_t6RGB888E"></a> <a id="_CPPv2N13data_format_t6RGB888E"></a> <a id="lcd__types_8h_1a5bf8652e0ba6d33572895efc752f5b8cacbcf87c79628b8c7fed02f39f7cbd15f"></a> enumerator RGB888
    :   RGB888 DMA2D color mode

    <a id="_CPPv4N13data_format_t6RGB565E"></a>

    <a id="_CPPv3N13data_format_t6RGB565E"></a> <a id="_CPPv2N13data_format_t6RGB565E"></a> <a id="lcd__types_8h_1a5bf8652e0ba6d33572895efc752f5b8ca183737a1f19f772782bc5e24cfd662e7"></a> enumerator RGB565
    :   RGB565 DMA2D color mode

    <a id="_CPPv4N13data_format_t4YUYVE"></a>

    <a id="_CPPv3N13data_format_t4YUYVE"></a> <a id="_CPPv2N13data_format_t4YUYVE"></a> <a id="lcd__types_8h_1a5bf8652e0ba6d33572895efc752f5b8ca0105757557d0eed9bac6f9f1c0185a0b"></a> enumerator YUYV
