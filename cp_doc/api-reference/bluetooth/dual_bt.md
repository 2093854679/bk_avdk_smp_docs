# 双模 BT



## Dual BT API 分类

Dual BT API 主要包括以下类型：

按功能划分的 BT API：
:   - BT GAP 接口

    - BT A2DP 接口

    - BT AVRCP 接口

    - BT HFP 接口

    - BT HID 接口

    - BT L2CAP 接口

    - BT SPP 接口


## 兼容性和扩展性

Dual BT API 具备较好的扩展性和向后兼容性。多数 BT 配置结构体中预留了字段，便于后续扩展。使用这些 API 时，应将预留字段初始化为 0，避免后续新增字段后影响兼容性。


## 编程原则

重要

使用 BT API 时建议遵循以下原则：
:   - 配置结构体中的预留字段应初始化为 0。

    - 使用 `BK_ERR_CHECK` 检查 BT API 的返回值。

    - 不确定 API 用法时，优先参考 BT 示例代码。

    - 不确定配置结构体字段如何初始化时，先使用默认配置宏，再按应用需求修改相关字段。

    - 不建议在 BT 事件回调中执行耗时操作，可将事件转发到应用任务中处理。


## 事件处理机制

Beken BT driver 采用事件驱动方式工作。应用通过 BT API 发起可发现、可连接、配对、profile 连接等操作，并在 BT 事件回调中获取状态变化和操作结果。


## API 参考


## bk_dm_gap_bt.h

`bk_dm_gap_bt.h` 提供 BT GAP 的可发现、可连接、配对和设备管理接口。


### Header File


- [bluetooth/bk_dm_gap_bt.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gap_bt.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gap_bt.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_register_callback([bk_bt_gap_cb_t](#_CPPv414bk_bt_gap_cb_t "bk_bt_gap_cb_t") callback)
:   register callback function. This function should be called after bk_bluedroid_enable() completes successfully

    返回
    :   - BK_OK : Succeed

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_set_scan_mode(bk_bt_conn_mode_t c_mode, bk_bt_disc_mode_t d_mode)
:   Set discoverability and connectability mode for legacy bluetooth.

    参数
    :   - **c_mode** – **[in]** : one of the enums of bk_bt_connection_mode_t

        - **d_mode** – **[in]** : one of the enums of bk_bt_discovery_mode_t

    返回
    :   - BK_OK : Succeed

        - BK_ERR_INVALID_ARG: if argument invalid

        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_get_scan_mode()
:   Get discoverability and connectability mode of legacy bluetooth.

    返回
    :   - BK_OK : Succeed

        - BK_ERR_INVALID_ARG: if argument invalid

        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_start_discovery([bk_bt_inq_mode_t](#_CPPv416bk_bt_inq_mode_t "bk_bt_inq_mode_t") mode, uint8_t inq_len, uint8_t num_rsps)
:   This function starts Inquiry and Name Discovery. When Inquiry is halted and cached results do not contain device name, then Name Discovery will connect to the peer target to get the device name. bk_bt_gap_cb_t will be called with BK_BT_GAP_DISC_STATE_CHANGED_EVT when Inquriry is started or Name Discovery is completed. bk_bt_gap_cb_t will be called with BK_BT_GAP_DISC_RES_EVT each time the two types of discovery results are got.

    参数
    :   - **mode** – **[in]** - Inquiry mode

        - **inq_len** – **[in]** - Inquiry duration in 1.28 sec units, ranging from 0x01 to 0x30. This parameter only specifies the total duration of the Inquiry process,

          - when this time expires, Inquiry will be halted.

        - **num_rsps** – **[in]** - Number of responses that can be received before the Inquiry is halted, value 0 indicates an unlimited number of responses.

    返回
    :   - BK_OK : Succeed

        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - BK_ERR_INVALID_ARG: if invalid parameters are provided

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_cancel_discovery(void)
:   Cancel Inquiry and Name Discovery. bk_bt_gap_cb_t will be called with BK_BT_GAP_DISC_STATE_CHANGED_EVT if Inquiry or Name Discovery is cancelled by calling this function.

    返回
    :   - BK_OK : Succeed

        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_get_remote_services([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda)
:   Start SDP to get remote services. bk_bt_gap_cb_t will be called with BK_BT_GAP_RMT_SRVCS_EVT after service discovery ends.

    返回
    :   - BK_OK : Succeed

        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_get_remote_service_record([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda, [bk_bt_uuid_t](dual_ble.md#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") *uuid)
:   Start SDP to look up the service matching uuid on the remote device.

    ```
                 bk_bt_gap_cb_t will be called with BK_BT_GAP_RMT_SRVC_REC_EVT after service discovery ends
    ```

    返回
    :   - BK_OK : Succeed

        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_config_eir_data([bk_bt_eir_data_t](#_CPPv416bk_bt_eir_data_t "bk_bt_eir_data_t") *eir_data)
:   This function is called to config EIR data.

    ```
                 bk_bt_gap_cb_t will be called with BK_BT_GAP_CONFIG_EIR_DATA_EVT after config EIR ends.
    ```

    参数
    :   **eir_data** – **[in]** - pointer of EIR data content

    返回
    :   - BK_OK : Succeed

        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - BK_ERR_INVALID_ARG: if param is invalid

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_set_cod([bk_bt_cod_t](#_CPPv411bk_bt_cod_t "bk_bt_cod_t") cod, [bk_bt_cod_mode_t](#_CPPv416bk_bt_cod_mode_t "bk_bt_cod_mode_t") mode)
:   This function is called to set class of device. The structure bk_bt_gap_cb_t will be called with BK_BT_GAP_SET_COD_EVT after set COD ends. Some profile have special restrictions on class of device, changes may cause these profile do not work.

    参数
    :   - **cod** – **[in]** - class of device

        - **mode** – **[in]** - setting mode

    返回
    :   - BK_OK : Succeed

        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - BK_ERR_INVALID_ARG: if param is invalid

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_read_rssi_delta([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_addr)
:   This function is called to read RSSI delta by address after connected. The RSSI value returned by BK_BT_GAP_READ_RSSI_DELTA_EVT.

    参数
    :   **remote_addr** – **[in]** - remote device address, corrbkonding to a certain connection handle

    返回
    :   - BK_OK : Succeed

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_remove_bond_device([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   Removes a device from the security database list of peer device.

    参数
    :   **bd_addr** – **[in]** : BD address of the peer device

    返回
    :   - BK_OK : success


        - BK_FAIL : failed

int bk_bt_gap_get_bond_device_num(void)
:   Get the device number from the security database list of peer device. It will return the device bonded number immediately.

    返回
    :   - >= 0 : bonded devices number


        - BK_FAIL : failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_get_bond_device_list(int *dev_num, [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") *dev_list)
:   Get the device from the security database list of peer device. It will return the device bonded information immediately.

    参数
    :   - **dev_num** – **[inout]** Indicate the dev_list array(buffer) size as input. If dev_num is large enough, it means the actual number as output. Suggest that dev_num value equal to [bk_ble_get_bond_device_num()](dual_ble.md#group__dm__gap__defines__v1_1ga197bcd6bbaf7eabfddabce66be9fad92 "dual_ble.md#group__dm__gap__defines__v1_1ga197bcd6bbaf7eabfddabce66be9fad92").

        - **dev_list** – **[out]** an array(buffer) of `bk_bd_addr_t` type. Use for storing the bonded devices address. The dev_list should be allocated by who call this API.

    返回
    :   - BK_OK : Succeed

        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - BK_FAIL: others

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_set_pin([bk_bt_pin_type_t](#_CPPv416bk_bt_pin_type_t "bk_bt_pin_type_t") pin_type, uint8_t pin_code_len, [bk_bt_pin_code_t](#_CPPv416bk_bt_pin_code_t "bk_bt_pin_code_t") pin_code)
:   Set pin type and default pin code for legacy pairing.

    参数
    :   - **pin_type** – **[in]** Use variable or fixed pin. If pin_type is BK_BT_PIN_TYPE_VARIABLE, pin_code and pin_code_len will be ignored, and BK_BT_GAP_PIN_REQ_EVT will come when control requests for pin code. Else, will use fixed pin code and not callback to users.

        - **pin_code_len** – **[in]** Length of pin_code

        - **pin_code** – **[in]** Pin_code

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_pin_reply([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, bool accept, uint8_t pin_code_len, [bk_bt_pin_code_t](#_CPPv416bk_bt_pin_code_t "bk_bt_pin_code_t") pin_code)
:   Reply the pin_code to the peer device for legacy pairing when BK_BT_GAP_PIN_REQ_EVT is coming.

    参数
    :   - **bd_addr** – **[in]** BD address of the peer

        - **accept** – **[in]** Pin_code reply successful or declined.

        - **pin_code_len** – **[in]** Length of pin_code

        - **pin_code** – **[in]** Pin_code

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_set_security_param([bk_bt_sp_param_t](#_CPPv416bk_bt_sp_param_t "bk_bt_sp_param_t") param_type, void *value, uint8_t len)
:   Set a GAP security parameter value. Overrides the default value.

    参数
    :   - **param_type** – **[in]** : the type of the param which is to be set

        - **value** – **[in]** : the param value

        - **len** – **[in]** : the length of the param value

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_ssp_passkey_reply([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, bool accept, uint32_t passkey)
:   Reply the key value to the peer device in the legacy connection stage.

    参数
    :   - **bd_addr** – **[in]** : BD address of the peer

        - **accept** – **[in]** : passkey entry successful or declined.

        - **passkey** – **[in]** : passkey value, must be a 6 digit number, can be lead by 0.

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_ssp_confirm_reply([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, bool accept)
:   Reply the confirm value to the peer device in the legacy connection stage.

    参数
    :   - **bd_addr** – **[in]** : BD address of the peer device

        - **accept** – **[in]** : numbers to compare are the same or different

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_set_afh_channels([bk_bt_gap_afh_channels](#_CPPv422bk_bt_gap_afh_channels "bk_bt_gap_afh_channels") channels)
:   Set the AFH channels.

    参数
    :   **channels** – **[in]** : The n th such field (in the range 0 to 78) contains the value for channel n : 0 means channel n is bad. 1 means channel n is unknown. The most significant bit is reserved and shall be set to 0. At least 20 channels shall be marked as unknown.

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_read_remote_name([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda)
:   Read the remote device name.

    参数
    :   **remote_bda** – **[in]** The remote device’s address

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_gap_connect([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, uint8_t allow_role_switch)
:   Connect the remote device.

    参数
    :   - **addr** – **[in]** The remote device’s address

        - **allow_role_switch** – **[in]** Allow the role switch

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_gap_disconnect([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, uint8_t reason)
:   Disconnect the remote device.

    参数
    :   - **addr** – **[in]** The remote device’s address

        - **reason** – **[in]** The disconnect reason

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_gap_create_conn_cancel(uint8_t *addr)
:   This API can be used to request cancellation of the ongoing connection creation process.

    参数
    :   **addr** – **[in]** The remote device’s address

    返回
    :   ```

                     - BK_ERR_BT_SUCCESS: cancel request is sent to lower layer successfully

                     - others: fail
        ```

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_gap_set_page_timeout(uint16_t timeout)
:   This api can be used to set the value for the Page_Timeout configuration parameter.

    参数
    :   **timeout** – **[in]** Page Timeout measured in number of Baseband slots, unit of 0.625ms

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_gap_set_page_scan_activity(uint16_t interval, uint16_t window)
:   This api can be used to set the value for the Page_Scan_Interval and Page_Scan_Window configuration parameters.

    参数
    :   - **interval** – **[in]** defines the amount of time between consecutive page scans, unit of 0.625ms,(Range: 0x0012 to 0x1000, only even values are valid)

        - **window** – **[in]** defines the amount of time for the duration of the page scan, unit of 0.625ms,(Range: 0x0011 to 0x1000, can only be less than or equal to the Page_Scan_Interval)

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_gap_authentication_request(uint8_t *addr)
:   This api can be used to start authentication request.

    参数
    :   **addr** – **[in]** The remote device’s address

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_gap_set_auto_sniff_policy([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda, uint32_t sec, [bk_bt_gap_sniff_config](#_CPPv422bk_bt_gap_sniff_config "bk_bt_gap_sniff_config") *config)
:   Set auto enter sniff policy. bk_bt_gap_cb_t will be called with BK_BT_GAP_SET_AUTO_SNIFF_CMPL_EVT after service discovery ends.

    参数
    :   - **remote_bda** – **[in]** The remote device’s address

        - **sec** – **[in]** How long time (second) enter sniff once no ACL data send or recv. When equal 0, will disable auto enter sniff.

        - **config** – **[in]** Sniff config. when is NULL, last config will be: max_interval: 500 msec min interval: 250 msec attempt: 5 msec timeout: 1.25 msec

    返回
    :   - BK_OK : Succeed

        - BK_FAIL: others


## bk_dm_a2dp.h

`bk_dm_a2dp.h` 提供 A2DP profile 的连接管理和音频流控制接口。


### Header File


- [bluetooth/bk_dm_a2dp.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_a2dp.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_a2dp.h")


### Functions

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_register_callback([bk_bt_a2dp_cb_t](#_CPPv415bk_bt_a2dp_cb_t "bk_bt_a2dp_cb_t") callback)
:   Register application callback function to A2DP module. used by both A2DP source and sink.

    参数
    :   **callback** – **[in]** A2DP event callback function

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_source_init(void)
:   Initialize the bluetooth A2DP source module. A2DP can work independently.


    **Attention**
    :   sink/source must init only one.

    返回
    :   - BK_ERR_BT_SUCCESS: if the initialization request is sent to lower layer successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_source_deinit(void)
:   De-initialize for A2DP source module. This function should be called only after bk_bt_a2dp_source_init() completes successfully, and BK_A2DP_PROF_STATE_EVT will reported to APP layer.

    返回
    :   - BK_ERR_BT_SUCCESS: if the initialization request is sent to lower layer successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_a2dp_source_register_data_callback([bk_a2dp_source_data_cb_t](#_CPPv424bk_a2dp_source_data_cb_t "bk_a2dp_source_data_cb_t") callback)
:   Register A2DP source data input function. For now, the input should be PCM data stream.

    参数
    :   **callback** – **[in]** A2DP source data callback function

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_a2dp_source_set_pcm_data_format(uint32_t sample_rate, uint8_t bit_depth, uint8_t channel_count)
:   set a2dp source data format

    参数
    :   - **sample_rate** – **[in]** pcm data sample rate, such as 8000 16000 32000 44100 48000.

        - **bit_depth** – **[in]** : pcm data bit depth, now support 16 bits only.

        - **channel_count** – **[in]** : pcm data channel count, support 1 or 2 now.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_a2dp_source_register_pcm_encode_callback([bk_a2dp_source_pcm_encode_cb_t](#_CPPv430bk_a2dp_source_pcm_encode_cb_t "bk_a2dp_source_pcm_encode_cb_t") cb)
:   register pcm encode callback.

    参数
    :   **cb** – **[in]** callback.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_a2dp_source_register_pcm_resample_callback([bk_a2dp_source_pcm_resample_cb_t](#_CPPv432bk_a2dp_source_pcm_resample_cb_t "bk_a2dp_source_pcm_resample_cb_t") cb)
:   register pcm resample callback, will be used if input pcm is not match a2dp negotiation, see BK_A2DP_AUDIO_SOURCE_CFG_EVT.

    参数
    :   **cb** – **[in]** callback.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_source_connect(uint8_t *addr)
:   Connect to remote A2DP sink device. This API must be called after bk_bt_a2dp_source_init()

    参数
    :   **addr** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: connect request is sent to lower layer successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_source_disconnect(uint8_t *addr)
:   Disconnect from the remote A2DP sink device. This API must be called after bk_bt_a2dp_source_init()

    参数
    :   **addr** – **[in]** remote bluetooth device address

    返回
    :   ```

                     - BK_ERR_BT_SUCCESS: connect request is sent to lower layer successfully

                     - others: fail
        ```

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_a2dp_media_ctrl([bk_a2dp_media_ctrl_t](#_CPPv420bk_a2dp_media_ctrl_t "bk_a2dp_media_ctrl_t") ctrl)
:   Media control commands. This API can be used for both A2DP sink and must be called after bk_bt_a2dp_source_init()


    **Attention**
    :   this function only used for a2dp source

    参数
    :   **ctrl** – **[in]** control commands for A2DP action

    返回
    :   - BK_ERR_BT_SUCCESS: control command is sent to lower layer successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_sink_init(uint8_t aac_supported)
:   Initialize the bluetooth A2DP sink module.

    参数
    :   **aac_supported** – **[in]** 1 means aac is supported, 0 means aac is not supported.

    返回
    :   - BK_ERR_BT_SUCCESS: the initialization request is successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_sink_deinit(void)
:   De-initialize for A2DP sink module. This function should be called only after bk_bt_a2dp_sink_init() completes successfully, and BK_A2DP_PROF_STATE_EVT will reported to APP layer.

    返回
    :   - BK_ERR_BT_SUCCESS: the deinitialization request is successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_sink_register_data_callback([bk_bt_sink_data_cb_t](#_CPPv420bk_bt_sink_data_cb_t "bk_bt_sink_data_cb_t") callback)
:   Register A2DP sink data output function;.

    参数
    :   **callback** – **[in]** A2DP sink data callback function

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_sink_connect(uint8_t *remote_bda)
:   Connect to remote bluetooth A2DP source device. This API must be called after bk_bt_a2dp_sink_init().

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_sink_disconnect(uint8_t *remote_bda)
:   Disconnect from the remote A2DP source device. This API must be called after bk_bt_a2dp_sink_init().

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_sink_set_delay_value(uint16_t delay_value)
:   Set delay reporting value.This API must be called after bk_bt_a2dp_sink_init().

    参数
    :   **delay_value** – **[in]** reporting value is in 1/10 millisecond

    返回
    :   - BK_ERR_BT_SUCCESS: delay value is sent to lower layer successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_a2dp_sink_get_delay_value(void)
:   Get delay reporting value. This API must be called after bk_bt_a2dp_sink_init().

    返回
    :   - BK_ERR_BT_SUCCESS: if the request is sent successfully

        - others: fail


## bk_dm_avrcp.h

`bk_dm_avrcp.h` 提供 AVRCP 控制器和目标端的媒体控制接口。


### Header File


- [bluetooth/bk_dm_avrcp.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_avrcp.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_avrcp.h")


### Functions

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_ct_init(void)
:   Initialize the bluetooth AVRCP controller module.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_ct_deinit(void)
:   Deinitialize the bluetooth AVRCP controller module.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_ct_register_callback([bk_avrcp_ct_cb_t](#_CPPv416bk_avrcp_ct_cb_t "bk_avrcp_ct_cb_t") callback)
:   Register application callbacks to AVRCP module.

    参数
    :   **callback** – **[in]** AVRCP controller callback function

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_ct_send_get_rn_capabilities_cmd(uint8_t *remote_bda)
:   Send GetCapabilities PDU to AVRCP target to retrieve remote device’s supported notification event_ids. This function should be called after BK_AVRCP_CT_CONNECTION_STATE_EVT is received and AVRCP connection is established.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_ct_send_register_notification_cmd(uint8_t *remote_bda, uint8_t event_id, uint32_t event_parameter)
:   Send register notification command to AVRCP target. This function should be called after BK_AVRCP_CT_CONNECTION_STATE_EVT is received and AVRCP connection is established.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address

        - **event_id** – **[in]** : id of events, e.g. BK_AVRCP_RN_PLAY_STATUS_CHANGE, BK_AVRCP_RN_TRACK_CHANGE, etc.

        - **event_parameter** – **[in]** : playback interval for BK_AVRCP_RN_PLAY_POS_CHANGED in second; For other events , value of this parameter is ignored.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_ct_send_passthrough_cmd(uint8_t *remote_bda, uint8_t key_code, uint8_t key_state)
:   Send passthrough command to AVRCP target. This function should be called after BK_AVRCP_CT_CONNECTION_STATE_EVT is received and AVRCP connection is established.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address.

        - **key_code** – **[in]** : passthrough command code, e.g. BK_AVRCP_PT_CMD_PLAY, BK_AVRCP_PT_CMD_STOP, etc.

        - **key_state** – **[in]** : passthrough command key state, BK_AVRCP_PT_CMD_STATE_PRESSED or BK_AVRCP_PT_CMD_STATE_RELEASED

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_ct_send_absolute_volume_cmd(uint8_t *remote_bda, uint8_t volume)
:   Send set absolute volume command to AVRCP target. This function should be called after BK_AVRCP_CT_CONNECTION_STATE_EVT is received and AVRCP connection is established.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address.

        - **volume** – **[in]** : volume, 0 to 0x7f, means 0% to 100%

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_ct_send_set_player_app_setting_cmd(uint8_t *remote_bda, uint8_t attr_id, uint8_t value_id)
:   Send player application settings command to AVRCP target. This function should be called after BK_AVRCP_CT_CONNECTION_STATE_EVT is received and AVRCP connection is established.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address.

        - **attr_id** – **[in]** : player application setting attribute IDs from one of bk_avrcp_ps_attr_ids_t

        - **value_id** – **[in]** : attribute value defined for the specific player application setting attribute

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_ct_send_get_elem_attribute_cmd(uint8_t *remote_bda, uint32_t media_attr_id_mask)
:   Send get media attr command to AVRCP target. This function should be called after BK_AVRCP_CT_CONNECTION_STATE_EVT is received and AVRCP connection is established.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address.

        - **media_attr_id_mask** – **[in]** : mask of bk_avrcp_media_attr_id_t, such as (1 << BK_AVRCP_MEDIA_ATTR_ID_TITLE) | (1 << BK_AVRCP_MEDIA_ATTR_ID_ARTIST).

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_tg_init(void)
:   Initialize the bluetooth AVRCP target module.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_tg_deinit(void)
:   Deinitialize the bluetooth AVRCP target module.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_tg_register_callback([bk_avrcp_tg_cb_t](#_CPPv416bk_avrcp_tg_cb_t "bk_avrcp_tg_cb_t") callback)
:   Register application callbacks to AVRCP target module.

    参数
    :   **callback** – **[in]** AVRCP target callback function

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_tg_get_rn_evt_cap([bk_avrcp_rn_cap_api_method_t](#_CPPv428bk_avrcp_rn_cap_api_method_t "bk_avrcp_rn_cap_api_method_t") cap, [bk_avrcp_rn_evt_cap_mask_t](#_CPPv426bk_avrcp_rn_evt_cap_mask_t "bk_avrcp_rn_evt_cap_mask_t") *evt_set)
:   Get the requested event notification capabilies on local AVRC target. The capability is returned in a bit mask representation in evt_set. This function should be called after bk_avrcp_tg_init().

    For capability type “BK_AVRCP_RN_CAP_API_METHOD_ALLOWED, the retrieved event set is constant and it covers all of the notification events that can possibly be supported with current implementation.

    For capability type BK_AVRCP_RN_CAP_API_METHOD_CURRENT_ENABLE, the event set covers the notification events selected to be supported under current configuration, The configuration can be changed using bk_avrcp_tg_set_rn_evt_cap().

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_tg_set_rn_evt_cap(const [bk_avrcp_rn_evt_cap_mask_t](#_CPPv426bk_avrcp_rn_evt_cap_mask_t "bk_avrcp_rn_evt_cap_mask_t") *evt_set)
:   Set the event notification capabilities on local AVRCP target. The capability is given in a bit mask representation in evt_set and must be a subset of allowed event IDs with current implementation. This function should be called after bk_avrcp_tg_init().

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

bool bk_bt_avrcp_rn_evt_bit_mask_operation([bk_avrcp_bit_mask_op_t](#_CPPv422bk_avrcp_bit_mask_op_t "bk_avrcp_bit_mask_op_t") op, [bk_avrcp_rn_evt_cap_mask_t](#_CPPv426bk_avrcp_rn_evt_cap_mask_t "bk_avrcp_rn_evt_cap_mask_t") *events, [bk_avrcp_rn_event_ids_t](#_CPPv423bk_avrcp_rn_event_ids_t "bk_avrcp_rn_event_ids_t") event_id)
:   Operate on the type [bk_avrcp_rn_evt_cap_mask_t](#structbk__avrcp__rn__evt__cap__mask__t "#structbk__avrcp__rn__evt__cap__mask__t") with regard to a specific event.

    For operation BK_AVRCP_BIT_MASK_OP_TEST, return true if the corresponding bit is set, otherwise false.

    参数
    :   - **op** – **[in]** operation requested on the bit mask field

        - **events** – **[in]** pointer to event notification capability bit mask structure

        - **event_id** – **[in]** notification event code

    返回
    :   For operation BK_AVRCP_BIT_MASK_OP_SET or BK_AVRCP_BIT_MASK_OP_CLEAR, return true for a successful operation, otherwise return false.

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_tg_send_rn_rsp(uint8_t *addr, [bk_avrcp_rn_event_ids_t](#_CPPv423bk_avrcp_rn_event_ids_t "bk_avrcp_rn_event_ids_t") event_id, [bk_avrcp_rn_rsp_t](#_CPPv417bk_avrcp_rn_rsp_t "bk_avrcp_rn_rsp_t") rsp, [bk_avrcp_rn_param_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t") *param)
:   Send RegisterNotification Response to remote AVRCP controller. Local event notification capability can be set using bk_avrcp_tg_set_rn_evt_cap(), in a bit mask representation in evt_set. This function should be called after bk_avrcp_tg_init().

    参数
    :   - **addr** – **[in]** peer addr

        - **event_id** – **[in]** notification event ID that remote AVRCP CT registers

        - **rsp** – **[in]** notification response code

        - **param** – **[in]** parameters included in the specific notification

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_tg_get_psth_cmd_filter([bk_avrcp_psth_filter_t](#_CPPv422bk_avrcp_psth_filter_t "bk_avrcp_psth_filter_t") filter, [bk_avrcp_psth_bit_mask_t](#_CPPv424bk_avrcp_psth_bit_mask_t "bk_avrcp_psth_bit_mask_t") *cmd_set)
:   Get the current filter of remote passthrough commands on AVRC target. Filter is given by filter type and bit mask for the passthrough commands. This function should be called after [bk_bt_avrcp_tg_init()](#group__dm__avrcp_1ga0f43a498c80b739f64c0bd8e8750e851 "#group__dm__avrcp_1ga0f43a498c80b739f64c0bd8e8750e851"). For filter type BK_AVRCP_PSTH_FILTER_METHOD_ALLOWED, the retrieved command set is constant and it covers all of the passthrough commands that can possibly be supported. For filter type BK_AVRCP_PSTH_FILTER_METHOD_CURRENT_ENABLE, the retrieved command set covers the passthrough commands selected to be supported according to current configuration. The configuration can be changed using [bk_bt_avrcp_tg_set_psth_cmd_filter()](#group__dm__avrcp_1ga4f02fd8c38fd08c72e06a633cfdca1ad "#group__dm__avrcp_1ga4f02fd8c38fd08c72e06a633cfdca1ad").

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_tg_set_psth_cmd_filter([bk_avrcp_psth_filter_t](#_CPPv422bk_avrcp_psth_filter_t "bk_avrcp_psth_filter_t") filter, const [bk_avrcp_psth_bit_mask_t](#_CPPv424bk_avrcp_psth_bit_mask_t "bk_avrcp_psth_bit_mask_t") *cmd_set)
:   Set the filter of remote passthrough commands on AVRC target. Filter is given by filter type and bit mask for the passthrough commands. This function should be called after [bk_bt_avrcp_tg_init()](#group__dm__avrcp_1ga0f43a498c80b739f64c0bd8e8750e851 "#group__dm__avrcp_1ga0f43a498c80b739f64c0bd8e8750e851").

    If filter type is BK_AVRCP_PSTH_FILTER_METHOD_ALLOWED, the passthrough commands which are set “1” as given in cmd_set will generate BK_AVRCP_CT_PASSTHROUGH_RSP_EVT callback event and are auto-accepted in the protocol stack, other commands are replied with response type “NOT IMPLEMENTED” (8). The set of supported commands should be a subset of allowed command set. The allowed command set can be retrieved using [bk_bt_avrcp_tg_get_psth_cmd_filter()](#group__dm__avrcp_1ga0b28fe5943a876887a6175eb3fe8b747 "#group__dm__avrcp_1ga0b28fe5943a876887a6175eb3fe8b747") with filter type “BK_AVRCP_PSTH_FILTER_METHOD_CURRENT_ENABLE”.

    Filter type “BK_AVRCP_PSTH_FILTER_METHOD_ALLOWED” does not apply to this function.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

bool bk_bt_avrcp_psth_bit_mask_operation([bk_avrcp_bit_mask_op_t](#_CPPv422bk_avrcp_bit_mask_op_t "bk_avrcp_bit_mask_op_t") op, [bk_avrcp_psth_bit_mask_t](#_CPPv424bk_avrcp_psth_bit_mask_t "bk_avrcp_psth_bit_mask_t") *psth, [bk_avrcp_pt_cmd_t](#_CPPv417bk_avrcp_pt_cmd_t "bk_avrcp_pt_cmd_t") cmd)
:   Operate on the type [bk_avrcp_psth_bit_mask_t](#structbk__avrcp__psth__bit__mask__t "#structbk__avrcp__psth__bit__mask__t") with regard to a specific PASSTHROUGH command.

    参数
    :   - **op** – **[in]** operation requested on the bit mask field

        - **psth** – **[in]** pointer to passthrough command bit mask structure

        - **cmd** – **[in]** passthrough command code

    返回
    :   For operation BK_AVRCP_BIT_MASK_OP_SET or BK_AVRCP_BIT_MASK_OP_CLEAR, return true for a successful operation, otherwise return false. For operation BK_AVRCP_BIT_MASK_OP_TEST, return true if the corresponding bit is set, otherwise false.

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_avrcp_connect(uint8_t *remote_bda)
:   Connect to remote bluetooth AVRCP. This API must be called after [bk_bt_avrcp_ct_init()](#group__dm__avrcp_1ga05f83b873d0086a261259a7523ea3e0f "#group__dm__avrcp_1ga05f83b873d0086a261259a7523ea3e0f") or bk_bt_avrcp_tg_init.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail


## bk_dm_hfp.h

`bk_dm_hfp.h` 提供 HFP 免提通话、SCO 音频和 AT 交互接口。


### Header File


- [bluetooth/bk_dm_hfp.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_hfp.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_hfp.h")


### Functions

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_register_callback([bk_bt_hf_client_cb_t](#_CPPv420bk_bt_hf_client_cb_t "bk_bt_hf_client_cb_t") callback)
:   Register application callback function to HFP client module.

    参数
    :   **callback** – **[in]** HFP client event callback function

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_init(uint8_t msbc_supported)
:   Initialize the bluetooth HFP client module.

    参数
    :   **msbc_supported** – **[in]** 1 means msbc is supported, 0 means msbc is not supported.

    返回
    :   - BK_ERR_BT_SUCCESS: the initialization request is successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_deinit(void)
:   De-initialize for HFP client module.

    返回
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_register_data_callback([bk_bt_hf_client_data_cb_t](#_CPPv425bk_bt_hf_client_data_cb_t "bk_bt_hf_client_data_cb_t") callback)
:   Register HFP client data input function;.

    参数
    :   **callback** – **[in]** HFP client incoming data callback function

    返回
    :   - BK_ERR_BT_SUCCESS: the initialization request is successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_voice_out_write(uint8_t *remote_bda, uint8_t *buf, uint16_t len)
:   Send voice data to HFP AG;.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address

        - **buf** – **[in]** : pointer to the data

        - **len** – **[in]** : size(in bytes) in buf

    返回
    :   - BK_ERR_BT_SUCCESS: the initialization request is successfully

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_connect(uint8_t *remote_bda)
:   Establish a Service Level Connection to remote bluetooth HFP audio gateway(AG) device. This function must be called after bk_bt_hf_client_init().

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: connect request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_disconnect(uint8_t *remote_bda)
:   Disconnect from the remote HFP audio gateway. This function must be called after bk_bt_hf_client_init().

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: connect request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_connect_audio(uint8_t *remote_bda)
:   Create audio connection with remote HFP AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: connect request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_disconnect_audio(uint8_t *remote_bda)
:   Release the established audio connection with remote HFP AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: disconnect request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_start_voice_recognition(uint8_t *remote_bda)
:   Enable voice recognition in the AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_stop_voice_recognition(uint8_t *remote_bda)
:   Disable voice recognition in the AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_volume_update(uint8_t *remote_bda, [bk_hf_volume_control_target_t](#_CPPv429bk_hf_volume_control_target_t "bk_hf_volume_control_target_t") type, uint8_t volume)
:   Volume synchronization with AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address

        - **type** – **[in]** volume control target, speaker or microphone

        - **volume** – **[in]** gain of the speaker of microphone, ranges 0 to 15

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_dial(uint8_t *remote_bda, const char *number)
:   Place a call with a specified number, if number is NULL, last called number is called. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address

        - **number** – **[in]** number string of the call. If NULL, the last number is called(aka re-dial)

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_dial_memory(uint8_t *remote_bda, int location)
:   Place a call with number specified by location(speed dial). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address

        - **location** – **[in]** location of the number in the memory

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_send_chld_cmd(uint8_t *remote_bda, [bk_hf_chld_type_t](#_CPPv417bk_hf_chld_type_t "bk_hf_chld_type_t") chld)
:   Send call hold and multiparty commands(Use AT+CHLD). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address

        - **chld** – **[in]** AT+CHLD call hold and multiparty handling AT command.

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_send_btrh_cmd(uint8_t *remote_bda, [bk_hf_btrh_cmd_t](#_CPPv416bk_hf_btrh_cmd_t "bk_hf_btrh_cmd_t") btrh)
:   Send response and hold action command(Send AT+BTRH command) As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address

        - **btrh** – **[in]** response and hold action to send

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_answer_call(uint8_t *remote_bda)
:   Answer an incoming call(send ATA command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_reject_call(uint8_t *remote_bda)
:   Reject an incoming call(send AT+CHUP command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_query_current_calls(uint8_t *remote_bda)
:   Query list of current calls in AG(send AT+CLCC command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_query_current_operator_name(uint8_t *remote_bda)
:   Query the name of currently selected network operator in AG(use AT+COPS commands). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_retrieve_subscriber_info(uint8_t *remote_bda)
:   Get subscriber information number from AG(send AT+CNUM command) As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_send_dtmf(uint8_t *remote_bda, const char *code)
:   Transmit DTMF codes during an ongoing call(use AT+VTS commands) As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address

        - **code** – **[in]** string of the dtmf code

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_request_last_voice_tag_number(uint8_t *remote_bda)
:   Request a phone number from AG corresponding to last voice tag recorded (send AT+BINP command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_send_nrec(uint8_t *remote_bda)
:   Disable echo cancellation and noise reduction in the AG (use AT+NREC=0 command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_redial(uint8_t *remote_bda)
:   This API allows user to redial the last number dialed (use AT+BLDN command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote_bda** – **[in]** remote bluetooth device address

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_hf_client_send_custom_cmd(uint8_t *remote_bda, const char *atcmd)
:   This API allows user to send custom AT Command. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote_bda** – **[in]** remote bluetooth device address

        - **atcmd** – **[in]** string of the custom atcmd.

    返回
    :   - BK_ERR_BT_SUCCESS: request is sent to lower layer

        - others: fail


## bk_dm_hidd.h

`bk_dm_hidd.h` 提供 Bluetooth HID Device profile 接口。


### Header File


- [bluetooth/bk_dm_hidd.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_hidd.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_hidd.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_register_callback([bk_hd_cb_t](#_CPPv410bk_hd_cb_t "bk_hd_cb_t") callback)
:   This function is called to init callbacks with HID device module.

    参数
    :   **callback** – **[in]** pointer to the init callback function.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_init(void)
:   Initializes HIDD interface. This function should be called after bk_bluedroid_init() and bk_bluedroid_enable() success, and should be called after bk_bt_hid_device_register_callback. When the operation is complete, the callback function will be called with BK_HIDD_INIT_EVT.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_deinit(void)
:   De-initializes HIDD interface. This function should be called after bk_bluedroid_init() and bk_bluedroid_enable() success, and should be called after bk_bt_hid_device_init(). When the operation is complete, the callback function will be called with BK_HIDD_DEINIT_EVT.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_register_app([bk_hidd_app_param_t](#_CPPv419bk_hidd_app_param_t "bk_hidd_app_param_t") *app_param)
:   Registers HIDD parameters with SDP and sets l2cap Quality of Service. This function should be called after [bk_bluetooth_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2 "dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2") success, and should be called after bk_bt_hid_device_init(). When the operation is complete, the callback function will be called with BK_HIDD_REGISTER_APP_EVT.

    参数
    :   **app_param** – **[in]** HIDD parameters

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_unregister_app(void)
:   Removes HIDD parameters from SDP and resets l2cap Quality of Service. This function should be called after [bk_bluetooth_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2 "dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2") success, and should be called after bk_bt_hid_device_init(). When the operation is complete, the callback function will be called with BK_HIDD_UNREGISTER_APP_EVT.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_connect([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   Connects to the peer HID Host with virtual cable. This function should be called after [bk_bluetooth_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2 "dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2") success, and should be called after bk_bt_hid_device_init(). When the operation is complete, the callback function will be called with BK_HIDD_OPEN_EVT.

    参数
    :   **bd_addr** – **[in]** Remote host bluetooth device address.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_disconnect(void)
:   Disconnects from the currently connected HID Host. This function should be called after [bk_bluetooth_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2 "dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2") success, and should be called after bk_bt_hid_device_init(). When the operation is complete, the callback function will be called with BK_HIDD_CLOSE_EVT.

    备注

    The disconnect operation will not remove the virtually cabled device. If the connect request from the different HID Host, it will reject the request.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_send_report(uint16_t len, uint8_t *data)
:   Sends HID report to the currently connected HID Host. This function should be called after [bk_bluetooth_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2 "dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2") success, and should be called after bk_bt_hid_device_init(). When the operation is complete, the callback function will be called with BK_HIDD_SEND_REPORT_EVT.

    参数
    :   - **len** – **[in]** length of report

        - **data** – **[in]** report data

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_send_response(uint8_t message_type, uint8_t res_status, uint16_t len, uint8_t *data)
:   Sends HID Handshake with error info for invalid set_report to the currently connected HID Host. This function should be called after [bk_bluetooth_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2 "dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2") success, and should be called after bk_bt_hid_device_init(). When the operation is complete, the callback function will be called with BK_HIDD_REPORT_ERR_EVT.

    参数
    :   - **message_type** – **[in]** type of hid message

        - **res_status** – **[in]** response status

        - **len** – **[in]** response data len

        - **data** – **[in]** response data

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_device_virtual_cable_unplug(void)
:   Remove the virtually cabled device. This function should be called after [bk_bluetooth_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2 "dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2") success, and should be called after bk_bt_hid_device_init(). When the operation is complete, the callback function will be called with BK_HIDD_VC_UNPLUG_EVT.

    备注

    If the connection exists, then HID Device will send a `VIRTUAL_CABLE_UNPLUG` control command to the peer HID Host, and the connection will be destroyed. If the connection does not exist, then HID Device will only unplug on it’s single side. Once the unplug operation is success, the related pairing and bonding information will be removed, then the HID Device can accept connection request from the different HID Host,

    返回
    :   - BK_OK: success


        - other: failed


### Unions

union bk_hidd_cb_param_t
:   *#include <bk_dm_hidd.h>*

    HID device callback parameters union.

    Public Members

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_init_evt_param](#_CPPv4N18bk_hidd_cb_param_t19hidd_init_evt_paramE "bk_hidd_cb_param_t::hidd_init_evt_param") init
    :   HIDD callback param of BK_HIDD_INIT_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_deinit_evt_param](#_CPPv4N18bk_hidd_cb_param_t21hidd_deinit_evt_paramE "bk_hidd_cb_param_t::hidd_deinit_evt_param") deinit
    :   HIDD callback param of BK_HIDD_DEINIT_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_register_app_evt_param](#_CPPv4N18bk_hidd_cb_param_t27hidd_register_app_evt_paramE "bk_hidd_cb_param_t::hidd_register_app_evt_param") register_app
    :   HIDD callback param of BK_HIDD_REGISTER_APP_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_unregister_app_evt_param](#_CPPv4N18bk_hidd_cb_param_t29hidd_unregister_app_evt_paramE "bk_hidd_cb_param_t::hidd_unregister_app_evt_param") unregister_app
    :   HIDD callback param of BK_HIDD_UNREGISTER_APP_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_open_evt_param](#_CPPv4N18bk_hidd_cb_param_t19hidd_open_evt_paramE "bk_hidd_cb_param_t::hidd_open_evt_param") open
    :   HIDD callback param of BK_HIDD_OPEN_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_close_evt_param](#_CPPv4N18bk_hidd_cb_param_t20hidd_close_evt_paramE "bk_hidd_cb_param_t::hidd_close_evt_param") close
    :   HIDD callback param of BK_HIDD_CLOSE_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_send_report_evt_param](#_CPPv4N18bk_hidd_cb_param_t26hidd_send_report_evt_paramE "bk_hidd_cb_param_t::hidd_send_report_evt_param") send_report
    :   HIDD callback param of BK_HIDD_SEND_REPORT_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_report_err_evt_param](#_CPPv4N18bk_hidd_cb_param_t25hidd_report_err_evt_paramE "bk_hidd_cb_param_t::hidd_report_err_evt_param") report_err
    :   HIDD callback param of BK_HIDD_REPORT_ERR_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_get_report_evt_param](#_CPPv4N18bk_hidd_cb_param_t25hidd_get_report_evt_paramE "bk_hidd_cb_param_t::hidd_get_report_evt_param") get_report
    :   HIDD callback param of BK_HIDD_GET_REPORT_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_set_report_evt_param](#_CPPv4N18bk_hidd_cb_param_t25hidd_set_report_evt_paramE "bk_hidd_cb_param_t::hidd_set_report_evt_param") set_report
    :   HIDD callback param of BK_HIDD_SET_REPORT_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_set_protocol_evt_param](#_CPPv4N18bk_hidd_cb_param_t27hidd_set_protocol_evt_paramE "bk_hidd_cb_param_t::hidd_set_protocol_evt_param") set_protocol
    :   HIDD callback param of BK_HIDD_SET_PROTOCOL_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_get_protocol_evt_param](#_CPPv4N18bk_hidd_cb_param_t27hidd_get_protocol_evt_paramE "bk_hidd_cb_param_t::hidd_get_protocol_evt_param") get_protocol
    :   HIDD callback param of BK_HIDD_GET_PROTOCOL_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_get_idle_evt_param](#_CPPv4N18bk_hidd_cb_param_t23hidd_get_idle_evt_paramE "bk_hidd_cb_param_t::hidd_get_idle_evt_param") get_idle
    :   HIDD callback param of BK_HIDD_GET_IDLE_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_set_idle_evt_param](#_CPPv4N18bk_hidd_cb_param_t23hidd_set_idle_evt_paramE "bk_hidd_cb_param_t::hidd_set_idle_evt_param") set_idle
    :   HIDD callback param of BK_HIDD_SET_IDLE_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_intr_data_evt_param](#_CPPv4N18bk_hidd_cb_param_t24hidd_intr_data_evt_paramE "bk_hidd_cb_param_t::hidd_intr_data_evt_param") intr_data
    :   HIDD callback param of BK_HIDD_INTR_DATA_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_ctrl_op_evt_param](#_CPPv4N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_paramE "bk_hidd_cb_param_t::hidd_ctrl_op_evt_param") ctrl_op
    :   HIDD callback param of BK_HIDD_INTR_DATA_EVT

    struct [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd_vc_unplug_param](#_CPPv4N18bk_hidd_cb_param_t20hidd_vc_unplug_paramE "bk_hidd_cb_param_t::hidd_vc_unplug_param") vc_unplug
    :   HIDD callback param of BK_HIDD_VC_UNPLUG_EVT

    struct hidd_close_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_CLOSE_EVT.

        Public Members

        [bk_hidd_status_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        [bk_hidd_connection_state_t](#_CPPv426bk_hidd_connection_state_t "bk_hidd_connection_state_t") conn_status
        :   connection status

    struct hidd_ctrl_op_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_CTRL_OP_EVT.

        Public Members

        [bk_hidd_message_type_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message_type
        :   message type

        [bk_hidd_ctrl_op_t](#_CPPv417bk_hidd_ctrl_op_t "bk_hidd_ctrl_op_t") op
        :   ctral operation

    struct hidd_deinit_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_DEINIT_EVT.

        Public Members

        [bk_hidd_status_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

    struct hidd_get_idle_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_GET_IDLE_EVT.

        Public Members

        [bk_hidd_message_type_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message_type
        :   message type

    struct hidd_get_protocol_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_GET_PROTOCOL_EVT.

        Public Members

        [bk_hidd_message_type_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message_type
        :   message type

    struct hidd_get_report_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_GET_REPORT_EVT.

        Public Members

        [bk_hidd_message_type_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message_type
        :   message type

        [bk_hidd_report_type_t](#_CPPv421bk_hidd_report_type_t "bk_hidd_report_type_t") report_type
        :   report type

        uint8_t report_id
        :   report id

        uint16_t buffer_size
        :   buffer size

    struct hidd_init_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_INIT_EVT.

        Public Members

        [bk_hidd_status_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

    struct hidd_intr_data_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_INTR_DATA_EVT.

        Public Members

        [bk_hidd_message_type_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message_type
        :   message type

        [bk_hidd_report_type_t](#_CPPv421bk_hidd_report_type_t "bk_hidd_report_type_t") report_type
        :   report type

        uint8_t report_id
        :   interrupt channel report id

        uint16_t len
        :   interrupt channel report data length

        uint8_t *data
        :   interrupt channel report data pointer

    struct hidd_open_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_OPEN_EVT.

        Public Members

        [bk_hidd_status_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        [bk_hidd_connection_state_t](#_CPPv426bk_hidd_connection_state_t "bk_hidd_connection_state_t") conn_status
        :   connection status

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
        :   host address

    struct hidd_register_app_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_REGISTER_APP_EVT.

        Public Members

        [bk_hidd_status_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        bool in_use
        :   indicate whether use virtual cable plug host address

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
        :   host address

    struct hidd_report_err_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_REPORT_ERR_EVT.

        Public Members

        [bk_hidd_status_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        uint8_t reason
        :   lower layer failed reason(ref hiddefs.h)

    struct hidd_send_report_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_SEND_REPORT_EVT.

        Public Members

        [bk_hidd_status_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        uint8_t report_id
        :   report id

    struct hidd_set_idle_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_SET_IDLE_EVT.

        Public Members

        [bk_hidd_message_type_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message_type
        :   message type

        uint8_t idle
        :   idle rate

    struct hidd_set_protocol_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_SET_PROTOCOL_EVT.

        Public Members

        [bk_hidd_protocol_mode_t](#_CPPv423bk_hidd_protocol_mode_t "bk_hidd_protocol_mode_t") protocol_mode
        :   protocol mode

    struct hidd_set_report_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_SET_REPORT_EVT.

        Public Members

        [bk_hidd_message_type_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message_type
        :   message type

        [bk_hidd_report_type_t](#_CPPv421bk_hidd_report_type_t "bk_hidd_report_type_t") report_type
        :   report type

        uint8_t report_id
        :   report id

        uint16_t len
        :   set_report data length

        uint8_t *data
        :   set_report data pointer

    struct hidd_unregister_app_evt_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_UNREGISTER_APP_EVT.

        Public Members

        [bk_hidd_status_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

    struct hidd_vc_unplug_param
    :   *#include <bk_dm_hidd.h>*

        BK_HIDD_VC_UNPLUG_EVT.

        Public Members

        [bk_hidd_status_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        [bk_hidd_connection_state_t](#_CPPv426bk_hidd_connection_state_t "bk_hidd_connection_state_t") conn_status
        :   connection status


### Structures

struct bk_hidd_app_param_t
:   HID device characteristics for SDP server.

    Public Members

    char *name
    :   service name

    char *description
    :   service description

    char *provider
    :   provider name

    uint8_t *subclass
    :   HID device subclass

    uint8_t *desc_list
    :   HID descriptor list

    int desc_list_len
    :   size in bytes of HID descriptor list

struct bk_hidd_qos_param_t
:   HIDD Quality of Service parameters negotiated over L2CAP.

    Public Members

    uint8_t service_type
    :   the level of service, 0 indicates no traffic

    uint32_t token_rate
    :   token rate in bytes per second, 0 indicates “don’t care”

    uint32_t token_bucket_size
    :   limit on the burstness of the application data

    uint32_t peak_bandwidth
    :   bytes per second, value 0 indicates “don’t care”

    uint32_t access_latency
    :   maximum acceptable delay in microseconds

    uint32_t delay_variation
    :   the difference in microseconds between the max and min delay


### Macros

BK_HID_CLASS_UNKNOWN
:   subclass of hid device

    unknown HID device subclass

BK_HID_CLASS_JOS
:   joystick

BK_HID_CLASS_GPD
:   game pad

BK_HID_CLASS_RMC
:   remote control

BK_HID_CLASS_SED
:   sensing device

BK_HID_CLASS_DGT
:   digitizer tablet

BK_HID_CLASS_CDR
:   card reader

BK_HID_CLASS_KBD
:   keyboard

BK_HID_CLASS_MIC
:   pointing device

BK_HID_CLASS_COM
:   combo keyboard/pointing


### Type Definitions

typedef void (*bk_hd_cb_t)([bk_hidd_cb_event_t](#_CPPv418bk_hidd_cb_event_t "bk_hidd_cb_event_t") event, [bk_hidd_cb_param_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t") *param)
:   HID device callback function type.

    Param event
    :   Event type

    Param param
    :   Point to callback parameter, currently is union type


### Enumerations

enum bk_hidd_handshake_error_t
:   HIDD handshake result code.


    *Values:*

    enumerator BK_HID_PAR_HANDSHAKE_RSP_SUCCESS
    :   successful

    enumerator BK_HID_PAR_HANDSHAKE_RSP_NOT_READY
    :   not ready, device is too busy to accept data

    enumerator BK_HID_PAR_HANDSHAKE_RSP_ERR_INVALID_REP_ID
    :   invalid report ID

    enumerator BK_HID_PAR_HANDSHAKE_RSP_ERR_UNSUPPORTED_REQ
    :   device does not support the request

    enumerator BK_HID_PAR_HANDSHAKE_RSP_ERR_INVALID_PARAM
    :   parameter value is out of range or inappropriate

    enumerator BK_HID_PAR_HANDSHAKE_RSP_ERR_UNKNOWN
    :   device could not identify the error condition

    enumerator BK_HID_PAR_HANDSHAKE_RSP_ERR_FATAL
    :   restart is essential to resume functionality

enum bk_hidd_message_type_t
:   HIDD message types.


    *Values:*

    enumerator BK_HIDD_MESSAGE_TYPE_HANDSHAKE
    :   handshake type

    enumerator BK_HIDD_MESSAGE_TYPE_HID_CONTROL
    :   hid control type

    enumerator BK_HIDD_MESSAGE_TYPE_GET_REPORT
    :   get report

    enumerator BK_HIDD_MESSAGE_TYPE_SET_REPORT
    :   set report

    enumerator BK_HIDD_MESSAGE_TYPE_GET_PROTOCOL
    :   get protocol

    enumerator BK_HIDD_MESSAGE_TYPE_SET_PROTOCOL
    :   set protocol

    enumerator BK_HIDD_MESSAGE_TYPE_GET_IDLE
    :   get idle [DEPRECATED]

    enumerator BK_HIDD_MESSAGE_TYPE_SET_IDLE
    :   set idle [DEPRECATED]

    enumerator BK_HIDD_MESSAGE_TYPE_DATA
    :   data intr

enum bk_hidd_report_type_t
:   HIDD report types.


    *Values:*

    enumerator BK_HIDD_REPORT_TYPE_RESERVED
    :   reserved

    enumerator BK_HIDD_REPORT_TYPE_INPUT
    :   input report

    enumerator BK_HIDD_REPORT_TYPE_OUTPUT
    :   output report

    enumerator BK_HIDD_REPORT_TYPE_FEATURE
    :   feature report

enum bk_hidd_ctrl_op_t
:   HIDD control operation.


    *Values:*

    enumerator BK_HIDD_CTRL_OP_NOP
    :   no operation

    enumerator BK_HIDD_CTRL_OP_HARD_RESET
    :   hadr reset

    enumerator BK_HIDD_CTRL_OP_SOFT_RESET
    :   soft reset

    enumerator BK_HIDD_CTRL_OP_SUSPEND
    :   suspend

    enumerator BK_HIDD_CTRL_OP_EXIT_SUSPEND
    :   exit suspend

enum bk_hidd_connection_state_t
:   HIDD connection state.


    *Values:*

    enumerator BK_HIDD_CONN_STATE_CONNECTED
    :   HID connection established

    enumerator BK_HIDD_CONN_STATE_CONNECTING
    :   connection to remote Bluetooth device

    enumerator BK_HIDD_CONN_STATE_DISCONNECTED
    :   connection released

    enumerator BK_HIDD_CONN_STATE_DISCONNECTING
    :   disconnecting to remote Bluetooth device

    enumerator BK_HIDD_CONN_STATE_UNKNOWN
    :   unknown connection state

enum bk_hidd_protocol_mode_t
:   HID device protocol modes.


    *Values:*

    enumerator BK_HIDD_REPORT_MODE
    :   Report Protocol Mode

    enumerator BK_HIDD_BOOT_MODE
    :   Boot Protocol Mode

    enumerator BK_HIDD_UNSUPPORTED_MODE
    :   unsupported

enum bk_hidd_boot_report_id_t
:   HID Boot Protocol report IDs.


    *Values:*

    enumerator BK_HIDD_BOOT_REPORT_ID_KEYBOARD
    :   report ID of Boot Protocol keyboard report

    enumerator BK_HIDD_BOOT_REPORT_ID_MOUSE
    :   report ID of Boot Protocol mouse report

enum [anonymous]
:   HID Boot Protocol report size including report ID.


    *Values:*

    enumerator BK_HIDD_BOOT_REPORT_SIZE_KEYBOARD
    :   report size of Boot Protocol keyboard report

    enumerator BK_HIDD_BOOT_REPORT_SIZE_MOUSE
    :   report size of Boot Protocol mouse report

enum bk_hidd_cb_event_t
:   HID device callback function events.


    *Values:*

    enumerator BK_HIDD_INIT_EVT
    :   When HID device is initialized, the event comes

    enumerator BK_HIDD_DEINIT_EVT
    :   When HID device is deinitialized, the event comes

    enumerator BK_HIDD_REGISTER_APP_EVT
    :   When HID device application registered, the event comes

    enumerator BK_HIDD_UNREGISTER_APP_EVT
    :   When HID device application unregistered, the event comes

    enumerator BK_HIDD_OPEN_EVT
    :   When HID device connection to host opened, the event comes

    enumerator BK_HIDD_CLOSE_EVT
    :   When HID device connection to host closed, the event comes

    enumerator BK_HIDD_SEND_REPORT_EVT
    :   When HID device send report to lower layer, the event comes

    enumerator BK_HIDD_REPORT_ERR_EVT
    :   When HID device report handshanke error to lower layer, the event comes

    enumerator BK_HIDD_GET_REPORT_EVT
    :   When HID device receives GET_REPORT request from host, the event comes

    enumerator BK_HIDD_SET_REPORT_EVT
    :   When HID device receives SET_REPORT request from host, the event comes

    enumerator BK_HIDD_GET_PROTOCOL_EVT
    :   When HID device receives GET_PROTOCOL request from host, the event comes

    enumerator BK_HIDD_SET_PROTOCOL_EVT
    :   When HID device receives SET_PROTOCOL request from host, the event comes

    enumerator BK_HIDD_GET_IDLE_EVT
    :   When HID device receives GET_IDLE request from host, the event comes

    enumerator BK_HIDD_SET_IDLE_EVT
    :   When HID device receives SET_IDLE request from host, the event comes

    enumerator BK_HIDD_INTR_DATA_EVT
    :   When HID device receives DATA from host on intr, the event comes

    enumerator BK_HIDD_CONTROL_EVT
    :   When HID device receives HID_CONTROL from host, the event comes

    enumerator BK_HIDD_VC_UNPLUG_EVT
    :   When HID device initiates Virtual Cable Unplug, the event comes

    enumerator BK_HIDD_API_ERR_EVT
    :   When HID device has API error, the event comes

enum bk_hidd_status_t
:   *Values:*

    enumerator BK_HIDD_SUCCESS

    enumerator BK_HIDD_ERROR
    :   general BK HD error

    enumerator BK_HIDD_NO_RES
    :   out of system resources

    enumerator BK_HIDD_BUSY
    :   Temporarily can not handle this request.

    enumerator BK_HIDD_NO_DATA
    :   No data.

    enumerator BK_HIDD_NEED_INIT
    :   HIDD module shall init first

    enumerator BK_HIDD_NEED_DEINIT
    :   HIDD module shall deinit first

    enumerator BK_HIDD_NEED_REG
    :   HIDD module shall register first

    enumerator BK_HIDD_NEED_DEREG
    :   HIDD module shall deregister first

    enumerator BK_HIDD_NO_CONNECTION
    :   connection may have been closed

    enumerator BK_HIDD_NO_ACL_LINK
    :   Baseband acl link not exist

    enumerator BK_HIDD_FAIL
    :   HIDD Fail


## bk_dm_hidh.h

`bk_dm_hidh.h` 提供 Bluetooth HID Host profile 接口。


### Header File


- [bluetooth/bk_dm_hidh.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_hidh.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_hidh.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_register_callback([bk_hh_cb_t](#_CPPv410bk_hh_cb_t "bk_hh_cb_t") callback)
:   This function is called to init callbacks with HID host module.

    参数
    :   **callback** – **[in]** pointer to the init callback function.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_init(void)
:   This function initializes HID host. This function should be called after [bk_bluetooth_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2 "dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2") success, and should be called after bk_bt_hid_host_register_callback(). When the operation is complete the callback function will be called with BK_HIDH_INIT_EVT.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_deinit(void)
:   Closes the interface. This function should be called after [bk_bluetooth_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2 "dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2") success, and should be called after bk_bt_hid_host_init(). When the operation is complete the callback function will be called with BK_HIDH_DEINIT_EVT.

    返回
    :   - BK_OK: success


        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_connect([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   Connect to HID device. When the operation is complete the callback function will be called with BK_HIDH_OPEN_EVT.

    参数
    :   **bd_addr** – **[in]** Remote device bluetooth device address.

    返回
    :   - BK_OK: success


        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_disconnect([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   Disconnect from HID device. When the operation is complete the callback function will be called with BK_HIDH_CLOSE_EVT.

    参数
    :   **bd_addr** – **[in]** Remote device bluetooth device address.

    返回
    :   - BK_OK: success


        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_virtual_cable_unplug([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   Virtual UnPlug (VUP) the specified HID device. When the operation is complete the callback function will be called with BK_HIDH_VC_UNPLUG_EVT.

    参数
    :   **bd_addr** – **[in]** Remote device bluetooth device address.

    返回
    :   - BK_OK: success


        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_set_info([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, [bk_hidh_hid_info_t](#_CPPv418bk_hidh_hid_info_t "bk_hidh_hid_info_t") *hid_info)
:   Set the HID device descriptor for the specified HID device. When the operation is complete the callback function will be called with BK_HIDH_SET_INFO_EVT.

    参数
    :   - **bd_addr** – **[in]** Remote device bluetooth device address.

        - **hid_info** – **[in]** HID device descriptor structure.

    返回
    :   - BK_OK: success


        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_get_protocol([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   Get the HID proto mode. When the operation is complete the callback function will be called with BK_HIDH_GET_PROTO_EVT.

    参数
    :   **bd_addr** – **[in]** Remote device bluetooth device address.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_set_protocol([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, [bk_hidh_protocol_mode_t](#_CPPv423bk_hidh_protocol_mode_t "bk_hidh_protocol_mode_t") protocol_mode)
:   Set the HID proto mode. When the operation is complete the callback function will be called with BK_HIDH_SET_PROTO_EVT.

    参数
    :   - **bd_addr** – **[in]** Remote device bluetooth device address.

        - **protocol_mode** – **[in]** Protocol mode type.

    返回
    :   - BK_OK: success

        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_get_report([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, [bk_hidh_report_type_t](#_CPPv421bk_hidh_report_type_t "bk_hidh_report_type_t") report_type, uint8_t report_id, int buffer_size)
:   Send a GET_REPORT to HID device. When the operation is complete the callback function will be called with BK_HIDH_GET_RPT_EVT.

    参数
    :   - **bd_addr** – **[in]** Remote device bluetooth device address.

        - **report_type** – **[in]** Report type

        - **report_id** – **[in]** Report id

        - **buffer_size** – **[in]** Buffer size

    返回
    :   - BK_OK: success


        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_set_report([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, [bk_hidh_report_type_t](#_CPPv421bk_hidh_report_type_t "bk_hidh_report_type_t") report_type, uint8_t *report, size_t len)
:   Send a SET_REPORT to HID device. When the operation is complete the callback function will be called with BK_HIDH_SET_RPT_EVT.

    参数
    :   - **bd_addr** – **[in]** Remote device bluetooth device address.

        - **report_type** – **[in]** Report type

        - **report** – **[in]** Report data pointer

        - **len** – **[in]** Report data length

    返回
    :   - BK_OK: success


        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_send_data([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, uint8_t *data, size_t len)
:   Send data to HID device. When the operation is complete the callback function will be called with BK_HIDH_DATA_EVT.

    参数
    :   - **bd_addr** – **[in]** Remote device bluetooth device address.

        - **data** – **[in]** Data pointer

        - **len** – **[in]** Data length

    返回
    :   - BK_OK: success


        - other: failed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_hid_host_sdp_dscp([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   Start SDP. When the operation is complete the callback function will be called with BK_HIDH_SDP_DSCP_EVT.

    参数
    :   **bd_addr** – **[in]** Remote device bluetooth device address.

    返回
    :   - BK_OK: success


        - other: failed


### Unions

union bk_hidh_cb_param_t
:   *#include <bk_dm_hidh.h>*

    HID host callback parameters union.

    Public Members

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_init_evt_param](#_CPPv4N18bk_hidh_cb_param_t19hidh_init_evt_paramE "bk_hidh_cb_param_t::hidh_init_evt_param") init
    :   HIDH callback param of BK_HIDH_INIT_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_uninit_evt_param](#_CPPv4N18bk_hidh_cb_param_t21hidh_uninit_evt_paramE "bk_hidh_cb_param_t::hidh_uninit_evt_param") deinit
    :   HIDH callback param of BK_HIDH_DEINIT_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_open_evt_param](#_CPPv4N18bk_hidh_cb_param_t19hidh_open_evt_paramE "bk_hidh_cb_param_t::hidh_open_evt_param") open
    :   HIDH callback param of BK_HIDH_OPEN_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_close_evt_param](#_CPPv4N18bk_hidh_cb_param_t20hidh_close_evt_paramE "bk_hidh_cb_param_t::hidh_close_evt_param") close
    :   HIDH callback param of BK_HIDH_CLOSE_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_unplug_evt_param](#_CPPv4N18bk_hidh_cb_param_t21hidh_unplug_evt_paramE "bk_hidh_cb_param_t::hidh_unplug_evt_param") unplug
    :   HIDH callback param of BK_HIDH_VC_UNPLUG_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_get_proto_evt_param](#_CPPv4N18bk_hidh_cb_param_t24hidh_get_proto_evt_paramE "bk_hidh_cb_param_t::hidh_get_proto_evt_param") get_proto
    :   HIDH callback param of BK_HIDH_GET_PROTO_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_set_proto_evt_param](#_CPPv4N18bk_hidh_cb_param_t24hidh_set_proto_evt_paramE "bk_hidh_cb_param_t::hidh_set_proto_evt_param") set_proto
    :   HIDH callback param of BK_HIDH_SET_PROTO_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_get_rpt_evt_param](#_CPPv4N18bk_hidh_cb_param_t22hidh_get_rpt_evt_paramE "bk_hidh_cb_param_t::hidh_get_rpt_evt_param") get_rpt
    :   HIDH callback param of BK_HIDH_GET_RPT_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_set_rpt_evt_param](#_CPPv4N18bk_hidh_cb_param_t22hidh_set_rpt_evt_paramE "bk_hidh_cb_param_t::hidh_set_rpt_evt_param") set_rpt
    :   HIDH callback param of BK_HIDH_SET_RPT_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_send_data_evt_param](#_CPPv4N18bk_hidh_cb_param_t24hidh_send_data_evt_paramE "bk_hidh_cb_param_t::hidh_send_data_evt_param") send_data
    :   HIDH callback param of BK_HIDH_DATA_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_data_ind_evt_param](#_CPPv4N18bk_hidh_cb_param_t23hidh_data_ind_evt_paramE "bk_hidh_cb_param_t::hidh_data_ind_evt_param") data_ind
    :   HIDH callback param of BK_HIDH_DATA_IND_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_add_dev_evt_param](#_CPPv4N18bk_hidh_cb_param_t22hidh_add_dev_evt_paramE "bk_hidh_cb_param_t::hidh_add_dev_evt_param") add_dev
    :   HIDH callback param of BK_HIDH_ADD_DEV_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_rmv_dev_evt_param](#_CPPv4N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_paramE "bk_hidh_cb_param_t::hidh_rmv_dev_evt_param") rmv_dev
    :   HIDH callback param of BK_HIDH_RMV_DEV_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_get_dscp_evt_param](#_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_paramE "bk_hidh_cb_param_t::hidh_get_dscp_evt_param") sdp_dscp
    :   HIDH callback param of BK_HIDH_GET_DSCP_EVT

    struct [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh_set_info_evt_param](#_CPPv4N18bk_hidh_cb_param_t23hidh_set_info_evt_paramE "bk_hidh_cb_param_t::hidh_set_info_evt_param") set_info
    :   HIDH callback param of BK_HIDH_SET_INFO_EVT

    struct hidh_add_dev_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_ADD_DEV_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t handle
        :   device handle

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
        :   device address

    struct hidh_close_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_CLOSE_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        [bk_hidh_connection_state_t](#_CPPv426bk_hidh_connection_state_t "bk_hidh_connection_state_t") conn_status
        :   connection status

        uint8_t handle
        :   device handle

    struct hidh_data_ind_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_DATA_IND_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t handle
        :   device handle

        [bk_hidh_protocol_mode_t](#_CPPv423bk_hidh_protocol_mode_t "bk_hidh_protocol_mode_t") proto_mode
        :   protocol mode

        uint16_t len
        :   data length

        uint8_t *data
        :   data pointer

        uint8_t report_type
        :   report type

    struct hidh_get_dscp_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_SDP_DSCP_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t sub_class
        :   HIDDeviceSubclass

        uint8_t reconn_init
        :   HIDReconnectInitiate

        uint8_t normal_conn
        :   HIDNormallyConnectable

        uint16_t ssr_max_latency
        :   SSR max latency in slots

        uint16_t ssr_min_tout
        :   SSR min timeout in slots

        uint8_t ctry_code
        :   Country Code

        uint16_t parse_version
        :   Parse Version

        uint8_t virtual_cable
        :   Virtual Cable

        uint8_t boot_device
        :   Boot device

        uint8_t remote_wake
        :   HIDRemoteWake

        uint8_t battery_power
        :   HIDBatteryPower

        uint16_t vendor_id
        :   Device Vendor ID

        uint16_t product_id
        :   Device Product ID

        uint16_t device_version
        :   Device Version

        uint16_t dl_len
        :   Device descriptor length

        uint8_t *dsc_list
        :   Device descriptor pointer

        uint8_t dsc_type
        :   Device ClassDescriptor type

    struct hidh_get_proto_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_GET_PROTO_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t handle
        :   device handle

        [bk_hidh_protocol_mode_t](#_CPPv423bk_hidh_protocol_mode_t "bk_hidh_protocol_mode_t") proto_mode
        :   protocol mode

    struct hidh_get_rpt_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_GET_RPT_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t handle
        :   device handle

        uint16_t len
        :   data length

        uint8_t *data
        :   data pointer

    struct hidh_init_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_INIT_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   status

    struct hidh_open_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_OPEN_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        [bk_hidh_connection_state_t](#_CPPv426bk_hidh_connection_state_t "bk_hidh_connection_state_t") conn_status
        :   connection status

        bool is_orig
        :   indicate if host intiate the connection

        uint8_t handle
        :   device handle

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
        :   device address

    struct hidh_rmv_dev_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_RMV_DEV_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t handle
        :   device handle

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
        :   device address

    struct hidh_send_data_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_DATA_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t handle
        :   device handle

        uint8_t reason
        :   lower layer failed reason

    struct hidh_set_info_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_SET_INFO_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t handle
        :   device handle

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
        :   device address

    struct hidh_set_proto_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_SET_PROTO_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t handle
        :   device handle

    struct hidh_set_rpt_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_SET_RPT_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        uint8_t handle
        :   device handle

    struct hidh_uninit_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_DEINIT_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   status

    struct hidh_unplug_evt_param
    :   *#include <bk_dm_hidh.h>*

        BK_HIDH_VC_UNPLUG_EVT.

        Public Members

        [bk_hidh_status_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        [bk_hidh_connection_state_t](#_CPPv426bk_hidh_connection_state_t "bk_hidh_connection_state_t") conn_status
        :   connection status

        uint8_t handle
        :   device handle


### Structures

struct bk_hidh_hid_info_t
:   HID device information from HID Device Service Record and Device ID Service Record.

    Public Members

    int attr_mask
    :   device attribute bit mask, refer to bk_hidh_dev_attr_t

    int dl_len
    :   SDP attrbutes of HID devices: HID device descriptor length

    uint8_t *dsc_list
    :   SDP attrbutes of HID devices: HID device descriptor definition


### Macros

BTHH_MAX_DSC_LEN
:   maximum size of HID Device report descriptor


### Type Definitions

typedef void (*bk_hh_cb_t)([bk_hidh_cb_event_t](#_CPPv418bk_hidh_cb_event_t "bk_hidh_cb_event_t") event, [bk_hidh_cb_param_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t") *param)
:   HID host callback function type.

    Param event
    :   Event type

    Param param
    :   Point to callback parameter, currently is union type


### Enumerations

enum bk_hidh_connection_state_t
:   HID host connection state.


    *Values:*

    enumerator BK_HIDH_CONN_STATE_CONNECTED
    :   connected state

    enumerator BK_HIDH_CONN_STATE_CONNECTING
    :   connecting state

    enumerator BK_HIDH_CONN_STATE_DISCONNECTED
    :   disconnected state

    enumerator BK_HIDH_CONN_STATE_DISCONNECTING
    :   disconnecting state

    enumerator BK_HIDH_CONN_STATE_UNKNOWN
    :   unknown state (initial state)

enum bk_hidh_status_t
:   HID handshake error code and vendor-defined result code.


    *Values:*

    enumerator BK_HIDH_OK
    :   successful

    enumerator BK_HIDH_HS_HID_NOT_READY
    :   handshake error: device not ready

    enumerator BK_HIDH_HS_INVALID_RPT_ID
    :   handshake error: invalid report ID

    enumerator BK_HIDH_HS_TRANS_NOT_SPT
    :   handshake error: HID device does not support the request

    enumerator BK_HIDH_HS_INVALID_PARAM
    :   handshake error: parameter value does not meet the expected criteria of called function or API

    enumerator BK_HIDH_HS_ERROR
    :   handshake error: HID device could not identify the error condition

    enumerator BK_HIDH_ERR
    :   general BK HID Host error

    enumerator BK_HIDH_ERR_SDP
    :   SDP error

    enumerator BK_HIDH_ERR_PROTO
    :   SET_PROTOCOL error, only used in BK_HIDH_OPEN_EVT callback

    enumerator BK_HIDH_ERR_DB_FULL
    :   device database full, used in BK_HIDH_OPEN_EVT/BK_HIDH_ADD_DEV_EVT

    enumerator BK_HIDH_ERR_TOD_UNSPT
    :   type of device not supported

    enumerator BK_HIDH_ERR_NO_RES
    :   out of system resources

    enumerator BK_HIDH_ERR_AUTH_FAILED
    :   authentication fail

    enumerator BK_HIDH_ERR_HDL
    :   connection handle error

    enumerator BK_HIDH_ERR_SEC
    :   encryption error

    enumerator BK_HIDH_BUSY
    :   vendor-defined: temporarily can not handle this request

    enumerator BK_HIDH_NO_DATA
    :   vendor-defined: no data.

    enumerator BK_HIDH_NEED_INIT
    :   vendor-defined: HIDH module shall initialize first

    enumerator BK_HIDH_NEED_DEINIT
    :   vendor-defined: HIDH module shall de-deinitialize first

    enumerator BK_HIDH_NO_CONNECTION
    :   vendor-defined: connection may have been closed

    enumerator BK_HIDH_NO_ACL_LINK
    :   vendor-defined: Baseband acl link not exist

enum bk_hidh_protocol_mode_t
:   HID host protocol modes.


    *Values:*

    enumerator BK_HIDH_BOOT_MODE
    :   boot protocol mode

    enumerator BK_HIDH_REPORT_MODE
    :   report protocol mode

    enumerator BK_HIDH_UNSUPPORTED_MODE
    :   unsupported protocol mode

enum bk_hidh_report_type_t
:   HID host report types.


    *Values:*

    enumerator BK_HIDH_REPORT_TYPE_OTHER
    :   unsupported report type

    enumerator BK_HIDH_REPORT_TYPE_INPUT
    :   input report type

    enumerator BK_HIDH_REPORT_TYPE_OUTPUT
    :   output report type

    enumerator BK_HIDH_REPORT_TYPE_FEATURE
    :   feature report type

enum bk_hidh_cb_event_t
:   HID host callback function events.


    *Values:*

    enumerator BK_HIDH_INIT_EVT
    :   when HID host is initialized, the event comes

    enumerator BK_HIDH_DEINIT_EVT
    :   when HID host is deinitialized, the event comes

    enumerator BK_HIDH_OPEN_EVT
    :   when HID host connection opened, the event comes

    enumerator BK_HIDH_CLOSE_EVT
    :   when HID host connection closed, the event comes

    enumerator BK_HIDH_GET_RPT_EVT
    :   when Get_Report command is called, the event comes

    enumerator BK_HIDH_SET_RPT_EVT
    :   when Set_Report command is called, the event comes

    enumerator BK_HIDH_GET_PROTO_EVT
    :   when Get_Protocol command is called, the event comes

    enumerator BK_HIDH_SET_PROTO_EVT
    :   when Set_Protocol command is called, the event comes

    enumerator BK_HIDH_SDP_DSCP_EVT
    :   when HIDH is connected, the event comes

    enumerator BK_HIDH_ADD_DEV_EVT
    :   when a device is added, the event comes

    enumerator BK_HIDH_RMV_DEV_EVT
    :   when a device is removed, the event comes

    enumerator BK_HIDH_VC_UNPLUG_EVT
    :   when virtually unplugged, the event comes

    enumerator BK_HIDH_DATA_EVT
    :   when send data on interrupt channel, the event comes

    enumerator BK_HIDH_DATA_IND_EVT
    :   when receive data on interrupt channel, the event comes

    enumerator BK_HIDH_SET_INFO_EVT
    :   when set the HID device descriptor, the event comes

enum bk_hidh_dev_attr_t
:   HID device information from HID Device Service Record and Device ID Service Record.


    *Values:*

    enumerator BK_HIDH_DEV_ATTR_VIRTUAL_CABLE
    :   whether Virtual Cables is supported

    enumerator BK_HIDH_DEV_ATTR_RECONNECT_INITIATE
    :   whether the HID device inititates the reconnection process

    enumerator BK_HIDH_DEV_ATTR_BATTERY_DEVICE
    :   whether Battery-powered device

    enumerator BK_HIDH_DEV_ATTR_REMOTE_WAKE
    :   whether wake-up signal to host supported

    enumerator BK_HIDH_DEV_ATTR_NORMALLY_CONNECTABLE
    :   whether device is in Page Scan mode when there is no active connection

    enumerator BK_HIDH_DEV_ATTR_BOOT_DEVICE
    :   whether Boot Protocol mode supported

enum bk_hidh_dev_app_id_t
:   application ID(non-zero) for each type of device


    *Values:*

    enumerator BK_HIDH_APP_ID_MOUSE
    :   pointing device

    enumerator BK_HIDH_APP_ID_KEYBOARD
    :   keyboard

    enumerator BK_HIDH_APP_ID_REMOTE_CONTROL
    :   remote control

    enumerator BK_HIDH_APP_ID_JOYSTICK
    :   joystick

    enumerator BK_HIDH_APP_ID_GAMEPAD
    :   gamepad


## bk_dm_l2cap.h

`bk_dm_l2cap.h` 提供 BT L2CAP 通道和数据传输接口。


### Header File


- [bluetooth/bk_dm_l2cap.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_l2cap.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_l2cap.h")


### Functions

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_l2cap_register_callback([bk_bt_l2cap_cb_t](#_CPPv416bk_bt_l2cap_cb_t "bk_bt_l2cap_cb_t") callback)
:   This function is called to init callbacks with L2CAP module.

    参数
    :   **callback** – **[in]** pointer to the init callback function.

    返回
    :   - BT_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_l2cap_init(void)
:   This function is called to init L2CAP module. When the operation is completed, the callback function will be called with BK_BT_L2CAP_INIT_EVT. This function should be called after bk_bluedroid_enable() completes successfully.

    返回
    :   - BT_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_l2cap_deinit(void)
:   This function is called to uninit l2cap module. The operation will close all active L2CAP connection first, then the callback function will be called with BK_BT_L2CAP_CLOSE_EVT, and the number of BK_BT_L2CAP_CLOSE_EVT is equal to the number of connection. When the operation is completed, the callback function will be called with BK_BT_L2CAP_UNINIT_EVT. This function should be called after bk_bt_l2cap_init() completes successfully.

    返回
    :   - BT_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_l2cap_connect([bk_bt_l2cap_cntl_flags_t](#_CPPv424bk_bt_l2cap_cntl_flags_t "bk_bt_l2cap_cntl_flags_t") cntl_flag, uint16_t remote_psm, [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") peer_bd_addr)
:   This function makes an L2CAP connection to a remote BD Address. When the connection is initiated or failed to initiate, the callback is called with BK_BT_L2CAP_CL_INIT_EVT. When the connection is established or failed, the callback is called with BK_BT_L2CAP_OPEN_EVT. This function must be called after bk_bt_l2cap_init() successful and before bk_bt_l2cap_deinit().

    参数
    :   - **cntl_flag** – **[in]** Lower 16-bit security settings mask.

        - **remote_psm** – **[in]** Remote device bluetooth Profile PSM.

        - **peer_bd_addr** – **[in]** Remote device bluetooth device address.

    返回
    :   - BT_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_l2cap_start_srv([bk_bt_l2cap_cntl_flags_t](#_CPPv424bk_bt_l2cap_cntl_flags_t "bk_bt_l2cap_cntl_flags_t") cntl_flag, uint16_t local_psm)
:   This function create a L2CAP server and starts listening for an L2CAP connection request from a remote Bluetooth device. When the server is started successfully, the callback is called with BK_BT_L2CAP_START_EVT. When the connection is established, the callback is called with BK_BT_L2CAP_OPEN_EVT. This function must be called after bk_bt_l2cap_init() successful and before bk_bt_l2cap_deinit().

    参数
    :   - **cntl_flag** – **[in]** Lower 16-bit security settings mask.

        - **local_psm** – **[in]** Dynamic PSM.

    返回
    :   - BT_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_l2cap_stop_all_srv(void)
:   This function stops all L2CAP servers. The operation will close all active L2CAP connection first, then the callback function will be called with BK_BT_L2CAP_CLOSE_EVT, and the number of BK_BT_L2CAP_CLOSE_EVT is equal to the number of connection. When the operation is completed, the callback is called with BK_BT_L2CAP_SRV_STOP_EVT. This function must be called after bk_bt_l2cap_init() successful and before bk_bt_l2cap_deinit().

    返回
    :   - BT_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_bt_l2cap_stop_srv(uint16_t local_psm)
:   This function stops a specific L2CAP server. The operation will close all active L2CAP connection first on the specific L2CAP server, then the callback function will be called with BK_BT_L2CAP_CLOSE_EVT, and the number of BK_BT_L2CAP_CLOSE_EVT is equal to the number of connection. When the operation is completed, the callback is called with BK_BT_L2CAP_SRV_STOP_EVT. This function must be called after bk_bt_l2cap_init() successful and before bk_bt_l2cap_deinit().

    参数
    :   **local_psm** – **[in]** Dynamic PSM.

    返回
    :   - BT_OK: success

        - other: failed

int bk_bt_l2cap_read(int fd, void *data, uint16_t size)

int bk_bt_l2cap_write(int fd, const void *data, uint16_t size)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_l2cap_close(int fd)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_bt_l2cap_set_data_callback([bk_bt_l2cap_data_cb_t](#_CPPv421bk_bt_l2cap_data_cb_t "bk_bt_l2cap_data_cb_t") callback)


### Unions

union bk_bt_l2cap_cb_param_t
:   *#include <bk_dm_l2cap.h>*

    L2CAP callback parameters union.

    Public Members

    struct [bk_bt_l2cap_cb_param_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap_init_evt_param](#_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_init_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_init_evt_param") init
    :   L2CAP callback param of BK_BT_L2CAP_INIT_EVT

    struct [bk_bt_l2cap_cb_param_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap_uninit_evt_param](#_CPPv4N22bk_bt_l2cap_cb_param_t22l2cap_uninit_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_uninit_evt_param") uninit
    :   L2CAP callback param of BK_BT_L2CAP_UNINIT_EVT

    struct [bk_bt_l2cap_cb_param_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap_open_evt_param](#_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_open_evt_param") open
    :   L2CAP callback param of BK_BT_L2CAP_OPEN_EVT

    struct [bk_bt_l2cap_cb_param_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap_close_evt_param](#_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_close_evt_param") close
    :   L2CAP callback param of BK_BT_L2CAP_CLOSE_EVT

    struct [bk_bt_l2cap_cb_param_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap_start_evt_param](#_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_start_evt_param") start
    :   L2CAP callback param of BK_BT_L2CAP_START_EVT

    struct [bk_bt_l2cap_cb_param_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap_cl_init_evt_param](#_CPPv4N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_cl_init_evt_param") cl_init
    :   L2CAP callback param of BK_BT_L2CAP_CL_INIT_EVT

    struct [bk_bt_l2cap_cb_param_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap_srv_stop_evt_param](#_CPPv4N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_srv_stop_evt_param") srv_stop
    :   L2CAP callback param of BK_BT_L2CAP_SRV_STOP_EVT

    struct l2cap_cl_init_evt_param
    :   *#include <bk_dm_l2cap.h>*

        BK_BT_L2CAP_CL_INIT_EVT.

        Public Members

        [bk_bt_l2cap_status_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

        uint8_t sec_id
        :   security ID used by this server

    struct l2cap_close_evt_param
    :   *#include <bk_dm_l2cap.h>*

        BK_BT_L2CAP_CLOSE_EVT.

        Public Members

        [bk_bt_l2cap_status_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

        bool async
        :   FALSE, if local initiates disconnect

        int fd
        :   File descriptor, lcid

    struct l2cap_init_evt_param
    :   *#include <bk_dm_l2cap.h>*

        BK_BT_L2CAP_INIT_EVT.

        Public Members

        [bk_bt_l2cap_status_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

    struct l2cap_open_evt_param
    :   *#include <bk_dm_l2cap.h>*

        BK_BT_L2CAP_OPEN_EVT.

        Public Members

        [bk_bt_l2cap_status_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

        int fd
        :   File descriptor, lcid

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rem_bda
        :   The peer address

        int32_t tx_mtu
        :   The transmit MTU

    struct l2cap_srv_stop_evt_param
    :   *#include <bk_dm_l2cap.h>*

        BK_BT_L2CAP_SRV_STOP_EVT.

        Public Members

        [bk_bt_l2cap_status_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        uint16_t psm
        :   local psm

    struct l2cap_start_evt_param
    :   *#include <bk_dm_l2cap.h>*

        BK_BT_L2CAP_START_EVT.

        Public Members

        [bk_bt_l2cap_status_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

        uint8_t sec_id
        :   security ID used by this server

    struct l2cap_uninit_evt_param
    :   *#include <bk_dm_l2cap.h>*

        BK_BT_L2CAP_UNINIT_EVT.

        Public Members

        [bk_bt_l2cap_status_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status


### Macros

BK_BT_L2CAP_SEC_NONE
:   Security Setting Mask. Use these three mask mode:

    1. BK_BT_L2CAP_SEC_NONE
    2. BK_BT_L2CAP_SEC_AUTHENTICATE
    3. (BK_BT_L2CAP_SEC_ENCRYPT|BK_BT_L2CAP_SEC_AUTHENTICATE) No security

BK_BT_L2CAP_SEC_AUTHORIZE
:   Authorization required

BK_BT_L2CAP_SEC_AUTHENTICATE
:   Authentication required

BK_BT_L2CAP_SEC_ENCRYPT
:   Encryption required


### Type Definitions

typedef uint32_t bk_bt_l2cap_cntl_flags_t

typedef void (*bk_bt_l2cap_cb_t)([bk_bt_l2cap_cb_event_t](#_CPPv422bk_bt_l2cap_cb_event_t "bk_bt_l2cap_cb_event_t") event, [bk_bt_l2cap_cb_param_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t") *param)
:   L2CAP callback function type.

    Param event
    :   Event type

    Param param
    :   Point to callback parameter, currently is union type

typedef void (*bk_bt_l2cap_data_cb_t)(int fd, void *data, uint16_t size)
:   L2CAP callback function type.

    Param fd
    :   File descriptor.

    Param data
    :   pointer to data.

    Param len
    :   data length


### Enumerations

enum bk_bt_l2cap_status_t
:   L2CAP operation success and failure codes.


    *Values:*

    enumerator BK_BT_L2CAP_SUCCESS
    :   Successful operation.

    enumerator BK_BT_L2CAP_FAILURE
    :   Generic failure.

    enumerator BK_BT_L2CAP_BUSY
    :   Temporarily can not handle this request.

    enumerator BK_BT_L2CAP_NO_RESOURCE
    :   No more resource

    enumerator BK_BT_L2CAP_NEED_INIT
    :   L2CAP module shall init first

    enumerator BK_BT_L2CAP_NEED_DEINIT
    :   L2CAP module shall deinit first

    enumerator BK_BT_L2CAP_NO_CONNECTION
    :   Connection may have been closed

    enumerator BK_BT_L2CAP_NO_SERVER
    :   No server

enum bk_bt_l2cap_cb_event_t
:   L2CAP callback function events.


    *Values:*

    enumerator BK_BT_L2CAP_INIT_EVT
    :   When L2CAP is initialized, the event comes

    enumerator BK_BT_L2CAP_UNINIT_EVT
    :   When L2CAP is deinitialized, the event comes

    enumerator BK_BT_L2CAP_OPEN_EVT
    :   When L2CAP Client connection open, the event comes

    enumerator BK_BT_L2CAP_CLOSE_EVT
    :   When L2CAP connection closed, the event comes

    enumerator BK_BT_L2CAP_START_EVT
    :   When L2CAP server started, the event comes

    enumerator BK_BT_L2CAP_CL_INIT_EVT
    :   When L2CAP client initiated a connection, the event comes

    enumerator BK_BT_L2CAP_SRV_STOP_EVT
    :   When L2CAP server stopped, the event comes


## bk_dm_spp.h

`bk_dm_spp.h` 提供 Serial Port Profile 连接和数据传输接口。


### Header File


- [bluetooth/bk_dm_spp.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_spp.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_spp.h")


### Functions

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_register_callback([bk_spp_cb_t](#_CPPv411bk_spp_cb_t "bk_spp_cb_t") callback)
:   This function is called to init callbacks with SPP module.

    参数
    :   **callback** – **[in]** pointer to the init callback function.

    返回
    :   - BK_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_init()
:   This function is called to init SPP module. When the operation is completed, the callback function will be called with BK_SPP_INIT_EVT. This function should be called after bk_bluedroid_enable() completes successfully.

    返回
    :   - BK_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_deinit(void)
:   This function is called to uninit SPP module. The operation will close all active SPP connection first, then the callback function will be called with BK_SPP_CLOSE_EVT, and the number of BK_SPP_CLOSE_EVT is equal to the number of connection. When the operation is completed, the callback function will be called with BK_SPP_UNINIT_EVT. This function should be called after bk_spp_init()/bk_spp_enhanced_init() completes successfully.

    返回
    :   - BK_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_start_discovery([bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   This function is called to performs service discovery for the services provided by the given peer device. When the operation is completed, the callback function will be called with BK_SPP_DISCOVERY_COMP_EVT. This function must be called after bk_spp_init()/bk_spp_enhanced_init() successful and before bk_spp_deinit().

    参数
    :   **bd_addr** – **[in]** Remote device bluetooth device address.

    返回
    :   - BK_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_connect([bk_spp_role_t](#_CPPv413bk_spp_role_t "bk_spp_role_t") role, uint8_t remote_scn, uint8_t *peer_bd_addr)
:   This function makes an SPP connection to a remote BD Address. When the connection is initiated or failed to initiate, the callback is called with BK_SPP_CL_INIT_EVT. When the connection is established or failed, the callback is called with BK_SPP_OPEN_EVT. This function must be called after bk_spp_init()/bk_spp_enhanced_init() successful and before bk_spp_deinit().

    参数
    :   - **role** – **[in]** Master or slave.

        - **remote_scn** – **[in]** Remote device bluetooth device SCN.

        - **peer_bd_addr** – **[in]** Remote device bluetooth device address.

    返回
    :   - BK_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_disconnect(uint32_t handle)
:   This function closes an SPP connection. When the operation is completed, the callback function will be called with BK_SPP_CLOSE_EVT. This function must be called after bk_spp_init()/bk_spp_enhanced_init() successful and before bk_spp_deinit().

    参数
    :   **handle** – **[in]** The connection handle.

    返回
    :   - BK_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_start_srv([bk_spp_role_t](#_CPPv413bk_spp_role_t "bk_spp_role_t") role, uint8_t local_scn, const char *name)
:   This function create a SPP server and starts listening for an SPP connection request from a remote Bluetooth device. When the server is started successfully, the callback is called with BK_SPP_START_EVT. When the connection is established, the callback is called with BK_SPP_SRV_OPEN_EVT. This function must be called after bk_spp_init()/bk_spp_enhanced_init() successful and before bk_spp_deinit().

    参数
    :   - **role** – **[in]** Master or slave.

        - **local_scn** – **[in]** The specific channel you want to get. If channel is 0, means get any channel.

        - **name** – **[in]** Server’s name.

    返回
    :   - BK_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_stop_srv(void)
:   This function stops all SPP servers. The operation will close all active SPP connection first, then the callback function will be called with BK_SPP_CLOSE_EVT, and the number of BK_SPP_CLOSE_EVT is equal to the number of connection. When the operation is completed, the callback is called with BK_SPP_SRV_STOP_EVT. This function must be called after bk_spp_init()/bk_spp_enhanced_init() successful and before bk_spp_deinit().

    返回
    :   - BK_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_stop_srv_scn(uint8_t scn)
:   This function stops a specific SPP server. The operation will close all active SPP connection first on the specific SPP server, then the callback function will be called with BK_SPP_CLOSE_EVT, and the number of BK_SPP_CLOSE_EVT is equal to the number of connection. When the operation is completed, the callback is called with BK_SPP_SRV_STOP_EVT. This function must be called after bk_spp_init()/bk_spp_enhanced_init() successful and before bk_spp_deinit().

    参数
    :   **scn** – **[in]** Server channel number.

    返回
    :   - BK_OK: success

        - other: failed

[bt_err_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk_spp_write(uint32_t handle, int len, uint8_t *p_data)
:   This function is used to write data, only for BK_SPP_MODE_CB. When this function need to be called repeatedly, it is strongly recommended to call this function again after the previous event BK_SPP_WRITE_EVT is received and the parameter ‘cong’ is equal to false. If the previous event BK_SPP_WRITE_EVT with parameter ‘cong’ is equal to true, the function can only be called again when the event BK_SPP_CONG_EVT with parameter ‘cong’ equal to false is received. This function must be called after an connection between initiator and acceptor has been established.

    参数
    :   - **handle** – **[in]** The connection handle.

        - **len** – **[in]** The length of the data written.

        - **p_data** – **[in]** The data written.

    返回
    :   - BK_OK: success

        - other: failed


### Unions

union bk_spp_cb_param_t
:   *#include <bk_dm_spp.h>*

    SPP callback parameters union.

    Public Members

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_init_evt_param](#_CPPv4N17bk_spp_cb_param_t18spp_init_evt_paramE "bk_spp_cb_param_t::spp_init_evt_param") init
    :   SPP callback param of SPP_INIT_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_uninit_evt_param](#_CPPv4N17bk_spp_cb_param_t20spp_uninit_evt_paramE "bk_spp_cb_param_t::spp_uninit_evt_param") uninit
    :   SPP callback param of SPP_UNINIT_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_discovery_comp_evt_param](#_CPPv4N17bk_spp_cb_param_t28spp_discovery_comp_evt_paramE "bk_spp_cb_param_t::spp_discovery_comp_evt_param") disc_comp
    :   SPP callback param of SPP_DISCOVERY_COMP_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_open_evt_param](#_CPPv4N17bk_spp_cb_param_t18spp_open_evt_paramE "bk_spp_cb_param_t::spp_open_evt_param") open
    :   SPP callback param of BK_SPP_OPEN_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_srv_open_evt_param](#_CPPv4N17bk_spp_cb_param_t22spp_srv_open_evt_paramE "bk_spp_cb_param_t::spp_srv_open_evt_param") srv_open
    :   SPP callback param of BK_SPP_SRV_OPEN_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_close_evt_param](#_CPPv4N17bk_spp_cb_param_t19spp_close_evt_paramE "bk_spp_cb_param_t::spp_close_evt_param") close
    :   SPP callback param of BK_SPP_CLOSE_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_start_evt_param](#_CPPv4N17bk_spp_cb_param_t19spp_start_evt_paramE "bk_spp_cb_param_t::spp_start_evt_param") start
    :   SPP callback param of BK_SPP_START_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_srv_stop_evt_param](#_CPPv4N17bk_spp_cb_param_t22spp_srv_stop_evt_paramE "bk_spp_cb_param_t::spp_srv_stop_evt_param") srv_stop
    :   SPP callback param of BK_SPP_SRV_STOP_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_cl_init_evt_param](#_CPPv4N17bk_spp_cb_param_t21spp_cl_init_evt_paramE "bk_spp_cb_param_t::spp_cl_init_evt_param") cl_init
    :   SPP callback param of BK_SPP_CL_INIT_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_write_evt_param](#_CPPv4N17bk_spp_cb_param_t19spp_write_evt_paramE "bk_spp_cb_param_t::spp_write_evt_param") write
    :   SPP callback param of BK_SPP_WRITE_EVT

    struct [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp_data_ind_evt_param](#_CPPv4N17bk_spp_cb_param_t22spp_data_ind_evt_paramE "bk_spp_cb_param_t::spp_data_ind_evt_param") data_ind
    :   SPP callback param of BK_SPP_DATA_IND_EVT

    struct spp_cl_init_evt_param
    :   *#include <bk_dm_spp.h>*

        BK_SPP_CL_INIT_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

    struct spp_close_evt_param
    :   *#include <bk_dm_spp.h>*

        BK_SPP_CLOSE_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

    struct spp_data_ind_evt_param
    :   *#include <bk_dm_spp.h>*

        BK_SPP_DATA_IND_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

        uint16_t len
        :   The length of data

        uint8_t *data
        :   The data received

    struct spp_discovery_comp_evt_param
    :   *#include <bk_dm_spp.h>*

        SPP_DISCOVERY_COMP_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        uint8_t scn_num
        :   The num of scn_num

        uint8_t scn[BK_SPP_MAX_SCN]
        :   channel #

        const char *service_name[BK_SPP_MAX_SCN]
        :   service_name

    struct spp_init_evt_param
    :   *#include <bk_dm_spp.h>*

        SPP_INIT_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

    struct spp_open_evt_param
    :   *#include <bk_dm_spp.h>*

        BK_SPP_OPEN_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rem_bda
        :   The peer address

    struct spp_srv_open_evt_param
    :   *#include <bk_dm_spp.h>*

        BK_SPP_SRV_OPEN_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rem_bda
        :   The peer address

    struct spp_srv_stop_evt_param
    :   *#include <bk_dm_spp.h>*

        BK_SPP_SRV_STOP_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        uint8_t scn
        :   Server channel number

    struct spp_start_evt_param
    :   *#include <bk_dm_spp.h>*

        BK_SPP_START_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

        uint8_t scn
        :   Server channel number

    struct spp_uninit_evt_param
    :   *#include <bk_dm_spp.h>*

        SPP_UNINIT_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

    struct spp_write_evt_param
    :   *#include <bk_dm_spp.h>*

        BK_SPP_WRITE_EVT.

        Public Members

        [bk_spp_status_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        uint32_t handle
        :   The connection handle

        uint16_t len
        :   The length of the data written.


### Macros

BK_SPP_MAX_SCN
:   SPP max SCN

BK_SPP_MIN_TX_BUFFER_SIZE
:   SPP min tx buffer

BK_SPP_MAX_TX_BUFFER_SIZE
:   SPP max tx buffer size


### Type Definitions

typedef void (*bk_spp_cb_t)([bk_spp_cb_event_t](#_CPPv417bk_spp_cb_event_t "bk_spp_cb_event_t") event, [bk_spp_cb_param_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t") *param)
:   SPP callback function type. When handle BK_SPP_DATA_IND_EVT, it is strongly recommended to cache incoming data, and process them in other lower priority application task rather than in this callback directly.

    Param event
    :   Event type

    Param param
    :   Point to callback parameter, currently is union type


### Enumerations

enum bk_spp_status_t
:   *Values:*

    enumerator BK_SPP_SUCCESS
    :   Successful operation.

    enumerator BK_SPP_FAILURE
    :   Generic failure.

    enumerator BK_SPP_BUSY
    :   Temporarily can not handle this request.

    enumerator BK_SPP_NO_DATA
    :   No data

    enumerator BK_SPP_NO_RESOURCE
    :   No more resource

    enumerator BK_SPP_NEED_INIT
    :   SPP module shall init first

    enumerator BK_SPP_NEED_DEINIT
    :   SPP module shall deinit first

    enumerator BK_SPP_NO_CONNECTION
    :   Connection may have been closed

    enumerator BK_SPP_NO_SERVER
    :   No SPP server

enum bk_spp_role_t
:   *Values:*

    enumerator BK_SPP_ROLE_MASTER
    :   Role: master

    enumerator BK_SPP_ROLE_SLAVE
    :   Role: slave

enum bk_spp_cb_event_t
:   SPP callback function events.


    *Values:*

    enumerator BK_SPP_INIT_EVT
    :   When SPP is initialized, the event comes

    enumerator BK_SPP_UNINIT_EVT
    :   When SPP is deinitialized, the event comes

    enumerator BK_SPP_DISCOVERY_COMP_EVT
    :   When SDP discovery complete, the event comes

    enumerator BK_SPP_OPEN_EVT
    :   When SPP Client connection open, the event comes

    enumerator BK_SPP_CLOSE_EVT
    :   When SPP connection closed, the event comes

    enumerator BK_SPP_START_EVT
    :   When SPP server started, the event comes

    enumerator BK_SPP_CL_INIT_EVT
    :   When SPP client initiated a connection, the event comes

    enumerator BK_SPP_DATA_IND_EVT
    :   When SPP connection received data, the event comes, only for BK_SPP_MODE_CB

    enumerator BK_SPP_WRITE_EVT
    :   When SPP write operation completes, the event comes, only for BK_SPP_MODE_CB

    enumerator BK_SPP_SRV_OPEN_EVT
    :   When SPP Server connection open, the event comes

    enumerator BK_SPP_SRV_STOP_EVT
    :   When SPP server stopped, the event comes


## API 类型定义


## bk_dm_a2dp_types.h

`bk_dm_a2dp_types.h` 定义 A2DP profile 使用的事件、状态和音频类型。


### Header File


- [bluetooth/bk_dm_a2dp_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_a2dp_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_a2dp_types.h")


### Unions

union bk_a2dp_cb_param_t
:   *#include <bk_dm_a2dp_types.h>*

    A2DP state callback parameters.

    Public Members

    struct [bk_a2dp_cb_param_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp_conn_state_param](#_CPPv4N18bk_a2dp_cb_param_t21a2dp_conn_state_paramE "bk_a2dp_cb_param_t::a2dp_conn_state_param") conn_state
    :   A2DP connection status

    struct [bk_a2dp_cb_param_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp_audio_state_param](#_CPPv4N18bk_a2dp_cb_param_t22a2dp_audio_state_paramE "bk_a2dp_cb_param_t::a2dp_audio_state_param") audio_state
    :   audio stream playing state

    struct [bk_a2dp_cb_param_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp_audio_cfg_param](#_CPPv4N18bk_a2dp_cb_param_t20a2dp_audio_cfg_paramE "bk_a2dp_cb_param_t::a2dp_audio_cfg_param") audio_cfg
    :   media codec configuration information

    struct [bk_a2dp_cb_param_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp_audio_source_cfg_param](#_CPPv4N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_paramE "bk_a2dp_cb_param_t::a2dp_audio_source_cfg_param") audio_source_cfg
    :   media codec configuration information

    struct [bk_a2dp_cb_param_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[media_ctrl_stat_param](#_CPPv4N18bk_a2dp_cb_param_t21media_ctrl_stat_paramE "bk_a2dp_cb_param_t::media_ctrl_stat_param") media_ctrl_stat
    :   status in acknowledgement to media control commands

    struct [bk_a2dp_cb_param_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp_prof_stat_param](#_CPPv4N18bk_a2dp_cb_param_t20a2dp_prof_stat_paramE "bk_a2dp_cb_param_t::a2dp_prof_stat_param") a2dp_prof_stat
    :   status to indicate a2dp prof init or deinit

    struct [bk_a2dp_cb_param_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp_set_stat_param](#_CPPv4N18bk_a2dp_cb_param_t19a2dp_set_stat_paramE "bk_a2dp_cb_param_t::a2dp_set_stat_param") a2dp_set_delay_value_stat
    :   A2DP sink set delay report value status

    struct [bk_a2dp_cb_param_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp_get_stat_param](#_CPPv4N18bk_a2dp_cb_param_t19a2dp_get_stat_paramE "bk_a2dp_cb_param_t::a2dp_get_stat_param") a2dp_get_delay_value_stat
    :   A2DP sink get delay report value status

    struct a2dp_audio_cfg_param
    :   *#include <bk_dm_a2dp_types.h>*

        BK_A2DP_AUDIO_CFG_EVT.

        Public Members

        uint8_t remote_bda[6]
        :   remote bluetooth device address

        [bk_a2dp_mcc_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t") mcc
        :   A2DP media codec capability information

    struct a2dp_audio_source_cfg_param
    :   *#include <bk_dm_a2dp_types.h>*

        BK_A2DP_AUDIO_SOURCE_CFG_EVT.

        Public Members

        uint8_t remote_bda[6]
        :   remote bluetooth device address

        uint16_t mtu

        [bk_a2dp_mcc_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t") mcc
        :   max payload len, only used in source A2DP media codec capability information

    struct a2dp_audio_state_param
    :   *#include <bk_dm_a2dp_types.h>*

        BK_A2DP_AUDIO_STATE_EVT.

        Public Members

        [bk_a2dp_audio_state_t](#_CPPv421bk_a2dp_audio_state_t "bk_a2dp_audio_state_t") state
        :   one of the values from bk_a2dp_audio_state_t

        uint8_t remote_bda[6]
        :   remote bluetooth device address

    struct a2dp_conn_state_param
    :   *#include <bk_dm_a2dp_types.h>*

        BK_A2DP_CONNECTION_STATE_EVT.

        Public Members

        [bk_a2dp_connection_state_t](#_CPPv426bk_a2dp_connection_state_t "bk_a2dp_connection_state_t") state
        :   one of values from bk_a2dp_connection_state_t

        uint8_t remote_bda[6]
        :   remote bluetooth device address

        [bk_a2dp_disc_rsn_t](#_CPPv418bk_a2dp_disc_rsn_t "bk_a2dp_disc_rsn_t") disc_rsn
        :   reason of disconnection for “DISCONNECTED”

    struct a2dp_get_stat_param
    :   *#include <bk_dm_a2dp_types.h>*

        BK_A2DP_SNK_GET_DELAY_VALUE_EVT.

        Public Members

        uint16_t delay_value
        :   delay report value

    struct a2dp_prof_stat_param
    :   *#include <bk_dm_a2dp_types.h>*

        BK_A2DP_PROF_STATE_EVT.

        Public Members

        uint8_t action

        uint8_t role
        :   0 means init, 1 means deinit

        uint8_t status
        :   0 means source, 1 means sink

        uint8_t reason
        :   0 means success, other means fail

    struct a2dp_set_stat_param
    :   *#include <bk_dm_a2dp_types.h>*

        BK_A2DP_SNK_SET_DELAY_VALUE_EVT.

        Public Members

        [bk_a2dp_set_delay_value_state_t](#_CPPv431bk_a2dp_set_delay_value_state_t "bk_a2dp_set_delay_value_state_t") set_state
        :   a2dp profile state param

        uint16_t delay_value
        :   delay report value

    struct media_ctrl_stat_param
    :   *#include <bk_dm_a2dp_types.h>*

        BK_A2DP_MEDIA_CTRL_ACK_EVT.

        Public Members

        [bk_a2dp_media_ctrl_t](#_CPPv420bk_a2dp_media_ctrl_t "bk_a2dp_media_ctrl_t") cmd
        :   media control commands to acknowledge

        [bk_a2dp_media_ctrl_ack_t](#_CPPv424bk_a2dp_media_ctrl_ack_t "bk_a2dp_media_ctrl_ack_t") status
        :   acknowledgement to media control commands


### Structures

struct bk_a2dp_mcc_t
:   A2DP media codec capabilities union.

    Public Members

    uint8_t type
    :   A2DP media codec type

    struct [bk_a2dp_mcc_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t")::[anonymous]::[anonymous] sbc_codec
    :   SBC codec capabilities.

    struct [bk_a2dp_mcc_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t")::[anonymous]::[anonymous] aac_codec
    :   MPEG-2, 4 AAC codec capabilities.

    union [bk_a2dp_mcc_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t")::[anonymous] cie
    :   A2DP codec information element


### Type Definitions

typedef void (*bk_bt_a2dp_cb_t)([bk_a2dp_cb_event_t](#_CPPv418bk_a2dp_cb_event_t "bk_a2dp_cb_event_t") event, [bk_a2dp_cb_param_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t") *param)
:   A2DP profile callback function type.

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter

typedef void (*bk_bt_sink_data_cb_t)(const uint8_t *buf, uint16_t len)
:   A2DP sink data callback function.

    Param buf
    :   **[in]** : pointer to the data received from A2DP source device

    Param len
    :   **[in]** : size(in bytes) in buf

typedef int32_t (*bk_a2dp_source_data_cb_t)(uint8_t *buf, int32_t len)
:   A2DP source data read callback function.

    Param buf
    :   **[in]** : buffer to be filled with PCM data stream from higher layer

    Param len
    :   **[in]** : size(in bytes) of data block to be copied to buf. -1 is an indication to user that data buffer shall be flushed

    Return
    :   size of bytes read successfully, if the argument len is -1, this value is ignored.

typedef int32_t (*bk_a2dp_source_pcm_resample_cb_t)(uint8_t *in_addr, uint32_t *in_len, uint8_t *out_addr, uint32_t *out_len)
:   pcm resample callback function

    Param in_addr
    :   **[in]** : input buff before resample (in bytes).

    Param [in|out]
    :   in_len : input buff len (in bytes). When call done, it should change to how many bytes had processed.

    Param out_addr
    :   **[in]** : input buff after resample (in bytes).

    Param [in|out]
    :   out_len : out buff len (in bytes). When call done, it should change to how many bytes had outputed.

    Return
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail, bluetooth will ignore the data.

typedef int32_t (*bk_a2dp_source_pcm_encode_cb_t)(uint8_t type, uint8_t *in_addr, uint32_t *in_len, uint8_t *out_addr, uint32_t *out_len)
:   pcm encode callback function

    Param type
    :   **[in]** : encode type, 0 means sbc.

    Param in_addr
    :   **[in]** : input buff before encode (in bytes).

    Param [in|out]
    :   in_len : input buff len (in bytes). When call done, it should change to how many bytes had processed.

    Param out_addr
    :   **[in]** : input buff after encode (in bytes).

    Param [in|out]
    :   out_len : out buff len (in bytes). When call done, it should change to how many bytes had outputed.

    Return
    :   - BK_ERR_BT_SUCCESS: success

        - others: fail, bluetooth will ignore the data.


### Enumerations

enum bk_a2dp_cb_event_t
:   A2DP callback events.


    *Values:*

    enumerator BK_A2DP_CONNECTION_STATE_EVT
    :   connection state changed event

    enumerator BK_A2DP_AUDIO_STATE_EVT
    :   audio stream transmission state changed event

    enumerator BK_A2DP_AUDIO_CFG_EVT
    :   audio codec is configured, only used for A2DP SINK

    enumerator BK_A2DP_AUDIO_SOURCE_CFG_EVT
    :   audio codec is configured, only used for A2DP SOURCE

    enumerator BK_A2DP_MEDIA_CTRL_ACK_EVT
    :   acknowledge event in response to media control commands

    enumerator BK_A2DP_PROF_STATE_EVT
    :   indicate a2dp init&deinit complete

    enumerator BK_A2DP_SNK_SET_DELAY_VALUE_EVT
    :   indicate a2dp sink set delay report value complete, only used for A2DP SINK

    enumerator BK_A2DP_SNK_GET_DELAY_VALUE_EVT
    :   indicate a2dp sink get delay report value complete, only used for A2DP SINK

enum bk_a2dp_connection_state_t
:   Bluetooth A2DP connection states.


    *Values:*

    enumerator BK_A2DP_CONNECTION_STATE_DISCONNECTED
    :   connection released

    enumerator BK_A2DP_CONNECTION_STATE_CONNECTING
    :   connecting remote device

    enumerator BK_A2DP_CONNECTION_STATE_CONNECTED
    :   connection established

    enumerator BK_A2DP_CONNECTION_STATE_DISCONNECTING
    :   disconnecting remote device

enum bk_a2dp_disc_rsn_t
:   Bluetooth A2DP disconnection reason.


    *Values:*

    enumerator BK_A2DP_DISC_RSN_NORMAL
    :   Finished disconnection that is initiated by local or remote device

    enumerator BK_A2DP_DISC_RSN_ABNORMAL
    :   Abnormal disconnection caused by signal loss

enum bk_a2dp_audio_state_t
:   Bluetooth A2DP datapath states.


    *Values:*

    enumerator BK_A2DP_AUDIO_STATE_SUSPEND
    :   audio stream datapath suspend

    enumerator BK_A2DP_AUDIO_STATE_STARTED
    :   audio stream datapath started

enum bk_a2dp_media_ctrl_t
:   A2DP media control commands.


    *Values:*

    enumerator BK_A2DP_MEDIA_CTRL_START
    :   command to set up media transmission channel

    enumerator BK_A2DP_MEDIA_CTRL_SUSPEND
    :   command to suspend media transmission

enum bk_a2dp_media_ctrl_ack_t
:   A2DP media control command acknowledgement code.


    *Values:*

    enumerator BK_A2DP_MEDIA_CTRL_ACK_SUCCESS
    :   media control command is acknowledged with success

    enumerator BK_A2DP_MEDIA_CTRL_ACK_FAILURE
    :   media control command is acknowledged with failure

    enumerator BK_A2DP_MEDIA_CTRL_ACK_BUSY
    :   media control command is rejected, as previous command is not yet acknowledged

enum bk_a2dp_set_delay_value_state_t
:   Bluetooth A2DP set delay report value states.


    *Values:*

    enumerator BK_A2DP_SET_SUCCESS
    :   A2DP profile set delay report value successful

    enumerator BK_A2DP_SET_FAIL
    :   A2DP profile set delay report value failed


## bk_dm_avrcp_types.h

`bk_dm_avrcp_types.h` 定义 AVRCP profile 使用的事件、状态和媒体控制类型。


### Header File


- [bluetooth/bk_dm_avrcp_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_avrcp_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_avrcp_types.h")


### Unions

union bk_avrcp_rn_param_t
:   *#include <bk_dm_avrcp_types.h>*

    AVRCP notification parameters.

    Public Members

    uint8_t volume
    :   response data for BK_AVRCP_RN_VOLUME_CHANGE, ranges 0..127

    [bk_avrcp_playback_stat_t](#_CPPv424bk_avrcp_playback_stat_t "bk_avrcp_playback_stat_t") playback
    :   response data for BK_AVRCP_RN_PLAY_STATUS_CHANGE

    uint8_t elm_id[8]
    :   response data for BK_AVRCP_RN_TRACK_CHANGE

    uint32_t play_pos
    :   response data for BK_AVRCP_RN_PLAY_POS_CHANGED, in millisecond

    [bk_avrcp_batt_stat_t](#_CPPv420bk_avrcp_batt_stat_t "bk_avrcp_batt_stat_t") batt
    :   response data for BK_AVRCP_RN_BATTERY_STATUS_CHANGE

    uint16_t player_id

    uint16_t uid

    struct [bk_avrcp_rn_param_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t")::[anonymous] [anonymous]

    uint16_t uid_counter
    :   response data for BK_AVRCP_RN_UIDS_CHANGE

    uint8_t system_status
    :   response data for BK_AVRCP_RN_SYSTEM_STATUS_CHANGE

    uint8_t player_app_set_count

    uint8_t attr_id

    uint8_t value_id

    struct [bk_avrcp_rn_param_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t")::[anonymous]::[anonymous] player_app_set_array[[BK_AVRCP_PS_MAX_ATTR](#_CPPv4N22bk_avrcp_ps_attr_ids_t20BK_AVRCP_PS_MAX_ATTRE "BK_AVRCP_PS_MAX_ATTR")]

    struct [bk_avrcp_rn_param_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t")::[anonymous] [anonymous]

union bk_avrcp_ct_cb_param_t
:   *#include <bk_dm_avrcp_types.h>*

    AVRCP controller callback parameters.

    Public Members

    struct [bk_avrcp_ct_cb_param_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp_ct_conn_state_param](#_CPPv4N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_conn_state_param") conn_state
    :   AVRCP connection status

    struct [bk_avrcp_ct_cb_param_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp_ct_psth_rsp_param](#_CPPv4N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_psth_rsp_param") psth_rsp
    :   passthrough command response

    struct [bk_avrcp_ct_cb_param_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp_ct_change_notify_param](#_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_change_notify_param") change_ntf
    :   notifications

    struct [bk_avrcp_ct_cb_param_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp_ct_get_rn_caps_rsp_param](#_CPPv4N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_get_rn_caps_rsp_param") get_rn_caps_rsp
    :   get supported event capabilities response from AVRCP target

    struct [bk_avrcp_ct_cb_param_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp_ct_set_volume_rsp_param](#_CPPv4N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_set_volume_rsp_param") set_volume_rsp
    :   set absolute volume response event

    struct [bk_avrcp_ct_cb_param_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp_ct_set_player_app_setting_rsp_param](#_CPPv4N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_set_player_app_setting_rsp_param") set_player_app_setting_rsp
    :   set player app setting response event

    struct [bk_avrcp_ct_cb_param_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp_ct_elem_attr_rsp_param](#_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param") elem_attr_rsp
    :   metadata attributes response

    struct avrcp_ct_change_notify_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_CT_CHANGE_NOTIFY_EVT.

        Public Members

        uint8_t event_id
        :   id of AVRCP event notification

        [bk_avrcp_rn_param_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t") event_parameter
        :   event notification parameter

        uint8_t remote_bda[6]
        :   remote bluetooth device address

    struct avrcp_ct_conn_state_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_CT_CONNECTION_STATE_EVT.

        Public Members

        uint8_t connected
        :   whether AVRCP connection is set up

        uint8_t remote_bda[6]
        :   remote bluetooth device address

    struct avrcp_ct_elem_attr_rsp_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_CT_GET_ELEM_ATTR_RSP_EVT.

        Public Members

        uint8_t status

        uint8_t attr_count
        :   0 means success

        uint32_t attr_id
        :   elem attribute id, see bk_avrcp_media_attr_id_t

        uint16_t attr_text_charset

        uint32_t attr_length
        :   attr text charset, see [http://www.iana.org/assignments/character-sets](http://www.iana.org/assignments/character-sets "http://www.iana.org/assignments/character-sets")

            attribute character length

        uint8_t *attr_text
        :   attribute itself

        struct [bk_avrcp_ct_cb_param_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp_ct_elem_attr_rsp_param](#_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param")::[anonymous] *attr_array
        :   attr_array count

        uint8_t remote_bda[6]
        :   elem array

            remote bluetooth device address

    struct avrcp_ct_get_rn_caps_rsp_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_CT_GET_RN_CAPABILITIES_RSP_EVT.

        Public Members

        uint8_t cap_count
        :   number of items provided in event or company_id according to cap_id used

        [bk_avrcp_rn_evt_cap_mask_t](#_CPPv426bk_avrcp_rn_evt_cap_mask_t "bk_avrcp_rn_evt_cap_mask_t") evt_set
        :   supported event_ids represented in bit-mask

        uint8_t remote_bda[6]
        :   remote bluetooth device address

    struct avrcp_ct_psth_rsp_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_CT_PASSTHROUGH_RSP_EVT.

        Public Members

        uint8_t tl
        :   transaction label, 0 to 15

        uint8_t key_code
        :   passthrough command code, see bk_avrcp_pt_cmd_t

        uint8_t key_state
        :   0 for PRESSED, 1 for RELEASED

        [bk_avrcp_rsp_t](#_CPPv414bk_avrcp_rsp_t "bk_avrcp_rsp_t") rsp_code
        :   response code

        uint8_t remote_bda[6]
        :   remote bluetooth device address

    struct avrcp_ct_set_player_app_setting_rsp_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_CT_SET_PLAYER_APP_SETTING_RSP_EVT.

        Public Members

        uint8_t status

        uint8_t remote_bda[6]
        :   0 means success

            remote bluetooth device address

    struct avrcp_ct_set_volume_rsp_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_CT_SET_ABSOLUTE_VOLUME_RSP_EVT.

        Public Members

        uint8_t status

        uint8_t volume
        :   0 means success

            the volume which has actually been set, range is 0 to 0x7f, means 0% to 100%

        uint8_t remote_bda[6]
        :   remote bluetooth device address

union bk_avrcp_tg_cb_param_t
:   *#include <bk_dm_avrcp_types.h>*

    AVRC target callback parameters.

    Public Members

    struct [bk_avrcp_tg_cb_param_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t")::[avrcp_tg_conn_stat_param](#_CPPv4N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_paramE "bk_avrcp_tg_cb_param_t::avrcp_tg_conn_stat_param") conn_stat
    :   AVRC connection status

    struct [bk_avrcp_tg_cb_param_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t")::[avrcp_tg_psth_cmd_param](#_CPPv4N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_paramE "bk_avrcp_tg_cb_param_t::avrcp_tg_psth_cmd_param") psth_cmd
    :   passthrough command

    struct [bk_avrcp_tg_cb_param_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t")::[avrcp_tg_set_abs_vol_param](#_CPPv4N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_paramE "bk_avrcp_tg_cb_param_t::avrcp_tg_set_abs_vol_param") set_abs_vol
    :   set absolute volume command targeted on audio sink

    struct [bk_avrcp_tg_cb_param_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t")::[avrcp_tg_reg_ntf_param](#_CPPv4N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_paramE "bk_avrcp_tg_cb_param_t::avrcp_tg_reg_ntf_param") reg_ntf
    :   register notification

    struct avrcp_tg_conn_stat_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_TG_CONNECTION_STATE_EVT.

        Public Members

        bool connected
        :   whether AVRC connection is set up

        uint8_t remote_bda[6]
        :   remote bluetooth device address

    struct avrcp_tg_psth_cmd_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_TG_PASSTHROUGH_CMD_EVT.

        Public Members

        uint8_t key_code
        :   passthrough command code

        uint8_t key_state
        :   0 for PRESSED, 1 for RELEASED

        uint8_t remote_bda[6]
        :   remote bluetooth device address

    struct avrcp_tg_reg_ntf_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_TG_REGISTER_NOTIFICATION_EVT.

        Public Members

        uint8_t event_id
        :   event id of bk_avrcp_rn_event_ids_t

        uint32_t event_parameter
        :   event notification parameter, used with BK_AVRCP_RN_PLAY_POS_CHANGED only now, means timer in second

        uint8_t remote_bda[6]
        :   remote bluetooth device address

    struct avrcp_tg_set_abs_vol_param
    :   *#include <bk_dm_avrcp_types.h>*

        BK_AVRCP_TG_SET_ABSOLUTE_VOLUME_CMD_EVT.

        Public Members

        uint8_t volume
        :   volume ranges from 0 to 127

        uint8_t remote_bda[6]
        :   remote bluetooth device address


### Structures

struct bk_avrcp_rn_evt_cap_mask_t
:   AVRCP target notification event capability bit mask.

    Public Members

    uint16_t bits
    :   bit mask representation of supported event_ids

struct bk_avrcp_psth_bit_mask_t
:   AVRC passthrough command bit mask.

    Public Members

    uint16_t bits[8]
    :   bit mask representation of PASSTHROUGH commands


### Type Definitions

typedef void (*bk_avrcp_ct_cb_t)([bk_avrcp_ct_cb_event_t](#_CPPv422bk_avrcp_ct_cb_event_t "bk_avrcp_ct_cb_event_t") event, [bk_avrcp_ct_cb_param_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t") *param)
:   AVRCP controller callback function type.

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter union

typedef void (*bk_avrcp_tg_cb_t)([bk_avrcp_tg_cb_event_t](#_CPPv422bk_avrcp_tg_cb_event_t "bk_avrcp_tg_cb_event_t") event, [bk_avrcp_tg_cb_param_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t") *param)
:   AVRCP target callback function type.

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter union


### Enumerations

enum bk_avrcp_rn_event_ids_t
:   AVRCP event notification ids.


    *Values:*

    enumerator BK_AVRCP_RN_PLAY_STATUS_CHANGE
    :   track status change, eg. from playing to paused

    enumerator BK_AVRCP_RN_TRACK_CHANGE
    :   new track is loaded

    enumerator BK_AVRCP_RN_TRACK_REACHED_END
    :   current track reached end

    enumerator BK_AVRCP_RN_TRACK_REACHED_START
    :   current track reached start position

    enumerator BK_AVRCP_RN_PLAY_POS_CHANGED
    :   track playing position changed

    enumerator BK_AVRCP_RN_BATTERY_STATUS_CHANGE
    :   battery status changed

    enumerator BK_AVRCP_RN_SYSTEM_STATUS_CHANGE
    :   system status changed

    enumerator BK_AVRCP_RN_APP_SETTING_CHANGE
    :   application settings changed

    enumerator BK_AVRCP_RN_NOW_PLAYING_CHANGE
    :   now playing content changed

    enumerator BK_AVRCP_RN_AVAILABLE_PLAYERS_CHANGE
    :   available players changed

    enumerator BK_AVRCP_RN_ADDRESSED_PLAYER_CHANGE
    :   the addressed player changed

    enumerator BK_AVRCP_RN_UIDS_CHANGE
    :   UIDs changed

    enumerator BK_AVRCP_RN_VOLUME_CHANGE
    :   volume changed locally on TG

    enumerator BK_AVRCP_RN_MAX_EVT

enum bk_avrcp_ct_cb_event_t
:   AVRCP Controller callback events.


    *Values:*

    enumerator BK_AVRCP_CT_CONNECTION_STATE_EVT
    :   connection state changed event

    enumerator BK_AVRCP_CT_PASSTHROUGH_RSP_EVT
    :   passthrough response event

    enumerator BK_AVRCP_CT_GET_ELEM_ATTR_RSP_EVT
    :   get elem attr response event

    enumerator BK_AVRCP_CT_PLAY_STATUS_RSP_EVT
    :   play status response event

    enumerator BK_AVRCP_CT_CHANGE_NOTIFY_EVT
    :   notification event

    enumerator BK_AVRCP_CT_REMOTE_FEATURES_EVT
    :   feature of remote device indication event

    enumerator BK_AVRCP_CT_GET_RN_CAPABILITIES_RSP_EVT
    :   supported notification events capability of peer device

    enumerator BK_AVRCP_CT_SET_ABSOLUTE_VOLUME_RSP_EVT
    :   set absolute volume response event

    enumerator BK_AVRCP_CT_SET_PLAYER_APP_SETTING_RSP_EVT

enum bk_avrcp_rsp_t
:   AVCTP response codes.


    *Values:*

    enumerator BK_AVRCP_RSP_NOT_IMPL
    :   not implemented

    enumerator BK_AVRCP_RSP_ACCEPT
    :   accept

    enumerator BK_AVRCP_RSP_REJECT
    :   reject

    enumerator BK_AVRCP_RSP_IN_TRANS
    :   in transition

    enumerator BK_AVRCP_RSP_IMPL_STBL
    :   implemented/stable

    enumerator BK_AVRCP_RSP_CHANGED
    :   changed

    enumerator BK_AVRCP_RSP_INTERIM
    :   interim

enum bk_avrcp_batt_stat_t
:   AVRCP battery status.


    *Values:*

    enumerator BK_AVRCP_BATT_NORMAL
    :   normal state

    enumerator BK_AVRCP_BATT_WARNING
    :   unable to operate soon

    enumerator BK_AVRCP_BATT_CRITICAL
    :   cannot operate any more

    enumerator BK_AVRCP_BATT_EXTERNAL
    :   plugged to external power supply

    enumerator BK_AVRCP_BATT_FULL_CHARGE
    :   when completely charged from external power supply

enum bk_avrcp_playback_stat_t
:   AVRCP current status of playback.


    *Values:*

    enumerator BK_AVRCP_PLAYBACK_STOPPED
    :   stopped

    enumerator BK_AVRCP_PLAYBACK_PLAYING
    :   playing

    enumerator BK_AVRCP_PLAYBACK_PAUSED
    :   paused

    enumerator BK_AVRCP_PLAYBACK_FWD_SEEK
    :   forward seek

    enumerator BK_AVRCP_PLAYBACK_REV_SEEK
    :   reverse seek

    enumerator BK_AVRCP_PLAYBACK_ERROR
    :   error

enum bk_avrcp_pt_cmd_t
:   AVRCP passthrough command code.


    *Values:*

    enumerator BK_AVRCP_PT_CMD_SELECT
    :   select

    enumerator BK_AVRCP_PT_CMD_UP
    :   up

    enumerator BK_AVRCP_PT_CMD_DOWN
    :   down

    enumerator BK_AVRCP_PT_CMD_LEFT
    :   left

    enumerator BK_AVRCP_PT_CMD_RIGHT
    :   right

    enumerator BK_AVRCP_PT_CMD_RIGHT_UP
    :   right-up

    enumerator BK_AVRCP_PT_CMD_RIGHT_DOWN
    :   right-down

    enumerator BK_AVRCP_PT_CMD_LEFT_UP
    :   left-up

    enumerator BK_AVRCP_PT_CMD_LEFT_DOWN
    :   left-down

    enumerator BK_AVRCP_PT_CMD_ROOT_MENU
    :   root menu

    enumerator BK_AVRCP_PT_CMD_SETUP_MENU
    :   setup menu

    enumerator BK_AVRCP_PT_CMD_CONT_MENU
    :   contents menu

    enumerator BK_AVRCP_PT_CMD_FAV_MENU
    :   favorite menu

    enumerator BK_AVRCP_PT_CMD_EXIT
    :   exit

    enumerator BK_AVRCP_PT_CMD_0
    :   0

    enumerator BK_AVRCP_PT_CMD_1
    :   1

    enumerator BK_AVRCP_PT_CMD_2
    :   2

    enumerator BK_AVRCP_PT_CMD_3
    :   3

    enumerator BK_AVRCP_PT_CMD_4
    :   4

    enumerator BK_AVRCP_PT_CMD_5
    :   5

    enumerator BK_AVRCP_PT_CMD_6
    :   6

    enumerator BK_AVRCP_PT_CMD_7
    :   7

    enumerator BK_AVRCP_PT_CMD_8
    :   8

    enumerator BK_AVRCP_PT_CMD_9
    :   9

    enumerator BK_AVRCP_PT_CMD_DOT
    :   dot

    enumerator BK_AVRCP_PT_CMD_ENTER
    :   enter

    enumerator BK_AVRCP_PT_CMD_CLEAR
    :   clear

    enumerator BK_AVRCP_PT_CMD_CHAN_UP
    :   channel up

    enumerator BK_AVRCP_PT_CMD_CHAN_DOWN
    :   channel down

    enumerator BK_AVRCP_PT_CMD_PREV_CHAN
    :   previous channel

    enumerator BK_AVRCP_PT_CMD_SOUND_SEL
    :   sound select

    enumerator BK_AVRCP_PT_CMD_INPUT_SEL
    :   input select

    enumerator BK_AVRCP_PT_CMD_DISP_INFO
    :   display information

    enumerator BK_AVRCP_PT_CMD_HELP
    :   help

    enumerator BK_AVRCP_PT_CMD_PAGE_UP
    :   page up

    enumerator BK_AVRCP_PT_CMD_PAGE_DOWN
    :   page down

    enumerator BK_AVRCP_PT_CMD_POWER
    :   power

    enumerator BK_AVRCP_PT_CMD_VOL_UP
    :   volume up

    enumerator BK_AVRCP_PT_CMD_VOL_DOWN
    :   volume down

    enumerator BK_AVRCP_PT_CMD_MUTE
    :   mute

    enumerator BK_AVRCP_PT_CMD_PLAY
    :   play

    enumerator BK_AVRCP_PT_CMD_STOP
    :   stop

    enumerator BK_AVRCP_PT_CMD_PAUSE
    :   pause

    enumerator BK_AVRCP_PT_CMD_RECORD
    :   record

    enumerator BK_AVRCP_PT_CMD_REWIND
    :   rewind

    enumerator BK_AVRCP_PT_CMD_FAST_FORWARD
    :   fast forward

    enumerator BK_AVRCP_PT_CMD_EJECT
    :   eject

    enumerator BK_AVRCP_PT_CMD_FORWARD
    :   forward

    enumerator BK_AVRCP_PT_CMD_BACKWARD
    :   backward

    enumerator BK_AVRCP_PT_CMD_ANGLE
    :   angle

    enumerator BK_AVRCP_PT_CMD_SUBPICT
    :   subpicture

    enumerator BK_AVRCP_PT_CMD_F1
    :   F1

    enumerator BK_AVRCP_PT_CMD_F2
    :   F2

    enumerator BK_AVRCP_PT_CMD_F3
    :   F3

    enumerator BK_AVRCP_PT_CMD_F4
    :   F4

    enumerator BK_AVRCP_PT_CMD_F5
    :   F5

    enumerator BK_AVRCP_PT_CMD_VENDOR
    :   vendor unique

enum bk_avrcp_pt_cmd_state_t
:   AVRCP passthrough command state.


    *Values:*

    enumerator BK_AVRCP_PT_CMD_STATE_PRESSED
    :   key pressed

    enumerator BK_AVRCP_PT_CMD_STATE_RELEASED
    :   key released

enum bk_avrcp_media_attr_id_t
:   AVRC media attribute id.


    *Values:*

    enumerator BK_AVRCP_MEDIA_ATTR_ID_TITLE
    :   title of the playing track

    enumerator BK_AVRCP_MEDIA_ATTR_ID_ARTIST
    :   track artist

    enumerator BK_AVRCP_MEDIA_ATTR_ID_ALBUM
    :   album name

    enumerator BK_AVRCP_MEDIA_ATTR_ID_TRACK_NUM
    :   track position on the album

    enumerator BK_AVRCP_MEDIA_ATTR_ID_NUM_TRACKS
    :   number of tracks on the album

    enumerator BK_AVRCP_MEDIA_ATTR_ID_GENRE
    :   track genre

    enumerator BK_AVRCP_MEDIA_ATTR_ID_PLAYING_TIME
    :   total album playing time in miliseconds

    enumerator BK_AVRCP_MEDIA_ATTR_ID_DEFAULT_COVER_ART

enum bk_avrcp_ps_attr_ids_t
:   AVRC player setting ids.


    *Values:*

    enumerator BK_AVRCP_PS_EQUALIZER
    :   equalizer, on or off

    enumerator BK_AVRCP_PS_REPEAT_MODE
    :   repeat mode

    enumerator BK_AVRCP_PS_SHUFFLE_MODE
    :   shuffle mode

    enumerator BK_AVRCP_PS_SCAN_MODE
    :   scan mode on or off

    enumerator BK_AVRCP_PS_MAX_ATTR

enum bk_avrcp_rn_rsp_t
:   AVRC notification response type.


    *Values:*

    enumerator BK_AVRCP_RN_RSP_INTERIM
    :   initial response to RegisterNotification, should be sent T_mtp(1000ms) from receiving the command

    enumerator BK_AVRCP_RN_RSP_CHANGED
    :   final response to RegisterNotification command

enum bk_avrcp_rn_cap_api_method_t
:   AVRC target notification event notification capability.


    *Values:*

    enumerator BK_AVRCP_RN_CAP_API_METHOD_ALLOWED
    :   all of the notification events that can possibly be supported, immutable

    enumerator BK_AVRCP_RN_CAP_API_METHOD_CURRENT_ENABLE
    :   notification events selectively supported according to the current configuration

    enumerator BK_AVRCP_RN_CAP_API_METHOD_MAX

enum bk_avrcp_psth_filter_t
:   AVRC passthrough command filter.


    *Values:*

    enumerator BK_AVRCP_PSTH_FILTER_METHOD_ALLOWED
    :   all of the PASSTHROUGH commands that can possibly be used, immutable

    enumerator BK_AVRCP_PSTH_FILTER_METHOD_CURRENT_ENABLE
    :   PASSTHROUGH commands selectively supported according to the current configuration

    enumerator BK_AVRCP_PSTH_FILTER_METHOD_MAX

enum bk_avrcp_bit_mask_op_t
:   *Values:*

    enumerator BK_AVRCP_BIT_MASK_OP_TEST
    :   operation code to test a specific bit

    enumerator BK_AVRCP_BIT_MASK_OP_SET
    :   operation code to set a specific bit

    enumerator BK_AVRCP_BIT_MASK_OP_CLEAR
    :   operation code to clear a specific bit

enum bk_avrcp_tg_cb_event_t
:   AVRC Target callback events.


    *Values:*

    enumerator BK_AVRCP_TG_CONNECTION_STATE_EVT
    :   connection state changed event

    enumerator BK_AVRCP_TG_PASSTHROUGH_CMD_EVT
    :   passthrough command event

    enumerator BK_AVRCP_TG_SET_ABSOLUTE_VOLUME_CMD_EVT
    :   set absolute volume command from remote device

    enumerator BK_AVRCP_TG_REGISTER_NOTIFICATION_EVT
    :   register notification event


## bk_dm_hfp_types.h

`bk_dm_hfp_types.h` 定义 HFP profile 使用的事件、状态和通话控制类型。


### Header File


- [bluetooth/bk_dm_hfp_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_hfp_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_hfp_types.h")


### Structures

struct bk_hf_client_cb_param_t
:   HFP client callback parameters.

    Public Members

    uint8_t remote_bda[6]
    :   remote bluetooth device address


### Macros

BK_HF_CLIENT_PEER_FEAT_3WAY

BK_HF_CLIENT_PEER_FEAT_ECNR

BK_HF_CLIENT_PEER_FEAT_VREC

BK_HF_CLIENT_PEER_FEAT_INBAND

BK_HF_CLIENT_PEER_FEAT_VTAG

BK_HF_CLIENT_PEER_FEAT_REJECT

BK_HF_CLIENT_PEER_FEAT_ECS

BK_HF_CLIENT_PEER_FEAT_ECC

BK_HF_CLIENT_PEER_FEAT_EXTERR

BK_HF_CLIENT_PEER_FEAT_CODEC

BK_HF_CLIENT_PEER_FEAT_HF_IND

BK_HF_CLIENT_PEER_FEAT_ESCO_S4

BK_HF_CLIENT_CHLD_FEAT_REL

BK_HF_CLIENT_CHLD_FEAT_REL_ACC

BK_HF_CLIENT_CHLD_FEAT_REL_X

BK_HF_CLIENT_CHLD_FEAT_HOLD_ACC

BK_HF_CLIENT_CHLD_FEAT_PRIV_X

BK_HF_CLIENT_CHLD_FEAT_MERGE

BK_HF_CLIENT_CHLD_FEAT_MERGE_DETACH


### Type Definitions

typedef void (*bk_bt_hf_client_cb_t)([bk_hf_client_cb_event_t](#_CPPv423bk_hf_client_cb_event_t "bk_hf_client_cb_event_t") event, [bk_hf_client_cb_param_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t") *param)
:   HFP client callback function type.

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter

typedef void (*bk_bt_hf_client_data_cb_t)(const uint8_t *buf, uint16_t len)
:   HFP client incoming data callback function.

    Param buf
    :   **[in]** : pointer to the data(payload of HCI synchronous data packet) received from HFP AG device

    Param len
    :   **[in]** : size(in bytes) in buf


### Enumerations

enum bk_hf_client_connection_state_t
:   Bluetooth HFP RFCOMM connection and service level connection status.


    *Values:*

    enumerator BK_HF_CLIENT_CONNECTION_STATE_DISCONNECTED
    :   RFCOMM data link channel released

    enumerator BK_HF_CLIENT_CONNECTION_STATE_CONNECTING
    :   connecting remote device on the RFCOMM data link

    enumerator BK_HF_CLIENT_CONNECTION_STATE_CONNECTED
    :   RFCOMM connection established

    enumerator BK_HF_CLIENT_CONNECTION_STATE_SLC_CONNECTED
    :   service level connection established

    enumerator BK_HF_CLIENT_CONNECTION_STATE_DISCONNECTING
    :   disconnecting with remote device on the RFCOMM dat link

enum bk_hf_client_audio_state_t
:   Bluetooth HFP audio connection status.


    *Values:*

    enumerator BK_HF_CLIENT_AUDIO_STATE_DISCONNECTED
    :   audio connection released

    enumerator BK_HF_CLIENT_AUDIO_STATE_CONNECTING
    :   audio connection has been initiated

    enumerator BK_HF_CLIENT_AUDIO_STATE_CONNECTED
    :   audio connection is established

enum bk_hf_client_cb_event_t
:   HF CLIENT callback events.


    *Values:*

    enumerator BK_HF_CLIENT_CONNECTION_STATE_EVT
    :   connection state changed event

    enumerator BK_HF_CLIENT_AUDIO_STATE_EVT
    :   audio connection state change event

    enumerator BK_HF_CLIENT_BVRA_EVT
    :   voice recognition state change event

    enumerator BK_HF_CLIENT_CIND_CALL_EVT
    :   call indication

    enumerator BK_HF_CLIENT_CIND_CALL_SETUP_EVT
    :   call setup indication

    enumerator BK_HF_CLIENT_CIND_CALL_HELD_EVT
    :   call held indication

    enumerator BK_HF_CLIENT_CIND_SERVICE_AVAILABILITY_EVT
    :   network service availability indication

    enumerator BK_HF_CLIENT_CIND_SIGNAL_STRENGTH_EVT
    :   signal strength indication

    enumerator BK_HF_CLIENT_CIND_ROAMING_STATUS_EVT
    :   roaming status indication

    enumerator BK_HF_CLIENT_CIND_BATTERY_LEVEL_EVT
    :   battery level indication

    enumerator BK_HF_CLIENT_COPS_CURRENT_OPERATOR_EVT
    :   current operator information

    enumerator BK_HF_CLIENT_BTRH_EVT
    :   call response and hold event

    enumerator BK_HF_CLIENT_CLIP_EVT
    :   Calling Line Identification notification

    enumerator BK_HF_CLIENT_CCWA_EVT
    :   call waiting notification

    enumerator BK_HF_CLIENT_CLCC_EVT
    :   list of current calls notification

    enumerator BK_HF_CLIENT_VOLUME_CONTROL_EVT
    :   audio volume control command from AG, provided by +VGM or +VGS message

    enumerator BK_HF_CLIENT_AT_RESPONSE_EVT
    :   AT command response event

    enumerator BK_HF_CLIENT_CNUM_EVT
    :   subscriber information response from AG

    enumerator BK_HF_CLIENT_BSIR_EVT
    :   setting of in-band ring tone

    enumerator BK_HF_CLIENT_BINP_EVT
    :   requested number of last voice tag from AG

    enumerator BK_HF_CLIENT_RING_IND_EVT
    :   ring indication event

enum bk_hf_codec_type_t
:   Codec Type.


    *Values:*

    enumerator CODEC_VOICE_CVSD
    :   cvsd

    enumerator CODEC_VOICE_MSBC
    :   msbc

enum bk_hf_vr_state_t
:   voice recognition state


    *Values:*

    enumerator BK_HF_VR_STATE_DISABLED
    :   voice recognition disabled

    enumerator BK_HF_VR_STATE_ENABLED
    :   voice recognition enabled

enum bk_hf_call_status_t
:   +CIND call status indicator values


    *Values:*

    enumerator BK_HF_CALL_STATUS_NO_CALLS
    :   no call in progress

    enumerator BK_HF_CALL_STATUS_CALL_IN_PROGRESS
    :   call is present(active or held)

enum bk_hf_call_setup_status_t
:   +CIND call setup status indicator values


    *Values:*

    enumerator BK_HF_CALL_SETUP_STATUS_IDLE
    :   no call setup in progress

    enumerator BK_HF_CALL_SETUP_STATUS_INCOMING
    :   incoming call setup in progress

    enumerator BK_HF_CALL_SETUP_STATUS_OUTGOING_DIALING
    :   outgoing call setup in dialing state

    enumerator BK_HF_CALL_SETUP_STATUS_OUTGOING_ALERTING
    :   outgoing call setup in alerting state

enum bk_hf_call_held_status_t
:   +CIND call held indicator values


    *Values:*

    enumerator BK_HF_CALL_HELD_STATUS_NONE
    :   no calls held

    enumerator BK_HF_CALL_HELD_STATUS_HELD_AND_ACTIVE
    :   both active and held call

    enumerator BK_HF_CALL_HELD_STATUS_HELD
    :   call on hold, no active call

enum bk_hf_network_state_t
:   +CIND network service availability status


    *Values:*

    enumerator BK_HF_NETWORK_STATE_NOT_AVAILABLE

    enumerator BK_HF_NETWORK_STATE_AVAILABLE

enum bk_hf_roaming_status_t
:   +CIND roaming status indicator values


    *Values:*

    enumerator BK_HF_ROAMING_STATUS_INACTIVE
    :   roaming is not active

    enumerator BK_HF_ROAMING_STATUS_ACTIVE
    :   a roaming is active

enum bk_hf_btrh_status_t
:   +BTRH response and hold result code


    *Values:*

    enumerator BK_HF_BTRH_STATUS_HELD
    :   incoming call is put on held in AG

    enumerator BK_HF_BTRH_STATUS_ACCEPTED
    :   held incoming call is accepted in AG

    enumerator BK_HF_BTRH_STATUS_REJECTED
    :   held incoming call is rejected in AG

enum bk_hf_current_call_status_t
:   +CLCC status of the call


    *Values:*

    enumerator BK_HF_CURRENT_CALL_STATUS_ACTIVE
    :   active

    enumerator BK_HF_CURRENT_CALL_STATUS_HELD
    :   held

    enumerator BK_HF_CURRENT_CALL_STATUS_DIALING
    :   dialing (outgoing calls only)

    enumerator BK_HF_CURRENT_CALL_STATUS_ALERTING
    :   alerting (outgoing calls only)

    enumerator BK_HF_CURRENT_CALL_STATUS_INCOMING
    :   incoming (incoming calls only)

    enumerator BK_HF_CURRENT_CALL_STATUS_WAITING
    :   waiting (incoming calls only)

    enumerator BK_HF_CURRENT_CALL_STATUS_HELD_BY_RBK_HOLD
    :   call held by response and hold

enum bk_hf_current_call_direction_t
:   +CLCC direction of the call


    *Values:*

    enumerator BK_HF_CURRENT_CALL_DIRECTION_OUTGOING
    :   outgoing

    enumerator BK_HF_CURRENT_CALL_DIRECTION_INCOMING
    :   incoming

enum bk_hf_current_call_mpty_type_t
:   +CLCC multi-party call flag


    *Values:*

    enumerator BK_HF_CURRENT_CALL_MPTY_TYPE_SINGLE
    :   not a member of a multi-party call

    enumerator BK_HF_CURRENT_CALL_MPTY_TYPE_MULTI
    :   member of a multi-party call

enum bk_hf_volume_control_target_t
:   Bluetooth HFP audio volume control target.


    *Values:*

    enumerator BK_HF_VOLUME_CONTROL_TARGET_SPK
    :   speaker

    enumerator BK_HF_VOLUME_CONTROL_TARGET_MIC
    :   microphone

enum bk_hf_chld_type_t
:   AT+CHLD command values.


    *Values:*

    enumerator BK_HF_CHLD_TYPE_REL
    :   <0>, Terminate all held or set UDUB(“busy”) to a waiting call

    enumerator BK_HF_CHLD_TYPE_REL_ACC
    :   <1>, Terminate all active calls and accepts a waiting/held call

    enumerator BK_HF_CHLD_TYPE_HOLD_ACC
    :   <2>, Hold all active calls and accepts a waiting/held call

    enumerator BK_HF_CHLD_TYPE_MERGE
    :   <3>, Add all held calls to a conference

    enumerator BK_HF_CHLD_TYPE_MERGE_DETACH
    :   <4>, connect the two calls and disconnects the subscriber from both calls

enum bk_hf_btrh_cmd_t
:   AT+BTRH response and hold action code.


    *Values:*

    enumerator BK_HF_BTRH_CMD_HOLD
    :   put the incoming call on hold

    enumerator BK_HF_BTRH_CMD_ACCEPT
    :   accept a held incoming call

    enumerator BK_HF_BTRH_CMD_REJECT
    :   reject a held incoming call

enum bk_hf_at_response_code_t
:   *Values:*

    enumerator BK_HF_AT_RESPONSE_CODE_OK
    :   acknowledges execution of a command line

    enumerator BK_HF_AT_RESPONSE_CODE_ERR
    :   command not accepted

    enumerator BK_HF_AT_RESPONSE_CODE_NO_CARRIER
    :   connection terminated

    enumerator BK_HF_AT_RESPONSE_CODE_BUSY
    :   busy signal detected

    enumerator BK_HF_AT_RESPONSE_CODE_NO_ANSWER
    :   connection completion timeout

    enumerator BK_HF_AT_RESPONSE_CODE_DELAYED
    :   delayed

    enumerator BK_HF_AT_RESPONSE_CODE_BLACKLISTED
    :   blacklisted

    enumerator BK_HF_AT_RESPONSE_CODE_CME
    :   CME error

enum bk_hf_at_response_t
:   *Values:*

    enumerator BK_HF_AT_RESPONSE_ERROR

    enumerator BK_HF_AT_RESPONSE_OK

enum bk_hf_cme_err_t
:   Extended Audio Gateway Error Result Code Response.


    *Values:*

    enumerator BK_HF_CME_AG_FAILURE
    :   ag failure

    enumerator BK_HF_CME_NO_CONNECTION_TO_PHONE
    :   no connection to phone

    enumerator BK_HF_CME_OPERATION_NOT_ALLOWED
    :   operation not allowed

    enumerator BK_HF_CME_OPERATION_NOT_SUPPORTED
    :   operation not supported

    enumerator BK_HF_CME_PH_SIM_PIN_REQUIRED
    :   PH-SIM PIN Required

    enumerator BK_HF_CME_SIM_NOT_INSERTED
    :   SIM not inserted

    enumerator BK_HF_CME_SIM_PIN_REQUIRED
    :   SIM PIN required

    enumerator BK_HF_CME_SIM_PUK_REQUIRED
    :   SIM PUK required

    enumerator BK_HF_CME_SIM_FAILURE
    :   SIM failure

    enumerator BK_HF_CME_SIM_BUSY
    :   SIM busy

    enumerator BK_HF_CME_INCORRECT_PASSWORD
    :   incorrect password

    enumerator BK_HF_CME_SIM_PIN2_REQUIRED
    :   SIM PIN2 required

    enumerator BK_HF_CME_SIM_PUK2_REQUIRED
    :   SIM PUK2 required

    enumerator BK_HF_CME_MEMORY_FULL
    :   memory full

    enumerator BK_HF_CME_INVALID_INDEX
    :   invalid index

    enumerator BK_HF_CME_MEMORY_FAILURE
    :   memory failure

    enumerator BK_HF_CME_TEXT_STRING_TOO_LONG
    :   test string too long

    enumerator BK_HF_CME_INVALID_CHARACTERS_IN_TEXT_STRING
    :   invalid characters in text string

    enumerator BK_HF_CME_DIAL_STRING_TOO_LONG
    :   dial string too long

    enumerator BK_HF_CME_INVALID_CHARACTERS_IN_DIAL_STRING
    :   invalid characters in dial string

    enumerator BK_HF_CME_NO_NETWORK_SERVICE
    :   no network service

    enumerator BK_HF_CME_NETWORK_TIMEOUT
    :   network timeout

    enumerator BK_HF_CME_NETWORK_NOT_ALLOWED
    :   network not allowed &#8212;emergency calls only

enum bk_hf_subscriber_service_type_t
:   +CNUM service type of the phone number


    *Values:*

    enumerator BK_HF_SUBSCRIBER_SERVICE_TYPE_UNKNOWN
    :   unknown

    enumerator BK_HF_SUBSCRIBER_SERVICE_TYPE_VOICE
    :   voice service

    enumerator BK_HF_SUBSCRIBER_SERVICE_TYPE_FAX
    :   fax service

enum bk_hf_client_in_band_ring_state_t
:   in-band ring tone state


    *Values:*

    enumerator BK_HF_CLIENT_IN_BAND_RINGTONE_NOT_PROVIDED

    enumerator BK_HF_CLIENT_IN_BAND_RINGTONE_PROVIDED


## bk_dm_gap_bt_types.h

`bk_dm_gap_bt_types.h` 定义 BT GAP 使用的设备、配对和连接相关类型。


### Header File


- [bluetooth/bk_dm_gap_bt_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gap_bt_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gap_bt_types.h")


### Unions

union bk_bt_cod_t
:   *#include <bk_dm_gap_bt_types.h>*

    Class of device.

    Public Members

    struct [bk_bt_cod_t](#_CPPv411bk_bt_cod_t "bk_bt_cod_t")::[class_of_device](#_CPPv4N11bk_bt_cod_t15class_of_deviceE "bk_bt_cod_t::class_of_device") cod_t

    uint32_t cod

    struct class_of_device
    :   Public Members

        uint32_t reserved_2
        :   reserved

        uint32_t minor
        :   minor class

        uint32_t major
        :   major class

        uint32_t service
        :   service class

        uint32_t reserved_8
        :   reserved

union bk_bt_gap_cb_param_t
:   *#include <bk_dm_gap_bt_types.h>*

    GAP state callback parameters.

    Public Members

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[disc_res_param](#_CPPv4N20bk_bt_gap_cb_param_t14disc_res_paramE "bk_bt_gap_cb_param_t::disc_res_param") disc_res
    :   discovery result parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[disc_state_changed_param](#_CPPv4N20bk_bt_gap_cb_param_t24disc_state_changed_paramE "bk_bt_gap_cb_param_t::disc_state_changed_param") disc_st_chg
    :   discovery state changed parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[rmt_srvcs_param](#_CPPv4N20bk_bt_gap_cb_param_t15rmt_srvcs_paramE "bk_bt_gap_cb_param_t::rmt_srvcs_param") rmt_srvcs
    :   services of remote device parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[rmt_srvc_rec_param](#_CPPv4N20bk_bt_gap_cb_param_t18rmt_srvc_rec_paramE "bk_bt_gap_cb_param_t::rmt_srvc_rec_param") rmt_srvc_rec
    :   specific service record from remote device parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[read_rssi_delta_param](#_CPPv4N20bk_bt_gap_cb_param_t21read_rssi_delta_paramE "bk_bt_gap_cb_param_t::read_rssi_delta_param") read_rssi_delta
    :   read rssi parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[config_eir_data_param](#_CPPv4N20bk_bt_gap_cb_param_t21config_eir_data_paramE "bk_bt_gap_cb_param_t::config_eir_data_param") config_eir_data
    :   config EIR data

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[auth_cmpl_param](#_CPPv4N20bk_bt_gap_cb_param_t15auth_cmpl_paramE "bk_bt_gap_cb_param_t::auth_cmpl_param") auth_cmpl
    :   authentication complete parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[pin_req_param](#_CPPv4N20bk_bt_gap_cb_param_t13pin_req_paramE "bk_bt_gap_cb_param_t::pin_req_param") pin_req
    :   pin request parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[cfm_req_param](#_CPPv4N20bk_bt_gap_cb_param_t13cfm_req_paramE "bk_bt_gap_cb_param_t::cfm_req_param") cfm_req
    :   confirm request parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[key_notif_param](#_CPPv4N20bk_bt_gap_cb_param_t15key_notif_paramE "bk_bt_gap_cb_param_t::key_notif_param") key_notif
    :   passkey notif parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[key_req_param](#_CPPv4N20bk_bt_gap_cb_param_t13key_req_paramE "bk_bt_gap_cb_param_t::key_req_param") key_req
    :   passkey request parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[set_afh_channels_param](#_CPPv4N20bk_bt_gap_cb_param_t22set_afh_channels_paramE "bk_bt_gap_cb_param_t::set_afh_channels_param") set_afh_channels
    :   set AFH channel parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[read_rmt_name_param](#_CPPv4N20bk_bt_gap_cb_param_t19read_rmt_name_paramE "bk_bt_gap_cb_param_t::read_rmt_name_param") read_rmt_name
    :   read Remote Name parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[mode_chg_param](#_CPPv4N20bk_bt_gap_cb_param_t14mode_chg_paramE "bk_bt_gap_cb_param_t::mode_chg_param") mode_chg
    :   mode change event parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[bt_remove_bond_dev_cmpl_evt_param](#_CPPv4N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_paramE "bk_bt_gap_cb_param_t::bt_remove_bond_dev_cmpl_evt_param") remove_bond_dev_cmpl
    :   Event parameter of BK_BT_GAP_REMOVE_BOND_DEV_COMPLETE_EVT

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[qos_cmpl_param](#_CPPv4N20bk_bt_gap_cb_param_t14qos_cmpl_paramE "bk_bt_gap_cb_param_t::qos_cmpl_param") qos_cmpl
    :   QoS complete parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[acl_conn_cmpl_stat_param](#_CPPv4N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_paramE "bk_bt_gap_cb_param_t::acl_conn_cmpl_stat_param") acl_conn_cmpl_stat
    :   ACL connection complete status parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[acl_disconn_cmpl_stat_param](#_CPPv4N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_paramE "bk_bt_gap_cb_param_t::acl_disconn_cmpl_stat_param") acl_disconn_cmpl_stat
    :   ACL disconnection complete status parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[link_key_notif_param](#_CPPv4N20bk_bt_gap_cb_param_t20link_key_notif_paramE "bk_bt_gap_cb_param_t::link_key_notif_param") link_key_notif
    :   link key notif parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[link_key_req_param](#_CPPv4N20bk_bt_gap_cb_param_t18link_key_req_paramE "bk_bt_gap_cb_param_t::link_key_req_param") link_key_req
    :   link key request parameter struct

    struct [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[auto_sniff_cmpl_param](#_CPPv4N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_paramE "bk_bt_gap_cb_param_t::auto_sniff_cmpl_param") auto_sniff_cmpl

    struct acl_conn_cmpl_stat_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_ACL_CONN_CMPL_STAT_EVT.

        Public Members

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   ACL connection status

        uint16_t handle
        :   ACL connection handle

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        uint32_t cod
        :   Class of Device for remote bluetooth device, it is only valid when paged by remote bluetooth device

    struct acl_disconn_cmpl_stat_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_ACL_DISCONN_CMPL_STAT_EVT.

        Public Members

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") reason
        :   ACL disconnection reason

        uint16_t handle
        :   ACL connection handle

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

    struct auth_cmpl_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_AUTH_CMPL_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   authentication complete status

    struct auto_sniff_cmpl_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_SET_AUTO_SNIFF_CMPL_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") result
        :   peer addr

    struct bt_remove_bond_dev_cmpl_evt_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_REMOVE_BOND_DEV_COMPLETE_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the remove bond device operation success status

    struct cfm_req_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_CFM_REQ_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        uint32_t num_val
        :   the numeric value for comparison.

    struct config_eir_data_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_CONFIG_EIR_DATA_EVT *.

        Public Members

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   config EIR status: BK_BT_STATUS_SUCCESS: config success BK_BT_STATUS_EIR_TOO_LARGE: the EIR data is more than 240B. The EIR may not contain the whole data. others: failed

        uint8_t eir_type_num
        :   the number of EIR types in EIR type

        [bk_bt_eir_type_t](#_CPPv416bk_bt_eir_type_t "bk_bt_eir_type_t") eir_type[BK_BT_EIR_TYPE_MAX_NUM]
        :   EIR types in EIR type

    struct disc_res_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_DISC_RES_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        int num_prop
        :   number of properties got

        [bk_bt_gap_dev_prop_t](#_CPPv420bk_bt_gap_dev_prop_t "bk_bt_gap_dev_prop_t") *prop
        :   properties discovered from the new device

    struct disc_state_changed_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_DISC_STATE_CHANGED_EVT.

        Public Members

        [bk_bt_gap_discovery_state_t](#_CPPv427bk_bt_gap_discovery_state_t "bk_bt_gap_discovery_state_t") state
        :   discovery state

    struct key_notif_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_KEY_NOTIF_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        uint32_t passkey
        :   the numeric value for passkey entry.

    struct key_req_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_KEY_REQ_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

    struct link_key_notif_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_LINK_KEY_NOTIF_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        uint8_t link_key[16]
        :   Link Key for the associated bda.

    struct link_key_req_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_LINK_KEY_REQ_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

    struct mode_chg_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_MODE_CHG_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        [bk_bt_pm_mode_t](#_CPPv415bk_bt_pm_mode_t "bk_bt_pm_mode_t") mode
        :   PM mode

    struct pin_req_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_PIN_REQ_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        bool min_16_digit
        :   TRUE if the pin returned must be at least 16 digits

    struct qos_cmpl_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_QOS_CMPL_EVT.

        Public Members

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   QoS status

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        uint32_t t_poll
        :   poll interval, the maximum time between transmissions which from the master to a particular slave on the ACL logical transport. unit is 0.625ms.

    struct read_rmt_name_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_READ_REMOTE_NAME_EVT.

        Public Members

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   read Remote Name status

        uint8_t rmt_name[BK_BT_GAP_MAX_BDNAME_LEN + 1]
        :   Remote device name

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

    struct read_rssi_delta_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_READ_RSSI_DELTA_EVT *.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   read rssi status

        int8_t rssi_delta
        :   rssi delta value range -128 ~127, The value zero indicates that the RSSI is inside the Golden Receive Power Range, the Golden Receive Power Range is from BK_BT_GAP_RSSI_LOW_THRLD to BK_BT_GAP_RSSI_HIGH_THRLD

    struct rmt_srvc_rec_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_RMT_SRVC_REC_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   service search status

    struct rmt_srvcs_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_RMT_SRVCS_EVT.

        Public Members

        [bk_bd_addr_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   service search status

        int num_uuids
        :   number of UUID in uuid_list

        [bk_bt_uuid_t](dual_ble.md#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") *uuid_list
        :   list of service UUIDs of remote device

    struct set_afh_channels_param
    :   *#include <bk_dm_gap_bt_types.h>*

        BK_BT_GAP_SET_AFH_CHANNELS_EVT.

        Public Members

        [bk_bt_status_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   set AFH channel status


### Structures

struct bk_bt_gap_dev_prop_t
:   Bluetooth Device Property Descriptor.

    Public Members

    [bk_bt_gap_dev_prop_type_t](#_CPPv425bk_bt_gap_dev_prop_type_t "bk_bt_gap_dev_prop_type_t") type
    :   Device property type

    int len
    :   Device property value length

    void *val
    :   Device property value

struct bk_bt_eir_data_t
:   EIR data content, according to “Supplement to the Bluetooth Core Specification”.

    Public Members

    bool fec_required
    :   FEC is required or not, true by default

    bool include_txpower
    :   EIR data include TX power, false by default

    bool include_uuid
    :   EIR data include UUID, false by default

    uint8_t flag
    :   EIR flags, see BK_BT_EIR_FLAG for details, EIR will not include flag if it is 0, 0 by default

    uint16_t manufacturer_len
    :   Manufacturer data length, 0 by default

    uint8_t *p_manufacturer_data
    :   Manufacturer data point

    uint16_t url_len
    :   URL length, 0 by default

    uint8_t *p_url
    :   URL point

struct bk_bt_gap_sniff_config
:   bt sniff config

    Public Members

    uint16_t sniff_min_interval
    :   unit 0.625ms, range: 1.25ms ~ 40.9s

    uint16_t sniff_attempt
    :   unit 0.625ms, range: 1.25ms ~ 40.9s

    uint16_t sniff_timeout
    :   unit 1.25ms, range: 1.25ms ~ 40.9s


### Macros

BK_BT_GAP_RSSI_HIGH_THRLD
:   RSSI threshold.

    High RSSI threshold

BK_BT_GAP_RSSI_LOW_THRLD
:   Low RSSI threshold

BK_BT_GAP_AFH_CHANNELS_LEN

BK_BT_GAP_MAX_BDNAME_LEN
:   Maximum bytes of Bluetooth device name.

BK_BT_GAP_EIR_DATA_LEN
:   Maximum size of EIR Significant part.

BK_BT_EIR_TYPE_FLAGS
:   Extended Inquiry Response data type.

    Flag with information such as BR/EDR and LE support

BK_BT_EIR_TYPE_INCMPL_16BITS_UUID
:   Incomplete list of 16-bit service UUIDs

BK_BT_EIR_TYPE_CMPL_16BITS_UUID
:   Complete list of 16-bit service UUIDs

BK_BT_EIR_TYPE_INCMPL_32BITS_UUID
:   Incomplete list of 32-bit service UUIDs

BK_BT_EIR_TYPE_CMPL_32BITS_UUID
:   Complete list of 32-bit service UUIDs

BK_BT_EIR_TYPE_INCMPL_128BITS_UUID
:   Incomplete list of 128-bit service UUIDs

BK_BT_EIR_TYPE_CMPL_128BITS_UUID
:   Complete list of 128-bit service UUIDs

BK_BT_EIR_TYPE_SHORT_LOCAL_NAME
:   Shortened Local Name

BK_BT_EIR_TYPE_CMPL_LOCAL_NAME
:   Complete Local Name

BK_BT_EIR_TYPE_TX_POWER_LEVEL
:   Tx power level, value is 1 octet ranging from -127 to 127, unit is dBm

BK_BT_EIR_TYPE_URL
:   Uniform resource identifier

BK_BT_EIR_TYPE_MANU_SPECIFIC
:   Manufacturer specific data

BK_BT_EIR_TYPE_MAX_NUM
:   MAX number of EIR type

BK_BT_EIR_FLAG_LIMIT_DISC

BK_BT_EIR_FLAG_GEN_DISC

BK_BT_EIR_FLAG_BREDR_NOT_SPT

BK_BT_EIR_FLAG_DMT_CONTROLLER_SPT

BK_BT_EIR_FLAG_DMT_HOST_SPT

BK_BT_EIR_MAX_LEN

BK_BT_PIN_CODE_LEN
:   Max pin code length

BK_BT_IO_CAP_OUT
:   IO Capability Constants DisplayOnly

BK_BT_IO_CAP_IO
:   DisplayYesNo

BK_BT_IO_CAP_IN
:   KeyboardOnly

BK_BT_IO_CAP_NONE
:   NoInputNoOutput

BK_BT_PM_MD_ACTIVE
:   Active mode

BK_BT_PM_MD_HOLD
:   Hold mode

BK_BT_PM_MD_SNIFF
:   Sniff mode

BK_BT_PM_MD_PARK
:   Park state

BK_BT_COD_SRVC_BIT_MASK
:   Bits of major service class field.

    Major service bit mask

BK_BT_COD_SRVC_BIT_OFFSET
:   Major service bit offset

BK_BT_COD_MAJOR_DEV_BIT_MASK
:   Bits of major device class field.

    Major device bit mask

BK_BT_COD_MAJOR_DEV_BIT_OFFSET
:   Major device bit offset

BK_BT_COD_MINOR_DEV_BIT_MASK
:   Bits of minor device class field.

    Minor device bit mask

BK_BT_COD_MINOR_DEV_BIT_OFFSET
:   Minor device bit offset

BK_BT_COD_FORMAT_TYPE_BIT_MASK
:   Bits of format type.

    Format type bit mask

BK_BT_COD_FORMAT_TYPE_BIT_OFFSET
:   Format type bit offset

BK_BT_COD_FORMAT_TYPE_1
:   Class of device format type 1.

BK_BT_GAP_MIN_INQ_LEN
:   Minimum and Maximum inquiry length Minimum inquiry duration, unit is 1.28s

BK_BT_GAP_MAX_INQ_LEN
:   Maximum inquiry duration, unit is 1.28s


### Type Definitions

typedef uint8_t bk_bt_gap_afh_channels[BK_BT_GAP_AFH_CHANNELS_LEN]

typedef uint8_t bk_bt_eir_type_t

typedef uint8_t bk_bt_pin_code_t[BK_BT_PIN_CODE_LEN]
:   Pin Code (upto 128 bits) MSB is 0

typedef uint8_t bk_bt_io_cap_t
:   Combination of the IO Capability

typedef uint8_t bk_bt_pm_mode_t

typedef void (*bk_bt_gap_cb_t)([bk_gap_bt_cb_event_t](#_CPPv420bk_gap_bt_cb_event_t "bk_gap_bt_cb_event_t") event, [bk_bt_gap_cb_param_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t") *param)
:   bluetooth GAP callback function type

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter


### Enumerations

enum bk_bt_cod_mode_t
:   class of device settings


    *Values:*

    enumerator BK_BT_SET_COD_MAJOR_MINOR
    :   overwrite major, minor class

    enumerator BK_BT_SET_COD_SERVICE_CLASS
    :   set the bits in the input, the current bit will remain

    enumerator BK_BT_CLR_COD_SERVICE_CLASS
    :   clear the bits in the input, others will remain

    enumerator BK_BT_SET_COD_ALL
    :   overwrite major, minor, set the bits in service class

    enumerator BK_BT_INIT_COD
    :   overwrite major, minor, and service class

enum bk_bt_gap_dev_prop_type_t
:   Bluetooth Device Property type.


    *Values:*

    enumerator BK_BT_GAP_DEV_PROP_BDNAME
    :   Bluetooth device name, value type is int8_t []

    enumerator BK_BT_GAP_DEV_PROP_COD
    :   Class of Device, value type is uint32_t

    enumerator BK_BT_GAP_DEV_PROP_RSSI
    :   Received Signal strength Indication, value type is int8_t, ranging from -128 to 127

    enumerator BK_BT_GAP_DEV_PROP_EIR
    :   Extended Inquiry Response, value type is uint8_t []

enum bk_bt_cod_srvc_t
:   Major service class field of Class of Device, mutiple bits can be set.


    *Values:*

    enumerator BK_BT_COD_SRVC_NONE
    :   None indicates an invalid value

    enumerator BK_BT_COD_SRVC_LMTD_DISCOVER
    :   Limited Discoverable Mode

    enumerator BK_BT_COD_SRVC_POSITIONING
    :   Positioning (Location identification)

    enumerator BK_BT_COD_SRVC_NETWORKING
    :   Networking, e.g. LAN, Ad hoc

    enumerator BK_BT_COD_SRVC_RENDERING
    :   Rendering, e.g. Printing, Speakers

    enumerator BK_BT_COD_SRVC_CAPTURING
    :   Capturing, e.g. Scanner, Microphone

    enumerator BK_BT_COD_SRVC_OBJ_TRANSFER
    :   Object Transfer, e.g. v-Inbox, v-Folder

    enumerator BK_BT_COD_SRVC_AUDIO
    :   Audio, e.g. Speaker, Microphone, Headset service

    enumerator BK_BT_COD_SRVC_TELEPHONY
    :   Telephony, e.g. Cordless telephony, Modem, Headset service

    enumerator BK_BT_COD_SRVC_INFORMATION
    :   Information, e.g., WEB-server, WAP-server

enum bk_bt_pin_type_t
:   *Values:*

    enumerator BK_BT_PIN_TYPE_VARIABLE
    :   Refer to BTM_PIN_TYPE_VARIABLE

    enumerator BK_BT_PIN_TYPE_FIXED
    :   Refer to BTM_PIN_TYPE_FIXED

enum bk_bt_sp_param_t
:   *Values:*

    enumerator BK_BT_SP_IOCAP_MODE
    :   Set IO mode

enum bk_bt_cod_major_dev_t
:   Major device class field of Class of Device.


    *Values:*

    enumerator BK_BT_COD_MAJOR_DEV_MISC
    :   Miscellaneous

    enumerator BK_BT_COD_MAJOR_DEV_COMPUTER
    :   Computer

    enumerator BK_BT_COD_MAJOR_DEV_PHONE
    :   Phone(cellular, cordless, pay phone, modem

    enumerator BK_BT_COD_MAJOR_DEV_LAN_NAP
    :   LAN, Network Access Point

    enumerator BK_BT_COD_MAJOR_DEV_AV
    :   Audio/Video(headset, speaker, stereo, video display, VCR

    enumerator BK_BT_COD_MAJOR_DEV_PERIPHERAL
    :   Peripheral(mouse, joystick, keyboard)

    enumerator BK_BT_COD_MAJOR_DEV_IMAGING
    :   Imaging(printer, scanner, camera, display

    enumerator BK_BT_COD_MAJOR_DEV_WEARABLE
    :   Wearable

    enumerator BK_BT_COD_MAJOR_DEV_TOY
    :   Toy

    enumerator BK_BT_COD_MAJOR_DEV_HEALTH
    :   Health

    enumerator BK_BT_COD_MAJOR_DEV_UNCATEGORIZED
    :   Uncategorized: device not specified

enum bk_bt_gap_discovery_state_t
:   Bluetooth Device Discovery state


    *Values:*

    enumerator BK_BT_GAP_DISCOVERY_STOPPED
    :   Device discovery stopped

    enumerator BK_BT_GAP_DISCOVERY_STARTED
    :   Device discovery started

enum bk_gap_bt_cb_event_t
:   BT GAP callback events.


    *Values:*

    enumerator BK_BT_GAP_DISC_RES_EVT
    :   Device discovery result event

    enumerator BK_BT_GAP_DISC_STATE_CHANGED_EVT
    :   Discovery state changed event

    enumerator BK_BT_GAP_RMT_SRVCS_EVT
    :   Get remote services event

    enumerator BK_BT_GAP_RMT_SRVC_REC_EVT
    :   Get remote service record event

    enumerator BK_BT_GAP_AUTH_CMPL_EVT
    :   Authentication complete event

    enumerator BK_BT_GAP_PIN_REQ_EVT
    :   Legacy Pairing Pin code request

    enumerator BK_BT_GAP_CFM_REQ_EVT
    :   Security Simple Pairing User Confirmation request.

    enumerator BK_BT_GAP_KEY_NOTIF_EVT
    :   Security Simple Pairing Passkey Notification

    enumerator BK_BT_GAP_KEY_REQ_EVT
    :   Security Simple Pairing Passkey request

    enumerator BK_BT_GAP_READ_RSSI_DELTA_EVT
    :   Read rssi event

    enumerator BK_BT_GAP_CONFIG_EIR_DATA_EVT
    :   Config EIR data event

    enumerator BK_BT_GAP_SET_AFH_CHANNELS_EVT
    :   Set AFH channels event

    enumerator BK_BT_GAP_READ_REMOTE_NAME_EVT
    :   Read Remote Name event

    enumerator BK_BT_GAP_MODE_CHG_EVT

    enumerator BK_BT_GAP_REMOVE_BOND_DEV_COMPLETE_EVT
    :   remove bond device complete event

    enumerator BK_BT_GAP_QOS_CMPL_EVT
    :   QOS complete event

    enumerator BK_BT_GAP_ACL_CONN_CMPL_STAT_EVT
    :   ACL connection complete status event

    enumerator BK_BT_GAP_ACL_DISCONN_CMPL_STAT_EVT
    :   ACL disconnection complete status event

    enumerator BK_BT_GAP_LINK_KEY_NOTIF_EVT
    :   Link Key Notification

    enumerator BK_BT_GAP_LINK_KEY_REQ_EVT
    :   Link Key request

    enumerator BK_BT_GAP_SET_AUTO_SNIFF_CMPL_EVT

    enumerator BK_BT_GAP_EVT_MAX
    :   set auto entry sniff req completed event

enum bk_bt_inq_mode_t
:   Inquiry Mode


    *Values:*

    enumerator BK_BT_INQ_MODE_GENERAL_INQUIRY
    :   General inquiry mode

    enumerator BK_BT_INQ_MODE_LIMITED_INQUIRY
    :   Limited inquiry mode


## 参考链接

> [API 参考：](../../api-reference/bluetooth.md "../../api-reference/bluetooth.md") 介绍蓝牙 API 接口。
>
> [蓝牙开发者指南：](../../developer-guide/bluetooth.md "../../developer-guide/bluetooth.md") 介绍蓝牙开发者指南。
