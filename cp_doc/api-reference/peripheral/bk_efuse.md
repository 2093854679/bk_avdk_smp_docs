# EFUSE


BK7259 CP 侧 EFUSE API（`include/driver/efuse.h`）。详细说明见
[EFUSE 开发指南](../../developer-guide/peripheral/bk_efuse.md "../../developer-guide/peripheral/bk_efuse.md")。


## EFUSE API Reference


### Header File


- [efuse.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/efuse.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/efuse.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_efuse_driver_init(void)
:   Init the EFUSE driver.

    This API init the resoure common:


    - Init EFUSE driver control memory


    **Attention**
    :   1. This API should be called before any other EFUSE APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_efuse_driver_deinit(void)
:   Deinit the EFUSE driver.

    This API free all resource related to EFUSE and disable EFUSE.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_efuse_write_byte(uint8_t addr, uint8_t data)
:   Efuse write operation @Notice: Each efuse address area has specific usage, please apply the area from PM before write data to the efuse address.

    参数
    :   - **addr** – efuse write address

        - **data** – efuse write data

    返回
    :   - BK_OK: succeed

        - BK_ERR_EFUSE_DRIVER_NOT_INIT: EFUSE driver not init

        - BK_ERR_EFUSE_ADDR_OUT_OF_RANGE: EFUSE address is out of range

        - BK_ERR_EFUSE_CANNOT_WRTIE: EFUSE cannot write, cannot change bit from 1 to 0

        - BK_ERR_EFUSE_WRTIE_NOT_EQUAL: EFUSE data read is not equal to the data written

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_efuse_read_byte(uint8_t addr, uint8_t *data)
:   Efuse read operation.

    参数
    :   - **addr** – read address

        - **data** – pointer to accept value of efuse read data

    返回
    :   - BK_OK: succeed

        - BK_ERR_EFUSE_DRIVER_NOT_INIT: EFUSE driver not init

        - BK_ERR_EFUSE_ADDR_OUT_OF_RANGE: EFUSE address is out of range

        - others: other errors.


## EFUSE API Typedefs


### Header File


- [efuse_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/efuse_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/efuse_types.h")


### Header File


- [hal/hal_efuse_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_efuse_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_efuse_types.h")


### Macros

BK_ERR_EFUSE_DRIVER_NOT_INIT
:   EFUSE driver not init

BK_ERR_EFUSE_ADDR_OUT_OF_RANGE
:   EFUSE address is out of range

BK_ERR_EFUSE_CANNOT_WRTIE
:   EFUSE cannot write, cannot change bit from 1 to 0

BK_ERR_EFUSE_WRTIE_NOT_EQUAL
:   EFUSE data read is not equal to the data written

BK_ERR_EFUSE_READ_FAIL
:   EFUSE data read fail

EFUSE_ADDR_BYTE0
:   efuse address defines @Notice: Each efuse address area has specific usage, please apply the area from PM before write data to the efuse address.

EFUSE_ADDR_BYTE1

EFUSE_ADDR_BYTE2

EFUSE_ADDR_BYTE3

EFUSE_ADDR_BYTE4

EFUSE_ADDR_BYTE5

EFUSE_ADDR_BYTE6

EFUSE_ADDR_BYTE7

EFUSE_ADDR_BYTE8

EFUSE_ADDR_BYTE9

EFUSE_ADDR_BYTE10

EFUSE_ADDR_BYTE11

EFUSE_ADDR_BYTE12

EFUSE_ADDR_BYTE13

EFUSE_ADDR_BYTE14

EFUSE_ADDR_BYTE15

EFUSE_ADDR_BYTE16

EFUSE_ADDR_BYTE17

EFUSE_ADDR_BYTE18

EFUSE_ADDR_BYTE19

EFUSE_ADDR_BYTE20

EFUSE_ADDR_BYTE21

EFUSE_ADDR_BYTE22

EFUSE_ADDR_BYTE23

EFUSE_ADDR_BYTE24

EFUSE_ADDR_BYTE25

EFUSE_ADDR_BYTE26

EFUSE_ADDR_BYTE27

EFUSE_ADDR_BYTE28

EFUSE_ADDR_BYTE29

EFUSE_ADDR_BYTE30

EFUSE_ADDR_BYTE31

EFUSE_DEVICE_ID_BYTE_NUM
:   efuse device id defines OTP2 device id (BK7259 / OTP v1) is 8 bytes, read/written via the OTP2 AHB path. Legacy raw-efuse device id is 5 bytes, stored at efuse address byte 0x18 ~ 0x1c. the efuse device id is set via ate cmds

EFUSE_LEGACY_DEVICE_ID_BYTE_NUM

EFUSE_DEVICE_ID_SN_MINIMUM

EFUSE_DEVICE_ID_SN_MAXIMUM

EFUSE_WAFER_ID_MINIMUM

EFUSE_WAFER_ID_MAXIMUM


### Type Definitions

typedef uint8_t efuse_unit_t
:   efuse uint id
