---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/wifi/bk_wifi_controller.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cp-wi-fi"></a>

# **CP Wi-Fi 控制器架构**

<a id="id1"></a>

## **概述**

BK7259 SMP 采用 AP 应用核 \+ CP 控制器核 的 Wi-Fi 架构。客户应用程序运行在 AP 核，通过 `ap/include/modules/wifi.h` 中的 bk\_wifi 系列 API 使用 Wi-Fi；CP 核承载 LMAC、wpa\_supplicant、PHY 及数据面，AP 侧 API 经 IPC 转发至 CP 执行。

本文描述 CP 侧控制器实现，供平台集成与驱动调试参考。

<a id="id5"></a>
![BK7259 SMP Wi-Fi 平台架构](../../../../_assets/bba6de3e015a6c35cc99-bk7259_smp_wifi_arch_zh.png)


BK7259 SMP Wi-Fi 平台架构（AP 应用核与 CP Wi-Fi 控制器）

<a id="id2"></a>

## **架构分层**

<a id="id6"></a>
![BK7259 SMP Wi-Fi 软件分层](../../../../_assets/0fa28bcfa0c6c5e08e0b-bk7259_smp_wifi_layers_zh.png)


BK7259 SMP Wi-Fi 软件分层与调用链

```
客户应用 (AP)  →  bk_wifi API (wifi_api.c)  →  wdrv IPC  →  cif_wifi_api (CP)  →  wifi_v2.c / LMAC / WPA
```

- AP 应用：projects/wifi/sta\_example/ap/ap\_main.c 等，调用 bk\_wifi API
- AP Wi-Fi Host：ap/components/bk\_wifi/src/wifi\_api.c；ap/components/bk\_wifi\_driver/（wdrv IPC 客户端）
- CP 控制器接口：cp/components/controller\_if/cif\_wifi\_api.c
- CP Wi-Fi 实现：cp/components/bk\_wifi/src/wifi\_v2.c；rwnx / rw\_msg（LMAC）；libwifi.a
- CP 网络：`cp/components/bk_wifi/src/wifi_netif.c`、`cp/components/bk_wifi/src/wifi_wpa_cmd.c` （内部 wpa 命令处理）

<a id="cp"></a>

## **CP 侧关键组件**

**wifi\_v2.c**

CP 上 `bk_wifi_*` 的真实实现。AP 侧 `wifi_api.c` 通过 IPC 将同名 API 请求映射到此。

**controller\_if**

`cif_wifi_api.c` 接收 AP 经 mailbox 发来的 Wi-Fi 控制命令，并将状态通过 indication 回传 AP。

**LMAC / libwifi.a**

底层 MAC 位于 `cp/components/bk_wifi/`，部分为预编译 `libwifi.a`。调试需使用 CP 串口及 [Wi-Fi 问题定位指南](bk_wifi_debug.md) 中的平台 CLI。

<a id="ap-cp"></a>

## **AP 与 CP 职责对照**

- 客户应用 / Demo：AP 核；CP 仅启动与 IPC 服务
- bk\_wifi API 调用：应用在 AP 发起；CP 执行驱动
- 事件 / DHCP：AP 上 bk\_event 与 netif；CP 负责数据面
- 推荐 CLI：AP 上 `sta` / `scan` / `ap`；CP 上 `ap_cmd` 转发
- 深度调试 CLI：CP 上 `pkt_dbg`、`wifi_diag` 等

<a id="id3"></a>

## **初始化说明**

CP 固件启动时完成 Wi-Fi 驱动与 controller 初始化；AP 侧 `bk_wifi_init()` 初始化 wdrv 并与 CP 同步。SMP 工程需 AP、CP 镜像同时烧录。

<a id="id4"></a>

## **相关文档**

- [Wi-Fi 问题定位指南](bk_wifi_debug.md) — 驱动与 LMAC 级问题定位
