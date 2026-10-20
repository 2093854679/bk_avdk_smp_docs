---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/system/logic_mailbox.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="mailbox-api"></a>

# 多核 Mailbox API

BK7259 CP 侧通过逻辑通道与 AP（`MAILBOX_CPU2`、`MAILBOX_CPU3`）及 CP 内另一核通信。
应用使用 `include/driver/mailbox_channel.h`；CP 编译时 `SELF_CPU` 为 `MAILBOX_CPU0`。

<a id="id1"></a>

## **逻辑通道编号**

- 位 7–6：目标 CPU；位 5–4：源 CPU；位 3–0：通道序号（每对最多 16 个）
- 同向通道内数值越小优先级越高

CP → AP 方向预定义 `MB_CHNL_WIFI_CMD`、`MB_CHNL_LOG` 等系统通道，`MB_CHNL_LOG` 优先级
最低且须保持在枚举末尾。自定义通道勿与 `mailbox_channel.h` 中 `MB_CHNL_*` 冲突。

<a id="id2"></a>

## **典型流程**

`mb_chnl_init` → `mb_chnl_open` → ``` mb_chnl_ctrl``（注册 RX/TX 回调）→
``mb_chnl_write ``` / `mb_chnl_read` → `mb_chnl_close`。

大块数据或跨核拷贝见 `mb_chnl_buff.h`；IPC 服务注册见 `bk_api_ipc.c`。

<a id="id3"></a>

## **示例**

[multi-core mailbox](../../examples/platform/bk_logic_mailbox.md)

<a id="header-file"></a>

### Header File

- [mailbox\_channel.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/mailbox_channel.h)

<a id="functions"></a>

### Functions

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

### Unions

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

    <a id="_CPPv4N13mb_chnl_hdr_tUt2_11E"></a>

    <a id="_CPPv3N13mb_chnl_hdr_tUt2_11E"></a> <a id="unionmb__chnl__hdr__t_1af89e9ad1d1f88d944e3e5bf0eda917a1"></a> struct [mb\_chnl\_hdr\_t](#_CPPv413mb_chnl_hdr_t "mb_chnl_hdr_t")::\[anonymous\] \[anonymous\]

    <a id="_CPPv4N13mb_chnl_hdr_t4dataE"></a>

    <a id="_CPPv3N13mb_chnl_hdr_t4dataE"></a> <a id="_CPPv2N13mb_chnl_hdr_t4dataE"></a> <a id="mb_chnl_hdr_t::data__u32"></a> <a id="unionmb__chnl__hdr__t_1af60e22114b656a4b8fcec5d73fc281ee"></a> u32 data

<a id="structures"></a>

### Structures

<a id="_CPPv413mb_chnl_cmd_t"></a>

<a id="_CPPv313mb_chnl_cmd_t"></a> <a id="_CPPv213mb_chnl_cmd_t"></a> <a id="mb_chnl_cmd_t"></a> <a id="structmb__chnl__cmd__t"></a> struct mb\_chnl\_cmd\_t

<a id="_CPPv413mb_chnl_ack_t"></a>

<a id="_CPPv313mb_chnl_ack_t"></a> <a id="_CPPv213mb_chnl_ack_t"></a> <a id="mb_chnl_ack_t"></a> <a id="structmb__chnl__ack__t"></a> struct mb\_chnl\_ack\_t

<a id="macros"></a>

### Macros

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

<a id="c.SRC_CPU"></a>

<a id="mailbox__channel_8h_1a40d263724fe044c39dbb4137e991f83a"></a> SRC\_CPU

<a id="c.CHNL_STATE_MASK"></a>

<a id="mailbox__channel_8h_1ae0e6f8c06a24ddd4967649ac7e860ceb"></a> CHNL\_STATE\_MASK

<a id="c.CHNL_STATE_COM_FAIL"></a>

<a id="mailbox__channel_8h_1a4e7a2e241af2e10ef5db329b77b5961b"></a> CHNL\_STATE\_COM\_FAIL

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv418chnl_tx_cmpl_isr_t"></a>

<a id="_CPPv318chnl_tx_cmpl_isr_t"></a> <a id="_CPPv218chnl_tx_cmpl_isr_t"></a> <a id="chnl_tx_cmpl_isr_t"></a> <a id="mailbox__channel_8h_1abedcd8c2305146dc98c1c2f6c3cb96d9"></a> typedef void (\*chnl\_tx\_cmpl\_isr\_t)(void \*param, [mb\_chnl\_ack\_t](#_CPPv413mb_chnl_ack_t "mb_chnl_ack_t") \*ack\_buf)

<a id="_CPPv413chnl_tx_isr_t"></a>

<a id="_CPPv313chnl_tx_isr_t"></a> <a id="_CPPv213chnl_tx_isr_t"></a> <a id="chnl_tx_isr_t"></a> <a id="mailbox__channel_8h_1a77e0c951d0c0ab125f7290908b4f4411"></a> typedef void (\*chnl\_tx\_isr\_t)(void \*param)

<a id="_CPPv413chnl_rx_isr_t"></a>

<a id="_CPPv313chnl_rx_isr_t"></a> <a id="_CPPv213chnl_rx_isr_t"></a> <a id="chnl_rx_isr_t"></a> <a id="mailbox__channel_8h_1a07a06f20dcc209a03f3bd8d1adee4258"></a> typedef void (\*chnl\_rx\_isr\_t)(void \*param, [mb\_chnl\_cmd\_t](#_CPPv413mb_chnl_cmd_t "mb_chnl_cmd_t") \*cmd\_buf)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv4Ut1_4"></a>

<a id="_CPPv3Ut1_4"></a> <a id="mailbox__channel_8h_1adc29c2ff13d900c2f185ee95427fb06c"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt1_421CP0_MB_LOG_CHNL_STARTE"></a>

    <a id="_CPPv3NUt1_421CP0_MB_LOG_CHNL_STARTE"></a> <a id="mailbox__channel_8h_1adc29c2ff13d900c2f185ee95427fb06cae8464d6c8279a605cf44565df0d36e15"></a> enumerator CP0\_MB\_LOG\_CHNL\_START

    <a id="_CPPv4NUt1_419CP0_MB_LOG_CHNL_ENDE"></a>

    <a id="_CPPv3NUt1_419CP0_MB_LOG_CHNL_ENDE"></a> <a id="mailbox__channel_8h_1adc29c2ff13d900c2f185ee95427fb06ca5100b555e612cf28b62d095f4f29bb5a"></a> enumerator CP0\_MB\_LOG\_CHNL\_END

    <a id="_CPPv4NUt1_419CP0_MB_LOG_CHNL_MAXE"></a>

    <a id="_CPPv3NUt1_419CP0_MB_LOG_CHNL_MAXE"></a> <a id="mailbox__channel_8h_1adc29c2ff13d900c2f185ee95427fb06caf5f285dd978df67210431a40797d0e57"></a> enumerator CP0\_MB\_LOG\_CHNL\_MAX

<a id="_CPPv4Ut1_5"></a>

<a id="_CPPv3Ut1_5"></a> <a id="mailbox__channel_8h_1a61dadd085c1777f559549e05962b2c9e"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt1_521CP1_MB_LOG_CHNL_STARTE"></a>

    <a id="_CPPv3NUt1_521CP1_MB_LOG_CHNL_STARTE"></a> <a id="mailbox__channel_8h_1a61dadd085c1777f559549e05962b2c9ea1f3fe7e9d138841aa31fcc7f8af62eba"></a> enumerator CP1\_MB\_LOG\_CHNL\_START

    <a id="_CPPv4NUt1_519CP1_MB_LOG_CHNL_ENDE"></a>

    <a id="_CPPv3NUt1_519CP1_MB_LOG_CHNL_ENDE"></a> <a id="mailbox__channel_8h_1a61dadd085c1777f559549e05962b2c9ea29652cdc02cf1f454b177b3e21b7949c"></a> enumerator CP1\_MB\_LOG\_CHNL\_END

    <a id="_CPPv4NUt1_519CP1_MB_LOG_CHNL_MAXE"></a>

    <a id="_CPPv3NUt1_519CP1_MB_LOG_CHNL_MAXE"></a> <a id="mailbox__channel_8h_1a61dadd085c1777f559549e05962b2c9ea64c2d548b15d31456e796fe085f0fa2a"></a> enumerator CP1\_MB\_LOG\_CHNL\_MAX

<a id="_CPPv4Ut1_6"></a>

<a id="_CPPv3Ut1_6"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt1_621CP2_MB_LOG_CHNL_STARTE"></a>

    <a id="_CPPv3NUt1_621CP2_MB_LOG_CHNL_STARTE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635ae60514f1589a08036cee9558080e5a38"></a> enumerator CP2\_MB\_LOG\_CHNL\_START

    <a id="_CPPv4NUt1_615MB_CHNL_HW_CTRLE"></a>

    <a id="_CPPv3NUt1_615MB_CHNL_HW_CTRLE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a812f03d3b835e31c4f85a4920c77267f"></a> enumerator MB\_CHNL\_HW\_CTRL

    <a id="_CPPv4NUt1_615CP2_MB_CHNL_IPCE"></a>

    <a id="_CPPv3NUt1_615CP2_MB_CHNL_IPCE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a0d469e8861f0cdf0afb1e26557ce4268"></a> enumerator CP2\_MB\_CHNL\_IPC

    <a id="_CPPv4NUt1_611MB_CHNL_PWCE"></a>

    <a id="_CPPv3NUt1_611MB_CHNL_PWCE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635adc17383cce953ce09820860dfcd5b016"></a> enumerator MB\_CHNL\_PWC

    <a id="_CPPv4NUt1_614MB_CHNL_BT_CMDE"></a>

    <a id="_CPPv3NUt1_614MB_CHNL_BT_CMDE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a9c3c502bb95866ec587f7bcd9c86e4d9"></a> enumerator MB\_CHNL\_BT\_CMD

    <a id="_CPPv4NUt1_616MB_CHNL_WIFI_CMDE"></a>

    <a id="_CPPv3NUt1_616MB_CHNL_WIFI_CMDE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a5f6a3ab4ef31c264c8e748218bbdf114"></a> enumerator MB\_CHNL\_WIFI\_CMD

    <a id="_CPPv4NUt1_617MB_CHNL_WIFI_DATAE"></a>

    <a id="_CPPv3NUt1_617MB_CHNL_WIFI_DATAE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a3d968a2594e047b5b835628798cd4ddf"></a> enumerator MB\_CHNL\_WIFI\_DATA

    <a id="_CPPv4NUt1_611MB_CHNL_USBE"></a>

    <a id="_CPPv3NUt1_611MB_CHNL_USBE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a7ca5d2425a49c60a974407b00ed3f186"></a> enumerator MB\_CHNL\_USB

    <a id="_CPPv4NUt1_617MB_CHNL_MIPC_SYNCE"></a>

    <a id="_CPPv3NUt1_617MB_CHNL_MIPC_SYNCE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635aad17ef6c44b91977ff8b083db32afdce"></a> enumerator MB\_CHNL\_MIPC\_SYNC

    <a id="_CPPv4NUt1_610MB_CHNL_ATE"></a>

    <a id="_CPPv3NUt1_610MB_CHNL_ATE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635abf5c8403f467cd4aadba04c6b7390bbb"></a> enumerator MB\_CHNL\_AT

    <a id="_CPPv4NUt1_613MB_CHNL_UART0E"></a>

    <a id="_CPPv3NUt1_613MB_CHNL_UART0E"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a6238882455af66d3cf5e3eb5ddd71783"></a> enumerator MB\_CHNL\_UART0

    <a id="_CPPv4NUt1_613MB_CHNL_UART1E"></a>

    <a id="_CPPv3NUt1_613MB_CHNL_UART1E"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a171eedef949bac2b94062b004dc46187"></a> enumerator MB\_CHNL\_UART1

    <a id="_CPPv4NUt1_613MB_CHNL_FLASHE"></a>

    <a id="_CPPv3NUt1_613MB_CHNL_FLASHE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a00f69f3bea9d74746e8629a9e8b8e900"></a> enumerator MB\_CHNL\_FLASH

    <a id="_CPPv4NUt1_614MB_CHNL_SARADCE"></a>

    <a id="_CPPv3NUt1_614MB_CHNL_SARADCE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a32ce438f5defa1b565e8b857d3f04063"></a> enumerator MB\_CHNL\_SARADC

    <a id="_CPPv4NUt1_611MB_CHNL_PHYE"></a>

    <a id="_CPPv3NUt1_611MB_CHNL_PHYE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a71b06e7492ecb8d3b00b58ec4643308e"></a> enumerator MB\_CHNL\_PHY

    <a id="_CPPv4NUt1_615MB_CHNL_AUD_AECE"></a>

    <a id="_CPPv3NUt1_615MB_CHNL_AUD_AECE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635add7319a64e2a311971b90d11e32b4fe1"></a> enumerator MB\_CHNL\_AUD\_AEC

    <a id="_CPPv4NUt1_611MB_CHNL_LOGE"></a>

    <a id="_CPPv3NUt1_611MB_CHNL_LOGE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a7e2d199d918137106c0d18e966971501"></a> enumerator MB\_CHNL\_LOG

    <a id="_CPPv4NUt1_619CP2_MB_LOG_CHNL_ENDE"></a>

    <a id="_CPPv3NUt1_619CP2_MB_LOG_CHNL_ENDE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635a201b8eadac51e5addbe5fd216a2a8891"></a> enumerator CP2\_MB\_LOG\_CHNL\_END

    <a id="_CPPv4NUt1_619CP2_MB_LOG_CHNL_MAXE"></a>

    <a id="_CPPv3NUt1_619CP2_MB_LOG_CHNL_MAXE"></a> <a id="mailbox__channel_8h_1a726ca809ffd3d67ab4b8476646f26635acf2c0691b60864f21c625c22428ab5bf"></a> enumerator CP2\_MB\_LOG\_CHNL\_MAX

<a id="_CPPv4Ut1_7"></a>

<a id="_CPPv3Ut1_7"></a> <a id="mailbox__channel_8h_1a0411cd49bb5b71852cecd93bcbf0ca2d"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt1_721CP3_MB_LOG_CHNL_STARTE"></a>

    <a id="_CPPv3NUt1_721CP3_MB_LOG_CHNL_STARTE"></a> <a id="mailbox__channel_8h_1a0411cd49bb5b71852cecd93bcbf0ca2daf1421c87a1c49ba5a986656b74eccd12"></a> enumerator CP3\_MB\_LOG\_CHNL\_START

    <a id="_CPPv4NUt1_719CP3_MB_LOG_CHNL_ENDE"></a>

    <a id="_CPPv3NUt1_719CP3_MB_LOG_CHNL_ENDE"></a> <a id="mailbox__channel_8h_1a0411cd49bb5b71852cecd93bcbf0ca2da8b68c9b63965452a68823257efafac45"></a> enumerator CP3\_MB\_LOG\_CHNL\_END

    <a id="_CPPv4NUt1_719CP3_MB_LOG_CHNL_MAXE"></a>

    <a id="_CPPv3NUt1_719CP3_MB_LOG_CHNL_MAXE"></a> <a id="mailbox__channel_8h_1a0411cd49bb5b71852cecd93bcbf0ca2da6f7bef5febabf57ae3a8c923981b8c31"></a> enumerator CP3\_MB\_LOG\_CHNL\_MAX

<a id="_CPPv4Ut1_8"></a>

<a id="_CPPv3Ut1_8"></a> <a id="mailbox__channel_8h_1abed82baf7f470b522273a3e37c24c600"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt1_817ACK_STATE_PENDINGE"></a>

    <a id="_CPPv3NUt1_817ACK_STATE_PENDINGE"></a> <a id="mailbox__channel_8h_1abed82baf7f470b522273a3e37c24c600a19a848d8730ac409b0ac60539cd6a8c5"></a> enumerator ACK\_STATE\_PENDING

    <a id="_CPPv4NUt1_818ACK_STATE_COMPLETEE"></a>

    <a id="_CPPv3NUt1_818ACK_STATE_COMPLETEE"></a> <a id="mailbox__channel_8h_1abed82baf7f470b522273a3e37c24c600aaff9b9f5425ba9fcc15fcf13dc9e722e"></a> enumerator ACK\_STATE\_COMPLETE

    <a id="_CPPv4NUt1_814ACK_STATE_FAILE"></a>

    <a id="_CPPv3NUt1_814ACK_STATE_FAILE"></a> <a id="mailbox__channel_8h_1abed82baf7f470b522273a3e37c24c600a49eaad5fcd74b5eee68b24286952feab"></a> enumerator ACK\_STATE\_FAIL

<a id="_CPPv4Ut1_9"></a>

<a id="_CPPv3Ut1_9"></a> <a id="mailbox__channel_8h_1ab04a0655cd1e3bcac5e8f48c18df1a57"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt1_918MB_CHNL_GET_STATUSE"></a>

    <a id="_CPPv3NUt1_918MB_CHNL_GET_STATUSE"></a> <a id="mailbox__channel_8h_1ab04a0655cd1e3bcac5e8f48c18df1a57a6c055355f86c53d23184e5e5a59af8fc"></a> enumerator MB\_CHNL\_GET\_STATUS

    <a id="_CPPv4NUt1_918MB_CHNL_SET_RX_ISRE"></a>

    <a id="_CPPv3NUt1_918MB_CHNL_SET_RX_ISRE"></a> <a id="mailbox__channel_8h_1ab04a0655cd1e3bcac5e8f48c18df1a57a7fcd12457c6858295341a0e62aaf12ea"></a> enumerator MB\_CHNL\_SET\_RX\_ISR

    <a id="_CPPv4NUt1_918MB_CHNL_SET_TX_ISRE"></a>

    <a id="_CPPv3NUt1_918MB_CHNL_SET_TX_ISRE"></a> <a id="mailbox__channel_8h_1ab04a0655cd1e3bcac5e8f48c18df1a57a20a9b622dca3d0305df4010533a06801"></a> enumerator MB\_CHNL\_SET\_TX\_ISR

    <a id="_CPPv4NUt1_923MB_CHNL_SET_TX_CMPL_ISRE"></a>

    <a id="_CPPv3NUt1_923MB_CHNL_SET_TX_CMPL_ISRE"></a> <a id="mailbox__channel_8h_1ab04a0655cd1e3bcac5e8f48c18df1a57a407262ff420a88ae35d8dc46dd21a433"></a> enumerator MB\_CHNL\_SET\_TX\_CMPL\_ISR

    <a id="_CPPv4NUt1_918MB_CHNL_WRITE_SYNCE"></a>

    <a id="_CPPv3NUt1_918MB_CHNL_WRITE_SYNCE"></a> <a id="mailbox__channel_8h_1ab04a0655cd1e3bcac5e8f48c18df1a57a3764fe87b0c2d0c432c130131668defb"></a> enumerator MB\_CHNL\_WRITE\_SYNC

    <a id="_CPPv4NUt1_916MB_CHNL_TX_RESETE"></a>

    <a id="_CPPv3NUt1_916MB_CHNL_TX_RESETE"></a> <a id="mailbox__channel_8h_1ab04a0655cd1e3bcac5e8f48c18df1a57a7f1d67f0b667bd0752811029084460f6"></a> enumerator MB\_CHNL\_TX\_RESET
