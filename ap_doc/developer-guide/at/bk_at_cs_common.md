---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/at/bk_at_cs_common.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bk-idk-at"></a>

# **BK IDK AT 基础命令集**

重要

*BK-IDK 默认支持本节介绍的所有AT命令*

<a id="cs-common"></a>

- [AT](#at) :测试模组AT启动
- [AT\+RST](#reset) :模组重启
- [AT\+VERSION](#version) :获取模组固件版本
- [AT\+ATVERSION](#atversion) :获取模组固件AT版本
- [AT\+HELP](#help) : 查询当前AT支持的所有AT命令
- [AT\+WLMAC](#cs-mac) :获取STA身份和SAP身份的MAC地址，也可以配置MAC地址

<a id="at-at"></a>

<a id="at"></a>

## [AT](#cs-common) **:测试模组AT启动**

**命令说明**

```
该命令用于判断模组是否正常启动AT。
```

**查询命令**

```
无
```

**执行命令**

```
AT
```

**参数**

```
无
```

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 15s |

<a id="at-rst"></a>

<a id="reset"></a>

## [AT\+RST](#cs-common) **:模组重启**

**命令说明**

```
该命令用于重启模组。
```

**查询命令**

```
无
```

**执行命令**

```
AT+RST
```

**参数**

```
无
```

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 15s |

<a id="at-version"></a>

<a id="version"></a>

## [AT\+VERSION](#cs-common) **:获取模组固件版本**

**命令说明**

```
该命令用于获取模组固件版本。
```

**查询命令**

```
无
```

**执行命令**

```
AT+VERSION
```

**参数**

```
无
```

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 15s |

**示例**

```
AT+VERSION

EVT:version:Jul 10 2025 14:21:39

EVT:chip id:72360101

EVT:soc: bk7259

CMDRSP:OK
```

<a id="at-atversion-at"></a>

<a id="atversion"></a>

## [AT\+ATVERSION](#cs-common) **:获取模组固件AT版本**

**命令说明**

```
该命令用于获取模组固件AT版本。
```

**查询命令**

```
无
```

**执行命令**

```
AT+ATVERSION
```

**参数**

```
无
```

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 15s |

**示例**

```
AT+ATVERSION

EVT:AT-VERSION:2.0

CMDRSP:OK
```

<a id="at-help-atat"></a>

<a id="help"></a>

## [AT\+HELP](#cs-common) **:查询当前AT支持的所有AT命令**

**命令说明**

```
该命令用于查询当前AT支持的所有AT命令。
```

**查询命令**

```
无
```

**执行命令**

```
AT+HELP
```

**参数**

```
无
```

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 15s |

**示例**

```
AT+HELP

CMDRSP:cmd:AT,help:AT

......

CMDRSP:cmd:AT+BLEENABLEFUZZFEAT,help:enable fuzz feature

CMDRSP:cmd:AT+BLEOOBDATA,help:provide oob data received from peer:AT+BLEOOBDATA

CMDRSP:OK
```

<a id="at-wlmac-stasapmac"></a>

<a id="cs-mac"></a>

## [AT\+WLMAC](#cs-common) **:获取或配置STA身份和SAP身份的MAC地址**

**命令说明**

```
该命令用于获取或配置STA身份和SAP身份的MAC地址。
```

**查询命令**

```
无
```

**执行命令**

```
AT+WLMAC
AT+WLMAC=mac_addr(可选)
```

**参数**

```
无参数：获取当前设备的STA/SAP的MAC地址

mac_addr: 配置STA身份的MAC地址(可选)
```

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 15s |

**示例**

```
AT+WLMAC

base mac: c8:47:8c:0d:81:2d
sta mac: c8:47:8c:0d:81:2d
ap mac: c8:47:8c:0d:81:2c

CMDRSP:OK
```
