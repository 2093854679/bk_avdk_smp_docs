# utils接口介绍

> - 需要包含头文件#include <posix/utils.h>;
> - 定义了posix公用的接口



## Header File


- [utils.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/utils.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/utils.h")


## Functions

size_t UTILS_strnlen(const char *const pcString, size_t xMaxLength)
:   Calculates the length of pcString, up to xMaxLength.

    参数
    :   - **pcString** – **[in]** The string to find the length of.

        - **xMaxLength** – **[in]** The limit when searching for the end of pcString.

    返回
    :   0 if pcString is NULL; otherwise, the length of pcString or xMaxLength, whichever is smaller.

int UTILS_AbsoluteTimespecToDeltaTicks(const struct [timespec](time.md#_CPPv48timespec "timespec") *const pxAbsoluteTime, const struct [timespec](time.md#_CPPv48timespec "timespec") *const pxCurrentTime, TickType_t *const pxResult)
:   Calculates the number of ticks between now and a given timespec.

    参数
    :   - **pxAbsoluteTime** – **[in]** A time in the future, specified as seconds and nanoseconds since CLOCK_REALTIME’s 0.

        - **pxCurrentTime** – **[in]** current time, specified as seconds and nanoseconds.

        - **pxResult** – **[out]** Where the result of the conversion is stored. The result is rounded up for fractional ticks.

    返回
    :   0 on success. Otherwise, ETIMEDOUT if pxAbsoluteTime is in the past, or EINVAL for invalid parameters.

int UTILS_TimespecToTicks(const struct [timespec](time.md#_CPPv48timespec "timespec") *const pxTimespec, TickType_t *const pxResult)
:   Converts a struct timespec to FreeRTOS ticks.

    参数
    :   - **pxTimespec** – **[in]** The timespec to convert.

        - **Where** – **[out]** the result of the conversion is stored. The result is rounded up for fractional ticks.

    返回
    :   0 on success. Otherwise, EINVAL for invalid parameters.

void UTILS_NanosecondsToTimespec(int64_t llSource, struct [timespec](time.md#_CPPv48timespec "timespec") *const pxDestination)
:   Converts an integer value to a timespec.

    参数
    :   - **llSource** – **[in]** The value to convert.

        - **pxDestination** – **[out]** Where to store the converted value.

    返回
    :   No return value.

int UTILS_TimespecAdd(const struct [timespec](time.md#_CPPv48timespec "timespec") *const x, const struct [timespec](time.md#_CPPv48timespec "timespec") *const y, struct [timespec](time.md#_CPPv48timespec "timespec") *const pxResult)
:   Calculates pxResult = x + y.

    参数
    :   - **x** – **[in]** The first argument for addition.

        - **y** – **[in]** The second argument for addition.

        - **pxResult** – **[out]** Where the result of the calculation is stored.

    返回
    :   -1 if any argument was NULL; 1 if result is negative (overflow); otherwise, 0.

int UTILS_TimespecAddNanoseconds(const struct [timespec](time.md#_CPPv48timespec "timespec") *const x, int64_t llNanoseconds, struct [timespec](time.md#_CPPv48timespec "timespec") *const pxResult)
:   Calculates pxResult = x + ( struct timespec ) nanosec.

    参数
    :   - **x** – **[in]** The first argument for addition.

        - **llNanoseconds** – **[in]** The second argument for addition.

        - **pxResult** – **[out]** Where the result of the calculation is stored.

    返回
    :   -1 if pxResult or x was NULL; 1 if result is negative; otherwise, 0.

int UTILS_TimespecSubtract(const struct [timespec](time.md#_CPPv48timespec "timespec") *const x, const struct [timespec](time.md#_CPPv48timespec "timespec") *const y, struct [timespec](time.md#_CPPv48timespec "timespec") *const pxResult)
:   Calculates pxResult = x - y. If the result is negative contents of pResult are undefined.

    参数
    :   - **x** – **[in]** The first argument for subtraction.

        - **y** – **[in]** The second argument for subtraction.

        - **pxResult** – **[out]** Where the result of the calculation is stored.

    返回
    :   -1 if any argument was NULL; 1 if result is negative; otherwise, 0.

int UTILS_TimespecCompare(const struct [timespec](time.md#_CPPv48timespec "timespec") *const x, const struct [timespec](time.md#_CPPv48timespec "timespec") *const y)
:   Compare x == y.

    参数
    :   - **x** – **[in]** The first argument for comparison.

        - **y** – **[in]** The second argument for comparison.

    返回
    :   0 if x == y; 1 if x > y; -1 if x < y or any argument was NULL

bool UTILS_ValidateTimespec(const struct [timespec](time.md#_CPPv48timespec "timespec") *const pxTimespec)
:   Checks that a timespec conforms to POSIX.

    A valid timespec must have 0 <= tv_nsec < 1000000000.

    参数
    :   **pxTimespec** – **[in]** The timespec to validate.

    返回
    :   true if the pxTimespec is valid, false otherwise.
