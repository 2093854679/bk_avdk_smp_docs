---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/wifi/bk_wifi_p2p.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="armino-wi-fi-p2p"></a>

# **Armino Wi-Fi P2P 使用指南**

<a id="wi-fi-p2p"></a>

## **Wi-Fi P2P 概述**

> Wi-Fi Direct，也被称为Wi-Fi P2P（Wi-Fi Peer-to-Peer），是Wi-Fi联盟发布的一种无线通信技术，旨在简化设备间的连接过程，实现快速、方便的无线通信。它允许设备直接相互连接，无需通过传统的Wi-Fi接入点（AP），就可以进行点对点通信。这意味着移动中的用户可以从笔记本电脑、智能手机和平板电脑等设备无线打印文档、共享屏幕、共享数据、同步文件和显示信息。

<a id="p2p"></a>

### **P2P架构**

> P2P架构中定义了三个组件，分别是：
>
> - P2P Device：
>   :   - 支持Wi-Fi P2P协议的设备，如智能手机、平板、笔记本等。
>       - 具备发现其他设备、协商连接、加入或者创建P2P Group的能力。
> - P2P Group Owner(GO):
>   :   - P2P网络中的”主控”角色，类似于传统Wi-Fi网络中的接入点（AP）。
>       - GO负责管理组内设备连接、资源分配和数据转发。
>       - 一个P2P Group只能有一个GO。
> - P2P Group Client(GC):
>   :   - 连接到GO的设备，类似于传统Wi-Fi网络中的终端设备（STA）。
>       - 可以与GO进行数据交换，也能与其他Client通信（通过GO转发）。
>       - 一个P2P Group可以有多个Client，形成1：n的拓扑结构。

<a id="id1"></a>

### **P2P 拓扑**

> - 在组建P2P Group（即 P2P Network）之前，终端都是一个一个的P2P Device。
> - 当这些P2P Device设备之间完成P2P协商后，其中将有一个Device来扮演GO的角色，而其他Device扮演GC的角色。
> - 由于GO的功能类似于AP，所以周围那些不支持P2P功能的STA也能发现并关联到GO。这些STA被称之为Legacy Clients。
>
> 最终构成的P2P Group拓扑图如下：
>
> <a id="id16"></a>
> ![../../_images/p2p_go_top.png](../../../../_assets/904dcbd83d21c8171cc8-p2p_go_top.png)
>
>
> P2P Group拓扑图

<a id="id2"></a>

### **P2P 并发操作**

> - 一个P2P设备可以与WLAN同时运行。这样的设备被称为P2P并发设备。下图展示了一个P2P并发设备，其中一个MAC实体作为WLAN-STA运行，以一个MAC实体作为P2P设备运行。
>
> <a id="id17"></a>
> ![../../_images/p2p_concurrent.png](../../../../_assets/b885c1b6847f4e7c28a8-p2p_concurrent.png)
>
>
> P2P Concurrent Device
>
> 备注
>
> P2P 与 WLAN 并发能力取决于工程配置与射频资源。示例工程见 [p2p](../../examples/projects/wifi/p2p.md)；若需 STA 与 P2P 同时运行，请评估信道/共存限制。

<a id="id3"></a>

### **P2P 实现过程**

> P2P的实现过程主要包括设备发现、服务发现、组网协商、安全配置、建立连接与数据传输等：
>
> - 设备发现（Device Discovery）：
>   :   - 设备通过发送和监听Probe Request/Response帧，在社交信道（如1、6、11）上发现彼此。
> - 服务发现（Service Discovery）：
>   :   - 可选阶段，用于查询对方是否支持特定服务。
> - 组建群组（Group Formation）：
>   :   - GO Negotiation：通过GO Negotiation协议，两个设备协商决定谁成为Group Owner。
>       - Provisioning：协商连接方式并完成安全认证，确保通信加密。
> - 建立连接与数据传输：
>   :   - 一旦连接成功，GO分配IP地址，Client加入网络。设备之间可通过TCP/IP协议进行数据交换。

<a id="id4"></a>

## **Wi-Fi P2P 特性支持**

> 目前 BK7259 SMP SDK 支持的 Wi-Fi P2P 特性如下：
>
> - 核心功能支持：
>   :   - 支持GO。
>       - 支持GC。
> - P2P安全特性支持：
>   :   - 连接建立前，通过WPS（Push Button）协议进行认证。
>       - 连接建立前后，使用WPA2加密通信数据。

<a id="id5"></a>

## **Wi-Fi P2P 移植指南**

> P2P 功能需要额外的代码空间以及 Memory。AP、CP 需分别使能对应的功能宏，详见 [p2p](../../examples/projects/wifi/p2p.md)：
>
> > - AP：`CONFIG_P2P`
> > - CP：`CONFIG_P2P` ， `CONFIG_P2P_GO` ， `CONFIG_WPS` （wpa\_supplicant 菜单）
> > - Flash 分区、RAM 分配可参考上述项目示例中的默认配置。

<a id="wi-fi-p2p-api"></a>

### **Wi-Fi P2P API介绍**

<a id="id6"></a>

#### **开启P2P**

> 函数 `bk_wifi_p2p_enable()` 用于开启P2P功能，传入的参数为P2P的SSID。也可使用 `bk_wifi_p2p_enable_with_intent()` 指定 GO intent。

<a id="id7"></a>

#### **监听 P2P 设备**

> 函数 `bk_wifi_p2p_listen()` 用于进入 P2P listen 状态，等待对端发现。

<a id="id8"></a>

#### **查找P2P设备**

> 函数 `bk_wifi_p2p_find()` 用于查找P2P设备，查找过程会广播Probe Request帧，并监听Probe Response帧。

<a id="id9"></a>

#### **停止查找P2P设备**

> 函数 `bk_wifi_p2p_stop_find()` 用于停止查找P2P设备，取消当前的p2p find操作。

<a id="id10"></a>

#### **连接 P2P 设备**

> 函数 `bk_wifi_p2p_connect()` 用于向指定对端 MAC 发起 P2P 连接（参数含 WPS method 与 GO intent）。

<a id="id11"></a>

#### **断开P2P连接**

> 函数 `bk_wifi_p2p_cancel()` 用于取消当前的p2p操作，包括查找、监听、连接等。

<a id="id12"></a>

#### **关闭P2P**

> 函数 `bk_wifi_p2p_disable()` 用于关闭P2P功能，关闭后，释放P2P资源。

<a id="wi-fi-p2p-command"></a>

### **Wi-Fi P2P Command介绍**

> 在 AP 核串口（需开启 CONFIG\_P2P 与 CONFIG\_WIFI\_CLI\_ENABLE）使用 `p2p` 命令：
>
> > - `p2p enable <ssid>`：开启 P2P，SSID 可选（默认 BEKEN SMP\_P2P）
> > - `p2p find`：查找 P2P 设备
> > - `p2p listen`：监听 P2P 设备
> > - `p2p stop_find`：停止查找
> > - `p2p connect`：连接对端（具体参数见 CLI help）
> > - `p2p cancel`：取消查找/监听/连接
> > - `p2p disable`：关闭 P2P

<a id="id13"></a>

### **Wi-Fi P2P Command使用示例**

> 示例1：开启P2P功能，传入的参数为P2P的SSID。
>
> ```
> p2p enable p2p_ssid    //如果不输入，使用默认值BEKEN SMP_P2P
> ```
>
> 示例2：查找P2P设备，查找过程会广播Probe Request帧，并监听Probe Response帧。
>
> ```
> p2p find
> ```
>
> 示例3：停止查找P2P设备，取消当前的p2p find操作。
>
> ```
> p2p stop_find
> ```
>
> 示例4：取消当前的p2p操作，包括查找、监听、连接等，包括断开P2P连接。
>
> ```
> p2p cancel
> ```
>
> 示例5：关闭P2P功能，关闭后，释放P2P资源。
>
> ```
> p2p disable
> ```
>
> 示例6：显示P2P命令帮助信息。
>
> ```
> p2p help
> ```

<a id="wi-fi-p2p-example"></a>

### **Wi-Fi P2P Example**

> 下面 Log 示例展示了 [p2p](../../examples/projects/wifi/p2p.md) 工程中的 Wi-Fi P2P 功能（AP 核串口）：
>
> ```
> p2p enable BEKEN SMP_P2P
>
> $
> wifid:mm_add_if_req: vif_idx=0, type=0, p2p=0, status=0
> wpa:State: DISCONNECTED -> INACTIVE
> wpa:State: INACTIVE -> DISCONNECTED
> lwip:mac c8:47:8c:2b:a4:a5
> WIFI:P2P event thread created successfully
> CMDRSP:OK
>
> p2p find
>
> $
> CMDRSP:OK
>
> wifid:[KW:]scanu_start_req:src_id=15,vif=0,dur=0,chan_cnt=3,ssid_len=7,bssid=0xffff-ffff-ffff
> wifid:[KW:]scanu_start_req:ssid=DIRECT-
> wifid:[KW:]scanu_confirm:status=0,req_type=0,upload_cnt=2,recv_cnt=72,time=370839us,result=1,rfcli=1
> wpa:Scan completed in 0.369000 seconds
> hitf:get scan result:1
> wpa:wpas_p2p_scan_res_handler: BSSID 3A:20:86:00:6E:48
> wpa:Peer found with Listen frequency 2462 MHz (rx_time=79.105000)
> wpa:P2P_EVENT_DEVICE_FOUND 3a:20:86:00:6e:48 p2p_dev_addr=3a:20:86:00:6e:48 name='真我GT 2 Pro' config_methods=0x188 new=1
>
> wpa:Sending GO Negotiation Response
> wpa:Received GO Negotiation Confirm from 3a:20:86:00:6e:48
> wpa:P2P-GO-NEG-SUCCESS role=client freq=2412 ht40=0 peer_dev=3a:20:86:00:6e:48 peer_iface=3a:20:86:00:6e:48 wps_method=PBC
> wpa:P2P: Start WPS Enrollee for peer 3a:20:86:00:6e:48 dev_addr 3a:20:86:00:6e:48 wps_method 3
> wpa:State: DISCONNECTED -> SCANNING
> [KW:]scanu_start_req:src_id=15,vif=0,dur=0,chan_cnt=1,ssid_len=24,bssid=0xffff-ffff-ffff
> [KW:]scanu_start_req:ssid=DIRECT-WI-真我GT 2 Pro
> [KW:]scanu_start_req:chan_idx=1
> [KW:]scanu_confirm:status=0,req_type=0,upload_cnt=2,recv_cnt=6,time=41949us,result=1,rfcli=1
> wpa:Scan completed in 0.040000 seconds
> hitf:get scan result:1
> wpa:Trying to associate with 3a:20:86:00:6e:48 (SSID='DIRECT-WI-\xe7\x9c\x9f\xe6\x88\x91GT 2 Pro' freq=2412 MHz)
> wpa:State: SCANNING -> ASSOCIATING
> lwip:remove vif0
> wifid:[KW:]mm_remove_if: vif0
> rwnx:FW features: [BCN][AUTOBCN][HWSCAN][CMON][MROLE][PS][DPSM][AMPDU][CHNL_CTXT][REORD][P2P][P2P_GO][UMAC][VHT][HE][BFMEE][WAPI][MFP][MU_MIMO_RX][TWT][PM_DSSS_ONLY]
> wifid:mm_add_if_req: vif_idx=0, type=0, p2p=1, status=0
> wpa:fsocket_reinit: create new socket 3
> lwip:mac c8:47:8c:2b:a4:a5
> [KW:]conn vif0-0,auth_type:0,bssid:203a-86-486e,ssid:DIRECT-WI-真我GT 2 Pro,is encryp:0.
> [KW:]scanu_start_req:src_id=7,vif=0,dur=0,chan_cnt=1,ssid_len=24,bssid=0x203a-86-486e
> [KW:]scanu_start_req:ssid=DIRECT-WI-真我GT 2 Pro
> [KW:]scanu_start_req:chan_idx=1
>
> wpa:State: ASSOCIATING -> ASSOCIATED
> wpa:CTRL-EVENT-EAP-STARTED EAP authentication started
> WPS: Building Message M1
> WPS: Received M2
> WPS: Building Message M3
> WPS: Received M4
> WPS: Building Message M5
> WPS: Received M6
> WPS: Building Message M7
> WPS: Received M8
> WPS: Building Message WSC_Done
> WPS-SUCCESS
> wpa:Group Formation completed successfully with 3a:20:86:00:6e:48
> wpa:P2P-GROUP-FORMATION-SUCCESS
> wpa:State: ASSOCIATED -> DISCONNECTED
> wpa:State: DISCONNECTED -> DISCONNECTED
> wpa:Trying to associate with 3a:20:86:00:6e:48 (SSID='DIRECT-WI-\xe7\x9c\x9f\xe6\x88\x91GT 2 Pro' freq=2412 MHz)
> wpa:State: DISCONNECTED -> ASSOCIATING
> [KW:]conn vif0-0,auth_type:0,bssid:203a-86-486e,ssid:DIRECT-WI-真我GT 2 Pro,is encryp:8.
> [KW:]scanu_join_req:src_id=7,dur=0,chan_cnt=1, ssid_len=24, bssid=0x203a-86-486e
> [KW:]scanu_join_req:ssid=DIRECT-WI-真我GT 2 Pro
> wpa:EAPOL: External notification - EAP success=0
> wpa:EAPOL: External notification - EAP fail=0
> wpa:State: ASSOCIATING -> ASSOCIATED
> wpa:State: ASSOCIATED -> 4WAY_HANDSHAKE
> wpa:WPA: TK 177c74bb19eff7801aefb61e2d09bfc0
> wpa:State: 4WAY_HANDSHAKE -> 4WAY_HANDSHAKE
> wpa:State: 4WAY_HANDSHAKE -> GROUP_HANDSHAKE
> wpa:State: GROUP_HANDSHAKE -> COMPLETED
> wpa:EAPOL: External notification - portValid=1
> wpa:EAPOL: External notification - EAP success=1
> lwip:sta ip start
> lwip:configuring iface sta (with DHCP client)
> lwip:[KW:]sta:DHCP_DISCOVER()
> cli:BK STA connected DIRECT-WI-真我GT 2 Pro
> [KW:]sta:DHCP_OFFER received in DHCP_STATE_SELECTING state
> [KW:]sta:DHCP_REQUEST(netif=0x2805ca58) en   2
> [KW:]sta:DHCP_ACK received
> ```

<a id="id14"></a>

### **Wi-Fi P2P常见问题**

**问题1： GO、GC的身份是如何确定的？**

> 答：GO、GC的身份是由双方设备协商决定，具体的流程可以参考下图：
>
> <a id="id18"></a>
> ![../../_images/p2p_go_determine.png](../../../../_assets/5af0fc35684b5e6e42dd-p2p_go_determine.png)
>
>
> Group Owner Determination流程图

**问题2：P2P连接失败的原因？**

> 答：P2P连接失败的原因可能有以下几种：
> :   - 协商失败，GO、GC身份确定失败。
>     - 安全认证失败，WPS认证失败。
>     - 连接超时。
>     - 等等其他原因。
>
>     P2P连接失败的问题，除了提供常规的串口Log外，空口包也是一个非常重要的定位手段，具体空口抓取可以参考 [BEKEN Wi-Fi 抓包指南](bk_wifi_capture.md)

<a id="id15"></a>

## **术语**

> | **缩写** | **术语** | **描述** |
> | --- | --- | --- |
> | P2P | Peer-to-Peer | 点对点连接 |
> | GO | Group Owner | 组所有者 |
> | GC | Group Client | 组客户端 |
> | WPS | Wi-Fi Protected Setup | Wi-Fi保护设置 |
> | PIN | Personal Identification Number | 个人识别码 |
> | PBC | Push Button Configuration | 推按钮配置 |
> | PS | Power Save mode | 省电模式 |
> | WSC | Wi-Fi Simple Configuration | Wi-Fi简单配置 |
> | WPA2 | Wi-Fi Protected Access 2 | Wi-Fi保护访问 2 |
> | EAP | Extensible Authentication Protocol | 可扩展认证协议 |
