---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7258/zh_CN/v3.1.1/developer-guide/interrupt/bk_interrupt.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: SMP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 中断管理

<a id="id2"></a>

## 概述

当前bk\_avdk\_smp支持bk7258(基于cortex-m33内核)，每个core有自身的NVIC(中断控制器)，同时所有的外部中断(比如外设产生的中断)可以路由到任意一个core上，结构如下：

<a id="id4"></a>
![Interrupt Overview](../../../../_assets/c25a0f844ee2a672be6a-interrupt_smp.png)


Interrupt Overview

整个中断处理框架可划分成三级:

> - 外设模块层级：各个外设独立控制中断的开关
> - 系统控制层级：由系统控制寄存器来决定某个外设的中断路由到哪一个core
> - Core层级 ：通过配置core内部的NVIC，来配置core对中断的具体行为（为了方便兼容不同的架构，软件实现了ICU (Interrupt Control Unit)模块）

1. 外设模块层级：

> 在 ARMINO 中，能产生中断的外设称为中断源，通常一个外设为一个中断源，与一个中断源宏 INT\_SRC\_DEV 对应，
> INT\_SRC\_DEV 中 DEV 表示外设名字，例如，GPIO 中断源宏为 INT\_SRC\_GPIO，SDIO 中断源为 INT\_SRC\_SDIO 等。
> SoC 支持的全部外设中断源请参考 int\_types.h 中 icu\_int\_src\_t 定义，相关API见各外设驱动。

备注

中断源与一个外设对应，而不是外设特定通道对应。

2. 系统控制层级：

系统控制层级提供了使能中断的功能，决定外部中断可以路由到哪一个CPU；接口位于middleware/driver/sys\_ctrl/sys\_driver.c，

对于CP系统，可调用如下的接口配置系统层级的中断：

```
int32 sys_drv_int_disable(uint32 param);
int32 sys_drv_int_enable(uint32 param);
int32 sys_drv_int_group2_disable(uint32 param);
int32 sys_drv_int_group2_enable(uint32 param);
```

对于AP系统，可调用如下的接口配置系统层级的中断：

```
int32 sys_drv_core_intr_group1_disable(uint32 core_id, uint32 param);
int32 sys_drv_core_intr_group1_enable(uint32 core_id, uint32 param);
int32 sys_drv_core_intr_group2_disable(uint32 core_id, uint32 param);
int32 sys_drv_core_intr_group2_enable(uint32 core_id, uint32 param);

以下是一个示例：(将USB中断路由到CPU2)

sys_drv_core_intr_group1_enable(CPU2_CORE_ID, USB_INTERRUPT_CTRL_BIT);
```

重要

*Note：对于bk7258,总共有64个外部中断，其中0-31属于group1,32-63属于group2*

3. Core层级的接口：

Core层级的中断控制器配置由于和CPU的架构相关，软件设计了一个中断管理的模块来统一管理，该模块被称为ICU (Interrupt Control Unit)，源码位于middleware/driver/icu
在ICU中设置了一张map表，用来记录当前所有的外部中断的信息，如中断号、默认优先级等。

> 同时提供了如下的API供应用层调用：

```
bk_err_t bk_int_isr_register(icu_int_src_t src, int_group_isr_t isr_callback, void*arg) 使能某个中断，配置为ICU_DEV_MAP中的优先级，并注册回调函数
bk_err_t bk_int_set_priority(icu_int_src_t int_src, uint32_t int_priority) 设置某个中断的优先级
bk_err_t bk_int_isr_unregister(icu_int_src_t src) 关闭某个中断
```

重要

配置某个外设的中断时，应该先调用bk\_int\_isr\_register注册对应的中断函数，再使能对应的外设中断位;
注销某个外设的中断则应该先关闭外设的中断，再调用bk\_int\_isr\_unregister函数。

OS适配层也提供了相应的中断屏蔽与解除屏蔽接口（对于cortex-m33内核，屏蔽期间只有NMI和hard fault可以响应）：

```
rtos_disable_int() 读取当前的中断屏蔽状态并屏蔽中断
void rtos_enable_int(uint32_t int_level)  解除中断屏蔽并恢复之前的中断屏蔽状态
```

<a id="id3"></a>

## 默认的中断初始化

中断的初始化在driver\_early\_init()中通过调用interrupt\_init()实现。
