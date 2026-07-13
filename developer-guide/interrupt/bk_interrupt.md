# 中断管理



## 概述

BK7259 为四核 AP+CP 架构：CPU0/CPU1 归属 CP 子系统，CPU2/CPU3 归属 AP 子系统。

**每个核各自拥有独立的 NVIC**；片上 64 路外部中断经系统控制寄存器路由后，可送达任意一个核处理。
整体关系如下：

![BK7259 中断路由概览](../_images/interrupt_smp.png)

BK7259 中断路由概览

从硬件到驱动的处理链路可划分为三级：

> - **外设模块层级**：各外设驱动控制本模块中断源的开关
> - **系统控制层级**：系统控制寄存器决定某路外部中断路由到哪一个核
> - **Core 层级**：各核内部 NVIC 完成优先级、向量等硬件行为；软件侧通过 **ICU** 模块统一封装（ICU 为软件抽象，不是片上硬件模块）

配置中断时通常按 **ICU 注册 ISR → 系统路由 → 外设使能** 的顺序进行；注销时顺序相反。


## 1. 外设模块层级

在 ARMINO 中，能产生中断的外设称为**中断源**，通常一个外设对应一个中断源，与 `INT_SRC_<DEV>` 宏一一对应。
例如 GPIO 为 `INT_SRC_GPIO`，UART0 为 `INT_SRC_UART0`。
全部中断源枚举见 `include/driver/int_types.h` （`icu_int_src_t`）；各外设的具体使能/关闭接口见对应驱动。

备注

中断源按**外设**划分，而不是按外设的某个通道划分。


## 2. 系统控制层级

系统控制层级负责将外部中断路由到目标核，接口位于 `middleware/driver/sys_ctrl/` （`sys_int_driver.c` / `sys_driver.h`）。

BK7259 共有 **64** 路外部中断：IRQ **0–31** 属于 **group1**，IRQ **32–63** 属于 **group2**。
`INT_SRC_*` 枚举值与 IRQ 编号一一对应，可直接作为 `int_num` 参数使用。


### 推荐接口（BK7259）

BK7259 上应优先使用 `sys_drv_set_int_en()` 完成按核路由：


```
int32_t sys_drv_set_int_en(uint32_t core_id, uint32_t int_num, uint32_t int_en);

```

`core_id` 为 SoC 物理核 ID （`CPU0_CORE_ID` … `CPU3_CORE_ID`，或 `rtos_get_core_id()`）；
`int_num` 为 `icu_int_src_t` / `INT_SRC_*` 中断源编号；
`int_en` 为 `1` （使能路由到该核）或 `0` （关闭）。

示例：将 UART0 中断路由到 AP 主核 CPU2：


```
sys_drv_set_int_en(CPU2_CORE_ID, INT_SRC_UART0, 1);

```

若希望路由到**当前运行核**，可将 `core_id` 设为 `rtos_get_core_id()`。
AP SMP 场景下，许多驱动默认把外设中断固定在 CPU2 （主核）；CP 侧常见写法类似，默认使用 CPU0。

备注

该接口同时适用于 AP 与 CP。AP/CP 的 `sys_hal_core_int_group*_enable()` 在 BK7259 上为空实现（待移除），不应再使用 `sys_drv_core_intr_group*_` 系列接口。


### 兼容接口（逐步淘汰）

部分旧驱动仍使用按位掩码操作的接口，以**当前运行核**为上下文（内部调用 `rtos_get_core_id()`）：


```
int32 sys_drv_int_disable(uint32 param);
int32 sys_drv_int_enable(uint32 param);
int32 sys_drv_int_group2_disable(uint32 param);
int32 sys_drv_int_group2_enable(uint32 param);

```

其中 `param` 为 `*_INTERRUPT_CTRL_BIT` 位掩码，而非 `INT_SRC_*` 枚举值。
新代码请统一改用 `sys_drv_set_int_en()`。


## 3. Core 层级与 ICU 软件抽象

各核内部的 **NVIC** 由架构相关代码初始化（如 `soc_isr_init()`）。
为屏蔽不同 CPU 架构差异、统一管理 ISR 注册与优先级，驱动层提供 **ICU（Interrupt Control Unit）** 软件模块，源码位于 `middleware/driver/icu/`。
ICU 维护一张映射表，记录中断源、默认优先级等信息，并对上层暴露统一 API：


```
bk_err_t bk_int_isr_register(icu_int_src_t src, int_group_isr_t isr_callback, void *arg);
bk_err_t bk_int_set_priority(icu_int_src_t int_src, uint32_t int_priority);
bk_err_t bk_int_isr_unregister(icu_int_src_t src);

```

重要

配置外设中断：应先调用 `bk_int_isr_register` 注册回调，再调用 `sys_drv_set_int_en` 完成路由，最后在对应外设驱动中使能中断位。
注销时：应先关闭外设中断，再 `sys_drv_set_int_en(..., 0)`，最后调用 `bk_int_isr_unregister`。


## OS 中断屏蔽接口

OS 抽象层提供临界区常用的中断屏蔽/恢复接口。屏蔽期间仅 NMI、HardFault 等不可屏蔽异常可响应：


```
uint32_t rtos_disable_int(void);          /* 屏蔽中断并返回先前状态 */
void rtos_enable_int(uint32_t int_level); /* 恢复先前中断屏蔽状态 */

```


## 默认初始化

中断子系统在启动早期完成初始化：`components_early_init()` 中调用 `interrupt_init()` （`middleware/driver/icu/interrupt_base.c`），
随后各外设驱动在 `driver_init()` 路径中按需 `bk_int_isr_register` 并通过 `sys_drv_set_int_en` 路由各自的中断源。
