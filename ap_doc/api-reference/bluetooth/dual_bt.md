---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/bluetooth/dual_bt.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bt"></a>

# 双模 BT

<a id="dual-bt-api"></a>

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

<a id="id1"></a>

## 兼容性和扩展性

Dual BT API 具备较好的扩展性和向后兼容性。多数 BT 配置结构体中预留了字段，便于后续扩展。使用这些 API 时，应将预留字段初始化为 0，避免后续新增字段后影响兼容性。

<a id="id2"></a>

## 编程原则

重要

使用 BT API 时建议遵循以下原则：
:   - 配置结构体中的预留字段应初始化为 0。
    - 使用 `BK_ERR_CHECK` 检查 BT API 的返回值。
    - 不确定 API 用法时，优先参考 BT 示例代码。
    - 不确定配置结构体字段如何初始化时，先使用默认配置宏，再按应用需求修改相关字段。
    - 不建议在 BT 事件回调中执行耗时操作，可将事件转发到应用任务中处理。

<a id="id3"></a>

## 事件处理机制

Beken BT driver 采用事件驱动方式工作。应用通过 BT API 发起可发现、可连接、配对、profile 连接等操作，并在 BT 事件回调中获取状态变化和操作结果。

<a id="api"></a>

## API 参考

<a id="bk-dm-gap-bt-h"></a>

## bk\_dm\_gap\_bt.h

`bk_dm_gap_bt.h` 提供 BT GAP 的可发现、可连接、配对和设备管理接口。

<a id="header-file"></a>

### Header File

- [bk\_dm\_gap\_bt.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_gap_bt.h)

<a id="functions"></a>

### Functions

<a id="_CPPv427bk_bt_gap_register_callback14bk_bt_gap_cb_t"></a>

<a id="_CPPv327bk_bt_gap_register_callback14bk_bt_gap_cb_t"></a> <a id="_CPPv227bk_bt_gap_register_callback14bk_bt_gap_cb_t"></a> <a id="bk_bt_gap_register_callback__bk_bt_gap_cb_t"></a> <a id="bk__dm__gap__bt_8h_1a4978688f3e7b7e715a274854f6c7268b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_register\_callback([bk\_bt\_gap\_cb\_t](#_CPPv414bk_bt_gap_cb_t "bk_bt_gap_cb_t") callback)
:   register callback function. This function should be called after bk\_bluedroid\_enable() completes successfully

    返回
    :   - BK\_OK : Succeed
        - BK\_FAIL: others

<a id="_CPPv423bk_bt_gap_set_scan_mode17bk_bt_conn_mode_t17bk_bt_disc_mode_t"></a>

<a id="_CPPv323bk_bt_gap_set_scan_mode17bk_bt_conn_mode_t17bk_bt_disc_mode_t"></a> <a id="_CPPv223bk_bt_gap_set_scan_mode17bk_bt_conn_mode_t17bk_bt_disc_mode_t"></a> <a id="bk_bt_gap_set_scan_mode__bk_bt_conn_mode_t.bk_bt_disc_mode_t"></a> <a id="bk__dm__gap__bt_8h_1a4999840b52964a43b06d5e007b9a6025"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_set\_scan\_mode([bk\_bt\_conn\_mode\_t](#_CPPv417bk_bt_conn_mode_t "bk_bt_conn_mode_t") c\_mode, [bk\_bt\_disc\_mode\_t](#_CPPv417bk_bt_disc_mode_t "bk_bt_disc_mode_t") d\_mode)
:   Set discoverability and connectability mode for legacy bluetooth.

    参数
    :   - **c\_mode** – **\[in\]** : one of the enums of bk\_bt\_connection\_mode\_t
        - **d\_mode** – **\[in\]** : one of the enums of bk\_bt\_discovery\_mode\_t

    返回
    :   - BK\_OK : Succeed
        - BK\_ERR\_INVALID\_ARG: if argument invalid
        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - BK\_FAIL: others

<a id="_CPPv423bk_bt_gap_get_scan_modev"></a>

<a id="_CPPv323bk_bt_gap_get_scan_modev"></a> <a id="_CPPv223bk_bt_gap_get_scan_modev"></a> <a id="bk_bt_gap_get_scan_mode"></a> <a id="bk__dm__gap__bt_8h_1a447f771b252f4a9e815b549c8eaed69f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_get\_scan\_mode()
:   Get discoverability and connectability mode of legacy bluetooth.

    返回
    :   - BK\_OK : Succeed
        - BK\_ERR\_INVALID\_ARG: if argument invalid
        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - BK\_FAIL: others

<a id="_CPPv425bk_bt_gap_start_discovery16bk_bt_inq_mode_t7uint8_t7uint8_t"></a>

<a id="_CPPv325bk_bt_gap_start_discovery16bk_bt_inq_mode_t7uint8_t7uint8_t"></a> <a id="_CPPv225bk_bt_gap_start_discovery16bk_bt_inq_mode_t7uint8_t7uint8_t"></a> <a id="bk_bt_gap_start_discovery__bk_bt_inq_mode_t.uint8_t.uint8_t"></a> <a id="bk__dm__gap__bt_8h_1aff1490fa21c1e5551887955d290a1d5f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_start\_discovery([bk\_bt\_inq\_mode\_t](#_CPPv416bk_bt_inq_mode_t "bk_bt_inq_mode_t") mode, uint8\_t inq\_len, uint8\_t num\_rsps)
:   This function starts Inquiry and Name Discovery. When Inquiry is halted and cached results do not contain device name, then Name Discovery will connect to the peer target to get the device name. bk\_bt\_gap\_cb\_t will be called with BK\_BT\_GAP\_DISC\_STATE\_CHANGED\_EVT when Inquriry is started or Name Discovery is completed. bk\_bt\_gap\_cb\_t will be called with BK\_BT\_GAP\_DISC\_RES\_EVT each time the two types of discovery results are got.

    参数
    :   - **mode** – **\[in\]** \- Inquiry mode
        - **inq\_len** – **\[in\]** \- Inquiry duration in 1.28 sec units, ranging from 0x01 to 0x30. This parameter only specifies the total duration of the Inquiry process,

          - when this time expires, Inquiry will be halted.
        - **num\_rsps** – **\[in\]** \- Number of responses that can be received before the Inquiry is halted, value 0 indicates an unlimited number of responses.

    返回
    :   - BK\_OK : Succeed
        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - BK\_ERR\_INVALID\_ARG: if invalid parameters are provided
        - BK\_FAIL: others

<a id="_CPPv426bk_bt_gap_cancel_discoveryv"></a>

<a id="_CPPv326bk_bt_gap_cancel_discoveryv"></a> <a id="_CPPv226bk_bt_gap_cancel_discoveryv"></a> <a id="bk_bt_gap_cancel_discovery__void"></a> <a id="bk__dm__gap__bt_8h_1ade931980b3eef23bb23404c68b663bd2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_cancel\_discovery(void)
:   Cancel Inquiry and Name Discovery. bk\_bt\_gap\_cb\_t will be called with BK\_BT\_GAP\_DISC\_STATE\_CHANGED\_EVT if Inquiry or Name Discovery is cancelled by calling this function.

    返回
    :   - BK\_OK : Succeed
        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - BK\_FAIL: others

<a id="_CPPv429bk_bt_gap_get_remote_services12bk_bd_addr_t"></a>

<a id="_CPPv329bk_bt_gap_get_remote_services12bk_bd_addr_t"></a> <a id="_CPPv229bk_bt_gap_get_remote_services12bk_bd_addr_t"></a> <a id="bk_bt_gap_get_remote_services__bk_bd_addr_t"></a> <a id="bk__dm__gap__bt_8h_1a0c29275845fc27b2344d04fd43dd1a55"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_get\_remote\_services([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda)
:   Start SDP to get remote services. bk\_bt\_gap\_cb\_t will be called with BK\_BT\_GAP\_RMT\_SRVCS\_EVT after service discovery ends.

    返回
    :   - BK\_OK : Succeed
        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - BK\_FAIL: others

<a id="_CPPv435bk_bt_gap_get_remote_service_record12bk_bd_addr_tP12bk_bt_uuid_t"></a>

<a id="_CPPv335bk_bt_gap_get_remote_service_record12bk_bd_addr_tP12bk_bt_uuid_t"></a> <a id="_CPPv235bk_bt_gap_get_remote_service_record12bk_bd_addr_tP12bk_bt_uuid_t"></a> <a id="bk_bt_gap_get_remote_service_record__bk_bd_addr_t.bk_bt_uuid_tP"></a> <a id="bk__dm__gap__bt_8h_1aa8af5a7aefcfd0732936bf4933e11097"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_get\_remote\_service\_record([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda, [bk\_bt\_uuid\_t](dual_ble.md#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") \*uuid)
:   Start SDP to look up the service matching uuid on the remote device.

    ```
                 bk_bt_gap_cb_t will be called with BK_BT_GAP_RMT_SRVC_REC_EVT after service discovery ends
    ```

    返回
    :   - BK\_OK : Succeed
        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - BK\_FAIL: others

<a id="_CPPv425bk_bt_gap_config_eir_dataP16bk_bt_eir_data_t"></a>

<a id="_CPPv325bk_bt_gap_config_eir_dataP16bk_bt_eir_data_t"></a> <a id="_CPPv225bk_bt_gap_config_eir_dataP16bk_bt_eir_data_t"></a> <a id="bk_bt_gap_config_eir_data__bk_bt_eir_data_tP"></a> <a id="bk__dm__gap__bt_8h_1a661e1c66750275acad09e206eb73c145"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_config\_eir\_data([bk\_bt\_eir\_data\_t](#_CPPv416bk_bt_eir_data_t "bk_bt_eir_data_t") \*eir\_data)
:   This function is called to config EIR data.

    ```
                 bk_bt_gap_cb_t will be called with BK_BT_GAP_CONFIG_EIR_DATA_EVT after config EIR ends.
    ```

    参数
    :   **eir\_data** – **\[in\]** \- pointer of EIR data content

    返回
    :   - BK\_OK : Succeed
        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - BK\_ERR\_INVALID\_ARG: if param is invalid
        - BK\_FAIL: others

<a id="_CPPv431bk_bt_gap_set_eir_raw_data_elemP25bk_bt_eir_raw_data_elem_t7uint8_t"></a>

<a id="_CPPv331bk_bt_gap_set_eir_raw_data_elemP25bk_bt_eir_raw_data_elem_t7uint8_t"></a> <a id="_CPPv231bk_bt_gap_set_eir_raw_data_elemP25bk_bt_eir_raw_data_elem_t7uint8_t"></a> <a id="bk_bt_gap_set_eir_raw_data_elem__bk_bt_eir_raw_data_elem_tP.uint8_t"></a> <a id="bk__dm__gap__bt_8h_1a9faab96dd3a4e09ed53df9b5ca44f43c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_set\_eir\_raw\_data\_elem([bk\_bt\_eir\_raw\_data\_elem\_t](#_CPPv425bk_bt_eir_raw_data_elem_t "bk_bt_eir_raw_data_elem_t") \*elem, uint8\_t count)

<a id="_CPPv417bk_bt_gap_set_cod11bk_bt_cod_t16bk_bt_cod_mode_t"></a>

<a id="_CPPv317bk_bt_gap_set_cod11bk_bt_cod_t16bk_bt_cod_mode_t"></a> <a id="_CPPv217bk_bt_gap_set_cod11bk_bt_cod_t16bk_bt_cod_mode_t"></a> <a id="bk_bt_gap_set_cod__bk_bt_cod_t.bk_bt_cod_mode_t"></a> <a id="bk__dm__gap__bt_8h_1ab59637f40998f1ec99a599d3659f6fa7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_set\_cod([bk\_bt\_cod\_t](#_CPPv411bk_bt_cod_t "bk_bt_cod_t") cod, [bk\_bt\_cod\_mode\_t](#_CPPv416bk_bt_cod_mode_t "bk_bt_cod_mode_t") mode)
:   This function is called to set class of device. The structure bk\_bt\_gap\_cb\_t will be called with BK\_BT\_GAP\_SET\_COD\_EVT after set COD ends. Some profile have special restrictions on class of device, changes may cause these profile do not work.

    参数
    :   - **cod** – **\[in\]** \- class of device
        - **mode** – **\[in\]** \- setting mode

    返回
    :   - BK\_OK : Succeed
        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - BK\_ERR\_INVALID\_ARG: if param is invalid
        - BK\_FAIL: others

<a id="_CPPv425bk_bt_gap_read_rssi_delta12bk_bd_addr_t"></a>

<a id="_CPPv325bk_bt_gap_read_rssi_delta12bk_bd_addr_t"></a> <a id="_CPPv225bk_bt_gap_read_rssi_delta12bk_bd_addr_t"></a> <a id="bk_bt_gap_read_rssi_delta__bk_bd_addr_t"></a> <a id="bk__dm__gap__bt_8h_1ae684dcf27579ce866c5a0534ca2d4f4d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_read\_rssi\_delta([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_addr)
:   This function is called to read RSSI delta by address after connected. The RSSI value returned by BK\_BT\_GAP\_READ\_RSSI\_DELTA\_EVT.

    参数
    :   **remote\_addr** – **\[in\]** \- remote device address, corrbkonding to a certain connection handle

    返回
    :   - BK\_OK : Succeed
        - BK\_FAIL: others

<a id="_CPPv427bk_bt_gap_set_addr_log_mask7uint8_t"></a>

<a id="_CPPv327bk_bt_gap_set_addr_log_mask7uint8_t"></a> <a id="_CPPv227bk_bt_gap_set_addr_log_mask7uint8_t"></a> <a id="bk_bt_gap_set_addr_log_mask__uint8_t"></a> <a id="bk__dm__gap__bt_8h_1a5dda237cf14f3d6322bb3ea63e231b12"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_set\_addr\_log\_mask(uint8\_t mask\_enable)
:   This function is called to mask the bluetooth device address printed in SDK log. By default the full address is printed. Once enabled, the address is printed as xx:xx:xx:xx:AA:BB with only the lowest 2 bytes visible.

    **Attention**
    :   This API can be called before [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2).

    参数
    :   **mask\_enable** – **\[in\]** \- 0: print full address, 1: mask the address

    返回
    :   - BK\_OK : Succeed
        - BK\_FAIL: others

<a id="_CPPv428bk_bt_gap_remove_bond_device12bk_bd_addr_t"></a>

<a id="_CPPv328bk_bt_gap_remove_bond_device12bk_bd_addr_t"></a> <a id="_CPPv228bk_bt_gap_remove_bond_device12bk_bd_addr_t"></a> <a id="bk_bt_gap_remove_bond_device__bk_bd_addr_t"></a> <a id="bk__dm__gap__bt_8h_1a4dd74bcabef102a9333fbf7cb885dfec"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_remove\_bond\_device([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   Removes a device from the security database list of peer device.

    参数
    :   **bd\_addr** – **\[in\]** : BD address of the peer device

    返回
    :   \- BK\_OK : success

        - BK\_FAIL : failed

<a id="_CPPv429bk_bt_gap_get_bond_device_numv"></a>

<a id="_CPPv329bk_bt_gap_get_bond_device_numv"></a> <a id="_CPPv229bk_bt_gap_get_bond_device_numv"></a> <a id="bk_bt_gap_get_bond_device_num__void"></a> <a id="bk__dm__gap__bt_8h_1a4ed8ba829b532b1667f7375c627fdf38"></a> int bk\_bt\_gap\_get\_bond\_device\_num(void)
:   Get the device number from the security database list of peer device. It will return the device bonded number immediately.

    返回
    :   \- \>\= 0 : bonded devices number

        - BK\_FAIL : failed

<a id="_CPPv430bk_bt_gap_get_bond_device_listPiP12bk_bd_addr_t"></a>

<a id="_CPPv330bk_bt_gap_get_bond_device_listPiP12bk_bd_addr_t"></a> <a id="_CPPv230bk_bt_gap_get_bond_device_listPiP12bk_bd_addr_t"></a> <a id="bk_bt_gap_get_bond_device_list__iP.bk_bd_addr_tP"></a> <a id="bk__dm__gap__bt_8h_1a680780f174bd0551b922231fa54a5449"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_get\_bond\_device\_list(int \*dev\_num, [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") \*dev\_list)
:   Get the device from the security database list of peer device. It will return the device bonded information immediately.

    参数
    :   - **dev\_num** – **\[inout\]** Indicate the dev\_list array(buffer) size as input. If dev\_num is large enough, it means the actual number as output. Suggest that dev\_num value equal to [bk\_ble\_get\_bond\_device\_num()](dual_ble.md#group__dm__gap__defines__v1_1ga197bcd6bbaf7eabfddabce66be9fad92).
        - **dev\_list** – **\[out\]** an array(buffer) of `bk_bd_addr_t` type. Use for storing the bonded devices address. The dev\_list should be allocated by who call this API.

    返回
    :   - BK\_OK : Succeed
        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - BK\_FAIL: others

<a id="_CPPv417bk_bt_gap_set_pin16bk_bt_pin_type_t7uint8_t16bk_bt_pin_code_t"></a>

<a id="_CPPv317bk_bt_gap_set_pin16bk_bt_pin_type_t7uint8_t16bk_bt_pin_code_t"></a> <a id="_CPPv217bk_bt_gap_set_pin16bk_bt_pin_type_t7uint8_t16bk_bt_pin_code_t"></a> <a id="bk_bt_gap_set_pin__bk_bt_pin_type_t.uint8_t.bk_bt_pin_code_t"></a> <a id="bk__dm__gap__bt_8h_1a3859e79cd11a76cd1ac22d0c25d922d1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_set\_pin([bk\_bt\_pin\_type\_t](#_CPPv416bk_bt_pin_type_t "bk_bt_pin_type_t") pin\_type, uint8\_t pin\_code\_len, [bk\_bt\_pin\_code\_t](#_CPPv416bk_bt_pin_code_t "bk_bt_pin_code_t") pin\_code)
:   Set pin type and default pin code for legacy pairing.

    参数
    :   - **pin\_type** – **\[in\]** Use variable or fixed pin. If pin\_type is BK\_BT\_PIN\_TYPE\_VARIABLE, pin\_code and pin\_code\_len will be ignored, and BK\_BT\_GAP\_PIN\_REQ\_EVT will come when control requests for pin code. Else, will use fixed pin code and not callback to users.
        - **pin\_code\_len** – **\[in\]** Length of pin\_code
        - **pin\_code** – **\[in\]** Pin\_code

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv419bk_bt_gap_pin_reply12bk_bd_addr_tb7uint8_t16bk_bt_pin_code_t"></a>

<a id="_CPPv319bk_bt_gap_pin_reply12bk_bd_addr_tb7uint8_t16bk_bt_pin_code_t"></a> <a id="_CPPv219bk_bt_gap_pin_reply12bk_bd_addr_tb7uint8_t16bk_bt_pin_code_t"></a> <a id="bk_bt_gap_pin_reply__bk_bd_addr_t.b.uint8_t.bk_bt_pin_code_t"></a> <a id="bk__dm__gap__bt_8h_1aa8e9da1f10611f426e800d5317fb277e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_pin\_reply([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, bool accept, uint8\_t pin\_code\_len, [bk\_bt\_pin\_code\_t](#_CPPv416bk_bt_pin_code_t "bk_bt_pin_code_t") pin\_code)
:   Reply the pin\_code to the peer device for legacy pairing when BK\_BT\_GAP\_PIN\_REQ\_EVT is coming.

    参数
    :   - **bd\_addr** – **\[in\]** BD address of the peer
        - **accept** – **\[in\]** Pin\_code reply successful or declined.
        - **pin\_code\_len** – **\[in\]** Length of pin\_code
        - **pin\_code** – **\[in\]** Pin\_code

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv428bk_bt_gap_set_security_param16bk_bt_sp_param_tPv7uint8_t"></a>

<a id="_CPPv328bk_bt_gap_set_security_param16bk_bt_sp_param_tPv7uint8_t"></a> <a id="_CPPv228bk_bt_gap_set_security_param16bk_bt_sp_param_tPv7uint8_t"></a> <a id="bk_bt_gap_set_security_param__bk_bt_sp_param_t.voidP.uint8_t"></a> <a id="bk__dm__gap__bt_8h_1adcb1d85b265b2da06d1ac4589b752302"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_set\_security\_param([bk\_bt\_sp\_param\_t](#_CPPv416bk_bt_sp_param_t "bk_bt_sp_param_t") param\_type, void \*value, uint8\_t len)
:   Set a GAP security parameter value. Overrides the default value.

    参数
    :   - **param\_type** – **\[in\]** : the type of the param which is to be set

          - BK\_BT\_SP\_IOCAP\_MODE : value\[0\] \= bk\_bt\_io\_cap\_t (0x00\~0x03), len \= 1
          - BK\_BT\_SP\_AUTHREQ\_MODE: value\[0\] \= authentication requirements (0x00\~0x05), len \= 1
          - BK\_BT\_SP\_OOB\_DATA : value \= \[bd\_addr(6)\]\[ssp\_c(16)\]\[ssp\_r(16)\], len \= 38
        - **value** – **\[in\]** : the param value
        - **len** – **\[in\]** : the length of the param value

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv427bk_bt_gap_ssp_passkey_reply12bk_bd_addr_tb8uint32_t"></a>

<a id="_CPPv327bk_bt_gap_ssp_passkey_reply12bk_bd_addr_tb8uint32_t"></a> <a id="_CPPv227bk_bt_gap_ssp_passkey_reply12bk_bd_addr_tb8uint32_t"></a> <a id="bk_bt_gap_ssp_passkey_reply__bk_bd_addr_t.b.uint32_t"></a> <a id="bk__dm__gap__bt_8h_1a18c54377a8f72b32d66b421cd15c9826"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_ssp\_passkey\_reply([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, bool accept, uint32\_t passkey)
:   Reply the key value to the peer device in the legacy connection stage.

    参数
    :   - **bd\_addr** – **\[in\]** : BD address of the peer
        - **accept** – **\[in\]** : passkey entry successful or declined.
        - **passkey** – **\[in\]** : passkey value, must be a 6 digit number, can be lead by 0\.

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv427bk_bt_gap_ssp_confirm_reply12bk_bd_addr_tb"></a>

<a id="_CPPv327bk_bt_gap_ssp_confirm_reply12bk_bd_addr_tb"></a> <a id="_CPPv227bk_bt_gap_ssp_confirm_reply12bk_bd_addr_tb"></a> <a id="bk_bt_gap_ssp_confirm_reply__bk_bd_addr_t.b"></a> <a id="bk__dm__gap__bt_8h_1a2737315af2be1a8e33051d697734dbdf"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_ssp\_confirm\_reply([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, bool accept)
:   Reply the confirm value to the peer device in the legacy connection stage.

    参数
    :   - **bd\_addr** – **\[in\]** : BD address of the peer device
        - **accept** – **\[in\]** : numbers to compare are the same or different

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv426bk_bt_gap_set_afh_channels22bk_bt_gap_afh_channels"></a>

<a id="_CPPv326bk_bt_gap_set_afh_channels22bk_bt_gap_afh_channels"></a> <a id="_CPPv226bk_bt_gap_set_afh_channels22bk_bt_gap_afh_channels"></a> <a id="bk_bt_gap_set_afh_channels__bk_bt_gap_afh_channels"></a> <a id="bk__dm__gap__bt_8h_1a9783071519aaf7a5ab01596c713eac78"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_set\_afh\_channels([bk\_bt\_gap\_afh\_channels](#_CPPv422bk_bt_gap_afh_channels "bk_bt_gap_afh_channels") channels)
:   Set the AFH channels.

    参数
    :   **channels** – **\[in\]** : The n th such field (in the range 0 to 78\) contains the value for channel n : 0 means channel n is bad. 1 means channel n is unknown. The most significant bit is reserved and shall be set to 0\. At least 20 channels shall be marked as unknown.

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv426bk_bt_gap_read_remote_name12bk_bd_addr_t"></a>

<a id="_CPPv326bk_bt_gap_read_remote_name12bk_bd_addr_t"></a> <a id="_CPPv226bk_bt_gap_read_remote_name12bk_bd_addr_t"></a> <a id="bk_bt_gap_read_remote_name__bk_bd_addr_t"></a> <a id="bk__dm__gap__bt_8h_1a7e91ec01353ef65f4bafa18e80fcb22c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_read\_remote\_name([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda)
:   Read the remote device name.

    参数
    :   **remote\_bda** – **\[in\]** The remote device’s address

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv417bk_bt_gap_connect12bk_bd_addr_t7uint8_t"></a>

<a id="_CPPv317bk_bt_gap_connect12bk_bd_addr_t7uint8_t"></a> <a id="_CPPv217bk_bt_gap_connect12bk_bd_addr_t7uint8_t"></a> <a id="bk_bt_gap_connect__bk_bd_addr_t.uint8_t"></a> <a id="bk__dm__gap__bt_8h_1a981e9783224423f4cd4a5221c21403fc"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_connect([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, uint8\_t allow\_role\_switch)
:   Connect the remote device.

    参数
    :   - **addr** – **\[in\]** The remote device’s address
        - **allow\_role\_switch** – **\[in\]** Allow the role switch

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv420bk_bt_gap_disconnect12bk_bd_addr_t7uint8_t"></a>

<a id="_CPPv320bk_bt_gap_disconnect12bk_bd_addr_t7uint8_t"></a> <a id="_CPPv220bk_bt_gap_disconnect12bk_bd_addr_t7uint8_t"></a> <a id="bk_bt_gap_disconnect__bk_bd_addr_t.uint8_t"></a> <a id="bk__dm__gap__bt_8h_1af512ed83465010e8ffbdcc51f5ea69a4"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_disconnect([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, uint8\_t reason)
:   Disconnect the remote device.

    参数
    :   - **addr** – **\[in\]** The remote device’s address
        - **reason** – **\[in\]** The disconnect reason

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv424bk_bt_gap_disconnect_sco12bk_bd_addr_t7uint8_t"></a>

<a id="_CPPv324bk_bt_gap_disconnect_sco12bk_bd_addr_t7uint8_t"></a> <a id="_CPPv224bk_bt_gap_disconnect_sco12bk_bd_addr_t7uint8_t"></a> <a id="bk_bt_gap_disconnect_sco__bk_bd_addr_t.uint8_t"></a> <a id="bk__dm__gap__bt_8h_1a5aac1523ed705d4b6a9890923d633fc1"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_disconnect\_sco([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") addr, uint8\_t reason)
:   Disconnect sco connection of the remote device.

    参数
    :   - **addr** – **\[in\]** The remote device’s address
        - **reason** – **\[in\]** The disconnect reason

    返回
    :   \- BK\_OK : success

        - BK\_ERR\_INVALID\_STATE: if bluetooth stack is not yet enabled
        - other : failed

<a id="_CPPv428bk_bt_gap_create_conn_cancelP7uint8_t"></a>

<a id="_CPPv328bk_bt_gap_create_conn_cancelP7uint8_t"></a> <a id="_CPPv228bk_bt_gap_create_conn_cancelP7uint8_t"></a> <a id="bk_bt_gap_create_conn_cancel__uint8_tP"></a> <a id="bk__dm__gap__bt_8h_1aad7e6450550b7f972df9c94222e674ba"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_create\_conn\_cancel(uint8\_t \*addr)
:   This API can be used to request cancellation of the ongoing connection creation process.

    参数
    :   **addr** – **\[in\]** The remote device’s address

    返回
    :   ```
                     - BK_ERR_BT_SUCCESS: cancel request is sent to lower layer successfully
                     - others: fail
        ```

<a id="_CPPv426bk_bt_gap_set_page_timeout8uint16_t"></a>

<a id="_CPPv326bk_bt_gap_set_page_timeout8uint16_t"></a> <a id="_CPPv226bk_bt_gap_set_page_timeout8uint16_t"></a> <a id="bk_bt_gap_set_page_timeout__uint16_t"></a> <a id="bk__dm__gap__bt_8h_1aeadcf072e4dc23d5842a0fa71b80e32d"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_set\_page\_timeout(uint16\_t timeout)
:   This api can be used to set the value for the Page\_Timeout configuration parameter.

    参数
    :   **timeout** – **\[in\]** Page Timeout measured in number of Baseband slots, unit of 0.625ms

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv432bk_bt_gap_set_page_scan_activity8uint16_t8uint16_t"></a>

<a id="_CPPv332bk_bt_gap_set_page_scan_activity8uint16_t8uint16_t"></a> <a id="_CPPv232bk_bt_gap_set_page_scan_activity8uint16_t8uint16_t"></a> <a id="bk_bt_gap_set_page_scan_activity__uint16_t.uint16_t"></a> <a id="bk__dm__gap__bt_8h_1ae736725fb5361a99b6cea1cefe506335"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_set\_page\_scan\_activity(uint16\_t interval, uint16\_t window)
:   This api can be used to set the value for the Page\_Scan\_Interval and Page\_Scan\_Window configuration parameters.

    参数
    :   - **interval** – **\[in\]** defines the amount of time between consecutive page scans, unit of 0.625ms,(Range: 0x0012 to 0x1000, only even values are valid)
        - **window** – **\[in\]** defines the amount of time for the duration of the page scan, unit of 0.625ms,(Range: 0x0011 to 0x1000, can only be less than or equal to the Page\_Scan\_Interval)

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv435bk_bt_gap_set_inquiry_scan_activity8uint16_t8uint16_t"></a>

<a id="_CPPv335bk_bt_gap_set_inquiry_scan_activity8uint16_t8uint16_t"></a> <a id="_CPPv235bk_bt_gap_set_inquiry_scan_activity8uint16_t8uint16_t"></a> <a id="bk_bt_gap_set_inquiry_scan_activity__uint16_t.uint16_t"></a> <a id="bk__dm__gap__bt_8h_1ab9d6d44a514ce58b621c5f2dc56bd99c"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_set\_inquiry\_scan\_activity(uint16\_t interval, uint16\_t window)
:   This api can be used to set the value for the Inquiry\_Scan\_Interval and Inquiry\_Scan\_Window configuration parameters.

    参数
    :   - **interval** – **\[in\]** defines the amount of time between consecutive page scans, unit of 0.625ms,(Range: 0x0012 to 0x1000, only even values are valid)
        - **window** – **\[in\]** defines the amount of time for the duration of the page scan, unit of 0.625ms,(Range: 0x0011 to 0x1000, can only be less than or equal to the Inquiry\_Scan\_Interval)

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv432bk_bt_gap_authentication_requestP7uint8_t"></a>

<a id="_CPPv332bk_bt_gap_authentication_requestP7uint8_t"></a> <a id="_CPPv232bk_bt_gap_authentication_requestP7uint8_t"></a> <a id="bk_bt_gap_authentication_request__uint8_tP"></a> <a id="bk__dm__gap__bt_8h_1aa0ad982778b0178b4ebc4bbac488d1c5"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_authentication\_request(uint8\_t \*addr)
:   This api can be used to start authentication request.

    参数
    :   **addr** – **\[in\]** The remote device’s address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv428bk_bt_gap_encryption_requestP7uint8_t"></a>

<a id="_CPPv328bk_bt_gap_encryption_requestP7uint8_t"></a> <a id="_CPPv228bk_bt_gap_encryption_requestP7uint8_t"></a> <a id="bk_bt_gap_encryption_request__uint8_tP"></a> <a id="bk__dm__gap__bt_8h_1ac83fde1dd50d86e75ce70b29f4a1231f"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_encryption\_request(uint8\_t \*addr)
:   This api can be used to start encryption request.

    参数
    :   **addr** – **\[in\]** The remote device’s address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv431bk_bt_gap_set_auto_sniff_policy12bk_bd_addr_t8uint32_tP22bk_bt_gap_sniff_config"></a>

<a id="_CPPv331bk_bt_gap_set_auto_sniff_policy12bk_bd_addr_t8uint32_tP22bk_bt_gap_sniff_config"></a> <a id="_CPPv231bk_bt_gap_set_auto_sniff_policy12bk_bd_addr_t8uint32_tP22bk_bt_gap_sniff_config"></a> <a id="bk_bt_gap_set_auto_sniff_policy__bk_bd_addr_t.uint32_t.bk_bt_gap_sniff_configP"></a> <a id="bk__dm__gap__bt_8h_1a9c4fa2bdf1d819f73675dd351a352f90"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_gap\_set\_auto\_sniff\_policy([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") remote\_bda, uint32\_t sec, [bk\_bt\_gap\_sniff\_config](#_CPPv422bk_bt_gap_sniff_config "bk_bt_gap_sniff_config") \*config)
:   Set auto enter sniff policy. bk\_bt\_gap\_cb\_t will be called with BK\_BT\_GAP\_SET\_AUTO\_SNIFF\_CMPL\_EVT after service discovery ends.

    参数
    :   - **remote\_bda** – **\[in\]** The remote device’s address
        - **sec** – **\[in\]** How long time (second) enter sniff once no ACL data send or recv. When equal 0, will disable auto enter sniff.
        - **config** – **\[in\]** Sniff config. when is NULL, last config will be: max\_interval: 500 msec min interval: 250 msec attempt: 5 msec timeout: 1.25 msec

    返回
    :   - BK\_OK : Succeed
        - BK\_FAIL: others

<a id="_CPPv423bk_bt_gap_sniff_controlP7uint8_t7uint8_tP22bk_bt_gap_sniff_config"></a>

<a id="_CPPv323bk_bt_gap_sniff_controlP7uint8_t7uint8_tP22bk_bt_gap_sniff_config"></a> <a id="_CPPv223bk_bt_gap_sniff_controlP7uint8_t7uint8_tP22bk_bt_gap_sniff_config"></a> <a id="bk_bt_gap_sniff_control__uint8_tP.uint8_t.bk_bt_gap_sniff_configP"></a> <a id="bk__dm__gap__bt_8h_1a33579ccdd799722326be838138c1aeca"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_sniff\_control(uint8\_t \*addr, uint8\_t exit, [bk\_bt\_gap\_sniff\_config](#_CPPv422bk_bt_gap_sniff_config "bk_bt_gap_sniff_config") \*config)
:   This api can be used to place device to sniff mode or end sniff mode.

    参数
    :   - **addr** – **\[in\]** The remote device’s address
        - **exit** – **\[in\]** 1 means to end sniff mode, 0 means to place device to sniff mode
        - **config** – **\[in\]** sniff mode config used to place device to sniff mode

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv421bk_bt_gap_switch_roleP7uint8_t7uint8_t"></a>

<a id="_CPPv321bk_bt_gap_switch_roleP7uint8_t7uint8_t"></a> <a id="_CPPv221bk_bt_gap_switch_roleP7uint8_t7uint8_t"></a> <a id="bk_bt_gap_switch_role__uint8_tP.uint8_t"></a> <a id="bk__dm__gap__bt_8h_1a27890a8fd6dcc00c77bae1babd1923a1"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_switch\_role(uint8\_t \*addr, uint8\_t new\_role)
:   This api can be used to is called to switch role between master and slave.If the connection is placed in sniff mode, please exit sniff mode first.

    参数
    :   - **addr** – **\[in\]** The remote device’s address
        - **new\_role** – **\[in\]** 0 means master, 1 means slave

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv424bk_bt_gap_set_local_nameP7uint8_t7uint8_t"></a>

<a id="_CPPv324bk_bt_gap_set_local_nameP7uint8_t7uint8_t"></a> <a id="_CPPv224bk_bt_gap_set_local_nameP7uint8_t7uint8_t"></a> <a id="bk_bt_gap_set_local_name__uint8_tP.uint8_t"></a> <a id="bk__dm__gap__bt_8h_1a06eeb3be49561eba06a6280073bbe950"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_set\_local\_name(uint8\_t \*name, uint8\_t len)
:   set the local name

    参数
    :   - **name** – **\[in\]** pointer of name
        - **len** – **\[in\]** the length of name

    返回
    :   - BK\_ERR\_BT\_SUCCESS: succeed
        - others: fail

<a id="_CPPv432bk_bt_gap_bredr_smp_authenticateP7uint8_t"></a>

<a id="_CPPv332bk_bt_gap_bredr_smp_authenticateP7uint8_t"></a> <a id="_CPPv232bk_bt_gap_bredr_smp_authenticateP7uint8_t"></a> <a id="bk_bt_gap_bredr_smp_authenticate__uint8_tP"></a> <a id="bk__dm__gap__bt_8h_1a2bc03320e95d91ae39d2bcb2a0c2c06d"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_bredr\_smp\_authenticate(uint8\_t \*addr)
:   Start SMP authentication over an existing BR/EDR link for CTKD.

    **Attention**
    :   The BR/EDR ACL link and its Link Key must already exist.

    参数
    :   **addr** – **\[in\]** remote BR/EDR device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request successfully posted
        - others: fail

<a id="_CPPv448bk_bt_gap_enable_secure_connections_host_support7uint8_t"></a>

<a id="_CPPv348bk_bt_gap_enable_secure_connections_host_support7uint8_t"></a> <a id="_CPPv248bk_bt_gap_enable_secure_connections_host_support7uint8_t"></a> <a id="bk_bt_gap_enable_secure_connections_host_support__uint8_t"></a> <a id="bk__dm__gap__bt_8h_1a24f9f23cafeea98cfb095debdbae73e3"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_enable\_secure\_connections\_host\_support(uint8\_t enable)
:   Enable or disable BR/EDR Secure Connections Host Support.

    **Attention**
    :   Must be called before page scan is enabled and before any ACL connection exists (HCI 0x0C7A requirement).

    参数
    :   **enable** – **\[in\]** 1 to enable, 0 to disable

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request successfully posted
        - others: fail

<a id="_CPPv423bk_bt_gap_linkkey_reply7uint8_tP23bk_bt_linkkey_storage_t"></a>

<a id="_CPPv323bk_bt_gap_linkkey_reply7uint8_tP23bk_bt_linkkey_storage_t"></a> <a id="_CPPv223bk_bt_gap_linkkey_reply7uint8_tP23bk_bt_linkkey_storage_t"></a> <a id="bk_bt_gap_linkkey_reply__uint8_t.bk_bt_linkkey_storage_tP"></a> <a id="bk__dm__gap__bt_8h_1aa4bfe6237c79b4fc52f329ce72cdb575"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_gap\_linkkey\_reply(uint8\_t is\_exist, [bk\_bt\_linkkey\_storage\_t](#_CPPv423bk_bt_linkkey_storage_t "bk_bt_linkkey_storage_t") \*key)
:   send linkkey when peer need authentication

    **Attention**
    :   key-\>addr must be valued

    参数
    :   - **is\_exist** – **\[in\]** : if linkkey exist. If no exist, peer may trigger pair procedure
        - **key** – **\[in\]** : linkkey,

    返回
    :   - BK\_ERR\_BT\_SUCCESS : Succeed
        - BK\_ERR\_BT\_FAIL: others

<a id="bk-dm-a2dp-h"></a>

## bk\_dm\_a2dp.h

`bk_dm_a2dp.h` 提供 A2DP profile 的连接管理和音频流控制接口。

<a id="id4"></a>

### Header File

- [bk\_dm\_a2dp.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_a2dp.h)

<a id="id5"></a>

### Functions

<a id="_CPPv428bk_bt_a2dp_register_callback15bk_bt_a2dp_cb_t"></a>

<a id="_CPPv328bk_bt_a2dp_register_callback15bk_bt_a2dp_cb_t"></a> <a id="_CPPv228bk_bt_a2dp_register_callback15bk_bt_a2dp_cb_t"></a> <a id="bk_bt_a2dp_register_callback__bk_bt_a2dp_cb_t"></a> <a id="bk__dm__a2dp_8h_1a1c2962b8533cc17858582860fec74759"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_register\_callback([bk\_bt\_a2dp\_cb\_t](#_CPPv415bk_bt_a2dp_cb_t "bk_bt_a2dp_cb_t") callback)
:   Register application callback function to A2DP module. used by both A2DP source and sink.

    参数
    :   **callback** – **\[in\]** A2DP event callback function

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv422bk_bt_a2dp_source_initv"></a>

<a id="_CPPv322bk_bt_a2dp_source_initv"></a> <a id="_CPPv222bk_bt_a2dp_source_initv"></a> <a id="bk_bt_a2dp_source_init__void"></a> <a id="bk__dm__a2dp_8h_1a5e5d4bd49e552ccad922d201f6740c3f"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_source\_init(void)
:   Initialize the bluetooth A2DP source module. A2DP can work independently.

    **Attention**
    :   sink/source must init only one.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: if the initialization request is sent to lower layer successfully
        - others: fail

<a id="_CPPv424bk_bt_a2dp_source_deinitv"></a>

<a id="_CPPv324bk_bt_a2dp_source_deinitv"></a> <a id="_CPPv224bk_bt_a2dp_source_deinitv"></a> <a id="bk_bt_a2dp_source_deinit__void"></a> <a id="bk__dm__a2dp_8h_1a10dc10528d7ce219abc70926b28b3f28"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_source\_deinit(void)
:   De-initialize for A2DP source module. This function should be called only after bk\_bt\_a2dp\_source\_init() completes successfully, and BK\_A2DP\_PROF\_STATE\_EVT will reported to APP layer.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: if the initialization request is sent to lower layer successfully
        - others: fail

<a id="_CPPv437bk_a2dp_source_register_data_callback24bk_a2dp_source_data_cb_t"></a>

<a id="_CPPv337bk_a2dp_source_register_data_callback24bk_a2dp_source_data_cb_t"></a> <a id="_CPPv237bk_a2dp_source_register_data_callback24bk_a2dp_source_data_cb_t"></a> <a id="bk_a2dp_source_register_data_callback__bk_a2dp_source_data_cb_t"></a> <a id="bk__dm__a2dp_8h_1a1fd35400831f8a440314914123f84849"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_a2dp\_source\_register\_data\_callback([bk\_a2dp\_source\_data\_cb\_t](#_CPPv424bk_a2dp_source_data_cb_t "bk_a2dp_source_data_cb_t") callback)
:   Register A2DP source data input function. For now, the input should be PCM data stream.

    参数
    :   **callback** – **\[in\]** A2DP source data callback function

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv434bk_a2dp_source_set_pcm_data_format8uint32_t7uint8_t7uint8_t"></a>

<a id="_CPPv334bk_a2dp_source_set_pcm_data_format8uint32_t7uint8_t7uint8_t"></a> <a id="_CPPv234bk_a2dp_source_set_pcm_data_format8uint32_t7uint8_t7uint8_t"></a> <a id="bk_a2dp_source_set_pcm_data_format__uint32_t.uint8_t.uint8_t"></a> <a id="bk__dm__a2dp_8h_1a96d84e1f4f359555c3bae211eaee5cb4"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_a2dp\_source\_set\_pcm\_data\_format(uint32\_t sample\_rate, uint8\_t bit\_depth, uint8\_t channel\_count)
:   set a2dp source data format

    参数
    :   - **sample\_rate** – **\[in\]** pcm data sample rate, such as 8000 16000 32000 44100 48000\.
        - **bit\_depth** – **\[in\]** : pcm data bit depth, now support 16 bits only.
        - **channel\_count** – **\[in\]** : pcm data channel count, support 1 or 2 now.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv443bk_a2dp_source_register_pcm_encode_callback30bk_a2dp_source_pcm_encode_cb_t"></a>

<a id="_CPPv343bk_a2dp_source_register_pcm_encode_callback30bk_a2dp_source_pcm_encode_cb_t"></a> <a id="_CPPv243bk_a2dp_source_register_pcm_encode_callback30bk_a2dp_source_pcm_encode_cb_t"></a> <a id="bk_a2dp_source_register_pcm_encode_callback__bk_a2dp_source_pcm_encode_cb_t"></a> <a id="bk__dm__a2dp_8h_1a3ba2a90599650077b254b345b628f818"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_a2dp\_source\_register\_pcm\_encode\_callback([bk\_a2dp\_source\_pcm\_encode\_cb\_t](#_CPPv430bk_a2dp_source_pcm_encode_cb_t "bk_a2dp_source_pcm_encode_cb_t") cb)
:   register pcm encode callback.

    参数
    :   **cb** – **\[in\]** callback.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv445bk_a2dp_source_register_pcm_resample_callback32bk_a2dp_source_pcm_resample_cb_t"></a>

<a id="_CPPv345bk_a2dp_source_register_pcm_resample_callback32bk_a2dp_source_pcm_resample_cb_t"></a> <a id="_CPPv245bk_a2dp_source_register_pcm_resample_callback32bk_a2dp_source_pcm_resample_cb_t"></a> <a id="bk_a2dp_source_register_pcm_resample_callback__bk_a2dp_source_pcm_resample_cb_t"></a> <a id="bk__dm__a2dp_8h_1aff7e34d1eaede4a3a9d8b1ee708bdb6b"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_a2dp\_source\_register\_pcm\_resample\_callback([bk\_a2dp\_source\_pcm\_resample\_cb\_t](#_CPPv432bk_a2dp_source_pcm_resample_cb_t "bk_a2dp_source_pcm_resample_cb_t") cb)
:   register pcm resample callback, will be used if input pcm is not match a2dp negotiation, see BK\_A2DP\_AUDIO\_SOURCE\_CFG\_EVT.

    参数
    :   **cb** – **\[in\]** callback.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv425bk_bt_a2dp_source_connectP7uint8_t"></a>

<a id="_CPPv325bk_bt_a2dp_source_connectP7uint8_t"></a> <a id="_CPPv225bk_bt_a2dp_source_connectP7uint8_t"></a> <a id="bk_bt_a2dp_source_connect__uint8_tP"></a> <a id="bk__dm__a2dp_8h_1a8b47cde7b1cc5b9baa48c93841c03dd5"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_source\_connect(uint8\_t \*addr)
:   Connect to remote A2DP sink device. This API must be called after bk\_bt\_a2dp\_source\_init()

    参数
    :   **addr** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: connect request is sent to lower layer successfully
        - others: fail

<a id="_CPPv428bk_bt_a2dp_source_disconnectP7uint8_t"></a>

<a id="_CPPv328bk_bt_a2dp_source_disconnectP7uint8_t"></a> <a id="_CPPv228bk_bt_a2dp_source_disconnectP7uint8_t"></a> <a id="bk_bt_a2dp_source_disconnect__uint8_tP"></a> <a id="bk__dm__a2dp_8h_1a55b454c848c5ae66dbabf98e63c2c966"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_source\_disconnect(uint8\_t \*addr)
:   Disconnect from the remote A2DP sink device. This API must be called after bk\_bt\_a2dp\_source\_init()

    参数
    :   **addr** – **\[in\]** remote bluetooth device address

    返回
    :   ```
                     - BK_ERR_BT_SUCCESS: connect request is sent to lower layer successfully
                     - others: fail
        ```

<a id="_CPPv418bk_a2dp_media_ctrl20bk_a2dp_media_ctrl_t"></a>

<a id="_CPPv318bk_a2dp_media_ctrl20bk_a2dp_media_ctrl_t"></a> <a id="_CPPv218bk_a2dp_media_ctrl20bk_a2dp_media_ctrl_t"></a> <a id="bk_a2dp_media_ctrl__bk_a2dp_media_ctrl_t"></a> <a id="bk__dm__a2dp_8h_1a359bea2bba78df5a7a86e19ce45cf922"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_a2dp\_media\_ctrl([bk\_a2dp\_media\_ctrl\_t](#_CPPv420bk_a2dp_media_ctrl_t "bk_a2dp_media_ctrl_t") ctrl)
:   Media control commands. This API can be used for both A2DP sink and must be called after bk\_bt\_a2dp\_source\_init()

    **Attention**
    :   this function only used for a2dp source

    参数
    :   **ctrl** – **\[in\]** control commands for A2DP action

    返回
    :   - BK\_ERR\_BT\_SUCCESS: control command is sent to lower layer successfully
        - others: fail

<a id="_CPPv420bk_bt_a2dp_sink_init7uint8_t"></a>

<a id="_CPPv320bk_bt_a2dp_sink_init7uint8_t"></a> <a id="_CPPv220bk_bt_a2dp_sink_init7uint8_t"></a> <a id="bk_bt_a2dp_sink_init__uint8_t"></a> <a id="bk__dm__a2dp_8h_1a134d9baea04522503520ffc4de2893f2"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_sink\_init(uint8\_t aac\_supported)
:   Initialize the bluetooth A2DP sink module.

    参数
    :   **aac\_supported** – **\[in\]** 1 means aac is supported, 0 means aac is not supported.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: the initialization request is successfully
        - others: fail

<a id="_CPPv422bk_bt_a2dp_sink_deinitv"></a>

<a id="_CPPv322bk_bt_a2dp_sink_deinitv"></a> <a id="_CPPv222bk_bt_a2dp_sink_deinitv"></a> <a id="bk_bt_a2dp_sink_deinit__void"></a> <a id="bk__dm__a2dp_8h_1afc63639812513bb4a51a2d5416a1ad94"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_sink\_deinit(void)
:   De-initialize for A2DP sink module. This function should be called only after bk\_bt\_a2dp\_sink\_init() completes successfully, and BK\_A2DP\_PROF\_STATE\_EVT will reported to APP layer.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: the deinitialization request is successfully
        - others: fail

<a id="_CPPv438bk_bt_a2dp_sink_register_data_callback20bk_bt_sink_data_cb_t"></a>

<a id="_CPPv338bk_bt_a2dp_sink_register_data_callback20bk_bt_sink_data_cb_t"></a> <a id="_CPPv238bk_bt_a2dp_sink_register_data_callback20bk_bt_sink_data_cb_t"></a> <a id="bk_bt_a2dp_sink_register_data_callback__bk_bt_sink_data_cb_t"></a> <a id="bk__dm__a2dp_8h_1adc785ae3d034f31e3036fa1abc201ce0"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_sink\_register\_data\_callback([bk\_bt\_sink\_data\_cb\_t](#_CPPv420bk_bt_sink_data_cb_t "bk_bt_sink_data_cb_t") callback)
:   Register A2DP sink data output function;.

    参数
    :   **callback** – **\[in\]** A2DP sink data callback function

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv423bk_bt_a2dp_sink_connectP7uint8_t"></a>

<a id="_CPPv323bk_bt_a2dp_sink_connectP7uint8_t"></a> <a id="_CPPv223bk_bt_a2dp_sink_connectP7uint8_t"></a> <a id="bk_bt_a2dp_sink_connect__uint8_tP"></a> <a id="bk__dm__a2dp_8h_1ad106a063945ecfc816f659dc756026dc"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_sink\_connect(uint8\_t \*remote\_bda)
:   Connect to remote bluetooth A2DP source device. This API must be called after bk\_bt\_a2dp\_sink\_init().

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv426bk_bt_a2dp_sink_disconnectP7uint8_t"></a>

<a id="_CPPv326bk_bt_a2dp_sink_disconnectP7uint8_t"></a> <a id="_CPPv226bk_bt_a2dp_sink_disconnectP7uint8_t"></a> <a id="bk_bt_a2dp_sink_disconnect__uint8_tP"></a> <a id="bk__dm__a2dp_8h_1a51a2a5f7bcded1a05d573e4e499d5a3d"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_sink\_disconnect(uint8\_t \*remote\_bda)
:   Disconnect from the remote A2DP source device. This API must be called after bk\_bt\_a2dp\_sink\_init().

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv431bk_bt_a2dp_sink_set_delay_value8uint16_t"></a>

<a id="_CPPv331bk_bt_a2dp_sink_set_delay_value8uint16_t"></a> <a id="_CPPv231bk_bt_a2dp_sink_set_delay_value8uint16_t"></a> <a id="bk_bt_a2dp_sink_set_delay_value__uint16_t"></a> <a id="bk__dm__a2dp_8h_1aca652f77c4a77e1176356b0be7c52b7f"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_sink\_set\_delay\_value(uint16\_t delay\_value)
:   Set delay reporting value.This API must be called after bk\_bt\_a2dp\_sink\_init().

    参数
    :   **delay\_value** – **\[in\]** reporting value is in 1/10 millisecond

    返回
    :   - BK\_ERR\_BT\_SUCCESS: delay value is sent to lower layer successfully
        - others: fail

<a id="_CPPv431bk_bt_a2dp_sink_get_delay_valuev"></a>

<a id="_CPPv331bk_bt_a2dp_sink_get_delay_valuev"></a> <a id="_CPPv231bk_bt_a2dp_sink_get_delay_valuev"></a> <a id="bk_bt_a2dp_sink_get_delay_value__void"></a> <a id="bk__dm__a2dp_8h_1a9aa25ebf2753e76ad2164f55921e8f50"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_sink\_get\_delay\_value(void)
:   Get delay reporting value. This API must be called after bk\_bt\_a2dp\_sink\_init().

    返回
    :   - BK\_ERR\_BT\_SUCCESS: if the request is sent successfully
        - others: fail

<a id="_CPPv418bk_bt_a2dp_set_cap7uint8_tP19bk_a2dp_codec_cap_t"></a>

<a id="_CPPv318bk_bt_a2dp_set_cap7uint8_tP19bk_a2dp_codec_cap_t"></a> <a id="_CPPv218bk_bt_a2dp_set_cap7uint8_tP19bk_a2dp_codec_cap_t"></a> <a id="bk_bt_a2dp_set_cap__uint8_t.bk_a2dp_codec_cap_tP"></a> <a id="bk__dm__a2dp_8h_1a91a43ce4d47b2e8690e93269a3890223"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_a2dp\_set\_cap(uint8\_t source\_or\_sink, [bk\_a2dp\_codec\_cap\_t](#_CPPv419bk_a2dp_codec_cap_t "bk_a2dp_codec_cap_t") \*cap)
:   set media cap. This API must be called after bk\_bt\_a2dp\_xxx\_init() and before connection completed

    参数
    :   - **source\_or\_sink** – **\[in\]** 0 source, 1 sink
        - **cap** – **\[in\]** media cap

    返回
    :   - BK\_ERR\_BT\_SUCCESS: if the request is sent successfully
        - others: fail

<a id="_CPPv432bk_a2dp_sink_offload_set_enabledb"></a>

<a id="_CPPv332bk_a2dp_sink_offload_set_enabledb"></a> <a id="_CPPv232bk_a2dp_sink_offload_set_enabledb"></a> <a id="bk_a2dp_sink_offload_set_enabled__b"></a> <a id="bk__dm__a2dp_8h_1a556fd96210d464ca16aff09638c57000"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_a2dp\_sink\_offload\_set\_enabled(bool en)
:   A2DP Sink Offload: enable/disable the feature at runtime.

    参数
    :   **en** – **\[in\]** true to enable / false to disable

    返回
    :   BK\_ERR\_BT\_SUCCESS on success; BK\_ERR\_BT\_BUSY if a session is active; others on fail.

<a id="_CPPv432bk_a2dp_sink_offload_get_enabledv"></a>

<a id="_CPPv332bk_a2dp_sink_offload_get_enabledv"></a> <a id="_CPPv232bk_a2dp_sink_offload_get_enabledv"></a> <a id="bk_a2dp_sink_offload_get_enabled__void"></a> <a id="bk__dm__a2dp_8h_1a54749df94e730e452990086fcbd7b895"></a> bool bk\_a2dp\_sink\_offload\_get\_enabled(void)
:   A2DP Sink Offload: read back the feature switch.

    返回
    :   true if enabled, else false.

<a id="_CPPv431bk_a2dp_sink_offload_set_volume7uint8_t"></a>

<a id="_CPPv331bk_a2dp_sink_offload_set_volume7uint8_t"></a> <a id="_CPPv231bk_a2dp_sink_offload_set_volume7uint8_t"></a> <a id="bk_a2dp_sink_offload_set_volume__uint8_t"></a> <a id="bk__dm__a2dp_8h_1a9e4249ba6409269cc5435c09622ba05b"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_a2dp\_sink\_offload\_set\_volume(uint8\_t vol)
:   A2DP Sink Offload: push AVRCP absolute volume to the CP.

    参数
    :   **vol** – **\[in\]** AVRCP absolute volume, 0\~127

    返回
    :   BK\_ERR\_BT\_SUCCESS on success; others on fail.

<a id="bk-dm-avrcp-h"></a>

## bk\_dm\_avrcp.h

`bk_dm_avrcp.h` 提供 AVRCP 控制器和目标端的媒体控制接口。

<a id="id6"></a>

### Header File

- [bk\_dm\_avrcp.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_avrcp.h)

<a id="id7"></a>

### Functions

<a id="_CPPv419bk_bt_avrcp_ct_initv"></a>

<a id="_CPPv319bk_bt_avrcp_ct_initv"></a> <a id="_CPPv219bk_bt_avrcp_ct_initv"></a> <a id="bk_bt_avrcp_ct_init__void"></a> <a id="group__dm__avrcp_1ga05f83b873d0086a261259a7523ea3e0f"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_init(void)
:   Initialize the bluetooth AVRCP controller module.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv421bk_bt_avrcp_ct_deinitv"></a>

<a id="_CPPv321bk_bt_avrcp_ct_deinitv"></a> <a id="_CPPv221bk_bt_avrcp_ct_deinitv"></a> <a id="bk_bt_avrcp_ct_deinit__void"></a> <a id="group__dm__avrcp_1ga9dcc948eeb6ada4e51a9f97499006377"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_deinit(void)
:   Deinitialize the bluetooth AVRCP controller module.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv432bk_bt_avrcp_ct_register_callback16bk_avrcp_ct_cb_t"></a>

<a id="_CPPv332bk_bt_avrcp_ct_register_callback16bk_avrcp_ct_cb_t"></a> <a id="_CPPv232bk_bt_avrcp_ct_register_callback16bk_avrcp_ct_cb_t"></a> <a id="bk_bt_avrcp_ct_register_callback__bk_avrcp_ct_cb_t"></a> <a id="group__dm__avrcp_1ga98b9a3d45af6f021d08b8a4634fcbe96"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_register\_callback([bk\_avrcp\_ct\_cb\_t](#_CPPv416bk_avrcp_ct_cb_t "bk_avrcp_ct_cb_t") callback)
:   Register application callbacks to AVRCP module.

    参数
    :   **callback** – **\[in\]** AVRCP controller callback function

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv443bk_bt_avrcp_ct_send_get_rn_capabilities_cmdP7uint8_t"></a>

<a id="_CPPv343bk_bt_avrcp_ct_send_get_rn_capabilities_cmdP7uint8_t"></a> <a id="_CPPv243bk_bt_avrcp_ct_send_get_rn_capabilities_cmdP7uint8_t"></a> <a id="bk_bt_avrcp_ct_send_get_rn_capabilities_cmd__uint8_tP"></a> <a id="group__dm__avrcp_1gaa0ae75204679264e619ecde057ab5ef8"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_send\_get\_rn\_capabilities\_cmd(uint8\_t \*remote\_bda)
:   Send GetCapabilities PDU to AVRCP target to retrieve remote device’s supported notification event\_ids. This function should be called after BK\_AVRCP\_CT\_CONNECTION\_STATE\_EVT is received and AVRCP connection is established.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv445bk_bt_avrcp_ct_send_register_notification_cmdP7uint8_t7uint8_t8uint32_t"></a>

<a id="_CPPv345bk_bt_avrcp_ct_send_register_notification_cmdP7uint8_t7uint8_t8uint32_t"></a> <a id="_CPPv245bk_bt_avrcp_ct_send_register_notification_cmdP7uint8_t7uint8_t8uint32_t"></a> <a id="bk_bt_avrcp_ct_send_register_notification_cmd__uint8_tP.uint8_t.uint32_t"></a> <a id="group__dm__avrcp_1ga77a5e528dc8926d747e4a1d1cd4e5782"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_send\_register\_notification\_cmd(uint8\_t \*remote\_bda, uint8\_t event\_id, uint32\_t event\_parameter)
:   Send register notification command to AVRCP target. This function should be called after BK\_AVRCP\_CT\_CONNECTION\_STATE\_EVT is received and AVRCP connection is established.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address
        - **event\_id** – **\[in\]** : id of events, e.g. BK\_AVRCP\_RN\_PLAY\_STATUS\_CHANGE, BK\_AVRCP\_RN\_TRACK\_CHANGE, etc.
        - **event\_parameter** – **\[in\]** : playback interval for BK\_AVRCP\_RN\_PLAY\_POS\_CHANGED in second; For other events , value of this parameter is ignored.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv435bk_bt_avrcp_ct_send_passthrough_cmdP7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv335bk_bt_avrcp_ct_send_passthrough_cmdP7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv235bk_bt_avrcp_ct_send_passthrough_cmdP7uint8_t7uint8_t7uint8_t"></a> <a id="bk_bt_avrcp_ct_send_passthrough_cmd__uint8_tP.uint8_t.uint8_t"></a> <a id="group__dm__avrcp_1ga1ae2337d958b6b0a4f5dc6722af52d67"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_send\_passthrough\_cmd(uint8\_t \*remote\_bda, uint8\_t key\_code, uint8\_t key\_state)
:   Send passthrough command to AVRCP target. This function should be called after BK\_AVRCP\_CT\_CONNECTION\_STATE\_EVT is received and AVRCP connection is established.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address.
        - **key\_code** – **\[in\]** : passthrough command code, e.g. BK\_AVRCP\_PT\_CMD\_PLAY, BK\_AVRCP\_PT\_CMD\_STOP, etc.
        - **key\_state** – **\[in\]** : passthrough command key state, BK\_AVRCP\_PT\_CMD\_STATE\_PRESSED or BK\_AVRCP\_PT\_CMD\_STATE\_RELEASED

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv439bk_bt_avrcp_ct_send_absolute_volume_cmdP7uint8_t7uint8_t"></a>

<a id="_CPPv339bk_bt_avrcp_ct_send_absolute_volume_cmdP7uint8_t7uint8_t"></a> <a id="_CPPv239bk_bt_avrcp_ct_send_absolute_volume_cmdP7uint8_t7uint8_t"></a> <a id="bk_bt_avrcp_ct_send_absolute_volume_cmd__uint8_tP.uint8_t"></a> <a id="group__dm__avrcp_1ga2ee3f0e14594f794b27ad6c7fe6df25d"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_send\_absolute\_volume\_cmd(uint8\_t \*remote\_bda, uint8\_t volume)
:   Send set absolute volume command to AVRCP target. This function should be called after BK\_AVRCP\_CT\_CONNECTION\_STATE\_EVT is received and AVRCP connection is established. if BK\_AVRCP\_SDP\_FEATURE\_CT\_CAT\_2 is not supported, this function shouldn’t be used.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address.
        - **volume** – **\[in\]** : volume, 0 to 0x7f, means 0% to 100%

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv446bk_bt_avrcp_ct_send_set_player_app_setting_cmdP7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv346bk_bt_avrcp_ct_send_set_player_app_setting_cmdP7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv246bk_bt_avrcp_ct_send_set_player_app_setting_cmdP7uint8_t7uint8_t7uint8_t"></a> <a id="bk_bt_avrcp_ct_send_set_player_app_setting_cmd__uint8_tP.uint8_t.uint8_t"></a> <a id="group__dm__avrcp_1ga81d068c5b94e3d2314fc5e5c8ed98c28"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_send\_set\_player\_app\_setting\_cmd(uint8\_t \*remote\_bda, uint8\_t attr\_id, uint8\_t value\_id)
:   Send player application settings command to AVRCP target. This function should be called after BK\_AVRCP\_CT\_CONNECTION\_STATE\_EVT is received and AVRCP connection is established.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address.
        - **attr\_id** – **\[in\]** : player application setting attribute IDs from one of bk\_avrcp\_ps\_attr\_ids\_t
        - **value\_id** – **\[in\]** : attribute value defined for the specific player application setting attribute

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv442bk_bt_avrcp_ct_send_get_elem_attribute_cmdP7uint8_t8uint32_t"></a>

<a id="_CPPv342bk_bt_avrcp_ct_send_get_elem_attribute_cmdP7uint8_t8uint32_t"></a> <a id="_CPPv242bk_bt_avrcp_ct_send_get_elem_attribute_cmdP7uint8_t8uint32_t"></a> <a id="bk_bt_avrcp_ct_send_get_elem_attribute_cmd__uint8_tP.uint32_t"></a> <a id="group__dm__avrcp_1gaabab7ac4c096394f5de95c751807d72f"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_send\_get\_elem\_attribute\_cmd(uint8\_t \*remote\_bda, uint32\_t media\_attr\_id\_mask)
:   Send get media attr command to AVRCP target. This function should be called after BK\_AVRCP\_CT\_CONNECTION\_STATE\_EVT is received and AVRCP connection is established.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address.
        - **media\_attr\_id\_mask** – **\[in\]** : mask of bk\_avrcp\_media\_attr\_id\_t, such as (1 \<\< BK\_AVRCP\_MEDIA\_ATTR\_ID\_TITLE) \| (1 \<\< BK\_AVRCP\_MEDIA\_ATTR\_ID\_ARTIST).

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv419bk_bt_avrcp_tg_initv"></a>

<a id="_CPPv319bk_bt_avrcp_tg_initv"></a> <a id="_CPPv219bk_bt_avrcp_tg_initv"></a> <a id="bk_bt_avrcp_tg_init__void"></a> <a id="group__dm__avrcp_1ga0f43a498c80b739f64c0bd8e8750e851"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_tg\_init(void)
:   Initialize the bluetooth AVRCP target module.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv421bk_bt_avrcp_tg_deinitv"></a>

<a id="_CPPv321bk_bt_avrcp_tg_deinitv"></a> <a id="_CPPv221bk_bt_avrcp_tg_deinitv"></a> <a id="bk_bt_avrcp_tg_deinit__void"></a> <a id="group__dm__avrcp_1ga9c881603be5f4304f893e200ecae26fc"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_tg\_deinit(void)
:   Deinitialize the bluetooth AVRCP target module.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv432bk_bt_avrcp_tg_register_callback16bk_avrcp_tg_cb_t"></a>

<a id="_CPPv332bk_bt_avrcp_tg_register_callback16bk_avrcp_tg_cb_t"></a> <a id="_CPPv232bk_bt_avrcp_tg_register_callback16bk_avrcp_tg_cb_t"></a> <a id="bk_bt_avrcp_tg_register_callback__bk_avrcp_tg_cb_t"></a> <a id="group__dm__avrcp_1ga6562799ebf8b35345a221329cc9c722a"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_tg\_register\_callback([bk\_avrcp\_tg\_cb\_t](#_CPPv416bk_avrcp_tg_cb_t "bk_avrcp_tg_cb_t") callback)
:   Register application callbacks to AVRCP target module.

    参数
    :   **callback** – **\[in\]** AVRCP target callback function

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv429bk_bt_avrcp_tg_get_rn_evt_cap28bk_avrcp_rn_cap_api_method_tP26bk_avrcp_rn_evt_cap_mask_t"></a>

<a id="_CPPv329bk_bt_avrcp_tg_get_rn_evt_cap28bk_avrcp_rn_cap_api_method_tP26bk_avrcp_rn_evt_cap_mask_t"></a> <a id="_CPPv229bk_bt_avrcp_tg_get_rn_evt_cap28bk_avrcp_rn_cap_api_method_tP26bk_avrcp_rn_evt_cap_mask_t"></a> <a id="bk_bt_avrcp_tg_get_rn_evt_cap__bk_avrcp_rn_cap_api_method_t.bk_avrcp_rn_evt_cap_mask_tP"></a> <a id="group__dm__avrcp_1gacb418fcfaaf7860d121af48e889eb728"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_tg\_get\_rn\_evt\_cap([bk\_avrcp\_rn\_cap\_api\_method\_t](#_CPPv428bk_avrcp_rn_cap_api_method_t "bk_avrcp_rn_cap_api_method_t") cap, [bk\_avrcp\_rn\_evt\_cap\_mask\_t](#_CPPv426bk_avrcp_rn_evt_cap_mask_t "bk_avrcp_rn_evt_cap_mask_t") \*evt\_set)
:   Get the requested event notification capabilies on local AVRC target. The capability is returned in a bit mask representation in evt\_set. This function should be called after bk\_avrcp\_tg\_init().

    For capability type “BK\_AVRCP\_RN\_CAP\_API\_METHOD\_ALLOWED, the retrieved event set is constant and it covers all of the notification events that can possibly be supported with current implementation.

    For capability type BK\_AVRCP\_RN\_CAP\_API\_METHOD\_CURRENT\_ENABLE, the event set covers the notification events selected to be supported under current configuration, The configuration can be changed using bk\_avrcp\_tg\_set\_rn\_evt\_cap().

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv429bk_bt_avrcp_tg_set_rn_evt_capPK26bk_avrcp_rn_evt_cap_mask_t"></a>

<a id="_CPPv329bk_bt_avrcp_tg_set_rn_evt_capPK26bk_avrcp_rn_evt_cap_mask_t"></a> <a id="_CPPv229bk_bt_avrcp_tg_set_rn_evt_capPK26bk_avrcp_rn_evt_cap_mask_t"></a> <a id="bk_bt_avrcp_tg_set_rn_evt_cap__bk_avrcp_rn_evt_cap_mask_tCP"></a> <a id="group__dm__avrcp_1ga3dac5bddfe848d8b63e1597dc36e5999"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_tg\_set\_rn\_evt\_cap(const [bk\_avrcp\_rn\_evt\_cap\_mask\_t](#_CPPv426bk_avrcp_rn_evt_cap_mask_t "bk_avrcp_rn_evt_cap_mask_t") \*evt\_set)
:   Set the event notification capabilities on local AVRCP target. The capability is given in a bit mask representation in evt\_set and must be a subset of allowed event IDs with current implementation. This function should be called after bk\_avrcp\_tg\_init().

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv437bk_bt_avrcp_rn_evt_bit_mask_operation22bk_avrcp_bit_mask_op_tP26bk_avrcp_rn_evt_cap_mask_t23bk_avrcp_rn_event_ids_t"></a>

<a id="_CPPv337bk_bt_avrcp_rn_evt_bit_mask_operation22bk_avrcp_bit_mask_op_tP26bk_avrcp_rn_evt_cap_mask_t23bk_avrcp_rn_event_ids_t"></a> <a id="_CPPv237bk_bt_avrcp_rn_evt_bit_mask_operation22bk_avrcp_bit_mask_op_tP26bk_avrcp_rn_evt_cap_mask_t23bk_avrcp_rn_event_ids_t"></a> <a id="bk_bt_avrcp_rn_evt_bit_mask_operation__bk_avrcp_bit_mask_op_t.bk_avrcp_rn_evt_cap_mask_tP.bk_avrcp_rn_event_ids_t"></a> <a id="group__dm__avrcp_1gaf37ed620c24631ee46a538a4c272d55a"></a> bool bk\_bt\_avrcp\_rn\_evt\_bit\_mask\_operation([bk\_avrcp\_bit\_mask\_op\_t](#_CPPv422bk_avrcp_bit_mask_op_t "bk_avrcp_bit_mask_op_t") op, [bk\_avrcp\_rn\_evt\_cap\_mask\_t](#_CPPv426bk_avrcp_rn_evt_cap_mask_t "bk_avrcp_rn_evt_cap_mask_t") \*events, [bk\_avrcp\_rn\_event\_ids\_t](#_CPPv423bk_avrcp_rn_event_ids_t "bk_avrcp_rn_event_ids_t") event\_id)
:   Operate on the type [bk\_avrcp\_rn\_evt\_cap\_mask\_t](#structbk__avrcp__rn__evt__cap__mask__t) with regard to a specific event.

    For operation BK\_AVRCP\_BIT\_MASK\_OP\_TEST, return true if the corresponding bit is set, otherwise false.

    参数
    :   - **op** – **\[in\]** operation requested on the bit mask field
        - **events** – **\[in\]** pointer to event notification capability bit mask structure
        - **event\_id** – **\[in\]** notification event code

    返回
    :   For operation BK\_AVRCP\_BIT\_MASK\_OP\_SET or BK\_AVRCP\_BIT\_MASK\_OP\_CLEAR, return true for a successful operation, otherwise return false.

<a id="_CPPv426bk_bt_avrcp_tg_send_rn_rspP7uint8_t23bk_avrcp_rn_event_ids_t17bk_avrcp_rn_rsp_tP19bk_avrcp_rn_param_t"></a>

<a id="_CPPv326bk_bt_avrcp_tg_send_rn_rspP7uint8_t23bk_avrcp_rn_event_ids_t17bk_avrcp_rn_rsp_tP19bk_avrcp_rn_param_t"></a> <a id="_CPPv226bk_bt_avrcp_tg_send_rn_rspP7uint8_t23bk_avrcp_rn_event_ids_t17bk_avrcp_rn_rsp_tP19bk_avrcp_rn_param_t"></a> <a id="bk_bt_avrcp_tg_send_rn_rsp__uint8_tP.bk_avrcp_rn_event_ids_t.bk_avrcp_rn_rsp_t.bk_avrcp_rn_param_tP"></a> <a id="group__dm__avrcp_1ga3afd14e8c63ae716f354592835a6228b"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_tg\_send\_rn\_rsp(uint8\_t \*addr, [bk\_avrcp\_rn\_event\_ids\_t](#_CPPv423bk_avrcp_rn_event_ids_t "bk_avrcp_rn_event_ids_t") event\_id, [bk\_avrcp\_rn\_rsp\_t](#_CPPv417bk_avrcp_rn_rsp_t "bk_avrcp_rn_rsp_t") rsp, [bk\_avrcp\_rn\_param\_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t") \*param)
:   Send RegisterNotification Response to remote AVRCP controller. Local event notification capability can be set using bk\_avrcp\_tg\_set\_rn\_evt\_cap(), in a bit mask representation in evt\_set. This function should be called after bk\_avrcp\_tg\_init().

    参数
    :   - **addr** – **\[in\]** peer addr
        - **event\_id** – **\[in\]** notification event ID that remote AVRCP CT registers
        - **rsp** – **\[in\]** notification response code
        - **param** – **\[in\]** parameters included in the specific notification

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv434bk_bt_avrcp_tg_get_psth_cmd_filter22bk_avrcp_psth_filter_tP24bk_avrcp_psth_bit_mask_t"></a>

<a id="_CPPv334bk_bt_avrcp_tg_get_psth_cmd_filter22bk_avrcp_psth_filter_tP24bk_avrcp_psth_bit_mask_t"></a> <a id="_CPPv234bk_bt_avrcp_tg_get_psth_cmd_filter22bk_avrcp_psth_filter_tP24bk_avrcp_psth_bit_mask_t"></a> <a id="bk_bt_avrcp_tg_get_psth_cmd_filter__bk_avrcp_psth_filter_t.bk_avrcp_psth_bit_mask_tP"></a> <a id="group__dm__avrcp_1ga0b28fe5943a876887a6175eb3fe8b747"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_tg\_get\_psth\_cmd\_filter([bk\_avrcp\_psth\_filter\_t](#_CPPv422bk_avrcp_psth_filter_t "bk_avrcp_psth_filter_t") filter, [bk\_avrcp\_psth\_bit\_mask\_t](#_CPPv424bk_avrcp_psth_bit_mask_t "bk_avrcp_psth_bit_mask_t") \*cmd\_set)
:   Get the current filter of remote passthrough commands on AVRC target. Filter is given by filter type and bit mask for the passthrough commands. This function should be called after [bk\_bt\_avrcp\_tg\_init()](#group__dm__avrcp_1ga0f43a498c80b739f64c0bd8e8750e851). For filter type BK\_AVRCP\_PSTH\_FILTER\_METHOD\_ALLOWED, the retrieved command set is constant and it covers all of the passthrough commands that can possibly be supported. For filter type BK\_AVRCP\_PSTH\_FILTER\_METHOD\_CURRENT\_ENABLE, the retrieved command set covers the passthrough commands selected to be supported according to current configuration. The configuration can be changed using [bk\_bt\_avrcp\_tg\_set\_psth\_cmd\_filter()](#group__dm__avrcp_1ga4f02fd8c38fd08c72e06a633cfdca1ad).

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv434bk_bt_avrcp_tg_set_psth_cmd_filter22bk_avrcp_psth_filter_tPK24bk_avrcp_psth_bit_mask_t"></a>

<a id="_CPPv334bk_bt_avrcp_tg_set_psth_cmd_filter22bk_avrcp_psth_filter_tPK24bk_avrcp_psth_bit_mask_t"></a> <a id="_CPPv234bk_bt_avrcp_tg_set_psth_cmd_filter22bk_avrcp_psth_filter_tPK24bk_avrcp_psth_bit_mask_t"></a> <a id="bk_bt_avrcp_tg_set_psth_cmd_filter__bk_avrcp_psth_filter_t.bk_avrcp_psth_bit_mask_tCP"></a> <a id="group__dm__avrcp_1ga4f02fd8c38fd08c72e06a633cfdca1ad"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_tg\_set\_psth\_cmd\_filter([bk\_avrcp\_psth\_filter\_t](#_CPPv422bk_avrcp_psth_filter_t "bk_avrcp_psth_filter_t") filter, const [bk\_avrcp\_psth\_bit\_mask\_t](#_CPPv424bk_avrcp_psth_bit_mask_t "bk_avrcp_psth_bit_mask_t") \*cmd\_set)
:   Set the filter of remote passthrough commands on AVRC target. Filter is given by filter type and bit mask for the passthrough commands. This function should be called after [bk\_bt\_avrcp\_tg\_init()](#group__dm__avrcp_1ga0f43a498c80b739f64c0bd8e8750e851).

    If filter type is BK\_AVRCP\_PSTH\_FILTER\_METHOD\_ALLOWED, the passthrough commands which are set “1” as given in cmd\_set will generate BK\_AVRCP\_CT\_PASSTHROUGH\_RSP\_EVT callback event and are auto-accepted in the protocol stack, other commands are replied with response type “NOT IMPLEMENTED” (8). The set of supported commands should be a subset of allowed command set. The allowed command set can be retrieved using [bk\_bt\_avrcp\_tg\_get\_psth\_cmd\_filter()](#group__dm__avrcp_1ga0b28fe5943a876887a6175eb3fe8b747) with filter type “BK\_AVRCP\_PSTH\_FILTER\_METHOD\_CURRENT\_ENABLE”.

    Filter type “BK\_AVRCP\_PSTH\_FILTER\_METHOD\_ALLOWED” does not apply to this function.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv435bk_bt_avrcp_psth_bit_mask_operation22bk_avrcp_bit_mask_op_tP24bk_avrcp_psth_bit_mask_t17bk_avrcp_pt_cmd_t"></a>

<a id="_CPPv335bk_bt_avrcp_psth_bit_mask_operation22bk_avrcp_bit_mask_op_tP24bk_avrcp_psth_bit_mask_t17bk_avrcp_pt_cmd_t"></a> <a id="_CPPv235bk_bt_avrcp_psth_bit_mask_operation22bk_avrcp_bit_mask_op_tP24bk_avrcp_psth_bit_mask_t17bk_avrcp_pt_cmd_t"></a> <a id="bk_bt_avrcp_psth_bit_mask_operation__bk_avrcp_bit_mask_op_t.bk_avrcp_psth_bit_mask_tP.bk_avrcp_pt_cmd_t"></a> <a id="group__dm__avrcp_1ga7568b142135f8498263e5427ef5e7077"></a> bool bk\_bt\_avrcp\_psth\_bit\_mask\_operation([bk\_avrcp\_bit\_mask\_op\_t](#_CPPv422bk_avrcp_bit_mask_op_t "bk_avrcp_bit_mask_op_t") op, [bk\_avrcp\_psth\_bit\_mask\_t](#_CPPv424bk_avrcp_psth_bit_mask_t "bk_avrcp_psth_bit_mask_t") \*psth, [bk\_avrcp\_pt\_cmd\_t](#_CPPv417bk_avrcp_pt_cmd_t "bk_avrcp_pt_cmd_t") cmd)
:   Operate on the type [bk\_avrcp\_psth\_bit\_mask\_t](#structbk__avrcp__psth__bit__mask__t) with regard to a specific PASSTHROUGH command.

    参数
    :   - **op** – **\[in\]** operation requested on the bit mask field
        - **psth** – **\[in\]** pointer to passthrough command bit mask structure
        - **cmd** – **\[in\]** passthrough command code

    返回
    :   For operation BK\_AVRCP\_BIT\_MASK\_OP\_SET or BK\_AVRCP\_BIT\_MASK\_OP\_CLEAR, return true for a successful operation, otherwise return false. For operation BK\_AVRCP\_BIT\_MASK\_OP\_TEST, return true if the corresponding bit is set, otherwise false.

<a id="_CPPv419bk_bt_avrcp_connectP7uint8_t"></a>

<a id="_CPPv319bk_bt_avrcp_connectP7uint8_t"></a> <a id="_CPPv219bk_bt_avrcp_connectP7uint8_t"></a> <a id="bk_bt_avrcp_connect__uint8_tP"></a> <a id="group__dm__avrcp_1ga172ff876d50e0f2d040b944845dfd44b"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_connect(uint8\_t \*remote\_bda)
:   Connect to remote bluetooth AVRCP. This API must be called after [bk\_bt\_avrcp\_ct\_init()](#group__dm__avrcp_1ga05f83b873d0086a261259a7523ea3e0f) or bk\_bt\_avrcp\_tg\_init.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv436bk_bt_avrcp_ct_sdp_feature_operation33bk_avrcp_sdp_feature_api_method_tP8uint16_t"></a>

<a id="_CPPv336bk_bt_avrcp_ct_sdp_feature_operation33bk_avrcp_sdp_feature_api_method_tP8uint16_t"></a> <a id="_CPPv236bk_bt_avrcp_ct_sdp_feature_operation33bk_avrcp_sdp_feature_api_method_tP8uint16_t"></a> <a id="bk_bt_avrcp_ct_sdp_feature_operation__bk_avrcp_sdp_feature_api_method_t.uint16_tP"></a> <a id="group__dm__avrcp_1ga7f2935b47a935cfb69b726021190f498"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_ct\_sdp\_feature\_operation([bk\_avrcp\_sdp\_feature\_api\_method\_t](#_CPPv433bk_avrcp_sdp_feature_api_method_t "bk_avrcp_sdp_feature_api_method_t") method, uint16\_t \*feat)
:   config ct sdp feature. This function must be done before any avrcp connection.

    参数
    :   - **method** – **\[in\]** operation
        - **\[in\|out\]** – feat: As output when method is BK\_AVRCP\_SDP\_FEATURE\_API\_METHOD\_GET\_XXX. As input when method is BK\_AVRCP\_SDP\_FEATURE\_API\_METHOD\_SET.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv436bk_bt_avrcp_tg_sdp_feature_operation33bk_avrcp_sdp_feature_api_method_tP8uint16_t"></a>

<a id="_CPPv336bk_bt_avrcp_tg_sdp_feature_operation33bk_avrcp_sdp_feature_api_method_tP8uint16_t"></a> <a id="_CPPv236bk_bt_avrcp_tg_sdp_feature_operation33bk_avrcp_sdp_feature_api_method_tP8uint16_t"></a> <a id="bk_bt_avrcp_tg_sdp_feature_operation__bk_avrcp_sdp_feature_api_method_t.uint16_tP"></a> <a id="group__dm__avrcp_1gaae3d3c5432eeff1329c44f6f89f2a14b"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_avrcp\_tg\_sdp\_feature\_operation([bk\_avrcp\_sdp\_feature\_api\_method\_t](#_CPPv433bk_avrcp_sdp_feature_api_method_t "bk_avrcp_sdp_feature_api_method_t") method, uint16\_t \*feat)
:   config tg sdp feature. This function must be done before any avrcp connection.

    参数
    :   - **method** – **\[in\]** operation
        - **\[in\|out\]** – feat: As output when method is BK\_AVRCP\_SDP\_FEATURE\_API\_METHOD\_GET\_XXX. As input when method is BK\_AVRCP\_SDP\_FEATURE\_API\_METHOD\_SET.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="bk-dm-hfp-h"></a>

## bk\_dm\_hfp.h

`bk_dm_hfp.h` 提供 HFP 免提通话、SCO 音频和 AT 交互接口。

<a id="id8"></a>

### Header File

- [bk\_dm\_hfp.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_hfp.h)

<a id="id9"></a>

### Functions

<a id="_CPPv433bk_bt_hf_client_register_callback20bk_bt_hf_client_cb_t"></a>

<a id="_CPPv333bk_bt_hf_client_register_callback20bk_bt_hf_client_cb_t"></a> <a id="_CPPv233bk_bt_hf_client_register_callback20bk_bt_hf_client_cb_t"></a> <a id="bk_bt_hf_client_register_callback__bk_bt_hf_client_cb_t"></a> <a id="bk__dm__hfp_8h_1a3383e8cead5fa53c5bff87e24c6a5bbd"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_register\_callback([bk\_bt\_hf\_client\_cb\_t](#_CPPv420bk_bt_hf_client_cb_t "bk_bt_hf_client_cb_t") callback)
:   Register application callback function to HFP client module.

    参数
    :   **callback** – **\[in\]** HFP client event callback function

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv420bk_bt_hf_client_init7uint8_t"></a>

<a id="_CPPv320bk_bt_hf_client_init7uint8_t"></a> <a id="_CPPv220bk_bt_hf_client_init7uint8_t"></a> <a id="bk_bt_hf_client_init__uint8_t"></a> <a id="bk__dm__hfp_8h_1a10b46524ccd07e86e4d061491c68cdcc"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_init(uint8\_t msbc\_supported)
:   Initialize the bluetooth HFP client module.

    参数
    :   **msbc\_supported** – **\[in\]** 1 means msbc is supported, 0 means msbc is not supported.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: the initialization request is successfully
        - others: fail

<a id="_CPPv422bk_bt_hf_client_deinitv"></a>

<a id="_CPPv322bk_bt_hf_client_deinitv"></a> <a id="_CPPv222bk_bt_hf_client_deinitv"></a> <a id="bk_bt_hf_client_deinit__void"></a> <a id="bk__dm__hfp_8h_1aa17022159ea19e431837cd2b17b7af34"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_deinit(void)
:   De-initialize for HFP client module.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail

<a id="_CPPv438bk_bt_hf_client_register_data_callback25bk_bt_hf_client_data_cb_t"></a>

<a id="_CPPv338bk_bt_hf_client_register_data_callback25bk_bt_hf_client_data_cb_t"></a> <a id="_CPPv238bk_bt_hf_client_register_data_callback25bk_bt_hf_client_data_cb_t"></a> <a id="bk_bt_hf_client_register_data_callback__bk_bt_hf_client_data_cb_t"></a> <a id="bk__dm__hfp_8h_1ad1430efcaf04eea36b54f4121d2ee372"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_register\_data\_callback([bk\_bt\_hf\_client\_data\_cb\_t](#_CPPv425bk_bt_hf_client_data_cb_t "bk_bt_hf_client_data_cb_t") callback)
:   Register HFP client data input function;.

    参数
    :   **callback** – **\[in\]** HFP client incoming data callback function

    返回
    :   - BK\_ERR\_BT\_SUCCESS: the initialization request is successfully
        - others: fail

<a id="_CPPv431bk_bt_hf_client_voice_out_writeP7uint8_tP7uint8_t8uint16_t"></a>

<a id="_CPPv331bk_bt_hf_client_voice_out_writeP7uint8_tP7uint8_t8uint16_t"></a> <a id="_CPPv231bk_bt_hf_client_voice_out_writeP7uint8_tP7uint8_t8uint16_t"></a> <a id="bk_bt_hf_client_voice_out_write__uint8_tP.uint8_tP.uint16_t"></a> <a id="bk__dm__hfp_8h_1ae1ac1aa80bab355d71f28e4cb1b796d2"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_voice\_out\_write(uint8\_t \*remote\_bda, uint8\_t \*buf, uint16\_t len)
:   Send voice data to HFP AG;.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address
        - **buf** – **\[in\]** : pointer to the data
        - **len** – **\[in\]** : size(in bytes) in buf

    返回
    :   - BK\_ERR\_BT\_SUCCESS: the initialization request is successfully
        - others: fail

<a id="_CPPv423bk_bt_hf_client_connectP7uint8_t"></a>

<a id="_CPPv323bk_bt_hf_client_connectP7uint8_t"></a> <a id="_CPPv223bk_bt_hf_client_connectP7uint8_t"></a> <a id="bk_bt_hf_client_connect__uint8_tP"></a> <a id="bk__dm__hfp_8h_1a1c27d50ce2032aa2ac2d02a5ba857b05"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_connect(uint8\_t \*remote\_bda)
:   Establish a Service Level Connection to remote bluetooth HFP audio gateway(AG) device. This function must be called after bk\_bt\_hf\_client\_init().

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: connect request is sent to lower layer
        - others: fail

<a id="_CPPv426bk_bt_hf_client_disconnectP7uint8_t"></a>

<a id="_CPPv326bk_bt_hf_client_disconnectP7uint8_t"></a> <a id="_CPPv226bk_bt_hf_client_disconnectP7uint8_t"></a> <a id="bk_bt_hf_client_disconnect__uint8_tP"></a> <a id="bk__dm__hfp_8h_1abcc797e1c569dbe8513dda427e6c9ca1"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_disconnect(uint8\_t \*remote\_bda)
:   Disconnect from the remote HFP audio gateway. This function must be called after bk\_bt\_hf\_client\_init().

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: connect request is sent to lower layer
        - others: fail

<a id="_CPPv429bk_bt_hf_client_connect_audioP7uint8_t"></a>

<a id="_CPPv329bk_bt_hf_client_connect_audioP7uint8_t"></a> <a id="_CPPv229bk_bt_hf_client_connect_audioP7uint8_t"></a> <a id="bk_bt_hf_client_connect_audio__uint8_tP"></a> <a id="bk__dm__hfp_8h_1ae91953dca86b357a7a09ec4bb13c6e55"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_connect\_audio(uint8\_t \*remote\_bda)
:   Create audio connection with remote HFP AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: connect request is sent to lower layer
        - others: fail

<a id="_CPPv432bk_bt_hf_client_disconnect_audioP7uint8_t"></a>

<a id="_CPPv332bk_bt_hf_client_disconnect_audioP7uint8_t"></a> <a id="_CPPv232bk_bt_hf_client_disconnect_audioP7uint8_t"></a> <a id="bk_bt_hf_client_disconnect_audio__uint8_tP"></a> <a id="bk__dm__hfp_8h_1a64a34ae81121dd410ec1a884b6b5ddf5"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_disconnect\_audio(uint8\_t \*remote\_bda)
:   Release the established audio connection with remote HFP AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: disconnect request is sent to lower layer
        - others: fail

<a id="_CPPv439bk_bt_hf_client_start_voice_recognitionP7uint8_t"></a>

<a id="_CPPv339bk_bt_hf_client_start_voice_recognitionP7uint8_t"></a> <a id="_CPPv239bk_bt_hf_client_start_voice_recognitionP7uint8_t"></a> <a id="bk_bt_hf_client_start_voice_recognition__uint8_tP"></a> <a id="bk__dm__hfp_8h_1a2dd2ee2f4c74fd56a52d768989b2b3ec"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_start\_voice\_recognition(uint8\_t \*remote\_bda)
:   Enable voice recognition in the AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv438bk_bt_hf_client_stop_voice_recognitionP7uint8_t"></a>

<a id="_CPPv338bk_bt_hf_client_stop_voice_recognitionP7uint8_t"></a> <a id="_CPPv238bk_bt_hf_client_stop_voice_recognitionP7uint8_t"></a> <a id="bk_bt_hf_client_stop_voice_recognition__uint8_tP"></a> <a id="bk__dm__hfp_8h_1a981f554d760640a92e8543910ac5f52b"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_stop\_voice\_recognition(uint8\_t \*remote\_bda)
:   Disable voice recognition in the AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv429bk_bt_hf_client_volume_updateP7uint8_t29bk_hf_volume_control_target_t7uint8_t"></a>

<a id="_CPPv329bk_bt_hf_client_volume_updateP7uint8_t29bk_hf_volume_control_target_t7uint8_t"></a> <a id="_CPPv229bk_bt_hf_client_volume_updateP7uint8_t29bk_hf_volume_control_target_t7uint8_t"></a> <a id="bk_bt_hf_client_volume_update__uint8_tP.bk_hf_volume_control_target_t.uint8_t"></a> <a id="bk__dm__hfp_8h_1aadd872b5aa01baaf2aedcdb4c14a8a7b"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_volume\_update(uint8\_t \*remote\_bda, bk\_hf\_volume\_control\_target\_t type, uint8\_t volume)
:   Volume synchronization with AG. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address
        - **type** – **\[in\]** volume control target, speaker or microphone
        - **volume** – **\[in\]** gain of the speaker of microphone, ranges 0 to 15

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv420bk_bt_hf_client_dialP7uint8_tPKc"></a>

<a id="_CPPv320bk_bt_hf_client_dialP7uint8_tPKc"></a> <a id="_CPPv220bk_bt_hf_client_dialP7uint8_tPKc"></a> <a id="bk_bt_hf_client_dial__uint8_tP.cCP"></a> <a id="bk__dm__hfp_8h_1a2f58366fb3b3ff715cc7121b4ae86792"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_dial(uint8\_t \*remote\_bda, const char \*number)
:   Place a call with a specified number, if number is NULL, last called number is called. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address
        - **number** – **\[in\]** number string of the call. If NULL, the last number is called(aka re-dial)

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv427bk_bt_hf_client_dial_memoryP7uint8_ti"></a>

<a id="_CPPv327bk_bt_hf_client_dial_memoryP7uint8_ti"></a> <a id="_CPPv227bk_bt_hf_client_dial_memoryP7uint8_ti"></a> <a id="bk_bt_hf_client_dial_memory__uint8_tP.i"></a> <a id="bk__dm__hfp_8h_1a009709579b9cfca6eb0bffbed49ea849"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_dial\_memory(uint8\_t \*remote\_bda, int location)
:   Place a call with number specified by location(speed dial). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address
        - **location** – **\[in\]** location of the number in the memory

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv429bk_bt_hf_client_send_chld_cmdP7uint8_t17bk_hf_chld_type_t"></a>

<a id="_CPPv329bk_bt_hf_client_send_chld_cmdP7uint8_t17bk_hf_chld_type_t"></a> <a id="_CPPv229bk_bt_hf_client_send_chld_cmdP7uint8_t17bk_hf_chld_type_t"></a> <a id="bk_bt_hf_client_send_chld_cmd__uint8_tP.bk_hf_chld_type_t"></a> <a id="bk__dm__hfp_8h_1a1a5e7d43358b87af7349789d5816d8a6"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_send\_chld\_cmd(uint8\_t \*remote\_bda, bk\_hf\_chld\_type\_t chld)
:   Send call hold and multiparty commands(Use AT\+CHLD). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address
        - **chld** – **\[in\]** AT\+CHLD call hold and multiparty handling AT command.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv429bk_bt_hf_client_send_btrh_cmdP7uint8_t16bk_hf_btrh_cmd_t"></a>

<a id="_CPPv329bk_bt_hf_client_send_btrh_cmdP7uint8_t16bk_hf_btrh_cmd_t"></a> <a id="_CPPv229bk_bt_hf_client_send_btrh_cmdP7uint8_t16bk_hf_btrh_cmd_t"></a> <a id="bk_bt_hf_client_send_btrh_cmd__uint8_tP.bk_hf_btrh_cmd_t"></a> <a id="bk__dm__hfp_8h_1a4b964816509a2dc3c10392a1a2390381"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_send\_btrh\_cmd(uint8\_t \*remote\_bda, bk\_hf\_btrh\_cmd\_t btrh)
:   Send response and hold action command(Send AT\+BTRH command) As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address
        - **btrh** – **\[in\]** response and hold action to send

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv427bk_bt_hf_client_answer_callP7uint8_t"></a>

<a id="_CPPv327bk_bt_hf_client_answer_callP7uint8_t"></a> <a id="_CPPv227bk_bt_hf_client_answer_callP7uint8_t"></a> <a id="bk_bt_hf_client_answer_call__uint8_tP"></a> <a id="bk__dm__hfp_8h_1a04da482f9fcbfeb8f051fc113946e366"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_answer\_call(uint8\_t \*remote\_bda)
:   Answer an incoming call(send ATA command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv427bk_bt_hf_client_reject_callP7uint8_t"></a>

<a id="_CPPv327bk_bt_hf_client_reject_callP7uint8_t"></a> <a id="_CPPv227bk_bt_hf_client_reject_callP7uint8_t"></a> <a id="bk_bt_hf_client_reject_call__uint8_tP"></a> <a id="bk__dm__hfp_8h_1aae9bc42037b987304022af07a05941d7"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_reject\_call(uint8\_t \*remote\_bda)
:   Reject an incoming call(send AT\+CHUP command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv435bk_bt_hf_client_query_current_callsP7uint8_t"></a>

<a id="_CPPv335bk_bt_hf_client_query_current_callsP7uint8_t"></a> <a id="_CPPv235bk_bt_hf_client_query_current_callsP7uint8_t"></a> <a id="bk_bt_hf_client_query_current_calls__uint8_tP"></a> <a id="bk__dm__hfp_8h_1a1aedb0ad4dd3d343dd3618974cd3d6b5"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_query\_current\_calls(uint8\_t \*remote\_bda)
:   Query list of current calls in AG(send AT\+CLCC command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv443bk_bt_hf_client_query_current_operator_nameP7uint8_t"></a>

<a id="_CPPv343bk_bt_hf_client_query_current_operator_nameP7uint8_t"></a> <a id="_CPPv243bk_bt_hf_client_query_current_operator_nameP7uint8_t"></a> <a id="bk_bt_hf_client_query_current_operator_name__uint8_tP"></a> <a id="bk__dm__hfp_8h_1ad910e6cec3a24655a728bb3d2f696a5c"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_query\_current\_operator\_name(uint8\_t \*remote\_bda)
:   Query the name of currently selected network operator in AG(use AT\+COPS commands). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv440bk_bt_hf_client_retrieve_subscriber_infoP7uint8_t"></a>

<a id="_CPPv340bk_bt_hf_client_retrieve_subscriber_infoP7uint8_t"></a> <a id="_CPPv240bk_bt_hf_client_retrieve_subscriber_infoP7uint8_t"></a> <a id="bk_bt_hf_client_retrieve_subscriber_info__uint8_tP"></a> <a id="bk__dm__hfp_8h_1a134e0c1d111b35a4f896ca59bd19ab47"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_retrieve\_subscriber\_info(uint8\_t \*remote\_bda)
:   Get subscriber information number from AG(send AT\+CNUM command) As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv425bk_bt_hf_client_send_dtmfP7uint8_tPKc"></a>

<a id="_CPPv325bk_bt_hf_client_send_dtmfP7uint8_tPKc"></a> <a id="_CPPv225bk_bt_hf_client_send_dtmfP7uint8_tPKc"></a> <a id="bk_bt_hf_client_send_dtmf__uint8_tP.cCP"></a> <a id="bk__dm__hfp_8h_1add427eb4cc244f17bf4589ba53065542"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_send\_dtmf(uint8\_t \*remote\_bda, const char \*code)
:   Transmit DTMF codes during an ongoing call(use AT\+VTS commands) As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address
        - **code** – **\[in\]** string of the dtmf code

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv445bk_bt_hf_client_request_last_voice_tag_numberP7uint8_t"></a>

<a id="_CPPv345bk_bt_hf_client_request_last_voice_tag_numberP7uint8_t"></a> <a id="_CPPv245bk_bt_hf_client_request_last_voice_tag_numberP7uint8_t"></a> <a id="bk_bt_hf_client_request_last_voice_tag_number__uint8_tP"></a> <a id="bk__dm__hfp_8h_1af88406654d051256e4937bdfcf6499ab"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_request\_last\_voice\_tag\_number(uint8\_t \*remote\_bda)
:   Request a phone number from AG corresponding to last voice tag recorded (send AT\+BINP command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv425bk_bt_hf_client_send_nrecP7uint8_t"></a>

<a id="_CPPv325bk_bt_hf_client_send_nrecP7uint8_t"></a> <a id="_CPPv225bk_bt_hf_client_send_nrecP7uint8_t"></a> <a id="bk_bt_hf_client_send_nrec__uint8_tP"></a> <a id="bk__dm__hfp_8h_1a2ba1327b9007cf66779440a17d635244"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_send\_nrec(uint8\_t \*remote\_bda)
:   Disable echo cancellation and noise reduction in the AG (use AT\+NREC\=0 command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv422bk_bt_hf_client_redialP7uint8_t"></a>

<a id="_CPPv322bk_bt_hf_client_redialP7uint8_t"></a> <a id="_CPPv222bk_bt_hf_client_redialP7uint8_t"></a> <a id="bk_bt_hf_client_redial__uint8_tP"></a> <a id="bk__dm__hfp_8h_1a74b9376efe488e0348635ab0314730c9"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_redial(uint8\_t \*remote\_bda)
:   This API allows user to redial the last number dialed (use AT\+BLDN command). As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   **remote\_bda** – **\[in\]** remote bluetooth device address

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv431bk_bt_hf_client_send_custom_cmdP7uint8_tPKc"></a>

<a id="_CPPv331bk_bt_hf_client_send_custom_cmdP7uint8_tPKc"></a> <a id="_CPPv231bk_bt_hf_client_send_custom_cmdP7uint8_tPKc"></a> <a id="bk_bt_hf_client_send_custom_cmd__uint8_tP.cCP"></a> <a id="bk__dm__hfp_8h_1a8d92b27dec7dd12dc3c227ce3ed27c69"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_hf\_client\_send\_custom\_cmd(uint8\_t \*remote\_bda, const char \*atcmd)
:   This API allows user to send custom AT Command. As a precondition to use this API, Service Level Connection shall exist with AG.

    参数
    :   - **remote\_bda** – **\[in\]** remote bluetooth device address
        - **atcmd** – **\[in\]** string of the custom atcmd.

    返回
    :   - BK\_ERR\_BT\_SUCCESS: request is sent to lower layer
        - others: fail

<a id="_CPPv430bk_hfp_sco_offload_set_enabledb"></a>

<a id="_CPPv330bk_hfp_sco_offload_set_enabledb"></a> <a id="_CPPv230bk_hfp_sco_offload_set_enabledb"></a> <a id="bk_hfp_sco_offload_set_enabled__b"></a> <a id="bk__dm__hfp_8h_1a42840c3f85944203890ecc0994840f7c"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_hfp\_sco\_offload\_set\_enabled(bool en)
:   HFP SCO Offload: enable/disable the full-duplex voice offload to CP at runtime. When enabled, the host starts/stops the offload itself on SCO connect/disconnect and the HFP service forwards \+VGS and suppresses the AP host audio path, so the application stays offload-agnostic.

    参数
    :   **en** – **\[in\]** true to enable / false to disable

    返回
    :   BK\_ERR\_BT\_SUCCESS on success; BK\_ERR\_BT\_BUSY if a session is active; others on fail.

<a id="_CPPv430bk_hfp_sco_offload_get_enabledv"></a>

<a id="_CPPv330bk_hfp_sco_offload_get_enabledv"></a> <a id="_CPPv230bk_hfp_sco_offload_get_enabledv"></a> <a id="bk_hfp_sco_offload_get_enabled__void"></a> <a id="bk__dm__hfp_8h_1a0934e8de0b1e329109b5cdb40c3e6b33"></a> bool bk\_hfp\_sco\_offload\_get\_enabled(void)
:   HFP SCO Offload: read back the feature switch.

    返回
    :   true if enabled, else false.

<a id="_CPPv429bk_hfp_sco_offload_set_volume7uint8_t"></a>

<a id="_CPPv329bk_hfp_sco_offload_set_volume7uint8_t"></a> <a id="_CPPv229bk_hfp_sco_offload_set_volume7uint8_t"></a> <a id="bk_hfp_sco_offload_set_volume__uint8_t"></a> <a id="bk__dm__hfp_8h_1a0c670681afa7c0187ca0f9b7480f4720"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_hfp\_sco\_offload\_set\_volume(uint8\_t vgs)
:   HFP SCO Offload: push HFP speaker volume (\+VGS) to the CP. Driven by the HFP service on \+VGS when offload is enabled.

    参数
    :   **vgs** – **\[in\]** HFP \+VGS speaker gain, 0\~15

    返回
    :   BK\_ERR\_BT\_SUCCESS on success; others on fail.

<a id="bk-dm-hidd-h"></a>

## bk\_dm\_hidd.h

`bk_dm_hidd.h` 提供 Bluetooth HID Device profile 接口。

<a id="id10"></a>

### Header File

- [bk\_dm\_hidd.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_hidd.h)

<a id="id11"></a>

### Functions

<a id="_CPPv434bk_bt_hid_device_register_callback10bk_hd_cb_t"></a>

<a id="_CPPv334bk_bt_hid_device_register_callback10bk_hd_cb_t"></a> <a id="_CPPv234bk_bt_hid_device_register_callback10bk_hd_cb_t"></a> <a id="bk_bt_hid_device_register_callback__bk_hd_cb_t"></a> <a id="bk__dm__hidd_8h_1a512dd353f045c1a2e663618f37a6f898"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_register\_callback([bk\_hd\_cb\_t](#_CPPv410bk_hd_cb_t "bk_hd_cb_t") callback)
:   This function is called to init callbacks with HID device module.

    参数
    :   **callback** – **\[in\]** pointer to the init callback function.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv421bk_bt_hid_device_initv"></a>

<a id="_CPPv321bk_bt_hid_device_initv"></a> <a id="_CPPv221bk_bt_hid_device_initv"></a> <a id="bk_bt_hid_device_init__void"></a> <a id="bk__dm__hidd_8h_1af89f6d73feadb573325d6b908b518d79"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_init(void)
:   Initializes HIDD interface. This function should be called after bk\_bluedroid\_init() and bk\_bluedroid\_enable() success, and should be called after bk\_bt\_hid\_device\_register\_callback. When the operation is complete, the callback function will be called with BK\_HIDD\_INIT\_EVT.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv423bk_bt_hid_device_deinitv"></a>

<a id="_CPPv323bk_bt_hid_device_deinitv"></a> <a id="_CPPv223bk_bt_hid_device_deinitv"></a> <a id="bk_bt_hid_device_deinit__void"></a> <a id="bk__dm__hidd_8h_1a62bd981c93b478f42ab21477e4bcb771"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_deinit(void)
:   De-initializes HIDD interface. This function should be called after bk\_bluedroid\_init() and bk\_bluedroid\_enable() success, and should be called after bk\_bt\_hid\_device\_init(). When the operation is complete, the callback function will be called with BK\_HIDD\_DEINIT\_EVT.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv429bk_bt_hid_device_register_appP19bk_hidd_app_param_t"></a>

<a id="_CPPv329bk_bt_hid_device_register_appP19bk_hidd_app_param_t"></a> <a id="_CPPv229bk_bt_hid_device_register_appP19bk_hidd_app_param_t"></a> <a id="bk_bt_hid_device_register_app__bk_hidd_app_param_tP"></a> <a id="bk__dm__hidd_8h_1aaf7bf4786439e9d83a058635c5ea1cb8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_register\_app([bk\_hidd\_app\_param\_t](#_CPPv419bk_hidd_app_param_t "bk_hidd_app_param_t") \*app\_param)
:   Registers HIDD parameters with SDP and sets l2cap Quality of Service. This function should be called after [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2) success, and should be called after bk\_bt\_hid\_device\_init(). When the operation is complete, the callback function will be called with BK\_HIDD\_REGISTER\_APP\_EVT.

    参数
    :   **app\_param** – **\[in\]** HIDD parameters

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv431bk_bt_hid_device_unregister_appv"></a>

<a id="_CPPv331bk_bt_hid_device_unregister_appv"></a> <a id="_CPPv231bk_bt_hid_device_unregister_appv"></a> <a id="bk_bt_hid_device_unregister_app__void"></a> <a id="bk__dm__hidd_8h_1acf180057dc7a80f740f1cdd87864793d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_unregister\_app(void)
:   Removes HIDD parameters from SDP and resets l2cap Quality of Service. This function should be called after [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2) success, and should be called after bk\_bt\_hid\_device\_init(). When the operation is complete, the callback function will be called with BK\_HIDD\_UNREGISTER\_APP\_EVT.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv424bk_bt_hid_device_connect12bk_bd_addr_t"></a>

<a id="_CPPv324bk_bt_hid_device_connect12bk_bd_addr_t"></a> <a id="_CPPv224bk_bt_hid_device_connect12bk_bd_addr_t"></a> <a id="bk_bt_hid_device_connect__bk_bd_addr_t"></a> <a id="bk__dm__hidd_8h_1a0a55d0669d985e764424f50e31782351"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_connect([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   Connects to the peer HID Host with virtual cable. This function should be called after [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2) success, and should be called after bk\_bt\_hid\_device\_init(). When the operation is complete, the callback function will be called with BK\_HIDD\_OPEN\_EVT.

    参数
    :   **bd\_addr** – **\[in\]** Remote host bluetooth device address.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv427bk_bt_hid_device_disconnectv"></a>

<a id="_CPPv327bk_bt_hid_device_disconnectv"></a> <a id="_CPPv227bk_bt_hid_device_disconnectv"></a> <a id="bk_bt_hid_device_disconnect__void"></a> <a id="bk__dm__hidd_8h_1af65b672ad19f949654f34f8e41a45a8d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_disconnect(void)
:   Disconnects from the currently connected HID Host. This function should be called after [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2) success, and should be called after bk\_bt\_hid\_device\_init(). When the operation is complete, the callback function will be called with BK\_HIDD\_CLOSE\_EVT.

    备注

    The disconnect operation will not remove the virtually cabled device. If the connect request from the different HID Host, it will reject the request.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv428bk_bt_hid_device_send_report8uint16_tP7uint8_t"></a>

<a id="_CPPv328bk_bt_hid_device_send_report8uint16_tP7uint8_t"></a> <a id="_CPPv228bk_bt_hid_device_send_report8uint16_tP7uint8_t"></a> <a id="bk_bt_hid_device_send_report__uint16_t.uint8_tP"></a> <a id="bk__dm__hidd_8h_1a2cfc79873992a8beb5a3a6d7d720d34d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_send\_report(uint16\_t len, uint8\_t \*data)
:   Sends HID report to the currently connected HID Host. This function should be called after [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2) success, and should be called after bk\_bt\_hid\_device\_init(). When the operation is complete, the callback function will be called with BK\_HIDD\_SEND\_REPORT\_EVT.

    参数
    :   - **len** – **\[in\]** length of report
        - **data** – **\[in\]** report data

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv430bk_bt_hid_device_send_response7uint8_t7uint8_t8uint16_tP7uint8_t"></a>

<a id="_CPPv330bk_bt_hid_device_send_response7uint8_t7uint8_t8uint16_tP7uint8_t"></a> <a id="_CPPv230bk_bt_hid_device_send_response7uint8_t7uint8_t8uint16_tP7uint8_t"></a> <a id="bk_bt_hid_device_send_response__uint8_t.uint8_t.uint16_t.uint8_tP"></a> <a id="bk__dm__hidd_8h_1abe73c89d4f24398dc767c3659ce091fb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_send\_response(uint8\_t message\_type, uint8\_t res\_status, uint16\_t len, uint8\_t \*data)
:   Sends HID Handshake with error info for invalid set\_report to the currently connected HID Host. This function should be called after [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2) success, and should be called after bk\_bt\_hid\_device\_init(). When the operation is complete, the callback function will be called with BK\_HIDD\_REPORT\_ERR\_EVT.

    参数
    :   - **message\_type** – **\[in\]** type of hid message
        - **res\_status** – **\[in\]** response status
        - **len** – **\[in\]** response data len
        - **data** – **\[in\]** response data

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv437bk_bt_hid_device_virtual_cable_unplugv"></a>

<a id="_CPPv337bk_bt_hid_device_virtual_cable_unplugv"></a> <a id="_CPPv237bk_bt_hid_device_virtual_cable_unplugv"></a> <a id="bk_bt_hid_device_virtual_cable_unplug__void"></a> <a id="bk__dm__hidd_8h_1a513b74209644ee30441d3031e782e0c4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_device\_virtual\_cable\_unplug(void)
:   Remove the virtually cabled device. This function should be called after [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2) success, and should be called after bk\_bt\_hid\_device\_init(). When the operation is complete, the callback function will be called with BK\_HIDD\_VC\_UNPLUG\_EVT.

    备注

    If the connection exists, then HID Device will send a `VIRTUAL_CABLE_UNPLUG` control command to the peer HID Host, and the connection will be destroyed. If the connection does not exist, then HID Device will only unplug on it’s single side. Once the unplug operation is success, the related pairing and bonding information will be removed, then the HID Device can accept connection request from the different HID Host,

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="unions"></a>

### Unions

<a id="_CPPv418bk_hidd_cb_param_t"></a>

<a id="_CPPv318bk_hidd_cb_param_t"></a> <a id="_CPPv218bk_hidd_cb_param_t"></a> <a id="unionbk__hidd__cb__param__t"></a> union bk\_hidd\_cb\_param\_t
:   *#include \<bk\_dm\_hidd.h\>*

    HID device callback parameters union.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_hidd_cb_param_t4initE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t4initE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t4initE"></a> <a id="bk_hidd_cb_param_t::init__bk_hidd_cb_param_t::hidd_init_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1a20834fa456a773dccae7372410a51a20"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_init\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t19hidd_init_evt_paramE "bk_hidd_cb_param_t::hidd_init_evt_param") init
    :   HIDD callback param of BK\_HIDD\_INIT\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t6deinitE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t6deinitE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t6deinitE"></a> <a id="bk_hidd_cb_param_t::deinit__bk_hidd_cb_param_t::hidd_deinit_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1acd67038ac1854559bac5625d3629b7bf"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_deinit\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t21hidd_deinit_evt_paramE "bk_hidd_cb_param_t::hidd_deinit_evt_param") deinit
    :   HIDD callback param of BK\_HIDD\_DEINIT\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t12register_appE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t12register_appE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t12register_appE"></a> <a id="bk_hidd_cb_param_t::register_app__bk_hidd_cb_param_t::hidd_register_app_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1ab5b485aed9f00100cc2f97283d390a69"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_register\_app\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t27hidd_register_app_evt_paramE "bk_hidd_cb_param_t::hidd_register_app_evt_param") register\_app
    :   HIDD callback param of BK\_HIDD\_REGISTER\_APP\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t14unregister_appE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t14unregister_appE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t14unregister_appE"></a> <a id="bk_hidd_cb_param_t::unregister_app__bk_hidd_cb_param_t::hidd_unregister_app_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1a6c16b32b2e3c356956b8434aad0c2c8e"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_unregister\_app\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t29hidd_unregister_app_evt_paramE "bk_hidd_cb_param_t::hidd_unregister_app_evt_param") unregister\_app
    :   HIDD callback param of BK\_HIDD\_UNREGISTER\_APP\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t4openE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t4openE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t4openE"></a> <a id="bk_hidd_cb_param_t::open__bk_hidd_cb_param_t::hidd_open_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1adcaeb1a8a3142c4970d4df31d139842b"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_open\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t19hidd_open_evt_paramE "bk_hidd_cb_param_t::hidd_open_evt_param") open
    :   HIDD callback param of BK\_HIDD\_OPEN\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t5closeE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t5closeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t5closeE"></a> <a id="bk_hidd_cb_param_t::close__bk_hidd_cb_param_t::hidd_close_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1a65afcd8973200f6e644af8e2ecce6b89"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_close\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t20hidd_close_evt_paramE "bk_hidd_cb_param_t::hidd_close_evt_param") close
    :   HIDD callback param of BK\_HIDD\_CLOSE\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t11send_reportE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t11send_reportE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t11send_reportE"></a> <a id="bk_hidd_cb_param_t::send_report__bk_hidd_cb_param_t::hidd_send_report_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1af39512bcc19a4a793ad1a431fc299275"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_send\_report\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t26hidd_send_report_evt_paramE "bk_hidd_cb_param_t::hidd_send_report_evt_param") send\_report
    :   HIDD callback param of BK\_HIDD\_SEND\_REPORT\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t10report_errE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t10report_errE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t10report_errE"></a> <a id="bk_hidd_cb_param_t::report_err__bk_hidd_cb_param_t::hidd_report_err_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1a605fc0105ee911702016c5e620472025"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_report\_err\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t25hidd_report_err_evt_paramE "bk_hidd_cb_param_t::hidd_report_err_evt_param") report\_err
    :   HIDD callback param of BK\_HIDD\_REPORT\_ERR\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t10get_reportE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t10get_reportE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t10get_reportE"></a> <a id="bk_hidd_cb_param_t::get_report__bk_hidd_cb_param_t::hidd_get_report_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1ab4d50841b451b1bc4230bddd785c0330"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_get\_report\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t25hidd_get_report_evt_paramE "bk_hidd_cb_param_t::hidd_get_report_evt_param") get\_report
    :   HIDD callback param of BK\_HIDD\_GET\_REPORT\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t10set_reportE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t10set_reportE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t10set_reportE"></a> <a id="bk_hidd_cb_param_t::set_report__bk_hidd_cb_param_t::hidd_set_report_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1a01bccd65616008c66cfe53a4da784a68"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_set\_report\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t25hidd_set_report_evt_paramE "bk_hidd_cb_param_t::hidd_set_report_evt_param") set\_report
    :   HIDD callback param of BK\_HIDD\_SET\_REPORT\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t12set_protocolE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t12set_protocolE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t12set_protocolE"></a> <a id="bk_hidd_cb_param_t::set_protocol__bk_hidd_cb_param_t::hidd_set_protocol_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1a5b1f4b09066a3d1bcdebd6717ca97779"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_set\_protocol\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t27hidd_set_protocol_evt_paramE "bk_hidd_cb_param_t::hidd_set_protocol_evt_param") set\_protocol
    :   HIDD callback param of BK\_HIDD\_SET\_PROTOCOL\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t12get_protocolE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t12get_protocolE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t12get_protocolE"></a> <a id="bk_hidd_cb_param_t::get_protocol__bk_hidd_cb_param_t::hidd_get_protocol_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1aafc3b7e2ae0dbc74cd75ba48a3e25594"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_get\_protocol\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t27hidd_get_protocol_evt_paramE "bk_hidd_cb_param_t::hidd_get_protocol_evt_param") get\_protocol
    :   HIDD callback param of BK\_HIDD\_GET\_PROTOCOL\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t8get_idleE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t8get_idleE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t8get_idleE"></a> <a id="bk_hidd_cb_param_t::get_idle__bk_hidd_cb_param_t::hidd_get_idle_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1a71ce4e7c1f19734c16e2f9e291c0c6da"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_get\_idle\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t23hidd_get_idle_evt_paramE "bk_hidd_cb_param_t::hidd_get_idle_evt_param") get\_idle
    :   HIDD callback param of BK\_HIDD\_GET\_IDLE\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t8set_idleE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t8set_idleE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t8set_idleE"></a> <a id="bk_hidd_cb_param_t::set_idle__bk_hidd_cb_param_t::hidd_set_idle_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1a67ed1fadcaa52e3cbfec00ec33e0d8c2"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_set\_idle\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t23hidd_set_idle_evt_paramE "bk_hidd_cb_param_t::hidd_set_idle_evt_param") set\_idle
    :   HIDD callback param of BK\_HIDD\_SET\_IDLE\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t9intr_dataE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t9intr_dataE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t9intr_dataE"></a> <a id="bk_hidd_cb_param_t::intr_data__bk_hidd_cb_param_t::hidd_intr_data_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1a91ade0cb488905961527427b1bdfa8e1"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_intr\_data\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t24hidd_intr_data_evt_paramE "bk_hidd_cb_param_t::hidd_intr_data_evt_param") intr\_data
    :   HIDD callback param of BK\_HIDD\_INTR\_DATA\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t7ctrl_opE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t7ctrl_opE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t7ctrl_opE"></a> <a id="bk_hidd_cb_param_t::ctrl_op__bk_hidd_cb_param_t::hidd_ctrl_op_evt_param"></a> <a id="unionbk__hidd__cb__param__t_1aad95361497d65f56ed9d78a45ec5eaf6"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_ctrl\_op\_evt\_param](#_CPPv4N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_paramE "bk_hidd_cb_param_t::hidd_ctrl_op_evt_param") ctrl\_op
    :   HIDD callback param of BK\_HIDD\_INTR\_DATA\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t9vc_unplugE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t9vc_unplugE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t9vc_unplugE"></a> <a id="bk_hidd_cb_param_t::vc_unplug__bk_hidd_cb_param_t::hidd_vc_unplug_param"></a> <a id="unionbk__hidd__cb__param__t_1ad03fbe8e2402d143989eb0157a503a54"></a> struct [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t")::[hidd\_vc\_unplug\_param](#_CPPv4N18bk_hidd_cb_param_t20hidd_vc_unplug_paramE "bk_hidd_cb_param_t::hidd_vc_unplug_param") vc\_unplug
    :   HIDD callback param of BK\_HIDD\_VC\_UNPLUG\_EVT

    <a id="_CPPv4N18bk_hidd_cb_param_t20hidd_close_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t20hidd_close_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t20hidd_close_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_close_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__close__evt__param"></a> struct hidd\_close\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_CLOSE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t20hidd_close_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t20hidd_close_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t20hidd_close_evt_param6statusE"></a> <a id="bk_hidd_cb_param_t::hidd_close_evt_param::status__bk_hidd_status_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__close__evt__param_1a53ecd2a8a0fe5da99221d1beaab692fa"></a> [bk\_hidd\_status\_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidd_cb_param_t20hidd_close_evt_param11conn_statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t20hidd_close_evt_param11conn_statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t20hidd_close_evt_param11conn_statusE"></a> <a id="bk_hidd_cb_param_t::hidd_close_evt_param::conn_status__bk_hidd_connection_state_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__close__evt__param_1a13381b95d5099d2f2595c86d03ca5e97"></a> [bk\_hidd\_connection\_state\_t](#_CPPv426bk_hidd_connection_state_t "bk_hidd_connection_state_t") conn\_status
        :   connection status

    <a id="_CPPv4N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_ctrl_op_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__ctrl__op__evt__param"></a> struct hidd\_ctrl\_op\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_CTRL\_OP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_param12message_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_param12message_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_param12message_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_ctrl_op_evt_param::message_type__bk_hidd_message_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__ctrl__op__evt__param_1ac96911714db6894feee208372d981b66"></a> [bk\_hidd\_message\_type\_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message\_type
        :   message type

        <a id="_CPPv4N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_param2opE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_param2opE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t22hidd_ctrl_op_evt_param2opE"></a> <a id="bk_hidd_cb_param_t::hidd_ctrl_op_evt_param::op__bk_hidd_ctrl_op_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__ctrl__op__evt__param_1a101d0a8573fd066659838648af3d92ef"></a> [bk\_hidd\_ctrl\_op\_t](#_CPPv417bk_hidd_ctrl_op_t "bk_hidd_ctrl_op_t") op
        :   ctral operation

    <a id="_CPPv4N18bk_hidd_cb_param_t21hidd_deinit_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t21hidd_deinit_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t21hidd_deinit_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_deinit_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__deinit__evt__param"></a> struct hidd\_deinit\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_DEINIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t21hidd_deinit_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t21hidd_deinit_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t21hidd_deinit_evt_param6statusE"></a> <a id="bk_hidd_cb_param_t::hidd_deinit_evt_param::status__bk_hidd_status_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__deinit__evt__param_1a92a236a9d4b1852c4c5495389d82955d"></a> [bk\_hidd\_status\_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

    <a id="_CPPv4N18bk_hidd_cb_param_t23hidd_get_idle_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t23hidd_get_idle_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t23hidd_get_idle_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_get_idle_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__get__idle__evt__param"></a> struct hidd\_get\_idle\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_GET\_IDLE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t23hidd_get_idle_evt_param12message_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t23hidd_get_idle_evt_param12message_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t23hidd_get_idle_evt_param12message_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_get_idle_evt_param::message_type__bk_hidd_message_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__get__idle__evt__param_1a8c44f63b28c510d7aa8be2fb91b27ec1"></a> [bk\_hidd\_message\_type\_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message\_type
        :   message type

    <a id="_CPPv4N18bk_hidd_cb_param_t27hidd_get_protocol_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t27hidd_get_protocol_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t27hidd_get_protocol_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_get_protocol_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__get__protocol__evt__param"></a> struct hidd\_get\_protocol\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_GET\_PROTOCOL\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t27hidd_get_protocol_evt_param12message_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t27hidd_get_protocol_evt_param12message_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t27hidd_get_protocol_evt_param12message_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_get_protocol_evt_param::message_type__bk_hidd_message_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__get__protocol__evt__param_1a7bd794156b7780c2a7b60d98f4ecb362"></a> [bk\_hidd\_message\_type\_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message\_type
        :   message type

    <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_get_report_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_get_report_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_get_report_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_get_report_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__get__report__evt__param"></a> struct hidd\_get\_report\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_GET\_REPORT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_get_report_evt_param12message_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_get_report_evt_param12message_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_get_report_evt_param12message_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_get_report_evt_param::message_type__bk_hidd_message_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__get__report__evt__param_1a26e87da8bc1920120618edbaa1baea3b"></a> [bk\_hidd\_message\_type\_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message\_type
        :   message type

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_get_report_evt_param11report_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_get_report_evt_param11report_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_get_report_evt_param11report_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_get_report_evt_param::report_type__bk_hidd_report_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__get__report__evt__param_1a12f761a17b8b3cae44b4896aa8785481"></a> [bk\_hidd\_report\_type\_t](#_CPPv421bk_hidd_report_type_t "bk_hidd_report_type_t") report\_type
        :   report type

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_get_report_evt_param9report_idE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_get_report_evt_param9report_idE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_get_report_evt_param9report_idE"></a> <a id="bk_hidd_cb_param_t::hidd_get_report_evt_param::report_id__uint8_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__get__report__evt__param_1aba06b4ae806f2ce04222843758004e69"></a> uint8\_t report\_id
        :   report id

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_get_report_evt_param11buffer_sizeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_get_report_evt_param11buffer_sizeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_get_report_evt_param11buffer_sizeE"></a> <a id="bk_hidd_cb_param_t::hidd_get_report_evt_param::buffer_size__uint16_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__get__report__evt__param_1a451711777bbe5aa0523dda539ee13240"></a> uint16\_t buffer\_size
        :   buffer size

    <a id="_CPPv4N18bk_hidd_cb_param_t19hidd_init_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t19hidd_init_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t19hidd_init_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_init_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__init__evt__param"></a> struct hidd\_init\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_INIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t19hidd_init_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t19hidd_init_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t19hidd_init_evt_param6statusE"></a> <a id="bk_hidd_cb_param_t::hidd_init_evt_param::status__bk_hidd_status_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__init__evt__param_1aade59888b6c9318c0ebb97108e6e26ef"></a> [bk\_hidd\_status\_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

    <a id="_CPPv4N18bk_hidd_cb_param_t24hidd_intr_data_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t24hidd_intr_data_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t24hidd_intr_data_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_intr_data_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__intr__data__evt__param"></a> struct hidd\_intr\_data\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_INTR\_DATA\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t24hidd_intr_data_evt_param12message_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t24hidd_intr_data_evt_param12message_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t24hidd_intr_data_evt_param12message_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_intr_data_evt_param::message_type__bk_hidd_message_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__intr__data__evt__param_1a7e6df51156f44ab47367b69f9e357b43"></a> [bk\_hidd\_message\_type\_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message\_type
        :   message type

        <a id="_CPPv4N18bk_hidd_cb_param_t24hidd_intr_data_evt_param11report_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t24hidd_intr_data_evt_param11report_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t24hidd_intr_data_evt_param11report_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_intr_data_evt_param::report_type__bk_hidd_report_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__intr__data__evt__param_1a3fde3202fa33027c91090b6698cff6bb"></a> [bk\_hidd\_report\_type\_t](#_CPPv421bk_hidd_report_type_t "bk_hidd_report_type_t") report\_type
        :   report type

        <a id="_CPPv4N18bk_hidd_cb_param_t24hidd_intr_data_evt_param9report_idE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t24hidd_intr_data_evt_param9report_idE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t24hidd_intr_data_evt_param9report_idE"></a> <a id="bk_hidd_cb_param_t::hidd_intr_data_evt_param::report_id__uint8_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__intr__data__evt__param_1a8f1d15e9008eb2d8fc18db0c61943944"></a> uint8\_t report\_id
        :   interrupt channel report id

        <a id="_CPPv4N18bk_hidd_cb_param_t24hidd_intr_data_evt_param3lenE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t24hidd_intr_data_evt_param3lenE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t24hidd_intr_data_evt_param3lenE"></a> <a id="bk_hidd_cb_param_t::hidd_intr_data_evt_param::len__uint16_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__intr__data__evt__param_1a3ba779d3231a96e60ff43c98188ba2fb"></a> uint16\_t len
        :   interrupt channel report data length

        <a id="_CPPv4N18bk_hidd_cb_param_t24hidd_intr_data_evt_param4dataE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t24hidd_intr_data_evt_param4dataE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t24hidd_intr_data_evt_param4dataE"></a> <a id="bk_hidd_cb_param_t::hidd_intr_data_evt_param::data__uint8_tP"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__intr__data__evt__param_1a423de68925d2c97dcd259eeb88d29ae1"></a> uint8\_t \*data
        :   interrupt channel report data pointer

    <a id="_CPPv4N18bk_hidd_cb_param_t19hidd_open_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t19hidd_open_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t19hidd_open_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_open_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__open__evt__param"></a> struct hidd\_open\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_OPEN\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t19hidd_open_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t19hidd_open_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t19hidd_open_evt_param6statusE"></a> <a id="bk_hidd_cb_param_t::hidd_open_evt_param::status__bk_hidd_status_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__open__evt__param_1a955422dc4c3968feb3d1fdb8bb173bf7"></a> [bk\_hidd\_status\_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidd_cb_param_t19hidd_open_evt_param11conn_statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t19hidd_open_evt_param11conn_statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t19hidd_open_evt_param11conn_statusE"></a> <a id="bk_hidd_cb_param_t::hidd_open_evt_param::conn_status__bk_hidd_connection_state_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__open__evt__param_1a408f0e0facb434a7cd06b0a3a6e72b55"></a> [bk\_hidd\_connection\_state\_t](#_CPPv426bk_hidd_connection_state_t "bk_hidd_connection_state_t") conn\_status
        :   connection status

        <a id="_CPPv4N18bk_hidd_cb_param_t19hidd_open_evt_param7bd_addrE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t19hidd_open_evt_param7bd_addrE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t19hidd_open_evt_param7bd_addrE"></a> <a id="bk_hidd_cb_param_t::hidd_open_evt_param::bd_addr__bk_bd_addr_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__open__evt__param_1a25fcded0115ceef28ed43366d0009a58"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
        :   host address

    <a id="_CPPv4N18bk_hidd_cb_param_t27hidd_register_app_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t27hidd_register_app_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t27hidd_register_app_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_register_app_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__register__app__evt__param"></a> struct hidd\_register\_app\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_REGISTER\_APP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t27hidd_register_app_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t27hidd_register_app_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t27hidd_register_app_evt_param6statusE"></a> <a id="bk_hidd_cb_param_t::hidd_register_app_evt_param::status__bk_hidd_status_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__register__app__evt__param_1a067e93d91e026e63f4fc4d28c1341332"></a> [bk\_hidd\_status\_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidd_cb_param_t27hidd_register_app_evt_param6in_useE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t27hidd_register_app_evt_param6in_useE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t27hidd_register_app_evt_param6in_useE"></a> <a id="bk_hidd_cb_param_t::hidd_register_app_evt_param::in_use__b"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__register__app__evt__param_1a4c10de8d95ccdf3de444db8ae566b267"></a> bool in\_use
        :   indicate whether use virtual cable plug host address

        <a id="_CPPv4N18bk_hidd_cb_param_t27hidd_register_app_evt_param7bd_addrE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t27hidd_register_app_evt_param7bd_addrE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t27hidd_register_app_evt_param7bd_addrE"></a> <a id="bk_hidd_cb_param_t::hidd_register_app_evt_param::bd_addr__bk_bd_addr_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__register__app__evt__param_1ad73b4baf5d2a784a7764c61c12f0e8c5"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
        :   host address

    <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_report_err_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_report_err_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_report_err_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_report_err_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__report__err__evt__param"></a> struct hidd\_report\_err\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_REPORT\_ERR\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_report_err_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_report_err_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_report_err_evt_param6statusE"></a> <a id="bk_hidd_cb_param_t::hidd_report_err_evt_param::status__bk_hidd_status_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__report__err__evt__param_1a965f113ee84075d4cd77553d713f15cd"></a> [bk\_hidd\_status\_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_report_err_evt_param6reasonE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_report_err_evt_param6reasonE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_report_err_evt_param6reasonE"></a> <a id="bk_hidd_cb_param_t::hidd_report_err_evt_param::reason__uint8_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__report__err__evt__param_1a234a71f9ca5a708b4866124e00def3d2"></a> uint8\_t reason
        :   lower layer failed reason(ref hiddefs.h)

    <a id="_CPPv4N18bk_hidd_cb_param_t26hidd_send_report_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t26hidd_send_report_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t26hidd_send_report_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_send_report_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__send__report__evt__param"></a> struct hidd\_send\_report\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_SEND\_REPORT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t26hidd_send_report_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t26hidd_send_report_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t26hidd_send_report_evt_param6statusE"></a> <a id="bk_hidd_cb_param_t::hidd_send_report_evt_param::status__bk_hidd_status_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__send__report__evt__param_1aeb769c86712c911c8250f25c2809b80d"></a> [bk\_hidd\_status\_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidd_cb_param_t26hidd_send_report_evt_param9report_idE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t26hidd_send_report_evt_param9report_idE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t26hidd_send_report_evt_param9report_idE"></a> <a id="bk_hidd_cb_param_t::hidd_send_report_evt_param::report_id__uint8_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__send__report__evt__param_1a021c09c7ca6cebf9a22f1c51b96c42ef"></a> uint8\_t report\_id
        :   report id

    <a id="_CPPv4N18bk_hidd_cb_param_t23hidd_set_idle_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t23hidd_set_idle_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t23hidd_set_idle_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_set_idle_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__idle__evt__param"></a> struct hidd\_set\_idle\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_SET\_IDLE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t23hidd_set_idle_evt_param12message_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t23hidd_set_idle_evt_param12message_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t23hidd_set_idle_evt_param12message_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_set_idle_evt_param::message_type__bk_hidd_message_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__idle__evt__param_1a6bab6a4261f2da2c0af774966ea89160"></a> [bk\_hidd\_message\_type\_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message\_type
        :   message type

        <a id="_CPPv4N18bk_hidd_cb_param_t23hidd_set_idle_evt_param4idleE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t23hidd_set_idle_evt_param4idleE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t23hidd_set_idle_evt_param4idleE"></a> <a id="bk_hidd_cb_param_t::hidd_set_idle_evt_param::idle__uint8_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__idle__evt__param_1a4ee3c0fd9ff7ab5036824e2d91dd7ef3"></a> uint8\_t idle
        :   idle rate

    <a id="_CPPv4N18bk_hidd_cb_param_t27hidd_set_protocol_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t27hidd_set_protocol_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t27hidd_set_protocol_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_set_protocol_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__protocol__evt__param"></a> struct hidd\_set\_protocol\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_SET\_PROTOCOL\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t27hidd_set_protocol_evt_param13protocol_modeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t27hidd_set_protocol_evt_param13protocol_modeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t27hidd_set_protocol_evt_param13protocol_modeE"></a> <a id="bk_hidd_cb_param_t::hidd_set_protocol_evt_param::protocol_mode__bk_hidd_protocol_mode_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__protocol__evt__param_1a338ff3fec234ecdfd60ca06117b9291a"></a> [bk\_hidd\_protocol\_mode\_t](#_CPPv423bk_hidd_protocol_mode_t "bk_hidd_protocol_mode_t") protocol\_mode
        :   protocol mode

    <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_set_report_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_set_report_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_set_report_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_set_report_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__report__evt__param"></a> struct hidd\_set\_report\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_SET\_REPORT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_set_report_evt_param12message_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_set_report_evt_param12message_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_set_report_evt_param12message_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_set_report_evt_param::message_type__bk_hidd_message_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__report__evt__param_1a8d812dcdeb2b645910a19aba3e2af33d"></a> [bk\_hidd\_message\_type\_t](#_CPPv422bk_hidd_message_type_t "bk_hidd_message_type_t") message\_type
        :   message type

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_set_report_evt_param11report_typeE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_set_report_evt_param11report_typeE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_set_report_evt_param11report_typeE"></a> <a id="bk_hidd_cb_param_t::hidd_set_report_evt_param::report_type__bk_hidd_report_type_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__report__evt__param_1a371ec7eba669ba97fd6787434c665d19"></a> [bk\_hidd\_report\_type\_t](#_CPPv421bk_hidd_report_type_t "bk_hidd_report_type_t") report\_type
        :   report type

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_set_report_evt_param9report_idE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_set_report_evt_param9report_idE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_set_report_evt_param9report_idE"></a> <a id="bk_hidd_cb_param_t::hidd_set_report_evt_param::report_id__uint8_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__report__evt__param_1ad7dafebef5ad48d941674b3de73f6d85"></a> uint8\_t report\_id
        :   report id

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_set_report_evt_param3lenE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_set_report_evt_param3lenE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_set_report_evt_param3lenE"></a> <a id="bk_hidd_cb_param_t::hidd_set_report_evt_param::len__uint16_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__report__evt__param_1aecc4a988d2282e90c5ebffb793d0ed82"></a> uint16\_t len
        :   set\_report data length

        <a id="_CPPv4N18bk_hidd_cb_param_t25hidd_set_report_evt_param4dataE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t25hidd_set_report_evt_param4dataE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t25hidd_set_report_evt_param4dataE"></a> <a id="bk_hidd_cb_param_t::hidd_set_report_evt_param::data__uint8_tP"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__set__report__evt__param_1a027615c8324b0ee9fe651e611fa50530"></a> uint8\_t \*data
        :   set\_report data pointer

    <a id="_CPPv4N18bk_hidd_cb_param_t29hidd_unregister_app_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t29hidd_unregister_app_evt_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t29hidd_unregister_app_evt_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_unregister_app_evt_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__unregister__app__evt__param"></a> struct hidd\_unregister\_app\_evt\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_UNREGISTER\_APP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t29hidd_unregister_app_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t29hidd_unregister_app_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t29hidd_unregister_app_evt_param6statusE"></a> <a id="bk_hidd_cb_param_t::hidd_unregister_app_evt_param::status__bk_hidd_status_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__unregister__app__evt__param_1a6a54f829c974bc80202adafb2d6430c2"></a> [bk\_hidd\_status\_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

    <a id="_CPPv4N18bk_hidd_cb_param_t20hidd_vc_unplug_paramE"></a>

    <a id="_CPPv3N18bk_hidd_cb_param_t20hidd_vc_unplug_paramE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t20hidd_vc_unplug_paramE"></a> <a id="bk_hidd_cb_param_t::hidd_vc_unplug_param"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__vc__unplug__param"></a> struct hidd\_vc\_unplug\_param
    :   *#include \<bk\_dm\_hidd.h\>*

        BK\_HIDD\_VC\_UNPLUG\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidd_cb_param_t20hidd_vc_unplug_param6statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t20hidd_vc_unplug_param6statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t20hidd_vc_unplug_param6statusE"></a> <a id="bk_hidd_cb_param_t::hidd_vc_unplug_param::status__bk_hidd_status_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__vc__unplug__param_1a0cae5e136219154a58a064a2eabeb7c9"></a> [bk\_hidd\_status\_t](#_CPPv416bk_hidd_status_t "bk_hidd_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidd_cb_param_t20hidd_vc_unplug_param11conn_statusE"></a>

        <a id="_CPPv3N18bk_hidd_cb_param_t20hidd_vc_unplug_param11conn_statusE"></a> <a id="_CPPv2N18bk_hidd_cb_param_t20hidd_vc_unplug_param11conn_statusE"></a> <a id="bk_hidd_cb_param_t::hidd_vc_unplug_param::conn_status__bk_hidd_connection_state_t"></a> <a id="structbk__hidd__cb__param__t_1_1hidd__vc__unplug__param_1adac94e7bae6b9fa40b54ab583a79d599"></a> [bk\_hidd\_connection\_state\_t](#_CPPv426bk_hidd_connection_state_t "bk_hidd_connection_state_t") conn\_status
        :   connection status

<a id="structures"></a>

### Structures

<a id="_CPPv419bk_hidd_app_param_t"></a>

<a id="_CPPv319bk_hidd_app_param_t"></a> <a id="_CPPv219bk_hidd_app_param_t"></a> <a id="bk_hidd_app_param_t"></a> <a id="structbk__hidd__app__param__t"></a> struct bk\_hidd\_app\_param\_t
:   HID device characteristics for SDP server.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_hidd_app_param_t4nameE"></a>

    <a id="_CPPv3N19bk_hidd_app_param_t4nameE"></a> <a id="_CPPv2N19bk_hidd_app_param_t4nameE"></a> <a id="bk_hidd_app_param_t::name__cP"></a> <a id="structbk__hidd__app__param__t_1aac7fdb29177b10cfff6e1138ed481b90"></a> char \*name
    :   service name

    <a id="_CPPv4N19bk_hidd_app_param_t11descriptionE"></a>

    <a id="_CPPv3N19bk_hidd_app_param_t11descriptionE"></a> <a id="_CPPv2N19bk_hidd_app_param_t11descriptionE"></a> <a id="bk_hidd_app_param_t::description__cP"></a> <a id="structbk__hidd__app__param__t_1af2380b6fa796a3c16f7abb8802d64607"></a> char \*description
    :   service description

    <a id="_CPPv4N19bk_hidd_app_param_t8providerE"></a>

    <a id="_CPPv3N19bk_hidd_app_param_t8providerE"></a> <a id="_CPPv2N19bk_hidd_app_param_t8providerE"></a> <a id="bk_hidd_app_param_t::provider__cP"></a> <a id="structbk__hidd__app__param__t_1ae9475248651731213b41db15899745dd"></a> char \*provider
    :   provider name

    <a id="_CPPv4N19bk_hidd_app_param_t8subclassE"></a>

    <a id="_CPPv3N19bk_hidd_app_param_t8subclassE"></a> <a id="_CPPv2N19bk_hidd_app_param_t8subclassE"></a> <a id="bk_hidd_app_param_t::subclass__uint8_tP"></a> <a id="structbk__hidd__app__param__t_1a61893d866e02202faa146f5c741c985a"></a> uint8\_t \*subclass
    :   HID device subclass

    <a id="_CPPv4N19bk_hidd_app_param_t9desc_listE"></a>

    <a id="_CPPv3N19bk_hidd_app_param_t9desc_listE"></a> <a id="_CPPv2N19bk_hidd_app_param_t9desc_listE"></a> <a id="bk_hidd_app_param_t::desc_list__uint8_tP"></a> <a id="structbk__hidd__app__param__t_1a4941a635c235a9480aef89b6f8054bb7"></a> uint8\_t \*desc\_list
    :   HID descriptor list

    <a id="_CPPv4N19bk_hidd_app_param_t13desc_list_lenE"></a>

    <a id="_CPPv3N19bk_hidd_app_param_t13desc_list_lenE"></a> <a id="_CPPv2N19bk_hidd_app_param_t13desc_list_lenE"></a> <a id="bk_hidd_app_param_t::desc_list_len__i"></a> <a id="structbk__hidd__app__param__t_1ad62901debcb0ca917a57cbfea575743e"></a> int desc\_list\_len
    :   size in bytes of HID descriptor list

<a id="_CPPv419bk_hidd_qos_param_t"></a>

<a id="_CPPv319bk_hidd_qos_param_t"></a> <a id="_CPPv219bk_hidd_qos_param_t"></a> <a id="bk_hidd_qos_param_t"></a> <a id="structbk__hidd__qos__param__t"></a> struct bk\_hidd\_qos\_param\_t
:   HIDD Quality of Service parameters negotiated over L2CAP.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_hidd_qos_param_t12service_typeE"></a>

    <a id="_CPPv3N19bk_hidd_qos_param_t12service_typeE"></a> <a id="_CPPv2N19bk_hidd_qos_param_t12service_typeE"></a> <a id="bk_hidd_qos_param_t::service_type__uint8_t"></a> <a id="structbk__hidd__qos__param__t_1af161ae3e5bd184ce03d832d997dbad6b"></a> uint8\_t service\_type
    :   the level of service, 0 indicates no traffic

    <a id="_CPPv4N19bk_hidd_qos_param_t10token_rateE"></a>

    <a id="_CPPv3N19bk_hidd_qos_param_t10token_rateE"></a> <a id="_CPPv2N19bk_hidd_qos_param_t10token_rateE"></a> <a id="bk_hidd_qos_param_t::token_rate__uint32_t"></a> <a id="structbk__hidd__qos__param__t_1a98f3b52b5adf4926ee083f054ee9b179"></a> uint32\_t token\_rate
    :   token rate in bytes per second, 0 indicates “don’t care”

    <a id="_CPPv4N19bk_hidd_qos_param_t17token_bucket_sizeE"></a>

    <a id="_CPPv3N19bk_hidd_qos_param_t17token_bucket_sizeE"></a> <a id="_CPPv2N19bk_hidd_qos_param_t17token_bucket_sizeE"></a> <a id="bk_hidd_qos_param_t::token_bucket_size__uint32_t"></a> <a id="structbk__hidd__qos__param__t_1ad2023488c65193d99c1b7c4d986c4663"></a> uint32\_t token\_bucket\_size
    :   limit on the burstness of the application data

    <a id="_CPPv4N19bk_hidd_qos_param_t14peak_bandwidthE"></a>

    <a id="_CPPv3N19bk_hidd_qos_param_t14peak_bandwidthE"></a> <a id="_CPPv2N19bk_hidd_qos_param_t14peak_bandwidthE"></a> <a id="bk_hidd_qos_param_t::peak_bandwidth__uint32_t"></a> <a id="structbk__hidd__qos__param__t_1a1ba1d664f637d757e29bf55155d79a86"></a> uint32\_t peak\_bandwidth
    :   bytes per second, value 0 indicates “don’t care”

    <a id="_CPPv4N19bk_hidd_qos_param_t14access_latencyE"></a>

    <a id="_CPPv3N19bk_hidd_qos_param_t14access_latencyE"></a> <a id="_CPPv2N19bk_hidd_qos_param_t14access_latencyE"></a> <a id="bk_hidd_qos_param_t::access_latency__uint32_t"></a> <a id="structbk__hidd__qos__param__t_1a3ce00e35440f0b00e2b9d7e2c4c51de3"></a> uint32\_t access\_latency
    :   maximum acceptable delay in microseconds

    <a id="_CPPv4N19bk_hidd_qos_param_t15delay_variationE"></a>

    <a id="_CPPv3N19bk_hidd_qos_param_t15delay_variationE"></a> <a id="_CPPv2N19bk_hidd_qos_param_t15delay_variationE"></a> <a id="bk_hidd_qos_param_t::delay_variation__uint32_t"></a> <a id="structbk__hidd__qos__param__t_1ae6e8f6c62b63833fd38be97855863617"></a> uint32\_t delay\_variation
    :   the difference in microseconds between the max and min delay

<a id="macros"></a>

### Macros

<a id="c.BK_HID_CLASS_UNKNOWN"></a>

<a id="bk__dm__hidd_8h_1afe10d51e5b66c69aee23f8366153af33"></a> BK\_HID\_CLASS\_UNKNOWN
:   subclass of hid device

    unknown HID device subclass

<a id="c.BK_HID_CLASS_JOS"></a>

<a id="bk__dm__hidd_8h_1abdb0c89c19cff71bbdc77f2ebe0a7688"></a> BK\_HID\_CLASS\_JOS
:   joystick

<a id="c.BK_HID_CLASS_GPD"></a>

<a id="bk__dm__hidd_8h_1a3e4fd3f858e70b12d4e99b0b9324ab3d"></a> BK\_HID\_CLASS\_GPD
:   game pad

<a id="c.BK_HID_CLASS_RMC"></a>

<a id="bk__dm__hidd_8h_1ac709aebdeb8cf0b9a5cffec600aade8e"></a> BK\_HID\_CLASS\_RMC
:   remote control

<a id="c.BK_HID_CLASS_SED"></a>

<a id="bk__dm__hidd_8h_1a7eae98c02a3240ad7c42a800f46eb07a"></a> BK\_HID\_CLASS\_SED
:   sensing device

<a id="c.BK_HID_CLASS_DGT"></a>

<a id="bk__dm__hidd_8h_1a8ccf9b8e458b3ad711a9325fd71744ae"></a> BK\_HID\_CLASS\_DGT
:   digitizer tablet

<a id="c.BK_HID_CLASS_CDR"></a>

<a id="bk__dm__hidd_8h_1ae99837d6b6a7993ea4cac8f262bc87cd"></a> BK\_HID\_CLASS\_CDR
:   card reader

<a id="c.BK_HID_CLASS_KBD"></a>

<a id="bk__dm__hidd_8h_1a70e54adc93d9cd14ae664cdb459aadc6"></a> BK\_HID\_CLASS\_KBD
:   keyboard

<a id="c.BK_HID_CLASS_MIC"></a>

<a id="bk__dm__hidd_8h_1aef9bd4f5c3114858be9a84209d78626a"></a> BK\_HID\_CLASS\_MIC
:   pointing device

<a id="c.BK_HID_CLASS_COM"></a>

<a id="bk__dm__hidd_8h_1a7711bd557625cc99efe24cd8a54ae9c0"></a> BK\_HID\_CLASS\_COM
:   combo keyboard/pointing

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410bk_hd_cb_t"></a>

<a id="_CPPv310bk_hd_cb_t"></a> <a id="_CPPv210bk_hd_cb_t"></a> <a id="bk_hd_cb_t"></a> <a id="bk__dm__hidd_8h_1afbc278e6688863942efd7d32c30b6763"></a> typedef void (\*bk\_hd\_cb\_t)([bk\_hidd\_cb\_event\_t](#_CPPv418bk_hidd_cb_event_t "bk_hidd_cb_event_t") event, [bk\_hidd\_cb\_param\_t](#_CPPv418bk_hidd_cb_param_t "bk_hidd_cb_param_t") \*param)
:   HID device callback function type.

    Param event
    :   Event type

    Param param
    :   Point to callback parameter, currently is union type

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv425bk_hidd_handshake_error_t"></a>

<a id="_CPPv325bk_hidd_handshake_error_t"></a> <a id="_CPPv225bk_hidd_handshake_error_t"></a> <a id="bk__dm__hidd_8h_1a75a0faeb968fe79bbca9b67f4c411f6d"></a> enum bk\_hidd\_handshake\_error\_t
:   HIDD handshake result code.

    *Values:*

    <a id="_CPPv4N25bk_hidd_handshake_error_t32BK_HID_PAR_HANDSHAKE_RSP_SUCCESSE"></a>

    <a id="_CPPv3N25bk_hidd_handshake_error_t32BK_HID_PAR_HANDSHAKE_RSP_SUCCESSE"></a> <a id="_CPPv2N25bk_hidd_handshake_error_t32BK_HID_PAR_HANDSHAKE_RSP_SUCCESSE"></a> <a id="bk__dm__hidd_8h_1a75a0faeb968fe79bbca9b67f4c411f6da2e134e9e9066cf7481b53225cc8e8249"></a> enumerator BK\_HID\_PAR\_HANDSHAKE\_RSP\_SUCCESS
    :   successful

    <a id="_CPPv4N25bk_hidd_handshake_error_t34BK_HID_PAR_HANDSHAKE_RSP_NOT_READYE"></a>

    <a id="_CPPv3N25bk_hidd_handshake_error_t34BK_HID_PAR_HANDSHAKE_RSP_NOT_READYE"></a> <a id="_CPPv2N25bk_hidd_handshake_error_t34BK_HID_PAR_HANDSHAKE_RSP_NOT_READYE"></a> <a id="bk__dm__hidd_8h_1a75a0faeb968fe79bbca9b67f4c411f6da7bc1ee03fd31163640102a59bdad5c29"></a> enumerator BK\_HID\_PAR\_HANDSHAKE\_RSP\_NOT\_READY
    :   not ready, device is too busy to accept data

    <a id="_CPPv4N25bk_hidd_handshake_error_t43BK_HID_PAR_HANDSHAKE_RSP_ERR_INVALID_REP_IDE"></a>

    <a id="_CPPv3N25bk_hidd_handshake_error_t43BK_HID_PAR_HANDSHAKE_RSP_ERR_INVALID_REP_IDE"></a> <a id="_CPPv2N25bk_hidd_handshake_error_t43BK_HID_PAR_HANDSHAKE_RSP_ERR_INVALID_REP_IDE"></a> <a id="bk__dm__hidd_8h_1a75a0faeb968fe79bbca9b67f4c411f6da02904e71ea54ec1f4ea937ae1f8068ff"></a> enumerator BK\_HID\_PAR\_HANDSHAKE\_RSP\_ERR\_INVALID\_REP\_ID
    :   invalid report ID

    <a id="_CPPv4N25bk_hidd_handshake_error_t44BK_HID_PAR_HANDSHAKE_RSP_ERR_UNSUPPORTED_REQE"></a>

    <a id="_CPPv3N25bk_hidd_handshake_error_t44BK_HID_PAR_HANDSHAKE_RSP_ERR_UNSUPPORTED_REQE"></a> <a id="_CPPv2N25bk_hidd_handshake_error_t44BK_HID_PAR_HANDSHAKE_RSP_ERR_UNSUPPORTED_REQE"></a> <a id="bk__dm__hidd_8h_1a75a0faeb968fe79bbca9b67f4c411f6da56b13ab920f3300527d14110465db1e9"></a> enumerator BK\_HID\_PAR\_HANDSHAKE\_RSP\_ERR\_UNSUPPORTED\_REQ
    :   device does not support the request

    <a id="_CPPv4N25bk_hidd_handshake_error_t42BK_HID_PAR_HANDSHAKE_RSP_ERR_INVALID_PARAME"></a>

    <a id="_CPPv3N25bk_hidd_handshake_error_t42BK_HID_PAR_HANDSHAKE_RSP_ERR_INVALID_PARAME"></a> <a id="_CPPv2N25bk_hidd_handshake_error_t42BK_HID_PAR_HANDSHAKE_RSP_ERR_INVALID_PARAME"></a> <a id="bk__dm__hidd_8h_1a75a0faeb968fe79bbca9b67f4c411f6da05452d7fe5a10c6285ae0c0ddeb9f5f3"></a> enumerator BK\_HID\_PAR\_HANDSHAKE\_RSP\_ERR\_INVALID\_PARAM
    :   parameter value is out of range or inappropriate

    <a id="_CPPv4N25bk_hidd_handshake_error_t36BK_HID_PAR_HANDSHAKE_RSP_ERR_UNKNOWNE"></a>

    <a id="_CPPv3N25bk_hidd_handshake_error_t36BK_HID_PAR_HANDSHAKE_RSP_ERR_UNKNOWNE"></a> <a id="_CPPv2N25bk_hidd_handshake_error_t36BK_HID_PAR_HANDSHAKE_RSP_ERR_UNKNOWNE"></a> <a id="bk__dm__hidd_8h_1a75a0faeb968fe79bbca9b67f4c411f6dada7c8be434368f35e538c83cfc8e560c"></a> enumerator BK\_HID\_PAR\_HANDSHAKE\_RSP\_ERR\_UNKNOWN
    :   device could not identify the error condition

    <a id="_CPPv4N25bk_hidd_handshake_error_t34BK_HID_PAR_HANDSHAKE_RSP_ERR_FATALE"></a>

    <a id="_CPPv3N25bk_hidd_handshake_error_t34BK_HID_PAR_HANDSHAKE_RSP_ERR_FATALE"></a> <a id="_CPPv2N25bk_hidd_handshake_error_t34BK_HID_PAR_HANDSHAKE_RSP_ERR_FATALE"></a> <a id="bk__dm__hidd_8h_1a75a0faeb968fe79bbca9b67f4c411f6da98673642163e04b8a3a008a48d3d9635"></a> enumerator BK\_HID\_PAR\_HANDSHAKE\_RSP\_ERR\_FATAL
    :   restart is essential to resume functionality

<a id="_CPPv422bk_hidd_message_type_t"></a>

<a id="_CPPv322bk_hidd_message_type_t"></a> <a id="_CPPv222bk_hidd_message_type_t"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41c"></a> enum bk\_hidd\_message\_type\_t
:   HIDD message types.

    *Values:*

    <a id="_CPPv4N22bk_hidd_message_type_t30BK_HIDD_MESSAGE_TYPE_HANDSHAKEE"></a>

    <a id="_CPPv3N22bk_hidd_message_type_t30BK_HIDD_MESSAGE_TYPE_HANDSHAKEE"></a> <a id="_CPPv2N22bk_hidd_message_type_t30BK_HIDD_MESSAGE_TYPE_HANDSHAKEE"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41ca9becf922f871aa8db378ec1c046685f7"></a> enumerator BK\_HIDD\_MESSAGE\_TYPE\_HANDSHAKE
    :   handshake type

    <a id="_CPPv4N22bk_hidd_message_type_t32BK_HIDD_MESSAGE_TYPE_HID_CONTROLE"></a>

    <a id="_CPPv3N22bk_hidd_message_type_t32BK_HIDD_MESSAGE_TYPE_HID_CONTROLE"></a> <a id="_CPPv2N22bk_hidd_message_type_t32BK_HIDD_MESSAGE_TYPE_HID_CONTROLE"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41ca5b1d4e5fad139b4a8cad48ffd2721989"></a> enumerator BK\_HIDD\_MESSAGE\_TYPE\_HID\_CONTROL
    :   hid control type

    <a id="_CPPv4N22bk_hidd_message_type_t31BK_HIDD_MESSAGE_TYPE_GET_REPORTE"></a>

    <a id="_CPPv3N22bk_hidd_message_type_t31BK_HIDD_MESSAGE_TYPE_GET_REPORTE"></a> <a id="_CPPv2N22bk_hidd_message_type_t31BK_HIDD_MESSAGE_TYPE_GET_REPORTE"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41caec20491e29ec2168512f1397774a95af"></a> enumerator BK\_HIDD\_MESSAGE\_TYPE\_GET\_REPORT
    :   get report

    <a id="_CPPv4N22bk_hidd_message_type_t31BK_HIDD_MESSAGE_TYPE_SET_REPORTE"></a>

    <a id="_CPPv3N22bk_hidd_message_type_t31BK_HIDD_MESSAGE_TYPE_SET_REPORTE"></a> <a id="_CPPv2N22bk_hidd_message_type_t31BK_HIDD_MESSAGE_TYPE_SET_REPORTE"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41caaa48b3a10ca71cf6a998f09aa496719e"></a> enumerator BK\_HIDD\_MESSAGE\_TYPE\_SET\_REPORT
    :   set report

    <a id="_CPPv4N22bk_hidd_message_type_t33BK_HIDD_MESSAGE_TYPE_GET_PROTOCOLE"></a>

    <a id="_CPPv3N22bk_hidd_message_type_t33BK_HIDD_MESSAGE_TYPE_GET_PROTOCOLE"></a> <a id="_CPPv2N22bk_hidd_message_type_t33BK_HIDD_MESSAGE_TYPE_GET_PROTOCOLE"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41ca0da1aaa4e0ca64cba2b0832ba26c1728"></a> enumerator BK\_HIDD\_MESSAGE\_TYPE\_GET\_PROTOCOL
    :   get protocol

    <a id="_CPPv4N22bk_hidd_message_type_t33BK_HIDD_MESSAGE_TYPE_SET_PROTOCOLE"></a>

    <a id="_CPPv3N22bk_hidd_message_type_t33BK_HIDD_MESSAGE_TYPE_SET_PROTOCOLE"></a> <a id="_CPPv2N22bk_hidd_message_type_t33BK_HIDD_MESSAGE_TYPE_SET_PROTOCOLE"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41caafde29d243064869efe96c625f5104af"></a> enumerator BK\_HIDD\_MESSAGE\_TYPE\_SET\_PROTOCOL
    :   set protocol

    <a id="_CPPv4N22bk_hidd_message_type_t29BK_HIDD_MESSAGE_TYPE_GET_IDLEE"></a>

    <a id="_CPPv3N22bk_hidd_message_type_t29BK_HIDD_MESSAGE_TYPE_GET_IDLEE"></a> <a id="_CPPv2N22bk_hidd_message_type_t29BK_HIDD_MESSAGE_TYPE_GET_IDLEE"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41ca89b8c91085a2a3e151c8156cf993352e"></a> enumerator BK\_HIDD\_MESSAGE\_TYPE\_GET\_IDLE
    :   get idle \[DEPRECATED\]

    <a id="_CPPv4N22bk_hidd_message_type_t29BK_HIDD_MESSAGE_TYPE_SET_IDLEE"></a>

    <a id="_CPPv3N22bk_hidd_message_type_t29BK_HIDD_MESSAGE_TYPE_SET_IDLEE"></a> <a id="_CPPv2N22bk_hidd_message_type_t29BK_HIDD_MESSAGE_TYPE_SET_IDLEE"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41caedc934b53a9241b5a4b95ed777b2c592"></a> enumerator BK\_HIDD\_MESSAGE\_TYPE\_SET\_IDLE
    :   set idle \[DEPRECATED\]

    <a id="_CPPv4N22bk_hidd_message_type_t25BK_HIDD_MESSAGE_TYPE_DATAE"></a>

    <a id="_CPPv3N22bk_hidd_message_type_t25BK_HIDD_MESSAGE_TYPE_DATAE"></a> <a id="_CPPv2N22bk_hidd_message_type_t25BK_HIDD_MESSAGE_TYPE_DATAE"></a> <a id="bk__dm__hidd_8h_1a1b9c0b7d080f498aae3db9686bd9a41ca9ecbf72d30323db4ac328fe08257d10b"></a> enumerator BK\_HIDD\_MESSAGE\_TYPE\_DATA
    :   data intr

<a id="_CPPv421bk_hidd_report_type_t"></a>

<a id="_CPPv321bk_hidd_report_type_t"></a> <a id="_CPPv221bk_hidd_report_type_t"></a> <a id="bk__dm__hidd_8h_1ac04cbe31706f2af5fc1d48beddd92b80"></a> enum bk\_hidd\_report\_type\_t
:   HIDD report types.

    *Values:*

    <a id="_CPPv4N21bk_hidd_report_type_t28BK_HIDD_REPORT_TYPE_RESERVEDE"></a>

    <a id="_CPPv3N21bk_hidd_report_type_t28BK_HIDD_REPORT_TYPE_RESERVEDE"></a> <a id="_CPPv2N21bk_hidd_report_type_t28BK_HIDD_REPORT_TYPE_RESERVEDE"></a> <a id="bk__dm__hidd_8h_1ac04cbe31706f2af5fc1d48beddd92b80a0dd6890aceb094f5e7b7d3389377dd06"></a> enumerator BK\_HIDD\_REPORT\_TYPE\_RESERVED
    :   reserved

    <a id="_CPPv4N21bk_hidd_report_type_t25BK_HIDD_REPORT_TYPE_INPUTE"></a>

    <a id="_CPPv3N21bk_hidd_report_type_t25BK_HIDD_REPORT_TYPE_INPUTE"></a> <a id="_CPPv2N21bk_hidd_report_type_t25BK_HIDD_REPORT_TYPE_INPUTE"></a> <a id="bk__dm__hidd_8h_1ac04cbe31706f2af5fc1d48beddd92b80a272a081bca90aa1a180efc9382385c07"></a> enumerator BK\_HIDD\_REPORT\_TYPE\_INPUT
    :   input report

    <a id="_CPPv4N21bk_hidd_report_type_t26BK_HIDD_REPORT_TYPE_OUTPUTE"></a>

    <a id="_CPPv3N21bk_hidd_report_type_t26BK_HIDD_REPORT_TYPE_OUTPUTE"></a> <a id="_CPPv2N21bk_hidd_report_type_t26BK_HIDD_REPORT_TYPE_OUTPUTE"></a> <a id="bk__dm__hidd_8h_1ac04cbe31706f2af5fc1d48beddd92b80ab4826e1efae83b5db323a5f6e42b84c2"></a> enumerator BK\_HIDD\_REPORT\_TYPE\_OUTPUT
    :   output report

    <a id="_CPPv4N21bk_hidd_report_type_t27BK_HIDD_REPORT_TYPE_FEATUREE"></a>

    <a id="_CPPv3N21bk_hidd_report_type_t27BK_HIDD_REPORT_TYPE_FEATUREE"></a> <a id="_CPPv2N21bk_hidd_report_type_t27BK_HIDD_REPORT_TYPE_FEATUREE"></a> <a id="bk__dm__hidd_8h_1ac04cbe31706f2af5fc1d48beddd92b80ab0b73472a308b7e090146e13bcc32600"></a> enumerator BK\_HIDD\_REPORT\_TYPE\_FEATURE
    :   feature report

<a id="_CPPv417bk_hidd_ctrl_op_t"></a>

<a id="_CPPv317bk_hidd_ctrl_op_t"></a> <a id="_CPPv217bk_hidd_ctrl_op_t"></a> <a id="bk__dm__hidd_8h_1afcb4b09c3c0f562c86f83442ed529451"></a> enum bk\_hidd\_ctrl\_op\_t
:   HIDD control operation.

    *Values:*

    <a id="_CPPv4N17bk_hidd_ctrl_op_t19BK_HIDD_CTRL_OP_NOPE"></a>

    <a id="_CPPv3N17bk_hidd_ctrl_op_t19BK_HIDD_CTRL_OP_NOPE"></a> <a id="_CPPv2N17bk_hidd_ctrl_op_t19BK_HIDD_CTRL_OP_NOPE"></a> <a id="bk__dm__hidd_8h_1afcb4b09c3c0f562c86f83442ed529451a45a7ef98d81928e0196f3efdaf4c1517"></a> enumerator BK\_HIDD\_CTRL\_OP\_NOP
    :   no operation

    <a id="_CPPv4N17bk_hidd_ctrl_op_t26BK_HIDD_CTRL_OP_HARD_RESETE"></a>

    <a id="_CPPv3N17bk_hidd_ctrl_op_t26BK_HIDD_CTRL_OP_HARD_RESETE"></a> <a id="_CPPv2N17bk_hidd_ctrl_op_t26BK_HIDD_CTRL_OP_HARD_RESETE"></a> <a id="bk__dm__hidd_8h_1afcb4b09c3c0f562c86f83442ed529451a7a657832eb327962c928e86ff5e9fc62"></a> enumerator BK\_HIDD\_CTRL\_OP\_HARD\_RESET
    :   hadr reset

    <a id="_CPPv4N17bk_hidd_ctrl_op_t26BK_HIDD_CTRL_OP_SOFT_RESETE"></a>

    <a id="_CPPv3N17bk_hidd_ctrl_op_t26BK_HIDD_CTRL_OP_SOFT_RESETE"></a> <a id="_CPPv2N17bk_hidd_ctrl_op_t26BK_HIDD_CTRL_OP_SOFT_RESETE"></a> <a id="bk__dm__hidd_8h_1afcb4b09c3c0f562c86f83442ed529451adc547881cc9778c6062cc4dad3722ba7"></a> enumerator BK\_HIDD\_CTRL\_OP\_SOFT\_RESET
    :   soft reset

    <a id="_CPPv4N17bk_hidd_ctrl_op_t23BK_HIDD_CTRL_OP_SUSPENDE"></a>

    <a id="_CPPv3N17bk_hidd_ctrl_op_t23BK_HIDD_CTRL_OP_SUSPENDE"></a> <a id="_CPPv2N17bk_hidd_ctrl_op_t23BK_HIDD_CTRL_OP_SUSPENDE"></a> <a id="bk__dm__hidd_8h_1afcb4b09c3c0f562c86f83442ed529451a42fc6edd4daec8bf5317a978d199c853"></a> enumerator BK\_HIDD\_CTRL\_OP\_SUSPEND
    :   suspend

    <a id="_CPPv4N17bk_hidd_ctrl_op_t28BK_HIDD_CTRL_OP_EXIT_SUSPENDE"></a>

    <a id="_CPPv3N17bk_hidd_ctrl_op_t28BK_HIDD_CTRL_OP_EXIT_SUSPENDE"></a> <a id="_CPPv2N17bk_hidd_ctrl_op_t28BK_HIDD_CTRL_OP_EXIT_SUSPENDE"></a> <a id="bk__dm__hidd_8h_1afcb4b09c3c0f562c86f83442ed529451a18f14c563fdc46eb94657e075e6a900a"></a> enumerator BK\_HIDD\_CTRL\_OP\_EXIT\_SUSPEND
    :   exit suspend

<a id="_CPPv426bk_hidd_connection_state_t"></a>

<a id="_CPPv326bk_hidd_connection_state_t"></a> <a id="_CPPv226bk_hidd_connection_state_t"></a> <a id="bk__dm__hidd_8h_1a383790353fa8681394654b6a33ccf2f2"></a> enum bk\_hidd\_connection\_state\_t
:   HIDD connection state.

    *Values:*

    <a id="_CPPv4N26bk_hidd_connection_state_t28BK_HIDD_CONN_STATE_CONNECTEDE"></a>

    <a id="_CPPv3N26bk_hidd_connection_state_t28BK_HIDD_CONN_STATE_CONNECTEDE"></a> <a id="_CPPv2N26bk_hidd_connection_state_t28BK_HIDD_CONN_STATE_CONNECTEDE"></a> <a id="bk__dm__hidd_8h_1a383790353fa8681394654b6a33ccf2f2ae5a8574fd3fa47948e3e18ea4fab6193"></a> enumerator BK\_HIDD\_CONN\_STATE\_CONNECTED
    :   HID connection established

    <a id="_CPPv4N26bk_hidd_connection_state_t29BK_HIDD_CONN_STATE_CONNECTINGE"></a>

    <a id="_CPPv3N26bk_hidd_connection_state_t29BK_HIDD_CONN_STATE_CONNECTINGE"></a> <a id="_CPPv2N26bk_hidd_connection_state_t29BK_HIDD_CONN_STATE_CONNECTINGE"></a> <a id="bk__dm__hidd_8h_1a383790353fa8681394654b6a33ccf2f2ab65dbcf8022ecdb6d3b911b4c9d5382e"></a> enumerator BK\_HIDD\_CONN\_STATE\_CONNECTING
    :   connection to remote Bluetooth device

    <a id="_CPPv4N26bk_hidd_connection_state_t31BK_HIDD_CONN_STATE_DISCONNECTEDE"></a>

    <a id="_CPPv3N26bk_hidd_connection_state_t31BK_HIDD_CONN_STATE_DISCONNECTEDE"></a> <a id="_CPPv2N26bk_hidd_connection_state_t31BK_HIDD_CONN_STATE_DISCONNECTEDE"></a> <a id="bk__dm__hidd_8h_1a383790353fa8681394654b6a33ccf2f2af1ad69ea038905f68905dc053faf2ac0"></a> enumerator BK\_HIDD\_CONN\_STATE\_DISCONNECTED
    :   connection released

    <a id="_CPPv4N26bk_hidd_connection_state_t32BK_HIDD_CONN_STATE_DISCONNECTINGE"></a>

    <a id="_CPPv3N26bk_hidd_connection_state_t32BK_HIDD_CONN_STATE_DISCONNECTINGE"></a> <a id="_CPPv2N26bk_hidd_connection_state_t32BK_HIDD_CONN_STATE_DISCONNECTINGE"></a> <a id="bk__dm__hidd_8h_1a383790353fa8681394654b6a33ccf2f2a76355877bc13976ccf378d8888d5ef57"></a> enumerator BK\_HIDD\_CONN\_STATE\_DISCONNECTING
    :   disconnecting to remote Bluetooth device

    <a id="_CPPv4N26bk_hidd_connection_state_t26BK_HIDD_CONN_STATE_UNKNOWNE"></a>

    <a id="_CPPv3N26bk_hidd_connection_state_t26BK_HIDD_CONN_STATE_UNKNOWNE"></a> <a id="_CPPv2N26bk_hidd_connection_state_t26BK_HIDD_CONN_STATE_UNKNOWNE"></a> <a id="bk__dm__hidd_8h_1a383790353fa8681394654b6a33ccf2f2adeaf10b91a47a6ef9014d61588707b1a"></a> enumerator BK\_HIDD\_CONN\_STATE\_UNKNOWN
    :   unknown connection state

<a id="_CPPv423bk_hidd_protocol_mode_t"></a>

<a id="_CPPv323bk_hidd_protocol_mode_t"></a> <a id="_CPPv223bk_hidd_protocol_mode_t"></a> <a id="bk__dm__hidd_8h_1ab3b84c63adc9b7144bb784fabab1ec61"></a> enum bk\_hidd\_protocol\_mode\_t
:   HID device protocol modes.

    *Values:*

    <a id="_CPPv4N23bk_hidd_protocol_mode_t19BK_HIDD_REPORT_MODEE"></a>

    <a id="_CPPv3N23bk_hidd_protocol_mode_t19BK_HIDD_REPORT_MODEE"></a> <a id="_CPPv2N23bk_hidd_protocol_mode_t19BK_HIDD_REPORT_MODEE"></a> <a id="bk__dm__hidd_8h_1ab3b84c63adc9b7144bb784fabab1ec61a7eeee7d0d6b27612e040474db26abcdd"></a> enumerator BK\_HIDD\_REPORT\_MODE
    :   Report Protocol Mode

    <a id="_CPPv4N23bk_hidd_protocol_mode_t17BK_HIDD_BOOT_MODEE"></a>

    <a id="_CPPv3N23bk_hidd_protocol_mode_t17BK_HIDD_BOOT_MODEE"></a> <a id="_CPPv2N23bk_hidd_protocol_mode_t17BK_HIDD_BOOT_MODEE"></a> <a id="bk__dm__hidd_8h_1ab3b84c63adc9b7144bb784fabab1ec61aa1b1fc7c725e59de52699b17d9a1b872"></a> enumerator BK\_HIDD\_BOOT\_MODE
    :   Boot Protocol Mode

    <a id="_CPPv4N23bk_hidd_protocol_mode_t24BK_HIDD_UNSUPPORTED_MODEE"></a>

    <a id="_CPPv3N23bk_hidd_protocol_mode_t24BK_HIDD_UNSUPPORTED_MODEE"></a> <a id="_CPPv2N23bk_hidd_protocol_mode_t24BK_HIDD_UNSUPPORTED_MODEE"></a> <a id="bk__dm__hidd_8h_1ab3b84c63adc9b7144bb784fabab1ec61a3d1d4e0c60f1895069aed574290013a8"></a> enumerator BK\_HIDD\_UNSUPPORTED\_MODE
    :   unsupported

<a id="_CPPv424bk_hidd_boot_report_id_t"></a>

<a id="_CPPv324bk_hidd_boot_report_id_t"></a> <a id="_CPPv224bk_hidd_boot_report_id_t"></a> <a id="bk__dm__hidd_8h_1ac356a0273cbd958bc4f2ab2cd06c89b0"></a> enum bk\_hidd\_boot\_report\_id\_t
:   HID Boot Protocol report IDs.

    *Values:*

    <a id="_CPPv4N24bk_hidd_boot_report_id_t31BK_HIDD_BOOT_REPORT_ID_KEYBOARDE"></a>

    <a id="_CPPv3N24bk_hidd_boot_report_id_t31BK_HIDD_BOOT_REPORT_ID_KEYBOARDE"></a> <a id="_CPPv2N24bk_hidd_boot_report_id_t31BK_HIDD_BOOT_REPORT_ID_KEYBOARDE"></a> <a id="bk__dm__hidd_8h_1ac356a0273cbd958bc4f2ab2cd06c89b0aeb3cf9369f7ac39035387a029bed1666"></a> enumerator BK\_HIDD\_BOOT\_REPORT\_ID\_KEYBOARD
    :   report ID of Boot Protocol keyboard report

    <a id="_CPPv4N24bk_hidd_boot_report_id_t28BK_HIDD_BOOT_REPORT_ID_MOUSEE"></a>

    <a id="_CPPv3N24bk_hidd_boot_report_id_t28BK_HIDD_BOOT_REPORT_ID_MOUSEE"></a> <a id="_CPPv2N24bk_hidd_boot_report_id_t28BK_HIDD_BOOT_REPORT_ID_MOUSEE"></a> <a id="bk__dm__hidd_8h_1ac356a0273cbd958bc4f2ab2cd06c89b0a3df72f17270c5650af5587a79e0fbb49"></a> enumerator BK\_HIDD\_BOOT\_REPORT\_ID\_MOUSE
    :   report ID of Boot Protocol mouse report

<a id="_CPPv4Ut2_55"></a>

<a id="_CPPv3Ut2_55"></a> <a id="bk__dm__hidd_8h_1a1be3860693af99a6c1da72580097294c"></a> enum \[anonymous\]
:   HID Boot Protocol report size including report ID.

    *Values:*

    <a id="_CPPv4NUt2_5533BK_HIDD_BOOT_REPORT_SIZE_KEYBOARDE"></a>

    <a id="_CPPv3NUt2_5533BK_HIDD_BOOT_REPORT_SIZE_KEYBOARDE"></a> <a id="bk__dm__hidd_8h_1a1be3860693af99a6c1da72580097294caaed1b78aa118c9c06e11fc945e539362"></a> enumerator BK\_HIDD\_BOOT\_REPORT\_SIZE\_KEYBOARD
    :   report size of Boot Protocol keyboard report

    <a id="_CPPv4NUt2_5530BK_HIDD_BOOT_REPORT_SIZE_MOUSEE"></a>

    <a id="_CPPv3NUt2_5530BK_HIDD_BOOT_REPORT_SIZE_MOUSEE"></a> <a id="bk__dm__hidd_8h_1a1be3860693af99a6c1da72580097294cae88b9e89ff8ceeca32e9b7fdadfafbcb"></a> enumerator BK\_HIDD\_BOOT\_REPORT\_SIZE\_MOUSE
    :   report size of Boot Protocol mouse report

<a id="_CPPv418bk_hidd_cb_event_t"></a>

<a id="_CPPv318bk_hidd_cb_event_t"></a> <a id="_CPPv218bk_hidd_cb_event_t"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70"></a> enum bk\_hidd\_cb\_event\_t
:   HID device callback function events.

    *Values:*

    <a id="_CPPv4N18bk_hidd_cb_event_t16BK_HIDD_INIT_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t16BK_HIDD_INIT_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t16BK_HIDD_INIT_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70adc8429fe464cb87e901093acb6989dad"></a> enumerator BK\_HIDD\_INIT\_EVT
    :   When HID device is initialized, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t18BK_HIDD_DEINIT_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t18BK_HIDD_DEINIT_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t18BK_HIDD_DEINIT_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a2dcd5767aa134c89d93e0873e589785f"></a> enumerator BK\_HIDD\_DEINIT\_EVT
    :   When HID device is deinitialized, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t24BK_HIDD_REGISTER_APP_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t24BK_HIDD_REGISTER_APP_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t24BK_HIDD_REGISTER_APP_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70ab57f86ba3fcc256ceb10960e47106f67"></a> enumerator BK\_HIDD\_REGISTER\_APP\_EVT
    :   When HID device application registered, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t26BK_HIDD_UNREGISTER_APP_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t26BK_HIDD_UNREGISTER_APP_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t26BK_HIDD_UNREGISTER_APP_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70ac62d4d07412a3428630276b88c46b20a"></a> enumerator BK\_HIDD\_UNREGISTER\_APP\_EVT
    :   When HID device application unregistered, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t16BK_HIDD_OPEN_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t16BK_HIDD_OPEN_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t16BK_HIDD_OPEN_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a89f7aa0138acd19b8c7b242d9e431928"></a> enumerator BK\_HIDD\_OPEN\_EVT
    :   When HID device connection to host opened, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t17BK_HIDD_CLOSE_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t17BK_HIDD_CLOSE_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t17BK_HIDD_CLOSE_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a1dcd55244ddbfa24ba0a80175a63ca17"></a> enumerator BK\_HIDD\_CLOSE\_EVT
    :   When HID device connection to host closed, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t23BK_HIDD_SEND_REPORT_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t23BK_HIDD_SEND_REPORT_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t23BK_HIDD_SEND_REPORT_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a7c7adf1663bc372e1a54be5615dd8010"></a> enumerator BK\_HIDD\_SEND\_REPORT\_EVT
    :   When HID device send report to lower layer, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t22BK_HIDD_REPORT_ERR_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t22BK_HIDD_REPORT_ERR_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t22BK_HIDD_REPORT_ERR_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70af126ad65594f1cc558ad0a0d17b2029e"></a> enumerator BK\_HIDD\_REPORT\_ERR\_EVT
    :   When HID device report handshanke error to lower layer, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t22BK_HIDD_GET_REPORT_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t22BK_HIDD_GET_REPORT_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t22BK_HIDD_GET_REPORT_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a9c03f25cdd98d04fb7812eacecd4b5d9"></a> enumerator BK\_HIDD\_GET\_REPORT\_EVT
    :   When HID device receives GET\_REPORT request from host, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t22BK_HIDD_SET_REPORT_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t22BK_HIDD_SET_REPORT_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t22BK_HIDD_SET_REPORT_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70ad8d53082060086c0646bbb24a362bbd6"></a> enumerator BK\_HIDD\_SET\_REPORT\_EVT
    :   When HID device receives SET\_REPORT request from host, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t24BK_HIDD_GET_PROTOCOL_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t24BK_HIDD_GET_PROTOCOL_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t24BK_HIDD_GET_PROTOCOL_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70aae979616083221282b50e61a4a1be851"></a> enumerator BK\_HIDD\_GET\_PROTOCOL\_EVT
    :   When HID device receives GET\_PROTOCOL request from host, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t24BK_HIDD_SET_PROTOCOL_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t24BK_HIDD_SET_PROTOCOL_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t24BK_HIDD_SET_PROTOCOL_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a6d9a5e8b60464b36454375a1b1f34be3"></a> enumerator BK\_HIDD\_SET\_PROTOCOL\_EVT
    :   When HID device receives SET\_PROTOCOL request from host, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t20BK_HIDD_GET_IDLE_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t20BK_HIDD_GET_IDLE_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t20BK_HIDD_GET_IDLE_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a83821a84e0f5fa2a5b75f31fb2e31d3c"></a> enumerator BK\_HIDD\_GET\_IDLE\_EVT
    :   When HID device receives GET\_IDLE request from host, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t20BK_HIDD_SET_IDLE_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t20BK_HIDD_SET_IDLE_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t20BK_HIDD_SET_IDLE_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a073747404be68e0ee95a9beb00420c17"></a> enumerator BK\_HIDD\_SET\_IDLE\_EVT
    :   When HID device receives SET\_IDLE request from host, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t21BK_HIDD_INTR_DATA_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t21BK_HIDD_INTR_DATA_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t21BK_HIDD_INTR_DATA_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a0ba05fa3fcd29fbfc89422bcfe0341f1"></a> enumerator BK\_HIDD\_INTR\_DATA\_EVT
    :   When HID device receives DATA from host on intr, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t19BK_HIDD_CONTROL_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t19BK_HIDD_CONTROL_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t19BK_HIDD_CONTROL_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70af4d9605c0e2f363517aad9da4fe66dd6"></a> enumerator BK\_HIDD\_CONTROL\_EVT
    :   When HID device receives HID\_CONTROL from host, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t21BK_HIDD_VC_UNPLUG_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t21BK_HIDD_VC_UNPLUG_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t21BK_HIDD_VC_UNPLUG_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a12aed72d329de6cbebc01b1c8f18e869"></a> enumerator BK\_HIDD\_VC\_UNPLUG\_EVT
    :   When HID device initiates Virtual Cable Unplug, the event comes

    <a id="_CPPv4N18bk_hidd_cb_event_t19BK_HIDD_API_ERR_EVTE"></a>

    <a id="_CPPv3N18bk_hidd_cb_event_t19BK_HIDD_API_ERR_EVTE"></a> <a id="_CPPv2N18bk_hidd_cb_event_t19BK_HIDD_API_ERR_EVTE"></a> <a id="bk__dm__hidd_8h_1a03c12bc08bee0af46fdf42c2adea1b70a8710797c3c9e907944d1fa40929c4732"></a> enumerator BK\_HIDD\_API\_ERR\_EVT
    :   When HID device has API error, the event comes

<a id="_CPPv416bk_hidd_status_t"></a>

<a id="_CPPv316bk_hidd_status_t"></a> <a id="_CPPv216bk_hidd_status_t"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29e"></a> enum bk\_hidd\_status\_t
:   *Values:*

    <a id="_CPPv4N16bk_hidd_status_t15BK_HIDD_SUCCESSE"></a>

    <a id="_CPPv3N16bk_hidd_status_t15BK_HIDD_SUCCESSE"></a> <a id="_CPPv2N16bk_hidd_status_t15BK_HIDD_SUCCESSE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29ea746662fceb0259aba579d1aac00d9d74"></a> enumerator BK\_HIDD\_SUCCESS

    <a id="_CPPv4N16bk_hidd_status_t13BK_HIDD_ERRORE"></a>

    <a id="_CPPv3N16bk_hidd_status_t13BK_HIDD_ERRORE"></a> <a id="_CPPv2N16bk_hidd_status_t13BK_HIDD_ERRORE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29eae89ed0b310cc1a90fce7db1ceeda388b"></a> enumerator BK\_HIDD\_ERROR
    :   general BK HD error

    <a id="_CPPv4N16bk_hidd_status_t14BK_HIDD_NO_RESE"></a>

    <a id="_CPPv3N16bk_hidd_status_t14BK_HIDD_NO_RESE"></a> <a id="_CPPv2N16bk_hidd_status_t14BK_HIDD_NO_RESE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29eadb7d778b606cbba9b34a6a8daa1313f7"></a> enumerator BK\_HIDD\_NO\_RES
    :   out of system resources

    <a id="_CPPv4N16bk_hidd_status_t12BK_HIDD_BUSYE"></a>

    <a id="_CPPv3N16bk_hidd_status_t12BK_HIDD_BUSYE"></a> <a id="_CPPv2N16bk_hidd_status_t12BK_HIDD_BUSYE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29ea083dbe74c7447035c1f9708730e6e7a8"></a> enumerator BK\_HIDD\_BUSY
    :   Temporarily can not handle this request.

    <a id="_CPPv4N16bk_hidd_status_t15BK_HIDD_NO_DATAE"></a>

    <a id="_CPPv3N16bk_hidd_status_t15BK_HIDD_NO_DATAE"></a> <a id="_CPPv2N16bk_hidd_status_t15BK_HIDD_NO_DATAE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29ea19b398f3145fae6f3a71c94bca063e17"></a> enumerator BK\_HIDD\_NO\_DATA
    :   No data.

    <a id="_CPPv4N16bk_hidd_status_t17BK_HIDD_NEED_INITE"></a>

    <a id="_CPPv3N16bk_hidd_status_t17BK_HIDD_NEED_INITE"></a> <a id="_CPPv2N16bk_hidd_status_t17BK_HIDD_NEED_INITE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29ea71223d868b3e6c60cdf2e7c5e7ffa332"></a> enumerator BK\_HIDD\_NEED\_INIT
    :   HIDD module shall init first

    <a id="_CPPv4N16bk_hidd_status_t19BK_HIDD_NEED_DEINITE"></a>

    <a id="_CPPv3N16bk_hidd_status_t19BK_HIDD_NEED_DEINITE"></a> <a id="_CPPv2N16bk_hidd_status_t19BK_HIDD_NEED_DEINITE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29ea2da184429e9aebe178c3895085fa985d"></a> enumerator BK\_HIDD\_NEED\_DEINIT
    :   HIDD module shall deinit first

    <a id="_CPPv4N16bk_hidd_status_t16BK_HIDD_NEED_REGE"></a>

    <a id="_CPPv3N16bk_hidd_status_t16BK_HIDD_NEED_REGE"></a> <a id="_CPPv2N16bk_hidd_status_t16BK_HIDD_NEED_REGE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29ea79039f07609e8ef87a6a9ab745542eb4"></a> enumerator BK\_HIDD\_NEED\_REG
    :   HIDD module shall register first

    <a id="_CPPv4N16bk_hidd_status_t18BK_HIDD_NEED_DEREGE"></a>

    <a id="_CPPv3N16bk_hidd_status_t18BK_HIDD_NEED_DEREGE"></a> <a id="_CPPv2N16bk_hidd_status_t18BK_HIDD_NEED_DEREGE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29ea2c6434bdaaf295cf569bd9bde3d95a16"></a> enumerator BK\_HIDD\_NEED\_DEREG
    :   HIDD module shall deregister first

    <a id="_CPPv4N16bk_hidd_status_t21BK_HIDD_NO_CONNECTIONE"></a>

    <a id="_CPPv3N16bk_hidd_status_t21BK_HIDD_NO_CONNECTIONE"></a> <a id="_CPPv2N16bk_hidd_status_t21BK_HIDD_NO_CONNECTIONE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29eaa4e837c4e0cd1be0b7efe7be35ca3aff"></a> enumerator BK\_HIDD\_NO\_CONNECTION
    :   connection may have been closed

    <a id="_CPPv4N16bk_hidd_status_t19BK_HIDD_NO_ACL_LINKE"></a>

    <a id="_CPPv3N16bk_hidd_status_t19BK_HIDD_NO_ACL_LINKE"></a> <a id="_CPPv2N16bk_hidd_status_t19BK_HIDD_NO_ACL_LINKE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29eabbaee867767d1744caae1f9d9a7bca4c"></a> enumerator BK\_HIDD\_NO\_ACL\_LINK
    :   Baseband acl link not exist

    <a id="_CPPv4N16bk_hidd_status_t12BK_HIDD_FAILE"></a>

    <a id="_CPPv3N16bk_hidd_status_t12BK_HIDD_FAILE"></a> <a id="_CPPv2N16bk_hidd_status_t12BK_HIDD_FAILE"></a> <a id="bk__dm__hidd_8h_1afd77dc7a1c3c68caa402a69e072fc29ea3993a070d73cb2a076996dd1ca522511"></a> enumerator BK\_HIDD\_FAIL
    :   HIDD Fail

<a id="bk-dm-hidh-h"></a>

## bk\_dm\_hidh.h

`bk_dm_hidh.h` 提供 Bluetooth HID Host profile 接口。

<a id="id12"></a>

### Header File

- [bk\_dm\_hidh.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_hidh.h)

<a id="id13"></a>

### Functions

<a id="_CPPv432bk_bt_hid_host_register_callback10bk_hh_cb_t"></a>

<a id="_CPPv332bk_bt_hid_host_register_callback10bk_hh_cb_t"></a> <a id="_CPPv232bk_bt_hid_host_register_callback10bk_hh_cb_t"></a> <a id="bk_bt_hid_host_register_callback__bk_hh_cb_t"></a> <a id="bk__dm__hidh_8h_1a54ac53bd80ea0cf5e50ba4b6b8733ef2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_register\_callback([bk\_hh\_cb\_t](#_CPPv410bk_hh_cb_t "bk_hh_cb_t") callback)
:   This function is called to init callbacks with HID host module.

    参数
    :   **callback** – **\[in\]** pointer to the init callback function.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv419bk_bt_hid_host_initv"></a>

<a id="_CPPv319bk_bt_hid_host_initv"></a> <a id="_CPPv219bk_bt_hid_host_initv"></a> <a id="bk_bt_hid_host_init__void"></a> <a id="bk__dm__hidh_8h_1ac8be628a7c55a499df6f4fe912319c44"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_init(void)
:   This function initializes HID host. This function should be called after [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2) success, and should be called after bk\_bt\_hid\_host\_register\_callback(). When the operation is complete the callback function will be called with BK\_HIDH\_INIT\_EVT.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv421bk_bt_hid_host_deinitv"></a>

<a id="_CPPv321bk_bt_hid_host_deinitv"></a> <a id="_CPPv221bk_bt_hid_host_deinitv"></a> <a id="bk_bt_hid_host_deinit__void"></a> <a id="bk__dm__hidh_8h_1ab8c64c8cfbd0db789637d0e918dc8519"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_deinit(void)
:   Closes the interface. This function should be called after [bk\_bluetooth\_init()](dual_ble.md#group__dm__bluetooth_1ga577c57a04b4b4589adfb5736442015a2) success, and should be called after bk\_bt\_hid\_host\_init(). When the operation is complete the callback function will be called with BK\_HIDH\_DEINIT\_EVT.

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="_CPPv422bk_bt_hid_host_connect12bk_bd_addr_t"></a>

<a id="_CPPv322bk_bt_hid_host_connect12bk_bd_addr_t"></a> <a id="_CPPv222bk_bt_hid_host_connect12bk_bd_addr_t"></a> <a id="bk_bt_hid_host_connect__bk_bd_addr_t"></a> <a id="bk__dm__hidh_8h_1aaee37ba345afcdd67aeb952ffdf066dc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_connect([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   Connect to HID device. When the operation is complete the callback function will be called with BK\_HIDH\_OPEN\_EVT.

    参数
    :   **bd\_addr** – **\[in\]** Remote device bluetooth device address.

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="_CPPv425bk_bt_hid_host_disconnect12bk_bd_addr_t"></a>

<a id="_CPPv325bk_bt_hid_host_disconnect12bk_bd_addr_t"></a> <a id="_CPPv225bk_bt_hid_host_disconnect12bk_bd_addr_t"></a> <a id="bk_bt_hid_host_disconnect__bk_bd_addr_t"></a> <a id="bk__dm__hidh_8h_1ac13289ca8b377b0c497696667fadb238"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_disconnect([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   Disconnect from HID device. When the operation is complete the callback function will be called with BK\_HIDH\_CLOSE\_EVT.

    参数
    :   **bd\_addr** – **\[in\]** Remote device bluetooth device address.

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="_CPPv435bk_bt_hid_host_virtual_cable_unplug12bk_bd_addr_t"></a>

<a id="_CPPv335bk_bt_hid_host_virtual_cable_unplug12bk_bd_addr_t"></a> <a id="_CPPv235bk_bt_hid_host_virtual_cable_unplug12bk_bd_addr_t"></a> <a id="bk_bt_hid_host_virtual_cable_unplug__bk_bd_addr_t"></a> <a id="bk__dm__hidh_8h_1a98784f040a59e60f10b8b887e15e0e30"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_virtual\_cable\_unplug([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   Virtual UnPlug (VUP) the specified HID device. When the operation is complete the callback function will be called with BK\_HIDH\_VC\_UNPLUG\_EVT.

    参数
    :   **bd\_addr** – **\[in\]** Remote device bluetooth device address.

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="_CPPv423bk_bt_hid_host_set_info12bk_bd_addr_tP18bk_hidh_hid_info_t"></a>

<a id="_CPPv323bk_bt_hid_host_set_info12bk_bd_addr_tP18bk_hidh_hid_info_t"></a> <a id="_CPPv223bk_bt_hid_host_set_info12bk_bd_addr_tP18bk_hidh_hid_info_t"></a> <a id="bk_bt_hid_host_set_info__bk_bd_addr_t.bk_hidh_hid_info_tP"></a> <a id="bk__dm__hidh_8h_1a9d06ed86bb31e7397e94e388bcd928fd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_set\_info([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, [bk\_hidh\_hid\_info\_t](#_CPPv418bk_hidh_hid_info_t "bk_hidh_hid_info_t") \*hid\_info)
:   Set the HID device descriptor for the specified HID device. When the operation is complete the callback function will be called with BK\_HIDH\_SET\_INFO\_EVT.

    参数
    :   - **bd\_addr** – **\[in\]** Remote device bluetooth device address.
        - **hid\_info** – **\[in\]** HID device descriptor structure.

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="_CPPv427bk_bt_hid_host_get_protocol12bk_bd_addr_t"></a>

<a id="_CPPv327bk_bt_hid_host_get_protocol12bk_bd_addr_t"></a> <a id="_CPPv227bk_bt_hid_host_get_protocol12bk_bd_addr_t"></a> <a id="bk_bt_hid_host_get_protocol__bk_bd_addr_t"></a> <a id="bk__dm__hidh_8h_1af7ca416613d7e4efc36719b267df8583"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_get\_protocol([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   Get the HID proto mode. When the operation is complete the callback function will be called with BK\_HIDH\_GET\_PROTO\_EVT.

    参数
    :   **bd\_addr** – **\[in\]** Remote device bluetooth device address.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv427bk_bt_hid_host_set_protocol12bk_bd_addr_t23bk_hidh_protocol_mode_t"></a>

<a id="_CPPv327bk_bt_hid_host_set_protocol12bk_bd_addr_t23bk_hidh_protocol_mode_t"></a> <a id="_CPPv227bk_bt_hid_host_set_protocol12bk_bd_addr_t23bk_hidh_protocol_mode_t"></a> <a id="bk_bt_hid_host_set_protocol__bk_bd_addr_t.bk_hidh_protocol_mode_t"></a> <a id="bk__dm__hidh_8h_1a3d5086b0614c513f757c9f89e8a3f57b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_set\_protocol([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, [bk\_hidh\_protocol\_mode\_t](#_CPPv423bk_hidh_protocol_mode_t "bk_hidh_protocol_mode_t") protocol\_mode)
:   Set the HID proto mode. When the operation is complete the callback function will be called with BK\_HIDH\_SET\_PROTO\_EVT.

    参数
    :   - **bd\_addr** – **\[in\]** Remote device bluetooth device address.
        - **protocol\_mode** – **\[in\]** Protocol mode type.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv425bk_bt_hid_host_get_report12bk_bd_addr_t21bk_hidh_report_type_t7uint8_ti"></a>

<a id="_CPPv325bk_bt_hid_host_get_report12bk_bd_addr_t21bk_hidh_report_type_t7uint8_ti"></a> <a id="_CPPv225bk_bt_hid_host_get_report12bk_bd_addr_t21bk_hidh_report_type_t7uint8_ti"></a> <a id="bk_bt_hid_host_get_report__bk_bd_addr_t.bk_hidh_report_type_t.uint8_t.i"></a> <a id="bk__dm__hidh_8h_1a0727eecb2424712475019ea0fe22bb30"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_get\_report([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, [bk\_hidh\_report\_type\_t](#_CPPv421bk_hidh_report_type_t "bk_hidh_report_type_t") report\_type, uint8\_t report\_id, int buffer\_size)
:   Send a GET\_REPORT to HID device. When the operation is complete the callback function will be called with BK\_HIDH\_GET\_RPT\_EVT.

    参数
    :   - **bd\_addr** – **\[in\]** Remote device bluetooth device address.
        - **report\_type** – **\[in\]** Report type
        - **report\_id** – **\[in\]** Report id
        - **buffer\_size** – **\[in\]** Buffer size

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="_CPPv425bk_bt_hid_host_set_report12bk_bd_addr_t21bk_hidh_report_type_tP7uint8_t6size_t"></a>

<a id="_CPPv325bk_bt_hid_host_set_report12bk_bd_addr_t21bk_hidh_report_type_tP7uint8_t6size_t"></a> <a id="_CPPv225bk_bt_hid_host_set_report12bk_bd_addr_t21bk_hidh_report_type_tP7uint8_t6size_t"></a> <a id="bk_bt_hid_host_set_report__bk_bd_addr_t.bk_hidh_report_type_t.uint8_tP.s"></a> <a id="bk__dm__hidh_8h_1aeb35fef15703216ab3f702bd820e68a7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_set\_report([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, [bk\_hidh\_report\_type\_t](#_CPPv421bk_hidh_report_type_t "bk_hidh_report_type_t") report\_type, uint8\_t \*report, size\_t len)
:   Send a SET\_REPORT to HID device. When the operation is complete the callback function will be called with BK\_HIDH\_SET\_RPT\_EVT.

    参数
    :   - **bd\_addr** – **\[in\]** Remote device bluetooth device address.
        - **report\_type** – **\[in\]** Report type
        - **report** – **\[in\]** Report data pointer
        - **len** – **\[in\]** Report data length

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="_CPPv424bk_bt_hid_host_send_data12bk_bd_addr_tP7uint8_t6size_t"></a>

<a id="_CPPv324bk_bt_hid_host_send_data12bk_bd_addr_tP7uint8_t6size_t"></a> <a id="_CPPv224bk_bt_hid_host_send_data12bk_bd_addr_tP7uint8_t6size_t"></a> <a id="bk_bt_hid_host_send_data__bk_bd_addr_t.uint8_tP.s"></a> <a id="bk__dm__hidh_8h_1adefddc8c25a1b6a68b82074802aaaaab"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_send\_data([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr, uint8\_t \*data, size\_t len)
:   Send data to HID device. When the operation is complete the callback function will be called with BK\_HIDH\_DATA\_EVT.

    参数
    :   - **bd\_addr** – **\[in\]** Remote device bluetooth device address.
        - **data** – **\[in\]** Data pointer
        - **len** – **\[in\]** Data length

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="_CPPv423bk_bt_hid_host_sdp_dscp12bk_bd_addr_t"></a>

<a id="_CPPv323bk_bt_hid_host_sdp_dscp12bk_bd_addr_t"></a> <a id="_CPPv223bk_bt_hid_host_sdp_dscp12bk_bd_addr_t"></a> <a id="bk_bt_hid_host_sdp_dscp__bk_bd_addr_t"></a> <a id="bk__dm__hidh_8h_1a085674d690ea882f8ed14771378cd402"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_hid\_host\_sdp\_dscp([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   Start SDP. When the operation is complete the callback function will be called with BK\_HIDH\_SDP\_DSCP\_EVT.

    参数
    :   **bd\_addr** – **\[in\]** Remote device bluetooth device address.

    返回
    :   \- BK\_OK: success

        - other: failed

<a id="id14"></a>

### Unions

<a id="_CPPv418bk_hidh_cb_param_t"></a>

<a id="_CPPv318bk_hidh_cb_param_t"></a> <a id="_CPPv218bk_hidh_cb_param_t"></a> <a id="unionbk__hidh__cb__param__t"></a> union bk\_hidh\_cb\_param\_t
:   *#include \<bk\_dm\_hidh.h\>*

    HID host callback parameters union.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_hidh_cb_param_t4initE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t4initE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t4initE"></a> <a id="bk_hidh_cb_param_t::init__bk_hidh_cb_param_t::hidh_init_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1aad014b8f3c1b81b408745b7283da456f"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_init\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t19hidh_init_evt_paramE "bk_hidh_cb_param_t::hidh_init_evt_param") init
    :   HIDH callback param of BK\_HIDH\_INIT\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t6deinitE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t6deinitE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t6deinitE"></a> <a id="bk_hidh_cb_param_t::deinit__bk_hidh_cb_param_t::hidh_uninit_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1adc5d47d3939d7ce3d0aa5454d71ebdd9"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_uninit\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t21hidh_uninit_evt_paramE "bk_hidh_cb_param_t::hidh_uninit_evt_param") deinit
    :   HIDH callback param of BK\_HIDH\_DEINIT\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t4openE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t4openE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t4openE"></a> <a id="bk_hidh_cb_param_t::open__bk_hidh_cb_param_t::hidh_open_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a59802d5b47a8727f5f44700ae90bba36"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_open\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t19hidh_open_evt_paramE "bk_hidh_cb_param_t::hidh_open_evt_param") open
    :   HIDH callback param of BK\_HIDH\_OPEN\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t5closeE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t5closeE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t5closeE"></a> <a id="bk_hidh_cb_param_t::close__bk_hidh_cb_param_t::hidh_close_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a90fb63baa45bbfc299b0de5627756275"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_close\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t20hidh_close_evt_paramE "bk_hidh_cb_param_t::hidh_close_evt_param") close
    :   HIDH callback param of BK\_HIDH\_CLOSE\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t6unplugE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t6unplugE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t6unplugE"></a> <a id="bk_hidh_cb_param_t::unplug__bk_hidh_cb_param_t::hidh_unplug_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a948964e99b5c31d3725c2e9a53acea7b"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_unplug\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t21hidh_unplug_evt_paramE "bk_hidh_cb_param_t::hidh_unplug_evt_param") unplug
    :   HIDH callback param of BK\_HIDH\_VC\_UNPLUG\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t9get_protoE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t9get_protoE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t9get_protoE"></a> <a id="bk_hidh_cb_param_t::get_proto__bk_hidh_cb_param_t::hidh_get_proto_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1aef0cc1bd5ee804b969ea243725f35e71"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_get\_proto\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t24hidh_get_proto_evt_paramE "bk_hidh_cb_param_t::hidh_get_proto_evt_param") get\_proto
    :   HIDH callback param of BK\_HIDH\_GET\_PROTO\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t9set_protoE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t9set_protoE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t9set_protoE"></a> <a id="bk_hidh_cb_param_t::set_proto__bk_hidh_cb_param_t::hidh_set_proto_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a9eac8700b5588cb6950c39919667bc73"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_set\_proto\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t24hidh_set_proto_evt_paramE "bk_hidh_cb_param_t::hidh_set_proto_evt_param") set\_proto
    :   HIDH callback param of BK\_HIDH\_SET\_PROTO\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t7get_rptE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t7get_rptE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t7get_rptE"></a> <a id="bk_hidh_cb_param_t::get_rpt__bk_hidh_cb_param_t::hidh_get_rpt_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a059d068dac45dab27396a346e5b26d60"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_get\_rpt\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t22hidh_get_rpt_evt_paramE "bk_hidh_cb_param_t::hidh_get_rpt_evt_param") get\_rpt
    :   HIDH callback param of BK\_HIDH\_GET\_RPT\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t7set_rptE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t7set_rptE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t7set_rptE"></a> <a id="bk_hidh_cb_param_t::set_rpt__bk_hidh_cb_param_t::hidh_set_rpt_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a359ad367d4330937cc3fd0bbc4215cac"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_set\_rpt\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t22hidh_set_rpt_evt_paramE "bk_hidh_cb_param_t::hidh_set_rpt_evt_param") set\_rpt
    :   HIDH callback param of BK\_HIDH\_SET\_RPT\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t9send_dataE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t9send_dataE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t9send_dataE"></a> <a id="bk_hidh_cb_param_t::send_data__bk_hidh_cb_param_t::hidh_send_data_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a33e13685889bb556bcdce6fff1c7b312"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_send\_data\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t24hidh_send_data_evt_paramE "bk_hidh_cb_param_t::hidh_send_data_evt_param") send\_data
    :   HIDH callback param of BK\_HIDH\_DATA\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t8data_indE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t8data_indE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t8data_indE"></a> <a id="bk_hidh_cb_param_t::data_ind__bk_hidh_cb_param_t::hidh_data_ind_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a83f1eccacdf86bf9cd35ee4b3044d906"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_data\_ind\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t23hidh_data_ind_evt_paramE "bk_hidh_cb_param_t::hidh_data_ind_evt_param") data\_ind
    :   HIDH callback param of BK\_HIDH\_DATA\_IND\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t7add_devE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t7add_devE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t7add_devE"></a> <a id="bk_hidh_cb_param_t::add_dev__bk_hidh_cb_param_t::hidh_add_dev_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a385d516c2e936ef5320a90b3ecfccb6d"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_add\_dev\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t22hidh_add_dev_evt_paramE "bk_hidh_cb_param_t::hidh_add_dev_evt_param") add\_dev
    :   HIDH callback param of BK\_HIDH\_ADD\_DEV\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t7rmv_devE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t7rmv_devE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t7rmv_devE"></a> <a id="bk_hidh_cb_param_t::rmv_dev__bk_hidh_cb_param_t::hidh_rmv_dev_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1aec80c1ae442a064579fff0ff84469936"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_rmv\_dev\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_paramE "bk_hidh_cb_param_t::hidh_rmv_dev_evt_param") rmv\_dev
    :   HIDH callback param of BK\_HIDH\_RMV\_DEV\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t8sdp_dscpE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t8sdp_dscpE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t8sdp_dscpE"></a> <a id="bk_hidh_cb_param_t::sdp_dscp__bk_hidh_cb_param_t::hidh_get_dscp_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a6ccea7195ea9f14381b311f45c396173"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_get\_dscp\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_paramE "bk_hidh_cb_param_t::hidh_get_dscp_evt_param") sdp\_dscp
    :   HIDH callback param of BK\_HIDH\_GET\_DSCP\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t8set_infoE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t8set_infoE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t8set_infoE"></a> <a id="bk_hidh_cb_param_t::set_info__bk_hidh_cb_param_t::hidh_set_info_evt_param"></a> <a id="unionbk__hidh__cb__param__t_1a88eda729cee489824228e88e68085861"></a> struct [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t")::[hidh\_set\_info\_evt\_param](#_CPPv4N18bk_hidh_cb_param_t23hidh_set_info_evt_paramE "bk_hidh_cb_param_t::hidh_set_info_evt_param") set\_info
    :   HIDH callback param of BK\_HIDH\_SET\_INFO\_EVT

    <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_add_dev_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_add_dev_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_add_dev_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_add_dev_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__add__dev__evt__param"></a> struct hidh\_add\_dev\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_ADD\_DEV\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_add_dev_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_add_dev_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_add_dev_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_add_dev_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__add__dev__evt__param_1ac1afca34a6340569c9188238fa2fb3a2"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_add_dev_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_add_dev_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_add_dev_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_add_dev_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__add__dev__evt__param_1a3ee4e7f31c5d4a556cb4ebee00ac70f0"></a> uint8\_t handle
        :   device handle

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_add_dev_evt_param7bd_addrE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_add_dev_evt_param7bd_addrE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_add_dev_evt_param7bd_addrE"></a> <a id="bk_hidh_cb_param_t::hidh_add_dev_evt_param::bd_addr__bk_bd_addr_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__add__dev__evt__param_1aa8c235a7e55f783f7b4ee3e2af78ab41"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
        :   device address

    <a id="_CPPv4N18bk_hidh_cb_param_t20hidh_close_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t20hidh_close_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t20hidh_close_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_close_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__close__evt__param"></a> struct hidh\_close\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_CLOSE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t20hidh_close_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t20hidh_close_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t20hidh_close_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_close_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__close__evt__param_1aa5a1a74c9bc1b500460c31cc9c16167c"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t20hidh_close_evt_param11conn_statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t20hidh_close_evt_param11conn_statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t20hidh_close_evt_param11conn_statusE"></a> <a id="bk_hidh_cb_param_t::hidh_close_evt_param::conn_status__bk_hidh_connection_state_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__close__evt__param_1a835783ffe366415ccffec65a0db16e16"></a> [bk\_hidh\_connection\_state\_t](#_CPPv426bk_hidh_connection_state_t "bk_hidh_connection_state_t") conn\_status
        :   connection status

        <a id="_CPPv4N18bk_hidh_cb_param_t20hidh_close_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t20hidh_close_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t20hidh_close_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_close_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__close__evt__param_1a111dd137eb9928bcb6da565980aae7d8"></a> uint8\_t handle
        :   device handle

    <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_data_ind_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_data_ind_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_data_ind_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_data_ind_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__data__ind__evt__param"></a> struct hidh\_data\_ind\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_DATA\_IND\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_data_ind_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_data_ind_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_data_ind_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_data_ind_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__data__ind__evt__param_1a88b311bd696311fb606edf50470c8878"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_data_ind_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_data_ind_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_data_ind_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_data_ind_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__data__ind__evt__param_1ae0a1dd653172461a7cbd92d2ecd455ed"></a> uint8\_t handle
        :   device handle

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_data_ind_evt_param10proto_modeE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_data_ind_evt_param10proto_modeE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_data_ind_evt_param10proto_modeE"></a> <a id="bk_hidh_cb_param_t::hidh_data_ind_evt_param::proto_mode__bk_hidh_protocol_mode_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__data__ind__evt__param_1adbfd304aeb922b143a9f1050d961be3e"></a> [bk\_hidh\_protocol\_mode\_t](#_CPPv423bk_hidh_protocol_mode_t "bk_hidh_protocol_mode_t") proto\_mode
        :   protocol mode

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_data_ind_evt_param3lenE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_data_ind_evt_param3lenE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_data_ind_evt_param3lenE"></a> <a id="bk_hidh_cb_param_t::hidh_data_ind_evt_param::len__uint16_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__data__ind__evt__param_1ab061fab650f335651e02fe871f28cdbe"></a> uint16\_t len
        :   data length

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_data_ind_evt_param4dataE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_data_ind_evt_param4dataE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_data_ind_evt_param4dataE"></a> <a id="bk_hidh_cb_param_t::hidh_data_ind_evt_param::data__uint8_tP"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__data__ind__evt__param_1aceb1827cb9558d49cf57d4d1d478e967"></a> uint8\_t \*data
        :   data pointer

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_data_ind_evt_param11report_typeE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_data_ind_evt_param11report_typeE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_data_ind_evt_param11report_typeE"></a> <a id="bk_hidh_cb_param_t::hidh_data_ind_evt_param::report_type__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__data__ind__evt__param_1a98d481ebd2fa14ce9bc75b67a19130ef"></a> uint8\_t report\_type
        :   report type

    <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param"></a> struct hidh\_get\_dscp\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_SDP\_DSCP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1ac9035ba40a315156ae31442a73af8815"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param9sub_classE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param9sub_classE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param9sub_classE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::sub_class__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a1c3299ff30769fa6cde6850bc530ad5e"></a> uint8\_t sub\_class
        :   HIDDeviceSubclass

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11reconn_initE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11reconn_initE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11reconn_initE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::reconn_init__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1ab36815c77afbed3c861b36957e126fad"></a> uint8\_t reconn\_init
        :   HIDReconnectInitiate

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11normal_connE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11normal_connE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11normal_connE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::normal_conn__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1af0fc788ab6b6c13ae227970310b7caec"></a> uint8\_t normal\_conn
        :   HIDNormallyConnectable

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param15ssr_max_latencyE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param15ssr_max_latencyE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param15ssr_max_latencyE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::ssr_max_latency__uint16_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a003f00c12a0fd1eb05b47a71124e1622"></a> uint16\_t ssr\_max\_latency
        :   SSR max latency in slots

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param12ssr_min_toutE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param12ssr_min_toutE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param12ssr_min_toutE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::ssr_min_tout__uint16_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a4405a4fdcd4bc5c0b18ad871e68f2fbd"></a> uint16\_t ssr\_min\_tout
        :   SSR min timeout in slots

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param9ctry_codeE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param9ctry_codeE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param9ctry_codeE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::ctry_code__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1adb163597fa01d1b4f4f33de58c5d46df"></a> uint8\_t ctry\_code
        :   Country Code

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param13parse_versionE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param13parse_versionE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param13parse_versionE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::parse_version__uint16_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a71fe21fdcf49ab90b385ffc04e799b58"></a> uint16\_t parse\_version
        :   Parse Version

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param13virtual_cableE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param13virtual_cableE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param13virtual_cableE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::virtual_cable__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a56dc6555e236964d7fd21f00d4ad0383"></a> uint8\_t virtual\_cable
        :   Virtual Cable

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11boot_deviceE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11boot_deviceE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11boot_deviceE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::boot_device__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a35ba87b815268fbb04de0464a19e4731"></a> uint8\_t boot\_device
        :   Boot device

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11remote_wakeE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11remote_wakeE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param11remote_wakeE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::remote_wake__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a39b190723aa802a6d6a54247f978e66d"></a> uint8\_t remote\_wake
        :   HIDRemoteWake

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param13battery_powerE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param13battery_powerE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param13battery_powerE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::battery_power__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a9ede837c1e119a64f3056f27b5bda22c"></a> uint8\_t battery\_power
        :   HIDBatteryPower

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param9vendor_idE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param9vendor_idE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param9vendor_idE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::vendor_id__uint16_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a319283f4226cb2a0e48349ac0743a782"></a> uint16\_t vendor\_id
        :   Device Vendor ID

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param10product_idE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param10product_idE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param10product_idE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::product_id__uint16_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a88010f604c1c85b20d96833018e3f81a"></a> uint16\_t product\_id
        :   Device Product ID

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param14device_versionE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param14device_versionE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param14device_versionE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::device_version__uint16_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a0aac111156ce9cb245d04aa4d8708b98"></a> uint16\_t device\_version
        :   Device Version

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param6dl_lenE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param6dl_lenE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param6dl_lenE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::dl_len__uint16_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1aa3af83e22ae598ad2f37109db17b3505"></a> uint16\_t dl\_len
        :   Device descriptor length

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param8dsc_listE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param8dsc_listE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param8dsc_listE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::dsc_list__uint8_tP"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1a38f67022300d0c0b7d4aa3d98e0cc89e"></a> uint8\_t \*dsc\_list
        :   Device descriptor pointer

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param8dsc_typeE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param8dsc_typeE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_get_dscp_evt_param8dsc_typeE"></a> <a id="bk_hidh_cb_param_t::hidh_get_dscp_evt_param::dsc_type__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__dscp__evt__param_1ae8612c253749b0ec6e7260196810ef34"></a> uint8\_t dsc\_type
        :   Device ClassDescriptor type

    <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_get_proto_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_get_proto_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_get_proto_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_get_proto_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__proto__evt__param"></a> struct hidh\_get\_proto\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_GET\_PROTO\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_get_proto_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_get_proto_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_get_proto_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_get_proto_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__proto__evt__param_1ace62634806fdc63bd405f8c42e357717"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_get_proto_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_get_proto_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_get_proto_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_get_proto_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__proto__evt__param_1a702cf5cec803bee295e23008539616a0"></a> uint8\_t handle
        :   device handle

        <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_get_proto_evt_param10proto_modeE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_get_proto_evt_param10proto_modeE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_get_proto_evt_param10proto_modeE"></a> <a id="bk_hidh_cb_param_t::hidh_get_proto_evt_param::proto_mode__bk_hidh_protocol_mode_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__proto__evt__param_1a015b6f42d74aed1d8702ad73174d9233"></a> [bk\_hidh\_protocol\_mode\_t](#_CPPv423bk_hidh_protocol_mode_t "bk_hidh_protocol_mode_t") proto\_mode
        :   protocol mode

    <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_get_rpt_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_get_rpt_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_get_rpt_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_get_rpt_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__rpt__evt__param"></a> struct hidh\_get\_rpt\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_GET\_RPT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_get_rpt_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__rpt__evt__param_1a42e6a4f76e3ec05237c03d2b3fea93a2"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_get_rpt_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__rpt__evt__param_1a25346fe277a63cc397b3059acd74e7f5"></a> uint8\_t handle
        :   device handle

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param3lenE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param3lenE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param3lenE"></a> <a id="bk_hidh_cb_param_t::hidh_get_rpt_evt_param::len__uint16_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__rpt__evt__param_1a040922bdf86370c65b9ce32d985eb3b1"></a> uint16\_t len
        :   data length

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param4dataE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param4dataE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_get_rpt_evt_param4dataE"></a> <a id="bk_hidh_cb_param_t::hidh_get_rpt_evt_param::data__uint8_tP"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__get__rpt__evt__param_1a669ca6a2d0b8a9b95db0870d08b958bf"></a> uint8\_t \*data
        :   data pointer

    <a id="_CPPv4N18bk_hidh_cb_param_t19hidh_init_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t19hidh_init_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t19hidh_init_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_init_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__init__evt__param"></a> struct hidh\_init\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_INIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t19hidh_init_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t19hidh_init_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t19hidh_init_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_init_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__init__evt__param_1acade543b6418a4bb0de0d0c68ecdb084"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   status

    <a id="_CPPv4N18bk_hidh_cb_param_t19hidh_open_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t19hidh_open_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t19hidh_open_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_open_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__open__evt__param"></a> struct hidh\_open\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_OPEN\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t19hidh_open_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t19hidh_open_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t19hidh_open_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_open_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__open__evt__param_1a9f98df24bcaa6c08bdcd320873612950"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t19hidh_open_evt_param11conn_statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t19hidh_open_evt_param11conn_statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t19hidh_open_evt_param11conn_statusE"></a> <a id="bk_hidh_cb_param_t::hidh_open_evt_param::conn_status__bk_hidh_connection_state_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__open__evt__param_1a7ecbc69c1a978cd47bb312ec0ccf03e6"></a> [bk\_hidh\_connection\_state\_t](#_CPPv426bk_hidh_connection_state_t "bk_hidh_connection_state_t") conn\_status
        :   connection status

        <a id="_CPPv4N18bk_hidh_cb_param_t19hidh_open_evt_param7is_origE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t19hidh_open_evt_param7is_origE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t19hidh_open_evt_param7is_origE"></a> <a id="bk_hidh_cb_param_t::hidh_open_evt_param::is_orig__b"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__open__evt__param_1ac98ee134f24a68a31b9c758396dac044"></a> bool is\_orig
        :   indicate if host intiate the connection

        <a id="_CPPv4N18bk_hidh_cb_param_t19hidh_open_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t19hidh_open_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t19hidh_open_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_open_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__open__evt__param_1a758fd15f41a9841da4cce1ad7d299c4d"></a> uint8\_t handle
        :   device handle

        <a id="_CPPv4N18bk_hidh_cb_param_t19hidh_open_evt_param7bd_addrE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t19hidh_open_evt_param7bd_addrE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t19hidh_open_evt_param7bd_addrE"></a> <a id="bk_hidh_cb_param_t::hidh_open_evt_param::bd_addr__bk_bd_addr_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__open__evt__param_1ab53bf9a8e116e12d44fb3fb48007cce8"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
        :   device address

    <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_rmv_dev_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__rmv__dev__evt__param"></a> struct hidh\_rmv\_dev\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_RMV\_DEV\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_rmv_dev_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__rmv__dev__evt__param_1a2e673242042bab34ee8bb99a2a9e4e32"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_rmv_dev_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__rmv__dev__evt__param_1a399f3ebd33e29602b99ac258b2ad13aa"></a> uint8\_t handle
        :   device handle

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_param7bd_addrE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_param7bd_addrE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_rmv_dev_evt_param7bd_addrE"></a> <a id="bk_hidh_cb_param_t::hidh_rmv_dev_evt_param::bd_addr__bk_bd_addr_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__rmv__dev__evt__param_1a8bb4779ede7916f00a9e03673e748df2"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
        :   device address

    <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_send_data_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_send_data_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_send_data_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_send_data_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__send__data__evt__param"></a> struct hidh\_send\_data\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_DATA\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_send_data_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_send_data_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_send_data_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_send_data_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__send__data__evt__param_1afd620a93aa913913cb1c483a4bbeb350"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_send_data_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_send_data_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_send_data_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_send_data_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__send__data__evt__param_1ad8c4d2a989434f7b8f2b949b62e4c233"></a> uint8\_t handle
        :   device handle

        <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_send_data_evt_param6reasonE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_send_data_evt_param6reasonE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_send_data_evt_param6reasonE"></a> <a id="bk_hidh_cb_param_t::hidh_send_data_evt_param::reason__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__send__data__evt__param_1a0d41913f837b30fd16dee8fcadd0c1e3"></a> uint8\_t reason
        :   lower layer failed reason

    <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_set_info_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_set_info_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_set_info_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_set_info_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__info__evt__param"></a> struct hidh\_set\_info\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_SET\_INFO\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_set_info_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_set_info_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_set_info_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_set_info_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__info__evt__param_1a145c2bc5cfa063f811d0ad1b0eb8d72b"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_set_info_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_set_info_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_set_info_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_set_info_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__info__evt__param_1ae331c6cdd0a5654637ff49de95433799"></a> uint8\_t handle
        :   device handle

        <a id="_CPPv4N18bk_hidh_cb_param_t23hidh_set_info_evt_param7bd_addrE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t23hidh_set_info_evt_param7bd_addrE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t23hidh_set_info_evt_param7bd_addrE"></a> <a id="bk_hidh_cb_param_t::hidh_set_info_evt_param::bd_addr__bk_bd_addr_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__info__evt__param_1a0df191b69b475b7c0af18ae77999dab9"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr
        :   device address

    <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_set_proto_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_set_proto_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_set_proto_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_set_proto_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__proto__evt__param"></a> struct hidh\_set\_proto\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_SET\_PROTO\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_set_proto_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_set_proto_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_set_proto_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_set_proto_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__proto__evt__param_1a2e90ede7575ef5ac05fc2cdf078fd5c2"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t24hidh_set_proto_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t24hidh_set_proto_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t24hidh_set_proto_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_set_proto_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__proto__evt__param_1a1cc92410fddfbccc4280bfddd732d1bf"></a> uint8\_t handle
        :   device handle

    <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_set_rpt_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_set_rpt_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_set_rpt_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_set_rpt_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__rpt__evt__param"></a> struct hidh\_set\_rpt\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_SET\_RPT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_set_rpt_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_set_rpt_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_set_rpt_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_set_rpt_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__rpt__evt__param_1afcb9d9726e37da02d64f99f1ba82e2ab"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t22hidh_set_rpt_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t22hidh_set_rpt_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t22hidh_set_rpt_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_set_rpt_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__set__rpt__evt__param_1a6539d3b066ba1941c4ba610df001fa39"></a> uint8\_t handle
        :   device handle

    <a id="_CPPv4N18bk_hidh_cb_param_t21hidh_uninit_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t21hidh_uninit_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t21hidh_uninit_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_uninit_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__uninit__evt__param"></a> struct hidh\_uninit\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_DEINIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t21hidh_uninit_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t21hidh_uninit_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t21hidh_uninit_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_uninit_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__uninit__evt__param_1abd1a0b924030665d17509bdcd3b49643"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   status

    <a id="_CPPv4N18bk_hidh_cb_param_t21hidh_unplug_evt_paramE"></a>

    <a id="_CPPv3N18bk_hidh_cb_param_t21hidh_unplug_evt_paramE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t21hidh_unplug_evt_paramE"></a> <a id="bk_hidh_cb_param_t::hidh_unplug_evt_param"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__unplug__evt__param"></a> struct hidh\_unplug\_evt\_param
    :   *#include \<bk\_dm\_hidh.h\>*

        BK\_HIDH\_VC\_UNPLUG\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_hidh_cb_param_t21hidh_unplug_evt_param6statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t21hidh_unplug_evt_param6statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t21hidh_unplug_evt_param6statusE"></a> <a id="bk_hidh_cb_param_t::hidh_unplug_evt_param::status__bk_hidh_status_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__unplug__evt__param_1ab88f4bab02a5c4c339e94866c7de084d"></a> [bk\_hidh\_status\_t](#_CPPv416bk_hidh_status_t "bk_hidh_status_t") status
        :   operation status

        <a id="_CPPv4N18bk_hidh_cb_param_t21hidh_unplug_evt_param11conn_statusE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t21hidh_unplug_evt_param11conn_statusE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t21hidh_unplug_evt_param11conn_statusE"></a> <a id="bk_hidh_cb_param_t::hidh_unplug_evt_param::conn_status__bk_hidh_connection_state_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__unplug__evt__param_1a9e9c6815afe56cc69f1c542049e80d1a"></a> [bk\_hidh\_connection\_state\_t](#_CPPv426bk_hidh_connection_state_t "bk_hidh_connection_state_t") conn\_status
        :   connection status

        <a id="_CPPv4N18bk_hidh_cb_param_t21hidh_unplug_evt_param6handleE"></a>

        <a id="_CPPv3N18bk_hidh_cb_param_t21hidh_unplug_evt_param6handleE"></a> <a id="_CPPv2N18bk_hidh_cb_param_t21hidh_unplug_evt_param6handleE"></a> <a id="bk_hidh_cb_param_t::hidh_unplug_evt_param::handle__uint8_t"></a> <a id="structbk__hidh__cb__param__t_1_1hidh__unplug__evt__param_1ae86b096347937dcda86c44878308f454"></a> uint8\_t handle
        :   device handle

<a id="id15"></a>

### Structures

<a id="_CPPv418bk_hidh_hid_info_t"></a>

<a id="_CPPv318bk_hidh_hid_info_t"></a> <a id="_CPPv218bk_hidh_hid_info_t"></a> <a id="bk_hidh_hid_info_t"></a> <a id="structbk__hidh__hid__info__t"></a> struct bk\_hidh\_hid\_info\_t
:   HID device information from HID Device Service Record and Device ID Service Record.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_hidh_hid_info_t9attr_maskE"></a>

    <a id="_CPPv3N18bk_hidh_hid_info_t9attr_maskE"></a> <a id="_CPPv2N18bk_hidh_hid_info_t9attr_maskE"></a> <a id="bk_hidh_hid_info_t::attr_mask__i"></a> <a id="structbk__hidh__hid__info__t_1a812152fc7b168d7801a07486562d279c"></a> int attr\_mask
    :   device attribute bit mask, refer to bk\_hidh\_dev\_attr\_t

    <a id="_CPPv4N18bk_hidh_hid_info_t6dl_lenE"></a>

    <a id="_CPPv3N18bk_hidh_hid_info_t6dl_lenE"></a> <a id="_CPPv2N18bk_hidh_hid_info_t6dl_lenE"></a> <a id="bk_hidh_hid_info_t::dl_len__i"></a> <a id="structbk__hidh__hid__info__t_1a103aa8c95179e677c161d2c9e61b4bb7"></a> int dl\_len
    :   SDP attrbutes of HID devices: HID device descriptor length

    <a id="_CPPv4N18bk_hidh_hid_info_t8dsc_listE"></a>

    <a id="_CPPv3N18bk_hidh_hid_info_t8dsc_listE"></a> <a id="_CPPv2N18bk_hidh_hid_info_t8dsc_listE"></a> <a id="bk_hidh_hid_info_t::dsc_list__uint8_tP"></a> <a id="structbk__hidh__hid__info__t_1ac54a739fc85bd544e0c2439d02f6c645"></a> uint8\_t \*dsc\_list
    :   SDP attrbutes of HID devices: HID device descriptor definition

<a id="id16"></a>

### Macros

<a id="c.BTHH_MAX_DSC_LEN"></a>

<a id="bk__dm__hidh_8h_1ad48a67897414aadb07622c021eb527eb"></a> BTHH\_MAX\_DSC\_LEN
:   maximum size of HID Device report descriptor

<a id="id17"></a>

### Type Definitions

<a id="_CPPv410bk_hh_cb_t"></a>

<a id="_CPPv310bk_hh_cb_t"></a> <a id="_CPPv210bk_hh_cb_t"></a> <a id="bk_hh_cb_t"></a> <a id="bk__dm__hidh_8h_1a3ceb473375d0eac57a9363c9a9e7c360"></a> typedef void (\*bk\_hh\_cb\_t)([bk\_hidh\_cb\_event\_t](#_CPPv418bk_hidh_cb_event_t "bk_hidh_cb_event_t") event, [bk\_hidh\_cb\_param\_t](#_CPPv418bk_hidh_cb_param_t "bk_hidh_cb_param_t") \*param)
:   HID host callback function type.

    Param event
    :   Event type

    Param param
    :   Point to callback parameter, currently is union type

<a id="id18"></a>

### Enumerations

<a id="_CPPv426bk_hidh_connection_state_t"></a>

<a id="_CPPv326bk_hidh_connection_state_t"></a> <a id="_CPPv226bk_hidh_connection_state_t"></a> <a id="bk__dm__hidh_8h_1a1fb8bc5fbddd85357349620514f7a8bb"></a> enum bk\_hidh\_connection\_state\_t
:   HID host connection state.

    *Values:*

    <a id="_CPPv4N26bk_hidh_connection_state_t28BK_HIDH_CONN_STATE_CONNECTEDE"></a>

    <a id="_CPPv3N26bk_hidh_connection_state_t28BK_HIDH_CONN_STATE_CONNECTEDE"></a> <a id="_CPPv2N26bk_hidh_connection_state_t28BK_HIDH_CONN_STATE_CONNECTEDE"></a> <a id="bk__dm__hidh_8h_1a1fb8bc5fbddd85357349620514f7a8bba74c2c6a84f28fc8e511c5ebbe9031afe"></a> enumerator BK\_HIDH\_CONN\_STATE\_CONNECTED
    :   connected state

    <a id="_CPPv4N26bk_hidh_connection_state_t29BK_HIDH_CONN_STATE_CONNECTINGE"></a>

    <a id="_CPPv3N26bk_hidh_connection_state_t29BK_HIDH_CONN_STATE_CONNECTINGE"></a> <a id="_CPPv2N26bk_hidh_connection_state_t29BK_HIDH_CONN_STATE_CONNECTINGE"></a> <a id="bk__dm__hidh_8h_1a1fb8bc5fbddd85357349620514f7a8bba62f42a0c41f9b293011b4d3e25745a9f"></a> enumerator BK\_HIDH\_CONN\_STATE\_CONNECTING
    :   connecting state

    <a id="_CPPv4N26bk_hidh_connection_state_t31BK_HIDH_CONN_STATE_DISCONNECTEDE"></a>

    <a id="_CPPv3N26bk_hidh_connection_state_t31BK_HIDH_CONN_STATE_DISCONNECTEDE"></a> <a id="_CPPv2N26bk_hidh_connection_state_t31BK_HIDH_CONN_STATE_DISCONNECTEDE"></a> <a id="bk__dm__hidh_8h_1a1fb8bc5fbddd85357349620514f7a8bba362ae74e91db9e31b5a04b3b93d329a7"></a> enumerator BK\_HIDH\_CONN\_STATE\_DISCONNECTED
    :   disconnected state

    <a id="_CPPv4N26bk_hidh_connection_state_t32BK_HIDH_CONN_STATE_DISCONNECTINGE"></a>

    <a id="_CPPv3N26bk_hidh_connection_state_t32BK_HIDH_CONN_STATE_DISCONNECTINGE"></a> <a id="_CPPv2N26bk_hidh_connection_state_t32BK_HIDH_CONN_STATE_DISCONNECTINGE"></a> <a id="bk__dm__hidh_8h_1a1fb8bc5fbddd85357349620514f7a8bba233a0abdaba79c3b0efbc3c0cf1e785c"></a> enumerator BK\_HIDH\_CONN\_STATE\_DISCONNECTING
    :   disconnecting state

    <a id="_CPPv4N26bk_hidh_connection_state_t26BK_HIDH_CONN_STATE_UNKNOWNE"></a>

    <a id="_CPPv3N26bk_hidh_connection_state_t26BK_HIDH_CONN_STATE_UNKNOWNE"></a> <a id="_CPPv2N26bk_hidh_connection_state_t26BK_HIDH_CONN_STATE_UNKNOWNE"></a> <a id="bk__dm__hidh_8h_1a1fb8bc5fbddd85357349620514f7a8bba3f775f137e248a3bfe8fee55505bd16e"></a> enumerator BK\_HIDH\_CONN\_STATE\_UNKNOWN
    :   unknown state (initial state)

<a id="_CPPv416bk_hidh_status_t"></a>

<a id="_CPPv316bk_hidh_status_t"></a> <a id="_CPPv216bk_hidh_status_t"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4"></a> enum bk\_hidh\_status\_t
:   HID handshake error code and vendor-defined result code.

    *Values:*

    <a id="_CPPv4N16bk_hidh_status_t10BK_HIDH_OKE"></a>

    <a id="_CPPv3N16bk_hidh_status_t10BK_HIDH_OKE"></a> <a id="_CPPv2N16bk_hidh_status_t10BK_HIDH_OKE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a4d785177c740f231b52a427425329d47"></a> enumerator BK\_HIDH\_OK
    :   successful

    <a id="_CPPv4N16bk_hidh_status_t24BK_HIDH_HS_HID_NOT_READYE"></a>

    <a id="_CPPv3N16bk_hidh_status_t24BK_HIDH_HS_HID_NOT_READYE"></a> <a id="_CPPv2N16bk_hidh_status_t24BK_HIDH_HS_HID_NOT_READYE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a053a84f3ce222acaa244a94a8312bcb7"></a> enumerator BK\_HIDH\_HS\_HID\_NOT\_READY
    :   handshake error: device not ready

    <a id="_CPPv4N16bk_hidh_status_t25BK_HIDH_HS_INVALID_RPT_IDE"></a>

    <a id="_CPPv3N16bk_hidh_status_t25BK_HIDH_HS_INVALID_RPT_IDE"></a> <a id="_CPPv2N16bk_hidh_status_t25BK_HIDH_HS_INVALID_RPT_IDE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a4d63b3725d1595f45554d82054257779"></a> enumerator BK\_HIDH\_HS\_INVALID\_RPT\_ID
    :   handshake error: invalid report ID

    <a id="_CPPv4N16bk_hidh_status_t24BK_HIDH_HS_TRANS_NOT_SPTE"></a>

    <a id="_CPPv3N16bk_hidh_status_t24BK_HIDH_HS_TRANS_NOT_SPTE"></a> <a id="_CPPv2N16bk_hidh_status_t24BK_HIDH_HS_TRANS_NOT_SPTE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a5667a0fe045dd2c854d84ca9a0d96167"></a> enumerator BK\_HIDH\_HS\_TRANS\_NOT\_SPT
    :   handshake error: HID device does not support the request

    <a id="_CPPv4N16bk_hidh_status_t24BK_HIDH_HS_INVALID_PARAME"></a>

    <a id="_CPPv3N16bk_hidh_status_t24BK_HIDH_HS_INVALID_PARAME"></a> <a id="_CPPv2N16bk_hidh_status_t24BK_HIDH_HS_INVALID_PARAME"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4ad4013ea537d8adfc099f122f2c50dede"></a> enumerator BK\_HIDH\_HS\_INVALID\_PARAM
    :   handshake error: parameter value does not meet the expected criteria of called function or API

    <a id="_CPPv4N16bk_hidh_status_t16BK_HIDH_HS_ERRORE"></a>

    <a id="_CPPv3N16bk_hidh_status_t16BK_HIDH_HS_ERRORE"></a> <a id="_CPPv2N16bk_hidh_status_t16BK_HIDH_HS_ERRORE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a5f52149e34f751bd1acb51f03a5d1f89"></a> enumerator BK\_HIDH\_HS\_ERROR
    :   handshake error: HID device could not identify the error condition

    <a id="_CPPv4N16bk_hidh_status_t11BK_HIDH_ERRE"></a>

    <a id="_CPPv3N16bk_hidh_status_t11BK_HIDH_ERRE"></a> <a id="_CPPv2N16bk_hidh_status_t11BK_HIDH_ERRE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4ac391ae65f62af23b2b0817f758595462"></a> enumerator BK\_HIDH\_ERR
    :   general BK HID Host error

    <a id="_CPPv4N16bk_hidh_status_t15BK_HIDH_ERR_SDPE"></a>

    <a id="_CPPv3N16bk_hidh_status_t15BK_HIDH_ERR_SDPE"></a> <a id="_CPPv2N16bk_hidh_status_t15BK_HIDH_ERR_SDPE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a7fa993cbfcae7c3a026047e31e4b2b36"></a> enumerator BK\_HIDH\_ERR\_SDP
    :   SDP error

    <a id="_CPPv4N16bk_hidh_status_t17BK_HIDH_ERR_PROTOE"></a>

    <a id="_CPPv3N16bk_hidh_status_t17BK_HIDH_ERR_PROTOE"></a> <a id="_CPPv2N16bk_hidh_status_t17BK_HIDH_ERR_PROTOE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a1a355c46e68aecacceb16a45215d61c3"></a> enumerator BK\_HIDH\_ERR\_PROTO
    :   SET\_PROTOCOL error, only used in BK\_HIDH\_OPEN\_EVT callback

    <a id="_CPPv4N16bk_hidh_status_t19BK_HIDH_ERR_DB_FULLE"></a>

    <a id="_CPPv3N16bk_hidh_status_t19BK_HIDH_ERR_DB_FULLE"></a> <a id="_CPPv2N16bk_hidh_status_t19BK_HIDH_ERR_DB_FULLE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a8d1138e0547cccf8849d48234cf98e41"></a> enumerator BK\_HIDH\_ERR\_DB\_FULL
    :   device database full, used in BK\_HIDH\_OPEN\_EVT/BK\_HIDH\_ADD\_DEV\_EVT

    <a id="_CPPv4N16bk_hidh_status_t21BK_HIDH_ERR_TOD_UNSPTE"></a>

    <a id="_CPPv3N16bk_hidh_status_t21BK_HIDH_ERR_TOD_UNSPTE"></a> <a id="_CPPv2N16bk_hidh_status_t21BK_HIDH_ERR_TOD_UNSPTE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a0f5d68796c63012f200b65bbfdf1f900"></a> enumerator BK\_HIDH\_ERR\_TOD\_UNSPT
    :   type of device not supported

    <a id="_CPPv4N16bk_hidh_status_t18BK_HIDH_ERR_NO_RESE"></a>

    <a id="_CPPv3N16bk_hidh_status_t18BK_HIDH_ERR_NO_RESE"></a> <a id="_CPPv2N16bk_hidh_status_t18BK_HIDH_ERR_NO_RESE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a29febed3c9a36d0b98497d303a941a3d"></a> enumerator BK\_HIDH\_ERR\_NO\_RES
    :   out of system resources

    <a id="_CPPv4N16bk_hidh_status_t23BK_HIDH_ERR_AUTH_FAILEDE"></a>

    <a id="_CPPv3N16bk_hidh_status_t23BK_HIDH_ERR_AUTH_FAILEDE"></a> <a id="_CPPv2N16bk_hidh_status_t23BK_HIDH_ERR_AUTH_FAILEDE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4af22f168b270de0d2388f430130c0f8f6"></a> enumerator BK\_HIDH\_ERR\_AUTH\_FAILED
    :   authentication fail

    <a id="_CPPv4N16bk_hidh_status_t15BK_HIDH_ERR_HDLE"></a>

    <a id="_CPPv3N16bk_hidh_status_t15BK_HIDH_ERR_HDLE"></a> <a id="_CPPv2N16bk_hidh_status_t15BK_HIDH_ERR_HDLE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a098424c09eb6ae7f5898c7749009f5c7"></a> enumerator BK\_HIDH\_ERR\_HDL
    :   connection handle error

    <a id="_CPPv4N16bk_hidh_status_t15BK_HIDH_ERR_SECE"></a>

    <a id="_CPPv3N16bk_hidh_status_t15BK_HIDH_ERR_SECE"></a> <a id="_CPPv2N16bk_hidh_status_t15BK_HIDH_ERR_SECE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4aa114702e5ed3c96746e9fc528b8c57c9"></a> enumerator BK\_HIDH\_ERR\_SEC
    :   encryption error

    <a id="_CPPv4N16bk_hidh_status_t12BK_HIDH_BUSYE"></a>

    <a id="_CPPv3N16bk_hidh_status_t12BK_HIDH_BUSYE"></a> <a id="_CPPv2N16bk_hidh_status_t12BK_HIDH_BUSYE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a70b5cda97f5e1f4c2a01fe33373bdb50"></a> enumerator BK\_HIDH\_BUSY
    :   vendor-defined: temporarily can not handle this request

    <a id="_CPPv4N16bk_hidh_status_t15BK_HIDH_NO_DATAE"></a>

    <a id="_CPPv3N16bk_hidh_status_t15BK_HIDH_NO_DATAE"></a> <a id="_CPPv2N16bk_hidh_status_t15BK_HIDH_NO_DATAE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a9bb915b3f4700f064b9d3031023ea303"></a> enumerator BK\_HIDH\_NO\_DATA
    :   vendor-defined: no data.

    <a id="_CPPv4N16bk_hidh_status_t17BK_HIDH_NEED_INITE"></a>

    <a id="_CPPv3N16bk_hidh_status_t17BK_HIDH_NEED_INITE"></a> <a id="_CPPv2N16bk_hidh_status_t17BK_HIDH_NEED_INITE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4ab6354d788555d269d302b21d29b90497"></a> enumerator BK\_HIDH\_NEED\_INIT
    :   vendor-defined: HIDH module shall initialize first

    <a id="_CPPv4N16bk_hidh_status_t19BK_HIDH_NEED_DEINITE"></a>

    <a id="_CPPv3N16bk_hidh_status_t19BK_HIDH_NEED_DEINITE"></a> <a id="_CPPv2N16bk_hidh_status_t19BK_HIDH_NEED_DEINITE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4aa96843562429370e5e05b86c53365246"></a> enumerator BK\_HIDH\_NEED\_DEINIT
    :   vendor-defined: HIDH module shall de-deinitialize first

    <a id="_CPPv4N16bk_hidh_status_t21BK_HIDH_NO_CONNECTIONE"></a>

    <a id="_CPPv3N16bk_hidh_status_t21BK_HIDH_NO_CONNECTIONE"></a> <a id="_CPPv2N16bk_hidh_status_t21BK_HIDH_NO_CONNECTIONE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4a310790a6abcc476a4cf3c2333dbbad39"></a> enumerator BK\_HIDH\_NO\_CONNECTION
    :   vendor-defined: connection may have been closed

    <a id="_CPPv4N16bk_hidh_status_t19BK_HIDH_NO_ACL_LINKE"></a>

    <a id="_CPPv3N16bk_hidh_status_t19BK_HIDH_NO_ACL_LINKE"></a> <a id="_CPPv2N16bk_hidh_status_t19BK_HIDH_NO_ACL_LINKE"></a> <a id="bk__dm__hidh_8h_1a38208f9c4d0110f0aa993e0286be96b4ae3833cb0d1cbc049f281322cd39d20a9"></a> enumerator BK\_HIDH\_NO\_ACL\_LINK
    :   vendor-defined: Baseband acl link not exist

<a id="_CPPv423bk_hidh_protocol_mode_t"></a>

<a id="_CPPv323bk_hidh_protocol_mode_t"></a> <a id="_CPPv223bk_hidh_protocol_mode_t"></a> <a id="bk__dm__hidh_8h_1a541bb53a5ab86d094d4d12b9770c908b"></a> enum bk\_hidh\_protocol\_mode\_t
:   HID host protocol modes.

    *Values:*

    <a id="_CPPv4N23bk_hidh_protocol_mode_t17BK_HIDH_BOOT_MODEE"></a>

    <a id="_CPPv3N23bk_hidh_protocol_mode_t17BK_HIDH_BOOT_MODEE"></a> <a id="_CPPv2N23bk_hidh_protocol_mode_t17BK_HIDH_BOOT_MODEE"></a> <a id="bk__dm__hidh_8h_1a541bb53a5ab86d094d4d12b9770c908bac09acf00e7bba4ccab422d08a4d23454"></a> enumerator BK\_HIDH\_BOOT\_MODE
    :   boot protocol mode

    <a id="_CPPv4N23bk_hidh_protocol_mode_t19BK_HIDH_REPORT_MODEE"></a>

    <a id="_CPPv3N23bk_hidh_protocol_mode_t19BK_HIDH_REPORT_MODEE"></a> <a id="_CPPv2N23bk_hidh_protocol_mode_t19BK_HIDH_REPORT_MODEE"></a> <a id="bk__dm__hidh_8h_1a541bb53a5ab86d094d4d12b9770c908bab8f49d9caa10afd461849da4ab3d01e9"></a> enumerator BK\_HIDH\_REPORT\_MODE
    :   report protocol mode

    <a id="_CPPv4N23bk_hidh_protocol_mode_t24BK_HIDH_UNSUPPORTED_MODEE"></a>

    <a id="_CPPv3N23bk_hidh_protocol_mode_t24BK_HIDH_UNSUPPORTED_MODEE"></a> <a id="_CPPv2N23bk_hidh_protocol_mode_t24BK_HIDH_UNSUPPORTED_MODEE"></a> <a id="bk__dm__hidh_8h_1a541bb53a5ab86d094d4d12b9770c908ba98e7d171e91a21ea6d9f703886ab2a8f"></a> enumerator BK\_HIDH\_UNSUPPORTED\_MODE
    :   unsupported protocol mode

<a id="_CPPv421bk_hidh_report_type_t"></a>

<a id="_CPPv321bk_hidh_report_type_t"></a> <a id="_CPPv221bk_hidh_report_type_t"></a> <a id="bk__dm__hidh_8h_1a7a5b88a13853f2a7c23f549392816b59"></a> enum bk\_hidh\_report\_type\_t
:   HID host report types.

    *Values:*

    <a id="_CPPv4N21bk_hidh_report_type_t25BK_HIDH_REPORT_TYPE_OTHERE"></a>

    <a id="_CPPv3N21bk_hidh_report_type_t25BK_HIDH_REPORT_TYPE_OTHERE"></a> <a id="_CPPv2N21bk_hidh_report_type_t25BK_HIDH_REPORT_TYPE_OTHERE"></a> <a id="bk__dm__hidh_8h_1a7a5b88a13853f2a7c23f549392816b59a88628f36d2f44e8d0b1d220c4ce4ee06"></a> enumerator BK\_HIDH\_REPORT\_TYPE\_OTHER
    :   unsupported report type

    <a id="_CPPv4N21bk_hidh_report_type_t25BK_HIDH_REPORT_TYPE_INPUTE"></a>

    <a id="_CPPv3N21bk_hidh_report_type_t25BK_HIDH_REPORT_TYPE_INPUTE"></a> <a id="_CPPv2N21bk_hidh_report_type_t25BK_HIDH_REPORT_TYPE_INPUTE"></a> <a id="bk__dm__hidh_8h_1a7a5b88a13853f2a7c23f549392816b59a612ccb5e2c24a6dd27a9442f3bdc4ada"></a> enumerator BK\_HIDH\_REPORT\_TYPE\_INPUT
    :   input report type

    <a id="_CPPv4N21bk_hidh_report_type_t26BK_HIDH_REPORT_TYPE_OUTPUTE"></a>

    <a id="_CPPv3N21bk_hidh_report_type_t26BK_HIDH_REPORT_TYPE_OUTPUTE"></a> <a id="_CPPv2N21bk_hidh_report_type_t26BK_HIDH_REPORT_TYPE_OUTPUTE"></a> <a id="bk__dm__hidh_8h_1a7a5b88a13853f2a7c23f549392816b59a2fbb0bf000f3924803ef371ac54ecb77"></a> enumerator BK\_HIDH\_REPORT\_TYPE\_OUTPUT
    :   output report type

    <a id="_CPPv4N21bk_hidh_report_type_t27BK_HIDH_REPORT_TYPE_FEATUREE"></a>

    <a id="_CPPv3N21bk_hidh_report_type_t27BK_HIDH_REPORT_TYPE_FEATUREE"></a> <a id="_CPPv2N21bk_hidh_report_type_t27BK_HIDH_REPORT_TYPE_FEATUREE"></a> <a id="bk__dm__hidh_8h_1a7a5b88a13853f2a7c23f549392816b59ac08e51aec41788ee0fa46233f3e851ab"></a> enumerator BK\_HIDH\_REPORT\_TYPE\_FEATURE
    :   feature report type

<a id="_CPPv418bk_hidh_cb_event_t"></a>

<a id="_CPPv318bk_hidh_cb_event_t"></a> <a id="_CPPv218bk_hidh_cb_event_t"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6"></a> enum bk\_hidh\_cb\_event\_t
:   HID host callback function events.

    *Values:*

    <a id="_CPPv4N18bk_hidh_cb_event_t16BK_HIDH_INIT_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t16BK_HIDH_INIT_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t16BK_HIDH_INIT_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6aa96a27407dcf2dad4f63197a3e4d1015"></a> enumerator BK\_HIDH\_INIT\_EVT
    :   when HID host is initialized, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t18BK_HIDH_DEINIT_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t18BK_HIDH_DEINIT_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t18BK_HIDH_DEINIT_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6a775b806e7c0d85e5ab79d0dfa7a8d34b"></a> enumerator BK\_HIDH\_DEINIT\_EVT
    :   when HID host is deinitialized, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t16BK_HIDH_OPEN_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t16BK_HIDH_OPEN_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t16BK_HIDH_OPEN_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6a70a90232a1395f4e6c36f4840ad514da"></a> enumerator BK\_HIDH\_OPEN\_EVT
    :   when HID host connection opened, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t17BK_HIDH_CLOSE_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t17BK_HIDH_CLOSE_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t17BK_HIDH_CLOSE_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6a4c541d9b269af8c25e1bdd9003532f35"></a> enumerator BK\_HIDH\_CLOSE\_EVT
    :   when HID host connection closed, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t19BK_HIDH_GET_RPT_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t19BK_HIDH_GET_RPT_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t19BK_HIDH_GET_RPT_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6ad1ed6bd476483b747886720544c73ea5"></a> enumerator BK\_HIDH\_GET\_RPT\_EVT
    :   when Get\_Report command is called, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t19BK_HIDH_SET_RPT_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t19BK_HIDH_SET_RPT_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t19BK_HIDH_SET_RPT_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6a97db2a1fd45a4e7f611333f396443b18"></a> enumerator BK\_HIDH\_SET\_RPT\_EVT
    :   when Set\_Report command is called, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t21BK_HIDH_GET_PROTO_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t21BK_HIDH_GET_PROTO_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t21BK_HIDH_GET_PROTO_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6ac86839c799d6a1e5d12f5365badbf076"></a> enumerator BK\_HIDH\_GET\_PROTO\_EVT
    :   when Get\_Protocol command is called, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t21BK_HIDH_SET_PROTO_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t21BK_HIDH_SET_PROTO_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t21BK_HIDH_SET_PROTO_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6aa6cf5ff905a8cc133ffbd297847f423e"></a> enumerator BK\_HIDH\_SET\_PROTO\_EVT
    :   when Set\_Protocol command is called, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t20BK_HIDH_SDP_DSCP_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t20BK_HIDH_SDP_DSCP_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t20BK_HIDH_SDP_DSCP_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6ade82d8c17675b0f29971b75b45ca86f5"></a> enumerator BK\_HIDH\_SDP\_DSCP\_EVT
    :   when HIDH is connected, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t19BK_HIDH_ADD_DEV_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t19BK_HIDH_ADD_DEV_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t19BK_HIDH_ADD_DEV_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6a1c2c004316b386bb48e3b37790efdb37"></a> enumerator BK\_HIDH\_ADD\_DEV\_EVT
    :   when a device is added, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t19BK_HIDH_RMV_DEV_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t19BK_HIDH_RMV_DEV_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t19BK_HIDH_RMV_DEV_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6af96f9e6634595f3313634bae4eb072f4"></a> enumerator BK\_HIDH\_RMV\_DEV\_EVT
    :   when a device is removed, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t21BK_HIDH_VC_UNPLUG_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t21BK_HIDH_VC_UNPLUG_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t21BK_HIDH_VC_UNPLUG_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6af95e8d9f1e73b3bdd344daa3cd59247d"></a> enumerator BK\_HIDH\_VC\_UNPLUG\_EVT
    :   when virtually unplugged, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t16BK_HIDH_DATA_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t16BK_HIDH_DATA_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t16BK_HIDH_DATA_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6a8a7ac924e92eb670706ed1b0412a8d81"></a> enumerator BK\_HIDH\_DATA\_EVT
    :   when send data on interrupt channel, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t20BK_HIDH_DATA_IND_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t20BK_HIDH_DATA_IND_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t20BK_HIDH_DATA_IND_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6af3975b9cb1ca5dcf0cdda934edc4ea83"></a> enumerator BK\_HIDH\_DATA\_IND\_EVT
    :   when receive data on interrupt channel, the event comes

    <a id="_CPPv4N18bk_hidh_cb_event_t20BK_HIDH_SET_INFO_EVTE"></a>

    <a id="_CPPv3N18bk_hidh_cb_event_t20BK_HIDH_SET_INFO_EVTE"></a> <a id="_CPPv2N18bk_hidh_cb_event_t20BK_HIDH_SET_INFO_EVTE"></a> <a id="bk__dm__hidh_8h_1a1fd627757a7ae5d01beae38d3a6d80d6ad367cdad10b89bffa39ab4c9fef9657f"></a> enumerator BK\_HIDH\_SET\_INFO\_EVT
    :   when set the HID device descriptor, the event comes

<a id="_CPPv418bk_hidh_dev_attr_t"></a>

<a id="_CPPv318bk_hidh_dev_attr_t"></a> <a id="_CPPv218bk_hidh_dev_attr_t"></a> <a id="bk__dm__hidh_8h_1ac81f4ca68d08ca2f27ac92e0cde0f69c"></a> enum bk\_hidh\_dev\_attr\_t
:   HID device information from HID Device Service Record and Device ID Service Record.

    *Values:*

    <a id="_CPPv4N18bk_hidh_dev_attr_t30BK_HIDH_DEV_ATTR_VIRTUAL_CABLEE"></a>

    <a id="_CPPv3N18bk_hidh_dev_attr_t30BK_HIDH_DEV_ATTR_VIRTUAL_CABLEE"></a> <a id="_CPPv2N18bk_hidh_dev_attr_t30BK_HIDH_DEV_ATTR_VIRTUAL_CABLEE"></a> <a id="bk__dm__hidh_8h_1ac81f4ca68d08ca2f27ac92e0cde0f69ca54f98e8065f409e623b5dce033776150"></a> enumerator BK\_HIDH\_DEV\_ATTR\_VIRTUAL\_CABLE
    :   whether Virtual Cables is supported

    <a id="_CPPv4N18bk_hidh_dev_attr_t35BK_HIDH_DEV_ATTR_RECONNECT_INITIATEE"></a>

    <a id="_CPPv3N18bk_hidh_dev_attr_t35BK_HIDH_DEV_ATTR_RECONNECT_INITIATEE"></a> <a id="_CPPv2N18bk_hidh_dev_attr_t35BK_HIDH_DEV_ATTR_RECONNECT_INITIATEE"></a> <a id="bk__dm__hidh_8h_1ac81f4ca68d08ca2f27ac92e0cde0f69cac88845701fb70258e18d9dea0863e8c6"></a> enumerator BK\_HIDH\_DEV\_ATTR\_RECONNECT\_INITIATE
    :   whether the HID device inititates the reconnection process

    <a id="_CPPv4N18bk_hidh_dev_attr_t31BK_HIDH_DEV_ATTR_BATTERY_DEVICEE"></a>

    <a id="_CPPv3N18bk_hidh_dev_attr_t31BK_HIDH_DEV_ATTR_BATTERY_DEVICEE"></a> <a id="_CPPv2N18bk_hidh_dev_attr_t31BK_HIDH_DEV_ATTR_BATTERY_DEVICEE"></a> <a id="bk__dm__hidh_8h_1ac81f4ca68d08ca2f27ac92e0cde0f69ca24bdabcb7f306178be93a48e2152b393"></a> enumerator BK\_HIDH\_DEV\_ATTR\_BATTERY\_DEVICE
    :   whether Battery-powered device

    <a id="_CPPv4N18bk_hidh_dev_attr_t28BK_HIDH_DEV_ATTR_REMOTE_WAKEE"></a>

    <a id="_CPPv3N18bk_hidh_dev_attr_t28BK_HIDH_DEV_ATTR_REMOTE_WAKEE"></a> <a id="_CPPv2N18bk_hidh_dev_attr_t28BK_HIDH_DEV_ATTR_REMOTE_WAKEE"></a> <a id="bk__dm__hidh_8h_1ac81f4ca68d08ca2f27ac92e0cde0f69ca93c0534160f3d48fa3c9c7bf7e6fb517"></a> enumerator BK\_HIDH\_DEV\_ATTR\_REMOTE\_WAKE
    :   whether wake-up signal to host supported

    <a id="_CPPv4N18bk_hidh_dev_attr_t37BK_HIDH_DEV_ATTR_NORMALLY_CONNECTABLEE"></a>

    <a id="_CPPv3N18bk_hidh_dev_attr_t37BK_HIDH_DEV_ATTR_NORMALLY_CONNECTABLEE"></a> <a id="_CPPv2N18bk_hidh_dev_attr_t37BK_HIDH_DEV_ATTR_NORMALLY_CONNECTABLEE"></a> <a id="bk__dm__hidh_8h_1ac81f4ca68d08ca2f27ac92e0cde0f69ca57fa62abcfd5e5f91e852a15877e70fd"></a> enumerator BK\_HIDH\_DEV\_ATTR\_NORMALLY\_CONNECTABLE
    :   whether device is in Page Scan mode when there is no active connection

    <a id="_CPPv4N18bk_hidh_dev_attr_t28BK_HIDH_DEV_ATTR_BOOT_DEVICEE"></a>

    <a id="_CPPv3N18bk_hidh_dev_attr_t28BK_HIDH_DEV_ATTR_BOOT_DEVICEE"></a> <a id="_CPPv2N18bk_hidh_dev_attr_t28BK_HIDH_DEV_ATTR_BOOT_DEVICEE"></a> <a id="bk__dm__hidh_8h_1ac81f4ca68d08ca2f27ac92e0cde0f69caff4a5ea40846a21abae6a5b6e9ce6a8e"></a> enumerator BK\_HIDH\_DEV\_ATTR\_BOOT\_DEVICE
    :   whether Boot Protocol mode supported

<a id="_CPPv420bk_hidh_dev_app_id_t"></a>

<a id="_CPPv320bk_hidh_dev_app_id_t"></a> <a id="_CPPv220bk_hidh_dev_app_id_t"></a> <a id="bk__dm__hidh_8h_1a1420b56eb4aa01320166bb121020145b"></a> enum bk\_hidh\_dev\_app\_id\_t
:   application ID(non-zero) for each type of device

    *Values:*

    <a id="_CPPv4N20bk_hidh_dev_app_id_t20BK_HIDH_APP_ID_MOUSEE"></a>

    <a id="_CPPv3N20bk_hidh_dev_app_id_t20BK_HIDH_APP_ID_MOUSEE"></a> <a id="_CPPv2N20bk_hidh_dev_app_id_t20BK_HIDH_APP_ID_MOUSEE"></a> <a id="bk__dm__hidh_8h_1a1420b56eb4aa01320166bb121020145ba8fafc1464cc704469de411dccd5199c7"></a> enumerator BK\_HIDH\_APP\_ID\_MOUSE
    :   pointing device

    <a id="_CPPv4N20bk_hidh_dev_app_id_t23BK_HIDH_APP_ID_KEYBOARDE"></a>

    <a id="_CPPv3N20bk_hidh_dev_app_id_t23BK_HIDH_APP_ID_KEYBOARDE"></a> <a id="_CPPv2N20bk_hidh_dev_app_id_t23BK_HIDH_APP_ID_KEYBOARDE"></a> <a id="bk__dm__hidh_8h_1a1420b56eb4aa01320166bb121020145ba96d85033133ff61411d2ac6a168a8117"></a> enumerator BK\_HIDH\_APP\_ID\_KEYBOARD
    :   keyboard

    <a id="_CPPv4N20bk_hidh_dev_app_id_t29BK_HIDH_APP_ID_REMOTE_CONTROLE"></a>

    <a id="_CPPv3N20bk_hidh_dev_app_id_t29BK_HIDH_APP_ID_REMOTE_CONTROLE"></a> <a id="_CPPv2N20bk_hidh_dev_app_id_t29BK_HIDH_APP_ID_REMOTE_CONTROLE"></a> <a id="bk__dm__hidh_8h_1a1420b56eb4aa01320166bb121020145ba3312d80fd40088ea54b74b85dd0b9763"></a> enumerator BK\_HIDH\_APP\_ID\_REMOTE\_CONTROL
    :   remote control

    <a id="_CPPv4N20bk_hidh_dev_app_id_t23BK_HIDH_APP_ID_JOYSTICKE"></a>

    <a id="_CPPv3N20bk_hidh_dev_app_id_t23BK_HIDH_APP_ID_JOYSTICKE"></a> <a id="_CPPv2N20bk_hidh_dev_app_id_t23BK_HIDH_APP_ID_JOYSTICKE"></a> <a id="bk__dm__hidh_8h_1a1420b56eb4aa01320166bb121020145ba989476811aafcef70b61f5f899914645"></a> enumerator BK\_HIDH\_APP\_ID\_JOYSTICK
    :   joystick

    <a id="_CPPv4N20bk_hidh_dev_app_id_t22BK_HIDH_APP_ID_GAMEPADE"></a>

    <a id="_CPPv3N20bk_hidh_dev_app_id_t22BK_HIDH_APP_ID_GAMEPADE"></a> <a id="_CPPv2N20bk_hidh_dev_app_id_t22BK_HIDH_APP_ID_GAMEPADE"></a> <a id="bk__dm__hidh_8h_1a1420b56eb4aa01320166bb121020145bab6002efbcfe560da68a8ca7e31f5b73e"></a> enumerator BK\_HIDH\_APP\_ID\_GAMEPAD
    :   gamepad

<a id="bk-dm-l2cap-h"></a>

## bk\_dm\_l2cap.h

`bk_dm_l2cap.h` 提供 BT L2CAP 通道和数据传输接口。

<a id="id19"></a>

### Header File

- [bk\_dm\_l2cap.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_l2cap.h)

<a id="id20"></a>

### Functions

<a id="_CPPv429bk_bt_l2cap_register_callback16bk_bt_l2cap_cb_t"></a>

<a id="_CPPv329bk_bt_l2cap_register_callback16bk_bt_l2cap_cb_t"></a> <a id="_CPPv229bk_bt_l2cap_register_callback16bk_bt_l2cap_cb_t"></a> <a id="bk_bt_l2cap_register_callback__bk_bt_l2cap_cb_t"></a> <a id="bk__dm__l2cap_8h_1a97fdfd14c4bcc52ac85eee1ece277492"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_l2cap\_register\_callback([bk\_bt\_l2cap\_cb\_t](#_CPPv416bk_bt_l2cap_cb_t "bk_bt_l2cap_cb_t") callback)
:   This function is called to init callbacks with L2CAP module.

    参数
    :   **callback** – **\[in\]** pointer to the init callback function.

    返回
    :   - BT\_OK: success
        - other: failed

<a id="_CPPv416bk_bt_l2cap_initv"></a>

<a id="_CPPv316bk_bt_l2cap_initv"></a> <a id="_CPPv216bk_bt_l2cap_initv"></a> <a id="bk_bt_l2cap_init__void"></a> <a id="bk__dm__l2cap_8h_1a7c6b74caa17939bdb5140e99545c29af"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_l2cap\_init(void)
:   This function is called to init L2CAP module. When the operation is completed, the callback function will be called with BK\_BT\_L2CAP\_INIT\_EVT. This function should be called after bk\_bluedroid\_enable() completes successfully.

    返回
    :   - BT\_OK: success
        - other: failed

<a id="_CPPv418bk_bt_l2cap_deinitv"></a>

<a id="_CPPv318bk_bt_l2cap_deinitv"></a> <a id="_CPPv218bk_bt_l2cap_deinitv"></a> <a id="bk_bt_l2cap_deinit__void"></a> <a id="bk__dm__l2cap_8h_1a35cf565da34a384b1923bd301233b713"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_l2cap\_deinit(void)
:   This function is called to uninit l2cap module. The operation will close all active L2CAP connection first, then the callback function will be called with BK\_BT\_L2CAP\_CLOSE\_EVT, and the number of BK\_BT\_L2CAP\_CLOSE\_EVT is equal to the number of connection. When the operation is completed, the callback function will be called with BK\_BT\_L2CAP\_UNINIT\_EVT. This function should be called after bk\_bt\_l2cap\_init() completes successfully.

    返回
    :   - BT\_OK: success
        - other: failed

<a id="_CPPv419bk_bt_l2cap_connect24bk_bt_l2cap_cntl_flags_t8uint16_t12bk_bd_addr_t"></a>

<a id="_CPPv319bk_bt_l2cap_connect24bk_bt_l2cap_cntl_flags_t8uint16_t12bk_bd_addr_t"></a> <a id="_CPPv219bk_bt_l2cap_connect24bk_bt_l2cap_cntl_flags_t8uint16_t12bk_bd_addr_t"></a> <a id="bk_bt_l2cap_connect__bk_bt_l2cap_cntl_flags_t.uint16_t.bk_bd_addr_t"></a> <a id="bk__dm__l2cap_8h_1ae16a36cd7e73b0b7f6fff7561249e189"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_l2cap\_connect([bk\_bt\_l2cap\_cntl\_flags\_t](#_CPPv424bk_bt_l2cap_cntl_flags_t "bk_bt_l2cap_cntl_flags_t") cntl\_flag, uint16\_t remote\_psm, [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") peer\_bd\_addr)
:   This function makes an L2CAP connection to a remote BD Address. When the connection is initiated or failed to initiate, the callback is called with BK\_BT\_L2CAP\_CL\_INIT\_EVT. When the connection is established or failed, the callback is called with BK\_BT\_L2CAP\_OPEN\_EVT. This function must be called after bk\_bt\_l2cap\_init() successful and before bk\_bt\_l2cap\_deinit().

    参数
    :   - **cntl\_flag** – **\[in\]** Lower 16-bit security settings mask.
        - **remote\_psm** – **\[in\]** Remote device bluetooth Profile PSM.
        - **peer\_bd\_addr** – **\[in\]** Remote device bluetooth device address.

    返回
    :   - BT\_OK: success
        - other: failed

<a id="_CPPv421bk_bt_l2cap_start_srv24bk_bt_l2cap_cntl_flags_t8uint16_t"></a>

<a id="_CPPv321bk_bt_l2cap_start_srv24bk_bt_l2cap_cntl_flags_t8uint16_t"></a> <a id="_CPPv221bk_bt_l2cap_start_srv24bk_bt_l2cap_cntl_flags_t8uint16_t"></a> <a id="bk_bt_l2cap_start_srv__bk_bt_l2cap_cntl_flags_t.uint16_t"></a> <a id="bk__dm__l2cap_8h_1af764429330d263ff052d5c7b005f5a6b"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_l2cap\_start\_srv([bk\_bt\_l2cap\_cntl\_flags\_t](#_CPPv424bk_bt_l2cap_cntl_flags_t "bk_bt_l2cap_cntl_flags_t") cntl\_flag, uint16\_t local\_psm)
:   This function create a L2CAP server and starts listening for an L2CAP connection request from a remote Bluetooth device. When the server is started successfully, the callback is called with BK\_BT\_L2CAP\_START\_EVT. When the connection is established, the callback is called with BK\_BT\_L2CAP\_OPEN\_EVT. This function must be called after bk\_bt\_l2cap\_init() successful and before bk\_bt\_l2cap\_deinit().

    参数
    :   - **cntl\_flag** – **\[in\]** Lower 16-bit security settings mask.
        - **local\_psm** – **\[in\]** Dynamic PSM.

    返回
    :   - BT\_OK: success
        - other: failed

<a id="_CPPv424bk_bt_l2cap_stop_all_srvv"></a>

<a id="_CPPv324bk_bt_l2cap_stop_all_srvv"></a> <a id="_CPPv224bk_bt_l2cap_stop_all_srvv"></a> <a id="bk_bt_l2cap_stop_all_srv__void"></a> <a id="bk__dm__l2cap_8h_1a575448d5ddfe3a3729ef3807990cab82"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_l2cap\_stop\_all\_srv(void)
:   This function stops all L2CAP servers. The operation will close all active L2CAP connection first, then the callback function will be called with BK\_BT\_L2CAP\_CLOSE\_EVT, and the number of BK\_BT\_L2CAP\_CLOSE\_EVT is equal to the number of connection. When the operation is completed, the callback is called with BK\_BT\_L2CAP\_SRV\_STOP\_EVT. This function must be called after bk\_bt\_l2cap\_init() successful and before bk\_bt\_l2cap\_deinit().

    返回
    :   - BT\_OK: success
        - other: failed

<a id="_CPPv420bk_bt_l2cap_stop_srv8uint16_t"></a>

<a id="_CPPv320bk_bt_l2cap_stop_srv8uint16_t"></a> <a id="_CPPv220bk_bt_l2cap_stop_srv8uint16_t"></a> <a id="bk_bt_l2cap_stop_srv__uint16_t"></a> <a id="bk__dm__l2cap_8h_1a8452f77e2e68814738af95daf9620e2b"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_bt\_l2cap\_stop\_srv(uint16\_t local\_psm)
:   This function stops a specific L2CAP server. The operation will close all active L2CAP connection first on the specific L2CAP server, then the callback function will be called with BK\_BT\_L2CAP\_CLOSE\_EVT, and the number of BK\_BT\_L2CAP\_CLOSE\_EVT is equal to the number of connection. When the operation is completed, the callback is called with BK\_BT\_L2CAP\_SRV\_STOP\_EVT. This function must be called after bk\_bt\_l2cap\_init() successful and before bk\_bt\_l2cap\_deinit().

    参数
    :   **local\_psm** – **\[in\]** Dynamic PSM.

    返回
    :   - BT\_OK: success
        - other: failed

<a id="_CPPv416bk_bt_l2cap_readiPv8uint16_t"></a>

<a id="_CPPv316bk_bt_l2cap_readiPv8uint16_t"></a> <a id="_CPPv216bk_bt_l2cap_readiPv8uint16_t"></a> <a id="bk_bt_l2cap_read__i.voidP.uint16_t"></a> <a id="bk__dm__l2cap_8h_1a81ac5c16f091f0faa4a614495579d529"></a> int bk\_bt\_l2cap\_read(int fd, void \*data, uint16\_t size)

<a id="_CPPv417bk_bt_l2cap_writeiPKv8uint16_t"></a>

<a id="_CPPv317bk_bt_l2cap_writeiPKv8uint16_t"></a> <a id="_CPPv217bk_bt_l2cap_writeiPKv8uint16_t"></a> <a id="bk_bt_l2cap_write__i.voidCP.uint16_t"></a> <a id="bk__dm__l2cap_8h_1ae1e7e6b592c94ae4c78e81bee425ef28"></a> int bk\_bt\_l2cap\_write(int fd, const void \*data, uint16\_t size)

<a id="_CPPv417bk_bt_l2cap_closei"></a>

<a id="_CPPv317bk_bt_l2cap_closei"></a> <a id="_CPPv217bk_bt_l2cap_closei"></a> <a id="bk_bt_l2cap_close__i"></a> <a id="bk__dm__l2cap_8h_1a6131e9b0523edfec94c7ab7430f34165"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_l2cap\_close(int fd)

<a id="_CPPv429bk_bt_l2cap_set_data_callback21bk_bt_l2cap_data_cb_t"></a>

<a id="_CPPv329bk_bt_l2cap_set_data_callback21bk_bt_l2cap_data_cb_t"></a> <a id="_CPPv229bk_bt_l2cap_set_data_callback21bk_bt_l2cap_data_cb_t"></a> <a id="bk_bt_l2cap_set_data_callback__bk_bt_l2cap_data_cb_t"></a> <a id="bk__dm__l2cap_8h_1ab06238ec5b5214607aa55eb0ce58bebf"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_bt\_l2cap\_set\_data\_callback([bk\_bt\_l2cap\_data\_cb\_t](#_CPPv421bk_bt_l2cap_data_cb_t "bk_bt_l2cap_data_cb_t") callback)

<a id="id21"></a>

### Unions

<a id="_CPPv422bk_bt_l2cap_cb_param_t"></a>

<a id="_CPPv322bk_bt_l2cap_cb_param_t"></a> <a id="_CPPv222bk_bt_l2cap_cb_param_t"></a> <a id="unionbk__bt__l2cap__cb__param__t"></a> union bk\_bt\_l2cap\_cb\_param\_t
:   *#include \<bk\_dm\_l2cap.h\>*

    L2CAP callback parameters union.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t4initE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t4initE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t4initE"></a> <a id="bk_bt_l2cap_cb_param_t::init__bk_bt_l2cap_cb_param_t::l2cap_init_evt_param"></a> <a id="unionbk__bt__l2cap__cb__param__t_1a19403bea35d80011177ec116bb55a2af"></a> struct [bk\_bt\_l2cap\_cb\_param\_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap\_init\_evt\_param](#_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_init_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_init_evt_param") init
    :   L2CAP callback param of BK\_BT\_L2CAP\_INIT\_EVT

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t6uninitE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t6uninitE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t6uninitE"></a> <a id="bk_bt_l2cap_cb_param_t::uninit__bk_bt_l2cap_cb_param_t::l2cap_uninit_evt_param"></a> <a id="unionbk__bt__l2cap__cb__param__t_1a24ac9beadb758ae02bc03e3fc692f89a"></a> struct [bk\_bt\_l2cap\_cb\_param\_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap\_uninit\_evt\_param](#_CPPv4N22bk_bt_l2cap_cb_param_t22l2cap_uninit_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_uninit_evt_param") uninit
    :   L2CAP callback param of BK\_BT\_L2CAP\_UNINIT\_EVT

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t4openE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t4openE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t4openE"></a> <a id="bk_bt_l2cap_cb_param_t::open__bk_bt_l2cap_cb_param_t::l2cap_open_evt_param"></a> <a id="unionbk__bt__l2cap__cb__param__t_1ad3af62ffe9696fd1530064e29216c8ba"></a> struct [bk\_bt\_l2cap\_cb\_param\_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap\_open\_evt\_param](#_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_open_evt_param") open
    :   L2CAP callback param of BK\_BT\_L2CAP\_OPEN\_EVT

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t5closeE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t5closeE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t5closeE"></a> <a id="bk_bt_l2cap_cb_param_t::close__bk_bt_l2cap_cb_param_t::l2cap_close_evt_param"></a> <a id="unionbk__bt__l2cap__cb__param__t_1a68c8941c1ca1fbd37d6f29a65ab18a20"></a> struct [bk\_bt\_l2cap\_cb\_param\_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap\_close\_evt\_param](#_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_close_evt_param") close
    :   L2CAP callback param of BK\_BT\_L2CAP\_CLOSE\_EVT

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t5startE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t5startE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t5startE"></a> <a id="bk_bt_l2cap_cb_param_t::start__bk_bt_l2cap_cb_param_t::l2cap_start_evt_param"></a> <a id="unionbk__bt__l2cap__cb__param__t_1a4e5ff7e291f90ad63ef1608eb87dc55f"></a> struct [bk\_bt\_l2cap\_cb\_param\_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap\_start\_evt\_param](#_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_start_evt_param") start
    :   L2CAP callback param of BK\_BT\_L2CAP\_START\_EVT

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t7cl_initE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t7cl_initE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t7cl_initE"></a> <a id="bk_bt_l2cap_cb_param_t::cl_init__bk_bt_l2cap_cb_param_t::l2cap_cl_init_evt_param"></a> <a id="unionbk__bt__l2cap__cb__param__t_1afaf407caaae9f0d15bd262aaad58b4bc"></a> struct [bk\_bt\_l2cap\_cb\_param\_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap\_cl\_init\_evt\_param](#_CPPv4N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_cl_init_evt_param") cl\_init
    :   L2CAP callback param of BK\_BT\_L2CAP\_CL\_INIT\_EVT

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t8srv_stopE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t8srv_stopE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t8srv_stopE"></a> <a id="bk_bt_l2cap_cb_param_t::srv_stop__bk_bt_l2cap_cb_param_t::l2cap_srv_stop_evt_param"></a> <a id="unionbk__bt__l2cap__cb__param__t_1a1f594f6f0555bf5e5670dd9dcac182eb"></a> struct [bk\_bt\_l2cap\_cb\_param\_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t")::[l2cap\_srv\_stop\_evt\_param](#_CPPv4N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_paramE "bk_bt_l2cap_cb_param_t::l2cap_srv_stop_evt_param") srv\_stop
    :   L2CAP callback param of BK\_BT\_L2CAP\_SRV\_STOP\_EVT

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_paramE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_paramE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_paramE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_cl_init_evt_param"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__cl__init__evt__param"></a> struct l2cap\_cl\_init\_evt\_param
    :   *#include \<bk\_dm\_l2cap.h\>*

        BK\_BT\_L2CAP\_CL\_INIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_param6statusE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_param6statusE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_param6statusE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_cl_init_evt_param::status__bk_bt_l2cap_status_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__cl__init__evt__param_1ac9027f2525460329b87544327fc041c9"></a> [bk\_bt\_l2cap\_status\_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_param6handleE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_param6handleE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_param6handleE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_cl_init_evt_param::handle__uint32_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__cl__init__evt__param_1ad4fb388841cb659e51bef54143de332f"></a> uint32\_t handle
        :   The connection handle

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_param6sec_idE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_param6sec_idE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t23l2cap_cl_init_evt_param6sec_idE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_cl_init_evt_param::sec_id__uint8_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__cl__init__evt__param_1a649449ba764f187c9a1a7d0d73bb1c27"></a> uint8\_t sec\_id
        :   security ID used by this server

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_paramE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_paramE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_paramE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_close_evt_param"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__close__evt__param"></a> struct l2cap\_close\_evt\_param
    :   *#include \<bk\_dm\_l2cap.h\>*

        BK\_BT\_L2CAP\_CLOSE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param6statusE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param6statusE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param6statusE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_close_evt_param::status__bk_bt_l2cap_status_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__close__evt__param_1a1bc5c657ea5051f2b4b34cb4d5be7802"></a> [bk\_bt\_l2cap\_status\_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param6handleE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param6handleE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param6handleE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_close_evt_param::handle__uint32_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__close__evt__param_1a963d433297bb8b024f8326aa11c992e0"></a> uint32\_t handle
        :   The connection handle

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param5asyncE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param5asyncE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param5asyncE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_close_evt_param::async__b"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__close__evt__param_1ae30ead9daef3a592d9b8bc1d6248d696"></a> bool async
        :   FALSE, if local initiates disconnect

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param2fdE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param2fdE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t21l2cap_close_evt_param2fdE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_close_evt_param::fd__i"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__close__evt__param_1ae0018a36199bc86bcf26774c603e8dcf"></a> int fd
        :   File descriptor, lcid

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_init_evt_paramE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t20l2cap_init_evt_paramE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t20l2cap_init_evt_paramE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_init_evt_param"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__init__evt__param"></a> struct l2cap\_init\_evt\_param
    :   *#include \<bk\_dm\_l2cap.h\>*

        BK\_BT\_L2CAP\_INIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_init_evt_param6statusE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t20l2cap_init_evt_param6statusE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t20l2cap_init_evt_param6statusE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_init_evt_param::status__bk_bt_l2cap_status_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__init__evt__param_1a96b06956eeb6057c47d65bbbf96aa437"></a> [bk\_bt\_l2cap\_status\_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_paramE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_paramE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_paramE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_open_evt_param"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__open__evt__param"></a> struct l2cap\_open\_evt\_param
    :   *#include \<bk\_dm\_l2cap.h\>*

        BK\_BT\_L2CAP\_OPEN\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param6statusE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param6statusE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param6statusE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_open_evt_param::status__bk_bt_l2cap_status_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__open__evt__param_1ad9630b62df2298cb1dcaf1dc5430f231"></a> [bk\_bt\_l2cap\_status\_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param6handleE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param6handleE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param6handleE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_open_evt_param::handle__uint32_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__open__evt__param_1a1d930a9ca7d18c74e1cd6aeebd782fa5"></a> uint32\_t handle
        :   The connection handle

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param2fdE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param2fdE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param2fdE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_open_evt_param::fd__i"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__open__evt__param_1ab0ecff7eb5b58241d3321a6fe2ba6e07"></a> int fd
        :   File descriptor, lcid

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param7rem_bdaE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param7rem_bdaE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param7rem_bdaE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_open_evt_param::rem_bda__bk_bd_addr_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__open__evt__param_1a5ecf08145434978ca907985288711b18"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rem\_bda
        :   The peer address

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param6tx_mtuE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param6tx_mtuE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t20l2cap_open_evt_param6tx_mtuE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_open_evt_param::tx_mtu__int32_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__open__evt__param_1a205a284f05afc94fc72dd6fb5e89171a"></a> int32\_t tx\_mtu
        :   The transmit MTU

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_paramE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_paramE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_paramE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_srv_stop_evt_param"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__srv__stop__evt__param"></a> struct l2cap\_srv\_stop\_evt\_param
    :   *#include \<bk\_dm\_l2cap.h\>*

        BK\_BT\_L2CAP\_SRV\_STOP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_param6statusE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_param6statusE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_param6statusE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_srv_stop_evt_param::status__bk_bt_l2cap_status_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__srv__stop__evt__param_1a4f6fd976d1f0b1eb423f81e45c085b0a"></a> [bk\_bt\_l2cap\_status\_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_param3psmE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_param3psmE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t24l2cap_srv_stop_evt_param3psmE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_srv_stop_evt_param::psm__uint16_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__srv__stop__evt__param_1ac3bf517d816ec9767ba2dceecdff757a"></a> uint16\_t psm
        :   local psm

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_paramE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_paramE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_paramE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_start_evt_param"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__start__evt__param"></a> struct l2cap\_start\_evt\_param
    :   *#include \<bk\_dm\_l2cap.h\>*

        BK\_BT\_L2CAP\_START\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_param6statusE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_param6statusE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_param6statusE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_start_evt_param::status__bk_bt_l2cap_status_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__start__evt__param_1a33b79745531b199a5d4491002d31059d"></a> [bk\_bt\_l2cap\_status\_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_param6handleE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_param6handleE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_param6handleE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_start_evt_param::handle__uint32_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__start__evt__param_1a82da31f05876ab8957946035263d7f2d"></a> uint32\_t handle
        :   The connection handle

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_param6sec_idE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_param6sec_idE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t21l2cap_start_evt_param6sec_idE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_start_evt_param::sec_id__uint8_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__start__evt__param_1a27091589662b1cd27b6b5e0c8c8c2145"></a> uint8\_t sec\_id
        :   security ID used by this server

    <a id="_CPPv4N22bk_bt_l2cap_cb_param_t22l2cap_uninit_evt_paramE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_param_t22l2cap_uninit_evt_paramE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t22l2cap_uninit_evt_paramE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_uninit_evt_param"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__uninit__evt__param"></a> struct l2cap\_uninit\_evt\_param
    :   *#include \<bk\_dm\_l2cap.h\>*

        BK\_BT\_L2CAP\_UNINIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_bt_l2cap_cb_param_t22l2cap_uninit_evt_param6statusE"></a>

        <a id="_CPPv3N22bk_bt_l2cap_cb_param_t22l2cap_uninit_evt_param6statusE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_param_t22l2cap_uninit_evt_param6statusE"></a> <a id="bk_bt_l2cap_cb_param_t::l2cap_uninit_evt_param::status__bk_bt_l2cap_status_t"></a> <a id="structbk__bt__l2cap__cb__param__t_1_1l2cap__uninit__evt__param_1a56b72429d7089a845c1d72ee7c3fd97b"></a> [bk\_bt\_l2cap\_status\_t](#_CPPv420bk_bt_l2cap_status_t "bk_bt_l2cap_status_t") status
        :   status

<a id="id22"></a>

### Macros

<a id="c.BK_BT_L2CAP_SEC_NONE"></a>

<a id="bk__dm__l2cap_8h_1ae7a131f3c5bef9b93cb84be742f71f9e"></a> BK\_BT\_L2CAP\_SEC\_NONE
:   Security Setting Mask. Use these three mask mode:

    1. BK\_BT\_L2CAP\_SEC\_NONE
    2. BK\_BT\_L2CAP\_SEC\_AUTHENTICATE
    3. (BK\_BT\_L2CAP\_SEC\_ENCRYPT\|BK\_BT\_L2CAP\_SEC\_AUTHENTICATE) No security

<a id="c.BK_BT_L2CAP_SEC_AUTHORIZE"></a>

<a id="bk__dm__l2cap_8h_1a0ece4caa2f597f7f5481cee5db884c57"></a> BK\_BT\_L2CAP\_SEC\_AUTHORIZE
:   Authorization required

<a id="c.BK_BT_L2CAP_SEC_AUTHENTICATE"></a>

<a id="bk__dm__l2cap_8h_1ae4123723f1c12b001284953ea33c79b4"></a> BK\_BT\_L2CAP\_SEC\_AUTHENTICATE
:   Authentication required

<a id="c.BK_BT_L2CAP_SEC_ENCRYPT"></a>

<a id="bk__dm__l2cap_8h_1a2de2570706ede6b8f966f3b429c50928"></a> BK\_BT\_L2CAP\_SEC\_ENCRYPT
:   Encryption required

<a id="id23"></a>

### Type Definitions

<a id="_CPPv424bk_bt_l2cap_cntl_flags_t"></a>

<a id="_CPPv324bk_bt_l2cap_cntl_flags_t"></a> <a id="_CPPv224bk_bt_l2cap_cntl_flags_t"></a> <a id="bk_bt_l2cap_cntl_flags_t"></a> <a id="bk__dm__l2cap_8h_1ad143323966ca98f9728f555b9a272426"></a> typedef uint32\_t bk\_bt\_l2cap\_cntl\_flags\_t

<a id="_CPPv416bk_bt_l2cap_cb_t"></a>

<a id="_CPPv316bk_bt_l2cap_cb_t"></a> <a id="_CPPv216bk_bt_l2cap_cb_t"></a> <a id="bk_bt_l2cap_cb_t"></a> <a id="bk__dm__l2cap_8h_1a815562e3d1a6bd11fab16847088617cb"></a> typedef void (\*bk\_bt\_l2cap\_cb\_t)([bk\_bt\_l2cap\_cb\_event\_t](#_CPPv422bk_bt_l2cap_cb_event_t "bk_bt_l2cap_cb_event_t") event, [bk\_bt\_l2cap\_cb\_param\_t](#_CPPv422bk_bt_l2cap_cb_param_t "bk_bt_l2cap_cb_param_t") \*param)
:   L2CAP callback function type.

    Param event
    :   Event type

    Param param
    :   Point to callback parameter, currently is union type

<a id="_CPPv421bk_bt_l2cap_data_cb_t"></a>

<a id="_CPPv321bk_bt_l2cap_data_cb_t"></a> <a id="_CPPv221bk_bt_l2cap_data_cb_t"></a> <a id="bk_bt_l2cap_data_cb_t"></a> <a id="bk__dm__l2cap_8h_1aa447e9543c3dbcc1f4f19184bc9ac395"></a> typedef void (\*bk\_bt\_l2cap\_data\_cb\_t)(int fd, void \*data, uint16\_t size)
:   L2CAP callback function type.

    Param fd
    :   File descriptor.

    Param data
    :   pointer to data.

    Param len
    :   data length

<a id="id24"></a>

### Enumerations

<a id="_CPPv420bk_bt_l2cap_status_t"></a>

<a id="_CPPv320bk_bt_l2cap_status_t"></a> <a id="_CPPv220bk_bt_l2cap_status_t"></a> <a id="bk__dm__l2cap_8h_1aa5b7ec0a7dec8e9ee216ecb02a196ad8"></a> enum bk\_bt\_l2cap\_status\_t
:   L2CAP operation success and failure codes.

    *Values:*

    <a id="_CPPv4N20bk_bt_l2cap_status_t19BK_BT_L2CAP_SUCCESSE"></a>

    <a id="_CPPv3N20bk_bt_l2cap_status_t19BK_BT_L2CAP_SUCCESSE"></a> <a id="_CPPv2N20bk_bt_l2cap_status_t19BK_BT_L2CAP_SUCCESSE"></a> <a id="bk__dm__l2cap_8h_1aa5b7ec0a7dec8e9ee216ecb02a196ad8a5b493197cd2cceebb8b15572ee9ce215"></a> enumerator BK\_BT\_L2CAP\_SUCCESS
    :   Successful operation.

    <a id="_CPPv4N20bk_bt_l2cap_status_t19BK_BT_L2CAP_FAILUREE"></a>

    <a id="_CPPv3N20bk_bt_l2cap_status_t19BK_BT_L2CAP_FAILUREE"></a> <a id="_CPPv2N20bk_bt_l2cap_status_t19BK_BT_L2CAP_FAILUREE"></a> <a id="bk__dm__l2cap_8h_1aa5b7ec0a7dec8e9ee216ecb02a196ad8a2933902bce6ab967216a8066bcde5662"></a> enumerator BK\_BT\_L2CAP\_FAILURE
    :   Generic failure.

    <a id="_CPPv4N20bk_bt_l2cap_status_t16BK_BT_L2CAP_BUSYE"></a>

    <a id="_CPPv3N20bk_bt_l2cap_status_t16BK_BT_L2CAP_BUSYE"></a> <a id="_CPPv2N20bk_bt_l2cap_status_t16BK_BT_L2CAP_BUSYE"></a> <a id="bk__dm__l2cap_8h_1aa5b7ec0a7dec8e9ee216ecb02a196ad8a33119fce5afad4585bd6723da3d86b40"></a> enumerator BK\_BT\_L2CAP\_BUSY
    :   Temporarily can not handle this request.

    <a id="_CPPv4N20bk_bt_l2cap_status_t23BK_BT_L2CAP_NO_RESOURCEE"></a>

    <a id="_CPPv3N20bk_bt_l2cap_status_t23BK_BT_L2CAP_NO_RESOURCEE"></a> <a id="_CPPv2N20bk_bt_l2cap_status_t23BK_BT_L2CAP_NO_RESOURCEE"></a> <a id="bk__dm__l2cap_8h_1aa5b7ec0a7dec8e9ee216ecb02a196ad8a5944da3fcc48d1738a25926f0db6b0f7"></a> enumerator BK\_BT\_L2CAP\_NO\_RESOURCE
    :   No more resource

    <a id="_CPPv4N20bk_bt_l2cap_status_t21BK_BT_L2CAP_NEED_INITE"></a>

    <a id="_CPPv3N20bk_bt_l2cap_status_t21BK_BT_L2CAP_NEED_INITE"></a> <a id="_CPPv2N20bk_bt_l2cap_status_t21BK_BT_L2CAP_NEED_INITE"></a> <a id="bk__dm__l2cap_8h_1aa5b7ec0a7dec8e9ee216ecb02a196ad8a3dab0fd096e022160780e4b58113b684"></a> enumerator BK\_BT\_L2CAP\_NEED\_INIT
    :   L2CAP module shall init first

    <a id="_CPPv4N20bk_bt_l2cap_status_t23BK_BT_L2CAP_NEED_DEINITE"></a>

    <a id="_CPPv3N20bk_bt_l2cap_status_t23BK_BT_L2CAP_NEED_DEINITE"></a> <a id="_CPPv2N20bk_bt_l2cap_status_t23BK_BT_L2CAP_NEED_DEINITE"></a> <a id="bk__dm__l2cap_8h_1aa5b7ec0a7dec8e9ee216ecb02a196ad8a15de0bb41b7ada2ad3ebef05383bfcab"></a> enumerator BK\_BT\_L2CAP\_NEED\_DEINIT
    :   L2CAP module shall deinit first

    <a id="_CPPv4N20bk_bt_l2cap_status_t25BK_BT_L2CAP_NO_CONNECTIONE"></a>

    <a id="_CPPv3N20bk_bt_l2cap_status_t25BK_BT_L2CAP_NO_CONNECTIONE"></a> <a id="_CPPv2N20bk_bt_l2cap_status_t25BK_BT_L2CAP_NO_CONNECTIONE"></a> <a id="bk__dm__l2cap_8h_1aa5b7ec0a7dec8e9ee216ecb02a196ad8a0548b73014f058a1b94d7bb4aa759256"></a> enumerator BK\_BT\_L2CAP\_NO\_CONNECTION
    :   Connection may have been closed

    <a id="_CPPv4N20bk_bt_l2cap_status_t21BK_BT_L2CAP_NO_SERVERE"></a>

    <a id="_CPPv3N20bk_bt_l2cap_status_t21BK_BT_L2CAP_NO_SERVERE"></a> <a id="_CPPv2N20bk_bt_l2cap_status_t21BK_BT_L2CAP_NO_SERVERE"></a> <a id="bk__dm__l2cap_8h_1aa5b7ec0a7dec8e9ee216ecb02a196ad8a5fa79656269cf642f165867e3fe6cf22"></a> enumerator BK\_BT\_L2CAP\_NO\_SERVER
    :   No server

<a id="_CPPv422bk_bt_l2cap_cb_event_t"></a>

<a id="_CPPv322bk_bt_l2cap_cb_event_t"></a> <a id="_CPPv222bk_bt_l2cap_cb_event_t"></a> <a id="bk__dm__l2cap_8h_1ad429f32f74c09dbf98a0a690e53693de"></a> enum bk\_bt\_l2cap\_cb\_event\_t
:   L2CAP callback function events.

    *Values:*

    <a id="_CPPv4N22bk_bt_l2cap_cb_event_t20BK_BT_L2CAP_INIT_EVTE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_event_t20BK_BT_L2CAP_INIT_EVTE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_event_t20BK_BT_L2CAP_INIT_EVTE"></a> <a id="bk__dm__l2cap_8h_1ad429f32f74c09dbf98a0a690e53693dea29e4f10ffc1d71af5e463f1b92f09259"></a> enumerator BK\_BT\_L2CAP\_INIT\_EVT
    :   When L2CAP is initialized, the event comes

    <a id="_CPPv4N22bk_bt_l2cap_cb_event_t22BK_BT_L2CAP_UNINIT_EVTE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_event_t22BK_BT_L2CAP_UNINIT_EVTE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_event_t22BK_BT_L2CAP_UNINIT_EVTE"></a> <a id="bk__dm__l2cap_8h_1ad429f32f74c09dbf98a0a690e53693dea0261d57b132c9b65e8515f76f7340019"></a> enumerator BK\_BT\_L2CAP\_UNINIT\_EVT
    :   When L2CAP is deinitialized, the event comes

    <a id="_CPPv4N22bk_bt_l2cap_cb_event_t20BK_BT_L2CAP_OPEN_EVTE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_event_t20BK_BT_L2CAP_OPEN_EVTE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_event_t20BK_BT_L2CAP_OPEN_EVTE"></a> <a id="bk__dm__l2cap_8h_1ad429f32f74c09dbf98a0a690e53693dea3f9cbc042df266ae98762f08d970b2fa"></a> enumerator BK\_BT\_L2CAP\_OPEN\_EVT
    :   When L2CAP Client connection open, the event comes

    <a id="_CPPv4N22bk_bt_l2cap_cb_event_t21BK_BT_L2CAP_CLOSE_EVTE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_event_t21BK_BT_L2CAP_CLOSE_EVTE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_event_t21BK_BT_L2CAP_CLOSE_EVTE"></a> <a id="bk__dm__l2cap_8h_1ad429f32f74c09dbf98a0a690e53693dea1623e769a7c7c64a715c5c26b1e07693"></a> enumerator BK\_BT\_L2CAP\_CLOSE\_EVT
    :   When L2CAP connection closed, the event comes

    <a id="_CPPv4N22bk_bt_l2cap_cb_event_t21BK_BT_L2CAP_START_EVTE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_event_t21BK_BT_L2CAP_START_EVTE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_event_t21BK_BT_L2CAP_START_EVTE"></a> <a id="bk__dm__l2cap_8h_1ad429f32f74c09dbf98a0a690e53693deabee57920df7574d6084b81bfbd913d7d"></a> enumerator BK\_BT\_L2CAP\_START\_EVT
    :   When L2CAP server started, the event comes

    <a id="_CPPv4N22bk_bt_l2cap_cb_event_t23BK_BT_L2CAP_CL_INIT_EVTE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_event_t23BK_BT_L2CAP_CL_INIT_EVTE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_event_t23BK_BT_L2CAP_CL_INIT_EVTE"></a> <a id="bk__dm__l2cap_8h_1ad429f32f74c09dbf98a0a690e53693deabd5215f82e49174fdce1d54a51803136"></a> enumerator BK\_BT\_L2CAP\_CL\_INIT\_EVT
    :   When L2CAP client initiated a connection, the event comes

    <a id="_CPPv4N22bk_bt_l2cap_cb_event_t24BK_BT_L2CAP_SRV_STOP_EVTE"></a>

    <a id="_CPPv3N22bk_bt_l2cap_cb_event_t24BK_BT_L2CAP_SRV_STOP_EVTE"></a> <a id="_CPPv2N22bk_bt_l2cap_cb_event_t24BK_BT_L2CAP_SRV_STOP_EVTE"></a> <a id="bk__dm__l2cap_8h_1ad429f32f74c09dbf98a0a690e53693dea0674ef7bcc955afce5524ad6769e1a2b"></a> enumerator BK\_BT\_L2CAP\_SRV\_STOP\_EVT
    :   When L2CAP server stopped, the event comes

<a id="bk-dm-spp-h"></a>

## bk\_dm\_spp.h

`bk_dm_spp.h` 提供 Serial Port Profile 连接和数据传输接口。

<a id="id25"></a>

### Header File

- [bk\_dm\_spp.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_spp.h)

<a id="id26"></a>

### Functions

<a id="_CPPv424bk_spp_register_callback11bk_spp_cb_t"></a>

<a id="_CPPv324bk_spp_register_callback11bk_spp_cb_t"></a> <a id="_CPPv224bk_spp_register_callback11bk_spp_cb_t"></a> <a id="bk_spp_register_callback__bk_spp_cb_t"></a> <a id="bk__dm__spp_8h_1ad6ca0e36eb93f5590a023cb7ff009327"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_register\_callback([bk\_spp\_cb\_t](#_CPPv411bk_spp_cb_t "bk_spp_cb_t") callback)
:   This function is called to init callbacks with SPP module.

    参数
    :   **callback** – **\[in\]** pointer to the init callback function.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv411bk_spp_initv"></a>

<a id="_CPPv311bk_spp_initv"></a> <a id="_CPPv211bk_spp_initv"></a> <a id="bk_spp_init"></a> <a id="bk__dm__spp_8h_1aa5bc0c36231b1c02cd63d7aedef1e6fd"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_init()
:   This function is called to init SPP module. When the operation is completed, the callback function will be called with BK\_SPP\_INIT\_EVT. This function should be called after bk\_bluedroid\_enable() completes successfully.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv413bk_spp_deinitv"></a>

<a id="_CPPv313bk_spp_deinitv"></a> <a id="_CPPv213bk_spp_deinitv"></a> <a id="bk_spp_deinit__void"></a> <a id="bk__dm__spp_8h_1a2d62a26b39110e1ff6b0bf8d33ad136d"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_deinit(void)
:   This function is called to uninit SPP module. The operation will close all active SPP connection first, then the callback function will be called with BK\_SPP\_CLOSE\_EVT, and the number of BK\_SPP\_CLOSE\_EVT is equal to the number of connection. When the operation is completed, the callback function will be called with BK\_SPP\_UNINIT\_EVT. This function should be called after bk\_spp\_init()/bk\_spp\_enhanced\_init() completes successfully.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv422bk_spp_start_discovery12bk_bd_addr_t"></a>

<a id="_CPPv322bk_spp_start_discovery12bk_bd_addr_t"></a> <a id="_CPPv222bk_spp_start_discovery12bk_bd_addr_t"></a> <a id="bk_spp_start_discovery__bk_bd_addr_t"></a> <a id="bk__dm__spp_8h_1ab57ddce66905307df5cf7eb5896f2bf0"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_start\_discovery([bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bd\_addr)
:   This function is called to performs service discovery for the services provided by the given peer device. When the operation is completed, the callback function will be called with BK\_SPP\_DISCOVERY\_COMP\_EVT. This function must be called after bk\_spp\_init()/bk\_spp\_enhanced\_init() successful and before bk\_spp\_deinit().

    参数
    :   **bd\_addr** – **\[in\]** Remote device bluetooth device address.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv414bk_spp_connect13bk_spp_role_t7uint8_tP7uint8_t"></a>

<a id="_CPPv314bk_spp_connect13bk_spp_role_t7uint8_tP7uint8_t"></a> <a id="_CPPv214bk_spp_connect13bk_spp_role_t7uint8_tP7uint8_t"></a> <a id="bk_spp_connect__bk_spp_role_t.uint8_t.uint8_tP"></a> <a id="bk__dm__spp_8h_1a325da42ed6dac34b5fd610b2c833ea14"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_connect([bk\_spp\_role\_t](#_CPPv413bk_spp_role_t "bk_spp_role_t") role, uint8\_t remote\_scn, uint8\_t \*peer\_bd\_addr)
:   This function makes an SPP connection to a remote BD Address. When the connection is initiated or failed to initiate, the callback is called with BK\_SPP\_CL\_INIT\_EVT. When the connection is established or failed, the callback is called with BK\_SPP\_OPEN\_EVT. This function must be called after bk\_spp\_init()/bk\_spp\_enhanced\_init() successful and before bk\_spp\_deinit().

    参数
    :   - **role** – **\[in\]** Master or slave.
        - **remote\_scn** – **\[in\]** Remote device bluetooth device SCN.
        - **peer\_bd\_addr** – **\[in\]** Remote device bluetooth device address.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv417bk_spp_disconnect8uint32_t"></a>

<a id="_CPPv317bk_spp_disconnect8uint32_t"></a> <a id="_CPPv217bk_spp_disconnect8uint32_t"></a> <a id="bk_spp_disconnect__uint32_t"></a> <a id="bk__dm__spp_8h_1a670f5635b29dbb05440b7869766a6b89"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_disconnect(uint32\_t handle)
:   This function closes an SPP connection. When the operation is completed, the callback function will be called with BK\_SPP\_CLOSE\_EVT. This function must be called after bk\_spp\_init()/bk\_spp\_enhanced\_init() successful and before bk\_spp\_deinit().

    参数
    :   **handle** – **\[in\]** The connection handle.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv416bk_spp_start_srv13bk_spp_role_t7uint8_tPKc"></a>

<a id="_CPPv316bk_spp_start_srv13bk_spp_role_t7uint8_tPKc"></a> <a id="_CPPv216bk_spp_start_srv13bk_spp_role_t7uint8_tPKc"></a> <a id="bk_spp_start_srv__bk_spp_role_t.uint8_t.cCP"></a> <a id="bk__dm__spp_8h_1ab17d4032630bfddbe93e61c196a89575"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_start\_srv([bk\_spp\_role\_t](#_CPPv413bk_spp_role_t "bk_spp_role_t") role, uint8\_t local\_scn, const char \*name)
:   This function create a SPP server and starts listening for an SPP connection request from a remote Bluetooth device. When the server is started successfully, the callback is called with BK\_SPP\_START\_EVT. When the connection is established, the callback is called with BK\_SPP\_SRV\_OPEN\_EVT. This function must be called after bk\_spp\_init()/bk\_spp\_enhanced\_init() successful and before bk\_spp\_deinit().

    参数
    :   - **role** – **\[in\]** Master or slave.
        - **local\_scn** – **\[in\]** The specific channel you want to get. If channel is 0, means get any channel.
        - **name** – **\[in\]** Server’s name.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv415bk_spp_stop_srvv"></a>

<a id="_CPPv315bk_spp_stop_srvv"></a> <a id="_CPPv215bk_spp_stop_srvv"></a> <a id="bk_spp_stop_srv__void"></a> <a id="bk__dm__spp_8h_1a35328d94ceb297ed8c5bafb22f5cb1d6"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_stop\_srv(void)
:   This function stops all SPP servers. The operation will close all active SPP connection first, then the callback function will be called with BK\_SPP\_CLOSE\_EVT, and the number of BK\_SPP\_CLOSE\_EVT is equal to the number of connection. When the operation is completed, the callback is called with BK\_SPP\_SRV\_STOP\_EVT. This function must be called after bk\_spp\_init()/bk\_spp\_enhanced\_init() successful and before bk\_spp\_deinit().

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv419bk_spp_stop_srv_scn7uint8_t"></a>

<a id="_CPPv319bk_spp_stop_srv_scn7uint8_t"></a> <a id="_CPPv219bk_spp_stop_srv_scn7uint8_t"></a> <a id="bk_spp_stop_srv_scn__uint8_t"></a> <a id="bk__dm__spp_8h_1a25db11e213e0cbc0cf9d85dbc30139b1"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_stop\_srv\_scn(uint8\_t scn)
:   This function stops a specific SPP server. The operation will close all active SPP connection first on the specific SPP server, then the callback function will be called with BK\_SPP\_CLOSE\_EVT, and the number of BK\_SPP\_CLOSE\_EVT is equal to the number of connection. When the operation is completed, the callback is called with BK\_SPP\_SRV\_STOP\_EVT. This function must be called after bk\_spp\_init()/bk\_spp\_enhanced\_init() successful and before bk\_spp\_deinit().

    参数
    :   **scn** – **\[in\]** Server channel number.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="_CPPv412bk_spp_write8uint32_tiP7uint8_t"></a>

<a id="_CPPv312bk_spp_write8uint32_tiP7uint8_t"></a> <a id="_CPPv212bk_spp_write8uint32_tiP7uint8_t"></a> <a id="bk_spp_write__uint32_t.i.uint8_tP"></a> <a id="bk__dm__spp_8h_1adcf4b7f89685eb5a26e2227260053341"></a> [bt\_err\_t](dual_ble.md#_CPPv48bt_err_t "bt_err_t") bk\_spp\_write(uint32\_t handle, int len, uint8\_t \*p\_data)
:   This function is used to write data, only for BK\_SPP\_MODE\_CB. When this function need to be called repeatedly, it is strongly recommended to call this function again after the previous event BK\_SPP\_WRITE\_EVT is received and the parameter ‘cong’ is equal to false. If the previous event BK\_SPP\_WRITE\_EVT with parameter ‘cong’ is equal to true, the function can only be called again when the event BK\_SPP\_CONG\_EVT with parameter ‘cong’ equal to false is received. This function must be called after an connection between initiator and acceptor has been established.

    参数
    :   - **handle** – **\[in\]** The connection handle.
        - **len** – **\[in\]** The length of the data written.
        - **p\_data** – **\[in\]** The data written.

    返回
    :   - BK\_OK: success
        - other: failed

<a id="id27"></a>

### Unions

<a id="_CPPv417bk_spp_cb_param_t"></a>

<a id="_CPPv317bk_spp_cb_param_t"></a> <a id="_CPPv217bk_spp_cb_param_t"></a> <a id="unionbk__spp__cb__param__t"></a> union bk\_spp\_cb\_param\_t
:   *#include \<bk\_dm\_spp.h\>*

    SPP callback parameters union.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_spp_cb_param_t4initE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t4initE"></a> <a id="_CPPv2N17bk_spp_cb_param_t4initE"></a> <a id="bk_spp_cb_param_t::init__bk_spp_cb_param_t::spp_init_evt_param"></a> <a id="unionbk__spp__cb__param__t_1a9d3b9956c5c5aebb958fa4fa5c995a43"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_init\_evt\_param](#_CPPv4N17bk_spp_cb_param_t18spp_init_evt_paramE "bk_spp_cb_param_t::spp_init_evt_param") init
    :   SPP callback param of SPP\_INIT\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t6uninitE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t6uninitE"></a> <a id="_CPPv2N17bk_spp_cb_param_t6uninitE"></a> <a id="bk_spp_cb_param_t::uninit__bk_spp_cb_param_t::spp_uninit_evt_param"></a> <a id="unionbk__spp__cb__param__t_1ade9a1ca30b4a765ab8fa78efd68e8c19"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_uninit\_evt\_param](#_CPPv4N17bk_spp_cb_param_t20spp_uninit_evt_paramE "bk_spp_cb_param_t::spp_uninit_evt_param") uninit
    :   SPP callback param of SPP\_UNINIT\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t9disc_compE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t9disc_compE"></a> <a id="_CPPv2N17bk_spp_cb_param_t9disc_compE"></a> <a id="bk_spp_cb_param_t::disc_comp__bk_spp_cb_param_t::spp_discovery_comp_evt_param"></a> <a id="unionbk__spp__cb__param__t_1a0d86e3b70214b7b32486ee54589b8af0"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_discovery\_comp\_evt\_param](#_CPPv4N17bk_spp_cb_param_t28spp_discovery_comp_evt_paramE "bk_spp_cb_param_t::spp_discovery_comp_evt_param") disc\_comp
    :   SPP callback param of SPP\_DISCOVERY\_COMP\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t4openE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t4openE"></a> <a id="_CPPv2N17bk_spp_cb_param_t4openE"></a> <a id="bk_spp_cb_param_t::open__bk_spp_cb_param_t::spp_open_evt_param"></a> <a id="unionbk__spp__cb__param__t_1a4cee8ed599f6662733adf75490903ad8"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_open\_evt\_param](#_CPPv4N17bk_spp_cb_param_t18spp_open_evt_paramE "bk_spp_cb_param_t::spp_open_evt_param") open
    :   SPP callback param of BK\_SPP\_OPEN\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t8srv_openE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t8srv_openE"></a> <a id="_CPPv2N17bk_spp_cb_param_t8srv_openE"></a> <a id="bk_spp_cb_param_t::srv_open__bk_spp_cb_param_t::spp_srv_open_evt_param"></a> <a id="unionbk__spp__cb__param__t_1a5b33f694bc36d0ab88038667e0c1c79b"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_srv\_open\_evt\_param](#_CPPv4N17bk_spp_cb_param_t22spp_srv_open_evt_paramE "bk_spp_cb_param_t::spp_srv_open_evt_param") srv\_open
    :   SPP callback param of BK\_SPP\_SRV\_OPEN\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t5closeE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t5closeE"></a> <a id="_CPPv2N17bk_spp_cb_param_t5closeE"></a> <a id="bk_spp_cb_param_t::close__bk_spp_cb_param_t::spp_close_evt_param"></a> <a id="unionbk__spp__cb__param__t_1acbd69e969b3a6f80c912a684a3491518"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_close\_evt\_param](#_CPPv4N17bk_spp_cb_param_t19spp_close_evt_paramE "bk_spp_cb_param_t::spp_close_evt_param") close
    :   SPP callback param of BK\_SPP\_CLOSE\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t5startE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t5startE"></a> <a id="_CPPv2N17bk_spp_cb_param_t5startE"></a> <a id="bk_spp_cb_param_t::start__bk_spp_cb_param_t::spp_start_evt_param"></a> <a id="unionbk__spp__cb__param__t_1adf5fc267b9cb61c5fd136baa901b949c"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_start\_evt\_param](#_CPPv4N17bk_spp_cb_param_t19spp_start_evt_paramE "bk_spp_cb_param_t::spp_start_evt_param") start
    :   SPP callback param of BK\_SPP\_START\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t8srv_stopE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t8srv_stopE"></a> <a id="_CPPv2N17bk_spp_cb_param_t8srv_stopE"></a> <a id="bk_spp_cb_param_t::srv_stop__bk_spp_cb_param_t::spp_srv_stop_evt_param"></a> <a id="unionbk__spp__cb__param__t_1a10303a1b53fef0f681577501ace105a1"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_srv\_stop\_evt\_param](#_CPPv4N17bk_spp_cb_param_t22spp_srv_stop_evt_paramE "bk_spp_cb_param_t::spp_srv_stop_evt_param") srv\_stop
    :   SPP callback param of BK\_SPP\_SRV\_STOP\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t7cl_initE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t7cl_initE"></a> <a id="_CPPv2N17bk_spp_cb_param_t7cl_initE"></a> <a id="bk_spp_cb_param_t::cl_init__bk_spp_cb_param_t::spp_cl_init_evt_param"></a> <a id="unionbk__spp__cb__param__t_1ad07c1790b5731418eacca2cd06c70349"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_cl\_init\_evt\_param](#_CPPv4N17bk_spp_cb_param_t21spp_cl_init_evt_paramE "bk_spp_cb_param_t::spp_cl_init_evt_param") cl\_init
    :   SPP callback param of BK\_SPP\_CL\_INIT\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t5writeE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t5writeE"></a> <a id="_CPPv2N17bk_spp_cb_param_t5writeE"></a> <a id="bk_spp_cb_param_t::write__bk_spp_cb_param_t::spp_write_evt_param"></a> <a id="unionbk__spp__cb__param__t_1a6d5fda254284ca8be9b06b994fc19034"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_write\_evt\_param](#_CPPv4N17bk_spp_cb_param_t19spp_write_evt_paramE "bk_spp_cb_param_t::spp_write_evt_param") write
    :   SPP callback param of BK\_SPP\_WRITE\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t8data_indE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t8data_indE"></a> <a id="_CPPv2N17bk_spp_cb_param_t8data_indE"></a> <a id="bk_spp_cb_param_t::data_ind__bk_spp_cb_param_t::spp_data_ind_evt_param"></a> <a id="unionbk__spp__cb__param__t_1a80b4426ef6be0497ed4c25132ceaa75a"></a> struct [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t")::[spp\_data\_ind\_evt\_param](#_CPPv4N17bk_spp_cb_param_t22spp_data_ind_evt_paramE "bk_spp_cb_param_t::spp_data_ind_evt_param") data\_ind
    :   SPP callback param of BK\_SPP\_DATA\_IND\_EVT

    <a id="_CPPv4N17bk_spp_cb_param_t21spp_cl_init_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t21spp_cl_init_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t21spp_cl_init_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_cl_init_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__cl__init__evt__param"></a> struct spp\_cl\_init\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        BK\_SPP\_CL\_INIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t21spp_cl_init_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t21spp_cl_init_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t21spp_cl_init_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_cl_init_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__cl__init__evt__param_1a11d12802fc91b7496b4770d14a2d3907"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        <a id="_CPPv4N17bk_spp_cb_param_t21spp_cl_init_evt_param6handleE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t21spp_cl_init_evt_param6handleE"></a> <a id="_CPPv2N17bk_spp_cb_param_t21spp_cl_init_evt_param6handleE"></a> <a id="bk_spp_cb_param_t::spp_cl_init_evt_param::handle__uint32_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__cl__init__evt__param_1a11561f3016ea743c3ea0d522742a4cbf"></a> uint32\_t handle
        :   The connection handle

    <a id="_CPPv4N17bk_spp_cb_param_t19spp_close_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t19spp_close_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_close_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_close_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__close__evt__param"></a> struct spp\_close\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        BK\_SPP\_CLOSE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t19spp_close_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t19spp_close_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_close_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_close_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__close__evt__param_1a68fe59f0a5087ede3fcd96613f0796db"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        <a id="_CPPv4N17bk_spp_cb_param_t19spp_close_evt_param6handleE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t19spp_close_evt_param6handleE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_close_evt_param6handleE"></a> <a id="bk_spp_cb_param_t::spp_close_evt_param::handle__uint32_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__close__evt__param_1ac4e2226a26fb66f734d830c25f5903db"></a> uint32\_t handle
        :   The connection handle

    <a id="_CPPv4N17bk_spp_cb_param_t22spp_data_ind_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t22spp_data_ind_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_data_ind_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_data_ind_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__data__ind__evt__param"></a> struct spp\_data\_ind\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        BK\_SPP\_DATA\_IND\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t22spp_data_ind_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t22spp_data_ind_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_data_ind_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_data_ind_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__data__ind__evt__param_1a473138e769f09d219827bfb175cd20b0"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        <a id="_CPPv4N17bk_spp_cb_param_t22spp_data_ind_evt_param6handleE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t22spp_data_ind_evt_param6handleE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_data_ind_evt_param6handleE"></a> <a id="bk_spp_cb_param_t::spp_data_ind_evt_param::handle__uint32_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__data__ind__evt__param_1a6073e80a0578535fb5b1ce2d7e7f1fe2"></a> uint32\_t handle
        :   The connection handle

        <a id="_CPPv4N17bk_spp_cb_param_t22spp_data_ind_evt_param3lenE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t22spp_data_ind_evt_param3lenE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_data_ind_evt_param3lenE"></a> <a id="bk_spp_cb_param_t::spp_data_ind_evt_param::len__uint16_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__data__ind__evt__param_1ad3582a597ea64f011737dffcc8b1c373"></a> uint16\_t len
        :   The length of data

        <a id="_CPPv4N17bk_spp_cb_param_t22spp_data_ind_evt_param4dataE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t22spp_data_ind_evt_param4dataE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_data_ind_evt_param4dataE"></a> <a id="bk_spp_cb_param_t::spp_data_ind_evt_param::data__uint8_tP"></a> <a id="structbk__spp__cb__param__t_1_1spp__data__ind__evt__param_1afc003cbc8352398b0c94f9996a6d8674"></a> uint8\_t \*data
        :   The data received

    <a id="_CPPv4N17bk_spp_cb_param_t28spp_discovery_comp_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t28spp_discovery_comp_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t28spp_discovery_comp_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_discovery_comp_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__discovery__comp__evt__param"></a> struct spp\_discovery\_comp\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        SPP\_DISCOVERY\_COMP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t28spp_discovery_comp_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t28spp_discovery_comp_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t28spp_discovery_comp_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_discovery_comp_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__discovery__comp__evt__param_1a008f1eeae0f4d112567d05921e0b30a1"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        <a id="_CPPv4N17bk_spp_cb_param_t28spp_discovery_comp_evt_param7scn_numE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t28spp_discovery_comp_evt_param7scn_numE"></a> <a id="_CPPv2N17bk_spp_cb_param_t28spp_discovery_comp_evt_param7scn_numE"></a> <a id="bk_spp_cb_param_t::spp_discovery_comp_evt_param::scn_num__uint8_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__discovery__comp__evt__param_1a9cf53e7df3b13516244fe0e76647deff"></a> uint8\_t scn\_num
        :   The num of scn\_num

        <a id="_CPPv4N17bk_spp_cb_param_t28spp_discovery_comp_evt_param3scnE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t28spp_discovery_comp_evt_param3scnE"></a> <a id="_CPPv2N17bk_spp_cb_param_t28spp_discovery_comp_evt_param3scnE"></a> <a id="bk_spp_cb_param_t::spp_discovery_comp_evt_param::scn__uint8_tA"></a> <a id="structbk__spp__cb__param__t_1_1spp__discovery__comp__evt__param_1a8b43358f11f5f7d2e3f47d1305088e96"></a> uint8\_t scn\[BK\_SPP\_MAX\_SCN\]
        :   channel \#

        <a id="_CPPv4N17bk_spp_cb_param_t28spp_discovery_comp_evt_param12service_nameE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t28spp_discovery_comp_evt_param12service_nameE"></a> <a id="_CPPv2N17bk_spp_cb_param_t28spp_discovery_comp_evt_param12service_nameE"></a> <a id="bk_spp_cb_param_t::spp_discovery_comp_evt_param::service_name__cCPA"></a> <a id="structbk__spp__cb__param__t_1_1spp__discovery__comp__evt__param_1a44a6f949d23aadfca57f6a00adac7e5d"></a> const char \*service\_name\[BK\_SPP\_MAX\_SCN\]
        :   service\_name

    <a id="_CPPv4N17bk_spp_cb_param_t18spp_init_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t18spp_init_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t18spp_init_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_init_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__init__evt__param"></a> struct spp\_init\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        SPP\_INIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t18spp_init_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t18spp_init_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t18spp_init_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_init_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__init__evt__param_1aeffe493de10fd9809e385f7b94e1e9aa"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

    <a id="_CPPv4N17bk_spp_cb_param_t18spp_open_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t18spp_open_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t18spp_open_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_open_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__open__evt__param"></a> struct spp\_open\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        BK\_SPP\_OPEN\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t18spp_open_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t18spp_open_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t18spp_open_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_open_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__open__evt__param_1af0777dc743a49a788d0809e67727c9bb"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        <a id="_CPPv4N17bk_spp_cb_param_t18spp_open_evt_param6handleE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t18spp_open_evt_param6handleE"></a> <a id="_CPPv2N17bk_spp_cb_param_t18spp_open_evt_param6handleE"></a> <a id="bk_spp_cb_param_t::spp_open_evt_param::handle__uint32_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__open__evt__param_1a9ceb2eb54273935fa991094084d24023"></a> uint32\_t handle
        :   The connection handle

        <a id="_CPPv4N17bk_spp_cb_param_t18spp_open_evt_param7rem_bdaE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t18spp_open_evt_param7rem_bdaE"></a> <a id="_CPPv2N17bk_spp_cb_param_t18spp_open_evt_param7rem_bdaE"></a> <a id="bk_spp_cb_param_t::spp_open_evt_param::rem_bda__bk_bd_addr_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__open__evt__param_1ae32da4e1aedb2589dcce415306d26345"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rem\_bda
        :   The peer address

    <a id="_CPPv4N17bk_spp_cb_param_t22spp_srv_open_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t22spp_srv_open_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_srv_open_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_srv_open_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__srv__open__evt__param"></a> struct spp\_srv\_open\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        BK\_SPP\_SRV\_OPEN\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t22spp_srv_open_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t22spp_srv_open_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_srv_open_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_srv_open_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__srv__open__evt__param_1aea14a07396dc8a1846aa1a7dcee4f570"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        <a id="_CPPv4N17bk_spp_cb_param_t22spp_srv_open_evt_param6handleE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t22spp_srv_open_evt_param6handleE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_srv_open_evt_param6handleE"></a> <a id="bk_spp_cb_param_t::spp_srv_open_evt_param::handle__uint32_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__srv__open__evt__param_1a6c3181ded0286107f894c9c58f5a7fa0"></a> uint32\_t handle
        :   The connection handle

        <a id="_CPPv4N17bk_spp_cb_param_t22spp_srv_open_evt_param7rem_bdaE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t22spp_srv_open_evt_param7rem_bdaE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_srv_open_evt_param7rem_bdaE"></a> <a id="bk_spp_cb_param_t::spp_srv_open_evt_param::rem_bda__bk_bd_addr_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__srv__open__evt__param_1ae21882b3208fe3be111a919410221b87"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") rem\_bda
        :   The peer address

    <a id="_CPPv4N17bk_spp_cb_param_t22spp_srv_stop_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t22spp_srv_stop_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_srv_stop_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_srv_stop_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__srv__stop__evt__param"></a> struct spp\_srv\_stop\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        BK\_SPP\_SRV\_STOP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t22spp_srv_stop_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t22spp_srv_stop_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_srv_stop_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_srv_stop_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__srv__stop__evt__param_1a572e7f88f3af9d9664d453960812f975"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        <a id="_CPPv4N17bk_spp_cb_param_t22spp_srv_stop_evt_param3scnE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t22spp_srv_stop_evt_param3scnE"></a> <a id="_CPPv2N17bk_spp_cb_param_t22spp_srv_stop_evt_param3scnE"></a> <a id="bk_spp_cb_param_t::spp_srv_stop_evt_param::scn__uint8_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__srv__stop__evt__param_1a92c9c42d2e485bde6208b9f572671d42"></a> uint8\_t scn
        :   Server channel number

    <a id="_CPPv4N17bk_spp_cb_param_t19spp_start_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t19spp_start_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_start_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_start_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__start__evt__param"></a> struct spp\_start\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        BK\_SPP\_START\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t19spp_start_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t19spp_start_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_start_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_start_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__start__evt__param_1a0377526ba6058a213608acef60962778"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        <a id="_CPPv4N17bk_spp_cb_param_t19spp_start_evt_param6handleE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t19spp_start_evt_param6handleE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_start_evt_param6handleE"></a> <a id="bk_spp_cb_param_t::spp_start_evt_param::handle__uint32_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__start__evt__param_1ac1aead2bf4e36d0bb2b2ec5b81f4f25a"></a> uint32\_t handle
        :   The connection handle

        <a id="_CPPv4N17bk_spp_cb_param_t19spp_start_evt_param3scnE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t19spp_start_evt_param3scnE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_start_evt_param3scnE"></a> <a id="bk_spp_cb_param_t::spp_start_evt_param::scn__uint8_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__start__evt__param_1a987f0c48c49726d98210d71ccadfa1ba"></a> uint8\_t scn
        :   Server channel number

    <a id="_CPPv4N17bk_spp_cb_param_t20spp_uninit_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t20spp_uninit_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t20spp_uninit_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_uninit_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__uninit__evt__param"></a> struct spp\_uninit\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        SPP\_UNINIT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t20spp_uninit_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t20spp_uninit_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t20spp_uninit_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_uninit_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__uninit__evt__param_1aeadaf8098f79330d9e8aeff430e31590"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

    <a id="_CPPv4N17bk_spp_cb_param_t19spp_write_evt_paramE"></a>

    <a id="_CPPv3N17bk_spp_cb_param_t19spp_write_evt_paramE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_write_evt_paramE"></a> <a id="bk_spp_cb_param_t::spp_write_evt_param"></a> <a id="structbk__spp__cb__param__t_1_1spp__write__evt__param"></a> struct spp\_write\_evt\_param
    :   *#include \<bk\_dm\_spp.h\>*

        BK\_SPP\_WRITE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N17bk_spp_cb_param_t19spp_write_evt_param6statusE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t19spp_write_evt_param6statusE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_write_evt_param6statusE"></a> <a id="bk_spp_cb_param_t::spp_write_evt_param::status__bk_spp_status_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__write__evt__param_1ad20a0f2497371b91ff14df59abbddbda"></a> [bk\_spp\_status\_t](#_CPPv415bk_spp_status_t "bk_spp_status_t") status
        :   status

        <a id="_CPPv4N17bk_spp_cb_param_t19spp_write_evt_param6handleE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t19spp_write_evt_param6handleE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_write_evt_param6handleE"></a> <a id="bk_spp_cb_param_t::spp_write_evt_param::handle__uint32_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__write__evt__param_1a209bc27763b2ab8f63286c38b4bc580a"></a> uint32\_t handle
        :   The connection handle

        <a id="_CPPv4N17bk_spp_cb_param_t19spp_write_evt_param3lenE"></a>

        <a id="_CPPv3N17bk_spp_cb_param_t19spp_write_evt_param3lenE"></a> <a id="_CPPv2N17bk_spp_cb_param_t19spp_write_evt_param3lenE"></a> <a id="bk_spp_cb_param_t::spp_write_evt_param::len__uint16_t"></a> <a id="structbk__spp__cb__param__t_1_1spp__write__evt__param_1ae6f44a3c4913176233b7c4274f911a79"></a> uint16\_t len
        :   The length of the data written.

<a id="id28"></a>

### Macros

<a id="c.BK_SPP_MAX_SCN"></a>

<a id="bk__dm__spp_8h_1a785e2d530f816914fa9a6142893add81"></a> BK\_SPP\_MAX\_SCN
:   SPP max SCN

<a id="c.BK_SPP_MIN_TX_BUFFER_SIZE"></a>

<a id="bk__dm__spp_8h_1a65cc40f856b15cdee103ecf81c6ae146"></a> BK\_SPP\_MIN\_TX\_BUFFER\_SIZE
:   SPP min tx buffer

<a id="c.BK_SPP_MAX_TX_BUFFER_SIZE"></a>

<a id="bk__dm__spp_8h_1a928e3a459f896865f2505fd221f9bf07"></a> BK\_SPP\_MAX\_TX\_BUFFER\_SIZE
:   SPP max tx buffer size

<a id="id29"></a>

### Type Definitions

<a id="_CPPv411bk_spp_cb_t"></a>

<a id="_CPPv311bk_spp_cb_t"></a> <a id="_CPPv211bk_spp_cb_t"></a> <a id="bk_spp_cb_t"></a> <a id="bk__dm__spp_8h_1a0ec1acc8d67bb396e3fec4636bc3d2e2"></a> typedef void (\*bk\_spp\_cb\_t)([bk\_spp\_cb\_event\_t](#_CPPv417bk_spp_cb_event_t "bk_spp_cb_event_t") event, [bk\_spp\_cb\_param\_t](#_CPPv417bk_spp_cb_param_t "bk_spp_cb_param_t") \*param)
:   SPP callback function type. When handle BK\_SPP\_DATA\_IND\_EVT, it is strongly recommended to cache incoming data, and process them in other lower priority application task rather than in this callback directly.

    Param event
    :   Event type

    Param param
    :   Point to callback parameter, currently is union type

<a id="id30"></a>

### Enumerations

<a id="_CPPv415bk_spp_status_t"></a>

<a id="_CPPv315bk_spp_status_t"></a> <a id="_CPPv215bk_spp_status_t"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1ec"></a> enum bk\_spp\_status\_t
:   *Values:*

    <a id="_CPPv4N15bk_spp_status_t14BK_SPP_SUCCESSE"></a>

    <a id="_CPPv3N15bk_spp_status_t14BK_SPP_SUCCESSE"></a> <a id="_CPPv2N15bk_spp_status_t14BK_SPP_SUCCESSE"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1ecadbd42204ffec5c4fe6f1b628acbe10a3"></a> enumerator BK\_SPP\_SUCCESS
    :   Successful operation.

    <a id="_CPPv4N15bk_spp_status_t14BK_SPP_FAILUREE"></a>

    <a id="_CPPv3N15bk_spp_status_t14BK_SPP_FAILUREE"></a> <a id="_CPPv2N15bk_spp_status_t14BK_SPP_FAILUREE"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1ecafc699a673f21977d4c0ecd1558b470a2"></a> enumerator BK\_SPP\_FAILURE
    :   Generic failure.

    <a id="_CPPv4N15bk_spp_status_t11BK_SPP_BUSYE"></a>

    <a id="_CPPv3N15bk_spp_status_t11BK_SPP_BUSYE"></a> <a id="_CPPv2N15bk_spp_status_t11BK_SPP_BUSYE"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1eca062136b35568517cf7446955e728dc47"></a> enumerator BK\_SPP\_BUSY
    :   Temporarily can not handle this request.

    <a id="_CPPv4N15bk_spp_status_t14BK_SPP_NO_DATAE"></a>

    <a id="_CPPv3N15bk_spp_status_t14BK_SPP_NO_DATAE"></a> <a id="_CPPv2N15bk_spp_status_t14BK_SPP_NO_DATAE"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1ecabff4ea50adfb4718c2819623f613c3ac"></a> enumerator BK\_SPP\_NO\_DATA
    :   No data

    <a id="_CPPv4N15bk_spp_status_t18BK_SPP_NO_RESOURCEE"></a>

    <a id="_CPPv3N15bk_spp_status_t18BK_SPP_NO_RESOURCEE"></a> <a id="_CPPv2N15bk_spp_status_t18BK_SPP_NO_RESOURCEE"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1ecab467c150afb33d6393d428dfac1f4f1d"></a> enumerator BK\_SPP\_NO\_RESOURCE
    :   No more resource

    <a id="_CPPv4N15bk_spp_status_t16BK_SPP_NEED_INITE"></a>

    <a id="_CPPv3N15bk_spp_status_t16BK_SPP_NEED_INITE"></a> <a id="_CPPv2N15bk_spp_status_t16BK_SPP_NEED_INITE"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1ecab1c8e812f1312599fa7f9228181c254d"></a> enumerator BK\_SPP\_NEED\_INIT
    :   SPP module shall init first

    <a id="_CPPv4N15bk_spp_status_t18BK_SPP_NEED_DEINITE"></a>

    <a id="_CPPv3N15bk_spp_status_t18BK_SPP_NEED_DEINITE"></a> <a id="_CPPv2N15bk_spp_status_t18BK_SPP_NEED_DEINITE"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1eca689b7626e952ef384478512c4565ccc0"></a> enumerator BK\_SPP\_NEED\_DEINIT
    :   SPP module shall deinit first

    <a id="_CPPv4N15bk_spp_status_t20BK_SPP_NO_CONNECTIONE"></a>

    <a id="_CPPv3N15bk_spp_status_t20BK_SPP_NO_CONNECTIONE"></a> <a id="_CPPv2N15bk_spp_status_t20BK_SPP_NO_CONNECTIONE"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1eca64fbabae475b2170add89ebf1c08b3d1"></a> enumerator BK\_SPP\_NO\_CONNECTION
    :   Connection may have been closed

    <a id="_CPPv4N15bk_spp_status_t16BK_SPP_NO_SERVERE"></a>

    <a id="_CPPv3N15bk_spp_status_t16BK_SPP_NO_SERVERE"></a> <a id="_CPPv2N15bk_spp_status_t16BK_SPP_NO_SERVERE"></a> <a id="bk__dm__spp_8h_1aad1d4a2559763053500818dacaffe1eca6547ef38d0002c4d37dd2926ebb28e51"></a> enumerator BK\_SPP\_NO\_SERVER
    :   No SPP server

<a id="_CPPv413bk_spp_role_t"></a>

<a id="_CPPv313bk_spp_role_t"></a> <a id="_CPPv213bk_spp_role_t"></a> <a id="bk__dm__spp_8h_1a98da9c0c3d07588a0a96a95453775506"></a> enum bk\_spp\_role\_t
:   *Values:*

    <a id="_CPPv4N13bk_spp_role_t18BK_SPP_ROLE_MASTERE"></a>

    <a id="_CPPv3N13bk_spp_role_t18BK_SPP_ROLE_MASTERE"></a> <a id="_CPPv2N13bk_spp_role_t18BK_SPP_ROLE_MASTERE"></a> <a id="bk__dm__spp_8h_1a98da9c0c3d07588a0a96a95453775506a98537ce4013096439bfa782714bce482"></a> enumerator BK\_SPP\_ROLE\_MASTER
    :   Role: master

    <a id="_CPPv4N13bk_spp_role_t17BK_SPP_ROLE_SLAVEE"></a>

    <a id="_CPPv3N13bk_spp_role_t17BK_SPP_ROLE_SLAVEE"></a> <a id="_CPPv2N13bk_spp_role_t17BK_SPP_ROLE_SLAVEE"></a> <a id="bk__dm__spp_8h_1a98da9c0c3d07588a0a96a95453775506aae7dc4cd9120901e04329428578ed7a4"></a> enumerator BK\_SPP\_ROLE\_SLAVE
    :   Role: slave

<a id="_CPPv417bk_spp_cb_event_t"></a>

<a id="_CPPv317bk_spp_cb_event_t"></a> <a id="_CPPv217bk_spp_cb_event_t"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884d"></a> enum bk\_spp\_cb\_event\_t
:   SPP callback function events.

    *Values:*

    <a id="_CPPv4N17bk_spp_cb_event_t15BK_SPP_INIT_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t15BK_SPP_INIT_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t15BK_SPP_INIT_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884da5e5f265dcc77d38592934b301eaf3ce1"></a> enumerator BK\_SPP\_INIT\_EVT
    :   When SPP is initialized, the event comes

    <a id="_CPPv4N17bk_spp_cb_event_t17BK_SPP_UNINIT_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t17BK_SPP_UNINIT_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t17BK_SPP_UNINIT_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884da5a7ae9ab1effa6d96f46948af68afec3"></a> enumerator BK\_SPP\_UNINIT\_EVT
    :   When SPP is deinitialized, the event comes

    <a id="_CPPv4N17bk_spp_cb_event_t25BK_SPP_DISCOVERY_COMP_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t25BK_SPP_DISCOVERY_COMP_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t25BK_SPP_DISCOVERY_COMP_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884dafb4b55c24ba9ccc510f5e7e468ef99c6"></a> enumerator BK\_SPP\_DISCOVERY\_COMP\_EVT
    :   When SDP discovery complete, the event comes

    <a id="_CPPv4N17bk_spp_cb_event_t15BK_SPP_OPEN_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t15BK_SPP_OPEN_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t15BK_SPP_OPEN_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884da307f299bf90500338d5131da5c807979"></a> enumerator BK\_SPP\_OPEN\_EVT
    :   When SPP Client connection open, the event comes

    <a id="_CPPv4N17bk_spp_cb_event_t16BK_SPP_CLOSE_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t16BK_SPP_CLOSE_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t16BK_SPP_CLOSE_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884da75935315fa70ffec071df09718aec848"></a> enumerator BK\_SPP\_CLOSE\_EVT
    :   When SPP connection closed, the event comes

    <a id="_CPPv4N17bk_spp_cb_event_t16BK_SPP_START_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t16BK_SPP_START_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t16BK_SPP_START_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884da8e0c88e53c982e68c7a1e52f49e42778"></a> enumerator BK\_SPP\_START\_EVT
    :   When SPP server started, the event comes

    <a id="_CPPv4N17bk_spp_cb_event_t18BK_SPP_CL_INIT_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t18BK_SPP_CL_INIT_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t18BK_SPP_CL_INIT_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884dad686f47ec5c151cb5c7a990eb4511341"></a> enumerator BK\_SPP\_CL\_INIT\_EVT
    :   When SPP client initiated a connection, the event comes

    <a id="_CPPv4N17bk_spp_cb_event_t19BK_SPP_DATA_IND_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t19BK_SPP_DATA_IND_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t19BK_SPP_DATA_IND_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884da0bcc22693919f23a6e0c93a4c0c0fd0d"></a> enumerator BK\_SPP\_DATA\_IND\_EVT
    :   When SPP connection received data, the event comes, only for BK\_SPP\_MODE\_CB

    <a id="_CPPv4N17bk_spp_cb_event_t16BK_SPP_WRITE_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t16BK_SPP_WRITE_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t16BK_SPP_WRITE_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884da9c2b575b100884fd626335712ef92870"></a> enumerator BK\_SPP\_WRITE\_EVT
    :   When SPP write operation completes, the event comes, only for BK\_SPP\_MODE\_CB

    <a id="_CPPv4N17bk_spp_cb_event_t19BK_SPP_SRV_OPEN_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t19BK_SPP_SRV_OPEN_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t19BK_SPP_SRV_OPEN_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884dae1a5e4f221809ce4b1d23cc1dedd0780"></a> enumerator BK\_SPP\_SRV\_OPEN\_EVT
    :   When SPP Server connection open, the event comes

    <a id="_CPPv4N17bk_spp_cb_event_t19BK_SPP_SRV_STOP_EVTE"></a>

    <a id="_CPPv3N17bk_spp_cb_event_t19BK_SPP_SRV_STOP_EVTE"></a> <a id="_CPPv2N17bk_spp_cb_event_t19BK_SPP_SRV_STOP_EVTE"></a> <a id="bk__dm__spp_8h_1a7aa13b1881d3faf735781da65d4f884da02175eb76ac896e30789ffab9008bac9"></a> enumerator BK\_SPP\_SRV\_STOP\_EVT
    :   When SPP server stopped, the event comes

<a id="id31"></a>

## API 类型定义

<a id="bk-dm-a2dp-types-h"></a>

## bk\_dm\_a2dp\_types.h

`bk_dm_a2dp_types.h` 定义 A2DP profile 使用的事件、状态和音频类型。

<a id="id32"></a>

### Header File

- [bk\_dm\_a2dp\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_a2dp_types.h)

<a id="id33"></a>

### Unions

<a id="_CPPv418bk_a2dp_cb_param_t"></a>

<a id="_CPPv318bk_a2dp_cb_param_t"></a> <a id="_CPPv218bk_a2dp_cb_param_t"></a> <a id="unionbk__a2dp__cb__param__t"></a> union bk\_a2dp\_cb\_param\_t
:   *#include \<bk\_dm\_a2dp\_types.h\>*

    A2DP state callback parameters.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18bk_a2dp_cb_param_t10conn_stateE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t10conn_stateE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t10conn_stateE"></a> <a id="bk_a2dp_cb_param_t::conn_state__bk_a2dp_cb_param_t::a2dp_conn_state_param"></a> <a id="unionbk__a2dp__cb__param__t_1a2ca275c55ef67723a32f6d64769307b4"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp\_conn\_state\_param](#_CPPv4N18bk_a2dp_cb_param_t21a2dp_conn_state_paramE "bk_a2dp_cb_param_t::a2dp_conn_state_param") conn\_state
    :   A2DP connection status

    <a id="_CPPv4N18bk_a2dp_cb_param_t11audio_stateE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t11audio_stateE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t11audio_stateE"></a> <a id="bk_a2dp_cb_param_t::audio_state__bk_a2dp_cb_param_t::a2dp_audio_state_param"></a> <a id="unionbk__a2dp__cb__param__t_1a6553aeabb23eb204dfbfab9ef3de0199"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp\_audio\_state\_param](#_CPPv4N18bk_a2dp_cb_param_t22a2dp_audio_state_paramE "bk_a2dp_cb_param_t::a2dp_audio_state_param") audio\_state
    :   audio stream playing state

    <a id="_CPPv4N18bk_a2dp_cb_param_t9audio_cfgE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t9audio_cfgE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t9audio_cfgE"></a> <a id="bk_a2dp_cb_param_t::audio_cfg__bk_a2dp_cb_param_t::a2dp_audio_cfg_param"></a> <a id="unionbk__a2dp__cb__param__t_1a47351683472833c6d9799652d490d706"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp\_audio\_cfg\_param](#_CPPv4N18bk_a2dp_cb_param_t20a2dp_audio_cfg_paramE "bk_a2dp_cb_param_t::a2dp_audio_cfg_param") audio\_cfg
    :   media codec configuration information

    <a id="_CPPv4N18bk_a2dp_cb_param_t16audio_source_cfgE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t16audio_source_cfgE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t16audio_source_cfgE"></a> <a id="bk_a2dp_cb_param_t::audio_source_cfg__bk_a2dp_cb_param_t::a2dp_audio_source_cfg_param"></a> <a id="unionbk__a2dp__cb__param__t_1af6e8646fefd6c22d67fd7c65e2de218b"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp\_audio\_source\_cfg\_param](#_CPPv4N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_paramE "bk_a2dp_cb_param_t::a2dp_audio_source_cfg_param") audio\_source\_cfg
    :   media codec configuration information

    <a id="_CPPv4N18bk_a2dp_cb_param_t15media_ctrl_statE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t15media_ctrl_statE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t15media_ctrl_statE"></a> <a id="bk_a2dp_cb_param_t::media_ctrl_stat__bk_a2dp_cb_param_t::media_ctrl_stat_param"></a> <a id="unionbk__a2dp__cb__param__t_1a637cf2373090b5c0247fd3c2892a446a"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[media\_ctrl\_stat\_param](#_CPPv4N18bk_a2dp_cb_param_t21media_ctrl_stat_paramE "bk_a2dp_cb_param_t::media_ctrl_stat_param") media\_ctrl\_stat
    :   status in acknowledgement to media control commands

    <a id="_CPPv4N18bk_a2dp_cb_param_t14a2dp_prof_statE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t14a2dp_prof_statE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t14a2dp_prof_statE"></a> <a id="bk_a2dp_cb_param_t::a2dp_prof_stat__bk_a2dp_cb_param_t::a2dp_prof_stat_param"></a> <a id="unionbk__a2dp__cb__param__t_1a193af12a0eb8eb01bb669ac84cc98aba"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp\_prof\_stat\_param](#_CPPv4N18bk_a2dp_cb_param_t20a2dp_prof_stat_paramE "bk_a2dp_cb_param_t::a2dp_prof_stat_param") a2dp\_prof\_stat
    :   status to indicate a2dp prof init or deinit

    <a id="_CPPv4N18bk_a2dp_cb_param_t25a2dp_set_delay_value_statE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t25a2dp_set_delay_value_statE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t25a2dp_set_delay_value_statE"></a> <a id="bk_a2dp_cb_param_t::a2dp_set_delay_value_stat__bk_a2dp_cb_param_t::a2dp_set_stat_param"></a> <a id="unionbk__a2dp__cb__param__t_1a2a696822a0511b6e01829706865bc875"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp\_set\_stat\_param](#_CPPv4N18bk_a2dp_cb_param_t19a2dp_set_stat_paramE "bk_a2dp_cb_param_t::a2dp_set_stat_param") a2dp\_set\_delay\_value\_stat
    :   A2DP sink set delay report value status

    <a id="_CPPv4N18bk_a2dp_cb_param_t25a2dp_get_delay_value_statE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t25a2dp_get_delay_value_statE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t25a2dp_get_delay_value_statE"></a> <a id="bk_a2dp_cb_param_t::a2dp_get_delay_value_stat__bk_a2dp_cb_param_t::a2dp_get_stat_param"></a> <a id="unionbk__a2dp__cb__param__t_1a58127a5539f9c37f0c15c199e61cbb9a"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp\_get\_stat\_param](#_CPPv4N18bk_a2dp_cb_param_t19a2dp_get_stat_paramE "bk_a2dp_cb_param_t::a2dp_get_stat_param") a2dp\_get\_delay\_value\_stat
    :   A2DP sink get delay report value status

    <a id="_CPPv4N18bk_a2dp_cb_param_t22a2dp_l2cap_connect_reqE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t22a2dp_l2cap_connect_reqE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t22a2dp_l2cap_connect_reqE"></a> <a id="bk_a2dp_cb_param_t::a2dp_l2cap_connect_req__bk_a2dp_cb_param_t::a2dp_l2cap_connect_req_param"></a> <a id="unionbk__a2dp__cb__param__t_1a73bd1b2b0d76c2c2e37fccfb99d5c8a9"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp\_l2cap\_connect\_req\_param](#_CPPv4N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_paramE "bk_a2dp_cb_param_t::a2dp_l2cap_connect_req_param") a2dp\_l2cap\_connect\_req

    <a id="_CPPv4N18bk_a2dp_cb_param_t22a2dp_set_cap_completedE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t22a2dp_set_cap_completedE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t22a2dp_set_cap_completedE"></a> <a id="bk_a2dp_cb_param_t::a2dp_set_cap_completed__bk_a2dp_cb_param_t::a2dp_set_cap_completed_param"></a> <a id="unionbk__a2dp__cb__param__t_1a4ea0a0d7ea80dcf429803384d4f9069b"></a> struct [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t")::[a2dp\_set\_cap\_completed\_param](#_CPPv4N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_paramE "bk_a2dp_cb_param_t::a2dp_set_cap_completed_param") a2dp\_set\_cap\_completed

    <a id="_CPPv4N18bk_a2dp_cb_param_t20a2dp_audio_cfg_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t20a2dp_audio_cfg_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t20a2dp_audio_cfg_paramE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_cfg_param"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__cfg__param"></a> struct a2dp\_audio\_cfg\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_AUDIO\_CFG\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t20a2dp_audio_cfg_param10remote_bdaE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t20a2dp_audio_cfg_param10remote_bdaE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t20a2dp_audio_cfg_param10remote_bdaE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_cfg_param::remote_bda__uint8_tA"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__cfg__param_1aa0c9625de8ba349940820e1be91c0cce"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

        <a id="_CPPv4N18bk_a2dp_cb_param_t20a2dp_audio_cfg_param3mccE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t20a2dp_audio_cfg_param3mccE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t20a2dp_audio_cfg_param3mccE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_cfg_param::mcc__bk_a2dp_mcc_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__cfg__param_1a1a646edf4611532b93d132cd2cbd53cf"></a> [bk\_a2dp\_mcc\_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t") mcc
        :   A2DP media codec capability information

    <a id="_CPPv4N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_paramE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_source_cfg_param"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__source__cfg__param"></a> struct a2dp\_audio\_source\_cfg\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_AUDIO\_SOURCE\_CFG\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_param10remote_bdaE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_param10remote_bdaE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_param10remote_bdaE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_source_cfg_param::remote_bda__uint8_tA"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__source__cfg__param_1a3928cdb23d078ac355385c0cb58dff5e"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

        <a id="_CPPv4N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_param3mtuE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_param3mtuE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_param3mtuE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_source_cfg_param::mtu__uint16_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__source__cfg__param_1a39527dc5bf6a842b889fb0491c13c85b"></a> uint16\_t mtu

        <a id="_CPPv4N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_param3mccE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_param3mccE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t27a2dp_audio_source_cfg_param3mccE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_source_cfg_param::mcc__bk_a2dp_mcc_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__source__cfg__param_1a36630858c8456d7e08c186e4163960b1"></a> [bk\_a2dp\_mcc\_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t") mcc
        :   max payload len, only used in source A2DP media codec capability information

    <a id="_CPPv4N18bk_a2dp_cb_param_t22a2dp_audio_state_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t22a2dp_audio_state_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t22a2dp_audio_state_paramE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_state_param"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__state__param"></a> struct a2dp\_audio\_state\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_AUDIO\_STATE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t22a2dp_audio_state_param5stateE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t22a2dp_audio_state_param5stateE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t22a2dp_audio_state_param5stateE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_state_param::state__bk_a2dp_audio_state_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__state__param_1a7ab7aafdd602e75670bf9f0ef57a14df"></a> [bk\_a2dp\_audio\_state\_t](#_CPPv421bk_a2dp_audio_state_t "bk_a2dp_audio_state_t") state
        :   one of the values from bk\_a2dp\_audio\_state\_t

        <a id="_CPPv4N18bk_a2dp_cb_param_t22a2dp_audio_state_param10remote_bdaE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t22a2dp_audio_state_param10remote_bdaE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t22a2dp_audio_state_param10remote_bdaE"></a> <a id="bk_a2dp_cb_param_t::a2dp_audio_state_param::remote_bda__uint8_tA"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__audio__state__param_1a8be843fa2c8a4c0bc15dd52dd863f1e3"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

    <a id="_CPPv4N18bk_a2dp_cb_param_t21a2dp_conn_state_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t21a2dp_conn_state_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t21a2dp_conn_state_paramE"></a> <a id="bk_a2dp_cb_param_t::a2dp_conn_state_param"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__conn__state__param"></a> struct a2dp\_conn\_state\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_CONNECTION\_STATE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t21a2dp_conn_state_param5stateE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t21a2dp_conn_state_param5stateE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t21a2dp_conn_state_param5stateE"></a> <a id="bk_a2dp_cb_param_t::a2dp_conn_state_param::state__bk_a2dp_connection_state_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__conn__state__param_1aa4846a9dc530ecdf62dac92c79983a78"></a> [bk\_a2dp\_connection\_state\_t](#_CPPv426bk_a2dp_connection_state_t "bk_a2dp_connection_state_t") state
        :   one of values from bk\_a2dp\_connection\_state\_t

        <a id="_CPPv4N18bk_a2dp_cb_param_t21a2dp_conn_state_param10remote_bdaE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t21a2dp_conn_state_param10remote_bdaE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t21a2dp_conn_state_param10remote_bdaE"></a> <a id="bk_a2dp_cb_param_t::a2dp_conn_state_param::remote_bda__uint8_tA"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__conn__state__param_1a70409b003ec97252a423100a1faad791"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

        <a id="_CPPv4N18bk_a2dp_cb_param_t21a2dp_conn_state_param8disc_rsnE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t21a2dp_conn_state_param8disc_rsnE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t21a2dp_conn_state_param8disc_rsnE"></a> <a id="bk_a2dp_cb_param_t::a2dp_conn_state_param::disc_rsn__bk_a2dp_disc_rsn_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__conn__state__param_1a301a64c4c1e86c2d1e638147eba2f909"></a> [bk\_a2dp\_disc\_rsn\_t](#_CPPv418bk_a2dp_disc_rsn_t "bk_a2dp_disc_rsn_t") disc\_rsn
        :   reason of disconnection for “DISCONNECTED”

    <a id="_CPPv4N18bk_a2dp_cb_param_t19a2dp_get_stat_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t19a2dp_get_stat_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t19a2dp_get_stat_paramE"></a> <a id="bk_a2dp_cb_param_t::a2dp_get_stat_param"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__get__stat__param"></a> struct a2dp\_get\_stat\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_SNK\_GET\_DELAY\_VALUE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t19a2dp_get_stat_param11delay_valueE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t19a2dp_get_stat_param11delay_valueE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t19a2dp_get_stat_param11delay_valueE"></a> <a id="bk_a2dp_cb_param_t::a2dp_get_stat_param::delay_value__uint16_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__get__stat__param_1ae60e5532b13fb3dc5194eba27c421d3a"></a> uint16\_t delay\_value
        :   delay report value

    <a id="_CPPv4N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_paramE"></a> <a id="bk_a2dp_cb_param_t::a2dp_l2cap_connect_req_param"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__l2cap__connect__req__param"></a> struct a2dp\_l2cap\_connect\_req\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_L2CAP\_CONNECT\_REQ\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_param10remote_bdaE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_param10remote_bdaE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_param10remote_bdaE"></a> <a id="bk_a2dp_cb_param_t::a2dp_l2cap_connect_req_param::remote_bda__uint8_tA"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__l2cap__connect__req__param_1af8a9078358a7045e7040f9c9bbcba3c2"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

        <a id="_CPPv4N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_param6acceptE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_param6acceptE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t28a2dp_l2cap_connect_req_param6acceptE"></a> <a id="bk_a2dp_cb_param_t::a2dp_l2cap_connect_req_param::accept__uint8_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__l2cap__connect__req__param_1a4a0c7e37f227cdfe8153b8f0f3ada374"></a> uint8\_t accept

    <a id="_CPPv4N18bk_a2dp_cb_param_t20a2dp_prof_stat_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t20a2dp_prof_stat_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t20a2dp_prof_stat_paramE"></a> <a id="bk_a2dp_cb_param_t::a2dp_prof_stat_param"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__prof__stat__param"></a> struct a2dp\_prof\_stat\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_PROF\_STATE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t20a2dp_prof_stat_param6actionE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t20a2dp_prof_stat_param6actionE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t20a2dp_prof_stat_param6actionE"></a> <a id="bk_a2dp_cb_param_t::a2dp_prof_stat_param::action__uint8_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__prof__stat__param_1a589768b4f25ca45f52a9541d23a59bdb"></a> uint8\_t action

        <a id="_CPPv4N18bk_a2dp_cb_param_t20a2dp_prof_stat_param4roleE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t20a2dp_prof_stat_param4roleE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t20a2dp_prof_stat_param4roleE"></a> <a id="bk_a2dp_cb_param_t::a2dp_prof_stat_param::role__uint8_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__prof__stat__param_1aa9f74d670b156f51853addd723588378"></a> uint8\_t role
        :   0 means init, 1 means deinit

        <a id="_CPPv4N18bk_a2dp_cb_param_t20a2dp_prof_stat_param6statusE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t20a2dp_prof_stat_param6statusE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t20a2dp_prof_stat_param6statusE"></a> <a id="bk_a2dp_cb_param_t::a2dp_prof_stat_param::status__uint8_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__prof__stat__param_1ab6227150d95821436e41fd904d3cb114"></a> uint8\_t status
        :   0 means source, 1 means sink

        <a id="_CPPv4N18bk_a2dp_cb_param_t20a2dp_prof_stat_param6reasonE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t20a2dp_prof_stat_param6reasonE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t20a2dp_prof_stat_param6reasonE"></a> <a id="bk_a2dp_cb_param_t::a2dp_prof_stat_param::reason__uint8_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__prof__stat__param_1a7cc4ab38c4e7844dd66dccd5e4e4a0b8"></a> uint8\_t reason
        :   0 means success, other means fail

    <a id="_CPPv4N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_paramE"></a> <a id="bk_a2dp_cb_param_t::a2dp_set_cap_completed_param"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__set__cap__completed__param"></a> struct a2dp\_set\_cap\_completed\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_SET\_CAP\_COMPLETED\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_param6statusE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_param6statusE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_param6statusE"></a> <a id="bk_a2dp_cb_param_t::a2dp_set_cap_completed_param::status__uint8_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__set__cap__completed__param_1a4d9d532f38f7683fd867fd902ef1607a"></a> uint8\_t status

        <a id="_CPPv4N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_param4roleE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_param4roleE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t28a2dp_set_cap_completed_param4roleE"></a> <a id="bk_a2dp_cb_param_t::a2dp_set_cap_completed_param::role__uint8_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__set__cap__completed__param_1a682082da0c6c16415b2b28f6ccd9950f"></a> uint8\_t role

    <a id="_CPPv4N18bk_a2dp_cb_param_t19a2dp_set_stat_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t19a2dp_set_stat_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t19a2dp_set_stat_paramE"></a> <a id="bk_a2dp_cb_param_t::a2dp_set_stat_param"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__set__stat__param"></a> struct a2dp\_set\_stat\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_SNK\_SET\_DELAY\_VALUE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t19a2dp_set_stat_param9set_stateE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t19a2dp_set_stat_param9set_stateE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t19a2dp_set_stat_param9set_stateE"></a> <a id="bk_a2dp_cb_param_t::a2dp_set_stat_param::set_state__bk_a2dp_set_delay_value_state_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__set__stat__param_1ada1ef026d8aa1b4a7ec19153699f32f9"></a> [bk\_a2dp\_set\_delay\_value\_state\_t](#_CPPv431bk_a2dp_set_delay_value_state_t "bk_a2dp_set_delay_value_state_t") set\_state
        :   a2dp profile state param

        <a id="_CPPv4N18bk_a2dp_cb_param_t19a2dp_set_stat_param11delay_valueE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t19a2dp_set_stat_param11delay_valueE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t19a2dp_set_stat_param11delay_valueE"></a> <a id="bk_a2dp_cb_param_t::a2dp_set_stat_param::delay_value__uint16_t"></a> <a id="structbk__a2dp__cb__param__t_1_1a2dp__set__stat__param_1a2fef41f6a7e310d7e3fd65854d8cdbd8"></a> uint16\_t delay\_value
        :   delay report value

    <a id="_CPPv4N18bk_a2dp_cb_param_t21media_ctrl_stat_paramE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_param_t21media_ctrl_stat_paramE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t21media_ctrl_stat_paramE"></a> <a id="bk_a2dp_cb_param_t::media_ctrl_stat_param"></a> <a id="structbk__a2dp__cb__param__t_1_1media__ctrl__stat__param"></a> struct media\_ctrl\_stat\_param
    :   *#include \<bk\_dm\_a2dp\_types.h\>*

        BK\_A2DP\_MEDIA\_CTRL\_ACK\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N18bk_a2dp_cb_param_t21media_ctrl_stat_param3cmdE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t21media_ctrl_stat_param3cmdE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t21media_ctrl_stat_param3cmdE"></a> <a id="bk_a2dp_cb_param_t::media_ctrl_stat_param::cmd__bk_a2dp_media_ctrl_t"></a> <a id="structbk__a2dp__cb__param__t_1_1media__ctrl__stat__param_1aa40fe9dd970abc312d14342444198469"></a> [bk\_a2dp\_media\_ctrl\_t](#_CPPv420bk_a2dp_media_ctrl_t "bk_a2dp_media_ctrl_t") cmd
        :   media control commands to acknowledge

        <a id="_CPPv4N18bk_a2dp_cb_param_t21media_ctrl_stat_param6statusE"></a>

        <a id="_CPPv3N18bk_a2dp_cb_param_t21media_ctrl_stat_param6statusE"></a> <a id="_CPPv2N18bk_a2dp_cb_param_t21media_ctrl_stat_param6statusE"></a> <a id="bk_a2dp_cb_param_t::media_ctrl_stat_param::status__bk_a2dp_media_ctrl_ack_t"></a> <a id="structbk__a2dp__cb__param__t_1_1media__ctrl__stat__param_1ad4620896fc5657cc36b81f3dd2305863"></a> [bk\_a2dp\_media\_ctrl\_ack\_t](#_CPPv424bk_a2dp_media_ctrl_ack_t "bk_a2dp_media_ctrl_ack_t") status
        :   acknowledgement to media control commands

<a id="id34"></a>

### Structures

<a id="_CPPv419bk_a2dp_codec_cap_t"></a>

<a id="_CPPv319bk_a2dp_codec_cap_t"></a> <a id="_CPPv219bk_a2dp_codec_cap_t"></a> <a id="bk_a2dp_codec_cap_t"></a> <a id="structbk__a2dp__codec__cap__t"></a> struct bk\_a2dp\_codec\_cap\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_a2dp_codec_cap_t12bit_pool_maxE"></a>

    <a id="_CPPv3N19bk_a2dp_codec_cap_t12bit_pool_maxE"></a> <a id="_CPPv2N19bk_a2dp_codec_cap_t12bit_pool_maxE"></a> <a id="bk_a2dp_codec_cap_t::bit_pool_max__uint8_t"></a> <a id="structbk__a2dp__codec__cap__t_1af10e28c106d06a29166dc4577f86dd00"></a> uint8\_t bit\_pool\_max
    :   must \>\= 2

<a id="_CPPv413bk_a2dp_mcc_t"></a>

<a id="_CPPv313bk_a2dp_mcc_t"></a> <a id="_CPPv213bk_a2dp_mcc_t"></a> <a id="bk_a2dp_mcc_t"></a> <a id="structbk__a2dp__mcc__t"></a> struct bk\_a2dp\_mcc\_t
:   A2DP media codec capabilities union.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13bk_a2dp_mcc_t4typeE"></a>

    <a id="_CPPv3N13bk_a2dp_mcc_t4typeE"></a> <a id="_CPPv2N13bk_a2dp_mcc_t4typeE"></a> <a id="bk_a2dp_mcc_t::type__uint8_t"></a> <a id="structbk__a2dp__mcc__t_1a9406441c4b52916460ad405d08591466"></a> uint8\_t type
    :   A2DP media codec type

    <a id="_CPPv4N13bk_a2dp_mcc_t9sbc_codecE"></a>

    <a id="_CPPv3N13bk_a2dp_mcc_t9sbc_codecE"></a> <a id="_CPPv2N13bk_a2dp_mcc_t9sbc_codecE"></a> <a id="structbk__a2dp__mcc__t_1a72f94adf7b23bfa4804db426958612ea"></a> struct [bk\_a2dp\_mcc\_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t")::\[anonymous\]::\[anonymous\] sbc\_codec
    :   SBC codec capabilities.

    <a id="_CPPv4N13bk_a2dp_mcc_t9aac_codecE"></a>

    <a id="_CPPv3N13bk_a2dp_mcc_t9aac_codecE"></a> <a id="_CPPv2N13bk_a2dp_mcc_t9aac_codecE"></a> <a id="structbk__a2dp__mcc__t_1a19c194c612bd4e30ecb3bd3da8e2731a"></a> struct [bk\_a2dp\_mcc\_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t")::\[anonymous\]::\[anonymous\] aac\_codec
    :   MPEG-2, 4 AAC codec capabilities.

    <a id="_CPPv4N13bk_a2dp_mcc_t3cieE"></a>

    <a id="_CPPv3N13bk_a2dp_mcc_t3cieE"></a> <a id="_CPPv2N13bk_a2dp_mcc_t3cieE"></a> <a id="structbk__a2dp__mcc__t_1a93a60771bd8fbfd2f68dcebf945454b2"></a> union [bk\_a2dp\_mcc\_t](#_CPPv413bk_a2dp_mcc_t "bk_a2dp_mcc_t")::\[anonymous\] cie
    :   A2DP codec information element

<a id="id35"></a>

### Type Definitions

<a id="_CPPv415bk_bt_a2dp_cb_t"></a>

<a id="_CPPv315bk_bt_a2dp_cb_t"></a> <a id="_CPPv215bk_bt_a2dp_cb_t"></a> <a id="bk_bt_a2dp_cb_t"></a> <a id="bk__dm__a2dp__types_8h_1abb6be2aa6fcd7c2254f5811598207c0b"></a> typedef void (\*bk\_bt\_a2dp\_cb\_t)([bk\_a2dp\_cb\_event\_t](#_CPPv418bk_a2dp_cb_event_t "bk_a2dp_cb_event_t") event, [bk\_a2dp\_cb\_param\_t](#_CPPv418bk_a2dp_cb_param_t "bk_a2dp_cb_param_t") \*param)
:   A2DP profile callback function type.

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter

<a id="_CPPv420bk_bt_sink_data_cb_t"></a>

<a id="_CPPv320bk_bt_sink_data_cb_t"></a> <a id="_CPPv220bk_bt_sink_data_cb_t"></a> <a id="bk_bt_sink_data_cb_t"></a> <a id="bk__dm__a2dp__types_8h_1af81ac94ef3391f28a2e9dcbb4a95d690"></a> typedef void (\*bk\_bt\_sink\_data\_cb\_t)(const uint8\_t \*buf, uint16\_t len)
:   A2DP sink data callback function.

    Param buf
    :   **\[in\]** : pointer to the data received from A2DP source device

    Param len
    :   **\[in\]** : size(in bytes) in buf

<a id="_CPPv424bk_a2dp_source_data_cb_t"></a>

<a id="_CPPv324bk_a2dp_source_data_cb_t"></a> <a id="_CPPv224bk_a2dp_source_data_cb_t"></a> <a id="bk_a2dp_source_data_cb_t"></a> <a id="bk__dm__a2dp__types_8h_1a41eb27b2409e7ede5fb379b1fd5279f6"></a> typedef int32\_t (\*bk\_a2dp\_source\_data\_cb\_t)(uint8\_t \*buf, int32\_t len)
:   A2DP source data read callback function.

    Param buf
    :   **\[in\]** : buffer to be filled with PCM data stream from higher layer

    Param len
    :   **\[in\]** : size(in bytes) of data block to be copied to buf. -1 is an indication to user that data buffer shall be flushed

    Return
    :   size of bytes read successfully, if the argument len is -1, this value is ignored.

<a id="_CPPv432bk_a2dp_source_pcm_resample_cb_t"></a>

<a id="_CPPv332bk_a2dp_source_pcm_resample_cb_t"></a> <a id="_CPPv232bk_a2dp_source_pcm_resample_cb_t"></a> <a id="bk_a2dp_source_pcm_resample_cb_t"></a> <a id="bk__dm__a2dp__types_8h_1aef015ad707803577a9aab7ec4c494bd2"></a> typedef int32\_t (\*bk\_a2dp\_source\_pcm\_resample\_cb\_t)(uint8\_t \*in\_addr, uint32\_t \*in\_len, uint8\_t \*out\_addr, uint32\_t \*out\_len)
:   pcm resample callback function

    Param in\_addr
    :   **\[in\]** : input buff before resample (in bytes).

    Param \[in\|out\]
    :   in\_len : input buff len (in bytes). When call done, it should change to how many bytes had processed.

    Param out\_addr
    :   **\[in\]** : input buff after resample (in bytes).

    Param \[in\|out\]
    :   out\_len : out buff len (in bytes). When call done, it should change to how many bytes had outputed.

    Return
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail, bluetooth will ignore the data.

<a id="_CPPv430bk_a2dp_source_pcm_encode_cb_t"></a>

<a id="_CPPv330bk_a2dp_source_pcm_encode_cb_t"></a> <a id="_CPPv230bk_a2dp_source_pcm_encode_cb_t"></a> <a id="bk_a2dp_source_pcm_encode_cb_t"></a> <a id="bk__dm__a2dp__types_8h_1acb345b4b67894286a8bfb0aaad30a073"></a> typedef int32\_t (\*bk\_a2dp\_source\_pcm\_encode\_cb\_t)(uint8\_t type, uint8\_t \*in\_addr, uint32\_t \*in\_len, uint8\_t \*out\_addr, uint32\_t \*out\_len)
:   pcm encode callback function

    Param type
    :   **\[in\]** : encode type, 0 means sbc.

    Param in\_addr
    :   **\[in\]** : input buff before encode (in bytes).

    Param \[in\|out\]
    :   in\_len : input buff len (in bytes). When call done, it should change to how many bytes had processed.

    Param out\_addr
    :   **\[in\]** : input buff after encode (in bytes).

    Param \[in\|out\]
    :   out\_len : out buff len (in bytes). When call done, it should change to how many bytes had outputed.

    Return
    :   - BK\_ERR\_BT\_SUCCESS: success
        - others: fail, bluetooth will ignore the data.

<a id="id36"></a>

### Enumerations

<a id="_CPPv418bk_a2dp_cb_event_t"></a>

<a id="_CPPv318bk_a2dp_cb_event_t"></a> <a id="_CPPv218bk_a2dp_cb_event_t"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5"></a> enum bk\_a2dp\_cb\_event\_t
:   A2DP callback events.

    *Values:*

    <a id="_CPPv4N18bk_a2dp_cb_event_t28BK_A2DP_CONNECTION_STATE_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t28BK_A2DP_CONNECTION_STATE_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t28BK_A2DP_CONNECTION_STATE_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5a7a1d3d85c10a4f9d30dfd041c75bcfb6"></a> enumerator BK\_A2DP\_CONNECTION\_STATE\_EVT
    :   connection state changed event

    <a id="_CPPv4N18bk_a2dp_cb_event_t23BK_A2DP_AUDIO_STATE_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t23BK_A2DP_AUDIO_STATE_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t23BK_A2DP_AUDIO_STATE_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5af6523df086d14460fba99ab956af78e1"></a> enumerator BK\_A2DP\_AUDIO\_STATE\_EVT
    :   audio stream transmission state changed event

    <a id="_CPPv4N18bk_a2dp_cb_event_t21BK_A2DP_AUDIO_CFG_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t21BK_A2DP_AUDIO_CFG_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t21BK_A2DP_AUDIO_CFG_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5adc22beb367229db519c745378fb54620"></a> enumerator BK\_A2DP\_AUDIO\_CFG\_EVT
    :   audio codec is configured, only used for A2DP SINK

    <a id="_CPPv4N18bk_a2dp_cb_event_t28BK_A2DP_AUDIO_SOURCE_CFG_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t28BK_A2DP_AUDIO_SOURCE_CFG_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t28BK_A2DP_AUDIO_SOURCE_CFG_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5ae02351051f042929063dab02f5927495"></a> enumerator BK\_A2DP\_AUDIO\_SOURCE\_CFG\_EVT
    :   audio codec is configured, only used for A2DP SOURCE

    <a id="_CPPv4N18bk_a2dp_cb_event_t26BK_A2DP_MEDIA_CTRL_ACK_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t26BK_A2DP_MEDIA_CTRL_ACK_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t26BK_A2DP_MEDIA_CTRL_ACK_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5a8f35111267997d402d56ba262d6ec253"></a> enumerator BK\_A2DP\_MEDIA\_CTRL\_ACK\_EVT
    :   acknowledge event in response to media control commands

    <a id="_CPPv4N18bk_a2dp_cb_event_t22BK_A2DP_PROF_STATE_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t22BK_A2DP_PROF_STATE_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t22BK_A2DP_PROF_STATE_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5ababfdc43688fbff3df37da5092fe681e"></a> enumerator BK\_A2DP\_PROF\_STATE\_EVT
    :   indicate a2dp init\&deinit complete

    <a id="_CPPv4N18bk_a2dp_cb_event_t31BK_A2DP_SNK_SET_DELAY_VALUE_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t31BK_A2DP_SNK_SET_DELAY_VALUE_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t31BK_A2DP_SNK_SET_DELAY_VALUE_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5ad7f969838fed3335cb5f9dfecf947469"></a> enumerator BK\_A2DP\_SNK\_SET\_DELAY\_VALUE\_EVT
    :   indicate a2dp sink set delay report value complete, only used for A2DP SINK

    <a id="_CPPv4N18bk_a2dp_cb_event_t31BK_A2DP_SNK_GET_DELAY_VALUE_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t31BK_A2DP_SNK_GET_DELAY_VALUE_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t31BK_A2DP_SNK_GET_DELAY_VALUE_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5acb66987a3f9de76bb419f890e247d137"></a> enumerator BK\_A2DP\_SNK\_GET\_DELAY\_VALUE\_EVT
    :   indicate a2dp sink get delay report value complete, only used for A2DP SINK

    <a id="_CPPv4N18bk_a2dp_cb_event_t29BK_A2DP_L2CAP_CONNECT_REQ_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t29BK_A2DP_L2CAP_CONNECT_REQ_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t29BK_A2DP_L2CAP_CONNECT_REQ_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5a8ce765de7207e01122a269b62bf01275"></a> enumerator BK\_A2DP\_L2CAP\_CONNECT\_REQ\_EVT

    <a id="_CPPv4N18bk_a2dp_cb_event_t29BK_A2DP_SET_CAP_COMPLETED_EVTE"></a>

    <a id="_CPPv3N18bk_a2dp_cb_event_t29BK_A2DP_SET_CAP_COMPLETED_EVTE"></a> <a id="_CPPv2N18bk_a2dp_cb_event_t29BK_A2DP_SET_CAP_COMPLETED_EVTE"></a> <a id="bk__dm__a2dp__types_8h_1aad6d91713de35db7ded8c9ae80d6ece5af6af5b3b9905800e4850d786afae1e20"></a> enumerator BK\_A2DP\_SET\_CAP\_COMPLETED\_EVT

<a id="_CPPv426bk_a2dp_connection_state_t"></a>

<a id="_CPPv326bk_a2dp_connection_state_t"></a> <a id="_CPPv226bk_a2dp_connection_state_t"></a> <a id="bk__dm__a2dp__types_8h_1a07aa05dfec96703c88d5b46f90c85e02"></a> enum bk\_a2dp\_connection\_state\_t
:   Bluetooth A2DP connection states.

    *Values:*

    <a id="_CPPv4N26bk_a2dp_connection_state_t37BK_A2DP_CONNECTION_STATE_DISCONNECTEDE"></a>

    <a id="_CPPv3N26bk_a2dp_connection_state_t37BK_A2DP_CONNECTION_STATE_DISCONNECTEDE"></a> <a id="_CPPv2N26bk_a2dp_connection_state_t37BK_A2DP_CONNECTION_STATE_DISCONNECTEDE"></a> <a id="bk__dm__a2dp__types_8h_1a07aa05dfec96703c88d5b46f90c85e02a0f84e234849ba7263315fb0ad354863e"></a> enumerator BK\_A2DP\_CONNECTION\_STATE\_DISCONNECTED
    :   connection released

    <a id="_CPPv4N26bk_a2dp_connection_state_t35BK_A2DP_CONNECTION_STATE_CONNECTINGE"></a>

    <a id="_CPPv3N26bk_a2dp_connection_state_t35BK_A2DP_CONNECTION_STATE_CONNECTINGE"></a> <a id="_CPPv2N26bk_a2dp_connection_state_t35BK_A2DP_CONNECTION_STATE_CONNECTINGE"></a> <a id="bk__dm__a2dp__types_8h_1a07aa05dfec96703c88d5b46f90c85e02a3eb1763d554e2ff3cca384ef8ad3e394"></a> enumerator BK\_A2DP\_CONNECTION\_STATE\_CONNECTING
    :   connecting remote device

    <a id="_CPPv4N26bk_a2dp_connection_state_t34BK_A2DP_CONNECTION_STATE_CONNECTEDE"></a>

    <a id="_CPPv3N26bk_a2dp_connection_state_t34BK_A2DP_CONNECTION_STATE_CONNECTEDE"></a> <a id="_CPPv2N26bk_a2dp_connection_state_t34BK_A2DP_CONNECTION_STATE_CONNECTEDE"></a> <a id="bk__dm__a2dp__types_8h_1a07aa05dfec96703c88d5b46f90c85e02a85653f02b0ba148acc4079adb870ea41"></a> enumerator BK\_A2DP\_CONNECTION\_STATE\_CONNECTED
    :   connection established

    <a id="_CPPv4N26bk_a2dp_connection_state_t38BK_A2DP_CONNECTION_STATE_DISCONNECTINGE"></a>

    <a id="_CPPv3N26bk_a2dp_connection_state_t38BK_A2DP_CONNECTION_STATE_DISCONNECTINGE"></a> <a id="_CPPv2N26bk_a2dp_connection_state_t38BK_A2DP_CONNECTION_STATE_DISCONNECTINGE"></a> <a id="bk__dm__a2dp__types_8h_1a07aa05dfec96703c88d5b46f90c85e02a5c735cf637c42e198faca3974dfb04fd"></a> enumerator BK\_A2DP\_CONNECTION\_STATE\_DISCONNECTING
    :   disconnecting remote device

<a id="_CPPv418bk_a2dp_disc_rsn_t"></a>

<a id="_CPPv318bk_a2dp_disc_rsn_t"></a> <a id="_CPPv218bk_a2dp_disc_rsn_t"></a> <a id="bk__dm__a2dp__types_8h_1a2b167fd4415b0e4ab99fad3586c06410"></a> enum bk\_a2dp\_disc\_rsn\_t
:   Bluetooth A2DP disconnection reason.

    *Values:*

    <a id="_CPPv4N18bk_a2dp_disc_rsn_t23BK_A2DP_DISC_RSN_NORMALE"></a>

    <a id="_CPPv3N18bk_a2dp_disc_rsn_t23BK_A2DP_DISC_RSN_NORMALE"></a> <a id="_CPPv2N18bk_a2dp_disc_rsn_t23BK_A2DP_DISC_RSN_NORMALE"></a> <a id="bk__dm__a2dp__types_8h_1a2b167fd4415b0e4ab99fad3586c06410abeaca5cdf4537dca09f7d7a6bee703b7"></a> enumerator BK\_A2DP\_DISC\_RSN\_NORMAL
    :   Finished disconnection that is initiated by local or remote device

    <a id="_CPPv4N18bk_a2dp_disc_rsn_t25BK_A2DP_DISC_RSN_ABNORMALE"></a>

    <a id="_CPPv3N18bk_a2dp_disc_rsn_t25BK_A2DP_DISC_RSN_ABNORMALE"></a> <a id="_CPPv2N18bk_a2dp_disc_rsn_t25BK_A2DP_DISC_RSN_ABNORMALE"></a> <a id="bk__dm__a2dp__types_8h_1a2b167fd4415b0e4ab99fad3586c06410a51cb601a97f5dd44da47cfd6c3cb10a0"></a> enumerator BK\_A2DP\_DISC\_RSN\_ABNORMAL
    :   Abnormal disconnection caused by signal loss

<a id="_CPPv421bk_a2dp_audio_state_t"></a>

<a id="_CPPv321bk_a2dp_audio_state_t"></a> <a id="_CPPv221bk_a2dp_audio_state_t"></a> <a id="bk__dm__a2dp__types_8h_1a9b80ac80a02e3dfcd5c339fb6e84e9f8"></a> enum bk\_a2dp\_audio\_state\_t
:   Bluetooth A2DP datapath states.

    *Values:*

    <a id="_CPPv4N21bk_a2dp_audio_state_t27BK_A2DP_AUDIO_STATE_SUSPENDE"></a>

    <a id="_CPPv3N21bk_a2dp_audio_state_t27BK_A2DP_AUDIO_STATE_SUSPENDE"></a> <a id="_CPPv2N21bk_a2dp_audio_state_t27BK_A2DP_AUDIO_STATE_SUSPENDE"></a> <a id="bk__dm__a2dp__types_8h_1a9b80ac80a02e3dfcd5c339fb6e84e9f8adb948f8e8c46906aeb09f8fc6b4d1fba"></a> enumerator BK\_A2DP\_AUDIO\_STATE\_SUSPEND
    :   audio stream datapath suspend

    <a id="_CPPv4N21bk_a2dp_audio_state_t27BK_A2DP_AUDIO_STATE_STARTEDE"></a>

    <a id="_CPPv3N21bk_a2dp_audio_state_t27BK_A2DP_AUDIO_STATE_STARTEDE"></a> <a id="_CPPv2N21bk_a2dp_audio_state_t27BK_A2DP_AUDIO_STATE_STARTEDE"></a> <a id="bk__dm__a2dp__types_8h_1a9b80ac80a02e3dfcd5c339fb6e84e9f8ad92853a9eb4330bbd809c1d8538ede7d"></a> enumerator BK\_A2DP\_AUDIO\_STATE\_STARTED
    :   audio stream datapath started

<a id="_CPPv420bk_a2dp_media_ctrl_t"></a>

<a id="_CPPv320bk_a2dp_media_ctrl_t"></a> <a id="_CPPv220bk_a2dp_media_ctrl_t"></a> <a id="bk__dm__a2dp__types_8h_1a026216b39590cf9e5ad2fa2fca7efba0"></a> enum bk\_a2dp\_media\_ctrl\_t
:   A2DP media control commands.

    *Values:*

    <a id="_CPPv4N20bk_a2dp_media_ctrl_t24BK_A2DP_MEDIA_CTRL_STARTE"></a>

    <a id="_CPPv3N20bk_a2dp_media_ctrl_t24BK_A2DP_MEDIA_CTRL_STARTE"></a> <a id="_CPPv2N20bk_a2dp_media_ctrl_t24BK_A2DP_MEDIA_CTRL_STARTE"></a> <a id="bk__dm__a2dp__types_8h_1a026216b39590cf9e5ad2fa2fca7efba0aae8b47cb2a00913e68839b6625c2aacb"></a> enumerator BK\_A2DP\_MEDIA\_CTRL\_START
    :   command to set up media transmission channel

    <a id="_CPPv4N20bk_a2dp_media_ctrl_t26BK_A2DP_MEDIA_CTRL_SUSPENDE"></a>

    <a id="_CPPv3N20bk_a2dp_media_ctrl_t26BK_A2DP_MEDIA_CTRL_SUSPENDE"></a> <a id="_CPPv2N20bk_a2dp_media_ctrl_t26BK_A2DP_MEDIA_CTRL_SUSPENDE"></a> <a id="bk__dm__a2dp__types_8h_1a026216b39590cf9e5ad2fa2fca7efba0abdce24104465a27adde46d8839e3b9ff"></a> enumerator BK\_A2DP\_MEDIA\_CTRL\_SUSPEND
    :   command to suspend media transmission

<a id="_CPPv424bk_a2dp_media_ctrl_ack_t"></a>

<a id="_CPPv324bk_a2dp_media_ctrl_ack_t"></a> <a id="_CPPv224bk_a2dp_media_ctrl_ack_t"></a> <a id="bk__dm__a2dp__types_8h_1a0db96c8b62acb8620c8aa31451dd0b37"></a> enum bk\_a2dp\_media\_ctrl\_ack\_t
:   A2DP media control command acknowledgement code.

    *Values:*

    <a id="_CPPv4N24bk_a2dp_media_ctrl_ack_t30BK_A2DP_MEDIA_CTRL_ACK_SUCCESSE"></a>

    <a id="_CPPv3N24bk_a2dp_media_ctrl_ack_t30BK_A2DP_MEDIA_CTRL_ACK_SUCCESSE"></a> <a id="_CPPv2N24bk_a2dp_media_ctrl_ack_t30BK_A2DP_MEDIA_CTRL_ACK_SUCCESSE"></a> <a id="bk__dm__a2dp__types_8h_1a0db96c8b62acb8620c8aa31451dd0b37a08729e376878395daedcc4de3b68afbb"></a> enumerator BK\_A2DP\_MEDIA\_CTRL\_ACK\_SUCCESS
    :   media control command is acknowledged with success

    <a id="_CPPv4N24bk_a2dp_media_ctrl_ack_t30BK_A2DP_MEDIA_CTRL_ACK_FAILUREE"></a>

    <a id="_CPPv3N24bk_a2dp_media_ctrl_ack_t30BK_A2DP_MEDIA_CTRL_ACK_FAILUREE"></a> <a id="_CPPv2N24bk_a2dp_media_ctrl_ack_t30BK_A2DP_MEDIA_CTRL_ACK_FAILUREE"></a> <a id="bk__dm__a2dp__types_8h_1a0db96c8b62acb8620c8aa31451dd0b37ab9fe1c927b4570db1cda12b1ae565682"></a> enumerator BK\_A2DP\_MEDIA\_CTRL\_ACK\_FAILURE
    :   media control command is acknowledged with failure

    <a id="_CPPv4N24bk_a2dp_media_ctrl_ack_t27BK_A2DP_MEDIA_CTRL_ACK_BUSYE"></a>

    <a id="_CPPv3N24bk_a2dp_media_ctrl_ack_t27BK_A2DP_MEDIA_CTRL_ACK_BUSYE"></a> <a id="_CPPv2N24bk_a2dp_media_ctrl_ack_t27BK_A2DP_MEDIA_CTRL_ACK_BUSYE"></a> <a id="bk__dm__a2dp__types_8h_1a0db96c8b62acb8620c8aa31451dd0b37ab90fd1a8978f2c1d3cf253554e0cd33c"></a> enumerator BK\_A2DP\_MEDIA\_CTRL\_ACK\_BUSY
    :   media control command is rejected, as previous command is not yet acknowledged

<a id="_CPPv420bk_a2dp_codec_type_t"></a>

<a id="_CPPv320bk_a2dp_codec_type_t"></a> <a id="_CPPv220bk_a2dp_codec_type_t"></a> <a id="bk__dm__a2dp__types_8h_1ab7ab8a009f94654535f353fbcc1e8a3d"></a> enum bk\_a2dp\_codec\_type\_t
:   *Values:*

    <a id="_CPPv4N20bk_a2dp_codec_type_t22BK_A2DP_CODEC_TYPE_SBCE"></a>

    <a id="_CPPv3N20bk_a2dp_codec_type_t22BK_A2DP_CODEC_TYPE_SBCE"></a> <a id="_CPPv2N20bk_a2dp_codec_type_t22BK_A2DP_CODEC_TYPE_SBCE"></a> <a id="bk__dm__a2dp__types_8h_1ab7ab8a009f94654535f353fbcc1e8a3dac692021536b2678d48363787c43d4cdc"></a> enumerator BK\_A2DP\_CODEC\_TYPE\_SBC

    <a id="_CPPv4N20bk_a2dp_codec_type_t22BK_A2DP_CODEC_TYPE_AACE"></a>

    <a id="_CPPv3N20bk_a2dp_codec_type_t22BK_A2DP_CODEC_TYPE_AACE"></a> <a id="_CPPv2N20bk_a2dp_codec_type_t22BK_A2DP_CODEC_TYPE_AACE"></a> <a id="bk__dm__a2dp__types_8h_1ab7ab8a009f94654535f353fbcc1e8a3dadec5f76328b1c69d1d84dc5d83debe43"></a> enumerator BK\_A2DP\_CODEC\_TYPE\_AAC

<a id="_CPPv425bk_a2dp_sbc_sample_freq_t"></a>

<a id="_CPPv325bk_a2dp_sbc_sample_freq_t"></a> <a id="_CPPv225bk_a2dp_sbc_sample_freq_t"></a> <a id="bk__dm__a2dp__types_8h_1af67a5b33f258c18286ba6a68f38a9f17"></a> enum bk\_a2dp\_sbc\_sample\_freq\_t
:   *Values:*

    <a id="_CPPv4N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_16000E"></a>

    <a id="_CPPv3N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_16000E"></a> <a id="_CPPv2N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_16000E"></a> <a id="bk__dm__a2dp__types_8h_1af67a5b33f258c18286ba6a68f38a9f17a20bf0bc96351067b52274bc1d390dd30"></a> enumerator BK\_A2DP\_SBC\_SAMPLE\_FREQ\_16000

    <a id="_CPPv4N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_32000E"></a>

    <a id="_CPPv3N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_32000E"></a> <a id="_CPPv2N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_32000E"></a> <a id="bk__dm__a2dp__types_8h_1af67a5b33f258c18286ba6a68f38a9f17a9f680d4a4dd371dca7a5a9bc68ace83a"></a> enumerator BK\_A2DP\_SBC\_SAMPLE\_FREQ\_32000

    <a id="_CPPv4N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_44100E"></a>

    <a id="_CPPv3N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_44100E"></a> <a id="_CPPv2N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_44100E"></a> <a id="bk__dm__a2dp__types_8h_1af67a5b33f258c18286ba6a68f38a9f17a6a136530ed285fd1bf17198a48be40d1"></a> enumerator BK\_A2DP\_SBC\_SAMPLE\_FREQ\_44100

    <a id="_CPPv4N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_48000E"></a>

    <a id="_CPPv3N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_48000E"></a> <a id="_CPPv2N25bk_a2dp_sbc_sample_freq_t29BK_A2DP_SBC_SAMPLE_FREQ_48000E"></a> <a id="bk__dm__a2dp__types_8h_1af67a5b33f258c18286ba6a68f38a9f17a335d9b33df0fdcae42983d8bdc267fda"></a> enumerator BK\_A2DP\_SBC\_SAMPLE\_FREQ\_48000

<a id="_CPPv426bk_a2dp_sbc_channel_mode_t"></a>

<a id="_CPPv326bk_a2dp_sbc_channel_mode_t"></a> <a id="_CPPv226bk_a2dp_sbc_channel_mode_t"></a> <a id="bk__dm__a2dp__types_8h_1ae6d716d073abff06740cae92080743b7"></a> enum bk\_a2dp\_sbc\_channel\_mode\_t
:   *Values:*

    <a id="_CPPv4N26bk_a2dp_sbc_channel_mode_t29BK_A2DP_SBC_CHANNEL_MODE_MONOE"></a>

    <a id="_CPPv3N26bk_a2dp_sbc_channel_mode_t29BK_A2DP_SBC_CHANNEL_MODE_MONOE"></a> <a id="_CPPv2N26bk_a2dp_sbc_channel_mode_t29BK_A2DP_SBC_CHANNEL_MODE_MONOE"></a> <a id="bk__dm__a2dp__types_8h_1ae6d716d073abff06740cae92080743b7af726976e870ab23ec5b060bed07b4e66"></a> enumerator BK\_A2DP\_SBC\_CHANNEL\_MODE\_MONO

    <a id="_CPPv4N26bk_a2dp_sbc_channel_mode_t29BK_A2DP_SBC_CHANNEL_MODE_DUALE"></a>

    <a id="_CPPv3N26bk_a2dp_sbc_channel_mode_t29BK_A2DP_SBC_CHANNEL_MODE_DUALE"></a> <a id="_CPPv2N26bk_a2dp_sbc_channel_mode_t29BK_A2DP_SBC_CHANNEL_MODE_DUALE"></a> <a id="bk__dm__a2dp__types_8h_1ae6d716d073abff06740cae92080743b7a0fe9096b2e7a0cacf5497cb4811b44b6"></a> enumerator BK\_A2DP\_SBC\_CHANNEL\_MODE\_DUAL

    <a id="_CPPv4N26bk_a2dp_sbc_channel_mode_t31BK_A2DP_SBC_CHANNEL_MODE_STEREOE"></a>

    <a id="_CPPv3N26bk_a2dp_sbc_channel_mode_t31BK_A2DP_SBC_CHANNEL_MODE_STEREOE"></a> <a id="_CPPv2N26bk_a2dp_sbc_channel_mode_t31BK_A2DP_SBC_CHANNEL_MODE_STEREOE"></a> <a id="bk__dm__a2dp__types_8h_1ae6d716d073abff06740cae92080743b7a653261ae3ae2dd27fcf869b3d386a385"></a> enumerator BK\_A2DP\_SBC\_CHANNEL\_MODE\_STEREO

    <a id="_CPPv4N26bk_a2dp_sbc_channel_mode_t37BK_A2DP_SBC_CHANNEL_MODE_JOINT_STEREOE"></a>

    <a id="_CPPv3N26bk_a2dp_sbc_channel_mode_t37BK_A2DP_SBC_CHANNEL_MODE_JOINT_STEREOE"></a> <a id="_CPPv2N26bk_a2dp_sbc_channel_mode_t37BK_A2DP_SBC_CHANNEL_MODE_JOINT_STEREOE"></a> <a id="bk__dm__a2dp__types_8h_1ae6d716d073abff06740cae92080743b7a510b73521093976335e3eb11a2c67afc"></a> enumerator BK\_A2DP\_SBC\_CHANNEL\_MODE\_JOINT\_STEREO

<a id="_CPPv423bk_a2dp_sbc_block_len_t"></a>

<a id="_CPPv323bk_a2dp_sbc_block_len_t"></a> <a id="_CPPv223bk_a2dp_sbc_block_len_t"></a> <a id="bk__dm__a2dp__types_8h_1ace9dd36841dc1b44deeee305a9e91a7e"></a> enum bk\_a2dp\_sbc\_block\_len\_t
:   *Values:*

    <a id="_CPPv4N23bk_a2dp_sbc_block_len_t23BK_A2DP_SBC_BLOCK_LEN_4E"></a>

    <a id="_CPPv3N23bk_a2dp_sbc_block_len_t23BK_A2DP_SBC_BLOCK_LEN_4E"></a> <a id="_CPPv2N23bk_a2dp_sbc_block_len_t23BK_A2DP_SBC_BLOCK_LEN_4E"></a> <a id="bk__dm__a2dp__types_8h_1ace9dd36841dc1b44deeee305a9e91a7ea91e68a628f136a73ee48f96e99eead37"></a> enumerator BK\_A2DP\_SBC\_BLOCK\_LEN\_4

    <a id="_CPPv4N23bk_a2dp_sbc_block_len_t23BK_A2DP_SBC_BLOCK_LEN_8E"></a>

    <a id="_CPPv3N23bk_a2dp_sbc_block_len_t23BK_A2DP_SBC_BLOCK_LEN_8E"></a> <a id="_CPPv2N23bk_a2dp_sbc_block_len_t23BK_A2DP_SBC_BLOCK_LEN_8E"></a> <a id="bk__dm__a2dp__types_8h_1ace9dd36841dc1b44deeee305a9e91a7ea7435947a242af1e4bc030360445b0fdc"></a> enumerator BK\_A2DP\_SBC\_BLOCK\_LEN\_8

    <a id="_CPPv4N23bk_a2dp_sbc_block_len_t24BK_A2DP_SBC_BLOCK_LEN_12E"></a>

    <a id="_CPPv3N23bk_a2dp_sbc_block_len_t24BK_A2DP_SBC_BLOCK_LEN_12E"></a> <a id="_CPPv2N23bk_a2dp_sbc_block_len_t24BK_A2DP_SBC_BLOCK_LEN_12E"></a> <a id="bk__dm__a2dp__types_8h_1ace9dd36841dc1b44deeee305a9e91a7ead19a6321f63d0018ab36d1121e01f2dc"></a> enumerator BK\_A2DP\_SBC\_BLOCK\_LEN\_12

    <a id="_CPPv4N23bk_a2dp_sbc_block_len_t24BK_A2DP_SBC_BLOCK_LEN_16E"></a>

    <a id="_CPPv3N23bk_a2dp_sbc_block_len_t24BK_A2DP_SBC_BLOCK_LEN_16E"></a> <a id="_CPPv2N23bk_a2dp_sbc_block_len_t24BK_A2DP_SBC_BLOCK_LEN_16E"></a> <a id="bk__dm__a2dp__types_8h_1ace9dd36841dc1b44deeee305a9e91a7eabac56adf1d9d5b32f55b35caa4f3ea98"></a> enumerator BK\_A2DP\_SBC\_BLOCK\_LEN\_16

<a id="_CPPv421bk_a2dp_sbc_subband_t"></a>

<a id="_CPPv321bk_a2dp_sbc_subband_t"></a> <a id="_CPPv221bk_a2dp_sbc_subband_t"></a> <a id="bk__dm__a2dp__types_8h_1acc3ce52f668c354fa93688c48c2a2d21"></a> enum bk\_a2dp\_sbc\_subband\_t
:   *Values:*

    <a id="_CPPv4N21bk_a2dp_sbc_subband_t21BK_A2DP_SBC_SUBBAND_4E"></a>

    <a id="_CPPv3N21bk_a2dp_sbc_subband_t21BK_A2DP_SBC_SUBBAND_4E"></a> <a id="_CPPv2N21bk_a2dp_sbc_subband_t21BK_A2DP_SBC_SUBBAND_4E"></a> <a id="bk__dm__a2dp__types_8h_1acc3ce52f668c354fa93688c48c2a2d21ac9bd3d76d8b52d17bee73c443daf107b"></a> enumerator BK\_A2DP\_SBC\_SUBBAND\_4

    <a id="_CPPv4N21bk_a2dp_sbc_subband_t21BK_A2DP_SBC_SUBBAND_8E"></a>

    <a id="_CPPv3N21bk_a2dp_sbc_subband_t21BK_A2DP_SBC_SUBBAND_8E"></a> <a id="_CPPv2N21bk_a2dp_sbc_subband_t21BK_A2DP_SBC_SUBBAND_8E"></a> <a id="bk__dm__a2dp__types_8h_1acc3ce52f668c354fa93688c48c2a2d21a9980efe4cc4fda370bfe72d7f02f117d"></a> enumerator BK\_A2DP\_SBC\_SUBBAND\_8

<a id="_CPPv422bk_a2dp_alloc_method_t"></a>

<a id="_CPPv322bk_a2dp_alloc_method_t"></a> <a id="_CPPv222bk_a2dp_alloc_method_t"></a> <a id="bk__dm__a2dp__types_8h_1a4e23938c1fbc2d3d494d23aabe320a53"></a> enum bk\_a2dp\_alloc\_method\_t
:   *Values:*

    <a id="_CPPv4N22bk_a2dp_alloc_method_t24BK_A2DP_ALLOC_METHOD_SNRE"></a>

    <a id="_CPPv3N22bk_a2dp_alloc_method_t24BK_A2DP_ALLOC_METHOD_SNRE"></a> <a id="_CPPv2N22bk_a2dp_alloc_method_t24BK_A2DP_ALLOC_METHOD_SNRE"></a> <a id="bk__dm__a2dp__types_8h_1a4e23938c1fbc2d3d494d23aabe320a53a54eb5aa055a31d5c1eea86c38c550975"></a> enumerator BK\_A2DP\_ALLOC\_METHOD\_SNR

    <a id="_CPPv4N22bk_a2dp_alloc_method_t29BK_A2DP_ALLOC_METHOD_LOUDNESSE"></a>

    <a id="_CPPv3N22bk_a2dp_alloc_method_t29BK_A2DP_ALLOC_METHOD_LOUDNESSE"></a> <a id="_CPPv2N22bk_a2dp_alloc_method_t29BK_A2DP_ALLOC_METHOD_LOUDNESSE"></a> <a id="bk__dm__a2dp__types_8h_1a4e23938c1fbc2d3d494d23aabe320a53a40406f3579cf79ae7442b3b21a0ffb8f"></a> enumerator BK\_A2DP\_ALLOC\_METHOD\_LOUDNESS

<a id="_CPPv431bk_a2dp_set_delay_value_state_t"></a>

<a id="_CPPv331bk_a2dp_set_delay_value_state_t"></a> <a id="_CPPv231bk_a2dp_set_delay_value_state_t"></a> <a id="bk__dm__a2dp__types_8h_1a4ed4501c6ceaf9be6dce0e910b810d52"></a> enum bk\_a2dp\_set\_delay\_value\_state\_t
:   Bluetooth A2DP set delay report value states.

    *Values:*

    <a id="_CPPv4N31bk_a2dp_set_delay_value_state_t19BK_A2DP_SET_SUCCESSE"></a>

    <a id="_CPPv3N31bk_a2dp_set_delay_value_state_t19BK_A2DP_SET_SUCCESSE"></a> <a id="_CPPv2N31bk_a2dp_set_delay_value_state_t19BK_A2DP_SET_SUCCESSE"></a> <a id="bk__dm__a2dp__types_8h_1a4ed4501c6ceaf9be6dce0e910b810d52ae58c96e94927bca8f07f806b10120173"></a> enumerator BK\_A2DP\_SET\_SUCCESS
    :   A2DP profile set delay report value successful

    <a id="_CPPv4N31bk_a2dp_set_delay_value_state_t16BK_A2DP_SET_FAILE"></a>

    <a id="_CPPv3N31bk_a2dp_set_delay_value_state_t16BK_A2DP_SET_FAILE"></a> <a id="_CPPv2N31bk_a2dp_set_delay_value_state_t16BK_A2DP_SET_FAILE"></a> <a id="bk__dm__a2dp__types_8h_1a4ed4501c6ceaf9be6dce0e910b810d52a992021827a91504d039c6e803db99eaa"></a> enumerator BK\_A2DP\_SET\_FAIL
    :   A2DP profile set delay report value failed

<a id="bk-dm-avrcp-types-h"></a>

## bk\_dm\_avrcp\_types.h

`bk_dm_avrcp_types.h` 定义 AVRCP profile 使用的事件、状态和媒体控制类型。

<a id="id37"></a>

### Header File

- [bk\_dm\_avrcp\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_avrcp_types.h)

<a id="id38"></a>

### Unions

<a id="_CPPv419bk_avrcp_rn_param_t"></a>

<a id="_CPPv319bk_avrcp_rn_param_t"></a> <a id="_CPPv219bk_avrcp_rn_param_t"></a> <a id="unionbk__avrcp__rn__param__t"></a> union bk\_avrcp\_rn\_param\_t
:   *#include \<bk\_dm\_avrcp\_types.h\>*

    AVRCP notification parameters.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19bk_avrcp_rn_param_t6volumeE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t6volumeE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t6volumeE"></a> <a id="bk_avrcp_rn_param_t::volume__uint8_t"></a> <a id="unionbk__avrcp__rn__param__t_1aad10cabcea6d19cc18d1d226a4db3fb9"></a> uint8\_t volume
    :   response data for BK\_AVRCP\_RN\_VOLUME\_CHANGE, ranges 0..127

    <a id="_CPPv4N19bk_avrcp_rn_param_t8playbackE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t8playbackE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t8playbackE"></a> <a id="bk_avrcp_rn_param_t::playback__bk_avrcp_playback_stat_t"></a> <a id="unionbk__avrcp__rn__param__t_1ae7b00714f8a3d6aa3ee7b32fc1155b1e"></a> [bk\_avrcp\_playback\_stat\_t](#_CPPv424bk_avrcp_playback_stat_t "bk_avrcp_playback_stat_t") playback
    :   response data for BK\_AVRCP\_RN\_PLAY\_STATUS\_CHANGE

    <a id="_CPPv4N19bk_avrcp_rn_param_t6elm_idE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t6elm_idE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t6elm_idE"></a> <a id="bk_avrcp_rn_param_t::elm_id__uint8_tA"></a> <a id="unionbk__avrcp__rn__param__t_1aef9eadb982a1cf6354167335869d5e85"></a> uint8\_t elm\_id\[8\]
    :   response data for BK\_AVRCP\_RN\_TRACK\_CHANGE

    <a id="_CPPv4N19bk_avrcp_rn_param_t8play_posE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t8play_posE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t8play_posE"></a> <a id="bk_avrcp_rn_param_t::play_pos__uint32_t"></a> <a id="unionbk__avrcp__rn__param__t_1af8b376bc0ae407121833019e05294b7b"></a> uint32\_t play\_pos
    :   response data for BK\_AVRCP\_RN\_PLAY\_POS\_CHANGED, in millisecond

    <a id="_CPPv4N19bk_avrcp_rn_param_t4battE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t4battE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t4battE"></a> <a id="bk_avrcp_rn_param_t::batt__bk_avrcp_batt_stat_t"></a> <a id="unionbk__avrcp__rn__param__t_1a6d28dbfa8d62a053ecc15210af137d33"></a> [bk\_avrcp\_batt\_stat\_t](#_CPPv420bk_avrcp_batt_stat_t "bk_avrcp_batt_stat_t") batt
    :   response data for BK\_AVRCP\_RN\_BATTERY\_STATUS\_CHANGE

    <a id="_CPPv4N19bk_avrcp_rn_param_t9player_idE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t9player_idE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t9player_idE"></a> <a id="bk_avrcp_rn_param_t::player_id__uint16_t"></a> <a id="unionbk__avrcp__rn__param__t_1a8e87556adbce560b8dea487659ba1c67"></a> uint16\_t player\_id

    <a id="_CPPv4N19bk_avrcp_rn_param_t3uidE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t3uidE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t3uidE"></a> <a id="bk_avrcp_rn_param_t::uid__uint16_t"></a> <a id="unionbk__avrcp__rn__param__t_1a40de0e95f4f2eb8736a1a02b62c38a8e"></a> uint16\_t uid

    <a id="_CPPv4N19bk_avrcp_rn_param_tUt2_48E"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_tUt2_48E"></a> <a id="unionbk__avrcp__rn__param__t_1a0874b9c3fdc1411879b9c9769fd71c51"></a> struct [bk\_avrcp\_rn\_param\_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t")::\[anonymous\] \[anonymous\]

    <a id="_CPPv4N19bk_avrcp_rn_param_t11uid_counterE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t11uid_counterE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t11uid_counterE"></a> <a id="bk_avrcp_rn_param_t::uid_counter__uint16_t"></a> <a id="unionbk__avrcp__rn__param__t_1a313ac074662694882308e7a81bdc9d90"></a> uint16\_t uid\_counter
    :   response data for BK\_AVRCP\_RN\_UIDS\_CHANGE

    <a id="_CPPv4N19bk_avrcp_rn_param_t13system_statusE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t13system_statusE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t13system_statusE"></a> <a id="bk_avrcp_rn_param_t::system_status__uint8_t"></a> <a id="unionbk__avrcp__rn__param__t_1adc80e93eeea858c4e5248a00872b05c8"></a> uint8\_t system\_status
    :   response data for BK\_AVRCP\_RN\_SYSTEM\_STATUS\_CHANGE

    <a id="_CPPv4N19bk_avrcp_rn_param_t20player_app_set_countE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t20player_app_set_countE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t20player_app_set_countE"></a> <a id="bk_avrcp_rn_param_t::player_app_set_count__uint8_t"></a> <a id="unionbk__avrcp__rn__param__t_1a948d48f75ca3b8b15002dd41cbadfee4"></a> uint8\_t player\_app\_set\_count

    <a id="_CPPv4N19bk_avrcp_rn_param_t7attr_idE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t7attr_idE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t7attr_idE"></a> <a id="bk_avrcp_rn_param_t::attr_id__uint8_t"></a> <a id="unionbk__avrcp__rn__param__t_1a0c63a49c9a7a17f34602a211a409bc48"></a> uint8\_t attr\_id

    <a id="_CPPv4N19bk_avrcp_rn_param_t8value_idE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t8value_idE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t8value_idE"></a> <a id="bk_avrcp_rn_param_t::value_id__uint8_t"></a> <a id="unionbk__avrcp__rn__param__t_1ad54039c34d936149831fbf7118b64720"></a> uint8\_t value\_id

    <a id="_CPPv4N19bk_avrcp_rn_param_t20player_app_set_arrayE"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_t20player_app_set_arrayE"></a> <a id="_CPPv2N19bk_avrcp_rn_param_t20player_app_set_arrayE"></a> <a id="unionbk__avrcp__rn__param__t_1a046813561d0e5d151a8a8bc07c0612d4"></a> struct [bk\_avrcp\_rn\_param\_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t")::\[anonymous\]::\[anonymous\] player\_app\_set\_array\[[BK\_AVRCP\_PS\_MAX\_ATTR](#_CPPv4N22bk_avrcp_ps_attr_ids_t20BK_AVRCP_PS_MAX_ATTRE "BK_AVRCP_PS_MAX_ATTR")\]

    <a id="_CPPv4N19bk_avrcp_rn_param_tUt2_50E"></a>

    <a id="_CPPv3N19bk_avrcp_rn_param_tUt2_50E"></a> <a id="unionbk__avrcp__rn__param__t_1ac5473bc5e7b536c150e3e97ab5383727"></a> struct [bk\_avrcp\_rn\_param\_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t")::\[anonymous\] \[anonymous\]

<a id="_CPPv422bk_avrcp_ct_cb_param_t"></a>

<a id="_CPPv322bk_avrcp_ct_cb_param_t"></a> <a id="_CPPv222bk_avrcp_ct_cb_param_t"></a> <a id="unionbk__avrcp__ct__cb__param__t"></a> union bk\_avrcp\_ct\_cb\_param\_t
:   *#include \<bk\_dm\_avrcp\_types.h\>*

    AVRCP controller callback parameters.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t10conn_stateE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t10conn_stateE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t10conn_stateE"></a> <a id="bk_avrcp_ct_cb_param_t::conn_state__bk_avrcp_ct_cb_param_t::avrcp_ct_conn_state_param"></a> <a id="unionbk__avrcp__ct__cb__param__t_1ae9b4846cc895da3acf4f2f9b13c48589"></a> struct [bk\_avrcp\_ct\_cb\_param\_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp\_ct\_conn\_state\_param](#_CPPv4N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_conn_state_param") conn\_state
    :   AVRCP connection status

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t8psth_rspE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t8psth_rspE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t8psth_rspE"></a> <a id="bk_avrcp_ct_cb_param_t::psth_rsp__bk_avrcp_ct_cb_param_t::avrcp_ct_psth_rsp_param"></a> <a id="unionbk__avrcp__ct__cb__param__t_1a606317b462d036c29c91765d7e7450ff"></a> struct [bk\_avrcp\_ct\_cb\_param\_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp\_ct\_psth\_rsp\_param](#_CPPv4N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_psth_rsp_param") psth\_rsp
    :   passthrough command response

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t10change_ntfE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t10change_ntfE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t10change_ntfE"></a> <a id="bk_avrcp_ct_cb_param_t::change_ntf__bk_avrcp_ct_cb_param_t::avrcp_ct_change_notify_param"></a> <a id="unionbk__avrcp__ct__cb__param__t_1a7288aab5d7f105a71da803e17ecb25a1"></a> struct [bk\_avrcp\_ct\_cb\_param\_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp\_ct\_change\_notify\_param](#_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_change_notify_param") change\_ntf
    :   notifications

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t15get_rn_caps_rspE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t15get_rn_caps_rspE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t15get_rn_caps_rspE"></a> <a id="bk_avrcp_ct_cb_param_t::get_rn_caps_rsp__bk_avrcp_ct_cb_param_t::avrcp_ct_get_rn_caps_rsp_param"></a> <a id="unionbk__avrcp__ct__cb__param__t_1ab912c27e12338ab3787dfa95b8edf72a"></a> struct [bk\_avrcp\_ct\_cb\_param\_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp\_ct\_get\_rn\_caps\_rsp\_param](#_CPPv4N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_get_rn_caps_rsp_param") get\_rn\_caps\_rsp
    :   get supported event capabilities response from AVRCP target

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t14set_volume_rspE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t14set_volume_rspE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t14set_volume_rspE"></a> <a id="bk_avrcp_ct_cb_param_t::set_volume_rsp__bk_avrcp_ct_cb_param_t::avrcp_ct_set_volume_rsp_param"></a> <a id="unionbk__avrcp__ct__cb__param__t_1adcc991fba650d525c0608867f13d32d4"></a> struct [bk\_avrcp\_ct\_cb\_param\_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp\_ct\_set\_volume\_rsp\_param](#_CPPv4N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_set_volume_rsp_param") set\_volume\_rsp
    :   set absolute volume response event

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t26set_player_app_setting_rspE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t26set_player_app_setting_rspE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t26set_player_app_setting_rspE"></a> <a id="bk_avrcp_ct_cb_param_t::set_player_app_setting_rsp__bk_avrcp_ct_cb_param_t::avrcp_ct_set_player_app_setting_rsp_param"></a> <a id="unionbk__avrcp__ct__cb__param__t_1a3115d00af185e2f00170d51d117b8b92"></a> struct [bk\_avrcp\_ct\_cb\_param\_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp\_ct\_set\_player\_app\_setting\_rsp\_param](#_CPPv4N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_set_player_app_setting_rsp_param") set\_player\_app\_setting\_rsp
    :   set player app setting response event

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t13elem_attr_rspE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t13elem_attr_rspE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t13elem_attr_rspE"></a> <a id="bk_avrcp_ct_cb_param_t::elem_attr_rsp__bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param"></a> <a id="unionbk__avrcp__ct__cb__param__t_1a3c2a0829537689574c48c6438d95e048"></a> struct [bk\_avrcp\_ct\_cb\_param\_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp\_ct\_elem\_attr\_rsp\_param](#_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param") elem\_attr\_rsp
    :   metadata attributes response

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_paramE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_paramE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_change_notify_param"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__change__notify__param"></a> struct avrcp\_ct\_change\_notify\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_CT\_CHANGE\_NOTIFY\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param8event_idE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param8event_idE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param8event_idE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_change_notify_param::event_id__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__change__notify__param_1ac3a48adacda8524e79ec653cba884d18"></a> uint8\_t event\_id
        :   id of AVRCP event notification

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param15event_parameterE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param15event_parameterE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param15event_parameterE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_change_notify_param::event_parameter__bk_avrcp_rn_param_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__change__notify__param_1a44e3794d1abdf36dcf1944a01eeaaec4"></a> [bk\_avrcp\_rn\_param\_t](#_CPPv419bk_avrcp_rn_param_t "bk_avrcp_rn_param_t") event\_parameter
        :   event notification parameter

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param10remote_bdaE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_change_notify_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__change__notify__param_1a106332659f99a55344e0061b9a48fb2f"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param6rn_rspE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param6rn_rspE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_change_notify_param6rn_rspE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_change_notify_param::rn_rsp__bk_avrcp_rn_rsp_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__change__notify__param_1a370621fcc836c468ad54df0c37d986ef"></a> [bk\_avrcp\_rn\_rsp\_t](#_CPPv417bk_avrcp_rn_rsp_t "bk_avrcp_rn_rsp_t") rn\_rsp
        :   peer rn rsp

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_paramE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_paramE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_conn_state_param"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__conn__state__param"></a> struct avrcp\_ct\_conn\_state\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_CT\_CONNECTION\_STATE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_param9connectedE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_param9connectedE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_param9connectedE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_conn_state_param::connected__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__conn__state__param_1adb9662c9502b9ee1c51cce04ba7ac395"></a> uint8\_t connected
        :   whether AVRCP connection is set up

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t25avrcp_ct_conn_state_param10remote_bdaE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_conn_state_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__conn__state__param_1a312d5ae30306f05976c0832351b2f503"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_paramE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_paramE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__elem__attr__rsp__param"></a> struct avrcp\_ct\_elem\_attr\_rsp\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_CT\_GET\_ELEM\_ATTR\_RSP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param6statusE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param6statusE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param6statusE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param::status__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__elem__attr__rsp__param_1a90e6df5f81edbe2f0129267cac50a924"></a> uint8\_t status

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param10attr_countE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param10attr_countE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param10attr_countE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param::attr_count__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__elem__attr__rsp__param_1af1c718b189e1e04f4e4f142ce07d0ee8"></a> uint8\_t attr\_count
        :   0 means success

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param7attr_idE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param7attr_idE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param7attr_idE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param::attr_id__uint32_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__elem__attr__rsp__param_1a1f70f5e07a34443975101b2bb0b2562c"></a> uint32\_t attr\_id
        :   elem attribute id, see bk\_avrcp\_media\_attr\_id\_t

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param17attr_text_charsetE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param17attr_text_charsetE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param17attr_text_charsetE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param::attr_text_charset__uint16_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__elem__attr__rsp__param_1acb2a0a3b3021d0b9e618514c24903caf"></a> uint16\_t attr\_text\_charset

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param11attr_lengthE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param11attr_lengthE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param11attr_lengthE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param::attr_length__uint32_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__elem__attr__rsp__param_1af08b99ac600959cada3af05ccab712ea"></a> uint32\_t attr\_length
        :   attr text charset, see <http://www.iana.org/assignments/character-sets>

            attribute character length

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param9attr_textE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param9attr_textE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param9attr_textE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param::attr_text__uint8_tP"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__elem__attr__rsp__param_1a85e00da19e639b2958a70199028386e7"></a> uint8\_t \*attr\_text
        :   attribute itself

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param10attr_arrayE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param10attr_arrayE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param10attr_arrayE"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__elem__attr__rsp__param_1a4f4e05d813335f33cf4352e6f6c2bd0d"></a> struct [bk\_avrcp\_ct\_cb\_param\_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t")::[avrcp\_ct\_elem\_attr\_rsp\_param](#_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_paramE "bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param")::\[anonymous\] \*attr\_array
        :   attr\_array count

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t28avrcp_ct_elem_attr_rsp_param10remote_bdaE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_elem_attr_rsp_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__elem__attr__rsp__param_1a844a4ab4b9e8e40718c609493cf307b8"></a> uint8\_t remote\_bda\[6\]
        :   elem array

            remote bluetooth device address

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_paramE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_paramE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_get_rn_caps_rsp_param"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__get__rn__caps__rsp__param"></a> struct avrcp\_ct\_get\_rn\_caps\_rsp\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_CT\_GET\_RN\_CAPABILITIES\_RSP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_param9cap_countE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_param9cap_countE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_param9cap_countE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_get_rn_caps_rsp_param::cap_count__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__get__rn__caps__rsp__param_1a6d84914e2210ab596344beaf041eecf5"></a> uint8\_t cap\_count
        :   number of items provided in event or company\_id according to cap\_id used

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_param7evt_setE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_param7evt_setE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_param7evt_setE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_get_rn_caps_rsp_param::evt_set__bk_avrcp_rn_evt_cap_mask_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__get__rn__caps__rsp__param_1a89f8787a21020c51a64e47940924404d"></a> [bk\_avrcp\_rn\_evt\_cap\_mask\_t](#_CPPv426bk_avrcp_rn_evt_cap_mask_t "bk_avrcp_rn_evt_cap_mask_t") evt\_set
        :   supported event\_ids represented in bit-mask

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t30avrcp_ct_get_rn_caps_rsp_param10remote_bdaE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_get_rn_caps_rsp_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__get__rn__caps__rsp__param_1a0b818f0c0053230419dbacdd85efb931"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_paramE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_paramE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_psth_rsp_param"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__psth__rsp__param"></a> struct avrcp\_ct\_psth\_rsp\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_CT\_PASSTHROUGH\_RSP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param2tlE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param2tlE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param2tlE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_psth_rsp_param::tl__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__psth__rsp__param_1a58d71634e3b6b6031739a59d830e3329"></a> uint8\_t tl
        :   transaction label, 0 to 15

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param8key_codeE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param8key_codeE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param8key_codeE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_psth_rsp_param::key_code__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__psth__rsp__param_1ac7e20bfad9cb0170ad590972a2c3dd74"></a> uint8\_t key\_code
        :   passthrough command code, see bk\_avrcp\_pt\_cmd\_t

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param9key_stateE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param9key_stateE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param9key_stateE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_psth_rsp_param::key_state__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__psth__rsp__param_1a5ba81a14e0a965eb0a599da6f01cb0aa"></a> uint8\_t key\_state
        :   0 for PRESSED, 1 for RELEASED

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param8rsp_codeE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param8rsp_codeE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param8rsp_codeE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_psth_rsp_param::rsp_code__bk_avrcp_rsp_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__psth__rsp__param_1a7f8077d6b3aea3bc1e60ce3c9c2a4314"></a> [bk\_avrcp\_rsp\_t](#_CPPv414bk_avrcp_rsp_t "bk_avrcp_rsp_t") rsp\_code
        :   response code

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t23avrcp_ct_psth_rsp_param10remote_bdaE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_psth_rsp_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__psth__rsp__param_1a981428cb561c1827f711b8b548546c35"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_paramE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_paramE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_set_player_app_setting_rsp_param"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__set__player__app__setting__rsp__param"></a> struct avrcp\_ct\_set\_player\_app\_setting\_rsp\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_CT\_SET\_PLAYER\_APP\_SETTING\_RSP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_param6statusE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_param6statusE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_param6statusE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_set_player_app_setting_rsp_param::status__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__set__player__app__setting__rsp__param_1ab138de4a177f2e944e4adc6d2cfb45b0"></a> uint8\_t status

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t41avrcp_ct_set_player_app_setting_rsp_param10remote_bdaE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_set_player_app_setting_rsp_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__set__player__app__setting__rsp__param_1abe68c50a97cef08c2669a03b68b51306"></a> uint8\_t remote\_bda\[6\]
        :   0 means success

            remote bluetooth device address

    <a id="_CPPv4N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_paramE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_paramE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_set_volume_rsp_param"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__set__volume__rsp__param"></a> struct avrcp\_ct\_set\_volume\_rsp\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_CT\_SET\_ABSOLUTE\_VOLUME\_RSP\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_param6statusE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_param6statusE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_param6statusE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_set_volume_rsp_param::status__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__set__volume__rsp__param_1a41c6f0c743415fa54fa0a0667501f3d2"></a> uint8\_t status

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_param6volumeE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_param6volumeE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_param6volumeE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_set_volume_rsp_param::volume__uint8_t"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__set__volume__rsp__param_1a93624c746c689d666025359ec812e635"></a> uint8\_t volume
        :   0 means success

            the volume which has actually been set, range is 0 to 0x7f, means 0% to 100%

        <a id="_CPPv4N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_param_t29avrcp_ct_set_volume_rsp_param10remote_bdaE"></a> <a id="bk_avrcp_ct_cb_param_t::avrcp_ct_set_volume_rsp_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__ct__cb__param__t_1_1avrcp__ct__set__volume__rsp__param_1a9b3bdc4fc2caa78c1a3a207ace875a56"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

<a id="_CPPv422bk_avrcp_tg_cb_param_t"></a>

<a id="_CPPv322bk_avrcp_tg_cb_param_t"></a> <a id="_CPPv222bk_avrcp_tg_cb_param_t"></a> <a id="unionbk__avrcp__tg__cb__param__t"></a> union bk\_avrcp\_tg\_cb\_param\_t
:   *#include \<bk\_dm\_avrcp\_types.h\>*

    AVRC target callback parameters.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_avrcp_tg_cb_param_t9conn_statE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_param_t9conn_statE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t9conn_statE"></a> <a id="bk_avrcp_tg_cb_param_t::conn_stat__bk_avrcp_tg_cb_param_t::avrcp_tg_conn_stat_param"></a> <a id="unionbk__avrcp__tg__cb__param__t_1a43405f2627c612b465879aeac9bb3390"></a> struct [bk\_avrcp\_tg\_cb\_param\_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t")::[avrcp\_tg\_conn\_stat\_param](#_CPPv4N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_paramE "bk_avrcp_tg_cb_param_t::avrcp_tg_conn_stat_param") conn\_stat
    :   AVRC connection status

    <a id="_CPPv4N22bk_avrcp_tg_cb_param_t8psth_cmdE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_param_t8psth_cmdE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t8psth_cmdE"></a> <a id="bk_avrcp_tg_cb_param_t::psth_cmd__bk_avrcp_tg_cb_param_t::avrcp_tg_psth_cmd_param"></a> <a id="unionbk__avrcp__tg__cb__param__t_1a263978f5c4ac822f668f23954dc59dee"></a> struct [bk\_avrcp\_tg\_cb\_param\_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t")::[avrcp\_tg\_psth\_cmd\_param](#_CPPv4N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_paramE "bk_avrcp_tg_cb_param_t::avrcp_tg_psth_cmd_param") psth\_cmd
    :   passthrough command

    <a id="_CPPv4N22bk_avrcp_tg_cb_param_t11set_abs_volE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_param_t11set_abs_volE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t11set_abs_volE"></a> <a id="bk_avrcp_tg_cb_param_t::set_abs_vol__bk_avrcp_tg_cb_param_t::avrcp_tg_set_abs_vol_param"></a> <a id="unionbk__avrcp__tg__cb__param__t_1ad98b35555e78f075ba32323d086fbc7f"></a> struct [bk\_avrcp\_tg\_cb\_param\_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t")::[avrcp\_tg\_set\_abs\_vol\_param](#_CPPv4N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_paramE "bk_avrcp_tg_cb_param_t::avrcp_tg_set_abs_vol_param") set\_abs\_vol
    :   set absolute volume command targeted on audio sink

    <a id="_CPPv4N22bk_avrcp_tg_cb_param_t7reg_ntfE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_param_t7reg_ntfE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t7reg_ntfE"></a> <a id="bk_avrcp_tg_cb_param_t::reg_ntf__bk_avrcp_tg_cb_param_t::avrcp_tg_reg_ntf_param"></a> <a id="unionbk__avrcp__tg__cb__param__t_1ad23b8ebc9228cc2ae19f4638dfca9ccc"></a> struct [bk\_avrcp\_tg\_cb\_param\_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t")::[avrcp\_tg\_reg\_ntf\_param](#_CPPv4N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_paramE "bk_avrcp_tg_cb_param_t::avrcp_tg_reg_ntf_param") reg\_ntf
    :   register notification

    <a id="_CPPv4N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_paramE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_paramE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_conn_stat_param"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__conn__stat__param"></a> struct avrcp\_tg\_conn\_stat\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_TG\_CONNECTION\_STATE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_param9connectedE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_param9connectedE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_param9connectedE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_conn_stat_param::connected__b"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__conn__stat__param_1ac84d5807f7b1ba792c87556b5370507d"></a> bool connected
        :   whether AVRC connection is set up

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t24avrcp_tg_conn_stat_param10remote_bdaE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_conn_stat_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__conn__stat__param_1acef3a6e6f8fc22a3dd3b88b845ee01a0"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

    <a id="_CPPv4N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_paramE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_paramE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_psth_cmd_param"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__psth__cmd__param"></a> struct avrcp\_tg\_psth\_cmd\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_TG\_PASSTHROUGH\_CMD\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_param8key_codeE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_param8key_codeE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_param8key_codeE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_psth_cmd_param::key_code__uint8_t"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__psth__cmd__param_1a387319421a90bf98eea484594c490e54"></a> uint8\_t key\_code
        :   passthrough command code

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_param9key_stateE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_param9key_stateE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_param9key_stateE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_psth_cmd_param::key_state__uint8_t"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__psth__cmd__param_1acfab04bc1065dc93ec9f4d33752731b8"></a> uint8\_t key\_state
        :   0 for PRESSED, 1 for RELEASED

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t23avrcp_tg_psth_cmd_param10remote_bdaE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_psth_cmd_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__psth__cmd__param_1a60bf36ec28775e90f7cb4f16dffdc766"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

    <a id="_CPPv4N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_paramE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_paramE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_reg_ntf_param"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__reg__ntf__param"></a> struct avrcp\_tg\_reg\_ntf\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_TG\_REGISTER\_NOTIFICATION\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_param8event_idE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_param8event_idE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_param8event_idE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_reg_ntf_param::event_id__uint8_t"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__reg__ntf__param_1af9cd66a648f1f24fde04bf838a4eebcf"></a> uint8\_t event\_id
        :   event id of bk\_avrcp\_rn\_event\_ids\_t

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_param15event_parameterE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_param15event_parameterE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_param15event_parameterE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_reg_ntf_param::event_parameter__uint32_t"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__reg__ntf__param_1a6a33d7382147277e732e92b26f14fa68"></a> uint32\_t event\_parameter
        :   event notification parameter, used with BK\_AVRCP\_RN\_PLAY\_POS\_CHANGED only now, means timer in second

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t22avrcp_tg_reg_ntf_param10remote_bdaE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_reg_ntf_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__reg__ntf__param_1a517cbdc6abfa3bc3e550226a1eeac51f"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

    <a id="_CPPv4N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_paramE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_paramE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_paramE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_set_abs_vol_param"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__set__abs__vol__param"></a> struct avrcp\_tg\_set\_abs\_vol\_param
    :   *#include \<bk\_dm\_avrcp\_types.h\>*

        BK\_AVRCP\_TG\_SET\_ABSOLUTE\_VOLUME\_CMD\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_param6volumeE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_param6volumeE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_param6volumeE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_set_abs_vol_param::volume__uint8_t"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__set__abs__vol__param_1a1a9133b3ba615d4c3d5f0abdace3414b"></a> uint8\_t volume
        :   volume ranges from 0 to 127

        <a id="_CPPv4N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_param10remote_bdaE"></a>

        <a id="_CPPv3N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_param10remote_bdaE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_param_t26avrcp_tg_set_abs_vol_param10remote_bdaE"></a> <a id="bk_avrcp_tg_cb_param_t::avrcp_tg_set_abs_vol_param::remote_bda__uint8_tA"></a> <a id="structbk__avrcp__tg__cb__param__t_1_1avrcp__tg__set__abs__vol__param_1a103589671bc2f00745a5af97b5afcdd6"></a> uint8\_t remote\_bda\[6\]
        :   remote bluetooth device address

<a id="id39"></a>

### Structures

<a id="_CPPv426bk_avrcp_rn_evt_cap_mask_t"></a>

<a id="_CPPv326bk_avrcp_rn_evt_cap_mask_t"></a> <a id="_CPPv226bk_avrcp_rn_evt_cap_mask_t"></a> <a id="bk_avrcp_rn_evt_cap_mask_t"></a> <a id="structbk__avrcp__rn__evt__cap__mask__t"></a> struct bk\_avrcp\_rn\_evt\_cap\_mask\_t
:   AVRCP target notification event capability bit mask.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N26bk_avrcp_rn_evt_cap_mask_t4bitsE"></a>

    <a id="_CPPv3N26bk_avrcp_rn_evt_cap_mask_t4bitsE"></a> <a id="_CPPv2N26bk_avrcp_rn_evt_cap_mask_t4bitsE"></a> <a id="bk_avrcp_rn_evt_cap_mask_t::bits__uint16_t"></a> <a id="structbk__avrcp__rn__evt__cap__mask__t_1a46db406a60787f02436984c9224487e4"></a> uint16\_t bits
    :   bit mask representation of supported event\_ids

<a id="_CPPv424bk_avrcp_psth_bit_mask_t"></a>

<a id="_CPPv324bk_avrcp_psth_bit_mask_t"></a> <a id="_CPPv224bk_avrcp_psth_bit_mask_t"></a> <a id="bk_avrcp_psth_bit_mask_t"></a> <a id="structbk__avrcp__psth__bit__mask__t"></a> struct bk\_avrcp\_psth\_bit\_mask\_t
:   AVRC passthrough command bit mask.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N24bk_avrcp_psth_bit_mask_t4bitsE"></a>

    <a id="_CPPv3N24bk_avrcp_psth_bit_mask_t4bitsE"></a> <a id="_CPPv2N24bk_avrcp_psth_bit_mask_t4bitsE"></a> <a id="bk_avrcp_psth_bit_mask_t::bits__uint16_tA"></a> <a id="structbk__avrcp__psth__bit__mask__t_1ab832daa8f17ea42877874ae98543194a"></a> uint16\_t bits\[8\]
    :   bit mask representation of PASSTHROUGH commands

<a id="id40"></a>

### Type Definitions

<a id="_CPPv416bk_avrcp_ct_cb_t"></a>

<a id="_CPPv316bk_avrcp_ct_cb_t"></a> <a id="_CPPv216bk_avrcp_ct_cb_t"></a> <a id="bk_avrcp_ct_cb_t"></a> <a id="group__dm__avrcp__types_1gaec80cf63a3e5c37e5c0dff4993caf959"></a> typedef void (\*bk\_avrcp\_ct\_cb\_t)([bk\_avrcp\_ct\_cb\_event\_t](#_CPPv422bk_avrcp_ct_cb_event_t "bk_avrcp_ct_cb_event_t") event, [bk\_avrcp\_ct\_cb\_param\_t](#_CPPv422bk_avrcp_ct_cb_param_t "bk_avrcp_ct_cb_param_t") \*param)
:   AVRCP controller callback function type.

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter union

<a id="_CPPv416bk_avrcp_tg_cb_t"></a>

<a id="_CPPv316bk_avrcp_tg_cb_t"></a> <a id="_CPPv216bk_avrcp_tg_cb_t"></a> <a id="bk_avrcp_tg_cb_t"></a> <a id="group__dm__avrcp__types_1gaa3776fe51bfabde4184b77b9e7138680"></a> typedef void (\*bk\_avrcp\_tg\_cb\_t)([bk\_avrcp\_tg\_cb\_event\_t](#_CPPv422bk_avrcp_tg_cb_event_t "bk_avrcp_tg_cb_event_t") event, [bk\_avrcp\_tg\_cb\_param\_t](#_CPPv422bk_avrcp_tg_cb_param_t "bk_avrcp_tg_cb_param_t") \*param)
:   AVRCP target callback function type.

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter union

<a id="id41"></a>

### Enumerations

<a id="_CPPv423bk_avrcp_rn_event_ids_t"></a>

<a id="_CPPv323bk_avrcp_rn_event_ids_t"></a> <a id="_CPPv223bk_avrcp_rn_event_ids_t"></a> <a id="group__dm__avrcp__types_1ga9f610ed41121b22c7e0da73deaacc2b4"></a> enum bk\_avrcp\_rn\_event\_ids\_t
:   AVRCP event notification ids.

    *Values:*

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t30BK_AVRCP_RN_PLAY_STATUS_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t30BK_AVRCP_RN_PLAY_STATUS_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t30BK_AVRCP_RN_PLAY_STATUS_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4a51f37ad1a62b2ba8ea12d7df77d9e3eb"></a> enumerator BK\_AVRCP\_RN\_PLAY\_STATUS\_CHANGE
    :   track status change, eg. from playing to paused

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t24BK_AVRCP_RN_TRACK_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t24BK_AVRCP_RN_TRACK_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t24BK_AVRCP_RN_TRACK_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4af5c4c294a36b5f0fdfa5c4a57f95fb80"></a> enumerator BK\_AVRCP\_RN\_TRACK\_CHANGE
    :   new track is loaded

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t29BK_AVRCP_RN_TRACK_REACHED_ENDE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t29BK_AVRCP_RN_TRACK_REACHED_ENDE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t29BK_AVRCP_RN_TRACK_REACHED_ENDE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4a91a2f67514018f1ea2718d7dca3d2ea9"></a> enumerator BK\_AVRCP\_RN\_TRACK\_REACHED\_END
    :   current track reached end

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t31BK_AVRCP_RN_TRACK_REACHED_STARTE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t31BK_AVRCP_RN_TRACK_REACHED_STARTE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t31BK_AVRCP_RN_TRACK_REACHED_STARTE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4aac65c06ee15b66ce751c9950c4c41efa"></a> enumerator BK\_AVRCP\_RN\_TRACK\_REACHED\_START
    :   current track reached start position

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t28BK_AVRCP_RN_PLAY_POS_CHANGEDE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t28BK_AVRCP_RN_PLAY_POS_CHANGEDE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t28BK_AVRCP_RN_PLAY_POS_CHANGEDE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4acb9e5ef96254c6e27917a2f3559d4be1"></a> enumerator BK\_AVRCP\_RN\_PLAY\_POS\_CHANGED
    :   track playing position changed

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t33BK_AVRCP_RN_BATTERY_STATUS_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t33BK_AVRCP_RN_BATTERY_STATUS_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t33BK_AVRCP_RN_BATTERY_STATUS_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4a5be43be4bec709e872b886404895a14c"></a> enumerator BK\_AVRCP\_RN\_BATTERY\_STATUS\_CHANGE
    :   battery status changed

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t32BK_AVRCP_RN_SYSTEM_STATUS_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t32BK_AVRCP_RN_SYSTEM_STATUS_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t32BK_AVRCP_RN_SYSTEM_STATUS_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4ade1b694f4b8c319cbdd42c3ed166185a"></a> enumerator BK\_AVRCP\_RN\_SYSTEM\_STATUS\_CHANGE
    :   system status changed

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t30BK_AVRCP_RN_APP_SETTING_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t30BK_AVRCP_RN_APP_SETTING_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t30BK_AVRCP_RN_APP_SETTING_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4a4faa93ed22abf30fce5f16f58a44431a"></a> enumerator BK\_AVRCP\_RN\_APP\_SETTING\_CHANGE
    :   application settings changed

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t30BK_AVRCP_RN_NOW_PLAYING_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t30BK_AVRCP_RN_NOW_PLAYING_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t30BK_AVRCP_RN_NOW_PLAYING_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4a9419cbd82937f75444a01273cb2a9384"></a> enumerator BK\_AVRCP\_RN\_NOW\_PLAYING\_CHANGE
    :   now playing content changed

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t36BK_AVRCP_RN_AVAILABLE_PLAYERS_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t36BK_AVRCP_RN_AVAILABLE_PLAYERS_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t36BK_AVRCP_RN_AVAILABLE_PLAYERS_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4a4a742e54dea35f71c6b537c55a3dc852"></a> enumerator BK\_AVRCP\_RN\_AVAILABLE\_PLAYERS\_CHANGE
    :   available players changed

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t35BK_AVRCP_RN_ADDRESSED_PLAYER_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t35BK_AVRCP_RN_ADDRESSED_PLAYER_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t35BK_AVRCP_RN_ADDRESSED_PLAYER_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4a89629d4ce833c585823025488f873c90"></a> enumerator BK\_AVRCP\_RN\_ADDRESSED\_PLAYER\_CHANGE
    :   the addressed player changed

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t23BK_AVRCP_RN_UIDS_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t23BK_AVRCP_RN_UIDS_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t23BK_AVRCP_RN_UIDS_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4aeafaeabcffea53bf2bec660722d074f6"></a> enumerator BK\_AVRCP\_RN\_UIDS\_CHANGE
    :   UIDs changed

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t25BK_AVRCP_RN_VOLUME_CHANGEE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t25BK_AVRCP_RN_VOLUME_CHANGEE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t25BK_AVRCP_RN_VOLUME_CHANGEE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4acb9a2787129aadd5ed1259142fd9cf65"></a> enumerator BK\_AVRCP\_RN\_VOLUME\_CHANGE
    :   volume changed locally on TG. Mandatory if BK\_AVRCP\_SDP\_FEATURE\_TG\_CAT\_2 is supported, Excluded otherwise

    <a id="_CPPv4N23bk_avrcp_rn_event_ids_t19BK_AVRCP_RN_MAX_EVTE"></a>

    <a id="_CPPv3N23bk_avrcp_rn_event_ids_t19BK_AVRCP_RN_MAX_EVTE"></a> <a id="_CPPv2N23bk_avrcp_rn_event_ids_t19BK_AVRCP_RN_MAX_EVTE"></a> <a id="group__dm__avrcp__types_1gga9f610ed41121b22c7e0da73deaacc2b4a2691df6d71f300710e13340695e9a767"></a> enumerator BK\_AVRCP\_RN\_MAX\_EVT

<a id="_CPPv422bk_avrcp_ct_cb_event_t"></a>

<a id="_CPPv322bk_avrcp_ct_cb_event_t"></a> <a id="_CPPv222bk_avrcp_ct_cb_event_t"></a> <a id="group__dm__avrcp__types_1gaa33191d1e57e846ceaf0e8abdaa8d1c0"></a> enum bk\_avrcp\_ct\_cb\_event\_t
:   AVRCP Controller callback events.

    *Values:*

    <a id="_CPPv4N22bk_avrcp_ct_cb_event_t32BK_AVRCP_CT_CONNECTION_STATE_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_event_t32BK_AVRCP_CT_CONNECTION_STATE_EVTE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_event_t32BK_AVRCP_CT_CONNECTION_STATE_EVTE"></a> <a id="group__dm__avrcp__types_1ggaa33191d1e57e846ceaf0e8abdaa8d1c0aa87a8c91b50434976ef87e7be6459442"></a> enumerator BK\_AVRCP\_CT\_CONNECTION\_STATE\_EVT
    :   connection state changed event

    <a id="_CPPv4N22bk_avrcp_ct_cb_event_t31BK_AVRCP_CT_PASSTHROUGH_RSP_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_event_t31BK_AVRCP_CT_PASSTHROUGH_RSP_EVTE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_event_t31BK_AVRCP_CT_PASSTHROUGH_RSP_EVTE"></a> <a id="group__dm__avrcp__types_1ggaa33191d1e57e846ceaf0e8abdaa8d1c0acb65eb943853e69dd3bad1ea71b21a00"></a> enumerator BK\_AVRCP\_CT\_PASSTHROUGH\_RSP\_EVT
    :   passthrough response event

    <a id="_CPPv4N22bk_avrcp_ct_cb_event_t33BK_AVRCP_CT_GET_ELEM_ATTR_RSP_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_event_t33BK_AVRCP_CT_GET_ELEM_ATTR_RSP_EVTE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_event_t33BK_AVRCP_CT_GET_ELEM_ATTR_RSP_EVTE"></a> <a id="group__dm__avrcp__types_1ggaa33191d1e57e846ceaf0e8abdaa8d1c0afd5f1516386989b657f789066d47aaf2"></a> enumerator BK\_AVRCP\_CT\_GET\_ELEM\_ATTR\_RSP\_EVT
    :   get elem attr response event

    <a id="_CPPv4N22bk_avrcp_ct_cb_event_t31BK_AVRCP_CT_PLAY_STATUS_RSP_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_event_t31BK_AVRCP_CT_PLAY_STATUS_RSP_EVTE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_event_t31BK_AVRCP_CT_PLAY_STATUS_RSP_EVTE"></a> <a id="group__dm__avrcp__types_1ggaa33191d1e57e846ceaf0e8abdaa8d1c0a77db166c0c5c467e4ce28c30621d384b"></a> enumerator BK\_AVRCP\_CT\_PLAY\_STATUS\_RSP\_EVT
    :   play status response event

    <a id="_CPPv4N22bk_avrcp_ct_cb_event_t29BK_AVRCP_CT_CHANGE_NOTIFY_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_event_t29BK_AVRCP_CT_CHANGE_NOTIFY_EVTE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_event_t29BK_AVRCP_CT_CHANGE_NOTIFY_EVTE"></a> <a id="group__dm__avrcp__types_1ggaa33191d1e57e846ceaf0e8abdaa8d1c0a430f301f662eac93af1d5e05cd3fb4fc"></a> enumerator BK\_AVRCP\_CT\_CHANGE\_NOTIFY\_EVT
    :   notification event

    <a id="_CPPv4N22bk_avrcp_ct_cb_event_t31BK_AVRCP_CT_REMOTE_FEATURES_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_event_t31BK_AVRCP_CT_REMOTE_FEATURES_EVTE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_event_t31BK_AVRCP_CT_REMOTE_FEATURES_EVTE"></a> <a id="group__dm__avrcp__types_1ggaa33191d1e57e846ceaf0e8abdaa8d1c0a60b68e2be5db5827becc9cd05d5136e8"></a> enumerator BK\_AVRCP\_CT\_REMOTE\_FEATURES\_EVT
    :   feature of remote device indication event

    <a id="_CPPv4N22bk_avrcp_ct_cb_event_t39BK_AVRCP_CT_GET_RN_CAPABILITIES_RSP_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_event_t39BK_AVRCP_CT_GET_RN_CAPABILITIES_RSP_EVTE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_event_t39BK_AVRCP_CT_GET_RN_CAPABILITIES_RSP_EVTE"></a> <a id="group__dm__avrcp__types_1ggaa33191d1e57e846ceaf0e8abdaa8d1c0aa07f2f7c12781a476755a5897ec47757"></a> enumerator BK\_AVRCP\_CT\_GET\_RN\_CAPABILITIES\_RSP\_EVT
    :   supported notification events capability of peer device

    <a id="_CPPv4N22bk_avrcp_ct_cb_event_t39BK_AVRCP_CT_SET_ABSOLUTE_VOLUME_RSP_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_event_t39BK_AVRCP_CT_SET_ABSOLUTE_VOLUME_RSP_EVTE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_event_t39BK_AVRCP_CT_SET_ABSOLUTE_VOLUME_RSP_EVTE"></a> <a id="group__dm__avrcp__types_1ggaa33191d1e57e846ceaf0e8abdaa8d1c0a99c8d02106c1e97b1e77f922b8a25406"></a> enumerator BK\_AVRCP\_CT\_SET\_ABSOLUTE\_VOLUME\_RSP\_EVT
    :   set absolute volume response event

    <a id="_CPPv4N22bk_avrcp_ct_cb_event_t42BK_AVRCP_CT_SET_PLAYER_APP_SETTING_RSP_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_ct_cb_event_t42BK_AVRCP_CT_SET_PLAYER_APP_SETTING_RSP_EVTE"></a> <a id="_CPPv2N22bk_avrcp_ct_cb_event_t42BK_AVRCP_CT_SET_PLAYER_APP_SETTING_RSP_EVTE"></a> <a id="group__dm__avrcp__types_1ggaa33191d1e57e846ceaf0e8abdaa8d1c0a95d834a34aa14adced9ff26fc7c948ce"></a> enumerator BK\_AVRCP\_CT\_SET\_PLAYER\_APP\_SETTING\_RSP\_EVT

<a id="_CPPv414bk_avrcp_rsp_t"></a>

<a id="_CPPv314bk_avrcp_rsp_t"></a> <a id="_CPPv214bk_avrcp_rsp_t"></a> <a id="group__dm__avrcp__types_1ga8f3af2776feebb89ae192e6ef7100c59"></a> enum bk\_avrcp\_rsp\_t
:   AVCTP response codes.

    *Values:*

    <a id="_CPPv4N14bk_avrcp_rsp_t21BK_AVRCP_RSP_NOT_IMPLE"></a>

    <a id="_CPPv3N14bk_avrcp_rsp_t21BK_AVRCP_RSP_NOT_IMPLE"></a> <a id="_CPPv2N14bk_avrcp_rsp_t21BK_AVRCP_RSP_NOT_IMPLE"></a> <a id="group__dm__avrcp__types_1gga8f3af2776feebb89ae192e6ef7100c59a90c8fc5fbe686f3022c76221ee848433"></a> enumerator BK\_AVRCP\_RSP\_NOT\_IMPL
    :   not implemented

    <a id="_CPPv4N14bk_avrcp_rsp_t19BK_AVRCP_RSP_ACCEPTE"></a>

    <a id="_CPPv3N14bk_avrcp_rsp_t19BK_AVRCP_RSP_ACCEPTE"></a> <a id="_CPPv2N14bk_avrcp_rsp_t19BK_AVRCP_RSP_ACCEPTE"></a> <a id="group__dm__avrcp__types_1gga8f3af2776feebb89ae192e6ef7100c59ab5a8dadd8591fc599e62222e3aa024a1"></a> enumerator BK\_AVRCP\_RSP\_ACCEPT
    :   accept

    <a id="_CPPv4N14bk_avrcp_rsp_t19BK_AVRCP_RSP_REJECTE"></a>

    <a id="_CPPv3N14bk_avrcp_rsp_t19BK_AVRCP_RSP_REJECTE"></a> <a id="_CPPv2N14bk_avrcp_rsp_t19BK_AVRCP_RSP_REJECTE"></a> <a id="group__dm__avrcp__types_1gga8f3af2776feebb89ae192e6ef7100c59a9797dec32a7dd7db504a290579ead629"></a> enumerator BK\_AVRCP\_RSP\_REJECT
    :   reject

    <a id="_CPPv4N14bk_avrcp_rsp_t21BK_AVRCP_RSP_IN_TRANSE"></a>

    <a id="_CPPv3N14bk_avrcp_rsp_t21BK_AVRCP_RSP_IN_TRANSE"></a> <a id="_CPPv2N14bk_avrcp_rsp_t21BK_AVRCP_RSP_IN_TRANSE"></a> <a id="group__dm__avrcp__types_1gga8f3af2776feebb89ae192e6ef7100c59ad86a42bfd9a397e19c8bf59de3e361a5"></a> enumerator BK\_AVRCP\_RSP\_IN\_TRANS
    :   in transition

    <a id="_CPPv4N14bk_avrcp_rsp_t22BK_AVRCP_RSP_IMPL_STBLE"></a>

    <a id="_CPPv3N14bk_avrcp_rsp_t22BK_AVRCP_RSP_IMPL_STBLE"></a> <a id="_CPPv2N14bk_avrcp_rsp_t22BK_AVRCP_RSP_IMPL_STBLE"></a> <a id="group__dm__avrcp__types_1gga8f3af2776feebb89ae192e6ef7100c59a9088c5bd37ecb77458a87d34ca6d1621"></a> enumerator BK\_AVRCP\_RSP\_IMPL\_STBL
    :   implemented/stable

    <a id="_CPPv4N14bk_avrcp_rsp_t20BK_AVRCP_RSP_CHANGEDE"></a>

    <a id="_CPPv3N14bk_avrcp_rsp_t20BK_AVRCP_RSP_CHANGEDE"></a> <a id="_CPPv2N14bk_avrcp_rsp_t20BK_AVRCP_RSP_CHANGEDE"></a> <a id="group__dm__avrcp__types_1gga8f3af2776feebb89ae192e6ef7100c59a881193c2cc7798ab80875f9a5432e1dd"></a> enumerator BK\_AVRCP\_RSP\_CHANGED
    :   changed

    <a id="_CPPv4N14bk_avrcp_rsp_t20BK_AVRCP_RSP_INTERIME"></a>

    <a id="_CPPv3N14bk_avrcp_rsp_t20BK_AVRCP_RSP_INTERIME"></a> <a id="_CPPv2N14bk_avrcp_rsp_t20BK_AVRCP_RSP_INTERIME"></a> <a id="group__dm__avrcp__types_1gga8f3af2776feebb89ae192e6ef7100c59aacc45f5e65584e023a35d7d61970a4a1"></a> enumerator BK\_AVRCP\_RSP\_INTERIM
    :   interim

<a id="_CPPv420bk_avrcp_batt_stat_t"></a>

<a id="_CPPv320bk_avrcp_batt_stat_t"></a> <a id="_CPPv220bk_avrcp_batt_stat_t"></a> <a id="group__dm__avrcp__types_1ga797447618ccc72cadc5acd07b04ce3dd"></a> enum bk\_avrcp\_batt\_stat\_t
:   AVRCP battery status.

    *Values:*

    <a id="_CPPv4N20bk_avrcp_batt_stat_t20BK_AVRCP_BATT_NORMALE"></a>

    <a id="_CPPv3N20bk_avrcp_batt_stat_t20BK_AVRCP_BATT_NORMALE"></a> <a id="_CPPv2N20bk_avrcp_batt_stat_t20BK_AVRCP_BATT_NORMALE"></a> <a id="group__dm__avrcp__types_1gga797447618ccc72cadc5acd07b04ce3dda253093c24586cbc2909e6dc774169bc8"></a> enumerator BK\_AVRCP\_BATT\_NORMAL
    :   normal state

    <a id="_CPPv4N20bk_avrcp_batt_stat_t21BK_AVRCP_BATT_WARNINGE"></a>

    <a id="_CPPv3N20bk_avrcp_batt_stat_t21BK_AVRCP_BATT_WARNINGE"></a> <a id="_CPPv2N20bk_avrcp_batt_stat_t21BK_AVRCP_BATT_WARNINGE"></a> <a id="group__dm__avrcp__types_1gga797447618ccc72cadc5acd07b04ce3ddaf7804f0a0b252ecfd3bf4e8c2d70beea"></a> enumerator BK\_AVRCP\_BATT\_WARNING
    :   unable to operate soon

    <a id="_CPPv4N20bk_avrcp_batt_stat_t22BK_AVRCP_BATT_CRITICALE"></a>

    <a id="_CPPv3N20bk_avrcp_batt_stat_t22BK_AVRCP_BATT_CRITICALE"></a> <a id="_CPPv2N20bk_avrcp_batt_stat_t22BK_AVRCP_BATT_CRITICALE"></a> <a id="group__dm__avrcp__types_1gga797447618ccc72cadc5acd07b04ce3dda342eae6c11af9d6aaded9566c5208782"></a> enumerator BK\_AVRCP\_BATT\_CRITICAL
    :   cannot operate any more

    <a id="_CPPv4N20bk_avrcp_batt_stat_t22BK_AVRCP_BATT_EXTERNALE"></a>

    <a id="_CPPv3N20bk_avrcp_batt_stat_t22BK_AVRCP_BATT_EXTERNALE"></a> <a id="_CPPv2N20bk_avrcp_batt_stat_t22BK_AVRCP_BATT_EXTERNALE"></a> <a id="group__dm__avrcp__types_1gga797447618ccc72cadc5acd07b04ce3dda7475438d3c30f276b125ead80f1817d4"></a> enumerator BK\_AVRCP\_BATT\_EXTERNAL
    :   plugged to external power supply

    <a id="_CPPv4N20bk_avrcp_batt_stat_t25BK_AVRCP_BATT_FULL_CHARGEE"></a>

    <a id="_CPPv3N20bk_avrcp_batt_stat_t25BK_AVRCP_BATT_FULL_CHARGEE"></a> <a id="_CPPv2N20bk_avrcp_batt_stat_t25BK_AVRCP_BATT_FULL_CHARGEE"></a> <a id="group__dm__avrcp__types_1gga797447618ccc72cadc5acd07b04ce3ddaabc59922d547b80f715dc265e6f82a17"></a> enumerator BK\_AVRCP\_BATT\_FULL\_CHARGE
    :   when completely charged from external power supply

<a id="_CPPv424bk_avrcp_playback_stat_t"></a>

<a id="_CPPv324bk_avrcp_playback_stat_t"></a> <a id="_CPPv224bk_avrcp_playback_stat_t"></a> <a id="group__dm__avrcp__types_1ga4f81825b1f00405e5a5694dea91b975c"></a> enum bk\_avrcp\_playback\_stat\_t
:   AVRCP current status of playback.

    *Values:*

    <a id="_CPPv4N24bk_avrcp_playback_stat_t25BK_AVRCP_PLAYBACK_STOPPEDE"></a>

    <a id="_CPPv3N24bk_avrcp_playback_stat_t25BK_AVRCP_PLAYBACK_STOPPEDE"></a> <a id="_CPPv2N24bk_avrcp_playback_stat_t25BK_AVRCP_PLAYBACK_STOPPEDE"></a> <a id="group__dm__avrcp__types_1gga4f81825b1f00405e5a5694dea91b975caea0a025a267b0b1a603f5da2891db30b"></a> enumerator BK\_AVRCP\_PLAYBACK\_STOPPED
    :   stopped

    <a id="_CPPv4N24bk_avrcp_playback_stat_t25BK_AVRCP_PLAYBACK_PLAYINGE"></a>

    <a id="_CPPv3N24bk_avrcp_playback_stat_t25BK_AVRCP_PLAYBACK_PLAYINGE"></a> <a id="_CPPv2N24bk_avrcp_playback_stat_t25BK_AVRCP_PLAYBACK_PLAYINGE"></a> <a id="group__dm__avrcp__types_1gga4f81825b1f00405e5a5694dea91b975ca72fc96ef5eb98035a6d4604e169426a5"></a> enumerator BK\_AVRCP\_PLAYBACK\_PLAYING
    :   playing

    <a id="_CPPv4N24bk_avrcp_playback_stat_t24BK_AVRCP_PLAYBACK_PAUSEDE"></a>

    <a id="_CPPv3N24bk_avrcp_playback_stat_t24BK_AVRCP_PLAYBACK_PAUSEDE"></a> <a id="_CPPv2N24bk_avrcp_playback_stat_t24BK_AVRCP_PLAYBACK_PAUSEDE"></a> <a id="group__dm__avrcp__types_1gga4f81825b1f00405e5a5694dea91b975ca8b7da446d4ee4a61c7ffaa144c378e69"></a> enumerator BK\_AVRCP\_PLAYBACK\_PAUSED
    :   paused

    <a id="_CPPv4N24bk_avrcp_playback_stat_t26BK_AVRCP_PLAYBACK_FWD_SEEKE"></a>

    <a id="_CPPv3N24bk_avrcp_playback_stat_t26BK_AVRCP_PLAYBACK_FWD_SEEKE"></a> <a id="_CPPv2N24bk_avrcp_playback_stat_t26BK_AVRCP_PLAYBACK_FWD_SEEKE"></a> <a id="group__dm__avrcp__types_1gga4f81825b1f00405e5a5694dea91b975ca76c71c7aefeb9835aa79d354324b6175"></a> enumerator BK\_AVRCP\_PLAYBACK\_FWD\_SEEK
    :   forward seek

    <a id="_CPPv4N24bk_avrcp_playback_stat_t26BK_AVRCP_PLAYBACK_REV_SEEKE"></a>

    <a id="_CPPv3N24bk_avrcp_playback_stat_t26BK_AVRCP_PLAYBACK_REV_SEEKE"></a> <a id="_CPPv2N24bk_avrcp_playback_stat_t26BK_AVRCP_PLAYBACK_REV_SEEKE"></a> <a id="group__dm__avrcp__types_1gga4f81825b1f00405e5a5694dea91b975caa17fdc49adf06050ea078ab34458c66e"></a> enumerator BK\_AVRCP\_PLAYBACK\_REV\_SEEK
    :   reverse seek

    <a id="_CPPv4N24bk_avrcp_playback_stat_t23BK_AVRCP_PLAYBACK_ERRORE"></a>

    <a id="_CPPv3N24bk_avrcp_playback_stat_t23BK_AVRCP_PLAYBACK_ERRORE"></a> <a id="_CPPv2N24bk_avrcp_playback_stat_t23BK_AVRCP_PLAYBACK_ERRORE"></a> <a id="group__dm__avrcp__types_1gga4f81825b1f00405e5a5694dea91b975ca033f405d46b82f5e5d49c2c6f41ff20c"></a> enumerator BK\_AVRCP\_PLAYBACK\_ERROR
    :   error

<a id="_CPPv417bk_avrcp_pt_cmd_t"></a>

<a id="_CPPv317bk_avrcp_pt_cmd_t"></a> <a id="_CPPv217bk_avrcp_pt_cmd_t"></a> <a id="group__dm__avrcp__types_1gae780de89845d9801b3ec7fd06bc5d701"></a> enum bk\_avrcp\_pt\_cmd\_t
:   AVRCP passthrough command code.

    *Values:*

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_SELECTE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_SELECTE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_SELECTE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a84bd40bb4a123d498aa57489acff71b5"></a> enumerator BK\_AVRCP\_PT\_CMD\_SELECT
    :   select

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_UPE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_UPE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_UPE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a3146314ce4fff6c9247abb7f7000a7a9"></a> enumerator BK\_AVRCP\_PT\_CMD\_UP
    :   up

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_DOWNE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_DOWNE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_DOWNE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701af5a04527adce945c2dff044e2e518413"></a> enumerator BK\_AVRCP\_PT\_CMD\_DOWN
    :   down

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_LEFTE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_LEFTE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_LEFTE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a0dca3356100bda0daaa116e4b7bcd19a"></a> enumerator BK\_AVRCP\_PT\_CMD\_LEFT
    :   left

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_RIGHTE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_RIGHTE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_RIGHTE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701aafe5a1447b374ddd1bb6aec86d057217"></a> enumerator BK\_AVRCP\_PT\_CMD\_RIGHT
    :   right

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_RIGHT_UPE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_RIGHT_UPE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_RIGHT_UPE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ad957ab2f3bbd5d406f1ddea0a3e10f21"></a> enumerator BK\_AVRCP\_PT\_CMD\_RIGHT\_UP
    :   right-up

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t26BK_AVRCP_PT_CMD_RIGHT_DOWNE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t26BK_AVRCP_PT_CMD_RIGHT_DOWNE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t26BK_AVRCP_PT_CMD_RIGHT_DOWNE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a50937cac078d4e3b9cd02129e8b0c2b9"></a> enumerator BK\_AVRCP\_PT\_CMD\_RIGHT\_DOWN
    :   right-down

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_LEFT_UPE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_LEFT_UPE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_LEFT_UPE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a8bbcb7b3797bec056d418161801023bd"></a> enumerator BK\_AVRCP\_PT\_CMD\_LEFT\_UP
    :   left-up

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_LEFT_DOWNE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_LEFT_DOWNE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_LEFT_DOWNE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a0154b4ad991696b29d4178b250f545f3"></a> enumerator BK\_AVRCP\_PT\_CMD\_LEFT\_DOWN
    :   left-down

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_ROOT_MENUE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_ROOT_MENUE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_ROOT_MENUE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701af83ce89a77c8763127f8c0c8e15a8dd5"></a> enumerator BK\_AVRCP\_PT\_CMD\_ROOT\_MENU
    :   root menu

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t26BK_AVRCP_PT_CMD_SETUP_MENUE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t26BK_AVRCP_PT_CMD_SETUP_MENUE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t26BK_AVRCP_PT_CMD_SETUP_MENUE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ac5ee19d87dd5adadeda96b9e86673d1a"></a> enumerator BK\_AVRCP\_PT\_CMD\_SETUP\_MENU
    :   setup menu

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_CONT_MENUE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_CONT_MENUE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_CONT_MENUE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a7001b5ed6defcba0e7d73c18c50a746c"></a> enumerator BK\_AVRCP\_PT\_CMD\_CONT\_MENU
    :   contents menu

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_FAV_MENUE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_FAV_MENUE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_FAV_MENUE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a8865092bf33f48f8d2d3f551a07c7f01"></a> enumerator BK\_AVRCP\_PT\_CMD\_FAV\_MENU
    :   favorite menu

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_EXITE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_EXITE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_EXITE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701aab48a86dff326d5d39f24c6c833ec286"></a> enumerator BK\_AVRCP\_PT\_CMD\_EXIT
    :   exit

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_0E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_0E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_0E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701aad4f990b86227490bac3c71191a3aca7"></a> enumerator BK\_AVRCP\_PT\_CMD\_0
    :   0

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_1E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_1E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_1E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ab7868003d706a323c6d68d5acfed5a8c"></a> enumerator BK\_AVRCP\_PT\_CMD\_1
    :   1

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_2E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_2E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_2E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a033b5186f3e1ed6b75bd90b10afe4a88"></a> enumerator BK\_AVRCP\_PT\_CMD\_2
    :   2

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_3E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_3E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_3E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a185b0d5e57cfbcb49b4a7e624d0676fc"></a> enumerator BK\_AVRCP\_PT\_CMD\_3
    :   3

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_4E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_4E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_4E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ad885fcf8d2f8ea242e87d0fbad1fce5f"></a> enumerator BK\_AVRCP\_PT\_CMD\_4
    :   4

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_5E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_5E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_5E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a39485cc3bca8d3d72c58450a2b420d4f"></a> enumerator BK\_AVRCP\_PT\_CMD\_5
    :   5

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_6E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_6E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_6E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a151fb9c4fa0a23eafc3fa5044e6645ed"></a> enumerator BK\_AVRCP\_PT\_CMD\_6
    :   6

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_7E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_7E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_7E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701af2054c7e21d07fb5d59c1c8b7d007cd4"></a> enumerator BK\_AVRCP\_PT\_CMD\_7
    :   7

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_8E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_8E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_8E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a70f4f117693c49ddf4132c197ca30d83"></a> enumerator BK\_AVRCP\_PT\_CMD\_8
    :   8

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_9E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_9E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t17BK_AVRCP_PT_CMD_9E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a47ea1b5f1334bb5495730cc2fd1d6399"></a> enumerator BK\_AVRCP\_PT\_CMD\_9
    :   9

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t19BK_AVRCP_PT_CMD_DOTE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t19BK_AVRCP_PT_CMD_DOTE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t19BK_AVRCP_PT_CMD_DOTE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a13a2751cd92dde88045f8fc09df8351f"></a> enumerator BK\_AVRCP\_PT\_CMD\_DOT
    :   dot

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_ENTERE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_ENTERE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_ENTERE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a349a86cb9d0efa0f7c690d55a23b910d"></a> enumerator BK\_AVRCP\_PT\_CMD\_ENTER
    :   enter

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_CLEARE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_CLEARE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_CLEARE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ab8729b06212e30e4ad33eca88be3fc60"></a> enumerator BK\_AVRCP\_PT\_CMD\_CLEAR
    :   clear

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_CHAN_UPE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_CHAN_UPE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_CHAN_UPE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a5c2ffd072684bdc40299ba16f0f9b861"></a> enumerator BK\_AVRCP\_PT\_CMD\_CHAN\_UP
    :   channel up

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_CHAN_DOWNE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_CHAN_DOWNE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_CHAN_DOWNE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a7497d7e0375648637a6ba5e4ff62cf46"></a> enumerator BK\_AVRCP\_PT\_CMD\_CHAN\_DOWN
    :   channel down

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_PREV_CHANE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_PREV_CHANE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_PREV_CHANE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701af8b9f935fb7c9b22bf5a8c362fc2468f"></a> enumerator BK\_AVRCP\_PT\_CMD\_PREV\_CHAN
    :   previous channel

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_SOUND_SELE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_SOUND_SELE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_SOUND_SELE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701adba3442b8c38eeeed58da19c0ffcf61f"></a> enumerator BK\_AVRCP\_PT\_CMD\_SOUND\_SEL
    :   sound select

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_INPUT_SELE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_INPUT_SELE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_INPUT_SELE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a70ea29cb1a105c2f69e4ea6694da2d56"></a> enumerator BK\_AVRCP\_PT\_CMD\_INPUT\_SEL
    :   input select

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_DISP_INFOE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_DISP_INFOE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_DISP_INFOE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a2b95d281c0cf36d53e1a4183ec7388dc"></a> enumerator BK\_AVRCP\_PT\_CMD\_DISP\_INFO
    :   display information

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_HELPE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_HELPE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_HELPE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a2cf3a272caa073447fc8712608efb837"></a> enumerator BK\_AVRCP\_PT\_CMD\_HELP
    :   help

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_PAGE_UPE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_PAGE_UPE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_PAGE_UPE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ad2645a23031264ed5c3ba10eb00f4604"></a> enumerator BK\_AVRCP\_PT\_CMD\_PAGE\_UP
    :   page up

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_PAGE_DOWNE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_PAGE_DOWNE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t25BK_AVRCP_PT_CMD_PAGE_DOWNE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a55a3318f848ca012897d6e76ab3b370c"></a> enumerator BK\_AVRCP\_PT\_CMD\_PAGE\_DOWN
    :   page down

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_POWERE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_POWERE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_POWERE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ab247eb05286afec0482665a6c7f0a91f"></a> enumerator BK\_AVRCP\_PT\_CMD\_POWER
    :   power

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_VOL_UPE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_VOL_UPE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_VOL_UPE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a5654e9e729e66bd3c2d0e27eca7bc963"></a> enumerator BK\_AVRCP\_PT\_CMD\_VOL\_UP
    :   volume up

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_VOL_DOWNE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_VOL_DOWNE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_VOL_DOWNE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a712afd017c4246b7052778de7d5f61b0"></a> enumerator BK\_AVRCP\_PT\_CMD\_VOL\_DOWN
    :   volume down

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_MUTEE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_MUTEE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_MUTEE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a871707c5039cb6a245547ff4db7c2f87"></a> enumerator BK\_AVRCP\_PT\_CMD\_MUTE
    :   mute

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_PLAYE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_PLAYE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_PLAYE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a06f284a1284901c5312256de851d6625"></a> enumerator BK\_AVRCP\_PT\_CMD\_PLAY
    :   play

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_STOPE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_STOPE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t20BK_AVRCP_PT_CMD_STOPE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a0fa51cd5a691df1607ef76476d2286ba"></a> enumerator BK\_AVRCP\_PT\_CMD\_STOP
    :   stop

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_PAUSEE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_PAUSEE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_PAUSEE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a89cefcd216afa2ebf0efb58fc7369c2a"></a> enumerator BK\_AVRCP\_PT\_CMD\_PAUSE
    :   pause

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_RECORDE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_RECORDE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_RECORDE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a437138a84b3bebc750e456ee2c581c78"></a> enumerator BK\_AVRCP\_PT\_CMD\_RECORD
    :   record

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_REWINDE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_REWINDE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_REWINDE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a62dfaa4d5b05cbf0057737db6c5f90ab"></a> enumerator BK\_AVRCP\_PT\_CMD\_REWIND
    :   rewind

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t28BK_AVRCP_PT_CMD_FAST_FORWARDE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t28BK_AVRCP_PT_CMD_FAST_FORWARDE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t28BK_AVRCP_PT_CMD_FAST_FORWARDE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ab2e59598f6fbf72fb874d6e77c4ef5b7"></a> enumerator BK\_AVRCP\_PT\_CMD\_FAST\_FORWARD
    :   fast forward

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_EJECTE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_EJECTE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_EJECTE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a3819f5026b92ab980a1ccd3a4ef6e8de"></a> enumerator BK\_AVRCP\_PT\_CMD\_EJECT
    :   eject

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_FORWARDE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_FORWARDE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_FORWARDE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a03a3364e715c7b50de594a2e18841bfd"></a> enumerator BK\_AVRCP\_PT\_CMD\_FORWARD
    :   forward

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_BACKWARDE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_BACKWARDE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t24BK_AVRCP_PT_CMD_BACKWARDE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a51dbedcf7abe4898f0b092d3bc9946d4"></a> enumerator BK\_AVRCP\_PT\_CMD\_BACKWARD
    :   backward

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_ANGLEE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_ANGLEE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t21BK_AVRCP_PT_CMD_ANGLEE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a2bc359a7fb33172fdaf9bdd287a5b0f9"></a> enumerator BK\_AVRCP\_PT\_CMD\_ANGLE
    :   angle

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_SUBPICTE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_SUBPICTE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t23BK_AVRCP_PT_CMD_SUBPICTE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a79a9940b3ff2277c6b5f9de4aab51dfd"></a> enumerator BK\_AVRCP\_PT\_CMD\_SUBPICT
    :   subpicture

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F1E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F1E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F1E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ac2acfbe7b471e25ab3b61b6b472deb29"></a> enumerator BK\_AVRCP\_PT\_CMD\_F1
    :   F1

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F2E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F2E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F2E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a69244e76bc7df5da599d774796b3ba35"></a> enumerator BK\_AVRCP\_PT\_CMD\_F2
    :   F2

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F3E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F3E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F3E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a6bc408b354e1b82ca21ac9732a540d38"></a> enumerator BK\_AVRCP\_PT\_CMD\_F3
    :   F3

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F4E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F4E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F4E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701a9df2a81304fa45d4364bbb1ac24624d3"></a> enumerator BK\_AVRCP\_PT\_CMD\_F4
    :   F4

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F5E"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F5E"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t18BK_AVRCP_PT_CMD_F5E"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701acdbe88ffc728ec79cf2adbe4076706ae"></a> enumerator BK\_AVRCP\_PT\_CMD\_F5
    :   F5

    <a id="_CPPv4N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_VENDORE"></a>

    <a id="_CPPv3N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_VENDORE"></a> <a id="_CPPv2N17bk_avrcp_pt_cmd_t22BK_AVRCP_PT_CMD_VENDORE"></a> <a id="group__dm__avrcp__types_1ggae780de89845d9801b3ec7fd06bc5d701ab10e5cbf2f3e313508f9376638d838c4"></a> enumerator BK\_AVRCP\_PT\_CMD\_VENDOR
    :   vendor unique

<a id="_CPPv423bk_avrcp_pt_cmd_state_t"></a>

<a id="_CPPv323bk_avrcp_pt_cmd_state_t"></a> <a id="_CPPv223bk_avrcp_pt_cmd_state_t"></a> <a id="group__dm__avrcp__types_1gab0f385b4e01d0e06e8692d98d163729a"></a> enum bk\_avrcp\_pt\_cmd\_state\_t
:   AVRCP passthrough command state.

    *Values:*

    <a id="_CPPv4N23bk_avrcp_pt_cmd_state_t29BK_AVRCP_PT_CMD_STATE_PRESSEDE"></a>

    <a id="_CPPv3N23bk_avrcp_pt_cmd_state_t29BK_AVRCP_PT_CMD_STATE_PRESSEDE"></a> <a id="_CPPv2N23bk_avrcp_pt_cmd_state_t29BK_AVRCP_PT_CMD_STATE_PRESSEDE"></a> <a id="group__dm__avrcp__types_1ggab0f385b4e01d0e06e8692d98d163729aa7a75b1f2754e0f7f98837b8ac4f50efe"></a> enumerator BK\_AVRCP\_PT\_CMD\_STATE\_PRESSED
    :   key pressed

    <a id="_CPPv4N23bk_avrcp_pt_cmd_state_t30BK_AVRCP_PT_CMD_STATE_RELEASEDE"></a>

    <a id="_CPPv3N23bk_avrcp_pt_cmd_state_t30BK_AVRCP_PT_CMD_STATE_RELEASEDE"></a> <a id="_CPPv2N23bk_avrcp_pt_cmd_state_t30BK_AVRCP_PT_CMD_STATE_RELEASEDE"></a> <a id="group__dm__avrcp__types_1ggab0f385b4e01d0e06e8692d98d163729aa8172ad7165b28713f66a1ddab8ef336b"></a> enumerator BK\_AVRCP\_PT\_CMD\_STATE\_RELEASED
    :   key released

<a id="_CPPv424bk_avrcp_media_attr_id_t"></a>

<a id="_CPPv324bk_avrcp_media_attr_id_t"></a> <a id="_CPPv224bk_avrcp_media_attr_id_t"></a> <a id="group__dm__avrcp__types_1gaf4e53e16beabd80e55bb7af4720e8830"></a> enum bk\_avrcp\_media\_attr\_id\_t
:   AVRC media attribute id.

    *Values:*

    <a id="_CPPv4N24bk_avrcp_media_attr_id_t28BK_AVRCP_MEDIA_ATTR_ID_TITLEE"></a>

    <a id="_CPPv3N24bk_avrcp_media_attr_id_t28BK_AVRCP_MEDIA_ATTR_ID_TITLEE"></a> <a id="_CPPv2N24bk_avrcp_media_attr_id_t28BK_AVRCP_MEDIA_ATTR_ID_TITLEE"></a> <a id="group__dm__avrcp__types_1ggaf4e53e16beabd80e55bb7af4720e8830aa6eac1770abb8361cd6df79013aac0f9"></a> enumerator BK\_AVRCP\_MEDIA\_ATTR\_ID\_TITLE
    :   title of the playing track

    <a id="_CPPv4N24bk_avrcp_media_attr_id_t29BK_AVRCP_MEDIA_ATTR_ID_ARTISTE"></a>

    <a id="_CPPv3N24bk_avrcp_media_attr_id_t29BK_AVRCP_MEDIA_ATTR_ID_ARTISTE"></a> <a id="_CPPv2N24bk_avrcp_media_attr_id_t29BK_AVRCP_MEDIA_ATTR_ID_ARTISTE"></a> <a id="group__dm__avrcp__types_1ggaf4e53e16beabd80e55bb7af4720e8830a5e74ee36a077dae71124b45f777cc2da"></a> enumerator BK\_AVRCP\_MEDIA\_ATTR\_ID\_ARTIST
    :   track artist

    <a id="_CPPv4N24bk_avrcp_media_attr_id_t28BK_AVRCP_MEDIA_ATTR_ID_ALBUME"></a>

    <a id="_CPPv3N24bk_avrcp_media_attr_id_t28BK_AVRCP_MEDIA_ATTR_ID_ALBUME"></a> <a id="_CPPv2N24bk_avrcp_media_attr_id_t28BK_AVRCP_MEDIA_ATTR_ID_ALBUME"></a> <a id="group__dm__avrcp__types_1ggaf4e53e16beabd80e55bb7af4720e8830a8e3aa69f35f334c1849284cbb543f2b1"></a> enumerator BK\_AVRCP\_MEDIA\_ATTR\_ID\_ALBUM
    :   album name

    <a id="_CPPv4N24bk_avrcp_media_attr_id_t32BK_AVRCP_MEDIA_ATTR_ID_TRACK_NUME"></a>

    <a id="_CPPv3N24bk_avrcp_media_attr_id_t32BK_AVRCP_MEDIA_ATTR_ID_TRACK_NUME"></a> <a id="_CPPv2N24bk_avrcp_media_attr_id_t32BK_AVRCP_MEDIA_ATTR_ID_TRACK_NUME"></a> <a id="group__dm__avrcp__types_1ggaf4e53e16beabd80e55bb7af4720e8830abcb89efa3ecef3aeac9f4e280998fd53"></a> enumerator BK\_AVRCP\_MEDIA\_ATTR\_ID\_TRACK\_NUM
    :   track position on the album

    <a id="_CPPv4N24bk_avrcp_media_attr_id_t33BK_AVRCP_MEDIA_ATTR_ID_NUM_TRACKSE"></a>

    <a id="_CPPv3N24bk_avrcp_media_attr_id_t33BK_AVRCP_MEDIA_ATTR_ID_NUM_TRACKSE"></a> <a id="_CPPv2N24bk_avrcp_media_attr_id_t33BK_AVRCP_MEDIA_ATTR_ID_NUM_TRACKSE"></a> <a id="group__dm__avrcp__types_1ggaf4e53e16beabd80e55bb7af4720e8830a2eac68bd647c3b8c738cdd057f60dad9"></a> enumerator BK\_AVRCP\_MEDIA\_ATTR\_ID\_NUM\_TRACKS
    :   number of tracks on the album

    <a id="_CPPv4N24bk_avrcp_media_attr_id_t28BK_AVRCP_MEDIA_ATTR_ID_GENREE"></a>

    <a id="_CPPv3N24bk_avrcp_media_attr_id_t28BK_AVRCP_MEDIA_ATTR_ID_GENREE"></a> <a id="_CPPv2N24bk_avrcp_media_attr_id_t28BK_AVRCP_MEDIA_ATTR_ID_GENREE"></a> <a id="group__dm__avrcp__types_1ggaf4e53e16beabd80e55bb7af4720e8830a938614fd58b4b8c6699a93931e3ac347"></a> enumerator BK\_AVRCP\_MEDIA\_ATTR\_ID\_GENRE
    :   track genre

    <a id="_CPPv4N24bk_avrcp_media_attr_id_t35BK_AVRCP_MEDIA_ATTR_ID_PLAYING_TIMEE"></a>

    <a id="_CPPv3N24bk_avrcp_media_attr_id_t35BK_AVRCP_MEDIA_ATTR_ID_PLAYING_TIMEE"></a> <a id="_CPPv2N24bk_avrcp_media_attr_id_t35BK_AVRCP_MEDIA_ATTR_ID_PLAYING_TIMEE"></a> <a id="group__dm__avrcp__types_1ggaf4e53e16beabd80e55bb7af4720e8830abc77adeac422024818b8e4b2d99f0b2f"></a> enumerator BK\_AVRCP\_MEDIA\_ATTR\_ID\_PLAYING\_TIME
    :   total album playing time in miliseconds

    <a id="_CPPv4N24bk_avrcp_media_attr_id_t40BK_AVRCP_MEDIA_ATTR_ID_DEFAULT_COVER_ARTE"></a>

    <a id="_CPPv3N24bk_avrcp_media_attr_id_t40BK_AVRCP_MEDIA_ATTR_ID_DEFAULT_COVER_ARTE"></a> <a id="_CPPv2N24bk_avrcp_media_attr_id_t40BK_AVRCP_MEDIA_ATTR_ID_DEFAULT_COVER_ARTE"></a> <a id="group__dm__avrcp__types_1ggaf4e53e16beabd80e55bb7af4720e8830af7ce87e49c5f53b79034bf67f72cd131"></a> enumerator BK\_AVRCP\_MEDIA\_ATTR\_ID\_DEFAULT\_COVER\_ART

<a id="_CPPv422bk_avrcp_ps_attr_ids_t"></a>

<a id="_CPPv322bk_avrcp_ps_attr_ids_t"></a> <a id="_CPPv222bk_avrcp_ps_attr_ids_t"></a> <a id="group__dm__avrcp__types_1gaa591c579433c3dd16370af0376495809"></a> enum bk\_avrcp\_ps\_attr\_ids\_t
:   AVRC player setting ids.

    *Values:*

    <a id="_CPPv4N22bk_avrcp_ps_attr_ids_t21BK_AVRCP_PS_EQUALIZERE"></a>

    <a id="_CPPv3N22bk_avrcp_ps_attr_ids_t21BK_AVRCP_PS_EQUALIZERE"></a> <a id="_CPPv2N22bk_avrcp_ps_attr_ids_t21BK_AVRCP_PS_EQUALIZERE"></a> <a id="group__dm__avrcp__types_1ggaa591c579433c3dd16370af0376495809afd63bd77e7e52840ae6999da7dbc96a6"></a> enumerator BK\_AVRCP\_PS\_EQUALIZER
    :   equalizer, on or off

    <a id="_CPPv4N22bk_avrcp_ps_attr_ids_t23BK_AVRCP_PS_REPEAT_MODEE"></a>

    <a id="_CPPv3N22bk_avrcp_ps_attr_ids_t23BK_AVRCP_PS_REPEAT_MODEE"></a> <a id="_CPPv2N22bk_avrcp_ps_attr_ids_t23BK_AVRCP_PS_REPEAT_MODEE"></a> <a id="group__dm__avrcp__types_1ggaa591c579433c3dd16370af0376495809acb61b41830e1e3b4e8bd4be359bf4cf2"></a> enumerator BK\_AVRCP\_PS\_REPEAT\_MODE
    :   repeat mode

    <a id="_CPPv4N22bk_avrcp_ps_attr_ids_t24BK_AVRCP_PS_SHUFFLE_MODEE"></a>

    <a id="_CPPv3N22bk_avrcp_ps_attr_ids_t24BK_AVRCP_PS_SHUFFLE_MODEE"></a> <a id="_CPPv2N22bk_avrcp_ps_attr_ids_t24BK_AVRCP_PS_SHUFFLE_MODEE"></a> <a id="group__dm__avrcp__types_1ggaa591c579433c3dd16370af0376495809a3329833142b8b358726198f634d10cf9"></a> enumerator BK\_AVRCP\_PS\_SHUFFLE\_MODE
    :   shuffle mode

    <a id="_CPPv4N22bk_avrcp_ps_attr_ids_t21BK_AVRCP_PS_SCAN_MODEE"></a>

    <a id="_CPPv3N22bk_avrcp_ps_attr_ids_t21BK_AVRCP_PS_SCAN_MODEE"></a> <a id="_CPPv2N22bk_avrcp_ps_attr_ids_t21BK_AVRCP_PS_SCAN_MODEE"></a> <a id="group__dm__avrcp__types_1ggaa591c579433c3dd16370af0376495809a1b7259212e9614b06db988975a09c7e4"></a> enumerator BK\_AVRCP\_PS\_SCAN\_MODE
    :   scan mode on or off

    <a id="_CPPv4N22bk_avrcp_ps_attr_ids_t20BK_AVRCP_PS_MAX_ATTRE"></a>

    <a id="_CPPv3N22bk_avrcp_ps_attr_ids_t20BK_AVRCP_PS_MAX_ATTRE"></a> <a id="_CPPv2N22bk_avrcp_ps_attr_ids_t20BK_AVRCP_PS_MAX_ATTRE"></a> <a id="group__dm__avrcp__types_1ggaa591c579433c3dd16370af0376495809a8406970ef92bf96d9ea4a70af2de7461"></a> enumerator BK\_AVRCP\_PS\_MAX\_ATTR

<a id="_CPPv433bk_avrcp_sdp_feature_api_method_t"></a>

<a id="_CPPv333bk_avrcp_sdp_feature_api_method_t"></a> <a id="_CPPv233bk_avrcp_sdp_feature_api_method_t"></a> <a id="group__dm__avrcp__types_1gae5b281f501193bb8ecbdb818a4f6b96e"></a> enum bk\_avrcp\_sdp\_feature\_api\_method\_t
:   AVRCP sdp feature method.

    *Values:*

    <a id="_CPPv4N33bk_avrcp_sdp_feature_api_method_t43BK_AVRCP_SDP_FEATURE_API_METHOD_GET_ALLOWEDE"></a>

    <a id="_CPPv3N33bk_avrcp_sdp_feature_api_method_t43BK_AVRCP_SDP_FEATURE_API_METHOD_GET_ALLOWEDE"></a> <a id="_CPPv2N33bk_avrcp_sdp_feature_api_method_t43BK_AVRCP_SDP_FEATURE_API_METHOD_GET_ALLOWEDE"></a> <a id="group__dm__avrcp__types_1ggae5b281f501193bb8ecbdb818a4f6b96ea30c6881f1eaf7321aaef00c7a14b2bd9"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_API\_METHOD\_GET\_ALLOWED
    :   all of the feature that can possibly be supported, immutable

    <a id="_CPPv4N33bk_avrcp_sdp_feature_api_method_t50BK_AVRCP_SDP_FEATURE_API_METHOD_GET_CURRENT_ENABLEE"></a>

    <a id="_CPPv3N33bk_avrcp_sdp_feature_api_method_t50BK_AVRCP_SDP_FEATURE_API_METHOD_GET_CURRENT_ENABLEE"></a> <a id="_CPPv2N33bk_avrcp_sdp_feature_api_method_t50BK_AVRCP_SDP_FEATURE_API_METHOD_GET_CURRENT_ENABLEE"></a> <a id="group__dm__avrcp__types_1ggae5b281f501193bb8ecbdb818a4f6b96ea0cc292739a5b6903c2bfb711db284175"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_API\_METHOD\_GET\_CURRENT\_ENABLE
    :   feature selectively supported according to the current configuration

    <a id="_CPPv4N33bk_avrcp_sdp_feature_api_method_t35BK_AVRCP_SDP_FEATURE_API_METHOD_SETE"></a>

    <a id="_CPPv3N33bk_avrcp_sdp_feature_api_method_t35BK_AVRCP_SDP_FEATURE_API_METHOD_SETE"></a> <a id="_CPPv2N33bk_avrcp_sdp_feature_api_method_t35BK_AVRCP_SDP_FEATURE_API_METHOD_SETE"></a> <a id="group__dm__avrcp__types_1ggae5b281f501193bb8ecbdb818a4f6b96ea28ec3dfb36921362c17156f6652864c2"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_API\_METHOD\_SET

    <a id="_CPPv4N33bk_avrcp_sdp_feature_api_method_t35BK_AVRCP_SDP_FEATURE_API_METHOD_MAXE"></a>

    <a id="_CPPv3N33bk_avrcp_sdp_feature_api_method_t35BK_AVRCP_SDP_FEATURE_API_METHOD_MAXE"></a> <a id="_CPPv2N33bk_avrcp_sdp_feature_api_method_t35BK_AVRCP_SDP_FEATURE_API_METHOD_MAXE"></a> <a id="group__dm__avrcp__types_1ggae5b281f501193bb8ecbdb818a4f6b96ea23ae4d097baaf9f5ff19016ca92d19f4"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_API\_METHOD\_MAX

<a id="_CPPv422bk_avrcp_sdp_feature_t"></a>

<a id="_CPPv322bk_avrcp_sdp_feature_t"></a> <a id="_CPPv222bk_avrcp_sdp_feature_t"></a> <a id="group__dm__avrcp__types_1ga21f9b8c44b15560a34b4f59cc1475a43"></a> enum bk\_avrcp\_sdp\_feature\_t
:   AVRCP sdp feature.

    *Values:*

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_1E"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_1E"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_1E"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43af88a5bb74db194cd91db8eede75117d1"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_CT\_CAT\_1

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_2E"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_2E"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_2E"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43a1309f5045259f1caecac0864a3d72e8e"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_CT\_CAT\_2

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_3E"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_3E"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_3E"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43a990d58a4a5f8c9baf162c127891663cb"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_CT\_CAT\_3

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_4E"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_4E"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_CT_CAT_4E"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43a633134d1f66317b0c207da8d98dad0e2"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_CT\_CAT\_4

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t40BK_AVRCP_SDP_FEATURE_CT_SUPPORT_BROWSINGE"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t40BK_AVRCP_SDP_FEATURE_CT_SUPPORT_BROWSINGE"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t40BK_AVRCP_SDP_FEATURE_CT_SUPPORT_BROWSINGE"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43ad4a502961a140c9e885001280c84f678"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_CT\_SUPPORT\_BROWSING

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t38BK_AVRCP_SDP_FEATURE_CT_SUPPORT_CA_GIPE"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t38BK_AVRCP_SDP_FEATURE_CT_SUPPORT_CA_GIPE"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t38BK_AVRCP_SDP_FEATURE_CT_SUPPORT_CA_GIPE"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43ac472508af8dbfd2ad20897a83d72f0b3"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_CT\_SUPPORT\_CA\_GIP

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t37BK_AVRCP_SDP_FEATURE_CT_SUPPORT_CA_GIE"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t37BK_AVRCP_SDP_FEATURE_CT_SUPPORT_CA_GIE"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t37BK_AVRCP_SDP_FEATURE_CT_SUPPORT_CA_GIE"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43af6844487518f04b01be33965010d0241"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_CT\_SUPPORT\_CA\_GI

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t38BK_AVRCP_SDP_FEATURE_CT_SUPPORT_CA_GLTE"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t38BK_AVRCP_SDP_FEATURE_CT_SUPPORT_CA_GLTE"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t38BK_AVRCP_SDP_FEATURE_CT_SUPPORT_CA_GLTE"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43a8476be13545fa7f343ab3fb620a106a6"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_CT\_SUPPORT\_CA\_GLT

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_1E"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_1E"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_1E"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43aa2fc0b97c385289b75c9001528fc0976"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_TG\_CAT\_1

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_2E"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_2E"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_2E"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43aac4437205fd37749700e489beb5730ac"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_TG\_CAT\_2

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_3E"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_3E"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_3E"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43a3f1e97dafbab6c34d778ba85fe37b5bb"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_TG\_CAT\_3

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_4E"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_4E"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t29BK_AVRCP_SDP_FEATURE_TG_CAT_4E"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43a417cb2f93b3a630a4524bf4e2756f686"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_TG\_CAT\_4

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t38BK_AVRCP_SDP_FEATURE_TG_PLAYER_APP_SETE"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t38BK_AVRCP_SDP_FEATURE_TG_PLAYER_APP_SETE"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t38BK_AVRCP_SDP_FEATURE_TG_PLAYER_APP_SETE"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43ab54e178073846f6a9d9760108dbc2f13"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_TG\_PLAYER\_APP\_SET

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t33BK_AVRCP_SDP_FEATURE_TG_GROUP_NAVE"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t33BK_AVRCP_SDP_FEATURE_TG_GROUP_NAVE"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t33BK_AVRCP_SDP_FEATURE_TG_GROUP_NAVE"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43a12baed49af7fed478a9396dc6fb3ba92"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_TG\_GROUP\_NAV

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t40BK_AVRCP_SDP_FEATURE_TG_SUPPORT_BROWSINGE"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t40BK_AVRCP_SDP_FEATURE_TG_SUPPORT_BROWSINGE"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t40BK_AVRCP_SDP_FEATURE_TG_SUPPORT_BROWSINGE"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43a2ae4c7fe91303568a274e285c339875a"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_TG\_SUPPORT\_BROWSING

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t45BK_AVRCP_SDP_FEATURE_TG_SUPPORT_MULT_MEDIA_PAE"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t45BK_AVRCP_SDP_FEATURE_TG_SUPPORT_MULT_MEDIA_PAE"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t45BK_AVRCP_SDP_FEATURE_TG_SUPPORT_MULT_MEDIA_PAE"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43ae1ec165162a7d7c3ced5a415a1756798"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_TG\_SUPPORT\_MULT\_MEDIA\_PA

    <a id="_CPPv4N22bk_avrcp_sdp_feature_t34BK_AVRCP_SDP_FEATURE_TG_SUPPORT_CAE"></a>

    <a id="_CPPv3N22bk_avrcp_sdp_feature_t34BK_AVRCP_SDP_FEATURE_TG_SUPPORT_CAE"></a> <a id="_CPPv2N22bk_avrcp_sdp_feature_t34BK_AVRCP_SDP_FEATURE_TG_SUPPORT_CAE"></a> <a id="group__dm__avrcp__types_1gga21f9b8c44b15560a34b4f59cc1475a43a94d00ed8693d154d8ed7f0442cb2a900"></a> enumerator BK\_AVRCP\_SDP\_FEATURE\_TG\_SUPPORT\_CA

<a id="_CPPv417bk_avrcp_rn_rsp_t"></a>

<a id="_CPPv317bk_avrcp_rn_rsp_t"></a> <a id="_CPPv217bk_avrcp_rn_rsp_t"></a> <a id="group__dm__avrcp__types_1gab7c0f64f7d22a9a5fafaa97504ff506f"></a> enum bk\_avrcp\_rn\_rsp\_t
:   AVRC notification response type.

    *Values:*

    <a id="_CPPv4N17bk_avrcp_rn_rsp_t23BK_AVRCP_RN_RSP_INTERIME"></a>

    <a id="_CPPv3N17bk_avrcp_rn_rsp_t23BK_AVRCP_RN_RSP_INTERIME"></a> <a id="_CPPv2N17bk_avrcp_rn_rsp_t23BK_AVRCP_RN_RSP_INTERIME"></a> <a id="group__dm__avrcp__types_1ggab7c0f64f7d22a9a5fafaa97504ff506faf1dcfc252d41628de9a97e371d5cc98c"></a> enumerator BK\_AVRCP\_RN\_RSP\_INTERIM
    :   initial response to RegisterNotification, should be sent T\_mtp(1000ms) from receiving the command

    <a id="_CPPv4N17bk_avrcp_rn_rsp_t23BK_AVRCP_RN_RSP_CHANGEDE"></a>

    <a id="_CPPv3N17bk_avrcp_rn_rsp_t23BK_AVRCP_RN_RSP_CHANGEDE"></a> <a id="_CPPv2N17bk_avrcp_rn_rsp_t23BK_AVRCP_RN_RSP_CHANGEDE"></a> <a id="group__dm__avrcp__types_1ggab7c0f64f7d22a9a5fafaa97504ff506fade53ae52535d1f417ab7bddb737b9105"></a> enumerator BK\_AVRCP\_RN\_RSP\_CHANGED
    :   final response to RegisterNotification command

<a id="_CPPv428bk_avrcp_rn_cap_api_method_t"></a>

<a id="_CPPv328bk_avrcp_rn_cap_api_method_t"></a> <a id="_CPPv228bk_avrcp_rn_cap_api_method_t"></a> <a id="group__dm__avrcp__types_1gaa3ecceff152dd8c74f3557f0adb1b920"></a> enum bk\_avrcp\_rn\_cap\_api\_method\_t
:   AVRC target notification event notification capability.

    *Values:*

    <a id="_CPPv4N28bk_avrcp_rn_cap_api_method_t34BK_AVRCP_RN_CAP_API_METHOD_ALLOWEDE"></a>

    <a id="_CPPv3N28bk_avrcp_rn_cap_api_method_t34BK_AVRCP_RN_CAP_API_METHOD_ALLOWEDE"></a> <a id="_CPPv2N28bk_avrcp_rn_cap_api_method_t34BK_AVRCP_RN_CAP_API_METHOD_ALLOWEDE"></a> <a id="group__dm__avrcp__types_1ggaa3ecceff152dd8c74f3557f0adb1b920a2316f7e38e5c29879fda3f80bf4de736"></a> enumerator BK\_AVRCP\_RN\_CAP\_API\_METHOD\_ALLOWED
    :   all of the notification events that can possibly be supported, immutable

    <a id="_CPPv4N28bk_avrcp_rn_cap_api_method_t41BK_AVRCP_RN_CAP_API_METHOD_CURRENT_ENABLEE"></a>

    <a id="_CPPv3N28bk_avrcp_rn_cap_api_method_t41BK_AVRCP_RN_CAP_API_METHOD_CURRENT_ENABLEE"></a> <a id="_CPPv2N28bk_avrcp_rn_cap_api_method_t41BK_AVRCP_RN_CAP_API_METHOD_CURRENT_ENABLEE"></a> <a id="group__dm__avrcp__types_1ggaa3ecceff152dd8c74f3557f0adb1b920a484109cf5cecbf3f4b5bd075fddbddb2"></a> enumerator BK\_AVRCP\_RN\_CAP\_API\_METHOD\_CURRENT\_ENABLE
    :   notification events selectively supported according to the current configuration

    <a id="_CPPv4N28bk_avrcp_rn_cap_api_method_t30BK_AVRCP_RN_CAP_API_METHOD_MAXE"></a>

    <a id="_CPPv3N28bk_avrcp_rn_cap_api_method_t30BK_AVRCP_RN_CAP_API_METHOD_MAXE"></a> <a id="_CPPv2N28bk_avrcp_rn_cap_api_method_t30BK_AVRCP_RN_CAP_API_METHOD_MAXE"></a> <a id="group__dm__avrcp__types_1ggaa3ecceff152dd8c74f3557f0adb1b920ac9c9146dd1915fb28eea587b348a8d0e"></a> enumerator BK\_AVRCP\_RN\_CAP\_API\_METHOD\_MAX

<a id="_CPPv422bk_avrcp_psth_filter_t"></a>

<a id="_CPPv322bk_avrcp_psth_filter_t"></a> <a id="_CPPv222bk_avrcp_psth_filter_t"></a> <a id="group__dm__avrcp__types_1ga9b74caa3788d39aa15670a7e9d301186"></a> enum bk\_avrcp\_psth\_filter\_t
:   AVRC passthrough command filter.

    *Values:*

    <a id="_CPPv4N22bk_avrcp_psth_filter_t35BK_AVRCP_PSTH_FILTER_METHOD_ALLOWEDE"></a>

    <a id="_CPPv3N22bk_avrcp_psth_filter_t35BK_AVRCP_PSTH_FILTER_METHOD_ALLOWEDE"></a> <a id="_CPPv2N22bk_avrcp_psth_filter_t35BK_AVRCP_PSTH_FILTER_METHOD_ALLOWEDE"></a> <a id="group__dm__avrcp__types_1gga9b74caa3788d39aa15670a7e9d301186a26283bbaedd099a5e282ae4359f7697b"></a> enumerator BK\_AVRCP\_PSTH\_FILTER\_METHOD\_ALLOWED
    :   all of the PASSTHROUGH commands that can possibly be used, immutable

    <a id="_CPPv4N22bk_avrcp_psth_filter_t42BK_AVRCP_PSTH_FILTER_METHOD_CURRENT_ENABLEE"></a>

    <a id="_CPPv3N22bk_avrcp_psth_filter_t42BK_AVRCP_PSTH_FILTER_METHOD_CURRENT_ENABLEE"></a> <a id="_CPPv2N22bk_avrcp_psth_filter_t42BK_AVRCP_PSTH_FILTER_METHOD_CURRENT_ENABLEE"></a> <a id="group__dm__avrcp__types_1gga9b74caa3788d39aa15670a7e9d301186a9cc445b729549515633b5dafceb57e2d"></a> enumerator BK\_AVRCP\_PSTH\_FILTER\_METHOD\_CURRENT\_ENABLE
    :   PASSTHROUGH commands selectively supported according to the current configuration

    <a id="_CPPv4N22bk_avrcp_psth_filter_t31BK_AVRCP_PSTH_FILTER_METHOD_MAXE"></a>

    <a id="_CPPv3N22bk_avrcp_psth_filter_t31BK_AVRCP_PSTH_FILTER_METHOD_MAXE"></a> <a id="_CPPv2N22bk_avrcp_psth_filter_t31BK_AVRCP_PSTH_FILTER_METHOD_MAXE"></a> <a id="group__dm__avrcp__types_1gga9b74caa3788d39aa15670a7e9d301186a7ea80adea3b5dddc653f50abf57e577a"></a> enumerator BK\_AVRCP\_PSTH\_FILTER\_METHOD\_MAX

<a id="_CPPv422bk_avrcp_bit_mask_op_t"></a>

<a id="_CPPv322bk_avrcp_bit_mask_op_t"></a> <a id="_CPPv222bk_avrcp_bit_mask_op_t"></a> <a id="group__dm__avrcp__types_1ga7dba0002921603f5fadb2713d3f78f67"></a> enum bk\_avrcp\_bit\_mask\_op\_t
:   *Values:*

    <a id="_CPPv4N22bk_avrcp_bit_mask_op_t25BK_AVRCP_BIT_MASK_OP_TESTE"></a>

    <a id="_CPPv3N22bk_avrcp_bit_mask_op_t25BK_AVRCP_BIT_MASK_OP_TESTE"></a> <a id="_CPPv2N22bk_avrcp_bit_mask_op_t25BK_AVRCP_BIT_MASK_OP_TESTE"></a> <a id="group__dm__avrcp__types_1gga7dba0002921603f5fadb2713d3f78f67afe75334545f50d5e4e61d3cc23f9eca6"></a> enumerator BK\_AVRCP\_BIT\_MASK\_OP\_TEST
    :   operation code to test a specific bit

    <a id="_CPPv4N22bk_avrcp_bit_mask_op_t24BK_AVRCP_BIT_MASK_OP_SETE"></a>

    <a id="_CPPv3N22bk_avrcp_bit_mask_op_t24BK_AVRCP_BIT_MASK_OP_SETE"></a> <a id="_CPPv2N22bk_avrcp_bit_mask_op_t24BK_AVRCP_BIT_MASK_OP_SETE"></a> <a id="group__dm__avrcp__types_1gga7dba0002921603f5fadb2713d3f78f67a38a4fd606261e0275221549e637e56e5"></a> enumerator BK\_AVRCP\_BIT\_MASK\_OP\_SET
    :   operation code to set a specific bit

    <a id="_CPPv4N22bk_avrcp_bit_mask_op_t26BK_AVRCP_BIT_MASK_OP_CLEARE"></a>

    <a id="_CPPv3N22bk_avrcp_bit_mask_op_t26BK_AVRCP_BIT_MASK_OP_CLEARE"></a> <a id="_CPPv2N22bk_avrcp_bit_mask_op_t26BK_AVRCP_BIT_MASK_OP_CLEARE"></a> <a id="group__dm__avrcp__types_1gga7dba0002921603f5fadb2713d3f78f67ac6c42e056b6289b17872ecd8e0632a7a"></a> enumerator BK\_AVRCP\_BIT\_MASK\_OP\_CLEAR
    :   operation code to clear a specific bit

<a id="_CPPv422bk_avrcp_tg_cb_event_t"></a>

<a id="_CPPv322bk_avrcp_tg_cb_event_t"></a> <a id="_CPPv222bk_avrcp_tg_cb_event_t"></a> <a id="group__dm__avrcp__types_1ga2160c8551d6b6e170804ad1c5519af3f"></a> enum bk\_avrcp\_tg\_cb\_event\_t
:   AVRC Target callback events.

    *Values:*

    <a id="_CPPv4N22bk_avrcp_tg_cb_event_t32BK_AVRCP_TG_CONNECTION_STATE_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_event_t32BK_AVRCP_TG_CONNECTION_STATE_EVTE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_event_t32BK_AVRCP_TG_CONNECTION_STATE_EVTE"></a> <a id="group__dm__avrcp__types_1gga2160c8551d6b6e170804ad1c5519af3fa4be15d462ea5dd7ac237cbae299aff94"></a> enumerator BK\_AVRCP\_TG\_CONNECTION\_STATE\_EVT
    :   connection state changed event

    <a id="_CPPv4N22bk_avrcp_tg_cb_event_t31BK_AVRCP_TG_PASSTHROUGH_CMD_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_event_t31BK_AVRCP_TG_PASSTHROUGH_CMD_EVTE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_event_t31BK_AVRCP_TG_PASSTHROUGH_CMD_EVTE"></a> <a id="group__dm__avrcp__types_1gga2160c8551d6b6e170804ad1c5519af3fa4bdd7e7400a67c99d665a8948b9780d1"></a> enumerator BK\_AVRCP\_TG\_PASSTHROUGH\_CMD\_EVT
    :   passthrough command event

    <a id="_CPPv4N22bk_avrcp_tg_cb_event_t39BK_AVRCP_TG_SET_ABSOLUTE_VOLUME_CMD_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_event_t39BK_AVRCP_TG_SET_ABSOLUTE_VOLUME_CMD_EVTE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_event_t39BK_AVRCP_TG_SET_ABSOLUTE_VOLUME_CMD_EVTE"></a> <a id="group__dm__avrcp__types_1gga2160c8551d6b6e170804ad1c5519af3fa1ad017746605324004027f2bdf7bc816"></a> enumerator BK\_AVRCP\_TG\_SET\_ABSOLUTE\_VOLUME\_CMD\_EVT
    :   set absolute volume command from remote device

    <a id="_CPPv4N22bk_avrcp_tg_cb_event_t37BK_AVRCP_TG_REGISTER_NOTIFICATION_EVTE"></a>

    <a id="_CPPv3N22bk_avrcp_tg_cb_event_t37BK_AVRCP_TG_REGISTER_NOTIFICATION_EVTE"></a> <a id="_CPPv2N22bk_avrcp_tg_cb_event_t37BK_AVRCP_TG_REGISTER_NOTIFICATION_EVTE"></a> <a id="group__dm__avrcp__types_1gga2160c8551d6b6e170804ad1c5519af3fa4f23fb048f10f19a725f01987ea278a3"></a> enumerator BK\_AVRCP\_TG\_REGISTER\_NOTIFICATION\_EVT
    :   register notification event

<a id="bk-dm-hfp-types-h"></a>

## bk\_dm\_hfp\_types.h

`bk_dm_hfp_types.h` 定义 HFP profile 使用的事件、状态和通话控制类型。

<a id="id42"></a>

### Header File

- [bk\_dm\_hfp\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_hfp_types.h)

<a id="id43"></a>

### Structures

<a id="_CPPv423bk_hf_client_cb_param_t"></a>

<a id="_CPPv323bk_hf_client_cb_param_t"></a> <a id="_CPPv223bk_hf_client_cb_param_t"></a> <a id="bk_hf_client_cb_param_t"></a> <a id="structbk__hf__client__cb__param__t"></a> struct bk\_hf\_client\_cb\_param\_t
:   HFP client callback parameters.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23bk_hf_client_cb_param_t10remote_bdaE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t10remote_bdaE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t10remote_bdaE"></a> <a id="bk_hf_client_cb_param_t::remote_bda__uint8_tA"></a> <a id="structbk__hf__client__cb__param__t_1a24c00d8098b8501e7e2981fd9b6e366d"></a> uint8\_t remote\_bda\[6\]
    :   remote bluetooth device address

    <a id="_CPPv4N23bk_hf_client_cb_param_t5stateE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t5stateE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t5stateE"></a> <a id="bk_hf_client_cb_param_t::state__bk_hf_client_connection_state_t"></a> <a id="structbk__hf__client__cb__param__t_1aa3149896e2cb955c40d053ea77d01999"></a> [bk\_hf\_client\_connection\_state\_t](#_CPPv431bk_hf_client_connection_state_t "bk_hf_client_connection_state_t") state
    :   HF connection state

    <a id="_CPPv4N23bk_hf_client_cb_param_t9peer_featE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t9peer_featE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t9peer_featE"></a> <a id="bk_hf_client_cb_param_t::peer_feat__uint32_t"></a> <a id="structbk__hf__client__cb__param__t_1a6dae3d8772e01e68e5bd25a81fad904c"></a> uint32\_t peer\_feat
    :   AG supported features

    <a id="_CPPv4N23bk_hf_client_cb_param_t9chld_featE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t9chld_featE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t9chld_featE"></a> <a id="bk_hf_client_cb_param_t::chld_feat__uint32_t"></a> <a id="structbk__hf__client__cb__param__t_1a9152584aaff88be1f57b90ab344dc8dc"></a> uint32\_t chld\_feat
    :   AG supported features on call hold and multiparty services

    <a id="_CPPv4N23bk_hf_client_cb_param_t10conn_stateE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t10conn_stateE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t10conn_stateE"></a> <a id="structbk__hf__client__cb__param__t_1acf1f0715a39e9bcaca16082862e296b4"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_conn\_stat\_param conn\_state
    :   HF callback param of BK\_HF\_CLIENT\_CONNECTION\_STATE\_EVT

    <a id="structbk__hf__client__cb__param__t_1aa6f234eac18f1c7c3e1da4eb738c3eeb"></a> [bk\_hf\_client\_audio\_state\_t](#_CPPv426bk_hf_client_audio_state_t "bk_hf_client_audio_state_t") state
    :   audio connection state

    <a id="_CPPv4N23bk_hf_client_cb_param_t10codec_typeE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t10codec_typeE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t10codec_typeE"></a> <a id="bk_hf_client_cb_param_t::codec_type__bk_hf_codec_type_t"></a> <a id="structbk__hf__client__cb__param__t_1a15ef8f75a0c9f6add0d1dc82120c7a2a"></a> bk\_hf\_codec\_type\_t codec\_type
    :   cvsd or msbc

    <a id="_CPPv4N23bk_hf_client_cb_param_t8intervalE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t8intervalE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t8intervalE"></a> <a id="bk_hf_client_cb_param_t::interval__uint8_t"></a> <a id="structbk__hf__client__cb__param__t_1afd6d61e9a30e994c48dc2c0e3f0c88ff"></a> uint8\_t interval
    :   tx interval in 625us

    <a id="_CPPv4N23bk_hf_client_cb_param_t13tx_packet_lenE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t13tx_packet_lenE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t13tx_packet_lenE"></a> <a id="bk_hf_client_cb_param_t::tx_packet_len__uint16_t"></a> <a id="structbk__hf__client__cb__param__t_1a36411cac868d2d840c70a445e37273ce"></a> uint16\_t tx\_packet\_len
    :   tx packet len in byte

    <a id="_CPPv4N23bk_hf_client_cb_param_t13rx_packet_lenE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t13rx_packet_lenE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t13rx_packet_lenE"></a> <a id="bk_hf_client_cb_param_t::rx_packet_len__uint16_t"></a> <a id="structbk__hf__client__cb__param__t_1afd87783f9d8409091df0c046995772e9"></a> uint16\_t rx\_packet\_len
    :   rx packet len in byte

    <a id="_CPPv4N23bk_hf_client_cb_param_t11packet_typeE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t11packet_typeE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t11packet_typeE"></a> <a id="bk_hf_client_cb_param_t::packet_type__uint8_t"></a> <a id="structbk__hf__client__cb__param__t_1a4cdec134c3734d01da2c849297a11ee9"></a> uint8\_t packet\_type
    :   coding packet type, see bk\_bt\_audio\_coding\_format\_t

    <a id="_CPPv4N23bk_hf_client_cb_param_t11audio_stateE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t11audio_stateE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t11audio_stateE"></a> <a id="structbk__hf__client__cb__param__t_1aa1c456abb58a6cdd034ee14a13342aa5"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_audio\_stat\_param audio\_state
    :   HF callback param of BK\_HF\_CLIENT\_AUDIO\_STATE\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t5valueE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t5valueE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t5valueE"></a> <a id="bk_hf_client_cb_param_t::value__bk_hf_vr_state_t"></a> <a id="structbk__hf__client__cb__param__t_1a44282b1cafb70690fa25bc88410d9c6b"></a> bk\_hf\_vr\_state\_t value
    :   voice recognition state

    <a id="_CPPv4N23bk_hf_client_cb_param_t4bvraE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4bvraE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4bvraE"></a> <a id="structbk__hf__client__cb__param__t_1a3c11cadc9984bc1adbcb1aac63fe12c2"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_bvra\_param bvra
    :   HF callback param of BK\_HF\_CLIENT\_BVRA\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t6statusE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t6statusE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t6statusE"></a> <a id="bk_hf_client_cb_param_t::status__bk_hf_call_status_t"></a> <a id="structbk__hf__client__cb__param__t_1a7164a6d9e32295d90f189d5fba1e8ea4"></a> bk\_hf\_call\_status\_t status
    :   call status indicator

    <a id="_CPPv4N23bk_hf_client_cb_param_t4callE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4callE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4callE"></a> <a id="structbk__hf__client__cb__param__t_1a6c69d7913af942392bd86499f8be5361"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_call\_ind\_param call
    :   HF callback param of BK\_HF\_CLIENT\_CIND\_CALL\_EVT

    <a id="structbk__hf__client__cb__param__t_1a035ce85f3df619c8b615c709cf8a329f"></a> bk\_hf\_call\_setup\_status\_t status
    :   call setup status indicator

    <a id="_CPPv4N23bk_hf_client_cb_param_t10call_setupE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t10call_setupE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t10call_setupE"></a> <a id="structbk__hf__client__cb__param__t_1ade9082d7a2f355bf71d478aa54466a71"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_call\_setup\_ind\_param call\_setup
    :   HF callback param of BK\_HF\_CLIENT\_BVRA\_EVT

    <a id="structbk__hf__client__cb__param__t_1a8ddbd65156cdef437b16206a154a5c17"></a> bk\_hf\_call\_held\_status\_t status
    :   bluetooth proprietary call hold status indicator

    <a id="_CPPv4N23bk_hf_client_cb_param_t9call_heldE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t9call_heldE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t9call_heldE"></a> <a id="structbk__hf__client__cb__param__t_1afb4db18e53501c537a11bf8f46f3fa9f"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_call\_held\_ind\_param call\_held
    :   HF callback param of BK\_HF\_CLIENT\_CIND\_CALL\_HELD\_EVT

    <a id="structbk__hf__client__cb__param__t_1a6d47d1cd9dad68c4419b7b9e6c52c1cd"></a> bk\_hf\_network\_state\_t status
    :   service availability status

    <a id="_CPPv4N23bk_hf_client_cb_param_t20service_availabilityE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t20service_availabilityE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t20service_availabilityE"></a> <a id="structbk__hf__client__cb__param__t_1a0ab56ffa3152c4e632989b8e82c36098"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_service\_availability\_param service\_availability
    :   HF callback param of BK\_HF\_CLIENT\_CIND\_SERVICE\_AVAILABILITY\_EVT

    <a id="structbk__hf__client__cb__param__t_1a45c23e65852621a8f3fb45e51ea114ee"></a> int value
    :   signal strength value, ranges from 0 to 5

        battery charge value, ranges from 0 to 5

    <a id="_CPPv4N23bk_hf_client_cb_param_t15signal_strengthE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t15signal_strengthE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t15signal_strengthE"></a> <a id="structbk__hf__client__cb__param__t_1add4aa33ab282c4e940ec5aeadf365f42"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_signal\_strength\_ind\_param signal\_strength
    :   HF callback param of BK\_HF\_CLIENT\_CIND\_SIGNAL\_STRENGTH\_EVT

    <a id="structbk__hf__client__cb__param__t_1a5f2b8008f6092a78d25eac408b7c27c7"></a> bk\_hf\_roaming\_status\_t status
    :   roaming status

    <a id="_CPPv4N23bk_hf_client_cb_param_t7roamingE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t7roamingE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t7roamingE"></a> <a id="structbk__hf__client__cb__param__t_1a3ec4c5bc2086eca81dc9acb68c391113"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_network\_roaming\_param roaming
    :   HF callback param of BK\_HF\_CLIENT\_CIND\_ROAMING\_STATUS\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t13battery_levelE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t13battery_levelE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t13battery_levelE"></a> <a id="structbk__hf__client__cb__param__t_1a2ce651318136fcc7109e8315abd471fa"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_battery\_level\_ind\_param battery\_level
    :   HF callback param of BK\_HF\_CLIENT\_CIND\_BATTERY\_LEVEL\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t4nameE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4nameE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4nameE"></a> <a id="bk_hf_client_cb_param_t::name__cCP"></a> <a id="structbk__hf__client__cb__param__t_1a9633c49c821190a6238d60447ff5f515"></a> const char \*name
    :   name of the network operator

        name string of the call

        name string of waiting call

    <a id="_CPPv4N23bk_hf_client_cb_param_t4copsE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4copsE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4copsE"></a> <a id="structbk__hf__client__cb__param__t_1ad07e8307918e2d637c7ede70a9301657"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_current\_operator\_param cops
    :   HF callback param of BK\_HF\_CLIENT\_COPS\_CURRENT\_OPERATOR\_EVT

    <a id="structbk__hf__client__cb__param__t_1ad3ae088b116ce266749bd591415a96b5"></a> bk\_hf\_btrh\_status\_t status
    :   call hold and response status result code

    <a id="_CPPv4N23bk_hf_client_cb_param_t4btrhE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4btrhE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4btrhE"></a> <a id="structbk__hf__client__cb__param__t_1a2cb4adff07bab35ce54fa9176e6697d2"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_btrh\_param btrh
    :   HF callback param of BK\_HF\_CLIENT\_BRTH\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t6numberE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t6numberE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t6numberE"></a> <a id="bk_hf_client_cb_param_t::number__cCP"></a> <a id="structbk__hf__client__cb__param__t_1a75d5d7b55c80fb1d17d142414f8de331"></a> const char \*number
    :   phone number string of call

        phone number string of waiting call

        phone number string

        phone number corresponding to the last voice tag in the HF

    <a id="_CPPv4N23bk_hf_client_cb_param_t4clipE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4clipE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4clipE"></a> <a id="structbk__hf__client__cb__param__t_1a6c896901f7395127794dcaaa0659aae3"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_clip\_param clip
    :   HF callback param of BK\_HF\_CLIENT\_CLIP\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t4ccwaE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4ccwaE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4ccwaE"></a> <a id="structbk__hf__client__cb__param__t_1ad6399f013e4eab4fb29a9ee1d3ef31ef"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_ccwa\_param ccwa
    :   HF callback param of BK\_HF\_CLIENT\_BVRA\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t3idxE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t3idxE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t3idxE"></a> <a id="bk_hf_client_cb_param_t::idx__i"></a> <a id="structbk__hf__client__cb__param__t_1a14ecfe6a207e2367e4e26c24e182bad7"></a> int idx
    :   numbering(starting with 1\) of the call

    <a id="_CPPv4N23bk_hf_client_cb_param_t3dirE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t3dirE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t3dirE"></a> <a id="bk_hf_client_cb_param_t::dir__bk_hf_current_call_direction_t"></a> <a id="structbk__hf__client__cb__param__t_1aa7f37e199e8215b9f4b11de0165ec2f2"></a> bk\_hf\_current\_call\_direction\_t dir
    :   direction of the call

    <a id="structbk__hf__client__cb__param__t_1a0024eaf691f612871b3976ae4e748162"></a> bk\_hf\_current\_call\_status\_t status
    :   status of the call

    <a id="_CPPv4N23bk_hf_client_cb_param_t4mptyE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4mptyE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4mptyE"></a> <a id="bk_hf_client_cb_param_t::mpty__bk_hf_current_call_mpty_type_t"></a> <a id="structbk__hf__client__cb__param__t_1a10bed464a3ddd2d7382e42a7fc156efe"></a> bk\_hf\_current\_call\_mpty\_type\_t mpty
    :   multi-party flag

    <a id="structbk__hf__client__cb__param__t_1ac15a06a1ec8f26062c7a4b9658c2f8f0"></a> char \*number
    :   phone number(optional)

    <a id="_CPPv4N23bk_hf_client_cb_param_t4clccE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4clccE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4clccE"></a> <a id="structbk__hf__client__cb__param__t_1aaf924c1b740f2030eb03f0a6e22fceab"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_clcc\_param clcc
    :   HF callback param of BK\_HF\_CLIENT\_CLCC\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t4typeE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4typeE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4typeE"></a> <a id="bk_hf_client_cb_param_t::type__bk_hf_volume_control_target_t"></a> <a id="structbk__hf__client__cb__param__t_1ad00884df052da172de9c3124ed686c3a"></a> bk\_hf\_volume\_control\_target\_t type
    :   volume control target, speaker or microphone

    <a id="_CPPv4N23bk_hf_client_cb_param_t6volumeE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t6volumeE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t6volumeE"></a> <a id="bk_hf_client_cb_param_t::volume__i"></a> <a id="structbk__hf__client__cb__param__t_1a2c16f08b25730a83bc727a9c083f1bac"></a> int volume
    :   gain, ranges from 0 to 15

    <a id="_CPPv4N23bk_hf_client_cb_param_t14volume_controlE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t14volume_controlE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t14volume_controlE"></a> <a id="structbk__hf__client__cb__param__t_1ac635233977d95b03d335fc52a2e87dbb"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_volume\_control\_param volume\_control
    :   HF callback param of BK\_HF\_CLIENT\_VOLUME\_CONTROL\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t4codeE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4codeE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4codeE"></a> <a id="bk_hf_client_cb_param_t::code__bk_hf_at_response_code_t"></a> <a id="structbk__hf__client__cb__param__t_1a9c3853918446df03205b26002e270172"></a> bk\_hf\_at\_response\_code\_t code
    :   AT response code

    <a id="_CPPv4N23bk_hf_client_cb_param_t3cmeE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t3cmeE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t3cmeE"></a> <a id="bk_hf_client_cb_param_t::cme__bk_hf_cme_err_t"></a> <a id="structbk__hf__client__cb__param__t_1a9937f6f0cfbc691ea452eadd68fb36ce"></a> bk\_hf\_cme\_err\_t cme
    :   Extended Audio Gateway Error Result Code

    <a id="_CPPv4N23bk_hf_client_cb_param_t11at_responseE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t11at_responseE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t11at_responseE"></a> <a id="structbk__hf__client__cb__param__t_1a7eb08385b6b9a2290cf91087b96e2763"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_at\_response\_param at\_response
    :   HF callback param of BK\_HF\_CLIENT\_AT\_RESPONSE\_EVT

    <a id="structbk__hf__client__cb__param__t_1af0bfc1bc2df9792e42a769ff46a21cca"></a> bk\_hf\_subscriber\_service\_type\_t type
    :   service type that the phone number relates to

    <a id="_CPPv4N23bk_hf_client_cb_param_t4cnumE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4cnumE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4cnumE"></a> <a id="structbk__hf__client__cb__param__t_1ad24de02fee026eb12a62e0242758992d"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_cnum\_param cnum
    :   HF callback param of BK\_HF\_CLIENT\_CNUM\_EVT

    <a id="structbk__hf__client__cb__param__t_1a02f3879674987bda3414ab4646b7446e"></a> [bk\_hf\_client\_in\_band\_ring\_state\_t](#_CPPv433bk_hf_client_in_band_ring_state_t "bk_hf_client_in_band_ring_state_t") state
    :   setting state of in-band ring tone

    <a id="_CPPv4N23bk_hf_client_cb_param_t4bsirE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4bsirE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4bsirE"></a> <a id="structbk__hf__client__cb__param__t_1af7871005ac15f356165ddb9a86d42f5c"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_bsirparam bsir
    :   HF callback param of BK\_HF\_CLIENT\_BSIR\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t4binpE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4binpE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4binpE"></a> <a id="structbk__hf__client__cb__param__t_1a11c83e0b609f23c77be6a6c4279d0216"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_binp\_param binp
    :   HF callback param of BK\_HF\_CLIENT\_BINP\_EVT

    <a id="_CPPv4N23bk_hf_client_cb_param_t4dataE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t4dataE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t4dataE"></a> <a id="bk_hf_client_cb_param_t::data__cCP"></a> <a id="structbk__hf__client__cb__param__t_1af22336dc2c1813a3c2ff97c28c555a3f"></a> const char \*data
    :   unknown data

    <a id="_CPPv4N23bk_hf_client_cb_param_t8data_lenE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t8data_lenE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t8data_lenE"></a> <a id="bk_hf_client_cb_param_t::data_len__uint16_t"></a> <a id="structbk__hf__client__cb__param__t_1a536369f73483bdc31542dd3fe7680708"></a> uint16\_t data\_len
    :   the length of unknown data

    <a id="_CPPv4N23bk_hf_client_cb_param_t12unknown_dataE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_param_t12unknown_dataE"></a> <a id="_CPPv2N23bk_hf_client_cb_param_t12unknown_dataE"></a> <a id="structbk__hf__client__cb__param__t_1aeebc3776c2d0290a4bf7953f0db5b1c4"></a> struct [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t")::\[anonymous\]::hf\_client\_unknown\_data\_param unknown\_data
    :   HF callback param of BK\_HF\_CLIENT\_UNKNOWN\_DATA\_IND\_EVT

<a id="id44"></a>

### Type Definitions

<a id="_CPPv420bk_bt_hf_client_cb_t"></a>

<a id="_CPPv320bk_bt_hf_client_cb_t"></a> <a id="_CPPv220bk_bt_hf_client_cb_t"></a> <a id="bk_bt_hf_client_cb_t"></a> <a id="bk__dm__hfp__types_8h_1a52af54ebc7efe18f006f5dfc88819cf6"></a> typedef void (\*bk\_bt\_hf\_client\_cb\_t)([bk\_hf\_client\_cb\_event\_t](#_CPPv423bk_hf_client_cb_event_t "bk_hf_client_cb_event_t") event, [bk\_hf\_client\_cb\_param\_t](#_CPPv423bk_hf_client_cb_param_t "bk_hf_client_cb_param_t") \*param)
:   HFP client callback function type.

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter

<a id="_CPPv425bk_bt_hf_client_data_cb_t"></a>

<a id="_CPPv325bk_bt_hf_client_data_cb_t"></a> <a id="_CPPv225bk_bt_hf_client_data_cb_t"></a> <a id="bk_bt_hf_client_data_cb_t"></a> <a id="bk__dm__hfp__types_8h_1a72f2d4a3c9f20029ef9212f7d18e0a1b"></a> typedef void (\*bk\_bt\_hf\_client\_data\_cb\_t)(const uint8\_t \*buf, uint16\_t len)
:   HFP client incoming data callback function.

    Param buf
    :   **\[in\]** : pointer to the data(payload of HCI synchronous data packet) received from HFP AG device

    Param len
    :   **\[in\]** : size(in bytes) in buf

<a id="id45"></a>

### Enumerations

<a id="_CPPv431bk_hf_client_connection_state_t"></a>

<a id="_CPPv331bk_hf_client_connection_state_t"></a> <a id="_CPPv231bk_hf_client_connection_state_t"></a> <a id="bk__dm__hfp__types_8h_1a0f2b2c42f4d785e4aeb4e42e0a142e19"></a> enum bk\_hf\_client\_connection\_state\_t
:   Bluetooth HFP RFCOMM connection and service level connection status.

    *Values:*

    <a id="_CPPv4N31bk_hf_client_connection_state_t42BK_HF_CLIENT_CONNECTION_STATE_DISCONNECTEDE"></a>

    <a id="_CPPv3N31bk_hf_client_connection_state_t42BK_HF_CLIENT_CONNECTION_STATE_DISCONNECTEDE"></a> <a id="_CPPv2N31bk_hf_client_connection_state_t42BK_HF_CLIENT_CONNECTION_STATE_DISCONNECTEDE"></a> <a id="bk__dm__hfp__types_8h_1a0f2b2c42f4d785e4aeb4e42e0a142e19a8784108339bc7bbbc171b32efc94e82b"></a> enumerator BK\_HF\_CLIENT\_CONNECTION\_STATE\_DISCONNECTED
    :   RFCOMM data link channel released

    <a id="_CPPv4N31bk_hf_client_connection_state_t40BK_HF_CLIENT_CONNECTION_STATE_CONNECTINGE"></a>

    <a id="_CPPv3N31bk_hf_client_connection_state_t40BK_HF_CLIENT_CONNECTION_STATE_CONNECTINGE"></a> <a id="_CPPv2N31bk_hf_client_connection_state_t40BK_HF_CLIENT_CONNECTION_STATE_CONNECTINGE"></a> <a id="bk__dm__hfp__types_8h_1a0f2b2c42f4d785e4aeb4e42e0a142e19a73f0c20ed6a6d572f30b545350dd7787"></a> enumerator BK\_HF\_CLIENT\_CONNECTION\_STATE\_CONNECTING
    :   connecting remote device on the RFCOMM data link

    <a id="_CPPv4N31bk_hf_client_connection_state_t39BK_HF_CLIENT_CONNECTION_STATE_CONNECTEDE"></a>

    <a id="_CPPv3N31bk_hf_client_connection_state_t39BK_HF_CLIENT_CONNECTION_STATE_CONNECTEDE"></a> <a id="_CPPv2N31bk_hf_client_connection_state_t39BK_HF_CLIENT_CONNECTION_STATE_CONNECTEDE"></a> <a id="bk__dm__hfp__types_8h_1a0f2b2c42f4d785e4aeb4e42e0a142e19a06203a0d6b5787ac48d0dd41bb35adf9"></a> enumerator BK\_HF\_CLIENT\_CONNECTION\_STATE\_CONNECTED
    :   RFCOMM connection established

    <a id="_CPPv4N31bk_hf_client_connection_state_t43BK_HF_CLIENT_CONNECTION_STATE_SLC_CONNECTEDE"></a>

    <a id="_CPPv3N31bk_hf_client_connection_state_t43BK_HF_CLIENT_CONNECTION_STATE_SLC_CONNECTEDE"></a> <a id="_CPPv2N31bk_hf_client_connection_state_t43BK_HF_CLIENT_CONNECTION_STATE_SLC_CONNECTEDE"></a> <a id="bk__dm__hfp__types_8h_1a0f2b2c42f4d785e4aeb4e42e0a142e19adae268499203bbbb576ad02a3b4538eb"></a> enumerator BK\_HF\_CLIENT\_CONNECTION\_STATE\_SLC\_CONNECTED
    :   service level connection established

    <a id="_CPPv4N31bk_hf_client_connection_state_t43BK_HF_CLIENT_CONNECTION_STATE_DISCONNECTINGE"></a>

    <a id="_CPPv3N31bk_hf_client_connection_state_t43BK_HF_CLIENT_CONNECTION_STATE_DISCONNECTINGE"></a> <a id="_CPPv2N31bk_hf_client_connection_state_t43BK_HF_CLIENT_CONNECTION_STATE_DISCONNECTINGE"></a> <a id="bk__dm__hfp__types_8h_1a0f2b2c42f4d785e4aeb4e42e0a142e19ad623fad1697a9a95da6bf444f89dc70a"></a> enumerator BK\_HF\_CLIENT\_CONNECTION\_STATE\_DISCONNECTING
    :   disconnecting with remote device on the RFCOMM dat link

<a id="_CPPv426bk_hf_client_audio_state_t"></a>

<a id="_CPPv326bk_hf_client_audio_state_t"></a> <a id="_CPPv226bk_hf_client_audio_state_t"></a> <a id="bk__dm__hfp__types_8h_1a50bf2f9db92653ffc27b58a9582a2bec"></a> enum bk\_hf\_client\_audio\_state\_t
:   Bluetooth HFP audio connection status.

    *Values:*

    <a id="_CPPv4N26bk_hf_client_audio_state_t37BK_HF_CLIENT_AUDIO_STATE_DISCONNECTEDE"></a>

    <a id="_CPPv3N26bk_hf_client_audio_state_t37BK_HF_CLIENT_AUDIO_STATE_DISCONNECTEDE"></a> <a id="_CPPv2N26bk_hf_client_audio_state_t37BK_HF_CLIENT_AUDIO_STATE_DISCONNECTEDE"></a> <a id="bk__dm__hfp__types_8h_1a50bf2f9db92653ffc27b58a9582a2beca08750843a54242c0e5311376731cae88"></a> enumerator BK\_HF\_CLIENT\_AUDIO\_STATE\_DISCONNECTED
    :   audio connection released

    <a id="_CPPv4N26bk_hf_client_audio_state_t35BK_HF_CLIENT_AUDIO_STATE_CONNECTINGE"></a>

    <a id="_CPPv3N26bk_hf_client_audio_state_t35BK_HF_CLIENT_AUDIO_STATE_CONNECTINGE"></a> <a id="_CPPv2N26bk_hf_client_audio_state_t35BK_HF_CLIENT_AUDIO_STATE_CONNECTINGE"></a> <a id="bk__dm__hfp__types_8h_1a50bf2f9db92653ffc27b58a9582a2beca5351dcbc5a3111b949f28cf844e49c65"></a> enumerator BK\_HF\_CLIENT\_AUDIO\_STATE\_CONNECTING
    :   audio connection has been initiated

    <a id="_CPPv4N26bk_hf_client_audio_state_t34BK_HF_CLIENT_AUDIO_STATE_CONNECTEDE"></a>

    <a id="_CPPv3N26bk_hf_client_audio_state_t34BK_HF_CLIENT_AUDIO_STATE_CONNECTEDE"></a> <a id="_CPPv2N26bk_hf_client_audio_state_t34BK_HF_CLIENT_AUDIO_STATE_CONNECTEDE"></a> <a id="bk__dm__hfp__types_8h_1a50bf2f9db92653ffc27b58a9582a2beca1deabd31455786111ea53e2dd3ce6ef6"></a> enumerator BK\_HF\_CLIENT\_AUDIO\_STATE\_CONNECTED
    :   audio connection is established

<a id="_CPPv423bk_hf_client_cb_event_t"></a>

<a id="_CPPv323bk_hf_client_cb_event_t"></a> <a id="_CPPv223bk_hf_client_cb_event_t"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4"></a> enum bk\_hf\_client\_cb\_event\_t
:   HF CLIENT callback events.

    *Values:*

    <a id="_CPPv4N23bk_hf_client_cb_event_t33BK_HF_CLIENT_CONNECTION_STATE_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t33BK_HF_CLIENT_CONNECTION_STATE_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t33BK_HF_CLIENT_CONNECTION_STATE_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4ac2b99d8b8c2b8f9c64d18406cdf3f47e"></a> enumerator BK\_HF\_CLIENT\_CONNECTION\_STATE\_EVT
    :   connection state changed event

    <a id="_CPPv4N23bk_hf_client_cb_event_t28BK_HF_CLIENT_AUDIO_STATE_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t28BK_HF_CLIENT_AUDIO_STATE_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t28BK_HF_CLIENT_AUDIO_STATE_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a07f4b58e0480e9e8835f36682ab8a2ec"></a> enumerator BK\_HF\_CLIENT\_AUDIO\_STATE\_EVT
    :   audio connection state change event

    <a id="_CPPv4N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BVRA_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BVRA_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BVRA_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4aa93a58f33c4743991197afefd194ed96"></a> enumerator BK\_HF\_CLIENT\_BVRA\_EVT
    :   voice recognition state change event

    <a id="_CPPv4N23bk_hf_client_cb_event_t26BK_HF_CLIENT_CIND_CALL_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t26BK_HF_CLIENT_CIND_CALL_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t26BK_HF_CLIENT_CIND_CALL_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4acfbe77714a78892b20776461899bb637"></a> enumerator BK\_HF\_CLIENT\_CIND\_CALL\_EVT
    :   call indication

    <a id="_CPPv4N23bk_hf_client_cb_event_t32BK_HF_CLIENT_CIND_CALL_SETUP_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t32BK_HF_CLIENT_CIND_CALL_SETUP_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t32BK_HF_CLIENT_CIND_CALL_SETUP_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a88c7d94d566d57f750700159d14175f8"></a> enumerator BK\_HF\_CLIENT\_CIND\_CALL\_SETUP\_EVT
    :   call setup indication

    <a id="_CPPv4N23bk_hf_client_cb_event_t31BK_HF_CLIENT_CIND_CALL_HELD_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t31BK_HF_CLIENT_CIND_CALL_HELD_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t31BK_HF_CLIENT_CIND_CALL_HELD_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a98d7bcd623d23c25923af67097979f06"></a> enumerator BK\_HF\_CLIENT\_CIND\_CALL\_HELD\_EVT
    :   call held indication

    <a id="_CPPv4N23bk_hf_client_cb_event_t42BK_HF_CLIENT_CIND_SERVICE_AVAILABILITY_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t42BK_HF_CLIENT_CIND_SERVICE_AVAILABILITY_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t42BK_HF_CLIENT_CIND_SERVICE_AVAILABILITY_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a16889ab1c397108a23f8f64aea6b8049"></a> enumerator BK\_HF\_CLIENT\_CIND\_SERVICE\_AVAILABILITY\_EVT
    :   network service availability indication

    <a id="_CPPv4N23bk_hf_client_cb_event_t37BK_HF_CLIENT_CIND_SIGNAL_STRENGTH_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t37BK_HF_CLIENT_CIND_SIGNAL_STRENGTH_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t37BK_HF_CLIENT_CIND_SIGNAL_STRENGTH_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a1e9a2c54505098d126b9e7a2a51fd029"></a> enumerator BK\_HF\_CLIENT\_CIND\_SIGNAL\_STRENGTH\_EVT
    :   signal strength indication

    <a id="_CPPv4N23bk_hf_client_cb_event_t36BK_HF_CLIENT_CIND_ROAMING_STATUS_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t36BK_HF_CLIENT_CIND_ROAMING_STATUS_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t36BK_HF_CLIENT_CIND_ROAMING_STATUS_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4ac84c2fa34bda500d4f28977d9addaaa8"></a> enumerator BK\_HF\_CLIENT\_CIND\_ROAMING\_STATUS\_EVT
    :   roaming status indication

    <a id="_CPPv4N23bk_hf_client_cb_event_t35BK_HF_CLIENT_CIND_BATTERY_LEVEL_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t35BK_HF_CLIENT_CIND_BATTERY_LEVEL_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t35BK_HF_CLIENT_CIND_BATTERY_LEVEL_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a104e704a746bffe2fad22ef7d011eab7"></a> enumerator BK\_HF\_CLIENT\_CIND\_BATTERY\_LEVEL\_EVT
    :   battery level indication

    <a id="_CPPv4N23bk_hf_client_cb_event_t38BK_HF_CLIENT_COPS_CURRENT_OPERATOR_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t38BK_HF_CLIENT_COPS_CURRENT_OPERATOR_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t38BK_HF_CLIENT_COPS_CURRENT_OPERATOR_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4ae54774a46409331eab611826aa6ceee0"></a> enumerator BK\_HF\_CLIENT\_COPS\_CURRENT\_OPERATOR\_EVT
    :   current operator information

    <a id="_CPPv4N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BTRH_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BTRH_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BTRH_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4aedc58580951a25874581fd3fbb20791c"></a> enumerator BK\_HF\_CLIENT\_BTRH\_EVT
    :   call response and hold event

    <a id="_CPPv4N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CLIP_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CLIP_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CLIP_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4af8a00156d90c4b1be013c51a4d43acfc"></a> enumerator BK\_HF\_CLIENT\_CLIP\_EVT
    :   Calling Line Identification notification

    <a id="_CPPv4N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CCWA_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CCWA_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CCWA_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a044639f4c7179e54704992ee93a905b6"></a> enumerator BK\_HF\_CLIENT\_CCWA\_EVT
    :   call waiting notification

    <a id="_CPPv4N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CLCC_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CLCC_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CLCC_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4ae742ca87cee4eca7dc6a293cf1c6d205"></a> enumerator BK\_HF\_CLIENT\_CLCC\_EVT
    :   list of current calls notification

    <a id="_CPPv4N23bk_hf_client_cb_event_t31BK_HF_CLIENT_VOLUME_CONTROL_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t31BK_HF_CLIENT_VOLUME_CONTROL_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t31BK_HF_CLIENT_VOLUME_CONTROL_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a7bd044cf47f03265092b005cc45ac915"></a> enumerator BK\_HF\_CLIENT\_VOLUME\_CONTROL\_EVT
    :   audio volume control command from AG, provided by \+VGM or \+VGS message

    <a id="_CPPv4N23bk_hf_client_cb_event_t28BK_HF_CLIENT_AT_RESPONSE_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t28BK_HF_CLIENT_AT_RESPONSE_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t28BK_HF_CLIENT_AT_RESPONSE_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a5d7fc04aed3a395754678dbdf209123d"></a> enumerator BK\_HF\_CLIENT\_AT\_RESPONSE\_EVT
    :   AT command response event

    <a id="_CPPv4N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CNUM_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CNUM_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t21BK_HF_CLIENT_CNUM_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4aedf7554dbd0b3f8c6268be1cb5583026"></a> enumerator BK\_HF\_CLIENT\_CNUM\_EVT
    :   subscriber information response from AG

    <a id="_CPPv4N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BSIR_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BSIR_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BSIR_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a282027472e3a020e08faad9dae5bd6b4"></a> enumerator BK\_HF\_CLIENT\_BSIR\_EVT
    :   setting of in-band ring tone

    <a id="_CPPv4N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BINP_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BINP_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t21BK_HF_CLIENT_BINP_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4a793f7ec149c1f87f7258d29cade62af0"></a> enumerator BK\_HF\_CLIENT\_BINP\_EVT
    :   requested number of last voice tag from AG

    <a id="_CPPv4N23bk_hf_client_cb_event_t25BK_HF_CLIENT_RING_IND_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t25BK_HF_CLIENT_RING_IND_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t25BK_HF_CLIENT_RING_IND_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4ac73a0c579bec911c7b609a29f4d558b8"></a> enumerator BK\_HF\_CLIENT\_RING\_IND\_EVT
    :   ring indication event

    <a id="_CPPv4N23bk_hf_client_cb_event_t33BK_HF_CLIENT_UNKNOWN_DATA_IND_EVTE"></a>

    <a id="_CPPv3N23bk_hf_client_cb_event_t33BK_HF_CLIENT_UNKNOWN_DATA_IND_EVTE"></a> <a id="_CPPv2N23bk_hf_client_cb_event_t33BK_HF_CLIENT_UNKNOWN_DATA_IND_EVTE"></a> <a id="bk__dm__hfp__types_8h_1adfc78abb9a3d2ad22c387d0c193c2ca4aa9691f35da4f06bbe4c3dc53c11908f6"></a> enumerator BK\_HF\_CLIENT\_UNKNOWN\_DATA\_IND\_EVT
    :   unknown data from AG

<a id="_CPPv433bk_hf_client_in_band_ring_state_t"></a>

<a id="_CPPv333bk_hf_client_in_band_ring_state_t"></a> <a id="_CPPv233bk_hf_client_in_band_ring_state_t"></a> <a id="bk__dm__hfp__types_8h_1a362fad26fef8f6ab346991dd8c94dce9"></a> enum bk\_hf\_client\_in\_band\_ring\_state\_t
:   in-band ring tone state

    *Values:*

    <a id="_CPPv4N33bk_hf_client_in_band_ring_state_t42BK_HF_CLIENT_IN_BAND_RINGTONE_NOT_PROVIDEDE"></a>

    <a id="_CPPv3N33bk_hf_client_in_band_ring_state_t42BK_HF_CLIENT_IN_BAND_RINGTONE_NOT_PROVIDEDE"></a> <a id="_CPPv2N33bk_hf_client_in_band_ring_state_t42BK_HF_CLIENT_IN_BAND_RINGTONE_NOT_PROVIDEDE"></a> <a id="bk__dm__hfp__types_8h_1a362fad26fef8f6ab346991dd8c94dce9a5d920e7b7d87693d19578f93e91aead3"></a> enumerator BK\_HF\_CLIENT\_IN\_BAND\_RINGTONE\_NOT\_PROVIDED

    <a id="_CPPv4N33bk_hf_client_in_band_ring_state_t38BK_HF_CLIENT_IN_BAND_RINGTONE_PROVIDEDE"></a>

    <a id="_CPPv3N33bk_hf_client_in_band_ring_state_t38BK_HF_CLIENT_IN_BAND_RINGTONE_PROVIDEDE"></a> <a id="_CPPv2N33bk_hf_client_in_band_ring_state_t38BK_HF_CLIENT_IN_BAND_RINGTONE_PROVIDEDE"></a> <a id="bk__dm__hfp__types_8h_1a362fad26fef8f6ab346991dd8c94dce9ac6879afe145bce36409f5226bb907101"></a> enumerator BK\_HF\_CLIENT\_IN\_BAND\_RINGTONE\_PROVIDED

<a id="bk-dm-gap-bt-types-h"></a>

## bk\_dm\_gap\_bt\_types.h

`bk_dm_gap_bt_types.h` 定义 BT GAP 使用的设备、配对和连接相关类型。

<a id="id46"></a>

### Header File

- [bk\_dm\_gap\_bt\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_dm_gap_bt_types.h)

<a id="id47"></a>

### Unions

<a id="_CPPv411bk_bt_cod_t"></a>

<a id="_CPPv311bk_bt_cod_t"></a> <a id="_CPPv211bk_bt_cod_t"></a> <a id="unionbk__bt__cod__t"></a> union bk\_bt\_cod\_t
:   *#include \<bk\_dm\_gap\_bt\_types.h\>*

    Class of device.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N11bk_bt_cod_t5cod_tE"></a>

    <a id="_CPPv3N11bk_bt_cod_t5cod_tE"></a> <a id="_CPPv2N11bk_bt_cod_t5cod_tE"></a> <a id="bk_bt_cod_t::cod_t__bk_bt_cod_t::class_of_device"></a> <a id="unionbk__bt__cod__t_1ad39da20844ee9e3e21603504e409b393"></a> struct [bk\_bt\_cod\_t](#_CPPv411bk_bt_cod_t "bk_bt_cod_t")::[class\_of\_device](#_CPPv4N11bk_bt_cod_t15class_of_deviceE "bk_bt_cod_t::class_of_device") cod\_t

    <a id="_CPPv4N11bk_bt_cod_t3codE"></a>

    <a id="_CPPv3N11bk_bt_cod_t3codE"></a> <a id="_CPPv2N11bk_bt_cod_t3codE"></a> <a id="bk_bt_cod_t::cod__uint32_t"></a> <a id="unionbk__bt__cod__t_1a082b27e21a5c4c518cc9036a17bb5f92"></a> uint32\_t cod

    <a id="_CPPv4N11bk_bt_cod_t15class_of_deviceE"></a>

    <a id="_CPPv3N11bk_bt_cod_t15class_of_deviceE"></a> <a id="_CPPv2N11bk_bt_cod_t15class_of_deviceE"></a> <a id="bk_bt_cod_t::class_of_device"></a> <a id="structbk__bt__cod__t_1_1class__of__device"></a> struct class\_of\_device
    :   <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N11bk_bt_cod_t15class_of_device10reserved_2E"></a>

        <a id="_CPPv3N11bk_bt_cod_t15class_of_device10reserved_2E"></a> <a id="_CPPv2N11bk_bt_cod_t15class_of_device10reserved_2E"></a> <a id="bk_bt_cod_t::class_of_device::reserved_2__uint32_t"></a> <a id="structbk__bt__cod__t_1_1class__of__device_1a755b03838c8fbc0254021bd09ad5fb95"></a> uint32\_t reserved\_2
        :   reserved

        <a id="_CPPv4N11bk_bt_cod_t15class_of_device5minorE"></a>

        <a id="_CPPv3N11bk_bt_cod_t15class_of_device5minorE"></a> <a id="_CPPv2N11bk_bt_cod_t15class_of_device5minorE"></a> <a id="bk_bt_cod_t::class_of_device::minor__uint32_t"></a> <a id="structbk__bt__cod__t_1_1class__of__device_1a317b009c6720508fa321d3d5c7482fa1"></a> uint32\_t minor
        :   minor class

        <a id="_CPPv4N11bk_bt_cod_t15class_of_device5majorE"></a>

        <a id="_CPPv3N11bk_bt_cod_t15class_of_device5majorE"></a> <a id="_CPPv2N11bk_bt_cod_t15class_of_device5majorE"></a> <a id="bk_bt_cod_t::class_of_device::major__uint32_t"></a> <a id="structbk__bt__cod__t_1_1class__of__device_1a620bab1741477c5ffdc7f379774097a2"></a> uint32\_t major
        :   major class

        <a id="_CPPv4N11bk_bt_cod_t15class_of_device7serviceE"></a>

        <a id="_CPPv3N11bk_bt_cod_t15class_of_device7serviceE"></a> <a id="_CPPv2N11bk_bt_cod_t15class_of_device7serviceE"></a> <a id="bk_bt_cod_t::class_of_device::service__uint32_t"></a> <a id="structbk__bt__cod__t_1_1class__of__device_1a274770e8abb07ff7f5a8f4f875f4461e"></a> uint32\_t service
        :   service class

        <a id="_CPPv4N11bk_bt_cod_t15class_of_device10reserved_8E"></a>

        <a id="_CPPv3N11bk_bt_cod_t15class_of_device10reserved_8E"></a> <a id="_CPPv2N11bk_bt_cod_t15class_of_device10reserved_8E"></a> <a id="bk_bt_cod_t::class_of_device::reserved_8__uint32_t"></a> <a id="structbk__bt__cod__t_1_1class__of__device_1af586b04c1cad4d4c562acf2de1ae0e69"></a> uint32\_t reserved\_8
        :   reserved

<a id="_CPPv420bk_bt_gap_cb_param_t"></a>

<a id="_CPPv320bk_bt_gap_cb_param_t"></a> <a id="_CPPv220bk_bt_gap_cb_param_t"></a> <a id="unionbk__bt__gap__cb__param__t"></a> union bk\_bt\_gap\_cb\_param\_t
:   *#include \<bk\_dm\_gap\_bt\_types.h\>*

    GAP state callback parameters.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20bk_bt_gap_cb_param_t8disc_resE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t8disc_resE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t8disc_resE"></a> <a id="bk_bt_gap_cb_param_t::disc_res__bk_bt_gap_cb_param_t::disc_res_param"></a> <a id="unionbk__bt__gap__cb__param__t_1ab97f67c8b6475e661f473f105fed5eba"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[disc\_res\_param](#_CPPv4N20bk_bt_gap_cb_param_t14disc_res_paramE "bk_bt_gap_cb_param_t::disc_res_param") disc\_res
    :   discovery result parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t11disc_st_chgE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t11disc_st_chgE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t11disc_st_chgE"></a> <a id="bk_bt_gap_cb_param_t::disc_st_chg__bk_bt_gap_cb_param_t::disc_state_changed_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a6e6bdd166d802868fb516fd604bef231"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[disc\_state\_changed\_param](#_CPPv4N20bk_bt_gap_cb_param_t24disc_state_changed_paramE "bk_bt_gap_cb_param_t::disc_state_changed_param") disc\_st\_chg
    :   discovery state changed parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t9rmt_srvcsE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t9rmt_srvcsE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t9rmt_srvcsE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvcs__bk_bt_gap_cb_param_t::rmt_srvcs_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a13278eb7465c65138f294f91549b59f5"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[rmt\_srvcs\_param](#_CPPv4N20bk_bt_gap_cb_param_t15rmt_srvcs_paramE "bk_bt_gap_cb_param_t::rmt_srvcs_param") rmt\_srvcs
    :   services of remote device parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t12rmt_srvc_recE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t12rmt_srvc_recE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t12rmt_srvc_recE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvc_rec__bk_bt_gap_cb_param_t::rmt_srvc_rec_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a5d5a5374e4463b2e736822b6862bca27"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[rmt\_srvc\_rec\_param](#_CPPv4N20bk_bt_gap_cb_param_t18rmt_srvc_rec_paramE "bk_bt_gap_cb_param_t::rmt_srvc_rec_param") rmt\_srvc\_rec
    :   specific service record from remote device parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t15read_rssi_deltaE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t15read_rssi_deltaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15read_rssi_deltaE"></a> <a id="bk_bt_gap_cb_param_t::read_rssi_delta__bk_bt_gap_cb_param_t::read_rssi_delta_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a1af3d07bf8283d48c79a818fcbc34832"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[read\_rssi\_delta\_param](#_CPPv4N20bk_bt_gap_cb_param_t21read_rssi_delta_paramE "bk_bt_gap_cb_param_t::read_rssi_delta_param") read\_rssi\_delta
    :   read rssi parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t15config_eir_dataE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t15config_eir_dataE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15config_eir_dataE"></a> <a id="bk_bt_gap_cb_param_t::config_eir_data__bk_bt_gap_cb_param_t::config_eir_data_param"></a> <a id="unionbk__bt__gap__cb__param__t_1aa3b7a5e40a07a0c4ba0992f996762693"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[config\_eir\_data\_param](#_CPPv4N20bk_bt_gap_cb_param_t21config_eir_data_paramE "bk_bt_gap_cb_param_t::config_eir_data_param") config\_eir\_data
    :   config EIR data

    <a id="_CPPv4N20bk_bt_gap_cb_param_t9auth_cmplE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t9auth_cmplE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t9auth_cmplE"></a> <a id="bk_bt_gap_cb_param_t::auth_cmpl__bk_bt_gap_cb_param_t::auth_cmpl_param"></a> <a id="unionbk__bt__gap__cb__param__t_1ae9b01395247f8413f1e1a4acdb6dc78a"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[auth\_cmpl\_param](#_CPPv4N20bk_bt_gap_cb_param_t15auth_cmpl_paramE "bk_bt_gap_cb_param_t::auth_cmpl_param") auth\_cmpl
    :   authentication complete parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t17encryption_changeE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t17encryption_changeE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t17encryption_changeE"></a> <a id="bk_bt_gap_cb_param_t::encryption_change__bk_bt_gap_cb_param_t::encryption_change_param"></a> <a id="unionbk__bt__gap__cb__param__t_1ab3abd55a916adccd056ada4d4150b956"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[encryption\_change\_param](#_CPPv4N20bk_bt_gap_cb_param_t23encryption_change_paramE "bk_bt_gap_cb_param_t::encryption_change_param") encryption\_change

    <a id="_CPPv4N20bk_bt_gap_cb_param_t7pin_reqE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t7pin_reqE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t7pin_reqE"></a> <a id="bk_bt_gap_cb_param_t::pin_req__bk_bt_gap_cb_param_t::pin_req_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a9eec30a42ae70298bde7ea012fa650b0"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[pin\_req\_param](#_CPPv4N20bk_bt_gap_cb_param_t13pin_req_paramE "bk_bt_gap_cb_param_t::pin_req_param") pin\_req
    :   pin request parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t7cfm_reqE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t7cfm_reqE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t7cfm_reqE"></a> <a id="bk_bt_gap_cb_param_t::cfm_req__bk_bt_gap_cb_param_t::cfm_req_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a4681dae3b071bfa4fda29c32feba6748"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[cfm\_req\_param](#_CPPv4N20bk_bt_gap_cb_param_t13cfm_req_paramE "bk_bt_gap_cb_param_t::cfm_req_param") cfm\_req
    :   confirm request parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t9key_notifE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t9key_notifE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t9key_notifE"></a> <a id="bk_bt_gap_cb_param_t::key_notif__bk_bt_gap_cb_param_t::key_notif_param"></a> <a id="unionbk__bt__gap__cb__param__t_1abdc8dbbf165695d9a9b73caf57bbc76a"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[key\_notif\_param](#_CPPv4N20bk_bt_gap_cb_param_t15key_notif_paramE "bk_bt_gap_cb_param_t::key_notif_param") key\_notif
    :   passkey notif parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t7key_reqE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t7key_reqE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t7key_reqE"></a> <a id="bk_bt_gap_cb_param_t::key_req__bk_bt_gap_cb_param_t::key_req_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a49cb64bd7a9208fc928ec607418b443f"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[key\_req\_param](#_CPPv4N20bk_bt_gap_cb_param_t13key_req_paramE "bk_bt_gap_cb_param_t::key_req_param") key\_req
    :   passkey request parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t16set_afh_channelsE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t16set_afh_channelsE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t16set_afh_channelsE"></a> <a id="bk_bt_gap_cb_param_t::set_afh_channels__bk_bt_gap_cb_param_t::set_afh_channels_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a6154745725b0989d90cc977e0ebcdc81"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[set\_afh\_channels\_param](#_CPPv4N20bk_bt_gap_cb_param_t22set_afh_channels_paramE "bk_bt_gap_cb_param_t::set_afh_channels_param") set\_afh\_channels
    :   set AFH channel parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t13read_rmt_nameE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t13read_rmt_nameE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t13read_rmt_nameE"></a> <a id="bk_bt_gap_cb_param_t::read_rmt_name__bk_bt_gap_cb_param_t::read_rmt_name_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a42724806ca0cddca286d46b04dd211dc"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[read\_rmt\_name\_param](#_CPPv4N20bk_bt_gap_cb_param_t19read_rmt_name_paramE "bk_bt_gap_cb_param_t::read_rmt_name_param") read\_rmt\_name
    :   read Remote Name parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t8mode_chgE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t8mode_chgE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t8mode_chgE"></a> <a id="bk_bt_gap_cb_param_t::mode_chg__bk_bt_gap_cb_param_t::mode_chg_param"></a> <a id="unionbk__bt__gap__cb__param__t_1ac7538793d3b918b6a3873fc24c26e371"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[mode\_chg\_param](#_CPPv4N20bk_bt_gap_cb_param_t14mode_chg_paramE "bk_bt_gap_cb_param_t::mode_chg_param") mode\_chg
    :   mode change event parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t20remove_bond_dev_cmplE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t20remove_bond_dev_cmplE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20remove_bond_dev_cmplE"></a> <a id="bk_bt_gap_cb_param_t::remove_bond_dev_cmpl__bk_bt_gap_cb_param_t::bt_remove_bond_dev_cmpl_evt_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a09c1356bd320adf38dd8fd3fb1cbd029"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[bt\_remove\_bond\_dev\_cmpl\_evt\_param](#_CPPv4N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_paramE "bk_bt_gap_cb_param_t::bt_remove_bond_dev_cmpl_evt_param") remove\_bond\_dev\_cmpl
    :   Event parameter of BK\_BT\_GAP\_REMOVE\_BOND\_DEV\_COMPLETE\_EVT

    <a id="_CPPv4N20bk_bt_gap_cb_param_t8qos_cmplE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t8qos_cmplE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t8qos_cmplE"></a> <a id="bk_bt_gap_cb_param_t::qos_cmpl__bk_bt_gap_cb_param_t::qos_cmpl_param"></a> <a id="unionbk__bt__gap__cb__param__t_1ac408a34bfc2c4d5101e7253e6bf692f7"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[qos\_cmpl\_param](#_CPPv4N20bk_bt_gap_cb_param_t14qos_cmpl_paramE "bk_bt_gap_cb_param_t::qos_cmpl_param") qos\_cmpl
    :   QoS complete parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t18acl_conn_cmpl_statE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t18acl_conn_cmpl_statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t18acl_conn_cmpl_statE"></a> <a id="bk_bt_gap_cb_param_t::acl_conn_cmpl_stat__bk_bt_gap_cb_param_t::acl_conn_cmpl_stat_param"></a> <a id="unionbk__bt__gap__cb__param__t_1ac2b7f1cf02b8d268abc42a8cd2ade3b5"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[acl\_conn\_cmpl\_stat\_param](#_CPPv4N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_paramE "bk_bt_gap_cb_param_t::acl_conn_cmpl_stat_param") acl\_conn\_cmpl\_stat
    :   ACL connection complete status parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t21acl_disconn_cmpl_statE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t21acl_disconn_cmpl_statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21acl_disconn_cmpl_statE"></a> <a id="bk_bt_gap_cb_param_t::acl_disconn_cmpl_stat__bk_bt_gap_cb_param_t::acl_disconn_cmpl_stat_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a5e64c0a5a298fa9bc38dbf8cca4f713a"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[acl\_disconn\_cmpl\_stat\_param](#_CPPv4N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_paramE "bk_bt_gap_cb_param_t::acl_disconn_cmpl_stat_param") acl\_disconn\_cmpl\_stat
    :   ACL disconnection complete status parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t14link_key_notifE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t14link_key_notifE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14link_key_notifE"></a> <a id="bk_bt_gap_cb_param_t::link_key_notif__bk_bt_gap_cb_param_t::link_key_notif_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a93b9f1a3559b94527078d82e669fa6a5"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[link\_key\_notif\_param](#_CPPv4N20bk_bt_gap_cb_param_t20link_key_notif_paramE "bk_bt_gap_cb_param_t::link_key_notif_param") link\_key\_notif
    :   link key notif parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t12link_key_reqE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t12link_key_reqE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t12link_key_reqE"></a> <a id="bk_bt_gap_cb_param_t::link_key_req__bk_bt_gap_cb_param_t::link_key_req_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a605efef20b7cb923fbc6057cd9f35008"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[link\_key\_req\_param](#_CPPv4N20bk_bt_gap_cb_param_t18link_key_req_paramE "bk_bt_gap_cb_param_t::link_key_req_param") link\_key\_req
    :   link key request parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t15auto_sniff_cmplE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t15auto_sniff_cmplE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15auto_sniff_cmplE"></a> <a id="bk_bt_gap_cb_param_t::auto_sniff_cmpl__bk_bt_gap_cb_param_t::auto_sniff_cmpl_param"></a> <a id="unionbk__bt__gap__cb__param__t_1ae6f30fa767e65e5be9c69f19e0e5247b"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[auto\_sniff\_cmpl\_param](#_CPPv4N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_paramE "bk_bt_gap_cb_param_t::auto_sniff_cmpl_param") auto\_sniff\_cmpl

    <a id="_CPPv4N20bk_bt_gap_cb_param_t8role_chgE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t8role_chgE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t8role_chgE"></a> <a id="bk_bt_gap_cb_param_t::role_chg__bk_bt_gap_cb_param_t::role_chg_param"></a> <a id="unionbk__bt__gap__cb__param__t_1a5cc3834712367ba508435dc50a609155"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[role\_chg\_param](#_CPPv4N20bk_bt_gap_cb_param_t14role_chg_paramE "bk_bt_gap_cb_param_t::role_chg_param") role\_chg
    :   role change event parameter struct

    <a id="_CPPv4N20bk_bt_gap_cb_param_t14connection_reqE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t14connection_reqE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14connection_reqE"></a> <a id="bk_bt_gap_cb_param_t::connection_req__bk_bt_gap_cb_param_t::connection_req_param"></a> <a id="unionbk__bt__gap__cb__param__t_1ab38b0c1c037ed2d8b74876a0753ade6d"></a> struct [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t")::[connection\_req\_param](#_CPPv4N20bk_bt_gap_cb_param_t20connection_req_paramE "bk_bt_gap_cb_param_t::connection_req_param") connection\_req

    <a id="_CPPv4N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_paramE"></a> <a id="bk_bt_gap_cb_param_t::acl_conn_cmpl_stat_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1acl__conn__cmpl__stat__param"></a> struct acl\_conn\_cmpl\_stat\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_ACL\_CONN\_CMPL\_STAT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param4statE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param4statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param4statE"></a> <a id="bk_bt_gap_cb_param_t::acl_conn_cmpl_stat_param::stat__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1acl__conn__cmpl__stat__param_1a96ced42918a1e4ccbacd47b5dff10ec3"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   ACL connection status

        <a id="_CPPv4N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param6handleE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param6handleE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param6handleE"></a> <a id="bk_bt_gap_cb_param_t::acl_conn_cmpl_stat_param::handle__uint16_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1acl__conn__cmpl__stat__param_1af4537d55193e547d9ccc839185e46b29"></a> uint16\_t handle
        :   ACL connection handle

        <a id="_CPPv4N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::acl_conn_cmpl_stat_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1acl__conn__cmpl__stat__param_1a264e1252e2becc54f21f0fda38a8a205"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param3codE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param3codE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t24acl_conn_cmpl_stat_param3codE"></a> <a id="bk_bt_gap_cb_param_t::acl_conn_cmpl_stat_param::cod__uint32_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1acl__conn__cmpl__stat__param_1a01cf85f0bd4c4edc4697225b8fb58a2f"></a> uint32\_t cod
        :   Class of Device for remote bluetooth device, it is only valid when paged by remote bluetooth device

    <a id="_CPPv4N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_paramE"></a> <a id="bk_bt_gap_cb_param_t::acl_disconn_cmpl_stat_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1acl__disconn__cmpl__stat__param"></a> struct acl\_disconn\_cmpl\_stat\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_ACL\_DISCONN\_CMPL\_STAT\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_param6reasonE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_param6reasonE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_param6reasonE"></a> <a id="bk_bt_gap_cb_param_t::acl_disconn_cmpl_stat_param::reason__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1acl__disconn__cmpl__stat__param_1a560f6841facce569a0e7436ca06f0780"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") reason
        :   ACL disconnection reason

        <a id="_CPPv4N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_param6handleE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_param6handleE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_param6handleE"></a> <a id="bk_bt_gap_cb_param_t::acl_disconn_cmpl_stat_param::handle__uint16_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1acl__disconn__cmpl__stat__param_1a3f03f2faf64342b4700fb4a403eececf"></a> uint16\_t handle
        :   ACL connection handle

        <a id="_CPPv4N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t27acl_disconn_cmpl_stat_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::acl_disconn_cmpl_stat_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1acl__disconn__cmpl__stat__param_1af1b2444ce94b8b791fe2c2523ed90959"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

    <a id="_CPPv4N20bk_bt_gap_cb_param_t15auth_cmpl_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t15auth_cmpl_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15auth_cmpl_paramE"></a> <a id="bk_bt_gap_cb_param_t::auth_cmpl_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1auth__cmpl__param"></a> struct auth\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_AUTH\_CMPL\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t15auth_cmpl_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t15auth_cmpl_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15auth_cmpl_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::auth_cmpl_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1auth__cmpl__param_1a6ef8f655ce4be208f31cee3dd8051622"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t15auth_cmpl_param4statE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t15auth_cmpl_param4statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15auth_cmpl_param4statE"></a> <a id="bk_bt_gap_cb_param_t::auth_cmpl_param::stat__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1auth__cmpl__param_1a95b7dfd89d2bfe354b4b7606904987c3"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   authentication complete status

    <a id="_CPPv4N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_paramE"></a> <a id="bk_bt_gap_cb_param_t::auto_sniff_cmpl_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1auto__sniff__cmpl__param"></a> struct auto\_sniff\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_SET\_AUTO\_SNIFF\_CMPL\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::auto_sniff_cmpl_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1auto__sniff__cmpl__param_1a09d6490e47e252b773915488225d1f54"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda

        <a id="_CPPv4N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_param6resultE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_param6resultE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21auto_sniff_cmpl_param6resultE"></a> <a id="bk_bt_gap_cb_param_t::auto_sniff_cmpl_param::result__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1auto__sniff__cmpl__param_1a14e02d919cbfc6ec726533bf7aac6877"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") result
        :   peer addr

    <a id="_CPPv4N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_paramE"></a> <a id="bk_bt_gap_cb_param_t::bt_remove_bond_dev_cmpl_evt_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1bt__remove__bond__dev__cmpl__evt__param"></a> struct bt\_remove\_bond\_dev\_cmpl\_evt\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_REMOVE\_BOND\_DEV\_COMPLETE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::bt_remove_bond_dev_cmpl_evt_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1bt__remove__bond__dev__cmpl__evt__param_1a35af3bc537da78b38192c4628b7b2532"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_param6statusE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_param6statusE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t33bt_remove_bond_dev_cmpl_evt_param6statusE"></a> <a id="bk_bt_gap_cb_param_t::bt_remove_bond_dev_cmpl_evt_param::status__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1bt__remove__bond__dev__cmpl__evt__param_1a1530fcf034cbc577cfd034216c9de7b0"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   Indicate the remove bond device operation success status

    <a id="_CPPv4N20bk_bt_gap_cb_param_t13cfm_req_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t13cfm_req_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t13cfm_req_paramE"></a> <a id="bk_bt_gap_cb_param_t::cfm_req_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1cfm__req__param"></a> struct cfm\_req\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_CFM\_REQ\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t13cfm_req_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t13cfm_req_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t13cfm_req_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::cfm_req_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1cfm__req__param_1abb86b36f03f46293771f12bce58ad601"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t13cfm_req_param7num_valE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t13cfm_req_param7num_valE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t13cfm_req_param7num_valE"></a> <a id="bk_bt_gap_cb_param_t::cfm_req_param::num_val__uint32_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1cfm__req__param_1a1d2354640acbc4c6ff5ebf8d9ca597fc"></a> uint32\_t num\_val
        :   the numeric value for comparison.

    <a id="_CPPv4N20bk_bt_gap_cb_param_t21config_eir_data_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t21config_eir_data_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21config_eir_data_paramE"></a> <a id="bk_bt_gap_cb_param_t::config_eir_data_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1config__eir__data__param"></a> struct config\_eir\_data\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_CONFIG\_EIR\_DATA\_EVT \*.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t21config_eir_data_param4statE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t21config_eir_data_param4statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21config_eir_data_param4statE"></a> <a id="bk_bt_gap_cb_param_t::config_eir_data_param::stat__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1config__eir__data__param_1a11ccbe8f7cb5272e37eb40cd8feafa1a"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   config EIR status: BK\_BT\_STATUS\_SUCCESS: config success BK\_BT\_STATUS\_EIR\_TOO\_LARGE: the EIR data is more than 240B. The EIR may not contain the whole data. others: failed

        <a id="_CPPv4N20bk_bt_gap_cb_param_t21config_eir_data_param12eir_type_numE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t21config_eir_data_param12eir_type_numE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21config_eir_data_param12eir_type_numE"></a> <a id="bk_bt_gap_cb_param_t::config_eir_data_param::eir_type_num__uint8_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1config__eir__data__param_1adc0d5b3a67cb231782122810fd174d08"></a> uint8\_t eir\_type\_num
        :   the number of EIR types in EIR type

        <a id="_CPPv4N20bk_bt_gap_cb_param_t21config_eir_data_param8eir_typeE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t21config_eir_data_param8eir_typeE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21config_eir_data_param8eir_typeE"></a> <a id="bk_bt_gap_cb_param_t::config_eir_data_param::eir_type__bk_bt_eir_type_tA"></a> <a id="structbk__bt__gap__cb__param__t_1_1config__eir__data__param_1a971bca929a979b5bc6409526fd273a79"></a> [bk\_bt\_eir\_type\_t](#_CPPv416bk_bt_eir_type_t "bk_bt_eir_type_t") eir\_type\[BK\_BT\_EIR\_TYPE\_MAX\_NUM\]
        :   EIR types in EIR type

    <a id="_CPPv4N20bk_bt_gap_cb_param_t20connection_req_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t20connection_req_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20connection_req_paramE"></a> <a id="bk_bt_gap_cb_param_t::connection_req_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1connection__req__param"></a> struct connection\_req\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_CONNECTION\_REQ\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t20connection_req_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t20connection_req_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20connection_req_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::connection_req_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1connection__req__param_1a7aea46fad1140c264e7020c6b71d1ea2"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda

        <a id="_CPPv4N20bk_bt_gap_cb_param_t20connection_req_param4typeE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t20connection_req_param4typeE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20connection_req_param4typeE"></a> <a id="bk_bt_gap_cb_param_t::connection_req_param::type__uint8_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1connection__req__param_1aec612c8d64c3f1892908498182ed778b"></a> uint8\_t type
        :   peer addr

        <a id="_CPPv4N20bk_bt_gap_cb_param_t20connection_req_param3codE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t20connection_req_param3codE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20connection_req_param3codE"></a> <a id="bk_bt_gap_cb_param_t::connection_req_param::cod__bk_bt_cod_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1connection__req__param_1abef5d021c41f687adf567a09861efe28"></a> [bk\_bt\_cod\_t](#_CPPv411bk_bt_cod_t "bk_bt_cod_t") cod
        :   0 sco 1 acl 2 esco

        <a id="_CPPv4N20bk_bt_gap_cb_param_t20connection_req_param6acceptE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t20connection_req_param6acceptE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20connection_req_param6acceptE"></a> <a id="bk_bt_gap_cb_param_t::connection_req_param::accept__uint8_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1connection__req__param_1a05201b622b0355145b69d34f1e601e7a"></a> uint8\_t accept

        <a id="_CPPv4N20bk_bt_gap_cb_param_t20connection_req_param13reject_reasonE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t20connection_req_param13reject_reasonE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20connection_req_param13reject_reasonE"></a> <a id="bk_bt_gap_cb_param_t::connection_req_param::reject_reason__uint8_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1connection__req__param_1aa47d4d38d813d8082b1077d772d5ae02"></a> uint8\_t reject\_reason

    <a id="_CPPv4N20bk_bt_gap_cb_param_t14disc_res_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t14disc_res_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14disc_res_paramE"></a> <a id="bk_bt_gap_cb_param_t::disc_res_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1disc__res__param"></a> struct disc\_res\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_DISC\_RES\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14disc_res_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14disc_res_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14disc_res_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::disc_res_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1disc__res__param_1a336eaf56433e1ba03ceb27f7e83f7efb"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14disc_res_param8num_propE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14disc_res_param8num_propE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14disc_res_param8num_propE"></a> <a id="bk_bt_gap_cb_param_t::disc_res_param::num_prop__i"></a> <a id="structbk__bt__gap__cb__param__t_1_1disc__res__param_1a50b5b3077c9c262b97fdbdf095a332a5"></a> int num\_prop
        :   number of properties got

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14disc_res_param4propE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14disc_res_param4propE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14disc_res_param4propE"></a> <a id="bk_bt_gap_cb_param_t::disc_res_param::prop__bk_bt_gap_dev_prop_tP"></a> <a id="structbk__bt__gap__cb__param__t_1_1disc__res__param_1a21eb68cf60ef9504bf48f0606d975f4b"></a> [bk\_bt\_gap\_dev\_prop\_t](#_CPPv420bk_bt_gap_dev_prop_t "bk_bt_gap_dev_prop_t") \*prop
        :   properties discovered from the new device

    <a id="_CPPv4N20bk_bt_gap_cb_param_t24disc_state_changed_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t24disc_state_changed_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t24disc_state_changed_paramE"></a> <a id="bk_bt_gap_cb_param_t::disc_state_changed_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1disc__state__changed__param"></a> struct disc\_state\_changed\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_DISC\_STATE\_CHANGED\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t24disc_state_changed_param5stateE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t24disc_state_changed_param5stateE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t24disc_state_changed_param5stateE"></a> <a id="bk_bt_gap_cb_param_t::disc_state_changed_param::state__bk_bt_gap_discovery_state_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1disc__state__changed__param_1a146672efae0c5979201e731c19bb71fa"></a> [bk\_bt\_gap\_discovery\_state\_t](#_CPPv427bk_bt_gap_discovery_state_t "bk_bt_gap_discovery_state_t") state
        :   discovery state

    <a id="_CPPv4N20bk_bt_gap_cb_param_t23encryption_change_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t23encryption_change_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t23encryption_change_paramE"></a> <a id="bk_bt_gap_cb_param_t::encryption_change_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1encryption__change__param"></a> struct encryption\_change\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_ENCRYPTION\_CHANGE\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t23encryption_change_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t23encryption_change_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t23encryption_change_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::encryption_change_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1encryption__change__param_1a910938aede7f5c38fa2bcc873a127f00"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t23encryption_change_param6statusE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t23encryption_change_param6statusE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t23encryption_change_param6statusE"></a> <a id="bk_bt_gap_cb_param_t::encryption_change_param::status__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1encryption__change__param_1a450b2cf39610a49d47dc6baed1e1ad42"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") status
        :   HCI encryption change status

        <a id="_CPPv4N20bk_bt_gap_cb_param_t23encryption_change_param9encryptedE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t23encryption_change_param9encryptedE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t23encryption_change_param9encryptedE"></a> <a id="bk_bt_gap_cb_param_t::encryption_change_param::encrypted__uint8_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1encryption__change__param_1a61465e399901a5065112f51bd30db153"></a> uint8\_t encrypted
        :   0: encryption off, nonzero: encryption on

    <a id="_CPPv4N20bk_bt_gap_cb_param_t15key_notif_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t15key_notif_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15key_notif_paramE"></a> <a id="bk_bt_gap_cb_param_t::key_notif_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1key__notif__param"></a> struct key\_notif\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_KEY\_NOTIF\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t15key_notif_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t15key_notif_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15key_notif_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::key_notif_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1key__notif__param_1a63912787cf2019c4c35de0560abfefee"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t15key_notif_param7passkeyE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t15key_notif_param7passkeyE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15key_notif_param7passkeyE"></a> <a id="bk_bt_gap_cb_param_t::key_notif_param::passkey__uint32_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1key__notif__param_1ad455ee50f879d50465517336bc029f1c"></a> uint32\_t passkey
        :   the numeric value for passkey entry.

    <a id="_CPPv4N20bk_bt_gap_cb_param_t13key_req_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t13key_req_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t13key_req_paramE"></a> <a id="bk_bt_gap_cb_param_t::key_req_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1key__req__param"></a> struct key\_req\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_KEY\_REQ\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t13key_req_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t13key_req_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t13key_req_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::key_req_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1key__req__param_1a716e1b445541b637d2bd6eee8b6fa6dd"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

    <a id="_CPPv4N20bk_bt_gap_cb_param_t20link_key_notif_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t20link_key_notif_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20link_key_notif_paramE"></a> <a id="bk_bt_gap_cb_param_t::link_key_notif_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1link__key__notif__param"></a> struct link\_key\_notif\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_LINK\_KEY\_NOTIF\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t20link_key_notif_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t20link_key_notif_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20link_key_notif_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::link_key_notif_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1link__key__notif__param_1a8a1f11be7a84ce639ce36f34c5f09e13"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t20link_key_notif_param8link_keyE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t20link_key_notif_param8link_keyE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t20link_key_notif_param8link_keyE"></a> <a id="bk_bt_gap_cb_param_t::link_key_notif_param::link_key__uint8_tA"></a> <a id="structbk__bt__gap__cb__param__t_1_1link__key__notif__param_1addeec77f75b6074f84e644d9071bcf54"></a> uint8\_t link\_key\[16\]
        :   Link Key for the associated bda.

    <a id="_CPPv4N20bk_bt_gap_cb_param_t18link_key_req_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t18link_key_req_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t18link_key_req_paramE"></a> <a id="bk_bt_gap_cb_param_t::link_key_req_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1link__key__req__param"></a> struct link\_key\_req\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_LINK\_KEY\_REQ\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t18link_key_req_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t18link_key_req_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t18link_key_req_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::link_key_req_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1link__key__req__param_1a1290a26bebb3a58f188b98ccbc367f22"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

    <a id="_CPPv4N20bk_bt_gap_cb_param_t14mode_chg_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t14mode_chg_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14mode_chg_paramE"></a> <a id="bk_bt_gap_cb_param_t::mode_chg_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1mode__chg__param"></a> struct mode\_chg\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_MODE\_CHG\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14mode_chg_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14mode_chg_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14mode_chg_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::mode_chg_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1mode__chg__param_1a8b9f27f9e0dc1150a6b74ab1b6eaaee0"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14mode_chg_param4modeE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14mode_chg_param4modeE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14mode_chg_param4modeE"></a> <a id="bk_bt_gap_cb_param_t::mode_chg_param::mode__bk_bt_pm_mode_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1mode__chg__param_1a6b9dcc07100488cdfbad745391c95ea6"></a> [bk\_bt\_pm\_mode\_t](#_CPPv415bk_bt_pm_mode_t "bk_bt_pm_mode_t") mode
        :   PM mode

    <a id="_CPPv4N20bk_bt_gap_cb_param_t13pin_req_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t13pin_req_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t13pin_req_paramE"></a> <a id="bk_bt_gap_cb_param_t::pin_req_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1pin__req__param"></a> struct pin\_req\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_PIN\_REQ\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t13pin_req_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t13pin_req_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t13pin_req_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::pin_req_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1pin__req__param_1a4e32af364446593a7e0f597c09d14ea6"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t13pin_req_param12min_16_digitE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t13pin_req_param12min_16_digitE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t13pin_req_param12min_16_digitE"></a> <a id="bk_bt_gap_cb_param_t::pin_req_param::min_16_digit__b"></a> <a id="structbk__bt__gap__cb__param__t_1_1pin__req__param_1add4c609f54e18f6ac929160309f37758"></a> bool min\_16\_digit
        :   TRUE if the pin returned must be at least 16 digits

    <a id="_CPPv4N20bk_bt_gap_cb_param_t14qos_cmpl_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t14qos_cmpl_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14qos_cmpl_paramE"></a> <a id="bk_bt_gap_cb_param_t::qos_cmpl_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1qos__cmpl__param"></a> struct qos\_cmpl\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_QOS\_CMPL\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14qos_cmpl_param4statE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14qos_cmpl_param4statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14qos_cmpl_param4statE"></a> <a id="bk_bt_gap_cb_param_t::qos_cmpl_param::stat__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1qos__cmpl__param_1af3e3bdf0e09c9e310dee5e7e062382bd"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   QoS status

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14qos_cmpl_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14qos_cmpl_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14qos_cmpl_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::qos_cmpl_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1qos__cmpl__param_1af7e73b1fc7a019385c96ef9d137aa594"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14qos_cmpl_param6t_pollE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14qos_cmpl_param6t_pollE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14qos_cmpl_param6t_pollE"></a> <a id="bk_bt_gap_cb_param_t::qos_cmpl_param::t_poll__uint32_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1qos__cmpl__param_1a3744f65608a547fbb791c55cca9e3a9d"></a> uint32\_t t\_poll
        :   poll interval, the maximum time between transmissions which from the master to a particular slave on the ACL logical transport. unit is 0.625ms.

    <a id="_CPPv4N20bk_bt_gap_cb_param_t19read_rmt_name_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t19read_rmt_name_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t19read_rmt_name_paramE"></a> <a id="bk_bt_gap_cb_param_t::read_rmt_name_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1read__rmt__name__param"></a> struct read\_rmt\_name\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_READ\_REMOTE\_NAME\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t19read_rmt_name_param4statE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t19read_rmt_name_param4statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t19read_rmt_name_param4statE"></a> <a id="bk_bt_gap_cb_param_t::read_rmt_name_param::stat__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1read__rmt__name__param_1a1ed082c0122809eb8c70d8d7d6b24eb4"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   read Remote Name status

        <a id="_CPPv4N20bk_bt_gap_cb_param_t19read_rmt_name_param8rmt_nameE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t19read_rmt_name_param8rmt_nameE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t19read_rmt_name_param8rmt_nameE"></a> <a id="bk_bt_gap_cb_param_t::read_rmt_name_param::rmt_name__uint8_tA"></a> <a id="structbk__bt__gap__cb__param__t_1_1read__rmt__name__param_1a7e150a2b81b4bc4a58f4b33c7c31b191"></a> uint8\_t rmt\_name\[BK\_BT\_GAP\_MAX\_BDNAME\_LEN \+ 1\]
        :   Remote device name

        <a id="_CPPv4N20bk_bt_gap_cb_param_t19read_rmt_name_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t19read_rmt_name_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t19read_rmt_name_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::read_rmt_name_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1read__rmt__name__param_1a59e9c932990519a0d5a1a1ddc3411eb0"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

    <a id="_CPPv4N20bk_bt_gap_cb_param_t21read_rssi_delta_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t21read_rssi_delta_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21read_rssi_delta_paramE"></a> <a id="bk_bt_gap_cb_param_t::read_rssi_delta_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1read__rssi__delta__param"></a> struct read\_rssi\_delta\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_READ\_RSSI\_DELTA\_EVT \*.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t21read_rssi_delta_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t21read_rssi_delta_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21read_rssi_delta_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::read_rssi_delta_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1read__rssi__delta__param_1a06ca570e80d91abc6cf58939f289e004"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t21read_rssi_delta_param4statE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t21read_rssi_delta_param4statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21read_rssi_delta_param4statE"></a> <a id="bk_bt_gap_cb_param_t::read_rssi_delta_param::stat__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1read__rssi__delta__param_1a395cd21186b6fd7003ed76536a9c0586"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   read rssi status

        <a id="_CPPv4N20bk_bt_gap_cb_param_t21read_rssi_delta_param10rssi_deltaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t21read_rssi_delta_param10rssi_deltaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t21read_rssi_delta_param10rssi_deltaE"></a> <a id="bk_bt_gap_cb_param_t::read_rssi_delta_param::rssi_delta__int8_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1read__rssi__delta__param_1a4d68caf37c88a7e839aa73030d95cec9"></a> int8\_t rssi\_delta
        :   rssi delta value range -128 \~127, The value zero indicates that the RSSI is inside the Golden Receive Power Range, the Golden Receive Power Range is from BK\_BT\_GAP\_RSSI\_LOW\_THRLD to BK\_BT\_GAP\_RSSI\_HIGH\_THRLD

    <a id="_CPPv4N20bk_bt_gap_cb_param_t18rmt_srvc_rec_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t18rmt_srvc_rec_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t18rmt_srvc_rec_paramE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvc_rec_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1rmt__srvc__rec__param"></a> struct rmt\_srvc\_rec\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_RMT\_SRVC\_REC\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t18rmt_srvc_rec_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t18rmt_srvc_rec_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t18rmt_srvc_rec_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvc_rec_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1rmt__srvc__rec__param_1a8e9eaea4dca177b7926c4335dd48a16a"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t18rmt_srvc_rec_param4statE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t18rmt_srvc_rec_param4statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t18rmt_srvc_rec_param4statE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvc_rec_param::stat__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1rmt__srvc__rec__param_1a68e8cfcc0478ee5dec86cdfe087701d8"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   service search status

    <a id="_CPPv4N20bk_bt_gap_cb_param_t15rmt_srvcs_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t15rmt_srvcs_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15rmt_srvcs_paramE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvcs_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1rmt__srvcs__param"></a> struct rmt\_srvcs\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_RMT\_SRVCS\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t15rmt_srvcs_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t15rmt_srvcs_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15rmt_srvcs_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvcs_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1rmt__srvcs__param_1adebd83f356af5bb4f0a21df08a4880e2"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t15rmt_srvcs_param4statE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t15rmt_srvcs_param4statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15rmt_srvcs_param4statE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvcs_param::stat__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1rmt__srvcs__param_1acfb1de4ca8dfa888489f354be2d24776"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   service search status

        <a id="_CPPv4N20bk_bt_gap_cb_param_t15rmt_srvcs_param9num_uuidsE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t15rmt_srvcs_param9num_uuidsE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15rmt_srvcs_param9num_uuidsE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvcs_param::num_uuids__i"></a> <a id="structbk__bt__gap__cb__param__t_1_1rmt__srvcs__param_1ae3bdc57c71b1bc5b8da518f1556d9a84"></a> int num\_uuids
        :   number of UUID in uuid\_list

        <a id="_CPPv4N20bk_bt_gap_cb_param_t15rmt_srvcs_param9uuid_listE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t15rmt_srvcs_param9uuid_listE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t15rmt_srvcs_param9uuid_listE"></a> <a id="bk_bt_gap_cb_param_t::rmt_srvcs_param::uuid_list__bk_bt_uuid_tP"></a> <a id="structbk__bt__gap__cb__param__t_1_1rmt__srvcs__param_1a2d770f40b32dda659b302160d99e5f95"></a> [bk\_bt\_uuid\_t](dual_ble.md#_CPPv412bk_bt_uuid_t "bk_bt_uuid_t") \*uuid\_list
        :   list of service UUIDs of remote device

    <a id="_CPPv4N20bk_bt_gap_cb_param_t14role_chg_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t14role_chg_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14role_chg_paramE"></a> <a id="bk_bt_gap_cb_param_t::role_chg_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1role__chg__param"></a> struct role\_chg\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_ROLE\_CHG\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14role_chg_param6statusE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14role_chg_param6statusE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14role_chg_param6statusE"></a> <a id="bk_bt_gap_cb_param_t::role_chg_param::status__uint8_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1role__chg__param_1a0291d85423332a2f2572b3eb4a457ea1"></a> uint8\_t status
        :   switch role status

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14role_chg_param3bdaE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14role_chg_param3bdaE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14role_chg_param3bdaE"></a> <a id="bk_bt_gap_cb_param_t::role_chg_param::bda__bk_bd_addr_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1role__chg__param_1acc5ce9f4a5dbcda9a2a8ab7d6e665652"></a> [bk\_bd\_addr\_t](dual_ble.md#_CPPv412bk_bd_addr_t "bk_bd_addr_t") bda
        :   remote bluetooth device address

        <a id="_CPPv4N20bk_bt_gap_cb_param_t14role_chg_param8new_roleE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t14role_chg_param8new_roleE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t14role_chg_param8new_roleE"></a> <a id="bk_bt_gap_cb_param_t::role_chg_param::new_role__uint8_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1role__chg__param_1a20d444b8dd2bec786259bcd0b3ec3588"></a> uint8\_t new\_role
        :   new role:BT\_MASTER\_ROLE or BT\_SLAVE\_ROLE

    <a id="_CPPv4N20bk_bt_gap_cb_param_t22set_afh_channels_paramE"></a>

    <a id="_CPPv3N20bk_bt_gap_cb_param_t22set_afh_channels_paramE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t22set_afh_channels_paramE"></a> <a id="bk_bt_gap_cb_param_t::set_afh_channels_param"></a> <a id="structbk__bt__gap__cb__param__t_1_1set__afh__channels__param"></a> struct set\_afh\_channels\_param
    :   *#include \<bk\_dm\_gap\_bt\_types.h\>*

        BK\_BT\_GAP\_SET\_AFH\_CHANNELS\_EVT.

        <a id="breathe-section-title-public-members"></a>

        Public Members

        <a id="_CPPv4N20bk_bt_gap_cb_param_t22set_afh_channels_param4statE"></a>

        <a id="_CPPv3N20bk_bt_gap_cb_param_t22set_afh_channels_param4statE"></a> <a id="_CPPv2N20bk_bt_gap_cb_param_t22set_afh_channels_param4statE"></a> <a id="bk_bt_gap_cb_param_t::set_afh_channels_param::stat__bk_bt_status_t"></a> <a id="structbk__bt__gap__cb__param__t_1_1set__afh__channels__param_1a009db910272e5033c1b12c6caac3d33e"></a> [bk\_bt\_status\_t](dual_ble.md#_CPPv414bk_bt_status_t "bk_bt_status_t") stat
        :   set AFH channel status

<a id="id48"></a>

### Structures

<a id="_CPPv420bk_bt_gap_dev_prop_t"></a>

<a id="_CPPv320bk_bt_gap_dev_prop_t"></a> <a id="_CPPv220bk_bt_gap_dev_prop_t"></a> <a id="bk_bt_gap_dev_prop_t"></a> <a id="structbk__bt__gap__dev__prop__t"></a> struct bk\_bt\_gap\_dev\_prop\_t
:   Bluetooth Device Property Descriptor.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20bk_bt_gap_dev_prop_t4typeE"></a>

    <a id="_CPPv3N20bk_bt_gap_dev_prop_t4typeE"></a> <a id="_CPPv2N20bk_bt_gap_dev_prop_t4typeE"></a> <a id="bk_bt_gap_dev_prop_t::type__bk_bt_gap_dev_prop_type_t"></a> <a id="structbk__bt__gap__dev__prop__t_1adc72458129c42384e54f9bce641e43ad"></a> [bk\_bt\_gap\_dev\_prop\_type\_t](#_CPPv425bk_bt_gap_dev_prop_type_t "bk_bt_gap_dev_prop_type_t") type
    :   Device property type

    <a id="_CPPv4N20bk_bt_gap_dev_prop_t3lenE"></a>

    <a id="_CPPv3N20bk_bt_gap_dev_prop_t3lenE"></a> <a id="_CPPv2N20bk_bt_gap_dev_prop_t3lenE"></a> <a id="bk_bt_gap_dev_prop_t::len__i"></a> <a id="structbk__bt__gap__dev__prop__t_1a4f43534037f62e6189e62cfc82cf698f"></a> int len
    :   Device property value length

    <a id="_CPPv4N20bk_bt_gap_dev_prop_t3valE"></a>

    <a id="_CPPv3N20bk_bt_gap_dev_prop_t3valE"></a> <a id="_CPPv2N20bk_bt_gap_dev_prop_t3valE"></a> <a id="bk_bt_gap_dev_prop_t::val__voidP"></a> <a id="structbk__bt__gap__dev__prop__t_1ae8e405f45c7eaa46469fed9c3539253e"></a> void \*val
    :   Device property value

<a id="_CPPv416bk_bt_eir_data_t"></a>

<a id="_CPPv316bk_bt_eir_data_t"></a> <a id="_CPPv216bk_bt_eir_data_t"></a> <a id="bk_bt_eir_data_t"></a> <a id="structbk__bt__eir__data__t"></a> struct bk\_bt\_eir\_data\_t
:   EIR data content, according to “Supplement to the Bluetooth Core Specification”.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16bk_bt_eir_data_t12fec_requiredE"></a>

    <a id="_CPPv3N16bk_bt_eir_data_t12fec_requiredE"></a> <a id="_CPPv2N16bk_bt_eir_data_t12fec_requiredE"></a> <a id="bk_bt_eir_data_t::fec_required__b"></a> <a id="structbk__bt__eir__data__t_1ad93af79c3114dbdc3eca063efb6497a0"></a> bool fec\_required
    :   FEC is required or not, true by default

    <a id="_CPPv4N16bk_bt_eir_data_t15include_txpowerE"></a>

    <a id="_CPPv3N16bk_bt_eir_data_t15include_txpowerE"></a> <a id="_CPPv2N16bk_bt_eir_data_t15include_txpowerE"></a> <a id="bk_bt_eir_data_t::include_txpower__b"></a> <a id="structbk__bt__eir__data__t_1a63927d8d121bb7b22e79debcd79d4853"></a> bool include\_txpower
    :   EIR data include TX power, false by default

    <a id="_CPPv4N16bk_bt_eir_data_t12include_uuidE"></a>

    <a id="_CPPv3N16bk_bt_eir_data_t12include_uuidE"></a> <a id="_CPPv2N16bk_bt_eir_data_t12include_uuidE"></a> <a id="bk_bt_eir_data_t::include_uuid__b"></a> <a id="structbk__bt__eir__data__t_1a5551f72598b64858a6b58d656e3cf2a8"></a> bool include\_uuid
    :   EIR data include UUID, false by default

    <a id="_CPPv4N16bk_bt_eir_data_t4flagE"></a>

    <a id="_CPPv3N16bk_bt_eir_data_t4flagE"></a> <a id="_CPPv2N16bk_bt_eir_data_t4flagE"></a> <a id="bk_bt_eir_data_t::flag__uint8_t"></a> <a id="structbk__bt__eir__data__t_1a967fe489bcd4120a4bb735da906ba8c0"></a> uint8\_t flag
    :   EIR flags, see BK\_BT\_EIR\_FLAG for details, EIR will not include flag if it is 0, 0 by default

    <a id="_CPPv4N16bk_bt_eir_data_t16manufacturer_lenE"></a>

    <a id="_CPPv3N16bk_bt_eir_data_t16manufacturer_lenE"></a> <a id="_CPPv2N16bk_bt_eir_data_t16manufacturer_lenE"></a> <a id="bk_bt_eir_data_t::manufacturer_len__uint16_t"></a> <a id="structbk__bt__eir__data__t_1a73083f4a2809ffe24f2a139868f395fd"></a> uint16\_t manufacturer\_len
    :   Manufacturer data length, 0 by default

    <a id="_CPPv4N16bk_bt_eir_data_t19p_manufacturer_dataE"></a>

    <a id="_CPPv3N16bk_bt_eir_data_t19p_manufacturer_dataE"></a> <a id="_CPPv2N16bk_bt_eir_data_t19p_manufacturer_dataE"></a> <a id="bk_bt_eir_data_t::p_manufacturer_data__uint8_tP"></a> <a id="structbk__bt__eir__data__t_1adf0bcf7cf425d45a1b1dd13491281c05"></a> uint8\_t \*p\_manufacturer\_data
    :   Manufacturer data point

    <a id="_CPPv4N16bk_bt_eir_data_t7url_lenE"></a>

    <a id="_CPPv3N16bk_bt_eir_data_t7url_lenE"></a> <a id="_CPPv2N16bk_bt_eir_data_t7url_lenE"></a> <a id="bk_bt_eir_data_t::url_len__uint16_t"></a> <a id="structbk__bt__eir__data__t_1a0126baf54661336b1e85cd9104bc3f50"></a> uint16\_t url\_len
    :   URL length, 0 by default

    <a id="_CPPv4N16bk_bt_eir_data_t5p_urlE"></a>

    <a id="_CPPv3N16bk_bt_eir_data_t5p_urlE"></a> <a id="_CPPv2N16bk_bt_eir_data_t5p_urlE"></a> <a id="bk_bt_eir_data_t::p_url__uint8_tP"></a> <a id="structbk__bt__eir__data__t_1a266dc6610427612631511a5e4c9e1fdc"></a> uint8\_t \*p\_url
    :   URL point

<a id="_CPPv425bk_bt_eir_raw_data_elem_t"></a>

<a id="_CPPv325bk_bt_eir_raw_data_elem_t"></a> <a id="_CPPv225bk_bt_eir_raw_data_elem_t"></a> <a id="bk_bt_eir_raw_data_elem_t"></a> <a id="structbk__bt__eir__raw__data__elem__t"></a> struct bk\_bt\_eir\_raw\_data\_elem\_t

<a id="_CPPv422bk_bt_gap_sniff_config"></a>

<a id="_CPPv322bk_bt_gap_sniff_config"></a> <a id="_CPPv222bk_bt_gap_sniff_config"></a> <a id="bk_bt_gap_sniff_config"></a> <a id="structbk__bt__gap__sniff__config"></a> struct bk\_bt\_gap\_sniff\_config
:   bt sniff config

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_bt_gap_sniff_config18sniff_min_intervalE"></a>

    <a id="_CPPv3N22bk_bt_gap_sniff_config18sniff_min_intervalE"></a> <a id="_CPPv2N22bk_bt_gap_sniff_config18sniff_min_intervalE"></a> <a id="bk_bt_gap_sniff_config::sniff_min_interval__uint16_t"></a> <a id="structbk__bt__gap__sniff__config_1acea2245dc97808e9211804e8024536f5"></a> uint16\_t sniff\_min\_interval
    :   unit 0.625ms, range: 1.25ms \~ 40.9s

    <a id="_CPPv4N22bk_bt_gap_sniff_config13sniff_attemptE"></a>

    <a id="_CPPv3N22bk_bt_gap_sniff_config13sniff_attemptE"></a> <a id="_CPPv2N22bk_bt_gap_sniff_config13sniff_attemptE"></a> <a id="bk_bt_gap_sniff_config::sniff_attempt__uint16_t"></a> <a id="structbk__bt__gap__sniff__config_1a1cf7b9e4240269f02b0fa024575cc51e"></a> uint16\_t sniff\_attempt
    :   unit 0.625ms, range: 1.25ms \~ 40.9s

    <a id="_CPPv4N22bk_bt_gap_sniff_config13sniff_timeoutE"></a>

    <a id="_CPPv3N22bk_bt_gap_sniff_config13sniff_timeoutE"></a> <a id="_CPPv2N22bk_bt_gap_sniff_config13sniff_timeoutE"></a> <a id="bk_bt_gap_sniff_config::sniff_timeout__uint16_t"></a> <a id="structbk__bt__gap__sniff__config_1a4d8d678e0ef530036f05e3246db8245f"></a> uint16\_t sniff\_timeout
    :   unit 1.25ms, range: 1.25ms \~ 40.9s

<a id="_CPPv423bk_bt_linkkey_storage_t"></a>

<a id="_CPPv323bk_bt_linkkey_storage_t"></a> <a id="_CPPv223bk_bt_linkkey_storage_t"></a> <a id="bk_bt_linkkey_storage_t"></a> <a id="structbk__bt__linkkey__storage__t"></a> struct bk\_bt\_linkkey\_storage\_t
:   bt link key storage

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23bk_bt_linkkey_storage_t4sizeE"></a>

    <a id="_CPPv3N23bk_bt_linkkey_storage_t4sizeE"></a> <a id="_CPPv2N23bk_bt_linkkey_storage_t4sizeE"></a> <a id="bk_bt_linkkey_storage_t::size__uint16_t"></a> <a id="structbk__bt__linkkey__storage__t_1a4542bd9ea086a1b8744fe133cce57cce"></a> uint16\_t size
    :   this struct size

    <a id="_CPPv4N23bk_bt_linkkey_storage_t4addrE"></a>

    <a id="_CPPv3N23bk_bt_linkkey_storage_t4addrE"></a> <a id="_CPPv2N23bk_bt_linkkey_storage_t4addrE"></a> <a id="bk_bt_linkkey_storage_t::addr__uint8_tA"></a> <a id="structbk__bt__linkkey__storage__t_1a39b79bd1ac279579e1304c43e302541c"></a> uint8\_t addr\[6\]
    :   bt addr

    <a id="_CPPv4N23bk_bt_linkkey_storage_t8link_keyE"></a>

    <a id="_CPPv3N23bk_bt_linkkey_storage_t8link_keyE"></a> <a id="_CPPv2N23bk_bt_linkkey_storage_t8link_keyE"></a> <a id="bk_bt_linkkey_storage_t::link_key__uint8_tA"></a> <a id="structbk__bt__linkkey__storage__t_1a266975b9b33f91f055463023c1dd9c5d"></a> uint8\_t link\_key\[16\]
    :   bt link key

<a id="id49"></a>

### Macros

<a id="c.BK_BT_GAP_RSSI_HIGH_THRLD"></a>

<a id="bk__dm__gap__bt__types_8h_1afa43abe4cb00896a7a9d0ea1c8b0dc93"></a> BK\_BT\_GAP\_RSSI\_HIGH\_THRLD
:   RSSI threshold.

    High RSSI threshold

<a id="c.BK_BT_GAP_RSSI_LOW_THRLD"></a>

<a id="bk__dm__gap__bt__types_8h_1a750471ab8f2a826732eb0c3c79e6d04d"></a> BK\_BT\_GAP\_RSSI\_LOW\_THRLD
:   Low RSSI threshold

<a id="c.BK_BT_GAP_AFH_CHANNELS_LEN"></a>

<a id="bk__dm__gap__bt__types_8h_1a61b16b94c4adc5123fb5c38c077e5717"></a> BK\_BT\_GAP\_AFH\_CHANNELS\_LEN

<a id="c.BK_BT_GAP_MAX_BDNAME_LEN"></a>

<a id="bk__dm__gap__bt__types_8h_1ac8b10e66a77322d40e045dfb100769e8"></a> BK\_BT\_GAP\_MAX\_BDNAME\_LEN
:   Maximum bytes of Bluetooth device name.

<a id="c.BK_BT_GAP_EIR_DATA_LEN"></a>

<a id="bk__dm__gap__bt__types_8h_1aecb38736328b8c1fd70e224c5f692e5a"></a> BK\_BT\_GAP\_EIR\_DATA\_LEN
:   Maximum size of EIR Significant part.

<a id="c.BK_BT_EIR_TYPE_FLAGS"></a>

<a id="bk__dm__gap__bt__types_8h_1afb7b4739bff133d31e14d8a4c272cbc7"></a> BK\_BT\_EIR\_TYPE\_FLAGS
:   Extended Inquiry Response data type.

    Flag with information such as BR/EDR and LE support

<a id="c.BK_BT_EIR_TYPE_INCMPL_16BITS_UUID"></a>

<a id="bk__dm__gap__bt__types_8h_1afd52089d6564427719e0e1edeba46ad3"></a> BK\_BT\_EIR\_TYPE\_INCMPL\_16BITS\_UUID
:   Incomplete list of 16-bit service UUIDs

<a id="c.BK_BT_EIR_TYPE_CMPL_16BITS_UUID"></a>

<a id="bk__dm__gap__bt__types_8h_1a5ae6ec690f89a6b5e4719a72e47bba27"></a> BK\_BT\_EIR\_TYPE\_CMPL\_16BITS\_UUID
:   Complete list of 16-bit service UUIDs

<a id="c.BK_BT_EIR_TYPE_INCMPL_32BITS_UUID"></a>

<a id="bk__dm__gap__bt__types_8h_1afe126f808b066b3346139abbf2858895"></a> BK\_BT\_EIR\_TYPE\_INCMPL\_32BITS\_UUID
:   Incomplete list of 32-bit service UUIDs

<a id="c.BK_BT_EIR_TYPE_CMPL_32BITS_UUID"></a>

<a id="bk__dm__gap__bt__types_8h_1a1c9d57400f7654e3fd86767ee40a6f16"></a> BK\_BT\_EIR\_TYPE\_CMPL\_32BITS\_UUID
:   Complete list of 32-bit service UUIDs

<a id="c.BK_BT_EIR_TYPE_INCMPL_128BITS_UUID"></a>

<a id="bk__dm__gap__bt__types_8h_1a84aef68d0d8d22b380e0a43e82e1f540"></a> BK\_BT\_EIR\_TYPE\_INCMPL\_128BITS\_UUID
:   Incomplete list of 128-bit service UUIDs

<a id="c.BK_BT_EIR_TYPE_CMPL_128BITS_UUID"></a>

<a id="bk__dm__gap__bt__types_8h_1ad562b79e6a46616c10f896aa7728eb80"></a> BK\_BT\_EIR\_TYPE\_CMPL\_128BITS\_UUID
:   Complete list of 128-bit service UUIDs

<a id="c.BK_BT_EIR_TYPE_SHORT_LOCAL_NAME"></a>

<a id="bk__dm__gap__bt__types_8h_1ad1d16bd22214c940a3d594826a4f9ed1"></a> BK\_BT\_EIR\_TYPE\_SHORT\_LOCAL\_NAME
:   Shortened Local Name

<a id="c.BK_BT_EIR_TYPE_CMPL_LOCAL_NAME"></a>

<a id="bk__dm__gap__bt__types_8h_1a8d83e8983ba5afe25675834f980a67fc"></a> BK\_BT\_EIR\_TYPE\_CMPL\_LOCAL\_NAME
:   Complete Local Name

<a id="c.BK_BT_EIR_TYPE_TX_POWER_LEVEL"></a>

<a id="bk__dm__gap__bt__types_8h_1a8852def3fb3ec9e942f67b8096ab56ba"></a> BK\_BT\_EIR\_TYPE\_TX\_POWER\_LEVEL
:   Tx power level, value is 1 octet ranging from -127 to 127, unit is dBm

<a id="c.BK_BT_EIR_TYPE_URL"></a>

<a id="bk__dm__gap__bt__types_8h_1a7a0ddcc58929a2008dfda9d6e401048b"></a> BK\_BT\_EIR\_TYPE\_URL
:   Uniform resource identifier

<a id="c.BK_BT_EIR_TYPE_MANU_SPECIFIC"></a>

<a id="bk__dm__gap__bt__types_8h_1a6588ed4c108748a9431b7be9bcd08e91"></a> BK\_BT\_EIR\_TYPE\_MANU\_SPECIFIC
:   Manufacturer specific data

<a id="c.BK_BT_EIR_TYPE_MAX_NUM"></a>

<a id="bk__dm__gap__bt__types_8h_1a5aac59dde3adc568fd7e9b3baa1605d2"></a> BK\_BT\_EIR\_TYPE\_MAX\_NUM
:   MAX number of EIR type

<a id="c.BK_BT_EIR_FLAG_LIMIT_DISC"></a>

<a id="bk__dm__gap__bt__types_8h_1a58830d0875a47e22e93039ade0fa70ef"></a> BK\_BT\_EIR\_FLAG\_LIMIT\_DISC

<a id="c.BK_BT_EIR_FLAG_GEN_DISC"></a>

<a id="bk__dm__gap__bt__types_8h_1a4d053cbed1f752faffcb0251b7f6f509"></a> BK\_BT\_EIR\_FLAG\_GEN\_DISC

<a id="c.BK_BT_EIR_FLAG_BREDR_NOT_SPT"></a>

<a id="bk__dm__gap__bt__types_8h_1a8499c1a1bedeb07977367f70aa00825b"></a> BK\_BT\_EIR\_FLAG\_BREDR\_NOT\_SPT

<a id="c.BK_BT_EIR_FLAG_DMT_CONTROLLER_SPT"></a>

<a id="bk__dm__gap__bt__types_8h_1abc490709b047914203d2815dc9e024b1"></a> BK\_BT\_EIR\_FLAG\_DMT\_CONTROLLER\_SPT

<a id="c.BK_BT_EIR_FLAG_DMT_HOST_SPT"></a>

<a id="bk__dm__gap__bt__types_8h_1a58d5eaf07be59fbafb68eb4de7673f0d"></a> BK\_BT\_EIR\_FLAG\_DMT\_HOST\_SPT

<a id="c.BK_BT_EIR_MAX_LEN"></a>

<a id="bk__dm__gap__bt__types_8h_1a8dae07f68dc8e1b2d39f3fa06fc16342"></a> BK\_BT\_EIR\_MAX\_LEN

<a id="c.BK_BT_PIN_CODE_LEN"></a>

<a id="bk__dm__gap__bt__types_8h_1a317f3471b5dedd7a52b3a048707ac929"></a> BK\_BT\_PIN\_CODE\_LEN
:   Max pin code length

<a id="c.BK_BT_IO_CAP_OUT"></a>

<a id="bk__dm__gap__bt__types_8h_1a61bb44b66d2f8a2aee603253c6bd1cb6"></a> BK\_BT\_IO\_CAP\_OUT
:   IO Capability Constants DisplayOnly

<a id="c.BK_BT_IO_CAP_IO"></a>

<a id="bk__dm__gap__bt__types_8h_1ada9721135a24a8ff82cd82b35f131871"></a> BK\_BT\_IO\_CAP\_IO
:   DisplayYesNo

<a id="c.BK_BT_IO_CAP_IN"></a>

<a id="bk__dm__gap__bt__types_8h_1aff19a0d32df16488e8c029961707364d"></a> BK\_BT\_IO\_CAP\_IN
:   KeyboardOnly

<a id="c.BK_BT_IO_CAP_NONE"></a>

<a id="bk__dm__gap__bt__types_8h_1a3b1fc72658705279a3456c9ff94203c6"></a> BK\_BT\_IO\_CAP\_NONE
:   NoInputNoOutput

<a id="c.BK_BT_AUTH_REQ_NO_BONDING"></a>

<a id="bk__dm__gap__bt__types_8h_1a7892d4328432b000eda3c60ef09b9433"></a> BK\_BT\_AUTH\_REQ\_NO\_BONDING
:   SSP Authentication Requirements No MITM protection, no bonding

<a id="c.BK_BT_AUTH_REQ_NO_BONDING_MITM"></a>

<a id="bk__dm__gap__bt__types_8h_1a43bf79b7a8347ef918ed1ed32979851f"></a> BK\_BT\_AUTH\_REQ\_NO\_BONDING\_MITM
:   MITM protection, no bonding

<a id="c.BK_BT_AUTH_REQ_DEDICATED_BONDING"></a>

<a id="bk__dm__gap__bt__types_8h_1aeecad86b4990e3dde02f536fab79404a"></a> BK\_BT\_AUTH\_REQ\_DEDICATED\_BONDING
:   No MITM protection, dedicated bonding

<a id="c.BK_BT_AUTH_REQ_DEDICATED_BONDING_MITM"></a>

<a id="bk__dm__gap__bt__types_8h_1a74a2ac05ffec975b54d37470e71a8d4c"></a> BK\_BT\_AUTH\_REQ\_DEDICATED\_BONDING\_MITM
:   MITM protection, dedicated bonding

<a id="c.BK_BT_AUTH_REQ_GENERAL_BONDING"></a>

<a id="bk__dm__gap__bt__types_8h_1a300d195b0abe03e99a6af0a1d285a140"></a> BK\_BT\_AUTH\_REQ\_GENERAL\_BONDING
:   No MITM protection, general bonding

<a id="c.BK_BT_AUTH_REQ_GENERAL_BONDING_MITM"></a>

<a id="bk__dm__gap__bt__types_8h_1a16b9a11a24b098cc31560aa11a48d5f0"></a> BK\_BT\_AUTH\_REQ\_GENERAL\_BONDING\_MITM
:   MITM protection, general bonding

<a id="c.BK_BT_PM_MD_ACTIVE"></a>

<a id="bk__dm__gap__bt__types_8h_1a35d53deca278c47c70f85cc7f60b78a9"></a> BK\_BT\_PM\_MD\_ACTIVE
:   Active mode

<a id="c.BK_BT_PM_MD_HOLD"></a>

<a id="bk__dm__gap__bt__types_8h_1a0ad6b2503234f7d6ccb8ace5f016c19b"></a> BK\_BT\_PM\_MD\_HOLD
:   Hold mode

<a id="c.BK_BT_PM_MD_SNIFF"></a>

<a id="bk__dm__gap__bt__types_8h_1a6ea60b4c554535a2dcce544b7f87614a"></a> BK\_BT\_PM\_MD\_SNIFF
:   Sniff mode

<a id="c.BK_BT_PM_MD_PARK"></a>

<a id="bk__dm__gap__bt__types_8h_1a3eea1c0351e6aad26db87fe789607d64"></a> BK\_BT\_PM\_MD\_PARK
:   Park state

<a id="c.BK_BT_COD_SRVC_BIT_MASK"></a>

<a id="bk__dm__gap__bt__types_8h_1a2f67e14b276939c8a5d57ca7b7f2ec85"></a> BK\_BT\_COD\_SRVC\_BIT\_MASK
:   Bits of major service class field.

    Major service bit mask

<a id="c.BK_BT_COD_SRVC_BIT_OFFSET"></a>

<a id="bk__dm__gap__bt__types_8h_1a6721485f08c9e84978b0b0fbc3255eab"></a> BK\_BT\_COD\_SRVC\_BIT\_OFFSET
:   Major service bit offset

<a id="c.BK_BT_COD_MAJOR_DEV_BIT_MASK"></a>

<a id="bk__dm__gap__bt__types_8h_1a0ee959538b261fdb158fddffe2fbce6f"></a> BK\_BT\_COD\_MAJOR\_DEV\_BIT\_MASK
:   Bits of major device class field.

    Major device bit mask

<a id="c.BK_BT_COD_MAJOR_DEV_BIT_OFFSET"></a>

<a id="bk__dm__gap__bt__types_8h_1af980ba10fc43bb642c94c7dc50761d73"></a> BK\_BT\_COD\_MAJOR\_DEV\_BIT\_OFFSET
:   Major device bit offset

<a id="c.BK_BT_COD_MINOR_DEV_BIT_MASK"></a>

<a id="bk__dm__gap__bt__types_8h_1a2e9e3b41f5732fbbb0f83c4e008b90a8"></a> BK\_BT\_COD\_MINOR\_DEV\_BIT\_MASK
:   Bits of minor device class field.

    Minor device bit mask

<a id="c.BK_BT_COD_MINOR_DEV_BIT_OFFSET"></a>

<a id="bk__dm__gap__bt__types_8h_1abeefb50863f878ce0c2e8ff78389e010"></a> BK\_BT\_COD\_MINOR\_DEV\_BIT\_OFFSET
:   Minor device bit offset

<a id="c.BK_BT_COD_FORMAT_TYPE_BIT_MASK"></a>

<a id="bk__dm__gap__bt__types_8h_1aa67fb1557ec6b7d17a19f1006c85f201"></a> BK\_BT\_COD\_FORMAT\_TYPE\_BIT\_MASK
:   Bits of format type.

    Format type bit mask

<a id="c.BK_BT_COD_FORMAT_TYPE_BIT_OFFSET"></a>

<a id="bk__dm__gap__bt__types_8h_1af3e09d70ed9c9e8f0949842588b208ff"></a> BK\_BT\_COD\_FORMAT\_TYPE\_BIT\_OFFSET
:   Format type bit offset

<a id="c.BK_BT_COD_FORMAT_TYPE_1"></a>

<a id="bk__dm__gap__bt__types_8h_1a0ef9a3e873ea592bc43dce730f57bc11"></a> BK\_BT\_COD\_FORMAT\_TYPE\_1
:   Class of device format type 1\.

<a id="c.BK_BT_GAP_MIN_INQ_LEN"></a>

<a id="bk__dm__gap__bt__types_8h_1abb37f4e56936d0e64e8b5c1e2ef2d2fd"></a> BK\_BT\_GAP\_MIN\_INQ\_LEN
:   Minimum and Maximum inquiry length Minimum inquiry duration, unit is 1.28s

<a id="c.BK_BT_GAP_MAX_INQ_LEN"></a>

<a id="bk__dm__gap__bt__types_8h_1abb909c637ea4664a54cf08e01ff41bc5"></a> BK\_BT\_GAP\_MAX\_INQ\_LEN
:   Maximum inquiry duration, unit is 1.28s

<a id="c.BT_MASTER_ROLE"></a>

<a id="bk__dm__gap__bt__types_8h_1a910d72fe1dca6f9fdaacf8c5cda6bb69"></a> BT\_MASTER\_ROLE
:   bluetooth role defenitions

<a id="c.BT_SLAVE_ROLE"></a>

<a id="bk__dm__gap__bt__types_8h_1a9dac5bcb8fd989c7e5b8f3ea558a7980"></a> BT\_SLAVE\_ROLE

<a id="id50"></a>

### Type Definitions

<a id="_CPPv422bk_bt_gap_afh_channels"></a>

<a id="_CPPv322bk_bt_gap_afh_channels"></a> <a id="_CPPv222bk_bt_gap_afh_channels"></a> <a id="bk_bt_gap_afh_channels"></a> <a id="bk__dm__gap__bt__types_8h_1a53e5e46e088c5199a4c038d9ab1233d7"></a> typedef uint8\_t bk\_bt\_gap\_afh\_channels\[BK\_BT\_GAP\_AFH\_CHANNELS\_LEN\]

<a id="_CPPv416bk_bt_eir_type_t"></a>

<a id="_CPPv316bk_bt_eir_type_t"></a> <a id="_CPPv216bk_bt_eir_type_t"></a> <a id="bk_bt_eir_type_t"></a> <a id="bk__dm__gap__bt__types_8h_1a37fad4413f28436dc1c22a3e8e17208e"></a> typedef uint8\_t bk\_bt\_eir\_type\_t

<a id="_CPPv416bk_bt_pin_code_t"></a>

<a id="_CPPv316bk_bt_pin_code_t"></a> <a id="_CPPv216bk_bt_pin_code_t"></a> <a id="bk_bt_pin_code_t"></a> <a id="bk__dm__gap__bt__types_8h_1a80c878873178a07c1f65dc56a0d9956d"></a> typedef uint8\_t bk\_bt\_pin\_code\_t\[BK\_BT\_PIN\_CODE\_LEN\]
:   Pin Code (upto 128 bits) MSB is 0

<a id="_CPPv414bk_bt_io_cap_t"></a>

<a id="_CPPv314bk_bt_io_cap_t"></a> <a id="_CPPv214bk_bt_io_cap_t"></a> <a id="bk_bt_io_cap_t"></a> <a id="bk__dm__gap__bt__types_8h_1accafdba5facde4c827eaebd46f59ef58"></a> typedef uint8\_t bk\_bt\_io\_cap\_t
:   Combination of the IO Capability

<a id="_CPPv415bk_bt_pm_mode_t"></a>

<a id="_CPPv315bk_bt_pm_mode_t"></a> <a id="_CPPv215bk_bt_pm_mode_t"></a> <a id="bk_bt_pm_mode_t"></a> <a id="bk__dm__gap__bt__types_8h_1a3a15a50b2bcb028dfe1b77f8f62304b0"></a> typedef uint8\_t bk\_bt\_pm\_mode\_t

<a id="_CPPv414bk_bt_gap_cb_t"></a>

<a id="_CPPv314bk_bt_gap_cb_t"></a> <a id="_CPPv214bk_bt_gap_cb_t"></a> <a id="bk_bt_gap_cb_t"></a> <a id="bk__dm__gap__bt__types_8h_1a4048aa8aa56dfeebc10cfa3c8dc5c590"></a> typedef void (\*bk\_bt\_gap\_cb\_t)([bk\_gap\_bt\_cb\_event\_t](#_CPPv420bk_gap_bt_cb_event_t "bk_gap_bt_cb_event_t") event, [bk\_bt\_gap\_cb\_param\_t](#_CPPv420bk_bt_gap_cb_param_t "bk_bt_gap_cb_param_t") \*param)
:   bluetooth GAP callback function type

    Param event
    :   : Event type

    Param param
    :   : Pointer to callback parameter

<a id="id51"></a>

### Enumerations

<a id="_CPPv416bk_bt_cod_mode_t"></a>

<a id="_CPPv316bk_bt_cod_mode_t"></a> <a id="_CPPv216bk_bt_cod_mode_t"></a> <a id="bk__dm__gap__bt__types_8h_1ab00803a41926133285d083c823f144a5"></a> enum bk\_bt\_cod\_mode\_t
:   class of device settings

    *Values:*

    <a id="_CPPv4N16bk_bt_cod_mode_t25BK_BT_SET_COD_MAJOR_MINORE"></a>

    <a id="_CPPv3N16bk_bt_cod_mode_t25BK_BT_SET_COD_MAJOR_MINORE"></a> <a id="_CPPv2N16bk_bt_cod_mode_t25BK_BT_SET_COD_MAJOR_MINORE"></a> <a id="bk__dm__gap__bt__types_8h_1ab00803a41926133285d083c823f144a5a4f14087205e35b39b5cfd2b946c33130"></a> enumerator BK\_BT\_SET\_COD\_MAJOR\_MINOR
    :   overwrite major, minor class

    <a id="_CPPv4N16bk_bt_cod_mode_t27BK_BT_SET_COD_SERVICE_CLASSE"></a>

    <a id="_CPPv3N16bk_bt_cod_mode_t27BK_BT_SET_COD_SERVICE_CLASSE"></a> <a id="_CPPv2N16bk_bt_cod_mode_t27BK_BT_SET_COD_SERVICE_CLASSE"></a> <a id="bk__dm__gap__bt__types_8h_1ab00803a41926133285d083c823f144a5a7dc0a491d320bdd1b63de01e774db3d9"></a> enumerator BK\_BT\_SET\_COD\_SERVICE\_CLASS
    :   set the bits in the input, the current bit will remain

    <a id="_CPPv4N16bk_bt_cod_mode_t27BK_BT_CLR_COD_SERVICE_CLASSE"></a>

    <a id="_CPPv3N16bk_bt_cod_mode_t27BK_BT_CLR_COD_SERVICE_CLASSE"></a> <a id="_CPPv2N16bk_bt_cod_mode_t27BK_BT_CLR_COD_SERVICE_CLASSE"></a> <a id="bk__dm__gap__bt__types_8h_1ab00803a41926133285d083c823f144a5a7ca4d17023112a00ecca0748c7b2f3b4"></a> enumerator BK\_BT\_CLR\_COD\_SERVICE\_CLASS
    :   clear the bits in the input, others will remain

    <a id="_CPPv4N16bk_bt_cod_mode_t17BK_BT_SET_COD_ALLE"></a>

    <a id="_CPPv3N16bk_bt_cod_mode_t17BK_BT_SET_COD_ALLE"></a> <a id="_CPPv2N16bk_bt_cod_mode_t17BK_BT_SET_COD_ALLE"></a> <a id="bk__dm__gap__bt__types_8h_1ab00803a41926133285d083c823f144a5a2b2079310d43bd76166a3790929809af"></a> enumerator BK\_BT\_SET\_COD\_ALL
    :   overwrite major, minor, set the bits in service class

    <a id="_CPPv4N16bk_bt_cod_mode_t14BK_BT_INIT_CODE"></a>

    <a id="_CPPv3N16bk_bt_cod_mode_t14BK_BT_INIT_CODE"></a> <a id="_CPPv2N16bk_bt_cod_mode_t14BK_BT_INIT_CODE"></a> <a id="bk__dm__gap__bt__types_8h_1ab00803a41926133285d083c823f144a5a3bd7f73643daf5a5914796368af6dab5"></a> enumerator BK\_BT\_INIT\_COD
    :   overwrite major, minor, and service class

<a id="_CPPv425bk_bt_gap_dev_prop_type_t"></a>

<a id="_CPPv325bk_bt_gap_dev_prop_type_t"></a> <a id="_CPPv225bk_bt_gap_dev_prop_type_t"></a> <a id="bk__dm__gap__bt__types_8h_1aa1f2be74afec624071fbb72432cd84ef"></a> enum bk\_bt\_gap\_dev\_prop\_type\_t
:   Bluetooth Device Property type.

    *Values:*

    <a id="_CPPv4N25bk_bt_gap_dev_prop_type_t25BK_BT_GAP_DEV_PROP_BDNAMEE"></a>

    <a id="_CPPv3N25bk_bt_gap_dev_prop_type_t25BK_BT_GAP_DEV_PROP_BDNAMEE"></a> <a id="_CPPv2N25bk_bt_gap_dev_prop_type_t25BK_BT_GAP_DEV_PROP_BDNAMEE"></a> <a id="bk__dm__gap__bt__types_8h_1aa1f2be74afec624071fbb72432cd84efa54380bccd6bf635f57babcbeab79393f"></a> enumerator BK\_BT\_GAP\_DEV\_PROP\_BDNAME
    :   Bluetooth device name, value type is int8\_t \[\]

    <a id="_CPPv4N25bk_bt_gap_dev_prop_type_t22BK_BT_GAP_DEV_PROP_CODE"></a>

    <a id="_CPPv3N25bk_bt_gap_dev_prop_type_t22BK_BT_GAP_DEV_PROP_CODE"></a> <a id="_CPPv2N25bk_bt_gap_dev_prop_type_t22BK_BT_GAP_DEV_PROP_CODE"></a> <a id="bk__dm__gap__bt__types_8h_1aa1f2be74afec624071fbb72432cd84efa237d38b182c93027245632e27949054e"></a> enumerator BK\_BT\_GAP\_DEV\_PROP\_COD
    :   Class of Device, value type is uint32\_t

    <a id="_CPPv4N25bk_bt_gap_dev_prop_type_t23BK_BT_GAP_DEV_PROP_RSSIE"></a>

    <a id="_CPPv3N25bk_bt_gap_dev_prop_type_t23BK_BT_GAP_DEV_PROP_RSSIE"></a> <a id="_CPPv2N25bk_bt_gap_dev_prop_type_t23BK_BT_GAP_DEV_PROP_RSSIE"></a> <a id="bk__dm__gap__bt__types_8h_1aa1f2be74afec624071fbb72432cd84efac624e42fd0288b4fe4f00d3923ebd2f5"></a> enumerator BK\_BT\_GAP\_DEV\_PROP\_RSSI
    :   Received Signal strength Indication, value type is int8\_t, ranging from -128 to 127

    <a id="_CPPv4N25bk_bt_gap_dev_prop_type_t22BK_BT_GAP_DEV_PROP_EIRE"></a>

    <a id="_CPPv3N25bk_bt_gap_dev_prop_type_t22BK_BT_GAP_DEV_PROP_EIRE"></a> <a id="_CPPv2N25bk_bt_gap_dev_prop_type_t22BK_BT_GAP_DEV_PROP_EIRE"></a> <a id="bk__dm__gap__bt__types_8h_1aa1f2be74afec624071fbb72432cd84efaf8606e7599357787ed8134caf745caf2"></a> enumerator BK\_BT\_GAP\_DEV\_PROP\_EIR
    :   Extended Inquiry Response, value type is uint8\_t \[\]

<a id="_CPPv416bk_bt_cod_srvc_t"></a>

<a id="_CPPv316bk_bt_cod_srvc_t"></a> <a id="_CPPv216bk_bt_cod_srvc_t"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bc"></a> enum bk\_bt\_cod\_srvc\_t
:   Major service class field of Class of Device, mutiple bits can be set.

    *Values:*

    <a id="_CPPv4N16bk_bt_cod_srvc_t19BK_BT_COD_SRVC_NONEE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t19BK_BT_COD_SRVC_NONEE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t19BK_BT_COD_SRVC_NONEE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bca6f24afd0872c305f214b606d1da95b6b"></a> enumerator BK\_BT\_COD\_SRVC\_NONE
    :   None indicates an invalid value

    <a id="_CPPv4N16bk_bt_cod_srvc_t28BK_BT_COD_SRVC_LMTD_DISCOVERE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t28BK_BT_COD_SRVC_LMTD_DISCOVERE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t28BK_BT_COD_SRVC_LMTD_DISCOVERE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bcaa8ee200e4f3f2d4c7b093f60931f316f"></a> enumerator BK\_BT\_COD\_SRVC\_LMTD\_DISCOVER
    :   Limited Discoverable Mode

    <a id="_CPPv4N16bk_bt_cod_srvc_t26BK_BT_COD_SRVC_POSITIONINGE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t26BK_BT_COD_SRVC_POSITIONINGE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t26BK_BT_COD_SRVC_POSITIONINGE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bca41cd4fad38f31a9196118f1c4db0f37b"></a> enumerator BK\_BT\_COD\_SRVC\_POSITIONING
    :   Positioning (Location identification)

    <a id="_CPPv4N16bk_bt_cod_srvc_t25BK_BT_COD_SRVC_NETWORKINGE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t25BK_BT_COD_SRVC_NETWORKINGE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t25BK_BT_COD_SRVC_NETWORKINGE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bcaa4d1e2b0a6b6c7763f1704a7fc5eab2c"></a> enumerator BK\_BT\_COD\_SRVC\_NETWORKING
    :   Networking, e.g. LAN, Ad hoc

    <a id="_CPPv4N16bk_bt_cod_srvc_t24BK_BT_COD_SRVC_RENDERINGE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t24BK_BT_COD_SRVC_RENDERINGE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t24BK_BT_COD_SRVC_RENDERINGE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bcab1a15f36a8b0a9b21872f55b8a282b6c"></a> enumerator BK\_BT\_COD\_SRVC\_RENDERING
    :   Rendering, e.g. Printing, Speakers

    <a id="_CPPv4N16bk_bt_cod_srvc_t24BK_BT_COD_SRVC_CAPTURINGE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t24BK_BT_COD_SRVC_CAPTURINGE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t24BK_BT_COD_SRVC_CAPTURINGE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bcabe70d64410a052c542373ef0dbe2d91c"></a> enumerator BK\_BT\_COD\_SRVC\_CAPTURING
    :   Capturing, e.g. Scanner, Microphone

    <a id="_CPPv4N16bk_bt_cod_srvc_t27BK_BT_COD_SRVC_OBJ_TRANSFERE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t27BK_BT_COD_SRVC_OBJ_TRANSFERE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t27BK_BT_COD_SRVC_OBJ_TRANSFERE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bcab837a9bfaf5580a1f7b8bff9f95b51bd"></a> enumerator BK\_BT\_COD\_SRVC\_OBJ\_TRANSFER
    :   Object Transfer, e.g. v-Inbox, v-Folder

    <a id="_CPPv4N16bk_bt_cod_srvc_t20BK_BT_COD_SRVC_AUDIOE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t20BK_BT_COD_SRVC_AUDIOE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t20BK_BT_COD_SRVC_AUDIOE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bca6932a5d25036766b6b653e0d03d1a16d"></a> enumerator BK\_BT\_COD\_SRVC\_AUDIO
    :   Audio, e.g. Speaker, Microphone, Headset service

    <a id="_CPPv4N16bk_bt_cod_srvc_t24BK_BT_COD_SRVC_TELEPHONYE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t24BK_BT_COD_SRVC_TELEPHONYE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t24BK_BT_COD_SRVC_TELEPHONYE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bca0b5087d4566834e2979c9ee6765d4c98"></a> enumerator BK\_BT\_COD\_SRVC\_TELEPHONY
    :   Telephony, e.g. Cordless telephony, Modem, Headset service

    <a id="_CPPv4N16bk_bt_cod_srvc_t26BK_BT_COD_SRVC_INFORMATIONE"></a>

    <a id="_CPPv3N16bk_bt_cod_srvc_t26BK_BT_COD_SRVC_INFORMATIONE"></a> <a id="_CPPv2N16bk_bt_cod_srvc_t26BK_BT_COD_SRVC_INFORMATIONE"></a> <a id="bk__dm__gap__bt__types_8h_1a755aaf5f11faec24ac9fd1cbd81be5bcaa602a49ba26eb0ded99c8e515389efe8"></a> enumerator BK\_BT\_COD\_SRVC\_INFORMATION
    :   Information, e.g., WEB-server, WAP-server

<a id="_CPPv416bk_bt_pin_type_t"></a>

<a id="_CPPv316bk_bt_pin_type_t"></a> <a id="_CPPv216bk_bt_pin_type_t"></a> <a id="bk__dm__gap__bt__types_8h_1a0ad64c0ce01c61e5626a3ec1175b4ae7"></a> enum bk\_bt\_pin\_type\_t
:   *Values:*

    <a id="_CPPv4N16bk_bt_pin_type_t23BK_BT_PIN_TYPE_VARIABLEE"></a>

    <a id="_CPPv3N16bk_bt_pin_type_t23BK_BT_PIN_TYPE_VARIABLEE"></a> <a id="_CPPv2N16bk_bt_pin_type_t23BK_BT_PIN_TYPE_VARIABLEE"></a> <a id="bk__dm__gap__bt__types_8h_1a0ad64c0ce01c61e5626a3ec1175b4ae7af312a9474f5b317a161b8b13ff4577eb"></a> enumerator BK\_BT\_PIN\_TYPE\_VARIABLE
    :   Refer to BTM\_PIN\_TYPE\_VARIABLE

    <a id="_CPPv4N16bk_bt_pin_type_t20BK_BT_PIN_TYPE_FIXEDE"></a>

    <a id="_CPPv3N16bk_bt_pin_type_t20BK_BT_PIN_TYPE_FIXEDE"></a> <a id="_CPPv2N16bk_bt_pin_type_t20BK_BT_PIN_TYPE_FIXEDE"></a> <a id="bk__dm__gap__bt__types_8h_1a0ad64c0ce01c61e5626a3ec1175b4ae7a9c5c66f77da666bf711c5ea0e7808732"></a> enumerator BK\_BT\_PIN\_TYPE\_FIXED
    :   Refer to BTM\_PIN\_TYPE\_FIXED

<a id="_CPPv416bk_bt_sp_param_t"></a>

<a id="_CPPv316bk_bt_sp_param_t"></a> <a id="_CPPv216bk_bt_sp_param_t"></a> <a id="bk__dm__gap__bt__types_8h_1aaec10e10beb60e1418a98146fd2847cd"></a> enum bk\_bt\_sp\_param\_t
:   *Values:*

    <a id="_CPPv4N16bk_bt_sp_param_t19BK_BT_SP_IOCAP_MODEE"></a>

    <a id="_CPPv3N16bk_bt_sp_param_t19BK_BT_SP_IOCAP_MODEE"></a> <a id="_CPPv2N16bk_bt_sp_param_t19BK_BT_SP_IOCAP_MODEE"></a> <a id="bk__dm__gap__bt__types_8h_1aaec10e10beb60e1418a98146fd2847cda942ac7554a064ae4c22a16ec2a228d07"></a> enumerator BK\_BT\_SP\_IOCAP\_MODE
    :   Set IO capability. value\[0\]: bk\_bt\_io\_cap\_t (0x00\~0x03)

    <a id="_CPPv4N16bk_bt_sp_param_t21BK_BT_SP_AUTHREQ_MODEE"></a>

    <a id="_CPPv3N16bk_bt_sp_param_t21BK_BT_SP_AUTHREQ_MODEE"></a> <a id="_CPPv2N16bk_bt_sp_param_t21BK_BT_SP_AUTHREQ_MODEE"></a> <a id="bk__dm__gap__bt__types_8h_1aaec10e10beb60e1418a98146fd2847cdabfde42c291cef1bfe998d581c9023fe8"></a> enumerator BK\_BT\_SP\_AUTHREQ\_MODE
    :   Set local SSP AuthReq. value\[0\]: authentication requirements (0x00\~0x05)

    <a id="_CPPv4N16bk_bt_sp_param_t17BK_BT_SP_OOB_DATAE"></a>

    <a id="_CPPv3N16bk_bt_sp_param_t17BK_BT_SP_OOB_DATAE"></a> <a id="_CPPv2N16bk_bt_sp_param_t17BK_BT_SP_OOB_DATAE"></a> <a id="bk__dm__gap__bt__types_8h_1aaec10e10beb60e1418a98146fd2847cda9d2504f9f5ca71cfaf157e2228f8febc"></a> enumerator BK\_BT\_SP\_OOB\_DATA
    :   Set remote OOB data. value: \[bd\_addr(6)\]\[ssp\_c(16)\]\[ssp\_r(16)\]

<a id="_CPPv421bk_bt_cod_major_dev_t"></a>

<a id="_CPPv321bk_bt_cod_major_dev_t"></a> <a id="_CPPv221bk_bt_cod_major_dev_t"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72f"></a> enum bk\_bt\_cod\_major\_dev\_t
:   Major device class field of Class of Device.

    *Values:*

    <a id="_CPPv4N21bk_bt_cod_major_dev_t24BK_BT_COD_MAJOR_DEV_MISCE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t24BK_BT_COD_MAJOR_DEV_MISCE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t24BK_BT_COD_MAJOR_DEV_MISCE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72fae3fbcca61b2caa438fc77af7da2d4ffe"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_MISC
    :   Miscellaneous

    <a id="_CPPv4N21bk_bt_cod_major_dev_t28BK_BT_COD_MAJOR_DEV_COMPUTERE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t28BK_BT_COD_MAJOR_DEV_COMPUTERE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t28BK_BT_COD_MAJOR_DEV_COMPUTERE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72fa1ca7711370dc9ae7bb2ec1c9390af019"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_COMPUTER
    :   Computer

    <a id="_CPPv4N21bk_bt_cod_major_dev_t25BK_BT_COD_MAJOR_DEV_PHONEE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t25BK_BT_COD_MAJOR_DEV_PHONEE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t25BK_BT_COD_MAJOR_DEV_PHONEE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72fa90d4f003757f165da96abb1c61c5c0bb"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_PHONE
    :   Phone(cellular, cordless, pay phone, modem

    <a id="_CPPv4N21bk_bt_cod_major_dev_t27BK_BT_COD_MAJOR_DEV_LAN_NAPE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t27BK_BT_COD_MAJOR_DEV_LAN_NAPE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t27BK_BT_COD_MAJOR_DEV_LAN_NAPE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72faeba2f01b8a45629ac4f12e70f1e5e148"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_LAN\_NAP
    :   LAN, Network Access Point

    <a id="_CPPv4N21bk_bt_cod_major_dev_t22BK_BT_COD_MAJOR_DEV_AVE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t22BK_BT_COD_MAJOR_DEV_AVE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t22BK_BT_COD_MAJOR_DEV_AVE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72fae4d4670c60be6dd4daafb222e8af7aa9"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_AV
    :   Audio/Video(headset, speaker, stereo, video display, VCR

    <a id="_CPPv4N21bk_bt_cod_major_dev_t30BK_BT_COD_MAJOR_DEV_PERIPHERALE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t30BK_BT_COD_MAJOR_DEV_PERIPHERALE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t30BK_BT_COD_MAJOR_DEV_PERIPHERALE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72fa0be0a13d30aecc6904382617810e0e6d"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_PERIPHERAL
    :   Peripheral(mouse, joystick, keyboard)

    <a id="_CPPv4N21bk_bt_cod_major_dev_t27BK_BT_COD_MAJOR_DEV_IMAGINGE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t27BK_BT_COD_MAJOR_DEV_IMAGINGE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t27BK_BT_COD_MAJOR_DEV_IMAGINGE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72fa252d0c7d395bc17fab788b2fb3be7c0f"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_IMAGING
    :   Imaging(printer, scanner, camera, display

    <a id="_CPPv4N21bk_bt_cod_major_dev_t28BK_BT_COD_MAJOR_DEV_WEARABLEE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t28BK_BT_COD_MAJOR_DEV_WEARABLEE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t28BK_BT_COD_MAJOR_DEV_WEARABLEE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72fad4df72f7be3676f6f7029976c66a2a75"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_WEARABLE
    :   Wearable

    <a id="_CPPv4N21bk_bt_cod_major_dev_t23BK_BT_COD_MAJOR_DEV_TOYE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t23BK_BT_COD_MAJOR_DEV_TOYE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t23BK_BT_COD_MAJOR_DEV_TOYE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72fa651f8afbe7f312f6bd0f4b061a8b60b3"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_TOY
    :   Toy

    <a id="_CPPv4N21bk_bt_cod_major_dev_t26BK_BT_COD_MAJOR_DEV_HEALTHE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t26BK_BT_COD_MAJOR_DEV_HEALTHE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t26BK_BT_COD_MAJOR_DEV_HEALTHE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72fa51c239b06c43566ae1b40d00fa3d8b58"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_HEALTH
    :   Health

    <a id="_CPPv4N21bk_bt_cod_major_dev_t33BK_BT_COD_MAJOR_DEV_UNCATEGORIZEDE"></a>

    <a id="_CPPv3N21bk_bt_cod_major_dev_t33BK_BT_COD_MAJOR_DEV_UNCATEGORIZEDE"></a> <a id="_CPPv2N21bk_bt_cod_major_dev_t33BK_BT_COD_MAJOR_DEV_UNCATEGORIZEDE"></a> <a id="bk__dm__gap__bt__types_8h_1aff9fc19e86115aee3f63cd1fd6e0d72facc9ed1c786898543e83620f242e04ee7"></a> enumerator BK\_BT\_COD\_MAJOR\_DEV\_UNCATEGORIZED
    :   Uncategorized: device not specified

<a id="_CPPv427bk_bt_gap_discovery_state_t"></a>

<a id="_CPPv327bk_bt_gap_discovery_state_t"></a> <a id="_CPPv227bk_bt_gap_discovery_state_t"></a> <a id="bk__dm__gap__bt__types_8h_1a82dc83758cd68660838658f23941afce"></a> enum bk\_bt\_gap\_discovery\_state\_t
:   Bluetooth Device Discovery state

    *Values:*

    <a id="_CPPv4N27bk_bt_gap_discovery_state_t27BK_BT_GAP_DISCOVERY_STOPPEDE"></a>

    <a id="_CPPv3N27bk_bt_gap_discovery_state_t27BK_BT_GAP_DISCOVERY_STOPPEDE"></a> <a id="_CPPv2N27bk_bt_gap_discovery_state_t27BK_BT_GAP_DISCOVERY_STOPPEDE"></a> <a id="bk__dm__gap__bt__types_8h_1a82dc83758cd68660838658f23941afcea724fb584c16f2ccecb97ce45c6f46067"></a> enumerator BK\_BT\_GAP\_DISCOVERY\_STOPPED
    :   Device discovery stopped

    <a id="_CPPv4N27bk_bt_gap_discovery_state_t27BK_BT_GAP_DISCOVERY_STARTEDE"></a>

    <a id="_CPPv3N27bk_bt_gap_discovery_state_t27BK_BT_GAP_DISCOVERY_STARTEDE"></a> <a id="_CPPv2N27bk_bt_gap_discovery_state_t27BK_BT_GAP_DISCOVERY_STARTEDE"></a> <a id="bk__dm__gap__bt__types_8h_1a82dc83758cd68660838658f23941afcea79522f6dfdba2ff8a8f061848582ed2b"></a> enumerator BK\_BT\_GAP\_DISCOVERY\_STARTED
    :   Device discovery started

<a id="_CPPv420bk_gap_bt_cb_event_t"></a>

<a id="_CPPv320bk_gap_bt_cb_event_t"></a> <a id="_CPPv220bk_gap_bt_cb_event_t"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29a"></a> enum bk\_gap\_bt\_cb\_event\_t
:   BT GAP callback events.

    *Values:*

    <a id="_CPPv4N20bk_gap_bt_cb_event_t22BK_BT_GAP_DISC_RES_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t22BK_BT_GAP_DISC_RES_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t22BK_BT_GAP_DISC_RES_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aabdea55cf95cf7476c4eeacf2d3c47018"></a> enumerator BK\_BT\_GAP\_DISC\_RES\_EVT
    :   Device discovery result event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t32BK_BT_GAP_DISC_STATE_CHANGED_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t32BK_BT_GAP_DISC_STATE_CHANGED_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t32BK_BT_GAP_DISC_STATE_CHANGED_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aaf78e244681a56fb0cc59ac16698e1ebc"></a> enumerator BK\_BT\_GAP\_DISC\_STATE\_CHANGED\_EVT
    :   Discovery state changed event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t23BK_BT_GAP_RMT_SRVCS_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t23BK_BT_GAP_RMT_SRVCS_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t23BK_BT_GAP_RMT_SRVCS_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aaa75b2d5957e9f24fa781f3ce10cda30c"></a> enumerator BK\_BT\_GAP\_RMT\_SRVCS\_EVT
    :   Get remote services event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t26BK_BT_GAP_RMT_SRVC_REC_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t26BK_BT_GAP_RMT_SRVC_REC_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t26BK_BT_GAP_RMT_SRVC_REC_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aac947b5fe91fd3540e45ca496c6d67462"></a> enumerator BK\_BT\_GAP\_RMT\_SRVC\_REC\_EVT
    :   Get remote service record event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t23BK_BT_GAP_AUTH_CMPL_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t23BK_BT_GAP_AUTH_CMPL_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t23BK_BT_GAP_AUTH_CMPL_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa24855bcb1af8d162bc8415d39950014c"></a> enumerator BK\_BT\_GAP\_AUTH\_CMPL\_EVT
    :   Authentication complete event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t21BK_BT_GAP_PIN_REQ_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t21BK_BT_GAP_PIN_REQ_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t21BK_BT_GAP_PIN_REQ_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa9ed59d7553e97ebc428e35af2b84eeb1"></a> enumerator BK\_BT\_GAP\_PIN\_REQ\_EVT
    :   Legacy Pairing Pin code request

    <a id="_CPPv4N20bk_gap_bt_cb_event_t21BK_BT_GAP_CFM_REQ_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t21BK_BT_GAP_CFM_REQ_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t21BK_BT_GAP_CFM_REQ_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa1d1cd0320e43f85ec575b6a39b2b49a5"></a> enumerator BK\_BT\_GAP\_CFM\_REQ\_EVT
    :   Security Simple Pairing User Confirmation request.

    <a id="_CPPv4N20bk_gap_bt_cb_event_t23BK_BT_GAP_KEY_NOTIF_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t23BK_BT_GAP_KEY_NOTIF_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t23BK_BT_GAP_KEY_NOTIF_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aab0675e30c841596eaddce5a596fb6a29"></a> enumerator BK\_BT\_GAP\_KEY\_NOTIF\_EVT
    :   Security Simple Pairing Passkey Notification

    <a id="_CPPv4N20bk_gap_bt_cb_event_t21BK_BT_GAP_KEY_REQ_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t21BK_BT_GAP_KEY_REQ_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t21BK_BT_GAP_KEY_REQ_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aaab2550ea99272fcecb774f55ba728e58"></a> enumerator BK\_BT\_GAP\_KEY\_REQ\_EVT
    :   Security Simple Pairing Passkey request

    <a id="_CPPv4N20bk_gap_bt_cb_event_t29BK_BT_GAP_READ_RSSI_DELTA_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t29BK_BT_GAP_READ_RSSI_DELTA_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t29BK_BT_GAP_READ_RSSI_DELTA_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa6610531841f629ac050b29d0ec0e9ea8"></a> enumerator BK\_BT\_GAP\_READ\_RSSI\_DELTA\_EVT
    :   Read rssi event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t29BK_BT_GAP_CONFIG_EIR_DATA_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t29BK_BT_GAP_CONFIG_EIR_DATA_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t29BK_BT_GAP_CONFIG_EIR_DATA_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aad8a0c356896d88c313d1d25d9f08b785"></a> enumerator BK\_BT\_GAP\_CONFIG\_EIR\_DATA\_EVT
    :   Config EIR data event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t30BK_BT_GAP_SET_AFH_CHANNELS_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t30BK_BT_GAP_SET_AFH_CHANNELS_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t30BK_BT_GAP_SET_AFH_CHANNELS_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa51be30fe5ea782abef90568b8505f54b"></a> enumerator BK\_BT\_GAP\_SET\_AFH\_CHANNELS\_EVT
    :   Set AFH channels event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t30BK_BT_GAP_READ_REMOTE_NAME_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t30BK_BT_GAP_READ_REMOTE_NAME_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t30BK_BT_GAP_READ_REMOTE_NAME_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa380f44d1d54addf1c7d97c0ba3d3f564"></a> enumerator BK\_BT\_GAP\_READ\_REMOTE\_NAME\_EVT
    :   Read Remote Name event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t22BK_BT_GAP_MODE_CHG_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t22BK_BT_GAP_MODE_CHG_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t22BK_BT_GAP_MODE_CHG_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa5dd8d396a05422ff8f4031c7f943269c"></a> enumerator BK\_BT\_GAP\_MODE\_CHG\_EVT

    <a id="_CPPv4N20bk_gap_bt_cb_event_t38BK_BT_GAP_REMOVE_BOND_DEV_COMPLETE_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t38BK_BT_GAP_REMOVE_BOND_DEV_COMPLETE_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t38BK_BT_GAP_REMOVE_BOND_DEV_COMPLETE_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa179dfcd2388a2028d9ae47707737f86c"></a> enumerator BK\_BT\_GAP\_REMOVE\_BOND\_DEV\_COMPLETE\_EVT
    :   remove bond device complete event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t22BK_BT_GAP_QOS_CMPL_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t22BK_BT_GAP_QOS_CMPL_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t22BK_BT_GAP_QOS_CMPL_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aaaeda1abc8078f27df4b5994d240d39dc"></a> enumerator BK\_BT\_GAP\_QOS\_CMPL\_EVT
    :   QOS complete event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t32BK_BT_GAP_ACL_CONN_CMPL_STAT_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t32BK_BT_GAP_ACL_CONN_CMPL_STAT_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t32BK_BT_GAP_ACL_CONN_CMPL_STAT_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa3fe71ebfdd62aaf01349ee105a09649a"></a> enumerator BK\_BT\_GAP\_ACL\_CONN\_CMPL\_STAT\_EVT
    :   ACL connection complete status event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t35BK_BT_GAP_ACL_DISCONN_CMPL_STAT_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t35BK_BT_GAP_ACL_DISCONN_CMPL_STAT_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t35BK_BT_GAP_ACL_DISCONN_CMPL_STAT_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa1caa666a01545913513f2747f4908af3"></a> enumerator BK\_BT\_GAP\_ACL\_DISCONN\_CMPL\_STAT\_EVT
    :   ACL disconnection complete status event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t28BK_BT_GAP_LINK_KEY_NOTIF_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t28BK_BT_GAP_LINK_KEY_NOTIF_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t28BK_BT_GAP_LINK_KEY_NOTIF_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa6bd9dbd17f4dc507d8de9134b12ef474"></a> enumerator BK\_BT\_GAP\_LINK\_KEY\_NOTIF\_EVT
    :   Link Key Notification

    <a id="_CPPv4N20bk_gap_bt_cb_event_t26BK_BT_GAP_LINK_KEY_REQ_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t26BK_BT_GAP_LINK_KEY_REQ_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t26BK_BT_GAP_LINK_KEY_REQ_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa66ce7a1c1148f3d70363c898563b5c86"></a> enumerator BK\_BT\_GAP\_LINK\_KEY\_REQ\_EVT
    :   Link Key request

    <a id="_CPPv4N20bk_gap_bt_cb_event_t33BK_BT_GAP_SET_AUTO_SNIFF_CMPL_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t33BK_BT_GAP_SET_AUTO_SNIFF_CMPL_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t33BK_BT_GAP_SET_AUTO_SNIFF_CMPL_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa4b10175a7a32c63c74c7f6ce5038064c"></a> enumerator BK\_BT\_GAP\_SET\_AUTO\_SNIFF\_CMPL\_EVT

    <a id="_CPPv4N20bk_gap_bt_cb_event_t22BK_BT_GAP_ROLE_CHG_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t22BK_BT_GAP_ROLE_CHG_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t22BK_BT_GAP_ROLE_CHG_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa4fa2fe00ac7b1ca4f3a35a3f08fdd122"></a> enumerator BK\_BT\_GAP\_ROLE\_CHG\_EVT
    :   set auto entry sniff req completed event

        role change event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t28BK_BT_GAP_CONNECTION_REQ_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t28BK_BT_GAP_CONNECTION_REQ_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t28BK_BT_GAP_CONNECTION_REQ_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa7a5b82a0adcb40eb4957a4668e83fdd8"></a> enumerator BK\_BT\_GAP\_CONNECTION\_REQ\_EVT

    <a id="_CPPv4N20bk_gap_bt_cb_event_t31BK_BT_GAP_ENCRYPTION_CHANGE_EVTE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t31BK_BT_GAP_ENCRYPTION_CHANGE_EVTE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t31BK_BT_GAP_ENCRYPTION_CHANGE_EVTE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aad4e1c03bc982ba537469d35c56fd4241"></a> enumerator BK\_BT\_GAP\_ENCRYPTION\_CHANGE\_EVT
    :   BR/EDR encryption change event

    <a id="_CPPv4N20bk_gap_bt_cb_event_t17BK_BT_GAP_EVT_MAXE"></a>

    <a id="_CPPv3N20bk_gap_bt_cb_event_t17BK_BT_GAP_EVT_MAXE"></a> <a id="_CPPv2N20bk_gap_bt_cb_event_t17BK_BT_GAP_EVT_MAXE"></a> <a id="bk__dm__gap__bt__types_8h_1a4b2a3ddc10c1d26ac74f8c4016a9d29aa04802aa37381b7cee2236380a3243cb2"></a> enumerator BK\_BT\_GAP\_EVT\_MAX

<a id="_CPPv416bk_bt_inq_mode_t"></a>

<a id="_CPPv316bk_bt_inq_mode_t"></a> <a id="_CPPv216bk_bt_inq_mode_t"></a> <a id="bk__dm__gap__bt__types_8h_1a2e7658e3d81463f492ad78aa98c88a9c"></a> enum bk\_bt\_inq\_mode\_t
:   Inquiry Mode

    *Values:*

    <a id="_CPPv4N16bk_bt_inq_mode_t30BK_BT_INQ_MODE_GENERAL_INQUIRYE"></a>

    <a id="_CPPv3N16bk_bt_inq_mode_t30BK_BT_INQ_MODE_GENERAL_INQUIRYE"></a> <a id="_CPPv2N16bk_bt_inq_mode_t30BK_BT_INQ_MODE_GENERAL_INQUIRYE"></a> <a id="bk__dm__gap__bt__types_8h_1a2e7658e3d81463f492ad78aa98c88a9cad2e2f0eb73a57ae43836c867bd6e43aa"></a> enumerator BK\_BT\_INQ\_MODE\_GENERAL\_INQUIRY
    :   General inquiry mode

    <a id="_CPPv4N16bk_bt_inq_mode_t30BK_BT_INQ_MODE_LIMITED_INQUIRYE"></a>

    <a id="_CPPv3N16bk_bt_inq_mode_t30BK_BT_INQ_MODE_LIMITED_INQUIRYE"></a> <a id="_CPPv2N16bk_bt_inq_mode_t30BK_BT_INQ_MODE_LIMITED_INQUIRYE"></a> <a id="bk__dm__gap__bt__types_8h_1a2e7658e3d81463f492ad78aa98c88a9cac2f9b4eee75269a47930ab239d824dc0"></a> enumerator BK\_BT\_INQ\_MODE\_LIMITED\_INQUIRY
    :   Limited inquiry mode

<a id="_CPPv417bk_bt_conn_mode_t"></a>

<a id="_CPPv317bk_bt_conn_mode_t"></a> <a id="_CPPv217bk_bt_conn_mode_t"></a> <a id="bk__dm__gap__bt__types_8h_1a3fa3a6a98d6cf16673943c4f9f926e5a"></a> enum bk\_bt\_conn\_mode\_t
:   Discoverability and Connectability mode.

    *Values:*

    <a id="_CPPv4N17bk_bt_conn_mode_t21BK_BT_NON_CONNECTABLEE"></a>

    <a id="_CPPv3N17bk_bt_conn_mode_t21BK_BT_NON_CONNECTABLEE"></a> <a id="_CPPv2N17bk_bt_conn_mode_t21BK_BT_NON_CONNECTABLEE"></a> <a id="bk__dm__gap__bt__types_8h_1a3fa3a6a98d6cf16673943c4f9f926e5aadd0ef00016a0a0166e304055d8d4e4c5"></a> enumerator BK\_BT\_NON\_CONNECTABLE
    :   Non-connectable

    <a id="_CPPv4N17bk_bt_conn_mode_t17BK_BT_CONNECTABLEE"></a>

    <a id="_CPPv3N17bk_bt_conn_mode_t17BK_BT_CONNECTABLEE"></a> <a id="_CPPv2N17bk_bt_conn_mode_t17BK_BT_CONNECTABLEE"></a> <a id="bk__dm__gap__bt__types_8h_1a3fa3a6a98d6cf16673943c4f9f926e5aa31ec1ce972adfbf94bc4b1334dbccc8e"></a> enumerator BK\_BT\_CONNECTABLE
    :   Connectable

<a id="_CPPv417bk_bt_disc_mode_t"></a>

<a id="_CPPv317bk_bt_disc_mode_t"></a> <a id="_CPPv217bk_bt_disc_mode_t"></a> <a id="bk__dm__gap__bt__types_8h_1ac04c470895faddd677e699715a2b56d1"></a> enum bk\_bt\_disc\_mode\_t
:   *Values:*

    <a id="_CPPv4N17bk_bt_disc_mode_t22BK_BT_NON_DISCOVERABLEE"></a>

    <a id="_CPPv3N17bk_bt_disc_mode_t22BK_BT_NON_DISCOVERABLEE"></a> <a id="_CPPv2N17bk_bt_disc_mode_t22BK_BT_NON_DISCOVERABLEE"></a> <a id="bk__dm__gap__bt__types_8h_1ac04c470895faddd677e699715a2b56d1a977a2b191c5036b8fd034d84507bb991"></a> enumerator BK\_BT\_NON\_DISCOVERABLE
    :   Non-discoverable

    <a id="_CPPv4N17bk_bt_disc_mode_t18BK_BT_DISCOVERABLEE"></a>

    <a id="_CPPv3N17bk_bt_disc_mode_t18BK_BT_DISCOVERABLEE"></a> <a id="_CPPv2N17bk_bt_disc_mode_t18BK_BT_DISCOVERABLEE"></a> <a id="bk__dm__gap__bt__types_8h_1ac04c470895faddd677e699715a2b56d1ac7ad891c3fb9aaa3d528b77efce3d1ba"></a> enumerator BK\_BT\_DISCOVERABLE
    :   Discoverable

<a id="_CPPv412common_cod_t"></a>

<a id="_CPPv312common_cod_t"></a> <a id="_CPPv212common_cod_t"></a> <a id="bk__dm__gap__bt__types_8h_1ab4918e797f42831f18f1437a61bc99cf"></a> enum common\_cod\_t
:   *Values:*

    <a id="_CPPv4N12common_cod_t9COD_PHONEE"></a>

    <a id="_CPPv3N12common_cod_t9COD_PHONEE"></a> <a id="_CPPv2N12common_cod_t9COD_PHONEE"></a> <a id="bk__dm__gap__bt__types_8h_1ab4918e797f42831f18f1437a61bc99cfae78d990e53a650fccbd6a25af9c262b2"></a> enumerator COD\_PHONE

    <a id="_CPPv4N12common_cod_t12COD_SOUNDBARE"></a>

    <a id="_CPPv3N12common_cod_t12COD_SOUNDBARE"></a> <a id="_CPPv2N12common_cod_t12COD_SOUNDBARE"></a> <a id="bk__dm__gap__bt__types_8h_1ab4918e797f42831f18f1437a61bc99cfa35f5fdf7c8b5e9b521d2f2ea2fc4f0fd"></a> enumerator COD\_SOUNDBAR

    <a id="_CPPv4N12common_cod_t11COD_HEADSETE"></a>

    <a id="_CPPv3N12common_cod_t11COD_HEADSETE"></a> <a id="_CPPv2N12common_cod_t11COD_HEADSETE"></a> <a id="bk__dm__gap__bt__types_8h_1ab4918e797f42831f18f1437a61bc99cfa11312a7611013bbeee6f6eb49075eedc"></a> enumerator COD\_HEADSET

<a id="id52"></a>

## 参考链接

> [API 参考：](../bluetooth.md) 介绍蓝牙 API 接口。
>
> [蓝牙开发者指南：](../../developer-guide/bluetooth.md) 介绍蓝牙开发者指南。
