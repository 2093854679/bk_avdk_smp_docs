---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/network/bk_netif.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="netif"></a>

# Netif

`ap/include/components/netif.h` 提供网络接口 IP 配置；相关类型与事件见 [Netif 类型定义](bk_netif_types.md)。

<a id="netif-h"></a>

## netif.h

<a id="header-file"></a>

### Header File

- [netif.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/netif.h)

<a id="functions"></a>

### Functions

<a id="_CPPv423bk_netif_set_ip4_config10netif_if_tPK18netif_ip4_config_t"></a>

<a id="_CPPv323bk_netif_set_ip4_config10netif_if_tPK18netif_ip4_config_t"></a> <a id="_CPPv223bk_netif_set_ip4_config10netif_if_tPK18netif_ip4_config_t"></a> <a id="bk_netif_set_ip4_config__netif_if_t.netif_ip4_config_tCP"></a> <a id="group__bk__api__netif_1gadd74802f5d3fc434591918381e307cf6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_netif\_set\_ip4\_config([netif\_if\_t](bk_netif_types.md#_CPPv410netif_if_t "netif_if_t") ifx, const [netif\_ip4\_config\_t](bk_netif_types.md#_CPPv418netif_ip4_config_t "netif_ip4_config_t") \*config)
:   Set netif interface’s IP4 address information.

    This function is mainly used to set a static IP on an interface.

    **Attention**
    :   1\. For STA, if this API never calls, it gets the IP address via DHCP by default.

    **Attention**
    :   2\. If the interface is already up, we need to stop the interface first before calling this API, or restart the interface after the this API is called.

    **Attention**
    :   3\. Currently no sanity checking for the IP4 address to be configured, also no checking about the relationship between ip/mask/gateway/dns, the API caller need to guarantee that the correctness of the configured info.

    **Attention**
    :   4\. Avoid configuring same subnet for STA and AP.

    参数
    :   - **ifx** – The interface index
        - **config** – the IP4 information of the interface

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NETIF\_IF: invalid netif interface ID
        - BK\_ERR\_NULL\_PARAM: config is NULL

<a id="_CPPv423bk_netif_get_ip4_config10netif_if_tP18netif_ip4_config_t"></a>

<a id="_CPPv323bk_netif_get_ip4_config10netif_if_tP18netif_ip4_config_t"></a> <a id="_CPPv223bk_netif_get_ip4_config10netif_if_tP18netif_ip4_config_t"></a> <a id="bk_netif_get_ip4_config__netif_if_t.netif_ip4_config_tP"></a> <a id="group__bk__api__netif_1ga634a0e17fa52056d78f5f5c83af69173"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_netif\_get\_ip4\_config([netif\_if\_t](bk_netif_types.md#_CPPv410netif_if_t "netif_if_t") ifx, [netif\_ip4\_config\_t](bk_netif_types.md#_CPPv418netif_ip4_config_t "netif_ip4_config_t") \*config)
:   Get netif interface’s IP address information.

    If the interface is up, IP information is read directly from the TCP/IP stack. If the interface is down, the API just return all 0 information

    参数
    :   - **ifx** – netif interface ID
        - **config** – store the IP4 configuration info

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NETIF\_IF: invalid netif interface ID
        - BK\_ERR\_NULL\_PARAM: config is NULL

<a id="_CPPv426bk_netif_get_ip6_addr_info10netif_if_t"></a>

<a id="_CPPv326bk_netif_get_ip6_addr_info10netif_if_t"></a> <a id="_CPPv226bk_netif_get_ip6_addr_info10netif_if_t"></a> <a id="bk_netif_get_ip6_addr_info__netif_if_t"></a> <a id="group__bk__api__netif_1ga8c7db2d41ccae10db35a5b31f90baf44"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_netif\_get\_ip6\_addr\_info([netif\_if\_t](bk_netif_types.md#_CPPv410netif_if_t "netif_if_t") ifx)
:   Get netif interface’s IP6 address information.

    If the interface is up, IP6 information is read directly from the TCP/IP stack. If the interface is down, the API just return all 0 information

    参数
    :   **ifx** – netif interface ID

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NETIF\_IF: invalid netif interface ID
        - BK\_ERR\_NULL\_PARAM: config is NULL

<a id="_CPPv418bk_netif_static_ip18netif_ip4_config_t"></a>

<a id="_CPPv318bk_netif_static_ip18netif_ip4_config_t"></a> <a id="_CPPv218bk_netif_static_ip18netif_ip4_config_t"></a> <a id="bk_netif_static_ip__netif_ip4_config_t"></a> <a id="group__bk__api__netif_1ga9fd50f873579d4d8a9f85e6af28225dc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_netif\_static\_ip([netif\_ip4\_config\_t](bk_netif_types.md#_CPPv418netif_ip4_config_t "netif_ip4_config_t") static\_ip4\_config)
:   this function is only for the interface of NETIF\_IF\_STA to set a static IP .

    call back this function in netif\_wifi\_event\_cb()(in components/bk\_netif/bk\_netif.c) when case EVENT\_WIFI\_STA\_CONNECTED, and pass the param static\_ip4\_config includes ip, mask, gateway and dns for your static IP config. example: switch (event\_id) { case EVENT\_WIFI\_STA\_CONNECTED: #if CONFIG\_LWIP bk\_netif\_static\_ip(static\_ip4\_config); sta\_ip\_start(); #endif

    参数
    :   **static\_ip4\_config** – ipv4 config for this netif(only for NETIF\_IF\_STA).

    返回
    :   - BK\_OK: succeed
        - else: fail

<a id="_CPPv424bk_netif_set_dns_serversA_PKc7uint8_t"></a>

<a id="_CPPv324bk_netif_set_dns_serversA_PKc7uint8_t"></a> <a id="_CPPv224bk_netif_set_dns_serversA_PKc7uint8_t"></a> <a id="bk_netif_set_dns_servers__cCPA.uint8_t"></a> <a id="group__bk__api__netif_1ga6e0fb622e293778b8e6dde4e0b9bf135"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_netif\_set\_dns\_servers(const char \*servers\[\], uint8\_t count)
:   Set sticky IPv4 DNS servers (survive DHCP / SMP IPV4 sync / reconnect)

    On SMP, applies on AP and syncs full sticky snapshot to CP. Does not clear an existing IPv6 sticky override. Call [bk\_netif\_clear\_dns\_servers()](#group__bk__api__netif_1ga53fb006eac070982573b49442334dc4c) to stop re-apply on later reconnect.

    参数
    :   - **servers** – Array of IPv4 DNS strings, e.g. {“8.8.8.8”,”8.8.4.4”}.
        - **count** – Number of entries (\>\=1). Extra beyond SDK IPv4 DNS slots are ignored; if count \< slots, the last entry is repeated.

    返回
    :   BK\_OK, or BK\_ERR\_NULL\_PARAM / BK\_FAIL

<a id="_CPPv426bk_netif_clear_dns_serversv"></a>

<a id="_CPPv326bk_netif_clear_dns_serversv"></a> <a id="_CPPv226bk_netif_clear_dns_serversv"></a> <a id="bk_netif_clear_dns_servers__void"></a> <a id="group__bk__api__netif_1ga53fb006eac070982573b49442334dc4c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_netif\_clear\_dns\_servers(void)
:   Clear sticky DNS overrides (disable reconnect re-apply)

    Clears sticky IPv4/IPv6 config and zeros current DNS slots. STA disconnect alone only zeros slots and keeps sticky; reconnect will re-apply sticky unless this API was called.

    返回
    :   BK\_OK on success

<a id="id1"></a>

## 参考链接

- [Netif 类型定义](bk_netif_types.md)
- [Wi-Fi API](../wifi.md)
