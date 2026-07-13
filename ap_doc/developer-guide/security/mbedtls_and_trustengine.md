# Mbed TLS



## 概述

MbedTLS是一个适用于嵌入式系统的算法库，主要实现基础加密算法、X.509证书操作、SSL/TLS和DTLDS协议。


## MbedTLS版本

当前支持版本为：3.6.6


## MbedTLS介绍

[API Reference](https://mbed-tls.readthedocs.io/projects/api/en/v3.6.6/ "https://mbed-tls.readthedocs.io/projects/api/en/v3.6.6/")

[KnowledgeBase](https://mbed-tls.readthedocs.io/en/latest/kb/ "https://mbed-tls.readthedocs.io/en/latest/kb/")


## TE200（TrustEngine-200）介绍

BK7259采用了TE200（TrustEngine-200）作为硬件加速引擎，提供下述安全特性：

> - 高度安全保障。TE200 支持密钥阶梯、生命周期管理和真随机数发生器（TRNG），以提升系统的安全性。
> - 高性能和低功耗的加密/解密操作。这是通过 TE200 内部的加密引擎实现的。
> - 减少安全方面的软件复杂性。TE200 实现了一些安全功能，如生命周期管理。


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

- CONFIG_TRUSTENGINE_TEST             #支持经典MbedTLS API及性能测试

```


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

备注

默认配置为关闭硬件加速、使用纯软件加密（CONFIG_TRUSTENGINE=n、CONFIG_SW_CRYPTO=y）。


### 关闭MbedTLS

CONFIG_PSA_MBEDTLS 为 MbedTLS 总开关，置 n 即关闭整个 MbedTLS 组件，其下所有子选项（TRUSTENGINE/SW_CRYPTO/MBEDTLS_USE_PSA_CRYPTO/FULL_MBEDTLS 等）随之失效：


```
CONFIG_PSA_MBEDTLS=n

```


### 关闭硬件加速配置

关闭硬件加速时使用纯软件加密，CONFIG_TE200_ENTROPY 依赖 CONFIG_TRUSTENGINE，必须同时关闭：


```
CONFIG_TRUSTENGINE=n
CONFIG_SW_CRYPTO=y
CONFIG_TE200_ENTROPY=n

```


### 开启硬件加速配置


```
CONFIG_TRUSTENGINE=y
CONFIG_SW_CRYPTO=n

```

重要


*Note：TrustEngine已对MbedTLS API做了适配，CONFIG_TRUSTENGINE=y开启硬件加速后上层应用调用的mbedtls API保持不变;
开启硬件加速后会增加codesize;
TrustEngine只能运行在AP或者CP单侧，不能同时开启硬件加速*


### MbedTLS算法配置文件


```
components\psa_mbedtls\mbedtls_port\configs\mbedtls_psa_crypto_config.h

```
