# GPIO



## GPIO API Status

| API | BK7259 |
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


## GPIO API Reference


### Header File


- [gpio.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/gpio.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/gpio.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_driver_init(void)
:   Init the GPIO driver.

    This API init the resoure common to all GPIO channels:


    - Init GPIO driver control memory

    This API should be called before any other GPIO APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_driver_deinit(void)
:   Deinit the GPIO driver.

    This API free all resource related to GPIO and power down all GPIO channels.

    返回
    :   - BK_OK: succeed

        - others: other errors.

void bk_gpio_set_value(gpio_id_t id, uint32_t v)
:   Direct set GPIO config value.

    @NOTES Please be care to use this API,unless you know the detail mean, because it will set the GPIO config value. Sometimes the special GPIO needs to re-used by one more owner, after the second owner re-used it, it should restore the config value. Before re-use a GPIO, the owner can call bk_gpio_get_value and bakup it, after re-used finish, it call bk_gpio_set_value to restore the prevous value.

uint32_t bk_gpio_get_value(gpio_id_t id)
:   get GPIO config value.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_enable_output(gpio_id_t gpio_id)
:   enable GPIO output mode

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_disable_output(gpio_id_t gpio_id)
:   disable GPIO output mode

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_enable_input(gpio_id_t gpio_id)
:   enable GPIO input mode

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_disable_input(gpio_id_t gpio_id)
:   disable GPIO input mode

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_enable_pull(gpio_id_t gpio_id)
:   enable GPIO pull mode

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_disable_pull(gpio_id_t gpio_id)
:   disable gpio pull mode

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_pull_up(gpio_id_t gpio_id)
:   set GPIO as pull up mode

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_pull_down(gpio_id_t gpio_id)
:   set GPIO as pull down mode

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_set_config(gpio_id_t gpio_id, const gpio_config_t *config)
:   Config the GPIO mode.

    This API config GPIO’s mode


    - BK_OK: succeed

    - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

    - BK_ERR_GPIO_INVALID_MODE: invalid GPIO’s io_mode/pull_mode

    - BK_ERR_GPIO_INTERNAL_USED:GPIO was map to another device

    - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_set_output_high(gpio_id_t gpio_id)
:   Set the GPIO output high,.

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - BK_ERR_GPIO_NOT_OUTPUT_MODE:GPIO not in output mode

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_set_output_low(gpio_id_t gpio_id)
:   Set the GPIO output low,.

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - BK_ERR_GPIO_NOT_OUTPUT_MODE:GPIO not in output mode

        - others: other errors.

bool bk_gpio_get_input(gpio_id_t gpio_id)
:   Get the GPIO input value,.

    This API get GPIO’s input level: 0 :low_level 1:high_level.

    返回
    :   - input value

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - BK_ERR_GPIO_NOT_INPUT_MODE : GPIO is not input mode

        - others: other errors.

bool bk_gpio_set_capacity(gpio_id_t gpio_id, uint32 capacity)
:   Set the GPIO driver capacity.

    This API Set GPIO’s output driver capacity which range is 0~3.

    返回
    :   - input value

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - BK_ERR_GPIO_NOT_INPUT_MODE : GPIO is not input mode

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_set_interrupt_type(gpio_id_t gpio_id, gpio_int_type_t type)
:   Config the GPIO intterrupt type mode when use gpio intterrupt mode,.

    This API config all GPIO channels’ intterrupt mode, the mode included in gpio_int_type_t.

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - BK_ERR_GPIO_INVALID_INT_TYPE: invalid GPIO int type

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_enable_interrupt(gpio_id_t id)
:   Enable GPIO intterrupt.

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - BK_ERR_GPIO_NOT_INPUT_MODE : GPIO is not input mode

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_disable_interrupt(gpio_id_t id)
:   Disable GPIO intterrupt.

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid GPIO channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_clear_interrupt(gpio_id_t gpio_id)
:   Clear GPIO intterrupt.

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid gpio channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_register_isr(gpio_id_t id, [gpio_isr_t](#_CPPv410gpio_isr_t "gpio_isr_t") isr)
:   Register the interrupt service routine for GPIO channel.

    This API regist gpio isr callback function.

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid gpio channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_unregister_isr(gpio_id_t id)
:   Unregister the interrupt service routine for GPIO channel.

    This API deregist gpio isr callback function.

    返回
    :   - BK_OK: succeed

        - BK_ERR_GPIO_CHAN_ID: invalid gpio channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_reg_save(uint32_t *gpio_cfg)
:   Register save all gpio reg value.

    This API save all gpio reg value function.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_reg_restore(uint32_t *gpio_cfg)
:   Register restore all gpio reg value.

    This API restore all gpio reg value function.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_wakeup_enable(int64_t index, uint64_t type_l, uint64_t type_h)
:   Register configue the gpio wakeup value.

    This API configue the gpio wakeup value function.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_wakeup_interrupt_clear()
:   Register clear wake up interrupt.

    This API clear wake up interrupt function.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_gpio_ctrl_external_ldo(uint32_t module, gpio_id_t gpio_id, gpio_output_state_e value)
:   using the gpio to control the external ldo

    control the external ldo,multi modules power on use one gpio control


    **Attention**
    :   - This API is used to use the specific gpio(define in GPIO_CTRL_LDO_MAP in gpio_map.h) control the external ldo(multi modules power on use one gpio control)

    参数
    :   **-module:module** – ID (0~31), can use gpio_ctrl_ldo_module_e enum or custom value -gpio_id:gpio id -value:gpio output state

    返回
    :   - BK_OK: succeed

        - others: other errors.


### Macros

GPIO_LDO_DEFINE_APP_MODULE(offset)
:   GPIO LDO Module ID Helper Macros.

    These macros help application layer define custom module IDs safely

    Define application module ID with offset from APP_BASE

GPIO_LDO_MODULE_IS_VALID(id)
:   Check if module ID is valid (0-31)

GPIO_LDO_MODULE_IS_APP_RANGE(id)
:   Check if module ID is in application range (10-31)


## GPIO API Typedefs


### Header File


- [gpio_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/gpio_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/gpio_types.h")


### Structures

struct gpio_wakeup_config_t


### Macros

BK_ERR_GPIO_CHAN_ID
:   gpio channel number is invalid

BK_ERR_GPIO_INVALID_MODE
:   gpio mode is invalid

BK_ERR_GPIO_NOT_INPUT_MODE
:   gpio is not in input mode

BK_ERR_GPIO_SET_INVALID_FUNC_MODE
:   gpio perial mode is invalid or was be set as 2nd func

BK_ERR_GPIO_INVALID_INT_TYPE
:   gpio int type is invalid

BK_ERR_GPIOS_MAP_NONE
:   gpio map device is none

BK_ERR_GPIO_NOT_OUTPUT_MODE
:   gpio is not in output mode

BK_ERR_GPIO_BITS_NUM
:   gpio map bit num is error

BK_ERR_GPIO_INTERNAL_USED
:   gpio map was be map to a device

BK_ERR_GPIO_MAP_PWMS_CHAN
:   gpio map to pwm pwms’ channel is invalid

BK_ERR_GPIO_INVALID_ID
:   gpio id is invalid

BK_ERR_GPIO_WAKESOURCE_OVER_MAX_CNT
:   too much GPIO is register to wakeup source

BK_ERR_ANA_GPIO_TYPE_NOT_SUPPORT
:   analog gpio wake source pin config is invalid>

BK_ERR_GPIO_INVALID_OPERATE
:   gpio invalid operate,pleack check log

BK_ERR_GPIO_CONFIG_MISMATCH
:   gpio config is mismatch


### Type Definitions

typedef void (*gpio_isr_t)(gpio_id_t gpio_id)
:   GPIO interrupt service routine.
