---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7258/zh_CN/v3.1.1/developer-guide/ethernet/bk_ethernet.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: SMP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 以太网

<a id="id2"></a>

## 概述

BK7258 集成一路 10/100M 以太网 MAC，通过 RMII 接口与外部 PHY 相连，
在 lwIP 协议栈中注册为独立的网络接口。主要参数如下：

| 项目 | 说明 |
| --- | --- |
| MAC 控制器 | Synopsys DWC\_ether\_qos，支持 10/100M |
| 寄存器基址 | 0x460a0000 |
| 接口类型 | RMII，固定不可切换 |
| 数据有效信号 | RXDV（不使用 CRS\_DV） |
| PHY 型号 | SMSC LAN8710 / LAN8720 |
| PHY 地址 | MDIO 自动扫描，典型值为 1 |
| 引脚组 | 两组可选，编译期由 Kconfig 决定 |
| 发送描述符 | 32 个 |
| 接收描述符 | 16 个 |
| 接收缓冲 | 1536 字节 × 24 个，32 字节对齐，位于 SRAM |
| 示例工程 | projects/eth\_example |

以太网驱动位于 `middleware/driver/eth/`，lwIP 移植层位于
`components/lwip_intf_v2_1/lwip-2.1.2/port/ethernetif.c`。
AP 与 CP 两个子系统都包含完整的驱动代码，但同一时刻只能由其中一个子系统使用以太网。

备注

`0x48080000` 在 BK7258 上是 DMA2D 模块的基址，不是以太网。
从其它平台移植寄存器读写脚本时，请先确认基址。

<a id="id3"></a>

## 1 硬件设计

<a id="id4"></a>

### 1.1 参考时钟

RMII 接口需要一路 50MHz 参考时钟（REF\_CLK）。**该时钟由板级硬件提供，软件不负责产生。**

SMSC LAN8710/LAN8720 自带晶振（通常为 25MHz 晶振或 50MHz 有源晶振），
由 PHY 从 REF\_CLK 引脚将 50MHz 输出给 MAC。SoC 侧仅做两件事：

- 将对应引脚复用为 `GPIO_DEV_ENET_REF_CLK`
- 使能 MAC 模块时钟门控 `enet_cken`

因此软件侧不存在时钟方向、PLL 校准值、锁定等待或时序偏移等可配置项。
硬件设计时请确认下列几点：

- PHY 的晶振已正确起振，且频率符合 PHY 数据手册要求
- PHY 的 strap 配置使其在 REF\_CLK 引脚 **输出** 时钟
- REF\_CLK 走线尽量短，必要时加串阻，避免过冲影响 MAC 采样

重要

REF\_CLK 缺失时最典型的现象是 MAC 软复位超时，日志中会打印 `soft reset timeout`。
此时 MDIO 通常仍然正常（MDC 由 MAC 自行产生，不依赖 REF\_CLK），
出现”能读到 PHY、但软复位失败”的组合时，应优先怀疑 REF\_CLK。

<a id="id5"></a>

### 1.2 引脚分配

以太网引脚有两组，由 Kconfig 在编译期二选一，运行时在 `HAL_ETH_MspInit()`
中通过 `gpio_dev_map()` 完成映射。信号与 GPIO 的对应关系固定，工程不能自行调整。

引脚组 0（`CONFIG_ETH_PIN_GROUP0`，默认）：

| 信号 | GPIO |
| --- | --- |
| ENET\_PHY\_INT | GPIO27 |
| ENET\_MDC | GPIO29 |
| ENET\_MDIO | GPIO32 |
| ENET\_RXD0 | GPIO33 |
| ENET\_RXD1 | GPIO34 |
| ENET\_RXDV | GPIO35 |
| ENET\_TXD0 | GPIO36 |
| ENET\_TXD1 | GPIO37 |
| ENET\_TXEN | GPIO38 |
| ENET\_REF\_CLK | GPIO39 |

引脚组 1（`CONFIG_ETH_PIN_GROUP1`）：

| 信号 | GPIO |
| --- | --- |
| ENET\_PHY\_INT | GPIO46 |
| ENET\_MDC | GPIO47 |
| ENET\_MDIO | GPIO48 |
| ENET\_RXD0 | GPIO49 |
| ENET\_RXD1 | GPIO50 |
| ENET\_RXDV | GPIO51 |
| ENET\_TXD0 | GPIO52 |
| ENET\_TXD1 | GPIO53 |
| ENET\_TXEN | GPIO54 |
| ENET\_REF\_CLK | GPIO55 |

两组引脚都与其它外设共享 pad，选择时需要注意冲突：

- 引脚组 0 的第一复用功能是 `JPEG_*`，即 DVP 摄像头接口，同时还与
  TOUCH、SPI0、I2C1、PWM6-11、SLCD 等复用。启用 DVP 摄像头时不能使用该组。
- 引脚组 1 与 LCD 相关功能复用。启用 LCD 时不能使用该组。

备注

以太网引脚不经过工程的 `usr_gpio_cfg.h` 配置表。
`HAL_ETH_MspInit()` 中的映射是硬编码的，若需更换引脚只能修改 `ethernetif.c`。

<a id="id6"></a>

## 2 配置说明

<a id="kconfig"></a>

### 2.1 Kconfig 选项

以太网相关配置项定义在 `middleware/driver/eth/Kconfig`：

| 配置项 | 默认值 | 说明 |
| --- | --- | --- |
| CONFIG\_ETH | n | 以太网总开关 |
| CONFIG\_ETH\_PIN\_GROUP0 | y | 使用引脚组 0（GPIO27、29、32-39），与 DVP 摄像头冲突 |
| CONFIG\_ETH\_PIN\_GROUP1 | n | 使用引脚组 1（GPIO46-55），与 LCD 冲突 |
| CONFIG\_ETH\_DHCP | n | 开启则通过 DHCP 获取 IP，关闭则使用静态 IP |
| CONFIG\_ETH\_CSUM\_OFFLOAD | y | IP/TCP/UDP/ICMP 校验和由硬件计算 |
| CONFIG\_ETH\_PM\_CB\_SUPPORT | n | 低功耗进入/退出回调支持，同时负责 ETH 域上电 |
| CONFIG\_ETH\_PTP | n | IEEE 1588-2008 精确时间同步 |
| CONFIG\_ETH\_VLAN | n | VLAN 支持 |
| CONFIG\_ETH\_TSO | n | TCP 分段卸载 |
| CONFIG\_ETH\_LPI | n | 低功耗空闲。当前硬件不支持，请保持关闭 |
| CONFIG\_ETH\_EEE | n | Wake over LAN |
| CONFIG\_ETH\_REGISTER\_CALLBACKS | n | 使用 HAL 回调注册机制 |
| CONFIG\_PHY\_SMSC | y | SMSC 100M PHY 驱动（LAN8710/LAN8720） |
| CONFIG\_PHY\_MICREL\_KSZ90X1 | n | Micrel 千兆 PHY 驱动 |
| CONFIG\_PHY\_REALTEK | n | Realtek PHY 驱动 |

启用以太网的最小配置如下：

```
CONFIG_ETH=y
CONFIG_ETH_PIN_GROUP0=y
CONFIG_PHY_SMSC=y
CONFIG_ETH_CSUM_OFFLOAD=y
CONFIG_ETH_PM_CB_SUPPORT=y
```

<a id="ip"></a>

### 2.2 IP 地址配置

IP 获取方式由 `CONFIG_ETH_DHCP` 决定，缺省值定义在
`components/lwip_intf_v2_1/lwip-2.1.2/port/net.c` 的 `eth_ip_settings`：

- 开启 `CONFIG_ETH_DHCP`：地址类型为 `ADDR_TYPE_DHCP`，链路 up 后自动发起 DHCP
- 不开启：地址类型为 `ADDR_TYPE_STATIC`，使用结构体中的静态地址

需要修改静态地址时，直接调整 `eth_ip_settings` 中的 `address`、`gw`、
`netmask`、`dns1` 字段，注意这几个字段使用网络字节序。

<a id="id7"></a>

## 3 快速开始

SDK 提供了以太网示例工程 `projects/eth_example`，编译命令如下：

```
make bk7258 PROJECT=eth_example
```

该工程本身不包含以太网业务代码，以太网由 `bk_init()` 自动拉起。
烧录运行后，正常情况下会依次看到 PHY 识别、链路建立与 IP 配置的日志：

```
netif st connected to SMSC LAN8710/LAN8720, mode rmii, phyad 1
ETH link up, speed 100M, Full-duplex
lwip:D(1740):eth ip start
```

拔掉网线时会打印链路断开：

```
lwip:D(872619):ETH link down
lwip:D(872619):eth ip down
```

备注

`eth_example` 当前在 AP 侧启用 `CONFIG_ETH=y`，CP 侧未启用；
且 AP 侧未开启 `CONFIG_ETH_DHCP`，因此默认使用静态 IP。
若需要 DHCP，请在 AP 侧配置中补充 `CONFIG_ETH_DHCP=y`。

<a id="id8"></a>

## 4 驱动实现

<a id="id9"></a>

### 4.1 启动调用链

以太网在系统初始化阶段被同步拉起，完整调用链如下：

```
main()
└─ bk_init()
   └─ app_eth_init()
      └─ net_eth_start()
         ├─ miiphy_init()          MDIO 总线初始化
         ├─ ieee8023_phy_init()    按 Kconfig 注册 PHY 驱动
         ├─ net_ipv4stack_init()   协议栈初始化
         ├─ net_eth_add_netif()    注册 netif，触发硬件初始化
         │  └─ ethernetif_init()
         │     └─ low_level_init()
         │        └─ HAL_ETH_Init()
         │           └─ HAL_ETH_MspInit()
         └─ 创建 eth_link 线程，每 200ms 轮询链路状态
```

链路状态变为 up 后，`eth_link` 线程会调用 `eth_ip_start()` 完成 IP 配置。

备注

`app_eth_init()` 不检查 `net_eth_start()` 的返回值，也没有重试机制。
如果初始化阶段硬件尚未就绪（例如 REF\_CLK 还没有稳定），以太网不会自动恢复，
需要在应用层自行实现重试。

<a id="id10"></a>

### 4.2 初始化流程

`low_level_init()` 的主要步骤：

1. 分配私有数据结构 `eth_mac_priv`
2. 填充 `heth`：MAC 地址、`HAL_ETH_RMII_MODE`、收发描述符表、接收缓冲长度 1536
3. 调用 `HAL_ETH_Init()`，首次调用时触发 `HAL_ETH_MspInit()`
4. 初始化零拷贝接收池 `RX_POOL`
5. 设置 netif 的硬件地址、MTU 与 flags
6. PHY 初始化：分配并注册 MDIO 总线，调用 `phy_connect()` 自动扫描 PHY，
   随后执行 `phy_config()` 与 `phy_startup()`
7. 创建事件队列与 `EthIf` 线程

`HAL_ETH_MspInit()` 按下列顺序完成底层初始化：

1. **引脚复用**：按 Kconfig 选定的引脚组，先 `gpio_dev_unmap()` 解除原有功能，
   再 `gpio_dev_map()` 绑定到 ENET 功能
2. **电源与睡眠投票**（`CONFIG_ETH_PM_CB_SUPPORT`）：给 ETH 域上电，并禁止其进入低功耗
3. **MAC 软复位**：写 `ETH_RESET_CTRL`（位于 `ETH_BASE + 0x802*4`）
4. **使能模块时钟**：置位 `enet_cken`
5. **注册中断**：注册 `INT_SRC_ETH` 的处理函数并使能

重要

`HAL_ETH_MspInit()` 受 `if (heth->gState == HAL_ETH_STATE_RESET)` 保护，
整个运行期最多执行一次。软复位超时后 `gState` 被置为 `HAL_ETH_STATE_ERROR`，
此后再次调用 `HAL_ETH_Init()` 只会重发一次软复位，
**不会重新映射引脚、重新上电或重新使能时钟**。
若需要完整重做硬件初始化，必须先将 `gState` 手动恢复为 `HAL_ETH_STATE_RESET`。

MAC 软复位通过轮询 `DMAMR.SWR` 位自清零来判断完成，
超时时间由 `ETH_SWRESET_TIMEOUT` 定义，为 500ms。该过程依赖有效的 RMII 参考时钟。

<a id="phy"></a>

### 4.3 PHY 管理

驱动使用多 PHY 框架：`CONFIG_ETH=y` 时 `smsc.c`、`realtek.c`、
`micrel_ksz90x1.c` 等都会参与编译，但 `ieee8023_phy_init()`
只注册 Kconfig 中开启的驱动。`phy_connect()` 的 PHY 地址参数传入 -1，
表示扫描 MDIO 地址 0\~31，再按读到的 PHY ID 匹配已注册的驱动。

PHY 复位仅通过 MDIO 软复位实现（写 `BMCR_RESET` 后轮询，上限 500ms），
驱动中没有 GPIO 硬复位逻辑，也没有对应的 Kconfig 选项。
如果硬件设计了 PHY 复位引脚，需要在应用层自行控制。

LAN8710/LAN8720 的 REF\_CLK 方向与 RMII 时序均由硬件 strap 决定，
驱动中没有相关寄存器配置。若 RMII 接口出现时序问题，只能从硬件侧（strap 电阻、
走线长度、串阻）着手。

<a id="id11"></a>

## 5 调试命令

以太网没有专用的 CLI 命令，通用网络命令支持 `eth` 接口：

| 命令 | 说明 |
| --- | --- |
| ip eth | 查看或设置以太网接口的静态 IP |
| ipconfig eth | 同 ip eth |
| mac | 查看或设置以太网 MAC 地址 |
| ping \<ip\> | 连通性测试 |

<a id="id12"></a>

## 6 常见问题

**链路一直不 up，日志出现 soft reset timeout**

MAC 软复位在 500ms 内未完成，几乎可以确定是 RMII 参考时钟缺失。
用示波器测量 REF\_CLK 引脚（引脚组 0 为 GPIO39，引脚组 1 为 GPIO55）
是否有稳定的 50MHz。由于软件不产生该时钟，测不到即为硬件问题：
PHY 晶振未起振、PHY 未上电，或 PHY 的 strap 被配置为期望时钟输入。

**扫描不到 PHY**

检查 MDC/MDIO 两根信号线的引脚复用是否正确、MDIO 是否有上拉电阻，
以及 PHY 地址 strap 的设置。注意 MDIO 不依赖 REF\_CLK，
所以 MDIO 不通与 REF\_CLK 无关，应从 MDIO 自身的连线与上拉排查。

**以太网与摄像头或屏幕不能同时工作**

引脚组 0 与 DVP 摄像头复用同一组 pad，引脚组 1 与 LCD 复用。
请根据实际使用的外设选择另一组引脚，或调整硬件设计。

**链路已 up 但收发不通**

可以逐层读取寄存器缩小范围：先看发送描述符的 OWN 位与写回错误标志，
判断软件是否正确交付；再看 `MTL_TxQ0_Debug` 的队列包计数，
判断帧是否进入 MTL 并被 MAC 取走；再看 `Current_App_TxDesc` 与
`Current_App_RxDesc` 是否推进，判断 DMA 是否在回收描述符。
使用 MMC 统计寄存器前，建议先在已知能正常通信的场景下确认它确实在计数。

**获取不到 IP 地址**

先确认 `CONFIG_ETH_DHCP` 的配置是否符合预期。该选项未开启时使用静态 IP，
不会发出 DHCP 请求。若已开启 DHCP 仍拿不到地址，用 `ip eth` 查看当前接口状态，
并确认链路已经 up。
