---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_flash_partition.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="flash-partition"></a>

# FLASH PARTITION

BK7259 CP 侧 Flash 分区 API（`include/driver/flash_partition.h`）。

<a id="flash-partition-api-reference"></a>

## FLASH PARTITION API Reference

<a id="header-file"></a>

### Header File

- [flash\_partition.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/flash_partition.h)

<a id="functions"></a>

### Functions

<a id="_CPPv427bk_flash_partition_get_info14bk_partition_t"></a>

<a id="_CPPv327bk_flash_partition_get_info14bk_partition_t"></a> <a id="_CPPv227bk_flash_partition_get_info14bk_partition_t"></a> <a id="bk_flash_partition_get_info__bk_partition_t"></a> <a id="flash__partition_8h_1a6a40bf54d95fcf7edbd41d996068cf42"></a> [bk\_logic\_partition\_t](#_CPPv420bk_logic_partition_t "bk_logic_partition_t") \*bk\_flash\_partition\_get\_info([bk\_partition\_t](#_CPPv414bk_partition_t "bk_partition_t") partition)
:   Get the infomation of the specified flash area.

    参数
    :   **partition** – The target flash logical partition

    返回
    :   bk flash logic partition struct

<a id="_CPPv424bk_flash_partition_erase14bk_partition_t8uint32_t8uint32_t"></a>

<a id="_CPPv324bk_flash_partition_erase14bk_partition_t8uint32_t8uint32_t"></a> <a id="_CPPv224bk_flash_partition_erase14bk_partition_t8uint32_t8uint32_t"></a> <a id="bk_flash_partition_erase__bk_partition_t.uint32_t.uint32_t"></a> <a id="flash__partition_8h_1a69bd54922de9134d527a2cd597449f18"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_partition\_erase([bk\_partition\_t](#_CPPv414bk_partition_t "bk_partition_t") partition, uint32\_t offset, uint32\_t size)
:   Erase an area on a Flash logical partition.

    备注

    Erase on an address will erase all data on a sector that the address is belonged to, this function does not save data that beyond the address area but in the affected sector, the data will be lost.

    参数
    :   - **partition** – The target flash logical partition which should be erased
        - **offset** – Start address of the erased flash area
        - **size** – Size of the erased flash area

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv424bk_flash_partition_write14bk_partition_tPK7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv324bk_flash_partition_write14bk_partition_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv224bk_flash_partition_write14bk_partition_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="bk_flash_partition_write__bk_partition_t.uint8_tCP.uint32_t.uint32_t"></a> <a id="flash__partition_8h_1a0d8277d82a5816e7611cca4c9ba6afa2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_partition\_write([bk\_partition\_t](#_CPPv414bk_partition_t "bk_partition_t") partition, const uint8\_t \*buffer, uint32\_t offset, uint32\_t buffer\_len)
:   Write data to an area on a Flash logical partition.

    参数
    :   - **partition** – The target flash logical partition which should be written
        - **buffer** – Pointer to the data buffer that will be written to flash
        - **off\_set** – The offset of write address
        - **buffer\_len** – The length of the buffer

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv423bk_flash_partition_read14bk_partition_tP7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv323bk_flash_partition_read14bk_partition_tP7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv223bk_flash_partition_read14bk_partition_tP7uint8_t8uint32_t8uint32_t"></a> <a id="bk_flash_partition_read__bk_partition_t.uint8_tP.uint32_t.uint32_t"></a> <a id="flash__partition_8h_1a23fcd8caef7255dc7546f6f96aa3d357"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_flash\_partition\_read([bk\_partition\_t](#_CPPv414bk_partition_t "bk_partition_t") partition, uint8\_t \*out\_buffer, uint32\_t offset, uint32\_t buffer\_len)
:   Read data from an area on a Flash to data buffer in RAM.

    参数
    :   - **partition** – The target flash logical partition which should be read
        - **out\_buffer** – Pointer to the data buffer that stores the data read from flash
        - **offsets** – The offset of read address
        - **buffer\_len** – The length of the buffer

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv425bk_spec_flash_write_bytes14bk_partition_tPK7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv325bk_spec_flash_write_bytes14bk_partition_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv225bk_spec_flash_write_bytes14bk_partition_tPK7uint8_t8uint32_t8uint32_t"></a> <a id="bk_spec_flash_write_bytes__bk_partition_t.uint8_tCP.uint32_t.uint32_t"></a> <a id="flash__partition_8h_1a20dcf931fdefca108317b144f9088ec3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_spec\_flash\_write\_bytes([bk\_partition\_t](#_CPPv414bk_partition_t "bk_partition_t") partition, const uint8\_t \*user\_buf, uint32\_t size, uint32\_t offset)
:   Write data to flash (only operating 4k flash space)

    参数
    :   - **partition** – partition to write (eg:partition BK\_PARTITION\_RF\_FIRMWARE)
        - **user\_buf** – the pointer to data which is to write
        - **size** – size to write
        - **offset** – offset to write

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_FLASH\_ADDR\_OUT\_OF\_RANGE: flash address is out of range
        - others: other errors.

<a id="structures"></a>

### Structures

<a id="_CPPv420bk_logic_partition_t"></a>

<a id="_CPPv320bk_logic_partition_t"></a> <a id="_CPPv220bk_logic_partition_t"></a> <a id="bk_logic_partition_t"></a> <a id="structbk__logic__partition__t"></a> struct bk\_logic\_partition\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20bk_logic_partition_t15partition_ownerE"></a>

    <a id="_CPPv3N20bk_logic_partition_t15partition_ownerE"></a> <a id="_CPPv2N20bk_logic_partition_t15partition_ownerE"></a> <a id="bk_logic_partition_t::partition_owner__bk_flash_t"></a> <a id="structbk__logic__partition__t_1a4a84f0f2dc9f7a965d7d474dd2c45fbb"></a> [bk\_flash\_t](#_CPPv410bk_flash_t "bk_flash_t") partition\_owner
    :   flash partition owners

    <a id="_CPPv4N20bk_logic_partition_t21partition_descriptionE"></a>

    <a id="_CPPv3N20bk_logic_partition_t21partition_descriptionE"></a> <a id="_CPPv2N20bk_logic_partition_t21partition_descriptionE"></a> <a id="bk_logic_partition_t::partition_description__cCP"></a> <a id="structbk__logic__partition__t_1a6cc1bc293ee15fedcdc0f7f2313e39cc"></a> const char \*partition\_description
    :   flash partition description

    <a id="_CPPv4N20bk_logic_partition_t20partition_start_addrE"></a>

    <a id="_CPPv3N20bk_logic_partition_t20partition_start_addrE"></a> <a id="_CPPv2N20bk_logic_partition_t20partition_start_addrE"></a> <a id="bk_logic_partition_t::partition_start_addr__uint32_t"></a> <a id="structbk__logic__partition__t_1a406dee3af89af369a3a0e036af3b5bd6"></a> uint32\_t partition\_start\_addr
    :   flash partition start address

    <a id="_CPPv4N20bk_logic_partition_t16partition_lengthE"></a>

    <a id="_CPPv3N20bk_logic_partition_t16partition_lengthE"></a> <a id="_CPPv2N20bk_logic_partition_t16partition_lengthE"></a> <a id="bk_logic_partition_t::partition_length__uint32_t"></a> <a id="structbk__logic__partition__t_1a4fca2a7e34c6b94ca186c6371954bc52"></a> uint32\_t partition\_length
    :   flash partition length

    <a id="_CPPv4N20bk_logic_partition_t17partition_optionsE"></a>

    <a id="_CPPv3N20bk_logic_partition_t17partition_optionsE"></a> <a id="_CPPv2N20bk_logic_partition_t17partition_optionsE"></a> <a id="bk_logic_partition_t::partition_options__uint32_t"></a> <a id="structbk__logic__partition__t_1af56d447fab2e36c000a10033a298b704"></a> uint32\_t partition\_options
    :   flash partition options

<a id="macros"></a>

### Macros

<a id="c.PAR_OPT_READ_POS"></a>

<a id="flash__partition_8h_1ab1e58b6e8ff6f3761bdf24c04478c7f6"></a> PAR\_OPT\_READ\_POS

<a id="c.PAR_OPT_READ_DIS"></a>

<a id="flash__partition_8h_1a4f5a8817f87909dd93f8b655236bfa97"></a> PAR\_OPT\_READ\_DIS

<a id="c.PAR_OPT_READ_EN"></a>

<a id="flash__partition_8h_1ad38fd963b47f4417058bde27626cec60"></a> PAR\_OPT\_READ\_EN

<a id="c.PAR_OPT_WRITE_POS"></a>

<a id="flash__partition_8h_1a68ff33d27eb40be97075ac7acc28b1dc"></a> PAR\_OPT\_WRITE\_POS

<a id="c.PAR_OPT_WRITE_DIS"></a>

<a id="flash__partition_8h_1a2e3aedc128cf4fc5c1962e9229ef00e9"></a> PAR\_OPT\_WRITE\_DIS

<a id="c.PAR_OPT_WRITE_EN"></a>

<a id="flash__partition_8h_1a06797fb3f63772e5b3b7b72edd7ae86b"></a> PAR\_OPT\_WRITE\_EN

<a id="c.PAR_OPT_EXECUTE_POS"></a>

<a id="flash__partition_8h_1a4b859874465b68d0b73f199cb63a6a4e"></a> PAR\_OPT\_EXECUTE\_POS

<a id="c.PAR_OPT_EXECUTE_DIS"></a>

<a id="flash__partition_8h_1af195043b4881e393d9ae1771bfa79141"></a> PAR\_OPT\_EXECUTE\_DIS

<a id="c.PAR_OPT_EXECUTE_EN"></a>

<a id="flash__partition_8h_1ad3cbc9b409aa5a152c6f96e74b207055"></a> PAR\_OPT\_EXECUTE\_EN

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv414bk_partition_t"></a>

<a id="_CPPv314bk_partition_t"></a> <a id="_CPPv214bk_partition_t"></a> <a id="bk_partition_t"></a> <a id="flash__partition_8h_1a5ab0512c0b6e9b4e0961aefc9f5465fc"></a> typedef uint32\_t bk\_partition\_t

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv410bk_flash_t"></a>

<a id="_CPPv310bk_flash_t"></a> <a id="_CPPv210bk_flash_t"></a> <a id="flash__partition_8h_1a4269a42fcd5cccdf95cc910a91c515f8"></a> enum bk\_flash\_t
:   *Values:*

    <a id="_CPPv4N10bk_flash_t17BK_FLASH_EMBEDDEDE"></a>

    <a id="_CPPv3N10bk_flash_t17BK_FLASH_EMBEDDEDE"></a> <a id="_CPPv2N10bk_flash_t17BK_FLASH_EMBEDDEDE"></a> <a id="flash__partition_8h_1a4269a42fcd5cccdf95cc910a91c515f8a18d4385876664c390fb5dd7f411d72db"></a> enumerator BK\_FLASH\_EMBEDDED

    <a id="_CPPv4N10bk_flash_t12BK_FLASH_SPIE"></a>

    <a id="_CPPv3N10bk_flash_t12BK_FLASH_SPIE"></a> <a id="_CPPv2N10bk_flash_t12BK_FLASH_SPIE"></a> <a id="flash__partition_8h_1a4269a42fcd5cccdf95cc910a91c515f8ad29e6e471dea17232cabc86fea92d5d0"></a> enumerator BK\_FLASH\_SPI

    <a id="_CPPv4N10bk_flash_t12BK_FLASH_MAXE"></a>

    <a id="_CPPv3N10bk_flash_t12BK_FLASH_MAXE"></a> <a id="_CPPv2N10bk_flash_t12BK_FLASH_MAXE"></a> <a id="flash__partition_8h_1a4269a42fcd5cccdf95cc910a91c515f8a2dd397b52046e6b78c3aec143626d038"></a> enumerator BK\_FLASH\_MAX

    <a id="_CPPv4N10bk_flash_t13BK_FLASH_NONEE"></a>

    <a id="_CPPv3N10bk_flash_t13BK_FLASH_NONEE"></a> <a id="_CPPv2N10bk_flash_t13BK_FLASH_NONEE"></a> <a id="flash__partition_8h_1a4269a42fcd5cccdf95cc910a91c515f8ab37cc8aea703f16be396c045c6ddf474"></a> enumerator BK\_FLASH\_NONE
