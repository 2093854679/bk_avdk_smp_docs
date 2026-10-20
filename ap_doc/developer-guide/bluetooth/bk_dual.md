---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/bluetooth/bk_dual.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 双模蓝牙

<a id="id2"></a>

## 概述

双模蓝牙 host 同时支持经典蓝牙 BT(Classic) 与低功耗蓝牙 BLE，统一使用 `bk_dm_*` 系列接口。
与单BLE的 `bk_ble_*` 接口不同，双模下 BLE 的 GAP/GATT 操作使用 `bk_ble_gap_*` 、 `bk_ble_gatts_*` 、 `bk_ble_gattc_*` 接口
（声明在 `bk_dm_gap_ble.h` 、 `bk_dm_gatts.h` 、 `bk_dm_gattc.h` 中），所有结果与事件均通过注册的回调函数配合事件枚举上报。

常用头文件如下：

- `components/bluetooth/bk_dm_bluetooth.h` ：协议栈初始化、去初始化、获取地址。
- `components/bluetooth/bk_dm_gap_ble.h` ：BLE GAP，广播、扫描、连接、配对加密。
- `components/bluetooth/bk_dm_gatts.h` ：BLE GATT Server。
- `components/bluetooth/bk_dm_gattc.h` ：BLE GATT Client。
- `components/bluetooth/bk_dm_bap.h` ：LE Audio BAP（unicast / broadcast）。
- `components/bluetooth/bk_dm_a2dp.h` 、 `bk_dm_hfp.h` 、 `bk_dm_avrcp.h` 、 `bk_dm_spp.h` ：经典蓝牙各 profile。

本章主要介绍双模下 BLE 的常用使用场景；经典蓝牙 BT(A2DP/HFP/AVRCP/SPP) 的完整流程在对应工程中介绍，见 [经典蓝牙(BT)](#bt) 与 [参考链接](#id8) 。

<a id="id3"></a>

## 宏配置

双模与单BLE在 host 协议栈选择上由宏区分，相关宏说明见 [蓝牙概述](bk_overview.md) 。
使用双模功能前，请确认工程已选择双模协议栈并使能 BT 相关配置。

<a id="api"></a>

## API调用注意事项

大部分API结果通过回调上报，应当等待对应事件返回后再进行下一步操作。
回调、事件回调的处理不应有阻塞操作，且调用栈不能太深。

重要

应极力避免蓝牙task被阻塞，否则会出现断连、扫不到、连不上等异常现象。

<a id="ble"></a>

## 常用使用场景（双模 BLE）

可参考组件 `components/bk_network_provisioning` 中的 BLE 配网实现（双模 GATT Server），
以及工程 `projects/bluetooth/headset` （经典蓝牙）。

<a id="id4"></a>

### 协议栈初始化

在应用初始化阶段先初始化协议栈，再注册 GAP 与 GATT Server 回调，最后注册 app 获取 `gatts_if` 。
`bk_ble_gatts_app_register` 是异步接口，需要在回调收到 `BK_GATTS_REG_EVT` 后才能拿到 `gatts_if` 。

```
//初始化双模协议栈
bk_bluetooth_init();

//注册 BLE GAP 事件回调，广播/扫描/连接等结果在此上报
bk_ble_gap_register_callback(dm_ble_gap_common_cb);

//注册 GATT Server 事件回调，建库/读写/连接等事件在此上报
bk_ble_gatts_register_callback(dm_gatts_cb);

//注册 app，等待回调中的 BK_GATTS_REG_EVT 事件取得 gatts_if
bk_ble_gatts_app_register(0);
```

GATT 事件回调中处理 `BK_GATTS_REG_EVT` ，保存 `gatts_if` ：

```
static bk_gatt_if_t s_gatts_if = 0;

static int32_t dm_gatts_cb(bk_gatts_cb_event_t event, bk_gatt_if_t gatts_if, bk_ble_gatts_cb_param_t *comm_param)
{
    switch (event)
    {
    case BK_GATTS_REG_EVT:
    {
        struct gatts_reg_evt_param *param = (typeof(param))comm_param;
        //保存 gatts_if，后续建库、收发数据都要用到
        s_gatts_if = param->gatt_if;
        //通知初始化流程继续（一般用信号量同步）
        break;
    }
    //...其它事件见后文
    default:
        break;
    }
    return 0;
}
```

<a id="gatt-server"></a>

### 创建 GATT Server 数据库

双模通过 `bk_gatts_attr_db_t` 属性表一次性描述 service、characteristic、descriptor，
再调用 `bk_ble_gatts_create_attr_tab` 下发。建库完成后在回调的 `BK_GATTS_CREAT_ATTR_TAB_EVT`
事件中取得每条记录的 attribute handle，最后通过 `bk_ble_gatts_start_service` 启动服务。

属性表示例（其中 `BK_GATT_PRIMARY_SERVICE_DECL` 、 `BK_GATT_CHAR_DECL` 等为示例工程封装的辅助宏，
用于填充 `bk_gatts_attr_db_t` 结构，可直接参考组件实现）：

```
static uint16_t s_prop_cli_config;
static uint8_t   s_ssid[64];
static uint8_t   s_password[64];

static const bk_gatts_attr_db_t s_gatts_attr_db[] =
{
    //Service 声明
    {
        BK_GATT_PRIMARY_SERVICE_DECL(0xfa00),
    },
    //Characteristic：notify 属性
    {
        BK_GATT_CHAR_DECL(0xea01, 0, NULL,
                          BK_GATT_CHAR_PROP_BIT_NOTIFY,
                          BK_GATT_PERM_READ,
                          BK_GATT_RSP_BY_APP),
    },
    //Client Characteristic Configuration Descriptor(CCCD)
    {
        BK_GATT_CHAR_DESC_DECL(BK_GATT_UUID_CHAR_CLIENT_CONFIG,
                               sizeof(s_prop_cli_config), (uint8_t *)&s_prop_cli_config,
                               BK_GATT_PERM_READ | BK_GATT_PERM_WRITE,
                               BK_GATT_RSP_BY_APP),
    },
    //可读可写的 Characteristic
    {
        BK_GATT_CHAR_DECL(0xea05, sizeof(s_ssid), (uint8_t *)s_ssid,
                          BK_GATT_CHAR_PROP_BIT_READ | BK_GATT_CHAR_PROP_BIT_WRITE,
                          BK_GATT_PERM_READ | BK_GATT_PERM_WRITE,
                          BK_GATT_AUTO_RSP),
    },
};

//记录建库返回的 handle，顺序与属性表一致
static uint16_t s_service_attr_handle;
static uint16_t s_char_attr_handle;
static uint16_t s_char_desc_attr_handle;
static uint16_t s_char_ssid_handle;
```

下发属性表并启动服务：

```
//下发属性表，第三个参数为属性表条目数，第四个参数为预留的最大 attr 数
bk_ble_gatts_create_attr_tab(s_gatts_attr_db, s_gatts_if,
                             sizeof(s_gatts_attr_db) / sizeof(s_gatts_attr_db[0]), 30);
//等待回调中的 BK_GATTS_CREAT_ATTR_TAB_EVT 取得各 handle

//启动服务
bk_ble_gatts_start_service(s_service_attr_handle);
//等待回调中的 BK_GATTS_START_EVT
```

在 `BK_GATTS_CREAT_ATTR_TAB_EVT` 中保存 handle：

```
case BK_GATTS_CREAT_ATTR_TAB_EVT:
{
    struct gatts_add_attr_tab_evt_param *param = (typeof(param))comm_param;
    //param->handles[i] 与属性表第 i 条记录一一对应
    s_service_attr_handle  = param->handles[0];
    s_char_attr_handle     = param->handles[1];
    s_char_desc_attr_handle= param->handles[2];
    s_char_ssid_handle     = param->handles[3];
    break;
}
```

<a id="id5"></a>

### 广播

双模 BLE 使用扩展广播接口。先设置设备名与广播参数，再设置广播随机地址（如使用随机地址），
然后设置广播数据，最后开启广播。每一步都需等待对应的 GAP 事件返回后再执行下一步。

```
#define ADV_HANDLE 0

//设置设备名
bk_ble_gap_set_device_name("bk_dm_demo");

//设置扩展广播参数
bk_ble_gap_ext_adv_params_t adv_param =
{
    .type          = BK_BLE_GAP_SET_EXT_ADV_PROP_LEGACY_IND,
    .interval_min  = 120,
    .interval_max  = 160,
    .channel_map   = BK_ADV_CHNL_ALL,
    .filter_policy = ADV_FILTER_ALLOW_SCAN_ANY_CON_ANY,
    .primary_phy   = BK_BLE_GAP_PRI_PHY_1M,
    .secondary_phy = BK_BLE_GAP_PHY_1M,
    .sid           = 0,
    .scan_req_notif= 0,
    .own_addr_type = BLE_ADDR_TYPE_PUBLIC,
};
bk_ble_gap_set_adv_params(ADV_HANDLE, &adv_param);
//等待回调中的 BK_BLE_GAP_EXT_ADV_PARAMS_SET_COMPLETE_EVT

//设置广播数据（raw 形式，按 [len][type][data...] 拼装）
uint8_t adv_data[31] = {0x02, 0x01, 0x06, /* ...更多 AD 结构... */};
bk_ble_gap_set_adv_data_raw(ADV_HANDLE, sizeof(adv_data), adv_data);
//等待回调中的 BK_BLE_GAP_EXT_ADV_DATA_RAW_SET_COMPLETE_EVT

//开启广播
const bk_ble_gap_ext_adv_t ext_adv =
{
    .instance   = ADV_HANDLE,
    .duration   = 0,
    .max_events = 0,
};
bk_ble_gap_adv_start(1, &ext_adv);
//等待回调中的 BK_BLE_GAP_EXT_ADV_START_COMPLETE_EVT
```

停止广播并删除广播集：

```
const uint8_t ext_adv_inst[] = {ADV_HANDLE};
bk_ble_gap_adv_stop(sizeof(ext_adv_inst) / sizeof(ext_adv_inst[0]), ext_adv_inst);
//等待 BK_BLE_GAP_EXT_ADV_STOP_COMPLETE_EVT

bk_ble_gap_adv_set_remove(ADV_HANDLE);
//等待 BK_BLE_GAP_EXT_ADV_SET_REMOVE_COMPLETE_EVT
```

<a id="id6"></a>

### 处理连接与读写

连接、断开、读、写等事件统一在 GATT Server 回调中处理。
对于 `BK_GATTS_READ_EVT` 、 `BK_GATTS_WRITE_EVT` ，若 `need_rsp` 为真，需调用
`bk_ble_gatts_send_response` 回复对端。

```
static uint16_t s_conn_id = ~0;

static int32_t dm_gatts_cb(bk_gatts_cb_event_t event, bk_gatt_if_t gatts_if, bk_ble_gatts_cb_param_t *comm_param)
{
    switch (event)
    {
    case BK_GATTS_CONNECT_EVT:
    {
        struct gatts_connect_evt_param *param = (typeof(param))comm_param;
        s_conn_id = param->conn_id;
        break;
    }
    case BK_GATTS_DISCONNECT_EVT:
    {
        s_conn_id = ~0;
        break;
    }
    case BK_GATTS_WRITE_EVT:
    {
        struct gatts_write_evt_param *param = (typeof(param))comm_param;
        //param->handle 标识被写记录，param->value/param->len 为写入内容
        if (param->need_rsp)
        {
            bk_gatt_rsp_t rsp = {0};
            rsp.attr_value.handle = param->handle;
            rsp.attr_value.offset = param->offset;
            rsp.attr_value.len    = param->len;
            rsp.attr_value.value  = param->value;
            bk_ble_gatts_send_response(gatts_if, param->conn_id, param->trans_id,
                                       BK_GATT_OK, &rsp);
        }
        break;
    }
    case BK_GATTS_READ_EVT:
    {
        struct gatts_read_evt_param *param = (typeof(param))comm_param;
        if (param->need_rsp)
        {
            uint16_t len = 0;
            uint8_t *val = NULL;
            bk_ble_gatts_get_attr_value(param->handle, &len, &val);

            bk_gatt_rsp_t rsp = {0};
            rsp.attr_value.handle = param->handle;
            rsp.attr_value.offset = param->offset;
            rsp.attr_value.len    = len;
            rsp.attr_value.value  = val;
            bk_ble_gatts_send_response(gatts_if, param->conn_id, param->trans_id,
                                       BK_GATT_OK, &rsp);
        }
        break;
    }
    default:
        break;
    }
    return 0;
}
```

<a id="id7"></a>

### 发送通知/指示

连接建立后，可通过 `bk_ble_gatts_send_indicate` 向对端发送数据。
`need_confirm` 为 false 时发送 notification，为 true 时发送 indication。

```
int dm_gatts_notify(uint8_t *data, uint16_t length)
{
    if (s_conn_id == (uint16_t)~0)
    {
        //未连接，不能发送
        return BK_FAIL;
    }
    //最后一个参数 need_confirm：false=notification，true=indication
    return bk_ble_gatts_send_indicate(s_gatts_if, s_conn_id, s_char_attr_handle,
                                      length, data, 0);
}
```

<a id="client"></a>

### 扫描与连接（主机/Client）

作为主机时，可通过 GAP 接口扫描并发起连接，连接结果在 GAP 回调中上报；
随后可使用 `bk_ble_gattc_*` 接口进行服务发现与读写。

```
//设置扫描参数后开启扫描，扫描结果在 GAP 回调的扫描事件中上报
bk_ble_ext_scan_params_t scan_param = {0};
//...填充 scan_param...
bk_ble_gap_set_scan_params(&scan_param);
bk_ble_gap_start_scan(0 /*duration*/, 0 /*period*/);

//发起连接
bk_gap_create_conn_params_t conn = {0};
//...填充对端地址等...
bk_ble_gap_connect(&conn);
//连接结果在 BK_BLE_GAP_CONNECT_COMPLETE_EVT 中上报
```

<a id="bt"></a>

## 经典蓝牙(BT)

经典蓝牙各 profile(A2DP/HFP/AVRCP/SPP) 的初始化与使用流程随 profile 不同，差异较大，
统一在对应工程中给出完整可运行示例，不在此逐一展开：

- `projects/bluetooth/headset` ：蓝牙耳机/音箱场景，包含 A2DP Sink、AVRCP、HFP HF 等。

对应 API 头文件： `bk_dm_a2dp.h` 、 `bk_dm_hfp.h` 、 `bk_dm_avrcp.h` 、 `bk_dm_spp.h` 、 `bk_dm_gap_bt.h` 。

<a id="id8"></a>

## 参考链接

> [蓝牙概述](bk_overview.md) 介绍了蓝牙整体架构、AP/CP 分工与两套协议栈
>
> [双模BLE API](../../api-reference/bluetooth/dual_ble.md) 介绍了双模下 BLE 的API接口
>
> [双模BT API](../../api-reference/bluetooth/dual_bt.md) 介绍了双模下经典蓝牙的API接口
>
> 样例演示：可参考工程
>
> 1. 多模经典蓝牙 headset（A2DP/HFP/AVRCP）：[headset](../../examples/projects/bluetooth/headset.md)
> 2. 多模ble HOGP device demo：[dm\_ble\_hogp\_device](../../examples/projects/bluetooth/dm_ble_hogp_device.md)
> 3. 多模ble gatt server：[dm\_ble\_gatt\_server](../../examples/projects/bluetooth/dm_ble_gatt_server.md)
> 4. 多模ble gatt client：[dm\_ble\_gatt\_client](../../examples/projects/bluetooth/dm_ble_gatt_client.md)
> 5. 多模ble le audio broadcast source：[broadcast\_source](../../examples/projects/bluetooth/le_audio/broadcast_source.md)
> 6. 多模ble le audio broadcast sink（含 Scan Delegator）：[broadcast\_sink](../../examples/projects/bluetooth/le_audio/broadcast_sink.md)
> 7. 多模ble le audio unicast client（含 Broadcast Assistant）：[unicast\_client](../../examples/projects/bluetooth/le_audio/unicast_client.md)
> 8. 多模ble le audio unicast server：[unicast\_server](../../examples/projects/bluetooth/le_audio/unicast_server.md)
