# AP/CP 异常 Dump 协同机制


## 1 功能概述

BK7259 的 AP/CP 异常 Dump 采用协同方式处理 AP 异常场景。AP 异常后不再长时间独占 UART0 输出完整内存 Dump，而是只输出 AP CPU 寄存器和 AP 系统调试信息，然后释放 UART0 硬件 HSPL，由 CP 接管 UART0 输出 AP 内存窗口，最后由 CP 触发整板重启。

该机制主要解决 AP Dump 时间较长时，CP 因 AP 心跳超时或 AON WDT 超时提前复位单板的问题。

整体流程如下：


```
AP exception
    |
    |-- lock UART0 HSPL
    |-- dump AP CPU registers
    |-- publish AP runtime dump windows to shared memory
    |-- notify CP: IPC_AP_TRAP_HANDLE_BEGIN
    |-- dump AP task/backtrace/runtime debug info
    |-- unlock UART0 HSPL
    |-- notify CP: IPC_AP_TRAP_HANDLE_END
    |-- wait for CP reboot

CP receives IPC_AP_TRAP_HANDLE_END
    |
    |-- lock UART0 HSPL
    |-- dump AP memory windows
    |-- unlock UART0 HSPL
    |-- bk_wdt_force_reboot()

```


## 2 AP 侧处理流程

AP 异常入口位于：

> - `ap/components/coredump/bk_coredump.c`

AP 异常后的主要顺序为：

> - `bk_coredump_writer_init()` 获取 UART log HSPL。
> - `bk_coredump_meta_info()` 输出异常原因、构建信息等。
> - `bk_coredump_registers()` 输出 AP CPU 寄存器和 fault 相关寄存器。
> - `coredump_publish_ap_psram_windows()` 将 AP 实际使用的 PSRAM data/bss 窗口发布到共享寄存器。
> - `ipc_send_trap_handle_begin()` 通知 CP 进入 AP Dump 保护状态。
> - `coredump_prompt_info()` 输出 AP task/backtrace/runtime 等系统调试信息。
> - `bk_coredump_writer_deinit()` 释放 UART log HSPL。
> - `ipc_send_trap_handle_end()` 通知 CP 可以接管 UART 并 Dump AP 内存。
> - AP 停留在等待状态，由 CP 完成 Dump 后重启单板。

AP 异常路径中不再调用 `bk_coredump_memory()`，因此 AP 不再直接输出 AP 全内存 Dump。


## 3 CP 侧处理流程

CP 通过 mailbox 接收 AP trap 通知，处理入口位于：

> - `cp/middleware/driver/mailbox/mb_ipc_cmd.c`

当 CP 收到 `IPC_AP_TRAP_HANDLE_BEGIN` 时：

> - 设置 `g_ap_dump_flag = 1`。
> - 屏蔽 CP 大部分中断，降低 CP 抢占 UART 或进入异常路径的概率。
> - 调用 `mb_ipc_dump_notify(..., 1)`，使 heartbeat timeout 逻辑识别 AP 正在 Dump，避免因为 AP 无心跳而触发复位。
> - 如果启用 `CONFIG_SHELL_ASYNCLOG`，将 shell log CPU 切换到 AP Dump CPU。

当 CP 收到 `IPC_AP_TRAP_HANDLE_END` 时：

> - 调用 `bk_coredump_dump_ap_memory_for_trap()` 接管 UART0 并 Dump AP 内存窗口。
> - AP 内存 Dump 完成后清除 `g_ap_dump_flag` 和 heartbeat dump 状态。
> - 调用 `bk_wdt_force_reboot()` 触发整板重启。

CP 接管 Dump 的入口位于：

> - `cp/components/coredump/bk_coredump.c`

AP 内存窗口 Dump 逻辑位于：

> - `cp/components/coredump/bk_coredump_mem.c`
> - `cp/middleware/soc/bk7259/memory.c`


## 4 UART0 HSPL 管理

AP 和 CP 的 coredump UART writer 都使用 `BK_HSPL_RES_UART_LOG` 保护 UART0 输出。

相关文件：

> - `ap/components/coredump/bk_coredump_uart.c`
> - `cp/components/coredump/bk_coredump_uart.c`
> - `ap/middleware/driver/aspl/aspl_lock.c`
> - `cp/middleware/driver/aspl/aspl_lock.c`

当前机制要求：

> - AP 异常后先获取 UART0 HSPL，完成寄存器和任务信息输出。
> - AP 输出完成后必须释放 UART0 HSPL。
> - CP 在 `IPC_AP_TRAP_HANDLE_END` 后再获取 UART0 HSPL，输出 AP 内存。
> - CP Dump 完成后释放 UART0 HSPL，再触发 WDT reboot。


## 5 AP 内存 Dump 范围

CP 接管后 Dump 的 AP 内存窗口对齐 AP `CONFIG_MEMDUMP_ALL` 的语义，但避免输出无效的大块空数据。

当前 CP 接管 AP Dump 的顺序为：

> - AP SRAM bank：按 `bk7259_sram_info` 顺序 Dump `SRAM0` ~ `SRAM6`
> - AP runtime 注册的额外 Dump 内存：`AP_EXTRA_MEM`
> - AP 实际使用的 PSRAM 窗口：
>
>   - `AP_PSRAM_HEAP`
>   - `AP_PSRAM_DATA`
>   - `AP_PSRAM_BSS`
> - AP 外设寄存器窗口

其中 `CONFIG_AP_PSRAM_CODE_SECTION_ADDR` 对应的 AP PSRAM code section 不做 Dump，避免输出大量代码段数据并拉长异常处理时间。

AP PSRAM data/bss 不按 `CONFIG_AP_PSRAM_DATA_SECTION_SIZE` 整段 Dump，而是由 AP 在异常时发布实际使用窗口，CP 只按共享窗口输出，减少空数据。


## 6 共享寄存器

AP/CP 通过 `sys_sw_regs` 共享 Dump 窗口信息。共享结构位于 `.shared_memory`，固定大小为 `1024` 字节。

相关文件：

> - `ap/middleware/driver/sys_sw_regs/sys_sw_regs.h`
> - `ap/middleware/driver/sys_sw_regs/sys_sw_regs.c`
> - `cp/middleware/driver/sys_sw_regs/sys_sw_regs.h`
> - `cp/middleware/driver/sys_sw_regs/sys_sw_regs.c`

当前用于 AP Dump 的共享信息包括：

> - `ap_heap_dump[]`：发布 AP heap、AP PSRAM data/bss 等窗口。
> - `ap_extra_dump[]`：发布 `rtos_regist_plat_dump_hook()` 注册的 AP 额外 Dump 内存。

AP 侧 `rtos_regist_plat_dump_hook()` 仍保留本地列表，同时把合法窗口同步写入 `sys_sw_regs`，供 CP 在 AP 异常后读取。

CP 读取共享窗口后会做最小范围检查：

> - 地址非零。
> - size 非零。
> - 地址范围没有溢出。
> - 窗口位于 CP 可访问的 AP SRAM、AP PSRAM 或外设寄存器范围内。


## 7 维护注意事项

> - `sys_sw_regs_t` 是 AP/CP 共享 ABI，新增字段必须同步修改 AP/CP 两侧头文件。
> - `.shared_memory` 固定为 `1024` 字节，扩展共享结构时必须关注链接脚本断言。
> - AP 侧异常路径已经关闭中断，释放 UART HSPL 时不能恢复 AP 中断。
> - CP 在 AP 内存 Dump 完成前不要清除 heartbeat dump 状态，否则可能重新触发 heartbeat timeout。
> - AP 和 CP 的外设寄存器表应保持一致，避免 CP 接管 Dump 时遗漏 AP 侧关注的外设状态。
> - `CONFIG_AP_PSRAM_CODE_SECTION_ADDR` 区域不参与 AP 异常内存 Dump。
