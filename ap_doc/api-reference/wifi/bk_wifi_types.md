---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/wifi/bk_wifi_types.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wi-fi"></a>

# Wi-Fi 类型定义

`ap/include/modules/wifi_types.h` 定义 Wi-Fi 配置结构体、事件数据、错误码及默认配置宏（如 `WIFI_DEFAULT_STA_CONFIG`）。

<a id="wifi-types-h"></a>

## wifi\_types.h

<a id="header-file"></a>

### Header File

- [wifi\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/modules/wifi_types.h)

<a id="functions"></a>

### Functions

<a id="_CPPv433wifi_rlk_scan_get_register_cfm_cbv"></a>

<a id="_CPPv333wifi_rlk_scan_get_register_cfm_cbv"></a> <a id="_CPPv233wifi_rlk_scan_get_register_cfm_cbv"></a> <a id="wifi_rlk_scan_get_register_cfm_cb__void"></a> <a id="group__bk__api__wifi__v2__typedef_1ga758681738923281405e4cef9601dc56f"></a> [wifi\_rlk\_scan\_cfm\_cb\_t](#_CPPv422wifi_rlk_scan_cfm_cb_t "wifi_rlk_scan_cfm_cb_t") wifi\_rlk\_scan\_get\_register\_cfm\_cb(void)

<a id="structures"></a>

### Structures

<a id="_CPPv418wifi_init_config_t"></a>

<a id="_CPPv318wifi_init_config_t"></a> <a id="_CPPv218wifi_init_config_t"></a> <a id="wifi_init_config_t"></a> <a id="structwifi__init__config__t"></a> struct wifi\_init\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18wifi_init_config_t8featuresE"></a>

    <a id="_CPPv3N18wifi_init_config_t8featuresE"></a> <a id="_CPPv2N18wifi_init_config_t8featuresE"></a> <a id="wifi_init_config_t::features__uint64_t"></a> <a id="group__bk__api__wifi__v2_1gae9f99f3b03f67d5c39a0e20f901bd08b"></a> uint64\_t features
    :   WiFi feature bitmaps

    <a id="_CPPv4N18wifi_init_config_t8os_funcsE"></a>

    <a id="_CPPv3N18wifi_init_config_t8os_funcsE"></a> <a id="_CPPv2N18wifi_init_config_t8os_funcsE"></a> <a id="wifi_init_config_t::os_funcs__voidP"></a> <a id="group__bk__api__wifi__v2_1ga06ba2b0c66e5abe4f5edd681a0715716"></a> void \*os\_funcs
    :   WiFi OS functions

    <a id="_CPPv4N18wifi_init_config_t6os_valE"></a>

    <a id="_CPPv3N18wifi_init_config_t6os_valE"></a> <a id="_CPPv2N18wifi_init_config_t6os_valE"></a> <a id="wifi_init_config_t::os_val__voidP"></a> <a id="group__bk__api__wifi__v2_1gaa65b53e6647ab9a642a6d982c6da3f11"></a> void \*os\_val
    :   WiFI Values

    <a id="_CPPv4N18wifi_init_config_t8reservedE"></a>

    <a id="_CPPv3N18wifi_init_config_t8reservedE"></a> <a id="_CPPv2N18wifi_init_config_t8reservedE"></a> <a id="wifi_init_config_t::reserved__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga85267c94d0e747b3d001848dadda318b"></a> uint8\_t reserved\[16\]
    :   Reserved

<a id="_CPPv414wifi_channel_t"></a>

<a id="_CPPv314wifi_channel_t"></a> <a id="_CPPv214wifi_channel_t"></a> <a id="wifi_channel_t"></a> <a id="structwifi__channel__t"></a> struct wifi\_channel\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14wifi_channel_t7primaryE"></a>

    <a id="_CPPv3N14wifi_channel_t7primaryE"></a> <a id="_CPPv2N14wifi_channel_t7primaryE"></a> <a id="wifi_channel_t::primary__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga2753b11986e9c2876a93c8c4d8261b77"></a> uint8\_t primary
    :   Primary channel

    <a id="_CPPv4N14wifi_channel_t6secondE"></a>

    <a id="_CPPv3N14wifi_channel_t6secondE"></a> <a id="_CPPv2N14wifi_channel_t6secondE"></a> <a id="wifi_channel_t::second__wifi_second_channel_t"></a> <a id="group__bk__api__wifi__v2_1gaddd0b1028bfc9310ee2152a40c4df386"></a> [wifi\_second\_channel\_t](#_CPPv421wifi_second_channel_t "wifi_second_channel_t") second
    :   Secondary cahnnel

<a id="_CPPv47bk_vise"></a>

<a id="_CPPv37bk_vise"></a> <a id="_CPPv27bk_vise"></a> <a id="bk_vise"></a> <a id="structbk__vise"></a> struct bk\_vise

<a id="_CPPv417wifi_sta_config_t"></a>

<a id="_CPPv317wifi_sta_config_t"></a> <a id="_CPPv217wifi_sta_config_t"></a> <a id="wifi_sta_config_t"></a> <a id="structwifi__sta__config__t"></a> struct wifi\_sta\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17wifi_sta_config_t4ssidE"></a>

    <a id="_CPPv3N17wifi_sta_config_t4ssidE"></a> <a id="_CPPv2N17wifi_sta_config_t4ssidE"></a> <a id="wifi_sta_config_t::ssid__cA"></a> <a id="group__bk__api__wifi__v2_1ga173955fd4b6debbf470dcee831f82fe5"></a> char ssid\[WIFI\_SSID\_STR\_LEN\]
    :   SSID of AP to be connected

    <a id="_CPPv4N17wifi_sta_config_t5bssidE"></a>

    <a id="_CPPv3N17wifi_sta_config_t5bssidE"></a> <a id="_CPPv2N17wifi_sta_config_t5bssidE"></a> <a id="wifi_sta_config_t::bssid__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1gaf4c854d9f2fe90367777324fea95fc63"></a> uint8\_t bssid\[WIFI\_BSSID\_LEN\]
    :   BSSID of AP to be connected, fast connect only

    <a id="_CPPv4N17wifi_sta_config_t7channelE"></a>

    <a id="_CPPv3N17wifi_sta_config_t7channelE"></a> <a id="_CPPv2N17wifi_sta_config_t7channelE"></a> <a id="wifi_sta_config_t::channel__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga2cc86d1fa7e6aeebdfbc73068c19cbf7"></a> uint8\_t channel
    :   Primary channel of AP to be connected, fast connect only

    <a id="_CPPv4N17wifi_sta_config_t8securityE"></a>

    <a id="_CPPv3N17wifi_sta_config_t8securityE"></a> <a id="_CPPv2N17wifi_sta_config_t8securityE"></a> <a id="wifi_sta_config_t::security__wifi_security_t"></a> <a id="group__bk__api__wifi__v2_1gac23fbfa8a5f39e98bf8d42b9817a0b50"></a> [wifi\_security\_t](#_CPPv415wifi_security_t "wifi_security_t") security
    :   Security of AP to be connected

    <a id="_CPPv4N17wifi_sta_config_t8passwordE"></a>

    <a id="_CPPv3N17wifi_sta_config_t8passwordE"></a> <a id="_CPPv2N17wifi_sta_config_t8passwordE"></a> <a id="wifi_sta_config_t::password__cA"></a> <a id="group__bk__api__wifi__v2_1ga6a0700a6d3655cb0eb38453cadf15660"></a> char password\[WIFI\_PASSWORD\_LEN\]
    :   Security key or PMK of the wlan.

    <a id="_CPPv4N17wifi_sta_config_t3pskE"></a>

    <a id="_CPPv3N17wifi_sta_config_t3pskE"></a> <a id="_CPPv2N17wifi_sta_config_t3pskE"></a> <a id="wifi_sta_config_t::psk__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga18b5d00cb081bc70f9dcdfb167ae8a26"></a> uint8\_t psk\[WIFI\_PASSWORD\_LEN\]
    :   PSK of AP

    <a id="_CPPv4N17wifi_sta_config_t7ip_addrE"></a>

    <a id="_CPPv3N17wifi_sta_config_t7ip_addrE"></a> <a id="_CPPv2N17wifi_sta_config_t7ip_addrE"></a> <a id="wifi_sta_config_t::ip_addr__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1gafbc13d80f3fdb95399228cd9eefa2264"></a> uint8\_t ip\_addr\[4\]
    :   IP address

    <a id="_CPPv4N17wifi_sta_config_t7netmaskE"></a>

    <a id="_CPPv3N17wifi_sta_config_t7netmaskE"></a> <a id="_CPPv2N17wifi_sta_config_t7netmaskE"></a> <a id="wifi_sta_config_t::netmask__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga04415fbf53ad2856e2e67c6028d85d63"></a> uint8\_t netmask\[4\]
    :   NET address

    <a id="_CPPv4N17wifi_sta_config_t2gwE"></a>

    <a id="_CPPv3N17wifi_sta_config_t2gwE"></a> <a id="_CPPv2N17wifi_sta_config_t2gwE"></a> <a id="wifi_sta_config_t::gw__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1gac4f04c29a35bf6daba23e83b762b74e3"></a> uint8\_t gw\[4\]
    :   GW address

    <a id="_CPPv4N17wifi_sta_config_t4dns1E"></a>

    <a id="_CPPv3N17wifi_sta_config_t4dns1E"></a> <a id="_CPPv2N17wifi_sta_config_t4dns1E"></a> <a id="wifi_sta_config_t::dns1__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga713bc11340fc5d6316e2c35e1b1c4cb8"></a> uint8\_t dns1\[4\]
    :   DNS address

    <a id="_CPPv4N17wifi_sta_config_t23is_not_support_auto_fciE"></a>

    <a id="_CPPv3N17wifi_sta_config_t23is_not_support_auto_fciE"></a> <a id="_CPPv2N17wifi_sta_config_t23is_not_support_auto_fciE"></a> <a id="wifi_sta_config_t::is_not_support_auto_fci__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga55f295affe3bf20a237d624ca251858e"></a> uint8\_t is\_not\_support\_auto\_fci
    :   is not support auto fast connect

    <a id="_CPPv4N17wifi_sta_config_t20is_user_fast_connectE"></a>

    <a id="_CPPv3N17wifi_sta_config_t20is_user_fast_connectE"></a> <a id="_CPPv2N17wifi_sta_config_t20is_user_fast_connectE"></a> <a id="wifi_sta_config_t::is_user_fast_connect__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gacd6b220c8e41f8c57196cf3275782d1a"></a> uint8\_t is\_user\_fast\_connect
    :   is use user fast connect

    <a id="_CPPv4N17wifi_sta_config_t3pmfE"></a>

    <a id="_CPPv3N17wifi_sta_config_t3pmfE"></a> <a id="_CPPv2N17wifi_sta_config_t3pmfE"></a> <a id="wifi_sta_config_t::pmf__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gaff5c71052eeb8d2423993fa916a0446c"></a> uint8\_t pmf
    :   is support pmf

    <a id="_CPPv4N17wifi_sta_config_t2tkE"></a>

    <a id="_CPPv3N17wifi_sta_config_t2tkE"></a> <a id="_CPPv2N17wifi_sta_config_t2tkE"></a> <a id="wifi_sta_config_t::tk__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga79b2248b38ac81032f908df700a6d5d4"></a> uint8\_t tk\[16\]
    :   WPA3 tk key

    <a id="_CPPv4N17wifi_sta_config_t7pmk_lenE"></a>

    <a id="_CPPv3N17wifi_sta_config_t7pmk_lenE"></a> <a id="_CPPv2N17wifi_sta_config_t7pmk_lenE"></a> <a id="wifi_sta_config_t::pmk_len__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga2c624c781b0911bb4786211001df76af"></a> uint8\_t pmk\_len
    :   SAE PMK length

    <a id="_CPPv4N17wifi_sta_config_t3pmkE"></a>

    <a id="_CPPv3N17wifi_sta_config_t3pmkE"></a> <a id="_CPPv2N17wifi_sta_config_t3pmkE"></a> <a id="wifi_sta_config_t::pmk__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga8ca1352453290546770c13fd7e7a6bad"></a> uint8\_t pmk\[64\]
    :   SAE PMK

    <a id="_CPPv4N17wifi_sta_config_t5pmkidE"></a>

    <a id="_CPPv3N17wifi_sta_config_t5pmkidE"></a> <a id="_CPPv2N17wifi_sta_config_t5pmkidE"></a> <a id="wifi_sta_config_t::pmkid__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1gaa8931c99f537db4306e2c5cd142131b8"></a> uint8\_t pmkid\[16\]
    :   SAE PMKID

    <a id="_CPPv4N17wifi_sta_config_t4akmpE"></a>

    <a id="_CPPv3N17wifi_sta_config_t4akmpE"></a> <a id="_CPPv2N17wifi_sta_config_t4akmpE"></a> <a id="wifi_sta_config_t::akmp__i"></a> <a id="group__bk__api__wifi__v2_1ga5b4a7db959efd7b25ef9237b665ad5c8"></a> int akmp
    :   key mgmt (e.g. WPA\_KEY\_MGMT\_SAE)

    <a id="_CPPv4N17wifi_sta_config_t20auto_reconnect_countE"></a>

    <a id="_CPPv3N17wifi_sta_config_t20auto_reconnect_countE"></a> <a id="_CPPv2N17wifi_sta_config_t20auto_reconnect_countE"></a> <a id="wifi_sta_config_t::auto_reconnect_count__i"></a> <a id="group__bk__api__wifi__v2_1ga7a9d2fe502ba1e58ca5d7595dbc2a502"></a> int auto\_reconnect\_count
    :   auto reconnect max count, 0 for always reconnect

    <a id="_CPPv4N17wifi_sta_config_t22auto_reconnect_timeoutE"></a>

    <a id="_CPPv3N17wifi_sta_config_t22auto_reconnect_timeoutE"></a> <a id="_CPPv2N17wifi_sta_config_t22auto_reconnect_timeoutE"></a> <a id="wifi_sta_config_t::auto_reconnect_timeout__i"></a> <a id="group__bk__api__wifi__v2_1gae5f74786c5667ad5f0bb1ad862688e49"></a> int auto\_reconnect\_timeout
    :   auto reconnect timeout in secs, 0 for no timeout

    <a id="_CPPv4N17wifi_sta_config_t39disable_auto_reconnect_after_disconnectE"></a>

    <a id="_CPPv3N17wifi_sta_config_t39disable_auto_reconnect_after_disconnectE"></a> <a id="_CPPv2N17wifi_sta_config_t39disable_auto_reconnect_after_disconnectE"></a> <a id="wifi_sta_config_t::disable_auto_reconnect_after_disconnect__b"></a> <a id="group__bk__api__wifi__v2_1gacd8a95fa035752187cbcfc388d0df9f6"></a> bool disable\_auto\_reconnect\_after\_disconnect
    :   disable auto reconnect if deauth/disassoc by AP when in connected state

    <a id="_CPPv4N17wifi_sta_config_t8reservedE"></a>

    <a id="_CPPv3N17wifi_sta_config_t8reservedE"></a> <a id="_CPPv2N17wifi_sta_config_t8reservedE"></a> <a id="wifi_sta_config_t::reserved__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga2d40ae19dd768487ecdf0fa5b09c2f7c"></a> uint8\_t reserved\[32\]
    :   reserved, **must set to 0**

<a id="_CPPv423wifi_linkstate_reason_t"></a>

<a id="_CPPv323wifi_linkstate_reason_t"></a> <a id="_CPPv223wifi_linkstate_reason_t"></a> <a id="wifi_linkstate_reason_t"></a> <a id="structwifi__linkstate__reason__t"></a> struct wifi\_linkstate\_reason\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23wifi_linkstate_reason_t5stateE"></a>

    <a id="_CPPv3N23wifi_linkstate_reason_t5stateE"></a> <a id="_CPPv2N23wifi_linkstate_reason_t5stateE"></a> <a id="wifi_linkstate_reason_t::state__wifi_link_state_t"></a> <a id="group__bk__api__wifi__v2_1ga29e61eb4dd05859b9598bf6d36edca39"></a> [wifi\_link\_state\_t](#_CPPv417wifi_link_state_t "wifi_link_state_t") state
    :   Wifi linkstate

    <a id="_CPPv4N23wifi_linkstate_reason_t11reason_codeE"></a>

    <a id="_CPPv3N23wifi_linkstate_reason_t11reason_codeE"></a> <a id="_CPPv2N23wifi_linkstate_reason_t11reason_codeE"></a> <a id="wifi_linkstate_reason_t::reason_code__wifi_err_reason_t"></a> <a id="group__bk__api__wifi__v2_1ga626b24ac39702a34da66ab39b941a62c"></a> [wifi\_err\_reason\_t](#_CPPv417wifi_err_reason_t "wifi_err_reason_t") reason\_code
    :   Wifi disconnect reason code, success will be WIFI\_REASON\_MAX

<a id="_CPPv418wifi_link_status_t"></a>

<a id="_CPPv318wifi_link_status_t"></a> <a id="_CPPv218wifi_link_status_t"></a> <a id="wifi_link_status_t"></a> <a id="structwifi__link__status__t"></a> struct wifi\_link\_status\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18wifi_link_status_t5stateE"></a>

    <a id="_CPPv3N18wifi_link_status_t5stateE"></a> <a id="_CPPv2N18wifi_link_status_t5stateE"></a> <a id="wifi_link_status_t::state__wifi_link_state_t"></a> <a id="group__bk__api__wifi__v2_1gae2217f198571149fd1ea194e2987fa9a"></a> [wifi\_link\_state\_t](#_CPPv417wifi_link_state_t "wifi_link_state_t") state
    :   The WiFi connection status

    <a id="_CPPv4N18wifi_link_status_t3aidE"></a>

    <a id="_CPPv3N18wifi_link_status_t3aidE"></a> <a id="_CPPv2N18wifi_link_status_t3aidE"></a> <a id="wifi_link_status_t::aid__i"></a> <a id="group__bk__api__wifi__v2_1gaf7f1f46b82ff710670cab9ff4fb6d89b"></a> int aid
    :   STA AID

    <a id="_CPPv4N18wifi_link_status_t4rssiE"></a>

    <a id="_CPPv3N18wifi_link_status_t4rssiE"></a> <a id="_CPPv2N18wifi_link_status_t4rssiE"></a> <a id="wifi_link_status_t::rssi__i"></a> <a id="group__bk__api__wifi__v2_1ga726485b304bcbeacf81e8c199e4d9650"></a> int rssi
    :   The RSSI of AP the BK STA is connected

    <a id="_CPPv4N18wifi_link_status_t4ssidE"></a>

    <a id="_CPPv3N18wifi_link_status_t4ssidE"></a> <a id="_CPPv2N18wifi_link_status_t4ssidE"></a> <a id="wifi_link_status_t::ssid__cA"></a> <a id="group__bk__api__wifi__v2_1ga931982c6fb3f4b31f23bcb0f301fff23"></a> char ssid\[WIFI\_SSID\_STR\_LEN\]
    :   SSID of AP the BK STA is connected

    <a id="_CPPv4N18wifi_link_status_t5bssidE"></a>

    <a id="_CPPv3N18wifi_link_status_t5bssidE"></a> <a id="_CPPv2N18wifi_link_status_t5bssidE"></a> <a id="wifi_link_status_t::bssid__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga931ec371d60d095e55035f9601a032aa"></a> uint8\_t bssid\[WIFI\_BSSID\_LEN\]
    :   BSSID of AP the BK STA is connected

    <a id="_CPPv4N18wifi_link_status_t7channelE"></a>

    <a id="_CPPv3N18wifi_link_status_t7channelE"></a> <a id="_CPPv2N18wifi_link_status_t7channelE"></a> <a id="wifi_link_status_t::channel__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga2e6648f0d5426138954d395d3c181c83"></a> uint8\_t channel
    :   Primary channel of AP the BK STA is connected

    <a id="_CPPv4N18wifi_link_status_t8securityE"></a>

    <a id="_CPPv3N18wifi_link_status_t8securityE"></a> <a id="_CPPv2N18wifi_link_status_t8securityE"></a> <a id="wifi_link_status_t::security__wifi_security_t"></a> <a id="group__bk__api__wifi__v2_1ga1932604f49a07b22ba838dd0dd1da52c"></a> [wifi\_security\_t](#_CPPv415wifi_security_t "wifi_security_t") security
    :   Security of AP the BK STA is connected

    <a id="_CPPv4N18wifi_link_status_t8passwordE"></a>

    <a id="_CPPv3N18wifi_link_status_t8passwordE"></a> <a id="_CPPv2N18wifi_link_status_t8passwordE"></a> <a id="wifi_link_status_t::password__cA"></a> <a id="group__bk__api__wifi__v2_1ga412b62929f6c157e3ae980111bd41317"></a> char password\[WIFI\_PASSWORD\_LEN\]
    :   Passord of AP the BK STA is connected

<a id="_CPPv418wifi_scan_config_t"></a>

<a id="_CPPv318wifi_scan_config_t"></a> <a id="_CPPv218wifi_scan_config_t"></a> <a id="wifi_scan_config_t"></a> <a id="structwifi__scan__config__t"></a> struct wifi\_scan\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18wifi_scan_config_t4ssidE"></a>

    <a id="_CPPv3N18wifi_scan_config_t4ssidE"></a> <a id="_CPPv2N18wifi_scan_config_t4ssidE"></a> <a id="wifi_scan_config_t::ssid__cA"></a> <a id="group__bk__api__wifi__v2_1gace0f6592172fb7045603763e5691ac8a"></a> char ssid\[WIFI\_SSID\_STR\_LEN\]
    :   SSID to be scaned

    <a id="_CPPv4N18wifi_scan_config_t9scan_typeE"></a>

    <a id="_CPPv3N18wifi_scan_config_t9scan_typeE"></a> <a id="_CPPv2N18wifi_scan_config_t9scan_typeE"></a> <a id="wifi_scan_config_t::scan_type__u8"></a> <a id="group__bk__api__wifi__v2_1gaec9deac988493bc07f155f9605abef38"></a> u8 scan\_type
    :   0: active scan; 1: passive scan

    <a id="_CPPv4N18wifi_scan_config_t8chan_cntE"></a>

    <a id="_CPPv3N18wifi_scan_config_t8chan_cntE"></a> <a id="_CPPv2N18wifi_scan_config_t8chan_cntE"></a> <a id="wifi_scan_config_t::chan_cnt__u8"></a> <a id="group__bk__api__wifi__v2_1gaed43400cea3a9a05f3871514068869fa"></a> u8 chan\_cnt
    :   scan channel cnt

    <a id="_CPPv4N18wifi_scan_config_t7chan_nbE"></a>

    <a id="_CPPv3N18wifi_scan_config_t7chan_nbE"></a> <a id="_CPPv2N18wifi_scan_config_t7chan_nbE"></a> <a id="wifi_scan_config_t::chan_nb__u8A"></a> <a id="group__bk__api__wifi__v2_1ga24778fba9ded56ca8eaad50d30d04706"></a> u8 chan\_nb\[WIFI\_2BAND\_MAX\_CHAN\_NUM\]
    :   scan channel number 2.4g\+5g

    <a id="_CPPv4N18wifi_scan_config_t8durationE"></a>

    <a id="_CPPv3N18wifi_scan_config_t8durationE"></a> <a id="_CPPv2N18wifi_scan_config_t8durationE"></a> <a id="wifi_scan_config_t::duration__u32"></a> <a id="group__bk__api__wifi__v2_1ga213bbb8221eb054e2cdee0f88eeadecf"></a> u32 duration
    :   scan duration,ms

<a id="_CPPv419wifi_scan_ap_info_t"></a>

<a id="_CPPv319wifi_scan_ap_info_t"></a> <a id="_CPPv219wifi_scan_ap_info_t"></a> <a id="wifi_scan_ap_info_t"></a> <a id="structwifi__scan__ap__info__t"></a> struct wifi\_scan\_ap\_info\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19wifi_scan_ap_info_t4ssidE"></a>

    <a id="_CPPv3N19wifi_scan_ap_info_t4ssidE"></a> <a id="_CPPv2N19wifi_scan_ap_info_t4ssidE"></a> <a id="wifi_scan_ap_info_t::ssid__cA"></a> <a id="group__bk__api__wifi__v2_1gaa4c204effe106eddb1aeb5ef9c8b25d2"></a> char ssid\[WIFI\_SSID\_STR\_LEN\]
    :   SSID of AP found by scan

    <a id="_CPPv4N19wifi_scan_ap_info_t5bssidE"></a>

    <a id="_CPPv3N19wifi_scan_ap_info_t5bssidE"></a> <a id="_CPPv2N19wifi_scan_ap_info_t5bssidE"></a> <a id="wifi_scan_ap_info_t::bssid__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1gae3869d94dd1302a1c6f190f5f7f8995a"></a> uint8\_t bssid\[WIFI\_BSSID\_LEN\]
    :   BSSID of AP found by scan

    <a id="_CPPv4N19wifi_scan_ap_info_t4rssiE"></a>

    <a id="_CPPv3N19wifi_scan_ap_info_t4rssiE"></a> <a id="_CPPv2N19wifi_scan_ap_info_t4rssiE"></a> <a id="wifi_scan_ap_info_t::rssi__i"></a> <a id="group__bk__api__wifi__v2_1ga355b6900c5c6e658a5fdcb17d96f67ad"></a> int rssi
    :   RSSI of AP found by scan

    <a id="_CPPv4N19wifi_scan_ap_info_t7channelE"></a>

    <a id="_CPPv3N19wifi_scan_ap_info_t7channelE"></a> <a id="_CPPv2N19wifi_scan_ap_info_t7channelE"></a> <a id="wifi_scan_ap_info_t::channel__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gae4819d917122c72c505dc3240199d28e"></a> uint8\_t channel
    :   The channel of the AP found by scan

    <a id="_CPPv4N19wifi_scan_ap_info_t8securityE"></a>

    <a id="_CPPv3N19wifi_scan_ap_info_t8securityE"></a> <a id="_CPPv2N19wifi_scan_ap_info_t8securityE"></a> <a id="wifi_scan_ap_info_t::security__wifi_security_t"></a> <a id="group__bk__api__wifi__v2_1gad11455feb4df0ac53c237f659d8b9e4d"></a> [wifi\_security\_t](#_CPPv415wifi_security_t "wifi_security_t") security
    :   The security type of the AP found by scan

    <a id="_CPPv4N19wifi_scan_ap_info_t8reservedE"></a>

    <a id="_CPPv3N19wifi_scan_ap_info_t8reservedE"></a> <a id="_CPPv2N19wifi_scan_ap_info_t8reservedE"></a> <a id="wifi_scan_ap_info_t::reserved__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga03022794ede1f6e1b2b472fd4f7d8c9e"></a> uint8\_t reserved\[16\]
    :   Reserved, **must be zero**

<a id="_CPPv418wifi_scan_result_t"></a>

<a id="_CPPv318wifi_scan_result_t"></a> <a id="_CPPv218wifi_scan_result_t"></a> <a id="wifi_scan_result_t"></a> <a id="structwifi__scan__result__t"></a> struct wifi\_scan\_result\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18wifi_scan_result_t6ap_numE"></a>

    <a id="_CPPv3N18wifi_scan_result_t6ap_numE"></a> <a id="_CPPv2N18wifi_scan_result_t6ap_numE"></a> <a id="wifi_scan_result_t::ap_num__i"></a> <a id="group__bk__api__wifi__v2_1gababf0f253ac248d67f7dd25db0452287"></a> int ap\_num
    :   The number of AP found by scan

    <a id="_CPPv4N18wifi_scan_result_t3apsE"></a>

    <a id="_CPPv3N18wifi_scan_result_t3apsE"></a> <a id="_CPPv2N18wifi_scan_result_t3apsE"></a> <a id="wifi_scan_result_t::aps__wifi_scan_ap_info_tP"></a> <a id="group__bk__api__wifi__v2_1gafc7ec251f26525956b4d710092012c04"></a> [wifi\_scan\_ap\_info\_t](#_CPPv419wifi_scan_ap_info_t "wifi_scan_ap_info_t") \*aps
    :   The APs found by scan

<a id="_CPPv416wifi_ap_config_t"></a>

<a id="_CPPv316wifi_ap_config_t"></a> <a id="_CPPv216wifi_ap_config_t"></a> <a id="wifi_ap_config_t"></a> <a id="structwifi__ap__config__t"></a> struct wifi\_ap\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16wifi_ap_config_t4ssidE"></a>

    <a id="_CPPv3N16wifi_ap_config_t4ssidE"></a> <a id="_CPPv2N16wifi_ap_config_t4ssidE"></a> <a id="wifi_ap_config_t::ssid__cA"></a> <a id="group__bk__api__wifi__v2_1gaa931247a4b99b7bd4f9e364c697533f3"></a> char ssid\[WIFI\_SSID\_STR\_LEN\]
    :   The SSID of BK AP

    <a id="_CPPv4N16wifi_ap_config_t8passwordE"></a>

    <a id="_CPPv3N16wifi_ap_config_t8passwordE"></a> <a id="_CPPv2N16wifi_ap_config_t8passwordE"></a> <a id="wifi_ap_config_t::password__cA"></a> <a id="group__bk__api__wifi__v2_1ga711f1a365b4b3809fa13adcbeae8608d"></a> char password\[WIFI\_PASSWORD\_LEN\]
    :   Password of BK AP, ignored in an open system.

    <a id="_CPPv4N16wifi_ap_config_t7channelE"></a>

    <a id="_CPPv3N16wifi_ap_config_t7channelE"></a> <a id="_CPPv2N16wifi_ap_config_t7channelE"></a> <a id="wifi_ap_config_t::channel__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gab4005256cbe734b1a0b54c6c50609db3"></a> uint8\_t channel
    :   The channel of BK AP, 0 indicates default TODO

    <a id="_CPPv4N16wifi_ap_config_t8securityE"></a>

    <a id="_CPPv3N16wifi_ap_config_t8securityE"></a> <a id="_CPPv2N16wifi_ap_config_t8securityE"></a> <a id="wifi_ap_config_t::security__wifi_security_t"></a> <a id="group__bk__api__wifi__v2_1gaed1f22f0ba8a8d943ed574545a103556"></a> [wifi\_security\_t](#_CPPv415wifi_security_t "wifi_security_t") security
    :   Security type of BK AP, default value TODO

    <a id="_CPPv4N16wifi_ap_config_t6hiddenE"></a>

    <a id="_CPPv3N16wifi_ap_config_t6hiddenE"></a> <a id="_CPPv2N16wifi_ap_config_t6hiddenE"></a> <a id="wifi_ap_config_t::hidden__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga4e43520cd26178b2eb1b537fe04593be"></a> uint8\_t hidden
    :   Whether the BK AP is hidden

    <a id="_CPPv4N16wifi_ap_config_t3acsE"></a>

    <a id="_CPPv3N16wifi_ap_config_t3acsE"></a> <a id="_CPPv2N16wifi_ap_config_t3acsE"></a> <a id="wifi_ap_config_t::acs__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga365e2514f23c988ac1fe5e41a2326e3b"></a> uint8\_t acs
    :   Whether Auto Channel Selection is enabled

    <a id="_CPPv4N16wifi_ap_config_t18disable_dns_serverE"></a>

    <a id="_CPPv3N16wifi_ap_config_t18disable_dns_serverE"></a> <a id="_CPPv2N16wifi_ap_config_t18disable_dns_serverE"></a> <a id="wifi_ap_config_t::disable_dns_server__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gad4047539e5ad41c4dd95d52f6102ea0e"></a> uint8\_t disable\_dns\_server
    :   Whether to disable DNS server

    <a id="_CPPv4N16wifi_ap_config_t8vsie_lenE"></a>

    <a id="_CPPv3N16wifi_ap_config_t8vsie_lenE"></a> <a id="_CPPv2N16wifi_ap_config_t8vsie_lenE"></a> <a id="wifi_ap_config_t::vsie_len__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga70a682fa907176b7a2c044e69204cd67"></a> uint8\_t vsie\_len
    :   Beacon/ProbeResp Vendor Specific IE len

    <a id="_CPPv4N16wifi_ap_config_t4vsieE"></a>

    <a id="_CPPv3N16wifi_ap_config_t4vsieE"></a> <a id="_CPPv2N16wifi_ap_config_t4vsieE"></a> <a id="wifi_ap_config_t::vsie__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1gaaccfac4bdaecd48892a9b40dd0d9376d"></a> uint8\_t vsie\[255\]
    :   Beacon/ProbeResp Vendor Specific IE

    <a id="_CPPv4N16wifi_ap_config_t7max_conE"></a>

    <a id="_CPPv3N16wifi_ap_config_t7max_conE"></a> <a id="_CPPv2N16wifi_ap_config_t7max_conE"></a> <a id="wifi_ap_config_t::max_con__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga116921d43539d5acde0b878b8b0b61bb"></a> uint8\_t max\_con
    :   Max number of stations allowed to connect to BK AP, TODO default value?

    <a id="_CPPv4N16wifi_ap_config_t8reservedE"></a>

    <a id="_CPPv3N16wifi_ap_config_t8reservedE"></a> <a id="_CPPv2N16wifi_ap_config_t8reservedE"></a> <a id="wifi_ap_config_t::reserved__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1gad67b68cd2431f45036aec30c7d48c4ea"></a> uint8\_t reserved\[32\]
    :   Reserved, **must be zero**

<a id="_CPPv411wlan_ap_sta"></a>

<a id="_CPPv311wlan_ap_sta"></a> <a id="_CPPv211wlan_ap_sta"></a> <a id="wlan_ap_sta"></a> <a id="structwlan__ap__sta"></a> struct wlan\_ap\_sta
:   Wlan station information definition.

<a id="_CPPv412wlan_ap_stas"></a>

<a id="_CPPv312wlan_ap_stas"></a> <a id="_CPPv212wlan_ap_stas"></a> <a id="wlan_ap_stas"></a> <a id="structwlan__ap__stas"></a> struct wlan\_ap\_stas
:   Wlan connected stations information definition.

<a id="_CPPv412wlan_ap_vsie"></a>

<a id="_CPPv312wlan_ap_vsie"></a> <a id="_CPPv212wlan_ap_vsie"></a> <a id="wlan_ap_vsie"></a> <a id="structwlan__ap__vsie"></a> struct wlan\_ap\_vsie
:   softap beacon/probe response’s vendor IEs Dynamic change softap’s vendor specific IEs.

<a id="_CPPv413wlan_sta_vsie"></a>

<a id="_CPPv313wlan_sta_vsie"></a> <a id="_CPPv213wlan_sta_vsie"></a> <a id="wlan_sta_vsie"></a> <a id="structwlan__sta__vsie"></a> struct wlan\_sta\_vsie
:   STA vendor IEs for (re)assoc, scan, p2p, p2p go, etc. Dynamic change STA’s vendor specific IEs.

<a id="_CPPv421wifi_monitor_config_t"></a>

<a id="_CPPv321wifi_monitor_config_t"></a> <a id="_CPPv221wifi_monitor_config_t"></a> <a id="wifi_monitor_config_t"></a> <a id="structwifi__monitor__config__t"></a> struct wifi\_monitor\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21wifi_monitor_config_t14rx_mcast_frameE"></a>

    <a id="_CPPv3N21wifi_monitor_config_t14rx_mcast_frameE"></a> <a id="_CPPv2N21wifi_monitor_config_t14rx_mcast_frameE"></a> <a id="wifi_monitor_config_t::rx_mcast_frame__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga11e18caf7431f8dffb6fd9d3f7f8a2d8"></a> uint32\_t rx\_mcast\_frame
    :   Set this bit to enable callback to receive multicast/broadcast

    <a id="_CPPv4N21wifi_monitor_config_t12rx_dup_frameE"></a>

    <a id="_CPPv3N21wifi_monitor_config_t12rx_dup_frameE"></a> <a id="_CPPv2N21wifi_monitor_config_t12rx_dup_frameE"></a> <a id="wifi_monitor_config_t::rx_dup_frame__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga2e2175ad44c90e1604dc2d15282cf3d9"></a> uint32\_t rx\_dup\_frame
    :   Set this bit to enable callback to receive the duplicated

    <a id="_CPPv4N21wifi_monitor_config_t8reservedE"></a>

    <a id="_CPPv3N21wifi_monitor_config_t8reservedE"></a> <a id="_CPPv2N21wifi_monitor_config_t8reservedE"></a> <a id="wifi_monitor_config_t::reserved__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga55182a160c0a3e24d43e8ed4af1e6b97"></a> uint32\_t reserved
    :   Reserved bits, **must set to 0**

<a id="_CPPv417wifi_frame_info_t"></a>

<a id="_CPPv317wifi_frame_info_t"></a> <a id="_CPPv217wifi_frame_info_t"></a> <a id="wifi_frame_info_t"></a> <a id="structwifi__frame__info__t"></a> struct wifi\_frame\_info\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17wifi_frame_info_t4rssiE"></a>

    <a id="_CPPv3N17wifi_frame_info_t4rssiE"></a> <a id="_CPPv2N17wifi_frame_info_t4rssiE"></a> <a id="wifi_frame_info_t::rssi__i"></a> <a id="group__bk__api__wifi__v2_1ga6aff7f1e26a5ff819a3409d77e0b5521"></a> int rssi
    :   RSSI of the received frame in monitor mode

    <a id="_CPPv4N17wifi_frame_info_t6tsf_loE"></a>

    <a id="_CPPv3N17wifi_frame_info_t6tsf_loE"></a> <a id="_CPPv2N17wifi_frame_info_t6tsf_loE"></a> <a id="wifi_frame_info_t::tsf_lo__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gada0014a44f4f83a4ebf0a7a5a02942ee"></a> uint32\_t tsf\_lo
    :   Total length for the MPDU transfer

    <a id="_CPPv4N17wifi_frame_info_t6tsf_hiE"></a>

    <a id="_CPPv3N17wifi_frame_info_t6tsf_hiE"></a> <a id="_CPPv2N17wifi_frame_info_t6tsf_hiE"></a> <a id="wifi_frame_info_t::tsf_hi__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga3ea264c6284bdf8f027f77c28e94c986"></a> uint32\_t tsf\_hi
    :   TSF Low

    <a id="_CPPv4N17wifi_frame_info_t8recvec1aE"></a>

    <a id="_CPPv3N17wifi_frame_info_t8recvec1aE"></a> <a id="_CPPv2N17wifi_frame_info_t8recvec1aE"></a> <a id="wifi_frame_info_t::recvec1a__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gae0d333eb5879ed9daac99b9179407543"></a> uint32\_t recvec1a
    :   TSF High

    <a id="_CPPv4N17wifi_frame_info_t8recvec1bE"></a>

    <a id="_CPPv3N17wifi_frame_info_t8recvec1bE"></a> <a id="_CPPv2N17wifi_frame_info_t8recvec1bE"></a> <a id="wifi_frame_info_t::recvec1b__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga6987bcb47b35710458ce14d361276693"></a> uint32\_t recvec1b
    :   Receive Vector 1

    <a id="_CPPv4N17wifi_frame_info_t8recvec1cE"></a>

    <a id="_CPPv3N17wifi_frame_info_t8recvec1cE"></a> <a id="_CPPv2N17wifi_frame_info_t8recvec1cE"></a> <a id="wifi_frame_info_t::recvec1c__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gab9665aa96da68312cbb460de28151bd4"></a> uint32\_t recvec1c
    :   Receive Vector 1

    <a id="_CPPv4N17wifi_frame_info_t8recvec1dE"></a>

    <a id="_CPPv3N17wifi_frame_info_t8recvec1dE"></a> <a id="_CPPv2N17wifi_frame_info_t8recvec1dE"></a> <a id="wifi_frame_info_t::recvec1d__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga47e2615924af549eb291336b8fc3d8c7"></a> uint32\_t recvec1d
    :   Receive Vector 1

    <a id="_CPPv4N17wifi_frame_info_t8recvec2aE"></a>

    <a id="_CPPv3N17wifi_frame_info_t8recvec2aE"></a> <a id="_CPPv2N17wifi_frame_info_t8recvec2aE"></a> <a id="wifi_frame_info_t::recvec2a__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga60215dd424e32f2a7ceadfa5b649023c"></a> uint32\_t recvec2a
    :   Receive Vector 1

    <a id="_CPPv4N17wifi_frame_info_t8recvec2bE"></a>

    <a id="_CPPv3N17wifi_frame_info_t8recvec2bE"></a> <a id="_CPPv2N17wifi_frame_info_t8recvec2bE"></a> <a id="wifi_frame_info_t::recvec2b__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga7ab1c5ff3511be53769795a05b238268"></a> uint32\_t recvec2b
    :   Receive Vector 2

    <a id="_CPPv4N17wifi_frame_info_t5extraE"></a>

    <a id="_CPPv3N17wifi_frame_info_t5extraE"></a> <a id="_CPPv2N17wifi_frame_info_t5extraE"></a> <a id="wifi_frame_info_t::extra__voidP"></a> <a id="group__bk__api__wifi__v2_1ga4e37f0f729e51d7287a48d96f376066b"></a> void \*extra
    :   Receive Vector 2 extra info of this frame

<a id="_CPPv418wifi_rlk_chan_info"></a>

<a id="_CPPv318wifi_rlk_chan_info"></a> <a id="_CPPv218wifi_rlk_chan_info"></a> <a id="wifi_rlk_chan_info"></a> <a id="structwifi__rlk__chan__info"></a> struct wifi\_rlk\_chan\_info
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18wifi_rlk_chan_info4freqE"></a>

    <a id="_CPPv3N18wifi_rlk_chan_info4freqE"></a> <a id="_CPPv2N18wifi_rlk_chan_info4freqE"></a> <a id="wifi_rlk_chan_info::freq__uint16_t"></a> <a id="group__bk__api__wifi__v2_1ga7c1462fe97e388cb8d4e3f9e37be6646"></a> uint16\_t freq
    :   Frequency of the channel.

    <a id="_CPPv4N18wifi_rlk_chan_info9noise_dbmE"></a>

    <a id="_CPPv3N18wifi_rlk_chan_info9noise_dbmE"></a> <a id="_CPPv2N18wifi_rlk_chan_info9noise_dbmE"></a> <a id="wifi_rlk_chan_info::noise_dbm__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga71838c4db2e6c7cc1291950e256a2999"></a> uint8\_t noise\_dbm
    :   Noise in dbm.

    <a id="_CPPv4N18wifi_rlk_chan_info12chan_time_msE"></a>

    <a id="_CPPv3N18wifi_rlk_chan_info12chan_time_msE"></a> <a id="_CPPv2N18wifi_rlk_chan_info12chan_time_msE"></a> <a id="wifi_rlk_chan_info::chan_time_ms__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga1bed807c7db19d660083dc3b34a68f77"></a> uint32\_t chan\_time\_ms
    :   Amount of time spent of the channel (in ms)

    <a id="_CPPv4N18wifi_rlk_chan_info17chan_time_busy_msE"></a>

    <a id="_CPPv3N18wifi_rlk_chan_info17chan_time_busy_msE"></a> <a id="_CPPv2N18wifi_rlk_chan_info17chan_time_busy_msE"></a> <a id="wifi_rlk_chan_info::chan_time_busy_ms__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gacb6f1d2e071991c57883e997c8f4aa7b"></a> uint32\_t chan\_time\_busy\_ms
    :   Amount of time the primary channel was sensed busy.

<a id="_CPPv418wifi_rlk_base_info"></a>

<a id="_CPPv318wifi_rlk_base_info"></a> <a id="_CPPv218wifi_rlk_base_info"></a> <a id="wifi_rlk_base_info"></a> <a id="structwifi__rlk__base__info"></a> struct wifi\_rlk\_base\_info

<a id="_CPPv420wifi_filter_config_t"></a>

<a id="_CPPv320wifi_filter_config_t"></a> <a id="_CPPv220wifi_filter_config_t"></a> <a id="wifi_filter_config_t"></a> <a id="structwifi__filter__config__t"></a> struct wifi\_filter\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20wifi_filter_config_t19rx_all_default_mgmtE"></a>

    <a id="_CPPv3N20wifi_filter_config_t19rx_all_default_mgmtE"></a> <a id="_CPPv2N20wifi_filter_config_t19rx_all_default_mgmtE"></a> <a id="wifi_filter_config_t::rx_all_default_mgmt__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga687c38bc58f5cdc6077eb33cf3062345"></a> uint32\_t rx\_all\_default\_mgmt
    :   Set the bit to enable the callback to receive all management frame recived by WiFi driver

    <a id="_CPPv4N20wifi_filter_config_t12rx_probe_reqE"></a>

    <a id="_CPPv3N20wifi_filter_config_t12rx_probe_reqE"></a> <a id="_CPPv2N20wifi_filter_config_t12rx_probe_reqE"></a> <a id="wifi_filter_config_t::rx_probe_req__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga4a90c000675f2cf4809dfbbfdc97b1e9"></a> uint32\_t rx\_probe\_req
    :   Set the bit to enable the callback to receive probe request

    <a id="_CPPv4N20wifi_filter_config_t12rx_probe_rspE"></a>

    <a id="_CPPv3N20wifi_filter_config_t12rx_probe_rspE"></a> <a id="_CPPv2N20wifi_filter_config_t12rx_probe_rspE"></a> <a id="wifi_filter_config_t::rx_probe_rsp__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gafe83e7acbd6d9fc4e1f9143440bbcff7"></a> uint32\_t rx\_probe\_rsp
    :   Set the bit to enable the callback to receive probe response

    <a id="_CPPv4N20wifi_filter_config_t13rx_all_beaconE"></a>

    <a id="_CPPv3N20wifi_filter_config_t13rx_all_beaconE"></a> <a id="_CPPv2N20wifi_filter_config_t13rx_all_beaconE"></a> <a id="wifi_filter_config_t::rx_all_beacon__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gafd9a6181c3ccc3c6a5d94d7bf4efe985"></a> uint32\_t rx\_all\_beacon
    :   Set the bit to enable the callback to receive all beacon

    <a id="_CPPv4N20wifi_filter_config_t9rx_actionE"></a>

    <a id="_CPPv3N20wifi_filter_config_t9rx_actionE"></a> <a id="_CPPv2N20wifi_filter_config_t9rx_actionE"></a> <a id="wifi_filter_config_t::rx_action__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gaff61cbdfa1cb9c7735ff255ce9fd9b48"></a> uint32\_t rx\_action
    :   Set the bit to enable the callback to receive action frame

    <a id="_CPPv4N20wifi_filter_config_t8reservedE"></a>

    <a id="_CPPv3N20wifi_filter_config_t8reservedE"></a> <a id="_CPPv2N20wifi_filter_config_t8reservedE"></a> <a id="wifi_filter_config_t::reserved__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga973df8eff99eb428b0c3e929946c3543"></a> uint32\_t reserved
    :   Reserved bits, **must set to 0**

<a id="_CPPv414wifi_country_t"></a>

<a id="_CPPv314wifi_country_t"></a> <a id="_CPPv214wifi_country_t"></a> <a id="wifi_country_t"></a> <a id="structwifi__country__t"></a> struct wifi\_country\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14wifi_country_t2ccE"></a>

    <a id="_CPPv3N14wifi_country_t2ccE"></a> <a id="_CPPv2N14wifi_country_t2ccE"></a> <a id="wifi_country_t::cc__cA"></a> <a id="group__bk__api__wifi__v2_1ga1fd01869f4230eddd580637171e2e5cf"></a> char cc\[3\]
    :   country code string

    <a id="_CPPv4N14wifi_country_t5schanE"></a>

    <a id="_CPPv3N14wifi_country_t5schanE"></a> <a id="_CPPv2N14wifi_country_t5schanE"></a> <a id="wifi_country_t::schan__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gaf260339dd254a65b93a4e1d65576b117"></a> uint8\_t schan
    :   start channel

    <a id="_CPPv4N14wifi_country_t5nchanE"></a>

    <a id="_CPPv3N14wifi_country_t5nchanE"></a> <a id="_CPPv2N14wifi_country_t5nchanE"></a> <a id="wifi_country_t::nchan__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga1c129465b6bf5c803636dc05c21828dd"></a> uint8\_t nchan
    :   total channel number

    <a id="_CPPv4N14wifi_country_t12max_tx_powerE"></a>

    <a id="_CPPv3N14wifi_country_t12max_tx_powerE"></a> <a id="_CPPv2N14wifi_country_t12max_tx_powerE"></a> <a id="wifi_country_t::max_tx_power__int8_t"></a> <a id="group__bk__api__wifi__v2_1ga47a74c0fedee026097b4707efb792632"></a> int8\_t max\_tx\_power
    :   maximum tx power

    <a id="_CPPv4N14wifi_country_t6policyE"></a>

    <a id="_CPPv3N14wifi_country_t6policyE"></a> <a id="_CPPv2N14wifi_country_t6policyE"></a> <a id="wifi_country_t::policy__wifi_country_policy_t"></a> <a id="group__bk__api__wifi__v2_1ga80f2e1485534d43ae527f413d9c3095d"></a> [wifi\_country\_policy\_t](#_CPPv421wifi_country_policy_t "wifi_country_policy_t") policy
    :   country policy

<a id="_CPPv422wifi_event_scan_done_t"></a>

<a id="_CPPv322wifi_event_scan_done_t"></a> <a id="_CPPv222wifi_event_scan_done_t"></a> <a id="wifi_event_scan_done_t"></a> <a id="structwifi__event__scan__done__t"></a> struct wifi\_event\_scan\_done\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22wifi_event_scan_done_t7scan_idE"></a>

    <a id="_CPPv3N22wifi_event_scan_done_t7scan_idE"></a> <a id="_CPPv2N22wifi_event_scan_done_t7scan_idE"></a> <a id="wifi_event_scan_done_t::scan_id__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga20b753514128873656807dde26c25806"></a> uint32\_t scan\_id
    :   Scan ID

    <a id="_CPPv4N22wifi_event_scan_done_t13scan_use_timeE"></a>

    <a id="_CPPv3N22wifi_event_scan_done_t13scan_use_timeE"></a> <a id="_CPPv2N22wifi_event_scan_done_t13scan_use_timeE"></a> <a id="wifi_event_scan_done_t::scan_use_time__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga1f5fce0cd516e7bcda758e6ee8bf12a7"></a> uint32\_t scan\_use\_time
    :   scan time. us

<a id="_CPPv426wifi_event_network_found_t"></a>

<a id="_CPPv326wifi_event_network_found_t"></a> <a id="_CPPv226wifi_event_network_found_t"></a> <a id="wifi_event_network_found_t"></a> <a id="structwifi__event__network__found__t"></a> struct wifi\_event\_network\_found\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N26wifi_event_network_found_t4ssidE"></a>

    <a id="_CPPv3N26wifi_event_network_found_t4ssidE"></a> <a id="_CPPv2N26wifi_event_network_found_t4ssidE"></a> <a id="wifi_event_network_found_t::ssid__cA"></a> <a id="group__bk__api__wifi__v2_1gad59ad54d291e08b2cc012bb52b9c0f5b"></a> char ssid\[WIFI\_SSID\_STR\_LEN\]
    :   SSID found to be connected

    <a id="_CPPv4N26wifi_event_network_found_t5bssidE"></a>

    <a id="_CPPv3N26wifi_event_network_found_t5bssidE"></a> <a id="_CPPv2N26wifi_event_network_found_t5bssidE"></a> <a id="wifi_event_network_found_t::bssid__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga4af63f621b2cfa3dff458547c67d9529"></a> uint8\_t bssid\[WIFI\_BSSID\_LEN\]
    :   BSSID found to be connected

<a id="_CPPv426wifi_event_sta_connected_t"></a>

<a id="_CPPv326wifi_event_sta_connected_t"></a> <a id="_CPPv226wifi_event_sta_connected_t"></a> <a id="wifi_event_sta_connected_t"></a> <a id="structwifi__event__sta__connected__t"></a> struct wifi\_event\_sta\_connected\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N26wifi_event_sta_connected_t4ssidE"></a>

    <a id="_CPPv3N26wifi_event_sta_connected_t4ssidE"></a> <a id="_CPPv2N26wifi_event_sta_connected_t4ssidE"></a> <a id="wifi_event_sta_connected_t::ssid__cA"></a> <a id="group__bk__api__wifi__v2_1gae44a1f398d1e05aa00444cc1aa4aee5a"></a> char ssid\[WIFI\_SSID\_STR\_LEN\]
    :   SSID of connected AP

    <a id="_CPPv4N26wifi_event_sta_connected_t5bssidE"></a>

    <a id="_CPPv3N26wifi_event_sta_connected_t5bssidE"></a> <a id="_CPPv2N26wifi_event_sta_connected_t5bssidE"></a> <a id="wifi_event_sta_connected_t::bssid__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga604d35bc824aa92b370f478c4066ed53"></a> uint8\_t bssid\[WIFI\_BSSID\_LEN\]
    :   BSSID of connected AP

<a id="_CPPv429wifi_event_sta_disconnected_t"></a>

<a id="_CPPv329wifi_event_sta_disconnected_t"></a> <a id="_CPPv229wifi_event_sta_disconnected_t"></a> <a id="wifi_event_sta_disconnected_t"></a> <a id="structwifi__event__sta__disconnected__t"></a> struct wifi\_event\_sta\_disconnected\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N29wifi_event_sta_disconnected_t17disconnect_reasonE"></a>

    <a id="_CPPv3N29wifi_event_sta_disconnected_t17disconnect_reasonE"></a> <a id="_CPPv2N29wifi_event_sta_disconnected_t17disconnect_reasonE"></a> <a id="wifi_event_sta_disconnected_t::disconnect_reason__i"></a> <a id="group__bk__api__wifi__v2_1ga9b210ef1d662b2a29629754f7d507774"></a> int disconnect\_reason
    :   Disconnect reason of BK STA

    <a id="_CPPv4N29wifi_event_sta_disconnected_t15local_generatedE"></a>

    <a id="_CPPv3N29wifi_event_sta_disconnected_t15local_generatedE"></a> <a id="_CPPv2N29wifi_event_sta_disconnected_t15local_generatedE"></a> <a id="wifi_event_sta_disconnected_t::local_generated__b"></a> <a id="group__bk__api__wifi__v2_1ga8bb56bc2b970c2c802ffe11f91899948"></a> bool local\_generated
    :   if disconnect is request by local

<a id="_CPPv425wifi_event_ap_connected_t"></a>

<a id="_CPPv325wifi_event_ap_connected_t"></a> <a id="_CPPv225wifi_event_ap_connected_t"></a> <a id="wifi_event_ap_connected_t"></a> <a id="structwifi__event__ap__connected__t"></a> struct wifi\_event\_ap\_connected\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N25wifi_event_ap_connected_t3macE"></a>

    <a id="_CPPv3N25wifi_event_ap_connected_t3macE"></a> <a id="_CPPv2N25wifi_event_ap_connected_t3macE"></a> <a id="wifi_event_ap_connected_t::mac__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1gaaa082b5a590c648d34a3481b22604d26"></a> uint8\_t mac\[WIFI\_MAC\_LEN\]
    :   MAC of the STA connected to the BK AP

<a id="_CPPv428wifi_event_ap_disconnected_t"></a>

<a id="_CPPv328wifi_event_ap_disconnected_t"></a> <a id="_CPPv228wifi_event_ap_disconnected_t"></a> <a id="wifi_event_ap_disconnected_t"></a> <a id="structwifi__event__ap__disconnected__t"></a> struct wifi\_event\_ap\_disconnected\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N28wifi_event_ap_disconnected_t3macE"></a>

    <a id="_CPPv3N28wifi_event_ap_disconnected_t3macE"></a> <a id="_CPPv2N28wifi_event_ap_disconnected_t3macE"></a> <a id="wifi_event_ap_disconnected_t::mac__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1gadb4e6dc30c213cc53f1e0ab4fb799ea3"></a> uint8\_t mac\[WIFI\_MAC\_LEN\]
    :   MAC of the STA disconnected from the BK AP

<a id="_CPPv422wifi_statistics_info_t"></a>

<a id="_CPPv322wifi_statistics_info_t"></a> <a id="_CPPv222wifi_statistics_info_t"></a> <a id="wifi_statistics_info_t"></a> <a id="structwifi__statistics__info__t"></a> struct wifi\_statistics\_info\_t
:   Wi-Fi Statistic info.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22wifi_statistics_info_t16tx_success_countE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t16tx_success_countE"></a> <a id="_CPPv2N22wifi_statistics_info_t16tx_success_countE"></a> <a id="wifi_statistics_info_t::tx_success_count__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga75fa5f69654b9bd14f88559f2955ad46"></a> uint32\_t tx\_success\_count
    :   Number of TX successes, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t14tx_retry_countE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t14tx_retry_countE"></a> <a id="_CPPv2N22wifi_statistics_info_t14tx_retry_countE"></a> <a id="wifi_statistics_info_t::tx_retry_count__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga2b9d80c7f66c11b6def89cb1153ca7b5"></a> uint32\_t tx\_retry\_count
    :   Number of TX retries, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t13tx_fail_countE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t13tx_fail_countE"></a> <a id="_CPPv2N22wifi_statistics_info_t13tx_fail_countE"></a> <a id="wifi_statistics_info_t::tx_fail_count__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga6024723cccfc6a999a0e4451fe291af5"></a> uint32\_t tx\_fail\_count
    :   Number of TX failures, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t16rx_success_countE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t16rx_success_countE"></a> <a id="_CPPv2N22wifi_statistics_info_t16rx_success_countE"></a> <a id="wifi_statistics_info_t::rx_success_count__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gaefa4726286a6840096833fe24f03a916"></a> uint32\_t rx\_success\_count
    :   Number of RX successes, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t17rx_crcerror_countE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t17rx_crcerror_countE"></a> <a id="_CPPv2N22wifi_statistics_info_t17rx_crcerror_countE"></a> <a id="wifi_statistics_info_t::rx_crcerror_count__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga362dd76a480dfb489e5b87dc3a1e3c13"></a> uint32\_t rx\_crcerror\_count
    :   Number of RX FCS errors, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t15mic_error_countE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t15mic_error_countE"></a> <a id="_CPPv2N22wifi_statistics_info_t15mic_error_countE"></a> <a id="wifi_statistics_info_t::mic_error_count__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga6af2889ba06a3db9487c6e3d48eaa903"></a> uint32\_t mic\_error\_count
    :   Number of MIC errors, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t5noiseE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t5noiseE"></a> <a id="_CPPv2N22wifi_statistics_info_t5noiseE"></a> <a id="wifi_statistics_info_t::noise__int8_t"></a> <a id="group__bk__api__wifi__v2_1gacdedfd5d6f6d16043b919b6ac48197d2"></a> int8\_t noise
    :   Average noise level in dBm, -128 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t7phyrateE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t7phyrateE"></a> <a id="_CPPv2N22wifi_statistics_info_t7phyrateE"></a> <a id="wifi_statistics_info_t::phyrate__uint16_t"></a> <a id="group__bk__api__wifi__v2_1ga8ff500d5044f9a7392a481852dba1c55"></a> uint16\_t phyrate
    :   Maximum used PHY rate, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t6txrateE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t6txrateE"></a> <a id="_CPPv2N22wifi_statistics_info_t6txrateE"></a> <a id="wifi_statistics_info_t::txrate__uint16_t"></a> <a id="group__bk__api__wifi__v2_1ga9df8dbc49bc25de7a40ae3596ddb8a83"></a> uint16\_t txrate
    :   Average used TX rate, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t6rxrateE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t6rxrateE"></a> <a id="_CPPv2N22wifi_statistics_info_t6rxrateE"></a> <a id="wifi_statistics_info_t::rxrate__uint16_t"></a> <a id="group__bk__api__wifi__v2_1ga1718a529576569b810b026c300435acc"></a> uint16\_t rxrate
    :   Average used RX rate, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t4rssiE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t4rssiE"></a> <a id="_CPPv2N22wifi_statistics_info_t4rssiE"></a> <a id="wifi_statistics_info_t::rssi__int8_t"></a> <a id="group__bk__api__wifi__v2_1gac0747e25cd3c89c3f3cd4f598be4385a"></a> int8\_t rssi
    :   Average beacon RSSI in dBm, -128 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t9bandwidthE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t9bandwidthE"></a> <a id="_CPPv2N22wifi_statistics_info_t9bandwidthE"></a> <a id="wifi_statistics_info_t::bandwidth__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gad797fb8d4586f94afbfbe91a56682f0a"></a> uint8\_t bandwidth
    :   Average used bandwidth, 0 if unavailable

    <a id="_CPPv4N22wifi_statistics_info_t13idle_time_perE"></a>

    <a id="_CPPv3N22wifi_statistics_info_t13idle_time_perE"></a> <a id="_CPPv2N22wifi_statistics_info_t13idle_time_perE"></a> <a id="wifi_statistics_info_t::idle_time_per__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga481102f7a5ddf09b8daa5d729a30771d"></a> uint8\_t idle\_time\_per
    :   Percent of idle time, 0 if unavailable

<a id="_CPPv414raw_tx_cntrl_t"></a>

<a id="_CPPv314raw_tx_cntrl_t"></a> <a id="_CPPv214raw_tx_cntrl_t"></a> <a id="raw_tx_cntrl_t"></a> <a id="structraw__tx__cntrl__t"></a> struct raw\_tx\_cntrl\_t
:   Wi-Fi RAW TX control.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14raw_tx_cntrl_t7tx_rateE"></a>

    <a id="_CPPv3N14raw_tx_cntrl_t7tx_rateE"></a> <a id="_CPPv2N14raw_tx_cntrl_t7tx_rateE"></a> <a id="raw_tx_cntrl_t::tx_rate__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga105fb7de46f6eb363b6a3840dc374a6d"></a> uint32\_t tx\_rate
    :   RAW Data TX rate information

    <a id="_CPPv4N14raw_tx_cntrl_t8tx_powerE"></a>

    <a id="_CPPv3N14raw_tx_cntrl_t8tx_powerE"></a> <a id="_CPPv2N14raw_tx_cntrl_t8tx_powerE"></a> <a id="raw_tx_cntrl_t::tx_power__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga7a01d26ccad63affbd38d0ef29f8f264"></a> uint32\_t tx\_power
    :   RAW Data TX power information

    <a id="_CPPv4N14raw_tx_cntrl_t12tx_retry_cntE"></a>

    <a id="_CPPv3N14raw_tx_cntrl_t12tx_retry_cntE"></a> <a id="_CPPv2N14raw_tx_cntrl_t12tx_retry_cntE"></a> <a id="raw_tx_cntrl_t::tx_retry_cnt__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gaa43c32fc5138afb8caccb660ad877cad"></a> uint32\_t tx\_retry\_cnt
    :   RAW Data TX retry count

<a id="_CPPv418wifi_raw_tx_info_t"></a>

<a id="_CPPv318wifi_raw_tx_info_t"></a> <a id="_CPPv218wifi_raw_tx_info_t"></a> <a id="wifi_raw_tx_info_t"></a> <a id="structwifi__raw__tx__info__t"></a> struct wifi\_raw\_tx\_info\_t
:   Wi-Fi RAW TX control.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18wifi_raw_tx_info_t3pktE"></a>

    <a id="_CPPv3N18wifi_raw_tx_info_t3pktE"></a> <a id="_CPPv2N18wifi_raw_tx_info_t3pktE"></a> <a id="wifi_raw_tx_info_t::pkt__uint8_tP"></a> <a id="group__bk__api__wifi__v2_1ga357f8cb52865dacbff1bc7b9f64b3461"></a> uint8\_t \*pkt
    :   RAW data tx packet address

    <a id="_CPPv4N18wifi_raw_tx_info_t3lenE"></a>

    <a id="_CPPv3N18wifi_raw_tx_info_t3lenE"></a> <a id="_CPPv2N18wifi_raw_tx_info_t3lenE"></a> <a id="wifi_raw_tx_info_t::len__i"></a> <a id="group__bk__api__wifi__v2_1gaaafc45d0951efd5b56d03757f8b5a7a4"></a> int len
    :   RAW data tx packet length

    <a id="_CPPv4N18wifi_raw_tx_info_t4typeE"></a>

    <a id="_CPPv3N18wifi_raw_tx_info_t4typeE"></a> <a id="_CPPv2N18wifi_raw_tx_info_t4typeE"></a> <a id="wifi_raw_tx_info_t::type__i"></a> <a id="group__bk__api__wifi__v2_1gaf043b27624ad1f2859731ae381bd0314"></a> int type
    :   Raw data tx packet type length

    <a id="_CPPv4N18wifi_raw_tx_info_t8tx_cntrlE"></a>

    <a id="_CPPv3N18wifi_raw_tx_info_t8tx_cntrlE"></a> <a id="_CPPv2N18wifi_raw_tx_info_t8tx_cntrlE"></a> <a id="wifi_raw_tx_info_t::tx_cntrl__raw_tx_cntrl_t"></a> <a id="group__bk__api__wifi__v2_1gae23c160b93223bd0d3d54810c1b3d1cf"></a> [raw\_tx\_cntrl\_t](#_CPPv414raw_tx_cntrl_t "raw_tx_cntrl_t") tx\_cntrl
    :   RAW data tx control information

<a id="_CPPv417wifi_ftm_config_t"></a>

<a id="_CPPv317wifi_ftm_config_t"></a> <a id="_CPPv217wifi_ftm_config_t"></a> <a id="wifi_ftm_config_t"></a> <a id="structwifi__ftm__config__t"></a> struct wifi\_ftm\_config\_t
:   FTM configuration and results.

    Wi-Fi fine timing measurement configuration.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17wifi_ftm_config_t13ftm_per_burstE"></a>

    <a id="_CPPv3N17wifi_ftm_config_t13ftm_per_burstE"></a> <a id="_CPPv2N17wifi_ftm_config_t13ftm_per_burstE"></a> <a id="wifi_ftm_config_t::ftm_per_burst__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga091f38d5a8f83cb91adff13652f26f28"></a> uint8\_t ftm\_per\_burst
    :   Number of FTMs per Burst

    <a id="_CPPv4N17wifi_ftm_config_t10nb_ftm_rspE"></a>

    <a id="_CPPv3N17wifi_ftm_config_t10nb_ftm_rspE"></a> <a id="_CPPv2N17wifi_ftm_config_t10nb_ftm_rspE"></a> <a id="wifi_ftm_config_t::nb_ftm_rsp__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga4a0d8523f58fabbce82a52cf912cc1d8"></a> uint8\_t nb\_ftm\_rsp
    :   Number of FTM responders on which we do the measurements

<a id="_CPPv419wifi_ftm_rsp_info_t"></a>

<a id="_CPPv319wifi_ftm_rsp_info_t"></a> <a id="_CPPv219wifi_ftm_rsp_info_t"></a> <a id="wifi_ftm_rsp_info_t"></a> <a id="structwifi__ftm__rsp__info__t"></a> struct wifi\_ftm\_rsp\_info\_t
:   Wi-Fi fine timing measurement results.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19wifi_ftm_rsp_info_t5bssidE"></a>

    <a id="_CPPv3N19wifi_ftm_rsp_info_t5bssidE"></a> <a id="_CPPv2N19wifi_ftm_rsp_info_t5bssidE"></a> <a id="wifi_ftm_rsp_info_t::bssid__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga35de386dafa284745c14d843ab5faad6"></a> uint8\_t bssid\[WIFI\_BSSID\_LEN\]
    :   MAC Address of the FTM responder

    <a id="_CPPv4N19wifi_ftm_rsp_info_t3rttE"></a>

    <a id="_CPPv3N19wifi_ftm_rsp_info_t3rttE"></a> <a id="_CPPv2N19wifi_ftm_rsp_info_t3rttE"></a> <a id="wifi_ftm_rsp_info_t::rtt__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga4a1fda122183915c9c180d87ed73aefa"></a> uint32\_t rtt
    :   Round Trip Time (in ns)

    <a id="_CPPv4N19wifi_ftm_rsp_info_t8distanceE"></a>

    <a id="_CPPv3N19wifi_ftm_rsp_info_t8distanceE"></a> <a id="_CPPv2N19wifi_ftm_rsp_info_t8distanceE"></a> <a id="wifi_ftm_rsp_info_t::distance__float"></a> <a id="group__bk__api__wifi__v2_1gab6f472fb284e9d1dce0c478fe70cf7e6"></a> float distance
    :   Distance (in m)

<a id="_CPPv418wifi_ftm_results_t"></a>

<a id="_CPPv318wifi_ftm_results_t"></a> <a id="_CPPv218wifi_ftm_results_t"></a> <a id="wifi_ftm_results_t"></a> <a id="structwifi__ftm__results__t"></a> struct wifi\_ftm\_results\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18wifi_ftm_results_t10nb_ftm_rspE"></a>

    <a id="_CPPv3N18wifi_ftm_results_t10nb_ftm_rspE"></a> <a id="_CPPv2N18wifi_ftm_results_t10nb_ftm_rspE"></a> <a id="wifi_ftm_results_t::nb_ftm_rsp__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gaa1a90e2fe5225c7ef2ad30163f3428e5"></a> uint8\_t nb\_ftm\_rsp
    :   Number of FTM responders for which we have a measurement

    <a id="_CPPv4N18wifi_ftm_results_t3rspE"></a>

    <a id="_CPPv3N18wifi_ftm_results_t3rspE"></a> <a id="_CPPv2N18wifi_ftm_results_t3rspE"></a> <a id="wifi_ftm_results_t::rsp__wifi_ftm_rsp_info_tP"></a> <a id="group__bk__api__wifi__v2_1gad528a891cb9d56c0794b73984f55d00e"></a> [wifi\_ftm\_rsp\_info\_t](#_CPPv419wifi_ftm_rsp_info_t "wifi_ftm_rsp_info_t") \*rsp
    :   Per-responder measurements

<a id="_CPPv413wifi_rx_pkt_t"></a>

<a id="_CPPv313wifi_rx_pkt_t"></a> <a id="_CPPv213wifi_rx_pkt_t"></a> <a id="wifi_rx_pkt_t"></a> <a id="structwifi__rx__pkt__t"></a> struct wifi\_rx\_pkt\_t
:   CSI configuration and results.

    Wi-Fi Channel State Information configuration and results.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13wifi_rx_pkt_t4rssiE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t4rssiE"></a> <a id="_CPPv2N13wifi_rx_pkt_t4rssiE"></a> <a id="wifi_rx_pkt_t::rssi__int8_t"></a> <a id="group__bk__api__wifi__v2_1ga234c13b1be149aa92886ce458bbf01bc"></a> int8\_t rssi
    :   Received Signal Strength Indicator(RSSI) of packet. unit: dBm

    <a id="_CPPv4N13wifi_rx_pkt_t4rateE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t4rateE"></a> <a id="_CPPv2N13wifi_rx_pkt_t4rateE"></a> <a id="wifi_rx_pkt_t::rate__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gadc17290944206869d9c15df6a50883df"></a> uint8\_t rate
    :   PHY rate encoding of the packet. Only valid for non HT(11bg) packet

    <a id="_CPPv4N13wifi_rx_pkt_t7foramatE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t7foramatE"></a> <a id="_CPPv2N13wifi_rx_pkt_t7foramatE"></a> <a id="wifi_rx_pkt_t::foramat__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga9ba7f29c56b329d95fa31c1e9f012395"></a> uint8\_t foramat
    :   0x0:non HT(11g) packet; 0x2:HT(11n)packet;0x4:VHT(11ac)packet;0x5:HE(11ax)packet

    <a id="_CPPv4N13wifi_rx_pkt_t3mcsE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t3mcsE"></a> <a id="_CPPv2N13wifi_rx_pkt_t3mcsE"></a> <a id="wifi_rx_pkt_t::mcs__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gab2f79e4de13424c4a409e9a8729ac614"></a> uint8\_t mcs
    :   Modulation Coding Scheme.

    <a id="_CPPv4N13wifi_rx_pkt_t3cwbE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t3cwbE"></a> <a id="_CPPv2N13wifi_rx_pkt_t3cwbE"></a> <a id="wifi_rx_pkt_t::cwb__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga3fced97ca08cffeabfe0a553fa90c402"></a> uint8\_t cwb
    :   Channel Bandwidth of the packet. 0: 20MHz; 1: 40MHz

    <a id="_CPPv4N13wifi_rx_pkt_t11aggregationE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t11aggregationE"></a> <a id="_CPPv2N13wifi_rx_pkt_t11aggregationE"></a> <a id="wifi_rx_pkt_t::aggregation__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gae3e30729d3bf4203ae7700a81dc07083"></a> uint8\_t aggregation
    :   Aggregation. 0: MPDU packet; 1: AMPDU packet

    <a id="_CPPv4N13wifi_rx_pkt_t4stbcE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t4stbcE"></a> <a id="_CPPv2N13wifi_rx_pkt_t4stbcE"></a> <a id="wifi_rx_pkt_t::stbc__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga67307eea8a7886fdf8761e09fb2292d3"></a> uint8\_t stbc
    :   Space Time Block Code(STBC). 0: non STBC packet; 1: STBC packet

    <a id="_CPPv4N13wifi_rx_pkt_t10fec_codingE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t10fec_codingE"></a> <a id="_CPPv2N13wifi_rx_pkt_t10fec_codingE"></a> <a id="wifi_rx_pkt_t::fec_coding__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga64cfe74eab3a47f9ffe4380936755ddf"></a> uint8\_t fec\_coding
    :   Forward Error Correction(FEC). Flag is set for 11n packets which are LDPC

    <a id="_CPPv4N13wifi_rx_pkt_t3sgiE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t3sgiE"></a> <a id="_CPPv2N13wifi_rx_pkt_t3sgiE"></a> <a id="wifi_rx_pkt_t::sgi__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gab00eff901f28775446dea2f9d3586817"></a> uint8\_t sgi
    :   Short Guide Interval(SGI). 0: Long GI; 1: Short GI

    <a id="_CPPv4N13wifi_rx_pkt_t7channelE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t7channelE"></a> <a id="_CPPv2N13wifi_rx_pkt_t7channelE"></a> <a id="wifi_rx_pkt_t::channel__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga5c1c3b5946cdc42dcbcbc3adec771fb5"></a> uint8\_t channel
    :   primary channel on which this packet is received

    <a id="_CPPv4N13wifi_rx_pkt_t17secondary_channelE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t17secondary_channelE"></a> <a id="_CPPv2N13wifi_rx_pkt_t17secondary_channelE"></a> <a id="wifi_rx_pkt_t::secondary_channel__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gadc84e5e22c927e0802a9525ab47a6de2"></a> uint8\_t secondary\_channel
    :   secondary channel on which this packet is received. 0: none; 1: above; 2: below

    <a id="_CPPv4N13wifi_rx_pkt_t7sig_lenE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t7sig_lenE"></a> <a id="_CPPv2N13wifi_rx_pkt_t7sig_lenE"></a> <a id="wifi_rx_pkt_t::sig_len__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga33d07357384c815c2dffa67f46a1fdbd"></a> uint8\_t sig\_len
    :   length of packet including Frame Check Sequence(FCS)

    <a id="_CPPv4N13wifi_rx_pkt_t9timestampE"></a>

    <a id="_CPPv3N13wifi_rx_pkt_t9timestampE"></a> <a id="_CPPv2N13wifi_rx_pkt_t9timestampE"></a> <a id="wifi_rx_pkt_t::timestamp__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gaca9068ee6a593eca73a0e3110753d1f7"></a> uint32\_t timestamp
    :   timestamp. The local time when this packet is received. unit: microsecond

<a id="_CPPv415wifi_csi_info_t"></a>

<a id="_CPPv315wifi_csi_info_t"></a> <a id="_CPPv215wifi_csi_info_t"></a> <a id="wifi_csi_info_t"></a> <a id="structwifi__csi__info__t"></a> struct wifi\_csi\_info\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15wifi_csi_info_t7rx_ctrlE"></a>

    <a id="_CPPv3N15wifi_csi_info_t7rx_ctrlE"></a> <a id="_CPPv2N15wifi_csi_info_t7rx_ctrlE"></a> <a id="wifi_csi_info_t::rx_ctrl__wifi_rx_pkt_t"></a> <a id="group__bk__api__wifi__v2_1ga5e4ee945449747c6695b659435edadb2"></a> struct [wifi\_rx\_pkt\_t](#_CPPv413wifi_rx_pkt_t "wifi_rx_pkt_t") rx\_ctrl
    :   rx packet ctrl

    <a id="_CPPv4N15wifi_csi_info_t3macE"></a>

    <a id="_CPPv3N15wifi_csi_info_t3macE"></a> <a id="_CPPv2N15wifi_csi_info_t3macE"></a> <a id="wifi_csi_info_t::mac__uint8_tA"></a> <a id="group__bk__api__wifi__v2_1ga3ed1204b1fc2fa7fa38e90e57b594285"></a> uint8\_t mac\[WIFI\_MAC\_LEN\]
    :   MAC Address of the CSI info receive

    <a id="_CPPv4N15wifi_csi_info_t3lenE"></a>

    <a id="_CPPv3N15wifi_csi_info_t3lenE"></a> <a id="_CPPv2N15wifi_csi_info_t3lenE"></a> <a id="wifi_csi_info_t::len__uint16_t"></a> <a id="group__bk__api__wifi__v2_1gaf5bf2caab08c7a52322641e89fca6a3c"></a> uint16\_t len
    :   The length of CSI info

    <a id="_CPPv4N15wifi_csi_info_t9data_typeE"></a>

    <a id="_CPPv3N15wifi_csi_info_t9data_typeE"></a> <a id="_CPPv2N15wifi_csi_info_t9data_typeE"></a> <a id="wifi_csi_info_t::data_type__uint16_t"></a> <a id="group__bk__api__wifi__v2_1gab13fd2261dc287b468380fe3a88b8173"></a> uint16\_t data\_type
    :   out data type 0: buf, 1:abs

    <a id="_CPPv4N15wifi_csi_info_t3bufE"></a>

    <a id="_CPPv3N15wifi_csi_info_t3bufE"></a> <a id="_CPPv2N15wifi_csi_info_t3bufE"></a> <a id="wifi_csi_info_t::buf__uint32_tA"></a> <a id="group__bk__api__wifi__v2_1gaa487486f92c0a2a7f7df9d615336f57c"></a> uint32\_t buf\[52\]
    :   CSI info

    <a id="_CPPv4N15wifi_csi_info_t4realE"></a>

    <a id="_CPPv3N15wifi_csi_info_t4realE"></a> <a id="_CPPv2N15wifi_csi_info_t4realE"></a> <a id="wifi_csi_info_t::real__double"></a> <a id="group__bk__api__wifi__v2_1gab098dabbc165df24d644967efcccfeb0"></a> double real
    :   \< CSI info iq

<a id="_CPPv416wifi_csi_alg_ind"></a>

<a id="_CPPv316wifi_csi_alg_ind"></a> <a id="_CPPv216wifi_csi_alg_ind"></a> <a id="wifi_csi_alg_ind"></a> <a id="structwifi__csi__alg__ind"></a> struct wifi\_csi\_alg\_ind

<a id="_CPPv416wifi_csi_cfg_dbg"></a>

<a id="_CPPv316wifi_csi_cfg_dbg"></a> <a id="_CPPv216wifi_csi_cfg_dbg"></a> <a id="wifi_csi_cfg_dbg"></a> <a id="structwifi__csi__cfg__dbg"></a> struct wifi\_csi\_cfg\_dbg

<a id="_CPPv418wifi_csi_start_dbg"></a>

<a id="_CPPv318wifi_csi_start_dbg"></a> <a id="_CPPv218wifi_csi_start_dbg"></a> <a id="wifi_csi_start_dbg"></a> <a id="structwifi__csi__start__dbg"></a> struct wifi\_csi\_start\_dbg

<a id="_CPPv410tx_stats_t"></a>

<a id="_CPPv310tx_stats_t"></a> <a id="_CPPv210tx_stats_t"></a> <a id="tx_stats_t"></a> <a id="structtx__stats__t"></a> struct tx\_stats\_t
:   Wi-Fi tx statistics.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N10tx_stats_t15tx_singel_totalE"></a>

    <a id="_CPPv3N10tx_stats_t15tx_singel_totalE"></a> <a id="_CPPv2N10tx_stats_t15tx_singel_totalE"></a> <a id="tx_stats_t::tx_singel_total__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gaa0b78b346e2dcaf8f15653ef209b0d05"></a> uint32\_t tx\_singel\_total
    :   tx single mpdu total count

    <a id="_CPPv4N10tx_stats_t15tx_singel_retryE"></a>

    <a id="_CPPv3N10tx_stats_t15tx_singel_retryE"></a> <a id="_CPPv2N10tx_stats_t15tx_singel_retryE"></a> <a id="tx_stats_t::tx_singel_retry__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gadaae08ae82d4f1f67d67d546bafae675"></a> uint32\_t tx\_singel\_retry
    :   tx single mpdu retry count

    <a id="_CPPv4N10tx_stats_t12tx_agg_totalE"></a>

    <a id="_CPPv3N10tx_stats_t12tx_agg_totalE"></a> <a id="_CPPv2N10tx_stats_t12tx_agg_totalE"></a> <a id="tx_stats_t::tx_agg_total__uint32_t"></a> <a id="group__bk__api__wifi__v2_1gaedba761cc950cc444afb80ea55acd4e3"></a> uint32\_t tx\_agg\_total
    :   tx mpdu of ampdu total count

    <a id="_CPPv4N10tx_stats_t11tx_agg_failE"></a>

    <a id="_CPPv3N10tx_stats_t11tx_agg_failE"></a> <a id="_CPPv2N10tx_stats_t11tx_agg_failE"></a> <a id="tx_stats_t::tx_agg_fail__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga623468861344cb8c57c46ad6b7d2cf26"></a> uint32\_t tx\_agg\_fail
    :   tx mpdu of ampdu fail count

<a id="_CPPv417wifi_tx_pwr_lmt_t"></a>

<a id="_CPPv317wifi_tx_pwr_lmt_t"></a> <a id="_CPPv217wifi_tx_pwr_lmt_t"></a> <a id="wifi_tx_pwr_lmt_t"></a> <a id="structwifi__tx__pwr__lmt__t"></a> struct wifi\_tx\_pwr\_lmt\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17wifi_tx_pwr_lmt_t10regulationE"></a>

    <a id="_CPPv3N17wifi_tx_pwr_lmt_t10regulationE"></a> <a id="_CPPv2N17wifi_tx_pwr_lmt_t10regulationE"></a> <a id="wifi_tx_pwr_lmt_t::regulation__wifi_regulation_t"></a> <a id="group__bk__api__wifi__v2_1ga7e58401eb3caa3380a02506c3bbdafd9"></a> [wifi\_regulation\_t](#_CPPv417wifi_regulation_t "wifi_regulation_t") regulation
    :   region regulation 0 REGUALTION\_NULL 1 REGUALTION\_FCC 2 REGUALTION\_ETSI 3 REGUALTION\_JP 4 REGUALTION\_EXT

    <a id="_CPPv4N17wifi_tx_pwr_lmt_t11ratesectionE"></a>

    <a id="_CPPv3N17wifi_tx_pwr_lmt_t11ratesectionE"></a> <a id="_CPPv2N17wifi_tx_pwr_lmt_t11ratesectionE"></a> <a id="wifi_tx_pwr_lmt_t::ratesection__wifi_ratesection_t"></a> <a id="group__bk__api__wifi__v2_1ga18a9bfc78bd5777ae5aa55c89a642bed"></a> [wifi\_ratesection\_t](#_CPPv418wifi_ratesection_t "wifi_ratesection_t") ratesection
    :   ratesection 0 RATE\_NULL 1 RATE\_CCK 2 RATE\_OFDM 3 RATE\_HT 4 RATE\_VHT 5 RATE\_HE

    <a id="_CPPv4N17wifi_tx_pwr_lmt_t7channelE"></a>

    <a id="_CPPv3N17wifi_tx_pwr_lmt_t7channelE"></a> <a id="_CPPv2N17wifi_tx_pwr_lmt_t7channelE"></a> <a id="wifi_tx_pwr_lmt_t::channel__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gad31f7724b31bef16b0de9f29867c18f9"></a> uint8\_t channel
    :   channel range from 1-14

    <a id="_CPPv4N17wifi_tx_pwr_lmt_t5valueE"></a>

    <a id="_CPPv3N17wifi_tx_pwr_lmt_t5valueE"></a> <a id="_CPPv2N17wifi_tx_pwr_lmt_t5valueE"></a> <a id="wifi_tx_pwr_lmt_t::value__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga6a4e26292440960e3464f67f1c2aa689"></a> uint8\_t value
    :   value max tx power

<a id="_CPPv418bk_bridge_config_t"></a>

<a id="_CPPv318bk_bridge_config_t"></a> <a id="_CPPv218bk_bridge_config_t"></a> <a id="bk_bridge_config_t"></a> <a id="structbk__bridge__config__t"></a> struct bk\_bridge\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_bridge_config_t17keep_sta_on_closeE"></a>

    <a id="_CPPv3N18bk_bridge_config_t17keep_sta_on_closeE"></a> <a id="_CPPv2N18bk_bridge_config_t17keep_sta_on_closeE"></a> <a id="bk_bridge_config_t::keep_sta_on_close__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gab9931548bc933632efc8d591c65adb4c"></a> uint8\_t keep\_sta\_on\_close
    :   1: keep STA connected after bridge close; 0: stop STA on close (default).

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_WIFI_NOT_INIT"></a>

<a id="group__bk__api__wifi__v2__enum_1ga3e53cec7119809b7717506ad5f36085f"></a> BK\_ERR\_WIFI\_NOT\_INIT
:   WiFi is not initialized, call bk\_wifi\_init() to init the WiFi

<a id="c.BK_ERR_WIFI_STA_NOT_STARTED"></a>

<a id="group__bk__api__wifi__v2__enum_1ga17397126f67479e898c44c2e1578a984"></a> BK\_ERR\_WIFI\_STA\_NOT\_STARTED
:   STA is not started, call [bk\_wifi\_sta\_start()](bk_wifi.md#group__bk__api__wifi__v2_1gaaf144e78b9438143e21f7c75e8c23ecf) to start the STA

<a id="c.BK_ERR_WIFI_AP_NOT_STARTED"></a>

<a id="group__bk__api__wifi__v2__enum_1ga34aaecea3c4f55fe70c11300da07baa9"></a> BK\_ERR\_WIFI\_AP\_NOT\_STARTED
:   AP is not initialized, call [bk\_wifi\_ap\_start()](bk_wifi.md#group__bk__api__wifi__v2_1ga664be1db35e4ef799f2178bfc466a2e5) to start the AP

<a id="c.BK_ERR_WIFI_CHAN_RANGE"></a>

<a id="group__bk__api__wifi__v2__enum_1ga8bf3b9834855ed40271d83a1332e1d06"></a> BK\_ERR\_WIFI\_CHAN\_RANGE
:   Invalid channel range

<a id="c.BK_ERR_WIFI_COUNTRY_POLICY"></a>

<a id="group__bk__api__wifi__v2__enum_1gab54a20c4c8c8ae4d3adea384a3749fdf"></a> BK\_ERR\_WIFI\_COUNTRY\_POLICY
:   Invalid country policy

<a id="c.BK_ERR_WIFI_RESERVED_FIELD"></a>

<a id="group__bk__api__wifi__v2__enum_1gaf7265e0814c2c72e238c2941338e0d9a"></a> BK\_ERR\_WIFI\_RESERVED\_FIELD
:   Reserved fields not 0

<a id="c.BK_ERR_WIFI_MONITOR_IP"></a>

<a id="group__bk__api__wifi__v2__enum_1ga6757a1fb11154019aea1acbc9a3a0bb9"></a> BK\_ERR\_WIFI\_MONITOR\_IP
:   Monitor is in progress

<a id="c.BK_ERR_WIFI_STA_NOT_CONFIG"></a>

<a id="group__bk__api__wifi__v2__enum_1ga1e66a2588e18bec7a53a5429450ed1e7"></a> BK\_ERR\_WIFI\_STA\_NOT\_CONFIG
:   STA is not configured, call bk\_wifi\_sta\_config() to configure it

<a id="c.BK_ERR_WIFI_AP_NOT_CONFIG"></a>

<a id="group__bk__api__wifi__v2__enum_1ga2baae2e392326f80340c427904258c95"></a> BK\_ERR\_WIFI\_AP\_NOT\_CONFIG
:   AP is not configured, call bk\_wifi\_ap\_config() to configure it

<a id="c.BK_ERR_WIFI_DRIVER"></a>

<a id="group__bk__api__wifi__v2__enum_1ga47bd90f7ae0e9c24e9082c20c957297e"></a> BK\_ERR\_WIFI\_DRIVER
:   Internal WiFi driver error

<a id="c.BK_ERR_WIFI_MONITOR_ENTER"></a>

<a id="group__bk__api__wifi__v2__enum_1gae81db1f58e616d8d52e9937906d1b778"></a> BK\_ERR\_WIFI\_MONITOR\_ENTER
:   WiFi failed to enter monitor mode

<a id="c.BK_ERR_WIFI_DRIVER_DEL_VIF"></a>

<a id="group__bk__api__wifi__v2__enum_1ga1f5df9c7ae88414099ca70ee560a7dc2"></a> BK\_ERR\_WIFI\_DRIVER\_DEL\_VIF
:   WiFi driver failed to delete WiFi virtual interface

<a id="c.BK_ERR_WIFI_DRIVER_AP_START"></a>

<a id="group__bk__api__wifi__v2__enum_1ga0d255c15f94c4e773dc746906479b7c7"></a> BK\_ERR\_WIFI\_DRIVER\_AP\_START
:   WiFi driver failed to start BK AP

<a id="c.BK_ERR_WIFI_CHAN_NUMBER"></a>

<a id="group__bk__api__wifi__v2__enum_1gaf0e6f1d89444885164d19206c49ed42a"></a> BK\_ERR\_WIFI\_CHAN\_NUMBER
:   Invalid channel number

<a id="c.WIFI_MIN_CHAN_NUM"></a>

<a id="group__bk__api__wifi__v2__enum_1gaa4fdfa3785cfcfe8e88072acb4b94913"></a> WIFI\_MIN\_CHAN\_NUM
:   Minimum supported channel number

<a id="c.WIFI_MAX_CHAN_NUM"></a>

<a id="group__bk__api__wifi__v2__enum_1ga736217f5963b4ae49dc331aa143c70bb"></a> WIFI\_MAX\_CHAN\_NUM
:   Maximum supported channel number

<a id="c.WIFI_MAX_SCAN_CHAN_DUR"></a>

<a id="group__bk__api__wifi__v2__enum_1ga518251a605e88070abffd60373679ec8"></a> WIFI\_MAX\_SCAN\_CHAN\_DUR
:   scan duration param, need less than 200ms

<a id="c.WIFI_CHANNEL_NUM_2G4"></a>

<a id="group__bk__api__wifi__v2__enum_1gacd06456321ebd80b9001f069135c17ba"></a> WIFI\_CHANNEL\_NUM\_2G4
:   Maximum supported 2.4G channel number

<a id="c.WIFI_CHANNEL_NUM_5G"></a>

<a id="group__bk__api__wifi__v2__enum_1gac2564f06820fef7feb201c608694e866"></a> WIFI\_CHANNEL\_NUM\_5G
:   Maximum supported 5G channel numbe

<a id="c.WIFI_2BAND_MAX_CHAN_NUM"></a>

<a id="group__bk__api__wifi__v2__enum_1ga0a3b488fd022c9562533ae2ad22eadaa"></a> WIFI\_2BAND\_MAX\_CHAN\_NUM

<a id="c.WIFI_SSID_STR_LEN"></a>

<a id="group__bk__api__wifi__v2__enum_1ga0494f16536e40b559f4f4965b4f6d218"></a> WIFI\_SSID\_STR\_LEN
:   Maximum **NULL-terminated** WiFi SSID length

<a id="c.WIFI_BSSID_LEN"></a>

<a id="group__bk__api__wifi__v2__enum_1ga3f6e17172d889ba61f6fb28820b3cd12"></a> WIFI\_BSSID\_LEN
:   Length of BSSID

<a id="c.WIFI_MAC_LEN"></a>

<a id="group__bk__api__wifi__v2__enum_1gabc871a0934ad71ec71b29de3f9bc4815"></a> WIFI\_MAC\_LEN
:   Length of MAC

<a id="c.WIFI_PASSWORD_LEN"></a>

<a id="group__bk__api__wifi__v2__enum_1gaf4b865a3a45e5f7a5ca3f561a649e804"></a> WIFI\_PASSWORD\_LEN
:   Maximum **NULL-terminated** WiFi password length

<a id="c.WIFI_DEFAULT_INIT_CONFIG"></a>

<a id="group__bk__api__wifi__v2__enum_1ga412e5b8a95fbe4baf89a44c949b30a44"></a> WIFI\_DEFAULT\_INIT\_CONFIG()
:   default init configuration

<a id="c.WIFI_DEFAULT_STA_CONFIG"></a>

<a id="group__bk__api__wifi__v2__enum_1ga04611cd1fea13178e3c1654cfafd4253"></a> WIFI\_DEFAULT\_STA\_CONFIG()
:   default STA configuration

<a id="c.WIFI_DEFAULT_AP_CONFIG"></a>

<a id="group__bk__api__wifi__v2__enum_1ga0710d007a12faf0163e20b04f4e73aba"></a> WIFI\_DEFAULT\_AP\_CONFIG()
:   default AP configuration

<a id="c.WIFI_DEFAULT_SCAN_CONFIG"></a>

<a id="group__bk__api__wifi__v2__enum_1ga15d1f6c3ddee8b3a7068aa7711c885f5"></a> WIFI\_DEFAULT\_SCAN\_CONFIG()
:   default Scan configuration

<a id="c.WIFI_DEFAULT_FILTER_CONFIG"></a>

<a id="group__bk__api__wifi__v2__enum_1ga92389c2b9bbad59c8194debb8c51efa5"></a> WIFI\_DEFAULT\_FILTER\_CONFIG()
:   default Filter configuration

<a id="c.WIFI_DEFAULT_FTM_CONFIG"></a>

<a id="group__bk__api__wifi__v2__enum_1ga8a528409f2d46eeab15affaacf634263"></a> WIFI\_DEFAULT\_FTM\_CONFIG()
:   default FTM configuration

<a id="c.BK_MAX_STA_TYPE"></a>

<a id="group__bk__api__wifi__v2__typedef_1gafd21e4dbe54802b84c9014913faef2d4"></a> BK\_MAX\_STA\_TYPE

<a id="c.OUI_BEKEN"></a>

<a id="group__bk__api__wifi__v2__typedef_1ga8c05f9c6420142a4b7fa4cfe8dfb8aca"></a> OUI\_BEKEN

<a id="c.WLAN_EID_VENDOR_SPECIFIC"></a>

<a id="group__bk__api__wifi__v2__typedef_1ga35f179d40f064114d74f686c2eb3b159"></a> WLAN\_EID\_VENDOR\_SPECIFIC

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv411BK_STA_TYPE"></a>

<a id="_CPPv311BK_STA_TYPE"></a> <a id="_CPPv211BK_STA_TYPE"></a> <a id="BK_STA_TYPE"></a> <a id="group__bk__api__wifi__v2__typedef_1ga338c42a75d2f50a9ef55c2238fc33adf"></a> typedef enum [sta\_type](#_CPPv48sta_type "sta_type") BK\_STA\_TYPE

<a id="_CPPv413wlan_ap_sta_t"></a>

<a id="_CPPv313wlan_ap_sta_t"></a> <a id="_CPPv213wlan_ap_sta_t"></a> <a id="wlan_ap_sta_t"></a> <a id="group__bk__api__wifi__v2__typedef_1gaef5913aef30a4dee0001e45a0450473d"></a> typedef struct [wlan\_ap\_sta](#_CPPv411wlan_ap_sta "wlan_ap_sta") wlan\_ap\_sta\_t
:   Wlan station information definition.

<a id="_CPPv414wlan_ap_stas_t"></a>

<a id="_CPPv314wlan_ap_stas_t"></a> <a id="_CPPv214wlan_ap_stas_t"></a> <a id="wlan_ap_stas_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga6c2683431c3956e933cd3340c1329f41"></a> typedef struct [wlan\_ap\_stas](#_CPPv412wlan_ap_stas "wlan_ap_stas") wlan\_ap\_stas\_t
:   Wlan connected stations information definition.

<a id="_CPPv414wlan_ap_vsie_t"></a>

<a id="_CPPv314wlan_ap_vsie_t"></a> <a id="_CPPv214wlan_ap_vsie_t"></a> <a id="wlan_ap_vsie_t"></a> <a id="group__bk__api__wifi__v2__typedef_1gaaecb4a474ea19a8599453f36b74ae4aa"></a> typedef struct [wlan\_ap\_vsie](#_CPPv412wlan_ap_vsie "wlan_ap_vsie") wlan\_ap\_vsie\_t
:   softap beacon/probe response’s vendor IEs Dynamic change softap’s vendor specific IEs.

<a id="_CPPv415wlan_sta_vsie_t"></a>

<a id="_CPPv315wlan_sta_vsie_t"></a> <a id="_CPPv215wlan_sta_vsie_t"></a> <a id="wlan_sta_vsie_t"></a> <a id="group__bk__api__wifi__v2__typedef_1gae8c7d3c160a32f4f0b618913dafe3faa"></a> typedef struct [wlan\_sta\_vsie](#_CPPv413wlan_sta_vsie "wlan_sta_vsie") wlan\_sta\_vsie\_t
:   STA vendor IEs for (re)assoc, scan, p2p, p2p go, etc. Dynamic change STA’s vendor specific IEs.

<a id="_CPPv417wifi_monitor_cb_t"></a>

<a id="_CPPv317wifi_monitor_cb_t"></a> <a id="_CPPv217wifi_monitor_cb_t"></a> <a id="wifi_monitor_cb_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga7a1cb892e0cb787179b189d79faa421e"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*wifi\_monitor\_cb\_t)(const uint8\_t \*frame, uint32\_t len, const [wifi\_frame\_info\_t](#_CPPv417wifi_frame_info_t "wifi_frame_info_t") \*frame\_info)
:   Monitor callback to receive frames relayed by WiFi driver.

    **Attention**
    :   1\. The memory of frame and frame\_info will be freed immediately when the callback is returned. If we want to use the frame or frame\_info in other task, make a copy of them and handle them accordingly.

    **Attention**
    :   2\. Don’t do too much work in the callback because the callback is called in context of WiFi core thread, too much work may impact the performance of WiFi.

<a id="_CPPv420wifi_rlk_chan_info_t"></a>

<a id="_CPPv320wifi_rlk_chan_info_t"></a> <a id="_CPPv220wifi_rlk_chan_info_t"></a> <a id="wifi_rlk_chan_info_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga9d50876726075b1f3fa57cc1e36f124f"></a> typedef struct [wifi\_rlk\_chan\_info](#_CPPv418wifi_rlk_chan_info "wifi_rlk_chan_info") wifi\_rlk\_chan\_info\_t

<a id="_CPPv420wifi_rlk_base_info_t"></a>

<a id="_CPPv320wifi_rlk_base_info_t"></a> <a id="_CPPv220wifi_rlk_base_info_t"></a> <a id="wifi_rlk_base_info_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga8a41983d1759b1542cb4741a9f19a80d"></a> typedef struct [wifi\_rlk\_base\_info](#_CPPv418wifi_rlk_base_info "wifi_rlk_base_info") wifi\_rlk\_base\_info\_t

<a id="_CPPv422wifi_rlk_scan_cfm_cb_t"></a>

<a id="_CPPv322wifi_rlk_scan_cfm_cb_t"></a> <a id="_CPPv222wifi_rlk_scan_cfm_cb_t"></a> <a id="wifi_rlk_scan_cfm_cb_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga7b2ceefa837dfa63a8659ae2c527b24b"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*wifi\_rlk\_scan\_cfm\_cb\_t)(void)

<a id="_CPPv416wifi_filter_cb_t"></a>

<a id="_CPPv316wifi_filter_cb_t"></a> <a id="_CPPv216wifi_filter_cb_t"></a> <a id="wifi_filter_cb_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga4f78a94640b8b4e51f59fa17fea4b923"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*wifi\_filter\_cb\_t)(const uint8\_t \*frame, uint32\_t len, const [wifi\_frame\_info\_t](#_CPPv417wifi_frame_info_t "wifi_frame_info_t") \*frame\_info)
:   Filter callback to receive frames relayed by WiFi driver.

    **Attention**
    :   1\. The memory of frame and frame\_info will be freed immediately when the callback is returned. If we want to use the frame or frame\_info in other task, make a copy of them and handle them accordingly.

    **Attention**
    :   2\. Don’t do too much work in the callback because the callback is called in context of WiFi core thread, too much work may impact the performance of WiFi.

<a id="_CPPv413wifi_csi_cb_t"></a>

<a id="_CPPv313wifi_csi_cb_t"></a> <a id="_CPPv213wifi_csi_cb_t"></a> <a id="wifi_csi_cb_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga1049b9985d49124ef64821770ebd313b"></a> typedef void (\*wifi\_csi\_cb\_t)(struct [wifi\_csi\_info\_t](#_CPPv415wifi_csi_info_t "wifi_csi_info_t") \*info)

<a id="_CPPv421wifi_beacon_cc_rxed_t"></a>

<a id="_CPPv321wifi_beacon_cc_rxed_t"></a> <a id="_CPPv221wifi_beacon_cc_rxed_t"></a> <a id="wifi_beacon_cc_rxed_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga164b8762b3b18d74c6e4cb834a33edd1"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*wifi\_beacon\_cc\_rxed\_t)(void \*ctxt, uint8\_t \*cc, uint8\_t cc\_len)

<a id="_CPPv418wifi_get_vsie_cb_t"></a>

<a id="_CPPv318wifi_get_vsie_cb_t"></a> <a id="_CPPv218wifi_get_vsie_cb_t"></a> <a id="wifi_get_vsie_cb_t"></a> <a id="group__bk__api__wifi__v2_1gabce969b7ac1ba6eb13f177a11f29745f"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*wifi\_get\_vsie\_cb\_t)(void \*vendor\_ie, uint8\_t frame\_type)
:   wifi get vsie cb interface

    Param void\*
    :   vendor\_ie

    Param frame
    :   type 1: probe response(or beacon) 2: assoc response

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv411wifi_band_t"></a>

<a id="_CPPv311wifi_band_t"></a> <a id="_CPPv211wifi_band_t"></a> <a id="group__bk__api__wifi__v2__enum_1ga88bf982f778c6644a16c5dd47a3eebda"></a> enum wifi\_band\_t
:   enum ieee80211\_band \- supported frequency bands

    The bands are assigned this way because the supported bitrates differ in these bands.

    @IEEE80211\_BAND\_2GHZ: 2.4GHz ISM band @IEEE80211\_BAND\_5GHZ: around 5GHz band (4.9-5.7) @IEEE80211\_BAND\_6GHZ: around 6GHz band (5.925-7.125) @IEEE80211\_BAND\_60GHZ: around 60 GHz band (58.32 \- 64.80 GHz) @IEEE80211\_NUM\_BANDS: number of defined bands

    *Values:*

    <a id="_CPPv4N11wifi_band_t19IEEE80211_BAND_2GHZE"></a>

    <a id="_CPPv3N11wifi_band_t19IEEE80211_BAND_2GHZE"></a> <a id="_CPPv2N11wifi_band_t19IEEE80211_BAND_2GHZE"></a> <a id="group__bk__api__wifi__v2__enum_1gga88bf982f778c6644a16c5dd47a3eebdaaf339f82c036557f42f668a358aa96da3"></a> enumerator IEEE80211\_BAND\_2GHZ

    <a id="_CPPv4N11wifi_band_t19IEEE80211_BAND_5GHZE"></a>

    <a id="_CPPv3N11wifi_band_t19IEEE80211_BAND_5GHZE"></a> <a id="_CPPv2N11wifi_band_t19IEEE80211_BAND_5GHZE"></a> <a id="group__bk__api__wifi__v2__enum_1gga88bf982f778c6644a16c5dd47a3eebdaa0871c8866251ec4e668e956bb0427cfa"></a> enumerator IEEE80211\_BAND\_5GHZ

    <a id="_CPPv4N11wifi_band_t19IEEE80211_BAND_6GHZE"></a>

    <a id="_CPPv3N11wifi_band_t19IEEE80211_BAND_6GHZE"></a> <a id="_CPPv2N11wifi_band_t19IEEE80211_BAND_6GHZE"></a> <a id="group__bk__api__wifi__v2__enum_1gga88bf982f778c6644a16c5dd47a3eebdaa309372a5d128e7a1ee9a5cd55f27f622"></a> enumerator IEEE80211\_BAND\_6GHZ

    <a id="_CPPv4N11wifi_band_t20IEEE80211_BAND_60GHZE"></a>

    <a id="_CPPv3N11wifi_band_t20IEEE80211_BAND_60GHZE"></a> <a id="_CPPv2N11wifi_band_t20IEEE80211_BAND_60GHZE"></a> <a id="group__bk__api__wifi__v2__enum_1gga88bf982f778c6644a16c5dd47a3eebdaa8e43a12ab8250a1d24e84496b6b9d8fb"></a> enumerator IEEE80211\_BAND\_60GHZ

    <a id="_CPPv4N11wifi_band_t19IEEE80211_NUM_BANDSE"></a>

    <a id="_CPPv3N11wifi_band_t19IEEE80211_NUM_BANDSE"></a> <a id="_CPPv2N11wifi_band_t19IEEE80211_NUM_BANDSE"></a> <a id="group__bk__api__wifi__v2__enum_1gga88bf982f778c6644a16c5dd47a3eebdaa703cf67d516a80d6dae1b1995017b9a4"></a> enumerator IEEE80211\_NUM\_BANDS

<a id="_CPPv412wifi_event_t"></a>

<a id="_CPPv312wifi_event_t"></a> <a id="_CPPv212wifi_event_t"></a> <a id="group__bk__api__wifi__v2__enum_1ga4d4930414997036f72c92e8a02a6de33"></a> enum wifi\_event\_t
:   WiFi public event type.

    *Values:*

    <a id="_CPPv4N12wifi_event_t20EVENT_WIFI_SCAN_DONEE"></a>

    <a id="_CPPv3N12wifi_event_t20EVENT_WIFI_SCAN_DONEE"></a> <a id="_CPPv2N12wifi_event_t20EVENT_WIFI_SCAN_DONEE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33a70b73fdd0fe544808f91625b672c8381"></a> enumerator EVENT\_WIFI\_SCAN\_DONE
    :   WiFi scan done event

    <a id="_CPPv4N12wifi_event_t24EVENT_WIFI_STA_CONNECTEDE"></a>

    <a id="_CPPv3N12wifi_event_t24EVENT_WIFI_STA_CONNECTEDE"></a> <a id="_CPPv2N12wifi_event_t24EVENT_WIFI_STA_CONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33a18bf31613ee317b91cac1d081439db1f"></a> enumerator EVENT\_WIFI\_STA\_CONNECTED
    :   The BK STA is connected

    <a id="_CPPv4N12wifi_event_t27EVENT_WIFI_STA_DISCONNECTEDE"></a>

    <a id="_CPPv3N12wifi_event_t27EVENT_WIFI_STA_DISCONNECTEDE"></a> <a id="_CPPv2N12wifi_event_t27EVENT_WIFI_STA_DISCONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33a7dfa9bfd390236e0dd4b9565cba07daa"></a> enumerator EVENT\_WIFI\_STA\_DISCONNECTED
    :   The BK STA is disconnected

    <a id="_CPPv4N12wifi_event_t23EVENT_WIFI_AP_CONNECTEDE"></a>

    <a id="_CPPv3N12wifi_event_t23EVENT_WIFI_AP_CONNECTEDE"></a> <a id="_CPPv2N12wifi_event_t23EVENT_WIFI_AP_CONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33abc51ea6bc465bbbbe83e62b5b085006b"></a> enumerator EVENT\_WIFI\_AP\_CONNECTED
    :   A STA is connected to the BK AP (SoftAP role)

    <a id="_CPPv4N12wifi_event_t26EVENT_WIFI_AP_DISCONNECTEDE"></a>

    <a id="_CPPv3N12wifi_event_t26EVENT_WIFI_AP_DISCONNECTEDE"></a> <a id="_CPPv2N12wifi_event_t26EVENT_WIFI_AP_DISCONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33ac8f0ceb3b967f3422335c7358f627f99"></a> enumerator EVENT\_WIFI\_AP\_DISCONNECTED
    :   A STA is disconnected from the BK AP (SoftAP role)

    <a id="_CPPv4N12wifi_event_t23EVENT_WIFI_GO_CONNECTEDE"></a>

    <a id="_CPPv3N12wifi_event_t23EVENT_WIFI_GO_CONNECTEDE"></a> <a id="_CPPv2N12wifi_event_t23EVENT_WIFI_GO_CONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33a6932581fea15034fbc9251c729106f6e"></a> enumerator EVENT\_WIFI\_GO\_CONNECTED
    :   A GC is connected to the local P2P GO

    <a id="_CPPv4N12wifi_event_t26EVENT_WIFI_GO_DISCONNECTEDE"></a>

    <a id="_CPPv3N12wifi_event_t26EVENT_WIFI_GO_DISCONNECTEDE"></a> <a id="_CPPv2N12wifi_event_t26EVENT_WIFI_GO_DISCONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33a281ebd0b9706b88492b6372b9beca2cb"></a> enumerator EVENT\_WIFI\_GO\_DISCONNECTED
    :   A GC is disconnected from the local P2P GO

    <a id="_CPPv4N12wifi_event_t23EVENT_WIFI_GC_CONNECTEDE"></a>

    <a id="_CPPv3N12wifi_event_t23EVENT_WIFI_GC_CONNECTEDE"></a> <a id="_CPPv2N12wifi_event_t23EVENT_WIFI_GC_CONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33ad604a835cce5539ee13aad4e0547e29a"></a> enumerator EVENT\_WIFI\_GC\_CONNECTED
    :   The local P2P GC is connected to the remote GO

    <a id="_CPPv4N12wifi_event_t26EVENT_WIFI_GC_DISCONNECTEDE"></a>

    <a id="_CPPv3N12wifi_event_t26EVENT_WIFI_GC_DISCONNECTEDE"></a> <a id="_CPPv2N12wifi_event_t26EVENT_WIFI_GC_DISCONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33ac4afaa1dac203cf07e4bc5df40464e6c"></a> enumerator EVENT\_WIFI\_GC\_DISCONNECTED
    :   The local P2P GC is disconnected from the remote GO

    <a id="_CPPv4N12wifi_event_t24EVENT_WIFI_NETWORK_FOUNDE"></a>

    <a id="_CPPv3N12wifi_event_t24EVENT_WIFI_NETWORK_FOUNDE"></a> <a id="_CPPv2N12wifi_event_t24EVENT_WIFI_NETWORK_FOUNDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33ad2130915964e9a9a66bddbc2e0fa0907"></a> enumerator EVENT\_WIFI\_NETWORK\_FOUND
    :   The BK STA find target AP

    <a id="_CPPv4N12wifi_event_t16EVENT_WIFI_COUNTE"></a>

    <a id="_CPPv3N12wifi_event_t16EVENT_WIFI_COUNTE"></a> <a id="_CPPv2N12wifi_event_t16EVENT_WIFI_COUNTE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4d4930414997036f72c92e8a02a6de33a45f8fd32bccb88538c4e36c1bf884c8c"></a> enumerator EVENT\_WIFI\_COUNT
    :   WiFi event count

<a id="_CPPv417wifi_err_reason_t"></a>

<a id="_CPPv317wifi_err_reason_t"></a> <a id="_CPPv217wifi_err_reason_t"></a> <a id="group__bk__api__wifi__v2__enum_1gaf2f44e69763071bbe8c3903158c5a357"></a> enum wifi\_err\_reason\_t
:   *Values:*

    <a id="_CPPv4N17wifi_err_reason_t20WIFI_REASON_RESERVEDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t20WIFI_REASON_RESERVEDE"></a> <a id="_CPPv2N17wifi_err_reason_t20WIFI_REASON_RESERVEDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357aeb810b53563e59d566d1c1dffce9b3a3"></a> enumerator WIFI\_REASON\_RESERVED

    <a id="_CPPv4N17wifi_err_reason_t23WIFI_REASON_UNSPECIFIEDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t23WIFI_REASON_UNSPECIFIEDE"></a> <a id="_CPPv2N17wifi_err_reason_t23WIFI_REASON_UNSPECIFIEDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a976f9cb06ee9e62bf5141d11a80d8199"></a> enumerator WIFI\_REASON\_UNSPECIFIED

    <a id="_CPPv4N17wifi_err_reason_t31WIFI_REASON_PREV_AUTH_NOT_VALIDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t31WIFI_REASON_PREV_AUTH_NOT_VALIDE"></a> <a id="_CPPv2N17wifi_err_reason_t31WIFI_REASON_PREV_AUTH_NOT_VALIDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a33bba2a2a3b682f80eac4350957ac64f"></a> enumerator WIFI\_REASON\_PREV\_AUTH\_NOT\_VALID

    <a id="_CPPv4N17wifi_err_reason_t26WIFI_REASON_DEAUTH_LEAVINGE"></a>

    <a id="_CPPv3N17wifi_err_reason_t26WIFI_REASON_DEAUTH_LEAVINGE"></a> <a id="_CPPv2N17wifi_err_reason_t26WIFI_REASON_DEAUTH_LEAVINGE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ae41fb8600a5cf9d95b218c6fe903f588"></a> enumerator WIFI\_REASON\_DEAUTH\_LEAVING

    <a id="_CPPv4N17wifi_err_reason_t38WIFI_REASON_DISASSOC_DUE_TO_INACTIVITYE"></a>

    <a id="_CPPv3N17wifi_err_reason_t38WIFI_REASON_DISASSOC_DUE_TO_INACTIVITYE"></a> <a id="_CPPv2N17wifi_err_reason_t38WIFI_REASON_DISASSOC_DUE_TO_INACTIVITYE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a959f13c5cd53fe5b57ef28f7412d124d"></a> enumerator WIFI\_REASON\_DISASSOC\_DUE\_TO\_INACTIVITY

    <a id="_CPPv4N17wifi_err_reason_t28WIFI_REASON_DISASSOC_AP_BUSYE"></a>

    <a id="_CPPv3N17wifi_err_reason_t28WIFI_REASON_DISASSOC_AP_BUSYE"></a> <a id="_CPPv2N17wifi_err_reason_t28WIFI_REASON_DISASSOC_AP_BUSYE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357adf76631da677a459991221c5d3f3c151"></a> enumerator WIFI\_REASON\_DISASSOC\_AP\_BUSY

    <a id="_CPPv4N17wifi_err_reason_t41WIFI_REASON_CLASS2_FRAME_FROM_NONAUTH_STAE"></a>

    <a id="_CPPv3N17wifi_err_reason_t41WIFI_REASON_CLASS2_FRAME_FROM_NONAUTH_STAE"></a> <a id="_CPPv2N17wifi_err_reason_t41WIFI_REASON_CLASS2_FRAME_FROM_NONAUTH_STAE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a33038f81427b85bb06ebc96a5e4333b1"></a> enumerator WIFI\_REASON\_CLASS2\_FRAME\_FROM\_NONAUTH\_STA

    <a id="_CPPv4N17wifi_err_reason_t42WIFI_REASON_CLASS3_FRAME_FROM_NONASSOC_STAE"></a>

    <a id="_CPPv3N17wifi_err_reason_t42WIFI_REASON_CLASS3_FRAME_FROM_NONASSOC_STAE"></a> <a id="_CPPv2N17wifi_err_reason_t42WIFI_REASON_CLASS3_FRAME_FROM_NONASSOC_STAE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a82e17676f57006229f6560106fd0b778"></a> enumerator WIFI\_REASON\_CLASS3\_FRAME\_FROM\_NONASSOC\_STA

    <a id="_CPPv4N17wifi_err_reason_t33WIFI_REASON_DISASSOC_STA_HAS_LEFTE"></a>

    <a id="_CPPv3N17wifi_err_reason_t33WIFI_REASON_DISASSOC_STA_HAS_LEFTE"></a> <a id="_CPPv2N17wifi_err_reason_t33WIFI_REASON_DISASSOC_STA_HAS_LEFTE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ab987db2bf12af11504c38aa158f82f6b"></a> enumerator WIFI\_REASON\_DISASSOC\_STA\_HAS\_LEFT

    <a id="_CPPv4N17wifi_err_reason_t38WIFI_REASON_STA_REQ_ASSOC_WITHOUT_AUTHE"></a>

    <a id="_CPPv3N17wifi_err_reason_t38WIFI_REASON_STA_REQ_ASSOC_WITHOUT_AUTHE"></a> <a id="_CPPv2N17wifi_err_reason_t38WIFI_REASON_STA_REQ_ASSOC_WITHOUT_AUTHE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a08e67aa577437487eee2f070c029e824"></a> enumerator WIFI\_REASON\_STA\_REQ\_ASSOC\_WITHOUT\_AUTH

    <a id="_CPPv4N17wifi_err_reason_t36WIFI_REASON_PWR_CAPABILITY_NOT_VALIDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t36WIFI_REASON_PWR_CAPABILITY_NOT_VALIDE"></a> <a id="_CPPv2N17wifi_err_reason_t36WIFI_REASON_PWR_CAPABILITY_NOT_VALIDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ab8cb5d125a4528950b1f8afb47114bbc"></a> enumerator WIFI\_REASON\_PWR\_CAPABILITY\_NOT\_VALID

    <a id="_CPPv4N17wifi_err_reason_t39WIFI_REASON_SUPPORTED_CHANNEL_NOT_VALIDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t39WIFI_REASON_SUPPORTED_CHANNEL_NOT_VALIDE"></a> <a id="_CPPv2N17wifi_err_reason_t39WIFI_REASON_SUPPORTED_CHANNEL_NOT_VALIDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a131dc746f66ae4ce7110bbba1627ee30"></a> enumerator WIFI\_REASON\_SUPPORTED\_CHANNEL\_NOT\_VALID

    <a id="_CPPv4N17wifi_err_reason_t35WIFI_REASON_BSS_TRANSITION_DISASSOCE"></a>

    <a id="_CPPv3N17wifi_err_reason_t35WIFI_REASON_BSS_TRANSITION_DISASSOCE"></a> <a id="_CPPv2N17wifi_err_reason_t35WIFI_REASON_BSS_TRANSITION_DISASSOCE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ae016c532830e08f69dbf730af6869bc7"></a> enumerator WIFI\_REASON\_BSS\_TRANSITION\_DISASSOC

    <a id="_CPPv4N17wifi_err_reason_t22WIFI_REASON_INVALID_IEE"></a>

    <a id="_CPPv3N17wifi_err_reason_t22WIFI_REASON_INVALID_IEE"></a> <a id="_CPPv2N17wifi_err_reason_t22WIFI_REASON_INVALID_IEE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a89b89284499f00a44ffb448c41f6d7c1"></a> enumerator WIFI\_REASON\_INVALID\_IE

    <a id="_CPPv4N17wifi_err_reason_t31WIFI_REASON_MICHAEL_MIC_FAILUREE"></a>

    <a id="_CPPv3N17wifi_err_reason_t31WIFI_REASON_MICHAEL_MIC_FAILUREE"></a> <a id="_CPPv2N17wifi_err_reason_t31WIFI_REASON_MICHAEL_MIC_FAILUREE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a8665f4acc6ef6f1ec2a5273dc257638b"></a> enumerator WIFI\_REASON\_MICHAEL\_MIC\_FAILURE

    <a id="_CPPv4N17wifi_err_reason_t34WIFI_REASON_4WAY_HANDSHAKE_TIMEOUTE"></a>

    <a id="_CPPv3N17wifi_err_reason_t34WIFI_REASON_4WAY_HANDSHAKE_TIMEOUTE"></a> <a id="_CPPv2N17wifi_err_reason_t34WIFI_REASON_4WAY_HANDSHAKE_TIMEOUTE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ac9fc8823a1c371dfb1c39daeb8090b44"></a> enumerator WIFI\_REASON\_4WAY\_HANDSHAKE\_TIMEOUT

    <a id="_CPPv4N17wifi_err_reason_t36WIFI_REASON_GROUP_KEY_UPDATE_TIMEOUTE"></a>

    <a id="_CPPv3N17wifi_err_reason_t36WIFI_REASON_GROUP_KEY_UPDATE_TIMEOUTE"></a> <a id="_CPPv2N17wifi_err_reason_t36WIFI_REASON_GROUP_KEY_UPDATE_TIMEOUTE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a1271a3cb9f8c81b796054ce88ca3f51d"></a> enumerator WIFI\_REASON\_GROUP\_KEY\_UPDATE\_TIMEOUT

    <a id="_CPPv4N17wifi_err_reason_t30WIFI_REASON_IE_IN_4WAY_DIFFERSE"></a>

    <a id="_CPPv3N17wifi_err_reason_t30WIFI_REASON_IE_IN_4WAY_DIFFERSE"></a> <a id="_CPPv2N17wifi_err_reason_t30WIFI_REASON_IE_IN_4WAY_DIFFERSE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ac44df5ca9975e4d70d6afe2357f00390"></a> enumerator WIFI\_REASON\_IE\_IN\_4WAY\_DIFFERS

    <a id="_CPPv4N17wifi_err_reason_t34WIFI_REASON_GROUP_CIPHER_NOT_VALIDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t34WIFI_REASON_GROUP_CIPHER_NOT_VALIDE"></a> <a id="_CPPv2N17wifi_err_reason_t34WIFI_REASON_GROUP_CIPHER_NOT_VALIDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357add540d0cbd39c63068e62d784a3017da"></a> enumerator WIFI\_REASON\_GROUP\_CIPHER\_NOT\_VALID

    <a id="_CPPv4N17wifi_err_reason_t37WIFI_REASON_PAIRWISE_CIPHER_NOT_VALIDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t37WIFI_REASON_PAIRWISE_CIPHER_NOT_VALIDE"></a> <a id="_CPPv2N17wifi_err_reason_t37WIFI_REASON_PAIRWISE_CIPHER_NOT_VALIDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a39ae347e702c2262cb41da348f14550e"></a> enumerator WIFI\_REASON\_PAIRWISE\_CIPHER\_NOT\_VALID

    <a id="_CPPv4N17wifi_err_reason_t26WIFI_REASON_AKMP_NOT_VALIDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t26WIFI_REASON_AKMP_NOT_VALIDE"></a> <a id="_CPPv2N17wifi_err_reason_t26WIFI_REASON_AKMP_NOT_VALIDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a9d3f3cb0bf8d2e5b15ed7966e60fe112"></a> enumerator WIFI\_REASON\_AKMP\_NOT\_VALID

    <a id="_CPPv4N17wifi_err_reason_t38WIFI_REASON_UNSUPPORTED_RSN_IE_VERSIONE"></a>

    <a id="_CPPv3N17wifi_err_reason_t38WIFI_REASON_UNSUPPORTED_RSN_IE_VERSIONE"></a> <a id="_CPPv2N17wifi_err_reason_t38WIFI_REASON_UNSUPPORTED_RSN_IE_VERSIONE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a417f54751618433d59f85150866c03ef"></a> enumerator WIFI\_REASON\_UNSUPPORTED\_RSN\_IE\_VERSION

    <a id="_CPPv4N17wifi_err_reason_t32WIFI_REASON_INVALID_RSN_IE_CAPABE"></a>

    <a id="_CPPv3N17wifi_err_reason_t32WIFI_REASON_INVALID_RSN_IE_CAPABE"></a> <a id="_CPPv2N17wifi_err_reason_t32WIFI_REASON_INVALID_RSN_IE_CAPABE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a0b810d356a6df8102ec0450e1c9a0618"></a> enumerator WIFI\_REASON\_INVALID\_RSN\_IE\_CAPAB

    <a id="_CPPv4N17wifi_err_reason_t35WIFI_REASON_IEEE_802_1X_AUTH_FAILEDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t35WIFI_REASON_IEEE_802_1X_AUTH_FAILEDE"></a> <a id="_CPPv2N17wifi_err_reason_t35WIFI_REASON_IEEE_802_1X_AUTH_FAILEDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a9993167a1a1889c923fcb27ff63b2c25"></a> enumerator WIFI\_REASON\_IEEE\_802\_1X\_AUTH\_FAILED

    <a id="_CPPv4N17wifi_err_reason_t33WIFI_REASON_CIPHER_SUITE_REJECTEDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t33WIFI_REASON_CIPHER_SUITE_REJECTEDE"></a> <a id="_CPPv2N17wifi_err_reason_t33WIFI_REASON_CIPHER_SUITE_REJECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357aca4ebf78c471b5da5e057175a612e911"></a> enumerator WIFI\_REASON\_CIPHER\_SUITE\_REJECTED

    <a id="_CPPv4N17wifi_err_reason_t37WIFI_REASON_TDLS_TEARDOWN_UNREACHABLEE"></a>

    <a id="_CPPv3N17wifi_err_reason_t37WIFI_REASON_TDLS_TEARDOWN_UNREACHABLEE"></a> <a id="_CPPv2N17wifi_err_reason_t37WIFI_REASON_TDLS_TEARDOWN_UNREACHABLEE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a215e65911c8c23926fded83fa39c822b"></a> enumerator WIFI\_REASON\_TDLS\_TEARDOWN\_UNREACHABLE

    <a id="_CPPv4N17wifi_err_reason_t37WIFI_REASON_TDLS_TEARDOWN_UNSPECIFIEDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t37WIFI_REASON_TDLS_TEARDOWN_UNSPECIFIEDE"></a> <a id="_CPPv2N17wifi_err_reason_t37WIFI_REASON_TDLS_TEARDOWN_UNSPECIFIEDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a7fd7c75f431d097e921d822bc92cf96b"></a> enumerator WIFI\_REASON\_TDLS\_TEARDOWN\_UNSPECIFIED

    <a id="_CPPv4N17wifi_err_reason_t34WIFI_REASON_SSP_REQUESTED_DISASSOCE"></a>

    <a id="_CPPv3N17wifi_err_reason_t34WIFI_REASON_SSP_REQUESTED_DISASSOCE"></a> <a id="_CPPv2N17wifi_err_reason_t34WIFI_REASON_SSP_REQUESTED_DISASSOCE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357adae236d4d38412f34602e992a20de7a7"></a> enumerator WIFI\_REASON\_SSP\_REQUESTED\_DISASSOC

    <a id="_CPPv4N17wifi_err_reason_t36WIFI_REASON_NO_SSP_ROAMING_AGREEMENTE"></a>

    <a id="_CPPv3N17wifi_err_reason_t36WIFI_REASON_NO_SSP_ROAMING_AGREEMENTE"></a> <a id="_CPPv2N17wifi_err_reason_t36WIFI_REASON_NO_SSP_ROAMING_AGREEMENTE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ae7ea7d61d8ae4c2429e6f71af84d50b1"></a> enumerator WIFI\_REASON\_NO\_SSP\_ROAMING\_AGREEMENT

    <a id="_CPPv4N17wifi_err_reason_t29WIFI_REASON_BAD_CIPHER_OR_AKME"></a>

    <a id="_CPPv3N17wifi_err_reason_t29WIFI_REASON_BAD_CIPHER_OR_AKME"></a> <a id="_CPPv2N17wifi_err_reason_t29WIFI_REASON_BAD_CIPHER_OR_AKME"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a63149e9c5e84c991688377aead698e9a"></a> enumerator WIFI\_REASON\_BAD\_CIPHER\_OR\_AKM

    <a id="_CPPv4N17wifi_err_reason_t40WIFI_REASON_NOT_AUTHORIZED_THIS_LOCATIONE"></a>

    <a id="_CPPv3N17wifi_err_reason_t40WIFI_REASON_NOT_AUTHORIZED_THIS_LOCATIONE"></a> <a id="_CPPv2N17wifi_err_reason_t40WIFI_REASON_NOT_AUTHORIZED_THIS_LOCATIONE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a65e5541e83035e905a7234ea4234c46a"></a> enumerator WIFI\_REASON\_NOT\_AUTHORIZED\_THIS\_LOCATION

    <a id="_CPPv4N17wifi_err_reason_t39WIFI_REASON_SERVICE_CHANGE_PRECLUDES_TSE"></a>

    <a id="_CPPv3N17wifi_err_reason_t39WIFI_REASON_SERVICE_CHANGE_PRECLUDES_TSE"></a> <a id="_CPPv2N17wifi_err_reason_t39WIFI_REASON_SERVICE_CHANGE_PRECLUDES_TSE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a82330c591a483eeeae2acbc1a1d11bda"></a> enumerator WIFI\_REASON\_SERVICE\_CHANGE\_PRECLUDES\_TS

    <a id="_CPPv4N17wifi_err_reason_t34WIFI_REASON_UNSPECIFIED_QOS_REASONE"></a>

    <a id="_CPPv3N17wifi_err_reason_t34WIFI_REASON_UNSPECIFIED_QOS_REASONE"></a> <a id="_CPPv2N17wifi_err_reason_t34WIFI_REASON_UNSPECIFIED_QOS_REASONE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a05abcccc4f4ba52fd60761f253b82087"></a> enumerator WIFI\_REASON\_UNSPECIFIED\_QOS\_REASON

    <a id="_CPPv4N17wifi_err_reason_t32WIFI_REASON_NOT_ENOUGH_BANDWIDTHE"></a>

    <a id="_CPPv3N17wifi_err_reason_t32WIFI_REASON_NOT_ENOUGH_BANDWIDTHE"></a> <a id="_CPPv2N17wifi_err_reason_t32WIFI_REASON_NOT_ENOUGH_BANDWIDTHE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a88328baecd33bd4912f35826ffef4ba5"></a> enumerator WIFI\_REASON\_NOT\_ENOUGH\_BANDWIDTH

    <a id="_CPPv4N17wifi_err_reason_t28WIFI_REASON_DISASSOC_LOW_ACKE"></a>

    <a id="_CPPv3N17wifi_err_reason_t28WIFI_REASON_DISASSOC_LOW_ACKE"></a> <a id="_CPPv2N17wifi_err_reason_t28WIFI_REASON_DISASSOC_LOW_ACKE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a999c07b2c62f5971083506245ca231d6"></a> enumerator WIFI\_REASON\_DISASSOC\_LOW\_ACK

    <a id="_CPPv4N17wifi_err_reason_t25WIFI_REASON_EXCEEDED_TXOPE"></a>

    <a id="_CPPv3N17wifi_err_reason_t25WIFI_REASON_EXCEEDED_TXOPE"></a> <a id="_CPPv2N17wifi_err_reason_t25WIFI_REASON_EXCEEDED_TXOPE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a7668084413d351d497c250eee7387d6d"></a> enumerator WIFI\_REASON\_EXCEEDED\_TXOP

    <a id="_CPPv4N17wifi_err_reason_t23WIFI_REASON_STA_LEAVINGE"></a>

    <a id="_CPPv3N17wifi_err_reason_t23WIFI_REASON_STA_LEAVINGE"></a> <a id="_CPPv2N17wifi_err_reason_t23WIFI_REASON_STA_LEAVINGE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357add591c1bedadd550edaffe45ab879e6b"></a> enumerator WIFI\_REASON\_STA\_LEAVING

    <a id="_CPPv4N17wifi_err_reason_t25WIFI_REASON_END_TS_BA_DLSE"></a>

    <a id="_CPPv3N17wifi_err_reason_t25WIFI_REASON_END_TS_BA_DLSE"></a> <a id="_CPPv2N17wifi_err_reason_t25WIFI_REASON_END_TS_BA_DLSE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a040cd385166c966f9e5ab2b11794025b"></a> enumerator WIFI\_REASON\_END\_TS\_BA\_DLS

    <a id="_CPPv4N17wifi_err_reason_t25WIFI_REASON_UNKNOWN_TS_BAE"></a>

    <a id="_CPPv3N17wifi_err_reason_t25WIFI_REASON_UNKNOWN_TS_BAE"></a> <a id="_CPPv2N17wifi_err_reason_t25WIFI_REASON_UNKNOWN_TS_BAE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ad2f05a777c06f8b54e053a56754fb4c8"></a> enumerator WIFI\_REASON\_UNKNOWN\_TS\_BA

    <a id="_CPPv4N17wifi_err_reason_t19WIFI_REASON_TIMEOUTE"></a>

    <a id="_CPPv3N17wifi_err_reason_t19WIFI_REASON_TIMEOUTE"></a> <a id="_CPPv2N17wifi_err_reason_t19WIFI_REASON_TIMEOUTE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357abf48fd373a4f12e000d90e713ee3a5f1"></a> enumerator WIFI\_REASON\_TIMEOUT

    <a id="_CPPv4N17wifi_err_reason_t28WIFI_REASON_PEERKEY_MISMATCHE"></a>

    <a id="_CPPv3N17wifi_err_reason_t28WIFI_REASON_PEERKEY_MISMATCHE"></a> <a id="_CPPv2N17wifi_err_reason_t28WIFI_REASON_PEERKEY_MISMATCHE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357aa2e5d3fa9760b684462d18061d09b071"></a> enumerator WIFI\_REASON\_PEERKEY\_MISMATCH

    <a id="_CPPv4N17wifi_err_reason_t43WIFI_REASON_AUTHORIZED_ACCESS_LIMIT_REACHEDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t43WIFI_REASON_AUTHORIZED_ACCESS_LIMIT_REACHEDE"></a> <a id="_CPPv2N17wifi_err_reason_t43WIFI_REASON_AUTHORIZED_ACCESS_LIMIT_REACHEDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a566f9c1c3a8408ed5249e2ba1771aa70"></a> enumerator WIFI\_REASON\_AUTHORIZED\_ACCESS\_LIMIT\_REACHED

    <a id="_CPPv4N17wifi_err_reason_t41WIFI_REASON_EXTERNAL_SERVICE_REQUIREMENTSE"></a>

    <a id="_CPPv3N17wifi_err_reason_t41WIFI_REASON_EXTERNAL_SERVICE_REQUIREMENTSE"></a> <a id="_CPPv2N17wifi_err_reason_t41WIFI_REASON_EXTERNAL_SERVICE_REQUIREMENTSE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a443f64781f1e5d1d8d296504a2f6dc68"></a> enumerator WIFI\_REASON\_EXTERNAL\_SERVICE\_REQUIREMENTS

    <a id="_CPPv4N17wifi_err_reason_t41WIFI_REASON_INVALID_FT_ACTION_FRAME_COUNTE"></a>

    <a id="_CPPv3N17wifi_err_reason_t41WIFI_REASON_INVALID_FT_ACTION_FRAME_COUNTE"></a> <a id="_CPPv2N17wifi_err_reason_t41WIFI_REASON_INVALID_FT_ACTION_FRAME_COUNTE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a8c766be339cb1667638adf86576f517b"></a> enumerator WIFI\_REASON\_INVALID\_FT\_ACTION\_FRAME\_COUNT

    <a id="_CPPv4N17wifi_err_reason_t25WIFI_REASON_INVALID_PMKIDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t25WIFI_REASON_INVALID_PMKIDE"></a> <a id="_CPPv2N17wifi_err_reason_t25WIFI_REASON_INVALID_PMKIDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a80c5e73cdd5cb3b2e1fef1e3509d7ab7"></a> enumerator WIFI\_REASON\_INVALID\_PMKID

    <a id="_CPPv4N17wifi_err_reason_t23WIFI_REASON_INVALID_MDEE"></a>

    <a id="_CPPv3N17wifi_err_reason_t23WIFI_REASON_INVALID_MDEE"></a> <a id="_CPPv2N17wifi_err_reason_t23WIFI_REASON_INVALID_MDEE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357aa411dacf36d46f92cb90afae19cf48ab"></a> enumerator WIFI\_REASON\_INVALID\_MDE

    <a id="_CPPv4N17wifi_err_reason_t23WIFI_REASON_INVALID_FTEE"></a>

    <a id="_CPPv3N17wifi_err_reason_t23WIFI_REASON_INVALID_FTEE"></a> <a id="_CPPv2N17wifi_err_reason_t23WIFI_REASON_INVALID_FTEE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a5ae6446bf31d57f4ccc66eb457b33f61"></a> enumerator WIFI\_REASON\_INVALID\_FTE

    <a id="_CPPv4N17wifi_err_reason_t34WIFI_REASON_MESH_PEERING_CANCELLEDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t34WIFI_REASON_MESH_PEERING_CANCELLEDE"></a> <a id="_CPPv2N17wifi_err_reason_t34WIFI_REASON_MESH_PEERING_CANCELLEDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a6b1eda6f35920b3bf55109e9c39241e2"></a> enumerator WIFI\_REASON\_MESH\_PEERING\_CANCELLED

    <a id="_CPPv4N17wifi_err_reason_t26WIFI_REASON_MESH_MAX_PEERSE"></a>

    <a id="_CPPv3N17wifi_err_reason_t26WIFI_REASON_MESH_MAX_PEERSE"></a> <a id="_CPPv2N17wifi_err_reason_t26WIFI_REASON_MESH_MAX_PEERSE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357abf3a452a2c8cb3d6a6ae096815687de9"></a> enumerator WIFI\_REASON\_MESH\_MAX\_PEERS

    <a id="_CPPv4N17wifi_err_reason_t40WIFI_REASON_MESH_CONFIG_POLICY_VIOLATIONE"></a>

    <a id="_CPPv3N17wifi_err_reason_t40WIFI_REASON_MESH_CONFIG_POLICY_VIOLATIONE"></a> <a id="_CPPv2N17wifi_err_reason_t40WIFI_REASON_MESH_CONFIG_POLICY_VIOLATIONE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a7a7754fb7300c0e91cebbebb42775f95"></a> enumerator WIFI\_REASON\_MESH\_CONFIG\_POLICY\_VIOLATION

    <a id="_CPPv4N17wifi_err_reason_t27WIFI_REASON_MESH_CLOSE_RCVDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t27WIFI_REASON_MESH_CLOSE_RCVDE"></a> <a id="_CPPv2N17wifi_err_reason_t27WIFI_REASON_MESH_CLOSE_RCVDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357af5e0a3e9e5d506b7edb166ba248bba44"></a> enumerator WIFI\_REASON\_MESH\_CLOSE\_RCVD

    <a id="_CPPv4N17wifi_err_reason_t28WIFI_REASON_MESH_MAX_RETRIESE"></a>

    <a id="_CPPv3N17wifi_err_reason_t28WIFI_REASON_MESH_MAX_RETRIESE"></a> <a id="_CPPv2N17wifi_err_reason_t28WIFI_REASON_MESH_MAX_RETRIESE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ae74a633ca82e9b09edf2cbaecb67b8df"></a> enumerator WIFI\_REASON\_MESH\_MAX\_RETRIES

    <a id="_CPPv4N17wifi_err_reason_t32WIFI_REASON_MESH_CONFIRM_TIMEOUTE"></a>

    <a id="_CPPv3N17wifi_err_reason_t32WIFI_REASON_MESH_CONFIRM_TIMEOUTE"></a> <a id="_CPPv2N17wifi_err_reason_t32WIFI_REASON_MESH_CONFIRM_TIMEOUTE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a13e4c1892196f91b050a1d12d3b2136a"></a> enumerator WIFI\_REASON\_MESH\_CONFIRM\_TIMEOUT

    <a id="_CPPv4N17wifi_err_reason_t28WIFI_REASON_MESH_INVALID_GTKE"></a>

    <a id="_CPPv3N17wifi_err_reason_t28WIFI_REASON_MESH_INVALID_GTKE"></a> <a id="_CPPv2N17wifi_err_reason_t28WIFI_REASON_MESH_INVALID_GTKE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357aeda8587c6defef19a15d827687c99723"></a> enumerator WIFI\_REASON\_MESH\_INVALID\_GTK

    <a id="_CPPv4N17wifi_err_reason_t36WIFI_REASON_MESH_INCONSISTENT_PARAMSE"></a>

    <a id="_CPPv3N17wifi_err_reason_t36WIFI_REASON_MESH_INCONSISTENT_PARAMSE"></a> <a id="_CPPv2N17wifi_err_reason_t36WIFI_REASON_MESH_INCONSISTENT_PARAMSE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ac92b7ce586eaacfee48fd6ca60ab32fd"></a> enumerator WIFI\_REASON\_MESH\_INCONSISTENT\_PARAMS

    <a id="_CPPv4N17wifi_err_reason_t37WIFI_REASON_MESH_INVALID_SECURITY_CAPE"></a>

    <a id="_CPPv3N17wifi_err_reason_t37WIFI_REASON_MESH_INVALID_SECURITY_CAPE"></a> <a id="_CPPv2N17wifi_err_reason_t37WIFI_REASON_MESH_INVALID_SECURITY_CAPE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357acff0977b60ba0201cc000afeeac159db"></a> enumerator WIFI\_REASON\_MESH\_INVALID\_SECURITY\_CAP

    <a id="_CPPv4N17wifi_err_reason_t41WIFI_REASON_MESH_PATH_ERROR_NO_PROXY_INFOE"></a>

    <a id="_CPPv3N17wifi_err_reason_t41WIFI_REASON_MESH_PATH_ERROR_NO_PROXY_INFOE"></a> <a id="_CPPv2N17wifi_err_reason_t41WIFI_REASON_MESH_PATH_ERROR_NO_PROXY_INFOE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a5403edf3f9c99372fb24d3d0c6e362ec"></a> enumerator WIFI\_REASON\_MESH\_PATH\_ERROR\_NO\_PROXY\_INFO

    <a id="_CPPv4N17wifi_err_reason_t46WIFI_REASON_MESH_PATH_ERROR_NO_FORWARDING_INFOE"></a>

    <a id="_CPPv3N17wifi_err_reason_t46WIFI_REASON_MESH_PATH_ERROR_NO_FORWARDING_INFOE"></a> <a id="_CPPv2N17wifi_err_reason_t46WIFI_REASON_MESH_PATH_ERROR_NO_FORWARDING_INFOE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357af4c91cecda66e66285fad2c02270df3d"></a> enumerator WIFI\_REASON\_MESH\_PATH\_ERROR\_NO\_FORWARDING\_INFO

    <a id="_CPPv4N17wifi_err_reason_t44WIFI_REASON_MESH_PATH_ERROR_DEST_UNREACHABLEE"></a>

    <a id="_CPPv3N17wifi_err_reason_t44WIFI_REASON_MESH_PATH_ERROR_DEST_UNREACHABLEE"></a> <a id="_CPPv2N17wifi_err_reason_t44WIFI_REASON_MESH_PATH_ERROR_DEST_UNREACHABLEE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357ac0c9474e2c67608652462ae95d76f496"></a> enumerator WIFI\_REASON\_MESH\_PATH\_ERROR\_DEST\_UNREACHABLE

    <a id="_CPPv4N17wifi_err_reason_t46WIFI_REASON_MAC_ADDRESS_ALREADY_EXISTS_IN_MBSSE"></a>

    <a id="_CPPv3N17wifi_err_reason_t46WIFI_REASON_MAC_ADDRESS_ALREADY_EXISTS_IN_MBSSE"></a> <a id="_CPPv2N17wifi_err_reason_t46WIFI_REASON_MAC_ADDRESS_ALREADY_EXISTS_IN_MBSSE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a5aca4931966b6b7f27006731e3292202"></a> enumerator WIFI\_REASON\_MAC\_ADDRESS\_ALREADY\_EXISTS\_IN\_MBSS

    <a id="_CPPv4N17wifi_err_reason_t46WIFI_REASON_MESH_CHANNEL_SWITCH_REGULATORY_REQE"></a>

    <a id="_CPPv3N17wifi_err_reason_t46WIFI_REASON_MESH_CHANNEL_SWITCH_REGULATORY_REQE"></a> <a id="_CPPv2N17wifi_err_reason_t46WIFI_REASON_MESH_CHANNEL_SWITCH_REGULATORY_REQE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a5a57cf5fe5ee4546505536064f8d216b"></a> enumerator WIFI\_REASON\_MESH\_CHANNEL\_SWITCH\_REGULATORY\_REQ

    <a id="_CPPv4N17wifi_err_reason_t43WIFI_REASON_MESH_CHANNEL_SWITCH_UNSPECIFIEDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t43WIFI_REASON_MESH_CHANNEL_SWITCH_UNSPECIFIEDE"></a> <a id="_CPPv2N17wifi_err_reason_t43WIFI_REASON_MESH_CHANNEL_SWITCH_UNSPECIFIEDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a7169d1770e021ac4d9caf58ef930b7b8"></a> enumerator WIFI\_REASON\_MESH\_CHANNEL\_SWITCH\_UNSPECIFIED

    <a id="_CPPv4N17wifi_err_reason_t23WIFI_REASON_BEACON_LOSTE"></a>

    <a id="_CPPv3N17wifi_err_reason_t23WIFI_REASON_BEACON_LOSTE"></a> <a id="_CPPv2N17wifi_err_reason_t23WIFI_REASON_BEACON_LOSTE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a062cefbcbce2d1ab72e5c125fc644ab1"></a> enumerator WIFI\_REASON\_BEACON\_LOST
    :   The BK STA can’t detect the beacon of the connected AP

    <a id="_CPPv4N17wifi_err_reason_t23WIFI_REASON_NO_AP_FOUNDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t23WIFI_REASON_NO_AP_FOUNDE"></a> <a id="_CPPv2N17wifi_err_reason_t23WIFI_REASON_NO_AP_FOUNDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357af82af1859d31e0937c7270d9cc9d9206"></a> enumerator WIFI\_REASON\_NO\_AP\_FOUND
    :   Can’t find the target AP

    <a id="_CPPv4N17wifi_err_reason_t26WIFI_REASON_WRONG_PASSWORDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t26WIFI_REASON_WRONG_PASSWORDE"></a> <a id="_CPPv2N17wifi_err_reason_t26WIFI_REASON_WRONG_PASSWORDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a05668c52edd86c86cb54a1e60b635cb5"></a> enumerator WIFI\_REASON\_WRONG\_PASSWORD
    :   The password is wrong

    <a id="_CPPv4N17wifi_err_reason_t29WIFI_REASON_DISCONNECT_BY_APPE"></a>

    <a id="_CPPv3N17wifi_err_reason_t29WIFI_REASON_DISCONNECT_BY_APPE"></a> <a id="_CPPv2N17wifi_err_reason_t29WIFI_REASON_DISCONNECT_BY_APPE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a8020cf41e19caed91a3ac9eb40de87de"></a> enumerator WIFI\_REASON\_DISCONNECT\_BY\_APP
    :   The BK STA disconnected by application

    <a id="_CPPv4N17wifi_err_reason_t24WIFI_REASON_DHCP_TIMEOUTE"></a>

    <a id="_CPPv3N17wifi_err_reason_t24WIFI_REASON_DHCP_TIMEOUTE"></a> <a id="_CPPv2N17wifi_err_reason_t24WIFI_REASON_DHCP_TIMEOUTE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a442ca60ac9b344d4338487f8dd1f4fd3"></a> enumerator WIFI\_REASON\_DHCP\_TIMEOUT
    :   The BK STA dhcp timeout, 20s

    <a id="_CPPv4N17wifi_err_reason_t26WIFI_REASON_P2P_NEG_FAILEDE"></a>

    <a id="_CPPv3N17wifi_err_reason_t26WIFI_REASON_P2P_NEG_FAILEDE"></a> <a id="_CPPv2N17wifi_err_reason_t26WIFI_REASON_P2P_NEG_FAILEDE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357a45913cf0f466bfe5da071a7c43bf769a"></a> enumerator WIFI\_REASON\_P2P\_NEG\_FAILED
    :   The BK P2P neg failed

    <a id="_CPPv4N17wifi_err_reason_t15WIFI_REASON_MAXE"></a>

    <a id="_CPPv3N17wifi_err_reason_t15WIFI_REASON_MAXE"></a> <a id="_CPPv2N17wifi_err_reason_t15WIFI_REASON_MAXE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaf2f44e69763071bbe8c3903158c5a357abb99e24bbd9427f0708c926b0de86b2d"></a> enumerator WIFI\_REASON\_MAX
    :   The BK STA connect success

<a id="_CPPv415wifi_security_t"></a>

<a id="_CPPv315wifi_security_t"></a> <a id="_CPPv215wifi_security_t"></a> <a id="group__bk__api__wifi__v2__enum_1ga010e38e08f1370cc671b2f65a26042ad"></a> enum wifi\_security\_t
:   *Values:*

    <a id="_CPPv4N15wifi_security_t18WIFI_SECURITY_NONEE"></a>

    <a id="_CPPv3N15wifi_security_t18WIFI_SECURITY_NONEE"></a> <a id="_CPPv2N15wifi_security_t18WIFI_SECURITY_NONEE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada33a293ccf3a4ffe3ad24bda9145190a9"></a> enumerator WIFI\_SECURITY\_NONE
    :   Open system.

    <a id="_CPPv4N15wifi_security_t17WIFI_SECURITY_WEPE"></a>

    <a id="_CPPv3N15wifi_security_t17WIFI_SECURITY_WEPE"></a> <a id="_CPPv2N15wifi_security_t17WIFI_SECURITY_WEPE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada2051e50876375942df94bdd2e1f5dae6"></a> enumerator WIFI\_SECURITY\_WEP
    :   WEP security, **it’s unsafe security, please don’t use it**

    <a id="_CPPv4N15wifi_security_t22WIFI_SECURITY_WPA_TKIPE"></a>

    <a id="_CPPv3N15wifi_security_t22WIFI_SECURITY_WPA_TKIPE"></a> <a id="_CPPv2N15wifi_security_t22WIFI_SECURITY_WPA_TKIPE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada40fb9b4f6c3427830eb50439b9009ea4"></a> enumerator WIFI\_SECURITY\_WPA\_TKIP
    :   WPA TKIP

    <a id="_CPPv4N15wifi_security_t21WIFI_SECURITY_WPA_AESE"></a>

    <a id="_CPPv3N15wifi_security_t21WIFI_SECURITY_WPA_AESE"></a> <a id="_CPPv2N15wifi_security_t21WIFI_SECURITY_WPA_AESE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042adaa13f938cb24eea07b70eabd66ade152b"></a> enumerator WIFI\_SECURITY\_WPA\_AES
    :   WPA AES

    <a id="_CPPv4N15wifi_security_t23WIFI_SECURITY_WPA_MIXEDE"></a>

    <a id="_CPPv3N15wifi_security_t23WIFI_SECURITY_WPA_MIXEDE"></a> <a id="_CPPv2N15wifi_security_t23WIFI_SECURITY_WPA_MIXEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada6e920955c329f296285d0833c41f5424"></a> enumerator WIFI\_SECURITY\_WPA\_MIXED
    :   WPA AES or TKIP

    <a id="_CPPv4N15wifi_security_t23WIFI_SECURITY_WPA2_TKIPE"></a>

    <a id="_CPPv3N15wifi_security_t23WIFI_SECURITY_WPA2_TKIPE"></a> <a id="_CPPv2N15wifi_security_t23WIFI_SECURITY_WPA2_TKIPE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada09ae5057124a07bd0a01951e4ae6a7c2"></a> enumerator WIFI\_SECURITY\_WPA2\_TKIP
    :   WPA2 TKIP

    <a id="_CPPv4N15wifi_security_t22WIFI_SECURITY_WPA2_AESE"></a>

    <a id="_CPPv3N15wifi_security_t22WIFI_SECURITY_WPA2_AESE"></a> <a id="_CPPv2N15wifi_security_t22WIFI_SECURITY_WPA2_AESE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada573efbfc2c9182f319b301ba2584fc46"></a> enumerator WIFI\_SECURITY\_WPA2\_AES
    :   WPA2 AES

    <a id="_CPPv4N15wifi_security_t24WIFI_SECURITY_WPA2_MIXEDE"></a>

    <a id="_CPPv3N15wifi_security_t24WIFI_SECURITY_WPA2_MIXEDE"></a> <a id="_CPPv2N15wifi_security_t24WIFI_SECURITY_WPA2_MIXEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042adaf66ff147f179d4808272771237b60533"></a> enumerator WIFI\_SECURITY\_WPA2\_MIXED
    :   WPA2 AES or TKIP

    <a id="_CPPv4N15wifi_security_t22WIFI_SECURITY_WPA3_SAEE"></a>

    <a id="_CPPv3N15wifi_security_t22WIFI_SECURITY_WPA3_SAEE"></a> <a id="_CPPv2N15wifi_security_t22WIFI_SECURITY_WPA3_SAEE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada111c17fe9ff0e63765051aa41406ce0e"></a> enumerator WIFI\_SECURITY\_WPA3\_SAE
    :   WPA3 SAE

    <a id="_CPPv4N15wifi_security_t29WIFI_SECURITY_WPA3_WPA2_MIXEDE"></a>

    <a id="_CPPv3N15wifi_security_t29WIFI_SECURITY_WPA3_WPA2_MIXEDE"></a> <a id="_CPPv2N15wifi_security_t29WIFI_SECURITY_WPA3_WPA2_MIXEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042adab90b89fbe6f6820a5e9fa243f85aceea"></a> enumerator WIFI\_SECURITY\_WPA3\_WPA2\_MIXED
    :   WPA3 SAE or WPA2 AES

    <a id="_CPPv4N15wifi_security_t17WIFI_SECURITY_EAPE"></a>

    <a id="_CPPv3N15wifi_security_t17WIFI_SECURITY_EAPE"></a> <a id="_CPPv2N15wifi_security_t17WIFI_SECURITY_EAPE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada0a1de0eb5a7a0dba682a19ffb7cf8103"></a> enumerator WIFI\_SECURITY\_EAP
    :   EAP

    <a id="_CPPv4N15wifi_security_t17WIFI_SECURITY_OWEE"></a>

    <a id="_CPPv3N15wifi_security_t17WIFI_SECURITY_OWEE"></a> <a id="_CPPv2N15wifi_security_t17WIFI_SECURITY_OWEE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada48e16f954c45a290cff801ca20586f0f"></a> enumerator WIFI\_SECURITY\_OWE
    :   OWE

    <a id="_CPPv4N15wifi_security_t18WIFI_SECURITY_AUTOE"></a>

    <a id="_CPPv3N15wifi_security_t18WIFI_SECURITY_AUTOE"></a> <a id="_CPPv2N15wifi_security_t18WIFI_SECURITY_AUTOE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada67b77452432c7a01ffa6a3008941ad6c"></a> enumerator WIFI\_SECURITY\_AUTO
    :   WiFi automatically detect the security type

    <a id="_CPPv4N15wifi_security_t27WIFI_SECURITY_TYPE_WAPI_PSKE"></a>

    <a id="_CPPv3N15wifi_security_t27WIFI_SECURITY_TYPE_WAPI_PSKE"></a> <a id="_CPPv2N15wifi_security_t27WIFI_SECURITY_TYPE_WAPI_PSKE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada1358abe54efe484d0c67033fb2edd518"></a> enumerator WIFI\_SECURITY\_TYPE\_WAPI\_PSK

    <a id="_CPPv4N15wifi_security_t28WIFI_SECURITY_TYPE_WAPI_CERTE"></a>

    <a id="_CPPv3N15wifi_security_t28WIFI_SECURITY_TYPE_WAPI_CERTE"></a> <a id="_CPPv2N15wifi_security_t28WIFI_SECURITY_TYPE_WAPI_CERTE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada6ed77c40d27fd70bc1a78a5581b242d5"></a> enumerator WIFI\_SECURITY\_TYPE\_WAPI\_CERT

    <a id="_CPPv4N15wifi_security_t31WIFI_SECURITY_TYPE_WAPI_UNKNOWNE"></a>

    <a id="_CPPv3N15wifi_security_t31WIFI_SECURITY_TYPE_WAPI_UNKNOWNE"></a> <a id="_CPPv2N15wifi_security_t31WIFI_SECURITY_TYPE_WAPI_UNKNOWNE"></a> <a id="group__bk__api__wifi__v2__enum_1gga010e38e08f1370cc671b2f65a26042ada1f6c634e21bf5622d4227ccaefef151f"></a> enumerator WIFI\_SECURITY\_TYPE\_WAPI\_UNKNOWN

<a id="_CPPv417wifi_link_state_t"></a>

<a id="_CPPv317wifi_link_state_t"></a> <a id="_CPPv217wifi_link_state_t"></a> <a id="group__bk__api__wifi__v2__enum_1ga4173eff95b62808051ec8f9af3435b10"></a> enum wifi\_link\_state\_t
:   *Values:*

    <a id="_CPPv4N17wifi_link_state_t23WIFI_LINKSTATE_STA_IDLEE"></a>

    <a id="_CPPv3N17wifi_link_state_t23WIFI_LINKSTATE_STA_IDLEE"></a> <a id="_CPPv2N17wifi_link_state_t23WIFI_LINKSTATE_STA_IDLEE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10a09a516d7abd3c5681de1aadf097f4310"></a> enumerator WIFI\_LINKSTATE\_STA\_IDLE
    :   sta mode is idle

    <a id="_CPPv4N17wifi_link_state_t29WIFI_LINKSTATE_STA_CONNECTINGE"></a>

    <a id="_CPPv3N17wifi_link_state_t29WIFI_LINKSTATE_STA_CONNECTINGE"></a> <a id="_CPPv2N17wifi_link_state_t29WIFI_LINKSTATE_STA_CONNECTINGE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10a6cdfde664c6840fb4d0736ca725e9df4"></a> enumerator WIFI\_LINKSTATE\_STA\_CONNECTING
    :   sta mode is connecting

    <a id="_CPPv4N17wifi_link_state_t31WIFI_LINKSTATE_STA_DISCONNECTEDE"></a>

    <a id="_CPPv3N17wifi_link_state_t31WIFI_LINKSTATE_STA_DISCONNECTEDE"></a> <a id="_CPPv2N17wifi_link_state_t31WIFI_LINKSTATE_STA_DISCONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10a284f9d36abc54bc38982213f63bf6e8b"></a> enumerator WIFI\_LINKSTATE\_STA\_DISCONNECTED
    :   sta mode is disconnected

    <a id="_CPPv4N17wifi_link_state_t28WIFI_LINKSTATE_STA_CONNECTEDE"></a>

    <a id="_CPPv3N17wifi_link_state_t28WIFI_LINKSTATE_STA_CONNECTEDE"></a> <a id="_CPPv2N17wifi_link_state_t28WIFI_LINKSTATE_STA_CONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10a26df5f7619ee219bd4aab733a8a63e62"></a> enumerator WIFI\_LINKSTATE\_STA\_CONNECTED
    :   sta mode is connected

    <a id="_CPPv4N17wifi_link_state_t33WIFI_LINKSTATE_STA_CONNECT_FAILEDE"></a>

    <a id="_CPPv3N17wifi_link_state_t33WIFI_LINKSTATE_STA_CONNECT_FAILEDE"></a> <a id="_CPPv2N17wifi_link_state_t33WIFI_LINKSTATE_STA_CONNECT_FAILEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10aca4a8a6f8b98b6b23ae47b0d2be0965e"></a> enumerator WIFI\_LINKSTATE\_STA\_CONNECT\_FAILED
    :   sta mode is connec fail

    <a id="_CPPv4N17wifi_link_state_t25WIFI_LINKSTATE_STA_GOT_IPE"></a>

    <a id="_CPPv3N17wifi_link_state_t25WIFI_LINKSTATE_STA_GOT_IPE"></a> <a id="_CPPv2N17wifi_link_state_t25WIFI_LINKSTATE_STA_GOT_IPE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10ae63b6c62932542faeff9cdc3b1bccfad"></a> enumerator WIFI\_LINKSTATE\_STA\_GOT\_IP
    :   sta mode got ip

    <a id="_CPPv4N17wifi_link_state_t28WIFI_LINKSTATE_STA_SCAN_DONEE"></a>

    <a id="_CPPv3N17wifi_link_state_t28WIFI_LINKSTATE_STA_SCAN_DONEE"></a> <a id="_CPPv2N17wifi_link_state_t28WIFI_LINKSTATE_STA_SCAN_DONEE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10ac9704f2e626449f014f21b2040f198e5"></a> enumerator WIFI\_LINKSTATE\_STA\_SCAN\_DONE

    <a id="_CPPv4N17wifi_link_state_t27WIFI_LINKSTATE_AP_CONNECTEDE"></a>

    <a id="_CPPv3N17wifi_link_state_t27WIFI_LINKSTATE_AP_CONNECTEDE"></a> <a id="_CPPv2N17wifi_link_state_t27WIFI_LINKSTATE_AP_CONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10a8c3041ca9da36552c1c879bf9f40bf53"></a> enumerator WIFI\_LINKSTATE\_AP\_CONNECTED
    :   softap mode, a client association success

    <a id="_CPPv4N17wifi_link_state_t30WIFI_LINKSTATE_AP_DISCONNECTEDE"></a>

    <a id="_CPPv3N17wifi_link_state_t30WIFI_LINKSTATE_AP_DISCONNECTEDE"></a> <a id="_CPPv2N17wifi_link_state_t30WIFI_LINKSTATE_AP_DISCONNECTEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10adb4180194c47e43de9b85af3d2913c56"></a> enumerator WIFI\_LINKSTATE\_AP\_DISCONNECTED
    :   softap mode, a client disconnect

    <a id="_CPPv4N17wifi_link_state_t32WIFI_LINKSTATE_AP_CONNECT_FAILEDE"></a>

    <a id="_CPPv3N17wifi_link_state_t32WIFI_LINKSTATE_AP_CONNECT_FAILEDE"></a> <a id="_CPPv2N17wifi_link_state_t32WIFI_LINKSTATE_AP_CONNECT_FAILEDE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10af5a9e0f229b6341f43ebd3c57e6e0e5b"></a> enumerator WIFI\_LINKSTATE\_AP\_CONNECT\_FAILED
    :   softap mode, a client association failed

    <a id="_CPPv4N17wifi_link_state_t18WIFI_LINKSTATE_MAXE"></a>

    <a id="_CPPv3N17wifi_link_state_t18WIFI_LINKSTATE_MAXE"></a> <a id="_CPPv2N17wifi_link_state_t18WIFI_LINKSTATE_MAXE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4173eff95b62808051ec8f9af3435b10a5ba0b8dc6fb0d9484d7ea70ae1b4dd9a"></a> enumerator WIFI\_LINKSTATE\_MAX
    :   reserved

<a id="_CPPv421wifi_country_policy_t"></a>

<a id="_CPPv321wifi_country_policy_t"></a> <a id="_CPPv221wifi_country_policy_t"></a> <a id="group__bk__api__wifi__v2__enum_1ga5bc9a18309dadba51c6b33742b22caab"></a> enum wifi\_country\_policy\_t
:   *Values:*

    <a id="_CPPv4N21wifi_country_policy_t24WIFI_COUNTRY_POLICY_AUTOE"></a>

    <a id="_CPPv3N21wifi_country_policy_t24WIFI_COUNTRY_POLICY_AUTOE"></a> <a id="_CPPv2N21wifi_country_policy_t24WIFI_COUNTRY_POLICY_AUTOE"></a> <a id="group__bk__api__wifi__v2__enum_1gga5bc9a18309dadba51c6b33742b22caaba5e8710ac8a30e8f1bc27b0c4f6945301"></a> enumerator WIFI\_COUNTRY\_POLICY\_AUTO
    :   Country policy is auto, use the country info of AP to which the station is connected

    <a id="_CPPv4N21wifi_country_policy_t26WIFI_COUNTRY_POLICY_MANUALE"></a>

    <a id="_CPPv3N21wifi_country_policy_t26WIFI_COUNTRY_POLICY_MANUALE"></a> <a id="_CPPv2N21wifi_country_policy_t26WIFI_COUNTRY_POLICY_MANUALE"></a> <a id="group__bk__api__wifi__v2__enum_1gga5bc9a18309dadba51c6b33742b22caabad7e0750058f60a010b71d2445e44dde1"></a> enumerator WIFI\_COUNTRY\_POLICY\_MANUAL
    :   Country policy is manual, always use the configured country info

<a id="_CPPv421wifi_second_channel_t"></a>

<a id="_CPPv321wifi_second_channel_t"></a> <a id="_CPPv221wifi_second_channel_t"></a> <a id="group__bk__api__wifi__v2__enum_1ga3306794e1a9adad8e00f7d68e7930805"></a> enum wifi\_second\_channel\_t
:   *Values:*

    <a id="_CPPv4N21wifi_second_channel_t24WIFI_SECOND_CHANNEL_NONEE"></a>

    <a id="_CPPv3N21wifi_second_channel_t24WIFI_SECOND_CHANNEL_NONEE"></a> <a id="_CPPv2N21wifi_second_channel_t24WIFI_SECOND_CHANNEL_NONEE"></a> <a id="group__bk__api__wifi__v2__enum_1gga3306794e1a9adad8e00f7d68e7930805a58b87547af406c2cd74bc85612d148f2"></a> enumerator WIFI\_SECOND\_CHANNEL\_NONE
    :   HT20 mode, no secondary channel

    <a id="_CPPv4N21wifi_second_channel_t25WIFI_SECOND_CHANNEL_ABOVEE"></a>

    <a id="_CPPv3N21wifi_second_channel_t25WIFI_SECOND_CHANNEL_ABOVEE"></a> <a id="_CPPv2N21wifi_second_channel_t25WIFI_SECOND_CHANNEL_ABOVEE"></a> <a id="group__bk__api__wifi__v2__enum_1gga3306794e1a9adad8e00f7d68e7930805a891095a7e17644b9912d5470979954b1"></a> enumerator WIFI\_SECOND\_CHANNEL\_ABOVE
    :   Second channel is above the primary channel

    <a id="_CPPv4N21wifi_second_channel_t25WIFI_SECOND_CHANNEL_BELOWE"></a>

    <a id="_CPPv3N21wifi_second_channel_t25WIFI_SECOND_CHANNEL_BELOWE"></a> <a id="_CPPv2N21wifi_second_channel_t25WIFI_SECOND_CHANNEL_BELOWE"></a> <a id="group__bk__api__wifi__v2__enum_1gga3306794e1a9adad8e00f7d68e7930805a904ab4a518e0a1b4e3b2bbb48cb6b358"></a> enumerator WIFI\_SECOND\_CHANNEL\_BELOW
    :   Second channel is below the primary channel

<a id="_CPPv417wifi_regulation_t"></a>

<a id="_CPPv317wifi_regulation_t"></a> <a id="_CPPv217wifi_regulation_t"></a> <a id="group__bk__api__wifi__v2__enum_1ga37e2eea436f04320ed304089acce47e5"></a> enum wifi\_regulation\_t
:   *Values:*

    <a id="_CPPv4N17wifi_regulation_t14WIFI_REGU_NULLE"></a>

    <a id="_CPPv3N17wifi_regulation_t14WIFI_REGU_NULLE"></a> <a id="_CPPv2N17wifi_regulation_t14WIFI_REGU_NULLE"></a> <a id="group__bk__api__wifi__v2__enum_1gga37e2eea436f04320ed304089acce47e5a2b9d49ee82a9ae3de8c9b7caea8b276b"></a> enumerator WIFI\_REGU\_NULL

    <a id="_CPPv4N17wifi_regulation_t13WIFI_REGU_FCCE"></a>

    <a id="_CPPv3N17wifi_regulation_t13WIFI_REGU_FCCE"></a> <a id="_CPPv2N17wifi_regulation_t13WIFI_REGU_FCCE"></a> <a id="group__bk__api__wifi__v2__enum_1gga37e2eea436f04320ed304089acce47e5ad5c49dee3f40770637b7996c241e5d13"></a> enumerator WIFI\_REGU\_FCC

    <a id="_CPPv4N17wifi_regulation_t14WIFI_REGU_ETSIE"></a>

    <a id="_CPPv3N17wifi_regulation_t14WIFI_REGU_ETSIE"></a> <a id="_CPPv2N17wifi_regulation_t14WIFI_REGU_ETSIE"></a> <a id="group__bk__api__wifi__v2__enum_1gga37e2eea436f04320ed304089acce47e5a2da946c884d2b5a9ad6e29f794a97072"></a> enumerator WIFI\_REGU\_ETSI

    <a id="_CPPv4N17wifi_regulation_t13WIFI_REGU_MKKE"></a>

    <a id="_CPPv3N17wifi_regulation_t13WIFI_REGU_MKKE"></a> <a id="_CPPv2N17wifi_regulation_t13WIFI_REGU_MKKE"></a> <a id="group__bk__api__wifi__v2__enum_1gga37e2eea436f04320ed304089acce47e5aebc91b4082419bf07ec37d75db2901ab"></a> enumerator WIFI\_REGU\_MKK

    <a id="_CPPv4N17wifi_regulation_t13WIFI_REGU_EXTE"></a>

    <a id="_CPPv3N17wifi_regulation_t13WIFI_REGU_EXTE"></a> <a id="_CPPv2N17wifi_regulation_t13WIFI_REGU_EXTE"></a> <a id="group__bk__api__wifi__v2__enum_1gga37e2eea436f04320ed304089acce47e5ad6bfafda7a5621fb772971568131cb60"></a> enumerator WIFI\_REGU\_EXT

<a id="_CPPv418wifi_ratesection_t"></a>

<a id="_CPPv318wifi_ratesection_t"></a> <a id="_CPPv218wifi_ratesection_t"></a> <a id="group__bk__api__wifi__v2__enum_1ga4f8d473202c3e99fd3ea319e6d43531d"></a> enum wifi\_ratesection\_t
:   *Values:*

    <a id="_CPPv4N18wifi_ratesection_t12WIFI_RS_NULLE"></a>

    <a id="_CPPv3N18wifi_ratesection_t12WIFI_RS_NULLE"></a> <a id="_CPPv2N18wifi_ratesection_t12WIFI_RS_NULLE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4f8d473202c3e99fd3ea319e6d43531dae7c4a462fcd5464bd5be74bd1bec937d"></a> enumerator WIFI\_RS\_NULL

    <a id="_CPPv4N18wifi_ratesection_t11WIFI_RS_CCKE"></a>

    <a id="_CPPv3N18wifi_ratesection_t11WIFI_RS_CCKE"></a> <a id="_CPPv2N18wifi_ratesection_t11WIFI_RS_CCKE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4f8d473202c3e99fd3ea319e6d43531daa816a3830d8b26a8fdc2c08d213064b9"></a> enumerator WIFI\_RS\_CCK

    <a id="_CPPv4N18wifi_ratesection_t12WIFI_RS_OFDME"></a>

    <a id="_CPPv3N18wifi_ratesection_t12WIFI_RS_OFDME"></a> <a id="_CPPv2N18wifi_ratesection_t12WIFI_RS_OFDME"></a> <a id="group__bk__api__wifi__v2__enum_1gga4f8d473202c3e99fd3ea319e6d43531da654114e9a4a3d4f4273dc679a9be1ec9"></a> enumerator WIFI\_RS\_OFDM

    <a id="_CPPv4N18wifi_ratesection_t10WIFI_RS_HTE"></a>

    <a id="_CPPv3N18wifi_ratesection_t10WIFI_RS_HTE"></a> <a id="_CPPv2N18wifi_ratesection_t10WIFI_RS_HTE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4f8d473202c3e99fd3ea319e6d43531da307e25d4b9f6cf12022de6f80aa9ee1a"></a> enumerator WIFI\_RS\_HT

    <a id="_CPPv4N18wifi_ratesection_t11WIFI_RS_VHTE"></a>

    <a id="_CPPv3N18wifi_ratesection_t11WIFI_RS_VHTE"></a> <a id="_CPPv2N18wifi_ratesection_t11WIFI_RS_VHTE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4f8d473202c3e99fd3ea319e6d43531daf848d2dc01992814ea9d1839cd82b0d2"></a> enumerator WIFI\_RS\_VHT

    <a id="_CPPv4N18wifi_ratesection_t10WIFI_RS_HEE"></a>

    <a id="_CPPv3N18wifi_ratesection_t10WIFI_RS_HEE"></a> <a id="_CPPv2N18wifi_ratesection_t10WIFI_RS_HEE"></a> <a id="group__bk__api__wifi__v2__enum_1gga4f8d473202c3e99fd3ea319e6d43531da9d66c91f5b53cf8b04a5fcd390959f52"></a> enumerator WIFI\_RS\_HE

<a id="_CPPv417wifi_tx_raw_pkt_t"></a>

<a id="_CPPv317wifi_tx_raw_pkt_t"></a> <a id="_CPPv217wifi_tx_raw_pkt_t"></a> <a id="group__bk__api__wifi__v2__enum_1gaba2da6a456633bee003189c8076e40dd"></a> enum wifi\_tx\_raw\_pkt\_t
:   *Values:*

    <a id="_CPPv4N17wifi_tx_raw_pkt_t16WIFI_TX_RAW_DATAE"></a>

    <a id="_CPPv3N17wifi_tx_raw_pkt_t16WIFI_TX_RAW_DATAE"></a> <a id="_CPPv2N17wifi_tx_raw_pkt_t16WIFI_TX_RAW_DATAE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaba2da6a456633bee003189c8076e40dda38e77f10b07e6b822c02d23acf6af7f8"></a> enumerator WIFI\_TX\_RAW\_DATA
    :   Wi-Fi tx raw data

    <a id="_CPPv4N17wifi_tx_raw_pkt_t25WIFI_TX_RAW_SPECIAL_DATTAE"></a>

    <a id="_CPPv3N17wifi_tx_raw_pkt_t25WIFI_TX_RAW_SPECIAL_DATTAE"></a> <a id="_CPPv2N17wifi_tx_raw_pkt_t25WIFI_TX_RAW_SPECIAL_DATTAE"></a> <a id="group__bk__api__wifi__v2__enum_1ggaba2da6a456633bee003189c8076e40dda20a231bdbdd94b8eec47e512d01fbb91"></a> enumerator WIFI\_TX\_RAW\_SPECIAL\_DATTA
    :   Wi-Fi tx raw speacial data

<a id="_CPPv417wifi_capability_t"></a>

<a id="_CPPv317wifi_capability_t"></a> <a id="_CPPv217wifi_capability_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga1bc14fb46de73ab0c10a7aa6f93469b1"></a> enum wifi\_capability\_t
:   WiFi capability interface ID.

    *Values:*

    <a id="_CPPv4N17wifi_capability_t19WIFI_CAPA_ID_ERP_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t19WIFI_CAPA_ID_ERP_ENE"></a> <a id="_CPPv2N17wifi_capability_t19WIFI_CAPA_ID_ERP_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1ab3e86139f96fa7bf44bfca2e48e99288"></a> enumerator WIFI\_CAPA\_ID\_ERP\_EN
    :   Update Wi-Fi 11g support capability

    <a id="_CPPv4N17wifi_capability_t18WIFI_CAPA_ID_HT_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t18WIFI_CAPA_ID_HT_ENE"></a> <a id="_CPPv2N17wifi_capability_t18WIFI_CAPA_ID_HT_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1a509db8830dd020d46467f5f901c61750"></a> enumerator WIFI\_CAPA\_ID\_HT\_EN
    :   Update Wi-Fi 11n support capability

    <a id="_CPPv4N17wifi_capability_t19WIFI_CAPA_ID_VHT_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t19WIFI_CAPA_ID_VHT_ENE"></a> <a id="_CPPv2N17wifi_capability_t19WIFI_CAPA_ID_VHT_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1a20a580b04bf57e6643dd7f6caced3b0e"></a> enumerator WIFI\_CAPA\_ID\_VHT\_EN
    :   Update Wi-Fi 11ac support capability

    <a id="_CPPv4N17wifi_capability_t18WIFI_CAPA_ID_HE_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t18WIFI_CAPA_ID_HE_ENE"></a> <a id="_CPPv2N17wifi_capability_t18WIFI_CAPA_ID_HE_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1a539c9e9af6fc31f9a0e6ff59ed692e60"></a> enumerator WIFI\_CAPA\_ID\_HE\_EN
    :   Update Wi-Fi 11ax support capability

    <a id="_CPPv4N17wifi_capability_t24WIFI_CAPA_ID_TX_AMPDU_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t24WIFI_CAPA_ID_TX_AMPDU_ENE"></a> <a id="_CPPv2N17wifi_capability_t24WIFI_CAPA_ID_TX_AMPDU_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1a90c2ebb0b0317f1f0e63ac6682234ac7"></a> enumerator WIFI\_CAPA\_ID\_TX\_AMPDU\_EN
    :   Update Wi-Fi TX AMPDU support capability

    <a id="_CPPv4N17wifi_capability_t24WIFI_CAPA_ID_RX_AMPDU_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t24WIFI_CAPA_ID_RX_AMPDU_ENE"></a> <a id="_CPPv2N17wifi_capability_t24WIFI_CAPA_ID_RX_AMPDU_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1a3700a20c2b98c1057cf037609259a165"></a> enumerator WIFI\_CAPA\_ID\_RX\_AMPDU\_EN
    :   Update Wi-Fi RX AMPDU support capability

    <a id="_CPPv4N17wifi_capability_t25WIFI_CAPA_ID_TX_AMPDU_NUME"></a>

    <a id="_CPPv3N17wifi_capability_t25WIFI_CAPA_ID_TX_AMPDU_NUME"></a> <a id="_CPPv2N17wifi_capability_t25WIFI_CAPA_ID_TX_AMPDU_NUME"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1af49634dbabbc838822f79ac41c2736ed"></a> enumerator WIFI\_CAPA\_ID\_TX\_AMPDU\_NUM
    :   Update Wi-Fi TX AMPDU maximum number

    <a id="_CPPv4N17wifi_capability_t25WIFI_CAPA_ID_RX_AMPDU_NUME"></a>

    <a id="_CPPv3N17wifi_capability_t25WIFI_CAPA_ID_RX_AMPDU_NUME"></a> <a id="_CPPv2N17wifi_capability_t25WIFI_CAPA_ID_RX_AMPDU_NUME"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1a94706d23864a16daa9da8fdcab9cb078"></a> enumerator WIFI\_CAPA\_ID\_RX\_AMPDU\_NUM
    :   Update Wi-Fi RX AMPDU maximum number

    <a id="_CPPv4N17wifi_capability_t20WIFI_CAPA_ID_VHT_MCSE"></a>

    <a id="_CPPv3N17wifi_capability_t20WIFI_CAPA_ID_VHT_MCSE"></a> <a id="_CPPv2N17wifi_capability_t20WIFI_CAPA_ID_VHT_MCSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1a540fa8c0fd197d5fab3e5cda5d459bea"></a> enumerator WIFI\_CAPA\_ID\_VHT\_MCS
    :   Update Wi-Fi VHT MCS

    <a id="_CPPv4N17wifi_capability_t19WIFI_CAPA_ID_HE_MCSE"></a>

    <a id="_CPPv3N17wifi_capability_t19WIFI_CAPA_ID_HE_MCSE"></a> <a id="_CPPv2N17wifi_capability_t19WIFI_CAPA_ID_HE_MCSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1aecfd132e3d6befab007b9e494fb023cf"></a> enumerator WIFI\_CAPA\_ID\_HE\_MCS
    :   Update Wi-Fi HE MCS

    <a id="_CPPv4N17wifi_capability_t19WIFI_CAPA_ID_B40_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t19WIFI_CAPA_ID_B40_ENE"></a> <a id="_CPPv2N17wifi_capability_t19WIFI_CAPA_ID_B40_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1a2d33c8884f8ec6ef08917bfecb58590e"></a> enumerator WIFI\_CAPA\_ID\_B40\_EN
    :   Update Wi-Fi 40M bandwidth support capability

    <a id="_CPPv4N17wifi_capability_t20WIFI_CAPA_ID_STBC_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t20WIFI_CAPA_ID_STBC_ENE"></a> <a id="_CPPv2N17wifi_capability_t20WIFI_CAPA_ID_STBC_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1ac5c351263a116445f5e06cf768049e89"></a> enumerator WIFI\_CAPA\_ID\_STBC\_EN
    :   Update Wi-Fi STBC support capability

    <a id="_CPPv4N17wifi_capability_t19WIFI_CAPA_ID_SGI_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t19WIFI_CAPA_ID_SGI_ENE"></a> <a id="_CPPv2N17wifi_capability_t19WIFI_CAPA_ID_SGI_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1afdfb433a65abbcabaadbc3bb6c57b6df"></a> enumerator WIFI\_CAPA\_ID\_SGI\_EN
    :   Update Wi-Fi Short GI support capability

    <a id="_CPPv4N17wifi_capability_t20WIFI_CAPA_ID_LDPC_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t20WIFI_CAPA_ID_LDPC_ENE"></a> <a id="_CPPv2N17wifi_capability_t20WIFI_CAPA_ID_LDPC_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1a9d7b5c52661ed0f3fd96e71d4751a531"></a> enumerator WIFI\_CAPA\_ID\_LDPC\_EN
    :   Update Wi-Fi LDPC support capability

    <a id="_CPPv4N17wifi_capability_t26WIFI_CAPA_ID_BEAMFORMEE_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t26WIFI_CAPA_ID_BEAMFORMEE_ENE"></a> <a id="_CPPv2N17wifi_capability_t26WIFI_CAPA_ID_BEAMFORMEE_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1aa976ce961e99b6667ff5d87ac8be793b"></a> enumerator WIFI\_CAPA\_ID\_BEAMFORMEE\_EN
    :   Update Wi-Fi Beamforming support capability

    <a id="_CPPv4N17wifi_capability_t24WIFI_CAPA_ID_11B_ONLY_ENE"></a>

    <a id="_CPPv3N17wifi_capability_t24WIFI_CAPA_ID_11B_ONLY_ENE"></a> <a id="_CPPv2N17wifi_capability_t24WIFI_CAPA_ID_11B_ONLY_ENE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1ab905eabd71d5435d08f5e869e8727969"></a> enumerator WIFI\_CAPA\_ID\_11B\_ONLY\_EN
    :   Update Wi-Fi 11b support capability

    <a id="_CPPv4N17wifi_capability_t16WIFI_CAPA_ID_MAXE"></a>

    <a id="_CPPv3N17wifi_capability_t16WIFI_CAPA_ID_MAXE"></a> <a id="_CPPv2N17wifi_capability_t16WIFI_CAPA_ID_MAXE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga1bc14fb46de73ab0c10a7aa6f93469b1aa67a283f3bf515e1bd9f664d47469876"></a> enumerator WIFI\_CAPA\_ID\_MAX

<a id="_CPPv426wifi_legacy_rate_support_t"></a>

<a id="_CPPv326wifi_legacy_rate_support_t"></a> <a id="_CPPv226wifi_legacy_rate_support_t"></a> <a id="group__bk__api__wifi__v2__typedef_1ga4dce7ced783b5d63174cae8167d1c22d"></a> enum wifi\_legacy\_rate\_support\_t
:   enum wifi legacy rate support \- Legacy rate support definitions

    *Values:*

    <a id="_CPPv4N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_1MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_1MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_1MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22da8b40c42452b919a8c86d1932aa468d8a"></a> enumerator WIFI\_LEGACY\_RATE\_1MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_2MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_2MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_2MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22dabcc8bce282a55feb0744d2a64d1e8d6c"></a> enumerator WIFI\_LEGACY\_RATE\_2MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t24WIFI_LEGACY_RATE_5_5MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t24WIFI_LEGACY_RATE_5_5MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t24WIFI_LEGACY_RATE_5_5MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22da4a33e42352b0799f030c65463df696c4"></a> enumerator WIFI\_LEGACY\_RATE\_5\_5MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_11MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_11MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_11MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22dac9dde0e36fcd183a1ce677ce19ea011f"></a> enumerator WIFI\_LEGACY\_RATE\_11MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_6MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_6MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_6MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22da484d7c60e0c1ffb4e0b692bbb87da3af"></a> enumerator WIFI\_LEGACY\_RATE\_6MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_9MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_9MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t22WIFI_LEGACY_RATE_9MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22da4c2bbe6850627f983b92966cd6412012"></a> enumerator WIFI\_LEGACY\_RATE\_9MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_12MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_12MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_12MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22dafd71942f993c8abacd451dcbca9e54be"></a> enumerator WIFI\_LEGACY\_RATE\_12MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_18MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_18MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_18MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22dabb8bfca0b2d31d261d171512215c64c7"></a> enumerator WIFI\_LEGACY\_RATE\_18MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_24MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_24MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_24MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22da79b93dfedfe4475a66e1da5182d5fdb0"></a> enumerator WIFI\_LEGACY\_RATE\_24MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_36MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_36MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_36MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22da771388c79b2edce60f679d179ec21576"></a> enumerator WIFI\_LEGACY\_RATE\_36MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_48MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_48MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_48MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22da279a630df6d6cff8312ffff3ac22bd91"></a> enumerator WIFI\_LEGACY\_RATE\_48MBPS

    <a id="_CPPv4N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_54MBPSE"></a>

    <a id="_CPPv3N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_54MBPSE"></a> <a id="_CPPv2N26wifi_legacy_rate_support_t23WIFI_LEGACY_RATE_54MBPSE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga4dce7ced783b5d63174cae8167d1c22da86ea55d0a6f71d120f5b9997d5ae88f3"></a> enumerator WIFI\_LEGACY\_RATE\_54MBPS

<a id="_CPPv422wifi_vht_mcs_support_t"></a>

<a id="_CPPv322wifi_vht_mcs_support_t"></a> <a id="_CPPv222wifi_vht_mcs_support_t"></a> <a id="group__bk__api__wifi__v2__typedef_1gadb26f2daae2c9087a555c24eddbecb0a"></a> enum wifi\_vht\_mcs\_support\_t
:   enum wifi\_vht\_mcs\_support\_t \- VHT MCS support definitions @WIFI\_VHT\_MCS\_SUPPORT\_0\_7: MCSes 0-7 are supported for the number of streams @WIFI\_VHT\_MCS\_SUPPORT\_0\_8: MCSes 0-8 are supported @WIFI\_VHT\_MCS\_SUPPORT\_0\_9: MCSes 0-9 are supported @WIFI\_VHT\_MCS\_NOT\_SUPPORTED: This number of streams isn’t supported

    *Values:*

    <a id="_CPPv4N22wifi_vht_mcs_support_t24WIFI_VHT_MCS_SUPPORT_0_7E"></a>

    <a id="_CPPv3N22wifi_vht_mcs_support_t24WIFI_VHT_MCS_SUPPORT_0_7E"></a> <a id="_CPPv2N22wifi_vht_mcs_support_t24WIFI_VHT_MCS_SUPPORT_0_7E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggadb26f2daae2c9087a555c24eddbecb0aa062b704f0871c4a2d56681c14f804929"></a> enumerator WIFI\_VHT\_MCS\_SUPPORT\_0\_7

    <a id="_CPPv4N22wifi_vht_mcs_support_t24WIFI_VHT_MCS_SUPPORT_0_8E"></a>

    <a id="_CPPv3N22wifi_vht_mcs_support_t24WIFI_VHT_MCS_SUPPORT_0_8E"></a> <a id="_CPPv2N22wifi_vht_mcs_support_t24WIFI_VHT_MCS_SUPPORT_0_8E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggadb26f2daae2c9087a555c24eddbecb0aa209c326411d901faed481cff5cd43f6a"></a> enumerator WIFI\_VHT\_MCS\_SUPPORT\_0\_8

    <a id="_CPPv4N22wifi_vht_mcs_support_t24WIFI_VHT_MCS_SUPPORT_0_9E"></a>

    <a id="_CPPv3N22wifi_vht_mcs_support_t24WIFI_VHT_MCS_SUPPORT_0_9E"></a> <a id="_CPPv2N22wifi_vht_mcs_support_t24WIFI_VHT_MCS_SUPPORT_0_9E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggadb26f2daae2c9087a555c24eddbecb0aaabebf87c28a705d8cb1de13b2a4976cb"></a> enumerator WIFI\_VHT\_MCS\_SUPPORT\_0\_9

    <a id="_CPPv4N22wifi_vht_mcs_support_t26WIFI_VHT_MCS_NOT_SUPPORTEDE"></a>

    <a id="_CPPv3N22wifi_vht_mcs_support_t26WIFI_VHT_MCS_NOT_SUPPORTEDE"></a> <a id="_CPPv2N22wifi_vht_mcs_support_t26WIFI_VHT_MCS_NOT_SUPPORTEDE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggadb26f2daae2c9087a555c24eddbecb0aa112ae860aeec764efa0f0f4ce1545c5c"></a> enumerator WIFI\_VHT\_MCS\_NOT\_SUPPORTED

<a id="_CPPv421wifi_he_mcs_support_t"></a>

<a id="_CPPv321wifi_he_mcs_support_t"></a> <a id="_CPPv221wifi_he_mcs_support_t"></a> <a id="group__bk__api__wifi__v2__typedef_1gae7464a9b074f1be5423f165133c9ad3a"></a> enum wifi\_he\_mcs\_support\_t
:   enum wifi\_he\_mcs\_support\_t \- HE MCS support definitions @WIFI\_HE\_MCS\_SUPPORT\_0\_7: MCSes 0-7 are supported for the number of streams @WIFI\_HE\_MCS\_SUPPORT\_0\_9: MCSes 0-9 are supported @WIFI\_HE\_MCS\_SUPPORT\_0\_11: MCSes 0-11 are supported @WIFI\_HE\_MCS\_NOT\_SUPPORTED: This number of streams isn’t supported

    *Values:*

    <a id="_CPPv4N21wifi_he_mcs_support_t23WIFI_HE_MCS_SUPPORT_0_7E"></a>

    <a id="_CPPv3N21wifi_he_mcs_support_t23WIFI_HE_MCS_SUPPORT_0_7E"></a> <a id="_CPPv2N21wifi_he_mcs_support_t23WIFI_HE_MCS_SUPPORT_0_7E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggae7464a9b074f1be5423f165133c9ad3aa4e0382b30014b923c2a8837784f5c424"></a> enumerator WIFI\_HE\_MCS\_SUPPORT\_0\_7

    <a id="_CPPv4N21wifi_he_mcs_support_t23WIFI_HE_MCS_SUPPORT_0_9E"></a>

    <a id="_CPPv3N21wifi_he_mcs_support_t23WIFI_HE_MCS_SUPPORT_0_9E"></a> <a id="_CPPv2N21wifi_he_mcs_support_t23WIFI_HE_MCS_SUPPORT_0_9E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggae7464a9b074f1be5423f165133c9ad3aae4ebc49186f71531199b487be61b467b"></a> enumerator WIFI\_HE\_MCS\_SUPPORT\_0\_9

    <a id="_CPPv4N21wifi_he_mcs_support_t24WIFI_HE_MCS_SUPPORT_0_11E"></a>

    <a id="_CPPv3N21wifi_he_mcs_support_t24WIFI_HE_MCS_SUPPORT_0_11E"></a> <a id="_CPPv2N21wifi_he_mcs_support_t24WIFI_HE_MCS_SUPPORT_0_11E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggae7464a9b074f1be5423f165133c9ad3aa2714520af3f93b9d74fd13b37cb043d1"></a> enumerator WIFI\_HE\_MCS\_SUPPORT\_0\_11

    <a id="_CPPv4N21wifi_he_mcs_support_t25WIFI_HE_MCS_NOT_SUPPORTEDE"></a>

    <a id="_CPPv3N21wifi_he_mcs_support_t25WIFI_HE_MCS_NOT_SUPPORTEDE"></a> <a id="_CPPv2N21wifi_he_mcs_support_t25WIFI_HE_MCS_NOT_SUPPORTEDE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggae7464a9b074f1be5423f165133c9ad3aa7c2eb8768bd4374f50fb00861ae4d953"></a> enumerator WIFI\_HE\_MCS\_NOT\_SUPPORTED

<a id="_CPPv420wifi_video_quality_t"></a>

<a id="_CPPv320wifi_video_quality_t"></a> <a id="_CPPv220wifi_video_quality_t"></a> <a id="group__bk__api__wifi__v2__typedef_1gaccc1dda3078a15f1e1acb8df8b8a4ca5"></a> enum wifi\_video\_quality\_t
:   enum wifi\_video\_quality\_t \- video quality definitions @WIFI\_VIDEO\_QUALITY\_FD: video quality choose Fluent definition(FD) @WIFI\_VIDEO\_QUALITY\_SD: video quality choose Standard definition(SD) @WIFI\_VIDEO\_QUALITY\_HD: video quality choose High definition(HD)

    *Values:*

    <a id="_CPPv4N20wifi_video_quality_t21WIFI_VIDEO_QUALITY_FDE"></a>

    <a id="_CPPv3N20wifi_video_quality_t21WIFI_VIDEO_QUALITY_FDE"></a> <a id="_CPPv2N20wifi_video_quality_t21WIFI_VIDEO_QUALITY_FDE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggaccc1dda3078a15f1e1acb8df8b8a4ca5a95fbd41afb553a19d285604033ca540a"></a> enumerator WIFI\_VIDEO\_QUALITY\_FD

    <a id="_CPPv4N20wifi_video_quality_t21WIFI_VIDEO_QUALITY_SDE"></a>

    <a id="_CPPv3N20wifi_video_quality_t21WIFI_VIDEO_QUALITY_SDE"></a> <a id="_CPPv2N20wifi_video_quality_t21WIFI_VIDEO_QUALITY_SDE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggaccc1dda3078a15f1e1acb8df8b8a4ca5a7556ce1d9e6acf402fea1b133a2b254b"></a> enumerator WIFI\_VIDEO\_QUALITY\_SD

    <a id="_CPPv4N20wifi_video_quality_t21WIFI_VIDEO_QUALITY_HDE"></a>

    <a id="_CPPv3N20wifi_video_quality_t21WIFI_VIDEO_QUALITY_HDE"></a> <a id="_CPPv2N20wifi_video_quality_t21WIFI_VIDEO_QUALITY_HDE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggaccc1dda3078a15f1e1acb8df8b8a4ca5a4d6e17d52b320707ed2054d4ab172eab"></a> enumerator WIFI\_VIDEO\_QUALITY\_HD

<a id="_CPPv413wifi_sta_vsie"></a>

<a id="_CPPv313wifi_sta_vsie"></a> <a id="_CPPv213wifi_sta_vsie"></a> <a id="group__bk__api__wifi__v2__typedef_1gaa1d5b5ba230d1c589aef12cc2f37b74a"></a> enum wifi\_sta\_vsie
:   *Values:*

    <a id="_CPPv4N13wifi_sta_vsie26WIFI_VENDOR_ELEM_ASSOC_REQE"></a>

    <a id="_CPPv3N13wifi_sta_vsie26WIFI_VENDOR_ELEM_ASSOC_REQE"></a> <a id="_CPPv2N13wifi_sta_vsie26WIFI_VENDOR_ELEM_ASSOC_REQE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggaa1d5b5ba230d1c589aef12cc2f37b74aa26a026a55299e3c1d38a55d19ccb4012"></a> enumerator WIFI\_VENDOR\_ELEM\_ASSOC\_REQ

    <a id="_CPPv4N13wifi_sta_vsie26WIFI_VENDOR_ELEM_PROBE_REQE"></a>

    <a id="_CPPv3N13wifi_sta_vsie26WIFI_VENDOR_ELEM_PROBE_REQE"></a> <a id="_CPPv2N13wifi_sta_vsie26WIFI_VENDOR_ELEM_PROBE_REQE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggaa1d5b5ba230d1c589aef12cc2f37b74aa49490b43ee20cbe063ea6684ff56ec92"></a> enumerator WIFI\_VENDOR\_ELEM\_PROBE\_REQ

    <a id="_CPPv4N13wifi_sta_vsie27NUM_WIFI_VENDOR_ELEM_FRAMESE"></a>

    <a id="_CPPv3N13wifi_sta_vsie27NUM_WIFI_VENDOR_ELEM_FRAMESE"></a> <a id="_CPPv2N13wifi_sta_vsie27NUM_WIFI_VENDOR_ELEM_FRAMESE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggaa1d5b5ba230d1c589aef12cc2f37b74aab5c7caa3432bfa14169d5e3d3e87a67a"></a> enumerator NUM\_WIFI\_VENDOR\_ELEM\_FRAMES

<a id="_CPPv416wifi_pkt_dbg_bit"></a>

<a id="_CPPv316wifi_pkt_dbg_bit"></a> <a id="_CPPv216wifi_pkt_dbg_bit"></a> <a id="group__bk__api__wifi__v2__typedef_1ga65ff512611910fcd645e8efab7316bb6"></a> enum wifi\_pkt\_dbg\_bit
:   *Values:*

    <a id="_CPPv4N16wifi_pkt_dbg_bit24WIFI_TX_DBG_LOG_DATA_PKTE"></a>

    <a id="_CPPv3N16wifi_pkt_dbg_bit24WIFI_TX_DBG_LOG_DATA_PKTE"></a> <a id="_CPPv2N16wifi_pkt_dbg_bit24WIFI_TX_DBG_LOG_DATA_PKTE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga65ff512611910fcd645e8efab7316bb6ae53b72fc7c8fce307fb61ef74f305bc5"></a> enumerator WIFI\_TX\_DBG\_LOG\_DATA\_PKT

    <a id="_CPPv4N16wifi_pkt_dbg_bit24WIFI_TX_DBG_LOG_MGMT_PKTE"></a>

    <a id="_CPPv3N16wifi_pkt_dbg_bit24WIFI_TX_DBG_LOG_MGMT_PKTE"></a> <a id="_CPPv2N16wifi_pkt_dbg_bit24WIFI_TX_DBG_LOG_MGMT_PKTE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga65ff512611910fcd645e8efab7316bb6a53d30b9ddc27679a2572b5dab7157b8a"></a> enumerator WIFI\_TX\_DBG\_LOG\_MGMT\_PKT

    <a id="_CPPv4N16wifi_pkt_dbg_bit24WIFI_TX_DBG_LOG_PUSH_PKTE"></a>

    <a id="_CPPv3N16wifi_pkt_dbg_bit24WIFI_TX_DBG_LOG_PUSH_PKTE"></a> <a id="_CPPv2N16wifi_pkt_dbg_bit24WIFI_TX_DBG_LOG_PUSH_PKTE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga65ff512611910fcd645e8efab7316bb6a0f8ecd6dbe5f9a6c6da8963fc379b5a7"></a> enumerator WIFI\_TX\_DBG\_LOG\_PUSH\_PKT

    <a id="_CPPv4N16wifi_pkt_dbg_bit24WIFI_RX_DBG_LOG_DATA_PKTE"></a>

    <a id="_CPPv3N16wifi_pkt_dbg_bit24WIFI_RX_DBG_LOG_DATA_PKTE"></a> <a id="_CPPv2N16wifi_pkt_dbg_bit24WIFI_RX_DBG_LOG_DATA_PKTE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga65ff512611910fcd645e8efab7316bb6ad3bb4a4b56b20dcee42ba29c751f1758"></a> enumerator WIFI\_RX\_DBG\_LOG\_DATA\_PKT

    <a id="_CPPv4N16wifi_pkt_dbg_bit24WIFI_RX_DBG_LOG_MGMT_PKTE"></a>

    <a id="_CPPv3N16wifi_pkt_dbg_bit24WIFI_RX_DBG_LOG_MGMT_PKTE"></a> <a id="_CPPv2N16wifi_pkt_dbg_bit24WIFI_RX_DBG_LOG_MGMT_PKTE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga65ff512611910fcd645e8efab7316bb6a61a4e02404d495fc72798c370d843e81"></a> enumerator WIFI\_RX\_DBG\_LOG\_MGMT\_PKT

<a id="_CPPv48sta_type"></a>

<a id="_CPPv38sta_type"></a> <a id="_CPPv28sta_type"></a> <a id="group__bk__api__wifi__v2__typedef_1gac7141fcda810097a30599e5b9f949197"></a> enum sta\_type
:   *Values:*

    <a id="_CPPv4N8sta_type9STA_TYPE1E"></a>

    <a id="_CPPv3N8sta_type9STA_TYPE1E"></a> <a id="_CPPv2N8sta_type9STA_TYPE1E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggac7141fcda810097a30599e5b9f949197a25eefb955c6774fd37d27c799f84df3e"></a> enumerator STA\_TYPE1

    <a id="_CPPv4N8sta_type9STA_TYPE2E"></a>

    <a id="_CPPv3N8sta_type9STA_TYPE2E"></a> <a id="_CPPv2N8sta_type9STA_TYPE2E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggac7141fcda810097a30599e5b9f949197a87b078c4dbc4077c7cdfb1753b24adf7"></a> enumerator STA\_TYPE2

    <a id="_CPPv4N8sta_type9STA_TYPE3E"></a>

    <a id="_CPPv3N8sta_type9STA_TYPE3E"></a> <a id="_CPPv2N8sta_type9STA_TYPE3E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggac7141fcda810097a30599e5b9f949197ac025e413837f3f2509c9cad6949254c7"></a> enumerator STA\_TYPE3

    <a id="_CPPv4N8sta_type9STA_TYPE4E"></a>

    <a id="_CPPv3N8sta_type9STA_TYPE4E"></a> <a id="_CPPv2N8sta_type9STA_TYPE4E"></a> <a id="group__bk__api__wifi__v2__typedef_1ggac7141fcda810097a30599e5b9f949197a4befbd118160defd3264f8d3c8c72026"></a> enumerator STA\_TYPE4

    <a id="_CPPv4N8sta_type12MAX_STA_TYPEE"></a>

    <a id="_CPPv3N8sta_type12MAX_STA_TYPEE"></a> <a id="_CPPv2N8sta_type12MAX_STA_TYPEE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggac7141fcda810097a30599e5b9f949197a410c3e48fc755dae2a47f6b0cac9e692"></a> enumerator MAX\_STA\_TYPE

<a id="_CPPv4Ut2_12"></a>

<a id="_CPPv3Ut2_12"></a> <a id="group__bk__api__wifi__v2__typedef_1gac36f475ca5b446f4fde4c9b90bec77c8"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt2_1212SCAN_TYPE_CCE"></a>

    <a id="_CPPv3NUt2_1212SCAN_TYPE_CCE"></a> <a id="group__bk__api__wifi__v2__typedef_1ggac36f475ca5b446f4fde4c9b90bec77c8a15a318100b5dcc8f636a3ea429a6b02a"></a> enumerator SCAN\_TYPE\_CC

<a id="_CPPv4Ut2_13"></a>

<a id="_CPPv3Ut2_13"></a> <a id="group__bk__api__wifi__v2__typedef_1ga05589fbab0657f08285ebdfe93f5ec9e"></a> enum \[anonymous\]
:   BC/MC Filter.

    *Values:*

    <a id="_CPPv4NUt2_1315WIFI_BCMC_CLOSEE"></a>

    <a id="_CPPv3NUt2_1315WIFI_BCMC_CLOSEE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga05589fbab0657f08285ebdfe93f5ec9eac4d8aa4a655058d6dec1720e7e422af1"></a> enumerator WIFI\_BCMC\_CLOSE

    <a id="_CPPv4NUt2_1310WIFI_MC_ONE"></a>

    <a id="_CPPv3NUt2_1310WIFI_MC_ONE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga05589fbab0657f08285ebdfe93f5ec9ea22623105bf43ab4a45b671a7a3dd2f86"></a> enumerator WIFI\_MC\_ON

    <a id="_CPPv4NUt2_1310WIFI_BC_ONE"></a>

    <a id="_CPPv3NUt2_1310WIFI_BC_ONE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga05589fbab0657f08285ebdfe93f5ec9ea0be6be5152922defb58ee1809a8bb6ea"></a> enumerator WIFI\_BC\_ON

    <a id="_CPPv4NUt2_1313WIFI_BC_MC_ONE"></a>

    <a id="_CPPv3NUt2_1313WIFI_BC_MC_ONE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga05589fbab0657f08285ebdfe93f5ec9eababf41aca67fe457ce1014f472eb3bd3"></a> enumerator WIFI\_BC\_MC\_ON

<a id="_CPPv413wifi_standard"></a>

<a id="_CPPv313wifi_standard"></a> <a id="_CPPv213wifi_standard"></a> <a id="group__bk__api__wifi__v2__typedef_1ga3dc00bec8f6993cbc09e35742ec7c266"></a> enum wifi\_standard
:   IEEE 802.11 Standards.

    *Values:*

    <a id="_CPPv4N13wifi_standard18WIFI_STANDARD_NONEE"></a>

    <a id="_CPPv3N13wifi_standard18WIFI_STANDARD_NONEE"></a> <a id="_CPPv2N13wifi_standard18WIFI_STANDARD_NONEE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga3dc00bec8f6993cbc09e35742ec7c266a2bbed9de7eb1f9a7a009f7181bd4fa49"></a> enumerator WIFI\_STANDARD\_NONE

    <a id="_CPPv4N13wifi_standard17WIFI_STANDARD_11AE"></a>

    <a id="_CPPv3N13wifi_standard17WIFI_STANDARD_11AE"></a> <a id="_CPPv2N13wifi_standard17WIFI_STANDARD_11AE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga3dc00bec8f6993cbc09e35742ec7c266abf1ce4e3f6248bd1456706e1bd893956"></a> enumerator WIFI\_STANDARD\_11A

    <a id="_CPPv4N13wifi_standard17WIFI_STANDARD_11BE"></a>

    <a id="_CPPv3N13wifi_standard17WIFI_STANDARD_11BE"></a> <a id="_CPPv2N13wifi_standard17WIFI_STANDARD_11BE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga3dc00bec8f6993cbc09e35742ec7c266a751c2b61a411525c732b7572a16c3a4f"></a> enumerator WIFI\_STANDARD\_11B

    <a id="_CPPv4N13wifi_standard17WIFI_STANDARD_11GE"></a>

    <a id="_CPPv3N13wifi_standard17WIFI_STANDARD_11GE"></a> <a id="_CPPv2N13wifi_standard17WIFI_STANDARD_11GE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga3dc00bec8f6993cbc09e35742ec7c266a2c1da2e83752f9e1d6cc2cff995781a4"></a> enumerator WIFI\_STANDARD\_11G

    <a id="_CPPv4N13wifi_standard17WIFI_STANDARD_11NE"></a>

    <a id="_CPPv3N13wifi_standard17WIFI_STANDARD_11NE"></a> <a id="_CPPv2N13wifi_standard17WIFI_STANDARD_11NE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga3dc00bec8f6993cbc09e35742ec7c266ac831a54d496253ded3ca6aec88883551"></a> enumerator WIFI\_STANDARD\_11N

    <a id="_CPPv4N13wifi_standard18WIFI_STANDARD_11ACE"></a>

    <a id="_CPPv3N13wifi_standard18WIFI_STANDARD_11ACE"></a> <a id="_CPPv2N13wifi_standard18WIFI_STANDARD_11ACE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga3dc00bec8f6993cbc09e35742ec7c266a462cfe2b1157b814a281a31405b6d82e"></a> enumerator WIFI\_STANDARD\_11AC

    <a id="_CPPv4N13wifi_standard18WIFI_STANDARD_11AXE"></a>

    <a id="_CPPv3N13wifi_standard18WIFI_STANDARD_11AXE"></a> <a id="_CPPv2N13wifi_standard18WIFI_STANDARD_11AXE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga3dc00bec8f6993cbc09e35742ec7c266ad1afd541d645bc898024720f1fdcd17a"></a> enumerator WIFI\_STANDARD\_11AX

    <a id="_CPPv4N13wifi_standard17WIFI_STANDARD_MAXE"></a>

    <a id="_CPPv3N13wifi_standard17WIFI_STANDARD_MAXE"></a> <a id="_CPPv2N13wifi_standard17WIFI_STANDARD_MAXE"></a> <a id="group__bk__api__wifi__v2__typedef_1gga3dc00bec8f6993cbc09e35742ec7c266a82f02bc94488309e7a4fa588662d2b63"></a> enumerator WIFI\_STANDARD\_MAX

<a id="_CPPv417bk_bridge_state_t"></a>

<a id="_CPPv317bk_bridge_state_t"></a> <a id="_CPPv217bk_bridge_state_t"></a> <a id="group__bk__api__wifi__v2_1ga98ddd9264ec668932c0b92d85b53887c"></a> enum bk\_bridge\_state\_t
:   *Values:*

    <a id="_CPPv4N17bk_bridge_state_t21BRIDGE_STATE_DISABLEDE"></a>

    <a id="_CPPv3N17bk_bridge_state_t21BRIDGE_STATE_DISABLEDE"></a> <a id="_CPPv2N17bk_bridge_state_t21BRIDGE_STATE_DISABLEDE"></a> <a id="group__bk__api__wifi__v2_1gga98ddd9264ec668932c0b92d85b53887ca895f589ef877cb5b7d2fcee9a660e0d9"></a> enumerator BRIDGE\_STATE\_DISABLED

    <a id="_CPPv4N17bk_bridge_state_t22BRIDGE_STATE_DISABLINGE"></a>

    <a id="_CPPv3N17bk_bridge_state_t22BRIDGE_STATE_DISABLINGE"></a> <a id="_CPPv2N17bk_bridge_state_t22BRIDGE_STATE_DISABLINGE"></a> <a id="group__bk__api__wifi__v2_1gga98ddd9264ec668932c0b92d85b53887cae1c276dcc03cce71f177b3d584f33f81"></a> enumerator BRIDGE\_STATE\_DISABLING

    <a id="_CPPv4N17bk_bridge_state_t21BRIDGE_STATE_ENABLINGE"></a>

    <a id="_CPPv3N17bk_bridge_state_t21BRIDGE_STATE_ENABLINGE"></a> <a id="_CPPv2N17bk_bridge_state_t21BRIDGE_STATE_ENABLINGE"></a> <a id="group__bk__api__wifi__v2_1gga98ddd9264ec668932c0b92d85b53887cab2d3fa287b30725e58d16d9acb682fc6"></a> enumerator BRIDGE\_STATE\_ENABLING

    <a id="_CPPv4N17bk_bridge_state_t20BRIDGE_STATE_ENABLEDE"></a>

    <a id="_CPPv3N17bk_bridge_state_t20BRIDGE_STATE_ENABLEDE"></a> <a id="_CPPv2N17bk_bridge_state_t20BRIDGE_STATE_ENABLEDE"></a> <a id="group__bk__api__wifi__v2_1gga98ddd9264ec668932c0b92d85b53887ca50168bd512dc5ab2db3edc91a9bbaf07"></a> enumerator BRIDGE\_STATE\_ENABLED
