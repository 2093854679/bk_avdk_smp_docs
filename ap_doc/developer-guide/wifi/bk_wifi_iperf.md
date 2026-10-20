---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/wifi/bk_wifi_iperf.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wi-fi-iperf"></a>

# Wi-Fi iPerf

本节介绍 iPerf CLI 用法，用于 Wi-Fi 连通后测试 TCP/UDP 吞吐。编译与工程说明见 [iperf](../../examples/projects/wifi/iperf.md)。

<a id="iperf"></a>

## **iPerf 用法**

```
Usage: iperf [-s|-c host] [options]
       iperf [-h|--stop]

Client/Server:
-p           server port to listen on/connect to

Server specific:
-s           run in server mode

Client specific:
-c <host>    run in client mode, connecting to <host>

Miscellaneous:
-u           udp support, and the default mode is tcp
-h           print this message and quit
--stop       stop iperf program
```

<a id="id1"></a>

## **命令示例**

| 模式 | 命令 |
| --- | --- |
| TCP Client 上行 | `iperf -c IP` |
| UDP Client 上行 | `iperf -c IP -u` |
| TCP Server 下行 | `iperf -s` |
| UDP Server 下行 | `iperf -s -u` |

使用前请先通过 [Wi-Fi AP/STA/P2P 模式与 CLI](bk_wifi_mode.md) 完成 STA 或 SoftAP 联网，再在 AP 串口（或 `ap_cmd`）执行上述命令。

<a id="id2"></a>

## **运行日志示例**

```
iperf -c 192.168.40.69
iperf: connect to iperf server successful!
[0-1] sec bandwidth: 20021 Kbits/sec.
[1-2] sec bandwidth: 21757 Kbits/sec.
```

<a id="id3"></a>

## **常见问题**

- 建议使用 iPerf 2.0.x 版本（[iPerf 下载](https://iperf.fr/)）
- 吞吐受 RF 性能、环境干扰、内存、路由器兼容性等影响
- 吞吐偏低时可结合 [Wi-Fi 问题定位指南](bk_wifi_debug.md) 与空口抓包分析
