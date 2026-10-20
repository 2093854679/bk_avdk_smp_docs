---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# 双模 BLE API



## Dual BLE API 分类

Dual BLE API 主要包括以下类型：

按功能划分的 Dual BLE API：
:   - BLE GAP 接口

    - BLE GATT 公共接口

    - BLE GATTC 接口

    - BLE GATTS 接口


## 兼容性和扩展性

Dual BLE API 具备较好的扩展性和向后兼容性。多数 BLE 配置结构体中预留了字段，便于后续扩展。使用这些 API 时，应将预留字段初始化为 0，避免后续新增字段后影响兼容性。


## 编程原则

重要

使用 BLE API 时建议遵循以下原则：
:   - 配置结构体中的预留字段应初始化为 0。

    - 使用 `BK_ERR_CHECK` 检查 BLE API 的返回值。

    - 不确定 API 用法时，优先参考 BLE 示例代码。

    - 不确定配置结构体字段如何初始化时，先使用默认配置宏，再按应用需求修改相关字段。

    - 不建议在 BLE 事件回调中执行耗时操作，可将事件转发到应用任务中处理。


## 事件处理机制

Beken BLE driver 采用事件驱动方式工作。应用通过 BLE API 发起扫描、广播、连接、GATT 访问等操作，并在 BLE 事件回调中获取状态变化和操作结果。


## API 参考


## bk_dm_gap_ble.h

`bk_dm_gap_ble.h` 提供 BLE GAP 的广播、扫描、连接和安全相关接口。


### Header File


- [bluetooth/bk_dm_gap_ble.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gap_ble.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gap_ble.h")


### Functions

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_register_callback([bk_ble_gap_cb_t](#_CPPv415bk_ble_gap_cb_t "bk_ble_gap_cb_t") callback)
:   This function is called to occur gap event, such as scan result.

    参数
    :   **callback** – **[in]** callback function

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_update_conn_params([bk_ble_conn_update_params_t](#_CPPv427bk_ble_conn_update_params_t "bk_ble_conn_update_params_t") *params)
:   Update connection parameters, can only be used when connection is up.

    参数
    :   **params** – **[in]** - connection update parameters

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_pkt_data_len([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_device, uint16_t tx_data_length)
:   This function is to set maximum LE data packet size.

    参数
    :   - **remote_device** – **[in]** - remote device

        - **tx_data_length** – **[in]** - data len

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_rand_addr([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rand_addr)
:   This function sets the static Random Address and Non-Resolvable Private Address for the application.

    参数
    :   **rand_addr** – **[in]** the random address which should be setting

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_config_local_privacy(bool privacy_enable)
:   Enable/disable privacy on the local device.

    参数
    :   **privacy_enable** – **[in]** - enable/disable privacy on remote device.

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_config_local_icon(uint16_t icon)
:   set local gap appearance icon

    参数
    :   **icon** – **[in]** - External appearance value, these values are defined by the Bluetooth SIG, please refer to [https://specificationrefs.bluetooth.com/assigned-values/Appearance%20Values.pdf](https://specificationrefs.bluetooth.com/assigned-values/Appearance%20Values.pdf "https://specificationrefs.bluetooth.com/assigned-values/Appearance%20Values.pdf")

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_update_whitelist(bool add_remove, [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda, [bk_ble_wl_addr_type_t](#_CPPv421bk_ble_wl_addr_type_t "bk_ble_wl_addr_type_t") wl_addr_type)
:   Add or remove device from white list.

    参数
    :   - **add_remove** – **[in]** the value is true if added the ble device to the white list, and false remove to the white list.

        - **remote_bda** – **[in]** the remote device address add/remove from the white list.

        - **wl_addr_type** – **[in]** whitelist address type

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_clear_whitelist(void)
:   Clear all white list.

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_get_whitelist_size(uint16_t *length)
:   Get the whitelist size in the controller.

    参数
    :   **length** – **[out]** the white list length.

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_device_name(const char *name)
:   Set device name to the local device.

    参数
    :   **name** – **[in]** - device name.

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_get_device_name(char *name, uint32_t *size)
:   Get device name of the local device.

    参数
    :   - **name** – **[out]** - device name.

        - **size** – **[inout]** - name output max size, and real size after return.

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_get_local_used_addr([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") local_used_addr, uint8_t *addr_type)
:   This function is called to get local used address and address type. uint8_t *bk_bt_dev_get_address(void) get the public address.

    参数
    :   - **local_used_addr** – **[in]** - current local used ble address (six bytes)

        - **addr_type** – **[in]** - ble address type

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_read_rssi([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_addr)
:   This function is called to read the RSSI of remote device. The address of link policy results are returned in the gap callback function with BK_GAP_BLE_READ_RSSI_COMPLETE_EVT event.

    参数
    :   **remote_addr** – **[in]** : The remote connection device address.

    返回
    :   - BK_OK : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_security_param([bk_ble_sm_param_t](#_CPPv417bk_ble_sm_param_t "bk_ble_sm_param_t") param_type, void *value, uint8_t len)
:   Set a GAP security parameter value. Overrides the default value.

    ```
                   Secure connection is highly recommended to avoid some major
                   vulnerabilities like 'Impersonation in the Pin Pairing Protocol'
                   (CVE-2020-26555) and 'Authentication of the LE Legacy Pairing
                   Protocol'.

                   To accept only `secure connection mode`, it is necessary do as following:

                   1. Set bit `BK_LE_AUTH_REQ_SC_ONLY` (`param_type` is
                   `BK_BLE_SM_AUTHEN_REQ_MODE`), bit `BK_LE_AUTH_BOND` and bit
                   `BK_LE_AUTH_REQ_MITM` is optional as required.

                   2. Set to `BK_BLE_ONLY_ACCEPT_SPECIFIED_AUTH_ENABLE` (`param_type` is
                   `BK_BLE_SM_ONLY_ACCEPT_SPECIFIED_SEC_AUTH`).

                   3. Set to `bk_ble_key_distr_mask_t` (`param_type` is
                   `BK_BLE_SM_SET_INIT_KEY` or `BK_BLE_SM_SET_RSP_KEY`).
    ```

    参数
    :   - **param_type** – **[in]** : the type of the param which to be set

        - **value** – **[in]** : the param value

        - **len** – **[in]** : the length of the param value

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_security_rsp([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, bool accept)
:   Grant security request access.

    参数
    :   - **bd_addr** – **[in]** : BD address of the peer

        - **accept** – **[in]** : accept the security request or not

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_set_encryption([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, [bk_ble_sec_act_t](#_CPPv416bk_ble_sec_act_t "bk_ble_sec_act_t") sec_act)
:   Set a gap parameter value. Use this function to change the default GAP parameter values.

    参数
    :   - **bd_addr** – **[in]** : the address of the peer device need to encryption

        - **sec_act** – **[in]** : This is the security action to indicate what kind of BLE security level is required for the BLE link if the BLE is supported

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_passkey_reply([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, bool accept, uint32_t passkey)
:   Reply the key value to the peer device in the legacy connection stage.

    参数
    :   - **bd_addr** – **[in]** : BD address of the peer

        - **accept** – **[in]** : passkey entry successful or declined.

        - **passkey** – **[in]** : passkey value, must be a 6 digit number, can be lead by 0.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_confirm_reply([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, bool accept)
:   Reply the confirm value to the peer device in the secure connection stage.

    参数
    :   - **bd_addr** – **[in]** : BD address of the peer device

        - **accept** – **[in]** : numbers to compare are the same or different.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_pair_key_reply([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, bool accept, [bk_ble_key_type_t](#_CPPv417bk_ble_key_type_t "bk_ble_key_type_t") type, void *data, uint32_t len)
:   Reply the save key.

    参数
    :   - **bd_addr** – **[in]** : BD address of the peer device

        - **accept** – **[in]** : true or false

        - **type** – **[in]** : key type.

        - **data** – **[in]** : key data, when type is: BK_LE_KEY_LENC, data is [bk_ble_lenc_keys_t](#structbk__ble__lenc__keys__t "#structbk__ble__lenc__keys__t"). When accept is false, data and len will be ignore.

        - **len** – **[in]** : key len

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_remove_bond_device([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   Removes a device from the security database list of peer device. It manages unpairing event while connected.

    参数
    :   **bd_addr** – **[in]** : BD address of the peer device

    返回
    :   - BK_OK : success


        - other : failed

int bk_ble_get_bond_device_num(void)
:   Get the device number from the security database list of peer device. It will return the device bonded number immediately.

    返回
    :   - >= 0 : bonded devices number.


        - BK_FAIL : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_get_bond_device_list(int *dev_num, [bk_ble_bond_dev_t](#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") *dev_list)
:   Get the device from the security database list of peer device. It will return the device bonded information immediately.

    参数
    :   - **dev_num** – **[inout]** Indicate the dev_list array(buffer) size as input. If dev_num is large enough, it means the actual number as output. Suggest that dev_num value equal to [bk_ble_get_bond_device_num()](#group__dm__gap__defines__v1_1ga197bcd6bbaf7eabfddabce66be9fad92 "#group__dm__gap__defines__v1_1ga197bcd6bbaf7eabfddabce66be9fad92").

        - **dev_list** – **[out]** an array(buffer) of `bk_ble_bond_dev_t` type. Use for storing the bonded devices address. The dev_list should be allocated by who call this API.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_connect([bk_gap_create_conn_params_t](#_CPPv427bk_gap_create_conn_params_t "bk_gap_create_conn_params_t") *param)
:   This function is to connect the physical connection of the peer device.


    **Attention**
    :   1. local_addr_type can be BLE_ADDR_TYPE_PUBLIC ~ BLE_ADDR_TYPE_RPA_RANDOM.


    **Attention**
    :   2. if local_addr_type is BLE_ADDR_TYPE_PUBLIC, and initiator_filter_policy policy not enable, host will use local public addr/peer_addr/peer_addr_type to connect.


    **Attention**
    :   3. if local_addr_type is BLE_ADDR_TYPE_RANDOM, and initiator_filter_policy policy not enable, host will use peer_addr/peer_addr_type, random addr that set in bk_ble_gap_set_adv_rand_addr to connect.


    **Attention**
    :   4. if local_addr_type is BLE_ADDR_TYPE_RPA_PUBLIC, host will try search bond list’s nominal addr by peer_addr/peer_addr_type, if found and BK_LE_KEY_PID | BK_LE_KEY_LID present then host will generate RPA addr to connect peer RPA ADV, otherwise see attention 2.


    **Attention**
    :   5. if local_addr_type is BLE_ADDR_TYPE_RPA_RANDOM, host will try search bond list’s nominal addr by peer_addr/peer_addr_type, if found and BK_LE_KEY_PID | BK_LE_KEY_LID present then host will generate RPA addr to connect peer RPA ADV, otherwise see attention 3.

    参数
    :   **param** – **[in]** : connect param

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_disconnect([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_device)
:   This function is to disconnect the physical connection of the peer device.

    参数
    :   **remote_device** – **[in]** : BD address of the peer device

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_cancel_connect(void)
:   This function is to cancel the physical connection that have not connect completed.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_get_current_conn_params([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, [bk_gap_conn_params_t](#_CPPv420bk_gap_conn_params_t "bk_gap_conn_params_t") *conn_params)
:   This function is called to read the connection parameters information of the device.

    参数
    :   - **bd_addr** – **[in]** BD address of the peer device.

        - **conn_params** – **[out]** the connection parameters information

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_gap_ble_set_channels([bk_ble_gap_channels](#_CPPv419bk_ble_gap_channels "bk_ble_gap_channels") channels)
:   BLE set channels.

    参数
    :   **channels** – **[in]** : The n th such field (in the range 0 to 36) contains the value for the link layer channel index n. 0 means channel n is bad. 1 means channel n is unknown. The most significant bits are reserved and shall be set to 0. At least one channel shall be marked as unknown.

    返回
    :   - BK_OK : success


        - BK_ERR_INVALID_STATE: if bluetooth stack is not yet enabled

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_read_phy([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   This function is used to read the current transmitter PHY and receiver PHY on the connection identified by remote address.

    参数
    :   **bd_addr** – **[in]** : BD address of the peer device

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_preferred_default_phy([bk_ble_gap_phy_mask_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") tx_phy_mask, [bk_ble_gap_phy_mask_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") rx_phy_mask)
:   This function is used to allows the Host to specify its preferred values for the transmitter PHY and receiver PHY to be used for all subsequent connections over the LE transport.

    参数
    :   - **tx_phy_mask** – **[in]** : indicates the transmitter PHYs that the Host prefers the Controller to use

        - **rx_phy_mask** – **[in]** : indicates the receiver PHYs that the Host prefers the Controller to use

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_preferred_phy([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr, [bk_ble_gap_all_phys_t](#_CPPv421bk_ble_gap_all_phys_t "bk_ble_gap_all_phys_t") all_phys_mask, [bk_ble_gap_phy_mask_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") tx_phy_mask, [bk_ble_gap_phy_mask_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") rx_phy_mask, [bk_ble_gap_prefer_phy_options_t](#_CPPv431bk_ble_gap_prefer_phy_options_t "bk_ble_gap_prefer_phy_options_t") phy_options)
:   This function is used to set the PHY preferences for the connection identified by the remote address. The Controller might not be able to make the change (e.g. because the peer does not support the requested PHY) or may decide that the current PHY is preferable.

    参数
    :   - **bd_addr** – **[in]** : remote address

        - **all_phys_mask** – **[in]** : a bit field that allows the Host to specify

        - **tx_phy_mask** – **[in]** : a bit field that indicates the transmitter PHYs that the Host prefers the Controller to use

        - **rx_phy_mask** – **[in]** : a bit field that indicates the receiver PHYs that the Host prefers the Controller to use

        - **phy_options** – **[in]** : a bit field that allows the Host to specify options for PHYs

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_adv_rand_addr(uint8_t instance, [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rand_addr)
:   This function is used by the Host to set the random device address specified by the Random_Address parameter.

    参数
    :   - **instance** – **[in]** : Used to identify an advertising set

        - **rand_addr** – **[in]** : Random Device Address

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_adv_params(uint8_t instance, const [bk_ble_gap_ext_adv_params_t](#_CPPv427bk_ble_gap_ext_adv_params_t "bk_ble_gap_ext_adv_params_t") *params)
:   This function is used by the Host to set the advertising parameters.


    **Attention**
    :   1. local_addr_type can be BLE_ADDR_TYPE_PUBLIC ~ BLE_ADDR_TYPE_RPA_RANDOM.


    **Attention**
    :   2. if local_addr_type is BLE_ADDR_TYPE_PUBLIC, host will use public addr to send adv.


    **Attention**
    :   3. if local_addr_type is BLE_ADDR_TYPE_RANDOM, host will use random addr that set in bk_ble_gap_set_adv_rand_addr to send adv.


    **Attention**
    :   4. if local_addr_type is BLE_ADDR_TYPE_RPA_PUBLIC, host will try search bond list by peer_addr/peer_addr_type, if found and BK_LE_KEY_PID | BK_LE_KEY_LID present then host will generate RPA addr to send ADV, otherwise see attention 2.


    **Attention**
    :   5. if local_addr_type is BLE_ADDR_TYPE_RPA_RANDOM, host will try search bond list by peer_addr/peer_addr_type, if found and BK_LE_KEY_PID | BK_LE_KEY_LID present then host will generate RPA addr to send ADV, otherwise see attention 3.

    参数
    :   - **instance** – **[in]** : identifies the advertising set whose parameters are being configured.

        - **params** – **[in]** : advertising parameters

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_adv_data([bk_ble_adv_data_t](#_CPPv417bk_ble_adv_data_t "bk_ble_adv_data_t") *adv_data)
:   This function is used to set the data used in advertising PDUs that have a data field.

    参数
    :   - **instance** – **[in]** : identifies the advertising set whose data are being configured

        - **length** – **[in]** : data length

        - **data** – **[in]** : data information

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_adv_data_raw(uint8_t instance, uint16_t length, const uint8_t *data)
:   This function is used to set the data used in advertising PDUs that have a data field.

    参数
    :   - **instance** – **[in]** : identifies the advertising set whose data are being configured

        - **length** – **[in]** : data length

        - **data** – **[in]** : data information

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_scan_rsp_data_raw(uint8_t instance, uint16_t length, const uint8_t *scan_rsp_data)
:   This function is used to provide scan response data used in scanning response PDUs.

    参数
    :   - **instance** – **[in]** : identifies the advertising set whose response data are being configured.

        - **length** – **[in]** : responsedata length

        - **scan_rsp_data** – **[in]** : response data information

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_adv_start(uint8_t num_adv, const [bk_ble_gap_ext_adv_t](#_CPPv420bk_ble_gap_ext_adv_t "bk_ble_gap_ext_adv_t") *ext_adv)
:   This function is used to request the Controller to enable one or more advertising sets using the advertising sets identified by the instance parameter.

    参数
    :   - **num_adv** – **[in]** : Number of advertising sets to enable or disable

        - **ext_adv** – **[in]** : adv parameters

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_adv_stop(uint8_t num_adv, const uint8_t *ext_adv_inst)
:   This function is used to request the Controller to disable one or more advertising sets using the advertising sets identified by the instance parameter.

    参数
    :   - **num_adv** – **[in]** : Number of advertising sets to enable or disable

        - **ext_adv_inst** – **[in]** : ext adv instance

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_adv_set_remove(uint8_t instance)
:   This function is used to remove an advertising set from the Controller.

    参数
    :   **instance** – **[in]** : Used to identify an advertising set

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_adv_set_clear(void)
:   This function is used to remove all existing advertising sets from the Controller.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_periodic_adv_params(uint8_t instance, const [bk_ble_gap_periodic_adv_params_t](#_CPPv432bk_ble_gap_periodic_adv_params_t "bk_ble_gap_periodic_adv_params_t") *params)
:   This function is used by the Host to set the parameters for periodic advertising.

    参数
    :   - **instance** – **[in]** : identifies the advertising set whose periodic advertising parameters are being configured.

        - **params** – **[in]** : periodic adv parameters

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_periodic_adv_data_raw(uint8_t instance, uint16_t length, const uint8_t *data)
:   This function is used to set the data used in periodic advertising PDUs.

    参数
    :   - **instance** – **[in]** : identifies the advertising set whose periodic advertising parameters are being configured.

        - **length** – **[in]** : the length of periodic data

        - **data** – **[in]** : periodic data information

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_periodic_adv_start(uint8_t instance)
:   This function is used to request the Controller to enable the periodic advertising for the advertising set specified.

    参数
    :   **instance** – **[in]** : Used to identify an advertising set

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_periodic_adv_stop(uint8_t instance)
:   This function is used to request the Controller to disable the periodic advertising for the advertising set specified.

    参数
    :   **instance** – **[in]** : Used to identify an advertising set

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_periodic_adv_create_sync(const [bk_ble_gap_periodic_adv_sync_params_t](#_CPPv437bk_ble_gap_periodic_adv_sync_params_t "bk_ble_gap_periodic_adv_sync_params_t") *params)
:   This function is used to synchronize with periodic advertising from an advertiser and begin receiving periodic advertising packets.

    参数
    :   **params** – **[in]** : sync parameters

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_periodic_adv_sync_cancel(void)
:   This function is used to cancel the LE_Periodic_Advertising_Create_Sync command while it is pending.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_periodic_adv_sync_terminate(uint16_t sync_handle)
:   This function is used to stop reception of the periodic advertising identified by the Sync Handle parameter.

    参数
    :   **sync_handle** – **[in]** : identify the periodic advertiser

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_periodic_adv_add_dev_to_list([bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr_type, [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, uint8_t sid)
:   This function is used to add a single device to the Periodic Advertiser list stored in the Controller.

    参数
    :   - **addr_type** – **[in]** : address type

        - **addr** – **[in]** : Device Address

        - **sid** – **[in]** : Advertising SID subfield in the ADI field used to identify the Periodic Advertising

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_periodic_adv_remove_dev_from_list([bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr_type, [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, uint8_t sid)
:   This function is used to remove one device from the list of Periodic Advertisers stored in the Controller. Removals from the Periodic Advertisers List take effect immediately.

    参数
    :   - **addr_type** – **[in]** : address type

        - **addr** – **[in]** : Device Address

        - **sid** – **[in]** : Advertising SID subfield in the ADI field used to identify the Periodic Advertising

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_periodic_adv_clear_dev(void)
:   This function is used to remove all devices from the list of Periodic Advertisers in the Controller.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_set_scan_params(const [bk_ble_ext_scan_params_t](#_CPPv424bk_ble_ext_scan_params_t "bk_ble_ext_scan_params_t") *params)
:   This function is used to set the extended scan parameters to be used on the advertising channels.

    参数
    :   **params** – **[in]** : scan parameters

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_start_scan(uint32_t duration, uint16_t period)
:   This function is used to enable scanning.

    参数
    :   - **duration** – **[in]** : Scan duration

        - **period** – **[in]** : Time interval from when the Controller started its last Scan Duration until it begins the subsequent Scan Duration.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_stop_scan(void)
:   This function is used to disable scanning.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_prefer_connect_params_set([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, [bk_ble_gap_phy_mask_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") phy_mask, const [bk_ble_gap_conn_params_t](#_CPPv424bk_ble_gap_conn_params_t "bk_ble_gap_conn_params_t") *phy_1m_conn_params, const [bk_ble_gap_conn_params_t](#_CPPv424bk_ble_gap_conn_params_t "bk_ble_gap_conn_params_t") *phy_2m_conn_params, const [bk_ble_gap_conn_params_t](#_CPPv424bk_ble_gap_conn_params_t "bk_ble_gap_conn_params_t") *phy_coded_conn_params)
:   This function is used to set aux connection parameters.

    参数
    :   - **addr** – **[in]** : device address

        - **phy_mask** – **[in]** : indicates the PHY(s) on which the advertising packets should be received on the primary advertising channel and the PHYs for which connection parameters have been specified.

        - **phy_1m_conn_params** – **[in]** : Scan connectable advertisements on the LE 1M PHY. Connection parameters for the LE 1M PHY are provided.

        - **phy_2m_conn_params** – **[in]** : Connection parameters for the LE 2M PHY are provided.

        - **phy_coded_conn_params** – **[in]** : Scan connectable advertisements on the LE Coded PHY. Connection parameters for the LE Coded PHY are provided.

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_create_bond([bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr)
:   This function is used to create bond to peer, this function must used after connected.

    参数
    :   **bd_addr** – **[in]** : peer address

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_bond_dev_list_operation([bk_gap_bond_dev_list_operation_t](#_CPPv432bk_gap_bond_dev_list_operation_t "bk_gap_bond_dev_list_operation_t") op, [bk_ble_bond_dev_t](#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") *device)
:   This function is used to add, remove or clean bond dev info. BK_BLE_GAP_BOND_DEV_LIST_OPERATEION_COMPLETE_EVT evt will report when completed.


    **Attention**
    :   1. Because app layer save bond info, when ble power on, app layer must add bond dev info one by one.


    **Attention**
    :   2. When app layer remove bond info from it self storage, app layer should call BK_GAP_BOND_DEV_LIST_OPERATION_REMOVE or BK_GAP_BOND_DEV_LIST_OPERATION_CLEAN after it done.


    **Attention**
    :   3. This func can’t be call when ble connection/adv/scan is exist.

    参数
    :   - **op** – **[in]** : operation

        - **device** – **[in]** : device info

    返回
    :   - BK_OK : success


        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gap_generate_rpa(uint8_t *irk)
:   This function is used to generate rpa. BK_BLE_GAP_GENERATE_RPA_COMPLETE_EVT evt will report when completed.

    参数
    :   **irk** – **[in]** : the key which used to generate rpa, when this argument is NULL, host will use current local irk to generate. If local irk is not exist(suchas ir not set), will return fail.

    返回
    :   - BK_OK : success


        - other : failed


## bk_dm_gattc.h

`bk_dm_gattc.h` 提供 BLE GATT Client 发现、读写、订阅和事件处理接口。


### Header File


- [bluetooth/bk_dm_gattc.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gattc.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gattc.h")


### Functions

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_register_callback([bk_gattc_cb_t](#_CPPv413bk_gattc_cb_t "bk_gattc_cb_t") callback)
:   This function is called to register application callbacks with GATTC module.

    参数
    :   **callback** – **[in]** : pointer to the application callback function.

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_app_register(uint16_t app_id)
:   This function is called to register application callbacks with GATTC module.

    参数
    :   **app_id** – **[in]** : Application Identify (UUID), for different application

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_app_unregister([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if)
:   This function is called to unregister an application from GATTC module.

    参数
    :   **gattc_if** – **[in]** Gatt client access interface.

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_send_mtu_req([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id)
:   Configure the MTU size in the GATT channel. This can be done only once per connection. Before using, use [bk_ble_gatt_set_local_mtu()](#group__dm__gatt__common__functions__v1_1ga07d73be77fe528eeaa17df45fb6d4efe "#group__dm__gatt__common__functions__v1_1ga07d73be77fe528eeaa17df45fb6d4efe") to configure the local MTU size.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** connection ID.

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_read_char([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, uint16_t handle, [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req)
:   This function is called to read a service’s characteristics of the given characteristic handle.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** : connection ID.

        - **handle** – **[in]** : characteritic handle to read.

        - **auth_req** – **[in]** : authenticate request type

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_read_by_type([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, uint16_t start_handle, uint16_t end_handle, [bk_bt_uuid_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") *uuid, [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req)
:   This function is called to read a service’s characteristics of the given characteristic UUID.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** : connection ID.

        - **start_handle** – **[in]** : the attribute start handle.

        - **end_handle** – **[in]** : the attribute end handle

        - **uuid** – **[in]** : The UUID of attribute which will be read.

        - **auth_req** – **[in]** : authenticate request type

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_read_multiple([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, [bk_gattc_multi_t](#_CPPv416bk_gattc_multi_t "bk_gattc_multi_t") *read_multi, [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req)
:   This function is called to read multiple characteristic or characteristic descriptors.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** : connection ID.

        - **read_multi** – **[in]** : pointer to the read multiple parameter.

        - **auth_req** – **[in]** : authenticate request type

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_read_char_descr([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, uint16_t handle, [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req)
:   This function is called to read a characteristics descriptor.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** : connection ID.

        - **handle** – **[in]** : descriptor handle to read.

        - **auth_req** – **[in]** : authenticate request type

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_write_char([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, uint16_t handle, uint16_t value_len, uint8_t *value, [bk_gatt_write_type_t](#_CPPv420bk_gatt_write_type_t "bk_gatt_write_type_t") write_type, [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req)
:   This function is called to write characteristic value.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** : connection ID.

        - **handle** – **[in]** : characteristic handle to write.

        - **value_len** – **[in]** length of the value to be written.

        - **value** – **[in]** : the value to be written.

        - **write_type** – **[in]** : the type of attribute write operation.

        - **auth_req** – **[in]** : authentication request.

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_write_char_descr([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, uint16_t handle, uint16_t value_len, uint8_t *value, [bk_gatt_write_type_t](#_CPPv420bk_gatt_write_type_t "bk_gatt_write_type_t") write_type, [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req)
:   This function is called to write characteristic descriptor value.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** : connection ID

        - **handle** – **[in]** : descriptor handle to write.

        - **value_len** – **[in]** length of the value to be written.

        - **value** – **[in]** : the value to be written.

        - **write_type** – **[in]** : the type of attribute write operation.

        - **auth_req** – **[in]** : authentication request.

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_prepare_write([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, uint16_t handle, uint16_t offset, uint16_t value_len, uint8_t *value, [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req)
:   This function is called to prepare write a characteristic value.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** : connection ID.

        - **handle** – **[in]** : characteristic handle to prepare write.

        - **offset** – **[in]** : offset of the write value.

        - **value_len** – **[in]** length of the value to be written.

        - **value** – **[in]** : the value to be written.

        - **auth_req** – **[in]** : authentication request.

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_prepare_write_char_descr([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, uint16_t handle, uint16_t offset, uint16_t value_len, uint8_t *value, [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req)
:   This function is called to prepare write a characteristic descriptor value.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** : connection ID.

        - **handle** – **[in]** : characteristic descriptor handle to prepare write.

        - **offset** – **[in]** : offset of the write value.

        - **value_len** – **[in]** length of the value to be written.

        - **value** – **[in]** : the value to be written.

        - **auth_req** – **[in]** : authentication request.

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_execute_write([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, bool is_execute)
:   This function is called to execute write a prepare write sequence.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **conn_id** – **[in]** : connection ID.

        - **is_execute** – **[in]** : execute or cancel.

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_discover([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, uint16_t conn_id, [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req)
:   Triggle a discovery of the remote device.

    参数
    :   - **gattc_if** – **[in]** Gatt client access interface.

        - **handle** – **[in]** : GATT characteristic handle.

        - **auth_req** – **[in]** : authentication request.

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed


### Unions

union bk_ble_gattc_cb_param_t
:   *#include <bk_dm_gattc.h>*

    Gatt client callback parameters union.

    Public Members

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_reg_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t19gattc_reg_evt_paramE "bk_ble_gattc_cb_param_t::gattc_reg_evt_param") reg
    :   Gatt client callback param of BK_GATTC_REG_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_cfg_mtu_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_paramE "bk_ble_gattc_cb_param_t::gattc_cfg_mtu_evt_param") cfg_mtu
    :   Gatt client callback param of BK_GATTC_CFG_MTU_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_read_char_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_paramE "bk_ble_gattc_cb_param_t::gattc_read_char_evt_param") read
    :   Gatt client callback param of BK_GATTC_READ_CHAR_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_write_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t21gattc_write_evt_paramE "bk_ble_gattc_cb_param_t::gattc_write_evt_param") write
    :   Gatt client callback param of BK_GATTC_WRITE_DESCR_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_exec_cmpl_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_paramE "bk_ble_gattc_cb_param_t::gattc_exec_cmpl_evt_param") exec_cmpl
    :   Gatt client callback param of BK_GATTC_EXEC_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_notify_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t22gattc_notify_evt_paramE "bk_ble_gattc_cb_param_t::gattc_notify_evt_param") notify
    :   Gatt client callback param of BK_GATTC_NOTIFY_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_srvc_chg_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t24gattc_srvc_chg_evt_paramE "bk_ble_gattc_cb_param_t::gattc_srvc_chg_evt_param") srvc_chg
    :   Gatt client callback param of BK_GATTC_SRVC_CHG_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_connect_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t23gattc_connect_evt_paramE "bk_ble_gattc_cb_param_t::gattc_connect_evt_param") connect
    :   Gatt client callback param of BK_GATTC_CONNECT_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_disconnect_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_paramE "bk_ble_gattc_cb_param_t::gattc_disconnect_evt_param") disconnect
    :   Gatt client callback param of BK_GATTC_DISCONNECT_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_dis_srvc_cmpl_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_srvc_cmpl_evt_param") dis_srvc_cmpl
    :   Gatt client callback param of BK_GATTC_DIS_SRVC_CMPL_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_dis_res_service_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param") dis_res_service
    :   Gatt client callback param of BK_GATTC_DIS_RES_SERVICE_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_dis_res_char_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param") dis_res_char
    :   Gatt client callback param of BK_GATTC_DIS_RES_CHAR_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_dis_res_char_desc_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param") dis_res_char_desc
    :   Gatt client callback param of BK_GATTC_DIS_RES_CHAR_DESC_EVT

    struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_read_by_type_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_paramE "bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param") read_by_type

    struct gattc_cfg_mtu_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_CFG_MTU_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t conn_id
        :   Connection id

        uint16_t mtu
        :   MTU size

    struct gattc_connect_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_CONNECT_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        uint8_t link_role
        :   Link role : master role = 0 ; slave role = 1

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda
        :   Remote bluetooth device address

        [bk_gatt_conn_params_t](#_CPPv421bk_gatt_conn_params_t "bk_gatt_conn_params_t") conn_params
        :   current connection parameters

    struct gattc_dis_res_char_desc_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_DIS_RES_CHAR_DESC_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        uint16_t char_handle
        :   which char handle own this desc

        uint16_t desc_handle
        :   desc handle

        [bk_gatt_id_t](#_CPPv412bk_gatt_id_t "bk_gatt_id_t") uuid

        struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_dis_res_char_desc_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param")::[anonymous] *array

        uint32_t count

    struct gattc_dis_res_char_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_DIS_RES_CHAR_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        uint16_t start_handle
        :   char start handle

        uint16_t end_handle
        :   char end handle

        uint16_t char_value_handle
        :   char declar value handle

        [bk_gatt_id_t](#_CPPv412bk_gatt_id_t "bk_gatt_id_t") uuid
        :   uuid

        struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_dis_res_char_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param")::[anonymous] *array

        uint32_t count

    struct gattc_dis_res_service_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_DIS_RES_SERVICE_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        uint16_t start_handle
        :   Service start handle

        uint16_t end_handle
        :   Service end handle

        [bk_gatt_id_t](#_CPPv412bk_gatt_id_t "bk_gatt_id_t") srvc_id
        :   Service id, include service uuid and other information

        bool is_primary
        :   True if this is the primary service

        struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_dis_res_service_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param")::[anonymous] *array

        uint32_t count

    struct gattc_dis_srvc_cmpl_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_DIS_SRVC_CMPL_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t conn_id
        :   Connection id

    struct gattc_disconnect_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_DISCONNECT_EVT.

        Public Members

        [bk_gatt_conn_reason_t](#_CPPv421bk_gatt_conn_reason_t "bk_gatt_conn_reason_t") reason
        :   The reason of gatt connection close

        uint16_t conn_id
        :   Connection id

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda
        :   Remote bluetooth device address

    struct gattc_exec_cmpl_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_EXEC_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t conn_id
        :   Connection id

    struct gattc_notify_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_NOTIFY_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda
        :   Remote bluetooth device address

        uint16_t handle
        :   The Characteristic or descriptor handle

        uint16_t value_len
        :   Notify attribute value

        uint8_t *value
        :   Notify attribute value

        bool is_notify
        :   True means notify, false means indicate

    struct gattc_read_by_type_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_READ_BY_TYPE_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t conn_id
        :   Connection id

        uint16_t elem_count

        uint16_t handle

        uint8_t *value
        :   attr handle

        uint16_t len
        :   attr value

        struct [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc_read_by_type_evt_param](#_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_paramE "bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param")::[anonymous] *elem
        :   elem_count

    struct gattc_read_char_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_READ_CHAR_EVT, BK_GATTC_READ_DESCR_EVT, BK_GATTC_READ_MULTIPLE_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t conn_id
        :   Connection id

        uint16_t handle
        :   Characteristic handle, Not used when BK_GATTC_READ_MULTIPLE_EVT

        uint8_t *value
        :   Characteristic value

        uint16_t value_len
        :   Characteristic value length

    struct gattc_reg_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_REG_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t app_id
        :   Application id which input in register API

        [bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatt_if

    struct gattc_srvc_chg_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_SRVC_CHG_EVT.

        Public Members

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda
        :   Remote bluetooth device address

    struct gattc_write_evt_param
    :   *#include <bk_dm_gattc.h>*

        BK_GATTC_WRITE_CHAR_EVT, BK_GATTC_PREP_WRITE_EVT, BK_GATTC_WRITE_DESCR_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t conn_id
        :   Connection id

        uint16_t handle
        :   The Characteristic or descriptor handle

        uint16_t offset
        :   The prepare write offset, this value is valid only when prepare write


### Type Definitions

typedef int32_t (*bk_gattc_cb_t)([bk_gattc_cb_event_t](#_CPPv419bk_gattc_cb_event_t "bk_gattc_cb_event_t") event, [bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc_if, [bk_ble_gattc_cb_param_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t") *param)
:   GATT Client callback function type.

    Param event
    :   : Event type

    Param gattc_if
    :   : GATT client access interface, normally different gattc_if correspond to different profile

    Param param
    :   : Point to callback parameter, currently is union type


### Enumerations

enum bk_gattc_cb_event_t
:   GATT Client callback function events.


    *Values:*

    enumerator BK_GATTC_REG_EVT
    :   When GATT client is registered, the event comes

    enumerator BK_GATTC_UNREG_EVT
    :   When GATT client is unregistered, the event comes

    enumerator BK_GATTC_READ_CHAR_EVT
    :   When GATT characteristic is read, the event comes

    enumerator BK_GATTC_WRITE_CHAR_EVT
    :   When GATT characteristic write operation completes, the event comes

    enumerator BK_GATTC_READ_DESCR_EVT
    :   When GATT characteristic descriptor read completes, the event comes

    enumerator BK_GATTC_WRITE_DESCR_EVT
    :   When GATT characteristic descriptor write completes, the event comes

    enumerator BK_GATTC_NOTIFY_EVT
    :   When GATT notification or indication arrives, the event comes

    enumerator BK_GATTC_PREP_WRITE_EVT
    :   When GATT prepare-write operation completes, the event comes

    enumerator BK_GATTC_EXEC_EVT
    :   When write execution completes, the event comes

    enumerator BK_GATTC_CFG_MTU_EVT
    :   When configuration of MTU completes, the event comes

    enumerator BK_GATTC_CONNECT_EVT
    :   When the ble physical connection is set up, the event comes

    enumerator BK_GATTC_DISCONNECT_EVT
    :   When the ble physical connection disconnected, the event comes

    enumerator BK_GATTC_READ_MULTIPLE_EVT
    :   When the ble characteristic or descriptor multiple complete, the event comes

    enumerator BK_GATTC_DIS_SRVC_CMPL_EVT
    :   When the ble discover service complete, the event comes

    enumerator BK_GATTC_DIS_RES_SERVICE_EVT

    enumerator BK_GATTC_DIS_RES_CHAR_EVT

    enumerator BK_GATTC_DIS_RES_CHAR_DESC_EVT

    enumerator BK_GATTC_READ_BY_TYPE_EVT


## bk_dm_gatts.h

`bk_dm_gatts.h` 提供 BLE GATT Server 服务表创建、属性读写和通知接口。


### Header File


- [bluetooth/bk_dm_gatts.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gatts.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gatts.h")


### Functions

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_register_callback([bk_gatts_cb_t](#_CPPv413bk_gatts_cb_t "bk_gatts_cb_t") callback)
:   This function is called to register application callbacks with BTA GATTS module.

    参数
    :   **callback** – : see bk_gatts_cb_t

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_app_register(uint16_t app_id)
:   This function is called to register application identifier.

    参数
    :   **app_id** – : app id, not used now

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_app_unregister([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts_if)
:   unregister with GATT Server.

    参数
    :   **gatts_if** – **[in]** GATT server access interface

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_create_service([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts_if, [bk_gatt_srvc_id_t](#_CPPv417bk_gatt_srvc_id_t "bk_gatt_srvc_id_t") *service_id, uint16_t num_handle)
:   Create a service. When service creation is done, a callback event BK_GATTS_CREATE_EVT is called to report status and service ID to the profile. The service ID obtained in the callback function needs to be used when adding included service and characteristics/descriptors into the service.

    参数
    :   - **gatts_if** – **[in]** GATT server access interface

        - **service_id** – **[in]** service ID.

        - **num_handle** – **[in]** number of handle requested for this service.

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_create_attr_tab(const [bk_gatts_attr_db_t](#_CPPv418bk_gatts_attr_db_t "bk_gatts_attr_db_t") *gatts_attr_db, [bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts_if, uint16_t count, uint32_t max_attr_count)
:   Create a service attribute tab. Only one service once.

    参数
    :   - **gatts_attr_db** – **[in]** the pointer to the service attr tab. At least has one service declar

        - **gatts_if** – **[in]** GATT server access interface

        - **count** – **[in]** the number of gatts_attr_db.

        - **max_attr_count** – **[in]** max attr num of this service.

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_add_char(uint16_t service_handle, [bk_bt_uuid_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") *char_uuid, [bk_gatt_perm_t](#_CPPv414bk_gatt_perm_t "bk_gatt_perm_t") perm, [bk_gatt_char_prop_t](#_CPPv419bk_gatt_char_prop_t "bk_gatt_char_prop_t") property, [bk_attr_value_t](#_CPPv415bk_attr_value_t "bk_attr_value_t") *char_val, [bk_attr_control_t](#_CPPv417bk_attr_control_t "bk_attr_control_t") *control)
:   This function is called to add a characteristic into a service.

    参数
    :   - **service_handle** – **[in]** service handle to which this included service is to be added.

        - **char_uuid** – **[in]** : Characteristic UUID.

        - **perm** – **[in]** : Characteristic value declaration attribute permission.

        - **property** – **[in]** : Characteristic Properties

        - **char_val** – **[in]** : Characteristic value

        - **control** – **[in]** : attribute response control byte

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_add_char_descr(uint16_t service_handle, uint16_t char_handle, [bk_bt_uuid_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") *descr_uuid, [bk_gatt_perm_t](#_CPPv414bk_gatt_perm_t "bk_gatt_perm_t") perm, [bk_attr_value_t](#_CPPv415bk_attr_value_t "bk_attr_value_t") *char_descr_val, [bk_attr_control_t](#_CPPv417bk_attr_control_t "bk_attr_control_t") *control)
:   This function is called to add characteristic descriptor. When it’s done, a callback event BK_GATTS_ADD_DESCR_EVT is called to report the status and an ID number for this descriptor.

    参数
    :   - **service_handle** – **[in]** service handle to which this characteristic descriptor is to be added.

        - **char_handle** – **[in]** which characteristic descriptor is to be added.

        - **char_handle** – **[in]** which characteristic descriptor is to be added.

        - **perm** – **[in]** descriptor access permission.

        - **descr_uuid** – **[in]** descriptor UUID.

        - **char_descr_val** – **[in]** : Characteristic descriptor value

        - **control** – **[in]** : attribute response control byte

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_start_service(uint16_t service_attr_handle)
:   This function is called to start a service.

    参数
    :   **service_attr_handle** – **[in]** the service handle to be started.

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_stop_service(uint16_t service_attr_handle)
:   This function is called to stop a service.

    参数
    :   **service_attr_handle** – **[in]** the service handle to be stop.

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_send_indicate([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts_if, uint16_t conn_id, uint16_t attr_handle, uint16_t value_len, uint8_t *value, bool need_confirm)
:   Send indicate or notify to GATT client. Set param need_confirm as false will send notification, otherwise indication.

    参数
    :   - **gatts_if** – **[in]** GATT server access interface

        - **conn_id** – **[in]** - connection handle.

        - **attr_handle** – **[in]** - attribute handle to indicate.

        - **value_len** – **[in]** - indicate value length.

        - **value** – **[in]** value to indicate.

        - **need_confirm** – **[in]** - Whether a confirmation is required. false sends a GATT notification, true sends a GATT indication.

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_send_response([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts_if, uint16_t conn_id, uint32_t trans_id, [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status, [bk_gatt_rsp_t](#_CPPv413bk_gatt_rsp_t "bk_gatt_rsp_t") *rsp)
:   This function is called to send a response to a request.

    参数
    :   - **gatts_if** – **[in]** GATT server access interface

        - **conn_id** – **[in]** - connection handle.

        - **trans_id** – **[in]** - Transaction id

        - **status** – **[in]** - response status

        - **rsp** – **[in]** - response data.

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_set_attr_value(uint16_t attr_handle, uint16_t length, const uint8_t *value)
:   This function is called to set the attribute value by the application.

    参数
    :   - **attr_handle** – **[in]** the attribute handle which to be set

        - **length** – **[in]** the value length

        - **value** – **[in]** the pointer to the attribute value

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_get_attr_value(uint16_t attr_handle, uint16_t *length, uint8_t **value)
:   Retrieve attribute value.

    参数
    :   - **attr_handle** – **[in]** Attribute handle.

        - **length** – **[out]** pointer to the attribute value length

        - **value** – **[out]** Pointer to attribute value payload, the value cannot be modified by user

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_send_service_change_indicate([bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts_if, uint16_t conn_id, uint8_t all_connected)
:   Send service change indicate.

    参数
    :   - **gatts_if** – **[in]** GATT server access interface

        - **conn_id** – **[in]** - connection handle.

        - **all_connected** – **[in]** - If all_connected is true then it will send service change indicate to all the connected devices and conn_id will be ignore.

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatts_char_property_operation([bk_gatts_char_property_bit_mask_op_t](#_CPPv436bk_gatts_char_property_bit_mask_op_t "bk_gatts_char_property_bit_mask_op_t") op, uint16_t attr_handle, uint16_t *io)
:   Get or set characteristic property.

    参数
    :   - **op** – **[in]** GATT get or set.

        - **attr_handle** – **[in]** char value attr handle.

        - **[in|out]** – io: input when set and output when set

    返回
    :   - BK_ERR_BLE_SUCCESS : success

        - other : failed


### Unions

union bk_ble_gatts_cb_param_t
:   *#include <bk_dm_gatts.h>*

    Gatt server callback parameters union.

    Public Members

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_reg_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t19gatts_reg_evt_paramE "bk_ble_gatts_cb_param_t::gatts_reg_evt_param") reg
    :   Gatt server callback param of BK_GATTS_REG_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_read_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_paramE "bk_ble_gatts_cb_param_t::gatts_read_evt_param") read
    :   Gatt server callback param of BK_GATTS_READ_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_write_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_paramE "bk_ble_gatts_cb_param_t::gatts_write_evt_param") write
    :   Gatt server callback param of BK_GATTS_WRITE_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_exec_write_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_paramE "bk_ble_gatts_cb_param_t::gatts_exec_write_evt_param") exec_write
    :   Gatt server callback param of BK_GATTS_EXEC_WRITE_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_mtu_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_paramE "bk_ble_gatts_cb_param_t::gatts_mtu_evt_param") mtu
    :   Gatt server callback param of BK_GATTS_MTU_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_conf_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t20gatts_conf_evt_paramE "bk_ble_gatts_cb_param_t::gatts_conf_evt_param") conf
    :   Gatt server callback param of BK_GATTS_CONF_EVT (confirm)

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_create_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t22gatts_create_evt_paramE "bk_ble_gatts_cb_param_t::gatts_create_evt_param") create
    :   Gatt server callback param of BK_GATTS_CREATE_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_add_char_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_paramE "bk_ble_gatts_cb_param_t::gatts_add_char_evt_param") add_char
    :   Gatt server callback param of BK_GATTS_ADD_CHAR_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_add_char_descr_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_paramE "bk_ble_gatts_cb_param_t::gatts_add_char_descr_evt_param") add_char_descr
    :   Gatt server callback param of BK_GATTS_ADD_CHAR_DESCR_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_start_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t21gatts_start_evt_paramE "bk_ble_gatts_cb_param_t::gatts_start_evt_param") start
    :   Gatt server callback param of BK_GATTS_START_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_stop_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t20gatts_stop_evt_paramE "bk_ble_gatts_cb_param_t::gatts_stop_evt_param") stop
    :   Gatt server callback param of BK_GATTS_STOP_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_connect_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t23gatts_connect_evt_paramE "bk_ble_gatts_cb_param_t::gatts_connect_evt_param") connect
    :   Gatt server callback param of BK_GATTS_CONNECT_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_disconnect_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_paramE "bk_ble_gatts_cb_param_t::gatts_disconnect_evt_param") disconnect
    :   Gatt server callback param of BK_GATTS_DISCONNECT_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_rsp_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_paramE "bk_ble_gatts_cb_param_t::gatts_rsp_evt_param") rsp
    :   Gatt server callback param of BK_GATTS_RESPONSE_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_add_attr_tab_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_paramE "bk_ble_gatts_cb_param_t::gatts_add_attr_tab_evt_param") add_attr_tab
    :   Gatt server callback param of BK_GATTS_CREAT_ATTR_TAB_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_set_attr_val_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_paramE "bk_ble_gatts_cb_param_t::gatts_set_attr_val_evt_param") set_attr_val
    :   Gatt server callback param of BK_GATTS_SET_ATTR_VAL_EVT

    struct [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts_send_service_change_evt_param](#_CPPv4N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_paramE "bk_ble_gatts_cb_param_t::gatts_send_service_change_evt_param") service_change
    :   Gatt server callback param of BK_GATTS_SEND_SERVICE_CHANGE_EVT

    struct gatts_add_attr_tab_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_CREAT_ATTR_TAB_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        [bk_bt_uuid_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") svc_uuid
        :   Service uuid type

        uint16_t num_handle
        :   The number of the attribute handle to be added to the gatts database

        uint16_t *handles
        :   The number to the handles

    struct gatts_add_char_descr_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_ADD_CHAR_DESCR_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t attr_handle
        :   Descriptor attribute handle

        uint16_t service_handle
        :   Service attribute handle

        [bk_bt_uuid_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") descr_uuid
        :   Characteristic descriptor uuid

    struct gatts_add_char_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_ADD_CHAR_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t attr_handle
        :   Characteristic attribute handle

        uint16_t service_handle
        :   Service attribute handle

        [bk_bt_uuid_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") char_uuid
        :   Characteristic uuid

    struct gatts_conf_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_CONF_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t conn_id
        :   Connection id

        uint16_t handle
        :   attribute handle. Not used when send indicate

        uint16_t len
        :   The indication or notification value length, len is valid when send notification or indication failed. Not used when indicate

        uint8_t *value
        :   The indication or notification value , value is valid when send notification or indication failed. Not used when indicate

    struct gatts_connect_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_CONNECT_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        uint8_t link_role
        :   Link role : master role = 0 ; slave role = 1

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda
        :   Remote bluetooth device address

        [bk_gatt_conn_params_t](#_CPPv421bk_gatt_conn_params_t "bk_gatt_conn_params_t") conn_params
        :   current Connection parameters. Not used now

    struct gatts_create_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_UNREG_EVT.

        BK_GATTS_CREATE_EVT

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t service_handle
        :   Service attribute handle

        [bk_gatt_srvc_id_t](#_CPPv417bk_gatt_srvc_id_t "bk_gatt_srvc_id_t") service_id
        :   Service id, include service uuid and other information

    struct gatts_disconnect_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_DISCONNECT_EVT.

        Public Members

        [bk_gatt_conn_reason_t](#_CPPv421bk_gatt_conn_reason_t "bk_gatt_conn_reason_t") reason
        :   The reason of gatt connection close

        uint16_t conn_id
        :   Connection id

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda
        :   Remote bluetooth device address

    struct gatts_exec_write_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_EXEC_WRITE_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        uint32_t trans_id
        :   Transaction id

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   The bluetooth device address which been written

        uint8_t exec_write_flag
        :   Execute write flag

        bool need_rsp

    struct gatts_mtu_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_MTU_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        uint16_t mtu
        :   MTU size

    struct gatts_read_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_READ_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        uint32_t trans_id
        :   Transaction id

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   The bluetooth device address which been read

        uint16_t handle
        :   The attribute handle

        uint16_t offset
        :   Offset of the value, if the value is too long

        bool is_long
        :   The value is too long or not

        bool need_rsp
        :   The read operation need to do response

    struct gatts_reg_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_REG_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t app_id
        :   Application id which input in register API, not used now

        [bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatt_if

    struct gatts_rsp_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_RESPONSE_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t handle
        :   Attribute handle which send response

    struct gatts_send_service_change_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_SEND_SERVICE_CHANGE_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t conn_id
        :   Connection id

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda
        :   Remote bluetooth device address

    struct gatts_set_attr_val_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_SET_ATTR_VAL_EVT.

        Public Members

        uint16_t srvc_handle
        :   The service handle

        uint16_t attr_handle
        :   The attribute handle

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

    struct gatts_start_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_START_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t service_handle
        :   Service attribute handle

    struct gatts_stop_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_STOP_EVT.

        Public Members

        [bk_gatt_status_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        uint16_t service_handle
        :   Service attribute handle

    struct gatts_write_evt_param
    :   *#include <bk_dm_gatts.h>*

        BK_GATTS_WRITE_EVT.

        Public Members

        uint16_t conn_id
        :   Connection id

        uint32_t trans_id
        :   Transaction id

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   The bluetooth device address which been written

        uint16_t handle
        :   The attribute handle

        uint16_t offset
        :   Offset of the value, if the value is too long

        bool need_rsp
        :   The write operation need to do response

        bool is_prep
        :   This write operation is prepare write

        uint16_t len
        :   The write attribute value length

        uint8_t *value
        :   The write attribute value


### Macros

BK_GATT_PREP_WRITE_CANCEL
:   Prepare write flag to indicate cancel prepare write

BK_GATT_PREP_WRITE_EXEC
:   Prepare write flag to indicate execute prepare write


### Type Definitions

typedef int32_t (*bk_gatts_cb_t)([bk_gatts_cb_event_t](#_CPPv419bk_gatts_cb_event_t "bk_gatts_cb_event_t") event, [bk_gatt_if_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts_if, [bk_ble_gatts_cb_param_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t") *param)
:   GATT Server callback function type.

    Param event
    :   : Event type

    Param gatts_if
    :   : GATT server access interface, normally different gatts_if correspond to different profile

    Param param
    :   : Point to callback parameter, currently is union type


### Enumerations

enum bk_gatts_cb_event_t
:   GATT Server callback function events.


    *Values:*

    enumerator BK_GATTS_REG_EVT
    :   When register application id, the event comes

    enumerator BK_GATTS_READ_EVT
    :   When gatt client request read operation, the event comes

    enumerator BK_GATTS_WRITE_EVT
    :   When gatt client request write operation, the event comes

    enumerator BK_GATTS_EXEC_WRITE_EVT
    :   When gatt client request execute write, the event comes

    enumerator BK_GATTS_MTU_EVT
    :   When set mtu complete, the event comes

    enumerator BK_GATTS_CONF_EVT
    :   When receive confirm after send notify or indicate, the event comes

    enumerator BK_GATTS_UNREG_EVT
    :   When unregister gatt_if, the event comes

    enumerator BK_GATTS_CREATE_EVT
    :   When create service complete, the event comes

    enumerator BK_GATTS_ADD_CHAR_EVT
    :   When add characteristic complete, the event comes

    enumerator BK_GATTS_ADD_CHAR_DESCR_EVT
    :   When add descriptor complete, the event comes

    enumerator BK_GATTS_START_EVT
    :   When start service complete, the event comes

    enumerator BK_GATTS_STOP_EVT
    :   When stop service complete, the event comes

    enumerator BK_GATTS_CONNECT_EVT
    :   When gatt client connect, the event comes

    enumerator BK_GATTS_DISCONNECT_EVT
    :   When gatt client disconnect, the event comes

    enumerator BK_GATTS_RESPONSE_EVT
    :   When gatt send write/read/error response complete, the event comes

    enumerator BK_GATTS_CREAT_ATTR_TAB_EVT
    :   When gatt create table complete, the event comes

    enumerator BK_GATTS_SET_ATTR_VAL_EVT
    :   When gatt set attr value complete, the event comes

    enumerator BK_GATTS_SEND_SERVICE_CHANGE_EVT
    :   When gatt send service change indication complete, the event comes

enum bk_gatts_char_property_bit_mask_op_t
:   *Values:*

    enumerator BK_GATTS_CHAR_PROPERTY_BIT_MASK_OP_GET

    enumerator BK_GATTS_CHAR_PROPERTY_BIT_MASK_OP_SET


## bk_dm_gatt_common.h

`bk_dm_gatt_common.h` 定义 BLE GATT Client 和 Server 共用的接口与辅助能力。


### Header File


- [bluetooth/bk_dm_gatt_common.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gatt_common.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gatt_common.h")


### Functions

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_gatt_set_local_mtu(uint16_t mtu)
:   This function is called to set local MTU, the function is called before BLE connection.

    参数
    :   **mtu** – **[in]** the size of MTU. Max is 517, min is 23

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_get_hci_handle_from_gatt_conn_id(uint16_t gatt_conn_id, uint16_t *hci_handle)
:   This function is use to get hci_handle from gatt conn id,.


    **Attention**
    :   1. This function only could be used when connection exist.

    参数
    :   - **gatt_conn_id** – **[in]** id from gatts_connect_evt_param/gattc_connect_evt_param

        - **[in|out]** – hci_handle: output hci handle

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed

[ble_err_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk_ble_get_gatt_conn_id_from_hci_handle(uint16_t hci_handle, uint16_t *gatt_conn_id)
:   This function is use to get gatt conn id from hci_handle,.


    **Attention**
    :   1. This function only could be used when connection exist.

    参数
    :   - **hci_handle** – **[in]** hci handle from BK_BLE_GAP_CONNECT_COMPLETE_EVT

        - **[in|out]** – gatt_conn_id: output gatt conn id

    返回
    :   - BK_ERR_BLE_SUCCESS: success

        - other: failed


## API 类型定义


## bk_dm_gap_ble_types.h

`bk_dm_gap_ble_types.h` 定义 BLE GAP 使用的参数、事件和状态类型。


### Header File


- [bluetooth/bk_dm_gap_ble_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gap_ble_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gap_ble_types.h")


### Unions

union bk_ble_key_value_t
:   *#include <bk_dm_gap_ble_types.h>*

    union type of the security key value

    Public Members

    [bk_ble_penc_keys_t](#_CPPv418bk_ble_penc_keys_t "bk_ble_penc_keys_t") penc_key
    :   received peer encryption key

    [bk_ble_pcsrk_keys_t](#_CPPv419bk_ble_pcsrk_keys_t "bk_ble_pcsrk_keys_t") pcsrk_key
    :   received peer device SRK

    [bk_ble_pid_keys_t](#_CPPv417bk_ble_pid_keys_t "bk_ble_pid_keys_t") pid_key
    :   peer device ID key

    [bk_ble_lenc_keys_t](#_CPPv418bk_ble_lenc_keys_t "bk_ble_lenc_keys_t") lenc_key
    :   local encryption reproduction keys LTK = = d1(ER,DIV,0)

    [bk_ble_lcsrk_keys_t](#_CPPv419bk_ble_lcsrk_keys_t "bk_ble_lcsrk_keys_t") lcsrk_key
    :   local device CSRK = d1(ER,DIV,1)

union bk_ble_sec_t
:   *#include <bk_dm_gap_ble_types.h>*

    union associated with ble security

    Public Members

    [bk_ble_sec_key_notif_t](#_CPPv422bk_ble_sec_key_notif_t "bk_ble_sec_key_notif_t") key_notif
    :   passkey notification/req or number compare notification

    [bk_ble_sec_req_t](#_CPPv416bk_ble_sec_req_t "bk_ble_sec_req_t") ble_req
    :   BLE SMP related request

    [bk_ble_local_keys_t](#_CPPv419bk_ble_local_keys_t "bk_ble_local_keys_t") ble_local_keys
    :   BLE local event

    [bk_ble_auth_cmpl_t](#_CPPv418bk_ble_auth_cmpl_t "bk_ble_auth_cmpl_t") auth_cmpl
    :   Authentication complete indication.

union bk_ble_gap_cb_param_t
:   *#include <bk_dm_gap_ble_types.h>*

    Gap callback parameters union.

    Public Members

    [bk_ble_sec_t](#_CPPv412bk_ble_sec_t "bk_ble_sec_t") ble_security
    :   ble gap security union type

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_set_rand_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_set_rand_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_set_rand_cmpl_evt_param") set_rand_addr_cmpl
    :   Event parameter of BK_BLE_GAP_SET_STATIC_RAND_ADDR_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_update_conn_params_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_paramE "bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param") update_conn_params
    :   Event parameter of BK_BLE_GAP_UPDATE_CONN_PARAMS_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_pkt_data_length_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_pkt_data_length_cmpl_evt_param") pkt_data_length_cmpl
    :   Event parameter of BK_BLE_GAP_SET_PKT_LENGTH_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_local_privacy_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_local_privacy_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_local_privacy_cmpl_evt_param") local_privacy_cmpl
    :   Event parameter of BK_BLE_GAP_SET_LOCAL_PRIVACY_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_bond_dev_key_req_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t30ble_bond_dev_key_req_evt_paramE "bk_ble_gap_cb_param_t::ble_bond_dev_key_req_evt_param") bond_key_req_evt
    :   Event parameter of BK_BLE_GAP_BOND_KEY_REQ_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_bond_dev_key_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_paramE "bk_ble_gap_cb_param_t::ble_bond_dev_key_evt_param") bond_dev_key_generate_evt
    :   Event parameter of BK_BLE_GAP_BOND_KEY_GENERATE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_bond_dev_list_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_paramE "bk_ble_gap_cb_param_t::ble_bond_dev_list_evt_param") bond_dev_list_op_cmpl
    :   Event parameter of BK_BLE_GAP_BOND_DEV_LIST_OPERATEION_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_read_rssi_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_read_rssi_cmpl_evt_param") read_rssi_cmpl
    :   Event parameter of BK_BLE_GAP_READ_RSSI_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_update_whitelist_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_update_whitelist_cmpl_evt_param") update_whitelist_cmpl
    :   Event parameter of BK_BLE_GAP_UPDATE_WHITELIST_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_set_channels_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t31ble_set_channels_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_set_channels_cmpl_evt_param") ble_set_channels
    :   Event parameter of BK_BLE_GAP_SET_CHANNELS_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_read_phy_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_read_phy_cmpl_evt_param") read_phy
    :   Event parameter of BK_BLE_GAP_READ_PHY_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_set_perf_def_phy_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_set_perf_def_phy_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_set_perf_def_phy_cmpl_evt_param") set_perf_def_phy
    :   Event parameter of BK_BLE_GAP_SET_PREFERRED_DEFAULT_PHY_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_set_perf_phy_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t31ble_set_perf_phy_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_set_perf_phy_cmpl_evt_param") set_perf_phy
    :   Event parameter of BK_BLE_GAP_SET_PREFERRED_PHY_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_set_rand_addr_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t36ble_adv_set_rand_addr_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_set_rand_addr_cmpl_evt_param") adv_set_rand_addr
    :   Event parameter of BK_BLE_GAP_EXT_ADV_SET_RAND_ADDR_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_params_set_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_adv_params_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_params_set_cmpl_evt_param") adv_params_set
    :   Event parameter of BK_BLE_GAP_EXT_ADV_PARAMS_SET_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_data_set_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t31ble_adv_data_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_data_set_cmpl_evt_param") adv_data_set
    :   Event parameter of BK_BLE_GAP_EXT_ADV_DATA_SET_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_scan_rsp_set_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_adv_scan_rsp_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_scan_rsp_set_cmpl_evt_param") scan_rsp_data_set
    :   Event parameter of BK_BLE_GAP_EXT_SCAN_RSP_DATA_SET_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_data_raw_set_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_adv_data_raw_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_data_raw_set_cmpl_evt_param") adv_data_raw_set
    :   Event parameter of BK_BLE_GAP_EXT_ADV_DATA_SET_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_scan_rsp_data_raw_set_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t40ble_scan_rsp_data_raw_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_scan_rsp_data_raw_set_cmpl_evt_param") scan_rsp_data_raw_set
    :   Event parameter of BK_BLE_GAP_EXT_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_start_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t28ble_adv_start_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_start_cmpl_evt_param") adv_start
    :   Event parameter of BK_BLE_GAP_EXT_ADV_START_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_stop_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_adv_stop_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_stop_cmpl_evt_param") adv_stop
    :   Event parameter of BK_BLE_GAP_EXT_ADV_STOP_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_set_remove_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_adv_set_remove_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_set_remove_cmpl_evt_param") adv_remove
    :   Event parameter of BK_BLE_GAP_ADV_SET_REMOVE_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_set_clear_cmpl_evt_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_adv_set_clear_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_set_clear_cmpl_evt_param") adv_clear
    :   Event parameter of BK_BLE_GAP_ADV_SET_CLEAR_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_periodic_adv_set_params_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t38ble_periodic_adv_set_params_cmpl_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_set_params_cmpl_param") peroid_adv_set_params
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_SET_PARAMS_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_periodic_adv_data_set_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t36ble_periodic_adv_data_set_cmpl_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_data_set_cmpl_param") period_adv_data_set
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_DATA_SET_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_periodic_adv_start_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_start_cmpl_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_start_cmpl_param") period_adv_start
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_START_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_periodic_adv_stop_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_periodic_adv_stop_cmpl_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_stop_cmpl_param") period_adv_stop
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_STOP_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_period_adv_create_sync_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t37ble_period_adv_create_sync_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_create_sync_cmpl_param") period_adv_create_sync
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_CREATE_SYNC_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_period_adv_sync_cancel_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t37ble_period_adv_sync_cancel_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_sync_cancel_cmpl_param") period_adv_sync_cancel
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_SYNC_CANCEL_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_period_adv_sync_terminate_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t40ble_period_adv_sync_terminate_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_sync_terminate_cmpl_param") period_adv_sync_term
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_SYNC_TERMINATE_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_period_adv_add_dev_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_period_adv_add_dev_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_add_dev_cmpl_param") period_adv_add_dev
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_ADD_DEV_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_period_adv_remove_dev_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t36ble_period_adv_remove_dev_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_remove_dev_cmpl_param") period_adv_remove_dev
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_REMOVE_DEV_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_period_adv_clear_dev_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_period_adv_clear_dev_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_clear_dev_cmpl_param") period_adv_clear_dev
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_CLEAR_DEV_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_scan_params_set_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t30ble_scan_params_set_cmpl_paramE "bk_ble_gap_cb_param_t::ble_scan_params_set_cmpl_param") scan_params_set
    :   Event parameter of BK_BLE_GAP_SCAN_PARAMS_SET_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_scan_start_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t25ble_scan_start_cmpl_paramE "bk_ble_gap_cb_param_t::ble_scan_start_cmpl_param") scan_start
    :   Event parameter of BK_BLE_GAP_SCAN_START_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_scan_stop_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t24ble_scan_stop_cmpl_paramE "bk_ble_gap_cb_param_t::ble_scan_stop_cmpl_param") scan_stop
    :   Event parameter of BK_BLE_GAP_SCAN_STOP_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_conn_params_set_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t30ble_conn_params_set_cmpl_paramE "bk_ble_gap_cb_param_t::ble_conn_params_set_cmpl_param") conn_params_set
    :   Event parameter of BK_BLE_GAP_PREFER_CONN_PARAMS_SET_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_adv_terminate_param](#_CPPv4N21bk_ble_gap_cb_param_t23ble_adv_terminate_paramE "bk_ble_gap_cb_param_t::ble_adv_terminate_param") adv_terminate
    :   Event parameter of BK_BLE_GAP_ADV_TERMINATED_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_scan_req_received_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_scan_req_received_paramE "bk_ble_gap_cb_param_t::ble_scan_req_received_param") scan_req_received
    :   Event parameter of BK_BLE_GAP_SCAN_REQ_RECEIVED_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_channel_sel_alg_param](#_CPPv4N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_paramE "bk_ble_gap_cb_param_t::ble_channel_sel_alg_param") channel_sel_alg
    :   Event parameter of BK_BLE_GAP_CHANNEL_SELECT_ALGORITHM_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_periodic_adv_sync_lost_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_periodic_adv_sync_lost_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_sync_lost_param") periodic_adv_sync_lost
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_SYNC_LOST_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_periodic_adv_sync_estab_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param") periodic_adv_sync_estab
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_SYNC_ESTAB_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_phy_update_cmpl_param](#_CPPv4N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_paramE "bk_ble_gap_cb_param_t::ble_phy_update_cmpl_param") phy_update
    :   Event parameter of BK_BLE_GAP_PHY_UPDATE_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_ext_adv_report_param](#_CPPv4N21bk_ble_gap_cb_param_t24ble_ext_adv_report_paramE "bk_ble_gap_cb_param_t::ble_ext_adv_report_param") ext_adv_report
    :   Event parameter of BK_BLE_GAP_EXT_ADV_REPORT_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_periodic_adv_report_param](#_CPPv4N21bk_ble_gap_cb_param_t29ble_periodic_adv_report_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_report_param") period_adv_report
    :   Event parameter of BK_BLE_GAP_PERIODIC_ADV_REPORT_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_connect_complete_param](#_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_paramE "bk_ble_gap_cb_param_t::ble_connect_complete_param") connect_complete
    :   Event parameter of BK_BLE_GAP_CONNECT_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_disconnect_complete_param](#_CPPv4N21bk_ble_gap_cb_param_t29ble_disconnect_complete_paramE "bk_ble_gap_cb_param_t::ble_disconnect_complete_param") disconnect_complete
    :   Event parameter of BK_BLE_GAP_DISCONNECT_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_connect_cancel_param](#_CPPv4N21bk_ble_gap_cb_param_t24ble_connect_cancel_paramE "bk_ble_gap_cb_param_t::ble_connect_cancel_param") connect_cancel
    :   Event parameter of BK_BLE_GAP_CONNECT_CANCEL_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_conntection_update_param_req](#_CPPv4N21bk_ble_gap_cb_param_t32ble_conntection_update_param_reqE "bk_ble_gap_cb_param_t::ble_conntection_update_param_req") update_conn_param_req
    :   Event parameter of BK_BLE_GAP_UPDATE_CONN_PARAMS_REQ_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_set_security_params_cmpl](#_CPPv4N21bk_ble_gap_cb_param_t28ble_set_security_params_cmplE "bk_ble_gap_cb_param_t::ble_set_security_params_cmpl") set_security_params_cmpl
    :   Event parameter of BK_BLE_GAP_SET_SECURITY_PARAMS_COMPLETE_EVT

    struct [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble_generate_rpa_cmpl](#_CPPv4N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmplE "bk_ble_gap_cb_param_t::ble_generate_rpa_cmpl") generate_rpa_cmpl
    :   Event parameter of BK_BLE_GAP_GENERATE_RPA_COMPLETE_EVT

    struct ble_adv_data_raw_set_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_ADV_DATA_RAW_SET_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising data set status

    struct ble_adv_data_set_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_ADV_DATA_SET_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising data set status

    struct ble_adv_params_set_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_ADV_PARAMS_SET_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising parameters set status

    struct ble_adv_scan_rsp_set_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_SCAN_RSP_DATA_SET_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising scan response data set status

    struct ble_adv_set_clear_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_ADV_SET_CLEAR_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate advertising stop operation success status

    struct ble_adv_set_rand_addr_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_ADV_SET_RAND_ADDR_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising random address set status

    struct ble_adv_set_remove_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_ADV_SET_REMOVE_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate advertising stop operation success status

    struct ble_adv_start_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_ADV_START_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate advertising start operation success status

    struct ble_adv_stop_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_ADV_STOP_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate advertising stop operation success status

    struct ble_adv_terminate_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_ADV_TERMINATED_EVT.

        Public Members

        uint8_t status
        :   Indicate adv terminate status

        uint8_t adv_instance
        :   extend advertising handle

        uint16_t conn_idx
        :   connection index

        uint8_t completed_event
        :   the number of completed extend advertising events

    struct ble_bond_dev_key_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_BOND_KEY_GENERATE_EVT.

        Public Members

        [bk_ble_bond_dev_t](#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") bond_dev
        :   bond device Structure

    struct ble_bond_dev_key_req_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_BOND_KEY_REQ_EVT.

        Public Members

        [bk_ble_bond_key_req_t](#_CPPv421bk_ble_bond_key_req_t "bk_ble_bond_key_req_t") key_req
        :   bond device Structure

    struct ble_bond_dev_list_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_BOND_DEV_LIST_OPERATEION_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        [bk_gap_bond_dev_list_operation_t](#_CPPv432bk_gap_bond_dev_list_operation_t "bk_gap_bond_dev_list_operation_t") op
        :   operation id

    struct ble_channel_sel_alg_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_CHANNEL_SELECT_ALGORITHM_EVT.

        Public Members

        uint16_t conn_handle
        :   connection handle

        uint8_t channel_sel_alg
        :   channel selection algorithm

    struct ble_conn_params_set_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PREFER_CONN_PARAMS_SET_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend connection parameters set status

    struct ble_connect_cancel_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_CONNECT_CANCEL_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

    struct ble_connect_complete_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_CONNECT_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda
        :   Remote bluetooth device address

        [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") remote_bda_type

        uint8_t link_role
        :   Link role : master role = 0 ; slave role = 1

        uint16_t conn_intv

        uint16_t conn_latency

        uint16_t supervision_timeout

        uint16_t hci_handle

    struct ble_conntection_update_param_req
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_UPDATE_CONN_PARAMS_REQ_EVT.

        Public Members

        uint8_t can_modify
        :   if true, param can be modify before accept

        [bk_ble_conn_update_params_t](#_CPPv427bk_ble_conn_update_params_t "bk_ble_conn_update_params_t") param

        uint8_t accept

    struct ble_disconnect_complete_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_DISCONNECT_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_bda
        :   Remote bluetooth device address

        [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") remote_bda_type

        uint8_t reason

        uint16_t hci_handle

    struct ble_ext_adv_report_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_ADV_REPORT_EVT.

        Public Members

        [bk_ble_gap_ext_adv_reprot_t](#_CPPv427bk_ble_gap_ext_adv_reprot_t "bk_ble_gap_ext_adv_reprot_t") params
        :   extend advertising report parameters

    struct ble_generate_rpa_cmpl
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_GENERATE_RPA_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr

        [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr_type

    struct ble_local_privacy_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SET_LOCAL_PRIVACY_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the set local privacy operation success status

    struct ble_period_adv_add_dev_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_ADD_DEV_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising device list add status

    struct ble_period_adv_clear_dev_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_CLEAR_DEV_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising device list clean status

    struct ble_period_adv_create_sync_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_CREATE_SYNC_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising create sync status

    struct ble_period_adv_remove_dev_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_REMOVE_DEV_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising device list remove status

    struct ble_period_adv_sync_cancel_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_SYNC_CANCEL_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising sync cancel status

    struct ble_period_adv_sync_terminate_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_SYNC_TERMINATE_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising sync terminate status

    struct ble_periodic_adv_data_set_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_DATA_SET_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising data set status

    struct ble_periodic_adv_report_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_REPORT_EVT.

        Public Members

        [bk_ble_gap_periodic_adv_report_t](#_CPPv432bk_ble_gap_periodic_adv_report_t "bk_ble_gap_periodic_adv_report_t") params
        :   periodic advertising report parameters

    struct ble_periodic_adv_set_params_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_SET_PARAMS_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertisingparameters set status

    struct ble_periodic_adv_start_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_START_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising start status

    struct ble_periodic_adv_stop_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_STOP_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising stop status

    struct ble_periodic_adv_sync_estab_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_SYNC_ESTAB_EVT.

        Public Members

        uint8_t status
        :   periodic advertising sync status

        uint16_t sync_handle
        :   periodic advertising sync handle

        uint8_t sid
        :   periodic advertising sid

        [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") adv_addr_type
        :   periodic advertising address type

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") adv_addr
        :   periodic advertising address

        [bk_ble_gap_phy_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") adv_phy
        :   periodic advertising phy type

        uint16_t period_adv_interval
        :   periodic advertising interval

        uint8_t adv_clk_accuracy
        :   periodic advertising clock accuracy

    struct ble_periodic_adv_sync_lost_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PERIODIC_ADV_SYNC_LOST_EVT.

        Public Members

        uint16_t sync_handle
        :   sync handle

    struct ble_phy_update_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_PHY_UPDATE_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   phy update status

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   address

        [bk_ble_gap_phy_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") tx_phy
        :   tx phy type

        [bk_ble_gap_phy_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") rx_phy
        :   rx phy type

    struct ble_pkt_data_length_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SET_PKT_LENGTH_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the set pkt data length operation success status

        [bk_ble_pkt_data_length_params_t](#_CPPv431bk_ble_pkt_data_length_params_t "bk_ble_pkt_data_length_params_t") params
        :   pkt data length value

    struct ble_read_phy_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_READ_PHY_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   read phy complete status

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   read phy address

        [bk_ble_gap_phy_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") tx_phy
        :   tx phy type

        [bk_ble_gap_phy_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") rx_phy
        :   rx phy type

    struct ble_read_rssi_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_READ_RSSI_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the read adv tx power operation success status

        int8_t rssi
        :   The ble remote device rssi value, the range is from -127 to 20, the unit is dbm, if the RSSI cannot be read, the RSSI metric shall be set to 127.

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote_addr
        :   The remote device address

    struct ble_scan_params_set_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SCAN_PARAMS_SET_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising parameters set status

    struct ble_scan_req_received_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SCAN_REQ_RECEIVED_EVT.

        Public Members

        uint8_t adv_instance
        :   extend advertising handle

        [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") scan_addr_type
        :   scanner address type

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") scan_addr
        :   scanner address

    struct ble_scan_rsp_data_raw_set_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_EXT_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising scan response data set status

    struct ble_scan_start_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SCAN_START_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising start status

    struct ble_scan_stop_cmpl_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SCAN_STOP_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising stop status

    struct ble_set_channels_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SET_CHANNELS_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   BLE set channel status

    struct ble_set_perf_def_phy_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SET_PREFERRED_DEFAULT_PHY_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate perf default phy set status

    struct ble_set_perf_phy_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SET_PREFERRED_PHY_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate perf phy set status

    struct ble_set_rand_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SET_STATIC_RAND_ADDR_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate set static rand address operation success status

    struct ble_set_security_params_cmpl
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_SET_SECURITY_PARAMS_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        [bk_ble_sm_param_t](#_CPPv417bk_ble_sm_param_t "bk_ble_sm_param_t") param

    struct ble_update_conn_params_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_UPDATE_CONN_PARAMS_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate update connection parameters success status

        [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   Bluetooth device address

        uint16_t min_int
        :   Min connection interval

        uint16_t max_int
        :   Max connection interval

        uint16_t latency
        :   Slave latency for the connection in number of connection events. Range: 0x0000 to 0x01F3

        uint16_t conn_int
        :   Current connection interval

        uint16_t timeout
        :   Supervision timeout for the LE Link. Range: 0x000A to 0x0C80. Mandatory Range: 0x000A to 0x0C80 Time = N * 10 msec

    struct ble_update_whitelist_cmpl_evt_param
    :   *#include <bk_dm_gap_ble_types.h>*

        BK_BLE_GAP_UPDATE_WHITELIST_COMPLETE_EVT.

        Public Members

        [bk_bt_status_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the add or remove whitelist operation success status

        [bk_ble_wl_operation_t](#_CPPv421bk_ble_wl_operation_t "bk_ble_wl_operation_t") wl_operation
        :   The value is BK_BLE_WHITELIST_ADD if add address to whitelist operation success, BK_BLE_WHITELIST_REMOVE if remove address from the whitelist operation success


### Structures

struct bk_ble_adv_params_t
:   Advertising parameters.

    Public Members

    uint16_t adv_int_min
    :   Minimum advertising interval for undirected and low duty cycle directed advertising. Range: 0x0020 to 0x4000 Default: N = 0x0800 (1.28 second) Time = N * 0.625 msec Time Range: 20 ms to 10.24 sec

    uint16_t adv_int_max
    :   Maximum advertising interval for undirected and low duty cycle directed advertising. Range: 0x0020 to 0x4000 Default: N = 0x0800 (1.28 second) Time = N * 0.625 msec Time Range: 20 ms to 10.24 sec Advertising max interval

    [bk_ble_adv_type_t](#_CPPv417bk_ble_adv_type_t "bk_ble_adv_type_t") adv_type
    :   Advertising type

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") own_addr_type
    :   Owner bluetooth device address type

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") peer_addr
    :   Peer device bluetooth device address

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") peer_addr_type
    :   Peer device bluetooth device address type, only support public address type and random address type

    [bk_ble_adv_channel_t](#_CPPv420bk_ble_adv_channel_t "bk_ble_adv_channel_t") channel_map
    :   Advertising channel map

    [bk_ble_adv_filter_t](#_CPPv419bk_ble_adv_filter_t "bk_ble_adv_filter_t") adv_filter_policy
    :   Advertising filter policy

struct bk_ble_adv_data_t
:   Advertising data content, according to “Supplement to the Bluetooth Core Specification”.

    Public Members

    bool set_scan_rsp
    :   Set this advertising data as scan response or not

    bool include_name
    :   Advertising data include device name or not

    bool include_txpower
    :   Advertising data include TX power

    int min_interval
    :   Advertising data show slave preferred connection min interval. The connection interval in the following manner: connIntervalmin = Conn_Interval_Min * 1.25 ms Conn_Interval_Min range: 0x0006 to 0x0C80 Value of 0xFFFF indicates no specific minimum. Values not defined above are reserved for future use.

    int max_interval
    :   Advertising data show slave preferred connection max interval. The connection interval in the following manner: connIntervalmax = Conn_Interval_Max * 1.25 ms Conn_Interval_Max range: 0x0006 to 0x0C80 Conn_Interval_Max shall be equal to or greater than the Conn_Interval_Min. Value of 0xFFFF indicates no specific maximum. Values not defined above are reserved for future use.

    int appearance
    :   External appearance of device

    uint16_t manufacturer_len
    :   Manufacturer data length

    uint8_t *p_manufacturer_data
    :   Manufacturer data point

    uint16_t service_data_len
    :   Service data length

    uint8_t *p_service_data
    :   Service data point

    uint16_t service_uuid_len
    :   Service uuid length

    uint8_t *p_service_uuid
    :   Service uuid array point

    uint8_t flag
    :   Advertising flag of discovery mode, see BLE_ADV_DATA_FLAG detail

struct bk_ble_scan_params_t
:   Ble scan parameters.

    Public Members

    [bk_ble_scan_type_t](#_CPPv418bk_ble_scan_type_t "bk_ble_scan_type_t") scan_type
    :   Scan type

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") own_addr_type
    :   Owner address type

    [bk_ble_scan_filter_t](#_CPPv420bk_ble_scan_filter_t "bk_ble_scan_filter_t") scan_filter_policy
    :   Scan filter policy

    uint16_t scan_interval
    :   Scan interval. This is defined as the time interval from when the Controller started its last LE scan until it begins the subsequent LE scan. Range: 0x0004 to 0x4000 Default: 0x0010 (10 ms) Time = N * 0.625 msec Time Range: 2.5 msec to 10.24 seconds

    uint16_t scan_window
    :   Scan window. The duration of the LE scan. LE_Scan_Window shall be less than or equal to LE_Scan_Interval Range: 0x0004 to 0x4000 Default: 0x0010 (10 ms) Time = N * 0.625 msec Time Range: 2.5 msec to 10240 msec

    [bk_ble_scan_duplicate_t](#_CPPv423bk_ble_scan_duplicate_t "bk_ble_scan_duplicate_t") scan_duplicate
    :   The Scan_Duplicates parameter controls whether the Link Layer should filter out duplicate advertising reports (BLE_SCAN_DUPLICATE_ENABLE) to the Host, or if the Link Layer should generate advertising reports for each packet received

struct bk_gap_create_conn_params_t
:   create connection param

    Public Members

    uint16_t scan_interval
    :   scan interval, unit in 0.625ms

    uint16_t scan_window
    :   scan window, unit in 0.625ms

    uint8_t initiator_filter_policy
    :   policy that how to use white list. 0 means not used, 1 means only connect device that in white list

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") local_addr_type
    :   local address type

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") peer_addr
    :   peer addr

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") peer_addr_type
    :   Peer address type, only BLE_ADDR_TYPE_PUBLIC or BLE_ADDR_TYPE_RANDOM available

    uint16_t conn_interval_min
    :   conn min interval, unit in 1.25ms, Range: 7.5ms to 4s

    uint16_t conn_interval_max
    :   conn max interval, unit in 1.25ms, Range: 7.5ms to 4s

    uint16_t conn_latency
    :   latency Range: 0x0000 to 0x01F3

    uint16_t supervision_timeout
    :   conn timeout, unit in 10ms Range: 100ms to 32s

    uint16_t min_ce
    :   minimum length of connection event recommended, unit in 0.625ms Range: 0x0000 to 0xFFFF

    uint16_t max_ce
    :   maximum length of connection event recommended, unit in 0.625ms Range: 0x0000 to 0xFFFF

struct bk_gap_conn_params_t
:   connection parameters information

    Public Members

    uint16_t interval
    :   connection interval

    uint16_t latency
    :   Slave latency for the connection in number of connection events. Range: 0x0000 to 0x01F3

    uint16_t timeout
    :   Supervision timeout for the LE Link. Range: 0x000A to 0x0C80. Mandatory Range: 0x000A to 0x0C80 Time = N * 10 msec Time Range: 100 msec to 32 seconds

struct bk_ble_conn_update_params_t
:   Connection update parameters.

    Public Members

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
    :   Bluetooth device address

    uint16_t min_int
    :   Min connection interval

    uint16_t max_int
    :   Max connection interval

    uint16_t latency
    :   Slave latency for the connection in number of connection events. Range: 0x0000 to 0x01F3

    uint16_t timeout
    :   Supervision timeout for the LE Link. Range: 0x000A to 0x0C80. Mandatory Range: 0x000A to 0x0C80 Time = N * 10 msec Time Range: 100 msec to 32 seconds

struct bk_ble_pkt_data_length_params_t
:   BLE pkt date length keys.

    Public Members

    uint16_t rx_len
    :   pkt rx data length value

    uint16_t tx_len
    :   pkt tx data length value

struct bk_ble_penc_keys_t
:   BLE encryption keys.

    Public Members

    [bk_bt_octet16_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") ltk
    :   The long term key

    [bk_bt_octet8_t](#_CPPv414bk_bt_octet8_t "bk_bt_octet8_t") rand
    :   The random number

    uint16_t ediv
    :   The ediv value

    uint8_t sec_level
    :   The security level of the security link, see bk_ble_security_level_t

    uint8_t key_size
    :   The key size(7~16) of the security link

struct bk_ble_pcsrk_keys_t
:   BLE CSRK keys.

    Public Members

    uint32_t counter
    :   The counter

    [bk_bt_octet16_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") csrk
    :   The csrk key

    uint8_t sec_level
    :   The security level see bk_ble_security_level_t

struct bk_ble_pid_keys_t
:   BLE pid keys.

    Public Members

    [bk_bt_octet16_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") irk
    :   The irk value

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr_type
    :   The address type

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") static_addr
    :   The static address

struct bk_ble_lenc_keys_t
:   BLE Encryption reproduction keys.

    Public Members

    [bk_bt_octet16_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") ltk
    :   The long term key

    [bk_bt_octet8_t](#_CPPv414bk_bt_octet8_t "bk_bt_octet8_t") rand
    :   The random number

    uint16_t div
    :   The div value

    uint8_t key_size
    :   The key size of the security link

    uint8_t sec_level
    :   The security level of the security link see bk_ble_security_level_t

struct bk_ble_lcsrk_keys_t
:   BLE SRK keys.

    Public Members

    uint32_t counter
    :   The counter value

    uint16_t div
    :   The div value

    uint8_t sec_level
    :   The security level of the security link see bk_ble_security_level_t

    [bk_bt_octet16_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") csrk
    :   The csrk key value

struct bk_ble_link_keys_t

struct bk_ble_sec_key_notif_t
:   Structure associated with BK_KEY_NOTIF_EVT.

    Public Members

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
    :   peer address

    uint32_t passkey
    :   the passkey or numeric value for comparison. If just_works, do not show this number to UI

struct bk_ble_sec_req_t
:   Structure of the security request.

    Public Members

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
    :   peer address

struct bk_ble_bond_key_info_t
:   struct type of the bond key information value

    Public Members

    [bk_ble_key_mask_t](#_CPPv417bk_ble_key_mask_t "bk_ble_key_mask_t") key_mask
    :   the key mask to indicate witch key is present

    [bk_ble_penc_keys_t](#_CPPv418bk_ble_penc_keys_t "bk_ble_penc_keys_t") penc_key
    :   received peer encryption key

    [bk_ble_pid_keys_t](#_CPPv417bk_ble_pid_keys_t "bk_ble_pid_keys_t") pid_key
    :   peer device ID key

    [bk_ble_pcsrk_keys_t](#_CPPv419bk_ble_pcsrk_keys_t "bk_ble_pcsrk_keys_t") pcsrk_key
    :   received peer device SRK

    [bk_ble_lenc_keys_t](#_CPPv418bk_ble_lenc_keys_t "bk_ble_lenc_keys_t") lenc_key
    :   local encryption reproduction keys LTK = = d1(ER,DIV,0)

    [bk_ble_pid_keys_t](#_CPPv417bk_ble_pid_keys_t "bk_ble_pid_keys_t") lid_key
    :   local device ID key

    [bk_ble_lcsrk_keys_t](#_CPPv419bk_ble_lcsrk_keys_t "bk_ble_lcsrk_keys_t") lcsrk_key
    :   local device CSRK = d1(ER,DIV,1)

struct bk_ble_bond_dev_t
:   struct type of the bond device value

    Public Members

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
    :   peer nominal address

    [bk_ble_bond_key_info_t](#_CPPv422bk_ble_bond_key_info_t "bk_ble_bond_key_info_t") bond_key
    :   peer address type

        the bond key information

struct bk_ble_local_keys_t
:   structure type of the ble local keys value

    Public Members

    [bk_bt_octet16_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") ir
    :   the 16 bits of the ir value

    [bk_bt_octet16_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") er
    :   the 16 bits of the er value

    [bk_bt_octet16_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") dhk
    :   the 16 bits of the dh key value

struct bk_ble_auth_cmpl_t
:   Structure associated with BK_AUTH_CMPL_EVT.

    Public Members

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd_addr
    :   BD address peer device.

    bool success
    :   TRUE of authentication succeeded, FALSE if failed.

    uint8_t fail_reason
    :   The HCI reason/error code for when success=FALSE

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr_type
    :   Peer device address type

    [bk_bt_dev_type_t](#_CPPv416bk_bt_dev_type_t "bk_bt_dev_type_t") dev_type
    :   Device type

    [bk_ble_auth_req_t](#_CPPv417bk_ble_auth_req_t "bk_ble_auth_req_t") auth_mode
    :   authentication mode

struct bk_ble_bond_key_req_t

struct bk_ble_gap_ext_adv_params_t
:   ext adv parameters

    Public Members

    [bk_ble_ext_adv_type_mask_t](#_CPPv426bk_ble_ext_adv_type_mask_t "bk_ble_ext_adv_type_mask_t") type
    :   ext adv type

    uint32_t interval_min
    :   ext adv minimum interval

    uint32_t interval_max
    :   ext adv maximum interval

    [bk_ble_adv_channel_t](#_CPPv420bk_ble_adv_channel_t "bk_ble_adv_channel_t") channel_map
    :   ext adv channel map

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") own_addr_type
    :   ext adv own address type

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") peer_addr_type
    :   ext adv peer address type, only BLE_ADDR_TYPE_PUBLIC and BLE_ADDR_TYPE_RANDOM is valid

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") peer_addr
    :   ext adv peer address

    [bk_ble_adv_filter_t](#_CPPv419bk_ble_adv_filter_t "bk_ble_adv_filter_t") filter_policy
    :   ext adv filter policy

    int8_t tx_power
    :   ext adv tx power

    [bk_ble_gap_pri_phy_t](#_CPPv420bk_ble_gap_pri_phy_t "bk_ble_gap_pri_phy_t") primary_phy
    :   ext adv primary phy

    uint8_t max_skip
    :   ext adv maximum skip

    [bk_ble_gap_phy_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") secondary_phy
    :   ext adv secondary phy

    uint8_t sid
    :   ext adv sid

    bool scan_req_notif
    :   ext adv scan request event notify

struct bk_ble_ext_scan_cfg_t
:   ext scan config

    Public Members

    [bk_ble_scan_type_t](#_CPPv418bk_ble_scan_type_t "bk_ble_scan_type_t") scan_type
    :   ext scan type

    uint16_t scan_interval
    :   ext scan interval

    uint16_t scan_window
    :   ext scan window

struct bk_ble_ext_scan_params_t
:   ext scan parameters

    Public Members

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") own_addr_type
    :   ext scan own address type

    [bk_ble_scan_filter_t](#_CPPv420bk_ble_scan_filter_t "bk_ble_scan_filter_t") filter_policy
    :   ext scan filter policy

    [bk_ble_scan_duplicate_t](#_CPPv423bk_ble_scan_duplicate_t "bk_ble_scan_duplicate_t") scan_duplicate
    :   ext scan duplicate scan

    [bk_ble_ext_scan_cfg_mask_t](#_CPPv426bk_ble_ext_scan_cfg_mask_t "bk_ble_ext_scan_cfg_mask_t") cfg_mask
    :   ext scan config mask

    [bk_ble_ext_scan_cfg_t](#_CPPv421bk_ble_ext_scan_cfg_t "bk_ble_ext_scan_cfg_t") uncoded_cfg
    :   ext scan uncoded config parameters

    [bk_ble_ext_scan_cfg_t](#_CPPv421bk_ble_ext_scan_cfg_t "bk_ble_ext_scan_cfg_t") coded_cfg
    :   ext scan coded config parameters

struct bk_ble_gap_conn_params_t
:   create extend connection parameters

    Public Members

    uint16_t scan_interval
    :   init scan interval

    uint16_t scan_window
    :   init scan window

    uint16_t interval_min
    :   minimum interval

    uint16_t interval_max
    :   maximum interval

    uint16_t latency
    :   ext scan type

    uint16_t supervision_timeout
    :   connection supervision timeout

    uint16_t min_ce_len
    :   minimum ce length

    uint16_t max_ce_len
    :   maximum ce length

struct bk_ble_gap_ext_adv_t
:   extend adv enable parameters

    Public Members

    uint8_t instance
    :   advertising handle

    int duration
    :   advertising duration

    int max_events
    :   maximum number of extended advertising events

struct bk_ble_gap_periodic_adv_params_t
:   periodic adv parameters

    Public Members

    uint16_t interval_min
    :   periodic advertising minimum interval

    uint16_t interval_max
    :   periodic advertising maximum interval

    uint8_t properties
    :   periodic advertising properties

struct bk_ble_gap_periodic_adv_sync_params_t
:   periodic adv sync parameters

    Public Members

    [bk_ble_gap_sync_t](#_CPPv417bk_ble_gap_sync_t "bk_ble_gap_sync_t") filter_policy
    :   periodic advertising sync filter policy

    uint8_t sid
    :   periodic advertising sid

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr_type
    :   periodic advertising address type

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr
    :   periodic advertising address

    uint16_t skip
    :   the maximum number of periodic advertising events that can be skipped

    uint16_t sync_timeout
    :   synchronization timeout

struct bk_ble_gap_ext_adv_reprot_t
:   extend adv report parameters

    Public Members

    [bk_ble_gap_adv_type_t](#_CPPv421bk_ble_gap_adv_type_t "bk_ble_gap_adv_type_t") event_type
    :   extend advertising type

    uint8_t addr_type
    :   extend advertising address type

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr
    :   extend advertising address

    [bk_ble_gap_pri_phy_t](#_CPPv420bk_ble_gap_pri_phy_t "bk_ble_gap_pri_phy_t") primary_phy
    :   extend advertising primary phy

    [bk_ble_gap_phy_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") secondly_phy
    :   extend advertising secondary phy

    uint8_t sid
    :   extend advertising sid

    uint8_t tx_power
    :   extend advertising tx power

    int8_t rssi
    :   extend advertising rssi

    uint16_t per_adv_interval
    :   periodic advertising interval

    uint8_t dir_addr_type
    :   direct address type

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") dir_addr
    :   direct address

    [bk_ble_gap_ext_adv_data_status_t](#_CPPv432bk_ble_gap_ext_adv_data_status_t "bk_ble_gap_ext_adv_data_status_t") data_status
    :   data type

    uint8_t adv_data_len
    :   extend advertising data length

    uint8_t adv_data[251]
    :   extend advertising data

struct bk_ble_gap_periodic_adv_report_t
:   periodic adv report parameters

    Public Members

    uint16_t sync_handle
    :   periodic advertising train handle

    uint8_t tx_power
    :   periodic advertising tx power

    int8_t rssi
    :   periodic advertising rssi

    [bk_ble_gap_ext_adv_data_status_t](#_CPPv432bk_ble_gap_ext_adv_data_status_t "bk_ble_gap_ext_adv_data_status_t") data_status
    :   periodic advertising data type

    uint8_t data_length
    :   periodic advertising data length

    uint8_t data[251]
    :   periodic advertising data

struct bk_ble_gap_periodic_adv_sync_estab_t
:   perodic adv sync establish parameters

    Public Members

    uint8_t status
    :   periodic advertising sync status

    uint16_t sync_handle
    :   periodic advertising train handle

    uint8_t sid
    :   periodic advertising sid

    [bk_ble_addr_type_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr_type
    :   periodic advertising address type

    [bk_bd_addr_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") adv_addr
    :   periodic advertising address

    [bk_ble_gap_phy_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") adv_phy
    :   periodic advertising adv phy type

    uint16_t period_adv_interval
    :   periodic advertising interval

    uint8_t adv_clk_accuracy
    :   periodic advertising clock accuracy


### Macros

BK_BLE_ONLY_ACCEPT_SPECIFIED_AUTH_DISABLE
:   authentication disable

BK_BLE_ONLY_ACCEPT_SPECIFIED_AUTH_ENABLE
:   authentication enable

BK_BLE_GAP_CHANNELS_LEN
:   channel length

BK_BLE_ADV_DATA_LEN_MAX
:   Advertising data maximum length.

BK_BLE_SCAN_RSP_DATA_LEN_MAX
:   Scan response data maximum length.

BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_IND
:   ADV_DIRECT_IND (low duty cycle)

BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_LD_DIR
:   ADV_DIRECT_IND (high duty cycle)

BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_HD_DIR
:   ADV_SCAN_IND

BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_SCAN
:   ADV_NONCONN_IND

BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_NONCONN

EXT_ADV_TX_PWR_NO_PREFERENCE
:   Extend advertising tx power, range: [-127, +126] dBm.

    host has no preference for tx power


### Type Definitions

typedef uint8_t bk_ble_key_type_t
:   see bk_le_key_enum_t

typedef uint8_t bk_ble_key_mask_t
:   see bk_le_key_enum_t

typedef uint8_t bk_ble_auth_req_t
:   see bk_le_auth_enum_t

typedef uint8_t bk_ble_gap_channels[BK_BLE_GAP_CHANNELS_LEN]

typedef uint16_t bk_ble_ext_adv_type_mask_t
:   such as BK_BLE_GAP_SET_EXT_ADV_PROP_CONNECTABLE and BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_IND

typedef uint8_t bk_ble_gap_phy_t
:   see bk_ble_gap_phy_enum_t

typedef uint8_t bk_ble_gap_all_phys_t

typedef uint8_t bk_ble_gap_pri_phy_t
:   see bk_ble_gap_pri_phy_enum_t

typedef uint8_t bk_ble_gap_phy_mask_t
:   see bk_ble_gap_phy_pref_enum_t

typedef uint16_t bk_ble_gap_prefer_phy_options_t
:   see bk_ble_gap_coded_phy_pref_enum_t

typedef uint8_t bk_ble_ext_scan_cfg_mask_t
:   see bk_ble_gap_ext_scan_cfg_enum_t

typedef uint8_t bk_ble_gap_ext_adv_data_status_t
:   see bk_ble_gap_ext_adv_data_seg_enum_t

typedef uint8_t bk_ble_gap_sync_t
:   see bk_ble_gap_sync_policy_enum_t

typedef uint8_t bk_ble_gap_adv_type_t
:   see bk_ble_adv_report_ext_type_enum_t

typedef void (*bk_ble_gap_cb_t)([bk_ble_gap_cb_event_t](#_CPPv421bk_ble_gap_cb_event_t "bk_ble_gap_cb_event_t") event, [bk_ble_gap_cb_param_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t") *param)
:   GAP callback function type, todo: modify docx.

    Param event
    :   : Event type

    Param param
    :   : Point to callback parameter, currently is union type


### Enumerations

enum bk_le_key_enum_t
:   *Values:*

    enumerator BK_LE_KEY_NONE
    :   No encryption key

    enumerator BK_LE_KEY_PENC
    :   encryption key, encryption information of peer device

    enumerator BK_LE_KEY_PID
    :   identity key of the peer device

    enumerator BK_LE_KEY_PCSRK
    :   peer SRK

    enumerator BK_LE_KEY_PLK
    :   Link key

    enumerator BK_LE_KEY_LLK
    :   link key

    enumerator BK_LE_KEY_LENC
    :   master role security information:div

    enumerator BK_LE_KEY_LID
    :   master device ID key

    enumerator BK_LE_KEY_LCSRK
    :   local CSRK has been deliver to peer

enum bk_le_auth_enum_t
:   *Values:*

    enumerator BK_LE_AUTH_NO_BOND
    :   0 no bondingv

    enumerator BK_LE_AUTH_BOND
    :   1 << 0 device in the bonding with peer

    enumerator BK_LE_AUTH_REQ_MITM
    :   1 << 2 man in the middle attack

    enumerator BK_LE_AUTH_REQ_BOND_MITM
    :   0101 banding with man in the middle attack

    enumerator BK_LE_AUTH_REQ_SC_ONLY
    :   1 << 3 secure connection

    enumerator BK_LE_AUTH_REQ_SC_BOND
    :   1001 secure connection with band

    enumerator BK_LE_AUTH_REQ_SC_MITM
    :   1100 secure conn with MITM

    enumerator BK_LE_AUTH_REQ_SC_MITM_BOND
    :   1101 SC with MITM and Bonding

enum bk_io_cap_enum_t
:   IO capability.


    *Values:*

    enumerator BK_IO_CAP_DISPLAY_ONLY
    :   output: display, input: none

    enumerator BK_IO_CAP_DISPLAY_YESNO
    :   output: display, input: yes or no

    enumerator BK_IO_CAP_KEYBOARD_ONLY
    :   output: none, input: keyboard. note: when both local and peer are keyboard only, both side should input same passkey which negotiated in other way, such as oral speak

    enumerator BK_IO_CAP_NONE
    :   NoInputNoOutput

    enumerator BK_IO_CAP_KEYBOARD_DISPLAY
    :   output: display, input: keyboard

enum bk_ble_gap_cb_event_t
:   GAP BLE callback event type.


    *Values:*

    enumerator BK_BLE_GAP_ADV_DATA_SET_COMPLETE_EVT
    :   When advertising data set complete, the event comes

    enumerator BK_BLE_GAP_SCAN_RSP_DATA_SET_COMPLETE_EVT
    :   When scan response data set complete, the event comes

    enumerator BK_BLE_GAP_SCAN_PARAM_SET_COMPLETE_EVT
    :   When scan parameters set complete, the event comes

    enumerator BK_BLE_GAP_SCAN_RESULT_EVT
    :   When one scan result ready, the event comes each time

    enumerator BK_BLE_GAP_ADV_DATA_RAW_SET_COMPLETE_EVT
    :   When raw advertising data set complete, the event comes

    enumerator BK_BLE_GAP_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVT
    :   When raw advertising data set complete, the event comes

    enumerator BK_BLE_GAP_ADV_START_COMPLETE_EVT
    :   When start advertising complete, the event comes

    enumerator BK_BLE_GAP_SCAN_START_COMPLETE_EVT
    :   When start scan complete, the event comes

    enumerator BK_BLE_GAP_AUTH_CMPL_EVT
    :   Authentication complete indication, param is [bk_ble_sec_t](#unionbk__ble__sec__t "#unionbk__ble__sec__t").

    enumerator BK_BLE_GAP_KEY_EVT
    :   BLE key event for peer device keys, param is [bk_ble_sec_t](#unionbk__ble__sec__t "#unionbk__ble__sec__t")

    enumerator BK_BLE_GAP_SEC_REQ_EVT
    :   BLE security request, param is [bk_ble_sec_t](#unionbk__ble__sec__t "#unionbk__ble__sec__t").

    enumerator BK_BLE_GAP_PASSKEY_NOTIF_EVT
    :   passkey notification event, param is [bk_ble_sec_t](#unionbk__ble__sec__t "#unionbk__ble__sec__t")

    enumerator BK_BLE_GAP_PASSKEY_REQ_EVT
    :   passkey request event, param is [bk_ble_sec_t](#unionbk__ble__sec__t "#unionbk__ble__sec__t")

    enumerator BK_BLE_GAP_OOB_REQ_EVT
    :   OOB request event, param is [bk_ble_sec_t](#unionbk__ble__sec__t "#unionbk__ble__sec__t")

    enumerator BK_BLE_GAP_LOCAL_IR_EVT
    :   BLE local IR (Encryption Root value used to generate identity resolving key) event

    enumerator BK_BLE_GAP_LOCAL_ER_EVT
    :   BLE local ER (identity Root 128-bit random static value used to generate Long Term Key) event

    enumerator BK_BLE_GAP_NC_REQ_EVT
    :   Numeric Comparison request event, param is [bk_ble_sec_t](#unionbk__ble__sec__t "#unionbk__ble__sec__t")

    enumerator BK_BLE_GAP_BOND_KEY_REQ_EVT
    :   the mapping relation of param.ble_key.key_type is : when BK_LE_KEY_LENC, app need reply BK_LE_KEY_LENC with bk_ble_pair_key_reply according compare param.ble_key.lenc_key

    enumerator BK_BLE_GAP_BOND_KEY_GENERATE_EVT
    :   app layer should save to storage for next power on.

    enumerator BK_BLE_GAP_BOND_DEV_LIST_OPERATEION_COMPLETE_EVT

    enumerator BK_BLE_GAP_ADV_STOP_COMPLETE_EVT
    :   When stop adv complete, the event comes

    enumerator BK_BLE_GAP_SCAN_STOP_COMPLETE_EVT
    :   When stop scan complete, the event comes

    enumerator BK_BLE_GAP_SET_STATIC_RAND_ADDR_EVT
    :   When set the static rand address complete, the event comes

    enumerator BK_BLE_GAP_UPDATE_CONN_PARAMS_EVT
    :   When update connection parameters complete, the event comes

    enumerator BK_BLE_GAP_SET_PKT_LENGTH_COMPLETE_EVT
    :   When set pkt length complete, the event comes

    enumerator BK_BLE_GAP_SET_LOCAL_PRIVACY_COMPLETE_EVT
    :   When Enable/disable privacy on the local device complete, the event comes

    enumerator BK_BLE_GAP_READ_RSSI_COMPLETE_EVT
    :   When read the rssi complete, the event comes

    enumerator BK_BLE_GAP_UPDATE_WHITELIST_COMPLETE_EVT
    :   When add or remove whitelist complete, the event comes

    enumerator BK_BLE_GAP_UPDATE_DUPLICATE_EXCEPTIONAL_LIST_COMPLETE_EVT
    :   When update duplicate exceptional list complete, the event comes

    enumerator BK_BLE_GAP_SET_CHANNELS_COMPLETE_EVT
    :   When setting BLE channels complete, the event comes

    enumerator BK_BLE_GAP_READ_PHY_COMPLETE_EVT
    :   when reading phy complete, this event comes

    enumerator BK_BLE_GAP_SET_PREFERRED_DEFAULT_PHY_COMPLETE_EVT
    :   when preferred default phy complete, this event comes

    enumerator BK_BLE_GAP_SET_PREFERRED_PHY_COMPLETE_EVT
    :   when preferred phy complete , this event comes

    enumerator BK_BLE_GAP_EXT_ADV_SET_RAND_ADDR_COMPLETE_EVT
    :   when extended set random address complete, the event comes

    enumerator BK_BLE_GAP_EXT_ADV_PARAMS_SET_COMPLETE_EVT
    :   when extended advertising parameter complete, the event comes

    enumerator BK_BLE_GAP_EXT_ADV_DATA_SET_COMPLETE_EVT
    :   when extended advertising data complete, the event comes

    enumerator BK_BLE_GAP_EXT_SCAN_RSP_DATA_SET_COMPLETE_EVT
    :   when extended scan response data complete, the event comes

    enumerator BK_BLE_GAP_EXT_ADV_DATA_RAW_SET_COMPLETE_EVT
    :   when raw extended advertising data complete, the event comes

    enumerator BK_BLE_GAP_EXT_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVT
    :   when raw extended scan response data complete, the event comes

    enumerator BK_BLE_GAP_EXT_ADV_START_COMPLETE_EVT
    :   when extended advertising start complete, the event comes

    enumerator BK_BLE_GAP_EXT_ADV_STOP_COMPLETE_EVT
    :   when extended advertising stop complete, the event comes

    enumerator BK_BLE_GAP_EXT_ADV_SET_REMOVE_COMPLETE_EVT
    :   when extended advertising set remove complete, the event comes

    enumerator BK_BLE_GAP_EXT_ADV_SET_CLEAR_COMPLETE_EVT
    :   when extended advertising set clear complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_SET_PARAMS_COMPLETE_EVT
    :   when periodic advertising parameter complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_DATA_SET_COMPLETE_EVT
    :   when periodic advertising data complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_START_COMPLETE_EVT
    :   when periodic advertising start complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_STOP_COMPLETE_EVT
    :   when periodic advertising stop complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_CREATE_SYNC_COMPLETE_EVT
    :   when periodic advertising create sync complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_SYNC_CANCEL_COMPLETE_EVT
    :   when extended advertising sync cancel complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_SYNC_TERMINATE_COMPLETE_EVT
    :   when extended advertising sync terminate complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_ADD_DEV_COMPLETE_EVT
    :   when extended advertising add device complete , the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_REMOVE_DEV_COMPLETE_EVT
    :   when extended advertising remove device complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_CLEAR_DEV_COMPLETE_EVT
    :   when extended advertising clear device, the event comes

    enumerator BK_BLE_GAP_EXT_SCAN_PARAMS_SET_COMPLETE_EVT
    :   when extended scan parameter complete, the event comes

    enumerator BK_BLE_GAP_EXT_SCAN_START_COMPLETE_EVT
    :   when extended scan start complete, the event comes

    enumerator BK_BLE_GAP_EXT_SCAN_STOP_COMPLETE_EVT
    :   when extended scan stop complete, the event comes

    enumerator BK_BLE_GAP_PREFER_EXT_CONN_PARAMS_SET_COMPLETE_EVT
    :   when extended prefer connection parameter set complete, the event comes

    enumerator BK_BLE_GAP_PHY_UPDATE_COMPLETE_EVT
    :   when ble phy update complete, the event comes

    enumerator BK_BLE_GAP_EXT_ADV_REPORT_EVT
    :   when extended advertising report complete, the event comes

    enumerator BK_BLE_GAP_SCAN_TIMEOUT_EVT
    :   when scan timeout complete, the event comes

    enumerator BK_BLE_GAP_ADV_TERMINATED_EVT
    :   when advertising terminate data complete, the event comes

    enumerator BK_BLE_GAP_SCAN_REQ_RECEIVED_EVT
    :   when scan req received complete, the event comes

    enumerator BK_BLE_GAP_CHANNEL_SELECT_ALGORITHM_EVT
    :   when channel select algorithm complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_REPORT_EVT
    :   when periodic report advertising complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_SYNC_LOST_EVT
    :   when periodic advertising sync lost complete, the event comes

    enumerator BK_BLE_GAP_PERIODIC_ADV_SYNC_ESTAB_EVT
    :   when periodic advertising sync establish complete, the event comes

    enumerator BK_BLE_GAP_CONNECT_COMPLETE_EVT
    :   when ble connection complete, the event comes

    enumerator BK_BLE_GAP_DISCONNECT_COMPLETE_EVT
    :   when ble disconnect complete, the event comes

    enumerator BK_BLE_GAP_CONNECT_CANCEL_EVT
    :   when ble connect cancel complete, the event comes

    enumerator BK_BLE_GAP_UPDATE_CONN_PARAMS_REQ_EVT
    :   when peer req update param, the event comes

    enumerator BK_BLE_GAP_SET_SECURITY_PARAMS_COMPLETE_EVT
    :   when set security params complete, the event comes

    enumerator BK_BLE_GAP_GENERATE_RPA_COMPLETE_EVT
    :   when generate rpa complete, the event comes

    enumerator BK_BLE_GAP_EVT_MAX
    :   when maximum advertising event complete, the event comes

enum bk_ble_adv_data_type
:   The type of advertising data(not adv_type)


    *Values:*

    enumerator BK_BLE_AD_TYPE_FLAG

    enumerator BK_BLE_AD_TYPE_16SRV_PART

    enumerator BK_BLE_AD_TYPE_16SRV_CMPL

    enumerator BK_BLE_AD_TYPE_32SRV_PART

    enumerator BK_BLE_AD_TYPE_32SRV_CMPL

    enumerator BK_BLE_AD_TYPE_128SRV_PART

    enumerator BK_BLE_AD_TYPE_128SRV_CMPL

    enumerator BK_BLE_AD_TYPE_NAME_SHORT

    enumerator BK_BLE_AD_TYPE_NAME_CMPL

    enumerator BK_BLE_AD_TYPE_TX_PWR

    enumerator BK_BLE_AD_TYPE_DEV_CLASS

    enumerator BK_BLE_AD_TYPE_SM_TK

    enumerator BK_BLE_AD_TYPE_SM_OOB_FLAG

    enumerator BK_BLE_AD_TYPE_INT_RANGE

    enumerator BK_BLE_AD_TYPE_SOL_SRV_UUID

    enumerator BK_BLE_AD_TYPE_128SOL_SRV_UUID

    enumerator BK_BLE_AD_TYPE_SERVICE_DATA

    enumerator BK_BLE_AD_TYPE_PUBLIC_TARGET

    enumerator BK_BLE_AD_TYPE_RANDOM_TARGET

    enumerator BK_BLE_AD_TYPE_APPEARANCE

    enumerator BK_BLE_AD_TYPE_ADV_INT

    enumerator BK_BLE_AD_TYPE_LE_DEV_ADDR

    enumerator BK_BLE_AD_TYPE_LE_ROLE

    enumerator BK_BLE_AD_TYPE_SPAIR_C256

    enumerator BK_BLE_AD_TYPE_SPAIR_R256

    enumerator BK_BLE_AD_TYPE_32SOL_SRV_UUID

    enumerator BK_BLE_AD_TYPE_32SERVICE_DATA

    enumerator BK_BLE_AD_TYPE_128SERVICE_DATA

    enumerator BK_BLE_AD_TYPE_LE_SECURE_CONFIRM

    enumerator BK_BLE_AD_TYPE_LE_SECURE_RANDOM

    enumerator BK_BLE_AD_TYPE_URI

    enumerator BK_BLE_AD_TYPE_INDOOR_POSITION

    enumerator BK_BLE_AD_TYPE_TRANS_DISC_DATA

    enumerator BK_BLE_AD_TYPE_LE_SUPPORT_FEATURE

    enumerator BK_BLE_AD_TYPE_CHAN_MAP_UPDATE

    enumerator BK_BLE_AD_TYPE_MANU

enum bk_ble_adv_type_t
:   Advertising mode.


    *Values:*

    enumerator ADV_TYPE_IND
    :   adv that can be scan and connect

    enumerator ADV_TYPE_DIRECT_IND_HIGH
    :   adv that can be connect by special device(white list). This send adv more frequently.

    enumerator ADV_TYPE_SCAN_IND
    :   adv that can be scan

    enumerator ADV_TYPE_NONCONN_IND
    :   adv that can’t be scan and connect

    enumerator ADV_TYPE_DIRECT_IND_LOW
    :   adv that can be connect by special device(white list). This send adv more few.

enum bk_ble_adv_channel_t
:   Advertising channel mask.


    *Values:*

    enumerator BK_ADV_CHNL_37
    :   channel 37

    enumerator BK_ADV_CHNL_38
    :   channel 38

    enumerator BK_ADV_CHNL_39
    :   channel 39

    enumerator BK_ADV_CHNL_ALL
    :   channel all

enum bk_ble_adv_filter_t
:   Advertising filter.


    *Values:*

    enumerator ADV_FILTER_ALLOW_SCAN_ANY_CON_ANY
    :   Allow both scan and connection requests from anyone.

    enumerator ADV_FILTER_ALLOW_SCAN_WLST_CON_ANY
    :   Allow both scan req from White List devices only and connection req from anyone.

    enumerator ADV_FILTER_ALLOW_SCAN_ANY_CON_WLST
    :   Allow both scan req from anyone and connection req from White List devices only.

    enumerator ADV_FILTER_ALLOW_SCAN_WLST_CON_WLST
    :   Allow scan and connection requests from White List devices only.

enum bk_ble_sec_act_t
:   ble encrypt method


    *Values:*

    enumerator BK_BLE_SEC_ENCRYPT
    :   If the device has already bonded, the stack will used Long Term Key (LTK) to encrypt with the remote device directly. Else if the device hasn’t bonded, the stack will used the default authentication request used the bk_ble_gap_set_security_param function set by the user.

    enumerator BK_BLE_SEC_ENCRYPT_NO_MITM
    :   If the device has been already bonded, the stack will check the LTK (Long Term Key) Whether the authentication request has been met, and if met, use the LTK to encrypt with the remote device directly, else re-pair with the remote device. Else if the device hasn’t been bonded, the stack will use NO MITM authentication request in the current link instead of using the authreq in the bk_ble_gap_set_security_param function set by the user.

    enumerator BK_BLE_SEC_ENCRYPT_MITM
    :   If the device has been already bonded, the stack will check the LTK (Long Term Key) whether the authentication request has been met, and if met, use the LTK to encrypt with the remote device directly, else re-pair with the remote device. Else if the device hasn’t been bonded, the stack will use MITM authentication request in the current link instead of using the authreq in the bk_ble_gap_set_security_param function set by the user.

enum bk_ble_sm_param_t
:   ble sm option


    *Values:*

    enumerator BK_BLE_SM_AUTHEN_REQ_MODE
    :   Authentication requirements of local device, see bk_ble_auth_req_t.

    enumerator BK_BLE_SM_IOCAP_MODE
    :   The IO capability of local device, see bk_io_cap_enum_t.

    enumerator BK_BLE_SM_SET_INIT_KEY
    :   Initiator Key Distribution/Generation, use BK_BLE_SM_SET_LOCAL_REMOTE_KEY instead !!!

    enumerator BK_BLE_SM_SET_RSP_KEY
    :   Responder Key Distribution/Generation, use BK_BLE_SM_SET_LOCAL_REMOTE_KEY instead !!!

    enumerator BK_BLE_SM_MAX_KEY_SIZE
    :   Maximum Encryption key size to support.

    enumerator BK_BLE_SM_MIN_KEY_SIZE
    :   Minimum Encryption key size requirement from Peer.

    enumerator BK_BLE_SM_SET_STATIC_PASSKEY
    :   Set static Passkey.

    enumerator BK_BLE_SM_CLEAR_STATIC_PASSKEY
    :   Reset static Passkey.

    enumerator BK_BLE_SM_ONLY_ACCEPT_SPECIFIED_SEC_AUTH
    :   Accept only specified SMP Authentication requirement.

    enumerator BK_BLE_SM_OOB_SUPPORT
    :   Enable/Disable OOB support.

    enumerator BK_BLE_SM_SET_ER
    :   set ER, 16 bytes

    enumerator BK_BLE_SM_SET_IR
    :   set IR, 16 bytes

    enumerator BK_BLE_SM_SET_LOCAL_REMOTE_KEY
    :   local and remote init key, first 4 bits means local, last 4 bits means remote

enum bk_ble_key_distr_mask_t
:   the key distribution mask type


    *Values:*

    enumerator BK_BLE_KEY_DISTR_ENC_KEY_MASK

    enumerator BK_BLE_KEY_DISTR_ID_KEY_MASK
    :   Used to exchange the encryption key in the init key & response key, not used now.

    enumerator BK_BLE_KEY_DISTR_CSR_KEY_MASK
    :   Used to exchange the IRK key in the init key & response key, not used now.

    enumerator BK_BLE_KEY_DISTR_LINK_KEY_MASK
    :   Used to exchange the CSRK key in the init key & response key, not used now.

        Used to exchange the link key(this key just used in the BLE & BR/EDR coexist mode) in the init key & response key, must used with BK_LE_AUTH_REQ_SC_MITM_BOND.

enum bk_ble_scan_type_t
:   Ble scan type.


    *Values:*

    enumerator BLE_SCAN_TYPE_PASSIVE
    :   Passive scan

    enumerator BLE_SCAN_TYPE_ACTIVE
    :   Active scan

enum bk_ble_scan_filter_t
:   Ble scan filter type.


    *Values:*

    enumerator BLE_SCAN_FILTER_ALLOW_ALL
    :   Accept all :

        1. advertisement packets except directed advertising packets not addressed to this device (default).

    enumerator BLE_SCAN_FILTER_ALLOW_ONLY_WLST
    :   Accept only :

        1. advertisement packets from devices where the advertiser’s address is in the White list.
        2. Directed advertising packets which are not addressed for this device shall be ignored.

    enumerator BLE_SCAN_FILTER_ALLOW_UND_RPA_DIR
    :   Accept all :

        1. undirected advertisement packets, and
        2. directed advertising packets where the initiator address is a resolvable private address, and
        3. directed advertising packets addressed to this device.

    enumerator BLE_SCAN_FILTER_ALLOW_WLIST_RPA_DIR
    :   Accept all :

        1. advertisement packets from devices where the advertiser’s address is in the White list, and
        2. directed advertising packets where the initiator address is a resolvable private address, and
        3. directed advertising packets addressed to this device.

enum bk_ble_scan_duplicate_t
:   Ble scan duplicate type.


    *Values:*

    enumerator BLE_SCAN_DUPLICATE_DISABLE
    :   the Link Layer should generate advertising reports to the host for each packet received

    enumerator BLE_SCAN_DUPLICATE_ENABLE
    :   the Link Layer should filter out duplicate advertising reports to the Host

    enumerator BLE_SCAN_DUPLICATE_MAX
    :   0x02 – 0xFF, Reserved for future use

enum bk_ble_security_level_t
:   *Values:*

    enumerator BK_BLE_SECURITY_LEVEL_1

    enumerator BK_BLE_SECURITY_LEVEL_2

    enumerator BK_BLE_SECURITY_LEVEL_3

    enumerator BK_BLE_SECURITY_LEVEL_4

enum bk_gap_bond_dev_list_operation_t
:   bond dev list operation


    *Values:*

    enumerator BK_GAP_BOND_DEV_LIST_OPERATION_ADD

    enumerator BK_GAP_BOND_DEV_LIST_OPERATION_REMOVE

    enumerator BK_GAP_BOND_DEV_LIST_OPERATION_CLEAN

enum bk_gap_search_evt_t
:   Sub Event of BK_BLE_GAP_SCAN_RESULT_EVT.


    *Values:*

    enumerator BK_GAP_SEARCH_INQ_RES_EVT
    :   Inquiry result for a peer device.

    enumerator BK_GAP_SEARCH_INQ_CMPL_EVT
    :   Inquiry complete.

    enumerator BK_GAP_SEARCH_DISC_RES_EVT
    :   Discovery result for a peer device.

    enumerator BK_GAP_SEARCH_DISC_BLE_RES_EVT
    :   Discovery result for BLE GATT based service on a peer device.

    enumerator BK_GAP_SEARCH_DISC_CMPL_EVT
    :   Discovery complete.

    enumerator BK_GAP_SEARCH_DI_DISC_CMPL_EVT
    :   Discovery complete.

    enumerator BK_GAP_SEARCH_SEARCH_CANCEL_CMPL_EVT
    :   Search cancelled

    enumerator BK_GAP_SEARCH_INQ_DISCARD_NUM_EVT
    :   The number of pkt discarded by flow control

enum bk_ble_evt_type_t
:   Ble scan result event type, to indicate the result is scan response or advertising data or other.


    *Values:*

    enumerator BK_BLE_EVT_CONN_ADV
    :   Connectable undirected advertising (ADV_IND)

    enumerator BK_BLE_EVT_CONN_DIR_ADV
    :   Connectable directed advertising (ADV_DIRECT_IND)

    enumerator BK_BLE_EVT_DISC_ADV
    :   Scannable undirected advertising (ADV_SCAN_IND)

    enumerator BK_BLE_EVT_NON_CONN_ADV
    :   Non connectable undirected advertising (ADV_NONCONN_IND)

    enumerator BK_BLE_EVT_SCAN_RSP
    :   Scan Response (SCAN_RSP)

enum bk_ble_wl_operation_t
:   white list op


    *Values:*

    enumerator BK_BLE_WHITELIST_REMOVE
    :   remove mac from whitelist

    enumerator BK_BLE_WHITELIST_ADD
    :   add address to whitelist

    enumerator BK_BLE_WHITELIST_CLEAN
    :   clean whitelist

enum bk_ble_gap_set_ext_adv_prop_t
:   ext adv prop


    *Values:*

    enumerator BK_BLE_GAP_SET_EXT_ADV_PROP_NONCONN_NONSCANNABLE_UNDIRECTED
    :   Non-Connectable and Non-Scannable Undirected advertising

    enumerator BK_BLE_GAP_SET_EXT_ADV_PROP_CONNECTABLE
    :   Connectable advertising

    enumerator BK_BLE_GAP_SET_EXT_ADV_PROP_SCANNABLE
    :   Scannable advertising

    enumerator BK_BLE_GAP_SET_EXT_ADV_PROP_DIRECTED
    :   Directed advertising

    enumerator BK_BLE_GAP_SET_EXT_ADV_PROP_HD_DIRECTED
    :   High Duty Cycle Directed Connectable advertising (<= 3.75 ms Advertising Interval)

    enumerator BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY
    :   Use legacy advertising PDUs

    enumerator BK_BLE_GAP_SET_EXT_ADV_PROP_ANON_ADV
    :   Omit advertiser’s address from all PDUs (“anonymous advertising”)

    enumerator BK_BLE_GAP_SET_EXT_ADV_PROP_INCLUDE_TX_PWR
    :   Include TxPower in the extended header of the advertising PDU

    enumerator BK_BLE_GAP_SET_EXT_ADV_PROP_MASK
    :   Reserved for future use

enum bk_ble_gap_phy_enum_t
:   *Values:*

    enumerator BK_BLE_GAP_PHY_1M
    :   Secondery Advertisement PHY is LE1M

    enumerator BK_BLE_GAP_PHY_2M
    :   Secondery Advertisement PHY is LE2M

    enumerator BK_BLE_GAP_PHY_CODED
    :   Secondery Advertisement PHY is LE Coded

enum bk_ble_gap_noprefer_enum_t
:   ble gap noprefer phy


    *Values:*

    enumerator BK_BLE_GAP_NO_PREFER_TRANSMIT_PHY
    :   No Prefer TX PHY supported by controller

    enumerator BK_BLE_GAP_NO_PREFER_RECEIVE_PHY
    :   No Prefer RX PHY supported by controller

enum bk_ble_gap_pri_phy_enum_t
:   Primary phy only support 1M and LE coded phy.


    *Values:*

    enumerator BK_BLE_GAP_PRI_PHY_1M
    :   Primary Phy is LE1M

    enumerator BK_BLE_GAP_PRI_PHY_CODED
    :   Primary Phy is LE CODED

enum bk_ble_gap_phy_pref_enum_t
:   *Values:*

    enumerator BK_BLE_GAP_PHY_1M_PREF_MASK
    :   The Host prefers use the LE1M transmitter or reciever PHY

    enumerator BK_BLE_GAP_PHY_2M_PREF_MASK
    :   The Host prefers use the LE2M transmitter or reciever PHY

    enumerator BK_BLE_GAP_PHY_CODED_PREF_MASK
    :   The Host prefers use the LE CODED transmitter or reciever PHY

enum bk_ble_gap_coded_phy_pref_enum_t
:   ble gap coded phy pref param


    *Values:*

    enumerator BK_BLE_GAP_PHY_OPTIONS_NO_PREF
    :   The Host has no preferred coding when transmitting on the LE Coded PHY

    enumerator BK_BLE_GAP_PHY_OPTIONS_PREF_S2_CODING
    :   The Host prefers that S=2 coding be used when transmitting on the LE Coded PHY

    enumerator BK_BLE_GAP_PHY_OPTIONS_PREF_S8_CODING
    :   The Host prefers that S=8 coding be used when transmitting on the LE Coded PHY

enum bk_ble_gap_ext_scan_cfg_enum_t
:   ble gap ext scan cfg


    *Values:*

    enumerator BK_BLE_GAP_EXT_SCAN_CFG_UNCODE_MASK
    :   Scan Advertisements on the LE1M PHY

    enumerator BK_BLE_GAP_EXT_SCAN_CFG_CODE_MASK
    :   Scan advertisements on the LE coded PHY

enum bk_ble_gap_ext_adv_data_seg_enum_t
:   Advertising data seg.


    *Values:*

    enumerator BK_BLE_GAP_EXT_ADV_DATA_COMPLETE
    :   extended advertising data compete

    enumerator BK_BLE_GAP_EXT_ADV_DATA_INCOMPLETE
    :   extended advertising data incomplete

    enumerator BK_BLE_GAP_EXT_ADV_DATA_TRUNCATED
    :   extended advertising data truncated mode

enum bk_ble_gap_sync_policy_enum_t
:   Advertising SYNC policy.


    *Values:*

    enumerator BK_BLE_GAP_SYNC_POLICY_BY_ADV_INFO
    :   sync policy by advertising info

    enumerator BK_BLE_GAP_SYNC_POLICY_BY_PERIODIC_LIST
    :   periodic advertising sync policy

enum bk_ble_adv_report_ext_type_enum_t
:   Advertising report.


    *Values:*

    enumerator BK_BLE_ADV_REPORT_EXT_ADV_IND
    :   advertising report with extended advertising indication type

    enumerator BK_BLE_ADV_REPORT_EXT_SCAN_IND
    :   advertising report with extended scan indication type

    enumerator BK_BLE_ADV_REPORT_EXT_DIRECT_ADV
    :   advertising report with extended direct advertising indication type

    enumerator BK_BLE_ADV_REPORT_EXT_SCAN_RSP
    :   advertising report with extended scan response indication type

    enumerator BK_BLE_LEGACY_ADV_TYPE_IND
    :   advertising report with legacy advertising indication type

    enumerator BK_BLE_LEGACY_ADV_TYPE_DIRECT_IND
    :   advertising report with legacy direct indication type

    enumerator BK_BLE_LEGACY_ADV_TYPE_SCAN_IND
    :   advertising report with legacy scan indication type

    enumerator BK_BLE_LEGACY_ADV_TYPE_NONCON_IND
    :   advertising report with legacy non connectable indication type

    enumerator BK_BLE_LEGACY_ADV_TYPE_SCAN_RSP_TO_ADV_IND
    :   advertising report with legacy scan response indication type

    enumerator BK_BLE_LEGACY_ADV_TYPE_SCAN_RSP_TO_ADV_SCAN_IND
    :   advertising report with legacy advertising with scan response indication type


## bk_dm_gatt_types.h

`bk_dm_gatt_types.h` 定义 BLE GATT 公共数据结构、权限、属性和回调类型。


### Header File


- [bluetooth/bk_dm_gatt_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gatt_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_gatt_types.h")


### Structures

struct bk_gatt_id_t
:   Gatt id, include uuid and instance id.

    Public Members

    [bk_bt_uuid_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") uuid
    :   UUID

struct bk_gatt_srvc_id_t
:   Gatt service id, include id (uuid and instance id) and primary flag.

    Public Members

    [bk_gatt_id_t](#_CPPv412bk_gatt_id_t "bk_gatt_id_t") id
    :   Gatt id, include uuid and instance

    bool is_primary
    :   This service is primary or not

struct bk_attr_value_t
:   set the attribute value type

    Public Members

    uint16_t attr_max_len
    :   attribute max value length

    uint16_t attr_len
    :   attribute current value length

    uint8_t *attr_value
    :   the pointer to attribute value

struct bk_attr_desc_t
:   Attribute description (used to create database)

    Public Members

    [bk_bt_uuid_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") attr_content
    :   attr type

    [bk_attr_value_t](#_CPPv415bk_attr_value_t "bk_attr_value_t") value
    :   attr content if attr_type is service or char

    [bk_gatt_char_prop_t](#_CPPv419bk_gatt_char_prop_t "bk_gatt_char_prop_t") prop
    :   Element value if attr_type is char or desc.

    [bk_gatt_perm_enum_t](#_CPPv419bk_gatt_perm_enum_t "bk_gatt_perm_enum_t") perm
    :   char prop, only used if attr_type is char

        Attribute permission

struct bk_attr_control_t
:   attribute auto response flag

    Public Members

    uint8_t auto_rsp
    :   if auto_rsp set to BK_GATT_RSP_BY_APP, means the response of Write/Read operation will by replied by application. if auto_rsp set to BK_GATT_AUTO_RSP, means the response of Write/Read operation will be replied by GATT stack automatically.

struct bk_gatts_attr_db_t
:   attribute type added to the gatt server database

    Public Members

    [bk_attr_desc_t](#_CPPv414bk_attr_desc_t "bk_attr_desc_t") att_desc
    :   The attribute type

    [bk_attr_control_t](#_CPPv417bk_attr_control_t "bk_attr_control_t") attr_control
    :   The attribute control type, not used if attr type is service

struct bk_gatt_value_t
:   Gatt attribute value.

    Public Members

    uint8_t *value
    :   Gatt attribute value

    uint16_t handle
    :   Gatt attribute handle

    uint16_t offset
    :   Gatt attribute value offset

    uint16_t len
    :   Gatt attribute value length

    [bk_gatt_auth_req_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth_req
    :   Gatt authentication request see bk_gatt_auth_req_t

struct bk_gatt_rsp_t
:   GATT remote read request response type.

    Public Members

    [bk_gatt_value_t](#_CPPv415bk_gatt_value_t "bk_gatt_value_t") attr_value
    :   Gatt attribute structure

struct bk_gatt_conn_params_t
:   Connection parameters information.

    Public Members

    uint16_t interval
    :   connection interval

    uint16_t latency
    :   Slave latency for the connection in number of connection events. Range: 0x0000 to 0x01F3

    uint16_t timeout
    :   Supervision timeout for the LE Link. Range: 0x000A to 0x0C80. Mandatory Range: 0x000A to 0x0C80 Time = N * 10 msec Time Range: 100 msec to 32 seconds

struct bk_gattc_multi_t
:   read multiple attribute

    Public Members

    uint8_t num_attr
    :   The number of the attribute

    uint16_t handles[BK_GATT_MAX_READ_MULTI_HANDLES]
    :   The handles list


### Macros

BK_GATT_MAX_READ_MULTI_HANDLES

BK_GATT_RSP_BY_APP

BK_GATT_AUTO_RSP


### Type Definitions

typedef uint16_t bk_gatt_perm_t
:   see bk_gatt_perm_enum_t

typedef uint8_t bk_gatt_char_prop_t
:   see bk_gatt_char_prop_enum_t

typedef uint8_t bk_gatt_if_t
:   Gatt interface type, different application on GATT client use different gatt_if


### Enumerations

enum bk_gatt_uuid_enum_t
:   gatt uuid type, All “BK_GATT_UUID_xxx” is attribute types


    *Values:*

    enumerator BK_GATT_UUID_GAP_SVC

    enumerator BK_GATT_UUID_GATT_SVC
    :   Generic Access Profile service.

    enumerator BK_GATT_UUID_IMMEDIATE_ALERT_SVC
    :   Generic Attribute Profile service.

    enumerator BK_GATT_UUID_LINK_LOSS_SVC
    :   Immediate alert service.

    enumerator BK_GATT_UUID_TX_POWER_SVC
    :   Link Loss service.

    enumerator BK_GATT_UUID_CURRENT_TIME_SVC
    :   TX Power service.

    enumerator BK_GATT_UUID_REF_TIME_UPDATE_SVC
    :   Current Time Service service.

    enumerator BK_GATT_UUID_NEXT_DST_CHANGE_SVC
    :   Reference Time Update service.

    enumerator BK_GATT_UUID_GLUCOSE_SVC
    :   Next DST Change service.

    enumerator BK_GATT_UUID_HEALTH_THERMOM_SVC
    :   Glucose service.

    enumerator BK_GATT_UUID_DEVICE_INFO_SVC
    :   Health Thermometer service.

    enumerator BK_GATT_UUID_HEART_RATE_SVC
    :   Device Information service.

    enumerator BK_GATT_UUID_PHONE_ALERT_STATUS_SVC
    :   Heart Rate service.

    enumerator BK_GATT_UUID_BATTERY_SERVICE_SVC
    :   Phone Alert Status service.

    enumerator BK_GATT_UUID_BLOOD_PRESSURE_SVC
    :   Battery service.

    enumerator BK_GATT_UUID_ALERT_NTF_SVC
    :   Blood Pressure service.

    enumerator BK_GATT_UUID_HID_SVC
    :   Alert Notification service.

    enumerator BK_GATT_UUID_SCAN_PARAMETERS_SVC
    :   HID service.

    enumerator BK_GATT_UUID_RUNNING_SPEED_CADENCE_SVC
    :   Scan Parameters service.

    enumerator BK_GATT_UUID_Automation_IO_SVC
    :   Running Speed and Cadence service.

    enumerator BK_GATT_UUID_CYCLING_SPEED_CADENCE_SVC
    :   Automation IO service.

    enumerator BK_GATT_UUID_CYCLING_POWER_SVC
    :   Cycling Speed and Cadence service.

    enumerator BK_GATT_UUID_LOCATION_AND_NAVIGATION_SVC
    :   Cycling Power service.

    enumerator BK_GATT_UUID_ENVIRONMENTAL_SENSING_SVC
    :   Location and Navigation service.

    enumerator BK_GATT_UUID_BODY_COMPOSITION
    :   Environmental Sensing service.

    enumerator BK_GATT_UUID_USER_DATA_SVC
    :   Body Composition service.

    enumerator BK_GATT_UUID_WEIGHT_SCALE_SVC
    :   User Data service.

    enumerator BK_GATT_UUID_BOND_MANAGEMENT_SVC
    :   Weight Scale service.

    enumerator BK_GATT_UUID_CONT_GLUCOSE_MONITOR_SVC
    :   Bond Management service.

    enumerator BK_GATT_UUID_PRI_SERVICE
    :   Continuous Glucose Monitoring service.

        Declarations

    enumerator BK_GATT_UUID_SEC_SERVICE

    enumerator BK_GATT_UUID_INCLUDE_SERVICE

    enumerator BK_GATT_UUID_CHAR_DECLARE

    enumerator BK_GATT_UUID_CHAR_EXT_PROP
    :   Characteristic Declaration.

        Descriptors

    enumerator BK_GATT_UUID_CHAR_USER_DESCRIPTION
    :   Characteristic Extended Properties.

    enumerator BK_GATT_UUID_CHAR_CLIENT_CONFIG
    :   Characteristic User Description.

    enumerator BK_GATT_UUID_CHAR_SRVR_CONFIG
    :   Client Characteristic Configuration.

    enumerator BK_GATT_UUID_CHAR_PRESENT_FORMAT
    :   Server Characteristic Configuration.

    enumerator BK_GATT_UUID_CHAR_AGG_FORMAT
    :   Characteristic Presentation Format.

    enumerator BK_GATT_UUID_CHAR_VALID_RANGE
    :   Characteristic Aggregate Format.

    enumerator BK_GATT_UUID_EXT_RPT_REF_DESCR
    :   Characteristic Valid Range.

    enumerator BK_GATT_UUID_RPT_REF_DESCR
    :   External Report Reference.

    enumerator BK_GATT_UUID_NUM_DIGITALS_DESCR
    :   Report Reference.

    enumerator BK_GATT_UUID_VALUE_TRIGGER_DESCR
    :   Number of Digitals.

    enumerator BK_GATT_UUID_ENV_SENSING_CONFIG_DESCR
    :   Value Trigger Setting.

    enumerator BK_GATT_UUID_ENV_SENSING_MEASUREMENT_DESCR
    :   Environmental Sensing Configuration.

    enumerator BK_GATT_UUID_ENV_SENSING_TRIGGER_DESCR
    :   Environmental Sensing Measurement.

    enumerator BK_GATT_UUID_TIME_TRIGGER_DESCR
    :   Environmental Sensing Trigger Setting.

    enumerator BK_GATT_UUID_BR_EDR_TRANS_BLOCK_DATA
    :   Time Trigger Setting.

    enumerator BK_GATT_UUID_OBSERVATION_SCHEDULE
    :   Complete BRT-EDR Transport BLock Data.

    enumerator BK_GATT_UUID_VALID_RANGE_ACCURACY
    :   Observation Schedule.

    enumerator BK_GATT_UUID_MEASUREMENT_DESCRIPTION
    :   Valid Range and Accuracy.

    enumerator BK_GATT_UUID_MANUFACTURER_LIMITS

    enumerator BK_GATT_UUID_PROCESS_TOLERANCES

    enumerator BK_GATT_UUID_IMD_TRIGGER_SETTING

    enumerator BK_GATT_UUID_GAP_DEVICE_NAME
    :   GAP Profile Attributes.

    enumerator BK_GATT_UUID_GAP_APPEARANCE

    enumerator BK_GATT_UUID_GAP_PREF_CONN_PARAM

    enumerator BK_GATT_UUID_GAP_CENTRAL_ADDR_RESOL

    enumerator BK_GATT_UUID_GAP_RESOLV_RPVIATE_ADDR_ONLY

    enumerator BK_GATT_UUID_GAP_ENCRYPT_DATA_KEY_MATERIAL

    enumerator BK_GATT_UUID_GAP_BLE_GATT_SECURITY_LVL

    enumerator BK_GATT_UUID_GATT_SRV_CHGD
    :   Attribute Profile Attribute UUID.

    enumerator BK_GATT_UUID_GATT_CLI_SUPPORT_FEAT

    enumerator BK_GATT_UUID_GATT_DATABASE_HASH

    enumerator BK_GATT_UUID_GATT_SRV_SUPPORT_FEAT

    enumerator BK_GATT_UUID_ALERT_LEVEL
    :   Link BK_Loss Service.

    enumerator BK_GATT_UUID_TX_POWER_LEVEL
    :   Alert Level.

    enumerator BK_GATT_UUID_CURRENT_TIME
    :   TX power level.

        Current Time Service

    enumerator BK_GATT_UUID_LOCAL_TIME_INFO
    :   Current Time.

    enumerator BK_GATT_UUID_REF_TIME_INFO
    :   Local time info.

    enumerator BK_GATT_UUID_NW_STATUS
    :   reference time information

        Network availability Profile

    enumerator BK_GATT_UUID_NW_TRIGGER
    :   network availability status

    enumerator BK_GATT_UUID_ALERT_STATUS
    :   Network availability trigger.

        Phone alert

    enumerator BK_GATT_UUID_RINGER_CP
    :   alert status

    enumerator BK_GATT_UUID_RINGER_SETTING
    :   ringer control point

    enumerator BK_GATT_UUID_GM_MEASUREMENT
    :   ringer setting

        Glucose Service

    enumerator BK_GATT_UUID_GM_CONTEXT

    enumerator BK_GATT_UUID_GM_CONTROL_POINT

    enumerator BK_GATT_UUID_GM_FEATURE

    enumerator BK_GATT_UUID_SYSTEM_ID
    :   device information characteristic

    enumerator BK_GATT_UUID_MODEL_NUMBER_STR

    enumerator BK_GATT_UUID_SERIAL_NUMBER_STR

    enumerator BK_GATT_UUID_FW_VERSION_STR

    enumerator BK_GATT_UUID_HW_VERSION_STR

    enumerator BK_GATT_UUID_SW_VERSION_STR

    enumerator BK_GATT_UUID_MANU_NAME

    enumerator BK_GATT_UUID_IEEE_DATA

    enumerator BK_GATT_UUID_PNP_ID

    enumerator BK_GATT_UUID_HID_INFORMATION
    :   HID characteristics.

    enumerator BK_GATT_UUID_HID_REPORT_MAP

    enumerator BK_GATT_UUID_HID_CONTROL_POINT

    enumerator BK_GATT_UUID_HID_REPORT

    enumerator BK_GATT_UUID_HID_PROTO_MODE

    enumerator BK_GATT_UUID_HID_BT_KB_INPUT

    enumerator BK_GATT_UUID_HID_BT_KB_OUTPUT

    enumerator BK_GATT_UUID_HID_BT_MOUSE_INPUT

    enumerator BK_GATT_HEART_RATE_MEAS
    :   Heart Rate Measurement.

    enumerator BK_GATT_BODY_SENSOR_LOCATION
    :   Body Sensor Location.

    enumerator BK_GATT_HEART_RATE_CNTL_POINT
    :   Heart Rate Control Point.

    enumerator BK_GATT_UUID_BATTERY_LEVEL
    :   Battery Service characteristics.

    enumerator BK_GATT_UUID_SC_CONTROL_POINT
    :   Sensor Service.

    enumerator BK_GATT_UUID_SENSOR_LOCATION

    enumerator BK_GATT_UUID_RSC_MEASUREMENT
    :   Runners speed and cadence service.

    enumerator BK_GATT_UUID_RSC_FEATURE

    enumerator BK_GATT_UUID_CSC_MEASUREMENT
    :   Cycling speed and cadence service.

    enumerator BK_GATT_UUID_CSC_FEATURE

    enumerator BK_GATT_UUID_SCAN_INT_WINDOW
    :   Scan BK_Parameter characteristics.

    enumerator BK_GATT_UUID_SCAN_REFRESH

enum bk_gatt_status_t
:   GATT success code and error codes.


    *Values:*

    enumerator BK_GATT_OK

    enumerator BK_GATT_INVALID_HANDLE

    enumerator BK_GATT_READ_NOT_PERMIT

    enumerator BK_GATT_WRITE_NOT_PERMIT

    enumerator BK_GATT_INVALID_PDU

    enumerator BK_GATT_INSUF_AUTHENTICATION

    enumerator BK_GATT_REQ_NOT_SUPPORTED

    enumerator BK_GATT_INVALID_OFFSET

    enumerator BK_GATT_INSUF_AUTHORIZATION

    enumerator BK_GATT_PREPARE_Q_FULL

    enumerator BK_GATT_NOT_FOUND

    enumerator BK_GATT_NOT_LONG

    enumerator BK_GATT_INSUF_KEY_SIZE

    enumerator BK_GATT_INVALID_ATTR_LEN

    enumerator BK_GATT_ERR_UNLIKELY

    enumerator BK_GATT_INSUF_ENCRYPTION

    enumerator BK_GATT_UNSUPPORT_GRP_TYPE

    enumerator BK_GATT_INSUF_RESOURCE

    enumerator BK_GATT_DB_OUT_OF_SYNC

    enumerator BK_GATT_PARAM_VAL_NOT_ALLOW

    enumerator BK_GATT_WRITE_REQ_REJECT

    enumerator BK_GATT_CCC_CFG_ERR
    :   Write Request Rejected.

    enumerator BK_GATT_PRC_IN_PROGRESS
    :   0xFD Client Characteristic Configuration Descriptor Improperly Configured

    enumerator BK_GATT_OUT_OF_RANGE
    :   0xFE Procedure Already in progress

    enumerator BK_GATT_UNKNOWN_ERROR
    :   0xFF Attribute value out of range */

enum bk_gatt_conn_reason_t
:   Gatt Connection reason enum.


    *Values:*

    enumerator BK_GATT_CONN_UNKNOWN
    :   Gatt connection unknown

enum bk_gatt_auth_req_t
:   Gatt authentication request type.


    *Values:*

    enumerator BK_GATT_AUTH_REQ_NONE

enum bk_gatt_perm_enum_t
:   Attribute permissions.


    **Attention**
    :   When MITM is enable, key generation method can not be Just Work. This require both local and peer iocap configuration suitable. See bluetooth core specification Version 5.4 | Vol 3, Part H, 2.3.5.1 Selecting key generation method.


    *Values:*

    enumerator BK_GATT_PERM_READ

    enumerator BK_GATT_PERM_READ_ENCRYPTED

    enumerator BK_GATT_PERM_READ_ENC_MITM

    enumerator BK_GATT_PERM_WRITE

    enumerator BK_GATT_PERM_WRITE_ENCRYPTED

    enumerator BK_GATT_PERM_WRITE_ENC_MITM

    enumerator BK_GATT_PERM_WRITE_SIGNED

    enumerator BK_GATT_PERM_WRITE_SIGNED_MITM

    enumerator BK_GATT_PERM_READ_AUTHORIZATION

    enumerator BK_GATT_PERM_WRITE_AUTHORIZATION

enum bk_gatt_char_prop_enum_t
:   definition of characteristic properties


    *Values:*

    enumerator BK_GATT_CHAR_PROP_BIT_BROADCAST

    enumerator BK_GATT_CHAR_PROP_BIT_READ

    enumerator BK_GATT_CHAR_PROP_BIT_WRITE_NR

    enumerator BK_GATT_CHAR_PROP_BIT_WRITE

    enumerator BK_GATT_CHAR_PROP_BIT_NOTIFY

    enumerator BK_GATT_CHAR_PROP_BIT_INDICATE

    enumerator BK_GATT_CHAR_PROP_BIT_AUTH_SIGNED_WRITE

    enumerator BK_GATT_CHAR_PROP_BIT_EXT_PROP

enum bk_service_source_t
:   gatt service source


    *Values:*

    enumerator BK_GATT_SERVICE_FROM_REMOTE_DEVICE

    enumerator BK_GATT_SERVICE_FROM_NVS_FLASH

    enumerator BK_GATT_SERVICE_FROM_UNKNOWN

enum bk_gatt_write_type_t
:   Gatt write type.


    *Values:*

    enumerator BK_GATT_WRITE_TYPE_NO_RSP
    :   Gatt write attribute need no response

    enumerator BK_GATT_WRITE_TYPE_RSP
    :   Gatt write attribute need remote response


## bk_dm_bluetooth.h

`bk_dm_bluetooth.h` 提供 Bluetooth 通用 API 和通用初始化能力。


### Header File


- [bluetooth/bk_dm_bluetooth.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_bluetooth.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_bluetooth.h")


### Functions

[bk_bluetooth_status_t](#_CPPv421bk_bluetooth_status_t "bk_bluetooth_status_t") bk_bluetooth_get_status(void)
:   Get bluetooth status.

    返回
    :   Bluetooth status

[bt_err_t](#_CPPv48bt_err_t "bt_err_t") bk_bluetooth_init(void)
:   init bluetooth.

    返回
    :   - BT_OK: success

        - others: fail

[bt_err_t](#_CPPv48bt_err_t "bt_err_t") bk_bluetooth_deinit(void)
:   deinit bluetooth.

    返回
    :   - BT_OK: success

        - others: fail

[bt_err_t](#_CPPv48bt_err_t "bt_err_t") bk_bluetooth_get_address(uint8_t *addr)
:   Get bluetooth device address. Must use after “bk_bluetooth_init”.

    参数
    :   **addr** – **[out]** - bluetooth device address

    返回
    :   - BT_OK: success

        - others: fail

[bt_err_t](#_CPPv48bt_err_t "bt_err_t") bk_bluetooth_reg_secondary_controller([bk_bluetooth_secondary_callback_t](#_CPPv433bk_bluetooth_secondary_callback_t "bk_bluetooth_secondary_callback_t") *cb)


## bk_dm_bluetooth_types.h

`bk_dm_bluetooth_types.h` 定义 Bluetooth 通用 API 使用的基础类型。


### Header File


- [bluetooth/bk_dm_bluetooth_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_bluetooth_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_dm_bluetooth_types.h")


### Structures

struct bt_cmd_param_t
:   Public Members

    uint8_t cmd_idx
    :   actv_idx

    [bt_err_t](#_CPPv48bt_err_t "bt_err_t") status
    :   The status for this command

struct bk_bt_uuid_t
:   UUID type.

    Public Members

    uint16_t len
    :   UUID length, 16bit, 32bit or 128bit

    uint16_t uuid16
    :   16bit UUID

    uint32_t uuid32
    :   32bit UUID

    uint8_t uuid128[BK_UUID_LEN_128]
    :   128bit UUID

    union [bk_bt_uuid_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t")::[anonymous] uuid
    :   UUID

struct bk_bluetooth_secondary_callback_t


### Macros

BK_BT_ADDR_LEN

BK_ERR_BT_SUCCESS
:   success

BK_ERR_BT_FAIL
:   fail

BK_ERR_BT_NO_MEM
:   no mem

BK_ERR_BT_PROFILE
:   profile err

BK_ERR_BT_CMD_NOT_SUPPORT
:   unknow cmd err

BK_ERR_BT_UNKNOW_IDX
:   index err, suchas conn_ind

BK_ERR_BT_BT_STATUS
:   ble status not match

BK_ERR_BT_CMD_RUN
:   cmd run err

BK_ERR_BT_INIT_CREATE
:   create init err, such as bk_ble_create_init

BK_ERR_BT_INIT_STATE
:   current init status not match

BT_OK
:   success

BT_FAIL
:   failure

BT_INTERFACE_NOT_SUPPORT
:   interface not support

BK_BT_OCTET16_LEN

BK_BT_OCTET8_LEN

BK_UUID_LEN_16

BK_UUID_LEN_32

BK_UUID_LEN_128

BK_BD_ADDR_LEN
:   Bluetooth address length.


### Type Definitions

typedef int bt_err_t

typedef uint8_t bk_bt_octet16_t[BK_BT_OCTET16_LEN]

typedef uint8_t bk_bt_octet8_t[BK_BT_OCTET8_LEN]

typedef uint8_t bk_link_key_t[BK_BT_OCTET16_LEN]

typedef uint8_t bk_bd_addr_t[BK_BD_ADDR_LEN]
:   Bluetooth device address.

typedef void (*bt_cmd_cb_t)([bt_cmd_t](#_CPPv48bt_cmd_t "bt_cmd_t") cmd, [bt_cmd_param_t](#_CPPv414bt_cmd_param_t "bt_cmd_param_t") *param)
:   for sync bt api call return

    most bt api have bt_cmd_cb_t param, you must wait is callback.

    Param -
    :   cmd: cmd id.


        - param: param


### Enumerations

enum bk_bluetooth_status_t
:   Bluetooth status type, to indicate whether the bluetooth is ready.


    *Values:*

    enumerator BK_BLUETOOTH_STATUS_UNINITIALIZED
    :   Bluetooth not initialized

    enumerator BK_BLUETOOTH_STATUS_ENABLED
    :   Bluetooth initialized and enabled

enum BK_BT_CONTROLLER_STACK_TYPE
:   *Values:*

    enumerator BK_BT_CONTROLLER_STACK_TYPE_BTDM_5_2

    enumerator BK_BT_CONTROLLER_STACK_NOT_SUPPORT

enum BK_BT_HOST_STACK_TYPE
:   *Values:*

    enumerator BK_BT_HOST_STACK_TYPE_ETHERMIND

    enumerator BK_BT_HOST_STACK_TYPE_NOT_SUPPORT

enum bk_bt_status_t
:   Status Return Value.


    *Values:*

    enumerator BK_BT_STATUS_SUCCESS

    enumerator BK_BT_STATUS_UNKNOWN_HCI_COMMAND

    enumerator BK_BT_STATUS_UNKNOWN_CONNECTION_ID

    enumerator BK_BT_STATUS_HARDWARE_FAILURE

    enumerator BK_BT_STATUS_PAGE_TIMEOUT

    enumerator BK_BT_STATUS_AUTH_FAILURE

    enumerator BK_BT_STATUS_PIN_MISSING

    enumerator BK_BT_STATUS_MEMORY_CAPA_EXCEED

    enumerator BK_BT_STATUS_CON_TIMEOUT

    enumerator BK_BT_STATUS_CON_LIMIT_EXCEED

    enumerator BK_BT_STATUS_SYNC_CON_LIMIT_DEV_EXCEED

    enumerator BK_BT_STATUS_CON_ALREADY_EXISTS

    enumerator BK_BT_STATUS_COMMAND_DISALLOWED

    enumerator BK_BT_STATUS_CONN_REJ_LIMITED_RESOURCES

    enumerator BK_BT_STATUS_CONN_REJ_SECURITY_REASONS

    enumerator BK_BT_STATUS_CONN_REJ_UNACCEPTABLE_BDADDR

    enumerator BK_BT_STATUS_CONN_ACCEPT_TIMEOUT_EXCEED

    enumerator BK_BT_STATUS_UNSUPPORTED

    enumerator BK_BT_STATUS_INVALID_HCI_PARAM

    enumerator BK_BT_STATUS_REMOTE_USER_TERM_CON

    enumerator BK_BT_STATUS_REMOTE_DEV_TERM_LOW_RESOURCES

    enumerator BK_BT_STATUS_REMOTE_DEV_POWER_OFF

    enumerator BK_BT_STATUS_CON_TERM_BY_LOCAL_HOST

    enumerator BK_BT_STATUS_REPEATED_ATTEMPTS

    enumerator BK_BT_STATUS_PAIRING_NOT_ALLOWED

    enumerator BK_BT_STATUS_UNKNOWN_LMP_PDU

    enumerator BK_BT_STATUS_UNSUPPORTED_REMOTE_FEATURE

    enumerator BK_BT_STATUS_SCO_OFFSET_REJECTED

    enumerator BK_BT_STATUS_SCO_INTERVAL_REJECTED

    enumerator BK_BT_STATUS_SCO_AIR_MODE_REJECTED

    enumerator BK_BT_STATUS_INVALID_LMP_PARAM

    enumerator BK_BT_STATUS_UNSPECIFIED_ERROR

    enumerator BK_BT_STATUS_UNSUPPORTED_LMP_PARAM_VALUE

    enumerator BK_BT_STATUS_ROLE_CHANGE_NOT_ALLOWED

    enumerator BK_BT_STATUS_LMP_RSP_TIMEOUT

    enumerator BK_BT_STATUS_LMP_COLLISION

    enumerator BK_BT_STATUS_LMP_PDU_NOT_ALLOWED

    enumerator BK_BT_STATUS_ENC_MODE_NOT_ACCEPT

    enumerator BK_BT_STATUS_LINK_KEY_CANT_CHANGE

    enumerator BK_BT_STATUS_QOS_NOT_SUPPORTED

    enumerator BK_BT_STATUS_INSTANT_PASSED

    enumerator BK_BT_STATUS_PAIRING_WITH_UNIT_KEY_NOT_SUP

    enumerator BK_BT_STATUS_DIFF_TRANSACTION_COLLISION

    enumerator BK_BT_STATUS_QOS_UNACCEPTABLE_PARAM

    enumerator BK_BT_STATUS_QOS_REJECTED

    enumerator BK_BT_STATUS_CHANNEL_CLASS_NOT_SUP

    enumerator BK_BT_STATUS_INSUFFICIENT_SECURITY

    enumerator BK_BT_STATUS_PARAM_OUT_OF_MAND_RANGE

    enumerator BK_BT_STATUS_ROLE_SWITCH_PEND

    enumerator BK_BT_STATUS_RESERVED_SLOT_VIOLATION

    enumerator BK_BT_STATUS_ROLE_SWITCH_FAIL

    enumerator BK_BT_STATUS_EIR_TOO_LARGE

    enumerator BK_BT_STATUS_SP_NOT_SUPPORTED_HOST

    enumerator BK_BT_STATUS_HOST_BUSY_PAIRING

    enumerator BK_BT_STATUS_CONTROLLER_BUSY

    enumerator BK_BT_STATUS_UNACCEPTABLE_CONN_PARAM

    enumerator BK_BT_STATUS_ADV_TO

    enumerator BK_BT_STATUS_TERMINATED_MIC_FAILURE

    enumerator BK_BT_STATUS_CONN_FAILED_TO_BE_EST

    enumerator BK_BT_STATUS_CCA_REJ_USE_CLOCK_DRAG

    enumerator BK_BT_STATUS_TYPE0_SUBMAP_NOT_DEFINED

    enumerator BK_BT_STATUS_UNKNOWN_ADVERTISING_ID

    enumerator BK_BT_STATUS_LIMIT_REACHED

    enumerator BK_BT_STATUS_OPERATION_CANCELED_BY_HOST

    enumerator BK_BT_STATUS_PKT_TOO_LONG

    enumerator BK_BT_STATUS_TOO_LATE

    enumerator BK_BT_STATUS_TOO_EARLY

    enumerator BK_BT_STATUS_UNDEFINED

enum bt_cmd_t
:   *Values:*

    enumerator BT_CMD_INQUIRY

    enumerator BT_CMD_CREATE_CONNECT

    enumerator BT_CMD_DISCONNECT

    enumerator BT_CMD_SDP

    enumerator BT_CMD_READ_SCAN_ENABLE

    enumerator BT_CMD_WRITE_SCAN_ENABLE

    enumerator BT_CMD_MAX

enum bk_bt_dev_type_t
:   Bluetooth device type.


    *Values:*

    enumerator BK_BT_DEVICE_TYPE_BREDR

    enumerator BK_BT_DEVICE_TYPE_BLE

    enumerator BK_BT_DEVICE_TYPE_DUMO

enum bk_ble_addr_type_t
:   BLE device address type.


    *Values:*

    enumerator BLE_ADDR_TYPE_PUBLIC

    enumerator BLE_ADDR_TYPE_RANDOM

    enumerator BLE_ADDR_TYPE_RPA_PUBLIC
    :   when used with own addr, below means rpa effort, otherwise public when used with peer addr, below doesn’t used

    enumerator BLE_ADDR_TYPE_RPA_RANDOM
    :   when used with own addr, below means rpa effort, otherwise random when used with peer addr, below doesn’t used

enum bk_ble_wl_addr_type_t
:   white list address type


    *Values:*

    enumerator BLE_WL_ADDR_TYPE_PUBLIC

    enumerator BLE_WL_ADDR_TYPE_RANDOM


## 参考链接

> [API 参考：](../../api-reference/bluetooth.md "../../api-reference/bluetooth.md") 介绍蓝牙 API 接口。
>
> [蓝牙开发者指南：](../../developer-guide/bluetooth.md "../../developer-guide/bluetooth.md") 介绍蓝牙开发者指南。
