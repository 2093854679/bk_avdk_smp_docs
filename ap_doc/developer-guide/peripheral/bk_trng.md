# 随机数 (RNG) 使用指南



## 概述

BK7259 已移除独立的 TRNG 外设驱动（`bk_trng_*` 系列 API 及 `driver/trng.h` 不再提供）。
系统随机数统一通过 `bk_rand()` 与 `bk_fill_rand()` 获取，定义于 `components/bk_platform.h`。

熵源由 PSA Mbed TLS 平台层在运行时选择，优先级如下：

1. TrustEngine TE200 硬件 TRNG（需开启 CONFIG_TRUSTENGINE 与 CONFIG_TE200_ENTROPY）
2. OTP 随机数（CONFIG_OTP_V1，未启用 TrustEngine 时）
3. 软件 `rand()` 回退（`components/bk_system/bk_platform.c` 中的 weak 实现）

更多 TrustEngine / Mbed TLS 配置说明见 [Mbed TLS](../security/mbedtls_and_trustengine.md "../security/mbedtls_and_trustengine.md")。


## 使用方法

获取 32 位随机整数:


```
#include <components/bk_platform.h>

int value = bk_rand();

```

填充缓冲区:


```
uint8_t buf[16];
if (bk_fill_rand(buf, sizeof(buf)) != 0) {
    /* buff 为 NULL 或 len 为 0 */
}

```

备注

启用 CONFIG_PSA_MBEDTLS 时，`bk_rand()` 与 `bk_fill_rand()` 由 PSA 平台层提供 strong 实现，覆盖 `bk_platform.c` 中的 weak 默认实现。系统启动后可直接调用，无需单独初始化 TRNG 外设。


## 推荐配置

密码学或安全相关场景建议开启:


```
CONFIG_PSA_MBEDTLS=y
CONFIG_TRUSTENGINE=y
CONFIG_TE200_ENTROPY=y

```
