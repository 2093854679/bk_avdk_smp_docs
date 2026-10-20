---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_cp_fast_boot.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cp"></a>

# CP快速启动

<a id="id1"></a>

## 概述

CP快速启动是BK7259在 `CONFIG_DEEP_LV=y` 时，从
``` PM_MODE_LOW_VOLTAGE``（sleep mode，下文简称Deep-LV）恢复CP运行现场的机制。
进入Deep-LV前，系统把CPU、NVIC、SCB、MPU、SAU、FPU和FreeRTOS执行现场保存到保持供电
的CP SRAM，并使CP CPU域掉电；CP SRAM和cache处于硬件Retention配置。唤醒时启动代码
识别 ``dlv_startup ``` 标志，恢复架构和FreeRTOS现场，最终返回睡眠前的执行点继续运行。

重要

CP快速启动不是Deep Sleep复位后由bootloader执行的fastboot的冷启动。本文只描述
`PM_MODE_LOW_VOLTAGE` sleep mode的Deep-LV现场保存与恢复；`PM_MODE_DEEP_SLEEP` 唤醒后的
复位启动不属于本机制。

<a id="cppsram"></a>

### CP恢复不依赖PSRAM

CP工程必须保持 `CONFIG_PSRAM_AS_SYS_MEMORY=n`。CP的任务栈、heap、TCB、全局变量及
Deep-LV上下文均位于CP SRAM，不使用PSRAM保存系统现场。因此CP快速恢复不依赖
`CONFIG_PSRAM_DATA_RETENTION_ENABLE`，也没有AP快速启动中的PSRAM controller/cell
恢复流程。

CP使用M52，CP恢复所需的代码、数据和上下文依赖CP SRAM/cache Retention及启动恢复路径。

<a id="id2"></a>

## 快速恢复与普通启动的区别

```
                       冷启动/普通复位                          CP快速恢复（Deep-LV）
             +----------------------------------+        +----------------------------------+
CP启动 --->  | 执行复位和完整启动流程           |        | CP SRAM和软件状态保持            |
             | 初始化C运行环境                  |        | dlv_startup识别恢复启动          |
             | 初始化FreeRTOS和系统服务         |        | 恢复CPU和FreeRTOS执行现场        |
             | 初始化CP基础驱动                 |        | SDK恢复UART/TIMER等基础资源      |
             | 初始化低功耗业务和应用           |        | 恢复Wi-Fi/BLE保活状态            |
             +----------------+-----------------+        +----------------+-----------------+
                              |                                           |
                              v                                           v
               业务从初始状态运行                             从睡眠前原执行点继续运行
```

按照当前BK7259 SDK的开发分工，大部分外设和多媒体应用运行在AP侧。CP侧主要承担电源管理、
唤醒源、Wi-Fi/BLE保活和少量基础驱动功能。SDK已经完成UART、TIMER等常用CP驱动以及
Wi-Fi、BLE保活场景的Deep-LV适配，用户不需要重复注册这些模块的回调，也不能占用它们
已经使用的 `dev_id` 回调槽位。

CP侧用户主要需要适配以下内容：

> - 根据业务状态判断何时允许进入低功耗，停止新请求并完成睡眠投票。
> - 配置产品实际使用的RTC、GPIO等唤醒源。
> - 验证基于低功耗的应用在唤醒后能够从原执行点继续运行。
> - 仅当用户新增CP侧驱动、直接操作掉电硬件，或现有SDK未覆盖特定场景时，才注册
>   `PM_MODE_LOW_VOLTAGE` enter/exit回调。

快速恢复后，原任务、任务栈、TCB、heap对象和CP SRAM变量继续使用原地址，应用入口不会因
本次Deep-LV恢复而重新执行。对于用户新增的CP驱动，软件对象仍存在并不代表硬件仍在运行：
外设寄存器、FIFO、BUSY状态、pending IRQ、DMA状态及中断中的事务不会自动保持。

<a id="id3"></a>

## 资源状态

| 资源 | 是否下电 | 是否Retention | 恢复方式 |
| --- | --- | --- | --- |
| CP SRAM | 否 | 是，硬件Retention | 原地保留数据、任务栈、TCB、heap和Deep-LV上下文。 |
| CP CPU | 是 | 否 | 软件保存并恢复寄存器和任务执行现场。 |
| CPU架构上下文 | 随CPU域丢失 | 否，软件备份 | 在CP SRAM中保存并恢复CPU、NVIC、SCB、MPU、SAU、FPU及SysTick相关状态。 |
| Cache | CPU域进入低功耗 | 是，硬件Retention配置 | 睡前清理D-cache并使I-cache失效；恢复时重建cache配置并使旧cache内容失效， 软件不能依赖睡前cache line或tag。 |
| CP外设 | 按对应电源/时钟域处理 | 否 | SDK已适配模块按既有流程恢复；用户新增驱动通过低压enter/exit回调恢复寄存器或 重新初始化。 |

备注

表中的“硬件Retention”表示对应存储资源在Deep-LV期间由硬件保持；CPU架构上下文是
软件备份到retained SRAM，不属于CPU硬件Retention。Cache虽配置为Retention，当前
恢复流程仍会清理或失效cache，用户不得把cache内容当作持久数据。

<a id="id4"></a>

## 配置

建议以 `projects/pm/pm/cp/config/bk7259/defconfig` 为基线移植，并检查最终生成的
配置，而不是只检查增量 `defconfig`。

<a id="id5"></a>

### 核心配置

```
CONFIG_DEEP_LV=y
CONFIG_FREERTOS_USE_TICKLESS_IDLE=2
CONFIG_PSRAM_AS_SYS_MEMORY=n
```

`CONFIG_DEEP_LV` 启用CP CPU域掉电和 `dlv_startup` 恢复路径；
`CONFIG_FREERTOS_USE_TICKLESS_IDLE=2` 使空闲任务进入电源管理流程。
`CONFIG_PSRAM_AS_SYS_MEMORY=n` 保证CP系统现场不放入PSRAM。

`CONFIG_PM_AP_POWERDOWN_WHEN_LV` 只控制进入低压睡眠时是否同时关闭AP，不是CP快速恢复
的核心开关。需要AP协同时，另请参考 [AP快速启动配置说明](bk_ap_fast_boot_config.md)；不要将AP快速启动的
PSRAM、DTCM或AP多核恢复要求写入CP恢复流程。

<a id="id6"></a>

### 调试配置

以下配置用于定位问题，不是CP快速启动的必选项：

```
CONFIG_DEEP_LV_DEBUG_GPIO=y
CONFIG_DEEP_LV_DEBUG_LOG=y
CONFIG_PM_CP_DEEP_LV_SRAM_CHECK=y
```

`CONFIG_DEEP_LV_DEBUG_GPIO` 输出GPIO时序标记，
`CONFIG_DEEP_LV_DEBUG_LOG` 输出Deep-LV AON快照日志，
`CONFIG_PM_CP_DEEP_LV_SRAM_CHECK` 在睡眠前后校验CP SRAM。正式功耗和性能验收时应评估
并关闭不需要的调试项，避免测量结果受调试开销影响。

<a id="id7"></a>

### 唤醒源配置

使用AON RTC时需配置 `CONFIG_AON_RTC=y`，注册RTC alarm后调用：

```
bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_RTC, NULL);
```

使用GPIO时需按工程要求启用 `CONFIG_GPIO_WAKEUP_SUPPORT=y`；需要动态注册时还应启用
`CONFIG_GPIO_DYNAMIC_WAKEUP_SUPPORT=y`，并在设置系统唤醒源前注册GPIO：

```
bk_gpio_register_wakeup_source(GPIO_18, GPIO_INT_TYPE_FALLING_EDGE);
bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_GPIO, NULL);
```

完整RTC和GPIO配置分别参见 [设置RTC作为唤醒源-系统进入深度、超深度睡眠以及睡眠模式配置说明](bk_rtc_sleep.md) 和 [设置GPIO作为唤醒源-系统进入深度、超深度睡眠以及睡眠模式配置说明](bk_gpio_sleep.md)。

<a id="id8"></a>

## 用户接入流程

1. 以上述CP工程为基线启用核心配置，并确认CP系统内存未放入PSRAM。
2. 配置并验证至少一个Deep-LV唤醒源。
3. 确认产品使用的UART、TIMER、Wi-Fi和BLE等SDK模块已经按现有流程完成初始化和投票，
   不重复注册其低压回调。
4. 仅梳理用户新增的CP驱动或低功耗应用所使用的掉电资源；需要恢复硬件时注册
   `PM_MODE_LOW_VOLTAGE` enter/exit回调。
5. 根据业务状态判断是否允许睡眠，在普通任务上下文停止新事务并等待已提交事务有界结束；
   不要把业务排空和等待工作留给回调。
6. 调用 `bk_pm_sleep_mode_set(PM_MODE_LOW_VOLTAGE)` 选择低压睡眠。
7. 业务准备完成后，通过 `bk_pm_module_vote_sleep_ctrl()` 投睡眠票；Wi-Fi、Bluetooth
   等模块仍需按各自流程完成睡眠投票。
8. 唤醒后重点检查低功耗应用的状态连续性，以及用户新增驱动的恢复结果，再允许提交新事务。

典型入口如下：

```
/* 唤醒源和用户新增驱动所需的回调应在此之前完成配置。 */
bk_pm_sleep_mode_set(PM_MODE_LOW_VOLTAGE);

/* 应用已停止新事务，并确认已有事务结束后再投票。 */
bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP, 1, 0);
```

取消应用睡眠条件时，使用同一模块撤销睡眠票：

```
bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP, 0, 0);
```

该流程使用通用PM接口，不存在也不需要 `cp_fast_boot` 专用CLI。

<a id="id9"></a>

## 低压回调接口

SDK已有的CP基础驱动和Wi-Fi/BLE保活流程已经完成低压适配。仅当用户新增CP驱动、直接管理
掉电硬件或需要补充特定恢复流程时，才通过 `cp/include/modules/pm.h` 中的接口注册
低压睡眠回调：

```
typedef int (*pm_cb)(uint64_t sleep_time, void *args);

typedef struct {
    pm_cb cb;
    void *args;
} pm_cb_conf_t;

bk_err_t bk_pm_sleep_register_cb(
    pm_sleep_mode_e sleep_mode,
    pm_dev_id_e dev_id,
    pm_cb_conf_t *enter_config,
    pm_cb_conf_t *exit_config);
```

enter回调在关闭资源并进入Deep-LV前执行，exit回调在唤醒并完成基础恢复后执行。两类回调
均按 `dev_id` 从小到大调用，当前传入的 `sleep_time` 固定为0。

警告

enter和exit回调都位于全局中断关闭的关键路径。回调必须短小、确定、非阻塞，只访问
必要寄存器和retained SRAM。禁止日志、delay、锁、queue/semaphore、动态内存、
等待中断，以及任何可能触发RTOS调度或阻塞的操作。

<a id="id10"></a>

### 注册规则和当前限制

> - `dev_id` 必须小于 `PM_DEV_ID_MAX`，并由模块独占；低压模式使用按 `dev_id`
>   索引的enter/exit固定槽位。
> - 同一 `dev_id` 后注册的非空enter或exit回调会覆盖先前对应槽位，不会形成回调链。
> - 只有 `PM_MODE_LOW_VOLTAGE` 同时使用enter和exit固定槽位；其他睡眠模式的组织方式
>   不同，不应依赖本节规则。
> - 当前注册框架忽略回调返回值，回调返回非零不能中止睡眠，也不能触发回滚。
> - 当前注册API对不支持的模式、越界 `dev_id`、空回调等无效配置仍可能返回
>   `BK_OK`。调用者必须自行保证模式、ID、函数和参数合法，不能仅靠返回值判断已注册。
> - 注销使用
>   `bk_pm_sleep_unregister_cb(PM_MODE_LOW_VOLTAGE, dev_id, enter_cb, exit_cb)`。应传入合法
>   `dev_id`，并在模块仍正常运行、不会同时进入睡眠时完成注册或注销。

<a id="id11"></a>

### 用户代码示例

以下示例展示一个由用户驱动独占 `PM_DEV_ID_TIMER_3` 槽位的寄存器备份方案。实际驱动
应替换寄存器地址和有效配置字段，并确保这些指针及上下文位于CP SRAM。示例只恢复静态
配置，不保存计数值、FIFO、BUSY、pending IRQ或正在执行的事务。

```
#include <stdint.h>
#include <stdbool.h>
#include <modules/pm.h>

typedef struct {
    volatile uint32_t *ctrl_reg;
    volatile uint32_t *period_reg;
    uint32_t saved_ctrl;
    uint32_t saved_period;
    volatile bool restore_done;
} user_timer_pm_t;

static user_timer_pm_t s_timer_pm;

static int user_timer_lv_enter(uint64_t sleep_time, void *args)
{
    user_timer_pm_t *ctx = (user_timer_pm_t *)args;
    (void)sleep_time; /* 当前框架固定传0。 */

    ctx->saved_ctrl = *ctx->ctrl_reg;
    ctx->saved_period = *ctx->period_reg;
    *ctx->ctrl_reg = 0; /* 驱动定义的同步停止动作；不得等待中断。 */
    ctx->restore_done = false;
    return 0;           /* 当前框架不会检查该返回值。 */
}

static int user_timer_lv_exit(uint64_t sleep_time, void *args)
{
    user_timer_pm_t *ctx = (user_timer_pm_t *)args;
    (void)sleep_time;

    *ctx->period_reg = ctx->saved_period;
    *ctx->ctrl_reg = ctx->saved_ctrl;
    ctx->restore_done = true;
    return 0;
}

bk_err_t user_timer_pm_init(volatile uint32_t *ctrl,
                            volatile uint32_t *period)
{
    static pm_cb_conf_t enter_config = {
        .cb = user_timer_lv_enter,
        .args = &s_timer_pm,
    };
    static pm_cb_conf_t exit_config = {
        .cb = user_timer_lv_exit,
        .args = &s_timer_pm,
    };

    if ((ctrl == NULL) || (period == NULL)) {
        return BK_FAIL;
    }

    s_timer_pm.ctrl_reg = ctrl;
    s_timer_pm.period_reg = period;
    enter_config.args = &s_timer_pm;
    exit_config.args = &s_timer_pm;

    return bk_pm_sleep_register_cb(PM_MODE_LOW_VOLTAGE,
                                   PM_DEV_ID_TIMER_3,
                                   &enter_config,
                                   &exit_config);
}

bk_err_t user_timer_pm_deinit(void)
{
    return bk_pm_sleep_unregister_cb(PM_MODE_LOW_VOLTAGE,
                                     PM_DEV_ID_TIMER_3,
                                     true,
                                     true);
}
```

因为注册API当前可能对无效输入返回 `BK_OK`，初始化代码仍需在调用前验证指针，确认
`PM_DEV_ID_TIMER_3` 没有被其他模块使用，并通过实际睡眠/唤醒测试验证回调已经执行。
`restore_done` 只能由唤醒后的任务读取；不要在exit回调中发送queue或semaphore。

<a id="id12"></a>

## 驱动恢复策略

用户新增的CP驱动可按硬件特点选择一种策略：

> - **寄存器备份/恢复：** enter回调把仍有效的静态配置寄存器保存到CP SRAM并安全停止
>   硬件，exit回调按依赖顺序写回。只适合少量、明确且可同步访问的寄存器。
> - **重新初始化：** enter回调只执行最小同步停机；exit回调执行不阻塞的最小硬件恢复，
>   复杂初始化由唤醒后的普通任务根据保留的配置重新执行。

无论采用哪种策略，都不得恢复旧FIFO内容、BUSY状态、pending IRQ或中断中的事务。睡前
必须在普通任务上下文拒绝新请求并让DMA、总线传输和异步事务有界结束。驱动恢复应幂等，
且不能重复创建仍保留在CP SRAM中的mutex、queue、semaphore、task或heap对象。

<a id="id13"></a>

## 失败处理与限制

> - enter/exit回调返回值当前被框架忽略，不能用返回值阻止Deep-LV。可能失败的检查和有界
>   等待必须在投睡眠票之前完成。
> - 回调中发现异常时，只能把错误标志写入retained SRAM并执行安全的最小处理；全局中断
>   恢复后再由任务读取标志、记录日志、重新初始化或停止相关业务。
> - 如果CP SRAM校验失败、恢复后发生Fault，或关键驱动不能恢复，应停止继续使用旧业务
>   状态并转入产品定义的安全复位/冷启动路径。
> - Deep-LV不保证外设事务连续。任何无法在睡前排空且无法在唤醒后重建的业务，都不应在
>   活动期间允许系统进入低压睡眠。
> - 唤醒耗时取决于芯片配置、时钟、电源、唤醒源和回调实现；本文不承诺未经目标工程和
>   目标板验证的固定毫秒指标。

<a id="id14"></a>

## 调试与验收

建议先仅保留一个RTC或GPIO唤醒源和最少业务，再逐步加入驱动回调。验收至少包括：

> - 验证每次进入的是 `PM_MODE_LOW_VOLTAGE` Deep-LV，而不是Deep Sleep复位启动。
> - 在任务栈、heap和静态变量中放置连续性标记，确认唤醒后原任务从原执行点继续。
> - 开启 `CONFIG_PM_CP_DEEP_LV_SRAM_CHECK` 时确认CP SRAM睡前/睡后校验无异常。
> - 检查SDK已适配模块和用户新增驱动的配置、时钟、中断及首个新事务；确认没有恢复旧
>   FIFO、BUSY、pending IRQ、DMA或中断中的事务。
> - 覆盖RTC、GPIO及产品实际唤醒源，验证唤醒原因和重复睡眠/唤醒循环。
> - 覆盖空闲、业务切换、通信停止边界和异常恢复场景，确认无HardFault、MemFault、
>   UsageFault、死锁或永久无法再次睡眠。
> - 关闭详细日志后测量低功耗电流和恢复时间，并以目标板、量产配置的实测结果验收。

<a id="id15"></a>

## 常见问题

<a id="id16"></a>

### 唤醒后重新执行了应用初始化

本次可能走了冷启动、普通复位或Deep Sleep路径，而不是Deep-LV快速恢复。检查最终配置中
`CONFIG_DEEP_LV`、睡眠模式、唤醒原因和 `dlv_startup` 恢复路径。

<a id="id17"></a>

### 变量正常但外设异常

CP SRAM保持成功不等于外设状态保持。对于SDK已有模块，先检查对应功能配置和睡眠投票；
对于用户新增驱动，确认已注册低压enter/exit回调，并选择了寄存器恢复或重新初始化策略。
同时确认睡前已停止DMA和异步事务。

<a id="id18"></a>

### 注册返回成功但回调没有执行

当前API可能对不支持模式或无效配置返回 `BK_OK`。检查是否使用
`PM_MODE_LOW_VOLTAGE`、`dev_id < PM_DEV_ID_MAX`、回调是否非空，以及同一 `dev_id`
是否被后注册模块覆盖。

<a id="psram-retention"></a>

### 是否需要开启PSRAM retention

CP快速恢复不需要。保持 `CONFIG_PSRAM_AS_SYS_MEMORY=n`，CP系统现场位于CP SRAM。
`CONFIG_PSRAM_DATA_RETENTION_ENABLE` 属于使用PSRAM数据保持的其他流程，不是CP
Deep-LV恢复的依赖。

<a id="dtcm"></a>

### 是否需要备份DTCM

不需要。当前CP M52 Deep-LV流程未调用ITCM/DTCM save/restore；不要照搬AP的DTCM备份
路径。

<a id="id19"></a>

## 相关代码和文档

> - 工程基线：`projects/pm/pm/cp/config/bk7259/defconfig`
> - PM公开接口：`cp/include/modules/pm.h`
> - 低压回调注册与调用：`cp/components/bk_pm/src/services/bk_pm_sleep.c`
> - CPU与架构现场保存恢复：`cp/middleware/driver/deep_lv/deep_lv.c`
> - Deep-LV启动入口：`cp/middleware/soc/bk7259/soc_init.c`
> - Deep-LV电源与Retention配置：`cp/middleware/soc/bk7259/hal/sys_pm_hal.c`
> - 工程配置说明：[低功耗工程配置说明](bk_lowpower_project_config.md)
> - 睡眠模式说明：[睡眠模式说明](bk_sleep_mode.md)
> - GPIO唤醒说明：[设置GPIO作为唤醒源-系统进入深度、超深度睡眠以及睡眠模式配置说明](bk_gpio_sleep.md)
> - RTC唤醒说明：[设置RTC作为唤醒源-系统进入深度、超深度睡眠以及睡眠模式配置说明](bk_rtc_sleep.md)
> - AP协同快速启动：[AP快速启动配置说明](bk_ap_fast_boot_config.md)
