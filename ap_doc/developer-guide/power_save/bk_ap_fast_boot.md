---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_ap_fast_boot.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap"></a>

# AP快速启动

<a id="cpap"></a>

## 使用前必读：CP与AP配置

本文面向使用AP快速启动的用户，重点说明工程配置、回调选择、上下电流程、限制条件和
验收方法。接入业务前，应先确认CP和AP两侧配置匹配。

CP侧必须开启：

```
CONFIG_PM_AP_POWERDOWN_WHEN_LV=y
CONFIG_PSRAM_DATA_RETENTION_ENABLE=y
CONFIG_PM_AP_FAST_BOOT_ENABLE=y
```

AP侧必须开启：

```
CONFIG_SOC_SMP=y
CONFIG_CPU_HOTPLUG=y
CONFIG_CPU_HOTPLUG_BOOT_OFFLINE=n
CONFIG_PSRAM_DATA_RETENTION_ENABLE=y
CONFIG_PM_AP_FAST_BOOT_ENABLE=y
```

`CONFIG_PM_AP_FAST_BOOT_ENABLE` 在AP侧依赖SMP和PSRAM retention，在CP侧依赖允许
在睡眠模式下关闭AP，并确保PSRAM始终处于retention状态。AP快速启动过程中只关闭AP
电源域；PSRAM controller随AP掉电，PSRAM颗粒供电保持，颗粒中的数据不会丢失。AP恢复
时需要重新初始化PSRAM controller，之后才能继续访问保留的数据。完整低功耗链路还应
在CP和AP最终配置中确认：

```
CONFIG_PSRAM=y
CONFIG_DEEP_LV=y
CONFIG_FREERTOS_USE_TICKLESS_IDLE=2
```

使用RTC作为唤醒源时，CP侧还需要 `CONFIG_AON_RTC=y`；使用GPIO等其他唤醒源时，
应开启对应驱动和唤醒配置。上述依赖通常已由Kconfig或工程基线带入，仍应检查最终生成
的配置。建议直接以
`projects/pm/ap_fast_boot/cp/config/bk7259/defconfig` 和
`projects/pm/ap_fast_boot/ap/config/bk7259_ap/defconfig` 为基线移植，不要只复制
上述配置项。

警告

CP和AP任一侧未开启PSRAM data retention，或者两侧快速启动配置不一致时，都不能
恢复原有执行现场。AP首次冷启动必须按正常SMP流程启动AP0和AP1，因此不能开启
`CONFIG_CPU_HOTPLUG_BOOT_OFFLINE`。

开始接入前，用户还应确认：

> - 所有访问PSRAM、DMA、掉电外设或依赖AP1的业务都能停止，并且等待时间有上限。
> - 上层应用和底层SDK需要的回调均已注册成功，回调参数在AP恢复后仍然有效。
> - AP ON/OFF投票能够成对执行，OFF失败时业务可以继续运行或正确回滚。
> - 业务恢复以 `app_resume` 为准，不能把 `BOOT_SUCCESS` 当作全部资源已经就绪。

<a id="id1"></a>

## 功能概述

AP快速启动用于解决AP掉电后重新执行镜像加载、C运行库初始化、`bk_init()` 和应用
`main()` 导致的启动时间较长问题。启用该功能后，系统在AP掉电前保存AP运行现场，
AP重新上电时恢复原有FreeRTOS执行点，而不是执行一次精简的冷启动。

在硬件、电源、时钟和回调耗时满足要求的条件下，AP0可在CP发起上电后的
10 ms内恢复调度。该指标应以CP日志中的 `AP_TIME ap0_restore_scheduler_ready` 为准。
AP1重新上线、掉电外设恢复和用户业务恢复属于后续阶段，不包含在AP0恢复调度时间内，
用户应在目标板和量产配置上实测确认。

适用场景包括门铃、摄像头和电池设备：AP完成图像、音频或AI业务后掉电，RTC、GPIO、
Wi-Fi、BLE等事件到来时由CP快速拉起AP继续处理。

重要

快速启动保留软件执行现场，但不会保持CPU、外设和多媒体硬件寄存器。用户必须通过
本章介绍的回调机制停止正在运行的业务，并在恢复阶段重新建立掉电硬件状态。

<a id="id2"></a>

## 快速启动与冷启动的区别

```
                            冷启动                                    AP快速启动
             +----------------------------------+        +----------------------------------+
AP上电 ---->  | 加载/校验AP镜像                  |        | SRAM/PSRAM数据保持                |
             | 初始化C运行环境                   |        | 恢复PSRAM控制器                   |
             | 执行bk_init/main                 |        | 恢复DTCM和AP0现场                 |
             | 外设驱动上电及初始化               |        | 恢复或重新初始化外设驱动           |
             | 多媒体驱动上电及初始化             |        | 恢复或重新初始化多媒体驱动         |
             +----------------+-----------------+        +----------------+-----------------+
                              |                                           |
                              v                                           v
                     业务从初始状态运行                           原任务、栈和变量继续运行
```

冷启动会完整执行外设驱动和多媒体驱动的上电及初始化。AP快速启动保留前一次运行的AP SRAM
和PSRAM中的软件状态，但外设及多媒体硬件状态会随AP掉电而丢失。为了使驱动和业务恢复后
正常工作，各模块可根据硬件特性和业务需求选择以下方案：

> - **备份并恢复寄存器：** AP掉电前停止业务和DMA，将掉电后丢失的有效配置寄存器保存到
>   保留内存；唤醒后按依赖顺序恢复寄存器。不得恢复旧FIFO、BUSY、pending IRQ或中断前
>   正在执行的瞬时事务。
> - **重新初始化驱动：** AP掉电前停止并排空业务；唤醒后复位硬件，并使用保留的有效配置
>   重新执行外设或多媒体驱动初始化。

同一系统可以按模块混合使用两种方案。各业务应综合硬件复位行为、配置复杂度、依赖关系、
恢复耗时、失败回滚和幂等要求选择方案，并在 `app_resume` 启动用户业务前完成底层驱动
恢复。

快速恢复后具有以下特征：

> - AP的 `main()` 不会再次执行。
> - 已创建的任务、queue、semaphore、mutex、timer和heap对象继续使用原地址。
> - 栈上局部变量、AP SRAM全局变量和PSRAM数据保持原值。
> - AP0从掉电前保存的执行点继续调度，不从任务入口重新运行。
> - AP1的动态执行现场不保持；AP1在AP0恢复后重新上线并加入SMP调度。
> - 掉电外设、多媒体模块和DMA的硬件状态不会因为软件内存保持而自动恢复。

<a id="id3"></a>

## 掉电期间的电源和数据状态

开启AP快速启动后，关闭AP时各资源状态如下：

| 资源 | AP掉电期间状态 | 处理方式 |
| --- | --- | --- |
| AP SRAM | 保持供电 | `.data`、`.bss`、TCB、任务栈和heap等数据原地保持。 |
| AP0 DTCM | DTCM本体掉电 | 掉电前备份到保持供电的AP SRAM，恢复中断和调度前写回。 |
| PSRAM cell | 保持供电 | 数据原地保持；恢复时只恢复PSRAM控制器、时钟、mode和pad状态。 |
| AP0 | 掉电 | 掉电前保存架构上下文，上电后恢复并返回原执行点。 |
| AP1 | 掉电 | 掉电前hotplug offline，恢复后重新online，不保存原动态执行现场。 |
| AP外设和多媒体模块 | 掉电 | UART、SPI、I2C、DMA、camera、ISP、LCD、audio等按驱动要求恢复。 |

下表汇总AP关闭期间各资源是否下电以及是否支持Retention，便于用户快速判断哪些状态
可以直接继续使用，哪些状态必须通过备份或重新初始化恢复：

| 资源 | 是否下电 | 是否Retention |
| --- | --- | --- |
| AP SRAM | 否，保持供电 | 是 |
| AP0 DTCM | 是 | 否，内容备份到AP SRAM |
| PSRAM cell | 否，cell LDO保持供电 | 是 |
| AP0 CPU | 是 | 否，架构上下文另行保存 |
| AP1 CPU | 是 | 否，不保存动态执行现场 |
| AP外设和多媒体模块 | 是 | 否，按模块要求重新初始化 |

备注

本表中的Retention表示资源自身在AP掉电期间保持供电并保留原状态。AP0 DTCM和AP0
CPU上下文通过软件备份与恢复实现，不属于硬件Retention；外设寄存器、FIFO、DMA
瞬时状态和AP1动态执行现场均不保留。

整体关系如下：

```
            AP掉电期间保持                              AP掉电期间关闭
+------------------------------------+      +------------------------------------+
| AP SRAM                            |      | AP                                 |
|   全局变量、TCB、任务栈、heap        |      | UART / SPI / I2C / DMA             |
|                                    |      | Camera / ISP / LCD / Audio         |
| PSRAM                              |      | 其他AP掉电域硬件                    |
|   全局数据、动态对象、业务buffer     |      |                                    |
+-----------------+------------------+      +-----------------+------------------+
                  |                                             |
                  +----------------------+----------------------+
                                         |
                                         v
                        软件对象继续使用，硬件必须重新恢复
```

备注

AP SRAM或PSRAM中的指针和软件状态虽然保持，但其指向的外设寄存器、DMA瞬时状态、
FIFO内容和正在进行的硬件事务不保持。不得把“变量仍在”理解为“外设仍在运行”。

<a id="id4"></a>

## 工程基线与编译验证

完成文首配置后，推荐先编译并运行示例工程 `projects/pm/ap_fast_boot`：

```
make bk7259 PROJECT=pm/ap_fast_boot
```

编译后应检查CP和AP最终生成的配置，而不只检查用户工程中的增量 `defconfig`。即使
链接文件中没有显式的 `.psram.data`，任务栈、heap对象或业务buffer仍可能位于
PSRAM。PSRAM数据失效后继续恢复旧PC、TCB或指针可能导致HardFault或数据破坏。

<a id="id5"></a>

## 用户使用流程

用户接入时应完成以下工作：

1. 同时开启CP和AP的快速启动及PSRAM保持配置。
2. 梳理所有AP业务使用的任务、AP1、DMA、外设和PSRAM buffer。
3. 上层应用按需注册 `prepare_power_off` 和 `app_resume`；底层SDK和硬件所有者
   负责其余必要回调。
4. 检查回调注册结果；注册失败或必要模块未接入时禁止关闭AP。
5. 关闭AP前停止新请求，并让已提交业务有界地排空。
6. 使用AP启动投票接口成对控制AP，不直接操作AP电源域。
7. 在 `app_resume` 中恢复用户业务，不在 `main()` 中等待再次初始化。
8. 在目标板上验证启动时间、数据完整性、低功耗电流和循环稳定性。

推荐的用户状态机：

```
  +----------------------+
  |       RUNNING        |
  |   接受并处理新业务     |
  +----------+-----------+
             |
      收到AP关闭请求
             |
             v
  +----------------------+
  |       DRAINING       |
  |      拒绝新请求       |
  |    排空queue/DMA     |
  +------+--------+------+
         |        |
   失败/取消      排空完成
         |        |
         v        v
+------------+  +----------------------+
|  ROLLBACK  |  |      SUSPENDED       |
|  恢复入口   |  |   AP CPU/外设掉电    |
+-----+------+  +----------+-----------+
      |                    |
      |                AP快速恢复
      |                    |
      +----------+---------+
                 |
                 v
      +----------------------+
      | app_resume完成       |
      | 恢复用户业务入口      |
      +----------+-----------+
                 |
                 +----------> RUNNING
```

<a id="id6"></a>

## AP上下电投票

AP由多个模块共同投票控制。只有所有模块都释放ON票后，AP才会真正关闭。调用成功仅表示
本模块的投票已接受，不代表AP一定已经完成掉电。

CP侧控制示例：

```
#include <modules/pm.h>

bk_err_t app_start_ap(void)
{
    return bk_pm_module_vote_boot_ap_ctrl(
        PM_BOOT_AP_MODULE_NAME_APP,
        PM_POWER_MODULE_STATE_ON);
}

bk_err_t app_stop_ap(void)
{
    return bk_pm_module_vote_boot_ap_ctrl(
        PM_BOOT_AP_MODULE_NAME_APP,
        PM_POWER_MODULE_STATE_OFF);
}
```

使用时应遵守以下规则：

> - 同一业务始终使用同一个 `PM_BOOT_AP_MODULE_NAME_*`。
> - ON和OFF必须成对调用。
> - OFF失败时不能假定AP已关闭，应保持业务可恢复或执行回滚。
> - Wi-Fi、BLE、多媒体等其他模块仍持有ON票时，AP不会关闭。
> - 不要绕过投票接口直接切断AP电源。

<a id="id7"></a>

## 低功耗回调机制

新业务统一使用 `bk_pm_ap_power_ops_register()` 注册AP电源转换操作：

```
typedef bk_err_t (*pm_ap_power_callback_t)(void *arg);

typedef struct {
    const char *name;
    pm_ap_power_callback_t prepare_power_off;
    pm_ap_power_callback_t quiesce;
    pm_ap_power_callback_t backup;
    pm_ap_power_callback_t restore;
    pm_ap_power_callback_t resume;
    pm_ap_power_callback_t app_resume;
    void *arg;
    uint8_t priority;
} pm_ap_power_ops_t;

bk_err_t bk_pm_ap_power_ops_register(const pm_ap_power_ops_t *ops);
bk_err_t bk_pm_ap_power_ops_unregister(const pm_ap_power_ops_t *ops);
```

模块不需要实现全部回调。应用只需填写自己实际参与的阶段，未使用的成员保持为
`NULL`。

| 回调 | 主要用途 | 执行上下文 | AP1状态 | 可否使用RTOS |
| --- | --- | --- | --- | --- |
| `prepare_power_off` | 原子拒绝新请求，非阻塞检查pending/inflight是否排空 | AP0 Idle，关中断 | 在线 | 不允许 |
| `quiesce` | 最终停止业务、周期任务和传输 | AP0 PM任务，开中断 | 在线 | 允许，必须有超时 |
| `backup` | 备份掉电后丢失的硬件配置 | AP0，关中断 | 离线 | 不允许 |
| `restore` | 恢复硬件寄存器或最小硬件环境 | AP0，关中断 | 离线 | 不允许 |
| `resume` | 恢复驱动、中间件和提交入口，也用于失败回滚 | AP0 PM任务，开中断 | 在线 | 允许 |
| `app_resume` | 系统及双向通信就绪后恢复用户业务 | AP0 PM任务，开中断 | 在线 | 允许 |

<a id="id8"></a>

### 注册接口限制

调用 `bk_pm_ap_power_ops_register()` 前必须满足以下条件：

> - `ops` 和 `ops->name` 不能为 `NULL`，并且至少实现一个回调。
> - `quiesce` 非空时必须同时提供 `resume`，用于关闭失败时恢复已经停止的模块。
> - `backup` 和 `restore` 必须成对提供，不能只备份不恢复或只恢复未备份的数据。
> - 注册和注销只能在AP正常运行且未进入关闭准备流程时执行。下电、恢复或
>   `prepare_power_off` 探测期间调用会返回 `BK_ERR_BUSY`。
> - 同一个描述符地址不能重复注册，否则返回 `BK_ERR_BUSY`。注销时必须传入注册时的
>   同一个描述符地址。
> - 注册接口内部需要申请内存，内存不足时返回 `BK_ERR_NO_MEM`。应在模块初始化的
>   任务上下文注册，不能在中断或电源回调中临时注册。
> - 描述符建议定义为全局或 `static const`。`name`、`arg` 及回调访问的状态在
>   整个注册期间必须有效，并且在AP恢复后仍可访问；不能把局部临时变量或AP1任务栈地址
>   作为 `arg`。

用户必须检查注册返回值。注册失败时，该模块不会参与AP关闭和恢复流程；如果模块仍在
访问PSRAM、DMA或掉电外设，则本次AP关闭不具备安全条件，不应继续释放AP ON票。

用户选择回调时按以下原则判断：

> - 应用已在投OFF票前停止新业务，`prepare_power_off` 只做无副作用的状态检查：
>   通常只需实现 `prepare_power_off` 和 `app_resume`。
> - `prepare_power_off` 会修改业务入口或其他需要回滚的状态：还必须实现幂等
>   `resume`，确保本次关闭取消时能够重新开放入口。
> - 必须在任务上下文等待存量事务、FIFO或DMA有界排空：由底层模块实现 `quiesce`，
>   并同时实现幂等 `resume`。
> - 必须保存和恢复掉电硬件寄存器：由硬件所有者成对实现 `backup` 和 `restore`。
> - 必须恢复驱动、中间件、IPC或系统服务入口：由对应SDK模块实现 `resume`。

<a id="sdk"></a>

### 上层应用与底层SDK职责

上层应用程序注册回调时，主要使用 `prepare_power_off` 和 `app_resume`：

> - `prepare_power_off` 用于停止接收新业务，并以非阻塞方式检查应用任务、queue和
>   inflight事务是否已经排空。该回调在关中断环境执行，不能调用RTOS接口、等待资源或
>   执行耗时操作。
> - `app_resume` 在系统服务、AP1和CP/AP双向通信均已就绪后执行，用于恢复用户业务
>   入口、重新同步业务状态并启动应用任务。

`quiesce`、`backup`、`restore` 和 `resume` 主要由底层SDK模块注册，或者由
确实需要直接管理底层硬件资源的模块实现。上层应用不应为了接收上下电通知而实现这些
回调。但如果应用在 `prepare_power_off` 中关闭了业务入口，则需要额外实现幂等
`resume`，用于关闭失败或取消时回滚应用状态。

其中，真正操作底层硬件的 `backup` 和 `restore` 在AP0关中断且AP1离线的环境中
执行，只允许访问寄存器和保留的静态内存，禁止使用日志、动态内存、锁、delay和等待
中断完成。`quiesce` 和 `resume` 在PM任务上下文执行，是否允许使用RTOS接口应以
上表所列执行上下文为准。

<a id="id9"></a>

### 各模块补充说明（预留）

以下模块的SDK基础适配已经完成，包括AP快速启动所需的停止、恢复和基础时序衔接。
下列条目仅预留给对应模块负责人补充用户使用时的额外限制、场景差异、配置要求、调试
方法和验收标准；如果模块没有额外注意事项，可标注“暂无”：

> - **Wi-Fi：** 预留补充业务模式、CP/AP通信依赖、恢复时机及异常处理等额外说明。
> - **BLE：** 预留补充连接模式、协议状态、恢复时机及异常处理等额外说明。
> - **驱动外设：** 预留补充UART、SPI、I2C、DMA等外设在不同使用方式下的额外配置和
>   限制说明。
> - **多媒体：** 预留补充camera、ISP、LCD、audio等模块在不同数据流和buffer模式下的
>   额外配置、恢复顺序及验收说明。

<a id="id10"></a>

### 回调顺序

数字越小优先级越高。建议使用SDK定义的优先级：

| 优先级 | 宏 | 典型模块 |
| --- | --- | --- |
| 0 | `PM_AP_POWER_PRIORITY_PLATFORM` | 电源、时钟、pinmux |
| 50 | `PM_AP_POWER_PRIORITY_BUS` | 总线、DMA、中断控制 |
| 100 | `PM_AP_POWER_PRIORITY_PERIPHERAL` | UART、SPI、I2C等外设 |
| 150 | `PM_AP_POWER_PRIORITY_SERVICE` | IPC、协议和系统服务 |
| 200 | `PM_AP_POWER_PRIORITY_APPLICATION` | 用户应用 |

关闭阶段从低层依赖的反方向执行，恢复阶段按依赖正方向执行：

```
AP关闭：
  应用(200) -> 服务(150) -> 外设(100) -> 总线(50) -> 平台(0)

AP恢复：
  平台(0) -> 总线(50) -> 外设(100) -> 服务(150)
      -> AP_FULL_READY -> CP开放业务通信 -> 应用app_resume(200)
```

该顺序保证上层业务先停止、底层资源最后关闭；恢复时先恢复底层资源，用户业务最后启动。

<a id="id11"></a>

## AP关闭时序

```
CP/电源管理           AP0 Idle              AP0 PM任务             AP1                驱动/应用
     |                    |                      |                  |                     |
     |-- AP OFF请求 ----->|                      |                  |                     |
     |                    |-- prepare_power_off（逆优先级） ------------------------------>|
     |                    |<------------------------------ BUSY：退出Idle，任务继续排空 ----|
     |                    |                      |                  |                     |
     |                    |-- 下一轮非阻塞检查 ------------------------------------------->|
     |                    |<----------------------------------------------------- BK_OK --|
     |<-- prepare READY --|                      |                  |                     |
     |-- recovery请求 -------------------------->|                  |                     |
     |                    |                      |-- quiesce ------>| 驱动/应用           |
     |                    |                      |-- 检查DMA空闲 -->|                     |
     |                    |                      |-- offline ------>|                     |
     |                    |                      |-- backup（关中断） -------------------> |
     |                    |<--------- PREPARED --|                  |                     |
     |                    |-- 检查IRQ/DMA/AP1状态 ----------------->|                     |
     |                    |-- 备份DTCM和AP0上下文 ----------------->|                     |
     |<------ sleep ACK --|                      |                  |                    |
     |-- 保持SRAM/PSRAM并关闭AP电源 ----------------------------------------------------->| OFF
```

`prepare_power_off` 可能被Idle重复调用，必须满足：

> - 第一次调用时以原子方式关闭新业务入口。
> - 只读取保留内存中的lock-free状态。
> - pending或inflight未清零时立即返回 `BK_ERR_BUSY`。
> - 不打印日志，不delay，不申请内存，不使用mutex、semaphore或queue。
> - 必须幂等、常量时间，不能主动等待任务或中断完成。

`quiesce` 在正常PM任务上下文执行，可以等待已有任务完成，但必须设置超时。建议主要
排空工作在收到关闭请求后立即开始，不要把复杂业务停止全部推迟到回调内。

<a id="id12"></a>

## AP恢复时序

```
CP/电源管理               AP0                AP0 PM任务             AP1              用户应用
     |                     |                      |                  |                   |
     |-- AP ON ----------->|                      |                  |                   |
     |-- 恢复PSRAM控制器- ->|                      |                  |                   |
     |-- 恢复DTCM/上下文 -->|                      |                  |                   |
     |                     |-- 返回WFI后续位置 --->|                  |                   |
     |<---- BOOT_SUCCESS --| AP0可调度            |                  |                   |
     |                     |--------------------->|                  |                   |
     |                     |                      |-- restore（关中断） ---------------->| 驱动
     |                     |                      |-- online ------->|                   |
     |                     |                      |<-------- ready --|                   |
     |                     |                      |-- resume --------------------------->| 服务
     |<-------------------------- AP_FULL_READY --|                  |                   |
     |-- 开放CP->AP业务通信 ----------------------------------------->|                   |
     |-- PWC恢复通知 ---------------------------->|                  |                   |
     |                     |                      |-- app_resume ----------------------->|
     |                     |                      |<-------------------- BK_OK/BK_FAIL --|
     |-- 执行CP侧POWER_ON回调 ------------------->|                  |                   |
```

`BOOT_SUCCESS` 只表示AP0和基础调度环境已经恢复，不表示AP1、外设和用户业务全部
可用。用户业务应等待 `app_resume`，不要在观察到 `BOOT_SUCCESS` 后立即访问camera、
ISP或依赖AP1的资源。

<a id="id13"></a>

## 用户代码示例

以下示例演示一个带异步事务的用户模块。模块关闭新提交入口，等待存量事务排空，并在真实
快速恢复后重启用户业务。示例中的 `inflight` 必须在每次异步事务开始和结束时原子增减。

```
#include <modules/pm.h>
#include <os/os.h>

typedef struct {
    volatile bool accepting;
    volatile uint32_t inflight;
    volatile bool suspended;
} app_pm_context_t;

static app_pm_context_t s_app_pm = {
    .accepting = true,
};

static bk_err_t app_request_enter(void)
{
    if (!__atomic_load_n(&s_app_pm.accepting, __ATOMIC_ACQUIRE)) {
        return BK_ERR_BUSY;
    }

    __atomic_add_fetch(&s_app_pm.inflight, 1, __ATOMIC_ACQ_REL);
    if (!__atomic_load_n(&s_app_pm.accepting, __ATOMIC_ACQUIRE)) {
        __atomic_sub_fetch(&s_app_pm.inflight, 1, __ATOMIC_RELEASE);
        return BK_ERR_BUSY;
    }
    return BK_OK;
}

static void app_request_exit(void)
{
    __atomic_sub_fetch(&s_app_pm.inflight, 1, __ATOMIC_RELEASE);
}

static bk_err_t app_prepare_power_off(void *arg)
{
    app_pm_context_t *ctx = arg;

    /* 关中断环境：只允许常量时间的原子操作。 */
    __atomic_store_n(&ctx->accepting, false, __ATOMIC_RELEASE);
    return (__atomic_load_n(&ctx->inflight, __ATOMIC_ACQUIRE) == 0U) ?
        BK_OK : BK_ERR_BUSY;
}

static bk_err_t app_quiesce(void *arg)
{
    app_pm_context_t *ctx = arg;

    /* 此处可使用RTOS接口，但所有等待都必须有超时。 */
    if (__atomic_load_n(&ctx->inflight, __ATOMIC_ACQUIRE) != 0U) {
        return BK_ERR_BUSY;
    }
    app_stop_periodic_work();
    ctx->suspended = true;
    return BK_OK;
}

static bk_err_t app_resume(void *arg)
{
    app_pm_context_t *ctx = arg;

    /*
     * 真实恢复和关闭失败回滚都会进入此回调，因此必须幂等。
     * 此处只恢复模块/服务入口，不执行需要CP双向通信的用户业务。
     */
    app_restore_service_if_needed();
    __atomic_store_n(&ctx->accepting, true, __ATOMIC_RELEASE);
    return BK_OK;
}

static bk_err_t app_final_resume(void *arg)
{
    app_pm_context_t *ctx = arg;

    /* AP1、驱动和AP/CP双向通信均已就绪。 */
    app_sync_state_with_cp();
    app_start_periodic_work();
    ctx->suspended = false;
    return BK_OK;
}

static const pm_ap_power_ops_t s_app_power_ops = {
    .name = "customer_app",
    .prepare_power_off = app_prepare_power_off,
    .quiesce = app_quiesce,
    .resume = app_resume,
    .app_resume = app_final_resume,
    .arg = &s_app_pm,
    .priority = PM_AP_POWER_PRIORITY_APPLICATION,
};

bk_err_t app_pm_init(void)
{
    return bk_pm_ap_power_ops_register(&s_app_power_ops);
}

bk_err_t app_pm_deinit(void)
{
    return bk_pm_ap_power_ops_unregister(&s_app_power_ops);
}
```

如果用户模块直接管理掉电外设，还需要成对实现 `backup` 和 `restore`。两个回调运行时
AP1已经离线且AP0全局中断关闭，只能操作寄存器和静态内存。禁止日志、动态内存、锁、
delay以及等待中断完成。对于复杂驱动，更推荐在保留内存中缓存有效配置，并在 `resume`
中复位控制器后按缓存重新初始化；不要恢复旧FIFO、BUSY、pending IRQ或被中断的事务。

仅需要最终业务恢复通知的应用可以只注册 `app_resume`：

```
static bk_err_t camera_app_resume(void *arg)
{
    camera_context_t *ctx = arg;

    camera_sync_state_with_cp();
    camera_restart_worker(ctx);
    return BK_OK;
}

static const pm_ap_power_ops_t s_camera_app_ops = {
    .name = "camera_app",
    .app_resume = camera_app_resume,
    .arg = &s_camera_context,
    .priority = PM_AP_POWER_PRIORITY_APPLICATION,
};
```

<a id="id14"></a>

## 失败和回滚

快速启动流程不会在前置条件不满足时强制关闭AP：

```
prepare/quiesce/backup/AP1 offline失败
                   |
                   v
      +--------------------------+
      | 不发布最终sleep ACK       |
      | 不切断AP电源              |
      +------------+-------------+
                   |
                   v
      +--------------------------+
      | restore已备份硬件         |
      | AP1重新online            |
      | 调用幂等resume            |
      +------------+-------------+
                   |
                   v
              恢复RUNNING
```

用户应按以下要求处理异常：

> - `prepare_power_off` 返回BUSY时让原任务继续排空，不在回调中等待。
> - `quiesce` 或 `backup` 返回错误时，本次AP关闭会取消；`resume` 必须能恢复入口。
> - `resume` 可能在真实唤醒和关闭失败回滚中执行，必须幂等。
> - `app_resume` 只在AP真实掉电并完成快速恢复后执行一次，不用于普通回滚。
> - PSRAM恢复失败时，保留数据和指针不再可信，应走冷启动回退并重建业务状态。
> - 回调失败后应保留错误日志和降级路径，不应继续启动依赖未恢复资源的业务。

<a id="id15"></a>

## 调试与验收

示例工程提供以下CP串口命令：

```
ap_fast_boot off
ap_fast_boot on
ap_fast_boot cycle
```

AP示例日志中的 `RESUME_PROOF` 可验证执行现场连续性：

> - `seq` 在恢复后继续递增。
> - `stack` 保持 `0x12345678`。
> - `heap_value` 保持 `0xA55A5AA5`。
> - `main_entries` 始终为1。

性能测试时重点关注：

> - `AP_TIME ap0_restore_scheduler_ready`：AP0恢复调度时间，10 ms目标使用该项判断。
> - `AP_TIME startup_success`：CP侧完整AP启动流程时间。
> - `AP_TIME cpu3_online`：AP1重新加入调度的时间。
> - 各 `AP_FAST_CB` 日志：回调名称、返回值和耗时。

建议至少执行1000次AP OFF/ON循环，并覆盖AP空闲、高负载、DMA活动、camera/ISP业务、
PSRAM大块读写以及Wi-Fi/BLE同时运行等场景。验收时同时确认：

> - 无HardFault、MemFault、UsageFault和spinlock错误。
> - AP主函数不重复执行，任务和内存数据连续。
> - AP1和依赖AP1的业务在ready后正常运行。
> - 无DMA或外设在AP掉电后继续访问PSRAM。
> - 快速恢复时间、低功耗电流和业务恢复时间满足产品要求。

<a id="id16"></a>

## 常见问题

<a id="ap-main"></a>

### AP恢复后又进入了 `main()`

说明本次走了冷启动或快速恢复回退。检查CP/AP配置是否一致、PSRAM retention是否成功、
DTCM上下文是否有效，以及日志中是否有restore、AP1或回调失败。

<a id="apoff"></a>

### AP投OFF票后没有掉电

其他模块可能仍持有AP ON票，或某个 `prepare_power_off` 一直返回BUSY。检查Wi-Fi、
BLE、多媒体投票，并在任务上下文使用PM调试信息定位未排空模块。

<a id="id17"></a>

### 恢复后变量正常但外设异常

这是典型的“软件状态保持、硬件状态丢失”。确认对应驱动已经实现
`quiesce/backup/restore/resume`，并且恢复时没有重复创建保留的mutex、queue、
semaphore或DMA通道。

<a id="ms"></a>

### 启动时间超过10 ms

先确认比较的是 `ap0_restore_scheduler_ready`，而不是包含AP1、用户回调或业务初始化的
总时间。关闭详细串口日志，检查PSRAM恢复、硬件 `restore` 回调和CP电源时序耗时。
任何同步日志、长时间回调或恢复阶段阻塞操作都会增加启动时间。

<a id="id18"></a>

## 相关代码和示例

> - 示例工程：`projects/pm/ap_fast_boot`
> - 回调接口：`ap/include/modules/pm.h`
> - AP回调编排：`ap/components/bk_pm/src/clients/bk_pm_client_ap_ctrl.c`
> - AP快速恢复流程：`ap/middleware/soc/bk7259_ap/hal/sys_pm_hal.c`
> - CPU上下文保存恢复：`ap/middleware/driver/deep_lv/deep_lv.c`
> - 驱动接入参考：`ap/middleware/driver/pwr_clk/i2c_ap_fast_pm_demo.c`
