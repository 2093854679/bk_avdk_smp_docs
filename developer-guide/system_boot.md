---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/system_boot/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cp-ap"></a>

# 系统启动流程（CP \+ AP）

本章节按当前代码实现，梳理从 CP 进入 reset handler 到 AP 启动完成的完整链路。
重点回答以下问题：

- CP 从哪里进入 reset 后续初始化，直到任务调度启动。
- AP 是在 CP 的哪个线程、哪个时机被拉起。
- `main` 任务与 `user_app` 任务之间的同步关系。
- 哪些初始化线程会在运行后自删除，调试时需要注意什么。

备注

- 文中以 `projects/app` 默认流程为参考（CP 侧 `cp_main.c` 会调用 `bk_start_ap_system()`，AP 侧 `main()` 调用 `bk_init()`）。
- 不同项目/配置会裁剪部分步骤（例如是否允许 AP 热启动/掉电重启、是否启用 CPU hotplug）。

<a id="id1"></a>

## 启动全景框图（按时间顺序）

```
+--------------------------------------------------------------+
| SoC 上电/复位                                                 |
+--------------------------------------------------------------+
                            |
                            v
+--------------------------------------------------------------+
| CP CPU0: reset -> soc_prep_hook -> _soc_start                |
|   - 早期时钟/电源初始化                                       |
|   - 向量表重定位、MPU/Cache/core_init                         |
|   - pm_hardware_init                                         |
+--------------------------------------------------------------+
                            |
                            v
+--------------------------------------------------------------+
| CP entry_main                                                |
|   - rtos_init + components_early_init                        |
|   - 创建 app_main_thread / user_app_thread                   |
|   - rtos_start_scheduler                                     |
+--------------------------------------------------------------+
                            |
                            v
+--------------------------------------------------------------+
| CP app_main_thread                                           |
|   - pm_thread_main                                           |
|   - 调用工程 main() -> 执行 bk_init()                         |
|   - bk_init() 末尾 rtos_user_app_launch_over() 释放 user_app |
|   - app_main_thread 自删除                                   |
+--------------------------------------------------------------+
                            |
                            v
+--------------------------------------------------------------+
| CP user_app_thread                                           |
|   - 阻塞等待 user_app_sema                                    |
|   - 被 release 后执行 s_user_app_entry = user_app_main        |
|   - user_app_main() 内调用 bk_start_ap_system() 拉起 AP       |
|   - user_app_thread 自删除                                    |
+--------------------------------------------------------------+
                            |
                            v
+--------------------------------------------------------------+
| AP CPU2: reset -> soc_prep_hook -> _soc_start                |
|   - 向量表重定位、MPU/L1/L2 Cache、core_init                   |
|   - entry_main -> rtos_init -> components_early_init         |
|   - start_app_main_thread -> rtos_start_scheduler            |
+--------------------------------------------------------------+
                            |
                            v
+--------------------------------------------------------------+
| AP app_main_thread -> main() -> bk_init()                    |
|   - components_init/driver_init                              |
|   - wifi/cli/at/ble 等组件初始化                              |
|   - bk_pm_cp1_boot_ok_response_set()                         |
|   - bk_pm_ap_boot_success_set(true)                          |
+--------------------------------------------------------------+
                            |
                            v
+--------------------------------------------------------------+
| CP 等待 AP boot_success（超时可重试/复位策略）                 |
+--------------------------------------------------------------+
```

<a id="id2"></a>

## 阶段 0：术语与核编号

- 物理核编号：CP 子系统为 `CPU0/CPU1`，AP 子系统为 `CPU2/CPU3`。
- SMP 逻辑核：每个子系统内部都以逻辑 `core0/core1` 运行。
- 启动主核：CP 侧由 CPU0 先执行；AP 侧由 CPU2 先执行。

<a id="cp-reset-entry-main"></a>

## 阶段 1：CP 从 reset 到 entry\_main

CP 侧启动主链路如下（代码位置：`cp/middleware/soc/bk7259/soc_init.c`）：

1. 进入 `soc_prep_hook()`

   - 执行 `sys_drv_early_init()`，完成电源/时钟/模拟域的最早期配置。
   - 执行 `reboot_tag_init()` 等复位上下文准备。
   - 配置 FPU 低功耗状态与 SCB CCR 的 LOB 位。
2. 进入 `_soc_start()`

   - 主核执行 `relocate_vector_table()`。
   - 配置 mpu\_enable()（按配置）。
   - 按平台配置完成早期 cache 状态处理。`CONFIG_CACHE_MAINTENANCE` 仅控制业务
     per-buffer cache clean/invalidate API，当前推荐默认关闭；boot 阶段需要的系统级
     cache 操作由平台启动代码保留。
   - 执行 `core_init()`，可选 `cm_backtrace_init()`。
   - 主核执行 `pm_hardware_init()`。
   - 跳转 `entry_main()`。

<a id="cp-entry-main"></a>

## 阶段 2：CP entry\_main 到任务调度启动

代码位置：`cp/components/bk_startup/system_main.c`，`entry_main()` 顺序为：

1. `rtos_init()`。
2. `components_early_init()`。
3. bk\_module\_init()（弱符号扩展点）。
4. rtos\_user\_app\_preinit()：初始化 user\_app\_sema（计数 1）。
5. 创建两个线程：

   - `start_app_main_thread()` -\> 线程函数 `app_main_thread`。
   - `start_user_app_thread()` -\> 线程函数 `user_app_thread`。
6. `rtos_init_base_time()`，可选启动 WWDT。
7. `rtos_start_scheduler()`。

其中第 2 步 `components_early_init()` 是“调度器启动前”的关键初始化阶段。
此阶段仍处于启动上下文，不应依赖普通任务调度。

```
components_early_init()（未启动调度器）
├─ interrupt_init()                     // 中断框架
├─ reset_reason_init() [CONFIG_RESET_REASON]
├─ app_phy_init()                       // PHY/RF 适配早期准备
├─ driver_early_init()
│  ├─ CP: wakeup/aon_pmu/efuse/aon_rtc/hspl/ipi [按宏]
│  ├─ CP: sys_drv + gpio + ate + uart + wwdt驱动 [按宏]
│  └─ AP: aon_pmu/hspl/ipi + wwdt驱动 [按宏]
├─ pm_init()                            // PM 回调与低功耗准备
├─ bandgap_init()/random_init()/product_id_boot_check()
└─ bk_stack_guard_setup()
```

CP/AP 在“调度器前初始化”阶段对比如下：

```
CP components_early_init
  - interrupt/reset_reason
  - app_phy_init
  - driver_early_init: sys/gpio/ate/uart 已在此阶段初始化
  - PM/OTP/bandgap/random/stack_guard

AP components_early_init
  - interrupt/reset_reason
  - app_phy_init
  - driver_early_init: 以 AON/HSPL/IPI/WWDT 等早期驱动为主
  - PM/random/stack_guard
```

CP/AP pre-scheduler 并排时序图：

```
时间向下
   |
   v
+--------------------------------------+   +--------------------------------------+
| CP (CPU0)                            |   | AP (CPU2)                            |
+--------------------------------------+   +--------------------------------------+
| rtos_init()                          |   | rtos_init()                          |
| components_early_init()              |   | components_early_init()              |
|  - interrupt/reset_reason            |   |  - interrupt/reset_reason            |
|  - app_phy_init                      |   |  - app_phy_init                      |
|  - driver_early_init                 |   |  - driver_early_init                 |
|    * AON/HSPL/IPI (按宏)             |   |    * AON/HSPL/IPI/WWDT (按宏)         |
|    * sys/gpio/ate/uart (按宏)        |   |                                      |
|  - pm/random/stack_guard             |   |  - pm/random/stack_guard             |
| bk_module_init()                     |   | bk_module_init()                     |
| rtos_user_app_preinit()              |   |                                      |
| create app_main/user_app threads     |   | create app_main thread               |
| rtos_init_base_time()                |   | rtos_init_base_time()                |
| rtos_start_scheduler()               |   | rtos_start_scheduler()               |
+--------------------------------------+   +--------------------------------------+
```

重要

常规工程中，AP 拉起依赖 `user_app_thread` 被信号释放后，执行项目注册的
`s_user_app_entry`。

<a id="main-user-app-cp-ap"></a>

## 阶段 3：main 线程与 user\_app 线程同步机制（CP/AP 通用模型）

在 `projects/app/cp/cp_main.c` 中：

1. 工程 `main()` 先执行 `rtos_set_user_app_entry(user_app_main)`，注册 user\_app 入口。
2. 然后执行 bk\_init()（位于 CP app\_main\_thread 上下文）。
3. `bk_init()` 完成关键初始化后调用 `rtos_user_app_launch_over()`，给 `user_app_sema`。
4. 此时一直阻塞在 `rtos_user_app_waiting_for_launch()` 的 user\_app\_thread 被释放。
5. user\_app\_thread 执行 ``` s_user_app_entry``（即 ``user_app_main ```），其中调用 `bk_start_ap_system()`。

CP 的 `bk_init()` 细分（在 app\_main\_thread 上下文）：

```
CP bk_init()
├─ components_init()
│  ├─ driver_init()
│  │  ├─ timer/dma/wdt/mailbox/ipc
│  │  ├─ flash/easyflash/adc/spi/i2c/qspi/calendar
│  │  ├─ ckmn/lin/usb/can/pwm/irda/uid/psram(按宏)
│  │  └─ 其他平台与安全相关驱动(按宏)
│  ├─ wdt_init()
│  ├─ sensor_init() [温度/电压检测按宏]
│  └─ bk_module_init() + 启动信息打印
├─ wifi/bt/ble/mac 等协议栈初始化(按宏)
├─ at server/cli/mp3/semi-host/um/ota 等业务初始化(按宏)
├─ rtos_user_app_launch_over()   // 释放 user_app_thread
└─ 返回到 app_main_thread（后续线程可自删除）
```

等价时序如下：

```
app_main_thread:
  -> main()
  -> bk_init()
  -> rtos_user_app_launch_over()  // give semaphore

user_app_thread:
  -> rtos_user_app_waiting_for_launch() // block
  -> (semaphore released)
  -> s_user_app_entry() == user_app_main()
  -> bk_start_ap_system()
```

``` bk_start_ap_system()``（``cp/components/bk_startup/system_main.c ```）核心动作：

- 打印 `cp start ap system`。
- 调用 `bk_multicore_start(CONFIG_AP_SYS_MASTER_CPU_ID)` 启动 AP 主核。
- 成功后置位内部 `s_ap_system_started`，防止重复拉起（受配置宏影响）。

从代码结构上，CP 和 AP 都具备同一套同步原语：

- `rtos_user_app_preinit()`：创建 `user_app_sema`。
- `rtos_user_app_waiting_for_launch()`：user\_app 线程阻塞等待。
- `rtos_user_app_launch_over()`：main 初始化完成后释放 user\_app。

差异在于当前启动路径选择：

- CP：`entry_main()` 中会同时创建 `app_main_thread` 与 `user_app_thread`，因此同步链路实际生效。
- AP：代码中同样有上述同步函数，但当前 `entry_main()` 未启动 `start_user_app_thread()`，因此默认仅保留 `app_main_thread` 主路径。

<a id="ap-reset"></a>

## 阶段 4：AP 从 reset 到调度启动

AP 侧启动代码在 `ap/middleware/soc/bk7259_ap/soc_init.c` 与
`ap/components/bk_startup/system_main.c`：

1. AP 进入 `soc_prep_hook()`

   - 初始化 FPU/LOB 等基础硬件状态。
   - 为后续缓存与内核初始化准备执行环境。
2. AP 进入 `_soc_start()`

   - 主核执行 relocate\_vector\_table()（CPU2）。
   - ICache invalidate。
   - 可选 `mpu_enable()`。
   - 按配置初始化 L2（`CONFIG_L2_CACHE_ENABLE`：CPU2 初始化、CPU3 等待）。
   - L1 I/D Cache 在 AP 启动路径中按 `CONFIG_ICACHE` / `CONFIG_DCACHE` 分别使能；
     当前推荐配置为 L2 cache 开启、L1 D-cache 关闭。`CONFIG_CACHE_MAINTENANCE`
     仅控制业务 per-buffer cache clean/invalidate API，不影响 boot、MPU/cache 初始化、
     低功耗和 CPU hotplug 所需的系统级 cache 操作。
   - `core_init()`、可选 `cm_backtrace_init()`。
   - 主核进入 `entry_main()`；从核走 `soc_isr_init()` 和 `_othercore_start()`。
3. 进入 entry\_main()（AP 启动主入口）

   - `set_ap_startup_index(AP_ENTER_ENTRY_MAIN)` 记录启动里程碑。
   - `rtos_init()`。
   - ``` components_early_init()``（内部包含 ``interrupt_init() ```、`driver_early_init()`）。
   - `bk_module_init()`。
   - `start_app_main_thread()`。
   - `rtos_init_base_time()`。
   - `set_ap_startup_index(AP_ENTER_RTOS_START_SCHEDULER)`。
   - `rtos_start_scheduler()`。

AP 侧 `components_early_init()` 同样发生在调度器启动前，核心是：

- 中断/复位原因初始化。
- `driver_early_init()` 完成最小可用早期驱动（AON/HSPL/IPI/WWDT 等，按宏）。
- PM 与随机栈保护等基础能力初始化。
- 尚未进入普通任务调度，不应依赖线程间异步行为。

<a id="ap-main"></a>

## 阶段 5：AP main 线程执行与启动完成标记

AP 调度起来后，`app_main_thread()` 顺序为：

1. `bk_pm_ap_thread_main()`。
2. 调用工程 ``` main()``（如 ``projects/app/ap/ap_main.c ```）。
3. 工程 `main()` 调用 ``` bk_init()``（``ap/components/bk_init/bk_init.c ```）。
4. `app_main_thread` 完成后执行 `rtos_delete_thread(NULL)` 自删除。

`bk_init()` 内部关键点：

```
AP bk_init()
├─ set_ap_startup_index(AP_ENTER_BK_INIT)
├─ components_init()
│  ├─ driver_init()
│  │  ├─ sys/gpio/uart/timer/dma
│  │  ├─ mailbox/ipc/pm_mailbox
│  │  ├─ flash/easyflash/security
│  │  ├─ spi/i2c/qspi/calendar/ckmn/lin 等(按宏)
│  │  └─ 可选 usb/can/touch/hpdma/uid 等(按宏)
│  ├─ wdt_init()
│  └─ 启动信息打印（reset reason/chip id）
├─ app_wifi_init()/app_cli_init()/cpu_hp_governor_init() [按宏]
├─ at_server_init()/atsvr_app_init() [CONFIG_AT]
├─ 其他业务初始化：ntp/um/ota/eth/ble/psram detect 等(按宏)
├─ bk_pm_cp1_boot_ok_response_set()
├─ bk_pm_ap_boot_success_set(BK_TRUE)
└─ set_ap_startup_index(AP_EXIT_BK_INIT)
```

<a id="id3"></a>

## 阶段 6：CP 侧等待 AP 启动成功

CP 电源管理控制中会等待 AP 启动完成（`cp/components/bk_pm/src/services/bk_pm_ap_ctrl.c`）：

- `pm_module_bootup_cpu1()` 拉起 AP 后轮询 `bk_pm_ap_boot_success_get()`。
- 默认等待窗口约 `PM_BOOT_AP_WAITING_TIEM = 1800ms`。
- 超时后可重试（`PM_BOOT_AP_TRY_COUNT = 3`），仍失败时可触发复位策略（配置相关）。
- AP 下电时会清理 `boot_success`，以支持下一次拉起流程。

<a id="id4"></a>

## 任务生命周期与自删除注意点

以下线程是“初始化后会退出”的，不是常驻任务：

- CP `app_main_thread`：执行 `pm_thread_main()` 和工程 `main()` 后自删除。
- CP `user_app_thread`：执行 `s_user_app_entry` 后自删除，并释放 `user_app_sema`。
- AP `app_main_thread`：执行 AP 工程 `main()` 后自删除。
- AP `user_app_thread`：当前 `entry_main()` 中未启动（`start_user_app_thread()` 被注释）。

<a id="id5"></a>

## 同步与生命周期注意点（重点）

- 线程函数里的局部变量在 `rtos_delete_thread(NULL)` 后立即失效，不能把其地址传给异步模块长期持有。
- 若需要跨线程/跨阶段保留数据，优先使用：
  \- 静态存储区（static/global）
  \- 堆内存（并明确释放时机）
  \- 明确所有权的消息拷贝（queue/mailbox 深拷贝）
- 通过 `user_app_sema` 释放的同步点之后，`app_main_thread` 可能很快结束并删除；不要依赖其栈上对象在 user\_app 阶段仍可访问。
- 同理，`user_app_thread` 自删除后，其线程栈上的上下文全部无效；回调参数若引用其局部对象会产生悬挂指针风险。

<a id="id6"></a>

## 关键函数索引（便于代码跳转）

- CP 早期启动：`cp/middleware/soc/bk7259/soc_init.c`
  \- `soc_prep_hook()`
  \- `_soc_start()`
- CP 系统入口与拉起 AP：`cp/components/bk_startup/system_main.c`
  \- `entry_main()`
  \- `bk_start_ap_system()`
- AP 早期启动：`ap/middleware/soc/bk7259_ap/soc_init.c`
  \- `soc_prep_hook()`
  \- `_soc_start()`
- AP 系统入口：`ap/components/bk_startup/system_main.c`
  \- `entry_main()`
  \- `app_main_thread()`
- AP 组件初始化：`ap/components/bk_init/bk_init.c`
  \- `bk_init()`
- AP 启动成功同步与等待：`cp/components/bk_pm/src/services/bk_pm_ap_ctrl.c`
  \- `bk_pm_ap_boot_success_set/get()`
  \- `pm_module_bootup_cpu1()`
