---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/at/bk_at_cs_wifi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bk-idk-at-wi-fi"></a>

<a id="cs-wifi-at"></a>

# **BK IDK AT Wi-Fi命令**

重要

*BK-IDK 默认支持本节介绍的所有 AT 命令*

*除非特定指定，Wi-Fi AT 命令的超时时间均为 15s*

BK7259 SMP

SMP 版 AT 在 **AP 侧** 实现。默认串口接 CP 时，每条 AT 前需加 `ap_cmd` 前缀（例如 `ap_cmd AT+STASTART=...`），详见 [BK IDK AT 入门指南](bk_at_start_guide.md)。

- [AT\+WLMAC](#cs-wifi-mac) : 获取或配置 STA / SoftAP 的 MAC 地址
- [AT\+STASTART](#cs-wifi-stastart) : 以STA身份连接至指定SSID的路由器上
- [AT\+STASTOP](#cs-wifi-stastop) : 以STA身份从目前正在连接的路由器上断开
- [AT\+WIFISTATUS](#cs-wifi-getstatus) : 用来查看wifi设备当前的模式状态或指定参数信息
- [AT\+WIFISCAN](#cs-wifi-scan) : 扫描周围AP信息
- [AT\+SAPSTART](#cs-wifi-sapstart) : 以SAP身份创建SoftAP
- [AT\+SAPSTOP](#cs-wifi-sapstop) : 停止当前开启的SoftAP
- [AT\+STAPING](#cs-wifi-pingstart) : 进行指定IP地址和指定时长和每包大小的PING包操作
- [AT\+STAPINGSTOP](#cs-wifi-pingstop) : 停止当前正在进行的PING包操作
- [AT\+GETINTERVAL](#cs-wifi-getinterval) : 获取STATION连接热点的listen interval的值
- [AT\+GETMODE](#cs-wifi-getmode) : 获取设备支持的 Wi-Fi 模式
- [AT\+HIDDENSAP](#cs-wifi-hiddensap) : 以SoftAP的身份启动一个隐藏ssid的热点。
- [AT\+CLOSECSA](#cs-wifi-closecsa) : 用于执行关闭Wi-Fi多身份（SoftAP\+ STA）共存模式下SoftAP主动切换到STA的信道上的操作。
- [AT\+NETBRIDGE](#cs-wifi-netbridge) : 开启或关闭 Wi-Fi 桥接模式。

<a id="at-stastart-stassid"></a>

<a id="cs-wifi-stastart"></a>

## [AT\+STASTART](#cs-wifi-at) **:以STA身份连接至指定SSID的路由器上**

**命令说明**

```
该命令用于以STA身份连接至指定SSID的路由器或者热点上。
```

**查询命令**

```
无
```

**执行命令**

```
AT+STASTART=ssid, pwd(可选)
```

**参数**

```
ssid：要以STA身份连接的AP路由器或者热点的SSID

pwd：该路由器或者热点的密码，如果该路由器或者热点为OPEN则忽略此选项
```

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 20s |

**AT消息**

```
EVT:WLAN STA CONNECTED

CONNECTED SSID: xxxx(该AP的SSID)

EVT:GOT-IP

sta got ip:192.168.xx.xx所获得的IP地址
```

**示例**

```
AT+STASTART=ax86u,12345678

EVT:WLAN STA CONNECTED

CONNECTED SSID:ax86u

EVT:BK STA GOT IP

sta got ip:192.168.50.159

CMDRSP:OK
```

<a id="at-stastop-sta"></a>

<a id="cs-wifi-stastop"></a>

## [AT\+STASTOP](#cs-wifi-at) **:以STA身份从目前正在连接的路由器上断开**

**命令说明**

```
该命令用于将STA身份从目前正在连接的路由器上断开。
```

**查询命令**

```
无
```

**执行命令**

```
AT+STASTOP
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

<a id="at-wifistatus-wifi"></a>

<a id="cs-wifi-getstatus"></a>

## [AT\+WIFISTATUS](#cs-wifi-at) **:用来查看wifi设备当前的模式状态或指定参数信息**

**命令说明**

```
该命令用于查看wifi设备当前的模式状态或指定参数信息。
```

**查询命令**

```
无
```

**执行命令**

```
AT+WIFISTATUS

AT+WIFISTATUS=param1

AT+WIFISTATUS=param1,param2
```

**参数**

```
无参数：查看wi-fi设备当前的模式状态

param1：查询wi-fi状态的身份，取值范围：STA/AP

param2：查询wi-fi的具体状态。
```

注意

STA支持：RSSI、BSSID、SSID、IP、CHANNEL

AP支持：SSID、CHANNEL、SECURITY、IP

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 15s |

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**AT消息**

```
无参数时:
    EVT:'sta: x, ap: x (1:对应身份已启动；0:对应身份未启动)
    EVT:sta:rssi=xxx,aid=xx,ssid=xxxx,bssid=xx:xx:xx:xx:xx:xx,channel=xx,cipher_type=xxx(STA开启)
    EVT:softap: ssid=1 , channel=3, cipher_type=WPA2-AES(SAP开启)
    EVT:ap_ip=xxx,ap_gate=xxx,ap_mask=xxx,ap_dns=xxx(SAP开启)

单一参数：
    STA状态：
    CMDRSP:STA_WIFI_CONNECT
    CMDRSP:STA_WIFI_DISCONNECT

    AP状态：
    CMDRSP:AP_WIFI_START
    CMDRSP:AP_WIFI_CLOSE

两个参数：
    STA身份：
        RSSI:    CMDRSP:sta_rssi:xxx
        CHANNEL: CMDRSP:sta_chnl:xx
        BSSID：  CMDRSP:sta_bssid:xx:xx:xx:xx:xx:xx
        SSID：   CMDRSP:sta_ssid::xxx
        IP：     CMDRSP:STA_IP=192.168.xx.xx,GATE=192.168.xx.xx,MASK=xxx.xxx.xxx.x,DNS=xxx.xx.xx.

    AP身份：
        SSID:    CMDRSP:ap_ssid:xxx
        CHANNEL: CMDRSP:ap_chnl:xx
        SECURITY:CMDRSP:ap_security:xxx
        IP：     CMDRSP:AP_IP=192.168.xx.xx,GATE=192.168.xx.xx,MASK=xxx.xxx.xxx.x,DNS=xxx.xx.xx.
```

<a id="at-wifiscan-ap"></a>

<a id="cs-wifi-scan"></a>

## [AT\+WIFISCAN](#cs-wifi-at) **:扫描周围AP信息**

**命令说明**

```
该命令用于扫描周围AP信息，可以通过配置指定扫描信道、扫描时长等。
```

**查询命令**

```
无
```

**执行命令**

```
AT+WIFISCAN
AT+WIFISCAN=param1
AT+WIFISCAN=param1<,param2,param3,param4,param5,param6>(param2~param6均为可选参数)
AT+WIFISCAN=SET_SSID,SSID,TYPE,DURATION,CNT,NUMBER
```

**参数**

```
无参数：设备会扫描周围所有的AP信息并打印
只有param1:ssid 可以返按照指定ssid进行扫描。

其他情况：

    a) param1:SET_SSID,是否指定ssid扫描,指定ssid:1; 不指定ssid:0；

    b) param2:SSID,若参数a为1，则填写目标ssid，否则此值为0；

    c) param3:TYPE,扫描类型，主动扫描:0，被动扫描:1；【若不指定则填写0】

    d) param4:DURATION,单信道扫描时长，单位为ms;【若不指定则填写0】

    e) param5:CNT,指定扫描信道的数量；【若不指定则填写0】

    f) param6:NUMBER,若e中指定扫描信道个数不为0 ，则f填写扫描的信道编号；【可选，若e为0不填写】
```

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 5s |

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**AT消息**

```
EVT:WLAN STA SCAN_DONE
```

**示例**

```
1.AT+WIFISCAN【使用默认方式全信道扫描全部AP】

2.AT+WIFISCAN=aclsemi【使用默认方式全信道扫描指定ssid的AP】

3.AT+WIFISCAN=1,aclsemi,0,0,0【扫描aclsemi路由器，其他默认】

4.AT+WIFISCAN=0,0,0,0,3,1,6,11【扫描1/6/11信道全部AP，其他默认】

5.AT+WIFISCAN=0,0,1,0,0【被动扫描，其他默认】

6.AT+WIFISCAN=0,0,0,70,0【指定信道扫描时长70ms，其他默认】

7.AT+WIFISCAN=1,aclsemi,1,70,3,1,6,11【扫描指定ssid路由器，被动扫描，信道扫描时长70ms，仅扫描1/6/11信道】
```

备注

当配置的 *duration* 时间在0\~120ms(包括120ms)时，当扫描时间超过1.6s时会认定为失败

**只有在配置了duration时此情况才生效**

**示例**

```
AT+WIFISCAN

scan found 64 AP

                          SSID                     BSSID         RSSI chan security
-------------------------------- -----------------   ---- ---- ---------
NETGEAR55                        74:d0:2b:6d:6b:cc    -49  3  WPA3-SAE
tplink                           c0:61:18:2b:82:b4    -49 10  WPA-AES
aclsemi_2.4G                     74:50:4e:3f:7e:d1    -57  6  WPA2-AES
daily_test                       50:0f:f5:63:0c:21    -58  3  WPA3-WPA2-MIX
ChinaNet-AbO3                    ba:a1:4a:65:54:b5    -58 11  WPA2-MIX
OpenWrt                          d4:da:21:76:0d:d9    -29  1  NONE
······

CMDRSP:OK

$EVT:WLAN STA SCAN_DONE
```

<a id="at-sapstart-sapsoftap"></a>

<a id="cs-wifi-sapstart"></a>

## [AT\+SAPSTART](#cs-wifi-at) **:以SAP身份创建SoftAP**

**命令说明**

```
该命令用于以SAP身份创建SoftA。
```

**查询命令**

```
无
```

**执行命令**

```
AT+SAPSTART=ssid
AT+SAPSTART=ssid,password
AT+SAPSTART=ssid,channel（当第二个参数小于3个字符时会被认为是信道参）
AT+SAPSTART=ssid,password,channel
```

**参数**

```
ssid:SSID,想要创建的SoftAP的SSID字符串

password:密码,想要创建的SoftAP的密码，如果想将SAP设为OPEN则忽视此选项

channel:信道,当您设置ssid和pwd之后，第三个参数为设置的信道值
```

备注

SSID设置长度请不要超过32个字符，超过32个字符会返回失败！

密码设置长度请置于8\~64个字节之间，小于8个字节则按照OPEN处理，超过64个字节将创建失败！

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

**属性**

> | 是否超时 | 超时时间 |
> | --- | --- |
> | 是 | 15s |

**AT消息**

```
当有STA连接至本SAP时打印

EVT:WLAN SAP CONNECTED + 连接上的STA的MAC地址
```

<a id="at-sapstop-softap"></a>

<a id="cs-wifi-sapstop"></a>

## [AT\+SAPSTOP](#cs-wifi-at) **:停止当前开启的SoftAP**

**查询命令**

```
无
```

**执行命令**

```
AT+SAPSTOP
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

<a id="at-staping-ipping"></a>

<a id="cs-wifi-pingstart"></a>

## [AT\+STAPING](#cs-wifi-at) **:进行指定IP地址和指定时长和每包大小的PING包操作**

**查询命令**

```
无
```

**执行命令**

```
AT+STAPING=ip
AT+STAPING=ip,num
AT+STAPING=ip,num,size
```

**参数**

```
ip:想要PING的目标IP地址
num:想要PING的包的个数
size:想要PING的包的大小
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

<a id="at-stapingstop-ping"></a>

<a id="cs-wifi-pingstop"></a>

## [AT\+STAPINGSTOP](#cs-wifi-at) **:停止当前正在进行的PING包工作**

**查询命令**

```
无
```

**执行命令**

```
AT+STAPINGSTOP
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

<a id="at-wlmac-sta-softap-mac"></a>

<a id="cs-wifi-mac"></a>

## [AT\+WLMAC](#cs-wifi-at) **:获取或配置 STA / SoftAP 的 MAC 地址**

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
无参数：获取当前设备的 STA / SoftAP MAC 地址

mac_addr：配置 STA 身份的 MAC 地址（可选）
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

<a id="at-getinterval-stationlisten-interval"></a>

<a id="cs-wifi-getinterval"></a>

## [AT\+GETINTERVAL](#cs-wifi-at) **:获取STATION连接热点的listen interval的值**

**命令说明**

```
获取当前STATION连接热点的listen interval的值。
```

**查询命令**

```
无
```

**执行命令**

```
AT+GETINTERVAL
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
AT+GETINTERVAL

EVT: get wifi listen interval 1.

CMDRSP:OK
```

<a id="at-getmode-wi-fi"></a>

<a id="cs-wifi-getmode"></a>

## [AT\+GETMODE](#cs-wifi-at) **:获取设备支持的 Wi-Fi 模式**

**执行命令**

```
AT+GETMODE
```

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```

<a id="at-hiddensap-softapssid"></a>

<a id="cs-wifi-hiddensap"></a>

## [AT\+HIDDENSAP](#cs-wifi-at) **:以SoftAP的身份启动一个隐藏ssid的热点**

**命令说明**

```
该命令用于以SoftAP的身份启动一个隐藏ssid的热点。
```

**查询命令**

```
无
```

**执行命令**

```
AT+HIDDENSAP=ssid, pwd(可选)
```

**参数**

```
ssid：启动热点的SSID

pwd：热点的密码，如果热点设置为OPEN则忽略该参数
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

<a id="at-closecsa-wi-fi-softap-sta-softapsta"></a>

<a id="cs-wifi-closecsa"></a>

## [AT\+CLOSECSA](#cs-wifi-at) **:关闭Wi-Fi SoftAP \+ STA 共存模式下SoftAP主动切换到STA的信道上的操作**

**命令说明**

```
该命令用于执行关闭Wi-Fi SoftAP + STA 共存模式下SoftAP主动切换到STA的信道上的操作。

当关闭该功能后，再启动SoftAP时，SoftAP将根据客户配置的信道或者默认信道启动，不会再主动将信道切换到已经连接的STA的信道上。
```

**查询命令**

```
无
```

**执行命令**

```
AT+CLOSECSA=close_csa
```

**参数**

```
close_csa：是否关闭Wi-Fi SoftAP + STA 共存模式下SoftAP主动切换到STA的信道上，取值范围：0/1。
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

<a id="at-netbridge-wi-fi"></a>

<a id="cs-wifi-netbridge"></a>

### [AT\+NETBRIDGE](#cs-wifi-at) **:开启或关闭 Wi-Fi 桥接模式**

**执行命令**

```
AT+NETBRIDGE=OPEN,<bridge_ssid>,<router_ssid>[,<key>]
AT+NETBRIDGE=CLOSE
```

**参数**

```
bridge_ssid: 桥接侧创建的 SoftAP SSID

router_ssid: 作为 STA 连接的上游路由器 SSID

key: 路由器密码（可选）
```

**响应**

```
CMDRSP:OK

CMDRSP:ERROR
```
