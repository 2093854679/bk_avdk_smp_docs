---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/bluetooth/single_ble.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ble-api"></a>

# BLE API

<a id="id1"></a>

## BLE API 分类

BLE API 主要包括以下类型：

按功能划分的 BLE API：
:   - BLE 公共接口
    - BLE 扫描接口
    - BLE 广播接口
    - BLE 连接接口

<a id="id2"></a>

## 兼容性和扩展性

BLE API 具备较好的扩展性和向后兼容性。多数 BLE 配置结构体中预留了字段，便于后续扩展。使用这些 API 时，应将预留字段初始化为 0，避免后续新增字段后影响兼容性。

<a id="id3"></a>

## 编程原则

重要

使用 BLE API 时建议遵循以下原则：
:   - 配置结构体中的预留字段应初始化为 0。
    - 使用 `BK_ERR_CHECK` 检查 BLE API 的返回值。
    - 不确定 API 用法时，优先参考 BLE 示例代码。
    - 不确定配置结构体字段如何初始化时，先使用默认配置宏，再按应用需求修改相关字段。
    - 不建议在 BLE 事件回调中执行耗时操作，可将事件转发到应用任务中处理。

<a id="id4"></a>

## 事件处理机制

Beken BLE driver 采用事件驱动方式工作。应用通过 BLE API 发起扫描、广播、连接、ATT 数据库访问等操作，并在 BLE 事件回调中获取状态变化和操作结果。

<a id="api"></a>

## API 参考

<a id="bk-ble-h"></a>

## bk\_ble.h

`bk_ble.h` 提供传统 BLE 的扫描、广播、连接和 ATT 数据库等接口。

<a id="header-file"></a>

### Header File

- [bk\_ble.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_ble.h)

<a id="functions"></a>

### Functions

<a id="_CPPv416bk_ble_create_dbP13bk_ble_db_cfg"></a>

<a id="_CPPv316bk_ble_create_dbP13bk_ble_db_cfg"></a> <a id="_CPPv216bk_ble_create_dbP13bk_ble_db_cfg"></a> <a id="bk_ble_create_db__bk_ble_db_cfgP"></a> <a id="group__bk__ble__api__v1_1ga48fc31375113253658e599d347a37878"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_create\_db(struct [bk\_ble\_db\_cfg](#_CPPv413bk_ble_db_cfg "bk_ble_db_cfg") \*ble\_db\_cfg)
:   Register a gatt service.

    User example: First we must build test\_service\_db test\_service\_db is a database for att, which used in ble discovery. reading writing and other operation is used on a att database.

    ```
    enum {
        TEST_IDX_SVC,
        TEST_IDX_CHAR_DECL,
        TEST_IDX_CHAR_VALUE,
        TEST_IDX_CHAR_DESC,

        TEST_IDX_CHAR_DATALEN_DECL,
        TEST_IDX_CHAR_DATALEN_VALUE,

        TEST_IDX_CHAR_INTER_DECL,
        TEST_IDX_CHAR_INTER_VALUE,

        TEST_IDX_NB,
    };

    //att records database.

    ble_attm_desc_t test_service_db[TEST_IDX_NB] = {
       //  Service Declaration
       [TEST_IDX_SVC]              = {DECL_PRIMARY_SERVICE_128, BK_BLE_PERM_SET(RD, ENABLE), 0, 0},
       // Characteristic declare
       [TEST_IDX_CHAR_DECL]    = {DECL_CHARACTERISTIC_128,  BK_BLE_PERM_SET(RD, ENABLE), 0, 0},
       // Characteristic Value
       [TEST_IDX_CHAR_VALUE]   = {{0x34, 0x12, 0},     BK_BLE_PERM_SET(NTF, ENABLE), BK_BLE_PERM_SET(RI, ENABLE) | BK_BLE_PERM_SET(UUID_LEN, UUID_16), 128},
       //Client Characteristic Configuration Descriptor
       [TEST_IDX_CHAR_DESC] = {DESC_CLIENT_CHAR_CFG_128, BK_BLE_PERM_SET(RD, ENABLE) | BK_BLE_PERM_SET(WRITE_REQ, ENABLE), 0, 0},
    };
    ```

    TEST\_IDX\_SVC is nessecery, is declare a primary att service. The macro define is:

    ```
    #define DECL_PRIMARY_SERVICE_128     {0x00,0x28,0}
    ```

    which is an UUID say it is a “primary service” [BK\_BLE\_PERM\_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) means it can be read, and must be read, so it can be discove by peer master.

    TEST\_IDX\_CHAR\_DECL declare a characteristic as a element in service, it must be [BK\_BLE\_PERM\_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b)

    ```
    #define DECL_CHARACTERISTIC_128      {0x03,0x28,0}
    ```

    show it’s a “characteristic”

    [BK\_BLE\_PERM\_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) means it can be read, and must be read, so it can be discove by peer master.

    TEST\_IDX\_CHAR\_VALUE is the real value of TEST\_IDX\_CHAR\_DECL, {0x34, 0x12, 0} means it’s type is 0x1234, you can determine by you self [BK\_BLE\_PERM\_SET(NTF, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) means it cant notify peer, such as value change. For exzample, BLE mouse report pos by “notify” peer. [BK\_BLE\_PERM\_SET(RI, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) means if peer read this att record, it will enable notification. [BK\_BLE\_PERM\_SET(UUID\_LEN, UUID\_16)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) means the first elem’s max len of TEST\_IDX\_CHAR\_VALUE.

    TEST\_IDX\_CHAR\_DESC is a Client Characteristic Configuration Descriptor for TEST\_IDX\_CHAR\_VALUE, it used by peer master as know as a client. As common usage, it config TEST\_IDX\_CHAR\_VALUE indication or notification. Peer can write this att handle to triggle it. Must be [BK\_BLE\_PERM\_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) \| [BK\_BLE\_PERM\_SET(WRITE\_REQ, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b)

    Now, you have a basic database for peer, in this case, peer write TEST\_IDX\_CHAR\_DESC or read TEST\_IDX\_CHAR\_VALUE to enable notification, and then we notify peer by TEST\_IDX\_CHAR\_VALUE

    Secondlly, we build ble\_db\_cfg

    ```
    struct bk_ble_db_cfg ble_db_cfg;

    ble_db_cfg.att_db = (ble_attm_desc_t *)test_service_db;
    ble_db_cfg.att_db_nb = TEST_IDX_NB;
    ble_db_cfg.prf_task_id = g_test_prf_task_id;
    ble_db_cfg.start_hdl = 0;
    ble_db_cfg.svc_perm = BK_BLE_PERM_SET(SVC_UUID_LEN, UUID_16);
    ```

    prf\_task\_id is app handle. If you have multi att service, used prf\_task\_id to distinguish it. svc\_perm show TEST\_IDX\_SVC UUID type’s len.

    参数
    :   **\-** – ble\_db\_cfg: service param

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv420bk_ble_set_notice_cb15ble_notice_cb_t"></a>

<a id="_CPPv320bk_ble_set_notice_cb15ble_notice_cb_t"></a> <a id="_CPPv220bk_ble_set_notice_cb15ble_notice_cb_t"></a> <a id="bk_ble_set_notice_cb__ble_notice_cb_t"></a> <a id="group__bk__ble__api__v1_1gaf161dd87d3a0fcc95e6cee58e4d18f0a"></a> void bk\_ble\_set\_notice\_cb([ble\_notice\_cb\_t](#_CPPv415ble_notice_cb_t "ble_notice_cb_t") func)
:   Register ble event notification callback.

    User example:

    ```
       void ble_at_notice_cb(ble_notice_t notice, void *param)
    {
        switch (notice) {

        case BLE_5_WRITE_EVENT: {

            if (w_req->prf_id == g_test_prf_task_id)
            {
                switch(w_req->att_idx)
                {
                case TEST_IDX_CHAR_DECL:
                    break;
                case TEST_IDX_CHAR_VALUE:
                    break;
                case TEST_IDX_CHAR_DESC:
                    //when peer enable notification, we create time and notify peer, such as
                    //write_buffer = (uint8_t *)os_malloc(s_test_data_len);
                    //bk_ble_send_noti_value(s_test_data_len, write_buffer, g_test_prf_task_id, TEST_IDX_CHAR_VALUE);
                    break;

                default:
                    break;
                }
            }
            break;
        }
        case BLE_5_CREATE_DB:
        //bk_ble_create_db success here
        break;
        }
    }

    bk_ble_set_notice_cb(ble_at_notice_cb);
    ```

    **Attention**
    :   1\. you must regist it, otherwise you cant get any event !

    **Attention**
    :   2\. you must regist it before bk\_ble\_create\_db, otherwise you cant get BLE\_5\_CREATE\_DB event

    参数
    :   **\-** – func: event callback

    返回
    :   - void

<a id="_CPPv424bk_ble_appm_get_dev_nameP7uint8_t8uint32_t"></a>

<a id="_CPPv324bk_ble_appm_get_dev_nameP7uint8_t8uint32_t"></a> <a id="_CPPv224bk_ble_appm_get_dev_nameP7uint8_t8uint32_t"></a> <a id="bk_ble_appm_get_dev_name__uint8_tP.uint32_t"></a> <a id="group__bk__ble__api__v1_1ga448a1a40bc38145553a43edcd3e481aa"></a> uint8\_t bk\_ble\_appm\_get\_dev\_name(uint8\_t \*name, uint32\_t buf\_len)
:   Get device name.

    参数
    :   **\-** – name: store the device name

        - buf\_len: the length of buf to store the device name

    返回
    :   - length: the length of device name

<a id="_CPPv424bk_ble_appm_set_dev_name7uint8_tP7uint8_t"></a>

<a id="_CPPv324bk_ble_appm_set_dev_name7uint8_tP7uint8_t"></a> <a id="_CPPv224bk_ble_appm_set_dev_name7uint8_tP7uint8_t"></a> <a id="bk_ble_appm_set_dev_name__uint8_t.uint8_tP"></a> <a id="group__bk__ble__api__v1_1gaf5cb0e30cb1ebd5711a12a9ca2346505"></a> uint8\_t bk\_ble\_appm\_set\_dev\_name(uint8\_t len, uint8\_t \*name)
:   Set device name.

    参数
    :   **\-** – len: the length of device name

        - name: the device name to be set

    返回
    :   - length: the length of device name

<a id="_CPPv425bk_ble_create_advertising7uint8_tP15ble_adv_param_t12ble_cmd_cb_t"></a>

<a id="_CPPv325bk_ble_create_advertising7uint8_tP15ble_adv_param_t12ble_cmd_cb_t"></a> <a id="_CPPv225bk_ble_create_advertising7uint8_tP15ble_adv_param_t12ble_cmd_cb_t"></a> <a id="bk_ble_create_advertising__uint8_t.ble_adv_param_tP.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1gac697edafd3d29640923bfb753f3043c2"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_create\_advertising(uint8\_t actv\_idx, [ble\_adv\_param\_t](#_CPPv415ble_adv_param_t "ble_adv_param_t") \*adv\_param, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Create a ble advertising activity.

    User example:

    ```
    ble_adv_param_t adv_param;

    adv_param.own_addr_type = OWN_ADDR_TYPE_PUBLIC_ADDR;
    adv_param.adv_type = 0; //ADV_IND
    adv_param.chnl_map = 7;
    adv_param.adv_prop = 3;
    adv_param.adv_intv_min = 0x120; //min
    adv_param.adv_intv_max = 0x160; //max
    adv_param.prim_phy = 1;// 1M
    adv_param.second_phy = 1;// 1M
    actv_idx = bk_ble_get_idle_actv_idx_handle();
    if (actv_idx != UNKNOW_ACT_IDX) {
        bk_ble_create_advertising(actv_idx, &adv_param, ble_at_cmd_cb);
    }
    ```

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    参数
    :   **\-** – actv\_idx: the index of activity

        - adv\_param: the advertising parameter
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_CREATE\_ADV

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv425bk_ble_modify_advertising7uint8_tP15ble_adv_param_t12ble_cmd_cb_t"></a>

<a id="_CPPv325bk_ble_modify_advertising7uint8_tP15ble_adv_param_t12ble_cmd_cb_t"></a> <a id="_CPPv225bk_ble_modify_advertising7uint8_tP15ble_adv_param_t12ble_cmd_cb_t"></a> <a id="bk_ble_modify_advertising__uint8_t.ble_adv_param_tP.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga3a97b348d26d694eea308c9047064488"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_modify\_advertising(uint8\_t actv\_idx, [ble\_adv\_param\_t](#_CPPv415ble_adv_param_t "ble_adv_param_t") \*adv\_param, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   modify a ble advertising activity

    **Attention**
    :   1.you must wait callback status, 0 mean success. 2.This function only be called when adv created and not started.

    参数
    :   **\-** – actv\_idx: the index of activity

        - adv\_param: the advertising parameter
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_MODIFY\_ADV

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv424bk_ble_start_advertising7uint8_t6uint1612ble_cmd_cb_t"></a>

<a id="_CPPv324bk_ble_start_advertising7uint8_t6uint1612ble_cmd_cb_t"></a> <a id="_CPPv224bk_ble_start_advertising7uint8_t6uint1612ble_cmd_cb_t"></a> <a id="bk_ble_start_advertising__uint8_t.uint16.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga91507146a662c6c47a76f52916accdd1"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_start\_advertising(uint8\_t actv\_idx, uint16 duration, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Start a ble advertising.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_advertising

    参数
    :   **\-** – actv\_idx: the index of activity

        - duration: Advertising duration (in unit of 10ms). 0 means that advertising continues
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_START\_ADV

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv428bk_ble_start_advertising_ext7uint8_t6uint167uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv328bk_ble_start_advertising_ext7uint8_t6uint167uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv228bk_ble_start_advertising_ext7uint8_t6uint167uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_start_advertising_ext__uint8_t.uint16.uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1gaafc65d89c6d6b27c446782e21291c46b"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_start\_advertising\_ext(uint8\_t actv\_idx, uint16 duration, uint8\_t max\_evt, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Start a ble advertising with a maximum number of advertising events.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_advertising

    参数
    :   **\-** – actv\_idx: the index of activity

        - duration: Advertising duration (in unit of 10ms). 0 means that advertising continues
        - max\_evt: maximum number of advertising events to send. 0 means no limit
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_START\_ADV

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv423bk_ble_stop_advertising7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv323bk_ble_stop_advertising7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv223bk_ble_stop_advertising7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_stop_advertising__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga8c6b7d094110e544c24e45ed5aff9fc5"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_stop\_advertising(uint8\_t actv\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Stop the advertising that has been started.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_start\_advertising

    参数
    :   **\-** – actv\_idx: the index of activity

        - callback: register a callback for this action, ble\_cmd\_t: BLE\_STOP\_ADV

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv425bk_ble_delete_advertising7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv325bk_ble_delete_advertising7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv225bk_ble_delete_advertising7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_delete_advertising__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga7ae152d6b52f7d01ecc975ad51cb42d3"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_delete\_advertising(uint8\_t actv\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Delete the advertising that has been created.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_advertising

    参数
    :   **\-** – actv\_idx: the index of activity

        - callback: register a callback for this action, ble\_cmd\_t: BLE\_DELETE\_ADV

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv419bk_ble_set_adv_data7uint8_tP7uint8_t7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv319bk_ble_set_adv_data7uint8_tP7uint8_t7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv219bk_ble_set_adv_data7uint8_tP7uint8_t7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_set_adv_data__uint8_t.uint8_tP.uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga2702094390c495f1392f444cdb56fa74"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_set\_adv\_data(uint8\_t actv\_idx, uint8\_t \*adv\_buff, uint8\_t adv\_len, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Set the advertising data.

    User example:

    ```
    const uint8_t adv_data[] = {0x02, 0x01, 0x06, 0x0A, 0x09, 0x37, 0x32, 0x33, 0x31, 0x4e, 0x5f, 0x42, 0x4c, 0x45};
    bk_ble_set_adv_data(actv_idx, adv_data, sizeof(adv_data), ble_at_cmd_cb);
    ```

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_advertising

    参数
    :   **\-** – actv\_idx: the index of activity

        - adv\_buff: advertising data
        - adv\_len: the length of advertising data
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_SET\_ADV\_DATA

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv424bk_ble_set_scan_rsp_data7uint8_tP7uint8_t7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv324bk_ble_set_scan_rsp_data7uint8_tP7uint8_t7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv224bk_ble_set_scan_rsp_data7uint8_tP7uint8_t7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_set_scan_rsp_data__uint8_t.uint8_tP.uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1gaf5cdf9f084cb3d354708814e98b7ee89"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_set\_scan\_rsp\_data(uint8\_t actv\_idx, uint8\_t \*scan\_buff, uint8\_t scan\_len, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Set the scan response data.

    User example:

    ```
    const uint8_t scan_data[] = {0x02, 0x01, 0x06, 0x0A, 0x09, 0x37, 0x32, 0x33, 0x31, 0x4e, 0x5f, 0x42, 0x4c, 0x45};
    bk_ble_set_scan_rsp_data(actv_idx, scan_data, sizeof(scan_data), ble_at_cmd_cb);
    ```

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.scan rsp data similaly to adv data

    **Attention**
    :   3.must used after bk\_ble\_create\_advertising

    参数
    :   **\-** – actv\_idx: the index of activity

        - scan\_buff: scan response data
        - scan\_len: the length of scan response data
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_SET\_RSP\_DATA

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv423bk_ble_set_per_adv_data7uint8_tP7uint8_t7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv323bk_ble_set_per_adv_data7uint8_tP7uint8_t7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv223bk_ble_set_per_adv_data7uint8_tP7uint8_t7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_set_per_adv_data__uint8_t.uint8_tP.uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga383697ec5d75e11dc41c229a226d37fb"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_set\_per\_adv\_data(uint8\_t actv\_idx, uint8\_t \*per\_adv\_buff, uint8\_t per\_adv\_len, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Set the periodic advertising data.

    User example:

    ```
    const uint8_t adv_data[] = {0x02, 0x01, 0x06, 0x0A, 0x09, 0x37, 0x32, 0x33, 0x31, 0x4e, 0x5f, 0x42, 0x4c, 0x45};
    bk_ble_set_per_adv_data(actv_idx, adv_data, sizeof(adv_data), ble_at_cmd_cb);
    ```

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_advertising

    参数
    :   **\-** – actv\_idx: the index of activity

        - per\_adv\_buff: periodic advertising data
        - per\_adv\_len: the length of periodic advertising data
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_SET\_ADV\_DATA

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv426bk_ble_set_adv_random_addr7uint8_tP7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv326bk_ble_set_adv_random_addr7uint8_tP7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv226bk_ble_set_adv_random_addr7uint8_tP7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_set_adv_random_addr__uint8_t.uint8_tP.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1gaafc68ebc3bb23987096b8fdd99cc7fa2"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_set\_adv\_random\_addr(uint8\_t actv\_idx, uint8\_t \*addr, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Set the adv random addr.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_advertising

    参数
    :   **\-** – actv\_idx: the index of activity

        - addr: random address
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_SET\_ADV\_RANDOM\_ADDR

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv415bk_ble_read_phy7uint8_t"></a>

<a id="_CPPv315bk_ble_read_phy7uint8_t"></a> <a id="_CPPv215bk_ble_read_phy7uint8_t"></a> <a id="bk_ble_read_phy__uint8_t"></a> <a id="group__bk__ble__api__v1_1ga8e69af76e3ebefb0d346ca9255442d7b"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_read\_phy(uint8\_t conn\_idx)
:   Read the phy of connection device.

    User example:

    ```
    bk_ble_read_phy(conn_idx);
    ```

    **Attention**
    :   1.must used after after connected

    参数
    :   **\-** – conn\_idx: the index of connection device

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv414bk_ble_set_phy7uint8_tP13ble_set_phy_t"></a>

<a id="_CPPv314bk_ble_set_phy7uint8_tP13ble_set_phy_t"></a> <a id="_CPPv214bk_ble_set_phy7uint8_tP13ble_set_phy_t"></a> <a id="bk_ble_set_phy__uint8_t.ble_set_phy_tP"></a> <a id="group__bk__ble__api__v1_1ga7bb8bab27172087eb7d85c3f453446a0"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_set\_phy(uint8\_t conn\_idx, [ble\_set\_phy\_t](#_CPPv413ble_set_phy_t "ble_set_phy_t") \*phy\_info)
:   Set the phy of connection device.

    User example:

    ```
    ble_set_phy_t * phy = {0x04, 0x01, 0x01};
    //set tx phy to s2 coded phy, and set rx phy to 1M phy
    bk_ble_set_phy(1, phy);
    ```

    **Attention**
    :   1.must used after after connected

    参数
    :   **\-** – conn\_idx: the index of connection device

        - phy\_info: phy parameters

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv419bk_ble_update_param7uint8_tP16ble_conn_param_t"></a>

<a id="_CPPv319bk_ble_update_param7uint8_tP16ble_conn_param_t"></a> <a id="_CPPv219bk_ble_update_param7uint8_tP16ble_conn_param_t"></a> <a id="bk_ble_update_param__uint8_t.ble_conn_param_tP"></a> <a id="group__bk__ble__api__v1_1ga2d069f95de976e5df02b8e6f77a011d6"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_update\_param(uint8\_t conn\_idx, [ble\_conn\_param\_t](#_CPPv416ble_conn_param_t "ble_conn_param_t") \*conn\_param)
:   Update connection parameters.

    **Attention**
    :   1.must used after connected

    参数
    :   **\-** – conn\_idx: the index of connection

        - conn\_param: connection parameters

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv417bk_ble_disconnect7uint8_t"></a>

<a id="_CPPv317bk_ble_disconnect7uint8_t"></a> <a id="_CPPv217bk_ble_disconnect7uint8_t"></a> <a id="bk_ble_disconnect__uint8_t"></a> <a id="group__bk__ble__api__v1_1gae0c8cf210cb4de1c5bb7ab84d3e604f6"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_disconnect(uint8\_t conn\_idx)
:   Disconnect a ble connection.

    **Attention**
    :   1.must used after connected

    参数
    :   **\-** – conn\_idx: the index of connection

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv422bk_ble_gatt_mtu_change7uint8_t"></a>

<a id="_CPPv322bk_ble_gatt_mtu_change7uint8_t"></a> <a id="_CPPv222bk_ble_gatt_mtu_change7uint8_t"></a> <a id="bk_ble_gatt_mtu_change__uint8_t"></a> <a id="group__bk__ble__api__v1_1gad3315e1cae014584e043e51f17cf0f03"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatt\_mtu\_change(uint8\_t conn\_idx)
:   Exchange MTU, negotiating with the local maximum MTU.

    This API always requests the local maximum MTU. If you want to negotiate a specified MTU value, use [bk\_ble\_gatt\_mtu\_change\_ex()](#group__bk__ble__api__v1_1ga4d97bc3503ed9017055acdd4865dec78) instead.

    **Attention**
    :   1.must used after connected

    参数
    :   **\-** – conn\_idx: the index of connection

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv425bk_ble_gatt_mtu_change_ex7uint8_t8uint16_t"></a>

<a id="_CPPv325bk_ble_gatt_mtu_change_ex7uint8_t8uint16_t"></a> <a id="_CPPv225bk_ble_gatt_mtu_change_ex7uint8_t8uint16_t"></a> <a id="bk_ble_gatt_mtu_change_ex__uint8_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga4d97bc3503ed9017055acdd4865dec78"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatt\_mtu\_change\_ex(uint8\_t conn\_idx, uint16\_t mtu)
:   Exchange MTU with a specified value.

    **Attention**
    :   1.must used after connected

    参数
    :   **\-** – conn\_idx: the index of connection

        - mtu: the MTU value the client requests. The finally negotiated MTU is the minimum of this value, the peer’s MTU and the local maximum MTU, and is also clamped to the minimum legal ATT MTU. Passing 0 means using the local maximum MTU (same as bk\_ble\_gatt\_mtu\_change).

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv418bk_ble_set_max_mtu8uint16_t"></a>

<a id="_CPPv318bk_ble_set_max_mtu8uint16_t"></a> <a id="_CPPv218bk_ble_set_max_mtu8uint16_t"></a> <a id="bk_ble_set_max_mtu__uint16_t"></a> <a id="group__bk__ble__api__v1_1gad3584b9ef0305ac4f8c15520d7302045"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_set\_max\_mtu(uint16\_t max\_mtu)
:   Set maximal Exchange MTU.

    **Attention**
    :   1.must used before connected

    参数
    :   **\-** – max\_mtu: the value to set

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv421bk_ble_create_scaning7uint8_tP16ble_scan_param_t12ble_cmd_cb_t"></a>

<a id="_CPPv321bk_ble_create_scaning7uint8_tP16ble_scan_param_t12ble_cmd_cb_t"></a> <a id="_CPPv221bk_ble_create_scaning7uint8_tP16ble_scan_param_t12ble_cmd_cb_t"></a> <a id="bk_ble_create_scaning__uint8_t.ble_scan_param_tP.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga0543b2a2e91eb632db83762d976ec616"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_create\_scaning(uint8\_t actv\_idx, [ble\_scan\_param\_t](#_CPPv416ble_scan_param_t "ble_scan_param_t") \*scan\_param, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Create a ble scan activity.

    User example:

    ```
    ble_scan_param_t scan_param;

    scan_param.own_addr_type = OWN_ADDR_TYPE_PUBLIC_ADDR;
    scan_param.scan_phy = 5;
    scan_param.scan_intv = 0x64; //interval
    scan_param.scan_wd = 0x1e; //windows
    bk_ble_create_scaning(actv_idx, &scan_param, ble_at_cmd);
    ```

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    参数
    :   **\-** – actv\_idx: the index of activity

        - scan\_param: the scan parameter
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_CREATE\_SCAN

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv420bk_ble_start_scaning7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv320bk_ble_start_scaning7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv220bk_ble_start_scaning7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_start_scaning__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga6ab237005c5a40cda9f44fa9776c1ce2"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_start\_scaning(uint8\_t actv\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Start a ble scan.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_scaning

    **Attention**
    :   3.adv will report in ble\_notice\_cb\_t as BLE\_5\_REPORT\_ADV

    参数
    :   **\-** – actv\_idx: the index of activity

        - callback: register a callback for this action, ble\_cmd\_t: BLE\_START\_SCAN

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv423bk_ble_start_scaning_ex7uint8_t7uint8_t8uint16_t8uint16_t12ble_cmd_cb_t"></a>

<a id="_CPPv323bk_ble_start_scaning_ex7uint8_t7uint8_t8uint16_t8uint16_t12ble_cmd_cb_t"></a> <a id="_CPPv223bk_ble_start_scaning_ex7uint8_t7uint8_t8uint16_t8uint16_t12ble_cmd_cb_t"></a> <a id="bk_ble_start_scaning_ex__uint8_t.uint8_t.uint16_t.uint16_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1gac42673372c1fce4d583e03135f099627"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_start\_scaning\_ex(uint8\_t actv\_idx, uint8\_t filt\_duplicate, uint16\_t duration, uint16\_t period, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

<a id="_CPPv419bk_ble_stop_scaning7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv319bk_ble_stop_scaning7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv219bk_ble_stop_scaning7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_stop_scaning__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga72336462591df1db0904e1a799eb7502"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_stop\_scaning(uint8\_t actv\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Stop the scan that has been started.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_start\_scaning

    参数
    :   **\-** – actv\_idx: the index of activity

        - callback: register a callback for this action, ble\_cmd\_t: BLE\_STOP\_SCAN

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv421bk_ble_delete_scaning7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv321bk_ble_delete_scaning7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv221bk_ble_delete_scaning7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_delete_scaning__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1gad109f017d81f4712a6c934bf17bb3d51"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_delete\_scaning(uint8\_t actv\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Delete the scan that has been created.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_scaning

    参数
    :   **\-** – actv\_idx: the index of activity

        - callback: register a callback for this action, ble\_cmd\_t: BLE\_DELETE\_SCAN

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv418bk_ble_create_init7uint8_tP16ble_conn_param_t12ble_cmd_cb_t"></a>

<a id="_CPPv318bk_ble_create_init7uint8_tP16ble_conn_param_t12ble_cmd_cb_t"></a> <a id="_CPPv218bk_ble_create_init7uint8_tP16ble_conn_param_t12ble_cmd_cb_t"></a> <a id="bk_ble_create_init__uint8_t.ble_conn_param_tP.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga1b4daf940ba925f1023604f1f78a69e5"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_create\_init(uint8\_t con\_idx, [ble\_conn\_param\_t](#_CPPv416ble_conn_param_t "ble_conn_param_t") \*conn\_param, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Create a activity for initiating a connection.

    User example:

    ```
    ble_conn_param_t conn_param;
    conn_param.intv_min = 0x40; //interval
    conn_param.intv_max = 0x40; //interval
    conn_param.con_latency = 0;
    conn_param.sup_to = 0x200;//supervision timeout
    conn_param.init_phys = INIT_PHY_TYPE_LE_1M;// 1M
    conn_param.filter_policy = INIT_TYPE_LE_DIRECT_CONN_EST;// initiating type, see enum \ref initiating_filter_type_le (DIRECT: connect the indicated peer address; AUTO: connect devices in the white list)
    bk_ble_create_init(con_idx, &conn_param, ble_at_cmd);
    ```

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    参数
    :   **\-** – con\_idx: the index of connection

        - conn\_param: the connection parameter
        - callback: register a callback for this action, ble\_cmd\_t: BLE\_INIT\_CREATE

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv422bk_ble_init_start_conn7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv322bk_ble_init_start_conn7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv222bk_ble_init_start_conn7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_init_start_conn__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga57dd321d593ba5ddeb24f821dc34bb96"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_init\_start\_conn(uint8\_t con\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Initiate a connection.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_init

    **Attention**
    :   3.when connect result, will recv BLE\_5\_INIT\_CONNECT\_EVENT in ble\_notice\_cb\_t

    参数
    :   **\-** – con\_idx: the index of connection

        - callback: register a callback for this action, ble\_cmd\_t: BLE\_INIT\_START\_CONN

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv421bk_ble_init_stop_conn7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv321bk_ble_init_stop_conn7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv221bk_ble_init_stop_conn7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_init_stop_conn__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga6c383277ac66a267565a8759a1fb37f3"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_init\_stop\_conn(uint8\_t con\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Stop a connection.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_init\_start\_conn

    参数
    :   **\-** – con\_idx: the index of connection

        - callback: register a callback for this action, ble\_cmd\_t: BLE\_INIT\_STOP\_CONN

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv432bk_ble_init_set_connect_dev_addr7uint8_tP9bd_addr_t7uint8_t"></a>

<a id="_CPPv332bk_ble_init_set_connect_dev_addr7uint8_tP9bd_addr_t7uint8_t"></a> <a id="_CPPv232bk_ble_init_set_connect_dev_addr7uint8_tP9bd_addr_t7uint8_t"></a> <a id="bk_ble_init_set_connect_dev_addr__uint8_t.bd_addr_tP.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga5effaee518f4279b18480590f11492b2"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_init\_set\_connect\_dev\_addr(uint8\_t connidx, [bd\_addr\_t](#_CPPv49bd_addr_t "bd_addr_t") \*bdaddr, uint8\_t addr\_type)
:   Set the address of the device to be connected.

    **Attention**
    :   1.you must wait callback status, 0 mean success.

    **Attention**
    :   2.must used after bk\_ble\_create\_init

    **Attention**
    :   3.addr\_type must right, if wrong, cant connect

    参数
    :   **\-** – connidx: the index of connection

        - bdaddr: the address of the device to be connected
        - addr\_type: the address type of the device to be connected, OWN\_ADDR\_TYPE\_PUBLIC\_ADDR means public ,OWN\_ADDR\_TYPE\_RANDOM\_ADDR means random

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv427bk_ble_create_periodic_sync7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv327bk_ble_create_periodic_sync7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv227bk_ble_create_periodic_sync7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_create_periodic_sync__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1gae223c377f88d86cfd2c00924308a884b"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_create\_periodic\_sync(uint8\_t actv\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

<a id="_CPPv426bk_ble_start_periodic_sync7uint8_tP20ble_periodic_param_t12ble_cmd_cb_t"></a>

<a id="_CPPv326bk_ble_start_periodic_sync7uint8_tP20ble_periodic_param_t12ble_cmd_cb_t"></a> <a id="_CPPv226bk_ble_start_periodic_sync7uint8_tP20ble_periodic_param_t12ble_cmd_cb_t"></a> <a id="bk_ble_start_periodic_sync__uint8_t.ble_periodic_param_tP.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1ga6fc9e9c9de75337df138562176fa7ebf"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_start\_periodic\_sync(uint8\_t actv\_idx, [ble\_periodic\_param\_t](#_CPPv420ble_periodic_param_t "ble_periodic_param_t") \*param, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

<a id="_CPPv425bk_ble_stop_periodic_sync7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv325bk_ble_stop_periodic_sync7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv225bk_ble_stop_periodic_sync7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_stop_periodic_sync__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1gaa96fa107f270ed0d7ada77fea3100dfa"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_stop\_periodic\_sync(uint8\_t actv\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

<a id="_CPPv427bk_ble_delete_periodic_sync7uint8_t12ble_cmd_cb_t"></a>

<a id="_CPPv327bk_ble_delete_periodic_sync7uint8_t12ble_cmd_cb_t"></a> <a id="_CPPv227bk_ble_delete_periodic_sync7uint8_t12ble_cmd_cb_t"></a> <a id="bk_ble_delete_periodic_sync__uint8_t.ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1_1gabed96772625693380d83c81d4b704933"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_delete\_periodic\_sync(uint8\_t actv\_idx, [ble\_cmd\_cb\_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

<a id="_CPPv431bk_ble_get_idle_actv_idx_handlev"></a>

<a id="_CPPv331bk_ble_get_idle_actv_idx_handlev"></a> <a id="_CPPv231bk_ble_get_idle_actv_idx_handlev"></a> <a id="bk_ble_get_idle_actv_idx_handle__void"></a> <a id="group__bk__ble__api__v1_1ga59256bec7de3df45f39570d5ef69d082"></a> uint8\_t bk\_ble\_get\_idle\_actv\_idx\_handle(void)
:   Get an idle activity.

    返回
    :   - xx: the idle activity’s index

<a id="_CPPv429bk_ble_get_max_actv_idx_countv"></a>

<a id="_CPPv329bk_ble_get_max_actv_idx_countv"></a> <a id="_CPPv229bk_ble_get_max_actv_idx_countv"></a> <a id="bk_ble_get_max_actv_idx_count__void"></a> <a id="group__bk__ble__api__v1_1gada33374d8018856640754918b9297e1d"></a> uint8\_t bk\_ble\_get\_max\_actv\_idx\_count(void)
:   Get the maximum count of activities.

    返回
    :   - xx: the maximum count of activities

<a id="_CPPv429bk_ble_get_max_conn_idx_countv"></a>

<a id="_CPPv329bk_ble_get_max_conn_idx_countv"></a> <a id="_CPPv229bk_ble_get_max_conn_idx_countv"></a> <a id="bk_ble_get_max_conn_idx_count__void"></a> <a id="group__bk__ble__api__v1_1ga5974f690de4bd01eba232d898fc21173"></a> uint8\_t bk\_ble\_get\_max\_conn\_idx\_count(void)
:   Get the maximum count of supported connections.

    返回
    :   - xx: the maximum count of supported connections

<a id="_CPPv431bk_ble_get_idle_conn_idx_handlev"></a>

<a id="_CPPv331bk_ble_get_idle_conn_idx_handlev"></a> <a id="_CPPv231bk_ble_get_idle_conn_idx_handlev"></a> <a id="bk_ble_get_idle_conn_idx_handle__void"></a> <a id="group__bk__ble__api__v1_1ga127748f4f5b2d17a8326ac63af539254"></a> uint8\_t bk\_ble\_get\_idle\_conn\_idx\_handle(void)
:   Get an idle connection activity.

    返回
    :   - xx: the idle connection activity’s index

<a id="_CPPv430bk_ble_find_conn_idx_from_addrP9bd_addr_t"></a>

<a id="_CPPv330bk_ble_find_conn_idx_from_addrP9bd_addr_t"></a> <a id="_CPPv230bk_ble_find_conn_idx_from_addrP9bd_addr_t"></a> <a id="bk_ble_find_conn_idx_from_addr__bd_addr_tP"></a> <a id="group__bk__ble__api__v1_1gacaf401abda1e95bf14f3e7b4b14e9d31"></a> uint8\_t bk\_ble\_find\_conn\_idx\_from\_addr([bd\_addr\_t](#_CPPv49bd_addr_t "bd_addr_t") \*connt\_addr)
:   Find the specific connection activity by address.

    参数
    :   **\-** – connt\_addr: the address of the connected device

    返回
    :   - xx: the index of the connection activity meeting the address

<a id="_CPPv424bk_ble_get_connect_stateP9bd_addr_t"></a>

<a id="_CPPv324bk_ble_get_connect_stateP9bd_addr_t"></a> <a id="_CPPv224bk_ble_get_connect_stateP9bd_addr_t"></a> <a id="bk_ble_get_connect_state__bd_addr_tP"></a> <a id="group__bk__ble__api__v1_1ga3048473f9c8c4c226eeb664e7e53a430"></a> uint8\_t bk\_ble\_get\_connect\_state([bd\_addr\_t](#_CPPv49bd_addr_t "bd_addr_t") \*connt\_addr)
:   Get the connection state of the specific device.

    参数
    :   **\-** – connt\_addr: the device’s address

    返回
    :   - 1: this device is connected
        - 0: this device is disconnected

<a id="_CPPv414bk_ble_get_macP7uint8_t"></a>

<a id="_CPPv314bk_ble_get_macP7uint8_t"></a> <a id="_CPPv214bk_ble_get_macP7uint8_t"></a> <a id="bk_ble_get_mac__uint8_tP"></a> <a id="group__bk__ble__api__v1_1ga7473327e2502d76d164da8dffd05c58c"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_get\_mac(uint8\_t \*mac)
:   get ble mac addr,this api is deprecated,please use bk\_bluetooth\_get\_address

    **Attention**
    :   1\. return mac is 6 bytes.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv422bk_ble_send_noti_value7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t"></a>

<a id="_CPPv322bk_ble_send_noti_value7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t"></a> <a id="_CPPv222bk_ble_send_noti_value7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t"></a> <a id="bk_ble_send_noti_value__uint8_t.uint32_t.uint8_tP.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga743b3b5e1a8789a83099ab260115a6c7"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_send\_noti\_value(uint8\_t con\_idx, uint32\_t len, uint8\_t \*buf, uint16\_t prf\_id, uint16\_t att\_idx)
:   As slaver, send a notification of an attribute’s value.

    参数
    :   **\-** – con\_idx: the index of connection

        - len: the length of attribute’s value
        - buf: attribute’s value
        - prf\_id: The id of the profile
        - att\_idx: The index of the attribute

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv421bk_ble_send_ind_value7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t"></a>

<a id="_CPPv321bk_ble_send_ind_value7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t"></a> <a id="_CPPv221bk_ble_send_ind_value7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t"></a> <a id="bk_ble_send_ind_value__uint8_t.uint32_t.uint8_tP.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga1762c826416150f03376d283904c27a0"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_send\_ind\_value(uint8\_t con\_idx, uint32\_t len, uint8\_t \*buf, uint16\_t prf\_id, uint16\_t att\_idx)
:   As slaver, send an indication of an attribute’s value.

    参数
    :   **\-** – con\_idx: the index of connection

        - len: the length of attribute’s value
        - buf: attribute’s value
        - prf\_id: The id of the profile
        - att\_idx: The index of the attribute

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv428bk_ble_reg_hci_recv_callback18ble_hci_to_host_cb18ble_hci_to_host_cb"></a>

<a id="_CPPv328bk_ble_reg_hci_recv_callback18ble_hci_to_host_cb18ble_hci_to_host_cb"></a> <a id="_CPPv228bk_ble_reg_hci_recv_callback18ble_hci_to_host_cb18ble_hci_to_host_cb"></a> <a id="bk_ble_reg_hci_recv_callback__ble_hci_to_host_cb.ble_hci_to_host_cb"></a> <a id="group__bk__ble__api__v1_1ga0f4a056d95139bcd0ab6e1da8c58c0a2"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_reg\_hci\_recv\_callback([ble\_hci\_to\_host\_cb](#_CPPv418ble_hci_to_host_cb "ble_hci_to_host_cb") evt\_cb, [ble\_hci\_to\_host\_cb](#_CPPv418ble_hci_to_host_cb "ble_hci_to_host_cb") acl\_cb)
:   reg hci recv callback

    **Attention**
    :   1\. you must call this after recv BLE\_5\_STACK\_OK evt !

    参数
    :   **\-** – evt\_cb: evt callback function

        - acl\_cb: acl callback function

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv424bk_ble_hci_to_controller7uint8_tP7uint8_t8uint16_t"></a>

<a id="_CPPv324bk_ble_hci_to_controller7uint8_tP7uint8_t8uint16_t"></a> <a id="_CPPv224bk_ble_hci_to_controller7uint8_tP7uint8_t8uint16_t"></a> <a id="bk_ble_hci_to_controller__uint8_t.uint8_tP.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga3ec321524722d7477284ca9058c2140f"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_hci\_to\_controller(uint8\_t type, uint8\_t \*buf, uint16\_t len)
:   send hci to controller.

    **Attention**
    :   1\. you must call this after bk\_ble\_reg\_hci\_recv\_callback !

    参数
    :   **\-** – type: see [BK\_BLE\_HCI\_TYPE](#group__bk__ble__api__v1_1ga28e61788890c70b81bec53fc9a5ea22c).

        - buf: payload
        - len: buf’s len

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed

<a id="_CPPv428bk_ble_hci_cmd_to_controllerP7uint8_t8uint16_t"></a>

<a id="_CPPv328bk_ble_hci_cmd_to_controllerP7uint8_t8uint16_t"></a> <a id="_CPPv228bk_ble_hci_cmd_to_controllerP7uint8_t8uint16_t"></a> <a id="bk_ble_hci_cmd_to_controller__uint8_tP.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga1ef1a5b9e5879e45c132c00113c80210"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_hci\_cmd\_to\_controller(uint8\_t \*buf, uint16\_t len)
:   send hci cmd to controller.

    **Attention**
    :   1\. you must call this after bk\_ble\_reg\_hci\_recv\_callback !

    参数
    :   **\-** – buf: payload

        - len: buf’s len

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed

<a id="_CPPv428bk_ble_hci_acl_to_controllerP7uint8_t8uint16_t"></a>

<a id="_CPPv328bk_ble_hci_acl_to_controllerP7uint8_t8uint16_t"></a> <a id="_CPPv228bk_ble_hci_acl_to_controllerP7uint8_t8uint16_t"></a> <a id="bk_ble_hci_acl_to_controller__uint8_tP.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga42c06f4782cd0f9269ef723299c5656e"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_hci\_acl\_to\_controller(uint8\_t \*buf, uint16\_t len)
:   send hci acl to controller.

    **Attention**
    :   1\. you must call this after bk\_ble\_reg\_hci\_recv\_callback !

    参数
    :   **\-** – buf: payload

        - len: buf’s len

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed

<a id="_CPPv425bk_ble_if_support_centralP7uint8_t"></a>

<a id="_CPPv325bk_ble_if_support_centralP7uint8_t"></a> <a id="_CPPv225bk_ble_if_support_centralP7uint8_t"></a> <a id="bk_ble_if_support_central__uint8_tP"></a> <a id="group__bk__ble__api__v1_1gab48622b9f97434399b0057e2d7fa7a4d"></a> uint8\_t bk\_ble\_if\_support\_central(uint8\_t \*count)

<a id="_CPPv432bk_ble_get_controller_stack_typev"></a>

<a id="_CPPv332bk_ble_get_controller_stack_typev"></a> <a id="_CPPv232bk_ble_get_controller_stack_typev"></a> <a id="bk_ble_get_controller_stack_type__void"></a> <a id="group__bk__ble__api__v1_1gad34af9c7166e9e393789e03c8c06a23f"></a> [BK\_BLE\_CONTROLLER\_STACK\_TYPE](#_CPPv428BK_BLE_CONTROLLER_STACK_TYPE "BK_BLE_CONTROLLER_STACK_TYPE") bk\_ble\_get\_controller\_stack\_type(void)

<a id="_CPPv426bk_ble_get_host_stack_typev"></a>

<a id="_CPPv326bk_ble_get_host_stack_typev"></a> <a id="_CPPv226bk_ble_get_host_stack_typev"></a> <a id="bk_ble_get_host_stack_type__void"></a> <a id="group__bk__ble__api__v1_1gaaf9743eb06680f2d5fba04e6c2b526d0"></a> [BK\_BLE\_HOST\_STACK\_TYPE](#_CPPv422BK_BLE_HOST_STACK_TYPE "BK_BLE_HOST_STACK_TYPE") bk\_ble\_get\_host\_stack\_type(void)

<a id="_CPPv420bk_ble_get_env_statev"></a>

<a id="_CPPv320bk_ble_get_env_statev"></a> <a id="_CPPv220bk_ble_get_env_statev"></a> <a id="bk_ble_get_env_state__void"></a> <a id="group__bk__ble__api__v1_1ga3a4ee0a3aaf16dac82123483730cdedb"></a> uint8\_t bk\_ble\_get\_env\_state(void)

<a id="_CPPv426bk_ble_set_task_stack_size8uint16_t"></a>

<a id="_CPPv326bk_ble_set_task_stack_size8uint16_t"></a> <a id="_CPPv226bk_ble_set_task_stack_size8uint16_t"></a> <a id="bk_ble_set_task_stack_size__uint16_t"></a> <a id="group__bk__ble__api__v1_1gacdc2660fdb8672cdd73749f91c952f29"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_set\_task\_stack\_size(uint16\_t size)

<a id="_CPPv439bk_ble_register_app_sdp_charac_callback23app_sdp_charac_callback"></a>

<a id="_CPPv339bk_ble_register_app_sdp_charac_callback23app_sdp_charac_callback"></a> <a id="_CPPv239bk_ble_register_app_sdp_charac_callback23app_sdp_charac_callback"></a> <a id="bk_ble_register_app_sdp_charac_callback__app_sdp_charac_callback"></a> <a id="group__bk__ble__api__v1_1gae17451331278acf39079608c0f31cf9d"></a> void bk\_ble\_register\_app\_sdp\_charac\_callback([app\_sdp\_charac\_callback](#_CPPv423app_sdp_charac_callback "app_sdp_charac_callback") cb)

<a id="_CPPv439bk_ble_register_app_sdp_common_callback21app_sdp_comm_callback"></a>

<a id="_CPPv339bk_ble_register_app_sdp_common_callback21app_sdp_comm_callback"></a> <a id="_CPPv239bk_ble_register_app_sdp_common_callback21app_sdp_comm_callback"></a> <a id="bk_ble_register_app_sdp_common_callback__app_sdp_comm_callback"></a> <a id="group__bk__ble__api__v1_1ga1c7f8f3a73702fe8ecc729d960e08274"></a> void bk\_ble\_register\_app\_sdp\_common\_callback([app\_sdp\_comm\_callback](#_CPPv421app_sdp_comm_callback "app_sdp_comm_callback") cb)

<a id="_CPPv421bk_ble_gatt_write_ccc7uint8_t8uint16_t8uint16_t"></a>

<a id="_CPPv321bk_ble_gatt_write_ccc7uint8_t8uint16_t8uint16_t"></a> <a id="_CPPv221bk_ble_gatt_write_ccc7uint8_t8uint16_t8uint16_t"></a> <a id="bk_ble_gatt_write_ccc__uint8_t.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga7eef50132e596d6d6e46cd48d44afbf4"></a> uint8\_t bk\_ble\_gatt\_write\_ccc(uint8\_t con\_idx, uint16\_t ccc\_handle, uint16\_t ccc\_value)
:   As master, enable notification or indication.

    参数
    :   **\-** – con\_idx: the index of connection

        - ccc\_handle: the handle of Client Characteristic Configuration descriptor
        - ccc\_value: descriptor value, 0x01 means notification ,0x02 means indication

    返回
    :   - 0: succeed
        - others: errors.

<a id="_CPPv423bk_ble_gatt_write_value7uint8_t8uint16_t8uint16_tP7uint8_t"></a>

<a id="_CPPv323bk_ble_gatt_write_value7uint8_t8uint16_t8uint16_tP7uint8_t"></a> <a id="_CPPv223bk_ble_gatt_write_value7uint8_t8uint16_t8uint16_tP7uint8_t"></a> <a id="bk_ble_gatt_write_value__uint8_t.uint16_t.uint16_t.uint8_tP"></a> <a id="group__bk__ble__api__v1_1ga5d8594b965d7972b27469437d1fafb54"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gatt\_write\_value(uint8\_t con\_idx, uint16\_t att\_handle, uint16\_t len, uint8\_t \*data)
:   As master, write attribute value.

    参数
    :   **\-** – con\_idx: the index of connection

        - att\_handle: the handle of attribute value
        - data: value data
        - len: the length of attribute value

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv426bk_ble_read_response_value7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t"></a>

<a id="_CPPv326bk_ble_read_response_value7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t"></a> <a id="_CPPv226bk_ble_read_response_value7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t"></a> <a id="bk_ble_read_response_value__uint8_t.uint32_t.uint8_tP.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga891545eb2345032de540840166c483a8"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_read\_response\_value(uint8\_t con\_idx, uint32\_t len, uint8\_t \*buf, uint16\_t prf\_id, uint16\_t att\_idx)
:   As slaver, send response value.

    参数
    :   **\-** – con\_idx: the idx of app connections

        - len: the length of attribute’s value
        - buf: attribute’s value
        - prf\_id: The id of the profile
        - att\_idx: The index of the attribute

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv430bk_ble_read_response_value_ext7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t7uint8_t"></a>

<a id="_CPPv330bk_ble_read_response_value_ext7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t7uint8_t"></a> <a id="_CPPv230bk_ble_read_response_value_ext7uint8_t8uint32_tP7uint8_t8uint16_t8uint16_t7uint8_t"></a> <a id="bk_ble_read_response_value_ext__uint8_t.uint32_t.uint8_tP.uint16_t.uint16_t.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga8a072ba053e04a14545611bfea8e2655"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_read\_response\_value\_ext(uint8\_t con\_idx, uint32\_t len, uint8\_t \*buf, uint16\_t prf\_id, uint16\_t att\_idx, uint8\_t ret\_status)
:   As slaver, send read response value with a return status.

    Same as [bk\_ble\_read\_response\_value()](#group__bk__ble__api__v1_1ga891545eb2345032de540840166c483a8), but allows the application to report a specific ATT error status to the peer instead of always returning success.

    参数
    :   **\-** – con\_idx: the idx of app connections

        - len: the length of attribute’s value
        - buf: attribute’s value
        - prf\_id: The id of the profile
        - att\_idx: The index of the attribute
        - ret\_status: ATT return status (0 means success, non-zero means the ATT error code reported to peer)

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv421bk_ble_write_response7uint8_t8uint16_t8uint16_t7uint8_t"></a>

<a id="_CPPv321bk_ble_write_response7uint8_t8uint16_t8uint16_t7uint8_t"></a> <a id="_CPPv221bk_ble_write_response7uint8_t8uint16_t8uint16_t7uint8_t"></a> <a id="bk_ble_write_response__uint8_t.uint16_t.uint16_t.uint8_t"></a> <a id="group__bk__ble__api__v1_1gaaf96a877e9e5fe902a2e83da2d01f27a"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_write\_response(uint8\_t con\_idx, uint16\_t prf\_id, uint16\_t att\_idx, uint8\_t ret\_status)
:   As slaver, send write response (confirm a Write Request) to the peer.

    Sends the ATT Write Response for a Write Request that was reported to the application via BLE\_5\_WRITE\_EVENT, optionally carrying an ATT error code.

    **Attention**
    :   - This API MUST ONLY be called when the auto write-response feature (\_auto\_rsp\_write\_req) is DISABLED. When \_auto\_rsp\_write\_req is enabled, the stack automatically confirms every Write Request with a success status, so calling this API would send a duplicate GATTC\_WRITE\_CFM and may cause a mismatched/incorrect write response. In that mode the application should only process the data reported by BLE\_5\_WRITE\_EVENT and MUST NOT call this API.
        - When \_auto\_rsp\_write\_req is disabled, call this API after receiving BLE\_5\_WRITE\_EVENT and before the peer’s request times out, to confirm the Write Request or return a specific ATT error to the peer (e.g. invalid length, out-of-range value, insufficient authorization).
        - Only applies to a Write Request ([ble\_write\_req\_t.is\_cmd](#structble__write__req__t_1a3935f8e8d59e51753a134571e06f9ec0) \=\= 0). Do NOT call it for a Write Command (is\_cmd \=\= 1), which expects no response.

    参数
    :   **\-** – con\_idx: the idx of app connections

        - prf\_id: The id of the profile
        - att\_idx: The index of the attribute
        - ret\_status: ATT return status (0 means success, non-zero means the ATT error code reported to peer)

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv425bk_ble_sec_send_auth_mode7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv325bk_ble_sec_send_auth_mode7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv225bk_ble_sec_send_auth_mode7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a> <a id="bk_ble_sec_send_auth_mode__uint8_t.uint8_t.uint8_t.uint8_t.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga3b406cbb6440cbff728fb52de36f91e6"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_sec\_send\_auth\_mode(uint8\_t con\_idx, uint8\_t mode, uint8\_t iocap, uint8\_t sec\_req, uint8\_t oob)
:   As slave, accept a pairing request from peer with the specified security features.

    Used by the SLAVE (pairing responder) inside the BLE\_5\_PAIRING\_REQ event handler to accept the pairing initiated by the peer, replying the Pairing Response with the given features. To reject instead, use [bk\_ble\_reject\_pairing()](#group__bk__ble__api__v1_1ga443972f2fd64e485a46614c16f7d74c3). Not used by the master; the master sets its own features when it initiates pairing via [bk\_ble\_create\_bond()](#group__bk__ble__api__v1_1gac786e0c3ad011349f19ccfc337037ce9)/bk\_ble\_create\_bond\_ext().

    参数
    :   **\-** – con\_idx: the index of connection

        - mode: authentication features (see enum gap\_auth)
        - iocap: IO Capability Values (see enum bk\_ble\_gap\_io\_cap)
        - sec\_req: Security Defines (see enum gap\_sec\_req)
        - oob: OOB Data Present Flag Values (see enum gap\_oob)

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv429bk_ble_sec_send_auth_mode_ext7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv329bk_ble_sec_send_auth_mode_ext7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv229bk_ble_sec_send_auth_mode_ext7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a> <a id="bk_ble_sec_send_auth_mode_ext__uint8_t.uint8_t.uint8_t.uint8_t.uint8_t.uint8_t.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga2e5becd15200d2f15376b7f58754963b"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_sec\_send\_auth\_mode\_ext(uint8\_t con\_idx, uint8\_t mode, uint8\_t iocap, uint8\_t sec\_req, uint8\_t oob, uint8\_t initiator\_key\_distr, uint8\_t responder\_key\_distr)
:   As slave, accept a pairing request from peer with security features and key distribution.

    Same as [bk\_ble\_sec\_send\_auth\_mode()](#group__bk__ble__api__v1_1ga3b406cbb6440cbff728fb52de36f91e6) but also specifies the initiator/responder key distribution. Used by the SLAVE (pairing responder) inside the BLE\_5\_PAIRING\_REQ event handler to accept the pairing initiated by the peer. To reject instead, use [bk\_ble\_reject\_pairing()](#group__bk__ble__api__v1_1ga443972f2fd64e485a46614c16f7d74c3).

    参数
    :   **\-** – con\_idx: the index of connection

        - mode: authentication features (see enum gap\_auth)
        - iocap: IO Capability Values (see enum bk\_ble\_gap\_io\_cap)
        - sec\_req: Security Defines (see enum gap\_sec\_req)
        - oob: OOB Data Present Flag Values (see enum gap\_oob)
        - initiator\_key\_distr: init key distr, see gap\_key\_distr
        - responder\_key\_distr: resp key distr, see gap\_key\_distr

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv421bk_ble_reject_pairing7uint8_t"></a>

<a id="_CPPv321bk_ble_reject_pairing7uint8_t"></a> <a id="_CPPv221bk_ble_reject_pairing7uint8_t"></a> <a id="bk_ble_reject_pairing__uint8_t"></a> <a id="group__bk__ble__api__v1_1ga443972f2fd64e485a46614c16f7d74c3"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_reject\_pairing(uint8\_t con\_idx)
:   As slave, reject a pairing request from peer.

    **Attention**
    :   Used by the SLAVE (pairing responder) in the BLE\_5\_PAIRING\_REQ event handler when the local side wants to reject the pairing request initiated by the peer. Only valid for the slave role; to accept instead, use [bk\_ble\_sec\_send\_auth\_mode()](#group__bk__ble__api__v1_1ga3b406cbb6440cbff728fb52de36f91e6)/\_ext().

    参数
    :   **\-** – con\_idx: the index of connection

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv411bk_ble_initv"></a>

<a id="_CPPv311bk_ble_initv"></a> <a id="_CPPv211bk_ble_initv"></a> <a id="bk_ble_init__void"></a> <a id="group__bk__ble__api__v1_1ga6e2fb78d12d18f8adfa8221a4dc9d4b4"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_init(void)
:   ble init function,this api is deprecated,please use bk\_bluetooth\_init.

    Param

<a id="_CPPv413bk_ble_deinitv"></a>

<a id="_CPPv313bk_ble_deinitv"></a> <a id="_CPPv213bk_ble_deinitv"></a> <a id="bk_ble_deinit__void"></a> <a id="group__bk__ble__api__v1_1gaf520ce1148fdad9b4f3eb3841ef07091"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_deinit(void)
:   ble deinit function,this api is deprecated,please use bk\_bluetooth\_deinit.

    Param

<a id="_CPPv421bk_ble_delete_serviceP13bk_ble_db_cfg"></a>

<a id="_CPPv321bk_ble_delete_serviceP13bk_ble_db_cfg"></a> <a id="_CPPv221bk_ble_delete_serviceP13bk_ble_db_cfg"></a> <a id="bk_ble_delete_service__bk_ble_db_cfgP"></a> <a id="group__bk__ble__api__v1_1gad0471e4a212ec50d89da0237ca07c3fe"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_delete\_service(struct [bk\_ble\_db\_cfg](#_CPPv413bk_ble_db_cfg "bk_ble_db_cfg") \*ble\_db\_cfg)
:   Unregister a gatt service.

    User example:

    ```
    struct bk_ble_db_cfg ble_db_cfg;
    uint16 service_uuid = 0x1800;

    os_memcpy(&(ble_db_cfg.uuid[0]), &service_uuid, 2);
    ble_db_cfg.svc_perm = BK_BLE_PERM_SET(SVC_UUID_LEN, UUID_16);
    ```

    **Attention**
    :   1.you must set the uuid of service and the len of uuid.

    参数
    :   **\-** – ble\_db\_cfg: service param

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv415bk_ble_att_read7uint8_t8uint16_t"></a>

<a id="_CPPv315bk_ble_att_read7uint8_t8uint16_t"></a> <a id="_CPPv215bk_ble_att_read7uint8_t8uint16_t"></a> <a id="bk_ble_att_read__uint8_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga2dff3792fbbce670c5eb9bab35a8a68f"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_att\_read(uint8\_t con\_idx, uint16\_t att\_handle)
:   As master, read attribute value, the result is reported in the callback registered through bk\_ble\_register\_app\_sdp\_charac\_callback.

    参数
    :   **\-** – con\_idx: the index of connection

        - att\_handle: the handle of attribute value

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv418bk_ble_create_bond7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv318bk_ble_create_bond7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv218bk_ble_create_bond7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a> <a id="bk_ble_create_bond__uint8_t.uint8_t.uint8_t.uint8_t.uint8_t"></a> <a id="group__bk__ble__api__v1_1gac786e0c3ad011349f19ccfc337037ce9"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_create\_bond(uint8\_t con\_idx, uint8\_t auth, uint8\_t iocap, uint8\_t sec\_req, uint8\_t oob)
:   Start the security procedure on the link (usable by both master and slave)

    - As MASTER: if the link is not bonded it starts pairing (sends a Pairing Request); if already bonded it starts encryption using the stored LTK.
    - As SLAVE : it sends a Security Request asking the master to start pairing/encryption.

    **Attention**
    :   if the link has not been bonded, it will trigger pairing, otherwise it will trigger the link encryption.

    参数
    :   **\-** – con\_idx: the index of connection

        - auth: authentication features(see enum [gap\_auth](#group__bk__ble__api__v1__typedef_1gabddf59399b398b7d0cdb34f77becadb8))
        - iocap: IO Capability Values(see enum [bk\_ble\_gap\_io\_cap](#group__bk__ble__api__v1__typedef_1ga47c2938c3450762bfc853c0891ce35d4))
        - sec\_req: Security Defines(see enum [gap\_sec\_req](#group__bk__ble__api__v1__typedef_1ga5bdf085cbe078d063965de5462611445))
        - oob: OOB Data Present Flag Values(see enum [gap\_oob](#group__bk__ble__api__v1__typedef_1ga009fe656dba3e223453288e3fc6fa68c))

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv422bk_ble_create_bond_ext7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv322bk_ble_create_bond_ext7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv222bk_ble_create_bond_ext7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t7uint8_t"></a> <a id="bk_ble_create_bond_ext__uint8_t.uint8_t.uint8_t.uint8_t.uint8_t.uint8_t.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga2427a2bc27b9a7472534821dd603cf34"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_create\_bond\_ext(uint8\_t con\_idx, uint8\_t auth, uint8\_t iocap, uint8\_t sec\_req, uint8\_t oob, uint8\_t initiator\_key\_distr, uint8\_t responder\_key\_distr)
:   Start the security procedure on the link with key distribution (usable by both master and slave)

    Same as [bk\_ble\_create\_bond()](#group__bk__ble__api__v1_1gac786e0c3ad011349f19ccfc337037ce9) but also specifies the initiator/responder key distribution.

    - As MASTER: if not bonded it starts pairing; if already bonded it starts encryption.
    - As SLAVE : it sends a Security Request asking the master to start pairing/encryption.

    **Attention**
    :   if the link has not been bonded, it will trigger pairing, otherwise it will trigger the link encryption.

    参数
    :   **\-** – con\_idx: the index of connection

        - auth: authentication features(see enum [gap\_auth](#group__bk__ble__api__v1__typedef_1gabddf59399b398b7d0cdb34f77becadb8))
        - iocap: IO Capability Values(see enum [bk\_ble\_gap\_io\_cap](#group__bk__ble__api__v1__typedef_1ga47c2938c3450762bfc853c0891ce35d4))
        - sec\_req: Security Defines(see enum [gap\_sec\_req](#group__bk__ble__api__v1__typedef_1ga5bdf085cbe078d063965de5462611445))
        - oob: OOB Data Present Flag Values(see enum [gap\_oob](#group__bk__ble__api__v1__typedef_1ga009fe656dba3e223453288e3fc6fa68c))
        - initiator\_key\_distr: init key distr, see gap\_key\_distr
        - responder\_key\_distr: resp key distr, see gap\_key\_distr

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv419bk_ble_passkey_send7uint8_t7uint8_t8uint32_t"></a>

<a id="_CPPv319bk_ble_passkey_send7uint8_t7uint8_t8uint32_t"></a> <a id="_CPPv219bk_ble_passkey_send7uint8_t7uint8_t8uint32_t"></a> <a id="bk_ble_passkey_send__uint8_t.uint8_t.uint32_t"></a> <a id="group__bk__ble__api__v1_1gad3908431a386c015571bc53cdcc53b8d"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_passkey\_send(uint8\_t con\_idx, uint8\_t accept, uint32\_t passkey)
:   Reply the passkey during pairing (Passkey Entry model; usable by both master and slave)

    **Attention**
    :   Call this in response to the BLE\_5\_PARING\_PASSKEY\_INPUT\_REQ event, when the local side needs to input the passkey displayed on the peer. Applies to whichever role received the request (master or slave).

    参数
    :   **\-** – con\_idx: the index of connection

        - accept: accept(true) / reject(false) the pairing
        - passkey: the num that peer need to input or local need to input

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv426bk_ble_number_compare_send7uint8_t7uint8_t"></a>

<a id="_CPPv326bk_ble_number_compare_send7uint8_t7uint8_t"></a> <a id="_CPPv226bk_ble_number_compare_send7uint8_t7uint8_t"></a> <a id="bk_ble_number_compare_send__uint8_t.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga5d75e7894809d173a6d4c85239735cc5"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_number\_compare\_send(uint8\_t con\_idx, uint8\_t accept)
:   Reply the numeric comparison result during LE Secure Connections pairing (Numeric Comparison model; usable by both master and slave)

    **Attention**
    :   Call this in response to the BLE\_5\_PARING\_NUMBER\_COMPARE\_REQ\_EVENT event after the user confirms whether the two displayed 6-digit values match. Applies to whichever role received the request (master or slave).

    参数
    :   **\-** – con\_idx: the index of connection

        - accept: accept(true) / reject(false) the pairing

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv416bk_ble_read_rssi7uint8_t"></a>

<a id="_CPPv316bk_ble_read_rssi7uint8_t"></a> <a id="_CPPv216bk_ble_read_rssi7uint8_t"></a> <a id="bk_ble_read_rssi__uint8_t"></a> <a id="group__bk__ble__api__v1_1ga826f2819108947636cd1f673a930f85f"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_read\_rssi(uint8\_t conn\_idx)
:   Read the rssi of connection device. The result will report in callback registered through bk\_ble\_set\_notice\_cb with evt BLE\_5\_READ\_RSSI\_CMPL\_EVENT, and param is [ble\_read\_rssi\_rsp\_t](#structble__read__rssi__rsp__t) \*.

    User example:

    ```
    bk_ble_read_rssi(conn_idx);
    ```

    **Attention**
    :   1.must used after after connected

    参数
    :   **\-** – conn\_idx: the index of connection device

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv430bk_ble_config_local_appearance8uint16_t"></a>

<a id="_CPPv330bk_ble_config_local_appearance8uint16_t"></a> <a id="_CPPv230bk_ble_config_local_appearance8uint16_t"></a> <a id="bk_ble_config_local_appearance__uint16_t"></a> <a id="group__bk__ble__api__v1_1ga6275e926ec40b18a657121c793306011"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_config\_local\_appearance(uint16\_t appearance)
:   set local gap appearance

    参数
    :   **appearance** – **\[in\]** \- External appearance value, these values are defined by the Bluetooth SIG, please refer to <https://specificationrefs.bluetooth.com/assigned-values/Appearance%20Values.pdf>

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv431bk_ble_discover_primary_service7uint8_t8uint16_t8uint16_t"></a>

<a id="_CPPv331bk_ble_discover_primary_service7uint8_t8uint16_t8uint16_t"></a> <a id="_CPPv231bk_ble_discover_primary_service7uint8_t8uint16_t8uint16_t"></a> <a id="bk_ble_discover_primary_service__uint8_t.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga6a47d52c21bd14dca65e649a803ada8c"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_discover\_primary\_service(uint8\_t conn\_id, uint16\_t sh, uint16\_t eh)
:   Discover peer primary service. The result is report in the callback registered through bk\_ble\_register\_app\_sdp\_common\_callback, and evt is MST\_TYPE\_DISCOVER\_PRI\_SERVICE\_RSP. When completed, callback will report MST\_TYPE\_DISCOVER\_COMPLETED with [ble\_descover\_complete\_inf](#structble__descover__complete__inf) and MST\_TYPE\_DISCOVER\_PRI\_SERVICE\_RSP.

    参数
    :   **\-** – sh: att start handle

        - eh: att end handle

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv439bk_ble_discover_primary_service_by_uuid7uint8_t8uint16_t8uint16_t8uint16_t"></a>

<a id="_CPPv339bk_ble_discover_primary_service_by_uuid7uint8_t8uint16_t8uint16_t8uint16_t"></a> <a id="_CPPv239bk_ble_discover_primary_service_by_uuid7uint8_t8uint16_t8uint16_t8uint16_t"></a> <a id="bk_ble_discover_primary_service_by_uuid__uint8_t.uint16_t.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1gacd90936a4c76203ced8af706c795f83e"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_discover\_primary\_service\_by\_uuid(uint8\_t conn\_id, uint16\_t sh, uint16\_t eh, uint16\_t uuid)
:   Discover peer primary service. The result is report in the callback registered through bk\_ble\_register\_app\_sdp\_common\_callback, and evt is MST\_TYPE\_DISCOVER\_PRI\_SERVICE\_BY\_UUID\_RSP. When completed, callback will report MST\_TYPE\_DISCOVER\_COMPLETED with [ble\_descover\_complete\_inf](#structble__descover__complete__inf) and MST\_TYPE\_DISCOVER\_PRI\_SERVICE\_BY\_UUID\_RSP.

    参数
    :   **\-** – sh: att start handle

        - eh: att end handle

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed

<a id="_CPPv442bk_ble_discover_primary_service_by_128uuid7uint8_t8uint16_t8uint16_tP7uint8_t"></a>

<a id="_CPPv342bk_ble_discover_primary_service_by_128uuid7uint8_t8uint16_t8uint16_tP7uint8_t"></a> <a id="_CPPv242bk_ble_discover_primary_service_by_128uuid7uint8_t8uint16_t8uint16_tP7uint8_t"></a> <a id="bk_ble_discover_primary_service_by_128uuid__uint8_t.uint16_t.uint16_t.uint8_tP"></a> <a id="group__bk__ble__api__v1_1gaa0f48fe52635ed8291f4bb8f20f3c1e8"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_discover\_primary\_service\_by\_128uuid(uint8\_t conn\_id, uint16\_t sh, uint16\_t eh, uint8\_t \*uuid)
:   Discover peer primary service. The result is report in the callback registered through bk\_ble\_register\_app\_sdp\_common\_callback, and evt is MST\_TYPE\_DISCOVER\_PRI\_SERVICE\_BY\_128\_UUID\_RSP. When completed, callback will report MST\_TYPE\_DISCOVER\_COMPLETED with [ble\_descover\_complete\_inf](#structble__descover__complete__inf) and MST\_TYPE\_DISCOVER\_PRI\_SERVICE\_BY\_128\_UUID\_RSP. bk\_ble\_read\_rssi(conn\_idx);.

    参数
    :   **\-** – conn\_id: the index of connection

        - sh: att start handle
        - eh: att end handle
        - uuid: uuid that service need to find in 128bits

    返回
    :   - others: fail

<a id="_CPPv430bk_ble_discover_characteristic7uint8_t8uint16_t8uint16_t"></a>

<a id="_CPPv330bk_ble_discover_characteristic7uint8_t8uint16_t8uint16_t"></a> <a id="_CPPv230bk_ble_discover_characteristic7uint8_t8uint16_t8uint16_t"></a> <a id="bk_ble_discover_characteristic__uint8_t.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga114d6592e9c897955970d3f0d01d20f0"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_discover\_characteristic(uint8\_t conn\_id, uint16\_t sh, uint16\_t eh)
:   Discover peer characteristic. The result is report in the callback registered through bk\_ble\_register\_app\_sdp\_common\_callback, and evt is MST\_TYPE\_DISCOVER\_CHAR\_RSP. When completed, callback will report MST\_TYPE\_DISCOVER\_COMPLETED with [ble\_descover\_complete\_inf](#structble__descover__complete__inf) and MST\_TYPE\_DISCOVER\_CHAR\_RSP.

    参数
    :   **\-** – conn\_id: the index of connection

        - sh: att start handle
        - eh: att end handle

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv438bk_ble_discover_characteristic_by_uuid7uint8_t8uint16_t8uint16_t8uint16_t"></a>

<a id="_CPPv338bk_ble_discover_characteristic_by_uuid7uint8_t8uint16_t8uint16_t8uint16_t"></a> <a id="_CPPv238bk_ble_discover_characteristic_by_uuid7uint8_t8uint16_t8uint16_t8uint16_t"></a> <a id="bk_ble_discover_characteristic_by_uuid__uint8_t.uint16_t.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga7b09af5e20509e41b42e467af475cd49"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_discover\_characteristic\_by\_uuid(uint8\_t conn\_id, uint16\_t sh, uint16\_t eh, uint16\_t uuid)
:   Discover peer characteristic. The result is report in the callback registered through bk\_ble\_register\_app\_sdp\_common\_callback, and evt is MST\_TYPE\_DISCOVER\_CHAR\_BY\_UUID\_RSP. When completed, callback will report MST\_TYPE\_DISCOVER\_COMPLETED with [ble\_descover\_complete\_inf](#structble__descover__complete__inf) and MST\_TYPE\_DISCOVER\_CHAR\_BY\_UUID\_RSP.

    参数
    :   **\-** – conn\_id: the index of connection

        - sh: att start handle
        - eh: att end handle

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv441bk_ble_discover_characteristic_by_128uuid7uint8_t8uint16_t8uint16_tP7uint8_t"></a>

<a id="_CPPv341bk_ble_discover_characteristic_by_128uuid7uint8_t8uint16_t8uint16_tP7uint8_t"></a> <a id="_CPPv241bk_ble_discover_characteristic_by_128uuid7uint8_t8uint16_t8uint16_tP7uint8_t"></a> <a id="bk_ble_discover_characteristic_by_128uuid__uint8_t.uint16_t.uint16_t.uint8_tP"></a> <a id="group__bk__ble__api__v1_1ga1416ce651a3eb33f5f711facf79deac6"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_discover\_characteristic\_by\_128uuid(uint8\_t conn\_id, uint16\_t sh, uint16\_t eh, uint8\_t \*uuid)
:   Discover peer characteristic. The result is report in the callback registered through bk\_ble\_register\_app\_sdp\_common\_callback, and evt is MST\_TYPE\_DISCOVER\_CHAR\_BY\_128\_UUID\_RSP. When completed, callback will report MST\_TYPE\_DISCOVER\_COMPLETED with [ble\_descover\_complete\_inf](#structble__descover__complete__inf) and MST\_TYPE\_DISCOVER\_CHAR\_BY\_128\_UUID\_RSP.

    参数
    :   **\-** – conn\_id: the index of connection

        - sh: att start handle
        - eh: att end handle

    返回
    :   - others: fail

<a id="_CPPv441bk_ble_discover_characteristic_descriptor7uint8_t8uint16_t8uint16_t"></a>

<a id="_CPPv341bk_ble_discover_characteristic_descriptor7uint8_t8uint16_t8uint16_t"></a> <a id="_CPPv241bk_ble_discover_characteristic_descriptor7uint8_t8uint16_t8uint16_t"></a> <a id="bk_ble_discover_characteristic_descriptor__uint8_t.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga70cb2d7506fbf5dc80bbdb66bfdd0919"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_discover\_characteristic\_descriptor(uint8\_t conn\_id, uint16\_t sh, uint16\_t eh)
:   Discover peer characteristic descriptor. The result is report in the callback registered through bk\_ble\_register\_app\_sdp\_common\_callback, and evt is MST\_TYPE\_DISCOVER\_CHAR\_DESC. When completed, callback will report MST\_TYPE\_DISCOVER\_COMPLETED with [ble\_descover\_complete\_inf](#structble__descover__complete__inf) and MST\_TYPE\_DISCOVER\_CHAR\_DESC.

    参数
    :   **\-** – conn\_id: the index of connection

        - sh: att start handle
        - eh: att end handle

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv417bk_ble_gattc_read7uint8_t8uint16_t8uint16_t"></a>

<a id="_CPPv317bk_ble_gattc_read7uint8_t8uint16_t8uint16_t"></a> <a id="_CPPv217bk_ble_gattc_read7uint8_t8uint16_t8uint16_t"></a> <a id="bk_ble_gattc_read__uint8_t.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga59559466bbfdc422e1dc9d1a767f8bad"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_read(uint8\_t con\_idx, uint16\_t att\_handle, uint16\_t offset)
:   As master, read attribute value, the result is reported in the callback registered through bk\_ble\_register\_app\_sdp\_charac\_callback.

    参数
    :   **\-** – con\_idx: the index of connection

        - att\_handle: the handle of attribute value
        - offset: the offset of attribute value

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv425bk_ble_gattc_read_by_uuid7uint8_t8uint16_t8uint16_tP7uint8_t7uint8_t"></a>

<a id="_CPPv325bk_ble_gattc_read_by_uuid7uint8_t8uint16_t8uint16_tP7uint8_t7uint8_t"></a> <a id="_CPPv225bk_ble_gattc_read_by_uuid7uint8_t8uint16_t8uint16_tP7uint8_t7uint8_t"></a> <a id="bk_ble_gattc_read_by_uuid__uint8_t.uint16_t.uint16_t.uint8_tP.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga9cd028a6be13887d30b44d507e70ccf9"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_read\_by\_uuid(uint8\_t conn\_id, uint16\_t sh, uint16\_t eh, uint8\_t \*uuid, uint8\_t uuid\_len)
:   As master, read attribute value, the result is reported in the callback registered through bk\_ble\_register\_app\_sdp\_charac\_callback.

    参数
    :   **\-** – con\_idx: the index of connection

        - sh: the start handle of attribute
        - eh: the end handle of attribute
        - uuid: uuid
        - uuid\_len: uuid len, may be 2 or 16

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv418bk_ble_gattc_write7uint8_t8uint16_tP7uint8_t8uint16_t7uint8_t"></a>

<a id="_CPPv318bk_ble_gattc_write7uint8_t8uint16_tP7uint8_t8uint16_t7uint8_t"></a> <a id="_CPPv218bk_ble_gattc_write7uint8_t8uint16_tP7uint8_t8uint16_t7uint8_t"></a> <a id="bk_ble_gattc_write__uint8_t.uint16_t.uint8_tP.uint16_t.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga717111fc7918c6d76dda6122a15d76eb"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_gattc\_write(uint8\_t con\_idx, uint16\_t att\_handle, uint8\_t \*data, uint16\_t len, uint8\_t is\_write\_cmd)
:   As master, write attribute value.

    参数
    :   **\-** – con\_idx: the index of connection

        - att\_handle: the handle of attribute value
        - data: value data
        - len: the length of attribute value
        - is\_write\_cmd: when true, will trigger write cmd, otherwise write req.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv423bk_ble_clear_white_listv"></a>

<a id="_CPPv323bk_ble_clear_white_listv"></a> <a id="_CPPv223bk_ble_clear_white_listv"></a> <a id="bk_ble_clear_white_list__void"></a> <a id="group__bk__ble__api__v1_1ga2a023a365afa7b2ad3eb5818540ad18e"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_clear\_white\_list(void)
:   clear the white list.

    Param

<a id="_CPPv432bk_ble_add_devices_to_while_listP9bd_addr_t7uint8_t"></a>

<a id="_CPPv332bk_ble_add_devices_to_while_listP9bd_addr_t7uint8_t"></a> <a id="_CPPv232bk_ble_add_devices_to_while_listP9bd_addr_t7uint8_t"></a> <a id="bk_ble_add_devices_to_while_list__bd_addr_tP.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga97257f56c5410ec86f49bb1d521301d1"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_add\_devices\_to\_while\_list([bd\_addr\_t](#_CPPv49bd_addr_t "bd_addr_t") \*addr, uint8\_t addr\_type)
:   Add a device to the while list.

    参数
    :   **\-** – addr: the address of the device.

        - addr\_type: the type of the address, 0 is public address, 1 is random address.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv437bk_ble_remove_devices_from_while_listP9bd_addr_t7uint8_t"></a>

<a id="_CPPv337bk_ble_remove_devices_from_while_listP9bd_addr_t7uint8_t"></a> <a id="_CPPv237bk_ble_remove_devices_from_while_listP9bd_addr_t7uint8_t"></a> <a id="bk_ble_remove_devices_from_while_list__bd_addr_tP.uint8_t"></a> <a id="group__bk__ble__api__v1_1gaad8714efc7d2602444a7fc1edbb8d08e"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_remove\_devices\_from\_while\_list([bd\_addr\_t](#_CPPv49bd_addr_t "bd_addr_t") \*addr, uint8\_t addr\_type)
:   Remove a device from the while list.

    参数
    :   **\-** – addr: the address of the device.

        - addr\_type: the type of the address, 0 is public address, 1 is random address.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv419bk_ble_tx_power_setf"></a>

<a id="_CPPv319bk_ble_tx_power_setf"></a> <a id="_CPPv219bk_ble_tx_power_setf"></a> <a id="bk_ble_tx_power_set__float"></a> <a id="group__bk__ble__api__v1_1ga7850470669532c678d020d005b6fe56e"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_tx\_power\_set(float pwr\_gain)
:   Set tx power.

    参数
    :   **\-** – pwr\_gain: tx power gain

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv420bk_ble_oob_req_reply7uint8_t7uint8_tP7uint8_t7uint8_t"></a>

<a id="_CPPv320bk_ble_oob_req_reply7uint8_t7uint8_tP7uint8_t7uint8_t"></a> <a id="_CPPv220bk_ble_oob_req_reply7uint8_t7uint8_tP7uint8_t7uint8_t"></a> <a id="bk_ble_oob_req_reply__uint8_t.uint8_t.uint8_tP.uint8_t"></a> <a id="group__bk__ble__api__v1_1ga50fc5027dd4dd4ace7f492fe0acaaee8"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_oob\_req\_reply(uint8\_t con\_idx, uint8\_t accept, uint8\_t \*tk, uint8\_t len)
:   Provide the Legacy-OOB Temporary Key for SMP, in response to BLE\_5\_OOB\_REQ\_EVENT (LE legacy pairing OOB; usable by both master and slave)

    **Attention**
    :   Applies to whichever role received the request. When accept is true, tk must be a 128-bit (GAP\_KEY\_LEN) random number; accept\=false rejects the pairing.

    参数
    :   **\-** – con\_idx: the index of connection

        - accept: Accept or Reject the OOB
        - tk: Temporary Key value, the TK value shall be a 128-bit random number
        - len: length of temporary key, should always be 128-bit

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv423bk_ble_sc_oob_req_reply7uint8_t7uint8_tAL16E_7uint8_tAL16E_7uint8_t"></a>

<a id="_CPPv323bk_ble_sc_oob_req_reply7uint8_t7uint8_tAL16E_7uint8_tAL16E_7uint8_t"></a> <a id="_CPPv223bk_ble_sc_oob_req_reply7uint8_t7uint8_tA16_7uint8_tA16_7uint8_t"></a> <a id="bk_ble_sc_oob_req_reply__uint8_t.uint8_t.uint8_tA.uint8_tA"></a> <a id="group__bk__ble__api__v1_1ga12be0cf4be5eb91818989e33e60e6199"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_sc\_oob\_req\_reply(uint8\_t con\_idx, uint8\_t accept, uint8\_t conf\[16\], uint8\_t rand\[16\])
:   Provide the LE Secure Connections OOB data (conf/rand) for SMP, in response to BLE\_5\_SC\_OOB\_REQ\_EVENT (LE Secure Connections OOB; usable by both master and slave)

    **Attention**
    :   Applies to whichever role received the request. The local OOB conf/rand to be transferred to the peer are delivered earlier via the BLE\_5\_SC\_LOC\_OOB\_IND event. accept\=false rejects the pairing.

    参数
    :   **\-** – con\_idx: the index of connection

        - accept: Accept or Reject the OOB
        - conf: Confirmation value, it shall be a 128-bit random number
        - rand: Randomizer value, it should be a 128-bit random number

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv414bk_ble_coc_reg8uint16_t"></a>

<a id="_CPPv314bk_ble_coc_reg8uint16_t"></a> <a id="_CPPv214bk_ble_coc_reg8uint16_t"></a> <a id="bk_ble_coc_reg__uint16_t"></a> <a id="group__bk__ble__api__v1_1gae917eee83e271d6375cfdb71c0ba1a5d"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_coc\_reg(uint16\_t psm)
:   Register a Protocol/Service Multiplexer (PSM) for BLE COC.

    Registers a PSM value to enable BLE Connection Oriented Channel (COC) services. PSM is used to identify different services or protocols over a single BLE connection.

    参数
    :   **\-** – psm: Protocol/Service Multiplexer value to register

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv416bk_ble_coc_unreg8uint16_t"></a>

<a id="_CPPv316bk_ble_coc_unreg8uint16_t"></a> <a id="_CPPv216bk_ble_coc_unreg8uint16_t"></a> <a id="bk_ble_coc_unreg__uint16_t"></a> <a id="group__bk__ble__api__v1_1gaaf64a6b615a70589a0c3c86263bc2abe"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_coc\_unreg(uint16\_t psm)
:   Unregister a Protocol/Service Multiplexer (PSM) for BLE COC.

    Unregisters a previously registered PSM value, disabling the associated COC service. All active connections on this PSM should be closed before unregistering.

    参数
    :   **\-** – psm: Protocol/Service Multiplexer value to unregister

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv417bk_ble_coc_config8uint16_t7uint8_t"></a>

<a id="_CPPv317bk_ble_coc_config8uint16_t7uint8_t"></a> <a id="_CPPv217bk_ble_coc_config8uint16_t7uint8_t"></a> <a id="bk_ble_coc_config__uint16_t.uint8_t"></a> <a id="group__bk__ble__api__v1_1gaa6ea432af0aebd14ff87299224998f78"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_coc\_config(uint16\_t psm, uint8\_t sec\_lvl)
:   config the security level of a BLE COC channel

    Configures the security level required for a previously registered PSM. Incoming/outgoing connections on this PSM must satisfy the configured security level before the channel can be established.

    参数
    :   **\-** – psm: Protocol/Service Multiplexer value to configure

        - sec\_lvl: required security level, of type enum coc\_security:

          - BK\_BLE\_COC\_SEC\_NONE: no security
          - BK\_BLE\_COC\_SEC\_UNAUTH\_ENCRYPT: unauthenticated encryption
          - BK\_BLE\_COC\_SEC\_AUTH\_ENCRYPT: authenticated encryption
          - BK\_BLE\_COC\_SEC\_SECURE\_CONNECTION: LE Secure Connections

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv427bk_ble_coc_get_current_info7uint8_t8uint16_t7uint8_tP8uint32_t"></a>

<a id="_CPPv327bk_ble_coc_get_current_info7uint8_t8uint16_t7uint8_tP8uint32_t"></a> <a id="_CPPv227bk_ble_coc_get_current_info7uint8_t8uint16_t7uint8_tP8uint32_t"></a> <a id="bk_ble_coc_get_current_info__uint8_t.uint16_t.uint8_t.uint32_tP"></a> <a id="group__bk__ble__api__v1_1ga76a6914163e03be37e34be115d51d7fa"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_coc\_get\_current\_info(uint8\_t conn\_idx, uint16\_t cid, uint8\_t type, uint32\_t \*output)
:   Get current information of a BLE COC channel.

    Retrieves the current information of a Connection Oriented Channel (COC) based on the specified information type. This function can be used to query various channel parameters such as current credits, maximum credits, MTU, MPS, etc.

    备注

    - The function must be called after the COC channel is established
    - The output parameter must point to a valid memory location
    - The meaning of the output value depends on the type parameter

    参数
    :   **\-** – conn\_idx: the index of BLE connection to the remote device

        - cid: Channel ID of the COC connection to query
        - type: Information type to retrieve, of type enum coc\_info. Possible values:

          - BK\_BLE\_COC\_PEER\_CURRENT\_CREDIT: Peer’s current available credits
          - BK\_BLE\_COC\_PEER\_MAX\_CREDIT: Peer’s maximum credits
          - BK\_BLE\_COC\_PEER\_MTU: Peer’s Maximum Transmission Unit size
          - BK\_BLE\_COC\_PEER\_MPS: Peer’s Maximum PDU Payload Size
          - BK\_BLE\_COC\_LOCAL\_CURRENT\_CREDIT: Local current available credits
          - BK\_BLE\_COC\_LOCAL\_MAX\_CREDIT: Local maximum credits
          - BK\_BLE\_COC\_LOCAL\_MTU: Local Maximum Transmission Unit size
          - BK\_BLE\_COC\_LOCAL\_MPS: Local Maximum PDU Payload Size
        - output: Pointer to a uint32\_t variable to store the retrieved information. The value will be written to this location upon successful retrieval. Must not be NULL.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed, information retrieved and stored in output
        - BK\_ERR\_BLE\_FAIL: fail, invalid parameters or channel not found
        - BK\_ERR\_BLE\_UNKNOW\_IDX: invalid connection index or channel ID
        - others: fail

<a id="_CPPv425bk_ble_coc_connection_req7uint8_t8uint16_t8uint16_t8uint16_t8uint16_t"></a>

<a id="_CPPv325bk_ble_coc_connection_req7uint8_t8uint16_t8uint16_t8uint16_t8uint16_t"></a> <a id="_CPPv225bk_ble_coc_connection_req7uint8_t8uint16_t8uint16_t8uint16_t8uint16_t"></a> <a id="bk_ble_coc_connection_req__uint8_t.uint16_t.uint16_t.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga2e28f6d7e3a339db9cbe63e988b496e0"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_coc\_connection\_req(uint8\_t conn\_idx, uint16\_t psm, uint16\_t mtu, uint16\_t mps, uint16\_t credit)
:   Request to establish a BLE COC connection.

    Initiates a connection request to establish a Connection Oriented Channel with a remote device on the specified connection using the given PSM.

    **Attention**
    :   the connection result is reported in ble\_notice\_cb\_t as BLE\_5\_COC\_CONNECTION\_COMPL\_EVENT

    参数
    :   **\-** – conn\_idx: the index of BLE connection to the remote device

        - psm: Protocol/Service Multiplexer value to connect to
        - mtu: max transmision unit size, use default value if 0
        - mps: max pdu payload size, use default value if 0
        - credit: init credit, use default value if 0

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv428bk_ble_coc_disconnection_req7uint8_t8uint16_t"></a>

<a id="_CPPv328bk_ble_coc_disconnection_req7uint8_t8uint16_t"></a> <a id="_CPPv228bk_ble_coc_disconnection_req7uint8_t8uint16_t"></a> <a id="bk_ble_coc_disconnection_req__uint8_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1ga9f250dd17d2cc3ff8c956b1b1afadb36"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_coc\_disconnection\_req(uint8\_t conn\_idx, uint16\_t cid)
:   Request to disconnect a BLE COC channel.

    Initiates a disconnection request to close an established Connection Oriented Channel identified by the channel ID.

    **Attention**
    :   the disconnection result is reported in ble\_notice\_cb\_t as BLE\_5\_COC\_DISCCONNECT\_COMPL\_EVENT

    参数
    :   **\-** – conn\_idx: the index of BLE connection

        - cid: Channel ID of the COC connection to disconnect

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv429bk_ble_coc_accept_connect_req7uint8_t7uint8_t8uint16_t8uint16_t8uint16_t8uint16_t"></a>

<a id="_CPPv329bk_ble_coc_accept_connect_req7uint8_t7uint8_t8uint16_t8uint16_t8uint16_t8uint16_t"></a> <a id="_CPPv229bk_ble_coc_accept_connect_req7uint8_t7uint8_t8uint16_t8uint16_t8uint16_t8uint16_t"></a> <a id="bk_ble_coc_accept_connect_req__uint8_t.uint8_t.uint16_t.uint16_t.uint16_t.uint16_t"></a> <a id="group__bk__ble__api__v1_1gae88a19d316727e59989b2b3e80e99981"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_coc\_accept\_connect\_req(uint8\_t conn\_idx, uint8\_t accept, uint16\_t peer\_cid, uint16\_t mtu, uint16\_t mps, uint16\_t credit)
:   Accept or reject a BLE COC connection request from a peer device.

    Responds to an incoming Connection Oriented Channel (COC) connection request from a remote device. This function is typically called by the server side after receiving a connection request event. It allows the application to accept or reject the connection and specify the channel parameters.

    备注

    - This function should be called in response to a COC connection request event (BLE\_5\_COC\_CONNECT\_REQ\_EVENT); the result is reported as BLE\_5\_COC\_CONNECTION\_COMPL\_EVENT
    - If accept is 0, the connection will be rejected and mtu/mps/credit parameters are ignored
    - If accept is non-zero, the connection will be accepted with the specified parameters
    - The actual MTU and MPS used will be the minimum of local and peer values after negotiation
    - The function must be called before the connection request timeout expires

    参数
    :   **\-** – conn\_idx: the index of BLE connection to the remote device

        - accept: Flag to accept or reject the connection request.

          - 0: Reject the connection request
          - 1 (non-zero): Accept the connection request
        - peer\_cid: Peer’s Channel ID from the connection request event
        - mtu: Maximum Transmission Unit size for the channel. Use default value if 0\. This value will be negotiated with the peer.
        - mps: Maximum PDU Payload Size for the channel. Use default value if 0\. This value will be negotiated with the peer.
        - credit: Initial credit value for the channel. Use default value if 0\. Credits are used for flow control.

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed, connection request accepted or rejected
        - BK\_ERR\_BLE\_FAIL: fail, invalid parameters or connection request not found
        - BK\_ERR\_BLE\_UNKNOW\_IDX: invalid connection index or peer channel ID
        - others: fail

<a id="_CPPv419bk_ble_coc_send_req7uint8_t8uint16_tP7uint8_t8uint32_t"></a>

<a id="_CPPv319bk_ble_coc_send_req7uint8_t8uint16_tP7uint8_t8uint32_t"></a> <a id="_CPPv219bk_ble_coc_send_req7uint8_t8uint16_tP7uint8_t8uint32_t"></a> <a id="bk_ble_coc_send_req__uint8_t.uint16_t.uint8_tP.uint32_t"></a> <a id="group__bk__ble__api__v1_1gac2d72917dadeb0e3f7b620f4d8c6b519"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_coc\_send\_req(uint8\_t conn\_idx, uint16\_t cid, uint8\_t \*data, uint32\_t len)
:   Send data over a BLE COC channel.

    Transmits data through an established Connection Oriented Channel. The data will be sent to the remote device on the specified channel.

    **Attention**
    :   the transmission completion is reported in ble\_notice\_cb\_t as BLE\_5\_COC\_TX\_DONE

    参数
    :   **\-** – conn\_idx: the index of BLE connection

        - cid: Channel ID of the COC connection
        - data: Pointer to the data buffer to send
        - len: Length of data to send in bytes

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: fail

<a id="_CPPv433bk_ble_host_register_hci_callback16ble_hci_to_cp_cb"></a>

<a id="_CPPv333bk_ble_host_register_hci_callback16ble_hci_to_cp_cb"></a> <a id="_CPPv233bk_ble_host_register_hci_callback16ble_hci_to_cp_cb"></a> <a id="bk_ble_host_register_hci_callback__ble_hci_to_cp_cb"></a> <a id="group__bk__ble__api__v1_1ga542053a5dba682d2b25f8a8d92358bb7"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") bk\_ble\_host\_register\_hci\_callback([ble\_hci\_to\_cp\_cb](#_CPPv416ble_hci_to_cp_cb "ble_hci_to_cp_cb") cb)
:   register hci callback for host only

    **Attention**
    :   used for host only

    参数
    :   **\-** – cb: hci callback function used to recv hci data from host

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed
        - others: other errors.

<a id="_CPPv423bk_ble_hci_send_to_hostP7uint8_t8uint32_t"></a>

<a id="_CPPv323bk_ble_hci_send_to_hostP7uint8_t8uint32_t"></a> <a id="_CPPv223bk_ble_hci_send_to_hostP7uint8_t8uint32_t"></a> <a id="bk_ble_hci_send_to_host__uint8_tP.uint32_t"></a> <a id="group__bk__ble__api__v1_1ga9ea910e33bae552917d662eb3dd3f964"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_ble\_hci\_send\_to\_host(uint8\_t \*buf, uint32\_t len)
:   send hci data to host.

    **Attention**
    :   used for host only

    参数
    :   **\-** – buf: payload

        - len: buf’s len

    返回
    :   - BK\_ERR\_BLE\_SUCCESS: succeed

<a id="id5"></a>

## API 类型定义

<a id="bk-ble-types-h"></a>

## bk\_ble\_types.h

`bk_ble_types.h` 定义传统 BLE API 使用的配置、事件和数据类型。

<a id="id6"></a>

### Header File

- [bk\_ble\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/bluetooth/bk_ble_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv415ble_sdp_svc_ind"></a>

<a id="_CPPv315ble_sdp_svc_ind"></a> <a id="_CPPv215ble_sdp_svc_ind"></a> <a id="ble_sdp_svc_ind"></a> <a id="structble__sdp__svc__ind"></a> struct ble\_sdp\_svc\_ind
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15ble_sdp_svc_ind8uuid_lenE"></a>

    <a id="_CPPv3N15ble_sdp_svc_ind8uuid_lenE"></a> <a id="_CPPv2N15ble_sdp_svc_ind8uuid_lenE"></a> <a id="ble_sdp_svc_ind::uuid_len__uint8_t"></a> <a id="structble__sdp__svc__ind_1a6f9ace123d16e90645e16cdaa59f045b"></a> uint8\_t uuid\_len
    :   Service UUID Length.

    <a id="_CPPv4N15ble_sdp_svc_ind4uuidE"></a>

    <a id="_CPPv3N15ble_sdp_svc_ind4uuidE"></a> <a id="_CPPv2N15ble_sdp_svc_ind4uuidE"></a> <a id="ble_sdp_svc_ind::uuid__uint8_tA"></a> <a id="structble__sdp__svc__ind_1ab1cdd5bb5d4c48c2dc38d350befae802"></a> uint8\_t uuid\[16\]
    :   Service UUID.

    <a id="_CPPv4N15ble_sdp_svc_ind9start_hdlE"></a>

    <a id="_CPPv3N15ble_sdp_svc_ind9start_hdlE"></a> <a id="_CPPv2N15ble_sdp_svc_ind9start_hdlE"></a> <a id="ble_sdp_svc_ind::start_hdl__uint16_t"></a> <a id="structble__sdp__svc__ind_1ada0877057c70c911000207c351676a59"></a> uint16\_t start\_hdl
    :   Service start handle.

    <a id="_CPPv4N15ble_sdp_svc_ind7end_hdlE"></a>

    <a id="_CPPv3N15ble_sdp_svc_ind7end_hdlE"></a> <a id="_CPPv2N15ble_sdp_svc_ind7end_hdlE"></a> <a id="ble_sdp_svc_ind::end_hdl__uint16_t"></a> <a id="structble__sdp__svc__ind_1a36c26bdc2e02da1bdbe9f5c517bf7b5d"></a> uint16\_t end\_hdl
    :   Service end handle.

<a id="_CPPv416ble_sdp_char_inf"></a>

<a id="_CPPv316ble_sdp_char_inf"></a> <a id="_CPPv216ble_sdp_char_inf"></a> <a id="ble_sdp_char_inf"></a> <a id="structble__sdp__char__inf"></a> struct ble\_sdp\_char\_inf
:   characteristic info

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16ble_sdp_char_inf8uuid_lenE"></a>

    <a id="_CPPv3N16ble_sdp_char_inf8uuid_lenE"></a> <a id="_CPPv2N16ble_sdp_char_inf8uuid_lenE"></a> <a id="ble_sdp_char_inf::uuid_len__uint8_t"></a> <a id="structble__sdp__char__inf_1a84583b32f7d117f521693d09f5e4e2a9"></a> uint8\_t uuid\_len
    :   Characteristic UUID Length.

    <a id="_CPPv4N16ble_sdp_char_inf4uuidE"></a>

    <a id="_CPPv3N16ble_sdp_char_inf4uuidE"></a> <a id="_CPPv2N16ble_sdp_char_inf4uuidE"></a> <a id="ble_sdp_char_inf::uuid__uint8_tA"></a> <a id="structble__sdp__char__inf_1a2d63ce72eb25d98f28debd417d2b518e"></a> uint8\_t uuid\[16\]
    :   Characteristic UUID.

    <a id="_CPPv4N16ble_sdp_char_inf8char_hdlE"></a>

    <a id="_CPPv3N16ble_sdp_char_inf8char_hdlE"></a> <a id="_CPPv2N16ble_sdp_char_inf8char_hdlE"></a> <a id="ble_sdp_char_inf::char_hdl__uint16_t"></a> <a id="structble__sdp__char__inf_1a74a26115d03737d4307b254f35e44c18"></a> uint16\_t char\_hdl
    :   Characteristic handle.

    <a id="_CPPv4N16ble_sdp_char_inf7val_hdlE"></a>

    <a id="_CPPv3N16ble_sdp_char_inf7val_hdlE"></a> <a id="_CPPv2N16ble_sdp_char_inf7val_hdlE"></a> <a id="ble_sdp_char_inf::val_hdl__uint16_t"></a> <a id="structble__sdp__char__inf_1a4b6e93dbc8da6b65512da75d7729b37d"></a> uint16\_t val\_hdl
    :   Value handle.

    <a id="_CPPv4N16ble_sdp_char_inf4propE"></a>

    <a id="_CPPv3N16ble_sdp_char_inf4propE"></a> <a id="_CPPv2N16ble_sdp_char_inf4propE"></a> <a id="ble_sdp_char_inf::prop__uint8_t"></a> <a id="structble__sdp__char__inf_1a5dea06aef1aa6fe99d10c7acd4671732"></a> uint8\_t prop
    :   Characteristic properties.

    <a id="_CPPv4N16ble_sdp_char_inf13char_ehdl_offE"></a>

    <a id="_CPPv3N16ble_sdp_char_inf13char_ehdl_offE"></a> <a id="_CPPv2N16ble_sdp_char_inf13char_ehdl_offE"></a> <a id="ble_sdp_char_inf::char_ehdl_off__uint8_t"></a> <a id="structble__sdp__char__inf_1a294bd833aed072d81770df134a38d58b"></a> uint8\_t char\_ehdl\_off
    :   End of characteristic offset.

<a id="_CPPv421ble_sdp_char_desc_inf"></a>

<a id="_CPPv321ble_sdp_char_desc_inf"></a> <a id="_CPPv221ble_sdp_char_desc_inf"></a> <a id="ble_sdp_char_desc_inf"></a> <a id="structble__sdp__char__desc__inf"></a> struct ble\_sdp\_char\_desc\_inf
:   characteristic description

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21ble_sdp_char_desc_inf8uuid_lenE"></a>

    <a id="_CPPv3N21ble_sdp_char_desc_inf8uuid_lenE"></a> <a id="_CPPv2N21ble_sdp_char_desc_inf8uuid_lenE"></a> <a id="ble_sdp_char_desc_inf::uuid_len__uint8_t"></a> <a id="structble__sdp__char__desc__inf_1a8802e4441451c97fa67e26bdbdde7c2a"></a> uint8\_t uuid\_len
    :   UUID length.

    <a id="_CPPv4N21ble_sdp_char_desc_inf4uuidE"></a>

    <a id="_CPPv3N21ble_sdp_char_desc_inf4uuidE"></a> <a id="_CPPv2N21ble_sdp_char_desc_inf4uuidE"></a> <a id="ble_sdp_char_desc_inf::uuid__uint8_tA"></a> <a id="structble__sdp__char__desc__inf_1a3b3080c1d0ca69b20bb938b3cedb941e"></a> uint8\_t uuid\[16\]
    :   UUID.

    <a id="_CPPv4N21ble_sdp_char_desc_inf8desc_hdlE"></a>

    <a id="_CPPv3N21ble_sdp_char_desc_inf8desc_hdlE"></a> <a id="_CPPv2N21ble_sdp_char_desc_inf8desc_hdlE"></a> <a id="ble_sdp_char_desc_inf::desc_hdl__uint16_t"></a> <a id="structble__sdp__char__desc__inf_1a7cd69cc67ad4a2fb03eadb773e0225de"></a> uint16\_t desc\_hdl
    :   Descriptor handle.

<a id="_CPPv425ble_descover_complete_inf"></a>

<a id="_CPPv325ble_descover_complete_inf"></a> <a id="_CPPv225ble_descover_complete_inf"></a> <a id="ble_descover_complete_inf"></a> <a id="structble__descover__complete__inf"></a> struct ble\_descover\_complete\_inf
:   discover completed evt param, see MST\_TYPE\_DISCOVER\_COMPLETED

<a id="_CPPv413ble_smp_ind_t"></a>

<a id="_CPPv313ble_smp_ind_t"></a> <a id="_CPPv213ble_smp_ind_t"></a> <a id="ble_smp_ind_t"></a> <a id="structble__smp__ind__t"></a> struct ble\_smp\_ind\_t

<a id="_CPPv417ble_attc_wr_rd_op"></a>

<a id="_CPPv317ble_attc_wr_rd_op"></a> <a id="_CPPv217ble_attc_wr_rd_op"></a> <a id="ble_attc_wr_rd_op"></a> <a id="structble__attc__wr__rd__op"></a> struct ble\_attc\_wr\_rd\_op
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17ble_attc_wr_rd_op6statusE"></a>

    <a id="_CPPv3N17ble_attc_wr_rd_op6statusE"></a> <a id="_CPPv2N17ble_attc_wr_rd_op6statusE"></a> <a id="ble_attc_wr_rd_op::status__uint8_t"></a> <a id="structble__attc__wr__rd__op_1a503a2240092b3dfcc81063faa63df0d0"></a> uint8\_t status
    :   Status of the request.

    <a id="_CPPv4N17ble_attc_wr_rd_op7seq_numE"></a>

    <a id="_CPPv3N17ble_attc_wr_rd_op7seq_numE"></a> <a id="_CPPv2N17ble_attc_wr_rd_op7seq_numE"></a> <a id="ble_attc_wr_rd_op::seq_num__uint16_t"></a> <a id="structble__attc__wr__rd__op_1a260b547697f5add39cfab2dd63de66b4"></a> uint16\_t seq\_num
    :   operation sequence number \- provided when operation is started

<a id="_CPPv418ble_attc_event_ind"></a>

<a id="_CPPv318ble_attc_event_ind"></a> <a id="_CPPv218ble_attc_event_ind"></a> <a id="ble_attc_event_ind"></a> <a id="structble__attc__event__ind"></a> struct ble\_attc\_event\_ind
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18ble_attc_event_ind4typeE"></a>

    <a id="_CPPv3N18ble_attc_event_ind4typeE"></a> <a id="_CPPv2N18ble_attc_event_ind4typeE"></a> <a id="ble_attc_event_ind::type__msg_attc"></a> <a id="structble__attc__event__ind_1ac2579853c8097a9951057055a30242d9"></a> enum [msg\_attc](#_CPPv48msg_attc "msg_attc") type
    :   Event Type.

    <a id="_CPPv4N18ble_attc_event_ind9start_hdlE"></a>

    <a id="_CPPv3N18ble_attc_event_ind9start_hdlE"></a> <a id="_CPPv2N18ble_attc_event_ind9start_hdlE"></a> <a id="ble_attc_event_ind::start_hdl__uint16_t"></a> <a id="structble__attc__event__ind_1a75f263f209f7c64bbbe81b2e88aa560d"></a> uint16\_t start\_hdl
    :   if start\_hdl \= end\_hdl \= 0,it is invaild

<a id="_CPPv415ble_cmd_param_t"></a>

<a id="_CPPv315ble_cmd_param_t"></a> <a id="_CPPv215ble_cmd_param_t"></a> <a id="ble_cmd_param_t"></a> <a id="structble__cmd__param__t"></a> struct ble\_cmd\_param\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15ble_cmd_param_t7cmd_idxE"></a>

    <a id="_CPPv3N15ble_cmd_param_t7cmd_idxE"></a> <a id="_CPPv2N15ble_cmd_param_t7cmd_idxE"></a> <a id="ble_cmd_param_t::cmd_idx__uint8_t"></a> <a id="structble__cmd__param__t_1ae740a8e25fad23170b2e6cda2e17552a"></a> uint8\_t cmd\_idx
    :   actv\_idx

    <a id="_CPPv4N15ble_cmd_param_t6statusE"></a>

    <a id="_CPPv3N15ble_cmd_param_t6statusE"></a> <a id="_CPPv2N15ble_cmd_param_t6statusE"></a> <a id="ble_cmd_param_t::status__ble_err_t"></a> <a id="structble__cmd__param__t_1aa36c3b32869b750ee7b34364337b9a16"></a> [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") status
    :   The status for this command

<a id="_CPPv418ble_att_info_req_t"></a>

<a id="_CPPv318ble_att_info_req_t"></a> <a id="_CPPv218ble_att_info_req_t"></a> <a id="ble_att_info_req_t"></a> <a id="structble__att__info__req__t"></a> struct ble\_att\_info\_req\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18ble_att_info_req_t8conn_idxE"></a>

    <a id="_CPPv3N18ble_att_info_req_t8conn_idxE"></a> <a id="_CPPv2N18ble_att_info_req_t8conn_idxE"></a> <a id="ble_att_info_req_t::conn_idx__uint8_t"></a> <a id="structble__att__info__req__t_1aad446a224db42be81b4d554c49ef9d59"></a> uint8\_t conn\_idx
    :   The index of the connection

    <a id="_CPPv4N18ble_att_info_req_t6prf_idE"></a>

    <a id="_CPPv3N18ble_att_info_req_t6prf_idE"></a> <a id="_CPPv2N18ble_att_info_req_t6prf_idE"></a> <a id="ble_att_info_req_t::prf_id__uint16_t"></a> <a id="structble__att__info__req__t_1a2220587285bcea14d8ad6cb118389939"></a> uint16\_t prf\_id
    :   The id of the profile

    <a id="_CPPv4N18ble_att_info_req_t7att_idxE"></a>

    <a id="_CPPv3N18ble_att_info_req_t7att_idxE"></a> <a id="_CPPv2N18ble_att_info_req_t7att_idxE"></a> <a id="ble_att_info_req_t::att_idx__uint16_t"></a> <a id="structble__att__info__req__t_1a4aef6fd992c708d8a1f8d9ca0ae8f620"></a> uint16\_t att\_idx
    :   The index of the attribute

    <a id="_CPPv4N18ble_att_info_req_t6lengthE"></a>

    <a id="_CPPv3N18ble_att_info_req_t6lengthE"></a> <a id="_CPPv2N18ble_att_info_req_t6lengthE"></a> <a id="ble_att_info_req_t::length__uint16_t"></a> <a id="structble__att__info__req__t_1addeea7b9d3a80bd0da33e01769984a88"></a> uint16\_t length
    :   The length of the attribute

    <a id="_CPPv4N18ble_att_info_req_t6statusE"></a>

    <a id="_CPPv3N18ble_att_info_req_t6statusE"></a> <a id="_CPPv2N18ble_att_info_req_t6statusE"></a> <a id="ble_att_info_req_t::status__uint8_t"></a> <a id="structble__att__info__req__t_1af2c1feb324e1b62d3496b38cddc16090"></a> uint8\_t status
    :   Use to know if it’s possible to modify the attribute ,can contains authorization or application error code

<a id="_CPPv415ble_write_req_t"></a>

<a id="_CPPv315ble_write_req_t"></a> <a id="_CPPv215ble_write_req_t"></a> <a id="ble_write_req_t"></a> <a id="structble__write__req__t"></a> struct ble\_write\_req\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15ble_write_req_t8conn_idxE"></a>

    <a id="_CPPv3N15ble_write_req_t8conn_idxE"></a> <a id="_CPPv2N15ble_write_req_t8conn_idxE"></a> <a id="ble_write_req_t::conn_idx__uint8_t"></a> <a id="structble__write__req__t_1a861f0a0a6b01edef93912d4bbd028dc8"></a> uint8\_t conn\_idx
    :   The index of the connection

    <a id="_CPPv4N15ble_write_req_t6prf_idE"></a>

    <a id="_CPPv3N15ble_write_req_t6prf_idE"></a> <a id="_CPPv2N15ble_write_req_t6prf_idE"></a> <a id="ble_write_req_t::prf_id__uint16_t"></a> <a id="structble__write__req__t_1ad6a43fae0f27bb7b7c782996dd55df79"></a> uint16\_t prf\_id
    :   The id of the profile

    <a id="_CPPv4N15ble_write_req_t7att_idxE"></a>

    <a id="_CPPv3N15ble_write_req_t7att_idxE"></a> <a id="_CPPv2N15ble_write_req_t7att_idxE"></a> <a id="ble_write_req_t::att_idx__uint16_t"></a> <a id="structble__write__req__t_1a8a2f44bb70fffa7c1201e40374c48729"></a> uint16\_t att\_idx
    :   The index of the attribute

    <a id="_CPPv4N15ble_write_req_t5valueE"></a>

    <a id="_CPPv3N15ble_write_req_t5valueE"></a> <a id="_CPPv2N15ble_write_req_t5valueE"></a> <a id="ble_write_req_t::value__uint8_tP"></a> <a id="structble__write__req__t_1a06235bf4af0dd453f712d93b6d6a599e"></a> uint8\_t \*value
    :   The attribute value

    <a id="_CPPv4N15ble_write_req_t3lenE"></a>

    <a id="_CPPv3N15ble_write_req_t3lenE"></a> <a id="_CPPv2N15ble_write_req_t3lenE"></a> <a id="ble_write_req_t::len__uint16_t"></a> <a id="structble__write__req__t_1a790cfbc5d85f6e21f465caa178e0bd90"></a> uint16\_t len
    :   The length of the attribute value

    <a id="_CPPv4N15ble_write_req_t6is_cmdE"></a>

    <a id="_CPPv3N15ble_write_req_t6is_cmdE"></a> <a id="_CPPv2N15ble_write_req_t6is_cmdE"></a> <a id="ble_write_req_t::is_cmd__uint8_t"></a> <a id="structble__write__req__t_1a3935f8e8d59e51753a134571e06f9ec0"></a> uint8\_t is\_cmd
    :   1: write command (no response); 0: write request (response expected)

<a id="_CPPv414ble_read_req_t"></a>

<a id="_CPPv314ble_read_req_t"></a> <a id="_CPPv214ble_read_req_t"></a> <a id="ble_read_req_t"></a> <a id="structble__read__req__t"></a> struct ble\_read\_req\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14ble_read_req_t8conn_idxE"></a>

    <a id="_CPPv3N14ble_read_req_t8conn_idxE"></a> <a id="_CPPv2N14ble_read_req_t8conn_idxE"></a> <a id="ble_read_req_t::conn_idx__uint8_t"></a> <a id="structble__read__req__t_1afd2730611ca865ba0e765151f93096f4"></a> uint8\_t conn\_idx
    :   The index of the connection

    <a id="_CPPv4N14ble_read_req_t6prf_idE"></a>

    <a id="_CPPv3N14ble_read_req_t6prf_idE"></a> <a id="_CPPv2N14ble_read_req_t6prf_idE"></a> <a id="ble_read_req_t::prf_id__uint16_t"></a> <a id="structble__read__req__t_1abbf2cf04db6dc60e709de501a943b037"></a> uint16\_t prf\_id
    :   The id of the profile

    <a id="_CPPv4N14ble_read_req_t7att_idxE"></a>

    <a id="_CPPv3N14ble_read_req_t7att_idxE"></a> <a id="_CPPv2N14ble_read_req_t7att_idxE"></a> <a id="ble_read_req_t::att_idx__uint16_t"></a> <a id="structble__read__req__t_1aa2ee1cd30db266822d352b51ee358c8f"></a> uint16\_t att\_idx
    :   The index of the attribute

    <a id="_CPPv4N14ble_read_req_t5valueE"></a>

    <a id="_CPPv3N14ble_read_req_t5valueE"></a> <a id="_CPPv2N14ble_read_req_t5valueE"></a> <a id="ble_read_req_t::value__uint8_tP"></a> <a id="structble__read__req__t_1a5528bdce8e953fe243aa6be2e5fcc26c"></a> uint8\_t \*value
    :   The attribute value

    <a id="_CPPv4N14ble_read_req_t4sizeE"></a>

    <a id="_CPPv3N14ble_read_req_t4sizeE"></a> <a id="_CPPv2N14ble_read_req_t4sizeE"></a> <a id="ble_read_req_t::size__uint16_t"></a> <a id="structble__read__req__t_1a8eeeb01cf9a26119cf84d6fd2dd12c45"></a> uint16\_t size
    :   The size of attribute value to read

    <a id="_CPPv4N14ble_read_req_t6lengthE"></a>

    <a id="_CPPv3N14ble_read_req_t6lengthE"></a> <a id="_CPPv2N14ble_read_req_t6lengthE"></a> <a id="ble_read_req_t::length__uint16_t"></a> <a id="structble__read__req__t_1a66f24478110858738158617e6fd864ba"></a> uint16\_t length
    :   The data length read

<a id="_CPPv414ble_recv_adv_t"></a>

<a id="_CPPv314ble_recv_adv_t"></a> <a id="_CPPv214ble_recv_adv_t"></a> <a id="ble_recv_adv_t"></a> <a id="structble__recv__adv__t"></a> struct ble\_recv\_adv\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14ble_recv_adv_t8actv_idxE"></a>

    <a id="_CPPv3N14ble_recv_adv_t8actv_idxE"></a> <a id="_CPPv2N14ble_recv_adv_t8actv_idxE"></a> <a id="ble_recv_adv_t::actv_idx__uint8_t"></a> <a id="structble__recv__adv__t_1abf28d3ae03f016f54ac3b1c649f7e959"></a> uint8\_t actv\_idx
    :   The index of the activity

    <a id="_CPPv4N14ble_recv_adv_t8evt_typeE"></a>

    <a id="_CPPv3N14ble_recv_adv_t8evt_typeE"></a> <a id="_CPPv2N14ble_recv_adv_t8evt_typeE"></a> <a id="ble_recv_adv_t::evt_type__uint8_t"></a> <a id="structble__recv__adv__t_1a47da49c1aa9a1073dc7627fa0d8a1968"></a> uint8\_t evt\_type
    :   Event type (see enum [adv\_report\_info](#group__bk__ble__api__v1__typedef_1ga8648555af760e5e51dcbd0829cb4dd16) and see enum [adv\_report\_type](#group__bk__ble__api__v1__typedef_1ga586827f2b8e2c17b183858febd25a205))

    <a id="_CPPv4N14ble_recv_adv_t13adv_addr_typeE"></a>

    <a id="_CPPv3N14ble_recv_adv_t13adv_addr_typeE"></a> <a id="_CPPv2N14ble_recv_adv_t13adv_addr_typeE"></a> <a id="ble_recv_adv_t::adv_addr_type__uint8_t"></a> <a id="structble__recv__adv__t_1aa9f900b13290663a3cb8c8fc7e127cff"></a> uint8\_t adv\_addr\_type
    :   Advertising address type: public/random

    <a id="_CPPv4N14ble_recv_adv_t8adv_addrE"></a>

    <a id="_CPPv3N14ble_recv_adv_t8adv_addrE"></a> <a id="_CPPv2N14ble_recv_adv_t8adv_addrE"></a> <a id="ble_recv_adv_t::adv_addr__uint8_tA"></a> <a id="structble__recv__adv__t_1ada1b929edd545a73837ec3e492034589"></a> uint8\_t adv\_addr\[6\]
    :   Advertising address value

    <a id="_CPPv4N14ble_recv_adv_t8data_lenE"></a>

    <a id="_CPPv3N14ble_recv_adv_t8data_lenE"></a> <a id="_CPPv2N14ble_recv_adv_t8data_lenE"></a> <a id="ble_recv_adv_t::data_len__uint8_t"></a> <a id="structble__recv__adv__t_1ad6f78528d3f14be445e36e322b2a1da0"></a> uint8\_t data\_len
    :   Data length in advertising packet

    <a id="_CPPv4N14ble_recv_adv_t4dataE"></a>

    <a id="_CPPv3N14ble_recv_adv_t4dataE"></a> <a id="_CPPv2N14ble_recv_adv_t4dataE"></a> <a id="ble_recv_adv_t::data__uint8_tP"></a> <a id="structble__recv__adv__t_1a649fcb58e3240174507cee3e269da8fd"></a> uint8\_t \*data
    :   Data of advertising packet

    <a id="_CPPv4N14ble_recv_adv_t4rssiE"></a>

    <a id="_CPPv3N14ble_recv_adv_t4rssiE"></a> <a id="_CPPv2N14ble_recv_adv_t4rssiE"></a> <a id="ble_recv_adv_t::rssi__int8_t"></a> <a id="structble__recv__adv__t_1a72cefcee1c6babb09efa37816ceb8c1c"></a> int8\_t rssi
    :   RSSI value for advertising packet (in dBm, between -127 and \+20 dBm)

<a id="_CPPv416ble_mtu_change_t"></a>

<a id="_CPPv316ble_mtu_change_t"></a> <a id="_CPPv216ble_mtu_change_t"></a> <a id="ble_mtu_change_t"></a> <a id="structble__mtu__change__t"></a> struct ble\_mtu\_change\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16ble_mtu_change_t8conn_idxE"></a>

    <a id="_CPPv3N16ble_mtu_change_t8conn_idxE"></a> <a id="_CPPv2N16ble_mtu_change_t8conn_idxE"></a> <a id="ble_mtu_change_t::conn_idx__uint8_t"></a> <a id="structble__mtu__change__t_1a90a0e12708869c47e85896788c7b40de"></a> uint8\_t conn\_idx
    :   The index of connection

    <a id="_CPPv4N16ble_mtu_change_t8mtu_sizeE"></a>

    <a id="_CPPv3N16ble_mtu_change_t8mtu_sizeE"></a> <a id="_CPPv2N16ble_mtu_change_t8mtu_sizeE"></a> <a id="ble_mtu_change_t::mtu_size__uint16_t"></a> <a id="structble__mtu__change__t_1a193ad9078c7dbf8c59f0c57180cf84d4"></a> uint16\_t mtu\_size
    :   The MTU size to exchange

<a id="_CPPv414ble_conn_ind_t"></a>

<a id="_CPPv314ble_conn_ind_t"></a> <a id="_CPPv214ble_conn_ind_t"></a> <a id="ble_conn_ind_t"></a> <a id="structble__conn__ind__t"></a> struct ble\_conn\_ind\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14ble_conn_ind_t8conn_idxE"></a>

    <a id="_CPPv3N14ble_conn_ind_t8conn_idxE"></a> <a id="_CPPv2N14ble_conn_ind_t8conn_idxE"></a> <a id="ble_conn_ind_t::conn_idx__uint8_t"></a> <a id="structble__conn__ind__t_1af4f295eb48b648b67d0443bfb3403620"></a> uint8\_t conn\_idx
    :   The index of connection.

    <a id="_CPPv4N14ble_conn_ind_t14peer_addr_typeE"></a>

    <a id="_CPPv3N14ble_conn_ind_t14peer_addr_typeE"></a> <a id="_CPPv2N14ble_conn_ind_t14peer_addr_typeE"></a> <a id="ble_conn_ind_t::peer_addr_type__uint8_t"></a> <a id="structble__conn__ind__t_1ad47dc6314a101f301cbe02bd8e148ad8"></a> uint8\_t peer\_addr\_type
    :   Peer address type.

    <a id="_CPPv4N14ble_conn_ind_t9peer_addrE"></a>

    <a id="_CPPv3N14ble_conn_ind_t9peer_addrE"></a> <a id="_CPPv2N14ble_conn_ind_t9peer_addrE"></a> <a id="ble_conn_ind_t::peer_addr__uint8_tA"></a> <a id="structble__conn__ind__t_1a0b799a282a21ff0c6ff25ffaa9454a1c"></a> uint8\_t peer\_addr\[6\]
    :   Peer BT address.

    <a id="_CPPv4N14ble_conn_ind_t12clk_accuracyE"></a>

    <a id="_CPPv3N14ble_conn_ind_t12clk_accuracyE"></a> <a id="_CPPv2N14ble_conn_ind_t12clk_accuracyE"></a> <a id="ble_conn_ind_t::clk_accuracy__uint8_t"></a> <a id="structble__conn__ind__t_1a96a0b4a0940d4d6484bc978a0be2ddc3"></a> uint8\_t clk\_accuracy
    :   Clock accuracy.

    <a id="_CPPv4N14ble_conn_ind_t12con_intervalE"></a>

    <a id="_CPPv3N14ble_conn_ind_t12con_intervalE"></a> <a id="_CPPv2N14ble_conn_ind_t12con_intervalE"></a> <a id="ble_conn_ind_t::con_interval__uint16_t"></a> <a id="structble__conn__ind__t_1a4c9e41b945f7413c8f1603e852e2d240"></a> uint16\_t con\_interval
    :   Connection interval.

    <a id="_CPPv4N14ble_conn_ind_t11con_latencyE"></a>

    <a id="_CPPv3N14ble_conn_ind_t11con_latencyE"></a> <a id="_CPPv2N14ble_conn_ind_t11con_latencyE"></a> <a id="ble_conn_ind_t::con_latency__uint16_t"></a> <a id="structble__conn__ind__t_1a901a0ecf301b255d03e33e038f103761"></a> uint16\_t con\_latency
    :   Connection latency.

    <a id="_CPPv4N14ble_conn_ind_t6sup_toE"></a>

    <a id="_CPPv3N14ble_conn_ind_t6sup_toE"></a> <a id="_CPPv2N14ble_conn_ind_t6sup_toE"></a> <a id="ble_conn_ind_t::sup_to__uint16_t"></a> <a id="structble__conn__ind__t_1a0bce0270464e23963578f8c258797eb0"></a> uint16\_t sup\_to
    :   Link supervision timeout.

<a id="_CPPv416ble_discon_ind_t"></a>

<a id="_CPPv316ble_discon_ind_t"></a> <a id="_CPPv216ble_discon_ind_t"></a> <a id="ble_discon_ind_t"></a> <a id="structble__discon__ind__t"></a> struct ble\_discon\_ind\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16ble_discon_ind_t8conn_idxE"></a>

    <a id="_CPPv3N16ble_discon_ind_t8conn_idxE"></a> <a id="_CPPv2N16ble_discon_ind_t8conn_idxE"></a> <a id="ble_discon_ind_t::conn_idx__uint8_t"></a> <a id="structble__discon__ind__t_1aef720d93c729e305c25cfe81780ad71b"></a> uint8\_t conn\_idx
    :   The index of connection.

    <a id="_CPPv4N16ble_discon_ind_t6reasonE"></a>

    <a id="_CPPv3N16ble_discon_ind_t6reasonE"></a> <a id="_CPPv2N16ble_discon_ind_t6reasonE"></a> <a id="ble_discon_ind_t::reason__uint8_t"></a> <a id="structble__discon__ind__t_1ad74b0d40dc32e699dd9e12ed1cde7aa1"></a> uint8\_t reason
    :   Reason of disconnection.

<a id="_CPPv415ble_create_db_t"></a>

<a id="_CPPv315ble_create_db_t"></a> <a id="_CPPv215ble_create_db_t"></a> <a id="ble_create_db_t"></a> <a id="structble__create__db__t"></a> struct ble\_create\_db\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15ble_create_db_t6statusE"></a>

    <a id="_CPPv3N15ble_create_db_t6statusE"></a> <a id="_CPPv2N15ble_create_db_t6statusE"></a> <a id="ble_create_db_t::status__uint8_t"></a> <a id="structble__create__db__t_1a824468db37268d79ceb9f0a0b2915520"></a> uint8\_t status
    :   The status for creating db

    <a id="_CPPv4N15ble_create_db_t6prf_idE"></a>

    <a id="_CPPv3N15ble_create_db_t6prf_idE"></a> <a id="_CPPv2N15ble_create_db_t6prf_idE"></a> <a id="ble_create_db_t::prf_id__uint8_t"></a> <a id="structble__create__db__t_1ae95753676e170782ec6113bbc803681d"></a> uint8\_t prf\_id
    :   The id of the profile

<a id="_CPPv415ble_attm_desc_t"></a>

<a id="_CPPv315ble_attm_desc_t"></a> <a id="_CPPv215ble_attm_desc_t"></a> <a id="ble_attm_desc_t"></a> <a id="structble__attm__desc__t"></a> struct ble\_attm\_desc\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15ble_attm_desc_t4uuidE"></a>

    <a id="_CPPv3N15ble_attm_desc_t4uuidE"></a> <a id="_CPPv2N15ble_attm_desc_t4uuidE"></a> <a id="ble_attm_desc_t::uuid__uint8_tA"></a> <a id="structble__attm__desc__t_1aa5556efddeaf989b1176681cf2266910"></a> uint8\_t uuid\[16\]
    :   16 bits UUID LSB First

    <a id="_CPPv4N15ble_attm_desc_t4permE"></a>

    <a id="_CPPv3N15ble_attm_desc_t4permE"></a> <a id="_CPPv2N15ble_attm_desc_t4permE"></a> <a id="ble_attm_desc_t::perm__uint16_t"></a> <a id="structble__attm__desc__t_1ae1395c22253723f638922bbc40c8fdc7"></a> uint16\_t perm
    :   Attribute Permissions (see enum [bk\_ble\_perm\_mask](#group__bk__ble__api__v1_1gaa529f18ac0ecdf658b9e49c2fffc7f22))

    <a id="_CPPv4N15ble_attm_desc_t8ext_permE"></a>

    <a id="_CPPv3N15ble_attm_desc_t8ext_permE"></a> <a id="_CPPv2N15ble_attm_desc_t8ext_permE"></a> <a id="ble_attm_desc_t::ext_perm__uint16_t"></a> <a id="structble__attm__desc__t_1aae56741bd16e5a0fc21f5c2a14a293d3"></a> uint16\_t ext\_perm
    :   Attribute Extended Permissions (see enum [bk\_ble\_ext\_perm\_mask](#group__bk__ble__api__v1_1ga3c750771a137d5504854bfcebb6e5235))

    <a id="_CPPv4N15ble_attm_desc_t8max_sizeE"></a>

    <a id="_CPPv3N15ble_attm_desc_t8max_sizeE"></a> <a id="_CPPv2N15ble_attm_desc_t8max_sizeE"></a> <a id="ble_attm_desc_t::max_size__uint16_t"></a> <a id="structble__attm__desc__t_1aa8d08dcf8d2024e44da8ec1cd189d00a"></a> uint16\_t max\_size
    :   Attribute Max Size note: for characteristic declaration contains handle offset note: for included service, contains target service handle

    <a id="_CPPv4N15ble_attm_desc_t15p_value_contextE"></a>

    <a id="_CPPv3N15ble_attm_desc_t15p_value_contextE"></a> <a id="_CPPv2N15ble_attm_desc_t15p_value_contextE"></a> <a id="ble_attm_desc_t::p_value_context__voidP"></a> <a id="structble__attm__desc__t_1a51917b04896f84d52bf4773415fc660c"></a> void \*p\_value\_context
    :   pointer to value if [BK\_BLE\_PERM\_SET(RI, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) not set and [BK\_BLE\_PERM\_SET(VALUE\_INCL, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) set

<a id="_CPPv413bk_ble_db_cfg"></a>

<a id="_CPPv313bk_ble_db_cfg"></a> <a id="_CPPv213bk_ble_db_cfg"></a> <a id="bk_ble_db_cfg"></a> <a id="structbk__ble__db__cfg"></a> struct bk\_ble\_db\_cfg
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13bk_ble_db_cfg4uuidE"></a>

    <a id="_CPPv3N13bk_ble_db_cfg4uuidE"></a> <a id="_CPPv2N13bk_ble_db_cfg4uuidE"></a> <a id="bk_ble_db_cfg::uuid__uint8_tA"></a> <a id="structbk__ble__db__cfg_1aed7b89e50bbe97f1c998072f202a49e1"></a> uint8\_t uuid\[16\]
    :   Service uuid.

    <a id="_CPPv4N13bk_ble_db_cfg9att_db_nbE"></a>

    <a id="_CPPv3N13bk_ble_db_cfg9att_db_nbE"></a> <a id="_CPPv2N13bk_ble_db_cfg9att_db_nbE"></a> <a id="bk_ble_db_cfg::att_db_nb__uint8_t"></a> <a id="structbk__ble__db__cfg_1a850dc90e7312e9b79c80a3a6a2874d45"></a> uint8\_t att\_db\_nb
    :   Number of db.

    <a id="_CPPv4N13bk_ble_db_cfg9start_hdlE"></a>

    <a id="_CPPv3N13bk_ble_db_cfg9start_hdlE"></a> <a id="_CPPv2N13bk_ble_db_cfg9start_hdlE"></a> <a id="bk_ble_db_cfg::start_hdl__uint16_t"></a> <a id="structbk__ble__db__cfg_1a963b8418954491413550ad82081a5997"></a> uint16\_t start\_hdl
    :   Start handler, 0 means autoalloc.

    <a id="_CPPv4N13bk_ble_db_cfg6att_dbE"></a>

    <a id="_CPPv3N13bk_ble_db_cfg6att_dbE"></a> <a id="_CPPv2N13bk_ble_db_cfg6att_dbE"></a> <a id="bk_ble_db_cfg::att_db__ble_attm_desc_tP"></a> <a id="structbk__ble__db__cfg_1ade205f79f2b9e4a7a78afa5c20fa2236"></a> [ble\_attm\_desc\_t](#_CPPv415ble_attm_desc_t "ble_attm_desc_t") \*att\_db
    :   Attribute database.

    <a id="_CPPv4N13bk_ble_db_cfg8svc_permE"></a>

    <a id="_CPPv3N13bk_ble_db_cfg8svc_permE"></a> <a id="_CPPv2N13bk_ble_db_cfg8svc_permE"></a> <a id="bk_ble_db_cfg::svc_perm__uint8_t"></a> <a id="structbk__ble__db__cfg_1a5d40d0a144bb9551f76ad1a94b402c63"></a> uint8\_t svc\_perm
    :   Service config.

<a id="_CPPv417ble_init_config_t"></a>

<a id="_CPPv317ble_init_config_t"></a> <a id="_CPPv217ble_init_config_t"></a> <a id="ble_init_config_t"></a> <a id="structble__init__config__t"></a> struct ble\_init\_config\_t

<a id="_CPPv49bd_addr_t"></a>

<a id="_CPPv39bd_addr_t"></a> <a id="_CPPv29bd_addr_t"></a> <a id="bd_addr_t"></a> <a id="structbd__addr__t"></a> struct bd\_addr\_t

<a id="_CPPv417ble_cmd_cmp_evt_t"></a>

<a id="_CPPv317ble_cmd_cmp_evt_t"></a> <a id="_CPPv217ble_cmd_cmp_evt_t"></a> <a id="ble_cmd_cmp_evt_t"></a> <a id="structble__cmd__cmp__evt__t"></a> struct ble\_cmd\_cmp\_evt\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17ble_cmd_cmp_evt_t8conn_idxE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t8conn_idxE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t8conn_idxE"></a> <a id="ble_cmd_cmp_evt_t::conn_idx__uint8_t"></a> <a id="structble__cmd__cmp__evt__t_1a14612959f482d00b064d75aad85e226b"></a> uint8\_t conn\_idx
    :   The index of connection.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t3cmdE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t3cmdE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t3cmdE"></a> <a id="ble_cmd_cmp_evt_t::cmd__uint8_t"></a> <a id="structble__cmd__cmp__evt__t_1aade764f95d495269484551166753320e"></a> uint8\_t cmd
    :   Command operation.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t6statusE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t6statusE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t6statusE"></a> <a id="ble_cmd_cmp_evt_t::status__uint8_t"></a> <a id="structble__cmd__cmp__evt__t_1abf1b93dfd8d3870401765a9010252d31"></a> uint8\_t status
    :   Command operation status.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t3psmE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t3psmE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t3psmE"></a> <a id="ble_cmd_cmp_evt_t::psm__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1a9127963a8297b90ad50b7e24f242bce7"></a> uint16\_t psm
    :   registered Protocol/Service Multiplexer value

        configured Protocol/Service Multiplexer value

    <a id="_CPPv4N17ble_cmd_cmp_evt_t11coc_reg_evtE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t11coc_reg_evtE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t11coc_reg_evtE"></a> <a id="structble__cmd__cmp__evt__t_1a0da542aecb747725e7fce4a5a556c71d"></a> struct [ble\_cmd\_cmp\_evt\_t](#_CPPv417ble_cmd_cmp_evt_t "ble_cmd_cmp_evt_t")::\[anonymous\]::\[anonymous\] coc\_reg\_evt
    :   BLE\_5\_COC\_REG\_COMPL\_EVENT.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t14coc_config_evtE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t14coc_config_evtE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t14coc_config_evtE"></a> <a id="structble__cmd__cmp__evt__t_1aee20e76a8e5faaca48fc9e821f8fc9e9"></a> struct [ble\_cmd\_cmp\_evt\_t](#_CPPv417ble_cmd_cmp_evt_t "ble_cmd_cmp_evt_t")::\[anonymous\]::\[anonymous\] coc\_config\_evt
    :   BLE\_5\_COC\_CONFIG\_COMPL\_EVENT.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t6le_psmE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t6le_psmE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t6le_psmE"></a> <a id="ble_cmd_cmp_evt_t::le_psm__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1a7fede8e3558b88b08f87991e3f85f37d"></a> uint16\_t le\_psm
    :   Protocol/Service Multiplexer value.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t9local_cidE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t9local_cidE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t9local_cidE"></a> <a id="ble_cmd_cmp_evt_t::local_cid__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1aac1a552389adedbde4806786e6cc22f2"></a> uint16\_t local\_cid
    :   local Channel ID of the established channel

        local Channel ID of the disconnected channel

    <a id="_CPPv4N17ble_cmd_cmp_evt_t11peer_creditE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t11peer_creditE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t11peer_creditE"></a> <a id="ble_cmd_cmp_evt_t::peer_credit__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1ae59f1ef0d221d16e95f31d18cd46b8a7"></a> uint16\_t peer\_credit
    :   peer’s initial credits

    <a id="_CPPv4N17ble_cmd_cmp_evt_t8peer_mtuE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t8peer_mtuE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t8peer_mtuE"></a> <a id="ble_cmd_cmp_evt_t::peer_mtu__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1a532524991d43f1b3e8b46401acebad4c"></a> uint16\_t peer\_mtu
    :   peer’s Maximum Transmission Unit size

    <a id="_CPPv4N17ble_cmd_cmp_evt_t8peer_mpsE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t8peer_mpsE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t8peer_mpsE"></a> <a id="ble_cmd_cmp_evt_t::peer_mps__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1a3952b9648b8848e8a0b3e80005b5deb5"></a> uint16\_t peer\_mps
    :   peer’s Maximum PDU Payload Size

    <a id="_CPPv4N17ble_cmd_cmp_evt_t24coc_connection_compl_evtE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t24coc_connection_compl_evtE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t24coc_connection_compl_evtE"></a> <a id="structble__cmd__cmp__evt__t_1aea61da2132cbc65235dbadc989d5fda3"></a> struct [ble\_cmd\_cmp\_evt\_t](#_CPPv417ble_cmd_cmp_evt_t "ble_cmd_cmp_evt_t")::\[anonymous\]::\[anonymous\] coc\_connection\_compl\_evt
    :   BLE\_5\_COC\_CONNECTION\_COMPL\_EVENT.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t6reasonE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t6reasonE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t6reasonE"></a> <a id="ble_cmd_cmp_evt_t::reason__uint8_t"></a> <a id="structble__cmd__cmp__evt__t_1a10c15dc79dffd794761c187bdedbf59c"></a> uint8\_t reason
    :   disconnection reason

    <a id="_CPPv4N17ble_cmd_cmp_evt_t24coc_disconnect_compl_evtE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t24coc_disconnect_compl_evtE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t24coc_disconnect_compl_evtE"></a> <a id="structble__cmd__cmp__evt__t_1a13c41a8e7c34111a97dd322aed105671"></a> struct [ble\_cmd\_cmp\_evt\_t](#_CPPv417ble_cmd_cmp_evt_t "ble_cmd_cmp_evt_t")::\[anonymous\]::\[anonymous\] coc\_disconnect\_compl\_evt
    :   BLE\_5\_COC\_DISCCONNECT\_COMPL\_EVENT.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t3cidE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t3cidE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t3cidE"></a> <a id="ble_cmd_cmp_evt_t::cid__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1ab72e04d00b229bfd135e27c6de391119"></a> uint16\_t cid
    :   Channel ID.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t6creditE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t6creditE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t6creditE"></a> <a id="ble_cmd_cmp_evt_t::credit__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1a458958c73262d74a081dae4990fc3e14"></a> uint16\_t credit
    :   remaining/returned credits

        remaining credits

    <a id="_CPPv4N17ble_cmd_cmp_evt_t18coc_send_compl_evtE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t18coc_send_compl_evtE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t18coc_send_compl_evtE"></a> <a id="structble__cmd__cmp__evt__t_1a412c7d9dfc3f1a8ded22dd7488f66661"></a> struct [ble\_cmd\_cmp\_evt\_t](#_CPPv417ble_cmd_cmp_evt_t "ble_cmd_cmp_evt_t")::\[anonymous\]::\[anonymous\] coc\_send\_compl\_evt
    :   BLE\_5\_COC\_TX\_DONE.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t6offsetE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t6offsetE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t6offsetE"></a> <a id="ble_cmd_cmp_evt_t::offset__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1abc485bc5dc9505e639c740dc75b86134"></a> uint16\_t offset
    :   data offset within the SDU

    <a id="_CPPv4N17ble_cmd_cmp_evt_t6lengthE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t6lengthE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t6lengthE"></a> <a id="ble_cmd_cmp_evt_t::length__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1a5cb0291b6fd0259f311d443bb977272d"></a> uint16\_t length
    :   length of received data

    <a id="_CPPv4N17ble_cmd_cmp_evt_t4dataE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t4dataE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t4dataE"></a> <a id="ble_cmd_cmp_evt_t::data__uint8_tCP"></a> <a id="structble__cmd__cmp__evt__t_1a2954a59f1c4bb7c6681e4baebf461920"></a> const uint8\_t \*data
    :   pointer to the received data

    <a id="_CPPv4N17ble_cmd_cmp_evt_t12coc_recv_evtE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t12coc_recv_evtE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t12coc_recv_evtE"></a> <a id="structble__cmd__cmp__evt__t_1a535708e1c91a186d9bc7a3b945e39a7a"></a> struct [ble\_cmd\_cmp\_evt\_t](#_CPPv417ble_cmd_cmp_evt_t "ble_cmd_cmp_evt_t")::\[anonymous\]::\[anonymous\] coc\_recv\_evt
    :   BLE\_5\_COC\_RX\_IND.

    <a id="_CPPv4N17ble_cmd_cmp_evt_t8peer_cidE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t8peer_cidE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t8peer_cidE"></a> <a id="ble_cmd_cmp_evt_t::peer_cid__uint16_t"></a> <a id="structble__cmd__cmp__evt__t_1ac9cc8f10f39f0618692c83c6834b2e79"></a> uint16\_t peer\_cid
    :   peer’s Channel ID

    <a id="_CPPv4N17ble_cmd_cmp_evt_t19coc_connect_req_evtE"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_t19coc_connect_req_evtE"></a> <a id="_CPPv2N17ble_cmd_cmp_evt_t19coc_connect_req_evtE"></a> <a id="structble__cmd__cmp__evt__t_1afc56135177a09ecc680958ec038c9498"></a> struct [ble\_cmd\_cmp\_evt\_t](#_CPPv417ble_cmd_cmp_evt_t "ble_cmd_cmp_evt_t")::\[anonymous\]::\[anonymous\] coc\_connect\_req\_evt
    :   BLE\_5\_COC\_CONNECT\_REQ\_EVENT.

    <a id="_CPPv4N17ble_cmd_cmp_evt_tUt1_4E"></a>

    <a id="_CPPv3N17ble_cmd_cmp_evt_tUt1_4E"></a> <a id="structble__cmd__cmp__evt__t_1a4009e521a27a6af2f28c1aa0acf1728b"></a> union [ble\_cmd\_cmp\_evt\_t](#_CPPv417ble_cmd_cmp_evt_t "ble_cmd_cmp_evt_t")::\[anonymous\] \[anonymous\]
    :   Event-specific payload, valid according to the reported “cmd”.

<a id="_CPPv414ble_read_phy_t"></a>

<a id="_CPPv314ble_read_phy_t"></a> <a id="_CPPv214ble_read_phy_t"></a> <a id="ble_read_phy_t"></a> <a id="structble__read__phy__t"></a> struct ble\_read\_phy\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N14ble_read_phy_t6tx_phyE"></a>

    <a id="_CPPv3N14ble_read_phy_t6tx_phyE"></a> <a id="_CPPv2N14ble_read_phy_t6tx_phyE"></a> <a id="ble_read_phy_t::tx_phy__uint8_t"></a> <a id="structble__read__phy__t_1a512ed2d8fd49223a8910b4f209ba4e77"></a> uint8\_t tx\_phy
    :   The transmitter PHY

    <a id="_CPPv4N14ble_read_phy_t6rx_phyE"></a>

    <a id="_CPPv3N14ble_read_phy_t6rx_phyE"></a> <a id="_CPPv2N14ble_read_phy_t6rx_phyE"></a> <a id="ble_read_phy_t::rx_phy__uint8_t"></a> <a id="structble__read__phy__t_1aaacac6fe720bc36b1b34566ab1abde3f"></a> uint8\_t rx\_phy
    :   The receiver PHY

<a id="_CPPv413ble_set_phy_t"></a>

<a id="_CPPv313ble_set_phy_t"></a> <a id="_CPPv213ble_set_phy_t"></a> <a id="ble_set_phy_t"></a> <a id="structble__set__phy__t"></a> struct ble\_set\_phy\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13ble_set_phy_t6tx_phyE"></a>

    <a id="_CPPv3N13ble_set_phy_t6tx_phyE"></a> <a id="_CPPv2N13ble_set_phy_t6tx_phyE"></a> <a id="ble_set_phy_t::tx_phy__uint8_t"></a> <a id="structble__set__phy__t_1a7c02467fdbc77d96d67dff65d90112b9"></a> uint8\_t tx\_phy
    :   The transmitter PHY

    <a id="_CPPv4N13ble_set_phy_t6rx_phyE"></a>

    <a id="_CPPv3N13ble_set_phy_t6rx_phyE"></a> <a id="_CPPv2N13ble_set_phy_t6rx_phyE"></a> <a id="ble_set_phy_t::rx_phy__uint8_t"></a> <a id="structble__set__phy__t_1a0eb779c69a7ed6e92f45d552818e3161"></a> uint8\_t rx\_phy
    :   The receiver PHY

    <a id="_CPPv4N13ble_set_phy_t7phy_optE"></a>

    <a id="_CPPv3N13ble_set_phy_t7phy_optE"></a> <a id="_CPPv2N13ble_set_phy_t7phy_optE"></a> <a id="ble_set_phy_t::phy_opt__uint8_t"></a> <a id="structble__set__phy__t_1a8a96262b9400a193679625f6ac192a3f"></a> uint8\_t phy\_opt
    :   PHY options

<a id="_CPPv415ble_adv_param_t"></a>

<a id="_CPPv315ble_adv_param_t"></a> <a id="_CPPv215ble_adv_param_t"></a> <a id="ble_adv_param_t"></a> <a id="structble__adv__param__t"></a> struct ble\_adv\_param\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N15ble_adv_param_t13own_addr_typeE"></a>

    <a id="_CPPv3N15ble_adv_param_t13own_addr_typeE"></a> <a id="_CPPv2N15ble_adv_param_t13own_addr_typeE"></a> <a id="ble_adv_param_t::own_addr_type__uint8_t"></a> <a id="structble__adv__param__t_1a6f1a854b16ae312ff007c80969c91475"></a> uint8\_t own\_addr\_type
    :   Own address type: see enum [ble\_own\_addr\_type](#group__bk__ble__api__v1__typedef_1gaaa7b5c55bc3b207c84e20eca8e0c7223).

    <a id="_CPPv4N15ble_adv_param_t8adv_typeE"></a>

    <a id="_CPPv3N15ble_adv_param_t8adv_typeE"></a> <a id="_CPPv2N15ble_adv_param_t8adv_typeE"></a> <a id="ble_adv_param_t::adv_type__uint8_t"></a> <a id="structble__adv__param__t_1a6e865fec2db0cc0eaee3e477918f1c38"></a> uint8\_t adv\_type
    :   Advertising type (see enum [adv\_type](#structble__adv__param__t_1a6e865fec2db0cc0eaee3e477918f1c38))

    <a id="_CPPv4N15ble_adv_param_t8chnl_mapE"></a>

    <a id="_CPPv3N15ble_adv_param_t8chnl_mapE"></a> <a id="_CPPv2N15ble_adv_param_t8chnl_mapE"></a> <a id="ble_adv_param_t::chnl_map__uint8_t"></a> <a id="structble__adv__param__t_1ae5136acc3ec82c51b7fcc690a15aa80b"></a> uint8\_t chnl\_map
    :   Bit field indicating the channel mapping (see enum [adv\_chnl\_map](#group__bk__ble__api__v1__typedef_1ga57c9e3ee8efb2e8c2fcc35e570f8679a))

    <a id="_CPPv4N15ble_adv_param_t8adv_propE"></a>

    <a id="_CPPv3N15ble_adv_param_t8adv_propE"></a> <a id="_CPPv2N15ble_adv_param_t8adv_propE"></a> <a id="ble_adv_param_t::adv_prop__uint16_t"></a> <a id="structble__adv__param__t_1a88155e8b3ac2265ed5f26e01d0e024dd"></a> uint16\_t adv\_prop
    :   Bit field value provided advertising properties (see enum [adv\_prop\_bf](#group__bk__ble__api__v1__typedef_1ga6b5140e1b8fe4043c83c62cbdfdd20c3))

    <a id="_CPPv4N15ble_adv_param_t12adv_intv_minE"></a>

    <a id="_CPPv3N15ble_adv_param_t12adv_intv_minE"></a> <a id="_CPPv2N15ble_adv_param_t12adv_intv_minE"></a> <a id="ble_adv_param_t::adv_intv_min__uint32_t"></a> <a id="structble__adv__param__t_1a10f76572775faab83d26244978ec53d9"></a> uint32\_t adv\_intv\_min
    :   Minimum advertising interval (in unit of 625us). Must be greater than or equal to 20ms.

    <a id="_CPPv4N15ble_adv_param_t12adv_intv_maxE"></a>

    <a id="_CPPv3N15ble_adv_param_t12adv_intv_maxE"></a> <a id="_CPPv2N15ble_adv_param_t12adv_intv_maxE"></a> <a id="ble_adv_param_t::adv_intv_max__uint32_t"></a> <a id="structble__adv__param__t_1a68c97dfb28cb08faef0eb43eff114c69"></a> uint32\_t adv\_intv\_max
    :   Maximum advertising interval (in unit of 625us). Must be greater than or equal to 20ms.

    <a id="_CPPv4N15ble_adv_param_t8prim_phyE"></a>

    <a id="_CPPv3N15ble_adv_param_t8prim_phyE"></a> <a id="_CPPv2N15ble_adv_param_t8prim_phyE"></a> <a id="ble_adv_param_t::prim_phy__uint8_t"></a> <a id="structble__adv__param__t_1a15208842eae32fc0e618f3a104b15d8e"></a> uint8\_t prim\_phy
    :   Indicate on which PHY primary advertising has to be performed (see enum [phy\_type\_le](#group__bk__ble__api__v1__typedef_1ga4acd0e053cbeead642d1317913613874)) Note that LE 2M PHY is not allowed and that legacy advertising only support LE 1M PHY

    <a id="_CPPv4N15ble_adv_param_t10second_phyE"></a>

    <a id="_CPPv3N15ble_adv_param_t10second_phyE"></a> <a id="_CPPv2N15ble_adv_param_t10second_phyE"></a> <a id="ble_adv_param_t::second_phy__uint8_t"></a> <a id="structble__adv__param__t_1a996fd748977a38954f18006538ba1c1b"></a> uint8\_t second\_phy
    :   Indicate on which PHY secondary advertising has to be performed (see enum [phy\_type\_le](#group__bk__ble__api__v1__typedef_1ga4acd0e053cbeead642d1317913613874))

    <a id="_CPPv4N15ble_adv_param_t14peer_addr_typeE"></a>

    <a id="_CPPv3N15ble_adv_param_t14peer_addr_typeE"></a> <a id="_CPPv2N15ble_adv_param_t14peer_addr_typeE"></a> <a id="ble_adv_param_t::peer_addr_type__uint8_t"></a> <a id="structble__adv__param__t_1a2374b2ee7a1b171ed41706411809c509"></a> uint8\_t peer\_addr\_type
    :   Peer address type: 0\=public/1\=private random, used for directed adv.

    <a id="_CPPv4N15ble_adv_param_t9peer_addrE"></a>

    <a id="_CPPv3N15ble_adv_param_t9peer_addrE"></a> <a id="_CPPv2N15ble_adv_param_t9peer_addrE"></a> <a id="ble_adv_param_t::peer_addr__bd_addr_t"></a> <a id="structble__adv__param__t_1a06f30baba8c4630a7eb553fc3caacd20"></a> [bd\_addr\_t](#_CPPv49bd_addr_t "bd_addr_t") peer\_addr
    :   Peer address, used for directed adv.

<a id="_CPPv416ble_scan_param_t"></a>

<a id="_CPPv316ble_scan_param_t"></a> <a id="_CPPv216ble_scan_param_t"></a> <a id="ble_scan_param_t"></a> <a id="structble__scan__param__t"></a> struct ble\_scan\_param\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16ble_scan_param_t13own_addr_typeE"></a>

    <a id="_CPPv3N16ble_scan_param_t13own_addr_typeE"></a> <a id="_CPPv2N16ble_scan_param_t13own_addr_typeE"></a> <a id="ble_scan_param_t::own_addr_type__uint8_t"></a> <a id="structble__scan__param__t_1abe6dce83e26b4ba6e6385d526b4d1bdb"></a> uint8\_t own\_addr\_type
    :   Own address type: see enum [ble\_own\_addr\_type](#group__bk__ble__api__v1__typedef_1gaaa7b5c55bc3b207c84e20eca8e0c7223).

    <a id="_CPPv4N16ble_scan_param_t8scan_phyE"></a>

    <a id="_CPPv3N16ble_scan_param_t8scan_phyE"></a> <a id="_CPPv2N16ble_scan_param_t8scan_phyE"></a> <a id="ble_scan_param_t::scan_phy__uint8_t"></a> <a id="structble__scan__param__t_1a4e220e9c3d40f93ab380f7b14c8de3ed"></a> uint8\_t scan\_phy
    :   on which the advertising packets should be received: LE 1M\=1 / LE CODED\=4 / LE 1M and LE CODED\=5

    <a id="_CPPv4N16ble_scan_param_t9scan_intvE"></a>

    <a id="_CPPv3N16ble_scan_param_t9scan_intvE"></a> <a id="_CPPv2N16ble_scan_param_t9scan_intvE"></a> <a id="ble_scan_param_t::scan_intv__uint16_t"></a> <a id="structble__scan__param__t_1a4e5db3d10db53fa49af639924d82290f"></a> uint16\_t scan\_intv
    :   Scan interval (in unit of 625us). Must be greater than or equal to 2.5ms.

    <a id="_CPPv4N16ble_scan_param_t7scan_wdE"></a>

    <a id="_CPPv3N16ble_scan_param_t7scan_wdE"></a> <a id="_CPPv2N16ble_scan_param_t7scan_wdE"></a> <a id="ble_scan_param_t::scan_wd__uint16_t"></a> <a id="structble__scan__param__t_1a5f9e94be9176f6c8c96d2508aa376227"></a> uint16\_t scan\_wd
    :   Scan window (in unit of 625us). Must be greater than or equal to 2.5ms.

    <a id="_CPPv4N16ble_scan_param_t9scan_typeE"></a>

    <a id="_CPPv3N16ble_scan_param_t9scan_typeE"></a> <a id="_CPPv2N16ble_scan_param_t9scan_typeE"></a> <a id="ble_scan_param_t::scan_type__uint8_t"></a> <a id="structble__scan__param__t_1a02946aca2c31fc1b4efa9912c61ac6a0"></a> uint8\_t scan\_type
    :   Scan type: see enum [ble\_scan\_type](#group__bk__ble__api__v1__typedef_1ga364631dfaf59ba0e1df8a02a43fa63d6).

    <a id="_CPPv4N16ble_scan_param_t11scan_filterE"></a>

    <a id="_CPPv3N16ble_scan_param_t11scan_filterE"></a> <a id="_CPPv2N16ble_scan_param_t11scan_filterE"></a> <a id="ble_scan_param_t::scan_filter__uint8_t"></a> <a id="structble__scan__param__t_1abf2b4dc1485ec6aa9631a5e819562ffb"></a> uint8\_t scan\_filter
    :   Scan type: see enum [ble\_scan\_filter\_policy](#group__bk__ble__api__v1__typedef_1ga6bbb5b4b01f2f6a60164943eb569795e).

<a id="_CPPv416ble_conn_param_t"></a>

<a id="_CPPv316ble_conn_param_t"></a> <a id="_CPPv216ble_conn_param_t"></a> <a id="ble_conn_param_t"></a> <a id="structble__conn__param__t"></a> struct ble\_conn\_param\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N16ble_conn_param_t8intv_minE"></a>

    <a id="_CPPv3N16ble_conn_param_t8intv_minE"></a> <a id="_CPPv2N16ble_conn_param_t8intv_minE"></a> <a id="ble_conn_param_t::intv_min__uint16_t"></a> <a id="structble__conn__param__t_1aca198b6c52b979cdcc00940b6821c935"></a> uint16\_t intv\_min
    :   Connection interval minimum (in unit of 1.25ms). Must be greater than or equal to 7.5ms.

    <a id="_CPPv4N16ble_conn_param_t8intv_maxE"></a>

    <a id="_CPPv3N16ble_conn_param_t8intv_maxE"></a> <a id="_CPPv2N16ble_conn_param_t8intv_maxE"></a> <a id="ble_conn_param_t::intv_max__uint16_t"></a> <a id="structble__conn__param__t_1a78809b7b8cf8043c7cde434b4d1e0a12"></a> uint16\_t intv\_max
    :   Connection interval maximum (in unit of 1.25ms). Must be greater than or equal to 7.5ms.

    <a id="_CPPv4N16ble_conn_param_t11con_latencyE"></a>

    <a id="_CPPv3N16ble_conn_param_t11con_latencyE"></a> <a id="_CPPv2N16ble_conn_param_t11con_latencyE"></a> <a id="ble_conn_param_t::con_latency__uint16_t"></a> <a id="structble__conn__param__t_1a25b0aba39495037e46c3c07d107bfaf4"></a> uint16\_t con\_latency
    :   Connection latency. The range is 0x0000 to 0x01F3.

    <a id="_CPPv4N16ble_conn_param_t6sup_toE"></a>

    <a id="_CPPv3N16ble_conn_param_t6sup_toE"></a> <a id="_CPPv2N16ble_conn_param_t6sup_toE"></a> <a id="ble_conn_param_t::sup_to__uint16_t"></a> <a id="structble__conn__param__t_1abb1fa7075dc1063cb2a029c181a79f63"></a> uint16\_t sup\_to
    :   Link supervision timeout(in unit of 10ms). Must be greater than or equal to 100ms.

    <a id="_CPPv4N16ble_conn_param_t9init_physE"></a>

    <a id="_CPPv3N16ble_conn_param_t9init_physE"></a> <a id="_CPPv2N16ble_conn_param_t9init_physE"></a> <a id="ble_conn_param_t::init_phys__uint8_t"></a> <a id="structble__conn__param__t_1ae5cf2a7588a3e78fb906d623194f686a"></a> uint8\_t init\_phys
    :   on which the advertising packets should be received on the primary advertising physical channel (see enum [phy\_type\_le](#group__bk__ble__api__v1__typedef_1ga4acd0e053cbeead642d1317913613874))

    <a id="_CPPv4N16ble_conn_param_t8conn_idxE"></a>

    <a id="_CPPv3N16ble_conn_param_t8conn_idxE"></a> <a id="_CPPv2N16ble_conn_param_t8conn_idxE"></a> <a id="ble_conn_param_t::conn_idx__uint8_t"></a> <a id="structble__conn__param__t_1a5b6481d017cbfe9380e808c9e9d437f9"></a> uint8\_t conn\_idx
    :   The index of connection.

    <a id="_CPPv4N16ble_conn_param_t13filter_policyE"></a>

    <a id="_CPPv3N16ble_conn_param_t13filter_policyE"></a> <a id="_CPPv2N16ble_conn_param_t13filter_policyE"></a> <a id="ble_conn_param_t::filter_policy__uint8_t"></a> <a id="structble__conn__param__t_1a777332c2f5a124436031f064b6a034a4"></a> uint8\_t filter\_policy
    :   Initiating type: see enum [initiating\_filter\_type\_le](#group__bk__ble__api__v1__typedef_1gaf5be121573ef75ad997530941fa7c99a) (e.g. INIT\_TYPE\_LE\_DIRECT\_CONN\_EST connects the indicated peer address, INIT\_TYPE\_LE\_AUTO\_CONN\_EST connects devices in the white list)

<a id="_CPPv420ble_periodic_param_t"></a>

<a id="_CPPv320ble_periodic_param_t"></a> <a id="_CPPv220ble_periodic_param_t"></a> <a id="ble_periodic_param_t"></a> <a id="structble__periodic__param__t"></a> struct ble\_periodic\_param\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20ble_periodic_param_t14report_disableE"></a>

    <a id="_CPPv3N20ble_periodic_param_t14report_disableE"></a> <a id="_CPPv2N20ble_periodic_param_t14report_disableE"></a> <a id="ble_periodic_param_t::report_disable__uint8_t"></a> <a id="structble__periodic__param__t_1ae1d57ecf55a55dc5f778c9603dc9b2e7"></a> uint8\_t report\_disable
    :   1 to disable periodic advertising report, 0 to enable them by default

    <a id="_CPPv4N20ble_periodic_param_t7adv_sidE"></a>

    <a id="_CPPv3N20ble_periodic_param_t7adv_sidE"></a> <a id="_CPPv2N20ble_periodic_param_t7adv_sidE"></a> <a id="ble_periodic_param_t::adv_sid__uint8_t"></a> <a id="structble__periodic__param__t_1a75ae20862225eeafcec072af2475e8e5"></a> uint8\_t adv\_sid
    :   adv sid of advertiser(0x00 to 0x0F)

    <a id="_CPPv4N20ble_periodic_param_t8adv_addrE"></a>

    <a id="_CPPv3N20ble_periodic_param_t8adv_addrE"></a> <a id="_CPPv2N20ble_periodic_param_t8adv_addrE"></a> <a id="ble_periodic_param_t::adv_addr__bd_addr_t"></a> <a id="structble__periodic__param__t_1aa5e55b7c6667f7a8a64381d5f57beb0a"></a> [bd\_addr\_t](#_CPPv49bd_addr_t "bd_addr_t") adv\_addr
    :   Address of advertiser with which synchronization has to be established (used only if use\_pal is false)

    <a id="_CPPv4N20ble_periodic_param_t4skipE"></a>

    <a id="_CPPv3N20ble_periodic_param_t4skipE"></a> <a id="_CPPv2N20ble_periodic_param_t4skipE"></a> <a id="ble_periodic_param_t::skip__uint16_t"></a> <a id="structble__periodic__param__t_1ae7fd1bf008f4a247996f5892a0378b50"></a> uint16\_t skip
    :   Number of periodic advertising that can be skipped after a successful receive. Maximum authorized value is 499

    <a id="_CPPv4N20ble_periodic_param_t7sync_toE"></a>

    <a id="_CPPv3N20ble_periodic_param_t7sync_toE"></a> <a id="_CPPv2N20ble_periodic_param_t7sync_toE"></a> <a id="ble_periodic_param_t::sync_to__uint16_t"></a> <a id="structble__periodic__param__t_1a70e718edb4b1f61d9baa5c1c9c784914"></a> uint16\_t sync\_to
    :   Synchronization timeout for the periodic advertising (in unit of 10ms between 100ms and 163.84s)

    <a id="_CPPv4N20ble_periodic_param_t8cte_typeE"></a>

    <a id="_CPPv3N20ble_periodic_param_t8cte_typeE"></a> <a id="_CPPv2N20ble_periodic_param_t8cte_typeE"></a> <a id="ble_periodic_param_t::cte_type__uint8_t"></a> <a id="structble__periodic__param__t_1a6af2f2c28db8765fde4dad4e89d82fb4"></a> uint8\_t cte\_type
    :   Type of Constant Tone Extension device should sync on (see enum [ble\_sync\_cte\_type](#group__bk__ble__api__v1__typedef_1ga7249d9eb7c2b2f4a4f56b4c241e6db5f)).

<a id="_CPPv426ble_conn_update_para_ind_t"></a>

<a id="_CPPv326ble_conn_update_para_ind_t"></a> <a id="_CPPv226ble_conn_update_para_ind_t"></a> <a id="ble_conn_update_para_ind_t"></a> <a id="structble__conn__update__para__ind__t"></a> struct ble\_conn\_update\_para\_ind\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N26ble_conn_update_para_ind_t8conn_idxE"></a>

    <a id="_CPPv3N26ble_conn_update_para_ind_t8conn_idxE"></a> <a id="_CPPv2N26ble_conn_update_para_ind_t8conn_idxE"></a> <a id="ble_conn_update_para_ind_t::conn_idx__uint8_t"></a> <a id="structble__conn__update__para__ind__t_1a0011063616f8807786ae4dcb74d775d0"></a> uint8\_t conn\_idx
    :   0:is not agree,1:is agree,0xFF;Let me think about it;other:is agree

    <a id="_CPPv4N26ble_conn_update_para_ind_t10ce_len_minE"></a>

    <a id="_CPPv3N26ble_conn_update_para_ind_t10ce_len_minE"></a> <a id="_CPPv2N26ble_conn_update_para_ind_t10ce_len_minE"></a> <a id="ble_conn_update_para_ind_t::ce_len_min__uint16_t"></a> <a id="structble__conn__update__para__ind__t_1a24a00a5ff64af79fb58cd202752ac783"></a> uint16\_t ce\_len\_min
    :   Minimum Connection Event Duration.

    <a id="_CPPv4N26ble_conn_update_para_ind_t10ce_len_maxE"></a>

    <a id="_CPPv3N26ble_conn_update_para_ind_t10ce_len_maxE"></a> <a id="_CPPv2N26ble_conn_update_para_ind_t10ce_len_maxE"></a> <a id="ble_conn_update_para_ind_t::ce_len_max__uint16_t"></a> <a id="structble__conn__update__para__ind__t_1a0a7b127322f162ab289d4c2a4ea1fbe9"></a> uint16\_t ce\_len\_max
    :   Maximum Connection Event Duration.

    <a id="_CPPv4N26ble_conn_update_para_ind_t8intv_minE"></a>

    <a id="_CPPv3N26ble_conn_update_para_ind_t8intv_minE"></a> <a id="_CPPv2N26ble_conn_update_para_ind_t8intv_minE"></a> <a id="ble_conn_update_para_ind_t::intv_min__uint16_t"></a> <a id="structble__conn__update__para__ind__t_1addcda9188c4ef00cb5a9206b666eb2cf"></a> uint16\_t intv\_min
    :   Connection interval minimum.

    <a id="_CPPv4N26ble_conn_update_para_ind_t8intv_maxE"></a>

    <a id="_CPPv3N26ble_conn_update_para_ind_t8intv_maxE"></a> <a id="_CPPv2N26ble_conn_update_para_ind_t8intv_maxE"></a> <a id="ble_conn_update_para_ind_t::intv_max__uint16_t"></a> <a id="structble__conn__update__para__ind__t_1a266cf438364df9cb38cd2c9588e8b70c"></a> uint16\_t intv\_max
    :   Connection interval maximum.

    <a id="_CPPv4N26ble_conn_update_para_ind_t7latencyE"></a>

    <a id="_CPPv3N26ble_conn_update_para_ind_t7latencyE"></a> <a id="_CPPv2N26ble_conn_update_para_ind_t7latencyE"></a> <a id="ble_conn_update_para_ind_t::latency__uint16_t"></a> <a id="structble__conn__update__para__ind__t_1ae86d7e016b82cd2f409588262dffef67"></a> uint16\_t latency
    :   Latency.

    <a id="_CPPv4N26ble_conn_update_para_ind_t8time_outE"></a>

    <a id="_CPPv3N26ble_conn_update_para_ind_t8time_outE"></a> <a id="_CPPv2N26ble_conn_update_para_ind_t8time_outE"></a> <a id="ble_conn_update_para_ind_t::time_out__uint16_t"></a> <a id="structble__conn__update__para__ind__t_1aec7a28e3af4c1e8bcd1b1e7dde38b21c"></a> uint16\_t time\_out
    :   Supervision timeout.

<a id="_CPPv420mst_comm_updata_para"></a>

<a id="_CPPv320mst_comm_updata_para"></a> <a id="_CPPv220mst_comm_updata_para"></a> <a id="mst_comm_updata_para"></a> <a id="structmst__comm__updata__para"></a> struct mst\_comm\_updata\_para
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N20mst_comm_updata_para8is_agreeE"></a>

    <a id="_CPPv3N20mst_comm_updata_para8is_agreeE"></a> <a id="_CPPv2N20mst_comm_updata_para8is_agreeE"></a> <a id="mst_comm_updata_para::is_agree__uint8_t"></a> <a id="structmst__comm__updata__para_1a79d2e4cc44e721d1d25b40e5ddc50577"></a> uint8\_t is\_agree
    :   Status of the request.

    <a id="_CPPv4N20mst_comm_updata_para10ce_len_minE"></a>

    <a id="_CPPv3N20mst_comm_updata_para10ce_len_minE"></a> <a id="_CPPv2N20mst_comm_updata_para10ce_len_minE"></a> <a id="mst_comm_updata_para::ce_len_min__uint16_t"></a> <a id="structmst__comm__updata__para_1a18b3e9067466395ae730bf48b845d1ff"></a> uint16\_t ce\_len\_min
    :   Minimum Connection Event Duration.

        0:is not agree,1:is agree,0xFF;Let me think about it;other:is agree

    <a id="_CPPv4N20mst_comm_updata_para10ce_len_maxE"></a>

    <a id="_CPPv3N20mst_comm_updata_para10ce_len_maxE"></a> <a id="_CPPv2N20mst_comm_updata_para10ce_len_maxE"></a> <a id="mst_comm_updata_para::ce_len_max__uint16_t"></a> <a id="structmst__comm__updata__para_1a3f87e250d9bb8e337ef8a717d382b30d"></a> uint16\_t ce\_len\_max
    :   Maximum Connection Event Duration.

    <a id="_CPPv4N20mst_comm_updata_para8intv_minE"></a>

    <a id="_CPPv3N20mst_comm_updata_para8intv_minE"></a> <a id="_CPPv2N20mst_comm_updata_para8intv_minE"></a> <a id="mst_comm_updata_para::intv_min__uint16_t"></a> <a id="structmst__comm__updata__para_1aca468e10620cf89651108256681c0ccf"></a> uint16\_t intv\_min
    :   Connection interval minimum.

    <a id="_CPPv4N20mst_comm_updata_para8intv_maxE"></a>

    <a id="_CPPv3N20mst_comm_updata_para8intv_maxE"></a> <a id="_CPPv2N20mst_comm_updata_para8intv_maxE"></a> <a id="mst_comm_updata_para::intv_max__uint16_t"></a> <a id="structmst__comm__updata__para_1a9fee9122ac2425d5117c3744f206c0b1"></a> uint16\_t intv\_max
    :   Connection interval maximum.

    <a id="_CPPv4N20mst_comm_updata_para7latencyE"></a>

    <a id="_CPPv3N20mst_comm_updata_para7latencyE"></a> <a id="_CPPv2N20mst_comm_updata_para7latencyE"></a> <a id="mst_comm_updata_para::latency__uint16_t"></a> <a id="structmst__comm__updata__para_1a314f2629aa454c7f87a59ea66971cd9b"></a> uint16\_t latency
    :   Latency.

    <a id="_CPPv4N20mst_comm_updata_para8time_outE"></a>

    <a id="_CPPv3N20mst_comm_updata_para8time_outE"></a> <a id="_CPPv2N20mst_comm_updata_para8time_outE"></a> <a id="mst_comm_updata_para::time_out__uint16_t"></a> <a id="structmst__comm__updata__para_1ae3d4443a920e55371bde8a8e31b280d4"></a> uint16\_t time\_out
    :   Supervision timeout.

<a id="_CPPv421ble_adv_stopped_ind_t"></a>

<a id="_CPPv321ble_adv_stopped_ind_t"></a> <a id="_CPPv221ble_adv_stopped_ind_t"></a> <a id="ble_adv_stopped_ind_t"></a> <a id="structble__adv__stopped__ind__t"></a> struct ble\_adv\_stopped\_ind\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21ble_adv_stopped_ind_t7adv_idxE"></a>

    <a id="_CPPv3N21ble_adv_stopped_ind_t7adv_idxE"></a> <a id="_CPPv2N21ble_adv_stopped_ind_t7adv_idxE"></a> <a id="ble_adv_stopped_ind_t::adv_idx__uint8_t"></a> <a id="structble__adv__stopped__ind__t_1a08b3d5d954b333fc06c60cb3dc95f303"></a> uint8\_t adv\_idx
    :   The index of adv.

    <a id="_CPPv4N21ble_adv_stopped_ind_t6reasonE"></a>

    <a id="_CPPv3N21ble_adv_stopped_ind_t6reasonE"></a> <a id="_CPPv2N21ble_adv_stopped_ind_t6reasonE"></a> <a id="ble_adv_stopped_ind_t::reason__uint8_t"></a> <a id="structble__adv__stopped__ind__t_1ae8282158810d42ca62487af566e06774"></a> uint8\_t reason
    :   the stopped reason,0:adv is stopped by user stop or link establishment;1:adv is stopped by timeout

    <a id="_CPPv4N21ble_adv_stopped_ind_t8conn_idxE"></a>

    <a id="_CPPv3N21ble_adv_stopped_ind_t8conn_idxE"></a> <a id="_CPPv2N21ble_adv_stopped_ind_t8conn_idxE"></a> <a id="ble_adv_stopped_ind_t::conn_idx__uint8_t"></a> <a id="structble__adv__stopped__ind__t_1a67d9fc00a872c97fa23529b930d5bbfa"></a> uint8\_t conn\_idx
    :   the index of connection established (valid when adv stopped due to link establishment)

<a id="_CPPv422ble_scan_stopped_ind_t"></a>

<a id="_CPPv322ble_scan_stopped_ind_t"></a> <a id="_CPPv222ble_scan_stopped_ind_t"></a> <a id="ble_scan_stopped_ind_t"></a> <a id="structble__scan__stopped__ind__t"></a> struct ble\_scan\_stopped\_ind\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22ble_scan_stopped_ind_t8scan_idxE"></a>

    <a id="_CPPv3N22ble_scan_stopped_ind_t8scan_idxE"></a> <a id="_CPPv2N22ble_scan_stopped_ind_t8scan_idxE"></a> <a id="ble_scan_stopped_ind_t::scan_idx__uint8_t"></a> <a id="structble__scan__stopped__ind__t_1aed5a00f701227a2e315621067cd018bd"></a> uint8\_t scan\_idx
    :   The index of scan.

    <a id="_CPPv4N22ble_scan_stopped_ind_t6reasonE"></a>

    <a id="_CPPv3N22ble_scan_stopped_ind_t6reasonE"></a> <a id="_CPPv2N22ble_scan_stopped_ind_t6reasonE"></a> <a id="ble_scan_stopped_ind_t::reason__uint8_t"></a> <a id="structble__scan__stopped__ind__t_1a1f83149967968a9f3f353ad014fad00d"></a> uint8\_t reason
    :   the stopped reason,0:scan is stopped by user stop;1:scan is stopped by timeout

<a id="_CPPv419ble_read_rssi_rsp_t"></a>

<a id="_CPPv319ble_read_rssi_rsp_t"></a> <a id="_CPPv219ble_read_rssi_rsp_t"></a> <a id="ble_read_rssi_rsp_t"></a> <a id="structble__read__rssi__rsp__t"></a> struct ble\_read\_rssi\_rsp\_t
:   BLE\_5\_READ\_RSSI\_CMPL\_EVENT data.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N19ble_read_rssi_rsp_t8conn_idxE"></a>

    <a id="_CPPv3N19ble_read_rssi_rsp_t8conn_idxE"></a> <a id="_CPPv2N19ble_read_rssi_rsp_t8conn_idxE"></a> <a id="ble_read_rssi_rsp_t::conn_idx__uint8_t"></a> <a id="structble__read__rssi__rsp__t_1a77e37c24f1efd6f62479f47ef6b7b070"></a> uint8\_t conn\_idx
    :   The index of connection.

    <a id="_CPPv4N19ble_read_rssi_rsp_t4rssiE"></a>

    <a id="_CPPv3N19ble_read_rssi_rsp_t4rssiE"></a> <a id="_CPPv2N19ble_read_rssi_rsp_t4rssiE"></a> <a id="ble_read_rssi_rsp_t::rssi__int8_t"></a> <a id="structble__read__rssi__rsp__t_1a66cd9f9cf444bbdec7aa766e84843ad1"></a> int8\_t rssi
    :   RSSI value.

<a id="_CPPv417bk_ble_enc_keys_t"></a>

<a id="_CPPv317bk_ble_enc_keys_t"></a> <a id="_CPPv217bk_ble_enc_keys_t"></a> <a id="bk_ble_enc_keys_t"></a> <a id="structbk__ble__enc__keys__t"></a> struct bk\_ble\_enc\_keys\_t
:   BLE encryption keys.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_ble_enc_keys_t3ltkE"></a>

    <a id="_CPPv3N17bk_ble_enc_keys_t3ltkE"></a> <a id="_CPPv2N17bk_ble_enc_keys_t3ltkE"></a> <a id="bk_ble_enc_keys_t::ltk__uint8_tA"></a> <a id="structbk__ble__enc__keys__t_1abfcbca1e448a26e6eeef882a8f6985f5"></a> uint8\_t ltk\[16\]
    :   The long term key

    <a id="_CPPv4N17bk_ble_enc_keys_t4randE"></a>

    <a id="_CPPv3N17bk_ble_enc_keys_t4randE"></a> <a id="_CPPv2N17bk_ble_enc_keys_t4randE"></a> <a id="bk_ble_enc_keys_t::rand__uint8_tA"></a> <a id="structbk__ble__enc__keys__t_1a8d2c0057e3e33fde64e76b7cabf3900e"></a> uint8\_t rand\[8\]
    :   The random number

    <a id="_CPPv4N17bk_ble_enc_keys_t4edivE"></a>

    <a id="_CPPv3N17bk_ble_enc_keys_t4edivE"></a> <a id="_CPPv2N17bk_ble_enc_keys_t4edivE"></a> <a id="bk_ble_enc_keys_t::ediv__uint16_t"></a> <a id="structbk__ble__enc__keys__t_1afbcc8648ec3b558836d9a36ffe6c85fc"></a> uint16\_t ediv
    :   The ediv value

    <a id="_CPPv4N17bk_ble_enc_keys_t8key_sizeE"></a>

    <a id="_CPPv3N17bk_ble_enc_keys_t8key_sizeE"></a> <a id="_CPPv2N17bk_ble_enc_keys_t8key_sizeE"></a> <a id="bk_ble_enc_keys_t::key_size__uint8_t"></a> <a id="structbk__ble__enc__keys__t_1aa316e02b877049307de30f6636812a7b"></a> uint8\_t key\_size
    :   The key size(7\~16) of the security link

<a id="_CPPv417bk_ble_irk_info_t"></a>

<a id="_CPPv317bk_ble_irk_info_t"></a> <a id="_CPPv217bk_ble_irk_info_t"></a> <a id="bk_ble_irk_info_t"></a> <a id="structbk__ble__irk__info__t"></a> struct bk\_ble\_irk\_info\_t
:   BLE irk info.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17bk_ble_irk_info_t3irkE"></a>

    <a id="_CPPv3N17bk_ble_irk_info_t3irkE"></a> <a id="_CPPv2N17bk_ble_irk_info_t3irkE"></a> <a id="bk_ble_irk_info_t::irk__uint8_tA"></a> <a id="structbk__ble__irk__info__t_1ae65313c99fc658ab24b1f41cb7de9c2a"></a> uint8\_t irk\[16\]
    :   The irk value

    <a id="_CPPv4N17bk_ble_irk_info_t9addr_typeE"></a>

    <a id="_CPPv3N17bk_ble_irk_info_t9addr_typeE"></a> <a id="_CPPv2N17bk_ble_irk_info_t9addr_typeE"></a> <a id="bk_ble_irk_info_t::addr_type__uint8_t"></a> <a id="structbk__ble__irk__info__t_1ae05b95631fc1b2d6c2797f9166b2c595"></a> uint8\_t addr\_type
    :   The address type

    <a id="_CPPv4N17bk_ble_irk_info_t7id_addrE"></a>

    <a id="_CPPv3N17bk_ble_irk_info_t7id_addrE"></a> <a id="_CPPv2N17bk_ble_irk_info_t7id_addrE"></a> <a id="bk_ble_irk_info_t::id_addr__uint8_tA"></a> <a id="structbk__ble__irk__info__t_1af7fa1dd2a7fdfda6ad567e193b5d3d61"></a> uint8\_t id\_addr\[6\]
    :   The Identity address

<a id="_CPPv412bk_ble_key_t"></a>

<a id="_CPPv312bk_ble_key_t"></a> <a id="_CPPv212bk_ble_key_t"></a> <a id="bk_ble_key_t"></a> <a id="structbk__ble__key__t"></a> struct bk\_ble\_key\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12bk_ble_key_t14peer_addr_typeE"></a>

    <a id="_CPPv3N12bk_ble_key_t14peer_addr_typeE"></a> <a id="_CPPv2N12bk_ble_key_t14peer_addr_typeE"></a> <a id="bk_ble_key_t::peer_addr_type__uint8_t"></a> <a id="structbk__ble__key__t_1a94eef1aec4e0ed3112c7637cdec11392"></a> uint8\_t peer\_addr\_type
    :   Peer address type.

    <a id="_CPPv4N12bk_ble_key_t9peer_addrE"></a>

    <a id="_CPPv3N12bk_ble_key_t9peer_addrE"></a> <a id="_CPPv2N12bk_ble_key_t9peer_addrE"></a> <a id="bk_ble_key_t::peer_addr__uint8_tA"></a> <a id="structbk__ble__key__t_1ab06b92bf96ee61e3517156a31fc519c2"></a> uint8\_t peer\_addr\[6\]
    :   Peer address.

    <a id="_CPPv4N12bk_ble_key_t4authE"></a>

    <a id="_CPPv3N12bk_ble_key_t4authE"></a> <a id="_CPPv2N12bk_ble_key_t4authE"></a> <a id="bk_ble_key_t::auth__uint8_t"></a> <a id="structbk__ble__key__t_1ae7eb349108077ef53990fdf475418d20"></a> uint8\_t auth
    :   Authentication level.

    <a id="_CPPv4N12bk_ble_key_t4pencE"></a>

    <a id="_CPPv3N12bk_ble_key_t4pencE"></a> <a id="_CPPv2N12bk_ble_key_t4pencE"></a> <a id="bk_ble_key_t::penc__bk_ble_enc_keys_t"></a> <a id="structbk__ble__key__t_1a60fd9ce633b2725f3d6e3e7a2132158a"></a> [bk\_ble\_enc\_keys\_t](#_CPPv417bk_ble_enc_keys_t "bk_ble_enc_keys_t") penc
    :   received peer encryption key

    <a id="_CPPv4N12bk_ble_key_t4lencE"></a>

    <a id="_CPPv3N12bk_ble_key_t4lencE"></a> <a id="_CPPv2N12bk_ble_key_t4lencE"></a> <a id="bk_ble_key_t::lenc__bk_ble_enc_keys_t"></a> <a id="structbk__ble__key__t_1a757fbcc0528c0feb538ec1c564cab6c3"></a> [bk\_ble\_enc\_keys\_t](#_CPPv417bk_ble_enc_keys_t "bk_ble_enc_keys_t") lenc
    :   local encryption key

    <a id="_CPPv4N12bk_ble_key_t4pirkE"></a>

    <a id="_CPPv3N12bk_ble_key_t4pirkE"></a> <a id="_CPPv2N12bk_ble_key_t4pirkE"></a> <a id="bk_ble_key_t::pirk__bk_ble_irk_info_t"></a> <a id="structbk__ble__key__t_1a9696d35b1616f1c7cfec05575553bab1"></a> [bk\_ble\_irk\_info\_t](#_CPPv417bk_ble_irk_info_t "bk_ble_irk_info_t") pirk
    :   peer Identity Resolving Key information

<a id="_CPPv422bk_ble_bond_info_req_t"></a>

<a id="_CPPv322bk_ble_bond_info_req_t"></a> <a id="_CPPv222bk_ble_bond_info_req_t"></a> <a id="bk_ble_bond_info_req_t"></a> <a id="structbk__ble__bond__info__req__t"></a> struct bk\_ble\_bond\_info\_req\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22bk_ble_bond_info_req_t9key_foundE"></a>

    <a id="_CPPv3N22bk_ble_bond_info_req_t9key_foundE"></a> <a id="_CPPv2N22bk_ble_bond_info_req_t9key_foundE"></a> <a id="bk_ble_bond_info_req_t::key_found__uint8_t"></a> <a id="structbk__ble__bond__info__req__t_1a25ad2d0cef34ae1af9a21d58d5096a12"></a> uint8\_t key\_found
    :   check whether key is found

<a id="_CPPv421bk_ble_gatt_cmp_evt_t"></a>

<a id="_CPPv321bk_ble_gatt_cmp_evt_t"></a> <a id="_CPPv221bk_ble_gatt_cmp_evt_t"></a> <a id="bk_ble_gatt_cmp_evt_t"></a> <a id="structbk__ble__gatt__cmp__evt__t"></a> struct bk\_ble\_gatt\_cmp\_evt\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21bk_ble_gatt_cmp_evt_t9operationE"></a>

    <a id="_CPPv3N21bk_ble_gatt_cmp_evt_t9operationE"></a> <a id="_CPPv2N21bk_ble_gatt_cmp_evt_t9operationE"></a> <a id="bk_ble_gatt_cmp_evt_t::operation__uint8_t"></a> <a id="structbk__ble__gatt__cmp__evt__t_1a4f1c7ab4087e69ab38efbc01defb4ec7"></a> uint8\_t operation
    :   GATT request type.

    <a id="_CPPv4N21bk_ble_gatt_cmp_evt_t6statusE"></a>

    <a id="_CPPv3N21bk_ble_gatt_cmp_evt_t6statusE"></a> <a id="_CPPv2N21bk_ble_gatt_cmp_evt_t6statusE"></a> <a id="bk_ble_gatt_cmp_evt_t::status__uint8_t"></a> <a id="structbk__ble__gatt__cmp__evt__t_1ab6f669e9b0ff3b4cbeed97bb85856c86"></a> uint8\_t status
    :   Status of the request.

    <a id="_CPPv4N21bk_ble_gatt_cmp_evt_t6prf_idE"></a>

    <a id="_CPPv3N21bk_ble_gatt_cmp_evt_t6prf_idE"></a> <a id="_CPPv2N21bk_ble_gatt_cmp_evt_t6prf_idE"></a> <a id="bk_ble_gatt_cmp_evt_t::prf_id__uint16_t"></a> <a id="structbk__ble__gatt__cmp__evt__t_1aefce1670fd67a48b0cddf1959faff1a8"></a> uint16\_t prf\_id
    :   service id

    <a id="_CPPv4N21bk_ble_gatt_cmp_evt_t6att_idE"></a>

    <a id="_CPPv3N21bk_ble_gatt_cmp_evt_t6att_idE"></a> <a id="_CPPv2N21bk_ble_gatt_cmp_evt_t6att_idE"></a> <a id="bk_ble_gatt_cmp_evt_t::att_id__uint16_t"></a> <a id="structbk__ble__gatt__cmp__evt__t_1af31bd0dca8d56bb142027a40683d3570"></a> uint16\_t att\_id
    :   attribute id

    <a id="_CPPv4N21bk_ble_gatt_cmp_evt_t8conn_idxE"></a>

    <a id="_CPPv3N21bk_ble_gatt_cmp_evt_t8conn_idxE"></a> <a id="_CPPv2N21bk_ble_gatt_cmp_evt_t8conn_idxE"></a> <a id="bk_ble_gatt_cmp_evt_t::conn_idx__uint8_t"></a> <a id="structbk__ble__gatt__cmp__evt__t_1a1e3f6db035c7b3c061e11e62d3906208"></a> uint8\_t conn\_idx
    :   connection index

<a id="_CPPv418ble_loc_oob_data_t"></a>

<a id="_CPPv318ble_loc_oob_data_t"></a> <a id="_CPPv218ble_loc_oob_data_t"></a> <a id="ble_loc_oob_data_t"></a> <a id="structble__loc__oob__data__t"></a> struct ble\_loc\_oob\_data\_t
:   BLE\_5\_SC\_LOC\_OOB\_IND data.

    <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18ble_loc_oob_data_t8conn_idxE"></a>

    <a id="_CPPv3N18ble_loc_oob_data_t8conn_idxE"></a> <a id="_CPPv2N18ble_loc_oob_data_t8conn_idxE"></a> <a id="ble_loc_oob_data_t::conn_idx__uint8_t"></a> <a id="structble__loc__oob__data__t_1af595c4058eb3b55036e6c89ebab710fa"></a> uint8\_t conn\_idx
    :   The index of connection.

    <a id="_CPPv4N18ble_loc_oob_data_t11local_oob_cE"></a>

    <a id="_CPPv3N18ble_loc_oob_data_t11local_oob_cE"></a> <a id="_CPPv2N18ble_loc_oob_data_t11local_oob_cE"></a> <a id="ble_loc_oob_data_t::local_oob_c__uint8_tA"></a> <a id="structble__loc__oob__data__t_1a6b2e18364a7046f15e6ee08ceb687fae"></a> uint8\_t local\_oob\_c\[16\]
    :   Local OOB Data Confirmation/Commitment.

    <a id="_CPPv4N18ble_loc_oob_data_t11local_oob_rE"></a>

    <a id="_CPPv3N18ble_loc_oob_data_t11local_oob_rE"></a> <a id="_CPPv2N18ble_loc_oob_data_t11local_oob_rE"></a> <a id="ble_loc_oob_data_t::local_oob_r__uint8_tA"></a> <a id="structble__loc__oob__data__t_1a2f4588d14870b08ac6aadea2b36d2da5"></a> uint8\_t local\_oob\_r\[16\]
    :   Local OOB Data Randomizer.

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_BLE_SUCCESS"></a>

<a id="group__bk__ble__api__v1_1ga081979d9071f263e708969a25b0a9d07"></a> BK\_ERR\_BLE\_SUCCESS
:   success

<a id="c.BK_ERR_BLE_FAIL"></a>

<a id="group__bk__ble__api__v1_1gad00f606f99bcdd8a940e2e6bbfef6d3c"></a> BK\_ERR\_BLE\_FAIL
:   fail

<a id="c.BK_ERR_BLE_NO_MEM"></a>

<a id="group__bk__ble__api__v1_1gac22ab18e83a2472f6b3bc75b2b3c0968"></a> BK\_ERR\_BLE\_NO\_MEM
:   no mem

<a id="c.BK_ERR_BLE_PROFILE"></a>

<a id="group__bk__ble__api__v1_1ga417d140f9bf91159e14c609f953593ac"></a> BK\_ERR\_BLE\_PROFILE
:   profile err

<a id="c.BK_ERR_BLE_CREATE_DB"></a>

<a id="group__bk__ble__api__v1_1ga7184d63fc78c9f2dd944281b263a9292"></a> BK\_ERR\_BLE\_CREATE\_DB
:   bk\_ble\_create\_db err

<a id="c.BK_ERR_BLE_CMD_NOT_SUPPORT"></a>

<a id="group__bk__ble__api__v1_1gafe155fd3e34200c3dc1ed76dd3a56475"></a> BK\_ERR\_BLE\_CMD\_NOT\_SUPPORT
:   unknow cmd err

<a id="c.BK_ERR_BLE_UNKNOW_IDX"></a>

<a id="group__bk__ble__api__v1_1gad46c25ca7786a81b8c0816716f9cff07"></a> BK\_ERR\_BLE\_UNKNOW\_IDX
:   index err, suchas conn\_ind

<a id="c.BK_ERR_BLE_BLE_STATUS"></a>

<a id="group__bk__ble__api__v1_1ga3a7c17a33464079ddf58e0aba6e766e5"></a> BK\_ERR\_BLE\_BLE\_STATUS
:   ble status not match

<a id="c.BK_ERR_BLE_ADV_DATA"></a>

<a id="group__bk__ble__api__v1_1gaca1266cf2089898726e8270d1e8376c7"></a> BK\_ERR\_BLE\_ADV\_DATA
:   adv data err, such as too long

<a id="c.BK_ERR_BLE_CMD_RUN"></a>

<a id="group__bk__ble__api__v1_1ga1c7dbaeeee7fe1691bcd7d2d4aa67a2b"></a> BK\_ERR\_BLE\_CMD\_RUN
:   cmd run err

<a id="c.BK_ERR_BLE_INIT_CREATE"></a>

<a id="group__bk__ble__api__v1_1gac982525fa3f88935fae8cadcb5dfa4a3"></a> BK\_ERR\_BLE\_INIT\_CREATE
:   create init err, such as bk\_ble\_create\_init

<a id="c.BK_ERR_BLE_INIT_STATE"></a>

<a id="group__bk__ble__api__v1_1ga294839cec2a404230984f2333ce38b1c"></a> BK\_ERR\_BLE\_INIT\_STATE
:   current init status not match

<a id="c.BK_ERR_BLE_ATTC_WRITE"></a>

<a id="group__bk__ble__api__v1_1gab5ec291b766d4436cc27ad2843b616dc"></a> BK\_ERR\_BLE\_ATTC\_WRITE
:   att write err

<a id="c.BK_ERR_BLE_ATTC_WRITE_UNREGISTER"></a>

<a id="group__bk__ble__api__v1_1ga12009758a11d77482c0ee14e9403e997"></a> BK\_ERR\_BLE\_ATTC\_WRITE\_UNREGISTER
:   att handle is not regist

<a id="c.BK_BLE_MAX_ADV_DATA_LEN"></a>

<a id="group__bk__ble__api__v1_1ga89718ba447b76d92120a318754cf253b"></a> BK\_BLE\_MAX\_ADV\_DATA\_LEN
:   max ble adv data len

<a id="c.BK_BLE_GAP_BD_ADDR_LEN"></a>

<a id="group__bk__ble__api__v1_1gaea4b7b2187d942384b18bf2f4b607223"></a> BK\_BLE\_GAP\_BD\_ADDR\_LEN
:   BD address length.

<a id="c.BK_BLE_APP_DEVICE_NAME_MAX_LEN"></a>

<a id="group__bk__ble__api__v1_1ga1e8c921e258212da6460840aa4301fda"></a> BK\_BLE\_APP\_DEVICE\_NAME\_MAX\_LEN
:   Maximal length of the Device Name value.

<a id="c.BK_BLE_PERM_SET"></a>

<a id="group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b"></a> BK\_BLE\_PERM\_SET(access, right)
:   for [ble\_attm\_desc\_t](#structble__attm__desc__t), build database perm,

<a id="c.BK_BLE_PERM_GET"></a>

<a id="group__bk__ble__api__v1_1gae03690e23cd26e504a15bf4b93337d5e"></a> BK\_BLE\_PERM\_GET(perm, access)

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv49ble_err_t"></a>

<a id="_CPPv39ble_err_t"></a> <a id="_CPPv29ble_err_t"></a> <a id="ble_err_t"></a> <a id="group__bk__ble__api__v1_1ga3358a7925e0da86de797cf98ad5c878e"></a> typedef [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") ble\_err\_t
:   ble api return enum

<a id="_CPPv416app_sdp_callback"></a>

<a id="_CPPv316app_sdp_callback"></a> <a id="_CPPv216app_sdp_callback"></a> <a id="app_sdp_callback"></a> <a id="group__bk__ble__api__v1_1gae5e8f654ec22353f88ae802c5e68b582"></a> typedef void (\*app\_sdp\_callback)(unsigned char conidx, uint16\_t chars\_val\_hdl, unsigned char uuid\_len, unsigned char \*uuid)

<a id="_CPPv423app_sdp_charac_callback"></a>

<a id="_CPPv323app_sdp_charac_callback"></a> <a id="_CPPv223app_sdp_charac_callback"></a> <a id="app_sdp_charac_callback"></a> <a id="group__bk__ble__api__v1_1gae9875a9a5e0213d69298803a737021f9"></a> typedef void (\*app\_sdp\_charac\_callback)([CHAR\_TYPE](#_CPPv49CHAR_TYPE "CHAR_TYPE") type, uint8 conidx, uint16\_t hdl, uint16\_t len, uint8 \*data)

<a id="_CPPv421app_sdp_comm_callback"></a>

<a id="_CPPv321app_sdp_comm_callback"></a> <a id="_CPPv221app_sdp_comm_callback"></a> <a id="app_sdp_comm_callback"></a> <a id="group__bk__ble__api__v1_1ga208b68fba77b926cd23c708523a782f4"></a> typedef void (\*app\_sdp\_comm\_callback)([MASTER\_COMMON\_TYPE](#_CPPv418MASTER_COMMON_TYPE "MASTER_COMMON_TYPE") type, uint8 conidx, void \*param)

<a id="_CPPv412ble_cmd_cb_t"></a>

<a id="_CPPv312ble_cmd_cb_t"></a> <a id="_CPPv212ble_cmd_cb_t"></a> <a id="ble_cmd_cb_t"></a> <a id="group__bk__ble__api__v1__typedef_1ga8748e603749159a8f60c549bb387f886"></a> typedef void (\*ble\_cmd\_cb\_t)([ble\_cmd\_t](#_CPPv49ble_cmd_t "ble_cmd_t") cmd, [ble\_cmd\_param\_t](#_CPPv415ble_cmd_param_t "ble_cmd_param_t") \*param)
:   for sync ble api call return

    most ble api have ble\_cmd\_cb\_t param, you must wait is callback.

    Param \-
    :   cmd: cmd id.

        - param: param

<a id="_CPPv415ble_notice_cb_t"></a>

<a id="_CPPv315ble_notice_cb_t"></a> <a id="_CPPv215ble_notice_cb_t"></a> <a id="ble_notice_cb_t"></a> <a id="group__bk__ble__api__v1__typedef_1ga6da7ef3abb3e483c1a3d109a55720964"></a> typedef void (\*ble\_notice\_cb\_t)([ble\_notice\_t](#_CPPv412ble_notice_t "ble_notice_t") notice, void \*param)
:   for async ble api event.

    ble event report.

    Param \-
    :   notice: event id.

        - param: param

<a id="_CPPv418ble_hci_to_host_cb"></a>

<a id="_CPPv318ble_hci_to_host_cb"></a> <a id="_CPPv218ble_hci_to_host_cb"></a> <a id="ble_hci_to_host_cb"></a> <a id="group__bk__ble__api__v1__typedef_1gacce5539c67afa8131c5913a9512d4252"></a> typedef [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") (\*ble\_hci\_to\_host\_cb)(uint8\_t \*buf, uint16\_t len)
:   for hci callback.

    stack report evt, acl to upper

    Param \-
    :   buf: payload

        - len: buf’s len

    Return
    :   - BK\_ERR\_BLE\_SUCCESS: succeed

<a id="_CPPv416ble_hci_to_cp_cb"></a>

<a id="_CPPv316ble_hci_to_cp_cb"></a> <a id="_CPPv216ble_hci_to_cp_cb"></a> <a id="ble_hci_to_cp_cb"></a> <a id="group__bk__ble__api__v1__typedef_1gabeaaf7b6e64aa6adf81d09b8eac5f6aa"></a> typedef [ble\_err\_t](#_CPPv49ble_err_t "ble_err_t") (\*ble\_hci\_to\_cp\_cb)(uint8\_t \*buf, uint16\_t len)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv428BK_BLE_CONTROLLER_STACK_TYPE"></a>

<a id="_CPPv328BK_BLE_CONTROLLER_STACK_TYPE"></a> <a id="_CPPv228BK_BLE_CONTROLLER_STACK_TYPE"></a> <a id="group__bk__ble__api__v1_1gadebabc09c1f14686ca765cf16ed7ee10"></a> enum BK\_BLE\_CONTROLLER\_STACK\_TYPE
:   *Values:*

    <a id="_CPPv4N28BK_BLE_CONTROLLER_STACK_TYPE34BK_BLE_CONTROLLER_STACK_TYPE_BLE_4E"></a>

    <a id="_CPPv3N28BK_BLE_CONTROLLER_STACK_TYPE34BK_BLE_CONTROLLER_STACK_TYPE_BLE_4E"></a> <a id="_CPPv2N28BK_BLE_CONTROLLER_STACK_TYPE34BK_BLE_CONTROLLER_STACK_TYPE_BLE_4E"></a> <a id="group__bk__ble__api__v1_1ggadebabc09c1f14686ca765cf16ed7ee10af1a420a7192790e7d01b3d9fd0c0e31a"></a> enumerator BK\_BLE\_CONTROLLER\_STACK\_TYPE\_BLE\_4

    <a id="_CPPv4N28BK_BLE_CONTROLLER_STACK_TYPE36BK_BLE_CONTROLLER_STACK_TYPE_BLE_5_XE"></a>

    <a id="_CPPv3N28BK_BLE_CONTROLLER_STACK_TYPE36BK_BLE_CONTROLLER_STACK_TYPE_BLE_5_XE"></a> <a id="_CPPv2N28BK_BLE_CONTROLLER_STACK_TYPE36BK_BLE_CONTROLLER_STACK_TYPE_BLE_5_XE"></a> <a id="group__bk__ble__api__v1_1ggadebabc09c1f14686ca765cf16ed7ee10a54673346abd20a6d105883505a574b98"></a> enumerator BK\_BLE\_CONTROLLER\_STACK\_TYPE\_BLE\_5\_X

    <a id="_CPPv4N28BK_BLE_CONTROLLER_STACK_TYPE37BK_BLE_CONTROLLER_STACK_TYPE_BTDM_5_2E"></a>

    <a id="_CPPv3N28BK_BLE_CONTROLLER_STACK_TYPE37BK_BLE_CONTROLLER_STACK_TYPE_BTDM_5_2E"></a> <a id="_CPPv2N28BK_BLE_CONTROLLER_STACK_TYPE37BK_BLE_CONTROLLER_STACK_TYPE_BTDM_5_2E"></a> <a id="group__bk__ble__api__v1_1ggadebabc09c1f14686ca765cf16ed7ee10aeaffb69b63e0d7b78d4c7fe05838edf8"></a> enumerator BK\_BLE\_CONTROLLER\_STACK\_TYPE\_BTDM\_5\_2

<a id="_CPPv422BK_BLE_HOST_STACK_TYPE"></a>

<a id="_CPPv322BK_BLE_HOST_STACK_TYPE"></a> <a id="_CPPv222BK_BLE_HOST_STACK_TYPE"></a> <a id="group__bk__ble__api__v1_1ga4b5ac5d4250839875c2633fe296e396e"></a> enum BK\_BLE\_HOST\_STACK\_TYPE
:   *Values:*

    <a id="_CPPv4N22BK_BLE_HOST_STACK_TYPE27BK_BLE_HOST_STACK_TYPE_RW_4E"></a>

    <a id="_CPPv3N22BK_BLE_HOST_STACK_TYPE27BK_BLE_HOST_STACK_TYPE_RW_4E"></a> <a id="_CPPv2N22BK_BLE_HOST_STACK_TYPE27BK_BLE_HOST_STACK_TYPE_RW_4E"></a> <a id="group__bk__ble__api__v1_1gga4b5ac5d4250839875c2633fe296e396eadbf620d83af7c90c11406db28578518b"></a> enumerator BK\_BLE\_HOST\_STACK\_TYPE\_RW\_4

    <a id="_CPPv4N22BK_BLE_HOST_STACK_TYPE29BK_BLE_HOST_STACK_TYPE_RW_5_XE"></a>

    <a id="_CPPv3N22BK_BLE_HOST_STACK_TYPE29BK_BLE_HOST_STACK_TYPE_RW_5_XE"></a> <a id="_CPPv2N22BK_BLE_HOST_STACK_TYPE29BK_BLE_HOST_STACK_TYPE_RW_5_XE"></a> <a id="group__bk__ble__api__v1_1gga4b5ac5d4250839875c2633fe296e396ea6cdadfd5a12a3f22222d73c88fc93d1c"></a> enumerator BK\_BLE\_HOST\_STACK\_TYPE\_RW\_5\_X

    <a id="_CPPv4N22BK_BLE_HOST_STACK_TYPE29BK_BLE_HOST_STACK_TYPE_RW_5_2E"></a>

    <a id="_CPPv3N22BK_BLE_HOST_STACK_TYPE29BK_BLE_HOST_STACK_TYPE_RW_5_2E"></a> <a id="_CPPv2N22BK_BLE_HOST_STACK_TYPE29BK_BLE_HOST_STACK_TYPE_RW_5_2E"></a> <a id="group__bk__ble__api__v1_1gga4b5ac5d4250839875c2633fe296e396ea6b6ce980ea05293faa37ef3bc97ff653"></a> enumerator BK\_BLE\_HOST\_STACK\_TYPE\_RW\_5\_2

    <a id="_CPPv4N22BK_BLE_HOST_STACK_TYPE32BK_BLE_HOST_STACK_TYPE_ETHERMINDE"></a>

    <a id="_CPPv3N22BK_BLE_HOST_STACK_TYPE32BK_BLE_HOST_STACK_TYPE_ETHERMINDE"></a> <a id="_CPPv2N22BK_BLE_HOST_STACK_TYPE32BK_BLE_HOST_STACK_TYPE_ETHERMINDE"></a> <a id="group__bk__ble__api__v1_1gga4b5ac5d4250839875c2633fe296e396ea19cb02c85924c35ad72853fa94ae1622"></a> enumerator BK\_BLE\_HOST\_STACK\_TYPE\_ETHERMIND

<a id="_CPPv415BK_BLE_HCI_TYPE"></a>

<a id="_CPPv315BK_BLE_HCI_TYPE"></a> <a id="_CPPv215BK_BLE_HCI_TYPE"></a> <a id="group__bk__ble__api__v1_1ga28e61788890c70b81bec53fc9a5ea22c"></a> enum BK\_BLE\_HCI\_TYPE
:   hci type enum

    *Values:*

    <a id="_CPPv4N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_CMDE"></a>

    <a id="_CPPv3N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_CMDE"></a> <a id="_CPPv2N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_CMDE"></a> <a id="group__bk__ble__api__v1_1gga28e61788890c70b81bec53fc9a5ea22caf40ea31e4569058c5962a5897cb1c1b3"></a> enumerator BK\_BLE\_HCI\_TYPE\_CMD

    <a id="_CPPv4N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_ACLE"></a>

    <a id="_CPPv3N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_ACLE"></a> <a id="_CPPv2N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_ACLE"></a> <a id="group__bk__ble__api__v1_1gga28e61788890c70b81bec53fc9a5ea22cab62feafcb11f987813e1af652a149c7a"></a> enumerator BK\_BLE\_HCI\_TYPE\_ACL

    <a id="_CPPv4N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_SCOE"></a>

    <a id="_CPPv3N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_SCOE"></a> <a id="_CPPv2N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_SCOE"></a> <a id="group__bk__ble__api__v1_1gga28e61788890c70b81bec53fc9a5ea22ca1f25d213e298fc45cc141a2dc316ca27"></a> enumerator BK\_BLE\_HCI\_TYPE\_SCO

    <a id="_CPPv4N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_EVTE"></a>

    <a id="_CPPv3N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_EVTE"></a> <a id="_CPPv2N15BK_BLE_HCI_TYPE19BK_BLE_HCI_TYPE_EVTE"></a> <a id="group__bk__ble__api__v1_1gga28e61788890c70b81bec53fc9a5ea22ca49bb45c98e664aac984eb6115fa9a7b1"></a> enumerator BK\_BLE\_HCI\_TYPE\_EVT

<a id="_CPPv414ble_actv_state"></a>

<a id="_CPPv314ble_actv_state"></a> <a id="_CPPv214ble_actv_state"></a> <a id="group__bk__ble__api__v1_1gaaa02b94e7c27fcf23e3f6f2c8064df7c"></a> enum ble\_actv\_state
:   ble actv type

    *Values:*

    <a id="_CPPv4N14ble_actv_state13BLE_ACTV_IDLEE"></a>

    <a id="_CPPv3N14ble_actv_state13BLE_ACTV_IDLEE"></a> <a id="_CPPv2N14ble_actv_state13BLE_ACTV_IDLEE"></a> <a id="group__bk__ble__api__v1_1ggaaa02b94e7c27fcf23e3f6f2c8064df7cacc3d4df066c5303ba17e488d6ec32391"></a> enumerator BLE\_ACTV\_IDLE

    <a id="_CPPv4N14ble_actv_state20BLE_ACTV_ADV_CREATEDE"></a>

    <a id="_CPPv3N14ble_actv_state20BLE_ACTV_ADV_CREATEDE"></a> <a id="_CPPv2N14ble_actv_state20BLE_ACTV_ADV_CREATEDE"></a> <a id="group__bk__ble__api__v1_1ggaaa02b94e7c27fcf23e3f6f2c8064df7ca28c3e9b2c3ef021fe7c1e7165699ce73"></a> enumerator BLE\_ACTV\_ADV\_CREATED

    <a id="_CPPv4N14ble_actv_state20BLE_ACTV_ADV_STARTEDE"></a>

    <a id="_CPPv3N14ble_actv_state20BLE_ACTV_ADV_STARTEDE"></a> <a id="_CPPv2N14ble_actv_state20BLE_ACTV_ADV_STARTEDE"></a> <a id="group__bk__ble__api__v1_1ggaaa02b94e7c27fcf23e3f6f2c8064df7ca887345ad2348693920c57bd665f45a0d"></a> enumerator BLE\_ACTV\_ADV\_STARTED

    <a id="_CPPv4N14ble_actv_state21BLE_ACTV_SCAN_CREATEDE"></a>

    <a id="_CPPv3N14ble_actv_state21BLE_ACTV_SCAN_CREATEDE"></a> <a id="_CPPv2N14ble_actv_state21BLE_ACTV_SCAN_CREATEDE"></a> <a id="group__bk__ble__api__v1_1ggaaa02b94e7c27fcf23e3f6f2c8064df7cab2b71e515de971346c2850e37a207d13"></a> enumerator BLE\_ACTV\_SCAN\_CREATED

    <a id="_CPPv4N14ble_actv_state21BLE_ACTV_SCAN_STARTEDE"></a>

    <a id="_CPPv3N14ble_actv_state21BLE_ACTV_SCAN_STARTEDE"></a> <a id="_CPPv2N14ble_actv_state21BLE_ACTV_SCAN_STARTEDE"></a> <a id="group__bk__ble__api__v1_1ggaaa02b94e7c27fcf23e3f6f2c8064df7ca8b318035b80c96e60fa886381961b1a9"></a> enumerator BLE\_ACTV\_SCAN\_STARTED

    <a id="_CPPv4N14ble_actv_state21BLE_ACTV_INIT_CREATEDE"></a>

    <a id="_CPPv3N14ble_actv_state21BLE_ACTV_INIT_CREATEDE"></a> <a id="_CPPv2N14ble_actv_state21BLE_ACTV_INIT_CREATEDE"></a> <a id="group__bk__ble__api__v1_1ggaaa02b94e7c27fcf23e3f6f2c8064df7ca71ea6a51f8a0b0ce28020ad9981933a7"></a> enumerator BLE\_ACTV\_INIT\_CREATED

    <a id="_CPPv4N14ble_actv_state25BLE_ACTV_PER_SYNC_CREATEDE"></a>

    <a id="_CPPv3N14ble_actv_state25BLE_ACTV_PER_SYNC_CREATEDE"></a> <a id="_CPPv2N14ble_actv_state25BLE_ACTV_PER_SYNC_CREATEDE"></a> <a id="group__bk__ble__api__v1_1ggaaa02b94e7c27fcf23e3f6f2c8064df7ca33ffd415f95b920f347d08a3e4c8eaf4"></a> enumerator BLE\_ACTV\_PER\_SYNC\_CREATED

    <a id="_CPPv4N14ble_actv_state25BLE_ACTV_PER_SYNC_STARTEDE"></a>

    <a id="_CPPv3N14ble_actv_state25BLE_ACTV_PER_SYNC_STARTEDE"></a> <a id="_CPPv2N14ble_actv_state25BLE_ACTV_PER_SYNC_STARTEDE"></a> <a id="group__bk__ble__api__v1_1ggaaa02b94e7c27fcf23e3f6f2c8064df7ca99a18b28bd100de07d67f3c06d6134ea"></a> enumerator BLE\_ACTV\_PER\_SYNC\_STARTED

<a id="_CPPv416bk_ble_perm_mask"></a>

<a id="_CPPv316bk_ble_perm_mask"></a> <a id="_CPPv216bk_ble_perm_mask"></a> <a id="group__bk__ble__api__v1_1gaa529f18ac0ecdf658b9e49c2fffc7f22"></a> enum bk\_ble\_perm\_mask
:   normal perm, for BK\_BLE\_PERM\_SET

    | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 \- 6 | 5 \- 4 | 3 \- 2 | 1 \- 0 |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | EXT | WS | I | N | WR | WC | RD | B | NP | IP | WP | RP |

    **Attention**
    :   you cant use this direct, use [BK\_BLE\_PERM\_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) instead

    Bit \[0-1\] : Read Permission (0 \= NO\_AUTH, 1 \= UNAUTH, 2 \= AUTH, 3 \= SEC\_CON)

    Bit \[2-3\] : Write Permission (0 \= NO\_AUTH, 1 \= UNAUTH, 2 \= AUTH, 3 \= SEC\_CON)

    Bit \[4-5\] : Indication Permission (0 \= NO\_AUTH, 1 \= UNAUTH, 2 \= AUTH, 3 \= SEC\_CON)

    Bit \[6-7\] : Notification Permission (0 \= NO\_AUTH, 1 \= UNAUTH, 2 \= AUTH, 3 \= SEC\_CON)

    Bit \[8\] : Broadcast permission

    Bit \[9\] : Read Command accepted

    Bit \[10\] : Write Command accepted

    Bit \[11\] : Write Request accepted

    Bit \[12\] : Send Notification

    Bit \[13\] : Send Indication

    Bit \[14\] : Write Signed accepted

    Bit \[15\] : Extended properties present

    *Values:*

    <a id="_CPPv4N16bk_ble_perm_mask14BK_BLE_RP_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask14BK_BLE_RP_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask14BK_BLE_RP_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a8db925c764699883032b59f18bb98abd"></a> enumerator BK\_BLE\_RP\_MASK
    :   Read Permission Mask.

    <a id="_CPPv4N16bk_ble_perm_mask13BK_BLE_RP_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask13BK_BLE_RP_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask13BK_BLE_RP_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a0d9ec2bc3c350b06bcad469eaa2266f4"></a> enumerator BK\_BLE\_RP\_POS

    <a id="_CPPv4N16bk_ble_perm_mask14BK_BLE_WP_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask14BK_BLE_WP_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask14BK_BLE_WP_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a0441f3e2131b90e4f7f0f9b56ddc9bb1"></a> enumerator BK\_BLE\_WP\_MASK
    :   Write Permission Mask.

    <a id="_CPPv4N16bk_ble_perm_mask13BK_BLE_WP_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask13BK_BLE_WP_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask13BK_BLE_WP_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a1e3e97f5039eed8cd2e58f922448dbac"></a> enumerator BK\_BLE\_WP\_POS

    <a id="_CPPv4N16bk_ble_perm_mask14BK_BLE_IP_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask14BK_BLE_IP_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask14BK_BLE_IP_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22ac989b546af16e79828c9687eaf4a2cf5"></a> enumerator BK\_BLE\_IP\_MASK
    :   Indication Access Mask.

    <a id="_CPPv4N16bk_ble_perm_mask13BK_BLE_IP_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask13BK_BLE_IP_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask13BK_BLE_IP_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a71a49563a14010a4ac82774d8a72b99c"></a> enumerator BK\_BLE\_IP\_POS

    <a id="_CPPv4N16bk_ble_perm_mask14BK_BLE_NP_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask14BK_BLE_NP_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask14BK_BLE_NP_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a1e7ca16a0d453d4a1b12293e0c3d37f0"></a> enumerator BK\_BLE\_NP\_MASK
    :   Notification Access Mask.

    <a id="_CPPv4N16bk_ble_perm_mask13BK_BLE_NP_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask13BK_BLE_NP_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask13BK_BLE_NP_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22af86e8881eb54765715d96884da17d57f"></a> enumerator BK\_BLE\_NP\_POS

    <a id="_CPPv4N16bk_ble_perm_mask21BK_BLE_BROADCAST_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask21BK_BLE_BROADCAST_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask21BK_BLE_BROADCAST_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a5ab1d50471f0870dcaeb916dce369a6d"></a> enumerator BK\_BLE\_BROADCAST\_MASK
    :   Broadcast descriptor present.

    <a id="_CPPv4N16bk_ble_perm_mask20BK_BLE_BROADCAST_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask20BK_BLE_BROADCAST_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask20BK_BLE_BROADCAST_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a3120d6a33d6c51b177df8731773ec888"></a> enumerator BK\_BLE\_BROADCAST\_POS

    <a id="_CPPv4N16bk_ble_perm_mask14BK_BLE_RD_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask14BK_BLE_RD_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask14BK_BLE_RD_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a64ea4430c8769ee1d57002125ea7dcab"></a> enumerator BK\_BLE\_RD\_MASK
    :   Read Access Mask.

    <a id="_CPPv4N16bk_ble_perm_mask13BK_BLE_RD_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask13BK_BLE_RD_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask13BK_BLE_RD_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a9649ef76a0e3d6f55a3d687065bad642"></a> enumerator BK\_BLE\_RD\_POS

    <a id="_CPPv4N16bk_ble_perm_mask25BK_BLE_WRITE_COMMAND_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask25BK_BLE_WRITE_COMMAND_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask25BK_BLE_WRITE_COMMAND_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a2b8cd657ac425926da41dda643eca722"></a> enumerator BK\_BLE\_WRITE\_COMMAND\_MASK
    :   Write Command Enabled attribute Mask.

    <a id="_CPPv4N16bk_ble_perm_mask24BK_BLE_WRITE_COMMAND_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask24BK_BLE_WRITE_COMMAND_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask24BK_BLE_WRITE_COMMAND_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a83e1ef223d6d12cd8389eb1858023a02"></a> enumerator BK\_BLE\_WRITE\_COMMAND\_POS

    <a id="_CPPv4N16bk_ble_perm_mask21BK_BLE_WRITE_REQ_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask21BK_BLE_WRITE_REQ_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask21BK_BLE_WRITE_REQ_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22ae99f3fe056cccd5dc3c7bf43103810c8"></a> enumerator BK\_BLE\_WRITE\_REQ\_MASK
    :   Write Request Enabled attribute Mask.

    <a id="_CPPv4N16bk_ble_perm_mask20BK_BLE_WRITE_REQ_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask20BK_BLE_WRITE_REQ_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask20BK_BLE_WRITE_REQ_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a19cf0afd18af3681a2370918e6321edc"></a> enumerator BK\_BLE\_WRITE\_REQ\_POS

    <a id="_CPPv4N16bk_ble_perm_mask15BK_BLE_NTF_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask15BK_BLE_NTF_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask15BK_BLE_NTF_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a5575973122b8460041e00c353aed3bb1"></a> enumerator BK\_BLE\_NTF\_MASK
    :   Notification Access Mask.

    <a id="_CPPv4N16bk_ble_perm_mask14BK_BLE_NTF_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask14BK_BLE_NTF_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask14BK_BLE_NTF_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a480ed7d3d56fd33bc277bee67281678e"></a> enumerator BK\_BLE\_NTF\_POS

    <a id="_CPPv4N16bk_ble_perm_mask15BK_BLE_IND_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask15BK_BLE_IND_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask15BK_BLE_IND_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a5a8414b2b11be5582064dc9d6c6c2594"></a> enumerator BK\_BLE\_IND\_MASK
    :   Indication Access Mask.

    <a id="_CPPv4N16bk_ble_perm_mask14BK_BLE_IND_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask14BK_BLE_IND_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask14BK_BLE_IND_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a867b5f08a7e4a26fcebc5b0aa2fea24c"></a> enumerator BK\_BLE\_IND\_POS

    <a id="_CPPv4N16bk_ble_perm_mask24BK_BLE_WRITE_SIGNED_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask24BK_BLE_WRITE_SIGNED_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask24BK_BLE_WRITE_SIGNED_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a6123ccc407fc95e5da9afa709cf4f187"></a> enumerator BK\_BLE\_WRITE\_SIGNED\_MASK
    :   Write Signed Enabled attribute Mask.

    <a id="_CPPv4N16bk_ble_perm_mask23BK_BLE_WRITE_SIGNED_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask23BK_BLE_WRITE_SIGNED_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask23BK_BLE_WRITE_SIGNED_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22ab398b4f194dd33b5b3fc6f951411031c"></a> enumerator BK\_BLE\_WRITE\_SIGNED\_POS

    <a id="_CPPv4N16bk_ble_perm_mask15BK_BLE_EXT_MASKE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask15BK_BLE_EXT_MASKE"></a> <a id="_CPPv2N16bk_ble_perm_mask15BK_BLE_EXT_MASKE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a275468e5a7ccdcd6e92da92aabca6d43"></a> enumerator BK\_BLE\_EXT\_MASK
    :   Extended properties descriptor present.

    <a id="_CPPv4N16bk_ble_perm_mask14BK_BLE_EXT_POSE"></a>

    <a id="_CPPv3N16bk_ble_perm_mask14BK_BLE_EXT_POSE"></a> <a id="_CPPv2N16bk_ble_perm_mask14BK_BLE_EXT_POSE"></a> <a id="group__bk__ble__api__v1_1ggaa529f18ac0ecdf658b9e49c2fffc7f22a52b38cbd5b7829e36645a06fced773ff"></a> enumerator BK\_BLE\_EXT\_POS

<a id="_CPPv420bk_ble_ext_perm_mask"></a>

<a id="_CPPv320bk_ble_ext_perm_mask"></a> <a id="_CPPv220bk_ble_ext_perm_mask"></a> <a id="group__bk__ble__api__v1_1ga3c750771a137d5504854bfcebb6e5235"></a> enum bk\_ble\_ext\_perm\_mask
:   Attribute Extended permissions, for BK\_BLE\_PERM\_SET.

    Extended Value permission bit field

    **Attention**
    :   you cant use this direct, use [BK\_BLE\_PERM\_SET(EKS, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) instead

    | 15 | 14 \- 13 | 12 | 11 | 10 \- 0 |
    | --- | --- | --- | --- | --- |
    | RI | UUID\_LEN | EKS | INCL | Reserved |

    Bit \[0-10\] : Reserved

    Bit \[11\] : Attribute Value is included(Value present in Database)

    Bit \[12\] : Encryption key Size must be 16 bytes

    Bit \[13-14\]: UUID Length (0 \= 16 bits, 1 \= 32 bits, 2 \= 128 bits, 3 \= RFU)

    Bit \[15\] : Trigger Read Indication (0 \= Value present in Database, 1 \= Value not present in Database)

    *Values:*

    <a id="_CPPv4N20bk_ble_ext_perm_mask22BK_BLE_VALUE_INCL_MASKE"></a>

    <a id="_CPPv3N20bk_ble_ext_perm_mask22BK_BLE_VALUE_INCL_MASKE"></a> <a id="_CPPv2N20bk_ble_ext_perm_mask22BK_BLE_VALUE_INCL_MASKE"></a> <a id="group__bk__ble__api__v1_1gga3c750771a137d5504854bfcebb6e5235ad60ba325fbb4c8b7e585bbb205452fea"></a> enumerator BK\_BLE\_VALUE\_INCL\_MASK
    :   Attribute Value is included.

    <a id="_CPPv4N20bk_ble_ext_perm_mask21BK_BLE_VALUE_INCL_POSE"></a>

    <a id="_CPPv3N20bk_ble_ext_perm_mask21BK_BLE_VALUE_INCL_POSE"></a> <a id="_CPPv2N20bk_ble_ext_perm_mask21BK_BLE_VALUE_INCL_POSE"></a> <a id="group__bk__ble__api__v1_1gga3c750771a137d5504854bfcebb6e5235aac2e0574cee0dcabee8c352344f07d86"></a> enumerator BK\_BLE\_VALUE\_INCL\_POS

    <a id="_CPPv4N20bk_ble_ext_perm_mask15BK_BLE_EKS_MASKE"></a>

    <a id="_CPPv3N20bk_ble_ext_perm_mask15BK_BLE_EKS_MASKE"></a> <a id="_CPPv2N20bk_ble_ext_perm_mask15BK_BLE_EKS_MASKE"></a> <a id="group__bk__ble__api__v1_1gga3c750771a137d5504854bfcebb6e5235a1017d3efa95446f54b971268fd2b183d"></a> enumerator BK\_BLE\_EKS\_MASK
    :   Check Encryption key size Mask.

    <a id="_CPPv4N20bk_ble_ext_perm_mask14BK_BLE_EKS_POSE"></a>

    <a id="_CPPv3N20bk_ble_ext_perm_mask14BK_BLE_EKS_POSE"></a> <a id="_CPPv2N20bk_ble_ext_perm_mask14BK_BLE_EKS_POSE"></a> <a id="group__bk__ble__api__v1_1gga3c750771a137d5504854bfcebb6e5235a8e7d250d2f898ca4340256cff38a70d9"></a> enumerator BK\_BLE\_EKS\_POS

    <a id="_CPPv4N20bk_ble_ext_perm_mask20BK_BLE_UUID_LEN_MASKE"></a>

    <a id="_CPPv3N20bk_ble_ext_perm_mask20BK_BLE_UUID_LEN_MASKE"></a> <a id="_CPPv2N20bk_ble_ext_perm_mask20BK_BLE_UUID_LEN_MASKE"></a> <a id="group__bk__ble__api__v1_1gga3c750771a137d5504854bfcebb6e5235a6eaf2efbea77f3a8cd3dfbd71d881cf1"></a> enumerator BK\_BLE\_UUID\_LEN\_MASK
    :   UUID Length.

    <a id="_CPPv4N20bk_ble_ext_perm_mask19BK_BLE_UUID_LEN_POSE"></a>

    <a id="_CPPv3N20bk_ble_ext_perm_mask19BK_BLE_UUID_LEN_POSE"></a> <a id="_CPPv2N20bk_ble_ext_perm_mask19BK_BLE_UUID_LEN_POSE"></a> <a id="group__bk__ble__api__v1_1gga3c750771a137d5504854bfcebb6e5235a74b4a92205e2440cce4cffd6b3986a9d"></a> enumerator BK\_BLE\_UUID\_LEN\_POS

    <a id="_CPPv4N20bk_ble_ext_perm_mask14BK_BLE_RI_MASKE"></a>

    <a id="_CPPv3N20bk_ble_ext_perm_mask14BK_BLE_RI_MASKE"></a> <a id="_CPPv2N20bk_ble_ext_perm_mask14BK_BLE_RI_MASKE"></a> <a id="group__bk__ble__api__v1_1gga3c750771a137d5504854bfcebb6e5235a20524048dc2f5302b68c55cd6cefc65a"></a> enumerator BK\_BLE\_RI\_MASK
    :   Read trigger Indication.

    <a id="_CPPv4N20bk_ble_ext_perm_mask13BK_BLE_RI_POSE"></a>

    <a id="_CPPv3N20bk_ble_ext_perm_mask13BK_BLE_RI_POSE"></a> <a id="_CPPv2N20bk_ble_ext_perm_mask13BK_BLE_RI_POSE"></a> <a id="group__bk__ble__api__v1_1gga3c750771a137d5504854bfcebb6e5235aa257ae6f47e63be8408b1f7763adb53d"></a> enumerator BK\_BLE\_RI\_POS

<a id="_CPPv420bk_ble_svc_perm_mask"></a>

<a id="_CPPv320bk_ble_svc_perm_mask"></a> <a id="_CPPv220bk_ble_svc_perm_mask"></a> <a id="group__bk__ble__api__v1_1ga391834053b6777e7f684b4ea71d34811"></a> enum bk\_ble\_svc\_perm\_mask
:   Service permissions, for BK\_BLE\_PERM\_SET.

    | 7 | 6 \- 5 | 4 | 3 \- 2 | 1 | 0 |
    | --- | --- | --- | --- | --- | --- |
    | SEC | UUID\_LEN | DIS | AUTH | EKS | MI |

    **Attention**
    :   you cant use this direct, use [BK\_BLE\_PERM\_SET(SVC\_UUID\_LEN, UUID\_16)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b) instead

    Bit \[0\] : Task that manage service is multi-instantiated (Connection index is conveyed)

    Bit \[1\] : Encryption key Size must be 16 bytes

    Bit \[2-3\]: Service Permission (0 \= NO\_AUTH, 1 \= UNAUTH, 2 \= AUTH, 3 \= Secure Connect)

    Bit \[4\] : Disable the service

    Bit \[5-6\]: UUID Length (0 \= 16 bits, 1 \= 32 bits, 2 \= 128 bits, 3 \= RFU)

    Bit \[7\] : Secondary Service (0 \= Primary Service, 1 \= Secondary Service)

    *Values:*

    <a id="_CPPv4N20bk_ble_svc_perm_mask18BK_BLE_SVC_MI_MASKE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask18BK_BLE_SVC_MI_MASKE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask18BK_BLE_SVC_MI_MASKE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811a205433f5f13db7900adda586526235b6"></a> enumerator BK\_BLE\_SVC\_MI\_MASK
    :   Task that manage service is multi-instantiated.

    <a id="_CPPv4N20bk_ble_svc_perm_mask17BK_BLE_SVC_MI_POSE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask17BK_BLE_SVC_MI_POSE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask17BK_BLE_SVC_MI_POSE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811a93a8cc723b54c02351db07aa18ae445c"></a> enumerator BK\_BLE\_SVC\_MI\_POS

    <a id="_CPPv4N20bk_ble_svc_perm_mask19BK_BLE_SVC_EKS_MASKE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask19BK_BLE_SVC_EKS_MASKE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask19BK_BLE_SVC_EKS_MASKE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811ad09e6a3af1c92221ea1e907ff626cd32"></a> enumerator BK\_BLE\_SVC\_EKS\_MASK
    :   Check Encryption key size for service Access.

    <a id="_CPPv4N20bk_ble_svc_perm_mask18BK_BLE_SVC_EKS_POSE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask18BK_BLE_SVC_EKS_POSE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask18BK_BLE_SVC_EKS_POSE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811a786da7d843e324aa9bc1c4869cd51b40"></a> enumerator BK\_BLE\_SVC\_EKS\_POS

    <a id="_CPPv4N20bk_ble_svc_perm_mask20BK_BLE_SVC_AUTH_MASKE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask20BK_BLE_SVC_AUTH_MASKE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask20BK_BLE_SVC_AUTH_MASKE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811af3a4b289d81263c8f642f43f725d8a91"></a> enumerator BK\_BLE\_SVC\_AUTH\_MASK
    :   Service Permission authentication.

    <a id="_CPPv4N20bk_ble_svc_perm_mask19BK_BLE_SVC_AUTH_POSE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask19BK_BLE_SVC_AUTH_POSE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask19BK_BLE_SVC_AUTH_POSE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811a2bbe5cbe4e227abdbb830266cfed8da4"></a> enumerator BK\_BLE\_SVC\_AUTH\_POS

    <a id="_CPPv4N20bk_ble_svc_perm_mask19BK_BLE_SVC_DIS_MASKE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask19BK_BLE_SVC_DIS_MASKE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask19BK_BLE_SVC_DIS_MASKE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811a85f7157e31162ceb509d826a9c942ae5"></a> enumerator BK\_BLE\_SVC\_DIS\_MASK
    :   Disable the service.

    <a id="_CPPv4N20bk_ble_svc_perm_mask18BK_BLE_SVC_DIS_POSE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask18BK_BLE_SVC_DIS_POSE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask18BK_BLE_SVC_DIS_POSE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811ad14b0d9c8b2ffd64034c1bad9f54ecf0"></a> enumerator BK\_BLE\_SVC\_DIS\_POS

    <a id="_CPPv4N20bk_ble_svc_perm_mask24BK_BLE_SVC_UUID_LEN_MASKE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask24BK_BLE_SVC_UUID_LEN_MASKE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask24BK_BLE_SVC_UUID_LEN_MASKE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811ab80ac257bc219d788b864dcef3959174"></a> enumerator BK\_BLE\_SVC\_UUID\_LEN\_MASK
    :   Service UUID Length.

    <a id="_CPPv4N20bk_ble_svc_perm_mask23BK_BLE_SVC_UUID_LEN_POSE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask23BK_BLE_SVC_UUID_LEN_POSE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask23BK_BLE_SVC_UUID_LEN_POSE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811adf7c2194f9888b39b7a5e45f9964677a"></a> enumerator BK\_BLE\_SVC\_UUID\_LEN\_POS

    <a id="_CPPv4N20bk_ble_svc_perm_mask25BK_BLE_SVC_SECONDARY_MASKE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask25BK_BLE_SVC_SECONDARY_MASKE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask25BK_BLE_SVC_SECONDARY_MASKE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811abfdd1487376e4303a15dab9199334c34"></a> enumerator BK\_BLE\_SVC\_SECONDARY\_MASK
    :   Service type Secondary.

    <a id="_CPPv4N20bk_ble_svc_perm_mask24BK_BLE_SVC_SECONDARY_POSE"></a>

    <a id="_CPPv3N20bk_ble_svc_perm_mask24BK_BLE_SVC_SECONDARY_POSE"></a> <a id="_CPPv2N20bk_ble_svc_perm_mask24BK_BLE_SVC_SECONDARY_POSE"></a> <a id="group__bk__ble__api__v1_1gga391834053b6777e7f684b4ea71d34811ad701e9394a71730315214c2866772855"></a> enumerator BK\_BLE\_SVC\_SECONDARY\_POS

<a id="_CPPv4Ut1_0"></a>

<a id="_CPPv3Ut1_0"></a> <a id="group__bk__ble__api__v1_1ga06fc87d81c62e9abb8790b6e5713c55b"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt1_025BK_BLE_PERM_RIGHT_DISABLEE"></a>

    <a id="_CPPv3NUt1_025BK_BLE_PERM_RIGHT_DISABLEE"></a> <a id="group__bk__ble__api__v1_1gga06fc87d81c62e9abb8790b6e5713c55ba9be1c04515409aa5eeaaae93c9e92fcd"></a> enumerator BK\_BLE\_PERM\_RIGHT\_DISABLE
    :   Disable access.

    <a id="_CPPv4NUt1_024BK_BLE_PERM_RIGHT_ENABLEE"></a>

    <a id="_CPPv3NUt1_024BK_BLE_PERM_RIGHT_ENABLEE"></a> <a id="group__bk__ble__api__v1_1gga06fc87d81c62e9abb8790b6e5713c55baa86aa249371126b53055fbd024bf2bb1"></a> enumerator BK\_BLE\_PERM\_RIGHT\_ENABLE
    :   Enable access.

<a id="_CPPv4Ut1_1"></a>

<a id="_CPPv3Ut1_1"></a> <a id="group__bk__ble__api__v1_1gadf764cbdea00d65edcd07bb9953ad2b7"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt1_125BK_BLE_PERM_RIGHT_NO_AUTHE"></a>

    <a id="_CPPv3NUt1_125BK_BLE_PERM_RIGHT_NO_AUTHE"></a> <a id="group__bk__ble__api__v1_1ggadf764cbdea00d65edcd07bb9953ad2b7a11a016e005f711095fa7f29b8d47e5c5"></a> enumerator BK\_BLE\_PERM\_RIGHT\_NO\_AUTH
    :   No Authentication.

    <a id="_CPPv4NUt1_124BK_BLE_PERM_RIGHT_UNAUTHE"></a>

    <a id="_CPPv3NUt1_124BK_BLE_PERM_RIGHT_UNAUTHE"></a> <a id="group__bk__ble__api__v1_1ggadf764cbdea00d65edcd07bb9953ad2b7a4639ac034d0b1cc495d15a52f96a3e6e"></a> enumerator BK\_BLE\_PERM\_RIGHT\_UNAUTH
    :   Access Requires Unauthenticated link.

    <a id="_CPPv4NUt1_122BK_BLE_PERM_RIGHT_AUTHE"></a>

    <a id="_CPPv3NUt1_122BK_BLE_PERM_RIGHT_AUTHE"></a> <a id="group__bk__ble__api__v1_1ggadf764cbdea00d65edcd07bb9953ad2b7a20d838c38c592c6caec2f1c8051b605e"></a> enumerator BK\_BLE\_PERM\_RIGHT\_AUTH
    :   Access Requires Authenticated link.

    <a id="_CPPv4NUt1_125BK_BLE_PERM_RIGHT_SEC_CONE"></a>

    <a id="_CPPv3NUt1_125BK_BLE_PERM_RIGHT_SEC_CONE"></a> <a id="group__bk__ble__api__v1_1ggadf764cbdea00d65edcd07bb9953ad2b7aeb25a35bd13703406ea346c1c2c0f33f"></a> enumerator BK\_BLE\_PERM\_RIGHT\_SEC\_CON
    :   Access Requires Secure Connection link.

<a id="_CPPv4Ut1_2"></a>

<a id="_CPPv3Ut1_2"></a> <a id="group__bk__ble__api__v1_1ga99fb83031ce9923c84392b4e92f956b5"></a> enum \[anonymous\]
:   *Values:*

    <a id="_CPPv4NUt1_225BK_BLE_PERM_RIGHT_UUID_16E"></a>

    <a id="_CPPv3NUt1_225BK_BLE_PERM_RIGHT_UUID_16E"></a> <a id="group__bk__ble__api__v1_1gga99fb83031ce9923c84392b4e92f956b5a25db928cc38335fa3dda0a78ae58bf0d"></a> enumerator BK\_BLE\_PERM\_RIGHT\_UUID\_16
    :   16 bits UUID

    <a id="_CPPv4NUt1_225BK_BLE_PERM_RIGHT_UUID_32E"></a>

    <a id="_CPPv3NUt1_225BK_BLE_PERM_RIGHT_UUID_32E"></a> <a id="group__bk__ble__api__v1_1gga99fb83031ce9923c84392b4e92f956b5ae1a469cb692c2f336665501223ba85bc"></a> enumerator BK\_BLE\_PERM\_RIGHT\_UUID\_32
    :   32 bits UUID

    <a id="_CPPv4NUt1_226BK_BLE_PERM_RIGHT_UUID_128E"></a>

    <a id="_CPPv3NUt1_226BK_BLE_PERM_RIGHT_UUID_128E"></a> <a id="group__bk__ble__api__v1_1gga99fb83031ce9923c84392b4e92f956b5acb88d87262c6d823d670c03339900560"></a> enumerator BK\_BLE\_PERM\_RIGHT\_UUID\_128
    :   128 bits UUID

    <a id="_CPPv4NUt1_226BK_BLE_PERM_RIGHT_UUID_RFUE"></a>

    <a id="_CPPv3NUt1_226BK_BLE_PERM_RIGHT_UUID_RFUE"></a> <a id="group__bk__ble__api__v1_1gga99fb83031ce9923c84392b4e92f956b5a5ebf47fcd932d30f544e4826e5ba4452"></a> enumerator BK\_BLE\_PERM\_RIGHT\_UUID\_RFU
    :   Invalid.

<a id="_CPPv49ble_cmd_t"></a>

<a id="_CPPv39ble_cmd_t"></a> <a id="_CPPv29ble_cmd_t"></a> <a id="group__bk__ble__api__v1_1ga9801599b87e214e2e00bb28da16f0e0d"></a> enum ble\_cmd\_t
:   *Values:*

    <a id="_CPPv4N9ble_cmd_t12BLE_CMD_NONEE"></a>

    <a id="_CPPv3N9ble_cmd_t12BLE_CMD_NONEE"></a> <a id="_CPPv2N9ble_cmd_t12BLE_CMD_NONEE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dae0c65fbac97a567ea04b132950ebb7ea"></a> enumerator BLE\_CMD\_NONE

    <a id="_CPPv4N9ble_cmd_t14BLE_CREATE_ADVE"></a>

    <a id="_CPPv3N9ble_cmd_t14BLE_CREATE_ADVE"></a> <a id="_CPPv2N9ble_cmd_t14BLE_CREATE_ADVE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dad8d6dded22b2c38b5884fdd9eac8292b"></a> enumerator BLE\_CREATE\_ADV
    :   ADV\_CMD:FOR BLE 5.1.

    <a id="_CPPv4N9ble_cmd_t14BLE_MODIFY_ADVE"></a>

    <a id="_CPPv3N9ble_cmd_t14BLE_MODIFY_ADVE"></a> <a id="_CPPv2N9ble_cmd_t14BLE_MODIFY_ADVE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da93546bf104bfd72a5f9337e382dff2d8"></a> enumerator BLE\_MODIFY\_ADV

    <a id="_CPPv4N9ble_cmd_t16BLE_SET_ADV_DATAE"></a>

    <a id="_CPPv3N9ble_cmd_t16BLE_SET_ADV_DATAE"></a> <a id="_CPPv2N9ble_cmd_t16BLE_SET_ADV_DATAE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0daa241768e9fae960b000adc1f5dfb7f16"></a> enumerator BLE\_SET\_ADV\_DATA

    <a id="_CPPv4N9ble_cmd_t16BLE_SET_RSP_DATAE"></a>

    <a id="_CPPv3N9ble_cmd_t16BLE_SET_RSP_DATAE"></a> <a id="_CPPv2N9ble_cmd_t16BLE_SET_RSP_DATAE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dad819543a4e331990b8a96757757e4a7c"></a> enumerator BLE\_SET\_RSP\_DATA

    <a id="_CPPv4N9ble_cmd_t13BLE_START_ADVE"></a>

    <a id="_CPPv3N9ble_cmd_t13BLE_START_ADVE"></a> <a id="_CPPv2N9ble_cmd_t13BLE_START_ADVE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da0e4f768a7f8bec5ffa17b02aec76ed8f"></a> enumerator BLE\_START\_ADV

    <a id="_CPPv4N9ble_cmd_t12BLE_STOP_ADVE"></a>

    <a id="_CPPv3N9ble_cmd_t12BLE_STOP_ADVE"></a> <a id="_CPPv2N9ble_cmd_t12BLE_STOP_ADVE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da8aad650777fa00a735c7b77753b613d3"></a> enumerator BLE\_STOP\_ADV

    <a id="_CPPv4N9ble_cmd_t14BLE_DELETE_ADVE"></a>

    <a id="_CPPv3N9ble_cmd_t14BLE_DELETE_ADVE"></a> <a id="_CPPv2N9ble_cmd_t14BLE_DELETE_ADVE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0daec68cf87faaad45c46b0f31b0af8edba"></a> enumerator BLE\_DELETE\_ADV

    <a id="_CPPv4N9ble_cmd_t12BLE_INIT_ADVE"></a>

    <a id="_CPPv3N9ble_cmd_t12BLE_INIT_ADVE"></a> <a id="_CPPv2N9ble_cmd_t12BLE_INIT_ADVE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0daf6aa5752806fa6b8348c477fbce2d816"></a> enumerator BLE\_INIT\_ADV
    :   ADV\_CMD:FOR BLE 4.2.

    <a id="_CPPv4N9ble_cmd_t14BLE_DEINIT_ADVE"></a>

    <a id="_CPPv3N9ble_cmd_t14BLE_DEINIT_ADVE"></a> <a id="_CPPv2N9ble_cmd_t14BLE_DEINIT_ADVE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dafa46c3ac7a39a89297f9cf38e5734607"></a> enumerator BLE\_DEINIT\_ADV

    <a id="_CPPv4N9ble_cmd_t15BLE_CREATE_SCANE"></a>

    <a id="_CPPv3N9ble_cmd_t15BLE_CREATE_SCANE"></a> <a id="_CPPv2N9ble_cmd_t15BLE_CREATE_SCANE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da869869af192b70cfc351720b73ffe4a9"></a> enumerator BLE\_CREATE\_SCAN
    :   SCAN\_CMD:FOR BLE 5.1.

    <a id="_CPPv4N9ble_cmd_t14BLE_START_SCANE"></a>

    <a id="_CPPv3N9ble_cmd_t14BLE_START_SCANE"></a> <a id="_CPPv2N9ble_cmd_t14BLE_START_SCANE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da99b194c61a93c591dfcecc85ca5b262d"></a> enumerator BLE\_START\_SCAN

    <a id="_CPPv4N9ble_cmd_t13BLE_STOP_SCANE"></a>

    <a id="_CPPv3N9ble_cmd_t13BLE_STOP_SCANE"></a> <a id="_CPPv2N9ble_cmd_t13BLE_STOP_SCANE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da72e0c7b7302aee05bd752862e45fcce3"></a> enumerator BLE\_STOP\_SCAN

    <a id="_CPPv4N9ble_cmd_t15BLE_DELETE_SCANE"></a>

    <a id="_CPPv3N9ble_cmd_t15BLE_DELETE_SCANE"></a> <a id="_CPPv2N9ble_cmd_t15BLE_DELETE_SCANE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da008a42de3af4f564a9ac9e1ffdf600d5"></a> enumerator BLE\_DELETE\_SCAN

    <a id="_CPPv4N9ble_cmd_t13BLE_INIT_SCANE"></a>

    <a id="_CPPv3N9ble_cmd_t13BLE_INIT_SCANE"></a> <a id="_CPPv2N9ble_cmd_t13BLE_INIT_SCANE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da2b54b635c5d892c3d4209c88d18c3d4d"></a> enumerator BLE\_INIT\_SCAN
    :   SCAN\_CMD:FOR BLE 4.2.

    <a id="_CPPv4N9ble_cmd_t15BLE_DEINIT_SCANE"></a>

    <a id="_CPPv3N9ble_cmd_t15BLE_DEINIT_SCANE"></a> <a id="_CPPv2N9ble_cmd_t15BLE_DEINIT_SCANE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dae7aee5579f9a8c32e4accfc0849f2851"></a> enumerator BLE\_DEINIT\_SCAN

    <a id="_CPPv4N9ble_cmd_t19BLE_CONN_UPDATE_MTUE"></a>

    <a id="_CPPv3N9ble_cmd_t19BLE_CONN_UPDATE_MTUE"></a> <a id="_CPPv2N9ble_cmd_t19BLE_CONN_UPDATE_MTUE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da84c7214d655474e6036ca2ed6a2548a9"></a> enumerator BLE\_CONN\_UPDATE\_MTU
    :   conn

    <a id="_CPPv4N9ble_cmd_t21BLE_CONN_UPDATE_PARAME"></a>

    <a id="_CPPv3N9ble_cmd_t21BLE_CONN_UPDATE_PARAME"></a> <a id="_CPPv2N9ble_cmd_t21BLE_CONN_UPDATE_PARAME"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dae9df6e284106ae6ae6a8f52d1c8c38f0"></a> enumerator BLE\_CONN\_UPDATE\_PARAM

    <a id="_CPPv4N9ble_cmd_t17BLE_CONN_DIS_CONNE"></a>

    <a id="_CPPv3N9ble_cmd_t17BLE_CONN_DIS_CONNE"></a> <a id="_CPPv2N9ble_cmd_t17BLE_CONN_DIS_CONNE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0daea8cdfeef1216950ea0a170a4504a483"></a> enumerator BLE\_CONN\_DIS\_CONN

    <a id="_CPPv4N9ble_cmd_t17BLE_CONN_READ_PHYE"></a>

    <a id="_CPPv3N9ble_cmd_t17BLE_CONN_READ_PHYE"></a> <a id="_CPPv2N9ble_cmd_t17BLE_CONN_READ_PHYE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da6193b3a8977665c459fc25928727c73d"></a> enumerator BLE\_CONN\_READ\_PHY

    <a id="_CPPv4N9ble_cmd_t16BLE_CONN_SET_PHYE"></a>

    <a id="_CPPv3N9ble_cmd_t16BLE_CONN_SET_PHYE"></a> <a id="_CPPv2N9ble_cmd_t16BLE_CONN_SET_PHYE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da5a0e8649e35d581c35cad91eeeaa3751"></a> enumerator BLE\_CONN\_SET\_PHY

    <a id="_CPPv4N9ble_cmd_t16BLE_CONN_ENCRYPTE"></a>

    <a id="_CPPv3N9ble_cmd_t16BLE_CONN_ENCRYPTE"></a> <a id="_CPPv2N9ble_cmd_t16BLE_CONN_ENCRYPTE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0daabf8ff611e57569c7217c50327c90cd6"></a> enumerator BLE\_CONN\_ENCRYPT

    <a id="_CPPv4N9ble_cmd_t15BLE_INIT_CREATEE"></a>

    <a id="_CPPv3N9ble_cmd_t15BLE_INIT_CREATEE"></a> <a id="_CPPv2N9ble_cmd_t15BLE_INIT_CREATEE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dabd8968e94c1fdc9ae6008d354b50a489"></a> enumerator BLE\_INIT\_CREATE
    :   init

    <a id="_CPPv4N9ble_cmd_t19BLE_INIT_START_CONNE"></a>

    <a id="_CPPv3N9ble_cmd_t19BLE_INIT_START_CONNE"></a> <a id="_CPPv2N9ble_cmd_t19BLE_INIT_START_CONNE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da3ccfcd2f8b73f4865da997819c276146"></a> enumerator BLE\_INIT\_START\_CONN

    <a id="_CPPv4N9ble_cmd_t18BLE_INIT_STOP_CONNE"></a>

    <a id="_CPPv3N9ble_cmd_t18BLE_INIT_STOP_CONNE"></a> <a id="_CPPv2N9ble_cmd_t18BLE_INIT_STOP_CONNE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da55ef40219395cb7704ca37011e1d5766"></a> enumerator BLE\_INIT\_STOP\_CONN

    <a id="_CPPv4N9ble_cmd_t17BLE_INIT_DIS_CONNE"></a>

    <a id="_CPPv3N9ble_cmd_t17BLE_INIT_DIS_CONNE"></a> <a id="_CPPv2N9ble_cmd_t17BLE_INIT_DIS_CONNE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da28d88b1603ae434a90c8b77ec5e9b0cd"></a> enumerator BLE\_INIT\_DIS\_CONN

    <a id="_CPPv4N9ble_cmd_t18BLE_INIT_READ_CHARE"></a>

    <a id="_CPPv3N9ble_cmd_t18BLE_INIT_READ_CHARE"></a> <a id="_CPPv2N9ble_cmd_t18BLE_INIT_READ_CHARE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0daae1277dbb85965f808e52a7737ab1b78"></a> enumerator BLE\_INIT\_READ\_CHAR

    <a id="_CPPv4N9ble_cmd_t19BLE_INIT_WRITE_CHARE"></a>

    <a id="_CPPv3N9ble_cmd_t19BLE_INIT_WRITE_CHARE"></a> <a id="_CPPv2N9ble_cmd_t19BLE_INIT_WRITE_CHARE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da305d34a23e2b8b41c2fdae235b0cdd73"></a> enumerator BLE\_INIT\_WRITE\_CHAR

    <a id="_CPPv4N9ble_cmd_t15BLE_SET_MAX_MTUE"></a>

    <a id="_CPPv3N9ble_cmd_t15BLE_SET_MAX_MTUE"></a> <a id="_CPPv2N9ble_cmd_t15BLE_SET_MAX_MTUE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dac0ea1ba46581a91ef34d9a2055bf3444"></a> enumerator BLE\_SET\_MAX\_MTU
    :   config

    <a id="_CPPv4N9ble_cmd_t19BLE_CREATE_PERIODICE"></a>

    <a id="_CPPv3N9ble_cmd_t19BLE_CREATE_PERIODICE"></a> <a id="_CPPv2N9ble_cmd_t19BLE_CREATE_PERIODICE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da0ab84f3504a51898fb6e6c398d774aa2"></a> enumerator BLE\_CREATE\_PERIODIC

    <a id="_CPPv4N9ble_cmd_t18BLE_START_PERIODICE"></a>

    <a id="_CPPv3N9ble_cmd_t18BLE_START_PERIODICE"></a> <a id="_CPPv2N9ble_cmd_t18BLE_START_PERIODICE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0daec19de508a314b95fd7aba251eb4ccb5"></a> enumerator BLE\_START\_PERIODIC

    <a id="_CPPv4N9ble_cmd_t17BLE_STOP_PERIODICE"></a>

    <a id="_CPPv3N9ble_cmd_t17BLE_STOP_PERIODICE"></a> <a id="_CPPv2N9ble_cmd_t17BLE_STOP_PERIODICE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da053740e7ea912054b0cd57e46e6f7078"></a> enumerator BLE\_STOP\_PERIODIC

    <a id="_CPPv4N9ble_cmd_t19BLE_DELETE_PERIODICE"></a>

    <a id="_CPPv3N9ble_cmd_t19BLE_DELETE_PERIODICE"></a> <a id="_CPPv2N9ble_cmd_t19BLE_DELETE_PERIODICE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da587b64656c33f64d7dd3afbe7ff47327"></a> enumerator BLE\_DELETE\_PERIODIC

    <a id="_CPPv4N9ble_cmd_t18BLE_SET_LOCAL_NAMEE"></a>

    <a id="_CPPv3N9ble_cmd_t18BLE_SET_LOCAL_NAMEE"></a> <a id="_CPPv2N9ble_cmd_t18BLE_SET_LOCAL_NAMEE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da31751fb34c3aa15783ef646d0723a350"></a> enumerator BLE\_SET\_LOCAL\_NAME

    <a id="_CPPv4N9ble_cmd_t18BLE_GET_LOCAL_NAMEE"></a>

    <a id="_CPPv3N9ble_cmd_t18BLE_GET_LOCAL_NAMEE"></a> <a id="_CPPv2N9ble_cmd_t18BLE_GET_LOCAL_NAMEE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dacbd5681b06cc721f8dfbc7716ec02e2a"></a> enumerator BLE\_GET\_LOCAL\_NAME

    <a id="_CPPv4N9ble_cmd_t19BLE_READ_LOCAL_ADDRE"></a>

    <a id="_CPPv3N9ble_cmd_t19BLE_READ_LOCAL_ADDRE"></a> <a id="_CPPv2N9ble_cmd_t19BLE_READ_LOCAL_ADDRE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dae5e4ec6d104a7f1849c03572dd66fb8d"></a> enumerator BLE\_READ\_LOCAL\_ADDR

    <a id="_CPPv4N9ble_cmd_t19BLE_SET_RANDOM_ADDRE"></a>

    <a id="_CPPv3N9ble_cmd_t19BLE_SET_RANDOM_ADDRE"></a> <a id="_CPPv2N9ble_cmd_t19BLE_SET_RANDOM_ADDRE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0daf80386d514d080863522d25870d182c4"></a> enumerator BLE\_SET\_RANDOM\_ADDR

    <a id="_CPPv4N9ble_cmd_t23BLE_SET_ADV_RANDOM_ADDRE"></a>

    <a id="_CPPv3N9ble_cmd_t23BLE_SET_ADV_RANDOM_ADDRE"></a> <a id="_CPPv2N9ble_cmd_t23BLE_SET_ADV_RANDOM_ADDRE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da4ad13e035a98840e76d413f56cee8d18"></a> enumerator BLE\_SET\_ADV\_RANDOM\_ADDR

    <a id="_CPPv4N9ble_cmd_t18BLE_ADD_WHITE_LISTE"></a>

    <a id="_CPPv3N9ble_cmd_t18BLE_ADD_WHITE_LISTE"></a> <a id="_CPPv2N9ble_cmd_t18BLE_ADD_WHITE_LISTE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da6fb015283fe76d06bc81cce988aec578"></a> enumerator BLE\_ADD\_WHITE\_LIST

    <a id="_CPPv4N9ble_cmd_t18BLE_RMV_WHITE_LISTE"></a>

    <a id="_CPPv3N9ble_cmd_t18BLE_RMV_WHITE_LISTE"></a> <a id="_CPPv2N9ble_cmd_t18BLE_RMV_WHITE_LISTE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0dac34c9762e40f1a6f609cda9261bf0f9f"></a> enumerator BLE\_RMV\_WHITE\_LIST

    <a id="_CPPv4N9ble_cmd_t18BLE_CLE_WHITE_LISTE"></a>

    <a id="_CPPv3N9ble_cmd_t18BLE_CLE_WHITE_LISTE"></a> <a id="_CPPv2N9ble_cmd_t18BLE_CLE_WHITE_LISTE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da7d48d68b61acd8868aa183b632d14185"></a> enumerator BLE\_CLE\_WHITE\_LIST

    <a id="_CPPv4N9ble_cmd_t11BLE_CMD_MAXE"></a>

    <a id="_CPPv3N9ble_cmd_t11BLE_CMD_MAXE"></a> <a id="_CPPv2N9ble_cmd_t11BLE_CMD_MAXE"></a> <a id="group__bk__ble__api__v1_1gga9801599b87e214e2e00bb28da16f0e0da5c5c3e336ee535c0d8ef3ea30151f9d7"></a> enumerator BLE\_CMD\_MAX

<a id="_CPPv412ble_notice_t"></a>

<a id="_CPPv312ble_notice_t"></a> <a id="_CPPv212ble_notice_t"></a> <a id="group__bk__ble__api__v1_1ga0bcca73e43830fd3440cb09cc01294f3"></a> enum ble\_notice\_t
:   *Values:*

    <a id="_CPPv4N12ble_notice_t14BLE_5_STACK_OKE"></a>

    <a id="_CPPv3N12ble_notice_t14BLE_5_STACK_OKE"></a> <a id="_CPPv2N12ble_notice_t14BLE_5_STACK_OKE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a7e01206fd01dc61e5a6615668e7703ee"></a> enumerator BLE\_5\_STACK\_OK
    :   ble stack init ok, param null.This event is deprecated,please do not use it.

    <a id="_CPPv4N12ble_notice_t17BLE_5_WRITE_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t17BLE_5_WRITE_EVENTE"></a> <a id="_CPPv2N12ble_notice_t17BLE_5_WRITE_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a58574fe9c4dc1778f56561196e304d39"></a> enumerator BLE\_5\_WRITE\_EVENT
    :   peer write our, param [ble\_write\_req\_t](#structble__write__req__t)

    <a id="_CPPv4N12ble_notice_t16BLE_5_READ_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t16BLE_5_READ_EVENTE"></a> <a id="_CPPv2N12ble_notice_t16BLE_5_READ_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a9000f45195301685f3c1f93141c0c8c6"></a> enumerator BLE\_5\_READ\_EVENT
    :   peer read our, param [ble\_read\_req\_t](#structble__read__req__t)

    <a id="_CPPv4N12ble_notice_t16BLE_5_REPORT_ADVE"></a>

    <a id="_CPPv3N12ble_notice_t16BLE_5_REPORT_ADVE"></a> <a id="_CPPv2N12ble_notice_t16BLE_5_REPORT_ADVE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3ae3dfc071331695f61f2a2c192ec7e505"></a> enumerator BLE\_5\_REPORT\_ADV
    :   scan peer adv report, param [ble\_recv\_adv\_t](#structble__recv__adv__t)

    <a id="_CPPv4N12ble_notice_t16BLE_5_MTU_CHANGEE"></a>

    <a id="_CPPv3N12ble_notice_t16BLE_5_MTU_CHANGEE"></a> <a id="_CPPv2N12ble_notice_t16BLE_5_MTU_CHANGEE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3ad21acd32dd01acb3ebc2b091b4b81465"></a> enumerator BLE\_5\_MTU\_CHANGE
    :   mtu change event, param [ble\_mtu\_change\_t](#structble__mtu__change__t)

    <a id="_CPPv4N12ble_notice_t19BLE_5_CONNECT_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t19BLE_5_CONNECT_EVENTE"></a> <a id="_CPPv2N12ble_notice_t19BLE_5_CONNECT_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a5e72b31146968abb86e292c10c2af7af"></a> enumerator BLE\_5\_CONNECT\_EVENT
    :   as slaver, recv connnect event, param [ble\_conn\_ind\_t](#structble__conn__ind__t)

    <a id="_CPPv4N12ble_notice_t22BLE_5_DISCONNECT_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t22BLE_5_DISCONNECT_EVENTE"></a> <a id="_CPPv2N12ble_notice_t22BLE_5_DISCONNECT_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a4b238cacc401b2a9fa242fdae0bf3ca4"></a> enumerator BLE\_5\_DISCONNECT\_EVENT
    :   recv disconnect event, param [ble\_discon\_ind\_t](#structble__discon__ind__t)

    <a id="_CPPv4N12ble_notice_t18BLE_5_ATT_INFO_REQE"></a>

    <a id="_CPPv3N12ble_notice_t18BLE_5_ATT_INFO_REQE"></a> <a id="_CPPv2N12ble_notice_t18BLE_5_ATT_INFO_REQE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3acf4178aace725bb5fec85b2b456f8c2b"></a> enumerator BLE\_5\_ATT\_INFO\_REQ

    <a id="_CPPv4N12ble_notice_t15BLE_5_CREATE_DBE"></a>

    <a id="_CPPv3N12ble_notice_t15BLE_5_CREATE_DBE"></a> <a id="_CPPv2N12ble_notice_t15BLE_5_CREATE_DBE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3af194509a3be556f3feafcd4274a04977"></a> enumerator BLE\_5\_CREATE\_DB
    :   create db event, param [ble\_create\_db\_t](#structble__create__db__t)

    <a id="_CPPv4N12ble_notice_t13BLE_5_TX_DONEE"></a>

    <a id="_CPPv3N12ble_notice_t13BLE_5_TX_DONEE"></a> <a id="_CPPv2N12ble_notice_t13BLE_5_TX_DONEE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a5922d24bc5d4a14db372e6878e7bd23b"></a> enumerator BLE\_5\_TX\_DONE
    :   tx complete event, param null

    <a id="_CPPv4N12ble_notice_t17BLE_5_PAIRING_REQE"></a>

    <a id="_CPPv3N12ble_notice_t17BLE_5_PAIRING_REQE"></a> <a id="_CPPv2N12ble_notice_t17BLE_5_PAIRING_REQE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3aee1be53af00f9a7156f13e19d1ebd023"></a> enumerator BLE\_5\_PAIRING\_REQ
    :   as slave, peer requests pairing (Pairing Request), param [ble\_smp\_ind\_t](#structble__smp__ind__t); accept with [bk\_ble\_sec\_send\_auth\_mode()](#group__bk__ble__api__v1_1ga3b406cbb6440cbff728fb52de36f91e6)/\_ext() or reject with [bk\_ble\_reject\_pairing()](#group__bk__ble__api__v1_1ga443972f2fd64e485a46614c16f7d74c3)

    <a id="_CPPv4N12ble_notice_t21BLE_5_PAIRING_SUCCEEDE"></a>

    <a id="_CPPv3N12ble_notice_t21BLE_5_PAIRING_SUCCEEDE"></a> <a id="_CPPv2N12ble_notice_t21BLE_5_PAIRING_SUCCEEDE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3aa1855717d8b1523ea883ab4a1c22991b"></a> enumerator BLE\_5\_PAIRING\_SUCCEED
    :   pairing succeed, param [ble\_smp\_ind\_t](#structble__smp__ind__t)

    <a id="_CPPv4N12ble_notice_t20BLE_5_PAIRING_FAILEDE"></a>

    <a id="_CPPv3N12ble_notice_t20BLE_5_PAIRING_FAILEDE"></a> <a id="_CPPv2N12ble_notice_t20BLE_5_PAIRING_FAILEDE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3afa4d4ffbfac6c4bd0bc582415390cf8f"></a> enumerator BLE\_5\_PAIRING\_FAILED
    :   pairing failed, param [ble\_smp\_ind\_t](#structble__smp__ind__t) (status \= SMP fail reason code)

    <a id="_CPPv4N12ble_notice_t24BLE_5_PARING_PASSKEY_REQE"></a>

    <a id="_CPPv3N12ble_notice_t24BLE_5_PARING_PASSKEY_REQE"></a> <a id="_CPPv2N12ble_notice_t24BLE_5_PARING_PASSKEY_REQE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a7de37581ca661bbed6c1fb1dce3d6de8"></a> enumerator BLE\_5\_PARING\_PASSKEY\_REQ
    :   discarded, replace with BLE\_5\_PARING\_PASSKEY\_INPUT\_REQ and BLE\_5\_PARING\_PASSKEY\_DISPLAY\_REQ

    <a id="_CPPv4N12ble_notice_t19BLE_5_ENCRYPT_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t19BLE_5_ENCRYPT_EVENTE"></a> <a id="_CPPv2N12ble_notice_t19BLE_5_ENCRYPT_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a111c96778f8d51b7ee36f7bb5312a37b"></a> enumerator BLE\_5\_ENCRYPT\_EVENT
    :   link encrypted, param [ble\_smp\_ind\_t](#structble__smp__ind__t) (status \= auth level)

    <a id="_CPPv4N12ble_notice_t24BLE_5_INIT_CONNECT_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t24BLE_5_INIT_CONNECT_EVENTE"></a> <a id="_CPPv2N12ble_notice_t24BLE_5_INIT_CONNECT_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a225e83c86c3ef4aad89ee1b0119db864"></a> enumerator BLE\_5\_INIT\_CONNECT\_EVENT
    :   as master, recv connect event

    <a id="_CPPv4N12ble_notice_t27BLE_5_INIT_DISCONNECT_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t27BLE_5_INIT_DISCONNECT_EVENTE"></a> <a id="_CPPv2N12ble_notice_t27BLE_5_INIT_DISCONNECT_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a9ba0ce42303bd30b85669b8f439f28ac"></a> enumerator BLE\_5\_INIT\_DISCONNECT\_EVENT

    <a id="_CPPv4N12ble_notice_t31BLE_5_INIT_CONNECT_FAILED_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t31BLE_5_INIT_CONNECT_FAILED_EVENTE"></a> <a id="_CPPv2N12ble_notice_t31BLE_5_INIT_CONNECT_FAILED_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a4636ece2656518c0262ff637cdeaf187"></a> enumerator BLE\_5\_INIT\_CONNECT\_FAILED\_EVENT

    <a id="_CPPv4N12ble_notice_t25BLE_5_SDP_REGISTER_FAILEDE"></a>

    <a id="_CPPv3N12ble_notice_t25BLE_5_SDP_REGISTER_FAILEDE"></a> <a id="_CPPv2N12ble_notice_t25BLE_5_SDP_REGISTER_FAILEDE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a1f4984843b5aa177d9a3f1ad1f5b7ddb"></a> enumerator BLE\_5\_SDP\_REGISTER\_FAILED

    <a id="_CPPv4N12ble_notice_t20BLE_5_READ_PHY_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t20BLE_5_READ_PHY_EVENTE"></a> <a id="_CPPv2N12ble_notice_t20BLE_5_READ_PHY_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a6a01d522725ed8b863fc389e515a1f05"></a> enumerator BLE\_5\_READ\_PHY\_EVENT
    :   get current conn phy result, param [ble\_read\_phy\_t](#structble__read__phy__t)

    <a id="_CPPv4N12ble_notice_t23BLE_5_CONN_UPDATA_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t23BLE_5_CONN_UPDATA_EVENTE"></a> <a id="_CPPv2N12ble_notice_t23BLE_5_CONN_UPDATA_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3ad154891d46bf4d5aba9177d6929a6f47"></a> enumerator BLE\_5\_CONN\_UPDATA\_EVENT
    :   recv conn update event, param [ble\_conn\_param\_t](#structble__conn__param__t)

    <a id="_CPPv4N12ble_notice_t30BLE_5_PERIODIC_SYNC_CMPL_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t30BLE_5_PERIODIC_SYNC_CMPL_EVENTE"></a> <a id="_CPPv2N12ble_notice_t30BLE_5_PERIODIC_SYNC_CMPL_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a208dc372f5e897b1eb27ecb89fc66148"></a> enumerator BLE\_5\_PERIODIC\_SYNC\_CMPL\_EVENT

    <a id="_CPPv4N12ble_notice_t37BLE_5_DISCOVERY_PRIMARY_SERVICE_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t37BLE_5_DISCOVERY_PRIMARY_SERVICE_EVENTE"></a> <a id="_CPPv2N12ble_notice_t37BLE_5_DISCOVERY_PRIMARY_SERVICE_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a31cfa7ec8408adaaddf603c6b76e602b"></a> enumerator BLE\_5\_DISCOVERY\_PRIMARY\_SERVICE\_EVENT

    <a id="_CPPv4N12ble_notice_t26BLE_5_DISCOVERY_CHAR_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t26BLE_5_DISCOVERY_CHAR_EVENTE"></a> <a id="_CPPv2N12ble_notice_t26BLE_5_DISCOVERY_CHAR_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3aaa8a8cd749202a1a367136545d5b259a"></a> enumerator BLE\_5\_DISCOVERY\_CHAR\_EVENT

    <a id="_CPPv4N12ble_notice_t23BLE_5_RECV_NOTIFY_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t23BLE_5_RECV_NOTIFY_EVENTE"></a> <a id="_CPPv2N12ble_notice_t23BLE_5_RECV_NOTIFY_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a3c50c9dc2eca3432a5ac7dfaf5911442"></a> enumerator BLE\_5\_RECV\_NOTIFY\_EVENT

    <a id="_CPPv4N12ble_notice_t23BLE_5_ATT_READ_RESPONSEE"></a>

    <a id="_CPPv3N12ble_notice_t23BLE_5_ATT_READ_RESPONSEE"></a> <a id="_CPPv2N12ble_notice_t23BLE_5_ATT_READ_RESPONSEE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3af9032e438d373977b21e3c5abd02dd78"></a> enumerator BLE\_5\_ATT\_READ\_RESPONSE

    <a id="_CPPv4N12ble_notice_t22BLE_5_CONN_UPD_PAR_ASKE"></a>

    <a id="_CPPv3N12ble_notice_t22BLE_5_CONN_UPD_PAR_ASKE"></a> <a id="_CPPv2N12ble_notice_t22BLE_5_CONN_UPD_PAR_ASKE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a5588230fe069304807cdda84d62f72d2"></a> enumerator BLE\_5\_CONN\_UPD\_PAR\_ASK

    <a id="_CPPv4N12ble_notice_t22BLE_5_SHUTDOWN_SUCCEEDE"></a>

    <a id="_CPPv3N12ble_notice_t22BLE_5_SHUTDOWN_SUCCEEDE"></a> <a id="_CPPv2N12ble_notice_t22BLE_5_SHUTDOWN_SUCCEEDE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a6036e01bc2c2bc3840e9e8757a2f925d"></a> enumerator BLE\_5\_SHUTDOWN\_SUCCEED

    <a id="_CPPv4N12ble_notice_t25BLE_5_DELETE_SERVICE_DONEE"></a>

    <a id="_CPPv3N12ble_notice_t25BLE_5_DELETE_SERVICE_DONEE"></a> <a id="_CPPv2N12ble_notice_t25BLE_5_DELETE_SERVICE_DONEE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3aefacd1478b41576fa1931578e51ec5d0"></a> enumerator BLE\_5\_DELETE\_SERVICE\_DONE
    :   delete service event

    <a id="_CPPv4N12ble_notice_t23BLE_5_GAP_CMD_CMP_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t23BLE_5_GAP_CMD_CMP_EVENTE"></a> <a id="_CPPv2N12ble_notice_t23BLE_5_GAP_CMD_CMP_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3aad8f19c6a415b68102fa6417e89c97a7"></a> enumerator BLE\_5\_GAP\_CMD\_CMP\_EVENT

    <a id="_CPPv4N12ble_notice_t23BLE_5_ADV_STOPPED_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t23BLE_5_ADV_STOPPED_EVENTE"></a> <a id="_CPPv2N12ble_notice_t23BLE_5_ADV_STOPPED_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a49356063db96a4f58ab225316ee06d4f"></a> enumerator BLE\_5\_ADV\_STOPPED\_EVENT

    <a id="_CPPv4N12ble_notice_t26BLE_5_READ_RSSI_CMPL_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t26BLE_5_READ_RSSI_CMPL_EVENTE"></a> <a id="_CPPv2N12ble_notice_t26BLE_5_READ_RSSI_CMPL_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a3c331d159e7072140f2c7b2eadffd063"></a> enumerator BLE\_5\_READ\_RSSI\_CMPL\_EVENT

    <a id="_CPPv4N12ble_notice_t15BLE_5_KEY_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t15BLE_5_KEY_EVENTE"></a> <a id="_CPPv2N12ble_notice_t15BLE_5_KEY_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a0443e21c5655917032a9bef7dcc6693b"></a> enumerator BLE\_5\_KEY\_EVENT
    :   pairing distributed keys (bond info) reported to app, param [bk\_ble\_key\_t](#structbk__ble__key__t)

    <a id="_CPPv4N12ble_notice_t25BLE_5_BOND_INFO_REQ_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t25BLE_5_BOND_INFO_REQ_EVENTE"></a> <a id="_CPPv2N12ble_notice_t25BLE_5_BOND_INFO_REQ_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a40dc4decaf756c09b5d8d5114ada720f"></a> enumerator BLE\_5\_BOND\_INFO\_REQ\_EVENT
    :   request app to provide the stored bond info, param [bk\_ble\_bond\_info\_req\_t](#structbk__ble__bond__info__req__t)

    <a id="_CPPv4N12ble_notice_t21BLE_5_READ_BLOB_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t21BLE_5_READ_BLOB_EVENTE"></a> <a id="_CPPv2N12ble_notice_t21BLE_5_READ_BLOB_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a2f85011b6d99d7c4faa8e4b36a079d1b"></a> enumerator BLE\_5\_READ\_BLOB\_EVENT

    <a id="_CPPv4N12ble_notice_t32BLE_5_PAIRING_SECURITY_REQ_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t32BLE_5_PAIRING_SECURITY_REQ_EVENTE"></a> <a id="_CPPv2N12ble_notice_t32BLE_5_PAIRING_SECURITY_REQ_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3ac8e24fcd0e33e631f11ecb17e2ef168d"></a> enumerator BLE\_5\_PAIRING\_SECURITY\_REQ\_EVENT
    :   as master, peer(slave) sent a Security Request, param [ble\_smp\_ind\_t](#structble__smp__ind__t); start pairing/encryption with [bk\_ble\_create\_bond()](#group__bk__ble__api__v1_1gac786e0c3ad011349f19ccfc337037ce9)/\_ext()

    <a id="_CPPv4N12ble_notice_t37BLE_5_PARING_NUMBER_COMPARE_REQ_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t37BLE_5_PARING_NUMBER_COMPARE_REQ_EVENTE"></a> <a id="_CPPv2N12ble_notice_t37BLE_5_PARING_NUMBER_COMPARE_REQ_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a74205d4cc126d7ad37e0bbef68e3fdaa"></a> enumerator BLE\_5\_PARING\_NUMBER\_COMPARE\_REQ\_EVENT
    :   LE SC numeric comparison request, param [ble\_smp\_ind\_t](#structble__smp__ind__t) (num \= 6-digit compare value); reply with [bk\_ble\_number\_compare\_send()](#group__bk__ble__api__v1_1ga5d75e7894809d173a6d4c85239735cc5)

    <a id="_CPPv4N12ble_notice_t19BLE_5_OOB_REQ_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t19BLE_5_OOB_REQ_EVENTE"></a> <a id="_CPPv2N12ble_notice_t19BLE_5_OOB_REQ_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a35ddf504a764649f4663e4477c518adc"></a> enumerator BLE\_5\_OOB\_REQ\_EVENT
    :   legacy OOB data request

    <a id="_CPPv4N12ble_notice_t22BLE_5_SC_OOB_REQ_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t22BLE_5_SC_OOB_REQ_EVENTE"></a> <a id="_CPPv2N12ble_notice_t22BLE_5_SC_OOB_REQ_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a1a3a470ef4ca03f1703b29944813710b"></a> enumerator BLE\_5\_SC\_OOB\_REQ\_EVENT
    :   LE Secure Connections OOB data request.

    <a id="_CPPv4N12ble_notice_t20BLE_5_SC_LOC_OOB_INDE"></a>

    <a id="_CPPv3N12ble_notice_t20BLE_5_SC_LOC_OOB_INDE"></a> <a id="_CPPv2N12ble_notice_t20BLE_5_SC_LOC_OOB_INDE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a7d379ac3364a96c99291b3a566466c20"></a> enumerator BLE\_5\_SC\_LOC\_OOB\_IND
    :   local LE Secure Connections OOB data indication (see [ble\_loc\_oob\_data\_t](#structble__loc__oob__data__t))

    <a id="_CPPv4N12ble_notice_t24BLE_5_SCAN_STOPPED_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t24BLE_5_SCAN_STOPPED_EVENTE"></a> <a id="_CPPv2N12ble_notice_t24BLE_5_SCAN_STOPPED_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a4be0fa5f3418ac0a787f5036c7d0742a"></a> enumerator BLE\_5\_SCAN\_STOPPED\_EVENT

    <a id="_CPPv4N12ble_notice_t30BLE_5_PARING_PASSKEY_INPUT_REQE"></a>

    <a id="_CPPv3N12ble_notice_t30BLE_5_PARING_PASSKEY_INPUT_REQE"></a> <a id="_CPPv2N12ble_notice_t30BLE_5_PARING_PASSKEY_INPUT_REQE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3aaa129acafbbf51ff76b5e06c71c1cd8d"></a> enumerator BLE\_5\_PARING\_PASSKEY\_INPUT\_REQ
    :   pairing passkey input request (local side should input the peer-displayed passkey)

    <a id="_CPPv4N12ble_notice_t32BLE_5_PARING_PASSKEY_DISPLAY_REQE"></a>

    <a id="_CPPv3N12ble_notice_t32BLE_5_PARING_PASSKEY_DISPLAY_REQE"></a> <a id="_CPPv2N12ble_notice_t32BLE_5_PARING_PASSKEY_DISPLAY_REQE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a36a3e8dfa14475313b3eba602bb5a129"></a> enumerator BLE\_5\_PARING\_PASSKEY\_DISPLAY\_REQ
    :   pairing passkey display request (local side should display the passkey to the user)

    <a id="_CPPv4N12ble_notice_t25BLE_5_COC_REG_COMPL_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t25BLE_5_COC_REG_COMPL_EVENTE"></a> <a id="_CPPv2N12ble_notice_t25BLE_5_COC_REG_COMPL_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a33384a777ea6d4919eeecad03fdda2bd"></a> enumerator BLE\_5\_COC\_REG\_COMPL\_EVENT
    :   COC PSM register complete (see coc\_reg\_evt)

    <a id="_CPPv4N12ble_notice_t27BLE_5_COC_UNREG_COMPL_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t27BLE_5_COC_UNREG_COMPL_EVENTE"></a> <a id="_CPPv2N12ble_notice_t27BLE_5_COC_UNREG_COMPL_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a6deb2a4e90f796a6463a33e9b10c1129"></a> enumerator BLE\_5\_COC\_UNREG\_COMPL\_EVENT
    :   COC PSM unregister complete.

    <a id="_CPPv4N12ble_notice_t28BLE_5_COC_CONFIG_COMPL_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t28BLE_5_COC_CONFIG_COMPL_EVENTE"></a> <a id="_CPPv2N12ble_notice_t28BLE_5_COC_CONFIG_COMPL_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a3d5b39cf554effd2c13fec534b870696"></a> enumerator BLE\_5\_COC\_CONFIG\_COMPL\_EVENT
    :   COC PSM config complete (see coc\_config\_evt)

    <a id="_CPPv4N12ble_notice_t32BLE_5_COC_CONNECTION_COMPL_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t32BLE_5_COC_CONNECTION_COMPL_EVENTE"></a> <a id="_CPPv2N12ble_notice_t32BLE_5_COC_CONNECTION_COMPL_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a3335763791c68423288dc9c38e3d8f7e"></a> enumerator BLE\_5\_COC\_CONNECTION\_COMPL\_EVENT
    :   COC channel connection complete (see coc\_connection\_compl\_evt)

    <a id="_CPPv4N12ble_notice_t33BLE_5_COC_DISCCONNECT_COMPL_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t33BLE_5_COC_DISCCONNECT_COMPL_EVENTE"></a> <a id="_CPPv2N12ble_notice_t33BLE_5_COC_DISCCONNECT_COMPL_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a101cb33b7ed582b672e22c2178b8fdcd"></a> enumerator BLE\_5\_COC\_DISCCONNECT\_COMPL\_EVENT
    :   COC channel disconnection complete (see coc\_disconnect\_compl\_evt)

    <a id="_CPPv4N12ble_notice_t17BLE_5_COC_TX_DONEE"></a>

    <a id="_CPPv3N12ble_notice_t17BLE_5_COC_TX_DONEE"></a> <a id="_CPPv2N12ble_notice_t17BLE_5_COC_TX_DONEE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3a84ef5a5412927152525bc1110d41c9ba"></a> enumerator BLE\_5\_COC\_TX\_DONE
    :   COC data transmission done (see coc\_send\_compl\_evt)

    <a id="_CPPv4N12ble_notice_t16BLE_5_COC_RX_INDE"></a>

    <a id="_CPPv3N12ble_notice_t16BLE_5_COC_RX_INDE"></a> <a id="_CPPv2N12ble_notice_t16BLE_5_COC_RX_INDE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3abfe496771986f01857217979946cbaf4"></a> enumerator BLE\_5\_COC\_RX\_IND
    :   COC data received (see coc\_recv\_evt)

    <a id="_CPPv4N12ble_notice_t27BLE_5_COC_CONNECT_REQ_EVENTE"></a>

    <a id="_CPPv3N12ble_notice_t27BLE_5_COC_CONNECT_REQ_EVENTE"></a> <a id="_CPPv2N12ble_notice_t27BLE_5_COC_CONNECT_REQ_EVENTE"></a> <a id="group__bk__ble__api__v1_1gga0bcca73e43830fd3440cb09cc01294f3ab7e9ac38aea49dba994bae2ce1bba8b8"></a> enumerator BLE\_5\_COC\_CONNECT\_REQ\_EVENT
    :   incoming COC connection request (see coc\_connect\_req\_evt)

<a id="_CPPv49CHAR_TYPE"></a>

<a id="_CPPv39CHAR_TYPE"></a> <a id="_CPPv29CHAR_TYPE"></a> <a id="group__bk__ble__api__v1_1gaeb41f806b82df447b2f964ca753fcd5a"></a> enum CHAR\_TYPE
:   *Values:*

    <a id="_CPPv4N9CHAR_TYPE13CHARAC_NOTIFYE"></a>

    <a id="_CPPv3N9CHAR_TYPE13CHARAC_NOTIFYE"></a> <a id="_CPPv2N9CHAR_TYPE13CHARAC_NOTIFYE"></a> <a id="group__bk__ble__api__v1_1ggaeb41f806b82df447b2f964ca753fcd5aa1fb0421d90a47c4f9f17fa07f3f9527c"></a> enumerator CHARAC\_NOTIFY

    <a id="_CPPv4N9CHAR_TYPE15CHARAC_INDICATEE"></a>

    <a id="_CPPv3N9CHAR_TYPE15CHARAC_INDICATEE"></a> <a id="_CPPv2N9CHAR_TYPE15CHARAC_INDICATEE"></a> <a id="group__bk__ble__api__v1_1ggaeb41f806b82df447b2f964ca753fcd5aabfab0b7e2c9af256a073fcac363a2069"></a> enumerator CHARAC\_INDICATE

    <a id="_CPPv4N9CHAR_TYPE11CHARAC_READE"></a>

    <a id="_CPPv3N9CHAR_TYPE11CHARAC_READE"></a> <a id="_CPPv2N9CHAR_TYPE11CHARAC_READE"></a> <a id="group__bk__ble__api__v1_1ggaeb41f806b82df447b2f964ca753fcd5aac3ded6ca552396ccd9fc3952958c2c1f"></a> enumerator CHARAC\_READ

    <a id="_CPPv4N9CHAR_TYPE16CHARAC_READ_DONEE"></a>

    <a id="_CPPv3N9CHAR_TYPE16CHARAC_READ_DONEE"></a> <a id="_CPPv2N9CHAR_TYPE16CHARAC_READ_DONEE"></a> <a id="group__bk__ble__api__v1_1ggaeb41f806b82df447b2f964ca753fcd5aab5bef3e6bee72022dcca2fe237f2cfef"></a> enumerator CHARAC\_READ\_DONE

    <a id="_CPPv4N9CHAR_TYPE17CHARAC_WRITE_DONEE"></a>

    <a id="_CPPv3N9CHAR_TYPE17CHARAC_WRITE_DONEE"></a> <a id="_CPPv2N9CHAR_TYPE17CHARAC_WRITE_DONEE"></a> <a id="group__bk__ble__api__v1_1ggaeb41f806b82df447b2f964ca753fcd5aa8be6c2cf932d7864c493b7030b30113d"></a> enumerator CHARAC\_WRITE\_DONE

<a id="_CPPv418MASTER_COMMON_TYPE"></a>

<a id="_CPPv318MASTER_COMMON_TYPE"></a> <a id="_CPPv218MASTER_COMMON_TYPE"></a> <a id="group__bk__ble__api__v1_1gad953151559361a2e0102c4c9a3bd77d8"></a> enum MASTER\_COMMON\_TYPE
:   *Values:*

    <a id="_CPPv4N18MASTER_COMMON_TYPE17MST_TYPE_SVR_UUIDE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE17MST_TYPE_SVR_UUIDE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE17MST_TYPE_SVR_UUIDE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a40d7f7821c82fdb5eafc28ba287f575a"></a> enumerator MST\_TYPE\_SVR\_UUID

    <a id="_CPPv4N18MASTER_COMMON_TYPE17MST_TYPE_ATT_UUIDE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE17MST_TYPE_ATT_UUIDE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE17MST_TYPE_ATT_UUIDE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a6f5412e98ae0565eebc2c304ddd355be"></a> enumerator MST\_TYPE\_ATT\_UUID

    <a id="_CPPv4N18MASTER_COMMON_TYPE17MST_TYPE_ATT_DESCE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE17MST_TYPE_ATT_DESCE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE17MST_TYPE_ATT_DESCE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a30728c63c38992b7f6d6254a0b6b4e5d"></a> enumerator MST\_TYPE\_ATT\_DESC

    <a id="_CPPv4N18MASTER_COMMON_TYPE16MST_TYPE_SDP_ENDE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE16MST_TYPE_SDP_ENDE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE16MST_TYPE_SDP_ENDE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a12a890e8a7a2c63114b597ee5ff8e135"></a> enumerator MST\_TYPE\_SDP\_END

    <a id="_CPPv4N18MASTER_COMMON_TYPE22MST_TYPE_ATTC_SVR_UUIDE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE22MST_TYPE_ATTC_SVR_UUIDE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE22MST_TYPE_ATTC_SVR_UUIDE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a938ba3fc112ac31f5b32c048ee512612"></a> enumerator MST\_TYPE\_ATTC\_SVR\_UUID

    <a id="_CPPv4N18MASTER_COMMON_TYPE22MST_TYPE_ATTC_ATT_UUIDE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE22MST_TYPE_ATTC_ATT_UUIDE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE22MST_TYPE_ATTC_ATT_UUIDE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a6778001ac4a5e4f048bc640938474cc2"></a> enumerator MST\_TYPE\_ATTC\_ATT\_UUID
    :   Service the UUID.

    <a id="_CPPv4N18MASTER_COMMON_TYPE22MST_TYPE_ATTC_ATT_DESCE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE22MST_TYPE_ATTC_ATT_DESCE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE22MST_TYPE_ATTC_ATT_DESCE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a49fe52837f95c7e9cb6ddb77b3f1f965"></a> enumerator MST\_TYPE\_ATTC\_ATT\_DESC
    :   ATT of a service.

    <a id="_CPPv4N18MASTER_COMMON_TYPE23MST_TYPS_ATTC_PARAM_ERRE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE23MST_TYPS_ATTC_PARAM_ERRE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE23MST_TYPS_ATTC_PARAM_ERRE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8aecfd4e6f7d2dc45d4d69008a98c91edd"></a> enumerator MST\_TYPS\_ATTC\_PARAM\_ERR
    :   ATT DESC of a service.

    <a id="_CPPv4N18MASTER_COMMON_TYPE17MST_TYPE_ATTC_ERRE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE17MST_TYPE_ATTC_ERRE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE17MST_TYPE_ATTC_ERRE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a5a69eb2441261a46dcdfcafa0f9b4b46"></a> enumerator MST\_TYPE\_ATTC\_ERR
    :   The delivered parameter is abnormal or unknown.

    <a id="_CPPv4N18MASTER_COMMON_TYPE17MST_TYPE_ATTC_ENDE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE17MST_TYPE_ATTC_ENDE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE17MST_TYPE_ATTC_ENDE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a5fc80545b3afb0a6e20ec358286f5350"></a> enumerator MST\_TYPE\_ATTC\_END
    :   if appm\_get\_init\_attc\_info return is ok \&\& ble is disconnect,so update the event

    <a id="_CPPv4N18MASTER_COMMON_TYPE23MST_TYPE_ATTC_WRITE_RSPE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE23MST_TYPE_ATTC_WRITE_RSPE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE23MST_TYPE_ATTC_WRITE_RSPE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a29ef1c6f91053c591fcda8c15e4325ab"></a> enumerator MST\_TYPE\_ATTC\_WRITE\_RSP
    :   End of the operation.

    <a id="_CPPv4N18MASTER_COMMON_TYPE31MST_TYPE_ATTC_WRITE_NO_RESPONSEE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE31MST_TYPE_ATTC_WRITE_NO_RESPONSEE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE31MST_TYPE_ATTC_WRITE_NO_RESPONSEE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a5391e5bce23207515664d310e297dee5"></a> enumerator MST\_TYPE\_ATTC\_WRITE\_NO\_RESPONSE

    <a id="_CPPv4N18MASTER_COMMON_TYPE30MST_TYPE_ATTC_CHARAC_READ_DONEE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE30MST_TYPE_ATTC_CHARAC_READ_DONEE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE30MST_TYPE_ATTC_CHARAC_READ_DONEE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8acc3aeff18054812e394d0ab8d87e5650"></a> enumerator MST\_TYPE\_ATTC\_CHARAC\_READ\_DONE

    <a id="_CPPv4N18MASTER_COMMON_TYPE16MST_TYPE_MTU_EXCE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE16MST_TYPE_MTU_EXCE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE16MST_TYPE_MTU_EXCE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8aaa6f4467c2d938d9c7b423d0e985636b"></a> enumerator MST\_TYPE\_MTU\_EXC

    <a id="_CPPv4N18MASTER_COMMON_TYPE21MST_TYPE_MTU_EXC_DONEE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE21MST_TYPE_MTU_EXC_DONEE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE21MST_TYPE_MTU_EXC_DONEE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8adb9b3ecc9349fed7cf2890b0a8e8d296"></a> enumerator MST\_TYPE\_MTU\_EXC\_DONE

    <a id="_CPPv4N18MASTER_COMMON_TYPE16MST_TYPE_UPP_ASKE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE16MST_TYPE_UPP_ASKE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE16MST_TYPE_UPP_ASKE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a820948e8285b78bfc765eed754f0ae69"></a> enumerator MST\_TYPE\_UPP\_ASK

    <a id="_CPPv4N18MASTER_COMMON_TYPE22MST_TYPE_UPDATA_STATUSE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE22MST_TYPE_UPDATA_STATUSE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE22MST_TYPE_UPDATA_STATUSE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a1cf96778e72fd3ddbcf8994fe7bda0d4"></a> enumerator MST\_TYPE\_UPDATA\_STATUS
    :   Ask if you agree to update the parameter.

    <a id="_CPPv4N18MASTER_COMMON_TYPE33MST_TYPE_DISCOVER_PRI_SERVICE_RSPE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE33MST_TYPE_DISCOVER_PRI_SERVICE_RSPE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE33MST_TYPE_DISCOVER_PRI_SERVICE_RSPE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a638e45347a59c6a9c8d6f0319f15388a"></a> enumerator MST\_TYPE\_DISCOVER\_PRI\_SERVICE\_RSP

    <a id="_CPPv4N18MASTER_COMMON_TYPE41MST_TYPE_DISCOVER_PRI_SERVICE_BY_UUID_RSPE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE41MST_TYPE_DISCOVER_PRI_SERVICE_BY_UUID_RSPE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE41MST_TYPE_DISCOVER_PRI_SERVICE_BY_UUID_RSPE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8aa98ca54c5bb44550d003f1ac6b665298"></a> enumerator MST\_TYPE\_DISCOVER\_PRI\_SERVICE\_BY\_UUID\_RSP

    <a id="_CPPv4N18MASTER_COMMON_TYPE45MST_TYPE_DISCOVER_PRI_SERVICE_BY_128_UUID_RSPE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE45MST_TYPE_DISCOVER_PRI_SERVICE_BY_128_UUID_RSPE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE45MST_TYPE_DISCOVER_PRI_SERVICE_BY_128_UUID_RSPE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8aac51cdfc39fadd6cf55e80e0b994bc1a"></a> enumerator MST\_TYPE\_DISCOVER\_PRI\_SERVICE\_BY\_128\_UUID\_RSP

    <a id="_CPPv4N18MASTER_COMMON_TYPE26MST_TYPE_DISCOVER_CHAR_RSPE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE26MST_TYPE_DISCOVER_CHAR_RSPE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE26MST_TYPE_DISCOVER_CHAR_RSPE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8adda51021674cfd442741acc122ba6468"></a> enumerator MST\_TYPE\_DISCOVER\_CHAR\_RSP

    <a id="_CPPv4N18MASTER_COMMON_TYPE34MST_TYPE_DISCOVER_CHAR_BY_UUID_RSPE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE34MST_TYPE_DISCOVER_CHAR_BY_UUID_RSPE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE34MST_TYPE_DISCOVER_CHAR_BY_UUID_RSPE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a5589b3440fc6d21d5a2372c9be486491"></a> enumerator MST\_TYPE\_DISCOVER\_CHAR\_BY\_UUID\_RSP

    <a id="_CPPv4N18MASTER_COMMON_TYPE38MST_TYPE_DISCOVER_CHAR_BY_128_UUID_RSPE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE38MST_TYPE_DISCOVER_CHAR_BY_128_UUID_RSPE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE38MST_TYPE_DISCOVER_CHAR_BY_128_UUID_RSPE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a0e853ae0f1403933d78ed9e5b6267100"></a> enumerator MST\_TYPE\_DISCOVER\_CHAR\_BY\_128\_UUID\_RSP

    <a id="_CPPv4N18MASTER_COMMON_TYPE27MST_TYPE_DISCOVER_CHAR_DESCE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE27MST_TYPE_DISCOVER_CHAR_DESCE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE27MST_TYPE_DISCOVER_CHAR_DESCE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8a3c03df202c225b1babc20519897bd759"></a> enumerator MST\_TYPE\_DISCOVER\_CHAR\_DESC

    <a id="_CPPv4N18MASTER_COMMON_TYPE27MST_TYPE_DISCOVER_COMPLETEDE"></a>

    <a id="_CPPv3N18MASTER_COMMON_TYPE27MST_TYPE_DISCOVER_COMPLETEDE"></a> <a id="_CPPv2N18MASTER_COMMON_TYPE27MST_TYPE_DISCOVER_COMPLETEDE"></a> <a id="group__bk__ble__api__v1_1ggad953151559361a2e0102c4c9a3bd77d8ac0f43be6aa5dfdccb07267580b5471f0"></a> enumerator MST\_TYPE\_DISCOVER\_COMPLETED

<a id="_CPPv48msg_attc"></a>

<a id="_CPPv38msg_attc"></a> <a id="_CPPv28msg_attc"></a> <a id="group__bk__ble__api__v1_1ga0d2f5c239f8dfb71778af9b1c083c7fb"></a> enum msg\_attc
:   *Values:*

    <a id="_CPPv4N8msg_attc12MST_ATTC_ALLE"></a>

    <a id="_CPPv3N8msg_attc12MST_ATTC_ALLE"></a> <a id="_CPPv2N8msg_attc12MST_ATTC_ALLE"></a> <a id="group__bk__ble__api__v1_1gga0d2f5c239f8dfb71778af9b1c083c7fba440ee17bea84fcec7ac2d5c560782e36"></a> enumerator MST\_ATTC\_ALL

    <a id="_CPPv4N8msg_attc25MST_ATTC_GET_SVR_UUID_ALLE"></a>

    <a id="_CPPv3N8msg_attc25MST_ATTC_GET_SVR_UUID_ALLE"></a> <a id="_CPPv2N8msg_attc25MST_ATTC_GET_SVR_UUID_ALLE"></a> <a id="group__bk__ble__api__v1_1gga0d2f5c239f8dfb71778af9b1c083c7fba123018e64df63423d6ba48eaab039c83"></a> enumerator MST\_ATTC\_GET\_SVR\_UUID\_ALL

    <a id="_CPPv4N8msg_attc33MST_ATTC_GET_SVR_UUID_BY_SVR_UUIDE"></a>

    <a id="_CPPv3N8msg_attc33MST_ATTC_GET_SVR_UUID_BY_SVR_UUIDE"></a> <a id="_CPPv2N8msg_attc33MST_ATTC_GET_SVR_UUID_BY_SVR_UUIDE"></a> <a id="group__bk__ble__api__v1_1gga0d2f5c239f8dfb71778af9b1c083c7fba6c9862959bd1ece0714db964dcbd630f"></a> enumerator MST\_ATTC\_GET\_SVR\_UUID\_BY\_SVR\_UUID

    <a id="_CPPv4N8msg_attc25MST_ATTC_GET_ATT_UUID_ALLE"></a>

    <a id="_CPPv3N8msg_attc25MST_ATTC_GET_ATT_UUID_ALLE"></a> <a id="_CPPv2N8msg_attc25MST_ATTC_GET_ATT_UUID_ALLE"></a> <a id="group__bk__ble__api__v1_1gga0d2f5c239f8dfb71778af9b1c083c7fba8d62374968ebefec650974d9054f6ede"></a> enumerator MST\_ATTC\_GET\_ATT\_UUID\_ALL

    <a id="_CPPv4N8msg_attc30MST_ATTC_GET_ATT_DESC_UUID_ALLE"></a>

    <a id="_CPPv3N8msg_attc30MST_ATTC_GET_ATT_DESC_UUID_ALLE"></a> <a id="_CPPv2N8msg_attc30MST_ATTC_GET_ATT_DESC_UUID_ALLE"></a> <a id="group__bk__ble__api__v1_1gga0d2f5c239f8dfb71778af9b1c083c7fba5befb9a5f2f8abc2049165b716db0a52"></a> enumerator MST\_ATTC\_GET\_ATT\_DESC\_UUID\_ALL

    <a id="_CPPv4N8msg_attc28MST_ATTC_SVR_ATT_BY_SVR_UUIDE"></a>

    <a id="_CPPv3N8msg_attc28MST_ATTC_SVR_ATT_BY_SVR_UUIDE"></a> <a id="_CPPv2N8msg_attc28MST_ATTC_SVR_ATT_BY_SVR_UUIDE"></a> <a id="group__bk__ble__api__v1_1gga0d2f5c239f8dfb71778af9b1c083c7fba36e59b3b049324509d82ba96d46de3af"></a> enumerator MST\_ATTC\_SVR\_ATT\_BY\_SVR\_UUID

    <a id="_CPPv4N8msg_attc33MST_ATTC_SVR_ATT_DESC_BY_SVR_UUIDE"></a>

    <a id="_CPPv3N8msg_attc33MST_ATTC_SVR_ATT_DESC_BY_SVR_UUIDE"></a> <a id="_CPPv2N8msg_attc33MST_ATTC_SVR_ATT_DESC_BY_SVR_UUIDE"></a> <a id="group__bk__ble__api__v1_1gga0d2f5c239f8dfb71778af9b1c083c7fba32e30f0af1fb1aea03aea509eb016f55"></a> enumerator MST\_ATTC\_SVR\_ATT\_DESC\_BY\_SVR\_UUID

    <a id="_CPPv4N8msg_attc37MST_ATTC_SVR_ATT_AND_DESC_BY_SVR_UUIDE"></a>

    <a id="_CPPv3N8msg_attc37MST_ATTC_SVR_ATT_AND_DESC_BY_SVR_UUIDE"></a> <a id="_CPPv2N8msg_attc37MST_ATTC_SVR_ATT_AND_DESC_BY_SVR_UUIDE"></a> <a id="group__bk__ble__api__v1_1gga0d2f5c239f8dfb71778af9b1c083c7fba0c5322b3d104392cd0ca1cd076998b94"></a> enumerator MST\_ATTC\_SVR\_ATT\_AND\_DESC\_BY\_SVR\_UUID
    :   Gets all ATT-DESC’s for this SVR-UUID for this connection.

<a id="_CPPv415adv_report_type"></a>

<a id="_CPPv315adv_report_type"></a> <a id="_CPPv215adv_report_type"></a> <a id="group__bk__ble__api__v1__typedef_1ga586827f2b8e2c17b183858febd25a205"></a> enum adv\_report\_type
:   *Values:*

    <a id="_CPPv4N15adv_report_type19REPORT_TYPE_ADV_EXTE"></a>

    <a id="_CPPv3N15adv_report_type19REPORT_TYPE_ADV_EXTE"></a> <a id="_CPPv2N15adv_report_type19REPORT_TYPE_ADV_EXTE"></a> <a id="group__bk__ble__api__v1__typedef_1gga586827f2b8e2c17b183858febd25a205a59ad919478107532715a49e6ad75114f"></a> enumerator REPORT\_TYPE\_ADV\_EXT
    :   Extended advertising report.

    <a id="_CPPv4N15adv_report_type19REPORT_TYPE_ADV_LEGE"></a>

    <a id="_CPPv3N15adv_report_type19REPORT_TYPE_ADV_LEGE"></a> <a id="_CPPv2N15adv_report_type19REPORT_TYPE_ADV_LEGE"></a> <a id="group__bk__ble__api__v1__typedef_1gga586827f2b8e2c17b183858febd25a205a44d7aebbbfbbeb34e40de6f4a0e9c9df"></a> enumerator REPORT\_TYPE\_ADV\_LEG
    :   Legacy advertising report.

    <a id="_CPPv4N15adv_report_type24REPORT_TYPE_SCAN_RSP_EXTE"></a>

    <a id="_CPPv3N15adv_report_type24REPORT_TYPE_SCAN_RSP_EXTE"></a> <a id="_CPPv2N15adv_report_type24REPORT_TYPE_SCAN_RSP_EXTE"></a> <a id="group__bk__ble__api__v1__typedef_1gga586827f2b8e2c17b183858febd25a205a76fb8ea453b6ad91445db1586cb43802"></a> enumerator REPORT\_TYPE\_SCAN\_RSP\_EXT
    :   Extended scan response report.

    <a id="_CPPv4N15adv_report_type24REPORT_TYPE_SCAN_RSP_LEGE"></a>

    <a id="_CPPv3N15adv_report_type24REPORT_TYPE_SCAN_RSP_LEGE"></a> <a id="_CPPv2N15adv_report_type24REPORT_TYPE_SCAN_RSP_LEGE"></a> <a id="group__bk__ble__api__v1__typedef_1gga586827f2b8e2c17b183858febd25a205a3706f1a939dcdeffba155441cad99cb1"></a> enumerator REPORT\_TYPE\_SCAN\_RSP\_LEG
    :   Legacy scan response report.

    <a id="_CPPv4N15adv_report_type19REPORT_TYPE_PER_ADVE"></a>

    <a id="_CPPv3N15adv_report_type19REPORT_TYPE_PER_ADVE"></a> <a id="_CPPv2N15adv_report_type19REPORT_TYPE_PER_ADVE"></a> <a id="group__bk__ble__api__v1__typedef_1gga586827f2b8e2c17b183858febd25a205a570e3ca9160eb5704457953f00688f00"></a> enumerator REPORT\_TYPE\_PER\_ADV
    :   Periodic advertising report.

<a id="_CPPv415adv_report_info"></a>

<a id="_CPPv315adv_report_info"></a> <a id="_CPPv215adv_report_info"></a> <a id="group__bk__ble__api__v1__typedef_1ga8648555af760e5e51dcbd0829cb4dd16"></a> enum adv\_report\_info
:   *Values:*

    <a id="_CPPv4N15adv_report_info28REPORT_INFO_REPORT_TYPE_MASKE"></a>

    <a id="_CPPv3N15adv_report_info28REPORT_INFO_REPORT_TYPE_MASKE"></a> <a id="_CPPv2N15adv_report_info28REPORT_INFO_REPORT_TYPE_MASKE"></a> <a id="group__bk__ble__api__v1__typedef_1gga8648555af760e5e51dcbd0829cb4dd16a7f1330821b7bfeba8a4bbf59006b3bd2"></a> enumerator REPORT\_INFO\_REPORT\_TYPE\_MASK
    :   Report Type.

    <a id="_CPPv4N15adv_report_info24REPORT_INFO_COMPLETE_BITE"></a>

    <a id="_CPPv3N15adv_report_info24REPORT_INFO_COMPLETE_BITE"></a> <a id="_CPPv2N15adv_report_info24REPORT_INFO_COMPLETE_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga8648555af760e5e51dcbd0829cb4dd16ad0cdca29003a242c00a3cf8a182fe12f"></a> enumerator REPORT\_INFO\_COMPLETE\_BIT
    :   Report is complete.

    <a id="_CPPv4N15adv_report_info24REPORT_INFO_CONN_ADV_BITE"></a>

    <a id="_CPPv3N15adv_report_info24REPORT_INFO_CONN_ADV_BITE"></a> <a id="_CPPv2N15adv_report_info24REPORT_INFO_CONN_ADV_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga8648555af760e5e51dcbd0829cb4dd16a318b428e1033ec328c35dc9c09411361"></a> enumerator REPORT\_INFO\_CONN\_ADV\_BIT
    :   Connectable advertising.

    <a id="_CPPv4N15adv_report_info24REPORT_INFO_SCAN_ADV_BITE"></a>

    <a id="_CPPv3N15adv_report_info24REPORT_INFO_SCAN_ADV_BITE"></a> <a id="_CPPv2N15adv_report_info24REPORT_INFO_SCAN_ADV_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga8648555af760e5e51dcbd0829cb4dd16a250f38dcce7713b54b3def41b23d6163"></a> enumerator REPORT\_INFO\_SCAN\_ADV\_BIT
    :   Scannable advertising.

    <a id="_CPPv4N15adv_report_info23REPORT_INFO_DIR_ADV_BITE"></a>

    <a id="_CPPv3N15adv_report_info23REPORT_INFO_DIR_ADV_BITE"></a> <a id="_CPPv2N15adv_report_info23REPORT_INFO_DIR_ADV_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga8648555af760e5e51dcbd0829cb4dd16adadb02b6d7a4ad4e31236ea5b5d529fe"></a> enumerator REPORT\_INFO\_DIR\_ADV\_BIT
    :   Directed advertising.

<a id="_CPPv48adv_type"></a>

<a id="_CPPv38adv_type"></a> <a id="_CPPv28adv_type"></a> <a id="group__bk__ble__api__v1__typedef_1ga9dc8280460afec1e78fb24edf38968ec"></a> enum adv\_type
:   Type of advertising that can be created.

    *Values:*

    <a id="_CPPv4N8adv_type15ADV_TYPE_LEGACYE"></a>

    <a id="_CPPv3N8adv_type15ADV_TYPE_LEGACYE"></a> <a id="_CPPv2N8adv_type15ADV_TYPE_LEGACYE"></a> <a id="group__bk__ble__api__v1__typedef_1gga9dc8280460afec1e78fb24edf38968eca1484c4d607906882daa1e1e25f3f0445"></a> enumerator ADV\_TYPE\_LEGACY
    :   Legacy advertising.

    <a id="_CPPv4N8adv_type17ADV_TYPE_EXTENDEDE"></a>

    <a id="_CPPv3N8adv_type17ADV_TYPE_EXTENDEDE"></a> <a id="_CPPv2N8adv_type17ADV_TYPE_EXTENDEDE"></a> <a id="group__bk__ble__api__v1__typedef_1gga9dc8280460afec1e78fb24edf38968eca667aa96d416488694e3a87d503e6181e"></a> enumerator ADV\_TYPE\_EXTENDED
    :   Extended advertising.

    <a id="_CPPv4N8adv_type17ADV_TYPE_PERIODICE"></a>

    <a id="_CPPv3N8adv_type17ADV_TYPE_PERIODICE"></a> <a id="_CPPv2N8adv_type17ADV_TYPE_PERIODICE"></a> <a id="group__bk__ble__api__v1__typedef_1gga9dc8280460afec1e78fb24edf38968eca86ddf30995d689cbd242ea2ff43aa9ba"></a> enumerator ADV\_TYPE\_PERIODIC
    :   Periodic advertising.

<a id="_CPPv411adv_prop_bf"></a>

<a id="_CPPv311adv_prop_bf"></a> <a id="_CPPv211adv_prop_bf"></a> <a id="group__bk__ble__api__v1__typedef_1ga6b5140e1b8fe4043c83c62cbdfdd20c3"></a> enum adv\_prop\_bf
:   Advertising properties bit field bit positions.

    *Values:*

    <a id="_CPPv4N11adv_prop_bf24ADV_PROP_CONNECTABLE_BITE"></a>

    <a id="_CPPv3N11adv_prop_bf24ADV_PROP_CONNECTABLE_BITE"></a> <a id="_CPPv2N11adv_prop_bf24ADV_PROP_CONNECTABLE_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6b5140e1b8fe4043c83c62cbdfdd20c3a984052b2241764d01c3b65db394706ee"></a> enumerator ADV\_PROP\_CONNECTABLE\_BIT
    :   Indicate that advertising is connectable, reception of CONNECT\_REQ or AUX\_CONNECT\_REQ PDUs is accepted. Not applicable for periodic advertising.

    <a id="_CPPv4N11adv_prop_bf22ADV_PROP_SCANNABLE_BITE"></a>

    <a id="_CPPv3N11adv_prop_bf22ADV_PROP_SCANNABLE_BITE"></a> <a id="_CPPv2N11adv_prop_bf22ADV_PROP_SCANNABLE_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6b5140e1b8fe4043c83c62cbdfdd20c3a96cabc80e4f429480b3cb3b4a7dabdfe"></a> enumerator ADV\_PROP\_SCANNABLE\_BIT
    :   Indicate that advertising is scannable, reception of SCAN\_REQ or AUX\_SCAN\_REQ PDUs is accepted

    <a id="_CPPv4N11adv_prop_bf21ADV_PROP_DIRECTED_BITE"></a>

    <a id="_CPPv3N11adv_prop_bf21ADV_PROP_DIRECTED_BITE"></a> <a id="_CPPv2N11adv_prop_bf21ADV_PROP_DIRECTED_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6b5140e1b8fe4043c83c62cbdfdd20c3a688e041835db559dcb8883816ef94ae7"></a> enumerator ADV\_PROP\_DIRECTED\_BIT
    :   Indicate that advertising targets a specific device. Only apply in following cases:

        - Legacy advertising: if connectable
        - Extended advertising: connectable or (non connectable and non discoverable)

    <a id="_CPPv4N11adv_prop_bf16ADV_PROP_HDC_BITE"></a>

    <a id="_CPPv3N11adv_prop_bf16ADV_PROP_HDC_BITE"></a> <a id="_CPPv2N11adv_prop_bf16ADV_PROP_HDC_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6b5140e1b8fe4043c83c62cbdfdd20c3a0dc0b915b1a059b3b87ffecd9a4298f3"></a> enumerator ADV\_PROP\_HDC\_BIT
    :   Indicate that High Duty Cycle has to be used for advertising on primary channel Apply only if created advertising is not an extended advertising

    <a id="_CPPv4N11adv_prop_bf24ADV_PROP_PROP_LEGACY_BITE"></a>

    <a id="_CPPv3N11adv_prop_bf24ADV_PROP_PROP_LEGACY_BITE"></a> <a id="_CPPv2N11adv_prop_bf24ADV_PROP_PROP_LEGACY_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6b5140e1b8fe4043c83c62cbdfdd20c3ac95ae1003bc603b78ba3fa5b6a2e42b9"></a> enumerator ADV\_PROP\_PROP\_LEGACY\_BIT
    :   Use legacy advertising PDUs.

    <a id="_CPPv4N11adv_prop_bf22ADV_PROP_ANONYMOUS_BITE"></a>

    <a id="_CPPv3N11adv_prop_bf22ADV_PROP_ANONYMOUS_BITE"></a> <a id="_CPPv2N11adv_prop_bf22ADV_PROP_ANONYMOUS_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6b5140e1b8fe4043c83c62cbdfdd20c3a3e10c259a29b7487e96e5b43a258f54a"></a> enumerator ADV\_PROP\_ANONYMOUS\_BIT
    :   Enable anonymous mode. Device address won’t appear in send PDUs Valid only if created advertising is an extended advertising

    <a id="_CPPv4N11adv_prop_bf19ADV_PROP_TX_PWR_BITE"></a>

    <a id="_CPPv3N11adv_prop_bf19ADV_PROP_TX_PWR_BITE"></a> <a id="_CPPv2N11adv_prop_bf19ADV_PROP_TX_PWR_BITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6b5140e1b8fe4043c83c62cbdfdd20c3a93482ad3e5cec8729eed91844a2180b6"></a> enumerator ADV\_PROP\_TX\_PWR\_BIT
    :   Include TX Power in the extended header of the advertising PDU. Valid only if created advertising is not a legacy advertising

<a id="_CPPv412adv_chnl_map"></a>

<a id="_CPPv312adv_chnl_map"></a> <a id="_CPPv212adv_chnl_map"></a> <a id="group__bk__ble__api__v1__typedef_1ga57c9e3ee8efb2e8c2fcc35e570f8679a"></a> enum adv\_chnl\_map
:   Advertising channels enables.

    *Values:*

    <a id="_CPPv4N12adv_chnl_map11ADV_CHNL_37E"></a>

    <a id="_CPPv3N12adv_chnl_map11ADV_CHNL_37E"></a> <a id="_CPPv2N12adv_chnl_map11ADV_CHNL_37E"></a> <a id="group__bk__ble__api__v1__typedef_1gga57c9e3ee8efb2e8c2fcc35e570f8679aa5019ec058bd0e2a1e7895261518d029c"></a> enumerator ADV\_CHNL\_37
    :   Byte value for advertising channel map for channel 37 enable.

    <a id="_CPPv4N12adv_chnl_map11ADV_CHNL_38E"></a>

    <a id="_CPPv3N12adv_chnl_map11ADV_CHNL_38E"></a> <a id="_CPPv2N12adv_chnl_map11ADV_CHNL_38E"></a> <a id="group__bk__ble__api__v1__typedef_1gga57c9e3ee8efb2e8c2fcc35e570f8679aae1f1c6ec2492ba7858ad64d749b5dae9"></a> enumerator ADV\_CHNL\_38
    :   Byte value for advertising channel map for channel 38 enable.

    <a id="_CPPv4N12adv_chnl_map11ADV_CHNL_39E"></a>

    <a id="_CPPv3N12adv_chnl_map11ADV_CHNL_39E"></a> <a id="_CPPv2N12adv_chnl_map11ADV_CHNL_39E"></a> <a id="group__bk__ble__api__v1__typedef_1gga57c9e3ee8efb2e8c2fcc35e570f8679aaf09c24430d3cd6436a96d4bfcedce34e"></a> enumerator ADV\_CHNL\_39
    :   Byte value for advertising channel map for channel 39 enable.

    <a id="_CPPv4N12adv_chnl_map13ADV_ALL_CHNLSE"></a>

    <a id="_CPPv3N12adv_chnl_map13ADV_ALL_CHNLSE"></a> <a id="_CPPv2N12adv_chnl_map13ADV_ALL_CHNLSE"></a> <a id="group__bk__ble__api__v1__typedef_1gga57c9e3ee8efb2e8c2fcc35e570f8679aa765fea1b0bce17dd282f807b9fc53a00"></a> enumerator ADV\_ALL\_CHNLS
    :   Byte value for advertising channel map for channel 37, 38 and 39 enable.

<a id="_CPPv411phy_type_le"></a>

<a id="_CPPv311phy_type_le"></a> <a id="_CPPv211phy_type_le"></a> <a id="group__bk__ble__api__v1__typedef_1ga4acd0e053cbeead642d1317913613874"></a> enum phy\_type\_le
:   PHY Type.

    *Values:*

    <a id="_CPPv4N11phy_type_le14PHY_TYPE_LE_1ME"></a>

    <a id="_CPPv3N11phy_type_le14PHY_TYPE_LE_1ME"></a> <a id="_CPPv2N11phy_type_le14PHY_TYPE_LE_1ME"></a> <a id="group__bk__ble__api__v1__typedef_1gga4acd0e053cbeead642d1317913613874ab011c206022d171051175c0a77377c84"></a> enumerator PHY\_TYPE\_LE\_1M
    :   LE 1M.

    <a id="_CPPv4N11phy_type_le14PHY_TYPE_LE_2ME"></a>

    <a id="_CPPv3N11phy_type_le14PHY_TYPE_LE_2ME"></a> <a id="_CPPv2N11phy_type_le14PHY_TYPE_LE_2ME"></a> <a id="group__bk__ble__api__v1__typedef_1gga4acd0e053cbeead642d1317913613874ae4c9d6b43453986dbe6db98ea56350e3"></a> enumerator PHY\_TYPE\_LE\_2M
    :   LE 2M.

    <a id="_CPPv4N11phy_type_le17PHY_TYPE_LE_CODEDE"></a>

    <a id="_CPPv3N11phy_type_le17PHY_TYPE_LE_CODEDE"></a> <a id="_CPPv2N11phy_type_le17PHY_TYPE_LE_CODEDE"></a> <a id="group__bk__ble__api__v1__typedef_1gga4acd0e053cbeead642d1317913613874a041b5c82139db2960ab6b5adf120469f"></a> enumerator PHY\_TYPE\_LE\_CODED
    :   LE Coded.

<a id="_CPPv422initiating_phy_type_le"></a>

<a id="_CPPv322initiating_phy_type_le"></a> <a id="_CPPv222initiating_phy_type_le"></a> <a id="group__bk__ble__api__v1__typedef_1ga016191e9a8530c40e1f0616481c286de"></a> enum initiating\_phy\_type\_le
:   Initiating PHY Type.

    *Values:*

    <a id="_CPPv4N22initiating_phy_type_le19INIT_PHY_TYPE_LE_1ME"></a>

    <a id="_CPPv3N22initiating_phy_type_le19INIT_PHY_TYPE_LE_1ME"></a> <a id="_CPPv2N22initiating_phy_type_le19INIT_PHY_TYPE_LE_1ME"></a> <a id="group__bk__ble__api__v1__typedef_1gga016191e9a8530c40e1f0616481c286dea071f993c59e44e41a79b1dbcb3b75981"></a> enumerator INIT\_PHY\_TYPE\_LE\_1M
    :   LE 1M.

    <a id="_CPPv4N22initiating_phy_type_le19INIT_PHY_TYPE_LE_2ME"></a>

    <a id="_CPPv3N22initiating_phy_type_le19INIT_PHY_TYPE_LE_2ME"></a> <a id="_CPPv2N22initiating_phy_type_le19INIT_PHY_TYPE_LE_2ME"></a> <a id="group__bk__ble__api__v1__typedef_1gga016191e9a8530c40e1f0616481c286dea22a42cbeeff8d2141e8a308485081cd6"></a> enumerator INIT\_PHY\_TYPE\_LE\_2M
    :   LE 2M.

    <a id="_CPPv4N22initiating_phy_type_le22INIT_PHY_TYPE_LE_CODEDE"></a>

    <a id="_CPPv3N22initiating_phy_type_le22INIT_PHY_TYPE_LE_CODEDE"></a> <a id="_CPPv2N22initiating_phy_type_le22INIT_PHY_TYPE_LE_CODEDE"></a> <a id="group__bk__ble__api__v1__typedef_1gga016191e9a8530c40e1f0616481c286dea043d21edc125c554918969c3c3128921"></a> enumerator INIT\_PHY\_TYPE\_LE\_CODED
    :   LE Coded.

<a id="_CPPv417ble_own_addr_type"></a>

<a id="_CPPv317ble_own_addr_type"></a> <a id="_CPPv217ble_own_addr_type"></a> <a id="group__bk__ble__api__v1__typedef_1gaaa7b5c55bc3b207c84e20eca8e0c7223"></a> enum ble\_own\_addr\_type
:   Own addr type.

    *Values:*

    <a id="_CPPv4N17ble_own_addr_type35OWN_ADDR_TYPE_PUBLIC_OR_STATIC_ADDRE"></a>

    <a id="_CPPv3N17ble_own_addr_type35OWN_ADDR_TYPE_PUBLIC_OR_STATIC_ADDRE"></a> <a id="_CPPv2N17ble_own_addr_type35OWN_ADDR_TYPE_PUBLIC_OR_STATIC_ADDRE"></a> <a id="group__bk__ble__api__v1__typedef_1ggaaa7b5c55bc3b207c84e20eca8e0c7223aeaab267da1451e15d2ce73518d28d2af"></a> enumerator OWN\_ADDR\_TYPE\_PUBLIC\_OR\_STATIC\_ADDR
    :   Public or Private Static Address according to device address configuration Attention: Private Static Address is not used now, so set will be public Attention: this enum is derecated, use OWN\_ADDR\_TYPE\_PUBLIC\_ADDR instead.

    <a id="_CPPv4N17ble_own_addr_type37OWN_ADDR_TYPE_GEN_RSLV_OR_RANDOM_ADDRE"></a>

    <a id="_CPPv3N17ble_own_addr_type37OWN_ADDR_TYPE_GEN_RSLV_OR_RANDOM_ADDRE"></a> <a id="_CPPv2N17ble_own_addr_type37OWN_ADDR_TYPE_GEN_RSLV_OR_RANDOM_ADDRE"></a> <a id="group__bk__ble__api__v1__typedef_1ggaaa7b5c55bc3b207c84e20eca8e0c7223a107021a6faa3d66be8dda1f818139b60"></a> enumerator OWN\_ADDR\_TYPE\_GEN\_RSLV\_OR\_RANDOM\_ADDR
    :   Generated resolvable private random or random address, will auto refresh periodic Attention: RPA is not used now, so set will be random

    <a id="_CPPv4N17ble_own_addr_type41OWN_ADDR_TYPE_GEN_NON_RSLV_OR_RANDOM_ADDRE"></a>

    <a id="_CPPv3N17ble_own_addr_type41OWN_ADDR_TYPE_GEN_NON_RSLV_OR_RANDOM_ADDRE"></a> <a id="_CPPv2N17ble_own_addr_type41OWN_ADDR_TYPE_GEN_NON_RSLV_OR_RANDOM_ADDRE"></a> <a id="group__bk__ble__api__v1__typedef_1ggaaa7b5c55bc3b207c84e20eca8e0c7223a9c6a03741c65a51820fb48664849c37c"></a> enumerator OWN\_ADDR\_TYPE\_GEN\_NON\_RSLV\_OR\_RANDOM\_ADDR
    :   Generated non-resolvable private random or random address, will auto refresh periodic Attention: NRPA is not used now, so set will be random

    <a id="_CPPv4N17ble_own_addr_type25OWN_ADDR_TYPE_PUBLIC_ADDRE"></a>

    <a id="_CPPv3N17ble_own_addr_type25OWN_ADDR_TYPE_PUBLIC_ADDRE"></a> <a id="_CPPv2N17ble_own_addr_type25OWN_ADDR_TYPE_PUBLIC_ADDRE"></a> <a id="group__bk__ble__api__v1__typedef_1ggaaa7b5c55bc3b207c84e20eca8e0c7223a0f46389eb0d937a720eee274c2454a23"></a> enumerator OWN\_ADDR\_TYPE\_PUBLIC\_ADDR
    :   public addr

    <a id="_CPPv4N17ble_own_addr_type25OWN_ADDR_TYPE_RANDOM_ADDRE"></a>

    <a id="_CPPv3N17ble_own_addr_type25OWN_ADDR_TYPE_RANDOM_ADDRE"></a> <a id="_CPPv2N17ble_own_addr_type25OWN_ADDR_TYPE_RANDOM_ADDRE"></a> <a id="group__bk__ble__api__v1__typedef_1ggaaa7b5c55bc3b207c84e20eca8e0c7223a2cfd1122299fb3201e3ca0ad83ba519d"></a> enumerator OWN\_ADDR\_TYPE\_RANDOM\_ADDR
    :   use bk\_ble\_set\_adv\_random\_addr addr

<a id="_CPPv425initiating_filter_type_le"></a>

<a id="_CPPv325initiating_filter_type_le"></a> <a id="_CPPv225initiating_filter_type_le"></a> <a id="group__bk__ble__api__v1__typedef_1gaf5be121573ef75ad997530941fa7c99a"></a> enum initiating\_filter\_type\_le
:   *Values:*

    <a id="_CPPv4N25initiating_filter_type_le28INIT_TYPE_LE_DIRECT_CONN_ESTE"></a>

    <a id="_CPPv3N25initiating_filter_type_le28INIT_TYPE_LE_DIRECT_CONN_ESTE"></a> <a id="_CPPv2N25initiating_filter_type_le28INIT_TYPE_LE_DIRECT_CONN_ESTE"></a> <a id="group__bk__ble__api__v1__typedef_1ggaf5be121573ef75ad997530941fa7c99aac544ad8cb2a01c5a2a40d34471120075"></a> enumerator INIT\_TYPE\_LE\_DIRECT\_CONN\_EST
    :   Direct connection establishment, establish a connection with an indicated device.

    <a id="_CPPv4N25initiating_filter_type_le26INIT_TYPE_LE_AUTO_CONN_ESTE"></a>

    <a id="_CPPv3N25initiating_filter_type_le26INIT_TYPE_LE_AUTO_CONN_ESTE"></a> <a id="_CPPv2N25initiating_filter_type_le26INIT_TYPE_LE_AUTO_CONN_ESTE"></a> <a id="group__bk__ble__api__v1__typedef_1ggaf5be121573ef75ad997530941fa7c99aa17c76dea9d272b2d3638f598e6d90e9f"></a> enumerator INIT\_TYPE\_LE\_AUTO\_CONN\_EST
    :   Automatic connection establishment, establish a connection with all devices whose address is present in the white list

    <a id="_CPPv4N25initiating_filter_type_le22INIT_TYPE_LE_NAME_DISCE"></a>

    <a id="_CPPv3N25initiating_filter_type_le22INIT_TYPE_LE_NAME_DISCE"></a> <a id="_CPPv2N25initiating_filter_type_le22INIT_TYPE_LE_NAME_DISCE"></a> <a id="group__bk__ble__api__v1__typedef_1ggaf5be121573ef75ad997530941fa7c99aaf6c7d6fcc30faedd48475a7850ab4997"></a> enumerator INIT\_TYPE\_LE\_NAME\_DISC
    :   Name discovery, Establish a connection with an indicated device in order to read content of its Device Name characteristic. Connection is closed once this operation is stopped.

<a id="_CPPv413ble_scan_type"></a>

<a id="_CPPv313ble_scan_type"></a> <a id="_CPPv213ble_scan_type"></a> <a id="group__bk__ble__api__v1__typedef_1ga364631dfaf59ba0e1df8a02a43fa63d6"></a> enum ble\_scan\_type
:   Scan type.

    *Values:*

    <a id="_CPPv4N13ble_scan_type16PASSIVE_SCANNINGE"></a>

    <a id="_CPPv3N13ble_scan_type16PASSIVE_SCANNINGE"></a> <a id="_CPPv2N13ble_scan_type16PASSIVE_SCANNINGE"></a> <a id="group__bk__ble__api__v1__typedef_1gga364631dfaf59ba0e1df8a02a43fa63d6a97fcce64a6b44d75440726c52ec6f97f"></a> enumerator PASSIVE\_SCANNING
    :   Passive Scanning. No scanning PDUs shall be sent (default)

    <a id="_CPPv4N13ble_scan_type15ACTIVE_SCANNINGE"></a>

    <a id="_CPPv3N13ble_scan_type15ACTIVE_SCANNINGE"></a> <a id="_CPPv2N13ble_scan_type15ACTIVE_SCANNINGE"></a> <a id="group__bk__ble__api__v1__typedef_1gga364631dfaf59ba0e1df8a02a43fa63d6a7860d9176638c54d7ca46b2ecf2785b7"></a> enumerator ACTIVE\_SCANNING
    :   Active scanning. Scanning PDUs may be sent.

<a id="_CPPv422ble_scan_filter_policy"></a>

<a id="_CPPv322ble_scan_filter_policy"></a> <a id="_CPPv222ble_scan_filter_policy"></a> <a id="group__bk__ble__api__v1__typedef_1ga6bbb5b4b01f2f6a60164943eb569795e"></a> enum ble\_scan\_filter\_policy
:   Scan filter policy.

    *Values:*

    <a id="_CPPv4N22ble_scan_filter_policy26BASIC_UNFILTER_SCAN_POLICYE"></a>

    <a id="_CPPv3N22ble_scan_filter_policy26BASIC_UNFILTER_SCAN_POLICYE"></a> <a id="_CPPv2N22ble_scan_filter_policy26BASIC_UNFILTER_SCAN_POLICYE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6bbb5b4b01f2f6a60164943eb569795ea3cf1a230bb224ba096bf985b83cf07f1"></a> enumerator BASIC\_UNFILTER\_SCAN\_POLICY
    :   Basic unfiltered scanning filter policy.

    <a id="_CPPv4N22ble_scan_filter_policy24BASIC_FILTER_SCAN_POLICYE"></a>

    <a id="_CPPv3N22ble_scan_filter_policy24BASIC_FILTER_SCAN_POLICYE"></a> <a id="_CPPv2N22ble_scan_filter_policy24BASIC_FILTER_SCAN_POLICYE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6bbb5b4b01f2f6a60164943eb569795ea8ab18db2ee0d82d69c0882184166773b"></a> enumerator BASIC\_FILTER\_SCAN\_POLICY
    :   Basic filtered scanning filter policy.

    <a id="_CPPv4N22ble_scan_filter_policy27EXTENED_UNFILER_SCAN_POLICYE"></a>

    <a id="_CPPv3N22ble_scan_filter_policy27EXTENED_UNFILER_SCAN_POLICYE"></a> <a id="_CPPv2N22ble_scan_filter_policy27EXTENED_UNFILER_SCAN_POLICYE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6bbb5b4b01f2f6a60164943eb569795eafaad4e1cbebf3a2414c71d9323cc8a47"></a> enumerator EXTENED\_UNFILER\_SCAN\_POLICY
    :   Extended unfiltered scanning filter policy.

    <a id="_CPPv4N22ble_scan_filter_policy25EXTENED_FILER_SCAN_POLICYE"></a>

    <a id="_CPPv3N22ble_scan_filter_policy25EXTENED_FILER_SCAN_POLICYE"></a> <a id="_CPPv2N22ble_scan_filter_policy25EXTENED_FILER_SCAN_POLICYE"></a> <a id="group__bk__ble__api__v1__typedef_1gga6bbb5b4b01f2f6a60164943eb569795eafaa9957843cd3367faf09f5d162d7635"></a> enumerator EXTENED\_FILER\_SCAN\_POLICY
    :   Extended filtered scanning filter policy.

<a id="_CPPv417ble_sync_cte_type"></a>

<a id="_CPPv317ble_sync_cte_type"></a> <a id="_CPPv217ble_sync_cte_type"></a> <a id="group__bk__ble__api__v1__typedef_1ga7249d9eb7c2b2f4a4f56b4c241e6db5f"></a> enum ble\_sync\_cte\_type
:   Constant Tone Extension sync filtering type.

    *Values:*

    <a id="_CPPv4N17ble_sync_cte_type20CTE_NO_SYNC_WITH_AOAE"></a>

    <a id="_CPPv3N17ble_sync_cte_type20CTE_NO_SYNC_WITH_AOAE"></a> <a id="_CPPv2N17ble_sync_cte_type20CTE_NO_SYNC_WITH_AOAE"></a> <a id="group__bk__ble__api__v1__typedef_1gga7249d9eb7c2b2f4a4f56b4c241e6db5faffcb176752b31b7cca43dc72da2bdae2"></a> enumerator CTE\_NO\_SYNC\_WITH\_AOA
    :   Do not sync to packets with an AoA Constant Tone Extension.

    <a id="_CPPv4N17ble_sync_cte_type29CTE_NO_SYNC_WITH_AOD_1US_SLOTE"></a>

    <a id="_CPPv3N17ble_sync_cte_type29CTE_NO_SYNC_WITH_AOD_1US_SLOTE"></a> <a id="_CPPv2N17ble_sync_cte_type29CTE_NO_SYNC_WITH_AOD_1US_SLOTE"></a> <a id="group__bk__ble__api__v1__typedef_1gga7249d9eb7c2b2f4a4f56b4c241e6db5fab8ffe31c3315edd8230de9b3d7dc3ced"></a> enumerator CTE\_NO\_SYNC\_WITH\_AOD\_1US\_SLOT
    :   Do not sync to packets with an AoD Constant Tone Extension with 1 us slots.

    <a id="_CPPv4N17ble_sync_cte_type29CTE_NO_SYNC_WITH_AOD_2US_SLOTE"></a>

    <a id="_CPPv3N17ble_sync_cte_type29CTE_NO_SYNC_WITH_AOD_2US_SLOTE"></a> <a id="_CPPv2N17ble_sync_cte_type29CTE_NO_SYNC_WITH_AOD_2US_SLOTE"></a> <a id="group__bk__ble__api__v1__typedef_1gga7249d9eb7c2b2f4a4f56b4c241e6db5fa0b6c9b189783b7156f5cc69f08b28cd7"></a> enumerator CTE\_NO\_SYNC\_WITH\_AOD\_2US\_SLOT
    :   Do not sync to packets with an AoD Constant Tone Extension with 2 us slots.

    <a id="_CPPv4N17ble_sync_cte_type23CTE_NO_SYNC_WITH_TYPE_3E"></a>

    <a id="_CPPv3N17ble_sync_cte_type23CTE_NO_SYNC_WITH_TYPE_3E"></a> <a id="_CPPv2N17ble_sync_cte_type23CTE_NO_SYNC_WITH_TYPE_3E"></a> <a id="group__bk__ble__api__v1__typedef_1gga7249d9eb7c2b2f4a4f56b4c241e6db5fa4741a8ef436097f7776b316a40c67ce5"></a> enumerator CTE\_NO\_SYNC\_WITH\_TYPE\_3
    :   Do not sync to packets with a type 3 Constant Tone Extension (currently reserved for future use)

    <a id="_CPPv4N17ble_sync_cte_type23CTE_NO_SYNC_WITHOUT_CTEE"></a>

    <a id="_CPPv3N17ble_sync_cte_type23CTE_NO_SYNC_WITHOUT_CTEE"></a> <a id="_CPPv2N17ble_sync_cte_type23CTE_NO_SYNC_WITHOUT_CTEE"></a> <a id="group__bk__ble__api__v1__typedef_1gga7249d9eb7c2b2f4a4f56b4c241e6db5fac545a900f870e08037c81cbe287155bc"></a> enumerator CTE\_NO\_SYNC\_WITHOUT\_CTE
    :   Do not sync to packets without a Constant Tone Extension.

<a id="_CPPv413gap_auth_mask"></a>

<a id="_CPPv313gap_auth_mask"></a> <a id="_CPPv213gap_auth_mask"></a> <a id="group__bk__ble__api__v1__typedef_1ga911a09effea6e7bee0e14e1de9ce92e2"></a> enum gap\_auth\_mask
:   Authentication mask.

    *Values:*

    <a id="_CPPv4N13gap_auth_mask13GAP_AUTH_NONEE"></a>

    <a id="_CPPv3N13gap_auth_mask13GAP_AUTH_NONEE"></a> <a id="_CPPv2N13gap_auth_mask13GAP_AUTH_NONEE"></a> <a id="group__bk__ble__api__v1__typedef_1gga911a09effea6e7bee0e14e1de9ce92e2aee34906a3ee68109b67c93292e0cad24"></a> enumerator GAP\_AUTH\_NONE
    :   No Flag set.

    <a id="_CPPv4N13gap_auth_mask13GAP_AUTH_BONDE"></a>

    <a id="_CPPv3N13gap_auth_mask13GAP_AUTH_BONDE"></a> <a id="_CPPv2N13gap_auth_mask13GAP_AUTH_BONDE"></a> <a id="group__bk__ble__api__v1__typedef_1gga911a09effea6e7bee0e14e1de9ce92e2a1abec2f02b72340592b33c687fe1db20"></a> enumerator GAP\_AUTH\_BOND
    :   Bond authentication.

    <a id="_CPPv4N13gap_auth_mask13GAP_AUTH_MITME"></a>

    <a id="_CPPv3N13gap_auth_mask13GAP_AUTH_MITME"></a> <a id="_CPPv2N13gap_auth_mask13GAP_AUTH_MITME"></a> <a id="group__bk__ble__api__v1__typedef_1gga911a09effea6e7bee0e14e1de9ce92e2ab1f36dbfbf9e7ef5c21a408fdaf81efc"></a> enumerator GAP\_AUTH\_MITM
    :   Man In the middle protection.

    <a id="_CPPv4N13gap_auth_mask16GAP_AUTH_SEC_CONE"></a>

    <a id="_CPPv3N13gap_auth_mask16GAP_AUTH_SEC_CONE"></a> <a id="_CPPv2N13gap_auth_mask16GAP_AUTH_SEC_CONE"></a> <a id="group__bk__ble__api__v1__typedef_1gga911a09effea6e7bee0e14e1de9ce92e2ac41f63724b17519ddd097a1a569e8fa0"></a> enumerator GAP\_AUTH\_SEC\_CON
    :   Secure Connection.

    <a id="_CPPv4N13gap_auth_mask18GAP_AUTH_KEY_NOTIFE"></a>

    <a id="_CPPv3N13gap_auth_mask18GAP_AUTH_KEY_NOTIFE"></a> <a id="_CPPv2N13gap_auth_mask18GAP_AUTH_KEY_NOTIFE"></a> <a id="group__bk__ble__api__v1__typedef_1gga911a09effea6e7bee0e14e1de9ce92e2aefb49a1256845c0cb3959ebc5b7c968b"></a> enumerator GAP\_AUTH\_KEY\_NOTIF
    :   Key Notification.

<a id="_CPPv48gap_auth"></a>

<a id="_CPPv38gap_auth"></a> <a id="_CPPv28gap_auth"></a> <a id="group__bk__ble__api__v1__typedef_1gabddf59399b398b7d0cdb34f77becadb8"></a> enum gap\_auth
:   *Values:*

    <a id="_CPPv4N8gap_auth28GAP_AUTH_REQ_NO_MITM_NO_BONDE"></a>

    <a id="_CPPv3N8gap_auth28GAP_AUTH_REQ_NO_MITM_NO_BONDE"></a> <a id="_CPPv2N8gap_auth28GAP_AUTH_REQ_NO_MITM_NO_BONDE"></a> <a id="group__bk__ble__api__v1__typedef_1ggabddf59399b398b7d0cdb34f77becadb8ac4aba04277037bac5ec5d8d9668ae657"></a> enumerator GAP\_AUTH\_REQ\_NO\_MITM\_NO\_BOND
    :   No MITM No Bonding.

    <a id="_CPPv4N8gap_auth25GAP_AUTH_REQ_NO_MITM_BONDE"></a>

    <a id="_CPPv3N8gap_auth25GAP_AUTH_REQ_NO_MITM_BONDE"></a> <a id="_CPPv2N8gap_auth25GAP_AUTH_REQ_NO_MITM_BONDE"></a> <a id="group__bk__ble__api__v1__typedef_1ggabddf59399b398b7d0cdb34f77becadb8ad3e559d487eb420f2ea7dae398566a50"></a> enumerator GAP\_AUTH\_REQ\_NO\_MITM\_BOND
    :   No MITM Bonding.

    <a id="_CPPv4N8gap_auth25GAP_AUTH_REQ_MITM_NO_BONDE"></a>

    <a id="_CPPv3N8gap_auth25GAP_AUTH_REQ_MITM_NO_BONDE"></a> <a id="_CPPv2N8gap_auth25GAP_AUTH_REQ_MITM_NO_BONDE"></a> <a id="group__bk__ble__api__v1__typedef_1ggabddf59399b398b7d0cdb34f77becadb8afdeda86ae5a14395edefa75a302fd899"></a> enumerator GAP\_AUTH\_REQ\_MITM\_NO\_BOND
    :   MITM No Bonding.

    <a id="_CPPv4N8gap_auth22GAP_AUTH_REQ_MITM_BONDE"></a>

    <a id="_CPPv3N8gap_auth22GAP_AUTH_REQ_MITM_BONDE"></a> <a id="_CPPv2N8gap_auth22GAP_AUTH_REQ_MITM_BONDE"></a> <a id="group__bk__ble__api__v1__typedef_1ggabddf59399b398b7d0cdb34f77becadb8acab77d5a0652d6d7a8a7fd78478304d9"></a> enumerator GAP\_AUTH\_REQ\_MITM\_BOND
    :   MITM and Bonding.

    <a id="_CPPv4N8gap_auth28GAP_AUTH_REQ_SEC_CON_NO_BONDE"></a>

    <a id="_CPPv3N8gap_auth28GAP_AUTH_REQ_SEC_CON_NO_BONDE"></a> <a id="_CPPv2N8gap_auth28GAP_AUTH_REQ_SEC_CON_NO_BONDE"></a> <a id="group__bk__ble__api__v1__typedef_1ggabddf59399b398b7d0cdb34f77becadb8afc97985dc697ac951b57b1a37219b542"></a> enumerator GAP\_AUTH\_REQ\_SEC\_CON\_NO\_BOND
    :   SEC\_CON and No Bonding.

    <a id="_CPPv4N8gap_auth25GAP_AUTH_REQ_SEC_CON_BONDE"></a>

    <a id="_CPPv3N8gap_auth25GAP_AUTH_REQ_SEC_CON_BONDE"></a> <a id="_CPPv2N8gap_auth25GAP_AUTH_REQ_SEC_CON_BONDE"></a> <a id="group__bk__ble__api__v1__typedef_1ggabddf59399b398b7d0cdb34f77becadb8a19fb7a7aafcdafc43587043c01111d5e"></a> enumerator GAP\_AUTH\_REQ\_SEC\_CON\_BOND
    :   SEC\_CON and Bonding.

    <a id="_CPPv4N8gap_auth17GAP_AUTH_REQ_LASTE"></a>

    <a id="_CPPv3N8gap_auth17GAP_AUTH_REQ_LASTE"></a> <a id="_CPPv2N8gap_auth17GAP_AUTH_REQ_LASTE"></a> <a id="group__bk__ble__api__v1__typedef_1ggabddf59399b398b7d0cdb34f77becadb8aad1781703b9196073699e3c920b808ee"></a> enumerator GAP\_AUTH\_REQ\_LAST

    <a id="_CPPv4N8gap_auth17GAP_AUTH_REQ_MASKE"></a>

    <a id="_CPPv3N8gap_auth17GAP_AUTH_REQ_MASKE"></a> <a id="_CPPv2N8gap_auth17GAP_AUTH_REQ_MASKE"></a> <a id="group__bk__ble__api__v1__typedef_1ggabddf59399b398b7d0cdb34f77becadb8a43e44e749147dd098d76822b5d1e9ccb"></a> enumerator GAP\_AUTH\_REQ\_MASK
    :   Mask of authentication features without reserved flag.

<a id="_CPPv417bk_ble_gap_io_cap"></a>

<a id="_CPPv317bk_ble_gap_io_cap"></a> <a id="_CPPv217bk_ble_gap_io_cap"></a> <a id="group__bk__ble__api__v1__typedef_1ga47c2938c3450762bfc853c0891ce35d4"></a> enum bk\_ble\_gap\_io\_cap
:   IO Capability Values.

    *Values:*

    <a id="_CPPv4N17bk_ble_gap_io_cap30BK_BLE_GAP_IO_CAP_DISPLAY_ONLYE"></a>

    <a id="_CPPv3N17bk_ble_gap_io_cap30BK_BLE_GAP_IO_CAP_DISPLAY_ONLYE"></a> <a id="_CPPv2N17bk_ble_gap_io_cap30BK_BLE_GAP_IO_CAP_DISPLAY_ONLYE"></a> <a id="group__bk__ble__api__v1__typedef_1gga47c2938c3450762bfc853c0891ce35d4ad9d174c2094e3c7d45b2f49c9f349a5a"></a> enumerator BK\_BLE\_GAP\_IO\_CAP\_DISPLAY\_ONLY
    :   Display Only.

    <a id="_CPPv4N17bk_ble_gap_io_cap32BK_BLE_GAP_IO_CAP_DISPLAY_YES_NOE"></a>

    <a id="_CPPv3N17bk_ble_gap_io_cap32BK_BLE_GAP_IO_CAP_DISPLAY_YES_NOE"></a> <a id="_CPPv2N17bk_ble_gap_io_cap32BK_BLE_GAP_IO_CAP_DISPLAY_YES_NOE"></a> <a id="group__bk__ble__api__v1__typedef_1gga47c2938c3450762bfc853c0891ce35d4add74d254d473140bad12f45e70bbf57e"></a> enumerator BK\_BLE\_GAP\_IO\_CAP\_DISPLAY\_YES\_NO
    :   Display Yes No.

    <a id="_CPPv4N17bk_ble_gap_io_cap25BK_BLE_GAP_IO_CAP_KB_ONLYE"></a>

    <a id="_CPPv3N17bk_ble_gap_io_cap25BK_BLE_GAP_IO_CAP_KB_ONLYE"></a> <a id="_CPPv2N17bk_ble_gap_io_cap25BK_BLE_GAP_IO_CAP_KB_ONLYE"></a> <a id="group__bk__ble__api__v1__typedef_1gga47c2938c3450762bfc853c0891ce35d4a46da585170227dfb4d4ccb519be70b56"></a> enumerator BK\_BLE\_GAP\_IO\_CAP\_KB\_ONLY
    :   Keyboard Only.

    <a id="_CPPv4N17bk_ble_gap_io_cap36BK_BLE_GAP_IO_CAP_NO_INPUT_NO_OUTPUTE"></a>

    <a id="_CPPv3N17bk_ble_gap_io_cap36BK_BLE_GAP_IO_CAP_NO_INPUT_NO_OUTPUTE"></a> <a id="_CPPv2N17bk_ble_gap_io_cap36BK_BLE_GAP_IO_CAP_NO_INPUT_NO_OUTPUTE"></a> <a id="group__bk__ble__api__v1__typedef_1gga47c2938c3450762bfc853c0891ce35d4aeab0e7b5d65a2a4a7148a6212b6e6d48"></a> enumerator BK\_BLE\_GAP\_IO\_CAP\_NO\_INPUT\_NO\_OUTPUT
    :   No Input No Output.

    <a id="_CPPv4N17bk_ble_gap_io_cap28BK_BLE_GAP_IO_CAP_KB_DISPLAYE"></a>

    <a id="_CPPv3N17bk_ble_gap_io_cap28BK_BLE_GAP_IO_CAP_KB_DISPLAYE"></a> <a id="_CPPv2N17bk_ble_gap_io_cap28BK_BLE_GAP_IO_CAP_KB_DISPLAYE"></a> <a id="group__bk__ble__api__v1__typedef_1gga47c2938c3450762bfc853c0891ce35d4a2dea1339854fb70450b06904b1384939"></a> enumerator BK\_BLE\_GAP\_IO\_CAP\_KB\_DISPLAY
    :   Keyboard Display.

    <a id="_CPPv4N17bk_ble_gap_io_cap22BK_BLE_GAP_IO_CAP_LASTE"></a>

    <a id="_CPPv3N17bk_ble_gap_io_cap22BK_BLE_GAP_IO_CAP_LASTE"></a> <a id="_CPPv2N17bk_ble_gap_io_cap22BK_BLE_GAP_IO_CAP_LASTE"></a> <a id="group__bk__ble__api__v1__typedef_1gga47c2938c3450762bfc853c0891ce35d4ac302d373a79219aa2367625531f40a80"></a> enumerator BK\_BLE\_GAP\_IO\_CAP\_LAST

<a id="_CPPv411gap_sec_req"></a>

<a id="_CPPv311gap_sec_req"></a> <a id="_CPPv211gap_sec_req"></a> <a id="group__bk__ble__api__v1__typedef_1ga5bdf085cbe078d063965de5462611445"></a> enum gap\_sec\_req
:   Security Defines.

    *Values:*

    <a id="_CPPv4N11gap_sec_req10GAP_NO_SECE"></a>

    <a id="_CPPv3N11gap_sec_req10GAP_NO_SECE"></a> <a id="_CPPv2N11gap_sec_req10GAP_NO_SECE"></a> <a id="group__bk__ble__api__v1__typedef_1gga5bdf085cbe078d063965de5462611445ad0af542571980627ce32404a067e23b1"></a> enumerator GAP\_NO\_SEC
    :   No security (no authentication and encryption)

    <a id="_CPPv4N11gap_sec_req24GAP_SEC1_NOAUTH_PAIR_ENCE"></a>

    <a id="_CPPv3N11gap_sec_req24GAP_SEC1_NOAUTH_PAIR_ENCE"></a> <a id="_CPPv2N11gap_sec_req24GAP_SEC1_NOAUTH_PAIR_ENCE"></a> <a id="group__bk__ble__api__v1__typedef_1gga5bdf085cbe078d063965de5462611445ae553513b59fee763c9634a779f814f1f"></a> enumerator GAP\_SEC1\_NOAUTH\_PAIR\_ENC
    :   Unauthenticated pairing with encryption.

    <a id="_CPPv4N11gap_sec_req22GAP_SEC1_AUTH_PAIR_ENCE"></a>

    <a id="_CPPv3N11gap_sec_req22GAP_SEC1_AUTH_PAIR_ENCE"></a> <a id="_CPPv2N11gap_sec_req22GAP_SEC1_AUTH_PAIR_ENCE"></a> <a id="group__bk__ble__api__v1__typedef_1gga5bdf085cbe078d063965de5462611445abcf255ee894be1d663e86d3fcc48dad5"></a> enumerator GAP\_SEC1\_AUTH\_PAIR\_ENC
    :   Authenticated pairing with encryption.

    <a id="_CPPv4N11gap_sec_req24GAP_SEC2_NOAUTH_DATA_SGNE"></a>

    <a id="_CPPv3N11gap_sec_req24GAP_SEC2_NOAUTH_DATA_SGNE"></a> <a id="_CPPv2N11gap_sec_req24GAP_SEC2_NOAUTH_DATA_SGNE"></a> <a id="group__bk__ble__api__v1__typedef_1gga5bdf085cbe078d063965de5462611445ad94fae22059a320c3f68e2768ad14ae6"></a> enumerator GAP\_SEC2\_NOAUTH\_DATA\_SGN
    :   Unauthenticated pairing with data signing.

    <a id="_CPPv4N11gap_sec_req22GAP_SEC2_AUTH_DATA_SGNE"></a>

    <a id="_CPPv3N11gap_sec_req22GAP_SEC2_AUTH_DATA_SGNE"></a> <a id="_CPPv2N11gap_sec_req22GAP_SEC2_AUTH_DATA_SGNE"></a> <a id="group__bk__ble__api__v1__typedef_1gga5bdf085cbe078d063965de5462611445ab8df9063d4930f0a60ff80c623704597"></a> enumerator GAP\_SEC2\_AUTH\_DATA\_SGN
    :   Authentication pairing with data signing.

    <a id="_CPPv4N11gap_sec_req25GAP_SEC1_SEC_CON_PAIR_ENCE"></a>

    <a id="_CPPv3N11gap_sec_req25GAP_SEC1_SEC_CON_PAIR_ENCE"></a> <a id="_CPPv2N11gap_sec_req25GAP_SEC1_SEC_CON_PAIR_ENCE"></a> <a id="group__bk__ble__api__v1__typedef_1gga5bdf085cbe078d063965de5462611445a4cf0120640cce2cfd5331e5e6745330d"></a> enumerator GAP\_SEC1\_SEC\_CON\_PAIR\_ENC
    :   Secure Connection pairing with encryption.

<a id="_CPPv47gap_oob"></a>

<a id="_CPPv37gap_oob"></a> <a id="_CPPv27gap_oob"></a> <a id="group__bk__ble__api__v1__typedef_1ga009fe656dba3e223453288e3fc6fa68c"></a> enum gap\_oob
:   OOB Data Present Flag Values.

    *Values:*

    <a id="_CPPv4N7gap_oob29GAP_OOB_AUTH_DATA_NOT_PRESENTE"></a>

    <a id="_CPPv3N7gap_oob29GAP_OOB_AUTH_DATA_NOT_PRESENTE"></a> <a id="_CPPv2N7gap_oob29GAP_OOB_AUTH_DATA_NOT_PRESENTE"></a> <a id="group__bk__ble__api__v1__typedef_1gga009fe656dba3e223453288e3fc6fa68cade9fd19ae99db1b0b5cd9ef872b1971f"></a> enumerator GAP\_OOB\_AUTH\_DATA\_NOT\_PRESENT
    :   OOB Data not present.

    <a id="_CPPv4N7gap_oob25GAP_OOB_AUTH_DATA_PRESENTE"></a>

    <a id="_CPPv3N7gap_oob25GAP_OOB_AUTH_DATA_PRESENTE"></a> <a id="_CPPv2N7gap_oob25GAP_OOB_AUTH_DATA_PRESENTE"></a> <a id="group__bk__ble__api__v1__typedef_1gga009fe656dba3e223453288e3fc6fa68cad6b453c05c5531e763bb06136744190c"></a> enumerator GAP\_OOB\_AUTH\_DATA\_PRESENT
    :   OOB data present.

    <a id="_CPPv4N7gap_oob22GAP_OOB_AUTH_DATA_LASTE"></a>

    <a id="_CPPv3N7gap_oob22GAP_OOB_AUTH_DATA_LASTE"></a> <a id="_CPPv2N7gap_oob22GAP_OOB_AUTH_DATA_LASTE"></a> <a id="group__bk__ble__api__v1__typedef_1gga009fe656dba3e223453288e3fc6fa68ca5f1ad604f71648ced05467cf2e6a871b"></a> enumerator GAP\_OOB\_AUTH\_DATA\_LAST

<a id="_CPPv413gap_key_distr"></a>

<a id="_CPPv313gap_key_distr"></a> <a id="_CPPv213gap_key_distr"></a> <a id="group__bk__ble__api__v1__typedef_1gada76f561ffe9e3ccfe49d34dfa809026"></a> enum gap\_key\_distr
:   key distr

    *Values:*

    <a id="_CPPv4N13gap_key_distr21BK_BLE_GAP_KDIST_NONEE"></a>

    <a id="_CPPv3N13gap_key_distr21BK_BLE_GAP_KDIST_NONEE"></a> <a id="_CPPv2N13gap_key_distr21BK_BLE_GAP_KDIST_NONEE"></a> <a id="group__bk__ble__api__v1__typedef_1ggada76f561ffe9e3ccfe49d34dfa809026a4943f14ce85da295db4cd5506ef96efb"></a> enumerator BK\_BLE\_GAP\_KDIST\_NONE
    :   No Keys to distribute.

    <a id="_CPPv4N13gap_key_distr23BK_BLE_GAP_KDIST_ENCKEYE"></a>

    <a id="_CPPv3N13gap_key_distr23BK_BLE_GAP_KDIST_ENCKEYE"></a> <a id="_CPPv2N13gap_key_distr23BK_BLE_GAP_KDIST_ENCKEYE"></a> <a id="group__bk__ble__api__v1__typedef_1ggada76f561ffe9e3ccfe49d34dfa809026a66354868d9a686a6dba73433c2138d9a"></a> enumerator BK\_BLE\_GAP\_KDIST\_ENCKEY
    :   Encryption key in distribution.

    <a id="_CPPv4N13gap_key_distr22BK_BLE_GAP_KDIST_IDKEYE"></a>

    <a id="_CPPv3N13gap_key_distr22BK_BLE_GAP_KDIST_IDKEYE"></a> <a id="_CPPv2N13gap_key_distr22BK_BLE_GAP_KDIST_IDKEYE"></a> <a id="group__bk__ble__api__v1__typedef_1ggada76f561ffe9e3ccfe49d34dfa809026a71be8146fff073334755a35a40495043"></a> enumerator BK\_BLE\_GAP\_KDIST\_IDKEY
    :   IRK (ID key)in distribution.

    <a id="_CPPv4N13gap_key_distr24BK_BLE_GAP_KDIST_SIGNKEYE"></a>

    <a id="_CPPv3N13gap_key_distr24BK_BLE_GAP_KDIST_SIGNKEYE"></a> <a id="_CPPv2N13gap_key_distr24BK_BLE_GAP_KDIST_SIGNKEYE"></a> <a id="group__bk__ble__api__v1__typedef_1ggada76f561ffe9e3ccfe49d34dfa809026a39871718f9cae2dfe278e60418ebeaa7"></a> enumerator BK\_BLE\_GAP\_KDIST\_SIGNKEY
    :   CSRK(Signature key) in distribution.

    <a id="_CPPv4N13gap_key_distr24BK_BLE_GAP_KDIST_LINKKEYE"></a>

    <a id="_CPPv3N13gap_key_distr24BK_BLE_GAP_KDIST_LINKKEYE"></a> <a id="_CPPv2N13gap_key_distr24BK_BLE_GAP_KDIST_LINKKEYE"></a> <a id="group__bk__ble__api__v1__typedef_1ggada76f561ffe9e3ccfe49d34dfa809026a9251489ea08f5024506c0f89758957e5"></a> enumerator BK\_BLE\_GAP\_KDIST\_LINKKEY
    :   LTK in distribution.

    <a id="_CPPv4N13gap_key_distr21BK_BLE_GAP_KDIST_LASTE"></a>

    <a id="_CPPv3N13gap_key_distr21BK_BLE_GAP_KDIST_LASTE"></a> <a id="_CPPv2N13gap_key_distr21BK_BLE_GAP_KDIST_LASTE"></a> <a id="group__bk__ble__api__v1__typedef_1ggada76f561ffe9e3ccfe49d34dfa809026a51c0865a3c734273dec07f9eba237730"></a> enumerator BK\_BLE\_GAP\_KDIST\_LAST

<a id="_CPPv48coc_info"></a>

<a id="_CPPv38coc_info"></a> <a id="_CPPv28coc_info"></a> <a id="group__bk__ble__api__v1__typedef_1ga1aa59926ff66b792c420003e4ccfde32"></a> enum coc\_info
:   COC channel information type, used as the “type” parameter of [bk\_ble\_coc\_get\_current\_info()](#group__bk__ble__api__v1_1ga76a6914163e03be37e34be115d51d7fa)

    *Values:*

    <a id="_CPPv4N8coc_info30BK_BLE_COC_PEER_CURRENT_CREDITE"></a>

    <a id="_CPPv3N8coc_info30BK_BLE_COC_PEER_CURRENT_CREDITE"></a> <a id="_CPPv2N8coc_info30BK_BLE_COC_PEER_CURRENT_CREDITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga1aa59926ff66b792c420003e4ccfde32aeb5cae2753b19b076858b7d18469419f"></a> enumerator BK\_BLE\_COC\_PEER\_CURRENT\_CREDIT
    :   Peer’s current available credits.

    <a id="_CPPv4N8coc_info26BK_BLE_COC_PEER_MAX_CREDITE"></a>

    <a id="_CPPv3N8coc_info26BK_BLE_COC_PEER_MAX_CREDITE"></a> <a id="_CPPv2N8coc_info26BK_BLE_COC_PEER_MAX_CREDITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga1aa59926ff66b792c420003e4ccfde32ad514cced76152c05ac65525a1173f914"></a> enumerator BK\_BLE\_COC\_PEER\_MAX\_CREDIT
    :   Peer’s maximum credits.

    <a id="_CPPv4N8coc_info19BK_BLE_COC_PEER_MTUE"></a>

    <a id="_CPPv3N8coc_info19BK_BLE_COC_PEER_MTUE"></a> <a id="_CPPv2N8coc_info19BK_BLE_COC_PEER_MTUE"></a> <a id="group__bk__ble__api__v1__typedef_1gga1aa59926ff66b792c420003e4ccfde32a1ad4a42d29b885265efdd3422f3d7288"></a> enumerator BK\_BLE\_COC\_PEER\_MTU
    :   Peer’s Maximum Transmission Unit size.

    <a id="_CPPv4N8coc_info19BK_BLE_COC_PEER_MPSE"></a>

    <a id="_CPPv3N8coc_info19BK_BLE_COC_PEER_MPSE"></a> <a id="_CPPv2N8coc_info19BK_BLE_COC_PEER_MPSE"></a> <a id="group__bk__ble__api__v1__typedef_1gga1aa59926ff66b792c420003e4ccfde32a03096fc7e39e58788728185d3ffae887"></a> enumerator BK\_BLE\_COC\_PEER\_MPS
    :   Peer’s Maximum PDU Payload Size.

    <a id="_CPPv4N8coc_info31BK_BLE_COC_LOCAL_CURRENT_CREDITE"></a>

    <a id="_CPPv3N8coc_info31BK_BLE_COC_LOCAL_CURRENT_CREDITE"></a> <a id="_CPPv2N8coc_info31BK_BLE_COC_LOCAL_CURRENT_CREDITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga1aa59926ff66b792c420003e4ccfde32abebf14ba9723b642e9eee8d28df537bd"></a> enumerator BK\_BLE\_COC\_LOCAL\_CURRENT\_CREDIT
    :   Local current available credits.

    <a id="_CPPv4N8coc_info27BK_BLE_COC_LOCAL_MAX_CREDITE"></a>

    <a id="_CPPv3N8coc_info27BK_BLE_COC_LOCAL_MAX_CREDITE"></a> <a id="_CPPv2N8coc_info27BK_BLE_COC_LOCAL_MAX_CREDITE"></a> <a id="group__bk__ble__api__v1__typedef_1gga1aa59926ff66b792c420003e4ccfde32aeaf21e6a7010e6160f62b8634fbef37d"></a> enumerator BK\_BLE\_COC\_LOCAL\_MAX\_CREDIT
    :   Local maximum credits.

    <a id="_CPPv4N8coc_info20BK_BLE_COC_LOCAL_MTUE"></a>

    <a id="_CPPv3N8coc_info20BK_BLE_COC_LOCAL_MTUE"></a> <a id="_CPPv2N8coc_info20BK_BLE_COC_LOCAL_MTUE"></a> <a id="group__bk__ble__api__v1__typedef_1gga1aa59926ff66b792c420003e4ccfde32a34fec96b2da75d0ec61cca55fd51dde3"></a> enumerator BK\_BLE\_COC\_LOCAL\_MTU
    :   Local Maximum Transmission Unit size.

    <a id="_CPPv4N8coc_info20BK_BLE_COC_LOCAL_MPSE"></a>

    <a id="_CPPv3N8coc_info20BK_BLE_COC_LOCAL_MPSE"></a> <a id="_CPPv2N8coc_info20BK_BLE_COC_LOCAL_MPSE"></a> <a id="group__bk__ble__api__v1__typedef_1gga1aa59926ff66b792c420003e4ccfde32a6933cd9799de75f62807a1ae8c722cce"></a> enumerator BK\_BLE\_COC\_LOCAL\_MPS
    :   Local Maximum PDU Payload Size.

<a id="_CPPv412coc_security"></a>

<a id="_CPPv312coc_security"></a> <a id="_CPPv212coc_security"></a> <a id="group__bk__ble__api__v1__typedef_1gae54b2f55d6f04060095afbb560fad330"></a> enum coc\_security
:   COC channel required security level, used as the “sec\_lvl” parameter of [bk\_ble\_coc\_config()](#group__bk__ble__api__v1_1gaa6ea432af0aebd14ff87299224998f78)

    *Values:*

    <a id="_CPPv4N12coc_security19BK_BLE_COC_SEC_NONEE"></a>

    <a id="_CPPv3N12coc_security19BK_BLE_COC_SEC_NONEE"></a> <a id="_CPPv2N12coc_security19BK_BLE_COC_SEC_NONEE"></a> <a id="group__bk__ble__api__v1__typedef_1ggae54b2f55d6f04060095afbb560fad330af583cad3561ed91bfc24c8908e6b8d61"></a> enumerator BK\_BLE\_COC\_SEC\_NONE
    :   No security.

    <a id="_CPPv4N12coc_security29BK_BLE_COC_SEC_UNAUTH_ENCRYPTE"></a>

    <a id="_CPPv3N12coc_security29BK_BLE_COC_SEC_UNAUTH_ENCRYPTE"></a> <a id="_CPPv2N12coc_security29BK_BLE_COC_SEC_UNAUTH_ENCRYPTE"></a> <a id="group__bk__ble__api__v1__typedef_1ggae54b2f55d6f04060095afbb560fad330a8d31af04bd13eedf0584789de995204b"></a> enumerator BK\_BLE\_COC\_SEC\_UNAUTH\_ENCRYPT
    :   Unauthenticated encryption.

    <a id="_CPPv4N12coc_security27BK_BLE_COC_SEC_AUTH_ENCRYPTE"></a>

    <a id="_CPPv3N12coc_security27BK_BLE_COC_SEC_AUTH_ENCRYPTE"></a> <a id="_CPPv2N12coc_security27BK_BLE_COC_SEC_AUTH_ENCRYPTE"></a> <a id="group__bk__ble__api__v1__typedef_1ggae54b2f55d6f04060095afbb560fad330a431dcc856d9adc9c3f2f648b44b1d124"></a> enumerator BK\_BLE\_COC\_SEC\_AUTH\_ENCRYPT
    :   Authenticated encryption.

    <a id="_CPPv4N12coc_security32BK_BLE_COC_SEC_SECURE_CONNECTIONE"></a>

    <a id="_CPPv3N12coc_security32BK_BLE_COC_SEC_SECURE_CONNECTIONE"></a> <a id="_CPPv2N12coc_security32BK_BLE_COC_SEC_SECURE_CONNECTIONE"></a> <a id="group__bk__ble__api__v1__typedef_1ggae54b2f55d6f04060095afbb560fad330a0a50eb23d9ab52209b7418eb5c2f747e"></a> enumerator BK\_BLE\_COC\_SEC\_SECURE\_CONNECTION
    :   LE Secure Connections.

<a id="id7"></a>

## 参考链接

> [API 参考：](../bluetooth.md) 介绍蓝牙 API 接口。
>
> [蓝牙开发者指南：](../../developer-guide/bluetooth.md) 介绍蓝牙开发者指南。
>
> [示例和演示：](../../examples/cli/bluetooth.md) 介绍蓝牙示例的使用和操作说明。
