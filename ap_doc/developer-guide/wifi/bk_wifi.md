---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/wifi/bk_wifi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="armino-wi-fi"></a>

# **Armino Wi-Fi 驱动程序**

<a id="id1"></a>

## **Armino Wi-Fi 功能列表**

Armino BK7259 支持以下 Wi-Fi 功能：

- 支持 3 个虚拟接口，即 STA、AP、Monitor
- 支持仅 station 模式、仅 AP 模式、station \+ AP 共存模式
- 支持 IEEE802.11 b/g/n/ax 2.4GHz 协议标准
- 支持 AMSDU、AMPDU、QoS、HT40 以及其他主要功能
- 支持802.11N MCS0-7
- 支持 WPA、WPA2 及 WPA3 等加密方式
- station 模式下支持低功耗休眠
- 空中数据传输最高可达 20Mbits/s TCP 吞吐和 35Mbits/s UDP 吞吐
- 支持 TWT

<a id="bk7259-smp"></a>

## **BK7259 SMP 架构（客户开发视角）**

BK7259 为 SMP 双核方案：**客户应用程序运行在 AP 核**，通过 `ap/include/modules/wifi.h` 中的 `bk_wifi_*` API 使用 Wi-Fi；**CP 核** 作为 Wi-Fi 控制器，运行 LMAC、wpa\_supplicant 及底层驱动，AP 侧 API 经 IPC 自动转发至 CP，客户 **无需** 在应用代码中直接调用 CP 驱动。

<a id="id50"></a>
![BK7259 SMP Wi-Fi 平台架构](../../../../_assets/797cbaee8c6168d0a950-bk7259_smp_wifi_arch_zh.png)


BK7259 SMP Wi-Fi 平台架构（AP 应用核与 CP Wi-Fi 控制器）

- 应用入口：`projects/*/ap/ap_main.c`
- 事件与 DHCP：在 AP 核注册 `bk_event_register_cb()`，关注 `EVENT_WIFI_*`、`EVENT_NETIF_GOT_IP4`
- 串口调试：默认 CP UART 可用 `ap_cmd sta/scan/ap` 转发 AP Wi-Fi CLI；接 AP UART 时直接使用 `sta` / `scan` / `ap`
- 快速入门：[Wi-Fi 快速入门](bk_wifi_get_started.md)；项目示例：[Wi-Fi 项目示例](../../examples/projects/wifi.md)；CLI 说明：[Wi-Fi AP/STA/P2P 模式与 CLI](bk_wifi_mode.md)

<a id="id2"></a>

## **如何编写 Armino Wi-Fi 应用程序**

<a id="id3"></a>

### **准备工作**

我们建议客户在编写自己的 Wi-Fi 应用程序之前，先阅读 [Wi-Fi 项目示例](../../examples/projects/wifi.md) 与 [Wi-Fi 快速入门](bk_wifi_get_started.md)。本文补充 Wi-Fi API 规则、实现限制及常见错误说明。

<a id="id4"></a>

### **设置 Armino Wi-Fi 编译时选项**

请参阅 [Armino Wi-Fi Menuconfig](#armino-wi-fi-menuconfig)

<a id="id5"></a>

### **Armino Wi-Fi 初始化**

请参阅 [Armino Wi-Fi station 一般情况](#armino-wi-fi-station) 、[Armino Wi-Fi AP 一般情况](#armino-wi-fi-ap)

<a id="wi-fi"></a>

### **启动/连接 Wi-Fi**

请参阅 [Armino Wi-Fi station 一般情况](#armino-wi-fi-station) 、[Armino Wi-Fi AP 一般情况](#armino-wi-fi-ap)

<a id="id6"></a>

### **事件处理**

一切顺利的理想情况下，按照 [Armino Wi-Fi事件描述](#id9) 中介绍的事件，如 [EVENT\_WIFI\_SCAN\_DONE](#event-wifi-scan-done) 、[EVENT\_WIFI\_STA\_CONNECTED](#event-wifi-sta-connected) 等，按照正常事件接收并调用回调函数。客户需要注意异常情况下的事件处理，如 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected)，使自己的应用程序更加强壮符合产品设计。更详细请参阅 [Armino Wi-Fi station 一般情况](#armino-wi-fi-station) 、[Armino Wi-Fi AP 一般情况](#armino-wi-fi-ap)

<a id="id7"></a>

### **异常恢复程序**

产品应用场景可能遇到比较恶劣的情况，异常恢复机制对于一个健壮的 Wi-Fi 应用程序至关重要，建议客户在设计之初予以重视。请参阅 [Armino Wi-Fi API 错误码](#armino-wi-fi-api)

<a id="armino-wi-fi-api"></a>

## **Armino Wi-Fi API 错误码**

Armino Wi-Fi 都有定义好的返回值，即错误代码。这些错误代码一般可以分为以下几种：

- 无错误，返回 OK，例如：BK\_OK
- 可恢复错误，例如：BK\_ERR\_WIFI\_STA\_NOT\_STARTED
- 其他客户自定义的错误

我们强烈建议客户在自己的应用程序中根据应用场景自定义错误代码，并根据错误级别区分严重程度。在 [wifi\_types.h](https://gitlab.bekencorp.com/wifi/armino/-/blob/main/include/modules/wifi_types.h) 中我们定义了一些常见的基础 API 错误码，客户在开发初期可以作为默认的错误处理代码，但是，我们仍然建议客户自己编写对应的 API 错误码

<a id="wi-fi-api"></a>

## **初始化 Wi-Fi API 参数**

初始化 API 的结构参数时，应该遵循以下两种方式之一：

- 设置该参数的所有字段
- 先使用 get API 获取当前配置，然后根据客户应用程序设置特定字段

初始化/获取整个结构参数至关重要，一般情况下，返回值为 0 意味着应用程序使用了默认参数，建议客户在设置参数 前先 get API 配置，根据当前已有的参数进行配置客制化字段。未来我们也会在升级 SDK 时将更多的字段初始化，确保客户应用程序在 SDK 升级过程中运行稳定。

<a id="id8"></a>

## **Armino Wi-Fi 编程模型**

<a id="id51"></a>
![../../_images/program.png](../../../../_assets/e2e2f30b0f1745832a1f-program.png)


Armino Wi-Fi 编程模型

Wi-Fi 驱动程序作为和上层代码（如 TCP/IP 协议栈、Application Task、Cli command等）的隔离组件，通常由用户应用程序代码负责调用 [Armino Wi-Fi 驱动程序 APIs](../../api-reference/wifi/bk_wifi.md) 来初始化 Wi-Fi 并进行相应的配置，Wi-Fi 驱动程序接收并处理 API 请求的数据，并将相关事件通知到应用程序处理
Armino Wi-Fi 事件处理是在 [armino event 库](bk_event.md) 基础上进行的。Armino SDK 中事件机制主要通过一个专门的事件任务来实现，应用程序可以使用 [`bk_event_register_cb()`](../../api-reference/system/bk_event.md#_CPPv420bk_event_register_cb14event_module_ti10event_cb_tPv "bk_event_register_cb") 中的回调函数来处理这些事件。除此之外，[BK NETIF 组件](../../api-reference/network/bk_netif.md) 也负责处理一些 Wi-Fi 事件，比如当 Wi-Fi station 连接至一个 AP 时，BK NETIF 会触发 [EVENT\_NETIF\_GOT\_IP4](#event-netif-got-ip4) 或者 [EVENT\_NETIF\_DHCP\_TIMEOUT](#event-netif-dhcp-timeout)

<a id="id9"></a>

## **Armino Wi-Fi事件描述**

<a id="event-wifi-scan-done"></a>

### **EVENT\_WIFI\_SCAN\_DONE**

扫描完成事件，由 [`bk_wifi_scan_start()`](../../api-reference/wifi/bk_wifi.md#_CPPv418bk_wifi_scan_startPK18wifi_scan_config_t "bk_wifi_scan_start") 函数触发，一般在以下情况产生：

- 扫描已经完成，比如 Wi-Fi 已经扫描到目标 SSID 或者 全部信道扫描完毕
- 当前扫描执行因函数 [`bk_wifi_scan_stop()`](../../api-reference/wifi/bk_wifi.md#_CPPv417bk_wifi_scan_stopv "bk_wifi_scan_stop") 而终止

以下情况下，将不会产生扫描完成事件：

- 当前扫描被终止
- 当前扫描是由函数 [`bk_wifi_sta_connect()`](../../api-reference/wifi/bk_wifi.md#_CPPv419bk_wifi_sta_connectv "bk_wifi_sta_connect") 发起

扫描示例见 [scan\_example](../../examples/projects/wifi/scan_example.md)；Scan API 见下文「Armino Wi-Fi 扫描」章节。

<a id="event-wifi-sta-connected"></a>

### **EVENT\_WIFI\_STA\_CONNECTED**

station 连接目标 AP 成功的事件，如果调用函数 [`bk_wifi_sta_connect()`](../../api-reference/wifi/bk_wifi.md#_CPPv419bk_wifi_sta_connectv "bk_wifi_sta_connect") 后接收到返回值 BK\_OK，并置上连接成功标志位 `WIFI_STA_CONNECTED_BIT`，则产生此连接事件。应用程序在接收到此事件后，根据应用场景决定是否启动 DHCP 客户端。如果应用程序启动 DHCP 客户端，在获取到 IP 地址之后即可开始接收和发送数据

<a id="event-wifi-sta-disconnected"></a>

### **EVENT\_WIFI\_STA\_DISCONNECTED**

此事件一般在以下情况下发生：

- 调用函数 [`bk_wifi_sta_stop()`](../../api-reference/wifi/bk_wifi.md#_CPPv416bk_wifi_sta_stopv "bk_wifi_sta_stop") 或者 [`bk_wifi_sta_disconnect()`](../../api-reference/wifi/bk_wifi.md#_CPPv422bk_wifi_sta_disconnectv "bk_wifi_sta_disconnect") 且此时，Wi-Fi station 已经成功连接 AP
- 调用函数 [`bk_wifi_sta_connect()`](../../api-reference/wifi/bk_wifi.md#_CPPv419bk_wifi_sta_connectv "bk_wifi_sta_connect")，但是 Wi-Fi 驱动程序因为某些原因未能成功连接 AP，比如：未能扫描到目标 AP、密码错误导致认证超时等
- Wi-Fi 连接成功后因为某些原因导致中断，比如：路由器掉电导致 station 连续丢失 N 个 Beacon、AP 主动删除 station、其他特殊情况等

当 Wi-Fi 驱动程序接收到该事件后，一般默认开始以下流程：

- 主动关闭 station 的 netif，并清除 IP 地址
- 通知应用层 Lwip 任务清除所有套接字状态错误的 TCP/UDP 连接。客户基于套接字编写的应用程序，回调函数可以在接收到此事件后尝试重启所有套接字

针对此断开事件，如果 **不是** 客户应用程序调用上述两个主动断开函数，Wi-Fi 驱动程序一般会自动发起重新连接。应用程序须明确区分当前断开事件发生的原因，并根据不同的原因采用不同的处理方式

<a id="event-netif-got-ip4"></a>

### **EVENT\_NETIF\_GOT\_IP4**

成功获取到 IPv4 地址事件，当 DHCP 客户端成功从 DHCP 服务器获取到 IPv4 地址时将产生此事件。收到此事件，代表整个 Wi-Fi station 连接流程真正成功完成，应用程序可以开始展开应用层业务，比如创建套接字等

该事件目前在以下情况下会上报：

- 开启 DHCP 客户端并成功从 DHCP 服务器分配到 IP 地址
- 使用静态 IP 功能时，Wi-Fi station 连接成功后直接从 flash 中读取保存的 IP 地址

<a id="event-netif-dhcp-timeout"></a>

### **EVENT\_NETIF\_DHCP\_TIMEOUT**

DHCP 客户端启动后，会默认开始一个定时器，当在定时器（20s）超时前 DHCP 客户端未能从 DHCP 服务器端获取到 IP 地址，将会触发此事件
对应的断开原因码为 260，详情可以参考 [Armino Wi-Fi 原因代码](#id35)

<a id="event-wifi-ap-connected"></a>

### **EVENT\_WIFI\_AP\_CONNECTED**

当每一个 station 成功接入 Armino Wi-Fi AP 的时候，都会触发此事件。事件应用在接收到此事件后，不需要做任何响应。应用程序回调函数也无需做出响应，一般客户应用程序可以基于此事件进行一些定制，比如获取接入 station 的基本信息等

<a id="event-wifi-ap-disconnected"></a>

### **EVENT\_WIFI\_AP\_DISCONNECTED**

此事件一般由以下几种情况触发：

- 应用程序通过调用函数 [`bk_wifi_ap_stop()`](../../api-reference/wifi/bk_wifi.md#_CPPv415bk_wifi_ap_stopv "bk_wifi_ap_stop") 主动断开 station 连接
- Wi-Fi 驱动程序因为某些原因断开 station 连接，比如：AP 在 5 分钟内没有接收到接入 station 的任何数据
- station 主动断开连接

该事件发生时，事件任务一般不需要特殊回应，但是应用程序的事件回调函数需要执行一些操作，如关闭与此 station 相关的套接字程序等

<a id="armino-wi-fi-station"></a>

## **Armino Wi-Fi station 一般情况**

下图为 Armino Wi-Fi station 模式下宏观场景，包含了初始化、配置、连接\&断开连接等各阶段的具体描述：

<a id="id52"></a>
![../../_images/connect_procedure.png](../../../../_assets/5b39d19a022d6ccc49a4-connect_procedure.png)


Armino Wi-Fi station 模式示例

<a id="id10"></a>

### **1\. Wi-Fi 初始化阶段**

- 1.1：应用 `main()` 调用 `bk_init()`，SDK 在 `app_wifi_init()` 中自动完成 event、netif 组件与 Wi-Fi 驱动初始化（客户\*\*无需\*\*手动调用 `bk_netif_init()`）
- 1.2：应用在自身任务中注册 Wi-Fi / netif 事件回调，并调用 [`bk_wifi_sta_set_config()`](../../api-reference/wifi/bk_wifi.md#_CPPv422bk_wifi_sta_set_configPK17wifi_sta_config_t "bk_wifi_sta_set_config") 等配置接口
- 1.3：应用创建业务任务（可选，与 Wi-Fi 初始化顺序无关）

建议客户只调用 `bk_init()`，详情参阅 [Wi-Fi 快速入门](bk_wifi_get_started.md)。

<a id="id11"></a>

### **2\. Wi-Fi 配置阶段**

Wi-Fi 驱动程序初始化完成后，可以进入到配置阶段。该场景下，Armino Wi-Fi 驱动程序处于 station 模式（默认）。应用程序可以调用函数 [`bk_wifi_sta_set_config()`](../../api-reference/wifi/bk_wifi.md#_CPPv422bk_wifi_sta_set_configPK17wifi_sta_config_t "bk_wifi_sta_set_config") 进行入参配置，一般情况下，用户只需要传入目标 AP 的名称和密码。请注意，该函数必须在函数 [`bk_wifi_sta_start()`](../../api-reference/wifi/bk_wifi.md#_CPPv417bk_wifi_sta_startv "bk_wifi_sta_start") 开启 Armino Wi-Fi station 之前调用。更详细的介绍可以访问 [wifi.h](https://gitlab.bekencorp.com/wifi/armino/-/blob/main/include/modules/wifi.h) 或者 [Armino Wi-Fi 配置](#id38)

<a id="id12"></a>

### **3\. Wi-Fi 启动阶段**

- 3.1：调用函数 [`bk_wifi_sta_start()`](../../api-reference/wifi/bk_wifi.md#_CPPv417bk_wifi_sta_startv "bk_wifi_sta_start") 开启 Wi-Fi 驱动程序
- 3.2：调用该函数前，必须确保参数已经配置成功，否则返回 `BK_ERR_WIFI_STA_NOT_CONFIG`；如果当前当前 station 已经启动，调用该函数时会直接返回 `BK_OK`。如果想重新加载 Wi-Fi 驱动程序，建议先调用 [`bk_wifi_sta_stop()`](../../api-reference/wifi/bk_wifi.md#_CPPv416bk_wifi_sta_stopv "bk_wifi_sta_stop")，然后再调用该函数。相关 API 介绍及使用方法可以参考 [wifi.h](https://gitlab.bekencorp.com/wifi/armino/-/blob/main/include/modules/wifi.h) ，API 返回值可以参阅 [Armino Wi-Fi API 错误码](#armino-wi-fi-api)

<a id="id14"></a>

### **4\. Wi-Fi 连接阶段**

- 4.1：调用函数 [`bk_wifi_sta_connect()`](../../api-reference/wifi/bk_wifi.md#_CPPv419bk_wifi_sta_connectv "bk_wifi_sta_connect") 后，Armino Wi-Fi 驱动程序将启动内部扫描、连接流程
- 4.2：开始扫描并成功发现目标 AP ，上报 [EVENT\_WIFI\_SCAN\_DONE](#event-wifi-scan-done) 事件
- 4.3：连接成功后，将产生 [EVENT\_WIFI\_STA\_CONNECTED](#event-wifi-sta-connected) 事件。事件任务接收成功后将启动 DHCP 客户端服务，触发 DHCP 流程
- 4.4：上述步骤 4.2、4.3 过程中，可能会遇到一些失败情况，如扫描不到 AP、连接失败等，这样的情况下，将触发 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected) 事件并提示对应的错误原因。下文阶段 6 将详细介绍 Armino Wi-Fi 断开流程

CLI 连网示例见 [Wi-Fi AP/STA/P2P 模式与 CLI](bk_wifi_mode.md)。

<a id="wi-fi-ip"></a>

### **5\. Wi-Fi 获取 IP 地址阶段**

- 5.1：一旦收到 [EVENT\_WIFI\_STA\_CONNECTED](#event-wifi-sta-connected) 事件，将启动 Lwip 的 DHCP 客户端获取 IP 地址
- 5.2：如果 Wi-Fi 驱动成功从 DHCP 服务器获取到 IP 地址，将触发 [EVENT\_NETIF\_GOT\_IP4](#event-netif-got-ip4) 事件
- 5.3：应用程序在收到 [EVENT\_NETIF\_GOT\_IP4](#event-netif-got-ip4) 事件后，基于 Lwip 构建的应用程序已经准备就绪，可以开始数据收发，比如：创建 TCP/UDP 套接字等。**请勿在获取 IP 地址之前启动任何套接字相关的操作**

<a id="id15"></a>

### **6\. Wi-Fi 断开阶段**

- 6.1：当 Wi-Fi 因为 AP 离线、RSSI 弱等原因断开连接，Wi-Fi 事件回调函数将产生 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected)。接收到此事件后，事件任务将通知 Lwip 清除所有任务并关闭所有 TCP/UDP 套接字
- 6.2：通常由于非期待的原因导致 Wi-Fi 断开，应用程序会发起重新连接。请参阅 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected)

<a id="id16"></a>

### **7\. Wi-Fi 清理阶段**

- 7.1：调用函数 [`bk_wifi_sta_disconnect()`](../../api-reference/wifi/bk_wifi.md#_CPPv422bk_wifi_sta_disconnectv "bk_wifi_sta_disconnect") 断开 Wi-Fi station 连接
- 7.2：调用函数 [`bk_wifi_sta_stop()`](../../api-reference/wifi/bk_wifi.md#_CPPv416bk_wifi_sta_stopv "bk_wifi_sta_stop") 终止 Wi-Fi 驱动程序，并释放相关的资源

<a id="armino-wi-fi-ap"></a>

## **Armino Wi-Fi AP 一般情况**

下图为 AP 模式下的宏观场景，各阶段与 station 模式类似，不再赘述，详细流程参考下图：

<a id="id53"></a>
![../../_images/ap_procedure.png](../../../../_assets/a43a76ebece455b9c0cd-ap_procedure.png)


Armino Wi-Fi AP 模式示例

<a id="id17"></a>

## **Armino Wi-Fi 扫描**

目前，仅 station 或者 station/AP 共存模式支持 Wi-Fi Scan，包含五个 API，详细介绍及使用方法可以参考 [wifi.h](https://gitlab.bekencorp.com/wifi/armino/-/blob/main/include/modules/wifi.h)

<a id="armino-wi-fi-scan-api"></a>

### **Armino Wi-Fi Scan API**

<a id="id19"></a>

#### **开启扫描**

函数 [`bk_wifi_scan_start()`](../../api-reference/wifi/bk_wifi.md#_CPPv418bk_wifi_scan_startPK18wifi_scan_config_t "bk_wifi_scan_start") 调用 Wi-Fi 驱动程序开始扫描，当扫描完成后，上报 EVENT\_WIFI\_SCAN\_DONE 事件，具体步骤可以参考如下：

- 准备扫描完成回调函数，回调函数可以参考 [`bk_wifi_scan_get_result()`](../../api-reference/wifi/bk_wifi.md#_CPPv423bk_wifi_scan_get_resultP18wifi_scan_result_t "bk_wifi_scan_get_result") 和 [`bk_wifi_scan_free_result()`](../../api-reference/wifi/bk_wifi.md#_CPPv424bk_wifi_scan_free_resultP18wifi_scan_result_t "bk_wifi_scan_free_result")
- 调用事件注册函数注册扫描完成事件回调，参考 [`bk_event_register_cb()`](../../api-reference/system/bk_event.md#_CPPv420bk_event_register_cb14event_module_ti10event_cb_tPv "bk_event_register_cb")
- 调用上述开始扫描函数，开启扫描

<a id="id20"></a>

#### **停止扫描**

调用函数 [`bk_wifi_scan_stop()`](../../api-reference/wifi/bk_wifi.md#_CPPv417bk_wifi_scan_stopv "bk_wifi_scan_stop") 停止 Wi-Fi 驱动程序扫描，作用与 [`bk_wifi_sta_disconnect()`](../../api-reference/wifi/bk_wifi.md#_CPPv422bk_wifi_sta_disconnectv "bk_wifi_sta_disconnect") 类似，但是该函数可能同步释放一些资源

<a id="id21"></a>

#### **获取扫描结果**

调用函数 [`bk_wifi_scan_get_result()`](../../api-reference/wifi/bk_wifi.md#_CPPv423bk_wifi_scan_get_resultP18wifi_scan_result_t "bk_wifi_scan_get_result") 获取扫描热点结果，一般返回值有以下几种：

- BK\_OK：扫描成功
- BK\_ERR\_NULL\_PARAM：扫描失败，扫描结果为空
- BK\_ERR\_NO\_MEM：扫描失败，没有内存
- others：其他错误

备注

1、调用者不需要单独申请内存，该API内会根据扫描结果申请内存
2、不要忘记调用 [`bk_wifi_scan_free_result()`](../../api-reference/wifi/bk_wifi.md#_CPPv424bk_wifi_scan_free_resultP18wifi_scan_result_t "bk_wifi_scan_free_result") 释放资源

<a id="id22"></a>

#### **输出扫描结果**

函数 [`bk_wifi_scan_dump_result()`](../../api-reference/wifi/bk_wifi.md#_CPPv424bk_wifi_scan_dump_resultPK18wifi_scan_result_t "bk_wifi_scan_dump_result") 用于打印输出扫描到的热点信息，返回值有两种：

- BK\_OK：打印成功
- BK\_ERR\_PARAM：无效的扫描结果

<a id="id23"></a>

#### **释放扫描结果**

调用 [`bk_wifi_scan_free_result()`](../../api-reference/wifi/bk_wifi.md#_CPPv424bk_wifi_scan_free_resultP18wifi_scan_result_t "bk_wifi_scan_free_result") 释放申请扫描结果内存

<a id="id24"></a>

### **Armino Wi-Fi 扫描类型**

Beken Wi-Fi 驱动程序支持在任意模式下进行扫描

| **扫描类型** | **描述** |
| --- | --- |
| 主动扫描 | 通过发送probe request进行扫描，默认为主动扫描 |
| 被动扫描 | 通过被动等待接收beacon而不发送probe request进行扫描 |
| 全信道扫描 | 扫描所有信道 |

<a id="id25"></a>

### **Armino Wi-Fi 扫描配置**

扫描信息通过函数 [`bk_wifi_scan_start()`](../../api-reference/wifi/bk_wifi.md#_CPPv418bk_wifi_scan_startPK18wifi_scan_config_t "bk_wifi_scan_start") 配置，当前仅支持配置 **SSID** ，其余信息保持默认配置，暂不开放修改。下表详细描述了 `wifi_scan_config_t` 各字段信息

| **字段** | **描述** |
| --- | --- |
| SSID | 如果该字段不为NULL，则仅可扫描到具有相同SSID的AP |

调用函数 [`bk_wifi_scan_start()`](../../api-reference/wifi/bk_wifi.md#_CPPv418bk_wifi_scan_startPK18wifi_scan_config_t "bk_wifi_scan_start") 开启扫描的默认配置信息如下：

| **默认配置** |
| --- |
| 全信道主动扫描 |
| 不忽略隐藏SSID的AP |
| 存在多个相同SSID AP，则会扫描到多个SSID AP |

<a id="id26"></a>

### **Armino Wi-Fi 全信道主动扫描过程**

扫描过程可以分为三个阶段：扫描配置、Wi-Fi 驱动程序内部扫描、扫描完成事件处理，可以通过下图展示：

<a id="id54"></a>
![../../_images/all_ch_scan.jpg](../../../../_assets/4825d2669cf5f809ca2a-all_ch_scan.jpg)


Armino 全信道主动扫描流程

<a id="id27"></a>

#### **扫描配置阶段**

调用函数 [`bk_wifi_set_country()`](../../api-reference/wifi/bk_wifi.md#_CPPv419bk_wifi_set_countryPK14wifi_country_t "bk_wifi_set_country") 配置国家/地区信息，请参阅 [Armino Wi-Fi 国家/地区代码](#id44) 。该过程可选，如果不调用，则使用默认国家/地区信息，当前默认为 CN。函数 [`bk_wifi_scan_start()`](../../api-reference/wifi/bk_wifi.md#_CPPv418bk_wifi_scan_startPK18wifi_scan_config_t "bk_wifi_scan_start") 配置扫描信息可以参考 [Armino Wi-Fi 扫描配置](#id25)

<a id="id28"></a>

#### **Wi-Fi 驱动程序内部扫描阶段**

Armino Wi-Fi 驱动程序顺序执行扫描，依次从信道 1 切换到信道 N，信道 N 的具体数值由配置的国家/地区决定

<a id="id29"></a>

#### **扫描完成后事件处理阶段**

当所有信道扫描全部完成后，将产生 [EVENT\_WIFI\_SCAN\_DONE](#event-wifi-scan-done) 事件，此后应用程序可以调用 [`bk_wifi_scan_get_result()`](../../api-reference/wifi/bk_wifi.md#_CPPv423bk_wifi_scan_get_resultP18wifi_scan_result_t "bk_wifi_scan_get_result") 获取扫描结果，通过 [`bk_wifi_scan_dump_result()`](../../api-reference/wifi/bk_wifi.md#_CPPv424bk_wifi_scan_dump_resultPK18wifi_scan_result_t "bk_wifi_scan_dump_result") 打印扫描结果，最后再通过 [`bk_wifi_scan_free_result()`](../../api-reference/wifi/bk_wifi.md#_CPPv424bk_wifi_scan_free_resultP18wifi_scan_result_t "bk_wifi_scan_free_result") 释放扫描结果

<a id="id30"></a>

## **Armino Wi-Fi Station 连接场景**

该场景仅针对在扫描阶段只找到一个目标 AP 的情况，**应用程序不用关注该连接过程，供感兴趣客户了解**

<a id="id55"></a>
![../../_images/sta_connect_procedure.png](../../../../_assets/80ab3e476c5ff665fd71-sta_connect_procedure.png)


Armion Wi-Fi Station 连接场景示例

<a id="id31"></a>

### **扫描阶段**

> - 1.1：Wi-Fi 驱动程序开始在 “Wi-Fi 连接”模式下扫描，详情参考\`\`
> - 1.2：如果未找到目标 AP，将产生 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected) 事件，且原因码为 `WIFI_REASON_NO_AP_FOUND`。请参考
>   [Armino Wi-Fi 原因代码](#id35)

<a id="id32"></a>

### **认证阶段**

> - 2.1：发送认证请求数据包并开启认证计时器
> - 2.2：如果在认证计时器超时之前未接收到认证响应数据包，将产生 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected) 事件，原因码为 `WIFI_REASON_AUTH_FAIL`。详情请参考 [Armino Wi-Fi 原因代码](#id35)
> - 2.3：接收到认证响应数据包，认证计时器取消
> - 2.4：AP 在响应中拒绝认证并发送 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected) 事件，原因码为 `WIFI_REASON_AUTH_FAIL` 或者 AP 指定的其他原因。详情请参考 [Armino Wi-Fi 原因代码](#id35)

<a id="id33"></a>

### **关联阶段**

> - 3.1：发送关联请求并开启关联计时器
> - 3.2：如果在关联计时器超时之前未收到关联响应，将产生 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected) 事件，原因码为 `WIFI_REASON_ASSOC_FAIL`，详情请参考 [Armino Wi-Fi 原因代码](#id35)
> - 3.3：接收关联响应，并停止关联计时器
> - 3.4：AP 在响应中拒绝关联并发送 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected) 事件，原因代码将在关联响应中指定。请参考 [Armino Wi-Fi 原因代码](#id35)

<a id="id34"></a>

### **四次握手阶段**

> - 4.1：开启握手定时器，定时器超时前未收到 AP 发送的 1/4 EAPOL 帧，将产生 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected) 事件，原因码为 `WIFI_REASON_HANDSHAKE_TIMEOUT`。详情请参考 [Armino Wi-Fi 原因代码](#id35)
> - 4.2：接收到 AP 发送的 1/4 EAPOL 帧
> - 4.3：station 回复 2/4 EAPOL 帧
> - 4.4：如果在握手定时器超时前未收到 AP 发送的 3/4 EAPOL 帧，将产生 [EVENT\_WIFI\_STA\_DISCONNECTED](#event-wifi-sta-disconnected) 事件，原因码为 `WIFI_REASON_HANDSHAKE_TIMEOUT`。详情请参考 [Armino Wi-Fi 原因代码](#id35)
> - 4.5：接收到 3/4 EAPOL 帧
> - 4.6：station 回复 4/4 EAPOL帧
> - 4.7：station 发送 [EVENT\_WIFI\_STA\_CONNECTED](#event-wifi-sta-connected) 事件

<a id="id35"></a>

### **Armino Wi-Fi 原因代码**

下表展示了 Armino SDK 中定义的 Wi-Fi 原因代码，第一列为 wifi\_types.h 中定义的名称（默认缺省 WIFI\_REASON），第二列为对应数值，该数值可以参考 IEEE 802.11-2020 中的标准数值，第三列为原因描述

| **原因代码** | **数值** | **描述** |
| --- | --- | --- |
| UNSPECIFIED | 1 | 未特定原因 |
| PREV\_AUTH\_NOT\_VALID | 2 | 先前的身份验证不再有效 |
| DEAUTH\_LEAVING | 3 | 发送 STA 离开（或者已经离开）ESS 而被取消身份认证 |
| DISASSOC\_DUE\_TO\_INACTIVITY | 4 | 由于不活动而解除关联 |
| DISASSOC\_AP\_BUSY | 5 | 因为 AP 无法处理所有当前关联的 STA |
| CLASS2\_FRAME\_FROM\_NONAUTH\_STA | 6 | 从未经验证的 STA 接收到的2类帧 |
| CLASS3\_FRAME\_FROM\_NONASSOC\_STA | 7 | 从非关联 STA 接收的3类帧 |
| DISASSOC\_STA\_HAS\_LEFT | 8 | 由于发送 STA 离开（或者已经离开）BSS 而解除关联 |
| STA\_REQ\_ASSOC\_WITHOUT\_AUTH | 9 | 请求（重新）关联的 STA 未通过响应 STA 的身份验证 |
| PWR\_CAPABILITY\_NOT\_VALID | 10 | 由于电源能力元素中的信息不可接受而解除关联 |
| SUPPORTED\_CHANNEL\_NOT\_VALID | 11 | “支持的信道”元素中的信息不可接受而解除关联 |
| BSS\_TRANSITION\_DISASSOC | 12 | 由于 BSS 过渡管理而解除关联 |
| INVALID\_IE | 13 | 无效信息元素 |
| MICHAEL\_MIC\_FAILURE | 14 | 信息完整性代码（MIC）故障 |
| 4WAY\_HANDSHAKE\_TIMEOUT | 15 | 四次握手超时 |
| GROUP\_KEY\_UPDATE\_TIMEOUT | 16 | 组密钥更新超时 |
| IE\_IN\_4WAY\_DIFFERS | 17 | 与（重新）关联请求/探测响应/信标帧不同的4次握手 中的信息元素 |
| GROUP\_CIPHER\_NOT\_VALID | 18 | 无效的组密码 |
| PAIRWISE\_CIPHER\_NOT\_VALID | 19 | 无效的成对密码 |
| AKMP\_NOT\_VALID | 20 | 无效 AKMP |
| UNSUPPORTED\_RSN\_IE\_VERSION | 21 | 不支持的 RSN 信息元素功能 |
| INVALID\_RSN\_IE\_CAPAB | 22 | 无效的 RSN 信息元素功能 |
| IEEE\_802\_1X\_AUTH\_FAILED | 23 | IEEE 802.1x 身份验证失败 |
| CIPHER\_SUITE\_REJECTED | 24 | 由于安全策略，密码套件被拒绝 |
| TDLS\_TEARDOWN\_UNREACHABLE | 25 | TDLS 直连无法到达对端，TDLS 直连断开 |
| TDLS\_TEARDOWN\_UNSPECIFIED | 26 | 未知原因的 TDLS 直连断开 |
| SSP\_REQUESTED\_DISASSOC | 27 | 由于会话被 SSP 请求中断而取消关联 |
| NO\_SSP\_ROAMING\_AGREEMENT | 28 | 由于缺少 SSP 漫游协议而取消关联 |
| BAD\_CIPHER\_OR\_AKM | 29 | 因为 SSP 密码套件或者 AKM 的需求，请求服务被拒 |
| NOT\_AUTHORIZED\_THIS\_LOCATION | 30 | 请求的服务在此位置未得到授权 |
| SERVICE\_CHANGE\_PRECLUDES\_TS | 31 | TS 被删除，原因是 BSS 服务特性或者运行模式改变 导致 Qos AP 缺少足够的带宽供 Qos STA |
| UNSPECIFIED\_QOS\_REASON | 32 | 未指定的 Qos 原因 |
| NOT\_ENOUGH\_BANDWIDTH | 33 | 因为 Qos AP 没有足够的带宽给 Qos STA 而取消关联 |
| DISASSOC\_LOW\_ACK | 34 | 由于大量的帧需要被确认但是没有确认，因为 AP 未 回复或者糟糕的信道条件导致关联取消 |
| EXCEEDED\_TXOP | 35 | 因为 STA 传输超过了 TXOPs 的限制而取消关联 |
| STA\_LEAVING | 36 | 请求 STA 正在离开 BSS 或者重启 |
| END\_TS\_BA\_DLS | 37 | 请求 STA 不再使用该流或者会话 |
| UNKNOWN\_TS\_BA | 38 | 请求 STA 使用一种尚未完成的机制接收帧 |
| TIMEOUT | 39 | 对端 STA 请求超时 |
| Reserved | 40-45 | 保留 |
| AUTHORIZED\_ACCESS\_LIMIT\_REACHED | 46 | 在 Disassociation 帧中：已达到授权访问限制 |
| EXTERNAL\_SERVICE\_REQUIREMENTS | 47 | 在 Disassociation 帧中：外部服务需求 |
| INVALID\_PMKID | 49 | 无效的成对主密钥标识符（PMKID） |
| BEACON\_LOST | 256 | 博通集成特有的 Wi-Fi 原因代码：连续丢失 N 个 信标 |
| NO\_AP\_FOUND | 257 | 博通集成特有的 Wi-Fi 原因代码：未扫描到目标 AP |
| WRONG\_PASSWORD | 258 | 博通集成特有的 Wi-Fi 原因代码：密码错误 一般密码输错，或者四次握手过程中丢包 |
| DISCONNECT\_BY\_APP | 259 | 博通集成特有的 Wi-Fi 原因代码：应用层主动断开 |
| DHCP\_TIMEOUT | 260 | 博通集成特有的 Wi-Fi 原因代码：DHCP 超时（20s） |

<a id="id36"></a>

### **密码相关 Wi-Fi 原因代码**

下表单独罗列了与 **密码错误** 有关的 Wi-Fi 原因代码，方便客户快速检索

| **原因代码** | **数值** | **描述** |
| --- | --- | --- |
| 4WAY\_HANDSHAKE\_TIMEOUT | 15 | 四次握手超时 |
| GROUP\_KEY\_UPDATE\_TIMEOUT | 16 | 组密钥更新超时 |
| GROUP\_CIPHER\_NOT\_VALID | 18 | 无效的组密码 |
| IEEE\_802\_1X\_AUTH\_FAILED | 23 | IEEE 802.1x 身份验证失败 |
| WRONG\_PASSWORD | 258 | 博通集成特有的 Wi-Fi 原因代码：密码错误 一般密码输错，或者四次握手过程中丢包 |

<a id="id37"></a>

### **信号强度相关 Wi-Fi 原因代码**

下表单独罗列了与 **信号强度** 有关的 Wi-Fi 原因代码，方便客户快速检索

| **原因代码** | **数值** | **描述** |
| --- | --- | --- |
| BEACON\_LOST | 256 | 博通集成特有的 Wi-Fi 原因代码：连续丢失 N 个 信标 |
| NO\_AP\_FOUND | 257 | 博通集成特有的 Wi-Fi 原因代码：未扫描到目标 AP |
| DHCP\_TIMEOUT | 260 | 博通集成特有的 Wi-Fi 原因代码：DHCP 超时（20s） |

<a id="armino-wi-fi-beacon"></a>

## Armino Wi-Fi Beacon 超时

<a id="id38"></a>

## **Armino Wi-Fi 配置**

一般情况下，客户需自己维护 Armino Wi-Fi 驱动程序的配置。Armino Wi-Fi 驱动程序提供一套默认的配置，供客户学习 Demo 时使用，分别为 `WIFI_DEFAULT_STA_CONFIG` 和 `WIFI_DEFAULT_AP_CONFIG`，具体可以参考 [wifi\_types.h](https://gitlab.bekencorp.com/wifi/armino/-/blob/main/include/modules/wifi_types.h)

<a id="id40"></a>

### **Armino Wi-Fi 模式**

| **模式** | **描述** |
| --- | --- |
| CONFIG\_ROLE\_AP | AP 模式：在此模式下，[`bk_wifi_ap_set_config()`](../../api-reference/wifi/bk_wifi.md#_CPPv421bk_wifi_ap_set_configPK16wifi_ap_config_t "bk_wifi_ap_set_config") 将初始化 AP 的 相关配置，如 SSID、Password、加密方式等； 然后调用 [`bk_wifi_ap_start()`](../../api-reference/wifi/bk_wifi.md#_CPPv416bk_wifi_ap_startv "bk_wifi_ap_start") 开启 AP 准备收发 Wi-Fi 数据 |
| CONFIG\_ROLE\_STA | station 模式: 详情可以参考 [Armino Wi-Fi station 一般情况](#armino-wi-fi-station) |

<a id="armino-station"></a>

### **Armino Station 基本配置**

客户应用程序通过调用 API [`bk_wifi_sta_set_config()`](../../api-reference/wifi/bk_wifi.md#_CPPv422bk_wifi_sta_set_configPK17wifi_sta_config_t "bk_wifi_sta_set_config") 来配置 Armino Wi-Fi station，下面罗列一些常见的参数。
这些参数的定义请参阅 [wifi\_types.h](https://gitlab.bekencorp.com/wifi/armino/-/blob/main/include/modules/wifi_types.h)

| **字段** | **描述** |
| --- | --- |
| ssid | station 连接的目标 AP 名称 |
| bssid | 目标 AP 的 MAC 地址，当同一个 AP 由多个 BSSID 组成时可以用此来区分 |
| channel | 扫描信道，设置为 0 代表全信道扫描；1-14 代表指定信道扫描 |
| security | 目标 AP 的加密方式，如 WPA、WPA2、WPA3 等 |
| password | 目标 AP 的密码 |

<a id="armino-ap"></a>

### **Armino AP 基本配置**

客户应用程序在开启 AP 模式前，需调用函数 [`bk_wifi_ap_set_config()`](../../api-reference/wifi/bk_wifi.md#_CPPv421bk_wifi_ap_set_configPK16wifi_ap_config_t "bk_wifi_ap_set_config") 来配置 AP 的基本参数，下表罗列了一些常见的参数
您也可以参阅 [wifi\_types.h](https://gitlab.bekencorp.com/wifi/armino/-/blob/main/include/modules/wifi_types.h)

| **字段** | **描述** |
| --- | --- |
| ssid | BEKEN AP 的名称 |
| password | BEKEN AP 的密码，不填表示 AP 不加密 |
| channel | BEKEN AP 的信道，默认信道 11 |
| security | BEKEN AP 的加密方式，如WPA、WPA2、WPA3等 |
| hidden | BEKEN AP 是否为隐藏热点，1 表示不广播 SSID，否则广播 |
| max\_con | BEKEN AP 支持的最大接入 station 数量，默认为 2 |

<a id="id43"></a>

### Armino Wi-Fi 协议模式

<a id="id44"></a>

### Armino Wi-Fi 国家/地区代码

目前国家/地区代码采用默认 CN，客户无需手动修改

<a id="id45"></a>

## **Wi-Fi 分片**

支持 Wi-Fi 接收分片，但不支持 Wi-Fi 发送分片

<a id="id46"></a>

## **Armino Wi-Fi 缓冲区使用情况**

<a id="wi-filwip"></a>

## Wi-Fi缓冲区内存和LwIP缓冲区内存介绍

- Wi-Fi内存块使用情况：主要为硬件接收缓冲区，软件发送描述符。硬件接收缓冲区为芯片硬件侧设计，默认配置大小，软件侧不可进行更改。 软件发送描述符所使用内存、SKB内存块均通过 **动态** 方式，从 SRAM 内申请使用
- LwIP内存块使用：LwIP 内存属于软件侧可配，通过宏定义的形式从 SRAM HEAP 中 **动态** 取出一定大小的 MEM 供 LwIP 使用

<a id="lwip-wi-fi"></a>

## LwIP/Wi-Fi 缓冲区内存配置的重要性

为了获得一个具有强健、高性能的系统，我们需要非常谨慎地考虑内存的使用或配置情况，因为：

- 鉴于 Armino 上整体内存有限，因此系统正常运行的情况下，Wi-Fi 与 LwIP 侧不可无限的申请内存
- 为获取 Wi-Fi 更好、更优的性能，LwIP 驱动程序中默认的TRX内存使用方式是按比例进行动态配置的,以达到Mem最高使用率，缓解TX或者RX时Mem占用紧张问题
- Wi-Fi 的吞吐量很大程度上取决于与内存相关的配置，如 TCP 窗口大小、LwIP Wi-Fi 接收/发送数据缓冲区数量等
- Armino LwIP 中可能使用的总内存峰值取决于场景需求等因素，例如极限吞吐量的获取、应用程序可能拥有的最大 TCP/UDP 连接、中继等场景
- 在考虑内存配置时，应用程序所需的总内存也是一个重要因素

由于上述原因，不存在一个适合所有应用程序的参数配置。相反，我们必须兼顾到为每个不同的应用程序考虑不同的内存配置。

<a id="armino"></a>

## Armino 数据流与内存使用模式

<a id="id56"></a>
![wifi_data_flow](../../../../_assets/7e6f9085077b3501dfe3-wifi_data_flow.png)


Armino 数据路径

Armino 数据流通路大概分为三层，分别为应用层、Wi-Fi层和硬件层,其中 WIFI 层包括 LwIP 层与 MAC 层以及相关接口层。

- RX 方向:数据在接收过程中，硬件将接收到的数据包传送到 Wi-Fi 的接收数据缓冲区、LwIP 的接收数据缓冲区进行相关协议处理，最后上传到应用层。Wi-Fi 的接收数据缓冲区和 LwIP 的接收数据缓冲区默认共享同一个缓冲区。Wi-Fi 的接收数据缓冲区和 LwIP 的接收数据缓冲区的大小都是从 SRAM HEAP 中申请而来。LwIP 的接收数据缓冲区的大小（LWIP\_MEM\_SIZE)可以针对不同场景下的需求进行配置
- TX 方向:数据在发送过程中，应用程序首先将要发送的消息通过LWIP数据接口将数据拷贝到LWIP的MEM(已动态申请的内存)中，进行 TCP/IP 封装，然后将消息发送到 Wi-Fi 层的发送数据缓冲区进行 MAC 封装处理，最后等待发送。为节省SRAM HEAP空间，Armino 在上层应用中数据传输拷贝使的是 PSRAM 空间，同时缓解了 SRAM 内存压力且不会减少应用程序的可用内存

<a id="id47"></a>

## 如何提升 Armino Wi-Fi 性能

Armino Wi-Fi 的性能受诸多参数的影响，各配置参数之间存在关联并相互制约。如果配置参数合理且最优，不仅可以提高性能，还可以增加应用程序的可用内存，提高稳定性。

在本节中，我们将简单介绍 Wi-Fi/LwIP 协议栈的工作模式，并说明各个参数的作用。我们将推荐相应的参数配置，您可以根据使用的场景从而选择最合适的配置，适当调节上述各层中 MEM 大小或数量，可以提高 Wi-Fi 性能。下面我们将介绍您需要配置的参数。

<a id="rx"></a>

### **接收数据方向(RX)相关参数：**

<a id="config-lwip-mem-max-rx-size"></a>

#### CONFIG\_LWIP\_MEM\_MAX\_RX\_SIZE:

该参数表示 LwIP 层配置接收数据缓冲区的大小。提高该参数可以增强数据包的接收性能。该参数需要与mac层处理接收数据缓冲区大小相匹配。该参数最大不能超过 LWIP\_MEM\_SIZE 的大小，默认配置为（LWIP\_MEM\_SIZE\*3）/4。

<a id="config-lwip-udp-recvmbox-size"></a>

#### CONFIG\_LWIP\_UDP\_RECVMBOX\_SIZE:

该参数表示 UDP RX 时，LwIP 内核会首先将数据包发送到 UDP 接收邮箱，然后应用程序再从邮箱中获取数据包。这意味着 LwIP 可以为每个 UDP 套接字缓存最大 UDP\_RECCVMBOX\_SIZE 数据包，因此所有 UDP 套接字可能缓存的最大 UDP 数据包是 UDP\_RECCVMBOX\_SIZE 与最大 UDP 套接字数量的倍数。换句话说，UDP\_RECVMBOX\_SIZE 越大意味着内存越大。
另一方面，如果接收邮件箱太小，邮件箱可能已满。因此，一般情况下，我们需要确保 UDP 接收信箱足够大，以避免 LwIP 核心与应用程序之间出现丢包现象。

<a id="config-lwip-tcp-wnd"></a>

#### CONFIG\_LWIP\_TCP\_WND:

该参数表示 LwIP 层用于每个 TCP 流的的接收数据缓冲区大小，默认配置为 29200(B) （20 \* default MSS的值），设置较小的默认接收窗口大小可以节省一些内存，但是会大大降低性能。同时，在有多个流的情况下，应相应降低该参数值。

<a id="tx"></a>

### **发送数据方向(TX)相关参数:**

<a id="config-lwip-mem-max-tx-size"></a>

#### CONFIG\_LWIP\_MEM\_MAX\_TX\_SIZE:

该参数表示LwIP 层配置接收数据缓冲区的大小，该参数最大不能超过 LWIP\_MEM\_SIZE 的大小，默认配置为（LWIP\_MEM\_SIZE\*5）/6。如果应该程序将发送大量需要拷贝的数据时，提高该参数可以增强数据包发送的性能。

<a id="config-lwip-tcp-snd-buf"></a>

#### CONFIG\_LWIP\_TCP\_SND\_BUF:

该参数表示 LwIP 层用于每个 TCP 流的的发送数据缓冲区大小。该值必须至少是 MSS 大小的 2 倍， Armino 上默认值是 MSS 大小的 20 倍。设置较小的默认 SND BUF 大小可以节省一些 RAM，但会降低性能。

<a id="trx"></a>

### **接收数据与发送数据方向(TRX)高度相关参数：**

<a id="config-lwip-mem-size"></a>

#### CONFIG\_LWIP\_MEM\_SIZE:

该参数表示 LwIP 层堆内存大小，从系统堆内存中申请。该参数默认配置大小为51200（50K），如果需要发送或接收大量数据，提高该参数可以提高整体吞吐性能。

<a id="config-lwip-tcp-mss"></a>

#### CONFIG\_LWIP\_TCP\_MSS:

该参数表示 TCP 最大报文长度，是 TCP 协议定义的一个选项，MSS（Maximum Segment Size，最大报文长度）选项用于在 TCP 连接建立时，收发双方协商通信时每一个报文段所能承载的最大数据长度。
该参数可以设置得更低以节省 RAM，默认值为 1460 (ipv4)/1440(ipv6)以获得最佳吞吐量。
IPv4 TCP\_MSS 范围： 576 \<\= TCP\_mSS \<\= 1460
IPv6 TCP\_MSS 范围： 1220\<\= TCP\_mSS \<\= 1440

<a id="config-lwip-memp-num-netbuf"></a>

#### CONFIG\_LWIP\_MEMP\_NUM\_NETBUF:

该参数表示 NetBuf 结构体数量。使用 netconn 和 socket 编程时，该值设置太小，可能导致接收数据时分配内存失败，从而不能同时为几个连接的数据收发服务。Armino上最小配置为16，最大为32。这里建议默认配置最大32。

<a id="config-lwip-pbuf-pool-size"></a>

#### CONFIG\_LWIP\_PBUF\_POOL\_SIZE:

该参数表示 pbuf 池中缓冲区的数量，参数可配置，最大配置为20，Armino 上建议默认配置大小为10。

<a id="config-lwip-tcp-snd-queuelen"></a>

#### CONFIG\_LWIP\_TCP\_SND\_QUEUELEN:

该参数表示TCP 发送缓冲空间，该参数限制发送缓冲区中 pbuf 的数量。该参数默认设置40，且至少要等于（2 \* TCP\_SND\_BUF/TCP\_MSS）才能正常工作。

<a id="config-lwip-memp-num-tcp-seg"></a>

#### CONFIG\_LWIP\_MEMP\_NUM\_TCP\_SEG:

该参数表示能够同时在队列里的TCP的网段数量，默认参数设置大小为80，且至少等于（2 \* LWIP\_TCP\_SND\_QUEUELEN）才能正常工作。

<a id="armino-wi-fi-menuconfig"></a>

## **Armino Wi-Fi Menuconfig**

Armino SDK 支持 menuconfig 配置功能编译选项，您也可以直接修改 [bk7259.defconfig](https://gitlab.bekencorp.com/wifi/armino/-/blob/main/middleware/soc/bk7259/bk7259.defconfig) ，两者作用相同。关于 menuconfig 使用

<a id="armino-wi-fi-mac"></a>

## **Armino Wi-Fi MAC 地址配置**

Armino Wi-Fi MAC 地址存在 flash 分区（0x3ff000）的前 6 个字节，涉及三个功能宏，对应的介绍如下表所示。客户根据项目需求，可以在
[bk7259.defconfig](https://gitlab.bekencorp.com/wifi/armino/-/blob/main/middleware/soc/bk7259/bk7259.defconfig) 中进行配置

| **宏定义** | **描述** | **配置** |
| --- | --- | --- |
| CONFIG\_NEW\_MAC\_POLICY | MAC 地址存在 flash 分区(0x3ff000)的前六个字节；如果该地址为空， 在 CONFIG\_RANDOM\_MAC\_ADDR 开启的情况下，随机生成并写入该值， 全擦 flash 会导致 MAC 地址丢失 | y |
| CONFIG\_RANDOM\_MAC\_ADDR | 随机生成 MAC 地址，当 flash 分区(0x3ff000)前六个字节为空时，随 机生成并写入。该 MAC 地址会符合 BEKEN 命令规则，即前三个 字节为 **C8:47:8C** | y |
| CONFIG\_BK\_MAC\_ADDR\_CHECK | 判断设置的 MAC 地址是否符合 BEKEN 命令规则，即前三个字节为 **C8:47:8C**。配置默认打开，如客户使用自己 MAC 地址规则，只需在 bk7259.defconfig 中置为 n | y |

为方便客户了解 Armino Wi-Fi MAC 地址的使用规则，下表中列出了可能的 MAC 地址宏功能组合，针对客户应用中可能遇到的一些问题，客户可以根据自己的产品定义进行相应的宏定义设计。 Armino Wi-Fi MAC 地址命令使用规则请参考 [BK IDK AT Wi-Fi命令](../at/bk_at_cs_wifi.md)。

| 使用示例 | 预期结果 |
| --- | --- |
| CONFIG\_NEW\_MAC\_POLICY \= y  CONFIG\_RANDOM\_MAC\_ADDR \= y  CONFIG\_BK\_MAC\_ADDR\_CHECK \= y | flash 分区(0x3ff000)的前六个字节为空时，首次开机后随机生成并写入。使用 AT\+MAC \= \<MAC\> 修改，需遵循 C8:47:8C 原则 |
| CONFIG\_NEW\_MAC\_POLICY \= y  CONFIG\_RANDOM\_MAC\_ADDR \= y  **CONFIG\_BK\_MAC\_ADDR\_CHECK \= n** | flash 分区(0x3ff000)的前六个字节为空时，首次开机后随机生成并写入。随机地址符合 C8:47:8C 规则，**支持客户定制 MAC 地址，无需遵循 C8:47:8C 规则** |
| CONFIG\_NEW\_MAC\_POLICY \= y  **CONFIG\_RANDOM\_MAC\_ADDR \= n**  **CONFIG\_BK\_MAC\_ADDR\_CHECK \= n** | flash 分区(0x3ff000)的前六个字节为空时，首次开机后使用软件默认 MAC 地址。**支持客户定制 MAC 地址，无需遵循 C8:47:8C 规则** |

<a id="id49"></a>

## **Armino Wi-Fi 故障定位**

无线网络问题，一般需要空口包协助分析，详情请参见 [BEKEN Wi-Fi 抓包指南](bk_wifi_capture.md)
