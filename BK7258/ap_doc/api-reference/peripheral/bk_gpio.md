---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_gpio.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="gpio"></a>

# GPIO 使用指南

<a id="gpio-api-status"></a>

## GPIO API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_gpio_driver_init()`](#_CPPv419bk_gpio_driver_initv "bk_gpio_driver_init") | Y |
| [`bk_gpio_driver_deinit()`](#_CPPv421bk_gpio_driver_deinitv "bk_gpio_driver_deinit") | Y |
| [`bk_gpio_enable_output()`](#_CPPv421bk_gpio_enable_output9gpio_id_t "bk_gpio_enable_output") | Y |
| [`bk_gpio_disable_output()`](#_CPPv422bk_gpio_disable_output9gpio_id_t "bk_gpio_disable_output") | Y |
| [`bk_gpio_enable_input()`](#_CPPv420bk_gpio_enable_input9gpio_id_t "bk_gpio_enable_input") | Y |
| [`bk_gpio_disable_input()`](#_CPPv421bk_gpio_disable_input9gpio_id_t "bk_gpio_disable_input") | Y |
| [`bk_gpio_enable_pull()`](#_CPPv419bk_gpio_enable_pull9gpio_id_t "bk_gpio_enable_pull") | Y |
| [`bk_gpio_disable_pull()`](#_CPPv420bk_gpio_disable_pull9gpio_id_t "bk_gpio_disable_pull") | Y |
| [`bk_gpio_pull_up()`](#_CPPv415bk_gpio_pull_up9gpio_id_t "bk_gpio_pull_up") | Y |
| [`bk_gpio_pull_down()`](#_CPPv417bk_gpio_pull_down9gpio_id_t "bk_gpio_pull_down") | Y |
| [`bk_gpio_set_output_high()`](#_CPPv423bk_gpio_set_output_high9gpio_id_t "bk_gpio_set_output_high") | Y |
| [`bk_gpio_set_output_low()`](#_CPPv422bk_gpio_set_output_low9gpio_id_t "bk_gpio_set_output_low") | Y |
| [`bk_gpio_get_input()`](#_CPPv417bk_gpio_get_input9gpio_id_t "bk_gpio_get_input") | Y |
| [`bk_gpio_set_config()`](#_CPPv418bk_gpio_set_config9gpio_id_tPK13gpio_config_t "bk_gpio_set_config") | Y |
| [`bk_gpio_register_isr()`](#_CPPv420bk_gpio_register_isr9gpio_id_t10gpio_isr_t "bk_gpio_register_isr") | Y |
| [`bk_gpio_enable_interrupt()`](#_CPPv424bk_gpio_enable_interrupt9gpio_id_t "bk_gpio_enable_interrupt") | Y |
| [`bk_gpio_disable_interrupt()`](#_CPPv425bk_gpio_disable_interrupt9gpio_id_t "bk_gpio_disable_interrupt") | Y |
| [`bk_gpio_set_interrupt_type()`](#_CPPv426bk_gpio_set_interrupt_type9gpio_id_t15gpio_int_type_t "bk_gpio_set_interrupt_type") | Y |

<a id="gpio-api-reference"></a>

## GPIO API Reference

<a id="header-file"></a>

### Header File

- [gpio.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/gpio.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419bk_gpio_driver_initv"></a>

<a id="_CPPv319bk_gpio_driver_initv"></a> <a id="_CPPv219bk_gpio_driver_initv"></a> <a id="bk_gpio_driver_init__void"></a> <a id="group__bk__api__gpio_1gacae1346ccd48c98d892fe82d0473cfde"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_driver\_init(void)
:   Init the GPIO driver.

    This API init the resoure common to all GPIO channels:

    - Init GPIO driver control memory

    This API should be called before any other GPIO APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_gpio_driver_deinitv"></a>

<a id="_CPPv321bk_gpio_driver_deinitv"></a> <a id="_CPPv221bk_gpio_driver_deinitv"></a> <a id="bk_gpio_driver_deinit__void"></a> <a id="group__bk__api__gpio_1ga1f1b3f85bc530c7bd4179fdcc3fb5868"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_driver\_deinit(void)
:   Deinit the GPIO driver.

    This API free all resource related to GPIO and power down all GPIO channels.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv417bk_gpio_set_value9gpio_id_t8uint32_t"></a>

<a id="_CPPv317bk_gpio_set_value9gpio_id_t8uint32_t"></a> <a id="_CPPv217bk_gpio_set_value9gpio_id_t8uint32_t"></a> <a id="bk_gpio_set_value__gpio_id_t.uint32_t"></a> <a id="group__bk__api__gpio_1ga6fb7ccbc222e0dc0a38bbc163a96407c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_set\_value(gpio\_id\_t id, uint32\_t v)
:   Direct set GPIO config value.

    @NOTES Please be care to use this API,unless you know the detail mean, because it will set the GPIO config value. Sometimes the special GPIO needs to re-used by one more owner, after the second owner re-used it, it should restore the config value. Before re-use a GPIO, the owner can call bk\_gpio\_get\_value and bakup it, after re-used finish, it call bk\_gpio\_set\_value to restore the prevous value.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv417bk_gpio_get_value9gpio_id_t"></a>

<a id="_CPPv317bk_gpio_get_value9gpio_id_t"></a> <a id="_CPPv217bk_gpio_get_value9gpio_id_t"></a> <a id="bk_gpio_get_value__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga21130dd4b1f24b16e8526226438f9b31"></a> uint32\_t bk\_gpio\_get\_value(gpio\_id\_t id)
:   get GPIO config value.

<a id="_CPPv421bk_gpio_enable_output9gpio_id_t"></a>

<a id="_CPPv321bk_gpio_enable_output9gpio_id_t"></a> <a id="_CPPv221bk_gpio_enable_output9gpio_id_t"></a> <a id="bk_gpio_enable_output__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga2973cb2479aaf6bbfe2efebd84d3985d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_enable\_output(gpio\_id\_t gpio\_id)
:   enable GPIO output mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv422bk_gpio_disable_output9gpio_id_t"></a>

<a id="_CPPv322bk_gpio_disable_output9gpio_id_t"></a> <a id="_CPPv222bk_gpio_disable_output9gpio_id_t"></a> <a id="bk_gpio_disable_output__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga2e177c4285dd8673b446bcd15db92126"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_disable\_output(gpio\_id\_t gpio\_id)
:   disable GPIO output mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv420bk_gpio_enable_input9gpio_id_t"></a>

<a id="_CPPv320bk_gpio_enable_input9gpio_id_t"></a> <a id="_CPPv220bk_gpio_enable_input9gpio_id_t"></a> <a id="bk_gpio_enable_input__gpio_id_t"></a> <a id="group__bk__api__gpio_1gaf9acdf13c743f920174bbb103f108ac7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_enable\_input(gpio\_id\_t gpio\_id)
:   enable GPIO input mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv421bk_gpio_disable_input9gpio_id_t"></a>

<a id="_CPPv321bk_gpio_disable_input9gpio_id_t"></a> <a id="_CPPv221bk_gpio_disable_input9gpio_id_t"></a> <a id="bk_gpio_disable_input__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga200faf135f7d18061fc1c4057bd48b6f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_disable\_input(gpio\_id\_t gpio\_id)
:   disable GPIO input mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv419bk_gpio_enable_pull9gpio_id_t"></a>

<a id="_CPPv319bk_gpio_enable_pull9gpio_id_t"></a> <a id="_CPPv219bk_gpio_enable_pull9gpio_id_t"></a> <a id="bk_gpio_enable_pull__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga231a1940364f61c699d2d4fba643a743"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_enable\_pull(gpio\_id\_t gpio\_id)
:   enable GPIO pull mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv420bk_gpio_disable_pull9gpio_id_t"></a>

<a id="_CPPv320bk_gpio_disable_pull9gpio_id_t"></a> <a id="_CPPv220bk_gpio_disable_pull9gpio_id_t"></a> <a id="bk_gpio_disable_pull__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga044f2ca367852a0ae8f85f9440db08f8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_disable\_pull(gpio\_id\_t gpio\_id)
:   disable gpio pull mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv415bk_gpio_pull_up9gpio_id_t"></a>

<a id="_CPPv315bk_gpio_pull_up9gpio_id_t"></a> <a id="_CPPv215bk_gpio_pull_up9gpio_id_t"></a> <a id="bk_gpio_pull_up__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga8d974991d0a7d561eda8bd14c9bfc3b5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_pull\_up(gpio\_id\_t gpio\_id)
:   set GPIO as pull up mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv417bk_gpio_pull_down9gpio_id_t"></a>

<a id="_CPPv317bk_gpio_pull_down9gpio_id_t"></a> <a id="_CPPv217bk_gpio_pull_down9gpio_id_t"></a> <a id="bk_gpio_pull_down__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga206cf499bae8f2d5b7057f8d3f3f21fe"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_pull\_down(gpio\_id\_t gpio\_id)
:   set GPIO as pull down mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv418bk_gpio_get_output9gpio_id_t"></a>

<a id="_CPPv318bk_gpio_get_output9gpio_id_t"></a> <a id="_CPPv218bk_gpio_get_output9gpio_id_t"></a> <a id="bk_gpio_get_output__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga7f0727891df79177a60026077b694db8"></a> bool bk\_gpio\_get\_output(gpio\_id\_t gpio\_id)
:   Get the GPIO output value,.

    This API get GPIO’s output level: 0 :low\_level 1:high\_level.

    返回
    :   - input value
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - BK\_ERR\_GPIO\_NOT\_OUTPUT\_MODE : GPIO is not output mode
        - others: other errors.

<a id="_CPPv418bk_gpio_set_config9gpio_id_tPK13gpio_config_t"></a>

<a id="_CPPv318bk_gpio_set_config9gpio_id_tPK13gpio_config_t"></a> <a id="_CPPv218bk_gpio_set_config9gpio_id_tPK13gpio_config_t"></a> <a id="bk_gpio_set_config__gpio_id_t.gpio_config_tCP"></a> <a id="group__bk__api__gpio_1gabc229ebbc3ae486f8538789a61491bc7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_set\_config(gpio\_id\_t gpio\_id, const gpio\_config\_t \*config)
:   Config the GPIO mode.

    This API config GPIO’s mode

    - BK\_OK: succeed
    - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
    - BK\_ERR\_GPIO\_INVALID\_MODE: invalid GPIO’s io\_mode/pull\_mode
    - BK\_ERR\_GPIO\_INTERNAL\_USED:GPIO was map to another device
    - others: other errors.

<a id="_CPPv423bk_gpio_set_output_high9gpio_id_t"></a>

<a id="_CPPv323bk_gpio_set_output_high9gpio_id_t"></a> <a id="_CPPv223bk_gpio_set_output_high9gpio_id_t"></a> <a id="bk_gpio_set_output_high__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga6813699d36a76f6ed87e72c6f90a0592"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_set\_output\_high(gpio\_id\_t gpio\_id)
:   Set the GPIO output high,.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - BK\_ERR\_GPIO\_NOT\_OUTPUT\_MODE:GPIO not in output mode
        - others: other errors.

<a id="_CPPv422bk_gpio_set_output_low9gpio_id_t"></a>

<a id="_CPPv322bk_gpio_set_output_low9gpio_id_t"></a> <a id="_CPPv222bk_gpio_set_output_low9gpio_id_t"></a> <a id="bk_gpio_set_output_low__gpio_id_t"></a> <a id="group__bk__api__gpio_1gad53b1f39990fd6d6d051b75b0424dd9c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_set\_output\_low(gpio\_id\_t gpio\_id)
:   Set the GPIO output low,.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - BK\_ERR\_GPIO\_NOT\_OUTPUT\_MODE:GPIO not in output mode
        - others: other errors.

<a id="_CPPv424bk_gpio_set_output_value9gpio_id_tb"></a>

<a id="_CPPv324bk_gpio_set_output_value9gpio_id_tb"></a> <a id="_CPPv224bk_gpio_set_output_value9gpio_id_tb"></a> <a id="bk_gpio_set_output_value__gpio_id_t.b"></a> <a id="group__bk__api__gpio_1ga0e61fdc7d71303db4c77be22f91c3a2b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_set\_output\_value(gpio\_id\_t gpio\_id, bool value)
:   Set the GPIO output value,.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv417bk_gpio_get_input9gpio_id_t"></a>

<a id="_CPPv317bk_gpio_get_input9gpio_id_t"></a> <a id="_CPPv217bk_gpio_get_input9gpio_id_t"></a> <a id="bk_gpio_get_input__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga71b4f9272a2c8bc27d906f2de602bce2"></a> bool bk\_gpio\_get\_input(gpio\_id\_t gpio\_id)
:   Get the GPIO input value,.

    This API get GPIO’s input level: 0 :low\_level 1:high\_level.

    返回
    :   - input value
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - BK\_ERR\_GPIO\_NOT\_INPUT\_MODE : GPIO is not input mode
        - others: other errors.

<a id="_CPPv420bk_gpio_set_capacity9gpio_id_t6uint32"></a>

<a id="_CPPv320bk_gpio_set_capacity9gpio_id_t6uint32"></a> <a id="_CPPv220bk_gpio_set_capacity9gpio_id_t6uint32"></a> <a id="bk_gpio_set_capacity__gpio_id_t.uint32"></a> <a id="group__bk__api__gpio_1ga2e422b1299cf61773beedbddcdc15c47"></a> bool bk\_gpio\_set\_capacity(gpio\_id\_t gpio\_id, uint32 capacity)
:   Set the GPIO driver capacity.

    This API Set GPIO’s output driver capacity which range is 0\~3.

    返回
    :   - input value
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - BK\_ERR\_GPIO\_NOT\_INPUT\_MODE : GPIO is not input mode
        - others: other errors.

<a id="_CPPv426bk_gpio_set_interrupt_type9gpio_id_t15gpio_int_type_t"></a>

<a id="_CPPv326bk_gpio_set_interrupt_type9gpio_id_t15gpio_int_type_t"></a> <a id="_CPPv226bk_gpio_set_interrupt_type9gpio_id_t15gpio_int_type_t"></a> <a id="bk_gpio_set_interrupt_type__gpio_id_t.gpio_int_type_t"></a> <a id="group__bk__api__gpio_1ga33259d746c51989bbeb0d98956570235"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_set\_interrupt\_type(gpio\_id\_t gpio\_id, gpio\_int\_type\_t type)
:   Config the GPIO intterrupt type mode when use gpio intterrupt mode,.

    This API config all GPIO channels’ intterrupt mode, the mode included in gpio\_int\_type\_t.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - BK\_ERR\_GPIO\_INVALID\_INT\_TYPE: invalid GPIO int type
        - others: other errors.

<a id="_CPPv424bk_gpio_enable_interrupt9gpio_id_t"></a>

<a id="_CPPv324bk_gpio_enable_interrupt9gpio_id_t"></a> <a id="_CPPv224bk_gpio_enable_interrupt9gpio_id_t"></a> <a id="bk_gpio_enable_interrupt__gpio_id_t"></a> <a id="group__bk__api__gpio_1gacd7ff15a6390a73472c435411da6c660"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_enable\_interrupt(gpio\_id\_t id)
:   Enable GPIO intterrupt.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - BK\_ERR\_GPIO\_NOT\_INPUT\_MODE : GPIO is not input mode
        - others: other errors.

<a id="_CPPv425bk_gpio_disable_interrupt9gpio_id_t"></a>

<a id="_CPPv325bk_gpio_disable_interrupt9gpio_id_t"></a> <a id="_CPPv225bk_gpio_disable_interrupt9gpio_id_t"></a> <a id="bk_gpio_disable_interrupt__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga48e0eaf44663f68f2f2cea47e6476f95"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_disable\_interrupt(gpio\_id\_t id)
:   Disable GPIO intterrupt.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid GPIO channel
        - others: other errors.

<a id="_CPPv423bk_gpio_clear_interrupt9gpio_id_t"></a>

<a id="_CPPv323bk_gpio_clear_interrupt9gpio_id_t"></a> <a id="_CPPv223bk_gpio_clear_interrupt9gpio_id_t"></a> <a id="bk_gpio_clear_interrupt__gpio_id_t"></a> <a id="group__bk__api__gpio_1ga9309e183217de3b2dfadd4b3d35290cd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_clear\_interrupt(gpio\_id\_t gpio\_id)
:   Clear GPIO intterrupt.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid gpio channel
        - others: other errors.

<a id="_CPPv420bk_gpio_register_isr9gpio_id_t10gpio_isr_t"></a>

<a id="_CPPv320bk_gpio_register_isr9gpio_id_t10gpio_isr_t"></a> <a id="_CPPv220bk_gpio_register_isr9gpio_id_t10gpio_isr_t"></a> <a id="bk_gpio_register_isr__gpio_id_t.gpio_isr_t"></a> <a id="group__bk__api__gpio_1gadf2d7a2aaf11b9140e9ee78de984ed2e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_register\_isr(gpio\_id\_t id, [gpio\_isr\_t](#_CPPv410gpio_isr_t "gpio_isr_t") isr)
:   Register the interrupt service routine for GPIO channel.

    This API regist gpio isr callback function.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid gpio channel
        - others: other errors.

<a id="_CPPv422bk_gpio_unregister_isr9gpio_id_t"></a>

<a id="_CPPv322bk_gpio_unregister_isr9gpio_id_t"></a> <a id="_CPPv222bk_gpio_unregister_isr9gpio_id_t"></a> <a id="bk_gpio_unregister_isr__gpio_id_t"></a> <a id="group__bk__api__gpio_1gac5d7e52d0c90e032dfa52089f6492f01"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_unregister\_isr(gpio\_id\_t id)
:   Unregister the interrupt service routine for GPIO channel.

    This API deregist gpio isr callback function.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_GPIO\_CHAN\_ID: invalid gpio channel
        - others: other errors.

<a id="_CPPv425bk_gpio_ctrl_external_ldo8uint32_t9gpio_id_t19gpio_output_state_e"></a>

<a id="_CPPv325bk_gpio_ctrl_external_ldo8uint32_t9gpio_id_t19gpio_output_state_e"></a> <a id="_CPPv225bk_gpio_ctrl_external_ldo8uint32_t9gpio_id_t19gpio_output_state_e"></a> <a id="bk_gpio_ctrl_external_ldo__uint32_t.gpio_id_t.gpio_output_state_e"></a> <a id="group__bk__api__gpio_1gafaa386b045c177619fbc9ea4b070e019"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_ctrl\_external\_ldo(uint32\_t module, gpio\_id\_t gpio\_id, gpio\_output\_state\_e value)
:   using the gpio to control the external ldo

    control the external ldo,multi modules power on use one gpio control

    **Attention**
    :   - This API is used to use the specific gpio(define in GPIO\_CTRL\_LDO\_MAP in gpio\_map.h) control the external ldo(multi modules power on use one gpio control)

    参数
    :   **-module:module** – ID (0\~31), can use gpio\_ctrl\_ldo\_module\_e enum or custom value -gpio\_id:gpio id -value:gpio output state

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_gpio_reg_saveP8uint32_t"></a>

<a id="_CPPv316bk_gpio_reg_saveP8uint32_t"></a> <a id="_CPPv216bk_gpio_reg_saveP8uint32_t"></a> <a id="bk_gpio_reg_save__uint32_tP"></a> <a id="group__bk__api__gpio_1gab087a8620f896615b5080fc7f5186b4d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_reg\_save(uint32\_t \*gpio\_cfg)
:   Register save all gpio reg value.

    This API save all gpio reg value function.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_gpio_reg_restoreP8uint32_t"></a>

<a id="_CPPv319bk_gpio_reg_restoreP8uint32_t"></a> <a id="_CPPv219bk_gpio_reg_restoreP8uint32_t"></a> <a id="bk_gpio_reg_restore__uint32_tP"></a> <a id="group__bk__api__gpio_1gac0f85bcc46f1f17f82d56d60720723ad"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_reg\_restore(uint32\_t \*gpio\_cfg)
:   Register restore all gpio reg value.

    This API restore all gpio reg value function.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_gpio_wakeup_enable7int64_t8uint64_t8uint64_t"></a>

<a id="_CPPv321bk_gpio_wakeup_enable7int64_t8uint64_t8uint64_t"></a> <a id="_CPPv221bk_gpio_wakeup_enable7int64_t8uint64_t8uint64_t"></a> <a id="bk_gpio_wakeup_enable__int64_t.uint64_t.uint64_t"></a> <a id="group__bk__api__gpio_1ga54bf46c728d9157572b533e225daf14c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_wakeup\_enable(int64\_t index, uint64\_t type\_l, uint64\_t type\_h)
:   Register configue the gpio wakeup value.

    This API configue the gpio wakeup value function.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv430bk_gpio_wakeup_interrupt_clearv"></a>

<a id="_CPPv330bk_gpio_wakeup_interrupt_clearv"></a> <a id="_CPPv230bk_gpio_wakeup_interrupt_clearv"></a> <a id="bk_gpio_wakeup_interrupt_clear"></a> <a id="group__bk__api__gpio_1gab8fe4b39f956d0151701327998bf044a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_gpio\_wakeup\_interrupt\_clear()
:   Register clear wake up interrupt.

    This API clear wake up interrupt function.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="macros"></a>

### Macros

<a id="c.GPIO_LDO_DEFINE_APP_MODULE"></a>

<a id="group__bk__api__gpio_1gad9a233244676dde0aae40aa323fa4a5d"></a> GPIO\_LDO\_DEFINE\_APP\_MODULE(offset)
:   GPIO LDO Module ID Helper Macros.

    These macros help application layer define custom module IDs safely

    Define application module ID with offset from APP\_BASE

<a id="c.GPIO_LDO_MODULE_IS_VALID"></a>

<a id="group__bk__api__gpio_1gab892d603525c8597171637c0f1a87dd8"></a> GPIO\_LDO\_MODULE\_IS\_VALID(id)
:   Check if module ID is valid (0-31)

<a id="c.GPIO_LDO_MODULE_IS_APP_RANGE"></a>

<a id="group__bk__api__gpio_1ga4a3064eb6a8c11b227849a27052bc5ce"></a> GPIO\_LDO\_MODULE\_IS\_APP\_RANGE(id)
:   Check if module ID is in application range (10-31)

<a id="gpio-api-typedefs"></a>

## GPIO API Typedefs

<a id="id1"></a>

### Header File

- [gpio\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/gpio_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv420gpio_wakeup_config_t"></a>

<a id="_CPPv320gpio_wakeup_config_t"></a> <a id="_CPPv220gpio_wakeup_config_t"></a> <a id="gpio_wakeup_config_t"></a> <a id="structgpio__wakeup__config__t"></a> struct gpio\_wakeup\_config\_t

<a id="id2"></a>

### Macros

<a id="c.BK_ERR_GPIO_CHAN_ID"></a>

<a id="group__bk__api__gpio__defs_1gaacc3e93706a93358d601c6ec04146261"></a> BK\_ERR\_GPIO\_CHAN\_ID
:   gpio channel number is invalid

<a id="c.BK_ERR_GPIO_INVALID_MODE"></a>

<a id="group__bk__api__gpio__defs_1gace5c41582937a21a27ae0820f313e9ee"></a> BK\_ERR\_GPIO\_INVALID\_MODE
:   gpio mode is invalid

<a id="c.BK_ERR_GPIO_NOT_INPUT_MODE"></a>

<a id="group__bk__api__gpio__defs_1ga0822231d653ff3a5b33526debcfddd1f"></a> BK\_ERR\_GPIO\_NOT\_INPUT\_MODE
:   gpio is not in input mode

<a id="c.BK_ERR_GPIO_SET_INVALID_FUNC_MODE"></a>

<a id="group__bk__api__gpio__defs_1ga8b45865d53d4c8b3a3f1132ec8ce05e3"></a> BK\_ERR\_GPIO\_SET\_INVALID\_FUNC\_MODE
:   gpio perial mode is invalid or was be set as 2nd func

<a id="c.BK_ERR_GPIO_INVALID_INT_TYPE"></a>

<a id="group__bk__api__gpio__defs_1ga97a713384ad81a53908f88b78bca5b13"></a> BK\_ERR\_GPIO\_INVALID\_INT\_TYPE
:   gpio int type is invalid

<a id="c.BK_ERR_GPIOS_MAP_NONE"></a>

<a id="group__bk__api__gpio__defs_1ga10f54a8b0a842f63d6a96af9b9f67a84"></a> BK\_ERR\_GPIOS\_MAP\_NONE
:   gpio map device is none

<a id="c.BK_ERR_GPIO_NOT_OUTPUT_MODE"></a>

<a id="group__bk__api__gpio__defs_1ga04b0272d3fc9708ce8f0ee7cfabdd77b"></a> BK\_ERR\_GPIO\_NOT\_OUTPUT\_MODE
:   gpio is not in output mode

<a id="c.BK_ERR_GPIO_BITS_NUM"></a>

<a id="group__bk__api__gpio__defs_1gaf9b248434af2ff4fd9cd48255cf0e176"></a> BK\_ERR\_GPIO\_BITS\_NUM
:   gpio map bit num is error

<a id="c.BK_ERR_GPIO_INTERNAL_USED"></a>

<a id="group__bk__api__gpio__defs_1ga7988719e8641431bff42a6dfe4f31631"></a> BK\_ERR\_GPIO\_INTERNAL\_USED
:   gpio map was be map to a device

<a id="c.BK_ERR_GPIO_MAP_PWMS_CHAN"></a>

<a id="group__bk__api__gpio__defs_1gabcf06b5e850fb98924efeb471d2aa539"></a> BK\_ERR\_GPIO\_MAP\_PWMS\_CHAN
:   gpio map to pwm pwms’ channel is invalid

<a id="c.BK_ERR_GPIO_INVALID_ID"></a>

<a id="group__bk__api__gpio__defs_1ga9621ce48723cd742c2e9f43667c94d1a"></a> BK\_ERR\_GPIO\_INVALID\_ID
:   gpio id is invalid

<a id="c.BK_ERR_GPIO_WAKESOURCE_OVER_MAX_CNT"></a>

<a id="group__bk__api__gpio__defs_1gafd653a6a90fb2b5e8145cf3b6c407ecd"></a> BK\_ERR\_GPIO\_WAKESOURCE\_OVER\_MAX\_CNT
:   too much GPIO is register to wakeup source

<a id="c.BK_ERR_ANA_GPIO_TYPE_NOT_SUPPORT"></a>

<a id="group__bk__api__gpio__defs_1gaa2b6eb440b415cab586e3a2cde07f5dc"></a> BK\_ERR\_ANA\_GPIO\_TYPE\_NOT\_SUPPORT
:   analog gpio wake source pin config is invalid\>

<a id="c.BK_ERR_GPIO_INVALID_OPERATE"></a>

<a id="group__bk__api__gpio__defs_1ga2718a1ed05d8d7992bd44d2896b9eb68"></a> BK\_ERR\_GPIO\_INVALID\_OPERATE
:   gpio invalid operate,pleack check log

<a id="c.BK_ERR_GPIO_CONFIG_MISMATCH"></a>

<a id="group__bk__api__gpio__defs_1ga8f464be405952b6789ced4fb201f940b"></a> BK\_ERR\_GPIO\_CONFIG\_MISMATCH
:   gpio config is mismatch

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410gpio_isr_t"></a>

<a id="_CPPv310gpio_isr_t"></a> <a id="_CPPv210gpio_isr_t"></a> <a id="gpio_isr_t"></a> <a id="group__bk__api__gpio__defs_1ga35b08da8d5d3e07661468da1cf30eed3"></a> typedef void (\*gpio\_isr\_t)(gpio\_id\_t gpio\_id)
:   GPIO interrupt service routine.
