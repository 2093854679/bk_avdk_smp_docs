---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/security/mbedtls_and_trustengine.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
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

当前支持版本为：3.5.2

<a id="id2"></a>

## MbedTLS介绍

[API Reference](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/security/mbed-tls.readthedocs.io/projects/api/en/v3.5.2/)

[KnowledgeBase](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/security/mbed-tls.readthedocs.io/en/latest/kb/)

<a id="id3"></a>

## 相关宏说明

```
- CONFIG_FULL_MBEDTLS                 #对MbedTLS进行裁剪，关闭后可优化codesize
- CONFIG_PSA_MBEDTLS                  #支持MbedTLS V3.5.2
- CONFIG_MBEDTLS_USE_PSA_CRYPTO       #tls协议支持PSA API
- CONFIG_TRUSTENGINE                  #支持硬件加速，开启后codesize会增加
- CONFIG_SW_CRYPTO                    #支持纯软件实现，与CONFIG_TRUSTENGINE互斥
- CONFIG_TE200_ENTROPY                #支持TrustEngine随机数熵源
- CONFIG_MBEDTLS_LOG_LEVEL="OFF"      #设置MbedTLS调试log等级（OFF/ERROR/WARNING/INFO/DEBUG）
- CONFIG_PSA_MBEDTLS_TEST             #支持PSA API测试
- CONFIG_TRUSTENGINE_TEST             #支持MbedTLS API及性能测试
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
CONFIG_TRUSTENGINE_TEST=n
```

重要

*Note：TrustEngine只能运行在一个cpu上，当前默认在AP上可开启硬件加速*

<a id="id4"></a>

### MbedTLS算法配置文件

```
components\psa_mbedtls\mbedtls_port\configs\mbedtls_psa_crypto_config.h
```
