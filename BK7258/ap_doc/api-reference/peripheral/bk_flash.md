---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_flash.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="flash"></a>

# FLASH

<a id="flash-api-status"></a>

## FLASH API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_flash_driver_init()`](#_CPPv420bk_flash_driver_initv "bk_flash_driver_init") | Y |
| [`bk_flash_driver_deinit()`](#_CPPv422bk_flash_driver_deinitv "bk_flash_driver_deinit") | Y |
| [`bk_flash_get_line_mode()`](#_CPPv422bk_flash_get_line_modev "bk_flash_get_line_mode") | Y |
| [`bk_flash_get_id()`](#_CPPv415bk_flash_get_idv "bk_flash_get_id") | Y |
| [`bk_flash_set_clk_dpll()`](#_CPPv421bk_flash_set_clk_dpllv "bk_flash_set_clk_dpll") | Y |
| [`bk_flash_set_clk_dco()`](#_CPPv420bk_flash_set_clk_dcov "bk_flash_set_clk_dco") | Y |
| [`bk_flash_write_enable()`](#_CPPv421bk_flash_write_enablev "bk_flash_write_enable") | Y |
| [`bk_flash_write_disable()`](#_CPPv422bk_flash_write_disablev "bk_flash_write_disable") | Y |
| [`bk_flash_set_protect_type()`](#_CPPv425bk_flash_set_protect_type20flash_protect_type_t "bk_flash_set_protect_type") | Y |
| [`bk_flash_get_protect_type()`](#_CPPv425bk_flash_get_protect_typev "bk_flash_get_protect_type") | Y |
| [`bk_flash_read_status_reg()`](#_CPPv424bk_flash_read_status_regv "bk_flash_read_status_reg") | Y |
| [`bk_flash_write_status_reg()`](#_CPPv425bk_flash_write_status_reg8uint16_t "bk_flash_write_status_reg") | Y |
| [`bk_flash_erase_sector()`](#_CPPv421bk_flash_erase_sector8uint32_t "bk_flash_erase_sector") | Y |
| [`bk_flash_write_bytes()`](#_CPPv420bk_flash_write_bytes8uint32_tPK7uint8_t8uint32_t "bk_flash_write_bytes") | Y |
| [`bk_flash_read_bytes()`](#_CPPv419bk_flash_read_bytes8uint32_tP7uint8_t8uint32_t "bk_flash_read_bytes") | Y |

<a id="flash-api-reference"></a>

## FLASH API Reference

<a id="header-file"></a>

### Header File

- [flash.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/flash.h)

<a id="functions"></a>

### Functions

<a id="_CPPv420bk_flash_driver_initv"></a>

<a id="_CPPv320bk_flash_driver_initv"></a> <a id="_CPPv220bk_flash_driver_initv"></a> <a id="bk_flash_driver_init__void"></a> <a id="flash_8h_1a1aee026efd127960beb97c31e0d2d7ac"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_driver\_init(void)
:   Init the flash driver.

    This API init the resoure common:

    - Init flash driver control memory

    **Attention**
    :   1\. This API should be called before any other flash APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_flash_driver_deinitv"></a>

<a id="_CPPv322bk_flash_driver_deinitv"></a> <a id="_CPPv222bk_flash_driver_deinitv"></a> <a id="bk_flash_driver_deinit__void"></a> <a id="flash_8h_1a36f79a5c775598f15fae3f73258abdcf"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_driver\_deinit(void)
:   Deinit the flash driver.

    This API free all resource related to flash and disable flash.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv433bk_flash_get_coutinuous_read_modev"></a>

<a id="_CPPv333bk_flash_get_coutinuous_read_modev"></a> <a id="_CPPv233bk_flash_get_coutinuous_read_modev"></a> <a id="bk_flash_get_coutinuous_read_mode__void"></a> <a id="flash_8h_1aae7440ffb2d407745f9f2e1dc9625100"></a> uint8\_t bk\_flash\_get\_coutinuous\_read\_mode(void)
:   Get flash coutinuous read mode.

    返回
    :   flash coutinuous read mode

<a id="_CPPv422bk_flash_get_line_modev"></a>

<a id="_CPPv322bk_flash_get_line_modev"></a> <a id="_CPPv222bk_flash_get_line_modev"></a> <a id="bk_flash_get_line_mode__void"></a> <a id="flash_8h_1af36b099d4825ab38109265fa74aeab22"></a> [flash\_line\_mode\_t](#_CPPv417flash_line_mode_t "flash_line_mode_t") bk\_flash\_get\_line\_mode(void)
:   Get flash line mode.

    返回
    :   flash line mode

<a id="_CPPv415bk_flash_get_idv"></a>

<a id="_CPPv315bk_flash_get_idv"></a> <a id="_CPPv215bk_flash_get_idv"></a> <a id="bk_flash_get_id__void"></a> <a id="flash_8h_1a85e8336aa46d46d418cb3bbb201e2157"></a> uint32\_t bk\_flash\_get\_id(void)
:   Get flash id.

    返回
    :   flash line mode

<a id="_CPPv421bk_flash_set_clk_dpllv"></a>

<a id="_CPPv321bk_flash_set_clk_dpllv"></a> <a id="_CPPv221bk_flash_set_clk_dpllv"></a> <a id="bk_flash_set_clk_dpll__void"></a> <a id="flash_8h_1a0034b6e55c75574d09ca6117c8213692"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_set\_clk\_dpll(void)
:   Set flash clock dpll.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_flash_set_clk_dcov"></a>

<a id="_CPPv320bk_flash_set_clk_dcov"></a> <a id="_CPPv220bk_flash_set_clk_dcov"></a> <a id="bk_flash_set_clk_dco__void"></a> <a id="flash_8h_1ae9b7f7db1d4ab0a5b3883c22326571e8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_set\_clk\_dco(void)
:   Set flash clock dco.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_flash_write_enablev"></a>

<a id="_CPPv321bk_flash_write_enablev"></a> <a id="_CPPv221bk_flash_write_enablev"></a> <a id="bk_flash_write_enable__void"></a> <a id="flash_8h_1a2a99979031c02c1e281af97b7f3ef29c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_write\_enable(void)
:   Enable flash write.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_flash_write_disablev"></a>

<a id="_CPPv322bk_flash_write_disablev"></a> <a id="_CPPv222bk_flash_write_disablev"></a> <a id="bk_flash_write_disable__void"></a> <a id="flash_8h_1a361fa60c4e09b698d5d4d91a8dc9916e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_write\_disable(void)
:   Disable flash write.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_flash_set_protect_type20flash_protect_type_t"></a>

<a id="_CPPv325bk_flash_set_protect_type20flash_protect_type_t"></a> <a id="_CPPv225bk_flash_set_protect_type20flash_protect_type_t"></a> <a id="bk_flash_set_protect_type__flash_protect_type_t"></a> <a id="flash_8h_1a99bf250d2493bd1eca20a2d8ebd4b848"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_set\_protect\_type([flash\_protect\_type\_t](#_CPPv420flash_protect_type_t "flash_protect_type_t") type)
:   Set flash protect type.

    参数
    :   **type** – flash protect type

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_flash_get_protect_typev"></a>

<a id="_CPPv325bk_flash_get_protect_typev"></a> <a id="_CPPv225bk_flash_get_protect_typev"></a> <a id="bk_flash_get_protect_type__void"></a> <a id="flash_8h_1aff0b4099fd04f92768bb1ec0f21c6554"></a> [flash\_protect\_type\_t](#_CPPv420flash_protect_type_t "flash_protect_type_t") bk\_flash\_get\_protect\_type(void)
:   Get flash protect type.

    返回
    :   the flash protect type

<a id="_CPPv424bk_flash_read_status_regv"></a>

<a id="_CPPv324bk_flash_read_status_regv"></a> <a id="_CPPv224bk_flash_read_status_regv"></a> <a id="bk_flash_read_status_reg__void"></a> <a id="flash_8h_1ac6a70665bb8d992bd2c2a90b2a3bd868"></a> uint16\_t bk\_flash\_read\_status\_reg(void)
:   Get flash status register value.

    返回
    :   the flash status register value

<a id="_CPPv425bk_flash_write_status_reg8uint16_t"></a>

<a id="_CPPv325bk_flash_write_status_reg8uint16_t"></a> <a id="_CPPv225bk_flash_write_status_reg8uint16_t"></a> <a id="bk_flash_write_status_reg__uint16_t"></a> <a id="flash_8h_1a54e1b925ca26ca0ad154a77d014a4361"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_write\_status\_reg(uint16\_t status\_reg\_data)
:   Set flash status register value.

    参数
    :   **status\_reg\_data** – the flash status register data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_flash_erase_sector8uint32_t"></a>

<a id="_CPPv321bk_flash_erase_sector8uint32_t"></a> <a id="_CPPv221bk_flash_erase_sector8uint32_t"></a> <a id="bk_flash_erase_sector__uint32_t"></a> <a id="flash_8h_1ad8c0d020fa712f64a20bc300e634d0de"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_erase\_sector(uint32\_t address)
:   Erase a sector of flash, use flash command 0x20.

    参数
    :   **address** – flash address

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_FLASH\_ADDR\_OUT\_OF\_RANGE: flash address is out of range
        - others: other errors.

<a id="_CPPv420bk_flash_erase_block8uint32_t"></a>

<a id="_CPPv320bk_flash_erase_block8uint32_t"></a> <a id="_CPPv220bk_flash_erase_block8uint32_t"></a> <a id="bk_flash_erase_block__uint32_t"></a> <a id="flash_8h_1a4606a2667f7c4e2b38aa90bed1eb5911"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_erase\_block(uint32\_t address)
:   Erase a sector of flash, use flash command 0xD8.

    参数
    :   **address** – flash address

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_FLASH\_ADDR\_OUT\_OF\_RANGE: flash address is out of range
        - others: other errors.

<a id="_CPPv425bk_flash_enter_deep_sleepv"></a>

<a id="_CPPv325bk_flash_enter_deep_sleepv"></a> <a id="_CPPv225bk_flash_enter_deep_sleepv"></a> <a id="bk_flash_enter_deep_sleep__void"></a> <a id="flash_8h_1a3019d1a0a9ce6e0a6dfb7f7bd217877c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_enter\_deep\_sleep(void)
:   Entry flash deep power-down flash, use flash command 0xB9.

    返回
    :   - BK\_OK: succeed
        - BK\_FAIL: failed

<a id="_CPPv424bk_flash_exit_deep_sleepv"></a>

<a id="_CPPv324bk_flash_exit_deep_sleepv"></a> <a id="_CPPv224bk_flash_exit_deep_sleepv"></a> <a id="bk_flash_exit_deep_sleep__void"></a> <a id="flash_8h_1a799244036900300b3dd89ca8079bded7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_exit\_deep\_sleep(void)
:   Exit flash deep power-down flash, use flash command 0xAB.

    返回
    :   - BK\_OK: succeed
        - BK\_FAIL: failed

<a id="_CPPv419bk_flash_erase_fast8uint32_t8uint32_t"></a>

<a id="_CPPv319bk_flash_erase_fast8uint32_t8uint32_t"></a> <a id="_CPPv219bk_flash_erase_fast8uint32_t8uint32_t"></a> <a id="bk_flash_erase_fast__uint32_t.uint32_t"></a> <a id="flash_8h_1a2610da02a397083c23b8f960b3eeaf2f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_erase\_fast(uint32\_t erase\_off, uint32\_t len)
:   Erases a specified range of flash memory.

    This function performs flash erase operations from the specified offset for the given length. Internally, it will choose the appropriate erase granularity (4K, 32K, or 64K) based on alignment and size.

    参数
    :   - **erase\_off** – The starting offset (in bytes) within the flash.
        - **len** – The total length (in bytes) of the flash to erase.

    返回
    :   - BK\_OK on success.
        - Other error codes on failure.

<a id="_CPPv420bk_flash_write_bytes8uint32_tPK7uint8_t8uint32_t"></a>

<a id="_CPPv320bk_flash_write_bytes8uint32_tPK7uint8_t8uint32_t"></a> <a id="_CPPv220bk_flash_write_bytes8uint32_tPK7uint8_t8uint32_t"></a> <a id="bk_flash_write_bytes__uint32_t.uint8_tCP.uint32_t"></a> <a id="flash_8h_1a12dad57774cf302a6f096b08554f2d2d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_write\_bytes(uint32\_t address, const uint8\_t \*user\_buf, uint32\_t size)
:   Write data to flash.

    参数
    :   - **address** – address to write
        - **user\_buf** – the pointer to data which is to write
        - **size** – size to write

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_FLASH\_ADDR\_OUT\_OF\_RANGE: flash address is out of range
        - others: other errors.

<a id="_CPPv419bk_flash_read_bytes8uint32_tP7uint8_t8uint32_t"></a>

<a id="_CPPv319bk_flash_read_bytes8uint32_tP7uint8_t8uint32_t"></a> <a id="_CPPv219bk_flash_read_bytes8uint32_tP7uint8_t8uint32_t"></a> <a id="bk_flash_read_bytes__uint32_t.uint8_tP.uint32_t"></a> <a id="flash_8h_1a9a59ee730ee28fb485f219a9d3fe7c24"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_read\_bytes(uint32\_t address, uint8\_t \*user\_buf, uint32\_t size)
:   Read data from flash.

    参数
    :   - **address** – address to read
        - **user\_buf** – the buffer to read the data
        - **size** – size to read

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_FLASH\_ADDR\_OUT\_OF\_RANGE: flash address is out of range
        - others: other errors.

<a id="_CPPv418bk_flash_read_word8uint32_tP8uint32_t8uint32_t"></a>

<a id="_CPPv318bk_flash_read_word8uint32_tP8uint32_t8uint32_t"></a> <a id="_CPPv218bk_flash_read_word8uint32_tP8uint32_t8uint32_t"></a> <a id="bk_flash_read_word__uint32_t.uint32_tP.uint32_t"></a> <a id="flash_8h_1a3ef5ef27f5abceb8b0e276367be8a5f3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_read\_word(uint32\_t address, uint32\_t \*user\_buf, uint32\_t size)
:   Read data from flas.

    参数
    :   - **address** – address to read
        - **user\_buf** – the buffer to read the data, intend to psram addr must aline by 4 Bytes
        - **size** – size to read, length uint by byte

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_FLASH\_ADDR\_OUT\_OF\_RANGE: flash address is out of range
        - others: other errors.

<a id="_CPPv425bk_flash_is_driver_initedv"></a>

<a id="_CPPv325bk_flash_is_driver_initedv"></a> <a id="_CPPv225bk_flash_is_driver_initedv"></a> <a id="bk_flash_is_driver_inited__void"></a> <a id="flash_8h_1a43aecdd3ad017041bff0a019316e18c6"></a> bool bk\_flash\_is\_driver\_inited(void)
:   Get flash init flag.

    返回
    :   the flash init flag

<a id="_CPPv431bk_flash_get_current_total_sizev"></a>

<a id="_CPPv331bk_flash_get_current_total_sizev"></a> <a id="_CPPv231bk_flash_get_current_total_sizev"></a> <a id="bk_flash_get_current_total_size__void"></a> <a id="flash_8h_1a46025696cf09a1a4bfa32a0f2d74934f"></a> uint32\_t bk\_flash\_get\_current\_total\_size(void)
:   Get flash total size.

    返回
    :   the flash total size

<a id="_CPPv437bk_flash_register_ps_suspend_callback19flash_ps_callback_t"></a>

<a id="_CPPv337bk_flash_register_ps_suspend_callback19flash_ps_callback_t"></a> <a id="_CPPv237bk_flash_register_ps_suspend_callback19flash_ps_callback_t"></a> <a id="bk_flash_register_ps_suspend_callback__flash_ps_callback_t"></a> <a id="flash_8h_1a6d438d8607fc964fb92a29cd46fbded3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_register\_ps\_suspend\_callback([flash\_ps\_callback\_t](#_CPPv419flash_ps_callback_t "flash_ps_callback_t") ps\_suspend\_cb)
:   Register flash power save suspend callback.

    参数
    :   **ps\_suspend\_cb** – power save suspend callback

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv436bk_flash_register_ps_resume_callback19flash_ps_callback_t"></a>

<a id="_CPPv336bk_flash_register_ps_resume_callback19flash_ps_callback_t"></a> <a id="_CPPv236bk_flash_register_ps_resume_callback19flash_ps_callback_t"></a> <a id="bk_flash_register_ps_resume_callback__flash_ps_callback_t"></a> <a id="flash_8h_1a0ae871bb89b81d1c3f811a06f5e56bc2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_register\_ps\_resume\_callback([flash\_ps\_callback\_t](#_CPPv419flash_ps_callback_t "flash_ps_callback_t") ps\_resume\_cb)
:   Register flash power save resume callback.

    参数
    :   **ps\_resume\_cb** – power save resume callback

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_flash_clk_switch8uint32_t8uint32_t"></a>

<a id="_CPPv319bk_flash_clk_switch8uint32_t8uint32_t"></a> <a id="_CPPv219bk_flash_clk_switch8uint32_t8uint32_t"></a> <a id="bk_flash_clk_switch__uint32_t.uint32_t"></a> <a id="flash_8h_1a5e1db73a1af0c2684e802698ccaedb3a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_clk\_switch(uint32\_t flash\_speed\_type, uint32\_t modules)
:   Modify flash speed type.

    参数
    :   - **flash\_speed\_type** – the high/low type of flash clock
        - **modules** – the app module to control the flash spped

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_flash_register_wait_cb21flash_wait_callback_t"></a>

<a id="_CPPv325bk_flash_register_wait_cb21flash_wait_callback_t"></a> <a id="_CPPv225bk_flash_register_wait_cb21flash_wait_callback_t"></a> <a id="bk_flash_register_wait_cb__flash_wait_callback_t"></a> <a id="flash_8h_1a0226b26923ed262274e49b68eb747615"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_register\_wait\_cb([flash\_wait\_callback\_t](#_CPPv421flash_wait_callback_t "flash_wait_callback_t") wait\_cb)
:   register a callback to be called when flash is busy waiting. WARNING/NOTES:

    1. the wait\_cb code is better in ITCM to avoid running in flash. or the wait\_cb will be blocked until flash is idle. 2.The wait\_cb will be called forever until flash is idle, so the implemetion of wait\_cb should garante the programm is safe.

    BK\_OK: succeed

    - others: registered too many(\>4) wait\_cb to flash.

    参数
    :   **wait\_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this wait\_cb to flash. When flash is writing/erasing, it will call this wait\_cb

    返回

<a id="_CPPv427bk_flash_unregister_wait_cb21flash_wait_callback_t"></a>

<a id="_CPPv327bk_flash_unregister_wait_cb21flash_wait_callback_t"></a> <a id="_CPPv227bk_flash_unregister_wait_cb21flash_wait_callback_t"></a> <a id="bk_flash_unregister_wait_cb__flash_wait_callback_t"></a> <a id="flash_8h_1a1509c2f2d99b0916cc1af093805114cd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_unregister\_wait\_cb([flash\_wait\_callback\_t](#_CPPv421flash_wait_callback_t "flash_wait_callback_t") wait\_cb)
:   unregister the wait\_cb from flash waiting.

    参数
    :   **wait\_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this wait\_cb to flash. When flash is writing/erasing, it will call this wait\_cb

    返回
    :   - BK\_OK: succeed
        - others: The wait\_cb isn’t registered to flash.

<a id="_CPPv427bk_flash_set_operate_status17flash_op_status_t"></a>

<a id="_CPPv327bk_flash_set_operate_status17flash_op_status_t"></a> <a id="_CPPv227bk_flash_set_operate_status17flash_op_status_t"></a> <a id="bk_flash_set_operate_status__flash_op_status_t"></a> <a id="flash_8h_1a20179ba4f633334461160cf79c4804d1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_set\_operate\_status([flash\_op\_status\_t](#_CPPv417flash_op_status_t "flash_op_status_t") status)
:   Set flash operate status.

    参数
    :   **flash** – operate status

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_flash_get_operate_statusv"></a>

<a id="_CPPv327bk_flash_get_operate_statusv"></a> <a id="_CPPv227bk_flash_get_operate_statusv"></a> <a id="bk_flash_get_operate_status__void"></a> <a id="flash_8h_1a18ce35416a3c47a30383cc149e6486aa"></a> [flash\_op\_status\_t](#_CPPv417flash_op_status_t "flash_op_status_t") bk\_flash\_get\_operate\_status(void)
:   Get flash operate status.

    返回
    :   flash operate status

<a id="_CPPv427mb_flash_register_op_notifyPv"></a>

<a id="_CPPv327mb_flash_register_op_notifyPv"></a> <a id="_CPPv227mb_flash_register_op_notifyPv"></a> <a id="mb_flash_register_op_notify__voidP"></a> <a id="flash_8h_1abc20dbdd03617f85aad0c5928d5ed2ba"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb\_flash\_register\_op\_notify(void \*notify\_cb)
:   register a callback to be called when flash is busy waiting.

    参数
    :   **wait\_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this wait\_cb to flash. When flash is writing/erasing, it will call this wait\_cb

    返回
    :   - BK\_OK: succeed
        - others: registered too many(\>4) wait\_cb to flash.

<a id="_CPPv429mb_flash_unregister_op_notifyPv"></a>

<a id="_CPPv329mb_flash_unregister_op_notifyPv"></a> <a id="_CPPv229mb_flash_unregister_op_notifyPv"></a> <a id="mb_flash_unregister_op_notify__voidP"></a> <a id="flash_8h_1a50d19ce22db68f47b6c252a0b9147527"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb\_flash\_unregister\_op\_notify(void \*notify\_cb)
:   unregister the wait\_cb from flash waiting.

    参数
    :   **wait\_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this wait\_cb to flash. When flash is writing/erasing, it will call this wait\_cb

    返回
    :   - BK\_OK: succeed
        - others: The wait\_cb isn’t registered to flash.

<a id="_CPPv424is_ble_erase_flash_readyv"></a>

<a id="_CPPv324is_ble_erase_flash_readyv"></a> <a id="_CPPv224is_ble_erase_flash_readyv"></a> <a id="is_ble_erase_flash_ready__void"></a> <a id="flash_8h_1aa1ed08f3f7070b21bc472905d8973e64"></a> bool is\_ble\_erase\_flash\_ready(void)
:   Get status if it is ready to erase flash, which means ble would sleep more than 56ms period.

    返回
    :   flash ready status

<a id="_CPPv424is_ble_write_flash_readyv"></a>

<a id="_CPPv324is_ble_write_flash_readyv"></a> <a id="_CPPv224is_ble_write_flash_readyv"></a> <a id="is_ble_write_flash_ready__void"></a> <a id="flash_8h_1a6a3223a2680eda86fa928cc1f6c6057d"></a> bool is\_ble\_write\_flash\_ready(void)
:   Get status if it is ready to write flash, which means ble would sleep more than 4ms period.

    返回
    :   flash ready status

<a id="_CPPv412ble_sleep_cb7uint8_t8uint32_t"></a>

<a id="_CPPv312ble_sleep_cb7uint8_t8uint32_t"></a> <a id="_CPPv212ble_sleep_cb7uint8_t8uint32_t"></a> <a id="ble_sleep_cb__uint8_t.uint32_t"></a> <a id="flash_8h_1a59012cf12d1801ac09364d15cd8dacae"></a> void ble\_sleep\_cb(uint8\_t is\_sleeping, uint32\_t slp\_period)
:   Callbak to register in flash, for ble operate flash using.

    返回

<a id="_CPPv425ble_callback_deal_handler8uint32_t"></a>

<a id="_CPPv325ble_callback_deal_handler8uint32_t"></a> <a id="_CPPv225ble_callback_deal_handler8uint32_t"></a> <a id="ble_callback_deal_handler__uint32_t"></a> <a id="flash_8h_1a30de4e7e38065a578e8cbe69660d947b"></a> int ble\_callback\_deal\_handler(uint32\_t deal\_flash\_time)
:   Get status if it is ready to operate flash, which means ble would sleep more than deal\_flash\_time ms period.

    返回
    :   flash ready status

<a id="_CPPv432mb_flash_register_op_uart_notifyPv"></a>

<a id="_CPPv332mb_flash_register_op_uart_notifyPv"></a> <a id="_CPPv232mb_flash_register_op_uart_notifyPv"></a> <a id="mb_flash_register_op_uart_notify__voidP"></a> <a id="flash_8h_1aeec5e2060299c2cc01f00cbb9cf9d629"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb\_flash\_register\_op\_uart\_notify(void \*notify\_cb)
:   register a callback to be called when flash is busy waiting.

    参数
    :   - **notify\_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this notify\_cb to flash. When flash is writing/erasing, it will call this notify\_cb
        - **args** – the arguments to pass to notify\_cb

    返回
    :   - BK\_OK: succeed
        - others: registered too many(\>4) notify\_cb to flash.

<a id="_CPPv434mb_flash_unregister_op_uart_notifyv"></a>

<a id="_CPPv334mb_flash_unregister_op_uart_notifyv"></a> <a id="_CPPv234mb_flash_unregister_op_uart_notifyv"></a> <a id="mb_flash_unregister_op_uart_notify__void"></a> <a id="flash_8h_1a4ee2331c6a7bae96b8d5efe052b61567"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb\_flash\_unregister\_op\_uart\_notify(void)
:   unregister the notify\_cb from flash waiting.

    返回
    :   - BK\_OK: succeed
        - others: The notify\_cb isn’t registered to flash.

<a id="_CPPv434mb_flash_register_op_camera_notifyPv"></a>

<a id="_CPPv334mb_flash_register_op_camera_notifyPv"></a> <a id="_CPPv234mb_flash_register_op_camera_notifyPv"></a> <a id="mb_flash_register_op_camera_notify__voidP"></a> <a id="flash_8h_1ac181eef50b26d8b42e7307816a0023b9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb\_flash\_register\_op\_camera\_notify(void \*notify\_cb)
:   register a callback to be called when flash is busy waiting.

    参数
    :   **wait\_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this wait\_cb to flash. When flash is writing/erasing, it will call this wait\_cb

    返回
    :   - BK\_OK: succeed
        - others: registered too many(\>4) wait\_cb to flash.

<a id="_CPPv436mb_flash_unregister_op_camera_notifyv"></a>

<a id="_CPPv336mb_flash_unregister_op_camera_notifyv"></a> <a id="_CPPv236mb_flash_unregister_op_camera_notifyv"></a> <a id="mb_flash_unregister_op_camera_notify__void"></a> <a id="flash_8h_1a94e718fdb701ab02ca04c30260923c2e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb\_flash\_unregister\_op\_camera\_notify(void)
:   unregister the wait\_cb from flash waiting.

    返回
    :   - BK\_OK: succeed
        - others: The wait\_cb isn’t registered to flash.

<a id="_CPPv448mb_flash_unregister_op_onboard_mic_stream_notifyv"></a>

<a id="_CPPv348mb_flash_unregister_op_onboard_mic_stream_notifyv"></a> <a id="_CPPv248mb_flash_unregister_op_onboard_mic_stream_notifyv"></a> <a id="mb_flash_unregister_op_onboard_mic_stream_notify__void"></a> <a id="flash_8h_1a342dabe5c1201e56c01a3b545d061c5e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb\_flash\_unregister\_op\_onboard\_mic\_stream\_notify(void)
:   unregister the wait\_cb from flash waiting.

    返回
    :   - BK\_OK: succeed
        - others: The wait\_cb isn’t registered to flash.

<a id="_CPPv446mb_flash_register_op_onboard_mic_stream_notifyPvPv"></a>

<a id="_CPPv346mb_flash_register_op_onboard_mic_stream_notifyPvPv"></a> <a id="_CPPv246mb_flash_register_op_onboard_mic_stream_notifyPvPv"></a> <a id="mb_flash_register_op_onboard_mic_stream_notify__voidP.voidP"></a> <a id="flash_8h_1a019490f447d45e18ebecf7ff8674aba0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") mb\_flash\_register\_op\_onboard\_mic\_stream\_notify(void \*notify\_cb, void \*args)
:   register a callback to be called when flash is busy waiting.

    参数
    :   - **notify\_cb:If** – flash is writing/erasing, it will block all of other applications. But maybe the application can’t be blocked when flash is writing/erasing. So the application should register this notify\_cb to flash. When flash is writing/erasing, it will call this notify\_cb
        - **args** – the arguments to pass to notify\_cb

    返回
    :   - BK\_OK: succeed
        - others: registered too many(\>4) notify\_cb to flash.

<a id="_CPPv423flash_get_excute_enablev"></a>

<a id="_CPPv323flash_get_excute_enablev"></a> <a id="_CPPv223flash_get_excute_enablev"></a> <a id="flash_get_excute_enable"></a> <a id="flash_8h_1a68ce5adef0cc4ce79967c2677368b718"></a> uint32\_t flash\_get\_excute\_enable()

<a id="_CPPv427bk_flash_power_saving_enterv"></a>

<a id="_CPPv327bk_flash_power_saving_enterv"></a> <a id="_CPPv227bk_flash_power_saving_enterv"></a> <a id="bk_flash_power_saving_enter__void"></a> <a id="flash_8h_1a4c872642c80b1fd44f2219e260b75231"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_power\_saving\_enter(void)
:   Set flash 2 line mode.

    参数
    :   **line\_mode** – flash 2 line mode

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_flash_power_saving_exitv"></a>

<a id="_CPPv326bk_flash_power_saving_exitv"></a> <a id="_CPPv226bk_flash_power_saving_exitv"></a> <a id="bk_flash_power_saving_exit__void"></a> <a id="flash_8h_1a16ae605a3f1f8c263ab9aa228706decd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_power\_saving\_exit(void)
:   Set flash 4 line mode.

    参数
    :   **line\_mode** – flash 4 line mode

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="macros"></a>

### Macros

<a id="c.S_WAKE_UP"></a>

<a id="flash_8h_1a175df1e0a79d0131ae66b3529b5f378a"></a> S\_WAKE\_UP

<a id="c.S_SLEEP"></a>

<a id="flash_8h_1ac7fd0e09423970426d6897f634c367e9"></a> S\_SLEEP

<a id="c.S_POWER_OFF"></a>

<a id="flash_8h_1ab0ea4cb5f77c801c64c87422baa8c9a7"></a> S\_POWER\_OFF

<a id="c.S_NO_BT"></a>

<a id="flash_8h_1aa9f6fb8bfe41e1eec7d617e89e0adbde"></a> S\_NO\_BT

<a id="c.ERASE_TOUCH_TIMEOUT"></a>

<a id="flash_8h_1a2b938a5483fee679d7eab36143a0ac87"></a> ERASE\_TOUCH\_TIMEOUT

<a id="c.ERASE_FLASH_TIMEOUT"></a>

<a id="flash_8h_1aed5dec73595c47dbdc8e2eecd116bb18"></a> ERASE\_FLASH\_TIMEOUT

<a id="c.WRITE_FLASH_TIMEOUT"></a>

<a id="flash_8h_1a85d7ee2678b37367de7022b0521fc3d3"></a> WRITE\_FLASH\_TIMEOUT

<a id="flash-api-typedefs"></a>

## FLASH API Typedefs

<a id="id1"></a>

### Header File

- [flash\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/flash_types.h)

<a id="id2"></a>

### Macros

<a id="c.BK_ERR_FLASH_NOT_INIT"></a>

<a id="flash__types_8h_1aef98eeedd537e6238bcde408332231b3"></a> BK\_ERR\_FLASH\_NOT\_INIT
:   FLASH driver not init

<a id="c.BK_ERR_FLASH_ADDR_OUT_OF_RANGE"></a>

<a id="flash__types_8h_1a204ac459b8f381583052f37f4c3e5b73"></a> BK\_ERR\_FLASH\_ADDR\_OUT\_OF\_RANGE
:   FLASH address is out of range

<a id="c.BK_ERR_FLASH_PARTITION_NOT_FOUND"></a>

<a id="flash__types_8h_1a4bebc953f1991fd6cb2c8bd7d174a72e"></a> BK\_ERR\_FLASH\_PARTITION\_NOT\_FOUND
:   FLASH partition not found

<a id="c.BK_ERR_FLASH_WAIT_CB_FULL"></a>

<a id="flash__types_8h_1ae1ee501bcd60b2d92546696adf4773f8"></a> BK\_ERR\_FLASH\_WAIT\_CB\_FULL
:   FLASH wait cb is registered too much

<a id="c.BK_ERR_FLASH_WAIT_CB_NOT_REGISTER"></a>

<a id="flash__types_8h_1a4bc730f10cbff493132b204b88947c4d"></a> BK\_ERR\_FLASH\_WAIT\_CB\_NOT\_REGISTER
:   FLASH wait cb is not registered but tried to unregister

<a id="c.FLASH_ATE_BIT"></a>

<a id="flash__types_8h_1ac33942eaa3d7a2cd5535b49f5506ecbf"></a> FLASH\_ATE\_BIT

<a id="c.FLASH_MAC_BIT"></a>

<a id="flash__types_8h_1a6d6fd30d1626df0afdbd9a2619788097"></a> FLASH\_MAC\_BIT

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv419flash_ps_callback_t"></a>

<a id="_CPPv319flash_ps_callback_t"></a> <a id="_CPPv219flash_ps_callback_t"></a> <a id="flash_ps_callback_t"></a> <a id="flash__types_8h_1af0fd7256e2cd078319684f590b567f5b"></a> typedef void (\*flash\_ps\_callback\_t)(void)

<a id="_CPPv421flash_wait_callback_t"></a>

<a id="_CPPv321flash_wait_callback_t"></a> <a id="_CPPv221flash_wait_callback_t"></a> <a id="flash_wait_callback_t"></a> <a id="flash__types_8h_1a8b863be5c57e4405493af6909b79740e"></a> typedef void (\*flash\_wait\_callback\_t)(void)

<a id="_CPPv445flash_op_notify_onboard_mic_stream_callback_t"></a>

<a id="_CPPv345flash_op_notify_onboard_mic_stream_callback_t"></a> <a id="_CPPv245flash_op_notify_onboard_mic_stream_callback_t"></a> <a id="flash_op_notify_onboard_mic_stream_callback_t"></a> <a id="flash__types_8h_1ab525598f76865dffe5e368547c4325e7"></a> typedef void (\*flash\_op\_notify\_onboard\_mic\_stream\_callback\_t)(uint32\_t param, void \*args)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv417flash_line_mode_t"></a>

<a id="_CPPv317flash_line_mode_t"></a> <a id="_CPPv217flash_line_mode_t"></a> <a id="flash__types_8h_1afd6268ef88485c1c7d1782f9af7e4b64"></a> enum flash\_line\_mode\_t
:   *Values:*

    <a id="_CPPv4N17flash_line_mode_t19FLASH_LINE_MODE_TWOE"></a>

    <a id="_CPPv3N17flash_line_mode_t19FLASH_LINE_MODE_TWOE"></a> <a id="_CPPv2N17flash_line_mode_t19FLASH_LINE_MODE_TWOE"></a> <a id="flash__types_8h_1afd6268ef88485c1c7d1782f9af7e4b64a2172b07e1fa6ca313f7929928c5d1d84"></a> enumerator FLASH\_LINE\_MODE\_TWO
    :   flash line mode 2

    <a id="_CPPv4N17flash_line_mode_t20FLASH_LINE_MODE_FOURE"></a>

    <a id="_CPPv3N17flash_line_mode_t20FLASH_LINE_MODE_FOURE"></a> <a id="_CPPv2N17flash_line_mode_t20FLASH_LINE_MODE_FOURE"></a> <a id="flash__types_8h_1afd6268ef88485c1c7d1782f9af7e4b64aaef368f2924e8a98e792ab656a1f3a5a"></a> enumerator FLASH\_LINE\_MODE\_FOUR
    :   flash line mode 4

<a id="_CPPv420flash_protect_type_t"></a>

<a id="_CPPv320flash_protect_type_t"></a> <a id="_CPPv220flash_protect_type_t"></a> <a id="flash__types_8h_1a400761a5e96975823cd332c6c934389b"></a> enum flash\_protect\_type\_t
:   *Values:*

    <a id="_CPPv4N20flash_protect_type_t18FLASH_PROTECT_NONEE"></a>

    <a id="_CPPv3N20flash_protect_type_t18FLASH_PROTECT_NONEE"></a> <a id="_CPPv2N20flash_protect_type_t18FLASH_PROTECT_NONEE"></a> <a id="flash__types_8h_1a400761a5e96975823cd332c6c934389ba584c2a91bee487a04c2bb99f6256180f"></a> enumerator FLASH\_PROTECT\_NONE
    :   flash protect type none

    <a id="_CPPv4N20flash_protect_type_t17FLASH_PROTECT_ALLE"></a>

    <a id="_CPPv3N20flash_protect_type_t17FLASH_PROTECT_ALLE"></a> <a id="_CPPv2N20flash_protect_type_t17FLASH_PROTECT_ALLE"></a> <a id="flash__types_8h_1a400761a5e96975823cd332c6c934389ba4f43dd00016845ef86a626739516f018"></a> enumerator FLASH\_PROTECT\_ALL
    :   flash protect type all

    <a id="_CPPv4N20flash_protect_type_t18FLASH_PROTECT_HALFE"></a>

    <a id="_CPPv3N20flash_protect_type_t18FLASH_PROTECT_HALFE"></a> <a id="_CPPv2N20flash_protect_type_t18FLASH_PROTECT_HALFE"></a> <a id="flash__types_8h_1a400761a5e96975823cd332c6c934389ba1d26529b9ee94f2144be518eb291b9e8"></a> enumerator FLASH\_PROTECT\_HALF
    :   flash protect type half

    <a id="_CPPv4N20flash_protect_type_t26FLASH_UNPROTECT_LAST_BLOCKE"></a>

    <a id="_CPPv3N20flash_protect_type_t26FLASH_UNPROTECT_LAST_BLOCKE"></a> <a id="_CPPv2N20flash_protect_type_t26FLASH_UNPROTECT_LAST_BLOCKE"></a> <a id="flash__types_8h_1a400761a5e96975823cd332c6c934389bad6038b6e4619b93993292f48b53c7812"></a> enumerator FLASH\_UNPROTECT\_LAST\_BLOCK
    :   flash protect type unprotect last block

<a id="_CPPv418flash_speed_type_t"></a>

<a id="_CPPv318flash_speed_type_t"></a> <a id="_CPPv218flash_speed_type_t"></a> <a id="flash__types_8h_1a989f7cb1194a321ca8f6cdffcde97c4b"></a> enum flash\_speed\_type\_t
:   *Values:*

    <a id="_CPPv4N18flash_speed_type_t16FLASH_SPEED_HIGHE"></a>

    <a id="_CPPv3N18flash_speed_type_t16FLASH_SPEED_HIGHE"></a> <a id="_CPPv2N18flash_speed_type_t16FLASH_SPEED_HIGHE"></a> <a id="flash__types_8h_1a989f7cb1194a321ca8f6cdffcde97c4ba341466f97c2fe87f6cf2ccb1b3d318f0"></a> enumerator FLASH\_SPEED\_HIGH

    <a id="_CPPv4N18flash_speed_type_t15FLASH_SPEED_LOWE"></a>

    <a id="_CPPv3N18flash_speed_type_t15FLASH_SPEED_LOWE"></a> <a id="_CPPv2N18flash_speed_type_t15FLASH_SPEED_LOWE"></a> <a id="flash__types_8h_1a989f7cb1194a321ca8f6cdffcde97c4bab871ec9a6c9ad8dd8c2954732f9344dd"></a> enumerator FLASH\_SPEED\_LOW

<a id="_CPPv419flash_ctrl_module_t"></a>

<a id="_CPPv319flash_ctrl_module_t"></a> <a id="_CPPv219flash_ctrl_module_t"></a> <a id="flash__types_8h_1a747e90731ab75d9cca268f6435f1285f"></a> enum flash\_ctrl\_module\_t
:   *Values:*

    <a id="_CPPv4N19flash_ctrl_module_t9FLASH_ATEE"></a>

    <a id="_CPPv3N19flash_ctrl_module_t9FLASH_ATEE"></a> <a id="_CPPv2N19flash_ctrl_module_t9FLASH_ATEE"></a> <a id="flash__types_8h_1a747e90731ab75d9cca268f6435f1285fa0c477a42e8604c290a028891ea785127"></a> enumerator FLASH\_ATE

    <a id="_CPPv4N19flash_ctrl_module_t9FLASH_MACE"></a>

    <a id="_CPPv3N19flash_ctrl_module_t9FLASH_MACE"></a> <a id="_CPPv2N19flash_ctrl_module_t9FLASH_MACE"></a> <a id="flash__types_8h_1a747e90731ab75d9cca268f6435f1285fa7457fbabac858f344db81f767bbb6859"></a> enumerator FLASH\_MAC

<a id="_CPPv417flash_op_status_t"></a>

<a id="_CPPv317flash_op_status_t"></a> <a id="_CPPv217flash_op_status_t"></a> <a id="flash__types_8h_1ad4ea084c1fef8e67ff0c8dec9206a2ae"></a> enum flash\_op\_status\_t
:   *Values:*

    <a id="_CPPv4N17flash_op_status_t13FLASH_OP_IDLEE"></a>

    <a id="_CPPv3N17flash_op_status_t13FLASH_OP_IDLEE"></a> <a id="_CPPv2N17flash_op_status_t13FLASH_OP_IDLEE"></a> <a id="flash__types_8h_1ad4ea084c1fef8e67ff0c8dec9206a2aea80f12ad482878040b1db1386e352c667"></a> enumerator FLASH\_OP\_IDLE

    <a id="_CPPv4N17flash_op_status_t13FLASH_OP_BUSYE"></a>

    <a id="_CPPv3N17flash_op_status_t13FLASH_OP_BUSYE"></a> <a id="_CPPv2N17flash_op_status_t13FLASH_OP_BUSYE"></a> <a id="flash__types_8h_1ad4ea084c1fef8e67ff0c8dec9206a2aea50af764961c89ceb34281b8e28dbabcc"></a> enumerator FLASH\_OP\_BUSY

<a id="id3"></a>

### Header File

- [hal\_flash\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_flash_types.h)

<a id="id4"></a>

### Type Definitions

<a id="_CPPv412flash_unit_t"></a>

<a id="_CPPv312flash_unit_t"></a> <a id="_CPPv212flash_unit_t"></a> <a id="flash_unit_t"></a> <a id="hal__flash__types_8h_1a02c64bf50abdd382678d2f436a95884d"></a> typedef uint8\_t flash\_unit\_t
:   flash uint id

<a id="id5"></a>

### Enumerations

<a id="_CPPv414flash_op_cmd_t"></a>

<a id="_CPPv314flash_op_cmd_t"></a> <a id="_CPPv214flash_op_cmd_t"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8"></a> enum flash\_op\_cmd\_t
:   *Values:*

    <a id="_CPPv4N14flash_op_cmd_t17FLASH_OP_CMD_WRENE"></a>

    <a id="_CPPv3N14flash_op_cmd_t17FLASH_OP_CMD_WRENE"></a> <a id="_CPPv2N14flash_op_cmd_t17FLASH_OP_CMD_WRENE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a1f9a9db5376a66e4064c8bb23a763776"></a> enumerator FLASH\_OP\_CMD\_WREN
    :   flash command write enable

    <a id="_CPPv4N14flash_op_cmd_t17FLASH_OP_CMD_WRDIE"></a>

    <a id="_CPPv3N14flash_op_cmd_t17FLASH_OP_CMD_WRDIE"></a> <a id="_CPPv2N14flash_op_cmd_t17FLASH_OP_CMD_WRDIE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8ab847d0bad92d8780f51450d118a3909a"></a> enumerator FLASH\_OP\_CMD\_WRDI
    :   flash command write disable

    <a id="_CPPv4N14flash_op_cmd_t17FLASH_OP_CMD_RDSRE"></a>

    <a id="_CPPv3N14flash_op_cmd_t17FLASH_OP_CMD_RDSRE"></a> <a id="_CPPv2N14flash_op_cmd_t17FLASH_OP_CMD_RDSRE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8ab5f8fc869ccd1824d021b6cac4fda862"></a> enumerator FLASH\_OP\_CMD\_RDSR
    :   flash command read status register

    <a id="_CPPv4N14flash_op_cmd_t17FLASH_OP_CMD_WRSRE"></a>

    <a id="_CPPv3N14flash_op_cmd_t17FLASH_OP_CMD_WRSRE"></a> <a id="_CPPv2N14flash_op_cmd_t17FLASH_OP_CMD_WRSRE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8ad1c8166f08eaba6f7596b3d8e570c68d"></a> enumerator FLASH\_OP\_CMD\_WRSR
    :   flash command write status register

    <a id="_CPPv4N14flash_op_cmd_t17FLASH_OP_CMD_READE"></a>

    <a id="_CPPv3N14flash_op_cmd_t17FLASH_OP_CMD_READE"></a> <a id="_CPPv2N14flash_op_cmd_t17FLASH_OP_CMD_READE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a5ea6d7dd2d6dede8b730a8c83fcd94ae"></a> enumerator FLASH\_OP\_CMD\_READ
    :   flash command read data

    <a id="_CPPv4N14flash_op_cmd_t18FLASH_OP_CMD_RDSR2E"></a>

    <a id="_CPPv3N14flash_op_cmd_t18FLASH_OP_CMD_RDSR2E"></a> <a id="_CPPv2N14flash_op_cmd_t18FLASH_OP_CMD_RDSR2E"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8aeb2a051bf8ab12926caaaff911972ed6"></a> enumerator FLASH\_OP\_CMD\_RDSR2
    :   flash command read status register-2

    <a id="_CPPv4N14flash_op_cmd_t18FLASH_OP_CMD_WRSR2E"></a>

    <a id="_CPPv3N14flash_op_cmd_t18FLASH_OP_CMD_WRSR2E"></a> <a id="_CPPv2N14flash_op_cmd_t18FLASH_OP_CMD_WRSR2E"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a4fb27f5b95b052132d76d94ce0a7d4b9"></a> enumerator FLASH\_OP\_CMD\_WRSR2
    :   flash command write status register-2

    <a id="_CPPv4N14flash_op_cmd_t15FLASH_OP_CMD_PPE"></a>

    <a id="_CPPv3N14flash_op_cmd_t15FLASH_OP_CMD_PPE"></a> <a id="_CPPv2N14flash_op_cmd_t15FLASH_OP_CMD_PPE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a22b07c4c0d4cc7da5199a44788974468"></a> enumerator FLASH\_OP\_CMD\_PP
    :   flash command page program

    <a id="_CPPv4N14flash_op_cmd_t15FLASH_OP_CMD_SEE"></a>

    <a id="_CPPv3N14flash_op_cmd_t15FLASH_OP_CMD_SEE"></a> <a id="_CPPv2N14flash_op_cmd_t15FLASH_OP_CMD_SEE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8ae3f333f93669689988b313010868e7fc"></a> enumerator FLASH\_OP\_CMD\_SE
    :   flash command sector erase

    <a id="_CPPv4N14flash_op_cmd_t16FLASH_OP_CMD_BE1E"></a>

    <a id="_CPPv3N14flash_op_cmd_t16FLASH_OP_CMD_BE1E"></a> <a id="_CPPv2N14flash_op_cmd_t16FLASH_OP_CMD_BE1E"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a959e9fbb57d305756134f8a70bee8c2e"></a> enumerator FLASH\_OP\_CMD\_BE1
    :   flash command block erase-1

    <a id="_CPPv4N14flash_op_cmd_t16FLASH_OP_CMD_BE2E"></a>

    <a id="_CPPv3N14flash_op_cmd_t16FLASH_OP_CMD_BE2E"></a> <a id="_CPPv2N14flash_op_cmd_t16FLASH_OP_CMD_BE2E"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a9f450e176f3ad2f4e09d05e0ab2465d9"></a> enumerator FLASH\_OP\_CMD\_BE2
    :   flash command block erase-2

    <a id="_CPPv4N14flash_op_cmd_t15FLASH_OP_CMD_CEE"></a>

    <a id="_CPPv3N14flash_op_cmd_t15FLASH_OP_CMD_CEE"></a> <a id="_CPPv2N14flash_op_cmd_t15FLASH_OP_CMD_CEE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a03476861341e93b5125afbe185d2ca47"></a> enumerator FLASH\_OP\_CMD\_CE
    :   flash command chip erase

    <a id="_CPPv4N14flash_op_cmd_t15FLASH_OP_CMD_DPE"></a>

    <a id="_CPPv3N14flash_op_cmd_t15FLASH_OP_CMD_DPE"></a> <a id="_CPPv2N14flash_op_cmd_t15FLASH_OP_CMD_DPE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a0cd718b000cadd5f926abec2b6452c82"></a> enumerator FLASH\_OP\_CMD\_DP

    <a id="_CPPv4N14flash_op_cmd_t17FLASH_OP_CMD_RFDPE"></a>

    <a id="_CPPv3N14flash_op_cmd_t17FLASH_OP_CMD_RFDPE"></a> <a id="_CPPv2N14flash_op_cmd_t17FLASH_OP_CMD_RFDPE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a0a82edf43db2f2777fef749e045c8ae3"></a> enumerator FLASH\_OP\_CMD\_RFDP

    <a id="_CPPv4N14flash_op_cmd_t17FLASH_OP_CMD_RDIDE"></a>

    <a id="_CPPv3N14flash_op_cmd_t17FLASH_OP_CMD_RDIDE"></a> <a id="_CPPv2N14flash_op_cmd_t17FLASH_OP_CMD_RDIDE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a3da66f4224405de66a9ce115b79cb589"></a> enumerator FLASH\_OP\_CMD\_RDID
    :   flash command read device id

    <a id="_CPPv4N14flash_op_cmd_t16FLASH_OP_CMD_HPME"></a>

    <a id="_CPPv3N14flash_op_cmd_t16FLASH_OP_CMD_HPME"></a> <a id="_CPPv2N14flash_op_cmd_t16FLASH_OP_CMD_HPME"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8ae9cbfe6ac77ea25a816b92ec40bb0584"></a> enumerator FLASH\_OP\_CMD\_HPM
    :   flash command high performance mode

    <a id="_CPPv4N14flash_op_cmd_t17FLASH_OP_CMD_CRMRE"></a>

    <a id="_CPPv3N14flash_op_cmd_t17FLASH_OP_CMD_CRMRE"></a> <a id="_CPPv2N14flash_op_cmd_t17FLASH_OP_CMD_CRMRE"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8afe62d81794d12873bdcea36e04883ff4"></a> enumerator FLASH\_OP\_CMD\_CRMR

    <a id="_CPPv4N14flash_op_cmd_t18FLASH_OP_CMD_CRMR2E"></a>

    <a id="_CPPv3N14flash_op_cmd_t18FLASH_OP_CMD_CRMR2E"></a> <a id="_CPPv2N14flash_op_cmd_t18FLASH_OP_CMD_CRMR2E"></a> <a id="hal__flash__types_8h_1ac324721ad3196c180c680194909d97e8a9f4d8256884938858b367a4cf1a09275"></a> enumerator FLASH\_OP\_CMD\_CRMR2

<a id="_CPPv412flash_mode_t"></a>

<a id="_CPPv312flash_mode_t"></a> <a id="_CPPv212flash_mode_t"></a> <a id="hal__flash__types_8h_1a419af4191aaa0567950f7ed7a6ab84bf"></a> enum flash\_mode\_t
:   *Values:*

    <a id="_CPPv4N12flash_mode_t19FLASH_MODE_STANDARDE"></a>

    <a id="_CPPv3N12flash_mode_t19FLASH_MODE_STANDARDE"></a> <a id="_CPPv2N12flash_mode_t19FLASH_MODE_STANDARDE"></a> <a id="hal__flash__types_8h_1a419af4191aaa0567950f7ed7a6ab84bfa65877e8480fb72766030f3ee0bb49e2e"></a> enumerator FLASH\_MODE\_STANDARD
    :   flash standard mode

    <a id="_CPPv4N12flash_mode_t15FLASH_MODE_DUALE"></a>

    <a id="_CPPv3N12flash_mode_t15FLASH_MODE_DUALE"></a> <a id="_CPPv2N12flash_mode_t15FLASH_MODE_DUALE"></a> <a id="hal__flash__types_8h_1a419af4191aaa0567950f7ed7a6ab84bfadbd0cc0ca8192ac4953e387dd427f79b"></a> enumerator FLASH\_MODE\_DUAL
    :   flash dual mode

    <a id="_CPPv4N12flash_mode_t15FLASH_MODE_QUADE"></a>

    <a id="_CPPv3N12flash_mode_t15FLASH_MODE_QUADE"></a> <a id="_CPPv2N12flash_mode_t15FLASH_MODE_QUADE"></a> <a id="hal__flash__types_8h_1a419af4191aaa0567950f7ed7a6ab84bfaf2705c8111f390f51e0b26c3af5af698"></a> enumerator FLASH\_MODE\_QUAD
    :   flash quad mode
