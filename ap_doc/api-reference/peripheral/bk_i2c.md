# I2C



## I2C API Status

| API | BK7259_AP |
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


## I2C UNIT Number

| Capability | BK7259_AP | BK7259_CP |
| --- | --- | --- |
| UNIT Number | 2 | 2 |


## I2C Pin and GPIO Map

| I2C Pin | BK7259_AP | BK7259_CP |
| --- | --- | --- |
| I2C0 SCL | 20 | 20 |
| I2C0 SDA | 21 | 21 |
| I2C1 SCL | 42 | 42 |
| I2C1 SDA | 43 | 43 |
| I2C1 SCL | 0 | 0 |
| I2C1 SDA | 1 | 1 |


## I2C API Reference


### Header File


- [i2c.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/i2c.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/i2c.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_driver_init(void)
:   Init the I2C driver.

    This API init the resoure common:


    - Init I2C driver control memory


    **Attention**
    :   1. This API should be called before any other I2C APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_driver_deinit(void)
:   Deinit the I2C driver.

    This API free all resource related to I2C and disable I2C.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_init([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, const [i2c_config_t](#_CPPv412i2c_config_t "i2c_config_t") *cfg)
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
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: I2C config paramter is NULL

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_deinit([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Deinit the I2C id.

    This API deinit the I2C id:


    - Stop the I2C id

    - Disable the I2C id interrupt

    - Power down the I2C id

    参数
    :   **id** – I2C id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_master_write([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint32_t dev_addr, const uint8_t *data, uint32_t size, uint32_t timeout_ms)
:   Write data to the I2C port from a given buffer and length, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id

        - **dev_addr** – slave device address

        - **data** – pointer to the buffer

        - **size** – data length to write

        - **timeout_ms** – timeout ms

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_master_write_noaddr([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, const uint8_t *data, uint32_t size, uint32_t timeout_ms)
:   Write data to the I2C port from a given buffer and length without slave address, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id

        - **data** – pointer to the buffer

        - **size** – data length to write

        - **timeout_ms** – timeout ms

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_master_read([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint32_t dev_addr, uint8_t *data, uint32_t size, uint32_t timeout_ms)
:   I2C read data from I2C buffer, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id

        - **dev_addr** – slave device address

        - **data** – pointer to the buffer

        - **size** – data length to read

        - **timeout_ms** – timeout ms

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_master_read_noaddr([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint8_t *data, uint32_t size, uint32_t timeout_ms)
:   I2C read data from I2C buffer without slave address, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id

        - **data** – pointer to the buffer

        - **size** – data length to read

        - **timeout_ms** – timeout ms

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_slave_write([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, const uint8_t *data, uint32_t size, uint32_t timeout_ms)
:   Write data to the I2C port from a given buffer and length, It shall only be called in I2C slave mode.

    参数
    :   - **id** – I2C id

        - **data** – pointer to the buffer

        - **size** – data length to write

        - **timeout_ms** – timeout ms

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_slave_read([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint8_t *data, uint32_t size, uint32_t timeout_ms)
:   I2C read data from I2C buffer, It shall only be called in I2C slave mode.

    参数
    :   - **id** – I2C id

        - **dev_addr** – slave device address

        - **data** – pointer to the buffer

        - **size** – data length to read

        - **timeout_ms** – timeout ms

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_memory_write([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, const [i2c_mem_param_t](#_CPPv415i2c_mem_param_t "i2c_mem_param_t") *mem_param)
:   Write data to the specific memory address from a given buffer and length, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id

        - **mem_param** – memory parameter

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: I2C mem_param is NULL

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_memory_read([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, const [i2c_mem_param_t](#_CPPv415i2c_mem_param_t "i2c_mem_param_t") *mem_param)
:   I2C read data from I2C specific memory address, It shall only be called in I2C master mode.

    参数
    :   - **id** – I2C id

        - **mem_param** – memory parameter

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: I2C mem_param is NULL

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_set_baud_rate([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint32_t baud_rate)
:   I2C set baud rate.

    参数
    :   - **id** – I2C id

        - **baud_rate** – baud rate

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_set_slave_address([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, uint16_t slave_addr)
:   Set slave address when current role is i2c slave.

    参数
    :   - **id** – I2C id

        - **slave_addr** – slave address

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_enable_interrupt([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Enable I2C interrupt.

    参数
    :   **id** – I2C id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_disable_interrupt([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Disable I2C interrupt.

    参数
    :   **id** – I2C id

    返回
    :   - BK_OK: succeed

        - others: other errors.

bool bk_i2c_is_bus_busy([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Check if I2C is busy.

    参数
    :   **id** – I2C id

    返回
    :   true: busy, false: not busy

uint32_t bk_i2c_get_cur_action([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Get i2c current action, such as start,stop,send write_addr.

    参数
    :   **id** – I2C id

    返回
    :   i2c action

void bk_i2c_timer_callback(int id, void *myTimer)
:   bk_i2c_timer_callback

    This API set timer call back

    返回

uint8_t bk_i2c_get_busstate(int id)
:   bk_i2c_get_busstate

    This API get bus status idle or busy

    返回
    :   - 1: idle

        - 0: busy.

uint8_t bk_i2c_get_transstate(int id)
:   bk_i2c_get_transstate

    This API get bus status idle or busy

    返回
    :   - 1: ok

        - 0: fail.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_init_v2([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, const [i2c_config_t](#_CPPv412i2c_config_t "i2c_config_t") *cfg)
:   Init the SIM I2C id.

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
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: I2C config paramter is NULL

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_deinit_v2([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id)
:   Deinit the SIM I2C driver.

    This API free all resource related to I2C and disable I2C.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_memory_write_v2([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, const [i2c_mem_param_t](#_CPPv415i2c_mem_param_t "i2c_mem_param_t") *mem_param)
:   Write data to the specific memory address from a given buffer and length, It shall only be called in SIM I2C master mode.

    参数
    :   - **id** – I2C id

        - **mem_param** – memory parameter

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: I2C mem_param is NULL

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2c_memory_read_v2([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, const [i2c_mem_param_t](#_CPPv415i2c_mem_param_t "i2c_mem_param_t") *mem_param)
:   SIM I2C read data from I2C specific memory address, It shall only be called in SIM I2C master mode.

    参数
    :   - **id** – I2C id

        - **mem_param** – memory parameter

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: I2C mem_param is NULL

        - BK_ERR_I2C_NOT_INIT: I2C driver not init

        - BK_ERR_I2C_INVALID_ID: I2C id number is invalid

        - BK_ERR_I2C_ID_NOT_INIT: I2C id not init

        - others: other errors.


## I2C API Typedefs


### Header File


- [i2c_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/i2c_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/i2c_types.h")


### Structures

struct i2c_mem_param_t


### Macros

BK_ERR_I2C_NOT_INIT
:   I2C driver not init

BK_ERR_I2C_ID_NOT_INIT
:   I2C id not init

BK_ERR_I2C_SM_BUS_BUSY
:   I2C bus busy

BK_ERR_I2C_ACK_TIMEOUT
:   I2C receive ack timeout

BK_ERR_I2C_CHECK_DEFCONFIG
:   I2C please check defconfig

BK_ERR_I2C_SCL_TIMEOUT
:   I2C SCL timeout


### Type Definitions

typedef void (*i2c_isr_t)([i2c_id_t](#_CPPv48i2c_id_t "i2c_id_t") id, void *param)
:   i2c interrupt service routine


### Enumerations

enum i2c_work_mode_t
:   *Values:*

    enumerator I2C_MASTER_WRITE
    :   I2C master write

    enumerator I2C_MASTER_READ
    :   I2C master read

    enumerator I2C_SLAVE_WRITE
    :   I2C slave write

    enumerator I2C_SLAVE_READ
    :   I2C slave read


### Header File


- [hal/hal_i2c_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_i2c_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_i2c_types.h")


### Structures

struct i2c_config_t


### Macros

I2C_BAUD_RATE_50KHZ

I2C_BAUD_RATE_100KHZ

I2C_BAUD_RATE_200KHZ

I2C_BAUD_RATE_400KHZ

I2C_DEFAULT_BAUD_RATE


### Type Definitions

typedef uint8_t i2c_unit_t
:   i2c uint id


### Enumerations

enum i2c_id_t
:   *Values:*

    enumerator I2C_ID_0
    :   i2c id 0

    enumerator I2C_ID_MAX
    :   i2c id max

enum i2c_src_clk_t
:   *Values:*

    enumerator I2C_SCLK_XTAL
    :   I2C source clock xtal

    enumerator I2C_SCLK_120M
    :   I2C source clock 120M

enum i2c_addr_mode_t
:   *Values:*

    enumerator I2C_ADDR_MODE_7BIT
    :   i2c address mode 7bit

    enumerator I2C_ADDR_MODE_10BIT
    :   i2c address mode 10bit

enum i2c_fifo_int_level_t
:   *Values:*

    enumerator I2C_FIFO_INT_LEVEL_1
    :   i2c fifo int level 1

    enumerator I2C_FIFO_INT_LEVEL_4
    :   i2c fifo int level 4

    enumerator I2C_FIFO_INT_LEVEL_8
    :   i2c fifo int level 8

    enumerator I2C_FIFO_INT_LEVEL_12
    :   i2c fifo int level 12

enum i2c_mem_addr_size_t
:   *Values:*

    enumerator I2C_MEM_ADDR_SIZE_8BIT
    :   i2c memory address size 8bit

    enumerator I2C_MEM_ADDR_SIZE_16BIT
    :   i2c memory address size 16bit
