---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/audio/audio_development_kit/audio_utils/count_util.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="count-util"></a>

# Count Util

The Count util provides a method to count the amount of data processed by the component. It prints the processed data volume periodically using a timer for debugging purposes.

<a id="api-reference"></a>

## API Reference

<a id="header-file"></a>

### Header File

- [count\_util.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/components/bk_audio/audio_utils/count_util.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418count_util_destroyP12count_util_t"></a>

<a id="_CPPv318count_util_destroyP12count_util_t"></a> <a id="_CPPv218count_util_destroyP12count_util_t"></a> <a id="count_util_destroy__count_util_tP"></a> <a id="count__util_8h_1a7920e2c4dc3a766a49935b2c3cc50165"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") count\_util\_destroy([count\_util\_t](#_CPPv412count_util_t "count_util_t") \*count\_util)
:   Destroy a count util.

    参数
    :   **count\_util** – **\[in\]** The count util handle

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="_CPPv417count_util_createP12count_util_t8uint32_tPc"></a>

<a id="_CPPv317count_util_createP12count_util_t8uint32_tPc"></a> <a id="_CPPv217count_util_createP12count_util_t8uint32_tPc"></a> <a id="count_util_create__count_util_tP.uint32_t.cP"></a> <a id="count__util_8h_1a4cca43a92015fd2931595e12ed996469"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") count\_util\_create([count\_util\_t](#_CPPv412count_util_t "count_util_t") \*count\_util, uint32\_t interval, char \*tag)
:   Create a count util.

    参数
    :   - **count\_util** – **\[in\]** The count util handle
        - **interval** – **\[in\]** The timer interval(ms)
        - **tag** – **\[in\]** The printf tag

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="_CPPv419count_util_add_sizeP12count_util_t7int32_t"></a>

<a id="_CPPv319count_util_add_sizeP12count_util_t7int32_t"></a> <a id="_CPPv219count_util_add_sizeP12count_util_t7int32_t"></a> <a id="count_util_add_size__count_util_tP.int32_t"></a> <a id="count__util_8h_1a2bb7b08cd798d310215378f4f9ba6047"></a> void count\_util\_add\_size([count\_util\_t](#_CPPv412count_util_t "count_util_t") \*count\_util, int32\_t size)
:   Add data size to count util.

    参数
    :   - **count\_util** – **\[in\]** The count util handle
        - **size** – **\[in\]** The data size(bytes)

    返回
    :   None

<a id="_CPPv424count_util_multi_destroyP18count_util_multi_t"></a>

<a id="_CPPv324count_util_multi_destroyP18count_util_multi_t"></a> <a id="_CPPv224count_util_multi_destroyP18count_util_multi_t"></a> <a id="count_util_multi_destroy__count_util_multi_tP"></a> <a id="count__util_8h_1a76650bd04a5cc4ddeee73e0067a2d787"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") count\_util\_multi\_destroy([count\_util\_multi\_t](#_CPPv418count_util_multi_t "count_util_multi_t") \*count\_util)
:   Destroy a multi-parameter count util.

    参数
    :   **count\_util** – **\[in\]** The multi-parameter count util handle

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="_CPPv423count_util_multi_createP18count_util_multi_t8uint32_tPPc8uint32_t"></a>

<a id="_CPPv323count_util_multi_createP18count_util_multi_t8uint32_tPPc8uint32_t"></a> <a id="_CPPv223count_util_multi_createP18count_util_multi_t8uint32_tPPc8uint32_t"></a> <a id="count_util_multi_create__count_util_multi_tP.uint32_t.cPP.uint32_t"></a> <a id="count__util_8h_1ad4a6c2ad08402c1bc24d0a3403609c04"></a> [bk\_err\_t](../../../system/os.md#_CPPv48bk_err_t "bk_err_t") count\_util\_multi\_create([count\_util\_multi\_t](#_CPPv418count_util_multi_t "count_util_multi_t") \*count\_util, uint32\_t interval, char \*\*tags, uint32\_t param\_count)
:   Create a multi-parameter count util.

    备注

    The tags array should contain param\_count strings

    参数
    :   - **count\_util** – **\[in\]** The multi-parameter count util handle
        - **interval** – **\[in\]** The timer interval(ms)
        - **tags** – **\[in\]** The array of parameter tags
        - **param\_count** – **\[in\]** The number of parameters

    返回
    :   The result

        - BK\_OK: success
        - BK\_ERR: failed

<a id="_CPPv425count_util_multi_add_sizeP18count_util_multi_t8uint32_t7int32_t"></a>

<a id="_CPPv325count_util_multi_add_sizeP18count_util_multi_t8uint32_t7int32_t"></a> <a id="_CPPv225count_util_multi_add_sizeP18count_util_multi_t8uint32_t7int32_t"></a> <a id="count_util_multi_add_size__count_util_multi_tP.uint32_t.int32_t"></a> <a id="count__util_8h_1af9f541faed7fc5df14dca247415c21ab"></a> void count\_util\_multi\_add\_size([count\_util\_multi\_t](#_CPPv418count_util_multi_t "count_util_multi_t") \*count\_util, uint32\_t param\_index, int32\_t size)
:   Add data size to specific parameter in multi-parameter count util.

    参数
    :   - **count\_util** – **\[in\]** The multi-parameter count util handle
        - **param\_index** – **\[in\]** The parameter index (0 to param\_count-1)
        - **size** – **\[in\]** The data size(bytes)

    返回
    :   None

<a id="structures"></a>

### Structures

<a id="_CPPv412count_util_t"></a>

<a id="_CPPv312count_util_t"></a> <a id="_CPPv212count_util_t"></a> <a id="count_util_t"></a> <a id="structcount__util__t"></a> struct count\_util\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12count_util_t5timerE"></a>

    <a id="_CPPv3N12count_util_t5timerE"></a> <a id="_CPPv2N12count_util_t5timerE"></a> <a id="count_util_t::timer__beken_timer_t"></a> <a id="structcount__util__t_1ad6c6dcccebe91e82ade2007866f295c7"></a> [beken\_timer\_t](../../../system/os.md#_CPPv413beken_timer_t "beken_timer_t") timer
    :   freertos timer

    <a id="_CPPv4N12count_util_t14timer_intervalE"></a>

    <a id="_CPPv3N12count_util_t14timer_intervalE"></a> <a id="_CPPv2N12count_util_t14timer_intervalE"></a> <a id="count_util_t::timer_interval__uint32_t"></a> <a id="structcount__util__t_1a9349bd8f49410977c09b9b511e18b5ff"></a> uint32\_t timer\_interval
    :   timer interval(ms)

    <a id="_CPPv4N12count_util_t9data_sizeE"></a>

    <a id="_CPPv3N12count_util_t9data_sizeE"></a> <a id="_CPPv2N12count_util_t9data_sizeE"></a> <a id="count_util_t::data_size__uint32_t"></a> <a id="structcount__util__t_1a7304003abc99e34ac01770f94059ec9f"></a> uint32\_t data\_size
    :   total data size(bytes)

    <a id="_CPPv4N12count_util_t3tagE"></a>

    <a id="_CPPv3N12count_util_t3tagE"></a> <a id="_CPPv2N12count_util_t3tagE"></a> <a id="count_util_t::tag__cA"></a> <a id="structcount__util__t_1ab9d4f558ff71ed720094e1fa5c6bb040"></a> char tag\[20\]
    :   printf tag

<a id="_CPPv418count_util_param_t"></a>

<a id="_CPPv318count_util_param_t"></a> <a id="_CPPv218count_util_param_t"></a> <a id="count_util_param_t"></a> <a id="structcount__util__param__t"></a> struct count\_util\_param\_t
:   Multi-parameter item structure for count util.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18count_util_param_t3tagE"></a>

    <a id="_CPPv3N18count_util_param_t3tagE"></a> <a id="_CPPv2N18count_util_param_t3tagE"></a> <a id="count_util_param_t::tag__cA"></a> <a id="structcount__util__param__t_1a693155c3df3a5d1ff956fadf63126b36"></a> char tag\[20\]
    :   parameter tag

    <a id="_CPPv4N18count_util_param_t9data_sizeE"></a>

    <a id="_CPPv3N18count_util_param_t9data_sizeE"></a> <a id="_CPPv2N18count_util_param_t9data_sizeE"></a> <a id="count_util_param_t::data_size__uint32_t"></a> <a id="structcount__util__param__t_1ac58a88800e6be3e63269400b43390dda"></a> uint32\_t data\_size
    :   total data size(bytes)

<a id="_CPPv418count_util_multi_t"></a>

<a id="_CPPv318count_util_multi_t"></a> <a id="_CPPv218count_util_multi_t"></a> <a id="count_util_multi_t"></a> <a id="structcount__util__multi__t"></a> struct count\_util\_multi\_t
:   Multi-parameter count util structure.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18count_util_multi_t5timerE"></a>

    <a id="_CPPv3N18count_util_multi_t5timerE"></a> <a id="_CPPv2N18count_util_multi_t5timerE"></a> <a id="count_util_multi_t::timer__beken_timer_t"></a> <a id="structcount__util__multi__t_1ae95bf50d6d6f8cc1251c28222dc769f4"></a> [beken\_timer\_t](../../../system/os.md#_CPPv413beken_timer_t "beken_timer_t") timer
    :   freertos timer

    <a id="_CPPv4N18count_util_multi_t14timer_intervalE"></a>

    <a id="_CPPv3N18count_util_multi_t14timer_intervalE"></a> <a id="_CPPv2N18count_util_multi_t14timer_intervalE"></a> <a id="count_util_multi_t::timer_interval__uint32_t"></a> <a id="structcount__util__multi__t_1ace559af0973fc730ca1de03bee0da3fe"></a> uint32\_t timer\_interval
    :   timer interval(ms)

    <a id="_CPPv4N18count_util_multi_t6paramsE"></a>

    <a id="_CPPv3N18count_util_multi_t6paramsE"></a> <a id="_CPPv2N18count_util_multi_t6paramsE"></a> <a id="count_util_multi_t::params__count_util_param_tP"></a> <a id="structcount__util__multi__t_1a585eaf7ffa7136611b540e76aa148697"></a> [count\_util\_param\_t](#_CPPv418count_util_param_t "count_util_param_t") \*params
    :   parameters array

    <a id="_CPPv4N18count_util_multi_t11param_countE"></a>

    <a id="_CPPv3N18count_util_multi_t11param_countE"></a> <a id="_CPPv2N18count_util_multi_t11param_countE"></a> <a id="count_util_multi_t::param_count__uint32_t"></a> <a id="structcount__util__multi__t_1a2eb35e6fe3b1ed5d371f021e99f74149"></a> uint32\_t param\_count
    :   number of parameters
