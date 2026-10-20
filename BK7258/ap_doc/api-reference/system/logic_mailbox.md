---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/system/logic_mailbox.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="multi-core-mailbox-api"></a>

# MULTI-CORE MAILBOX API

> - mailbox逻辑通道用于多核间信息交互

<a id="header-file"></a>

## Header File

- [mailbox\_channel.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/mailbox_channel.h)

<a id="functions"></a>

## Functions

<a id="_CPPv412mb_chnl_initv"></a>

<a id="_CPPv312mb_chnl_initv"></a> <a id="_CPPv212mb_chnl_initv"></a> <a id="mb_chnl_init__void"></a> <a id="mailbox__channel_8h_1af08f90c506bf90594c9a1915b5f73af5"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") mb\_chnl\_init(void)

<a id="_CPPv412mb_chnl_open2u8Pv"></a>

<a id="_CPPv312mb_chnl_open2u8Pv"></a> <a id="_CPPv212mb_chnl_open2u8Pv"></a> <a id="mb_chnl_open__u8.voidP"></a> <a id="mailbox__channel_8h_1a02c2f86e516c25d2cd139a9695b9b610"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") mb\_chnl\_open(u8 log\_chnl, void \*callback\_param)

<a id="_CPPv413mb_chnl_close2u8"></a>

<a id="_CPPv313mb_chnl_close2u8"></a> <a id="_CPPv213mb_chnl_close2u8"></a> <a id="mb_chnl_close__u8"></a> <a id="mailbox__channel_8h_1a75fadae871d05fde04f5c43179736453"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") mb\_chnl\_close(u8 log\_chnl)

<a id="_CPPv412mb_chnl_read2u8P13mb_chnl_cmd_t"></a>

<a id="_CPPv312mb_chnl_read2u8P13mb_chnl_cmd_t"></a> <a id="_CPPv212mb_chnl_read2u8P13mb_chnl_cmd_t"></a> <a id="mb_chnl_read__u8.mb_chnl_cmd_tP"></a> <a id="mailbox__channel_8h_1a0533191059e9ca2afc7c6683b76b02e7"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") mb\_chnl\_read(u8 log\_chnl, [mb\_chnl\_cmd\_t](#_CPPv413mb_chnl_cmd_t "mb_chnl_cmd_t") \*read\_buf)

<a id="_CPPv413mb_chnl_write2u8P13mb_chnl_cmd_t"></a>

<a id="_CPPv313mb_chnl_write2u8P13mb_chnl_cmd_t"></a> <a id="_CPPv213mb_chnl_write2u8P13mb_chnl_cmd_t"></a> <a id="mb_chnl_write__u8.mb_chnl_cmd_tP"></a> <a id="mailbox__channel_8h_1a4fc381430dcd1c09d38587ad952fa7f3"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") mb\_chnl\_write(u8 log\_chnl, [mb\_chnl\_cmd\_t](#_CPPv413mb_chnl_cmd_t "mb_chnl_cmd_t") \*cmd\_buf)

<a id="_CPPv412mb_chnl_ctrl2u82u8Pv"></a>

<a id="_CPPv312mb_chnl_ctrl2u82u8Pv"></a> <a id="_CPPv212mb_chnl_ctrl2u82u8Pv"></a> <a id="mb_chnl_ctrl__u8.u8.voidP"></a> <a id="mailbox__channel_8h_1ae75fcbf3be8a272e2bb8d7f3825f9fa6"></a> [bk\_err\_t](os.md#_CPPv48bk_err_t "bk_err_t") mb\_chnl\_ctrl(u8 log\_chnl, u8 cmd, void \*param)

<a id="unions"></a>

## Unions

<a id="_CPPv413mb_chnl_hdr_t"></a>

<a id="_CPPv313mb_chnl_hdr_t"></a> <a id="_CPPv213mb_chnl_hdr_t"></a> <a id="unionmb__chnl__hdr__t"></a> union mb\_chnl\_hdr\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13mb_chnl_hdr_t3cmdE"></a>

    <a id="_CPPv3N13mb_chnl_hdr_t3cmdE"></a> <a id="_CPPv2N13mb_chnl_hdr_t3cmdE"></a> <a id="mb_chnl_hdr_t::cmd__u32"></a> <a id="unionmb__chnl__hdr__t_1a9cf8162abfdf285053f2ebe937ce7d72"></a> u32 cmd

    <a id="_CPPv4N13mb_chnl_hdr_t5stateE"></a>

    <a id="_CPPv3N13mb_chnl_hdr_t5stateE"></a> <a id="_CPPv2N13mb_chnl_hdr_t5stateE"></a> <a id="mb_chnl_hdr_t::state__u32"></a> <a id="unionmb__chnl__hdr__t_1a3572e39136ec977f1c3e4d7922f5c0a9"></a> u32 state

    <a id="_CPPv4N13mb_chnl_hdr_t8ReservedE"></a>

    <a id="_CPPv3N13mb_chnl_hdr_t8ReservedE"></a> <a id="_CPPv2N13mb_chnl_hdr_t8ReservedE"></a> <a id="mb_chnl_hdr_t::Reserved__u32"></a> <a id="unionmb__chnl__hdr__t_1a3790087138e8732110d55bc2dcaf55fe"></a> u32 Reserved

    <a id="_CPPv4N13mb_chnl_hdr_tUt2_32E"></a>

    <a id="_CPPv3N13mb_chnl_hdr_tUt2_32E"></a> <a id="unionmb__chnl__hdr__t_1aeae84ca2ea498910a25369b359a72e9e"></a> struct [mb\_chnl\_hdr\_t](#_CPPv413mb_chnl_hdr_t "mb_chnl_hdr_t")::\[anonymous\] \[anonymous\]

    <a id="_CPPv4N13mb_chnl_hdr_t4dataE"></a>

    <a id="_CPPv3N13mb_chnl_hdr_t4dataE"></a> <a id="_CPPv2N13mb_chnl_hdr_t4dataE"></a> <a id="mb_chnl_hdr_t::data__u32"></a> <a id="unionmb__chnl__hdr__t_1af60e22114b656a4b8fcec5d73fc281ee"></a> u32 data

<a id="structures"></a>

## Structures

<a id="_CPPv413mb_chnl_cmd_t"></a>

<a id="_CPPv313mb_chnl_cmd_t"></a> <a id="_CPPv213mb_chnl_cmd_t"></a> <a id="mb_chnl_cmd_t"></a> <a id="structmb__chnl__cmd__t"></a> struct mb\_chnl\_cmd\_t

<a id="_CPPv413mb_chnl_ack_t"></a>

<a id="_CPPv313mb_chnl_ack_t"></a> <a id="_CPPv213mb_chnl_ack_t"></a> <a id="mb_chnl_ack_t"></a> <a id="structmb__chnl__ack__t"></a> struct mb\_chnl\_ack\_t

<a id="macros"></a>

## Macros

<a id="c.SYSTEM_CPU_NUM"></a>

<a id="mailbox__channel_8h_1a4ac32cd5c23af0c7319637b7df5cb7f7"></a> SYSTEM\_CPU\_NUM

<a id="c.DST_CPU_ID_MASK"></a>

<a id="mailbox__channel_8h_1ace9dbda3bc73639fee496ab022f9c149"></a> DST\_CPU\_ID\_MASK

<a id="c.DST_CPU_ID_POS"></a>

<a id="mailbox__channel_8h_1a46716c6e9a4c68b2268e36a1dd0abe40"></a> DST\_CPU\_ID\_POS

<a id="c.SRC_CPU_ID_MASK"></a>

<a id="mailbox__channel_8h_1a84710036dbc48a2d2c458c4105eda61e"></a> SRC\_CPU\_ID\_MASK

<a id="c.SRC_CPU_ID_POS"></a>

<a id="mailbox__channel_8h_1aa6f28c7d3bd940924bad76f3f49bc7f9"></a> SRC\_CPU\_ID\_POS

<a id="c.LOG_CHNL_ID_MASK"></a>

<a id="mailbox__channel_8h_1a613ab2f153f53cb8a2bd301af78daf84"></a> LOG\_CHNL\_ID\_MASK

<a id="c.GET_SRC_CPU_ID"></a>

<a id="mailbox__channel_8h_1a4e95d66cd9212595218e01f50931082b"></a> GET\_SRC\_CPU\_ID(log\_chnl)

<a id="c.GET_DST_CPU_ID"></a>

<a id="mailbox__channel_8h_1a20487cb761ef3b1893a01aee6720e95f"></a> GET\_DST\_CPU\_ID(log\_chnl)

<a id="c.CPX_LOG_CHNL_START"></a>

<a id="mailbox__channel_8h_1a691896553c1464be70a72556170349e2"></a> CPX\_LOG\_CHNL\_START(src\_cpu, dst\_cpu)

<a id="c.GET_LOG_CHNL_ID"></a>

<a id="mailbox__channel_8h_1ab798fdf923afbc06cab2c2259da10d39"></a> GET\_LOG\_CHNL\_ID(log\_chnl)

<a id="c.SELF_CPU"></a>

<a id="mailbox__channel_8h_1a9fd0dab20b8838f44933c422911a3157"></a> SELF\_CPU

<a id="c.MB_CHNL_MIPC"></a>

<a id="mailbox__channel_8h_1a8f11889517b636960b10b6c35b473830"></a> MB\_CHNL\_MIPC

<a id="c.SRC_CPU"></a>

<a id="mailbox__channel_8h_1a40d263724fe044c39dbb4137e991f83a"></a> SRC\_CPU

<a id="c.CHNL_STATE_MASK"></a>

<a id="mailbox__channel_8h_1ae0e6f8c06a24ddd4967649ac7e860ceb"></a> CHNL\_STATE\_MASK

<a id="c.CHNL_STATE_COM_FAIL"></a>

<a id="mailbox__channel_8h_1a4e7a2e241af2e10ef5db329b77b5961b"></a> CHNL\_STATE\_COM\_FAIL

<a id="type-definitions"></a>

## Type Definitions

<a id="_CPPv418chnl_tx_cmpl_isr_t"></a>

<a id="_CPPv318chnl_tx_cmpl_isr_t"></a> <a id="_CPPv218chnl_tx_cmpl_isr_t"></a> <a id="chnl_tx_cmpl_isr_t"></a> <a id="mailbox__channel_8h_1abedcd8c2305146dc98c1c2f6c3cb96d9"></a> typedef void (\*chnl\_tx\_cmpl\_isr\_t)(void \*param, [mb\_chnl\_ack\_t](#_CPPv413mb_chnl_ack_t "mb_chnl_ack_t") \*ack\_buf)

<a id="_CPPv413chnl_tx_isr_t"></a>

<a id="_CPPv313chnl_tx_isr_t"></a> <a id="_CPPv213chnl_tx_isr_t"></a> <a id="chnl_tx_isr_t"></a> <a id="mailbox__channel_8h_1a77e0c951d0c0ab125f7290908b4f4411"></a> typedef void (\*chnl\_tx\_isr\_t)(void \*param)

<a id="_CPPv413chnl_rx_isr_t"></a>

<a id="_CPPv313chnl_rx_isr_t"></a> <a id="_CPPv213chnl_rx_isr_t"></a> <a id="chnl_rx_isr_t"></a> <a id="mailbox__channel_8h_1a07a06f20dcc209a03f3bd8d1adee4258"></a> typedef void (\*chnl\_rx\_isr\_t)(void \*param, [mb\_chnl\_cmd\_t](#_CPPv413mb_chnl_cmd_t "mb_chnl_cmd_t") \*cmd\_buf)

<a id="enumerations"></a>

## Enumerations

<a id="_CPPv4Ut2_26"></a>

<a id="_CPPv3Ut2_26"></a> <a id="mailbox__channel_8h_1a7ff5f2dff38e7639981794c43dc9167b"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt2_2621CP1_MB_LOG_CHNL_STARTE"></a>

    <a id="_CPPv3NUt2_2621CP1_MB_LOG_CHNL_STARTE"></a> <a id="mailbox__channel_8h_1a7ff5f2dff38e7639981794c43dc9167ba1f3fe7e9d138841aa31fcc7f8af62eba"></a> enumerator CP1\_MB\_LOG\_CHNL\_START

    <a id="_CPPv4NUt2_2619CP1_MB_LOG_CHNL_ENDE"></a>

    <a id="_CPPv3NUt2_2619CP1_MB_LOG_CHNL_ENDE"></a> <a id="mailbox__channel_8h_1a7ff5f2dff38e7639981794c43dc9167ba29652cdc02cf1f454b177b3e21b7949c"></a> enumerator CP1\_MB\_LOG\_CHNL\_END

    <a id="_CPPv4NUt2_2619CP1_MB_LOG_CHNL_MAXE"></a>

    <a id="_CPPv3NUt2_2619CP1_MB_LOG_CHNL_MAXE"></a> <a id="mailbox__channel_8h_1a7ff5f2dff38e7639981794c43dc9167ba64c2d548b15d31456e796fe085f0fa2a"></a> enumerator CP1\_MB\_LOG\_CHNL\_MAX

<a id="_CPPv4Ut2_27"></a>

<a id="_CPPv3Ut2_27"></a> <a id="mailbox__channel_8h_1aabfcbcb5ac86a1edac4035264bc7d2b8"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt2_2721CP2_MB_LOG_CHNL_STARTE"></a>

    <a id="_CPPv3NUt2_2721CP2_MB_LOG_CHNL_STARTE"></a> <a id="mailbox__channel_8h_1aabfcbcb5ac86a1edac4035264bc7d2b8ae60514f1589a08036cee9558080e5a38"></a> enumerator CP2\_MB\_LOG\_CHNL\_START

    <a id="_CPPv4NUt2_2719CP2_MB_LOG_CHNL_ENDE"></a>

    <a id="_CPPv3NUt2_2719CP2_MB_LOG_CHNL_ENDE"></a> <a id="mailbox__channel_8h_1aabfcbcb5ac86a1edac4035264bc7d2b8a201b8eadac51e5addbe5fd216a2a8891"></a> enumerator CP2\_MB\_LOG\_CHNL\_END

    <a id="_CPPv4NUt2_2719CP2_MB_LOG_CHNL_MAXE"></a>

    <a id="_CPPv3NUt2_2719CP2_MB_LOG_CHNL_MAXE"></a> <a id="mailbox__channel_8h_1aabfcbcb5ac86a1edac4035264bc7d2b8acf2c0691b60864f21c625c22428ab5bf"></a> enumerator CP2\_MB\_LOG\_CHNL\_MAX

<a id="_CPPv4Ut2_28"></a>

<a id="_CPPv3Ut2_28"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181f"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt2_2821CP0_MB_LOG_CHNL_STARTE"></a>

    <a id="_CPPv3NUt2_2821CP0_MB_LOG_CHNL_STARTE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fae8464d6c8279a605cf44565df0d36e15"></a> enumerator CP0\_MB\_LOG\_CHNL\_START

    <a id="_CPPv4NUt2_2815MB_CHNL_HW_CTRLE"></a>

    <a id="_CPPv3NUt2_2815MB_CHNL_HW_CTRLE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa812f03d3b835e31c4f85a4920c77267f"></a> enumerator MB\_CHNL\_HW\_CTRL

    <a id="_CPPv4NUt2_2815CP0_MB_CHNL_IPCE"></a>

    <a id="_CPPv3NUt2_2815CP0_MB_CHNL_IPCE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fac9c3dc2679fbf3d5c57ecf1169e538b1"></a> enumerator CP0\_MB\_CHNL\_IPC

    <a id="_CPPv4NUt2_2811MB_CHNL_PWCE"></a>

    <a id="_CPPv3NUt2_2811MB_CHNL_PWCE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fadc17383cce953ce09820860dfcd5b016"></a> enumerator MB\_CHNL\_PWC

    <a id="_CPPv4NUt2_2814MB_CHNL_BT_CMDE"></a>

    <a id="_CPPv3NUt2_2814MB_CHNL_BT_CMDE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa9c3c502bb95866ec587f7bcd9c86e4d9"></a> enumerator MB\_CHNL\_BT\_CMD

    <a id="_CPPv4NUt2_2816MB_CHNL_WIFI_CMDE"></a>

    <a id="_CPPv3NUt2_2816MB_CHNL_WIFI_CMDE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa5f6a3ab4ef31c264c8e748218bbdf114"></a> enumerator MB\_CHNL\_WIFI\_CMD

    <a id="_CPPv4NUt2_2817MB_CHNL_WIFI_DATAE"></a>

    <a id="_CPPv3NUt2_2817MB_CHNL_WIFI_DATAE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa3d968a2594e047b5b835628798cd4ddf"></a> enumerator MB\_CHNL\_WIFI\_DATA

    <a id="_CPPv4NUt2_2811MB_CHNL_USBE"></a>

    <a id="_CPPv3NUt2_2811MB_CHNL_USBE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa7ca5d2425a49c60a974407b00ed3f186"></a> enumerator MB\_CHNL\_USB

    <a id="_CPPv4NUt2_2817MB_CHNL_MIPC_SYNCE"></a>

    <a id="_CPPv3NUt2_2817MB_CHNL_MIPC_SYNCE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181faad17ef6c44b91977ff8b083db32afdce"></a> enumerator MB\_CHNL\_MIPC\_SYNC

    <a id="_CPPv4NUt2_2810MB_CHNL_ATE"></a>

    <a id="_CPPv3NUt2_2810MB_CHNL_ATE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fabf5c8403f467cd4aadba04c6b7390bbb"></a> enumerator MB\_CHNL\_AT

    <a id="_CPPv4NUt2_2813MB_CHNL_UART0E"></a>

    <a id="_CPPv3NUt2_2813MB_CHNL_UART0E"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa6238882455af66d3cf5e3eb5ddd71783"></a> enumerator MB\_CHNL\_UART0

    <a id="_CPPv4NUt2_2813MB_CHNL_UART1E"></a>

    <a id="_CPPv3NUt2_2813MB_CHNL_UART1E"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa171eedef949bac2b94062b004dc46187"></a> enumerator MB\_CHNL\_UART1

    <a id="_CPPv4NUt2_2813MB_CHNL_FLASHE"></a>

    <a id="_CPPv3NUt2_2813MB_CHNL_FLASHE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa00f69f3bea9d74746e8629a9e8b8e900"></a> enumerator MB\_CHNL\_FLASH

    <a id="_CPPv4NUt2_2814MB_CHNL_SARADCE"></a>

    <a id="_CPPv3NUt2_2814MB_CHNL_SARADCE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa32ce438f5defa1b565e8b857d3f04063"></a> enumerator MB\_CHNL\_SARADC

    <a id="_CPPv4NUt2_2811MB_CHNL_PHYE"></a>

    <a id="_CPPv3NUt2_2811MB_CHNL_PHYE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa71b06e7492ecb8d3b00b58ec4643308e"></a> enumerator MB\_CHNL\_PHY

    <a id="_CPPv4NUt2_2811MB_CHNL_LOGE"></a>

    <a id="_CPPv3NUt2_2811MB_CHNL_LOGE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa7e2d199d918137106c0d18e966971501"></a> enumerator MB\_CHNL\_LOG

    <a id="_CPPv4NUt2_2819CP0_MB_LOG_CHNL_ENDE"></a>

    <a id="_CPPv3NUt2_2819CP0_MB_LOG_CHNL_ENDE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181fa5100b555e612cf28b62d095f4f29bb5a"></a> enumerator CP0\_MB\_LOG\_CHNL\_END

    <a id="_CPPv4NUt2_2819CP0_MB_LOG_CHNL_MAXE"></a>

    <a id="_CPPv3NUt2_2819CP0_MB_LOG_CHNL_MAXE"></a> <a id="mailbox__channel_8h_1a5d76b81b0ad4c19007a781d4edb8181faf5f285dd978df67210431a40797d0e57"></a> enumerator CP0\_MB\_LOG\_CHNL\_MAX

<a id="_CPPv4Ut2_29"></a>

<a id="_CPPv3Ut2_29"></a> <a id="mailbox__channel_8h_1aac34dfe6c6b73b43a4656c9dce041034"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt2_2917ACK_STATE_PENDINGE"></a>

    <a id="_CPPv3NUt2_2917ACK_STATE_PENDINGE"></a> <a id="mailbox__channel_8h_1aac34dfe6c6b73b43a4656c9dce041034a19a848d8730ac409b0ac60539cd6a8c5"></a> enumerator ACK\_STATE\_PENDING

    <a id="_CPPv4NUt2_2918ACK_STATE_COMPLETEE"></a>

    <a id="_CPPv3NUt2_2918ACK_STATE_COMPLETEE"></a> <a id="mailbox__channel_8h_1aac34dfe6c6b73b43a4656c9dce041034aaff9b9f5425ba9fcc15fcf13dc9e722e"></a> enumerator ACK\_STATE\_COMPLETE

    <a id="_CPPv4NUt2_2914ACK_STATE_FAILE"></a>

    <a id="_CPPv3NUt2_2914ACK_STATE_FAILE"></a> <a id="mailbox__channel_8h_1aac34dfe6c6b73b43a4656c9dce041034a49eaad5fcd74b5eee68b24286952feab"></a> enumerator ACK\_STATE\_FAIL

<a id="_CPPv4Ut2_30"></a>

<a id="_CPPv3Ut2_30"></a> <a id="mailbox__channel_8h_1a0ed680fdb405e7195d9f14032851eebb"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt2_3018MB_CHNL_GET_STATUSE"></a>

    <a id="_CPPv3NUt2_3018MB_CHNL_GET_STATUSE"></a> <a id="mailbox__channel_8h_1a0ed680fdb405e7195d9f14032851eebba6c055355f86c53d23184e5e5a59af8fc"></a> enumerator MB\_CHNL\_GET\_STATUS

    <a id="_CPPv4NUt2_3018MB_CHNL_SET_RX_ISRE"></a>

    <a id="_CPPv3NUt2_3018MB_CHNL_SET_RX_ISRE"></a> <a id="mailbox__channel_8h_1a0ed680fdb405e7195d9f14032851eebba7fcd12457c6858295341a0e62aaf12ea"></a> enumerator MB\_CHNL\_SET\_RX\_ISR

    <a id="_CPPv4NUt2_3018MB_CHNL_SET_TX_ISRE"></a>

    <a id="_CPPv3NUt2_3018MB_CHNL_SET_TX_ISRE"></a> <a id="mailbox__channel_8h_1a0ed680fdb405e7195d9f14032851eebba20a9b622dca3d0305df4010533a06801"></a> enumerator MB\_CHNL\_SET\_TX\_ISR

    <a id="_CPPv4NUt2_3023MB_CHNL_SET_TX_CMPL_ISRE"></a>

    <a id="_CPPv3NUt2_3023MB_CHNL_SET_TX_CMPL_ISRE"></a> <a id="mailbox__channel_8h_1a0ed680fdb405e7195d9f14032851eebba407262ff420a88ae35d8dc46dd21a433"></a> enumerator MB\_CHNL\_SET\_TX\_CMPL\_ISR

    <a id="_CPPv4NUt2_3018MB_CHNL_WRITE_SYNCE"></a>

    <a id="_CPPv3NUt2_3018MB_CHNL_WRITE_SYNCE"></a> <a id="mailbox__channel_8h_1a0ed680fdb405e7195d9f14032851eebba3764fe87b0c2d0c432c130131668defb"></a> enumerator MB\_CHNL\_WRITE\_SYNC

    <a id="_CPPv4NUt2_3016MB_CHNL_TX_RESETE"></a>

    <a id="_CPPv3NUt2_3016MB_CHNL_TX_RESETE"></a> <a id="mailbox__channel_8h_1a0ed680fdb405e7195d9f14032851eebba7f1d67f0b667bd0752811029084460f6"></a> enumerator MB\_CHNL\_TX\_RESET
