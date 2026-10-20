---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/wifi/bk_wifi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wi-fi-api"></a>

# Wi-Fi API

<a id="id1"></a>

## 概述

BK7259 SMP 上，客户应用在 **AP 核** 调用 `ap/include/modules/wifi.h` 中的 API；底层驱动在 CP 核执行，AP 侧经 IPC 自动转发。

使用说明、事件机制与示例工程请参阅 [Wi-Fi 开发者指南](../../developer-guide/wifi.md)。

<a id="id2"></a>

## 编程建议

重要

- 配置结构体预留字段应初始化为 0。
- 使用 `BK_ERR_CHECK` 或判断返回值处理 API 错误。
- STA/AP 配置建议先 `get` 再 `set`，或整体使用默认宏后修改必要字段。
- 事件回调中避免耗时操作，将业务转发到应用任务处理。
- 调用 `bk_init()` 完成 SDK 初始化；停止 Wi-Fi 使用 `bk_wifi_sta_stop()` / `bk_wifi_ap_stop()`；低功耗使用 PM 相关接口。本页仅列出 `ap/include` 公共头文件中的 API。

<a id="wifi-h"></a>

## wifi.h

<a id="header-file"></a>

### Header File

- [wifi.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/modules/wifi.h)

<a id="functions"></a>

### Functions

<a id="_CPPv417bk_wifi_sta_startv"></a>

<a id="_CPPv317bk_wifi_sta_startv"></a> <a id="_CPPv217bk_wifi_sta_startv"></a> <a id="bk_wifi_sta_start__void"></a> <a id="group__bk__api__wifi__v2_1gaaf144e78b9438143e21f7c75e8c23ecf"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_start(void)
:   This API initializes the WiFi driver, e.g. creating task for supplicant, allocating resource for low level WiFi driver etc.

    Usage example:

    ```
     wifi_init_config_t init_config = WIFI_DEFAULT_INIT_CONFIG();
     BK_LOG_ON_ERR(bk_wifi_init(&init_config);
    ```

    Start the BK STA

    **Attention**
    :   1\. This API is the 1st API that should be called before any other WiFi API can be called.

    **Attention**
    :   2\. Make sure the reserved field in config is zero, otherwise you may encounter compatibility issue in future if more config fields are added.

    This API init the resoure specific to BK STA, e.g. init STA specific globals, init the supplicant and STA specific WiFi driver etc.

    **Attention**
    :   1\. Make sure the [bk\_wifi\_sta\_set\_config()](#group__bk__api__wifi__v2_1ga0096c53cd18fce4b06d5229a7d63cb94) are succeedful before calling this API.

    **Attention**
    :   2\. This API connect the BK STA to the configured AP automatically.

    **Attention**
    :   3\. If the BK STA is already started, this API ignores the request and returns BK\_OK. if you want to restart the BK STA, call [bk\_wifi\_sta\_stop()](#group__bk__api__wifi__v2_1ga6f40eb9305ae390f7d777d652197894b) first and then call this API.

    **Attention**
    :   4\. TODO description about fast connection

    返回
    :   - BK\_OK: succeed
        - others: other errors.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_WIFI\_STA\_NOT\_CONFIG: the BK STA is not configured.
        - BK\_ERR\_WIFI\_MONITOR\_IP: the BK STA can’t be started because monitor is started.
        - others: other errors.

<a id="_CPPv416bk_wifi_sta_stopv"></a>

<a id="_CPPv316bk_wifi_sta_stopv"></a> <a id="_CPPv216bk_wifi_sta_stopv"></a> <a id="bk_wifi_sta_stop__void"></a> <a id="group__bk__api__wifi__v2_1ga6f40eb9305ae390f7d777d652197894b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_stop(void)
:   Stop the BK STA.

    **Attention**
    :   This API causes the BK STA disconnect from the AP, it similar as [bk\_wifi\_sta\_disconnect()](#group__bk__api__wifi__v2_1gae00bc75a589a66a378037c5adb05bc11), but this API may free resource.

    返回
    :   - BK\_OK: succeed
        - BK\_FAIL: fail

<a id="_CPPv417bk_wifi_scan_stopv"></a>

<a id="_CPPv317bk_wifi_scan_stopv"></a> <a id="_CPPv217bk_wifi_scan_stopv"></a> <a id="bk_wifi_scan_stop__void"></a> <a id="group__bk__api__wifi__v2_1gac82b880ed9021836162aca4aebd4c3e0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_scan\_stop(void)
:   Stop the pure scan operation.

    **Attention**
    :   This API causes the BK STA disconnect from the AP, it similar as [bk\_wifi\_sta\_disconnect()](#group__bk__api__wifi__v2_1gae00bc75a589a66a378037c5adb05bc11), but this API may free resource.

    返回
    :   - BK\_OK: succeed
        - BK\_FAIL: fail

<a id="_CPPv422bk_wifi_sta_set_configPK17wifi_sta_config_t"></a>

<a id="_CPPv322bk_wifi_sta_set_configPK17wifi_sta_config_t"></a> <a id="_CPPv222bk_wifi_sta_set_configPK17wifi_sta_config_t"></a> <a id="bk_wifi_sta_set_config__wifi_sta_config_tCP"></a> <a id="group__bk__api__wifi__v2_1ga0096c53cd18fce4b06d5229a7d63cb94"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_set\_config(const [wifi\_sta\_config\_t](bk_wifi_types.md#_CPPv417wifi_sta_config_t "wifi_sta_config_t") \*sta\_config)
:   Config the BK STA.

    This API configures the basic configurations of the BK STA, it should be called before we call [bk\_wifi\_sta\_start()](#group__bk__api__wifi__v2_1gaaf144e78b9438143e21f7c75e8c23ecf) to start the BK STA. It can also be used to update the configuration after the BK STA is started.

    Usage example:

    ```
    wifi_sta_config_t sta_config = WIFI_DEFAULT_STA_CONFIG();

    os_strncpy(sta_config.ssid, "ssid", WIFI_SSID_STR_LEN);
    os_strncpy(sta_config.password, "password", WIFI_PASSWORD_LEN);
    //more initialization here
    BK_LOG_ON_ERR(bk_wifi_sta_set_config(&sta_config));
    ```

    **Attention**
    :   1\. Don’t call this API when the monitor is in-progress

    **Attention**
    :   2\. If STA is already connected to AP, this API cases BK STA reconnects the AP.

    **Attention**
    :   3\. Make sure the reserved fields in sta\_config is zero, otherwise you may encounter compatibility issue in future if more config fields are added.

    **Attention**
    :   4\. Auto reconnect max count and timeout can be set. When user app receives EVENT\_WIFI\_STA\_DISCONNECTED event, it’s user app’s responsibility to reconnect to AP manually. Max count and timeout set to zero to let supplicant automatically handles connection without user app’s interaction.

    参数
    :   **sta\_config** – the STA configuration

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_WIFI\_NOT\_INIT: the STA is not initialized, call bk\_wifi\_init() first.
        - BK\_ERR\_NULL\_PARAM: parameter config is NULL.
        - BK\_ERR\_WIFI\_RESERVED\_FIELD: the reserved field of config is not 0\.
        - others: other errors

<a id="_CPPv422bk_wifi_sta_get_configP17wifi_sta_config_t"></a>

<a id="_CPPv322bk_wifi_sta_get_configP17wifi_sta_config_t"></a> <a id="_CPPv222bk_wifi_sta_get_configP17wifi_sta_config_t"></a> <a id="bk_wifi_sta_get_config__wifi_sta_config_tP"></a> <a id="group__bk__api__wifi__v2_1gabd063029cb792bd168970dd1f8dd06b3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_get\_config([wifi\_sta\_config\_t](bk_wifi_types.md#_CPPv417wifi_sta_config_t "wifi_sta_config_t") \*sta\_config)
:   Get the configuration of the BK STA.

    参数
    :   **sta\_config** – store the BK STA configuration

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: the parameter config is NULL.
        - BK\_ERR\_WIFI\_STA\_NOT\_CONFIG: STA is not configured yet.
        - others: other errors

<a id="_CPPv437bk_wifi_sta_get_linkstate_with_reasonP23wifi_linkstate_reason_t"></a>

<a id="_CPPv337bk_wifi_sta_get_linkstate_with_reasonP23wifi_linkstate_reason_t"></a> <a id="_CPPv237bk_wifi_sta_get_linkstate_with_reasonP23wifi_linkstate_reason_t"></a> <a id="bk_wifi_sta_get_linkstate_with_reason__wifi_linkstate_reason_tP"></a> <a id="group__bk__api__wifi__v2_1ga80b3efdbbca7a35ac7bdfb38546b8ccb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_get\_linkstate\_with\_reason([wifi\_linkstate\_reason\_t](bk_wifi_types.md#_CPPv423wifi_linkstate_reason_t "wifi_linkstate_reason_t") \*info)
:   Get the WiFi station state of the BK STA.

    - If sta is idle or connected, reason code will be WIFI\_REASON\_MAX

    **Attention**
    :   the difference between this API and [bk\_wifi\_sta\_get\_link\_status()](#group__bk__api__wifi__v2_1ga05fa3da4689980df705e03c6416df12e) is

        - This API gets the actual WiFi STA link status and reason code

    参数
    :   **state** – store the WiFi station state of the BK STA

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: the parameter config is NULL.
        - others: other errors

<a id="_CPPv427bk_wifi_sta_get_link_statusP18wifi_link_status_t"></a>

<a id="_CPPv327bk_wifi_sta_get_link_statusP18wifi_link_status_t"></a> <a id="_CPPv227bk_wifi_sta_get_link_statusP18wifi_link_status_t"></a> <a id="bk_wifi_sta_get_link_status__wifi_link_status_tP"></a> <a id="group__bk__api__wifi__v2_1ga05fa3da4689980df705e03c6416df12e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_get\_link\_status([wifi\_link\_status\_t](bk_wifi_types.md#_CPPv418wifi_link_status_t "wifi_link_status_t") \*link\_status)
:   Get the WiFi link info of the BK STA.

    Get the actual WiFi link status of the BK STA.

    **Attention**
    :   the difference between this API and [bk\_wifi\_sta\_get\_config()](#group__bk__api__wifi__v2_1gabd063029cb792bd168970dd1f8dd06b3) is

        - This API gets the actual STA link info while the later gets the configured value
        - This API can get more info of the link, such as RSSI, WiFi link status, AID etc.
        - The AID is only valid if @link\_status-\>state is WIFI\_LINK\_CONNECTED.

    参数
    :   **link\_status** – store the WiFi link status of the BK STA

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: the parameter link\_info is NULL.
        - BK\_ERR\_WIFI\_DRIVER: WiFi low level driver has failure.
        - BK\_ERR\_WIFI\_NO\_MEM: Not enough memory
        - others: other errors

<a id="_CPPv419bk_wifi_sta_connectv"></a>

<a id="_CPPv319bk_wifi_sta_connectv"></a> <a id="_CPPv219bk_wifi_sta_connectv"></a> <a id="bk_wifi_sta_connect__void"></a> <a id="group__bk__api__wifi__v2_1ga6a74829e23ce17663cb2480d02e07c06"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_connect(void)
:   Connect the BK STA to the AP.

    **Attention**
    :   1\. Make sure STA is started by [bk\_wifi\_sta\_start()](#group__bk__api__wifi__v2_1gaaf144e78b9438143e21f7c75e8c23ecf) before calling this API.

    **Attention**
    :   2\. Don’t call this API when the monitor is in-progress

    **Attention**
    :   3\. If STA is already connected to AP, this API reconnects the BK STA.

    **Attention**
    :   4\. TODO \- multiple same SSID connect???

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_WIFI\_STA\_NOT\_STARTED: the STA is not started, call [bk\_wifi\_sta\_start()](#group__bk__api__wifi__v2_1gaaf144e78b9438143e21f7c75e8c23ecf) first.
        - BK\_ERR\_WIFI\_MONITOR\_IP: the API is not allowed because monitor is in-progress.
        - others: other failures.

<a id="_CPPv422bk_wifi_sta_disconnectv"></a>

<a id="_CPPv322bk_wifi_sta_disconnectv"></a> <a id="_CPPv222bk_wifi_sta_disconnectv"></a> <a id="bk_wifi_sta_disconnect__void"></a> <a id="group__bk__api__wifi__v2_1gae00bc75a589a66a378037c5adb05bc11"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_disconnect(void)
:   Disconnect the WiFi connection of the BK STA.

    **Attention**
    :   TODO \- add description about disconnect event!

    返回
    :   - BK\_OK: succeed
        - others: other failures.

<a id="_CPPv418bk_wifi_scan_startPK18wifi_scan_config_t"></a>

<a id="_CPPv318bk_wifi_scan_startPK18wifi_scan_config_t"></a> <a id="_CPPv218bk_wifi_scan_startPK18wifi_scan_config_t"></a> <a id="bk_wifi_scan_start__wifi_scan_config_tCP"></a> <a id="group__bk__api__wifi__v2_1gaf4b85a984fa5c5d633769274a50b5b9c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_scan\_start(const [wifi\_scan\_config\_t](bk_wifi_types.md#_CPPv418wifi_scan_config_t "wifi_scan_config_t") \*scan\_config)
:   Start a scan.

    This API notifies the WiFi driver to start a scan, the event EVENT\_WIFI\_SCAN\_DONE will be raised if the scan is completed. General steps to use this API:

    - prepare the scan done event callback, the callback can call [bk\_wifi\_scan\_get\_result()](#group__bk__api__wifi__v2_1ga381d59740e2a90c6dbeef0c9eec345dc) to get the scan result and then call [bk\_wifi\_scan\_free\_result()](#group__bk__api__wifi__v2_1ga75df3c75b3bd8844e9e68c8e339859b6) to free the resource.
    - call bk\_event\_register\_cb(EVENT\_MOD\_WIFI, EVENT\_WIFI\_SCAN\_DONE, …) to register scan done event callback.
    - call this API to trigger this the scan.

    Usage example:

    ```
    //Define your scan done handler
    int scan_done_handler(void *arg, event_module_t event_module, int event_id, void *event_data)
    {
        wifi_scan_result_t scan_result = {0};

        BK_LOG_ON_ERR(bk_wifi_scan_get_result(&scan_result));
        bk_wifi_scan_dump_result(&scan_result);
        bk_wifi_scan_free_result(&scan_result);

        return BK_OK;
    }

    //Start the scan
    wifi_scan_config_t config = {0};

    BK_LOG_ON_ERR(bk_event_register_cb(EVENT_MOD_WIFI, EVENT_WIFI_SCAN_DONE, scan_done_handler, NULL));
    BK_LOG_ON_ERR(bk_wifi_scan_start(&scan_config));
    ```

    **Attention**
    :   1\. This API triggers an active scan on all channels (TODO double check)

    **Attention**
    :   2\. Pass NULL scan\_config to scan all APs, otherwise scan the SSID specified in scan\_config.ssid

    **Attention**
    :   3\. Make sure the reserved fields in scan\_config is zero, otherwise you may encounter compatibility issue in future if more config fields are added.

    **Attention**
    :   4\. TODO scan result limits???

    参数
    :   **scan\_config** – the configuration of scan

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_WIFI\_NOT\_INIT: the STA is not initialized, call bk\_wifi\_init() first.
        - BK\_ERR\_WIFI\_MONITOR\_IP: the API is not allowed because monitor is in-progress.
        - others: other failures.

<a id="_CPPv423bk_wifi_scan_get_resultP18wifi_scan_result_t"></a>

<a id="_CPPv323bk_wifi_scan_get_resultP18wifi_scan_result_t"></a> <a id="_CPPv223bk_wifi_scan_get_resultP18wifi_scan_result_t"></a> <a id="bk_wifi_scan_get_result__wifi_scan_result_tP"></a> <a id="group__bk__api__wifi__v2_1ga381d59740e2a90c6dbeef0c9eec345dc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_scan\_get\_result([wifi\_scan\_result\_t](bk_wifi_types.md#_CPPv418wifi_scan_result_t "wifi_scan_result_t") \*scan\_result)
:   Get the scan result.

    Usage example:

    ```
    wifi_scan_result_t scan_result = {0};

    BK_LOG_ON_ERR(bk_wifi_scan_get_result(&scan_result));
    bk_wifi_scan_free_result(&scan_result);
    ```

    **Attention**
    :   1\. The caller don’t need to allocate memory for scan\_result-\>aps, this API will allocate the memory for scan\_result-\>aps according to the actual found AP number.

    **Attention**
    :   2\. Don’t forget to call bk\_wifi\_scan\_free\_result(\&scan\_result) to free the the resource allocated in this API, otherwise memory leak.

    参数
    :   **scan\_result** – store the scan result

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: NULL scan\_result
        - BK\_ERR\_NO\_MEM: out of memory
        - others: other failures

<a id="_CPPv424bk_wifi_scan_dump_resultPK18wifi_scan_result_t"></a>

<a id="_CPPv324bk_wifi_scan_dump_resultPK18wifi_scan_result_t"></a> <a id="_CPPv224bk_wifi_scan_dump_resultPK18wifi_scan_result_t"></a> <a id="bk_wifi_scan_dump_result__wifi_scan_result_tCP"></a> <a id="group__bk__api__wifi__v2_1gaf4eee514ca5fa831a6d403bdb838efa7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_scan\_dump\_result(const [wifi\_scan\_result\_t](bk_wifi_types.md#_CPPv418wifi_scan_result_t "wifi_scan_result_t") \*scan\_result)
:   Dump the scan result.

    参数
    :   **scan\_result** – The scan result to be dumped.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PARAM: invalid scan result

<a id="_CPPv424bk_wifi_scan_free_resultP18wifi_scan_result_t"></a>

<a id="_CPPv324bk_wifi_scan_free_resultP18wifi_scan_result_t"></a> <a id="_CPPv224bk_wifi_scan_free_resultP18wifi_scan_result_t"></a> <a id="bk_wifi_scan_free_result__wifi_scan_result_tP"></a> <a id="group__bk__api__wifi__v2_1ga75df3c75b3bd8844e9e68c8e339859b6"></a> void bk\_wifi\_scan\_free\_result([wifi\_scan\_result\_t](bk_wifi_types.md#_CPPv418wifi_scan_result_t "wifi_scan_result_t") \*scan\_result)
:   Free the scan result.

    **Attention**
    :   This API free scan\_result-\>aps which allocated in [bk\_wifi\_scan\_get\_result()](#group__bk__api__wifi__v2_1ga381d59740e2a90c6dbeef0c9eec345dc), it doesn’t free scan\_result. So if scan\_result is allocated by the caller, the caller need to free it.

    参数
    :   **scan\_result** – The scan result to be freed.

    返回
    :   - BK\_OK: always succeed

<a id="_CPPv425bk_wifi_sta_add_vendor_ie7uint8_tP7uint8_t7uint8_t"></a>

<a id="_CPPv325bk_wifi_sta_add_vendor_ie7uint8_tP7uint8_t7uint8_t"></a> <a id="_CPPv225bk_wifi_sta_add_vendor_ie7uint8_tP7uint8_t7uint8_t"></a> <a id="bk_wifi_sta_add_vendor_ie__uint8_t.uint8_tP.uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga25b95ae1a74d886532f705319f1cc015"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_add\_vendor\_ie(uint8\_t frame, uint8\_t \*vsie, uint8\_t len)
:   Add/Update/Del STA’s Vendor Specific IE **before** connect to AP.

    **Attention**
    :   If you want to add vsie when sta starts, just initialize [wifi\_sta\_config\_t](bk_wifi_types.md#structwifi__sta__config__t) when call [bk\_wifi\_sta\_set\_config()](#group__bk__api__wifi__v2_1ga0096c53cd18fce4b06d5229a7d63cb94).

    参数
    :   - **buf** – vsie buf
        - **len** – vsie buf len

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv428bk_wifi_sta_update_vendor_ie7uint8_tP7uint8_t7uint8_t"></a>

<a id="_CPPv328bk_wifi_sta_update_vendor_ie7uint8_tP7uint8_t7uint8_t"></a> <a id="_CPPv228bk_wifi_sta_update_vendor_ie7uint8_tP7uint8_t7uint8_t"></a> <a id="bk_wifi_sta_update_vendor_ie__uint8_t.uint8_tP.uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga1f7834c37e0b43e89aaa17f3c1226fa9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_update\_vendor\_ie(uint8\_t frame, uint8\_t \*vsie, uint8\_t len)

<a id="_CPPv425bk_wifi_sta_del_vendor_ie7uint8_t"></a>

<a id="_CPPv325bk_wifi_sta_del_vendor_ie7uint8_t"></a> <a id="_CPPv225bk_wifi_sta_del_vendor_ie7uint8_t"></a> <a id="bk_wifi_sta_del_vendor_ie__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga4cf14b2234ba6e83aedc62ac825da03d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_del\_vendor\_ie(uint8\_t frame)

<a id="_CPPv416bk_wifi_ap_startv"></a>

<a id="_CPPv316bk_wifi_ap_startv"></a> <a id="_CPPv216bk_wifi_ap_startv"></a> <a id="bk_wifi_ap_start__void"></a> <a id="group__bk__api__wifi__v2_1ga664be1db35e4ef799f2178bfc466a2e5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_start(void)
:   Start the BK AP.

    This API init the resoure specific to BK AP, e.g. init BK AP specific globals, init the hostapd and AP specific WiFi driver etc.

    If the BK AP is already started, this API ignores the request and returns BK\_OK, we can call [bk\_wifi\_ap\_stop()](#group__bk__api__wifi__v2_1ga1836b0aeeb20668e861bad0baa2ea0d3) to stop BK AP first and then call [bk\_wifi\_ap\_start()](#group__bk__api__wifi__v2_1ga664be1db35e4ef799f2178bfc466a2e5) to restart it.

    **Restart** AP Usage example:

    ```
    BK_LOG_ON_ERR(bk_wifi_ap_stop());
    BK_LOG_ON_ERR(bk_wifi_ap_start());
    ```

    **Attention**
    :   1\. Don’t call this API when the monitor is in-progress

    **Attention**
    :   2\. If [bk\_wifi\_ap\_set\_config()](#group__bk__api__wifi__v2_1gac05d9c08d2f9212ad8568f0c6922db39) is not called, this API start the AP with default value, normally you should configure the AP first before calling this API.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_WIFI\_AP\_NOT\_CONFIG: the WiFi AP is not configured, call [bk\_wifi\_ap\_set\_config()](#group__bk__api__wifi__v2_1gac05d9c08d2f9212ad8568f0c6922db39) first.
        - others: other errors

<a id="_CPPv415bk_wifi_ap_stopv"></a>

<a id="_CPPv315bk_wifi_ap_stopv"></a> <a id="_CPPv215bk_wifi_ap_stopv"></a> <a id="bk_wifi_ap_stop__void"></a> <a id="group__bk__api__wifi__v2_1ga1836b0aeeb20668e861bad0baa2ea0d3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_stop(void)
:   Stop the BK AP.

    返回
    :   - BK\_OK: succeed
        - BK\_WIFI\_NOT\_INIT: the WiFi is not initialized, call bk\_wifi\_init() first.
        - others: other errors

<a id="_CPPv421bk_wifi_ap_set_configPK16wifi_ap_config_t"></a>

<a id="_CPPv321bk_wifi_ap_set_configPK16wifi_ap_config_t"></a> <a id="_CPPv221bk_wifi_ap_set_configPK16wifi_ap_config_t"></a> <a id="bk_wifi_ap_set_config__wifi_ap_config_tCP"></a> <a id="group__bk__api__wifi__v2_1gac05d9c08d2f9212ad8568f0c6922db39"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_set\_config(const [wifi\_ap\_config\_t](bk_wifi_types.md#_CPPv416wifi_ap_config_t "wifi_ap_config_t") \*ap\_config)
:   Config the BK AP.

    Usage example:

    ```
    wifi_ap_config_t ap_config = WIFI_DEFAULT_AP_CONFIG();

    os_strncpy(ap_config.ssid, "ssid", WIFI_SSID_STR_LEN);
    os_strncpy(ap_config.password, "password", WIFI_PASSWORD_LEN);
    BK_LOG_ON_ERR(bk_wifi_ap_set_config(&ap_config));
    ```

    **Attention**
    :   1\. Make sure the reserved field in config is zero, otherwise you may encounter compatibility issue in future if more config fields are added.

    参数
    :   **ap\_config** – the AP configuration

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: the ap\_config is NULL.
        - others: other errors

<a id="_CPPv421bk_wifi_ap_get_configP16wifi_ap_config_t"></a>

<a id="_CPPv321bk_wifi_ap_get_configP16wifi_ap_config_t"></a> <a id="_CPPv221bk_wifi_ap_get_configP16wifi_ap_config_t"></a> <a id="bk_wifi_ap_get_config__wifi_ap_config_tP"></a> <a id="group__bk__api__wifi__v2_1ga932494dcee096896906446086d82649b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_get\_config([wifi\_ap\_config\_t](bk_wifi_types.md#_CPPv416wifi_ap_config_t "wifi_ap_config_t") \*ap\_config)
:   Get the configuration of the BK AP.

    参数
    :   **ap\_config** – store the configuration of BK AP

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: the parameter config is NULL.
        - others: other errors

<a id="_CPPv423bk_wifi_ap_get_sta_listP14wlan_ap_stas_t"></a>

<a id="_CPPv323bk_wifi_ap_get_sta_listP14wlan_ap_stas_t"></a> <a id="_CPPv223bk_wifi_ap_get_sta_listP14wlan_ap_stas_t"></a> <a id="bk_wifi_ap_get_sta_list__wlan_ap_stas_tP"></a> <a id="group__bk__api__wifi__v2_1ga3c4500ec7dd69bf6d5b344f0ca22b330"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_get\_sta\_list([wlan\_ap\_stas\_t](bk_wifi_types.md#_CPPv414wlan_ap_stas_t "wlan_ap_stas_t") \*stas)
:   Get the STAs connected to BK AP.

    **Attention**
    :   Free stas-\>sta after usage.

    参数
    :   **stas** – store the STA list in BK AP

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv421bk_wifi_calculate_pmkPKcPKcPc"></a>

<a id="_CPPv321bk_wifi_calculate_pmkPKcPKcPc"></a> <a id="_CPPv221bk_wifi_calculate_pmkPKcPKcPc"></a> <a id="bk_wifi_calculate_pmk__cCP.cCP.cP"></a> <a id="group__bk__api__wifi__v2_1ga12b1db14c57293e05e32a7ec1047883a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_calculate\_pmk(const char \*ssid, const char \*pwd, char \*pmk)
:   Calculate softap’s Pmk when softap is starts.

    参数
    :   - **ssid** – softap’s ssid
        - **pwd** – softap’s pwd
        - **pmk** – softap’s pmk

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv424bk_wifi_ap_add_vendor_iePv7uint8_t"></a>

<a id="_CPPv324bk_wifi_ap_add_vendor_iePv7uint8_t"></a> <a id="_CPPv224bk_wifi_ap_add_vendor_iePv7uint8_t"></a> <a id="bk_wifi_ap_add_vendor_ie__voidP.uint8_t"></a> <a id="group__bk__api__wifi__v2_1gabe2ffb072255ac1f6a7bd3e271aa904a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_add\_vendor\_ie(void \*buf, uint8\_t len)
:   Add softap’s Vendor Specific IE when softap is running.

    **Attention**
    :   If you want to add vsie when softap starts, just initialize [wifi\_ap\_config\_t](bk_wifi_types.md#structwifi__ap__config__t) when call [bk\_wifi\_ap\_start()](#group__bk__api__wifi__v2_1ga664be1db35e4ef799f2178bfc466a2e5).

    参数
    :   - **buf** – vsie buf
        - **len** – vsie buf len

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv424bk_wifi_ap_del_vendor_iev"></a>

<a id="_CPPv324bk_wifi_ap_del_vendor_iev"></a> <a id="_CPPv224bk_wifi_ap_del_vendor_iev"></a> <a id="bk_wifi_ap_del_vendor_ie__void"></a> <a id="group__bk__api__wifi__v2_1ga8fdeff9c4e3ad6180eb74bafc452ca62"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_del\_vendor\_ie(void)
:   Delete softap’s Vendor Specific IE when softap is running.

    **Attention**
    :   If you want to add vsie when softap starts, just initialize [wifi\_ap\_config\_t](bk_wifi_types.md#structwifi__ap__config__t) when call [bk\_wifi\_ap\_start()](#group__bk__api__wifi__v2_1ga664be1db35e4ef799f2178bfc466a2e5).

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv428bk_wifi_ap_update_hidden_capb"></a>

<a id="_CPPv328bk_wifi_ap_update_hidden_capb"></a> <a id="_CPPv228bk_wifi_ap_update_hidden_capb"></a> <a id="bk_wifi_ap_update_hidden_cap__b"></a> <a id="group__bk__api__wifi__v2_1ga178bace6234723471c6d00b671a998ca"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_update\_hidden\_cap(bool flag)
:   Update softap’s Hidden Ssid Capaility when softap is running.

    - BK\_OK: succeed
    - others: other errors

    **Attention**
    :   If you want to update hidden ssid capability when softap starts, just call [bk\_wifi\_ap\_update\_hidden\_cap()](#group__bk__api__wifi__v2_1ga178bace6234723471c6d00b671a998ca).

    参数
    :   **flag** – set true for hidden ssid

    返回

<a id="_CPPv421bk_wifi_monitor_startv"></a>

<a id="_CPPv321bk_wifi_monitor_startv"></a> <a id="_CPPv221bk_wifi_monitor_startv"></a> <a id="bk_wifi_monitor_start__void"></a> <a id="group__bk__api__wifi__v2_1gafb67a0a2f743a9dbf65904a0a685a26f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_monitor\_start(void)
:   Start the monitor.

    **Attention**
    :   1\. When monitor mode is enabled, the scan will not work and [bk\_wifi\_scan\_start()](#group__bk__api__wifi__v2_1gaf4b85a984fa5c5d633769274a50b5b9c) returns BK\_ERR\_WIFI\_MONITOR\_IP.

    **Attention**
    :   2\. When monitor mode is enabled, the STA connect will not work and [bk\_wifi\_sta\_connect()](#group__bk__api__wifi__v2_1ga6a74829e23ce17663cb2480d02e07c06) returns BK\_ERR\_WIFI\_MONITOR\_IP.

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv420bk_wifi_monitor_stopv"></a>

<a id="_CPPv320bk_wifi_monitor_stopv"></a> <a id="_CPPv220bk_wifi_monitor_stopv"></a> <a id="bk_wifi_monitor_stop__void"></a> <a id="group__bk__api__wifi__v2_1ga64895e925025cb2b891abbf4f4608ab4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_monitor\_stop(void)
:   Stop the monitor.

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv426bk_wifi_monitor_set_configPK21wifi_monitor_config_t"></a>

<a id="_CPPv326bk_wifi_monitor_set_configPK21wifi_monitor_config_t"></a> <a id="_CPPv226bk_wifi_monitor_set_configPK21wifi_monitor_config_t"></a> <a id="bk_wifi_monitor_set_config__wifi_monitor_config_tCP"></a> <a id="group__bk__api__wifi__v2_1ga5bfbda3bbaa90a4ff3daa19e9acbbb3f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_monitor\_set\_config(const [wifi\_monitor\_config\_t](bk_wifi_types.md#_CPPv421wifi_monitor_config_t "wifi_monitor_config_t") \*monitor\_config)
:   Configure the monitor.

    参数
    :   **monitor\_config** – the configuration of monitor

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv426bk_wifi_monitor_get_configP21wifi_monitor_config_t"></a>

<a id="_CPPv326bk_wifi_monitor_get_configP21wifi_monitor_config_t"></a> <a id="_CPPv226bk_wifi_monitor_get_configP21wifi_monitor_config_t"></a> <a id="bk_wifi_monitor_get_config__wifi_monitor_config_tP"></a> <a id="group__bk__api__wifi__v2_1ga6013fd42f04c9acbee9a60ba1cc00fe5"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_monitor\_get\_config([wifi\_monitor\_config\_t](bk_wifi_types.md#_CPPv421wifi_monitor_config_t "wifi_monitor_config_t") \*monitor\_config)
:   Get the configuration of the monitor.

    参数
    :   **monitor\_config** – store the configuration of monitor

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv427bk_wifi_monitor_register_cbK17wifi_monitor_cb_t"></a>

<a id="_CPPv327bk_wifi_monitor_register_cbK17wifi_monitor_cb_t"></a> <a id="_CPPv227bk_wifi_monitor_register_cbK17wifi_monitor_cb_t"></a> <a id="bk_wifi_monitor_register_cb__wifi_monitor_cb_tC"></a> <a id="group__bk__api__wifi__v2_1ga61920d478aa5884503b20874337d62bb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_monitor\_register\_cb(const [wifi\_monitor\_cb\_t](bk_wifi_types.md#_CPPv417wifi_monitor_cb_t "wifi_monitor_cb_t") monitor\_cb)
:   Register the user callback of monitor.

    参数
    :   **monitor\_cb** – monitor callback

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv427bk_wifi_monitor_set_channelPK14wifi_channel_t"></a>

<a id="_CPPv327bk_wifi_monitor_set_channelPK14wifi_channel_t"></a> <a id="_CPPv227bk_wifi_monitor_set_channelPK14wifi_channel_t"></a> <a id="bk_wifi_monitor_set_channel__wifi_channel_tCP"></a> <a id="group__bk__api__wifi__v2_1gae2ba858f657a0e9dbb9fe594a83e0e87"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_monitor\_set\_channel(const [wifi\_channel\_t](bk_wifi_types.md#_CPPv414wifi_channel_t "wifi_channel_t") \*chan)
:   Set monitor channel.

    **Attention**
    :   1\. Currently we only support HT20, chan-\>second should always be 0\.

    **Attention**
    :   2\. This API is only used for settting monitor channel, NOT for other purpose.

    **Attention**
    :   3\. This API directly change the hardware channel, it may impacts BK STA/AP if the STA or AP interface is started. TODO describe details of the impact.

    **Attention**
    :   4\. The channel range can be set is from channel 1 to channel 14,

    参数
    :   **chan** – channel of monitor

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv422bk_wifi_monitor_resumev"></a>

<a id="_CPPv322bk_wifi_monitor_resumev"></a> <a id="_CPPv222bk_wifi_monitor_resumev"></a> <a id="bk_wifi_monitor_resume__void"></a> <a id="group__bk__api__wifi__v2_1gab6679fbb4ae72b047ec3b535a69661c3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_monitor\_resume(void)
:   resume the monitor to wakeup Wi-Fi from sleep mode

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv423bk_wifi_monitor_suspendv"></a>

<a id="_CPPv323bk_wifi_monitor_suspendv"></a> <a id="_CPPv223bk_wifi_monitor_suspendv"></a> <a id="bk_wifi_monitor_suspend__void"></a> <a id="group__bk__api__wifi__v2_1gac579e95b5dd742c3cb349eff26a666bb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_monitor\_suspend(void)
:   suspend the monitor to allow Wi-Fi can goto sleep mode

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv417bk_wifi_twt_setup7uint8_t8uint16_t7uint8_t"></a>

<a id="_CPPv317bk_wifi_twt_setup7uint8_t8uint16_t7uint8_t"></a> <a id="_CPPv217bk_wifi_twt_setup7uint8_t8uint16_t7uint8_t"></a> <a id="bk_wifi_twt_setup__uint8_t.uint16_t.uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga5def7b7b5e3cdb6a2e0c85b4aabe202d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_twt\_setup(uint8\_t setup\_type, uint16\_t mantissa, uint8\_t min\_twt)
:   twt set up

    参数
    :   - **setup\_type** – suggest/demand
        - **mantissa** – wake\_int\_mantissa
        - **min\_twt** – min\_twt\_wake\_dur

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv420bk_wifi_twt_teardownv"></a>

<a id="_CPPv320bk_wifi_twt_teardownv"></a> <a id="_CPPv220bk_wifi_twt_teardownv"></a> <a id="bk_wifi_twt_teardown__void"></a> <a id="group__bk__api__wifi__v2_1ga1e37ef1e6e1b3082152d2fe87b462916"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_twt\_teardown(void)
:   twt tear down

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv425bk_wifi_filter_set_configPK20wifi_filter_config_t"></a>

<a id="_CPPv325bk_wifi_filter_set_configPK20wifi_filter_config_t"></a> <a id="_CPPv225bk_wifi_filter_set_configPK20wifi_filter_config_t"></a> <a id="bk_wifi_filter_set_config__wifi_filter_config_tCP"></a> <a id="group__bk__api__wifi__v2_1gad89834d0bcf579fe0ac338cb0fcf3d21"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_filter\_set\_config(const [wifi\_filter\_config\_t](bk_wifi_types.md#_CPPv420wifi_filter_config_t "wifi_filter_config_t") \*filter\_config)
:   Set the filter configuration.

    The filter is used to configure what kind of management packets can be received by the filter callback registered by [bk\_wifi\_filter\_register\_cb()](#group__bk__api__wifi__v2_1ga0276b4fd054e03c62f79e0b52b1870c0).

    Per the WiFi receiving data path, the management frames are firstly received by WiFi hardware, then the hardware relays them to WiFi software (WiFi driver). Normally the hardware receives all management frames in the air, however it don’t relay all of them to WiFi driver (WiFi software), it only relays management frames necessary to STA or AP or scan or monitor, depends on which interface or function are enabled. In other word, WiFi driver only receives management frames necessary to them from hardware.

    When no filter callback is registered, all management frame processing is ended in WiFi driver unless the filter callback is registered.

    If filter callback is register and if filter\_config.rx\_all\_default\_mgmt is set to 1, then all the management frames received by WiFi driver are relayed to the filter callback. **Notified that the default management frame types can be received depends on whether STA or AP or scan or monitor are enabled or not, e.g. when only STA is enabled, the WiFi driver needs to handle PROBE response, but don’t need to handle PROBE request, so the WiFi driver only receive PROBE response from WiFi hardware**.

    Here is summary about default management frame received by WiFi:

    | Condition | Default management frame |
    | --- | --- |
    | STA connected | Management frames sent by the connected AP, such as beacon etc. |
    | AP started | Management frames sent by connected STA and probe request etc. |
    | Scan starting | Probe response and beacon frames of all APs. |
    | Monitor started | All kind of management frames |

    How about if the filter callback wants to receive more management frame types, e.g. want to receive PROBE request when only STA is enabled. We can set filter\_config-\>rx\_probe\_req to receive PROBE response no matter whether AP is enabled or NOT.

    Usage example:

    ```
    // Only receive management frame default received by WiFi driver
    // Equal to the case when bk_wifi_filter_set_config() is not called
    wifi_filter_config_t filter_config = WIFI_DEFAULT_FILTER_CONFIG();
    BK_LOG_ON_ERR(bk_wifi_filter_set_config(&filter_config);

    // Receive all beacon and management frames default received by WiFi driver
    filter_config.rx_all_beacon = 1;
    BK_LOG_ON_ERR(bk_wifi_filter_set_config(&filter_config);

    // Only receive all beacon
    filter_config.rx_all_beacon = 1;
    filter_config.rx_all_default_mgmt = 0;
    BK_LOG_ON_ERR(bk_wifi_filter_set_config(&filter_config);
    ```

    **Attention**
    :   1\. If this API is not called, the default filter is to relay all mamangement frames received by WiFi driver to the filter callback.

    **Attention**
    :   2\. If STA is enabled, the WiFi driver only receives beacon from the connected AP, if scan is enabled or filter\_config-\>rx\_all\_beacon is set, the WiFi driver receives beacons of all APs.

    参数
    :   **filter\_config** – configuration of filter

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv425bk_wifi_filter_get_configP20wifi_filter_config_t"></a>

<a id="_CPPv325bk_wifi_filter_get_configP20wifi_filter_config_t"></a> <a id="_CPPv225bk_wifi_filter_get_configP20wifi_filter_config_t"></a> <a id="bk_wifi_filter_get_config__wifi_filter_config_tP"></a> <a id="group__bk__api__wifi__v2_1ga5fc10f022beb010273cdece352634daf"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_filter\_get\_config([wifi\_filter\_config\_t](bk_wifi_types.md#_CPPv420wifi_filter_config_t "wifi_filter_config_t") \*filter\_config)
:   Get the filter configuration.

    参数
    :   **filter\_config** – store configuration of filter

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv426bk_wifi_filter_register_cbK16wifi_filter_cb_t"></a>

<a id="_CPPv326bk_wifi_filter_register_cbK16wifi_filter_cb_t"></a> <a id="_CPPv226bk_wifi_filter_register_cbK16wifi_filter_cb_t"></a> <a id="bk_wifi_filter_register_cb__wifi_filter_cb_tC"></a> <a id="group__bk__api__wifi__v2_1ga0276b4fd054e03c62f79e0b52b1870c0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_filter\_register\_cb(const [wifi\_filter\_cb\_t](bk_wifi_types.md#_CPPv416wifi_filter_cb_t "wifi_filter_cb_t") filter\_cb)
:   Register the filter user callback.

    **Attention**
    :   1\. If the monitor is enabled, the management packets received by filter callback can also be received by monitor callback. If this is not what we want, we can disable filter when enabling monitor, or disable monitor when enabling filter.

    **Attention**
    :   2\. During WiFi scan, the filter also works.

    **Attention**
    :   3\. Pass NULL callback or set all fields of filter\_config to 0 to disable the filter.

    **Attention**
    :   4\. The memory used to hold the frame buffer and frame\_info will be freed immediately when the callback is returned, so don’t relay them to other task. Make a copy of them and then relay to other task if necessary.

    **Attention**
    :   5\. Don’t do too much work in the filter callback because it’s called in WiFi driver core thread, otherwise it may impact the WiFi performance.

    参数
    :   **filter\_cb** – the filter user callback

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv419bk_wifi_sta_get_macP7uint8_t"></a>

<a id="_CPPv319bk_wifi_sta_get_macP7uint8_t"></a> <a id="_CPPv219bk_wifi_sta_get_macP7uint8_t"></a> <a id="bk_wifi_sta_get_mac__uint8_tP"></a> <a id="group__bk__api__wifi__v2_1ga2f4c7d2ddf5b64c341a8afcf67a1c739"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_get\_mac(uint8\_t \*mac)
:   Get the MAC of BK STA.

    **Attention**
    :   1\. The AP’s MAC is derived from the base MAC of the system.

    **Attention**
    :   2\. If you want to change the MAC of AP, call bk\_set\_mac() to set the base MAC of the system.

    参数
    :   **mac** – store the MAC of BK STA

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv418bk_wifi_ap_get_macP7uint8_t"></a>

<a id="_CPPv318bk_wifi_ap_get_macP7uint8_t"></a> <a id="_CPPv218bk_wifi_ap_get_macP7uint8_t"></a> <a id="bk_wifi_ap_get_mac__uint8_tP"></a> <a id="group__bk__api__wifi__v2_1ga10793928908208140565121eca953d90"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_get\_mac(uint8\_t \*mac)
:   Get the MAC of BK AP.

    **Attention**
    :   1\. The AP’s MAC is derived from the base MAC of the system.

    **Attention**
    :   2\. If you want to change the MAC of AP, call bk\_set\_mac() to set the base MAC of the system.

    参数
    :   **mac** – store the MAC of BK AP

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv416bk_wifi_send_rawP7uint8_ti"></a>

<a id="_CPPv316bk_wifi_send_rawP7uint8_ti"></a> <a id="_CPPv216bk_wifi_send_rawP7uint8_ti"></a> <a id="bk_wifi_send_raw__uint8_tP.i"></a> <a id="group__bk__api__wifi__v2_1ga292217fd7679b25131b8c55826d84907"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_send\_raw(uint8\_t \*buffer, int len)
:   Send raw 802.11 frame.

    **Attention**
    :   1\. This API can be used in WiFi station, softap, or monitor mode.

    **Attention**
    :   2\. Only support to send non-QoS frame.

    **Attention**
    :   3\. The frame sequence will be overwritten by WiFi driver.

    **Attention**
    :   4\. The API doesn’t check the correctness of the raw frame, the caller need to guarantee the correctness of the frame.

    参数
    :   - **buffer** – raw 802.11 frame
        - **len** – the length of the 802.11 frame

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv419bk_wifi_send_raw_exP18wifi_raw_tx_info_tPvPv"></a>

<a id="_CPPv319bk_wifi_send_raw_exP18wifi_raw_tx_info_tPvPv"></a> <a id="_CPPv219bk_wifi_send_raw_exP18wifi_raw_tx_info_tPvPv"></a> <a id="bk_wifi_send_raw_ex__wifi_raw_tx_info_tP.voidP.voidP"></a> <a id="group__bk__api__wifi__v2_1ga2bcf71fcfd0f9b74607340f64b657277"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_send\_raw\_ex([wifi\_raw\_tx\_info\_t](bk_wifi_types.md#_CPPv418wifi_raw_tx_info_t "wifi_raw_tx_info_t") \*raw\_tx, void \*cb, void \*param)
:   Send raw 802.11 frame.

    **Attention**
    :   1\. This API can be used in WiFi station, softap, or monitor mode.

    **Attention**
    :   2\. Only support to send non-QoS frame.

    **Attention**
    :   3\. The frame sequence will be overwritten by WiFi driver.

    **Attention**
    :   4\. The API doesn’t check the correctness of the raw frame, the caller need to guarantee the correctness of the frame.

    参数
    :   - **raw\_tx** – raw tx information, refer to struct [wifi\_raw\_tx\_info\_t](bk_wifi_types.md#structwifi__raw__tx__info__t)
        - **cb** – send status call back
        - **param** – send status call back paramter

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv422bk_wifi_send_tx_raw_exP18wifi_raw_tx_info_tPvPv"></a>

<a id="_CPPv322bk_wifi_send_tx_raw_exP18wifi_raw_tx_info_tPvPv"></a> <a id="_CPPv222bk_wifi_send_tx_raw_exP18wifi_raw_tx_info_tPvPv"></a> <a id="bk_wifi_send_tx_raw_ex__wifi_raw_tx_info_tP.voidP.voidP"></a> <a id="group__bk__api__wifi__v2_1ga2e18c3929fb874dd01aa1e850de94bca"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_send\_tx\_raw\_ex([wifi\_raw\_tx\_info\_t](bk_wifi_types.md#_CPPv418wifi_raw_tx_info_t "wifi_raw_tx_info_t") \*raw\_tx, void \*cb, void \*param)
:   Send raw 802.11 tx frame.

    **Attention**
    :   1\. This API can be used in WiFi station, softap, or monitor mode.

    **Attention**
    :   2\. Only support to send non-QoS frame.

    **Attention**
    :   3\. The frame sequence will be overwritten by WiFi driver.

    **Attention**
    :   4\. The API doesn’t check the correctness of the raw frame, the caller need to guarantee the correctness of the frame.

    参数
    :   - **raw\_tx** – raw tx information, refer to struct [wifi\_raw\_tx\_info\_t](bk_wifi_types.md#structwifi__raw__tx__info__t)
        - **cb** – send status call back
        - **param** – send status call back paramter

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv429bk_wifi_set_tx_raw_rate_power8uint32_t8uint32_t"></a>

<a id="_CPPv329bk_wifi_set_tx_raw_rate_power8uint32_t8uint32_t"></a> <a id="_CPPv229bk_wifi_set_tx_raw_rate_power8uint32_t8uint32_t"></a> <a id="bk_wifi_set_tx_raw_rate_power__uint32_t.uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga2650d71604e350578fc8c18fb5ea3d00"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_tx\_raw\_rate\_power(uint32\_t rate, uint32\_t power)
:   Update raw 802.11 frame TX rate and power.

    参数
    :   - **rate** – TX rate control
        - **power** – TX power control

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv421bk_wifi_set_tx_raw_ac7uint8_t"></a>

<a id="_CPPv321bk_wifi_set_tx_raw_ac7uint8_t"></a> <a id="_CPPv221bk_wifi_set_tx_raw_ac7uint8_t"></a> <a id="bk_wifi_set_tx_raw_ac__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga51eb1e9e836d29a1a6726d69037d1faa"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_tx\_raw\_ac(uint8\_t ac)
:   Update raw 802.11 frame TX AC.

    参数
    :   **ac** – TX AC

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv426bk_wifi_set_tx_raw_timeout8uint16_t"></a>

<a id="_CPPv326bk_wifi_set_tx_raw_timeout8uint16_t"></a> <a id="_CPPv226bk_wifi_set_tx_raw_timeout8uint16_t"></a> <a id="bk_wifi_set_tx_raw_timeout__uint16_t"></a> <a id="group__bk__api__wifi__v2_1gac9081dbb8aa6a9d63abaedfd70149b03"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_tx\_raw\_timeout(uint16\_t timeout\_ms)
:   Update raw 802.11 frame TX timeout.

    参数
    :   **timeout\_ms** – TX timeout in ms

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv427bk_wifi_set_wifi_media_modeb"></a>

<a id="_CPPv327bk_wifi_set_wifi_media_modeb"></a> <a id="_CPPv227bk_wifi_set_wifi_media_modeb"></a> <a id="bk_wifi_set_wifi_media_mode__b"></a> <a id="group__bk__api__wifi__v2_1ga9fc185f0df5a7d412408e8c397c076a8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_wifi\_media\_mode(bool flag)
:   Configure wifi multimedia mode when the multimedia is running.

    This API is used to configure multimedia mode of Wi-Fi. Multimedia mode can enchance video fluency and make a better experience of video.

    **Attention**
    :   1\. If you want to running multimedia mode,please configure this flag when open and close multimedia mode.

    **Attention**
    :   2\. Please set this flag before running multimedia and clear this flag after closing multimedia.

    **Attention**
    :   3\. If the flag is set when multimedia is turned on and it is not cleared after multimedia is turned off,the Wi-Fi will not be able to enter ps mode.

    参数
    :   **flag** – set true if you want to enable multimedia mode.

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv434bk_wifi_get_wifi_media_mode_configPb"></a>

<a id="_CPPv334bk_wifi_get_wifi_media_mode_configPb"></a> <a id="_CPPv234bk_wifi_get_wifi_media_mode_configPb"></a> <a id="bk_wifi_get_wifi_media_mode_config__bP"></a> <a id="group__bk__api__wifi__v2_1ga6d0e5d4612540151a95e4fa2feedf33b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_wifi\_media\_mode\_config(bool \*flag)
:   get wifi media mode configuration

    参数
    :   **flag** – store configuration of wifi media mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: the parameter config is NULL
        - others: other errors

<a id="_CPPv425bk_wifi_set_video_quality7uint8_t"></a>

<a id="_CPPv325bk_wifi_set_video_quality7uint8_t"></a> <a id="_CPPv225bk_wifi_set_video_quality7uint8_t"></a> <a id="bk_wifi_set_video_quality__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga6293cddbc6a8c7ad79d708a678c8c22a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_video\_quality(uint8\_t quality)
:   Configure video quality when the video is running.

    This API is used to configure video quality.There are three mode to choose:

    Fluent definition(FD): The video transmission is relatively stable and has strong anti-interference ability,which can ensure the stable video transmission in a complex enviroment;

    Standard definition(SD):The video transmission is stable in a clean environment and is slightly stuck in a complex environment,which transmission bandwidth is improved;

    High definition(HD):The video transmission gives priority to high speed which can transmit high-bandwidth data in a clean environment, but the video transmission is relatively stuck in a complex environment;

    The default value is HD mode when the video is running.

    **Attention**
    :   1\. If you want to running video mode,please configure this parameter when open video mode.

    **Attention**
    :   2\. Please configure this parameter before running video mode.

    **Attention**
    :   3\. Please configure bk\_wifi\_set\_wifi\_media\_mode(flag) before useing this API.

    参数
    :   **quality** – set the video quality when the video is running. Three mode can be choose: 0-FD,1-SD,2-HD,default is HD.

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv432bk_wifi_get_video_quality_configP7uint8_t"></a>

<a id="_CPPv332bk_wifi_get_video_quality_configP7uint8_t"></a> <a id="_CPPv232bk_wifi_get_video_quality_configP7uint8_t"></a> <a id="bk_wifi_get_video_quality_config__uint8_tP"></a> <a id="group__bk__api__wifi__v2_1gaac857413097ced726e8071fed659d6c6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_video\_quality\_config(uint8\_t \*quality)
:   get video quality configuration

    参数
    :   **quality** – store configuration of video quality

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: the parameter config is NULL
        - others: other errors

<a id="_CPPv422bk_wifi_set_default_ac8uint32_t"></a>

<a id="_CPPv322bk_wifi_set_default_ac8uint32_t"></a> <a id="_CPPv222bk_wifi_set_default_ac8uint32_t"></a> <a id="bk_wifi_set_default_ac__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga11967a6b5f2781897003fe24955a4f2e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_default\_ac(uint32\_t ac)
:   Configure defalut AC.

    This API is used to configure default AC,rang in \[0 3\]

    参数
    :   **ac** – set default AC rang in \[0 3\]

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv422bk_wifi_get_default_acP8uint32_t"></a>

<a id="_CPPv322bk_wifi_get_default_acP8uint32_t"></a> <a id="_CPPv222bk_wifi_get_default_acP8uint32_t"></a> <a id="bk_wifi_get_default_ac__uint32_tP"></a> <a id="group__bk__api__wifi__v2_1gaf8341bcaf566a9a50e34c855c6f56023"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_default\_ac(uint32\_t \*ac)
:   get default AC

    参数
    :   **ac** – store default AC

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: the parameter config is NULL
        - others: other errors

<a id="_CPPv421bk_wifi_get_tx_raw_acP7uint8_t"></a>

<a id="_CPPv321bk_wifi_get_tx_raw_acP7uint8_t"></a> <a id="_CPPv221bk_wifi_get_tx_raw_acP7uint8_t"></a> <a id="bk_wifi_get_tx_raw_ac__uint8_tP"></a> <a id="group__bk__api__wifi__v2_1ga4db7515aa0711410116b5acd3b93a4bb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_tx\_raw\_ac(uint8\_t \*ac)
:   get tx raw ac info

    参数
    :   **ac** – ac info

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv426bk_wifi_get_tx_raw_timeoutP8uint16_t"></a>

<a id="_CPPv326bk_wifi_get_tx_raw_timeoutP8uint16_t"></a> <a id="_CPPv226bk_wifi_get_tx_raw_timeoutP8uint16_t"></a> <a id="bk_wifi_get_tx_raw_timeout__uint16_tP"></a> <a id="group__bk__api__wifi__v2_1ga39995099b86b7f16604060ef4627cfb2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_tx\_raw\_timeout(uint16\_t \*time)
:   get tx raw timeout info

    参数
    :   **time** – timeout info

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv423bk_wifi_set_min_rsv_mem8uint16_t"></a>

<a id="_CPPv323bk_wifi_set_min_rsv_mem8uint16_t"></a> <a id="_CPPv223bk_wifi_set_min_rsv_mem8uint16_t"></a> <a id="bk_wifi_set_min_rsv_mem__uint16_t"></a> <a id="group__bk__api__wifi__v2_1ga04358a5590c7c7b3892bbd790ac6f8e1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_min\_rsv\_mem(uint16\_t mem\_bytes)
:   Update the minimux heap memory size that Wi-Fi should reserve.

    **Attention**
    :   1\. An small piece of extra memory will be malloced from heap for each TX packets delivered to Wi-Fi, so if the pending TX packets are too many for some reasons, the heap memory will be occupied too much by TX packets. To ensure the stability of whole system, this interface is provied to limit the memory size for Wi-Fi TX packets.

    **Attention**
    :   2\. The maximum valid value of memory size which could update via this API is 30K bytes

    **Attention**
    :   3\. The default minimux reserved memory size is 10K bytes

    参数
    :   **mem\_bytes** – the expected reserved memory size(bytes)

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv423bk_wifi_get_min_rsv_memP8uint16_t"></a>

<a id="_CPPv323bk_wifi_get_min_rsv_memP8uint16_t"></a> <a id="_CPPv223bk_wifi_get_min_rsv_memP8uint16_t"></a> <a id="bk_wifi_get_min_rsv_mem__uint16_tP"></a> <a id="group__bk__api__wifi__v2_1ga27c6f9387af82c93fdb4d4745567811e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_min\_rsv\_mem(uint16\_t \*mem\_bytes)
:   Get the minimux heap memory size that Wi-Fi currently creserves.

    参数
    :   **mem\_bytes** – return currently reserved memory size(bytes)

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv427bk_wifi_set_tx_max_msdu_cnt8uint16_t"></a>

<a id="_CPPv327bk_wifi_set_tx_max_msdu_cnt8uint16_t"></a> <a id="_CPPv227bk_wifi_set_tx_max_msdu_cnt8uint16_t"></a> <a id="bk_wifi_set_tx_max_msdu_cnt__uint16_t"></a> <a id="group__bk__api__wifi__v2_1ga1f4d92b573cb998c9b7844d5088097a4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_tx\_max\_msdu\_cnt(uint16\_t max\_cnt)
:   Update the maximum MSDU count that Wi-Fi could handle.

    参数
    :   **max\_cnt** – the maxmimum MSDU count

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv427bk_wifi_get_tx_max_msdu_cntP8uint16_t"></a>

<a id="_CPPv327bk_wifi_get_tx_max_msdu_cntP8uint16_t"></a> <a id="_CPPv227bk_wifi_get_tx_max_msdu_cntP8uint16_t"></a> <a id="bk_wifi_get_tx_max_msdu_cnt__uint16_tP"></a> <a id="group__bk__api__wifi__v2_1gae2d2f50c4bb2a7976a2f259450e44d2e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_tx\_max\_msdu\_cnt(uint16\_t \*max\_cnt)
:   Get the maximum MSDU count configuration that Wi-Fi could handle.

    参数
    :   **max\_cnt** – return the maxmimum MSDU count

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv424bk_wifi_set_data_rty_num7uint8_t"></a>

<a id="_CPPv324bk_wifi_set_data_rty_num7uint8_t"></a> <a id="_CPPv224bk_wifi_set_data_rty_num7uint8_t"></a> <a id="bk_wifi_set_data_rty_num__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga774f6bf3b9c4c8714a7aba4a4fdc9662"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_data\_rty\_num(uint8\_t rty\_num)
:   Set data frame retry numbers.

    参数
    :   **rty\_num** – data frame retry numbers

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv424bk_wifi_get_data_rty_numP8uint32_t"></a>

<a id="_CPPv324bk_wifi_get_data_rty_numP8uint32_t"></a> <a id="_CPPv224bk_wifi_get_data_rty_numP8uint32_t"></a> <a id="bk_wifi_get_data_rty_num__uint32_tP"></a> <a id="group__bk__api__wifi__v2_1ga0478c8d841bea3910c511064429c8713"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_data\_rty\_num(uint32\_t \*rty\_num)
:   Get data frame retry numbers.

    参数
    :   **rty\_num** – data frame retry numbers

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv424bk_wifi_set_mgmt_rty_num7uint8_t"></a>

<a id="_CPPv324bk_wifi_set_mgmt_rty_num7uint8_t"></a> <a id="_CPPv224bk_wifi_set_mgmt_rty_num7uint8_t"></a> <a id="bk_wifi_set_mgmt_rty_num__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gaad9a692a885f53de215245cea9e6cd5c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_mgmt\_rty\_num(uint8\_t rty\_num)
:   Set management frame retry numbers.

    参数
    :   **rty\_num** – management frame retry numbers

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv424bk_wifi_get_mgmt_rty_numP8uint32_t"></a>

<a id="_CPPv324bk_wifi_get_mgmt_rty_numP8uint32_t"></a> <a id="_CPPv224bk_wifi_get_mgmt_rty_numP8uint32_t"></a> <a id="bk_wifi_get_mgmt_rty_num__uint32_tP"></a> <a id="group__bk__api__wifi__v2_1gabedf576170e387eeb82636241bfd235c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_mgmt\_rty\_num(uint32\_t \*rty\_num)
:   Get management frame retry numbers.

    参数
    :   **rty\_num** – management frame retry numbers

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv419bk_wifi_capa_config17wifi_capability_t8uint32_t"></a>

<a id="_CPPv319bk_wifi_capa_config17wifi_capability_t8uint32_t"></a> <a id="_CPPv219bk_wifi_capa_config17wifi_capability_t8uint32_t"></a> <a id="bk_wifi_capa_config__wifi_capability_t.uint32_t"></a> <a id="group__bk__api__wifi__v2_1gac844dc0c4b7acd23f5ec8f5f1cc6fa90"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_capa\_config([wifi\_capability\_t](bk_wifi_types.md#_CPPv417wifi_capability_t "wifi_capability_t") capa\_id, uint32\_t capa\_val)
:   Update Wi-Fi capability configuration.

    This API is used to change some Wi-Fi capability configuration, please refer to wifi\_capability\_t to get the capability that has been supported.

    **Attention**
    :   1\. Please keep in mind that Wi-Fi behavior may change if the capability is changed to different value compared with the default value.

    **Attention**
    :   2\. We strongly suggest not using this API except you are very farmiliar with the Wi-Fi specification.

    **Attention**
    :   3\. If you want Wi-Fi working on 11b only mode, please set 11b only mode by configurate paramter capa\_id with WIFI\_CAPA\_ID\_11B\_ONLY\_EN and capa\_val with TRUE.

    参数
    :   - **capa\_id** – the specific capability you want to change
        - **capa\_val** – new capability value

    返回
    :   - BK\_OK: succeed
        - others: other errors

<a id="_CPPv419bk_wifi_set_countryPK14wifi_country_t"></a>

<a id="_CPPv319bk_wifi_set_countryPK14wifi_country_t"></a> <a id="_CPPv219bk_wifi_set_countryPK14wifi_country_t"></a> <a id="bk_wifi_set_country__wifi_country_tCP"></a> <a id="group__bk__api__wifi__v2_1gaa73a4fdaf2ca78ccd0d24c02d94e826f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_country(const [wifi\_country\_t](bk_wifi_types.md#_CPPv414wifi_country_t "wifi_country_t") \*country)
:   configure country info

    **Attention**
    :   1\. The default country is {.cc\=”CN”, .schan\=1, .nchan\=13, policy\=WIFI\_COUNTRY\_POLICY\_AUTO}

    **Attention**
    :   2\. When the country policy is WIFI\_COUNTRY\_POLICY\_AUTO, the country info of the AP to which the station is connected is used. E.g. if the configured country info is {.cc\=”USA”, .schan\=1, .nchan\=11} and the country info of the AP to which the station is connected is {.cc\=”JP”, .schan\=1, .nchan\=14} then the country info that will be used is {.cc\=”JP”, .schan\=1, .nchan\=14}. If the station disconnected from the AP the country info is set back back to the country info of the station automatically, {.cc\=”USA”, .schan\=1, .nchan\=11} in the example.

    **Attention**
    :   3\. When the country policy is WIFI\_COUNTRY\_POLICY\_MANUAL, always use the configured country info.

    **Attention**
    :   4\. When the country info is changed because of configuration or because the station connects to a different external AP, the country IE in probe response/beacon of the soft-AP is changed also.

    **Attention**
    :   5\. The country configuration is not stored into flash

    **Attention**
    :   6\. This API doesn’t validate the per-country rules, it’s up to the user to fill in all fields according to local regulations.

    参数
    :   **country** – the configured country info

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_WIFI\_NOT\_INIT: WiFi is not initialized
        - BK\_ERR\_PARAM: invalid argument

<a id="_CPPv419bk_wifi_get_countryP14wifi_country_t"></a>

<a id="_CPPv319bk_wifi_get_countryP14wifi_country_t"></a> <a id="_CPPv219bk_wifi_get_countryP14wifi_country_t"></a> <a id="bk_wifi_get_country__wifi_country_tP"></a> <a id="group__bk__api__wifi__v2_1gac7d81cf7284a781dc89f32a34bdbd19b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_country([wifi\_country\_t](bk_wifi_types.md#_CPPv414wifi_country_t "wifi_country_t") \*country)
:   get the current country info

    参数
    :   **country** – country info

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_WIFI\_NOT\_INIT: WiFi is not initialized
        - BK\_ERR\_PARAM: invalid argument

<a id="_CPPv421bk_wifi_sta_pm_enablev"></a>

<a id="_CPPv321bk_wifi_sta_pm_enablev"></a> <a id="_CPPv221bk_wifi_sta_pm_enablev"></a> <a id="bk_wifi_sta_pm_enable__void"></a> <a id="group__bk__api__wifi__v2_1gad4c99153083a4794817f4d94bb373511"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_pm\_enable(void)
:   enable wifi sta power management

    返回
    :   - BK\_OK: on succeed
        - others: real error, used for future.

<a id="_CPPv422bk_wifi_sta_pm_disablev"></a>

<a id="_CPPv322bk_wifi_sta_pm_disablev"></a> <a id="_CPPv222bk_wifi_sta_pm_disablev"></a> <a id="bk_wifi_sta_pm_disable__void"></a> <a id="group__bk__api__wifi__v2_1gace062a914995e24ed92af5627e10410a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_sta\_pm\_disable(void)
:   disable wifi sta power management

    返回
    :   - BK\_OK: on succeed
        - others: real error, used for future.

<a id="_CPPv419bk_wifi_get_channelv"></a>

<a id="_CPPv319bk_wifi_get_channelv"></a> <a id="_CPPv219bk_wifi_get_channelv"></a> <a id="bk_wifi_get_channel__void"></a> <a id="group__bk__api__wifi__v2_1ga78cd0fd3138dd36fb20c862ea33d4712"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_channel(void)
:   get current channel ID

    参数
    :   **basically** – range from 1\~13

    返回
    :   - BK\_OK: on succeed
        - others: real error, used for future.

<a id="_CPPv423bk_wifi_set_mac_addressPc"></a>

<a id="_CPPv323bk_wifi_set_mac_addressPc"></a> <a id="_CPPv223bk_wifi_set_mac_addressPc"></a> <a id="bk_wifi_set_mac_address__cP"></a> <a id="group__bk__api__wifi__v2_1gac6612c64c6284a344100b43ba4e9997f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_mac\_address(char \*mac)
:   Set Wi-Fi MAC addresses.

    The given MAC address will become the station MAC address.The AP MAC address (i.e BSSID) will be the same MAC address but with the local bit set.

    @usage example: mac c8478cxxyyzz txevm -e 2 //if needed

    备注

    on some platforms the change of MAC address can only take effect after reboot.

    参数
    :   **mac** – system mac

    返回
    :   ```
        - BK_OK: on succeed
         - others: real error, used for future.
        ```

<a id="_CPPv432bk_wifi_manual_cal_rfcali_statusv"></a>

<a id="_CPPv332bk_wifi_manual_cal_rfcali_statusv"></a> <a id="_CPPv232bk_wifi_manual_cal_rfcali_statusv"></a> <a id="bk_wifi_manual_cal_rfcali_status__void"></a> <a id="group__bk__api__wifi__v2_1gad0f9f4f5e6294e7c3e55c95f209d30d8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_manual\_cal\_rfcali\_status(void)
:   Get Wi-Fi Calibration status.

    返回
    :   - BK\_OK: on succeed
        - others: real error, used for future.

<a id="_CPPv442bk_wifi_ap_vif_probe_req_frame_cb_registerPv"></a>

<a id="_CPPv342bk_wifi_ap_vif_probe_req_frame_cb_registerPv"></a> <a id="_CPPv242bk_wifi_ap_vif_probe_req_frame_cb_registerPv"></a> <a id="bk_wifi_ap_vif_probe_req_frame_cb_register__voidP"></a> <a id="group__bk__api__wifi__v2_1ga27ed944101f44ef722ad441bbf793a5c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ap\_vif\_probe\_req\_frame\_cb\_register(void \*cb)
:   Register a cb of probe request for ap.

    参数
    :   **cb** – callback function of probe request to register

<a id="_CPPv432bk_wifi_send_listen_interval_req7uint8_t"></a>

<a id="_CPPv332bk_wifi_send_listen_interval_req7uint8_t"></a> <a id="_CPPv232bk_wifi_send_listen_interval_req7uint8_t"></a> <a id="bk_wifi_send_listen_interval_req__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gab85e92fdd41b151d1e99e3cd784e380f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_send\_listen\_interval\_req(uint8\_t interval)
:   Set listen interval.

    参数
    :   **any** – value is acceptable,but 1, 3, 10 is recommended.

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv427bk_wifi_get_listen_intervalP7uint8_t"></a>

<a id="_CPPv327bk_wifi_get_listen_intervalP7uint8_t"></a> <a id="_CPPv227bk_wifi_get_listen_intervalP7uint8_t"></a> <a id="bk_wifi_get_listen_interval__uint8_tP"></a> <a id="group__bk__api__wifi__v2_1ga2f3319ed4dd92eb1220934e30154d193"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_listen\_interval(uint8\_t \*listen\_interval)
:   Get listen interval.

    参数
    :   **return** – the configure listen interval

    返回
    :   -0: not set listen interval -others:return the configure listen interval value.

<a id="_CPPv429bk_wifi_send_arp_set_rate_req8uint16_t"></a>

<a id="_CPPv329bk_wifi_send_arp_set_rate_req8uint16_t"></a> <a id="_CPPv229bk_wifi_send_arp_set_rate_req8uint16_t"></a> <a id="bk_wifi_send_arp_set_rate_req__uint16_t"></a> <a id="group__bk__api__wifi__v2_1ga9ea1a5f451da1e093f0ff1e99000b0c6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_send\_arp\_set\_rate\_req(uint16\_t arp\_tx\_rate)
:   Set arp tx rate.

    参数
    :   **any** – value is acceptable,but 1, 6 is recommended.

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv429bk_wifi_send_bcn_loss_int_req7uint8_t7uint8_t"></a>

<a id="_CPPv329bk_wifi_send_bcn_loss_int_req7uint8_t7uint8_t"></a> <a id="_CPPv229bk_wifi_send_bcn_loss_int_req7uint8_t7uint8_t"></a> <a id="bk_wifi_send_bcn_loss_int_req__uint8_t.uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga9914fd1de54614e3f152b1d2415cb435"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_send\_bcn\_loss\_int\_req(uint8\_t interval, uint8\_t repeat\_num)
:   When beacon loss occurs,use beacon loss interval.

    参数
    :   - **interval** – any value is acceptable,it is recommended that this value less than listen interval
        - **repeat\_num** – set beacon loss interval number,the minimum value is 1

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv425bk_wifi_set_bcn_loss_time7uint8_t7uint8_t"></a>

<a id="_CPPv325bk_wifi_set_bcn_loss_time7uint8_t7uint8_t"></a> <a id="_CPPv225bk_wifi_set_bcn_loss_time7uint8_t7uint8_t"></a> <a id="bk_wifi_set_bcn_loss_time__uint8_t.uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga7bab2dc03a6d323612808f461fc3f3de"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_bcn\_loss\_time(uint8\_t wait\_cnt, uint8\_t wake\_cnt)
:   When beacon loss occurs,use bcn loss time.

    @usage example:(10s no beacon frame received(normal reception for the first 5s,ps off for the next 5s),disconnect from the router) DTIM10:wait\_cnt \= 5,wake\_cnt \= 50 DTIM1 :wait\_cnt \= 50,wake\_cnt \= 50

    参数
    :   - **wait\_cnt** – failed to receive beacon for wait\_cnt consecutive cycles, close ps,wait\_cnt corresponds to dtimx(listen\_interval)
        - **wake\_cnt** – after ps is turned off,the beacon fails to receive for wake\_cnt consecutive cycles, disconnect;wake\_cnt corresponds to dtim1

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv425bk_wifi_set_bcn_miss_time7uint8_t"></a>

<a id="_CPPv325bk_wifi_set_bcn_miss_time7uint8_t"></a> <a id="_CPPv225bk_wifi_set_bcn_miss_time7uint8_t"></a> <a id="bk_wifi_set_bcn_miss_time__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga7d593c4da831aa9614dfc014588bf766"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_bcn\_miss\_time(uint8\_t bcnmiss\_time)
:   configure beacon miss time.

    bcnmiss\_time: bcnmiss\_time not receive the beacon,disconnected from the router;unit: second

    @usage example:(30s no beacon frame received,disconnect from the router) bcnmiss\_time:30

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv424bk_wifi_set_bcn_recv_win7uint8_t7uint8_t7uint8_t"></a>

<a id="_CPPv324bk_wifi_set_bcn_recv_win7uint8_t7uint8_t7uint8_t"></a> <a id="_CPPv224bk_wifi_set_bcn_recv_win7uint8_t7uint8_t7uint8_t"></a> <a id="bk_wifi_set_bcn_recv_win__uint8_t.uint8_t.uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga93de8247d9cc2de8d9541360253686e6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_bcn\_recv\_win(uint8\_t default\_win, uint8\_t max\_win, uint8\_t step)
:   set beacon receive window.

    参数
    :   - **default\_win** – default beacon receive window(ms),minimum is 5,less than or equal to max\_win.
        - **max\_win** – max beacon receive window(ms),maximum is 20\.
        - **step** – increase the beacon reception time by a step value(ms)

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv431bk_wifi_bcn_cc_rxed_register_cbK21wifi_beacon_cc_rxed_tPv"></a>

<a id="_CPPv331bk_wifi_bcn_cc_rxed_register_cbK21wifi_beacon_cc_rxed_tPv"></a> <a id="_CPPv231bk_wifi_bcn_cc_rxed_register_cbK21wifi_beacon_cc_rxed_tPv"></a> <a id="bk_wifi_bcn_cc_rxed_register_cb__wifi_beacon_cc_rxed_tC.voidP"></a> <a id="group__bk__api__wifi__v2_1ga126e549848120c764fa77ac30ddee050"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_bcn\_cc\_rxed\_register\_cb(const [wifi\_beacon\_cc\_rxed\_t](bk_wifi_types.md#_CPPv421wifi_beacon_cc_rxed_t "wifi_beacon_cc_rxed_t") cc\_cb, void \*ctxt)
:   regist bcn cc rxed callback.

    参数
    :   **bcn** – cc the callback function.

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv413cc_scan_startv"></a>

<a id="_CPPv313cc_scan_startv"></a> <a id="_CPPv213cc_scan_startv"></a> <a id="cc_scan_start__void"></a> <a id="group__bk__api__wifi__v2_1gab4713d825f06b4a15840b41754381f71"></a> int cc\_scan\_start(void)
:   start scan procedure to find AP’s country code

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv412cc_scan_stopv"></a>

<a id="_CPPv312cc_scan_stopv"></a> <a id="_CPPv212cc_scan_stopv"></a> <a id="cc_scan_stop__void"></a> <a id="group__bk__api__wifi__v2_1gac48b18ba13d0a795978a8d71100429e0"></a> void cc\_scan\_stop(void)
:   stop scan procedure to find AP’s country code

    返回
    :   success

<a id="_CPPv420bk_scan_country_codeP7uint8_tPi"></a>

<a id="_CPPv320bk_scan_country_codeP7uint8_tPi"></a> <a id="_CPPv220bk_scan_country_codeP7uint8_tPi"></a> <a id="bk_scan_country_code__uint8_tP.iP"></a> <a id="group__bk__api__wifi__v2_1ga0311a1e4b4f6958db5c5b1fc44ef1f1d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_scan\_country\_code(uint8\_t \*country\_code, int \*len)
:   Get country code by scan.

    **Attention**
    :   Need open CONFIG\_WIFI\_SCAN\_COUNTRY\_CODE\=y in config

    参数
    :   - **country\_code** – The point of country code buffer
        - **len** – The length of the point of country code buffer

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv429bk_wifi_get_support_wifi_modeP7uint8_t"></a>

<a id="_CPPv329bk_wifi_get_support_wifi_modeP7uint8_t"></a> <a id="_CPPv229bk_wifi_get_support_wifi_modeP7uint8_t"></a> <a id="bk_wifi_get_support_wifi_mode__uint8_tP"></a> <a id="group__bk__api__wifi__v2_1ga823977c99fd408ec06fcfd33e3fff41a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_support\_wifi\_mode(uint8\_t \*support\_mode)
:   Get wifi support mode.

    参数
    :   **get** – wifi support info

    返回
    :   -2: support wifi6(HE) -1: support wifi4(HT) -0: support others(11n/g)

<a id="_CPPv426bk_wifi_get_statistic_infoP22wifi_statistics_info_t"></a>

<a id="_CPPv326bk_wifi_get_statistic_infoP22wifi_statistics_info_t"></a> <a id="_CPPv226bk_wifi_get_statistic_infoP22wifi_statistics_info_t"></a> <a id="bk_wifi_get_statistic_info__wifi_statistics_info_tP"></a> <a id="group__bk__api__wifi__v2_1gae7f7f32858ec93b741b6682d60eaddf9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_statistic\_info([wifi\_statistics\_info\_t](bk_wifi_types.md#_CPPv422wifi_statistics_info_t "wifi_statistics_info_t") \*wifiinfo)
:   Get wifi statistic info.

    参数
    :   **get** – wifi info from fw

    返回
    :   -BK\_OK: on success -others:real error, used for future.

<a id="_CPPv416bk_wifi_ota_dtimb"></a>

<a id="_CPPv316bk_wifi_ota_dtimb"></a> <a id="_CPPv216bk_wifi_ota_dtimb"></a> <a id="bk_wifi_ota_dtim__b"></a> <a id="group__bk__api__wifi__v2_1ga8c1255c2ce751393f9304c154bc75c40"></a> void bk\_wifi\_ota\_dtim(bool is\_open)
:   set wifi ps dtim info.

    参数
    :   **dtim** – 1 open or not

    返回
    :   -void.

<a id="_CPPv429bk_wifi_set_td_active_percent7uint8_t"></a>

<a id="_CPPv329bk_wifi_set_td_active_percent7uint8_t"></a> <a id="_CPPv229bk_wifi_set_td_active_percent7uint8_t"></a> <a id="bk_wifi_set_td_active_percent__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga10e352311d7fe5aadcc701add20ff41a"></a> void bk\_wifi\_set\_td\_active\_percent(uint8\_t active\_percent)
:   Set active\_percent.

    参数
    :   **{10ms-100ms}** – \*

    返回
    :   -void.

<a id="_CPPv430bk_wifi_mask_td_active_percentv"></a>

<a id="_CPPv330bk_wifi_mask_td_active_percentv"></a> <a id="_CPPv230bk_wifi_mask_td_active_percentv"></a> <a id="bk_wifi_mask_td_active_percent"></a> <a id="group__bk__api__wifi__v2_1ga1bd2739d41e9d1f4ec31276d190bec18"></a> void bk\_wifi\_mask\_td\_active\_percent()
:   mask active\_percent

    参数
    :   **\*** –

<a id="_CPPv428bk_wifi_ap_power_register_cb15FUNC_1PARAM_PTR"></a>

<a id="_CPPv328bk_wifi_ap_power_register_cb15FUNC_1PARAM_PTR"></a> <a id="_CPPv228bk_wifi_ap_power_register_cb15FUNC_1PARAM_PTR"></a> <a id="bk_wifi_ap_power_register_cb__FUNC_1PARAM_PTR"></a> <a id="group__bk__api__wifi__v2_1ga89517c629e44da48ffb89bdb21b73e38"></a> void bk\_wifi\_ap\_power\_register\_cb(FUNC\_1PARAM\_PTR cb)
:   register callback to get wifi ap power

    参数
    :   **callback** – interface \*

    返回
    :   -void.

<a id="_CPPv420bk_wlan_phy_open_ccav"></a>

<a id="_CPPv320bk_wlan_phy_open_ccav"></a> <a id="_CPPv220bk_wlan_phy_open_ccav"></a> <a id="bk_wlan_phy_open_cca__void"></a> <a id="group__bk__api__wifi__v2_1gab6111ca87fea32f862d4024b76e110a1"></a> void bk\_wlan\_phy\_open\_cca(void)

<a id="_CPPv421bk_wlan_phy_close_ccav"></a>

<a id="_CPPv321bk_wlan_phy_close_ccav"></a> <a id="_CPPv221bk_wlan_phy_close_ccav"></a> <a id="bk_wlan_phy_close_cca__void"></a> <a id="group__bk__api__wifi__v2_1ga897c1faa280f7ee71d0694b2a0aa9c73"></a> void bk\_wlan\_phy\_close\_cca(void)

<a id="_CPPv420bk_wlan_phy_show_ccav"></a>

<a id="_CPPv320bk_wlan_phy_show_ccav"></a> <a id="_CPPv220bk_wlan_phy_show_ccav"></a> <a id="bk_wlan_phy_show_cca__void"></a> <a id="group__bk__api__wifi__v2_1ga4d35cbf7a16c2baed5a0221c1da9b2a2"></a> void bk\_wlan\_phy\_show\_cca(void)

<a id="_CPPv417bk_wifi_ftm_startPK17wifi_ftm_config_tP18wifi_ftm_results_t"></a>

<a id="_CPPv317bk_wifi_ftm_startPK17wifi_ftm_config_tP18wifi_ftm_results_t"></a> <a id="_CPPv217bk_wifi_ftm_startPK17wifi_ftm_config_tP18wifi_ftm_results_t"></a> <a id="bk_wifi_ftm_start__wifi_ftm_config_tCP.wifi_ftm_results_tP"></a> <a id="group__bk__api__wifi__v2_1ga26fdfeaa0ffcbf1ffc0562f7eb0d78dd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ftm\_start(const [wifi\_ftm\_config\_t](bk_wifi_types.md#_CPPv417wifi_ftm_config_t "wifi_ftm_config_t") \*config, [wifi\_ftm\_results\_t](bk_wifi_types.md#_CPPv418wifi_ftm_results_t "wifi_ftm_results_t") \*ftm\_results)
:   Start a fine timing measurement (FTM)

    This API notifies the WiFi driver to start a fine timing measurement, and get the ftm results.

    参数
    :   - **config** – the configuration of ftm
        - **ftm\_results** – the results of ftm

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_WIFI\_NOT\_INIT: WiFi is not initialized
        - BK\_ERR\_WIFI\_STA\_NOT\_STARTED: the STA is not started, call [bk\_wifi\_sta\_start()](#group__bk__api__wifi__v2_1gaaf144e78b9438143e21f7c75e8c23ecf) first.
        - BK\_ERR\_WIFI\_DRIVER: WiFi low level driver has failure.
        - others: other failures.

<a id="_CPPv423bk_wifi_ftm_dump_resultPK18wifi_ftm_results_t"></a>

<a id="_CPPv323bk_wifi_ftm_dump_resultPK18wifi_ftm_results_t"></a> <a id="_CPPv223bk_wifi_ftm_dump_resultPK18wifi_ftm_results_t"></a> <a id="bk_wifi_ftm_dump_result__wifi_ftm_results_tCP"></a> <a id="group__bk__api__wifi__v2_1gac6f6ae11c304a848c79aba4d207c9702"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ftm\_dump\_result(const [wifi\_ftm\_results\_t](bk_wifi_types.md#_CPPv418wifi_ftm_results_t "wifi_ftm_results_t") \*ftm\_results)
:   Dump the ftm results.

    **Attention**
    :   call [bk\_wifi\_ftm\_start()](#group__bk__api__wifi__v2_1ga26fdfeaa0ffcbf1ffc0562f7eb0d78dd) first before call bk\_wifi\_ftm\_dump\_result.

    参数
    :   **ftm\_results** – The ftm result to be dumped.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PARAM: invalid scan result

<a id="_CPPv423bk_wifi_ftm_free_resultP18wifi_ftm_results_t"></a>

<a id="_CPPv323bk_wifi_ftm_free_resultP18wifi_ftm_results_t"></a> <a id="_CPPv223bk_wifi_ftm_free_resultP18wifi_ftm_results_t"></a> <a id="bk_wifi_ftm_free_result__wifi_ftm_results_tP"></a> <a id="group__bk__api__wifi__v2_1ga6d86fbebd9ff741ff8205be895e95663"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_ftm\_free\_result([wifi\_ftm\_results\_t](bk_wifi_types.md#_CPPv418wifi_ftm_results_t "wifi_ftm_results_t") \*ftm\_results)
:   Free the ftm result.

    **Attention**
    :   This API free ftm\_results-\>rsp which allocated in [bk\_wifi\_ftm\_start()](#group__bk__api__wifi__v2_1ga26fdfeaa0ffcbf1ffc0562f7eb0d78dd), it doesn’t free ftm\_results. So if ftm\_results is allocated by the caller, the caller need to free it.

    参数
    :   **ftm\_results** – The ftm result to be freed.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PARAM: invalid scan result

<a id="_CPPv427bk_wifi_set_pkt_trx_dbg_cfg8uint32_t"></a>

<a id="_CPPv327bk_wifi_set_pkt_trx_dbg_cfg8uint32_t"></a> <a id="_CPPv227bk_wifi_set_pkt_trx_dbg_cfg8uint32_t"></a> <a id="bk_wifi_set_pkt_trx_dbg_cfg__uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga07613ff50b3e5a1f06c6cf76d4c3305b"></a> void bk\_wifi\_set\_pkt\_trx\_dbg\_cfg(uint32\_t cfg\_bit)
:   Set Wi-Fi TX/RX debug log configuration.

    This API could enable the TX/RX debug log by setting the corresponding debug bit.

    **Attention**
    :   This API is only used for DEBUG Wi-Fi issues according to frame TX/RX, there will be a lot of logs generated after set debug bit and it will have affect on the performance. To capture the whole logs, you should increase the buadrate of UART.

    参数
    :   **cfg\_bit** – Please refer to enum wifi\_pkt\_dbg\_bit to get more detail.

    返回
    :   - void: always succeed

<a id="_CPPv422bk_wifi_set_ap_channel7uint8_t"></a>

<a id="_CPPv322bk_wifi_set_ap_channel7uint8_t"></a> <a id="_CPPv222bk_wifi_set_ap_channel7uint8_t"></a> <a id="bk_wifi_set_ap_channel__uint8_t"></a> <a id="group__bk__api__wifi__v2_1ga9044bebaf80a55765ce6f0df9b92a8a6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_ap\_channel(uint8\_t channel)
:   Set Wi-Fi Softap Channel.

    This API could be used to change softap operation channel.

    @channel The valid channel ID should range from 1-14.

    **Attention**
    :   This API can only be used when softap is enabled and make sure the internal CSA strategy is disabled by calling API bk\_feature\_close\_coexist\_csa.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PARAM: invalid channel ID

<a id="_CPPv422bk_wifi_set_ap_csa_cnt7uint8_t"></a>

<a id="_CPPv322bk_wifi_set_ap_csa_cnt7uint8_t"></a> <a id="_CPPv222bk_wifi_set_ap_csa_cnt7uint8_t"></a> <a id="bk_wifi_set_ap_csa_cnt__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gafe5afbb18727aef29bc0d5288b6bbf36"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_ap\_csa\_cnt(uint8\_t csa\_cnt)
:   Set Wi-Fi Softap CSA Count.

    This API could be used to change softap operation channel.

    @csa\_cnt The valid csa count should range from 0-255.

    **Attention**
    :   This API can only be used when softap is enabled and make sure the internal CSA strategy is disabled by calling API bk\_feature\_close\_coexist\_csa.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PARAM: invalid csa count

<a id="_CPPv427bk_wifi_set_ap_channel_stopv"></a>

<a id="_CPPv327bk_wifi_set_ap_channel_stopv"></a> <a id="_CPPv227bk_wifi_set_ap_channel_stopv"></a> <a id="bk_wifi_set_ap_channel_stop__void"></a> <a id="group__bk__api__wifi__v2_1gaf91efcb57005f0562ba96a57230bae62"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_ap\_channel\_stop(void)
:   Stop Wi-Fi Softap Channel Switch.

    This API could be used to stop softap operation channel.

    **Attention**
    :   This API can only be used when softap is enabled.

    返回
    :   - void: always succeed

<a id="_CPPv425bk_wifi_set_block_bcmc_en7uint8_t"></a>

<a id="_CPPv325bk_wifi_set_block_bcmc_en7uint8_t"></a> <a id="_CPPv225bk_wifi_set_block_bcmc_en7uint8_t"></a> <a id="bk_wifi_set_block_bcmc_en__uint8_t"></a> <a id="group__bk__api__wifi__v2_1gabd0ee4a405311a19356f68b40975316d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_block\_bcmc\_en(uint8\_t config)
:   Enable Wi-Fi rx block broadcast and multicast frame.

    This API could enable Wi-Fi rx block broadcast and multicast frame.

    参数
    :   **config** – block type. 0:WIFI\_BCMC\_CLOSE 1:WIFI\_MC\_ON, 2:WIFI\_BC\_ON, 3:WIFI\_BC\_MC\_ON,

    返回
    :   - void: always succeed

<a id="_CPPv425bk_wifi_get_block_bcmc_env"></a>

<a id="_CPPv325bk_wifi_get_block_bcmc_env"></a> <a id="_CPPv225bk_wifi_get_block_bcmc_env"></a> <a id="bk_wifi_get_block_bcmc_en__void"></a> <a id="group__bk__api__wifi__v2_1ga5235feedd63bb0e0391f5af9d7b9b839"></a> bool bk\_wifi\_get\_block\_bcmc\_en(void)
:   Get Wi-Fi rx block broadcast and multicast frame status.

    参数
    :   **void.** –

    返回
    :   - enable status

<a id="_CPPv418bk_wifi_set_ani_enb"></a>

<a id="_CPPv318bk_wifi_set_ani_enb"></a> <a id="_CPPv218bk_wifi_set_ani_enb"></a> <a id="bk_wifi_set_ani_en__b"></a> <a id="group__bk__api__wifi__v2_1gae1f1484a628bd37ae8f2a5136e68edfc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_ani\_en(bool enable)
:   Enable Wi-Fi microwave anti-interference policy.

    This API could enable Wi-Fi microwave anti-interference policy.

    参数
    :   **enable.** –

    返回
    :   - void: always succeed

<a id="_CPPv418bk_wifi_get_ani_env"></a>

<a id="_CPPv318bk_wifi_get_ani_env"></a> <a id="_CPPv218bk_wifi_get_ani_env"></a> <a id="bk_wifi_get_ani_en__void"></a> <a id="group__bk__api__wifi__v2_1ga81a0150bfb641fece6e8504beca5e30c"></a> bool bk\_wifi\_get\_ani\_en(void)
:   Get Wi-Fi microwave anti-interference policy enable status.

    参数
    :   **void.** –

    返回
    :   - enable status

<a id="_CPPv421bk_wifi_set_pwr_limitP17wifi_tx_pwr_lmt_t"></a>

<a id="_CPPv321bk_wifi_set_pwr_limitP17wifi_tx_pwr_lmt_t"></a> <a id="_CPPv221bk_wifi_set_pwr_limitP17wifi_tx_pwr_lmt_t"></a> <a id="bk_wifi_set_pwr_limit__wifi_tx_pwr_lmt_tP"></a> <a id="group__bk__api__wifi__v2_1gaff17d87c8ede896a47db7b7b4081212a"></a> int bk\_wifi\_set\_pwr\_limit([wifi\_tx\_pwr\_lmt\_t](bk_wifi_types.md#_CPPv417wifi_tx_pwr_lmt_t "wifi_tx_pwr_lmt_t") \*tx\_pwr\_lmt)
:   Set Wi-Fi Power Limit.

    This API could be used to change max tx power with regulation,ratesection and channel .

    **Attention**
    :   This API can only be used to modify rf max power limit for specific regulation,rate and channel.

    参数
    :   **tx\_pwr\_lmt** – wifi tx power limit info

    返回
    :   - void: always succeed

<a id="_CPPv418bk_wifi_get_cal_2gv"></a>

<a id="_CPPv318bk_wifi_get_cal_2gv"></a> <a id="_CPPv218bk_wifi_get_cal_2gv"></a> <a id="bk_wifi_get_cal_2g__void"></a> <a id="group__bk__api__wifi__v2_1ga10f18a3b00754d6229d68526c88f1fc1"></a> bool bk\_wifi\_get\_cal\_2g(void)
:   Get rf cal 2g information.

    This API could be used to check rf 2g calibration .

    返回
    :   - true:if rf 2g is calibrated, false: if rf 2g is not calibrated

<a id="_CPPv423bk_wifi_get_noise_floorP7uint8_t"></a>

<a id="_CPPv323bk_wifi_get_noise_floorP7uint8_t"></a> <a id="_CPPv223bk_wifi_get_noise_floorP7uint8_t"></a> <a id="bk_wifi_get_noise_floor__uint8_tP"></a> <a id="group__bk__api__wifi__v2_1gab268706b0f12487acba297e4e77f45d1"></a> void bk\_wifi\_get\_noise\_floor(uint8\_t \*noise\_floor)
:   Get noise floor.

    参数
    :   **noise\_floor** – store noise floor

    返回
    :   - void: always succeed

<a id="_CPPv420bk_wifi_get_tx_stats7uint8_tP10tx_stats_t"></a>

<a id="_CPPv320bk_wifi_get_tx_stats7uint8_tP10tx_stats_t"></a> <a id="_CPPv220bk_wifi_get_tx_stats7uint8_tP10tx_stats_t"></a> <a id="bk_wifi_get_tx_stats__uint8_t.tx_stats_tP"></a> <a id="group__bk__api__wifi__v2_1ga61deab95ef0153858c76c5fe65e383ef"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_tx\_stats(uint8\_t mode, struct [tx\_stats\_t](bk_wifi_types.md#_CPPv410tx_stats_t "tx_stats_t") \*tx\_stats)
:   Get tx stats.

    ```
        PER calculation formula:  per = (tx_agg_fail + tx_singel_retry)/(tx_agg_total + tx_singel_total*SINGLE_RETRY_CNT)
        - tx_agg_fail/tx_singel_retry/tx_agg_total/tx_singel_total: get from struct tx_stats,
        - SINGLE_RETRY_CNT: get from function bk_wifi_get_data_rty_num();
    ```

    参数
    :   **config** – mode. 0:STATION 1:SOFT AP

    返回
    :   - tx\_stats:tx statistics

<a id="_CPPv420bk_wifi_get_tx_power13wifi_standardPf"></a>

<a id="_CPPv320bk_wifi_get_tx_power13wifi_standardPf"></a> <a id="_CPPv220bk_wifi_get_tx_power13wifi_standardPf"></a> <a id="bk_wifi_get_tx_power__wifi_standard.floatP"></a> <a id="group__bk__api__wifi__v2_1gaf3d87a567db82eb0c071f82969e0e243"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_get\_tx\_power([wifi\_standard](bk_wifi_types.md#_CPPv413wifi_standard "wifi_standard") standard, float \*powerdBm)
:   Fetch 802.11 TX power by standards.

    参数
    :   - **standard** – IEEE 80211 standard
        - **power** – TX power in dBm

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv420bk_wifi_set_tx_power13wifi_standardf"></a>

<a id="_CPPv320bk_wifi_set_tx_power13wifi_standardf"></a> <a id="_CPPv220bk_wifi_set_tx_power13wifi_standardf"></a> <a id="bk_wifi_set_tx_power__wifi_standard.float"></a> <a id="group__bk__api__wifi__v2_1ga916cce8f8adcc43ea8cbdad5a04b1713"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_set\_tx\_power([wifi\_standard](bk_wifi_types.md#_CPPv413wifi_standard "wifi_standard") standard, float powerdBm)
:   Update 802.11 TX power by standards.

    参数
    :   - **standard** – IEEE 80211 standard
        - **power** – TX power in dBm

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv428bk_wifi_csi_info_cb_register13wifi_csi_cb_t"></a>

<a id="_CPPv328bk_wifi_csi_info_cb_register13wifi_csi_cb_t"></a> <a id="_CPPv228bk_wifi_csi_info_cb_register13wifi_csi_cb_t"></a> <a id="bk_wifi_csi_info_cb_register__wifi_csi_cb_t"></a> <a id="group__bk__api__wifi__v2_1ga0c3296bc8af3b29d92e425024917f523"></a> void bk\_wifi\_csi\_info\_cb\_register([wifi\_csi\_cb\_t](bk_wifi_types.md#_CPPv413wifi_csi_cb_t "wifi_csi_cb_t") cb)
:   user get csi data function

    **Attention**
    :   . the processing flow in this function should be as short as possible

    参数
    :   **cb** – user register callback function to get csi data

<a id="_CPPv422bk_wifi_csi_alg_configd"></a>

<a id="_CPPv322bk_wifi_csi_alg_configd"></a> <a id="_CPPv222bk_wifi_csi_alg_configd"></a> <a id="bk_wifi_csi_alg_config__double"></a> <a id="group__bk__api__wifi__v2_1ga5eefc3d0ed8b94b2067718c1a3879bfc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_csi\_alg\_config(double thres1)
:   config csi algorithm param

    参数
    :   **thres1** – detection sensitivity(default 5),the larger the value,the less sensitive it is for motion detection. , set range \>\=3

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv421bk_wifi_csi_start_req7uint8_t7uint8_t7uint8_t7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv321bk_wifi_csi_start_req7uint8_t7uint8_t7uint8_t7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv221bk_wifi_csi_start_req7uint8_t7uint8_t7uint8_t7uint8_t8uint32_t8uint32_t"></a> <a id="bk_wifi_csi_start_req__uint8_t.uint8_t.uint8_t.uint8_t.uint32_t.uint32_t"></a> <a id="group__bk__api__wifi__v2_1ga2852d066301e12c93a39f9f3333c1856"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_csi\_start\_req(uint8\_t csi\_work\_type, uint8\_t csi\_work\_mode, uint8\_t csi\_work\_identity, uint8\_t csi\_data\_format, uint32\_t csi\_data\_interval, uint32\_t delay)
:   start csi

    参数
    :   - **csi\_work\_type** – work type. 0: single mode group method, 1: dual mode group method
        - **csi\_work\_mode** – bit 100 \&#8212; algorithm; bit 1000 \&#8212; csi abs
        - **csi\_work\_identity** – bit 01\&#8212; support STA csi; bit 10 \&#8212; support AP csi
        - **csi\_data\_format** – frame format : NON\_HT 0x01;HT\_MM 0x02;HE\_SU 0x04(now algorithm only support NON\_HT)
        - **csi\_data\_interval** – csi data get interval(ms), set range \>\=10
        - **delay** – delay time for getting csi data(s), set range 0\~4000

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv420bk_wifi_csi_stop_reqv"></a>

<a id="_CPPv320bk_wifi_csi_stop_reqv"></a> <a id="_CPPv220bk_wifi_csi_stop_reqv"></a> <a id="bk_wifi_csi_stop_req__void"></a> <a id="group__bk__api__wifi__v2_1gadde0a34a609227ae3c85de3f007d5c5a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_csi\_stop\_req(void)
:   stop csi

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv434bk_wifi_csi_static_param_reset_req7uint8_t8uint32_t"></a>

<a id="_CPPv334bk_wifi_csi_static_param_reset_req7uint8_t8uint32_t"></a> <a id="_CPPv234bk_wifi_csi_static_param_reset_req7uint8_t8uint32_t"></a> <a id="bk_wifi_csi_static_param_reset_req__uint8_t.uint32_t"></a> <a id="group__bk__api__wifi__v2_1gadf9b414e277566146e16598f0d5913eb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_csi\_static\_param\_reset\_req(uint8\_t update\_cali\_mode, uint32\_t cali\_cnt)
:   clear csi static param to recalibration, only for old algorithm

    **Attention**
    :   . during calibration, the surrounding encironment must still

    参数
    :   - **update\_cali\_mode** – calibration mode. 0: no calibration, 1: start calibration and with update calibration result 2: start calibration, 3: update calibration result
        - **cali\_cnt** – calibration count frame

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="_CPPv430bk_wifi_csi_demo_turn_on_light7uint8_tb"></a>

<a id="_CPPv330bk_wifi_csi_demo_turn_on_light7uint8_tb"></a> <a id="_CPPv230bk_wifi_csi_demo_turn_on_light7uint8_tb"></a> <a id="bk_wifi_csi_demo_turn_on_light__uint8_t.b"></a> <a id="group__bk__api__wifi__v2_1gafd1ac2514415aa39dcae6902e735190a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_wifi\_csi\_demo\_turn\_on\_light(uint8\_t color, bool flicker)
:   csi demo light control

    参数
    :   - **color** – the color of the light
        - **flicker** – the light is flicker

    返回
    :   - kNoErr: succeed
        - otherwise: fail

<a id="id3"></a>

## 参考链接

- [Wi-Fi 类型定义](bk_wifi_types.md)
- [Netif](../network/bk_netif.md)
- [Wi-Fi 快速入门](../../developer-guide/wifi/bk_wifi_get_started.md)
- [Wi-Fi 项目示例](../../examples/projects/wifi.md)
