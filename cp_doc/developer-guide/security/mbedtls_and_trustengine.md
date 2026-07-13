# Mbed TLS



## 概述

MbedTLS是一个适用于嵌入式系统的算法库，主要实现基础加密算法、X.509证书操作、SSL/TLS和DTLDS协议。


## MbedTLS版本

当前支持版本为：3.6.6


## MbedTLS介绍

[API Reference](https://mbed-tls.readthedocs.io/projects/api/en/v3.6.6/ "https://mbed-tls.readthedocs.io/projects/api/en/v3.6.6/")

[KnowledgeBase](https://mbed-tls.readthedocs.io/en/latest/kb/ "https://mbed-tls.readthedocs.io/en/latest/kb/")


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

- CONFIG_TRUSTENGINE_TEST             #支持MbedTLS API及性能测试

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


### 关闭硬件加速配置（纯软件）

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


*Note：TrustEngine只能运行在一个cpu上，当前默认在AP上可开启硬件加速*


### MbedTLS算法配置文件


```
components\psa_mbedtls\mbedtls_port\configs\mbedtls_psa_crypto_config.h

```
