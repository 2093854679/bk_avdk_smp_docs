---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/bluetooth/service.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="profile"></a>

# Profile 服务

<a id="id1"></a>

## 概述

Bluetooth Service Layer 是 AP 侧 `bk_bluetooth` 组件中的上层封装，位于
`ap/components/bk_bluetooth/service/dm`。它基于 Bluetooth SDK API 实现常见业务流程，
例如连接管理、自动重连、音频链路控制、AVRCP 控制和 HFP HF 操作。

重要

Service Layer 面向常见蓝牙业务场景提供组合封装；底层能力和精细化控制可继续参考
`ap/include/components/bluetooth` 下的 Bluetooth SDK API。

<a id="id2"></a>

## 整体结构

Service Layer 由若干 profile service 和公共管理模块组成：

- BT manager：统一管理 BT 配对、可发现/可连接状态、自动重连和 profile 连接回调。
- A2DP Sink service：提供蓝牙音频 Sink 场景的连接管理、媒体数据事件和 codec 能力封装。
- AVRCP CT/TG service：提供播放器控制、曲目信息查询和绝对音量通知等 AVRCP 流程封装。
- HFP HF service：提供免提通话、SCO 音频、音量和 AT 命令交互封装。
- BLE GATT framework：提供 BLE GAP、GATTS、GATTC 和连接上下文管理封装。
- PAN/HIDD service：提供 PAN 网络接入和 HID 设备 demo 相关封装。

Bluetooth Mesh 使用独立的 Zephyr v2.7.6 Bluetooth Host/Mesh 组件，源码位于
`ap/components/bk_bluetooth/service/mesh`，示例工程为 `projects/bluetooth/mesh`。
该工程不属于 `service/dm` 封装层，应用侧通过 Zephyr Mesh API 和 `ble_mesh` CLI 演示配网与模型控制流程。

<a id="id3"></a>

## 源码位置

- `ap/components/bk_bluetooth/service/dm/bt_manager`：BT manager。
- `ap/components/bk_bluetooth/service/dm/a2dp`：A2DP Sink service 和音频数据处理。
- `ap/components/bk_bluetooth/service/dm/avrcp`：AVRCP CT/TG service。
- `ap/components/bk_bluetooth/service/dm/hfp`：HFP HF service 和 SCO 音频处理。
- `ap/components/bk_bluetooth/service/dm/ble/gatt`：BLE GATT framework。
- `ap/components/bk_bluetooth/service/dm/ble/hogpd`：HID-over-GATT keyboard demo。
- `ap/components/bk_bluetooth/service/dm/ble/bap`：LE Audio BAP API 封装（unicast / broadcast）。
- `ap/components/bk_bluetooth/service/dm/bk_pan`：PAN/HIDD service。
- `ap/components/bk_bluetooth/service/dm/storage`：蓝牙配对信息和 BLE bond 信息存储。
- `ap/components/bk_bluetooth/service/dm/utils`：ring buffer、LATM parser 等公共工具。

<a id="id4"></a>

## 宏配置

Service Layer 的编译由 Bluetooth、Profile、音频、网络和 CLI 配置共同决定：

- `CONFIG_BLUETOOTH_AP`：启用 AP 侧 Bluetooth 组件。
- `CONFIG_BLUETOOTH_HOST_ONLY`：启用 AP 侧 Bluetooth host。
- `CONFIG_BT`：启用 BR/EDR，包括 A2DP、AVRCP、HFP、PAN、HID 等 BT profile 能力。
- `CONFIG_BLE`：启用 BLE。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE`：启用 BTDM service 组件。开启后编译 BT manager、storage、A2DP Sink、AVRCP CT/TG、HFP HF 等 service。
- `CONFIG_AUDIO_PLAY`：启用 A2DP/HFP 音频播放相关处理，例如 `a2dp_sink_audio.c` 和 `hfp_hf_audio.c`。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATT`：启用 BLE GATT framework。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_USE_STORAGE`：控制 GATT 是否使用 `bluetooth_storage` 保存 bond 信息。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATTS_TEST_ATTR`：启用 GATTS 测试属性表。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATT_LOG_LEVEL`：配置 GATT framework 日志等级。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_HOGPD`：启用 HID-over-GATT keyboard demo。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_HOGPD_LOG_LEVEL`：配置 HOGPD demo 日志等级。
- `CONFIG_BLE_LE_AUDIO`：启用 LE Audio BAP API，并链接双模 Ethermind LE Audio host 库；`projects/bluetooth/le_audio/` 下各工程需开启。
- `CONFIG_BLE_MESH_ZEPHYR`：启用 Zephyr Bluetooth Mesh Host 组件；`projects/bluetooth/mesh` 工程需开启。
- `CONFIG_NET_PAN`：启用 PAN 网络 service。
- `CONFIG_CLI`：启用 BLE GATT、PAN、HOGPD 等 demo CLI 命令。

<a id="bt-manager"></a>

## BT Manager

BT manager 负责统一处理 BT 工作模式、配对状态、自动重连和 profile 回调注册。A2DP、
AVRCP、HFP、PAN 等 service 会通过 BT manager 协同连接和断开流程。

API 参考：

<a id="header-file"></a>

### Header File

- [bt\_manager.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/bt_manager/bt_manager.h)

<a id="functions"></a>

### Functions

<a id="_CPPv428bt_manager_register_callbackP14btm_callback_s"></a>

<a id="_CPPv328bt_manager_register_callbackP14btm_callback_s"></a> <a id="_CPPv228bt_manager_register_callbackP14btm_callback_s"></a> <a id="bt_manager_register_callback__btm_callback_sP"></a> <a id="bt__manager_8h_1a51dd280bad8e2aeedeb4f0ef4d40382d"></a> int bt\_manager\_register\_callback([btm\_callback\_s](#_CPPv414btm_callback_s "btm_callback_s") \*cb)
:   Register callback functions for the Bluetooth manager.

    参数
    :   **cb** – Pointer to the callback structure.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv426bt_manager_start_reconnectP7uint8_t7uint8_t"></a>

<a id="_CPPv326bt_manager_start_reconnectP7uint8_t7uint8_t"></a> <a id="_CPPv226bt_manager_start_reconnectP7uint8_t7uint8_t"></a> <a id="bt_manager_start_reconnect__uint8_tP.uint8_t"></a> <a id="bt__manager_8h_1af1b32a73463acad6ccad32f9db85a6bc"></a> void bt\_manager\_start\_reconnect(uint8\_t \*addr, uint8\_t immediate)
:   Start the reconnection process to a specified device.

    参数
    :   - **addr** – Pointer to the address of the device to reconnect to.
        - **immediate** – Whether to initiate the reconnection immediately.

<a id="_CPPv419bt_manager_set_mode7uint8_t"></a>

<a id="_CPPv319bt_manager_set_mode7uint8_t"></a> <a id="_CPPv219bt_manager_set_mode7uint8_t"></a> <a id="bt_manager_set_mode__uint8_t"></a> <a id="bt__manager_8h_1ab46879b59f772290a4940d0ef6761a3d"></a> void bt\_manager\_set\_mode(uint8\_t mode)
:   Set the operation mode of the Bluetooth manager.

    参数
    :   **mode** – The mode to set.

<a id="_CPPv419bt_manager_get_modev"></a>

<a id="_CPPv319bt_manager_get_modev"></a> <a id="_CPPv219bt_manager_get_modev"></a> <a id="bt_manager_get_mode__void"></a> <a id="bt__manager_8h_1a680795cb921c74857b85250f6d19916c"></a> uint8\_t bt\_manager\_get\_mode(void)
:   Get the current operation mode of the Bluetooth manager.

    返回
    :   The current operation mode.

<a id="_CPPv415bt_manager_initPK16bt_manager_cfg_t"></a>

<a id="_CPPv315bt_manager_initPK16bt_manager_cfg_t"></a> <a id="_CPPv215bt_manager_initPK16bt_manager_cfg_t"></a> <a id="bt_manager_init__bt_manager_cfg_tCP"></a> <a id="bt__manager_8h_1af330c44d24940ce760049bb4f15e9a44"></a> int bt\_manager\_init(const [bt\_manager\_cfg\_t](#_CPPv416bt_manager_cfg_t "bt_manager_cfg_t") \*cfg)
:   Initialize the Bluetooth manager.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv417bt_manager_deinitv"></a>

<a id="_CPPv317bt_manager_deinitv"></a> <a id="_CPPv217bt_manager_deinitv"></a> <a id="bt_manager_deinit__void"></a> <a id="bt__manager_8h_1a807b6eb9b56db06c86d436558e282e2e"></a> int bt\_manager\_deinit(void)
:   Deinitialize the Bluetooth manager.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv428bt_manager_get_connect_statev"></a>

<a id="_CPPv328bt_manager_get_connect_statev"></a> <a id="_CPPv228bt_manager_get_connect_statev"></a> <a id="bt_manager_get_connect_state__void"></a> <a id="bt__manager_8h_1a42d200bbc3376c9ad8984c015e213905"></a> uint8\_t bt\_manager\_get\_connect\_state(void)
:   Get the current connection state of the Bluetooth manager.

    返回
    :   The current connection state.

<a id="_CPPv428bt_manager_set_connect_state7uint8_t"></a>

<a id="_CPPv328bt_manager_set_connect_state7uint8_t"></a> <a id="_CPPv228bt_manager_set_connect_state7uint8_t"></a> <a id="bt_manager_set_connect_state__uint8_t"></a> <a id="bt__manager_8h_1a6021b125db046eb5c9e8b3813b070b5b"></a> void bt\_manager\_set\_connect\_state(uint8\_t state)
:   Set the current connection state of the Bluetooth manager.

    参数
    :   **state** – The connection state to set.

<a id="_CPPv431bt_manager_get_reconnect_deviceP7uint8_t"></a>

<a id="_CPPv331bt_manager_get_reconnect_deviceP7uint8_t"></a> <a id="_CPPv231bt_manager_get_reconnect_deviceP7uint8_t"></a> <a id="bt_manager_get_reconnect_device__uint8_tP"></a> <a id="bt__manager_8h_1ad82efd8e097bb3058b53560761384a13"></a> void bt\_manager\_get\_reconnect\_device(uint8\_t \*addr)
:   Get the address of the device to reconnect to.

    参数
    :   **addr** – Pointer to store the address of the device to reconnect to.

<a id="_CPPv431bt_manager_get_connected_devicev"></a>

<a id="_CPPv331bt_manager_get_connected_devicev"></a> <a id="_CPPv231bt_manager_get_connected_devicev"></a> <a id="bt_manager_get_connected_device__void"></a> <a id="bt__manager_8h_1af1b51c9c4946e391fee291992ca79863"></a> uint8\_t \*bt\_manager\_get\_connected\_device(void)
:   Get the address of the currently connected device.

    返回
    :   Pointer to the address of the currently connected device.

<a id="_CPPv430bt_manager_unregister_callback7uint8_t"></a>

<a id="_CPPv330bt_manager_unregister_callback7uint8_t"></a> <a id="_CPPv230bt_manager_unregister_callback7uint8_t"></a> <a id="bt_manager_unregister_callback__uint8_t"></a> <a id="bt__manager_8h_1a1c1abbcd8e691d842ee31326a06f78c0"></a> int bt\_manager\_unregister\_callback(uint8\_t index)
:   Unregister a callback function by index.

    参数
    :   **index** – The index of the callback to unregister.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv424bk_bt_enter_pairing_mode7uint8_t"></a>

<a id="_CPPv324bk_bt_enter_pairing_mode7uint8_t"></a> <a id="_CPPv224bk_bt_enter_pairing_mode7uint8_t"></a> <a id="bk_bt_enter_pairing_mode__uint8_t"></a> <a id="bt__manager_8h_1acb7cfc53199c42a20d6c4d9e4fa9c422"></a> void bk\_bt\_enter\_pairing\_mode(uint8\_t is\_visible)
:   Enter the Bluetooth pairing mode.

<a id="_CPPv421bt_manager_clean_bondv"></a>

<a id="_CPPv321bt_manager_clean_bondv"></a> <a id="_CPPv221bt_manager_clean_bondv"></a> <a id="bt_manager_clean_bond__void"></a> <a id="bt__manager_8h_1aa985d038fab9b30b7995644224a858da"></a> void bt\_manager\_clean\_bond(void)
:   Clean the bonded devices.

<a id="_CPPv428bt_manager_save_ctkd_linkkeyP7uint8_tP7uint8_t"></a>

<a id="_CPPv328bt_manager_save_ctkd_linkkeyP7uint8_tP7uint8_t"></a> <a id="_CPPv228bt_manager_save_ctkd_linkkeyP7uint8_tP7uint8_t"></a> <a id="bt_manager_save_ctkd_linkkey__uint8_tP.uint8_tP"></a> <a id="bt__manager_8h_1a3abd14a5511df9774ecfd2f29f477228"></a> int bt\_manager\_save\_ctkd\_linkkey(uint8\_t \*addr, uint8\_t \*linkkey)
:   Save the CTKD linkkey.

    参数
    :   - **addr** – Pointer to the address of the device.
        - **linkkey** – Pointer to the linkkey.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv437bt_manager_set_auto_accept_connection7uint8_t7uint8_t"></a>

<a id="_CPPv337bt_manager_set_auto_accept_connection7uint8_t7uint8_t"></a> <a id="_CPPv237bt_manager_set_auto_accept_connection7uint8_t7uint8_t"></a> <a id="bt_manager_set_auto_accept_connection__uint8_t.uint8_t"></a> <a id="bt__manager_8h_1a2f245b5ba63572cfb1d623342c1a6469"></a> void bt\_manager\_set\_auto\_accept\_connection(uint8\_t type, uint8\_t accept)
:   Set the auto accept connection.

    参数
    :   - **type** – The type of the connection.
        - **accept** – The accept state.

<a id="_CPPv431bt_manager_clear_reconnect_infov"></a>

<a id="_CPPv331bt_manager_clear_reconnect_infov"></a> <a id="_CPPv231bt_manager_clear_reconnect_infov"></a> <a id="bt_manager_clear_reconnect_info__void"></a> <a id="bt__manager_8h_1ae16fd168db30577dc5cdf77b69071e42"></a> void bt\_manager\_clear\_reconnect\_info(void)
:   Clear the reconnect information.

<a id="_CPPv422bt_manager_discover_bt8uint32_t8uint32_t"></a>

<a id="_CPPv322bt_manager_discover_bt8uint32_t8uint32_t"></a> <a id="_CPPv222bt_manager_discover_bt8uint32_t8uint32_t"></a> <a id="bt_manager_discover_bt__uint32_t.uint32_t"></a> <a id="bt__manager_8h_1a7bf08ea4c11207790edd793d5c434c56"></a> int bt\_manager\_discover\_bt(uint32\_t sec, uint32\_t num\_report)
:   Start Classic Bluetooth device discovery (inquiry).

    Inquiry results are delivered as BK\_BT\_GAP\_DISC\_RES\_EVT to the GAP callbacks registered via bt\_manager\_register\_callback().

    参数
    :   - **sec** – Inquiry duration in seconds.
        - **num\_report** – Max number of responses to report (0 \= unlimited; capped at 255).

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv429bt_manager_cancel_discover_btv"></a>

<a id="_CPPv329bt_manager_cancel_discover_btv"></a> <a id="_CPPv229bt_manager_cancel_discover_btv"></a> <a id="bt_manager_cancel_discover_bt__void"></a> <a id="bt__manager_8h_1a3caf8f74fdc628edef9b46c6951d51f1"></a> int bt\_manager\_cancel\_discover\_bt(void)
:   Cancel an ongoing Classic Bluetooth device discovery.

    返回
    :   0 on success, otherwise error code.

<a id="structures"></a>

### Structures

<a id="_CPPv414btm_callback_s"></a>

<a id="_CPPv314btm_callback_s"></a> <a id="_CPPv214btm_callback_s"></a> <a id="btm_callback_s"></a> <a id="structbtm__callback__s"></a> struct btm\_callback\_s
:   Structure for Bluetooth manager callbacks.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14btm_callback_s6gap_cbE"></a>

    <a id="_CPPv3N14btm_callback_s6gap_cbE"></a> <a id="_CPPv2N14btm_callback_s6gap_cbE"></a> <a id="btm_callback_s::gap_cb__btm_gap_event_cb"></a> <a id="structbtm__callback__s_1a15db5a0d3b33d257ad9e792022889631"></a> [btm\_gap\_event\_cb](#_CPPv416btm_gap_event_cb "btm_gap_event_cb") gap\_cb
    :   GAP event callback function.

    <a id="_CPPv4N14btm_callback_s16start_connect_cbE"></a>

    <a id="_CPPv3N14btm_callback_s16start_connect_cbE"></a> <a id="_CPPv2N14btm_callback_s16start_connect_cbE"></a> <a id="btm_callback_s::start_connect_cb__btm_start_profile_connect_cb"></a> <a id="structbtm__callback__s_1a6a677565715a39a2ec1cf943d2fdac60"></a> [btm\_start\_profile\_connect\_cb](#_CPPv428btm_start_profile_connect_cb "btm_start_profile_connect_cb") start\_connect\_cb
    :   Callback for starting profile connection.

    <a id="_CPPv4N14btm_callback_s15stop_connect_cbE"></a>

    <a id="_CPPv3N14btm_callback_s15stop_connect_cbE"></a> <a id="_CPPv2N14btm_callback_s15stop_connect_cbE"></a> <a id="btm_callback_s::stop_connect_cb__btm_stop_profile_connect_cb"></a> <a id="structbtm__callback__s_1ab0b87e2ffc3233a083f4425e5436d572"></a> [btm\_stop\_profile\_connect\_cb](#_CPPv427btm_stop_profile_connect_cb "btm_stop_profile_connect_cb") stop\_connect\_cb
    :   Callback for stopping profile connection.

    <a id="_CPPv4N14btm_callback_s19start_disconnect_cbE"></a>

    <a id="_CPPv3N14btm_callback_s19start_disconnect_cbE"></a> <a id="_CPPv2N14btm_callback_s19start_disconnect_cbE"></a> <a id="btm_callback_s::start_disconnect_cb__btm_start_profile_disconnect_cb"></a> <a id="structbtm__callback__s_1a4361305ecfd728e2e5431f561c99f304"></a> [btm\_start\_profile\_disconnect\_cb](#_CPPv431btm_start_profile_disconnect_cb "btm_start_profile_disconnect_cb") start\_disconnect\_cb
    :   Callback for starting profile disconnection.

    <a id="_CPPv4N14btm_callback_s17reconnect_fail_cbE"></a>

    <a id="_CPPv3N14btm_callback_s17reconnect_fail_cbE"></a> <a id="_CPPv2N14btm_callback_s17reconnect_fail_cbE"></a> <a id="btm_callback_s::reconnect_fail_cb__btm_reconnect_fail_cb"></a> <a id="structbtm__callback__s_1ae109a9396a606b767dfeae08224f7019"></a> [btm\_reconnect\_fail\_cb](#_CPPv421btm_reconnect_fail_cb "btm_reconnect_fail_cb") reconnect\_fail\_cb
    :   Callback for reconnect failure.

<a id="_CPPv416bt_manager_cfg_t"></a>

<a id="_CPPv316bt_manager_cfg_t"></a> <a id="_CPPv216bt_manager_cfg_t"></a> <a id="bt_manager_cfg_t"></a> <a id="structbt__manager__cfg__t"></a> struct bt\_manager\_cfg\_t
:   Bluetooth manager initialization configuration.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16bt_manager_cfg_t10local_nameE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t10local_nameE"></a> <a id="_CPPv2N16bt_manager_cfg_t10local_nameE"></a> <a id="bt_manager_cfg_t::local_name__cCP"></a> <a id="structbt__manager__cfg__t_1af99c6fef84f9b66cd869c9fa482a1d3c"></a> const char \*local\_name
    :   Complete local Bluetooth name.

    <a id="_CPPv4N16bt_manager_cfg_t12device_classE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t12device_classE"></a> <a id="_CPPv2N16bt_manager_cfg_t12device_classE"></a> <a id="bt_manager_cfg_t::device_class__uint32_t"></a> <a id="structbt__manager__cfg__t_1af8b3fc28f5ebd9602e2c78bc5e7a4757"></a> uint32\_t device\_class
    :   Bluetooth class of device. If 0, the component default is used.

    <a id="_CPPv4N16bt_manager_cfg_t18page_scan_intervalE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t18page_scan_intervalE"></a> <a id="_CPPv2N16bt_manager_cfg_t18page_scan_intervalE"></a> <a id="bt_manager_cfg_t::page_scan_interval__uint16_t"></a> <a id="structbt__manager__cfg__t_1a19b0b4324738fad540b42a8f16232c83"></a> uint16\_t page\_scan\_interval
    :   Page scan interval. If 0, the component default is used.

    <a id="_CPPv4N16bt_manager_cfg_t16page_scan_windowE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t16page_scan_windowE"></a> <a id="_CPPv2N16bt_manager_cfg_t16page_scan_windowE"></a> <a id="bt_manager_cfg_t::page_scan_window__uint16_t"></a> <a id="structbt__manager__cfg__t_1a0fefad4b48e1048d6448f81f9b0db5df"></a> uint16\_t page\_scan\_window
    :   Page scan window. If 0, the component default is used.

    <a id="_CPPv4N16bt_manager_cfg_t12page_timeoutE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t12page_timeoutE"></a> <a id="_CPPv2N16bt_manager_cfg_t12page_timeoutE"></a> <a id="bt_manager_cfg_t::page_timeout__uint16_t"></a> <a id="structbt__manager__cfg__t_1a83bf4f51068464ac8cfea99f314878b9"></a> uint16\_t page\_timeout
    :   Page timeout in 0.625 ms units. If 0, the component default is used.

    <a id="_CPPv4N16bt_manager_cfg_t21reconnect_interval_msE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t21reconnect_interval_msE"></a> <a id="_CPPv2N16bt_manager_cfg_t21reconnect_interval_msE"></a> <a id="bt_manager_cfg_t::reconnect_interval_ms__uint32_t"></a> <a id="structbt__manager__cfg__t_1a16cb275821cca0ced3b206213ebd78fc"></a> uint32\_t reconnect\_interval\_ms
    :   Reconnect interval in ms. If 0, the component default is used.

    <a id="_CPPv4N16bt_manager_cfg_t19max_reconnect_countE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t19max_reconnect_countE"></a> <a id="_CPPv2N16bt_manager_cfg_t19max_reconnect_countE"></a> <a id="bt_manager_cfg_t::max_reconnect_count__uint8_t"></a> <a id="structbt__manager__cfg__t_1a1610c5f3f69aba83a16bbc030848edf4"></a> uint8\_t max\_reconnect\_count
    :   Max reconnect attempts. If 0, the component default is used.

    <a id="_CPPv4N16bt_manager_cfg_t13io_capabilityE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t13io_capabilityE"></a> <a id="_CPPv2N16bt_manager_cfg_t13io_capabilityE"></a> <a id="bt_manager_cfg_t::io_capability__uint8_t"></a> <a id="structbt__manager__cfg__t_1a7fe957a224cd1c6793996d443c115e49"></a> uint8\_t io\_capability
    :   GAP IO capability. If 0xff, the component default is used.

    <a id="_CPPv4N16bt_manager_cfg_t12authreq_modeE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t12authreq_modeE"></a> <a id="_CPPv2N16bt_manager_cfg_t12authreq_modeE"></a> <a id="bt_manager_cfg_t::authreq_mode__uint8_t"></a> <a id="structbt__manager__cfg__t_1ac9a5f5927ed19d970988c5672bf13706"></a> uint8\_t authreq\_mode
    :   SSP authentication requirements (0x01\~0x05). If 0, the component default is used.

    <a id="_CPPv4N16bt_manager_cfg_t4roleE"></a>

    <a id="_CPPv3N16bt_manager_cfg_t4roleE"></a> <a id="_CPPv2N16bt_manager_cfg_t4roleE"></a> <a id="bt_manager_cfg_t::role__uint8_t"></a> <a id="structbt__manager__cfg__t_1a1d7c482cdc1b06857d849242ad46d361"></a> uint8\_t role
    :   Link role applied after ACL is up: 0 \= keep stack role (slave for headset/sink, default), 1 \= master (A2DP source), 2 \= slave.

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv416btm_gap_event_cb"></a>

<a id="_CPPv316btm_gap_event_cb"></a> <a id="_CPPv216btm_gap_event_cb"></a> <a id="btm_gap_event_cb"></a> <a id="bt__manager_8h_1a898bc8189df1c853082fa380e72f5e92"></a> typedef void (\*btm\_gap\_event\_cb)([bk\_gap\_bt\_cb\_event\_t](dual_bt.md#_CPPv420bk_gap_bt_cb_event_t "bk_gap_bt_cb_event_t") event, [bk\_bt\_gap\_cb\_param\_t](dual_bt.md#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t") \*param)
:   Callback function type for GAP (Generic Access Profile) events.

    Param event
    :   The GAP event type.

    Param param
    :   Pointer to the GAP callback parameter structure.

<a id="_CPPv428btm_start_profile_connect_cb"></a>

<a id="_CPPv328btm_start_profile_connect_cb"></a> <a id="_CPPv228btm_start_profile_connect_cb"></a> <a id="btm_start_profile_connect_cb"></a> <a id="bt__manager_8h_1ac5f11528d4387fcdfa4b4c31c4c0d5c6"></a> typedef void (\*btm\_start\_profile\_connect\_cb)(uint8\_t \*remote\_addr)
:   Callback function type for starting profile connection.

    Param remote\_addr
    :   Pointer to the remote device address.

<a id="_CPPv431btm_start_profile_disconnect_cb"></a>

<a id="_CPPv331btm_start_profile_disconnect_cb"></a> <a id="_CPPv231btm_start_profile_disconnect_cb"></a> <a id="btm_start_profile_disconnect_cb"></a> <a id="bt__manager_8h_1a172aae613c15618eeb6ba75395f29e99"></a> typedef void (\*btm\_start\_profile\_disconnect\_cb)(uint8\_t \*remote\_addr)
:   Callback function type for starting profile disconnection.

    Param remote\_addr
    :   Pointer to the remote device address.

<a id="_CPPv427btm_stop_profile_connect_cb"></a>

<a id="_CPPv327btm_stop_profile_connect_cb"></a> <a id="_CPPv227btm_stop_profile_connect_cb"></a> <a id="btm_stop_profile_connect_cb"></a> <a id="bt__manager_8h_1a77a6e8f09293dfe99296fc92dcac5d1a"></a> typedef void (\*btm\_stop\_profile\_connect\_cb)(void)
:   Callback function type for stopping profile connection.

<a id="_CPPv421btm_reconnect_fail_cb"></a>

<a id="_CPPv321btm_reconnect_fail_cb"></a> <a id="_CPPv221btm_reconnect_fail_cb"></a> <a id="btm_reconnect_fail_cb"></a> <a id="bt__manager_8h_1a7445a9e4c6917b66ccc3a34d041ca905"></a> typedef void (\*btm\_reconnect\_fail\_cb)(void)
:   Callback function type for reconnect failure.

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv4Ut2_56"></a>

<a id="_CPPv3Ut2_56"></a> <a id="bt__manager_8h_1ac9420823bfeba78fce625fc105e3b01d"></a> enum \[anonymous\]
:   Enumeration of Bluetooth manager operation modes.

    *Values:*

    <a id="_CPPv4NUt2_5619BT_MNG_MODE_PAIRINGE"></a>

    <a id="_CPPv3NUt2_5619BT_MNG_MODE_PAIRINGE"></a> <a id="bt__manager_8h_1ac9420823bfeba78fce625fc105e3b01dad0d7447d563469ae09ad20ff80cd5386"></a> enumerator BT\_MNG\_MODE\_PAIRING
    :   connectable and discoverable

    <a id="_CPPv4NUt2_5624BT_MNG_MODE_RECONNECTINGE"></a>

    <a id="_CPPv3NUt2_5624BT_MNG_MODE_RECONNECTINGE"></a> <a id="bt__manager_8h_1ac9420823bfeba78fce625fc105e3b01da42b296733defaf911db2953e8dd2dc53"></a> enumerator BT\_MNG\_MODE\_RECONNECTING
    :   no-connectable and no-discoverable

    <a id="_CPPv4NUt2_5622BT_MNG_MODE_CONNECTEEDE"></a>

    <a id="_CPPv3NUt2_5622BT_MNG_MODE_CONNECTEEDE"></a> <a id="bt__manager_8h_1ac9420823bfeba78fce625fc105e3b01daff7104fc9d8934e0b863039da932b2b6"></a> enumerator BT\_MNG\_MODE\_CONNECTEED
    :   no-connectable and no-discoverable

    <a id="_CPPv4NUt2_5623BT_MNG_MODE_CONNECTABLEE"></a>

    <a id="_CPPv3NUt2_5623BT_MNG_MODE_CONNECTABLEE"></a> <a id="bt__manager_8h_1ac9420823bfeba78fce625fc105e3b01daf824a506e58240d198ff5b5ab0b1b2ec"></a> enumerator BT\_MNG\_MODE\_CONNECTABLE
    :   connectable and no-discoverable

    <a id="_CPPv4NUt2_5616BT_MNG_MODE_IDLEE"></a>

    <a id="_CPPv3NUt2_5616BT_MNG_MODE_IDLEE"></a> <a id="bt__manager_8h_1ac9420823bfeba78fce625fc105e3b01daccc24e0dbc2bb59296359585469179e2"></a> enumerator BT\_MNG\_MODE\_IDLE
    :   no-connectable and no-discoverable

    <a id="_CPPv4NUt2_5629BT_MNG_MODE_DISCOVERABLE_ONLYE"></a>

    <a id="_CPPv3NUt2_5629BT_MNG_MODE_DISCOVERABLE_ONLYE"></a> <a id="bt__manager_8h_1ac9420823bfeba78fce625fc105e3b01dabeff69d1e7287631f65b13ff80112cd2"></a> enumerator BT\_MNG\_MODE\_DISCOVERABLE\_ONLY
    :   no-connectable and discoverable

    <a id="_CPPv4NUt2_5619BT_MNG_MODE_ALL_OFFE"></a>

    <a id="_CPPv3NUt2_5619BT_MNG_MODE_ALL_OFFE"></a> <a id="bt__manager_8h_1ac9420823bfeba78fce625fc105e3b01da0359824052d470d38a3413fe58d4207e"></a> enumerator BT\_MNG\_MODE\_ALL\_OFF
    :   no-connectable and no-discoverable

<a id="_CPPv4Ut2_57"></a>

<a id="_CPPv3Ut2_57"></a> <a id="bt__manager_8h_1afa9be5679ab03d785820f2474c5ccc6e"></a> enum \[anonymous\]
:   Enumeration of Bluetooth connection states.

    *Values:*

    <a id="_CPPv4NUt2_5713BT_STATE_IDLEE"></a>

    <a id="_CPPv3NUt2_5713BT_STATE_IDLEE"></a> <a id="bt__manager_8h_1afa9be5679ab03d785820f2474c5ccc6eaa980786e228b58789cce8629b821b6fa"></a> enumerator BT\_STATE\_IDLE
    :   Bluetooth is in idle state.

    <a id="_CPPv4NUt2_5727BT_STATE_WAIT_FOR_RECONNECTE"></a>

    <a id="_CPPv3NUt2_5727BT_STATE_WAIT_FOR_RECONNECTE"></a> <a id="bt__manager_8h_1afa9be5679ab03d785820f2474c5ccc6eafc0b84d52360b4385bd36e571434d130"></a> enumerator BT\_STATE\_WAIT\_FOR\_RECONNECT
    :   Waiting to initiate a reconnection.

    <a id="_CPPv4NUt2_5721BT_STATE_RECONNECTINGE"></a>

    <a id="_CPPv3NUt2_5721BT_STATE_RECONNECTINGE"></a> <a id="bt__manager_8h_1afa9be5679ab03d785820f2474c5ccc6ea7fdd3326f76638ad728776cf9c563c5a"></a> enumerator BT\_STATE\_RECONNECTING
    :   Currently in the process of reconnecting.

    <a id="_CPPv4NUt2_5723BT_STATE_LINK_CONNECTEDE"></a>

    <a id="_CPPv3NUt2_5723BT_STATE_LINK_CONNECTEDE"></a> <a id="bt__manager_8h_1afa9be5679ab03d785820f2474c5ccc6ea930e5efca490d4c203522fa8340158f1"></a> enumerator BT\_STATE\_LINK\_CONNECTED
    :   The link layer is connected.

    <a id="_CPPv4NUt2_5726BT_STATE_PROFILE_CONNECTEDE"></a>

    <a id="_CPPv3NUt2_5726BT_STATE_PROFILE_CONNECTEDE"></a> <a id="bt__manager_8h_1afa9be5679ab03d785820f2474c5ccc6ea957a36a998670efc3a2b63931f6b93b6"></a> enumerator BT\_STATE\_PROFILE\_CONNECTED
    :   The profile is connected.

    <a id="_CPPv4NUt2_5720BT_STATE_KEY_MISSINGE"></a>

    <a id="_CPPv3NUt2_5720BT_STATE_KEY_MISSINGE"></a> <a id="bt__manager_8h_1afa9be5679ab03d785820f2474c5ccc6eaf3f7170ea581187c24e78ef5f17e9ccf"></a> enumerator BT\_STATE\_KEY\_MISSING
    :   The encryption key is missing.

<a id="_CPPv4Ut2_58"></a>

<a id="_CPPv3Ut2_58"></a> <a id="bt__manager_8h_1ae6dceca96ec2c7a1b4aa211264a87ef6"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt2_5818PAIRING_STATE_IDLEE"></a>

    <a id="_CPPv3NUt2_5818PAIRING_STATE_IDLEE"></a> <a id="bt__manager_8h_1ae6dceca96ec2c7a1b4aa211264a87ef6abc5f4b55e1b6a21c7939d6e93ef5216e"></a> enumerator PAIRING\_STATE\_IDLE

    <a id="_CPPv4NUt2_5825PAIRING_STATE_PREPARATIONE"></a>

    <a id="_CPPv3NUt2_5825PAIRING_STATE_PREPARATIONE"></a> <a id="bt__manager_8h_1ae6dceca96ec2c7a1b4aa211264a87ef6afd84e29a40c0c5f352a816a0ee1fe22a"></a> enumerator PAIRING\_STATE\_PREPARATION

    <a id="_CPPv4NUt2_5822PAIRING_STATE_WAIT_CFME"></a>

    <a id="_CPPv3NUt2_5822PAIRING_STATE_WAIT_CFME"></a> <a id="bt__manager_8h_1ae6dceca96ec2c7a1b4aa211264a87ef6a1b34398584c07ad6b2c4484edf7daf69"></a> enumerator PAIRING\_STATE\_WAIT\_CFM

<a id="_CPPv4Ut2_59"></a>

<a id="_CPPv3Ut2_59"></a> <a id="bt__manager_8h_1a56a0f36da7f9eaaf54bd05cc2bf49173"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt2_5933BT_MNG_AUTO_ACCEPT_CONNECTION_ACLE"></a>

    <a id="_CPPv3NUt2_5933BT_MNG_AUTO_ACCEPT_CONNECTION_ACLE"></a> <a id="bt__manager_8h_1a56a0f36da7f9eaaf54bd05cc2bf49173a655a776d0e8c6cfe14093c5a966d5d11"></a> enumerator BT\_MNG\_AUTO\_ACCEPT\_CONNECTION\_ACL

    <a id="_CPPv4NUt2_5933BT_MNG_AUTO_ACCEPT_CONNECTION_SCOE"></a>

    <a id="_CPPv3NUt2_5933BT_MNG_AUTO_ACCEPT_CONNECTION_SCOE"></a> <a id="bt__manager_8h_1a56a0f36da7f9eaaf54bd05cc2bf49173aecb8ac6c5a8afaf77b2d45322e497d16"></a> enumerator BT\_MNG\_AUTO\_ACCEPT\_CONNECTION\_SCO

<a id="a2dp-sink-service"></a>

## A2DP Sink Service

A2DP Sink service 封装蓝牙音频 Sink 流程，包括 profile 初始化、连接控制、音频配置事件、
媒体数据事件和可选 AAC 支持。

API 参考：

<a id="id5"></a>

### Header File

- [bk\_a2dp\_sink\_service.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/a2dp/bk_a2dp_sink_service.h)

<a id="id6"></a>

### Functions

<a id="_CPPv430bk_a2dp_sink_register_event_cb23bk_a2dp_sink_event_cb_tPv"></a>

<a id="_CPPv330bk_a2dp_sink_register_event_cb23bk_a2dp_sink_event_cb_tPv"></a> <a id="_CPPv230bk_a2dp_sink_register_event_cb23bk_a2dp_sink_event_cb_tPv"></a> <a id="bk_a2dp_sink_register_event_cb__bk_a2dp_sink_event_cb_t.voidP"></a> <a id="bk__a2dp__sink__service_8h_1ac6551e08247760a6409ef4dba1c437e9"></a> int bk\_a2dp\_sink\_register\_event\_cb([bk\_a2dp\_sink\_event\_cb\_t](#_CPPv423bk_a2dp_sink_event_cb_t "bk_a2dp_sink_event_cb_t") cb, void \*user\_data)
:   Register the application event callback. Call before service init.

<a id="_CPPv425bk_a2dp_sink_service_initPK18bk_a2dp_sink_cfg_t"></a>

<a id="_CPPv325bk_a2dp_sink_service_initPK18bk_a2dp_sink_cfg_t"></a> <a id="_CPPv225bk_a2dp_sink_service_initPK18bk_a2dp_sink_cfg_t"></a> <a id="bk_a2dp_sink_service_init__bk_a2dp_sink_cfg_tCP"></a> <a id="bk__a2dp__sink__service_8h_1a00335365b5e8291874611463a73aafeb"></a> int bk\_a2dp\_sink\_service\_init(const [bk\_a2dp\_sink\_cfg\_t](#_CPPv418bk_a2dp_sink_cfg_t "bk_a2dp_sink_cfg_t") \*cfg)
:   Initialize A2DP sink profile and register internal Bluetooth callbacks.

<a id="_CPPv427bk_a2dp_sink_service_deinitv"></a>

<a id="_CPPv327bk_a2dp_sink_service_deinitv"></a> <a id="_CPPv227bk_a2dp_sink_service_deinitv"></a> <a id="bk_a2dp_sink_service_deinit__void"></a> <a id="bk__a2dp__sink__service_8h_1a9b692dacbeaca28fd3057284ae7076b8"></a> int bk\_a2dp\_sink\_service\_deinit(void)
:   Deinitialize A2DP sink profile and release service resources.

<a id="_CPPv420bk_a2dp_sink_connectAL6E_K7uint8_t"></a>

<a id="_CPPv320bk_a2dp_sink_connectAL6E_K7uint8_t"></a> <a id="_CPPv220bk_a2dp_sink_connectA6_K7uint8_t"></a> <a id="bk_a2dp_sink_connect__uint8_tCA"></a> <a id="bk__a2dp__sink__service_8h_1a030f1a174845b5134667533e5ab18713"></a> int bk\_a2dp\_sink\_connect(const uint8\_t bda\[6\])
:   Connect A2DP sink to the specified remote device.

<a id="_CPPv423bk_a2dp_sink_disconnectAL6E_K7uint8_t"></a>

<a id="_CPPv323bk_a2dp_sink_disconnectAL6E_K7uint8_t"></a> <a id="_CPPv223bk_a2dp_sink_disconnectA6_K7uint8_t"></a> <a id="bk_a2dp_sink_disconnect__uint8_tCA"></a> <a id="bk__a2dp__sink__service_8h_1a3b42a843a0bb11e2ff1e95b15c5e365c"></a> int bk\_a2dp\_sink\_disconnect(const uint8\_t bda\[6\])
:   Disconnect A2DP sink from the specified remote device.

<a id="id7"></a>

### Structures

<a id="_CPPv419bk_a2dp_sink_conn_t"></a>

<a id="_CPPv319bk_a2dp_sink_conn_t"></a> <a id="_CPPv219bk_a2dp_sink_conn_t"></a> <a id="bk_a2dp_sink_conn_t"></a> <a id="structbk__a2dp__sink__conn__t"></a> struct bk\_a2dp\_sink\_conn\_t
:   A2DP connection event payload.

<a id="_CPPv420bk_a2dp_media_data_t"></a>

<a id="_CPPv320bk_a2dp_media_data_t"></a> <a id="_CPPv220bk_a2dp_media_data_t"></a> <a id="bk_a2dp_media_data_t"></a> <a id="structbk__a2dp__media__data__t"></a> struct bk\_a2dp\_media\_data\_t
:   Media packet payload. The buffer is only valid during the event callback.

<a id="_CPPv418bk_a2dp_sink_cfg_t"></a>

<a id="_CPPv318bk_a2dp_sink_cfg_t"></a> <a id="_CPPv218bk_a2dp_sink_cfg_t"></a> <a id="bk_a2dp_sink_cfg_t"></a> <a id="structbk__a2dp__sink__cfg__t"></a> struct bk\_a2dp\_sink\_cfg\_t
:   A2DP sink service configuration.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_a2dp_sink_cfg_t13aac_supportedE"></a>

    <a id="_CPPv3N18bk_a2dp_sink_cfg_t13aac_supportedE"></a> <a id="_CPPv2N18bk_a2dp_sink_cfg_t13aac_supportedE"></a> <a id="bk_a2dp_sink_cfg_t::aac_supported__uint8_t"></a> <a id="structbk__a2dp__sink__cfg__t_1ad7107498644beb15dded034bf3ffe419"></a> uint8\_t aac\_supported
    :   Non-zero to advertise AAC support in addition to SBC.

    <a id="_CPPv4N18bk_a2dp_sink_cfg_t16auto_accept_connE"></a>

    <a id="_CPPv3N18bk_a2dp_sink_cfg_t16auto_accept_connE"></a> <a id="_CPPv2N18bk_a2dp_sink_cfg_t16auto_accept_connE"></a> <a id="bk_a2dp_sink_cfg_t::auto_accept_conn__uint8_t"></a> <a id="structbk__a2dp__sink__cfg__t_1ab4262788d3afcd77a583c63e773c4ff3"></a> uint8\_t auto\_accept\_conn
    :   Non-zero to accept or reconnect incoming devices automatically.

<a id="id8"></a>

### Type Definitions

<a id="_CPPv423bk_a2dp_sink_event_cb_t"></a>

<a id="_CPPv323bk_a2dp_sink_event_cb_t"></a> <a id="_CPPv223bk_a2dp_sink_event_cb_t"></a> <a id="bk_a2dp_sink_event_cb_t"></a> <a id="bk__a2dp__sink__service_8h_1a4691e0ffec501bdaf65a2e667689042e"></a> typedef void (\*bk\_a2dp\_sink\_event\_cb\_t)([bk\_a2dp\_sink\_evt\_t](#_CPPv418bk_a2dp_sink_evt_t "bk_a2dp_sink_evt_t") evt, void \*arg, void \*user\_data)
:   A2DP sink service event callback.

    The callback is invoked from the Bluetooth stack/service context. Copy data before posting it to another task if it must live beyond the callback.

<a id="id9"></a>

### Enumerations

<a id="_CPPv418bk_a2dp_sink_evt_t"></a>

<a id="_CPPv318bk_a2dp_sink_evt_t"></a> <a id="_CPPv218bk_a2dp_sink_evt_t"></a> <a id="bk__a2dp__sink__service_8h_1a87d5e5450086b0d3293d3ea546c917d2"></a> enum bk\_a2dp\_sink\_evt\_t
:   *Values:*

    <a id="_CPPv4N18bk_a2dp_sink_evt_t26BK_A2DP_SINK_EVT_CONNECTEDE"></a>

    <a id="_CPPv3N18bk_a2dp_sink_evt_t26BK_A2DP_SINK_EVT_CONNECTEDE"></a> <a id="_CPPv2N18bk_a2dp_sink_evt_t26BK_A2DP_SINK_EVT_CONNECTEDE"></a> <a id="bk__a2dp__sink__service_8h_1a87d5e5450086b0d3293d3ea546c917d2a897b5edad94adc5dceb9c4211eb74ffb"></a> enumerator BK\_A2DP\_SINK\_EVT\_CONNECTED
    :   arg: [bk\_a2dp\_sink\_conn\_t](#structbk__a2dp__sink__conn__t) \*

    <a id="_CPPv4N18bk_a2dp_sink_evt_t29BK_A2DP_SINK_EVT_DISCONNECTEDE"></a>

    <a id="_CPPv3N18bk_a2dp_sink_evt_t29BK_A2DP_SINK_EVT_DISCONNECTEDE"></a> <a id="_CPPv2N18bk_a2dp_sink_evt_t29BK_A2DP_SINK_EVT_DISCONNECTEDE"></a> <a id="bk__a2dp__sink__service_8h_1a87d5e5450086b0d3293d3ea546c917d2a116f845c10c49361c9c5419ddbec03ee"></a> enumerator BK\_A2DP\_SINK\_EVT\_DISCONNECTED
    :   arg: [bk\_a2dp\_sink\_conn\_t](#structbk__a2dp__sink__conn__t) \*

    <a id="_CPPv4N18bk_a2dp_sink_evt_t26BK_A2DP_SINK_EVT_AUDIO_CFGE"></a>

    <a id="_CPPv3N18bk_a2dp_sink_evt_t26BK_A2DP_SINK_EVT_AUDIO_CFGE"></a> <a id="_CPPv2N18bk_a2dp_sink_evt_t26BK_A2DP_SINK_EVT_AUDIO_CFGE"></a> <a id="bk__a2dp__sink__service_8h_1a87d5e5450086b0d3293d3ea546c917d2ad088ded582fe516807801577daf2c55b"></a> enumerator BK\_A2DP\_SINK\_EVT\_AUDIO\_CFG
    :   arg: [bk\_a2dp\_mcc\_t](dual_bt.md#structbk__a2dp__mcc__t) \*

    <a id="_CPPv4N18bk_a2dp_sink_evt_t29BK_A2DP_SINK_EVT_STREAM_STARTE"></a>

    <a id="_CPPv3N18bk_a2dp_sink_evt_t29BK_A2DP_SINK_EVT_STREAM_STARTE"></a> <a id="_CPPv2N18bk_a2dp_sink_evt_t29BK_A2DP_SINK_EVT_STREAM_STARTE"></a> <a id="bk__a2dp__sink__service_8h_1a87d5e5450086b0d3293d3ea546c917d2a88ea81ee951e1828e99f9e2b6588bb03"></a> enumerator BK\_A2DP\_SINK\_EVT\_STREAM\_START
    :   arg: [bk\_a2dp\_mcc\_t](dual_bt.md#structbk__a2dp__mcc__t) \*

    <a id="_CPPv4N18bk_a2dp_sink_evt_t31BK_A2DP_SINK_EVT_STREAM_SUSPENDE"></a>

    <a id="_CPPv3N18bk_a2dp_sink_evt_t31BK_A2DP_SINK_EVT_STREAM_SUSPENDE"></a> <a id="_CPPv2N18bk_a2dp_sink_evt_t31BK_A2DP_SINK_EVT_STREAM_SUSPENDE"></a> <a id="bk__a2dp__sink__service_8h_1a87d5e5450086b0d3293d3ea546c917d2af55b45bfb34b49590e8fbd643c32a567"></a> enumerator BK\_A2DP\_SINK\_EVT\_STREAM\_SUSPEND
    :   arg: NULL

    <a id="_CPPv4N18bk_a2dp_sink_evt_t27BK_A2DP_SINK_EVT_MEDIA_DATAE"></a>

    <a id="_CPPv3N18bk_a2dp_sink_evt_t27BK_A2DP_SINK_EVT_MEDIA_DATAE"></a> <a id="_CPPv2N18bk_a2dp_sink_evt_t27BK_A2DP_SINK_EVT_MEDIA_DATAE"></a> <a id="bk__a2dp__sink__service_8h_1a87d5e5450086b0d3293d3ea546c917d2a85f6fd6d89572849e558756bd06f167c"></a> enumerator BK\_A2DP\_SINK\_EVT\_MEDIA\_DATA
    :   arg: [bk\_a2dp\_media\_data\_t](#structbk__a2dp__media__data__t) \*

<a id="_CPPv420bk_a2dp_sink_codec_t"></a>

<a id="_CPPv320bk_a2dp_sink_codec_t"></a> <a id="_CPPv220bk_a2dp_sink_codec_t"></a> <a id="bk__a2dp__sink__service_8h_1ae55cfaa90aed7f291b2fd51a3dea5ab9"></a> enum bk\_a2dp\_sink\_codec\_t
:   Codec capabilities exposed by the sink service.

    *Values:*

    <a id="_CPPv4N20bk_a2dp_sink_codec_t22BK_A2DP_SINK_CODEC_SBCE"></a>

    <a id="_CPPv3N20bk_a2dp_sink_codec_t22BK_A2DP_SINK_CODEC_SBCE"></a> <a id="_CPPv2N20bk_a2dp_sink_codec_t22BK_A2DP_SINK_CODEC_SBCE"></a> <a id="bk__a2dp__sink__service_8h_1ae55cfaa90aed7f291b2fd51a3dea5ab9a8065a53bf0cd6b2d24ef10686796033f"></a> enumerator BK\_A2DP\_SINK\_CODEC\_SBC

    <a id="_CPPv4N20bk_a2dp_sink_codec_t22BK_A2DP_SINK_CODEC_AACE"></a>

    <a id="_CPPv3N20bk_a2dp_sink_codec_t22BK_A2DP_SINK_CODEC_AACE"></a> <a id="_CPPv2N20bk_a2dp_sink_codec_t22BK_A2DP_SINK_CODEC_AACE"></a> <a id="bk__a2dp__sink__service_8h_1ae55cfaa90aed7f291b2fd51a3dea5ab9a92ea4f9e2ed4b5991c7449b35e4d83ed"></a> enumerator BK\_A2DP\_SINK\_CODEC\_AAC

关键配置：

- `CONFIG_BT`：启用 BT。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE`：启用 A2DP Sink service 编译。
- `CONFIG_AUDIO_PLAY`：启用音频播放路径，用于媒体数据输出。

<a id="avrcp-ct-tg-service"></a>

## AVRCP CT/TG Service

AVRCP service 分为 Controller 和 Target 两个角色。Controller 侧用于播放控制、音量按键、
曲目信息查询等；Target 侧用于绝对音量通知和本地音量状态管理。

API 参考：

<a id="id10"></a>

### Header File

- [bk\_avrcp\_ct\_service.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/avrcp/bk_avrcp_ct_service.h)

<a id="id11"></a>

### Functions

<a id="_CPPv429bk_avrcp_ct_register_event_cb22bk_avrcp_ct_event_cb_tPv"></a>

<a id="_CPPv329bk_avrcp_ct_register_event_cb22bk_avrcp_ct_event_cb_tPv"></a> <a id="_CPPv229bk_avrcp_ct_register_event_cb22bk_avrcp_ct_event_cb_tPv"></a> <a id="bk_avrcp_ct_register_event_cb__bk_avrcp_ct_event_cb_t.voidP"></a> <a id="bk__avrcp__ct__service_8h_1a6c20c91340c37f214dce02af3d5a2b5f"></a> int bk\_avrcp\_ct\_register\_event\_cb([bk\_avrcp\_ct\_event\_cb\_t](#_CPPv422bk_avrcp_ct_event_cb_t "bk_avrcp_ct_event_cb_t") cb, void \*user\_data)
:   Register the application CT event callback. Call before service init.

<a id="_CPPv424bk_avrcp_ct_service_initPK17bk_avrcp_ct_cfg_t"></a>

<a id="_CPPv324bk_avrcp_ct_service_initPK17bk_avrcp_ct_cfg_t"></a> <a id="_CPPv224bk_avrcp_ct_service_initPK17bk_avrcp_ct_cfg_t"></a> <a id="bk_avrcp_ct_service_init__bk_avrcp_ct_cfg_tCP"></a> <a id="bk__avrcp__ct__service_8h_1a04b9c294745b4ec6d3c8ea575ceca032"></a> int bk\_avrcp\_ct\_service\_init(const [bk\_avrcp\_ct\_cfg\_t](#_CPPv417bk_avrcp_ct_cfg_t "bk_avrcp_ct_cfg_t") \*cfg)
:   Initialize AVRCP controller role and internal state.

<a id="_CPPv426bk_avrcp_ct_service_deinitv"></a>

<a id="_CPPv326bk_avrcp_ct_service_deinitv"></a> <a id="_CPPv226bk_avrcp_ct_service_deinitv"></a> <a id="bk_avrcp_ct_service_deinit__void"></a> <a id="bk__avrcp__ct__service_8h_1abbe5dd10e261f33629c92f18484a0363"></a> int bk\_avrcp\_ct\_service\_deinit(void)
:   Deinitialize AVRCP controller role and release resources.

<a id="_CPPv437bk_avrcp_ct_service_notify_a2dp_state7uint8_tAL6E_K7uint8_t"></a>

<a id="_CPPv337bk_avrcp_ct_service_notify_a2dp_state7uint8_tAL6E_K7uint8_t"></a> <a id="_CPPv237bk_avrcp_ct_service_notify_a2dp_state7uint8_tA6_K7uint8_t"></a> <a id="bk_avrcp_ct_service_notify_a2dp_state__uint8_t.uint8_tCA"></a> <a id="bk__avrcp__ct__service_8h_1a6edb550e3b219972aafc0966e48d701e"></a> void bk\_avrcp\_ct\_service\_notify\_a2dp\_state(uint8\_t connected, const uint8\_t bda\[6\])
:   Notify CT service of A2DP connection state for optional AVRCP auto-connect.

<a id="_CPPv423bk_avrcp_stop_reconnectv"></a>

<a id="_CPPv323bk_avrcp_stop_reconnectv"></a> <a id="_CPPv223bk_avrcp_stop_reconnectv"></a> <a id="bk_avrcp_stop_reconnect__void"></a> <a id="bk__avrcp__ct__service_8h_1a200e65b58afdf7ca06fdeb9cbb5f7c90"></a> int bk\_avrcp\_stop\_reconnect(void)
:   Stop the pending AVRCP controller auto-connect timer, if any.

<a id="_CPPv419bk_avrcp_ct_connectAL6E_K7uint8_t"></a>

<a id="_CPPv319bk_avrcp_ct_connectAL6E_K7uint8_t"></a> <a id="_CPPv219bk_avrcp_ct_connectA6_K7uint8_t"></a> <a id="bk_avrcp_ct_connect__uint8_tCA"></a> <a id="bk__avrcp__ct__service_8h_1a01c6906b50975db3aa3ff1d9c7f18c91"></a> int bk\_avrcp\_ct\_connect(const uint8\_t bda\[6\])
:   Connect AVRCP controller to the specified remote device.

<a id="_CPPv422bk_avrcp_ct_disconnectAL6E_K7uint8_t"></a>

<a id="_CPPv322bk_avrcp_ct_disconnectAL6E_K7uint8_t"></a> <a id="_CPPv222bk_avrcp_ct_disconnectA6_K7uint8_t"></a> <a id="bk_avrcp_ct_disconnect__uint8_tCA"></a> <a id="bk__avrcp__ct__service_8h_1a2d04176c4d3cf23305daf38288f69dad"></a> int bk\_avrcp\_ct\_disconnect(const uint8\_t bda\[6\])
:   Disconnect AVRCP controller from the specified remote device.

<a id="_CPPv424bk_avrcp_ct_is_connectedv"></a>

<a id="_CPPv324bk_avrcp_ct_is_connectedv"></a> <a id="_CPPv224bk_avrcp_ct_is_connectedv"></a> <a id="bk_avrcp_ct_is_connected__void"></a> <a id="bk__avrcp__ct__service_8h_1a7cbc62628656d1f1180220ae00103886"></a> int bk\_avrcp\_ct\_is\_connected(void)
:   Return non-zero when AVRCP controller is connected.

<a id="_CPPv416bk_avrcp_ct_playv"></a>

<a id="_CPPv316bk_avrcp_ct_playv"></a> <a id="_CPPv216bk_avrcp_ct_playv"></a> <a id="bk_avrcp_ct_play__void"></a> <a id="bk__avrcp__ct__service_8h_1a393338826377b5e015c1065df1b0b64a"></a> int bk\_avrcp\_ct\_play(void)
:   Send AVRCP play passthrough command.

<a id="_CPPv417bk_avrcp_ct_pausev"></a>

<a id="_CPPv317bk_avrcp_ct_pausev"></a> <a id="_CPPv217bk_avrcp_ct_pausev"></a> <a id="bk_avrcp_ct_pause__void"></a> <a id="bk__avrcp__ct__service_8h_1abac9bf6b0e9a338e779bef44877e0353"></a> int bk\_avrcp\_ct\_pause(void)
:   Send AVRCP pause passthrough command.

<a id="_CPPv416bk_avrcp_ct_nextv"></a>

<a id="_CPPv316bk_avrcp_ct_nextv"></a> <a id="_CPPv216bk_avrcp_ct_nextv"></a> <a id="bk_avrcp_ct_next__void"></a> <a id="bk__avrcp__ct__service_8h_1a1e0a44e03d73363ef6d1bb1fe7abce6f"></a> int bk\_avrcp\_ct\_next(void)
:   Send AVRCP next-track passthrough command.

<a id="_CPPv416bk_avrcp_ct_prevv"></a>

<a id="_CPPv316bk_avrcp_ct_prevv"></a> <a id="_CPPv216bk_avrcp_ct_prevv"></a> <a id="bk_avrcp_ct_prev__void"></a> <a id="bk__avrcp__ct__service_8h_1a954b56123b113e1fe1895479bbb2465d"></a> int bk\_avrcp\_ct\_prev(void)
:   Send AVRCP previous-track passthrough command.

<a id="_CPPv418bk_avrcp_ct_rewind8uint32_t"></a>

<a id="_CPPv318bk_avrcp_ct_rewind8uint32_t"></a> <a id="_CPPv218bk_avrcp_ct_rewind8uint32_t"></a> <a id="bk_avrcp_ct_rewind__uint32_t"></a> <a id="bk__avrcp__ct__service_8h_1a6dc15fac2d44984222436dec917c0fb2"></a> int bk\_avrcp\_ct\_rewind(uint32\_t ms)
:   Send AVRCP rewind command for the requested duration in milliseconds.

<a id="_CPPv424bk_avrcp_ct_fast_forward8uint32_t"></a>

<a id="_CPPv324bk_avrcp_ct_fast_forward8uint32_t"></a> <a id="_CPPv224bk_avrcp_ct_fast_forward8uint32_t"></a> <a id="bk_avrcp_ct_fast_forward__uint32_t"></a> <a id="bk__avrcp__ct__service_8h_1a58513e3623a781a3b91b9cef7fe29943"></a> int bk\_avrcp\_ct\_fast\_forward(uint32\_t ms)
:   Send AVRCP fast-forward command for the requested duration in milliseconds.

<a id="_CPPv418bk_avrcp_ct_vol_upv"></a>

<a id="_CPPv318bk_avrcp_ct_vol_upv"></a> <a id="_CPPv218bk_avrcp_ct_vol_upv"></a> <a id="bk_avrcp_ct_vol_up__void"></a> <a id="bk__avrcp__ct__service_8h_1a55f51264015590d77309fa5ee3a33862"></a> int bk\_avrcp\_ct\_vol\_up(void)
:   Increase local volume and notify/send passthrough according to peer support.

<a id="_CPPv420bk_avrcp_ct_vol_downv"></a>

<a id="_CPPv320bk_avrcp_ct_vol_downv"></a> <a id="_CPPv220bk_avrcp_ct_vol_downv"></a> <a id="bk_avrcp_ct_vol_down__void"></a> <a id="bk__avrcp__ct__service_8h_1a16d06ff0fcbd4f5bd3d6be0f15c823fd"></a> int bk\_avrcp\_ct\_vol\_down(void)
:   Decrease local volume and notify/send passthrough according to peer support.

<a id="_CPPv420bk_avrcp_ct_get_attr8uint32_t"></a>

<a id="_CPPv320bk_avrcp_ct_get_attr8uint32_t"></a> <a id="_CPPv220bk_avrcp_ct_get_attr8uint32_t"></a> <a id="bk_avrcp_ct_get_attr__uint32_t"></a> <a id="bk__avrcp__ct__service_8h_1abf7d904023794820dfa2d710557db950"></a> int bk\_avrcp\_ct\_get\_attr(uint32\_t attr\_id)
:   Request media element attributes. Pass 0 to request the default title attr.

<a id="_CPPv432bk_avrcp_ct_send_absolute_volume7uint8_t"></a>

<a id="_CPPv332bk_avrcp_ct_send_absolute_volume7uint8_t"></a> <a id="_CPPv232bk_avrcp_ct_send_absolute_volume7uint8_t"></a> <a id="bk_avrcp_ct_send_absolute_volume__uint8_t"></a> <a id="bk__avrcp__ct__service_8h_1a0b6728ad34e54a9a051c73d9e5c87bb7"></a> int bk\_avrcp\_ct\_send\_absolute\_volume(uint8\_t vol\_0\_7f)
:   Send an absolute volume (0x00-0x7f) to the peer (remote\_volume\_mode).

<a id="id12"></a>

### Structures

<a id="_CPPv425bk_avrcp_ct_abs_vol_rsp_t"></a>

<a id="_CPPv325bk_avrcp_ct_abs_vol_rsp_t"></a> <a id="_CPPv225bk_avrcp_ct_abs_vol_rsp_t"></a> <a id="bk_avrcp_ct_abs_vol_rsp_t"></a> <a id="structbk__avrcp__ct__abs__vol__rsp__t"></a> struct bk\_avrcp\_ct\_abs\_vol\_rsp\_t
:   Result of a set-absolute-volume command sent to the peer.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N25bk_avrcp_ct_abs_vol_rsp_t6statusE"></a>

    <a id="_CPPv3N25bk_avrcp_ct_abs_vol_rsp_t6statusE"></a> <a id="_CPPv2N25bk_avrcp_ct_abs_vol_rsp_t6statusE"></a> <a id="bk_avrcp_ct_abs_vol_rsp_t::status__uint8_t"></a> <a id="structbk__avrcp__ct__abs__vol__rsp__t_1a4376762d7f02172ca7f02a4b8cc49ac6"></a> uint8\_t status
    :   0 on success, non-zero when the peer rejected/failed the request.

    <a id="_CPPv4N25bk_avrcp_ct_abs_vol_rsp_t6volumeE"></a>

    <a id="_CPPv3N25bk_avrcp_ct_abs_vol_rsp_t6volumeE"></a> <a id="_CPPv2N25bk_avrcp_ct_abs_vol_rsp_t6volumeE"></a> <a id="bk_avrcp_ct_abs_vol_rsp_t::volume__uint8_t"></a> <a id="structbk__avrcp__ct__abs__vol__rsp__t_1adbf45b3ae30bbef10140778ccf13d97e"></a> uint8\_t volume
    :   Volume echoed back by the peer, in the 0x00-0x7f range.

<a id="_CPPv417bk_avrcp_ct_cfg_t"></a>

<a id="_CPPv317bk_avrcp_ct_cfg_t"></a> <a id="_CPPv217bk_avrcp_ct_cfg_t"></a> <a id="bk_avrcp_ct_cfg_t"></a> <a id="structbk__avrcp__ct__cfg__t"></a> struct bk\_avrcp\_ct\_cfg\_t
:   AVRCP controller service configuration.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_avrcp_ct_cfg_t26auto_ct_connect_after_a2dpE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_cfg_t26auto_ct_connect_after_a2dpE"></a> <a id="_CPPv2N17bk_avrcp_ct_cfg_t26auto_ct_connect_after_a2dpE"></a> <a id="bk_avrcp_ct_cfg_t::auto_ct_connect_after_a2dp__uint8_t"></a> <a id="structbk__avrcp__ct__cfg__t_1aa221c02439f908bd5dd9db74f0da2503"></a> uint8\_t auto\_ct\_connect\_after\_a2dp
    :   Non-zero to auto-connect CT after A2DP connects.

    <a id="_CPPv4N17bk_avrcp_ct_cfg_t18remote_volume_modeE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_cfg_t18remote_volume_modeE"></a> <a id="_CPPv2N17bk_avrcp_ct_cfg_t18remote_volume_modeE"></a> <a id="bk_avrcp_ct_cfg_t::remote_volume_mode__uint8_t"></a> <a id="structbk__avrcp__ct__cfg__t_1a6fb8edaebaeb1ce0d51e84461cac8b7d"></a> uint8\_t remote\_volume\_mode
    :   0: media-control controller (headset \- registers PLAY\_STATUS/TRACK/POS and drives remote media, default). 1: remote-volume controller (A2DP source \- registers peer VOLUME/BATTERY and sends absolute volume to the peer).

<a id="id13"></a>

### Type Definitions

<a id="_CPPv422bk_avrcp_ct_event_cb_t"></a>

<a id="_CPPv322bk_avrcp_ct_event_cb_t"></a> <a id="_CPPv222bk_avrcp_ct_event_cb_t"></a> <a id="bk_avrcp_ct_event_cb_t"></a> <a id="bk__avrcp__ct__service_8h_1abbe1707abf095df7b9b2dad6006dab33"></a> typedef void (\*bk\_avrcp\_ct\_event\_cb\_t)([bk\_avrcp\_ct\_evt\_t](#_CPPv417bk_avrcp_ct_evt_t "bk_avrcp_ct_evt_t") evt, void \*arg, void \*user\_data)
:   AVRCP controller event callback.

<a id="id14"></a>

### Enumerations

<a id="_CPPv417bk_avrcp_ct_evt_t"></a>

<a id="_CPPv317bk_avrcp_ct_evt_t"></a> <a id="_CPPv217bk_avrcp_ct_evt_t"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014"></a> enum bk\_avrcp\_ct\_evt\_t
:   *Values:*

    <a id="_CPPv4N17bk_avrcp_ct_evt_t25BK_AVRCP_CT_EVT_CONNECTEDE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_evt_t25BK_AVRCP_CT_EVT_CONNECTEDE"></a> <a id="_CPPv2N17bk_avrcp_ct_evt_t25BK_AVRCP_CT_EVT_CONNECTEDE"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014a2643bb9cc5ed64878cc2f6acd8e3df37"></a> enumerator BK\_AVRCP\_CT\_EVT\_CONNECTED
    :   arg: uint8\_t remote\_bda\[6\]

    <a id="_CPPv4N17bk_avrcp_ct_evt_t28BK_AVRCP_CT_EVT_DISCONNECTEDE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_evt_t28BK_AVRCP_CT_EVT_DISCONNECTEDE"></a> <a id="_CPPv2N17bk_avrcp_ct_evt_t28BK_AVRCP_CT_EVT_DISCONNECTEDE"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014a69ce0ad849b59dd39a4f38ec85ab98e2"></a> enumerator BK\_AVRCP\_CT\_EVT\_DISCONNECTED
    :   arg: uint8\_t remote\_bda\[6\]

    <a id="_CPPv4N17bk_avrcp_ct_evt_t35BK_AVRCP_CT_EVT_PLAY_STATUS_CHANGEDE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_evt_t35BK_AVRCP_CT_EVT_PLAY_STATUS_CHANGEDE"></a> <a id="_CPPv2N17bk_avrcp_ct_evt_t35BK_AVRCP_CT_EVT_PLAY_STATUS_CHANGEDE"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014ad0820b7768d2fcb85a5733c741efbb06"></a> enumerator BK\_AVRCP\_CT\_EVT\_PLAY\_STATUS\_CHANGED
    :   arg: uint8\_t \* playback status

    <a id="_CPPv4N17bk_avrcp_ct_evt_t29BK_AVRCP_CT_EVT_TRACK_CHANGEDE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_evt_t29BK_AVRCP_CT_EVT_TRACK_CHANGEDE"></a> <a id="_CPPv2N17bk_avrcp_ct_evt_t29BK_AVRCP_CT_EVT_TRACK_CHANGEDE"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014ad5371c17219ef32478e661e70d0da82c"></a> enumerator BK\_AVRCP\_CT\_EVT\_TRACK\_CHANGED
    :   arg: uint64\_t \* track id

    <a id="_CPPv4N17bk_avrcp_ct_evt_t29BK_AVRCP_CT_EVT_ELEM_ATTR_RSPE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_evt_t29BK_AVRCP_CT_EVT_ELEM_ATTR_RSPE"></a> <a id="_CPPv2N17bk_avrcp_ct_evt_t29BK_AVRCP_CT_EVT_ELEM_ATTR_RSPE"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014a8ed7aaac7c617baf86c366af21c2e70f"></a> enumerator BK\_AVRCP\_CT\_EVT\_ELEM\_ATTR\_RSP
    :   arg: [bk\_avrcp\_ct\_cb\_param\_t](dual_bt.md#unionbk__avrcp__ct__cb__param__t) \*

    <a id="_CPPv4N17bk_avrcp_ct_evt_t32BK_AVRCP_CT_EVT_PLAY_POS_CHANGEDE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_evt_t32BK_AVRCP_CT_EVT_PLAY_POS_CHANGEDE"></a> <a id="_CPPv2N17bk_avrcp_ct_evt_t32BK_AVRCP_CT_EVT_PLAY_POS_CHANGEDE"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014a7732180747c8cfdf4757b7e186b9e8de"></a> enumerator BK\_AVRCP\_CT\_EVT\_PLAY\_POS\_CHANGED
    :   arg: uint32\_t \* playing position in milliseconds

    <a id="_CPPv4N17bk_avrcp_ct_evt_t37BK_AVRCP_CT_EVT_REMOTE_VOLUME_CHANGEDE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_evt_t37BK_AVRCP_CT_EVT_REMOTE_VOLUME_CHANGEDE"></a> <a id="_CPPv2N17bk_avrcp_ct_evt_t37BK_AVRCP_CT_EVT_REMOTE_VOLUME_CHANGEDE"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014a8dfd95cf4ddee6f58bf5f0657ca133bb"></a> enumerator BK\_AVRCP\_CT\_EVT\_REMOTE\_VOLUME\_CHANGED
    :   arg: uint8\_t \* peer volume 0x00-0x7f (remote\_volume\_mode)

    <a id="_CPPv4N17bk_avrcp_ct_evt_t38BK_AVRCP_CT_EVT_REMOTE_BATTERY_CHANGEDE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_evt_t38BK_AVRCP_CT_EVT_REMOTE_BATTERY_CHANGEDE"></a> <a id="_CPPv2N17bk_avrcp_ct_evt_t38BK_AVRCP_CT_EVT_REMOTE_BATTERY_CHANGEDE"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014a6875cc209a6f3feac1ca57c99af73622"></a> enumerator BK\_AVRCP\_CT\_EVT\_REMOTE\_BATTERY\_CHANGED
    :   arg: uint8\_t \* peer battery status (remote\_volume\_mode)

    <a id="_CPPv4N17bk_avrcp_ct_evt_t34BK_AVRCP_CT_EVT_SET_ABS_VOLUME_RSPE"></a>

    <a id="_CPPv3N17bk_avrcp_ct_evt_t34BK_AVRCP_CT_EVT_SET_ABS_VOLUME_RSPE"></a> <a id="_CPPv2N17bk_avrcp_ct_evt_t34BK_AVRCP_CT_EVT_SET_ABS_VOLUME_RSPE"></a> <a id="bk__avrcp__ct__service_8h_1a183b2d479c6c13050133d407c3c60014ab9347a27161ea3b27dac5de2d976d9ce"></a> enumerator BK\_AVRCP\_CT\_EVT\_SET\_ABS\_VOLUME\_RSP
    :   arg: [bk\_avrcp\_ct\_abs\_vol\_rsp\_t](#structbk__avrcp__ct__abs__vol__rsp__t) \* (remote\_volume\_mode)

<a id="id15"></a>

### Header File

- [bk\_avrcp\_tg\_service.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/avrcp/bk_avrcp_tg_service.h)

<a id="id16"></a>

### Functions

<a id="_CPPv429bk_avrcp_tg_register_event_cb22bk_avrcp_tg_event_cb_tPv"></a>

<a id="_CPPv329bk_avrcp_tg_register_event_cb22bk_avrcp_tg_event_cb_tPv"></a> <a id="_CPPv229bk_avrcp_tg_register_event_cb22bk_avrcp_tg_event_cb_tPv"></a> <a id="bk_avrcp_tg_register_event_cb__bk_avrcp_tg_event_cb_t.voidP"></a> <a id="bk__avrcp__tg__service_8h_1a0cd371b6ac3cbf4b188295df24044ff8"></a> int bk\_avrcp\_tg\_register\_event\_cb([bk\_avrcp\_tg\_event\_cb\_t](#_CPPv422bk_avrcp_tg_event_cb_t "bk_avrcp_tg_event_cb_t") cb, void \*user\_data)
:   Register the application TG event callback. Call before service init.

<a id="_CPPv424bk_avrcp_tg_service_initPK17bk_avrcp_tg_cfg_t"></a>

<a id="_CPPv324bk_avrcp_tg_service_initPK17bk_avrcp_tg_cfg_t"></a> <a id="_CPPv224bk_avrcp_tg_service_initPK17bk_avrcp_tg_cfg_t"></a> <a id="bk_avrcp_tg_service_init__bk_avrcp_tg_cfg_tCP"></a> <a id="bk__avrcp__tg__service_8h_1a6f87440ba6f263979f86261b8ee95899"></a> int bk\_avrcp\_tg\_service\_init(const [bk\_avrcp\_tg\_cfg\_t](#_CPPv417bk_avrcp_tg_cfg_t "bk_avrcp_tg_cfg_t") \*cfg)
:   Initialize AVRCP target role and absolute-volume notification support.

<a id="_CPPv426bk_avrcp_tg_service_deinitv"></a>

<a id="_CPPv326bk_avrcp_tg_service_deinitv"></a> <a id="_CPPv226bk_avrcp_tg_service_deinitv"></a> <a id="bk_avrcp_tg_service_deinit__void"></a> <a id="bk__avrcp__tg__service_8h_1a7ee2c555cd14a1af808fdaed0c9995ca"></a> int bk\_avrcp\_tg\_service\_deinit(void)
:   Deinitialize AVRCP target role and release resources.

<a id="_CPPv422bk_avrcp_tg_disconnectAL6E_K7uint8_t"></a>

<a id="_CPPv322bk_avrcp_tg_disconnectAL6E_K7uint8_t"></a> <a id="_CPPv222bk_avrcp_tg_disconnectA6_K7uint8_t"></a> <a id="bk_avrcp_tg_disconnect__uint8_tCA"></a> <a id="bk__avrcp__tg__service_8h_1a25e02e3d4257c12df4cca9af8984295e"></a> int bk\_avrcp\_tg\_disconnect(const uint8\_t bda\[6\])
:   Disconnect AVRCP target from the specified remote device.

<a id="_CPPv424bk_avrcp_tg_is_connectedv"></a>

<a id="_CPPv324bk_avrcp_tg_is_connectedv"></a> <a id="_CPPv224bk_avrcp_tg_is_connectedv"></a> <a id="bk_avrcp_tg_is_connected__void"></a> <a id="bk__avrcp__tg__service_8h_1af4ea9661d22b45445857655e9bc2ef9a"></a> int bk\_avrcp\_tg\_is\_connected(void)
:   Return non-zero when AVRCP target is connected.

<a id="_CPPv432bk_avrcp_tg_notify_volume_change7uint8_t"></a>

<a id="_CPPv332bk_avrcp_tg_notify_volume_change7uint8_t"></a> <a id="_CPPv232bk_avrcp_tg_notify_volume_change7uint8_t"></a> <a id="bk_avrcp_tg_notify_volume_change__uint8_t"></a> <a id="bk__avrcp__tg__service_8h_1ac56893d061e253a072a27d5df2ac331f"></a> int bk\_avrcp\_tg\_notify\_volume\_change(uint8\_t vol\_0\_7f)
:   Notify the peer of a local volume change if it registered for the event.

<a id="_CPPv434bk_avrcp_tg_notify_playback_status7uint8_t"></a>

<a id="_CPPv334bk_avrcp_tg_notify_playback_status7uint8_t"></a> <a id="_CPPv234bk_avrcp_tg_notify_playback_status7uint8_t"></a> <a id="bk_avrcp_tg_notify_playback_status__uint8_t"></a> <a id="bk__avrcp__tg__service_8h_1a12eef11d14797fa4bafb0f40c2023670"></a> int bk\_avrcp\_tg\_notify\_playback\_status(uint8\_t playback)
:   Report the current playback status to the peer (player\_mode only).

    参数
    :   **playback** – one of bk\_avrcp\_playback\_stat\_t (BK\_AVRCP\_PLAYBACK\_\*).

<a id="_CPPv431bk_avrcp_tg_notify_track_change8uint64_t"></a>

<a id="_CPPv331bk_avrcp_tg_notify_track_change8uint64_t"></a> <a id="_CPPv231bk_avrcp_tg_notify_track_change8uint64_t"></a> <a id="bk_avrcp_tg_notify_track_change__uint64_t"></a> <a id="bk__avrcp__tg__service_8h_1af9aa1c109504ae4e94d0a77e01000f2c"></a> int bk\_avrcp\_tg\_notify\_track\_change(uint64\_t track\_id)
:   Report a track change to the peer (player\_mode only); track\_id is an opaque 8-byte id.

<a id="_CPPv427bk_avrcp_tg_notify_play_pos8uint32_t"></a>

<a id="_CPPv327bk_avrcp_tg_notify_play_pos8uint32_t"></a> <a id="_CPPv227bk_avrcp_tg_notify_play_pos8uint32_t"></a> <a id="bk_avrcp_tg_notify_play_pos__uint32_t"></a> <a id="bk__avrcp__tg__service_8h_1a0706496442530a2ea2c4c5259a2c5dba"></a> int bk\_avrcp\_tg\_notify\_play\_pos(uint32\_t pos\_ms)
:   Report the current playing position in milliseconds (player\_mode only).

<a id="_CPPv433bk_avrcp_tg_notify_battery_status7uint8_t"></a>

<a id="_CPPv333bk_avrcp_tg_notify_battery_status7uint8_t"></a> <a id="_CPPv233bk_avrcp_tg_notify_battery_status7uint8_t"></a> <a id="bk_avrcp_tg_notify_battery_status__uint8_t"></a> <a id="bk__avrcp__tg__service_8h_1ac1eb4c77b5adbc31474ef406fd6575f4"></a> int bk\_avrcp\_tg\_notify\_battery\_status(uint8\_t batt)
:   Report the current battery status to the peer (player\_mode only).

<a id="_CPPv428bk_avrcp_tg_set_local_volume7uint8_tPK7uint8_t"></a>

<a id="_CPPv328bk_avrcp_tg_set_local_volume7uint8_tPK7uint8_t"></a> <a id="_CPPv228bk_avrcp_tg_set_local_volume7uint8_tPK7uint8_t"></a> <a id="bk_avrcp_tg_set_local_volume__uint8_t.uint8_tCP"></a> <a id="bk__avrcp__tg__service_8h_1a7004ec5a78ca44c55b9c18d308d97f20"></a> int bk\_avrcp\_tg\_set\_local\_volume(uint8\_t vol, const uint8\_t \*bda)
:   Update local volume, save it for the device address, and emit TG event.

<a id="_CPPv434bk_avrcp_tg_get_local_volume_valuev"></a>

<a id="_CPPv334bk_avrcp_tg_get_local_volume_valuev"></a> <a id="_CPPv234bk_avrcp_tg_get_local_volume_valuev"></a> <a id="bk_avrcp_tg_get_local_volume_value__void"></a> <a id="bk__avrcp__tg__service_8h_1a57fadd5820f62a6417fccd3c9d87bcad"></a> uint8\_t bk\_avrcp\_tg\_get\_local\_volume\_value(void)
:   Return the current local volume in the AVRCP 0x00-0x7f range.

<a id="_CPPv431bk_avrcp_tg_emit_current_volumev"></a>

<a id="_CPPv331bk_avrcp_tg_emit_current_volumev"></a> <a id="_CPPv231bk_avrcp_tg_emit_current_volumev"></a> <a id="bk_avrcp_tg_emit_current_volume__void"></a> <a id="bk__avrcp__tg__service_8h_1a6bc92211d808b6ffeeb7a88952639a90"></a> void bk\_avrcp\_tg\_emit\_current\_volume(void)
:   Emit the current local volume through the registered TG event callback.

<a id="id17"></a>

### Structures

<a id="_CPPv425bk_avrcp_tg_passthrough_t"></a>

<a id="_CPPv325bk_avrcp_tg_passthrough_t"></a> <a id="_CPPv225bk_avrcp_tg_passthrough_t"></a> <a id="bk_avrcp_tg_passthrough_t"></a> <a id="structbk__avrcp__tg__passthrough__t"></a> struct bk\_avrcp\_tg\_passthrough\_t
:   Passthrough command delivered to the app in player\_mode.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N25bk_avrcp_tg_passthrough_t8key_codeE"></a>

    <a id="_CPPv3N25bk_avrcp_tg_passthrough_t8key_codeE"></a> <a id="_CPPv2N25bk_avrcp_tg_passthrough_t8key_codeE"></a> <a id="bk_avrcp_tg_passthrough_t::key_code__uint8_t"></a> <a id="structbk__avrcp__tg__passthrough__t_1a3d3c4ec57db03f99b69ae52187272de0"></a> uint8\_t key\_code
    :   AVRCP passthrough key code (BK\_AVRCP\_PT\_CMD\_\*).

    <a id="_CPPv4N25bk_avrcp_tg_passthrough_t9key_stateE"></a>

    <a id="_CPPv3N25bk_avrcp_tg_passthrough_t9key_stateE"></a> <a id="_CPPv2N25bk_avrcp_tg_passthrough_t9key_stateE"></a> <a id="bk_avrcp_tg_passthrough_t::key_state__uint8_t"></a> <a id="structbk__avrcp__tg__passthrough__t_1ac3f0c4928d4ab453e91273f644ad046d"></a> uint8\_t key\_state
    :   Non-zero when the key is pressed, zero when released.

<a id="_CPPv417bk_avrcp_tg_cfg_t"></a>

<a id="_CPPv317bk_avrcp_tg_cfg_t"></a> <a id="_CPPv217bk_avrcp_tg_cfg_t"></a> <a id="bk_avrcp_tg_cfg_t"></a> <a id="structbk__avrcp__tg__cfg__t"></a> struct bk\_avrcp\_tg\_cfg\_t
:   AVRCP target service configuration.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_avrcp_tg_cfg_t14default_volumeE"></a>

    <a id="_CPPv3N17bk_avrcp_tg_cfg_t14default_volumeE"></a> <a id="_CPPv2N17bk_avrcp_tg_cfg_t14default_volumeE"></a> <a id="bk_avrcp_tg_cfg_t::default_volume__uint8_t"></a> <a id="structbk__avrcp__tg__cfg__t_1ac3e13c8688537f8243e8b23242987915"></a> uint8\_t default\_volume
    :   Initial local AVRCP volume in the 0x00-0x7f range.

    <a id="_CPPv4N17bk_avrcp_tg_cfg_t11player_modeE"></a>

    <a id="_CPPv3N17bk_avrcp_tg_cfg_t11player_modeE"></a> <a id="_CPPv2N17bk_avrcp_tg_cfg_t11player_modeE"></a> <a id="bk_avrcp_tg_cfg_t::player_mode__uint8_t"></a> <a id="structbk__avrcp__tg__cfg__t_1a7b0e92196aebabc69966e5d95639d159"></a> uint8\_t player\_mode
    :   0: volume-sink target (headset/speaker, default) \- only VOLUME RN. 1: media-player target (A2DP source) \- accepts passthrough and answers PLAY\_STATUS / PLAY\_POS / BATTERY registered notifications.

<a id="id18"></a>

### Type Definitions

<a id="_CPPv422bk_avrcp_tg_event_cb_t"></a>

<a id="_CPPv322bk_avrcp_tg_event_cb_t"></a> <a id="_CPPv222bk_avrcp_tg_event_cb_t"></a> <a id="bk_avrcp_tg_event_cb_t"></a> <a id="bk__avrcp__tg__service_8h_1a5885cf084813055913c886685f336adb"></a> typedef void (\*bk\_avrcp\_tg\_event\_cb\_t)([bk\_avrcp\_tg\_evt\_t](#_CPPv417bk_avrcp_tg_evt_t "bk_avrcp_tg_evt_t") evt, void \*arg, void \*user\_data)
:   AVRCP target event callback.

<a id="id19"></a>

### Enumerations

<a id="_CPPv417bk_avrcp_tg_evt_t"></a>

<a id="_CPPv317bk_avrcp_tg_evt_t"></a> <a id="_CPPv217bk_avrcp_tg_evt_t"></a> <a id="bk__avrcp__tg__service_8h_1a1e0114e14128f88c715b3b4e8efd27c1"></a> enum bk\_avrcp\_tg\_evt\_t
:   *Values:*

    <a id="_CPPv4N17bk_avrcp_tg_evt_t25BK_AVRCP_TG_EVT_CONNECTEDE"></a>

    <a id="_CPPv3N17bk_avrcp_tg_evt_t25BK_AVRCP_TG_EVT_CONNECTEDE"></a> <a id="_CPPv2N17bk_avrcp_tg_evt_t25BK_AVRCP_TG_EVT_CONNECTEDE"></a> <a id="bk__avrcp__tg__service_8h_1a1e0114e14128f88c715b3b4e8efd27c1a2ce82bb5161c6a610ddca8cb5e1304ed"></a> enumerator BK\_AVRCP\_TG\_EVT\_CONNECTED
    :   arg: uint8\_t remote\_bda\[6\]

    <a id="_CPPv4N17bk_avrcp_tg_evt_t28BK_AVRCP_TG_EVT_DISCONNECTEDE"></a>

    <a id="_CPPv3N17bk_avrcp_tg_evt_t28BK_AVRCP_TG_EVT_DISCONNECTEDE"></a> <a id="_CPPv2N17bk_avrcp_tg_evt_t28BK_AVRCP_TG_EVT_DISCONNECTEDE"></a> <a id="bk__avrcp__tg__service_8h_1a1e0114e14128f88c715b3b4e8efd27c1ae213e07a03be74c1cf7ecc4b3aa49b6a"></a> enumerator BK\_AVRCP\_TG\_EVT\_DISCONNECTED
    :   arg: uint8\_t remote\_bda\[6\]

    <a id="_CPPv4N17bk_avrcp_tg_evt_t30BK_AVRCP_TG_EVT_VOLUME_CHANGEDE"></a>

    <a id="_CPPv3N17bk_avrcp_tg_evt_t30BK_AVRCP_TG_EVT_VOLUME_CHANGEDE"></a> <a id="_CPPv2N17bk_avrcp_tg_evt_t30BK_AVRCP_TG_EVT_VOLUME_CHANGEDE"></a> <a id="bk__avrcp__tg__service_8h_1a1e0114e14128f88c715b3b4e8efd27c1a049cc7c92b41ba9778d1a6172e12cb38"></a> enumerator BK\_AVRCP\_TG\_EVT\_VOLUME\_CHANGED
    :   arg: uint8\_t \* volume in 0x00-0x7f range

    <a id="_CPPv4N17bk_avrcp_tg_evt_t27BK_AVRCP_TG_EVT_PASSTHROUGHE"></a>

    <a id="_CPPv3N17bk_avrcp_tg_evt_t27BK_AVRCP_TG_EVT_PASSTHROUGHE"></a> <a id="_CPPv2N17bk_avrcp_tg_evt_t27BK_AVRCP_TG_EVT_PASSTHROUGHE"></a> <a id="bk__avrcp__tg__service_8h_1a1e0114e14128f88c715b3b4e8efd27c1a84cacc30e34d0a865e7cddc2f40e0a46"></a> enumerator BK\_AVRCP\_TG\_EVT\_PASSTHROUGH
    :   arg: [bk\_avrcp\_tg\_passthrough\_t](#structbk__avrcp__tg__passthrough__t) \* (player\_mode only)

关键配置：

- `CONFIG_BT`：启用 BT。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE`：启用 AVRCP CT/TG service 编译。

<a id="hfp-hf-service"></a>

## HFP HF Service

HFP HF service 封装免提设备流程，包括 service level 连接、SCO 音频连接、上下行语音数据、
AG 音量控制、通话控制和 AT 命令交互。

API 参考：

<a id="id20"></a>

### Header File

- [bk\_hfp\_hf\_service.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/hfp/bk_hfp_hf_service.h)

<a id="id21"></a>

### Functions

<a id="_CPPv427bk_hfp_hf_register_event_cb20bk_hfp_hf_event_cb_tPv"></a>

<a id="_CPPv327bk_hfp_hf_register_event_cb20bk_hfp_hf_event_cb_tPv"></a> <a id="_CPPv227bk_hfp_hf_register_event_cb20bk_hfp_hf_event_cb_tPv"></a> <a id="bk_hfp_hf_register_event_cb__bk_hfp_hf_event_cb_t.voidP"></a> <a id="bk__hfp__hf__service_8h_1a559ac4b1ac63777e4ea49141f1735b43"></a> int bk\_hfp\_hf\_register\_event\_cb([bk\_hfp\_hf\_event\_cb\_t](#_CPPv420bk_hfp_hf_event_cb_t "bk_hfp_hf_event_cb_t") cb, void \*user\_data)
:   Register the application event callback.

    Call this function before [bk\_hfp\_hf\_service\_init()](#bk__hfp__hf__service_8h_1a8e2e2a55820801e39c2a72c71d4ce81c).

    参数
    :   - **cb** – Event callback.
        - **user\_data** – User context passed back in the callback.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv422bk_hfp_hf_service_init7uint8_t"></a>

<a id="_CPPv322bk_hfp_hf_service_init7uint8_t"></a> <a id="_CPPv222bk_hfp_hf_service_init7uint8_t"></a> <a id="bk_hfp_hf_service_init__uint8_t"></a> <a id="bk__hfp__hf__service_8h_1a8e2e2a55820801e39c2a72c71d4ce81c"></a> int bk\_hfp\_hf\_service\_init(uint8\_t msbc\_supported)
:   Initialize the HFP HF service.

    参数
    :   **msbc\_supported** – Non-zero to enable mSBC support, zero to use CVSD only.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv424bk_hfp_hf_service_deinitv"></a>

<a id="_CPPv324bk_hfp_hf_service_deinitv"></a> <a id="_CPPv224bk_hfp_hf_service_deinitv"></a> <a id="bk_hfp_hf_service_deinit__void"></a> <a id="bk__hfp__hf__service_8h_1a17e1f728e0406736902f060d38767d7c"></a> int bk\_hfp\_hf\_service\_deinit(void)
:   Deinitialize the HFP HF service.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv417bk_hfp_hf_connectAL6E_K7uint8_t"></a>

<a id="_CPPv317bk_hfp_hf_connectAL6E_K7uint8_t"></a> <a id="_CPPv217bk_hfp_hf_connectA6_K7uint8_t"></a> <a id="bk_hfp_hf_connect__uint8_tCA"></a> <a id="bk__hfp__hf__service_8h_1a39796187a58aae61ef897b8f6b73c58a"></a> int bk\_hfp\_hf\_connect(const uint8\_t bda\[6\])
:   Connect to a remote HFP Audio Gateway.

    参数
    :   **bda** – Remote Bluetooth device address.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv420bk_hfp_hf_disconnectAL6E_K7uint8_t"></a>

<a id="_CPPv320bk_hfp_hf_disconnectAL6E_K7uint8_t"></a> <a id="_CPPv220bk_hfp_hf_disconnectA6_K7uint8_t"></a> <a id="bk_hfp_hf_disconnect__uint8_tCA"></a> <a id="bk__hfp__hf__service_8h_1ad79543e9efa82869ace1345f17ec81b8"></a> int bk\_hfp\_hf\_disconnect(const uint8\_t bda\[6\])
:   Disconnect from a remote HFP Audio Gateway.

    参数
    :   **bda** – Remote Bluetooth device address.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv429bk_hfp_hf_query_current_callsv"></a>

<a id="_CPPv329bk_hfp_hf_query_current_callsv"></a> <a id="_CPPv229bk_hfp_hf_query_current_callsv"></a> <a id="bk_hfp_hf_query_current_calls__void"></a> <a id="bk__hfp__hf__service_8h_1aac020472e1e48f3abad1da8ada981681"></a> int bk\_hfp\_hf\_query\_current\_calls(void)
:   Query the current call list from the connected Audio Gateway.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv423bk_hfp_hf_volume_update7uint8_t7uint8_t"></a>

<a id="_CPPv323bk_hfp_hf_volume_update7uint8_t7uint8_t"></a> <a id="_CPPv223bk_hfp_hf_volume_update7uint8_t7uint8_t"></a> <a id="bk_hfp_hf_volume_update__uint8_t.uint8_t"></a> <a id="bk__hfp__hf__service_8h_1a247ed9002df8379a98b7efe05405419a"></a> int bk\_hfp\_hf\_volume\_update(uint8\_t type, uint8\_t volume)
:   Update speaker or microphone volume on the connected Audio Gateway.

    参数
    :   - **type** – Volume target, such as speaker or microphone.
        - **volume** – Volume value.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv425bk_hfp_hf_send_custom_cmdPKc"></a>

<a id="_CPPv325bk_hfp_hf_send_custom_cmdPKc"></a> <a id="_CPPv225bk_hfp_hf_send_custom_cmdPKc"></a> <a id="bk_hfp_hf_send_custom_cmd__cCP"></a> <a id="bk__hfp__hf__service_8h_1af279650b05bdccca85d68af9d5650bd2"></a> int bk\_hfp\_hf\_send\_custom\_cmd(const char \*cmd)
:   Send a custom AT command to the connected Audio Gateway.

    参数
    :   **cmd** – AT command string.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv437bk_hfp_hf_query_current_operator_namev"></a>

<a id="_CPPv337bk_hfp_hf_query_current_operator_namev"></a> <a id="_CPPv237bk_hfp_hf_query_current_operator_namev"></a> <a id="bk_hfp_hf_query_current_operator_name__void"></a> <a id="bk__hfp__hf__service_8h_1a5565f3abfe6747b77dfee87e68427de5"></a> int bk\_hfp\_hf\_query\_current\_operator\_name(void)
:   Query the current operator name.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv434bk_hfp_hf_retrieve_subscriber_infov"></a>

<a id="_CPPv334bk_hfp_hf_retrieve_subscriber_infov"></a> <a id="_CPPv234bk_hfp_hf_retrieve_subscriber_infov"></a> <a id="bk_hfp_hf_retrieve_subscriber_info__void"></a> <a id="bk__hfp__hf__service_8h_1ae4ba89713975becbabbee7ee1e3f9f49"></a> int bk\_hfp\_hf\_retrieve\_subscriber\_info(void)
:   Retrieve subscriber number information.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv419bk_hfp_hf_send_dtmfPKc"></a>

<a id="_CPPv319bk_hfp_hf_send_dtmfPKc"></a> <a id="_CPPv219bk_hfp_hf_send_dtmfPKc"></a> <a id="bk_hfp_hf_send_dtmf__cCP"></a> <a id="bk__hfp__hf__service_8h_1afffd6ac2e76fc0fc43f3141e2f8b2874"></a> int bk\_hfp\_hf\_send\_dtmf(const char \*code)
:   Send a DTMF code.

    参数
    :   **code** – DTMF code string.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv439bk_hfp_hf_request_last_voice_tag_numberv"></a>

<a id="_CPPv339bk_hfp_hf_request_last_voice_tag_numberv"></a> <a id="_CPPv239bk_hfp_hf_request_last_voice_tag_numberv"></a> <a id="bk_hfp_hf_request_last_voice_tag_number__void"></a> <a id="bk__hfp__hf__service_8h_1ade8280366e187484f76fa1507d7d80e0"></a> int bk\_hfp\_hf\_request\_last\_voice\_tag\_number(void)
:   Request the last voice tag number.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv419bk_hfp_hf_send_nrecv"></a>

<a id="_CPPv319bk_hfp_hf_send_nrecv"></a> <a id="_CPPv219bk_hfp_hf_send_nrecv"></a> <a id="bk_hfp_hf_send_nrec__void"></a> <a id="bk__hfp__hf__service_8h_1a79843b783257992ffad07c0c77a32523"></a> int bk\_hfp\_hf\_send\_nrec(void)
:   Send the NREC command.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv433bk_hfp_hf_start_voice_recognitionv"></a>

<a id="_CPPv333bk_hfp_hf_start_voice_recognitionv"></a> <a id="_CPPv233bk_hfp_hf_start_voice_recognitionv"></a> <a id="bk_hfp_hf_start_voice_recognition__void"></a> <a id="bk__hfp__hf__service_8h_1a1dec6f45c35a6d00f4abe9dd220032c8"></a> int bk\_hfp\_hf\_start\_voice\_recognition(void)
:   Start voice recognition on the connected Audio Gateway.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv432bk_hfp_hf_stop_voice_recognitionv"></a>

<a id="_CPPv332bk_hfp_hf_stop_voice_recognitionv"></a> <a id="_CPPv232bk_hfp_hf_stop_voice_recognitionv"></a> <a id="bk_hfp_hf_stop_voice_recognition__void"></a> <a id="bk__hfp__hf__service_8h_1ad1765f57a33ce3ae4fd06e4bc7265824"></a> int bk\_hfp\_hf\_stop\_voice\_recognition(void)
:   Stop voice recognition on the connected Audio Gateway.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv414bk_hfp_hf_dialPKc"></a>

<a id="_CPPv314bk_hfp_hf_dialPKc"></a> <a id="_CPPv214bk_hfp_hf_dialPKc"></a> <a id="bk_hfp_hf_dial__cCP"></a> <a id="bk__hfp__hf__service_8h_1af833b313cc583fce6a8c9cb1bf6130e5"></a> int bk\_hfp\_hf\_dial(const char \*num)
:   Dial a phone number.

    参数
    :   **num** – Phone number string.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv421bk_hfp_hf_dial_memory7int32_t"></a>

<a id="_CPPv321bk_hfp_hf_dial_memory7int32_t"></a> <a id="_CPPv221bk_hfp_hf_dial_memory7int32_t"></a> <a id="bk_hfp_hf_dial_memory__int32_t"></a> <a id="bk__hfp__hf__service_8h_1a6fce3b7f5bf5bec1a1b062268def0dae"></a> int bk\_hfp\_hf\_dial\_memory(int32\_t location)
:   Dial a number from the Audio Gateway memory location.

    参数
    :   **location** – Memory location index.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv416bk_hfp_hf_redialv"></a>

<a id="_CPPv316bk_hfp_hf_redialv"></a> <a id="_CPPv216bk_hfp_hf_redialv"></a> <a id="bk_hfp_hf_redial__void"></a> <a id="bk__hfp__hf__service_8h_1abd0d7d991b5747da2b2462e374e4f44f"></a> int bk\_hfp\_hf\_redial(void)
:   Redial the last dialed number.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv421bk_hfp_hf_answer_callv"></a>

<a id="_CPPv321bk_hfp_hf_answer_callv"></a> <a id="_CPPv221bk_hfp_hf_answer_callv"></a> <a id="bk_hfp_hf_answer_call__void"></a> <a id="bk__hfp__hf__service_8h_1a0cb16653baa52534063a806f595d0b7c"></a> int bk\_hfp\_hf\_answer\_call(void)
:   Answer an incoming call.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv421bk_hfp_hf_reject_callv"></a>

<a id="_CPPv321bk_hfp_hf_reject_callv"></a> <a id="_CPPv221bk_hfp_hf_reject_callv"></a> <a id="bk_hfp_hf_reject_call__void"></a> <a id="bk__hfp__hf__service_8h_1ad8c6b345ed6df156d76b4b0737afba75"></a> int bk\_hfp\_hf\_reject\_call(void)
:   Reject an incoming call.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv423bk_hfp_hf_send_chld_cmd7uint8_t"></a>

<a id="_CPPv323bk_hfp_hf_send_chld_cmd7uint8_t"></a> <a id="_CPPv223bk_hfp_hf_send_chld_cmd7uint8_t"></a> <a id="bk_hfp_hf_send_chld_cmd__uint8_t"></a> <a id="bk__hfp__hf__service_8h_1af9ffcc2f34a0e29c65608b5fb776f281"></a> int bk\_hfp\_hf\_send\_chld\_cmd(uint8\_t op)
:   Send a call hold command.

    参数
    :   **op** – CHLD operation value.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv423bk_hfp_hf_send_btrh_cmd7uint8_t"></a>

<a id="_CPPv323bk_hfp_hf_send_btrh_cmd7uint8_t"></a> <a id="_CPPv223bk_hfp_hf_send_btrh_cmd7uint8_t"></a> <a id="bk_hfp_hf_send_btrh_cmd__uint8_t"></a> <a id="bk__hfp__hf__service_8h_1a28a38f1833b07979d43a646e6fb3c106"></a> int bk\_hfp\_hf\_send\_btrh\_cmd(uint8\_t op)
:   Send a call response and hold command.

    参数
    :   **op** – BTRH operation value.

    返回
    :   0 on success, otherwise error code.

<a id="id22"></a>

### Structures

<a id="_CPPv421bk_hfp_hf_conn_info_t"></a>

<a id="_CPPv321bk_hfp_hf_conn_info_t"></a> <a id="_CPPv221bk_hfp_hf_conn_info_t"></a> <a id="bk_hfp_hf_conn_info_t"></a> <a id="structbk__hfp__hf__conn__info__t"></a> struct bk\_hfp\_hf\_conn\_info\_t
:   Service-level connection event payload.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21bk_hfp_hf_conn_info_t10remote_bdaE"></a>

    <a id="_CPPv3N21bk_hfp_hf_conn_info_t10remote_bdaE"></a> <a id="_CPPv2N21bk_hfp_hf_conn_info_t10remote_bdaE"></a> <a id="bk_hfp_hf_conn_info_t::remote_bda__uint8_tA"></a> <a id="structbk__hfp__hf__conn__info__t_1a979d3b9749d62afa604d1b575f87a74b"></a> uint8\_t remote\_bda\[6\]
    :   Remote Bluetooth device address.

    <a id="_CPPv4N21bk_hfp_hf_conn_info_t9peer_featE"></a>

    <a id="_CPPv3N21bk_hfp_hf_conn_info_t9peer_featE"></a> <a id="_CPPv2N21bk_hfp_hf_conn_info_t9peer_featE"></a> <a id="bk_hfp_hf_conn_info_t::peer_feat__uint32_t"></a> <a id="structbk__hfp__hf__conn__info__t_1af6c999663f5698207654fbad16b9307a"></a> uint32\_t peer\_feat
    :   Peer-supported HFP features.

    <a id="_CPPv4N21bk_hfp_hf_conn_info_t9chld_featE"></a>

    <a id="_CPPv3N21bk_hfp_hf_conn_info_t9chld_featE"></a> <a id="_CPPv2N21bk_hfp_hf_conn_info_t9chld_featE"></a> <a id="bk_hfp_hf_conn_info_t::chld_feat__uint32_t"></a> <a id="structbk__hfp__hf__conn__info__t_1a3269e9590f2a938c0bf25e963b17e7c8"></a> uint32\_t chld\_feat
    :   Peer-supported call hold features.

<a id="_CPPv422bk_hfp_hf_audio_info_t"></a>

<a id="_CPPv322bk_hfp_hf_audio_info_t"></a> <a id="_CPPv222bk_hfp_hf_audio_info_t"></a> <a id="bk_hfp_hf_audio_info_t"></a> <a id="structbk__hfp__hf__audio__info__t"></a> struct bk\_hfp\_hf\_audio\_info\_t
:   SCO audio connection event payload.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_hfp_hf_audio_info_t10remote_bdaE"></a>

    <a id="_CPPv3N22bk_hfp_hf_audio_info_t10remote_bdaE"></a> <a id="_CPPv2N22bk_hfp_hf_audio_info_t10remote_bdaE"></a> <a id="bk_hfp_hf_audio_info_t::remote_bda__uint8_tA"></a> <a id="structbk__hfp__hf__audio__info__t_1a49fd6aea439eee96d30aeaeaf6073686"></a> uint8\_t remote\_bda\[6\]
    :   Remote Bluetooth device address.

    <a id="_CPPv4N22bk_hfp_hf_audio_info_t5codecE"></a>

    <a id="_CPPv3N22bk_hfp_hf_audio_info_t5codecE"></a> <a id="_CPPv2N22bk_hfp_hf_audio_info_t5codecE"></a> <a id="bk_hfp_hf_audio_info_t::codec__uint8_t"></a> <a id="structbk__hfp__hf__audio__info__t_1a004e3c4dab16d32ff68f12d2d98f9a55"></a> uint8\_t codec
    :   SCO codec, such as CODEC\_VOICE\_CVSD or CODEC\_VOICE\_MSBC.

<a id="_CPPv423bk_hfp_hf_volume_info_t"></a>

<a id="_CPPv323bk_hfp_hf_volume_info_t"></a> <a id="_CPPv223bk_hfp_hf_volume_info_t"></a> <a id="bk_hfp_hf_volume_info_t"></a> <a id="structbk__hfp__hf__volume__info__t"></a> struct bk\_hfp\_hf\_volume\_info\_t
:   AG volume control event payload.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23bk_hfp_hf_volume_info_t4typeE"></a>

    <a id="_CPPv3N23bk_hfp_hf_volume_info_t4typeE"></a> <a id="_CPPv2N23bk_hfp_hf_volume_info_t4typeE"></a> <a id="bk_hfp_hf_volume_info_t::type__uint8_t"></a> <a id="structbk__hfp__hf__volume__info__t_1a00ba8fc3924028cc336dd3ecf8ff7625"></a> uint8\_t type
    :   Volume target, such as speaker or microphone.

    <a id="_CPPv4N23bk_hfp_hf_volume_info_t6volumeE"></a>

    <a id="_CPPv3N23bk_hfp_hf_volume_info_t6volumeE"></a> <a id="_CPPv2N23bk_hfp_hf_volume_info_t6volumeE"></a> <a id="bk_hfp_hf_volume_info_t::volume__uint8_t"></a> <a id="structbk__hfp__hf__volume__info__t_1a28fc829c9eb72f30ad45844cdd6c0e30"></a> uint8\_t volume
    :   Volume value reported by the Audio Gateway.

<a id="_CPPv422bk_hfp_hf_voice_data_t"></a>

<a id="_CPPv322bk_hfp_hf_voice_data_t"></a> <a id="_CPPv222bk_hfp_hf_voice_data_t"></a> <a id="bk_hfp_hf_voice_data_t"></a> <a id="structbk__hfp__hf__voice__data__t"></a> struct bk\_hfp\_hf\_voice\_data\_t
:   Downlink voice packet. The buffer is only valid during the event callback.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_hfp_hf_voice_data_t4dataE"></a>

    <a id="_CPPv3N22bk_hfp_hf_voice_data_t4dataE"></a> <a id="_CPPv2N22bk_hfp_hf_voice_data_t4dataE"></a> <a id="bk_hfp_hf_voice_data_t::data__uint8_tCP"></a> <a id="structbk__hfp__hf__voice__data__t_1a2b8208a2dd6271fa01620fd15babfa3c"></a> const uint8\_t \*data
    :   Voice packet buffer.

    <a id="_CPPv4N22bk_hfp_hf_voice_data_t3lenE"></a>

    <a id="_CPPv3N22bk_hfp_hf_voice_data_t3lenE"></a> <a id="_CPPv2N22bk_hfp_hf_voice_data_t3lenE"></a> <a id="bk_hfp_hf_voice_data_t::len__uint16_t"></a> <a id="structbk__hfp__hf__voice__data__t_1a78783f6a14ac6c226d6662ace937a220"></a> uint16\_t len
    :   Voice packet length in bytes.

<a id="_CPPv428bk_hfp_hf_at_response_info_t"></a>

<a id="_CPPv328bk_hfp_hf_at_response_info_t"></a> <a id="_CPPv228bk_hfp_hf_at_response_info_t"></a> <a id="bk_hfp_hf_at_response_info_t"></a> <a id="structbk__hfp__hf__at__response__info__t"></a> struct bk\_hfp\_hf\_at\_response\_info\_t
:   AT response event payload.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N28bk_hfp_hf_at_response_info_t4codeE"></a>

    <a id="_CPPv3N28bk_hfp_hf_at_response_info_t4codeE"></a> <a id="_CPPv2N28bk_hfp_hf_at_response_info_t4codeE"></a> <a id="bk_hfp_hf_at_response_info_t::code__i"></a> <a id="structbk__hfp__hf__at__response__info__t_1abd6cf7cddf8ab9a63480affcb0663dc0"></a> int code
    :   AT response code, see BK\_HF\_AT\_RESPONSE\_CODE\_\*.

    <a id="_CPPv4N28bk_hfp_hf_at_response_info_t8asso_cmdE"></a>

    <a id="_CPPv3N28bk_hfp_hf_at_response_info_t8asso_cmdE"></a> <a id="_CPPv2N28bk_hfp_hf_at_response_info_t8asso_cmdE"></a> <a id="bk_hfp_hf_at_response_info_t::asso_cmd__i"></a> <a id="structbk__hfp__hf__at__response__info__t_1a9a355ada225cf500a117476c2874179a"></a> int asso\_cmd
    :   Associated AT command, see BK\_HF\_AT\_CMD\_\*.

    <a id="_CPPv4N28bk_hfp_hf_at_response_info_t3cmeE"></a>

    <a id="_CPPv3N28bk_hfp_hf_at_response_info_t3cmeE"></a> <a id="_CPPv2N28bk_hfp_hf_at_response_info_t3cmeE"></a> <a id="bk_hfp_hf_at_response_info_t::cme__i"></a> <a id="structbk__hfp__hf__at__response__info__t_1ab6e5b1d6945cba29e1a601d5f4567069"></a> int cme
    :   CME error code when present.

<a id="_CPPv421bk_hfp_hf_call_info_t"></a>

<a id="_CPPv321bk_hfp_hf_call_info_t"></a> <a id="_CPPv221bk_hfp_hf_call_info_t"></a> <a id="bk_hfp_hf_call_info_t"></a> <a id="structbk__hfp__hf__call__info__t"></a> struct bk\_hfp\_hf\_call\_info\_t
:   Call activity indicator payload (\+CIEV call).

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21bk_hfp_hf_call_info_t6statusE"></a>

    <a id="_CPPv3N21bk_hfp_hf_call_info_t6statusE"></a> <a id="_CPPv2N21bk_hfp_hf_call_info_t6statusE"></a> <a id="bk_hfp_hf_call_info_t::status__i"></a> <a id="structbk__hfp__hf__call__info__t_1aed1e9f31502997b0c4d10be1eec0264b"></a> int status
    :   Call activity status.

<a id="_CPPv427bk_hfp_hf_call_setup_info_t"></a>

<a id="_CPPv327bk_hfp_hf_call_setup_info_t"></a> <a id="_CPPv227bk_hfp_hf_call_setup_info_t"></a> <a id="bk_hfp_hf_call_setup_info_t"></a> <a id="structbk__hfp__hf__call__setup__info__t"></a> struct bk\_hfp\_hf\_call\_setup\_info\_t
:   Call setup indicator payload (\+CIEV callsetup).

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N27bk_hfp_hf_call_setup_info_t6statusE"></a>

    <a id="_CPPv3N27bk_hfp_hf_call_setup_info_t6statusE"></a> <a id="_CPPv2N27bk_hfp_hf_call_setup_info_t6statusE"></a> <a id="bk_hfp_hf_call_setup_info_t::status__i"></a> <a id="structbk__hfp__hf__call__setup__info__t_1a0efdbcc96caaa5adc97de90c7c78acfc"></a> int status
    :   Call setup status.

<a id="_CPPv421bk_hfp_hf_clip_info_t"></a>

<a id="_CPPv321bk_hfp_hf_clip_info_t"></a> <a id="_CPPv221bk_hfp_hf_clip_info_t"></a> <a id="bk_hfp_hf_clip_info_t"></a> <a id="structbk__hfp__hf__clip__info__t"></a> struct bk\_hfp\_hf\_clip\_info\_t
:   Calling line identification payload (\+CLIP). Strings valid only in callback.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21bk_hfp_hf_clip_info_t6numberE"></a>

    <a id="_CPPv3N21bk_hfp_hf_clip_info_t6numberE"></a> <a id="_CPPv2N21bk_hfp_hf_clip_info_t6numberE"></a> <a id="bk_hfp_hf_clip_info_t::number__cCP"></a> <a id="structbk__hfp__hf__clip__info__t_1a8ddc91f867ea9235b849b965336bd6c1"></a> const char \*number
    :   Caller number string.

    <a id="_CPPv4N21bk_hfp_hf_clip_info_t4nameE"></a>

    <a id="_CPPv3N21bk_hfp_hf_clip_info_t4nameE"></a> <a id="_CPPv2N21bk_hfp_hf_clip_info_t4nameE"></a> <a id="bk_hfp_hf_clip_info_t::name__cCP"></a> <a id="structbk__hfp__hf__clip__info__t_1a7d92202ca1bdc89dec2b0e73d7e814fc"></a> const char \*name
    :   Caller name string, if provided by the peer.

<a id="_CPPv421bk_hfp_hf_clcc_info_t"></a>

<a id="_CPPv321bk_hfp_hf_clcc_info_t"></a> <a id="_CPPv221bk_hfp_hf_clcc_info_t"></a> <a id="bk_hfp_hf_clcc_info_t"></a> <a id="structbk__hfp__hf__clcc__info__t"></a> struct bk\_hfp\_hf\_clcc\_info\_t
:   Current call list entry payload (\+CLCC). Strings valid only in callback.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21bk_hfp_hf_clcc_info_t3idxE"></a>

    <a id="_CPPv3N21bk_hfp_hf_clcc_info_t3idxE"></a> <a id="_CPPv2N21bk_hfp_hf_clcc_info_t3idxE"></a> <a id="bk_hfp_hf_clcc_info_t::idx__i"></a> <a id="structbk__hfp__hf__clcc__info__t_1ae1257ff12b807994e26f68bddb2fcc4a"></a> int idx
    :   Call index (starting from 1).

    <a id="_CPPv4N21bk_hfp_hf_clcc_info_t3dirE"></a>

    <a id="_CPPv3N21bk_hfp_hf_clcc_info_t3dirE"></a> <a id="_CPPv2N21bk_hfp_hf_clcc_info_t3dirE"></a> <a id="bk_hfp_hf_clcc_info_t::dir__i"></a> <a id="structbk__hfp__hf__clcc__info__t_1a554114b449c5ee3f2ab92401d41640c9"></a> int dir
    :   Direction: 0 \= outgoing (MO), 1 \= incoming (MT).

    <a id="_CPPv4N21bk_hfp_hf_clcc_info_t6statusE"></a>

    <a id="_CPPv3N21bk_hfp_hf_clcc_info_t6statusE"></a> <a id="_CPPv2N21bk_hfp_hf_clcc_info_t6statusE"></a> <a id="bk_hfp_hf_clcc_info_t::status__i"></a> <a id="structbk__hfp__hf__clcc__info__t_1a6e7cc93d2afddb972f860ccfd28b8be4"></a> int status
    :   Call status (see \+CLCC status).

    <a id="_CPPv4N21bk_hfp_hf_clcc_info_t4mptyE"></a>

    <a id="_CPPv3N21bk_hfp_hf_clcc_info_t4mptyE"></a> <a id="_CPPv2N21bk_hfp_hf_clcc_info_t4mptyE"></a> <a id="bk_hfp_hf_clcc_info_t::mpty__i"></a> <a id="structbk__hfp__hf__clcc__info__t_1a69c2a3c2eaa03ce8f156ced37cbf99cd"></a> int mpty
    :   Multi-party flag: 0 \= single, 1 \= multi-party.

    <a id="_CPPv4N21bk_hfp_hf_clcc_info_t6numberE"></a>

    <a id="_CPPv3N21bk_hfp_hf_clcc_info_t6numberE"></a> <a id="_CPPv2N21bk_hfp_hf_clcc_info_t6numberE"></a> <a id="bk_hfp_hf_clcc_info_t::number__cCP"></a> <a id="structbk__hfp__hf__clcc__info__t_1a5dddcabf2040c6581a614eea10ac697c"></a> const char \*number
    :   Phone number string, may be NULL/empty.

<a id="_CPPv421bk_hfp_hf_btrh_info_t"></a>

<a id="_CPPv321bk_hfp_hf_btrh_info_t"></a> <a id="_CPPv221bk_hfp_hf_btrh_info_t"></a> <a id="bk_hfp_hf_btrh_info_t"></a> <a id="structbk__hfp__hf__btrh__info__t"></a> struct bk\_hfp\_hf\_btrh\_info\_t
:   Call hold and response status payload (\+BTRH).

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21bk_hfp_hf_btrh_info_t6statusE"></a>

    <a id="_CPPv3N21bk_hfp_hf_btrh_info_t6statusE"></a> <a id="_CPPv2N21bk_hfp_hf_btrh_info_t6statusE"></a> <a id="bk_hfp_hf_btrh_info_t::status__i"></a> <a id="structbk__hfp__hf__btrh__info__t_1afec757724082d82651d7b7003e5135be"></a> int status
    :   Call hold and response status.

<a id="_CPPv429bk_hfp_hf_unknown_data_info_t"></a>

<a id="_CPPv329bk_hfp_hf_unknown_data_info_t"></a> <a id="_CPPv229bk_hfp_hf_unknown_data_info_t"></a> <a id="bk_hfp_hf_unknown_data_info_t"></a> <a id="structbk__hfp__hf__unknown__data__info__t"></a> struct bk\_hfp\_hf\_unknown\_data\_info\_t
:   Raw/unknown AT data from the AG (e.g. \+CGMI response). Valid only in callback.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N29bk_hfp_hf_unknown_data_info_t4dataE"></a>

    <a id="_CPPv3N29bk_hfp_hf_unknown_data_info_t4dataE"></a> <a id="_CPPv2N29bk_hfp_hf_unknown_data_info_t4dataE"></a> <a id="bk_hfp_hf_unknown_data_info_t::data__cCP"></a> <a id="structbk__hfp__hf__unknown__data__info__t_1a129b08673093bbd14a77acf910e98228"></a> const char \*data
    :   Raw AT data buffer.

    <a id="_CPPv4N29bk_hfp_hf_unknown_data_info_t3lenE"></a>

    <a id="_CPPv3N29bk_hfp_hf_unknown_data_info_t3lenE"></a> <a id="_CPPv2N29bk_hfp_hf_unknown_data_info_t3lenE"></a> <a id="bk_hfp_hf_unknown_data_info_t::len__uint16_t"></a> <a id="structbk__hfp__hf__unknown__data__info__t_1a8b45d96922f9d79287145c58864192d6"></a> uint16\_t len
    :   Raw AT data length in bytes.

<a id="id23"></a>

### Type Definitions

<a id="_CPPv420bk_hfp_hf_event_cb_t"></a>

<a id="_CPPv320bk_hfp_hf_event_cb_t"></a> <a id="_CPPv220bk_hfp_hf_event_cb_t"></a> <a id="bk_hfp_hf_event_cb_t"></a> <a id="bk__hfp__hf__service_8h_1a28cb742762d79136a31709b7e2baa0a3"></a> typedef void (\*bk\_hfp\_hf\_event\_cb\_t)([bk\_hfp\_hf\_evt\_t](#_CPPv415bk_hfp_hf_evt_t "bk_hfp_hf_evt_t") evt, void \*arg, void \*user\_data)
:   HFP HF service event callback.

    Invoked from the Bluetooth stack/service context. Copy data before posting it to another task if it must live beyond the callback.

    Param evt
    :   Event ID.

    Param arg
    :   Event payload. The concrete type depends on the event ID.

    Param user\_data
    :   User context passed to [bk\_hfp\_hf\_register\_event\_cb()](#bk__hfp__hf__service_8h_1a559ac4b1ac63777e4ea49141f1735b43).

<a id="id24"></a>

### Enumerations

<a id="_CPPv415bk_hfp_hf_evt_t"></a>

<a id="_CPPv315bk_hfp_hf_evt_t"></a> <a id="_CPPv215bk_hfp_hf_evt_t"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7db"></a> enum bk\_hfp\_hf\_evt\_t
:   *Values:*

    <a id="_CPPv4N15bk_hfp_hf_evt_t23BK_HFP_HF_EVT_CONNECTEDE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t23BK_HFP_HF_EVT_CONNECTEDE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t23BK_HFP_HF_EVT_CONNECTEDE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba94456ab1c9d5e365cae8cfbe22275216"></a> enumerator BK\_HFP\_HF\_EVT\_CONNECTED
    :   HFP service-level connection is established. Event data: [bk\_hfp\_hf\_conn\_info\_t](#structbk__hfp__hf__conn__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t26BK_HFP_HF_EVT_DISCONNECTEDE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t26BK_HFP_HF_EVT_DISCONNECTEDE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t26BK_HFP_HF_EVT_DISCONNECTEDE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba8061db27fcd3d3f2a1d31b0214f68508"></a> enumerator BK\_HFP\_HF\_EVT\_DISCONNECTED
    :   HFP service-level connection is disconnected. Event data: [bk\_hfp\_hf\_conn\_info\_t](#structbk__hfp__hf__conn__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t29BK_HFP_HF_EVT_AUDIO_CONNECTEDE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t29BK_HFP_HF_EVT_AUDIO_CONNECTEDE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t29BK_HFP_HF_EVT_AUDIO_CONNECTEDE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba16d98e5190787d41ba902669b7105eb5"></a> enumerator BK\_HFP\_HF\_EVT\_AUDIO\_CONNECTED
    :   SCO audio connection is established. Event data: [bk\_hfp\_hf\_audio\_info\_t](#structbk__hfp__hf__audio__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t32BK_HFP_HF_EVT_AUDIO_DISCONNECTEDE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t32BK_HFP_HF_EVT_AUDIO_DISCONNECTEDE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t32BK_HFP_HF_EVT_AUDIO_DISCONNECTEDE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba4c9c0023e86403da0e7848975bb14944"></a> enumerator BK\_HFP\_HF\_EVT\_AUDIO\_DISCONNECTED
    :   SCO audio connection is disconnected. Event data: NULL.

    <a id="_CPPv4N15bk_hfp_hf_evt_t28BK_HFP_HF_EVT_VOLUME_CHANGEDE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t28BK_HFP_HF_EVT_VOLUME_CHANGEDE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t28BK_HFP_HF_EVT_VOLUME_CHANGEDE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba11c7dea34eb658cf589ce13af4a0ae19"></a> enumerator BK\_HFP\_HF\_EVT\_VOLUME\_CHANGED
    :   Audio Gateway volume state is changed. Event data: [bk\_hfp\_hf\_volume\_info\_t](#structbk__hfp__hf__volume__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t24BK_HFP_HF_EVT_VOICE_DATAE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t24BK_HFP_HF_EVT_VOICE_DATAE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t24BK_HFP_HF_EVT_VOICE_DATAE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dbaaff754b0e6c2c55d04e6e3474ce8dc76"></a> enumerator BK\_HFP\_HF\_EVT\_VOICE\_DATA
    :   Downlink SCO voice packet is received. Event data: [bk\_hfp\_hf\_voice\_data\_t](#structbk__hfp__hf__voice__data__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t25BK_HFP_HF_EVT_AT_RESPONSEE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t25BK_HFP_HF_EVT_AT_RESPONSEE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t25BK_HFP_HF_EVT_AT_RESPONSEE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba73213f97cd658b888f62ea84fd1f93d1"></a> enumerator BK\_HFP\_HF\_EVT\_AT\_RESPONSE
    :   AT command response is received. Event data: [bk\_hfp\_hf\_at\_response\_info\_t](#structbk__hfp__hf__at__response__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_RINGE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_RINGE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_RINGE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba33ce0450052a9bfd65eed1092215dfae"></a> enumerator BK\_HFP\_HF\_EVT\_RING
    :   Incoming call ring indication is received. Event data: NULL.

    <a id="_CPPv4N15bk_hfp_hf_evt_t22BK_HFP_HF_EVT_CALL_INDE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t22BK_HFP_HF_EVT_CALL_INDE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t22BK_HFP_HF_EVT_CALL_INDE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba05dc003d620844cf38d45f1f5ac5048c"></a> enumerator BK\_HFP\_HF\_EVT\_CALL\_IND
    :   Call activity indicator is changed. Event data: [bk\_hfp\_hf\_call\_info\_t](#structbk__hfp__hf__call__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t28BK_HFP_HF_EVT_CALL_SETUP_INDE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t28BK_HFP_HF_EVT_CALL_SETUP_INDE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t28BK_HFP_HF_EVT_CALL_SETUP_INDE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dbacf927a0f41044b1890976e4165746c8d"></a> enumerator BK\_HFP\_HF\_EVT\_CALL\_SETUP\_IND
    :   Call setup indicator is changed. Event data: [bk\_hfp\_hf\_call\_setup\_info\_t](#structbk__hfp__hf__call__setup__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_CLIPE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_CLIPE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_CLIPE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba535f95152bbcd8c62b93138f6197de82"></a> enumerator BK\_HFP\_HF\_EVT\_CLIP
    :   Calling line identification is received. Event data: [bk\_hfp\_hf\_clip\_info\_t](#structbk__hfp__hf__clip__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_BTRHE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_BTRHE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_BTRHE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dbae7b7c4694760dda6d76e1580bc725b56"></a> enumerator BK\_HFP\_HF\_EVT\_BTRH
    :   Call hold and response status is received. Event data: [bk\_hfp\_hf\_btrh\_info\_t](#structbk__hfp__hf__btrh__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t26BK_HFP_HF_EVT_UNKNOWN_DATAE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t26BK_HFP_HF_EVT_UNKNOWN_DATAE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t26BK_HFP_HF_EVT_UNKNOWN_DATAE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba332912470f941d7c8710e57ffab87891"></a> enumerator BK\_HFP\_HF\_EVT\_UNKNOWN\_DATA
    :   Raw AT data is received from the Audio Gateway. Event data: [bk\_hfp\_hf\_unknown\_data\_info\_t](#structbk__hfp__hf__unknown__data__info__t).

    <a id="_CPPv4N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_CLCCE"></a>

    <a id="_CPPv3N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_CLCCE"></a> <a id="_CPPv2N15bk_hfp_hf_evt_t18BK_HFP_HF_EVT_CLCCE"></a> <a id="bk__hfp__hf__service_8h_1ac50d851d9531f9c8e41f745fa520b7dba5a1067a05570bcea2001a1b73a05c2fc"></a> enumerator BK\_HFP\_HF\_EVT\_CLCC
    :   Current call list entry is received (\+CLCC). Event data: [bk\_hfp\_hf\_clcc\_info\_t](#structbk__hfp__hf__clcc__info__t).

关键配置：

- `CONFIG_BT`：启用 BT。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE`：启用 HFP HF service 编译。
- `CONFIG_AUDIO_PLAY`：启用 SCO 音频播放/处理路径。

<a id="ble-gatt-framework"></a>

## BLE GATT Framework

BLE GATT framework 提供 GAP、GATTS、GATTC 和连接上下文管理封装，供 AT 层和部分业务组件
复用。它基于 Bluetooth SDK API 构建，常用于快速创建 BLE GATT Server/Client 测试和业务流程。

API 参考：

<a id="id25"></a>

### Header File

- [dm\_gatt.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/ble/gatt/dm_gatt.h)

<a id="id26"></a>

### Functions

<a id="_CPPv418bk_dm_prf_gap_mainP16cli_gatt_param_t"></a>

<a id="_CPPv318bk_dm_prf_gap_mainP16cli_gatt_param_t"></a> <a id="_CPPv218bk_dm_prf_gap_mainP16cli_gatt_param_t"></a> <a id="bk_dm_prf_gap_main__cli_gatt_param_tP"></a> <a id="dm__gatt_8h_1a015d836c778b2c25c97b1a109f5af01e"></a> int bk\_dm\_prf\_gap\_main([cli\_gatt\_param\_t](#_CPPv416cli_gatt_param_t "cli_gatt_param_t") \*param)
:   Initialize the BLE GAP framework.

    参数
    :   **param** – Optional initialization parameters. Pass NULL to use defaults.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv420bk_dm_prf_gap_deinitv"></a>

<a id="_CPPv320bk_dm_prf_gap_deinitv"></a> <a id="_CPPv220bk_dm_prf_gap_deinitv"></a> <a id="bk_dm_prf_gap_deinit__void"></a> <a id="dm__gatt_8h_1a3574c191fe00df08e7bb8eb3c420bf6f"></a> int bk\_dm\_prf\_gap\_deinit(void)
:   Deinitialize the BLE GAP framework.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv425bk_dm_prf_gap_disable_allv"></a>

<a id="_CPPv325bk_dm_prf_gap_disable_allv"></a> <a id="_CPPv225bk_dm_prf_gap_disable_allv"></a> <a id="bk_dm_prf_gap_disable_all__void"></a> <a id="dm__gatt_8h_1a62daa8e1b98339489b6487b326a97693"></a> int32\_t bk\_dm\_prf\_gap\_disable\_all(void)
:   Disable all GAP framework roles and activities.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv430bk_dm_prf_gap_add_gap_callbackPv"></a>

<a id="_CPPv330bk_dm_prf_gap_add_gap_callbackPv"></a> <a id="_CPPv230bk_dm_prf_gap_add_gap_callbackPv"></a> <a id="bk_dm_prf_gap_add_gap_callback__voidP"></a> <a id="dm__gatt_8h_1ab3b981ab81f719401278c6e42c589f23"></a> int bk\_dm\_prf\_gap\_add\_gap\_callback(void \*cb)
:   Register a BLE GAP callback.

    参数
    :   **cb** – Callback pointer. The callback type is defined by the BLE GAP SDK.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv425dm_gatt_get_authen_statusP7uint8_tP7uint8_tP7uint8_tP7uint8_t"></a>

<a id="_CPPv325dm_gatt_get_authen_statusP7uint8_tP7uint8_tP7uint8_tP7uint8_t"></a> <a id="_CPPv225dm_gatt_get_authen_statusP7uint8_tP7uint8_tP7uint8_tP7uint8_t"></a> <a id="dm_gatt_get_authen_status__uint8_tP.uint8_tP.uint8_tP.uint8_tP"></a> <a id="dm__gatt_8h_1a79432db9440620ba555630a3c292dab8"></a> int32\_t dm\_gatt\_get\_authen\_status(uint8\_t \*nominal\_addr, uint8\_t \*nominal\_addr\_type, uint8\_t \*identity\_addr, uint8\_t \*identity\_addr\_type)
:   Get authentication address mapping information.

    参数
    :   - **nominal\_addr** – Nominal address input buffer.
        - **nominal\_addr\_type** – Nominal address type output buffer.
        - **identity\_addr** – Identity address output buffer.
        - **identity\_addr\_type** – Identity address type output buffer.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv436dm_gatt_find_id_info_by_nominal_infoP7uint8_t7uint8_tP7uint8_tP7uint8_t"></a>

<a id="_CPPv336dm_gatt_find_id_info_by_nominal_infoP7uint8_t7uint8_tP7uint8_tP7uint8_t"></a> <a id="_CPPv236dm_gatt_find_id_info_by_nominal_infoP7uint8_t7uint8_tP7uint8_tP7uint8_t"></a> <a id="dm_gatt_find_id_info_by_nominal_info__uint8_tP.uint8_t.uint8_tP.uint8_tP"></a> <a id="dm__gatt_8h_1aebb88da1a46decb753fc3dd9d975d938"></a> int32\_t dm\_gatt\_find\_id\_info\_by\_nominal\_info(uint8\_t \*nominal\_addr, uint8\_t nominal\_addr\_type, uint8\_t \*identity\_addr, uint8\_t \*identity\_addr\_type)
:   Find identity address information by nominal address information.

    参数
    :   - **nominal\_addr** – Nominal address input buffer.
        - **nominal\_addr\_type** – Nominal address type.
        - **identity\_addr** – Identity address output buffer.
        - **identity\_addr\_type** – Identity address type output buffer.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv427bk_dm_prf_gap_passkey_reply7uint8_t8uint32_t"></a>

<a id="_CPPv327bk_dm_prf_gap_passkey_reply7uint8_t8uint32_t"></a> <a id="_CPPv227bk_dm_prf_gap_passkey_reply7uint8_t8uint32_t"></a> <a id="bk_dm_prf_gap_passkey_reply__uint8_t.uint32_t"></a> <a id="dm__gatt_8h_1a291035f46631b583545feeb897aec1a3"></a> int bk\_dm\_prf\_gap\_passkey\_reply(uint8\_t accept, uint32\_t passkey)
:   Reply to a BLE passkey request.

    参数
    :   - **accept** – Non-zero to accept the passkey, zero to reject.
        - **passkey** – Passkey value.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv433bk_dm_prf_gap_set_security_method7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv333bk_dm_prf_gap_set_security_method7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv233bk_dm_prf_gap_set_security_method7uint8_t7uint8_t7uint8_t"></a> <a id="bk_dm_prf_gap_set_security_method__uint8_t.uint8_t.uint8_t"></a> <a id="dm__gatt_8h_1a6727a4f5d50835baa10e6d14461560c5"></a> int bk\_dm\_prf\_gap\_set\_security\_method(uint8\_t iocap, uint8\_t auth\_req, uint8\_t key\_distr)
:   Configure BLE security method.

    参数
    :   - **iocap** – IO capability.
        - **auth\_req** – Authentication request flags.
        - **key\_distr** – Key distribution flags.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv439bk_dm_prf_gap_is_linkkey_distr_from_ltkv"></a>

<a id="_CPPv339bk_dm_prf_gap_is_linkkey_distr_from_ltkv"></a> <a id="_CPPv239bk_dm_prf_gap_is_linkkey_distr_from_ltkv"></a> <a id="bk_dm_prf_gap_is_linkkey_distr_from_ltk__void"></a> <a id="dm__gatt_8h_1a5c9d9ec24fbe88dd60fc56a2d7c1079e"></a> bool bk\_dm\_prf\_gap\_is\_linkkey\_distr\_from\_ltk(void)
:   Check whether link keys are distributed from LTK information.

    返回
    :   true if link keys are distributed from LTK, otherwise false.

<a id="_CPPv425bk_dm_prf_gap_create_bondP7uint8_t"></a>

<a id="_CPPv325bk_dm_prf_gap_create_bondP7uint8_t"></a> <a id="_CPPv225bk_dm_prf_gap_create_bondP7uint8_t"></a> <a id="bk_dm_prf_gap_create_bond__uint8_tP"></a> <a id="dm__gatt_8h_1a0febe3df9ca8f61b7b2fd7bb16a87e42"></a> int bk\_dm\_prf\_gap\_create\_bond(uint8\_t \*addr)
:   Create a BLE bond with a peer device.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv425bk_dm_prf_gap_remove_bondP7uint8_t"></a>

<a id="_CPPv325bk_dm_prf_gap_remove_bondP7uint8_t"></a> <a id="_CPPv225bk_dm_prf_gap_remove_bondP7uint8_t"></a> <a id="bk_dm_prf_gap_remove_bond__uint8_tP"></a> <a id="dm__gatt_8h_1a2cd0b06abf646a7de84845513aae8ca4"></a> int bk\_dm\_prf\_gap\_remove\_bond(uint8\_t \*addr)
:   Remove BLE bond information for a peer device.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv430bk_dm_prf_gap_get_bonded_countv"></a>

<a id="_CPPv330bk_dm_prf_gap_get_bonded_countv"></a> <a id="_CPPv230bk_dm_prf_gap_get_bonded_countv"></a> <a id="bk_dm_prf_gap_get_bonded_count__void"></a> <a id="dm__gatt_8h_1a2899067e6531a94ff991a1e3c665065c"></a> uint32\_t bk\_dm\_prf\_gap\_get\_bonded\_count(void)
:   Get the number of bonded BLE devices.

    返回
    :   Number of bonded devices.

<a id="_CPPv424bk_dm_prf_gap_clean_bondv"></a>

<a id="_CPPv324bk_dm_prf_gap_clean_bondv"></a> <a id="_CPPv224bk_dm_prf_gap_clean_bondv"></a> <a id="bk_dm_prf_gap_clean_bond__void"></a> <a id="dm__gatt_8h_1aebd9f023dee65c6492feb6fd7020def5"></a> int32\_t bk\_dm\_prf\_gap\_clean\_bond(void)
:   Clear all BLE bond information.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv428bk_dm_prf_gap_show_bond_listv"></a>

<a id="_CPPv328bk_dm_prf_gap_show_bond_listv"></a> <a id="_CPPv228bk_dm_prf_gap_show_bond_listv"></a> <a id="bk_dm_prf_gap_show_bond_list__void"></a> <a id="dm__gatt_8h_1a97c23d504d36497bbc429bece5817436"></a> int32\_t bk\_dm\_prf\_gap\_show\_bond\_list(void)
:   Print the BLE bond list for debugging.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv435bk_dm_prf_gap_get_bond_info_by_addrP7uint8_t"></a>

<a id="_CPPv335bk_dm_prf_gap_get_bond_info_by_addrP7uint8_t"></a> <a id="_CPPv235bk_dm_prf_gap_get_bond_info_by_addrP7uint8_t"></a> <a id="bk_dm_prf_gap_get_bond_info_by_addr__uint8_tP"></a> <a id="dm__gatt_8h_1a63c1b10eb11ddee84c1889992a3ea82b"></a> [bk\_ble\_bond\_dev\_t](dual_ble.md#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") \*bk\_dm\_prf\_gap\_get\_bond\_info\_by\_addr(uint8\_t \*addr)
:   Get BLE bond information by address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   Pointer to bond information on success, otherwise NULL.

<a id="_CPPv431bk_dm_prf_gap_bond_info_foreachPF7int32_tP17bk_ble_bond_dev_tPvEPv"></a>

<a id="_CPPv331bk_dm_prf_gap_bond_info_foreachPF7int32_tP17bk_ble_bond_dev_tPvEPv"></a> <a id="_CPPv231bk_dm_prf_gap_bond_info_foreachPF7int32_tP17bk_ble_bond_dev_tPvEPv"></a> <a id="dm__gatt_8h_1a38573b58bb7d3b746522ec554d19332d"></a> uint8\_t bk\_dm\_prf\_gap\_bond\_info\_foreach(int32\_t (\*func)([bk\_ble\_bond\_dev\_t](dual_ble.md#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") \*info, void \*arg), void \*arg)
:   Iterate over BLE bond information.

    参数
    :   - **func** – Callback invoked for each bond record.
        - **arg** – User argument passed to the callback.

    返回
    :   Number of visited bond records.

<a id="_CPPv429bk_dm_prf_gap_clean_local_keyv"></a>

<a id="_CPPv329bk_dm_prf_gap_clean_local_keyv"></a> <a id="_CPPv229bk_dm_prf_gap_clean_local_keyv"></a> <a id="bk_dm_prf_gap_clean_local_key__void"></a> <a id="dm__gatt_8h_1ac161dd013805456e351e773abbed90a2"></a> int32\_t bk\_dm\_prf\_gap\_clean\_local\_key(void)
:   Clear local BLE security keys.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv430bk_dm_prf_gap_update_whitelist7uint8_tP7uint8_t7uint8_t"></a>

<a id="_CPPv330bk_dm_prf_gap_update_whitelist7uint8_tP7uint8_t7uint8_t"></a> <a id="_CPPv230bk_dm_prf_gap_update_whitelist7uint8_tP7uint8_t7uint8_t"></a> <a id="bk_dm_prf_gap_update_whitelist__uint8_t.uint8_tP.uint8_t"></a> <a id="dm__gatt_8h_1a2f98dd701a1f9b476be50d862fca4697"></a> int32\_t bk\_dm\_prf\_gap\_update\_whitelist(uint8\_t add\_remove, uint8\_t \*addr, uint8\_t addr\_type)
:   Add or remove a BLE peer from the controller white list.

    参数
    :   - **add\_remove** – Non-zero to add the peer, zero to remove it.
        - **addr** – Peer BLE address.
        - **addr\_type** – White-list address type, 0 for public and 1 for random.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv429bk_dm_prf_gap_clear_whitelistv"></a>

<a id="_CPPv329bk_dm_prf_gap_clear_whitelistv"></a> <a id="_CPPv229bk_dm_prf_gap_clear_whitelistv"></a> <a id="bk_dm_prf_gap_clear_whitelist__void"></a> <a id="dm__gatt_8h_1a1fc20dd727161e972a460f3187611fce"></a> int32\_t bk\_dm\_prf\_gap\_clear\_whitelist(void)
:   Clear the controller BLE white list.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv426bk_dm_prf_gap_update_paramP7uint8_t8uint16_t8uint16_t"></a>

<a id="_CPPv326bk_dm_prf_gap_update_paramP7uint8_t8uint16_t8uint16_t"></a> <a id="_CPPv226bk_dm_prf_gap_update_paramP7uint8_t8uint16_t8uint16_t"></a> <a id="bk_dm_prf_gap_update_param__uint8_tP.uint16_t.uint16_t"></a> <a id="dm__gatt_8h_1a65fda7304b33f26ed9d41fd1689859d4"></a> int bk\_dm\_prf\_gap\_update\_param(uint8\_t \*addr, uint16\_t interval, uint16\_t tout)
:   Update BLE connection parameters.

    参数
    :   - **addr** – Peer BLE address.
        - **interval** – Connection interval.
        - **tout** – Supervision timeout.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv418dm_ble_gap_get_rpaP7uint8_t"></a>

<a id="_CPPv318dm_ble_gap_get_rpaP7uint8_t"></a> <a id="_CPPv218dm_ble_gap_get_rpaP7uint8_t"></a> <a id="dm_ble_gap_get_rpa__uint8_tP"></a> <a id="dm__gatt_8h_1a5196880e2f28c542a78974dd0ddeabb6"></a> int32\_t dm\_ble\_gap\_get\_rpa(uint8\_t \*rpa)
:   Get the current resolvable private address.

    参数
    :   **rpa** – Output buffer for the address. The buffer length must be 6 bytes.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv431bk_dm_prf_gap_get_identity_addrP7uint8_t"></a>

<a id="_CPPv331bk_dm_prf_gap_get_identity_addrP7uint8_t"></a> <a id="_CPPv231bk_dm_prf_gap_get_identity_addrP7uint8_t"></a> <a id="bk_dm_prf_gap_get_identity_addr__uint8_tP"></a> <a id="dm__gatt_8h_1a9d142bd11e4de92645bc39e47388b18b"></a> void bk\_dm\_prf\_gap\_get\_identity\_addr(uint8\_t \*addr)
:   Get the local identity address.

    参数
    :   **addr** – Output buffer for the address. The buffer length must be 6 bytes.

<a id="_CPPv433bk_dm_prf_gap_get_current_conn_idv"></a>

<a id="_CPPv333bk_dm_prf_gap_get_current_conn_idv"></a> <a id="_CPPv233bk_dm_prf_gap_get_current_conn_idv"></a> <a id="bk_dm_prf_gap_get_current_conn_id__void"></a> <a id="dm__gatt_8h_1ad65a7df82de192c0c388e1691a870c87"></a> int16\_t bk\_dm\_prf\_gap\_get\_current\_conn\_id(void)
:   Get the current BLE GATT connection ID.

    返回
    :   Current connection ID, or negative value when no connection is active.

<a id="_CPPv435dm_ble_gap_set_auto_accept_pair_req7uint8_t"></a>

<a id="_CPPv335dm_ble_gap_set_auto_accept_pair_req7uint8_t"></a> <a id="_CPPv235dm_ble_gap_set_auto_accept_pair_req7uint8_t"></a> <a id="dm_ble_gap_set_auto_accept_pair_req__uint8_t"></a> <a id="dm__gatt_8h_1a15546ececa531425300bbec54017f83d"></a> int dm\_ble\_gap\_set\_auto\_accept\_pair\_req(uint8\_t accpet)
:   Configure whether pairing requests are accepted automatically.

    参数
    :   **accpet** – Non-zero to accept automatically, zero to require application handling.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv424bk_dm_prf_gap_disconnectP7uint8_t"></a>

<a id="_CPPv324bk_dm_prf_gap_disconnectP7uint8_t"></a> <a id="_CPPv224bk_dm_prf_gap_disconnectP7uint8_t"></a> <a id="bk_dm_prf_gap_disconnect__uint8_tP"></a> <a id="dm__gatt_8h_1a603a4d4e90123fd869997f15de5bf047"></a> int32\_t bk\_dm\_prf\_gap\_disconnect(uint8\_t \*addr)
:   Disconnect a BLE GATT link by address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv428bk_dm_prf_gap_connect_cancelv"></a>

<a id="_CPPv328bk_dm_prf_gap_connect_cancelv"></a> <a id="_CPPv228bk_dm_prf_gap_connect_cancelv"></a> <a id="bk_dm_prf_gap_connect_cancel__void"></a> <a id="dm__gatt_8h_1a0430016c22f94f4df8c569d6cb086215"></a> int32\_t bk\_dm\_prf\_gap\_connect\_cancel(void)
:   Cancel an ongoing BLE connection attempt.

    返回
    :   0 on success, otherwise error code.

<a id="id27"></a>

### Structures

<a id="_CPPv416cli_gatt_param_t"></a>

<a id="_CPPv316cli_gatt_param_t"></a> <a id="_CPPv216cli_gatt_param_t"></a> <a id="cli_gatt_param_t"></a> <a id="structcli__gatt__param__t"></a> struct cli\_gatt\_param\_t
:   GATT framework initialization parameters.

<a id="macros"></a>

### Macros

<a id="c.GAP_IS_OLD_API"></a>

<a id="dm__gatt_8h_1a2ccd505174fc3f357690db84daaffeb0"></a> GAP\_IS\_OLD\_API
:   Enable BLE bond/local-key storage in the GATT framework. Enable the built-in GATTS test attribute table. Select the legacy GAP API path.

<a id="c.GATT_MAX_BOND_COUNT"></a>

<a id="dm__gatt_8h_1a8e7ac3667adac3c684fe1c62269ef9ed"></a> GATT\_MAX\_BOND\_COUNT
:   Maximum number of BLE bonded devices tracked by the GATT framework.

<a id="c.SYNC_CMD_TIMEOUT_MS"></a>

<a id="dm__gatt_8h_1aa1ecda6613aa60f14502fcd64d1cae9f"></a> SYNC\_CMD\_TIMEOUT\_MS
:   Timeout in milliseconds for synchronous GATT helper commands.

<a id="c.GATT_DEBUG_LEVEL"></a>

<a id="dm__gatt_8h_1a8efe0b3c92bfad719bf5b2fe35e2c84c"></a> GATT\_DEBUG\_LEVEL

<a id="c.gatt_loge"></a>

<a id="dm__gatt_8h_1ad75de5145836cbad685e7e2c1e821be8"></a> gatt\_loge(format, ...)

<a id="c.gatt_logw"></a>

<a id="dm__gatt_8h_1a75b254ef4b2432acbc0a2e550de7e478"></a> gatt\_logw(format, ...)

<a id="c.gatt_logi"></a>

<a id="dm__gatt_8h_1a5798ae86667ae01fc32f7480abd092c1"></a> gatt\_logi(format, ...)

<a id="c.gatt_logd"></a>

<a id="dm__gatt_8h_1aaad510e535013324c570497c48b0f725"></a> gatt\_logd(format, ...)

<a id="c.gatt_logv"></a>

<a id="dm__gatt_8h_1ae3c3c0462fdaa4bf91628a5cfd4d57df"></a> gatt\_logv(format, ...)

<a id="c.INTERESTING_SERIVCE_UUID"></a>

<a id="dm__gatt_8h_1a5f5cb27f71b23c2eee7682e8d72bca34"></a> INTERESTING\_SERIVCE\_UUID
:   Demo service UUID used by the GATT sample flow.

<a id="c.INTERESTING_CHAR_UUID"></a>

<a id="dm__gatt_8h_1a47bebdf40c0b89808ab9313b4ac53ec3"></a> INTERESTING\_CHAR\_UUID
:   Demo characteristic UUID used by the GATT sample flow.

<a id="c.GATT_PARAM_MEMBER"></a>

<a id="dm__gatt_8h_1a34e9af642b79d5babec5b1a8a480227e"></a> GATT\_PARAM\_MEMBER(type)
:   Helper macro used to declare CLI GATT parameter fields.

<a id="id28"></a>

### Enumerations

<a id="_CPPv4Ut2_60"></a>

<a id="_CPPv3Ut2_60"></a> <a id="dm__gatt_8h_1aa156d1cebb38c8a65846c4d9c006012a"></a> enum \[anonymous\]
:   GATT framework log levels.

    *Values:*

    <a id="_CPPv4NUt2_6022GATT_DEBUG_LEVEL_ERRORE"></a>

    <a id="_CPPv3NUt2_6022GATT_DEBUG_LEVEL_ERRORE"></a> <a id="dm__gatt_8h_1aa156d1cebb38c8a65846c4d9c006012aa06bc50c9a711f077f588a9f2bbf44738"></a> enumerator GATT\_DEBUG\_LEVEL\_ERROR
    :   Error log level.

    <a id="_CPPv4NUt2_6024GATT_DEBUG_LEVEL_WARNINGE"></a>

    <a id="_CPPv3NUt2_6024GATT_DEBUG_LEVEL_WARNINGE"></a> <a id="dm__gatt_8h_1aa156d1cebb38c8a65846c4d9c006012aa20d979adbd55c3966e1d3506bd24ce50"></a> enumerator GATT\_DEBUG\_LEVEL\_WARNING
    :   Warning log level.

    <a id="_CPPv4NUt2_6021GATT_DEBUG_LEVEL_INFOE"></a>

    <a id="_CPPv3NUt2_6021GATT_DEBUG_LEVEL_INFOE"></a> <a id="dm__gatt_8h_1aa156d1cebb38c8a65846c4d9c006012aa798ffee51237f0b1b147769a6ec5df6e"></a> enumerator GATT\_DEBUG\_LEVEL\_INFO
    :   Informational log level.

    <a id="_CPPv4NUt2_6022GATT_DEBUG_LEVEL_DEBUGE"></a>

    <a id="_CPPv3NUt2_6022GATT_DEBUG_LEVEL_DEBUGE"></a> <a id="dm__gatt_8h_1aa156d1cebb38c8a65846c4d9c006012aabc8c8c3883ffd7a46002b1944915f9a9"></a> enumerator GATT\_DEBUG\_LEVEL\_DEBUG
    :   Debug log level.

    <a id="_CPPv4NUt2_6024GATT_DEBUG_LEVEL_VERBOSEE"></a>

    <a id="_CPPv3NUt2_6024GATT_DEBUG_LEVEL_VERBOSEE"></a> <a id="dm__gatt_8h_1aa156d1cebb38c8a65846c4d9c006012aa057fb9c6cf8bf6311d3bc60628ba1318"></a> enumerator GATT\_DEBUG\_LEVEL\_VERBOSE
    :   Verbose log level.

<a id="_CPPv4Ut2_61"></a>

<a id="_CPPv3Ut2_61"></a> <a id="dm__gatt_8h_1af8654c714018c6241d9ebd01f3fb5a26"></a> enum \[anonymous\]
:   Return values used by registered BLE GAP application callbacks.

    *Values:*

    <a id="_CPPv4NUt2_6131DM_BLE_GAP_APP_CB_RET_PROCESSEDE"></a>

    <a id="_CPPv3NUt2_6131DM_BLE_GAP_APP_CB_RET_PROCESSEDE"></a> <a id="dm__gatt_8h_1af8654c714018c6241d9ebd01f3fb5a26a9ceda2b001d3b139947c7103d548db9b"></a> enumerator DM\_BLE\_GAP\_APP\_CB\_RET\_PROCESSED
    :   Event was processed by the callback.

    <a id="_CPPv4NUt2_6136DM_BLE_GAP_APP_CB_RET_NO_INTERESTINGE"></a>

    <a id="_CPPv3NUt2_6136DM_BLE_GAP_APP_CB_RET_NO_INTERESTINGE"></a> <a id="dm__gatt_8h_1af8654c714018c6241d9ebd01f3fb5a26af9038a845d7416fd9a006f036a22c6d8"></a> enumerator DM\_BLE\_GAP\_APP\_CB\_RET\_NO\_INTERESTING
    :   Event was not handled by the callback.

<a id="id29"></a>

### Header File

- [dm\_gatts.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/ble/gatt/dm_gatts.h)

<a id="id30"></a>

### Functions

<a id="_CPPv423bk_dm_prf_gatts_is_initv"></a>

<a id="_CPPv323bk_dm_prf_gatts_is_initv"></a> <a id="_CPPv223bk_dm_prf_gatts_is_initv"></a> <a id="bk_dm_prf_gatts_is_init__void"></a> <a id="dm__gatts_8h_1af35adecdb218bffbf4efc4fbdc349e9f"></a> int32\_t bk\_dm\_prf\_gatts\_is\_init(void)
:   Check whether GATTS has been initialized.

    返回
    :   Non-zero if initialized, otherwise zero.

<a id="_CPPv420bk_dm_prf_gatts_mainP16cli_gatt_param_t"></a>

<a id="_CPPv320bk_dm_prf_gatts_mainP16cli_gatt_param_t"></a> <a id="_CPPv220bk_dm_prf_gatts_mainP16cli_gatt_param_t"></a> <a id="bk_dm_prf_gatts_main__cli_gatt_param_tP"></a> <a id="dm__gatts_8h_1a82cc02d5375c7137b4e2183f1a41443b"></a> int bk\_dm\_prf\_gatts\_main([cli\_gatt\_param\_t](#_CPPv416cli_gatt_param_t "cli_gatt_param_t") \*param)
:   Initialize the GATTS wrapper.

    参数
    :   **param** – Optional GATT initialization parameters.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv422bk_dm_prf_gatts_deinitv"></a>

<a id="_CPPv322bk_dm_prf_gatts_deinitv"></a> <a id="_CPPv222bk_dm_prf_gatts_deinitv"></a> <a id="bk_dm_prf_gatts_deinit__void"></a> <a id="dm__gatts_8h_1a905b32121bab26195ffb2ed65bffc67d"></a> int bk\_dm\_prf\_gatts\_deinit(void)
:   Deinitialize the GATTS wrapper.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv454bk_dm_prf_gatts_deinit_because_bluetooth_deinit_futurev"></a>

<a id="_CPPv354bk_dm_prf_gatts_deinit_because_bluetooth_deinit_futurev"></a> <a id="_CPPv254bk_dm_prf_gatts_deinit_because_bluetooth_deinit_futurev"></a> <a id="bk_dm_prf_gatts_deinit_because_bluetooth_deinit_future__void"></a> <a id="dm__gatts_8h_1acbef37bba29dc40a5d5681bd8c930fb1"></a> int32\_t bk\_dm\_prf\_gatts\_deinit\_because\_bluetooth\_deinit\_future(void)
:   Deinitialize GATTS during Bluetooth deinitialization.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv426bk_dm_prf_gatts_disconnectP7uint8_t"></a>

<a id="_CPPv326bk_dm_prf_gatts_disconnectP7uint8_t"></a> <a id="_CPPv226bk_dm_prf_gatts_disconnectP7uint8_t"></a> <a id="bk_dm_prf_gatts_disconnect__uint8_tP"></a> <a id="dm__gatts_8h_1a011e4484c69b1158e12207d90c54d5cf"></a> int32\_t bk\_dm\_prf\_gatts\_disconnect(uint8\_t \*addr)
:   Disconnect a GATTS link by peer address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv426bk_dm_prf_gatts_enable_adv7uint8_t"></a>

<a id="_CPPv326bk_dm_prf_gatts_enable_adv7uint8_t"></a> <a id="_CPPv226bk_dm_prf_gatts_enable_adv7uint8_t"></a> <a id="bk_dm_prf_gatts_enable_adv__uint8_t"></a> <a id="dm__gatts_8h_1a3a8b78927ae0965a17166668c44f2af4"></a> int32\_t bk\_dm\_prf\_gatts\_enable\_adv(uint8\_t enable)
:   Enable or disable advertising.

    参数
    :   **enable** – Non-zero to enable advertising, zero to disable.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv430bk_dm_prf_gatts_enable_service8uint32_t7uint8_t"></a>

<a id="_CPPv330bk_dm_prf_gatts_enable_service8uint32_t7uint8_t"></a> <a id="_CPPv230bk_dm_prf_gatts_enable_service8uint32_t7uint8_t"></a> <a id="bk_dm_prf_gatts_enable_service__uint32_t.uint8_t"></a> <a id="dm__gatts_8h_1a60e1e4d9829539412004193a22bacef7"></a> int32\_t bk\_dm\_prf\_gatts\_enable\_service(uint32\_t index, uint8\_t enable)
:   Enable or disable a registered GATTS service.

    参数
    :   - **index** – Service index.
        - **enable** – Non-zero to enable the service, zero to disable.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv422bk_dm_prf_gatts_reg_dbP18bk_gatts_attr_db_t8uint32_tP8uint16_t18dm_ble_gatts_db_cb7uint8_t"></a>

<a id="_CPPv322bk_dm_prf_gatts_reg_dbP18bk_gatts_attr_db_t8uint32_tP8uint16_t18dm_ble_gatts_db_cb7uint8_t"></a> <a id="_CPPv222bk_dm_prf_gatts_reg_dbP18bk_gatts_attr_db_t8uint32_tP8uint16_t18dm_ble_gatts_db_cb7uint8_t"></a> <a id="bk_dm_prf_gatts_reg_db__bk_gatts_attr_db_tP.uint32_t.uint16_tP.dm_ble_gatts_db_cb.uint8_t"></a> <a id="dm__gatts_8h_1a6e24d180e5b0b045031a124841371de6"></a> int32\_t bk\_dm\_prf\_gatts\_reg\_db([bk\_gatts\_attr\_db\_t](dual_ble.md#_CPPv418bk_gatts_attr_db_t "bk_gatts_attr_db_t") \*list, uint32\_t count, uint16\_t \*attr\_handle\_list, [dm\_ble\_gatts\_db\_cb](#_CPPv418dm_ble_gatts_db_cb "dm_ble_gatts_db_cb") cb, uint8\_t need\_create\_tab)
:   Register a GATTS attribute database.

    参数
    :   - **list** – Attribute database list.
        - **count** – Number of attributes in the list.
        - **attr\_handle\_list** – Output attribute handle list.
        - **cb** – Database event callback.
        - **need\_create\_tab** – Non-zero to create the attribute table.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv424bk_dm_prf_gatts_unreg_dbP18bk_gatts_attr_db_t"></a>

<a id="_CPPv324bk_dm_prf_gatts_unreg_dbP18bk_gatts_attr_db_t"></a> <a id="_CPPv224bk_dm_prf_gatts_unreg_dbP18bk_gatts_attr_db_t"></a> <a id="bk_dm_prf_gatts_unreg_db__bk_gatts_attr_db_tP"></a> <a id="dm__gatts_8h_1a439419c5bef940259f80f6e81c7f2d16"></a> int32\_t bk\_dm\_prf\_gatts\_unreg\_db([bk\_gatts\_attr\_db\_t](dual_ble.md#_CPPv418bk_gatts_attr_db_t "bk_gatts_attr_db_t") \*list)
:   Unregister a GATTS attribute database.

    参数
    :   **list** – Attribute database list.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv441bk_dm_prf_gatts_get_buff_from_attr_handleP18bk_gatts_attr_db_tP8uint16_t8uint32_t8uint16_tP8uint32_tPP7uint8_tP8uint32_t"></a>

<a id="_CPPv341bk_dm_prf_gatts_get_buff_from_attr_handleP18bk_gatts_attr_db_tP8uint16_t8uint32_t8uint16_tP8uint32_tPP7uint8_tP8uint32_t"></a> <a id="_CPPv241bk_dm_prf_gatts_get_buff_from_attr_handleP18bk_gatts_attr_db_tP8uint16_t8uint32_t8uint16_tP8uint32_tPP7uint8_tP8uint32_t"></a> <a id="bk_dm_prf_gatts_get_buff_from_attr_handle__bk_gatts_attr_db_tP.uint16_tP.uint32_t.uint16_t.uint32_tP.uint8_tPP.uint32_tP"></a> <a id="dm__gatts_8h_1a9afeeb3221e4b3ec2a5f01122ca12dc2"></a> int32\_t bk\_dm\_prf\_gatts\_get\_buff\_from\_attr\_handle([bk\_gatts\_attr\_db\_t](dual_ble.md#_CPPv418bk_gatts_attr_db_t "bk_gatts_attr_db_t") \*attr\_list, uint16\_t \*attr\_handle\_list, uint32\_t size, uint16\_t attr\_handle, uint32\_t \*output\_index, uint8\_t \*\*output\_buff, uint32\_t \*output\_size)
:   Find an attribute value buffer by attribute handle.

    参数
    :   - **attr\_list** – Attribute database list.
        - **attr\_handle\_list** – Attribute handle list.
        - **size** – Number of attributes in the list.
        - **attr\_handle** – Attribute handle to find.
        - **output\_index** – Output index in the attribute list.
        - **output\_buff** – Output pointer to the attribute value buffer.
        - **output\_size** – Output attribute value buffer size.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv430bk_dm_prf_gatts_get_current_ifv"></a>

<a id="_CPPv330bk_dm_prf_gatts_get_current_ifv"></a> <a id="_CPPv230bk_dm_prf_gatts_get_current_ifv"></a> <a id="bk_dm_prf_gatts_get_current_if__void"></a> <a id="dm__gatts_8h_1ab8fbffe88c24d11ad9426db7716b3677"></a> [bk\_gatt\_if\_t](dual_ble.md#_CPPv412bk_gatt_if_t "bk_gatt_if_t") bk\_dm\_prf\_gatts\_get\_current\_if(void)
:   Get the current GATTS interface.

    返回
    :   Current GATT interface.

<a id="_CPPv434bk_dm_prf_gatts_add_gatts_callbackPv"></a>

<a id="_CPPv334bk_dm_prf_gatts_add_gatts_callbackPv"></a> <a id="_CPPv234bk_dm_prf_gatts_add_gatts_callbackPv"></a> <a id="bk_dm_prf_gatts_add_gatts_callback__voidP"></a> <a id="dm__gatts_8h_1a0c58a5dafb1d1b262c1f91c087a89ad5"></a> int bk\_dm\_prf\_gatts\_add\_gatts\_callback(void \*param)
:   Register a GATTS application callback.

    参数
    :   **param** – Callback pointer.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv444bk_dm_prf_gatts_send_service_change_indicate8uint16_t7uint8_t"></a>

<a id="_CPPv344bk_dm_prf_gatts_send_service_change_indicate8uint16_t7uint8_t"></a> <a id="_CPPv244bk_dm_prf_gatts_send_service_change_indicate8uint16_t7uint8_t"></a> <a id="bk_dm_prf_gatts_send_service_change_indicate__uint16_t.uint8_t"></a> <a id="dm__gatts_8h_1a1b0e0f1144d80f83190c8757dbb547d3"></a> int32\_t bk\_dm\_prf\_gatts\_send\_service\_change\_indicate(uint16\_t conn\_id, uint8\_t all\_connected)
:   Send a Service Changed indication.

    参数
    :   - **conn\_id** – GATT connection ID.
        - **all\_connected** – Non-zero to send to all connected peers.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv427bk_dm_prf_gatts_send_notify8uint16_t8uint16_tP7uint8_t8uint32_t7uint8_t"></a>

<a id="_CPPv327bk_dm_prf_gatts_send_notify8uint16_t8uint16_tP7uint8_t8uint32_t7uint8_t"></a> <a id="_CPPv227bk_dm_prf_gatts_send_notify8uint16_t8uint16_tP7uint8_t8uint32_t7uint8_t"></a> <a id="bk_dm_prf_gatts_send_notify__uint16_t.uint16_t.uint8_tP.uint32_t.uint8_t"></a> <a id="dm__gatts_8h_1a35918a05a7b58a300f008fd752fe3256"></a> int32\_t bk\_dm\_prf\_gatts\_send\_notify(uint16\_t gatt\_conn\_id, uint16\_t attr\_handle, uint8\_t \*data, uint32\_t len, uint8\_t is\_notify)
:   Send notification or indication.

    参数
    :   - **gatt\_conn\_id** – GATT connection ID.
        - **attr\_handle** – Attribute handle.
        - **data** – Data buffer.
        - **len** – Data length in bytes.
        - **is\_notify** – Non-zero to send notification, zero to send indication.

    返回
    :   0 on success, otherwise error code.

<a id="id31"></a>

### Macros

<a id="c.BK_GATT_ATTR_TYPE"></a>

<a id="dm__gatts_8h_1a568b6082055003bd37d0d4c1ccfc2ca5"></a> BK\_GATT\_ATTR\_TYPE(iuuid)
:   Build a 16-bit UUID attribute type initializer.

<a id="c.BK_GATT_ATTR_CONTENT"></a>

<a id="dm__gatts_8h_1aee4ed825e0a93223028b690120ee5415"></a> BK\_GATT\_ATTR\_CONTENT(iuuid)
:   Build a 16-bit UUID attribute content initializer.

<a id="c.BK_GATT_ATTR_VALUE"></a>

<a id="dm__gatts_8h_1a3422d38dca574dd6231b2b9815c568c5"></a> BK\_GATT\_ATTR\_VALUE(ilen, ivalue)
:   Build an attribute value initializer.

<a id="c.BK_GATT_ATTR_TYPE_128"></a>

<a id="dm__gatts_8h_1a8045ee1bb1cbc7b4cd6d4647e4e620d4"></a> BK\_GATT\_ATTR\_TYPE\_128(iuuid)
:   Build a 128-bit UUID attribute type initializer.

<a id="c.BK_GATT_ATTR_CONTENT_128"></a>

<a id="dm__gatts_8h_1a26bf41f75a60d3994978faf21244dd9b"></a> BK\_GATT\_ATTR\_CONTENT\_128(iuuid)
:   Build a 128-bit UUID attribute content initializer.

<a id="c.BK_GATT_PRIMARY_SERVICE_DECL"></a>

<a id="dm__gatts_8h_1a71e52523643a57e2b5089b271e7174f8"></a> BK\_GATT\_PRIMARY\_SERVICE\_DECL(iuuid)
:   Build a primary service declaration with a 16-bit service UUID.

<a id="c.BK_GATT_PRIMARY_SERVICE_DECL_128"></a>

<a id="dm__gatts_8h_1abc83c6c45f108b41d536fa98ac11e1fe"></a> BK\_GATT\_PRIMARY\_SERVICE\_DECL\_128(iuuid)
:   Build a primary service declaration with a 128-bit service UUID.

<a id="c.BK_GATT_CHAR_DECL"></a>

<a id="dm__gatts_8h_1ae44c82f5d96520134b68b8185e0f8d64"></a> BK\_GATT\_CHAR\_DECL(iuuid, ilen, ivalue, iprop, iperm, irsp)
:   Build a characteristic declaration with a 16-bit characteristic UUID.

<a id="c.BK_GATT_CHAR_DECL_128"></a>

<a id="dm__gatts_8h_1a5176e35ca91eea5a452727506c672e99"></a> BK\_GATT\_CHAR\_DECL\_128(iuuid, ilen, ivalue, iprop, iperm, irsp)
:   Build a characteristic declaration with a 128-bit characteristic UUID.

<a id="c.BK_GATT_CHAR_DESC_DECL"></a>

<a id="dm__gatts_8h_1ad8407e05c55d6e5da51e8d07dff95885"></a> BK\_GATT\_CHAR\_DESC\_DECL(iuuid, ilen, ivalue, iperm, irsp)
:   Build a characteristic descriptor declaration with a 16-bit descriptor UUID.

<a id="c.BK_GATT_CHAR_DESC_DECL_128"></a>

<a id="dm__gatts_8h_1a3cf3afceed3cb302cc34ae07126ae458"></a> BK\_GATT\_CHAR\_DESC\_DECL\_128(iuuid, ilen, ivalue, iperm, irsp)
:   Build a characteristic descriptor declaration with a 128-bit descriptor UUID.

<a id="id32"></a>

### Type Definitions

<a id="_CPPv418dm_ble_gatts_db_cb"></a>

<a id="_CPPv318dm_ble_gatts_db_cb"></a> <a id="_CPPv218dm_ble_gatts_db_cb"></a> <a id="dm_ble_gatts_db_cb"></a> <a id="dm__gatts_8h_1ad5d7cd1d91bb1114552ee96ffdfc03d8"></a> typedef int32\_t (\*dm\_ble\_gatts\_db\_cb)([bk\_gatts\_cb\_event\_t](dual_ble.md#_CPPv419bk_gatts_cb_event_t "bk_gatts_cb_event_t") event, [bk\_gatt\_if\_t](dual_ble.md#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts\_if, [bk\_ble\_gatts\_cb\_param\_t](dual_ble.md#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t") \*param)
:   GATTS database event callback.

    Param event
    :   GATTS callback event.

    Param gatts\_if
    :   GATTS interface.

    Param param
    :   Event parameter.

    Return
    :   0 on success, otherwise error code.

<a id="_CPPv419dm_ble_gatts_app_cb"></a>

<a id="_CPPv319dm_ble_gatts_app_cb"></a> <a id="_CPPv219dm_ble_gatts_app_cb"></a> <a id="dm_ble_gatts_app_cb"></a> <a id="dm__gatts_8h_1aa2dce32007ea625e2aa88aceb03ab7cb"></a> typedef int32\_t (\*dm\_ble\_gatts\_app\_cb)([bk\_gatts\_cb\_event\_t](dual_ble.md#_CPPv419bk_gatts_cb_event_t "bk_gatts_cb_event_t") event, [bk\_gatt\_if\_t](dual_ble.md#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts\_if, [bk\_ble\_gatts\_cb\_param\_t](dual_ble.md#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t") \*comm\_param)
:   GATTS application event callback.

    Param event
    :   GATTS callback event.

    Param gatts\_if
    :   GATTS interface.

    Param comm\_param
    :   Event parameter.

    Return
    :   0 on success, otherwise error code.

<a id="id33"></a>

### Header File

- [dm\_gattc.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/ble/gatt/dm_gattc.h)

<a id="id34"></a>

### Functions

<a id="_CPPv420bk_dm_prf_gattc_mainP16cli_gatt_param_t"></a>

<a id="_CPPv320bk_dm_prf_gattc_mainP16cli_gatt_param_t"></a> <a id="_CPPv220bk_dm_prf_gattc_mainP16cli_gatt_param_t"></a> <a id="bk_dm_prf_gattc_main__cli_gatt_param_tP"></a> <a id="dm__gattc_8h_1a8c3bf6e27e63aaa4f1c31dd9f08b6464"></a> int bk\_dm\_prf\_gattc\_main([cli\_gatt\_param\_t](#_CPPv416cli_gatt_param_t "cli_gatt_param_t") \*param)
:   Initialize the GATTC wrapper.

    参数
    :   **param** – Optional GATT initialization parameters.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv422bk_dm_prf_gattc_deinitv"></a>

<a id="_CPPv322bk_dm_prf_gattc_deinitv"></a> <a id="_CPPv222bk_dm_prf_gattc_deinitv"></a> <a id="bk_dm_prf_gattc_deinit__void"></a> <a id="dm__gattc_8h_1a28a0d0429935403eddd23c9733bd64ea"></a> int bk\_dm\_prf\_gattc\_deinit(void)
:   Deinitialize the GATTC wrapper.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv423bk_dm_prf_gattc_connectP7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv323bk_dm_prf_gattc_connectP7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv223bk_dm_prf_gattc_connectP7uint8_t8uint32_t8uint32_t"></a> <a id="bk_dm_prf_gattc_connect__uint8_tP.uint32_t.uint32_t"></a> <a id="dm__gattc_8h_1a539218c08a600965c4afbc64b2de8939"></a> int32\_t bk\_dm\_prf\_gattc\_connect(uint8\_t \*addr, uint32\_t addr\_type, uint32\_t s\_timeout)
:   Connect to a GATT server.

    参数
    :   - **addr** – Peer BLE address.
        - **addr\_type** – Peer BLE address type.
        - **s\_timeout** – Connection timeout in seconds.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv427bk_dm_prf_gattc_connect_extP7uint8_t8uint32_tP27bk_gap_create_conn_params_t"></a>

<a id="_CPPv327bk_dm_prf_gattc_connect_extP7uint8_t8uint32_tP27bk_gap_create_conn_params_t"></a> <a id="_CPPv227bk_dm_prf_gattc_connect_extP7uint8_t8uint32_tP27bk_gap_create_conn_params_t"></a> <a id="bk_dm_prf_gattc_connect_ext__uint8_tP.uint32_t.bk_gap_create_conn_params_tP"></a> <a id="dm__gattc_8h_1ac9fa76066ea23dd330478537391bbdad"></a> int32\_t bk\_dm\_prf\_gattc\_connect\_ext(uint8\_t \*addr, uint32\_t addr\_type, [bk\_gap\_create\_conn\_params\_t](dual_ble.md#_CPPv427bk_gap_create_conn_params_t "bk_gap_create_conn_params_t") \*pm)
:   Connect to a GATT server with custom connection parameters.

    When pm is NULL, falls back to default params identical to dm\_gattc\_connect(addr, addr\_type, 500). bk\_dm\_prf\_gattc\_connect(addr, addr\_type, 500).

    参数
    :   - **addr** – Peer BLE address.
        - **addr\_type** – Peer BLE address type.
        - **pm** – Custom connection parameters, or NULL to use defaults.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv426bk_dm_prf_gattc_disconnectP7uint8_t"></a>

<a id="_CPPv326bk_dm_prf_gattc_disconnectP7uint8_t"></a> <a id="_CPPv226bk_dm_prf_gattc_disconnectP7uint8_t"></a> <a id="bk_dm_prf_gattc_disconnect__uint8_tP"></a> <a id="dm__gattc_8h_1a61d7f93343fa6d15f51df5536a8509af"></a> int32\_t bk\_dm\_prf\_gattc\_disconnect(uint8\_t \*addr)
:   Disconnect from a GATT server.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv430bk_dm_prf_gattc_connect_cancelv"></a>

<a id="_CPPv330bk_dm_prf_gattc_connect_cancelv"></a> <a id="_CPPv230bk_dm_prf_gattc_connect_cancelv"></a> <a id="bk_dm_prf_gattc_connect_cancel__void"></a> <a id="dm__gattc_8h_1aa18eac1e499bf2388c6fdd1ea5f7aa3c"></a> int32\_t bk\_dm\_prf\_gattc\_connect\_cancel(void)
:   Cancel an ongoing GATTC connection attempt.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv424bk_dm_prf_gattc_discover8uint16_t"></a>

<a id="_CPPv324bk_dm_prf_gattc_discover8uint16_t"></a> <a id="_CPPv224bk_dm_prf_gattc_discover8uint16_t"></a> <a id="bk_dm_prf_gattc_discover__uint16_t"></a> <a id="dm__gattc_8h_1a48b46a9a50a9a725018142a0bbedaac0"></a> int32\_t bk\_dm\_prf\_gattc\_discover(uint16\_t conn\_id)
:   Discover services on a GATT server.

    参数
    :   **conn\_id** – GATT connection ID.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv421bk_dm_prf_gattc_write8uint16_t8uint16_tP7uint8_t8uint32_t"></a>

<a id="_CPPv321bk_dm_prf_gattc_write8uint16_t8uint16_tP7uint8_t8uint32_t"></a> <a id="_CPPv221bk_dm_prf_gattc_write8uint16_t8uint16_tP7uint8_t8uint32_t"></a> <a id="bk_dm_prf_gattc_write__uint16_t.uint16_t.uint8_tP.uint32_t"></a> <a id="dm__gattc_8h_1a0f48fb17cef123ad5cf706d0669e29aa"></a> int32\_t bk\_dm\_prf\_gattc\_write(uint16\_t conn\_id, uint16\_t attr\_handle, uint8\_t \*data, uint32\_t len)
:   Write an attribute on a GATT server.

    参数
    :   - **conn\_id** – GATT connection ID.
        - **attr\_handle** – Attribute handle.
        - **data** – Data buffer.
        - **len** – Data length in bytes.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv425bk_dm_prf_gattc_write_ext8uint16_t8uint16_tP7uint8_t8uint32_t7uint8_t"></a>

<a id="_CPPv325bk_dm_prf_gattc_write_ext8uint16_t8uint16_tP7uint8_t8uint32_t7uint8_t"></a> <a id="_CPPv225bk_dm_prf_gattc_write_ext8uint16_t8uint16_tP7uint8_t8uint32_t7uint8_t"></a> <a id="bk_dm_prf_gattc_write_ext__uint16_t.uint16_t.uint8_tP.uint32_t.uint8_t"></a> <a id="dm__gattc_8h_1a1c0cec3b385dd87c16a2a89c5d62f58e"></a> int32\_t bk\_dm\_prf\_gattc\_write\_ext(uint16\_t gatt\_conn\_id, uint16\_t attr\_handle, uint8\_t \*data, uint32\_t len, uint8\_t write\_req)
:   Write an attribute with selectable write mode.

    参数
    :   - **gatt\_conn\_id** – GATT connection ID.
        - **attr\_handle** – Attribute handle.
        - **data** – Data buffer.
        - **len** – Data length in bytes.
        - **write\_req** – Non-zero to use write request, zero to use write command.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv420bk_dm_prf_gattc_read8uint16_t8uint16_tP7uint8_t8uint32_t"></a>

<a id="_CPPv320bk_dm_prf_gattc_read8uint16_t8uint16_tP7uint8_t8uint32_t"></a> <a id="_CPPv220bk_dm_prf_gattc_read8uint16_t8uint16_tP7uint8_t8uint32_t"></a> <a id="bk_dm_prf_gattc_read__uint16_t.uint16_t.uint8_tP.uint32_t"></a> <a id="dm__gattc_8h_1ac3ba7b5f62387f86d04da6971d70de02"></a> int32\_t bk\_dm\_prf\_gattc\_read(uint16\_t gatt\_conn\_id, uint16\_t attr\_handle, uint8\_t \*data, uint32\_t len)
:   Read an attribute from a GATT server.

    参数
    :   - **gatt\_conn\_id** – GATT connection ID.
        - **attr\_handle** – Attribute handle.
        - **data** – Output buffer.
        - **len** – Output buffer length in bytes.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv428bk_dm_prf_gattc_send_mtu_reqP7uint8_t7uint8_t"></a>

<a id="_CPPv328bk_dm_prf_gattc_send_mtu_reqP7uint8_t7uint8_t"></a> <a id="_CPPv228bk_dm_prf_gattc_send_mtu_reqP7uint8_t7uint8_t"></a> <a id="bk_dm_prf_gattc_send_mtu_req__uint8_tP.uint8_t"></a> <a id="dm__gattc_8h_1a507b2a279d3197c7adcf45d2a7aa0e9e"></a> int32\_t bk\_dm\_prf\_gattc\_send\_mtu\_req(uint8\_t \*mac, uint8\_t gatt\_conn\_id)
:   Send an MTU exchange request.

    参数
    :   - **mac** – Peer BLE address.
        - **gatt\_conn\_id** – GATT connection ID.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv434bk_dm_prf_gattc_add_gattc_callbackPv"></a>

<a id="_CPPv334bk_dm_prf_gattc_add_gattc_callbackPv"></a> <a id="_CPPv234bk_dm_prf_gattc_add_gattc_callbackPv"></a> <a id="bk_dm_prf_gattc_add_gattc_callback__voidP"></a> <a id="dm__gattc_8h_1a8c8a6872553806b2fca80b043f768771"></a> int bk\_dm\_prf\_gattc\_add\_gattc\_callback(void \*param)
:   Register a GATTC application callback.

    参数
    :   **param** – Callback pointer.

    返回
    :   0 on success, otherwise error code.

<a id="id35"></a>

### Type Definitions

<a id="_CPPv419dm_ble_gattc_app_cb"></a>

<a id="_CPPv319dm_ble_gattc_app_cb"></a> <a id="_CPPv219dm_ble_gattc_app_cb"></a> <a id="dm_ble_gattc_app_cb"></a> <a id="dm__gattc_8h_1a5d9c01d5af4bc670caa135f495976b9e"></a> typedef int32\_t (\*dm\_ble\_gattc\_app\_cb)([bk\_gattc\_cb\_event\_t](dual_ble.md#_CPPv419bk_gattc_cb_event_t "bk_gattc_cb_event_t") event, [bk\_gatt\_if\_t](dual_ble.md#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, [bk\_ble\_gattc\_cb\_param\_t](dual_ble.md#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t") \*comm\_param)
:   GATTC application event callback.

    Param event
    :   GATTC callback event.

    Param gattc\_if
    :   GATTC interface.

    Param comm\_param
    :   Event parameter.

    Return
    :   0 on success, otherwise error code.

<a id="id36"></a>

### Header File

- [dm\_gatt\_connection.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/ble/gatt/dm_gatt_connection.h)

<a id="id37"></a>

### Functions

<a id="_CPPv419dm_ble_app_env_initv"></a>

<a id="_CPPv319dm_ble_app_env_initv"></a> <a id="_CPPv219dm_ble_app_env_initv"></a> <a id="dm_ble_app_env_init__void"></a> <a id="dm__gatt__connection_8h_1afb129111e02f0d828f23a023c5269a81"></a> int32\_t dm\_ble\_app\_env\_init(void)
:   Initialize the BLE GATT connection context pool.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv421dm_ble_app_env_deinitv"></a>

<a id="_CPPv321dm_ble_app_env_deinitv"></a> <a id="_CPPv221dm_ble_app_env_deinitv"></a> <a id="dm_ble_app_env_deinit__void"></a> <a id="dm__gatt__connection_8h_1a157edb4be5e2abc74eb831583bf36a71"></a> int32\_t dm\_ble\_app\_env\_deinit(void)
:   Deinitialize the BLE GATT connection context pool.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv428dm_ble_alloc_app_env_by_addrP7uint8_t8uint32_t"></a>

<a id="_CPPv328dm_ble_alloc_app_env_by_addrP7uint8_t8uint32_t"></a> <a id="_CPPv228dm_ble_alloc_app_env_by_addrP7uint8_t8uint32_t"></a> <a id="dm_ble_alloc_app_env_by_addr__uint8_tP.uint32_t"></a> <a id="dm__gatt__connection_8h_1a617c0abf1662227dfee660994a9b463e"></a> [dm\_gatt\_app\_env\_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") \*dm\_ble\_alloc\_app\_env\_by\_addr(uint8\_t \*addr, uint32\_t data\_len)
:   Allocate a connection context by peer address.

    参数
    :   - **addr** – Peer BLE address.
        - **data\_len** – Length of additional data to allocate for this connection.

    返回
    :   Pointer to the context on success, otherwise NULL.

<a id="_CPPv427dm_ble_find_app_env_by_addrP7uint8_t"></a>

<a id="_CPPv327dm_ble_find_app_env_by_addrP7uint8_t"></a> <a id="_CPPv227dm_ble_find_app_env_by_addrP7uint8_t"></a> <a id="dm_ble_find_app_env_by_addr__uint8_tP"></a> <a id="dm__gatt__connection_8h_1aed2d6c8013af2c6b41c3e934f85df950"></a> [dm\_gatt\_app\_env\_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") \*dm\_ble\_find\_app\_env\_by\_addr(uint8\_t \*addr)
:   Find a connection context by peer address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   Pointer to the context on success, otherwise NULL.

<a id="_CPPv430dm_ble_find_app_env_by_conn_id8uint16_t"></a>

<a id="_CPPv330dm_ble_find_app_env_by_conn_id8uint16_t"></a> <a id="_CPPv230dm_ble_find_app_env_by_conn_id8uint16_t"></a> <a id="dm_ble_find_app_env_by_conn_id__uint16_t"></a> <a id="dm__gatt__connection_8h_1ae82aa03cd9ee667f29c528dd57d09bbd"></a> [dm\_gatt\_app\_env\_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") \*dm\_ble\_find\_app\_env\_by\_conn\_id(uint16\_t conn\_id)
:   Find a connection context by connection ID.

    参数
    :   **conn\_id** – GATT connection ID.

    返回
    :   Pointer to the context on success, otherwise NULL.

<a id="_CPPv426dm_ble_del_app_env_by_addrP7uint8_t"></a>

<a id="_CPPv326dm_ble_del_app_env_by_addrP7uint8_t"></a> <a id="_CPPv226dm_ble_del_app_env_by_addrP7uint8_t"></a> <a id="dm_ble_del_app_env_by_addr__uint8_tP"></a> <a id="dm__gatt__connection_8h_1a951dc1d4d11adff23fbb6a66f3a52817"></a> uint8\_t dm\_ble\_del\_app\_env\_by\_addr(uint8\_t \*addr)
:   Delete a connection context by peer address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   Non-zero if a context was deleted, otherwise zero.

<a id="_CPPv423dm_ble_free_all_app_envv"></a>

<a id="_CPPv323dm_ble_free_all_app_envv"></a> <a id="_CPPv223dm_ble_free_all_app_envv"></a> <a id="dm_ble_free_all_app_env__void"></a> <a id="dm__gatt__connection_8h_1a40c2c0b7f69055bc4a3f7506a3f2dba8"></a> uint8\_t dm\_ble\_free\_all\_app\_env(void)
:   Free all connection contexts.

    返回
    :   Non-zero on success, otherwise zero.

<a id="_CPPv434dm_ble_alloc_addition_data_by_addrP7uint8_t8uint32_t"></a>

<a id="_CPPv334dm_ble_alloc_addition_data_by_addrP7uint8_t8uint32_t"></a> <a id="_CPPv234dm_ble_alloc_addition_data_by_addrP7uint8_t8uint32_t"></a> <a id="dm_ble_alloc_addition_data_by_addr__uint8_tP.uint32_t"></a> <a id="dm__gatt__connection_8h_1aa35a278a3a5bd17d915f68afc29745bf"></a> [dm\_gatt\_app\_env\_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") \*dm\_ble\_alloc\_addition\_data\_by\_addr(uint8\_t \*addr, uint32\_t data\_len)
:   Allocate or resize additional data for a connection.

    参数
    :   - **addr** – Peer BLE address.
        - **data\_len** – Additional data length in bytes.

    返回
    :   Pointer to the context on success, otherwise NULL.

<a id="_CPPv433dm_ble_alloc_profile_data_by_addr8uint32_tP7uint8_t8uint32_tPP7uint8_t"></a>

<a id="_CPPv333dm_ble_alloc_profile_data_by_addr8uint32_tP7uint8_t8uint32_tPP7uint8_t"></a> <a id="_CPPv233dm_ble_alloc_profile_data_by_addr8uint32_tP7uint8_t8uint32_tPP7uint8_t"></a> <a id="dm_ble_alloc_profile_data_by_addr__uint32_t.uint8_tP.uint32_t.uint8_tPP"></a> <a id="dm__gatt__connection_8h_1a49a3ce94b82f8a3b2f341ccb90d1c107"></a> [dm\_gatt\_app\_env\_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") \*dm\_ble\_alloc\_profile\_data\_by\_addr(uint32\_t profile\_id, uint8\_t \*addr, uint32\_t data\_len, uint8\_t \*\*output\_param)
:   Allocate profile-specific data for a connection.

    参数
    :   - **profile\_id** – Profile ID.
        - **addr** – Peer BLE address.
        - **data\_len** – Profile data length in bytes.
        - **output\_param** – Output pointer to the allocated profile data buffer.

    返回
    :   Pointer to the context on success, otherwise NULL.

<a id="_CPPv438dm_ble_find_profile_data_by_profile_idP17dm_gatt_app_env_t8uint32_t"></a>

<a id="_CPPv338dm_ble_find_profile_data_by_profile_idP17dm_gatt_app_env_t8uint32_t"></a> <a id="_CPPv238dm_ble_find_profile_data_by_profile_idP17dm_gatt_app_env_t8uint32_t"></a> <a id="dm_ble_find_profile_data_by_profile_id__dm_gatt_app_env_tP.uint32_t"></a> <a id="dm__gatt__connection_8h_1a3f5d7f4f645f8ab252eaf9aeb42ce580"></a> uint8\_t \*dm\_ble\_find\_profile\_data\_by\_profile\_id([dm\_gatt\_app\_env\_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") \*env, uint32\_t profile\_id)
:   Find profile-specific data by profile ID.

    参数
    :   - **env** – Connection context.
        - **profile\_id** – Profile ID.

    返回
    :   Pointer to profile data on success, otherwise NULL.

<a id="_CPPv422dm_ble_app_env_foreachPF7int32_tP17dm_gatt_app_env_tPvEPv"></a>

<a id="_CPPv322dm_ble_app_env_foreachPF7int32_tP17dm_gatt_app_env_tPvEPv"></a> <a id="_CPPv222dm_ble_app_env_foreachPF7int32_tP17dm_gatt_app_env_tPvEPv"></a> <a id="dm__gatt__connection_8h_1a82aa9741dbe62d9bcada93aa415b0754"></a> uint8\_t dm\_ble\_app\_env\_foreach(int32\_t (\*func)([dm\_gatt\_app\_env\_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") \*env, void \*arg), void \*arg)
:   Iterate over active connection contexts.

    参数
    :   - **func** – Callback invoked for each context.
        - **arg** – User argument passed to the callback.

    返回
    :   Number of visited contexts.

<a id="id38"></a>

### Structures

<a id="_CPPv417dm_gatt_app_env_t"></a>

<a id="_CPPv317dm_gatt_app_env_t"></a> <a id="_CPPv217dm_gatt_app_env_t"></a> <a id="dm_gatt_app_env_t"></a> <a id="structdm__gatt__app__env__t"></a> struct dm\_gatt\_app\_env\_t
:   BLE GATT per-connection context.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17dm_gatt_app_env_t4addrE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t4addrE"></a> <a id="_CPPv2N17dm_gatt_app_env_t4addrE"></a> <a id="dm_gatt_app_env_t::addr__bk_bd_addr_t"></a> <a id="structdm__gatt__app__env__t_1a7ee983b1cea60973710eac62a9a55508"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr
    :   Peer BLE address.

    <a id="_CPPv4N17dm_gatt_app_env_t9addr_typeE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t9addr_typeE"></a> <a id="_CPPv2N17dm_gatt_app_env_t9addr_typeE"></a> <a id="dm_gatt_app_env_t::addr_type__bk_ble_addr_type_t"></a> <a id="structdm__gatt__app__env__t_1a0fbf026745d5ab45250655ab606ea75b"></a> [bk\_ble\_addr\_type\_t](dual_ble.md#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr\_type
    :   Peer BLE address type.

    <a id="_CPPv4N17dm_gatt_app_env_t7conn_idE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t7conn_idE"></a> <a id="_CPPv2N17dm_gatt_app_env_t7conn_idE"></a> <a id="dm_gatt_app_env_t::conn_id__uint16_t"></a> <a id="structdm__gatt__app__env__t_1ad397a2b9345c419e8417f5614bc8b01b"></a> uint16\_t conn\_id
    :   GATT connection ID.

    <a id="_CPPv4N17dm_gatt_app_env_t6statusE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t6statusE"></a> <a id="_CPPv2N17dm_gatt_app_env_t6statusE"></a> <a id="dm_gatt_app_env_t::status__uint8_t"></a> <a id="structdm__gatt__app__env__t_1acce0812eccb251aa3a94eb597ad66ed5"></a> uint8\_t status
    :   Connection state, see GAP\_CONNECT\_STATUS\_\*.

    <a id="_CPPv4N17dm_gatt_app_env_t15local_is_masterE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t15local_is_masterE"></a> <a id="_CPPv2N17dm_gatt_app_env_t15local_is_masterE"></a> <a id="dm_gatt_app_env_t::local_is_master__uint8_t"></a> <a id="structdm__gatt__app__env__t_1a7222ce818c6520d9a219d5ae8be99cc9"></a> uint8\_t local\_is\_master
    :   Non-zero when the local device is master/central.

    <a id="_CPPv4N17dm_gatt_app_env_t9is_authenE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t9is_authenE"></a> <a id="_CPPv2N17dm_gatt_app_env_t9is_authenE"></a> <a id="dm_gatt_app_env_t::is_authen__uint8_t"></a> <a id="structdm__gatt__app__env__t_1a8945745fa09ff1f143234c6a6687aa6b"></a> uint8\_t is\_authen
    :   Non-zero when the link is authenticated.

    <a id="_CPPv4N17dm_gatt_app_env_t10server_semE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t10server_semE"></a> <a id="_CPPv2N17dm_gatt_app_env_t10server_semE"></a> <a id="dm_gatt_app_env_t::server_sem__beken_semaphore_t"></a> <a id="structdm__gatt__app__env__t_1a3dc7a59c5407cde4bad702e12616847b"></a> [beken\_semaphore\_t](../system/os.md#_CPPv417beken_semaphore_t "beken_semaphore_t") server\_sem
    :   Server operation semaphore.

    <a id="_CPPv4N17dm_gatt_app_env_t10client_semE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t10client_semE"></a> <a id="_CPPv2N17dm_gatt_app_env_t10client_semE"></a> <a id="dm_gatt_app_env_t::client_sem__beken_semaphore_t"></a> <a id="structdm__gatt__app__env__t_1af204182db728d8a468853d2186d45875"></a> [beken\_semaphore\_t](../system/os.md#_CPPv417beken_semaphore_t "beken_semaphore_t") client\_sem
    :   Client operation semaphore.

    <a id="_CPPv4N17dm_gatt_app_env_t8data_lenE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t8data_lenE"></a> <a id="_CPPv2N17dm_gatt_app_env_t8data_lenE"></a> <a id="dm_gatt_app_env_t::data_len__uint32_t"></a> <a id="structdm__gatt__app__env__t_1a427c84a976a83b663438d51fab4c1b11"></a> uint32\_t data\_len
    :   Length of connection-level additional data.

        Profile data length in bytes.

    <a id="_CPPv4N17dm_gatt_app_env_t4dataE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t4dataE"></a> <a id="_CPPv2N17dm_gatt_app_env_t4dataE"></a> <a id="dm_gatt_app_env_t::data__uint8_tP"></a> <a id="structdm__gatt__app__env__t_1af43b33123eb198f8e320d6bd552d8afb"></a> uint8\_t \*data
    :   Connection-level additional data.

        Profile data buffer.

    <a id="_CPPv4N17dm_gatt_app_env_t2idE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t2idE"></a> <a id="_CPPv2N17dm_gatt_app_env_t2idE"></a> <a id="dm_gatt_app_env_t::id__uint32_t"></a> <a id="structdm__gatt__app__env__t_1aaeb94620e3d75c45cc6755da636a5638"></a> uint32\_t id
    :   Profile ID.

    <a id="_CPPv4N17dm_gatt_app_env_t13profile_arrayE"></a>

    <a id="_CPPv3N17dm_gatt_app_env_t13profile_arrayE"></a> <a id="_CPPv2N17dm_gatt_app_env_t13profile_arrayE"></a> <a id="structdm__gatt__app__env__t_1ad61f6eff9b058c2a9d56ab2b8ccbef53"></a> struct [dm\_gatt\_app\_env\_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t")::\[anonymous\] profile\_array\[GATT\_MAX\_PROFILE\_COUNT\]
    :   Profile-specific data entries attached to this connection.

<a id="_CPPv422dm_gatt_demo_app_env_t"></a>

<a id="_CPPv322dm_gatt_demo_app_env_t"></a> <a id="_CPPv222dm_gatt_demo_app_env_t"></a> <a id="dm_gatt_demo_app_env_t"></a> <a id="structdm__gatt__demo__app__env__t"></a> struct dm\_gatt\_demo\_app\_env\_t
:   Demo GATT application context shared by GATTS and GATTC demo flows.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22dm_gatt_demo_app_env_t13notify_statusE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t13notify_statusE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t13notify_statusE"></a> <a id="dm_gatt_demo_app_env_t::notify_status__uint8_t"></a> <a id="structdm__gatt__demo__app__env__t_1a3628cb41db89ec1db1e590776c91ca27"></a> uint8\_t notify\_status
    :   Server notify status: 0 disabled, 1 notify, 2 indicate.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t10server_mtuE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t10server_mtuE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t10server_mtuE"></a> <a id="dm_gatt_demo_app_env_t::server_mtu__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1ae5ce3f7544e2ea748eb9e55bc575c09e"></a> uint16\_t server\_mtu
    :   Server MTU.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t18send_notify_statusE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t18send_notify_statusE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t18send_notify_statusE"></a> <a id="dm_gatt_demo_app_env_t::send_notify_status__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1afc00284bafae279cba931877ecb158ff"></a> uint16\_t send\_notify\_status
    :   Notify/indicate send status.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t20send_read_rsp_statusE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t20send_read_rsp_statusE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t20send_read_rsp_statusE"></a> <a id="dm_gatt_demo_app_env_t::send_read_rsp_status__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1a727405b2aefb4878f67f59dfbc4859e9"></a> uint16\_t send\_read\_rsp\_status
    :   Read response send status.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t10job_statusE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t10job_statusE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t10job_statusE"></a> <a id="dm_gatt_demo_app_env_t::job_status__uint8_t"></a> <a id="structdm__gatt__demo__app__env__t_1afe535e5f18e72c2b801a578a6febd30d"></a> uint8\_t job\_status
    :   Client job status.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t14mtu_req_statusE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t14mtu_req_statusE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t14mtu_req_statusE"></a> <a id="dm_gatt_demo_app_env_t::mtu_req_status__uint8_t"></a> <a id="structdm__gatt__demo__app__env__t_1af1d0e37d1e45c23f77bf769fa36a3c08"></a> uint8\_t mtu\_req\_status
    :   MTU request status, see GATTC\_MTU\_REQ\_STATUS\_\*.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t15discover_statusE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t15discover_statusE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t15discover_statusE"></a> <a id="dm_gatt_demo_app_env_t::discover_status__uint8_t"></a> <a id="structdm__gatt__demo__app__env__t_1a843e81c6e2237470223dab97e1607aa3"></a> uint8\_t discover\_status
    :   Discovery status, see GATTC\_DISCOVER\_STATUS\_\*.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t10client_mtuE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t10client_mtuE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t10client_mtuE"></a> <a id="dm_gatt_demo_app_env_t::client_mtu__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1a628cf126246a73af19da7d21c51fa547"></a> uint16\_t client\_mtu
    :   Client MTU.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t18noti_indica_switchE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t18noti_indica_switchE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t18noti_indica_switchE"></a> <a id="dm_gatt_demo_app_env_t::noti_indica_switch__uint8_t"></a> <a id="structdm__gatt__demo__app__env__t_1a59991c538ae3c1eaad507689445950d8"></a> uint8\_t noti\_indica\_switch
    :   Notification/indication subscription state.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t24noti_indicate_recv_countE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t24noti_indicate_recv_countE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t24noti_indicate_recv_countE"></a> <a id="dm_gatt_demo_app_env_t::noti_indicate_recv_count__uint8_t"></a> <a id="structdm__gatt__demo__app__env__t_1aef7869274c845f9c19bf96ad354e17d2"></a> uint8\_t noti\_indicate\_recv\_count
    :   Number of notifications/indications received.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t17write_read_statusE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t17write_read_statusE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t17write_read_statusE"></a> <a id="dm_gatt_demo_app_env_t::write_read_status__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1a6b3c26f993a39177933aec2598d0422c"></a> uint16\_t write\_read\_status
    :   Write/read operation status.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t9read_buffE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t9read_buffE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t9read_buffE"></a> <a id="dm_gatt_demo_app_env_t::read_buff__uint8_tP"></a> <a id="structdm__gatt__demo__app__env__t_1aa8d99d2a551e4b7c5daf08a76c1e7e2a"></a> uint8\_t \*read\_buff
    :   Read result buffer.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t13read_buff_lenE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t13read_buff_lenE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t13read_buff_lenE"></a> <a id="dm_gatt_demo_app_env_t::read_buff_len__uint32_t"></a> <a id="structdm__gatt__demo__app__env__t_1a7b664b188e919dd84c56db967103f9d9"></a> uint32\_t read\_buff\_len
    :   Read result buffer length.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t11read_offsetE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t11read_offsetE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t11read_offsetE"></a> <a id="dm_gatt_demo_app_env_t::read_offset__uint32_t"></a> <a id="structdm__gatt__demo__app__env__t_1aabc74ce273c97ceaf4e0b77a6338bb70"></a> uint32\_t read\_offset
    :   Read offset.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t34peer_interest_service_start_handleE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t34peer_interest_service_start_handleE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t34peer_interest_service_start_handleE"></a> <a id="dm_gatt_demo_app_env_t::peer_interest_service_start_handle__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1a940869346b6a574da318f0f32e0857ff"></a> uint16\_t peer\_interest\_service\_start\_handle
    :   Peer interested service start handle.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t32peer_interest_service_end_handleE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t32peer_interest_service_end_handleE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t32peer_interest_service_end_handleE"></a> <a id="dm_gatt_demo_app_env_t::peer_interest_service_end_handle__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1a045449800d44fc430004e4567a59cff9"></a> uint16\_t peer\_interest\_service\_end\_handle
    :   Peer interested service end handle.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t25peer_interest_char_handleE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t25peer_interest_char_handleE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t25peer_interest_char_handleE"></a> <a id="dm_gatt_demo_app_env_t::peer_interest_char_handle__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1aabb380bbbccb3e4bef6feb91dcc0f9b1"></a> uint16\_t peer\_interest\_char\_handle
    :   Peer interested characteristic handle.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t30peer_interest_char_desc_handleE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t30peer_interest_char_desc_handleE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t30peer_interest_char_desc_handleE"></a> <a id="dm_gatt_demo_app_env_t::peer_interest_char_desc_handle__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1ab376f503eb5006fd18d9ebf52f700257"></a> uint16\_t peer\_interest\_char\_desc\_handle
    :   Peer interested descriptor handle.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t29peer_gap_service_start_handleE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t29peer_gap_service_start_handleE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t29peer_gap_service_start_handleE"></a> <a id="dm_gatt_demo_app_env_t::peer_gap_service_start_handle__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1a5ec7bd7587df830eb79ee297cc0f1440"></a> uint16\_t peer\_gap\_service\_start\_handle
    :   Peer GAP service start handle.

    <a id="_CPPv4N22dm_gatt_demo_app_env_t27peer_gap_service_end_handleE"></a>

    <a id="_CPPv3N22dm_gatt_demo_app_env_t27peer_gap_service_end_handleE"></a> <a id="_CPPv2N22dm_gatt_demo_app_env_t27peer_gap_service_end_handleE"></a> <a id="dm_gatt_demo_app_env_t::peer_gap_service_end_handle__uint16_t"></a> <a id="structdm__gatt__demo__app__env__t_1a32b22bc0e3517b695e687808722908e2"></a> uint16\_t peer\_gap\_service\_end\_handle
    :   Peer GAP service end handle.

<a id="id39"></a>

### Macros

<a id="c.GATT_MAX_CONNECTION_COUNT"></a>

<a id="dm__gatt__connection_8h_1ad0e02957f996b64fcc508c291e39e2a0"></a> GATT\_MAX\_CONNECTION\_COUNT
:   Maximum number of GATT connections tracked by the framework.

<a id="c.GATT_MAX_PROFILE_COUNT"></a>

<a id="dm__gatt__connection_8h_1ac50dd5f4199c30ba3f4d5d35e1622de1"></a> GATT\_MAX\_PROFILE\_COUNT
:   Maximum number of profile-specific data blocks per connection.

<a id="id40"></a>

### Enumerations

<a id="_CPPv4Ut2_62"></a>

<a id="_CPPv3Ut2_62"></a> <a id="dm__gatt__connection_8h_1a2f80701c36e79c0640d91c788feee0b3"></a> enum \[anonymous\]
:   BLE GAP connection states used by [dm\_gatt\_app\_env\_t::status](#structdm__gatt__app__env__t_1acce0812eccb251aa3a94eb597ad66ed5).

    *Values:*

    <a id="_CPPv4NUt2_6223GAP_CONNECT_STATUS_IDLEE"></a>

    <a id="_CPPv3NUt2_6223GAP_CONNECT_STATUS_IDLEE"></a> <a id="dm__gatt__connection_8h_1a2f80701c36e79c0640d91c788feee0b3ac68f78c39b5fd285983edc0c609c65da"></a> enumerator GAP\_CONNECT\_STATUS\_IDLE
    :   Connection is idle.

    <a id="_CPPv4NUt2_6229GAP_CONNECT_STATUS_CONNECTINGE"></a>

    <a id="_CPPv3NUt2_6229GAP_CONNECT_STATUS_CONNECTINGE"></a> <a id="dm__gatt__connection_8h_1a2f80701c36e79c0640d91c788feee0b3a0dc18ff234a47206bca824af06b2a1e6"></a> enumerator GAP\_CONNECT\_STATUS\_CONNECTING
    :   Connection is being established.

    <a id="_CPPv4NUt2_6228GAP_CONNECT_STATUS_CONNECTEDE"></a>

    <a id="_CPPv3NUt2_6228GAP_CONNECT_STATUS_CONNECTEDE"></a> <a id="dm__gatt__connection_8h_1a2f80701c36e79c0640d91c788feee0b3a2d6abdace9b9d592909b562c69367d4f"></a> enumerator GAP\_CONNECT\_STATUS\_CONNECTED
    :   Connection is established.

    <a id="_CPPv4NUt2_6232GAP_CONNECT_STATUS_DISCONNECTINGE"></a>

    <a id="_CPPv3NUt2_6232GAP_CONNECT_STATUS_DISCONNECTINGE"></a> <a id="dm__gatt__connection_8h_1a2f80701c36e79c0640d91c788feee0b3a3a1ff66b2ca72dec621e3ba4fa29fa33"></a> enumerator GAP\_CONNECT\_STATUS\_DISCONNECTING
    :   Connection is being disconnected.

<a id="_CPPv4Ut2_63"></a>

<a id="_CPPv3Ut2_63"></a> <a id="dm__gatt__connection_8h_1a531c35e38ede3ea4e5ba5afb24b29493"></a> enum \[anonymous\]
:   GATTC MTU request states.

    *Values:*

    <a id="_CPPv4NUt2_6325GATTC_MTU_REQ_STATUS_IDLEE"></a>

    <a id="_CPPv3NUt2_6325GATTC_MTU_REQ_STATUS_IDLEE"></a> <a id="dm__gatt__connection_8h_1a531c35e38ede3ea4e5ba5afb24b29493adb9914f401139df4cb4cf60b31277a70"></a> enumerator GATTC\_MTU\_REQ\_STATUS\_IDLE
    :   No MTU request is running.

    <a id="_CPPv4NUt2_6324GATTC_MTU_REQ_STATUS_INGE"></a>

    <a id="_CPPv3NUt2_6324GATTC_MTU_REQ_STATUS_INGE"></a> <a id="dm__gatt__connection_8h_1a531c35e38ede3ea4e5ba5afb24b29493aa58f4151d163ee71a9fc1040e8c9d45d"></a> enumerator GATTC\_MTU\_REQ\_STATUS\_ING
    :   MTU request is in progress.

    <a id="_CPPv4NUt2_6330GATTC_MTU_REQ_STATUS_COMPLETEDE"></a>

    <a id="_CPPv3NUt2_6330GATTC_MTU_REQ_STATUS_COMPLETEDE"></a> <a id="dm__gatt__connection_8h_1a531c35e38ede3ea4e5ba5afb24b29493adea58d7443676a5e166113e387a01b59"></a> enumerator GATTC\_MTU\_REQ\_STATUS\_COMPLETED
    :   MTU request is complete.

<a id="_CPPv4Ut2_64"></a>

<a id="_CPPv3Ut2_64"></a> <a id="dm__gatt__connection_8h_1a9334a5b9057f32da96db9b5c6a045d67"></a> enum \[anonymous\]
:   GATTC service discovery states.

    *Values:*

    <a id="_CPPv4NUt2_6426GATTC_DISCOVER_STATUS_IDLEE"></a>

    <a id="_CPPv3NUt2_6426GATTC_DISCOVER_STATUS_IDLEE"></a> <a id="dm__gatt__connection_8h_1a9334a5b9057f32da96db9b5c6a045d67aa67f6bfb5e1d022e6aedad8eda539058"></a> enumerator GATTC\_DISCOVER\_STATUS\_IDLE
    :   No discovery is running.

    <a id="_CPPv4NUt2_6425GATTC_DISCOVER_STATUS_INGE"></a>

    <a id="_CPPv3NUt2_6425GATTC_DISCOVER_STATUS_INGE"></a> <a id="dm__gatt__connection_8h_1a9334a5b9057f32da96db9b5c6a045d67a092544d261bfe280e1e97c89e0b7e30b"></a> enumerator GATTC\_DISCOVER\_STATUS\_ING
    :   Discovery is in progress.

    <a id="_CPPv4NUt2_6431GATTC_DISCOVER_STATUS_COMPLETEDE"></a>

    <a id="_CPPv3NUt2_6431GATTC_DISCOVER_STATUS_COMPLETEDE"></a> <a id="dm__gatt__connection_8h_1a9334a5b9057f32da96db9b5c6a045d67a715dacc469669c0f7bca2dec1d776b85"></a> enumerator GATTC\_DISCOVER\_STATUS\_COMPLETED
    :   Discovery is complete.

<a id="id41"></a>

### Header File

- [dm\_gap\_utils.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/ble/gatt/dm_gap_utils.h)

<a id="id42"></a>

### Functions

<a id="_CPPv427bk_dm_prf_gap_is_addr_validP7uint8_t"></a>

<a id="_CPPv327bk_dm_prf_gap_is_addr_validP7uint8_t"></a> <a id="_CPPv227bk_dm_prf_gap_is_addr_validP7uint8_t"></a> <a id="bk_dm_prf_gap_is_addr_valid__uint8_tP"></a> <a id="dm__gap__utils_8h_1a61b98e644ea6aac32f723f87d2f60666"></a> uint8\_t bk\_dm\_prf\_gap\_is\_addr\_valid(uint8\_t \*addr)
:   Check whether a BLE address is valid.

    参数
    :   **addr** – BLE address buffer. The buffer length must be 6 bytes.

    返回
    :   Non-zero if the address is valid, otherwise zero.

<a id="_CPPv427bk_dm_prf_gap_is_data_validP7uint8_t8uint32_t"></a>

<a id="_CPPv327bk_dm_prf_gap_is_data_validP7uint8_t8uint32_t"></a> <a id="_CPPv227bk_dm_prf_gap_is_data_validP7uint8_t8uint32_t"></a> <a id="bk_dm_prf_gap_is_data_valid__uint8_tP.uint32_t"></a> <a id="dm__gap__utils_8h_1acde582ef1df4bd658e56681bad455343"></a> uint8\_t bk\_dm\_prf\_gap\_is\_data\_valid(uint8\_t \*data, uint32\_t len)
:   Check whether a data buffer is valid.

    参数
    :   - **data** – Data buffer.
        - **len** – Data length in bytes.

    返回
    :   Non-zero if the buffer is valid, otherwise zero.

关键配置：

- `CONFIG_BLE`：启用 BLE。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATT`：启用 BLE GATT framework。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_USE_STORAGE`：控制 bond 信息持久化。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATTS_TEST_ATTR`：启用测试属性表。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATT_LOG_LEVEL`：配置 GATT framework 日志等级。
- `CONFIG_CLI`：启用 BLE GATT demo CLI。

<a id="hogpd-demo"></a>

## HOGPD Demo

HOGPD Demo 基于 BLE GATT framework 实现 HID-over-GATT keyboard 示例。

API 参考：

<a id="id43"></a>

### Header File

- [hogpd.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/ble/hogpd/hogpd.h)

<a id="id44"></a>

### Functions

<a id="_CPPv420bk_dm_prf_hogpd_initv"></a>

<a id="_CPPv320bk_dm_prf_hogpd_initv"></a> <a id="_CPPv220bk_dm_prf_hogpd_initv"></a> <a id="bk_dm_prf_hogpd_init__void"></a> <a id="hogpd_8h_1af689982848e0cf1b5c129861ce993874"></a> int32\_t bk\_dm\_prf\_hogpd\_init(void)

<a id="_CPPv422bk_dm_prf_hogpd_deinit7uint8_t"></a>

<a id="_CPPv322bk_dm_prf_hogpd_deinit7uint8_t"></a> <a id="_CPPv222bk_dm_prf_hogpd_deinit7uint8_t"></a> <a id="bk_dm_prf_hogpd_deinit__uint8_t"></a> <a id="hogpd_8h_1a30559dc33c56ca9a0374562fc23b1955"></a> int32\_t bk\_dm\_prf\_hogpd\_deinit(uint8\_t deinit\_bluetooth\_future)

<a id="_CPPv454bk_dm_prf_hogpd_deinit_because_bluetooth_deinit_futurev"></a>

<a id="_CPPv354bk_dm_prf_hogpd_deinit_because_bluetooth_deinit_futurev"></a> <a id="_CPPv254bk_dm_prf_hogpd_deinit_because_bluetooth_deinit_futurev"></a> <a id="bk_dm_prf_hogpd_deinit_because_bluetooth_deinit_future__void"></a> <a id="hogpd_8h_1abea239d0065f8580046b7f423a61d877"></a> int32\_t bk\_dm\_prf\_hogpd\_deinit\_because\_bluetooth\_deinit\_future(void)

<a id="_CPPv422bk_dm_prf_hogpd_notify8uint16_tP7uint8_t8uint32_t7uint8_t7uint8_t"></a>

<a id="_CPPv322bk_dm_prf_hogpd_notify8uint16_tP7uint8_t8uint32_t7uint8_t7uint8_t"></a> <a id="_CPPv222bk_dm_prf_hogpd_notify8uint16_tP7uint8_t8uint32_t7uint8_t7uint8_t"></a> <a id="bk_dm_prf_hogpd_notify__uint16_t.uint8_tP.uint32_t.uint8_t.uint8_t"></a> <a id="hogpd_8h_1ad74dcf6305bb1446dfef509fc64c0ae1"></a> int32\_t bk\_dm\_prf\_hogpd\_notify(uint16\_t gatt\_conn\_handle, uint8\_t \*data, uint32\_t len, uint8\_t is\_notify, uint8\_t report\_id)

<a id="id45"></a>

### Macros

<a id="c.HOGPD_ENABLE"></a>

<a id="hogpd_8h_1a6329e419851304315763f068d76fb5cf"></a> HOGPD\_ENABLE

关键配置：

- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_HOGPD`：启用 HOGPD demo。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_HOGPD_LOG_LEVEL`：配置 HOGPD demo 日志等级。
- `CONFIG_CLI`：启用 HOGPD CLI。

<a id="pan-hidd-service"></a>

## PAN/HIDD Service

PAN/HIDD service 提供 PAN 网络接入、PAN demo CLI、HID device demo 和相关重连处理。

API 参考：

<a id="id46"></a>

### Header File

- [pan\_service.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/bk_pan/pan_service.h)

<a id="id47"></a>

### Functions

<a id="_CPPv416pan_service_initv"></a>

<a id="_CPPv316pan_service_initv"></a> <a id="_CPPv216pan_service_initv"></a> <a id="pan_service_init__void"></a> <a id="pan__service_8h_1a901a17045b4981326b56ab66f2d85606"></a> int pan\_service\_init(void)
:   Initialize the PAN service.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv417cli_pan_demo_initv"></a>

<a id="_CPPv317cli_pan_demo_initv"></a> <a id="_CPPv217cli_pan_demo_initv"></a> <a id="cli_pan_demo_init__void"></a> <a id="pan__service_8h_1a0a2d101ab153aea22ee737a17287bbc0"></a> int cli\_pan\_demo\_init(void)
:   Register PAN demo CLI commands.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv422bt_start_pan_reconnectv"></a>

<a id="_CPPv322bt_start_pan_reconnectv"></a> <a id="_CPPv222bt_start_pan_reconnectv"></a> <a id="bt_start_pan_reconnect__void"></a> <a id="pan__service_8h_1a5e9341d8a85809d9f7733b60504a03e4"></a> void bt\_start\_pan\_reconnect(void)
:   Start PAN reconnect flow.

<a id="_CPPv428pan_show_tx_data_cache_countv"></a>

<a id="_CPPv328pan_show_tx_data_cache_countv"></a> <a id="_CPPv228pan_show_tx_data_cache_countv"></a> <a id="pan_show_tx_data_cache_count__void"></a> <a id="pan__service_8h_1a44a4d1792cf0d1583ab4a297c6070228"></a> void pan\_show\_tx\_data\_cache\_count(void)
:   Print the current PAN TX data cache count.

<a id="_CPPv418pan_service_deinitv"></a>

<a id="_CPPv318pan_service_deinitv"></a> <a id="_CPPv218pan_service_deinitv"></a> <a id="pan_service_deinit__void"></a> <a id="pan__service_8h_1a7d3337f4ba46e9ee676e12bad248c17f"></a> int pan\_service\_deinit(void)
:   Deinitialize the PAN service.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv419cli_pan_demo_deinitv"></a>

<a id="_CPPv319cli_pan_demo_deinitv"></a> <a id="_CPPv219cli_pan_demo_deinitv"></a> <a id="cli_pan_demo_deinit__void"></a> <a id="pan__service_8h_1a2c7a190bfa13d702bf80c6361f7d3803"></a> int cli\_pan\_demo\_deinit(void)
:   Unregister PAN demo CLI commands.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv432bt_pan_reconnect_failure_handlerv"></a>

<a id="_CPPv332bt_pan_reconnect_failure_handlerv"></a> <a id="_CPPv232bt_pan_reconnect_failure_handlerv"></a> <a id="bt_pan_reconnect_failure_handler__void"></a> <a id="pan__service_8h_1a30101a0eeb3abacfeee69e29053e4a63"></a> void bt\_pan\_reconnect\_failure\_handler(void)
:   Handle PAN reconnect failure.

<a id="id48"></a>

### Header File

- [hidd\_service.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/bk_pan/hidd_service.h)

<a id="id49"></a>

### Functions

<a id="_CPPv412bt_hidd_initv"></a>

<a id="_CPPv312bt_hidd_initv"></a> <a id="_CPPv212bt_hidd_initv"></a> <a id="bt_hidd_init__void"></a> <a id="hidd__service_8h_1a3a8e750e8fe1ee8be302a16bf3ae7b34"></a> void bt\_hidd\_init(void)
:   Initialize the Bluetooth HID Device demo service.

<a id="_CPPv414bt_hidd_deinitv"></a>

<a id="_CPPv314bt_hidd_deinitv"></a> <a id="_CPPv214bt_hidd_deinitv"></a> <a id="bt_hidd_deinit__void"></a> <a id="hidd__service_8h_1a00f4f3ca82e57eae7772e750462038ff"></a> void bt\_hidd\_deinit(void)
:   Deinitialize the Bluetooth HID Device demo service.

关键配置：

- `CONFIG_NET_PAN`：启用 PAN service。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE`：启用 BTDM service 组件。若未启用，PAN 子组件会
  单独编译 BT manager 和 storage 依赖。
- `CONFIG_CLI`：启用 PAN demo CLI。

<a id="storage"></a>

## Storage

`bluetooth_storage` 用于保存 BT link key、BLE bond 信息、local key、音量和地址 hash 等
蓝牙业务数据。

API 参考：

<a id="id50"></a>

### Header File

- [bluetooth\_storage.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/components/bk_bluetooth/service/dm/storage/bluetooth_storage.h)

<a id="id51"></a>

### Functions

<a id="_CPPv422bluetooth_storage_initv"></a>

<a id="_CPPv322bluetooth_storage_initv"></a> <a id="_CPPv222bluetooth_storage_initv"></a> <a id="bluetooth_storage_init__void"></a> <a id="bluetooth__storage_8h_1a926b0de69de14d5b18027e8405c56cb5"></a> int32\_t bluetooth\_storage\_init(void)
:   Initialize Bluetooth storage.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv424bluetooth_storage_deinitv"></a>

<a id="_CPPv324bluetooth_storage_deinitv"></a> <a id="_CPPv224bluetooth_storage_deinitv"></a> <a id="bluetooth_storage_deinit__void"></a> <a id="bluetooth__storage_8h_1afd6ca3cbd1c58320001ac7e26669aecf"></a> int32\_t bluetooth\_storage\_deinit(void)
:   Deinitialize Bluetooth storage.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv441bluetooth_storage_find_linkkey_info_indexP7uint8_tP7uint8_t"></a>

<a id="_CPPv341bluetooth_storage_find_linkkey_info_indexP7uint8_tP7uint8_t"></a> <a id="_CPPv241bluetooth_storage_find_linkkey_info_indexP7uint8_tP7uint8_t"></a> <a id="bluetooth_storage_find_linkkey_info_index__uint8_tP.uint8_tP"></a> <a id="bluetooth__storage_8h_1a7ab9ceb25c342f8466e802bcd5dfe491"></a> int32\_t bluetooth\_storage\_find\_linkkey\_info\_index(uint8\_t \*addr, uint8\_t \*key)
:   Find a BT link key record by address.

    参数
    :   - **addr** – Remote Bluetooth device address.
        - **key** – Output buffer for the link key. Pass NULL when only the index is needed.

    返回
    :   Record index on success, otherwise negative error code.

<a id="_CPPv435bluetooth_storage_save_linkkey_infoP7uint8_tP7uint8_t"></a>

<a id="_CPPv335bluetooth_storage_save_linkkey_infoP7uint8_tP7uint8_t"></a> <a id="_CPPv235bluetooth_storage_save_linkkey_infoP7uint8_tP7uint8_t"></a> <a id="bluetooth_storage_save_linkkey_info__uint8_tP.uint8_tP"></a> <a id="bluetooth__storage_8h_1a736be064ec8268fb0decb265dc750fde"></a> int32\_t bluetooth\_storage\_save\_linkkey\_info(uint8\_t \*addr, uint8\_t \*key)
:   Save or update a BT link key record.

    参数
    :   - **addr** – Remote Bluetooth device address.
        - **key** – BT link key buffer. The buffer length must be 16 bytes.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv434bluetooth_storage_del_linkkey_infoP7uint8_t"></a>

<a id="_CPPv334bluetooth_storage_del_linkkey_infoP7uint8_t"></a> <a id="_CPPv234bluetooth_storage_del_linkkey_infoP7uint8_t"></a> <a id="bluetooth_storage_del_linkkey_info__uint8_tP"></a> <a id="bluetooth__storage_8h_1a66882d56122bb72403571e7153b3b3e3"></a> int32\_t bluetooth\_storage\_del\_linkkey\_info(uint8\_t \*addr)
:   Delete a BT link key record.

    参数
    :   **addr** – Remote Bluetooth device address.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv434bluetooth_storage_update_to_newestP7uint8_t"></a>

<a id="_CPPv334bluetooth_storage_update_to_newestP7uint8_t"></a> <a id="_CPPv234bluetooth_storage_update_to_newestP7uint8_t"></a> <a id="bluetooth_storage_update_to_newest__uint8_tP"></a> <a id="bluetooth__storage_8h_1a8490d47c804e6c4640c6a10f5786b0ed"></a> int32\_t bluetooth\_storage\_update\_to\_newest(uint8\_t \*addr)
:   Move a BT link key record to the newest position.

    参数
    :   **addr** – Remote Bluetooth device address.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv441bluetooth_storage_get_newest_linkkey_infoP7uint8_tP7uint8_t"></a>

<a id="_CPPv341bluetooth_storage_get_newest_linkkey_infoP7uint8_tP7uint8_t"></a> <a id="_CPPv241bluetooth_storage_get_newest_linkkey_infoP7uint8_tP7uint8_t"></a> <a id="bluetooth_storage_get_newest_linkkey_info__uint8_tP.uint8_tP"></a> <a id="bluetooth__storage_8h_1af84a1446c9624c8792cb056edc8b66ca"></a> int32\_t bluetooth\_storage\_get\_newest\_linkkey\_info(uint8\_t \*addr, uint8\_t \*key)
:   Get the newest valid BT link key record.

    参数
    :   - **addr** – Output buffer for the remote Bluetooth device address.
        - **key** – Output buffer for the link key. Pass NULL when only the address is needed.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv436bluetooth_storage_clean_linkkey_infov"></a>

<a id="_CPPv336bluetooth_storage_clean_linkkey_infov"></a> <a id="_CPPv236bluetooth_storage_clean_linkkey_infov"></a> <a id="bluetooth_storage_clean_linkkey_info__void"></a> <a id="bluetooth__storage_8h_1ab5408f1f2cc4e72662038a959adf0ee1"></a> int32\_t bluetooth\_storage\_clean\_linkkey\_info(void)
:   Clear all BT link key records.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv431bluetooth_storage_sync_to_flashv"></a>

<a id="_CPPv331bluetooth_storage_sync_to_flashv"></a> <a id="_CPPv231bluetooth_storage_sync_to_flashv"></a> <a id="bluetooth_storage_sync_to_flash__void"></a> <a id="bluetooth__storage_8h_1a69c05551ca0d8abc3bac14e7171403ee"></a> int32\_t bluetooth\_storage\_sync\_to\_flash(void)
:   Synchronize Bluetooth storage data to flash.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv431bluetooth_storage_linkkey_debugv"></a>

<a id="_CPPv331bluetooth_storage_linkkey_debugv"></a> <a id="_CPPv231bluetooth_storage_linkkey_debugv"></a> <a id="bluetooth_storage_linkkey_debug__void"></a> <a id="bluetooth__storage_8h_1a0242a93b90209a965df9acfe78fff57e"></a> int32\_t bluetooth\_storage\_linkkey\_debug(void)
:   Print BT link key records for debugging.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv437bluetooth_storage_find_volume_by_addrP7uint8_tP7uint8_t"></a>

<a id="_CPPv337bluetooth_storage_find_volume_by_addrP7uint8_tP7uint8_t"></a> <a id="_CPPv237bluetooth_storage_find_volume_by_addrP7uint8_tP7uint8_t"></a> <a id="bluetooth_storage_find_volume_by_addr__uint8_tP.uint8_tP"></a> <a id="bluetooth__storage_8h_1a28114ec9374058244fe95ce9b7d4255e"></a> int32\_t bluetooth\_storage\_find\_volume\_by\_addr(uint8\_t \*addr, uint8\_t \*volume)
:   Find saved A2DP volume by address.

    参数
    :   - **addr** – Remote Bluetooth device address.
        - **volume** – Output A2DP volume.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv441bluetooth_storage_find_hfp_volume_by_addrP7uint8_tP7uint8_tP7uint8_t"></a>

<a id="_CPPv341bluetooth_storage_find_hfp_volume_by_addrP7uint8_tP7uint8_tP7uint8_t"></a> <a id="_CPPv241bluetooth_storage_find_hfp_volume_by_addrP7uint8_tP7uint8_tP7uint8_t"></a> <a id="bluetooth_storage_find_hfp_volume_by_addr__uint8_tP.uint8_tP.uint8_tP"></a> <a id="bluetooth__storage_8h_1a7fb41736f9a0446713c3352324fe19f2"></a> int32\_t bluetooth\_storage\_find\_hfp\_volume\_by\_addr(uint8\_t \*addr, uint8\_t \*mic\_vol, uint8\_t \*spk\_vol)
:   Find saved HFP microphone and speaker volume by address.

    参数
    :   - **addr** – Remote Bluetooth device address.
        - **mic\_vol** – Output HFP microphone volume.
        - **spk\_vol** – Output HFP speaker volume.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv429bluetooth_storage_save_volumeP7uint8_t7uint8_t"></a>

<a id="_CPPv329bluetooth_storage_save_volumeP7uint8_t7uint8_t"></a> <a id="_CPPv229bluetooth_storage_save_volumeP7uint8_t7uint8_t"></a> <a id="bluetooth_storage_save_volume__uint8_tP.uint8_t"></a> <a id="bluetooth__storage_8h_1acdab3d866ceb33478fa256a9415e70e4"></a> int32\_t bluetooth\_storage\_save\_volume(uint8\_t \*addr, uint8\_t volume)
:   Save A2DP volume for a remote device.

    参数
    :   - **addr** – Remote Bluetooth device address.
        - **volume** – A2DP volume.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv433bluetooth_storage_save_hfp_volumeP7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv333bluetooth_storage_save_hfp_volumeP7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv233bluetooth_storage_save_hfp_volumeP7uint8_t7uint8_t7uint8_t"></a> <a id="bluetooth_storage_save_hfp_volume__uint8_tP.uint8_t.uint8_t"></a> <a id="bluetooth__storage_8h_1a150052009bcf019b68dbed8e2d7f52e8"></a> int32\_t bluetooth\_storage\_save\_hfp\_volume(uint8\_t \*addr, uint8\_t type, uint8\_t volume)
:   Save HFP volume for a remote device.

    参数
    :   - **addr** – Remote Bluetooth device address.
        - **type** – Volume target. 0 indicates microphone and 1 indicates speaker.
        - **volume** – HFP volume.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv427bluetooth_storage_save_hashP7uint8_t8uint32_t"></a>

<a id="_CPPv327bluetooth_storage_save_hashP7uint8_t8uint32_t"></a> <a id="_CPPv227bluetooth_storage_save_hashP7uint8_t8uint32_t"></a> <a id="bluetooth_storage_save_hash__uint8_tP.uint32_t"></a> <a id="bluetooth__storage_8h_1a1750edfd6b44436d59dd83c6ae5c637a"></a> int32\_t bluetooth\_storage\_save\_hash(uint8\_t \*addr, uint32\_t hash)
:   Save an address hash for a remote device.

    参数
    :   - **addr** – Remote Bluetooth device address.
        - **hash** – Address hash value.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv435bluetooth_storage_find_addr_by_hashP7uint8_t8uint32_t"></a>

<a id="_CPPv335bluetooth_storage_find_addr_by_hashP7uint8_t8uint32_t"></a> <a id="_CPPv235bluetooth_storage_find_addr_by_hashP7uint8_t8uint32_t"></a> <a id="bluetooth_storage_find_addr_by_hash__uint8_tP.uint32_t"></a> <a id="bluetooth__storage_8h_1a632905048fee406fc7b73427bd507886"></a> int32\_t bluetooth\_storage\_find\_addr\_by\_hash(uint8\_t \*addr, uint32\_t hash)
:   Find a remote device address by hash.

    参数
    :   - **addr** – Output remote Bluetooth device address.
        - **hash** – Address hash value.

    返回
    :   0 on success, otherwise error code.

<a id="_CPPv437bluetooth_storage_get_bond_device_numv"></a>

<a id="_CPPv337bluetooth_storage_get_bond_device_numv"></a> <a id="_CPPv237bluetooth_storage_get_bond_device_numv"></a> <a id="bluetooth_storage_get_bond_device_num__void"></a> <a id="bluetooth__storage_8h_1a71afd77043f391507b05e6c323692e44"></a> uint8\_t bluetooth\_storage\_get\_bond\_device\_num(void)
:   Get the number of bonded BT devices.

    返回
    :   Number of bonded devices.

<a id="_CPPv431bluetooth_storage_get_bond_hashA_8uint16_t8uint32_t"></a>

<a id="_CPPv331bluetooth_storage_get_bond_hashA_8uint16_t8uint32_t"></a> <a id="_CPPv231bluetooth_storage_get_bond_hashA_8uint16_t8uint32_t"></a> <a id="bluetooth_storage_get_bond_hash__uint16_tA.uint32_t"></a> <a id="bluetooth__storage_8h_1a71bbf7430d43f9dad122cb2c72fa6f63"></a> uint32\_t bluetooth\_storage\_get\_bond\_hash(uint16\_t hasharray\[\], uint32\_t arraylen)
:   Get compact bond hash values.

    参数
    :   - **hasharray** – Output hash array.
        - **arraylen** – Number of elements in hasharray.

    返回
    :   Number of hash values written to hasharray.

<a id="id52"></a>

### Structures

<a id="_CPPv422bt_user_storage_elem_t"></a>

<a id="_CPPv322bt_user_storage_elem_t"></a> <a id="_CPPv222bt_user_storage_elem_t"></a> <a id="bt_user_storage_elem_t"></a> <a id="structbt__user__storage__elem__t"></a> struct bt\_user\_storage\_elem\_t
:   Per-device record. BR/EDR link-key info and (for a dual-mode device) the BLE bond now share ONE slot, keyed by address, instead of two parallel arrays.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bt_user_storage_elem_t4addrE"></a>

    <a id="_CPPv3N22bt_user_storage_elem_t4addrE"></a> <a id="_CPPv2N22bt_user_storage_elem_t4addrE"></a> <a id="bt_user_storage_elem_t::addr__uint8_tA"></a> <a id="structbt__user__storage__elem__t_1a9984d7016df5bb2a35bf9a917959029a"></a> uint8\_t addr\[6\]
    :   Device address (BR/EDR BD\_ADDR; also the BLE address when they match).

    <a id="_CPPv4N22bt_user_storage_elem_t8link_keyE"></a>

    <a id="_CPPv3N22bt_user_storage_elem_t8link_keyE"></a> <a id="_CPPv2N22bt_user_storage_elem_t8link_keyE"></a> <a id="bt_user_storage_elem_t::link_key__uint8_tA"></a> <a id="structbt__user__storage__elem__t_1a06af380ebca28267ff65008015b065f4"></a> uint8\_t link\_key\[16\]
    :   BR/EDR link key (all-zero for a BLE-only record).

    <a id="_CPPv4N22bt_user_storage_elem_t11a2dp_volumeE"></a>

    <a id="_CPPv3N22bt_user_storage_elem_t11a2dp_volumeE"></a> <a id="_CPPv2N22bt_user_storage_elem_t11a2dp_volumeE"></a> <a id="bt_user_storage_elem_t::a2dp_volume__uint8_t"></a> <a id="structbt__user__storage__elem__t_1a991bccc2473a493516ce166fc56aeff0"></a> uint8\_t a2dp\_volume
    :   Saved A2DP volume.

    <a id="_CPPv4N22bt_user_storage_elem_t4hashE"></a>

    <a id="_CPPv3N22bt_user_storage_elem_t4hashE"></a> <a id="_CPPv2N22bt_user_storage_elem_t4hashE"></a> <a id="bt_user_storage_elem_t::hash__uint32_t"></a> <a id="structbt__user__storage__elem__t_1aaef82d1afab00dc7de444d6345b683d4"></a> uint32\_t hash
    :   Address hash used for compact lookup.

    <a id="_CPPv4N22bt_user_storage_elem_t11hfp_mic_volE"></a>

    <a id="_CPPv3N22bt_user_storage_elem_t11hfp_mic_volE"></a> <a id="_CPPv2N22bt_user_storage_elem_t11hfp_mic_volE"></a> <a id="bt_user_storage_elem_t::hfp_mic_vol__uint8_t"></a> <a id="structbt__user__storage__elem__t_1a34783d1fe9028c9ff6e2099b7e30c616"></a> uint8\_t hfp\_mic\_vol
    :   Saved HFP microphone volume.

    <a id="_CPPv4N22bt_user_storage_elem_t11hfp_spk_volE"></a>

    <a id="_CPPv3N22bt_user_storage_elem_t11hfp_spk_volE"></a> <a id="_CPPv2N22bt_user_storage_elem_t11hfp_spk_volE"></a> <a id="bt_user_storage_elem_t::hfp_spk_vol__uint8_t"></a> <a id="structbt__user__storage__elem__t_1a63bd87bf167722cd9643b0e2beb21b4a"></a> uint8\_t hfp\_spk\_vol
    :   Saved HFP speaker volume.

<a id="_CPPv417bt_user_storage_t"></a>

<a id="_CPPv317bt_user_storage_t"></a> <a id="_CPPv217bt_user_storage_t"></a> <a id="bt_user_storage_t"></a> <a id="structbt__user__storage__t"></a> struct bt\_user\_storage\_t
:   Bluetooth user storage data persisted by the service layer.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bt_user_storage_t3devE"></a>

    <a id="_CPPv3N17bt_user_storage_t3devE"></a> <a id="_CPPv2N17bt_user_storage_t3devE"></a> <a id="bt_user_storage_t::dev__bt_user_storage_elem_tA"></a> <a id="structbt__user__storage__t_1a37db48abd2a9b0b71a3557c382ffe2e2"></a> [bt\_user\_storage\_elem\_t](#_CPPv422bt_user_storage_elem_t "bt_user_storage_elem_t") dev\[BT\_LINKKEY\_MAX\_SAVE\_COUNT\]
    :   Per-device BR/EDR \+ BLE records.

<a id="id53"></a>

### Macros

<a id="c.BT_STORAGE_KEY"></a>

<a id="bluetooth__storage_8h_1adae9eded8ad79b9d8b4b75d53861b628"></a> BT\_STORAGE\_KEY
:   Persistent storage key used for Bluetooth user information.

<a id="c.BT_LINKKEY_MAX_SAVE_COUNT"></a>

<a id="bluetooth__storage_8h_1ac484124b075d2d971d0784b3e21bac0a"></a> BT\_LINKKEY\_MAX\_SAVE\_COUNT
:   Maximum number of BT link key or BLE bond records saved by this module.

<a id="id54"></a>

## 使用建议

需要快速构建典型蓝牙业务流程时，可参考
[蓝牙开发者指南](../../developer-guide/bluetooth.md)，其中包含常见蓝牙功能的设计说明和使用建议。

使用 service 层前，请确认工程已启用对应的 Bluetooth、Profile、音频或网络 Kconfig 选项。
