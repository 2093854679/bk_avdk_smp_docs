---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/security/mbedtls_and_trustengine.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="mbed-tls"></a>

# Mbed TLS

<a id="id1"></a>

## 概述

MbedTLS是一个适用于嵌入式系统的算法库，主要实现基础加密算法、X.509证书操作、SSL/TLS和DTLDS协议。

<a id="mbedtls"></a>

## MbedTLS版本

当前支持版本为：3.6.6

<a id="id2"></a>

## MbedTLS介绍

[API Reference](https://mbed-tls.readthedocs.io/projects/api/en/v3.6.6/)

[KnowledgeBase](https://mbed-tls.readthedocs.io/en/latest/kb/)

<a id="id3"></a>

## 相关宏说明

```
- CONFIG_FULL_MBEDTLS                 #MbedTLS算法裁剪开关，关闭(裁剪)后可优化codesize
- CONFIG_PSA_MBEDTLS                  #MbedTLS总开关(支持V3.6.6)，置n则关闭整个MbedTLS组件及其下所有子选项
- CONFIG_MBEDTLS_USE_PSA_CRYPTO       #TLS/X.509 及应用使用 PSA Crypto API，默认关闭该功能，仅支持经典mbedtls api
- CONFIG_TFM_CRYPTO                   #选择 PSA Crypto API 服务提供方：y 为安全世界，n 为非安全镜像内的本地服务端
- CONFIG_TRUSTENGINE                  #硬件加速开关，默认关闭；开启后codesize会增加，且与CONFIG_SW_CRYPTO互斥
- CONFIG_SW_CRYPTO                    #纯软件实现开关，默认开启，与CONFIG_TRUSTENGINE互斥(关闭硬件加速时使用)
- CONFIG_TE200_ENTROPY                #支持TrustEngine随机数熵源
- CONFIG_MBEDTLS_LOG_LEVEL="OFF"      #设置MbedTLS调试log等级（OFF/ERROR/WARNING/INFO/DEBUG）
- CONFIG_PSA_MBEDTLS_TEST             #支持PSA API测试
- CONFIG_CLASSIC_MBEDTLS_TEST         #支持经典MbedTLS API的软件/硬件测试
```

<a id="project"></a>

### project默认配置

```
CONFIG_FULL_MBEDTLS=n
CONFIG_PSA_MBEDTLS=y
CONFIG_MBEDTLS_USE_PSA_CRYPTO=n
CONFIG_TRUSTENGINE=n
CONFIG_SW_CRYPTO=y
CONFIG_TE200_ENTROPY=n
CONFIG_MBEDTLS_LOG_LEVEL="OFF"
CONFIG_PSA_MBEDTLS_TEST=n
CONFIG_CLASSIC_MBEDTLS_TEST=n
```

备注

默认配置为关闭硬件加速、使用纯软件加密（CONFIG\_TRUSTENGINE\=n、CONFIG\_SW\_CRYPTO\=y）。

<a id="id4"></a>

### 关闭MbedTLS

CONFIG\_PSA\_MBEDTLS 为 MbedTLS 总开关，置 n 即关闭整个 MbedTLS 组件，其下所有子选项（TRUSTENGINE/SW\_CRYPTO/MBEDTLS\_USE\_PSA\_CRYPTO/FULL\_MBEDTLS 等）随之失效：

```
CONFIG_PSA_MBEDTLS=n
```

<a id="id5"></a>

### 关闭硬件加速配置（纯软件）

关闭硬件加速时使用纯软件加密，CONFIG\_TE200\_ENTROPY 依赖 CONFIG\_TRUSTENGINE，必须同时关闭：

```
CONFIG_TRUSTENGINE=n
CONFIG_SW_CRYPTO=y
CONFIG_TE200_ENTROPY=n
```

<a id="id6"></a>

### 开启硬件加速配置

```
CONFIG_TRUSTENGINE=y
CONFIG_SW_CRYPTO=n
```

重要

*Note：TrustEngine只能运行在一个cpu上，当前默认在AP上可开启硬件加速*

重要

OTP 与硬件加速器（TrustEngine）共用同一个电源域。因此无论在 CP 侧还是 AP 侧，
只要开启了 CONFIG\_OTP\_V1，若同时再开启 CONFIG\_TRUSTENGINE，则必须和和 CONFIG\_OTP\_V1一起同时开启CONFIG\_AON\_ENCP。

原因：未开启 CONFIG\_AON\_ENCP 时，OTP 每次访问结束后会直接掉电（deinit），
这会一并关断该共享电源域，导致硬件加速器无法正常工作；开启 CONFIG\_AON\_ENCP 后，
OTP 访问结束改为休眠（sleep）而非掉电，从而保证共享电源域持续供电，硬件加速器可正常运行。

<a id="psa-crypto-api"></a>

### 安全工程的 PSA Crypto API 配置

在安全工程上，PSA Crypto API 是否可用、由哪一侧实现，由两个开关共同决定。

CONFIG\_MBEDTLS\_USE\_PSA\_CRYPTO 用于为 TLS/X.509 及应用代码启用 PSA Crypto API，它只依赖
CONFIG\_PSA\_MBEDTLS，因此在不运行 TF-M 的工程上同样可以开启。该开关关闭时只存在经典
mbedtls API，PSA CLI 测试也无法选择。

CONFIG\_TFM\_CRYPTO 进一步决定非安全侧看到的 PSA 服务提供方：

| CONFIG\_TFM\_CRYPTO | PSA 服务提供方 | 非安全侧构建 | 算法集配置文件 |
| --- | --- | --- | --- |
| y | 安全世界的加密服务，经 PSA client（IPC/veneer）访问 | 仅 MBEDTLS\_PSA\_CRYPTO\_CLIENT，不含本地服务端 | components/tfm/mbedcrypto\_config/crypto\_config\_psa.h |
| n | 链接进非安全镜像的本地 PSA 服务端 | MBEDTLS\_PSA\_CRYPTO\_C 与 MBEDTLS\_PSA\_CRYPTO\_CLIENT | components/psa\_mbedtls/mbedtls\_port/configs/mbedtls\_psa\_crypto\_config.h |

经典 mbedtls API 不受这两个开关影响，它始终运行在非安全侧，后端由 CONFIG\_TRUSTENGINE /
CONFIG\_SW\_CRYPTO 选择。所以工程可以同时使用硬件加速的经典 API 和由安全世界提供的 PSA API。

安全工程上的典型组合：

```
# PSA API 由安全世界提供
CONFIG_PSA_MBEDTLS=y
CONFIG_MBEDTLS_USE_PSA_CRYPTO=y
CONFIG_TFM_CRYPTO=y

# PSA API 由非安全镜像本地提供
CONFIG_PSA_MBEDTLS=y
CONFIG_MBEDTLS_USE_PSA_CRYPTO=y
# CONFIG_TFM_CRYPTO is not set
```

<a id="id7"></a>

### MbedTLS算法配置文件

```
components\psa_mbedtls\mbedtls_port\configs\mbedtls_psa_crypto_config.h
```

安全世界加密服务的算法集单独配置：

```
components\tfm\mbedcrypto_config\crypto_config_psa.h
```
