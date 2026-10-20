---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/security/mbedtls_and_trustengine.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
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

<a id="te200-trustengine-200"></a>

## TE200（TrustEngine-200）介绍

BK7259采用了TE200（TrustEngine-200）作为硬件加速引擎，提供下述安全特性：

> - 高度安全保障。TE200 支持密钥阶梯、生命周期管理和真随机数发生器（TRNG），以提升系统的安全性。
> - 高性能和低功耗的加密/解密操作。这是通过 TE200 内部的加密引擎实现的。
> - 减少安全方面的软件复杂性。TE200 实现了一些安全功能，如生命周期管理。

<a id="te200"></a>

### TE200 功能

TE200 支持下述特性：

> - 对称加密算法：AES-ECB/CBC/CTR/CBC-MAC/CMAC/CCM/GCM（密钥长度为128位、192位和256位）。
> - 对称加密算法：SM4-ECB/CBC/CTR/CBC-MAC/CMAC/CCM/GCM。
> - 散列算法：SHA1/224/256。
> - 散列算法：SM3。
> - 非对称加密算法：RSA 1024/2048/3072/4096 和 ECCP 192/224/256/384/512/521。
> - 非对称加密算法：SM2。
> - 密钥阶梯用于密钥管理。
> - 生命周期管理。
> - 真随机数发生器。
> - 一次性编程（OTP）。

它符合以下标准：

> - FIPS PUB 180-4：安全散列标准（SHS）
> - FIPS PUB 197：高级加密标准（AES）
> - NIST SP 800-38A：块密码工作模式的推荐方法和技术
> - NIST SP 800-38B：块密码工作模式协议——用于认证的CMAC模式
> - NIST SP 800-38C：块密码工作模式协议——用于认证和保密的CCM模式
> - NIST SP 800-38D：块密码工作模式协议——Galois/Counter Mode（GCM）和GMAC
> - NIST SP 800-90B：用于随机比特生成的熵源协议
> - GB/T 32918-2016：SM2椭圆曲线公钥密码算法
> - GB/T 32905-2016：SM3密码散列算法
> - GB/T 32907-2016：SM4块密码算法

其中：SM2公钥密码、SM3密码散列算法和SM4块密码算法是中国国家标准。

<a id="id3"></a>

## 相关宏说明

```
- CONFIG_FULL_MBEDTLS                 #MbedTLS算法裁剪开关，关闭(裁剪)后可优化codesize
- CONFIG_PSA_MBEDTLS                  #MbedTLS总开关(支持V3.6.6)，置n则关闭整个MbedTLS组件及其下所有子选项
- CONFIG_MBEDTLS_USE_PSA_CRYPTO       #tls协议支持PSA API，默认关闭该功能，仅支持经典mbedtls api
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

### 关闭硬件加速配置

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

*Note：TrustEngine已对MbedTLS API做了适配，CONFIG\_TRUSTENGINE\=y开启硬件加速后上层应用调用的mbedtls API保持不变;
开启硬件加速后会增加codesize;
TrustEngine只能运行在AP或者CP单侧，不能同时开启硬件加速*

重要

OTP 与硬件加速器（TrustEngine）共用同一个电源域。因此无论在 CP 侧还是 AP 侧，
只要开启了 CONFIG\_OTP\_V1，若同时再开启 CONFIG\_TRUSTENGINE，则必须和 CONFIG\_OTP\_V1 一起同时开启 CONFIG\_AON\_ENCP。

原因：未开启 CONFIG\_AON\_ENCP 时，OTP 每次访问结束后会直接掉电（deinit），
这会一并关断该共享电源域，导致硬件加速器无法正常工作；开启 CONFIG\_AON\_ENCP 后，
OTP 访问结束改为休眠（sleep）而非掉电，从而保证共享电源域持续供电，硬件加速器可正常运行。

<a id="id7"></a>

### MbedTLS算法配置文件

```
components\psa_mbedtls\mbedtls_port\configs\mbedtls_psa_crypto_config.h
```
