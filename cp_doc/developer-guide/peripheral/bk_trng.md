# 随机数 (RNG) 使用指南



## 概述

BK7259 已移除独立的 TRNG 外设驱动（`bk_trng_*` API 及 `driver/trng.h` 不再提供）。
系统随机数统一通过 `bk_rand()` 与 `bk_fill_rand()` 获取，定义于 `components/bk_platform.h`。

熵源由 PSA Mbed TLS 平台层在运行时选择：TrustEngine TE200 硬件 TRNG、OTP 随机数，或软件 `rand()` 回退。


## 使用方法

> - 获取随机整数：调用 `bk_rand()`
> - 填充随机字节：调用 `bk_fill_rand(buff, len)`

备注

启用 `CONFIG_PSA_MBEDTLS=y` 时，上述接口由 PSA 平台层提供 strong 实现，无需单独初始化 TRNG 外设。


## 推荐配置

安全相关场景建议开启 `CONFIG_PSA_MBEDTLS`、`CONFIG_TRUSTENGINE` 与 `CONFIG_TE200_ENTROPY`。
