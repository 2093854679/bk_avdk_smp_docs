# FLASH


BK7259 CP 侧 Flash API（`include/driver/flash.h`）。详细说明见
[FLASH 开发指南](../../developer-guide/peripheral/bk_flash.md "../../developer-guide/peripheral/bk_flash.md")。


## FLASH API Reference


### Header File


- [flash.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/flash.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/flash.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_driver_init(void)
:   Init the flash driver.

    This API init the resoure common:


    - Init flash driver control memory


    **Attention**
    :   1. This API should be called before any other flash APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_driver_deinit(void)
:   Deinit the flash driver.

    This API free all resource related to flash and disable flash.

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint8_t bk_flash_get_coutinuous_read_mode(void)
:   Get flash coutinuous read mode.

    返回
    :   flash coutinuous read mode

[flash_line_mode_t](#_CPPv417flash_line_mode_t "flash_line_mode_t") bk_flash_get_line_mode(void)
:   Get flash line mode.

    返回
    :   flash line mode

uint32_t bk_flash_get_id(void)
:   Get flash id.

    返回
    :   flash line mode

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_set_clk_dpll(void)
:   Set flash clock dpll.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_set_clk_dco(void)
:   Set flash clock dco.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_write_enable(void)
:   Enable flash write.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_write_disable(void)
:   Disable flash write.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_set_protect_type([flash_protect_type_t](#_CPPv420flash_protect_type_t "flash_protect_type_t") type)
:   Set flash protect type.

    参数
    :   **type** – flash protect type

    返回
    :   - BK_OK: succeed

        - others: other errors.

[flash_protect_type_t](#_CPPv420flash_protect_type_t "flash_protect_type_t") bk_flash_get_protect_type(void)
:   Get flash protect type.

    返回
    :   the flash protect type

uint16_t bk_flash_read_status_reg(void)
:   Get flash status register value.

    返回
    :   the flash status register value

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_write_status_reg(uint16_t status_reg_data)
:   Set flash status register value.

    参数
    :   **status_reg_data** – the flash status register data

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_erase_sector(uint32_t address)
:   Erase a sector of flash, use flash command 0x20.

    参数
    :   **address** – flash address

    返回
    :   - BK_OK: succeed

        - BK_ERR_FLASH_ADDR_OUT_OF_RANGE: flash address is out of range

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_erase_block(uint32_t address)
:   Erase a sector of flash, use flash command 0xD8.

    参数
    :   **address** – flash address

    返回
    :   - BK_OK: succeed

        - BK_ERR_FLASH_ADDR_OUT_OF_RANGE: flash address is out of range

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_enter_deep_sleep(void)
:   Entry flash deep power-down flash, use flash command 0xB9.

    返回
    :   - BK_OK: succeed

        - BK_FAIL: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_exit_deep_sleep(void)
:   Exit flash deep power-down flash, use flash command 0xAB.

    返回
    :   - BK_OK: succeed

        - BK_FAIL: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_erase_fast(uint32_t erase_off, uint32_t len)
:   Erases a specified range of flash memory.

    This function performs flash erase operations from the specified offset for the given length. Internally, it will choose the appropriate erase granularity (4K, 32K, or 64K) based on alignment and size.

    参数
    :   - **erase_off** – The starting offset (in bytes) within the flash.

        - **len** – The total length (in bytes) of the flash to erase.

    返回
    :   - BK_OK on success.

        - Other error codes on failure.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_write_bytes(uint32_t address, const uint8_t *user_buf, uint32_t size)
:   Write data to flash.

    参数
    :   - **address** – address to write

        - **user_buf** – the pointer to data which is to write

        - **size** – size to write

    返回
    :   - BK_OK: succeed

        - BK_ERR_FLASH_ADDR_OUT_OF_RANGE: flash address is out of range

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_read_bytes(uint32_t address, uint8_t *user_buf, uint32_t size)
:   Read data from flash.

    参数
    :   - **address** – address to read

        - **user_buf** – the buffer to read the data

        - **size** – size to read

    返回
    :   - BK_OK: succeed

        - BK_ERR_FLASH_ADDR_OUT_OF_RANGE: flash address is out of range

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_read_word(uint32_t address, uint32_t *user_buf, uint32_t size)
:   Read data from flas.

    参数
    :   - **address** – address to read

        - **user_buf** – the buffer to read the data, intend to psram addr must aline by 4 Bytes

        - **size** – size to read, length uint by byte

    返回
    :   - BK_OK: succeed

        - BK_ERR_FLASH_ADDR_OUT_OF_RANGE: flash address is out of range

        - others: other errors.

bool bk_flash_is_driver_inited(void)
:   Get flash init flag.

    返回
    :   the flash init flag

uint32_t bk_flash_get_current_total_size(void)
:   Get flash total size.

    返回
    :   the flash total size

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_register_ps_suspend_callback([flash_ps_callback_t](#_CPPv419flash_ps_callback_t "flash_ps_callback_t") ps_suspend_cb)
:   Register flash power save suspend callback.

    参数
    :   **ps_suspend_cb** – power save suspend callback

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_register_ps_resume_callback([flash_ps_callback_t](#_CPPv419flash_ps_callback_t "flash_ps_callback_t") ps_resume_cb)
:   Register flash power save resume callback.

    参数
    :   **ps_resume_cb** – power save resume callback

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_clk_switch(flash_clk_src_t clk_src, flash_clk_div_t clk_div)
:   Modify flash speed type.

    参数
    :   - **flash_speed_type** – the high/low type of flash clock

        - **modules** – the app module to control the flash spped

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_register_wait_cb([flash_wait_callback_t](#_CPPv421flash_wait_callback_t "flash_wait_callback_t") wait_cb)
:   register a callback to be called when flash is busy waiting. WARNING/NOTES:

    1. the wait_cb code is better in ITCM to avoid running in flash. or the wait_cb will be blocked until flash is idle. 2.The wait_cb will be called forever until flash is idle, so the implemetion of wait_cb should garante the programm is safe.

    BK_OK: succeed


    - others: registered too many(>4) wait_cb to flash.

    参数
    :   **wait_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this wait_cb to flash. When flash is writing/erasing, it will call this wait_cb

    返回

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_unregister_wait_cb([flash_wait_callback_t](#_CPPv421flash_wait_callback_t "flash_wait_callback_t") wait_cb)
:   unregister the wait_cb from flash waiting.

    参数
    :   **wait_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this wait_cb to flash. When flash is writing/erasing, it will call this wait_cb

    返回
    :   - BK_OK: succeed

        - others: The wait_cb isn’t registered to flash.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_set_operate_status([flash_op_status_t](#_CPPv417flash_op_status_t "flash_op_status_t") status)
:   Set flash operate status.

    参数
    :   **flash** – operate status

    返回
    :   - BK_OK: succeed

        - others: other errors.

[flash_op_status_t](#_CPPv417flash_op_status_t "flash_op_status_t") bk_flash_get_operate_status(void)
:   Get flash operate status.

    返回
    :   flash operate status

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb_flash_register_op_notify(void *notify_cb)
:   register a callback to be called when flash is busy waiting.

    参数
    :   **wait_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this wait_cb to flash. When flash is writing/erasing, it will call this wait_cb

    返回
    :   - BK_OK: succeed

        - others: registered too many(>4) wait_cb to flash.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb_flash_unregister_op_notify(void *notify_cb)
:   unregister the wait_cb from flash waiting.

    参数
    :   **wait_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this wait_cb to flash. When flash is writing/erasing, it will call this wait_cb

    返回
    :   - BK_OK: succeed

        - others: The wait_cb isn’t registered to flash.

bool is_ble_erase_flash_ready(void)
:   Get status if it is ready to erase flash, which means ble would sleep more than 56ms period.

    返回
    :   flash ready status

bool is_ble_write_flash_ready(void)
:   Get status if it is ready to write flash, which means ble would sleep more than 4ms period.

    返回
    :   flash ready status

void ble_sleep_cb(uint8_t is_sleeping, uint32_t slp_period)
:   Callbak to register in flash, for ble operate flash using.

    返回

int ble_callback_deal_handler(uint32_t deal_flash_time)
:   Get status if it is ready to operate flash, which means ble would sleep more than deal_flash_time ms period.

    返回
    :   flash ready status

uint32_t flash_get_excute_enable()

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_power_saving_enter(void)
:   Set flash 2 line mode.

    参数
    :   **line_mode** – flash 2 line mode

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_power_saving_exit(void)
:   Set flash 4 line mode.

    参数
    :   **line_mode** – flash 2 line mode

    返回
    :   - BK_OK: succeed

        - others: other errors.


### Macros

S_WAKE_UP

S_SLEEP

S_POWER_OFF

S_NO_BT

ERASE_TOUCH_TIMEOUT

ERASE_FLASH_TIMEOUT

WRITE_FLASH_TIMEOUT


## FLASH API Typedefs


### Header File


- [flash_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/flash_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/flash_types.h")


### Macros

BK_ERR_FLASH_NOT_INIT
:   FLASH driver not init

BK_ERR_FLASH_ADDR_OUT_OF_RANGE
:   FLASH address is out of range

BK_ERR_FLASH_PARTITION_NOT_FOUND
:   FLASH partition not found

BK_ERR_FLASH_WAIT_CB_FULL
:   FLASH wait cb is registered too much

BK_ERR_FLASH_WAIT_CB_NOT_REGISTER
:   FLASH wait cb is not registered but tried to unregister

FLASH_ATE_BIT

FLASH_MAC_BIT


### Type Definitions

typedef void (*flash_ps_callback_t)(void)

typedef void (*flash_wait_callback_t)(void)


### Enumerations

enum flash_line_mode_t
:   *Values:*

    enumerator FLASH_LINE_MODE_TWO
    :   flash line mode 2

    enumerator FLASH_LINE_MODE_FOUR
    :   flash line mode 4

enum flash_protect_type_t
:   *Values:*

    enumerator FLASH_PROTECT_NONE
    :   flash protect type none

    enumerator FLASH_PROTECT_ALL
    :   flash protect type all

    enumerator FLASH_PROTECT_HALF
    :   flash protect type half

    enumerator FLASH_UNPROTECT_LAST_BLOCK
    :   flash protect type unprotect last block

enum flash_speed_type_t
:   *Values:*

    enumerator FLASH_SPEED_HIGH

    enumerator FLASH_SPEED_LOW

enum flash_ctrl_module_t
:   *Values:*

    enumerator FLASH_ATE

    enumerator FLASH_MAC

enum flash_op_status_t
:   *Values:*

    enumerator FLASH_OP_IDLE

    enumerator FLASH_OP_BUSY


### Header File


- [hal/hal_flash_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_flash_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_flash_types.h")


### Type Definitions

typedef uint8_t flash_unit_t
:   flash uint id


### Enumerations

enum flash_op_cmd_t
:   *Values:*

    enumerator FLASH_OP_CMD_WREN
    :   flash command write enable

    enumerator FLASH_OP_CMD_WRDI
    :   flash command write disable

    enumerator FLASH_OP_CMD_RDSR
    :   flash command read status register

    enumerator FLASH_OP_CMD_WRSR
    :   flash command write status register

    enumerator FLASH_OP_CMD_READ
    :   flash command read data

    enumerator FLASH_OP_CMD_RDSR2
    :   flash command read status register-2

    enumerator FLASH_OP_CMD_WRSR2
    :   flash command write status register-2

    enumerator FLASH_OP_CMD_PP
    :   flash command page program

    enumerator FLASH_OP_CMD_SE
    :   flash command sector erase

    enumerator FLASH_OP_CMD_BE1
    :   flash command block erase-1

    enumerator FLASH_OP_CMD_BE2
    :   flash command block erase-2

    enumerator FLASH_OP_CMD_CE
    :   flash command chip erase

    enumerator FLASH_OP_CMD_DP

    enumerator FLASH_OP_CMD_RFDP

    enumerator FLASH_OP_CMD_RDID
    :   flash command read device id

    enumerator FLASH_OP_CMD_HPM
    :   flash command high performance mode

    enumerator FLASH_OP_CMD_CRMR

    enumerator FLASH_OP_CMD_CRMR2

enum flash_mode_t
:   *Values:*

    enumerator FLASH_MODE_STANDARD
    :   flash standard mode

    enumerator FLASH_MODE_DUAL
    :   flash dual mode

    enumerator FLASH_MODE_QUAD
    :   flash quad mode
