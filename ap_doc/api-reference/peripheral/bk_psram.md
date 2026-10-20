---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_psram.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="psram"></a>

# PSRAM

BK7259 AP 侧 PSRAM API（`include/driver/psram.h`、`include/driver/qspi_psram.h`）。
详细说明见 [PSRAM 开发指南](../../developer-guide/peripheral/bk_psram.md)。

<a id="psram-api-reference"></a>

## PSRAM API Reference

<a id="header-file"></a>

### Header File

- [psram.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/psram.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419bk_psram_byte_writePhh"></a>

<a id="_CPPv319bk_psram_byte_writePhh"></a> <a id="_CPPv219bk_psram_byte_writePhh"></a> <a id="bk_psram_byte_write__unsigned-cP.unsigned-c"></a> <a id="group__bk__api__psram_1gac58960fb49e5acf47daf93e57fae14b8"></a> static inline void bk\_psram\_byte\_write(unsigned char \*addr, unsigned char value)
:   write one byte of data to psram

    参数
    :   - **addr** – the psram address to write to
        - **value** – the value of one byte of data

    返回
    :   - NULL

<a id="_CPPv424bk_psram_half_word_writePtt"></a>

<a id="_CPPv324bk_psram_half_word_writePtt"></a> <a id="_CPPv224bk_psram_half_word_writePtt"></a> <a id="bk_psram_half_word_write__unsigned-shortP.unsigned-short"></a> <a id="group__bk__api__psram_1ga1c071f7644ca6505811e4c4d43abb5c1"></a> static inline void bk\_psram\_half\_word\_write(unsigned short \*dst, unsigned short value)
:   write two bytes of data to psram

    参数
    :   - **addr** – the psram address to write to
        - **value** – the value of two bytes of data

    返回
    :   - NULL

<a id="_CPPv419bk_psram_word_writePjj"></a>

<a id="_CPPv319bk_psram_word_writePjj"></a> <a id="_CPPv219bk_psram_word_writePjj"></a> <a id="bk_psram_word_write__unsigned-iP.unsigned-i"></a> <a id="group__bk__api__psram_1ga6acdee0f1f504b22215b88daeb8d958c"></a> static inline void bk\_psram\_word\_write(unsigned int \*src, unsigned int value)
:   write one word of data to psram

    参数
    :   - **addr** – the psram address to write to
        - **value** – the value of one word of data

    返回
    :   - NULL

<a id="_CPPv420bk_psram_word_memcpyPvPvj"></a>

<a id="_CPPv320bk_psram_word_memcpyPvPvj"></a> <a id="_CPPv220bk_psram_word_memcpyPvPvj"></a> <a id="bk_psram_word_memcpy__voidP.voidP.unsigned-i"></a> <a id="group__bk__api__psram_1ga8e1659f68c60c8f88207c8f9cc4717a6"></a> static inline void bk\_psram\_word\_memcpy(void \*dst\_t, void \*src\_t, unsigned int length)
:   psram memory copy

    @attation 1\. length unit is byte

    参数
    :   - **dst\_t** – the destination address to be copied to
        - **src\_t** – the source address to be copied
        - **length** – length of the data copy

    返回
    :   - NULL

<a id="_CPPv427bk_psram_heap_init_flag_getv"></a>

<a id="_CPPv327bk_psram_heap_init_flag_getv"></a> <a id="_CPPv227bk_psram_heap_init_flag_getv"></a> <a id="bk_psram_heap_init_flag_get"></a> <a id="group__bk__api__psram_1ga519b93957e2ac717c0f322f2c091de9c"></a> bool bk\_psram\_heap\_init\_flag\_get()
:   get psram heap init flag

    This API to get psram heap init flag:

    - init: true:init ;false:uninit

    返回
    :   heap\_init\_flag

<a id="_CPPv427bk_psram_heap_init_flag_setb"></a>

<a id="_CPPv327bk_psram_heap_init_flag_setb"></a> <a id="_CPPv227bk_psram_heap_init_flag_setb"></a> <a id="bk_psram_heap_init_flag_set__b"></a> <a id="group__bk__api__psram_1ga9a16a6f7e90ef9d4516bf13445808b7a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_heap\_init\_flag\_set(bool init)
:   set psram heap init flag

    This API set psram heap init flag:

    - init: true:init;false:uninit

    This API should be called before using the psram heap.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_psram_id_auto_detectv"></a>

<a id="_CPPv323bk_psram_id_auto_detectv"></a> <a id="_CPPv223bk_psram_id_auto_detectv"></a> <a id="bk_psram_id_auto_detect__void"></a> <a id="group__bk__api__psram_1ga34977ee07b249e21fcc07ef206e04d8f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_id\_auto\_detect(void)
:   detect psram id

    This API get psram chip id from easy flash, if easy flash function enable

    This API should be called when chip boot, must before bk\_psram\_init.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv413bk_psram_initv"></a>

<a id="_CPPv313bk_psram_initv"></a> <a id="_CPPv213bk_psram_initv"></a> <a id="bk_psram_init__void"></a> <a id="group__bk__api__psram_1gabf47723a4eb610a6ceb7b3d441b8d6a5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_init(void)
:   Init the PSRAM HW.

    This API init the resoure common to all PSRAM:

    - Psram power up, configure the clock control register
    - Select a frequency multiple
    - Psram config

    This API should be called before any other PSRAM APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_psram_deinitv"></a>

<a id="_CPPv315bk_psram_deinitv"></a> <a id="_CPPv215bk_psram_deinitv"></a> <a id="bk_psram_deinit__void"></a> <a id="group__bk__api__psram_1ga6769383edf8fcb4123d7ff969df851ca"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_deinit(void)
:   Deinit the PSRAM HW.

    This API free the resoure common to PSRAM:

    - Init PSRAM HW control register
    - power down PSRAM voltage

    @attation 1\. after calling this function, this api bk\_psram\_resume can not enable psram function

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_psram_memcpyP7uint8_tP7uint8_t8uint32_t"></a>

<a id="_CPPv315bk_psram_memcpyP7uint8_tP7uint8_t8uint32_t"></a> <a id="_CPPv215bk_psram_memcpyP7uint8_tP7uint8_t8uint32_t"></a> <a id="bk_psram_memcpy__uint8_tP.uint8_tP.uint32_t"></a> <a id="group__bk__api__psram_1gaa70c908ba770d090ce95087ddd73d9ca"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_memcpy(uint8\_t \*start\_addr, uint8\_t \*data\_buf, uint32\_t len)
:   continue write data to psram

    This API will write more fast than dtim

    @attation 1\. len uint byte

    参数
    :   - **start\_addr** – write to psram start addr
        - **data\_buf** – data buffer pointer
        - **len** – data len need write to psram

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_psram_memreadP7uint8_tP7uint8_t8uint32_t"></a>

<a id="_CPPv316bk_psram_memreadP7uint8_tP7uint8_t8uint32_t"></a> <a id="_CPPv216bk_psram_memreadP7uint8_tP7uint8_t8uint32_t"></a> <a id="bk_psram_memread__uint8_tP.uint8_tP.uint32_t"></a> <a id="group__bk__api__psram_1gabeb636eb9c172acdadaac204d8cce29d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_memread(uint8\_t \*start\_addr, uint8\_t \*data\_buf, uint32\_t len)
:   continue read data from psram

    This API will read more fast than dtim

    @attation 1\. len uint byte

    参数
    :   - **start\_addr** – read from psram start addr
        - **data\_buf** – data buffer pointer
        - **len** – data len need read from psram

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_psram_set_clk11psram_clk_t"></a>

<a id="_CPPv316bk_psram_set_clk11psram_clk_t"></a> <a id="_CPPv216bk_psram_set_clk11psram_clk_t"></a> <a id="bk_psram_set_clk__psram_clk_t"></a> <a id="group__bk__api__psram_1gadfdc138226dd64b929ed71ec53ea9a91"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_set\_clk([psram\_clk\_t](#_CPPv411psram_clk_t "psram_clk_t") clk)
:   set psram clk

    This API used to set psram work clk

    参数
    :   **clk:80/120/160/240** – @attation 1\. current only support 80/120/160

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_psram_set_voltage15psram_voltage_t"></a>

<a id="_CPPv320bk_psram_set_voltage15psram_voltage_t"></a> <a id="_CPPv220bk_psram_set_voltage15psram_voltage_t"></a> <a id="bk_psram_set_voltage__psram_voltage_t"></a> <a id="group__bk__api__psram_1ga3dd01cee15959da9e0b186f0fb76b892"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_set\_voltage([psram\_voltage\_t](#_CPPv415psram_voltage_t "psram_voltage_t") voltage)
:   set psram voltage

    This API used to set psram work voltage

    @attation 1\. current only used 1.8v

    参数
    :   **voltage** – 1.8/2.0/3.0/3.2

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_psram_strcatPcPKc"></a>

<a id="_CPPv315bk_psram_strcatPcPKc"></a> <a id="_CPPv215bk_psram_strcatPcPKc"></a> <a id="bk_psram_strcat__cP.cCP"></a> <a id="group__bk__api__psram_1ga114707f125c071951fea3ad34acc2463"></a> char \*bk\_psram\_strcat(char \*start\_addr, const char \*data\_buf)
:   string cat to psram

    This API is like strcat

    参数
    :   - **start\_addr** – write to psram start addr
        - **data\_buf** – string buffer pointer

    返回
    :   psram start addr

<a id="_CPPv436bk_psram_alloc_write_through_channelv"></a>

<a id="_CPPv336bk_psram_alloc_write_through_channelv"></a> <a id="_CPPv236bk_psram_alloc_write_through_channelv"></a> <a id="bk_psram_alloc_write_through_channel__void"></a> <a id="group__bk__api__psram_1ga37738d5ca9c9b4dd7ae29962aa875df3"></a> [psram\_write\_through\_area\_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") bk\_psram\_alloc\_write\_through\_channel(void)
:   Allocate a write-through channel (area) from the default pool.

    Returns the next available area (0\~7) for configuring PSRAM write-through. Prefer [bk\_psram\_alloc\_write\_through\_channel\_with\_psram\_id()](#group__bk__api__psram_1ga119f58f6fca3b43c6d868398180e6820) when the buffer is known to lie in PSRAM0 or PSRAM1 so that the area matches the chip.

    返回
    :   Allocated area (PSRAM\_WRITE\_THROUGH\_AREA\_0 \~ \_AREA\_7), or PSRAM\_WRITE\_THROUGH\_AREA\_COUNT if no channel is available.

<a id="_CPPv450bk_psram_alloc_write_through_channel_with_psram_id7uint8_t"></a>

<a id="_CPPv350bk_psram_alloc_write_through_channel_with_psram_id7uint8_t"></a> <a id="_CPPv250bk_psram_alloc_write_through_channel_with_psram_id7uint8_t"></a> <a id="bk_psram_alloc_write_through_channel_with_psram_id__uint8_t"></a> <a id="group__bk__api__psram_1ga119f58f6fca3b43c6d868398180e6820"></a> [psram\_write\_through\_area\_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") bk\_psram\_alloc\_write\_through\_channel\_with\_psram\_id(uint8\_t psram\_id)
:   alloc write\_through\_area for specific PSRAM

    Use when buffer is in a known PSRAM: psram\_id 0 -\> returns area 0\~3, psram\_id 1 -\> returns area 4\~7.

    参数
    :   **psram\_id** – 0\=PSRAM0, 1\=PSRAM1

    返回
    :   allocated area (0\~7), or PSRAM\_WRITE\_THROUGH\_AREA\_COUNT on failure

<a id="_CPPv435bk_psram_free_write_through_channel26psram_write_through_area_t"></a>

<a id="_CPPv335bk_psram_free_write_through_channel26psram_write_through_area_t"></a> <a id="_CPPv235bk_psram_free_write_through_channel26psram_write_through_area_t"></a> <a id="bk_psram_free_write_through_channel__psram_write_through_area_t"></a> <a id="group__bk__api__psram_1ga7baa86b67f12e70d9c5e2a5979722c06"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_free\_write\_through\_channel([psram\_write\_through\_area\_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area)
:   free write\_through\_area

    This API is free a area

    - BK\_OK: succeed
    - BK\_ERR\_PSRAM\_ADDR\_ALIGN: start or end is not 32 bytes aligned
    - BK\_ERR\_PSRAM\_ADDR\_OUT\_OF\_RANGE: start or end is invalid PSRAM address
    - BK\_ERR\_PSRAM\_ADDR\_RELATION: start \>\= end
    - BK\_ERR\_PSRAM\_AREA: invalid area

    **Attention**
    :   1\. The write through area is used for DMA2D accessing only, do not use it for CPU accessing PSRAM

    返回

<a id="_CPPv429bk_psram_enable_write_through26psram_write_through_area_t8uint32_t8uint32_t"></a>

<a id="_CPPv329bk_psram_enable_write_through26psram_write_through_area_t8uint32_t8uint32_t"></a> <a id="_CPPv229bk_psram_enable_write_through26psram_write_through_area_t8uint32_t8uint32_t"></a> <a id="bk_psram_enable_write_through__psram_write_through_area_t.uint32_t.uint32_t"></a> <a id="group__bk__api__psram_1ga2e41d9ea3a8d5a8f3b40014eca5f1ac2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_enable\_write\_through([psram\_write\_through\_area\_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area, uint32\_t start, uint32\_t end)
:   Enable and config PSRAM write through area.

    This API enables PSRAM write through area. The PSRAM hardware will always flush it’s internal cache-line, without considering whether the cache line is full or not, thus to improve the writing performance.

    - BK\_OK: succeed
    - BK\_ERR\_PSRAM\_ADDR\_ALIGN: start or end is not 32 bytes aligned
    - BK\_ERR\_PSRAM\_ADDR\_OUT\_OF\_RANGE: start or end is invalid PSRAM address
    - BK\_ERR\_PSRAM\_ADDR\_RELATION: start \>\= end
    - BK\_ERR\_PSRAM\_AREA: invalid area

    **Attention**
    :   1\. The write through area must only one master access, and the write length must integer multiples 32bytes, you can write by cpu/dma/dma2d.

    参数
    :   - **area** – PSRAM write through area
        - **start** – PSRAM write through area start address, should be 32 bytes aligned
        - **start** – PSRAM write through area end address, should be 32 bytes aligned

    返回

<a id="_CPPv430bk_psram_disable_write_through26psram_write_through_area_t"></a>

<a id="_CPPv330bk_psram_disable_write_through26psram_write_through_area_t"></a> <a id="_CPPv230bk_psram_disable_write_through26psram_write_through_area_t"></a> <a id="bk_psram_disable_write_through__psram_write_through_area_t"></a> <a id="group__bk__api__psram_1ga16ef83bee4618bcd0e9eb42d629db4ff"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_disable\_write\_through([psram\_write\_through\_area\_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area)
:   Disable PSRAM write through area.

    - BK\_OK: succeed
    - BK\_ERR\_PSRAM\_AREA: invalid area

    参数
    :   **area** – PSRAM write through area id

    返回

<a id="_CPPv418bk_psram_calibratev"></a>

<a id="_CPPv318bk_psram_calibratev"></a> <a id="_CPPv218bk_psram_calibratev"></a> <a id="bk_psram_calibrate__void"></a> <a id="group__bk__api__psram_1gad69361ca64db4f781af5165b2a676295"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_psram\_calibrate(void)

<a id="psram-api-typedefs"></a>

## PSRAM API Typedefs

<a id="id1"></a>

### Header File

- [psram\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/psram_types.h)

<a id="macros"></a>

### Macros

<a id="c.PSRAM_CHIP_ID"></a>

<a id="psram__types_8h_1aba28d5367b34a45a8aaa44ea0fd3e7cb"></a> PSRAM\_CHIP\_ID

<a id="c.BK_ERR_PSRAM_SERVER_NOT_INIT"></a>

<a id="psram__types_8h_1a5ca10aca1ddc4dcd1402e0924ee1d82d"></a> BK\_ERR\_PSRAM\_SERVER\_NOT\_INIT
:   psram server not init

<a id="c.BK_ERR_PSRAM_ADDR_ALIGN"></a>

<a id="psram__types_8h_1a0ca45cc288a3f0834c545e3e327a0195"></a> BK\_ERR\_PSRAM\_ADDR\_ALIGN

<a id="c.BK_ERR_PSRAM_ADDR_OUT_OF_RANGE"></a>

<a id="psram__types_8h_1a2776eb5d25ad3b41d8571021c09f00e5"></a> BK\_ERR\_PSRAM\_ADDR\_OUT\_OF\_RANGE

<a id="c.BK_ERR_PSRAM_ADDR_RELATION"></a>

<a id="psram__types_8h_1aff83eadb874eb7d0bfe29e07a46571e5"></a> BK\_ERR\_PSRAM\_ADDR\_RELATION

<a id="c.BK_ERR_PSRAM_AREA"></a>

<a id="psram__types_8h_1aac6bfc301a7828c85856519ae0dcb0e8"></a> BK\_ERR\_PSRAM\_AREA

<a id="c.PSRAM_WRITE_THROUGH_AREA_PER_PSRAM"></a>

<a id="psram__types_8h_1a21633181de1bda9dfc464e573a36d948"></a> PSRAM\_WRITE\_THROUGH\_AREA\_PER\_PSRAM

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv411psram_clk_t"></a>

<a id="_CPPv311psram_clk_t"></a> <a id="_CPPv211psram_clk_t"></a> <a id="psram__types_8h_1ab1eeb4f9d8369e7491b38bfd17dc7815"></a> enum psram\_clk\_t
:   *Values:*

    <a id="_CPPv4N11psram_clk_t10PSRAM_240ME"></a>

    <a id="_CPPv3N11psram_clk_t10PSRAM_240ME"></a> <a id="_CPPv2N11psram_clk_t10PSRAM_240ME"></a> <a id="psram__types_8h_1ab1eeb4f9d8369e7491b38bfd17dc7815a1cec316efb81983fe3159a91edabc01f"></a> enumerator PSRAM\_240M

    <a id="_CPPv4N11psram_clk_t10PSRAM_160ME"></a>

    <a id="_CPPv3N11psram_clk_t10PSRAM_160ME"></a> <a id="_CPPv2N11psram_clk_t10PSRAM_160ME"></a> <a id="psram__types_8h_1ab1eeb4f9d8369e7491b38bfd17dc7815a0f44ae166875dbcfb8e79967ebae2437"></a> enumerator PSRAM\_160M

    <a id="_CPPv4N11psram_clk_t10PSRAM_120ME"></a>

    <a id="_CPPv3N11psram_clk_t10PSRAM_120ME"></a> <a id="_CPPv2N11psram_clk_t10PSRAM_120ME"></a> <a id="psram__types_8h_1ab1eeb4f9d8369e7491b38bfd17dc7815a9deb02033c8e6eca720222255641b03f"></a> enumerator PSRAM\_120M

    <a id="_CPPv4N11psram_clk_t9PSRAM_80ME"></a>

    <a id="_CPPv3N11psram_clk_t9PSRAM_80ME"></a> <a id="_CPPv2N11psram_clk_t9PSRAM_80ME"></a> <a id="psram__types_8h_1ab1eeb4f9d8369e7491b38bfd17dc7815a467d3c392b84ad1dcd75350ec83ddcc5"></a> enumerator PSRAM\_80M

<a id="_CPPv415psram_voltage_t"></a>

<a id="_CPPv315psram_voltage_t"></a> <a id="_CPPv215psram_voltage_t"></a> <a id="psram__types_8h_1a85ee86247dc1a82282e189d1e5008a39"></a> enum psram\_voltage\_t
:   *Values:*

    <a id="_CPPv4N15psram_voltage_t15PSRAM_OUT_3_20VE"></a>

    <a id="_CPPv3N15psram_voltage_t15PSRAM_OUT_3_20VE"></a> <a id="_CPPv2N15psram_voltage_t15PSRAM_OUT_3_20VE"></a> <a id="psram__types_8h_1a85ee86247dc1a82282e189d1e5008a39a3054ae2817e54a26f53b2076938c962f"></a> enumerator PSRAM\_OUT\_3\_20V

    <a id="_CPPv4N15psram_voltage_t14PSRAM_OUT_3_0VE"></a>

    <a id="_CPPv3N15psram_voltage_t14PSRAM_OUT_3_0VE"></a> <a id="_CPPv2N15psram_voltage_t14PSRAM_OUT_3_0VE"></a> <a id="psram__types_8h_1a85ee86247dc1a82282e189d1e5008a39a5c642ff1ab334c9e562f23d20e7c0378"></a> enumerator PSRAM\_OUT\_3\_0V

    <a id="_CPPv4N15psram_voltage_t14PSRAM_OUT_2_0VE"></a>

    <a id="_CPPv3N15psram_voltage_t14PSRAM_OUT_2_0VE"></a> <a id="_CPPv2N15psram_voltage_t14PSRAM_OUT_2_0VE"></a> <a id="psram__types_8h_1a85ee86247dc1a82282e189d1e5008a39abb07b6b79c7e496be5ab889e888f7e06"></a> enumerator PSRAM\_OUT\_2\_0V

    <a id="_CPPv4N15psram_voltage_t15PSRAM_OUT_1_95VE"></a>

    <a id="_CPPv3N15psram_voltage_t15PSRAM_OUT_1_95VE"></a> <a id="_CPPv2N15psram_voltage_t15PSRAM_OUT_1_95VE"></a> <a id="psram__types_8h_1a85ee86247dc1a82282e189d1e5008a39ae855678ad003d64418e9ce4a4636a705"></a> enumerator PSRAM\_OUT\_1\_95V

    <a id="_CPPv4N15psram_voltage_t15PSRAM_OUT_1_90VE"></a>

    <a id="_CPPv3N15psram_voltage_t15PSRAM_OUT_1_90VE"></a> <a id="_CPPv2N15psram_voltage_t15PSRAM_OUT_1_90VE"></a> <a id="psram__types_8h_1a85ee86247dc1a82282e189d1e5008a39a22cf1b30f5b5540430ef8250c753382e"></a> enumerator PSRAM\_OUT\_1\_90V

    <a id="_CPPv4N15psram_voltage_t15PSRAM_OUT_1_85VE"></a>

    <a id="_CPPv3N15psram_voltage_t15PSRAM_OUT_1_85VE"></a> <a id="_CPPv2N15psram_voltage_t15PSRAM_OUT_1_85VE"></a> <a id="psram__types_8h_1a85ee86247dc1a82282e189d1e5008a39ae60f16c6eb6279219bb5627fa74c5a66"></a> enumerator PSRAM\_OUT\_1\_85V

    <a id="_CPPv4N15psram_voltage_t15PSRAM_OUT_1_80VE"></a>

    <a id="_CPPv3N15psram_voltage_t15PSRAM_OUT_1_80VE"></a> <a id="_CPPv2N15psram_voltage_t15PSRAM_OUT_1_80VE"></a> <a id="psram__types_8h_1a85ee86247dc1a82282e189d1e5008a39ab5bc3c366bc069eedae0cf83344e80f6"></a> enumerator PSRAM\_OUT\_1\_80V

<a id="_CPPv420psram_tansfer_mode_t"></a>

<a id="_CPPv320psram_tansfer_mode_t"></a> <a id="_CPPv220psram_tansfer_mode_t"></a> <a id="psram__types_8h_1a66bdfd4cadb11fbae35d08333b165b59"></a> enum psram\_tansfer\_mode\_t
:   *Values:*

    <a id="_CPPv4N20psram_tansfer_mode_t19PSRAM_INCRASE_TRANSE"></a>

    <a id="_CPPv3N20psram_tansfer_mode_t19PSRAM_INCRASE_TRANSE"></a> <a id="_CPPv2N20psram_tansfer_mode_t19PSRAM_INCRASE_TRANSE"></a> <a id="psram__types_8h_1a66bdfd4cadb11fbae35d08333b165b59a4bb9a21656be55917e93026e982addb6"></a> enumerator PSRAM\_INCRASE\_TRANS

    <a id="_CPPv4N20psram_tansfer_mode_t18PSRAM_32_WORD_WRAPE"></a>

    <a id="_CPPv3N20psram_tansfer_mode_t18PSRAM_32_WORD_WRAPE"></a> <a id="_CPPv2N20psram_tansfer_mode_t18PSRAM_32_WORD_WRAPE"></a> <a id="psram__types_8h_1a66bdfd4cadb11fbae35d08333b165b59ae4e8ad787b4336175087a492da75af68"></a> enumerator PSRAM\_32\_WORD\_WRAP

    <a id="_CPPv4N20psram_tansfer_mode_t18PSRAM_64_WORD_WRAPE"></a>

    <a id="_CPPv3N20psram_tansfer_mode_t18PSRAM_64_WORD_WRAPE"></a> <a id="_CPPv2N20psram_tansfer_mode_t18PSRAM_64_WORD_WRAPE"></a> <a id="psram__types_8h_1a66bdfd4cadb11fbae35d08333b165b59ad1589bffb26975feeee3a914bd4d2f64"></a> enumerator PSRAM\_64\_WORD\_WRAP

    <a id="_CPPv4N20psram_tansfer_mode_t19PSRAM_128_WORD_WRAPE"></a>

    <a id="_CPPv3N20psram_tansfer_mode_t19PSRAM_128_WORD_WRAPE"></a> <a id="_CPPv2N20psram_tansfer_mode_t19PSRAM_128_WORD_WRAPE"></a> <a id="psram__types_8h_1a66bdfd4cadb11fbae35d08333b165b59a8903fc6106ce57d8e01ea99908bb9241"></a> enumerator PSRAM\_128\_WORD\_WRAP

    <a id="_CPPv4N20psram_tansfer_mode_t19PSRAM_256_WORD_WRAPE"></a>

    <a id="_CPPv3N20psram_tansfer_mode_t19PSRAM_256_WORD_WRAPE"></a> <a id="_CPPv2N20psram_tansfer_mode_t19PSRAM_256_WORD_WRAPE"></a> <a id="psram__types_8h_1a66bdfd4cadb11fbae35d08333b165b59aeed39d0977ad92a89ced9e38e247f45b"></a> enumerator PSRAM\_256\_WORD\_WRAP

    <a id="_CPPv4N20psram_tansfer_mode_t19PSRAM_512_WORD_WRAPE"></a>

    <a id="_CPPv3N20psram_tansfer_mode_t19PSRAM_512_WORD_WRAPE"></a> <a id="_CPPv2N20psram_tansfer_mode_t19PSRAM_512_WORD_WRAPE"></a> <a id="psram__types_8h_1a66bdfd4cadb11fbae35d08333b165b59a96dcb909e7c85e2e6035c813b999bfa1"></a> enumerator PSRAM\_512\_WORD\_WRAP

    <a id="_CPPv4N20psram_tansfer_mode_t20PSRAM_1024_WORD_WRAPE"></a>

    <a id="_CPPv3N20psram_tansfer_mode_t20PSRAM_1024_WORD_WRAPE"></a> <a id="_CPPv2N20psram_tansfer_mode_t20PSRAM_1024_WORD_WRAPE"></a> <a id="psram__types_8h_1a66bdfd4cadb11fbae35d08333b165b59a669b56b6bd868ac1909593f2b8261d3a"></a> enumerator PSRAM\_1024\_WORD\_WRAP

    <a id="_CPPv4N20psram_tansfer_mode_t20PSRAM_2048_WORD_WRAPE"></a>

    <a id="_CPPv3N20psram_tansfer_mode_t20PSRAM_2048_WORD_WRAPE"></a> <a id="_CPPv2N20psram_tansfer_mode_t20PSRAM_2048_WORD_WRAPE"></a> <a id="psram__types_8h_1a66bdfd4cadb11fbae35d08333b165b59a2287e5822f77a4138f30cef3a5108a5a"></a> enumerator PSRAM\_2048\_WORD\_WRAP

<a id="_CPPv426psram_write_through_area_t"></a>

<a id="_CPPv326psram_write_through_area_t"></a> <a id="_CPPv226psram_write_through_area_t"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7"></a> enum psram\_write\_through\_area\_t
:   *Values:*

    <a id="_CPPv4N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_0E"></a>

    <a id="_CPPv3N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_0E"></a> <a id="_CPPv2N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_0E"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7ad4a40b3609f9f8dac13100aff368915d"></a> enumerator PSRAM\_WRITE\_THROUGH\_AREA\_0

    <a id="_CPPv4N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_1E"></a>

    <a id="_CPPv3N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_1E"></a> <a id="_CPPv2N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_1E"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7a8930e8f190aadb21ed668532c49258c4"></a> enumerator PSRAM\_WRITE\_THROUGH\_AREA\_1

    <a id="_CPPv4N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_2E"></a>

    <a id="_CPPv3N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_2E"></a> <a id="_CPPv2N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_2E"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7ac727d886210928688ef2a5727baa90b7"></a> enumerator PSRAM\_WRITE\_THROUGH\_AREA\_2

    <a id="_CPPv4N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_3E"></a>

    <a id="_CPPv3N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_3E"></a> <a id="_CPPv2N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_3E"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7a2362be5ab7238cc5f06ef6dfcb6d7808"></a> enumerator PSRAM\_WRITE\_THROUGH\_AREA\_3

    <a id="_CPPv4N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_4E"></a>

    <a id="_CPPv3N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_4E"></a> <a id="_CPPv2N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_4E"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7a8f011d9ad25070351ce2b538bc1f18d2"></a> enumerator PSRAM\_WRITE\_THROUGH\_AREA\_4

    <a id="_CPPv4N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_5E"></a>

    <a id="_CPPv3N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_5E"></a> <a id="_CPPv2N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_5E"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7a990a2aea63c917015bb9eaaad7db446f"></a> enumerator PSRAM\_WRITE\_THROUGH\_AREA\_5

    <a id="_CPPv4N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_6E"></a>

    <a id="_CPPv3N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_6E"></a> <a id="_CPPv2N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_6E"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7a0cf235381e9586ca6ad84ea3c68483f4"></a> enumerator PSRAM\_WRITE\_THROUGH\_AREA\_6

    <a id="_CPPv4N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_7E"></a>

    <a id="_CPPv3N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_7E"></a> <a id="_CPPv2N26psram_write_through_area_t26PSRAM_WRITE_THROUGH_AREA_7E"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7ad9bf9a04eda2e450edcc40654fb07066"></a> enumerator PSRAM\_WRITE\_THROUGH\_AREA\_7

    <a id="_CPPv4N26psram_write_through_area_t30PSRAM_WRITE_THROUGH_AREA_COUNTE"></a>

    <a id="_CPPv3N26psram_write_through_area_t30PSRAM_WRITE_THROUGH_AREA_COUNTE"></a> <a id="_CPPv2N26psram_write_through_area_t30PSRAM_WRITE_THROUGH_AREA_COUNTE"></a> <a id="psram__types_8h_1a7e7200af0bffce18181fa1695bc6d0e7a3ddfebbd253c8e3e796ecb7ea3c85552"></a> enumerator PSRAM\_WRITE\_THROUGH\_AREA\_COUNT

备注

QSPI PSRAM 相关 API（`qspi_psram.h`）见 [QSPI API](bk_qspi.md)。
