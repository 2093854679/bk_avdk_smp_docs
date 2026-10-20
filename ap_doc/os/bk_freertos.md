---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/os/bk_freertos.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="freertos"></a>

# FreeRTOS 操作系统

<a id="id1"></a>

## 概述

> - FreeRTOS 是一个迷你的实时操作系统内核。
> - 作为一个轻量级的操作系统，功能包括：任务管理、时间管理、信号量、消息队列、内存管理、记录功能、软件定时器、协程等，可基本满足较小系统的需要。
> - FreeRTOS 能在小 RAM 单片机上运行，是完全免费的开源操作系统，具有源码公开、可移植、可裁减、调度策略灵活的特点，可以方便地移植到各种单片机上运行。
> - Armino 平台 AP 侧 SMP 使用内核路径 `components/os_source/freertos_smp_v2p0`，版本基于 FreeRTOS Kernel V10.4.x 系列。

<a id="id2"></a>

## 通用架构

> - 一个 FreeRTOS 系统主要由 BSP 驱动、内核与组件组成。内核包含多任务调度、内存管理与任务间通信；组件包含网络协议、外设支持等。
> - FreeRTOS 内核与组件均可剪裁。嵌入式应用对内存空间要求苛刻，可剪裁 RTOS 非常重要，这使得 FreeRTOS 核心代码仅约 9000 行。

<a id="id21"></a>
![FreeRTOS architecture](../../../_assets/c171dcc5675a754df546-freertos_arch.png)


FreeRTOS 架构

<a id="id3"></a>

## 功能与特点

> - 用户可配置内核功能
> - 多平台支持
> - 提供较高层次的代码完整性保障
> - 目标代码小，简单易用
> - 遵循 MISRA-C 编程规范
> - 强大的执行跟踪功能
> - 堆栈溢出检测
> - 任务数量与优先级无硬性上限
> - 多个任务可分配相同优先级
> - 支持队列、二进制信号量、计数信号量及递归互斥
> - 支持优先级继承
> - 免费开源

<a id="id4"></a>

## 小结

> - FreeRTOS 内核支持优先级调度，CPU 总是运行就绪态中优先级最高的任务；同时也支持同优先级任务的时间片轮转。
> - 内核可配置为可剥夺型或不可剥夺型：可剥夺型保证实时性；不可剥夺型可减少不必要的上下文切换。
> - FreeRTOS 兼具实时性、开源性、可靠性与易用性，已支持多种硬件平台。

<a id="freertos-smp"></a>

## FreeRTOS SMP 架构

<a id="smp"></a>

### SMP 简介

> - Armino 平台 AP 侧 FreeRTOS SMP 内核路径：`components/os_source/freertos_smp_v2p0`
> - Symmetric Multiprocessing（SMP）是多处理器系统中常见的对称多处理架构
> - BK7259 AP 支持 FreeRTOS SMP，运行在 CPU2 与 CPU3（AP 双核 SMP）
> - 以下介绍 SMP 基本概念，以及在 FreeRTOS 中实现 SMP 的目的与优势

<a id="id5"></a>

### SMP 基本概念

1. 多处理器系统：由多个处理器核心组成，每个核心可独立执行任务。
2. 对称性：所有核心地位对等，可执行相同任务并访问相同系统资源（含外设与内存）。
3. 共享内存：核心通过共享内存通信，需防止竞态条件等问题。

<a id="id6"></a>

### 实现 SMP 的目的与优势

1. 提高性能：多核并行执行任务，分担负载。
2. 任务并行执行：不同核心可独立运行不同任务，提高吞吐量。
3. 更好资源利用：充分利用多核硬件，适合实时与高负载场景。
4. 系统灵活性：可按需扩展处理能力。
5. 实时性能：有助于满足实时系统的时限要求。

实现 SMP 需处理核间同步、共享资源管理与任务调度等挑战。

<a id="id7"></a>

### 调度策略

<a id="id8"></a>

#### 概述

SMP 模式下任务调度仍遵循基于优先级的抢占式与时间片轮转策略，与单核架构一致。区别在于 SMP 版本为每个 core 维护独立调度器（各自拥有 tick 中断）。

单个 core 上的调度策略与单核类似，但需额外考虑 core id 配置为 `tskNO_AFFINITY` 的情形。总体策略：

> - 指定了 core id 的任务只在对应 core 上运行
> - core id 为 `tskNO_AFFINITY` 时，任务可能在任意 core 上运行

<a id="id22"></a>
![SMP schedule](../../../_assets/dbebd547eaedfbe80c2c-smp_schedule.png)


SMP 双核调度示意

<a id="id9"></a>

#### 任务优先级

创建任务时优先级数字越大，优先级越高。调度时从就绪列表选择当前最高优先级任务。

SMP 模式下每个核独立调度：选择可在该核运行且优先级最高的就绪任务。需满足：

> - 任务亲和性兼容（已分配给当前核，或 core id 为 `tskNO_AFFINITY`）
> - 任务当前未在其他核上运行

示例（数字越大优先级越高）：

> - 任务 A：优先级 8，分配给核 0
> - 任务 B：优先级 7，分配给核 0
> - 任务 C：优先级 6，分配给核 1

调度后任务 A 在核 0 运行，任务 C 在核 1 运行；任务 B 虽为第二高优先级，但仅分配给核 0 且核 0 已被占用，故不执行。

<a id="id10"></a>

#### 任务抢占

单核系统中，更高优先级任务就绪时可抢占当前任务。SMP 系统中，调度器可对单个核独立抢占。

若更高优先级就绪任务可在多个核运行，调度器通常只抢占一个核，并优先选择当前核。

示例：

> - 任务 A：优先级 6，当前在核 0 运行
> - 任务 B：优先级 7，当前在核 1 运行
> - 任务 C：优先级 8，未固定核，由任务 B 解除阻塞

调度后任务 A 继续在核 0 运行，任务 C 抢占任务 B。

<a id="id11"></a>

#### 任务时间片

单核模式下，同优先级多个就绪任务会轮转切换。SMP 下特定任务可能无法在特定核运行（已分配给其他核，或已在其他核运行），时间片策略因此与单核有差异。

核在就绪任务中搜索可运行任务时，可能跳过同优先级列表中的部分任务。SMP 调度器会将选中任务置于列表末尾，使同优先级任务获得更均衡的时间片。

备注

为实现理想时间片轮转，建议将需要严格时间分配的同一优先级任务分配到同一核。

<a id="id12"></a>

#### 滴答时钟

SMP 内核中每个核有独立 tick 中断，周期相同但可能不同步。核 0 与核 1 的处理有区别：

核 0 负责：

> - 递增内核 tick 计数
> - 检查超时任务并加入就绪列表
> - 检查时间片轮转
> - 执行应用层 tick 回调

核 1 仅检查是否需要任务切换，并执行应用 tick 钩子（如有）。

<a id="id13"></a>

#### 任务挂起与恢复

SMP 内核无法在多个核上同时挂起调度器，`vTaskSuspendAll()` 与 `xTaskResumeAll()` 只能在特定核上调用。

在某一核调用 `vTaskSuspendAll()` 时：

> - 仅在该核禁用任务切换，中断仍可响应
> - 该核不再响应阻塞或主动引发的调度，也不进行时间片轮转
> - 中断解除阻塞时，亲和性匹配的任务进入该核待执行列表
> - 所有核调度器均挂起时，由中断解除阻塞的任务进入其分配核的待执行列表
> - 若为 core 0，tick 计数暂停但挂起期间仍会计数，tick 中断仍会触发应用时钟

在某一核调用 `xTaskResumeAll()` 时，待执行列表中的任务恢复运行；若为 core 0，补偿挂起的 tick 计数。

<a id="id14"></a>

#### 空闲任务

SMP 系统为每个核创建独立空闲任务，行为与单核模式相同。

<a id="id15"></a>

#### 软件定时器

SMP 软件定时器默认创建在 Core0 上，并设置为最高优先级。

备注

若与软件定时器交互的任务也在 Core0，可视为同步调用；若任务可能运行在其他 core，则需根据业务自行处理同步。

<a id="id16"></a>

### 资源同步

<a id="id23"></a>
![SMP shared resources](../../../_assets/b71dbc5cb14b02d44ce9-smp_resource.png)


SMP 双核共享资源（SRAM / 外设经系统总线访问）

<a id="id24"></a>
![SMP resource sync](../../../_assets/e77ad09f6f292c124424-smp_resource_sync.png)


SMP 架构共享资源同步

1. Task 间：信号量（Semaphore）、互斥锁（Mutex）、关调度
2. ISR 间：自旋锁（SpinLock）
3. Task/ISR 间：自旋锁（SpinLock）

<a id="id17"></a>

### 自旋锁与临界区

<a id="id18"></a>

#### 自旋锁

SMP 系统中共享资源访问依赖自旋锁。自旋锁通过架构提供的原子指令实现，保证多核环境下的互斥。

静态自旋锁供应用层使用；动态自旋锁供内核对象使用，与对象生命周期绑定。所有自旋锁资源位于 `sram_spinlock_section` 段，由 `CONFIG_SPINLOCK_SECTION` 控制。

备注

动态自旋锁随内核对象申请而分配，仅在对象销毁后回收。

自旋锁 API（`middleware/driver/spinlock`）：

> - `spin_lock`：获取锁，未获取到则自旋
> - `spin_trylock`：尝试获取，返回 1 表示已占用，0 表示成功
> - `spin_unlock`：释放锁
> - `_spin_lock_irqsave`：关中断并获取锁
> - `_spin_unlock_irqrestore`：释放锁并恢复中断

备注

当前自旋锁支持最大 256 级嵌套。

应用层使用示例：

```
#ifdef CONFIG_SOC_SMP
#include "spinlock.h"
static SPINLOCK_SECTION volatile spinlock_t test_spin_lock = SPIN_LOCK_INIT;
#endif

spin_lock(&test_spin_lock);
/* 临界区 */
spin_unlock(&test_spin_lock);
```

备注

spinlock 必须放在 `SPINLOCK_SECTION` 段中。

<a id="id19"></a>

#### 临界区

单核架构下，临界区通过屏蔽中断防止抢占与 ISR 干扰。SMP 架构下仅关中断不足以保护内存、外设等共享资源，需结合自旋锁，即关中断 \+ 自旋锁。

OS 适配层（`include/os/os.h`，实现见 `rtos_pub_smp.c`）提供两套全局临界区接口，均支持嵌套：

> - `rtos_enter_critical()` / `rtos_exit_critical()`：使用 `rtos_spin_lock`，供 OS 抽象层及通用短临界区使用
> - `rtos_enter_global_critical()` / `rtos_exit_global_critical()`：使用 `rtos_global_spin_lock`；SMP 下 `GLOBAL_INT_DISABLE()` / `GLOBAL_INT_RESTORE()` 宏映射到这对接口，兼容驱动中大量遗留写法

使用方式：

1. 调用 OS 适配层 `rtos_enter_critical()` / ``` rtos_exit_critical()``（所有调用者共用 ``rtos_spin_lock ```）：

```
uint32_t flags = rtos_enter_critical();
/* 临界区 */
rtos_exit_critical(flags);
```

2. 调用 `rtos_enter_global_critical()` / ``` rtos_exit_global_critical()``（共用 ``rtos_global_spin_lock ```，等价于 SMP 下的 `GLOBAL_INT_DISABLE` / `GLOBAL_INT_RESTORE`）：

```
uint32_t irq_level;
GLOBAL_INT_DISABLE();   /* 或 irq_level = rtos_enter_global_critical(); */
/* 临界区 */
GLOBAL_INT_RESTORE();   /* 或 rtos_exit_global_critical(irq_level); */
```

3. 模块自定义锁并封装（适合高频访问、需与全局锁隔离的资源）：

```
static SPINLOCK_SECTION volatile spinlock_t xx_spin_lock = SPIN_LOCK_INIT;

static inline uint32_t xx_enter_critical(void)
{
    uint32_t flags = rtos_disable_int();
#ifdef CONFIG_FREERTOS_SMP
    spin_lock(&xx_spin_lock);
#endif
    return flags;
}

static inline void xx_exit_critical(uint32_t flags)
{
#ifdef CONFIG_FREERTOS_SMP
    spin_unlock(&xx_spin_lock);
#endif
    rtos_enable_int(flags);
}
```

备注

方式 1 / 2 适用于低频、短临界区；方式 3 适用于高频访问且需独立锁粒度的模块。非必要场景优先使用 mutex 而非临界区。开启 `CONFIG_ISR_DISABLE_TIME_STATISTIC` 时可通过 `ap_cmd critstat` 统计关中断时长。

临界区使用限制：

> - 临界区应尽可能短，过长会影响调度性能
> - 不应在临界区内调用 FreeRTOS API 或阻塞函数
> - 尽量将操作移到临界区外
> - 典型临界区仅访问少量数据结构或寄存器

<a id="api"></a>

## API 参考

应用层应调用 SDK OS 适配层 API，而非直接调用内核 API。适配层源码位于 `components/bk_rtos/freertos/v10/rtos_pub_smp.c`，头文件为 `include/os/os.h`。

详见：

- [OS 抽象层](bk_os_abstract.md)

<a id="id20"></a>

## 工程配置

BK7259 AP 默认 app 工程启用 SMP，典型配置如下：

```
CONFIG_CPU_CNT=2
CONFIG_SOC_SMP=y
CONFIG_FREERTOS_SMP=y
CONFIG_SPINLOCK_SECTION=y
```
