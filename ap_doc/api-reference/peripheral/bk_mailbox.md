---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_mailbox.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="mailbox"></a>

# Mailbox

备注

BK7259 应用层跨核通信请使用 [多核 Mailbox API](../system/logic_mailbox.md) 中的
mb\_chnl 系列接口。本节 bk\_mailbox 为底层硬件 Mailbox 驱动，一般由中间件内部使用，
不建议应用直接调用。

<a id="mailbox-api-status"></a>

## Mailbox API Status

| API | BK7259\_AP |
| --- | --- |
| [`bk_mailbox_init()`](#_CPPv415bk_mailbox_initv "bk_mailbox_init") | 内部使用 |
| [`bk_mailbox_deinit()`](#_CPPv417bk_mailbox_deinitv "bk_mailbox_deinit") | 内部使用 |
| [`bk_mailbox_set_param()`](#_CPPv420bk_mailbox_set_paramP14mailbox_data_t8uint32_t8uint32_t8uint32_t8uint32_t "bk_mailbox_set_param") | 内部使用 |
| [`bk_mailbox_recv_callback_register()`](#_CPPv433bk_mailbox_recv_callback_register18mailbox_endpoint_t18mailbox_endpoint_t18mailbox_callback_t "bk_mailbox_recv_callback_register") | 内部使用 |
| [`bk_mailbox_recv_callback_unregister()`](#_CPPv435bk_mailbox_recv_callback_unregister18mailbox_endpoint_t18mailbox_endpoint_t "bk_mailbox_recv_callback_unregister") | 内部使用 |
| [`bk_mailbox_send()`](#_CPPv415bk_mailbox_sendP14mailbox_data_t18mailbox_endpoint_t18mailbox_endpoint_tPv "bk_mailbox_send") | 内部使用 |

<a id="mailbox-unit-number"></a>

## Mailbox UNIT Number

| Capability | BK7259\_AP |
| --- | --- |
| UNIT Number | 2 |

<a id="mailbox-api-reference"></a>

## Mailbox API Reference

<a id="header-file"></a>

### Header File

- [mailbox.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/mailbox.h)

<a id="functions"></a>

### Functions

<a id="_CPPv415bk_mailbox_initv"></a>

<a id="_CPPv315bk_mailbox_initv"></a> <a id="_CPPv215bk_mailbox_initv"></a> <a id="bk_mailbox_init__void"></a> <a id="group__bk__api__mailbox_1ga4abaf2e5feda91dbf313d819c76fe649"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_mailbox\_init(void)
:   Init the MAILBOX driver.

    This API init the resoure common to all MAILBOXs:

    - Init MAILBOX driver control register
    - Configure MAILBOX interrupt handling function

    This API should be called before any other MAILBOX APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv417bk_mailbox_deinitv"></a>

<a id="_CPPv317bk_mailbox_deinitv"></a> <a id="_CPPv217bk_mailbox_deinitv"></a> <a id="bk_mailbox_deinit__void"></a> <a id="group__bk__api__mailbox_1ga7eb892156089bd429d75b20223d5fc9b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_mailbox\_deinit(void)
:   Deinit the MAILBOX driver.

    This API free all resource related to MAILBOX.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_mailbox_set_paramP14mailbox_data_t8uint32_t8uint32_t8uint32_t8uint32_t"></a>

<a id="_CPPv320bk_mailbox_set_paramP14mailbox_data_t8uint32_t8uint32_t8uint32_t8uint32_t"></a> <a id="_CPPv220bk_mailbox_set_paramP14mailbox_data_t8uint32_t8uint32_t8uint32_t8uint32_t"></a> <a id="bk_mailbox_set_param__mailbox_data_tP.uint32_t.uint32_t.uint32_t.uint32_t"></a> <a id="group__bk__api__mailbox_1gabfa628fb80db4ed8712d5e87f0537aa0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_mailbox\_set\_param([mailbox\_data\_t](#_CPPv414mailbox_data_t "mailbox_data_t") \*data, uint32\_t p0, uint32\_t p1, uint32\_t p2, uint32\_t p3)
:   Configure the MAILBOX cmd and data.

    This API is used to configure data. Write parameters to variables as required by the structure, [mailbox\_data\_t](#structmailbox__data__t).

    example: [mailbox\_data\_t](#structmailbox__data__t) send\_data; uint32\_t param0 \= 123456; uint32\_t param1 \= 111; uint32\_t param2 \= 666; uint32\_t param3 \= 888; mailbox\_set\_param(\&send\_data, param0, param1, param2, param3);

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv433bk_mailbox_recv_callback_register18mailbox_endpoint_t18mailbox_endpoint_t18mailbox_callback_t"></a>

<a id="_CPPv333bk_mailbox_recv_callback_register18mailbox_endpoint_t18mailbox_endpoint_t18mailbox_callback_t"></a> <a id="_CPPv233bk_mailbox_recv_callback_register18mailbox_endpoint_t18mailbox_endpoint_t18mailbox_callback_t"></a> <a id="bk_mailbox_recv_callback_register__mailbox_endpoint_t.mailbox_endpoint_t.mailbox_callback_t"></a> <a id="group__bk__api__mailbox_1ga8a5676f49f6f5f5ce7fd70efe58eae93"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_mailbox\_recv\_callback\_register([mailbox\_endpoint\_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") src, [mailbox\_endpoint\_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") dst, [mailbox\_callback\_t](#_CPPv418mailbox_callback_t "mailbox_callback_t") callback)
:   Register the callback function for MAILBOX.

    **Attention**
    :   src : Associated with the CPU that needs to send data dst : Associated with the CPU of the current code execution system callback: After receiving the data, it is transmitted to the correspongding processing function. example: The current code runs in CPU0 and receives data from CPU1.

        ```
           src = MAILBOX_CPU1;
           dst = MAILBOX_CPU0;
           callback = receive_from_CPU_1;
        ```

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_MAILBOX\_SRC\_DST: MAILBOX data transmission direction error
        - BK\_ERR\_MAILBOX\_CALLBACK: Insufficient space or wrong format of registered function, etc
        - others: other errors.

<a id="_CPPv435bk_mailbox_recv_callback_unregister18mailbox_endpoint_t18mailbox_endpoint_t"></a>

<a id="_CPPv335bk_mailbox_recv_callback_unregister18mailbox_endpoint_t18mailbox_endpoint_t"></a> <a id="_CPPv235bk_mailbox_recv_callback_unregister18mailbox_endpoint_t18mailbox_endpoint_t"></a> <a id="bk_mailbox_recv_callback_unregister__mailbox_endpoint_t.mailbox_endpoint_t"></a> <a id="group__bk__api__mailbox_1ga49770c6bd33a09366a31acc37ee00136"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_mailbox\_recv\_callback\_unregister([mailbox\_endpoint\_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") src, [mailbox\_endpoint\_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") dst)
:   Unregister the callback function for MAILBOX.

    **Attention**
    :   src : Associated with the CPU that needs to send data dst : Associated with the CPU of the current code execution system callback: After receiving the data, it is transmitted to the correspongding processing function. example: The current code runs in CPU0 and receives data from CPU1.

        ```
           src = MAILBOX_CPU1
           dst = MAILBOX_CPU0
        ```

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_MAILBOX\_SRC\_DST: MAILBOX data transmission direction error.
        - BK\_ERR\_MAILBOX\_CALLBACK: Callback function is not registered.
        - others: other errors.

<a id="_CPPv415bk_mailbox_sendP14mailbox_data_t18mailbox_endpoint_t18mailbox_endpoint_tPv"></a>

<a id="_CPPv315bk_mailbox_sendP14mailbox_data_t18mailbox_endpoint_t18mailbox_endpoint_tPv"></a> <a id="_CPPv215bk_mailbox_sendP14mailbox_data_t18mailbox_endpoint_t18mailbox_endpoint_tPv"></a> <a id="bk_mailbox_send__mailbox_data_tP.mailbox_endpoint_t.mailbox_endpoint_t.voidP"></a> <a id="group__bk__api__mailbox_1gab326b627407ef2aa459f3c6a862f17aa"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_mailbox\_send([mailbox\_data\_t](#_CPPv414mailbox_data_t "mailbox_data_t") \*data, [mailbox\_endpoint\_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") src, [mailbox\_endpoint\_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") dst, void \*arg)
:   Unregister the callback function for MAILBOX.

    example: The current code runs in CPU0 and send data to CPU1.

    ```
       src = MAILBOX_ENDPOINT_CPU0
       dst = MAILBOX_CPU1
       data : mbx ('by mailbox_set_param(&mbx, p0, p1, p2, p3)')
    ```

    **Attention**
    :   Before sending data, need to use the mailbox\_set\_param() to configure the data format.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_MAILBOX\_SRC\_DST: MAILBOX data transmission direction error.
        - BK\_ERR\_MAILBOX\_BOX: No empty box store data.
        - BK\_ERR\_MAILBOX\_TIMEOUT: Timeout waiting for the opposite end to fetch data.
        - others: other errors.

<a id="mailbox-typedefs"></a>

## Mailbox Typedefs

<a id="id1"></a>

### Header File

- [mailbox\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/mailbox_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv414mailbox_data_t"></a>

<a id="_CPPv314mailbox_data_t"></a> <a id="_CPPv214mailbox_data_t"></a> <a id="mailbox_data_t"></a> <a id="structmailbox__data__t"></a> struct mailbox\_data\_t
:   A MAILBOX has multiple boxes, one box has four spaces to fill in data Define the meaning of each space by user.

    ```
         |_____________________________|      |_____________________________|
         |_____________________________|      |_____________________________|
         | Mailbox0                    |      | Mailbox1                    |
         |______________|______________|      |______________|______________|
         |     box0     |     box1     |      |     box0     |     box1     |
         | ____________ | ____________ |      | ____________ | ____________ |
         | | param0   | | | param0   | |      | | param0   | | | param0   | |
         | | param1   | | | param1   | |      | | param1   | | | param1   | |
         | | param2   | | | param2   | |      | | param2   | | | param2   | |
         | | param3   | | | param3   | |      | | param3   | | | param3   | |
         | |__________| | |__________| |      | |__________| | |__________| |
         | _____________|______________|      |______________|______________|
         |_____________________________|      |_____________________________|
    ```

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14mailbox_data_t6param0E"></a>

    <a id="_CPPv3N14mailbox_data_t6param0E"></a> <a id="_CPPv2N14mailbox_data_t6param0E"></a> <a id="mailbox_data_t::param0__uint32_t"></a> <a id="structmailbox__data__t_1a336300269aef78efbbdf7b90f2b1d87e"></a> uint32\_t param0
    :   MAILBOX Space 0

    <a id="_CPPv4N14mailbox_data_t6param1E"></a>

    <a id="_CPPv3N14mailbox_data_t6param1E"></a> <a id="_CPPv2N14mailbox_data_t6param1E"></a> <a id="mailbox_data_t::param1__uint32_t"></a> <a id="structmailbox__data__t_1a3059426a25472a1b6738b4522b981c07"></a> uint32\_t param1
    :   MAILBOX Space 1

    <a id="_CPPv4N14mailbox_data_t6param2E"></a>

    <a id="_CPPv3N14mailbox_data_t6param2E"></a> <a id="_CPPv2N14mailbox_data_t6param2E"></a> <a id="mailbox_data_t::param2__uint32_t"></a> <a id="structmailbox__data__t_1a58174ad60d15deccea38bb483d34f68d"></a> uint32\_t param2
    :   MAILBOX Space 2

    <a id="_CPPv4N14mailbox_data_t6param3E"></a>

    <a id="_CPPv3N14mailbox_data_t6param3E"></a> <a id="_CPPv2N14mailbox_data_t6param3E"></a> <a id="mailbox_data_t::param3__uint32_t"></a> <a id="structmailbox__data__t_1aeda3f3eb7dfd0b1592c2b0705cc2b561"></a> uint32\_t param3
    :   MAILBOX Space 3

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_MAILBOX_SRC_DST"></a>

<a id="group__bk__api__mailbox_1gaf065aefb459b5f602dfdc8177d6b57b7"></a> BK\_ERR\_MAILBOX\_SRC\_DST
:   MAILBOX source address error

<a id="c.BK_ERR_MAILBOX_ID"></a>

<a id="group__bk__api__mailbox_1gaec83aae0de18ac85a1f12534e64abf35"></a> BK\_ERR\_MAILBOX\_ID
:   MAILBOX BOX number error

<a id="c.BK_ERR_MAILBOX_FLAG"></a>

<a id="group__bk__api__mailbox_1ga31c633cdd668c84579ffe7a45a62c18c"></a> BK\_ERR\_MAILBOX\_FLAG
:   MAILBOX flag error

<a id="c.BK_ERR_MAILBOX_CALLBACK"></a>

<a id="group__bk__api__mailbox_1ga37cfb7794bab6e78ec08a1a77acb3307"></a> BK\_ERR\_MAILBOX\_CALLBACK
:   MAILBOX callback function error

<a id="c.BK_ERR_MAILBOX_TIMEOUT"></a>

<a id="group__bk__api__mailbox_1ga7593d1bb51aae91185c29377986f6993"></a> BK\_ERR\_MAILBOX\_TIMEOUT
:   MAILBOX waite timeout

<a id="c.BK_ERR_MAILBOX_NOT_INIT"></a>

<a id="group__bk__api__mailbox_1ga47c92b3576138e03c3e0378ae03e125e"></a> BK\_ERR\_MAILBOX\_NOT\_INIT
:   MAILBOX isnt init

<a id="c.BK_ERR_MAILBOX_REPEAT_INIT"></a>

<a id="group__bk__api__mailbox_1gab8584aa5639b45d49803cce513cb540d"></a> BK\_ERR\_MAILBOX\_REPEAT\_INIT
:   MAILBOX repeat init

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv418mailbox_callback_t"></a>

<a id="_CPPv318mailbox_callback_t"></a> <a id="_CPPv218mailbox_callback_t"></a> <a id="mailbox_callback_t"></a> <a id="group__bk__api__mailbox_1gac578b66ce9322b3052113d0b0179a2aa"></a> typedef void (\*mailbox\_callback\_t)([mailbox\_data\_t](#_CPPv414mailbox_data_t "mailbox_data_t") \*data)
:   MAILBOX interrupt service routine.

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv418mailbox_endpoint_t"></a>

<a id="_CPPv318mailbox_endpoint_t"></a> <a id="_CPPv218mailbox_endpoint_t"></a> <a id="group__bk__api__mailbox_1gaa67cb975c4e0c247b5a9b8fb15679764"></a> enum mailbox\_endpoint\_t
:   *Values:*

    <a id="_CPPv4N18mailbox_endpoint_t12MAILBOX_CPU0E"></a>

    <a id="_CPPv3N18mailbox_endpoint_t12MAILBOX_CPU0E"></a> <a id="_CPPv2N18mailbox_endpoint_t12MAILBOX_CPU0E"></a> <a id="group__bk__api__mailbox_1ggaa67cb975c4e0c247b5a9b8fb15679764a2edc71b36baa9a9cf2477f1430f16429"></a> enumerator MAILBOX\_CPU0
    :   MAILBOX CPU0 endpoint

    <a id="_CPPv4N18mailbox_endpoint_t12MAILBOX_CPU1E"></a>

    <a id="_CPPv3N18mailbox_endpoint_t12MAILBOX_CPU1E"></a> <a id="_CPPv2N18mailbox_endpoint_t12MAILBOX_CPU1E"></a> <a id="group__bk__api__mailbox_1ggaa67cb975c4e0c247b5a9b8fb15679764a697e2e606fc657753a71cc0f8d3d027d"></a> enumerator MAILBOX\_CPU1
    :   MAILBOX CPU1 endpoint

    <a id="_CPPv4N18mailbox_endpoint_t12MAILBOX_CPU2E"></a>

    <a id="_CPPv3N18mailbox_endpoint_t12MAILBOX_CPU2E"></a> <a id="_CPPv2N18mailbox_endpoint_t12MAILBOX_CPU2E"></a> <a id="group__bk__api__mailbox_1ggaa67cb975c4e0c247b5a9b8fb15679764aae29aaa7a3d7dfbe33288ddd71ffafd0"></a> enumerator MAILBOX\_CPU2
    :   MAILBOX CPU2 endpoint

    <a id="_CPPv4N18mailbox_endpoint_t12MAILBOX_CPU3E"></a>

    <a id="_CPPv3N18mailbox_endpoint_t12MAILBOX_CPU3E"></a> <a id="_CPPv2N18mailbox_endpoint_t12MAILBOX_CPU3E"></a> <a id="group__bk__api__mailbox_1ggaa67cb975c4e0c247b5a9b8fb15679764ac4567d08e40b558b6a7277625f797644"></a> enumerator MAILBOX\_CPU3
    :   MAILBOX CPU3 endpoint

    <a id="_CPPv4N18mailbox_endpoint_t11MAILBOX_DSPE"></a>

    <a id="_CPPv3N18mailbox_endpoint_t11MAILBOX_DSPE"></a> <a id="_CPPv2N18mailbox_endpoint_t11MAILBOX_DSPE"></a> <a id="group__bk__api__mailbox_1ggaa67cb975c4e0c247b5a9b8fb15679764a089914052f33c0ef86ce17a58a241633"></a> enumerator MAILBOX\_DSP
    :   MAILBOX DSP endpoint

    <a id="_CPPv4N18mailbox_endpoint_t24MAILBOX_ENDPOINT_INVALIDE"></a>

    <a id="_CPPv3N18mailbox_endpoint_t24MAILBOX_ENDPOINT_INVALIDE"></a> <a id="_CPPv2N18mailbox_endpoint_t24MAILBOX_ENDPOINT_INVALIDE"></a> <a id="group__bk__api__mailbox_1ggaa67cb975c4e0c247b5a9b8fb15679764afb061fc4c3a99a81b539d898007785f6"></a> enumerator MAILBOX\_ENDPOINT\_INVALID
    :   MAILBOX invalid endpoint

<a id="id2"></a>

### Header File

- [hal\_mailbox\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_mailbox_types.h)

<a id="id3"></a>

### Type Definitions

<a id="_CPPv412mailbox_id_t"></a>

<a id="_CPPv312mailbox_id_t"></a> <a id="_CPPv212mailbox_id_t"></a> <a id="mailbox_id_t"></a> <a id="hal__mailbox__types_8h_1ad19384d6ca86df118dc8b4c3a1d081a3"></a> typedef uint32\_t mailbox\_id\_t

<a id="_CPPv419mailbox_ep_config_t"></a>

<a id="_CPPv319mailbox_ep_config_t"></a> <a id="_CPPv219mailbox_ep_config_t"></a> <a id="mailbox_ep_config_t"></a> <a id="hal__mailbox__types_8h_1acb536127a0b1a6cd8451ed653d8d6216"></a> typedef uint32\_t mailbox\_ep\_config\_t
