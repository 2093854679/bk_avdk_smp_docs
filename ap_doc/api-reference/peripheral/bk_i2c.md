---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_i2c.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="i2c"></a>

# I2C

<a id="i2c-api-status"></a>

## I2C API Status

| API | BK7259\_AP |
| --- | --- |
| [`bk_i2c_driver_init()`](#_CPPv418bk_i2c_driver_initv "bk_i2c_driver_init") | Y |
| [`bk_i2c_driver_deinit()`](#_CPPv420bk_i2c_driver_deinitv "bk_i2c_driver_deinit") | Y |
| [`bk_i2c_init()`](#_CPPv411bk_i2c_init8i2c_id_tPK12i2c_config_t "bk_i2c_init") | Y |
| [`bk_i2c_deinit()`](#_CPPv413bk_i2c_deinit8i2c_id_t "bk_i2c_deinit") | Y |
| [`bk_i2c_master_write()`](#_CPPv419bk_i2c_master_write8i2c_id_t8uint32_tPK7uint8_t8uint32_t8uint32_t "bk_i2c_master_write") | Y |
| [`bk_i2c_master_read()`](#_CPPv418bk_i2c_master_read8i2c_id_t8uint32_tP7uint8_t8uint32_t8uint32_t "bk_i2c_master_read") | Y |
| [`bk_i2c_slave_write()`](#_CPPv418bk_i2c_slave_write8i2c_id_tPK7uint8_t8uint32_t8uint32_t "bk_i2c_slave_write") | Y |
| [`bk_i2c_slave_read()`](#_CPPv417bk_i2c_slave_read8i2c_id_tP7uint8_t8uint32_t8uint32_t "bk_i2c_slave_read") | Y |
| [`bk_i2c_memory_write()`](#_CPPv419bk_i2c_memory_write8i2c_id_tPK15i2c_mem_param_t "bk_i2c_memory_write") | Y |
| [`bk_i2c_memory_read()`](#_CPPv418bk_i2c_memory_read8i2c_id_tPK15i2c_mem_param_t "bk_i2c_memory_read") | Y |

<a id="i2c-unit-number"></a>

## I2C UNIT Number

| Capability | BK7259\_AP | BK7259\_CP |
| --- | --- | --- |
| UNIT Number | 2 | 2 |

<a id="i2c-pin-and-gpio-map"></a>

## I2C Pin and GPIO Map

| I2C Pin | BK7259\_AP | BK7259\_CP |
| --- | --- | --- |
| I2C0 SCL | 20 | 20 |
| I2C0 SDA | 21 | 21 |
| I2C1 SCL | 42 | 42 |
| I2C1 SDA | 43 | 43 |
| I2C1 SCL | 0 | 0 |
| I2C1 SDA | 1 | 1 |

<a id="i2c-api-reference"></a>

## I2C API Reference

<a id="header-file"></a>

### Header File

- [i2c.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/i2c.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_i2c_driver_initv"></a>

<a id="_CPPv318bk_i2c_driver_initv"></a> <a id="_CPPv218bk_i2c_driver_initv"></a> <a id="bk_i2c_driver_init__void"></a> <a id="i2c_8h_1a7a66021ef6c20b8b70ee659e491bed93"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_driver\_init(void)
:   Init the I2C driver.

    This API init the resoure common:

    - Init I2C driver control memory

    **Attention**
    :   1\. This API should be called before any other I2C APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_i2c_driver_deinitv"></a>

<a id="_CPPv320bk_i2c_driver_deinitv"></a> <a id="_CPPv220bk_i2c_driver_deinitv"></a> <a id="bk_i2c_driver_deinit__void"></a> <a id="i2c_8h_1ac216878ee86d85f1d366afd269274976"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_driver\_deinit(void)
:   Deinit the I2C driver.

    This API free all resource related to I2C and disable I2C.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_i2c_init8i2c_id_tPK12i2c_config_t"></a>

<a id="_CPPv311bk_i2c_init8i2c_id_tPK12i2c_config_t"></a> <a id="_CPPv211bk_i2c_init8i2c_id_tPK12i2c_config_t"></a> <a id="bk_i2c_init__i2c_id_t.i2c_config_tCP"></a> <a id="i2c_8h_1a184ca212e6e602b164349469c4cbc506"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_init([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, const [i2c\_config\_t](#_CPPv412i2c_config_t "i2c_config_t") \*cfg)
:   Init the I2C id.

    This API init the I2C id:

    - Power up the I2C id
    - Configure the I2C id clock
    - Map the I2C id to dedicated GPIO port
    - Set the I2C parameters
    - Start the I2C id

    **Attention**
    :   Multifunction GPIO initialization affects other functions

    参数
    :   - **id** – I2C id
        - **config** – I2C parameter settings

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: I2C config paramter is NULL
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - others: other errors.

<a id="_CPPv413bk_i2c_deinit8i2c_id_t"></a>

<a id="_CPPv313bk_i2c_deinit8i2c_id_t"></a> <a id="_CPPv213bk_i2c_deinit8i2c_id_t"></a> <a id="bk_i2c_deinit__i2c_id_t"></a> <a id="i2c_8h_1a02c72d467407aab151ef26f839ce23b8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_deinit([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Deinit the I2C id.

    This API deinit the I2C id:

    - Stop the I2C id
    - Disable the I2C id interrupt
    - Power down the I2C id

    参数
    :   **id** – I2C id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_i2c_master_write8i2c_id_t8uint32_tPK7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv319bk_i2c_master_write8i2c_id_t8uint32_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv219bk_i2c_master_write8i2c_id_t8uint32_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="bk_i2c_master_write__i2c_id_t.uint32_t.uint8_tCP.uint32_t.uint32_t"></a> <a id="i2c_8h_1a2c200ace339b65368d5816b420de025b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_master\_write([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint32\_t dev\_addr, const uint8\_t \*data, uint32\_t size, uint32\_t timeout\_ms)
:   Write data to the I2C port from a given buffer and length, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id
        - **dev\_addr** – slave device address
        - **data** – pointer to the buffer
        - **size** – data length to write
        - **timeout\_ms** – timeout ms

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - BK\_ERR\_I2C\_INVALID\_ID: I2C id number is invalid
        - BK\_ERR\_I2C\_ID\_NOT\_INIT: I2C id not init
        - others: other errors.

<a id="_CPPv426bk_i2c_master_write_noaddr8i2c_id_tPK7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv326bk_i2c_master_write_noaddr8i2c_id_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv226bk_i2c_master_write_noaddr8i2c_id_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="bk_i2c_master_write_noaddr__i2c_id_t.uint8_tCP.uint32_t.uint32_t"></a> <a id="i2c_8h_1a6a4cbb4478adeb5bfe8bfd872a3b56d7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_master\_write\_noaddr([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, const uint8\_t \*data, uint32\_t size, uint32\_t timeout\_ms)
:   Write data to the I2C port from a given buffer and length without slave address, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id
        - **data** – pointer to the buffer
        - **size** – data length to write
        - **timeout\_ms** – timeout ms

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - BK\_ERR\_I2C\_INVALID\_ID: I2C id number is invalid
        - BK\_ERR\_I2C\_ID\_NOT\_INIT: I2C id not init
        - others: other errors.

<a id="_CPPv418bk_i2c_master_read8i2c_id_t8uint32_tP7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv318bk_i2c_master_read8i2c_id_t8uint32_tP7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv218bk_i2c_master_read8i2c_id_t8uint32_tP7uint8_t8uint32_t8uint32_t"></a> <a id="bk_i2c_master_read__i2c_id_t.uint32_t.uint8_tP.uint32_t.uint32_t"></a> <a id="i2c_8h_1a494ef80524cb8299959369b68e527988"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_master\_read([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint32\_t dev\_addr, uint8\_t \*data, uint32\_t size, uint32\_t timeout\_ms)
:   I2C read data from I2C buffer, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id
        - **dev\_addr** – slave device address
        - **data** – pointer to the buffer
        - **size** – data length to read
        - **timeout\_ms** – timeout ms

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - BK\_ERR\_I2C\_INVALID\_ID: I2C id number is invalid
        - BK\_ERR\_I2C\_ID\_NOT\_INIT: I2C id not init
        - others: other errors.

<a id="_CPPv425bk_i2c_master_read_noaddr8i2c_id_tP7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv325bk_i2c_master_read_noaddr8i2c_id_tP7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv225bk_i2c_master_read_noaddr8i2c_id_tP7uint8_t8uint32_t8uint32_t"></a> <a id="bk_i2c_master_read_noaddr__i2c_id_t.uint8_tP.uint32_t.uint32_t"></a> <a id="i2c_8h_1a87123c2f1c44975f9fa7b15a96658576"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_master\_read\_noaddr([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint8\_t \*data, uint32\_t size, uint32\_t timeout\_ms)
:   I2C read data from I2C buffer without slave address, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id
        - **data** – pointer to the buffer
        - **size** – data length to read
        - **timeout\_ms** – timeout ms

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - BK\_ERR\_I2C\_INVALID\_ID: I2C id number is invalid
        - BK\_ERR\_I2C\_ID\_NOT\_INIT: I2C id not init
        - others: other errors.

<a id="_CPPv418bk_i2c_slave_write8i2c_id_tPK7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv318bk_i2c_slave_write8i2c_id_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv218bk_i2c_slave_write8i2c_id_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="bk_i2c_slave_write__i2c_id_t.uint8_tCP.uint32_t.uint32_t"></a> <a id="i2c_8h_1ad6b0bd4713f6a57d6a0bd763cef475aa"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_slave\_write([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, const uint8\_t \*data, uint32\_t size, uint32\_t timeout\_ms)
:   Write data to the I2C port from a given buffer and length, It shall only be called in I2C slave mode.

    参数
    :   - **id** – I2C id
        - **data** – pointer to the buffer
        - **size** – data length to write
        - **timeout\_ms** – timeout ms

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - BK\_ERR\_I2C\_INVALID\_ID: I2C id number is invalid
        - BK\_ERR\_I2C\_ID\_NOT\_INIT: I2C id not init
        - others: other errors.

<a id="_CPPv417bk_i2c_slave_read8i2c_id_tP7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv317bk_i2c_slave_read8i2c_id_tP7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv217bk_i2c_slave_read8i2c_id_tP7uint8_t8uint32_t8uint32_t"></a> <a id="bk_i2c_slave_read__i2c_id_t.uint8_tP.uint32_t.uint32_t"></a> <a id="i2c_8h_1ad10549f4dce8d3f25fa7b33dfcf65602"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_slave\_read([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint8\_t \*data, uint32\_t size, uint32\_t timeout\_ms)
:   I2C read data from I2C buffer, It shall only be called in I2C slave mode.

    参数
    :   - **id** – I2C id
        - **dev\_addr** – slave device address
        - **data** – pointer to the buffer
        - **size** – data length to read
        - **timeout\_ms** – timeout ms

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - BK\_ERR\_I2C\_INVALID\_ID: I2C id number is invalid
        - BK\_ERR\_I2C\_ID\_NOT\_INIT: I2C id not init
        - others: other errors.

<a id="_CPPv419bk_i2c_memory_write8i2c_id_tPK15i2c_mem_param_t"></a>

<a id="_CPPv319bk_i2c_memory_write8i2c_id_tPK15i2c_mem_param_t"></a> <a id="_CPPv219bk_i2c_memory_write8i2c_id_tPK15i2c_mem_param_t"></a> <a id="bk_i2c_memory_write__i2c_id_t.i2c_mem_param_tCP"></a> <a id="i2c_8h_1af89f2793d0b32fc051cad0a4fa080b6e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_memory\_write([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, const [i2c\_mem\_param\_t](#_CPPv415i2c_mem_param_t "i2c_mem_param_t") \*mem\_param)
:   Write data to the specific memory address from a given buffer and length, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id
        - **mem\_param** – memory parameter

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: I2C mem\_param is NULL
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - BK\_ERR\_I2C\_INVALID\_ID: I2C id number is invalid
        - BK\_ERR\_I2C\_ID\_NOT\_INIT: I2C id not init
        - others: other errors.

<a id="_CPPv418bk_i2c_memory_read8i2c_id_tPK15i2c_mem_param_t"></a>

<a id="_CPPv318bk_i2c_memory_read8i2c_id_tPK15i2c_mem_param_t"></a> <a id="_CPPv218bk_i2c_memory_read8i2c_id_tPK15i2c_mem_param_t"></a> <a id="bk_i2c_memory_read__i2c_id_t.i2c_mem_param_tCP"></a> <a id="i2c_8h_1a11116a62d1d2a019bb9aab2a1c373860"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_memory\_read([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, const [i2c\_mem\_param\_t](#_CPPv415i2c_mem_param_t "i2c_mem_param_t") \*mem\_param)
:   I2C read data from I2C specific memory address, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id
        - **mem\_param** – memory parameter

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: I2C mem\_param is NULL
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - BK\_ERR\_I2C\_INVALID\_ID: I2C id number is invalid
        - BK\_ERR\_I2C\_ID\_NOT\_INIT: I2C id not init
        - others: other errors.

<a id="_CPPv420bk_i2c_set_baud_rate8i2c_id_t8uint32_t"></a>

<a id="_CPPv320bk_i2c_set_baud_rate8i2c_id_t8uint32_t"></a> <a id="_CPPv220bk_i2c_set_baud_rate8i2c_id_t8uint32_t"></a> <a id="bk_i2c_set_baud_rate__i2c_id_t.uint32_t"></a> <a id="i2c_8h_1a3255bcfc4c8c84c102eca9affcc55a89"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_set\_baud\_rate([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint32\_t baud\_rate)
:   I2C set baud rate.

    参数
    :   - **id** – I2C id
        - **baud\_rate** – baud rate

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - BK\_ERR\_I2C\_INVALID\_ID: I2C id number is invalid
        - BK\_ERR\_I2C\_ID\_NOT\_INIT: I2C id not init
        - others: other errors.

<a id="_CPPv424bk_i2c_set_slave_address8i2c_id_t8uint16_t"></a>

<a id="_CPPv324bk_i2c_set_slave_address8i2c_id_t8uint16_t"></a> <a id="_CPPv224bk_i2c_set_slave_address8i2c_id_t8uint16_t"></a> <a id="bk_i2c_set_slave_address__i2c_id_t.uint16_t"></a> <a id="i2c_8h_1a9403c85084322227737de7257a206e57"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_set\_slave\_address([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint16\_t slave\_addr)
:   Set slave address when current role is i2c slave.

    参数
    :   - **id** – I2C id
        - **slave\_addr** – slave address

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2C\_NOT\_INIT: I2C driver not init
        - others: other errors.

<a id="_CPPv423bk_i2c_enable_interrupt8i2c_id_t"></a>

<a id="_CPPv323bk_i2c_enable_interrupt8i2c_id_t"></a> <a id="_CPPv223bk_i2c_enable_interrupt8i2c_id_t"></a> <a id="bk_i2c_enable_interrupt__i2c_id_t"></a> <a id="i2c_8h_1a4888dbd887d98a1890e461f644afbe11"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_enable\_interrupt([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Enable I2C interrupt.

    参数
    :   **id** – I2C id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_i2c_disable_interrupt8i2c_id_t"></a>

<a id="_CPPv324bk_i2c_disable_interrupt8i2c_id_t"></a> <a id="_CPPv224bk_i2c_disable_interrupt8i2c_id_t"></a> <a id="bk_i2c_disable_interrupt__i2c_id_t"></a> <a id="i2c_8h_1ac4178ac94172dfbb7b0b5014290d0604"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2c\_disable\_interrupt([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Disable I2C interrupt.

    参数
    :   **id** – I2C id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_i2c_is_bus_busy8i2c_id_t"></a>

<a id="_CPPv318bk_i2c_is_bus_busy8i2c_id_t"></a> <a id="_CPPv218bk_i2c_is_bus_busy8i2c_id_t"></a> <a id="bk_i2c_is_bus_busy__i2c_id_t"></a> <a id="i2c_8h_1ab75e8269f42a7c4220abd7e9757c2a98"></a> bool bk\_i2c\_is\_bus\_busy([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Check if I2C is busy.

    参数
    :   **id** – I2C id

    返回
    :   true: busy, false: not busy

<a id="_CPPv421bk_i2c_get_cur_action8i2c_id_t"></a>

<a id="_CPPv321bk_i2c_get_cur_action8i2c_id_t"></a> <a id="_CPPv221bk_i2c_get_cur_action8i2c_id_t"></a> <a id="bk_i2c_get_cur_action__i2c_id_t"></a> <a id="i2c_8h_1ae38d57ce673314ee8e50abd8a1918625"></a> uint32\_t bk\_i2c\_get\_cur\_action([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Get i2c current action, such as start,stop,send write\_addr.

    参数
    :   **id** – I2C id

    返回
    :   i2c action

<a id="_CPPv421bk_i2c_timer_callbackiPv"></a>

<a id="_CPPv321bk_i2c_timer_callbackiPv"></a> <a id="_CPPv221bk_i2c_timer_callbackiPv"></a> <a id="bk_i2c_timer_callback__i.voidP"></a> <a id="i2c_8h_1a87a8aa8f706332fde445118f72c670f3"></a> void bk\_i2c\_timer\_callback(int id, void \*myTimer)
:   bk\_i2c\_timer\_callback

    This API set timer call back

    返回

<a id="_CPPv419bk_i2c_get_busstatei"></a>

<a id="_CPPv319bk_i2c_get_busstatei"></a> <a id="_CPPv219bk_i2c_get_busstatei"></a> <a id="bk_i2c_get_busstate__i"></a> <a id="i2c_8h_1a4392f74fc3d6db4bbd1e470cec098407"></a> uint8\_t bk\_i2c\_get\_busstate(int id)
:   bk\_i2c\_get\_busstate

    This API get bus status idle or busy

    返回
    :   - 1: idle
        - 0: busy.

<a id="_CPPv421bk_i2c_get_transstatei"></a>

<a id="_CPPv321bk_i2c_get_transstatei"></a> <a id="_CPPv221bk_i2c_get_transstatei"></a> <a id="bk_i2c_get_transstate__i"></a> <a id="i2c_8h_1af4b096bfd84615ac065bc236de40f9c1"></a> uint8\_t bk\_i2c\_get\_transstate(int id)
:   bk\_i2c\_get\_transstate

    This API get bus status idle or busy

    返回
    :   - 1: ok
        - 0: fail.

<a id="i2c-api-typedefs"></a>

## I2C API Typedefs

<a id="id1"></a>

### Header File

- [i2c\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/i2c_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv415i2c_mem_param_t"></a>

<a id="_CPPv315i2c_mem_param_t"></a> <a id="_CPPv215i2c_mem_param_t"></a> <a id="i2c_mem_param_t"></a> <a id="structi2c__mem__param__t"></a> struct i2c\_mem\_param\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15i2c_mem_param_t8dev_addrE"></a>

    <a id="_CPPv3N15i2c_mem_param_t8dev_addrE"></a> <a id="_CPPv2N15i2c_mem_param_t8dev_addrE"></a> <a id="i2c_mem_param_t::dev_addr__uint32_t"></a> <a id="structi2c__mem__param__t_1ac50b11b2069c32201202fa19984ed844"></a> uint32\_t dev\_addr
    :   I2C slave device address

    <a id="_CPPv4N15i2c_mem_param_t8mem_addrE"></a>

    <a id="_CPPv3N15i2c_mem_param_t8mem_addrE"></a> <a id="_CPPv2N15i2c_mem_param_t8mem_addrE"></a> <a id="i2c_mem_param_t::mem_addr__uint32_t"></a> <a id="structi2c__mem__param__t_1a3d242c1b82351264929aad18927b02a0"></a> uint32\_t mem\_addr
    :   I2C slave device memerory address

    <a id="_CPPv4N15i2c_mem_param_t13mem_addr_sizeE"></a>

    <a id="_CPPv3N15i2c_mem_param_t13mem_addr_sizeE"></a> <a id="_CPPv2N15i2c_mem_param_t13mem_addr_sizeE"></a> <a id="i2c_mem_param_t::mem_addr_size__i2c_mem_addr_size_t"></a> <a id="structi2c__mem__param__t_1af9a1cd4d33b73c468b66517d24660c99"></a> [i2c\_mem\_addr\_size\_t](#_CPPv419i2c_mem_addr_size_t "i2c_mem_addr_size_t") mem\_addr\_size
    :   I2C slave device memerory address size

    <a id="_CPPv4N15i2c_mem_param_t4dataE"></a>

    <a id="_CPPv3N15i2c_mem_param_t4dataE"></a> <a id="_CPPv2N15i2c_mem_param_t4dataE"></a> <a id="i2c_mem_param_t::data__uint8_tP"></a> <a id="structi2c__mem__param__t_1ac14d180adca40c0b2aace23b99d87f73"></a> uint8\_t \*data
    :   I2C data pointer

    <a id="_CPPv4N15i2c_mem_param_t9data_sizeE"></a>

    <a id="_CPPv3N15i2c_mem_param_t9data_sizeE"></a> <a id="_CPPv2N15i2c_mem_param_t9data_sizeE"></a> <a id="i2c_mem_param_t::data_size__uint32_t"></a> <a id="structi2c__mem__param__t_1a8fba44b5e4276820bd4ac138958355ca"></a> uint32\_t data\_size
    :   I2C data size

    <a id="_CPPv4N15i2c_mem_param_t10timeout_msE"></a>

    <a id="_CPPv3N15i2c_mem_param_t10timeout_msE"></a> <a id="_CPPv2N15i2c_mem_param_t10timeout_msE"></a> <a id="i2c_mem_param_t::timeout_ms__uint32_t"></a> <a id="structi2c__mem__param__t_1afff20d607ab1e1fbc262ac6c2d0bc56c"></a> uint32\_t timeout\_ms
    :   I2C timeout ms

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_I2C_NOT_INIT"></a>

<a id="i2c__types_8h_1ad341b2ef46f5ab081e75d5f81ea166da"></a> BK\_ERR\_I2C\_NOT\_INIT
:   I2C driver not init

<a id="c.BK_ERR_I2C_ID_NOT_INIT"></a>

<a id="i2c__types_8h_1af673b4ab53a13d028729ff7fad5a304f"></a> BK\_ERR\_I2C\_ID\_NOT\_INIT
:   I2C id not init

<a id="c.BK_ERR_I2C_SM_BUS_BUSY"></a>

<a id="i2c__types_8h_1a080000a530c3efbf00b71817ac7a8411"></a> BK\_ERR\_I2C\_SM\_BUS\_BUSY
:   I2C bus busy

<a id="c.BK_ERR_I2C_ACK_TIMEOUT"></a>

<a id="i2c__types_8h_1a36aa2acae72a75f6a915e992ba0c5e49"></a> BK\_ERR\_I2C\_ACK\_TIMEOUT
:   I2C receive ack timeout

<a id="c.BK_ERR_I2C_CHECK_DEFCONFIG"></a>

<a id="i2c__types_8h_1a2993a5a6f63ce095757a7635390a87ae"></a> BK\_ERR\_I2C\_CHECK\_DEFCONFIG
:   I2C please check defconfig

<a id="c.BK_ERR_I2C_SCL_TIMEOUT"></a>

<a id="i2c__types_8h_1af954211881e0cf1d4fd453b4d08b64b6"></a> BK\_ERR\_I2C\_SCL\_TIMEOUT
:   I2C SCL timeout

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv49i2c_isr_t"></a>

<a id="_CPPv39i2c_isr_t"></a> <a id="_CPPv29i2c_isr_t"></a> <a id="i2c_isr_t"></a> <a id="i2c__types_8h_1a2dbe8b101e84f5bf8298f62e681025f2"></a> typedef void (\*i2c\_isr\_t)([i2c\_id\_t](#_CPPv48i2c_id_t "i2c_id_t") id, void \*param)
:   i2c interrupt service routine

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv415i2c_work_mode_t"></a>

<a id="_CPPv315i2c_work_mode_t"></a> <a id="_CPPv215i2c_work_mode_t"></a> <a id="i2c__types_8h_1ac9d8d79a0747bd98f82c86e274687e8d"></a> enum i2c\_work\_mode\_t
:   *Values:*

    <a id="_CPPv4N15i2c_work_mode_t16I2C_MASTER_WRITEE"></a>

    <a id="_CPPv3N15i2c_work_mode_t16I2C_MASTER_WRITEE"></a> <a id="_CPPv2N15i2c_work_mode_t16I2C_MASTER_WRITEE"></a> <a id="i2c__types_8h_1ac9d8d79a0747bd98f82c86e274687e8da26142ea4e9632dc03b60ba56467a07c0"></a> enumerator I2C\_MASTER\_WRITE
    :   I2C master write

    <a id="_CPPv4N15i2c_work_mode_t15I2C_MASTER_READE"></a>

    <a id="_CPPv3N15i2c_work_mode_t15I2C_MASTER_READE"></a> <a id="_CPPv2N15i2c_work_mode_t15I2C_MASTER_READE"></a> <a id="i2c__types_8h_1ac9d8d79a0747bd98f82c86e274687e8dac51f9be531d6d17fb679812ea1f047de"></a> enumerator I2C\_MASTER\_READ
    :   I2C master read

    <a id="_CPPv4N15i2c_work_mode_t15I2C_SLAVE_WRITEE"></a>

    <a id="_CPPv3N15i2c_work_mode_t15I2C_SLAVE_WRITEE"></a> <a id="_CPPv2N15i2c_work_mode_t15I2C_SLAVE_WRITEE"></a> <a id="i2c__types_8h_1ac9d8d79a0747bd98f82c86e274687e8da3c5f639c546b7bc9af0846402d67b077"></a> enumerator I2C\_SLAVE\_WRITE
    :   I2C slave write

    <a id="_CPPv4N15i2c_work_mode_t14I2C_SLAVE_READE"></a>

    <a id="_CPPv3N15i2c_work_mode_t14I2C_SLAVE_READE"></a> <a id="_CPPv2N15i2c_work_mode_t14I2C_SLAVE_READE"></a> <a id="i2c__types_8h_1ac9d8d79a0747bd98f82c86e274687e8dad07ffdcc87cf7803fb01f9e0d844e1b9"></a> enumerator I2C\_SLAVE\_READ
    :   I2C slave read

<a id="id2"></a>

### Header File

- [hal\_i2c\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_i2c_types.h)

<a id="id3"></a>

### Structures

<a id="_CPPv412i2c_config_t"></a>

<a id="_CPPv312i2c_config_t"></a> <a id="_CPPv212i2c_config_t"></a> <a id="i2c_config_t"></a> <a id="structi2c__config__t"></a> struct i2c\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12i2c_config_t9baud_rateE"></a>

    <a id="_CPPv3N12i2c_config_t9baud_rateE"></a> <a id="_CPPv2N12i2c_config_t9baud_rateE"></a> <a id="i2c_config_t::baud_rate__uint32_t"></a> <a id="structi2c__config__t_1a635875992c96a38dbf724c6727fd2fc1"></a> uint32\_t baud\_rate
    :   i2c clock rate

    <a id="_CPPv4N12i2c_config_t9addr_modeE"></a>

    <a id="_CPPv3N12i2c_config_t9addr_modeE"></a> <a id="_CPPv2N12i2c_config_t9addr_modeE"></a> <a id="i2c_config_t::addr_mode__i2c_addr_mode_t"></a> <a id="structi2c__config__t_1a9c50de5fc63aeee3d525ffc6d08ff560"></a> [i2c\_addr\_mode\_t](#_CPPv415i2c_addr_mode_t "i2c_addr_mode_t") addr\_mode
    :   i2c address mode

    <a id="_CPPv4N12i2c_config_t10slave_addrE"></a>

    <a id="_CPPv3N12i2c_config_t10slave_addrE"></a> <a id="_CPPv2N12i2c_config_t10slave_addrE"></a> <a id="i2c_config_t::slave_addr__uint16_t"></a> <a id="structi2c__config__t_1a9f2165312f721b0a686d2cf9e454c3ca"></a> uint16\_t slave\_addr
    :   i2c address for slave mode

    <a id="_CPPv4N12i2c_config_t7src_clkE"></a>

    <a id="_CPPv3N12i2c_config_t7src_clkE"></a> <a id="_CPPv2N12i2c_config_t7src_clkE"></a> <a id="i2c_config_t::src_clk__i2c_src_clk_t"></a> <a id="structi2c__config__t_1a3928bd842478c340578e44a153829ad6"></a> [i2c\_src\_clk\_t](#_CPPv413i2c_src_clk_t "i2c_src_clk_t") src\_clk
    :   i2c source clock

<a id="id4"></a>

### Macros

<a id="c.I2C_BAUD_RATE_50KHZ"></a>

<a id="hal__i2c__types_8h_1a861db27369d280889bd8909e9f8660b2"></a> I2C\_BAUD\_RATE\_50KHZ

<a id="c.I2C_BAUD_RATE_100KHZ"></a>

<a id="hal__i2c__types_8h_1a9d43eeb7af66e21b912524582fa3d106"></a> I2C\_BAUD\_RATE\_100KHZ

<a id="c.I2C_BAUD_RATE_200KHZ"></a>

<a id="hal__i2c__types_8h_1a251a13d5031c2d6269211b8fea6d71a6"></a> I2C\_BAUD\_RATE\_200KHZ

<a id="c.I2C_BAUD_RATE_400KHZ"></a>

<a id="hal__i2c__types_8h_1ac107b2d83392343d1058eb802758b846"></a> I2C\_BAUD\_RATE\_400KHZ

<a id="c.I2C_DEFAULT_BAUD_RATE"></a>

<a id="hal__i2c__types_8h_1a207445a2e17e56b36dcec7a8d2e76411"></a> I2C\_DEFAULT\_BAUD\_RATE

<a id="id5"></a>

### Type Definitions

<a id="_CPPv410i2c_unit_t"></a>

<a id="_CPPv310i2c_unit_t"></a> <a id="_CPPv210i2c_unit_t"></a> <a id="i2c_unit_t"></a> <a id="hal__i2c__types_8h_1a345ec4d22703d8ce253bac7b83e2632b"></a> typedef uint8\_t i2c\_unit\_t
:   i2c uint id

<a id="id6"></a>

### Enumerations

<a id="_CPPv48i2c_id_t"></a>

<a id="_CPPv38i2c_id_t"></a> <a id="_CPPv28i2c_id_t"></a> <a id="hal__i2c__types_8h_1af2fcdd34859c494bfb9eb2718aed0d64"></a> enum i2c\_id\_t
:   *Values:*

    <a id="_CPPv4N8i2c_id_t8I2C_ID_0E"></a>

    <a id="_CPPv3N8i2c_id_t8I2C_ID_0E"></a> <a id="_CPPv2N8i2c_id_t8I2C_ID_0E"></a> <a id="hal__i2c__types_8h_1af2fcdd34859c494bfb9eb2718aed0d64a7e9f8cfa87efd337fd020e0b8f3a6332"></a> enumerator I2C\_ID\_0
    :   i2c id 0

    <a id="_CPPv4N8i2c_id_t10I2C_ID_MAXE"></a>

    <a id="_CPPv3N8i2c_id_t10I2C_ID_MAXE"></a> <a id="_CPPv2N8i2c_id_t10I2C_ID_MAXE"></a> <a id="hal__i2c__types_8h_1af2fcdd34859c494bfb9eb2718aed0d64a608309f874b53747ae67e1fa8de3dc7d"></a> enumerator I2C\_ID\_MAX
    :   i2c id max

<a id="_CPPv413i2c_src_clk_t"></a>

<a id="_CPPv313i2c_src_clk_t"></a> <a id="_CPPv213i2c_src_clk_t"></a> <a id="hal__i2c__types_8h_1af1daba410e3699a55e49f9f4b3aa0bab"></a> enum i2c\_src\_clk\_t
:   *Values:*

    <a id="_CPPv4N13i2c_src_clk_t13I2C_SCLK_XTALE"></a>

    <a id="_CPPv3N13i2c_src_clk_t13I2C_SCLK_XTALE"></a> <a id="_CPPv2N13i2c_src_clk_t13I2C_SCLK_XTALE"></a> <a id="hal__i2c__types_8h_1af1daba410e3699a55e49f9f4b3aa0baba7d2ff79d7a10faacd2c1f934b7cc7738"></a> enumerator I2C\_SCLK\_XTAL
    :   I2C source clock xtal

    <a id="_CPPv4N13i2c_src_clk_t13I2C_SCLK_120ME"></a>

    <a id="_CPPv3N13i2c_src_clk_t13I2C_SCLK_120ME"></a> <a id="_CPPv2N13i2c_src_clk_t13I2C_SCLK_120ME"></a> <a id="hal__i2c__types_8h_1af1daba410e3699a55e49f9f4b3aa0baba0b8cf77bf5baf54a86b0173121c28938"></a> enumerator I2C\_SCLK\_120M
    :   I2C source clock 120M

<a id="_CPPv415i2c_addr_mode_t"></a>

<a id="_CPPv315i2c_addr_mode_t"></a> <a id="_CPPv215i2c_addr_mode_t"></a> <a id="hal__i2c__types_8h_1a7e11a27bbb10c136b92884ed8cf2e61a"></a> enum i2c\_addr\_mode\_t
:   *Values:*

    <a id="_CPPv4N15i2c_addr_mode_t18I2C_ADDR_MODE_7BITE"></a>

    <a id="_CPPv3N15i2c_addr_mode_t18I2C_ADDR_MODE_7BITE"></a> <a id="_CPPv2N15i2c_addr_mode_t18I2C_ADDR_MODE_7BITE"></a> <a id="hal__i2c__types_8h_1a7e11a27bbb10c136b92884ed8cf2e61aa59bb1c6aeeec9f94c93d9aca40bed88b"></a> enumerator I2C\_ADDR\_MODE\_7BIT
    :   i2c address mode 7bit

    <a id="_CPPv4N15i2c_addr_mode_t19I2C_ADDR_MODE_10BITE"></a>

    <a id="_CPPv3N15i2c_addr_mode_t19I2C_ADDR_MODE_10BITE"></a> <a id="_CPPv2N15i2c_addr_mode_t19I2C_ADDR_MODE_10BITE"></a> <a id="hal__i2c__types_8h_1a7e11a27bbb10c136b92884ed8cf2e61aaaf5c84ac712bacd50c095872bf525dd5"></a> enumerator I2C\_ADDR\_MODE\_10BIT
    :   i2c address mode 10bit

<a id="_CPPv420i2c_fifo_int_level_t"></a>

<a id="_CPPv320i2c_fifo_int_level_t"></a> <a id="_CPPv220i2c_fifo_int_level_t"></a> <a id="hal__i2c__types_8h_1aead75912dca5eafb4fcbf021b95d6e3e"></a> enum i2c\_fifo\_int\_level\_t
:   *Values:*

    <a id="_CPPv4N20i2c_fifo_int_level_t20I2C_FIFO_INT_LEVEL_1E"></a>

    <a id="_CPPv3N20i2c_fifo_int_level_t20I2C_FIFO_INT_LEVEL_1E"></a> <a id="_CPPv2N20i2c_fifo_int_level_t20I2C_FIFO_INT_LEVEL_1E"></a> <a id="hal__i2c__types_8h_1aead75912dca5eafb4fcbf021b95d6e3eae325412584ef0f908552cf4e9844db30"></a> enumerator I2C\_FIFO\_INT\_LEVEL\_1
    :   i2c fifo int level 1

    <a id="_CPPv4N20i2c_fifo_int_level_t20I2C_FIFO_INT_LEVEL_4E"></a>

    <a id="_CPPv3N20i2c_fifo_int_level_t20I2C_FIFO_INT_LEVEL_4E"></a> <a id="_CPPv2N20i2c_fifo_int_level_t20I2C_FIFO_INT_LEVEL_4E"></a> <a id="hal__i2c__types_8h_1aead75912dca5eafb4fcbf021b95d6e3ea2faeb3ce51ad094900b54a4d71f9677b"></a> enumerator I2C\_FIFO\_INT\_LEVEL\_4
    :   i2c fifo int level 4

    <a id="_CPPv4N20i2c_fifo_int_level_t20I2C_FIFO_INT_LEVEL_8E"></a>

    <a id="_CPPv3N20i2c_fifo_int_level_t20I2C_FIFO_INT_LEVEL_8E"></a> <a id="_CPPv2N20i2c_fifo_int_level_t20I2C_FIFO_INT_LEVEL_8E"></a> <a id="hal__i2c__types_8h_1aead75912dca5eafb4fcbf021b95d6e3ea0b8ec2d4b5758ec869557dd696169c45"></a> enumerator I2C\_FIFO\_INT\_LEVEL\_8
    :   i2c fifo int level 8

    <a id="_CPPv4N20i2c_fifo_int_level_t21I2C_FIFO_INT_LEVEL_12E"></a>

    <a id="_CPPv3N20i2c_fifo_int_level_t21I2C_FIFO_INT_LEVEL_12E"></a> <a id="_CPPv2N20i2c_fifo_int_level_t21I2C_FIFO_INT_LEVEL_12E"></a> <a id="hal__i2c__types_8h_1aead75912dca5eafb4fcbf021b95d6e3ea44efa608183b5f9ae5060b8c8ec57e9b"></a> enumerator I2C\_FIFO\_INT\_LEVEL\_12
    :   i2c fifo int level 12

<a id="_CPPv419i2c_mem_addr_size_t"></a>

<a id="_CPPv319i2c_mem_addr_size_t"></a> <a id="_CPPv219i2c_mem_addr_size_t"></a> <a id="hal__i2c__types_8h_1aa76ec3270e7cb75a1b8a36aaefb09a7b"></a> enum i2c\_mem\_addr\_size\_t
:   *Values:*

    <a id="_CPPv4N19i2c_mem_addr_size_t22I2C_MEM_ADDR_SIZE_8BITE"></a>

    <a id="_CPPv3N19i2c_mem_addr_size_t22I2C_MEM_ADDR_SIZE_8BITE"></a> <a id="_CPPv2N19i2c_mem_addr_size_t22I2C_MEM_ADDR_SIZE_8BITE"></a> <a id="hal__i2c__types_8h_1aa76ec3270e7cb75a1b8a36aaefb09a7badfb71dbda71a1cee74709ff49ae3fbae"></a> enumerator I2C\_MEM\_ADDR\_SIZE\_8BIT
    :   i2c memory address size 8bit

    <a id="_CPPv4N19i2c_mem_addr_size_t23I2C_MEM_ADDR_SIZE_16BITE"></a>

    <a id="_CPPv3N19i2c_mem_addr_size_t23I2C_MEM_ADDR_SIZE_16BITE"></a> <a id="_CPPv2N19i2c_mem_addr_size_t23I2C_MEM_ADDR_SIZE_16BITE"></a> <a id="hal__i2c__types_8h_1aa76ec3270e7cb75a1b8a36aaefb09a7ba24f481214396e299733448e3aa29f4a6"></a> enumerator I2C\_MEM\_ADDR\_SIZE\_16BIT
    :   i2c memory address size 16bit
