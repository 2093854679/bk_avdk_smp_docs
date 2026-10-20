---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/network/bk_netif_types.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="netif"></a>

# Netif 类型定义

`ap/include/components/netif_types.h` 定义 netif 接口枚举、IP 配置结构体及事件数据结构。

<a id="netif-types-h"></a>

## netif\_types.h

<a id="header-file"></a>

### Header File

- [netif\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/netif_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv418netif_ip4_config_t"></a>

<a id="_CPPv318netif_ip4_config_t"></a> <a id="_CPPv218netif_ip4_config_t"></a> <a id="netif_ip4_config_t"></a> <a id="structnetif__ip4__config__t"></a> struct netif\_ip4\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18netif_ip4_config_t2ipE"></a>

    <a id="_CPPv3N18netif_ip4_config_t2ipE"></a> <a id="_CPPv2N18netif_ip4_config_t2ipE"></a> <a id="netif_ip4_config_t::ip__cA"></a> <a id="structnetif__ip4__config__t_1a2fa5668658e3cd4267ea2db731d20fe7"></a> char ip\[NETIF\_IP4\_STR\_LEN\]
    :   Local IP address.

    <a id="_CPPv4N18netif_ip4_config_t4maskE"></a>

    <a id="_CPPv3N18netif_ip4_config_t4maskE"></a> <a id="_CPPv2N18netif_ip4_config_t4maskE"></a> <a id="netif_ip4_config_t::mask__cA"></a> <a id="structnetif__ip4__config__t_1a4cac0e2c02e738cd8aee1a4a79df163e"></a> char mask\[NETIF\_IP4\_STR\_LEN\]
    :   Netmask.

    <a id="_CPPv4N18netif_ip4_config_t7gatewayE"></a>

    <a id="_CPPv3N18netif_ip4_config_t7gatewayE"></a> <a id="_CPPv2N18netif_ip4_config_t7gatewayE"></a> <a id="netif_ip4_config_t::gateway__cA"></a> <a id="structnetif__ip4__config__t_1af885cd7d2ab730b9507abc4f9dc360d8"></a> char gateway\[NETIF\_IP4\_STR\_LEN\]
    :   Gateway IP address.

    <a id="_CPPv4N18netif_ip4_config_t3dnsE"></a>

    <a id="_CPPv3N18netif_ip4_config_t3dnsE"></a> <a id="_CPPv2N18netif_ip4_config_t3dnsE"></a> <a id="netif_ip4_config_t::dns__cA"></a> <a id="structnetif__ip4__config__t_1a4c2c025eaa7c1d4a3c7011377ad65b48"></a> char dns\[NETIF\_IP4\_STR\_LEN\]
    :   DNS server IP address.

<a id="_CPPv418netif_dns_config_t"></a>

<a id="_CPPv318netif_dns_config_t"></a> <a id="_CPPv218netif_dns_config_t"></a> <a id="netif_dns_config_t"></a> <a id="structnetif__dns__config__t"></a> struct netif\_dns\_config\_t
:   Sticky DNS override snapshot (AP/CP IPC and local apply).

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18netif_dns_config_t8dns4_cntE"></a>

    <a id="_CPPv3N18netif_dns_config_t8dns4_cntE"></a> <a id="_CPPv2N18netif_dns_config_t8dns4_cntE"></a> <a id="netif_dns_config_t::dns4_cnt__uint8_t"></a> <a id="structnetif__dns__config__t_1addf7198a6b4a85c132edd05e287981b6"></a> uint8\_t dns4\_cnt
    :   Valid entries in dns4\[\], 0..NETIF\_DNS\_SERVER\_MAX.

    <a id="_CPPv4N18netif_dns_config_t8dns6_cntE"></a>

    <a id="_CPPv3N18netif_dns_config_t8dns6_cntE"></a> <a id="_CPPv2N18netif_dns_config_t8dns6_cntE"></a> <a id="netif_dns_config_t::dns6_cnt__uint8_t"></a> <a id="structnetif__dns__config__t_1ad0ef5ff7c18aeaa7e765030ab841cd5a"></a> uint8\_t dns6\_cnt
    :   Valid entries in dns6\[\], 0..NETIF\_DNS\_SERVER\_MAX.

    <a id="_CPPv4N18netif_dns_config_t5v4_enE"></a>

    <a id="_CPPv3N18netif_dns_config_t5v4_enE"></a> <a id="_CPPv2N18netif_dns_config_t5v4_enE"></a> <a id="netif_dns_config_t::v4_en__uint8_t"></a> <a id="structnetif__dns__config__t_1a83d375146c056dda955823f5171f2d80"></a> uint8\_t v4\_en
    :   1: IPv4 sticky active.

    <a id="_CPPv4N18netif_dns_config_t5v6_enE"></a>

    <a id="_CPPv3N18netif_dns_config_t5v6_enE"></a> <a id="_CPPv2N18netif_dns_config_t5v6_enE"></a> <a id="netif_dns_config_t::v6_en__uint8_t"></a> <a id="structnetif__dns__config__t_1ab305f68f743e1d7bc981f10763905d7f"></a> uint8\_t v6\_en
    :   1: IPv6 sticky active.

<a id="_CPPv421netif_event_got_ip4_t"></a>

<a id="_CPPv321netif_event_got_ip4_t"></a> <a id="_CPPv221netif_event_got_ip4_t"></a> <a id="netif_event_got_ip4_t"></a> <a id="structnetif__event__got__ip4__t"></a> struct netif\_event\_got\_ip4\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21netif_event_got_ip4_t8netif_ifE"></a>

    <a id="_CPPv3N21netif_event_got_ip4_t8netif_ifE"></a> <a id="_CPPv2N21netif_event_got_ip4_t8netif_ifE"></a> <a id="netif_event_got_ip4_t::netif_if__netif_if_t"></a> <a id="structnetif__event__got__ip4__t_1a343bd40a06dc6cd07a6054fe5e90bbb1"></a> [netif\_if\_t](#_CPPv410netif_if_t "netif_if_t") netif\_if
    :   Netif interface ID

    <a id="_CPPv4N21netif_event_got_ip4_t2ipE"></a>

    <a id="_CPPv3N21netif_event_got_ip4_t2ipE"></a> <a id="_CPPv2N21netif_event_got_ip4_t2ipE"></a> <a id="netif_event_got_ip4_t::ip__cA"></a> <a id="structnetif__event__got__ip4__t_1ac7bb091a006f53a76a16aac95e5d52f3"></a> char ip\[NETIF\_IP4\_STR\_LEN\]
    :   Local IP address.

<a id="_CPPv421netif_event_got_ip6_t"></a>

<a id="_CPPv321netif_event_got_ip6_t"></a> <a id="_CPPv221netif_event_got_ip6_t"></a> <a id="netif_event_got_ip6_t"></a> <a id="structnetif__event__got__ip6__t"></a> struct netif\_event\_got\_ip6\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21netif_event_got_ip6_t8netif_ifE"></a>

    <a id="_CPPv3N21netif_event_got_ip6_t8netif_ifE"></a> <a id="_CPPv2N21netif_event_got_ip6_t8netif_ifE"></a> <a id="netif_event_got_ip6_t::netif_if__netif_if_t"></a> <a id="structnetif__event__got__ip6__t_1ab01c57b32eca136b8c260ca1278c5b03"></a> [netif\_if\_t](#_CPPv410netif_if_t "netif_if_t") netif\_if
    :   Netif interface ID

    <a id="_CPPv4N21netif_event_got_ip6_t2ipE"></a>

    <a id="_CPPv3N21netif_event_got_ip6_t2ipE"></a> <a id="_CPPv2N21netif_event_got_ip6_t2ipE"></a> <a id="netif_event_got_ip6_t::ip__cA"></a> <a id="structnetif__event__got__ip6__t_1af02baea8ab929de1f7ebe1a0838d5922"></a> char ip\[NETIF\_IP6\_STR\_LEN\]
    :   IPv6 address string, for debug

    <a id="_CPPv4N21netif_event_got_ip6_t8addr_idxE"></a>

    <a id="_CPPv3N21netif_event_got_ip6_t8addr_idxE"></a> <a id="_CPPv2N21netif_event_got_ip6_t8addr_idxE"></a> <a id="netif_event_got_ip6_t::addr_idx__uint8_t"></a> <a id="structnetif__event__got__ip6__t_1a5e23ae5f76aca7cf61c4373d12234af0"></a> uint8\_t addr\_idx
    :   IPv6 address index in netif

<a id="macros"></a>

### Macros

<a id="c.NETIF_IP4_STR_LEN"></a>

<a id="group__bk__api__netif__typedef_1ga759a49b7285f6291564fed85c38244fe"></a> NETIF\_IP4\_STR\_LEN
:   IP4 string length

<a id="c.NETIF_IP6_ADDR_LEN"></a>

<a id="group__bk__api__netif__typedef_1gabfa0cc1857793f7c36fea8afa6b5f08d"></a> NETIF\_IP6\_ADDR\_LEN
:   IP6 address length

<a id="c.NETIF_IP6_STR_LEN"></a>

<a id="group__bk__api__netif__typedef_1gacd63206d96de44869b72e13046c732d5"></a> NETIF\_IP6\_STR\_LEN
:   IP6 string length

<a id="c.BK_ERR_NETIF_IF"></a>

<a id="group__bk__api__netif__typedef_1ga2b28552175259825f7e58af945507ddb"></a> BK\_ERR\_NETIF\_IF
:   Invalid interface ID

<a id="c.NETIF_DNS_SERVER_MAX"></a>

<a id="group__bk__api__netif__typedef_1ga59fe58d521dc31b3e04295439717e0b8"></a> NETIF\_DNS\_SERVER\_MAX
:   IPC / snapshot capacity for sticky DNS lists. Must be \>\= DNS\_IPV4\_SERVER\_SLOTS and DNS\_IPV6\_SERVER\_SLOTS (lwipopts).

<a id="c.NETIF_MAX_IPV6_ADDRESSES"></a>

<a id="group__bk__api__netif__typedef_1gac1851deea1b9cdc862309426919bc370"></a> NETIF\_MAX\_IPV6\_ADDRESSES

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv410netif_if_t"></a>

<a id="_CPPv310netif_if_t"></a> <a id="_CPPv210netif_if_t"></a> <a id="group__bk__api__netif__typedef_1gafd0e8f6d2cd5550a97425b19e844266e"></a> enum netif\_if\_t
:   *Values:*

    <a id="_CPPv4N10netif_if_t12NETIF_IF_STAE"></a>

    <a id="_CPPv3N10netif_if_t12NETIF_IF_STAE"></a> <a id="_CPPv2N10netif_if_t12NETIF_IF_STAE"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266eadc188233960b61928d00b47db2e42931"></a> enumerator NETIF\_IF\_STA
    :   WiFi STA interface

    <a id="_CPPv4N10netif_if_t11NETIF_IF_APE"></a>

    <a id="_CPPv3N10netif_if_t11NETIF_IF_APE"></a> <a id="_CPPv2N10netif_if_t11NETIF_IF_APE"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266ea2a6344633c82cd07692275647736200a"></a> enumerator NETIF\_IF\_AP
    :   WiFi AP interface

    <a id="_CPPv4N10netif_if_t15NETIF_IF_BRIDGEE"></a>

    <a id="_CPPv3N10netif_if_t15NETIF_IF_BRIDGEE"></a> <a id="_CPPv2N10netif_if_t15NETIF_IF_BRIDGEE"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266ea73c86e8425a30941da583eb34cf8ee77"></a> enumerator NETIF\_IF\_BRIDGE
    :   WiFi BR interface

    <a id="_CPPv4N10netif_if_t12NETIF_IF_ETHE"></a>

    <a id="_CPPv3N10netif_if_t12NETIF_IF_ETHE"></a> <a id="_CPPv2N10netif_if_t12NETIF_IF_ETHE"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266ea8e2d44ceed69642a5745927a02cc626d"></a> enumerator NETIF\_IF\_ETH
    :   ETH interface

    <a id="_CPPv4N10netif_if_t12NETIF_IF_PANE"></a>

    <a id="_CPPv3N10netif_if_t12NETIF_IF_PANE"></a> <a id="_CPPv2N10netif_if_t12NETIF_IF_PANE"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266ea5bf7eef79f288ac1c9163e1bb9a7c7e3"></a> enumerator NETIF\_IF\_PAN
    :   BT PAN interface

    <a id="_CPPv4N10netif_if_t12NETIF_IF_PPPE"></a>

    <a id="_CPPv3N10netif_if_t12NETIF_IF_PPPE"></a> <a id="_CPPv2N10netif_if_t12NETIF_IF_PPPE"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266ea32909e433131d7e734ecba9de2904d51"></a> enumerator NETIF\_IF\_PPP
    :   PPP interface

    <a id="_CPPv4N10netif_if_t14NETIF_IF_MODEME"></a>

    <a id="_CPPv3N10netif_if_t14NETIF_IF_MODEME"></a> <a id="_CPPv2N10netif_if_t14NETIF_IF_MODEME"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266eaabc82a3ab580a1ca625737e3b18fdf33"></a> enumerator NETIF\_IF\_MODEM
    :   MODEM interface

    <a id="_CPPv4N10netif_if_t12NETIF_IF_P2PE"></a>

    <a id="_CPPv3N10netif_if_t12NETIF_IF_P2PE"></a> <a id="_CPPv2N10netif_if_t12NETIF_IF_P2PE"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266ea93ee247428f32b6d789930b17b6bb56c"></a> enumerator NETIF\_IF\_P2P
    :   WiFi P2P interface

    <a id="_CPPv4N10netif_if_t14NETIF_IF_COUNTE"></a>

    <a id="_CPPv3N10netif_if_t14NETIF_IF_COUNTE"></a> <a id="_CPPv2N10netif_if_t14NETIF_IF_COUNTE"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266eaac5e277f9669fb8db044fcb3ac33b237"></a> enumerator NETIF\_IF\_COUNT
    :   Number of BK netif

    <a id="_CPPv4N10netif_if_t16NETIF_IF_INVALIDE"></a>

    <a id="_CPPv3N10netif_if_t16NETIF_IF_INVALIDE"></a> <a id="_CPPv2N10netif_if_t16NETIF_IF_INVALIDE"></a> <a id="group__bk__api__netif__typedef_1ggafd0e8f6d2cd5550a97425b19e844266eac6a9cc0e75a493b3f06f729393896f31"></a> enumerator NETIF\_IF\_INVALID
    :   Invalid BK netif

<a id="_CPPv413netif_event_t"></a>

<a id="_CPPv313netif_event_t"></a> <a id="_CPPv213netif_event_t"></a> <a id="group__bk__api__netif__typedef_1gaee42e295fc1554aa4e1a496eca95bdb1"></a> enum netif\_event\_t
:   *Values:*

    <a id="_CPPv4N13netif_event_t19EVENT_NETIF_GOT_IP4E"></a>

    <a id="_CPPv3N13netif_event_t19EVENT_NETIF_GOT_IP4E"></a> <a id="_CPPv2N13netif_event_t19EVENT_NETIF_GOT_IP4E"></a> <a id="group__bk__api__netif__typedef_1ggaee42e295fc1554aa4e1a496eca95bdb1ad73d2fcda5d6a347b3e72364fd1791db"></a> enumerator EVENT\_NETIF\_GOT\_IP4
    :   Netif get IP4 event

    <a id="_CPPv4N13netif_event_t24EVENT_NETIF_DHCP_TIMEOUTE"></a>

    <a id="_CPPv3N13netif_event_t24EVENT_NETIF_DHCP_TIMEOUTE"></a> <a id="_CPPv2N13netif_event_t24EVENT_NETIF_DHCP_TIMEOUTE"></a> <a id="group__bk__api__netif__typedef_1ggaee42e295fc1554aa4e1a496eca95bdb1a1700ebfc3560dd7f451b3feabe0872c0"></a> enumerator EVENT\_NETIF\_DHCP\_TIMEOUT

    <a id="_CPPv4N13netif_event_t22EVENT_NETIF_GOT_IP6_LLE"></a>

    <a id="_CPPv3N13netif_event_t22EVENT_NETIF_GOT_IP6_LLE"></a> <a id="_CPPv2N13netif_event_t22EVENT_NETIF_GOT_IP6_LLE"></a> <a id="group__bk__api__netif__typedef_1ggaee42e295fc1554aa4e1a496eca95bdb1a50c705b8883e3fbadc2f0eb4d1dac0b0"></a> enumerator EVENT\_NETIF\_GOT\_IP6\_LL
    :   get IP4 addr timeout, 20s Netif get IP6 link-local event

    <a id="_CPPv4N13netif_event_t26EVENT_NETIF_GOT_IP6_GLOBALE"></a>

    <a id="_CPPv3N13netif_event_t26EVENT_NETIF_GOT_IP6_GLOBALE"></a> <a id="_CPPv2N13netif_event_t26EVENT_NETIF_GOT_IP6_GLOBALE"></a> <a id="group__bk__api__netif__typedef_1ggaee42e295fc1554aa4e1a496eca95bdb1a328799ad7fe1928a5b573d104b262980"></a> enumerator EVENT\_NETIF\_GOT\_IP6\_GLOBAL
    :   Netif get IP6 global or ULA event
