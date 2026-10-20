---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_efuse.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="efuse"></a>

# EFUSE

<a id="efuse-api-status"></a>

## EFUSE API Status

| API | BK7259\_AP |
| --- | --- |
| [`bk_efuse_driver_init()`](#_CPPv420bk_efuse_driver_initv "bk_efuse_driver_init") | Y |
| [`bk_efuse_driver_deinit()`](#_CPPv422bk_efuse_driver_deinitv "bk_efuse_driver_deinit") | Y |
| `bk_efuse_write()` | Y |
| `bk_efuse_read()` | Y |

<a id="efuse-api-reference"></a>

## Efuse API Reference

<a id="header-file"></a>

### Header File

- [efuse.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/efuse.h)

<a id="functions"></a>

### Functions

<a id="_CPPv420bk_efuse_driver_initv"></a>

<a id="_CPPv320bk_efuse_driver_initv"></a> <a id="_CPPv220bk_efuse_driver_initv"></a> <a id="bk_efuse_driver_init__void"></a> <a id="group__bk__api__efuse_1gaca4213e74a531c83a14ec2290a8a29d5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_efuse\_driver\_init(void)
:   Init the EFUSE driver.

    This API init the resoure common:

    - Init EFUSE driver control memory

    **Attention**
    :   1\. This API should be called before any other EFUSE APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_efuse_driver_deinitv"></a>

<a id="_CPPv322bk_efuse_driver_deinitv"></a> <a id="_CPPv222bk_efuse_driver_deinitv"></a> <a id="bk_efuse_driver_deinit__void"></a> <a id="group__bk__api__efuse_1gae5d373abe937e574ca3ae5ee17538ccd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_efuse\_driver\_deinit(void)
:   Deinit the EFUSE driver.

    This API free all resource related to EFUSE and disable EFUSE.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_efuse_write_byte7uint8_t7uint8_t"></a>

<a id="_CPPv319bk_efuse_write_byte7uint8_t7uint8_t"></a> <a id="_CPPv219bk_efuse_write_byte7uint8_t7uint8_t"></a> <a id="bk_efuse_write_byte__uint8_t.uint8_t"></a> <a id="group__bk__api__efuse_1gad3755868c50c91559d775b6f49879183"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_efuse\_write\_byte(uint8\_t addr, uint8\_t data)
:   Efuse write operation @Notice: Each efuse address area has specific usage, please apply the area from PM before write data to the efuse address.

    参数
    :   - **addr** – efuse write address
        - **data** – efuse write data

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_EFUSE\_DRIVER\_NOT\_INIT: EFUSE driver not init
        - BK\_ERR\_EFUSE\_ADDR\_OUT\_OF\_RANGE: EFUSE address is out of range
        - BK\_ERR\_EFUSE\_CANNOT\_WRTIE: EFUSE cannot write, cannot change bit from 1 to 0
        - BK\_ERR\_EFUSE\_WRTIE\_NOT\_EQUAL: EFUSE data read is not equal to the data written
        - others: other errors.

<a id="_CPPv418bk_efuse_read_byte7uint8_tP7uint8_t"></a>

<a id="_CPPv318bk_efuse_read_byte7uint8_tP7uint8_t"></a> <a id="_CPPv218bk_efuse_read_byte7uint8_tP7uint8_t"></a> <a id="bk_efuse_read_byte__uint8_t.uint8_tP"></a> <a id="group__bk__api__efuse_1ga1d4dfa52478e2cdedc3ae5f9a467c0d3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_efuse\_read\_byte(uint8\_t addr, uint8\_t \*data)
:   Efuse read operation.

    参数
    :   - **addr** – read address
        - **data** – pointer to accept value of efuse read data

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_EFUSE\_DRIVER\_NOT\_INIT: EFUSE driver not init
        - BK\_ERR\_EFUSE\_ADDR\_OUT\_OF\_RANGE: EFUSE address is out of range
        - others: other errors.

<a id="efuse-api-typedefs"></a>

## Efuse API Typedefs

<a id="id1"></a>

### Header File

- [efuse\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/efuse_types.h)

<a id="id2"></a>

### Header File

- [hal\_efuse\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_efuse_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_EFUSE_DRIVER_NOT_INIT"></a>

<a id="group__bk__api__efuse__defs_1ga76f876fae3d7a12a8eca49ba84faa85c"></a> BK\_ERR\_EFUSE\_DRIVER\_NOT\_INIT
:   EFUSE driver not init

<a id="c.BK_ERR_EFUSE_ADDR_OUT_OF_RANGE"></a>

<a id="group__bk__api__efuse__defs_1ga9e5dbc9c4de3ddeec48409259aa09d67"></a> BK\_ERR\_EFUSE\_ADDR\_OUT\_OF\_RANGE
:   EFUSE address is out of range

<a id="c.BK_ERR_EFUSE_CANNOT_WRTIE"></a>

<a id="group__bk__api__efuse__defs_1ga7a3950f4bb11971ca1a7a0fc7d2becf1"></a> BK\_ERR\_EFUSE\_CANNOT\_WRTIE
:   EFUSE cannot write, cannot change bit from 1 to 0

<a id="c.BK_ERR_EFUSE_WRTIE_NOT_EQUAL"></a>

<a id="group__bk__api__efuse__defs_1gaede874f0c778d95a182b935756d59108"></a> BK\_ERR\_EFUSE\_WRTIE\_NOT\_EQUAL
:   EFUSE data read is not equal to the data written

<a id="c.BK_ERR_EFUSE_READ_FAIL"></a>

<a id="group__bk__api__efuse__defs_1gabdeda2eeb6c85149121c1898567d1730"></a> BK\_ERR\_EFUSE\_READ\_FAIL
:   EFUSE data read fail

<a id="c.EFUSE_ADDR_BYTE0"></a>

<a id="group__bk__api__efuse__defs_1ga1b97dec5d2ab93da1418c70acf84a842"></a> EFUSE\_ADDR\_BYTE0
:   efuse address defines @Notice: Each efuse address area has specific usage, please apply the area from PM before write data to the efuse address.

<a id="c.EFUSE_ADDR_BYTE1"></a>

<a id="group__bk__api__efuse__defs_1ga8240d4135a802811ef6ab7c93551b1ec"></a> EFUSE\_ADDR\_BYTE1

<a id="c.EFUSE_ADDR_BYTE2"></a>

<a id="group__bk__api__efuse__defs_1ga28ae9eb25bb6dd57d9ddbf30de56569f"></a> EFUSE\_ADDR\_BYTE2

<a id="c.EFUSE_ADDR_BYTE3"></a>

<a id="group__bk__api__efuse__defs_1gac97ed3ed1845dcbcfa85715711e103e7"></a> EFUSE\_ADDR\_BYTE3

<a id="c.EFUSE_ADDR_BYTE4"></a>

<a id="group__bk__api__efuse__defs_1ga4a254bcc122b5bd37c8e8964fc93a6ab"></a> EFUSE\_ADDR\_BYTE4

<a id="c.EFUSE_ADDR_BYTE5"></a>

<a id="group__bk__api__efuse__defs_1gae9ceb70fa3766f16477fe42109affff7"></a> EFUSE\_ADDR\_BYTE5

<a id="c.EFUSE_ADDR_BYTE6"></a>

<a id="group__bk__api__efuse__defs_1gaf75f6a8acacc285191071f3b8ed747f7"></a> EFUSE\_ADDR\_BYTE6

<a id="c.EFUSE_ADDR_BYTE7"></a>

<a id="group__bk__api__efuse__defs_1ga23c6e40701b3fcb1b7b5d8f882c27ff9"></a> EFUSE\_ADDR\_BYTE7

<a id="c.EFUSE_ADDR_BYTE8"></a>

<a id="group__bk__api__efuse__defs_1ga0b64217e8b0cc5d1e3c98411431fa682"></a> EFUSE\_ADDR\_BYTE8

<a id="c.EFUSE_ADDR_BYTE9"></a>

<a id="group__bk__api__efuse__defs_1ga0fc484f2d8c0866ac765c97b604ba37f"></a> EFUSE\_ADDR\_BYTE9

<a id="c.EFUSE_ADDR_BYTE10"></a>

<a id="group__bk__api__efuse__defs_1ga44b18a9ec4560b64973e22ed2a24c901"></a> EFUSE\_ADDR\_BYTE10

<a id="c.EFUSE_ADDR_BYTE11"></a>

<a id="group__bk__api__efuse__defs_1ga921456ad6f56851c85b6b153ab7e399e"></a> EFUSE\_ADDR\_BYTE11

<a id="c.EFUSE_ADDR_BYTE12"></a>

<a id="group__bk__api__efuse__defs_1ga798ddc95316db7ce8cb04820d20f8117"></a> EFUSE\_ADDR\_BYTE12

<a id="c.EFUSE_ADDR_BYTE13"></a>

<a id="group__bk__api__efuse__defs_1ga437d578c5670e183d2b90d3c41428407"></a> EFUSE\_ADDR\_BYTE13

<a id="c.EFUSE_ADDR_BYTE14"></a>

<a id="group__bk__api__efuse__defs_1gafec982e101213550570f0c9f88371164"></a> EFUSE\_ADDR\_BYTE14

<a id="c.EFUSE_ADDR_BYTE15"></a>

<a id="group__bk__api__efuse__defs_1gad3657233253cffa5ac9e2105854cf149"></a> EFUSE\_ADDR\_BYTE15

<a id="c.EFUSE_ADDR_BYTE16"></a>

<a id="group__bk__api__efuse__defs_1gaa7349081779a6b8af4ac7e5b4145d72b"></a> EFUSE\_ADDR\_BYTE16

<a id="c.EFUSE_ADDR_BYTE17"></a>

<a id="group__bk__api__efuse__defs_1gae3b61e1f34c84c2381458b80887761de"></a> EFUSE\_ADDR\_BYTE17

<a id="c.EFUSE_ADDR_BYTE18"></a>

<a id="group__bk__api__efuse__defs_1gaacf0c6c17415141cd74ea94f2d0f56a9"></a> EFUSE\_ADDR\_BYTE18

<a id="c.EFUSE_ADDR_BYTE19"></a>

<a id="group__bk__api__efuse__defs_1gafd4792c9bdd77a0f2a1709e835f986ce"></a> EFUSE\_ADDR\_BYTE19

<a id="c.EFUSE_ADDR_BYTE20"></a>

<a id="group__bk__api__efuse__defs_1ga6b6ab9ecc7c81b5850dbfb8101d87b96"></a> EFUSE\_ADDR\_BYTE20

<a id="c.EFUSE_ADDR_BYTE21"></a>

<a id="group__bk__api__efuse__defs_1ga5d21b221daffb1bb7eecae4ccbbefa73"></a> EFUSE\_ADDR\_BYTE21

<a id="c.EFUSE_ADDR_BYTE22"></a>

<a id="group__bk__api__efuse__defs_1ga0d3ae47156007cf284b7e9354ca8fc0a"></a> EFUSE\_ADDR\_BYTE22

<a id="c.EFUSE_ADDR_BYTE23"></a>

<a id="group__bk__api__efuse__defs_1gaa4bb96e24a7c817706b42514f8bb70b1"></a> EFUSE\_ADDR\_BYTE23

<a id="c.EFUSE_ADDR_BYTE24"></a>

<a id="group__bk__api__efuse__defs_1ga9cd34434711a2c1f0e8824c85a7f6441"></a> EFUSE\_ADDR\_BYTE24

<a id="c.EFUSE_ADDR_BYTE25"></a>

<a id="group__bk__api__efuse__defs_1ga10565a2d160a57eb619bd75568782101"></a> EFUSE\_ADDR\_BYTE25

<a id="c.EFUSE_ADDR_BYTE26"></a>

<a id="group__bk__api__efuse__defs_1gadc26db7329bc73957747713eb287e373"></a> EFUSE\_ADDR\_BYTE26

<a id="c.EFUSE_ADDR_BYTE27"></a>

<a id="group__bk__api__efuse__defs_1ga7d13f02e3e32434757cd4902fdf1a5ef"></a> EFUSE\_ADDR\_BYTE27

<a id="c.EFUSE_ADDR_BYTE28"></a>

<a id="group__bk__api__efuse__defs_1ga816158a3bab1a0f9677eb8039c8747da"></a> EFUSE\_ADDR\_BYTE28

<a id="c.EFUSE_ADDR_BYTE29"></a>

<a id="group__bk__api__efuse__defs_1ga2673d5530fbf06c7ebc3904624cfb3dc"></a> EFUSE\_ADDR\_BYTE29

<a id="c.EFUSE_ADDR_BYTE30"></a>

<a id="group__bk__api__efuse__defs_1gac4729f479f18807d6ab94f9ec15b5a22"></a> EFUSE\_ADDR\_BYTE30

<a id="c.EFUSE_ADDR_BYTE31"></a>

<a id="group__bk__api__efuse__defs_1gabc1e8c6bef6b15ffe74fd6cc83dbe3ec"></a> EFUSE\_ADDR\_BYTE31

<a id="c.EFUSE_DEVICE_ID_BYTE_NUM"></a>

<a id="group__bk__api__efuse__defs_1ga68a11f22d7b04fad2d1c57bda5f208ba"></a> EFUSE\_DEVICE\_ID\_BYTE\_NUM
:   efuse device id defines OTP2 device id (BK7259 / OTP v1) is 8 bytes, read/written via the OTP2 AHB path. (Legacy raw-efuse device id on older parts is 5 bytes at efuse address 0x18 \~ 0x1c.) the efuse device id is set via ate cmds

<a id="c.EFUSE_DEVICE_ID_SN_MINIMUM"></a>

<a id="group__bk__api__efuse__defs_1ga3430ac7983c89fda1737d3d950cb95f2"></a> EFUSE\_DEVICE\_ID\_SN\_MINIMUM

<a id="c.EFUSE_DEVICE_ID_SN_MAXIMUM"></a>

<a id="group__bk__api__efuse__defs_1gaf3defd5a22760005316193fa7dde00f2"></a> EFUSE\_DEVICE\_ID\_SN\_MAXIMUM

<a id="c.EFUSE_WAFER_ID_MINIMUM"></a>

<a id="group__bk__api__efuse__defs_1ga555b306456685f180810f226230e7ae2"></a> EFUSE\_WAFER\_ID\_MINIMUM

<a id="c.EFUSE_WAFER_ID_MAXIMUM"></a>

<a id="group__bk__api__efuse__defs_1ga80dafd8c6a224bda227f63782b1c4a71"></a> EFUSE\_WAFER\_ID\_MAXIMUM

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv412efuse_unit_t"></a>

<a id="_CPPv312efuse_unit_t"></a> <a id="_CPPv212efuse_unit_t"></a> <a id="efuse_unit_t"></a> <a id="group__bk__api__efuse__defs_1ga2cd5c530432bebdc339e0d9446002563"></a> typedef uint8\_t efuse\_unit\_t
:   efuse uint id
