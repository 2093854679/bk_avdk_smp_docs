---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/wifi/bk_wifi_mode.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wi-fi-ap-sta-p2p-cli"></a>

# Wi-Fi AP/STA/P2P 模式与 CLI

本章说明 BK7259 SMP 上 STA、SoftAP、P2P 的 **CLI 使用方式**。应用开发应优先在 **AP 核** 调用 `bk_wifi_*` API；CLI 仅用于联调与验证。

<a id="cli-bk7259-smp"></a>

## **CLI 总览（BK7259 SMP）**

- **AP UART**：`sta` `ap` `scan` `stop` `state` ``` p2p``（需 ``CONFIG_P2P ```）
- **CP UART \+ \`\`ap\_cmd\`\`**：`ap_cmd sta` `ap_cmd scan` `ap_cmd ap` 等，转发至 AP Shell
- CLI 实现：`ap/components/bk_cli/cli_wifi.c`，需 `CONFIG_WIFI_CLI_ENABLE`
- `ap_cmd` 由 CP `cli_cpu1_command()` 经 mailbox 转发至 AP Shell，需 `CONFIG_SHELL_ASYNCLOG` 与 `CONFIG_MAILBOX`。详见 [系统调试](../debug_trace.md)

<a id="sta"></a>

## **STA 模式**

AP UART:

```
sta BEKEN_TEST 12345678
scan
stop sta
state
```

CP UART（`ap_cmd` 转发）:

```
ap_cmd sta BEKEN_TEST 12345678
ap_cmd scan
```

<a id="softap"></a>

## **SoftAP 模式**

AP UART:

```
ap BEKEN_TEST 12345678
stop ap
```

CP UART（`ap_cmd`）:

```
ap_cmd ap BEKEN_TEST 12345678
```

备注

BK7259 支持 AP \+ STA 共存。

<a id="p2p"></a>

## **P2P 模式**

需 AP/CP 均开启 `CONFIG_P2P`，详见 [p2p](../../examples/projects/wifi/p2p.md) 与 [Armino Wi-Fi P2P 使用指南](bk_wifi_p2p.md)。

AP UART（或 CP UART 使用 `ap_cmd p2p ...`）：

- `p2p enable` `p2p find` `p2p listen` `p2p connect` `p2p disable` 等

API 见 `ap/include/modules/wifi.h` 中 `bk_wifi_p2p_*`；详细说明见 [Armino Wi-Fi P2P 使用指南](bk_wifi_p2p.md)。

备注

BK7259 支持 AP \+ P2P 共存。
