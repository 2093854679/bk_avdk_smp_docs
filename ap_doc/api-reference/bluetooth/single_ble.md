# BLE API



## BLE API 分类

BLE API 主要包括以下类型：

按功能划分的 BLE API：
:   - BLE 公共接口

    - BLE 扫描接口

    - BLE 广播接口

    - BLE 连接接口


## 兼容性和扩展性

BLE API 具备较好的扩展性和向后兼容性。多数 BLE 配置结构体中预留了字段，便于后续扩展。使用这些 API 时，应将预留字段初始化为 0，避免后续新增字段后影响兼容性。


## 编程原则

重要

使用 BLE API 时建议遵循以下原则：
:   - 配置结构体中的预留字段应初始化为 0。

    - 使用 `BK_ERR_CHECK` 检查 BLE API 的返回值。

    - 不确定 API 用法时，优先参考 BLE 示例代码。

    - 不确定配置结构体字段如何初始化时，先使用默认配置宏，再按应用需求修改相关字段。

    - 不建议在 BLE 事件回调中执行耗时操作，可将事件转发到应用任务中处理。


## 事件处理机制

Beken BLE driver 采用事件驱动方式工作。应用通过 BLE API 发起扫描、广播、连接、ATT 数据库访问等操作，并在 BLE 事件回调中获取状态变化和操作结果。


## API 参考


## bk_ble.h

`bk_ble.h` 提供传统 BLE 的扫描、广播、连接和 ATT 数据库等接口。


### Header File


- [bluetooth/bk_ble.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_ble.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_ble.h")


### Functions

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_create_db(struct [bk_ble_db_cfg](#_CPPv413bk_ble_db_cfg "bk_ble_db_cfg") *ble_db_cfg)
:   Register a gatt service.

    User example: First we must build test_service_db test_service_db is a database for att, which used in ble discovery. reading writing and other operation is used on a att database.

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

    TEST_IDX_SVC is nessecery, is declare a primary att service. The macro define is:

    ```
    #define DECL_PRIMARY_SERVICE_128     {0x00,0x28,0}
    ```

    which is an UUID say it is a “primary service” [BK_BLE_PERM_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b") means it can be read, and must be read, so it can be discove by peer master.

    TEST_IDX_CHAR_DECL declare a characteristic as a element in service, it must be [BK_BLE_PERM_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b")

    ```
    #define DECL_CHARACTERISTIC_128      {0x03,0x28,0}
    ```

    show it’s a “characteristic”

    [BK_BLE_PERM_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b") means it can be read, and must be read, so it can be discove by peer master.

    TEST_IDX_CHAR_VALUE is the real value of TEST_IDX_CHAR_DECL, {0x34, 0x12, 0} means it’s type is 0x1234, you can determine by you self [BK_BLE_PERM_SET(NTF, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b") means it cant notify peer, such as value change. For exzample, BLE mouse report pos by “notify” peer. [BK_BLE_PERM_SET(RI, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b") means if peer read this att record, it will enable notification. [BK_BLE_PERM_SET(UUID_LEN, UUID_16)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b") means the first elem’s max len of TEST_IDX_CHAR_VALUE.

    TEST_IDX_CHAR_DESC is a Client Characteristic Configuration Descriptor for TEST_IDX_CHAR_VALUE, it used by peer master as know as a client. As common usage, it config TEST_IDX_CHAR_VALUE indication or notification. Peer can write this att handle to triggle it. Must be [BK_BLE_PERM_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b") | [BK_BLE_PERM_SET(WRITE_REQ, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b")

    Now, you have a basic database for peer, in this case, peer write TEST_IDX_CHAR_DESC or read TEST_IDX_CHAR_VALUE to enable notification, and then we notify peer by TEST_IDX_CHAR_VALUE

    Secondlly, we build ble_db_cfg

    ```
    struct bk_ble_db_cfg ble_db_cfg;

    ble_db_cfg.att_db = (ble_attm_desc_t *)test_service_db;
    ble_db_cfg.att_db_nb = TEST_IDX_NB;
    ble_db_cfg.prf_task_id = g_test_prf_task_id;
    ble_db_cfg.start_hdl = 0;
    ble_db_cfg.svc_perm = BK_BLE_PERM_SET(SVC_UUID_LEN, UUID_16);
    ```

    prf_task_id is app handle. If you have multi att service, used prf_task_id to distinguish it. svc_perm show TEST_IDX_SVC UUID type’s len.

    参数
    :   **-** – ble_db_cfg: service param

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

void bk_ble_set_notice_cb([ble_notice_cb_t](#_CPPv415ble_notice_cb_t "ble_notice_cb_t") func)
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
    :   1. you must regist it, otherwise you cant get any event !


    **Attention**
    :   2. you must regist it before bk_ble_create_db, otherwise you cant get BLE_5_CREATE_DB event

    参数
    :   **-** – func: event callback

    返回
    :   - void

uint8_t bk_ble_appm_get_dev_name(uint8_t *name, uint32_t buf_len)
:   Get device name.

    参数
    :   **-** – name: store the device name


        - buf_len: the length of buf to store the device name

    返回
    :   - length: the length of device name

uint8_t bk_ble_appm_set_dev_name(uint8_t len, uint8_t *name)
:   Set device name.

    参数
    :   **-** – len: the length of device name


        - name: the device name to be set

    返回
    :   - length: the length of device name

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_create_advertising(uint8_t actv_idx, [ble_adv_param_t](#_CPPv415ble_adv_param_t "ble_adv_param_t") *adv_param, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
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
    :   **-** – actv_idx: the index of activity


        - adv_param: the advertising parameter

        - callback: register a callback for this action, ble_cmd_t: BLE_CREATE_ADV

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_start_advertising(uint8_t actv_idx, uint16 duration, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Start a ble advertising.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_create_advertising

    参数
    :   **-** – actv_idx: the index of activity


        - duration: Advertising duration (in unit of 10ms). 0 means that advertising continues

        - callback: register a callback for this action, ble_cmd_t: BLE_START_ADV

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_stop_advertising(uint8_t actv_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Stop the advertising that has been started.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_start_advertising

    参数
    :   **-** – actv_idx: the index of activity


        - callback: register a callback for this action, ble_cmd_t: BLE_STOP_ADV

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_delete_advertising(uint8_t actv_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Delete the advertising that has been created.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_create_advertising

    参数
    :   **-** – actv_idx: the index of activity


        - callback: register a callback for this action, ble_cmd_t: BLE_DELETE_ADV

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_set_adv_data(uint8_t actv_idx, uint8_t *adv_buff, uint8_t adv_len, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Set the advertising data.

    User example:

    ```
    const uint8_t adv_data[] = {0x02, 0x01, 0x06, 0x0A, 0x09, 0x37, 0x32, 0x33, 0x31, 0x4e, 0x5f, 0x42, 0x4c, 0x45};
    bk_ble_set_adv_data(actv_idx, adv_data, sizeof(adv_data), ble_at_cmd_cb);
    ```


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_create_advertising

    参数
    :   **-** – actv_idx: the index of activity


        - adv_buff: advertising data

        - adv_len: the length of advertising data

        - callback: register a callback for this action, ble_cmd_t: BLE_SET_ADV_DATA

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_set_scan_rsp_data(uint8_t actv_idx, uint8_t *scan_buff, uint8_t scan_len, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
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
    :   3.must used after bk_ble_create_advertising

    参数
    :   **-** – actv_idx: the index of activity


        - scan_buff: scan response data

        - scan_len: the length of scan response data

        - callback: register a callback for this action, ble_cmd_t: BLE_SET_RSP_DATA

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_set_per_adv_data(uint8_t actv_idx, uint8_t *per_adv_buff, uint8_t per_adv_len, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Set the periodic advertising data.

    User example:

    ```
    const uint8_t adv_data[] = {0x02, 0x01, 0x06, 0x0A, 0x09, 0x37, 0x32, 0x33, 0x31, 0x4e, 0x5f, 0x42, 0x4c, 0x45};
    bk_ble_set_per_adv_data(actv_idx, adv_data, sizeof(adv_data), ble_at_cmd_cb);
    ```


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_create_advertising

    参数
    :   **-** – actv_idx: the index of activity


        - per_adv_buff: periodic advertising data

        - per_adv_len: the length of periodic advertising data

        - callback: register a callback for this action, ble_cmd_t: BLE_SET_ADV_DATA

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_set_adv_random_addr(uint8_t actv_idx, uint8_t *addr, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Set the adv random addr.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_create_advertising

    参数
    :   **-** – actv_idx: the index of activity


        - addr: random address

        - callback: register a callback for this action, ble_cmd_t: BLE_SET_ADV_RANDOM_ADDR

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_read_phy(uint8_t conn_idx)
:   Read the phy of connection device.

    User example:

    ```
    bk_ble_read_phy(conn_idx);
    ```


    **Attention**
    :   1.must used after after connected

    参数
    :   **-** – conn_idx: the index of connection device

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_set_phy(uint8_t conn_idx, [ble_set_phy_t](#_CPPv413ble_set_phy_t "ble_set_phy_t") *phy_info)
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
    :   **-** – conn_idx: the index of connection device


        - phy_info: phy parameters

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_update_param(uint8_t conn_idx, [ble_conn_param_t](#_CPPv416ble_conn_param_t "ble_conn_param_t") *conn_param)
:   Update connection parameters.


    **Attention**
    :   1.must used after connected

    参数
    :   **-** – conn_idx: the index of connection


        - conn_param: connection parameters

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_disconnect(uint8_t conn_idx)
:   Disconnect a ble connection.


    **Attention**
    :   1.must used after connected

    参数
    :   **-** – conn_idx: the index of connection

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_gatt_mtu_change(uint8_t conn_idx)
:   Exchange MTU.


    **Attention**
    :   1.must used after connected

    参数
    :   **-** – conn_idx: the index of connection

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_set_max_mtu(uint16_t max_mtu)
:   Set maximal Exchange MTU.


    **Attention**
    :   1.must used before connected

    参数
    :   **-** – max_mtu: the value to set

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_create_scaning(uint8_t actv_idx, [ble_scan_param_t](#_CPPv416ble_scan_param_t "ble_scan_param_t") *scan_param, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
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
    :   **-** – actv_idx: the index of activity


        - scan_param: the scan parameter

        - callback: register a callback for this action, ble_cmd_t: BLE_CREATE_SCAN

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_start_scaning(uint8_t actv_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Start a ble scan.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_create_scaning


    **Attention**
    :   3.adv will report in ble_notice_cb_t as BLE_5_REPORT_ADV

    参数
    :   **-** – actv_idx: the index of activity


        - callback: register a callback for this action, ble_cmd_t: BLE_START_SCAN

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_start_scaning_ex(uint8_t actv_idx, uint8_t filt_duplicate, uint16_t duration, uint16_t period, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_stop_scaning(uint8_t actv_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Stop the scan that has been started.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_start_scaning

    参数
    :   **-** – actv_idx: the index of activity


        - callback: register a callback for this action, ble_cmd_t: BLE_STOP_SCAN

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_delete_scaning(uint8_t actv_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Delete the scan that has been created.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_create_scaning

    参数
    :   **-** – actv_idx: the index of activity


        - callback: register a callback for this action, ble_cmd_t: BLE_DELETE_SCAN

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_create_init(uint8_t con_idx, [ble_conn_param_t](#_CPPv416ble_conn_param_t "ble_conn_param_t") *conn_param, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Create a activity for initiating a connection.

    User example:

    ```
    ble_conn_param_t conn_param;
    conn_param.intv_min = 0x40; //interval
    conn_param.intv_max = 0x40; //interval
    conn_param.con_latency = 0;
    conn_param.sup_to = 0x200;//supervision timeout
    conn_param.init_phys = 1;// 1M
    bk_ble_create_init(con_idx, &conn_param, ble_at_cmd);
    ```


    **Attention**
    :   1.you must wait callback status, 0 mean success.

    参数
    :   **-** – con_idx: the index of connection


        - conn_param: the connection parameter

        - callback: register a callback for this action, ble_cmd_t: BLE_INIT_CREATE

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_init_start_conn(uint8_t con_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Initiate a connection.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_create_init


    **Attention**
    :   3.when connect result, will recv BLE_5_INIT_CONNECT_EVENT in ble_notice_cb_t

    参数
    :   **-** – con_idx: the index of connection


        - callback: register a callback for this action, ble_cmd_t: BLE_INIT_START_CONN

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_init_stop_conn(uint8_t con_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)
:   Stop a connection.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_init_start_conn

    参数
    :   **-** – con_idx: the index of connection


        - callback: register a callback for this action, ble_cmd_t: BLE_INIT_STOP_CONN

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_init_set_connect_dev_addr(uint8_t connidx, [bd_addr_t](#_CPPv49bd_addr_t "bd_addr_t") *bdaddr, uint8_t addr_type)
:   Set the address of the device to be connected.


    **Attention**
    :   1.you must wait callback status, 0 mean success.


    **Attention**
    :   2.must used after bk_ble_create_init


    **Attention**
    :   3.addr_type must right, if wrong, cant connect

    参数
    :   **-** – connidx: the index of connection


        - bdaddr: the address of the device to be connected

        - addr_type: the address type of the device to be connected, OWN_ADDR_TYPE_PUBLIC_ADDR means public ,OWN_ADDR_TYPE_RANDOM_ADDR means random

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_create_periodic_sync(uint8_t actv_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_start_periodic_sync(uint8_t actv_idx, [ble_periodic_param_t](#_CPPv420ble_periodic_param_t "ble_periodic_param_t") *param, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_stop_periodic_sync(uint8_t actv_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_delete_periodic_sync(uint8_t actv_idx, [ble_cmd_cb_t](#_CPPv412ble_cmd_cb_t "ble_cmd_cb_t") callback)

uint8_t bk_ble_get_idle_actv_idx_handle(void)
:   Get an idle activity.

    返回
    :   - xx: the idle activity’s index

uint8_t bk_ble_get_max_actv_idx_count(void)
:   Get the maximum count of activities.

    返回
    :   - xx: the maximum count of activities

uint8_t bk_ble_get_max_conn_idx_count(void)
:   Get the maximum count of supported connections.

    返回
    :   - xx: the maximum count of supported connections

uint8_t bk_ble_get_idle_conn_idx_handle(void)
:   Get an idle connection activity.

    返回
    :   - xx: the idle connection activity’s index

uint8_t bk_ble_find_conn_idx_from_addr([bd_addr_t](#_CPPv49bd_addr_t "bd_addr_t") *connt_addr)
:   Find the specific connection activity by address.

    参数
    :   **-** – connt_addr: the address of the connected device

    返回
    :   - xx: the index of the connection activity meeting the address

uint8_t bk_ble_get_connect_state([bd_addr_t](#_CPPv49bd_addr_t "bd_addr_t") *connt_addr)
:   Get the connection state of the specific device.

    参数
    :   **-** – connt_addr: the device’s address

    返回
    :   - 1: this device is connected

        - 0: this device is disconnected

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_get_mac(uint8_t *mac)
:   get ble mac addr,this api is deprecated,please use bk_bluetooth_get_address


    **Attention**
    :   1. return mac is 6 bytes.

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_send_noti_value(uint8_t con_idx, uint32_t len, uint8_t *buf, uint16_t prf_id, uint16_t att_idx)
:   As slaver, send a notification of an attribute’s value.

    参数
    :   **-** – con_idx: the index of connection


        - len: the length of attribute’s value

        - buf: attribute’s value

        - prf_id: The id of the profile

        - att_idx: The index of the attribute

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_send_ind_value(uint8_t con_idx, uint32_t len, uint8_t *buf, uint16_t prf_id, uint16_t att_idx)
:   As slaver, send an indication of an attribute’s value.

    参数
    :   **-** – con_idx: the index of connection


        - len: the length of attribute’s value

        - buf: attribute’s value

        - prf_id: The id of the profile

        - att_idx: The index of the attribute

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_reg_hci_recv_callback([ble_hci_to_host_cb](#_CPPv418ble_hci_to_host_cb "ble_hci_to_host_cb") evt_cb, [ble_hci_to_host_cb](#_CPPv418ble_hci_to_host_cb "ble_hci_to_host_cb") acl_cb)
:   reg hci recv callback


    **Attention**
    :   1. you must call this after recv BLE_5_STACK_OK evt !

    参数
    :   **-** – evt_cb: evt callback function


        - acl_cb: acl callback function

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_hci_to_controller(uint8_t type, uint8_t *buf, uint16_t len)
:   send hci to controller.


    **Attention**
    :   1. you must call this after bk_ble_reg_hci_recv_callback !

    参数
    :   **-** – type: see [BK_BLE_HCI_TYPE](#group__bk__ble__api__v1_1ga28e61788890c70b81bec53fc9a5ea22c "#group__bk__ble__api__v1_1ga28e61788890c70b81bec53fc9a5ea22c").


        - buf: payload

        - len: buf’s len

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_hci_cmd_to_controller(uint8_t *buf, uint16_t len)
:   send hci cmd to controller.


    **Attention**
    :   1. you must call this after bk_ble_reg_hci_recv_callback !

    参数
    :   **-** – buf: payload


        - len: buf’s len

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_hci_acl_to_controller(uint8_t *buf, uint16_t len)
:   send hci acl to controller.


    **Attention**
    :   1. you must call this after bk_ble_reg_hci_recv_callback !

    参数
    :   **-** – buf: payload


        - len: buf’s len

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

uint8_t bk_ble_if_support_central(uint8_t *count)

[BK_BLE_CONTROLLER_STACK_TYPE](#_CPPv428BK_BLE_CONTROLLER_STACK_TYPE "BK_BLE_CONTROLLER_STACK_TYPE") bk_ble_get_controller_stack_type(void)

[BK_BLE_HOST_STACK_TYPE](#_CPPv422BK_BLE_HOST_STACK_TYPE "BK_BLE_HOST_STACK_TYPE") bk_ble_get_host_stack_type(void)

uint8_t bk_ble_get_env_state(void)

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_set_task_stack_size(uint16_t size)

void bk_ble_register_app_sdp_charac_callback([app_sdp_charac_callback](#_CPPv423app_sdp_charac_callback "app_sdp_charac_callback") cb)

void bk_ble_register_app_sdp_common_callback([app_sdp_comm_callback](#_CPPv421app_sdp_comm_callback "app_sdp_comm_callback") cb)

uint8_t bk_ble_gatt_write_ccc(uint8_t con_idx, uint16_t ccc_handle, uint16_t ccc_value)
:   As master, enable notification or indication.

    参数
    :   **-** – con_idx: the index of connection


        - ccc_handle: the handle of Client Characteristic Configuration descriptor

        - ccc_value: descriptor value, 0x01 means notification ,0x02 means indication

    返回
    :   - 0: succeed

        - others: errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_gatt_write_value(uint8_t con_idx, uint16_t att_handle, uint16_t len, uint8_t *data)
:   As master, write attribute value.

    参数
    :   **-** – con_idx: the index of connection


        - att_handle: the handle of attribute value

        - data: value data

        - len: the length of attribute value

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_read_response_value(uint8_t con_idx, uint32_t len, uint8_t *buf, uint16_t prf_id, uint16_t att_idx)
:   As slaver, send response value.

    参数
    :   **-** – con_idx: the idx of app connections


        - len: the length of attribute’s value

        - buf: attribute’s value

        - prf_id: The id of the profile

        - att_idx: The index of the attribute

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_sec_send_auth_mode(uint8_t con_idx, uint8_t mode, uint8_t iocap, uint8_t sec_req, uint8_t oob)
:   As master, configure attribute value.

    参数
    :   **-** – con_idx: the index of connection


        - mode: authentication features

        - iocap: IO Capability Values

        - sec_req: Security Defines

        - oob: OOB Data Present Flag Values

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_sec_send_auth_mode_ext(uint8_t con_idx, uint8_t mode, uint8_t iocap, uint8_t sec_req, uint8_t oob, uint8_t initiator_key_distr, uint8_t responder_key_distr)
:   As master, configure auth mode param.

    参数
    :   **-** – con_idx: the index of connection


        - mode: authentication features

        - iocap: IO Capability Values

        - sec_req: Security Defines

        - oob: OOB Data Present Flag Values

        - initiator_key_distr: init key distr, see gap_key_distr

        - responder_key_distr: resp key distr, see gap_key_distr

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_reject_pairing(uint8_t con_idx)
:   As slaver, reject a pairing request from peer.


    **Attention**
    :   used in the BLE_5_PAIRING_REQ event handler when the local side wants to reject the pairing request initiated by the peer.

    参数
    :   **-** – con_idx: the index of connection

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_init(void)
:   ble init function,this api is deprecated,please use bk_bluetooth_init.

    Param

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_deinit(void)
:   ble deinit function,this api is deprecated,please use bk_bluetooth_deinit.

    Param

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_delete_service(struct [bk_ble_db_cfg](#_CPPv413bk_ble_db_cfg "bk_ble_db_cfg") *ble_db_cfg)
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
    :   **-** – ble_db_cfg: service param

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_att_read(uint8_t con_idx, uint16_t att_handle)
:   As master, read attribute value, the result is reported in the callback registered through bk_ble_register_app_sdp_charac_callback.

    参数
    :   **-** – con_idx: the index of connection


        - att_handle: the handle of attribute value

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_create_bond(uint8_t con_idx, uint8_t auth, uint8_t iocap, uint8_t sec_req, uint8_t oob)
:   start authentication the link


    **Attention**
    :   if the link has not been bonded, it will trigger pairing, otherwise it will trigger the link encryption.

    参数
    :   **-** – con_idx: the index of connection


        - auth: authentication features(see enum [gap_auth](#group__bk__ble__api__v1__typedef_1gabddf59399b398b7d0cdb34f77becadb8 "#group__bk__ble__api__v1__typedef_1gabddf59399b398b7d0cdb34f77becadb8"))

        - iocap: IO Capability Values(see enum [bk_ble_gap_io_cap](#group__bk__ble__api__v1__typedef_1ga47c2938c3450762bfc853c0891ce35d4 "#group__bk__ble__api__v1__typedef_1ga47c2938c3450762bfc853c0891ce35d4"))

        - sec_req: Security Defines(see enum [gap_sec_req](#group__bk__ble__api__v1__typedef_1ga5bdf085cbe078d063965de5462611445 "#group__bk__ble__api__v1__typedef_1ga5bdf085cbe078d063965de5462611445"))

        - oob: OOB Data Present Flag Values(see enum [gap_oob](#group__bk__ble__api__v1__typedef_1ga009fe656dba3e223453288e3fc6fa68c "#group__bk__ble__api__v1__typedef_1ga009fe656dba3e223453288e3fc6fa68c"))

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_create_bond_ext(uint8_t con_idx, uint8_t auth, uint8_t iocap, uint8_t sec_req, uint8_t oob, uint8_t initiator_key_distr, uint8_t responder_key_distr)
:   create bond


    **Attention**
    :   if the link has not been bonded, it will trigger pairing, otherwise it will trigger the link encryption.

    参数
    :   **-** – con_idx: the index of connection


        - auth: authentication features(see enum [gap_auth](#group__bk__ble__api__v1__typedef_1gabddf59399b398b7d0cdb34f77becadb8 "#group__bk__ble__api__v1__typedef_1gabddf59399b398b7d0cdb34f77becadb8"))

        - iocap: IO Capability Values(see enum [bk_ble_gap_io_cap](#group__bk__ble__api__v1__typedef_1ga47c2938c3450762bfc853c0891ce35d4 "#group__bk__ble__api__v1__typedef_1ga47c2938c3450762bfc853c0891ce35d4"))

        - sec_req: Security Defines(see enum [gap_sec_req](#group__bk__ble__api__v1__typedef_1ga5bdf085cbe078d063965de5462611445 "#group__bk__ble__api__v1__typedef_1ga5bdf085cbe078d063965de5462611445"))

        - oob: OOB Data Present Flag Values(see enum [gap_oob](#group__bk__ble__api__v1__typedef_1ga009fe656dba3e223453288e3fc6fa68c "#group__bk__ble__api__v1__typedef_1ga009fe656dba3e223453288e3fc6fa68c"))

        - initiator_key_distr: init key distr, see gap_key_distr

        - responder_key_distr: resp key distr, see gap_key_distr

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_passkey_send(uint8_t con_idx, uint8_t accept, uint32_t passkey)
:   send passkey when pairing

    参数
    :   **-** – con_idx: the index of connection


        - accept: accept pair

        - passkey: the num that peer need to input or local need to input

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_number_compare_send(uint8_t con_idx, uint8_t accept)
:   send number compare accept when pairing

    参数
    :   **-** – con_idx: the index of connection


        - accept: accept pair

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_read_rssi(uint8_t conn_idx)
:   Read the rssi of connection device. The result will report in callback registered through bk_ble_set_notice_cb with evt BLE_5_READ_RSSI_CMPL_EVENT, and param is [ble_read_rssi_rsp_t](#structble__read__rssi__rsp__t "#structble__read__rssi__rsp__t") *.

    User example:

    ```
    bk_ble_read_rssi(conn_idx);
    ```


    **Attention**
    :   1.must used after after connected

    参数
    :   **-** – conn_idx: the index of connection device

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_config_local_appearance(uint16_t appearance)
:   set local gap appearance

    参数
    :   **appearance** – **[in]** - External appearance value, these values are defined by the Bluetooth SIG, please refer to [https://specificationrefs.bluetooth.com/assigned-values/Appearance%20Values.pdf](https://specificationrefs.bluetooth.com/assigned-values/Appearance%20Values.pdf "https://specificationrefs.bluetooth.com/assigned-values/Appearance%20Values.pdf")

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_discover_primary_service(uint8_t conn_id, uint16_t sh, uint16_t eh)
:   Discover peer primary service. The result is report in the callback registered through bk_ble_register_app_sdp_common_callback, and evt is MST_TYPE_DISCOVER_PRI_SERVICE_RSP. When completed, callback will report MST_TYPE_DISCOVER_COMPLETED with [ble_descover_complete_inf](#structble__descover__complete__inf "#structble__descover__complete__inf") and MST_TYPE_DISCOVER_PRI_SERVICE_RSP.

    参数
    :   **-** – sh: att start handle


        - eh: att end handle

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_discover_primary_service_by_uuid(uint8_t conn_id, uint16_t sh, uint16_t eh, uint16_t uuid)
:   Discover peer primary service. The result is report in the callback registered through bk_ble_register_app_sdp_common_callback, and evt is MST_TYPE_DISCOVER_PRI_SERVICE_BY_UUID_RSP. When completed, callback will report MST_TYPE_DISCOVER_COMPLETED with [ble_descover_complete_inf](#structble__descover__complete__inf "#structble__descover__complete__inf") and MST_TYPE_DISCOVER_PRI_SERVICE_BY_UUID_RSP.

    参数
    :   **-** – sh: att start handle


        - eh: att end handle

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_discover_primary_service_by_128uuid(uint8_t conn_id, uint16_t sh, uint16_t eh, uint8_t *uuid)
:   Discover peer primary service. The result is report in the callback registered through bk_ble_register_app_sdp_common_callback, and evt is MST_TYPE_DISCOVER_PRI_SERVICE_BY_128_UUID_RSP. When completed, callback will report MST_TYPE_DISCOVER_COMPLETED with [ble_descover_complete_inf](#structble__descover__complete__inf "#structble__descover__complete__inf") and MST_TYPE_DISCOVER_PRI_SERVICE_BY_128_UUID_RSP. bk_ble_read_rssi(conn_idx);.

    参数
    :   **-** – conn_id: the index of connection


        - sh: att start handle

        - eh: att end handle

        - uuid: uuid that service need to find in 128bits

    返回
    :   - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_discover_characteristic(uint8_t conn_id, uint16_t sh, uint16_t eh)
:   Discover peer characteristic. The result is report in the callback registered through bk_ble_register_app_sdp_common_callback, and evt is MST_TYPE_DISCOVER_CHAR_RSP. When completed, callback will report MST_TYPE_DISCOVER_COMPLETED with [ble_descover_complete_inf](#structble__descover__complete__inf "#structble__descover__complete__inf") and MST_TYPE_DISCOVER_CHAR_RSP.

    参数
    :   **-** – conn_id: the index of connection


        - sh: att start handle

        - eh: att end handle

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_discover_characteristic_by_uuid(uint8_t conn_id, uint16_t sh, uint16_t eh, uint16_t uuid)
:   Discover peer characteristic. The result is report in the callback registered through bk_ble_register_app_sdp_common_callback, and evt is MST_TYPE_DISCOVER_CHAR_BY_UUID_RSP. When completed, callback will report MST_TYPE_DISCOVER_COMPLETED with [ble_descover_complete_inf](#structble__descover__complete__inf "#structble__descover__complete__inf") and MST_TYPE_DISCOVER_CHAR_BY_UUID_RSP.

    参数
    :   **-** – conn_id: the index of connection


        - sh: att start handle

        - eh: att end handle

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_discover_characteristic_by_128uuid(uint8_t conn_id, uint16_t sh, uint16_t eh, uint8_t *uuid)
:   Discover peer characteristic. The result is report in the callback registered through bk_ble_register_app_sdp_common_callback, and evt is MST_TYPE_DISCOVER_CHAR_BY_128_UUID_RSP. When completed, callback will report MST_TYPE_DISCOVER_COMPLETED with [ble_descover_complete_inf](#structble__descover__complete__inf "#structble__descover__complete__inf") and MST_TYPE_DISCOVER_CHAR_BY_128_UUID_RSP.

    参数
    :   **-** – conn_id: the index of connection


        - sh: att start handle

        - eh: att end handle

    返回
    :   - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_discover_characteristic_descriptor(uint8_t conn_id, uint16_t sh, uint16_t eh)
:   Discover peer characteristic descriptor. The result is report in the callback registered through bk_ble_register_app_sdp_common_callback, and evt is MST_TYPE_DISCOVER_CHAR_DESC. When completed, callback will report MST_TYPE_DISCOVER_COMPLETED with [ble_descover_complete_inf](#structble__descover__complete__inf "#structble__descover__complete__inf") and MST_TYPE_DISCOVER_CHAR_DESC.

    参数
    :   **-** – conn_id: the index of connection


        - sh: att start handle

        - eh: att end handle

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_read(uint8_t con_idx, uint16_t att_handle, uint16_t offset)
:   As master, read attribute value, the result is reported in the callback registered through bk_ble_register_app_sdp_charac_callback.

    参数
    :   **-** – con_idx: the index of connection


        - att_handle: the handle of attribute value

        - offset: the offset of attribute value

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_read_by_uuid(uint8_t conn_id, uint16_t sh, uint16_t eh, uint8_t *uuid, uint8_t uuid_len)
:   As master, read attribute value, the result is reported in the callback registered through bk_ble_register_app_sdp_charac_callback.

    参数
    :   **-** – con_idx: the index of connection


        - sh: the start handle of attribute

        - eh: the end handle of attribute

        - uuid: uuid

        - uuid_len: uuid len, may be 2 or 16

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_gattc_write(uint8_t con_idx, uint16_t att_handle, uint8_t *data, uint16_t len, uint8_t is_write_cmd)
:   As master, write attribute value.

    参数
    :   **-** – con_idx: the index of connection


        - att_handle: the handle of attribute value

        - data: value data

        - len: the length of attribute value

        - is_write_cmd: when true, will trigger write cmd, otherwise write req.

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_clear_white_list(void)
:   clear the white list.

    Param

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_add_devices_to_while_list([bd_addr_t](#_CPPv49bd_addr_t "bd_addr_t") *addr, uint8_t addr_type)
:   Add a device to the while list.

    参数
    :   **-** – addr: the address of the device.


        - addr_type: the type of the address, 0 is public address, 1 is random address.

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_remove_devices_from_while_list([bd_addr_t](#_CPPv49bd_addr_t "bd_addr_t") *addr, uint8_t addr_type)
:   Remove a device from the while list.

    参数
    :   **-** – addr: the address of the device.


        - addr_type: the type of the address, 0 is public address, 1 is random address.

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_tx_power_set(float pwr_gain)
:   Set tx power.

    参数
    :   **-** – pwr_gain: tx power gain

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: fail

[ble_err_t](#_CPPv49ble_err_t "ble_err_t") bk_ble_host_register_hci_callback([ble_hci_to_cp_cb](#_CPPv416ble_hci_to_cp_cb "ble_hci_to_cp_cb") cb)
:   register hci callback for host only


    **Attention**
    :   used for host only

    参数
    :   **-** – cb: hci callback function used to recv hci data from host

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_ble_hci_send_to_host(uint8_t *buf, uint32_t len)
:   send hci data to host.


    **Attention**
    :   used for host only

    参数
    :   **-** – buf: payload


        - len: buf’s len

    返回
    :   - BK_ERR_BLE_SUCCESS: succeed


## API 类型定义


## bk_ble_types.h

`bk_ble_types.h` 定义传统 BLE API 使用的配置、事件和数据类型。


### Header File


- [bluetooth/bk_ble_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_ble_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/bluetooth/bk_ble_types.h")


### Structures

struct ble_sdp_svc_ind

struct ble_sdp_char_inf
:   characteristic info

struct ble_sdp_char_desc_inf
:   characteristic description

struct ble_descover_complete_inf
:   discover completed evt param, see MST_TYPE_DISCOVER_COMPLETED

struct ble_smp_ind_t

struct ble_attc_wr_rd_op

struct ble_attc_event_ind

struct ble_cmd_param_t

struct ble_att_info_req_t

struct ble_write_req_t

struct ble_read_req_t

struct ble_recv_adv_t

struct ble_mtu_change_t

struct ble_conn_ind_t

struct ble_discon_ind_t

struct ble_create_db_t

struct ble_attm_desc_t

struct bk_ble_db_cfg

struct ble_init_config_t

struct bd_addr_t

struct ble_cmd_cmp_evt_t

struct ble_read_phy_t

struct ble_set_phy_t

struct ble_adv_param_t

struct ble_scan_param_t

struct ble_conn_param_t

struct ble_periodic_param_t

struct ble_conn_update_para_ind_t

struct mst_comm_updata_para

struct ble_adv_stopped_ind_t

struct ble_scan_stopped_ind_t

struct ble_read_rssi_rsp_t
:   BLE_5_READ_RSSI_CMPL_EVENT data.

struct bk_ble_enc_keys_t
:   BLE encryption keys.

struct bk_ble_irk_info_t
:   BLE irk info.

struct bk_ble_key_t

struct bk_ble_bond_info_req_t

struct bk_ble_gatt_cmp_evt_t


### Macros

BK_ERR_BLE_SUCCESS
:   success

BK_ERR_BLE_FAIL
:   fail

BK_ERR_BLE_NO_MEM
:   no mem

BK_ERR_BLE_PROFILE
:   profile err

BK_ERR_BLE_CREATE_DB
:   bk_ble_create_db err

BK_ERR_BLE_CMD_NOT_SUPPORT
:   unknow cmd err

BK_ERR_BLE_UNKNOW_IDX
:   index err, suchas conn_ind

BK_ERR_BLE_BLE_STATUS
:   ble status not match

BK_ERR_BLE_ADV_DATA
:   adv data err, such as too long

BK_ERR_BLE_CMD_RUN
:   cmd run err

BK_ERR_BLE_INIT_CREATE
:   create init err, such as bk_ble_create_init

BK_ERR_BLE_INIT_STATE
:   current init status not match

BK_ERR_BLE_ATTC_WRITE
:   att write err

BK_ERR_BLE_ATTC_WRITE_UNREGISTER
:   att handle is not regist

BK_BLE_MAX_ADV_DATA_LEN
:   max ble adv data len

BK_BLE_GAP_BD_ADDR_LEN
:   BD address length.

BK_BLE_APP_DEVICE_NAME_MAX_LEN
:   Maximal length of the Device Name value.

BK_BLE_PERM_SET(access, right)
:   for [ble_attm_desc_t](#structble__attm__desc__t "#structble__attm__desc__t"), build database perm,

BK_BLE_PERM_GET(perm, access)


### Type Definitions

typedef [bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") ble_err_t
:   ble api return enum

typedef void (*app_sdp_callback)(unsigned char conidx, uint16_t chars_val_hdl, unsigned char uuid_len, unsigned char *uuid)

typedef void (*app_sdp_charac_callback)([CHAR_TYPE](#_CPPv49CHAR_TYPE "CHAR_TYPE") type, uint8 conidx, uint16_t hdl, uint16_t len, uint8 *data)

typedef void (*app_sdp_comm_callback)([MASTER_COMMON_TYPE](#_CPPv418MASTER_COMMON_TYPE "MASTER_COMMON_TYPE") type, uint8 conidx, void *param)

typedef void (*ble_cmd_cb_t)([ble_cmd_t](#_CPPv49ble_cmd_t "ble_cmd_t") cmd, [ble_cmd_param_t](#_CPPv415ble_cmd_param_t "ble_cmd_param_t") *param)
:   for sync ble api call return

    most ble api have ble_cmd_cb_t param, you must wait is callback.

    Param -
    :   cmd: cmd id.


        - param: param

typedef void (*ble_notice_cb_t)([ble_notice_t](#_CPPv412ble_notice_t "ble_notice_t") notice, void *param)
:   for async ble api event.

    ble event report.

    Param -
    :   notice: event id.


        - param: param

typedef [ble_err_t](#_CPPv49ble_err_t "ble_err_t") (*ble_hci_to_host_cb)(uint8_t *buf, uint16_t len)
:   for hci callback.

    stack report evt, acl to upper

    Param -
    :   buf: payload


        - len: buf’s len

    Return
    :   - BK_ERR_BLE_SUCCESS: succeed

typedef [ble_err_t](#_CPPv49ble_err_t "ble_err_t") (*ble_hci_to_cp_cb)(uint8_t *buf, uint16_t len)


### Enumerations

enum BK_BLE_CONTROLLER_STACK_TYPE
:   *Values:*

    enumerator BK_BLE_CONTROLLER_STACK_TYPE_BLE_4

    enumerator BK_BLE_CONTROLLER_STACK_TYPE_BLE_5_X

    enumerator BK_BLE_CONTROLLER_STACK_TYPE_BTDM_5_2

enum BK_BLE_HOST_STACK_TYPE
:   *Values:*

    enumerator BK_BLE_HOST_STACK_TYPE_RW_4

    enumerator BK_BLE_HOST_STACK_TYPE_RW_5_X

    enumerator BK_BLE_HOST_STACK_TYPE_RW_5_2

    enumerator BK_BLE_HOST_STACK_TYPE_ETHERMIND

enum BK_BLE_HCI_TYPE
:   hci type enum


    *Values:*

    enumerator BK_BLE_HCI_TYPE_CMD

    enumerator BK_BLE_HCI_TYPE_ACL

    enumerator BK_BLE_HCI_TYPE_SCO

    enumerator BK_BLE_HCI_TYPE_EVT

enum ble_actv_state
:   ble actv type


    *Values:*

    enumerator BLE_ACTV_IDLE

    enumerator BLE_ACTV_ADV_CREATED

    enumerator BLE_ACTV_ADV_STARTED

    enumerator BLE_ACTV_SCAN_CREATED

    enumerator BLE_ACTV_SCAN_STARTED

    enumerator BLE_ACTV_INIT_CREATED

    enumerator BLE_ACTV_PER_SYNC_CREATED

    enumerator BLE_ACTV_PER_SYNC_STARTED

enum bk_ble_perm_mask
:   normal perm, for BK_BLE_PERM_SET

    | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 - 6 | 5 - 4 | 3 - 2 | 1 - 0 |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | EXT | WS | I | N | WR | WC | RD | B | NP | IP | WP | RP |


    **Attention**
    :   you cant use this direct, use [BK_BLE_PERM_SET(RD, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b") instead

    Bit [0-1] : Read Permission (0 = NO_AUTH, 1 = UNAUTH, 2 = AUTH, 3 = SEC_CON)

    Bit [2-3] : Write Permission (0 = NO_AUTH, 1 = UNAUTH, 2 = AUTH, 3 = SEC_CON)

    Bit [4-5] : Indication Permission (0 = NO_AUTH, 1 = UNAUTH, 2 = AUTH, 3 = SEC_CON)

    Bit [6-7] : Notification Permission (0 = NO_AUTH, 1 = UNAUTH, 2 = AUTH, 3 = SEC_CON)

    Bit [8] : Broadcast permission

    Bit [9] : Read Command accepted

    Bit [10] : Write Command accepted

    Bit [11] : Write Request accepted

    Bit [12] : Send Notification

    Bit [13] : Send Indication

    Bit [14] : Write Signed accepted

    Bit [15] : Extended properties present


    *Values:*

    enumerator BK_BLE_RP_MASK
    :   Read Permission Mask.

    enumerator BK_BLE_RP_POS

    enumerator BK_BLE_WP_MASK
    :   Write Permission Mask.

    enumerator BK_BLE_WP_POS

    enumerator BK_BLE_IP_MASK
    :   Indication Access Mask.

    enumerator BK_BLE_IP_POS

    enumerator BK_BLE_NP_MASK
    :   Notification Access Mask.

    enumerator BK_BLE_NP_POS

    enumerator BK_BLE_BROADCAST_MASK
    :   Broadcast descriptor present.

    enumerator BK_BLE_BROADCAST_POS

    enumerator BK_BLE_RD_MASK
    :   Read Access Mask.

    enumerator BK_BLE_RD_POS

    enumerator BK_BLE_WRITE_COMMAND_MASK
    :   Write Command Enabled attribute Mask.

    enumerator BK_BLE_WRITE_COMMAND_POS

    enumerator BK_BLE_WRITE_REQ_MASK
    :   Write Request Enabled attribute Mask.

    enumerator BK_BLE_WRITE_REQ_POS

    enumerator BK_BLE_NTF_MASK
    :   Notification Access Mask.

    enumerator BK_BLE_NTF_POS

    enumerator BK_BLE_IND_MASK
    :   Indication Access Mask.

    enumerator BK_BLE_IND_POS

    enumerator BK_BLE_WRITE_SIGNED_MASK
    :   Write Signed Enabled attribute Mask.

    enumerator BK_BLE_WRITE_SIGNED_POS

    enumerator BK_BLE_EXT_MASK
    :   Extended properties descriptor present.

    enumerator BK_BLE_EXT_POS

enum bk_ble_ext_perm_mask
:   Attribute Extended permissions, for BK_BLE_PERM_SET.

    Extended Value permission bit field


    **Attention**
    :   you cant use this direct, use [BK_BLE_PERM_SET(EKS, ENABLE)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b") instead

    | 15 | 14 - 13 | 12 | 11 | 10 - 0 |
    | --- | --- | --- | --- | --- |
    | RI | UUID_LEN | EKS | INCL | Reserved |

    Bit [0-10] : Reserved

    Bit [11] : Attribute Value is included(Value present in Database)

    Bit [12] : Encryption key Size must be 16 bytes

    Bit [13-14]: UUID Length (0 = 16 bits, 1 = 32 bits, 2 = 128 bits, 3 = RFU)

    Bit [15] : Trigger Read Indication (0 = Value present in Database, 1 = Value not present in Database)


    *Values:*

    enumerator BK_BLE_VALUE_INCL_MASK
    :   Attribute Value is included.

    enumerator BK_BLE_VALUE_INCL_POS

    enumerator BK_BLE_EKS_MASK
    :   Check Encryption key size Mask.

    enumerator BK_BLE_EKS_POS

    enumerator BK_BLE_UUID_LEN_MASK
    :   UUID Length.

    enumerator BK_BLE_UUID_LEN_POS

    enumerator BK_BLE_RI_MASK
    :   Read trigger Indication.

    enumerator BK_BLE_RI_POS

enum bk_ble_svc_perm_mask
:   Service permissions, for BK_BLE_PERM_SET.

    | 7 | 6 - 5 | 4 | 3 - 2 | 1 | 0 |
    | --- | --- | --- | --- | --- | --- |
    | SEC | UUID_LEN | DIS | AUTH | EKS | MI |


    **Attention**
    :   you cant use this direct, use [BK_BLE_PERM_SET(SVC_UUID_LEN, UUID_16)](#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b "#group__bk__ble__api__v1_1ga12a5ba4c80b8f6fdc20573c242bd0b5b") instead

    Bit [0] : Task that manage service is multi-instantiated (Connection index is conveyed)

    Bit [1] : Encryption key Size must be 16 bytes

    Bit [2-3]: Service Permission (0 = NO_AUTH, 1 = UNAUTH, 2 = AUTH, 3 = Secure Connect)

    Bit [4] : Disable the service

    Bit [5-6]: UUID Length (0 = 16 bits, 1 = 32 bits, 2 = 128 bits, 3 = RFU)

    Bit [7] : Secondary Service (0 = Primary Service, 1 = Secondary Service)


    *Values:*

    enumerator BK_BLE_SVC_MI_MASK
    :   Task that manage service is multi-instantiated.

    enumerator BK_BLE_SVC_MI_POS

    enumerator BK_BLE_SVC_EKS_MASK
    :   Check Encryption key size for service Access.

    enumerator BK_BLE_SVC_EKS_POS

    enumerator BK_BLE_SVC_AUTH_MASK
    :   Service Permission authentication.

    enumerator BK_BLE_SVC_AUTH_POS

    enumerator BK_BLE_SVC_DIS_MASK
    :   Disable the service.

    enumerator BK_BLE_SVC_DIS_POS

    enumerator BK_BLE_SVC_UUID_LEN_MASK
    :   Service UUID Length.

    enumerator BK_BLE_SVC_UUID_LEN_POS

    enumerator BK_BLE_SVC_SECONDARY_MASK
    :   Service type Secondary.

    enumerator BK_BLE_SVC_SECONDARY_POS

enum [anonymous]
:   *Values:*

    enumerator BK_BLE_PERM_RIGHT_DISABLE
    :   Disable access.

    enumerator BK_BLE_PERM_RIGHT_ENABLE
    :   Enable access.

enum [anonymous]
:   *Values:*

    enumerator BK_BLE_PERM_RIGHT_NO_AUTH
    :   No Authentication.

    enumerator BK_BLE_PERM_RIGHT_UNAUTH
    :   Access Requires Unauthenticated link.

    enumerator BK_BLE_PERM_RIGHT_AUTH
    :   Access Requires Authenticated link.

    enumerator BK_BLE_PERM_RIGHT_SEC_CON
    :   Access Requires Secure Connection link.

enum [anonymous]
:   *Values:*

    enumerator BK_BLE_PERM_RIGHT_UUID_16
    :   16 bits UUID

    enumerator BK_BLE_PERM_RIGHT_UUID_32
    :   32 bits UUID

    enumerator BK_BLE_PERM_RIGHT_UUID_128
    :   128 bits UUID

    enumerator BK_BLE_PERM_RIGHT_UUID_RFU
    :   Invalid.

enum ble_cmd_t
:   *Values:*

    enumerator BLE_CMD_NONE

    enumerator BLE_CREATE_ADV
    :   ADV_CMD:FOR BLE 5.1.

    enumerator BLE_SET_ADV_DATA

    enumerator BLE_SET_RSP_DATA

    enumerator BLE_START_ADV

    enumerator BLE_STOP_ADV

    enumerator BLE_DELETE_ADV

    enumerator BLE_INIT_ADV
    :   ADV_CMD:FOR BLE 4.2.

    enumerator BLE_DEINIT_ADV

    enumerator BLE_CREATE_SCAN
    :   SCAN_CMD:FOR BLE 5.1.

    enumerator BLE_START_SCAN

    enumerator BLE_STOP_SCAN

    enumerator BLE_DELETE_SCAN

    enumerator BLE_INIT_SCAN
    :   SCAN_CMD:FOR BLE 4.2.

    enumerator BLE_DEINIT_SCAN

    enumerator BLE_CONN_UPDATE_MTU
    :   conn

    enumerator BLE_CONN_UPDATE_PARAM

    enumerator BLE_CONN_DIS_CONN

    enumerator BLE_CONN_READ_PHY

    enumerator BLE_CONN_SET_PHY

    enumerator BLE_CONN_ENCRYPT

    enumerator BLE_INIT_CREATE
    :   init

    enumerator BLE_INIT_START_CONN

    enumerator BLE_INIT_STOP_CONN

    enumerator BLE_INIT_DIS_CONN

    enumerator BLE_INIT_READ_CHAR

    enumerator BLE_INIT_WRITE_CHAR

    enumerator BLE_SET_MAX_MTU
    :   config

    enumerator BLE_CREATE_PERIODIC

    enumerator BLE_START_PERIODIC

    enumerator BLE_STOP_PERIODIC

    enumerator BLE_DELETE_PERIODIC

    enumerator BLE_SET_LOCAL_NAME

    enumerator BLE_GET_LOCAL_NAME

    enumerator BLE_READ_LOCAL_ADDR

    enumerator BLE_SET_RANDOM_ADDR

    enumerator BLE_SET_ADV_RANDOM_ADDR

    enumerator BLE_ADD_WHITE_LIST

    enumerator BLE_RMV_WHITE_LIST

    enumerator BLE_CLE_WHITE_LIST

    enumerator BLE_CMD_MAX

enum ble_notice_t
:   *Values:*

    enumerator BLE_5_STACK_OK
    :   ble stack init ok, param null.This event is deprecated,please do not use it.

    enumerator BLE_5_WRITE_EVENT
    :   peer write our, param [ble_write_req_t](#structble__write__req__t "#structble__write__req__t")

    enumerator BLE_5_READ_EVENT
    :   peer read our, param [ble_read_req_t](#structble__read__req__t "#structble__read__req__t")

    enumerator BLE_5_REPORT_ADV
    :   scan peer adv report, param [ble_recv_adv_t](#structble__recv__adv__t "#structble__recv__adv__t")

    enumerator BLE_5_MTU_CHANGE
    :   mtu change event, param [ble_mtu_change_t](#structble__mtu__change__t "#structble__mtu__change__t")

    enumerator BLE_5_CONNECT_EVENT
    :   as slaver, recv connnect event, param [ble_conn_ind_t](#structble__conn__ind__t "#structble__conn__ind__t")

    enumerator BLE_5_DISCONNECT_EVENT
    :   recv disconnect event, param [ble_discon_ind_t](#structble__discon__ind__t "#structble__discon__ind__t")

    enumerator BLE_5_ATT_INFO_REQ

    enumerator BLE_5_CREATE_DB
    :   create db event, param [ble_create_db_t](#structble__create__db__t "#structble__create__db__t")

    enumerator BLE_5_TX_DONE
    :   tx complete event, param null

    enumerator BLE_5_PAIRING_REQ
    :   smp report

    enumerator BLE_5_PAIRING_SUCCEED

    enumerator BLE_5_PAIRING_FAILED

    enumerator BLE_5_PARING_PASSKEY_REQ

    enumerator BLE_5_ENCRYPT_EVENT

    enumerator BLE_5_INIT_CONNECT_EVENT
    :   as master, recv connect event

    enumerator BLE_5_INIT_DISCONNECT_EVENT

    enumerator BLE_5_INIT_CONNECT_FAILED_EVENT

    enumerator BLE_5_SDP_REGISTER_FAILED

    enumerator BLE_5_READ_PHY_EVENT
    :   get current conn phy result, param [ble_read_phy_t](#structble__read__phy__t "#structble__read__phy__t")

    enumerator BLE_5_CONN_UPDATA_EVENT
    :   recv conn update event, param [ble_conn_param_t](#structble__conn__param__t "#structble__conn__param__t")

    enumerator BLE_5_PERIODIC_SYNC_CMPL_EVENT

    enumerator BLE_5_DISCOVERY_PRIMARY_SERVICE_EVENT

    enumerator BLE_5_DISCOVERY_CHAR_EVENT

    enumerator BLE_5_RECV_NOTIFY_EVENT

    enumerator BLE_5_ATT_READ_RESPONSE

    enumerator BLE_5_CONN_UPD_PAR_ASK

    enumerator BLE_5_SHUTDOWN_SUCCEED

    enumerator BLE_5_DELETE_SERVICE_DONE
    :   delete service event

    enumerator BLE_5_GAP_CMD_CMP_EVENT

    enumerator BLE_5_ADV_STOPPED_EVENT

    enumerator BLE_5_READ_RSSI_CMPL_EVENT

    enumerator BLE_5_KEY_EVENT

    enumerator BLE_5_BOND_INFO_REQ_EVENT

    enumerator BLE_5_READ_BLOB_EVENT

    enumerator BLE_5_PAIRING_SECURITY_REQ_EVENT

    enumerator BLE_5_PARING_NUMBER_COMPARE_REQ_EVENT

    enumerator BLE_5_SCAN_STOPPED_EVENT

enum CHAR_TYPE
:   *Values:*

    enumerator CHARAC_NOTIFY

    enumerator CHARAC_INDICATE

    enumerator CHARAC_READ

    enumerator CHARAC_READ_DONE

    enumerator CHARAC_WRITE_DONE

enum MASTER_COMMON_TYPE
:   *Values:*

    enumerator MST_TYPE_SVR_UUID

    enumerator MST_TYPE_ATT_UUID

    enumerator MST_TYPE_ATT_DESC

    enumerator MST_TYPE_SDP_END

    enumerator MST_TYPE_ATTC_SVR_UUID

    enumerator MST_TYPE_ATTC_ATT_UUID
    :   Service the UUID.

    enumerator MST_TYPE_ATTC_ATT_DESC
    :   ATT of a service.

    enumerator MST_TYPS_ATTC_PARAM_ERR
    :   ATT DESC of a service.

    enumerator MST_TYPE_ATTC_ERR
    :   The delivered parameter is abnormal or unknown.

    enumerator MST_TYPE_ATTC_END
    :   if appm_get_init_attc_info return is ok && ble is disconnect,so update the event

    enumerator MST_TYPE_ATTC_WRITE_RSP
    :   End of the operation.

    enumerator MST_TYPE_ATTC_WRITE_NO_RESPONSE

    enumerator MST_TYPE_ATTC_CHARAC_READ_DONE

    enumerator MST_TYPE_MTU_EXC

    enumerator MST_TYPE_MTU_EXC_DONE

    enumerator MST_TYPE_UPP_ASK

    enumerator MST_TYPE_UPDATA_STATUS
    :   Ask if you agree to update the parameter.

    enumerator MST_TYPE_DISCOVER_PRI_SERVICE_RSP

    enumerator MST_TYPE_DISCOVER_PRI_SERVICE_BY_UUID_RSP

    enumerator MST_TYPE_DISCOVER_PRI_SERVICE_BY_128_UUID_RSP

    enumerator MST_TYPE_DISCOVER_CHAR_RSP

    enumerator MST_TYPE_DISCOVER_CHAR_BY_UUID_RSP

    enumerator MST_TYPE_DISCOVER_CHAR_BY_128_UUID_RSP

    enumerator MST_TYPE_DISCOVER_CHAR_DESC

    enumerator MST_TYPE_DISCOVER_COMPLETED

enum msg_attc
:   *Values:*

    enumerator MST_ATTC_ALL

    enumerator MST_ATTC_GET_SVR_UUID_ALL

    enumerator MST_ATTC_GET_SVR_UUID_BY_SVR_UUID

    enumerator MST_ATTC_GET_ATT_UUID_ALL

    enumerator MST_ATTC_GET_ATT_DESC_UUID_ALL

    enumerator MST_ATTC_SVR_ATT_BY_SVR_UUID

    enumerator MST_ATTC_SVR_ATT_DESC_BY_SVR_UUID

    enumerator MST_ATTC_SVR_ATT_AND_DESC_BY_SVR_UUID
    :   Gets all ATT-DESC’s for this SVR-UUID for this connection.

enum adv_report_type
:   *Values:*

    enumerator REPORT_TYPE_ADV_EXT
    :   Extended advertising report.

    enumerator REPORT_TYPE_ADV_LEG
    :   Legacy advertising report.

    enumerator REPORT_TYPE_SCAN_RSP_EXT
    :   Extended scan response report.

    enumerator REPORT_TYPE_SCAN_RSP_LEG
    :   Legacy scan response report.

    enumerator REPORT_TYPE_PER_ADV
    :   Periodic advertising report.

enum adv_report_info
:   *Values:*

    enumerator REPORT_INFO_REPORT_TYPE_MASK
    :   Report Type.

    enumerator REPORT_INFO_COMPLETE_BIT
    :   Report is complete.

    enumerator REPORT_INFO_CONN_ADV_BIT
    :   Connectable advertising.

    enumerator REPORT_INFO_SCAN_ADV_BIT
    :   Scannable advertising.

    enumerator REPORT_INFO_DIR_ADV_BIT
    :   Directed advertising.

enum adv_type
:   Type of advertising that can be created.


    *Values:*

    enumerator ADV_TYPE_LEGACY
    :   Legacy advertising.

    enumerator ADV_TYPE_EXTENDED
    :   Extended advertising.

    enumerator ADV_TYPE_PERIODIC
    :   Periodic advertising.

enum adv_prop_bf
:   Advertising properties bit field bit positions.


    *Values:*

    enumerator ADV_PROP_CONNECTABLE_BIT
    :   Indicate that advertising is connectable, reception of CONNECT_REQ or AUX_CONNECT_REQ PDUs is accepted. Not applicable for periodic advertising.

    enumerator ADV_PROP_SCANNABLE_BIT
    :   Indicate that advertising is scannable, reception of SCAN_REQ or AUX_SCAN_REQ PDUs is accepted

    enumerator ADV_PROP_DIRECTED_BIT
    :   Indicate that advertising targets a specific device. Only apply in following cases:


        - Legacy advertising: if connectable

        - Extended advertising: connectable or (non connectable and non discoverable)

    enumerator ADV_PROP_HDC_BIT
    :   Indicate that High Duty Cycle has to be used for advertising on primary channel Apply only if created advertising is not an extended advertising

    enumerator ADV_PROP_PROP_LEGACY_BIT
    :   Use legacy advertising PDUs.

    enumerator ADV_PROP_ANONYMOUS_BIT
    :   Enable anonymous mode. Device address won’t appear in send PDUs Valid only if created advertising is an extended advertising

    enumerator ADV_PROP_TX_PWR_BIT
    :   Include TX Power in the extended header of the advertising PDU. Valid only if created advertising is not a legacy advertising

enum adv_chnl_map
:   Advertising channels enables.


    *Values:*

    enumerator ADV_CHNL_37
    :   Byte value for advertising channel map for channel 37 enable.

    enumerator ADV_CHNL_38
    :   Byte value for advertising channel map for channel 38 enable.

    enumerator ADV_CHNL_39
    :   Byte value for advertising channel map for channel 39 enable.

    enumerator ADV_ALL_CHNLS
    :   Byte value for advertising channel map for channel 37, 38 and 39 enable.

enum phy_type_le
:   PHY Type.


    *Values:*

    enumerator PHY_TYPE_LE_1M
    :   LE 1M.

    enumerator PHY_TYPE_LE_2M
    :   LE 2M.

    enumerator PHY_TYPE_LE_CODED
    :   LE Coded.

enum initiating_phy_type_le
:   Initiating PHY Type.


    *Values:*

    enumerator INIT_PHY_TYPE_LE_1M
    :   LE 1M.

    enumerator INIT_PHY_TYPE_LE_2M
    :   LE 2M.

    enumerator INIT_PHY_TYPE_LE_CODED
    :   LE Coded.

enum ble_own_addr_type
:   Own addr type.


    *Values:*

    enumerator OWN_ADDR_TYPE_PUBLIC_OR_STATIC_ADDR
    :   Public or Private Static Address according to device address configuration Attention: Private Static Address is not used now, so set will be public Attention: this enum is derecated, use OWN_ADDR_TYPE_PUBLIC_ADDR instead.

    enumerator OWN_ADDR_TYPE_GEN_RSLV_OR_RANDOM_ADDR
    :   Generated resolvable private random or random address, will auto refresh periodic Attention: RPA is not used now, so set will be random

    enumerator OWN_ADDR_TYPE_GEN_NON_RSLV_OR_RANDOM_ADDR
    :   Generated non-resolvable private random or random address, will auto refresh periodic Attention: NRPA is not used now, so set will be random

    enumerator OWN_ADDR_TYPE_PUBLIC_ADDR
    :   public addr

    enumerator OWN_ADDR_TYPE_RANDOM_ADDR
    :   use bk_ble_set_adv_random_addr addr

enum ble_scan_type
:   Scan type.


    *Values:*

    enumerator PASSIVE_SCANNING
    :   Passive Scanning. No scanning PDUs shall be sent (default)

    enumerator ACTIVE_SCANNING
    :   Active scanning. Scanning PDUs may be sent.

enum ble_scan_filter_policy
:   Scan filter policy.


    *Values:*

    enumerator BASIC_UNFILTER_SCAN_POLICY
    :   Basic unfiltered scanning filter policy.

    enumerator BASIC_FILTER_SCAN_POLICY
    :   Basic filtered scanning filter policy.

    enumerator EXTENED_UNFILER_SCAN_POLICY
    :   Extended unfiltered scanning filter policy.

    enumerator EXTENED_FILER_SCAN_POLICY
    :   Extended filtered scanning filter policy.

enum ble_sync_cte_type
:   Constant Tone Extension sync filtering type.


    *Values:*

    enumerator CTE_NO_SYNC_WITH_AOA
    :   Do not sync to packets with an AoA Constant Tone Extension.

    enumerator CTE_NO_SYNC_WITH_AOD_1US_SLOT
    :   Do not sync to packets with an AoD Constant Tone Extension with 1 us slots.

    enumerator CTE_NO_SYNC_WITH_AOD_2US_SLOT
    :   Do not sync to packets with an AoD Constant Tone Extension with 2 us slots.

    enumerator CTE_NO_SYNC_WITH_TYPE_3
    :   Do not sync to packets with a type 3 Constant Tone Extension (currently reserved for future use)

    enumerator CTE_NO_SYNC_WITHOUT_CTE
    :   Do not sync to packets without a Constant Tone Extension.

enum gap_auth_mask
:   Authentication mask.


    *Values:*

    enumerator GAP_AUTH_NONE
    :   No Flag set.

    enumerator GAP_AUTH_BOND
    :   Bond authentication.

    enumerator GAP_AUTH_MITM
    :   Man In the middle protection.

    enumerator GAP_AUTH_SEC_CON
    :   Secure Connection.

    enumerator GAP_AUTH_KEY_NOTIF
    :   Key Notification.

enum gap_auth
:   *Values:*

    enumerator GAP_AUTH_REQ_NO_MITM_NO_BOND
    :   No MITM No Bonding.

    enumerator GAP_AUTH_REQ_NO_MITM_BOND
    :   No MITM Bonding.

    enumerator GAP_AUTH_REQ_MITM_NO_BOND
    :   MITM No Bonding.

    enumerator GAP_AUTH_REQ_MITM_BOND
    :   MITM and Bonding.

    enumerator GAP_AUTH_REQ_SEC_CON_NO_BOND
    :   SEC_CON and No Bonding.

    enumerator GAP_AUTH_REQ_SEC_CON_BOND
    :   SEC_CON and Bonding.

    enumerator GAP_AUTH_REQ_LAST

    enumerator GAP_AUTH_REQ_MASK
    :   Mask of authentication features without reserved flag.

enum bk_ble_gap_io_cap
:   IO Capability Values.


    *Values:*

    enumerator BK_BLE_GAP_IO_CAP_DISPLAY_ONLY
    :   Display Only.

    enumerator BK_BLE_GAP_IO_CAP_DISPLAY_YES_NO
    :   Display Yes No.

    enumerator BK_BLE_GAP_IO_CAP_KB_ONLY
    :   Keyboard Only.

    enumerator BK_BLE_GAP_IO_CAP_NO_INPUT_NO_OUTPUT
    :   No Input No Output.

    enumerator BK_BLE_GAP_IO_CAP_KB_DISPLAY
    :   Keyboard Display.

    enumerator BK_BLE_GAP_IO_CAP_LAST

enum gap_sec_req
:   Security Defines.


    *Values:*

    enumerator GAP_NO_SEC
    :   No security (no authentication and encryption)

    enumerator GAP_SEC1_NOAUTH_PAIR_ENC
    :   Unauthenticated pairing with encryption.

    enumerator GAP_SEC1_AUTH_PAIR_ENC
    :   Authenticated pairing with encryption.

    enumerator GAP_SEC2_NOAUTH_DATA_SGN
    :   Unauthenticated pairing with data signing.

    enumerator GAP_SEC2_AUTH_DATA_SGN
    :   Authentication pairing with data signing.

    enumerator GAP_SEC1_SEC_CON_PAIR_ENC
    :   Secure Connection pairing with encryption.

enum gap_oob
:   OOB Data Present Flag Values.


    *Values:*

    enumerator GAP_OOB_AUTH_DATA_NOT_PRESENT
    :   OOB Data not present.

    enumerator GAP_OOB_AUTH_DATA_PRESENT
    :   OOB data present.

    enumerator GAP_OOB_AUTH_DATA_LAST

enum gap_key_distr
:   key distr


    *Values:*

    enumerator BK_BLE_GAP_KDIST_NONE
    :   No Keys to distribute.

    enumerator BK_BLE_GAP_KDIST_ENCKEY
    :   Encryption key in distribution.

    enumerator BK_BLE_GAP_KDIST_IDKEY
    :   IRK (ID key)in distribution.

    enumerator BK_BLE_GAP_KDIST_SIGNKEY
    :   CSRK(Signature key) in distribution.

    enumerator BK_BLE_GAP_KDIST_LINKKEY
    :   LTK in distribution.

    enumerator BK_BLE_GAP_KDIST_LAST


## 参考链接

> [API 参考：](../../api-reference/bluetooth.md "../../api-reference/bluetooth.md") 介绍蓝牙 API 接口。
>
> [蓝牙开发者指南：](../../developer-guide/bluetooth.md "../../developer-guide/bluetooth.md") 介绍蓝牙开发者指南。
>
> [示例和演示：](../../examples/cli/bluetooth.md "../../examples/cli/bluetooth.md") 介绍蓝牙示例的使用和操作说明。
