---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/wifi/bk_wifi_iperf.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wi-fi-iperf"></a>

# Wi-Fi iPerf 应用示例

本节介绍基于博通集成芯片的 iPerf 用法，包含三部分：

- iPerf 测试示例与配置
- 博通集成 iPerf 用法
- 常见问题

<a id="id1"></a>

## 示例与配置

iPerf 配置位于 `components/demos/net/iperf/iperf.c`，支持四种模式：
TCP\_SERVER、TCP\_CLIENT、UDP\_SERVER、UDP\_CLIENT

- IPERF\_REPORT\_INTERVAL—————–上报间隔，默认 1s
- IPERF\_MAX\_TX\_RETRY——————–最大重试次数，默认 10
- THREAD\_PROIRITY———————–系统线程优先级，默认 4

<a id="iperf"></a>

## 博通集成 iPerf 用法

<a id="id2"></a>

### iPerf 用法

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

<a id="id3"></a>

### iPerf 命令示例

|  |  |
| --- | --- |
| Client 模式（上行） | |
| TCP Client 模式 | iperf -c IP |
| UDP Client 模式 | iperf -c IP -u |
| Server 模式（下行） | |
| TCP Server 模式 | iperf -s |
| UDP Server 模式 | iperf -s -u |

<a id="id4"></a>

### iPerf 运行日志

```
iperf -c 192.168.40.69              //TCP Client TX
create iperf_tcp_c, tcb=30024cf0, stack=[30032170-30033170:4096], prio=5
iperf: connect to iperf server successful!
[0-1] sec bandwidth: 20021 Kbits/sec.
[1-2] sec bandwidth: 21757 Kbits/sec.

iperf -s -i1                        //TCP Server RX
create iperf_tcp_s, tcb=30024d20, stack=[30031ce0-30032ce0:4096], prio=5
iperf: new client connected from (192.168.40.69, 65070)
[0-1] sec bandwidth: 11567 Kbits/sec.
[1-2] sec bandwidth: 15658 Kbits/sec.

iperf -c 192.168.40.69 -u           //UDP Client TX
create iperf_udp_c, tcb=30024cf0, stack=[30031ce0-30032ce0:4096], prio=5
iperf udp mode run...
[0-1] sec bandwidth: 28141 Kbits/sec.
[1-2] sec bandwidth: 35268 Kbits/sec.

iperf -s -u -i1                     //UDP Server RX
create iperf_udp_s, tcb=30024cf0, stack=[30031ce0-30032ce0:4096], prio=5
[0-1] sec bandwidth: 17463 Kbits/sec.
[1-2] sec bandwidth: 18910 Kbits/sec.
```

<a id="id5"></a>

## 常见问题

<a id="id6"></a>

### iPerf 工具说明

- iPerf 工具下载：[Download](https://iperf.fr/) 。说明见 `iPerf user docs`

![../../_images/iperf.png](../../../../../_assets/036d3fbab323cef4d8a5-iperf.png)

- 建议使用 iPerf 2.0.x 版本

<a id="id7"></a>

### 影响 iPerf 吞吐的因素

- DUT Wi-Fi RF 性能，需保证 OTA、EVM 测试通过
- 测试环境干扰：最好在屏蔽室中测试
- 测试环境：AP 与 DUT 保持合理距离，外置天线优于内置天线
- 为 iPerf 运行预留足够内存
- 与部分路由器的兼容性
