# Profile 服务



## 概述

Bluetooth Service Layer 是 AP 侧 `bk_bluetooth` 组件中的上层封装，位于
`ap/components/bk_bluetooth/service/dm`。它基于 Bluetooth SDK API 实现常见业务流程，
例如连接管理、自动重连、音频链路控制、AVRCP 控制和 HFP HF 操作。

重要

Service Layer 面向常见蓝牙业务场景提供组合封装；底层能力和精细化控制可继续参考
`ap/include/components/bluetooth` 下的 Bluetooth SDK API。


## 整体结构

Service Layer 由若干 profile service 和公共管理模块组成：


- BT manager：统一管理 BT 配对、可发现/可连接状态、自动重连和 profile 连接回调。

- A2DP Sink service：提供蓝牙音频 Sink 场景的连接管理、媒体数据事件和 codec 能力封装。

- AVRCP CT/TG service：提供播放器控制、曲目信息查询和绝对音量通知等 AVRCP 流程封装。

- HFP HF service：提供免提通话、SCO 音频、音量和 AT 命令交互封装。

- BLE GATT framework：提供 BLE GAP、GATTS、GATTC 和连接上下文管理封装。

- PAN/HIDD service：提供 PAN 网络接入和 HID 设备 demo 相关封装。


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

- `CONFIG_BLE_LE_AUDIO`：启用 LE Audio BAP API，并链接双模 Ethermind LE Audio host 库；`projects/bluetooth/le_audio` 工程需开启。

- `CONFIG_NET_PAN`：启用 PAN 网络 service。

- `CONFIG_CLI`：启用 BLE GATT、PAN、HOGPD 等 demo CLI 命令。


## BT Manager

BT manager 负责统一处理 BT 工作模式、配对状态、自动重连和 profile 回调注册。A2DP、
AVRCP、HFP、PAN 等 service 会通过 BT manager 协同连接和断开流程。

API 参考：


### Header File


- [bk_bluetooth/service/dm/bt_manager/bt_manager.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/bt_manager/bt_manager.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/bt_manager/bt_manager.h")


### Functions

int bt_manager_register_callback([btm_callback_s](#_CPPv414btm_callback_s "btm_callback_s") *cb)
:   Register callback functions for the Bluetooth manager.

    参数
    :   **cb** – Pointer to the callback structure.

    返回
    :   0 on success, otherwise error code.

void bt_manager_start_reconnect(uint8_t *addr, uint8_t immediate)
:   Start the reconnection process to a specified device.

    参数
    :   - **addr** – Pointer to the address of the device to reconnect to.

        - **immediate** – Whether to initiate the reconnection immediately.

void bt_manager_set_mode(uint8_t mode)
:   Set the operation mode of the Bluetooth manager.

    参数
    :   **mode** – The mode to set.

uint8_t bt_manager_get_mode(void)
:   Get the current operation mode of the Bluetooth manager.

    返回
    :   The current operation mode.

int bt_manager_init(const [bt_manager_cfg_t](#_CPPv416bt_manager_cfg_t "bt_manager_cfg_t") *cfg)
:   Initialize the Bluetooth manager.

    返回
    :   0 on success, otherwise error code.

int bt_manager_deinit(void)
:   Deinitialize the Bluetooth manager.

    返回
    :   0 on success, otherwise error code.

uint8_t bt_manager_get_connect_state(void)
:   Get the current connection state of the Bluetooth manager.

    返回
    :   The current connection state.

void bt_manager_set_connect_state(uint8_t state)
:   Set the current connection state of the Bluetooth manager.

    参数
    :   **state** – The connection state to set.

void bt_manager_get_reconnect_device(uint8_t *addr)
:   Get the address of the device to reconnect to.

    参数
    :   **addr** – Pointer to store the address of the device to reconnect to.

uint8_t *bt_manager_get_connected_device(void)
:   Get the address of the currently connected device.

    返回
    :   Pointer to the address of the currently connected device.

int bt_manager_unregister_callback(uint8_t index)
:   Unregister a callback function by index.

    参数
    :   **index** – The index of the callback to unregister.

    返回
    :   0 on success, otherwise error code.

void bk_bt_enter_pairing_mode(uint8_t is_visible)
:   Enter the Bluetooth pairing mode.

void bt_manager_clean_bond(void)
:   Clean the bonded devices.

void bt_manager_set_auto_accept_connection(uint8_t type, uint8_t accept)

void bt_manager_clear_reconnect_info(void)
:   Clear the reconnect information.


### Structures

struct btm_callback_s
:   Structure for Bluetooth manager callbacks.

struct bt_manager_cfg_t
:   Bluetooth manager initialization configuration.


### Type Definitions

typedef void (*btm_gap_event_cb)([bk_gap_bt_cb_event_t](dual_bt.md#_CPPv420bk_gap_bt_cb_event_t "bk_gap_bt_cb_event_t") event, [bk_bt_gap_cb_param_t](dual_bt.md#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t") *param)
:   Callback function type for GAP (Generic Access Profile) events.

    Param event
    :   The GAP event type.

    Param param
    :   Pointer to the GAP callback parameter structure.

typedef void (*btm_start_profile_connect_cb)(uint8_t *remote_addr)
:   Callback function type for starting profile connection.

    Param remote_addr
    :   Pointer to the remote device address.

typedef void (*btm_start_profile_disconnect_cb)(uint8_t *remote_addr)
:   Callback function type for starting profile disconnection.

    Param remote_addr
    :   Pointer to the remote device address.

typedef void (*btm_stop_profile_connect_cb)(void)
:   Callback function type for stopping profile connection.

typedef void (*btm_reconnect_fail_cb)(void)
:   Callback function type for reconnect failure.


### Enumerations

enum [anonymous]
:   Enumeration of Bluetooth manager operation modes.


    *Values:*

    enumerator BT_MNG_MODE_PAIRING
    :   connectable and discoverable

    enumerator BT_MNG_MODE_RECONNECTING
    :   no-connectable and no-discoverable

    enumerator BT_MNG_MODE_CONNECTEED
    :   no-connectable and no-discoverable

    enumerator BT_MNG_MODE_CONNECTABLE
    :   connectable and no-discoverable

    enumerator BT_MNG_MODE_IDLE
    :   no-connectable and no-discoverable

    enumerator BT_MNG_MODE_DISCOVERABLE_ONLY
    :   no-connectable and discoverable

    enumerator BT_MNG_MODE_ALL_OFF
    :   no-connectable and no-discoverable

enum [anonymous]
:   Enumeration of Bluetooth connection states.


    *Values:*

    enumerator BT_STATE_IDLE
    :   Bluetooth is in idle state.

    enumerator BT_STATE_WAIT_FOR_RECONNECT
    :   Waiting to initiate a reconnection.

    enumerator BT_STATE_RECONNECTING
    :   Currently in the process of reconnecting.

    enumerator BT_STATE_LINK_CONNECTED
    :   The link layer is connected.

    enumerator BT_STATE_PROFILE_CONNECTED
    :   The profile is connected.

    enumerator BT_STATE_KEY_MISSING
    :   The encryption key is missing.

enum [anonymous]
:   *Values:*

    enumerator PAIRING_STATE_IDLE

    enumerator PAIRING_STATE_PREPARATION

    enumerator PAIRING_STATE_WAIT_CFM

enum [anonymous]
:   *Values:*

    enumerator BT_MNG_AUTO_ACCEPT_CONNECTION_ACL

    enumerator BT_MNG_AUTO_ACCEPT_CONNECTION_SCO


## A2DP Sink Service

A2DP Sink service 封装蓝牙音频 Sink 流程，包括 profile 初始化、连接控制、音频配置事件、
媒体数据事件和可选 AAC 支持。

API 参考：


### Header File


- [bk_bluetooth/service/dm/a2dp/bk_a2dp_sink_service.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/a2dp/bk_a2dp_sink_service.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/a2dp/bk_a2dp_sink_service.h")


### Functions

int bk_a2dp_sink_register_event_cb([bk_a2dp_sink_event_cb_t](#_CPPv423bk_a2dp_sink_event_cb_t "bk_a2dp_sink_event_cb_t") cb, void *user_data)
:   Register the application event callback. Call before service init.

int bk_a2dp_sink_service_init(const [bk_a2dp_sink_cfg_t](#_CPPv418bk_a2dp_sink_cfg_t "bk_a2dp_sink_cfg_t") *cfg)
:   Initialize A2DP sink profile and register internal Bluetooth callbacks.

int bk_a2dp_sink_service_deinit(void)
:   Deinitialize A2DP sink profile and release service resources.

int bk_a2dp_sink_connect(const uint8_t bda[6])
:   Connect A2DP sink to the specified remote device.

int bk_a2dp_sink_disconnect(const uint8_t bda[6])
:   Disconnect A2DP sink from the specified remote device.


### Structures

struct bk_a2dp_sink_conn_t
:   A2DP connection event payload.

struct bk_a2dp_media_data_t
:   Media packet payload. The buffer is only valid during the event callback.

struct bk_a2dp_sink_cfg_t
:   A2DP sink service configuration.


### Type Definitions

typedef void (*bk_a2dp_sink_event_cb_t)([bk_a2dp_sink_evt_t](#_CPPv418bk_a2dp_sink_evt_t "bk_a2dp_sink_evt_t") evt, void *arg, void *user_data)
:   A2DP sink service event callback.

    The callback is invoked from the Bluetooth stack/service context. Copy data before posting it to another task if it must live beyond the callback.


### Enumerations

enum bk_a2dp_sink_evt_t
:   *Values:*

    enumerator BK_A2DP_SINK_EVT_CONNECTED
    :   arg: [bk_a2dp_sink_conn_t](#structbk__a2dp__sink__conn__t "#structbk__a2dp__sink__conn__t") *

    enumerator BK_A2DP_SINK_EVT_DISCONNECTED
    :   arg: [bk_a2dp_sink_conn_t](#structbk__a2dp__sink__conn__t "#structbk__a2dp__sink__conn__t") *

    enumerator BK_A2DP_SINK_EVT_AUDIO_CFG
    :   arg: [bk_a2dp_mcc_t](dual_bt.md#structbk__a2dp__mcc__t "dual_bt.md#structbk__a2dp__mcc__t") *

    enumerator BK_A2DP_SINK_EVT_STREAM_START
    :   arg: [bk_a2dp_mcc_t](dual_bt.md#structbk__a2dp__mcc__t "dual_bt.md#structbk__a2dp__mcc__t") *

    enumerator BK_A2DP_SINK_EVT_STREAM_SUSPEND
    :   arg: NULL

    enumerator BK_A2DP_SINK_EVT_MEDIA_DATA
    :   arg: [bk_a2dp_media_data_t](#structbk__a2dp__media__data__t "#structbk__a2dp__media__data__t") *

enum bk_a2dp_sink_codec_t
:   Codec capabilities exposed by the sink service.


    *Values:*

    enumerator BK_A2DP_SINK_CODEC_SBC

    enumerator BK_A2DP_SINK_CODEC_AAC

关键配置：


- `CONFIG_BT`：启用 BT。

- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE`：启用 A2DP Sink service 编译。

- `CONFIG_AUDIO_PLAY`：启用音频播放路径，用于媒体数据输出。


## AVRCP CT/TG Service

AVRCP service 分为 Controller 和 Target 两个角色。Controller 侧用于播放控制、音量按键、
曲目信息查询等；Target 侧用于绝对音量通知和本地音量状态管理。

API 参考：


### Header File


- [bk_bluetooth/service/dm/avrcp/bk_avrcp_ct_service.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/avrcp/bk_avrcp_ct_service.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/avrcp/bk_avrcp_ct_service.h")


### Functions

int bk_avrcp_ct_register_event_cb([bk_avrcp_ct_event_cb_t](#_CPPv422bk_avrcp_ct_event_cb_t "bk_avrcp_ct_event_cb_t") cb, void *user_data)
:   Register the application CT event callback. Call before service init.

int bk_avrcp_ct_service_init(const [bk_avrcp_ct_cfg_t](#_CPPv417bk_avrcp_ct_cfg_t "bk_avrcp_ct_cfg_t") *cfg)
:   Initialize AVRCP controller role and internal state.

int bk_avrcp_ct_service_deinit(void)
:   Deinitialize AVRCP controller role and release resources.

void bk_avrcp_ct_service_notify_a2dp_state(uint8_t connected, const uint8_t bda[6])
:   Notify CT service of A2DP connection state for optional AVRCP auto-connect.

int bk_avrcp_stop_reconnect(void)
:   Stop the pending AVRCP controller auto-connect timer, if any.

int bk_avrcp_ct_connect(const uint8_t bda[6])
:   Connect AVRCP controller to the specified remote device.

int bk_avrcp_ct_disconnect(const uint8_t bda[6])
:   Disconnect AVRCP controller from the specified remote device.

int bk_avrcp_ct_is_connected(void)
:   Return non-zero when AVRCP controller is connected.

int bk_avrcp_ct_play(void)
:   Send AVRCP play passthrough command.

int bk_avrcp_ct_pause(void)
:   Send AVRCP pause passthrough command.

int bk_avrcp_ct_next(void)
:   Send AVRCP next-track passthrough command.

int bk_avrcp_ct_prev(void)
:   Send AVRCP previous-track passthrough command.

int bk_avrcp_ct_rewind(uint32_t ms)
:   Send AVRCP rewind command for the requested duration in milliseconds.

int bk_avrcp_ct_fast_forward(uint32_t ms)
:   Send AVRCP fast-forward command for the requested duration in milliseconds.

int bk_avrcp_ct_vol_up(void)
:   Increase local volume and notify/send passthrough according to peer support.

int bk_avrcp_ct_vol_down(void)
:   Decrease local volume and notify/send passthrough according to peer support.

int bk_avrcp_ct_get_attr(uint32_t attr_id)
:   Request media element attributes. Pass 0 to request the default title attr.


### Structures

struct bk_avrcp_ct_cfg_t
:   AVRCP controller service configuration.


### Type Definitions

typedef void (*bk_avrcp_ct_event_cb_t)([bk_avrcp_ct_evt_t](#_CPPv417bk_avrcp_ct_evt_t "bk_avrcp_ct_evt_t") evt, void *arg, void *user_data)
:   AVRCP controller event callback.


### Enumerations

enum bk_avrcp_ct_evt_t
:   *Values:*

    enumerator BK_AVRCP_CT_EVT_CONNECTED
    :   arg: uint8_t remote_bda[6]

    enumerator BK_AVRCP_CT_EVT_DISCONNECTED
    :   arg: uint8_t remote_bda[6]

    enumerator BK_AVRCP_CT_EVT_PLAY_STATUS_CHANGED
    :   arg: uint8_t * playback status

    enumerator BK_AVRCP_CT_EVT_TRACK_CHANGED
    :   arg: uint64_t * track id

    enumerator BK_AVRCP_CT_EVT_ELEM_ATTR_RSP
    :   arg: [bk_avrcp_ct_cb_param_t](dual_bt.md#unionbk__avrcp__ct__cb__param__t "dual_bt.md#unionbk__avrcp__ct__cb__param__t") *

    enumerator BK_AVRCP_CT_EVT_PLAY_POS_CHANGED
    :   arg: uint32_t * playing position in milliseconds


### Header File


- [bk_bluetooth/service/dm/avrcp/bk_avrcp_tg_service.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/avrcp/bk_avrcp_tg_service.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/avrcp/bk_avrcp_tg_service.h")


### Functions

int bk_avrcp_tg_register_event_cb([bk_avrcp_tg_event_cb_t](#_CPPv422bk_avrcp_tg_event_cb_t "bk_avrcp_tg_event_cb_t") cb, void *user_data)
:   Register the application TG event callback. Call before service init.

int bk_avrcp_tg_service_init(const [bk_avrcp_tg_cfg_t](#_CPPv417bk_avrcp_tg_cfg_t "bk_avrcp_tg_cfg_t") *cfg)
:   Initialize AVRCP target role and absolute-volume notification support.

int bk_avrcp_tg_service_deinit(void)
:   Deinitialize AVRCP target role and release resources.

int bk_avrcp_tg_disconnect(const uint8_t bda[6])
:   Disconnect AVRCP target from the specified remote device.

int bk_avrcp_tg_is_connected(void)
:   Return non-zero when AVRCP target is connected.

int bk_avrcp_tg_notify_volume_change(uint8_t vol_0_7f)
:   Notify the peer of a local volume change if it registered for the event.

int bk_avrcp_tg_set_local_volume(uint8_t vol, const uint8_t *bda)
:   Update local volume, save it for the device address, and emit TG event.

uint8_t bk_avrcp_tg_get_local_volume_value(void)
:   Return the current local volume in the AVRCP 0x00-0x7f range.

void bk_avrcp_tg_emit_current_volume(void)
:   Emit the current local volume through the registered TG event callback.


### Structures

struct bk_avrcp_tg_cfg_t
:   AVRCP target service configuration.


### Type Definitions

typedef void (*bk_avrcp_tg_event_cb_t)([bk_avrcp_tg_evt_t](#_CPPv417bk_avrcp_tg_evt_t "bk_avrcp_tg_evt_t") evt, void *arg, void *user_data)
:   AVRCP target event callback.


### Enumerations

enum bk_avrcp_tg_evt_t
:   *Values:*

    enumerator BK_AVRCP_TG_EVT_CONNECTED
    :   arg: uint8_t remote_bda[6]

    enumerator BK_AVRCP_TG_EVT_DISCONNECTED
    :   arg: uint8_t remote_bda[6]

    enumerator BK_AVRCP_TG_EVT_VOLUME_CHANGED
    :   arg: uint8_t * volume in 0x00-0x7f range

关键配置：


- `CONFIG_BT`：启用 BT。

- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE`：启用 AVRCP CT/TG service 编译。


## HFP HF Service

HFP HF service 封装免提设备流程，包括 service level 连接、SCO 音频连接、上下行语音数据、
AG 音量控制、通话控制和 AT 命令交互。

API 参考：


### Header File


- [bk_bluetooth/service/dm/hfp/bk_hfp_hf_service.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/hfp/bk_hfp_hf_service.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/hfp/bk_hfp_hf_service.h")


### Functions

int bk_hfp_hf_register_event_cb([bk_hfp_hf_event_cb_t](#_CPPv420bk_hfp_hf_event_cb_t "bk_hfp_hf_event_cb_t") cb, void *user_data)
:   Register the application event callback.

    Call this function before [bk_hfp_hf_service_init()](#bk__hfp__hf__service_8h_1a8e2e2a55820801e39c2a72c71d4ce81c "#bk__hfp__hf__service_8h_1a8e2e2a55820801e39c2a72c71d4ce81c").

    参数
    :   - **cb** – Event callback.

        - **user_data** – User context passed back in the callback.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_service_init(uint8_t msbc_supported)
:   Initialize the HFP HF service.

    参数
    :   **msbc_supported** – Non-zero to enable mSBC support, zero to use CVSD only.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_service_deinit(void)
:   Deinitialize the HFP HF service.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_connect(const uint8_t bda[6])
:   Connect to a remote HFP Audio Gateway.

    参数
    :   **bda** – Remote Bluetooth device address.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_disconnect(const uint8_t bda[6])
:   Disconnect from a remote HFP Audio Gateway.

    参数
    :   **bda** – Remote Bluetooth device address.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_query_current_calls(void)
:   Query the current call list from the connected Audio Gateway.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_volume_update(uint8_t type, uint8_t volume)
:   Update speaker or microphone volume on the connected Audio Gateway.

    参数
    :   - **type** – Volume target, such as speaker or microphone.

        - **volume** – Volume value.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_send_custom_cmd(const char *cmd)
:   Send a custom AT command to the connected Audio Gateway.

    参数
    :   **cmd** – AT command string.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_query_current_operator_name(void)
:   Query the current operator name.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_retrieve_subscriber_info(void)
:   Retrieve subscriber number information.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_send_dtmf(const char *code)
:   Send a DTMF code.

    参数
    :   **code** – DTMF code string.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_request_last_voice_tag_number(void)
:   Request the last voice tag number.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_send_nrec(void)
:   Send the NREC command.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_start_voice_recognition(void)
:   Start voice recognition on the connected Audio Gateway.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_stop_voice_recognition(void)
:   Stop voice recognition on the connected Audio Gateway.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_dial(const char *num)
:   Dial a phone number.

    参数
    :   **num** – Phone number string.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_dial_memory(int32_t location)
:   Dial a number from the Audio Gateway memory location.

    参数
    :   **location** – Memory location index.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_redial(void)
:   Redial the last dialed number.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_answer_call(void)
:   Answer an incoming call.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_reject_call(void)
:   Reject an incoming call.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_send_chld_cmd(uint8_t op)
:   Send a call hold command.

    参数
    :   **op** – CHLD operation value.

    返回
    :   0 on success, otherwise error code.

int bk_hfp_hf_send_btrh_cmd(uint8_t op)
:   Send a call response and hold command.

    参数
    :   **op** – BTRH operation value.

    返回
    :   0 on success, otherwise error code.


### Structures

struct bk_hfp_hf_conn_info_t
:   Service-level connection event payload.

struct bk_hfp_hf_audio_info_t
:   SCO audio connection event payload.

struct bk_hfp_hf_volume_info_t
:   AG volume control event payload.

struct bk_hfp_hf_voice_data_t
:   Downlink voice packet. The buffer is only valid during the event callback.

struct bk_hfp_hf_at_response_info_t
:   AT response event payload.

struct bk_hfp_hf_call_info_t
:   Call activity indicator payload (+CIEV call).

struct bk_hfp_hf_call_setup_info_t
:   Call setup indicator payload (+CIEV callsetup).

struct bk_hfp_hf_clip_info_t
:   Calling line identification payload (+CLIP). Strings valid only in callback.

struct bk_hfp_hf_btrh_info_t
:   Call hold and response status payload (+BTRH).

struct bk_hfp_hf_unknown_data_info_t
:   Raw/unknown AT data from the AG (e.g. +CGMI response). Valid only in callback.


### Type Definitions

typedef void (*bk_hfp_hf_event_cb_t)([bk_hfp_hf_evt_t](#_CPPv415bk_hfp_hf_evt_t "bk_hfp_hf_evt_t") evt, void *arg, void *user_data)
:   HFP HF service event callback.

    Invoked from the Bluetooth stack/service context. Copy data before posting it to another task if it must live beyond the callback.

    Param evt
    :   Event ID.

    Param arg
    :   Event payload. The concrete type depends on the event ID.

    Param user_data
    :   User context passed to [bk_hfp_hf_register_event_cb()](#bk__hfp__hf__service_8h_1a559ac4b1ac63777e4ea49141f1735b43 "#bk__hfp__hf__service_8h_1a559ac4b1ac63777e4ea49141f1735b43").


### Enumerations

enum bk_hfp_hf_evt_t
:   *Values:*

    enumerator BK_HFP_HF_EVT_CONNECTED
    :   HFP service-level connection is established. Event data: [bk_hfp_hf_conn_info_t](#structbk__hfp__hf__conn__info__t "#structbk__hfp__hf__conn__info__t").

    enumerator BK_HFP_HF_EVT_DISCONNECTED
    :   HFP service-level connection is disconnected. Event data: [bk_hfp_hf_conn_info_t](#structbk__hfp__hf__conn__info__t "#structbk__hfp__hf__conn__info__t").

    enumerator BK_HFP_HF_EVT_AUDIO_CONNECTED
    :   SCO audio connection is established. Event data: [bk_hfp_hf_audio_info_t](#structbk__hfp__hf__audio__info__t "#structbk__hfp__hf__audio__info__t").

    enumerator BK_HFP_HF_EVT_AUDIO_DISCONNECTED
    :   SCO audio connection is disconnected. Event data: NULL.

    enumerator BK_HFP_HF_EVT_VOLUME_CHANGED
    :   Audio Gateway volume state is changed. Event data: [bk_hfp_hf_volume_info_t](#structbk__hfp__hf__volume__info__t "#structbk__hfp__hf__volume__info__t").

    enumerator BK_HFP_HF_EVT_VOICE_DATA
    :   Downlink SCO voice packet is received. Event data: [bk_hfp_hf_voice_data_t](#structbk__hfp__hf__voice__data__t "#structbk__hfp__hf__voice__data__t").

    enumerator BK_HFP_HF_EVT_AT_RESPONSE
    :   AT command response is received. Event data: [bk_hfp_hf_at_response_info_t](#structbk__hfp__hf__at__response__info__t "#structbk__hfp__hf__at__response__info__t").

    enumerator BK_HFP_HF_EVT_RING
    :   Incoming call ring indication is received. Event data: NULL.

    enumerator BK_HFP_HF_EVT_CALL_IND
    :   Call activity indicator is changed. Event data: [bk_hfp_hf_call_info_t](#structbk__hfp__hf__call__info__t "#structbk__hfp__hf__call__info__t").

    enumerator BK_HFP_HF_EVT_CALL_SETUP_IND
    :   Call setup indicator is changed. Event data: [bk_hfp_hf_call_setup_info_t](#structbk__hfp__hf__call__setup__info__t "#structbk__hfp__hf__call__setup__info__t").

    enumerator BK_HFP_HF_EVT_CLIP
    :   Calling line identification is received. Event data: [bk_hfp_hf_clip_info_t](#structbk__hfp__hf__clip__info__t "#structbk__hfp__hf__clip__info__t").

    enumerator BK_HFP_HF_EVT_BTRH
    :   Call hold and response status is received. Event data: [bk_hfp_hf_btrh_info_t](#structbk__hfp__hf__btrh__info__t "#structbk__hfp__hf__btrh__info__t").

    enumerator BK_HFP_HF_EVT_UNKNOWN_DATA
    :   Raw AT data is received from the Audio Gateway. Event data: [bk_hfp_hf_unknown_data_info_t](#structbk__hfp__hf__unknown__data__info__t "#structbk__hfp__hf__unknown__data__info__t").

关键配置：


- `CONFIG_BT`：启用 BT。

- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE`：启用 HFP HF service 编译。

- `CONFIG_AUDIO_PLAY`：启用 SCO 音频播放/处理路径。


## BLE GATT Framework

BLE GATT framework 提供 GAP、GATTS、GATTC 和连接上下文管理封装，供 AT 层和部分业务组件
复用。它基于 Bluetooth SDK API 构建，常用于快速创建 BLE GATT Server/Client 测试和业务流程。

API 参考：


### Header File


- [bk_bluetooth/service/dm/ble/gatt/dm_gatt.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gatt.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gatt.h")


### Functions

int bk_dm_prf_gap_main([cli_gatt_param_t](#_CPPv416cli_gatt_param_t "cli_gatt_param_t") *param)
:   Initialize the BLE GAP framework.

    参数
    :   **param** – Optional initialization parameters. Pass NULL to use defaults.

    返回
    :   0 on success, otherwise error code.

int bk_dm_prf_gap_deinit(void)
:   Deinitialize the BLE GAP framework.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gap_disable_all(void)
:   Disable all GAP framework roles and activities.

    返回
    :   0 on success, otherwise error code.

int bk_dm_prf_gap_add_gap_callback(void *cb)
:   Register a BLE GAP callback.

    参数
    :   **cb** – Callback pointer. The callback type is defined by the BLE GAP SDK.

    返回
    :   0 on success, otherwise error code.

int32_t dm_gatt_get_authen_status(uint8_t *nominal_addr, uint8_t *nominal_addr_type, uint8_t *identity_addr, uint8_t *identity_addr_type)
:   Get authentication address mapping information.

    参数
    :   - **nominal_addr** – Nominal address input buffer.

        - **nominal_addr_type** – Nominal address type output buffer.

        - **identity_addr** – Identity address output buffer.

        - **identity_addr_type** – Identity address type output buffer.

    返回
    :   0 on success, otherwise error code.

int32_t dm_gatt_find_id_info_by_nominal_info(uint8_t *nominal_addr, uint8_t nominal_addr_type, uint8_t *identity_addr, uint8_t *identity_addr_type)
:   Find identity address information by nominal address information.

    参数
    :   - **nominal_addr** – Nominal address input buffer.

        - **nominal_addr_type** – Nominal address type.

        - **identity_addr** – Identity address output buffer.

        - **identity_addr_type** – Identity address type output buffer.

    返回
    :   0 on success, otherwise error code.

int bk_dm_prf_gap_passkey_reply(uint8_t accept, uint32_t passkey)
:   Reply to a BLE passkey request.

    参数
    :   - **accept** – Non-zero to accept the passkey, zero to reject.

        - **passkey** – Passkey value.

    返回
    :   0 on success, otherwise error code.

int bk_dm_prf_gap_set_security_method(uint8_t iocap, uint8_t auth_req, uint8_t key_distr)
:   Configure BLE security method.

    参数
    :   - **iocap** – IO capability.

        - **auth_req** – Authentication request flags.

        - **key_distr** – Key distribution flags.

    返回
    :   0 on success, otherwise error code.

bool bk_dm_prf_gap_is_linkkey_distr_from_ltk(void)
:   Check whether link keys are distributed from LTK information.

    返回
    :   true if link keys are distributed from LTK, otherwise false.

int bk_dm_prf_gap_create_bond(uint8_t *addr)
:   Create a BLE bond with a peer device.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

int bk_dm_prf_gap_remove_bond(uint8_t *addr)
:   Remove BLE bond information for a peer device.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

uint32_t bk_dm_prf_gap_get_bonded_count(void)
:   Get the number of bonded BLE devices.

    返回
    :   Number of bonded devices.

int32_t bk_dm_prf_gap_clean_bond(void)
:   Clear all BLE bond information.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gap_show_bond_list(void)
:   Print the BLE bond list for debugging.

    返回
    :   0 on success, otherwise error code.

[bk_ble_bond_dev_t](dual_ble.md#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") *bk_dm_prf_gap_get_bond_info_by_addr(uint8_t *addr)
:   Get BLE bond information by address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   Pointer to bond information on success, otherwise NULL.

uint8_t bk_dm_prf_gap_bond_info_foreach(int32_t (*func)([bk_ble_bond_dev_t](dual_ble.md#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") *info, void *arg), void *arg)
:   Iterate over BLE bond information.

    参数
    :   - **func** – Callback invoked for each bond record.

        - **arg** – User argument passed to the callback.

    返回
    :   Number of visited bond records.

int32_t bk_dm_prf_gap_clean_local_key(void)
:   Clear local BLE security keys.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gap_update_whitelist(uint8_t add_remove, uint8_t *addr, uint8_t addr_type)
:   Add or remove a BLE peer from the controller white list.

    参数
    :   - **add_remove** – Non-zero to add the peer, zero to remove it.

        - **addr** – Peer BLE address.

        - **addr_type** – White-list address type, 0 for public and 1 for random.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gap_clear_whitelist(void)
:   Clear the controller BLE white list.

    返回
    :   0 on success, otherwise error code.

int bk_dm_prf_gap_update_param(uint8_t *addr, uint16_t interval, uint16_t tout)
:   Update BLE connection parameters.

    参数
    :   - **addr** – Peer BLE address.

        - **interval** – Connection interval.

        - **tout** – Supervision timeout.

    返回
    :   0 on success, otherwise error code.

int32_t dm_ble_gap_get_rpa(uint8_t *rpa)
:   Get the current resolvable private address.

    参数
    :   **rpa** – Output buffer for the address. The buffer length must be 6 bytes.

    返回
    :   0 on success, otherwise error code.

void bk_dm_prf_gap_get_identity_addr(uint8_t *addr)
:   Get the local identity address.

    参数
    :   **addr** – Output buffer for the address. The buffer length must be 6 bytes.

int16_t bk_dm_prf_gap_get_current_conn_id(void)
:   Get the current BLE GATT connection ID.

    返回
    :   Current connection ID, or negative value when no connection is active.

int dm_ble_gap_set_auto_accept_pair_req(uint8_t accpet)
:   Configure whether pairing requests are accepted automatically.

    参数
    :   **accpet** – Non-zero to accept automatically, zero to require application handling.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gap_disconnect(uint8_t *addr)
:   Disconnect a BLE GATT link by address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gap_connect_cancel(void)
:   Cancel an ongoing BLE connection attempt.

    返回
    :   0 on success, otherwise error code.


### Structures

struct cli_gatt_param_t
:   GATT framework initialization parameters.


### Macros

GAP_IS_OLD_API
:   Enable BLE bond/local-key storage in the GATT framework. Enable the built-in GATTS test attribute table. Select the legacy GAP API path.

GATT_MAX_BOND_COUNT
:   Maximum number of BLE bonded devices tracked by the GATT framework.

SYNC_CMD_TIMEOUT_MS
:   Timeout in milliseconds for synchronous GATT helper commands.

GATT_DEBUG_LEVEL

gatt_loge(format, ...)

gatt_logw(format, ...)

gatt_logi(format, ...)

gatt_logd(format, ...)

gatt_logv(format, ...)

INTERESTING_SERIVCE_UUID
:   Demo service UUID used by the GATT sample flow.

INTERESTING_CHAR_UUID
:   Demo characteristic UUID used by the GATT sample flow.

GATT_PARAM_MEMBER(type)
:   Helper macro used to declare CLI GATT parameter fields.


### Enumerations

enum [anonymous]
:   GATT framework log levels.


    *Values:*

    enumerator GATT_DEBUG_LEVEL_ERROR
    :   Error log level.

    enumerator GATT_DEBUG_LEVEL_WARNING
    :   Warning log level.

    enumerator GATT_DEBUG_LEVEL_INFO
    :   Informational log level.

    enumerator GATT_DEBUG_LEVEL_DEBUG
    :   Debug log level.

    enumerator GATT_DEBUG_LEVEL_VERBOSE
    :   Verbose log level.

enum [anonymous]
:   Return values used by registered BLE GAP application callbacks.


    *Values:*

    enumerator DM_BLE_GAP_APP_CB_RET_PROCESSED
    :   Event was processed by the callback.

    enumerator DM_BLE_GAP_APP_CB_RET_NO_INTERESTING
    :   Event was not handled by the callback.


### Header File


- [bk_bluetooth/service/dm/ble/gatt/dm_gatts.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gatts.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gatts.h")


### Functions

int32_t bk_dm_prf_gatts_is_init(void)
:   Check whether GATTS has been initialized.

    返回
    :   Non-zero if initialized, otherwise zero.

int bk_dm_prf_gatts_main([cli_gatt_param_t](#_CPPv416cli_gatt_param_t "cli_gatt_param_t") *param)
:   Initialize the GATTS wrapper.

    参数
    :   **param** – Optional GATT initialization parameters.

    返回
    :   0 on success, otherwise error code.

int bk_dm_prf_gatts_deinit(void)
:   Deinitialize the GATTS wrapper.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gatts_deinit_because_bluetooth_deinit_future(void)
:   Deinitialize GATTS during Bluetooth deinitialization.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gatts_disconnect(uint8_t *addr)
:   Disconnect a GATTS link by peer address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gatts_enable_adv(uint8_t enable)
:   Enable or disable advertising.

    参数
    :   **enable** – Non-zero to enable advertising, zero to disable.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gatts_enable_service(uint32_t index, uint8_t enable)
:   Enable or disable a registered GATTS service.

    参数
    :   - **index** – Service index.

        - **enable** – Non-zero to enable the service, zero to disable.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gatts_reg_db([bk_gatts_attr_db_t](dual_ble.md#_CPPv418bk_gatts_attr_db_t "bk_gatts_attr_db_t") *list, uint32_t count, uint16_t *attr_handle_list, [dm_ble_gatts_db_cb](#_CPPv418dm_ble_gatts_db_cb "dm_ble_gatts_db_cb") cb, uint8_t need_create_tab)
:   Register a GATTS attribute database.

    参数
    :   - **list** – Attribute database list.

        - **count** – Number of attributes in the list.

        - **attr_handle_list** – Output attribute handle list.

        - **cb** – Database event callback.

        - **need_create_tab** – Non-zero to create the attribute table.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gatts_unreg_db([bk_gatts_attr_db_t](dual_ble.md#_CPPv418bk_gatts_attr_db_t "bk_gatts_attr_db_t") *list)
:   Unregister a GATTS attribute database.

    参数
    :   **list** – Attribute database list.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gatts_get_buff_from_attr_handle([bk_gatts_attr_db_t](dual_ble.md#_CPPv418bk_gatts_attr_db_t "bk_gatts_attr_db_t") *attr_list, uint16_t *attr_handle_list, uint32_t size, uint16_t attr_handle, uint32_t *output_index, uint8_t **output_buff, uint32_t *output_size)
:   Find an attribute value buffer by attribute handle.

    参数
    :   - **attr_list** – Attribute database list.

        - **attr_handle_list** – Attribute handle list.

        - **size** – Number of attributes in the list.

        - **attr_handle** – Attribute handle to find.

        - **output_index** – Output index in the attribute list.

        - **output_buff** – Output pointer to the attribute value buffer.

        - **output_size** – Output attribute value buffer size.

    返回
    :   0 on success, otherwise error code.

[bk_gatt_if_t](dual_ble.md#_CPPv412bk_gatt_if_t "bk_gatt_if_t") bk_dm_prf_gatts_get_current_if(void)
:   Get the current GATTS interface.

    返回
    :   Current GATT interface.

int bk_dm_prf_gatts_add_gatts_callback(void *param)
:   Register a GATTS application callback.

    参数
    :   **param** – Callback pointer.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gatts_send_service_change_indicate(uint16_t conn_id, uint8_t all_connected)
:   Send a Service Changed indication.

    参数
    :   - **conn_id** – GATT connection ID.

        - **all_connected** – Non-zero to send to all connected peers.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gatts_send_notify(uint16_t gatt_conn_id, uint16_t attr_handle, uint8_t *data, uint32_t len, uint8_t is_notify)
:   Send notification or indication.

    参数
    :   - **gatt_conn_id** – GATT connection ID.

        - **attr_handle** – Attribute handle.

        - **data** – Data buffer.

        - **len** – Data length in bytes.

        - **is_notify** – Non-zero to send notification, zero to send indication.

    返回
    :   0 on success, otherwise error code.


### Macros

BK_GATT_ATTR_TYPE(iuuid)
:   Build a 16-bit UUID attribute type initializer.

BK_GATT_ATTR_CONTENT(iuuid)
:   Build a 16-bit UUID attribute content initializer.

BK_GATT_ATTR_VALUE(ilen, ivalue)
:   Build an attribute value initializer.

BK_GATT_ATTR_TYPE_128(iuuid)
:   Build a 128-bit UUID attribute type initializer.

BK_GATT_ATTR_CONTENT_128(iuuid)
:   Build a 128-bit UUID attribute content initializer.

BK_GATT_PRIMARY_SERVICE_DECL(iuuid)
:   Build a primary service declaration with a 16-bit service UUID.

BK_GATT_PRIMARY_SERVICE_DECL_128(iuuid)
:   Build a primary service declaration with a 128-bit service UUID.

BK_GATT_CHAR_DECL(iuuid, ilen, ivalue, iprop, iperm, irsp)
:   Build a characteristic declaration with a 16-bit characteristic UUID.

BK_GATT_CHAR_DECL_128(iuuid, ilen, ivalue, iprop, iperm, irsp)
:   Build a characteristic declaration with a 128-bit characteristic UUID.

BK_GATT_CHAR_DESC_DECL(iuuid, ilen, ivalue, iperm, irsp)
:   Build a characteristic descriptor declaration with a 16-bit descriptor UUID.

BK_GATT_CHAR_DESC_DECL_128(iuuid, ilen, ivalue, iperm, irsp)
:   Build a characteristic descriptor declaration with a 128-bit descriptor UUID.


### Type Definitions

typedef int32_t (*dm_ble_gatts_db_cb)([bk_gatts_cb_event_t](dual_ble.md#_CPPv419bk_gatts_cb_event_t "bk_gatts_cb_event_t") event, [bk_gatt_if_t](dual_ble.md#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts_if, [bk_ble_gatts_cb_param_t](dual_ble.md#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t") *param)
:   GATTS database event callback.

    Param event
    :   GATTS callback event.

    Param gatts_if
    :   GATTS interface.

    Param param
    :   Event parameter.

    Return
    :   0 on success, otherwise error code.

typedef int32_t (*dm_ble_gatts_app_cb)([bk_gatts_cb_event_t](dual_ble.md#_CPPv419bk_gatts_cb_event_t "bk_gatts_cb_event_t") event, [bk_gatt_if_t](dual_ble.md#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts_if, [bk_ble_gatts_cb_param_t](dual_ble.md#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t") *comm_param)
:   GATTS application event callback.

    Param event
    :   GATTS callback event.

    Param gatts_if
    :   GATTS interface.

    Param comm_param
    :   Event parameter.

    Return
    :   0 on success, otherwise error code.


### Header File


- [bk_bluetooth/service/dm/ble/gatt/dm_gattc.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gattc.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gattc.h")


### Functions

int bk_dm_prf_gattc_main([cli_gatt_param_t](#_CPPv416cli_gatt_param_t "cli_gatt_param_t") *param)
:   Initialize the GATTC wrapper.

    参数
    :   **param** – Optional GATT initialization parameters.

    返回
    :   0 on success, otherwise error code.

int bk_dm_prf_gattc_deinit(void)
:   Deinitialize the GATTC wrapper.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gattc_connect(uint8_t *addr, uint32_t addr_type, uint32_t s_timeout)
:   Connect to a GATT server.

    参数
    :   - **addr** – Peer BLE address.

        - **addr_type** – Peer BLE address type.

        - **s_timeout** – Connection timeout in seconds.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gattc_connect_ext(uint8_t *addr, uint32_t addr_type, [bk_gap_create_conn_params_t](dual_ble.md#_CPPv427bk_gap_create_conn_params_t "bk_gap_create_conn_params_t") *pm)
:   Connect to a GATT server with custom connection parameters.

    When pm is NULL, falls back to default params identical to dm_gattc_connect(addr, addr_type, 500). bk_dm_prf_gattc_connect(addr, addr_type, 500).

    参数
    :   - **addr** – Peer BLE address.

        - **addr_type** – Peer BLE address type.

        - **pm** – Custom connection parameters, or NULL to use defaults.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gattc_disconnect(uint8_t *addr)
:   Disconnect from a GATT server.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gattc_connect_cancel(void)
:   Cancel an ongoing GATTC connection attempt.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gattc_discover(uint16_t conn_id)
:   Discover services on a GATT server.

    参数
    :   **conn_id** – GATT connection ID.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gattc_write(uint16_t conn_id, uint16_t attr_handle, uint8_t *data, uint32_t len)
:   Write an attribute on a GATT server.

    参数
    :   - **conn_id** – GATT connection ID.

        - **attr_handle** – Attribute handle.

        - **data** – Data buffer.

        - **len** – Data length in bytes.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gattc_write_ext(uint16_t gatt_conn_id, uint16_t attr_handle, uint8_t *data, uint32_t len, uint8_t write_req)
:   Write an attribute with selectable write mode.

    参数
    :   - **gatt_conn_id** – GATT connection ID.

        - **attr_handle** – Attribute handle.

        - **data** – Data buffer.

        - **len** – Data length in bytes.

        - **write_req** – Non-zero to use write request, zero to use write command.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gattc_read(uint16_t gatt_conn_id, uint16_t attr_handle, uint8_t *data, uint32_t len)
:   Read an attribute from a GATT server.

    参数
    :   - **gatt_conn_id** – GATT connection ID.

        - **attr_handle** – Attribute handle.

        - **data** – Output buffer.

        - **len** – Output buffer length in bytes.

    返回
    :   0 on success, otherwise error code.

int32_t bk_dm_prf_gattc_send_mtu_req(uint8_t *mac, uint8_t gatt_conn_id)
:   Send an MTU exchange request.

    参数
    :   - **mac** – Peer BLE address.

        - **gatt_conn_id** – GATT connection ID.

    返回
    :   0 on success, otherwise error code.

int bk_dm_prf_gattc_add_gattc_callback(void *param)
:   Register a GATTC application callback.

    参数
    :   **param** – Callback pointer.

    返回
    :   0 on success, otherwise error code.


### Type Definitions

typedef int32_t (*dm_ble_gattc_app_cb)([bk_gattc_cb_event_t](dual_ble.md#_CPPv419bk_gattc_cb_event_t "bk_gattc_cb_event_t") event, [bk_gatt_if_t](dual_ble.md#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, [bk_ble_gattc_cb_param_t](dual_ble.md#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t") *comm_param)
:   GATTC application event callback.

    Param event
    :   GATTC callback event.

    Param gattc_if
    :   GATTC interface.

    Param comm_param
    :   Event parameter.

    Return
    :   0 on success, otherwise error code.


### Header File


- [bk_bluetooth/service/dm/ble/gatt/dm_gatt_connection.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gatt_connection.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gatt_connection.h")


### Functions

int32_t dm_ble_app_env_init(void)
:   Initialize the BLE GATT connection context pool.

    返回
    :   0 on success, otherwise error code.

int32_t dm_ble_app_env_deinit(void)
:   Deinitialize the BLE GATT connection context pool.

    返回
    :   0 on success, otherwise error code.

[dm_gatt_app_env_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") *dm_ble_alloc_app_env_by_addr(uint8_t *addr, uint32_t data_len)
:   Allocate a connection context by peer address.

    参数
    :   - **addr** – Peer BLE address.

        - **data_len** – Length of additional data to allocate for this connection.

    返回
    :   Pointer to the context on success, otherwise NULL.

[dm_gatt_app_env_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") *dm_ble_find_app_env_by_addr(uint8_t *addr)
:   Find a connection context by peer address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   Pointer to the context on success, otherwise NULL.

[dm_gatt_app_env_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") *dm_ble_find_app_env_by_conn_id(uint16_t conn_id)
:   Find a connection context by connection ID.

    参数
    :   **conn_id** – GATT connection ID.

    返回
    :   Pointer to the context on success, otherwise NULL.

uint8_t dm_ble_del_app_env_by_addr(uint8_t *addr)
:   Delete a connection context by peer address.

    参数
    :   **addr** – Peer BLE address.

    返回
    :   Non-zero if a context was deleted, otherwise zero.

uint8_t dm_ble_free_all_app_env(void)
:   Free all connection contexts.

    返回
    :   Non-zero on success, otherwise zero.

[dm_gatt_app_env_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") *dm_ble_alloc_addition_data_by_addr(uint8_t *addr, uint32_t data_len)
:   Allocate or resize additional data for a connection.

    参数
    :   - **addr** – Peer BLE address.

        - **data_len** – Additional data length in bytes.

    返回
    :   Pointer to the context on success, otherwise NULL.

[dm_gatt_app_env_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") *dm_ble_alloc_profile_data_by_addr(uint32_t profile_id, uint8_t *addr, uint32_t data_len, uint8_t **output_param)
:   Allocate profile-specific data for a connection.

    参数
    :   - **profile_id** – Profile ID.

        - **addr** – Peer BLE address.

        - **data_len** – Profile data length in bytes.

        - **output_param** – Output pointer to the allocated profile data buffer.

    返回
    :   Pointer to the context on success, otherwise NULL.

uint8_t *dm_ble_find_profile_data_by_profile_id([dm_gatt_app_env_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") *env, uint32_t profile_id)
:   Find profile-specific data by profile ID.

    参数
    :   - **env** – Connection context.

        - **profile_id** – Profile ID.

    返回
    :   Pointer to profile data on success, otherwise NULL.

uint8_t dm_ble_app_env_foreach(int32_t (*func)([dm_gatt_app_env_t](#_CPPv417dm_gatt_app_env_t "dm_gatt_app_env_t") *env, void *arg), void *arg)
:   Iterate over active connection contexts.

    参数
    :   - **func** – Callback invoked for each context.

        - **arg** – User argument passed to the callback.

    返回
    :   Number of visited contexts.


### Structures

struct dm_gatt_app_env_t
:   BLE GATT per-connection context.

struct dm_gatt_demo_app_env_t
:   Demo GATT application context shared by GATTS and GATTC demo flows.


### Macros

GATT_MAX_CONNECTION_COUNT
:   Maximum number of GATT connections tracked by the framework.

GATT_MAX_PROFILE_COUNT
:   Maximum number of profile-specific data blocks per connection.


### Enumerations

enum [anonymous]
:   BLE GAP connection states used by dm_gatt_app_env_t::status.


    *Values:*

    enumerator GAP_CONNECT_STATUS_IDLE
    :   Connection is idle.

    enumerator GAP_CONNECT_STATUS_CONNECTING
    :   Connection is being established.

    enumerator GAP_CONNECT_STATUS_CONNECTED
    :   Connection is established.

    enumerator GAP_CONNECT_STATUS_DISCONNECTING
    :   Connection is being disconnected.

enum [anonymous]
:   GATTC MTU request states.


    *Values:*

    enumerator GATTC_MTU_REQ_STATUS_IDLE
    :   No MTU request is running.

    enumerator GATTC_MTU_REQ_STATUS_ING
    :   MTU request is in progress.

    enumerator GATTC_MTU_REQ_STATUS_COMPLETED
    :   MTU request is complete.

enum [anonymous]
:   GATTC service discovery states.


    *Values:*

    enumerator GATTC_DISCOVER_STATUS_IDLE
    :   No discovery is running.

    enumerator GATTC_DISCOVER_STATUS_ING
    :   Discovery is in progress.

    enumerator GATTC_DISCOVER_STATUS_COMPLETED
    :   Discovery is complete.


### Header File


- [bk_bluetooth/service/dm/ble/gatt/dm_gap_utils.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gap_utils.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/gatt/dm_gap_utils.h")


### Functions

uint8_t bk_dm_prf_gap_is_addr_valid(uint8_t *addr)
:   Check whether a BLE address is valid.

    参数
    :   **addr** – BLE address buffer. The buffer length must be 6 bytes.

    返回
    :   Non-zero if the address is valid, otherwise zero.

uint8_t bk_dm_prf_gap_is_data_valid(uint8_t *data, uint32_t len)
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


## HOGPD Demo

HOGPD Demo 基于 BLE GATT framework 实现 HID-over-GATT keyboard 示例。

API 参考：


### Header File


- [bk_bluetooth/service/dm/ble/hogpd/hogpd.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/hogpd/hogpd.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/ble/hogpd/hogpd.h")


### Functions

int32_t bk_dm_prf_hogpd_init(void)

int32_t bk_dm_prf_hogpd_deinit(uint8_t deinit_bluetooth_future)

int32_t bk_dm_prf_hogpd_deinit_because_bluetooth_deinit_future(void)

int32_t bk_dm_prf_hogpd_notify(uint16_t gatt_conn_handle, uint8_t *data, uint32_t len, uint8_t is_notify, uint8_t report_id)


### Macros

HOGPD_ENABLE

关键配置：


- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_HOGPD`：启用 HOGPD demo。

- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_HOGPD_LOG_LEVEL`：配置 HOGPD demo 日志等级。

- `CONFIG_CLI`：启用 HOGPD CLI。


## PAN/HIDD Service

PAN/HIDD service 提供 PAN 网络接入、PAN demo CLI、HID device demo 和相关重连处理。

API 参考：


### Header File


- [bk_bluetooth/service/dm/bk_pan/pan_service.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/bk_pan/pan_service.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/bk_pan/pan_service.h")


### Functions

int pan_service_init(void)
:   Initialize the PAN service.

    返回
    :   0 on success, otherwise error code.

int cli_pan_demo_init(void)
:   Register PAN demo CLI commands.

    返回
    :   0 on success, otherwise error code.

void bt_start_pan_reconnect(void)
:   Start PAN reconnect flow.

void pan_show_tx_data_cache_count(void)
:   Print the current PAN TX data cache count.

int pan_service_deinit(void)
:   Deinitialize the PAN service.

    返回
    :   0 on success, otherwise error code.

int cli_pan_demo_deinit(void)
:   Unregister PAN demo CLI commands.

    返回
    :   0 on success, otherwise error code.

void bt_pan_reconnect_failure_handler(void)
:   Handle PAN reconnect failure.


### Header File


- [bk_bluetooth/service/dm/bk_pan/hidd_service.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/bk_pan/hidd_service.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/bk_pan/hidd_service.h")


### Functions

void bt_hidd_init(void)
:   Initialize the Bluetooth HID Device demo service.

void bt_hidd_deinit(void)
:   Deinitialize the Bluetooth HID Device demo service.

关键配置：


- `CONFIG_NET_PAN`：启用 PAN service。

- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE`：启用 BTDM service 组件。若未启用，PAN 子组件会
  单独编译 BT manager 和 storage 依赖。

- `CONFIG_CLI`：启用 PAN demo CLI。


## Storage

`bluetooth_storage` 用于保存 BT link key、BLE bond 信息、local key、音量和地址 hash 等
蓝牙业务数据。

API 参考：


### Header File


- [bk_bluetooth/service/dm/storage/bluetooth_storage.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/storage/bluetooth_storage.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bk_bluetooth/service/dm/storage/bluetooth_storage.h")


### Functions

int32_t bluetooth_storage_init(void)
:   Initialize Bluetooth storage.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_deinit(void)
:   Deinitialize Bluetooth storage.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_find_linkkey_info_index(uint8_t *addr, uint8_t *key)
:   Find a BT link key record by address.

    参数
    :   - **addr** – Remote Bluetooth device address.

        - **key** – Output buffer for the link key. Pass NULL when only the index is needed.

    返回
    :   Record index on success, otherwise negative error code.

int32_t bluetooth_storage_save_linkkey_info(uint8_t *addr, uint8_t *key)
:   Save or update a BT link key record.

    参数
    :   - **addr** – Remote Bluetooth device address.

        - **key** – BT link key buffer. The buffer length must be 16 bytes.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_del_linkkey_info(uint8_t *addr)
:   Delete a BT link key record.

    参数
    :   **addr** – Remote Bluetooth device address.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_update_to_newest(uint8_t *addr)
:   Move a BT link key record to the newest position.

    参数
    :   **addr** – Remote Bluetooth device address.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_get_newest_linkkey_info(uint8_t *addr, uint8_t *key)
:   Get the newest valid BT link key record.

    参数
    :   - **addr** – Output buffer for the remote Bluetooth device address.

        - **key** – Output buffer for the link key. Pass NULL when only the address is needed.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_clean_linkkey_info(void)
:   Clear all BT link key records.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_sync_to_flash(void)
:   Synchronize Bluetooth storage data to flash.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_linkkey_debug(void)
:   Print BT link key records for debugging.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_find_volume_by_addr(uint8_t *addr, uint8_t *volume)
:   Find saved A2DP volume by address.

    参数
    :   - **addr** – Remote Bluetooth device address.

        - **volume** – Output A2DP volume.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_find_hfp_volume_by_addr(uint8_t *addr, uint8_t *mic_vol, uint8_t *spk_vol)
:   Find saved HFP microphone and speaker volume by address.

    参数
    :   - **addr** – Remote Bluetooth device address.

        - **mic_vol** – Output HFP microphone volume.

        - **spk_vol** – Output HFP speaker volume.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_save_volume(uint8_t *addr, uint8_t volume)
:   Save A2DP volume for a remote device.

    参数
    :   - **addr** – Remote Bluetooth device address.

        - **volume** – A2DP volume.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_save_hfp_volume(uint8_t *addr, uint8_t type, uint8_t volume)
:   Save HFP volume for a remote device.

    参数
    :   - **addr** – Remote Bluetooth device address.

        - **type** – Volume target. 0 indicates microphone and 1 indicates speaker.

        - **volume** – HFP volume.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_save_hash(uint8_t *addr, uint32_t hash)
:   Save an address hash for a remote device.

    参数
    :   - **addr** – Remote Bluetooth device address.

        - **hash** – Address hash value.

    返回
    :   0 on success, otherwise error code.

int32_t bluetooth_storage_find_addr_by_hash(uint8_t *addr, uint32_t hash)
:   Find a remote device address by hash.

    参数
    :   - **addr** – Output remote Bluetooth device address.

        - **hash** – Address hash value.

    返回
    :   0 on success, otherwise error code.

uint8_t bluetooth_storage_get_bond_device_num(void)
:   Get the number of bonded BT devices.

    返回
    :   Number of bonded devices.

uint32_t bluetooth_storage_get_bond_hash(uint16_t hasharray[], uint32_t arraylen)
:   Get compact bond hash values.

    参数
    :   - **hasharray** – Output hash array.

        - **arraylen** – Number of elements in hasharray.

    返回
    :   Number of hash values written to hasharray.


### Structures

struct bt_user_storage_elem_linkkey_t
:   Per-device BT link key and profile volume record.

    Public Members

    uint8_t addr[6]
    :   Remote Bluetooth device address.

    uint8_t link_key[16]
    :   BT link key.

    uint8_t a2dp_volume
    :   Saved A2DP volume.

    uint32_t hash
    :   Address hash used for compact lookup.

    uint8_t hfp_mic_vol
    :   Saved HFP microphone volume.

    uint8_t hfp_spk_vol
    :   Saved HFP speaker volume.

struct bt_user_storage_t
:   Bluetooth user storage data persisted by the service layer.

    Public Members

    [bt_user_storage_elem_linkkey_t](#_CPPv430bt_user_storage_elem_linkkey_t "bt_user_storage_elem_linkkey_t") linkkey[BT_LINKKEY_MAX_SAVE_COUNT]
    :   Saved BT link key records.


### Macros

BT_STORAGE_KEY
:   Persistent storage key used for Bluetooth user information.

BT_LINKKEY_MAX_SAVE_COUNT
:   Maximum number of BT link key or BLE bond records saved by this module.


## 使用建议

需要快速构建典型蓝牙业务流程时，可参考
[蓝牙开发者指南](../../developer-guide/bluetooth.md "../../developer-guide/bluetooth.md")，其中包含常见蓝牙功能的设计说明和使用建议。

使用 service 层前，请确认工程已启用对应的 Bluetooth、Profile、音频或网络 Kconfig 选项。
