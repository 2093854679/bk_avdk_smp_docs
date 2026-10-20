---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/network/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 网络

本章节描述 **通用网络栈** API，适用于 Wi-Fi、以太网、4G 等多种接入方式共用的网络抽象层。

- **Netif**：`ap/include/components/netif.h` 中的 IP 配置 API；类型与事件见 Netif 类型定义
- **以太网 / 4G 等**：后续版本在此章节扩展（如 `bk_modem`、以太网驱动相关 API）

Wi-Fi 专有 API 见 [Wi-Fi](wifi.md)。

- [Netif](network/bk_netif.md)
  - [netif.h](network/bk_netif.md#netif-h)
  - [参考链接](network/bk_netif.md#id1)
- [Netif 类型定义](network/bk_netif_types.md)
  - [netif\_types.h](network/bk_netif_types.md#netif-types-h)

## 模块导航

- [简介](../introduction.md)
- [H/W 参考手册](../hw-reference.md)
- [API 参考手册](../api-reference.md)
- [外设](peripheral.md)
- [系统](system.md)
- [Netif](network/bk_netif.md)
- [Netif 类型定义](network/bk_netif_types.md)
- [Wi-Fi](wifi.md)
- [多媒体](multimedia.md)
- [音频](audio.md)
- [蓝牙](bluetooth.md)
- [开发者指南](../developer-guide.md)
- [操作系统与内存管理](../os.md)
- [样例演示](../examples.md)
- [项目示例](../examples/projects.md)
- [应用开发](../application.md)
- [开发与贡献代码流程](../process.md)
- [云平台](../cloud.md)
- [常见问题](../FAQ.md)
- [支持的外设](../support_peripherals.md)
