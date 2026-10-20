---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/wifi/bk_wifi_get_started.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wi-fi"></a>

# Wi-Fi 快速入门

<a id="bk7259-smp"></a>

## **BK7259 SMP 说明**

- 客户应用运行在 AP 核：在 `projects/*/ap/ap_main.c` 中调用 `bk_wifi_*` API，处理 `EVENT_WIFI_*` / `EVENT_NETIF_*` 事件
- CP 核为 Wi-Fi 控制器：承载 LMAC、wpa\_supplicant；AP API 经 IPC 自动转发，客户无需直接调用 CP 侧驱动
- 串口调试：默认接 CP UART 时用 `ap_cmd sta <ssid> <password>`；接 AP UART 时直接使用 `sta` / `scan` / `ap`。详见 [Wi-Fi AP/STA/P2P 模式与 CLI](bk_wifi_mode.md) 与 [系统调试](../debug_trace.md)

<a id="id1"></a>

## **参考工程**

完整示例请参阅 [Wi-Fi 项目示例](../../examples/projects/wifi.md)。

<a id="sta"></a>

## **典型 STA 流程**

- 在 `main` 中调用 `bk_init`，SDK 内部会完成 event、netif、wifi 初始化
- 调用 `bk_event_register_cb` 注册 Wi-Fi / netif 事件
- 调用 `bk_wifi_sta_set_config` 与 `bk_wifi_sta_start`
- 收到 `EVENT_WIFI_STA_CONNECTED` 后走 DHCP；`EVENT_NETIF_GOT_IP4` 后可建 socket

<a id="id2"></a>

## **生命周期说明**

- 启动阶段：仅调用 `bk_init` 即可，不要手动调用 `bk_event_init`、`bk_netif_init`、`bk_wifi_init`
- 停止 STA：使用 `bk_wifi_sta_stop`，或先 `bk_wifi_sta_disconnect`
- 停止 AP：使用 `bk_wifi_ap_stop`
- 需要省电：使用 PM / 低功耗接口，而非反初始化整个 Wi-Fi 栈
- AP 侧无 `bk_wifi_deinit` API

CLI 快速验证（AP UART）:

```
sta your_ssid your_password
```

<a id="id3"></a>

## **下一步**

- 项目示例：[Wi-Fi 项目示例](../../examples/projects/wifi.md)
- API 与事件详解：[Armino Wi-Fi 驱动程序](bk_wifi.md)
- CLI 与 `ap_cmd`：[Wi-Fi AP/STA/P2P 模式与 CLI](bk_wifi_mode.md)
- 扫描 API：[Armino Wi-Fi 驱动程序](bk_wifi.md) 中「Armino Wi-Fi 扫描」；示例：[scan\_example](../../examples/projects/wifi/scan_example.md)
