---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/debug_trace/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 系统调试

<a id="arminoap"></a>

## **Armino平台AP系统调试命令**

BK7259 为 CP\+AP 双系统架构。日常调试时，串口连接在 CP 侧（`bk7259` defconfig 默认
`CONFIG_UART_PRINT_PORT=0`，即 DL\_UART0，波特率 115200）。AP 侧命令需通过 CP 串口以
`ap_cmd` 前缀转发。

<a id="id2"></a>

### 日志输出

详细机制见 [系统日志](error_log/bk_log.md)，此处仅列与调试相关的要点：

- 默认路径（`bk7259_ap.defconfig`）：`CONFIG_SYS_PRINT_DEV_MAILBOX=y`，AP log
  经 mailbox 转发到 CP，再由 CP 的 log 串口输出。
- AP 直连 UART（可选）：在 menuconfig 关闭 mailbox 打印、开启 UART 打印并指定 CONFIG\_UART\_PRINT\_PORT（AP defconfig 默认 5，与 CP UART0 不同）。
- Log 前缀：正常运行时 AP 日志带 `ap0` 与 `ap1` 标签（分别对应 AP 的 core0 /
  core1，即 CPU2 与 CPU3）；异常 dump 日志不带此前缀。CP 日志不带 cpu/ap 标签。
- 异步 log：默认开启 `CONFIG_SHELL_ASYNCLOG`；缓存耗尽时会出现 `INSRT:` 前缀的
  插入式输出。可用 `log [echo] [level] [sync] [whitelist]` 查看或调整配置。

<a id="cli"></a>

### 串口 CLI

CP 侧内置命令（直接在 CP 串口输入）：

```
help
log 1 3 0
ap_cmd help
```

AP 侧命令（在 CP 串口通过 `ap_cmd` 转发，SMP 工程必选此前缀）：

```
ap_cmd help
ap_cmd log
ap_cmd memshow
ap_cmd backtrace
ap_cmd critstat status
```

备注

`ap_cmd` 由 CP 的 `cli_cpu1_command()` 经 mailbox 转发到 AP shell 执行
（需 `CONFIG_SHELL_ASYNCLOG` 与 `CONFIG_MAILBOX`）。实际可用命令随工程
`menuconfig` 变化，以 `ap_cmd help` 实时输出为准，不要依赖旧文档中的
静态命令列表。

常见 AP 调试命令（需 `ap_cmd` 前缀）包括：

| 命令 | 说明 |
| --- | --- |
| `help` / `log` | 查看命令列表、调整 log 级别与同步模式 |
| `memshow` / `memleak` / `memhistory` / `memtrace` | 堆内存查看与 UAF 辅助（见本文末「AP 内置调试特性」） |
| `tasklist` / `backtrace` / `osinfo` / `cpuload` | 任务、调用栈与运行时信息 |
| `critstat status|set|dump` | 临界区中断屏蔽统计（需 `CONFIG_ISR_DISABLE_TIME_STATISTIC`） |
| `dwtf` / `dwtdw` / `dwtdd` / `dwti` | DWT 调试（见下文 DWT 章节） |
| `setswdmode` | 请求 CP 切换 SWD 调试口（见下文 SWD 章节） |

<a id="ate-uart"></a>

### ATE 模式下的 UART 切换（可选）

若工程启用 ATE 相关配置，可通过以下宏指定 ATE 检测管脚与 log 口切换行为：

- `CONFIG_UART_ATE_PORT`：ATE 模式检测管脚
- `CONFIG_UART_PRINT_PORT`：正常运行时 log UART
- `CONFIG_UART_ATE_PRINT_PORT`：进入 ATE 后切换到的 log UART

示例：ATE 用 UART1 TX 识别，正常运行 log 走 UART1，进 ATE 后 log/命令行走 UART0:

```
CONFIG_UART_ATE_PORT=1
CONFIG_UART_PRINT_PORT=1
CONFIG_UART_ATE_PRINT_PORT=0
```

<a id="dwt-data-watchpoint-and-trace"></a>

<a id="ap-dwt-debug"></a>

## **DWT 调试 (Data Watchpoint and Trace)**

<a id="id3"></a>

### 功能简介

DWT（Data Watchpoint and Trace）是 ARM Cortex-M 内核内置的调试单元，可在\*\*不连接 JLink 等外部调试器\*\*的情况下，
通过串口 CLI 实现类似硬件断点 / watchpoint 的调试能力。

主要功能包括：

- **周期计数（CYCCNT）**：精确统计 CPU 时钟周期，用于测量 CPU 运行频率
- **数据 watchpoint**：监控指定内存地址的读、写或读写访问
- **数据范围 watchpoint**：监控一段连续地址范围内的访问（`dwtdr`，非 SMP 模式下可用）
- **条件 watchpoint**：仅当向某地址写入特定值时才触发
- **指令 watchpoint**：监控 CPU 执行到某条指令地址时触发（类似硬件断点）

典型应用场景：

- 定位「谁在什么时候改写了某个变量」
- 监控关键标志位被写成特定值的时机
- 确认某段代码是否被执行
- 在无 JLink 环境下快速测量 CPU 频率

<a id="id4"></a>

### 软件架构

AP 侧调用链路:

```
串口 CLI (cli_dwt.c)
    → DWT 驱动 (ap/middleware/arch/cortex-m/dwt.c)
    → 配置 DWT 比较器 + 开启 Debug Monitor 模式
    → 命中时触发 DebugMon 异常
    → soc_debugmon_handler() → dump 系统信息
```

CP 侧调用链路类似，源码位于 `cp/components/bk_cli/cli_dwt.c` 和 `cp/middleware/arch/cortex-m/dwt.c`。

<a id="id5"></a>

### 工作原理

1. 通过 `DCB->DEMCR` 开启 Debug Monitor 模式（`MON_EN`）和 DWT 跟踪（`TRCENA`）
2. 配置 DWT 比较器（`COMP0~3` \+ `FUNCTION0~3`）设置监控条件
3. 当 CPU 访问/执行命中条件时，产生 Debug Event
4. 进入 Debug Monitor 异常（异常号 12），平台默认 handler 会 dump 寄存器、backtrace 和内存

备注

DWT CLI 使用的是 Debug Monitor 模式（无需 halt CPU），与 JLink SWD Halt 调试模式不同。
两者同时使用时可能冲突，建议按需选择其一。

<a id="ap-smp"></a>

### AP SMP 差异

BK7259 AP 开启 SMP 后，数据 watchpoint（`dwtdw`/`dwtdd`）会通过 IPI 同步到所有核，
确保任意核上的匹配访问都能被捕获。指令 watchpoint（`dwti`）仅在执行 CLI 命令的核上生效。

<a id="cli-cli-dwt"></a>

### CLI 命令 (cli\_dwt)

AP 侧通过 `cli_dwt.c` 将上述 DWT 能力封装为串口 shell 命令。

<a id="id6"></a>

### 编译与注册条件

- `CONFIG_CLI=y`：启用 CLI 组件
- `CONFIG_ARCH_CORTEX_M=y`：Cortex-M 架构（编译 `cli_dwt.c`）
- `CONFIG_DRV_CLI_SUPPORT=y`：通过 `DRV_CLI_CMD_EXPORT` 自动注册命令

BK7259 AP 开启 SMP（`CONFIG_SOC_SMP=y`），数据 watchpoint 会通过 IPI 同步到各核。

<a id="id7"></a>

### 命令列表

AP SMP 模式下可用命令如下（与非 SMP 的 `dwtd`/`dwtdr` 不同）：

| 命令 | 格式 | 功能 |
| --- | --- | --- |
| `dwtf` | `dwtf <ms>` | 用 DWT 周期计数器测量 CPU 频率（ms 为十进制） |
| `dwtdw` | `dwtdw 0x<addr>` | 监控指定地址被写入 |
| `dwtdd` | `dwtdd 0x<addr> 0x<value>` | 监控向地址写入指定值 |
| `dwti` | `dwti 0x<instruction_addr>` | 监控指令地址被执行 |

<a id="id8"></a>

### 参数格式

- 地址和数值参数必须使用 `0x` 前缀的十六进制格式，例如 `0x281a9070`
- `dwtf` 的时间参数 `<ms>` 为十进制，例如 `dwtf 100`

<a id="id9"></a>

### 使用示例

以下示例均通过 CP 串口输入，使用 `ap_cmd` 前缀。触发 watchpoint 写内存时可使用
memset（需 `CONFIG_DEBUG_VERSION`）或 memset\_pattern：

测量 CPU 频率（无副作用）:

```
ap_cmd dwtf 100
```

设置数据写 watchpoint 并触发 dump:

```
ap_cmd memshow
ap_cmd dwtdw 0x281a9070
ap_cmd memset_pattern 0x281a9070 0x4 0x55
```

设置条件 watchpoint（仅匹配值时触发）:

```
ap_cmd dwtdd 0x281a9070 0xAABBCCDD
ap_cmd memset_pattern 0x281a9070 0x4 0x11        # 不匹配，不 dump
ap_cmd memset_pattern 0x281a9070 0x4 0xAABBCCDD  # 匹配，触发 dump
```

设置指令 watchpoint（需已知函数地址，可从 map/elf 获取）:

```
ap_cmd dwti 0x64f691ec
ap_cmd memset_pattern 0x281a9070 0x4 0x55
```

<a id="id10"></a>

### 注意事项

- watchpoint 触发后会进入 Debug Monitor 异常并 dump 系统信息（`RESET_SOURCE_DEBUG_MONITOR_FAULT`），系统可能重启
- watchpoint 设置后一直有效，直到系统重启；无 CLI 清除命令
- 普通 `rtos_disable_int()` 运行态临界区使用 `BASEPRI` 屏蔽中断，DWT watchpoint 仍可按优先级响应；不要在 `PRIMASK` 特殊路径（如异常处理、启动流程、tickless sleep-entry 窗口）内依赖 DWT watchpoint，命中事件可能被丢弃，开中断后也不会补触发
- 同时连接 JLink SWD halt 调试时，可能与 Debug Monitor 模式冲突，建议二选一
- `dwtf` 执行期间会短暂关中断以保障计数精度，但不涉及 watchpoint 触发

<a id="arminoapswd"></a>

## **Armino平台AP系统swd调试**

ap系统支持在线调试，使用jlink工具及Eclipse上位机工具，即可快速搭建调式环境。

> - JLink环境通过Eclipse集成JLink gdb server \+ gdb 工具
> - Jlink和BK7259连线:
>
>   ```
>   1# VTref  ---- VREF
>   7# SWDIO  ---- SWDIO
>   9# SWCLK  ---- SWCLK
>   20# GND   ---- GND
>   ```
> - JLink软件版本
>   <https://www.segger.com/downloads/jlink/JLink_Windows_V898_x86_64.exe>
> - Arm工具链版本
>   <https://armkeil.blob.core.windows.net/developer/Files/downloads/gnu-rm/10.3-2021.10/gcc-arm-none-eabi-10.3-2021.10-win32.exe>
> - Eclipse版本
>   eclipse-embedcpp-2020-12-R-win32-x86\_64.zip
> - Eclipse工程配置
>
> > ![BK7259 JLink configuration](../../../_assets/707cff9b12ae274cef37-bk7236_jlink_config.png)
> >
> > ![BK7259 JLink configuration](../../../_assets/16b39d928bcb666919bf-bk7236_jlink_config2.png)
> >
> > ![BK7259 JLink configuration](../../../_assets/fd923a289eb43dd71309-bk7236_jlink_config3.png)
>
> - SWD 的物理管脚（默认 GPIO20\=SWCLK、GPIO21\=SWDIO，可通过 CP 侧
>   `CONFIG_SWD_DEBUG_MODE_PIN_CLK` 与 `CONFIG_SWD_DEBUG_MODE_PIN_DIO` 覆盖）
>   和调试口路由都由 CP 端统一管理
> - AP 侧通过 `ap_cmd setswdmode` 请求进入 SWD 调试模式（CP 侧也可直接输入
>   `setswdmode`）
> - AP 调用 `bk_set_swd_mode()` 时，会先关闭 AP 本核看门狗（WWDT/Task WDT），
>   再通过 mailbox IPC 通知 CP 调用其 `bk_set_swd_mode()` 完成调试口切换

备注

使用 JLink 进行 SWD 连接，需在 CP 侧 menuconfig 打开
`CONFIG_SWD_DEBUG_MODE`，或编译 `CONFIG_DEBUG_VERSION=y` 的 DEBUG 版本
（AP 侧 `setswdmode` / `bk_set_swd_mode()` 同样受
`CONFIG_DEBUG_VERSION` 或 `CONFIG_SWD_DEBUG_MODE` 保护）。

AP 侧 `setswdmode` 适用于系统已启动、mailbox IPC 可用后的运行时调试。如果需要
上电 very early boot 阶段即可让 JLink/Trace32 接入，应在 CP 启动路径中打开
`CONFIG_SWD_DEBUG_MODE`，由 CP 的 `Reset_Handler` / `Reset_Handler_Core0`
早期调用 `bk_enable_swd()` 完成调试口路由、WDT 处理和 SWD 管脚配置，不能依赖
AP CLI 命令。

警告

默认 SWD 管脚为 `GPIO20=SWCLK`、`GPIO21=SWDIO`。AP 工程的
`usr_gpio_cfg.h` 初始化较晚执行，如果其中把 GPIO20/21 配置成 SPI、LCD、I2C
等其他外设，会覆盖 SWD 管脚功能，导致系统启动后 JLink/Trace32 连接失败。
使用默认 SWD 管脚时，AP GPIO 表应将这两个管脚保留为 `GPIO_DEV_SWCLK` /
`GPIO_DEV_SWDIO`，或移除与 SWD 冲突的外设复用配置。

若开机即异常、串口命令来不及执行，可在 early boot 中（驱动尚未初始化时）调用：

```
bk_set_swd_mode();   /* AP：停本核看门狗并通知 CP 切 SWD */
while (g_test_mode); /* volatile 全局变量，防止编译器优化掉后续代码 */
```

接入 JLink 后修改 `g_test_mode` 即可继续单步调试。CP 侧也可在启动流程中直接
调用 bk\_set\_swd\_mode()（见 CP 文档），实现上电自动进入 SWD。

`bk_set_swd_mode()` 内部会自动完成：

- AP 端：关闭 WWDT、Task WDT
- CP 端：关闭 AON WDT/WWDT/Task WDT，并把 SWCLK/SWDIO 管脚映射到调试口

该接口仅做寄存器/IPC 操作，可在驱动未初始化的 early boot 或异常上下文中安全调用。

<a id="swd"></a>

### swd调试示例

连接好jlink后，可以按照以下步骤打断点调试：

- 根据函数指针或者函数名在Disassembly页找到dump的地址

<a id="id27"></a>
![BK7259 JLink configuration](../../../_assets/9259f95f109698a56943-jlink_1.png)


示意图1

<a id="id28"></a>
![BK7259 JLink configuration](../../../_assets/13e58b384679cbb5f8db-jlink_2.png)


示意图2

- 在dump函数之前的语句设置断点，将断点属性设置为hardware

<a id="id29"></a>
![BK7259 JLink configuration](../../../_assets/9aac10645ed1d3485ac6-jlink_3.png)


示意图3

- 点击resume继续运行程序。运行错误代码，如我在sta命令里，加了错误代码

<a id="id30"></a>
![BK7259 JLink configuration](../../../_assets/8ff9e5c270fd858e87f6-jlink_4.png)


示意图4

- 程序在断点处停下

<a id="id31"></a>
![BK7259 JLink configuration](../../../_assets/6af6e6cf6351d1f332ee-jlink_5.png)


示意图5

<a id="arminodump"></a>

## **Armino平台异常dump一键恢复现场工具**

> - 请参考发布工具中使用文档:
>   <https://dl.bekencorp.com/d/tools/Debug_tool/bk_coredump_tools.zip>
> - BK7259 dump工具常见问题:
>
>   - Kconfig 中 `CONFIG_DUMP_ENABLE` 默认关闭；`bk7259` / `bk7259_ap` 的
>     defconfig 已将其设为 `y`。若自定义工程关闭了 dump，需在 CP/AP 两侧
>     menuconfig 的 **Coredump** 中分别重新打开
>   - 当前架构为 CP\+AP，可在两侧 config 中分别打开 dump
>   - Dump 工具通过解析 log 中的 regs、内存段等内容恢复现场（详见工具包文档）
>   - Log 后缀支持 txt、log、DAT；编码仅支持 utf-8
>   - 工具目录下应只保留一份 Log，且 Log 中只含一次完整 dump（否则取最后一次）
>   - 工具可自动去掉规则时间戳 `[2026-02-03 14:35:13.375193]`，不规则时间戳需手动删除
>   - 若 dump 过程中连续两次异常（如越界检测触发 Assert），解析时需删掉第二次寄存器打印
>   - 单次 dump 会输出当前核寄存器、ITCM、DTCM、SRAM 分区、栈、外设寄存器及 EXTRA\_MEM 等
>   - 默认 CP 侧 Log/Dump 经 UART0 输出；AP 侧经 MAILBOX 转发到 CP 再经 UART0 输出
>   - 多核同时 dump 时需按核拆分 Log，分别用 CP/AP 的 elf 恢复
>
>     > dump 日志头部示例:
>     >
>     > ```
>     > @Dump-reason: MemFault
>     > build time => Jan 01 2026 12:00:00 !
>     > SMP-Core-id:0
>     > ```
>     >
>     > 寄存器格式（`CPU%d` 为异常核编号，与 `SMP-Core-id` 对应）:
>     >
>     > ```
>     > CPU2 Current regs:
>     > 0 r0 x 0x0
>     > 1 r1 x 0x28061ca0
>     > ...
>     > 14 sp x 0x20000928
>     > 15 lr x 0x21ec909
>     > 16 pc x 0x21ec8fa
>     > 17 xpsr x 0x61000000
>     > 18 msp x 0x2808ff48
>     > 19 psp x 0x20000908
>     > 20 primask x 0x0
>     > 21 basepri x 0x0
>     > 22 faultmask x 0x0
>     > 23 fpscr x 0x0
>     > 31 ER x 0xfffffffd
>     > 32 control x 0xc
>     > 40 MMFAR x 0x8061ca0
>     > 41 BFAR x 0x8061ca0
>     > 42 CFSR x 0x82
>     > 43 HFSR x 0x0
>     > 44 DFSR x 0x0
>     > 45 AFSR x 0x0
>     > 46 SHCSR x 0x0
>     > 47 ICSR x 0x0
>     > 48 VTOR x 0x28000000
>     > 49 MSPLIM x 0x0
>     > 50 PSPLIM x 0x0
>     > Traceback:
>     >     arm-none-eabi-addr2line -piaf -e app.elf 0x21ec8fa 0x21ec909 ...
>     > ```
>
>   备注
>
>   相较旧版 dump：寄存器新增 ``` 31 ER``（异常 LR）、``44 ```–`50` 故障/系统寄存器；
>   去掉旧版 `30 CPUx xPSR` 行；内存段 header 增加 `region` 字段。
>
>   内存编码由 `CONFIG_DUMP_UART_MEM_ENCODING_BASE64` /
>   `CONFIG_DUMP_UART_MEM_ENCODING_ASCII` 二选一（BK7259 defconfig 默认 Base64）。
>
>   内存段格式（Base64，默认）:
>
>   ```
>   >>>>stack mem dump begin, region: SRAM0, stack_top=28040000, stack end=28060000
>
>   <每行 32 字节数据的 Base64 编码，末尾含 CRC>
>
>   <<<<stack mem dump end. region: SRAM0, stack_top=28060000, stack end=28060000
>   ```
>
>   内存段格式（ASCII，可选）:
>
>   ```
>   >>>>stack mem dump begin, region: DTCM, stack_top=20000000, stack end=20004000
>
>   00 01 02 03 04 05 06 07 ...
>
>   <<<<stack mem dump end. region: DTCM, stack_top=20004000, stack end=20004000
>   ```
>
>   BK7259 AP 常见 `region` 名称：`DTCM`、`ITCM`、`SRAM0`–`SRAM6`、
>   `mstack`、`pstack`、``` EXTRA_MEM``（含中断记录等 plat dump 数据）、
>   ``MEM_CHECK ``` 及各外设寄存器块（`SYS`、`FLASH` 等）。
>
>   - 当系统打开CONFIG\_MEM\_DEBUG时, Dump过程会将当前系统正在使用的Heap内存全部打印出来, 并检查是否有内存越界:
>
>     ```
>     tick       addr         size   line    func                               task
>     --------   ----------   ----   -----   --------------------------------   ----------------
>     6976       0x28064b68   80     425     xQueueGenericCreate                media_ui_task
>     6976       0x28064be0   80     425     xQueueGenericCreate                media_ui_task
>     6976       0x28064c58   160    425     xQueueGenericCreate                media_ui_task
>     6976       0x28064d20   1024   863     xTaskCreate_ex                     media_ui_task
>     6976       0x28065148   104    868     xTaskCreate_ex                     media_ui_task
>     6976       0x2807d098   80     425     xQueueGenericCreate                transfer_major_task
>     6976       0x2807d110   80     425     xQueueGenericCreate                transfer_major_task
>     ```
>   - 正常情况下也会将task相关信息dump到日志, 供问题分析时参考

<a id="bk7259-dump"></a>

## **BK7259 在线 Dump 解析工具**

SDK 内置 `bk_dump_analyze.py`，可直接解析 AP/CP 异常 dump 与 heartbeat timeout
日志，不需要先导入 Eclipse。工具会从串口 log 中提取寄存器、traceback、内存段、
EXTRA\_MEM 和 heap 信息，并结合同一次构建的 `app.elf` 做符号化。

基本用法:

```
# AP 异常 dump
python3 tools/dump_tools/bk_dump_analyze.py \
    --log dump_ap.log \
    --elf projects/app/build/bk7259/app/bk7259_ap/app.elf

# CP 异常 dump
python3 tools/dump_tools/bk_dump_analyze.py \
    --mode cp-exception \
    --log dump_cp.log \
    --elf projects/app/build/bk7259/app/bk7259/app.elf

# 输出完整 Markdown 报告
python3 tools/dump_tools/bk_dump_analyze.py \
    --log dump_ap.log \
    --elf projects/app/build/bk7259/app/bk7259_ap/app.elf \
    -o report.md
```

主要输出包括：

- `Summary`：dump reason、build time、ELF 是否匹配、traceback 数量等。
- `Crash Point`：异常核 PC/LR/MSP/PSP、CFSR/HFSR/MMFAR/BFAR 及符号化结果。
- `Execution Context`：判断异常发生在 task/thread、ISR/handler，还是
  critical section / interrupts masked。
- `Primary Call Chain Candidates`：按置信度展示固件 traceback、任务栈或栈扫描链路。
- `Interrupt State`：解析 interrupt recorder，识别 ISR 是否进入未退出。
- `Heap Integrity`：离线扫描 MEM\_DEBUG canary，定位已分配堆块尾部越界。

`Execution Context` 的判断依据：

- `xPSR` 低 9 位（IPSR / exception number）非 0，说明异常发生在 handler/ISR。
- 调用链中出现 `timer_group_isr`、`bk_ipi_isr_dispatch`、
  `bk_int_dispatch_registered_isr` 等 ISR 分发帧时，判为 ISR/handler。
- dump\_test 日志中的 `DUMP_TEST_BEGIN mode=task_*|isr_*|critical_*` 可作为测试场景强证据。
- `PRIMASK` / `FAULTMASK` 可作为中断屏蔽证据；`BASEPRI` 只能作为弱提示，
  因为异常处理或 assert 路径也可能抬高 `BASEPRI`，不能单独据此判定 critical。

`Heap Integrity` 的工作方式：

- AP 侧会从 ELF 中查找 `s_sram_used`、`s_hsram_used`、`s_psram_used`、
  `s_psram_cache_used`，分别扫描 SRAM / HSRAM / PSRAM / PSRAM cache 已分配链表。
- CP 侧会查找 `xUsed`、`xPsramUsed`，扫描 SRAM / PSRAM 已分配链表。
- 对每个已分配块读取 MEM\_DEBUG 记录的 alloc func/line/task/tick，再检查
  `user + wantedSize` 后的 `0xcd` canary。
- 若 canary 被破坏，报告会显示 `Mem Overflow user=... tag=... actual=... alloc=...`。

能力边界：

- 工具能定位崩溃现场、符号化调用链、识别 ISR/critical 等执行上下文，并发现已破坏的
  heap canary。
- 对象内部字段被踩或 UAF 若没有破坏块尾 canary，工具通常只能看到 `PC=0`、
  函数指针异常等结果，不能仅凭 dump 自动给出「UAF」或「对象内越界」根因标签。
- 若 ELF 与 dump 不是同一次构建，符号化、heap used-list 地址和 alloc 现场都可能不可靠。

<a id="armino"></a>

## **Armino平台系统稳定性问题分析**

嵌入式稳定性问题是一类常见但不容易定位的问题，其具有以下特征：

> - 不可预测性：系统故障的时间点不固定，难以预测，可能在长时间运行后突然发生
> - 多样性：问题可能以崩溃、死机、卡顿或错误行为等多种形式出现
> - 累计效应：系统运行时间越长，资源泄漏或数据损坏等问题可能积累，最终导致崩溃
> - 环境依赖性：稳定性还可能受温度、湿度和电源波动等环境因素的影响

为了帮助用户更好的定位稳定性问题，下面的链接文档中提供了常见的分析手段

备注

> 本文档仅针对软件引起的稳定性问题,建议用户在碰到稳定性问题时，优先参考该文档

- 文档 [下载链接](https://dl.bekencorp.com/tools/system_debug/稳定性问题软件分析.pdf)
- 文档内容说明:

  - 文中介绍了系统调试相关的工具，请参考上述章节
  - 文中列举了系统可能出现异常的各种场景
  - 文中还列举了一些经典的稳定性问题的分析案例

<a id="ap"></a>

## **AP 内置调试特性**

本节按功能逐项说明 AP 侧内置调试能力的作用与查看方式（串口命令均需
`ap_cmd` 前缀）。DWT 见上文 [DWT 调试 (Data Watchpoint and Trace)](#ap-dwt-debug)，此处不重复。

<a id="config-mem-debug"></a>

### 1\. 堆内存分配跟踪（CONFIG\_MEM\_DEBUG）

<a id="id12"></a>

#### 作用

每次 `os_malloc()` / `pvPortMalloc()` 等分配时，在块头记录分配函数、行号、
任务名、分配 tick、请求大小；块尾填充 `0xcd` 用于检测写越界。可用于：

- 崩溃时确认当时还有哪些堆块未释放、是谁分配的
- 在线排查内存泄漏（对比不同时间点的存活列表）
- 配合 `CONFIG_MEM_DEBUG_OVERFLOW`，在 `free` 时发现尾部 tag 被破坏而 assert

<a id="id13"></a>

#### 开启配置

**Components** → **bk\_rtos** → **Modify Memory Debug Config**：

- ``` CONFIG_MEM_DEBUG=y``（``bk7259_ap.defconfig ``` 默认已开）
- 建议同时保持 `CONFIG_DUMP_ENABLE=y`，异常时自动打印堆列表
- 可选 `CONFIG_MEM_DEBUG_OVERFLOW=y`，开启写越界检测

<a id="id14"></a>

#### 如何查看

**方式一：串口 CLI（系统仍正常运行时）**

```
ap_cmd memshow                          # 先看各池剩余空间
ap_cmd memleak                          # 打印全部存活分配
ap_cmd memleak 60                       # 只看最近 60 秒内分配的块
ap_cmd memleak 0 0 media_ui_task        # 按任务名过滤
```

`memleak` 输出列含义：

```
tick       addr         size   line    func                               task
--------   ----------   ----   -----   --------------------------------   ----------------
6976       0x28064b68   80     425     xQueueGenericCreate                media_ui_task
```

- `tick`：分配时的系统 tick
- `addr`：用户可见指针（user ptr）
- `line` / `func` / `task`：分配调用点

也可通过 `osinfo` 一次性输出任务列表 \+ backtrace \+ 堆分配列表：

```
ap_cmd osinfo
```

**方式二：异常 / Assert 自动 dump（系统已崩溃时）**

开启 `CONFIG_DUMP_ENABLE` 后，MemFault 或 Assert 的串口日志中会自动附带与
`memleak` 相同格式的堆列表（由 `os_dump_memory_stats()` 打印）。在日志中
搜索 `tick` 表头即可定位。

<a id="uaf-config-heap-uaf-audit-poison-quarantine"></a>

### 2\. 堆 UAF 检测（CONFIG\_HEAP\_UAF\_AUDIT\_POISON / QUARANTINE）

<a id="id15"></a>

#### 作用

针对 Use-After-Free：块被 `free` 后仍被旧指针读写。

- 审计环 `CONFIG_HEAP_UAF_AUDIT_POISON`：每次 `free` 记录该块的
  alloc/free 函数、行号、任务、tick，并把 user 数据填为 `0xEE`
- Quarantine `CONFIG_HEAP_UAF_QUARANTINE`：已释放块暂不归还堆，若隔离
  期间 payload 被改写，出队时 assert 并打印 `HEAP UAF QUARANTINE POISON BROKEN`

典型场景：模块 A 释放后仍写旧指针，破坏了模块 B 刚申请到的同一块内存——crash
现场在 B，根因在 A；通过 free history 可反查该地址最近的释放者。

<a id="id16"></a>

#### 开启配置

依赖 `CONFIG_MEM_DEBUG=y`，路径同上 **Modify Memory Debug Config**：

```
CONFIG_HEAP_UAF_AUDIT_POISON=y
CONFIG_HEAP_UAF_FREE_RECORD_MAX=128        # free history 条数，默认 128
CONFIG_HEAP_UAF_QUARANTINE=y               # 可选，加强 UAF 检测
CONFIG_HEAP_UAF_QUARANTINE_BYTES=65536     # quarantine 最多扣留字节数
```

备注

UAF 与 quarantine 默认关闭；quarantine 会真实占用可用堆，仅调试期开启。

<a id="id17"></a>

#### 如何查看

**方式一：查某次 free 的历史记录**

```
ap_cmd memhistory           # 输出全部 free history（最新在前）
ap_cmd memhistory 20        # 只输出最近 20 条
```

单条记录格式：

```
addr 0x28064b68 size 80
  A xQueueGenericCreate:425
    task=media_ui_task, tick=6900
  F my_free_wrapper:102
    task=ui_task, tick=6950
```

- `A` 行：分配侧（函数:行号、任务、tick）
- `F` 行：释放侧

**方式二：按崩溃地址反查是否曾被 free**

将 MemFault 日志中的 `MMFAR` / `BFAR` 或寄存器里的可疑地址代入：

```
ap_cmd memtrace 0x28064b68
```

若地址落在近期 free 记录范围内，会打印匹配的 alloc/free 历史；否则提示
`addr ... is not found in heap free history`。

**方式三：Quarantine 自动命中（无需手动命令）**

隔离期间若有人写坏了 `0xEE` poison，串口会直接打印：

```
!!!!! HEAP UAF QUARANTINE POISON BROKEN !!!!!
!!!!! Freed block was modified before real free. !!!!!
  addr=0x28064b70 offset=0 expect=0xee actual=0x55 size=80
```

随后自动调用 `memtrace` 输出对应 free history，并触发 assert / dump。

<a id="task-task-recorder"></a>

### 3\. Task 切换记录（Task Recorder）

<a id="id18"></a>

#### 作用

在每次任务切换时，把当前核上最近 10 次调度的快照写入环形缓冲，记录：

| 字段 | 含义 |
| --- | --- |
| `tick` | 切换时的 OS tick |
| `time` | AON RTC 时间（微秒，低 32 位） |
| `TCB_ptr` | 任务控制块地址，可与 `tasklist` 输出对照 |
| `stack_top` | 切换瞬间 SP 值 |
| `stack_bottom` / `stack_size` | 栈底地址与栈大小；`stack_top` 接近 `stack_bottom` 表示栈余量不足 |

用于分析崩溃前最后执行了哪些任务、是否存在栈水位过低。

<a id="id19"></a>

#### 开启配置

**Armino Configuration** → **Compiler Options** → `CONFIG_DEBUG_VERSION=y`

该宏在 `ap/components/bk_rtos/include/bk_rtos_debug.h` 中自动定义
`FREERTOS_TASK_RECORDER=1`、`FREERTOS_TASK_RECORDER_CNT=10`。
SMP 下 core0 / core1 各一组缓冲，符号名为
`s_task_recorder_core0[]`、`s_task_recorder_core1[]`。

<a id="id20"></a>

#### 如何查看

Task Recorder 没有专用 CLI，不会在串口逐条打印，需结合异常 dump 查看。

**步骤 1：先读 dump 日志里的即时任务信息**

异常 dump 会自动打印（无需额外配置）：

```
ap_cmd tasklist      # 或等 dump 日志中的 >>>>dump task list begin
ap_cmd backtrace
```

`tasklist` 示例：

```
task         state   pri   water   no
media_task   R       5     128     3
```

其中 `water` 为栈剩余水位（字），越小越危险。

**步骤 2：在 Memory 窗口或 Eclipse Expressions 中查看切换历史**

Task Recorder 数据随 SRAM 分区一并导出。建议按以下步骤查看：

1. 使用上文 **异常 dump 一键恢复现场工具** 将 log 恢复到 Eclipse 调试环境
2. 在 `app.map` 中确认 `s_task_recorder_core0` / `s_task_recorder_core1` 的运行地址
3. 在 Eclipse 中任选一种方式观察：

   - **Memory** 窗口：跳转到上述地址，按 `task_list_recorder_t` 结构体布局读取
     `tick`、`time`、`TCB_ptr`、`stack_top`、`stack_bottom`、`stack_size`
   - **Expressions\*\*（或 \*\*Variables**）窗口：直接添加 `s_task_recorder_core0[9]` 等表达式

将 `TCB_ptr` 与 `tasklist` 输出中的任务地址对照，可还原崩溃前的调度顺序。
若 `stack_top` 接近 ``` stack_bottom``（结合 ``stack_size ``` 判断），说明该次切换时栈余量不足。

<a id="interrupt-recorder"></a>

### 4\. 中断记录（Interrupt Recorder）

<a id="id21"></a>

#### 作用

在每个 CPU 核上记录最近 40 次（可配）中断的进入/退出时间和 IRQ 号，
并统计两项汇总：

- 单次 ISR 耗时：同一条记录中 `exit_time - enter_time`
- 中断静默窗口：相邻两次 ISR 退出之间的时间差（`max_silence_us`）；
  若系统长时间没有中断完成，该值会很大

适用于系统卡死、心跳丢失、怀疑关中断过久或外设中断停止的场景。

<a id="id22"></a>

#### 开启配置

**Arch** → **Cortex-M** → **Modify Arch Config**：

```
CONFIG_INTERRUPT_DEBUG_RECORDER=y          # defconfig 默认已开
CONFIG_INTERRUPT_RECORDER_CNT=40           # 每核环形深度
CONFIG_INTERRUPT_GAP_DETECT_US=50000       # 静默超过 50ms 计入 silence_event_total
```

<a id="id23"></a>

#### 如何查看

**方式一：异常 dump 的 EXTRA\_MEM 段（崩溃后）**

初始化时 `s_interrupt_core0_dump` / `s_interrupt_core1_dump` 通过
`rtos_regist_plat_dump_hook()` 注册。异常 dump 日志中会出现：

```
>>>>EXTRA_MEM dump begin, stack_top=0x28xxxxxx, stack end=0x28xxxxxx
```

将 `stack_top` 与 `app.map` 中 `s_interrupt_core0_dump` 地址比对，确认
命中对应 `EXTRA_MEM` 段后，在 Eclipse **Memory** 窗口跳转到该地址，或在
**Expressions** 中添加 `s_interrupt_core0_dump` 观察汇总字段：

- `count`：累计中断次数
- `max_gap_us`：最长 ISR 退出间隔（微秒）
- `max_gap_irq`：post\_silence\_irq，静默窗口后第一个完成的 IRQ
- `recorder[]`：最近若干条 IRQ 的 `enter_time` / `exit_time` / IRQ 号

**方式二：串口文本 dump（需在代码中主动调用）**

固件提供 ``` bk_interrupt_dump_recorder()``（``interrupt.c ```），串口输出格式如下。
当前异常 dump 流程中该调用默认注释掉，若需在运行期手动触发，可在 CLI 或
调试代码中调用。输出示例：

```
interrupt recorder core0 total=120 depth=40 last_isr_exit_us=... max_silence_us=520000 post_silence_irq=5 ...
  [core0][119] irq=5 done=1 enter=1000234 exit=1000456
```

字段说明：

- `total`：累计中断次数；`depth`：当前缓冲中有效条数
- `max_silence_us`：启动以来最长的 ISR 退出间隔（微秒）
- `post_silence_irq`：该静默窗口结束后第一个完成的 IRQ
- `done=1`：该条记录已有完整 enter/exit；`done=0` 表示中断尚未退出

<a id="critstat"></a>

### 5\. 临界区中断屏蔽时长统计（critstat）

<a id="id24"></a>

#### 作用

hook `rtos_enter_critical()` / `rtos_exit_critical()` 及
`rtos_disable_int()` / `rtos_enable_int()`，统计 `BASEPRI` / `PRIMASK` 中断屏蔽持续时长
（微秒），并记录进入时的 LR、任务名、嵌套深度。

- 超过 trace 阈值（默认 5 s）：写入最近 16 条慢记录，可用 CLI 导出
- 超过 assert 阈值（默认 10 s）：打印摘要后 assert

用于定位临界区中断屏蔽过长导致的调度饿死、mailbox 超时、音频断续等。

<a id="id25"></a>

#### 开启配置

**Components** → **bk\_rtos** → **Modify OS Debug Config**：

```
CONFIG_ISR_DISABLE_TIME_STATISTIC=y
```

默认关闭。开启后 `critstat` 相关 CLI 才会注册。

<a id="id26"></a>

#### 如何查看

**步骤 1：复现前调低阈值（否则默认 5 s/10 s 很难触发）**

```
ap_cmd critstat set 100000 50000
```

表示中断屏蔽超过 50 ms 记 trace，超过 100 ms assert。
（`assert_us` 必须大于 `trace_us`。）

**步骤 2：查看当前状态**

```
ap_cmd critstat status
```

输出示例：

```
critstat: assert_threshold_us=100000 trace_threshold_us=50000 max_diff_us=82340 trace_cnt=3
critstat: core=0 nest=0 ignored_nest=0 max_nest=1 enter_lr=0x21abc123 task=0x28001234 name=wifi_task start_us=0x...
```

- `max_diff_us`：历史最大中断屏蔽时长
- `trace_cnt`：已记录的慢临界区条数
- `enter_lr`：进入中断屏蔽时的链接寄存器，可用 `addr2line -e app.elf 0x21abc123` 解析到函数

**步骤 3：导出慢临界区明细**

```
ap_cmd critstat dump
```

输出示例：

```
critstat dump: cnt=3 wr=3

[00] type=0 core=0 diff=82340us nest=1 task=0x28001234 name=wifi_task
     enter_lr=0x21abc123 exit_lr=0x21abc456 start=0x00000000xxxxxxxx end=0x00000000xxxxxxxx
```

- `diff`：本次中断屏蔽时长（微秒）
- `enter_lr` / `exit_lr`：进入、退出中断屏蔽时的返回地址，用 addr2line 定位代码
- `type=0`：慢临界区；`type=1`：触发 assert 的记录

**步骤 4：assert 时自动打印**

若中断屏蔽时间超过 assert 阈值，日志会先打印 `critstat assert:` 摘要（含
`enter_lr`、`exit_lr`、任务名、耗时），再触发 assert，无需手动 `dump`。
