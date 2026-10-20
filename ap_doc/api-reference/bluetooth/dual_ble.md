---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/bluetooth/dual_ble.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ble-api"></a>

# 双模 BLE API

<a id="dual-ble-api"></a>

## Dual BLE API 分类

Dual BLE API 主要包括以下类型：

按功能划分的 Dual BLE API：
:   - BLE GAP 接口
    - BLE GATT 公共接口
    - BLE GATTC 接口
    - BLE GATTS 接口

<a id="id1"></a>

## 兼容性和扩展性

Dual BLE API 具备较好的扩展性和向后兼容性。多数 BLE 配置结构体中预留了字段，便于后续扩展。使用这些 API 时，应将预留字段初始化为 0，避免后续新增字段后影响兼容性。

<a id="id2"></a>

## 编程原则

重要

使用 BLE API 时建议遵循以下原则：
:   - 配置结构体中的预留字段应初始化为 0。
    - 使用 `BK_ERR_CHECK` 检查 BLE API 的返回值。
    - 不确定 API 用法时，优先参考 BLE 示例代码。
    - 不确定配置结构体字段如何初始化时，先使用默认配置宏，再按应用需求修改相关字段。
    - 不建议在 BLE 事件回调中执行耗时操作，可将事件转发到应用任务中处理。

<a id="id3"></a>

## 事件处理机制

Beken BLE driver 采用事件驱动方式工作。应用通过 BLE API 发起扫描、广播、连接、GATT 访问等操作，并在 BLE 事件回调中获取状态变化和操作结果。

<a id="api"></a>

## API 参考

<a id="bk-dm-gap-ble-h"></a>

## bk\_dm\_gap\_ble.h

`bk_dm_gap_ble.h` 提供 BLE GAP 的广播、扫描、连接和安全相关接口。

<a id="header-file"></a>

### Header File

- [bk\_dm\_gap\_ble.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_gap_ble.h)

<a id="functions"></a>

### Functions

<a id="_CPPv428bk_ble_gap_register_callback15bk_ble_gap_cb_t"></a>

<a id="_CPPv328bk_ble_gap_register_callback15bk_ble_gap_cb_t"></a> <a id="_CPPv228bk_ble_gap_register_callback15bk_ble_gap_cb_t"></a> <a id="bk_ble_gap_register_callback__bk_ble_gap_cb_t"></a> <a id="group__dm__gap__defines__v1_1ga9917a99477ffe8807a4c50cfe75859fd"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_register\_callback([bk\_ble\_gap\_cb\_t](#_CPPv415bk_ble_gap_cb_t "bk_ble_gap_cb_t") callback)
:   This function is called to occur gap event, such as scan result.

    参数
    :   **callback** – **\[in\]** callback function

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv429bk_ble_gap_update_conn_paramsP27bk_ble_conn_update_params_t"></a>

<a id="_CPPv329bk_ble_gap_update_conn_paramsP27bk_ble_conn_update_params_t"></a> <a id="_CPPv229bk_ble_gap_update_conn_paramsP27bk_ble_conn_update_params_t"></a> <a id="bk_ble_gap_update_conn_params__bk_ble_conn_update_params_tP"></a> <a id="group__dm__gap__defines__v1_1ga0f208da41839869d6d32570b6da7965f"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_update\_conn\_params([bk\_ble\_conn\_update\_params\_t](#_CPPv427bk_ble_conn_update_params_t "bk_ble_conn_update_params_t") \*params)
:   Update connection parameters, can only be used when connection is up.

    参数
    :   **params** – **\[in\]** \- connection update parameters

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv427bk_ble_gap_set_pkt_data_len12bk_bd_addr_t8uint16_t"></a>

<a id="_CPPv327bk_ble_gap_set_pkt_data_len12bk_bd_addr_t8uint16_t"></a> <a id="_CPPv227bk_ble_gap_set_pkt_data_len12bk_bd_addr_t8uint16_t"></a> <a id="bk_ble_gap_set_pkt_data_len__bk_bd_addr_t.uint16_t"></a> <a id="group__dm__gap__defines__v1_1gaf3f9fe23200eea6630c616fc77c850ae"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_pkt\_data\_len([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_device, uint16\_t tx\_data\_length)
:   This function is to set maximum LE data packet size.

    参数
    :   - **remote\_device** – **\[in\]** \- remote device
        - **tx\_data\_length** – **\[in\]** \- data len

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv424bk_ble_gap_set_rand_addr12bk_bd_addr_t"></a>

<a id="_CPPv324bk_ble_gap_set_rand_addr12bk_bd_addr_t"></a> <a id="_CPPv224bk_ble_gap_set_rand_addr12bk_bd_addr_t"></a> <a id="bk_ble_gap_set_rand_addr__bk_bd_addr_t"></a> <a id="group__dm__gap__defines__v1_1gac186d93c3e4cfb7360b4fb4ab5c12556"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_rand\_addr([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rand\_addr)
:   This function sets the static Random Address and Non-Resolvable Private Address for the application.

    参数
    :   **rand\_addr** – **\[in\]** the random address which should be setting

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv431bk_ble_gap_config_local_privacyb"></a>

<a id="_CPPv331bk_ble_gap_config_local_privacyb"></a> <a id="_CPPv231bk_ble_gap_config_local_privacyb"></a> <a id="bk_ble_gap_config_local_privacy__b"></a> <a id="group__dm__gap__defines__v1_1ga342b67edf9c5723e0330d55c75e5b682"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_config\_local\_privacy(bool privacy\_enable)
:   Enable/disable privacy on the local device.

    参数
    :   **privacy\_enable** – **\[in\]** \- enable/disable privacy on remote device.

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv428bk_ble_gap_config_local_icon8uint16_t"></a>

<a id="_CPPv328bk_ble_gap_config_local_icon8uint16_t"></a> <a id="_CPPv228bk_ble_gap_config_local_icon8uint16_t"></a> <a id="bk_ble_gap_config_local_icon__uint16_t"></a> <a id="group__dm__gap__defines__v1_1gabf99f44df71af093421f027dba5650e4"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_config\_local\_icon(uint16\_t icon)
:   set local gap appearance icon

    参数
    :   **icon** – **\[in\]** \- External appearance value, these values are defined by the Bluetooth SIG, please refer to <https://specificationrefs.bluetooth.com/assigned-values/Appearance%20Values.pdf>

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv427bk_ble_gap_update_whitelistb12bk_bd_addr_t21bk_ble_wl_addr_type_t"></a>

<a id="_CPPv327bk_ble_gap_update_whitelistb12bk_bd_addr_t21bk_ble_wl_addr_type_t"></a> <a id="_CPPv227bk_ble_gap_update_whitelistb12bk_bd_addr_t21bk_ble_wl_addr_type_t"></a> <a id="bk_ble_gap_update_whitelist__b.bk_bd_addr_t.bk_ble_wl_addr_type_t"></a> <a id="group__dm__gap__defines__v1_1ga8d6f653d42047344e380993ca5885d15"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_update\_whitelist(bool add\_remove, [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda, [bk\_ble\_wl\_addr\_type\_t](#_CPPv421bk_ble_wl_addr_type_t "bk_ble_wl_addr_type_t") wl\_addr\_type)
:   Add or remove device from white list.

    参数
    :   - **add\_remove** – **\[in\]** the value is true if added the ble device to the white list, and false remove to the white list.
        - **remote\_bda** – **\[in\]** the remote device address add/remove from the white list.
        - **wl\_addr\_type** – **\[in\]** whitelist address type

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv426bk_ble_gap_clear_whitelistv"></a>

<a id="_CPPv326bk_ble_gap_clear_whitelistv"></a> <a id="_CPPv226bk_ble_gap_clear_whitelistv"></a> <a id="bk_ble_gap_clear_whitelist__void"></a> <a id="group__dm__gap__defines__v1_1ga06e5f393ecfd8c2e0e709e2b72257650"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_clear\_whitelist(void)
:   Clear all white list.

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv429bk_ble_gap_get_whitelist_sizeP8uint16_t"></a>

<a id="_CPPv329bk_ble_gap_get_whitelist_sizeP8uint16_t"></a> <a id="_CPPv229bk_ble_gap_get_whitelist_sizeP8uint16_t"></a> <a id="bk_ble_gap_get_whitelist_size__uint16_tP"></a> <a id="group__dm__gap__defines__v1_1ga0eb5072b71442fbec0708beaa431e0d0"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_get\_whitelist\_size(uint16\_t \*length)
:   Get the whitelist size in the controller.

    参数
    :   **length** – **\[out\]** the white list length.

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv426bk_ble_gap_set_device_namePKc"></a>

<a id="_CPPv326bk_ble_gap_set_device_namePKc"></a> <a id="_CPPv226bk_ble_gap_set_device_namePKc"></a> <a id="bk_ble_gap_set_device_name__cCP"></a> <a id="group__dm__gap__defines__v1_1gaa20047de9f09f91adb13253c5fb294dc"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_device\_name(const char \*name)
:   Set device name to the local device.

    参数
    :   **name** – **\[in\]** \- device name.

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv426bk_ble_gap_get_device_namePcP8uint32_t"></a>

<a id="_CPPv326bk_ble_gap_get_device_namePcP8uint32_t"></a> <a id="_CPPv226bk_ble_gap_get_device_namePcP8uint32_t"></a> <a id="bk_ble_gap_get_device_name__cP.uint32_tP"></a> <a id="group__dm__gap__defines__v1_1ga4cb944f13793fb905ee33b508f03dd4f"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_get\_device\_name(char \*name, uint32\_t \*size)
:   Get device name of the local device.

    参数
    :   - **name** – **\[out\]** \- device name.
        - **size** – **\[inout\]** \- name output max size, and real size after return.

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv430bk_ble_gap_get_local_used_addr12bk_bd_addr_tP7uint8_t"></a>

<a id="_CPPv330bk_ble_gap_get_local_used_addr12bk_bd_addr_tP7uint8_t"></a> <a id="_CPPv230bk_ble_gap_get_local_used_addr12bk_bd_addr_tP7uint8_t"></a> <a id="bk_ble_gap_get_local_used_addr__bk_bd_addr_t.uint8_tP"></a> <a id="group__dm__gap__defines__v1_1ga6fd3928d7c2e5158d3ee60fcf2226bb7"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_get\_local\_used\_addr([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") local\_used\_addr, uint8\_t \*addr\_type)
:   This function is called to get local used address and address type. uint8\_t \*bk\_bt\_dev\_get\_address(void) get the public address.

    参数
    :   - **local\_used\_addr** – **\[in\]** \- current local used ble address (six bytes)
        - **addr\_type** – **\[in\]** \- ble address type

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv420bk_ble_gap_read_rssi12bk_bd_addr_t"></a>

<a id="_CPPv320bk_ble_gap_read_rssi12bk_bd_addr_t"></a> <a id="_CPPv220bk_ble_gap_read_rssi12bk_bd_addr_t"></a> <a id="bk_ble_gap_read_rssi__bk_bd_addr_t"></a> <a id="group__dm__gap__defines__v1_1gaa81bdc6df672c6660bd8b97af757db53"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_read\_rssi([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_addr)
:   This function is called to read the RSSI of remote device. The address of link policy results are returned in the gap callback function with BK\_GAP\_BLE\_READ\_RSSI\_COMPLETE\_EVT event.

    参数
    :   **remote\_addr** – **\[in\]** : The remote connection device address.

    返回
    :   - BK\_OK : success
        - other : failed

<a id="_CPPv429bk_ble_gap_set_security_param17bk_ble_sm_param_tPv7uint8_t"></a>

<a id="_CPPv329bk_ble_gap_set_security_param17bk_ble_sm_param_tPv7uint8_t"></a> <a id="_CPPv229bk_ble_gap_set_security_param17bk_ble_sm_param_tPv7uint8_t"></a> <a id="bk_ble_gap_set_security_param__bk_ble_sm_param_t.voidP.uint8_t"></a> <a id="group__dm__gap__defines__v1_1ga05b745e73e813e94fc14aa147b63f049"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_security\_param([bk\_ble\_sm\_param\_t](#_CPPv417bk_ble_sm_param_t "bk_ble_sm_param_t") param\_type, void \*value, uint8\_t len)
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
    :   - **param\_type** – **\[in\]** : the type of the param which to be set
        - **value** – **\[in\]** : the param value
        - **len** – **\[in\]** : the length of the param value

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv423bk_ble_gap_security_rsp12bk_bd_addr_tb"></a>

<a id="_CPPv323bk_ble_gap_security_rsp12bk_bd_addr_tb"></a> <a id="_CPPv223bk_ble_gap_security_rsp12bk_bd_addr_tb"></a> <a id="bk_ble_gap_security_rsp__bk_bd_addr_t.b"></a> <a id="group__dm__gap__defines__v1_1ga1754ad54078e742c1fc9ce2eb902286a"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_security\_rsp([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, bool accept)
:   Grant security request access.

    参数
    :   - **bd\_addr** – **\[in\]** : BD address of the peer
        - **accept** – **\[in\]** : accept the security request or not

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv421bk_ble_set_encryption12bk_bd_addr_t16bk_ble_sec_act_t"></a>

<a id="_CPPv321bk_ble_set_encryption12bk_bd_addr_t16bk_ble_sec_act_t"></a> <a id="_CPPv221bk_ble_set_encryption12bk_bd_addr_t16bk_ble_sec_act_t"></a> <a id="bk_ble_set_encryption__bk_bd_addr_t.bk_ble_sec_act_t"></a> <a id="group__dm__gap__defines__v1_1ga946737f310a41a079f4ca251bb89f9f9"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_set\_encryption([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, [bk\_ble\_sec\_act\_t](#_CPPv416bk_ble_sec_act_t "bk_ble_sec_act_t") sec\_act)
:   Set a gap parameter value. Use this function to change the default GAP parameter values.

    参数
    :   - **bd\_addr** – **\[in\]** : the address of the peer device need to encryption
        - **sec\_act** – **\[in\]** : This is the security action to indicate what kind of BLE security level is required for the BLE link if the BLE is supported

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv420bk_ble_passkey_reply12bk_bd_addr_tb8uint32_t"></a>

<a id="_CPPv320bk_ble_passkey_reply12bk_bd_addr_tb8uint32_t"></a> <a id="_CPPv220bk_ble_passkey_reply12bk_bd_addr_tb8uint32_t"></a> <a id="bk_ble_passkey_reply__bk_bd_addr_t.b.uint32_t"></a> <a id="group__dm__gap__defines__v1_1ga0f030a1f3b3502255e3b5908eaeb5df7"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_passkey\_reply([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, bool accept, uint32\_t passkey)
:   Reply the key value to the peer device in the legacy connection stage.

    参数
    :   - **bd\_addr** – **\[in\]** : BD address of the peer
        - **accept** – **\[in\]** : passkey entry successful or declined.
        - **passkey** – **\[in\]** : passkey value, must be a 6 digit number, can be lead by 0\.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv420bk_ble_confirm_reply12bk_bd_addr_tb"></a>

<a id="_CPPv320bk_ble_confirm_reply12bk_bd_addr_tb"></a> <a id="_CPPv220bk_ble_confirm_reply12bk_bd_addr_tb"></a> <a id="bk_ble_confirm_reply__bk_bd_addr_t.b"></a> <a id="group__dm__gap__defines__v1_1ga3da0593f15d8b516ea83dc9b530d12b7"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_confirm\_reply([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, bool accept)
:   Reply the confirm value to the peer device in the secure connection stage.

    参数
    :   - **bd\_addr** – **\[in\]** : BD address of the peer device
        - **accept** – **\[in\]** : numbers to compare are the same or different.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv421bk_ble_pair_key_reply12bk_bd_addr_tb17bk_ble_key_type_tPv8uint32_t"></a>

<a id="_CPPv321bk_ble_pair_key_reply12bk_bd_addr_tb17bk_ble_key_type_tPv8uint32_t"></a> <a id="_CPPv221bk_ble_pair_key_reply12bk_bd_addr_tb17bk_ble_key_type_tPv8uint32_t"></a> <a id="bk_ble_pair_key_reply__bk_bd_addr_t.b.bk_ble_key_type_t.voidP.uint32_t"></a> <a id="group__dm__gap__defines__v1_1ga6b3056a5207ffac005c828b34e9187d3"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_pair\_key\_reply([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, bool accept, [bk\_ble\_key\_type\_t](#_CPPv417bk_ble_key_type_t "bk_ble_key_type_t") type, void \*data, uint32\_t len)
:   Reply the save key.

    参数
    :   - **bd\_addr** – **\[in\]** : BD address of the peer device
        - **accept** – **\[in\]** : true or false
        - **type** – **\[in\]** : key type.
        - **data** – **\[in\]** : key data, when type is: BK\_LE\_KEY\_LENC, data is [bk\_ble\_lenc\_keys\_t](#structbk__ble__lenc__keys__t). When accept is false, data and len will be ignore.
        - **len** – **\[in\]** : key len

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv425bk_ble_remove_bond_device12bk_bd_addr_t"></a>

<a id="_CPPv325bk_ble_remove_bond_device12bk_bd_addr_t"></a> <a id="_CPPv225bk_ble_remove_bond_device12bk_bd_addr_t"></a> <a id="bk_ble_remove_bond_device__bk_bd_addr_t"></a> <a id="group__dm__gap__defines__v1_1ga3cafe8f0a14a80152db3eb3813ccda3f"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_remove\_bond\_device([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   Removes a device from the security database list of peer device. It manages unpairing event while connected.

    参数
    :   **bd\_addr** – **\[in\]** : BD address of the peer device

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv426bk_ble_get_bond_device_numv"></a>

<a id="_CPPv326bk_ble_get_bond_device_numv"></a> <a id="_CPPv226bk_ble_get_bond_device_numv"></a> <a id="bk_ble_get_bond_device_num__void"></a> <a id="group__dm__gap__defines__v1_1ga197bcd6bbaf7eabfddabce66be9fad92"></a> int bk\_ble\_get\_bond\_device\_num(void)
:   Get the device number from the security database list of peer device. It will return the device bonded number immediately.

    返回
    :   \- \>\= 0 : bonded devices number.

        - BK\_FAIL : failed

<a id="_CPPv427bk_ble_get_bond_device_listPiP17bk_ble_bond_dev_t"></a>

<a id="_CPPv327bk_ble_get_bond_device_listPiP17bk_ble_bond_dev_t"></a> <a id="_CPPv227bk_ble_get_bond_device_listPiP17bk_ble_bond_dev_t"></a> <a id="bk_ble_get_bond_device_list__iP.bk_ble_bond_dev_tP"></a> <a id="group__dm__gap__defines__v1_1ga0e8d07a123d926760b7b66aeaea417f8"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_get\_bond\_device\_list(int \*dev\_num, [bk\_ble\_bond\_dev\_t](#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") \*dev\_list)
:   Get the device from the security database list of peer device. It will return the device bonded information immediately.

    参数
    :   - **dev\_num** – **\[inout\]** Indicate the dev\_list array(buffer) size as input. If dev\_num is large enough, it means the actual number as output. Suggest that dev\_num value equal to [bk\_ble\_get\_bond\_device\_num()](#group__dm__gap__defines__v1_1ga197bcd6bbaf7eabfddabce66be9fad92).
        - **dev\_list** – **\[out\]** an array(buffer) of `bk_ble_bond_dev_t` type. Use for storing the bonded devices address. The dev\_list should be allocated by who call this API.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv418bk_ble_gap_connectP27bk_gap_create_conn_params_t"></a>

<a id="_CPPv318bk_ble_gap_connectP27bk_gap_create_conn_params_t"></a> <a id="_CPPv218bk_ble_gap_connectP27bk_gap_create_conn_params_t"></a> <a id="bk_ble_gap_connect__bk_gap_create_conn_params_tP"></a> <a id="group__dm__gap__defines__v1_1ga23e98c1260203e5602e76c2e7daec711"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_connect([bk\_gap\_create\_conn\_params\_t](#_CPPv427bk_gap_create_conn_params_t "bk_gap_create_conn_params_t") \*param)
:   This function is to connect the physical connection of the peer device.

    **Attention**
    :   1\. local\_addr\_type can be BLE\_ADDR\_TYPE\_PUBLIC \~ BLE\_ADDR\_TYPE\_RPA\_RANDOM.

    **Attention**
    :   2\. if local\_addr\_type is BLE\_ADDR\_TYPE\_PUBLIC, and initiator\_filter\_policy policy not enable, host will use local public addr/peer\_addr/peer\_addr\_type to connect.

    **Attention**
    :   3\. if local\_addr\_type is BLE\_ADDR\_TYPE\_RANDOM, and initiator\_filter\_policy policy not enable, host will use peer\_addr/peer\_addr\_type, random addr that set in bk\_ble\_gap\_set\_adv\_rand\_addr to connect.

    **Attention**
    :   4\. if local\_addr\_type is BLE\_ADDR\_TYPE\_RPA\_PUBLIC, host will try search bond list’s nominal addr by peer\_addr/peer\_addr\_type, if found and BK\_LE\_KEY\_PID \| BK\_LE\_KEY\_LID present then host will generate RPA addr to connect peer RPA ADV, otherwise see attention 2\.

    **Attention**
    :   5\. if local\_addr\_type is BLE\_ADDR\_TYPE\_RPA\_RANDOM, host will try search bond list’s nominal addr by peer\_addr/peer\_addr\_type, if found and BK\_LE\_KEY\_PID \| BK\_LE\_KEY\_LID present then host will generate RPA addr to connect peer RPA ADV, otherwise see attention 3\.

    参数
    :   **param** – **\[in\]** : connect param

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv421bk_ble_gap_disconnect12bk_bd_addr_t"></a>

<a id="_CPPv321bk_ble_gap_disconnect12bk_bd_addr_t"></a> <a id="_CPPv221bk_ble_gap_disconnect12bk_bd_addr_t"></a> <a id="bk_ble_gap_disconnect__bk_bd_addr_t"></a> <a id="group__dm__gap__defines__v1_1ga26f6b220aba1cc0c824e75249f55a274"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_disconnect([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_device)
:   This function is to disconnect the physical connection of the peer device.

    参数
    :   **remote\_device** – **\[in\]** : BD address of the peer device

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv425bk_ble_gap_cancel_connectv"></a>

<a id="_CPPv325bk_ble_gap_cancel_connectv"></a> <a id="_CPPv225bk_ble_gap_cancel_connectv"></a> <a id="bk_ble_gap_cancel_connect__void"></a> <a id="group__dm__gap__defines__v1_1gabbcfef53af5e4760f1199d58daf87544"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_cancel\_connect(void)
:   This function is to cancel the physical connection that have not connect completed.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv430bk_ble_get_current_conn_params12bk_bd_addr_tP20bk_gap_conn_params_t"></a>

<a id="_CPPv330bk_ble_get_current_conn_params12bk_bd_addr_tP20bk_gap_conn_params_t"></a> <a id="_CPPv230bk_ble_get_current_conn_params12bk_bd_addr_tP20bk_gap_conn_params_t"></a> <a id="bk_ble_get_current_conn_params__bk_bd_addr_t.bk_gap_conn_params_tP"></a> <a id="group__dm__gap__defines__v1_1gab9b7072fbc5b8c0e78a46561b2ddf28a"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_get\_current\_conn\_params([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, [bk\_gap\_conn\_params\_t](#_CPPv420bk_gap_conn_params_t "bk_gap_conn_params_t") \*conn\_params)
:   This function is called to read the connection parameters information of the device.

    参数
    :   - **bd\_addr** – **\[in\]** BD address of the peer device.
        - **conn\_params** – **\[out\]** the connection parameters information

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv423bk_gap_ble_set_channels19bk_ble_gap_channels"></a>

<a id="_CPPv323bk_gap_ble_set_channels19bk_ble_gap_channels"></a> <a id="_CPPv223bk_gap_ble_set_channels19bk_ble_gap_channels"></a> <a id="bk_gap_ble_set_channels__bk_ble_gap_channels"></a> <a id="group__dm__gap__defines__v1_1ga9fee1ea31a1ed4ff8a29970be97e6c67"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_gap\_ble\_set\_channels([bk\_ble\_gap\_channels](#_CPPv419bk_ble_gap_channels "bk_ble_gap_channels") channels)
:   BLE set channels.

    参数
    :   **channels** – **\[in\]** : The n th such field (in the range 0 to 36\) contains the value for the link layer channel index n. 0 means channel n is bad. 1 means channel n is unknown. The most significant bits are reserved and shall be set to 0\. At least one channel shall be marked as unknown.

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv419bk_ble_gap_read_phy12bk_bd_addr_t"></a>

<a id="_CPPv319bk_ble_gap_read_phy12bk_bd_addr_t"></a> <a id="_CPPv219bk_ble_gap_read_phy12bk_bd_addr_t"></a> <a id="bk_ble_gap_read_phy__bk_bd_addr_t"></a> <a id="group__dm__gap__defines__v1_1gabf135b4794315977e5b0af6da31eb519"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_read\_phy([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   This function is used to read the current transmitter PHY and receiver PHY on the connection identified by remote address.

    参数
    :   **bd\_addr** – **\[in\]** : BD address of the peer device

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv436bk_ble_gap_set_preferred_default_phy21bk_ble_gap_phy_mask_t21bk_ble_gap_phy_mask_t"></a>

<a id="_CPPv336bk_ble_gap_set_preferred_default_phy21bk_ble_gap_phy_mask_t21bk_ble_gap_phy_mask_t"></a> <a id="_CPPv236bk_ble_gap_set_preferred_default_phy21bk_ble_gap_phy_mask_t21bk_ble_gap_phy_mask_t"></a> <a id="bk_ble_gap_set_preferred_default_phy__bk_ble_gap_phy_mask_t.bk_ble_gap_phy_mask_t"></a> <a id="group__dm__gap__defines__v1_1ga3ae013413484932fd8bf64a6c8399109"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_preferred\_default\_phy([bk\_ble\_gap\_phy\_mask\_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") tx\_phy\_mask, [bk\_ble\_gap\_phy\_mask\_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") rx\_phy\_mask)
:   This function is used to allows the Host to specify its preferred values for the transmitter PHY and receiver PHY to be used for all subsequent connections over the LE transport.

    参数
    :   - **tx\_phy\_mask** – **\[in\]** : indicates the transmitter PHYs that the Host prefers the Controller to use
        - **rx\_phy\_mask** – **\[in\]** : indicates the receiver PHYs that the Host prefers the Controller to use

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv428bk_ble_gap_set_preferred_phy12bk_bd_addr_t21bk_ble_gap_all_phys_t21bk_ble_gap_phy_mask_t21bk_ble_gap_phy_mask_t31bk_ble_gap_prefer_phy_options_t"></a>

<a id="_CPPv328bk_ble_gap_set_preferred_phy12bk_bd_addr_t21bk_ble_gap_all_phys_t21bk_ble_gap_phy_mask_t21bk_ble_gap_phy_mask_t31bk_ble_gap_prefer_phy_options_t"></a> <a id="_CPPv228bk_ble_gap_set_preferred_phy12bk_bd_addr_t21bk_ble_gap_all_phys_t21bk_ble_gap_phy_mask_t21bk_ble_gap_phy_mask_t31bk_ble_gap_prefer_phy_options_t"></a> <a id="bk_ble_gap_set_preferred_phy__bk_bd_addr_t.bk_ble_gap_all_phys_t.bk_ble_gap_phy_mask_t.bk_ble_gap_phy_mask_t.bk_ble_gap_prefer_phy_options_t"></a> <a id="group__dm__gap__defines__v1_1gac4bde0c1a3ff9083721a79b2c7d1c882"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_preferred\_phy([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, [bk\_ble\_gap\_all\_phys\_t](#_CPPv421bk_ble_gap_all_phys_t "bk_ble_gap_all_phys_t") all\_phys\_mask, [bk\_ble\_gap\_phy\_mask\_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") tx\_phy\_mask, [bk\_ble\_gap\_phy\_mask\_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") rx\_phy\_mask, [bk\_ble\_gap\_prefer\_phy\_options\_t](#_CPPv431bk_ble_gap_prefer_phy_options_t "bk_ble_gap_prefer_phy_options_t") phy\_options)
:   This function is used to set the PHY preferences for the connection identified by the remote address. The Controller might not be able to make the change (e.g. because the peer does not support the requested PHY) or may decide that the current PHY is preferable.

    参数
    :   - **bd\_addr** – **\[in\]** : remote address
        - **all\_phys\_mask** – **\[in\]** : a bit field that allows the Host to specify
        - **tx\_phy\_mask** – **\[in\]** : a bit field that indicates the transmitter PHYs that the Host prefers the Controller to use
        - **rx\_phy\_mask** – **\[in\]** : a bit field that indicates the receiver PHYs that the Host prefers the Controller to use
        - **phy\_options** – **\[in\]** : a bit field that allows the Host to specify options for PHYs

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv428bk_ble_gap_set_adv_rand_addr7uint8_t12bk_bd_addr_t"></a>

<a id="_CPPv328bk_ble_gap_set_adv_rand_addr7uint8_t12bk_bd_addr_t"></a> <a id="_CPPv228bk_ble_gap_set_adv_rand_addr7uint8_t12bk_bd_addr_t"></a> <a id="bk_ble_gap_set_adv_rand_addr__uint8_t.bk_bd_addr_t"></a> <a id="group__dm__gap__defines__v1_1gab6e463cecf57188342622ec0bd4585e2"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_adv\_rand\_addr(uint8\_t instance, [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rand\_addr)
:   This function is used by the Host to set the random device address specified by the Random\_Address parameter.

    参数
    :   - **instance** – **\[in\]** : Used to identify an advertising set
        - **rand\_addr** – **\[in\]** : Random Device Address

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv425bk_ble_gap_set_adv_params7uint8_tPK27bk_ble_gap_ext_adv_params_t"></a>

<a id="_CPPv325bk_ble_gap_set_adv_params7uint8_tPK27bk_ble_gap_ext_adv_params_t"></a> <a id="_CPPv225bk_ble_gap_set_adv_params7uint8_tPK27bk_ble_gap_ext_adv_params_t"></a> <a id="bk_ble_gap_set_adv_params__uint8_t.bk_ble_gap_ext_adv_params_tCP"></a> <a id="group__dm__gap__defines__v1_1gaeac87861910d4c04a06e55d514158ed5"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_adv\_params(uint8\_t instance, const [bk\_ble\_gap\_ext\_adv\_params\_t](#_CPPv427bk_ble_gap_ext_adv_params_t "bk_ble_gap_ext_adv_params_t") \*params)
:   This function is used by the Host to set the advertising parameters.

    **Attention**
    :   1\. local\_addr\_type can be BLE\_ADDR\_TYPE\_PUBLIC \~ BLE\_ADDR\_TYPE\_RPA\_RANDOM.

    **Attention**
    :   2\. if local\_addr\_type is BLE\_ADDR\_TYPE\_PUBLIC, host will use public addr to send adv.

    **Attention**
    :   3\. if local\_addr\_type is BLE\_ADDR\_TYPE\_RANDOM, host will use random addr that set in bk\_ble\_gap\_set\_adv\_rand\_addr to send adv.

    **Attention**
    :   4\. if local\_addr\_type is BLE\_ADDR\_TYPE\_RPA\_PUBLIC, host will try search bond list by peer\_addr/peer\_addr\_type, if found and BK\_LE\_KEY\_PID \| BK\_LE\_KEY\_LID present then host will generate RPA addr to send ADV, otherwise see attention 2\.

    **Attention**
    :   5\. if local\_addr\_type is BLE\_ADDR\_TYPE\_RPA\_RANDOM, host will try search bond list by peer\_addr/peer\_addr\_type, if found and BK\_LE\_KEY\_PID \| BK\_LE\_KEY\_LID present then host will generate RPA addr to send ADV, otherwise see attention 3\.

    参数
    :   - **instance** – **\[in\]** : identifies the advertising set whose parameters are being configured.
        - **params** – **\[in\]** : advertising parameters

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv423bk_ble_gap_set_adv_dataP17bk_ble_adv_data_t"></a>

<a id="_CPPv323bk_ble_gap_set_adv_dataP17bk_ble_adv_data_t"></a> <a id="_CPPv223bk_ble_gap_set_adv_dataP17bk_ble_adv_data_t"></a> <a id="bk_ble_gap_set_adv_data__bk_ble_adv_data_tP"></a> <a id="group__dm__gap__defines__v1_1ga9d0f34bdc90ddc13e353248f9056fa1b"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_adv\_data([bk\_ble\_adv\_data\_t](#_CPPv417bk_ble_adv_data_t "bk_ble_adv_data_t") \*adv\_data)
:   This function is used to set the data used in advertising PDUs that have a data field.

    参数
    :   - **instance** – **\[in\]** : identifies the advertising set whose data are being configured
        - **length** – **\[in\]** : data length
        - **data** – **\[in\]** : data information

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv427bk_ble_gap_set_adv_data_raw7uint8_t8uint16_tPK7uint8_t"></a>

<a id="_CPPv327bk_ble_gap_set_adv_data_raw7uint8_t8uint16_tPK7uint8_t"></a> <a id="_CPPv227bk_ble_gap_set_adv_data_raw7uint8_t8uint16_tPK7uint8_t"></a> <a id="bk_ble_gap_set_adv_data_raw__uint8_t.uint16_t.uint8_tCP"></a> <a id="group__dm__gap__defines__v1_1ga49c6094f46f95b399b33ef502861666d"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_adv\_data\_raw(uint8\_t instance, uint16\_t length, const uint8\_t \*data)
:   This function is used to set the data used in advertising PDUs that have a data field.

    参数
    :   - **instance** – **\[in\]** : identifies the advertising set whose data are being configured
        - **length** – **\[in\]** : data length
        - **data** – **\[in\]** : data information

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv432bk_ble_gap_set_scan_rsp_data_raw7uint8_t8uint16_tPK7uint8_t"></a>

<a id="_CPPv332bk_ble_gap_set_scan_rsp_data_raw7uint8_t8uint16_tPK7uint8_t"></a> <a id="_CPPv232bk_ble_gap_set_scan_rsp_data_raw7uint8_t8uint16_tPK7uint8_t"></a> <a id="bk_ble_gap_set_scan_rsp_data_raw__uint8_t.uint16_t.uint8_tCP"></a> <a id="group__dm__gap__defines__v1_1ga21aa74e54dc3a545cf0dee85b5893586"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_scan\_rsp\_data\_raw(uint8\_t instance, uint16\_t length, const uint8\_t \*scan\_rsp\_data)
:   This function is used to provide scan response data used in scanning response PDUs.

    参数
    :   - **instance** – **\[in\]** : identifies the advertising set whose response data are being configured.
        - **length** – **\[in\]** : responsedata length
        - **scan\_rsp\_data** – **\[in\]** : response data information

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv420bk_ble_gap_adv_start7uint8_tPK20bk_ble_gap_ext_adv_t"></a>

<a id="_CPPv320bk_ble_gap_adv_start7uint8_tPK20bk_ble_gap_ext_adv_t"></a> <a id="_CPPv220bk_ble_gap_adv_start7uint8_tPK20bk_ble_gap_ext_adv_t"></a> <a id="bk_ble_gap_adv_start__uint8_t.bk_ble_gap_ext_adv_tCP"></a> <a id="group__dm__gap__defines__v1_1gaee5d4fc40c7627a6bd4db74dd541698f"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_adv\_start(uint8\_t num\_adv, const [bk\_ble\_gap\_ext\_adv\_t](#_CPPv420bk_ble_gap_ext_adv_t "bk_ble_gap_ext_adv_t") \*ext\_adv)
:   This function is used to request the Controller to enable one or more advertising sets using the advertising sets identified by the instance parameter.

    参数
    :   - **num\_adv** – **\[in\]** : Number of advertising sets to enable or disable
        - **ext\_adv** – **\[in\]** : adv parameters

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv419bk_ble_gap_adv_stop7uint8_tPK7uint8_t"></a>

<a id="_CPPv319bk_ble_gap_adv_stop7uint8_tPK7uint8_t"></a> <a id="_CPPv219bk_ble_gap_adv_stop7uint8_tPK7uint8_t"></a> <a id="bk_ble_gap_adv_stop__uint8_t.uint8_tCP"></a> <a id="group__dm__gap__defines__v1_1ga9e850209592fe50f68c2b2a5350d8a46"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_adv\_stop(uint8\_t num\_adv, const uint8\_t \*ext\_adv\_inst)
:   This function is used to request the Controller to disable one or more advertising sets using the advertising sets identified by the instance parameter.

    参数
    :   - **num\_adv** – **\[in\]** : Number of advertising sets to enable or disable
        - **ext\_adv\_inst** – **\[in\]** : ext adv instance

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv425bk_ble_gap_adv_set_remove7uint8_t"></a>

<a id="_CPPv325bk_ble_gap_adv_set_remove7uint8_t"></a> <a id="_CPPv225bk_ble_gap_adv_set_remove7uint8_t"></a> <a id="bk_ble_gap_adv_set_remove__uint8_t"></a> <a id="group__dm__gap__defines__v1_1ga5d292b822dd453f6b5b8b9658c1fee3c"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_adv\_set\_remove(uint8\_t instance)
:   This function is used to remove an advertising set from the Controller.

    参数
    :   **instance** – **\[in\]** : Used to identify an advertising set

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv424bk_ble_gap_adv_set_clearv"></a>

<a id="_CPPv324bk_ble_gap_adv_set_clearv"></a> <a id="_CPPv224bk_ble_gap_adv_set_clearv"></a> <a id="bk_ble_gap_adv_set_clear__void"></a> <a id="group__dm__gap__defines__v1_1gad0aae5b11f2ad4aa2a8bafadef087a6b"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_adv\_set\_clear(void)
:   This function is used to remove all existing advertising sets from the Controller.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv434bk_ble_gap_set_periodic_adv_params7uint8_tPK32bk_ble_gap_periodic_adv_params_t"></a>

<a id="_CPPv334bk_ble_gap_set_periodic_adv_params7uint8_tPK32bk_ble_gap_periodic_adv_params_t"></a> <a id="_CPPv234bk_ble_gap_set_periodic_adv_params7uint8_tPK32bk_ble_gap_periodic_adv_params_t"></a> <a id="bk_ble_gap_set_periodic_adv_params__uint8_t.bk_ble_gap_periodic_adv_params_tCP"></a> <a id="group__dm__gap__defines__v1_1gae00220368016dad76d012cf5b6ec1b8e"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_periodic\_adv\_params(uint8\_t instance, const [bk\_ble\_gap\_periodic\_adv\_params\_t](#_CPPv432bk_ble_gap_periodic_adv_params_t "bk_ble_gap_periodic_adv_params_t") \*params)
:   This function is used by the Host to set the parameters for periodic advertising.

    参数
    :   - **instance** – **\[in\]** : identifies the advertising set whose periodic advertising parameters are being configured.
        - **params** – **\[in\]** : periodic adv parameters

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv436bk_ble_gap_set_periodic_adv_data_raw7uint8_t8uint16_tPK7uint8_t"></a>

<a id="_CPPv336bk_ble_gap_set_periodic_adv_data_raw7uint8_t8uint16_tPK7uint8_t"></a> <a id="_CPPv236bk_ble_gap_set_periodic_adv_data_raw7uint8_t8uint16_tPK7uint8_t"></a> <a id="bk_ble_gap_set_periodic_adv_data_raw__uint8_t.uint16_t.uint8_tCP"></a> <a id="group__dm__gap__defines__v1_1ga82030e61cbafab59b155864f8bed60d7"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_periodic\_adv\_data\_raw(uint8\_t instance, uint16\_t length, const uint8\_t \*data)
:   This function is used to set the data used in periodic advertising PDUs.

    参数
    :   - **instance** – **\[in\]** : identifies the advertising set whose periodic advertising parameters are being configured.
        - **length** – **\[in\]** : the length of periodic data
        - **data** – **\[in\]** : periodic data information

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv429bk_ble_gap_periodic_adv_start7uint8_t"></a>

<a id="_CPPv329bk_ble_gap_periodic_adv_start7uint8_t"></a> <a id="_CPPv229bk_ble_gap_periodic_adv_start7uint8_t"></a> <a id="bk_ble_gap_periodic_adv_start__uint8_t"></a> <a id="group__dm__gap__defines__v1_1gae741a2b69b62c7d46a2b7151ac067253"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_periodic\_adv\_start(uint8\_t instance)
:   This function is used to request the Controller to enable the periodic advertising for the advertising set specified.

    参数
    :   **instance** – **\[in\]** : Used to identify an advertising set

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv428bk_ble_gap_periodic_adv_stop7uint8_t"></a>

<a id="_CPPv328bk_ble_gap_periodic_adv_stop7uint8_t"></a> <a id="_CPPv228bk_ble_gap_periodic_adv_stop7uint8_t"></a> <a id="bk_ble_gap_periodic_adv_stop__uint8_t"></a> <a id="group__dm__gap__defines__v1_1gad29049f03cce43b7da93fb9ba9058d6c"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_periodic\_adv\_stop(uint8\_t instance)
:   This function is used to request the Controller to disable the periodic advertising for the advertising set specified.

    参数
    :   **instance** – **\[in\]** : Used to identify an advertising set

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv435bk_ble_gap_periodic_adv_create_syncPK37bk_ble_gap_periodic_adv_sync_params_t"></a>

<a id="_CPPv335bk_ble_gap_periodic_adv_create_syncPK37bk_ble_gap_periodic_adv_sync_params_t"></a> <a id="_CPPv235bk_ble_gap_periodic_adv_create_syncPK37bk_ble_gap_periodic_adv_sync_params_t"></a> <a id="bk_ble_gap_periodic_adv_create_sync__bk_ble_gap_periodic_adv_sync_params_tCP"></a> <a id="group__dm__gap__defines__v1_1ga2b644cf38d09e265042ec8d7ba295138"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_periodic\_adv\_create\_sync(const [bk\_ble\_gap\_periodic\_adv\_sync\_params\_t](#_CPPv437bk_ble_gap_periodic_adv_sync_params_t "bk_ble_gap_periodic_adv_sync_params_t") \*params)
:   This function is used to synchronize with periodic advertising from an advertiser and begin receiving periodic advertising packets.

    参数
    :   **params** – **\[in\]** : sync parameters

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv435bk_ble_gap_periodic_adv_sync_cancelv"></a>

<a id="_CPPv335bk_ble_gap_periodic_adv_sync_cancelv"></a> <a id="_CPPv235bk_ble_gap_periodic_adv_sync_cancelv"></a> <a id="bk_ble_gap_periodic_adv_sync_cancel__void"></a> <a id="group__dm__gap__defines__v1_1ga71bf7fe1a2304eb7e426ea2e0bb9e2e4"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_periodic\_adv\_sync\_cancel(void)
:   This function is used to cancel the LE\_Periodic\_Advertising\_Create\_Sync command while it is pending.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv438bk_ble_gap_periodic_adv_sync_terminate8uint16_t"></a>

<a id="_CPPv338bk_ble_gap_periodic_adv_sync_terminate8uint16_t"></a> <a id="_CPPv238bk_ble_gap_periodic_adv_sync_terminate8uint16_t"></a> <a id="bk_ble_gap_periodic_adv_sync_terminate__uint16_t"></a> <a id="group__dm__gap__defines__v1_1gafaf181a959fc5439c61c041fd4cb4315"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_periodic\_adv\_sync\_terminate(uint16\_t sync\_handle)
:   This function is used to stop reception of the periodic advertising identified by the Sync Handle parameter.

    参数
    :   **sync\_handle** – **\[in\]** : identify the periodic advertiser

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv439bk_ble_gap_periodic_adv_add_dev_to_list18bk_ble_addr_type_t12bk_bd_addr_t7uint8_t"></a>

<a id="_CPPv339bk_ble_gap_periodic_adv_add_dev_to_list18bk_ble_addr_type_t12bk_bd_addr_t7uint8_t"></a> <a id="_CPPv239bk_ble_gap_periodic_adv_add_dev_to_list18bk_ble_addr_type_t12bk_bd_addr_t7uint8_t"></a> <a id="bk_ble_gap_periodic_adv_add_dev_to_list__bk_ble_addr_type_t.bk_bd_addr_t.uint8_t"></a> <a id="group__dm__gap__defines__v1_1gadd88022a032ff428a1eee587c16aac64"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_periodic\_adv\_add\_dev\_to\_list([bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr\_type, [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, uint8\_t sid)
:   This function is used to add a single device to the Periodic Advertiser list stored in the Controller.

    参数
    :   - **addr\_type** – **\[in\]** : address type
        - **addr** – **\[in\]** : Device Address
        - **sid** – **\[in\]** : Advertising SID subfield in the ADI field used to identify the Periodic Advertising

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv444bk_ble_gap_periodic_adv_remove_dev_from_list18bk_ble_addr_type_t12bk_bd_addr_t7uint8_t"></a>

<a id="_CPPv344bk_ble_gap_periodic_adv_remove_dev_from_list18bk_ble_addr_type_t12bk_bd_addr_t7uint8_t"></a> <a id="_CPPv244bk_ble_gap_periodic_adv_remove_dev_from_list18bk_ble_addr_type_t12bk_bd_addr_t7uint8_t"></a> <a id="bk_ble_gap_periodic_adv_remove_dev_from_list__bk_ble_addr_type_t.bk_bd_addr_t.uint8_t"></a> <a id="group__dm__gap__defines__v1_1gafdbfb73ae1659b43452ac772cffb28c0"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_periodic\_adv\_remove\_dev\_from\_list([bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr\_type, [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, uint8\_t sid)
:   This function is used to remove one device from the list of Periodic Advertisers stored in the Controller. Removals from the Periodic Advertisers List take effect immediately.

    参数
    :   - **addr\_type** – **\[in\]** : address type
        - **addr** – **\[in\]** : Device Address
        - **sid** – **\[in\]** : Advertising SID subfield in the ADI field used to identify the Periodic Advertising

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv433bk_ble_gap_periodic_adv_clear_devv"></a>

<a id="_CPPv333bk_ble_gap_periodic_adv_clear_devv"></a> <a id="_CPPv233bk_ble_gap_periodic_adv_clear_devv"></a> <a id="bk_ble_gap_periodic_adv_clear_dev__void"></a> <a id="group__dm__gap__defines__v1_1ga3e47334b3f4cf0b7ebf6a3fbfceafe75"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_periodic\_adv\_clear\_dev(void)
:   This function is used to remove all devices from the list of Periodic Advertisers in the Controller.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv426bk_ble_gap_set_scan_paramsPK24bk_ble_ext_scan_params_t"></a>

<a id="_CPPv326bk_ble_gap_set_scan_paramsPK24bk_ble_ext_scan_params_t"></a> <a id="_CPPv226bk_ble_gap_set_scan_paramsPK24bk_ble_ext_scan_params_t"></a> <a id="bk_ble_gap_set_scan_params__bk_ble_ext_scan_params_tCP"></a> <a id="group__dm__gap__defines__v1_1ga772c913c5fb2e8b4b11b1b829fd933c1"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_set\_scan\_params(const [bk\_ble\_ext\_scan\_params\_t](#_CPPv424bk_ble_ext_scan_params_t "bk_ble_ext_scan_params_t") \*params)
:   This function is used to set the extended scan parameters to be used on the advertising channels.

    参数
    :   **params** – **\[in\]** : scan parameters

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv421bk_ble_gap_start_scan8uint32_t8uint16_t"></a>

<a id="_CPPv321bk_ble_gap_start_scan8uint32_t8uint16_t"></a> <a id="_CPPv221bk_ble_gap_start_scan8uint32_t8uint16_t"></a> <a id="bk_ble_gap_start_scan__uint32_t.uint16_t"></a> <a id="group__dm__gap__defines__v1_1gaab6dc17e2a58c210260be5923d4b9cb3"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_start\_scan(uint32\_t duration, uint16\_t period)
:   This function is used to enable scanning.

    参数
    :   - **duration** – **\[in\]** : Scan duration
        - **period** – **\[in\]** : Time interval from when the Controller started its last Scan Duration until it begins the subsequent Scan Duration.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv420bk_ble_gap_stop_scanv"></a>

<a id="_CPPv320bk_ble_gap_stop_scanv"></a> <a id="_CPPv220bk_ble_gap_stop_scanv"></a> <a id="bk_ble_gap_stop_scan__void"></a> <a id="group__dm__gap__defines__v1_1ga284a4d5fb6f330cf0aec96db908c9bea"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_stop\_scan(void)
:   This function is used to disable scanning.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv436bk_ble_gap_prefer_connect_params_set12bk_bd_addr_t21bk_ble_gap_phy_mask_tPK24bk_ble_gap_conn_params_tPK24bk_ble_gap_conn_params_tPK24bk_ble_gap_conn_params_t"></a>

<a id="_CPPv336bk_ble_gap_prefer_connect_params_set12bk_bd_addr_t21bk_ble_gap_phy_mask_tPK24bk_ble_gap_conn_params_tPK24bk_ble_gap_conn_params_tPK24bk_ble_gap_conn_params_t"></a> <a id="_CPPv236bk_ble_gap_prefer_connect_params_set12bk_bd_addr_t21bk_ble_gap_phy_mask_tPK24bk_ble_gap_conn_params_tPK24bk_ble_gap_conn_params_tPK24bk_ble_gap_conn_params_t"></a> <a id="bk_ble_gap_prefer_connect_params_set__bk_bd_addr_t.bk_ble_gap_phy_mask_t.bk_ble_gap_conn_params_tCP.bk_ble_gap_conn_params_tCP.bk_ble_gap_conn_params_tCP"></a> <a id="group__dm__gap__defines__v1_1ga07b0c5057d0cf21b26365675b5e97085"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_prefer\_connect\_params\_set([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, [bk\_ble\_gap\_phy\_mask\_t](#_CPPv421bk_ble_gap_phy_mask_t "bk_ble_gap_phy_mask_t") phy\_mask, const [bk\_ble\_gap\_conn\_params\_t](#_CPPv424bk_ble_gap_conn_params_t "bk_ble_gap_conn_params_t") \*phy\_1m\_conn\_params, const [bk\_ble\_gap\_conn\_params\_t](#_CPPv424bk_ble_gap_conn_params_t "bk_ble_gap_conn_params_t") \*phy\_2m\_conn\_params, const [bk\_ble\_gap\_conn\_params\_t](#_CPPv424bk_ble_gap_conn_params_t "bk_ble_gap_conn_params_t") \*phy\_coded\_conn\_params)
:   This function is used to set aux connection parameters.

    参数
    :   - **addr** – **\[in\]** : device address
        - **phy\_mask** – **\[in\]** : indicates the PHY(s) on which the advertising packets should be received on the primary advertising channel and the PHYs for which connection parameters have been specified.
        - **phy\_1m\_conn\_params** – **\[in\]** : Scan connectable advertisements on the LE 1M PHY. Connection parameters for the LE 1M PHY are provided.
        - **phy\_2m\_conn\_params** – **\[in\]** : Connection parameters for the LE 2M PHY are provided.
        - **phy\_coded\_conn\_params** – **\[in\]** : Scan connectable advertisements on the LE Coded PHY. Connection parameters for the LE Coded PHY are provided.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv422bk_ble_gap_create_bond12bk_bd_addr_t"></a>

<a id="_CPPv322bk_ble_gap_create_bond12bk_bd_addr_t"></a> <a id="_CPPv222bk_ble_gap_create_bond12bk_bd_addr_t"></a> <a id="bk_ble_gap_create_bond__bk_bd_addr_t"></a> <a id="group__dm__gap__defines__v1_1ga3efb091a721dc8a07dd78f8a0077787b"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_create\_bond([bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   This function is used to create bond to peer, this function must used after connected.

    参数
    :   **bd\_addr** – **\[in\]** : peer address

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv434bk_ble_gap_bond_dev_list_operation32bk_gap_bond_dev_list_operation_tP17bk_ble_bond_dev_t"></a>

<a id="_CPPv334bk_ble_gap_bond_dev_list_operation32bk_gap_bond_dev_list_operation_tP17bk_ble_bond_dev_t"></a> <a id="_CPPv234bk_ble_gap_bond_dev_list_operation32bk_gap_bond_dev_list_operation_tP17bk_ble_bond_dev_t"></a> <a id="bk_ble_gap_bond_dev_list_operation__bk_gap_bond_dev_list_operation_t.bk_ble_bond_dev_tP"></a> <a id="group__dm__gap__defines__v1_1ga96488693b5c079ac1b29de2ed7efac4e"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_bond\_dev\_list\_operation([bk\_gap\_bond\_dev\_list\_operation\_t](#_CPPv432bk_gap_bond_dev_list_operation_t "bk_gap_bond_dev_list_operation_t") op, [bk\_ble\_bond\_dev\_t](#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") \*device)
:   This function is used to add, remove or clean bond dev info. BK\_BLE\_GAP\_BOND\_DEV\_LIST\_OPERATEION\_COMPLETE\_EVT evt will report when completed.

    **Attention**
    :   1\. Because app layer save bond info, when ble power on, app layer must add bond dev info one by one.

    **Attention**
    :   2\. When app layer remove bond info from it self storage, app layer should call BK\_GAP\_BOND\_DEV\_LIST\_OPERATION\_REMOVE or BK\_GAP\_BOND\_DEV\_LIST\_OPERATION\_CLEAN after it done.

    **Attention**
    :   3\. This func can’t be call when ble connection/adv/scan is exist.

    参数
    :   - **op** – **\[in\]** : operation
        - **device** – **\[in\]** : device info

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="_CPPv423bk_ble_gap_generate_rpaP7uint8_t"></a>

<a id="_CPPv323bk_ble_gap_generate_rpaP7uint8_t"></a> <a id="_CPPv223bk_ble_gap_generate_rpaP7uint8_t"></a> <a id="bk_ble_gap_generate_rpa__uint8_tP"></a> <a id="group__dm__gap__defines__v1_1gaeb19f41b1da90acab6d4c032b1804e9e"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gap\_generate\_rpa(uint8\_t \*irk)
:   This function is used to generate rpa. BK\_BLE\_GAP\_GENERATE\_RPA\_COMPLETE\_EVT evt will report when completed.

    参数
    :   **irk** – **\[in\]** : the key which used to generate rpa, when this argument is NULL, host will use current local irk to generate. If local irk is not exist(suchas ir not set), will return fail.

    返回
    :   \- BK\_OK : success

        - other : failed

<a id="bk-dm-gattc-h"></a>

## bk\_dm\_gattc.h

`bk_dm_gattc.h` 提供 BLE GATT Client 发现、读写、订阅和事件处理接口。

<a id="id4"></a>

### Header File

- [bk\_dm\_gattc.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_gattc.h)

<a id="id5"></a>

### Functions

<a id="_CPPv430bk_ble_gattc_register_callback13bk_gattc_cb_t"></a>

<a id="_CPPv330bk_ble_gattc_register_callback13bk_gattc_cb_t"></a> <a id="_CPPv230bk_ble_gattc_register_callback13bk_gattc_cb_t"></a> <a id="bk_ble_gattc_register_callback__bk_gattc_cb_t"></a> <a id="group__dm__gattc__functions__v1_1gad0451eaf78a2f9907f491fb537ecc449"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_register\_callback([bk\_gattc\_cb\_t](#_CPPv413bk_gattc_cb_t "bk_gattc_cb_t") callback)
:   This function is called to register application callbacks with GATTC module.

    参数
    :   **callback** – **\[in\]** : pointer to the application callback function.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv425bk_ble_gattc_app_register8uint16_t"></a>

<a id="_CPPv325bk_ble_gattc_app_register8uint16_t"></a> <a id="_CPPv225bk_ble_gattc_app_register8uint16_t"></a> <a id="bk_ble_gattc_app_register__uint16_t"></a> <a id="group__dm__gattc__functions__v1_1ga0c9c5b0c4f6c152ba110fe710fa1f6dc"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_app\_register(uint16\_t app\_id)
:   This function is called to register application callbacks with GATTC module.

    参数
    :   **app\_id** – **\[in\]** : Application Identify (UUID), for different application

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv427bk_ble_gattc_app_unregister12bk_gatt_if_t"></a>

<a id="_CPPv327bk_ble_gattc_app_unregister12bk_gatt_if_t"></a> <a id="_CPPv227bk_ble_gattc_app_unregister12bk_gatt_if_t"></a> <a id="bk_ble_gattc_app_unregister__bk_gatt_if_t"></a> <a id="group__dm__gattc__functions__v1_1gafacaf7cbbed99b302a78b94b24150158"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_app\_unregister([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if)
:   This function is called to unregister an application from GATTC module.

    参数
    :   **gattc\_if** – **\[in\]** Gatt client access interface.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv425bk_ble_gattc_send_mtu_req12bk_gatt_if_t8uint16_t"></a>

<a id="_CPPv325bk_ble_gattc_send_mtu_req12bk_gatt_if_t8uint16_t"></a> <a id="_CPPv225bk_ble_gattc_send_mtu_req12bk_gatt_if_t8uint16_t"></a> <a id="bk_ble_gattc_send_mtu_req__bk_gatt_if_t.uint16_t"></a> <a id="group__dm__gattc__functions__v1_1gaf98ed8ad2f3bad27b4ded3ed0a8fd87d"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_send\_mtu\_req([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id)
:   Configure the MTU size in the GATT channel. This can be done only once per connection. Before using, use [bk\_ble\_gatt\_set\_local\_mtu()](#group__dm__gatt__common__functions__v1_1ga07d73be77fe528eeaa17df45fb6d4efe) to configure the local MTU size.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** connection ID.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv422bk_ble_gattc_read_char12bk_gatt_if_t8uint16_t8uint16_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv322bk_ble_gattc_read_char12bk_gatt_if_t8uint16_t8uint16_t18bk_gatt_auth_req_t"></a> <a id="_CPPv222bk_ble_gattc_read_char12bk_gatt_if_t8uint16_t8uint16_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_read_char__bk_gatt_if_t.uint16_t.uint16_t.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1gaf1396e7be29be81910c0beb08ff8f872"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_read\_char([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, uint16\_t handle, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   This function is called to read a service’s characteristics of the given characteristic handle.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** : connection ID.
        - **handle** – **\[in\]** : characteritic handle to read.
        - **auth\_req** – **\[in\]** : authenticate request type

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv425bk_ble_gattc_read_by_type12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP12bk_bt_uuid_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv325bk_ble_gattc_read_by_type12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP12bk_bt_uuid_t18bk_gatt_auth_req_t"></a> <a id="_CPPv225bk_ble_gattc_read_by_type12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP12bk_bt_uuid_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_read_by_type__bk_gatt_if_t.uint16_t.uint16_t.uint16_t.bk_bt_uuid_tP.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1gab4cdeda3396c9abd201dadfadb17e26e"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_read\_by\_type([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, uint16\_t start\_handle, uint16\_t end\_handle, [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") \*uuid, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   This function is called to read a service’s characteristics of the given characteristic UUID.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** : connection ID.
        - **start\_handle** – **\[in\]** : the attribute start handle.
        - **end\_handle** – **\[in\]** : the attribute end handle
        - **uuid** – **\[in\]** : The UUID of attribute which will be read.
        - **auth\_req** – **\[in\]** : authenticate request type

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv426bk_ble_gattc_read_multiple12bk_gatt_if_t8uint16_tP16bk_gattc_multi_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv326bk_ble_gattc_read_multiple12bk_gatt_if_t8uint16_tP16bk_gattc_multi_t18bk_gatt_auth_req_t"></a> <a id="_CPPv226bk_ble_gattc_read_multiple12bk_gatt_if_t8uint16_tP16bk_gattc_multi_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_read_multiple__bk_gatt_if_t.uint16_t.bk_gattc_multi_tP.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1ga3ceb27a2eeea124316b1381debe61b2e"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_read\_multiple([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, [bk\_gattc\_multi\_t](#_CPPv416bk_gattc_multi_t "bk_gattc_multi_t") \*read\_multi, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   This function is called to read multiple characteristic or characteristic descriptors.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** : connection ID.
        - **read\_multi** – **\[in\]** : pointer to the read multiple parameter.
        - **auth\_req** – **\[in\]** : authenticate request type

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv428bk_ble_gattc_read_char_descr12bk_gatt_if_t8uint16_t8uint16_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv328bk_ble_gattc_read_char_descr12bk_gatt_if_t8uint16_t8uint16_t18bk_gatt_auth_req_t"></a> <a id="_CPPv228bk_ble_gattc_read_char_descr12bk_gatt_if_t8uint16_t8uint16_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_read_char_descr__bk_gatt_if_t.uint16_t.uint16_t.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1ga940034dd5c5fcf5e7f5c86c86effae93"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_read\_char\_descr([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, uint16\_t handle, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   This function is called to read a characteristics descriptor.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** : connection ID.
        - **handle** – **\[in\]** : descriptor handle to read.
        - **auth\_req** – **\[in\]** : authenticate request type

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv423bk_ble_gattc_write_char12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP7uint8_t20bk_gatt_write_type_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv323bk_ble_gattc_write_char12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP7uint8_t20bk_gatt_write_type_t18bk_gatt_auth_req_t"></a> <a id="_CPPv223bk_ble_gattc_write_char12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP7uint8_t20bk_gatt_write_type_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_write_char__bk_gatt_if_t.uint16_t.uint16_t.uint16_t.uint8_tP.bk_gatt_write_type_t.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1ga6c97add9d33ea2f1f6a8b39eb6a45dcd"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_write\_char([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, uint16\_t handle, uint16\_t value\_len, uint8\_t \*value, [bk\_gatt\_write\_type\_t](#_CPPv420bk_gatt_write_type_t "bk_gatt_write_type_t") write\_type, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   This function is called to write characteristic value.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** : connection ID.
        - **handle** – **\[in\]** : characteristic handle to write.
        - **value\_len** – **\[in\]** length of the value to be written.
        - **value** – **\[in\]** : the value to be written.
        - **write\_type** – **\[in\]** : the type of attribute write operation.
        - **auth\_req** – **\[in\]** : authentication request.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv429bk_ble_gattc_write_char_descr12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP7uint8_t20bk_gatt_write_type_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv329bk_ble_gattc_write_char_descr12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP7uint8_t20bk_gatt_write_type_t18bk_gatt_auth_req_t"></a> <a id="_CPPv229bk_ble_gattc_write_char_descr12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP7uint8_t20bk_gatt_write_type_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_write_char_descr__bk_gatt_if_t.uint16_t.uint16_t.uint16_t.uint8_tP.bk_gatt_write_type_t.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1gadc1c494c4aeec40479c47fe22e2db604"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_write\_char\_descr([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, uint16\_t handle, uint16\_t value\_len, uint8\_t \*value, [bk\_gatt\_write\_type\_t](#_CPPv420bk_gatt_write_type_t "bk_gatt_write_type_t") write\_type, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   This function is called to write characteristic descriptor value.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** : connection ID
        - **handle** – **\[in\]** : descriptor handle to write.
        - **value\_len** – **\[in\]** length of the value to be written.
        - **value** – **\[in\]** : the value to be written.
        - **write\_type** – **\[in\]** : the type of attribute write operation.
        - **auth\_req** – **\[in\]** : authentication request.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv426bk_ble_gattc_prepare_write12bk_gatt_if_t8uint16_t8uint16_t8uint16_t8uint16_tP7uint8_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv326bk_ble_gattc_prepare_write12bk_gatt_if_t8uint16_t8uint16_t8uint16_t8uint16_tP7uint8_t18bk_gatt_auth_req_t"></a> <a id="_CPPv226bk_ble_gattc_prepare_write12bk_gatt_if_t8uint16_t8uint16_t8uint16_t8uint16_tP7uint8_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_prepare_write__bk_gatt_if_t.uint16_t.uint16_t.uint16_t.uint16_t.uint8_tP.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1ga4097beb3ee428b9ce0fa607d199a20f9"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_prepare\_write([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, uint16\_t handle, uint16\_t offset, uint16\_t value\_len, uint8\_t \*value, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   This function is called to prepare write a characteristic value.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** : connection ID.
        - **handle** – **\[in\]** : characteristic handle to prepare write.
        - **offset** – **\[in\]** : offset of the write value.
        - **value\_len** – **\[in\]** length of the value to be written.
        - **value** – **\[in\]** : the value to be written.
        - **auth\_req** – **\[in\]** : authentication request.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv437bk_ble_gattc_prepare_write_char_descr12bk_gatt_if_t8uint16_t8uint16_t8uint16_t8uint16_tP7uint8_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv337bk_ble_gattc_prepare_write_char_descr12bk_gatt_if_t8uint16_t8uint16_t8uint16_t8uint16_tP7uint8_t18bk_gatt_auth_req_t"></a> <a id="_CPPv237bk_ble_gattc_prepare_write_char_descr12bk_gatt_if_t8uint16_t8uint16_t8uint16_t8uint16_tP7uint8_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_prepare_write_char_descr__bk_gatt_if_t.uint16_t.uint16_t.uint16_t.uint16_t.uint8_tP.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1gaa20e209fbba8550da557992c4185d952"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_prepare\_write\_char\_descr([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, uint16\_t handle, uint16\_t offset, uint16\_t value\_len, uint8\_t \*value, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   This function is called to prepare write a characteristic descriptor value.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** : connection ID.
        - **handle** – **\[in\]** : characteristic descriptor handle to prepare write.
        - **offset** – **\[in\]** : offset of the write value.
        - **value\_len** – **\[in\]** length of the value to be written.
        - **value** – **\[in\]** : the value to be written.
        - **auth\_req** – **\[in\]** : authentication request.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv426bk_ble_gattc_execute_write12bk_gatt_if_t8uint16_tb"></a>

<a id="_CPPv326bk_ble_gattc_execute_write12bk_gatt_if_t8uint16_tb"></a> <a id="_CPPv226bk_ble_gattc_execute_write12bk_gatt_if_t8uint16_tb"></a> <a id="bk_ble_gattc_execute_write__bk_gatt_if_t.uint16_t.b"></a> <a id="group__dm__gattc__functions__v1_1ga105527ea8e16e2cece436c1721a67c50"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_execute\_write([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, bool is\_execute)
:   This function is called to execute write a prepare write sequence.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **conn\_id** – **\[in\]** : connection ID.
        - **is\_execute** – **\[in\]** : execute or cancel.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv421bk_ble_gattc_discover12bk_gatt_if_t8uint16_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv321bk_ble_gattc_discover12bk_gatt_if_t8uint16_t18bk_gatt_auth_req_t"></a> <a id="_CPPv221bk_ble_gattc_discover12bk_gatt_if_t8uint16_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_discover__bk_gatt_if_t.uint16_t.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1ga8c1b1f4d8589e3676561fe98f33e90bb"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_discover([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t conn\_id, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   Triggle a discovery of the remote device.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **handle** – **\[in\]** : GATT characteristic handle.
        - **auth\_req** – **\[in\]** : authentication request.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv437bk_ble_gattc_discover_service_by_uuid12bk_gatt_if_t8uint16_tP12bk_bt_uuid_t18bk_gatt_auth_req_t"></a>

<a id="_CPPv337bk_ble_gattc_discover_service_by_uuid12bk_gatt_if_t8uint16_tP12bk_bt_uuid_t18bk_gatt_auth_req_t"></a> <a id="_CPPv237bk_ble_gattc_discover_service_by_uuid12bk_gatt_if_t8uint16_tP12bk_bt_uuid_t18bk_gatt_auth_req_t"></a> <a id="bk_ble_gattc_discover_service_by_uuid__bk_gatt_if_t.uint16_t.bk_bt_uuid_tP.bk_gatt_auth_req_t"></a> <a id="group__dm__gattc__functions__v1_1gacfa49bb16d32818304bf72c45770aa7e"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_discover\_service\_by\_uuid([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, uint16\_t handle, [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") \*uuid, [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req)
:   Triggle discovery service of the remote device.

    参数
    :   - **gattc\_if** – **\[in\]** Gatt client access interface.
        - **handle** – **\[in\]** : GATT characteristic handle.
        - **uuid** – **\[in\]** : uuid
        - **auth\_req** – **\[in\]** : authentication request.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="unions"></a>

### Unions

<a id="_CPPv423bk_ble_gattc_cb_param_t"></a>

<a id="_CPPv323bk_ble_gattc_cb_param_t"></a> <a id="_CPPv223bk_ble_gattc_cb_param_t"></a> <a id="unionbk__ble__gattc__cb__param__t"></a> union bk\_ble\_gattc\_cb\_param\_t
:   *#include \<bk\_dm\_gattc.h\>*

    Gatt client callback parameters union.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t3regE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t3regE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t3regE"></a> <a id="bk_ble_gattc_cb_param_t::reg__bk_ble_gattc_cb_param_t::gattc_reg_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1abb4c6add20e89e2d77c638578202a768"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_reg\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t19gattc_reg_evt_paramE "bk_ble_gattc_cb_param_t::gattc_reg_evt_param") reg
    :   Gatt client callback param of BK\_GATTC\_REG\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t7cfg_mtuE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t7cfg_mtuE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t7cfg_mtuE"></a> <a id="bk_ble_gattc_cb_param_t::cfg_mtu__bk_ble_gattc_cb_param_t::gattc_cfg_mtu_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1a1464a4b05ed23dc9b2413adbdaaa2191"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_cfg\_mtu\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_paramE "bk_ble_gattc_cb_param_t::gattc_cfg_mtu_evt_param") cfg\_mtu
    :   Gatt client callback param of BK\_GATTC\_CFG\_MTU\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t4readE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t4readE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t4readE"></a> <a id="bk_ble_gattc_cb_param_t::read__bk_ble_gattc_cb_param_t::gattc_read_char_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1a54dfd4263d7f9e574db0d160b80976a3"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_read\_char\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_paramE "bk_ble_gattc_cb_param_t::gattc_read_char_evt_param") read
    :   Gatt client callback param of BK\_GATTC\_READ\_CHAR\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t5writeE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t5writeE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t5writeE"></a> <a id="bk_ble_gattc_cb_param_t::write__bk_ble_gattc_cb_param_t::gattc_write_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1a8dc786ef5575328eb3bcd4221c374794"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_write\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t21gattc_write_evt_paramE "bk_ble_gattc_cb_param_t::gattc_write_evt_param") write
    :   Gatt client callback param of BK\_GATTC\_WRITE\_DESCR\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t9exec_cmplE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t9exec_cmplE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t9exec_cmplE"></a> <a id="bk_ble_gattc_cb_param_t::exec_cmpl__bk_ble_gattc_cb_param_t::gattc_exec_cmpl_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1a9063c0762838d6c4bc29c3ff22f1f6fc"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_exec\_cmpl\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_paramE "bk_ble_gattc_cb_param_t::gattc_exec_cmpl_evt_param") exec\_cmpl
    :   Gatt client callback param of BK\_GATTC\_EXEC\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t6notifyE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t6notifyE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t6notifyE"></a> <a id="bk_ble_gattc_cb_param_t::notify__bk_ble_gattc_cb_param_t::gattc_notify_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1a5ec52f0ab2c2faaf33f90af4c453faf7"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_notify\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t22gattc_notify_evt_paramE "bk_ble_gattc_cb_param_t::gattc_notify_evt_param") notify
    :   Gatt client callback param of BK\_GATTC\_NOTIFY\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t8srvc_chgE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t8srvc_chgE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t8srvc_chgE"></a> <a id="bk_ble_gattc_cb_param_t::srvc_chg__bk_ble_gattc_cb_param_t::gattc_srvc_chg_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1ace5e6ab6462b236c2eb150ac8fbf018d"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_srvc\_chg\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t24gattc_srvc_chg_evt_paramE "bk_ble_gattc_cb_param_t::gattc_srvc_chg_evt_param") srvc\_chg
    :   Gatt client callback param of BK\_GATTC\_SRVC\_CHG\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t7connectE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t7connectE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t7connectE"></a> <a id="bk_ble_gattc_cb_param_t::connect__bk_ble_gattc_cb_param_t::gattc_connect_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1ae86944180f501100b44b75babf13c608"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_connect\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t23gattc_connect_evt_paramE "bk_ble_gattc_cb_param_t::gattc_connect_evt_param") connect
    :   Gatt client callback param of BK\_GATTC\_CONNECT\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t10disconnectE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t10disconnectE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t10disconnectE"></a> <a id="bk_ble_gattc_cb_param_t::disconnect__bk_ble_gattc_cb_param_t::gattc_disconnect_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1a09a283b0821482c6c2a9a240b7737379"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_disconnect\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_paramE "bk_ble_gattc_cb_param_t::gattc_disconnect_evt_param") disconnect
    :   Gatt client callback param of BK\_GATTC\_DISCONNECT\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t13dis_srvc_cmplE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t13dis_srvc_cmplE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t13dis_srvc_cmplE"></a> <a id="bk_ble_gattc_cb_param_t::dis_srvc_cmpl__bk_ble_gattc_cb_param_t::gattc_dis_srvc_cmpl_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1ab9d3fb3c01ca481469604dd904c9aa49"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_dis\_srvc\_cmpl\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_srvc_cmpl_evt_param") dis\_srvc\_cmpl
    :   Gatt client callback param of BK\_GATTC\_DIS\_SRVC\_CMPL\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t15dis_res_serviceE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t15dis_res_serviceE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t15dis_res_serviceE"></a> <a id="bk_ble_gattc_cb_param_t::dis_res_service__bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1a90ae5f5eeb9b49850a5d7dfb2e3de43b"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_dis\_res\_service\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param") dis\_res\_service
    :   Gatt client callback param of BK\_GATTC\_DIS\_RES\_SERVICE\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t12dis_res_charE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t12dis_res_charE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t12dis_res_charE"></a> <a id="bk_ble_gattc_cb_param_t::dis_res_char__bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1ad29845db500bbf0d2961d8953c85481d"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_dis\_res\_char\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param") dis\_res\_char
    :   Gatt client callback param of BK\_GATTC\_DIS\_RES\_CHAR\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t17dis_res_char_descE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t17dis_res_char_descE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t17dis_res_char_descE"></a> <a id="bk_ble_gattc_cb_param_t::dis_res_char_desc__bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1a99a6127e114a777a241d503bf9ef15bb"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_dis\_res\_char\_desc\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param") dis\_res\_char\_desc
    :   Gatt client callback param of BK\_GATTC\_DIS\_RES\_CHAR\_DESC\_EVT

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t12read_by_typeE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t12read_by_typeE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t12read_by_typeE"></a> <a id="bk_ble_gattc_cb_param_t::read_by_type__bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param"></a> <a id="unionbk__ble__gattc__cb__param__t_1a1d0ac21d277638e8c40a4ed738fe4f31"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_read\_by\_type\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_paramE "bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param") read\_by\_type

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_cfg_mtu_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__cfg__mtu__evt__param"></a> struct gattc\_cfg\_mtu\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_CFG\_MTU\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_param6statusE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_cfg_mtu_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__cfg__mtu__evt__param_1ab276dd30e505f268fa88294673e8ae32"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_cfg_mtu_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__cfg__mtu__evt__param_1a79fb3cdcfdccce2a70b80e225e29fa41"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_param3mtuE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_param3mtuE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t23gattc_cfg_mtu_evt_param3mtuE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_cfg_mtu_evt_param::mtu__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__cfg__mtu__evt__param_1a8046679657f0a0c147dd4d12730b5040"></a> uint16\_t mtu
        :   MTU size

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t23gattc_connect_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t23gattc_connect_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t23gattc_connect_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_connect_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__connect__evt__param"></a> struct gattc\_connect\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_CONNECT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_connect_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__connect__evt__param_1a93a251cc9fc92548fa116d5628411996"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param9link_roleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param9link_roleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param9link_roleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_connect_evt_param::link_role__uint8_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__connect__evt__param_1a2970d0f4b9542623f23ff8850a871949"></a> uint8\_t link\_role
        :   Link role : master role \= 0 ; slave role \= 1

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param10remote_bdaE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param10remote_bdaE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param10remote_bdaE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_connect_evt_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__connect__evt__param_1a4af2786f250fd1df06e0db9f96890851"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param11conn_paramsE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param11conn_paramsE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t23gattc_connect_evt_param11conn_paramsE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_connect_evt_param::conn_params__bk_gatt_conn_params_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__connect__evt__param_1ad3ca0c8a5bd6250e367c23bbd78a0f6e"></a> [bk\_gatt\_conn\_params\_t](#_CPPv421bk_gatt_conn_params_t "bk_gatt_conn_params_t") conn\_params
        :   current connection parameters

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__desc__evt__param"></a> struct gattc\_dis\_res\_char\_desc\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_DIS\_RES\_CHAR\_DESC\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__desc__evt__param_1a047d5cb1960b9a6fd0109f8703919d36"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param11char_handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param11char_handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param11char_handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param::char_handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__desc__evt__param_1ab294dc83730986af3d475fa1ed236ebc"></a> uint16\_t char\_handle
        :   which char handle own this desc

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param11desc_handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param11desc_handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param11desc_handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param::desc_handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__desc__evt__param_1a280a2179d01c9534344ac3189637ddd0"></a> uint16\_t desc\_handle
        :   desc handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param4uuidE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param4uuidE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param4uuidE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param::uuid__bk_gatt_id_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__desc__evt__param_1a7fdacc60232fd1361c50306ac83829e0"></a> [bk\_gatt\_id\_t](#_CPPv412bk_gatt_id_t "bk_gatt_id_t") uuid

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param5arrayE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param5arrayE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param5arrayE"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__desc__evt__param_1adc99cdebcf368cc9c30a04af652f3d29"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_dis\_res\_char\_desc\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param")::\[anonymous\] \*array

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param5countE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param5countE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t33gattc_dis_res_char_desc_evt_param5countE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_desc_evt_param::count__uint32_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__desc__evt__param_1a87936de27a3f3b097f06ca6080d8b96a"></a> uint32\_t count

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__evt__param"></a> struct gattc\_dis\_res\_char\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_DIS\_RES\_CHAR\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__evt__param_1a7d19629883c54b4179e4d657f9f755e5"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param12start_handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param12start_handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param12start_handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param::start_handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__evt__param_1a9e22a412c3646903ee005fb8da3d4054"></a> uint16\_t start\_handle
        :   char start handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param10end_handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param10end_handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param10end_handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param::end_handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__evt__param_1a60c18630423615e08c697a74d42d10f6"></a> uint16\_t end\_handle
        :   char end handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param17char_value_handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param17char_value_handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param17char_value_handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param::char_value_handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__evt__param_1af1b600d4e7707ab8e29eb48292addaaf"></a> uint16\_t char\_value\_handle
        :   char declar value handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param4uuidE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param4uuidE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param4uuidE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param::uuid__bk_gatt_id_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__evt__param_1af1dbb65b6fda091f8424b8dbc727c530"></a> [bk\_gatt\_id\_t](#_CPPv412bk_gatt_id_t "bk_gatt_id_t") uuid
        :   uuid

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param4propE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param4propE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param4propE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param::prop__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__evt__param_1a1765f0b6d55f49f1aa3f0feafc8f420d"></a> uint16\_t prop

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param5arrayE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param5arrayE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param5arrayE"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__evt__param_1adc8a751ea9a05d51f9ead2cec0b74b9d"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_dis\_res\_char\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param")::\[anonymous\] \*array

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param5countE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param5countE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_dis_res_char_evt_param5countE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_char_evt_param::count__uint32_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__char__evt__param_1ae01339f7e47d797c6717efdf1e3fc61e"></a> uint32\_t count

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__service__evt__param"></a> struct gattc\_dis\_res\_service\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_DIS\_RES\_SERVICE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__service__evt__param_1a13221efb71c310691a984b22e70e4ad7"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param12start_handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param12start_handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param12start_handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param::start_handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__service__evt__param_1a8bdd3d3f216191983a3d09d42d8acd78"></a> uint16\_t start\_handle
        :   Service start handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param10end_handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param10end_handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param10end_handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param::end_handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__service__evt__param_1aa171871248666ff54086889592bdaaba"></a> uint16\_t end\_handle
        :   Service end handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param7srvc_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param7srvc_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param7srvc_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param::srvc_id__bk_gatt_id_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__service__evt__param_1a0ccae45e59cd377b1da53ee89f6cac65"></a> [bk\_gatt\_id\_t](#_CPPv412bk_gatt_id_t "bk_gatt_id_t") srvc\_id
        :   Service id, include service uuid and other information

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param10is_primaryE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param10is_primaryE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param10is_primaryE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param::is_primary__b"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__service__evt__param_1a8f816d6db86e5e2f858edcc29f0c19c0"></a> bool is\_primary
        :   True if this is the primary service

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param5arrayE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param5arrayE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param5arrayE"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__service__evt__param_1a731333ffde54f8ae2c641a575581df46"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_dis\_res\_service\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_paramE "bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param")::\[anonymous\] \*array

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param5countE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param5countE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t31gattc_dis_res_service_evt_param5countE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_res_service_evt_param::count__uint32_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__res__service__evt__param_1a23afd78f1c4177e5a54897ea567d89d3"></a> uint32\_t count

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_srvc_cmpl_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__srvc__cmpl__evt__param"></a> struct gattc\_dis\_srvc\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_DIS\_SRVC\_CMPL\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_param6statusE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_srvc_cmpl_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__srvc__cmpl__evt__param_1a5231b0d0a0ff4aed241772ba23adc17d"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t29gattc_dis_srvc_cmpl_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_dis_srvc_cmpl_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__dis__srvc__cmpl__evt__param_1ac2f0174712200cc469d0c04a6a03bfb8"></a> uint16\_t conn\_id
        :   Connection id

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_disconnect_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__disconnect__evt__param"></a> struct gattc\_disconnect\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_DISCONNECT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_param6reasonE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_param6reasonE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_param6reasonE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_disconnect_evt_param::reason__bk_gatt_conn_reason_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__disconnect__evt__param_1a5229297986b6ae94f40d9ce1c4c288b3"></a> [bk\_gatt\_conn\_reason\_t](#_CPPv421bk_gatt_conn_reason_t "bk_gatt_conn_reason_t") reason
        :   The reason of gatt connection close

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_disconnect_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__disconnect__evt__param_1a4a62609936fb15b98597696eccd95cc0"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_param10remote_bdaE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_param10remote_bdaE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t26gattc_disconnect_evt_param10remote_bdaE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_disconnect_evt_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__disconnect__evt__param_1a85ba7e313d3caa212bf10b2c9beeddd0"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_exec_cmpl_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__exec__cmpl__evt__param"></a> struct gattc\_exec\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_EXEC\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_param6statusE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_exec_cmpl_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__exec__cmpl__evt__param_1a535696640388ca98d3273cf073f4043c"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t25gattc_exec_cmpl_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_exec_cmpl_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__exec__cmpl__evt__param_1a325682e16487a803fb2ca5f8ce9ab458"></a> uint16\_t conn\_id
        :   Connection id

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t22gattc_notify_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t22gattc_notify_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t22gattc_notify_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_notify_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__notify__evt__param"></a> struct gattc\_notify\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_NOTIFY\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_notify_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__notify__evt__param_1af78b3805239f32bd3b6493a1fc57f663"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param10remote_bdaE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param10remote_bdaE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param10remote_bdaE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_notify_evt_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__notify__evt__param_1a8d7cafa829aaa23577ce59b4e1e0e57d"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param6handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param6handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param6handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_notify_evt_param::handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__notify__evt__param_1a72f561b0a46fa1b937d31d38848e8722"></a> uint16\_t handle
        :   The Characteristic or descriptor handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param9value_lenE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param9value_lenE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param9value_lenE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_notify_evt_param::value_len__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__notify__evt__param_1a6c9786dfa5282c7826d782f92020046b"></a> uint16\_t value\_len
        :   Notify attribute value

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param5valueE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param5valueE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param5valueE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_notify_evt_param::value__uint8_tP"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__notify__evt__param_1a90db8c4e52c8edfbc7a27e5d0f6833b5"></a> uint8\_t \*value
        :   Notify attribute value

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param9is_notifyE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param9is_notifyE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t22gattc_notify_evt_param9is_notifyE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_notify_evt_param::is_notify__b"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__notify__evt__param_1ad1180f6eb0e577dda994960dc312a526"></a> bool is\_notify
        :   True means notify, false means indicate

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__by__type__evt__param"></a> struct gattc\_read\_by\_type\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_READ\_BY\_TYPE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param6statusE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__by__type__evt__param_1a5c9340850a47879a1d74a2ff5381e74b"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__by__type__evt__param_1af29ae274678260b7af92d6b1c8422a64"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param10elem_countE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param10elem_countE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param10elem_countE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param::elem_count__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__by__type__evt__param_1a9dcfae15246617a72453d003437296cc"></a> uint16\_t elem\_count

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param6handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param6handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param6handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param::handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__by__type__evt__param_1a2afd9ab41d731bf65b7dc97448ea0e8b"></a> uint16\_t handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param5valueE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param5valueE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param5valueE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param::value__uint8_tP"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__by__type__evt__param_1a1823db2202b6f5b1633af43fad4c556d"></a> uint8\_t \*value
        :   attr handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param3lenE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param3lenE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param3lenE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param::len__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__by__type__evt__param_1af3ba3090b03df9361d8483e323fa56d2"></a> uint16\_t len
        :   attr value

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param4elemE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param4elemE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_param4elemE"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__by__type__evt__param_1aea2171acdd0ec397190d306c747d4b96"></a> struct [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t")::[gattc\_read\_by\_type\_evt\_param](#_CPPv4N23bk_ble_gattc_cb_param_t28gattc_read_by_type_evt_paramE "bk_ble_gattc_cb_param_t::gattc_read_by_type_evt_param")::\[anonymous\] \*elem
        :   elem\_count

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_char_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__char__evt__param"></a> struct gattc\_read\_char\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_READ\_CHAR\_EVT, BK\_GATTC\_READ\_DESCR\_EVT, BK\_GATTC\_READ\_MULTIPLE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param6statusE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_char_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__char__evt__param_1a56d3ddc7cb2b1d3922258e02b7c7d1c6"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_char_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__char__evt__param_1a23f1f307736d5a78d388bb310a378ed1"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param6handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param6handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param6handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_char_evt_param::handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__char__evt__param_1a545dc946d17acf2c7a58e9b9e8f8d58f"></a> uint16\_t handle
        :   Characteristic handle, Not used when BK\_GATTC\_READ\_MULTIPLE\_EVT

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param5valueE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param5valueE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param5valueE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_char_evt_param::value__uint8_tP"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__char__evt__param_1acc2a9f384f329b202ea00ad7e837f454"></a> uint8\_t \*value
        :   Characteristic value

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param9value_lenE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param9value_lenE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t25gattc_read_char_evt_param9value_lenE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_read_char_evt_param::value_len__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__read__char__evt__param_1a18f1d07b19b90f90932616046d08d086"></a> uint16\_t value\_len
        :   Characteristic value length

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t19gattc_reg_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t19gattc_reg_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t19gattc_reg_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_reg_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__reg__evt__param"></a> struct gattc\_reg\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_REG\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t19gattc_reg_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t19gattc_reg_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t19gattc_reg_evt_param6statusE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_reg_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__reg__evt__param_1a899fc6647bb14f8b71b5b9831221d20e"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t19gattc_reg_evt_param6app_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t19gattc_reg_evt_param6app_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t19gattc_reg_evt_param6app_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_reg_evt_param::app_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__reg__evt__param_1af07d4cd56871f9c2bf6f9c37b5287c1e"></a> uint16\_t app\_id
        :   Application id which input in register API

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t19gattc_reg_evt_param7gatt_ifE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t19gattc_reg_evt_param7gatt_ifE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t19gattc_reg_evt_param7gatt_ifE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_reg_evt_param::gatt_if__bk_gatt_if_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__reg__evt__param_1a8f05b914135805920408b986c4c9805e"></a> [bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatt\_if

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t24gattc_srvc_chg_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t24gattc_srvc_chg_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t24gattc_srvc_chg_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_srvc_chg_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__srvc__chg__evt__param"></a> struct gattc\_srvc\_chg\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_SRVC\_CHG\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t24gattc_srvc_chg_evt_param10remote_bdaE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t24gattc_srvc_chg_evt_param10remote_bdaE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t24gattc_srvc_chg_evt_param10remote_bdaE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_srvc_chg_evt_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__srvc__chg__evt__param_1ac0defbd585c9bdb9337cb2f3e6d5b024"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

    <a id="_CPPv4N23bk_ble_gattc_cb_param_t21gattc_write_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gattc_cb_param_t21gattc_write_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t21gattc_write_evt_paramE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_write_evt_param"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__write__evt__param"></a> struct gattc\_write\_evt\_param
    :   *#include \<bk\_dm\_gattc.h\>*

        BK\_GATTC\_WRITE\_CHAR\_EVT, BK\_GATTC\_PREP\_WRITE\_EVT, BK\_GATTC\_WRITE\_DESCR\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t21gattc_write_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t21gattc_write_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t21gattc_write_evt_param6statusE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_write_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__write__evt__param_1af6fd2c761ce5c1e7783395b4bacc7496"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t21gattc_write_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t21gattc_write_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t21gattc_write_evt_param7conn_idE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_write_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__write__evt__param_1af9f406ea1f14d78ccd9989b545d40cf2"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t21gattc_write_evt_param6handleE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t21gattc_write_evt_param6handleE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t21gattc_write_evt_param6handleE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_write_evt_param::handle__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__write__evt__param_1ad8a31ed7f56cf7bba44ba2da323bbe35"></a> uint16\_t handle
        :   The Characteristic or descriptor handle

        <a id="_CPPv4N23bk_ble_gattc_cb_param_t21gattc_write_evt_param6offsetE"></a>

        <a id="_CPPv3N23bk_ble_gattc_cb_param_t21gattc_write_evt_param6offsetE"></a> <a id="_CPPv2N23bk_ble_gattc_cb_param_t21gattc_write_evt_param6offsetE"></a> <a id="bk_ble_gattc_cb_param_t::gattc_write_evt_param::offset__uint16_t"></a> <a id="structbk__ble__gattc__cb__param__t_1_1gattc__write__evt__param_1a8f56abeb699ec06543e2fbf4121536df"></a> uint16\_t offset
        :   The prepare write offset, this value is valid only when prepare write

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv413bk_gattc_cb_t"></a>

<a id="_CPPv313bk_gattc_cb_t"></a> <a id="_CPPv213bk_gattc_cb_t"></a> <a id="bk_gattc_cb_t"></a> <a id="group__dm__gattc__types__v1_1ga7d77b3ced6bea1c7e047ba4366623d02"></a> typedef int32\_t (\*bk\_gattc\_cb\_t)([bk\_gattc\_cb\_event\_t](#_CPPv419bk_gattc_cb_event_t "bk_gattc_cb_event_t") event, [bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gattc\_if, [bk\_ble\_gattc\_cb\_param\_t](#_CPPv423bk_ble_gattc_cb_param_t "bk_ble_gattc_cb_param_t") \*param)
:   GATT Client callback function type.

    Param event
    :   : Event type

    Param gattc\_if
    :   : GATT client access interface, normally different gattc\_if correspond to different profile

    Param param
    :   : Point to callback parameter, currently is union type

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv419bk_gattc_cb_event_t"></a>

<a id="_CPPv319bk_gattc_cb_event_t"></a> <a id="_CPPv219bk_gattc_cb_event_t"></a> <a id="group__dm__gattc__types__v1_1ga0dd66887e05215e2803da7749e54bebb"></a> enum bk\_gattc\_cb\_event\_t
:   GATT Client callback function events.

    *Values:*

    <a id="_CPPv4N19bk_gattc_cb_event_t16BK_GATTC_REG_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t16BK_GATTC_REG_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t16BK_GATTC_REG_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebbadcb14673a8ac9237d84a7e19bad197fa"></a> enumerator BK\_GATTC\_REG\_EVT
    :   When GATT client is registered, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t18BK_GATTC_UNREG_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t18BK_GATTC_UNREG_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t18BK_GATTC_UNREG_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba81275a4b8451a07d15bbc06148e8c0ce"></a> enumerator BK\_GATTC\_UNREG\_EVT
    :   When GATT client is unregistered, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t22BK_GATTC_READ_CHAR_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t22BK_GATTC_READ_CHAR_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t22BK_GATTC_READ_CHAR_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebbac0811ec80b37e4cc6671f335143fcad5"></a> enumerator BK\_GATTC\_READ\_CHAR\_EVT
    :   When GATT characteristic is read, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t23BK_GATTC_WRITE_CHAR_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t23BK_GATTC_WRITE_CHAR_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t23BK_GATTC_WRITE_CHAR_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebbad95459406516a5d0310cf71439a8d9b0"></a> enumerator BK\_GATTC\_WRITE\_CHAR\_EVT
    :   When GATT characteristic write operation completes, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t23BK_GATTC_READ_DESCR_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t23BK_GATTC_READ_DESCR_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t23BK_GATTC_READ_DESCR_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebbad14acd6c59f20ec5419b9b08bf903463"></a> enumerator BK\_GATTC\_READ\_DESCR\_EVT
    :   When GATT characteristic descriptor read completes, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t24BK_GATTC_WRITE_DESCR_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t24BK_GATTC_WRITE_DESCR_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t24BK_GATTC_WRITE_DESCR_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebbabf2f7a34823d3a9e2e937a7470f40238"></a> enumerator BK\_GATTC\_WRITE\_DESCR\_EVT
    :   When GATT characteristic descriptor write completes, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t19BK_GATTC_NOTIFY_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t19BK_GATTC_NOTIFY_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t19BK_GATTC_NOTIFY_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba1c66acbd490ecc95f3eed837734107a8"></a> enumerator BK\_GATTC\_NOTIFY\_EVT
    :   When GATT notification or indication arrives, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t23BK_GATTC_PREP_WRITE_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t23BK_GATTC_PREP_WRITE_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t23BK_GATTC_PREP_WRITE_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba7266155ed7d5fabec0acb3a24fa1a80b"></a> enumerator BK\_GATTC\_PREP\_WRITE\_EVT
    :   When GATT prepare-write operation completes, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t17BK_GATTC_EXEC_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t17BK_GATTC_EXEC_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t17BK_GATTC_EXEC_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba8964ca5f1fbc59b149d40b73b88ac3a7"></a> enumerator BK\_GATTC\_EXEC\_EVT
    :   When write execution completes, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t20BK_GATTC_CFG_MTU_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t20BK_GATTC_CFG_MTU_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t20BK_GATTC_CFG_MTU_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba436e9bda8fc404c920ed1a64d0d1f222"></a> enumerator BK\_GATTC\_CFG\_MTU\_EVT
    :   When configuration of MTU completes, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t20BK_GATTC_CONNECT_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t20BK_GATTC_CONNECT_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t20BK_GATTC_CONNECT_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba53ac1bd73e3f1c60e0ecadbb9018eb30"></a> enumerator BK\_GATTC\_CONNECT\_EVT
    :   When the ble physical connection is set up, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t23BK_GATTC_DISCONNECT_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t23BK_GATTC_DISCONNECT_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t23BK_GATTC_DISCONNECT_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba59adbd3e592e8f1b46c2572029c499bc"></a> enumerator BK\_GATTC\_DISCONNECT\_EVT
    :   When the ble physical connection disconnected, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t26BK_GATTC_READ_MULTIPLE_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t26BK_GATTC_READ_MULTIPLE_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t26BK_GATTC_READ_MULTIPLE_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba105bd1831963557194912870efbcaf86"></a> enumerator BK\_GATTC\_READ\_MULTIPLE\_EVT
    :   When the ble characteristic or descriptor multiple complete, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t26BK_GATTC_DIS_SRVC_CMPL_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t26BK_GATTC_DIS_SRVC_CMPL_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t26BK_GATTC_DIS_SRVC_CMPL_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba7f96a4faff1a0ebe1de8be3b82a9a5d2"></a> enumerator BK\_GATTC\_DIS\_SRVC\_CMPL\_EVT
    :   When the ble discover service complete, the event comes

    <a id="_CPPv4N19bk_gattc_cb_event_t28BK_GATTC_DIS_RES_SERVICE_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t28BK_GATTC_DIS_RES_SERVICE_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t28BK_GATTC_DIS_RES_SERVICE_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba43cd12bb0a545d474e022fb1b086e098"></a> enumerator BK\_GATTC\_DIS\_RES\_SERVICE\_EVT

    <a id="_CPPv4N19bk_gattc_cb_event_t25BK_GATTC_DIS_RES_CHAR_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t25BK_GATTC_DIS_RES_CHAR_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t25BK_GATTC_DIS_RES_CHAR_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba8e37178c9a07f138610a433f640c740d"></a> enumerator BK\_GATTC\_DIS\_RES\_CHAR\_EVT

    <a id="_CPPv4N19bk_gattc_cb_event_t30BK_GATTC_DIS_RES_CHAR_DESC_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t30BK_GATTC_DIS_RES_CHAR_DESC_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t30BK_GATTC_DIS_RES_CHAR_DESC_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba2d39d7bfd0434eeac35dcb1e06f8dfd0"></a> enumerator BK\_GATTC\_DIS\_RES\_CHAR\_DESC\_EVT

    <a id="_CPPv4N19bk_gattc_cb_event_t25BK_GATTC_READ_BY_TYPE_EVTE"></a>

    <a id="_CPPv3N19bk_gattc_cb_event_t25BK_GATTC_READ_BY_TYPE_EVTE"></a> <a id="_CPPv2N19bk_gattc_cb_event_t25BK_GATTC_READ_BY_TYPE_EVTE"></a> <a id="group__dm__gattc__types__v1_1gga0dd66887e05215e2803da7749e54bebba9e602fb2ff289969d6af26bc08f2d76e"></a> enumerator BK\_GATTC\_READ\_BY\_TYPE\_EVT

<a id="bk-dm-gatts-h"></a>

## bk\_dm\_gatts.h

`bk_dm_gatts.h` 提供 BLE GATT Server 服务表创建、属性读写和通知接口。

<a id="id6"></a>

### Header File

- [bk\_dm\_gatts.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_gatts.h)

<a id="id7"></a>

### Functions

<a id="_CPPv430bk_ble_gatts_register_callback13bk_gatts_cb_t"></a>

<a id="_CPPv330bk_ble_gatts_register_callback13bk_gatts_cb_t"></a> <a id="_CPPv230bk_ble_gatts_register_callback13bk_gatts_cb_t"></a> <a id="bk_ble_gatts_register_callback__bk_gatts_cb_t"></a> <a id="group__dm__gatts__functions__v1_1ga5e7a7e838568678bec173d95eb77d5c7"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_register\_callback([bk\_gatts\_cb\_t](#_CPPv413bk_gatts_cb_t "bk_gatts_cb_t") callback)
:   This function is called to register application callbacks with BTA GATTS module.

    参数
    :   **callback** – : see bk\_gatts\_cb\_t

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv425bk_ble_gatts_app_register8uint16_t"></a>

<a id="_CPPv325bk_ble_gatts_app_register8uint16_t"></a> <a id="_CPPv225bk_ble_gatts_app_register8uint16_t"></a> <a id="bk_ble_gatts_app_register__uint16_t"></a> <a id="group__dm__gatts__functions__v1_1ga0d30436ba135a075304f6580d827aa0d"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_app\_register(uint16\_t app\_id)
:   This function is called to register application identifier.

    参数
    :   **app\_id** – : app id, not used now

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv427bk_ble_gatts_app_unregister12bk_gatt_if_t"></a>

<a id="_CPPv327bk_ble_gatts_app_unregister12bk_gatt_if_t"></a> <a id="_CPPv227bk_ble_gatts_app_unregister12bk_gatt_if_t"></a> <a id="bk_ble_gatts_app_unregister__bk_gatt_if_t"></a> <a id="group__dm__gatts__functions__v1_1gaa7613cd71440c9c032cac357ac202248"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_app\_unregister([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts\_if)
:   unregister with GATT Server.

    参数
    :   **gatts\_if** – **\[in\]** GATT server access interface

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv427bk_ble_gatts_create_service12bk_gatt_if_tP17bk_gatt_srvc_id_t8uint16_t"></a>

<a id="_CPPv327bk_ble_gatts_create_service12bk_gatt_if_tP17bk_gatt_srvc_id_t8uint16_t"></a> <a id="_CPPv227bk_ble_gatts_create_service12bk_gatt_if_tP17bk_gatt_srvc_id_t8uint16_t"></a> <a id="bk_ble_gatts_create_service__bk_gatt_if_t.bk_gatt_srvc_id_tP.uint16_t"></a> <a id="group__dm__gatts__functions__v1_1ga1f21efd48f364d3632d64b8768f4696e"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_create\_service([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts\_if, [bk\_gatt\_srvc\_id\_t](#_CPPv417bk_gatt_srvc_id_t "bk_gatt_srvc_id_t") \*service\_id, uint16\_t num\_handle)
:   Create a service. When service creation is done, a callback event BK\_GATTS\_CREATE\_EVT is called to report status and service ID to the profile. The service ID obtained in the callback function needs to be used when adding included service and characteristics/descriptors into the service.

    参数
    :   - **gatts\_if** – **\[in\]** GATT server access interface
        - **service\_id** – **\[in\]** service ID.
        - **num\_handle** – **\[in\]** number of handle requested for this service.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv428bk_ble_gatts_create_attr_tabPK18bk_gatts_attr_db_t12bk_gatt_if_t8uint16_t8uint32_t"></a>

<a id="_CPPv328bk_ble_gatts_create_attr_tabPK18bk_gatts_attr_db_t12bk_gatt_if_t8uint16_t8uint32_t"></a> <a id="_CPPv228bk_ble_gatts_create_attr_tabPK18bk_gatts_attr_db_t12bk_gatt_if_t8uint16_t8uint32_t"></a> <a id="bk_ble_gatts_create_attr_tab__bk_gatts_attr_db_tCP.bk_gatt_if_t.uint16_t.uint32_t"></a> <a id="group__dm__gatts__functions__v1_1ga7da2e234ba849084b69ce36cfd62f391"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_create\_attr\_tab(const [bk\_gatts\_attr\_db\_t](#_CPPv418bk_gatts_attr_db_t "bk_gatts_attr_db_t") \*gatts\_attr\_db, [bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts\_if, uint16\_t count, uint32\_t max\_attr\_count)
:   Create a service attribute tab. Only one service once.

    参数
    :   - **gatts\_attr\_db** – **\[in\]** the pointer to the service attr tab. At least has one service declar
        - **gatts\_if** – **\[in\]** GATT server access interface
        - **count** – **\[in\]** the number of gatts\_attr\_db.
        - **max\_attr\_count** – **\[in\]** max attr num of this service.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv421bk_ble_gatts_add_char8uint16_tP12bk_bt_uuid_t14bk_gatt_perm_t19bk_gatt_char_prop_tP15bk_attr_value_tP17bk_attr_control_t"></a>

<a id="_CPPv321bk_ble_gatts_add_char8uint16_tP12bk_bt_uuid_t14bk_gatt_perm_t19bk_gatt_char_prop_tP15bk_attr_value_tP17bk_attr_control_t"></a> <a id="_CPPv221bk_ble_gatts_add_char8uint16_tP12bk_bt_uuid_t14bk_gatt_perm_t19bk_gatt_char_prop_tP15bk_attr_value_tP17bk_attr_control_t"></a> <a id="bk_ble_gatts_add_char__uint16_t.bk_bt_uuid_tP.bk_gatt_perm_t.bk_gatt_char_prop_t.bk_attr_value_tP.bk_attr_control_tP"></a> <a id="group__dm__gatts__functions__v1_1ga61c7d9b735986ebed04c6cd2e8f8f82c"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_add\_char(uint16\_t service\_handle, [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") \*char\_uuid, [bk\_gatt\_perm\_t](#_CPPv414bk_gatt_perm_t "bk_gatt_perm_t") perm, [bk\_gatt\_char\_prop\_t](#_CPPv419bk_gatt_char_prop_t "bk_gatt_char_prop_t") property, [bk\_attr\_value\_t](#_CPPv415bk_attr_value_t "bk_attr_value_t") \*char\_val, [bk\_attr\_control\_t](#_CPPv417bk_attr_control_t "bk_attr_control_t") \*control)
:   This function is called to add a characteristic into a service.

    参数
    :   - **service\_handle** – **\[in\]** service handle to which this included service is to be added.
        - **char\_uuid** – **\[in\]** : Characteristic UUID.
        - **perm** – **\[in\]** : Characteristic value declaration attribute permission.
        - **property** – **\[in\]** : Characteristic Properties
        - **char\_val** – **\[in\]** : Characteristic value
        - **control** – **\[in\]** : attribute response control byte

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv427bk_ble_gatts_add_char_descr8uint16_t8uint16_tP12bk_bt_uuid_t14bk_gatt_perm_tP15bk_attr_value_tP17bk_attr_control_t"></a>

<a id="_CPPv327bk_ble_gatts_add_char_descr8uint16_t8uint16_tP12bk_bt_uuid_t14bk_gatt_perm_tP15bk_attr_value_tP17bk_attr_control_t"></a> <a id="_CPPv227bk_ble_gatts_add_char_descr8uint16_t8uint16_tP12bk_bt_uuid_t14bk_gatt_perm_tP15bk_attr_value_tP17bk_attr_control_t"></a> <a id="bk_ble_gatts_add_char_descr__uint16_t.uint16_t.bk_bt_uuid_tP.bk_gatt_perm_t.bk_attr_value_tP.bk_attr_control_tP"></a> <a id="group__dm__gatts__functions__v1_1ga482bc5145e5ceda85ac1bf6de268f322"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_add\_char\_descr(uint16\_t service\_handle, uint16\_t char\_handle, [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") \*descr\_uuid, [bk\_gatt\_perm\_t](#_CPPv414bk_gatt_perm_t "bk_gatt_perm_t") perm, [bk\_attr\_value\_t](#_CPPv415bk_attr_value_t "bk_attr_value_t") \*char\_descr\_val, [bk\_attr\_control\_t](#_CPPv417bk_attr_control_t "bk_attr_control_t") \*control)
:   This function is called to add characteristic descriptor. When it’s done, a callback event BK\_GATTS\_ADD\_DESCR\_EVT is called to report the status and an ID number for this descriptor.

    参数
    :   - **service\_handle** – **\[in\]** service handle to which this characteristic descriptor is to be added.
        - **char\_handle** – **\[in\]** which characteristic descriptor is to be added.
        - **char\_handle** – **\[in\]** which characteristic descriptor is to be added.
        - **perm** – **\[in\]** descriptor access permission.
        - **descr\_uuid** – **\[in\]** descriptor UUID.
        - **char\_descr\_val** – **\[in\]** : Characteristic descriptor value
        - **control** – **\[in\]** : attribute response control byte

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv426bk_ble_gatts_start_service8uint16_t"></a>

<a id="_CPPv326bk_ble_gatts_start_service8uint16_t"></a> <a id="_CPPv226bk_ble_gatts_start_service8uint16_t"></a> <a id="bk_ble_gatts_start_service__uint16_t"></a> <a id="group__dm__gatts__functions__v1_1ga30a94fe03aff7fb95c201746978648f8"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_start\_service(uint16\_t service\_attr\_handle)
:   This function is called to start a service.

    参数
    :   **service\_attr\_handle** – **\[in\]** the service handle to be started.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv425bk_ble_gatts_stop_service8uint16_t"></a>

<a id="_CPPv325bk_ble_gatts_stop_service8uint16_t"></a> <a id="_CPPv225bk_ble_gatts_stop_service8uint16_t"></a> <a id="bk_ble_gatts_stop_service__uint16_t"></a> <a id="group__dm__gatts__functions__v1_1gadb7008391f8b9d702a0d701ce583bbfd"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_stop\_service(uint16\_t service\_attr\_handle)
:   This function is called to stop a service.

    参数
    :   **service\_attr\_handle** – **\[in\]** the service handle to be stop.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv426bk_ble_gatts_send_indicate12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP7uint8_tb"></a>

<a id="_CPPv326bk_ble_gatts_send_indicate12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP7uint8_tb"></a> <a id="_CPPv226bk_ble_gatts_send_indicate12bk_gatt_if_t8uint16_t8uint16_t8uint16_tP7uint8_tb"></a> <a id="bk_ble_gatts_send_indicate__bk_gatt_if_t.uint16_t.uint16_t.uint16_t.uint8_tP.b"></a> <a id="group__dm__gatts__functions__v1_1ga709f9099bc0da302f9f558f97e1ca7b7"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_send\_indicate([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts\_if, uint16\_t conn\_id, uint16\_t attr\_handle, uint16\_t value\_len, uint8\_t \*value, bool need\_confirm)
:   Send indicate or notify to GATT client. Set param need\_confirm as false will send notification, otherwise indication.

    参数
    :   - **gatts\_if** – **\[in\]** GATT server access interface
        - **conn\_id** – **\[in\]** \- connection handle.
        - **attr\_handle** – **\[in\]** \- attribute handle to indicate.
        - **value\_len** – **\[in\]** \- indicate value length.
        - **value** – **\[in\]** value to indicate.
        - **need\_confirm** – **\[in\]** \- Whether a confirmation is required. false sends a GATT notification, true sends a GATT indication.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv426bk_ble_gatts_send_response12bk_gatt_if_t8uint16_t8uint32_t16bk_gatt_status_tP13bk_gatt_rsp_t"></a>

<a id="_CPPv326bk_ble_gatts_send_response12bk_gatt_if_t8uint16_t8uint32_t16bk_gatt_status_tP13bk_gatt_rsp_t"></a> <a id="_CPPv226bk_ble_gatts_send_response12bk_gatt_if_t8uint16_t8uint32_t16bk_gatt_status_tP13bk_gatt_rsp_t"></a> <a id="bk_ble_gatts_send_response__bk_gatt_if_t.uint16_t.uint32_t.bk_gatt_status_t.bk_gatt_rsp_tP"></a> <a id="group__dm__gatts__functions__v1_1ga2007436fe68ba2490a68e6e2016f6e07"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_send\_response([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts\_if, uint16\_t conn\_id, uint32\_t trans\_id, [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status, [bk\_gatt\_rsp\_t](#_CPPv413bk_gatt_rsp_t "bk_gatt_rsp_t") \*rsp)
:   This function is called to send a response to a request.

    参数
    :   - **gatts\_if** – **\[in\]** GATT server access interface
        - **conn\_id** – **\[in\]** \- connection handle.
        - **trans\_id** – **\[in\]** \- Transaction id
        - **status** – **\[in\]** \- response status
        - **rsp** – **\[in\]** \- response data.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv427bk_ble_gatts_set_attr_value8uint16_t8uint16_tPK7uint8_t"></a>

<a id="_CPPv327bk_ble_gatts_set_attr_value8uint16_t8uint16_tPK7uint8_t"></a> <a id="_CPPv227bk_ble_gatts_set_attr_value8uint16_t8uint16_tPK7uint8_t"></a> <a id="bk_ble_gatts_set_attr_value__uint16_t.uint16_t.uint8_tCP"></a> <a id="group__dm__gatts__functions__v1_1ga6ac3874d19db5442cfc5f4dd41be57df"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_set\_attr\_value(uint16\_t attr\_handle, uint16\_t length, const uint8\_t \*value)
:   This function is called to set the attribute value by the application.

    参数
    :   - **attr\_handle** – **\[in\]** the attribute handle which to be set
        - **length** – **\[in\]** the value length
        - **value** – **\[in\]** the pointer to the attribute value

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv427bk_ble_gatts_get_attr_value8uint16_tP8uint16_tPP7uint8_t"></a>

<a id="_CPPv327bk_ble_gatts_get_attr_value8uint16_tP8uint16_tPP7uint8_t"></a> <a id="_CPPv227bk_ble_gatts_get_attr_value8uint16_tP8uint16_tPP7uint8_t"></a> <a id="bk_ble_gatts_get_attr_value__uint16_t.uint16_tP.uint8_tPP"></a> <a id="group__dm__gatts__functions__v1_1ga804cdb0e19e5c933bc76fc6a4d5d902c"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_get\_attr\_value(uint16\_t attr\_handle, uint16\_t \*length, uint8\_t \*\*value)
:   Retrieve attribute value.

    参数
    :   - **attr\_handle** – **\[in\]** Attribute handle.
        - **length** – **\[out\]** pointer to the attribute value length
        - **value** – **\[out\]** Pointer to attribute value payload, the value cannot be modified by user

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv441bk_ble_gatts_send_service_change_indicate12bk_gatt_if_t8uint16_t7uint8_t"></a>

<a id="_CPPv341bk_ble_gatts_send_service_change_indicate12bk_gatt_if_t8uint16_t7uint8_t"></a> <a id="_CPPv241bk_ble_gatts_send_service_change_indicate12bk_gatt_if_t8uint16_t7uint8_t"></a> <a id="bk_ble_gatts_send_service_change_indicate__bk_gatt_if_t.uint16_t.uint8_t"></a> <a id="group__dm__gatts__functions__v1_1ga0d9dcac41bc4aebd8a5dbda940b12ea8"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_send\_service\_change\_indicate([bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts\_if, uint16\_t conn\_id, uint8\_t all\_connected)
:   Send service change indicate.

    参数
    :   - **gatts\_if** – **\[in\]** GATT server access interface
        - **conn\_id** – **\[in\]** \- connection handle.
        - **all\_connected** – **\[in\]** \- If all\_connected is true then it will send service change indicate to all the connected devices and conn\_id will be ignore.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="_CPPv436bk_ble_gatts_char_property_operation36bk_gatts_char_property_bit_mask_op_t8uint16_tP8uint16_t"></a>

<a id="_CPPv336bk_ble_gatts_char_property_operation36bk_gatts_char_property_bit_mask_op_t8uint16_tP8uint16_t"></a> <a id="_CPPv236bk_ble_gatts_char_property_operation36bk_gatts_char_property_bit_mask_op_t8uint16_tP8uint16_t"></a> <a id="bk_ble_gatts_char_property_operation__bk_gatts_char_property_bit_mask_op_t.uint16_t.uint16_tP"></a> <a id="group__dm__gatts__functions__v1_1ga854360c884a6061d5380fe3632265669"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatts\_char\_property\_operation([bk\_gatts\_char\_property\_bit\_mask\_op\_t](#_CPPv436bk_gatts_char_property_bit_mask_op_t "bk_gatts_char_property_bit_mask_op_t") op, uint16\_t attr\_handle, uint16\_t \*io)
:   Get or set characteristic property.

    参数
    :   - **op** – **\[in\]** GATT get or set.
        - **attr\_handle** – **\[in\]** char value attr handle.
        - **\[in\|out\]** – io: input when set and output when set

    返回
    :   - BK\_ERR\_BLE\_SUCCESS : success
        - other : failed

<a id="id8"></a>

### Unions

<a id="_CPPv423bk_ble_gatts_cb_param_t"></a>

<a id="_CPPv323bk_ble_gatts_cb_param_t"></a> <a id="_CPPv223bk_ble_gatts_cb_param_t"></a> <a id="unionbk__ble__gatts__cb__param__t"></a> union bk\_ble\_gatts\_cb\_param\_t
:   *#include \<bk\_dm\_gatts.h\>*

    Gatt server callback parameters union.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t3regE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t3regE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t3regE"></a> <a id="bk_ble_gatts_cb_param_t::reg__bk_ble_gatts_cb_param_t::gatts_reg_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a4af9336707dfb10caca5fbfc9f8080a6"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_reg\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t19gatts_reg_evt_paramE "bk_ble_gatts_cb_param_t::gatts_reg_evt_param") reg
    :   Gatt server callback param of BK\_GATTS\_REG\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t4readE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t4readE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t4readE"></a> <a id="bk_ble_gatts_cb_param_t::read__bk_ble_gatts_cb_param_t::gatts_read_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a42405673ff2a370fa55237c604818448"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_read\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_paramE "bk_ble_gatts_cb_param_t::gatts_read_evt_param") read
    :   Gatt server callback param of BK\_GATTS\_READ\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t5writeE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t5writeE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t5writeE"></a> <a id="bk_ble_gatts_cb_param_t::write__bk_ble_gatts_cb_param_t::gatts_write_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a51dae48fc6a79dfe8e754bd1046b0903"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_write\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_paramE "bk_ble_gatts_cb_param_t::gatts_write_evt_param") write
    :   Gatt server callback param of BK\_GATTS\_WRITE\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t10exec_writeE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t10exec_writeE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t10exec_writeE"></a> <a id="bk_ble_gatts_cb_param_t::exec_write__bk_ble_gatts_cb_param_t::gatts_exec_write_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a4085bd327b888df4dee9626e37a7b10d"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_exec\_write\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_paramE "bk_ble_gatts_cb_param_t::gatts_exec_write_evt_param") exec\_write
    :   Gatt server callback param of BK\_GATTS\_EXEC\_WRITE\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t3mtuE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t3mtuE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t3mtuE"></a> <a id="bk_ble_gatts_cb_param_t::mtu__bk_ble_gatts_cb_param_t::gatts_mtu_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a014695d2abe24cf747e845fb8025c4e0"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_mtu\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_paramE "bk_ble_gatts_cb_param_t::gatts_mtu_evt_param") mtu
    :   Gatt server callback param of BK\_GATTS\_MTU\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t4confE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t4confE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t4confE"></a> <a id="bk_ble_gatts_cb_param_t::conf__bk_ble_gatts_cb_param_t::gatts_conf_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a12c491508205946604a34cc3c7091966"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_conf\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t20gatts_conf_evt_paramE "bk_ble_gatts_cb_param_t::gatts_conf_evt_param") conf
    :   Gatt server callback param of BK\_GATTS\_CONF\_EVT (confirm)

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t6createE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t6createE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t6createE"></a> <a id="bk_ble_gatts_cb_param_t::create__bk_ble_gatts_cb_param_t::gatts_create_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1ac6908db0307bf54a671b30311784a1f9"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_create\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t22gatts_create_evt_paramE "bk_ble_gatts_cb_param_t::gatts_create_evt_param") create
    :   Gatt server callback param of BK\_GATTS\_CREATE\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t8add_charE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t8add_charE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t8add_charE"></a> <a id="bk_ble_gatts_cb_param_t::add_char__bk_ble_gatts_cb_param_t::gatts_add_char_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a5154eb90d41bc578c77d0a547abbeeac"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_add\_char\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_paramE "bk_ble_gatts_cb_param_t::gatts_add_char_evt_param") add\_char
    :   Gatt server callback param of BK\_GATTS\_ADD\_CHAR\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t14add_char_descrE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t14add_char_descrE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t14add_char_descrE"></a> <a id="bk_ble_gatts_cb_param_t::add_char_descr__bk_ble_gatts_cb_param_t::gatts_add_char_descr_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a0c170e7359c78bb80c7c9fe21a1edd67"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_add\_char\_descr\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_paramE "bk_ble_gatts_cb_param_t::gatts_add_char_descr_evt_param") add\_char\_descr
    :   Gatt server callback param of BK\_GATTS\_ADD\_CHAR\_DESCR\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t5startE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t5startE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t5startE"></a> <a id="bk_ble_gatts_cb_param_t::start__bk_ble_gatts_cb_param_t::gatts_start_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a33618fd40cef11d4b012974fbb6ada4d"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_start\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t21gatts_start_evt_paramE "bk_ble_gatts_cb_param_t::gatts_start_evt_param") start
    :   Gatt server callback param of BK\_GATTS\_START\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t4stopE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t4stopE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t4stopE"></a> <a id="bk_ble_gatts_cb_param_t::stop__bk_ble_gatts_cb_param_t::gatts_stop_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a7b63484ec69816858f8e479dc20c2ac0"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_stop\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t20gatts_stop_evt_paramE "bk_ble_gatts_cb_param_t::gatts_stop_evt_param") stop
    :   Gatt server callback param of BK\_GATTS\_STOP\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t7connectE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t7connectE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t7connectE"></a> <a id="bk_ble_gatts_cb_param_t::connect__bk_ble_gatts_cb_param_t::gatts_connect_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1aea98dd4563e3e506a6c78b1225bceb43"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_connect\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t23gatts_connect_evt_paramE "bk_ble_gatts_cb_param_t::gatts_connect_evt_param") connect
    :   Gatt server callback param of BK\_GATTS\_CONNECT\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t10disconnectE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t10disconnectE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t10disconnectE"></a> <a id="bk_ble_gatts_cb_param_t::disconnect__bk_ble_gatts_cb_param_t::gatts_disconnect_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1ac7290a1a9cb727f20f9033330cb00be9"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_disconnect\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_paramE "bk_ble_gatts_cb_param_t::gatts_disconnect_evt_param") disconnect
    :   Gatt server callback param of BK\_GATTS\_DISCONNECT\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t3rspE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t3rspE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t3rspE"></a> <a id="bk_ble_gatts_cb_param_t::rsp__bk_ble_gatts_cb_param_t::gatts_rsp_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a2c3a0414099964773cc6b9e8a7aa4423"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_rsp\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_paramE "bk_ble_gatts_cb_param_t::gatts_rsp_evt_param") rsp
    :   Gatt server callback param of BK\_GATTS\_RESPONSE\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t12add_attr_tabE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t12add_attr_tabE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t12add_attr_tabE"></a> <a id="bk_ble_gatts_cb_param_t::add_attr_tab__bk_ble_gatts_cb_param_t::gatts_add_attr_tab_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a6042b6e494726d43b15d5bcaf7bbfad7"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_add\_attr\_tab\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_paramE "bk_ble_gatts_cb_param_t::gatts_add_attr_tab_evt_param") add\_attr\_tab
    :   Gatt server callback param of BK\_GATTS\_CREAT\_ATTR\_TAB\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t12set_attr_valE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t12set_attr_valE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t12set_attr_valE"></a> <a id="bk_ble_gatts_cb_param_t::set_attr_val__bk_ble_gatts_cb_param_t::gatts_set_attr_val_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a14da28353480214d500c973e8c060faf"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_set\_attr\_val\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_paramE "bk_ble_gatts_cb_param_t::gatts_set_attr_val_evt_param") set\_attr\_val
    :   Gatt server callback param of BK\_GATTS\_SET\_ATTR\_VAL\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t14service_changeE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t14service_changeE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t14service_changeE"></a> <a id="bk_ble_gatts_cb_param_t::service_change__bk_ble_gatts_cb_param_t::gatts_send_service_change_evt_param"></a> <a id="unionbk__ble__gatts__cb__param__t_1a81c2f5b8881b4e73419264429e5c89ab"></a> struct [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t")::[gatts\_send\_service\_change\_evt\_param](#_CPPv4N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_paramE "bk_ble_gatts_cb_param_t::gatts_send_service_change_evt_param") service\_change
    :   Gatt server callback param of BK\_GATTS\_SEND\_SERVICE\_CHANGE\_EVT

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_attr_tab_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__attr__tab__evt__param"></a> struct gatts\_add\_attr\_tab\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_CREAT\_ATTR\_TAB\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_attr_tab_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__attr__tab__evt__param_1aa661a62ed72b5d81d118c5bdc3f61c2b"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param8svc_uuidE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param8svc_uuidE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param8svc_uuidE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_attr_tab_evt_param::svc_uuid__bk_bt_uuid_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__attr__tab__evt__param_1a9d8e8f00895f66fe65c1e07b7c11a968"></a> [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") svc\_uuid
        :   Service uuid type

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param10num_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param10num_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param10num_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_attr_tab_evt_param::num_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__attr__tab__evt__param_1a20b94b85a3393b3e136c0ee9e1063a1f"></a> uint16\_t num\_handle
        :   The number of the attribute handle to be added to the gatts database

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param7handlesE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param7handlesE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t28gatts_add_attr_tab_evt_param7handlesE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_attr_tab_evt_param::handles__uint16_tP"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__attr__tab__evt__param_1ae593cf468decc6ff1d59a33930f31015"></a> uint16\_t \*handles
        :   The number to the handles

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_descr_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__descr__evt__param"></a> struct gatts\_add\_char\_descr\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_ADD\_CHAR\_DESCR\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_descr_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__descr__evt__param_1a94381a2dd68316d71b898f2af9795552"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param11attr_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param11attr_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param11attr_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_descr_evt_param::attr_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__descr__evt__param_1aea3a3e68f2947d73a46786f949a14a83"></a> uint16\_t attr\_handle
        :   Descriptor attribute handle

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param14service_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param14service_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param14service_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_descr_evt_param::service_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__descr__evt__param_1ad267238a869b3e32bd63fb37f901c985"></a> uint16\_t service\_handle
        :   Service attribute handle

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param10descr_uuidE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param10descr_uuidE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t30gatts_add_char_descr_evt_param10descr_uuidE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_descr_evt_param::descr_uuid__bk_bt_uuid_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__descr__evt__param_1a8cd66643fc698da68d78648cb18c05ae"></a> [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") descr\_uuid
        :   Characteristic descriptor uuid

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__evt__param"></a> struct gatts\_add\_char\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_ADD\_CHAR\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__evt__param_1afcb71aebcd08f811022428658d153e75"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param11attr_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param11attr_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param11attr_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_evt_param::attr_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__evt__param_1abe2fdf3b09c76397fdf9874e514cebc3"></a> uint16\_t attr\_handle
        :   Characteristic attribute handle

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param14service_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param14service_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param14service_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_evt_param::service_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__evt__param_1a066e57e2be8d0b49de55cd1216b3d696"></a> uint16\_t service\_handle
        :   Service attribute handle

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param9char_uuidE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param9char_uuidE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t24gatts_add_char_evt_param9char_uuidE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_add_char_evt_param::char_uuid__bk_bt_uuid_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__add__char__evt__param_1a7c041dd039a900e4171b8d9d644ecd9a"></a> [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") char\_uuid
        :   Characteristic uuid

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_conf_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_conf_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_conf_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_conf_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__conf__evt__param"></a> struct gatts\_conf\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_CONF\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_conf_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__conf__evt__param_1af43515ed346daf14da4316c20ad9b3c2"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param7conn_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_conf_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__conf__evt__param_1ad64ddfc56d5846eabd2299019dba42c4"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param6handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param6handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param6handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_conf_evt_param::handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__conf__evt__param_1a36e1337b27cd946c5d75c0ebf8c3d9af"></a> uint16\_t handle
        :   attribute handle. Not used when send indicate

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param3lenE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param3lenE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param3lenE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_conf_evt_param::len__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__conf__evt__param_1a5b0c86cb982ab0e8ea331da9d21d27a4"></a> uint16\_t len
        :   The indication or notification value length, len is valid when send notification or indication failed. Not used when indicate

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param5valueE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param5valueE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_conf_evt_param5valueE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_conf_evt_param::value__uint8_tP"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__conf__evt__param_1a18a953a977c5aeba844d5ae8ada242bc"></a> uint8\_t \*value
        :   The indication or notification value , value is valid when send notification or indication failed. Not used when indicate

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t23gatts_connect_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t23gatts_connect_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t23gatts_connect_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_connect_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__connect__evt__param"></a> struct gatts\_connect\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_CONNECT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param7conn_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_connect_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__connect__evt__param_1a850e7e84a7653d450aa6a29c758027ee"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param9link_roleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param9link_roleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param9link_roleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_connect_evt_param::link_role__uint8_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__connect__evt__param_1a67eba4ff8623d04a72e1751fb334b298"></a> uint8\_t link\_role
        :   Link role : master role \= 0 ; slave role \= 1

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param10remote_bdaE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param10remote_bdaE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param10remote_bdaE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_connect_evt_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__connect__evt__param_1a1c1e48bcbd592997cb7aaae26a6db959"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param11conn_paramsE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param11conn_paramsE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t23gatts_connect_evt_param11conn_paramsE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_connect_evt_param::conn_params__bk_gatt_conn_params_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__connect__evt__param_1a83cab547dc65c29a96f5b732c9629bd9"></a> [bk\_gatt\_conn\_params\_t](#_CPPv421bk_gatt_conn_params_t "bk_gatt_conn_params_t") conn\_params
        :   current Connection parameters. Not used now

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t22gatts_create_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t22gatts_create_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t22gatts_create_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_create_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__create__evt__param"></a> struct gatts\_create\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_UNREG\_EVT.

        BK\_GATTS\_CREATE\_EVT

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t22gatts_create_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t22gatts_create_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t22gatts_create_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_create_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__create__evt__param_1a38474a58902f2ed7283b882cf1b321ef"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t22gatts_create_evt_param14service_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t22gatts_create_evt_param14service_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t22gatts_create_evt_param14service_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_create_evt_param::service_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__create__evt__param_1aaa065729e50fd303a177e59da8c965ea"></a> uint16\_t service\_handle
        :   Service attribute handle

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t22gatts_create_evt_param10service_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t22gatts_create_evt_param10service_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t22gatts_create_evt_param10service_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_create_evt_param::service_id__bk_gatt_srvc_id_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__create__evt__param_1a02b2e4cab3f4517f29e7100811dbef8f"></a> [bk\_gatt\_srvc\_id\_t](#_CPPv417bk_gatt_srvc_id_t "bk_gatt_srvc_id_t") service\_id
        :   Service id, include service uuid and other information

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_disconnect_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__disconnect__evt__param"></a> struct gatts\_disconnect\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_DISCONNECT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_param6reasonE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_param6reasonE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_param6reasonE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_disconnect_evt_param::reason__bk_gatt_conn_reason_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__disconnect__evt__param_1af77d6c60308e99b58e1a7c41183c580f"></a> [bk\_gatt\_conn\_reason\_t](#_CPPv421bk_gatt_conn_reason_t "bk_gatt_conn_reason_t") reason
        :   The reason of gatt connection close

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_param7conn_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_disconnect_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__disconnect__evt__param_1af73f03eb8ba69a14859429a83f904659"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_param10remote_bdaE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_param10remote_bdaE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_disconnect_evt_param10remote_bdaE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_disconnect_evt_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__disconnect__evt__param_1a3f0df28ce5da85d9b3d8b7e9385ada7e"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_exec_write_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__exec__write__evt__param"></a> struct gatts\_exec\_write\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_EXEC\_WRITE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param7conn_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_exec_write_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__exec__write__evt__param_1a24a8e08bab48cf14941627302d47cd9c"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param8trans_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param8trans_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param8trans_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_exec_write_evt_param::trans_id__uint32_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__exec__write__evt__param_1a9040f80a2b2b321dd957b2cfb11a781d"></a> uint32\_t trans\_id
        :   Transaction id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param3bdaE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param3bdaE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param3bdaE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_exec_write_evt_param::bda__bk_bd_addr_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__exec__write__evt__param_1aa0b728c301459baae1a35af5c2faae9b"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   The bluetooth device address which been written

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param15exec_write_flagE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param15exec_write_flagE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param15exec_write_flagE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_exec_write_evt_param::exec_write_flag__uint8_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__exec__write__evt__param_1a2a616c86831f5c0bf6ba2ab0559b9ece"></a> uint8\_t exec\_write\_flag
        :   Execute write flag

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param8need_rspE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param8need_rspE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t26gatts_exec_write_evt_param8need_rspE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_exec_write_evt_param::need_rsp__b"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__exec__write__evt__param_1ae13ebb0222406338fb4f4fafd9e3c162"></a> bool need\_rsp

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_mtu_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__mtu__evt__param"></a> struct gatts\_mtu\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_MTU\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_param7conn_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_mtu_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__mtu__evt__param_1a84b1151210db4cc920b97ab241cd8861"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_param3mtuE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_param3mtuE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_mtu_evt_param3mtuE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_mtu_evt_param::mtu__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__mtu__evt__param_1a7ff2e87e7033a29d7d4c28cc15dff082"></a> uint16\_t mtu
        :   MTU size

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_read_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_read_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_read_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__read__evt__param"></a> struct gatts\_read\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_READ\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_read_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_read_evt_param7conn_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_read_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__read__evt__param_1a95eb16213098d2d6ac7d35e1baade7c3"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_param8trans_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_read_evt_param8trans_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_read_evt_param8trans_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_read_evt_param::trans_id__uint32_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__read__evt__param_1a413291790eeead0698dd8c8a5e0629e3"></a> uint32\_t trans\_id
        :   Transaction id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_param3bdaE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_read_evt_param3bdaE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_read_evt_param3bdaE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_read_evt_param::bda__bk_bd_addr_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__read__evt__param_1a802a668ec3148617f2dc84f567156bf3"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   The bluetooth device address which been read

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_param6handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_read_evt_param6handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_read_evt_param6handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_read_evt_param::handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__read__evt__param_1adef0cc4ddce94390d79d7a975b4fd952"></a> uint16\_t handle
        :   The attribute handle

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_param6offsetE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_read_evt_param6offsetE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_read_evt_param6offsetE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_read_evt_param::offset__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__read__evt__param_1a32fb929fdccb5a2dfec3d4c7e89a725f"></a> uint16\_t offset
        :   Offset of the value, if the value is too long

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_param7is_longE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_read_evt_param7is_longE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_read_evt_param7is_longE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_read_evt_param::is_long__b"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__read__evt__param_1a92ead3b159d662aa8b9956c9d000b7ec"></a> bool is\_long
        :   The value is too long or not

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_read_evt_param8need_rspE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_read_evt_param8need_rspE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_read_evt_param8need_rspE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_read_evt_param::need_rsp__b"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__read__evt__param_1a6b8ae064f77fed5843fa135b3616ab82"></a> bool need\_rsp
        :   The read operation need to do response

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_reg_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_reg_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_reg_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_reg_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__reg__evt__param"></a> struct gatts\_reg\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_REG\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_reg_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_reg_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_reg_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_reg_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__reg__evt__param_1a3fd750f25b2cdf0ee8bab1ce6f37ce0d"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_reg_evt_param6app_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_reg_evt_param6app_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_reg_evt_param6app_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_reg_evt_param::app_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__reg__evt__param_1a049a9877314ae43870a47fa62aef21ce"></a> uint16\_t app\_id
        :   Application id which input in register API, not used now

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_reg_evt_param7gatt_ifE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_reg_evt_param7gatt_ifE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_reg_evt_param7gatt_ifE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_reg_evt_param::gatt_if__bk_gatt_if_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__reg__evt__param_1a91f93c96e8db373e2f8d0ce9aca2fcf4"></a> [bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatt\_if

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_rsp_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__rsp__evt__param"></a> struct gatts\_rsp\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_RESPONSE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_rsp_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__rsp__evt__param_1a55e9440304063d123a7f0b10f33ac599"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param6handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param6handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param6handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_rsp_evt_param::handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__rsp__evt__param_1ac88e6448200d8e5179907cfa7545ba30"></a> uint16\_t handle
        :   Attribute handle which send response

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param7conn_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_rsp_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__rsp__evt__param_1af40ff598b80e667a554789601bd5a4c1"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param10remote_bdaE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param10remote_bdaE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t19gatts_rsp_evt_param10remote_bdaE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_rsp_evt_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__rsp__evt__param_1ab2ad977a7645032a5436133dfae621b3"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_send_service_change_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__send__service__change__evt__param"></a> struct gatts\_send\_service\_change\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_SEND\_SERVICE\_CHANGE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_send_service_change_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__send__service__change__evt__param_1a1015d11acf3c9c121430e0d3dd2bd15d"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_param7conn_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_send_service_change_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__send__service__change__evt__param_1a396b77662ba7a49b2447f5e2dcd312a3"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_param10remote_bdaE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_param10remote_bdaE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t35gatts_send_service_change_evt_param10remote_bdaE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_send_service_change_evt_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__send__service__change__evt__param_1ae39a2dbebe2eb475d63a0cde674adeae"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_set_attr_val_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__set__attr__val__evt__param"></a> struct gatts\_set\_attr\_val\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_SET\_ATTR\_VAL\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_param11srvc_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_param11srvc_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_param11srvc_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_set_attr_val_evt_param::srvc_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__set__attr__val__evt__param_1a2fbada061e5cf3044e9bf4a2e8fc3209"></a> uint16\_t srvc\_handle
        :   The service handle

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_param11attr_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_param11attr_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_param11attr_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_set_attr_val_evt_param::attr_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__set__attr__val__evt__param_1a14d5e28c1837e4858ad2061f95ea9436"></a> uint16\_t attr\_handle
        :   The attribute handle

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t28gatts_set_attr_val_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_set_attr_val_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__set__attr__val__evt__param_1a18fc3b978cce0b56d2bf8da63e859500"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_start_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_start_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_start_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_start_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__start__evt__param"></a> struct gatts\_start\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_START\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_start_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_start_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_start_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_start_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__start__evt__param_1a843b9d444c48b77d4d5b59d575f4fa6c"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_start_evt_param14service_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_start_evt_param14service_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_start_evt_param14service_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_start_evt_param::service_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__start__evt__param_1a1a8b9f61e7dce844476c4500e838d637"></a> uint16\_t service\_handle
        :   Service attribute handle

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_stop_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_stop_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_stop_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_stop_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__stop__evt__param"></a> struct gatts\_stop\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_STOP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_stop_evt_param6statusE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_stop_evt_param6statusE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_stop_evt_param6statusE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_stop_evt_param::status__bk_gatt_status_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__stop__evt__param_1a2c0736ca380ae00aa2370103f340d896"></a> [bk\_gatt\_status\_t](#_CPPv416bk_gatt_status_t "bk_gatt_status_t") status
        :   Operation status

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t20gatts_stop_evt_param14service_handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t20gatts_stop_evt_param14service_handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t20gatts_stop_evt_param14service_handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_stop_evt_param::service_handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__stop__evt__param_1ad77e0452ca1b7d76b57e41579110619a"></a> uint16\_t service\_handle
        :   Service attribute handle

    <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_paramE"></a>

    <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_paramE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_paramE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param"></a> struct gatts\_write\_evt\_param
    :   *#include \<bk\_dm\_gatts.h\>*

        BK\_GATTS\_WRITE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_param7conn_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_param7conn_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_param7conn_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param::conn_id__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param_1a04cb100aa718fc382a914c15b3b1f07a"></a> uint16\_t conn\_id
        :   Connection id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_param8trans_idE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_param8trans_idE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_param8trans_idE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param::trans_id__uint32_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param_1ae073afb480930cba4fef64ce98be6286"></a> uint32\_t trans\_id
        :   Transaction id

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_param3bdaE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_param3bdaE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_param3bdaE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param::bda__bk_bd_addr_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param_1a7af84eecd078a062c61d54a75195199f"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   The bluetooth device address which been written

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_param6handleE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_param6handleE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_param6handleE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param::handle__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param_1a382e8f5c3c208a472a3db39d3325aade"></a> uint16\_t handle
        :   The attribute handle

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_param6offsetE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_param6offsetE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_param6offsetE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param::offset__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param_1aee27ee713270cb16a240dfba5930dac6"></a> uint16\_t offset
        :   Offset of the value, if the value is too long

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_param8need_rspE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_param8need_rspE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_param8need_rspE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param::need_rsp__b"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param_1ab192ffa42ec4963895176eec12bdbc06"></a> bool need\_rsp
        :   The write operation need to do response

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_param7is_prepE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_param7is_prepE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_param7is_prepE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param::is_prep__b"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param_1a799c4e0a80d355e84e840d5cc2e2f91a"></a> bool is\_prep
        :   This write operation is prepare write

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_param3lenE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_param3lenE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_param3lenE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param::len__uint16_t"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param_1ac7584fda164ea714427b4f1ba85d48ce"></a> uint16\_t len
        :   The write attribute value length

        <a id="_CPPv4N23bk_ble_gatts_cb_param_t21gatts_write_evt_param5valueE"></a>

        <a id="_CPPv3N23bk_ble_gatts_cb_param_t21gatts_write_evt_param5valueE"></a> <a id="_CPPv2N23bk_ble_gatts_cb_param_t21gatts_write_evt_param5valueE"></a> <a id="bk_ble_gatts_cb_param_t::gatts_write_evt_param::value__uint8_tP"></a> <a id="structbk__ble__gatts__cb__param__t_1_1gatts__write__evt__param_1ad3a7818e4f3066c9132c92a26f82d563"></a> uint8\_t \*value
        :   The write attribute value

<a id="macros"></a>

### Macros

<a id="c.BK_GATT_PREP_WRITE_CANCEL"></a>

<a id="bk__dm__gatts_8h_1aa0b928fd74ffb53128c4e33539cd3fc2"></a> BK\_GATT\_PREP\_WRITE\_CANCEL
:   Prepare write flag to indicate cancel prepare write

<a id="c.BK_GATT_PREP_WRITE_EXEC"></a>

<a id="bk__dm__gatts_8h_1a4f5bc5a97926d5e67873db6c8ecad43e"></a> BK\_GATT\_PREP\_WRITE\_EXEC
:   Prepare write flag to indicate execute prepare write

<a id="id9"></a>

### Type Definitions

<a id="_CPPv413bk_gatts_cb_t"></a>

<a id="_CPPv313bk_gatts_cb_t"></a> <a id="_CPPv213bk_gatts_cb_t"></a> <a id="bk_gatts_cb_t"></a> <a id="group__dm__gatts__types__v1_1gaba1c16457f7bb9e58e3848be7d3b71a7"></a> typedef int32\_t (\*bk\_gatts\_cb\_t)([bk\_gatts\_cb\_event\_t](#_CPPv419bk_gatts_cb_event_t "bk_gatts_cb_event_t") event, [bk\_gatt\_if\_t](#_CPPv412bk_gatt_if_t "bk_gatt_if_t") gatts\_if, [bk\_ble\_gatts\_cb\_param\_t](#_CPPv423bk_ble_gatts_cb_param_t "bk_ble_gatts_cb_param_t") \*param)
:   GATT Server callback function type.

    Param event
    :   : Event type

    Param gatts\_if
    :   : GATT server access interface, normally different gatts\_if correspond to different profile

    Param param
    :   : Point to callback parameter, currently is union type

<a id="id10"></a>

### Enumerations

<a id="_CPPv419bk_gatts_cb_event_t"></a>

<a id="_CPPv319bk_gatts_cb_event_t"></a> <a id="_CPPv219bk_gatts_cb_event_t"></a> <a id="group__dm__gatts__types__v1_1ga20b7bade865d1e6ac7399d979f2bf032"></a> enum bk\_gatts\_cb\_event\_t
:   GATT Server callback function events.

    *Values:*

    <a id="_CPPv4N19bk_gatts_cb_event_t16BK_GATTS_REG_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t16BK_GATTS_REG_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t16BK_GATTS_REG_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a29b104722c53781081e518f90857647a"></a> enumerator BK\_GATTS\_REG\_EVT
    :   When register application id, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t17BK_GATTS_READ_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t17BK_GATTS_READ_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t17BK_GATTS_READ_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032aee6fc6e463cb38f0cf0b1198edbc5e11"></a> enumerator BK\_GATTS\_READ\_EVT
    :   When gatt client request read operation, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t18BK_GATTS_WRITE_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t18BK_GATTS_WRITE_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t18BK_GATTS_WRITE_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a477a6a6e2b4a1811bb0dc8545563d1fa"></a> enumerator BK\_GATTS\_WRITE\_EVT
    :   When gatt client request write operation, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t23BK_GATTS_EXEC_WRITE_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t23BK_GATTS_EXEC_WRITE_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t23BK_GATTS_EXEC_WRITE_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032aa6a5bebb17a9c65c23a6793749a3c090"></a> enumerator BK\_GATTS\_EXEC\_WRITE\_EVT
    :   When gatt client request execute write, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t16BK_GATTS_MTU_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t16BK_GATTS_MTU_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t16BK_GATTS_MTU_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a8b8bf6ac91763c0c8155aaad33ed61cc"></a> enumerator BK\_GATTS\_MTU\_EVT
    :   When set mtu complete, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t17BK_GATTS_CONF_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t17BK_GATTS_CONF_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t17BK_GATTS_CONF_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a5852ada3dd2b026a35c1356499af9a2a"></a> enumerator BK\_GATTS\_CONF\_EVT
    :   When receive confirm after send notify or indicate, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t18BK_GATTS_UNREG_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t18BK_GATTS_UNREG_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t18BK_GATTS_UNREG_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a0f7083765ce120d09ced33c8c0164c1c"></a> enumerator BK\_GATTS\_UNREG\_EVT
    :   When unregister gatt\_if, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t19BK_GATTS_CREATE_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t19BK_GATTS_CREATE_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t19BK_GATTS_CREATE_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032aaafbaf643080ec1551674361c2df796a"></a> enumerator BK\_GATTS\_CREATE\_EVT
    :   When create service complete, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t21BK_GATTS_ADD_CHAR_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t21BK_GATTS_ADD_CHAR_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t21BK_GATTS_ADD_CHAR_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a3af32457e4097e99abc85a9044190b37"></a> enumerator BK\_GATTS\_ADD\_CHAR\_EVT
    :   When add characteristic complete, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t27BK_GATTS_ADD_CHAR_DESCR_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t27BK_GATTS_ADD_CHAR_DESCR_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t27BK_GATTS_ADD_CHAR_DESCR_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032ab534cd067923a07fcac9c9ca911aac98"></a> enumerator BK\_GATTS\_ADD\_CHAR\_DESCR\_EVT
    :   When add descriptor complete, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t18BK_GATTS_START_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t18BK_GATTS_START_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t18BK_GATTS_START_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a7f6faf852d966eb13cceee7de738196d"></a> enumerator BK\_GATTS\_START\_EVT
    :   When start service complete, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t17BK_GATTS_STOP_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t17BK_GATTS_STOP_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t17BK_GATTS_STOP_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a835afce7295e44820f067a26a7c9d7da"></a> enumerator BK\_GATTS\_STOP\_EVT
    :   When stop service complete, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t20BK_GATTS_CONNECT_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t20BK_GATTS_CONNECT_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t20BK_GATTS_CONNECT_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032af2f8a9b499914d9a5fdc1d1627fe2616"></a> enumerator BK\_GATTS\_CONNECT\_EVT
    :   When gatt client connect, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t23BK_GATTS_DISCONNECT_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t23BK_GATTS_DISCONNECT_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t23BK_GATTS_DISCONNECT_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032ad6da1f59e4eaf28900b5c916b0a3c6f5"></a> enumerator BK\_GATTS\_DISCONNECT\_EVT
    :   When gatt client disconnect, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t21BK_GATTS_RESPONSE_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t21BK_GATTS_RESPONSE_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t21BK_GATTS_RESPONSE_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a8429493effb9ae69b25d31c76ba87fb2"></a> enumerator BK\_GATTS\_RESPONSE\_EVT
    :   When gatt send write/read/error response complete, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t27BK_GATTS_CREAT_ATTR_TAB_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t27BK_GATTS_CREAT_ATTR_TAB_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t27BK_GATTS_CREAT_ATTR_TAB_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032afe4e0414baf2ab607b2ce19cc9d7db07"></a> enumerator BK\_GATTS\_CREAT\_ATTR\_TAB\_EVT
    :   When gatt create table complete, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t25BK_GATTS_SET_ATTR_VAL_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t25BK_GATTS_SET_ATTR_VAL_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t25BK_GATTS_SET_ATTR_VAL_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032a3a6d383ca68ef18ac8f7bf1967967b71"></a> enumerator BK\_GATTS\_SET\_ATTR\_VAL\_EVT
    :   When gatt set attr value complete, the event comes

    <a id="_CPPv4N19bk_gatts_cb_event_t32BK_GATTS_SEND_SERVICE_CHANGE_EVTE"></a>

    <a id="_CPPv3N19bk_gatts_cb_event_t32BK_GATTS_SEND_SERVICE_CHANGE_EVTE"></a> <a id="_CPPv2N19bk_gatts_cb_event_t32BK_GATTS_SEND_SERVICE_CHANGE_EVTE"></a> <a id="group__dm__gatts__types__v1_1gga20b7bade865d1e6ac7399d979f2bf032af5f92532e502134ba10dfcb6608d6614"></a> enumerator BK\_GATTS\_SEND\_SERVICE\_CHANGE\_EVT
    :   When gatt send service change indication complete, the event comes

<a id="_CPPv436bk_gatts_char_property_bit_mask_op_t"></a>

<a id="_CPPv336bk_gatts_char_property_bit_mask_op_t"></a> <a id="_CPPv236bk_gatts_char_property_bit_mask_op_t"></a> <a id="group__dm__gatts__types__v1_1ga45c3884502760653358070336e01d418"></a> enum bk\_gatts\_char\_property\_bit\_mask\_op\_t
:   *Values:*

    <a id="_CPPv4N36bk_gatts_char_property_bit_mask_op_t38BK_GATTS_CHAR_PROPERTY_BIT_MASK_OP_GETE"></a>

    <a id="_CPPv3N36bk_gatts_char_property_bit_mask_op_t38BK_GATTS_CHAR_PROPERTY_BIT_MASK_OP_GETE"></a> <a id="_CPPv2N36bk_gatts_char_property_bit_mask_op_t38BK_GATTS_CHAR_PROPERTY_BIT_MASK_OP_GETE"></a> <a id="group__dm__gatts__types__v1_1gga45c3884502760653358070336e01d418a02f59f9cc11199644cd774f6b0cc2b2f"></a> enumerator BK\_GATTS\_CHAR\_PROPERTY\_BIT\_MASK\_OP\_GET

    <a id="_CPPv4N36bk_gatts_char_property_bit_mask_op_t38BK_GATTS_CHAR_PROPERTY_BIT_MASK_OP_SETE"></a>

    <a id="_CPPv3N36bk_gatts_char_property_bit_mask_op_t38BK_GATTS_CHAR_PROPERTY_BIT_MASK_OP_SETE"></a> <a id="_CPPv2N36bk_gatts_char_property_bit_mask_op_t38BK_GATTS_CHAR_PROPERTY_BIT_MASK_OP_SETE"></a> <a id="group__dm__gatts__types__v1_1gga45c3884502760653358070336e01d418a376980ada858ee1b526060e183b4de17"></a> enumerator BK\_GATTS\_CHAR\_PROPERTY\_BIT\_MASK\_OP\_SET

<a id="bk-dm-gatt-common-h"></a>

## bk\_dm\_gatt\_common.h

`bk_dm_gatt_common.h` 定义 BLE GATT Client 和 Server 共用的接口与辅助能力。

<a id="id11"></a>

### Header File

- [bk\_dm\_gatt\_common.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_gatt_common.h)

<a id="id12"></a>

### Functions

<a id="_CPPv425bk_ble_gatt_set_local_mtu8uint16_t"></a>

<a id="_CPPv325bk_ble_gatt_set_local_mtu8uint16_t"></a> <a id="_CPPv225bk_ble_gatt_set_local_mtu8uint16_t"></a> <a id="bk_ble_gatt_set_local_mtu__uint16_t"></a> <a id="group__dm__gatt__common__functions__v1_1ga07d73be77fe528eeaa17df45fb6d4efe"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatt\_set\_local\_mtu(uint16\_t mtu)
:   This function is called to set local MTU, the function is called before BLE connection.

    参数
    :   **mtu** – **\[in\]** the size of MTU. Max is 517, min is 23

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv439bk_ble_get_hci_handle_from_gatt_conn_id8uint16_tP8uint16_t"></a>

<a id="_CPPv339bk_ble_get_hci_handle_from_gatt_conn_id8uint16_tP8uint16_t"></a> <a id="_CPPv239bk_ble_get_hci_handle_from_gatt_conn_id8uint16_tP8uint16_t"></a> <a id="bk_ble_get_hci_handle_from_gatt_conn_id__uint16_t.uint16_tP"></a> <a id="group__dm__gatt__common__functions__v1_1ga41df0de8c280582c831bc239ac2bbccc"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_get\_hci\_handle\_from\_gatt\_conn\_id(uint16\_t gatt\_conn\_id, uint16\_t \*hci\_handle)
:   This function is use to get hci\_handle from gatt conn id,.

    **Attention**
    :   1\. This function only could be used when connection exist.

    参数
    :   - **gatt\_conn\_id** – **\[in\]** id from gatts\_connect\_evt\_param/gattc\_connect\_evt\_param
        - **\[in\|out\]** – hci\_handle: output hci handle

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="_CPPv439bk_ble_get_gatt_conn_id_from_hci_handle8uint16_tP8uint16_t"></a>

<a id="_CPPv339bk_ble_get_gatt_conn_id_from_hci_handle8uint16_tP8uint16_t"></a> <a id="_CPPv239bk_ble_get_gatt_conn_id_from_hci_handle8uint16_tP8uint16_t"></a> <a id="bk_ble_get_gatt_conn_id_from_hci_handle__uint16_t.uint16_tP"></a> <a id="group__dm__gatt__common__functions__v1_1ga945639df68df0e3282cfc28b50d295f7"></a> [ble\_err\_t](single_ble.md#_CPPv49ble_err_t "ble_err_t") bk\_ble\_get\_gatt\_conn\_id\_from\_hci\_handle(uint16\_t hci\_handle, uint16\_t \*gatt\_conn\_id)
:   This function is use to get gatt conn id from hci\_handle,.

    **Attention**
    :   1\. This function only could be used when connection exist.

    参数
    :   - **hci\_handle** – **\[in\]** hci handle from BK\_BLE\_GAP\_CONNECT\_COMPLETE\_EVT
        - **\[in\|out\]** – gatt\_conn\_id: output gatt conn id

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: success
        - other: failed

<a id="id13"></a>

## API 类型定义

<a id="bk-dm-gap-ble-types-h"></a>

## bk\_dm\_gap\_ble\_types.h

`bk_dm_gap_ble_types.h` 定义 BLE GAP 使用的参数、事件和状态类型。

<a id="id14"></a>

### Header File

- [bk\_dm\_gap\_ble\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_gap_ble_types.h)

<a id="id15"></a>

### Unions

<a id="_CPPv418bk_ble_key_value_t"></a>

<a id="_CPPv318bk_ble_key_value_t"></a> <a id="_CPPv218bk_ble_key_value_t"></a> <a id="unionbk__ble__key__value__t"></a> union bk\_ble\_key\_value\_t
:   *#include \<bk\_dm\_gap\_ble\_types.h\>*

    union type of the security key value

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_ble_key_value_t8penc_keyE"></a>

    <a id="_CPPv3N18bk_ble_key_value_t8penc_keyE"></a> <a id="_CPPv2N18bk_ble_key_value_t8penc_keyE"></a> <a id="bk_ble_key_value_t::penc_key__bk_ble_penc_keys_t"></a> <a id="unionbk__ble__key__value__t_1a09e60f5f7cc2def7c4bb5439429b7cde"></a> [bk\_ble\_penc\_keys\_t](#_CPPv418bk_ble_penc_keys_t "bk_ble_penc_keys_t") penc\_key
    :   received peer encryption key

    <a id="_CPPv4N18bk_ble_key_value_t9pcsrk_keyE"></a>

    <a id="_CPPv3N18bk_ble_key_value_t9pcsrk_keyE"></a> <a id="_CPPv2N18bk_ble_key_value_t9pcsrk_keyE"></a> <a id="bk_ble_key_value_t::pcsrk_key__bk_ble_pcsrk_keys_t"></a> <a id="unionbk__ble__key__value__t_1a46342411157c92039a65273aa6fc37f5"></a> [bk\_ble\_pcsrk\_keys\_t](#_CPPv419bk_ble_pcsrk_keys_t "bk_ble_pcsrk_keys_t") pcsrk\_key
    :   received peer device SRK

    <a id="_CPPv4N18bk_ble_key_value_t7pid_keyE"></a>

    <a id="_CPPv3N18bk_ble_key_value_t7pid_keyE"></a> <a id="_CPPv2N18bk_ble_key_value_t7pid_keyE"></a> <a id="bk_ble_key_value_t::pid_key__bk_ble_pid_keys_t"></a> <a id="unionbk__ble__key__value__t_1af95bf8b1c532cdccbe93bd7225e5de45"></a> [bk\_ble\_pid\_keys\_t](#_CPPv417bk_ble_pid_keys_t "bk_ble_pid_keys_t") pid\_key
    :   peer device ID key

    <a id="_CPPv4N18bk_ble_key_value_t8lenc_keyE"></a>

    <a id="_CPPv3N18bk_ble_key_value_t8lenc_keyE"></a> <a id="_CPPv2N18bk_ble_key_value_t8lenc_keyE"></a> <a id="bk_ble_key_value_t::lenc_key__bk_ble_lenc_keys_t"></a> <a id="unionbk__ble__key__value__t_1ae1c7b2c22b4f393d8e46ec800a8c7201"></a> [bk\_ble\_lenc\_keys\_t](#_CPPv418bk_ble_lenc_keys_t "bk_ble_lenc_keys_t") lenc\_key
    :   local encryption reproduction keys LTK \= \= d1(ER,DIV,0)

    <a id="_CPPv4N18bk_ble_key_value_t9lcsrk_keyE"></a>

    <a id="_CPPv3N18bk_ble_key_value_t9lcsrk_keyE"></a> <a id="_CPPv2N18bk_ble_key_value_t9lcsrk_keyE"></a> <a id="bk_ble_key_value_t::lcsrk_key__bk_ble_lcsrk_keys_t"></a> <a id="unionbk__ble__key__value__t_1a6e0dfa262ec177befa29142dce554b43"></a> [bk\_ble\_lcsrk\_keys\_t](#_CPPv419bk_ble_lcsrk_keys_t "bk_ble_lcsrk_keys_t") lcsrk\_key
    :   local device CSRK \= d1(ER,DIV,1)

<a id="_CPPv412bk_ble_sec_t"></a>

<a id="_CPPv312bk_ble_sec_t"></a> <a id="_CPPv212bk_ble_sec_t"></a> <a id="unionbk__ble__sec__t"></a> union bk\_ble\_sec\_t
:   *#include \<bk\_dm\_gap\_ble\_types.h\>*

    union associated with ble security

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12bk_ble_sec_t9key_notifE"></a>

    <a id="_CPPv3N12bk_ble_sec_t9key_notifE"></a> <a id="_CPPv2N12bk_ble_sec_t9key_notifE"></a> <a id="bk_ble_sec_t::key_notif__bk_ble_sec_key_notif_t"></a> <a id="unionbk__ble__sec__t_1aa932d31e4f5f84952ea0b8a77766817e"></a> [bk\_ble\_sec\_key\_notif\_t](#_CPPv422bk_ble_sec_key_notif_t "bk_ble_sec_key_notif_t") key\_notif
    :   passkey notification/req or number compare notification

    <a id="_CPPv4N12bk_ble_sec_t7ble_reqE"></a>

    <a id="_CPPv3N12bk_ble_sec_t7ble_reqE"></a> <a id="_CPPv2N12bk_ble_sec_t7ble_reqE"></a> <a id="bk_ble_sec_t::ble_req__bk_ble_sec_req_t"></a> <a id="unionbk__ble__sec__t_1a74ca96942dd7d65d2356baf0ca595b16"></a> [bk\_ble\_sec\_req\_t](#_CPPv416bk_ble_sec_req_t "bk_ble_sec_req_t") ble\_req
    :   BLE SMP related request

    <a id="_CPPv4N12bk_ble_sec_t14ble_local_keysE"></a>

    <a id="_CPPv3N12bk_ble_sec_t14ble_local_keysE"></a> <a id="_CPPv2N12bk_ble_sec_t14ble_local_keysE"></a> <a id="bk_ble_sec_t::ble_local_keys__bk_ble_local_keys_t"></a> <a id="unionbk__ble__sec__t_1a5d670d0fb4e26e1b1eb5034276d0727b"></a> [bk\_ble\_local\_keys\_t](#_CPPv419bk_ble_local_keys_t "bk_ble_local_keys_t") ble\_local\_keys
    :   BLE local event

    <a id="_CPPv4N12bk_ble_sec_t9auth_cmplE"></a>

    <a id="_CPPv3N12bk_ble_sec_t9auth_cmplE"></a> <a id="_CPPv2N12bk_ble_sec_t9auth_cmplE"></a> <a id="bk_ble_sec_t::auth_cmpl__bk_ble_auth_cmpl_t"></a> <a id="unionbk__ble__sec__t_1a4a32de57cd9b16dd98d7f024f9ad28c7"></a> [bk\_ble\_auth\_cmpl\_t](#_CPPv418bk_ble_auth_cmpl_t "bk_ble_auth_cmpl_t") auth\_cmpl
    :   Authentication complete indication.

<a id="_CPPv421bk_ble_gap_cb_param_t"></a>

<a id="_CPPv321bk_ble_gap_cb_param_t"></a> <a id="_CPPv221bk_ble_gap_cb_param_t"></a> <a id="unionbk__ble__gap__cb__param__t"></a> union bk\_ble\_gap\_cb\_param\_t
:   *#include \<bk\_dm\_gap\_ble\_types.h\>*

    Gap callback parameters union.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21bk_ble_gap_cb_param_t12ble_securityE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t12ble_securityE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t12ble_securityE"></a> <a id="bk_ble_gap_cb_param_t::ble_security__bk_ble_sec_t"></a> <a id="unionbk__ble__gap__cb__param__t_1a3737901c8c8beacfb1b33c43fbae6f5a"></a> [bk\_ble\_sec\_t](#_CPPv412bk_ble_sec_t "bk_ble_sec_t") ble\_security
    :   ble gap security union type

    <a id="_CPPv4N21bk_ble_gap_cb_param_t18set_rand_addr_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t18set_rand_addr_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t18set_rand_addr_cmplE"></a> <a id="bk_ble_gap_cb_param_t::set_rand_addr_cmpl__bk_ble_gap_cb_param_t::ble_set_rand_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a8d601eebd8987cc6cdbbe35fd4d3d890"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_set\_rand\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_set_rand_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_set_rand_cmpl_evt_param") set\_rand\_addr\_cmpl
    :   Event parameter of BK\_BLE\_GAP\_SET\_STATIC\_RAND\_ADDR\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t18update_conn_paramsE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t18update_conn_paramsE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t18update_conn_paramsE"></a> <a id="bk_ble_gap_cb_param_t::update_conn_params__bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1ab513dc440591dd4d0b67c89bd0b78a77"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_update\_conn\_params\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_paramE "bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param") update\_conn\_params
    :   Event parameter of BK\_BLE\_GAP\_UPDATE\_CONN\_PARAMS\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t20pkt_data_length_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t20pkt_data_length_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t20pkt_data_length_cmplE"></a> <a id="bk_ble_gap_cb_param_t::pkt_data_length_cmpl__bk_ble_gap_cb_param_t::ble_pkt_data_length_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a99319a65383a09c2823fe865f0d7fdf3"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_pkt\_data\_length\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_pkt_data_length_cmpl_evt_param") pkt\_data\_length\_cmpl
    :   Event parameter of BK\_BLE\_GAP\_SET\_PKT\_LENGTH\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t18local_privacy_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t18local_privacy_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t18local_privacy_cmplE"></a> <a id="bk_ble_gap_cb_param_t::local_privacy_cmpl__bk_ble_gap_cb_param_t::ble_local_privacy_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a80ae4a472deeed653ceebefa57a9edc2"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_local\_privacy\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_local_privacy_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_local_privacy_cmpl_evt_param") local\_privacy\_cmpl
    :   Event parameter of BK\_BLE\_GAP\_SET\_LOCAL\_PRIVACY\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t16bond_key_req_evtE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t16bond_key_req_evtE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t16bond_key_req_evtE"></a> <a id="bk_ble_gap_cb_param_t::bond_key_req_evt__bk_ble_gap_cb_param_t::ble_bond_dev_key_req_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a0f8d8939ed4f3c3381e7ab5d943733f9"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_bond\_dev\_key\_req\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t30ble_bond_dev_key_req_evt_paramE "bk_ble_gap_cb_param_t::ble_bond_dev_key_req_evt_param") bond\_key\_req\_evt
    :   Event parameter of BK\_BLE\_GAP\_BOND\_KEY\_REQ\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t25bond_dev_key_generate_evtE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t25bond_dev_key_generate_evtE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25bond_dev_key_generate_evtE"></a> <a id="bk_ble_gap_cb_param_t::bond_dev_key_generate_evt__bk_ble_gap_cb_param_t::ble_bond_dev_key_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a2aeec2a973766750ea4cf11345f2c221"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_bond\_dev\_key\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_paramE "bk_ble_gap_cb_param_t::ble_bond_dev_key_evt_param") bond\_dev\_key\_generate\_evt
    :   Event parameter of BK\_BLE\_GAP\_BOND\_KEY\_GENERATE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t21bond_dev_list_op_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t21bond_dev_list_op_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21bond_dev_list_op_cmplE"></a> <a id="bk_ble_gap_cb_param_t::bond_dev_list_op_cmpl__bk_ble_gap_cb_param_t::ble_bond_dev_list_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a61a2bb3fb500f1e4085e83dbe79572a2"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_bond\_dev\_list\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_paramE "bk_ble_gap_cb_param_t::ble_bond_dev_list_evt_param") bond\_dev\_list\_op\_cmpl
    :   Event parameter of BK\_BLE\_GAP\_BOND\_DEV\_LIST\_OPERATEION\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t14read_rssi_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t14read_rssi_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t14read_rssi_cmplE"></a> <a id="bk_ble_gap_cb_param_t::read_rssi_cmpl__bk_ble_gap_cb_param_t::ble_read_rssi_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1af9e3162d7e7564ec80b1a609b5d3fbcd"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_read\_rssi\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_read_rssi_cmpl_evt_param") read\_rssi\_cmpl
    :   Event parameter of BK\_BLE\_GAP\_READ\_RSSI\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t21update_whitelist_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t21update_whitelist_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21update_whitelist_cmplE"></a> <a id="bk_ble_gap_cb_param_t::update_whitelist_cmpl__bk_ble_gap_cb_param_t::ble_update_whitelist_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a8a84474f154b27535d56f245654e68af"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_update\_whitelist\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_update_whitelist_cmpl_evt_param") update\_whitelist\_cmpl
    :   Event parameter of BK\_BLE\_GAP\_UPDATE\_WHITELIST\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t16ble_set_channelsE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t16ble_set_channelsE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t16ble_set_channelsE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_channels__bk_ble_gap_cb_param_t::ble_set_channels_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1afc54b4bdecddeed4380ab57517d299f9"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_set\_channels\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t31ble_set_channels_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_set_channels_cmpl_evt_param") ble\_set\_channels
    :   Event parameter of BK\_BLE\_GAP\_SET\_CHANNELS\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t8read_phyE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t8read_phyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t8read_phyE"></a> <a id="bk_ble_gap_cb_param_t::read_phy__bk_ble_gap_cb_param_t::ble_read_phy_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1aadf7f3b6e681118494c0c5e3a642e574"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_read\_phy\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_read_phy_cmpl_evt_param") read\_phy
    :   Event parameter of BK\_BLE\_GAP\_READ\_PHY\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t16set_perf_def_phyE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t16set_perf_def_phyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t16set_perf_def_phyE"></a> <a id="bk_ble_gap_cb_param_t::set_perf_def_phy__bk_ble_gap_cb_param_t::ble_set_perf_def_phy_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1ab2d37f85216ec85e94580615d99b38b6"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_set\_perf\_def\_phy\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_set_perf_def_phy_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_set_perf_def_phy_cmpl_evt_param") set\_perf\_def\_phy
    :   Event parameter of BK\_BLE\_GAP\_SET\_PREFERRED\_DEFAULT\_PHY\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t12set_perf_phyE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t12set_perf_phyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t12set_perf_phyE"></a> <a id="bk_ble_gap_cb_param_t::set_perf_phy__bk_ble_gap_cb_param_t::ble_set_perf_phy_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a3b62a5360ab56f4b704457d3d9972114"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_set\_perf\_phy\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t31ble_set_perf_phy_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_set_perf_phy_cmpl_evt_param") set\_perf\_phy
    :   Event parameter of BK\_BLE\_GAP\_SET\_PREFERRED\_PHY\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t17adv_set_rand_addrE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t17adv_set_rand_addrE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t17adv_set_rand_addrE"></a> <a id="bk_ble_gap_cb_param_t::adv_set_rand_addr__bk_ble_gap_cb_param_t::ble_adv_set_rand_addr_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1aa13243fdb0d8c13556b7db58c98268c2"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_set\_rand\_addr\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t36ble_adv_set_rand_addr_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_set_rand_addr_cmpl_evt_param") adv\_set\_rand\_addr
    :   Event parameter of BK\_BLE\_GAP\_EXT\_ADV\_SET\_RAND\_ADDR\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t14adv_params_setE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t14adv_params_setE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t14adv_params_setE"></a> <a id="bk_ble_gap_cb_param_t::adv_params_set__bk_ble_gap_cb_param_t::ble_adv_params_set_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a8e359229facb4d7bb40ccb54daa7aff9"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_params\_set\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_adv_params_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_params_set_cmpl_evt_param") adv\_params\_set
    :   Event parameter of BK\_BLE\_GAP\_EXT\_ADV\_PARAMS\_SET\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t12adv_data_setE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t12adv_data_setE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t12adv_data_setE"></a> <a id="bk_ble_gap_cb_param_t::adv_data_set__bk_ble_gap_cb_param_t::ble_adv_data_set_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1adee99fccd51fc67ef2413324dd29b1c3"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_data\_set\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t31ble_adv_data_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_data_set_cmpl_evt_param") adv\_data\_set
    :   Event parameter of BK\_BLE\_GAP\_EXT\_ADV\_DATA\_SET\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t17scan_rsp_data_setE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t17scan_rsp_data_setE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t17scan_rsp_data_setE"></a> <a id="bk_ble_gap_cb_param_t::scan_rsp_data_set__bk_ble_gap_cb_param_t::ble_adv_scan_rsp_set_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1afb6d73fe0ba40f7b0fd62519372692c6"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_scan\_rsp\_set\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_adv_scan_rsp_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_scan_rsp_set_cmpl_evt_param") scan\_rsp\_data\_set
    :   Event parameter of BK\_BLE\_GAP\_EXT\_SCAN\_RSP\_DATA\_SET\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t16adv_data_raw_setE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t16adv_data_raw_setE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t16adv_data_raw_setE"></a> <a id="bk_ble_gap_cb_param_t::adv_data_raw_set__bk_ble_gap_cb_param_t::ble_adv_data_raw_set_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a5095b05986638af935259a63139e3b78"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_data\_raw\_set\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_adv_data_raw_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_data_raw_set_cmpl_evt_param") adv\_data\_raw\_set
    :   Event parameter of BK\_BLE\_GAP\_EXT\_ADV\_DATA\_SET\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t21scan_rsp_data_raw_setE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t21scan_rsp_data_raw_setE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21scan_rsp_data_raw_setE"></a> <a id="bk_ble_gap_cb_param_t::scan_rsp_data_raw_set__bk_ble_gap_cb_param_t::ble_scan_rsp_data_raw_set_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a2ad3975e94300717db25c8640229b1a7"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_scan\_rsp\_data\_raw\_set\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t40ble_scan_rsp_data_raw_set_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_scan_rsp_data_raw_set_cmpl_evt_param") scan\_rsp\_data\_raw\_set
    :   Event parameter of BK\_BLE\_GAP\_EXT\_SCAN\_RSP\_DATA\_RAW\_SET\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t9adv_startE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t9adv_startE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t9adv_startE"></a> <a id="bk_ble_gap_cb_param_t::adv_start__bk_ble_gap_cb_param_t::ble_adv_start_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1ac2065ead3b47ad9831a3171a5f194f6b"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_start\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t28ble_adv_start_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_start_cmpl_evt_param") adv\_start
    :   Event parameter of BK\_BLE\_GAP\_EXT\_ADV\_START\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t8adv_stopE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t8adv_stopE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t8adv_stopE"></a> <a id="bk_ble_gap_cb_param_t::adv_stop__bk_ble_gap_cb_param_t::ble_adv_stop_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1aab77c705e3312acd6638f4d02117ac6c"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_stop\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_adv_stop_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_stop_cmpl_evt_param") adv\_stop
    :   Event parameter of BK\_BLE\_GAP\_EXT\_ADV\_STOP\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t10adv_removeE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t10adv_removeE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t10adv_removeE"></a> <a id="bk_ble_gap_cb_param_t::adv_remove__bk_ble_gap_cb_param_t::ble_adv_set_remove_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a40480d6f4b7eb9601a56ac1be13207bc"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_set\_remove\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_adv_set_remove_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_set_remove_cmpl_evt_param") adv\_remove
    :   Event parameter of BK\_BLE\_GAP\_ADV\_SET\_REMOVE\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t9adv_clearE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t9adv_clearE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t9adv_clearE"></a> <a id="bk_ble_gap_cb_param_t::adv_clear__bk_ble_gap_cb_param_t::ble_adv_set_clear_cmpl_evt_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a9de198cfac844ab693c2579f83bb231a"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_set\_clear\_cmpl\_evt\_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_adv_set_clear_cmpl_evt_paramE "bk_ble_gap_cb_param_t::ble_adv_set_clear_cmpl_evt_param") adv\_clear
    :   Event parameter of BK\_BLE\_GAP\_ADV\_SET\_CLEAR\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t21peroid_adv_set_paramsE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t21peroid_adv_set_paramsE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21peroid_adv_set_paramsE"></a> <a id="bk_ble_gap_cb_param_t::peroid_adv_set_params__bk_ble_gap_cb_param_t::ble_periodic_adv_set_params_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a6c7f8e39d7b92c2a8565aac5753a41a1"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_periodic\_adv\_set\_params\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t38ble_periodic_adv_set_params_cmpl_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_set_params_cmpl_param") peroid\_adv\_set\_params
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_SET\_PARAMS\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t19period_adv_data_setE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t19period_adv_data_setE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t19period_adv_data_setE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_data_set__bk_ble_gap_cb_param_t::ble_periodic_adv_data_set_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a15a5c1351e954f39c73a00fead358627"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_periodic\_adv\_data\_set\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t36ble_periodic_adv_data_set_cmpl_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_data_set_cmpl_param") period\_adv\_data\_set
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_DATA\_SET\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t16period_adv_startE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t16period_adv_startE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t16period_adv_startE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_start__bk_ble_gap_cb_param_t::ble_periodic_adv_start_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a047a4ceedc2e217c08bd2355f0555fee"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_periodic\_adv\_start\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_start_cmpl_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_start_cmpl_param") period\_adv\_start
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_START\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t15period_adv_stopE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t15period_adv_stopE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t15period_adv_stopE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_stop__bk_ble_gap_cb_param_t::ble_periodic_adv_stop_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1af4b64047f6268e7ba383c2a8bd0ea304"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_periodic\_adv\_stop\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_periodic_adv_stop_cmpl_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_stop_cmpl_param") period\_adv\_stop
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_STOP\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t22period_adv_create_syncE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t22period_adv_create_syncE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t22period_adv_create_syncE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_create_sync__bk_ble_gap_cb_param_t::ble_period_adv_create_sync_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1ac83e754a2437f2bd6f4d976fbbd2e542"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_period\_adv\_create\_sync\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t37ble_period_adv_create_sync_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_create_sync_cmpl_param") period\_adv\_create\_sync
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_CREATE\_SYNC\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t22period_adv_sync_cancelE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t22period_adv_sync_cancelE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t22period_adv_sync_cancelE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_sync_cancel__bk_ble_gap_cb_param_t::ble_period_adv_sync_cancel_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1ace4177e304b7d244ae4c10cca0117366"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_period\_adv\_sync\_cancel\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t37ble_period_adv_sync_cancel_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_sync_cancel_cmpl_param") period\_adv\_sync\_cancel
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_CANCEL\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t20period_adv_sync_termE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t20period_adv_sync_termE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t20period_adv_sync_termE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_sync_term__bk_ble_gap_cb_param_t::ble_period_adv_sync_terminate_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1aa4ab51890f57832978a71bd2af51796f"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_period\_adv\_sync\_terminate\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t40ble_period_adv_sync_terminate_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_sync_terminate_cmpl_param") period\_adv\_sync\_term
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_TERMINATE\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t18period_adv_add_devE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t18period_adv_add_devE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t18period_adv_add_devE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_add_dev__bk_ble_gap_cb_param_t::ble_period_adv_add_dev_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1ab1027b8f99db0e4f67c01a1638320c3c"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_period\_adv\_add\_dev\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_period_adv_add_dev_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_add_dev_cmpl_param") period\_adv\_add\_dev
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_ADD\_DEV\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t21period_adv_remove_devE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t21period_adv_remove_devE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21period_adv_remove_devE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_remove_dev__bk_ble_gap_cb_param_t::ble_period_adv_remove_dev_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a940e085e9174057d2b83efc6dda6762b"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_period\_adv\_remove\_dev\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t36ble_period_adv_remove_dev_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_remove_dev_cmpl_param") period\_adv\_remove\_dev
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_REMOVE\_DEV\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t20period_adv_clear_devE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t20period_adv_clear_devE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t20period_adv_clear_devE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_clear_dev__bk_ble_gap_cb_param_t::ble_period_adv_clear_dev_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1ad59719fba3deccebb03a57d7e899d8de"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_period\_adv\_clear\_dev\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t35ble_period_adv_clear_dev_cmpl_paramE "bk_ble_gap_cb_param_t::ble_period_adv_clear_dev_cmpl_param") period\_adv\_clear\_dev
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_CLEAR\_DEV\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t15scan_params_setE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t15scan_params_setE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t15scan_params_setE"></a> <a id="bk_ble_gap_cb_param_t::scan_params_set__bk_ble_gap_cb_param_t::ble_scan_params_set_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1abd55c1269866b436180c892a2ed9037d"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_scan\_params\_set\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t30ble_scan_params_set_cmpl_paramE "bk_ble_gap_cb_param_t::ble_scan_params_set_cmpl_param") scan\_params\_set
    :   Event parameter of BK\_BLE\_GAP\_SCAN\_PARAMS\_SET\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t10scan_startE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t10scan_startE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t10scan_startE"></a> <a id="bk_ble_gap_cb_param_t::scan_start__bk_ble_gap_cb_param_t::ble_scan_start_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a2b32d6f345f112f0635baaea801052e9"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_scan\_start\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t25ble_scan_start_cmpl_paramE "bk_ble_gap_cb_param_t::ble_scan_start_cmpl_param") scan\_start
    :   Event parameter of BK\_BLE\_GAP\_SCAN\_START\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t9scan_stopE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t9scan_stopE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t9scan_stopE"></a> <a id="bk_ble_gap_cb_param_t::scan_stop__bk_ble_gap_cb_param_t::ble_scan_stop_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a7b632150b5d18f1ef5144d5dfaa7c844"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_scan\_stop\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t24ble_scan_stop_cmpl_paramE "bk_ble_gap_cb_param_t::ble_scan_stop_cmpl_param") scan\_stop
    :   Event parameter of BK\_BLE\_GAP\_SCAN\_STOP\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t15conn_params_setE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t15conn_params_setE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t15conn_params_setE"></a> <a id="bk_ble_gap_cb_param_t::conn_params_set__bk_ble_gap_cb_param_t::ble_conn_params_set_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1aafdcffa3ebbeb76ee4e57c5305a287bc"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_conn\_params\_set\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t30ble_conn_params_set_cmpl_paramE "bk_ble_gap_cb_param_t::ble_conn_params_set_cmpl_param") conn\_params\_set
    :   Event parameter of BK\_BLE\_GAP\_PREFER\_CONN\_PARAMS\_SET\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t13adv_terminateE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t13adv_terminateE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t13adv_terminateE"></a> <a id="bk_ble_gap_cb_param_t::adv_terminate__bk_ble_gap_cb_param_t::ble_adv_terminate_param"></a> <a id="unionbk__ble__gap__cb__param__t_1aba5c1fabe41e726daaee4576e1988845"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_adv\_terminate\_param](#_CPPv4N21bk_ble_gap_cb_param_t23ble_adv_terminate_paramE "bk_ble_gap_cb_param_t::ble_adv_terminate_param") adv\_terminate
    :   Event parameter of BK\_BLE\_GAP\_ADV\_TERMINATED\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t17scan_req_receivedE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t17scan_req_receivedE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t17scan_req_receivedE"></a> <a id="bk_ble_gap_cb_param_t::scan_req_received__bk_ble_gap_cb_param_t::ble_scan_req_received_param"></a> <a id="unionbk__ble__gap__cb__param__t_1aa78b7593b4bbec33d7036d47e27a036c"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_scan\_req\_received\_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_scan_req_received_paramE "bk_ble_gap_cb_param_t::ble_scan_req_received_param") scan\_req\_received
    :   Event parameter of BK\_BLE\_GAP\_SCAN\_REQ\_RECEIVED\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t15channel_sel_algE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t15channel_sel_algE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t15channel_sel_algE"></a> <a id="bk_ble_gap_cb_param_t::channel_sel_alg__bk_ble_gap_cb_param_t::ble_channel_sel_alg_param"></a> <a id="unionbk__ble__gap__cb__param__t_1ae72aa4333edeec4384eb1f36809d3f88"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_channel\_sel\_alg\_param](#_CPPv4N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_paramE "bk_ble_gap_cb_param_t::ble_channel_sel_alg_param") channel\_sel\_alg
    :   Event parameter of BK\_BLE\_GAP\_CHANNEL\_SELECT\_ALGORITHM\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t22periodic_adv_sync_lostE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t22periodic_adv_sync_lostE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t22periodic_adv_sync_lostE"></a> <a id="bk_ble_gap_cb_param_t::periodic_adv_sync_lost__bk_ble_gap_cb_param_t::ble_periodic_adv_sync_lost_param"></a> <a id="unionbk__ble__gap__cb__param__t_1af4283a745d34aae3af05c13addf7cebf"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_periodic\_adv\_sync\_lost\_param](#_CPPv4N21bk_ble_gap_cb_param_t32ble_periodic_adv_sync_lost_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_sync_lost_param") periodic\_adv\_sync\_lost
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_LOST\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t23periodic_adv_sync_estabE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t23periodic_adv_sync_estabE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t23periodic_adv_sync_estabE"></a> <a id="bk_ble_gap_cb_param_t::periodic_adv_sync_estab__bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param"></a> <a id="unionbk__ble__gap__cb__param__t_1afa71f1f067874142bcb424b366cfc419"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_periodic\_adv\_sync\_estab\_param](#_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param") periodic\_adv\_sync\_estab
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_ESTAB\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t10phy_updateE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t10phy_updateE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t10phy_updateE"></a> <a id="bk_ble_gap_cb_param_t::phy_update__bk_ble_gap_cb_param_t::ble_phy_update_cmpl_param"></a> <a id="unionbk__ble__gap__cb__param__t_1abda001643fcc32f5cb43a591b8027acf"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_phy\_update\_cmpl\_param](#_CPPv4N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_paramE "bk_ble_gap_cb_param_t::ble_phy_update_cmpl_param") phy\_update
    :   Event parameter of BK\_BLE\_GAP\_PHY\_UPDATE\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t14ext_adv_reportE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t14ext_adv_reportE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t14ext_adv_reportE"></a> <a id="bk_ble_gap_cb_param_t::ext_adv_report__bk_ble_gap_cb_param_t::ble_ext_adv_report_param"></a> <a id="unionbk__ble__gap__cb__param__t_1abd7379462b398b4cdae183749afaea8b"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_ext\_adv\_report\_param](#_CPPv4N21bk_ble_gap_cb_param_t24ble_ext_adv_report_paramE "bk_ble_gap_cb_param_t::ble_ext_adv_report_param") ext\_adv\_report
    :   Event parameter of BK\_BLE\_GAP\_EXT\_ADV\_REPORT\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t17period_adv_reportE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t17period_adv_reportE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t17period_adv_reportE"></a> <a id="bk_ble_gap_cb_param_t::period_adv_report__bk_ble_gap_cb_param_t::ble_periodic_adv_report_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a00bbcf2b462ed576b58c67a74d209ead"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_periodic\_adv\_report\_param](#_CPPv4N21bk_ble_gap_cb_param_t29ble_periodic_adv_report_paramE "bk_ble_gap_cb_param_t::ble_periodic_adv_report_param") period\_adv\_report
    :   Event parameter of BK\_BLE\_GAP\_PERIODIC\_ADV\_REPORT\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t16connect_completeE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t16connect_completeE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t16connect_completeE"></a> <a id="bk_ble_gap_cb_param_t::connect_complete__bk_ble_gap_cb_param_t::ble_connect_complete_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a32d9ec51e31f947c10117a5fc226b8dc"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_connect\_complete\_param](#_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_paramE "bk_ble_gap_cb_param_t::ble_connect_complete_param") connect\_complete
    :   Event parameter of BK\_BLE\_GAP\_CONNECT\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t19disconnect_completeE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t19disconnect_completeE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t19disconnect_completeE"></a> <a id="bk_ble_gap_cb_param_t::disconnect_complete__bk_ble_gap_cb_param_t::ble_disconnect_complete_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a79f9ada5798d336b66926a1ac42db870"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_disconnect\_complete\_param](#_CPPv4N21bk_ble_gap_cb_param_t29ble_disconnect_complete_paramE "bk_ble_gap_cb_param_t::ble_disconnect_complete_param") disconnect\_complete
    :   Event parameter of BK\_BLE\_GAP\_DISCONNECT\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t14connect_cancelE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t14connect_cancelE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t14connect_cancelE"></a> <a id="bk_ble_gap_cb_param_t::connect_cancel__bk_ble_gap_cb_param_t::ble_connect_cancel_param"></a> <a id="unionbk__ble__gap__cb__param__t_1a9dedfd6f03347eca11ebea388d424c5b"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_connect\_cancel\_param](#_CPPv4N21bk_ble_gap_cb_param_t24ble_connect_cancel_paramE "bk_ble_gap_cb_param_t::ble_connect_cancel_param") connect\_cancel
    :   Event parameter of BK\_BLE\_GAP\_CONNECT\_CANCEL\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t21update_conn_param_reqE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t21update_conn_param_reqE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21update_conn_param_reqE"></a> <a id="bk_ble_gap_cb_param_t::update_conn_param_req__bk_ble_gap_cb_param_t::ble_conntection_update_param_req"></a> <a id="unionbk__ble__gap__cb__param__t_1a4d287cd0e995b937df4a72d9c4572e33"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_conntection\_update\_param\_req](#_CPPv4N21bk_ble_gap_cb_param_t32ble_conntection_update_param_reqE "bk_ble_gap_cb_param_t::ble_conntection_update_param_req") update\_conn\_param\_req
    :   Event parameter of BK\_BLE\_GAP\_UPDATE\_CONN\_PARAMS\_REQ\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t24set_security_params_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t24set_security_params_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t24set_security_params_cmplE"></a> <a id="bk_ble_gap_cb_param_t::set_security_params_cmpl__bk_ble_gap_cb_param_t::ble_set_security_params_cmpl"></a> <a id="unionbk__ble__gap__cb__param__t_1ae141514c6665868e7a3430d7deec1fdb"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_set\_security\_params\_cmpl](#_CPPv4N21bk_ble_gap_cb_param_t28ble_set_security_params_cmplE "bk_ble_gap_cb_param_t::ble_set_security_params_cmpl") set\_security\_params\_cmpl
    :   Event parameter of BK\_BLE\_GAP\_SET\_SECURITY\_PARAMS\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t17generate_rpa_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t17generate_rpa_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t17generate_rpa_cmplE"></a> <a id="bk_ble_gap_cb_param_t::generate_rpa_cmpl__bk_ble_gap_cb_param_t::ble_generate_rpa_cmpl"></a> <a id="unionbk__ble__gap__cb__param__t_1a17ef9b63f173f0e087d84adcc741f04a"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_generate\_rpa\_cmpl](#_CPPv4N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmplE "bk_ble_gap_cb_param_t::ble_generate_rpa_cmpl") generate\_rpa\_cmpl
    :   Event parameter of BK\_BLE\_GAP\_GENERATE\_RPA\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t17encryption_changeE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t17encryption_changeE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t17encryption_changeE"></a> <a id="bk_ble_gap_cb_param_t::encryption_change__bk_ble_gap_cb_param_t::ble_encryption_change_param"></a> <a id="unionbk__ble__gap__cb__param__t_1abf1d9e3caec3d81f9691fd63aebf707f"></a> struct [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t")::[ble\_encryption\_change\_param](#_CPPv4N21bk_ble_gap_cb_param_t27ble_encryption_change_paramE "bk_ble_gap_cb_param_t::ble_encryption_change_param") encryption\_change
    :   Event parameter of BK\_BLE\_GAP\_ENCRYPTION\_CHANGE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_adv_data_raw_set_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_adv_data_raw_set_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_adv_data_raw_set_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_data_raw_set_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__data__raw__set__cmpl__evt__param"></a> struct ble\_adv\_data\_raw\_set\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_ADV\_DATA\_RAW\_SET\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_adv_data_raw_set_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_adv_data_raw_set_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_adv_data_raw_set_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_data_raw_set_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__data__raw__set__cmpl__evt__param_1ae41c7b7236373f4fc27640b7f8b9ac58"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising data set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t31ble_adv_data_set_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t31ble_adv_data_set_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t31ble_adv_data_set_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_data_set_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__data__set__cmpl__evt__param"></a> struct ble\_adv\_data\_set\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_ADV\_DATA\_SET\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t31ble_adv_data_set_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t31ble_adv_data_set_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t31ble_adv_data_set_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_data_set_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__data__set__cmpl__evt__param_1a6396fff32a09c7ac008a11ae54940002"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising data set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_adv_params_set_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_adv_params_set_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_adv_params_set_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_params_set_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__params__set__cmpl__evt__param"></a> struct ble\_adv\_params\_set\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_ADV\_PARAMS\_SET\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_adv_params_set_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_adv_params_set_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_adv_params_set_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_params_set_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__params__set__cmpl__evt__param_1a2c311be6448a2ba71190dd63fae0e18c"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising parameters set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_adv_scan_rsp_set_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_adv_scan_rsp_set_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_adv_scan_rsp_set_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_scan_rsp_set_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__scan__rsp__set__cmpl__evt__param"></a> struct ble\_adv\_scan\_rsp\_set\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_SCAN\_RSP\_DATA\_SET\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_adv_scan_rsp_set_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_adv_scan_rsp_set_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_adv_scan_rsp_set_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_scan_rsp_set_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__scan__rsp__set__cmpl__evt__param_1a8b308de38d152fbd072f614b95b20f43"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising scan response data set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_adv_set_clear_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_adv_set_clear_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_adv_set_clear_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_set_clear_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__set__clear__cmpl__evt__param"></a> struct ble\_adv\_set\_clear\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_ADV\_SET\_CLEAR\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_adv_set_clear_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_adv_set_clear_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_adv_set_clear_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_set_clear_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__set__clear__cmpl__evt__param_1a073a8631e7cc05ff81ed3f80305e78d1"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate advertising stop operation success status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t36ble_adv_set_rand_addr_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t36ble_adv_set_rand_addr_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t36ble_adv_set_rand_addr_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_set_rand_addr_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__set__rand__addr__cmpl__evt__param"></a> struct ble\_adv\_set\_rand\_addr\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_ADV\_SET\_RAND\_ADDR\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t36ble_adv_set_rand_addr_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t36ble_adv_set_rand_addr_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t36ble_adv_set_rand_addr_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_set_rand_addr_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__set__rand__addr__cmpl__evt__param_1a8c233ab6d4a38065e92f88de0758f8d5"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising random address set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_adv_set_remove_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_adv_set_remove_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_adv_set_remove_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_set_remove_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__set__remove__cmpl__evt__param"></a> struct ble\_adv\_set\_remove\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_ADV\_SET\_REMOVE\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_adv_set_remove_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_adv_set_remove_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_adv_set_remove_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_set_remove_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__set__remove__cmpl__evt__param_1a9d8655e53ea1decff3a3ff9d5bb552ac"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate advertising stop operation success status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t28ble_adv_start_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t28ble_adv_start_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t28ble_adv_start_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_start_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__start__cmpl__evt__param"></a> struct ble\_adv\_start\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_ADV\_START\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t28ble_adv_start_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t28ble_adv_start_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t28ble_adv_start_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_start_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__start__cmpl__evt__param_1adee348640ab34995785486a6a6ac205e"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate advertising start operation success status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_adv_stop_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_adv_stop_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_adv_stop_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_stop_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__stop__cmpl__evt__param"></a> struct ble\_adv\_stop\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_ADV\_STOP\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_adv_stop_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_adv_stop_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_adv_stop_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_stop_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__stop__cmpl__evt__param_1afe96212c579c2dda9baa6b7578c18637"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate advertising stop operation success status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t23ble_adv_terminate_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t23ble_adv_terminate_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t23ble_adv_terminate_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_terminate_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__terminate__param"></a> struct ble\_adv\_terminate\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_ADV\_TERMINATED\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t23ble_adv_terminate_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t23ble_adv_terminate_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t23ble_adv_terminate_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_terminate_param::status__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__terminate__param_1a8175603564c99ecfb9127efc8fec4fa2"></a> uint8\_t status
        :   Indicate adv terminate status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t23ble_adv_terminate_param12adv_instanceE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t23ble_adv_terminate_param12adv_instanceE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t23ble_adv_terminate_param12adv_instanceE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_terminate_param::adv_instance__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__terminate__param_1a8866902de597f3519c83eb493ce12e14"></a> uint8\_t adv\_instance
        :   extend advertising handle

        <a id="_CPPv4N21bk_ble_gap_cb_param_t23ble_adv_terminate_param8conn_idxE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t23ble_adv_terminate_param8conn_idxE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t23ble_adv_terminate_param8conn_idxE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_terminate_param::conn_idx__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__terminate__param_1a659473ccb519c7abe01b84765a741cff"></a> uint16\_t conn\_idx
        :   connection index

        <a id="_CPPv4N21bk_ble_gap_cb_param_t23ble_adv_terminate_param15completed_eventE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t23ble_adv_terminate_param15completed_eventE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t23ble_adv_terminate_param15completed_eventE"></a> <a id="bk_ble_gap_cb_param_t::ble_adv_terminate_param::completed_event__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__adv__terminate__param_1a8a9a59082dba9f9f49664d6a123dc37f"></a> uint8\_t completed\_event
        :   the number of completed extend advertising events

    <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_bond_dev_key_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__bond__dev__key__evt__param"></a> struct ble\_bond\_dev\_key\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_BOND\_KEY\_GENERATE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_param8bond_devE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_param8bond_devE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_param8bond_devE"></a> <a id="bk_ble_gap_cb_param_t::ble_bond_dev_key_evt_param::bond_dev__bk_ble_bond_dev_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__bond__dev__key__evt__param_1a38c1c404c16e1b8ad5d8ea66b615ef23"></a> [bk\_ble\_bond\_dev\_t](#_CPPv417bk_ble_bond_dev_t "bk_ble_bond_dev_t") bond\_dev
        :   bond device Structure

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_param9transportE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_param9transportE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_bond_dev_key_evt_param9transportE"></a> <a id="bk_ble_gap_cb_param_t::ble_bond_dev_key_evt_param::transport__bk_ble_key_transport_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__bond__dev__key__evt__param_1ab2c3e34a117836bef2c7c4ea76fd0d08"></a> [bk\_ble\_key\_transport\_t](#_CPPv422bk_ble_key_transport_t "bk_ble_key_transport_t") transport
        :   Originating transport of the key-generation procedure

    <a id="_CPPv4N21bk_ble_gap_cb_param_t30ble_bond_dev_key_req_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t30ble_bond_dev_key_req_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t30ble_bond_dev_key_req_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_bond_dev_key_req_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__bond__dev__key__req__evt__param"></a> struct ble\_bond\_dev\_key\_req\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_BOND\_KEY\_REQ\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t30ble_bond_dev_key_req_evt_param7key_reqE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t30ble_bond_dev_key_req_evt_param7key_reqE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t30ble_bond_dev_key_req_evt_param7key_reqE"></a> <a id="bk_ble_gap_cb_param_t::ble_bond_dev_key_req_evt_param::key_req__bk_ble_bond_key_req_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__bond__dev__key__req__evt__param_1a928f768424c46dad41063d1a091ee8b1"></a> [bk\_ble\_bond\_key\_req\_t](#_CPPv421bk_ble_bond_key_req_t "bk_ble_bond_key_req_t") key\_req
        :   bond device Structure

    <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_bond_dev_list_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__bond__dev__list__evt__param"></a> struct ble\_bond\_dev\_list\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_BOND\_DEV\_LIST\_OPERATEION\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_bond_dev_list_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__bond__dev__list__evt__param_1aad9c14419f0634e7a7e78396b92b49f8"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_param2opE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_param2opE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_bond_dev_list_evt_param2opE"></a> <a id="bk_ble_gap_cb_param_t::ble_bond_dev_list_evt_param::op__bk_gap_bond_dev_list_operation_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__bond__dev__list__evt__param_1a2a770cd664cb96a1b50065b64063e311"></a> [bk\_gap\_bond\_dev\_list\_operation\_t](#_CPPv432bk_gap_bond_dev_list_operation_t "bk_gap_bond_dev_list_operation_t") op
        :   operation id

    <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_channel_sel_alg_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__channel__sel__alg__param"></a> struct ble\_channel\_sel\_alg\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_CHANNEL\_SELECT\_ALGORITHM\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_param11conn_handleE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_param11conn_handleE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_param11conn_handleE"></a> <a id="bk_ble_gap_cb_param_t::ble_channel_sel_alg_param::conn_handle__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__channel__sel__alg__param_1a6cfacabcb0e9b7bc33eb899aff84dbdd"></a> uint16\_t conn\_handle
        :   connection handle

        <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_param15channel_sel_algE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_param15channel_sel_algE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_channel_sel_alg_param15channel_sel_algE"></a> <a id="bk_ble_gap_cb_param_t::ble_channel_sel_alg_param::channel_sel_alg__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__channel__sel__alg__param_1a3df1d22cfb6b56a9f629b643c86a7d43"></a> uint8\_t channel\_sel\_alg
        :   channel selection algorithm

    <a id="_CPPv4N21bk_ble_gap_cb_param_t30ble_conn_params_set_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t30ble_conn_params_set_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t30ble_conn_params_set_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_conn_params_set_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__conn__params__set__cmpl__param"></a> struct ble\_conn\_params\_set\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PREFER\_CONN\_PARAMS\_SET\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t30ble_conn_params_set_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t30ble_conn_params_set_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t30ble_conn_params_set_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_conn_params_set_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__conn__params__set__cmpl__param_1a576885059f1f01a4249740635ed198b6"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend connection parameters set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t24ble_connect_cancel_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t24ble_connect_cancel_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t24ble_connect_cancel_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_cancel_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__cancel__param"></a> struct ble\_connect\_cancel\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_CONNECT\_CANCEL\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t24ble_connect_cancel_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t24ble_connect_cancel_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t24ble_connect_cancel_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_cancel_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__cancel__param_1a230e19d7c68993d37127269669e40c85"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_connect_complete_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_connect_complete_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_complete_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__complete__param"></a> struct ble\_connect\_complete\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_CONNECT\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_connect_complete_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_connect_complete_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_complete_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__complete__param_1a3dcb0cef4e0eeeb2608c8bc3bb9bfde9"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_param10remote_bdaE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_connect_complete_param10remote_bdaE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_connect_complete_param10remote_bdaE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_complete_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__complete__param_1a7c4fb49bef4d2f9dfa6fd1e097bcfe03"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_param15remote_bda_typeE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_connect_complete_param15remote_bda_typeE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_connect_complete_param15remote_bda_typeE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_complete_param::remote_bda_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__complete__param_1aed0c81e48d97efe8e1f8cbe7e696eeeb"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") remote\_bda\_type

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_param9link_roleE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_connect_complete_param9link_roleE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_connect_complete_param9link_roleE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_complete_param::link_role__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__complete__param_1ad580156cd71e50ea8a7b6b6450f04ac7"></a> uint8\_t link\_role
        :   Link role : master role \= 0 ; slave role \= 1

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_param9conn_intvE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_connect_complete_param9conn_intvE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_connect_complete_param9conn_intvE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_complete_param::conn_intv__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__complete__param_1a055c8515ec964268d403682cc99f265a"></a> uint16\_t conn\_intv

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_param12conn_latencyE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_connect_complete_param12conn_latencyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_connect_complete_param12conn_latencyE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_complete_param::conn_latency__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__complete__param_1acd5f4b406e1ce8ac23313e3e8fb85300"></a> uint16\_t conn\_latency

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_param19supervision_timeoutE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_connect_complete_param19supervision_timeoutE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_connect_complete_param19supervision_timeoutE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_complete_param::supervision_timeout__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__complete__param_1a8d458d7fc93623554e422da4b2eea9f7"></a> uint16\_t supervision\_timeout

        <a id="_CPPv4N21bk_ble_gap_cb_param_t26ble_connect_complete_param10hci_handleE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t26ble_connect_complete_param10hci_handleE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t26ble_connect_complete_param10hci_handleE"></a> <a id="bk_ble_gap_cb_param_t::ble_connect_complete_param::hci_handle__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__connect__complete__param_1adae809ddab26b7832d3b744cf83c09eb"></a> uint16\_t hci\_handle

    <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_conntection_update_param_reqE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_conntection_update_param_reqE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_conntection_update_param_reqE"></a> <a id="bk_ble_gap_cb_param_t::ble_conntection_update_param_req"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__conntection__update__param__req"></a> struct ble\_conntection\_update\_param\_req
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_UPDATE\_CONN\_PARAMS\_REQ\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_conntection_update_param_req10can_modifyE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_conntection_update_param_req10can_modifyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_conntection_update_param_req10can_modifyE"></a> <a id="bk_ble_gap_cb_param_t::ble_conntection_update_param_req::can_modify__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__conntection__update__param__req_1a5e58a23f4b9a1d82a3f14518de5ffddf"></a> uint8\_t can\_modify
        :   if true, param can be modify before accept

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_conntection_update_param_req5paramE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_conntection_update_param_req5paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_conntection_update_param_req5paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_conntection_update_param_req::param__bk_ble_conn_update_params_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__conntection__update__param__req_1a09c21a41c4f8ea18cfe45a0d3b72aa91"></a> [bk\_ble\_conn\_update\_params\_t](#_CPPv427bk_ble_conn_update_params_t "bk_ble_conn_update_params_t") param

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_conntection_update_param_req6acceptE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_conntection_update_param_req6acceptE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_conntection_update_param_req6acceptE"></a> <a id="bk_ble_gap_cb_param_t::ble_conntection_update_param_req::accept__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__conntection__update__param__req_1aeb7a7087b7c85cfdcf4897c0d7b24442"></a> uint8\_t accept

    <a id="_CPPv4N21bk_ble_gap_cb_param_t29ble_disconnect_complete_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t29ble_disconnect_complete_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t29ble_disconnect_complete_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_disconnect_complete_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__disconnect__complete__param"></a> struct ble\_disconnect\_complete\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_DISCONNECT\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_disconnect_complete_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__disconnect__complete__param_1a643d3e9fa235846771495a01a16b9de8"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param10remote_bdaE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param10remote_bdaE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param10remote_bdaE"></a> <a id="bk_ble_gap_cb_param_t::ble_disconnect_complete_param::remote_bda__bk_bd_addr_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__disconnect__complete__param_1ad5ba997b125f4dc72ad904d4761850cd"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda
        :   Remote bluetooth device address

        <a id="_CPPv4N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param15remote_bda_typeE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param15remote_bda_typeE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param15remote_bda_typeE"></a> <a id="bk_ble_gap_cb_param_t::ble_disconnect_complete_param::remote_bda_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__disconnect__complete__param_1aaeaffb125b4bb3c1a6872fc3d07d49c3"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") remote\_bda\_type

        <a id="_CPPv4N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param6reasonE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param6reasonE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param6reasonE"></a> <a id="bk_ble_gap_cb_param_t::ble_disconnect_complete_param::reason__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__disconnect__complete__param_1a0c3ca54e8f3df54ef6f3fdbb578f2c22"></a> uint8\_t reason

        <a id="_CPPv4N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param10hci_handleE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param10hci_handleE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t29ble_disconnect_complete_param10hci_handleE"></a> <a id="bk_ble_gap_cb_param_t::ble_disconnect_complete_param::hci_handle__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__disconnect__complete__param_1a99278024c8514a00b9fed95a3695941f"></a> uint16\_t hci\_handle

    <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_encryption_change_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_encryption_change_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_encryption_change_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_encryption_change_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__encryption__change__param"></a> struct ble\_encryption\_change\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_ENCRYPTION\_CHANGE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_encryption_change_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_encryption_change_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_encryption_change_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_encryption_change_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__encryption__change__param_1a3c09643f8b3cad00c5b20fa62adcb4e6"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_encryption_change_param11conn_handleE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_encryption_change_param11conn_handleE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_encryption_change_param11conn_handleE"></a> <a id="bk_ble_gap_cb_param_t::ble_encryption_change_param::conn_handle__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__encryption__change__param_1a0bf80ba381471d8e63f9529b2b85733d"></a> uint16\_t conn\_handle

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_encryption_change_param9encryptedE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_encryption_change_param9encryptedE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_encryption_change_param9encryptedE"></a> <a id="bk_ble_gap_cb_param_t::ble_encryption_change_param::encrypted__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__encryption__change__param_1ab2287b130ee1f16fcf6aa02df665ab1c"></a> uint8\_t encrypted

    <a id="_CPPv4N21bk_ble_gap_cb_param_t24ble_ext_adv_report_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t24ble_ext_adv_report_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t24ble_ext_adv_report_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_ext_adv_report_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__ext__adv__report__param"></a> struct ble\_ext\_adv\_report\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_ADV\_REPORT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t24ble_ext_adv_report_param6paramsE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t24ble_ext_adv_report_param6paramsE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t24ble_ext_adv_report_param6paramsE"></a> <a id="bk_ble_gap_cb_param_t::ble_ext_adv_report_param::params__bk_ble_gap_ext_adv_reprot_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__ext__adv__report__param_1aa60aec5539b5ed459c1a902186f37f72"></a> [bk\_ble\_gap\_ext\_adv\_reprot\_t](#_CPPv427bk_ble_gap_ext_adv_reprot_t "bk_ble_gap_ext_adv_reprot_t") params
        :   extend advertising report parameters

    <a id="_CPPv4N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmplE"></a> <a id="bk_ble_gap_cb_param_t::ble_generate_rpa_cmpl"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__generate__rpa__cmpl"></a> struct ble\_generate\_rpa\_cmpl
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_GENERATE\_RPA\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmpl6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmpl6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmpl6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_generate_rpa_cmpl::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__generate__rpa__cmpl_1accf1c14831d85bfdd2769cfba286a200"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmpl4addrE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmpl4addrE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmpl4addrE"></a> <a id="bk_ble_gap_cb_param_t::ble_generate_rpa_cmpl::addr__bk_bd_addr_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__generate__rpa__cmpl_1ae801cd94d74348928787e367f13b36b4"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr

        <a id="_CPPv4N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmpl9addr_typeE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmpl9addr_typeE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t21ble_generate_rpa_cmpl9addr_typeE"></a> <a id="bk_ble_gap_cb_param_t::ble_generate_rpa_cmpl::addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__generate__rpa__cmpl_1a54550a3ad805ad8e17a2cb12c074d019"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr\_type

    <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_local_privacy_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_local_privacy_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_local_privacy_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_local_privacy_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__local__privacy__cmpl__evt__param"></a> struct ble\_local\_privacy\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SET\_LOCAL\_PRIVACY\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_local_privacy_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_local_privacy_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_local_privacy_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_local_privacy_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__local__privacy__cmpl__evt__param_1a1a820342e2fd459ba8dad4c81b371bd3"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the set local privacy operation success status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_period_adv_add_dev_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_period_adv_add_dev_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_period_adv_add_dev_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_add_dev_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__add__dev__cmpl__param"></a> struct ble\_period\_adv\_add\_dev\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_ADD\_DEV\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_period_adv_add_dev_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_period_adv_add_dev_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_period_adv_add_dev_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_add_dev_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__add__dev__cmpl__param_1ac78a6c80774ca1c532fd06c483b43673"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising device list add status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_period_adv_clear_dev_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_period_adv_clear_dev_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_period_adv_clear_dev_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_clear_dev_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__clear__dev__cmpl__param"></a> struct ble\_period\_adv\_clear\_dev\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_CLEAR\_DEV\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_period_adv_clear_dev_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_period_adv_clear_dev_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_period_adv_clear_dev_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_clear_dev_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__clear__dev__cmpl__param_1af3181b6b98841572d0663639f885eea3"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising device list clean status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t37ble_period_adv_create_sync_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t37ble_period_adv_create_sync_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t37ble_period_adv_create_sync_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_create_sync_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__create__sync__cmpl__param"></a> struct ble\_period\_adv\_create\_sync\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_CREATE\_SYNC\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t37ble_period_adv_create_sync_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t37ble_period_adv_create_sync_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t37ble_period_adv_create_sync_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_create_sync_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__create__sync__cmpl__param_1a1628f878d6a6d9c4d6ce2fa22a59d8ad"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising create sync status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t36ble_period_adv_remove_dev_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t36ble_period_adv_remove_dev_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t36ble_period_adv_remove_dev_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_remove_dev_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__remove__dev__cmpl__param"></a> struct ble\_period\_adv\_remove\_dev\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_REMOVE\_DEV\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t36ble_period_adv_remove_dev_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t36ble_period_adv_remove_dev_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t36ble_period_adv_remove_dev_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_remove_dev_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__remove__dev__cmpl__param_1a6a7ff0a0019cea89ffe1053a9e4f7fe4"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising device list remove status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t37ble_period_adv_sync_cancel_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t37ble_period_adv_sync_cancel_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t37ble_period_adv_sync_cancel_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_sync_cancel_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__sync__cancel__cmpl__param"></a> struct ble\_period\_adv\_sync\_cancel\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_CANCEL\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t37ble_period_adv_sync_cancel_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t37ble_period_adv_sync_cancel_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t37ble_period_adv_sync_cancel_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_sync_cancel_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__sync__cancel__cmpl__param_1ad030c4625a71daf46c7be01dbfc5cca9"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising sync cancel status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t40ble_period_adv_sync_terminate_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t40ble_period_adv_sync_terminate_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t40ble_period_adv_sync_terminate_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_sync_terminate_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__sync__terminate__cmpl__param"></a> struct ble\_period\_adv\_sync\_terminate\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_TERMINATE\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t40ble_period_adv_sync_terminate_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t40ble_period_adv_sync_terminate_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t40ble_period_adv_sync_terminate_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_period_adv_sync_terminate_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__period__adv__sync__terminate__cmpl__param_1aa7b63ada8e5daeb02479ac19f5b998a6"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising sync terminate status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t36ble_periodic_adv_data_set_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t36ble_periodic_adv_data_set_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t36ble_periodic_adv_data_set_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_data_set_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__data__set__cmpl__param"></a> struct ble\_periodic\_adv\_data\_set\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_DATA\_SET\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t36ble_periodic_adv_data_set_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t36ble_periodic_adv_data_set_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t36ble_periodic_adv_data_set_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_data_set_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__data__set__cmpl__param_1a58655ad9f8cb264bb95c051535982f5b"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising data set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t29ble_periodic_adv_report_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t29ble_periodic_adv_report_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t29ble_periodic_adv_report_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_report_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__report__param"></a> struct ble\_periodic\_adv\_report\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_REPORT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t29ble_periodic_adv_report_param6paramsE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t29ble_periodic_adv_report_param6paramsE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t29ble_periodic_adv_report_param6paramsE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_report_param::params__bk_ble_gap_periodic_adv_report_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__report__param_1a8722cd89e780e203970b1e6871a47525"></a> [bk\_ble\_gap\_periodic\_adv\_report\_t](#_CPPv432bk_ble_gap_periodic_adv_report_t "bk_ble_gap_periodic_adv_report_t") params
        :   periodic advertising report parameters

    <a id="_CPPv4N21bk_ble_gap_cb_param_t38ble_periodic_adv_set_params_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t38ble_periodic_adv_set_params_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t38ble_periodic_adv_set_params_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_set_params_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__set__params__cmpl__param"></a> struct ble\_periodic\_adv\_set\_params\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_SET\_PARAMS\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t38ble_periodic_adv_set_params_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t38ble_periodic_adv_set_params_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t38ble_periodic_adv_set_params_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_set_params_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__set__params__cmpl__param_1af3edd053b86038e568364d7b03a90e1d"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertisingparameters set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_start_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_start_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_start_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_start_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__start__cmpl__param"></a> struct ble\_periodic\_adv\_start\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_START\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_start_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_start_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_start_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_start_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__start__cmpl__param_1a6b933f8a2bdb6a122321a8dc5b7f4209"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising start status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_periodic_adv_stop_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_periodic_adv_stop_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_periodic_adv_stop_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_stop_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__stop__cmpl__param"></a> struct ble\_periodic\_adv\_stop\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_STOP\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_periodic_adv_stop_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_periodic_adv_stop_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_periodic_adv_stop_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_stop_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__stop__cmpl__param_1a370d27d9caf024c7128eda204df8834e"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate periodic advertising stop status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__estab__param"></a> struct ble\_periodic\_adv\_sync\_estab\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_ESTAB\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param::status__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__estab__param_1ac6bcb301dd5d525bc45e55094c55ed95"></a> uint8\_t status
        :   periodic advertising sync status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param11sync_handleE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param11sync_handleE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param11sync_handleE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param::sync_handle__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__estab__param_1a1829db87a651c01b906923419ae7f336"></a> uint16\_t sync\_handle
        :   periodic advertising sync handle

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param3sidE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param3sidE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param3sidE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param::sid__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__estab__param_1a3db3e1276c240123174d96ccd7ef70a1"></a> uint8\_t sid
        :   periodic advertising sid

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param13adv_addr_typeE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param13adv_addr_typeE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param13adv_addr_typeE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param::adv_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__estab__param_1a5095f2c92651b0ca8e2a27b75e3283a8"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") adv\_addr\_type
        :   periodic advertising address type

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param8adv_addrE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param8adv_addrE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param8adv_addrE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param::adv_addr__bk_bd_addr_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__estab__param_1a0fa21b6f63fb9f9612b7e90b3c12a262"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") adv\_addr
        :   periodic advertising address

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param7adv_phyE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param7adv_phyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param7adv_phyE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param::adv_phy__bk_ble_gap_phy_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__estab__param_1ad23d8d73f98abba45e4a89aa83d746c9"></a> [bk\_ble\_gap\_phy\_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") adv\_phy
        :   periodic advertising phy type

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param19period_adv_intervalE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param19period_adv_intervalE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param19period_adv_intervalE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param::period_adv_interval__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__estab__param_1a3cbf9d7d5f32062250f793e3e6a42986"></a> uint16\_t period\_adv\_interval
        :   periodic advertising interval

        <a id="_CPPv4N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param16adv_clk_accuracyE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param16adv_clk_accuracyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t33ble_periodic_adv_sync_estab_param16adv_clk_accuracyE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_estab_param::adv_clk_accuracy__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__estab__param_1aefea014e9e02b3eea92ea40373616997"></a> uint8\_t adv\_clk\_accuracy
        :   periodic advertising clock accuracy

    <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_periodic_adv_sync_lost_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_periodic_adv_sync_lost_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_periodic_adv_sync_lost_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_lost_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__lost__param"></a> struct ble\_periodic\_adv\_sync\_lost\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_LOST\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_periodic_adv_sync_lost_param11sync_handleE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_periodic_adv_sync_lost_param11sync_handleE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_periodic_adv_sync_lost_param11sync_handleE"></a> <a id="bk_ble_gap_cb_param_t::ble_periodic_adv_sync_lost_param::sync_handle__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__periodic__adv__sync__lost__param_1a2f52531eb85ffc286d74262b620a952a"></a> uint16\_t sync\_handle
        :   sync handle

    <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_phy_update_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__phy__update__cmpl__param"></a> struct ble\_phy\_update\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_PHY\_UPDATE\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_phy_update_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__phy__update__cmpl__param_1a7e619c8164c8ab79f3b64dfc02608d39"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   phy update status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param3bdaE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param3bdaE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param3bdaE"></a> <a id="bk_ble_gap_cb_param_t::ble_phy_update_cmpl_param::bda__bk_bd_addr_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__phy__update__cmpl__param_1a4d6c6b3e2304e1c4e2b34feba6d47311"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   address

        <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param6tx_phyE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param6tx_phyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param6tx_phyE"></a> <a id="bk_ble_gap_cb_param_t::ble_phy_update_cmpl_param::tx_phy__bk_ble_gap_phy_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__phy__update__cmpl__param_1ae7419011a135730a5865e63d5794ecc9"></a> [bk\_ble\_gap\_phy\_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") tx\_phy
        :   tx phy type

        <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param6rx_phyE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param6rx_phyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_phy_update_cmpl_param6rx_phyE"></a> <a id="bk_ble_gap_cb_param_t::ble_phy_update_cmpl_param::rx_phy__bk_ble_gap_phy_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__phy__update__cmpl__param_1a601f2b2beaf27a6b1fc7ba33e0079fec"></a> [bk\_ble\_gap\_phy\_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") rx\_phy
        :   rx phy type

    <a id="_CPPv4N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_pkt_data_length_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__pkt__data__length__cmpl__evt__param"></a> struct ble\_pkt\_data\_length\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SET\_PKT\_LENGTH\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_pkt_data_length_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__pkt__data__length__cmpl__evt__param_1a872db95c48e2c9103f3a12616cbf8b36"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the set pkt data length operation success status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_param6paramsE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_param6paramsE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t34ble_pkt_data_length_cmpl_evt_param6paramsE"></a> <a id="bk_ble_gap_cb_param_t::ble_pkt_data_length_cmpl_evt_param::params__bk_ble_pkt_data_length_params_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__pkt__data__length__cmpl__evt__param_1a90d981ff3fa34b17fc30835521bafa83"></a> [bk\_ble\_pkt\_data\_length\_params\_t](#_CPPv431bk_ble_pkt_data_length_params_t "bk_ble_pkt_data_length_params_t") params
        :   pkt data length value

    <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_read_phy_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__read__phy__cmpl__evt__param"></a> struct ble\_read\_phy\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_READ\_PHY\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_read_phy_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__read__phy__cmpl__evt__param_1adc8592f6bb677553bdf12cb4f874bfc9"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   read phy complete status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param3bdaE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param3bdaE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param3bdaE"></a> <a id="bk_ble_gap_cb_param_t::ble_read_phy_cmpl_evt_param::bda__bk_bd_addr_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__read__phy__cmpl__evt__param_1a0c8d1480dd14cc00fab00a84d7ff7d47"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   read phy address

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param6tx_phyE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param6tx_phyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param6tx_phyE"></a> <a id="bk_ble_gap_cb_param_t::ble_read_phy_cmpl_evt_param::tx_phy__bk_ble_gap_phy_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__read__phy__cmpl__evt__param_1a45e416d41b9064281972effbd7875172"></a> [bk\_ble\_gap\_phy\_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") tx\_phy
        :   tx phy type

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param6rx_phyE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param6rx_phyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_read_phy_cmpl_evt_param6rx_phyE"></a> <a id="bk_ble_gap_cb_param_t::ble_read_phy_cmpl_evt_param::rx_phy__bk_ble_gap_phy_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__read__phy__cmpl__evt__param_1aa01942f536fe275726278216a03f8ae3"></a> [bk\_ble\_gap\_phy\_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") rx\_phy
        :   rx phy type

    <a id="_CPPv4N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_read_rssi_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__read__rssi__cmpl__evt__param"></a> struct ble\_read\_rssi\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_READ\_RSSI\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_read_rssi_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__read__rssi__cmpl__evt__param_1a539ec64048fb2ab2498d4a4e57489527"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the read adv tx power operation success status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_param4rssiE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_param4rssiE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_param4rssiE"></a> <a id="bk_ble_gap_cb_param_t::ble_read_rssi_cmpl_evt_param::rssi__int8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__read__rssi__cmpl__evt__param_1a7dc6ba441c44236f3fa67aa0c0705d62"></a> int8\_t rssi
        :   The ble remote device rssi value, the range is from -127 to 20, the unit is dbm, if the RSSI cannot be read, the RSSI metric shall be set to 127\.

        <a id="_CPPv4N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_param11remote_addrE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_param11remote_addrE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t28ble_read_rssi_cmpl_evt_param11remote_addrE"></a> <a id="bk_ble_gap_cb_param_t::ble_read_rssi_cmpl_evt_param::remote_addr__bk_bd_addr_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__read__rssi__cmpl__evt__param_1af6d7ee628893f58b6a543745f03aed4d"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_addr
        :   The remote device address

    <a id="_CPPv4N21bk_ble_gap_cb_param_t30ble_scan_params_set_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t30ble_scan_params_set_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t30ble_scan_params_set_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_params_set_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__params__set__cmpl__param"></a> struct ble\_scan\_params\_set\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SCAN\_PARAMS\_SET\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t30ble_scan_params_set_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t30ble_scan_params_set_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t30ble_scan_params_set_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_params_set_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__params__set__cmpl__param_1a0c156a1d90cacdb798ae89a7349e23bd"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising parameters set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_scan_req_received_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_scan_req_received_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_scan_req_received_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_req_received_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__req__received__param"></a> struct ble\_scan\_req\_received\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SCAN\_REQ\_RECEIVED\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_scan_req_received_param12adv_instanceE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_scan_req_received_param12adv_instanceE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_scan_req_received_param12adv_instanceE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_req_received_param::adv_instance__uint8_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__req__received__param_1ad447b5e114e0ca035359b3a149c6f18c"></a> uint8\_t adv\_instance
        :   extend advertising handle

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_scan_req_received_param14scan_addr_typeE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_scan_req_received_param14scan_addr_typeE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_scan_req_received_param14scan_addr_typeE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_req_received_param::scan_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__req__received__param_1a6bf2babe85a7a6f4ddf4ae3302cb130d"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") scan\_addr\_type
        :   scanner address type

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_scan_req_received_param9scan_addrE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_scan_req_received_param9scan_addrE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_scan_req_received_param9scan_addrE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_req_received_param::scan_addr__bk_bd_addr_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__req__received__param_1ad741737258d8373b86aeae792e544892"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") scan\_addr
        :   scanner address

    <a id="_CPPv4N21bk_ble_gap_cb_param_t40ble_scan_rsp_data_raw_set_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t40ble_scan_rsp_data_raw_set_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t40ble_scan_rsp_data_raw_set_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_rsp_data_raw_set_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__rsp__data__raw__set__cmpl__evt__param"></a> struct ble\_scan\_rsp\_data\_raw\_set\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_EXT\_SCAN\_RSP\_DATA\_RAW\_SET\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t40ble_scan_rsp_data_raw_set_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t40ble_scan_rsp_data_raw_set_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t40ble_scan_rsp_data_raw_set_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_rsp_data_raw_set_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__rsp__data__raw__set__cmpl__evt__param_1a6511721802c113c6fdab9dd9682796a2"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising scan response data set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_scan_start_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_scan_start_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_scan_start_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_start_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__start__cmpl__param"></a> struct ble\_scan\_start\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SCAN\_START\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t25ble_scan_start_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t25ble_scan_start_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t25ble_scan_start_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_start_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__start__cmpl__param_1aae9745110e5dd04982102616ac014281"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising start status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t24ble_scan_stop_cmpl_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t24ble_scan_stop_cmpl_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t24ble_scan_stop_cmpl_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_stop_cmpl_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__stop__cmpl__param"></a> struct ble\_scan\_stop\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SCAN\_STOP\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t24ble_scan_stop_cmpl_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t24ble_scan_stop_cmpl_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t24ble_scan_stop_cmpl_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_scan_stop_cmpl_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__scan__stop__cmpl__param_1a9561c22dc039bef369295b097ccd525d"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate extend advertising stop status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t31ble_set_channels_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t31ble_set_channels_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t31ble_set_channels_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_channels_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__channels__cmpl__evt__param"></a> struct ble\_set\_channels\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SET\_CHANNELS\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t31ble_set_channels_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t31ble_set_channels_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t31ble_set_channels_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_channels_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__channels__cmpl__evt__param_1ae8b420bfa1e9c21939925ed3b3a6c7db"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   BLE set channel status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_set_perf_def_phy_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_set_perf_def_phy_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_set_perf_def_phy_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_perf_def_phy_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__perf__def__phy__cmpl__evt__param"></a> struct ble\_set\_perf\_def\_phy\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SET\_PREFERRED\_DEFAULT\_PHY\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_set_perf_def_phy_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_set_perf_def_phy_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_set_perf_def_phy_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_perf_def_phy_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__perf__def__phy__cmpl__evt__param_1ac3a6ec8bd0c98fbbf81a5bb8e67840be"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate perf default phy set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t31ble_set_perf_phy_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t31ble_set_perf_phy_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t31ble_set_perf_phy_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_perf_phy_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__perf__phy__cmpl__evt__param"></a> struct ble\_set\_perf\_phy\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SET\_PREFERRED\_PHY\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t31ble_set_perf_phy_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t31ble_set_perf_phy_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t31ble_set_perf_phy_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_perf_phy_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__perf__phy__cmpl__evt__param_1a1ccd56cfc374eaf41b535bdaaf9ae80b"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate perf phy set status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_set_rand_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_set_rand_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_set_rand_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_rand_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__rand__cmpl__evt__param"></a> struct ble\_set\_rand\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SET\_STATIC\_RAND\_ADDR\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t27ble_set_rand_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t27ble_set_rand_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t27ble_set_rand_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_rand_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__rand__cmpl__evt__param_1ad01bdfaa9d9cfffabe548a581b324271"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate set static rand address operation success status

    <a id="_CPPv4N21bk_ble_gap_cb_param_t28ble_set_security_params_cmplE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t28ble_set_security_params_cmplE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t28ble_set_security_params_cmplE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_security_params_cmpl"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__security__params__cmpl"></a> struct ble\_set\_security\_params\_cmpl
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_SET\_SECURITY\_PARAMS\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t28ble_set_security_params_cmpl6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t28ble_set_security_params_cmpl6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t28ble_set_security_params_cmpl6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_security_params_cmpl::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__security__params__cmpl_1a20ec5ee564454ef9b9db886a8d72f23b"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t28ble_set_security_params_cmpl5paramE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t28ble_set_security_params_cmpl5paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t28ble_set_security_params_cmpl5paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_set_security_params_cmpl::param__bk_ble_sm_param_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__set__security__params__cmpl_1a75d05708c2a4b6517fc6087c5549e748"></a> [bk\_ble\_sm\_param\_t](#_CPPv417bk_ble_sm_param_t "bk_ble_sm_param_t") param

    <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__conn__params__evt__param"></a> struct ble\_update\_conn\_params\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_UPDATE\_CONN\_PARAMS\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__conn__params__evt__param_1a64cb4469c27e242121f95b3d11d253f1"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate update connection parameters success status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param3bdaE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param3bdaE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param3bdaE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param::bda__bk_bd_addr_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__conn__params__evt__param_1a5285ef994283b5fd34c8699e59e648ba"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   Bluetooth device address

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7min_intE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7min_intE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7min_intE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param::min_int__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__conn__params__evt__param_1aec1505d2924d0d00a00d002c1f534acd"></a> uint16\_t min\_int
        :   Min connection interval

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7max_intE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7max_intE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7max_intE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param::max_int__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__conn__params__evt__param_1a85fc4b239b57ca42d7d02144bd03542b"></a> uint16\_t max\_int
        :   Max connection interval

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7latencyE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7latencyE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7latencyE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param::latency__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__conn__params__evt__param_1a99031d35ac41fbb79d25ccc0222642bd"></a> uint16\_t latency
        :   Slave latency for the connection in number of connection events. Range: 0x0000 to 0x01F3

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param8conn_intE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param8conn_intE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param8conn_intE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param::conn_int__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__conn__params__evt__param_1a0d346c8696c09b7542c3ac8745f35234"></a> uint16\_t conn\_int
        :   Current connection interval

        <a id="_CPPv4N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7timeoutE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7timeoutE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t32ble_update_conn_params_evt_param7timeoutE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_conn_params_evt_param::timeout__uint16_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__conn__params__evt__param_1a03e91d8fa3c123dd2f2169425c935460"></a> uint16\_t timeout
        :   Supervision timeout for the LE Link. Range: 0x000A to 0x0C80. Mandatory Range: 0x000A to 0x0C80 Time \= N \* 10 msec

    <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_paramE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_paramE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_paramE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_whitelist_cmpl_evt_param"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__whitelist__cmpl__evt__param"></a> struct ble\_update\_whitelist\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_ble\_types.h\>*

        BK\_BLE\_GAP\_UPDATE\_WHITELIST\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_param6statusE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_param6statusE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_whitelist_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__whitelist__cmpl__evt__param_1a4dbb4e463f980f3065f219aba54a7794"></a> [bk\_bt\_status\_t](#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the add or remove whitelist operation success status

        <a id="_CPPv4N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_param12wl_operationE"></a>

        <a id="_CPPv3N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_param12wl_operationE"></a> <a id="_CPPv2N21bk_ble_gap_cb_param_t35ble_update_whitelist_cmpl_evt_param12wl_operationE"></a> <a id="bk_ble_gap_cb_param_t::ble_update_whitelist_cmpl_evt_param::wl_operation__bk_ble_wl_operation_t"></a> <a id="structbk__ble__gap__cb__param__t_1_1ble__update__whitelist__cmpl__evt__param_1a31f4763963c2a16b4e641e7a1a3cd090"></a> [bk\_ble\_wl\_operation\_t](#_CPPv421bk_ble_wl_operation_t "bk_ble_wl_operation_t") wl\_operation
        :   The value is BK\_BLE\_WHITELIST\_ADD if add address to whitelist operation success, BK\_BLE\_WHITELIST\_REMOVE if remove address from the whitelist operation success

<a id="structures"></a>

### Structures

<a id="_CPPv419bk_ble_adv_params_t"></a>

<a id="_CPPv319bk_ble_adv_params_t"></a> <a id="_CPPv219bk_ble_adv_params_t"></a> <a id="bk_ble_adv_params_t"></a> <a id="structbk__ble__adv__params__t"></a> struct bk\_ble\_adv\_params\_t
:   Advertising parameters.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_ble_adv_params_t11adv_int_minE"></a>

    <a id="_CPPv3N19bk_ble_adv_params_t11adv_int_minE"></a> <a id="_CPPv2N19bk_ble_adv_params_t11adv_int_minE"></a> <a id="bk_ble_adv_params_t::adv_int_min__uint16_t"></a> <a id="structbk__ble__adv__params__t_1a96996a71f9ec4c9f2eec86183001293e"></a> uint16\_t adv\_int\_min
    :   Minimum advertising interval for undirected and low duty cycle directed advertising. Range: 0x0020 to 0x4000 Default: N \= 0x0800 (1.28 second) Time \= N \* 0.625 msec Time Range: 20 ms to 10.24 sec

    <a id="_CPPv4N19bk_ble_adv_params_t11adv_int_maxE"></a>

    <a id="_CPPv3N19bk_ble_adv_params_t11adv_int_maxE"></a> <a id="_CPPv2N19bk_ble_adv_params_t11adv_int_maxE"></a> <a id="bk_ble_adv_params_t::adv_int_max__uint16_t"></a> <a id="structbk__ble__adv__params__t_1af33a1015f6bf4489ed9936e41cacc9d5"></a> uint16\_t adv\_int\_max
    :   Maximum advertising interval for undirected and low duty cycle directed advertising. Range: 0x0020 to 0x4000 Default: N \= 0x0800 (1.28 second) Time \= N \* 0.625 msec Time Range: 20 ms to 10.24 sec Advertising max interval

    <a id="_CPPv4N19bk_ble_adv_params_t8adv_typeE"></a>

    <a id="_CPPv3N19bk_ble_adv_params_t8adv_typeE"></a> <a id="_CPPv2N19bk_ble_adv_params_t8adv_typeE"></a> <a id="bk_ble_adv_params_t::adv_type__bk_ble_adv_type_t"></a> <a id="structbk__ble__adv__params__t_1ae2df37ab58cd27cc5926422d31e73901"></a> [bk\_ble\_adv\_type\_t](#_CPPv417bk_ble_adv_type_t "bk_ble_adv_type_t") adv\_type
    :   Advertising type

    <a id="_CPPv4N19bk_ble_adv_params_t13own_addr_typeE"></a>

    <a id="_CPPv3N19bk_ble_adv_params_t13own_addr_typeE"></a> <a id="_CPPv2N19bk_ble_adv_params_t13own_addr_typeE"></a> <a id="bk_ble_adv_params_t::own_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__adv__params__t_1a70d41d91ec469b87bc660fbec9651273"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") own\_addr\_type
    :   Owner bluetooth device address type

    <a id="_CPPv4N19bk_ble_adv_params_t9peer_addrE"></a>

    <a id="_CPPv3N19bk_ble_adv_params_t9peer_addrE"></a> <a id="_CPPv2N19bk_ble_adv_params_t9peer_addrE"></a> <a id="bk_ble_adv_params_t::peer_addr__bk_bd_addr_t"></a> <a id="structbk__ble__adv__params__t_1a9523f690c01e773abda7616b7c23b98e"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") peer\_addr
    :   Peer device bluetooth device address

    <a id="_CPPv4N19bk_ble_adv_params_t14peer_addr_typeE"></a>

    <a id="_CPPv3N19bk_ble_adv_params_t14peer_addr_typeE"></a> <a id="_CPPv2N19bk_ble_adv_params_t14peer_addr_typeE"></a> <a id="bk_ble_adv_params_t::peer_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__adv__params__t_1a5ef65e3a18ea69077971ecea5f48bc2d"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") peer\_addr\_type
    :   Peer device bluetooth device address type, only support public address type and random address type

    <a id="_CPPv4N19bk_ble_adv_params_t11channel_mapE"></a>

    <a id="_CPPv3N19bk_ble_adv_params_t11channel_mapE"></a> <a id="_CPPv2N19bk_ble_adv_params_t11channel_mapE"></a> <a id="bk_ble_adv_params_t::channel_map__bk_ble_adv_channel_t"></a> <a id="structbk__ble__adv__params__t_1a7a8f1f52595735c5eb2489b82221d025"></a> [bk\_ble\_adv\_channel\_t](#_CPPv420bk_ble_adv_channel_t "bk_ble_adv_channel_t") channel\_map
    :   Advertising channel map

    <a id="_CPPv4N19bk_ble_adv_params_t17adv_filter_policyE"></a>

    <a id="_CPPv3N19bk_ble_adv_params_t17adv_filter_policyE"></a> <a id="_CPPv2N19bk_ble_adv_params_t17adv_filter_policyE"></a> <a id="bk_ble_adv_params_t::adv_filter_policy__bk_ble_adv_filter_t"></a> <a id="structbk__ble__adv__params__t_1a0b225244b46d417bc0cfe45d5d3ecebb"></a> [bk\_ble\_adv\_filter\_t](#_CPPv419bk_ble_adv_filter_t "bk_ble_adv_filter_t") adv\_filter\_policy
    :   Advertising filter policy

<a id="_CPPv417bk_ble_adv_data_t"></a>

<a id="_CPPv317bk_ble_adv_data_t"></a> <a id="_CPPv217bk_ble_adv_data_t"></a> <a id="bk_ble_adv_data_t"></a> <a id="structbk__ble__adv__data__t"></a> struct bk\_ble\_adv\_data\_t
:   Advertising data content, according to “Supplement to the Bluetooth Core Specification”.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_ble_adv_data_t12set_scan_rspE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t12set_scan_rspE"></a> <a id="_CPPv2N17bk_ble_adv_data_t12set_scan_rspE"></a> <a id="bk_ble_adv_data_t::set_scan_rsp__b"></a> <a id="structbk__ble__adv__data__t_1a84f64f34e83e634191265b2610bad344"></a> bool set\_scan\_rsp
    :   Set this advertising data as scan response or not

    <a id="_CPPv4N17bk_ble_adv_data_t12include_nameE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t12include_nameE"></a> <a id="_CPPv2N17bk_ble_adv_data_t12include_nameE"></a> <a id="bk_ble_adv_data_t::include_name__b"></a> <a id="structbk__ble__adv__data__t_1aa85d19f7cd8e4c291000af10d830f049"></a> bool include\_name
    :   Advertising data include device name or not

    <a id="_CPPv4N17bk_ble_adv_data_t15include_txpowerE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t15include_txpowerE"></a> <a id="_CPPv2N17bk_ble_adv_data_t15include_txpowerE"></a> <a id="bk_ble_adv_data_t::include_txpower__b"></a> <a id="structbk__ble__adv__data__t_1aa0fe5441eed923ac307ea556008b50cd"></a> bool include\_txpower
    :   Advertising data include TX power

    <a id="_CPPv4N17bk_ble_adv_data_t12min_intervalE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t12min_intervalE"></a> <a id="_CPPv2N17bk_ble_adv_data_t12min_intervalE"></a> <a id="bk_ble_adv_data_t::min_interval__i"></a> <a id="structbk__ble__adv__data__t_1ada9984656773e78af8a18715591ee9a8"></a> int min\_interval
    :   Advertising data show slave preferred connection min interval. The connection interval in the following manner: connIntervalmin \= Conn\_Interval\_Min \* 1.25 ms Conn\_Interval\_Min range: 0x0006 to 0x0C80 Value of 0xFFFF indicates no specific minimum. Values not defined above are reserved for future use.

    <a id="_CPPv4N17bk_ble_adv_data_t12max_intervalE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t12max_intervalE"></a> <a id="_CPPv2N17bk_ble_adv_data_t12max_intervalE"></a> <a id="bk_ble_adv_data_t::max_interval__i"></a> <a id="structbk__ble__adv__data__t_1a1f32168fb12647ed286f5f15b6ece1fc"></a> int max\_interval
    :   Advertising data show slave preferred connection max interval. The connection interval in the following manner: connIntervalmax \= Conn\_Interval\_Max \* 1.25 ms Conn\_Interval\_Max range: 0x0006 to 0x0C80 Conn\_Interval\_Max shall be equal to or greater than the Conn\_Interval\_Min. Value of 0xFFFF indicates no specific maximum. Values not defined above are reserved for future use.

    <a id="_CPPv4N17bk_ble_adv_data_t10appearanceE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t10appearanceE"></a> <a id="_CPPv2N17bk_ble_adv_data_t10appearanceE"></a> <a id="bk_ble_adv_data_t::appearance__i"></a> <a id="structbk__ble__adv__data__t_1aa7a0aac93bb8cceb734b6c1e07297b8a"></a> int appearance
    :   External appearance of device

    <a id="_CPPv4N17bk_ble_adv_data_t16manufacturer_lenE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t16manufacturer_lenE"></a> <a id="_CPPv2N17bk_ble_adv_data_t16manufacturer_lenE"></a> <a id="bk_ble_adv_data_t::manufacturer_len__uint16_t"></a> <a id="structbk__ble__adv__data__t_1a0c2522640aeb38c603e6ca0417c6148e"></a> uint16\_t manufacturer\_len
    :   Manufacturer data length

    <a id="_CPPv4N17bk_ble_adv_data_t19p_manufacturer_dataE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t19p_manufacturer_dataE"></a> <a id="_CPPv2N17bk_ble_adv_data_t19p_manufacturer_dataE"></a> <a id="bk_ble_adv_data_t::p_manufacturer_data__uint8_tP"></a> <a id="structbk__ble__adv__data__t_1a5d71441e072833ee7677a7590abef85e"></a> uint8\_t \*p\_manufacturer\_data
    :   Manufacturer data point

    <a id="_CPPv4N17bk_ble_adv_data_t16service_data_lenE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t16service_data_lenE"></a> <a id="_CPPv2N17bk_ble_adv_data_t16service_data_lenE"></a> <a id="bk_ble_adv_data_t::service_data_len__uint16_t"></a> <a id="structbk__ble__adv__data__t_1a07894bea83f8813eb61148857a47b0ab"></a> uint16\_t service\_data\_len
    :   Service data length

    <a id="_CPPv4N17bk_ble_adv_data_t14p_service_dataE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t14p_service_dataE"></a> <a id="_CPPv2N17bk_ble_adv_data_t14p_service_dataE"></a> <a id="bk_ble_adv_data_t::p_service_data__uint8_tP"></a> <a id="structbk__ble__adv__data__t_1a4d78047b2e621ed551afe76110df9053"></a> uint8\_t \*p\_service\_data
    :   Service data point

    <a id="_CPPv4N17bk_ble_adv_data_t16service_uuid_lenE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t16service_uuid_lenE"></a> <a id="_CPPv2N17bk_ble_adv_data_t16service_uuid_lenE"></a> <a id="bk_ble_adv_data_t::service_uuid_len__uint16_t"></a> <a id="structbk__ble__adv__data__t_1a0a9f68a121c665b694c1971029bcea95"></a> uint16\_t service\_uuid\_len
    :   Service uuid length

    <a id="_CPPv4N17bk_ble_adv_data_t14p_service_uuidE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t14p_service_uuidE"></a> <a id="_CPPv2N17bk_ble_adv_data_t14p_service_uuidE"></a> <a id="bk_ble_adv_data_t::p_service_uuid__uint8_tP"></a> <a id="structbk__ble__adv__data__t_1a286f9f090a31bae38dfe81d76d5c3d8e"></a> uint8\_t \*p\_service\_uuid
    :   Service uuid array point

    <a id="_CPPv4N17bk_ble_adv_data_t4flagE"></a>

    <a id="_CPPv3N17bk_ble_adv_data_t4flagE"></a> <a id="_CPPv2N17bk_ble_adv_data_t4flagE"></a> <a id="bk_ble_adv_data_t::flag__uint8_t"></a> <a id="structbk__ble__adv__data__t_1ac98a733c4c1f7e9b71d91d8bfa510c14"></a> uint8\_t flag
    :   Advertising flag of discovery mode, see BLE\_ADV\_DATA\_FLAG detail

<a id="_CPPv420bk_ble_scan_params_t"></a>

<a id="_CPPv320bk_ble_scan_params_t"></a> <a id="_CPPv220bk_ble_scan_params_t"></a> <a id="bk_ble_scan_params_t"></a> <a id="structbk__ble__scan__params__t"></a> struct bk\_ble\_scan\_params\_t
:   Ble scan parameters.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20bk_ble_scan_params_t9scan_typeE"></a>

    <a id="_CPPv3N20bk_ble_scan_params_t9scan_typeE"></a> <a id="_CPPv2N20bk_ble_scan_params_t9scan_typeE"></a> <a id="bk_ble_scan_params_t::scan_type__bk_ble_scan_type_t"></a> <a id="structbk__ble__scan__params__t_1a20130775f8c4453e95e612cf1adf53cc"></a> [bk\_ble\_scan\_type\_t](#_CPPv418bk_ble_scan_type_t "bk_ble_scan_type_t") scan\_type
    :   Scan type

    <a id="_CPPv4N20bk_ble_scan_params_t13own_addr_typeE"></a>

    <a id="_CPPv3N20bk_ble_scan_params_t13own_addr_typeE"></a> <a id="_CPPv2N20bk_ble_scan_params_t13own_addr_typeE"></a> <a id="bk_ble_scan_params_t::own_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__scan__params__t_1a883871855bce8ecff339ec3fb59464fc"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") own\_addr\_type
    :   Owner address type

    <a id="_CPPv4N20bk_ble_scan_params_t18scan_filter_policyE"></a>

    <a id="_CPPv3N20bk_ble_scan_params_t18scan_filter_policyE"></a> <a id="_CPPv2N20bk_ble_scan_params_t18scan_filter_policyE"></a> <a id="bk_ble_scan_params_t::scan_filter_policy__bk_ble_scan_filter_t"></a> <a id="structbk__ble__scan__params__t_1a7429be13c46bedbc966c15f1bc11525c"></a> [bk\_ble\_scan\_filter\_t](#_CPPv420bk_ble_scan_filter_t "bk_ble_scan_filter_t") scan\_filter\_policy
    :   Scan filter policy

    <a id="_CPPv4N20bk_ble_scan_params_t13scan_intervalE"></a>

    <a id="_CPPv3N20bk_ble_scan_params_t13scan_intervalE"></a> <a id="_CPPv2N20bk_ble_scan_params_t13scan_intervalE"></a> <a id="bk_ble_scan_params_t::scan_interval__uint16_t"></a> <a id="structbk__ble__scan__params__t_1a7ce78f66ba544dc84cc6666a6965bed9"></a> uint16\_t scan\_interval
    :   Scan interval. This is defined as the time interval from when the Controller started its last LE scan until it begins the subsequent LE scan. Range: 0x0004 to 0x4000 Default: 0x0010 (10 ms) Time \= N \* 0.625 msec Time Range: 2.5 msec to 10.24 seconds

    <a id="_CPPv4N20bk_ble_scan_params_t11scan_windowE"></a>

    <a id="_CPPv3N20bk_ble_scan_params_t11scan_windowE"></a> <a id="_CPPv2N20bk_ble_scan_params_t11scan_windowE"></a> <a id="bk_ble_scan_params_t::scan_window__uint16_t"></a> <a id="structbk__ble__scan__params__t_1a59d5eac499054286c1041e04119815a6"></a> uint16\_t scan\_window
    :   Scan window. The duration of the LE scan. LE\_Scan\_Window shall be less than or equal to LE\_Scan\_Interval Range: 0x0004 to 0x4000 Default: 0x0010 (10 ms) Time \= N \* 0.625 msec Time Range: 2.5 msec to 10240 msec

    <a id="_CPPv4N20bk_ble_scan_params_t14scan_duplicateE"></a>

    <a id="_CPPv3N20bk_ble_scan_params_t14scan_duplicateE"></a> <a id="_CPPv2N20bk_ble_scan_params_t14scan_duplicateE"></a> <a id="bk_ble_scan_params_t::scan_duplicate__bk_ble_scan_duplicate_t"></a> <a id="structbk__ble__scan__params__t_1a33ba5308a16deee4a59c8c612d3911b1"></a> [bk\_ble\_scan\_duplicate\_t](#_CPPv423bk_ble_scan_duplicate_t "bk_ble_scan_duplicate_t") scan\_duplicate
    :   The Scan\_Duplicates parameter controls whether the Link Layer should filter out duplicate advertising reports (BLE\_SCAN\_DUPLICATE\_ENABLE) to the Host, or if the Link Layer should generate advertising reports for each packet received

<a id="_CPPv427bk_gap_create_conn_params_t"></a>

<a id="_CPPv327bk_gap_create_conn_params_t"></a> <a id="_CPPv227bk_gap_create_conn_params_t"></a> <a id="bk_gap_create_conn_params_t"></a> <a id="structbk__gap__create__conn__params__t"></a> struct bk\_gap\_create\_conn\_params\_t
:   create connection param

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N27bk_gap_create_conn_params_t13scan_intervalE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t13scan_intervalE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t13scan_intervalE"></a> <a id="bk_gap_create_conn_params_t::scan_interval__uint16_t"></a> <a id="structbk__gap__create__conn__params__t_1a353ef7eecbeddf35385c5affb0419790"></a> uint16\_t scan\_interval
    :   scan interval, unit in 0.625ms

    <a id="_CPPv4N27bk_gap_create_conn_params_t11scan_windowE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t11scan_windowE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t11scan_windowE"></a> <a id="bk_gap_create_conn_params_t::scan_window__uint16_t"></a> <a id="structbk__gap__create__conn__params__t_1a85e64300f59050bd85c973c92a52d5a9"></a> uint16\_t scan\_window
    :   scan window, unit in 0.625ms

    <a id="_CPPv4N27bk_gap_create_conn_params_t23initiator_filter_policyE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t23initiator_filter_policyE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t23initiator_filter_policyE"></a> <a id="bk_gap_create_conn_params_t::initiator_filter_policy__uint8_t"></a> <a id="structbk__gap__create__conn__params__t_1ad59631f27c2afa9634d346b95a1b16d7"></a> uint8\_t initiator\_filter\_policy
    :   policy that how to use white list. 0 means not used, 1 means only connect device that in white list

    <a id="_CPPv4N27bk_gap_create_conn_params_t15local_addr_typeE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t15local_addr_typeE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t15local_addr_typeE"></a> <a id="bk_gap_create_conn_params_t::local_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__gap__create__conn__params__t_1a2b077efa4264a938be8569fed02d9c3b"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") local\_addr\_type
    :   local address type

    <a id="_CPPv4N27bk_gap_create_conn_params_t9peer_addrE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t9peer_addrE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t9peer_addrE"></a> <a id="bk_gap_create_conn_params_t::peer_addr__bk_bd_addr_t"></a> <a id="structbk__gap__create__conn__params__t_1aa0409f95b089547817ed369e06bf21bc"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") peer\_addr
    :   peer addr

    <a id="_CPPv4N27bk_gap_create_conn_params_t14peer_addr_typeE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t14peer_addr_typeE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t14peer_addr_typeE"></a> <a id="bk_gap_create_conn_params_t::peer_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__gap__create__conn__params__t_1a476ce065c3d9429f85510b1aa15177a5"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") peer\_addr\_type
    :   Peer address type, only BLE\_ADDR\_TYPE\_PUBLIC or BLE\_ADDR\_TYPE\_RANDOM available

    <a id="_CPPv4N27bk_gap_create_conn_params_t17conn_interval_minE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t17conn_interval_minE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t17conn_interval_minE"></a> <a id="bk_gap_create_conn_params_t::conn_interval_min__uint16_t"></a> <a id="structbk__gap__create__conn__params__t_1acc8666f7e4f90cd953a4aa48c77d6c05"></a> uint16\_t conn\_interval\_min
    :   conn min interval, unit in 1.25ms, Range: 7.5ms to 4s

    <a id="_CPPv4N27bk_gap_create_conn_params_t17conn_interval_maxE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t17conn_interval_maxE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t17conn_interval_maxE"></a> <a id="bk_gap_create_conn_params_t::conn_interval_max__uint16_t"></a> <a id="structbk__gap__create__conn__params__t_1a3d93d84e66e5ef70beec178ad768b0ac"></a> uint16\_t conn\_interval\_max
    :   conn max interval, unit in 1.25ms, Range: 7.5ms to 4s

    <a id="_CPPv4N27bk_gap_create_conn_params_t12conn_latencyE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t12conn_latencyE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t12conn_latencyE"></a> <a id="bk_gap_create_conn_params_t::conn_latency__uint16_t"></a> <a id="structbk__gap__create__conn__params__t_1af0be6a27d9e72c061b1a19c0071af787"></a> uint16\_t conn\_latency
    :   latency Range: 0x0000 to 0x01F3

    <a id="_CPPv4N27bk_gap_create_conn_params_t19supervision_timeoutE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t19supervision_timeoutE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t19supervision_timeoutE"></a> <a id="bk_gap_create_conn_params_t::supervision_timeout__uint16_t"></a> <a id="structbk__gap__create__conn__params__t_1ade9da6ee89ab63d240ad2159d316472b"></a> uint16\_t supervision\_timeout
    :   conn timeout, unit in 10ms Range: 100ms to 32s

    <a id="_CPPv4N27bk_gap_create_conn_params_t6min_ceE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t6min_ceE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t6min_ceE"></a> <a id="bk_gap_create_conn_params_t::min_ce__uint16_t"></a> <a id="structbk__gap__create__conn__params__t_1aee7267a373f9ad577b5a8afd9cc3174c"></a> uint16\_t min\_ce
    :   minimum length of connection event recommended, unit in 0.625ms Range: 0x0000 to 0xFFFF

    <a id="_CPPv4N27bk_gap_create_conn_params_t6max_ceE"></a>

    <a id="_CPPv3N27bk_gap_create_conn_params_t6max_ceE"></a> <a id="_CPPv2N27bk_gap_create_conn_params_t6max_ceE"></a> <a id="bk_gap_create_conn_params_t::max_ce__uint16_t"></a> <a id="structbk__gap__create__conn__params__t_1a642293f9ffc2f6d01f961c9f89c002e8"></a> uint16\_t max\_ce
    :   maximum length of connection event recommended, unit in 0.625ms Range: 0x0000 to 0xFFFF

<a id="_CPPv420bk_gap_conn_params_t"></a>

<a id="_CPPv320bk_gap_conn_params_t"></a> <a id="_CPPv220bk_gap_conn_params_t"></a> <a id="bk_gap_conn_params_t"></a> <a id="structbk__gap__conn__params__t"></a> struct bk\_gap\_conn\_params\_t
:   connection parameters information

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20bk_gap_conn_params_t8intervalE"></a>

    <a id="_CPPv3N20bk_gap_conn_params_t8intervalE"></a> <a id="_CPPv2N20bk_gap_conn_params_t8intervalE"></a> <a id="bk_gap_conn_params_t::interval__uint16_t"></a> <a id="structbk__gap__conn__params__t_1a8af39dd33946a3ebcca317dcea7bcea5"></a> uint16\_t interval
    :   connection interval

    <a id="_CPPv4N20bk_gap_conn_params_t7latencyE"></a>

    <a id="_CPPv3N20bk_gap_conn_params_t7latencyE"></a> <a id="_CPPv2N20bk_gap_conn_params_t7latencyE"></a> <a id="bk_gap_conn_params_t::latency__uint16_t"></a> <a id="structbk__gap__conn__params__t_1afa4c5a34913c8a07d7d15a776a5f6491"></a> uint16\_t latency
    :   Slave latency for the connection in number of connection events. Range: 0x0000 to 0x01F3

    <a id="_CPPv4N20bk_gap_conn_params_t7timeoutE"></a>

    <a id="_CPPv3N20bk_gap_conn_params_t7timeoutE"></a> <a id="_CPPv2N20bk_gap_conn_params_t7timeoutE"></a> <a id="bk_gap_conn_params_t::timeout__uint16_t"></a> <a id="structbk__gap__conn__params__t_1a02e8ceedd4944da4e0fe1c3cf1f0473c"></a> uint16\_t timeout
    :   Supervision timeout for the LE Link. Range: 0x000A to 0x0C80. Mandatory Range: 0x000A to 0x0C80 Time \= N \* 10 msec Time Range: 100 msec to 32 seconds

<a id="_CPPv427bk_ble_conn_update_params_t"></a>

<a id="_CPPv327bk_ble_conn_update_params_t"></a> <a id="_CPPv227bk_ble_conn_update_params_t"></a> <a id="bk_ble_conn_update_params_t"></a> <a id="structbk__ble__conn__update__params__t"></a> struct bk\_ble\_conn\_update\_params\_t
:   Connection update parameters.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N27bk_ble_conn_update_params_t3bdaE"></a>

    <a id="_CPPv3N27bk_ble_conn_update_params_t3bdaE"></a> <a id="_CPPv2N27bk_ble_conn_update_params_t3bdaE"></a> <a id="bk_ble_conn_update_params_t::bda__bk_bd_addr_t"></a> <a id="structbk__ble__conn__update__params__t_1ac63f2a15a4f817e23fe6eccdc2f961cc"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
    :   Bluetooth device address

    <a id="_CPPv4N27bk_ble_conn_update_params_t7min_intE"></a>

    <a id="_CPPv3N27bk_ble_conn_update_params_t7min_intE"></a> <a id="_CPPv2N27bk_ble_conn_update_params_t7min_intE"></a> <a id="bk_ble_conn_update_params_t::min_int__uint16_t"></a> <a id="structbk__ble__conn__update__params__t_1a53e38d7af867c3568acc6a6dae7ee1d9"></a> uint16\_t min\_int
    :   Min connection interval

    <a id="_CPPv4N27bk_ble_conn_update_params_t7max_intE"></a>

    <a id="_CPPv3N27bk_ble_conn_update_params_t7max_intE"></a> <a id="_CPPv2N27bk_ble_conn_update_params_t7max_intE"></a> <a id="bk_ble_conn_update_params_t::max_int__uint16_t"></a> <a id="structbk__ble__conn__update__params__t_1a47dc50d7aa5acc9bd185c0c2bb50a85c"></a> uint16\_t max\_int
    :   Max connection interval

    <a id="_CPPv4N27bk_ble_conn_update_params_t7latencyE"></a>

    <a id="_CPPv3N27bk_ble_conn_update_params_t7latencyE"></a> <a id="_CPPv2N27bk_ble_conn_update_params_t7latencyE"></a> <a id="bk_ble_conn_update_params_t::latency__uint16_t"></a> <a id="structbk__ble__conn__update__params__t_1a42ff6f715da07e986c207386edb2481b"></a> uint16\_t latency
    :   Slave latency for the connection in number of connection events. Range: 0x0000 to 0x01F3

    <a id="_CPPv4N27bk_ble_conn_update_params_t7timeoutE"></a>

    <a id="_CPPv3N27bk_ble_conn_update_params_t7timeoutE"></a> <a id="_CPPv2N27bk_ble_conn_update_params_t7timeoutE"></a> <a id="bk_ble_conn_update_params_t::timeout__uint16_t"></a> <a id="structbk__ble__conn__update__params__t_1a730de502f163b614da664dba5a67d52a"></a> uint16\_t timeout
    :   Supervision timeout for the LE Link. Range: 0x000A to 0x0C80. Mandatory Range: 0x000A to 0x0C80 Time \= N \* 10 msec Time Range: 100 msec to 32 seconds

<a id="_CPPv431bk_ble_pkt_data_length_params_t"></a>

<a id="_CPPv331bk_ble_pkt_data_length_params_t"></a> <a id="_CPPv231bk_ble_pkt_data_length_params_t"></a> <a id="bk_ble_pkt_data_length_params_t"></a> <a id="structbk__ble__pkt__data__length__params__t"></a> struct bk\_ble\_pkt\_data\_length\_params\_t
:   BLE pkt date length keys.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N31bk_ble_pkt_data_length_params_t6rx_lenE"></a>

    <a id="_CPPv3N31bk_ble_pkt_data_length_params_t6rx_lenE"></a> <a id="_CPPv2N31bk_ble_pkt_data_length_params_t6rx_lenE"></a> <a id="bk_ble_pkt_data_length_params_t::rx_len__uint16_t"></a> <a id="structbk__ble__pkt__data__length__params__t_1a305fdca4d13e549ac910a2a9b2d55284"></a> uint16\_t rx\_len
    :   pkt rx data length value

    <a id="_CPPv4N31bk_ble_pkt_data_length_params_t6tx_lenE"></a>

    <a id="_CPPv3N31bk_ble_pkt_data_length_params_t6tx_lenE"></a> <a id="_CPPv2N31bk_ble_pkt_data_length_params_t6tx_lenE"></a> <a id="bk_ble_pkt_data_length_params_t::tx_len__uint16_t"></a> <a id="structbk__ble__pkt__data__length__params__t_1a17e79124a7e88697ec668aca56bac17a"></a> uint16\_t tx\_len
    :   pkt tx data length value

<a id="_CPPv418bk_ble_penc_keys_t"></a>

<a id="_CPPv318bk_ble_penc_keys_t"></a> <a id="_CPPv218bk_ble_penc_keys_t"></a> <a id="bk_ble_penc_keys_t"></a> <a id="structbk__ble__penc__keys__t"></a> struct bk\_ble\_penc\_keys\_t
:   BLE encryption keys.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_ble_penc_keys_t3ltkE"></a>

    <a id="_CPPv3N18bk_ble_penc_keys_t3ltkE"></a> <a id="_CPPv2N18bk_ble_penc_keys_t3ltkE"></a> <a id="bk_ble_penc_keys_t::ltk__bk_bt_octet16_t"></a> <a id="structbk__ble__penc__keys__t_1aabdc68bb55ff97c5a4b198209e43adae"></a> [bk\_bt\_octet16\_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") ltk
    :   The long term key

    <a id="_CPPv4N18bk_ble_penc_keys_t4randE"></a>

    <a id="_CPPv3N18bk_ble_penc_keys_t4randE"></a> <a id="_CPPv2N18bk_ble_penc_keys_t4randE"></a> <a id="bk_ble_penc_keys_t::rand__bk_bt_octet8_t"></a> <a id="structbk__ble__penc__keys__t_1a8c1b0a41f3cb9b642d1d859e8c47d2c3"></a> [bk\_bt\_octet8\_t](#_CPPv414bk_bt_octet8_t "bk_bt_octet8_t") rand
    :   The random number

    <a id="_CPPv4N18bk_ble_penc_keys_t4edivE"></a>

    <a id="_CPPv3N18bk_ble_penc_keys_t4edivE"></a> <a id="_CPPv2N18bk_ble_penc_keys_t4edivE"></a> <a id="bk_ble_penc_keys_t::ediv__uint16_t"></a> <a id="structbk__ble__penc__keys__t_1a65b0972ee46821b5745ee6d08147470f"></a> uint16\_t ediv
    :   The ediv value

    <a id="_CPPv4N18bk_ble_penc_keys_t9sec_levelE"></a>

    <a id="_CPPv3N18bk_ble_penc_keys_t9sec_levelE"></a> <a id="_CPPv2N18bk_ble_penc_keys_t9sec_levelE"></a> <a id="bk_ble_penc_keys_t::sec_level__uint8_t"></a> <a id="structbk__ble__penc__keys__t_1abd070493efbeea645714ef3fbb074b53"></a> uint8\_t sec\_level
    :   The security level of the security link, see bk\_ble\_security\_level\_t

    <a id="_CPPv4N18bk_ble_penc_keys_t8key_sizeE"></a>

    <a id="_CPPv3N18bk_ble_penc_keys_t8key_sizeE"></a> <a id="_CPPv2N18bk_ble_penc_keys_t8key_sizeE"></a> <a id="bk_ble_penc_keys_t::key_size__uint8_t"></a> <a id="structbk__ble__penc__keys__t_1a0e4d0b01dd2a60300dd0cf42e54ed081"></a> uint8\_t key\_size
    :   The key size(7\~16) of the security link

<a id="_CPPv419bk_ble_pcsrk_keys_t"></a>

<a id="_CPPv319bk_ble_pcsrk_keys_t"></a> <a id="_CPPv219bk_ble_pcsrk_keys_t"></a> <a id="bk_ble_pcsrk_keys_t"></a> <a id="structbk__ble__pcsrk__keys__t"></a> struct bk\_ble\_pcsrk\_keys\_t
:   BLE CSRK keys.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_ble_pcsrk_keys_t7counterE"></a>

    <a id="_CPPv3N19bk_ble_pcsrk_keys_t7counterE"></a> <a id="_CPPv2N19bk_ble_pcsrk_keys_t7counterE"></a> <a id="bk_ble_pcsrk_keys_t::counter__uint32_t"></a> <a id="structbk__ble__pcsrk__keys__t_1ad873214f26e21623b01f356e4faabe48"></a> uint32\_t counter
    :   The counter

    <a id="_CPPv4N19bk_ble_pcsrk_keys_t4csrkE"></a>

    <a id="_CPPv3N19bk_ble_pcsrk_keys_t4csrkE"></a> <a id="_CPPv2N19bk_ble_pcsrk_keys_t4csrkE"></a> <a id="bk_ble_pcsrk_keys_t::csrk__bk_bt_octet16_t"></a> <a id="structbk__ble__pcsrk__keys__t_1a98e6ecf3d5ee075ed40cff75e3ff65e7"></a> [bk\_bt\_octet16\_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") csrk
    :   The csrk key

    <a id="_CPPv4N19bk_ble_pcsrk_keys_t9sec_levelE"></a>

    <a id="_CPPv3N19bk_ble_pcsrk_keys_t9sec_levelE"></a> <a id="_CPPv2N19bk_ble_pcsrk_keys_t9sec_levelE"></a> <a id="bk_ble_pcsrk_keys_t::sec_level__uint8_t"></a> <a id="structbk__ble__pcsrk__keys__t_1a467ec4479565f71f4d812b240c635b00"></a> uint8\_t sec\_level
    :   The security level see bk\_ble\_security\_level\_t

<a id="_CPPv417bk_ble_pid_keys_t"></a>

<a id="_CPPv317bk_ble_pid_keys_t"></a> <a id="_CPPv217bk_ble_pid_keys_t"></a> <a id="bk_ble_pid_keys_t"></a> <a id="structbk__ble__pid__keys__t"></a> struct bk\_ble\_pid\_keys\_t
:   BLE pid keys.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_ble_pid_keys_t3irkE"></a>

    <a id="_CPPv3N17bk_ble_pid_keys_t3irkE"></a> <a id="_CPPv2N17bk_ble_pid_keys_t3irkE"></a> <a id="bk_ble_pid_keys_t::irk__bk_bt_octet16_t"></a> <a id="structbk__ble__pid__keys__t_1a040d160f3f28cec6b2b6f3afea9d8411"></a> [bk\_bt\_octet16\_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") irk
    :   The irk value

    <a id="_CPPv4N17bk_ble_pid_keys_t9addr_typeE"></a>

    <a id="_CPPv3N17bk_ble_pid_keys_t9addr_typeE"></a> <a id="_CPPv2N17bk_ble_pid_keys_t9addr_typeE"></a> <a id="bk_ble_pid_keys_t::addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__pid__keys__t_1acc7f0008ec2e7defcf0ef036ee5dc1ff"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr\_type
    :   The address type

    <a id="_CPPv4N17bk_ble_pid_keys_t11static_addrE"></a>

    <a id="_CPPv3N17bk_ble_pid_keys_t11static_addrE"></a> <a id="_CPPv2N17bk_ble_pid_keys_t11static_addrE"></a> <a id="bk_ble_pid_keys_t::static_addr__bk_bd_addr_t"></a> <a id="structbk__ble__pid__keys__t_1a20122bf132ee9aaf222fd84d0f8e589c"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") static\_addr
    :   The static address

<a id="_CPPv418bk_ble_lenc_keys_t"></a>

<a id="_CPPv318bk_ble_lenc_keys_t"></a> <a id="_CPPv218bk_ble_lenc_keys_t"></a> <a id="bk_ble_lenc_keys_t"></a> <a id="structbk__ble__lenc__keys__t"></a> struct bk\_ble\_lenc\_keys\_t
:   BLE Encryption reproduction keys.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_ble_lenc_keys_t3ltkE"></a>

    <a id="_CPPv3N18bk_ble_lenc_keys_t3ltkE"></a> <a id="_CPPv2N18bk_ble_lenc_keys_t3ltkE"></a> <a id="bk_ble_lenc_keys_t::ltk__bk_bt_octet16_t"></a> <a id="structbk__ble__lenc__keys__t_1afedebc8c97f872fb55d0453efb2174a0"></a> [bk\_bt\_octet16\_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") ltk
    :   The long term key

    <a id="_CPPv4N18bk_ble_lenc_keys_t4randE"></a>

    <a id="_CPPv3N18bk_ble_lenc_keys_t4randE"></a> <a id="_CPPv2N18bk_ble_lenc_keys_t4randE"></a> <a id="bk_ble_lenc_keys_t::rand__bk_bt_octet8_t"></a> <a id="structbk__ble__lenc__keys__t_1ad650d8212e5cbc8384b86d9feda302cf"></a> [bk\_bt\_octet8\_t](#_CPPv414bk_bt_octet8_t "bk_bt_octet8_t") rand
    :   The random number

    <a id="_CPPv4N18bk_ble_lenc_keys_t3divE"></a>

    <a id="_CPPv3N18bk_ble_lenc_keys_t3divE"></a> <a id="_CPPv2N18bk_ble_lenc_keys_t3divE"></a> <a id="bk_ble_lenc_keys_t::div__uint16_t"></a> <a id="structbk__ble__lenc__keys__t_1a89b57224828db8a1b5b2578f9a378bb5"></a> uint16\_t div
    :   The div value

    <a id="_CPPv4N18bk_ble_lenc_keys_t8key_sizeE"></a>

    <a id="_CPPv3N18bk_ble_lenc_keys_t8key_sizeE"></a> <a id="_CPPv2N18bk_ble_lenc_keys_t8key_sizeE"></a> <a id="bk_ble_lenc_keys_t::key_size__uint8_t"></a> <a id="structbk__ble__lenc__keys__t_1adbe3ecdd837270b4bc482e0be449128d"></a> uint8\_t key\_size
    :   The key size of the security link

    <a id="_CPPv4N18bk_ble_lenc_keys_t9sec_levelE"></a>

    <a id="_CPPv3N18bk_ble_lenc_keys_t9sec_levelE"></a> <a id="_CPPv2N18bk_ble_lenc_keys_t9sec_levelE"></a> <a id="bk_ble_lenc_keys_t::sec_level__uint8_t"></a> <a id="structbk__ble__lenc__keys__t_1ac05c15e05df628e45d8045711993a7d2"></a> uint8\_t sec\_level
    :   The security level of the security link see bk\_ble\_security\_level\_t

<a id="_CPPv419bk_ble_lcsrk_keys_t"></a>

<a id="_CPPv319bk_ble_lcsrk_keys_t"></a> <a id="_CPPv219bk_ble_lcsrk_keys_t"></a> <a id="bk_ble_lcsrk_keys_t"></a> <a id="structbk__ble__lcsrk__keys__t"></a> struct bk\_ble\_lcsrk\_keys\_t
:   BLE SRK keys.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_ble_lcsrk_keys_t7counterE"></a>

    <a id="_CPPv3N19bk_ble_lcsrk_keys_t7counterE"></a> <a id="_CPPv2N19bk_ble_lcsrk_keys_t7counterE"></a> <a id="bk_ble_lcsrk_keys_t::counter__uint32_t"></a> <a id="structbk__ble__lcsrk__keys__t_1ab6915c694674cf75f2d60568cd198f47"></a> uint32\_t counter
    :   The counter value

    <a id="_CPPv4N19bk_ble_lcsrk_keys_t3divE"></a>

    <a id="_CPPv3N19bk_ble_lcsrk_keys_t3divE"></a> <a id="_CPPv2N19bk_ble_lcsrk_keys_t3divE"></a> <a id="bk_ble_lcsrk_keys_t::div__uint16_t"></a> <a id="structbk__ble__lcsrk__keys__t_1a50002d7fae22a1f8b8811bf03b019ee8"></a> uint16\_t div
    :   The div value

    <a id="_CPPv4N19bk_ble_lcsrk_keys_t9sec_levelE"></a>

    <a id="_CPPv3N19bk_ble_lcsrk_keys_t9sec_levelE"></a> <a id="_CPPv2N19bk_ble_lcsrk_keys_t9sec_levelE"></a> <a id="bk_ble_lcsrk_keys_t::sec_level__uint8_t"></a> <a id="structbk__ble__lcsrk__keys__t_1a533bd021b6085c36185a21c480b11810"></a> uint8\_t sec\_level
    :   The security level of the security link see bk\_ble\_security\_level\_t

    <a id="_CPPv4N19bk_ble_lcsrk_keys_t4csrkE"></a>

    <a id="_CPPv3N19bk_ble_lcsrk_keys_t4csrkE"></a> <a id="_CPPv2N19bk_ble_lcsrk_keys_t4csrkE"></a> <a id="bk_ble_lcsrk_keys_t::csrk__bk_bt_octet16_t"></a> <a id="structbk__ble__lcsrk__keys__t_1a998b0142be9b51115dd542d6274efb5d"></a> [bk\_bt\_octet16\_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") csrk
    :   The csrk key value

<a id="_CPPv418bk_ble_link_keys_t"></a>

<a id="_CPPv318bk_ble_link_keys_t"></a> <a id="_CPPv218bk_ble_link_keys_t"></a> <a id="bk_ble_link_keys_t"></a> <a id="structbk__ble__link__keys__t"></a> struct bk\_ble\_link\_keys\_t

<a id="_CPPv422bk_ble_sec_key_notif_t"></a>

<a id="_CPPv322bk_ble_sec_key_notif_t"></a> <a id="_CPPv222bk_ble_sec_key_notif_t"></a> <a id="bk_ble_sec_key_notif_t"></a> <a id="structbk__ble__sec__key__notif__t"></a> struct bk\_ble\_sec\_key\_notif\_t
:   Structure associated with BK\_KEY\_NOTIF\_EVT.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_ble_sec_key_notif_t7bd_addrE"></a>

    <a id="_CPPv3N22bk_ble_sec_key_notif_t7bd_addrE"></a> <a id="_CPPv2N22bk_ble_sec_key_notif_t7bd_addrE"></a> <a id="bk_ble_sec_key_notif_t::bd_addr__bk_bd_addr_t"></a> <a id="structbk__ble__sec__key__notif__t_1a488b2de79091f737c8ef52ef2c6f406e"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
    :   peer address

    <a id="_CPPv4N22bk_ble_sec_key_notif_t7passkeyE"></a>

    <a id="_CPPv3N22bk_ble_sec_key_notif_t7passkeyE"></a> <a id="_CPPv2N22bk_ble_sec_key_notif_t7passkeyE"></a> <a id="bk_ble_sec_key_notif_t::passkey__uint32_t"></a> <a id="structbk__ble__sec__key__notif__t_1a8553d9c08c4d5093ff55c095ba63b0ae"></a> uint32\_t passkey
    :   the passkey or numeric value for comparison. If just\_works, do not show this number to UI

<a id="_CPPv416bk_ble_sec_req_t"></a>

<a id="_CPPv316bk_ble_sec_req_t"></a> <a id="_CPPv216bk_ble_sec_req_t"></a> <a id="bk_ble_sec_req_t"></a> <a id="structbk__ble__sec__req__t"></a> struct bk\_ble\_sec\_req\_t
:   Structure of the security request.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16bk_ble_sec_req_t7bd_addrE"></a>

    <a id="_CPPv3N16bk_ble_sec_req_t7bd_addrE"></a> <a id="_CPPv2N16bk_ble_sec_req_t7bd_addrE"></a> <a id="bk_ble_sec_req_t::bd_addr__bk_bd_addr_t"></a> <a id="structbk__ble__sec__req__t_1ad0e133b06f06e61b0d4d0d08466ee222"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
    :   peer address

<a id="_CPPv422bk_ble_bond_key_info_t"></a>

<a id="_CPPv322bk_ble_bond_key_info_t"></a> <a id="_CPPv222bk_ble_bond_key_info_t"></a> <a id="bk_ble_bond_key_info_t"></a> <a id="structbk__ble__bond__key__info__t"></a> struct bk\_ble\_bond\_key\_info\_t
:   struct type of the bond key information value

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_ble_bond_key_info_t8key_maskE"></a>

    <a id="_CPPv3N22bk_ble_bond_key_info_t8key_maskE"></a> <a id="_CPPv2N22bk_ble_bond_key_info_t8key_maskE"></a> <a id="bk_ble_bond_key_info_t::key_mask__bk_ble_key_mask_t"></a> <a id="structbk__ble__bond__key__info__t_1aaa00909c42da0ad1bed9a618ea673e5e"></a> [bk\_ble\_key\_mask\_t](#_CPPv417bk_ble_key_mask_t "bk_ble_key_mask_t") key\_mask
    :   the key mask to indicate witch key is present

    <a id="_CPPv4N22bk_ble_bond_key_info_t8penc_keyE"></a>

    <a id="_CPPv3N22bk_ble_bond_key_info_t8penc_keyE"></a> <a id="_CPPv2N22bk_ble_bond_key_info_t8penc_keyE"></a> <a id="bk_ble_bond_key_info_t::penc_key__bk_ble_penc_keys_t"></a> <a id="structbk__ble__bond__key__info__t_1a153e603d4dbdf6e3d88fea79b32d1252"></a> [bk\_ble\_penc\_keys\_t](#_CPPv418bk_ble_penc_keys_t "bk_ble_penc_keys_t") penc\_key
    :   received peer encryption key

    <a id="_CPPv4N22bk_ble_bond_key_info_t7pid_keyE"></a>

    <a id="_CPPv3N22bk_ble_bond_key_info_t7pid_keyE"></a> <a id="_CPPv2N22bk_ble_bond_key_info_t7pid_keyE"></a> <a id="bk_ble_bond_key_info_t::pid_key__bk_ble_pid_keys_t"></a> <a id="structbk__ble__bond__key__info__t_1af6d731e6dfd2c301af8069bebbc5ab0a"></a> [bk\_ble\_pid\_keys\_t](#_CPPv417bk_ble_pid_keys_t "bk_ble_pid_keys_t") pid\_key
    :   peer device ID key

    <a id="_CPPv4N22bk_ble_bond_key_info_t9pcsrk_keyE"></a>

    <a id="_CPPv3N22bk_ble_bond_key_info_t9pcsrk_keyE"></a> <a id="_CPPv2N22bk_ble_bond_key_info_t9pcsrk_keyE"></a> <a id="bk_ble_bond_key_info_t::pcsrk_key__bk_ble_pcsrk_keys_t"></a> <a id="structbk__ble__bond__key__info__t_1a0fb6e1c60d8836fe7e0176b597de66b3"></a> [bk\_ble\_pcsrk\_keys\_t](#_CPPv419bk_ble_pcsrk_keys_t "bk_ble_pcsrk_keys_t") pcsrk\_key
    :   received peer device SRK

    <a id="_CPPv4N22bk_ble_bond_key_info_t8lenc_keyE"></a>

    <a id="_CPPv3N22bk_ble_bond_key_info_t8lenc_keyE"></a> <a id="_CPPv2N22bk_ble_bond_key_info_t8lenc_keyE"></a> <a id="bk_ble_bond_key_info_t::lenc_key__bk_ble_lenc_keys_t"></a> <a id="structbk__ble__bond__key__info__t_1a9f43741d08948538a14810700e2f22c1"></a> [bk\_ble\_lenc\_keys\_t](#_CPPv418bk_ble_lenc_keys_t "bk_ble_lenc_keys_t") lenc\_key
    :   local encryption reproduction keys LTK \= \= d1(ER,DIV,0)

    <a id="_CPPv4N22bk_ble_bond_key_info_t7lid_keyE"></a>

    <a id="_CPPv3N22bk_ble_bond_key_info_t7lid_keyE"></a> <a id="_CPPv2N22bk_ble_bond_key_info_t7lid_keyE"></a> <a id="bk_ble_bond_key_info_t::lid_key__bk_ble_pid_keys_t"></a> <a id="structbk__ble__bond__key__info__t_1a5580e5a40cba41a8131e951d377a3833"></a> [bk\_ble\_pid\_keys\_t](#_CPPv417bk_ble_pid_keys_t "bk_ble_pid_keys_t") lid\_key
    :   local device ID key

    <a id="_CPPv4N22bk_ble_bond_key_info_t9lcsrk_keyE"></a>

    <a id="_CPPv3N22bk_ble_bond_key_info_t9lcsrk_keyE"></a> <a id="_CPPv2N22bk_ble_bond_key_info_t9lcsrk_keyE"></a> <a id="bk_ble_bond_key_info_t::lcsrk_key__bk_ble_lcsrk_keys_t"></a> <a id="structbk__ble__bond__key__info__t_1aadc6c80a25d1611036e326ad6e424486"></a> [bk\_ble\_lcsrk\_keys\_t](#_CPPv419bk_ble_lcsrk_keys_t "bk_ble_lcsrk_keys_t") lcsrk\_key
    :   local device CSRK \= d1(ER,DIV,1)

<a id="_CPPv417bk_ble_bond_dev_t"></a>

<a id="_CPPv317bk_ble_bond_dev_t"></a> <a id="_CPPv217bk_ble_bond_dev_t"></a> <a id="bk_ble_bond_dev_t"></a> <a id="structbk__ble__bond__dev__t"></a> struct bk\_ble\_bond\_dev\_t
:   struct type of the bond device value

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_ble_bond_dev_t7bd_addrE"></a>

    <a id="_CPPv3N17bk_ble_bond_dev_t7bd_addrE"></a> <a id="_CPPv2N17bk_ble_bond_dev_t7bd_addrE"></a> <a id="bk_ble_bond_dev_t::bd_addr__bk_bd_addr_t"></a> <a id="structbk__ble__bond__dev__t_1a8e25c46c09714f87fecf7537e214597a"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
    :   peer nominal address

    <a id="_CPPv4N17bk_ble_bond_dev_t8bond_keyE"></a>

    <a id="_CPPv3N17bk_ble_bond_dev_t8bond_keyE"></a> <a id="_CPPv2N17bk_ble_bond_dev_t8bond_keyE"></a> <a id="bk_ble_bond_dev_t::bond_key__bk_ble_bond_key_info_t"></a> <a id="structbk__ble__bond__dev__t_1a429c72e4213d3bf9be90990539e60b0c"></a> [bk\_ble\_bond\_key\_info\_t](#_CPPv422bk_ble_bond_key_info_t "bk_ble_bond_key_info_t") bond\_key
    :   peer address type

        the bond key information

<a id="_CPPv419bk_ble_local_keys_t"></a>

<a id="_CPPv319bk_ble_local_keys_t"></a> <a id="_CPPv219bk_ble_local_keys_t"></a> <a id="bk_ble_local_keys_t"></a> <a id="structbk__ble__local__keys__t"></a> struct bk\_ble\_local\_keys\_t
:   structure type of the ble local keys value

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_ble_local_keys_t2irE"></a>

    <a id="_CPPv3N19bk_ble_local_keys_t2irE"></a> <a id="_CPPv2N19bk_ble_local_keys_t2irE"></a> <a id="bk_ble_local_keys_t::ir__bk_bt_octet16_t"></a> <a id="structbk__ble__local__keys__t_1a24fee66dd370ebaa026b48c6dea60412"></a> [bk\_bt\_octet16\_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") ir
    :   the 16 bits of the ir value

    <a id="_CPPv4N19bk_ble_local_keys_t2erE"></a>

    <a id="_CPPv3N19bk_ble_local_keys_t2erE"></a> <a id="_CPPv2N19bk_ble_local_keys_t2erE"></a> <a id="bk_ble_local_keys_t::er__bk_bt_octet16_t"></a> <a id="structbk__ble__local__keys__t_1aba187bc4f2cc8eea64b0e884c7053688"></a> [bk\_bt\_octet16\_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") er
    :   the 16 bits of the er value

    <a id="_CPPv4N19bk_ble_local_keys_t3dhkE"></a>

    <a id="_CPPv3N19bk_ble_local_keys_t3dhkE"></a> <a id="_CPPv2N19bk_ble_local_keys_t3dhkE"></a> <a id="bk_ble_local_keys_t::dhk__bk_bt_octet16_t"></a> <a id="structbk__ble__local__keys__t_1a33572f635f10dce614774bdadeb01a23"></a> [bk\_bt\_octet16\_t](#_CPPv415bk_bt_octet16_t "bk_bt_octet16_t") dhk
    :   the 16 bits of the dh key value

<a id="_CPPv418bk_ble_auth_cmpl_t"></a>

<a id="_CPPv318bk_ble_auth_cmpl_t"></a> <a id="_CPPv218bk_ble_auth_cmpl_t"></a> <a id="bk_ble_auth_cmpl_t"></a> <a id="structbk__ble__auth__cmpl__t"></a> struct bk\_ble\_auth\_cmpl\_t
:   Structure associated with BK\_AUTH\_CMPL\_EVT.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_ble_auth_cmpl_t7bd_addrE"></a>

    <a id="_CPPv3N18bk_ble_auth_cmpl_t7bd_addrE"></a> <a id="_CPPv2N18bk_ble_auth_cmpl_t7bd_addrE"></a> <a id="bk_ble_auth_cmpl_t::bd_addr__bk_bd_addr_t"></a> <a id="structbk__ble__auth__cmpl__t_1a7ef3540c6bd42efc3aa0de9fce4c885d"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
    :   BD address peer device.

    <a id="_CPPv4N18bk_ble_auth_cmpl_t7successE"></a>

    <a id="_CPPv3N18bk_ble_auth_cmpl_t7successE"></a> <a id="_CPPv2N18bk_ble_auth_cmpl_t7successE"></a> <a id="bk_ble_auth_cmpl_t::success__b"></a> <a id="structbk__ble__auth__cmpl__t_1a7982514b7031c5dd0535c7290595477e"></a> bool success
    :   TRUE of authentication succeeded, FALSE if failed.

    <a id="_CPPv4N18bk_ble_auth_cmpl_t11fail_reasonE"></a>

    <a id="_CPPv3N18bk_ble_auth_cmpl_t11fail_reasonE"></a> <a id="_CPPv2N18bk_ble_auth_cmpl_t11fail_reasonE"></a> <a id="bk_ble_auth_cmpl_t::fail_reason__uint8_t"></a> <a id="structbk__ble__auth__cmpl__t_1acdb1865e842f19bda174ad117e046500"></a> uint8\_t fail\_reason
    :   The HCI reason/error code for when success\=FALSE

    <a id="_CPPv4N18bk_ble_auth_cmpl_t9addr_typeE"></a>

    <a id="_CPPv3N18bk_ble_auth_cmpl_t9addr_typeE"></a> <a id="_CPPv2N18bk_ble_auth_cmpl_t9addr_typeE"></a> <a id="bk_ble_auth_cmpl_t::addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__auth__cmpl__t_1a8f0978f7dbfdec83b92730bce8249d29"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr\_type
    :   Peer device address type

    <a id="_CPPv4N18bk_ble_auth_cmpl_t8dev_typeE"></a>

    <a id="_CPPv3N18bk_ble_auth_cmpl_t8dev_typeE"></a> <a id="_CPPv2N18bk_ble_auth_cmpl_t8dev_typeE"></a> <a id="bk_ble_auth_cmpl_t::dev_type__bk_bt_dev_type_t"></a> <a id="structbk__ble__auth__cmpl__t_1a6d943535ac94e150e6b9fb0193d09c56"></a> [bk\_bt\_dev\_type\_t](#_CPPv416bk_bt_dev_type_t "bk_bt_dev_type_t") dev\_type
    :   Device type

    <a id="_CPPv4N18bk_ble_auth_cmpl_t9auth_modeE"></a>

    <a id="_CPPv3N18bk_ble_auth_cmpl_t9auth_modeE"></a> <a id="_CPPv2N18bk_ble_auth_cmpl_t9auth_modeE"></a> <a id="bk_ble_auth_cmpl_t::auth_mode__bk_ble_auth_req_t"></a> <a id="structbk__ble__auth__cmpl__t_1a4851d719de9e02dd6dc8088f0e707417"></a> [bk\_ble\_auth\_req\_t](#_CPPv417bk_ble_auth_req_t "bk_ble_auth_req_t") auth\_mode
    :   authentication mode

<a id="_CPPv421bk_ble_bond_key_req_t"></a>

<a id="_CPPv321bk_ble_bond_key_req_t"></a> <a id="_CPPv221bk_ble_bond_key_req_t"></a> <a id="bk_ble_bond_key_req_t"></a> <a id="structbk__ble__bond__key__req__t"></a> struct bk\_ble\_bond\_key\_req\_t

<a id="_CPPv427bk_ble_gap_ext_adv_params_t"></a>

<a id="_CPPv327bk_ble_gap_ext_adv_params_t"></a> <a id="_CPPv227bk_ble_gap_ext_adv_params_t"></a> <a id="bk_ble_gap_ext_adv_params_t"></a> <a id="structbk__ble__gap__ext__adv__params__t"></a> struct bk\_ble\_gap\_ext\_adv\_params\_t
:   ext adv parameters

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t4typeE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t4typeE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t4typeE"></a> <a id="bk_ble_gap_ext_adv_params_t::type__bk_ble_ext_adv_type_mask_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1a3bfa169f4ff5d7018ac63642a4f70940"></a> [bk\_ble\_ext\_adv\_type\_mask\_t](#_CPPv426bk_ble_ext_adv_type_mask_t "bk_ble_ext_adv_type_mask_t") type
    :   ext adv type

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t12interval_minE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t12interval_minE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t12interval_minE"></a> <a id="bk_ble_gap_ext_adv_params_t::interval_min__uint32_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1a648501316faf1b1d645f87b5b2e2f138"></a> uint32\_t interval\_min
    :   ext adv minimum interval in 0.625ms. Range: 20 ms to 10485.759375s

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t12interval_maxE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t12interval_maxE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t12interval_maxE"></a> <a id="bk_ble_gap_ext_adv_params_t::interval_max__uint32_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1aa28466fdebf75dae7b8a1c2daf104d64"></a> uint32\_t interval\_max
    :   ext adv maximum interval in 0.625ms. Range: 20 ms to 10485.759375s

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t11channel_mapE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t11channel_mapE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t11channel_mapE"></a> <a id="bk_ble_gap_ext_adv_params_t::channel_map__bk_ble_adv_channel_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1aaab83e16fcac8c6feba40fd25ed053d3"></a> [bk\_ble\_adv\_channel\_t](#_CPPv420bk_ble_adv_channel_t "bk_ble_adv_channel_t") channel\_map
    :   ext adv channel map

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t13own_addr_typeE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t13own_addr_typeE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t13own_addr_typeE"></a> <a id="bk_ble_gap_ext_adv_params_t::own_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1a5fb8b1992fd511508aae857639c2e6d2"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") own\_addr\_type
    :   ext adv own address type

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t14peer_addr_typeE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t14peer_addr_typeE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t14peer_addr_typeE"></a> <a id="bk_ble_gap_ext_adv_params_t::peer_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1ac63bfd8b025fc7bcea0f7d427f7deeff"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") peer\_addr\_type
    :   ext adv peer address type, only BLE\_ADDR\_TYPE\_PUBLIC and BLE\_ADDR\_TYPE\_RANDOM is valid

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t9peer_addrE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t9peer_addrE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t9peer_addrE"></a> <a id="bk_ble_gap_ext_adv_params_t::peer_addr__bk_bd_addr_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1a118ca4c43f72439f7d38913f59c62087"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") peer\_addr
    :   ext adv peer address

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t13filter_policyE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t13filter_policyE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t13filter_policyE"></a> <a id="bk_ble_gap_ext_adv_params_t::filter_policy__bk_ble_adv_filter_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1acf6bf7368b6133e001c265d11eb5123d"></a> [bk\_ble\_adv\_filter\_t](#_CPPv419bk_ble_adv_filter_t "bk_ble_adv_filter_t") filter\_policy
    :   ext adv filter policy

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t8tx_powerE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t8tx_powerE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t8tx_powerE"></a> <a id="bk_ble_gap_ext_adv_params_t::tx_power__int8_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1a411355316b31ed3c76923354db1d6cb1"></a> int8\_t tx\_power
    :   ext adv tx power

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t11primary_phyE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t11primary_phyE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t11primary_phyE"></a> <a id="bk_ble_gap_ext_adv_params_t::primary_phy__bk_ble_gap_pri_phy_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1a7eecb5bc21122765fc26e967eb073db1"></a> [bk\_ble\_gap\_pri\_phy\_t](#_CPPv420bk_ble_gap_pri_phy_t "bk_ble_gap_pri_phy_t") primary\_phy
    :   ext adv primary phy

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t8max_skipE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t8max_skipE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t8max_skipE"></a> <a id="bk_ble_gap_ext_adv_params_t::max_skip__uint8_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1ae59a853930e5aaedb4a274d9fb0e8cee"></a> uint8\_t max\_skip
    :   ext adv maximum skip

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t13secondary_phyE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t13secondary_phyE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t13secondary_phyE"></a> <a id="bk_ble_gap_ext_adv_params_t::secondary_phy__bk_ble_gap_phy_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1ad0e27901f5854c0df465b63fa927d80d"></a> [bk\_ble\_gap\_phy\_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") secondary\_phy
    :   ext adv secondary phy

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t3sidE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t3sidE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t3sidE"></a> <a id="bk_ble_gap_ext_adv_params_t::sid__uint8_t"></a> <a id="structbk__ble__gap__ext__adv__params__t_1ad3859f7148fa7c9fb1b92708de778c62"></a> uint8\_t sid
    :   ext adv sid

    <a id="_CPPv4N27bk_ble_gap_ext_adv_params_t14scan_req_notifE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_params_t14scan_req_notifE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_params_t14scan_req_notifE"></a> <a id="bk_ble_gap_ext_adv_params_t::scan_req_notif__b"></a> <a id="structbk__ble__gap__ext__adv__params__t_1a76496552f3ff374dc7301fb146c3fbef"></a> bool scan\_req\_notif
    :   ext adv scan request event notify

<a id="_CPPv421bk_ble_ext_scan_cfg_t"></a>

<a id="_CPPv321bk_ble_ext_scan_cfg_t"></a> <a id="_CPPv221bk_ble_ext_scan_cfg_t"></a> <a id="bk_ble_ext_scan_cfg_t"></a> <a id="structbk__ble__ext__scan__cfg__t"></a> struct bk\_ble\_ext\_scan\_cfg\_t
:   ext scan config

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21bk_ble_ext_scan_cfg_t9scan_typeE"></a>

    <a id="_CPPv3N21bk_ble_ext_scan_cfg_t9scan_typeE"></a> <a id="_CPPv2N21bk_ble_ext_scan_cfg_t9scan_typeE"></a> <a id="bk_ble_ext_scan_cfg_t::scan_type__bk_ble_scan_type_t"></a> <a id="structbk__ble__ext__scan__cfg__t_1a5934616ae056c2544c7fbbc4c6864fce"></a> [bk\_ble\_scan\_type\_t](#_CPPv418bk_ble_scan_type_t "bk_ble_scan_type_t") scan\_type
    :   ext scan type

    <a id="_CPPv4N21bk_ble_ext_scan_cfg_t13scan_intervalE"></a>

    <a id="_CPPv3N21bk_ble_ext_scan_cfg_t13scan_intervalE"></a> <a id="_CPPv2N21bk_ble_ext_scan_cfg_t13scan_intervalE"></a> <a id="bk_ble_ext_scan_cfg_t::scan_interval__uint16_t"></a> <a id="structbk__ble__ext__scan__cfg__t_1a5afeb02ae6060e05c322714ad738c102"></a> uint16\_t scan\_interval
    :   ext scan interval (in unit of 0.625ms, range: 2.5 ms to 40.959375s)

    <a id="_CPPv4N21bk_ble_ext_scan_cfg_t11scan_windowE"></a>

    <a id="_CPPv3N21bk_ble_ext_scan_cfg_t11scan_windowE"></a> <a id="_CPPv2N21bk_ble_ext_scan_cfg_t11scan_windowE"></a> <a id="bk_ble_ext_scan_cfg_t::scan_window__uint16_t"></a> <a id="structbk__ble__ext__scan__cfg__t_1ade9b4b3e46999512fd7277fa137b896a"></a> uint16\_t scan\_window
    :   ext scan window (in unit of 0.625ms, range: 2.5 ms to 40.959375s)

<a id="_CPPv424bk_ble_ext_scan_params_t"></a>

<a id="_CPPv324bk_ble_ext_scan_params_t"></a> <a id="_CPPv224bk_ble_ext_scan_params_t"></a> <a id="bk_ble_ext_scan_params_t"></a> <a id="structbk__ble__ext__scan__params__t"></a> struct bk\_ble\_ext\_scan\_params\_t
:   ext scan parameters

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N24bk_ble_ext_scan_params_t13own_addr_typeE"></a>

    <a id="_CPPv3N24bk_ble_ext_scan_params_t13own_addr_typeE"></a> <a id="_CPPv2N24bk_ble_ext_scan_params_t13own_addr_typeE"></a> <a id="bk_ble_ext_scan_params_t::own_addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__ext__scan__params__t_1afd41a841588fa163e879c87f63c202f1"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") own\_addr\_type
    :   ext scan own address type

    <a id="_CPPv4N24bk_ble_ext_scan_params_t13filter_policyE"></a>

    <a id="_CPPv3N24bk_ble_ext_scan_params_t13filter_policyE"></a> <a id="_CPPv2N24bk_ble_ext_scan_params_t13filter_policyE"></a> <a id="bk_ble_ext_scan_params_t::filter_policy__bk_ble_scan_filter_t"></a> <a id="structbk__ble__ext__scan__params__t_1aa067ba2bce93bd07c3427373bc41b4cb"></a> [bk\_ble\_scan\_filter\_t](#_CPPv420bk_ble_scan_filter_t "bk_ble_scan_filter_t") filter\_policy
    :   ext scan filter policy

    <a id="_CPPv4N24bk_ble_ext_scan_params_t14scan_duplicateE"></a>

    <a id="_CPPv3N24bk_ble_ext_scan_params_t14scan_duplicateE"></a> <a id="_CPPv2N24bk_ble_ext_scan_params_t14scan_duplicateE"></a> <a id="bk_ble_ext_scan_params_t::scan_duplicate__bk_ble_scan_duplicate_t"></a> <a id="structbk__ble__ext__scan__params__t_1a8649abcd436404e5bedbd9b33bacd133"></a> [bk\_ble\_scan\_duplicate\_t](#_CPPv423bk_ble_scan_duplicate_t "bk_ble_scan_duplicate_t") scan\_duplicate
    :   ext scan duplicate scan

    <a id="_CPPv4N24bk_ble_ext_scan_params_t8cfg_maskE"></a>

    <a id="_CPPv3N24bk_ble_ext_scan_params_t8cfg_maskE"></a> <a id="_CPPv2N24bk_ble_ext_scan_params_t8cfg_maskE"></a> <a id="bk_ble_ext_scan_params_t::cfg_mask__bk_ble_ext_scan_cfg_mask_t"></a> <a id="structbk__ble__ext__scan__params__t_1aaf978088383808f046de4d762828e441"></a> [bk\_ble\_ext\_scan\_cfg\_mask\_t](#_CPPv426bk_ble_ext_scan_cfg_mask_t "bk_ble_ext_scan_cfg_mask_t") cfg\_mask
    :   ext scan config mask

    <a id="_CPPv4N24bk_ble_ext_scan_params_t11uncoded_cfgE"></a>

    <a id="_CPPv3N24bk_ble_ext_scan_params_t11uncoded_cfgE"></a> <a id="_CPPv2N24bk_ble_ext_scan_params_t11uncoded_cfgE"></a> <a id="bk_ble_ext_scan_params_t::uncoded_cfg__bk_ble_ext_scan_cfg_t"></a> <a id="structbk__ble__ext__scan__params__t_1a86df5cf7f4d554b1828ff95408e56ef6"></a> [bk\_ble\_ext\_scan\_cfg\_t](#_CPPv421bk_ble_ext_scan_cfg_t "bk_ble_ext_scan_cfg_t") uncoded\_cfg
    :   ext scan uncoded config parameters

    <a id="_CPPv4N24bk_ble_ext_scan_params_t9coded_cfgE"></a>

    <a id="_CPPv3N24bk_ble_ext_scan_params_t9coded_cfgE"></a> <a id="_CPPv2N24bk_ble_ext_scan_params_t9coded_cfgE"></a> <a id="bk_ble_ext_scan_params_t::coded_cfg__bk_ble_ext_scan_cfg_t"></a> <a id="structbk__ble__ext__scan__params__t_1a5f2eca8dad6483b409e917198b1bcf9b"></a> [bk\_ble\_ext\_scan\_cfg\_t](#_CPPv421bk_ble_ext_scan_cfg_t "bk_ble_ext_scan_cfg_t") coded\_cfg
    :   ext scan coded config parameters

<a id="_CPPv424bk_ble_gap_conn_params_t"></a>

<a id="_CPPv324bk_ble_gap_conn_params_t"></a> <a id="_CPPv224bk_ble_gap_conn_params_t"></a> <a id="bk_ble_gap_conn_params_t"></a> <a id="structbk__ble__gap__conn__params__t"></a> struct bk\_ble\_gap\_conn\_params\_t
:   create extend connection parameters

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N24bk_ble_gap_conn_params_t13scan_intervalE"></a>

    <a id="_CPPv3N24bk_ble_gap_conn_params_t13scan_intervalE"></a> <a id="_CPPv2N24bk_ble_gap_conn_params_t13scan_intervalE"></a> <a id="bk_ble_gap_conn_params_t::scan_interval__uint16_t"></a> <a id="structbk__ble__gap__conn__params__t_1a4a739e3adbaa326c53c91032f1dd9aff"></a> uint16\_t scan\_interval
    :   init scan interval

    <a id="_CPPv4N24bk_ble_gap_conn_params_t11scan_windowE"></a>

    <a id="_CPPv3N24bk_ble_gap_conn_params_t11scan_windowE"></a> <a id="_CPPv2N24bk_ble_gap_conn_params_t11scan_windowE"></a> <a id="bk_ble_gap_conn_params_t::scan_window__uint16_t"></a> <a id="structbk__ble__gap__conn__params__t_1ae8983ac4790124043ed737255d8e3b48"></a> uint16\_t scan\_window
    :   init scan window

    <a id="_CPPv4N24bk_ble_gap_conn_params_t12interval_minE"></a>

    <a id="_CPPv3N24bk_ble_gap_conn_params_t12interval_minE"></a> <a id="_CPPv2N24bk_ble_gap_conn_params_t12interval_minE"></a> <a id="bk_ble_gap_conn_params_t::interval_min__uint16_t"></a> <a id="structbk__ble__gap__conn__params__t_1ae0c9f1e322da4af1904bb48bbbf30d6c"></a> uint16\_t interval\_min
    :   minimum interval

    <a id="_CPPv4N24bk_ble_gap_conn_params_t12interval_maxE"></a>

    <a id="_CPPv3N24bk_ble_gap_conn_params_t12interval_maxE"></a> <a id="_CPPv2N24bk_ble_gap_conn_params_t12interval_maxE"></a> <a id="bk_ble_gap_conn_params_t::interval_max__uint16_t"></a> <a id="structbk__ble__gap__conn__params__t_1a1fc1492c21250f431535037ff5573535"></a> uint16\_t interval\_max
    :   maximum interval

    <a id="_CPPv4N24bk_ble_gap_conn_params_t7latencyE"></a>

    <a id="_CPPv3N24bk_ble_gap_conn_params_t7latencyE"></a> <a id="_CPPv2N24bk_ble_gap_conn_params_t7latencyE"></a> <a id="bk_ble_gap_conn_params_t::latency__uint16_t"></a> <a id="structbk__ble__gap__conn__params__t_1a5286597c1153b65ad14495618fc87e85"></a> uint16\_t latency
    :   ext scan type

    <a id="_CPPv4N24bk_ble_gap_conn_params_t19supervision_timeoutE"></a>

    <a id="_CPPv3N24bk_ble_gap_conn_params_t19supervision_timeoutE"></a> <a id="_CPPv2N24bk_ble_gap_conn_params_t19supervision_timeoutE"></a> <a id="bk_ble_gap_conn_params_t::supervision_timeout__uint16_t"></a> <a id="structbk__ble__gap__conn__params__t_1a65f7aa2a792519c687400d7501da6c5f"></a> uint16\_t supervision\_timeout
    :   connection supervision timeout

    <a id="_CPPv4N24bk_ble_gap_conn_params_t10min_ce_lenE"></a>

    <a id="_CPPv3N24bk_ble_gap_conn_params_t10min_ce_lenE"></a> <a id="_CPPv2N24bk_ble_gap_conn_params_t10min_ce_lenE"></a> <a id="bk_ble_gap_conn_params_t::min_ce_len__uint16_t"></a> <a id="structbk__ble__gap__conn__params__t_1a65bc5be53830336e885af6df008b6d26"></a> uint16\_t min\_ce\_len
    :   minimum ce length

    <a id="_CPPv4N24bk_ble_gap_conn_params_t10max_ce_lenE"></a>

    <a id="_CPPv3N24bk_ble_gap_conn_params_t10max_ce_lenE"></a> <a id="_CPPv2N24bk_ble_gap_conn_params_t10max_ce_lenE"></a> <a id="bk_ble_gap_conn_params_t::max_ce_len__uint16_t"></a> <a id="structbk__ble__gap__conn__params__t_1a89041d25337da953ca17f6790966862f"></a> uint16\_t max\_ce\_len
    :   maximum ce length

<a id="_CPPv420bk_ble_gap_ext_adv_t"></a>

<a id="_CPPv320bk_ble_gap_ext_adv_t"></a> <a id="_CPPv220bk_ble_gap_ext_adv_t"></a> <a id="bk_ble_gap_ext_adv_t"></a> <a id="structbk__ble__gap__ext__adv__t"></a> struct bk\_ble\_gap\_ext\_adv\_t
:   extend adv enable parameters

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20bk_ble_gap_ext_adv_t8instanceE"></a>

    <a id="_CPPv3N20bk_ble_gap_ext_adv_t8instanceE"></a> <a id="_CPPv2N20bk_ble_gap_ext_adv_t8instanceE"></a> <a id="bk_ble_gap_ext_adv_t::instance__uint8_t"></a> <a id="structbk__ble__gap__ext__adv__t_1a16e019e602f609e503f3cc1fd87992bc"></a> uint8\_t instance
    :   advertising handle

    <a id="_CPPv4N20bk_ble_gap_ext_adv_t8durationE"></a>

    <a id="_CPPv3N20bk_ble_gap_ext_adv_t8durationE"></a> <a id="_CPPv2N20bk_ble_gap_ext_adv_t8durationE"></a> <a id="bk_ble_gap_ext_adv_t::duration__i"></a> <a id="structbk__ble__gap__ext__adv__t_1a72073f41b5caa4ac64d87e2c61e2ca30"></a> int duration
    :   advertising duration

    <a id="_CPPv4N20bk_ble_gap_ext_adv_t10max_eventsE"></a>

    <a id="_CPPv3N20bk_ble_gap_ext_adv_t10max_eventsE"></a> <a id="_CPPv2N20bk_ble_gap_ext_adv_t10max_eventsE"></a> <a id="bk_ble_gap_ext_adv_t::max_events__i"></a> <a id="structbk__ble__gap__ext__adv__t_1a2bdc71b77e80b3679172e343e0eb2971"></a> int max\_events
    :   maximum number of extended advertising events

<a id="_CPPv432bk_ble_gap_periodic_adv_params_t"></a>

<a id="_CPPv332bk_ble_gap_periodic_adv_params_t"></a> <a id="_CPPv232bk_ble_gap_periodic_adv_params_t"></a> <a id="bk_ble_gap_periodic_adv_params_t"></a> <a id="structbk__ble__gap__periodic__adv__params__t"></a> struct bk\_ble\_gap\_periodic\_adv\_params\_t
:   periodic adv parameters

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N32bk_ble_gap_periodic_adv_params_t12interval_minE"></a>

    <a id="_CPPv3N32bk_ble_gap_periodic_adv_params_t12interval_minE"></a> <a id="_CPPv2N32bk_ble_gap_periodic_adv_params_t12interval_minE"></a> <a id="bk_ble_gap_periodic_adv_params_t::interval_min__uint16_t"></a> <a id="structbk__ble__gap__periodic__adv__params__t_1af5c1c09af30bd4a9cb322b41f4a27d1a"></a> uint16\_t interval\_min
    :   periodic advertising minimum interval

    <a id="_CPPv4N32bk_ble_gap_periodic_adv_params_t12interval_maxE"></a>

    <a id="_CPPv3N32bk_ble_gap_periodic_adv_params_t12interval_maxE"></a> <a id="_CPPv2N32bk_ble_gap_periodic_adv_params_t12interval_maxE"></a> <a id="bk_ble_gap_periodic_adv_params_t::interval_max__uint16_t"></a> <a id="structbk__ble__gap__periodic__adv__params__t_1aefc163a3c8bc2bb029728ae34664ec4a"></a> uint16\_t interval\_max
    :   periodic advertising maximum interval

    <a id="_CPPv4N32bk_ble_gap_periodic_adv_params_t10propertiesE"></a>

    <a id="_CPPv3N32bk_ble_gap_periodic_adv_params_t10propertiesE"></a> <a id="_CPPv2N32bk_ble_gap_periodic_adv_params_t10propertiesE"></a> <a id="bk_ble_gap_periodic_adv_params_t::properties__uint8_t"></a> <a id="structbk__ble__gap__periodic__adv__params__t_1a41b0d5776cee3b88d8ca37c99ce1fa72"></a> uint8\_t properties
    :   periodic advertising properties

<a id="_CPPv437bk_ble_gap_periodic_adv_sync_params_t"></a>

<a id="_CPPv337bk_ble_gap_periodic_adv_sync_params_t"></a> <a id="_CPPv237bk_ble_gap_periodic_adv_sync_params_t"></a> <a id="bk_ble_gap_periodic_adv_sync_params_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__params__t"></a> struct bk\_ble\_gap\_periodic\_adv\_sync\_params\_t
:   periodic adv sync parameters

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N37bk_ble_gap_periodic_adv_sync_params_t13filter_policyE"></a>

    <a id="_CPPv3N37bk_ble_gap_periodic_adv_sync_params_t13filter_policyE"></a> <a id="_CPPv2N37bk_ble_gap_periodic_adv_sync_params_t13filter_policyE"></a> <a id="bk_ble_gap_periodic_adv_sync_params_t::filter_policy__bk_ble_gap_sync_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__params__t_1afb148414aabf9991435a256fe0ab5727"></a> [bk\_ble\_gap\_sync\_t](#_CPPv417bk_ble_gap_sync_t "bk_ble_gap_sync_t") filter\_policy
    :   periodic advertising sync filter policy

    <a id="_CPPv4N37bk_ble_gap_periodic_adv_sync_params_t3sidE"></a>

    <a id="_CPPv3N37bk_ble_gap_periodic_adv_sync_params_t3sidE"></a> <a id="_CPPv2N37bk_ble_gap_periodic_adv_sync_params_t3sidE"></a> <a id="bk_ble_gap_periodic_adv_sync_params_t::sid__uint8_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__params__t_1a2e2599a815a491c10cf22c967610b329"></a> uint8\_t sid
    :   periodic advertising sid

    <a id="_CPPv4N37bk_ble_gap_periodic_adv_sync_params_t9addr_typeE"></a>

    <a id="_CPPv3N37bk_ble_gap_periodic_adv_sync_params_t9addr_typeE"></a> <a id="_CPPv2N37bk_ble_gap_periodic_adv_sync_params_t9addr_typeE"></a> <a id="bk_ble_gap_periodic_adv_sync_params_t::addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__params__t_1afcf4874c9ffbcdc0e5cfb71732b7a94d"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr\_type
    :   periodic advertising address type

    <a id="_CPPv4N37bk_ble_gap_periodic_adv_sync_params_t4addrE"></a>

    <a id="_CPPv3N37bk_ble_gap_periodic_adv_sync_params_t4addrE"></a> <a id="_CPPv2N37bk_ble_gap_periodic_adv_sync_params_t4addrE"></a> <a id="bk_ble_gap_periodic_adv_sync_params_t::addr__bk_bd_addr_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__params__t_1ab6eb1bb508ab8ece5e39259185166fdd"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr
    :   periodic advertising address

    <a id="_CPPv4N37bk_ble_gap_periodic_adv_sync_params_t4skipE"></a>

    <a id="_CPPv3N37bk_ble_gap_periodic_adv_sync_params_t4skipE"></a> <a id="_CPPv2N37bk_ble_gap_periodic_adv_sync_params_t4skipE"></a> <a id="bk_ble_gap_periodic_adv_sync_params_t::skip__uint16_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__params__t_1a38f37ddd565246f79df3442e19626c41"></a> uint16\_t skip
    :   the maximum number of periodic advertising events that can be skipped

    <a id="_CPPv4N37bk_ble_gap_periodic_adv_sync_params_t12sync_timeoutE"></a>

    <a id="_CPPv3N37bk_ble_gap_periodic_adv_sync_params_t12sync_timeoutE"></a> <a id="_CPPv2N37bk_ble_gap_periodic_adv_sync_params_t12sync_timeoutE"></a> <a id="bk_ble_gap_periodic_adv_sync_params_t::sync_timeout__uint16_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__params__t_1a3cb893bc2ce882ffc6ccffa6aad863a6"></a> uint16\_t sync\_timeout
    :   synchronization timeout

<a id="_CPPv427bk_ble_gap_ext_adv_reprot_t"></a>

<a id="_CPPv327bk_ble_gap_ext_adv_reprot_t"></a> <a id="_CPPv227bk_ble_gap_ext_adv_reprot_t"></a> <a id="bk_ble_gap_ext_adv_reprot_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t"></a> struct bk\_ble\_gap\_ext\_adv\_reprot\_t
:   extend adv report parameters

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t10event_typeE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t10event_typeE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t10event_typeE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::event_type__bk_ble_gap_adv_type_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a62150aaf245b46e6f2d4650c5c90cbb8"></a> [bk\_ble\_gap\_adv\_type\_t](#_CPPv421bk_ble_gap_adv_type_t "bk_ble_gap_adv_type_t") event\_type
    :   extend advertising type

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t9addr_typeE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t9addr_typeE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t9addr_typeE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::addr_type__uint8_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a23472b38de92362f363c6792679f37b4"></a> uint8\_t addr\_type
    :   extend advertising address type

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t4addrE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t4addrE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t4addrE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::addr__bk_bd_addr_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a3590d255edaeaac70f049e722aa49441"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr
    :   extend advertising address

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t11primary_phyE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t11primary_phyE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t11primary_phyE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::primary_phy__bk_ble_gap_pri_phy_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a0ab7b3fd0fb54e0475777b051a45c9fc"></a> [bk\_ble\_gap\_pri\_phy\_t](#_CPPv420bk_ble_gap_pri_phy_t "bk_ble_gap_pri_phy_t") primary\_phy
    :   extend advertising primary phy

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t12secondly_phyE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t12secondly_phyE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t12secondly_phyE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::secondly_phy__bk_ble_gap_phy_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a6883152b525f070a7b454c70275bd4d3"></a> [bk\_ble\_gap\_phy\_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") secondly\_phy
    :   extend advertising secondary phy

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t3sidE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t3sidE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t3sidE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::sid__uint8_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a8b86aab99b279391b8cffb58813cca6a"></a> uint8\_t sid
    :   extend advertising sid

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t8tx_powerE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t8tx_powerE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t8tx_powerE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::tx_power__uint8_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a0fa2b8629fc83a0be47a6135873cc7bd"></a> uint8\_t tx\_power
    :   extend advertising tx power

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t4rssiE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t4rssiE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t4rssiE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::rssi__int8_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a6984e00aaa22754f0da0f2f4e5de103e"></a> int8\_t rssi
    :   extend advertising rssi

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t16per_adv_intervalE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t16per_adv_intervalE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t16per_adv_intervalE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::per_adv_interval__uint16_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a900d59cd7d4edea9b25922cb44760e12"></a> uint16\_t per\_adv\_interval
    :   periodic advertising interval

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t13dir_addr_typeE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t13dir_addr_typeE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t13dir_addr_typeE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::dir_addr_type__uint8_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a4571edd4f14ae6bb9056dd4919f7d72b"></a> uint8\_t dir\_addr\_type
    :   direct address type

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t8dir_addrE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t8dir_addrE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t8dir_addrE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::dir_addr__bk_bd_addr_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a705241b40f1f066f220c16b4dffb66f8"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") dir\_addr
    :   direct address

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t11data_statusE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t11data_statusE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t11data_statusE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::data_status__bk_ble_gap_ext_adv_data_status_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1a353da76c610a4caf11e4cc1ae1c1f679"></a> [bk\_ble\_gap\_ext\_adv\_data\_status\_t](#_CPPv432bk_ble_gap_ext_adv_data_status_t "bk_ble_gap_ext_adv_data_status_t") data\_status
    :   data type

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t12adv_data_lenE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t12adv_data_lenE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t12adv_data_lenE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::adv_data_len__uint8_t"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1ab819151aca34b4846c4149a1677cd18e"></a> uint8\_t adv\_data\_len
    :   extend advertising data length

    <a id="_CPPv4N27bk_ble_gap_ext_adv_reprot_t8adv_dataE"></a>

    <a id="_CPPv3N27bk_ble_gap_ext_adv_reprot_t8adv_dataE"></a> <a id="_CPPv2N27bk_ble_gap_ext_adv_reprot_t8adv_dataE"></a> <a id="bk_ble_gap_ext_adv_reprot_t::adv_data__uint8_tA"></a> <a id="structbk__ble__gap__ext__adv__reprot__t_1ac4b9d068b5ba73af1759627bdac58482"></a> uint8\_t adv\_data\[251\]
    :   extend advertising data

<a id="_CPPv432bk_ble_gap_periodic_adv_report_t"></a>

<a id="_CPPv332bk_ble_gap_periodic_adv_report_t"></a> <a id="_CPPv232bk_ble_gap_periodic_adv_report_t"></a> <a id="bk_ble_gap_periodic_adv_report_t"></a> <a id="structbk__ble__gap__periodic__adv__report__t"></a> struct bk\_ble\_gap\_periodic\_adv\_report\_t
:   periodic adv report parameters

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N32bk_ble_gap_periodic_adv_report_t11sync_handleE"></a>

    <a id="_CPPv3N32bk_ble_gap_periodic_adv_report_t11sync_handleE"></a> <a id="_CPPv2N32bk_ble_gap_periodic_adv_report_t11sync_handleE"></a> <a id="bk_ble_gap_periodic_adv_report_t::sync_handle__uint16_t"></a> <a id="structbk__ble__gap__periodic__adv__report__t_1a0380ea97bac9bff7898302ae04db5446"></a> uint16\_t sync\_handle
    :   periodic advertising train handle

    <a id="_CPPv4N32bk_ble_gap_periodic_adv_report_t8tx_powerE"></a>

    <a id="_CPPv3N32bk_ble_gap_periodic_adv_report_t8tx_powerE"></a> <a id="_CPPv2N32bk_ble_gap_periodic_adv_report_t8tx_powerE"></a> <a id="bk_ble_gap_periodic_adv_report_t::tx_power__uint8_t"></a> <a id="structbk__ble__gap__periodic__adv__report__t_1afc7501eb05285df61c1b69d0bb071294"></a> uint8\_t tx\_power
    :   periodic advertising tx power

    <a id="_CPPv4N32bk_ble_gap_periodic_adv_report_t4rssiE"></a>

    <a id="_CPPv3N32bk_ble_gap_periodic_adv_report_t4rssiE"></a> <a id="_CPPv2N32bk_ble_gap_periodic_adv_report_t4rssiE"></a> <a id="bk_ble_gap_periodic_adv_report_t::rssi__int8_t"></a> <a id="structbk__ble__gap__periodic__adv__report__t_1a9ac1d20d006a4ecae7866ccaaf78fcee"></a> int8\_t rssi
    :   periodic advertising rssi

    <a id="_CPPv4N32bk_ble_gap_periodic_adv_report_t11data_statusE"></a>

    <a id="_CPPv3N32bk_ble_gap_periodic_adv_report_t11data_statusE"></a> <a id="_CPPv2N32bk_ble_gap_periodic_adv_report_t11data_statusE"></a> <a id="bk_ble_gap_periodic_adv_report_t::data_status__bk_ble_gap_ext_adv_data_status_t"></a> <a id="structbk__ble__gap__periodic__adv__report__t_1a2e20510670bd2dfe640a5dc41109dfab"></a> [bk\_ble\_gap\_ext\_adv\_data\_status\_t](#_CPPv432bk_ble_gap_ext_adv_data_status_t "bk_ble_gap_ext_adv_data_status_t") data\_status
    :   periodic advertising data type

    <a id="_CPPv4N32bk_ble_gap_periodic_adv_report_t11data_lengthE"></a>

    <a id="_CPPv3N32bk_ble_gap_periodic_adv_report_t11data_lengthE"></a> <a id="_CPPv2N32bk_ble_gap_periodic_adv_report_t11data_lengthE"></a> <a id="bk_ble_gap_periodic_adv_report_t::data_length__uint8_t"></a> <a id="structbk__ble__gap__periodic__adv__report__t_1aaa0da2ac7473965d23bf6364601a1948"></a> uint8\_t data\_length
    :   periodic advertising data length

    <a id="_CPPv4N32bk_ble_gap_periodic_adv_report_t4dataE"></a>

    <a id="_CPPv3N32bk_ble_gap_periodic_adv_report_t4dataE"></a> <a id="_CPPv2N32bk_ble_gap_periodic_adv_report_t4dataE"></a> <a id="bk_ble_gap_periodic_adv_report_t::data__uint8_tA"></a> <a id="structbk__ble__gap__periodic__adv__report__t_1a442ad015d0b54310c53e1d4885110ac2"></a> uint8\_t data\[251\]
    :   periodic advertising data

<a id="_CPPv436bk_ble_gap_periodic_adv_sync_estab_t"></a>

<a id="_CPPv336bk_ble_gap_periodic_adv_sync_estab_t"></a> <a id="_CPPv236bk_ble_gap_periodic_adv_sync_estab_t"></a> <a id="bk_ble_gap_periodic_adv_sync_estab_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__estab__t"></a> struct bk\_ble\_gap\_periodic\_adv\_sync\_estab\_t
:   perodic adv sync establish parameters

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N36bk_ble_gap_periodic_adv_sync_estab_t6statusE"></a>

    <a id="_CPPv3N36bk_ble_gap_periodic_adv_sync_estab_t6statusE"></a> <a id="_CPPv2N36bk_ble_gap_periodic_adv_sync_estab_t6statusE"></a> <a id="bk_ble_gap_periodic_adv_sync_estab_t::status__uint8_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__estab__t_1a0a3dbf660763ab0486dc822fe7b2a218"></a> uint8\_t status
    :   periodic advertising sync status

    <a id="_CPPv4N36bk_ble_gap_periodic_adv_sync_estab_t11sync_handleE"></a>

    <a id="_CPPv3N36bk_ble_gap_periodic_adv_sync_estab_t11sync_handleE"></a> <a id="_CPPv2N36bk_ble_gap_periodic_adv_sync_estab_t11sync_handleE"></a> <a id="bk_ble_gap_periodic_adv_sync_estab_t::sync_handle__uint16_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__estab__t_1ac5844688063dce8d016e3d09f077b790"></a> uint16\_t sync\_handle
    :   periodic advertising train handle

    <a id="_CPPv4N36bk_ble_gap_periodic_adv_sync_estab_t3sidE"></a>

    <a id="_CPPv3N36bk_ble_gap_periodic_adv_sync_estab_t3sidE"></a> <a id="_CPPv2N36bk_ble_gap_periodic_adv_sync_estab_t3sidE"></a> <a id="bk_ble_gap_periodic_adv_sync_estab_t::sid__uint8_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__estab__t_1ae11b7765a80b98e22feae0dffc0bc1bd"></a> uint8\_t sid
    :   periodic advertising sid

    <a id="_CPPv4N36bk_ble_gap_periodic_adv_sync_estab_t9addr_typeE"></a>

    <a id="_CPPv3N36bk_ble_gap_periodic_adv_sync_estab_t9addr_typeE"></a> <a id="_CPPv2N36bk_ble_gap_periodic_adv_sync_estab_t9addr_typeE"></a> <a id="bk_ble_gap_periodic_adv_sync_estab_t::addr_type__bk_ble_addr_type_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__estab__t_1a01e7f25b6a7400bb2ef9fbe36268a016"></a> [bk\_ble\_addr\_type\_t](#_CPPv418bk_ble_addr_type_t "bk_ble_addr_type_t") addr\_type
    :   periodic advertising address type

    <a id="_CPPv4N36bk_ble_gap_periodic_adv_sync_estab_t8adv_addrE"></a>

    <a id="_CPPv3N36bk_ble_gap_periodic_adv_sync_estab_t8adv_addrE"></a> <a id="_CPPv2N36bk_ble_gap_periodic_adv_sync_estab_t8adv_addrE"></a> <a id="bk_ble_gap_periodic_adv_sync_estab_t::adv_addr__bk_bd_addr_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__estab__t_1a194e825338e3398beaec507bac0402f9"></a> [bk\_bd\_addr\_t](#_CPPv412bk_bd_addr_t "bk_bd_addr_t") adv\_addr
    :   periodic advertising address

    <a id="_CPPv4N36bk_ble_gap_periodic_adv_sync_estab_t7adv_phyE"></a>

    <a id="_CPPv3N36bk_ble_gap_periodic_adv_sync_estab_t7adv_phyE"></a> <a id="_CPPv2N36bk_ble_gap_periodic_adv_sync_estab_t7adv_phyE"></a> <a id="bk_ble_gap_periodic_adv_sync_estab_t::adv_phy__bk_ble_gap_phy_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__estab__t_1abe2d1244710a8d8382681889308202c5"></a> [bk\_ble\_gap\_phy\_t](#_CPPv416bk_ble_gap_phy_t "bk_ble_gap_phy_t") adv\_phy
    :   periodic advertising adv phy type

    <a id="_CPPv4N36bk_ble_gap_periodic_adv_sync_estab_t19period_adv_intervalE"></a>

    <a id="_CPPv3N36bk_ble_gap_periodic_adv_sync_estab_t19period_adv_intervalE"></a> <a id="_CPPv2N36bk_ble_gap_periodic_adv_sync_estab_t19period_adv_intervalE"></a> <a id="bk_ble_gap_periodic_adv_sync_estab_t::period_adv_interval__uint16_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__estab__t_1a29789b1fd1a9e258a84562a473830506"></a> uint16\_t period\_adv\_interval
    :   periodic advertising interval

    <a id="_CPPv4N36bk_ble_gap_periodic_adv_sync_estab_t16adv_clk_accuracyE"></a>

    <a id="_CPPv3N36bk_ble_gap_periodic_adv_sync_estab_t16adv_clk_accuracyE"></a> <a id="_CPPv2N36bk_ble_gap_periodic_adv_sync_estab_t16adv_clk_accuracyE"></a> <a id="bk_ble_gap_periodic_adv_sync_estab_t::adv_clk_accuracy__uint8_t"></a> <a id="structbk__ble__gap__periodic__adv__sync__estab__t_1ab23e4fd8f028dae4b106a250064e86fe"></a> uint8\_t adv\_clk\_accuracy
    :   periodic advertising clock accuracy

<a id="id16"></a>

### Macros

<a id="c.BK_BLE_KEY_TRANSPORT_NONE"></a>

<a id="group__dm__gap__defines__v1_1ga599950632659878ddf1cb83f5fffcb49"></a> BK\_BLE\_KEY\_TRANSPORT\_NONE
:   Transport on which the key-generation procedure originated.

<a id="c.BK_BLE_KEY_TRANSPORT_BR_EDR"></a>

<a id="group__dm__gap__defines__v1_1ga3bf4c1bdfc1ebc2dd97586c6b5e1a5f0"></a> BK\_BLE\_KEY\_TRANSPORT\_BR\_EDR

<a id="c.BK_BLE_KEY_TRANSPORT_LE"></a>

<a id="group__dm__gap__defines__v1_1gaebcd43b4b43666f8448a0468e09453af"></a> BK\_BLE\_KEY\_TRANSPORT\_LE

<a id="c.BK_BLE_ONLY_ACCEPT_SPECIFIED_AUTH_DISABLE"></a>

<a id="group__dm__gap__defines__v1_1ga7d8d4528fc154551cb1ad406a81f620e"></a> BK\_BLE\_ONLY\_ACCEPT\_SPECIFIED\_AUTH\_DISABLE
:   authentication disable

<a id="c.BK_BLE_ONLY_ACCEPT_SPECIFIED_AUTH_ENABLE"></a>

<a id="group__dm__gap__defines__v1_1gafa5715c8f3168d5d3c166f3d1a2b3ce9"></a> BK\_BLE\_ONLY\_ACCEPT\_SPECIFIED\_AUTH\_ENABLE
:   authentication enable

<a id="c.BK_BLE_GAP_CHANNELS_LEN"></a>

<a id="group__dm__gap__defines__v1_1ga99ccf003538b852c70db447a0200a1ef"></a> BK\_BLE\_GAP\_CHANNELS\_LEN
:   channel length

<a id="c.BK_BLE_ADV_DATA_LEN_MAX"></a>

<a id="group__dm__gap__defines__v1_1ga090a5147417316db7820bf14093241ae"></a> BK\_BLE\_ADV\_DATA\_LEN\_MAX
:   Advertising data maximum length.

<a id="c.BK_BLE_SCAN_RSP_DATA_LEN_MAX"></a>

<a id="group__dm__gap__defines__v1_1ga0fb427d8e5783d0d2204ed7744091c32"></a> BK\_BLE\_SCAN\_RSP\_DATA\_LEN\_MAX
:   Scan response data maximum length.

<a id="c.BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_IND"></a>

<a id="group__dm__gap__defines__v1_1ga259fcf06a521a71d192c5df8254e1e2e"></a> BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_LEGACY\_IND
:   ADV\_DIRECT\_IND (low duty cycle)

<a id="c.BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_LD_DIR"></a>

<a id="group__dm__gap__defines__v1_1gaa07adec2f201429a55641cbbb6825db4"></a> BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_LEGACY\_LD\_DIR
:   ADV\_DIRECT\_IND (high duty cycle)

<a id="c.BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_HD_DIR"></a>

<a id="group__dm__gap__defines__v1_1gad342dc672a26e21b447ea497b1179cae"></a> BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_LEGACY\_HD\_DIR
:   ADV\_SCAN\_IND

<a id="c.BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_SCAN"></a>

<a id="group__dm__gap__defines__v1_1gac70bf604a257cb4755ba2ae4e0b16494"></a> BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_LEGACY\_SCAN
:   ADV\_NONCONN\_IND

<a id="c.BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_NONCONN"></a>

<a id="group__dm__gap__defines__v1_1ga7f5ef4eba094d8b5f841115ab6535971"></a> BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_LEGACY\_NONCONN

<a id="c.EXT_ADV_TX_PWR_NO_PREFERENCE"></a>

<a id="group__dm__gap__defines__v1_1ga6a312234a6453d0b1bd9de4d08afc75d"></a> EXT\_ADV\_TX\_PWR\_NO\_PREFERENCE
:   Extend advertising tx power, range: \[-127, \+126\] dBm.

    host has no preference for tx power

<a id="id17"></a>

### Type Definitions

<a id="_CPPv417bk_ble_key_type_t"></a>

<a id="_CPPv317bk_ble_key_type_t"></a> <a id="_CPPv217bk_ble_key_type_t"></a> <a id="bk_ble_key_type_t"></a> <a id="group__dm__gap__defines__v1_1ga586b99344508d13fa960365a7085bfa6"></a> typedef uint8\_t bk\_ble\_key\_type\_t
:   see bk\_le\_key\_enum\_t

<a id="_CPPv417bk_ble_key_mask_t"></a>

<a id="_CPPv317bk_ble_key_mask_t"></a> <a id="_CPPv217bk_ble_key_mask_t"></a> <a id="bk_ble_key_mask_t"></a> <a id="group__dm__gap__defines__v1_1gaaaa5d37e19787e86d0730088821be72a"></a> typedef uint8\_t bk\_ble\_key\_mask\_t
:   see bk\_le\_key\_enum\_t

<a id="_CPPv422bk_ble_key_transport_t"></a>

<a id="_CPPv322bk_ble_key_transport_t"></a> <a id="_CPPv222bk_ble_key_transport_t"></a> <a id="bk_ble_key_transport_t"></a> <a id="group__dm__gap__defines__v1_1ga7e744a5fc7bac4969bef27f3691a2463"></a> typedef uint8\_t bk\_ble\_key\_transport\_t

<a id="_CPPv417bk_ble_auth_req_t"></a>

<a id="_CPPv317bk_ble_auth_req_t"></a> <a id="_CPPv217bk_ble_auth_req_t"></a> <a id="bk_ble_auth_req_t"></a> <a id="group__dm__gap__defines__v1_1ga703c088045326930fd60269e51ee53f6"></a> typedef uint8\_t bk\_ble\_auth\_req\_t
:   see bk\_le\_auth\_enum\_t

<a id="_CPPv419bk_ble_gap_channels"></a>

<a id="_CPPv319bk_ble_gap_channels"></a> <a id="_CPPv219bk_ble_gap_channels"></a> <a id="bk_ble_gap_channels"></a> <a id="group__dm__gap__defines__v1_1gae2d393c70867635101cced131d11968a"></a> typedef uint8\_t bk\_ble\_gap\_channels\[BK\_BLE\_GAP\_CHANNELS\_LEN\]

<a id="_CPPv426bk_ble_ext_adv_type_mask_t"></a>

<a id="_CPPv326bk_ble_ext_adv_type_mask_t"></a> <a id="_CPPv226bk_ble_ext_adv_type_mask_t"></a> <a id="bk_ble_ext_adv_type_mask_t"></a> <a id="group__dm__gap__defines__v1_1gadef651a1d7c9a031dca5b5a15cbf9f2e"></a> typedef uint16\_t bk\_ble\_ext\_adv\_type\_mask\_t
:   such as BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_CONNECTABLE and BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_LEGACY\_IND

<a id="_CPPv416bk_ble_gap_phy_t"></a>

<a id="_CPPv316bk_ble_gap_phy_t"></a> <a id="_CPPv216bk_ble_gap_phy_t"></a> <a id="bk_ble_gap_phy_t"></a> <a id="group__dm__gap__defines__v1_1gad6fb3899a3833b89d11b49770e1579bd"></a> typedef uint8\_t bk\_ble\_gap\_phy\_t
:   see bk\_ble\_gap\_phy\_enum\_t

<a id="_CPPv421bk_ble_gap_all_phys_t"></a>

<a id="_CPPv321bk_ble_gap_all_phys_t"></a> <a id="_CPPv221bk_ble_gap_all_phys_t"></a> <a id="bk_ble_gap_all_phys_t"></a> <a id="group__dm__gap__defines__v1_1ga0a88420fece17524acec6b2edd46cc02"></a> typedef uint8\_t bk\_ble\_gap\_all\_phys\_t

<a id="_CPPv420bk_ble_gap_pri_phy_t"></a>

<a id="_CPPv320bk_ble_gap_pri_phy_t"></a> <a id="_CPPv220bk_ble_gap_pri_phy_t"></a> <a id="bk_ble_gap_pri_phy_t"></a> <a id="group__dm__gap__defines__v1_1ga8b846d0cc745557aec4d0a57be0c62b8"></a> typedef uint8\_t bk\_ble\_gap\_pri\_phy\_t
:   see bk\_ble\_gap\_pri\_phy\_enum\_t

<a id="_CPPv421bk_ble_gap_phy_mask_t"></a>

<a id="_CPPv321bk_ble_gap_phy_mask_t"></a> <a id="_CPPv221bk_ble_gap_phy_mask_t"></a> <a id="bk_ble_gap_phy_mask_t"></a> <a id="group__dm__gap__defines__v1_1gaee78668d0e5d040d5b230c2ad2dec6a3"></a> typedef uint8\_t bk\_ble\_gap\_phy\_mask\_t
:   see bk\_ble\_gap\_phy\_pref\_enum\_t

<a id="_CPPv431bk_ble_gap_prefer_phy_options_t"></a>

<a id="_CPPv331bk_ble_gap_prefer_phy_options_t"></a> <a id="_CPPv231bk_ble_gap_prefer_phy_options_t"></a> <a id="bk_ble_gap_prefer_phy_options_t"></a> <a id="group__dm__gap__defines__v1_1ga0b6dd202bcd1b8b3d5b5f848072e5f88"></a> typedef uint16\_t bk\_ble\_gap\_prefer\_phy\_options\_t
:   see bk\_ble\_gap\_coded\_phy\_pref\_enum\_t

<a id="_CPPv426bk_ble_ext_scan_cfg_mask_t"></a>

<a id="_CPPv326bk_ble_ext_scan_cfg_mask_t"></a> <a id="_CPPv226bk_ble_ext_scan_cfg_mask_t"></a> <a id="bk_ble_ext_scan_cfg_mask_t"></a> <a id="group__dm__gap__defines__v1_1ga04e5fbe241d414fabd522e21afb2408e"></a> typedef uint8\_t bk\_ble\_ext\_scan\_cfg\_mask\_t
:   see bk\_ble\_gap\_ext\_scan\_cfg\_enum\_t

<a id="_CPPv432bk_ble_gap_ext_adv_data_status_t"></a>

<a id="_CPPv332bk_ble_gap_ext_adv_data_status_t"></a> <a id="_CPPv232bk_ble_gap_ext_adv_data_status_t"></a> <a id="bk_ble_gap_ext_adv_data_status_t"></a> <a id="group__dm__gap__defines__v1_1ga7d4bf781a7fea3f1bfb96bfac5ca9c40"></a> typedef uint8\_t bk\_ble\_gap\_ext\_adv\_data\_status\_t
:   see bk\_ble\_gap\_ext\_adv\_data\_seg\_enum\_t

<a id="_CPPv417bk_ble_gap_sync_t"></a>

<a id="_CPPv317bk_ble_gap_sync_t"></a> <a id="_CPPv217bk_ble_gap_sync_t"></a> <a id="bk_ble_gap_sync_t"></a> <a id="group__dm__gap__defines__v1_1ga72e13af0ff23f699276a68453792554d"></a> typedef uint8\_t bk\_ble\_gap\_sync\_t
:   see bk\_ble\_gap\_sync\_policy\_enum\_t

<a id="_CPPv421bk_ble_gap_adv_type_t"></a>

<a id="_CPPv321bk_ble_gap_adv_type_t"></a> <a id="_CPPv221bk_ble_gap_adv_type_t"></a> <a id="bk_ble_gap_adv_type_t"></a> <a id="group__dm__gap__defines__v1_1gaf1cb21d3be61c8f21285dee39621510c"></a> typedef uint8\_t bk\_ble\_gap\_adv\_type\_t
:   see bk\_ble\_adv\_report\_ext\_type\_enum\_t

<a id="_CPPv415bk_ble_gap_cb_t"></a>

<a id="_CPPv315bk_ble_gap_cb_t"></a> <a id="_CPPv215bk_ble_gap_cb_t"></a> <a id="bk_ble_gap_cb_t"></a> <a id="group__dm__gap__defines__v1_1gaaa35a4b81a39782b854d008c17293dd3"></a> typedef void (\*bk\_ble\_gap\_cb\_t)([bk\_ble\_gap\_cb\_event\_t](#_CPPv421bk_ble_gap_cb_event_t "bk_ble_gap_cb_event_t") event, [bk\_ble\_gap\_cb\_param\_t](#_CPPv421bk_ble_gap_cb_param_t "bk_ble_gap_cb_param_t") \*param)
:   GAP callback function type, todo: modify docx.

    Param event
    :   : Event type

    Param param
    :   : Point to callback parameter, currently is union type

<a id="id18"></a>

### Enumerations

<a id="_CPPv416bk_le_key_enum_t"></a>

<a id="_CPPv316bk_le_key_enum_t"></a> <a id="_CPPv216bk_le_key_enum_t"></a> <a id="group__dm__gap__defines__v1_1ga51744320580f2fcfed2d874d35cb3929"></a> enum bk\_le\_key\_enum\_t
:   *Values:*

    <a id="_CPPv4N16bk_le_key_enum_t14BK_LE_KEY_NONEE"></a>

    <a id="_CPPv3N16bk_le_key_enum_t14BK_LE_KEY_NONEE"></a> <a id="_CPPv2N16bk_le_key_enum_t14BK_LE_KEY_NONEE"></a> <a id="group__dm__gap__defines__v1_1gga51744320580f2fcfed2d874d35cb3929ac10950408135426cde63dad851e3d01d"></a> enumerator BK\_LE\_KEY\_NONE
    :   No encryption key

    <a id="_CPPv4N16bk_le_key_enum_t14BK_LE_KEY_PENCE"></a>

    <a id="_CPPv3N16bk_le_key_enum_t14BK_LE_KEY_PENCE"></a> <a id="_CPPv2N16bk_le_key_enum_t14BK_LE_KEY_PENCE"></a> <a id="group__dm__gap__defines__v1_1gga51744320580f2fcfed2d874d35cb3929aede973189261709e7508e643a2233625"></a> enumerator BK\_LE\_KEY\_PENC
    :   encryption key, encryption information of peer device

    <a id="_CPPv4N16bk_le_key_enum_t13BK_LE_KEY_PIDE"></a>

    <a id="_CPPv3N16bk_le_key_enum_t13BK_LE_KEY_PIDE"></a> <a id="_CPPv2N16bk_le_key_enum_t13BK_LE_KEY_PIDE"></a> <a id="group__dm__gap__defines__v1_1gga51744320580f2fcfed2d874d35cb3929a99fdd185b8756a3894c9363078cf8b28"></a> enumerator BK\_LE\_KEY\_PID
    :   identity key of the peer device

    <a id="_CPPv4N16bk_le_key_enum_t15BK_LE_KEY_PCSRKE"></a>

    <a id="_CPPv3N16bk_le_key_enum_t15BK_LE_KEY_PCSRKE"></a> <a id="_CPPv2N16bk_le_key_enum_t15BK_LE_KEY_PCSRKE"></a> <a id="group__dm__gap__defines__v1_1gga51744320580f2fcfed2d874d35cb3929a21661d347d29721d46657247082ad847"></a> enumerator BK\_LE\_KEY\_PCSRK
    :   peer SRK

    <a id="_CPPv4N16bk_le_key_enum_t13BK_LE_KEY_PLKE"></a>

    <a id="_CPPv3N16bk_le_key_enum_t13BK_LE_KEY_PLKE"></a> <a id="_CPPv2N16bk_le_key_enum_t13BK_LE_KEY_PLKE"></a> <a id="group__dm__gap__defines__v1_1gga51744320580f2fcfed2d874d35cb3929a64da09f562f679a0446e4da20f4df683"></a> enumerator BK\_LE\_KEY\_PLK
    :   Link key

    <a id="_CPPv4N16bk_le_key_enum_t13BK_LE_KEY_LLKE"></a>

    <a id="_CPPv3N16bk_le_key_enum_t13BK_LE_KEY_LLKE"></a> <a id="_CPPv2N16bk_le_key_enum_t13BK_LE_KEY_LLKE"></a> <a id="group__dm__gap__defines__v1_1gga51744320580f2fcfed2d874d35cb3929a1bb58b17370ffcec0c884ebb4de3f3ab"></a> enumerator BK\_LE\_KEY\_LLK
    :   link key

    <a id="_CPPv4N16bk_le_key_enum_t14BK_LE_KEY_LENCE"></a>

    <a id="_CPPv3N16bk_le_key_enum_t14BK_LE_KEY_LENCE"></a> <a id="_CPPv2N16bk_le_key_enum_t14BK_LE_KEY_LENCE"></a> <a id="group__dm__gap__defines__v1_1gga51744320580f2fcfed2d874d35cb3929a08eb83fbd8c2e85d9075111c5ca68dab"></a> enumerator BK\_LE\_KEY\_LENC
    :   master role security information:div

    <a id="_CPPv4N16bk_le_key_enum_t13BK_LE_KEY_LIDE"></a>

    <a id="_CPPv3N16bk_le_key_enum_t13BK_LE_KEY_LIDE"></a> <a id="_CPPv2N16bk_le_key_enum_t13BK_LE_KEY_LIDE"></a> <a id="group__dm__gap__defines__v1_1gga51744320580f2fcfed2d874d35cb3929a69f539e23cdb27465f0844a119682e92"></a> enumerator BK\_LE\_KEY\_LID
    :   master device ID key

    <a id="_CPPv4N16bk_le_key_enum_t15BK_LE_KEY_LCSRKE"></a>

    <a id="_CPPv3N16bk_le_key_enum_t15BK_LE_KEY_LCSRKE"></a> <a id="_CPPv2N16bk_le_key_enum_t15BK_LE_KEY_LCSRKE"></a> <a id="group__dm__gap__defines__v1_1gga51744320580f2fcfed2d874d35cb3929afd22bfbece5c5cfdcb3430b54b788c12"></a> enumerator BK\_LE\_KEY\_LCSRK
    :   local CSRK has been deliver to peer

<a id="_CPPv417bk_le_auth_enum_t"></a>

<a id="_CPPv317bk_le_auth_enum_t"></a> <a id="_CPPv217bk_le_auth_enum_t"></a> <a id="group__dm__gap__defines__v1_1ga5dbad5ffce58000457970d71a3a502e9"></a> enum bk\_le\_auth\_enum\_t
:   *Values:*

    <a id="_CPPv4N17bk_le_auth_enum_t18BK_LE_AUTH_NO_BONDE"></a>

    <a id="_CPPv3N17bk_le_auth_enum_t18BK_LE_AUTH_NO_BONDE"></a> <a id="_CPPv2N17bk_le_auth_enum_t18BK_LE_AUTH_NO_BONDE"></a> <a id="group__dm__gap__defines__v1_1gga5dbad5ffce58000457970d71a3a502e9ae48895cba4a187e22e196fbf8bcc9663"></a> enumerator BK\_LE\_AUTH\_NO\_BOND
    :   0 no bondingv

    <a id="_CPPv4N17bk_le_auth_enum_t15BK_LE_AUTH_BONDE"></a>

    <a id="_CPPv3N17bk_le_auth_enum_t15BK_LE_AUTH_BONDE"></a> <a id="_CPPv2N17bk_le_auth_enum_t15BK_LE_AUTH_BONDE"></a> <a id="group__dm__gap__defines__v1_1gga5dbad5ffce58000457970d71a3a502e9a94fc3c8212f5e850c0120cdd6e3685f9"></a> enumerator BK\_LE\_AUTH\_BOND
    :   1 \<\< 0 device in the bonding with peer

    <a id="_CPPv4N17bk_le_auth_enum_t19BK_LE_AUTH_REQ_MITME"></a>

    <a id="_CPPv3N17bk_le_auth_enum_t19BK_LE_AUTH_REQ_MITME"></a> <a id="_CPPv2N17bk_le_auth_enum_t19BK_LE_AUTH_REQ_MITME"></a> <a id="group__dm__gap__defines__v1_1gga5dbad5ffce58000457970d71a3a502e9adb5e98d1652f10555e7757aa49cacfd3"></a> enumerator BK\_LE\_AUTH\_REQ\_MITM
    :   1 \<\< 2 man in the middle attack

    <a id="_CPPv4N17bk_le_auth_enum_t24BK_LE_AUTH_REQ_BOND_MITME"></a>

    <a id="_CPPv3N17bk_le_auth_enum_t24BK_LE_AUTH_REQ_BOND_MITME"></a> <a id="_CPPv2N17bk_le_auth_enum_t24BK_LE_AUTH_REQ_BOND_MITME"></a> <a id="group__dm__gap__defines__v1_1gga5dbad5ffce58000457970d71a3a502e9af2f66917e966388a3ae7d557414dd4b4"></a> enumerator BK\_LE\_AUTH\_REQ\_BOND\_MITM
    :   0101 banding with man in the middle attack

    <a id="_CPPv4N17bk_le_auth_enum_t22BK_LE_AUTH_REQ_SC_ONLYE"></a>

    <a id="_CPPv3N17bk_le_auth_enum_t22BK_LE_AUTH_REQ_SC_ONLYE"></a> <a id="_CPPv2N17bk_le_auth_enum_t22BK_LE_AUTH_REQ_SC_ONLYE"></a> <a id="group__dm__gap__defines__v1_1gga5dbad5ffce58000457970d71a3a502e9a37566a5122e0af7c49987128e2e4a7cf"></a> enumerator BK\_LE\_AUTH\_REQ\_SC\_ONLY
    :   1 \<\< 3 secure connection

    <a id="_CPPv4N17bk_le_auth_enum_t22BK_LE_AUTH_REQ_SC_BONDE"></a>

    <a id="_CPPv3N17bk_le_auth_enum_t22BK_LE_AUTH_REQ_SC_BONDE"></a> <a id="_CPPv2N17bk_le_auth_enum_t22BK_LE_AUTH_REQ_SC_BONDE"></a> <a id="group__dm__gap__defines__v1_1gga5dbad5ffce58000457970d71a3a502e9a6aa85e589706acd0848ce93cb6be48bc"></a> enumerator BK\_LE\_AUTH\_REQ\_SC\_BOND
    :   1001 secure connection with band

    <a id="_CPPv4N17bk_le_auth_enum_t22BK_LE_AUTH_REQ_SC_MITME"></a>

    <a id="_CPPv3N17bk_le_auth_enum_t22BK_LE_AUTH_REQ_SC_MITME"></a> <a id="_CPPv2N17bk_le_auth_enum_t22BK_LE_AUTH_REQ_SC_MITME"></a> <a id="group__dm__gap__defines__v1_1gga5dbad5ffce58000457970d71a3a502e9a39cd1b8c0c7d9680694a4d77810fee4e"></a> enumerator BK\_LE\_AUTH\_REQ\_SC\_MITM
    :   1100 secure conn with MITM

    <a id="_CPPv4N17bk_le_auth_enum_t27BK_LE_AUTH_REQ_SC_MITM_BONDE"></a>

    <a id="_CPPv3N17bk_le_auth_enum_t27BK_LE_AUTH_REQ_SC_MITM_BONDE"></a> <a id="_CPPv2N17bk_le_auth_enum_t27BK_LE_AUTH_REQ_SC_MITM_BONDE"></a> <a id="group__dm__gap__defines__v1_1gga5dbad5ffce58000457970d71a3a502e9a5c1603b430d06a7b7a65c8d054eafcb7"></a> enumerator BK\_LE\_AUTH\_REQ\_SC\_MITM\_BOND
    :   1101 SC with MITM and Bonding

<a id="_CPPv416bk_io_cap_enum_t"></a>

<a id="_CPPv316bk_io_cap_enum_t"></a> <a id="_CPPv216bk_io_cap_enum_t"></a> <a id="group__dm__gap__defines__v1_1ga72ea5d7bd4ba11823fa08cfde8383d90"></a> enum bk\_io\_cap\_enum\_t
:   IO capability.

    *Values:*

    <a id="_CPPv4N16bk_io_cap_enum_t22BK_IO_CAP_DISPLAY_ONLYE"></a>

    <a id="_CPPv3N16bk_io_cap_enum_t22BK_IO_CAP_DISPLAY_ONLYE"></a> <a id="_CPPv2N16bk_io_cap_enum_t22BK_IO_CAP_DISPLAY_ONLYE"></a> <a id="group__dm__gap__defines__v1_1gga72ea5d7bd4ba11823fa08cfde8383d90a5fba1776e50f60f208367a155f43ae8f"></a> enumerator BK\_IO\_CAP\_DISPLAY\_ONLY
    :   output: display, input: none

    <a id="_CPPv4N16bk_io_cap_enum_t23BK_IO_CAP_DISPLAY_YESNOE"></a>

    <a id="_CPPv3N16bk_io_cap_enum_t23BK_IO_CAP_DISPLAY_YESNOE"></a> <a id="_CPPv2N16bk_io_cap_enum_t23BK_IO_CAP_DISPLAY_YESNOE"></a> <a id="group__dm__gap__defines__v1_1gga72ea5d7bd4ba11823fa08cfde8383d90a3b0eae4672a7cbde8aec06974ede8d5b"></a> enumerator BK\_IO\_CAP\_DISPLAY\_YESNO
    :   output: display, input: yes or no

    <a id="_CPPv4N16bk_io_cap_enum_t23BK_IO_CAP_KEYBOARD_ONLYE"></a>

    <a id="_CPPv3N16bk_io_cap_enum_t23BK_IO_CAP_KEYBOARD_ONLYE"></a> <a id="_CPPv2N16bk_io_cap_enum_t23BK_IO_CAP_KEYBOARD_ONLYE"></a> <a id="group__dm__gap__defines__v1_1gga72ea5d7bd4ba11823fa08cfde8383d90a06eae22e0773f53971314013750e989d"></a> enumerator BK\_IO\_CAP\_KEYBOARD\_ONLY
    :   output: none, input: keyboard. note: when both local and peer are keyboard only, both side should input same passkey which negotiated in other way, such as oral speak

    <a id="_CPPv4N16bk_io_cap_enum_t14BK_IO_CAP_NONEE"></a>

    <a id="_CPPv3N16bk_io_cap_enum_t14BK_IO_CAP_NONEE"></a> <a id="_CPPv2N16bk_io_cap_enum_t14BK_IO_CAP_NONEE"></a> <a id="group__dm__gap__defines__v1_1gga72ea5d7bd4ba11823fa08cfde8383d90a5430cd3a6da726c08ba93f78fad7ecba"></a> enumerator BK\_IO\_CAP\_NONE
    :   NoInputNoOutput

    <a id="_CPPv4N16bk_io_cap_enum_t26BK_IO_CAP_KEYBOARD_DISPLAYE"></a>

    <a id="_CPPv3N16bk_io_cap_enum_t26BK_IO_CAP_KEYBOARD_DISPLAYE"></a> <a id="_CPPv2N16bk_io_cap_enum_t26BK_IO_CAP_KEYBOARD_DISPLAYE"></a> <a id="group__dm__gap__defines__v1_1gga72ea5d7bd4ba11823fa08cfde8383d90a4f5e9f3fcb0f568f2e407820de7836a0"></a> enumerator BK\_IO\_CAP\_KEYBOARD\_DISPLAY
    :   output: display, input: keyboard

<a id="_CPPv421bk_ble_gap_cb_event_t"></a>

<a id="_CPPv321bk_ble_gap_cb_event_t"></a> <a id="_CPPv221bk_ble_gap_cb_event_t"></a> <a id="group__dm__gap__defines__v1_1gace9462d6a5ecd73deb995f8dcaf075b2"></a> enum bk\_ble\_gap\_cb\_event\_t
:   GAP BLE callback event type.

    *Values:*

    <a id="_CPPv4N21bk_ble_gap_cb_event_t36BK_BLE_GAP_ADV_DATA_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t36BK_BLE_GAP_ADV_DATA_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t36BK_BLE_GAP_ADV_DATA_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a8ee427e1dd3eef6fef5f569a61139747"></a> enumerator BK\_BLE\_GAP\_ADV\_DATA\_SET\_COMPLETE\_EVT
    :   When advertising data set complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t41BK_BLE_GAP_SCAN_RSP_DATA_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t41BK_BLE_GAP_SCAN_RSP_DATA_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t41BK_BLE_GAP_SCAN_RSP_DATA_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ad69fb16802f5eb118bca452acbf428fc"></a> enumerator BK\_BLE\_GAP\_SCAN\_RSP\_DATA\_SET\_COMPLETE\_EVT
    :   When scan response data set complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t38BK_BLE_GAP_SCAN_PARAM_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t38BK_BLE_GAP_SCAN_PARAM_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t38BK_BLE_GAP_SCAN_PARAM_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a1c95815b42627ad86a16f660fbdae606"></a> enumerator BK\_BLE\_GAP\_SCAN\_PARAM\_SET\_COMPLETE\_EVT
    :   When scan parameters set complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t26BK_BLE_GAP_SCAN_RESULT_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t26BK_BLE_GAP_SCAN_RESULT_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t26BK_BLE_GAP_SCAN_RESULT_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2aba932610a9f5bd09057e0a0571fdf4df"></a> enumerator BK\_BLE\_GAP\_SCAN\_RESULT\_EVT
    :   When one scan result ready, the event comes each time

    <a id="_CPPv4N21bk_ble_gap_cb_event_t40BK_BLE_GAP_ADV_DATA_RAW_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t40BK_BLE_GAP_ADV_DATA_RAW_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t40BK_BLE_GAP_ADV_DATA_RAW_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ad08c64864f74e6e419b8577cae42ad62"></a> enumerator BK\_BLE\_GAP\_ADV\_DATA\_RAW\_SET\_COMPLETE\_EVT
    :   When raw advertising data set complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t45BK_BLE_GAP_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t45BK_BLE_GAP_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t45BK_BLE_GAP_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2adb588f66fbad8c44c5fdd9a85dfb0657"></a> enumerator BK\_BLE\_GAP\_SCAN\_RSP\_DATA\_RAW\_SET\_COMPLETE\_EVT
    :   When raw advertising data set complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t33BK_BLE_GAP_ADV_START_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t33BK_BLE_GAP_ADV_START_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t33BK_BLE_GAP_ADV_START_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2aed693ef3b410afe3027f150bfc5ab764"></a> enumerator BK\_BLE\_GAP\_ADV\_START\_COMPLETE\_EVT
    :   When start advertising complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t34BK_BLE_GAP_SCAN_START_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t34BK_BLE_GAP_SCAN_START_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t34BK_BLE_GAP_SCAN_START_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a3abf8323a1f31aebd0a27055be7971d2"></a> enumerator BK\_BLE\_GAP\_SCAN\_START\_COMPLETE\_EVT
    :   When start scan complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t24BK_BLE_GAP_AUTH_CMPL_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t24BK_BLE_GAP_AUTH_CMPL_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t24BK_BLE_GAP_AUTH_CMPL_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2aec5ed410031222efb97968020221ce99"></a> enumerator BK\_BLE\_GAP\_AUTH\_CMPL\_EVT
    :   Authentication complete indication, param is [bk\_ble\_sec\_t](#unionbk__ble__sec__t).

    <a id="_CPPv4N21bk_ble_gap_cb_event_t18BK_BLE_GAP_KEY_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t18BK_BLE_GAP_KEY_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t18BK_BLE_GAP_KEY_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a0e6dc8bec4f2f397ec89f452281a1e76"></a> enumerator BK\_BLE\_GAP\_KEY\_EVT
    :   BLE key event for peer device keys, param is [bk\_ble\_sec\_t](#unionbk__ble__sec__t)

    <a id="_CPPv4N21bk_ble_gap_cb_event_t22BK_BLE_GAP_SEC_REQ_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t22BK_BLE_GAP_SEC_REQ_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t22BK_BLE_GAP_SEC_REQ_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2aa433936cb0c9e4a9c586238e287d0bde"></a> enumerator BK\_BLE\_GAP\_SEC\_REQ\_EVT
    :   BLE security request, param is [bk\_ble\_sec\_t](#unionbk__ble__sec__t).

    <a id="_CPPv4N21bk_ble_gap_cb_event_t28BK_BLE_GAP_PASSKEY_NOTIF_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t28BK_BLE_GAP_PASSKEY_NOTIF_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t28BK_BLE_GAP_PASSKEY_NOTIF_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a8e75cc4999428501409ccefa86a48c19"></a> enumerator BK\_BLE\_GAP\_PASSKEY\_NOTIF\_EVT
    :   passkey notification event, param is [bk\_ble\_sec\_t](#unionbk__ble__sec__t)

    <a id="_CPPv4N21bk_ble_gap_cb_event_t26BK_BLE_GAP_PASSKEY_REQ_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t26BK_BLE_GAP_PASSKEY_REQ_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t26BK_BLE_GAP_PASSKEY_REQ_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ade95449a2b1e89c4f501f0e9264b8cdb"></a> enumerator BK\_BLE\_GAP\_PASSKEY\_REQ\_EVT
    :   passkey request event, param is [bk\_ble\_sec\_t](#unionbk__ble__sec__t)

    <a id="_CPPv4N21bk_ble_gap_cb_event_t22BK_BLE_GAP_OOB_REQ_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t22BK_BLE_GAP_OOB_REQ_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t22BK_BLE_GAP_OOB_REQ_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2af9006a6c4992f2bbe562da809649cad8"></a> enumerator BK\_BLE\_GAP\_OOB\_REQ\_EVT
    :   OOB request event, param is [bk\_ble\_sec\_t](#unionbk__ble__sec__t)

    <a id="_CPPv4N21bk_ble_gap_cb_event_t23BK_BLE_GAP_LOCAL_IR_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t23BK_BLE_GAP_LOCAL_IR_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t23BK_BLE_GAP_LOCAL_IR_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a2001effefd53cbc3ce1785b473e0dcf4"></a> enumerator BK\_BLE\_GAP\_LOCAL\_IR\_EVT
    :   BLE local IR (Encryption Root value used to generate identity resolving key) event

    <a id="_CPPv4N21bk_ble_gap_cb_event_t23BK_BLE_GAP_LOCAL_ER_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t23BK_BLE_GAP_LOCAL_ER_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t23BK_BLE_GAP_LOCAL_ER_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a97d8914c9cdeb5b465cbd05874464d52"></a> enumerator BK\_BLE\_GAP\_LOCAL\_ER\_EVT
    :   BLE local ER (identity Root 128-bit random static value used to generate Long Term Key) event

    <a id="_CPPv4N21bk_ble_gap_cb_event_t21BK_BLE_GAP_NC_REQ_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t21BK_BLE_GAP_NC_REQ_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t21BK_BLE_GAP_NC_REQ_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ac90b9471c45ae94b52f8e1bb1aae23d8"></a> enumerator BK\_BLE\_GAP\_NC\_REQ\_EVT
    :   Numeric Comparison request event, param is [bk\_ble\_sec\_t](#unionbk__ble__sec__t)

    <a id="_CPPv4N21bk_ble_gap_cb_event_t27BK_BLE_GAP_BOND_KEY_REQ_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t27BK_BLE_GAP_BOND_KEY_REQ_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t27BK_BLE_GAP_BOND_KEY_REQ_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a3a162d28e810b1bdefeff848bc02bbf7"></a> enumerator BK\_BLE\_GAP\_BOND\_KEY\_REQ\_EVT
    :   the mapping relation of param.ble\_key.key\_type is : when BK\_LE\_KEY\_LENC, app need reply BK\_LE\_KEY\_LENC with bk\_ble\_pair\_key\_reply according compare param.ble\_key.lenc\_key

    <a id="_CPPv4N21bk_ble_gap_cb_event_t32BK_BLE_GAP_BOND_KEY_GENERATE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t32BK_BLE_GAP_BOND_KEY_GENERATE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t32BK_BLE_GAP_BOND_KEY_GENERATE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ae408cd0150fe78d52de03891f04c4d9a"></a> enumerator BK\_BLE\_GAP\_BOND\_KEY\_GENERATE\_EVT
    :   app layer should save to storage for next power on.

    <a id="_CPPv4N21bk_ble_gap_cb_event_t48BK_BLE_GAP_BOND_DEV_LIST_OPERATEION_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t48BK_BLE_GAP_BOND_DEV_LIST_OPERATEION_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t48BK_BLE_GAP_BOND_DEV_LIST_OPERATEION_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a28fa2a92accbc9cb1d10203dceed8d38"></a> enumerator BK\_BLE\_GAP\_BOND\_DEV\_LIST\_OPERATEION\_COMPLETE\_EVT

    <a id="_CPPv4N21bk_ble_gap_cb_event_t32BK_BLE_GAP_ADV_STOP_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t32BK_BLE_GAP_ADV_STOP_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t32BK_BLE_GAP_ADV_STOP_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a24d9f7e74c9259ff91595413e551fe39"></a> enumerator BK\_BLE\_GAP\_ADV\_STOP\_COMPLETE\_EVT
    :   When stop adv complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t33BK_BLE_GAP_SCAN_STOP_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t33BK_BLE_GAP_SCAN_STOP_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t33BK_BLE_GAP_SCAN_STOP_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a07486a6eaf01d464c8f5ace1a5f2e92b"></a> enumerator BK\_BLE\_GAP\_SCAN\_STOP\_COMPLETE\_EVT
    :   When stop scan complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t35BK_BLE_GAP_SET_STATIC_RAND_ADDR_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t35BK_BLE_GAP_SET_STATIC_RAND_ADDR_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t35BK_BLE_GAP_SET_STATIC_RAND_ADDR_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a4a81025ed660a6569499536ac237758c"></a> enumerator BK\_BLE\_GAP\_SET\_STATIC\_RAND\_ADDR\_EVT
    :   When set the static rand address complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t33BK_BLE_GAP_UPDATE_CONN_PARAMS_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t33BK_BLE_GAP_UPDATE_CONN_PARAMS_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t33BK_BLE_GAP_UPDATE_CONN_PARAMS_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a31c195ed10c0b6350c0e69f3bc8871c9"></a> enumerator BK\_BLE\_GAP\_UPDATE\_CONN\_PARAMS\_EVT
    :   When update connection parameters complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t38BK_BLE_GAP_SET_PKT_LENGTH_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t38BK_BLE_GAP_SET_PKT_LENGTH_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t38BK_BLE_GAP_SET_PKT_LENGTH_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a00c61f0b668c5efd32194dd680e1c63b"></a> enumerator BK\_BLE\_GAP\_SET\_PKT\_LENGTH\_COMPLETE\_EVT
    :   When set pkt length complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t41BK_BLE_GAP_SET_LOCAL_PRIVACY_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t41BK_BLE_GAP_SET_LOCAL_PRIVACY_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t41BK_BLE_GAP_SET_LOCAL_PRIVACY_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a0501380717700c1801a9f16dbd4d4c93"></a> enumerator BK\_BLE\_GAP\_SET\_LOCAL\_PRIVACY\_COMPLETE\_EVT
    :   When Enable/disable privacy on the local device complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t33BK_BLE_GAP_READ_RSSI_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t33BK_BLE_GAP_READ_RSSI_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t33BK_BLE_GAP_READ_RSSI_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a59dfad4e30a2fa4928206f7c01c54b53"></a> enumerator BK\_BLE\_GAP\_READ\_RSSI\_COMPLETE\_EVT
    :   When read the rssi complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t40BK_BLE_GAP_UPDATE_WHITELIST_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t40BK_BLE_GAP_UPDATE_WHITELIST_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t40BK_BLE_GAP_UPDATE_WHITELIST_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2acfab229889e5ca2953706efc7511f410"></a> enumerator BK\_BLE\_GAP\_UPDATE\_WHITELIST\_COMPLETE\_EVT
    :   When add or remove whitelist complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t57BK_BLE_GAP_UPDATE_DUPLICATE_EXCEPTIONAL_LIST_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t57BK_BLE_GAP_UPDATE_DUPLICATE_EXCEPTIONAL_LIST_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t57BK_BLE_GAP_UPDATE_DUPLICATE_EXCEPTIONAL_LIST_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ac7b4a5f89b55ff256e4581ac4ad5b303"></a> enumerator BK\_BLE\_GAP\_UPDATE\_DUPLICATE\_EXCEPTIONAL\_LIST\_COMPLETE\_EVT
    :   When update duplicate exceptional list complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t36BK_BLE_GAP_SET_CHANNELS_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t36BK_BLE_GAP_SET_CHANNELS_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t36BK_BLE_GAP_SET_CHANNELS_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a438dffd9cba45c093bba5755628875b2"></a> enumerator BK\_BLE\_GAP\_SET\_CHANNELS\_COMPLETE\_EVT
    :   When setting BLE channels complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t32BK_BLE_GAP_READ_PHY_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t32BK_BLE_GAP_READ_PHY_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t32BK_BLE_GAP_READ_PHY_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a6a3d7af77069b0dad0b59149fa2070a8"></a> enumerator BK\_BLE\_GAP\_READ\_PHY\_COMPLETE\_EVT
    :   when reading phy complete, this event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t49BK_BLE_GAP_SET_PREFERRED_DEFAULT_PHY_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t49BK_BLE_GAP_SET_PREFERRED_DEFAULT_PHY_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t49BK_BLE_GAP_SET_PREFERRED_DEFAULT_PHY_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a59cf24c6db966b0e88c728fc80bddd86"></a> enumerator BK\_BLE\_GAP\_SET\_PREFERRED\_DEFAULT\_PHY\_COMPLETE\_EVT
    :   when preferred default phy complete, this event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t41BK_BLE_GAP_SET_PREFERRED_PHY_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t41BK_BLE_GAP_SET_PREFERRED_PHY_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t41BK_BLE_GAP_SET_PREFERRED_PHY_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a3333711f306e5d06d50df386fbd18d53"></a> enumerator BK\_BLE\_GAP\_SET\_PREFERRED\_PHY\_COMPLETE\_EVT
    :   when preferred phy complete , this event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t45BK_BLE_GAP_EXT_ADV_SET_RAND_ADDR_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t45BK_BLE_GAP_EXT_ADV_SET_RAND_ADDR_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t45BK_BLE_GAP_EXT_ADV_SET_RAND_ADDR_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2aeced56acdbe96bca099aee0bfec0d753"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_SET\_RAND\_ADDR\_COMPLETE\_EVT
    :   when extended set random address complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t42BK_BLE_GAP_EXT_ADV_PARAMS_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t42BK_BLE_GAP_EXT_ADV_PARAMS_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t42BK_BLE_GAP_EXT_ADV_PARAMS_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ac54f4fdbb6372198b1876eb7a1184f7a"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_PARAMS\_SET\_COMPLETE\_EVT
    :   when extended advertising parameter complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t40BK_BLE_GAP_EXT_ADV_DATA_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t40BK_BLE_GAP_EXT_ADV_DATA_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t40BK_BLE_GAP_EXT_ADV_DATA_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a534101fe23138b466032fcb038c8b941"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_DATA\_SET\_COMPLETE\_EVT
    :   when extended advertising data complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t45BK_BLE_GAP_EXT_SCAN_RSP_DATA_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t45BK_BLE_GAP_EXT_SCAN_RSP_DATA_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t45BK_BLE_GAP_EXT_SCAN_RSP_DATA_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2afdb76341a4091420eb12bc1b02f7cbb1"></a> enumerator BK\_BLE\_GAP\_EXT\_SCAN\_RSP\_DATA\_SET\_COMPLETE\_EVT
    :   when extended scan response data complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t44BK_BLE_GAP_EXT_ADV_DATA_RAW_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t44BK_BLE_GAP_EXT_ADV_DATA_RAW_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t44BK_BLE_GAP_EXT_ADV_DATA_RAW_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a33edebb13d4c207ad6b57c8b742c564b"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_DATA\_RAW\_SET\_COMPLETE\_EVT
    :   when raw extended advertising data complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t49BK_BLE_GAP_EXT_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t49BK_BLE_GAP_EXT_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t49BK_BLE_GAP_EXT_SCAN_RSP_DATA_RAW_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a751b13df650570211635431215585346"></a> enumerator BK\_BLE\_GAP\_EXT\_SCAN\_RSP\_DATA\_RAW\_SET\_COMPLETE\_EVT
    :   when raw extended scan response data complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t37BK_BLE_GAP_EXT_ADV_START_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t37BK_BLE_GAP_EXT_ADV_START_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t37BK_BLE_GAP_EXT_ADV_START_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a8d2d654afa906caf57eba744e6508b2e"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_START\_COMPLETE\_EVT
    :   when extended advertising start complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t36BK_BLE_GAP_EXT_ADV_STOP_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t36BK_BLE_GAP_EXT_ADV_STOP_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t36BK_BLE_GAP_EXT_ADV_STOP_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a32bb3647ef40b462ad088cbc6f6fa31a"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_STOP\_COMPLETE\_EVT
    :   when extended advertising stop complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t42BK_BLE_GAP_EXT_ADV_SET_REMOVE_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t42BK_BLE_GAP_EXT_ADV_SET_REMOVE_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t42BK_BLE_GAP_EXT_ADV_SET_REMOVE_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a75718414838d0d0747ebe36ba1068ba7"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_SET\_REMOVE\_COMPLETE\_EVT
    :   when extended advertising set remove complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t41BK_BLE_GAP_EXT_ADV_SET_CLEAR_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t41BK_BLE_GAP_EXT_ADV_SET_CLEAR_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t41BK_BLE_GAP_EXT_ADV_SET_CLEAR_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2acf278fb4b5739a86ef995c4f1926656d"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_SET\_CLEAR\_COMPLETE\_EVT
    :   when extended advertising set clear complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t47BK_BLE_GAP_PERIODIC_ADV_SET_PARAMS_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t47BK_BLE_GAP_PERIODIC_ADV_SET_PARAMS_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t47BK_BLE_GAP_PERIODIC_ADV_SET_PARAMS_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a8392446bb9165c19385918cbb5175fbc"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_SET\_PARAMS\_COMPLETE\_EVT
    :   when periodic advertising parameter complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t45BK_BLE_GAP_PERIODIC_ADV_DATA_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t45BK_BLE_GAP_PERIODIC_ADV_DATA_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t45BK_BLE_GAP_PERIODIC_ADV_DATA_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a3e64a38364f848f925e23acbcf606816"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_DATA\_SET\_COMPLETE\_EVT
    :   when periodic advertising data complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t42BK_BLE_GAP_PERIODIC_ADV_START_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t42BK_BLE_GAP_PERIODIC_ADV_START_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t42BK_BLE_GAP_PERIODIC_ADV_START_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a8fb074e76aa9c3249c3580fbb625ce1d"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_START\_COMPLETE\_EVT
    :   when periodic advertising start complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t41BK_BLE_GAP_PERIODIC_ADV_STOP_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t41BK_BLE_GAP_PERIODIC_ADV_STOP_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t41BK_BLE_GAP_PERIODIC_ADV_STOP_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2af9db5d973cec1824c2808e63b9e33ea1"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_STOP\_COMPLETE\_EVT
    :   when periodic advertising stop complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t48BK_BLE_GAP_PERIODIC_ADV_CREATE_SYNC_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t48BK_BLE_GAP_PERIODIC_ADV_CREATE_SYNC_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t48BK_BLE_GAP_PERIODIC_ADV_CREATE_SYNC_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ac434632a82c64bb0a5e53d12c159d9d2"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_CREATE\_SYNC\_COMPLETE\_EVT
    :   when periodic advertising create sync complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t48BK_BLE_GAP_PERIODIC_ADV_SYNC_CANCEL_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t48BK_BLE_GAP_PERIODIC_ADV_SYNC_CANCEL_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t48BK_BLE_GAP_PERIODIC_ADV_SYNC_CANCEL_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a26288325a0d377a3fecbda45a8f471e5"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_CANCEL\_COMPLETE\_EVT
    :   when extended advertising sync cancel complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t51BK_BLE_GAP_PERIODIC_ADV_SYNC_TERMINATE_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t51BK_BLE_GAP_PERIODIC_ADV_SYNC_TERMINATE_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t51BK_BLE_GAP_PERIODIC_ADV_SYNC_TERMINATE_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a82b8550a446430d5fb8720b40329b99a"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_TERMINATE\_COMPLETE\_EVT
    :   when extended advertising sync terminate complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t44BK_BLE_GAP_PERIODIC_ADV_ADD_DEV_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t44BK_BLE_GAP_PERIODIC_ADV_ADD_DEV_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t44BK_BLE_GAP_PERIODIC_ADV_ADD_DEV_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a55ed838802cd51153ab56b32073a3adf"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_ADD\_DEV\_COMPLETE\_EVT
    :   when extended advertising add device complete , the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t47BK_BLE_GAP_PERIODIC_ADV_REMOVE_DEV_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t47BK_BLE_GAP_PERIODIC_ADV_REMOVE_DEV_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t47BK_BLE_GAP_PERIODIC_ADV_REMOVE_DEV_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2aedb0f5728425f43071825b68acc09fd3"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_REMOVE\_DEV\_COMPLETE\_EVT
    :   when extended advertising remove device complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t46BK_BLE_GAP_PERIODIC_ADV_CLEAR_DEV_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t46BK_BLE_GAP_PERIODIC_ADV_CLEAR_DEV_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t46BK_BLE_GAP_PERIODIC_ADV_CLEAR_DEV_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ab777c2fd7a898c65ba3ac2587e707326"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_CLEAR\_DEV\_COMPLETE\_EVT
    :   when extended advertising clear device, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t43BK_BLE_GAP_EXT_SCAN_PARAMS_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t43BK_BLE_GAP_EXT_SCAN_PARAMS_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t43BK_BLE_GAP_EXT_SCAN_PARAMS_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ae07a07650e8c7c192ef6378e27beebc1"></a> enumerator BK\_BLE\_GAP\_EXT\_SCAN\_PARAMS\_SET\_COMPLETE\_EVT
    :   when extended scan parameter complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t38BK_BLE_GAP_EXT_SCAN_START_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t38BK_BLE_GAP_EXT_SCAN_START_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t38BK_BLE_GAP_EXT_SCAN_START_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2adfee961a2a2dddcc387dd4783ad5498d"></a> enumerator BK\_BLE\_GAP\_EXT\_SCAN\_START\_COMPLETE\_EVT
    :   when extended scan start complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t37BK_BLE_GAP_EXT_SCAN_STOP_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t37BK_BLE_GAP_EXT_SCAN_STOP_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t37BK_BLE_GAP_EXT_SCAN_STOP_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ab3a0e5cb9e5cfd7a80f726ea3790ead0"></a> enumerator BK\_BLE\_GAP\_EXT\_SCAN\_STOP\_COMPLETE\_EVT
    :   when extended scan stop complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t50BK_BLE_GAP_PREFER_EXT_CONN_PARAMS_SET_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t50BK_BLE_GAP_PREFER_EXT_CONN_PARAMS_SET_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t50BK_BLE_GAP_PREFER_EXT_CONN_PARAMS_SET_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2abeaa1156978f2916dfbd0a8a06e4c216"></a> enumerator BK\_BLE\_GAP\_PREFER\_EXT\_CONN\_PARAMS\_SET\_COMPLETE\_EVT
    :   when extended prefer connection parameter set complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t34BK_BLE_GAP_PHY_UPDATE_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t34BK_BLE_GAP_PHY_UPDATE_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t34BK_BLE_GAP_PHY_UPDATE_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a0c861ecc261d5f69fa600fcc179a8f75"></a> enumerator BK\_BLE\_GAP\_PHY\_UPDATE\_COMPLETE\_EVT
    :   when ble phy update complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t29BK_BLE_GAP_EXT_ADV_REPORT_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t29BK_BLE_GAP_EXT_ADV_REPORT_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t29BK_BLE_GAP_EXT_ADV_REPORT_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a1102b1ab5e0bfb8a1b38e1b4812443d9"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_REPORT\_EVT
    :   when extended advertising report complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t27BK_BLE_GAP_SCAN_TIMEOUT_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t27BK_BLE_GAP_SCAN_TIMEOUT_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t27BK_BLE_GAP_SCAN_TIMEOUT_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2af8bfd224a889d3e9b91363b43f116660"></a> enumerator BK\_BLE\_GAP\_SCAN\_TIMEOUT\_EVT
    :   when scan timeout complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t29BK_BLE_GAP_ADV_TERMINATED_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t29BK_BLE_GAP_ADV_TERMINATED_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t29BK_BLE_GAP_ADV_TERMINATED_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a1aa55ff081a9a3d647075bc5d1b70fde"></a> enumerator BK\_BLE\_GAP\_ADV\_TERMINATED\_EVT
    :   when advertising terminate data complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t32BK_BLE_GAP_SCAN_REQ_RECEIVED_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t32BK_BLE_GAP_SCAN_REQ_RECEIVED_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t32BK_BLE_GAP_SCAN_REQ_RECEIVED_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2aee399b35a2dee73c6a96f1c266644fd4"></a> enumerator BK\_BLE\_GAP\_SCAN\_REQ\_RECEIVED\_EVT
    :   when scan req received complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t39BK_BLE_GAP_CHANNEL_SELECT_ALGORITHM_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t39BK_BLE_GAP_CHANNEL_SELECT_ALGORITHM_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t39BK_BLE_GAP_CHANNEL_SELECT_ALGORITHM_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ac3abc44e374e0dfe2844f3611ba4ec84"></a> enumerator BK\_BLE\_GAP\_CHANNEL\_SELECT\_ALGORITHM\_EVT
    :   when channel select algorithm complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t34BK_BLE_GAP_PERIODIC_ADV_REPORT_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t34BK_BLE_GAP_PERIODIC_ADV_REPORT_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t34BK_BLE_GAP_PERIODIC_ADV_REPORT_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a4e0c356b4ddff1b63221912e6fd04021"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_REPORT\_EVT
    :   when periodic report advertising complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t37BK_BLE_GAP_PERIODIC_ADV_SYNC_LOST_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t37BK_BLE_GAP_PERIODIC_ADV_SYNC_LOST_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t37BK_BLE_GAP_PERIODIC_ADV_SYNC_LOST_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ad9ce54943bdaa13ced61ce74825c76c2"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_LOST\_EVT
    :   when periodic advertising sync lost complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t38BK_BLE_GAP_PERIODIC_ADV_SYNC_ESTAB_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t38BK_BLE_GAP_PERIODIC_ADV_SYNC_ESTAB_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t38BK_BLE_GAP_PERIODIC_ADV_SYNC_ESTAB_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2ab0f7e31415d8ad3292906049b204e1fb"></a> enumerator BK\_BLE\_GAP\_PERIODIC\_ADV\_SYNC\_ESTAB\_EVT
    :   when periodic advertising sync establish complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t31BK_BLE_GAP_CONNECT_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t31BK_BLE_GAP_CONNECT_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t31BK_BLE_GAP_CONNECT_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a0621cead5d819803b0414dd4b5854af3"></a> enumerator BK\_BLE\_GAP\_CONNECT\_COMPLETE\_EVT
    :   when ble connection complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t34BK_BLE_GAP_DISCONNECT_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t34BK_BLE_GAP_DISCONNECT_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t34BK_BLE_GAP_DISCONNECT_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a83bab21e1c3d6eb9f673e9ad81af3c5f"></a> enumerator BK\_BLE\_GAP\_DISCONNECT\_COMPLETE\_EVT
    :   when ble disconnect complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t29BK_BLE_GAP_CONNECT_CANCEL_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t29BK_BLE_GAP_CONNECT_CANCEL_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t29BK_BLE_GAP_CONNECT_CANCEL_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a5b38b557cba8dac067827939cf6b955b"></a> enumerator BK\_BLE\_GAP\_CONNECT\_CANCEL\_EVT
    :   when ble connect cancel complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t37BK_BLE_GAP_UPDATE_CONN_PARAMS_REQ_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t37BK_BLE_GAP_UPDATE_CONN_PARAMS_REQ_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t37BK_BLE_GAP_UPDATE_CONN_PARAMS_REQ_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2abc4377247b00be8250858140647fbb1d"></a> enumerator BK\_BLE\_GAP\_UPDATE\_CONN\_PARAMS\_REQ\_EVT
    :   when peer req update param, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t43BK_BLE_GAP_SET_SECURITY_PARAMS_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t43BK_BLE_GAP_SET_SECURITY_PARAMS_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t43BK_BLE_GAP_SET_SECURITY_PARAMS_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a75c8c417431ca58c73d2935971386b57"></a> enumerator BK\_BLE\_GAP\_SET\_SECURITY\_PARAMS\_COMPLETE\_EVT
    :   when set security params complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t36BK_BLE_GAP_GENERATE_RPA_COMPLETE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t36BK_BLE_GAP_GENERATE_RPA_COMPLETE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t36BK_BLE_GAP_GENERATE_RPA_COMPLETE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a16400ac97f8d5a118fbf2e38413bacaf"></a> enumerator BK\_BLE\_GAP\_GENERATE\_RPA\_COMPLETE\_EVT
    :   when generate rpa complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t32BK_BLE_GAP_ENCRYPTION_CHANGE_EVTE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t32BK_BLE_GAP_ENCRYPTION_CHANGE_EVTE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t32BK_BLE_GAP_ENCRYPTION_CHANGE_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2acb10ab69a68d0427412a7b8126d7a481"></a> enumerator BK\_BLE\_GAP\_ENCRYPTION\_CHANGE\_EVT
    :   when encryption change complete, the event comes

    <a id="_CPPv4N21bk_ble_gap_cb_event_t18BK_BLE_GAP_EVT_MAXE"></a>

    <a id="_CPPv3N21bk_ble_gap_cb_event_t18BK_BLE_GAP_EVT_MAXE"></a> <a id="_CPPv2N21bk_ble_gap_cb_event_t18BK_BLE_GAP_EVT_MAXE"></a> <a id="group__dm__gap__defines__v1_1ggace9462d6a5ecd73deb995f8dcaf075b2a5c4b1e4f7f8d26fdb7ac959ede6b4270"></a> enumerator BK\_BLE\_GAP\_EVT\_MAX
    :   when maximum advertising event complete, the event comes

<a id="_CPPv420bk_ble_adv_data_type"></a>

<a id="_CPPv320bk_ble_adv_data_type"></a> <a id="_CPPv220bk_ble_adv_data_type"></a> <a id="group__dm__gap__defines__v1_1ga80cc9d983fbfbfe3e80970b9fd0af073"></a> enum bk\_ble\_adv\_data\_type
:   The type of advertising data(not adv\_type)

    *Values:*

    <a id="_CPPv4N20bk_ble_adv_data_type19BK_BLE_AD_TYPE_FLAGE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type19BK_BLE_AD_TYPE_FLAGE"></a> <a id="_CPPv2N20bk_ble_adv_data_type19BK_BLE_AD_TYPE_FLAGE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a672c758eb6845b8a60123801292ebfe6"></a> enumerator BK\_BLE\_AD\_TYPE\_FLAG

    <a id="_CPPv4N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_16SRV_PARTE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_16SRV_PARTE"></a> <a id="_CPPv2N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_16SRV_PARTE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a140fb799909dbcd30d4f652ee95e61ac"></a> enumerator BK\_BLE\_AD\_TYPE\_16SRV\_PART

    <a id="_CPPv4N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_16SRV_CMPLE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_16SRV_CMPLE"></a> <a id="_CPPv2N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_16SRV_CMPLE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073afdd991394115aff1f4ef14f1cc2a7f85"></a> enumerator BK\_BLE\_AD\_TYPE\_16SRV\_CMPL

    <a id="_CPPv4N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_32SRV_PARTE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_32SRV_PARTE"></a> <a id="_CPPv2N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_32SRV_PARTE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a65b624a4c66d8a07683934f5dec9e36d"></a> enumerator BK\_BLE\_AD\_TYPE\_32SRV\_PART

    <a id="_CPPv4N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_32SRV_CMPLE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_32SRV_CMPLE"></a> <a id="_CPPv2N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_32SRV_CMPLE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ac42692c01f2a837ca06821557551fce1"></a> enumerator BK\_BLE\_AD\_TYPE\_32SRV\_CMPL

    <a id="_CPPv4N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_128SRV_PARTE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_128SRV_PARTE"></a> <a id="_CPPv2N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_128SRV_PARTE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a11fcb4051dbe3541451cf215d490d622"></a> enumerator BK\_BLE\_AD\_TYPE\_128SRV\_PART

    <a id="_CPPv4N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_128SRV_CMPLE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_128SRV_CMPLE"></a> <a id="_CPPv2N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_128SRV_CMPLE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a0ec8fc24365644a9cc6a9e0c0e2b9ca9"></a> enumerator BK\_BLE\_AD\_TYPE\_128SRV\_CMPL

    <a id="_CPPv4N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_NAME_SHORTE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_NAME_SHORTE"></a> <a id="_CPPv2N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_NAME_SHORTE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a006ac954521ee22eaba6a27fefd81674"></a> enumerator BK\_BLE\_AD\_TYPE\_NAME\_SHORT

    <a id="_CPPv4N20bk_ble_adv_data_type24BK_BLE_AD_TYPE_NAME_CMPLE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type24BK_BLE_AD_TYPE_NAME_CMPLE"></a> <a id="_CPPv2N20bk_ble_adv_data_type24BK_BLE_AD_TYPE_NAME_CMPLE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a2e2c41d1ebef5b6164a091fc274e9ea4"></a> enumerator BK\_BLE\_AD\_TYPE\_NAME\_CMPL

    <a id="_CPPv4N20bk_ble_adv_data_type21BK_BLE_AD_TYPE_TX_PWRE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type21BK_BLE_AD_TYPE_TX_PWRE"></a> <a id="_CPPv2N20bk_ble_adv_data_type21BK_BLE_AD_TYPE_TX_PWRE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a88adcc3cf89381b73c169e2e0659fd2d"></a> enumerator BK\_BLE\_AD\_TYPE\_TX\_PWR

    <a id="_CPPv4N20bk_ble_adv_data_type24BK_BLE_AD_TYPE_DEV_CLASSE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type24BK_BLE_AD_TYPE_DEV_CLASSE"></a> <a id="_CPPv2N20bk_ble_adv_data_type24BK_BLE_AD_TYPE_DEV_CLASSE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a99fec4246dbee98687a4538565426bc2"></a> enumerator BK\_BLE\_AD\_TYPE\_DEV\_CLASS

    <a id="_CPPv4N20bk_ble_adv_data_type20BK_BLE_AD_TYPE_SM_TKE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type20BK_BLE_AD_TYPE_SM_TKE"></a> <a id="_CPPv2N20bk_ble_adv_data_type20BK_BLE_AD_TYPE_SM_TKE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a66f5b423903d1fa58fd80d2656f4b049"></a> enumerator BK\_BLE\_AD\_TYPE\_SM\_TK

    <a id="_CPPv4N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_SM_OOB_FLAGE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_SM_OOB_FLAGE"></a> <a id="_CPPv2N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_SM_OOB_FLAGE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ad7026ac1efb6bd3942001d526a9d53db"></a> enumerator BK\_BLE\_AD\_TYPE\_SM\_OOB\_FLAG

    <a id="_CPPv4N20bk_ble_adv_data_type24BK_BLE_AD_TYPE_INT_RANGEE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type24BK_BLE_AD_TYPE_INT_RANGEE"></a> <a id="_CPPv2N20bk_ble_adv_data_type24BK_BLE_AD_TYPE_INT_RANGEE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a33363c93a3e2e8c9385e62f34f7ce28d"></a> enumerator BK\_BLE\_AD\_TYPE\_INT\_RANGE

    <a id="_CPPv4N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_SOL_SRV_UUIDE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_SOL_SRV_UUIDE"></a> <a id="_CPPv2N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_SOL_SRV_UUIDE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a09bd72665bfc4e6bb7f6991c93d16465"></a> enumerator BK\_BLE\_AD\_TYPE\_SOL\_SRV\_UUID

    <a id="_CPPv4N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_128SOL_SRV_UUIDE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_128SOL_SRV_UUIDE"></a> <a id="_CPPv2N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_128SOL_SRV_UUIDE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a582f55dd194e5b2bd8abd657ce022886"></a> enumerator BK\_BLE\_AD\_TYPE\_128SOL\_SRV\_UUID

    <a id="_CPPv4N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_SERVICE_DATAE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_SERVICE_DATAE"></a> <a id="_CPPv2N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_SERVICE_DATAE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a6b07d47e14d4ea4aca6dc94f1c2b5187"></a> enumerator BK\_BLE\_AD\_TYPE\_SERVICE\_DATA

    <a id="_CPPv4N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_PUBLIC_TARGETE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_PUBLIC_TARGETE"></a> <a id="_CPPv2N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_PUBLIC_TARGETE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a9c2e2a7c160218080fbfe92d5268513b"></a> enumerator BK\_BLE\_AD\_TYPE\_PUBLIC\_TARGET

    <a id="_CPPv4N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_RANDOM_TARGETE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_RANDOM_TARGETE"></a> <a id="_CPPv2N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_RANDOM_TARGETE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ae82ffa3a682c3287aebab43a3445021a"></a> enumerator BK\_BLE\_AD\_TYPE\_RANDOM\_TARGET

    <a id="_CPPv4N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_APPEARANCEE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_APPEARANCEE"></a> <a id="_CPPv2N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_APPEARANCEE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a2a565e32d1c53c8b7a672159b0089d76"></a> enumerator BK\_BLE\_AD\_TYPE\_APPEARANCE

    <a id="_CPPv4N20bk_ble_adv_data_type22BK_BLE_AD_TYPE_ADV_INTE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type22BK_BLE_AD_TYPE_ADV_INTE"></a> <a id="_CPPv2N20bk_ble_adv_data_type22BK_BLE_AD_TYPE_ADV_INTE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a3a1737ba11251c15a431b6050c791a8a"></a> enumerator BK\_BLE\_AD\_TYPE\_ADV\_INT

    <a id="_CPPv4N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_LE_DEV_ADDRE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_LE_DEV_ADDRE"></a> <a id="_CPPv2N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_LE_DEV_ADDRE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073aa54d6f3bb650e61b6534a1e9807d320c"></a> enumerator BK\_BLE\_AD\_TYPE\_LE\_DEV\_ADDR

    <a id="_CPPv4N20bk_ble_adv_data_type22BK_BLE_AD_TYPE_LE_ROLEE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type22BK_BLE_AD_TYPE_LE_ROLEE"></a> <a id="_CPPv2N20bk_ble_adv_data_type22BK_BLE_AD_TYPE_LE_ROLEE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a4ee8f338ca210abd00bdb10d3998cead"></a> enumerator BK\_BLE\_AD\_TYPE\_LE\_ROLE

    <a id="_CPPv4N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_SPAIR_C256E"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_SPAIR_C256E"></a> <a id="_CPPv2N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_SPAIR_C256E"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a682438144f96e40affecef72dbbfeebf"></a> enumerator BK\_BLE\_AD\_TYPE\_SPAIR\_C256

    <a id="_CPPv4N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_SPAIR_R256E"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_SPAIR_R256E"></a> <a id="_CPPv2N20bk_ble_adv_data_type25BK_BLE_AD_TYPE_SPAIR_R256E"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a2bad085682ed44d54992f08ab5d927d0"></a> enumerator BK\_BLE\_AD\_TYPE\_SPAIR\_R256

    <a id="_CPPv4N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_32SOL_SRV_UUIDE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_32SOL_SRV_UUIDE"></a> <a id="_CPPv2N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_32SOL_SRV_UUIDE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a959ad88cc6f91ae39dfae1ed02da2441"></a> enumerator BK\_BLE\_AD\_TYPE\_32SOL\_SRV\_UUID

    <a id="_CPPv4N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_32SERVICE_DATAE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_32SERVICE_DATAE"></a> <a id="_CPPv2N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_32SERVICE_DATAE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a1e93a0c7e01d28a9d1245c9262bcd5b3"></a> enumerator BK\_BLE\_AD\_TYPE\_32SERVICE\_DATA

    <a id="_CPPv4N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_128SERVICE_DATAE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_128SERVICE_DATAE"></a> <a id="_CPPv2N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_128SERVICE_DATAE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ab08aeff96e4bc8e89fde2f4891cb6b6c"></a> enumerator BK\_BLE\_AD\_TYPE\_128SERVICE\_DATA

    <a id="_CPPv4N20bk_ble_adv_data_type32BK_BLE_AD_TYPE_LE_SECURE_CONFIRME"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type32BK_BLE_AD_TYPE_LE_SECURE_CONFIRME"></a> <a id="_CPPv2N20bk_ble_adv_data_type32BK_BLE_AD_TYPE_LE_SECURE_CONFIRME"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a8810747e8ea8c9dc8889684ec2fa3291"></a> enumerator BK\_BLE\_AD\_TYPE\_LE\_SECURE\_CONFIRM

    <a id="_CPPv4N20bk_ble_adv_data_type31BK_BLE_AD_TYPE_LE_SECURE_RANDOME"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type31BK_BLE_AD_TYPE_LE_SECURE_RANDOME"></a> <a id="_CPPv2N20bk_ble_adv_data_type31BK_BLE_AD_TYPE_LE_SECURE_RANDOME"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ac70d1116436867dbd0a95fd2d1e4c6a7"></a> enumerator BK\_BLE\_AD\_TYPE\_LE\_SECURE\_RANDOM

    <a id="_CPPv4N20bk_ble_adv_data_type18BK_BLE_AD_TYPE_URIE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type18BK_BLE_AD_TYPE_URIE"></a> <a id="_CPPv2N20bk_ble_adv_data_type18BK_BLE_AD_TYPE_URIE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a27037cbb1e0c2cf1abe08608b3ea7033"></a> enumerator BK\_BLE\_AD\_TYPE\_URI

    <a id="_CPPv4N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_INDOOR_POSITIONE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_INDOOR_POSITIONE"></a> <a id="_CPPv2N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_INDOOR_POSITIONE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a740b309369990c775a41f8f490d7667a"></a> enumerator BK\_BLE\_AD\_TYPE\_INDOOR\_POSITION

    <a id="_CPPv4N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_TRANS_DISC_DATAE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_TRANS_DISC_DATAE"></a> <a id="_CPPv2N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_TRANS_DISC_DATAE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a4d4883ff7c8ed0478ed5d4257319722e"></a> enumerator BK\_BLE\_AD\_TYPE\_TRANS\_DISC\_DATA

    <a id="_CPPv4N20bk_ble_adv_data_type33BK_BLE_AD_TYPE_LE_SUPPORT_FEATUREE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type33BK_BLE_AD_TYPE_LE_SUPPORT_FEATUREE"></a> <a id="_CPPv2N20bk_ble_adv_data_type33BK_BLE_AD_TYPE_LE_SUPPORT_FEATUREE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ab7efa05add80efce8f81e52ae9e72dd1"></a> enumerator BK\_BLE\_AD\_TYPE\_LE\_SUPPORT\_FEATURE

    <a id="_CPPv4N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_CHAN_MAP_UPDATEE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_CHAN_MAP_UPDATEE"></a> <a id="_CPPv2N20bk_ble_adv_data_type30BK_BLE_AD_TYPE_CHAN_MAP_UPDATEE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a53003fad6f91eeb31d694dca0f96ef34"></a> enumerator BK\_BLE\_AD\_TYPE\_CHAN\_MAP\_UPDATE

    <a id="_CPPv4N20bk_ble_adv_data_type21BK_BLE_AD_TYPE_PB_ADVE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type21BK_BLE_AD_TYPE_PB_ADVE"></a> <a id="_CPPv2N20bk_ble_adv_data_type21BK_BLE_AD_TYPE_PB_ADVE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a99c4cc228f4685008f27e96ed2af560e"></a> enumerator BK\_BLE\_AD\_TYPE\_PB\_ADV

    <a id="_CPPv4N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_MESH_MESSAGEE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_MESH_MESSAGEE"></a> <a id="_CPPv2N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_MESH_MESSAGEE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a2890375e599e22b20248cf6e1c348fe8"></a> enumerator BK\_BLE\_AD\_TYPE\_MESH\_MESSAGE

    <a id="_CPPv4N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_MESH_BEACONE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_MESH_BEACONE"></a> <a id="_CPPv2N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_MESH_BEACONE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ac3562d07661bf28192996776d3691cd4"></a> enumerator BK\_BLE\_AD\_TYPE\_MESH\_BEACON

    <a id="_CPPv4N20bk_ble_adv_data_type23BK_BLE_AD_TYPE_BIG_INFOE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type23BK_BLE_AD_TYPE_BIG_INFOE"></a> <a id="_CPPv2N20bk_ble_adv_data_type23BK_BLE_AD_TYPE_BIG_INFOE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a20f7b37a9423d25f4f30f0145ab3cb55"></a> enumerator BK\_BLE\_AD\_TYPE\_BIG\_INFO

    <a id="_CPPv4N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_BROADCAST_CODEE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_BROADCAST_CODEE"></a> <a id="_CPPv2N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_BROADCAST_CODEE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a9cd9ede45aad70096c787100b4e9828e"></a> enumerator BK\_BLE\_AD\_TYPE\_BROADCAST\_CODE

    <a id="_CPPv4N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_RESOLV_SET_IDE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_RESOLV_SET_IDE"></a> <a id="_CPPv2N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_RESOLV_SET_IDE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ab5a0ec3f4dc53774b9969c60b49e0f8c"></a> enumerator BK\_BLE\_AD\_TYPE\_RESOLV\_SET\_ID

    <a id="_CPPv4N20bk_ble_adv_data_type32BK_BLE_AD_TYPE_ADV_INTERVAL_LONGE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type32BK_BLE_AD_TYPE_ADV_INTERVAL_LONGE"></a> <a id="_CPPv2N20bk_ble_adv_data_type32BK_BLE_AD_TYPE_ADV_INTERVAL_LONGE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a34522aff35b8b8ae99e3bd773025f584"></a> enumerator BK\_BLE\_AD\_TYPE\_ADV\_INTERVAL\_LONG

    <a id="_CPPv4N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_BROADCAST_NAMEE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_BROADCAST_NAMEE"></a> <a id="_CPPv2N20bk_ble_adv_data_type29BK_BLE_AD_TYPE_BROADCAST_NAMEE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073aba78d9705d9606678733019caa9056ee"></a> enumerator BK\_BLE\_AD\_TYPE\_BROADCAST\_NAME

    <a id="_CPPv4N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_ENCRYPTED_ADVE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_ENCRYPTED_ADVE"></a> <a id="_CPPv2N20bk_ble_adv_data_type28BK_BLE_AD_TYPE_ENCRYPTED_ADVE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ae98543449a84cbd146ed11b47bd5f357"></a> enumerator BK\_BLE\_AD\_TYPE\_ENCRYPTED\_ADV

    <a id="_CPPv4N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_PER_ADV_RTIE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_PER_ADV_RTIE"></a> <a id="_CPPv2N20bk_ble_adv_data_type26BK_BLE_AD_TYPE_PER_ADV_RTIE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073ac177b1a0d3d9844e62bc218d73d4da2b"></a> enumerator BK\_BLE\_AD\_TYPE\_PER\_ADV\_RTI

    <a id="_CPPv4N20bk_ble_adv_data_type31BK_BLE_AD_TYPE_ELEC_SHELF_LABELE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type31BK_BLE_AD_TYPE_ELEC_SHELF_LABELE"></a> <a id="_CPPv2N20bk_ble_adv_data_type31BK_BLE_AD_TYPE_ELEC_SHELF_LABELE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a4250ad74faf3dc88facc690f0012e999"></a> enumerator BK\_BLE\_AD\_TYPE\_ELEC\_SHELF\_LABEL

    <a id="_CPPv4N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_3D_INFO_DATAE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_3D_INFO_DATAE"></a> <a id="_CPPv2N20bk_ble_adv_data_type27BK_BLE_AD_TYPE_3D_INFO_DATAE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a7791ac48d2c140a584b88e8d5b863473"></a> enumerator BK\_BLE\_AD\_TYPE\_3D\_INFO\_DATA

    <a id="_CPPv4N20bk_ble_adv_data_type19BK_BLE_AD_TYPE_MANUE"></a>

    <a id="_CPPv3N20bk_ble_adv_data_type19BK_BLE_AD_TYPE_MANUE"></a> <a id="_CPPv2N20bk_ble_adv_data_type19BK_BLE_AD_TYPE_MANUE"></a> <a id="group__dm__gap__defines__v1_1gga80cc9d983fbfbfe3e80970b9fd0af073a7ca31994e2baa5b5d1dd8d414344a21f"></a> enumerator BK\_BLE\_AD\_TYPE\_MANU

<a id="_CPPv417bk_ble_adv_type_t"></a>

<a id="_CPPv317bk_ble_adv_type_t"></a> <a id="_CPPv217bk_ble_adv_type_t"></a> <a id="group__dm__gap__defines__v1_1ga7a90cd2faf66e13bf29ee4c2eb1da842"></a> enum bk\_ble\_adv\_type\_t
:   Advertising mode.

    *Values:*

    <a id="_CPPv4N17bk_ble_adv_type_t12ADV_TYPE_INDE"></a>

    <a id="_CPPv3N17bk_ble_adv_type_t12ADV_TYPE_INDE"></a> <a id="_CPPv2N17bk_ble_adv_type_t12ADV_TYPE_INDE"></a> <a id="group__dm__gap__defines__v1_1gga7a90cd2faf66e13bf29ee4c2eb1da842a6184cb2f7476f32a5668a92abcf57d3c"></a> enumerator ADV\_TYPE\_IND
    :   adv that can be scan and connect

    <a id="_CPPv4N17bk_ble_adv_type_t24ADV_TYPE_DIRECT_IND_HIGHE"></a>

    <a id="_CPPv3N17bk_ble_adv_type_t24ADV_TYPE_DIRECT_IND_HIGHE"></a> <a id="_CPPv2N17bk_ble_adv_type_t24ADV_TYPE_DIRECT_IND_HIGHE"></a> <a id="group__dm__gap__defines__v1_1gga7a90cd2faf66e13bf29ee4c2eb1da842a2f15d026f3f47b3aeb5072f84ccd7096"></a> enumerator ADV\_TYPE\_DIRECT\_IND\_HIGH
    :   adv that can be connect by special device(white list). This send adv more frequently.

    <a id="_CPPv4N17bk_ble_adv_type_t17ADV_TYPE_SCAN_INDE"></a>

    <a id="_CPPv3N17bk_ble_adv_type_t17ADV_TYPE_SCAN_INDE"></a> <a id="_CPPv2N17bk_ble_adv_type_t17ADV_TYPE_SCAN_INDE"></a> <a id="group__dm__gap__defines__v1_1gga7a90cd2faf66e13bf29ee4c2eb1da842a472bde7144c7c4b716a08ba454003f5a"></a> enumerator ADV\_TYPE\_SCAN\_IND
    :   adv that can be scan

    <a id="_CPPv4N17bk_ble_adv_type_t20ADV_TYPE_NONCONN_INDE"></a>

    <a id="_CPPv3N17bk_ble_adv_type_t20ADV_TYPE_NONCONN_INDE"></a> <a id="_CPPv2N17bk_ble_adv_type_t20ADV_TYPE_NONCONN_INDE"></a> <a id="group__dm__gap__defines__v1_1gga7a90cd2faf66e13bf29ee4c2eb1da842ab4a10b318e480dd2a4cecc333d5f9b5f"></a> enumerator ADV\_TYPE\_NONCONN\_IND
    :   adv that can’t be scan and connect

    <a id="_CPPv4N17bk_ble_adv_type_t23ADV_TYPE_DIRECT_IND_LOWE"></a>

    <a id="_CPPv3N17bk_ble_adv_type_t23ADV_TYPE_DIRECT_IND_LOWE"></a> <a id="_CPPv2N17bk_ble_adv_type_t23ADV_TYPE_DIRECT_IND_LOWE"></a> <a id="group__dm__gap__defines__v1_1gga7a90cd2faf66e13bf29ee4c2eb1da842aeb1a51ef68ffd9f532afdfff3c365087"></a> enumerator ADV\_TYPE\_DIRECT\_IND\_LOW
    :   adv that can be connect by special device(white list). This send adv more few.

<a id="_CPPv420bk_ble_adv_channel_t"></a>

<a id="_CPPv320bk_ble_adv_channel_t"></a> <a id="_CPPv220bk_ble_adv_channel_t"></a> <a id="group__dm__gap__defines__v1_1gaf9040d55789cc0128361c96642b422e0"></a> enum bk\_ble\_adv\_channel\_t
:   Advertising channel mask.

    *Values:*

    <a id="_CPPv4N20bk_ble_adv_channel_t14BK_ADV_CHNL_37E"></a>

    <a id="_CPPv3N20bk_ble_adv_channel_t14BK_ADV_CHNL_37E"></a> <a id="_CPPv2N20bk_ble_adv_channel_t14BK_ADV_CHNL_37E"></a> <a id="group__dm__gap__defines__v1_1ggaf9040d55789cc0128361c96642b422e0a20d4aba0126616764c88c855eeeea7bc"></a> enumerator BK\_ADV\_CHNL\_37
    :   channel 37

    <a id="_CPPv4N20bk_ble_adv_channel_t14BK_ADV_CHNL_38E"></a>

    <a id="_CPPv3N20bk_ble_adv_channel_t14BK_ADV_CHNL_38E"></a> <a id="_CPPv2N20bk_ble_adv_channel_t14BK_ADV_CHNL_38E"></a> <a id="group__dm__gap__defines__v1_1ggaf9040d55789cc0128361c96642b422e0a711a99ac1a74cd4632a9ef10b1a4aa80"></a> enumerator BK\_ADV\_CHNL\_38
    :   channel 38

    <a id="_CPPv4N20bk_ble_adv_channel_t14BK_ADV_CHNL_39E"></a>

    <a id="_CPPv3N20bk_ble_adv_channel_t14BK_ADV_CHNL_39E"></a> <a id="_CPPv2N20bk_ble_adv_channel_t14BK_ADV_CHNL_39E"></a> <a id="group__dm__gap__defines__v1_1ggaf9040d55789cc0128361c96642b422e0a97544d83428dca1d60a502824f958973"></a> enumerator BK\_ADV\_CHNL\_39
    :   channel 39

    <a id="_CPPv4N20bk_ble_adv_channel_t15BK_ADV_CHNL_ALLE"></a>

    <a id="_CPPv3N20bk_ble_adv_channel_t15BK_ADV_CHNL_ALLE"></a> <a id="_CPPv2N20bk_ble_adv_channel_t15BK_ADV_CHNL_ALLE"></a> <a id="group__dm__gap__defines__v1_1ggaf9040d55789cc0128361c96642b422e0a6825086efc9c26ec53189de99cb76509"></a> enumerator BK\_ADV\_CHNL\_ALL
    :   channel all

<a id="_CPPv419bk_ble_adv_filter_t"></a>

<a id="_CPPv319bk_ble_adv_filter_t"></a> <a id="_CPPv219bk_ble_adv_filter_t"></a> <a id="group__dm__gap__defines__v1_1ga80eb05eb7959d98404b05c7b7bc3dfcc"></a> enum bk\_ble\_adv\_filter\_t
:   Advertising filter.

    *Values:*

    <a id="_CPPv4N19bk_ble_adv_filter_t33ADV_FILTER_ALLOW_SCAN_ANY_CON_ANYE"></a>

    <a id="_CPPv3N19bk_ble_adv_filter_t33ADV_FILTER_ALLOW_SCAN_ANY_CON_ANYE"></a> <a id="_CPPv2N19bk_ble_adv_filter_t33ADV_FILTER_ALLOW_SCAN_ANY_CON_ANYE"></a> <a id="group__dm__gap__defines__v1_1gga80eb05eb7959d98404b05c7b7bc3dfccab436a2357176d151ce3c179056d39c18"></a> enumerator ADV\_FILTER\_ALLOW\_SCAN\_ANY\_CON\_ANY
    :   Allow both scan and connection requests from anyone.

    <a id="_CPPv4N19bk_ble_adv_filter_t34ADV_FILTER_ALLOW_SCAN_WLST_CON_ANYE"></a>

    <a id="_CPPv3N19bk_ble_adv_filter_t34ADV_FILTER_ALLOW_SCAN_WLST_CON_ANYE"></a> <a id="_CPPv2N19bk_ble_adv_filter_t34ADV_FILTER_ALLOW_SCAN_WLST_CON_ANYE"></a> <a id="group__dm__gap__defines__v1_1gga80eb05eb7959d98404b05c7b7bc3dfcca79004d57f8b100f4741f6897f8088c36"></a> enumerator ADV\_FILTER\_ALLOW\_SCAN\_WLST\_CON\_ANY
    :   Allow both scan req from White List devices only and connection req from anyone.

    <a id="_CPPv4N19bk_ble_adv_filter_t34ADV_FILTER_ALLOW_SCAN_ANY_CON_WLSTE"></a>

    <a id="_CPPv3N19bk_ble_adv_filter_t34ADV_FILTER_ALLOW_SCAN_ANY_CON_WLSTE"></a> <a id="_CPPv2N19bk_ble_adv_filter_t34ADV_FILTER_ALLOW_SCAN_ANY_CON_WLSTE"></a> <a id="group__dm__gap__defines__v1_1gga80eb05eb7959d98404b05c7b7bc3dfccaa28f3eeb327e70389b607b272c821e19"></a> enumerator ADV\_FILTER\_ALLOW\_SCAN\_ANY\_CON\_WLST
    :   Allow both scan req from anyone and connection req from White List devices only.

    <a id="_CPPv4N19bk_ble_adv_filter_t35ADV_FILTER_ALLOW_SCAN_WLST_CON_WLSTE"></a>

    <a id="_CPPv3N19bk_ble_adv_filter_t35ADV_FILTER_ALLOW_SCAN_WLST_CON_WLSTE"></a> <a id="_CPPv2N19bk_ble_adv_filter_t35ADV_FILTER_ALLOW_SCAN_WLST_CON_WLSTE"></a> <a id="group__dm__gap__defines__v1_1gga80eb05eb7959d98404b05c7b7bc3dfcca3c20b52145d6267ec9d32d6dbbfb617b"></a> enumerator ADV\_FILTER\_ALLOW\_SCAN\_WLST\_CON\_WLST
    :   Allow scan and connection requests from White List devices only.

<a id="_CPPv416bk_ble_sec_act_t"></a>

<a id="_CPPv316bk_ble_sec_act_t"></a> <a id="_CPPv216bk_ble_sec_act_t"></a> <a id="group__dm__gap__defines__v1_1gadc11e1e2683585ac84647007f9c38eec"></a> enum bk\_ble\_sec\_act\_t
:   ble encrypt method

    *Values:*

    <a id="_CPPv4N16bk_ble_sec_act_t18BK_BLE_SEC_ENCRYPTE"></a>

    <a id="_CPPv3N16bk_ble_sec_act_t18BK_BLE_SEC_ENCRYPTE"></a> <a id="_CPPv2N16bk_ble_sec_act_t18BK_BLE_SEC_ENCRYPTE"></a> <a id="group__dm__gap__defines__v1_1ggadc11e1e2683585ac84647007f9c38eeca001be391093c034c71b77c31091115de"></a> enumerator BK\_BLE\_SEC\_ENCRYPT
    :   If the device has already bonded, the stack will used Long Term Key (LTK) to encrypt with the remote device directly. Else if the device hasn’t bonded, the stack will used the default authentication request used the bk\_ble\_gap\_set\_security\_param function set by the user.

    <a id="_CPPv4N16bk_ble_sec_act_t26BK_BLE_SEC_ENCRYPT_NO_MITME"></a>

    <a id="_CPPv3N16bk_ble_sec_act_t26BK_BLE_SEC_ENCRYPT_NO_MITME"></a> <a id="_CPPv2N16bk_ble_sec_act_t26BK_BLE_SEC_ENCRYPT_NO_MITME"></a> <a id="group__dm__gap__defines__v1_1ggadc11e1e2683585ac84647007f9c38eecab7f3c9ca7bf22aa91d71adac6f0734a9"></a> enumerator BK\_BLE\_SEC\_ENCRYPT\_NO\_MITM
    :   If the device has been already bonded, the stack will check the LTK (Long Term Key) Whether the authentication request has been met, and if met, use the LTK to encrypt with the remote device directly, else re-pair with the remote device. Else if the device hasn’t been bonded, the stack will use NO MITM authentication request in the current link instead of using the authreq in the bk\_ble\_gap\_set\_security\_param function set by the user.

    <a id="_CPPv4N16bk_ble_sec_act_t23BK_BLE_SEC_ENCRYPT_MITME"></a>

    <a id="_CPPv3N16bk_ble_sec_act_t23BK_BLE_SEC_ENCRYPT_MITME"></a> <a id="_CPPv2N16bk_ble_sec_act_t23BK_BLE_SEC_ENCRYPT_MITME"></a> <a id="group__dm__gap__defines__v1_1ggadc11e1e2683585ac84647007f9c38eeca384bfe70d895a2f0ed1666b8261a1da0"></a> enumerator BK\_BLE\_SEC\_ENCRYPT\_MITM
    :   If the device has been already bonded, the stack will check the LTK (Long Term Key) whether the authentication request has been met, and if met, use the LTK to encrypt with the remote device directly, else re-pair with the remote device. Else if the device hasn’t been bonded, the stack will use MITM authentication request in the current link instead of using the authreq in the bk\_ble\_gap\_set\_security\_param function set by the user.

<a id="_CPPv417bk_ble_sm_param_t"></a>

<a id="_CPPv317bk_ble_sm_param_t"></a> <a id="_CPPv217bk_ble_sm_param_t"></a> <a id="group__dm__gap__defines__v1_1ga3797c167c7f9030a70ee6aa4d7454064"></a> enum bk\_ble\_sm\_param\_t
:   ble sm option

    *Values:*

    <a id="_CPPv4N17bk_ble_sm_param_t25BK_BLE_SM_AUTHEN_REQ_MODEE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t25BK_BLE_SM_AUTHEN_REQ_MODEE"></a> <a id="_CPPv2N17bk_ble_sm_param_t25BK_BLE_SM_AUTHEN_REQ_MODEE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064a9d8cc500d92b30301847224943e75381"></a> enumerator BK\_BLE\_SM\_AUTHEN\_REQ\_MODE
    :   Authentication requirements of local device, see bk\_ble\_auth\_req\_t.

    <a id="_CPPv4N17bk_ble_sm_param_t20BK_BLE_SM_IOCAP_MODEE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t20BK_BLE_SM_IOCAP_MODEE"></a> <a id="_CPPv2N17bk_ble_sm_param_t20BK_BLE_SM_IOCAP_MODEE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064a23b75167926bea7ce4946727be9d7e1e"></a> enumerator BK\_BLE\_SM\_IOCAP\_MODE
    :   The IO capability of local device, see bk\_io\_cap\_enum\_t.

    <a id="_CPPv4N17bk_ble_sm_param_t22BK_BLE_SM_SET_INIT_KEYE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t22BK_BLE_SM_SET_INIT_KEYE"></a> <a id="_CPPv2N17bk_ble_sm_param_t22BK_BLE_SM_SET_INIT_KEYE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064a508e188da550a8a115a9680c3cd74307"></a> enumerator BK\_BLE\_SM\_SET\_INIT\_KEY
    :   Initiator Key Distribution/Generation, use BK\_BLE\_SM\_SET\_LOCAL\_REMOTE\_KEY instead !!!

    <a id="_CPPv4N17bk_ble_sm_param_t21BK_BLE_SM_SET_RSP_KEYE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t21BK_BLE_SM_SET_RSP_KEYE"></a> <a id="_CPPv2N17bk_ble_sm_param_t21BK_BLE_SM_SET_RSP_KEYE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064a2b1d41526543c6b597c7b435bebde978"></a> enumerator BK\_BLE\_SM\_SET\_RSP\_KEY
    :   Responder Key Distribution/Generation, use BK\_BLE\_SM\_SET\_LOCAL\_REMOTE\_KEY instead !!!

    <a id="_CPPv4N17bk_ble_sm_param_t22BK_BLE_SM_MAX_KEY_SIZEE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t22BK_BLE_SM_MAX_KEY_SIZEE"></a> <a id="_CPPv2N17bk_ble_sm_param_t22BK_BLE_SM_MAX_KEY_SIZEE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064ae0c538ec3c5e63857b4a99c003443109"></a> enumerator BK\_BLE\_SM\_MAX\_KEY\_SIZE
    :   Maximum Encryption key size to support.

    <a id="_CPPv4N17bk_ble_sm_param_t22BK_BLE_SM_MIN_KEY_SIZEE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t22BK_BLE_SM_MIN_KEY_SIZEE"></a> <a id="_CPPv2N17bk_ble_sm_param_t22BK_BLE_SM_MIN_KEY_SIZEE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064ad59eb2777443f16efe21cd015a14f6fe"></a> enumerator BK\_BLE\_SM\_MIN\_KEY\_SIZE
    :   Minimum Encryption key size requirement from Peer.

    <a id="_CPPv4N17bk_ble_sm_param_t28BK_BLE_SM_SET_STATIC_PASSKEYE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t28BK_BLE_SM_SET_STATIC_PASSKEYE"></a> <a id="_CPPv2N17bk_ble_sm_param_t28BK_BLE_SM_SET_STATIC_PASSKEYE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064a32ad869d149063238cb76479ce6cda85"></a> enumerator BK\_BLE\_SM\_SET\_STATIC\_PASSKEY
    :   Set static Passkey.

    <a id="_CPPv4N17bk_ble_sm_param_t30BK_BLE_SM_CLEAR_STATIC_PASSKEYE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t30BK_BLE_SM_CLEAR_STATIC_PASSKEYE"></a> <a id="_CPPv2N17bk_ble_sm_param_t30BK_BLE_SM_CLEAR_STATIC_PASSKEYE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064a7299f30265738862ec843ce1f4a8aeda"></a> enumerator BK\_BLE\_SM\_CLEAR\_STATIC\_PASSKEY
    :   Reset static Passkey.

    <a id="_CPPv4N17bk_ble_sm_param_t40BK_BLE_SM_ONLY_ACCEPT_SPECIFIED_SEC_AUTHE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t40BK_BLE_SM_ONLY_ACCEPT_SPECIFIED_SEC_AUTHE"></a> <a id="_CPPv2N17bk_ble_sm_param_t40BK_BLE_SM_ONLY_ACCEPT_SPECIFIED_SEC_AUTHE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064acdf34f88eb8d5e500b3a749490f215d9"></a> enumerator BK\_BLE\_SM\_ONLY\_ACCEPT\_SPECIFIED\_SEC\_AUTH
    :   Accept only specified SMP Authentication requirement.

    <a id="_CPPv4N17bk_ble_sm_param_t21BK_BLE_SM_OOB_SUPPORTE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t21BK_BLE_SM_OOB_SUPPORTE"></a> <a id="_CPPv2N17bk_ble_sm_param_t21BK_BLE_SM_OOB_SUPPORTE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064a24dd8d55b46a566448394e40c2bc26d7"></a> enumerator BK\_BLE\_SM\_OOB\_SUPPORT
    :   Enable/Disable OOB support.

    <a id="_CPPv4N17bk_ble_sm_param_t16BK_BLE_SM_SET_ERE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t16BK_BLE_SM_SET_ERE"></a> <a id="_CPPv2N17bk_ble_sm_param_t16BK_BLE_SM_SET_ERE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064a18c91c1b2d9ff848824f0b76d34c5816"></a> enumerator BK\_BLE\_SM\_SET\_ER
    :   set ER, 16 bytes

    <a id="_CPPv4N17bk_ble_sm_param_t16BK_BLE_SM_SET_IRE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t16BK_BLE_SM_SET_IRE"></a> <a id="_CPPv2N17bk_ble_sm_param_t16BK_BLE_SM_SET_IRE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064a9a52c96525bb230056ba271a17666922"></a> enumerator BK\_BLE\_SM\_SET\_IR
    :   set IR, 16 bytes

    <a id="_CPPv4N17bk_ble_sm_param_t30BK_BLE_SM_SET_LOCAL_REMOTE_KEYE"></a>

    <a id="_CPPv3N17bk_ble_sm_param_t30BK_BLE_SM_SET_LOCAL_REMOTE_KEYE"></a> <a id="_CPPv2N17bk_ble_sm_param_t30BK_BLE_SM_SET_LOCAL_REMOTE_KEYE"></a> <a id="group__dm__gap__defines__v1_1gga3797c167c7f9030a70ee6aa4d7454064af0f12ac0b25b3909c62b0174fc22c03e"></a> enumerator BK\_BLE\_SM\_SET\_LOCAL\_REMOTE\_KEY
    :   local and remote init key, first 4 bits means local, last 4 bits means remote

<a id="_CPPv423bk_ble_key_distr_mask_t"></a>

<a id="_CPPv323bk_ble_key_distr_mask_t"></a> <a id="_CPPv223bk_ble_key_distr_mask_t"></a> <a id="group__dm__gap__defines__v1_1gabb33ea532ac1fe6b48380139f8d2e7a9"></a> enum bk\_ble\_key\_distr\_mask\_t
:   the key distribution mask type

    *Values:*

    <a id="_CPPv4N23bk_ble_key_distr_mask_t29BK_BLE_KEY_DISTR_ENC_KEY_MASKE"></a>

    <a id="_CPPv3N23bk_ble_key_distr_mask_t29BK_BLE_KEY_DISTR_ENC_KEY_MASKE"></a> <a id="_CPPv2N23bk_ble_key_distr_mask_t29BK_BLE_KEY_DISTR_ENC_KEY_MASKE"></a> <a id="group__dm__gap__defines__v1_1ggabb33ea532ac1fe6b48380139f8d2e7a9ab972c38e04f22fe20bab5bf69a1743d4"></a> enumerator BK\_BLE\_KEY\_DISTR\_ENC\_KEY\_MASK

    <a id="_CPPv4N23bk_ble_key_distr_mask_t28BK_BLE_KEY_DISTR_ID_KEY_MASKE"></a>

    <a id="_CPPv3N23bk_ble_key_distr_mask_t28BK_BLE_KEY_DISTR_ID_KEY_MASKE"></a> <a id="_CPPv2N23bk_ble_key_distr_mask_t28BK_BLE_KEY_DISTR_ID_KEY_MASKE"></a> <a id="group__dm__gap__defines__v1_1ggabb33ea532ac1fe6b48380139f8d2e7a9a3b4b2bf888bb2f7340aaabf976bbd83e"></a> enumerator BK\_BLE\_KEY\_DISTR\_ID\_KEY\_MASK
    :   Used to exchange the encryption key in the init key \& response key, not used now.

    <a id="_CPPv4N23bk_ble_key_distr_mask_t29BK_BLE_KEY_DISTR_CSR_KEY_MASKE"></a>

    <a id="_CPPv3N23bk_ble_key_distr_mask_t29BK_BLE_KEY_DISTR_CSR_KEY_MASKE"></a> <a id="_CPPv2N23bk_ble_key_distr_mask_t29BK_BLE_KEY_DISTR_CSR_KEY_MASKE"></a> <a id="group__dm__gap__defines__v1_1ggabb33ea532ac1fe6b48380139f8d2e7a9af7459173772f3927bb9b3b1998c6e2e3"></a> enumerator BK\_BLE\_KEY\_DISTR\_CSR\_KEY\_MASK
    :   Used to exchange the IRK key in the init key \& response key, not used now.

    <a id="_CPPv4N23bk_ble_key_distr_mask_t30BK_BLE_KEY_DISTR_LINK_KEY_MASKE"></a>

    <a id="_CPPv3N23bk_ble_key_distr_mask_t30BK_BLE_KEY_DISTR_LINK_KEY_MASKE"></a> <a id="_CPPv2N23bk_ble_key_distr_mask_t30BK_BLE_KEY_DISTR_LINK_KEY_MASKE"></a> <a id="group__dm__gap__defines__v1_1ggabb33ea532ac1fe6b48380139f8d2e7a9a67c82c19cc17208b86a7a4aab3574dce"></a> enumerator BK\_BLE\_KEY\_DISTR\_LINK\_KEY\_MASK
    :   Used to exchange the CSRK key in the init key \& response key, not used now.

        Used to exchange the link key(this key just used in the BLE \& BR/EDR coexist mode) in the init key \& response key, must used with BK\_LE\_AUTH\_REQ\_SC\_MITM\_BOND.

<a id="_CPPv418bk_ble_scan_type_t"></a>

<a id="_CPPv318bk_ble_scan_type_t"></a> <a id="_CPPv218bk_ble_scan_type_t"></a> <a id="group__dm__gap__defines__v1_1ga4c7b639106657ab274e2e965ee3df5d1"></a> enum bk\_ble\_scan\_type\_t
:   Ble scan type.

    *Values:*

    <a id="_CPPv4N18bk_ble_scan_type_t21BLE_SCAN_TYPE_PASSIVEE"></a>

    <a id="_CPPv3N18bk_ble_scan_type_t21BLE_SCAN_TYPE_PASSIVEE"></a> <a id="_CPPv2N18bk_ble_scan_type_t21BLE_SCAN_TYPE_PASSIVEE"></a> <a id="group__dm__gap__defines__v1_1gga4c7b639106657ab274e2e965ee3df5d1a5f75e05208682d64caadd5e0c457080f"></a> enumerator BLE\_SCAN\_TYPE\_PASSIVE
    :   Passive scan

    <a id="_CPPv4N18bk_ble_scan_type_t20BLE_SCAN_TYPE_ACTIVEE"></a>

    <a id="_CPPv3N18bk_ble_scan_type_t20BLE_SCAN_TYPE_ACTIVEE"></a> <a id="_CPPv2N18bk_ble_scan_type_t20BLE_SCAN_TYPE_ACTIVEE"></a> <a id="group__dm__gap__defines__v1_1gga4c7b639106657ab274e2e965ee3df5d1ae41ddebf30ab44c32df8f10c3bbe98dc"></a> enumerator BLE\_SCAN\_TYPE\_ACTIVE
    :   Active scan

<a id="_CPPv420bk_ble_scan_filter_t"></a>

<a id="_CPPv320bk_ble_scan_filter_t"></a> <a id="_CPPv220bk_ble_scan_filter_t"></a> <a id="group__dm__gap__defines__v1_1gaa0832d79fda02b77aaf6b469ba20e79f"></a> enum bk\_ble\_scan\_filter\_t
:   Ble scan filter type.

    *Values:*

    <a id="_CPPv4N20bk_ble_scan_filter_t25BLE_SCAN_FILTER_ALLOW_ALLE"></a>

    <a id="_CPPv3N20bk_ble_scan_filter_t25BLE_SCAN_FILTER_ALLOW_ALLE"></a> <a id="_CPPv2N20bk_ble_scan_filter_t25BLE_SCAN_FILTER_ALLOW_ALLE"></a> <a id="group__dm__gap__defines__v1_1ggaa0832d79fda02b77aaf6b469ba20e79fa244391edffc03acd1bcb4c305c53e7f0"></a> enumerator BLE\_SCAN\_FILTER\_ALLOW\_ALL
    :   Accept all :

        1. advertisement packets except directed advertising packets not addressed to this device (default).

    <a id="_CPPv4N20bk_ble_scan_filter_t31BLE_SCAN_FILTER_ALLOW_ONLY_WLSTE"></a>

    <a id="_CPPv3N20bk_ble_scan_filter_t31BLE_SCAN_FILTER_ALLOW_ONLY_WLSTE"></a> <a id="_CPPv2N20bk_ble_scan_filter_t31BLE_SCAN_FILTER_ALLOW_ONLY_WLSTE"></a> <a id="group__dm__gap__defines__v1_1ggaa0832d79fda02b77aaf6b469ba20e79fadadd26a05a98c69f5feb3b51ff98a8f7"></a> enumerator BLE\_SCAN\_FILTER\_ALLOW\_ONLY\_WLST
    :   Accept only :

        1. advertisement packets from devices where the advertiser’s address is in the White list.
        2. Directed advertising packets which are not addressed for this device shall be ignored.

    <a id="_CPPv4N20bk_ble_scan_filter_t33BLE_SCAN_FILTER_ALLOW_UND_RPA_DIRE"></a>

    <a id="_CPPv3N20bk_ble_scan_filter_t33BLE_SCAN_FILTER_ALLOW_UND_RPA_DIRE"></a> <a id="_CPPv2N20bk_ble_scan_filter_t33BLE_SCAN_FILTER_ALLOW_UND_RPA_DIRE"></a> <a id="group__dm__gap__defines__v1_1ggaa0832d79fda02b77aaf6b469ba20e79fab3babad073a0a4e1d07de308e6c36c6b"></a> enumerator BLE\_SCAN\_FILTER\_ALLOW\_UND\_RPA\_DIR
    :   Accept all :

        1. undirected advertisement packets, and
        2. directed advertising packets where the initiator address is a resolvable private address, and
        3. directed advertising packets addressed to this device.

    <a id="_CPPv4N20bk_ble_scan_filter_t35BLE_SCAN_FILTER_ALLOW_WLIST_RPA_DIRE"></a>

    <a id="_CPPv3N20bk_ble_scan_filter_t35BLE_SCAN_FILTER_ALLOW_WLIST_RPA_DIRE"></a> <a id="_CPPv2N20bk_ble_scan_filter_t35BLE_SCAN_FILTER_ALLOW_WLIST_RPA_DIRE"></a> <a id="group__dm__gap__defines__v1_1ggaa0832d79fda02b77aaf6b469ba20e79faa07081e3890e3f3b7c063035c532bc4d"></a> enumerator BLE\_SCAN\_FILTER\_ALLOW\_WLIST\_RPA\_DIR
    :   Accept all :

        1. advertisement packets from devices where the advertiser’s address is in the White list, and
        2. directed advertising packets where the initiator address is a resolvable private address, and
        3. directed advertising packets addressed to this device.

<a id="_CPPv423bk_ble_scan_duplicate_t"></a>

<a id="_CPPv323bk_ble_scan_duplicate_t"></a> <a id="_CPPv223bk_ble_scan_duplicate_t"></a> <a id="group__dm__gap__defines__v1_1gabfe0955838dbc2f6f2d12040c70097aa"></a> enum bk\_ble\_scan\_duplicate\_t
:   Ble scan duplicate type.

    *Values:*

    <a id="_CPPv4N23bk_ble_scan_duplicate_t26BLE_SCAN_DUPLICATE_DISABLEE"></a>

    <a id="_CPPv3N23bk_ble_scan_duplicate_t26BLE_SCAN_DUPLICATE_DISABLEE"></a> <a id="_CPPv2N23bk_ble_scan_duplicate_t26BLE_SCAN_DUPLICATE_DISABLEE"></a> <a id="group__dm__gap__defines__v1_1ggabfe0955838dbc2f6f2d12040c70097aaaf534b4f49a06771d43074fa5b6d7b55f"></a> enumerator BLE\_SCAN\_DUPLICATE\_DISABLE
    :   the Link Layer should generate advertising reports to the host for each packet received

    <a id="_CPPv4N23bk_ble_scan_duplicate_t25BLE_SCAN_DUPLICATE_ENABLEE"></a>

    <a id="_CPPv3N23bk_ble_scan_duplicate_t25BLE_SCAN_DUPLICATE_ENABLEE"></a> <a id="_CPPv2N23bk_ble_scan_duplicate_t25BLE_SCAN_DUPLICATE_ENABLEE"></a> <a id="group__dm__gap__defines__v1_1ggabfe0955838dbc2f6f2d12040c70097aaa0f4bb038e4ae023d5b5abef427e37ae7"></a> enumerator BLE\_SCAN\_DUPLICATE\_ENABLE
    :   the Link Layer should filter out duplicate advertising reports to the Host

    <a id="_CPPv4N23bk_ble_scan_duplicate_t22BLE_SCAN_DUPLICATE_MAXE"></a>

    <a id="_CPPv3N23bk_ble_scan_duplicate_t22BLE_SCAN_DUPLICATE_MAXE"></a> <a id="_CPPv2N23bk_ble_scan_duplicate_t22BLE_SCAN_DUPLICATE_MAXE"></a> <a id="group__dm__gap__defines__v1_1ggabfe0955838dbc2f6f2d12040c70097aaad0a0844bcee5da2696dfd335c7af3f2a"></a> enumerator BLE\_SCAN\_DUPLICATE\_MAX
    :   0x02 – 0xFF, Reserved for future use

<a id="_CPPv423bk_ble_security_level_t"></a>

<a id="_CPPv323bk_ble_security_level_t"></a> <a id="_CPPv223bk_ble_security_level_t"></a> <a id="group__dm__gap__defines__v1_1ga2f6fa99eb5c300f0075548180152a447"></a> enum bk\_ble\_security\_level\_t
:   *Values:*

    <a id="_CPPv4N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_1E"></a>

    <a id="_CPPv3N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_1E"></a> <a id="_CPPv2N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_1E"></a> <a id="group__dm__gap__defines__v1_1gga2f6fa99eb5c300f0075548180152a447a8f78cdecca6b97a26acdb335d26d6f75"></a> enumerator BK\_BLE\_SECURITY\_LEVEL\_1

    <a id="_CPPv4N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_2E"></a>

    <a id="_CPPv3N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_2E"></a> <a id="_CPPv2N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_2E"></a> <a id="group__dm__gap__defines__v1_1gga2f6fa99eb5c300f0075548180152a447a9d4b5cce2816da5249d3aac8722f4cf8"></a> enumerator BK\_BLE\_SECURITY\_LEVEL\_2

    <a id="_CPPv4N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_3E"></a>

    <a id="_CPPv3N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_3E"></a> <a id="_CPPv2N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_3E"></a> <a id="group__dm__gap__defines__v1_1gga2f6fa99eb5c300f0075548180152a447a97dd3dcbf65518ad3225a2042f77ae00"></a> enumerator BK\_BLE\_SECURITY\_LEVEL\_3

    <a id="_CPPv4N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_4E"></a>

    <a id="_CPPv3N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_4E"></a> <a id="_CPPv2N23bk_ble_security_level_t23BK_BLE_SECURITY_LEVEL_4E"></a> <a id="group__dm__gap__defines__v1_1gga2f6fa99eb5c300f0075548180152a447a6a69f3bd7222a1756a7a3e1d66da9953"></a> enumerator BK\_BLE\_SECURITY\_LEVEL\_4

<a id="_CPPv432bk_gap_bond_dev_list_operation_t"></a>

<a id="_CPPv332bk_gap_bond_dev_list_operation_t"></a> <a id="_CPPv232bk_gap_bond_dev_list_operation_t"></a> <a id="group__dm__gap__defines__v1_1gae8c52862fe2857be73adfd732e62f962"></a> enum bk\_gap\_bond\_dev\_list\_operation\_t
:   bond dev list operation

    *Values:*

    <a id="_CPPv4N32bk_gap_bond_dev_list_operation_t34BK_GAP_BOND_DEV_LIST_OPERATION_ADDE"></a>

    <a id="_CPPv3N32bk_gap_bond_dev_list_operation_t34BK_GAP_BOND_DEV_LIST_OPERATION_ADDE"></a> <a id="_CPPv2N32bk_gap_bond_dev_list_operation_t34BK_GAP_BOND_DEV_LIST_OPERATION_ADDE"></a> <a id="group__dm__gap__defines__v1_1ggae8c52862fe2857be73adfd732e62f962a5a90f15f19a1d035600b55478abbf2a8"></a> enumerator BK\_GAP\_BOND\_DEV\_LIST\_OPERATION\_ADD

    <a id="_CPPv4N32bk_gap_bond_dev_list_operation_t37BK_GAP_BOND_DEV_LIST_OPERATION_REMOVEE"></a>

    <a id="_CPPv3N32bk_gap_bond_dev_list_operation_t37BK_GAP_BOND_DEV_LIST_OPERATION_REMOVEE"></a> <a id="_CPPv2N32bk_gap_bond_dev_list_operation_t37BK_GAP_BOND_DEV_LIST_OPERATION_REMOVEE"></a> <a id="group__dm__gap__defines__v1_1ggae8c52862fe2857be73adfd732e62f962aabbc17939cb55439ab69b9507d6cfb3a"></a> enumerator BK\_GAP\_BOND\_DEV\_LIST\_OPERATION\_REMOVE

    <a id="_CPPv4N32bk_gap_bond_dev_list_operation_t36BK_GAP_BOND_DEV_LIST_OPERATION_CLEANE"></a>

    <a id="_CPPv3N32bk_gap_bond_dev_list_operation_t36BK_GAP_BOND_DEV_LIST_OPERATION_CLEANE"></a> <a id="_CPPv2N32bk_gap_bond_dev_list_operation_t36BK_GAP_BOND_DEV_LIST_OPERATION_CLEANE"></a> <a id="group__dm__gap__defines__v1_1ggae8c52862fe2857be73adfd732e62f962adf85bbab6325c396da752701205a6902"></a> enumerator BK\_GAP\_BOND\_DEV\_LIST\_OPERATION\_CLEAN

<a id="_CPPv419bk_gap_search_evt_t"></a>

<a id="_CPPv319bk_gap_search_evt_t"></a> <a id="_CPPv219bk_gap_search_evt_t"></a> <a id="group__dm__gap__defines__v1_1gae1edfed382858299908335bc07b842ba"></a> enum bk\_gap\_search\_evt\_t
:   Sub Event of BK\_BLE\_GAP\_SCAN\_RESULT\_EVT.

    *Values:*

    <a id="_CPPv4N19bk_gap_search_evt_t25BK_GAP_SEARCH_INQ_RES_EVTE"></a>

    <a id="_CPPv3N19bk_gap_search_evt_t25BK_GAP_SEARCH_INQ_RES_EVTE"></a> <a id="_CPPv2N19bk_gap_search_evt_t25BK_GAP_SEARCH_INQ_RES_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggae1edfed382858299908335bc07b842baa342d7a5c9004f7093dfbeb9d1ec72327"></a> enumerator BK\_GAP\_SEARCH\_INQ\_RES\_EVT
    :   Inquiry result for a peer device.

    <a id="_CPPv4N19bk_gap_search_evt_t26BK_GAP_SEARCH_INQ_CMPL_EVTE"></a>

    <a id="_CPPv3N19bk_gap_search_evt_t26BK_GAP_SEARCH_INQ_CMPL_EVTE"></a> <a id="_CPPv2N19bk_gap_search_evt_t26BK_GAP_SEARCH_INQ_CMPL_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggae1edfed382858299908335bc07b842baa40b379b4cc33e86653ee6559055bfdf7"></a> enumerator BK\_GAP\_SEARCH\_INQ\_CMPL\_EVT
    :   Inquiry complete.

    <a id="_CPPv4N19bk_gap_search_evt_t26BK_GAP_SEARCH_DISC_RES_EVTE"></a>

    <a id="_CPPv3N19bk_gap_search_evt_t26BK_GAP_SEARCH_DISC_RES_EVTE"></a> <a id="_CPPv2N19bk_gap_search_evt_t26BK_GAP_SEARCH_DISC_RES_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggae1edfed382858299908335bc07b842baa3bdacd63b4bd771719695867488dec07"></a> enumerator BK\_GAP\_SEARCH\_DISC\_RES\_EVT
    :   Discovery result for a peer device.

    <a id="_CPPv4N19bk_gap_search_evt_t30BK_GAP_SEARCH_DISC_BLE_RES_EVTE"></a>

    <a id="_CPPv3N19bk_gap_search_evt_t30BK_GAP_SEARCH_DISC_BLE_RES_EVTE"></a> <a id="_CPPv2N19bk_gap_search_evt_t30BK_GAP_SEARCH_DISC_BLE_RES_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggae1edfed382858299908335bc07b842baa4eca5c40c6398477e17ad10e34e24e5c"></a> enumerator BK\_GAP\_SEARCH\_DISC\_BLE\_RES\_EVT
    :   Discovery result for BLE GATT based service on a peer device.

    <a id="_CPPv4N19bk_gap_search_evt_t27BK_GAP_SEARCH_DISC_CMPL_EVTE"></a>

    <a id="_CPPv3N19bk_gap_search_evt_t27BK_GAP_SEARCH_DISC_CMPL_EVTE"></a> <a id="_CPPv2N19bk_gap_search_evt_t27BK_GAP_SEARCH_DISC_CMPL_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggae1edfed382858299908335bc07b842baa8eae4951461dff3df8f23c469e84f8c8"></a> enumerator BK\_GAP\_SEARCH\_DISC\_CMPL\_EVT
    :   Discovery complete.

    <a id="_CPPv4N19bk_gap_search_evt_t30BK_GAP_SEARCH_DI_DISC_CMPL_EVTE"></a>

    <a id="_CPPv3N19bk_gap_search_evt_t30BK_GAP_SEARCH_DI_DISC_CMPL_EVTE"></a> <a id="_CPPv2N19bk_gap_search_evt_t30BK_GAP_SEARCH_DI_DISC_CMPL_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggae1edfed382858299908335bc07b842baa4577f4f9556c8b43c4aa10884fcddad6"></a> enumerator BK\_GAP\_SEARCH\_DI\_DISC\_CMPL\_EVT
    :   Discovery complete.

    <a id="_CPPv4N19bk_gap_search_evt_t36BK_GAP_SEARCH_SEARCH_CANCEL_CMPL_EVTE"></a>

    <a id="_CPPv3N19bk_gap_search_evt_t36BK_GAP_SEARCH_SEARCH_CANCEL_CMPL_EVTE"></a> <a id="_CPPv2N19bk_gap_search_evt_t36BK_GAP_SEARCH_SEARCH_CANCEL_CMPL_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggae1edfed382858299908335bc07b842baa09d1a2e61096ac317e75e162799b0e4a"></a> enumerator BK\_GAP\_SEARCH\_SEARCH\_CANCEL\_CMPL\_EVT
    :   Search cancelled

    <a id="_CPPv4N19bk_gap_search_evt_t33BK_GAP_SEARCH_INQ_DISCARD_NUM_EVTE"></a>

    <a id="_CPPv3N19bk_gap_search_evt_t33BK_GAP_SEARCH_INQ_DISCARD_NUM_EVTE"></a> <a id="_CPPv2N19bk_gap_search_evt_t33BK_GAP_SEARCH_INQ_DISCARD_NUM_EVTE"></a> <a id="group__dm__gap__defines__v1_1ggae1edfed382858299908335bc07b842baad1fa34fae91b65852cc6799d49989fbe"></a> enumerator BK\_GAP\_SEARCH\_INQ\_DISCARD\_NUM\_EVT
    :   The number of pkt discarded by flow control

<a id="_CPPv417bk_ble_evt_type_t"></a>

<a id="_CPPv317bk_ble_evt_type_t"></a> <a id="_CPPv217bk_ble_evt_type_t"></a> <a id="group__dm__gap__defines__v1_1gaad0049934e2ae1a8df005997c985a3a3"></a> enum bk\_ble\_evt\_type\_t
:   Ble scan result event type, to indicate the result is scan response or advertising data or other.

    *Values:*

    <a id="_CPPv4N17bk_ble_evt_type_t19BK_BLE_EVT_CONN_ADVE"></a>

    <a id="_CPPv3N17bk_ble_evt_type_t19BK_BLE_EVT_CONN_ADVE"></a> <a id="_CPPv2N17bk_ble_evt_type_t19BK_BLE_EVT_CONN_ADVE"></a> <a id="group__dm__gap__defines__v1_1ggaad0049934e2ae1a8df005997c985a3a3a5fd137086a3c24297b31f854037f7643"></a> enumerator BK\_BLE\_EVT\_CONN\_ADV
    :   Connectable undirected advertising (ADV\_IND)

    <a id="_CPPv4N17bk_ble_evt_type_t23BK_BLE_EVT_CONN_DIR_ADVE"></a>

    <a id="_CPPv3N17bk_ble_evt_type_t23BK_BLE_EVT_CONN_DIR_ADVE"></a> <a id="_CPPv2N17bk_ble_evt_type_t23BK_BLE_EVT_CONN_DIR_ADVE"></a> <a id="group__dm__gap__defines__v1_1ggaad0049934e2ae1a8df005997c985a3a3ae7822ae855c56d18cd42a9eb11e0d6cc"></a> enumerator BK\_BLE\_EVT\_CONN\_DIR\_ADV
    :   Connectable directed advertising (ADV\_DIRECT\_IND)

    <a id="_CPPv4N17bk_ble_evt_type_t19BK_BLE_EVT_DISC_ADVE"></a>

    <a id="_CPPv3N17bk_ble_evt_type_t19BK_BLE_EVT_DISC_ADVE"></a> <a id="_CPPv2N17bk_ble_evt_type_t19BK_BLE_EVT_DISC_ADVE"></a> <a id="group__dm__gap__defines__v1_1ggaad0049934e2ae1a8df005997c985a3a3a8706392b7fe0ea96b5dba00d9bb88a3c"></a> enumerator BK\_BLE\_EVT\_DISC\_ADV
    :   Scannable undirected advertising (ADV\_SCAN\_IND)

    <a id="_CPPv4N17bk_ble_evt_type_t23BK_BLE_EVT_NON_CONN_ADVE"></a>

    <a id="_CPPv3N17bk_ble_evt_type_t23BK_BLE_EVT_NON_CONN_ADVE"></a> <a id="_CPPv2N17bk_ble_evt_type_t23BK_BLE_EVT_NON_CONN_ADVE"></a> <a id="group__dm__gap__defines__v1_1ggaad0049934e2ae1a8df005997c985a3a3a8e7ccbef2a142bb9978c006643524098"></a> enumerator BK\_BLE\_EVT\_NON\_CONN\_ADV
    :   Non connectable undirected advertising (ADV\_NONCONN\_IND)

    <a id="_CPPv4N17bk_ble_evt_type_t19BK_BLE_EVT_SCAN_RSPE"></a>

    <a id="_CPPv3N17bk_ble_evt_type_t19BK_BLE_EVT_SCAN_RSPE"></a> <a id="_CPPv2N17bk_ble_evt_type_t19BK_BLE_EVT_SCAN_RSPE"></a> <a id="group__dm__gap__defines__v1_1ggaad0049934e2ae1a8df005997c985a3a3a7002e5f234cf9042b7fea5481efc498c"></a> enumerator BK\_BLE\_EVT\_SCAN\_RSP
    :   Scan Response (SCAN\_RSP)

<a id="_CPPv421bk_ble_wl_operation_t"></a>

<a id="_CPPv321bk_ble_wl_operation_t"></a> <a id="_CPPv221bk_ble_wl_operation_t"></a> <a id="group__dm__gap__defines__v1_1ga7879b1447e8067d2b09e1142f8f38c7d"></a> enum bk\_ble\_wl\_operation\_t
:   white list op

    *Values:*

    <a id="_CPPv4N21bk_ble_wl_operation_t23BK_BLE_WHITELIST_REMOVEE"></a>

    <a id="_CPPv3N21bk_ble_wl_operation_t23BK_BLE_WHITELIST_REMOVEE"></a> <a id="_CPPv2N21bk_ble_wl_operation_t23BK_BLE_WHITELIST_REMOVEE"></a> <a id="group__dm__gap__defines__v1_1gga7879b1447e8067d2b09e1142f8f38c7da4a771b771ffafc410810fb7fcb30e572"></a> enumerator BK\_BLE\_WHITELIST\_REMOVE
    :   remove mac from whitelist

    <a id="_CPPv4N21bk_ble_wl_operation_t20BK_BLE_WHITELIST_ADDE"></a>

    <a id="_CPPv3N21bk_ble_wl_operation_t20BK_BLE_WHITELIST_ADDE"></a> <a id="_CPPv2N21bk_ble_wl_operation_t20BK_BLE_WHITELIST_ADDE"></a> <a id="group__dm__gap__defines__v1_1gga7879b1447e8067d2b09e1142f8f38c7da3b8b5e21640d77de1ceceb6f82da182f"></a> enumerator BK\_BLE\_WHITELIST\_ADD
    :   add address to whitelist

    <a id="_CPPv4N21bk_ble_wl_operation_t22BK_BLE_WHITELIST_CLEANE"></a>

    <a id="_CPPv3N21bk_ble_wl_operation_t22BK_BLE_WHITELIST_CLEANE"></a> <a id="_CPPv2N21bk_ble_wl_operation_t22BK_BLE_WHITELIST_CLEANE"></a> <a id="group__dm__gap__defines__v1_1gga7879b1447e8067d2b09e1142f8f38c7daf5174debb58f58a88fd0fd4048f20c39"></a> enumerator BK\_BLE\_WHITELIST\_CLEAN
    :   clean whitelist

<a id="_CPPv429bk_ble_gap_set_ext_adv_prop_t"></a>

<a id="_CPPv329bk_ble_gap_set_ext_adv_prop_t"></a> <a id="_CPPv229bk_ble_gap_set_ext_adv_prop_t"></a> <a id="group__dm__gap__defines__v1_1gabcd47bc92fdd005c8c7ef1f2b39aa248"></a> enum bk\_ble\_gap\_set\_ext\_adv\_prop\_t
:   ext adv prop

    *Values:*

    <a id="_CPPv4N29bk_ble_gap_set_ext_adv_prop_t59BK_BLE_GAP_SET_EXT_ADV_PROP_NONCONN_NONSCANNABLE_UNDIRECTEDE"></a>

    <a id="_CPPv3N29bk_ble_gap_set_ext_adv_prop_t59BK_BLE_GAP_SET_EXT_ADV_PROP_NONCONN_NONSCANNABLE_UNDIRECTEDE"></a> <a id="_CPPv2N29bk_ble_gap_set_ext_adv_prop_t59BK_BLE_GAP_SET_EXT_ADV_PROP_NONCONN_NONSCANNABLE_UNDIRECTEDE"></a> <a id="group__dm__gap__defines__v1_1ggabcd47bc92fdd005c8c7ef1f2b39aa248a8afec3f97c19292de81a2078b6cbb552"></a> enumerator BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_NONCONN\_NONSCANNABLE\_UNDIRECTED
    :   Non-Connectable and Non-Scannable Undirected advertising

    <a id="_CPPv4N29bk_ble_gap_set_ext_adv_prop_t39BK_BLE_GAP_SET_EXT_ADV_PROP_CONNECTABLEE"></a>

    <a id="_CPPv3N29bk_ble_gap_set_ext_adv_prop_t39BK_BLE_GAP_SET_EXT_ADV_PROP_CONNECTABLEE"></a> <a id="_CPPv2N29bk_ble_gap_set_ext_adv_prop_t39BK_BLE_GAP_SET_EXT_ADV_PROP_CONNECTABLEE"></a> <a id="group__dm__gap__defines__v1_1ggabcd47bc92fdd005c8c7ef1f2b39aa248a379935d75752f0e18bb63de4c94c66c5"></a> enumerator BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_CONNECTABLE
    :   Connectable advertising

    <a id="_CPPv4N29bk_ble_gap_set_ext_adv_prop_t37BK_BLE_GAP_SET_EXT_ADV_PROP_SCANNABLEE"></a>

    <a id="_CPPv3N29bk_ble_gap_set_ext_adv_prop_t37BK_BLE_GAP_SET_EXT_ADV_PROP_SCANNABLEE"></a> <a id="_CPPv2N29bk_ble_gap_set_ext_adv_prop_t37BK_BLE_GAP_SET_EXT_ADV_PROP_SCANNABLEE"></a> <a id="group__dm__gap__defines__v1_1ggabcd47bc92fdd005c8c7ef1f2b39aa248ab017fffebe27add973900bdcc9cdc239"></a> enumerator BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_SCANNABLE
    :   Scannable advertising

    <a id="_CPPv4N29bk_ble_gap_set_ext_adv_prop_t36BK_BLE_GAP_SET_EXT_ADV_PROP_DIRECTEDE"></a>

    <a id="_CPPv3N29bk_ble_gap_set_ext_adv_prop_t36BK_BLE_GAP_SET_EXT_ADV_PROP_DIRECTEDE"></a> <a id="_CPPv2N29bk_ble_gap_set_ext_adv_prop_t36BK_BLE_GAP_SET_EXT_ADV_PROP_DIRECTEDE"></a> <a id="group__dm__gap__defines__v1_1ggabcd47bc92fdd005c8c7ef1f2b39aa248a0770639933922960b916f2ef7576e1ef"></a> enumerator BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_DIRECTED
    :   Directed advertising

    <a id="_CPPv4N29bk_ble_gap_set_ext_adv_prop_t39BK_BLE_GAP_SET_EXT_ADV_PROP_HD_DIRECTEDE"></a>

    <a id="_CPPv3N29bk_ble_gap_set_ext_adv_prop_t39BK_BLE_GAP_SET_EXT_ADV_PROP_HD_DIRECTEDE"></a> <a id="_CPPv2N29bk_ble_gap_set_ext_adv_prop_t39BK_BLE_GAP_SET_EXT_ADV_PROP_HD_DIRECTEDE"></a> <a id="group__dm__gap__defines__v1_1ggabcd47bc92fdd005c8c7ef1f2b39aa248a6a17f8dce0129dd93e9bf71da68167b0"></a> enumerator BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_HD\_DIRECTED
    :   High Duty Cycle Directed Connectable advertising (\<\= 3.75 ms Advertising Interval)

    <a id="_CPPv4N29bk_ble_gap_set_ext_adv_prop_t34BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACYE"></a>

    <a id="_CPPv3N29bk_ble_gap_set_ext_adv_prop_t34BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACYE"></a> <a id="_CPPv2N29bk_ble_gap_set_ext_adv_prop_t34BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACYE"></a> <a id="group__dm__gap__defines__v1_1ggabcd47bc92fdd005c8c7ef1f2b39aa248ae3ad1821d06952d32110bf3d29f32e87"></a> enumerator BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_LEGACY
    :   Use legacy advertising PDUs

    <a id="_CPPv4N29bk_ble_gap_set_ext_adv_prop_t36BK_BLE_GAP_SET_EXT_ADV_PROP_ANON_ADVE"></a>

    <a id="_CPPv3N29bk_ble_gap_set_ext_adv_prop_t36BK_BLE_GAP_SET_EXT_ADV_PROP_ANON_ADVE"></a> <a id="_CPPv2N29bk_ble_gap_set_ext_adv_prop_t36BK_BLE_GAP_SET_EXT_ADV_PROP_ANON_ADVE"></a> <a id="group__dm__gap__defines__v1_1ggabcd47bc92fdd005c8c7ef1f2b39aa248a62a02db768b91be4684032708c2b852a"></a> enumerator BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_ANON\_ADV
    :   Omit advertiser’s address from all PDUs (“anonymous advertising”)

    <a id="_CPPv4N29bk_ble_gap_set_ext_adv_prop_t42BK_BLE_GAP_SET_EXT_ADV_PROP_INCLUDE_TX_PWRE"></a>

    <a id="_CPPv3N29bk_ble_gap_set_ext_adv_prop_t42BK_BLE_GAP_SET_EXT_ADV_PROP_INCLUDE_TX_PWRE"></a> <a id="_CPPv2N29bk_ble_gap_set_ext_adv_prop_t42BK_BLE_GAP_SET_EXT_ADV_PROP_INCLUDE_TX_PWRE"></a> <a id="group__dm__gap__defines__v1_1ggabcd47bc92fdd005c8c7ef1f2b39aa248ada3fbf316c1bedbaecc67223304353b3"></a> enumerator BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_INCLUDE\_TX\_PWR
    :   Include TxPower in the extended header of the advertising PDU

    <a id="_CPPv4N29bk_ble_gap_set_ext_adv_prop_t32BK_BLE_GAP_SET_EXT_ADV_PROP_MASKE"></a>

    <a id="_CPPv3N29bk_ble_gap_set_ext_adv_prop_t32BK_BLE_GAP_SET_EXT_ADV_PROP_MASKE"></a> <a id="_CPPv2N29bk_ble_gap_set_ext_adv_prop_t32BK_BLE_GAP_SET_EXT_ADV_PROP_MASKE"></a> <a id="group__dm__gap__defines__v1_1ggabcd47bc92fdd005c8c7ef1f2b39aa248a71a04a2ef53435b7d03aff0c40719e0a"></a> enumerator BK\_BLE\_GAP\_SET\_EXT\_ADV\_PROP\_MASK
    :   Reserved for future use

<a id="_CPPv421bk_ble_gap_phy_enum_t"></a>

<a id="_CPPv321bk_ble_gap_phy_enum_t"></a> <a id="_CPPv221bk_ble_gap_phy_enum_t"></a> <a id="group__dm__gap__defines__v1_1ga732f14d4c8de9f1374db68d20e4e0c1f"></a> enum bk\_ble\_gap\_phy\_enum\_t
:   *Values:*

    <a id="_CPPv4N21bk_ble_gap_phy_enum_t17BK_BLE_GAP_PHY_1ME"></a>

    <a id="_CPPv3N21bk_ble_gap_phy_enum_t17BK_BLE_GAP_PHY_1ME"></a> <a id="_CPPv2N21bk_ble_gap_phy_enum_t17BK_BLE_GAP_PHY_1ME"></a> <a id="group__dm__gap__defines__v1_1gga732f14d4c8de9f1374db68d20e4e0c1face709b04b6fa9b42abab1f0695dc24d5"></a> enumerator BK\_BLE\_GAP\_PHY\_1M
    :   Secondery Advertisement PHY is LE1M

    <a id="_CPPv4N21bk_ble_gap_phy_enum_t17BK_BLE_GAP_PHY_2ME"></a>

    <a id="_CPPv3N21bk_ble_gap_phy_enum_t17BK_BLE_GAP_PHY_2ME"></a> <a id="_CPPv2N21bk_ble_gap_phy_enum_t17BK_BLE_GAP_PHY_2ME"></a> <a id="group__dm__gap__defines__v1_1gga732f14d4c8de9f1374db68d20e4e0c1fadf2288f2b137e69469caa7cac117bb29"></a> enumerator BK\_BLE\_GAP\_PHY\_2M
    :   Secondery Advertisement PHY is LE2M

    <a id="_CPPv4N21bk_ble_gap_phy_enum_t20BK_BLE_GAP_PHY_CODEDE"></a>

    <a id="_CPPv3N21bk_ble_gap_phy_enum_t20BK_BLE_GAP_PHY_CODEDE"></a> <a id="_CPPv2N21bk_ble_gap_phy_enum_t20BK_BLE_GAP_PHY_CODEDE"></a> <a id="group__dm__gap__defines__v1_1gga732f14d4c8de9f1374db68d20e4e0c1fac8462199251ba7301b278ac6bf4bc58f"></a> enumerator BK\_BLE\_GAP\_PHY\_CODED
    :   Secondery Advertisement PHY is LE Coded

<a id="_CPPv426bk_ble_gap_noprefer_enum_t"></a>

<a id="_CPPv326bk_ble_gap_noprefer_enum_t"></a> <a id="_CPPv226bk_ble_gap_noprefer_enum_t"></a> <a id="group__dm__gap__defines__v1_1ga7fd8fa2d799830afacabf90dbf80c625"></a> enum bk\_ble\_gap\_noprefer\_enum\_t
:   ble gap noprefer phy

    *Values:*

    <a id="_CPPv4N26bk_ble_gap_noprefer_enum_t33BK_BLE_GAP_NO_PREFER_TRANSMIT_PHYE"></a>

    <a id="_CPPv3N26bk_ble_gap_noprefer_enum_t33BK_BLE_GAP_NO_PREFER_TRANSMIT_PHYE"></a> <a id="_CPPv2N26bk_ble_gap_noprefer_enum_t33BK_BLE_GAP_NO_PREFER_TRANSMIT_PHYE"></a> <a id="group__dm__gap__defines__v1_1gga7fd8fa2d799830afacabf90dbf80c625a1e214b85ced59e22620a821c462b1fc3"></a> enumerator BK\_BLE\_GAP\_NO\_PREFER\_TRANSMIT\_PHY
    :   No Prefer TX PHY supported by controller

    <a id="_CPPv4N26bk_ble_gap_noprefer_enum_t32BK_BLE_GAP_NO_PREFER_RECEIVE_PHYE"></a>

    <a id="_CPPv3N26bk_ble_gap_noprefer_enum_t32BK_BLE_GAP_NO_PREFER_RECEIVE_PHYE"></a> <a id="_CPPv2N26bk_ble_gap_noprefer_enum_t32BK_BLE_GAP_NO_PREFER_RECEIVE_PHYE"></a> <a id="group__dm__gap__defines__v1_1gga7fd8fa2d799830afacabf90dbf80c625ab94529fa6da65d215589561948ba7785"></a> enumerator BK\_BLE\_GAP\_NO\_PREFER\_RECEIVE\_PHY
    :   No Prefer RX PHY supported by controller

<a id="_CPPv425bk_ble_gap_pri_phy_enum_t"></a>

<a id="_CPPv325bk_ble_gap_pri_phy_enum_t"></a> <a id="_CPPv225bk_ble_gap_pri_phy_enum_t"></a> <a id="group__dm__gap__defines__v1_1ga22cc153ad39f0a4ed1ad8196af85b5f9"></a> enum bk\_ble\_gap\_pri\_phy\_enum\_t
:   Primary phy only support 1M and LE coded phy.

    *Values:*

    <a id="_CPPv4N25bk_ble_gap_pri_phy_enum_t21BK_BLE_GAP_PRI_PHY_1ME"></a>

    <a id="_CPPv3N25bk_ble_gap_pri_phy_enum_t21BK_BLE_GAP_PRI_PHY_1ME"></a> <a id="_CPPv2N25bk_ble_gap_pri_phy_enum_t21BK_BLE_GAP_PRI_PHY_1ME"></a> <a id="group__dm__gap__defines__v1_1gga22cc153ad39f0a4ed1ad8196af85b5f9a8761d1ef0f0947a00c1679bd966c9abb"></a> enumerator BK\_BLE\_GAP\_PRI\_PHY\_1M
    :   Primary Phy is LE1M

    <a id="_CPPv4N25bk_ble_gap_pri_phy_enum_t24BK_BLE_GAP_PRI_PHY_CODEDE"></a>

    <a id="_CPPv3N25bk_ble_gap_pri_phy_enum_t24BK_BLE_GAP_PRI_PHY_CODEDE"></a> <a id="_CPPv2N25bk_ble_gap_pri_phy_enum_t24BK_BLE_GAP_PRI_PHY_CODEDE"></a> <a id="group__dm__gap__defines__v1_1gga22cc153ad39f0a4ed1ad8196af85b5f9aa707a2101f842c81acd62789487f29df"></a> enumerator BK\_BLE\_GAP\_PRI\_PHY\_CODED
    :   Primary Phy is LE CODED

<a id="_CPPv426bk_ble_gap_phy_pref_enum_t"></a>

<a id="_CPPv326bk_ble_gap_phy_pref_enum_t"></a> <a id="_CPPv226bk_ble_gap_phy_pref_enum_t"></a> <a id="group__dm__gap__defines__v1_1gadd3adf6677b9c5226ba1c27d9b5e3d49"></a> enum bk\_ble\_gap\_phy\_pref\_enum\_t
:   *Values:*

    <a id="_CPPv4N26bk_ble_gap_phy_pref_enum_t27BK_BLE_GAP_PHY_1M_PREF_MASKE"></a>

    <a id="_CPPv3N26bk_ble_gap_phy_pref_enum_t27BK_BLE_GAP_PHY_1M_PREF_MASKE"></a> <a id="_CPPv2N26bk_ble_gap_phy_pref_enum_t27BK_BLE_GAP_PHY_1M_PREF_MASKE"></a> <a id="group__dm__gap__defines__v1_1ggadd3adf6677b9c5226ba1c27d9b5e3d49a3436d719dd8b0d76666c50baa2e283d6"></a> enumerator BK\_BLE\_GAP\_PHY\_1M\_PREF\_MASK
    :   The Host prefers use the LE1M transmitter or reciever PHY

    <a id="_CPPv4N26bk_ble_gap_phy_pref_enum_t27BK_BLE_GAP_PHY_2M_PREF_MASKE"></a>

    <a id="_CPPv3N26bk_ble_gap_phy_pref_enum_t27BK_BLE_GAP_PHY_2M_PREF_MASKE"></a> <a id="_CPPv2N26bk_ble_gap_phy_pref_enum_t27BK_BLE_GAP_PHY_2M_PREF_MASKE"></a> <a id="group__dm__gap__defines__v1_1ggadd3adf6677b9c5226ba1c27d9b5e3d49addf683676f501984dddbd8d84dad9091"></a> enumerator BK\_BLE\_GAP\_PHY\_2M\_PREF\_MASK
    :   The Host prefers use the LE2M transmitter or reciever PHY

    <a id="_CPPv4N26bk_ble_gap_phy_pref_enum_t30BK_BLE_GAP_PHY_CODED_PREF_MASKE"></a>

    <a id="_CPPv3N26bk_ble_gap_phy_pref_enum_t30BK_BLE_GAP_PHY_CODED_PREF_MASKE"></a> <a id="_CPPv2N26bk_ble_gap_phy_pref_enum_t30BK_BLE_GAP_PHY_CODED_PREF_MASKE"></a> <a id="group__dm__gap__defines__v1_1ggadd3adf6677b9c5226ba1c27d9b5e3d49a7ccecb389346a8f41dc664d532f8c9aa"></a> enumerator BK\_BLE\_GAP\_PHY\_CODED\_PREF\_MASK
    :   The Host prefers use the LE CODED transmitter or reciever PHY

<a id="_CPPv432bk_ble_gap_coded_phy_pref_enum_t"></a>

<a id="_CPPv332bk_ble_gap_coded_phy_pref_enum_t"></a> <a id="_CPPv232bk_ble_gap_coded_phy_pref_enum_t"></a> <a id="group__dm__gap__defines__v1_1gad6aefd283e1c86d8a496a7be035298ec"></a> enum bk\_ble\_gap\_coded\_phy\_pref\_enum\_t
:   ble gap coded phy pref param

    *Values:*

    <a id="_CPPv4N32bk_ble_gap_coded_phy_pref_enum_t30BK_BLE_GAP_PHY_OPTIONS_NO_PREFE"></a>

    <a id="_CPPv3N32bk_ble_gap_coded_phy_pref_enum_t30BK_BLE_GAP_PHY_OPTIONS_NO_PREFE"></a> <a id="_CPPv2N32bk_ble_gap_coded_phy_pref_enum_t30BK_BLE_GAP_PHY_OPTIONS_NO_PREFE"></a> <a id="group__dm__gap__defines__v1_1ggad6aefd283e1c86d8a496a7be035298ecab89a815de1447d3a786f6cbcc069dec1"></a> enumerator BK\_BLE\_GAP\_PHY\_OPTIONS\_NO\_PREF
    :   The Host has no preferred coding when transmitting on the LE Coded PHY

    <a id="_CPPv4N32bk_ble_gap_coded_phy_pref_enum_t37BK_BLE_GAP_PHY_OPTIONS_PREF_S2_CODINGE"></a>

    <a id="_CPPv3N32bk_ble_gap_coded_phy_pref_enum_t37BK_BLE_GAP_PHY_OPTIONS_PREF_S2_CODINGE"></a> <a id="_CPPv2N32bk_ble_gap_coded_phy_pref_enum_t37BK_BLE_GAP_PHY_OPTIONS_PREF_S2_CODINGE"></a> <a id="group__dm__gap__defines__v1_1ggad6aefd283e1c86d8a496a7be035298ecabe99d63cbd8f391e49e21b3824986e72"></a> enumerator BK\_BLE\_GAP\_PHY\_OPTIONS\_PREF\_S2\_CODING
    :   The Host prefers that S\=2 coding be used when transmitting on the LE Coded PHY

    <a id="_CPPv4N32bk_ble_gap_coded_phy_pref_enum_t37BK_BLE_GAP_PHY_OPTIONS_PREF_S8_CODINGE"></a>

    <a id="_CPPv3N32bk_ble_gap_coded_phy_pref_enum_t37BK_BLE_GAP_PHY_OPTIONS_PREF_S8_CODINGE"></a> <a id="_CPPv2N32bk_ble_gap_coded_phy_pref_enum_t37BK_BLE_GAP_PHY_OPTIONS_PREF_S8_CODINGE"></a> <a id="group__dm__gap__defines__v1_1ggad6aefd283e1c86d8a496a7be035298eca39e16dc42378b76e12a68d8a0b49f68e"></a> enumerator BK\_BLE\_GAP\_PHY\_OPTIONS\_PREF\_S8\_CODING
    :   The Host prefers that S\=8 coding be used when transmitting on the LE Coded PHY

<a id="_CPPv430bk_ble_gap_ext_scan_cfg_enum_t"></a>

<a id="_CPPv330bk_ble_gap_ext_scan_cfg_enum_t"></a> <a id="_CPPv230bk_ble_gap_ext_scan_cfg_enum_t"></a> <a id="group__dm__gap__defines__v1_1ga29c2ac84ccb6d00a85777a27d3437b49"></a> enum bk\_ble\_gap\_ext\_scan\_cfg\_enum\_t
:   ble gap ext scan cfg

    *Values:*

    <a id="_CPPv4N30bk_ble_gap_ext_scan_cfg_enum_t35BK_BLE_GAP_EXT_SCAN_CFG_UNCODE_MASKE"></a>

    <a id="_CPPv3N30bk_ble_gap_ext_scan_cfg_enum_t35BK_BLE_GAP_EXT_SCAN_CFG_UNCODE_MASKE"></a> <a id="_CPPv2N30bk_ble_gap_ext_scan_cfg_enum_t35BK_BLE_GAP_EXT_SCAN_CFG_UNCODE_MASKE"></a> <a id="group__dm__gap__defines__v1_1gga29c2ac84ccb6d00a85777a27d3437b49ad2b168fda06039728134a92e8a9b5735"></a> enumerator BK\_BLE\_GAP\_EXT\_SCAN\_CFG\_UNCODE\_MASK
    :   Scan Advertisements on the LE1M PHY

    <a id="_CPPv4N30bk_ble_gap_ext_scan_cfg_enum_t33BK_BLE_GAP_EXT_SCAN_CFG_CODE_MASKE"></a>

    <a id="_CPPv3N30bk_ble_gap_ext_scan_cfg_enum_t33BK_BLE_GAP_EXT_SCAN_CFG_CODE_MASKE"></a> <a id="_CPPv2N30bk_ble_gap_ext_scan_cfg_enum_t33BK_BLE_GAP_EXT_SCAN_CFG_CODE_MASKE"></a> <a id="group__dm__gap__defines__v1_1gga29c2ac84ccb6d00a85777a27d3437b49a7898e3b8f6fb1e860c78ea02aa434c44"></a> enumerator BK\_BLE\_GAP\_EXT\_SCAN\_CFG\_CODE\_MASK
    :   Scan advertisements on the LE coded PHY

<a id="_CPPv434bk_ble_gap_ext_adv_data_seg_enum_t"></a>

<a id="_CPPv334bk_ble_gap_ext_adv_data_seg_enum_t"></a> <a id="_CPPv234bk_ble_gap_ext_adv_data_seg_enum_t"></a> <a id="group__dm__gap__defines__v1_1ga4326f1f23a7e6b41df3a2dded0fd511a"></a> enum bk\_ble\_gap\_ext\_adv\_data\_seg\_enum\_t
:   Advertising data seg.

    *Values:*

    <a id="_CPPv4N34bk_ble_gap_ext_adv_data_seg_enum_t32BK_BLE_GAP_EXT_ADV_DATA_COMPLETEE"></a>

    <a id="_CPPv3N34bk_ble_gap_ext_adv_data_seg_enum_t32BK_BLE_GAP_EXT_ADV_DATA_COMPLETEE"></a> <a id="_CPPv2N34bk_ble_gap_ext_adv_data_seg_enum_t32BK_BLE_GAP_EXT_ADV_DATA_COMPLETEE"></a> <a id="group__dm__gap__defines__v1_1gga4326f1f23a7e6b41df3a2dded0fd511aa5778d76dbd5fb807a5c2816eb3e2307a"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_DATA\_COMPLETE
    :   extended advertising data compete

    <a id="_CPPv4N34bk_ble_gap_ext_adv_data_seg_enum_t34BK_BLE_GAP_EXT_ADV_DATA_INCOMPLETEE"></a>

    <a id="_CPPv3N34bk_ble_gap_ext_adv_data_seg_enum_t34BK_BLE_GAP_EXT_ADV_DATA_INCOMPLETEE"></a> <a id="_CPPv2N34bk_ble_gap_ext_adv_data_seg_enum_t34BK_BLE_GAP_EXT_ADV_DATA_INCOMPLETEE"></a> <a id="group__dm__gap__defines__v1_1gga4326f1f23a7e6b41df3a2dded0fd511aadd77c4c6311c33e55185d1a7262b688f"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_DATA\_INCOMPLETE
    :   extended advertising data incomplete

    <a id="_CPPv4N34bk_ble_gap_ext_adv_data_seg_enum_t33BK_BLE_GAP_EXT_ADV_DATA_TRUNCATEDE"></a>

    <a id="_CPPv3N34bk_ble_gap_ext_adv_data_seg_enum_t33BK_BLE_GAP_EXT_ADV_DATA_TRUNCATEDE"></a> <a id="_CPPv2N34bk_ble_gap_ext_adv_data_seg_enum_t33BK_BLE_GAP_EXT_ADV_DATA_TRUNCATEDE"></a> <a id="group__dm__gap__defines__v1_1gga4326f1f23a7e6b41df3a2dded0fd511aaad8bdd2b66be3f9fe8f1c8e3fef2f5fc"></a> enumerator BK\_BLE\_GAP\_EXT\_ADV\_DATA\_TRUNCATED
    :   extended advertising data truncated mode

<a id="_CPPv429bk_ble_gap_sync_policy_enum_t"></a>

<a id="_CPPv329bk_ble_gap_sync_policy_enum_t"></a> <a id="_CPPv229bk_ble_gap_sync_policy_enum_t"></a> <a id="group__dm__gap__defines__v1_1gac6af63939e969c495ba68d883dc9fbe4"></a> enum bk\_ble\_gap\_sync\_policy\_enum\_t
:   Advertising SYNC policy.

    *Values:*

    <a id="_CPPv4N29bk_ble_gap_sync_policy_enum_t34BK_BLE_GAP_SYNC_POLICY_BY_ADV_INFOE"></a>

    <a id="_CPPv3N29bk_ble_gap_sync_policy_enum_t34BK_BLE_GAP_SYNC_POLICY_BY_ADV_INFOE"></a> <a id="_CPPv2N29bk_ble_gap_sync_policy_enum_t34BK_BLE_GAP_SYNC_POLICY_BY_ADV_INFOE"></a> <a id="group__dm__gap__defines__v1_1ggac6af63939e969c495ba68d883dc9fbe4a377a15f6462b34f8c0d8a6a392504156"></a> enumerator BK\_BLE\_GAP\_SYNC\_POLICY\_BY\_ADV\_INFO
    :   sync policy by advertising info

    <a id="_CPPv4N29bk_ble_gap_sync_policy_enum_t39BK_BLE_GAP_SYNC_POLICY_BY_PERIODIC_LISTE"></a>

    <a id="_CPPv3N29bk_ble_gap_sync_policy_enum_t39BK_BLE_GAP_SYNC_POLICY_BY_PERIODIC_LISTE"></a> <a id="_CPPv2N29bk_ble_gap_sync_policy_enum_t39BK_BLE_GAP_SYNC_POLICY_BY_PERIODIC_LISTE"></a> <a id="group__dm__gap__defines__v1_1ggac6af63939e969c495ba68d883dc9fbe4addebc6a7f3308e43aef0c6b504216707"></a> enumerator BK\_BLE\_GAP\_SYNC\_POLICY\_BY\_PERIODIC\_LIST
    :   periodic advertising sync policy

<a id="_CPPv433bk_ble_adv_report_ext_type_enum_t"></a>

<a id="_CPPv333bk_ble_adv_report_ext_type_enum_t"></a> <a id="_CPPv233bk_ble_adv_report_ext_type_enum_t"></a> <a id="group__dm__gap__defines__v1_1ga98093619e3f89754e1e42a437a6ed074"></a> enum bk\_ble\_adv\_report\_ext\_type\_enum\_t
:   Advertising report.

    *Values:*

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t29BK_BLE_ADV_REPORT_EXT_ADV_INDE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t29BK_BLE_ADV_REPORT_EXT_ADV_INDE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t29BK_BLE_ADV_REPORT_EXT_ADV_INDE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074ad000592430cab48797b888f9dc0d2690"></a> enumerator BK\_BLE\_ADV\_REPORT\_EXT\_ADV\_IND
    :   advertising report with extended advertising indication type

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t30BK_BLE_ADV_REPORT_EXT_SCAN_INDE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t30BK_BLE_ADV_REPORT_EXT_SCAN_INDE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t30BK_BLE_ADV_REPORT_EXT_SCAN_INDE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074af122d35fc5ccc94aa2900a295b16b924"></a> enumerator BK\_BLE\_ADV\_REPORT\_EXT\_SCAN\_IND
    :   advertising report with extended scan indication type

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t32BK_BLE_ADV_REPORT_EXT_DIRECT_ADVE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t32BK_BLE_ADV_REPORT_EXT_DIRECT_ADVE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t32BK_BLE_ADV_REPORT_EXT_DIRECT_ADVE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074ab456b5485170b7e201bb8a12b109a841"></a> enumerator BK\_BLE\_ADV\_REPORT\_EXT\_DIRECT\_ADV
    :   advertising report with extended direct advertising indication type

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t30BK_BLE_ADV_REPORT_EXT_SCAN_RSPE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t30BK_BLE_ADV_REPORT_EXT_SCAN_RSPE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t30BK_BLE_ADV_REPORT_EXT_SCAN_RSPE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074ad35f534a7efec10142116e8fd046d28e"></a> enumerator BK\_BLE\_ADV\_REPORT\_EXT\_SCAN\_RSP
    :   advertising report with extended scan response indication type

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t26BK_BLE_LEGACY_ADV_TYPE_INDE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t26BK_BLE_LEGACY_ADV_TYPE_INDE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t26BK_BLE_LEGACY_ADV_TYPE_INDE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074a8f94607a27f0691eedb522910cd7c32e"></a> enumerator BK\_BLE\_LEGACY\_ADV\_TYPE\_IND
    :   advertising report with legacy advertising indication type

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t33BK_BLE_LEGACY_ADV_TYPE_DIRECT_INDE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t33BK_BLE_LEGACY_ADV_TYPE_DIRECT_INDE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t33BK_BLE_LEGACY_ADV_TYPE_DIRECT_INDE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074a21d194f6132bdbe4279b53191d461322"></a> enumerator BK\_BLE\_LEGACY\_ADV\_TYPE\_DIRECT\_IND
    :   advertising report with legacy direct indication type

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t31BK_BLE_LEGACY_ADV_TYPE_SCAN_INDE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t31BK_BLE_LEGACY_ADV_TYPE_SCAN_INDE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t31BK_BLE_LEGACY_ADV_TYPE_SCAN_INDE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074aa81d84d236f707f9d4cb28d0954c57f7"></a> enumerator BK\_BLE\_LEGACY\_ADV\_TYPE\_SCAN\_IND
    :   advertising report with legacy scan indication type

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t33BK_BLE_LEGACY_ADV_TYPE_NONCON_INDE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t33BK_BLE_LEGACY_ADV_TYPE_NONCON_INDE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t33BK_BLE_LEGACY_ADV_TYPE_NONCON_INDE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074acacbcee932b2a516a072405662447e53"></a> enumerator BK\_BLE\_LEGACY\_ADV\_TYPE\_NONCON\_IND
    :   advertising report with legacy non connectable indication type

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t42BK_BLE_LEGACY_ADV_TYPE_SCAN_RSP_TO_ADV_INDE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t42BK_BLE_LEGACY_ADV_TYPE_SCAN_RSP_TO_ADV_INDE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t42BK_BLE_LEGACY_ADV_TYPE_SCAN_RSP_TO_ADV_INDE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074a8c2fb6c3f497642ac0a7d242a9b847e4"></a> enumerator BK\_BLE\_LEGACY\_ADV\_TYPE\_SCAN\_RSP\_TO\_ADV\_IND
    :   advertising report with legacy scan response indication type

    <a id="_CPPv4N33bk_ble_adv_report_ext_type_enum_t47BK_BLE_LEGACY_ADV_TYPE_SCAN_RSP_TO_ADV_SCAN_INDE"></a>

    <a id="_CPPv3N33bk_ble_adv_report_ext_type_enum_t47BK_BLE_LEGACY_ADV_TYPE_SCAN_RSP_TO_ADV_SCAN_INDE"></a> <a id="_CPPv2N33bk_ble_adv_report_ext_type_enum_t47BK_BLE_LEGACY_ADV_TYPE_SCAN_RSP_TO_ADV_SCAN_INDE"></a> <a id="group__dm__gap__defines__v1_1gga98093619e3f89754e1e42a437a6ed074a09fcc97e5f2df722e7511b3ca57e6ed7"></a> enumerator BK\_BLE\_LEGACY\_ADV\_TYPE\_SCAN\_RSP\_TO\_ADV\_SCAN\_IND
    :   advertising report with legacy advertising with scan response indication type

<a id="bk-dm-gatt-types-h"></a>

## bk\_dm\_gatt\_types.h

`bk_dm_gatt_types.h` 定义 BLE GATT 公共数据结构、权限、属性和回调类型。

<a id="id19"></a>

### Header File

- [bk\_dm\_gatt\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_gatt_types.h)

<a id="id20"></a>

### Structures

<a id="_CPPv412bk_gatt_id_t"></a>

<a id="_CPPv312bk_gatt_id_t"></a> <a id="_CPPv212bk_gatt_id_t"></a> <a id="bk_gatt_id_t"></a> <a id="structbk__gatt__id__t"></a> struct bk\_gatt\_id\_t
:   Gatt id, include uuid and instance id.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12bk_gatt_id_t4uuidE"></a>

    <a id="_CPPv3N12bk_gatt_id_t4uuidE"></a> <a id="_CPPv2N12bk_gatt_id_t4uuidE"></a> <a id="bk_gatt_id_t::uuid__bk_bt_uuid_t"></a> <a id="structbk__gatt__id__t_1a68901cd859a8a88cece33714bb5636fa"></a> [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") uuid
    :   UUID

<a id="_CPPv417bk_gatt_srvc_id_t"></a>

<a id="_CPPv317bk_gatt_srvc_id_t"></a> <a id="_CPPv217bk_gatt_srvc_id_t"></a> <a id="bk_gatt_srvc_id_t"></a> <a id="structbk__gatt__srvc__id__t"></a> struct bk\_gatt\_srvc\_id\_t
:   Gatt service id, include id (uuid and instance id) and primary flag.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_gatt_srvc_id_t2idE"></a>

    <a id="_CPPv3N17bk_gatt_srvc_id_t2idE"></a> <a id="_CPPv2N17bk_gatt_srvc_id_t2idE"></a> <a id="bk_gatt_srvc_id_t::id__bk_gatt_id_t"></a> <a id="structbk__gatt__srvc__id__t_1a1e6d5ea95b5ca1c6f99f66fc0d1914d0"></a> [bk\_gatt\_id\_t](#_CPPv412bk_gatt_id_t "bk_gatt_id_t") id
    :   Gatt id, include uuid and instance

    <a id="_CPPv4N17bk_gatt_srvc_id_t10is_primaryE"></a>

    <a id="_CPPv3N17bk_gatt_srvc_id_t10is_primaryE"></a> <a id="_CPPv2N17bk_gatt_srvc_id_t10is_primaryE"></a> <a id="bk_gatt_srvc_id_t::is_primary__b"></a> <a id="structbk__gatt__srvc__id__t_1af98fcbf22f3fdd124a72483f80f6507c"></a> bool is\_primary
    :   This service is primary or not

<a id="_CPPv415bk_attr_value_t"></a>

<a id="_CPPv315bk_attr_value_t"></a> <a id="_CPPv215bk_attr_value_t"></a> <a id="bk_attr_value_t"></a> <a id="structbk__attr__value__t"></a> struct bk\_attr\_value\_t
:   set the attribute value type

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15bk_attr_value_t12attr_max_lenE"></a>

    <a id="_CPPv3N15bk_attr_value_t12attr_max_lenE"></a> <a id="_CPPv2N15bk_attr_value_t12attr_max_lenE"></a> <a id="bk_attr_value_t::attr_max_len__uint16_t"></a> <a id="structbk__attr__value__t_1ac021ae5303a30d77ce336d8452425d2c"></a> uint16\_t attr\_max\_len
    :   attribute max value length

    <a id="_CPPv4N15bk_attr_value_t8attr_lenE"></a>

    <a id="_CPPv3N15bk_attr_value_t8attr_lenE"></a> <a id="_CPPv2N15bk_attr_value_t8attr_lenE"></a> <a id="bk_attr_value_t::attr_len__uint16_t"></a> <a id="structbk__attr__value__t_1ab97c6b6d22a2394f432c990c94abbee1"></a> uint16\_t attr\_len
    :   attribute current value length

    <a id="_CPPv4N15bk_attr_value_t10attr_valueE"></a>

    <a id="_CPPv3N15bk_attr_value_t10attr_valueE"></a> <a id="_CPPv2N15bk_attr_value_t10attr_valueE"></a> <a id="bk_attr_value_t::attr_value__uint8_tP"></a> <a id="structbk__attr__value__t_1a57964ecda9dc668ac1f848c202436bb8"></a> uint8\_t \*attr\_value
    :   the pointer to attribute value

<a id="_CPPv414bk_attr_desc_t"></a>

<a id="_CPPv314bk_attr_desc_t"></a> <a id="_CPPv214bk_attr_desc_t"></a> <a id="bk_attr_desc_t"></a> <a id="structbk__attr__desc__t"></a> struct bk\_attr\_desc\_t
:   Attribute description (used to create database)

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14bk_attr_desc_t12attr_contentE"></a>

    <a id="_CPPv3N14bk_attr_desc_t12attr_contentE"></a> <a id="_CPPv2N14bk_attr_desc_t12attr_contentE"></a> <a id="bk_attr_desc_t::attr_content__bk_bt_uuid_t"></a> <a id="structbk__attr__desc__t_1a9d8ee97bf6e46a8ed29e3e7d5bed1470"></a> [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") attr\_content
    :   attr type

    <a id="_CPPv4N14bk_attr_desc_t5valueE"></a>

    <a id="_CPPv3N14bk_attr_desc_t5valueE"></a> <a id="_CPPv2N14bk_attr_desc_t5valueE"></a> <a id="bk_attr_desc_t::value__bk_attr_value_t"></a> <a id="structbk__attr__desc__t_1abfa2a0a08eabf82ba8abfdbec3d7818e"></a> [bk\_attr\_value\_t](#_CPPv415bk_attr_value_t "bk_attr_value_t") value
    :   attr content if attr\_type is service or char

    <a id="_CPPv4N14bk_attr_desc_t4propE"></a>

    <a id="_CPPv3N14bk_attr_desc_t4propE"></a> <a id="_CPPv2N14bk_attr_desc_t4propE"></a> <a id="bk_attr_desc_t::prop__bk_gatt_char_prop_t"></a> <a id="structbk__attr__desc__t_1a948b84d3f91b6980d0aea950cb58a040"></a> [bk\_gatt\_char\_prop\_t](#_CPPv419bk_gatt_char_prop_t "bk_gatt_char_prop_t") prop
    :   Element value if attr\_type is char or desc.

    <a id="_CPPv4N14bk_attr_desc_t4permE"></a>

    <a id="_CPPv3N14bk_attr_desc_t4permE"></a> <a id="_CPPv2N14bk_attr_desc_t4permE"></a> <a id="bk_attr_desc_t::perm__bk_gatt_perm_enum_t"></a> <a id="structbk__attr__desc__t_1a60b2063a73ced9eb1484f47d1d12b07e"></a> [bk\_gatt\_perm\_enum\_t](#_CPPv419bk_gatt_perm_enum_t "bk_gatt_perm_enum_t") perm
    :   char prop, only used if attr\_type is char

        Attribute permission

<a id="_CPPv417bk_attr_control_t"></a>

<a id="_CPPv317bk_attr_control_t"></a> <a id="_CPPv217bk_attr_control_t"></a> <a id="bk_attr_control_t"></a> <a id="structbk__attr__control__t"></a> struct bk\_attr\_control\_t
:   attribute auto response flag

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_attr_control_t8auto_rspE"></a>

    <a id="_CPPv3N17bk_attr_control_t8auto_rspE"></a> <a id="_CPPv2N17bk_attr_control_t8auto_rspE"></a> <a id="bk_attr_control_t::auto_rsp__uint8_t"></a> <a id="structbk__attr__control__t_1ab13183f7bd864db3cc848920cc044ae8"></a> uint8\_t auto\_rsp
    :   if auto\_rsp set to BK\_GATT\_RSP\_BY\_APP, means the response of Write/Read operation will by replied by application. if auto\_rsp set to BK\_GATT\_AUTO\_RSP, means the response of Write/Read operation will be replied by GATT stack automatically.

<a id="_CPPv418bk_gatts_attr_db_t"></a>

<a id="_CPPv318bk_gatts_attr_db_t"></a> <a id="_CPPv218bk_gatts_attr_db_t"></a> <a id="bk_gatts_attr_db_t"></a> <a id="structbk__gatts__attr__db__t"></a> struct bk\_gatts\_attr\_db\_t
:   attribute type added to the gatt server database

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_gatts_attr_db_t8att_descE"></a>

    <a id="_CPPv3N18bk_gatts_attr_db_t8att_descE"></a> <a id="_CPPv2N18bk_gatts_attr_db_t8att_descE"></a> <a id="bk_gatts_attr_db_t::att_desc__bk_attr_desc_t"></a> <a id="structbk__gatts__attr__db__t_1a6c3dc75b240965c6b9749a0d42d643c4"></a> [bk\_attr\_desc\_t](#_CPPv414bk_attr_desc_t "bk_attr_desc_t") att\_desc
    :   The attribute type

    <a id="_CPPv4N18bk_gatts_attr_db_t12attr_controlE"></a>

    <a id="_CPPv3N18bk_gatts_attr_db_t12attr_controlE"></a> <a id="_CPPv2N18bk_gatts_attr_db_t12attr_controlE"></a> <a id="bk_gatts_attr_db_t::attr_control__bk_attr_control_t"></a> <a id="structbk__gatts__attr__db__t_1acfdc9d4c773d482ef565b1ff328bff4f"></a> [bk\_attr\_control\_t](#_CPPv417bk_attr_control_t "bk_attr_control_t") attr\_control
    :   The attribute control type, not used if attr type is service

<a id="_CPPv415bk_gatt_value_t"></a>

<a id="_CPPv315bk_gatt_value_t"></a> <a id="_CPPv215bk_gatt_value_t"></a> <a id="bk_gatt_value_t"></a> <a id="structbk__gatt__value__t"></a> struct bk\_gatt\_value\_t
:   Gatt attribute value.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15bk_gatt_value_t5valueE"></a>

    <a id="_CPPv3N15bk_gatt_value_t5valueE"></a> <a id="_CPPv2N15bk_gatt_value_t5valueE"></a> <a id="bk_gatt_value_t::value__uint8_tP"></a> <a id="structbk__gatt__value__t_1ac993157d4cb4461627d226213e9eb676"></a> uint8\_t \*value
    :   Gatt attribute value

    <a id="_CPPv4N15bk_gatt_value_t6handleE"></a>

    <a id="_CPPv3N15bk_gatt_value_t6handleE"></a> <a id="_CPPv2N15bk_gatt_value_t6handleE"></a> <a id="bk_gatt_value_t::handle__uint16_t"></a> <a id="structbk__gatt__value__t_1ab5bc089e5b649b72e4573110d152ebb3"></a> uint16\_t handle
    :   Gatt attribute handle

    <a id="_CPPv4N15bk_gatt_value_t6offsetE"></a>

    <a id="_CPPv3N15bk_gatt_value_t6offsetE"></a> <a id="_CPPv2N15bk_gatt_value_t6offsetE"></a> <a id="bk_gatt_value_t::offset__uint16_t"></a> <a id="structbk__gatt__value__t_1a7f20ec591726c26628be5dc8ff7a3a80"></a> uint16\_t offset
    :   Gatt attribute value offset

    <a id="_CPPv4N15bk_gatt_value_t3lenE"></a>

    <a id="_CPPv3N15bk_gatt_value_t3lenE"></a> <a id="_CPPv2N15bk_gatt_value_t3lenE"></a> <a id="bk_gatt_value_t::len__uint16_t"></a> <a id="structbk__gatt__value__t_1a8a7b98b8cef94175437e79084b96a93e"></a> uint16\_t len
    :   Gatt attribute value length

    <a id="_CPPv4N15bk_gatt_value_t8auth_reqE"></a>

    <a id="_CPPv3N15bk_gatt_value_t8auth_reqE"></a> <a id="_CPPv2N15bk_gatt_value_t8auth_reqE"></a> <a id="bk_gatt_value_t::auth_req__bk_gatt_auth_req_t"></a> <a id="structbk__gatt__value__t_1a7baad55566339b32a66d6fa2c684f479"></a> [bk\_gatt\_auth\_req\_t](#_CPPv418bk_gatt_auth_req_t "bk_gatt_auth_req_t") auth\_req
    :   Gatt authentication request see bk\_gatt\_auth\_req\_t

<a id="_CPPv413bk_gatt_rsp_t"></a>

<a id="_CPPv313bk_gatt_rsp_t"></a> <a id="_CPPv213bk_gatt_rsp_t"></a> <a id="bk_gatt_rsp_t"></a> <a id="structbk__gatt__rsp__t"></a> struct bk\_gatt\_rsp\_t
:   GATT remote read request response type.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13bk_gatt_rsp_t10attr_valueE"></a>

    <a id="_CPPv3N13bk_gatt_rsp_t10attr_valueE"></a> <a id="_CPPv2N13bk_gatt_rsp_t10attr_valueE"></a> <a id="bk_gatt_rsp_t::attr_value__bk_gatt_value_t"></a> <a id="structbk__gatt__rsp__t_1a580ba7a002504063e10eaa06cae48c48"></a> [bk\_gatt\_value\_t](#_CPPv415bk_gatt_value_t "bk_gatt_value_t") attr\_value
    :   Gatt attribute structure

<a id="_CPPv421bk_gatt_conn_params_t"></a>

<a id="_CPPv321bk_gatt_conn_params_t"></a> <a id="_CPPv221bk_gatt_conn_params_t"></a> <a id="bk_gatt_conn_params_t"></a> <a id="structbk__gatt__conn__params__t"></a> struct bk\_gatt\_conn\_params\_t
:   Connection parameters information.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21bk_gatt_conn_params_t8intervalE"></a>

    <a id="_CPPv3N21bk_gatt_conn_params_t8intervalE"></a> <a id="_CPPv2N21bk_gatt_conn_params_t8intervalE"></a> <a id="bk_gatt_conn_params_t::interval__uint16_t"></a> <a id="structbk__gatt__conn__params__t_1a082b17a34e2066bceee5ec3fbd273cc8"></a> uint16\_t interval
    :   connection interval

    <a id="_CPPv4N21bk_gatt_conn_params_t7latencyE"></a>

    <a id="_CPPv3N21bk_gatt_conn_params_t7latencyE"></a> <a id="_CPPv2N21bk_gatt_conn_params_t7latencyE"></a> <a id="bk_gatt_conn_params_t::latency__uint16_t"></a> <a id="structbk__gatt__conn__params__t_1a0ed12e67a569d2a4afe12274b03c561c"></a> uint16\_t latency
    :   Slave latency for the connection in number of connection events. Range: 0x0000 to 0x01F3

    <a id="_CPPv4N21bk_gatt_conn_params_t7timeoutE"></a>

    <a id="_CPPv3N21bk_gatt_conn_params_t7timeoutE"></a> <a id="_CPPv2N21bk_gatt_conn_params_t7timeoutE"></a> <a id="bk_gatt_conn_params_t::timeout__uint16_t"></a> <a id="structbk__gatt__conn__params__t_1ab211bda5acb0295212d0060d91fde82b"></a> uint16\_t timeout
    :   Supervision timeout for the LE Link. Range: 0x000A to 0x0C80. Mandatory Range: 0x000A to 0x0C80 Time \= N \* 10 msec Time Range: 100 msec to 32 seconds

<a id="_CPPv416bk_gattc_multi_t"></a>

<a id="_CPPv316bk_gattc_multi_t"></a> <a id="_CPPv216bk_gattc_multi_t"></a> <a id="bk_gattc_multi_t"></a> <a id="structbk__gattc__multi__t"></a> struct bk\_gattc\_multi\_t
:   read multiple attribute

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16bk_gattc_multi_t8num_attrE"></a>

    <a id="_CPPv3N16bk_gattc_multi_t8num_attrE"></a> <a id="_CPPv2N16bk_gattc_multi_t8num_attrE"></a> <a id="bk_gattc_multi_t::num_attr__uint8_t"></a> <a id="structbk__gattc__multi__t_1a1454c6dbb103e5f5221c3b21c648725f"></a> uint8\_t num\_attr
    :   The number of the attribute

    <a id="_CPPv4N16bk_gattc_multi_t7handlesE"></a>

    <a id="_CPPv3N16bk_gattc_multi_t7handlesE"></a> <a id="_CPPv2N16bk_gattc_multi_t7handlesE"></a> <a id="bk_gattc_multi_t::handles__uint16_tA"></a> <a id="structbk__gattc__multi__t_1a6dbafb6e6d528c9143a14c6210f440e1"></a> uint16\_t handles\[BK\_GATT\_MAX\_READ\_MULTI\_HANDLES\]
    :   The handles list

<a id="id21"></a>

### Macros

<a id="c.BK_GATT_MAX_READ_MULTI_HANDLES"></a>

<a id="group__dm__gatt__types__v1_1ga7c5963c0ab61811db2e8b07e647b3eda"></a> BK\_GATT\_MAX\_READ\_MULTI\_HANDLES

<a id="c.BK_GATT_RSP_BY_APP"></a>

<a id="bk__dm__gatt__types_8h_1a61f63bfdd1f97fdbab654f965e397824"></a> BK\_GATT\_RSP\_BY\_APP

<a id="c.BK_GATT_AUTO_RSP"></a>

<a id="bk__dm__gatt__types_8h_1a4d98dd8b85dc675abfa8d139b0cccdde"></a> BK\_GATT\_AUTO\_RSP

<a id="id22"></a>

### Type Definitions

<a id="_CPPv414bk_gatt_perm_t"></a>

<a id="_CPPv314bk_gatt_perm_t"></a> <a id="_CPPv214bk_gatt_perm_t"></a> <a id="bk_gatt_perm_t"></a> <a id="group__dm__gatt__types__v1_1gae2e95e1f6113bf6f05c4160d035a49bc"></a> typedef uint16\_t bk\_gatt\_perm\_t
:   see bk\_gatt\_perm\_enum\_t

<a id="_CPPv419bk_gatt_char_prop_t"></a>

<a id="_CPPv319bk_gatt_char_prop_t"></a> <a id="_CPPv219bk_gatt_char_prop_t"></a> <a id="bk_gatt_char_prop_t"></a> <a id="group__dm__gatt__types__v1_1ga1dff634c35ed71e92c08482fed07df23"></a> typedef uint8\_t bk\_gatt\_char\_prop\_t
:   see bk\_gatt\_char\_prop\_enum\_t

<a id="_CPPv412bk_gatt_if_t"></a>

<a id="_CPPv312bk_gatt_if_t"></a> <a id="_CPPv212bk_gatt_if_t"></a> <a id="bk_gatt_if_t"></a> <a id="group__dm__gatt__types__v1_1gacc09c1af3a9d05c67fd7a1e5f6676eb7"></a> typedef uint8\_t bk\_gatt\_if\_t
:   Gatt interface type, different application on GATT client use different gatt\_if

<a id="id23"></a>

### Enumerations

<a id="_CPPv419bk_gatt_uuid_enum_t"></a>

<a id="_CPPv319bk_gatt_uuid_enum_t"></a> <a id="_CPPv219bk_gatt_uuid_enum_t"></a> <a id="group__dm__gatt__types__v1_1ga96957f08912423621a21377bae694ca9"></a> enum bk\_gatt\_uuid\_enum\_t
:   gatt uuid type, All “BK\_GATT\_UUID\_xxx” is attribute types

    *Values:*

    <a id="_CPPv4N19bk_gatt_uuid_enum_t20BK_GATT_UUID_GAP_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t20BK_GATT_UUID_GAP_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t20BK_GATT_UUID_GAP_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a60d4228542268ec29c386111df23eb8a"></a> enumerator BK\_GATT\_UUID\_GAP\_SVC

    <a id="_CPPv4N19bk_gatt_uuid_enum_t21BK_GATT_UUID_GATT_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t21BK_GATT_UUID_GATT_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t21BK_GATT_UUID_GATT_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a148c90af6a84173613b2d6705cacc712"></a> enumerator BK\_GATT\_UUID\_GATT\_SVC
    :   Generic Access Profile service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_IMMEDIATE_ALERT_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_IMMEDIATE_ALERT_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_IMMEDIATE_ALERT_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a5758736f10bd1a38df935c9b71d44e95"></a> enumerator BK\_GATT\_UUID\_IMMEDIATE\_ALERT\_SVC
    :   Generic Attribute Profile service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t26BK_GATT_UUID_LINK_LOSS_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t26BK_GATT_UUID_LINK_LOSS_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t26BK_GATT_UUID_LINK_LOSS_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a038c6ae722a2e14758b0b4bbaf5dcad8"></a> enumerator BK\_GATT\_UUID\_LINK\_LOSS\_SVC
    :   Immediate alert service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t25BK_GATT_UUID_TX_POWER_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t25BK_GATT_UUID_TX_POWER_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t25BK_GATT_UUID_TX_POWER_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a8ba6e4a8a1cd62eb9a23ec76ca76dcfe"></a> enumerator BK\_GATT\_UUID\_TX\_POWER\_SVC
    :   Link Loss service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_CURRENT_TIME_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_CURRENT_TIME_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_CURRENT_TIME_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a9ad2c07a4dfc6d09e815b6af5b7c8c74"></a> enumerator BK\_GATT\_UUID\_CURRENT\_TIME\_SVC
    :   TX Power service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_REF_TIME_UPDATE_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_REF_TIME_UPDATE_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_REF_TIME_UPDATE_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a2c777ae26e8536db3a9b7368775a6dbb"></a> enumerator BK\_GATT\_UUID\_REF\_TIME\_UPDATE\_SVC
    :   Current Time Service service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_NEXT_DST_CHANGE_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_NEXT_DST_CHANGE_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_NEXT_DST_CHANGE_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9adb57d96f44c97b5f0f4296accf696442"></a> enumerator BK\_GATT\_UUID\_NEXT\_DST\_CHANGE\_SVC
    :   Reference Time Update service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t24BK_GATT_UUID_GLUCOSE_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t24BK_GATT_UUID_GLUCOSE_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t24BK_GATT_UUID_GLUCOSE_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a4b3a20b250b7666a1a8d1bb98512a051"></a> enumerator BK\_GATT\_UUID\_GLUCOSE\_SVC
    :   Next DST Change service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t31BK_GATT_UUID_HEALTH_THERMOM_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t31BK_GATT_UUID_HEALTH_THERMOM_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t31BK_GATT_UUID_HEALTH_THERMOM_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a25ea11edefa14b5521674904a1ff310f"></a> enumerator BK\_GATT\_UUID\_HEALTH\_THERMOM\_SVC
    :   Glucose service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_DEVICE_INFO_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_DEVICE_INFO_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_DEVICE_INFO_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a83d99757c4b774ce7339f9d6b90ab8eb"></a> enumerator BK\_GATT\_UUID\_DEVICE\_INFO\_SVC
    :   Health Thermometer service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HEART_RATE_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HEART_RATE_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HEART_RATE_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a3b32017efaf8f0be9d49dd52c1f613e9"></a> enumerator BK\_GATT\_UUID\_HEART\_RATE\_SVC
    :   Device Information service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t35BK_GATT_UUID_PHONE_ALERT_STATUS_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t35BK_GATT_UUID_PHONE_ALERT_STATUS_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t35BK_GATT_UUID_PHONE_ALERT_STATUS_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ab58f99cc53fec03af6e148b191a8fa52"></a> enumerator BK\_GATT\_UUID\_PHONE\_ALERT\_STATUS\_SVC
    :   Heart Rate service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_BATTERY_SERVICE_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_BATTERY_SERVICE_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_BATTERY_SERVICE_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ace441233288ef9c27ba809931df3490d"></a> enumerator BK\_GATT\_UUID\_BATTERY\_SERVICE\_SVC
    :   Phone Alert Status service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t31BK_GATT_UUID_BLOOD_PRESSURE_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t31BK_GATT_UUID_BLOOD_PRESSURE_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t31BK_GATT_UUID_BLOOD_PRESSURE_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a037cd9e0f8f2de3f513785caa05dc457"></a> enumerator BK\_GATT\_UUID\_BLOOD\_PRESSURE\_SVC
    :   Battery service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t26BK_GATT_UUID_ALERT_NTF_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t26BK_GATT_UUID_ALERT_NTF_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t26BK_GATT_UUID_ALERT_NTF_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a655830aa2233928919610d06deceef9a"></a> enumerator BK\_GATT\_UUID\_ALERT\_NTF\_SVC
    :   Blood Pressure service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t20BK_GATT_UUID_HID_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t20BK_GATT_UUID_HID_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t20BK_GATT_UUID_HID_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ad63a883e84e50919941a21489c2887e2"></a> enumerator BK\_GATT\_UUID\_HID\_SVC
    :   Alert Notification service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_SCAN_PARAMETERS_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_SCAN_PARAMETERS_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_SCAN_PARAMETERS_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9add6545c56f3caa0972a3b7d4dc36a697"></a> enumerator BK\_GATT\_UUID\_SCAN\_PARAMETERS\_SVC
    :   HID service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t38BK_GATT_UUID_RUNNING_SPEED_CADENCE_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t38BK_GATT_UUID_RUNNING_SPEED_CADENCE_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t38BK_GATT_UUID_RUNNING_SPEED_CADENCE_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a13c6634721841878dafa289108e4dfdc"></a> enumerator BK\_GATT\_UUID\_RUNNING\_SPEED\_CADENCE\_SVC
    :   Scan Parameters service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t30BK_GATT_UUID_AUTOMATION_IO_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t30BK_GATT_UUID_AUTOMATION_IO_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t30BK_GATT_UUID_AUTOMATION_IO_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ab0a35d174b48aaad285743679d9b8abb"></a> enumerator BK\_GATT\_UUID\_AUTOMATION\_IO\_SVC
    :   Running Speed and Cadence service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t38BK_GATT_UUID_CYCLING_SPEED_CADENCE_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t38BK_GATT_UUID_CYCLING_SPEED_CADENCE_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t38BK_GATT_UUID_CYCLING_SPEED_CADENCE_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a25bc574ad2adbfa2db929706d78ee30f"></a> enumerator BK\_GATT\_UUID\_CYCLING\_SPEED\_CADENCE\_SVC
    :   Automation IO service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t30BK_GATT_UUID_CYCLING_POWER_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t30BK_GATT_UUID_CYCLING_POWER_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t30BK_GATT_UUID_CYCLING_POWER_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a83eadda4df197b75c5f9e3ea9d860ead"></a> enumerator BK\_GATT\_UUID\_CYCLING\_POWER\_SVC
    :   Cycling Speed and Cadence service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t40BK_GATT_UUID_LOCATION_AND_NAVIGATION_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t40BK_GATT_UUID_LOCATION_AND_NAVIGATION_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t40BK_GATT_UUID_LOCATION_AND_NAVIGATION_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a7745de7f29d4967dd2f9e277ef54b88d"></a> enumerator BK\_GATT\_UUID\_LOCATION\_AND\_NAVIGATION\_SVC
    :   Cycling Power service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t38BK_GATT_UUID_ENVIRONMENTAL_SENSING_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t38BK_GATT_UUID_ENVIRONMENTAL_SENSING_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t38BK_GATT_UUID_ENVIRONMENTAL_SENSING_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9af2745ab886223b3fcd8e5c867186664b"></a> enumerator BK\_GATT\_UUID\_ENVIRONMENTAL\_SENSING\_SVC
    :   Location and Navigation service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_BODY_COMPOSITIONE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_BODY_COMPOSITIONE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_BODY_COMPOSITIONE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a2a15400c5cc19b5b1e43edb85f545bfe"></a> enumerator BK\_GATT\_UUID\_BODY\_COMPOSITION
    :   Environmental Sensing service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t26BK_GATT_UUID_USER_DATA_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t26BK_GATT_UUID_USER_DATA_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t26BK_GATT_UUID_USER_DATA_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9acf1d8d7c1e6cba2dea6e8e216cad1789"></a> enumerator BK\_GATT\_UUID\_USER\_DATA\_SVC
    :   Body Composition service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_WEIGHT_SCALE_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_WEIGHT_SCALE_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_WEIGHT_SCALE_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aa6de9e0663e5cb182e40f372c2479d9b"></a> enumerator BK\_GATT\_UUID\_WEIGHT\_SCALE\_SVC
    :   User Data service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_BOND_MANAGEMENT_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_BOND_MANAGEMENT_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_BOND_MANAGEMENT_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aa4add7b4ef594b3050f9a51c667109d6"></a> enumerator BK\_GATT\_UUID\_BOND\_MANAGEMENT\_SVC
    :   Weight Scale service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t37BK_GATT_UUID_CONT_GLUCOSE_MONITOR_SVCE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t37BK_GATT_UUID_CONT_GLUCOSE_MONITOR_SVCE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t37BK_GATT_UUID_CONT_GLUCOSE_MONITOR_SVCE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ae1bb0f43cd50c59d0684786a4d4d5910"></a> enumerator BK\_GATT\_UUID\_CONT\_GLUCOSE\_MONITOR\_SVC
    :   Bond Management service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t24BK_GATT_UUID_PRI_SERVICEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t24BK_GATT_UUID_PRI_SERVICEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t24BK_GATT_UUID_PRI_SERVICEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9afee3c3063c3b5fb22ca2705a80cfc67f"></a> enumerator BK\_GATT\_UUID\_PRI\_SERVICE
    :   Continuous Glucose Monitoring service.

        Declarations

    <a id="_CPPv4N19bk_gatt_uuid_enum_t24BK_GATT_UUID_SEC_SERVICEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t24BK_GATT_UUID_SEC_SERVICEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t24BK_GATT_UUID_SEC_SERVICEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ad82c6c2cf421182d79d86f0300facf15"></a> enumerator BK\_GATT\_UUID\_SEC\_SERVICE

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_INCLUDE_SERVICEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_INCLUDE_SERVICEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_INCLUDE_SERVICEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a6ec0f3f27baaa37373e387d1cdfc70b1"></a> enumerator BK\_GATT\_UUID\_INCLUDE\_SERVICE

    <a id="_CPPv4N19bk_gatt_uuid_enum_t25BK_GATT_UUID_CHAR_DECLAREE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t25BK_GATT_UUID_CHAR_DECLAREE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t25BK_GATT_UUID_CHAR_DECLAREE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a4df00ae14863d6020e422cddd83e4ead"></a> enumerator BK\_GATT\_UUID\_CHAR\_DECLARE

    <a id="_CPPv4N19bk_gatt_uuid_enum_t26BK_GATT_UUID_CHAR_EXT_PROPE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t26BK_GATT_UUID_CHAR_EXT_PROPE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t26BK_GATT_UUID_CHAR_EXT_PROPE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a4c27f2fb2cbde6f2055e15d58ed075dc"></a> enumerator BK\_GATT\_UUID\_CHAR\_EXT\_PROP
    :   Characteristic Declaration.

        Descriptors

    <a id="_CPPv4N19bk_gatt_uuid_enum_t34BK_GATT_UUID_CHAR_USER_DESCRIPTIONE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t34BK_GATT_UUID_CHAR_USER_DESCRIPTIONE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t34BK_GATT_UUID_CHAR_USER_DESCRIPTIONE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a2cd770b7d680294c70c115b4779d594e"></a> enumerator BK\_GATT\_UUID\_CHAR\_USER\_DESCRIPTION
    :   Characteristic Extended Properties.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t31BK_GATT_UUID_CHAR_CLIENT_CONFIGE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t31BK_GATT_UUID_CHAR_CLIENT_CONFIGE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t31BK_GATT_UUID_CHAR_CLIENT_CONFIGE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9acda65851322410ad87eda2a64ba0bf58"></a> enumerator BK\_GATT\_UUID\_CHAR\_CLIENT\_CONFIG
    :   Characteristic User Description.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_CHAR_SRVR_CONFIGE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_CHAR_SRVR_CONFIGE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_CHAR_SRVR_CONFIGE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ac661d87713a1a117f3a5ed0688e925a6"></a> enumerator BK\_GATT\_UUID\_CHAR\_SRVR\_CONFIG
    :   Client Characteristic Configuration.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_CHAR_PRESENT_FORMATE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_CHAR_PRESENT_FORMATE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_CHAR_PRESENT_FORMATE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a99bf46238eed55eb29bc97910511de98"></a> enumerator BK\_GATT\_UUID\_CHAR\_PRESENT\_FORMAT
    :   Server Characteristic Configuration.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_CHAR_AGG_FORMATE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_CHAR_AGG_FORMATE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_CHAR_AGG_FORMATE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a95845571f3eb1abc34a47919742ff590"></a> enumerator BK\_GATT\_UUID\_CHAR\_AGG\_FORMAT
    :   Characteristic Presentation Format.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_CHAR_VALID_RANGEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_CHAR_VALID_RANGEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_CHAR_VALID_RANGEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aa37c86d8a5018911b5b3d225725b06ed"></a> enumerator BK\_GATT\_UUID\_CHAR\_VALID\_RANGE
    :   Characteristic Aggregate Format.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t30BK_GATT_UUID_EXT_RPT_REF_DESCRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t30BK_GATT_UUID_EXT_RPT_REF_DESCRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t30BK_GATT_UUID_EXT_RPT_REF_DESCRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9afd8afa59197c46857a651c3e2b5a33f4"></a> enumerator BK\_GATT\_UUID\_EXT\_RPT\_REF\_DESCR
    :   Characteristic Valid Range.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t26BK_GATT_UUID_RPT_REF_DESCRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t26BK_GATT_UUID_RPT_REF_DESCRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t26BK_GATT_UUID_RPT_REF_DESCRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aeaff16fc82c75677c9a2d5498937fa8d"></a> enumerator BK\_GATT\_UUID\_RPT\_REF\_DESCR
    :   External Report Reference.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t31BK_GATT_UUID_NUM_DIGITALS_DESCRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t31BK_GATT_UUID_NUM_DIGITALS_DESCRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t31BK_GATT_UUID_NUM_DIGITALS_DESCRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aa1af1067a5f957ab10e747380482b7ae"></a> enumerator BK\_GATT\_UUID\_NUM\_DIGITALS\_DESCR
    :   Report Reference.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_VALUE_TRIGGER_DESCRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_VALUE_TRIGGER_DESCRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_VALUE_TRIGGER_DESCRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a6464a2235556f644e5b1894da5b76450"></a> enumerator BK\_GATT\_UUID\_VALUE\_TRIGGER\_DESCR
    :   Number of Digitals.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t37BK_GATT_UUID_ENV_SENSING_CONFIG_DESCRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t37BK_GATT_UUID_ENV_SENSING_CONFIG_DESCRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t37BK_GATT_UUID_ENV_SENSING_CONFIG_DESCRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9adbe0bbbab5ea4e0b9ef790061fc03f1f"></a> enumerator BK\_GATT\_UUID\_ENV\_SENSING\_CONFIG\_DESCR
    :   Value Trigger Setting.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t42BK_GATT_UUID_ENV_SENSING_MEASUREMENT_DESCRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t42BK_GATT_UUID_ENV_SENSING_MEASUREMENT_DESCRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t42BK_GATT_UUID_ENV_SENSING_MEASUREMENT_DESCRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aaedbaa0e8f390a11d9d899acb007b867"></a> enumerator BK\_GATT\_UUID\_ENV\_SENSING\_MEASUREMENT\_DESCR
    :   Environmental Sensing Configuration.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t38BK_GATT_UUID_ENV_SENSING_TRIGGER_DESCRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t38BK_GATT_UUID_ENV_SENSING_TRIGGER_DESCRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t38BK_GATT_UUID_ENV_SENSING_TRIGGER_DESCRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a9ee775fe5c605334f552903c6aa9a45a"></a> enumerator BK\_GATT\_UUID\_ENV\_SENSING\_TRIGGER\_DESCR
    :   Environmental Sensing Measurement.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t31BK_GATT_UUID_TIME_TRIGGER_DESCRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t31BK_GATT_UUID_TIME_TRIGGER_DESCRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t31BK_GATT_UUID_TIME_TRIGGER_DESCRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aa36819235adf2448649ac7d70ed75007"></a> enumerator BK\_GATT\_UUID\_TIME\_TRIGGER\_DESCR
    :   Environmental Sensing Trigger Setting.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t36BK_GATT_UUID_BR_EDR_TRANS_BLOCK_DATAE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t36BK_GATT_UUID_BR_EDR_TRANS_BLOCK_DATAE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t36BK_GATT_UUID_BR_EDR_TRANS_BLOCK_DATAE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a8f813fa6943bc5d0d5dfde0129811827"></a> enumerator BK\_GATT\_UUID\_BR\_EDR\_TRANS\_BLOCK\_DATA
    :   Time Trigger Setting.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t33BK_GATT_UUID_OBSERVATION_SCHEDULEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t33BK_GATT_UUID_OBSERVATION_SCHEDULEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t33BK_GATT_UUID_OBSERVATION_SCHEDULEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a5d4b22f46b02c60d1869aa2b96dd4c69"></a> enumerator BK\_GATT\_UUID\_OBSERVATION\_SCHEDULE
    :   Complete BRT-EDR Transport BLock Data.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t33BK_GATT_UUID_VALID_RANGE_ACCURACYE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t33BK_GATT_UUID_VALID_RANGE_ACCURACYE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t33BK_GATT_UUID_VALID_RANGE_ACCURACYE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a66bd0f6a5e2406fbafc95f31765ca5e6"></a> enumerator BK\_GATT\_UUID\_VALID\_RANGE\_ACCURACY
    :   Observation Schedule.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t36BK_GATT_UUID_MEASUREMENT_DESCRIPTIONE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t36BK_GATT_UUID_MEASUREMENT_DESCRIPTIONE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t36BK_GATT_UUID_MEASUREMENT_DESCRIPTIONE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a64a18b002b6d268967adcfcfda0485a0"></a> enumerator BK\_GATT\_UUID\_MEASUREMENT\_DESCRIPTION
    :   Valid Range and Accuracy.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_MANUFACTURER_LIMITSE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_MANUFACTURER_LIMITSE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_MANUFACTURER_LIMITSE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a85a9466b35128eb135f638cc886aa2b9"></a> enumerator BK\_GATT\_UUID\_MANUFACTURER\_LIMITS

    <a id="_CPPv4N19bk_gatt_uuid_enum_t31BK_GATT_UUID_PROCESS_TOLERANCESE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t31BK_GATT_UUID_PROCESS_TOLERANCESE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t31BK_GATT_UUID_PROCESS_TOLERANCESE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a84bfbb9d18ad719dfd9f0f621560a577"></a> enumerator BK\_GATT\_UUID\_PROCESS\_TOLERANCES

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_IMD_TRIGGER_SETTINGE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_IMD_TRIGGER_SETTINGE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_IMD_TRIGGER_SETTINGE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ac7fed403f0b3f776441f0fd9c9264f38"></a> enumerator BK\_GATT\_UUID\_IMD\_TRIGGER\_SETTING

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_COOK_SENSOR_INFOE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_COOK_SENSOR_INFOE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_COOK_SENSOR_INFOE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a60a1210e4951646650d52c6b8f59f59b"></a> enumerator BK\_GATT\_UUID\_COOK\_SENSOR\_INFO

    <a id="_CPPv4N19bk_gatt_uuid_enum_t33BK_GATT_UUID_COOK_TRIGGER_SETTINGE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t33BK_GATT_UUID_COOK_TRIGGER_SETTINGE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t33BK_GATT_UUID_COOK_TRIGGER_SETTINGE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a6f3e4806e2b9fe61e555703fdade1bd4"></a> enumerator BK\_GATT\_UUID\_COOK\_TRIGGER\_SETTING

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_GAP_DEVICE_NAMEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_GAP_DEVICE_NAMEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_GAP_DEVICE_NAMEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ac73e8125eb0403e354e99e977b5e3587"></a> enumerator BK\_GATT\_UUID\_GAP\_DEVICE\_NAME
    :   GAP Profile Attributes.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_GAP_APPEARANCEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_GAP_APPEARANCEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_GAP_APPEARANCEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ad1d32b034cd6bd14201b15a17765aeb4"></a> enumerator BK\_GATT\_UUID\_GAP\_APPEARANCE

    <a id="_CPPv4N19bk_gatt_uuid_enum_t32BK_GATT_UUID_GAP_PREF_CONN_PARAME"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t32BK_GATT_UUID_GAP_PREF_CONN_PARAME"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t32BK_GATT_UUID_GAP_PREF_CONN_PARAME"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a74ae27a12d43f738c187a16da14d5051"></a> enumerator BK\_GATT\_UUID\_GAP\_PREF\_CONN\_PARAM

    <a id="_CPPv4N19bk_gatt_uuid_enum_t35BK_GATT_UUID_GAP_CENTRAL_ADDR_RESOLE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t35BK_GATT_UUID_GAP_CENTRAL_ADDR_RESOLE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t35BK_GATT_UUID_GAP_CENTRAL_ADDR_RESOLE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a9c21d7c526928e86441eaa922c99f042"></a> enumerator BK\_GATT\_UUID\_GAP\_CENTRAL\_ADDR\_RESOL

    <a id="_CPPv4N19bk_gatt_uuid_enum_t41BK_GATT_UUID_GAP_RESOLV_RPVIATE_ADDR_ONLYE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t41BK_GATT_UUID_GAP_RESOLV_RPVIATE_ADDR_ONLYE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t41BK_GATT_UUID_GAP_RESOLV_RPVIATE_ADDR_ONLYE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a5a7b53f7d5ceecc9e1e46f6f89e7ac0b"></a> enumerator BK\_GATT\_UUID\_GAP\_RESOLV\_RPVIATE\_ADDR\_ONLY

    <a id="_CPPv4N19bk_gatt_uuid_enum_t42BK_GATT_UUID_GAP_ENCRYPT_DATA_KEY_MATERIALE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t42BK_GATT_UUID_GAP_ENCRYPT_DATA_KEY_MATERIALE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t42BK_GATT_UUID_GAP_ENCRYPT_DATA_KEY_MATERIALE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a4e24561e50baf497c964be8a2b61dcef"></a> enumerator BK\_GATT\_UUID\_GAP\_ENCRYPT\_DATA\_KEY\_MATERIAL

    <a id="_CPPv4N19bk_gatt_uuid_enum_t38BK_GATT_UUID_GAP_BLE_GATT_SECURITY_LVLE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t38BK_GATT_UUID_GAP_BLE_GATT_SECURITY_LVLE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t38BK_GATT_UUID_GAP_BLE_GATT_SECURITY_LVLE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ab43d6bef886baf452ca4c9b047180448"></a> enumerator BK\_GATT\_UUID\_GAP\_BLE\_GATT\_SECURITY\_LVL

    <a id="_CPPv4N19bk_gatt_uuid_enum_t26BK_GATT_UUID_GATT_SRV_CHGDE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t26BK_GATT_UUID_GATT_SRV_CHGDE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t26BK_GATT_UUID_GATT_SRV_CHGDE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a98d7990ee222bb41ded48990164a176b"></a> enumerator BK\_GATT\_UUID\_GATT\_SRV\_CHGD
    :   Attribute Profile Attribute UUID.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t34BK_GATT_UUID_GATT_CLI_SUPPORT_FEATE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t34BK_GATT_UUID_GATT_CLI_SUPPORT_FEATE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t34BK_GATT_UUID_GATT_CLI_SUPPORT_FEATE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aa39587b78fd606934985382ddfddd259"></a> enumerator BK\_GATT\_UUID\_GATT\_CLI\_SUPPORT\_FEAT

    <a id="_CPPv4N19bk_gatt_uuid_enum_t31BK_GATT_UUID_GATT_DATABASE_HASHE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t31BK_GATT_UUID_GATT_DATABASE_HASHE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t31BK_GATT_UUID_GATT_DATABASE_HASHE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a0b10e2e4a5d04a0655abe093d87fea28"></a> enumerator BK\_GATT\_UUID\_GATT\_DATABASE\_HASH

    <a id="_CPPv4N19bk_gatt_uuid_enum_t34BK_GATT_UUID_GATT_SRV_SUPPORT_FEATE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t34BK_GATT_UUID_GATT_SRV_SUPPORT_FEATE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t34BK_GATT_UUID_GATT_SRV_SUPPORT_FEATE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a9124b17c5c3019cb369573318da21141"></a> enumerator BK\_GATT\_UUID\_GATT\_SRV\_SUPPORT\_FEAT

    <a id="_CPPv4N19bk_gatt_uuid_enum_t24BK_GATT_UUID_ALERT_LEVELE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t24BK_GATT_UUID_ALERT_LEVELE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t24BK_GATT_UUID_ALERT_LEVELE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a2b777161c3c7577f4388b2226cd5f072"></a> enumerator BK\_GATT\_UUID\_ALERT\_LEVEL
    :   Link BK\_Loss Service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_TX_POWER_LEVELE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_TX_POWER_LEVELE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_TX_POWER_LEVELE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a824ef4d728e6f26eec58f10aa9351489"></a> enumerator BK\_GATT\_UUID\_TX\_POWER\_LEVEL
    :   Alert Level.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t25BK_GATT_UUID_CURRENT_TIMEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t25BK_GATT_UUID_CURRENT_TIMEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t25BK_GATT_UUID_CURRENT_TIMEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a172fcf0b586865f00b79bfd1cfc1679e"></a> enumerator BK\_GATT\_UUID\_CURRENT\_TIME
    :   TX power level.

        Current Time Service

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_LOCAL_TIME_INFOE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_LOCAL_TIME_INFOE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_LOCAL_TIME_INFOE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a9a2c4838a3d842a155cd2de96821906c"></a> enumerator BK\_GATT\_UUID\_LOCAL\_TIME\_INFO
    :   Current Time.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t26BK_GATT_UUID_REF_TIME_INFOE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t26BK_GATT_UUID_REF_TIME_INFOE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t26BK_GATT_UUID_REF_TIME_INFOE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9acd2727ce3ee23164881ccdd519bb8f98"></a> enumerator BK\_GATT\_UUID\_REF\_TIME\_INFO
    :   Local time info.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t22BK_GATT_UUID_NW_STATUSE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t22BK_GATT_UUID_NW_STATUSE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t22BK_GATT_UUID_NW_STATUSE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a13d97eacad76b5d5230beb8cefaf04dc"></a> enumerator BK\_GATT\_UUID\_NW\_STATUS
    :   reference time information

        Network availability Profile

    <a id="_CPPv4N19bk_gatt_uuid_enum_t23BK_GATT_UUID_NW_TRIGGERE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t23BK_GATT_UUID_NW_TRIGGERE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t23BK_GATT_UUID_NW_TRIGGERE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a16ab4148036ae0cbbcd68f1a81c06a4e"></a> enumerator BK\_GATT\_UUID\_NW\_TRIGGER
    :   network availability status

    <a id="_CPPv4N19bk_gatt_uuid_enum_t25BK_GATT_UUID_ALERT_STATUSE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t25BK_GATT_UUID_ALERT_STATUSE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t25BK_GATT_UUID_ALERT_STATUSE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a03704e0013bf3c5102bf53d52104ab0b"></a> enumerator BK\_GATT\_UUID\_ALERT\_STATUS
    :   Network availability trigger.

        Phone alert

    <a id="_CPPv4N19bk_gatt_uuid_enum_t22BK_GATT_UUID_RINGER_CPE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t22BK_GATT_UUID_RINGER_CPE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t22BK_GATT_UUID_RINGER_CPE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a67dabfc536e18d152cfd56eef4f9f859"></a> enumerator BK\_GATT\_UUID\_RINGER\_CP
    :   alert status

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_RINGER_SETTINGE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_RINGER_SETTINGE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_RINGER_SETTINGE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a4d5a7a0c7af7517cef4051cde80c7a79"></a> enumerator BK\_GATT\_UUID\_RINGER\_SETTING
    :   ringer control point

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_GM_MEASUREMENTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_GM_MEASUREMENTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_GM_MEASUREMENTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a45abd0951ed5b5f62f8f9cba7403d9fa"></a> enumerator BK\_GATT\_UUID\_GM\_MEASUREMENT
    :   ringer setting

        Glucose Service

    <a id="_CPPv4N19bk_gatt_uuid_enum_t23BK_GATT_UUID_GM_CONTEXTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t23BK_GATT_UUID_GM_CONTEXTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t23BK_GATT_UUID_GM_CONTEXTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a0fe96ed13cec3f807833f801a37302d5"></a> enumerator BK\_GATT\_UUID\_GM\_CONTEXT

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_GM_CONTROL_POINTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_GM_CONTROL_POINTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_GM_CONTROL_POINTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a722a509afb7c46535b5013237e2205be"></a> enumerator BK\_GATT\_UUID\_GM\_CONTROL\_POINT

    <a id="_CPPv4N19bk_gatt_uuid_enum_t23BK_GATT_UUID_GM_FEATUREE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t23BK_GATT_UUID_GM_FEATUREE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t23BK_GATT_UUID_GM_FEATUREE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ac05ee291ad6a548456c37df22cd8a9ed"></a> enumerator BK\_GATT\_UUID\_GM\_FEATURE

    <a id="_CPPv4N19bk_gatt_uuid_enum_t22BK_GATT_UUID_SYSTEM_IDE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t22BK_GATT_UUID_SYSTEM_IDE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t22BK_GATT_UUID_SYSTEM_IDE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aef80d7b51dbabc98e52a679c944e8452"></a> enumerator BK\_GATT\_UUID\_SYSTEM\_ID
    :   device information characteristic

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_MODEL_NUMBER_STRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_MODEL_NUMBER_STRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_MODEL_NUMBER_STRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a1ea9a8c61bdbf596515895f633ae81a8"></a> enumerator BK\_GATT\_UUID\_MODEL\_NUMBER\_STR

    <a id="_CPPv4N19bk_gatt_uuid_enum_t30BK_GATT_UUID_SERIAL_NUMBER_STRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t30BK_GATT_UUID_SERIAL_NUMBER_STRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t30BK_GATT_UUID_SERIAL_NUMBER_STRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a87e301c40f5aa5b5b1717f7e25abc4c8"></a> enumerator BK\_GATT\_UUID\_SERIAL\_NUMBER\_STR

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_FW_VERSION_STRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_FW_VERSION_STRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_FW_VERSION_STRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a35450ea92ba18e35cd646af612d1c620"></a> enumerator BK\_GATT\_UUID\_FW\_VERSION\_STR

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HW_VERSION_STRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HW_VERSION_STRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HW_VERSION_STRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a47b62ab3a6f4b03fed745cd4a08cf20e"></a> enumerator BK\_GATT\_UUID\_HW\_VERSION\_STR

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_SW_VERSION_STRE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_SW_VERSION_STRE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_SW_VERSION_STRE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aa14bd02c58b7684bd11535b2c2466e85"></a> enumerator BK\_GATT\_UUID\_SW\_VERSION\_STR

    <a id="_CPPv4N19bk_gatt_uuid_enum_t22BK_GATT_UUID_MANU_NAMEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t22BK_GATT_UUID_MANU_NAMEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t22BK_GATT_UUID_MANU_NAMEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a04ceede7cc2d53edf01407ba18ac41d7"></a> enumerator BK\_GATT\_UUID\_MANU\_NAME

    <a id="_CPPv4N19bk_gatt_uuid_enum_t22BK_GATT_UUID_IEEE_DATAE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t22BK_GATT_UUID_IEEE_DATAE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t22BK_GATT_UUID_IEEE_DATAE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a25358d05f7d27883ecfa98b92ffd4cf3"></a> enumerator BK\_GATT\_UUID\_IEEE\_DATA

    <a id="_CPPv4N19bk_gatt_uuid_enum_t19BK_GATT_UUID_PNP_IDE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t19BK_GATT_UUID_PNP_IDE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t19BK_GATT_UUID_PNP_IDE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a6fa014214c76eeaf90bfa82044d87eaa"></a> enumerator BK\_GATT\_UUID\_PNP\_ID

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_HID_INFORMATIONE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_HID_INFORMATIONE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_HID_INFORMATIONE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aff479ff19d6be7ca162760ed2cee63bd"></a> enumerator BK\_GATT\_UUID\_HID\_INFORMATION
    :   HID characteristics.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HID_REPORT_MAPE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HID_REPORT_MAPE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HID_REPORT_MAPE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9adda9213dff410aa420ab7078bf989f1a"></a> enumerator BK\_GATT\_UUID\_HID\_REPORT\_MAP

    <a id="_CPPv4N19bk_gatt_uuid_enum_t30BK_GATT_UUID_HID_CONTROL_POINTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t30BK_GATT_UUID_HID_CONTROL_POINTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t30BK_GATT_UUID_HID_CONTROL_POINTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9aa45d4342db30deacbeeb4658e68a50be"></a> enumerator BK\_GATT\_UUID\_HID\_CONTROL\_POINT

    <a id="_CPPv4N19bk_gatt_uuid_enum_t23BK_GATT_UUID_HID_REPORTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t23BK_GATT_UUID_HID_REPORTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t23BK_GATT_UUID_HID_REPORTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a64fd4d1a41c0f20e2d8924befe958fa7"></a> enumerator BK\_GATT\_UUID\_HID\_REPORT

    <a id="_CPPv4N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HID_PROTO_MODEE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HID_PROTO_MODEE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t27BK_GATT_UUID_HID_PROTO_MODEE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a390fda60c79d8b535ed8207d1e7a7c10"></a> enumerator BK\_GATT\_UUID\_HID\_PROTO\_MODE

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_HID_BT_KB_INPUTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_HID_BT_KB_INPUTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_HID_BT_KB_INPUTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a69f14fd12d9f3f90c0c16afefe6d93bb"></a> enumerator BK\_GATT\_UUID\_HID\_BT\_KB\_INPUT

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_HID_BT_KB_OUTPUTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_HID_BT_KB_OUTPUTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_HID_BT_KB_OUTPUTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a32ad1b984ef5c036d427b978f04540b3"></a> enumerator BK\_GATT\_UUID\_HID\_BT\_KB\_OUTPUT

    <a id="_CPPv4N19bk_gatt_uuid_enum_t31BK_GATT_UUID_HID_BT_MOUSE_INPUTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t31BK_GATT_UUID_HID_BT_MOUSE_INPUTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t31BK_GATT_UUID_HID_BT_MOUSE_INPUTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a71391d9b45382c34480ac0e82bbffdff"></a> enumerator BK\_GATT\_UUID\_HID\_BT\_MOUSE\_INPUT

    <a id="_CPPv4N19bk_gatt_uuid_enum_t23BK_GATT_HEART_RATE_MEASE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t23BK_GATT_HEART_RATE_MEASE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t23BK_GATT_HEART_RATE_MEASE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a8e053a2d42d807b5db176be11936dc4e"></a> enumerator BK\_GATT\_HEART\_RATE\_MEAS
    :   Heart Rate Measurement.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_BODY_SENSOR_LOCATIONE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_BODY_SENSOR_LOCATIONE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_BODY_SENSOR_LOCATIONE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ad2c80de000c9160949a80796d100ca0c"></a> enumerator BK\_GATT\_BODY\_SENSOR\_LOCATION
    :   Body Sensor Location.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_HEART_RATE_CNTL_POINTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_HEART_RATE_CNTL_POINTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_HEART_RATE_CNTL_POINTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a816bc2c8287b681e32c98ebae62c7c00"></a> enumerator BK\_GATT\_HEART\_RATE\_CNTL\_POINT
    :   Heart Rate Control Point.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t26BK_GATT_UUID_BATTERY_LEVELE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t26BK_GATT_UUID_BATTERY_LEVELE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t26BK_GATT_UUID_BATTERY_LEVELE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9af22a8f7a333957e4489c0d8590d3ddf8"></a> enumerator BK\_GATT\_UUID\_BATTERY\_LEVEL
    :   Battery Service characteristics.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t29BK_GATT_UUID_SC_CONTROL_POINTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t29BK_GATT_UUID_SC_CONTROL_POINTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t29BK_GATT_UUID_SC_CONTROL_POINTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a7f85322551a96e2ec5b0cf35f4c43d90"></a> enumerator BK\_GATT\_UUID\_SC\_CONTROL\_POINT
    :   Sensor Service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_SENSOR_LOCATIONE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_SENSOR_LOCATIONE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_SENSOR_LOCATIONE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a5f7a63755481fbcbb52d5de3133b43a8"></a> enumerator BK\_GATT\_UUID\_SENSOR\_LOCATION

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_RSC_MEASUREMENTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_RSC_MEASUREMENTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_RSC_MEASUREMENTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a496df0fabf93f1a1178df342ea46e9bc"></a> enumerator BK\_GATT\_UUID\_RSC\_MEASUREMENT
    :   Runners speed and cadence service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t24BK_GATT_UUID_RSC_FEATUREE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t24BK_GATT_UUID_RSC_FEATUREE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t24BK_GATT_UUID_RSC_FEATUREE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a45436871d9368c9de700898444d3d9db"></a> enumerator BK\_GATT\_UUID\_RSC\_FEATURE

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_CSC_MEASUREMENTE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_CSC_MEASUREMENTE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_CSC_MEASUREMENTE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ac09315177bb46a5014f9724b10ab621f"></a> enumerator BK\_GATT\_UUID\_CSC\_MEASUREMENT
    :   Cycling speed and cadence service.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t24BK_GATT_UUID_CSC_FEATUREE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t24BK_GATT_UUID_CSC_FEATUREE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t24BK_GATT_UUID_CSC_FEATUREE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9ab5041f5f29acb14a5ee5ee3fc74d0169"></a> enumerator BK\_GATT\_UUID\_CSC\_FEATURE

    <a id="_CPPv4N19bk_gatt_uuid_enum_t28BK_GATT_UUID_SCAN_INT_WINDOWE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t28BK_GATT_UUID_SCAN_INT_WINDOWE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t28BK_GATT_UUID_SCAN_INT_WINDOWE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9a82e2ed83d86a7c8c14b20db9a31abb81"></a> enumerator BK\_GATT\_UUID\_SCAN\_INT\_WINDOW
    :   Scan BK\_Parameter characteristics.

    <a id="_CPPv4N19bk_gatt_uuid_enum_t25BK_GATT_UUID_SCAN_REFRESHE"></a>

    <a id="_CPPv3N19bk_gatt_uuid_enum_t25BK_GATT_UUID_SCAN_REFRESHE"></a> <a id="_CPPv2N19bk_gatt_uuid_enum_t25BK_GATT_UUID_SCAN_REFRESHE"></a> <a id="group__dm__gatt__types__v1_1gga96957f08912423621a21377bae694ca9acdcb9a7887c588469939c71c2341cb6d"></a> enumerator BK\_GATT\_UUID\_SCAN\_REFRESH

<a id="_CPPv416bk_gatt_status_t"></a>

<a id="_CPPv316bk_gatt_status_t"></a> <a id="_CPPv216bk_gatt_status_t"></a> <a id="group__dm__gatt__types__v1_1ga431c805fe6dbfe9db180c467fd1625d5"></a> enum bk\_gatt\_status\_t
:   GATT success code and error codes.

    *Values:*

    <a id="_CPPv4N16bk_gatt_status_t10BK_GATT_OKE"></a>

    <a id="_CPPv3N16bk_gatt_status_t10BK_GATT_OKE"></a> <a id="_CPPv2N16bk_gatt_status_t10BK_GATT_OKE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5ac4ffab417d0b0242e401350f32648804"></a> enumerator BK\_GATT\_OK

    <a id="_CPPv4N16bk_gatt_status_t22BK_GATT_INVALID_HANDLEE"></a>

    <a id="_CPPv3N16bk_gatt_status_t22BK_GATT_INVALID_HANDLEE"></a> <a id="_CPPv2N16bk_gatt_status_t22BK_GATT_INVALID_HANDLEE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5aa4a2a5e6117693ea5382153dee13a255"></a> enumerator BK\_GATT\_INVALID\_HANDLE

    <a id="_CPPv4N16bk_gatt_status_t23BK_GATT_READ_NOT_PERMITE"></a>

    <a id="_CPPv3N16bk_gatt_status_t23BK_GATT_READ_NOT_PERMITE"></a> <a id="_CPPv2N16bk_gatt_status_t23BK_GATT_READ_NOT_PERMITE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5afd5cc0f8696f13775a79abe91fdb8eb8"></a> enumerator BK\_GATT\_READ\_NOT\_PERMIT

    <a id="_CPPv4N16bk_gatt_status_t24BK_GATT_WRITE_NOT_PERMITE"></a>

    <a id="_CPPv3N16bk_gatt_status_t24BK_GATT_WRITE_NOT_PERMITE"></a> <a id="_CPPv2N16bk_gatt_status_t24BK_GATT_WRITE_NOT_PERMITE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a136ca80e08a2ab9b9ee0d559ceb71ff6"></a> enumerator BK\_GATT\_WRITE\_NOT\_PERMIT

    <a id="_CPPv4N16bk_gatt_status_t19BK_GATT_INVALID_PDUE"></a>

    <a id="_CPPv3N16bk_gatt_status_t19BK_GATT_INVALID_PDUE"></a> <a id="_CPPv2N16bk_gatt_status_t19BK_GATT_INVALID_PDUE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5aee033d69817cd2500727f714d4059661"></a> enumerator BK\_GATT\_INVALID\_PDU

    <a id="_CPPv4N16bk_gatt_status_t28BK_GATT_INSUF_AUTHENTICATIONE"></a>

    <a id="_CPPv3N16bk_gatt_status_t28BK_GATT_INSUF_AUTHENTICATIONE"></a> <a id="_CPPv2N16bk_gatt_status_t28BK_GATT_INSUF_AUTHENTICATIONE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a575b836338f8ac8de1ea5fa1e0c0f7ef"></a> enumerator BK\_GATT\_INSUF\_AUTHENTICATION

    <a id="_CPPv4N16bk_gatt_status_t25BK_GATT_REQ_NOT_SUPPORTEDE"></a>

    <a id="_CPPv3N16bk_gatt_status_t25BK_GATT_REQ_NOT_SUPPORTEDE"></a> <a id="_CPPv2N16bk_gatt_status_t25BK_GATT_REQ_NOT_SUPPORTEDE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a33edeeec797505a724a194154b315b1a"></a> enumerator BK\_GATT\_REQ\_NOT\_SUPPORTED

    <a id="_CPPv4N16bk_gatt_status_t22BK_GATT_INVALID_OFFSETE"></a>

    <a id="_CPPv3N16bk_gatt_status_t22BK_GATT_INVALID_OFFSETE"></a> <a id="_CPPv2N16bk_gatt_status_t22BK_GATT_INVALID_OFFSETE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a23700aeac8f86a379ee3c961ee817f34"></a> enumerator BK\_GATT\_INVALID\_OFFSET

    <a id="_CPPv4N16bk_gatt_status_t27BK_GATT_INSUF_AUTHORIZATIONE"></a>

    <a id="_CPPv3N16bk_gatt_status_t27BK_GATT_INSUF_AUTHORIZATIONE"></a> <a id="_CPPv2N16bk_gatt_status_t27BK_GATT_INSUF_AUTHORIZATIONE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a3271d0a9c9d23da5ce7b1262e8d300ec"></a> enumerator BK\_GATT\_INSUF\_AUTHORIZATION

    <a id="_CPPv4N16bk_gatt_status_t22BK_GATT_PREPARE_Q_FULLE"></a>

    <a id="_CPPv3N16bk_gatt_status_t22BK_GATT_PREPARE_Q_FULLE"></a> <a id="_CPPv2N16bk_gatt_status_t22BK_GATT_PREPARE_Q_FULLE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a0e1703bab8adc96d9f45bd91c8393fd6"></a> enumerator BK\_GATT\_PREPARE\_Q\_FULL

    <a id="_CPPv4N16bk_gatt_status_t17BK_GATT_NOT_FOUNDE"></a>

    <a id="_CPPv3N16bk_gatt_status_t17BK_GATT_NOT_FOUNDE"></a> <a id="_CPPv2N16bk_gatt_status_t17BK_GATT_NOT_FOUNDE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5aa1341a81f2b0cfcfa61798e792c53fcd"></a> enumerator BK\_GATT\_NOT\_FOUND

    <a id="_CPPv4N16bk_gatt_status_t16BK_GATT_NOT_LONGE"></a>

    <a id="_CPPv3N16bk_gatt_status_t16BK_GATT_NOT_LONGE"></a> <a id="_CPPv2N16bk_gatt_status_t16BK_GATT_NOT_LONGE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a26f8ca976c042a93c2c0856dc410ec4c"></a> enumerator BK\_GATT\_NOT\_LONG

    <a id="_CPPv4N16bk_gatt_status_t22BK_GATT_INSUF_KEY_SIZEE"></a>

    <a id="_CPPv3N16bk_gatt_status_t22BK_GATT_INSUF_KEY_SIZEE"></a> <a id="_CPPv2N16bk_gatt_status_t22BK_GATT_INSUF_KEY_SIZEE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5ab78c22096682abf123561ef73e480d19"></a> enumerator BK\_GATT\_INSUF\_KEY\_SIZE

    <a id="_CPPv4N16bk_gatt_status_t24BK_GATT_INVALID_ATTR_LENE"></a>

    <a id="_CPPv3N16bk_gatt_status_t24BK_GATT_INVALID_ATTR_LENE"></a> <a id="_CPPv2N16bk_gatt_status_t24BK_GATT_INVALID_ATTR_LENE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a7e9261d570b3dca45c9d9cafa713f310"></a> enumerator BK\_GATT\_INVALID\_ATTR\_LEN

    <a id="_CPPv4N16bk_gatt_status_t20BK_GATT_ERR_UNLIKELYE"></a>

    <a id="_CPPv3N16bk_gatt_status_t20BK_GATT_ERR_UNLIKELYE"></a> <a id="_CPPv2N16bk_gatt_status_t20BK_GATT_ERR_UNLIKELYE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a02eb0340146f3894a142bc450f1b94cf"></a> enumerator BK\_GATT\_ERR\_UNLIKELY

    <a id="_CPPv4N16bk_gatt_status_t24BK_GATT_INSUF_ENCRYPTIONE"></a>

    <a id="_CPPv3N16bk_gatt_status_t24BK_GATT_INSUF_ENCRYPTIONE"></a> <a id="_CPPv2N16bk_gatt_status_t24BK_GATT_INSUF_ENCRYPTIONE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5ae6eef49764154bd140a09ca897724504"></a> enumerator BK\_GATT\_INSUF\_ENCRYPTION

    <a id="_CPPv4N16bk_gatt_status_t26BK_GATT_UNSUPPORT_GRP_TYPEE"></a>

    <a id="_CPPv3N16bk_gatt_status_t26BK_GATT_UNSUPPORT_GRP_TYPEE"></a> <a id="_CPPv2N16bk_gatt_status_t26BK_GATT_UNSUPPORT_GRP_TYPEE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a40cbe3680bc8295040eb731d69356f8d"></a> enumerator BK\_GATT\_UNSUPPORT\_GRP\_TYPE

    <a id="_CPPv4N16bk_gatt_status_t22BK_GATT_INSUF_RESOURCEE"></a>

    <a id="_CPPv3N16bk_gatt_status_t22BK_GATT_INSUF_RESOURCEE"></a> <a id="_CPPv2N16bk_gatt_status_t22BK_GATT_INSUF_RESOURCEE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5ac7aa2b2412d84edc15c5b9a2ea581093"></a> enumerator BK\_GATT\_INSUF\_RESOURCE

    <a id="_CPPv4N16bk_gatt_status_t22BK_GATT_DB_OUT_OF_SYNCE"></a>

    <a id="_CPPv3N16bk_gatt_status_t22BK_GATT_DB_OUT_OF_SYNCE"></a> <a id="_CPPv2N16bk_gatt_status_t22BK_GATT_DB_OUT_OF_SYNCE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5ae9c41be258ae706ede079005bdaa1408"></a> enumerator BK\_GATT\_DB\_OUT\_OF\_SYNC

    <a id="_CPPv4N16bk_gatt_status_t27BK_GATT_PARAM_VAL_NOT_ALLOWE"></a>

    <a id="_CPPv3N16bk_gatt_status_t27BK_GATT_PARAM_VAL_NOT_ALLOWE"></a> <a id="_CPPv2N16bk_gatt_status_t27BK_GATT_PARAM_VAL_NOT_ALLOWE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a499ad07ee0a58ba63e8fbb77b1724790"></a> enumerator BK\_GATT\_PARAM\_VAL\_NOT\_ALLOW

    <a id="_CPPv4N16bk_gatt_status_t24BK_GATT_WRITE_REQ_REJECTE"></a>

    <a id="_CPPv3N16bk_gatt_status_t24BK_GATT_WRITE_REQ_REJECTE"></a> <a id="_CPPv2N16bk_gatt_status_t24BK_GATT_WRITE_REQ_REJECTE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a9180004268a490f6924456200c405a41"></a> enumerator BK\_GATT\_WRITE\_REQ\_REJECT

    <a id="_CPPv4N16bk_gatt_status_t19BK_GATT_CCC_CFG_ERRE"></a>

    <a id="_CPPv3N16bk_gatt_status_t19BK_GATT_CCC_CFG_ERRE"></a> <a id="_CPPv2N16bk_gatt_status_t19BK_GATT_CCC_CFG_ERRE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5aa8651c95d0fc3fd3b53dd34bf4f2c48f"></a> enumerator BK\_GATT\_CCC\_CFG\_ERR
    :   Write Request Rejected.

    <a id="_CPPv4N16bk_gatt_status_t23BK_GATT_PRC_IN_PROGRESSE"></a>

    <a id="_CPPv3N16bk_gatt_status_t23BK_GATT_PRC_IN_PROGRESSE"></a> <a id="_CPPv2N16bk_gatt_status_t23BK_GATT_PRC_IN_PROGRESSE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5ae24d3444d20fd95c72f00433245a7abf"></a> enumerator BK\_GATT\_PRC\_IN\_PROGRESS
    :   0xFD Client Characteristic Configuration Descriptor Improperly Configured

    <a id="_CPPv4N16bk_gatt_status_t20BK_GATT_OUT_OF_RANGEE"></a>

    <a id="_CPPv3N16bk_gatt_status_t20BK_GATT_OUT_OF_RANGEE"></a> <a id="_CPPv2N16bk_gatt_status_t20BK_GATT_OUT_OF_RANGEE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a59d490174407c284dce3d05f87d4c31a"></a> enumerator BK\_GATT\_OUT\_OF\_RANGE
    :   0xFE Procedure Already in progress

    <a id="_CPPv4N16bk_gatt_status_t21BK_GATT_UNKNOWN_ERRORE"></a>

    <a id="_CPPv3N16bk_gatt_status_t21BK_GATT_UNKNOWN_ERRORE"></a> <a id="_CPPv2N16bk_gatt_status_t21BK_GATT_UNKNOWN_ERRORE"></a> <a id="group__dm__gatt__types__v1_1gga431c805fe6dbfe9db180c467fd1625d5a07d5e2c59fc0dd17cc83f4a1048547a1"></a> enumerator BK\_GATT\_UNKNOWN\_ERROR
    :   0xFF Attribute value out of range \*/

<a id="_CPPv421bk_gatt_conn_reason_t"></a>

<a id="_CPPv321bk_gatt_conn_reason_t"></a> <a id="_CPPv221bk_gatt_conn_reason_t"></a> <a id="group__dm__gatt__types__v1_1ga8df1d0d5112f9dbb74ecaea6aa9c6cbb"></a> enum bk\_gatt\_conn\_reason\_t
:   Gatt Connection reason enum.

    *Values:*

    <a id="_CPPv4N21bk_gatt_conn_reason_t20BK_GATT_CONN_UNKNOWNE"></a>

    <a id="_CPPv3N21bk_gatt_conn_reason_t20BK_GATT_CONN_UNKNOWNE"></a> <a id="_CPPv2N21bk_gatt_conn_reason_t20BK_GATT_CONN_UNKNOWNE"></a> <a id="group__dm__gatt__types__v1_1gga8df1d0d5112f9dbb74ecaea6aa9c6cbba67f7ca4e822928fa0864d9172f435efa"></a> enumerator BK\_GATT\_CONN\_UNKNOWN
    :   Gatt connection unknown

<a id="_CPPv418bk_gatt_auth_req_t"></a>

<a id="_CPPv318bk_gatt_auth_req_t"></a> <a id="_CPPv218bk_gatt_auth_req_t"></a> <a id="group__dm__gatt__types__v1_1gaf8e0f1db3c43602013aca95cd688b85f"></a> enum bk\_gatt\_auth\_req\_t
:   Gatt authentication request type.

    *Values:*

    <a id="_CPPv4N18bk_gatt_auth_req_t21BK_GATT_AUTH_REQ_NONEE"></a>

    <a id="_CPPv3N18bk_gatt_auth_req_t21BK_GATT_AUTH_REQ_NONEE"></a> <a id="_CPPv2N18bk_gatt_auth_req_t21BK_GATT_AUTH_REQ_NONEE"></a> <a id="group__dm__gatt__types__v1_1ggaf8e0f1db3c43602013aca95cd688b85fa34acda39943a0eee3bc3e1d11f7f7c95"></a> enumerator BK\_GATT\_AUTH\_REQ\_NONE

<a id="_CPPv419bk_gatt_perm_enum_t"></a>

<a id="_CPPv319bk_gatt_perm_enum_t"></a> <a id="_CPPv219bk_gatt_perm_enum_t"></a> <a id="group__dm__gatt__types__v1_1ga47b9277fda6e83083b3792135f1c8422"></a> enum bk\_gatt\_perm\_enum\_t
:   Attribute permissions.

    **Attention**
    :   When MITM is enable, key generation method can not be Just Work. This require both local and peer iocap configuration suitable. See bluetooth core specification Version 5.4 \| Vol 3, Part H, 2.3.5.1 Selecting key generation method.

    *Values:*

    <a id="_CPPv4N19bk_gatt_perm_enum_t17BK_GATT_PERM_READE"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t17BK_GATT_PERM_READE"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t17BK_GATT_PERM_READE"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422a22678ed7b040d66c91c958a8b8ec61fc"></a> enumerator BK\_GATT\_PERM\_READ

    <a id="_CPPv4N19bk_gatt_perm_enum_t27BK_GATT_PERM_READ_ENCRYPTEDE"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t27BK_GATT_PERM_READ_ENCRYPTEDE"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t27BK_GATT_PERM_READ_ENCRYPTEDE"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422abc877c5e7af9c941e8e5213ec8383bd3"></a> enumerator BK\_GATT\_PERM\_READ\_ENCRYPTED

    <a id="_CPPv4N19bk_gatt_perm_enum_t26BK_GATT_PERM_READ_ENC_MITME"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t26BK_GATT_PERM_READ_ENC_MITME"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t26BK_GATT_PERM_READ_ENC_MITME"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422a2d55d823c7de6860cc4d204f9d218c95"></a> enumerator BK\_GATT\_PERM\_READ\_ENC\_MITM

    <a id="_CPPv4N19bk_gatt_perm_enum_t18BK_GATT_PERM_WRITEE"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t18BK_GATT_PERM_WRITEE"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t18BK_GATT_PERM_WRITEE"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422a7aa49222cd280487913c219ccf7b2726"></a> enumerator BK\_GATT\_PERM\_WRITE

    <a id="_CPPv4N19bk_gatt_perm_enum_t28BK_GATT_PERM_WRITE_ENCRYPTEDE"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t28BK_GATT_PERM_WRITE_ENCRYPTEDE"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t28BK_GATT_PERM_WRITE_ENCRYPTEDE"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422a7e0a632c894c550e99db4e2b38567959"></a> enumerator BK\_GATT\_PERM\_WRITE\_ENCRYPTED

    <a id="_CPPv4N19bk_gatt_perm_enum_t27BK_GATT_PERM_WRITE_ENC_MITME"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t27BK_GATT_PERM_WRITE_ENC_MITME"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t27BK_GATT_PERM_WRITE_ENC_MITME"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422a9058eee7d18db0dc4e840928862f0ae9"></a> enumerator BK\_GATT\_PERM\_WRITE\_ENC\_MITM

    <a id="_CPPv4N19bk_gatt_perm_enum_t25BK_GATT_PERM_WRITE_SIGNEDE"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t25BK_GATT_PERM_WRITE_SIGNEDE"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t25BK_GATT_PERM_WRITE_SIGNEDE"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422acf5502b1214989a1994748f48517021e"></a> enumerator BK\_GATT\_PERM\_WRITE\_SIGNED

    <a id="_CPPv4N19bk_gatt_perm_enum_t30BK_GATT_PERM_WRITE_SIGNED_MITME"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t30BK_GATT_PERM_WRITE_SIGNED_MITME"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t30BK_GATT_PERM_WRITE_SIGNED_MITME"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422abaf6d47d36ef3f1a3904e4f1eca1377d"></a> enumerator BK\_GATT\_PERM\_WRITE\_SIGNED\_MITM

    <a id="_CPPv4N19bk_gatt_perm_enum_t31BK_GATT_PERM_READ_AUTHORIZATIONE"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t31BK_GATT_PERM_READ_AUTHORIZATIONE"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t31BK_GATT_PERM_READ_AUTHORIZATIONE"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422a720c05d07930b4e5bf9fa20ff7e06362"></a> enumerator BK\_GATT\_PERM\_READ\_AUTHORIZATION

    <a id="_CPPv4N19bk_gatt_perm_enum_t32BK_GATT_PERM_WRITE_AUTHORIZATIONE"></a>

    <a id="_CPPv3N19bk_gatt_perm_enum_t32BK_GATT_PERM_WRITE_AUTHORIZATIONE"></a> <a id="_CPPv2N19bk_gatt_perm_enum_t32BK_GATT_PERM_WRITE_AUTHORIZATIONE"></a> <a id="group__dm__gatt__types__v1_1gga47b9277fda6e83083b3792135f1c8422a93f7dacf7ff72e9b54acab038a7e3b43"></a> enumerator BK\_GATT\_PERM\_WRITE\_AUTHORIZATION

<a id="_CPPv424bk_gatt_char_prop_enum_t"></a>

<a id="_CPPv324bk_gatt_char_prop_enum_t"></a> <a id="_CPPv224bk_gatt_char_prop_enum_t"></a> <a id="group__dm__gatt__types__v1_1ga24c775f26c7322eb059d1aa42bb48b1a"></a> enum bk\_gatt\_char\_prop\_enum\_t
:   definition of characteristic properties

    *Values:*

    <a id="_CPPv4N24bk_gatt_char_prop_enum_t31BK_GATT_CHAR_PROP_BIT_BROADCASTE"></a>

    <a id="_CPPv3N24bk_gatt_char_prop_enum_t31BK_GATT_CHAR_PROP_BIT_BROADCASTE"></a> <a id="_CPPv2N24bk_gatt_char_prop_enum_t31BK_GATT_CHAR_PROP_BIT_BROADCASTE"></a> <a id="group__dm__gatt__types__v1_1gga24c775f26c7322eb059d1aa42bb48b1aa1f6fd43fe95c1eb0c65a77556d5c063d"></a> enumerator BK\_GATT\_CHAR\_PROP\_BIT\_BROADCAST

    <a id="_CPPv4N24bk_gatt_char_prop_enum_t26BK_GATT_CHAR_PROP_BIT_READE"></a>

    <a id="_CPPv3N24bk_gatt_char_prop_enum_t26BK_GATT_CHAR_PROP_BIT_READE"></a> <a id="_CPPv2N24bk_gatt_char_prop_enum_t26BK_GATT_CHAR_PROP_BIT_READE"></a> <a id="group__dm__gatt__types__v1_1gga24c775f26c7322eb059d1aa42bb48b1aafcedc39e03e177fc0cd5a7193c69b98f"></a> enumerator BK\_GATT\_CHAR\_PROP\_BIT\_READ

    <a id="_CPPv4N24bk_gatt_char_prop_enum_t30BK_GATT_CHAR_PROP_BIT_WRITE_NRE"></a>

    <a id="_CPPv3N24bk_gatt_char_prop_enum_t30BK_GATT_CHAR_PROP_BIT_WRITE_NRE"></a> <a id="_CPPv2N24bk_gatt_char_prop_enum_t30BK_GATT_CHAR_PROP_BIT_WRITE_NRE"></a> <a id="group__dm__gatt__types__v1_1gga24c775f26c7322eb059d1aa42bb48b1aa2a3618492344c325fa580cee1fc0aae5"></a> enumerator BK\_GATT\_CHAR\_PROP\_BIT\_WRITE\_NR

    <a id="_CPPv4N24bk_gatt_char_prop_enum_t27BK_GATT_CHAR_PROP_BIT_WRITEE"></a>

    <a id="_CPPv3N24bk_gatt_char_prop_enum_t27BK_GATT_CHAR_PROP_BIT_WRITEE"></a> <a id="_CPPv2N24bk_gatt_char_prop_enum_t27BK_GATT_CHAR_PROP_BIT_WRITEE"></a> <a id="group__dm__gatt__types__v1_1gga24c775f26c7322eb059d1aa42bb48b1aaf67919f5917396336672f03878360fe3"></a> enumerator BK\_GATT\_CHAR\_PROP\_BIT\_WRITE

    <a id="_CPPv4N24bk_gatt_char_prop_enum_t28BK_GATT_CHAR_PROP_BIT_NOTIFYE"></a>

    <a id="_CPPv3N24bk_gatt_char_prop_enum_t28BK_GATT_CHAR_PROP_BIT_NOTIFYE"></a> <a id="_CPPv2N24bk_gatt_char_prop_enum_t28BK_GATT_CHAR_PROP_BIT_NOTIFYE"></a> <a id="group__dm__gatt__types__v1_1gga24c775f26c7322eb059d1aa42bb48b1aa6255d8cd061eca8e0cfce3c6570f34ae"></a> enumerator BK\_GATT\_CHAR\_PROP\_BIT\_NOTIFY

    <a id="_CPPv4N24bk_gatt_char_prop_enum_t30BK_GATT_CHAR_PROP_BIT_INDICATEE"></a>

    <a id="_CPPv3N24bk_gatt_char_prop_enum_t30BK_GATT_CHAR_PROP_BIT_INDICATEE"></a> <a id="_CPPv2N24bk_gatt_char_prop_enum_t30BK_GATT_CHAR_PROP_BIT_INDICATEE"></a> <a id="group__dm__gatt__types__v1_1gga24c775f26c7322eb059d1aa42bb48b1aa9666873807230777f46163d739c9d572"></a> enumerator BK\_GATT\_CHAR\_PROP\_BIT\_INDICATE

    <a id="_CPPv4N24bk_gatt_char_prop_enum_t39BK_GATT_CHAR_PROP_BIT_AUTH_SIGNED_WRITEE"></a>

    <a id="_CPPv3N24bk_gatt_char_prop_enum_t39BK_GATT_CHAR_PROP_BIT_AUTH_SIGNED_WRITEE"></a> <a id="_CPPv2N24bk_gatt_char_prop_enum_t39BK_GATT_CHAR_PROP_BIT_AUTH_SIGNED_WRITEE"></a> <a id="group__dm__gatt__types__v1_1gga24c775f26c7322eb059d1aa42bb48b1aa6c10c8d03ae8eff61fa10f12e07a2abf"></a> enumerator BK\_GATT\_CHAR\_PROP\_BIT\_AUTH\_SIGNED\_WRITE

    <a id="_CPPv4N24bk_gatt_char_prop_enum_t30BK_GATT_CHAR_PROP_BIT_EXT_PROPE"></a>

    <a id="_CPPv3N24bk_gatt_char_prop_enum_t30BK_GATT_CHAR_PROP_BIT_EXT_PROPE"></a> <a id="_CPPv2N24bk_gatt_char_prop_enum_t30BK_GATT_CHAR_PROP_BIT_EXT_PROPE"></a> <a id="group__dm__gatt__types__v1_1gga24c775f26c7322eb059d1aa42bb48b1aa98ceeab2f5300b856805035751530b61"></a> enumerator BK\_GATT\_CHAR\_PROP\_BIT\_EXT\_PROP

<a id="_CPPv419bk_service_source_t"></a>

<a id="_CPPv319bk_service_source_t"></a> <a id="_CPPv219bk_service_source_t"></a> <a id="group__dm__gatt__types__v1_1ga299d081f931ab85067ed76d6a256fe6d"></a> enum bk\_service\_source\_t
:   gatt service source

    *Values:*

    <a id="_CPPv4N19bk_service_source_t34BK_GATT_SERVICE_FROM_REMOTE_DEVICEE"></a>

    <a id="_CPPv3N19bk_service_source_t34BK_GATT_SERVICE_FROM_REMOTE_DEVICEE"></a> <a id="_CPPv2N19bk_service_source_t34BK_GATT_SERVICE_FROM_REMOTE_DEVICEE"></a> <a id="group__dm__gatt__types__v1_1gga299d081f931ab85067ed76d6a256fe6dae17272eeff6c7d49a0d35d5293727401"></a> enumerator BK\_GATT\_SERVICE\_FROM\_REMOTE\_DEVICE

    <a id="_CPPv4N19bk_service_source_t30BK_GATT_SERVICE_FROM_NVS_FLASHE"></a>

    <a id="_CPPv3N19bk_service_source_t30BK_GATT_SERVICE_FROM_NVS_FLASHE"></a> <a id="_CPPv2N19bk_service_source_t30BK_GATT_SERVICE_FROM_NVS_FLASHE"></a> <a id="group__dm__gatt__types__v1_1gga299d081f931ab85067ed76d6a256fe6da6a27a92e4de207a6ec450a6b66f6ad43"></a> enumerator BK\_GATT\_SERVICE\_FROM\_NVS\_FLASH

    <a id="_CPPv4N19bk_service_source_t28BK_GATT_SERVICE_FROM_UNKNOWNE"></a>

    <a id="_CPPv3N19bk_service_source_t28BK_GATT_SERVICE_FROM_UNKNOWNE"></a> <a id="_CPPv2N19bk_service_source_t28BK_GATT_SERVICE_FROM_UNKNOWNE"></a> <a id="group__dm__gatt__types__v1_1gga299d081f931ab85067ed76d6a256fe6daaa53561d2a8702b3465f8cd715be9208"></a> enumerator BK\_GATT\_SERVICE\_FROM\_UNKNOWN

<a id="_CPPv420bk_gatt_write_type_t"></a>

<a id="_CPPv320bk_gatt_write_type_t"></a> <a id="_CPPv220bk_gatt_write_type_t"></a> <a id="group__dm__gatt__types__v1_1ga492e8d84dd5b68d5f28b521386939a26"></a> enum bk\_gatt\_write\_type\_t
:   Gatt write type.

    *Values:*

    <a id="_CPPv4N20bk_gatt_write_type_t25BK_GATT_WRITE_TYPE_NO_RSPE"></a>

    <a id="_CPPv3N20bk_gatt_write_type_t25BK_GATT_WRITE_TYPE_NO_RSPE"></a> <a id="_CPPv2N20bk_gatt_write_type_t25BK_GATT_WRITE_TYPE_NO_RSPE"></a> <a id="group__dm__gatt__types__v1_1gga492e8d84dd5b68d5f28b521386939a26ad2c0e093553ab9cf3b4787520eaf021b"></a> enumerator BK\_GATT\_WRITE\_TYPE\_NO\_RSP
    :   Gatt write attribute need no response

    <a id="_CPPv4N20bk_gatt_write_type_t22BK_GATT_WRITE_TYPE_RSPE"></a>

    <a id="_CPPv3N20bk_gatt_write_type_t22BK_GATT_WRITE_TYPE_RSPE"></a> <a id="_CPPv2N20bk_gatt_write_type_t22BK_GATT_WRITE_TYPE_RSPE"></a> <a id="group__dm__gatt__types__v1_1gga492e8d84dd5b68d5f28b521386939a26a3796d077f5702b8c21be985880f98724"></a> enumerator BK\_GATT\_WRITE\_TYPE\_RSP
    :   Gatt write attribute need remote response

<a id="bk-dm-bluetooth-h"></a>

## bk\_dm\_bluetooth.h

`bk_dm_bluetooth.h` 提供 Bluetooth 通用 API 和通用初始化能力。

<a id="id24"></a>

### Header File

- [bk\_dm\_bluetooth.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_bluetooth.h)

<a id="id25"></a>

### Functions

<a id="_CPPv423bk_bluetooth_get_statusv"></a>

<a id="_CPPv323bk_bluetooth_get_statusv"></a> <a id="_CPPv223bk_bluetooth_get_statusv"></a> <a id="bk_bluetooth_get_status__void"></a> <a id="group__dm__bluetooth_1gae17bb7b378bfff48332bb162d7066784"></a> [bk\_bluetooth\_status\_t](#_CPPv421bk_bluetooth_status_t "bk_bluetooth_status_t") bk\_bluetooth\_get\_status(void)
:   Get bluetooth status.

    返回
    :   Bluetooth status

<a id="_CPPv417bk_bluetooth_initv"></a>

<a id="_CPPv317bk_bluetooth_initv"></a> <a id="_CPPv217bk_bluetooth_initv"></a> <a id="bk_bluetooth_init__void"></a> <a id="group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2"></a> [bt\_err\_t](#_CPPv48bt_err_t "bt_err_t") bk\_bluetooth\_init(void)
:   init bluetooth.

    返回
    :   - BT\_OK: success
        - others: fail

<a id="_CPPv419bk_bluetooth_deinitv"></a>

<a id="_CPPv319bk_bluetooth_deinitv"></a> <a id="_CPPv219bk_bluetooth_deinitv"></a> <a id="bk_bluetooth_deinit__void"></a> <a id="group__dm__bluetooth_1ga78fcf706b6d4d50bba64407345d6023a"></a> [bt\_err\_t](#_CPPv48bt_err_t "bt_err_t") bk\_bluetooth\_deinit(void)
:   deinit bluetooth.

    返回
    :   - BT\_OK: success
        - others: fail

<a id="_CPPv424bk_bluetooth_get_addressP7uint8_t"></a>

<a id="_CPPv324bk_bluetooth_get_addressP7uint8_t"></a> <a id="_CPPv224bk_bluetooth_get_addressP7uint8_t"></a> <a id="bk_bluetooth_get_address__uint8_tP"></a> <a id="group__dm__bluetooth_1gaa3c50fd3ec11c2061671c4844fe893d6"></a> [bt\_err\_t](#_CPPv48bt_err_t "bt_err_t") bk\_bluetooth\_get\_address(uint8\_t \*addr)
:   Get bluetooth device address. Must use after “bk\_bluetooth\_init”.

    参数
    :   **addr** – **\[out\]** \- bluetooth device address

    返回
    :   - BT\_OK: success
        - others: fail

<a id="_CPPv434bk_dual_host_register_hci_callback17dual_hci_to_cp_cb"></a>

<a id="_CPPv334bk_dual_host_register_hci_callback17dual_hci_to_cp_cb"></a> <a id="_CPPv234bk_dual_host_register_hci_callback17dual_hci_to_cp_cb"></a> <a id="bk_dual_host_register_hci_callback__dual_hci_to_cp_cb"></a> <a id="group__dm__bluetooth_1ga60eff0ae89f12e8abe79ca47b947ac05"></a> [bt\_err\_t](#_CPPv48bt_err_t "bt_err_t") bk\_dual\_host\_register\_hci\_callback([dual\_hci\_to\_cp\_cb](#_CPPv417dual_hci_to_cp_cb "dual_hci_to_cp_cb") cb)
:   register hci callback for dual mode host only

    **Attention**
    :   used for dual mode host only

    参数
    :   **\-** – cb: hci callback function used to recv hci data from host

    返回
    :   - BT\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_dual_hci_send_to_hostP7uint8_t8uint32_t"></a>

<a id="_CPPv324bk_dual_hci_send_to_hostP7uint8_t8uint32_t"></a> <a id="_CPPv224bk_dual_hci_send_to_hostP7uint8_t8uint32_t"></a> <a id="bk_dual_hci_send_to_host__uint8_tP.uint32_t"></a> <a id="group__dm__bluetooth_1ga72c11fa9064dfee612cc87423941208d"></a> [bt\_err\_t](#_CPPv48bt_err_t "bt_err_t") bk\_dual\_hci\_send\_to\_host(uint8\_t \*buf, uint32\_t len)
:   send hci data to host.

    **Attention**
    :   used for dual mode host only

    参数
    :   **\-** – buf: payload

        - len: buf’s len

    返回
    :   - BT\_OK: succeed

<a id="_CPPv437bk_bluetooth_reg_secondary_controllerP33bk_bluetooth_secondary_callback_t"></a>

<a id="_CPPv337bk_bluetooth_reg_secondary_controllerP33bk_bluetooth_secondary_callback_t"></a> <a id="_CPPv237bk_bluetooth_reg_secondary_controllerP33bk_bluetooth_secondary_callback_t"></a> <a id="bk_bluetooth_reg_secondary_controller__bk_bluetooth_secondary_callback_tP"></a> <a id="group__dm__bluetooth_1gaa2f200ea377c52706b5f5ef2809f362e"></a> [bt\_err\_t](#_CPPv48bt_err_t "bt_err_t") bk\_bluetooth\_reg\_secondary\_controller([bk\_bluetooth\_secondary\_callback\_t](#_CPPv433bk_bluetooth_secondary_callback_t "bk_bluetooth_secondary_callback_t") \*cb)
:   reg secondary controller.

    **Attention**
    :   used for dual mode host only

    参数
    :   **\-** – cb: callback

    返回
    :   - BT\_OK: succeed

<a id="_CPPv420bk_bluetooth_h5_initP17bluetooth_h5_cb_t"></a>

<a id="_CPPv320bk_bluetooth_h5_initP17bluetooth_h5_cb_t"></a> <a id="_CPPv220bk_bluetooth_h5_initP17bluetooth_h5_cb_t"></a> <a id="bk_bluetooth_h5_init__bluetooth_h5_cb_tP"></a> <a id="group__dm__bluetooth_1ga5d02845801df2ca338d898c8d249d3ac"></a> int32\_t bk\_bluetooth\_h5\_init([bluetooth\_h5\_cb\_t](#_CPPv417bluetooth_h5_cb_t "bluetooth_h5_cb_t") \*cb)
:   init h5 module.

    **Attention**
    :   this module only encode/decode h5 package

    参数
    :   **\-** – cb: callback

    返回
    :   - BT\_OK: succeed

<a id="_CPPv422bk_bluetooth_h5_deinitv"></a>

<a id="_CPPv322bk_bluetooth_h5_deinitv"></a> <a id="_CPPv222bk_bluetooth_h5_deinitv"></a> <a id="bk_bluetooth_h5_deinit__void"></a> <a id="group__dm__bluetooth_1ga8f6e79898eb32ffc2d2104bc8b212ed4"></a> int32\_t bk\_bluetooth\_h5\_deinit(void)
:   deinit h5 module.

    **Attention**
    :   this module only encode/decode h5 package

    返回
    :   - BT\_OK: succeed

<a id="_CPPv429bk_bluetooth_h5_set_h5_enable7uint8_t"></a>

<a id="_CPPv329bk_bluetooth_h5_set_h5_enable7uint8_t"></a> <a id="_CPPv229bk_bluetooth_h5_set_h5_enable7uint8_t"></a> <a id="bk_bluetooth_h5_set_h5_enable__uint8_t"></a> <a id="group__dm__bluetooth_1ga9318de5f9c1989ec97275518d5d36263"></a> int32\_t bk\_bluetooth\_h5\_set\_h5\_enable(uint8\_t enable)
:   enable h5 module.

    参数
    :   **\-** – enable: enable or disable

    返回
    :   - BT\_OK: succeed

<a id="_CPPv429bk_bluetooth_h5_get_h5_enablev"></a>

<a id="_CPPv329bk_bluetooth_h5_get_h5_enablev"></a> <a id="_CPPv229bk_bluetooth_h5_get_h5_enablev"></a> <a id="bk_bluetooth_h5_get_h5_enable__void"></a> <a id="group__dm__bluetooth_1ga19f99e9bcd0c020b2dee4479fecc7b34"></a> uint8\_t bk\_bluetooth\_h5\_get\_h5\_enable(void)
:   get module enable status.

    返回
    :   - BT\_OK: succeed

<a id="_CPPv420bk_bluetooth_h5_sendPK7uint8_t7uint8_t8uint16_t"></a>

<a id="_CPPv320bk_bluetooth_h5_sendPK7uint8_t7uint8_t8uint16_t"></a> <a id="_CPPv220bk_bluetooth_h5_sendPK7uint8_t7uint8_t8uint16_t"></a> <a id="bk_bluetooth_h5_send__uint8_tCP.uint8_t.uint16_t"></a> <a id="group__dm__bluetooth_1ga74ad64e08eab625458c81b814df89478"></a> int8\_t bk\_bluetooth\_h5\_send(const uint8\_t \*payload, uint8\_t type, uint16\_t len)
:   encode h4 data to h5 and send.

    **Attention**
    :   when encode completed, bluetooth\_h5\_cb\_t-\>encode\_data\_cb will be called.

    参数
    :   **\-** – payload: hci data payload

        - type: cmd/evt/acl/sco/iso
        - len: payload len

    返回
    :   - BT\_OK: succeed

<a id="_CPPv425bk_bluetooth_h5_recv_dataP7uint8_t8uint32_t"></a>

<a id="_CPPv325bk_bluetooth_h5_recv_dataP7uint8_t8uint32_t"></a> <a id="_CPPv225bk_bluetooth_h5_recv_dataP7uint8_t8uint32_t"></a> <a id="bk_bluetooth_h5_recv_data__uint8_tP.uint32_t"></a> <a id="group__dm__bluetooth_1ga97eb5e58cc164dfb4e36e70ced836b04"></a> int32\_t bk\_bluetooth\_h5\_recv\_data(uint8\_t \*data, uint32\_t count)
:   decode h5 data.

    **Attention**
    :   when decode completed, bluetooth\_h5\_cb\_t-\>decode\_data\_ext\_cb will be called.

    参数
    :   **\-** – payload: h5 data payload

        - count: data len

    返回
    :   - BT\_OK: succeed

<a id="_CPPv429bk_bluetooth_h5_send_sync_req7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv329bk_bluetooth_h5_send_sync_req7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv229bk_bluetooth_h5_send_sync_req7uint8_t7uint8_t7uint8_t"></a> <a id="bk_bluetooth_h5_send_sync_req__uint8_t.uint8_t.uint8_t"></a> <a id="group__dm__bluetooth_1gafae44ff15b546e01a8a9b1929dd5ad87"></a> int8\_t bk\_bluetooth\_h5\_send\_sync\_req(uint8\_t win\_size, uint8\_t fc, uint8\_t dic)
:   send h5 sync/config to peer.

    **Attention**
    :   when recv nego completed from peer, bluetooth\_h5\_cb\_t-\>notify\_h5\_nego\_completed will be called.

    参数
    :   **\-** – win\_size: win size

        - fc: flow control, no need to set
        - dic: if enable crc check

    返回
    :   - BT\_OK: succeed

<a id="_CPPv428bk_bluetooth_h5_check_retranv"></a>

<a id="_CPPv328bk_bluetooth_h5_check_retranv"></a> <a id="_CPPv228bk_bluetooth_h5_check_retranv"></a> <a id="bk_bluetooth_h5_check_retran__void"></a> <a id="group__dm__bluetooth_1ga363c929717b889a2ee858e0dafe10a0d"></a> int32\_t bk\_bluetooth\_h5\_check\_retran(void)
:   check if have unack packaged in h5 queue.

    **Attention**
    :   This function must be called in bluetooth\_h5\_cb\_t-\>notify\_tx\_ack\_tout\_cb context.

    返回
    :   - BT\_OK: succeed

<a id="bk-dm-bluetooth-types-h"></a>

## bk\_dm\_bluetooth\_types.h

`bk_dm_bluetooth_types.h` 定义 Bluetooth 通用 API 使用的基础类型。

<a id="id26"></a>

### Header File

- [bk\_dm\_bluetooth\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_bluetooth_types.h)

<a id="id27"></a>

### Structures

<a id="_CPPv414bt_cmd_param_t"></a>

<a id="_CPPv314bt_cmd_param_t"></a> <a id="_CPPv214bt_cmd_param_t"></a> <a id="bt_cmd_param_t"></a> <a id="structbt__cmd__param__t"></a> struct bt\_cmd\_param\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14bt_cmd_param_t7cmd_idxE"></a>

    <a id="_CPPv3N14bt_cmd_param_t7cmd_idxE"></a> <a id="_CPPv2N14bt_cmd_param_t7cmd_idxE"></a> <a id="bt_cmd_param_t::cmd_idx__uint8_t"></a> <a id="group__bk__bt__api__v1__typedef_1ga945b7e75fc9ee6b83269815c8139377e"></a> uint8\_t cmd\_idx
    :   actv\_idx

    <a id="_CPPv4N14bt_cmd_param_t6statusE"></a>

    <a id="_CPPv3N14bt_cmd_param_t6statusE"></a> <a id="_CPPv2N14bt_cmd_param_t6statusE"></a> <a id="bt_cmd_param_t::status__bt_err_t"></a> <a id="group__bk__bt__api__v1__typedef_1ga9c83ef62b7c7ad3f3ffa6126fab94dd1"></a> [bt\_err\_t](#_CPPv48bt_err_t "bt_err_t") status
    :   The status for this command

<a id="_CPPv412bk_bt_uuid_t"></a>

<a id="_CPPv312bk_bt_uuid_t"></a> <a id="_CPPv212bk_bt_uuid_t"></a> <a id="bk_bt_uuid_t"></a> <a id="structbk__bt__uuid__t"></a> struct bk\_bt\_uuid\_t
:   UUID type.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12bk_bt_uuid_t3lenE"></a>

    <a id="_CPPv3N12bk_bt_uuid_t3lenE"></a> <a id="_CPPv2N12bk_bt_uuid_t3lenE"></a> <a id="bk_bt_uuid_t::len__uint16_t"></a> <a id="group__bk__bt__api__v1__typedef_1ga246cd5cd10fee76e24d1a3f3e3c378af"></a> uint16\_t len
    :   UUID length, 16bit, 32bit or 128bit

    <a id="_CPPv4N12bk_bt_uuid_t6uuid16E"></a>

    <a id="_CPPv3N12bk_bt_uuid_t6uuid16E"></a> <a id="_CPPv2N12bk_bt_uuid_t6uuid16E"></a> <a id="bk_bt_uuid_t::uuid16__uint16_t"></a> <a id="group__bk__bt__api__v1__typedef_1ga9fa57ffe70e8e7ac666f607876012227"></a> uint16\_t uuid16
    :   16bit UUID

    <a id="_CPPv4N12bk_bt_uuid_t6uuid32E"></a>

    <a id="_CPPv3N12bk_bt_uuid_t6uuid32E"></a> <a id="_CPPv2N12bk_bt_uuid_t6uuid32E"></a> <a id="bk_bt_uuid_t::uuid32__uint32_t"></a> <a id="group__bk__bt__api__v1__typedef_1ga0b37353b17975e53ec0471c485953cf2"></a> uint32\_t uuid32
    :   32bit UUID

    <a id="_CPPv4N12bk_bt_uuid_t7uuid128E"></a>

    <a id="_CPPv3N12bk_bt_uuid_t7uuid128E"></a> <a id="_CPPv2N12bk_bt_uuid_t7uuid128E"></a> <a id="bk_bt_uuid_t::uuid128__uint8_tA"></a> <a id="group__bk__bt__api__v1__typedef_1ga9af601d88a198c716d103ddec931acdb"></a> uint8\_t uuid128\[BK\_UUID\_LEN\_128\]
    :   128bit UUID

    <a id="_CPPv4N12bk_bt_uuid_t4uuidE"></a>

    <a id="_CPPv3N12bk_bt_uuid_t4uuidE"></a> <a id="_CPPv2N12bk_bt_uuid_t4uuidE"></a> <a id="group__bk__bt__api__v1__typedef_1ga4b1429fa306aea9526107772bba4d758"></a> union [bk\_bt\_uuid\_t](#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t")::\[anonymous\] uuid
    :   UUID

<a id="_CPPv433bk_bluetooth_secondary_callback_t"></a>

<a id="_CPPv333bk_bluetooth_secondary_callback_t"></a> <a id="_CPPv233bk_bluetooth_secondary_callback_t"></a> <a id="bk_bluetooth_secondary_callback_t"></a> <a id="structbk__bluetooth__secondary__callback__t"></a> struct bk\_bluetooth\_secondary\_callback\_t

<a id="_CPPv417bluetooth_h5_cb_t"></a>

<a id="_CPPv317bluetooth_h5_cb_t"></a> <a id="_CPPv217bluetooth_h5_cb_t"></a> <a id="bluetooth_h5_cb_t"></a> <a id="structbluetooth__h5__cb__t"></a> struct bluetooth\_h5\_cb\_t

<a id="id28"></a>

### Macros

<a id="c.BK_BT_ADDR_LEN"></a>

<a id="bk__dm__bluetooth__types_8h_1ad42ccd4239e1654bc6ae217626cfb77e"></a> BK\_BT\_ADDR\_LEN

<a id="c.BK_BT_STREAM_TO_UINT8"></a>

<a id="bk__dm__bluetooth__types_8h_1a530610003929dcc690d70dd5d9392bbc"></a> BK\_BT\_STREAM\_TO\_UINT8(u8, p)

<a id="c.BK_BT_STREAM_TO_UINT16"></a>

<a id="bk__dm__bluetooth__types_8h_1a46f173048ebc1f6947eb5e776e11370a"></a> BK\_BT\_STREAM\_TO\_UINT16(u16, p)

<a id="c.BK_BT_STREAM_TO_UINT24"></a>

<a id="bk__dm__bluetooth__types_8h_1a79a13656296bbb87bf865d2ae8b4cb8d"></a> BK\_BT\_STREAM\_TO\_UINT24(u24, p)

<a id="c.BK_BT_STREAM_TO_UINT32"></a>

<a id="bk__dm__bluetooth__types_8h_1a5fdbabf08bf949313dd0205be14c2ba5"></a> BK\_BT\_STREAM\_TO\_UINT32(u32, p)

<a id="c.BK_ERR_BT_SUCCESS"></a>

<a id="bk__dm__bluetooth__types_8h_1abfab26e6ae490aa53d96c5490820798f"></a> BK\_ERR\_BT\_SUCCESS
:   success

<a id="c.BK_ERR_BT_FAIL"></a>

<a id="bk__dm__bluetooth__types_8h_1a5e0e2db0d961a428f4043333a6eed865"></a> BK\_ERR\_BT\_FAIL
:   fail

<a id="c.BK_ERR_BT_NO_MEM"></a>

<a id="bk__dm__bluetooth__types_8h_1a3313377033aaa2c043febccb6d97065c"></a> BK\_ERR\_BT\_NO\_MEM
:   no mem

<a id="c.BK_ERR_BT_PROFILE"></a>

<a id="bk__dm__bluetooth__types_8h_1a49d0c551c53d630dbe0f9116e8a63333"></a> BK\_ERR\_BT\_PROFILE
:   profile err

<a id="c.BK_ERR_BT_CMD_NOT_SUPPORT"></a>

<a id="bk__dm__bluetooth__types_8h_1ac7408f077b4cb9d9e6e46ad661039e05"></a> BK\_ERR\_BT\_CMD\_NOT\_SUPPORT
:   unknow cmd err

<a id="c.BK_ERR_BT_UNKNOW_IDX"></a>

<a id="bk__dm__bluetooth__types_8h_1ada2f080fa6fadc64cfae88f9f101c717"></a> BK\_ERR\_BT\_UNKNOW\_IDX
:   index err, suchas conn\_ind

<a id="c.BK_ERR_BT_BT_STATUS"></a>

<a id="bk__dm__bluetooth__types_8h_1a6c692856cc5d5da94f9c9acbc6fd8e9a"></a> BK\_ERR\_BT\_BT\_STATUS
:   ble status not match

<a id="c.BK_ERR_BT_CMD_RUN"></a>

<a id="bk__dm__bluetooth__types_8h_1a980707fe33bba73b71c3e1d16be5c76c"></a> BK\_ERR\_BT\_CMD\_RUN
:   cmd run err

<a id="c.BK_ERR_BT_INIT_CREATE"></a>

<a id="bk__dm__bluetooth__types_8h_1a1baac8d13586079b2bdc60342a7e0195"></a> BK\_ERR\_BT\_INIT\_CREATE
:   create init err, such as bk\_ble\_create\_init

<a id="c.BK_ERR_BT_INIT_STATE"></a>

<a id="bk__dm__bluetooth__types_8h_1a9cd4bf56c8c5ee25ae142cf12c630680"></a> BK\_ERR\_BT\_INIT\_STATE
:   current init status not match

<a id="c.BT_OK"></a>

<a id="bk__dm__bluetooth__types_8h_1aa390f78789688bbd5276dfee3ae08f0c"></a> BT\_OK
:   success

<a id="c.BT_FAIL"></a>

<a id="bk__dm__bluetooth__types_8h_1abf9a91fd65f8eb15ac3ea5eae4a7ef48"></a> BT\_FAIL
:   failure

<a id="c.BT_INTERFACE_NOT_SUPPORT"></a>

<a id="bk__dm__bluetooth__types_8h_1ad2faa220a250bb609b07ea406d4801c1"></a> BT\_INTERFACE\_NOT\_SUPPORT
:   interface not support

<a id="c.BK_BT_OCTET16_LEN"></a>

<a id="group__bk__bt__api__v1__typedef_1gac374443b7bd51c88d0f3b60cfde192d0"></a> BK\_BT\_OCTET16\_LEN

<a id="c.BK_BT_OCTET8_LEN"></a>

<a id="group__bk__bt__api__v1__typedef_1gaacaa5a4e917466b09ef05a5fd0d77341"></a> BK\_BT\_OCTET8\_LEN

<a id="c.BK_UUID_LEN_16"></a>

<a id="group__bk__bt__api__v1__typedef_1gaf761f9f27c23c501cb76a1af503a8abf"></a> BK\_UUID\_LEN\_16

<a id="c.BK_UUID_LEN_32"></a>

<a id="group__bk__bt__api__v1__typedef_1ga84dd8f82ddcc90eb29565c0be52949f9"></a> BK\_UUID\_LEN\_32

<a id="c.BK_UUID_LEN_128"></a>

<a id="group__bk__bt__api__v1__typedef_1gad3166f86111d34381f4f33a682bfae52"></a> BK\_UUID\_LEN\_128

<a id="c.BK_BD_ADDR_LEN"></a>

<a id="group__bk__bt__api__v1__typedef_1gadeccfbdebfbf06af931a9f41de53177f"></a> BK\_BD\_ADDR\_LEN
:   Bluetooth address length.

<a id="id29"></a>

### Type Definitions

<a id="_CPPv48bt_err_t"></a>

<a id="_CPPv38bt_err_t"></a> <a id="_CPPv28bt_err_t"></a> <a id="bt_err_t"></a> <a id="bk__dm__bluetooth__types_8h_1a5a4557426c7e758c6f6eeec2a07884e9"></a> typedef int bt\_err\_t

<a id="_CPPv415bk_bt_octet16_t"></a>

<a id="_CPPv315bk_bt_octet16_t"></a> <a id="_CPPv215bk_bt_octet16_t"></a> <a id="bk_bt_octet16_t"></a> <a id="group__bk__bt__api__v1__typedef_1ga9f0988d5df1f310cce284c9a7f3479ba"></a> typedef uint8\_t bk\_bt\_octet16\_t\[BK\_BT\_OCTET16\_LEN\]

<a id="_CPPv414bk_bt_octet8_t"></a>

<a id="_CPPv314bk_bt_octet8_t"></a> <a id="_CPPv214bk_bt_octet8_t"></a> <a id="bk_bt_octet8_t"></a> <a id="group__bk__bt__api__v1__typedef_1gab1356f64f3567db6f846eb94affa8b86"></a> typedef uint8\_t bk\_bt\_octet8\_t\[BK\_BT\_OCTET8\_LEN\]

<a id="_CPPv413bk_link_key_t"></a>

<a id="_CPPv313bk_link_key_t"></a> <a id="_CPPv213bk_link_key_t"></a> <a id="bk_link_key_t"></a> <a id="group__bk__bt__api__v1__typedef_1ga41a7a2ea1698c5e46b21d6b8ab2c305f"></a> typedef uint8\_t bk\_link\_key\_t\[BK\_BT\_OCTET16\_LEN\]

<a id="_CPPv412bk_bd_addr_t"></a>

<a id="_CPPv312bk_bd_addr_t"></a> <a id="_CPPv212bk_bd_addr_t"></a> <a id="bk_bd_addr_t"></a> <a id="group__bk__bt__api__v1__typedef_1ga28a1a4ccff0c06cad5e9e8689cabb740"></a> typedef uint8\_t bk\_bd\_addr\_t\[BK\_BD\_ADDR\_LEN\]
:   Bluetooth device address.

<a id="_CPPv411bt_cmd_cb_t"></a>

<a id="_CPPv311bt_cmd_cb_t"></a> <a id="_CPPv211bt_cmd_cb_t"></a> <a id="bt_cmd_cb_t"></a> <a id="group__bk__bt__api__v1__typedef_1ga598538e157ef488585cccafa95e906bd"></a> typedef void (\*bt\_cmd\_cb\_t)([bt\_cmd\_t](#_CPPv48bt_cmd_t "bt_cmd_t") cmd, [bt\_cmd\_param\_t](#_CPPv414bt_cmd_param_t "bt_cmd_param_t") \*param)
:   for sync bt api call return

    most bt api have bt\_cmd\_cb\_t param, you must wait is callback.

    Param \-
    :   cmd: cmd id.

        - param: param

<a id="_CPPv417dual_hci_to_cp_cb"></a>

<a id="_CPPv317dual_hci_to_cp_cb"></a> <a id="_CPPv217dual_hci_to_cp_cb"></a> <a id="dual_hci_to_cp_cb"></a> <a id="group__bk__bt__api__v1__typedef_1ga9822acabb10959132ee5ca7303686735"></a> typedef [bt\_err\_t](#_CPPv48bt_err_t "bt_err_t") (\*dual\_hci\_to\_cp\_cb)(uint8\_t type, uint8\_t \*buf, uint16\_t len)

<a id="id30"></a>

### Enumerations

<a id="_CPPv421bk_bluetooth_status_t"></a>

<a id="_CPPv321bk_bluetooth_status_t"></a> <a id="_CPPv221bk_bluetooth_status_t"></a> <a id="bk__dm__bluetooth__types_8h_1ae1b59227f427ab1ab30c3eb930230a0a"></a> enum bk\_bluetooth\_status\_t
:   Bluetooth status type, to indicate whether the bluetooth is ready.

    *Values:*

    <a id="_CPPv4N21bk_bluetooth_status_t33BK_BLUETOOTH_STATUS_UNINITIALIZEDE"></a>

    <a id="_CPPv3N21bk_bluetooth_status_t33BK_BLUETOOTH_STATUS_UNINITIALIZEDE"></a> <a id="_CPPv2N21bk_bluetooth_status_t33BK_BLUETOOTH_STATUS_UNINITIALIZEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gae1b59227f427ab1ab30c3eb930230a0aa4383d79dee95f78d2bd7deaf39376399"></a> enumerator BK\_BLUETOOTH\_STATUS\_UNINITIALIZED
    :   Bluetooth not initialized

    <a id="_CPPv4N21bk_bluetooth_status_t27BK_BLUETOOTH_STATUS_ENABLEDE"></a>

    <a id="_CPPv3N21bk_bluetooth_status_t27BK_BLUETOOTH_STATUS_ENABLEDE"></a> <a id="_CPPv2N21bk_bluetooth_status_t27BK_BLUETOOTH_STATUS_ENABLEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gae1b59227f427ab1ab30c3eb930230a0aa4442c1f823ab0e321243aa5516661e1e"></a> enumerator BK\_BLUETOOTH\_STATUS\_ENABLED
    :   Bluetooth initialized and enabled

<a id="_CPPv427BK_BT_CONTROLLER_STACK_TYPE"></a>

<a id="_CPPv327BK_BT_CONTROLLER_STACK_TYPE"></a> <a id="_CPPv227BK_BT_CONTROLLER_STACK_TYPE"></a> <a id="bk__dm__bluetooth__types_8h_1a7e4d6560c8e4c48bdf7f1fb1986e729a"></a> enum BK\_BT\_CONTROLLER\_STACK\_TYPE
:   *Values:*

    <a id="_CPPv4N27BK_BT_CONTROLLER_STACK_TYPE36BK_BT_CONTROLLER_STACK_TYPE_BTDM_5_2E"></a>

    <a id="_CPPv3N27BK_BT_CONTROLLER_STACK_TYPE36BK_BT_CONTROLLER_STACK_TYPE_BTDM_5_2E"></a> <a id="_CPPv2N27BK_BT_CONTROLLER_STACK_TYPE36BK_BT_CONTROLLER_STACK_TYPE_BTDM_5_2E"></a> <a id="bk__dm__bluetooth__types_8h_1ga7e4d6560c8e4c48bdf7f1fb1986e729aac51ad630b33fe5caa857f3c4c398e277"></a> enumerator BK\_BT\_CONTROLLER\_STACK\_TYPE\_BTDM\_5\_2

    <a id="_CPPv4N27BK_BT_CONTROLLER_STACK_TYPE34BK_BT_CONTROLLER_STACK_NOT_SUPPORTE"></a>

    <a id="_CPPv3N27BK_BT_CONTROLLER_STACK_TYPE34BK_BT_CONTROLLER_STACK_NOT_SUPPORTE"></a> <a id="_CPPv2N27BK_BT_CONTROLLER_STACK_TYPE34BK_BT_CONTROLLER_STACK_NOT_SUPPORTE"></a> <a id="bk__dm__bluetooth__types_8h_1ga7e4d6560c8e4c48bdf7f1fb1986e729aa539554a3a2ce19081e53234a83fa44f2"></a> enumerator BK\_BT\_CONTROLLER\_STACK\_NOT\_SUPPORT

<a id="_CPPv421BK_BT_HOST_STACK_TYPE"></a>

<a id="_CPPv321BK_BT_HOST_STACK_TYPE"></a> <a id="_CPPv221BK_BT_HOST_STACK_TYPE"></a> <a id="bk__dm__bluetooth__types_8h_1a2d92d490b1809fdbcea27bb631136a90"></a> enum BK\_BT\_HOST\_STACK\_TYPE
:   *Values:*

    <a id="_CPPv4N21BK_BT_HOST_STACK_TYPE31BK_BT_HOST_STACK_TYPE_ETHERMINDE"></a>

    <a id="_CPPv3N21BK_BT_HOST_STACK_TYPE31BK_BT_HOST_STACK_TYPE_ETHERMINDE"></a> <a id="_CPPv2N21BK_BT_HOST_STACK_TYPE31BK_BT_HOST_STACK_TYPE_ETHERMINDE"></a> <a id="bk__dm__bluetooth__types_8h_1ga2d92d490b1809fdbcea27bb631136a90a7a08c3324e2cb9fe088bf20d9154e40f"></a> enumerator BK\_BT\_HOST\_STACK\_TYPE\_ETHERMIND

    <a id="_CPPv4N21BK_BT_HOST_STACK_TYPE33BK_BT_HOST_STACK_TYPE_NOT_SUPPORTE"></a>

    <a id="_CPPv3N21BK_BT_HOST_STACK_TYPE33BK_BT_HOST_STACK_TYPE_NOT_SUPPORTE"></a> <a id="_CPPv2N21BK_BT_HOST_STACK_TYPE33BK_BT_HOST_STACK_TYPE_NOT_SUPPORTE"></a> <a id="bk__dm__bluetooth__types_8h_1ga2d92d490b1809fdbcea27bb631136a90afc540d45976a3be35a458b22ccfd251b"></a> enumerator BK\_BT\_HOST\_STACK\_TYPE\_NOT\_SUPPORT

<a id="_CPPv414bk_bt_status_t"></a>

<a id="_CPPv314bk_bt_status_t"></a> <a id="_CPPv214bk_bt_status_t"></a> <a id="bk__dm__bluetooth__types_8h_1afdf5079d9baee5818018b058ca2c443a"></a> enum bk\_bt\_status\_t
:   Status Return Value.

    *Values:*

    <a id="_CPPv4N14bk_bt_status_t20BK_BT_STATUS_SUCCESSE"></a>

    <a id="_CPPv3N14bk_bt_status_t20BK_BT_STATUS_SUCCESSE"></a> <a id="_CPPv2N14bk_bt_status_t20BK_BT_STATUS_SUCCESSE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aab93fcc8c7ee6db85f1861c736df53715"></a> enumerator BK\_BT\_STATUS\_SUCCESS

    <a id="_CPPv4N14bk_bt_status_t32BK_BT_STATUS_UNKNOWN_HCI_COMMANDE"></a>

    <a id="_CPPv3N14bk_bt_status_t32BK_BT_STATUS_UNKNOWN_HCI_COMMANDE"></a> <a id="_CPPv2N14bk_bt_status_t32BK_BT_STATUS_UNKNOWN_HCI_COMMANDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aada896863209e261da3ce7112551208bb"></a> enumerator BK\_BT\_STATUS\_UNKNOWN\_HCI\_COMMAND

    <a id="_CPPv4N14bk_bt_status_t34BK_BT_STATUS_UNKNOWN_CONNECTION_IDE"></a>

    <a id="_CPPv3N14bk_bt_status_t34BK_BT_STATUS_UNKNOWN_CONNECTION_IDE"></a> <a id="_CPPv2N14bk_bt_status_t34BK_BT_STATUS_UNKNOWN_CONNECTION_IDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aade469b18cd7e20f930611b914cda37ed"></a> enumerator BK\_BT\_STATUS\_UNKNOWN\_CONNECTION\_ID

    <a id="_CPPv4N14bk_bt_status_t29BK_BT_STATUS_HARDWARE_FAILUREE"></a>

    <a id="_CPPv3N14bk_bt_status_t29BK_BT_STATUS_HARDWARE_FAILUREE"></a> <a id="_CPPv2N14bk_bt_status_t29BK_BT_STATUS_HARDWARE_FAILUREE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aae69c7006fe6bbf964ec5687d289a875a"></a> enumerator BK\_BT\_STATUS\_HARDWARE\_FAILURE

    <a id="_CPPv4N14bk_bt_status_t25BK_BT_STATUS_PAGE_TIMEOUTE"></a>

    <a id="_CPPv3N14bk_bt_status_t25BK_BT_STATUS_PAGE_TIMEOUTE"></a> <a id="_CPPv2N14bk_bt_status_t25BK_BT_STATUS_PAGE_TIMEOUTE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aaeca70ef51b3512575e64a5c9c40ba1c3"></a> enumerator BK\_BT\_STATUS\_PAGE\_TIMEOUT

    <a id="_CPPv4N14bk_bt_status_t25BK_BT_STATUS_AUTH_FAILUREE"></a>

    <a id="_CPPv3N14bk_bt_status_t25BK_BT_STATUS_AUTH_FAILUREE"></a> <a id="_CPPv2N14bk_bt_status_t25BK_BT_STATUS_AUTH_FAILUREE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aaa71012cb045c8f63addec87e204bd6fa"></a> enumerator BK\_BT\_STATUS\_AUTH\_FAILURE

    <a id="_CPPv4N14bk_bt_status_t24BK_BT_STATUS_PIN_MISSINGE"></a>

    <a id="_CPPv3N14bk_bt_status_t24BK_BT_STATUS_PIN_MISSINGE"></a> <a id="_CPPv2N14bk_bt_status_t24BK_BT_STATUS_PIN_MISSINGE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aac43d079446281c711de7794736d74673"></a> enumerator BK\_BT\_STATUS\_PIN\_MISSING

    <a id="_CPPv4N14bk_bt_status_t31BK_BT_STATUS_MEMORY_CAPA_EXCEEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t31BK_BT_STATUS_MEMORY_CAPA_EXCEEDE"></a> <a id="_CPPv2N14bk_bt_status_t31BK_BT_STATUS_MEMORY_CAPA_EXCEEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aaec231d782347b849eb1f9bdf8513de58"></a> enumerator BK\_BT\_STATUS\_MEMORY\_CAPA\_EXCEED

    <a id="_CPPv4N14bk_bt_status_t24BK_BT_STATUS_CON_TIMEOUTE"></a>

    <a id="_CPPv3N14bk_bt_status_t24BK_BT_STATUS_CON_TIMEOUTE"></a> <a id="_CPPv2N14bk_bt_status_t24BK_BT_STATUS_CON_TIMEOUTE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa6e51f5bce4b4669432f88238fe513329"></a> enumerator BK\_BT\_STATUS\_CON\_TIMEOUT

    <a id="_CPPv4N14bk_bt_status_t29BK_BT_STATUS_CON_LIMIT_EXCEEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t29BK_BT_STATUS_CON_LIMIT_EXCEEDE"></a> <a id="_CPPv2N14bk_bt_status_t29BK_BT_STATUS_CON_LIMIT_EXCEEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa625a7802ece4469e1af0747007fe06ca"></a> enumerator BK\_BT\_STATUS\_CON\_LIMIT\_EXCEED

    <a id="_CPPv4N14bk_bt_status_t38BK_BT_STATUS_SYNC_CON_LIMIT_DEV_EXCEEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t38BK_BT_STATUS_SYNC_CON_LIMIT_DEV_EXCEEDE"></a> <a id="_CPPv2N14bk_bt_status_t38BK_BT_STATUS_SYNC_CON_LIMIT_DEV_EXCEEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa9b61ba58d5fba1ae7f9869efb4caee80"></a> enumerator BK\_BT\_STATUS\_SYNC\_CON\_LIMIT\_DEV\_EXCEED

    <a id="_CPPv4N14bk_bt_status_t31BK_BT_STATUS_CON_ALREADY_EXISTSE"></a>

    <a id="_CPPv3N14bk_bt_status_t31BK_BT_STATUS_CON_ALREADY_EXISTSE"></a> <a id="_CPPv2N14bk_bt_status_t31BK_BT_STATUS_CON_ALREADY_EXISTSE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aada60c8595d80c3fb1b15e19602428fd6"></a> enumerator BK\_BT\_STATUS\_CON\_ALREADY\_EXISTS

    <a id="_CPPv4N14bk_bt_status_t31BK_BT_STATUS_COMMAND_DISALLOWEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t31BK_BT_STATUS_COMMAND_DISALLOWEDE"></a> <a id="_CPPv2N14bk_bt_status_t31BK_BT_STATUS_COMMAND_DISALLOWEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aab45fcc108c3ebb1025729ca66e5a9699"></a> enumerator BK\_BT\_STATUS\_COMMAND\_DISALLOWED

    <a id="_CPPv4N14bk_bt_status_t39BK_BT_STATUS_CONN_REJ_LIMITED_RESOURCESE"></a>

    <a id="_CPPv3N14bk_bt_status_t39BK_BT_STATUS_CONN_REJ_LIMITED_RESOURCESE"></a> <a id="_CPPv2N14bk_bt_status_t39BK_BT_STATUS_CONN_REJ_LIMITED_RESOURCESE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aaa1e5a11ec176a4490c9f9c87d9867580"></a> enumerator BK\_BT\_STATUS\_CONN\_REJ\_LIMITED\_RESOURCES

    <a id="_CPPv4N14bk_bt_status_t38BK_BT_STATUS_CONN_REJ_SECURITY_REASONSE"></a>

    <a id="_CPPv3N14bk_bt_status_t38BK_BT_STATUS_CONN_REJ_SECURITY_REASONSE"></a> <a id="_CPPv2N14bk_bt_status_t38BK_BT_STATUS_CONN_REJ_SECURITY_REASONSE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa7a9654e3981f159c74b2b3ef6a56b1fc"></a> enumerator BK\_BT\_STATUS\_CONN\_REJ\_SECURITY\_REASONS

    <a id="_CPPv4N14bk_bt_status_t41BK_BT_STATUS_CONN_REJ_UNACCEPTABLE_BDADDRE"></a>

    <a id="_CPPv3N14bk_bt_status_t41BK_BT_STATUS_CONN_REJ_UNACCEPTABLE_BDADDRE"></a> <a id="_CPPv2N14bk_bt_status_t41BK_BT_STATUS_CONN_REJ_UNACCEPTABLE_BDADDRE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa87b64f934ba49a6f42dd65a2f2022bc0"></a> enumerator BK\_BT\_STATUS\_CONN\_REJ\_UNACCEPTABLE\_BDADDR

    <a id="_CPPv4N14bk_bt_status_t39BK_BT_STATUS_CONN_ACCEPT_TIMEOUT_EXCEEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t39BK_BT_STATUS_CONN_ACCEPT_TIMEOUT_EXCEEDE"></a> <a id="_CPPv2N14bk_bt_status_t39BK_BT_STATUS_CONN_ACCEPT_TIMEOUT_EXCEEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa441812137034eb02bbaa5c7d913890df"></a> enumerator BK\_BT\_STATUS\_CONN\_ACCEPT\_TIMEOUT\_EXCEED

    <a id="_CPPv4N14bk_bt_status_t24BK_BT_STATUS_UNSUPPORTEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t24BK_BT_STATUS_UNSUPPORTEDE"></a> <a id="_CPPv2N14bk_bt_status_t24BK_BT_STATUS_UNSUPPORTEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa3e8f6136534ea417217956c3ded764da"></a> enumerator BK\_BT\_STATUS\_UNSUPPORTED

    <a id="_CPPv4N14bk_bt_status_t30BK_BT_STATUS_INVALID_HCI_PARAME"></a>

    <a id="_CPPv3N14bk_bt_status_t30BK_BT_STATUS_INVALID_HCI_PARAME"></a> <a id="_CPPv2N14bk_bt_status_t30BK_BT_STATUS_INVALID_HCI_PARAME"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa3285860b006acb7f0a24cbf135850fb2"></a> enumerator BK\_BT\_STATUS\_INVALID\_HCI\_PARAM

    <a id="_CPPv4N14bk_bt_status_t33BK_BT_STATUS_REMOTE_USER_TERM_CONE"></a>

    <a id="_CPPv3N14bk_bt_status_t33BK_BT_STATUS_REMOTE_USER_TERM_CONE"></a> <a id="_CPPv2N14bk_bt_status_t33BK_BT_STATUS_REMOTE_USER_TERM_CONE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aafc2f5bb1ca087e6d84c1a21d14d4e229"></a> enumerator BK\_BT\_STATUS\_REMOTE\_USER\_TERM\_CON

    <a id="_CPPv4N14bk_bt_status_t42BK_BT_STATUS_REMOTE_DEV_TERM_LOW_RESOURCESE"></a>

    <a id="_CPPv3N14bk_bt_status_t42BK_BT_STATUS_REMOTE_DEV_TERM_LOW_RESOURCESE"></a> <a id="_CPPv2N14bk_bt_status_t42BK_BT_STATUS_REMOTE_DEV_TERM_LOW_RESOURCESE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa7a0ca73f752dbdf81e061ff9ae18515c"></a> enumerator BK\_BT\_STATUS\_REMOTE\_DEV\_TERM\_LOW\_RESOURCES

    <a id="_CPPv4N14bk_bt_status_t33BK_BT_STATUS_REMOTE_DEV_POWER_OFFE"></a>

    <a id="_CPPv3N14bk_bt_status_t33BK_BT_STATUS_REMOTE_DEV_POWER_OFFE"></a> <a id="_CPPv2N14bk_bt_status_t33BK_BT_STATUS_REMOTE_DEV_POWER_OFFE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa4c5abada34417573ed4abc3981e640d5"></a> enumerator BK\_BT\_STATUS\_REMOTE\_DEV\_POWER\_OFF

    <a id="_CPPv4N14bk_bt_status_t35BK_BT_STATUS_CON_TERM_BY_LOCAL_HOSTE"></a>

    <a id="_CPPv3N14bk_bt_status_t35BK_BT_STATUS_CON_TERM_BY_LOCAL_HOSTE"></a> <a id="_CPPv2N14bk_bt_status_t35BK_BT_STATUS_CON_TERM_BY_LOCAL_HOSTE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa308a1caadde11c6baa7af0a32dd6ceb4"></a> enumerator BK\_BT\_STATUS\_CON\_TERM\_BY\_LOCAL\_HOST

    <a id="_CPPv4N14bk_bt_status_t30BK_BT_STATUS_REPEATED_ATTEMPTSE"></a>

    <a id="_CPPv3N14bk_bt_status_t30BK_BT_STATUS_REPEATED_ATTEMPTSE"></a> <a id="_CPPv2N14bk_bt_status_t30BK_BT_STATUS_REPEATED_ATTEMPTSE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa0b350e008e5746d6097d263a10d54cd1"></a> enumerator BK\_BT\_STATUS\_REPEATED\_ATTEMPTS

    <a id="_CPPv4N14bk_bt_status_t32BK_BT_STATUS_PAIRING_NOT_ALLOWEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t32BK_BT_STATUS_PAIRING_NOT_ALLOWEDE"></a> <a id="_CPPv2N14bk_bt_status_t32BK_BT_STATUS_PAIRING_NOT_ALLOWEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa9944dcf8613aa44382092a571e1751a3"></a> enumerator BK\_BT\_STATUS\_PAIRING\_NOT\_ALLOWED

    <a id="_CPPv4N14bk_bt_status_t28BK_BT_STATUS_UNKNOWN_LMP_PDUE"></a>

    <a id="_CPPv3N14bk_bt_status_t28BK_BT_STATUS_UNKNOWN_LMP_PDUE"></a> <a id="_CPPv2N14bk_bt_status_t28BK_BT_STATUS_UNKNOWN_LMP_PDUE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa5a8471afdb63c25ab23a7b43fcdad85d"></a> enumerator BK\_BT\_STATUS\_UNKNOWN\_LMP\_PDU

    <a id="_CPPv4N14bk_bt_status_t39BK_BT_STATUS_UNSUPPORTED_REMOTE_FEATUREE"></a>

    <a id="_CPPv3N14bk_bt_status_t39BK_BT_STATUS_UNSUPPORTED_REMOTE_FEATUREE"></a> <a id="_CPPv2N14bk_bt_status_t39BK_BT_STATUS_UNSUPPORTED_REMOTE_FEATUREE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa0fb43f65046db1d39f369df526b7f53d"></a> enumerator BK\_BT\_STATUS\_UNSUPPORTED\_REMOTE\_FEATURE

    <a id="_CPPv4N14bk_bt_status_t32BK_BT_STATUS_SCO_OFFSET_REJECTEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t32BK_BT_STATUS_SCO_OFFSET_REJECTEDE"></a> <a id="_CPPv2N14bk_bt_status_t32BK_BT_STATUS_SCO_OFFSET_REJECTEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa3fd5cb4434f435afc0637d539f683413"></a> enumerator BK\_BT\_STATUS\_SCO\_OFFSET\_REJECTED

    <a id="_CPPv4N14bk_bt_status_t34BK_BT_STATUS_SCO_INTERVAL_REJECTEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t34BK_BT_STATUS_SCO_INTERVAL_REJECTEDE"></a> <a id="_CPPv2N14bk_bt_status_t34BK_BT_STATUS_SCO_INTERVAL_REJECTEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aacfb18cae4dd358c322a9c9182f89a188"></a> enumerator BK\_BT\_STATUS\_SCO\_INTERVAL\_REJECTED

    <a id="_CPPv4N14bk_bt_status_t34BK_BT_STATUS_SCO_AIR_MODE_REJECTEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t34BK_BT_STATUS_SCO_AIR_MODE_REJECTEDE"></a> <a id="_CPPv2N14bk_bt_status_t34BK_BT_STATUS_SCO_AIR_MODE_REJECTEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aaa81a5d60b6cbe74b2e3aa29830a99ebb"></a> enumerator BK\_BT\_STATUS\_SCO\_AIR\_MODE\_REJECTED

    <a id="_CPPv4N14bk_bt_status_t30BK_BT_STATUS_INVALID_LMP_PARAME"></a>

    <a id="_CPPv3N14bk_bt_status_t30BK_BT_STATUS_INVALID_LMP_PARAME"></a> <a id="_CPPv2N14bk_bt_status_t30BK_BT_STATUS_INVALID_LMP_PARAME"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa154eaa038777ac1cbe7ba307fa32570c"></a> enumerator BK\_BT\_STATUS\_INVALID\_LMP\_PARAM

    <a id="_CPPv4N14bk_bt_status_t30BK_BT_STATUS_UNSPECIFIED_ERRORE"></a>

    <a id="_CPPv3N14bk_bt_status_t30BK_BT_STATUS_UNSPECIFIED_ERRORE"></a> <a id="_CPPv2N14bk_bt_status_t30BK_BT_STATUS_UNSPECIFIED_ERRORE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa37f5c6ff1310059b2d69a4c2dce63791"></a> enumerator BK\_BT\_STATUS\_UNSPECIFIED\_ERROR

    <a id="_CPPv4N14bk_bt_status_t40BK_BT_STATUS_UNSUPPORTED_LMP_PARAM_VALUEE"></a>

    <a id="_CPPv3N14bk_bt_status_t40BK_BT_STATUS_UNSUPPORTED_LMP_PARAM_VALUEE"></a> <a id="_CPPv2N14bk_bt_status_t40BK_BT_STATUS_UNSUPPORTED_LMP_PARAM_VALUEE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa63fed40e6ba9ba22dd01be6e955d851f"></a> enumerator BK\_BT\_STATUS\_UNSUPPORTED\_LMP\_PARAM\_VALUE

    <a id="_CPPv4N14bk_bt_status_t36BK_BT_STATUS_ROLE_CHANGE_NOT_ALLOWEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t36BK_BT_STATUS_ROLE_CHANGE_NOT_ALLOWEDE"></a> <a id="_CPPv2N14bk_bt_status_t36BK_BT_STATUS_ROLE_CHANGE_NOT_ALLOWEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa9b2c5d1caead5ed3a5eac1102f9f11dc"></a> enumerator BK\_BT\_STATUS\_ROLE\_CHANGE\_NOT\_ALLOWED

    <a id="_CPPv4N14bk_bt_status_t28BK_BT_STATUS_LMP_RSP_TIMEOUTE"></a>

    <a id="_CPPv3N14bk_bt_status_t28BK_BT_STATUS_LMP_RSP_TIMEOUTE"></a> <a id="_CPPv2N14bk_bt_status_t28BK_BT_STATUS_LMP_RSP_TIMEOUTE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aac46e02ea984629bed5758c8f971d8746"></a> enumerator BK\_BT\_STATUS\_LMP\_RSP\_TIMEOUT

    <a id="_CPPv4N14bk_bt_status_t26BK_BT_STATUS_LMP_COLLISIONE"></a>

    <a id="_CPPv3N14bk_bt_status_t26BK_BT_STATUS_LMP_COLLISIONE"></a> <a id="_CPPv2N14bk_bt_status_t26BK_BT_STATUS_LMP_COLLISIONE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aadbdee73ae4f1a2301d53d21d20733d90"></a> enumerator BK\_BT\_STATUS\_LMP\_COLLISION

    <a id="_CPPv4N14bk_bt_status_t32BK_BT_STATUS_LMP_PDU_NOT_ALLOWEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t32BK_BT_STATUS_LMP_PDU_NOT_ALLOWEDE"></a> <a id="_CPPv2N14bk_bt_status_t32BK_BT_STATUS_LMP_PDU_NOT_ALLOWEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa4890ba09313f631ecaab87bd9b58b540"></a> enumerator BK\_BT\_STATUS\_LMP\_PDU\_NOT\_ALLOWED

    <a id="_CPPv4N14bk_bt_status_t32BK_BT_STATUS_ENC_MODE_NOT_ACCEPTE"></a>

    <a id="_CPPv3N14bk_bt_status_t32BK_BT_STATUS_ENC_MODE_NOT_ACCEPTE"></a> <a id="_CPPv2N14bk_bt_status_t32BK_BT_STATUS_ENC_MODE_NOT_ACCEPTE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa105d40e49693590d1635f79dd9bc7adf"></a> enumerator BK\_BT\_STATUS\_ENC\_MODE\_NOT\_ACCEPT

    <a id="_CPPv4N14bk_bt_status_t33BK_BT_STATUS_LINK_KEY_CANT_CHANGEE"></a>

    <a id="_CPPv3N14bk_bt_status_t33BK_BT_STATUS_LINK_KEY_CANT_CHANGEE"></a> <a id="_CPPv2N14bk_bt_status_t33BK_BT_STATUS_LINK_KEY_CANT_CHANGEE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aaca1e748da2b722aa53ee5de5fc452e7a"></a> enumerator BK\_BT\_STATUS\_LINK\_KEY\_CANT\_CHANGE

    <a id="_CPPv4N14bk_bt_status_t30BK_BT_STATUS_QOS_NOT_SUPPORTEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t30BK_BT_STATUS_QOS_NOT_SUPPORTEDE"></a> <a id="_CPPv2N14bk_bt_status_t30BK_BT_STATUS_QOS_NOT_SUPPORTEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa01134ef6de3e3ffaf62cde6d3fbf833b"></a> enumerator BK\_BT\_STATUS\_QOS\_NOT\_SUPPORTED

    <a id="_CPPv4N14bk_bt_status_t27BK_BT_STATUS_INSTANT_PASSEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t27BK_BT_STATUS_INSTANT_PASSEDE"></a> <a id="_CPPv2N14bk_bt_status_t27BK_BT_STATUS_INSTANT_PASSEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa3fb81549065fe945b058a0bc3b52af6a"></a> enumerator BK\_BT\_STATUS\_INSTANT\_PASSED

    <a id="_CPPv4N14bk_bt_status_t42BK_BT_STATUS_PAIRING_WITH_UNIT_KEY_NOT_SUPE"></a>

    <a id="_CPPv3N14bk_bt_status_t42BK_BT_STATUS_PAIRING_WITH_UNIT_KEY_NOT_SUPE"></a> <a id="_CPPv2N14bk_bt_status_t42BK_BT_STATUS_PAIRING_WITH_UNIT_KEY_NOT_SUPE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa11b2fc6d9a605831b899a88aef0b88e8"></a> enumerator BK\_BT\_STATUS\_PAIRING\_WITH\_UNIT\_KEY\_NOT\_SUP

    <a id="_CPPv4N14bk_bt_status_t39BK_BT_STATUS_DIFF_TRANSACTION_COLLISIONE"></a>

    <a id="_CPPv3N14bk_bt_status_t39BK_BT_STATUS_DIFF_TRANSACTION_COLLISIONE"></a> <a id="_CPPv2N14bk_bt_status_t39BK_BT_STATUS_DIFF_TRANSACTION_COLLISIONE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa45233800f03e2e56683b943b5275b7e7"></a> enumerator BK\_BT\_STATUS\_DIFF\_TRANSACTION\_COLLISION

    <a id="_CPPv4N14bk_bt_status_t35BK_BT_STATUS_QOS_UNACCEPTABLE_PARAME"></a>

    <a id="_CPPv3N14bk_bt_status_t35BK_BT_STATUS_QOS_UNACCEPTABLE_PARAME"></a> <a id="_CPPv2N14bk_bt_status_t35BK_BT_STATUS_QOS_UNACCEPTABLE_PARAME"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa7f886945a4335c5b8bb40c0358f83497"></a> enumerator BK\_BT\_STATUS\_QOS\_UNACCEPTABLE\_PARAM

    <a id="_CPPv4N14bk_bt_status_t25BK_BT_STATUS_QOS_REJECTEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t25BK_BT_STATUS_QOS_REJECTEDE"></a> <a id="_CPPv2N14bk_bt_status_t25BK_BT_STATUS_QOS_REJECTEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aab672cd52c0d10e0a3e3301c79276edd4"></a> enumerator BK\_BT\_STATUS\_QOS\_REJECTED

    <a id="_CPPv4N14bk_bt_status_t34BK_BT_STATUS_CHANNEL_CLASS_NOT_SUPE"></a>

    <a id="_CPPv3N14bk_bt_status_t34BK_BT_STATUS_CHANNEL_CLASS_NOT_SUPE"></a> <a id="_CPPv2N14bk_bt_status_t34BK_BT_STATUS_CHANNEL_CLASS_NOT_SUPE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aacea0546a42a1c96a7802d99c056f5015"></a> enumerator BK\_BT\_STATUS\_CHANNEL\_CLASS\_NOT\_SUP

    <a id="_CPPv4N14bk_bt_status_t34BK_BT_STATUS_INSUFFICIENT_SECURITYE"></a>

    <a id="_CPPv3N14bk_bt_status_t34BK_BT_STATUS_INSUFFICIENT_SECURITYE"></a> <a id="_CPPv2N14bk_bt_status_t34BK_BT_STATUS_INSUFFICIENT_SECURITYE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aacfc71a9a8c74018ee5802bddea7a17c2"></a> enumerator BK\_BT\_STATUS\_INSUFFICIENT\_SECURITY

    <a id="_CPPv4N14bk_bt_status_t36BK_BT_STATUS_PARAM_OUT_OF_MAND_RANGEE"></a>

    <a id="_CPPv3N14bk_bt_status_t36BK_BT_STATUS_PARAM_OUT_OF_MAND_RANGEE"></a> <a id="_CPPv2N14bk_bt_status_t36BK_BT_STATUS_PARAM_OUT_OF_MAND_RANGEE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aab45e8c49e37fd33f274229ced356892c"></a> enumerator BK\_BT\_STATUS\_PARAM\_OUT\_OF\_MAND\_RANGE

    <a id="_CPPv4N14bk_bt_status_t29BK_BT_STATUS_ROLE_SWITCH_PENDE"></a>

    <a id="_CPPv3N14bk_bt_status_t29BK_BT_STATUS_ROLE_SWITCH_PENDE"></a> <a id="_CPPv2N14bk_bt_status_t29BK_BT_STATUS_ROLE_SWITCH_PENDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa22ad3c3d185090194cd060e6f327fad3"></a> enumerator BK\_BT\_STATUS\_ROLE\_SWITCH\_PEND

    <a id="_CPPv4N14bk_bt_status_t36BK_BT_STATUS_RESERVED_SLOT_VIOLATIONE"></a>

    <a id="_CPPv3N14bk_bt_status_t36BK_BT_STATUS_RESERVED_SLOT_VIOLATIONE"></a> <a id="_CPPv2N14bk_bt_status_t36BK_BT_STATUS_RESERVED_SLOT_VIOLATIONE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa7c604c8abb6661653e5ca2ca05c61a35"></a> enumerator BK\_BT\_STATUS\_RESERVED\_SLOT\_VIOLATION

    <a id="_CPPv4N14bk_bt_status_t29BK_BT_STATUS_ROLE_SWITCH_FAILE"></a>

    <a id="_CPPv3N14bk_bt_status_t29BK_BT_STATUS_ROLE_SWITCH_FAILE"></a> <a id="_CPPv2N14bk_bt_status_t29BK_BT_STATUS_ROLE_SWITCH_FAILE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa242ebd797356d3c77642c715b2e7f0cc"></a> enumerator BK\_BT\_STATUS\_ROLE\_SWITCH\_FAIL

    <a id="_CPPv4N14bk_bt_status_t26BK_BT_STATUS_EIR_TOO_LARGEE"></a>

    <a id="_CPPv3N14bk_bt_status_t26BK_BT_STATUS_EIR_TOO_LARGEE"></a> <a id="_CPPv2N14bk_bt_status_t26BK_BT_STATUS_EIR_TOO_LARGEE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa66803bca77fb6da2e6a35fedfdfe4144"></a> enumerator BK\_BT\_STATUS\_EIR\_TOO\_LARGE

    <a id="_CPPv4N14bk_bt_status_t34BK_BT_STATUS_SP_NOT_SUPPORTED_HOSTE"></a>

    <a id="_CPPv3N14bk_bt_status_t34BK_BT_STATUS_SP_NOT_SUPPORTED_HOSTE"></a> <a id="_CPPv2N14bk_bt_status_t34BK_BT_STATUS_SP_NOT_SUPPORTED_HOSTE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa063b953c6f3f90494038579eae54ccab"></a> enumerator BK\_BT\_STATUS\_SP\_NOT\_SUPPORTED\_HOST

    <a id="_CPPv4N14bk_bt_status_t30BK_BT_STATUS_HOST_BUSY_PAIRINGE"></a>

    <a id="_CPPv3N14bk_bt_status_t30BK_BT_STATUS_HOST_BUSY_PAIRINGE"></a> <a id="_CPPv2N14bk_bt_status_t30BK_BT_STATUS_HOST_BUSY_PAIRINGE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa21d2c657bf058c33887d6aea7481e08d"></a> enumerator BK\_BT\_STATUS\_HOST\_BUSY\_PAIRING

    <a id="_CPPv4N14bk_bt_status_t28BK_BT_STATUS_CONTROLLER_BUSYE"></a>

    <a id="_CPPv3N14bk_bt_status_t28BK_BT_STATUS_CONTROLLER_BUSYE"></a> <a id="_CPPv2N14bk_bt_status_t28BK_BT_STATUS_CONTROLLER_BUSYE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa42c54768560466df5b1e5da591744417"></a> enumerator BK\_BT\_STATUS\_CONTROLLER\_BUSY

    <a id="_CPPv4N14bk_bt_status_t36BK_BT_STATUS_UNACCEPTABLE_CONN_PARAME"></a>

    <a id="_CPPv3N14bk_bt_status_t36BK_BT_STATUS_UNACCEPTABLE_CONN_PARAME"></a> <a id="_CPPv2N14bk_bt_status_t36BK_BT_STATUS_UNACCEPTABLE_CONN_PARAME"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa14490b12ee3da614f13930afa878424f"></a> enumerator BK\_BT\_STATUS\_UNACCEPTABLE\_CONN\_PARAM

    <a id="_CPPv4N14bk_bt_status_t19BK_BT_STATUS_ADV_TOE"></a>

    <a id="_CPPv3N14bk_bt_status_t19BK_BT_STATUS_ADV_TOE"></a> <a id="_CPPv2N14bk_bt_status_t19BK_BT_STATUS_ADV_TOE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa2d65eee180805d5ca784032b33f41933"></a> enumerator BK\_BT\_STATUS\_ADV\_TO

    <a id="_CPPv4N14bk_bt_status_t35BK_BT_STATUS_TERMINATED_MIC_FAILUREE"></a>

    <a id="_CPPv3N14bk_bt_status_t35BK_BT_STATUS_TERMINATED_MIC_FAILUREE"></a> <a id="_CPPv2N14bk_bt_status_t35BK_BT_STATUS_TERMINATED_MIC_FAILUREE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aaaad61e2e7c5596f8f02b6ec05c7b590b"></a> enumerator BK\_BT\_STATUS\_TERMINATED\_MIC\_FAILURE

    <a id="_CPPv4N14bk_bt_status_t34BK_BT_STATUS_CONN_FAILED_TO_BE_ESTE"></a>

    <a id="_CPPv3N14bk_bt_status_t34BK_BT_STATUS_CONN_FAILED_TO_BE_ESTE"></a> <a id="_CPPv2N14bk_bt_status_t34BK_BT_STATUS_CONN_FAILED_TO_BE_ESTE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aaef53b821e25f7d1c7880f400849dd8cb"></a> enumerator BK\_BT\_STATUS\_CONN\_FAILED\_TO\_BE\_EST

    <a id="_CPPv4N14bk_bt_status_t35BK_BT_STATUS_CCA_REJ_USE_CLOCK_DRAGE"></a>

    <a id="_CPPv3N14bk_bt_status_t35BK_BT_STATUS_CCA_REJ_USE_CLOCK_DRAGE"></a> <a id="_CPPv2N14bk_bt_status_t35BK_BT_STATUS_CCA_REJ_USE_CLOCK_DRAGE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa91e2edccf83b6a1aefbfb1056d8ebe45"></a> enumerator BK\_BT\_STATUS\_CCA\_REJ\_USE\_CLOCK\_DRAG

    <a id="_CPPv4N14bk_bt_status_t37BK_BT_STATUS_TYPE0_SUBMAP_NOT_DEFINEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t37BK_BT_STATUS_TYPE0_SUBMAP_NOT_DEFINEDE"></a> <a id="_CPPv2N14bk_bt_status_t37BK_BT_STATUS_TYPE0_SUBMAP_NOT_DEFINEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa954354477cacdbcf9cb69cfb00af933d"></a> enumerator BK\_BT\_STATUS\_TYPE0\_SUBMAP\_NOT\_DEFINED

    <a id="_CPPv4N14bk_bt_status_t35BK_BT_STATUS_UNKNOWN_ADVERTISING_IDE"></a>

    <a id="_CPPv3N14bk_bt_status_t35BK_BT_STATUS_UNKNOWN_ADVERTISING_IDE"></a> <a id="_CPPv2N14bk_bt_status_t35BK_BT_STATUS_UNKNOWN_ADVERTISING_IDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa24ea2e931bcd5056a8240c60517a317d"></a> enumerator BK\_BT\_STATUS\_UNKNOWN\_ADVERTISING\_ID

    <a id="_CPPv4N14bk_bt_status_t26BK_BT_STATUS_LIMIT_REACHEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t26BK_BT_STATUS_LIMIT_REACHEDE"></a> <a id="_CPPv2N14bk_bt_status_t26BK_BT_STATUS_LIMIT_REACHEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aabb14779914737f2c68d009df74dc5a49"></a> enumerator BK\_BT\_STATUS\_LIMIT\_REACHED

    <a id="_CPPv4N14bk_bt_status_t39BK_BT_STATUS_OPERATION_CANCELED_BY_HOSTE"></a>

    <a id="_CPPv3N14bk_bt_status_t39BK_BT_STATUS_OPERATION_CANCELED_BY_HOSTE"></a> <a id="_CPPv2N14bk_bt_status_t39BK_BT_STATUS_OPERATION_CANCELED_BY_HOSTE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa7e8a84c156fe64d429cef43393e57fc6"></a> enumerator BK\_BT\_STATUS\_OPERATION\_CANCELED\_BY\_HOST

    <a id="_CPPv4N14bk_bt_status_t25BK_BT_STATUS_PKT_TOO_LONGE"></a>

    <a id="_CPPv3N14bk_bt_status_t25BK_BT_STATUS_PKT_TOO_LONGE"></a> <a id="_CPPv2N14bk_bt_status_t25BK_BT_STATUS_PKT_TOO_LONGE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa56cb399c9a0726236e293c11101f2189"></a> enumerator BK\_BT\_STATUS\_PKT\_TOO\_LONG

    <a id="_CPPv4N14bk_bt_status_t21BK_BT_STATUS_TOO_LATEE"></a>

    <a id="_CPPv3N14bk_bt_status_t21BK_BT_STATUS_TOO_LATEE"></a> <a id="_CPPv2N14bk_bt_status_t21BK_BT_STATUS_TOO_LATEE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa127abb21d09ecfdf9f1ebf86511d2e21"></a> enumerator BK\_BT\_STATUS\_TOO\_LATE

    <a id="_CPPv4N14bk_bt_status_t22BK_BT_STATUS_TOO_EARLYE"></a>

    <a id="_CPPv3N14bk_bt_status_t22BK_BT_STATUS_TOO_EARLYE"></a> <a id="_CPPv2N14bk_bt_status_t22BK_BT_STATUS_TOO_EARLYE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa755b139600fdf66a17dec54b11491c67"></a> enumerator BK\_BT\_STATUS\_TOO\_EARLY

    <a id="_CPPv4N14bk_bt_status_t34BK_BT_STATUS_INSUFFICIENT_CHANNELSE"></a>

    <a id="_CPPv3N14bk_bt_status_t34BK_BT_STATUS_INSUFFICIENT_CHANNELSE"></a> <a id="_CPPv2N14bk_bt_status_t34BK_BT_STATUS_INSUFFICIENT_CHANNELSE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aa9936e5a684b14659c8dfa83df119df6d"></a> enumerator BK\_BT\_STATUS\_INSUFFICIENT\_CHANNELS

    <a id="_CPPv4N14bk_bt_status_t22BK_BT_STATUS_UNDEFINEDE"></a>

    <a id="_CPPv3N14bk_bt_status_t22BK_BT_STATUS_UNDEFINEDE"></a> <a id="_CPPv2N14bk_bt_status_t22BK_BT_STATUS_UNDEFINEDE"></a> <a id="bk__dm__bluetooth__types_8h_1gafdf5079d9baee5818018b058ca2c443aafb4d2ff03def9b314da4aff8ce51d24b"></a> enumerator BK\_BT\_STATUS\_UNDEFINED

<a id="_CPPv48bt_cmd_t"></a>

<a id="_CPPv38bt_cmd_t"></a> <a id="_CPPv28bt_cmd_t"></a> <a id="bk__dm__bluetooth__types_8h_1a046528c08c5e557f513f95a4c25000d9"></a> enum bt\_cmd\_t
:   *Values:*

    <a id="_CPPv4N8bt_cmd_t14BT_CMD_INQUIRYE"></a>

    <a id="_CPPv3N8bt_cmd_t14BT_CMD_INQUIRYE"></a> <a id="_CPPv2N8bt_cmd_t14BT_CMD_INQUIRYE"></a> <a id="bk__dm__bluetooth__types_8h_1ga046528c08c5e557f513f95a4c25000d9a45eb5358b964fa6c895b46d31d433d22"></a> enumerator BT\_CMD\_INQUIRY

    <a id="_CPPv4N8bt_cmd_t21BT_CMD_CREATE_CONNECTE"></a>

    <a id="_CPPv3N8bt_cmd_t21BT_CMD_CREATE_CONNECTE"></a> <a id="_CPPv2N8bt_cmd_t21BT_CMD_CREATE_CONNECTE"></a> <a id="bk__dm__bluetooth__types_8h_1ga046528c08c5e557f513f95a4c25000d9a2625a64c3303bd4e0498985bcc2f3e95"></a> enumerator BT\_CMD\_CREATE\_CONNECT

    <a id="_CPPv4N8bt_cmd_t17BT_CMD_DISCONNECTE"></a>

    <a id="_CPPv3N8bt_cmd_t17BT_CMD_DISCONNECTE"></a> <a id="_CPPv2N8bt_cmd_t17BT_CMD_DISCONNECTE"></a> <a id="bk__dm__bluetooth__types_8h_1ga046528c08c5e557f513f95a4c25000d9a132edbd77b26ea097a576637673e9890"></a> enumerator BT\_CMD\_DISCONNECT

    <a id="_CPPv4N8bt_cmd_t10BT_CMD_SDPE"></a>

    <a id="_CPPv3N8bt_cmd_t10BT_CMD_SDPE"></a> <a id="_CPPv2N8bt_cmd_t10BT_CMD_SDPE"></a> <a id="bk__dm__bluetooth__types_8h_1ga046528c08c5e557f513f95a4c25000d9ac01d77e39f721e3d0ae16bbd8ff8dc4d"></a> enumerator BT\_CMD\_SDP

    <a id="_CPPv4N8bt_cmd_t23BT_CMD_READ_SCAN_ENABLEE"></a>

    <a id="_CPPv3N8bt_cmd_t23BT_CMD_READ_SCAN_ENABLEE"></a> <a id="_CPPv2N8bt_cmd_t23BT_CMD_READ_SCAN_ENABLEE"></a> <a id="bk__dm__bluetooth__types_8h_1ga046528c08c5e557f513f95a4c25000d9a97303e62ab450d9983ab26e9c5324c7c"></a> enumerator BT\_CMD\_READ\_SCAN\_ENABLE

    <a id="_CPPv4N8bt_cmd_t24BT_CMD_WRITE_SCAN_ENABLEE"></a>

    <a id="_CPPv3N8bt_cmd_t24BT_CMD_WRITE_SCAN_ENABLEE"></a> <a id="_CPPv2N8bt_cmd_t24BT_CMD_WRITE_SCAN_ENABLEE"></a> <a id="bk__dm__bluetooth__types_8h_1ga046528c08c5e557f513f95a4c25000d9a169b66a0d71737e0d150b393f668ff36"></a> enumerator BT\_CMD\_WRITE\_SCAN\_ENABLE

    <a id="_CPPv4N8bt_cmd_t10BT_CMD_MAXE"></a>

    <a id="_CPPv3N8bt_cmd_t10BT_CMD_MAXE"></a> <a id="_CPPv2N8bt_cmd_t10BT_CMD_MAXE"></a> <a id="bk__dm__bluetooth__types_8h_1ga046528c08c5e557f513f95a4c25000d9a99b0f0b2602d889fbb448d19398ebf88"></a> enumerator BT\_CMD\_MAX

<a id="_CPPv416bk_bt_dev_type_t"></a>

<a id="_CPPv316bk_bt_dev_type_t"></a> <a id="_CPPv216bk_bt_dev_type_t"></a> <a id="group__bk__bt__api__v1__typedef_1gab923f0f1ef494de272e35d5522257cae"></a> enum bk\_bt\_dev\_type\_t
:   Bluetooth device type.

    *Values:*

    <a id="_CPPv4N16bk_bt_dev_type_t23BK_BT_DEVICE_TYPE_BREDRE"></a>

    <a id="_CPPv3N16bk_bt_dev_type_t23BK_BT_DEVICE_TYPE_BREDRE"></a> <a id="_CPPv2N16bk_bt_dev_type_t23BK_BT_DEVICE_TYPE_BREDRE"></a> <a id="group__bk__bt__api__v1__typedef_1ggab923f0f1ef494de272e35d5522257caeaf1c574dee212fe75571cc781f6fca2b2"></a> enumerator BK\_BT\_DEVICE\_TYPE\_BREDR

    <a id="_CPPv4N16bk_bt_dev_type_t21BK_BT_DEVICE_TYPE_BLEE"></a>

    <a id="_CPPv3N16bk_bt_dev_type_t21BK_BT_DEVICE_TYPE_BLEE"></a> <a id="_CPPv2N16bk_bt_dev_type_t21BK_BT_DEVICE_TYPE_BLEE"></a> <a id="group__bk__bt__api__v1__typedef_1ggab923f0f1ef494de272e35d5522257caeaab2e598a7b31b2cce92d446d5276418b"></a> enumerator BK\_BT\_DEVICE\_TYPE\_BLE

    <a id="_CPPv4N16bk_bt_dev_type_t22BK_BT_DEVICE_TYPE_DUMOE"></a>

    <a id="_CPPv3N16bk_bt_dev_type_t22BK_BT_DEVICE_TYPE_DUMOE"></a> <a id="_CPPv2N16bk_bt_dev_type_t22BK_BT_DEVICE_TYPE_DUMOE"></a> <a id="group__bk__bt__api__v1__typedef_1ggab923f0f1ef494de272e35d5522257caea771b9d2bfc1a82d29046f1bcaff687ec"></a> enumerator BK\_BT\_DEVICE\_TYPE\_DUMO

<a id="_CPPv418bk_ble_addr_type_t"></a>

<a id="_CPPv318bk_ble_addr_type_t"></a> <a id="_CPPv218bk_ble_addr_type_t"></a> <a id="group__bk__bt__api__v1__typedef_1gaf3c970b6b04b9a9e8260bd4123dfdf6f"></a> enum bk\_ble\_addr\_type\_t
:   BLE device address type.

    *Values:*

    <a id="_CPPv4N18bk_ble_addr_type_t20BLE_ADDR_TYPE_PUBLICE"></a>

    <a id="_CPPv3N18bk_ble_addr_type_t20BLE_ADDR_TYPE_PUBLICE"></a> <a id="_CPPv2N18bk_ble_addr_type_t20BLE_ADDR_TYPE_PUBLICE"></a> <a id="group__bk__bt__api__v1__typedef_1ggaf3c970b6b04b9a9e8260bd4123dfdf6fa7fd1fcdd8421c7d69e24574f155714d3"></a> enumerator BLE\_ADDR\_TYPE\_PUBLIC

    <a id="_CPPv4N18bk_ble_addr_type_t20BLE_ADDR_TYPE_RANDOME"></a>

    <a id="_CPPv3N18bk_ble_addr_type_t20BLE_ADDR_TYPE_RANDOME"></a> <a id="_CPPv2N18bk_ble_addr_type_t20BLE_ADDR_TYPE_RANDOME"></a> <a id="group__bk__bt__api__v1__typedef_1ggaf3c970b6b04b9a9e8260bd4123dfdf6fae59f625403ab0127fd6f0a2f8d6b6e38"></a> enumerator BLE\_ADDR\_TYPE\_RANDOM

    <a id="_CPPv4N18bk_ble_addr_type_t24BLE_ADDR_TYPE_RPA_PUBLICE"></a>

    <a id="_CPPv3N18bk_ble_addr_type_t24BLE_ADDR_TYPE_RPA_PUBLICE"></a> <a id="_CPPv2N18bk_ble_addr_type_t24BLE_ADDR_TYPE_RPA_PUBLICE"></a> <a id="group__bk__bt__api__v1__typedef_1ggaf3c970b6b04b9a9e8260bd4123dfdf6fadd639f15898f0aff40a11c5d00b94d8c"></a> enumerator BLE\_ADDR\_TYPE\_RPA\_PUBLIC
    :   when used with own addr, below means rpa effort, otherwise public when used with peer addr, below doesn’t used

    <a id="_CPPv4N18bk_ble_addr_type_t24BLE_ADDR_TYPE_RPA_RANDOME"></a>

    <a id="_CPPv3N18bk_ble_addr_type_t24BLE_ADDR_TYPE_RPA_RANDOME"></a> <a id="_CPPv2N18bk_ble_addr_type_t24BLE_ADDR_TYPE_RPA_RANDOME"></a> <a id="group__bk__bt__api__v1__typedef_1ggaf3c970b6b04b9a9e8260bd4123dfdf6faecdb1969a46a79e92c1dda55a5064d57"></a> enumerator BLE\_ADDR\_TYPE\_RPA\_RANDOM
    :   when used with own addr, below means rpa effort, otherwise random when used with peer addr, below doesn’t used

<a id="_CPPv421bk_ble_wl_addr_type_t"></a>

<a id="_CPPv321bk_ble_wl_addr_type_t"></a> <a id="_CPPv221bk_ble_wl_addr_type_t"></a> <a id="group__bk__bt__api__v1__typedef_1gad2aa23fbf8b225d0c22a6358e10c50b0"></a> enum bk\_ble\_wl\_addr\_type\_t
:   white list address type

    *Values:*

    <a id="_CPPv4N21bk_ble_wl_addr_type_t23BLE_WL_ADDR_TYPE_PUBLICE"></a>

    <a id="_CPPv3N21bk_ble_wl_addr_type_t23BLE_WL_ADDR_TYPE_PUBLICE"></a> <a id="_CPPv2N21bk_ble_wl_addr_type_t23BLE_WL_ADDR_TYPE_PUBLICE"></a> <a id="group__bk__bt__api__v1__typedef_1ggad2aa23fbf8b225d0c22a6358e10c50b0ab13ad8dc865189d509404ca4513640f3"></a> enumerator BLE\_WL\_ADDR\_TYPE\_PUBLIC

    <a id="_CPPv4N21bk_ble_wl_addr_type_t23BLE_WL_ADDR_TYPE_RANDOME"></a>

    <a id="_CPPv3N21bk_ble_wl_addr_type_t23BLE_WL_ADDR_TYPE_RANDOME"></a> <a id="_CPPv2N21bk_ble_wl_addr_type_t23BLE_WL_ADDR_TYPE_RANDOME"></a> <a id="group__bk__bt__api__v1__typedef_1ggad2aa23fbf8b225d0c22a6358e10c50b0a12735d9987e3759ed26023b93b564775"></a> enumerator BLE\_WL\_ADDR\_TYPE\_RANDOM

<a id="id31"></a>

## 参考链接

> [API 参考：](../bluetooth.md) 介绍蓝牙 API 接口。
>
> [蓝牙开发者指南：](../../developer-guide/bluetooth.md) 介绍蓝牙开发者指南。
