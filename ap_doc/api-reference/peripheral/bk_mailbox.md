# Mailbox


备注

BK7259 应用层跨核通信请使用 [多核 Mailbox API](../system/logic_mailbox.md "../system/logic_mailbox.md") 中的
mb_chnl 系列接口。本节 bk_mailbox 为底层硬件 Mailbox 驱动，一般由中间件内部使用，
不建议应用直接调用。


## Mailbox API Status

| API | BK7259_AP |
| --- | --- |
| [`bk_mailbox_init()`](#_CPPv415bk_mailbox_initv "bk_mailbox_init") | 内部使用 |
| [`bk_mailbox_deinit()`](#_CPPv417bk_mailbox_deinitv "bk_mailbox_deinit") | 内部使用 |
| [`bk_mailbox_set_param()`](#_CPPv420bk_mailbox_set_paramP14mailbox_data_t8uint32_t8uint32_t8uint32_t8uint32_t "bk_mailbox_set_param") | 内部使用 |
| [`bk_mailbox_recv_callback_register()`](#_CPPv433bk_mailbox_recv_callback_register18mailbox_endpoint_t18mailbox_endpoint_t18mailbox_callback_t "bk_mailbox_recv_callback_register") | 内部使用 |
| [`bk_mailbox_recv_callback_unregister()`](#_CPPv435bk_mailbox_recv_callback_unregister18mailbox_endpoint_t18mailbox_endpoint_t "bk_mailbox_recv_callback_unregister") | 内部使用 |
| [`bk_mailbox_send()`](#_CPPv415bk_mailbox_sendP14mailbox_data_t18mailbox_endpoint_t18mailbox_endpoint_tPv "bk_mailbox_send") | 内部使用 |


## Mailbox UNIT Number

| Capability | BK7259_AP |
| --- | --- |
| UNIT Number | 2 |


## Mailbox API Reference


### Header File


- [mailbox.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/mailbox.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/mailbox.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_mailbox_init(void)
:   Init the MAILBOX driver.

    This API init the resoure common to all MAILBOXs:


    - Init MAILBOX driver control register

    - Configure MAILBOX interrupt handling function

    This API should be called before any other MAILBOX APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_mailbox_deinit(void)
:   Deinit the MAILBOX driver.

    This API free all resource related to MAILBOX.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_mailbox_set_param([mailbox_data_t](#_CPPv414mailbox_data_t "mailbox_data_t") *data, uint32_t p0, uint32_t p1, uint32_t p2, uint32_t p3)
:   Configure the MAILBOX cmd and data.

    This API is used to configure data. Write parameters to variables as required by the structure, [mailbox_data_t](#structmailbox__data__t "#structmailbox__data__t").

    example: [mailbox_data_t](#structmailbox__data__t "#structmailbox__data__t") send_data; uint32_t param0 = 123456; uint32_t param1 = 111; uint32_t param2 = 666; uint32_t param3 = 888; mailbox_set_param(&send_data, param0, param1, param2, param3);

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_mailbox_recv_callback_register([mailbox_endpoint_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") src, [mailbox_endpoint_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") dst, [mailbox_callback_t](#_CPPv418mailbox_callback_t "mailbox_callback_t") callback)
:   Register the callback function for MAILBOX.


    **Attention**
    :   src : Associated with the CPU that needs to send data dst : Associated with the CPU of the current code execution system callback: After receiving the data, it is transmitted to the correspongding processing function. example: The current code runs in CPU0 and receives data from CPU1.

        ```
           src = MAILBOX_CPU1;
           dst = MAILBOX_CPU0;
           callback = receive_from_CPU_1;
        ```

    返回
    :   - BK_OK: succeed

        - BK_ERR_MAILBOX_SRC_DST: MAILBOX data transmission direction error

        - BK_ERR_MAILBOX_CALLBACK: Insufficient space or wrong format of registered function, etc

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_mailbox_recv_callback_unregister([mailbox_endpoint_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") src, [mailbox_endpoint_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") dst)
:   Unregister the callback function for MAILBOX.


    **Attention**
    :   src : Associated with the CPU that needs to send data dst : Associated with the CPU of the current code execution system callback: After receiving the data, it is transmitted to the correspongding processing function. example: The current code runs in CPU0 and receives data from CPU1.

        ```
           src = MAILBOX_CPU1
           dst = MAILBOX_CPU0
        ```

    返回
    :   - BK_OK: succeed

        - BK_ERR_MAILBOX_SRC_DST: MAILBOX data transmission direction error.

        - BK_ERR_MAILBOX_CALLBACK: Callback function is not registered.

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_mailbox_send([mailbox_data_t](#_CPPv414mailbox_data_t "mailbox_data_t") *data, [mailbox_endpoint_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") src, [mailbox_endpoint_t](#_CPPv418mailbox_endpoint_t "mailbox_endpoint_t") dst, void *arg)
:   Unregister the callback function for MAILBOX.

    example: The current code runs in CPU0 and send data to CPU1.

    ```
       src = MAILBOX_ENDPOINT_CPU0
       dst = MAILBOX_CPU1
       data : mbx ('by mailbox_set_param(&mbx, p0, p1, p2, p3)')
    ```


    **Attention**
    :   Before sending data, need to use the mailbox_set_param() to configure the data format.

    返回
    :   - BK_OK: succeed

        - BK_ERR_MAILBOX_SRC_DST: MAILBOX data transmission direction error.

        - BK_ERR_MAILBOX_BOX: No empty box store data.

        - BK_ERR_MAILBOX_TIMEOUT: Timeout waiting for the opposite end to fetch data.

        - others: other errors.


## Mailbox Typedefs


### Header File


- [mailbox_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/mailbox_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/mailbox_types.h")


### Structures

struct mailbox_data_t
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


### Macros

BK_ERR_MAILBOX_SRC_DST
:   MAILBOX source address error

BK_ERR_MAILBOX_ID
:   MAILBOX BOX number error

BK_ERR_MAILBOX_FLAG
:   MAILBOX flag error

BK_ERR_MAILBOX_CALLBACK
:   MAILBOX callback function error

BK_ERR_MAILBOX_TIMEOUT
:   MAILBOX waite timeout

BK_ERR_MAILBOX_NOT_INIT
:   MAILBOX isnt init

BK_ERR_MAILBOX_REPEAT_INIT
:   MAILBOX repeat init


### Type Definitions

typedef void (*mailbox_callback_t)([mailbox_data_t](#_CPPv414mailbox_data_t "mailbox_data_t") *data)
:   MAILBOX interrupt service routine.


### Enumerations

enum mailbox_endpoint_t
:   *Values:*

    enumerator MAILBOX_CPU0
    :   MAILBOX CPU0 endpoint

    enumerator MAILBOX_CPU1
    :   MAILBOX CPU1 endpoint

    enumerator MAILBOX_CPU2
    :   MAILBOX CPU2 endpoint

    enumerator MAILBOX_CPU3
    :   MAILBOX CPU3 endpoint

    enumerator MAILBOX_DSP
    :   MAILBOX DSP endpoint

    enumerator MAILBOX_ENDPOINT_INVALID
    :   MAILBOX invalid endpoint


### Header File


- [hal/hal_mailbox_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_mailbox_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_mailbox_types.h")


### Type Definitions

typedef uint32_t mailbox_id_t

typedef uint32_t mailbox_ep_config_t
