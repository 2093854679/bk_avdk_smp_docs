---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_can.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="can"></a>

# CAN

<a id="can-api-status"></a>

## CAN API Status

| API | BK7258\_ap |
| --- | --- |
| [`bk_can_init()`](#_CPPv411bk_can_initP9can_dev_t "bk_can_init") | Y |
| [`bk_can_driver_init()`](#_CPPv418bk_can_driver_initv "bk_can_driver_init") | Y |
| [`bk_can_driver_deinit()`](#_CPPv420bk_can_driver_deinitv "bk_can_driver_deinit") | Y |
| [`bk_can_deinit()`](#_CPPv413bk_can_deinitv "bk_can_deinit") | Y |
| [`bk_can_send()`](#_CPPv411bk_can_sendP11can_frame_s8uint32_t "bk_can_send") | Y |
| [`bk_can_acc_filter_set()`](#_CPPv421bk_can_acc_filter_setP20can_acc_filter_cmd_s "bk_can_acc_filter_set") | Y |
| [`bk_can_register_isr_callback()`](#_CPPv428bk_can_register_isr_callbackP18can_callback_des_tP18can_callback_des_t "bk_can_register_isr_callback") | Y |
| [`bk_can_register_err_callback()`](#_CPPv428bk_can_register_err_callbackP18can_callback_des_t "bk_can_register_err_callback") | Y |
| [`can_driver_bit_rate_config()`](#_CPPv426can_driver_bit_rate_config14can_bit_rate_e14can_bit_rate_e "can_driver_bit_rate_config") | Y |

<a id="can-api-reference"></a>

## CAN API Reference

<a id="header-file"></a>

### Header File

- [can.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/can.h)

<a id="functions"></a>

### Functions

<a id="_CPPv411bk_can_initP9can_dev_t"></a>

<a id="_CPPv311bk_can_initP9can_dev_t"></a> <a id="_CPPv211bk_can_initP9can_dev_t"></a> <a id="bk_can_init__can_dev_tP"></a> <a id="can_8h_1a8cf22444f3c361fb83762755988f1c1f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_can\_init([can\_dev\_t](#_CPPv49can_dev_t "can_dev_t") \*can)
:   The CAN config.

    参数
    :   **can** – **\[in\]** structure of parameters

    返回
    :   bk\_err\_t error code

<a id="_CPPv418bk_can_driver_initv"></a>

<a id="_CPPv318bk_can_driver_initv"></a> <a id="_CPPv218bk_can_driver_initv"></a> <a id="bk_can_driver_init__void"></a> <a id="can_8h_1a8612c76a49397aad1bd93c8449befd05"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_can\_driver\_init(void)
:   CAN software module init.

    返回
    :   bk\_err\_t error code

<a id="_CPPv420bk_can_driver_deinitv"></a>

<a id="_CPPv320bk_can_driver_deinitv"></a> <a id="_CPPv220bk_can_driver_deinitv"></a> <a id="bk_can_driver_deinit__void"></a> <a id="can_8h_1a2c8426ba704394eaf25101b8f9394a2a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_can\_driver\_deinit(void)
:   CAN software module deinit.

    返回
    :   bk\_err\_t error code

<a id="_CPPv413bk_can_deinitv"></a>

<a id="_CPPv313bk_can_deinitv"></a> <a id="_CPPv213bk_can_deinitv"></a> <a id="bk_can_deinit__void"></a> <a id="can_8h_1a3ccd11af54601fe1655012b8e9a366d0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_can\_deinit(void)
:   free the CAN config

    返回
    :   bk\_err\_t error code

<a id="_CPPv414bk_can_receiveP7uint8_t8uint32_tP8uint32_t8uint32_t"></a>

<a id="_CPPv314bk_can_receiveP7uint8_t8uint32_tP8uint32_t8uint32_t"></a> <a id="_CPPv214bk_can_receiveP7uint8_t8uint32_tP8uint32_t8uint32_t"></a> <a id="bk_can_receive__uint8_tP.uint32_t.uint32_tP.uint32_t"></a> <a id="can_8h_1a4bb931b09908db921434ad8aeb5fdfb6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_can\_receive(uint8\_t \*data, uint32\_t expect\_size, uint32\_t \*recv\_size, uint32\_t timeout)
:   CAN receive frames.

    备注

    Pop out the data from software fifo

    参数
    :   - **data** – **\[in\]** buffer to store data in
        - **expect\_size** – **\[in\]** size of data expect to get
        - **recv\_size** – **\[in\]** size of data actually get
        - **timeout** – **\[in\]** max wait time to achieve the expect size

    返回
    :   bk\_err\_t error code

<a id="_CPPv415bk_can_send_ptbP11can_frame_s"></a>

<a id="_CPPv315bk_can_send_ptbP11can_frame_s"></a> <a id="_CPPv215bk_can_send_ptbP11can_frame_s"></a> <a id="bk_can_send_ptb__can_frame_sP"></a> <a id="can_8h_1a101a41517bc7f5520f3375e9c0d08794"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_can\_send\_ptb([can\_frame\_s](#_CPPv411can_frame_s "can_frame_s") \*frame)
:   CAN send frame through primary transmit buffer.

    备注

    Put in fifo one message that would be transmitted at the next possible positon

    参数
    :   **frame** – **\[in\]** One frame for transmission

    返回
    :   bk\_err\_t error code

<a id="_CPPv411bk_can_sendP11can_frame_s8uint32_t"></a>

<a id="_CPPv311bk_can_sendP11can_frame_s8uint32_t"></a> <a id="_CPPv211bk_can_sendP11can_frame_s8uint32_t"></a> <a id="bk_can_send__can_frame_sP.uint32_t"></a> <a id="can_8h_1a89145492b038d6d30a2c9c2fa5e81cc8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_can\_send([can\_frame\_s](#_CPPv411can_frame_s "can_frame_s") \*frame, uint32\_t timeout)
:   CAN send frame through secondary transmit buffer.

    备注

    Put in fifo frames that would be sent out together Data in fifo would be conbined to reach the longest legal length Data share the same arbitration parameter

    参数
    :   - **frame** – **\[in\]** One frame for transmission
        - **timeout** – **\[in\]** max wait time to send out all data

    返回
    :   bk\_err\_t error code

<a id="_CPPv421bk_can_acc_filter_setP20can_acc_filter_cmd_s"></a>

<a id="_CPPv321bk_can_acc_filter_setP20can_acc_filter_cmd_s"></a> <a id="_CPPv221bk_can_acc_filter_setP20can_acc_filter_cmd_s"></a> <a id="bk_can_acc_filter_set__can_acc_filter_cmd_sP"></a> <a id="can_8h_1ac3bb07653f5355a5894f18de2687ea20"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_can\_acc\_filter\_set([can\_acc\_filter\_cmd\_s](#_CPPv420can_acc_filter_cmd_s "can_acc_filter_cmd_s") \*cmd)
:   CAN acceptance filter set.

    备注

    Only filter 0 accpet all messages by default Disabled bits result in accepting the message

    参数
    :   **cmd** – **\[in\]** structure of parameter

    返回
    :   bk\_err\_t error code

<a id="_CPPv428bk_can_register_isr_callbackP18can_callback_des_tP18can_callback_des_t"></a>

<a id="_CPPv328bk_can_register_isr_callbackP18can_callback_des_tP18can_callback_des_t"></a> <a id="_CPPv228bk_can_register_isr_callbackP18can_callback_des_tP18can_callback_des_t"></a> <a id="bk_can_register_isr_callback__can_callback_des_tP.can_callback_des_tP"></a> <a id="can_8h_1a8b55d1ceacc7e1ada0f7b21aa31df6c3"></a> void bk\_can\_register\_isr\_callback([can\_callback\_des\_t](#_CPPv418can_callback_des_t "can_callback_des_t") \*rx\_cb, [can\_callback\_des\_t](#_CPPv418can_callback_des_t "can_callback_des_t") \*tx\_cb)
:   CAN register callback.

    备注

    Register to send and receive completed interrupt callback funcitons. The callback funciton is called in the interrupt. Pay attention to the operation.

    参数
    :   - **rx\_cb** – **\[in\]** Receive callback functions and parameters
        - **tx\_cb** – **\[in\]** Send callback functions and parameters

<a id="_CPPv428bk_can_register_err_callbackP18can_callback_des_t"></a>

<a id="_CPPv328bk_can_register_err_callbackP18can_callback_des_t"></a> <a id="_CPPv228bk_can_register_err_callbackP18can_callback_des_t"></a> <a id="bk_can_register_err_callback__can_callback_des_tP"></a> <a id="can_8h_1aa79d3c7972d89c3a3b7a721bcc3daecb"></a> void bk\_can\_register\_err\_callback([can\_callback\_des\_t](#_CPPv418can_callback_des_t "can_callback_des_t") \*err\_cb)
:   CAN register callback.

    备注

    Register to Error interrupt callback funcitons. The callback funciton is called in the interrupt. Pay attention to the operation.

    参数
    :   **err\_cb** – **\[in\]** Error callback functions and parameters

<a id="_CPPv426can_driver_bit_rate_config14can_bit_rate_e14can_bit_rate_e"></a>

<a id="_CPPv326can_driver_bit_rate_config14can_bit_rate_e14can_bit_rate_e"></a> <a id="_CPPv226can_driver_bit_rate_config14can_bit_rate_e14can_bit_rate_e"></a> <a id="can_driver_bit_rate_config__can_bit_rate_e.can_bit_rate_e"></a> <a id="can_8h_1a6b76aae67de220b27624982396aabd66"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") can\_driver\_bit\_rate\_config([can\_bit\_rate\_e](#_CPPv414can_bit_rate_e "can_bit_rate_e") s\_speed, [can\_bit\_rate\_e](#_CPPv414can_bit_rate_e "can_bit_rate_e") f\_speed)
:   Adjusting the Baud Rate.

    备注

    Berfore sending data, the baud rate can be adjusted Pay attention to the protocol used to prevent speed mismatch.

    参数
    :   - **s\_speed** – **\[in\]** CAN2.0 Baud rate
        - **f\_speed** – **\[in\]** CAN FD Baud rate

<a id="can-api-typedefs"></a>

## CAN API Typedefs

<a id="id1"></a>

### Header File

- [can\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/can_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv414can_gpio_map_t"></a>

<a id="_CPPv314can_gpio_map_t"></a> <a id="_CPPv214can_gpio_map_t"></a> <a id="can_gpio_map_t"></a> <a id="structcan__gpio__map__t"></a> struct can\_gpio\_map\_t

<a id="_CPPv410can_gpio_t"></a>

<a id="_CPPv310can_gpio_t"></a> <a id="_CPPv210can_gpio_t"></a> <a id="can_gpio_t"></a> <a id="structcan__gpio__t"></a> struct can\_gpio\_t

<a id="_CPPv410can_fifo_t"></a>

<a id="_CPPv310can_fifo_t"></a> <a id="_CPPv210can_fifo_t"></a> <a id="can_fifo_t"></a> <a id="structcan__fifo__t"></a> struct can\_fifo\_t

<a id="_CPPv49can_env_t"></a>

<a id="_CPPv39can_env_t"></a> <a id="_CPPv29can_env_t"></a> <a id="can_env_t"></a> <a id="structcan__env__t"></a> struct can\_env\_t

<a id="_CPPv412can_config_t"></a>

<a id="_CPPv312can_config_t"></a> <a id="_CPPv212can_config_t"></a> <a id="can_config_t"></a> <a id="structcan__config__t"></a> struct can\_config\_t

<a id="_CPPv49can_dev_t"></a>

<a id="_CPPv39can_dev_t"></a> <a id="_CPPv29can_dev_t"></a> <a id="can_dev_t"></a> <a id="structcan__dev__t"></a> struct can\_dev\_t

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_CAN_NOT_INIT"></a>

<a id="can__types_8h_1a87d089f33b86b614a918bc0b3a78cd37"></a> BK\_ERR\_CAN\_NOT\_INIT
:   CAN driver not init

<a id="c.BK_ERR_CAN_INT_TYPE"></a>

<a id="can__types_8h_1ae0ecb2c748079da7a1d0353a57c91f38"></a> BK\_ERR\_CAN\_INT\_TYPE
:   CAN interrupte type error

<a id="c.BK_ERR_CAN_BIT_ERROR"></a>

<a id="can__types_8h_1a68902dafdce3e2a5a9fea10293a2a1e1"></a> BK\_ERR\_CAN\_BIT\_ERROR
:   CAN bit error

<a id="c.BK_ERR_CAN_CHK_ERROR"></a>

<a id="can__types_8h_1a7e776b136be7e848fdc806e0972d46e9"></a> BK\_ERR\_CAN\_CHK\_ERROR
:   CAN checksum error

<a id="c.BK_ERR_CAN_TIMEOUT_ERROR"></a>

<a id="can__types_8h_1a8ecf17cf39c0438cf58a718689a72423"></a> BK\_ERR\_CAN\_TIMEOUT\_ERROR
:   CAN timeout error

<a id="c.BK_ERR_CAN_PARITY_ERROR"></a>

<a id="can__types_8h_1a4d3a463fabbc8b6e579545a78b8f4a29"></a> BK\_ERR\_CAN\_PARITY\_ERROR
:   CAN identifier parity error

<a id="c.BK_ERR_CAN_HAL_INVALID_ADDR"></a>

<a id="can__types_8h_1ae16d52443453f80b513f0b48fdf5525a"></a> BK\_ERR\_CAN\_HAL\_INVALID\_ADDR
:   CAN invalid addr

<a id="c.BK_ERR_CAN_HAL_INVALID_ARG"></a>

<a id="can__types_8h_1a2f110f8dd6db829c96ea4c258e1a06da"></a> BK\_ERR\_CAN\_HAL\_INVALID\_ARG
:   CAN invalid arg

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv412can_status_e"></a>

<a id="_CPPv312can_status_e"></a> <a id="_CPPv212can_status_e"></a> <a id="can__types_8h_1abd01fd14919f17553ccc3305d5303c0f"></a> enum can\_status\_e
:   *Values:*

    <a id="_CPPv4N12can_status_e17CAN_STATUS_CLOSEDE"></a>

    <a id="_CPPv3N12can_status_e17CAN_STATUS_CLOSEDE"></a> <a id="_CPPv2N12can_status_e17CAN_STATUS_CLOSEDE"></a> <a id="can__types_8h_1abd01fd14919f17553ccc3305d5303c0faa48115f40b72c0038679e9952c2685fd"></a> enumerator CAN\_STATUS\_CLOSED

    <a id="_CPPv4N12can_status_e15CAN_STATUS_IDLEE"></a>

    <a id="_CPPv3N12can_status_e15CAN_STATUS_IDLEE"></a> <a id="_CPPv2N12can_status_e15CAN_STATUS_IDLEE"></a> <a id="can__types_8h_1abd01fd14919f17553ccc3305d5303c0fa23d0cecee5dc8177e87db72046b3fd0f"></a> enumerator CAN\_STATUS\_IDLE

    <a id="_CPPv4N12can_status_e17CAN_STATUS_OPENEDE"></a>

    <a id="_CPPv3N12can_status_e17CAN_STATUS_OPENEDE"></a> <a id="_CPPv2N12can_status_e17CAN_STATUS_OPENEDE"></a> <a id="can__types_8h_1abd01fd14919f17553ccc3305d5303c0fa926a6c155f0e8169f50c1361299be7f5"></a> enumerator CAN\_STATUS\_OPENED

<a id="id2"></a>

### Header File

- [hal\_can\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_can_types.h)

<a id="id3"></a>

### Structures

<a id="_CPPv417can_core_br_tab_s"></a>

<a id="_CPPv317can_core_br_tab_s"></a> <a id="_CPPv217can_core_br_tab_s"></a> <a id="can_core_br_tab_s"></a> <a id="structcan__core__br__tab__s"></a> struct can\_core\_br\_tab\_s

<a id="_CPPv411can_speed_t"></a>

<a id="_CPPv311can_speed_t"></a> <a id="_CPPv211can_speed_t"></a> <a id="can_speed_t"></a> <a id="structcan__speed__t"></a> struct can\_speed\_t

<a id="_CPPv420can_acc_filter_cmd_s"></a>

<a id="_CPPv320can_acc_filter_cmd_s"></a> <a id="_CPPv220can_acc_filter_cmd_s"></a> <a id="can_acc_filter_cmd_s"></a> <a id="structcan__acc__filter__cmd__s"></a> struct can\_acc\_filter\_cmd\_s

<a id="_CPPv415can_frame_tag_t"></a>

<a id="_CPPv315can_frame_tag_t"></a> <a id="_CPPv215can_frame_tag_t"></a> <a id="can_frame_tag_t"></a> <a id="structcan__frame__tag__t"></a> struct can\_frame\_tag\_t

<a id="_CPPv411can_frame_s"></a>

<a id="_CPPv311can_frame_s"></a> <a id="_CPPv211can_frame_s"></a> <a id="can_frame_s"></a> <a id="structcan__frame__s"></a> struct can\_frame\_s

<a id="_CPPv418can_callback_des_t"></a>

<a id="_CPPv318can_callback_des_t"></a> <a id="_CPPv218can_callback_des_t"></a> <a id="can_callback_des_t"></a> <a id="structcan__callback__des__t"></a> struct can\_callback\_des\_t

<a id="_CPPv49can_hal_t"></a>

<a id="_CPPv39can_hal_t"></a> <a id="_CPPv29can_hal_t"></a> <a id="can_hal_t"></a> <a id="structcan__hal__t"></a> struct can\_hal\_t

<a id="id4"></a>

### Macros

<a id="c.RX_INT_FLAG_GROUP"></a>

<a id="hal__can__types_8h_1a02767cf817d8de7fb7dbd788fca80818"></a> RX\_INT\_FLAG\_GROUP

<a id="c.TX_INT_FLAG_GROUP"></a>

<a id="hal__can__types_8h_1a8ac80d1aba78f02c00d9251889a7f7eb"></a> TX\_INT\_FLAG\_GROUP

<a id="c.ERR_INT_FLAG_GROUP"></a>

<a id="hal__can__types_8h_1a4c2abc8aebec1822b85a8bb1496c218b"></a> ERR\_INT\_FLAG\_GROUP

<a id="c.TT_INT_FLAG_GROUP"></a>

<a id="hal__can__types_8h_1abda23045d2996cea8632551738919fbe"></a> TT\_INT\_FLAG\_GROUP

<a id="c.MEM_INT_FLAG_GROUP"></a>

<a id="hal__can__types_8h_1a6aa41a6183772736ed6a92af8a9918e5"></a> MEM\_INT\_FLAG\_GROUP

<a id="c.SAFE_INT_FLAG_GROUP"></a>

<a id="hal__can__types_8h_1ae2225f702372515e4a0feab9c465a542"></a> SAFE\_INT\_FLAG\_GROUP

<a id="c.OTHER_INT_FLAG_GROUP"></a>

<a id="hal__can__types_8h_1a380f98e13f7538132ab74c84c7f69e70"></a> OTHER\_INT\_FLAG\_GROUP

<a id="c.CC_RAM_MEMTYPE"></a>

<a id="hal__can__types_8h_1ab0201c423f142c461db188fcb2d7a5f5"></a> CC\_RAM\_MEMTYPE

<a id="c.CC_RAM_TYPE"></a>

<a id="hal__can__types_8h_1ad6f1b7c32451673db7e8e8fabd210fdf"></a> CC\_RAM\_TYPE

<a id="c.CC_RAM_ECC"></a>

<a id="hal__can__types_8h_1ad824e33b7135a8f41c4058ccb3c02881"></a> CC\_RAM\_ECC

<a id="c.CC_RAM_ES"></a>

<a id="hal__can__types_8h_1a5874941f183bcd4059438ff514b22376"></a> CC\_RAM\_ES

<a id="c.CC_RBUF_SLOTS"></a>

<a id="hal__can__types_8h_1afd3a6a89914486c51848cfe65cea1277"></a> CC\_RBUF\_SLOTS

<a id="c.CC_STB_ENABLE"></a>

<a id="hal__can__types_8h_1a72bafd125d62d862ff680616f15dcb60"></a> CC\_STB\_ENABLE

<a id="c.CC_STB_SLOTS"></a>

<a id="hal__can__types_8h_1a8e3fa0faf91d0a4e348711f6fd211aeb"></a> CC\_STB\_SLOTS

<a id="c.CC_STB_PRIO"></a>

<a id="hal__can__types_8h_1a92141a08f34ef0214b53ffe5d6734009"></a> CC\_STB\_PRIO

<a id="c.CC_ACF_NUMBER"></a>

<a id="hal__can__types_8h_1aea91b25271037f92a5c7c0b3122bb7b4"></a> CC\_ACF\_NUMBER

<a id="c.CC_CAN_FD"></a>

<a id="hal__can__types_8h_1a823992860c63f4b3851e2a7c1e9d2272"></a> CC\_CAN\_FD

<a id="c.CC_UPWARD_COMPATIBILITY"></a>

<a id="hal__can__types_8h_1abfc5f77c6d3906fc7d18370c41b664f7"></a> CC\_UPWARD\_COMPATIBILITY

<a id="c.CC_TTCAN"></a>

<a id="hal__can__types_8h_1a1fd53feeb4bba9e0041d4974049a314e"></a> CC\_TTCAN

<a id="c.CC_CIA603"></a>

<a id="hal__can__types_8h_1a28f1313c53fb324e7d8f08ba6aa1b497"></a> CC\_CIA603

<a id="c.CC_SAFETY_ENABLE"></a>

<a id="hal__can__types_8h_1a774d5fc2a05ac7e24599df6140ff4a1e"></a> CC\_SAFETY\_ENABLE

<a id="c.CAN_20_MAX_PAYLOAD"></a>

<a id="hal__can__types_8h_1abe42583a1dbf2c40d5358cf165e6f292"></a> CAN\_20\_MAX\_PAYLOAD

<a id="c.CAN_FD_MAX_PAYLOAD"></a>

<a id="hal__can__types_8h_1aef0e3e4e871f505042abc8e63ecf3bbf"></a> CAN\_FD\_MAX\_PAYLOAD

<a id="c.MAX_ACF_NUM"></a>

<a id="hal__can__types_8h_1abecd14a5e6eccfd9aa3f0d10038a083a"></a> MAX\_ACF\_NUM

<a id="c.FDF_CAN_20"></a>

<a id="hal__can__types_8h_1a5bf4918b83d3760721a7da73e22e164a"></a> FDF\_CAN\_20

<a id="c.FDF_CAN_FD"></a>

<a id="hal__can__types_8h_1a638a50dca4b8f5b6238b6718a6314e77"></a> FDF\_CAN\_FD

<a id="c.CAN_STAND_ID_MASK"></a>

<a id="hal__can__types_8h_1a6a57a07b513e2aa2f075128a8c384d42"></a> CAN\_STAND\_ID\_MASK

<a id="c.CAN_EXT_ID_MASK"></a>

<a id="hal__can__types_8h_1a15ee71e8abcf51008925585049125986"></a> CAN\_EXT\_ID\_MASK

<a id="c.POS_TTSEN"></a>

<a id="hal__can__types_8h_1a5055aa8a04a24a1fccc682c189838e76"></a> POS\_TTSEN

<a id="c.TTSEN_MASK"></a>

<a id="hal__can__types_8h_1adc48fae5df65060995a792b0eda09c12"></a> TTSEN\_MASK

<a id="c.RSTAT_EMPTY"></a>

<a id="hal__can__types_8h_1a5ed71749320ea71791f795d98866131a"></a> RSTAT\_EMPTY

<a id="c.RSTAT_AFWL"></a>

<a id="hal__can__types_8h_1acfb939e234e5d1ef40559272214b904d"></a> RSTAT\_AFWL

<a id="c.RSTAT_NOFULL"></a>

<a id="hal__can__types_8h_1a49330ef06fcf0276efab99d4243386ae"></a> RSTAT\_NOFULL

<a id="c.RSTAT_FULL"></a>

<a id="hal__can__types_8h_1a327ecbd8c7f1f7d7adce067ed852ceca"></a> RSTAT\_FULL

<a id="c.BUF_REG_NUM"></a>

<a id="hal__can__types_8h_1a0cf8d43a3350b4de787e7c125b672bd4"></a> BUF\_REG\_NUM

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv412can_callback"></a>

<a id="_CPPv312can_callback"></a> <a id="_CPPv212can_callback"></a> <a id="can_callback"></a> <a id="hal__can__types_8h_1aa8ee639835709df5f8b4c09303ea8dda"></a> typedef void (\*can\_callback)(void \*param)

<a id="_CPPv410can_fifo_f"></a>

<a id="_CPPv310can_fifo_f"></a> <a id="_CPPv210can_fifo_f"></a> <a id="can_fifo_f"></a> <a id="hal__can__types_8h_1af510c17c12483c928e984ac82530429d"></a> typedef uint32\_t (\*can\_fifo\_f)(uint8\_t \*buf, uint32\_t len)

<a id="_CPPv410can_size_f"></a>

<a id="_CPPv310can_size_f"></a> <a id="_CPPv210can_size_f"></a> <a id="can_size_f"></a> <a id="hal__can__types_8h_1ae04153ada33882de8f41e55ad949b918"></a> typedef uint32\_t (\*can\_size\_f)(void)

<a id="id5"></a>

### Enumerations

<a id="_CPPv413can_channel_t"></a>

<a id="_CPPv313can_channel_t"></a> <a id="_CPPv213can_channel_t"></a> <a id="hal__can__types_8h_1aa046a5d34dedd1dd0cb61de072f3f36d"></a> enum can\_channel\_t
:   *Values:*

    <a id="_CPPv4N13can_channel_t10CAN_CHAN_0E"></a>

    <a id="_CPPv3N13can_channel_t10CAN_CHAN_0E"></a> <a id="_CPPv2N13can_channel_t10CAN_CHAN_0E"></a> <a id="hal__can__types_8h_1aa046a5d34dedd1dd0cb61de072f3f36daf5f69426bc5f93d145e65b701c59162f"></a> enumerator CAN\_CHAN\_0
    :   can gpio44/gpio45/gpuo46

    <a id="_CPPv4N13can_channel_t12CAN_CHAN_MAXE"></a>

    <a id="_CPPv3N13can_channel_t12CAN_CHAN_MAXE"></a> <a id="_CPPv2N13can_channel_t12CAN_CHAN_MAXE"></a> <a id="hal__can__types_8h_1aa046a5d34dedd1dd0cb61de072f3f36da39a1c99a630a8c1d06af38a135e418ea"></a> enumerator CAN\_CHAN\_MAX

<a id="_CPPv414can_bit_rate_e"></a>

<a id="_CPPv314can_bit_rate_e"></a> <a id="_CPPv214can_bit_rate_e"></a> <a id="hal__can__types_8h_1a433c510fc7c90f693c6e294227fffa7b"></a> enum can\_bit\_rate\_e
:   *Values:*

    <a id="_CPPv4N14can_bit_rate_e11CAN_BR_125KE"></a>

    <a id="_CPPv3N14can_bit_rate_e11CAN_BR_125KE"></a> <a id="_CPPv2N14can_bit_rate_e11CAN_BR_125KE"></a> <a id="hal__can__types_8h_1a433c510fc7c90f693c6e294227fffa7baaf56eab9e9da959e445c6c6e00b5e8c1"></a> enumerator CAN\_BR\_125K

    <a id="_CPPv4N14can_bit_rate_e11CAN_BR_250KE"></a>

    <a id="_CPPv3N14can_bit_rate_e11CAN_BR_250KE"></a> <a id="_CPPv2N14can_bit_rate_e11CAN_BR_250KE"></a> <a id="hal__can__types_8h_1a433c510fc7c90f693c6e294227fffa7ba923a4193520c7d44b5030b411e27605e"></a> enumerator CAN\_BR\_250K

    <a id="_CPPv4N14can_bit_rate_e11CAN_BR_500KE"></a>

    <a id="_CPPv3N14can_bit_rate_e11CAN_BR_500KE"></a> <a id="_CPPv2N14can_bit_rate_e11CAN_BR_500KE"></a> <a id="hal__can__types_8h_1a433c510fc7c90f693c6e294227fffa7ba0f0037758de794fb961574185d22d7db"></a> enumerator CAN\_BR\_500K

    <a id="_CPPv4N14can_bit_rate_e11CAN_BR_800KE"></a>

    <a id="_CPPv3N14can_bit_rate_e11CAN_BR_800KE"></a> <a id="_CPPv2N14can_bit_rate_e11CAN_BR_800KE"></a> <a id="hal__can__types_8h_1a433c510fc7c90f693c6e294227fffa7bae6cfe92aada8ab76339475a6a685af95"></a> enumerator CAN\_BR\_800K

    <a id="_CPPv4N14can_bit_rate_e9CAN_BR_1ME"></a>

    <a id="_CPPv3N14can_bit_rate_e9CAN_BR_1ME"></a> <a id="_CPPv2N14can_bit_rate_e9CAN_BR_1ME"></a> <a id="hal__can__types_8h_1a433c510fc7c90f693c6e294227fffa7babb92cc5f18b241fe1b4ccffc290bc5c9"></a> enumerator CAN\_BR\_1M

    <a id="_CPPv4N14can_bit_rate_e9CAN_BR_2ME"></a>

    <a id="_CPPv3N14can_bit_rate_e9CAN_BR_2ME"></a> <a id="_CPPv2N14can_bit_rate_e9CAN_BR_2ME"></a> <a id="hal__can__types_8h_1a433c510fc7c90f693c6e294227fffa7baffc88a31ad4c44f3d3dd5b489f126f53"></a> enumerator CAN\_BR\_2M

    <a id="_CPPv4N14can_bit_rate_e9CAN_BR_4ME"></a>

    <a id="_CPPv3N14can_bit_rate_e9CAN_BR_4ME"></a> <a id="_CPPv2N14can_bit_rate_e9CAN_BR_4ME"></a> <a id="hal__can__types_8h_1a433c510fc7c90f693c6e294227fffa7bac834f95e93afd412ef85f46745b15701"></a> enumerator CAN\_BR\_4M

    <a id="_CPPv4N14can_bit_rate_e9CAN_BR_5ME"></a>

    <a id="_CPPv3N14can_bit_rate_e9CAN_BR_5ME"></a> <a id="_CPPv2N14can_bit_rate_e9CAN_BR_5ME"></a> <a id="hal__can__types_8h_1a433c510fc7c90f693c6e294227fffa7ba94555a2e0dc0c19f11347eede824805d"></a> enumerator CAN\_BR\_5M

<a id="_CPPv414can_ctrl_cmd_e"></a>

<a id="_CPPv314can_ctrl_cmd_e"></a> <a id="_CPPv214can_ctrl_cmd_e"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799"></a> enum can\_ctrl\_cmd\_e
:   *Values:*

    <a id="_CPPv4N14can_ctrl_cmd_e20CMD_CAN_MODUILE_INITE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e20CMD_CAN_MODUILE_INITE"></a> <a id="_CPPv2N14can_ctrl_cmd_e20CMD_CAN_MODUILE_INITE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799a40c5f124c21da49e710953ffe5d06d02"></a> enumerator CMD\_CAN\_MODUILE\_INIT

    <a id="_CPPv4N14can_ctrl_cmd_e23CMD_CAN_SET_RX_CALLBACKE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e23CMD_CAN_SET_RX_CALLBACKE"></a> <a id="_CPPv2N14can_ctrl_cmd_e23CMD_CAN_SET_RX_CALLBACKE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799ae35ea69fd75b2da95808b0330fe6a77e"></a> enumerator CMD\_CAN\_SET\_RX\_CALLBACK

    <a id="_CPPv4N14can_ctrl_cmd_e23CMD_CAN_SET_TX_CALLBACKE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e23CMD_CAN_SET_TX_CALLBACKE"></a> <a id="_CPPv2N14can_ctrl_cmd_e23CMD_CAN_SET_TX_CALLBACKE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799a9adc2ed503b807f0c48c1d47077e2cf1"></a> enumerator CMD\_CAN\_SET\_TX\_CALLBACK

    <a id="_CPPv4N14can_ctrl_cmd_e17CMD_CAN_RESET_REQE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e17CMD_CAN_RESET_REQE"></a> <a id="_CPPv2N14can_ctrl_cmd_e17CMD_CAN_RESET_REQE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799ab9091cf2c66bee94b14e5d8d604d77b8"></a> enumerator CMD\_CAN\_RESET\_REQ

    <a id="_CPPv4N14can_ctrl_cmd_e22CMD_CAN_ACC_FILTER_SETE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e22CMD_CAN_ACC_FILTER_SETE"></a> <a id="_CPPv2N14can_ctrl_cmd_e22CMD_CAN_ACC_FILTER_SETE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799ab8e2a5bde4eda925ae203002d167959c"></a> enumerator CMD\_CAN\_ACC\_FILTER\_SET

    <a id="_CPPv4N14can_ctrl_cmd_e19CMD_CAN_SET_TX_FIFOE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e19CMD_CAN_SET_TX_FIFOE"></a> <a id="_CPPv2N14can_ctrl_cmd_e19CMD_CAN_SET_TX_FIFOE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799a546c86c34b40d2249267b89bf3abcd2a"></a> enumerator CMD\_CAN\_SET\_TX\_FIFO

    <a id="_CPPv4N14can_ctrl_cmd_e19CMD_CAN_GET_TX_SIZEE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e19CMD_CAN_GET_TX_SIZEE"></a> <a id="_CPPv2N14can_ctrl_cmd_e19CMD_CAN_GET_TX_SIZEE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799ab6324016330d8ba3aee069b40cd238a2"></a> enumerator CMD\_CAN\_GET\_TX\_SIZE

    <a id="_CPPv4N14can_ctrl_cmd_e19CMD_CAN_SET_RX_FIFOE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e19CMD_CAN_SET_RX_FIFOE"></a> <a id="_CPPv2N14can_ctrl_cmd_e19CMD_CAN_SET_RX_FIFOE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799a3c38bac4371d66d56a1ff84cbd307cce"></a> enumerator CMD\_CAN\_SET\_RX\_FIFO

    <a id="_CPPv4N14can_ctrl_cmd_e21CMD_CAN_FD_BOSCH_MODEE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e21CMD_CAN_FD_BOSCH_MODEE"></a> <a id="_CPPv2N14can_ctrl_cmd_e21CMD_CAN_FD_BOSCH_MODEE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799aee16d15e383a8a155ea38d1990b9f47c"></a> enumerator CMD\_CAN\_FD\_BOSCH\_MODE

    <a id="_CPPv4N14can_ctrl_cmd_e24CMD_CAN_GET_RX_FRAME_TAGE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e24CMD_CAN_GET_RX_FRAME_TAGE"></a> <a id="_CPPv2N14can_ctrl_cmd_e24CMD_CAN_GET_RX_FRAME_TAGE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799ad4d8a20ca084d75d91d8373b83a1ea3d"></a> enumerator CMD\_CAN\_GET\_RX\_FRAME\_TAG

    <a id="_CPPv4N14can_ctrl_cmd_e24CMD_CAN_SET_TX_FRAME_TAGE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e24CMD_CAN_SET_TX_FRAME_TAGE"></a> <a id="_CPPv2N14can_ctrl_cmd_e24CMD_CAN_SET_TX_FRAME_TAGE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799a0559e4fda0c6dd67322dcaa25adf9722"></a> enumerator CMD\_CAN\_SET\_TX\_FRAME\_TAG

    <a id="_CPPv4N14can_ctrl_cmd_e17CMD_CAN_PTB_INBUFE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e17CMD_CAN_PTB_INBUFE"></a> <a id="_CPPv2N14can_ctrl_cmd_e17CMD_CAN_PTB_INBUFE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799a88e83eb005b7504bf67455dcac1955d5"></a> enumerator CMD\_CAN\_PTB\_INBUF

    <a id="_CPPv4N14can_ctrl_cmd_e20CMD_CAN_TRANS_SWITCHE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e20CMD_CAN_TRANS_SWITCHE"></a> <a id="_CPPv2N14can_ctrl_cmd_e20CMD_CAN_TRANS_SWITCHE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799ac5abd20df7b0520d405d3f4595f3b02f"></a> enumerator CMD\_CAN\_TRANS\_SWITCH

    <a id="_CPPv4N14can_ctrl_cmd_e17CMD_CAN_STB_INBUFE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e17CMD_CAN_STB_INBUFE"></a> <a id="_CPPv2N14can_ctrl_cmd_e17CMD_CAN_STB_INBUFE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799ae21ee4fc1e424ad2d3adddb363abce74"></a> enumerator CMD\_CAN\_STB\_INBUF

    <a id="_CPPv4N14can_ctrl_cmd_e24CMD_CAN_SET_ERR_CALLBACKE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e24CMD_CAN_SET_ERR_CALLBACKE"></a> <a id="_CPPv2N14can_ctrl_cmd_e24CMD_CAN_SET_ERR_CALLBACKE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799ac878774f9955aad9860508fdc7e7dc75"></a> enumerator CMD\_CAN\_SET\_ERR\_CALLBACK

    <a id="_CPPv4N14can_ctrl_cmd_e18CMD_CAN_BUSOFF_CLRE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e18CMD_CAN_BUSOFF_CLRE"></a> <a id="_CPPv2N14can_ctrl_cmd_e18CMD_CAN_BUSOFF_CLRE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799aa259ca5f8dbdbb3e3bea24f22bfe2ed7"></a> enumerator CMD\_CAN\_BUSOFF\_CLR

    <a id="_CPPv4N14can_ctrl_cmd_e16CMD_CAN_GET_KOERE"></a>

    <a id="_CPPv3N14can_ctrl_cmd_e16CMD_CAN_GET_KOERE"></a> <a id="_CPPv2N14can_ctrl_cmd_e16CMD_CAN_GET_KOERE"></a> <a id="hal__can__types_8h_1a26dc5d730d7b9a60bd4d7a26792b8799a2d22af5cd782404e633a488cf032ede9"></a> enumerator CMD\_CAN\_GET\_KOER

<a id="_CPPv412drv_switch_e"></a>

<a id="_CPPv312drv_switch_e"></a> <a id="_CPPv212drv_switch_e"></a> <a id="hal__can__types_8h_1a4da819e4f4a7b08f842f0bfe54a335d5"></a> enum drv\_switch\_e
:   *Values:*

    <a id="_CPPv4N12drv_switch_e14DRIVER_DISABLEE"></a>

    <a id="_CPPv3N12drv_switch_e14DRIVER_DISABLEE"></a> <a id="_CPPv2N12drv_switch_e14DRIVER_DISABLEE"></a> <a id="hal__can__types_8h_1a4da819e4f4a7b08f842f0bfe54a335d5ab67143fab9225c20d3c2e4077c27896f"></a> enumerator DRIVER\_DISABLE

    <a id="_CPPv4N12drv_switch_e13DRIVER_ENABLEE"></a>

    <a id="_CPPv3N12drv_switch_e13DRIVER_ENABLEE"></a> <a id="_CPPv2N12drv_switch_e13DRIVER_ENABLEE"></a> <a id="hal__can__types_8h_1a4da819e4f4a7b08f842f0bfe54a335d5a0a33f4daffb549055ca1c850daa90790"></a> enumerator DRIVER\_ENABLE

<a id="_CPPv413can_err_int_e"></a>

<a id="_CPPv313can_err_int_e"></a> <a id="_CPPv213can_err_int_e"></a> <a id="hal__can__types_8h_1aa2ab39432ae8416e00326e5ed0bc6594"></a> enum can\_err\_int\_e
:   *Values:*

    <a id="_CPPv4N13can_err_int_e14CAN_ERRINT_BUSE"></a>

    <a id="_CPPv3N13can_err_int_e14CAN_ERRINT_BUSE"></a> <a id="_CPPv2N13can_err_int_e14CAN_ERRINT_BUSE"></a> <a id="hal__can__types_8h_1aa2ab39432ae8416e00326e5ed0bc6594a94c5d04d0694745db8390f875da7cb4e"></a> enumerator CAN\_ERRINT\_BUS

    <a id="_CPPv4N13can_err_int_e19CAN_ERRINT_ARB_LOSTE"></a>

    <a id="_CPPv3N13can_err_int_e19CAN_ERRINT_ARB_LOSTE"></a> <a id="_CPPv2N13can_err_int_e19CAN_ERRINT_ARB_LOSTE"></a> <a id="hal__can__types_8h_1aa2ab39432ae8416e00326e5ed0bc6594a8c004a950ebba196bef34bcacc3f9710"></a> enumerator CAN\_ERRINT\_ARB\_LOST

    <a id="_CPPv4N13can_err_int_e18CAN_ERRINT_PASSIVEE"></a>

    <a id="_CPPv3N13can_err_int_e18CAN_ERRINT_PASSIVEE"></a> <a id="_CPPv2N13can_err_int_e18CAN_ERRINT_PASSIVEE"></a> <a id="hal__can__types_8h_1aa2ab39432ae8416e00326e5ed0bc6594a0d9221aab7652bdf0f2d98cd81f96139"></a> enumerator CAN\_ERRINT\_PASSIVE

    <a id="_CPPv4N13can_err_int_e19CAN_ERRINT_WARN_LIME"></a>

    <a id="_CPPv3N13can_err_int_e19CAN_ERRINT_WARN_LIME"></a> <a id="_CPPv2N13can_err_int_e19CAN_ERRINT_WARN_LIME"></a> <a id="hal__can__types_8h_1aa2ab39432ae8416e00326e5ed0bc6594ae45f50f0269602fb8f3ac7b64e14c4c0"></a> enumerator CAN\_ERRINT\_WARN\_LIM

<a id="_CPPv414can_protocol_e"></a>

<a id="_CPPv314can_protocol_e"></a> <a id="_CPPv214can_protocol_e"></a> <a id="hal__can__types_8h_1ac38a077b8db32d96ffef5b57afe3f683"></a> enum can\_protocol\_e
:   *Values:*

    <a id="_CPPv4N14can_protocol_e17CAN_PROTO_CLASSICE"></a>

    <a id="_CPPv3N14can_protocol_e17CAN_PROTO_CLASSICE"></a> <a id="_CPPv2N14can_protocol_e17CAN_PROTO_CLASSICE"></a> <a id="hal__can__types_8h_1ac38a077b8db32d96ffef5b57afe3f683a6a2e80c6fc8d11db4865f33cc6360be0"></a> enumerator CAN\_PROTO\_CLASSIC
    :   Classic CAN

    <a id="_CPPv4N14can_protocol_e12CAN_PROTO_FDE"></a>

    <a id="_CPPv3N14can_protocol_e12CAN_PROTO_FDE"></a> <a id="_CPPv2N14can_protocol_e12CAN_PROTO_FDE"></a> <a id="hal__can__types_8h_1ac38a077b8db32d96ffef5b57afe3f683a23322d79ea742e25d5d06b6dddf565d2"></a> enumerator CAN\_PROTO\_FD
    :   CAN FD

<a id="_CPPv410can_form_e"></a>

<a id="_CPPv310can_form_e"></a> <a id="_CPPv210can_form_e"></a> <a id="hal__can__types_8h_1a0e4b6eb7dd0e7426179cba42594f2c6d"></a> enum can\_form\_e
:   *Values:*

    <a id="_CPPv4N10can_form_e12CAN_FORM_STDE"></a>

    <a id="_CPPv3N10can_form_e12CAN_FORM_STDE"></a> <a id="_CPPv2N10can_form_e12CAN_FORM_STDE"></a> <a id="hal__can__types_8h_1a0e4b6eb7dd0e7426179cba42594f2c6dac1708ab068ce23bd8d686f5e354e1c4d"></a> enumerator CAN\_FORM\_STD

    <a id="_CPPv4N10can_form_e12CAN_FORM_EXTE"></a>

    <a id="_CPPv3N10can_form_e12CAN_FORM_EXTE"></a> <a id="_CPPv2N10can_form_e12CAN_FORM_EXTE"></a> <a id="hal__can__types_8h_1a0e4b6eb7dd0e7426179cba42594f2c6dabb789e21db3e0132cd3421be052a38df"></a> enumerator CAN\_FORM\_EXT

<a id="_CPPv411can_frame_e"></a>

<a id="_CPPv311can_frame_e"></a> <a id="_CPPv211can_frame_e"></a> <a id="hal__can__types_8h_1aaa3b0f536cadcc1dd90e4d25e12cc9a6"></a> enum can\_frame\_e
:   *Values:*

    <a id="_CPPv4N11can_frame_e14CAN_FRAME_DATAE"></a>

    <a id="_CPPv3N11can_frame_e14CAN_FRAME_DATAE"></a> <a id="_CPPv2N11can_frame_e14CAN_FRAME_DATAE"></a> <a id="hal__can__types_8h_1aaa3b0f536cadcc1dd90e4d25e12cc9a6a6ecca1e3eba0ac7333b06c88fde51c34"></a> enumerator CAN\_FRAME\_DATA

    <a id="_CPPv4N11can_frame_e14CAN_FRAME_REMTE"></a>

    <a id="_CPPv3N11can_frame_e14CAN_FRAME_REMTE"></a> <a id="_CPPv2N11can_frame_e14CAN_FRAME_REMTE"></a> <a id="hal__can__types_8h_1aaa3b0f536cadcc1dd90e4d25e12cc9a6af22776e6e9d8238f4cbdf496cd7922ac"></a> enumerator CAN\_FRAME\_REMT

<a id="_CPPv411can_brate_e"></a>

<a id="_CPPv311can_brate_e"></a> <a id="_CPPv211can_brate_e"></a> <a id="hal__can__types_8h_1a0f8690b506af887396488deba663f50e"></a> enum can\_brate\_e
:   *Values:*

    <a id="_CPPv4N11can_brate_e17CAN_BIT_RATE_SLOWE"></a>

    <a id="_CPPv3N11can_brate_e17CAN_BIT_RATE_SLOWE"></a> <a id="_CPPv2N11can_brate_e17CAN_BIT_RATE_SLOWE"></a> <a id="hal__can__types_8h_1a0f8690b506af887396488deba663f50ea6b360417d9ed08290961ed02c9a42206"></a> enumerator CAN\_BIT\_RATE\_SLOW

    <a id="_CPPv4N11can_brate_e17CAN_BIT_RATE_FASTE"></a>

    <a id="_CPPv3N11can_brate_e17CAN_BIT_RATE_FASTE"></a> <a id="_CPPv2N11can_brate_e17CAN_BIT_RATE_FASTE"></a> <a id="hal__can__types_8h_1a0f8690b506af887396488deba663f50ea3fa8e7eed20b88d64cc42a21a1c25edb"></a> enumerator CAN\_BIT\_RATE\_FAST

<a id="_CPPv418can_acc_mask_ide_e"></a>

<a id="_CPPv318can_acc_mask_ide_e"></a> <a id="_CPPv218can_acc_mask_ide_e"></a> <a id="hal__can__types_8h_1a55c2df8ad3bfa762cd32db84fc53acca"></a> enum can\_acc\_mask\_ide\_e
:   *Values:*

    <a id="_CPPv4N18can_acc_mask_ide_e15CAN_ACCEPT_BOTHE"></a>

    <a id="_CPPv3N18can_acc_mask_ide_e15CAN_ACCEPT_BOTHE"></a> <a id="_CPPv2N18can_acc_mask_ide_e15CAN_ACCEPT_BOTHE"></a> <a id="hal__can__types_8h_1a55c2df8ad3bfa762cd32db84fc53accaa3827c4e3ef86706ee8f75026401b51e2"></a> enumerator CAN\_ACCEPT\_BOTH

    <a id="_CPPv4N18can_acc_mask_ide_e19CAN_ACCEPT_STANDARDE"></a>

    <a id="_CPPv3N18can_acc_mask_ide_e19CAN_ACCEPT_STANDARDE"></a> <a id="_CPPv2N18can_acc_mask_ide_e19CAN_ACCEPT_STANDARDE"></a> <a id="hal__can__types_8h_1a55c2df8ad3bfa762cd32db84fc53accaa8de1da8fc0ec92eae30c70101feb65fd"></a> enumerator CAN\_ACCEPT\_STANDARD

    <a id="_CPPv4N18can_acc_mask_ide_e19CAN_ACCEPT_EXTENDEDE"></a>

    <a id="_CPPv3N18can_acc_mask_ide_e19CAN_ACCEPT_EXTENDEDE"></a> <a id="_CPPv2N18can_acc_mask_ide_e19CAN_ACCEPT_EXTENDEDE"></a> <a id="hal__can__types_8h_1a55c2df8ad3bfa762cd32db84fc53accaa84ed923793b4607bd32f9f76b864c74f"></a> enumerator CAN\_ACCEPT\_EXTENDED

<a id="_CPPv415can_loc_reset_c"></a>

<a id="_CPPv315can_loc_reset_c"></a> <a id="_CPPv215can_loc_reset_c"></a> <a id="hal__can__types_8h_1a8eea0f9892310e6c666160cf63e59b9e"></a> enum can\_loc\_reset\_c
:   *Values:*

    <a id="_CPPv4N15can_loc_reset_c16CAN_RESET_REQ_ENE"></a>

    <a id="_CPPv3N15can_loc_reset_c16CAN_RESET_REQ_ENE"></a> <a id="_CPPv2N15can_loc_reset_c16CAN_RESET_REQ_ENE"></a> <a id="hal__can__types_8h_1a8eea0f9892310e6c666160cf63e59b9ea2717e929f7a9321aaea41c87c1d3bafe"></a> enumerator CAN\_RESET\_REQ\_EN

    <a id="_CPPv4N15can_loc_reset_c16CAN_RESET_REQ_NOE"></a>

    <a id="_CPPv3N15can_loc_reset_c16CAN_RESET_REQ_NOE"></a> <a id="_CPPv2N15can_loc_reset_c16CAN_RESET_REQ_NOE"></a> <a id="hal__can__types_8h_1a8eea0f9892310e6c666160cf63e59b9eaf4956a2e27e337b66ed89a505bb7cc5a"></a> enumerator CAN\_RESET\_REQ\_NO

<a id="_CPPv418can_trans_switch_c"></a>

<a id="_CPPv318can_trans_switch_c"></a> <a id="_CPPv218can_trans_switch_c"></a> <a id="hal__can__types_8h_1addd0ed8e827939fba3dd35081271f9f3"></a> enum can\_trans\_switch\_c
:   *Values:*

    <a id="_CPPv4N18can_trans_switch_c7CAN_TPEE"></a>

    <a id="_CPPv3N18can_trans_switch_c7CAN_TPEE"></a> <a id="_CPPv2N18can_trans_switch_c7CAN_TPEE"></a> <a id="hal__can__types_8h_1addd0ed8e827939fba3dd35081271f9f3a060d001985383fe17613519a912c2252"></a> enumerator CAN\_TPE

    <a id="_CPPv4N18can_trans_switch_c7CAN_TPAE"></a>

    <a id="_CPPv3N18can_trans_switch_c7CAN_TPAE"></a> <a id="_CPPv2N18can_trans_switch_c7CAN_TPAE"></a> <a id="hal__can__types_8h_1addd0ed8e827939fba3dd35081271f9f3abe1a4d0ac960696ec0e0453ebe1ae0e7"></a> enumerator CAN\_TPA

    <a id="_CPPv4N18can_trans_switch_c9CAN_TSONEE"></a>

    <a id="_CPPv3N18can_trans_switch_c9CAN_TSONEE"></a> <a id="_CPPv2N18can_trans_switch_c9CAN_TSONEE"></a> <a id="hal__can__types_8h_1addd0ed8e827939fba3dd35081271f9f3a8044b38aec89ec9cd06deb0d0f7bb966"></a> enumerator CAN\_TSONE

    <a id="_CPPv4N18can_trans_switch_c9CAN_TSALLE"></a>

    <a id="_CPPv3N18can_trans_switch_c9CAN_TSALLE"></a> <a id="_CPPv2N18can_trans_switch_c9CAN_TSALLE"></a> <a id="hal__can__types_8h_1addd0ed8e827939fba3dd35081271f9f3aad22a7f35d8ea42fa07057a0ef11168e"></a> enumerator CAN\_TSALL

    <a id="_CPPv4N18can_trans_switch_c7CAN_TSAE"></a>

    <a id="_CPPv3N18can_trans_switch_c7CAN_TSAE"></a> <a id="_CPPv2N18can_trans_switch_c7CAN_TSAE"></a> <a id="hal__can__types_8h_1addd0ed8e827939fba3dd35081271f9f3a795ae6e3fb129092d37e260c0d070285"></a> enumerator CAN\_TSA

<a id="_CPPv415can_koer_code_e"></a>

<a id="_CPPv315can_koer_code_e"></a> <a id="_CPPv215can_koer_code_e"></a> <a id="hal__can__types_8h_1a16f04630f165e0923c37727b219ba5bb"></a> enum can\_koer\_code\_e
:   *Values:*

    <a id="_CPPv4N15can_koer_code_e11CAN_KOER_NOE"></a>

    <a id="_CPPv3N15can_koer_code_e11CAN_KOER_NOE"></a> <a id="_CPPv2N15can_koer_code_e11CAN_KOER_NOE"></a> <a id="hal__can__types_8h_1a16f04630f165e0923c37727b219ba5bba96990ef16486ef73ea570107d52fc364"></a> enumerator CAN\_KOER\_NO

    <a id="_CPPv4N15can_koer_code_e12CAN_KOER_BITE"></a>

    <a id="_CPPv3N15can_koer_code_e12CAN_KOER_BITE"></a> <a id="_CPPv2N15can_koer_code_e12CAN_KOER_BITE"></a> <a id="hal__can__types_8h_1a16f04630f165e0923c37727b219ba5bba6aa231364103e67ab5d83b59855178e0"></a> enumerator CAN\_KOER\_BIT

    <a id="_CPPv4N15can_koer_code_e13CAN_KOER_FORME"></a>

    <a id="_CPPv3N15can_koer_code_e13CAN_KOER_FORME"></a> <a id="_CPPv2N15can_koer_code_e13CAN_KOER_FORME"></a> <a id="hal__can__types_8h_1a16f04630f165e0923c37727b219ba5bba1fde0079e90b068315143023d9ea50a0"></a> enumerator CAN\_KOER\_FORM

    <a id="_CPPv4N15can_koer_code_e14CAN_KOER_STUFFE"></a>

    <a id="_CPPv3N15can_koer_code_e14CAN_KOER_STUFFE"></a> <a id="_CPPv2N15can_koer_code_e14CAN_KOER_STUFFE"></a> <a id="hal__can__types_8h_1a16f04630f165e0923c37727b219ba5bba69623e2e6e187e957323f4e282a64ebc"></a> enumerator CAN\_KOER\_STUFF

    <a id="_CPPv4N15can_koer_code_e12CAN_KOER_ACKE"></a>

    <a id="_CPPv3N15can_koer_code_e12CAN_KOER_ACKE"></a> <a id="_CPPv2N15can_koer_code_e12CAN_KOER_ACKE"></a> <a id="hal__can__types_8h_1a16f04630f165e0923c37727b219ba5bbad426a9634ce0e8ddd7e221d63def7543"></a> enumerator CAN\_KOER\_ACK

    <a id="_CPPv4N15can_koer_code_e12CAN_KOER_CRCE"></a>

    <a id="_CPPv3N15can_koer_code_e12CAN_KOER_CRCE"></a> <a id="_CPPv2N15can_koer_code_e12CAN_KOER_CRCE"></a> <a id="hal__can__types_8h_1a16f04630f165e0923c37727b219ba5bbae5766567aecdae1e26df67006f9e03dc"></a> enumerator CAN\_KOER\_CRC

    <a id="_CPPv4N15can_koer_code_e14CAN_KOER_OTHERE"></a>

    <a id="_CPPv3N15can_koer_code_e14CAN_KOER_OTHERE"></a> <a id="_CPPv2N15can_koer_code_e14CAN_KOER_OTHERE"></a> <a id="hal__can__types_8h_1a16f04630f165e0923c37727b219ba5bba1c3d0fc696653696efcd2fd5f14a1f3b"></a> enumerator CAN\_KOER\_OTHER

    <a id="_CPPv4N15can_koer_code_e14CAN_KOER_NOUSEE"></a>

    <a id="_CPPv3N15can_koer_code_e14CAN_KOER_NOUSEE"></a> <a id="_CPPv2N15can_koer_code_e14CAN_KOER_NOUSEE"></a> <a id="hal__can__types_8h_1a16f04630f165e0923c37727b219ba5bbace51f67113b0ea52abdf77186421b383"></a> enumerator CAN\_KOER\_NOUSE
