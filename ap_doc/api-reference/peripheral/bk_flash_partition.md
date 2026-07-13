# FLASH PARTITION



## FLASH PARTITION API Status

| API | BK7259_AP |
| --- | --- |
| [`bk_flash_partition_get_info()`](#_CPPv427bk_flash_partition_get_info14bk_partition_t "bk_flash_partition_get_info") | Y |
| [`bk_flash_partition_erase()`](#_CPPv424bk_flash_partition_erase14bk_partition_t8uint32_t8uint32_t "bk_flash_partition_erase") | Y |
| [`bk_flash_partition_write()`](#_CPPv424bk_flash_partition_write14bk_partition_tPK7uint8_t8uint32_t8uint32_t "bk_flash_partition_write") | Y |
| [`bk_flash_partition_read()`](#_CPPv423bk_flash_partition_read14bk_partition_tP7uint8_t8uint32_t8uint32_t "bk_flash_partition_read") | Y |


## FLASH PARTITION API Reference


### Header File


- [flash_partition.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/flash_partition.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/flash_partition.h")


### Functions

[bk_logic_partition_t](#_CPPv420bk_logic_partition_t "bk_logic_partition_t") *bk_flash_partition_get_info([bk_partition_t](#_CPPv414bk_partition_t "bk_partition_t") partition)
:   Get the infomation of the specified flash area.

    参数
    :   **partition** – The target flash logical partition

    返回
    :   bk flash logic partition struct

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_partition_erase([bk_partition_t](#_CPPv414bk_partition_t "bk_partition_t") partition, uint32_t offset, uint32_t size)
:   Erase an area on a Flash logical partition.

    备注

    Erase on an address will erase all data on a sector that the address is belonged to, this function does not save data that beyond the address area but in the affected sector, the data will be lost.

    参数
    :   - **partition** – The target flash logical partition which should be erased

        - **offset** – Start address of the erased flash area

        - **size** – Size of the erased flash area

    返回
    :   - BK_OK: succeed

        - others: other errors

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_partition_write([bk_partition_t](#_CPPv414bk_partition_t "bk_partition_t") partition, const uint8_t *buffer, uint32_t offset, uint32_t buffer_len)
:   Write data to an area on a Flash logical partition.

    参数
    :   - **partition** – The target flash logical partition which should be written

        - **buffer** – Pointer to the data buffer that will be written to flash

        - **off_set** – The offset of write address

        - **buffer_len** – The length of the buffer

    返回
    :   - BK_OK: succeed

        - others: other errors

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_flash_partition_read([bk_partition_t](#_CPPv414bk_partition_t "bk_partition_t") partition, uint8_t *out_buffer, uint32_t offset, uint32_t buffer_len)
:   Read data from an area on a Flash to data buffer in RAM.

    参数
    :   - **partition** – The target flash logical partition which should be read

        - **out_buffer** – Pointer to the data buffer that stores the data read from flash

        - **offsets** – The offset of read address

        - **buffer_len** – The length of the buffer

    返回
    :   - BK_OK: succeed

        - others: other errors

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_spec_flash_write_bytes([bk_partition_t](#_CPPv414bk_partition_t "bk_partition_t") partition, const uint8_t *user_buf, uint32_t size, uint32_t offset)
:   Write data to flash (only operating 4k flash space)

    参数
    :   - **partition** – partition to write (eg:partition BK_PARTITION_RF_FIRMWARE)

        - **user_buf** – the pointer to data which is to write

        - **size** – size to write

        - **offset** – offset to write

    返回
    :   - BK_OK: succeed

        - BK_ERR_FLASH_ADDR_OUT_OF_RANGE: flash address is out of range

        - others: other errors.


### Structures

struct bk_logic_partition_t


### Macros

PAR_OPT_READ_POS

PAR_OPT_READ_DIS

PAR_OPT_READ_EN

PAR_OPT_WRITE_POS

PAR_OPT_WRITE_DIS

PAR_OPT_WRITE_EN

PAR_OPT_EXECUTE_POS

PAR_OPT_EXECUTE_DIS

PAR_OPT_EXECUTE_EN


### Type Definitions

typedef uint32_t bk_partition_t


### Enumerations

enum bk_flash_t
:   *Values:*

    enumerator BK_FLASH_EMBEDDED

    enumerator BK_FLASH_SPI

    enumerator BK_FLASH_MAX

    enumerator BK_FLASH_NONE
