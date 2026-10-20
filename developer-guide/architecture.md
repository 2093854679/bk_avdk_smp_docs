---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/architecture/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap-smp-cp"></a>

# AP(SMP)\+CP 架构

<a id="id1"></a>

## **架构概述**

在当前 BK7259 SMP 代码库中，SoC 以四核 AP\+CP 方式使用。
CPU0 与 CPU1 归属 CP 子系统，CPU2 与 CPU3 归属 AP 子系统。
AP 默认以 SMP 方式运行；CP 同样支持 SMP，但可配，工程可按需配置为单核（仅 CPU0）或双核 SMP（CPU0 \+ CPU1，需开启 `CONFIG_SOC_SMP` 与 `CONFIG_FREERTOS_SMP`）。

<a id="id27"></a>
![AP and CP architecture](../../_assets/fe5e02c80f539488ea72-bk7259_arch.png)


AP(SMP)\+CP 架构

如上图所示, AP和CP是独立的两个子系统, 其独立性体现为：

> - CP 代码编译为独立镜像，可运行于 CPU0（单核）或 CPU0/CPU1（SMP），主要承载连接、低功耗控制和系统管理功能
> - AP 代码作为 CPU2 与 CPU3 的独立镜像编译（默认 SMP），主要承载多媒体与面向应用的工作负载

从应用层的视角看, CP上运行Wi-Fi, BLE, 用于低功耗保活的LWIP协议栈, 及必要的外设；AP上运行多媒体模块, 给上层提供的LWIP协议栈, 应用经常使用的外设。
AP和CP之间通过Mailbox\+共享内存通讯。从应用层的视角, AP和CP之间通过虚拟Uart接口通讯。
AP的Log通过MailBox发送到CP从UART0输出。

在当前架构下, 大多数面向客户的应用开发都在 AP 上完成；除非工程显式需要调整 CP 侧逻辑，否则 CP 功能以及 AP/CP 之间的协同通常由底层实现。

从职责边界看，BK7259 SDK 可以按以下方式理解:

```
+-------------------+----------------------------------------------+
| 层次              | 主要职责                                     |
+===================+==============================================+
| Project           | 产品工程、分区、Kconfig、AP/CP 用户入口      |
+-------------------+----------------------------------------------+
| AP components     | 应用服务、多媒体、网络接口、CLI、文件系统    |
+-------------------+----------------------------------------------+
| AP middleware     | AP 侧外设驱动、Mailbox、IPC、SoC HAL         |
+-------------------+----------------------------------------------+
| CP components     | Wi-Fi、BLE、低功耗保活、系统管理、CLI        |
+-------------------+----------------------------------------------+
| CP middleware     | CP 侧外设驱动、Mailbox、IPC、SoC HAL         |
+-------------------+----------------------------------------------+
| properties/tools  | 芯片库、第三方库、构建、分区与打包工具       |
+-------------------+----------------------------------------------+
```

开发时应优先判断修改属于哪一层：

> - 产品业务、UI、音视频流程和大多数应用逻辑放在 `projects` 或 AP 侧组件中
> - 面向 AP 的通用能力抽象放在 `ap/components` 中
> - 片上外设、寄存器、HAL、Mailbox 和 IPC 驱动放在 `ap/middleware` 或 `cp/middleware` 中
> - Wi-Fi/BLE 协议栈、低功耗保活以及系统复位/看门狗等基础能力通常由 CP 侧维护

备注

本文档描述的是当前 BK7259 SMP SDK 的实现边界。实际工程是否启用某个模块，
以工程的 `sdkconfig`、`defconfig` 和 Kconfig 依赖为准。

新架构的SDK组成也采用全新的目录, 具体结构如下:

```
ubuntu240:~/bk_avdk_smp$ tree -L 2
├── ap
│   ├── CMakeLists.txt
│   ├── components
│   ├── docs
│   ├── include
│   ├── Kconfig
│   ├── Makefile
│   ├── middleware
│   ├── properties
│   └── requirements.txt
├── cp
│   ├── CMakeLists.txt
│   ├── components
│   ├── docs
│   ├── include
│   ├── Kconfig
│   ├── Makefile
│   ├── middleware
│   ├── properties
│   └── requirements.txt
├── docs
│   ├── bk7259
│   └── version.json
├── LICENSE
├── Makefile
├── projects
│   ├── app
│   ├── app_ab
│   ├── doorbell
│   ├── lvgl
│   └── test
├── README_CN.md
├── README.md
└── tools
    ├── armino_doc.py
    ├── bk_bootloader_post.py
    ├── bk_smp_auto_partition.py
    ├── bk_smp_package.py
    ├── build_main.mk
    ├── build_tools
    └── env_tools
```

AP和CP代码分别在各自的目录下, 两者间的代码完全独立。工程目录下包含ap\_main文件夹和cp\_main文件夹, 用来分别存放客户对于AP和CP的需求代码。

其中常用目录职责如下：

> - `projects`：产品工程入口。典型工程会包含 `ap`、`cp` 子目录以及分区、配置文件。
>   例如 `projects/app/ap/ap_main.c` 是 AP 侧应用入口示例。
> - `ap/components`：AP 侧组件。包含 `bk_init`、`bk_cli`、`bk_wifi`、
>   `bk_bluetooth`、`bk_audio`、`bk_vpu`、`bk_camera`、`bk_display`、
>   `lvgl` 等面向应用或业务能力的模块。
> - `ap/middleware`：AP 侧中间件与驱动。包含 `driver`、`soc`、`arch`、
>   `boards` 等目录，主要承载外设驱动、SoC HAL、Mailbox、IPC、多核控制等底层能力。
> - `cp/components`：CP 侧组件。主要承载连接、低功耗、控制与系统服务能力。
> - `cp/middleware`：CP 侧中间件与驱动。与 AP 侧结构类似，但面向 CPU0/CPU1 所在子系统。
> - `properties`：芯片库、协议栈或预编译模块等属性化组件。
> - `tools`：构建、分区、打包、dump 分析和环境辅助工具。

基于以上的目录结构, 构建过程如下:

> - 先根据Project配置的分区表, 自动分区工具生成对应的分区表及相关文件
> - 然后编译BK7259 AP系统, 生成SMP镜像
> - 然后编译BK7259 CP系统, 生成bootloader和cp.bin镜像
> - 将bootloader.bin,cp.bin,ap.bin根据分区表打包成all-app.bin

<a id="id2"></a>

## **启动流程**

BK7259 采用 AP/CP 独立镜像启动：CP 先完成自身初始化，再由 `user_app` 线程拉起 AP；
AP/CP 各自在 SMP 子系统内由 primary core 完成基础资源初始化后，再释放 secondary core 加入调度。

完整启动链路（复位、调度启动、CP 拉起 AP、启动完成同步、关键代码路径等）请参阅：

[系统启动流程（CP \+ AP）](system_boot.md)

重要

`projects/app/ap/ap_main.c` 中的业务入口函数是标准 `main()`。
文档或代码注释中如果提到 `app_main`，通常需要结合上下文区分是文件名、
RTOS 创建的 `main` 任务，还是其他工程中的用户入口函数。

<a id="id3"></a>

## **构建与镜像**

BK7259 工程由顶层工程配置驱动 AP/CP 两套镜像构建。以 `projects/app` 为例：

> - `projects/app/CMakeLists.txt` 引入 Armino 工程构建框架并声明工程名
> - `projects/app/ap/CMakeLists.txt` 注册 AP 侧应用源文件和组件依赖
> - 工程配置决定 AP/CP 的 Kconfig、分区表、RAM region 和最终镜像布局

构建产物的关系如下:

```
Project config
    -> partition and RAM region generation
    -> AP image: ap.bin
    -> CP image: cp.bin
    -> bootloader.bin
    -> package: all-app.bin
```

AP 与 CP 分别链接各自目录下的组件和中间件。跨子系统能力不通过直接链接对方代码实现，
而是通过 Mailbox、共享内存、逻辑 IPC 或虚拟 UART 等机制交互。

<a id="id4"></a>

## **核间通信设计**

BK7259 AP 与 CP 的通信由多层机制组成。不同层服务于不同抽象级别：

> - 硬件 Mailbox：负责 CPU 间中断通知和少量参数传递
> - Mailbox adapter：完成硬件驱动适配、共享内存可见性处理、回调分发
> - Mailbox channel：在基础 Mailbox 之上提供逻辑通道、ACK 和通道状态管理
> - MB IPC：提供端口、socket、同步/异步发送、路由和数据完整性检查
> - BK IPC API：面向应用或模块的逻辑 IPC 注册、发送和回调接口
> - 虚拟 UART：面向应用调试或简单命令交互的串口式抽象

基础 Mailbox 数据路径如下:

```
sender
    -> prepare mailbox_data_t in shared memory
    -> publish shared-memory metadata with ordering
    -> mbox0_drv_send_message()
    -> remote mailbox ISR
    -> read shared-memory metadata with ordering
    -> dispatch registered callback
```

AP 侧相关代码路径：

> - `ap/middleware/driver/mailbox/mbox0_adapter.c`：基础 Mailbox 适配层
> - `ap/middleware/driver/mailbox/mailbox_channel.c`：逻辑 Mailbox channel
> - `ap/middleware/driver/mailbox/mb_ipc.c`：端口化 IPC 路由与 socket 管理
> - `ap/middleware/driver/mailbox/bk_api_ipc.c`：面向业务模块的 IPC API

CP 侧存在对应实现，路径位于 `cp/middleware/driver/mailbox`。

典型 IPC 使用方式请参考 [多核通讯-IPC通讯接口](multicore_communication/bk_api_ipc.md)。
AP/CP 虚拟 UART 请参考多核通讯章节中的虚拟 UART 文档。

备注

Mailbox 传递的数据应优先放在 non-cacheable 共享内存中。当前推荐配置下，普通共享
buffer 不需要业务层手动 clean/invalidate；若工程自行引入 cacheable 共享 buffer，
必须结合访问 master 和生命周期单独设计一致性处理。

<a id="id5"></a>

## **关键模块职责**

<a id="wi-fi"></a>

### Wi-Fi 与网络

CP 侧主要承载 Wi-Fi/BLE 连接、低功耗保活和必要协议栈。AP 侧通过
`ap/components/bk_wifi`、`ap/components/bk_wifi_driver`、`bk_netif` 等
模块提供应用可见接口、网络设备抽象和控制面。

在 `CONFIG_WIFI_VNET_CONTROLLER` 等配置启用时，AP 侧 `bk_wifi_init()`
会进一步初始化 Wi-Fi driver。最终是否启用 Wi-Fi 仍取决于工程配置。

<a id="phy-notify"></a>

### PHY notify

`ap/components/bk_wifi/src/phy_notify.c` 用于在 PHY 操作前后通知相关核或模块。
启用 `CONFIG_PHY_MB` 时，代码通过 `MB_CHNL_PHY` 发送 `IPC_PHY_OP_START`
和 `IPC_PHY_OP_END`，并等待 ACK。该机制用于避免多核并发访问 PHY 相关资源。

<a id="bluetooth"></a>

### Bluetooth

Bluetooth 在 CP 侧承担控制器、协议栈或底层连接相关职责；AP 侧可根据
`CONFIG_BLUETOOTH_AP`、`CONFIG_BLUETOOTH` 等配置初始化蓝牙接口或 IPC client。
应用开发时应优先使用组件暴露的 API，不应直接跨目录调用 CP 内部实现。

<a id="id6"></a>

### 音视频与多媒体

AP 侧是多媒体和面向应用负载的主要承载域。典型模块包括：

> - `bk_camera`、`bk_display`、`bk_dvp`、`bk_uvc`：采集和显示设备
> - `bk_vpu`、`bk_video_player`、`bk_video_pipeline`：视频编解码和播放管线
> - `bk_audio`、`audio_play`、`audio_record`：音频采集、播放和算法
> - `lvgl`、`bk_gpu`：UI 和图形加速

多媒体链路通常对内存带宽、PSRAM、DMA 和中断路由敏感。新增功能时应同步检查
任务优先级、buffer 所在内存、cache 同步和中断 affinity。

<a id="pm"></a>

### PM 与低功耗

低功耗策略以 CP 侧为主，AP 侧通过 mailbox、心跳和 PM client/server 机制与 CP
协同。AP 侧启动完成后会根据 `CONFIG_MAILBOX` 等配置向 CP 响应启动状态。
如果工程需要 AP 掉电保活、PSRAM 掉电或连接保活，应优先参考对应示例工程和
PM 模块接口，不建议直接绕过 CP 侧控制逻辑。

<a id="id7"></a>

## **系统控制**

<a id="id8"></a>

### **资源划分**

BK7259 同时包含每核本地 TCM 资源以及 AP/CP 可见的共享 SRAM、
PSRAM 与 Flash 资源。

当前的SDK中已经按照资源的需求划分好了CP与AP的内存。

如果上层应用需要重新划分资源, 可以在工程中修改ram\_regions.csv配置。

具体请参考 [RAM资源分区配置](config_tools/bk_config_ram_regions.md#bk-config-ram-regions) .

考虑到sram资源有限, 为了系统资源的充分利用。新架构中sram的布局也进行了调整。

当前sram内存布局如下(以doorbell工程为例):

```
0x28000000  CP_RAM
0x2805F000  SWAP
0x28100000  AP_HSRAM_HEAP
0x28180000  AP_RAM
```

备注

不建议随意修改该布局；如果工程确实需要调整容量，应通过 RAM
region 生成流程来修改 AP 与 CP 的 SRAM 归属。

对于 PSRAM 的使用约束与 CP/AP 侧差异，见 [内存资源](memory_resource.md)。

<a id="id9"></a>

### **系统复位**

架构采用的是全复位方案, 即CP或AP系统出现异常时, 整个系统全部复位。

也支持上层应用主动调用bk\_reboot接口进行复位。

<a id="id10"></a>

### **系统看门狗**

BK7259 硬件看门狗分为两类职责不同的机制：

- **AON WDT** （系统级）：由 CP 侧统一配置与喂狗；超时直接触发系统复位。
- **WWDT** （核级）：AP/CP 各核各自拥有 WWDT，超时时进入该核 **NMI** （`soc_nmi_handler` → `RESET_SOURCE_NMI_WDT`），用于单核卡死检测与 dump，不等同于 AON 的系统级硬复位。

AP 侧不配置、不喂 AON WDT；AP 是否存活由 AP 向 CP 发送核间心跳、由 CP 侧监测确认（见下一节）。

在 `CONFIG_WDT_EN` 打开后，CP 侧 AON WDT 与 TASK\_WDT 配置如下（WWDT 在 AP/CP 两侧均可独立使能）：

| 类型 / 宏 | 默认（defconfig） | 说明 |
| --- | --- | --- |
| AON WDT | — | 常供电 AON 域中断看门狗，用于系统级超时复位 |
| `CONFIG_INT_WDT` | y | 使能 AON WDT（Kconfig 称 AON\_WDT Interrupt Watchdog） |
| `CONFIG_SUPPORT_AON_WDT` | y | 使用 AON 看门狗后端 |
| `CONFIG_INT_WDT_PERIOD_MS` | 8000 | AON WDT 超时周期（ms） |
| WWDT | — | 各核独立的窗口看门狗；超时进 NMI。CP 启动核在 `entry_main` 中 `bk_wwdt_start`；从核由 systick 路径自动拉起/喂狗 |
| `CONFIG_SUPPORT_WWDT` | y（CP/AP） | 使能本侧 WWDT |
| `CONFIG_INT_WWDT_PERIOD_MS` | 2000（Kconfig 默认） | WWDT 周期（ms） |
| TASK\_WDT（可选） | — | 软件任务看门狗，监测 CP 任务是否长时间未调度 |
| `CONFIG_TASK_WDT` | y | 使能任务看门狗 |
| `CONFIG_TASK_WDT_PERIOD_MS` | 60000 | 任务看门狗周期（ms） |

喂狗与停狗分布在 CP 启动、低功耗、PHY、PM 等路径（如 `cp/components/bk_startup/system_main.c`、`cp/components/bk_pm/`）。
AON WDT 与 TASK\_WDT 超时可触发系统复位；WWDT 超时先进入 NMI，由异常/dump 流程处理。

AP 侧同样可使能 ``` CONFIG_SUPPORT_WWDT``（defconfig 默认 y），在 ``ap/components/bk_startup/system_main.c ``` 的 `entry_main` 中拉起启动核 WWDT，各从核在运行后自动启用本核 WWDT。AP 侧可选 `CONFIG_TASK_WDT` 做本侧任务调度监测，与 WWDT/AON WDT 相互独立。

<a id="id11"></a>

### **核间心跳**

除硬件看门狗外，AP/CP 通过双向核间心跳互相确认对端是否存活。两条链路相互独立，宏开关也不同。

<a id="ap-cp-ap"></a>

#### AP → CP：确认 AP 是否活着

这是产品默认开启的主链路：由 AP 定时发送心跳，CP 接收并判断是否超时。

> - 总开关：``` CONFIG_SLAVE_HEART_BEAT``（依赖 ``CONFIG_MAILBOX ```；AP/CP 需同时使能）
> - AP 发送：``` ap/middleware/driver/mailbox/mb_ipc_heartbeat.c``（``SLAVE_HB_TASK ```）
> - CP 监测：``` cp/middleware/driver/mailbox/mb_ipc_heartbeat.c``（``MASTER_HB_TASK ```）
> - AP 默认每 2 s（`MB_IPC_HEARTBEAT_TIME`）发送一次；启动时先发 power-up 通知
> - CP 超时未收到则 `BK_ASSERT(false)` 触发系统复位

传输方式（由 `CONFIG_SLAVE_HEART_BEAT_USE_IPI` 选择，依赖 `CONFIG_IPI`）：

| 方式 | 说明 |
| --- | --- |
| Mailbox（`CONFIG_SLAVE_HEART_BEAT_USE_IPI=n`） | AP 调用 ipc\_send\_power\_up / ipc\_send\_heart\_beat，经 Mailbox IPC 通知 CP。BK7259 默认配置 |
| IPI（`CONFIG_SLAVE_HEART_BEAT_USE_IPI=y`） | AP 经 `IPI_DOMAIN_HEARTBEAT` 发送 power-up / heartbeat；CP 注册 IPI 回调处理 |

CP 侧超时窗口 `HB_TIMEOUT_MS`：`CONFIG_WDT_EN` 开启时等于 `CONFIG_INT_WDT_PERIOD_MS` （defconfig 默认 8000 ms）；关闭时为 `MB_IPC_HEARTBEAT_TIME * 3` （默认 6000 ms）。

<a id="cp-ap-cp"></a>

#### CP → AP：确认 CP 是否活着（可选）

反向链路用于 AP 监测 CP 是否出现异常跑飞，需显式打开 ``` CONFIG_CP_HANG_DUMP_BY_AP``（AP/CP 两侧均需配置，且依赖 ``CONFIG_IPI ``` 与 `DEBUG_VERSION` 或 `DUMP_ENABLE`）。

> - CP 发送：`cp/components/coredump/bk_coredump_cp_hang.c`，`entry_main()` 中 `bk_cp_hang_debug_heartbeat_init()` 创建 `cp_hang_hb` 任务，经 IPI（`IPI_DOMAIN_CP_HANG_DEBUG`）向 AP 发送心跳
> - 发送周期：`CONFIG_CP_HANG_DUMP_BY_AP_PERIOD_MS`，默认 1000 ms
> - AP 监测：`ap/components/coredump/bk_coredump_cp_hang.c`，`bk_cp_hang_dump_by_ap_init()` 注册 IPI 回调并创建 `cp_hang_mon` 任务
> - CP 超时：AP 采集 CP 可见寄存器/内存上下文后复位（可选 `CONFIG_CP_HANG_DUMP_BY_AP_MEMDUMP` 输出 CP RAM/PSRAM 窗口）

备注

- AP → CP 心跳走 Mailbox 或 IPI，用于确认 AP 子系统存活，与 AON/WWDT 配合使用。
- CP → AP 心跳仅走 IPI，属于调试/诊断能力，默认关闭；不能替代 CP 侧 AON WDT 对 CP 自身的监测。
- 低功耗下 CP 监测 AP 时会在 `mb_ipc_enter_lv` / `mb_ipc_exit_lv` 中暂停或刷新检查；AP 可用 `mb_ipc_heartbeat_pause()` 暂停发送。

<a id="id12"></a>

### **系统调试**

系统的log由CP管理, 如果是CP侧的log, 则直接通过串口输出; 如果是AP侧的log, 由AP通过mailbox传送到CP侧, 再由串口输出。
CP侧的log不带任何前缀, AP侧的log会带ap0或ap1前缀。

如以下是系统启动的部分log示例:

```
os:I(7):mem_type start    end      size
os:I(7):-------- -------- -------- --------
os:I(7):ram      0x28064e00 0x2809e7f8 236024
os:I(7):non_heap 0x28064e00 0x280853a0 132512
os:I(7):iram     0x8064000 0x8064c40 3136
os:I(7):data     0x28064e00 0x28066128 4904
os:I(7):bss      0x28066140 0x2808539c 127580
os:I(7):heap     0x280853a0 0x2809e7f8 103512
os:I(7):psram    0x60700000 0x60720000 131072
os:I(8):create flash_svr, tcb=28088e00, stack=[280887d8-28088dd8:1536], prio=3
flash:I(8):id=0xc86517
ef:I(9):ENV start address is 0x007FA000, size is 8192 bytes.
ef:I(10):EasyFlash V4.1.0 is initialize success.
(11):ate enabled is 0
(11):driver_init end
sensor:I(11):saradc low value:[9bb]
sensor:I(11):saradc high value:[136a]
sensor:I(11):sdmadc low value:[6ec1]
sensor:I(11):sdmadc high value:[89e4]
init:I(11):reason - power on
init:I(11):regs - 0, 0, 0
init:I(11):armino rev:
init:I(11):armino soc id:53434647_72360101
bk_init:I(11):armino app init: Jun  6 2025 17:30:09
bk_init:I(11):verify id: unknown
bk_init:I(11):APP Version: unknown
nv:I(11):vnd_cal_version = 24-04-10 00:00:00
os:I(12):create event, tcb=28089ba8, stack=[28089380-28089b80:2048], prio=1

......

bluetoot:I(97):bk_bluetooth_init ok
os:I(98):create rosc_calib, tcb=28095028, stack=[28094000-28095000:4096], prio=1
(98):user app entry(0x2033561)
(99):reset_cpu1_core at: 02150000, start=1
ap0:AP:E(13):Mailbox send data fail[ret:-4103]
ap0:os:I(13):psram:0x60720000,size:655360
ap0:os:I(1):
ap0:os:I(13):mem_type start    end      size
ap0:os:I(13):-------- -------- -------- --------
ap0:os:I(13):ram      0x28010600 0x28060ff8 330232
ap0:os:I(13):non_heap 0x28010600 0x2801a400 40448
ap0:os:I(13):iram     0x8010000 0x8010508 1288
ap0:os:I(13):data     0x28010600 0x28010f44 2372
ap0:os:I(13):bss      0x28011d40 0x2801a3fc 34492
ap0:os:I(13):heap     0x2801a400 0x28060ff8 289784
ap0:os:I(13):psram    0x60720000 0x607c0000 655360
ap0:ef:I(14):ENV start address is 0x007FC000, size is 8192 bytes.
ap0:ef:I(32):EasyFlash V4.1.0 is initialize success.
ap0:(33):driver_init end
ap0:init:I(33):reason - power on
ap0:init:I(33):regs - 0, 0, 0
ap0:init:I(33):armino rev:
ap0:init:I(33):armino soc id:53434647_72360101
ap0:bk_init:I(33):armino app init: Jun  6 2025 17:30:00
ap0:bk_init:I(33):verify id: unknown
ap0:bk_init:I(33):APP Version: unknown
ap0:gpio:I(34):bk_gpio_driver_init:has inited
ap0:OS:I(34):create cli, tcb=2801ede8, stack=[2801d1c0-2801edc0:7168], prio=5, xCoreID=0
```

系统支持通过CLI命令对模块进行调试。CP侧的CLI命令不需要带任何前缀; AP侧的CLI命令必须带上 ap\_cmd 前缀。

以下是CP侧和AP侧输入memshow命令的示例:

```
CP侧
memshow （输入命令）

os:I(108703):create shell_handle, tcb=28087270, stack=[28085648-28087248:7168], prio=5
cli:I(108704):================Static memory================
os:I(108704):
os:I(108704):mem_type start    end      size
os:I(108704):-------- -------- -------- --------
os:I(108704):ram      0x28064e00 0x2809e7f8 236024
os:I(108704):non_heap 0x28064e00 0x280853a0 132512
os:I(108704):iram     0x8064000 0x8064c40 3136
os:I(108704):data     0x28064e00 0x28066128 4904
os:I(108704):bss      0x28066140 0x2808539c 127580
os:I(108704):heap     0x280853a0 0x2809e7f8 103512
os:I(108704):psram    0x60700000 0x60720000 131072
cli:I(108704):================Dynamic memory================
name    total   free    minimum   peak
heap        103512  31688   26200   77312
psram       131072  131040  129104  1968

AP侧
ap_cmd memshow （输入命令）
os:I(2009):create shell_handle, tcb=280871e0, stack=[280855b8-280871b8:7168], prio=5

$ap0:cli:I(1857):================Static memory================
ap0:os:I(1857):
ap0:os:I(1857):mem_type start    end      size
ap0:os:I(1857):-------- -------- -------- --------
ap0:os:I(1857):ram      0x28010600 0x28060ff8 330232
ap0:os:I(1857):non_heap 0x28010600 0x2801a408 40456
ap0:os:I(1857):iram     0x8010000 0x8010508 1288
ap0:os:I(1857):data     0x28010600 0x28010f44 2372
ap0:os:I(1857):bss      0x28011d40 0x2801a404 34500
ap0:os:I(1857):heap     0x2801a408 0x28060ff8 289776
ap0:os:I(1857):psram    0x60720000 0x607c0000 655360
ap0:cli:I(1857):================Dynamic memory================
name    total   free    minimum   peak
heap        289784  250736  246400  43384
psram       655360  655328  655288  72
```

当系统发生了异常时, 如果开启了宏CONFIG\_DEBUG\_FIRMWARE或CONFIG\_DUMP\_ENABLE, 会有dump log输出。如果是CP侧发生了异常, dump log直接通过串口进行输出;
如果是AP侧发生了异常, dump log通过mailbox传输到CP侧, 由CP侧控制串口进行输出。

备注

为了兼容性, AP侧的cli命令统一带ap\_cmd前缀, 因为此时AP为smp系统, 两个core可以看作一个整体。
但是AP侧的log 输出可能带有ap0 和 ap1, 这是为了区分具体是哪个core在运行代码输出的log。

如：

ap1:(95040):cpu2\_test\_task run core: 2

ap0:(95040):cpu1\_test\_task run core: 1

ap0:(96040):cpu1\_test\_task run core: 1

ap1:(96040):cpu2\_test\_task run core: 2

<a id="cp"></a>

## **CP子系统**

CP侧的功能比较简单, 主要分为以下部分：

> - 运行Wi-Fi, BLE, 用于低功耗保活的LWIP协议栈
> - 管理系统的log输出以及cli命令响应
> - 管理核间心跳, 检测AP是否在线
> - 系统的低功耗管理

<a id="ap"></a>

## **AP子系统**

<a id="id13"></a>

### **概述**

按照新的架构设计, BK7259 AP 子系统支持双核 SMP，两个核共享外设与内存资源。每个core又各自含有自身的NVIC、cache等私有资源。核间可以通过 mailbox 传递必要信息；FreeRTOS SMP 的 cross-core 调度通知还支持 IPI doorbell，由 `CONFIG_FREERTOS_SMP_CROSS_CORE_IPI` 控制是否启用，关闭时仍走 mailbox doorbell 路径。无论使用 mailbox 还是 IPI，SMP 命令本身仍通过共享内存中的 `crosscore_mb_cmd[]` 位图传递。

<a id="id28"></a>
![AP and CP architecture](../../_assets/76f6d8d62619a11e6738-smp.png)


SMP 架构示意图

备注

1.图中的CPU0/CPU1指的是逻辑core id, 具体解释见下一章节, 后续我们统一用逻辑id来表述。

2.SMP 中的 mailbox 指一条物理 mailbox 通道；IPI 为处理器间中断 doorbell，二者都只负责唤醒对端 core，真正的 SMP 命令放在共享 SRAM 的 `crosscore_mb_cmd[]` 中。是否用 IPI 替代 mailbox doorbell 由 `CONFIG_FREERTOS_SMP_CROSS_CORE_IPI` 控制，IPI driver 总开关为 `CONFIG_IPI`。

<a id="core-id"></a>

### **core id管理**

每个 SMP 镜像都有自己的逻辑 core 编号，同时 SoC 仍然保留物理
CPU ID。

从内核视角看，逻辑 ID 总是从 0、1 开始排列，表示当前子系统中的
logical core。

而从应用层视角看，某些资源配置必须绑定到具体物理核，因此需要通过
`os.h` 中的 `rtos_get_core_id()` 获取物理 ID：

- CP 返回 `CPU0_CORE_ID` 或 `CPU1_CORE_ID`
- AP 返回 `CPU2_CORE_ID` 或 `CPU3_CORE_ID`

在SMP启动过程中, 每个core会分别将自身的core id记录到特定位置。

重要

注意：获取物理 CPU ID 时只应调用 `rtos_get_core_id()`。
只有在当前 SMP 子系统内部需要判断逻辑核时，才应使用
`portGET_CORE_ID()`。

<a id="smp"></a>

### **SMP启动流程**

子系统内 SMP 启动是完整系统启动流程的一部分，CP/AP 全链路时序请参阅
[系统启动流程（CP \+ AP）](system_boot.md)。

在系统的引导和初始化阶段, 只有一个上下文, 只能由一个处理器来处理。

所以对于SMP系统, 一般会有一个先启动的core(称为primary core), 由其负责初始化整个系统的资源, 而其他的core则等待这些资源准备好后再开始工作。

对于每个 SMP 子系统，primary core 都是逻辑 Core 0。它负责引导该
子系统的 memory、cache、中断以及外设等资源。

Core 0 完成资源初始化后，会释放逻辑 Core 1，然后进入正常任务调度。
在当前代码中，CP primary core 释放 CPU1，AP primary core 释放
CPU3。

<a id="id29"></a>
![SMP boot](../../_assets/975afe96adfe4e8a7a8a-smp_boot.png)


SMP 启动流程

<a id="id14"></a>

### **SMP编程注意事项**

从软件的时间看, SMP系统与单CPU系统在编程上还是有一些差异的。这些差异主要体现在:

- 虽然外设与内存资源都是共享的, 但是如果多个CPU同时对共享资源进行访问时, 需要加临界区保护。运行态本地临界区通过 `BASEPRI` 屏蔽当前 core 上的普通可抢占中断；
  跨 core 共享资源还需要结合自旋锁或 SMP 感知的互斥机制，不能只依赖单核本地中断屏蔽。SMP 临界区与任务绑核说明见 AP 文档「操作系统与内存管理」章节。
- 每个core都有自身的中断管理器, 但外设的中断通常是由某一个core来进行处理。需要根据实际需求配置中断路由。
  具体可以参考 [中断管理](interrupt.md)。
- 上层创建的任务可以绑定到SMP系统的某个CPU, 也可以不绑定核, 由内核自行管理。在不绑定核的情形下, 需要注意对访问资源的独占保护。
  创建任务的 API 请参考 AP 文档中的 OS 抽象层章节。

<a id="id15"></a>

## **应用开发参考**

<a id="id16"></a>

### AP 侧应用入口

大多数产品应用应从 `projects` 目录下的 AP 工程入口开始开发。以
`projects/app` 为例：

> - `projects/app/CMakeLists.txt`：声明工程并引入构建框架
> - `projects/app/ap/CMakeLists.txt`：注册 AP 应用源文件和组件依赖
> - `projects/app/ap/ap_main.c`：AP 侧 `main()`，先调用 `bk_init()`
>   完成 SDK 初始化，再启动业务逻辑

推荐开发方式：

> - 在 `main()` 中保持初始化顺序清晰，先完成 `bk_init()`，再创建业务任务
> - 长时间运行或阻塞式业务应放入独立 task，不建议直接阻塞 `main` 任务
> - 需要复用的业务能力可以抽成 AP 侧 component，再由工程 CMake 声明依赖
> - 面向客户或产品的逻辑优先放 AP 侧，只有确实需要连接、低功耗或 CP 侧资源时才修改 CP

<a id="id17"></a>

### 新增 AP 组件

新增通用组件时建议遵循以下规则：

> - 组件目录放在 `ap/components/<component_name>`
> - 使用 `CMakeLists.txt` 注册源文件、头文件和依赖
> - 对外头文件只暴露稳定 API，内部实现细节放在组件私有目录
> - 组件依赖驱动时通过 `driver` 或已有组件 API 调用，不直接访问寄存器
> - 涉及共享数据、DMA buffer 或跨核访问时明确 cache 同步责任

如果功能只服务某个工程，不建议过早沉淀为公共组件；可以先放在
`projects/<project>/ap` 下，待多个工程复用后再抽象。

<a id="ap-cp-ipc"></a>

### 新增 AP/CP IPC 通道

新增跨 AP/CP 的业务通信时，优先使用 `BK_IPC_CHANNEL_REGISTER` 注册逻辑通道。
基本步骤如下：

> 1. 在 AP 和 CP 两侧声明同名逻辑通道
> 2. 为两侧分别实现 `rx_cb` 和可选 `tx_cb`
> 3. 使用相同 route 注册通道
> 4. 调用 `bk_ipc_send()` 发送数据
> 5. 根据业务需要选择同步或异步发送标志

设计 IPC 数据结构时应注意：

> - 消息结构应固定版本，避免 AP/CP 两侧结构体定义不一致
> - 大块数据优先放共享 buffer，Mailbox/IPC 中只传描述符或控制消息
> - 异步发送时明确 buffer 生命周期，必要时在 `tx_cb` 中释放
> - 同步发送不得在持有长临界区或中断上下文中滥用，避免死锁或长时间阻塞
> - 错误码需要在调用方处理，不能假设对端一定在线或通道一定空闲

<a id="id18"></a>

### 调试建议

常用调试入口：

> - CP CLI：直接输入命令，例如 `memshow`
> - AP CLI：使用 `ap_cmd` 前缀，例如 `ap_cmd memshow`
> - AP log：通过 Mailbox 送到 CP，再从 UART0 输出，通常带 `ap0` 或 `ap1` 前缀
> - dump 分析：AP 异常 dump 通过 CP 输出，可结合 `tools/dump_tools` 中工具分析

排查 AP/CP 协同时建议先确认：

> - AP 与 CP 镜像是否来自同一次构建
> - 分区表和 RAM region 是否与工程配置一致
> - Mailbox/IPC 相关 Kconfig 是否同时在两侧启用
> - AP/CP 两侧消息结构、route 和通道名是否一致
> - AP 日志中是否存在 Mailbox busy、timeout 或 send fail

<a id="id19"></a>

## **平台与驱动开发参考**

<a id="id20"></a>

### 驱动分层边界

平台或驱动开发应优先保持以下分层：

> - `middleware/soc`：SoC 寄存器、LL/HAL、芯片相关初始化
> - `middleware/driver`：外设驱动、驱动模型、Mailbox、Flash、GPIO、DMA 等
> - `components`：面向业务或应用的模块封装
> - `projects`：产品工程配置与业务入口

不建议应用直接访问 `soc` 或寄存器层。如果组件需要新增硬件能力，应先在 driver
层形成稳定接口，再由 component 调用。

<a id="ap-cp"></a>

### AP/CP 协同原则

AP 与 CP 是独立镜像，不能依赖直接函数调用或共享全局变量完成协同。新增跨域功能时
应明确以下内容：

> - 功能主控侧：判断逻辑应放 AP、CP 还是两侧协作
> - 通信机制：选择 BK IPC、Mailbox channel、虚拟 UART 或专用共享内存协议
> - 状态机：定义 init、ready、busy、error、reset 等状态
> - 超时与恢复：对端无响应、Mailbox 满、AP/CP reset 时如何恢复
> - 版本兼容：AP/CP 消息结构和命令号应同步维护

连接、低功耗、看门狗、系统复位等通常由 CP 主控；多媒体、UI、AI、应用工作负载通常
由 AP 主控。若 AP 需要影响 CP 侧策略，应通过 CP 暴露的 API 或 IPC 请求完成。

<a id="id21"></a>

### SMP 与中断约束

AP 与 CP 内部都是 SMP 子系统。修改驱动或中断路径时需要考虑：

> - 共享资源必须使用适合 SMP 的临界区，不能只依赖单核关中断
> - 外设中断通常路由到指定 core，修改路由前需确认 task affinity 和 ISR 依赖
> - hard-pinned task 会影响 AP hotplug 和负载迁移
> - DMA buffer、共享内存和 IPC buffer 必须遵守当前内存属性策略；默认使用
>   non-cacheable buffer，避免业务层手动维护 cache 一致性
> - ISR 中只做必要工作，复杂逻辑应投递到 task 或 worker 中处理

AP / CP CPU hotplug 的设计边界和测试方法，请参考 AP / CP 文档集的 Developer Guide → CPU Hotplug 章节。

<a id="id22"></a>

### 资源修改原则

修改内存、分区或 PSRAM 使用方式时应遵循：

> - AP/CP SRAM 归属通过 RAM region 配置生成，不建议手工改链接脚本结果
> - CP 侧不应将长期运行的 task、queue 或代码放入可能掉电的 PSRAM
> - 大 buffer 应优先评估 PSRAM、cache、DMA 可见性和访问延迟
> - 修改分区后需要重新生成并确认最终 `all-app.bin` 包含正确镜像
> - 资源布局变化需要同步更新文档、工程配置和调试脚本

<a id="id23"></a>

## **常见开发场景**

<a id="id24"></a>

### 添加一个 AP 侧业务任务

> 1. 在工程 AP 目录新增业务源文件
> 2. 在 `projects/<project>/ap/CMakeLists.txt` 注册源文件和依赖组件
> 3. 在 `main()` 调用 `bk_init()` 之后创建业务 task
> 4. 使用 `rtos_*` API 创建同步对象、队列和线程
> 5. 通过 `ap_cmd`、日志和 `memshow` 验证任务运行状态

<a id="id25"></a>

### 添加一个 AP/CP 控制命令

> 1. 定义命令号和消息结构
> 2. 在 AP/CP 两侧注册 IPC 通道和回调
> 3. 在主控侧封装同步或异步发送 API
> 4. 在从属侧处理命令并返回结果
> 5. 增加 CLI 或 UT 测试覆盖正常、超时和错误路径

<a id="id26"></a>

### 定位 AP 侧异常

> 1. 通过 UART0 收集包含 AP dump 的完整日志
> 2. 确认 `app.elf` 与日志对应同一次构建
> 3. 使用 dump 分析工具生成报告
> 4. 结合 `ap0`/`ap1` 前缀判断异常发生的物理 core
> 5. 检查最近修改的 task、ISR、IPC 和共享 buffer 生命周期
