---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_otp.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="otp"></a>

# OTP

BK7259 AP 侧 OTP API（`include/driver/otp.h`）。详细说明见
[OTP 开发指南](../../developer-guide/peripheral/bk_otp.md)。

<a id="otp-api-reference"></a>

## OTP API Reference

<a id="header-file"></a>

### Header File

- [otp.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/otp.h)

<a id="functions"></a>

### Functions

<a id="_CPPv411bk_otp_initv"></a>

<a id="_CPPv311bk_otp_initv"></a> <a id="_CPPv211bk_otp_initv"></a> <a id="bk_otp_init__void"></a> <a id="otp_8h_1ae522f946c99f1feec8a9df087e9e59d9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_otp\_init(void)

<a id="_CPPv413bk_otp_deinitv"></a>

<a id="_CPPv313bk_otp_deinitv"></a> <a id="_CPPv213bk_otp_deinitv"></a> <a id="bk_otp_deinit__void"></a> <a id="otp_8h_1ab339b618bfb770e540dd627a0c225f3b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_otp\_deinit(void)
:   OTP finalization.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv427bk_otp_read_bytes_nonsecureP7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv327bk_otp_read_bytes_nonsecureP7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv227bk_otp_read_bytes_nonsecureP7uint8_t8uint32_t8uint32_t"></a> <a id="bk_otp_read_bytes_nonsecure__uint8_tP.uint32_t.uint32_t"></a> <a id="group__bk__api__otp_1gab58d38855b06b459f5ce367a93504726"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_otp\_read\_bytes\_nonsecure(uint8\_t \*buffer, uint32\_t addr, uint32\_t len)
:   OTP read operation.

    **Attention**
    :   1\. addr\+len should be less than 0x800

    **Attention**
    :   2\. this API can only access non-secure OTP bank

    **Attention**
    :   3\. this api blocks for 5ms waiting for OTP to stabilize

    参数
    :   - **buffer** – point to the buffer that reads the data
        - **addr** – read address, address range 0x0\&#8212;0x800
        - **len** – read length

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_EFUSE\_DRIVER\_NOT\_INIT: EFUSE driver not init
        - BK\_ERR\_EFUSE\_ADDR\_OUT\_OF\_RANGE: EFUSE address is out of range
        - others: other errors.

<a id="_CPPv425bk_otp_apb_read_by_offset8uint32_tP7uint8_t8uint32_t"></a>

<a id="_CPPv325bk_otp_apb_read_by_offset8uint32_tP7uint8_t8uint32_t"></a> <a id="_CPPv225bk_otp_apb_read_by_offset8uint32_tP7uint8_t8uint32_t"></a> <a id="bk_otp_apb_read_by_offset__uint32_t.uint8_tP.uint32_t"></a> <a id="otp_8h_1accde87870742c67a063dd31f99bd886c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_otp\_apb\_read\_by\_offset(uint32\_t item\_offset, uint8\_t \*buf, uint32\_t size)
:   OTP read with item real offset.

    参数
    :   - **item\_offset** – the real item offset to read from otp
        - **buf** – point to the buffer that reads the data
        - **size** – length of item to read

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NO\_READ\_PERMISSION: wrong permission to read
        - BK\_ERR\_OTP\_ADDR\_OUT\_OF\_RANGE: param size not match item real size
        - others: other errors.

<a id="_CPPv425bk_otp_ahb_read_by_offset8uint32_tP7uint8_t8uint32_t"></a>

<a id="_CPPv325bk_otp_ahb_read_by_offset8uint32_tP7uint8_t8uint32_t"></a> <a id="_CPPv225bk_otp_ahb_read_by_offset8uint32_tP7uint8_t8uint32_t"></a> <a id="bk_otp_ahb_read_by_offset__uint32_t.uint8_tP.uint32_t"></a> <a id="otp_8h_1a60123a3406cc0bdd2ad97f5421cf241d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_otp\_ahb\_read\_by\_offset(uint32\_t item\_offset, uint8\_t \*buf, uint32\_t size)
:   OTP2 read with item real offset.

    参数
    :   - **item\_offset** – the real item offset to read from otp2
        - **buf** – point to the buffer that reads the data
        - **size** – length of item to read

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="otp-api-typedefs"></a>

## OTP API Typedefs

<a id="id1"></a>

### Header File

- [otp\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/otp_types.h)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv412otp_status_t"></a>

<a id="_CPPv312otp_status_t"></a> <a id="_CPPv212otp_status_t"></a> <a id="otp__types_8h_1a9f6249ec413ca338e313ab62277d3c33"></a> enum otp\_status\_t
:   *Values:*

    <a id="_CPPv4N12otp_status_t8OTP_BUSYE"></a>

    <a id="_CPPv3N12otp_status_t8OTP_BUSYE"></a> <a id="_CPPv2N12otp_status_t8OTP_BUSYE"></a> <a id="otp__types_8h_1a9f6249ec413ca338e313ab62277d3c33a5c9d82f66f5eb0f03ec07d5d3e70fd90"></a> enumerator OTP\_BUSY

    <a id="_CPPv4N12otp_status_t9OTP_ERRORE"></a>

    <a id="_CPPv3N12otp_status_t9OTP_ERRORE"></a> <a id="_CPPv2N12otp_status_t9OTP_ERRORE"></a> <a id="otp__types_8h_1a9f6249ec413ca338e313ab62277d3c33a9195f0574a9b7d5a6611eb54a19823f0"></a> enumerator OTP\_ERROR

    <a id="_CPPv4N12otp_status_t11OTP_WARNINGE"></a>

    <a id="_CPPv3N12otp_status_t11OTP_WARNINGE"></a> <a id="_CPPv2N12otp_status_t11OTP_WARNINGE"></a> <a id="otp__types_8h_1a9f6249ec413ca338e313ab62277d3c33ab7a73f540337fa83c4864b22f9c696c8"></a> enumerator OTP\_WARNING

    <a id="_CPPv4N12otp_status_t9OTP_WRONGE"></a>

    <a id="_CPPv3N12otp_status_t9OTP_WRONGE"></a> <a id="_CPPv2N12otp_status_t9OTP_WRONGE"></a> <a id="otp__types_8h_1a9f6249ec413ca338e313ab62277d3c33a443154fcd38ac21dbf06e44b8a2cdc10"></a> enumerator OTP\_WRONG

    <a id="_CPPv4N12otp_status_t10OTP_FORBIDE"></a>

    <a id="_CPPv3N12otp_status_t10OTP_FORBIDE"></a> <a id="_CPPv2N12otp_status_t10OTP_FORBIDE"></a> <a id="otp__types_8h_1a9f6249ec413ca338e313ab62277d3c33a61f717875aa2d60b9523bb1c176e32af"></a> enumerator OTP\_FORBID

<a id="id2"></a>

### Header File

- [hal\_otp\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_otp_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_OTP_READ_BUFFER_NULL"></a>

<a id="group__bk__api__otp__defs_1ga34eabd469de5eb16b11feac5304f7dc4"></a> BK\_ERR\_OTP\_READ\_BUFFER\_NULL
:   The pointed buff is NULL

<a id="c.BK_ERR_OTP_ADDR_OUT_OF_RANGE"></a>

<a id="group__bk__api__otp__defs_1ga1116a21845e799f79d7be9262cd0f1c1"></a> BK\_ERR\_OTP\_ADDR\_OUT\_OF\_RANGE
:   OTP address is out of range

<a id="c.BK_ERR_NO_READ_PERMISSION"></a>

<a id="group__bk__api__otp__defs_1gab5d0b4137fb2d548ba78ee556eb49a86"></a> BK\_ERR\_NO\_READ\_PERMISSION
:   Not have read privilege

<a id="c.BK_ERR_NO_WRITE_PERMISSION"></a>

<a id="group__bk__api__otp__defs_1ga269a95f00829201c8b059186b6e906bb"></a> BK\_ERR\_NO\_WRITE\_PERMISSION
:   Not have write privilege

<a id="c.BK_ERR_OTP_PERMISSION_WRONG"></a>

<a id="group__bk__api__otp__defs_1ga08b97acbc8414ae763ac353d0943d6f1"></a> BK\_ERR\_OTP\_PERMISSION\_WRONG
:   OTP permission value error

<a id="c.BK_ERR_OTP_NOT_EMPTY"></a>

<a id="group__bk__api__otp__defs_1gafe1d3d52ebe3e67188f1d03f185d94e7"></a> BK\_ERR\_OTP\_NOT\_EMPTY
:   try to write area already has value

<a id="c.BK_ERR_OTP_UPDATE_NOT_EQUAL"></a>

<a id="group__bk__api__otp__defs_1ga9d5a3b00c9b500135f687237b7289ecf"></a> BK\_ERR\_OTP\_UPDATE\_NOT\_EQUAL
:   after update not equal to expected

<a id="c.BK_ERR_OTP_OPERATION_ERROR"></a>

<a id="group__bk__api__otp__defs_1ga06a42b9c333417c249257179db17e443"></a> BK\_ERR\_OTP\_OPERATION\_ERROR
:   otp operation error

<a id="c.BK_ERR_OTP_OPERATION_WARNING"></a>

<a id="group__bk__api__otp__defs_1gab82c7d51a5ebd996a0b31aed7e27b620"></a> BK\_ERR\_OTP\_OPERATION\_WARNING
:   otp operation warning

<a id="c.BK_ERR_OTP_OPERATION_WRONG"></a>

<a id="group__bk__api__otp__defs_1ga5337785c7eeb5281750b40f966494608"></a> BK\_ERR\_OTP\_OPERATION\_WRONG
:   otp operation wrong

<a id="c.BK_ERR_OTP_OPERATION_FORBID"></a>

<a id="group__bk__api__otp__defs_1ga408beda6f3153d69f4cee4a0dfa1db0a"></a> BK\_ERR\_OTP\_OPERATION\_FORBID
:   otp operation forbid

<a id="c.BK_ERR_OTP_OPERATION_FAIL"></a>

<a id="group__bk__api__otp__defs_1gae39ee7f621e1559df939d3cbbdc4d614"></a> BK\_ERR\_OTP\_OPERATION\_FAIL

<a id="c.BK_ERR_OTP_INIT_FAIL"></a>

<a id="group__bk__api__otp__defs_1gaf179fa5bdc72248bf1da6fccb461ddcb"></a> BK\_ERR\_OTP\_INIT\_FAIL

<a id="c.BK_ERR_OTP_INDEX_WRONG"></a>

<a id="group__bk__api__otp__defs_1ga70fb42a3faeff462e8b651390d6560d0"></a> BK\_ERR\_OTP\_INDEX\_WRONG
:   OTP item index error

<a id="c.BK_ERR_OTP_OPERATION_ERROR_MASK"></a>

<a id="group__bk__api__otp__defs_1ga30710a0cbc089e1220e48b5c32df0367"></a> BK\_ERR\_OTP\_OPERATION\_ERROR\_MASK

<a id="c.BK_ERR_OTP_OPERATION_FAIL_MASK"></a>

<a id="group__bk__api__otp__defs_1gab481493e6b9e3c1dcbb19343ef207a6d"></a> BK\_ERR\_OTP\_OPERATION\_FAIL\_MASK

<a id="c.BK_ERR_OTP_INIT_FAIL_MASK"></a>

<a id="group__bk__api__otp__defs_1gac45e80b1e287d801fd99e27f248b4efc"></a> BK\_ERR\_OTP\_INIT\_FAIL\_MASK

<a id="c.BK_ERR_OTP_FULL_ERROR_MASK"></a>

<a id="group__bk__api__otp__defs_1gaa2f5bd731dc72fd449f4ff3570b58f37"></a> BK\_ERR\_OTP\_FULL\_ERROR\_MASK

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410otp_unit_t"></a>

<a id="_CPPv310otp_unit_t"></a> <a id="_CPPv210otp_unit_t"></a> <a id="otp_unit_t"></a> <a id="group__bk__api__otp__defs_1ga1486636abbfe984723523a30b3e5db99"></a> typedef uint8\_t otp\_unit\_t
:   otp uint id
