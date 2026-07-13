# **BK IDK AT 基础命令集**


重要


*BK-IDK 默认支持本节介绍的所有AT命令*


- [AT](#at "#at") :测试模组AT启动

- [AT+RST](#reset "#reset") :模组重启

- [AT+VERSION](#version "#version") :获取模组固件版本

- [AT+ATVERSION](#atversion "#atversion") :获取模组固件AT版本

- [AT+HELP](#help "#help") : 查询当前AT支持的所有AT命令

- [AT+WLMAC](#cs-mac "#cs-mac") :获取STA身份和SAP身份的MAC地址，也可以配置MAC地址


## [AT](#cs-common "#cs-common") **:测试模组AT启动**


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


## [AT+RST](#cs-common "#cs-common") **:模组重启**


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


## [AT+VERSION](#cs-common "#cs-common") **:获取模组固件版本**


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


## [AT+ATVERSION](#cs-common "#cs-common") **:获取模组固件AT版本**


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


## [AT+HELP](#cs-common "#cs-common") **:查询当前AT支持的所有AT命令**


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


## [AT+WLMAC](#cs-common "#cs-common") **:获取或配置STA身份和SAP身份的MAC地址**


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
