# OTP


BK7259 AP 侧 OTP API（`include/driver/otp.h`）。详细说明见
[OTP 开发指南](../../developer-guide/peripheral/bk_otp.md "../../developer-guide/peripheral/bk_otp.md")。


## OTP API Reference


### Header File


- [otp.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/otp.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/otp.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_otp_init(void)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_otp_deinit(void)
:   OTP finalization.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_otp_read_bytes_nonsecure(uint8_t *buffer, uint32_t addr, uint32_t len)
:   OTP read operation.


    **Attention**
    :   1. addr+len should be less than 0x800


    **Attention**
    :   2. this API can only access non-secure OTP bank


    **Attention**
    :   3. this api blocks for 5ms waiting for OTP to stabilize

    参数
    :   - **buffer** – point to the buffer that reads the data

        - **addr** – read address, address range 0x0&#8212;0x800

        - **len** – read length

    返回
    :   - BK_OK: succeed

        - BK_ERR_EFUSE_DRIVER_NOT_INIT: EFUSE driver not init

        - BK_ERR_EFUSE_ADDR_OUT_OF_RANGE: EFUSE address is out of range

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_otp_apb_read_by_offset(uint32_t item_offset, uint8_t *buf, uint32_t size)
:   OTP read with item real offset.

    参数
    :   - **item_offset** – the real item offset to read from otp

        - **buf** – point to the buffer that reads the data

        - **size** – length of item to read

    返回
    :   - BK_OK: succeed

        - BK_ERR_NO_READ_PERMISSION: wrong permission to read

        - BK_ERR_OTP_ADDR_OUT_OF_RANGE: param size not match item real size

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_otp_ahb_read_by_offset(uint32_t item_offset, uint8_t *buf, uint32_t size)
:   OTP2 read with item real offset.

    参数
    :   - **item_offset** – the real item offset to read from otp2

        - **buf** – point to the buffer that reads the data

        - **size** – length of item to read

    返回
    :   - BK_OK: succeed

        - others: other errors.


## OTP API Typedefs


### Header File


- [otp_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/otp_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/otp_types.h")


### Enumerations

enum otp_status_t
:   *Values:*

    enumerator OTP_BUSY

    enumerator OTP_ERROR

    enumerator OTP_WARNING

    enumerator OTP_WRONG

    enumerator OTP_FORBID


### Header File


- [hal/hal_otp_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_otp_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_otp_types.h")


### Macros

BK_ERR_OTP_READ_BUFFER_NULL
:   The pointed buff is NULL

BK_ERR_OTP_ADDR_OUT_OF_RANGE
:   OTP address is out of range

BK_ERR_NO_READ_PERMISSION
:   Not have read privilege

BK_ERR_NO_WRITE_PERMISSION
:   Not have write privilege

BK_ERR_OTP_PERMISSION_WRONG
:   OTP permission value error

BK_ERR_OTP_NOT_EMPTY
:   try to write area already has value

BK_ERR_OTP_UPDATE_NOT_EQUAL
:   after update not equal to expected

BK_ERR_OTP_OPERATION_ERROR
:   otp operation error

BK_ERR_OTP_OPERATION_WARNING
:   otp operation warning

BK_ERR_OTP_OPERATION_WRONG
:   otp operation wrong

BK_ERR_OTP_OPERATION_FORBID
:   otp operation forbid

BK_ERR_OTP_OPERATION_FAIL

BK_ERR_OTP_INIT_FAIL

BK_ERR_OTP_INDEX_WRONG
:   OTP item index error

BK_ERR_OTP_OPERATION_ERROR_MASK

BK_ERR_OTP_OPERATION_FAIL_MASK

BK_ERR_OTP_INIT_FAIL_MASK

BK_ERR_OTP_FULL_ERROR_MASK


### Type Definitions

typedef uint8_t otp_unit_t
:   otp uint id
