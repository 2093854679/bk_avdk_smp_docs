---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_ipi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ipi"></a>

# IPI

<a id="id1"></a>

## IPI 简介

IPI（Inter-Processor Interrupt，处理器间中断）用于在多核系统中让一个 CPU core 向另一个 CPU core 发送中断通知。它适合用作轻量级 doorbell：发送方通过 IPI 唤醒目标 core，目标 core 在 IPI 中断中读取少量事件信息，或进一步到共享内存、状态位图中处理真正的数据。

在 BK7259 的 CP \+ AP SMP 架构中，IPI 可以用于以下场景：

> - AP/CP 之间的轻量通知，例如心跳通知。
> - AP 内部 SMP core 之间的调度通知，例如 CPU2 与 CPU3 之间的 cross-core yield。
> - CP 内部 SMP core 之间的调度通知，例如 CPU0 与 CPU1 之间的 cross-core yield。
> - USB RISC-V bridge 等需要从协处理器通知 AP 的场景。
> - CLI 或驱动测试场景。

备注

IPI 不是数据 FIFO。IPI 硬件每个目标 core 只有 pending/value 语义，不适合承载大量数据或连续队列数据。软件设计上应将 IPI 作为 doorbell 使用，把持久状态、命令位图或大块数据放在共享内存中。

<a id="id2"></a>

## IPI 硬件与软件设计机制

IPI 硬件提供按目标 core 触发中断的能力。发送方写入一个 32 bit value 并触发目标 core 的 IPI 中断，接收方在 IPI ISR 中读取 value 并清除 pending 状态。

由于硬件 IPI 通道不是 FIFO，也不是为每个业务模块提供独立逻辑通道，因此软件层在 IPI driver 中引入了 domain 复用机制。所有公共 IPI 用户都使用 domain 编码格式发送 IPI，IPI driver 在统一 ISR 中解析 value，并根据 domain 分发到对应软件模块注册的 callback。

IPI value 的编码格式如下：

> - bit 30..27：source CPU ID，表示发送 IPI 的 CPU core。
> - bit 26..24：software domain，表示 IPI 属于哪个软件模块。
> - bit 23..16：event ID，表示 domain 内部定义的事件类型。
> - bit 15..0：payload，表示 domain 内部自定义的紧凑参数。

编码和解析由公共宏完成：

```
IPI_VALUE_MAKE(src, domain, event, payload)
IPI_VALUE_GET_SRC(value)
IPI_VALUE_GET_DOMAIN(value)
IPI_VALUE_GET_EVENT(value)
IPI_VALUE_GET_PAYLOAD(value)
```

Domain 机制的核心目标是避免多个模块直接抢占同一个 IPI 硬件回调。各模块只注册自己的 domain callback，IPI driver 统一负责硬件 ISR、value 解析和 callback 分发。

<a id="domain"></a>

## 当前 Domain 使用情况

当前软件中已经分配的 IPI domain 及其使用方式如下：

| Domain | 值 | 使用模块 | event 含义 | payload 含义 |
| --- | --- | --- | --- | --- |
| `IPI_DOMAIN_RESERVED` | 0 | 保留 | 不使用 | 不使用 |
| `IPI_DOMAIN_HEARTBEAT` | 1 | AP/CP heartbeat | 心跳事件，如 power up/heart | 当前事件的轻量参数，通常为 0 或事件附加值 |
| `IPI_DOMAIN_SMP` | 2 | FreeRTOS SMP cross-core notify | SMP doorbell 事件 | 发送方 CPU core ID |
| `IPI_DOMAIN_USB` | 3 | USB RISC-V bridge | USB 中断/通知事件 | USB bridge 传递的紧凑状态或序号 |
| `IPI_DOMAIN_TEST` | 7 | IPI CLI、HSPL test | 测试模块自定义事件 | 测试模块自定义参数 |

各 domain 的典型使用方式如下：

> - `IPI_DOMAIN_HEARTBEAT`：AP 侧 heartbeat 任务通过 IPI 向 CP 侧发送 power up 和周期 heartbeat 通知，CP 侧注册 heartbeat callback 后复用原有心跳状态机处理通知。
> - `IPI_DOMAIN_SMP`：AP 或 CP 各自的 SMP port 使用该 domain 作为双核之间的调度 doorbell。IPI 的 payload 只携带发送方 core ID，具体命令仍通过 `crosscore_mb_cmd[]` 位图传递。
> - `IPI_DOMAIN_USB`：RISC-V USB firmware 通过该 domain 通知 AP 侧 USB host/device driver，实际 USB 状态和数据由 USB bridge 的共享状态维护。
> - `IPI_DOMAIN_TEST`：IPI CLI 和 HSPL test 使用该 domain 做收发验证或压力测试，event/payload 由测试代码自行定义。

新增 IPI 用户时不建议复用已有业务 domain。如果确实属于已有 domain 的子事件，应在该 domain 内定义明确 event，并确认不会和现有事件冲突。

<a id="id3"></a>

## IPI 初始化流程

IPI driver 通过 `bk_ipi_driver_init()` 完成初始化，主要工作包括：

> - 初始化 IPI HAL。
> - 清除所有 core 的 pending 状态。
> - 注册 IPI 中断处理函数。
> - 打开对应 CPU core 的 IPI 中断路由。
> - 根据配置注册 IPI CLI 测试命令。

系统公共 driver 初始化阶段会在 `CONFIG_IPI` 使能时调用 `bk_ipi_driver_init()`。业务模块在注册 domain callback 前，需要确保 IPI driver 已经初始化完成。

如果某个模块在调度器启动早期就需要 IPI，例如 FreeRTOS SMP cross-core doorbell，则必须保证 `bk_ipi_driver_init()` 早于该模块的 domain callback 注册。

<a id="smp-cross-core-ipi"></a>

## SMP cross-core IPI 通知机制

FreeRTOS SMP 的 cross-core notify 原本使用 mailbox 作为 doorbell。改为 IPI 后，软件命令传递方式不变，IPI 只替代硬件通知路径。

发送侧流程如下：

1. 发送 core 调用 `crosscore_int_send(xCoreID, cmd)`。
2. 在关中断和 spinlock 保护下，将命令记录到 `crosscore_mb_cmd[]` 位图。
3. 设置 `crosscore_mb_busy[]`，用于合并连续通知。
4. 如果旧 busy 状态为 0，则发送 `IPI_DOMAIN_SMP` IPI doorbell。
5. 如果旧 busy 状态不为 0，则只累加命令位图，不重复触发硬件 IPI。

接收侧流程如下：

1. 目标 core 进入 IPI ISR。
2. IPI driver 解析 domain/event/payload。
3. 当 domain 为 `IPI_DOMAIN_SMP` 时，调用 SMP 注册的 callback。
4. SMP callback 校验 event 后，将 payload 中携带的 source core 转换为兼容旧 mailbox ISR 的 `mailbox_data_t`。
5. 复用原有 `crosscore_mb_rx_isr()` 读取 `crosscore_mb_cmd[]`，清 busy，并执行 yield、DWT、hotplug 等动作。

因此，IPI 方案中真正的 SMP 命令仍由共享位图承载，IPI 只负责通知目标 core “有命令需要处理”。

<a id="id4"></a>

## 配置宏说明

IPI 相关配置宏如下：

> - `CONFIG_IPI`：IPI driver 总开关，打开后编译并初始化 IPI driver。
> - `CONFIG_IPI_TEST`：IPI CLI 测试开关，依赖 `CONFIG_IPI` 和 `CONFIG_DRIVER_TEST`。
> - `CONFIG_IPI_DUMP`：打开 `bk_ipi_dump_info()` 调试接口，便于查看 IPI driver 和 domain callback 注册状态。

基于 IPI 的业务功能配置如下：

> - `CONFIG_SLAVE_HEART_BEAT_USE_IPI`：心跳机制使用 `IPI_DOMAIN_HEARTBEAT`，关闭时保留 mailbox 心跳路径。
> - `CONFIG_FREERTOS_SMP_CROSS_CORE_IPI`：FreeRTOS SMP cross-core notify 使用 `IPI_DOMAIN_SMP`，关闭时保留 mailbox doorbell 路径。
> - `CONFIG_USB_RISCV_BRIDGE`：USB RISC-V bridge 使用 `IPI_DOMAIN_USB` 通知 AP。

默认配置中，IPI driver 可以独立打开，但心跳和 SMP cross-core notify 是否使用 IPI 由各自独立宏控制，便于按模块验证和回退。

<a id="ipi-api"></a>

## IPI API 使用说明

`bk_err_t bk_ipi_driver_init(void);`
:   初始化 IPI driver，注册 IPI ISR 并使能对应 core 的 IPI 中断路由。重复调用会直接返回 `BK_OK`。

`bk_err_t bk_ipi_driver_deinit(void);`
:   反初始化 IPI driver，清除 domain callback 并关闭 IPI 中断。

`bk_err_t bk_ipi_send_domain(ipi_core_id_t core_id, ipi_domain_t domain, uint8_t event, uint16_t payload);`
:   向目标 core 发送一个 domain 编码的 IPI。`core_id` 为目标 core，`domain` 表示软件通道，`event` 和 `payload` 由 domain 用户自行定义。

`uint32_t bk_ipi_get_status(ipi_core_id_t core_id);`
:   获取指定 core 的 IPI pending 状态。

`uint32_t bk_ipi_get_all_status(void);`
:   获取所有 core 的 IPI pending 状态位图。

`bk_err_t bk_ipi_clear(ipi_core_id_t core_id);`
:   清除指定 core 的 IPI pending 状态。

`bk_err_t bk_ipi_enable(ipi_core_id_t core_id);`
:   使能指定 core 的 IPI 中断。

`bk_err_t bk_ipi_disable(ipi_core_id_t core_id);`
:   关闭指定 core 的 IPI 中断。

`bk_err_t bk_ipi_register_domain_callback(ipi_domain_t domain, ipi_domain_callback_t callback, void *param);`
:   注册 domain callback。IPI ISR 解析到对应 domain 后会调用该 callback。注册前必须保证 IPI driver 已初始化。

`bk_err_t bk_ipi_unregister_domain_callback(ipi_domain_t domain);`
:   取消注册 domain callback。

`uint32_t bk_ipi_get_device_status(void);`
:   获取 IPI 设备状态寄存器值。

`void bk_ipi_dump_info(void);`
:   打印 IPI driver 初始化状态和各 domain callback 注册状态。该接口仅在 `CONFIG_IPI_DUMP` 打开时可用。

<a id="domain-callback"></a>

## Domain Callback 说明

Domain callback 类型如下：

```
typedef void (*ipi_domain_callback_t)(ipi_core_id_t core_id,
                                      uint32_t value,
                                      uint8_t src_cpu,
                                      uint8_t event,
                                      uint16_t payload,
                                      void *param);
```

参数说明：

> - `core_id`：当前 pending 的目标 core/channel。
> - `value`：原始 32 bit IPI value。
> - `src_cpu`：发送方 CPU ID。
> - `event`：domain 内事件 ID。
> - `payload`：domain 内紧凑参数。
> - `param`：注册 callback 时传入的用户参数。

Callback 在 IPI ISR 上下文执行，应避免复杂处理、阻塞等待、大量日志打印或耗时操作。推荐在 callback 中只完成状态记录、位图更新、轻量唤醒等操作。

<a id="id5"></a>

## 使用注意事项

1. IPI 是 doorbell，不是数据通道。需要可靠保存的数据应放在共享内存或模块自己的状态结构中。
2. 同一个 domain 只能注册一个 callback，多个模块不能共用同一个 domain。
3. 新增 IPI 用户时，应优先申请新的 domain 或在已有 domain 内定义清晰的 event。
4. IPI value 只有 16 bit payload，不适合直接传递指针、大块数据或复杂结构。
5. IPI callback 运行在中断上下文，应保持短小，避免影响系统实时性。
6. 高频路径，例如 SMP cross-core notify，不建议在 callback 中打印日志；调试时可使用计数器或低频采样打印。
7. 如果模块在调度器启动早期使用 IPI，必须确认 IPI driver 初始化早于 domain callback 注册。
