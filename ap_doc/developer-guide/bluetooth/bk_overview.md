---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/bluetooth/bk_overview.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 蓝牙概述

本章对 BK7259 蓝牙做整体介绍，帮助开发者在阅读单BLE、双模蓝牙、DUT 等具体章节前，
先建立对蓝牙协议架构、BK7259 上蓝牙的软硬件分工，以及两套蓝牙协议栈的整体认识，
最后给出常用的蓝牙宏配置说明。

<a id="id2"></a>

## 1 蓝牙协议架构简介

蓝牙是一种短距无线通信技术，协议自上而下分为 **应用层(Application)**、**主机(Host)**、
**主机控制器接口(HCI)** 和 **控制器(Controller)** 四大部分。其中 Host 与 Controller
是两个相对独立的子系统，通过标准的 HCI 接口交互，这也是 BK7259 上蓝牙能拆分到两颗
CPU 子系统运行的基础。

各层主要职责如下：

| 层次 | 主要模块 | 职责 |
| --- | --- | --- |
| 应用层 Application | profile / 用户业务 | 业务逻辑、GATT profile、AT/CLI 命令等。 |
| 主机 Host | GAP、GATT、ATT、SMP、L2CAP / SDP、RFCOMM、A2DP、AVRCP、HFP 等 | 设备发现与连接管理、属性/服务数据库、加密配对、逻辑链路复用、各类上层 profile。 |
| 接口 HCI | HCI command / event / ACL / SCO | Host 与 Controller 之间的标准命令与数据通道。 |
| 控制器 Controller | Link Layer / Link Manager、Baseband、PHY | 链路调度、跳频、收发时序、射频物理层。 |

备注

本章只做工程视角的概要说明。完整的协议定义请参考
[Bluetooth Core Specification](https://www.bluetooth.com/specifications/specs/core-specification/)
及相关蓝牙协议文档；AD Type、UUID 等具体取值参考
[Assigned Numbers](https://www.bluetooth.com/specifications/assigned-numbers)。

<a id="bk7259-ap-cp"></a>

## 2 BK7259 蓝牙系统架构（AP / CP 分工）

BK7259 是多核 SMP 平台：CPU0、CPU1 组成通信处理器(CP)子系统，CPU2、CPU3 组成应用处理器(AP)
子系统，AP 与 CP 编译为相互独立的两个 image。蓝牙正是利用 HCI 这一标准分界，把协议栈拆分到
AP 与 CP 两个子系统上运行，整体架构如下图所示：

<a id="id7"></a>
![BK7259 蓝牙 AP/CP 架构](../../../../_assets/aaf3d3a74f191a5ba79c-bt_arch_ap_cp.png)


图 1\. BK7259 蓝牙 AP / CP 软件架构

各子系统职责如下：

- **AP 子系统：默认运行蓝牙 Host。** 由配置项 `CONFIG_BLUETOOTH_AP=y` 与
  `CONFIG_BLUETOOTH_HOST_ONLY=y` 控制，运行 GAP/GATT/SMP 等 Host 协议以及上层 profile、
  AT/CLI 命令。单 BLE 协议栈下应用通过 `bk_ble_*` API 使用 BLE 功能；双模协议栈下应用通过
  `bk_dm_*` API 使用蓝牙功能（经典蓝牙与 BLE 均经此接口）。
- **CP 子系统：默认运行蓝牙 Controller。** 由配置项 `CONFIG_BTDM_CONTROLLER_ONLY=y` 控制，
  运行 Link Layer、Baseband 调度并直接驱动射频。
- **AP 与 CP 之间通过 HCI over IPC 通信。** 由 `CONFIG_BLUETOOTH_SUPPORT_IPC=y` 使能，
  Host 产生的 HCI command/ACL 经核间 IPC 透传给 CP 的 Controller，Controller 的 HCI event/ACL
  经 IPC 回传给 AP 的 Host。相关实现位于 `bk_bluetooth/core/hci` 与 `bk_bluetooth/core/ipc`。

一次典型的蓝牙操作在 AP / CP 之间的交互时序如下图所示：

<a id="id8"></a>
![HCI over IPC 交互时序](../../../../_assets/15d29a72dbf2a11627fc-bt_hci_ipc_seq.png)


图 2\. HCI over IPC 交互时序

备注

AP 默认 `CONFIG_BLUETOOTH_AUTO_ENABLE=y`，开机阶段自动完成蓝牙协议栈初始化与 Host/Controller
握手，应用层无需手动拉起。

<a id="bk7259-sdk"></a>

## 3 BK7259 的两套蓝牙 SDK（协议栈）

BK7259 提供两套独立的蓝牙协议栈，分别面向 **单BLE** 与 **双模(BT \+ BLE)** 场景，
工程通过宏配置选择其中一套。

<a id="ble"></a>

### 3.1 单 BLE 协议栈

- 面向只使用 BLE 的产品（如 IoT 配网、BLE 数据透传、HID 等）。
- 通过 `CONFIG_BLE=y`、`CONFIG_BT=n` 选择，仅包含 BLE 相关能力（GAP/GATT/SMP）。
- 应用编程使用 `bk_ble_*` 系列 API，具体用法见 [单BLE](bk_ble.md)。
- Bluetooth Mesh 工程使用 Zephyr v2.7.6 Bluetooth Host 和 Mesh 协议栈，仍然基于 BLE
  controller-only 运行，示例工程为 `projects/bluetooth/mesh`。

<a id="bt-ble"></a>

### 3.2 双模协议栈（BT \+ BLE）

- 面向需要经典蓝牙的产品（如 A2DP/HFP 音频、SPP、AVRCP），并同时支持 BLE。
- 通过 `CONFIG_BT=y`、`CONFIG_BLE=y` 选择，在 BLE 之外额外提供经典蓝牙的各类 profile。
- 应用编程统一使用 `bk_dm_*` 系列 API（经典蓝牙与 BLE 均经此接口）。
- 上层经典蓝牙/双模 service 由 `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE` 及其子模块开关控制，
  BLE 侧公共 GATT 框架由 `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATT` 控制。

两套协议栈的对比如下：

| 维度 | 单 BLE 协议栈 | 双模协议栈(BT \+ BLE) |
| --- | --- | --- |
| 适用场景 | 仅 BLE | 经典蓝牙 \+ BLE |
| 关键开关 | `CONFIG_BLE=y` / `CONFIG_BT=n` | `CONFIG_BLE=y` / `CONFIG_BT=y` |
| 上层能力 | GAP/GATT/SMP | 额外提供 A2DP/AVRCP/HFP/SPP 等 profile |

备注

Bluetooth Mesh 是基于 BLE 的独立协议栈场景，AP 侧使用 Zephyr Bluetooth Host/Mesh，
CP 侧仍运行 BLE controller-only。Mesh 工程不使用 `bk_ble_*`/`bk_dm_*` 应用 API，
而是通过 Zephyr Mesh API 和 `ble_mesh` CLI 演示配网与模型控制流程。

备注

media 与蓝牙因内存复用无法共存；使用蓝牙前需关闭 media 相关功能，使用 media 前需关闭蓝牙功能。

<a id="id3"></a>

## 4 蓝牙宏配置

蓝牙相关宏分布在 AP 与 CP 各自的 `bk_bluetooth/Kconfig` 中，可通过 menuconfig 配置或在工程
defconfig 中覆盖。下表列出常用配置项。

<a id="ap-host"></a>

### 4.1 AP 侧（Host）配置

位于 `ap/components/bk_bluetooth/Kconfig`：

| 配置项 | 默认 | 说明 |
| --- | --- | --- |
| `CONFIG_BLUETOOTH_AP` | y | 使能 AP 侧蓝牙。 |
| `CONFIG_BLUETOOTH_HOST_ONLY` | y | AP 仅运行 Host（与 CP 的 Controller 配对）。 |
| `CONFIG_BT` | n | 使能经典蓝牙（需双模协议栈）。 |
| `CONFIG_BLE` | y | 使能 BLE。 |
| `CONFIG_BLUETOOTH_AUTO_ENABLE` | y | 开机自动初始化蓝牙协议栈。 |
| `CONFIG_BLUETOOTH_SUPPORT_IPC` | y | 通过核间 IPC 与 CP Controller 通信（HCI over IPC）。 |
| `CONFIG_BLUETOOTH_BLE_SLAVE_ONLY` | n | 仅支持 BLE 从机角色，进一步裁剪。 |
| `CONFIG_BLUETOOTH_BLE_SLAVE_OBSERVER` | n | 仅支持 BLE 从机 \+ observer。 |
| `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE` | n | 使能双模上层 service（A2DP/AVRCP/HFP 等）。 |
| `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATT` | y | 使能公共 GATT 框架（`dm_*`），供 AT Server 与上层 demo 使用。 |
| `CONFIG_BLE_LE_AUDIO` | n | 使能 LE Audio BAP API，并链接双模 LE Audio host 库；`projects/bluetooth/le_audio/` 下各工程（broadcast\_source / broadcast\_sink / unicast\_client / unicast\_server）需开启。 |

<a id="cp-controller"></a>

### 4.2 CP 侧（Controller）配置

位于 `cp/components/bk_bluetooth/Kconfig`：

| 配置项 | 默认 | 说明 |
| --- | --- | --- |
| `CONFIG_BTDM_CONTROLLER_ONLY` | y | CP 仅运行 Controller。 |
| `CONFIG_BT` / `CONFIG_BLE` | n / y | 是否使能经典蓝牙 / BLE（需与 AP 侧保持一致）。 |
| `CONFIG_BLUETOOTH_BLE_SLAVE_ONLY` | n | 仅支持 BLE 从机角色，进一步裁剪（需与 AP 侧保持一致）。 |
| `CONFIG_BLUETOOTH_SUPPORT_IPC` | y | 与 AP Host 通过 IPC 通信。 |
| `CONFIG_BLE_LV_SUPPORT` | n | 支持低压睡眠。 |
| `CONFIG_BLUETOOTH_SUPPORT_LPO_ROSC` | n | 低功耗时钟源使用内部 ROSC。 |

<a id="id4"></a>

### 4.3 协议栈的选择

选择”单 BLE”还是”双模”，由上述公共宏决定：`CONFIG_BLE` / `CONFIG_BT` 决定使能的协议类型。
AP 与 CP 两侧的相关开关需保持一致。

<a id="id5"></a>

### 4.4 典型场景宏配置

下面给出三种常见产品形态的推荐宏组合。以下所有开关都需要 **AP 与 CP 两侧保持一致**。

**场景 1：BLE 最大使用场景（默认配置）**

面向需要同时管理多条 BLE 连接的产品，是 SDK 的默认配置：使能单 BLE 协议栈，
支持最多 8 条链路（主机 master \+ 从机 slave 混合），并可同时进行广播(adv)与扫描(scan)。

- `CONFIG_BLE=y` / `CONFIG_BT=n`：单 BLE 协议栈。

**场景 2：BLE 配网场景（最小内存配置）**

面向仅用于 IoT 配网的产品，追求最小内存/代码体积：在场景 1 基础上仅保留 BLE 从机角色，
裁剪 master/central 相关能力。

- 在场景 1（`CONFIG_BLE=y` / `CONFIG_BT=n`）的基础上，额外开启：
- `CONFIG_BLUETOOTH_BLE_SLAVE_ONLY=y`：仅支持 BLE 从机角色，裁剪 master/central 相关能力，减小内存占用。

**场景 3：双模场景（BLE \+ 经典蓝牙）**

在场景 1 的基础上额外使能经典蓝牙，支持 A2DP / AVRCP / HFP 等 profile。

- `CONFIG_BLE=y` / `CONFIG_BT=y`：双模协议栈。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE=y`：使能上层双模 service（A2DP/AVRCP/HFP 等）。
- `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATT=y`：使能公共 GATT 框架。
- 应用编程统一使用 `bk_dm_*` 系列 API。

**场景 4：Bluetooth Mesh**

面向 Bluetooth Mesh 节点或 provisioner 场景：AP 运行 Zephyr v2.7.6 Bluetooth Host/Mesh，
CP 运行 BLE controller-only，通过 HCI over IPC 通信。

- `CONFIG_BLE=y` / `CONFIG_BT=n`：单 BLE controller。
- AP 侧开启 `CONFIG_BLE_MESH_ZEPHYR=y`，并按需开启 `CONFIG_BT_MESH_PB_ADV`、
  `CONFIG_BT_MESH_PB_GATT`、`CONFIG_BT_MESH_GATT_PROXY` 等 Mesh 能力。
- CP 侧保持 `CONFIG_BTDM_CONTROLLER_ONLY=y`。

三种场景对应的 AP 侧与 CP 侧宏配置如下：

| 场景 | AP 侧宏 | CP 侧宏 |
| --- | --- | --- |
| 场景 1：BLE 最大 | `CONFIG_BLUETOOTH_AP=y`  `CONFIG_BLE=y`  `CONFIG_BT=n` | `CONFIG_BLUETOOTH=y`  `CONFIG_BLE=y`  `CONFIG_BT=n` |
| 场景 2：BLE 配网 | `CONFIG_BLUETOOTH_AP=y`  `CONFIG_BLE=y`  `CONFIG_BT=n`  `CONFIG_BLUETOOTH_BLE_SLAVE_ONLY=y` | `CONFIG_BLUETOOTH=y`  `CONFIG_BLE=y`  `CONFIG_BT=n`  `CONFIG_BLUETOOTH_BLE_SLAVE_ONLY=y` |
| 场景 3：双模 | `CONFIG_BLUETOOTH_AP=y`  `CONFIG_BLE=y`  `CONFIG_BT=y`  `CONFIG_BLUETOOTH_BTDM_COMPONENT_ENABLE=y`  `CONFIG_BLUETOOTH_BTDM_COMPONENT_BLE_GATT=y` | `CONFIG_BLUETOOTH=y`  `CONFIG_BLE=y`  `CONFIG_BT=y` |
| 场景 4：Bluetooth Mesh | `CONFIG_BLUETOOTH_AP=y`  `CONFIG_BLUETOOTH_HOST_ONLY=y`  `CONFIG_BLE=y`  `CONFIG_BT=n`  `CONFIG_BLE_MESH_ZEPHYR=y` | `CONFIG_BLUETOOTH=y`  `CONFIG_BLE=y`  `CONFIG_BT=n`  `CONFIG_BTDM_CONTROLLER_ONLY=y` |

<a id="id6"></a>

## 5 参考链接

- [单BLE](bk_ble.md)：BLE 常用使用场景与示例。
- [双模蓝牙](bk_dual.md)：双模蓝牙说明。
- [DUT](dut.md)：蓝牙射频 DUT 测试。
- [API 参考](../../api-reference/bluetooth.md) 介绍了蓝牙 API 接口。
