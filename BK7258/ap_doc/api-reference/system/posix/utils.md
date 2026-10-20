---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/system/posix/utils.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="utils"></a>

# utils接口介绍

> - 需要包含头文件#include \<posix/utils.h\>;
> - 定义了posix公用的接口

<a id="header-file"></a>

## Header File

- [utils.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/posix/utils.h)

<a id="functions"></a>

## Functions

<a id="_CPPv413UTILS_strnlenPCKc6size_t"></a>

<a id="_CPPv313UTILS_strnlenPCKc6size_t"></a> <a id="_CPPv213UTILS_strnlenPCKc6size_t"></a> <a id="UTILS_strnlen__cCPC.s"></a> <a id="utils_8h_1ae1e06073e3115214a76205be6149d83a"></a> size\_t UTILS\_strnlen(const char \*const pcString, size\_t xMaxLength)
:   Calculates the length of pcString, up to xMaxLength.

    参数
    :   - **pcString** – **\[in\]** The string to find the length of.
        - **xMaxLength** – **\[in\]** The limit when searching for the end of pcString.

    返回
    :   0 if pcString is NULL; otherwise, the length of pcString or xMaxLength, whichever is smaller.

<a id="_CPPv434UTILS_AbsoluteTimespecToDeltaTicksPCK8timespecPCK8timespecPC10TickType_t"></a>

<a id="_CPPv334UTILS_AbsoluteTimespecToDeltaTicksPCK8timespecPCK8timespecPC10TickType_t"></a> <a id="_CPPv234UTILS_AbsoluteTimespecToDeltaTicksPCK8timespecPCK8timespecPC10TickType_t"></a> <a id="UTILS_AbsoluteTimespecToDeltaTicks__timespecCPC.timespecCPC.TickType_tPC"></a> <a id="utils_8h_1a858c841d9d8d7baed0ea06bb9ac31cb3"></a> int UTILS\_AbsoluteTimespecToDeltaTicks(const struct [timespec](time.md#_CPPv48timespec "timespec") \*const pxAbsoluteTime, const struct [timespec](time.md#_CPPv48timespec "timespec") \*const pxCurrentTime, TickType\_t \*const pxResult)
:   Calculates the number of ticks between now and a given timespec.

    参数
    :   - **pxAbsoluteTime** – **\[in\]** A time in the future, specified as seconds and nanoseconds since CLOCK\_REALTIME’s 0\.
        - **pxCurrentTime** – **\[in\]** current time, specified as seconds and nanoseconds.
        - **pxResult** – **\[out\]** Where the result of the conversion is stored. The result is rounded up for fractional ticks.

    返回
    :   0 on success. Otherwise, ETIMEDOUT if pxAbsoluteTime is in the past, or EINVAL for invalid parameters.

<a id="_CPPv421UTILS_TimespecToTicksPCK8timespecPC10TickType_t"></a>

<a id="_CPPv321UTILS_TimespecToTicksPCK8timespecPC10TickType_t"></a> <a id="_CPPv221UTILS_TimespecToTicksPCK8timespecPC10TickType_t"></a> <a id="UTILS_TimespecToTicks__timespecCPC.TickType_tPC"></a> <a id="utils_8h_1a5375610b0556953de42a89cd38c7ff3f"></a> int UTILS\_TimespecToTicks(const struct [timespec](time.md#_CPPv48timespec "timespec") \*const pxTimespec, TickType\_t \*const pxResult)
:   Converts a struct timespec to FreeRTOS ticks.

    参数
    :   - **pxTimespec** – **\[in\]** The timespec to convert.
        - **Where** – **\[out\]** the result of the conversion is stored. The result is rounded up for fractional ticks.

    返回
    :   0 on success. Otherwise, EINVAL for invalid parameters.

<a id="_CPPv427UTILS_NanosecondsToTimespec7int64_tPC8timespec"></a>

<a id="_CPPv327UTILS_NanosecondsToTimespec7int64_tPC8timespec"></a> <a id="_CPPv227UTILS_NanosecondsToTimespec7int64_tPC8timespec"></a> <a id="UTILS_NanosecondsToTimespec__int64_t.timespecPC"></a> <a id="utils_8h_1a470a49f37255ae6aabb10f7943a116e0"></a> void UTILS\_NanosecondsToTimespec(int64\_t llSource, struct [timespec](time.md#_CPPv48timespec "timespec") \*const pxDestination)
:   Converts an integer value to a timespec.

    参数
    :   - **llSource** – **\[in\]** The value to convert.
        - **pxDestination** – **\[out\]** Where to store the converted value.

    返回
    :   No return value.

<a id="_CPPv417UTILS_TimespecAddPCK8timespecPCK8timespecPC8timespec"></a>

<a id="_CPPv317UTILS_TimespecAddPCK8timespecPCK8timespecPC8timespec"></a> <a id="_CPPv217UTILS_TimespecAddPCK8timespecPCK8timespecPC8timespec"></a> <a id="UTILS_TimespecAdd__timespecCPC.timespecCPC.timespecPC"></a> <a id="utils_8h_1a296316a153cf3234bf48e0b268b29fcb"></a> int UTILS\_TimespecAdd(const struct [timespec](time.md#_CPPv48timespec "timespec") \*const x, const struct [timespec](time.md#_CPPv48timespec "timespec") \*const y, struct [timespec](time.md#_CPPv48timespec "timespec") \*const pxResult)
:   Calculates pxResult \= x \+ y.

    参数
    :   - **x** – **\[in\]** The first argument for addition.
        - **y** – **\[in\]** The second argument for addition.
        - **pxResult** – **\[out\]** Where the result of the calculation is stored.

    返回
    :   -1 if any argument was NULL; 1 if result is negative (overflow); otherwise, 0\.

<a id="_CPPv428UTILS_TimespecAddNanosecondsPCK8timespec7int64_tPC8timespec"></a>

<a id="_CPPv328UTILS_TimespecAddNanosecondsPCK8timespec7int64_tPC8timespec"></a> <a id="_CPPv228UTILS_TimespecAddNanosecondsPCK8timespec7int64_tPC8timespec"></a> <a id="UTILS_TimespecAddNanoseconds__timespecCPC.int64_t.timespecPC"></a> <a id="utils_8h_1a2183fc6650a802981f72c8765d1e231e"></a> int UTILS\_TimespecAddNanoseconds(const struct [timespec](time.md#_CPPv48timespec "timespec") \*const x, int64\_t llNanoseconds, struct [timespec](time.md#_CPPv48timespec "timespec") \*const pxResult)
:   Calculates pxResult \= x \+ ( struct timespec ) nanosec.

    参数
    :   - **x** – **\[in\]** The first argument for addition.
        - **llNanoseconds** – **\[in\]** The second argument for addition.
        - **pxResult** – **\[out\]** Where the result of the calculation is stored.

    返回
    :   -1 if pxResult or x was NULL; 1 if result is negative; otherwise, 0\.

<a id="_CPPv422UTILS_TimespecSubtractPCK8timespecPCK8timespecPC8timespec"></a>

<a id="_CPPv322UTILS_TimespecSubtractPCK8timespecPCK8timespecPC8timespec"></a> <a id="_CPPv222UTILS_TimespecSubtractPCK8timespecPCK8timespecPC8timespec"></a> <a id="UTILS_TimespecSubtract__timespecCPC.timespecCPC.timespecPC"></a> <a id="utils_8h_1a3d3fce8c0d895a6006d7cb06a26f2b84"></a> int UTILS\_TimespecSubtract(const struct [timespec](time.md#_CPPv48timespec "timespec") \*const x, const struct [timespec](time.md#_CPPv48timespec "timespec") \*const y, struct [timespec](time.md#_CPPv48timespec "timespec") \*const pxResult)
:   Calculates pxResult \= x \- y. If the result is negative contents of pResult are undefined.

    参数
    :   - **x** – **\[in\]** The first argument for subtraction.
        - **y** – **\[in\]** The second argument for subtraction.
        - **pxResult** – **\[out\]** Where the result of the calculation is stored.

    返回
    :   -1 if any argument was NULL; 1 if result is negative; otherwise, 0\.

<a id="_CPPv421UTILS_TimespecComparePCK8timespecPCK8timespec"></a>

<a id="_CPPv321UTILS_TimespecComparePCK8timespecPCK8timespec"></a> <a id="_CPPv221UTILS_TimespecComparePCK8timespecPCK8timespec"></a> <a id="UTILS_TimespecCompare__timespecCPC.timespecCPC"></a> <a id="utils_8h_1aa91f0c25033f0a2abed4d7ba63fddbf8"></a> int UTILS\_TimespecCompare(const struct [timespec](time.md#_CPPv48timespec "timespec") \*const x, const struct [timespec](time.md#_CPPv48timespec "timespec") \*const y)
:   Compare x \=\= y.

    参数
    :   - **x** – **\[in\]** The first argument for comparison.
        - **y** – **\[in\]** The second argument for comparison.

    返回
    :   0 if x \=\= y; 1 if x \> y; -1 if x \< y or any argument was NULL

<a id="_CPPv422UTILS_ValidateTimespecPCK8timespec"></a>

<a id="_CPPv322UTILS_ValidateTimespecPCK8timespec"></a> <a id="_CPPv222UTILS_ValidateTimespecPCK8timespec"></a> <a id="UTILS_ValidateTimespec__timespecCPC"></a> <a id="utils_8h_1a4ad9c68fd0045c8e4bbdb45e6810232e"></a> bool UTILS\_ValidateTimespec(const struct [timespec](time.md#_CPPv48timespec "timespec") \*const pxTimespec)
:   Checks that a timespec conforms to POSIX.

    A valid timespec must have 0 \<\= tv\_nsec \< 1000000000.

    参数
    :   **pxTimespec** – **\[in\]** The timespec to validate.

    返回
    :   true if the pxTimespec is valid, false otherwise.
