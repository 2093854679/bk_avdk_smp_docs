---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/wifi/bk_rlk.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bk-rlk-api"></a>

# BK-RLK API

`ap/include/modules/raw_link.h` 提供 BK-RLK 原链路通信 API。使用指南见 [Armino Wi-Fi BK-RLK 使用指南](../../developer-guide/wifi/bk_rlk.md)。

<a id="raw-link-h"></a>

## raw\_link.h

<a id="header-file"></a>

### Header File

- [raw\_link.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/modules/raw_link.h)

<a id="functions"></a>

### Functions

<a id="_CPPv411bk_rlk_initv"></a>

<a id="_CPPv311bk_rlk_initv"></a> <a id="_CPPv211bk_rlk_initv"></a> <a id="bk_rlk_init__void"></a> <a id="raw__link_8h_1aad9cf94995ec0409fb5c06a88ded806f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_init(void)
:   Initialize Raw Link function.

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv413bk_rlk_deinitv"></a>

<a id="_CPPv313bk_rlk_deinitv"></a> <a id="_CPPv213bk_rlk_deinitv"></a> <a id="bk_rlk_deinit__void"></a> <a id="raw__link_8h_1a15156403bc70650ce765c21f0be985e4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_deinit(void)
:   De-Initialize Raw Link function.

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv423bk_rlk_register_recv_cb16bk_rlk_recv_cb_t"></a>

<a id="_CPPv323bk_rlk_register_recv_cb16bk_rlk_recv_cb_t"></a> <a id="_CPPv223bk_rlk_register_recv_cb16bk_rlk_recv_cb_t"></a> <a id="bk_rlk_register_recv_cb__bk_rlk_recv_cb_t"></a> <a id="raw__link_8h_1acf871abf66168a3746e524941c031579"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_register\_recv\_cb([bk\_rlk\_recv\_cb\_t](#_CPPv416bk_rlk_recv_cb_t "bk_rlk_recv_cb_t") cb)
:   Register callback function of receiving Raw Link data.

    参数
    :   **cb** – callback function of receiving Raw Link data

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NOT\_INIT: Raw Link is not initialized
        - others : other errors

<a id="_CPPv423bk_rlk_ungister_recv_cbv"></a>

<a id="_CPPv323bk_rlk_ungister_recv_cbv"></a> <a id="_CPPv223bk_rlk_ungister_recv_cbv"></a> <a id="bk_rlk_ungister_recv_cb__void"></a> <a id="raw__link_8h_1acf934e6e36e8d2331b7cfefc83bd6c32"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_ungister\_recv\_cb(void)
:   Unregister callback function of receiving Raw Link data.

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized
        - others : other errors

<a id="_CPPv423bk_rlk_register_send_cb16bk_rlk_send_cb_t"></a>

<a id="_CPPv323bk_rlk_register_send_cb16bk_rlk_send_cb_t"></a> <a id="_CPPv223bk_rlk_register_send_cb16bk_rlk_send_cb_t"></a> <a id="bk_rlk_register_send_cb__bk_rlk_send_cb_t"></a> <a id="raw__link_8h_1ad7d7663cfa4ec7076093f4e63b35a5fa"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_register\_send\_cb([bk\_rlk\_send\_cb\_t](#_CPPv416bk_rlk_send_cb_t "bk_rlk_send_cb_t") cb)
:   Register callback function of sending BK RLK data.

    参数
    :   **cb** – callback function of sending BK RLK data for MAC send status

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv425bk_rlk_unregister_send_cbv"></a>

<a id="_CPPv325bk_rlk_unregister_send_cbv"></a> <a id="_CPPv225bk_rlk_unregister_send_cbv"></a> <a id="bk_rlk_unregister_send_cb__void"></a> <a id="raw__link_8h_1a2d83f6299e21d02c83b4251e0f85f587"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_unregister\_send\_cb(void)
:   Unregister callback function of sending Raw Link data.

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv426bk_rlk_register_acs_cfm_cb15bk_rlk_acs_cb_t"></a>

<a id="_CPPv326bk_rlk_register_acs_cfm_cb15bk_rlk_acs_cb_t"></a> <a id="_CPPv226bk_rlk_register_acs_cfm_cb15bk_rlk_acs_cb_t"></a> <a id="bk_rlk_register_acs_cfm_cb__bk_rlk_acs_cb_t"></a> <a id="raw__link_8h_1aaa7bd8f4a1eb3d8cfae2327ac10efc6c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_register\_acs\_cfm\_cb([bk\_rlk\_acs\_cb\_t](#_CPPv415bk_rlk_acs_cb_t "bk_rlk_acs_cb_t") cb)
:   Register callback function of Raw Link ACS confirmation.

    参数
    :   **cb** – callback function of Raw Link ACS confirmation status

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv428bk_rlk_unregister_acs_cfm_cbv"></a>

<a id="_CPPv328bk_rlk_unregister_acs_cfm_cbv"></a> <a id="_CPPv228bk_rlk_unregister_acs_cfm_cbv"></a> <a id="bk_rlk_unregister_acs_cfm_cb__void"></a> <a id="raw__link_8h_1acef64bf64d79f3a615030c811c5061fc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_unregister\_acs\_cfm\_cb(void)
:   Unregister callback function of Raw Link ACS confirmation.

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv418bk_rlk_set_channel7uint8_t"></a>

<a id="_CPPv318bk_rlk_set_channel7uint8_t"></a> <a id="_CPPv218bk_rlk_set_channel7uint8_t"></a> <a id="bk_rlk_set_channel__uint8_t"></a> <a id="raw__link_8h_1abddf85a672ba5e1d2b87c4f5f5410f11"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_set\_channel(uint8\_t chan)
:   Set BK Raw Link channel.

    **Attention**
    :   1\. Currently we only support HT20, chan-\>second should always be 0\.

    **Attention**
    :   2\. This API is only used for settting Raw Link channel, NOT for other purpose.

    **Attention**
    :   3\. The channel range can be set is from channel 1 to channel 13,

    参数
    :   **chan** – channel of Raw Link

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv418bk_rlk_get_channelv"></a>

<a id="_CPPv318bk_rlk_get_channelv"></a> <a id="_CPPv218bk_rlk_get_channelv"></a> <a id="bk_rlk_get_channel__void"></a> <a id="raw__link_8h_1a9535b4e84b228a5b63013c3a3b8ca396"></a> uint8\_t bk\_rlk\_get\_channel(void)
:   BK Raw Link get current channel.

    **Attention**
    :   1\. This API is only valid if it is called after bk\_rlk\_init()

    返回
    :   - chan : current channel
        - others : Failed to set mac header type

<a id="_CPPv411bk_rlk_sendPK7uint8_tPKv6size_t"></a>

<a id="_CPPv311bk_rlk_sendPK7uint8_tPKv6size_t"></a> <a id="_CPPv211bk_rlk_sendPK7uint8_tPKv6size_t"></a> <a id="bk_rlk_send__uint8_tCP.voidCP.s"></a> <a id="raw__link_8h_1a5c626012d27ac53a50056766207eb4d2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_send(const uint8\_t \*peer\_mac\_addr, const void \*data, size\_t len)
:   Send BK Raw Links data.

    **Attention**
    :   1\. If peer\_addr is not NULL, send data to the peer whose MAC address matches peer\_addr

    **Attention**
    :   2\. If peer\_addr is NULL, send data to all of the peers that are added to the peer list

    参数
    :   - **peer\_mac\_addr** – peer MAC address
        - **data** – data to send
        - **len** – length of data

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized
        - BK\_ERR\_NO\_MEM : out of memory
        - BK\_ERR\_NOT\_FOUND : peer is not found

<a id="_CPPv414bk_rlk_send_exPK7uint8_tPK20bk_rlk_config_info_t"></a>

<a id="_CPPv314bk_rlk_send_exPK7uint8_tPK20bk_rlk_config_info_t"></a> <a id="_CPPv214bk_rlk_send_exPK7uint8_tPK20bk_rlk_config_info_t"></a> <a id="bk_rlk_send_ex__uint8_tCP.bk_rlk_config_info_tCP"></a> <a id="raw__link_8h_1a3c0dc701318b1dd427bb7097faa79852"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_send\_ex(const uint8\_t \*peer\_mac\_addr, const [bk\_rlk\_config\_info\_t](#_CPPv420bk_rlk_config_info_t "bk_rlk_config_info_t") \*rlk\_tx)
:   Send Raw Links data.

    **Attention**
    :   1\. If peer\_addr is not NULL, send data to the peer whose MAC address matches peer\_addr

    **Attention**
    :   2\. If peer\_addr is NULL, send data to all of the peers that are added to the peer list

    **Attention**
    :   3\. if set cb is not NULL,cb prototype void (\*)(void \*, bool) cb has two arguments, first is args, second is tx success flag

    参数
    :   - **peer\_mac\_addr** – peer MAC address
        - **rlk\_tx** – configure BK Raw Link sending data information

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized
        - BK\_ERR\_NO\_MEM : out of memory
        - BK\_ERR\_NOT\_FOUND : peer is not found

<a id="_CPPv418bk_rlk_send_by_ouiPK7uint8_tPKv6size_t7uint8_tP7uint8_t"></a>

<a id="_CPPv318bk_rlk_send_by_ouiPK7uint8_tPKv6size_t7uint8_tP7uint8_t"></a> <a id="_CPPv218bk_rlk_send_by_ouiPK7uint8_tPKv6size_t7uint8_tP7uint8_t"></a> <a id="bk_rlk_send_by_oui__uint8_tCP.voidCP.s.uint8_t.uint8_tP"></a> <a id="raw__link_8h_1a3a07dd3332c48ef672b8785e270fe7f2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_send\_by\_oui(const uint8\_t \*peer\_mac\_addr, const void \*data, size\_t len, uint8\_t mac\_type, uint8\_t \*oui)
:   Send BK Raw Links data.

    **Attention**
    :   1\. If peer\_addr is not NULL, send data to the peer whose MAC address matches peer\_addr

    **Attention**
    :   2\. If peer\_addr is NULL, send data to all of the peers that are added to the peer list

    参数
    :   - **peer\_mac\_addr** – peer MAC address
        - **data** – data to send
        - **len** – length of data
        - **mac\_type** – frame type
        - **oui** – vendor oui

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized
        - BK\_ERR\_NO\_MEM : out of memory
        - BK\_ERR\_NOT\_FOUND : peer is not found

<a id="_CPPv415bk_rlk_add_peerPK18bk_rlk_peer_info_t"></a>

<a id="_CPPv315bk_rlk_add_peerPK18bk_rlk_peer_info_t"></a> <a id="_CPPv215bk_rlk_add_peerPK18bk_rlk_peer_info_t"></a> <a id="bk_rlk_add_peer__bk_rlk_peer_info_tCP"></a> <a id="raw__link_8h_1a3abf766f9976436a019deea7e35f174b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_add\_peer(const [bk\_rlk\_peer\_info\_t](#_CPPv418bk_rlk_peer_info_t "bk_rlk_peer_info_t") \*peer)
:   Add a peer to peer list.

    参数
    :   **peer** – peer information

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized
        - BK\_ERR\_IS\_FALL : peer list is full
        - BK\_ERR\_NO\_MEM : out of memory
        - BK\_ERR\_IS\_EXIST : peer has existed

<a id="_CPPv415bk_rlk_del_peerPK7uint8_t"></a>

<a id="_CPPv315bk_rlk_del_peerPK7uint8_t"></a> <a id="_CPPv215bk_rlk_del_peerPK7uint8_t"></a> <a id="bk_rlk_del_peer__uint8_tCP"></a> <a id="raw__link_8h_1a9cad2bbeafb9eaa40b0d0da2f9953f6a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_del\_peer(const uint8\_t \*peer\_mac\_addr)
:   Delete a peer from peer list.

    参数
    :   **peer\_mac\_addr** – peer MAC address

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized
        - BK\_ERR\_NOT\_FOUND : peer is not found

<a id="_CPPv415bk_rlk_get_peerPK7uint8_tP18bk_rlk_peer_info_t"></a>

<a id="_CPPv315bk_rlk_get_peerPK7uint8_tP18bk_rlk_peer_info_t"></a> <a id="_CPPv215bk_rlk_get_peerPK7uint8_tP18bk_rlk_peer_info_t"></a> <a id="bk_rlk_get_peer__uint8_tCP.bk_rlk_peer_info_tP"></a> <a id="raw__link_8h_1a67c51797d1ca3ca176bde7ab4bbbd005"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_get\_peer(const uint8\_t \*peer\_mac\_addr, [bk\_rlk\_peer\_info\_t](#_CPPv418bk_rlk_peer_info_t "bk_rlk_peer_info_t") \*peer)
:   Get a peer whose MAC address matches peer\_addr from peer list.

    参数
    :   - **peer\_mac\_addr** – peer MAC address
        - **peer** – peer information

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized
        - BK\_ERR\_NOT\_FOUND : peer is not found

<a id="_CPPv420bk_rlk_is_peer_existPK7uint8_t"></a>

<a id="_CPPv320bk_rlk_is_peer_existPK7uint8_t"></a> <a id="_CPPv220bk_rlk_is_peer_existPK7uint8_t"></a> <a id="bk_rlk_is_peer_exist__uint8_tCP"></a> <a id="raw__link_8h_1ae39f46051e0b093cc544bb6e5a967e6d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_is\_peer\_exist(const uint8\_t \*peer\_mac\_addr)
:   Peer exists or not.

    参数
    :   **peer\_mac\_addr** – peer MAC address

    返回
    :   - BK\_OK : peer exists
        - others : peer not exists

<a id="_CPPv419bk_rlk_get_peer_numP8uint32_t"></a>

<a id="_CPPv319bk_rlk_get_peer_numP8uint32_t"></a> <a id="_CPPv219bk_rlk_get_peer_numP8uint32_t"></a> <a id="bk_rlk_get_peer_num__uint32_tP"></a> <a id="raw__link_8h_1aa49178b847b8f0207a948f5e1e4dd33a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_get\_peer\_num(uint32\_t \*total\_num)
:   Get the number of peers.

    参数
    :   **num** – number of peers

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_RLK\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv416bk_rlk_set_tx_ac7uint8_t"></a>

<a id="_CPPv316bk_rlk_set_tx_ac7uint8_t"></a> <a id="_CPPv216bk_rlk_set_tx_ac7uint8_t"></a> <a id="bk_rlk_set_tx_ac__uint8_t"></a> <a id="raw__link_8h_1a9eb005b2167d32678667084a6aafb688"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_set\_tx\_ac(uint8\_t ac)
:   Set BK Raw Link TX AC.

    参数
    :   **ac** – sending Raw Link data AC

    返回
    :   - BK\_OK : succeed
        - others : Set TX AC error

<a id="_CPPv424bk_rlk_set_tx_timeout_ms8uint16_t"></a>

<a id="_CPPv324bk_rlk_set_tx_timeout_ms8uint16_t"></a> <a id="_CPPv224bk_rlk_set_tx_timeout_ms8uint16_t"></a> <a id="bk_rlk_set_tx_timeout_ms__uint16_t"></a> <a id="raw__link_8h_1a767cfb47b513844f37e9fe21d9dd4cf9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_set\_tx\_timeout\_ms(uint16\_t timeout\_ms)
:   Set BK Raw Link TX timeout.

    参数
    :   **ac** – sending Raw Link data timeout

    返回
    :   - BK\_OK : succeed
        - others : Set TX timeout error

<a id="_CPPv419bk_rlk_set_tx_power8uint32_t"></a>

<a id="_CPPv319bk_rlk_set_tx_power8uint32_t"></a> <a id="_CPPv219bk_rlk_set_tx_power8uint32_t"></a> <a id="bk_rlk_set_tx_power__uint32_t"></a> <a id="raw__link_8h_1a972468f7878d7c92e828f672bb727ac5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_set\_tx\_power(uint32\_t power)
:   Set BK Raw Link TX power.

    参数
    :   **power** – TX power control

    返回
    :   - BK\_OK : succeed
        - others : Set TX power error

<a id="_CPPv418bk_rlk_set_tx_rate8uint32_t"></a>

<a id="_CPPv318bk_rlk_set_tx_rate8uint32_t"></a> <a id="_CPPv218bk_rlk_set_tx_rate8uint32_t"></a> <a id="bk_rlk_set_tx_rate__uint32_t"></a> <a id="raw__link_8h_1a61a40703b16f50ab6c63c444ff9f4300"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_set\_tx\_rate(uint32\_t rate)
:   Set BK Raw Link TX rate.

    参数
    :   **rate** – TX rate control

    返回
    :   - BK\_OK : succeed
        - others : Set TX rate error

<a id="_CPPv423bk_rlk_set_tx_retry_cnt8uint32_t"></a>

<a id="_CPPv323bk_rlk_set_tx_retry_cnt8uint32_t"></a> <a id="_CPPv223bk_rlk_set_tx_retry_cnt8uint32_t"></a> <a id="bk_rlk_set_tx_retry_cnt__uint32_t"></a> <a id="raw__link_8h_1acd1b26be051bbccc134175be0d9a5deb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_set\_tx\_retry\_cnt(uint32\_t retry\_cnt)
:   Set BK Raw Link TX retry count.

    参数
    :   **rate** – TX retry count control

    返回
    :   - BK\_OK : succeed
        - others : Set TX rate error

<a id="_CPPv412bk_rlk_sleepv"></a>

<a id="_CPPv312bk_rlk_sleepv"></a> <a id="_CPPv212bk_rlk_sleepv"></a> <a id="bk_rlk_sleep__void"></a> <a id="raw__link_8h_1a5cdd7b971b9904d0c651b6be8e746cb4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_sleep(void)
:   Let Raw Link goto sleep mode to reduce power consumption.

    参数
    :   **void** –

    返回
    :   - BK\_OK : succeed
        - others : Raw Link failed to sleep

<a id="_CPPv413bk_rlk_wakeupv"></a>

<a id="_CPPv313bk_rlk_wakeupv"></a> <a id="_CPPv213bk_rlk_wakeupv"></a> <a id="bk_rlk_wakeup__void"></a> <a id="raw__link_8h_1af6dbffcedcf34023739d2be0ebbfefc6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_wakeup(void)
:   wakeup Raw Link

    参数
    :   **void** –

    返回
    :   - BK\_OK : succeed
        - others : Failed to wakeup raw link

<a id="_CPPv421bk_rlk_add_white_list7uint8_tP7uint8_t"></a>

<a id="_CPPv321bk_rlk_add_white_list7uint8_tP7uint8_t"></a> <a id="_CPPv221bk_rlk_add_white_list7uint8_tP7uint8_t"></a> <a id="bk_rlk_add_white_list__uint8_t.uint8_tP"></a> <a id="raw__link_8h_1ace3c7b12c2ca2fda7067bb7bc21be364"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_add\_white\_list(uint8\_t mac\_type, uint8\_t \*oui)
:   Raw Link add white list.

    参数
    :   - **mac\_type** – frame type
        - **oui** – vendor oui

    返回
    :   - BK\_OK : succeed
        - others : Failed to add white list

<a id="_CPPv421bk_rlk_del_white_list7uint8_tP7uint8_t"></a>

<a id="_CPPv321bk_rlk_del_white_list7uint8_tP7uint8_t"></a> <a id="_CPPv221bk_rlk_del_white_list7uint8_tP7uint8_t"></a> <a id="bk_rlk_del_white_list__uint8_t.uint8_tP"></a> <a id="raw__link_8h_1a46a250133d08fe5b390c8ea871534c5b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_del\_white\_list(uint8\_t mac\_type, uint8\_t \*oui)
:   Raw Link delete white list.

    参数
    :   - **mac\_type** – frame type
        - **oui** – vendor oui

    返回
    :   - BK\_OK : succeed
        - others : Failed to delete white list

<a id="_CPPv423bk_rlk_set_mac_hdr_type8uint16_t"></a>

<a id="_CPPv323bk_rlk_set_mac_hdr_type8uint16_t"></a> <a id="_CPPv223bk_rlk_set_mac_hdr_type8uint16_t"></a> <a id="bk_rlk_set_mac_hdr_type__uint16_t"></a> <a id="raw__link_8h_1afe950608190580bab393ff6f98ad98f2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_set\_mac\_hdr\_type(uint16\_t type)
:   Raw Link set MAC header type.

    **Attention**
    :   1\. This API is only valid if it is called after bk\_rlk\_init()

    参数
    :   **type** – The frame type used in 802.11 protocol BK-RLK support configurable types as shown in bk\_rlk\_mac\_hdr\_type\_t

    返回
    :   - BK\_OK : succeed
        - others : Failed to set mac header type

<a id="_CPPv421bk_rlk_mac_hdr_reinitv"></a>

<a id="_CPPv321bk_rlk_mac_hdr_reinitv"></a> <a id="_CPPv221bk_rlk_mac_hdr_reinitv"></a> <a id="bk_rlk_mac_hdr_reinit__void"></a> <a id="raw__link_8h_1a5641432a1559aa0e1435bf1ad4c4b774"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_mac\_hdr\_reinit(void)
:   BK-RLK MAC header reinit.

    参数
    :   **void** –

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized
        - others : Failed to reinit mac header

<a id="_CPPv416bk_rlk_acs_checkv"></a>

<a id="_CPPv316bk_rlk_acs_checkv"></a> <a id="_CPPv216bk_rlk_acs_checkv"></a> <a id="bk_rlk_acs_check__void"></a> <a id="raw__link_8h_1abb5f0953702f4c42fedfea2521537447"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_acs\_check(void)
:   Raw Link Auto Channel Select (ACS) funtion.

    **Attention**
    :   1\. This API is only valid if it is called after bk\_rlk\_init()

        1. The result of BK-RLK ACS is obtained to bk\_rlk\_register\_acs\_cfm\_cb
        2. This API only feeds back the evaluation of each cnannel and the suggested best channel.Automatic channel switching is temporarily closed and opened after full verification.

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv427bk_rlk_register_scan_cfm_cb16bk_rlk_scan_cb_t"></a>

<a id="_CPPv327bk_rlk_register_scan_cfm_cb16bk_rlk_scan_cb_t"></a> <a id="_CPPv227bk_rlk_register_scan_cfm_cb16bk_rlk_scan_cb_t"></a> <a id="bk_rlk_register_scan_cfm_cb__bk_rlk_scan_cb_t"></a> <a id="raw__link_8h_1a4dd9c31f60dc8ac0a63dde07143f791c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_register\_scan\_cfm\_cb([bk\_rlk\_scan\_cb\_t](#_CPPv416bk_rlk_scan_cb_t "bk_rlk_scan_cb_t") cb)
:   Register callback function of Raw Link SCAN confirmation.

    参数
    :   **cb** – callback function of Raw Link SCAN confirmation status

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv429bk_rlk_unregister_scan_cfm_cbv"></a>

<a id="_CPPv329bk_rlk_unregister_scan_cfm_cbv"></a> <a id="_CPPv229bk_rlk_unregister_scan_cfm_cbv"></a> <a id="bk_rlk_unregister_scan_cfm_cb__void"></a> <a id="raw__link_8h_1a404ff1f13d9f1b3ac2607a1c92fb31ec"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_unregister\_scan\_cfm\_cb(void)
:   Unregister callback function of Raw Link SCAN confirmation.

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv411bk_rlk_scanP18bk_rlk_scan_info_t"></a>

<a id="_CPPv311bk_rlk_scanP18bk_rlk_scan_info_t"></a> <a id="_CPPv211bk_rlk_scanP18bk_rlk_scan_info_t"></a> <a id="bk_rlk_scan__bk_rlk_scan_info_tP"></a> <a id="raw__link_8h_1aade9815a02af9a9a9daf6d5fffc779bd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_scan([bk\_rlk\_scan\_info\_t](#_CPPv418bk_rlk_scan_info_t "bk_rlk_scan_info_t") \*scan\_info)
:   BK Raw Link scan funtion.

    **Attention**
    :   1\. This API is only valid if it is called after bk\_rlk\_init()

        1. This API is only valid if it is called after bk\_rlk\_set\_role()

        1. The result of BK-RLK ACS is obtained to bk\_rlk\_register\_scan\_cfm\_cb
        2. This API only feeds back the BK-RLK devices of each cnannel

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv415bk_rlk_set_role13bk_rlk_role_tP23bk_rlk_extra_ies_info_t"></a>

<a id="_CPPv315bk_rlk_set_role13bk_rlk_role_tP23bk_rlk_extra_ies_info_t"></a> <a id="_CPPv215bk_rlk_set_role13bk_rlk_role_tP23bk_rlk_extra_ies_info_t"></a> <a id="bk_rlk_set_role__bk_rlk_role_t.bk_rlk_extra_ies_info_tP"></a> <a id="raw__link_8h_1a95f4b2cd79e43f469cb7100f634f3ee8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_set\_role([bk\_rlk\_role\_t](#_CPPv413bk_rlk_role_t "bk_rlk_role_t") role, [bk\_rlk\_extra\_ies\_info\_t](#_CPPv423bk_rlk_extra_ies_info_t "bk_rlk_extra_ies_info_t") \*ies\_info)
:   Set the role of the current BK Raw Link device.

    **Attention**
    :   1\. This API is only valid if it is called after bk\_rlk\_init()

        1. Current devices support roles are as follows:

           - BK\_RLK\_MASTER The master role sends Network Announcement frame regularly to keep time synchronization and keep alive with connected devices.
           - BK\_RLK\_SLAVE The slave role connects BK\_RLK\_MASTER devices.
           - BK\_RLK\_DUBID The double identity role. Support scan when add extra\_ies
           - BK\_RLK\_IDLE In a role-free state, the device cannot send frames but can receive frame.
        2. This role setting is optional.When the role is not set,the devices management is completely taken over by the upper application.

    参数
    :   **role** – Set the role of the current BK-RLK device

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv421bk_rlk_slave_app_initPc"></a>

<a id="_CPPv321bk_rlk_slave_app_initPc"></a> <a id="_CPPv221bk_rlk_slave_app_initPc"></a> <a id="bk_rlk_slave_app_init__cP"></a> <a id="raw__link_8h_1a1689e1e2055b421ef7c0d31d46a8fb5a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_slave\_app\_init(char \*ssid)
:   Start BK Raw Link slave device and connection master device.

    **Attention**
    :   1\. This API is only valid if it is called after bk\_rlk\_init()

        1. This API is only valid if it is called after bk\_rlk\_set\_role()

    参数
    :   **ssid** – The ssid of master device to be connected.

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv427bk_rlk_slave_bssid_app_initP7uint8_t"></a>

<a id="_CPPv327bk_rlk_slave_bssid_app_initP7uint8_t"></a> <a id="_CPPv227bk_rlk_slave_bssid_app_initP7uint8_t"></a> <a id="bk_rlk_slave_bssid_app_init__uint8_tP"></a> <a id="raw__link_8h_1a60cd3b681ba78904b4201db0de3f3022"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_slave\_bssid\_app\_init(uint8\_t \*bssid)
:   Start BK Raw Link slave device and connection master device.

    **Attention**
    :   1\. This API is only valid if it is called after bk\_rlk\_init()

        1. This API is only valid if it is called after bk\_rlk\_set\_role()

    参数
    :   **bssid** – The bssid of master device to be connected.

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="_CPPv431bk_rlk_set_acs_auto_switch_chan8uint32_t"></a>

<a id="_CPPv331bk_rlk_set_acs_auto_switch_chan8uint32_t"></a> <a id="_CPPv231bk_rlk_set_acs_auto_switch_chan8uint32_t"></a> <a id="bk_rlk_set_acs_auto_switch_chan__uint32_t"></a> <a id="raw__link_8h_1a5f0609c5757149b1ff335bd8d9a40db2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_rlk\_set\_acs\_auto\_switch\_chan(uint32\_t auto\_switch)
:   BK Raw Link set ACS automatic switch channel.

    **Attention**
    :   1\. This API is only valid if it is called after bk\_rlk\_init()

        1. This API is only valid if it is called after bk\_rlk\_set\_role()

    参数
    :   **auto** – ture auto switch channel,false not auto switch channel

    返回
    :   - BK\_OK : succeed
        - BK\_ERR\_NOT\_INIT : Raw Link is not initialized

<a id="structures"></a>

### Structures

<a id="_CPPv416bk_rlk_peer_info"></a>

<a id="_CPPv316bk_rlk_peer_info"></a> <a id="_CPPv216bk_rlk_peer_info"></a> <a id="bk_rlk_peer_info"></a> <a id="structbk__rlk__peer__info"></a> struct bk\_rlk\_peer\_info
:   BK Raw Link(RLK) peer list context structure.

<a id="_CPPv418bk_rlk_config_info"></a>

<a id="_CPPv318bk_rlk_config_info"></a> <a id="_CPPv218bk_rlk_config_info"></a> <a id="bk_rlk_config_info"></a> <a id="structbk__rlk__config__info"></a> struct bk\_rlk\_config\_info
:   BK Raw Link(RLK) configure tx information.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_rlk_config_info3lenE"></a>

    <a id="_CPPv3N18bk_rlk_config_info3lenE"></a> <a id="_CPPv2N18bk_rlk_config_info3lenE"></a> <a id="bk_rlk_config_info::len__uint16_t"></a> <a id="structbk__rlk__config__info_1a0301308bdb4f07e221b9c984c49db476"></a> uint16\_t len
    :   Rx length of BK RLK packet

    <a id="_CPPv4N18bk_rlk_config_info4dataE"></a>

    <a id="_CPPv3N18bk_rlk_config_info4dataE"></a> <a id="_CPPv2N18bk_rlk_config_info4dataE"></a> <a id="bk_rlk_config_info::data__uint8_tP"></a> <a id="structbk__rlk__config__info_1a70399f65664ecbb008f2f293f41dcaf6"></a> uint8\_t \*data
    :   Rx data address of BK RLK packet

    <a id="_CPPv4N18bk_rlk_config_info2cbE"></a>

    <a id="_CPPv3N18bk_rlk_config_info2cbE"></a> <a id="_CPPv2N18bk_rlk_config_info2cbE"></a> <a id="bk_rlk_config_info::cb__voidP"></a> <a id="structbk__rlk__config__info_1a13cc61b6c9445c9e4bff127f8b943eac"></a> void \*cb
    :   callback of TX,cb has two arguments, first is args, second is tx success flag

    <a id="_CPPv4N18bk_rlk_config_info4argsE"></a>

    <a id="_CPPv3N18bk_rlk_config_info4argsE"></a> <a id="_CPPv2N18bk_rlk_config_info4argsE"></a> <a id="bk_rlk_config_info::args__voidP"></a> <a id="structbk__rlk__config__info_1a3c01db4d7d75743eea8e110e60a97611"></a> void \*args
    :   callback arguments

    <a id="_CPPv4N18bk_rlk_config_info7tx_rateE"></a>

    <a id="_CPPv3N18bk_rlk_config_info7tx_rateE"></a> <a id="_CPPv2N18bk_rlk_config_info7tx_rateE"></a> <a id="bk_rlk_config_info::tx_rate__uint32_t"></a> <a id="structbk__rlk__config__info_1a0185fdb36cf96d0e667d67451e38de86"></a> uint32\_t tx\_rate
    :   TX rate information

    <a id="_CPPv4N18bk_rlk_config_info8tx_powerE"></a>

    <a id="_CPPv3N18bk_rlk_config_info8tx_powerE"></a> <a id="_CPPv2N18bk_rlk_config_info8tx_powerE"></a> <a id="bk_rlk_config_info::tx_power__uint32_t"></a> <a id="structbk__rlk__config__info_1a3fcf5a4df9e692a3084f006b02e7186e"></a> uint32\_t tx\_power
    :   TX power information

    <a id="_CPPv4N18bk_rlk_config_info12tx_retry_cntE"></a>

    <a id="_CPPv3N18bk_rlk_config_info12tx_retry_cntE"></a> <a id="_CPPv2N18bk_rlk_config_info12tx_retry_cntE"></a> <a id="bk_rlk_config_info::tx_retry_cnt__uint32_t"></a> <a id="structbk__rlk__config__info_1a9ae2a649844ec2ae8b9752648d25c9fa"></a> uint32\_t tx\_retry\_cnt
    :   TX retry count

<a id="_CPPv416bk_rlk_recv_info"></a>

<a id="_CPPv316bk_rlk_recv_info"></a> <a id="_CPPv216bk_rlk_recv_info"></a> <a id="bk_rlk_recv_info"></a> <a id="structbk__rlk__recv__info"></a> struct bk\_rlk\_recv\_info
:   BK Raw Link(RLK) Receive packet information.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16bk_rlk_recv_info8src_addrE"></a>

    <a id="_CPPv3N16bk_rlk_recv_info8src_addrE"></a> <a id="_CPPv2N16bk_rlk_recv_info8src_addrE"></a> <a id="bk_rlk_recv_info::src_addr__uint8_tA"></a> <a id="structbk__rlk__recv__info_1a72fbac98ae1ce98888e4e0b149f7bbf9"></a> uint8\_t src\_addr\[RLK\_WIFI\_MAC\_ADDR\_LEN\]
    :   Source address of BK RLK packet

    <a id="_CPPv4N16bk_rlk_recv_info8des_addrE"></a>

    <a id="_CPPv3N16bk_rlk_recv_info8des_addrE"></a> <a id="_CPPv2N16bk_rlk_recv_info8des_addrE"></a> <a id="bk_rlk_recv_info::des_addr__uint8_tA"></a> <a id="structbk__rlk__recv__info_1a68896692aea7baba639c3c90eb596bb0"></a> uint8\_t des\_addr\[RLK\_WIFI\_MAC\_ADDR\_LEN\]
    :   Destination address of BK RLK packet

    <a id="_CPPv4N16bk_rlk_recv_info4rssiE"></a>

    <a id="_CPPv3N16bk_rlk_recv_info4rssiE"></a> <a id="_CPPv2N16bk_rlk_recv_info4rssiE"></a> <a id="bk_rlk_recv_info::rssi__i"></a> <a id="structbk__rlk__recv__info_1ae10f9421a69ce7750b78762858fefac1"></a> int rssi
    :   Rx RSSI of BK RLK packet

    <a id="_CPPv4N16bk_rlk_recv_info3lenE"></a>

    <a id="_CPPv3N16bk_rlk_recv_info3lenE"></a> <a id="_CPPv2N16bk_rlk_recv_info3lenE"></a> <a id="bk_rlk_recv_info::len__uint16_t"></a> <a id="structbk__rlk__recv__info_1ab2ed229084c9fbba3ed3ebe26b958ad2"></a> uint16\_t len
    :   Rx length of BK RLK packet

    <a id="_CPPv4N16bk_rlk_recv_info4dataE"></a>

    <a id="_CPPv3N16bk_rlk_recv_info4dataE"></a> <a id="_CPPv2N16bk_rlk_recv_info4dataE"></a> <a id="bk_rlk_recv_info::data__uint8_tP"></a> <a id="structbk__rlk__recv__info_1a495deffc2c603cc2c9f046d1406d590b"></a> uint8\_t \*data
    :   Rx data address of BK RLK packet

<a id="_CPPv425bk_rlk_scan_master_info_t"></a>

<a id="_CPPv325bk_rlk_scan_master_info_t"></a> <a id="_CPPv225bk_rlk_scan_master_info_t"></a> <a id="bk_rlk_scan_master_info_t"></a> <a id="structbk__rlk__scan__master__info__t"></a> struct bk\_rlk\_scan\_master\_info\_t
:   BK Raw Link(RLK) Scan callback information.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N25bk_rlk_scan_master_info_t4ssidE"></a>

    <a id="_CPPv3N25bk_rlk_scan_master_info_t4ssidE"></a> <a id="_CPPv2N25bk_rlk_scan_master_info_t4ssidE"></a> <a id="bk_rlk_scan_master_info_t::ssid__cA"></a> <a id="structbk__rlk__scan__master__info__t_1aa10b589b920295213fbbd1535ca77093"></a> char ssid\[BK\_RLK\_SSID\_STR\_LEN\]
    :   SSID of master found by scan

    <a id="_CPPv4N25bk_rlk_scan_master_info_t5bssidE"></a>

    <a id="_CPPv3N25bk_rlk_scan_master_info_t5bssidE"></a> <a id="_CPPv2N25bk_rlk_scan_master_info_t5bssidE"></a> <a id="bk_rlk_scan_master_info_t::bssid__uint8_tA"></a> <a id="structbk__rlk__scan__master__info__t_1a2ff9365008c415324ad8fed51173847d"></a> uint8\_t bssid\[BK\_RLK\_BSSID\_LEN\]
    :   BSSID of master found by scan

    <a id="_CPPv4N25bk_rlk_scan_master_info_t4rssiE"></a>

    <a id="_CPPv3N25bk_rlk_scan_master_info_t4rssiE"></a> <a id="_CPPv2N25bk_rlk_scan_master_info_t4rssiE"></a> <a id="bk_rlk_scan_master_info_t::rssi__i"></a> <a id="structbk__rlk__scan__master__info__t_1a18d155b288b159183e0cc16c61f8a0b3"></a> int rssi
    :   RSSI of master found by scan

    <a id="_CPPv4N25bk_rlk_scan_master_info_t7channelE"></a>

    <a id="_CPPv3N25bk_rlk_scan_master_info_t7channelE"></a> <a id="_CPPv2N25bk_rlk_scan_master_info_t7channelE"></a> <a id="bk_rlk_scan_master_info_t::channel__uint8_t"></a> <a id="structbk__rlk__scan__master__info__t_1a7dcf353efe8326795936254556f442c2"></a> uint8\_t channel
    :   The channel of the master found by scan

<a id="_CPPv420bk_rlk_scan_result_t"></a>

<a id="_CPPv320bk_rlk_scan_result_t"></a> <a id="_CPPv220bk_rlk_scan_result_t"></a> <a id="bk_rlk_scan_result_t"></a> <a id="structbk__rlk__scan__result__t"></a> struct bk\_rlk\_scan\_result\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20bk_rlk_scan_result_t10master_numE"></a>

    <a id="_CPPv3N20bk_rlk_scan_result_t10master_numE"></a> <a id="_CPPv2N20bk_rlk_scan_result_t10master_numE"></a> <a id="bk_rlk_scan_result_t::master_num__i"></a> <a id="structbk__rlk__scan__result__t_1a11f9766bafd48aaed32709654cbe2cfa"></a> int master\_num
    :   The number of master found by scan

    <a id="_CPPv4N20bk_rlk_scan_result_t7mastersE"></a>

    <a id="_CPPv3N20bk_rlk_scan_result_t7mastersE"></a> <a id="_CPPv2N20bk_rlk_scan_result_t7mastersE"></a> <a id="bk_rlk_scan_result_t::masters__bk_rlk_scan_master_info_tP"></a> <a id="structbk__rlk__scan__result__t_1a0f60f298a7ea29e07cb447370dcc9177"></a> [bk\_rlk\_scan\_master\_info\_t](#_CPPv425bk_rlk_scan_master_info_t "bk_rlk_scan_master_info_t") \*masters
    :   The master found by scan

<a id="_CPPv418bk_rlk_scan_info_t"></a>

<a id="_CPPv318bk_rlk_scan_info_t"></a> <a id="_CPPv218bk_rlk_scan_info_t"></a> <a id="bk_rlk_scan_info_t"></a> <a id="structbk__rlk__scan__info__t"></a> struct bk\_rlk\_scan\_info\_t
:   BK Raw Link(RLK) Scan mode.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_rlk_scan_info_t9scan_modeE"></a>

    <a id="_CPPv3N18bk_rlk_scan_info_t9scan_modeE"></a> <a id="_CPPv2N18bk_rlk_scan_info_t9scan_modeE"></a> <a id="bk_rlk_scan_info_t::scan_mode__bk_rlk_scan_mode_t"></a> <a id="structbk__rlk__scan__info__t_1af3eab7a7c8d5b6fd1acc29bc1e8dec31"></a> [bk\_rlk\_scan\_mode\_t](#_CPPv418bk_rlk_scan_mode_t "bk_rlk_scan_mode_t") scan\_mode
    :   The Scan mode: BK\_RLK\_ALL\_SCAN,BK\_RLK\_ONE\_SSID\_SCAN and BK\_RLK\_ONE\_BSSID\_SCAN

    <a id="_CPPv4N18bk_rlk_scan_info_t4ssidE"></a>

    <a id="_CPPv3N18bk_rlk_scan_info_t4ssidE"></a> <a id="_CPPv2N18bk_rlk_scan_info_t4ssidE"></a> <a id="bk_rlk_scan_info_t::ssid__cP"></a> <a id="structbk__rlk__scan__info__t_1ac0b6e67d0dee72a354c2a60b54017919"></a> char \*ssid
    :   The peer ssid when choose BK\_RLK\_ONE\_SSID\_SCAN mode

    <a id="_CPPv4N18bk_rlk_scan_info_t5bssidE"></a>

    <a id="_CPPv3N18bk_rlk_scan_info_t5bssidE"></a> <a id="_CPPv2N18bk_rlk_scan_info_t5bssidE"></a> <a id="bk_rlk_scan_info_t::bssid__uint8_tA"></a> <a id="structbk__rlk__scan__info__t_1a51b64282be7aaf4996e3fef5c9cfb232"></a> uint8\_t bssid\[BK\_RLK\_BSSID\_LEN\]
    :   The peer ssid when choose BK\_RLK\_ONE\_BSSID\_SCAN mode

<a id="_CPPv423bk_rlk_extra_ies_info_t"></a>

<a id="_CPPv323bk_rlk_extra_ies_info_t"></a> <a id="_CPPv223bk_rlk_extra_ies_info_t"></a> <a id="bk_rlk_extra_ies_info_t"></a> <a id="structbk__rlk__extra__ies__info__t"></a> struct bk\_rlk\_extra\_ies\_info\_t
:   BK Raw Link(RLK) set extra\_ies.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23bk_rlk_extra_ies_info_t9extra_iesE"></a>

    <a id="_CPPv3N23bk_rlk_extra_ies_info_t9extra_iesE"></a> <a id="_CPPv2N23bk_rlk_extra_ies_info_t9extra_iesE"></a> <a id="bk_rlk_extra_ies_info_t::extra_ies__uint8_tP"></a> <a id="structbk__rlk__extra__ies__info__t_1a144f2832281aaee04c9dc49fb3256028"></a> uint8\_t \*extra\_ies
    :   extra\_ies \- Extra IE(s) to add into BK-RLK scan requst and response frame

    <a id="_CPPv4N23bk_rlk_extra_ies_info_t13extra_ies_lenE"></a>

    <a id="_CPPv3N23bk_rlk_extra_ies_info_t13extra_ies_lenE"></a> <a id="_CPPv2N23bk_rlk_extra_ies_info_t13extra_ies_lenE"></a> <a id="bk_rlk_extra_ies_info_t::extra_ies_len__uint32_t"></a> <a id="structbk__rlk__extra__ies__info__t_1a1b046dead33dbf7c83f0616907ae1e71"></a> uint32\_t extra\_ies\_len
    :   extra\_ies\_len \- Length of extra\_ies in octets

<a id="_CPPv417rlk_transfer_cb_t"></a>

<a id="_CPPv317rlk_transfer_cb_t"></a> <a id="_CPPv217rlk_transfer_cb_t"></a> <a id="rlk_transfer_cb_t"></a> <a id="structrlk__transfer__cb__t"></a> struct rlk\_transfer\_cb\_t
:   BK Raw Link(RLK) transfer callback structure.

<a id="macros"></a>

### Macros

<a id="c.RLK_WIFI_MAC_ADDR_LEN"></a>

<a id="raw__link_8h_1a40bac4334b13f59544d837ba86e77398"></a> RLK\_WIFI\_MAC\_ADDR\_LEN

<a id="c.BK_RLK_SSID_STR_LEN"></a>

<a id="raw__link_8h_1a3cdcdbc84d90c6ba1f5e21a68dccbec7"></a> BK\_RLK\_SSID\_STR\_LEN

<a id="c.BK_RLK_BSSID_LEN"></a>

<a id="raw__link_8h_1a35c3245e32102d9d4afd1a798bd223a0"></a> BK\_RLK\_BSSID\_LEN

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv418bk_rlk_peer_info_t"></a>

<a id="_CPPv318bk_rlk_peer_info_t"></a> <a id="_CPPv218bk_rlk_peer_info_t"></a> <a id="bk_rlk_peer_info_t"></a> <a id="raw__link_8h_1afad89c3b88c8270496c3b60e78947fbc"></a> typedef struct [bk\_rlk\_peer\_info](#_CPPv416bk_rlk_peer_info "bk_rlk_peer_info") bk\_rlk\_peer\_info\_t
:   BK Raw Link(RLK) peer list context structure.

<a id="_CPPv420bk_rlk_config_info_t"></a>

<a id="_CPPv320bk_rlk_config_info_t"></a> <a id="_CPPv220bk_rlk_config_info_t"></a> <a id="bk_rlk_config_info_t"></a> <a id="raw__link_8h_1a648673d1ea369e4417192a417b1651f9"></a> typedef struct [bk\_rlk\_config\_info](#_CPPv418bk_rlk_config_info "bk_rlk_config_info") bk\_rlk\_config\_info\_t
:   BK Raw Link(RLK) configure tx information.

<a id="_CPPv418bk_rlk_recv_info_t"></a>

<a id="_CPPv318bk_rlk_recv_info_t"></a> <a id="_CPPv218bk_rlk_recv_info_t"></a> <a id="bk_rlk_recv_info_t"></a> <a id="raw__link_8h_1a7763eaadb1e7680987d80e0a84c76a7d"></a> typedef struct [bk\_rlk\_recv\_info](#_CPPv416bk_rlk_recv_info "bk_rlk_recv_info") bk\_rlk\_recv\_info\_t
:   BK Raw Link(RLK) Receive packet information.

<a id="_CPPv419bk_rlk_send_ex_cb_t"></a>

<a id="_CPPv319bk_rlk_send_ex_cb_t"></a> <a id="_CPPv219bk_rlk_send_ex_cb_t"></a> <a id="bk_rlk_send_ex_cb_t"></a> <a id="raw__link_8h_1a01ca7aeb79184a718e3e5c4c27f06591"></a> typedef void (\*bk\_rlk\_send\_ex\_cb\_t)(void \*args, bool status)
:   Callback function of sending BK Raw Link data.

    Param args
    :   callback arguments

    Param status
    :   status of sending BK Raw Link data (succeed or fail)

<a id="_CPPv416bk_rlk_recv_cb_t"></a>

<a id="_CPPv316bk_rlk_recv_cb_t"></a> <a id="_CPPv216bk_rlk_recv_cb_t"></a> <a id="bk_rlk_recv_cb_t"></a> <a id="raw__link_8h_1a8b7db5ed16e55fb38438a498bdc45ef5"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*bk\_rlk\_recv\_cb\_t)([bk\_rlk\_recv\_info\_t](#_CPPv418bk_rlk_recv_info_t "bk_rlk_recv_info_t") \*rx\_info)
:   Callback function of receiving BK Raw Link data.

    **Attention**
    :   bk\_rlk\_info is a local variable，it can only be used in the callback.

    Param rx\_info
    :   received BK Raw Link packet information

<a id="_CPPv416bk_rlk_send_cb_t"></a>

<a id="_CPPv316bk_rlk_send_cb_t"></a> <a id="_CPPv216bk_rlk_send_cb_t"></a> <a id="bk_rlk_send_cb_t"></a> <a id="raw__link_8h_1a8d70902cd38fc6acddc4d9a7a3ea1c40"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*bk\_rlk\_send\_cb\_t)(const uint8\_t \*peer\_mac\_addr, [bk\_rlk\_send\_status\_t](#_CPPv420bk_rlk_send_status_t "bk_rlk_send_status_t") status)
:   Callback function of sending BK Raw Link data.

    Param peer\_mac\_addr
    :   peer MAC address

    Param status
    :   status of sending BK Raw Link data (succeed or fail)

<a id="_CPPv415bk_rlk_acs_cb_t"></a>

<a id="_CPPv315bk_rlk_acs_cb_t"></a> <a id="_CPPv215bk_rlk_acs_cb_t"></a> <a id="bk_rlk_acs_cb_t"></a> <a id="raw__link_8h_1aeff497a5996518d2f87ed7820a461e74"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*bk\_rlk\_acs\_cb\_t)(const uint32\_t chanstatus\[\], uint32\_t num\_channel, uint32\_t best\_channel)
:   BK Raw Link ACS confirmation callback.

    Param chanstatus\[\]
    :   Performance status of each channel sorted in descending order

    Param num\_channel
    :   The number of support channel

    Param best\_channel
    :   The best channel obtained by BK Raw Link ACS

<a id="_CPPv416bk_rlk_scan_cb_t"></a>

<a id="_CPPv316bk_rlk_scan_cb_t"></a> <a id="_CPPv216bk_rlk_scan_cb_t"></a> <a id="bk_rlk_scan_cb_t"></a> <a id="raw__link_8h_1ac4959c03a9e4a3eb2e7181b60f290e96"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") (\*bk\_rlk\_scan\_cb\_t)([bk\_rlk\_scan\_result\_t](#_CPPv420bk_rlk_scan_result_t "bk_rlk_scan_result_t") \*result)
:   BK Raw Link SCAN confirmation callback.

    Param result
    :   The BK-RLK masters devices obtained by BK Raw Link SCAN

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv416bk_rlk_wifi_if_t"></a>

<a id="_CPPv316bk_rlk_wifi_if_t"></a> <a id="_CPPv216bk_rlk_wifi_if_t"></a> <a id="raw__link_8h_1ae87a36983c60536db80f7b7230be3e6c"></a> enum bk\_rlk\_wifi\_if\_t
:   *Values:*

    <a id="_CPPv4N16bk_rlk_wifi_if_t11WIFI_IF_STAE"></a>

    <a id="_CPPv3N16bk_rlk_wifi_if_t11WIFI_IF_STAE"></a> <a id="_CPPv2N16bk_rlk_wifi_if_t11WIFI_IF_STAE"></a> <a id="raw__link_8h_1ae87a36983c60536db80f7b7230be3e6ca0f218baecd04fc1e2283709930046621"></a> enumerator WIFI\_IF\_STA

    <a id="_CPPv4N16bk_rlk_wifi_if_t10WIFI_IF_APE"></a>

    <a id="_CPPv3N16bk_rlk_wifi_if_t10WIFI_IF_APE"></a> <a id="_CPPv2N16bk_rlk_wifi_if_t10WIFI_IF_APE"></a> <a id="raw__link_8h_1ae87a36983c60536db80f7b7230be3e6ca8aeaa3a73ec9744683b9ca4b3d2c8569"></a> enumerator WIFI\_IF\_AP

    <a id="_CPPv4N16bk_rlk_wifi_if_t15WIFI_IF_UNKNOWNE"></a>

    <a id="_CPPv3N16bk_rlk_wifi_if_t15WIFI_IF_UNKNOWNE"></a> <a id="_CPPv2N16bk_rlk_wifi_if_t15WIFI_IF_UNKNOWNE"></a> <a id="raw__link_8h_1ae87a36983c60536db80f7b7230be3e6ca2ee8dc434007f4e0f9877619c9e953f4"></a> enumerator WIFI\_IF\_UNKNOWN

<a id="_CPPv413bk_rlk_role_t"></a>

<a id="_CPPv313bk_rlk_role_t"></a> <a id="_CPPv213bk_rlk_role_t"></a> <a id="raw__link_8h_1a18b00601517cd532a3ffe841c41e7455"></a> enum bk\_rlk\_role\_t
:   *Values:*

    <a id="_CPPv4N13bk_rlk_role_t13BK_RLK_MASTERE"></a>

    <a id="_CPPv3N13bk_rlk_role_t13BK_RLK_MASTERE"></a> <a id="_CPPv2N13bk_rlk_role_t13BK_RLK_MASTERE"></a> <a id="raw__link_8h_1a18b00601517cd532a3ffe841c41e7455aec70173b9c607ab2d589330898116b0d"></a> enumerator BK\_RLK\_MASTER
    :   Master role

    <a id="_CPPv4N13bk_rlk_role_t12BK_RLK_SLAVEE"></a>

    <a id="_CPPv3N13bk_rlk_role_t12BK_RLK_SLAVEE"></a> <a id="_CPPv2N13bk_rlk_role_t12BK_RLK_SLAVEE"></a> <a id="raw__link_8h_1a18b00601517cd532a3ffe841c41e7455a60805dcaac46c674247521fb6d055b38"></a> enumerator BK\_RLK\_SLAVE
    :   Slave role

    <a id="_CPPv4N13bk_rlk_role_t12BK_RLK_DUBIDE"></a>

    <a id="_CPPv3N13bk_rlk_role_t12BK_RLK_DUBIDE"></a> <a id="_CPPv2N13bk_rlk_role_t12BK_RLK_DUBIDE"></a> <a id="raw__link_8h_1a18b00601517cd532a3ffe841c41e7455a4a5db9f49398e108593d49e1beabec8b"></a> enumerator BK\_RLK\_DUBID
    :   Double identity role

    <a id="_CPPv4N13bk_rlk_role_t11BK_RLK_IDLEE"></a>

    <a id="_CPPv3N13bk_rlk_role_t11BK_RLK_IDLEE"></a> <a id="_CPPv2N13bk_rlk_role_t11BK_RLK_IDLEE"></a> <a id="raw__link_8h_1a18b00601517cd532a3ffe841c41e7455ad19aeb9bf1cc2c923de4065cd7ea984e"></a> enumerator BK\_RLK\_IDLE
    :   No role can be not transmission data

<a id="_CPPv421bk_rlk_mac_hdr_type_t"></a>

<a id="_CPPv321bk_rlk_mac_hdr_type_t"></a> <a id="_CPPv221bk_rlk_mac_hdr_type_t"></a> <a id="raw__link_8h_1af176c85db96de81cc3b8846e5ba22da6"></a> enum bk\_rlk\_mac\_hdr\_type\_t
:   *Values:*

    <a id="_CPPv4N21bk_rlk_mac_hdr_type_t26WIFI_MAC_HDR_TYPE_ASSOCREQE"></a>

    <a id="_CPPv3N21bk_rlk_mac_hdr_type_t26WIFI_MAC_HDR_TYPE_ASSOCREQE"></a> <a id="_CPPv2N21bk_rlk_mac_hdr_type_t26WIFI_MAC_HDR_TYPE_ASSOCREQE"></a> <a id="raw__link_8h_1af176c85db96de81cc3b8846e5ba22da6a7cc593f18873ae4193d93064a9da89b0"></a> enumerator WIFI\_MAC\_HDR\_TYPE\_ASSOCREQ

    <a id="_CPPv4N21bk_rlk_mac_hdr_type_t26WIFI_MAC_HDR_TYPE_ASSOCRESE"></a>

    <a id="_CPPv3N21bk_rlk_mac_hdr_type_t26WIFI_MAC_HDR_TYPE_ASSOCRESE"></a> <a id="_CPPv2N21bk_rlk_mac_hdr_type_t26WIFI_MAC_HDR_TYPE_ASSOCRESE"></a> <a id="raw__link_8h_1af176c85db96de81cc3b8846e5ba22da6af7203aa1b76b189fb58b1ac27787722e"></a> enumerator WIFI\_MAC\_HDR\_TYPE\_ASSOCRES

    <a id="_CPPv4N21bk_rlk_mac_hdr_type_t22WIFI_MAC_HDR_TYPE_AUTHE"></a>

    <a id="_CPPv3N21bk_rlk_mac_hdr_type_t22WIFI_MAC_HDR_TYPE_AUTHE"></a> <a id="_CPPv2N21bk_rlk_mac_hdr_type_t22WIFI_MAC_HDR_TYPE_AUTHE"></a> <a id="raw__link_8h_1af176c85db96de81cc3b8846e5ba22da6afdc983f5cf78517342a89b5d03f2ebd6"></a> enumerator WIFI\_MAC\_HDR\_TYPE\_AUTH

    <a id="_CPPv4N21bk_rlk_mac_hdr_type_t24WIFI_MAC_HDR_TYPE_ACTIONE"></a>

    <a id="_CPPv3N21bk_rlk_mac_hdr_type_t24WIFI_MAC_HDR_TYPE_ACTIONE"></a> <a id="_CPPv2N21bk_rlk_mac_hdr_type_t24WIFI_MAC_HDR_TYPE_ACTIONE"></a> <a id="raw__link_8h_1af176c85db96de81cc3b8846e5ba22da6aa66c69996206d79ec4a6293c47e41c24"></a> enumerator WIFI\_MAC\_HDR\_TYPE\_ACTION

<a id="_CPPv418bk_rlk_scan_mode_t"></a>

<a id="_CPPv318bk_rlk_scan_mode_t"></a> <a id="_CPPv218bk_rlk_scan_mode_t"></a> <a id="raw__link_8h_1abcbcb4d4bbbc879971624e1ad859ff57"></a> enum bk\_rlk\_scan\_mode\_t
:   *Values:*

    <a id="_CPPv4N18bk_rlk_scan_mode_t15BK_RLK_ALL_SCANE"></a>

    <a id="_CPPv3N18bk_rlk_scan_mode_t15BK_RLK_ALL_SCANE"></a> <a id="_CPPv2N18bk_rlk_scan_mode_t15BK_RLK_ALL_SCANE"></a> <a id="raw__link_8h_1abcbcb4d4bbbc879971624e1ad859ff57a79fa9a6596129cb53277f4b1c6cd5c84"></a> enumerator BK\_RLK\_ALL\_SCAN
    :   BK-RLK SCAN all BK-RLK device

    <a id="_CPPv4N18bk_rlk_scan_mode_t20BK_RLK_ONE_SSID_SCANE"></a>

    <a id="_CPPv3N18bk_rlk_scan_mode_t20BK_RLK_ONE_SSID_SCANE"></a> <a id="_CPPv2N18bk_rlk_scan_mode_t20BK_RLK_ONE_SSID_SCANE"></a> <a id="raw__link_8h_1abcbcb4d4bbbc879971624e1ad859ff57a31e1ce5c48e6970fa22e8674e4afb53c"></a> enumerator BK\_RLK\_ONE\_SSID\_SCAN
    :   BK-RLK ONE SCAN that used SSID method

    <a id="_CPPv4N18bk_rlk_scan_mode_t21BK_RLK_ONE_BSSID_SCANE"></a>

    <a id="_CPPv3N18bk_rlk_scan_mode_t21BK_RLK_ONE_BSSID_SCANE"></a> <a id="_CPPv2N18bk_rlk_scan_mode_t21BK_RLK_ONE_BSSID_SCANE"></a> <a id="raw__link_8h_1abcbcb4d4bbbc879971624e1ad859ff57a6024dafbed4e47e11c26423c5de35cfd"></a> enumerator BK\_RLK\_ONE\_BSSID\_SCAN
    :   BK-RLK ONE SCAN that used BSSID method

<a id="_CPPv420bk_rlk_send_status_t"></a>

<a id="_CPPv320bk_rlk_send_status_t"></a> <a id="_CPPv220bk_rlk_send_status_t"></a> <a id="raw__link_8h_1a99ff581b789693bafbfc6e3ebedcbae2"></a> enum bk\_rlk\_send\_status\_t
:   Status of sending BK Raw Link data .

    *Values:*

    <a id="_CPPv4N20bk_rlk_send_status_t16BK_RLK_SEND_FAILE"></a>

    <a id="_CPPv3N20bk_rlk_send_status_t16BK_RLK_SEND_FAILE"></a> <a id="_CPPv2N20bk_rlk_send_status_t16BK_RLK_SEND_FAILE"></a> <a id="raw__link_8h_1a99ff581b789693bafbfc6e3ebedcbae2a954c3780964ad6c9d6a904e3da4798f8"></a> enumerator BK\_RLK\_SEND\_FAIL
    :   Send BK Raw Link data fail

    <a id="_CPPv4N20bk_rlk_send_status_t19BK_RLK_SEND_SUCCESSE"></a>

    <a id="_CPPv3N20bk_rlk_send_status_t19BK_RLK_SEND_SUCCESSE"></a> <a id="_CPPv2N20bk_rlk_send_status_t19BK_RLK_SEND_SUCCESSE"></a> <a id="raw__link_8h_1a99ff581b789693bafbfc6e3ebedcbae2ad78bb164d89b10ff7da7e7cffa84b319"></a> enumerator BK\_RLK\_SEND\_SUCCESS
    :   Send BK Raw Link data successfully
