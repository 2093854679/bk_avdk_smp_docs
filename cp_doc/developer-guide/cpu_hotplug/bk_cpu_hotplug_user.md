# CPU Hotplug 使用指南（CP）



## 1 功能简介

CPU Hotplug 允许在系统运行过程中动态下线（offline）和上线（online）CP 从核，
从而在负载较轻时关闭从核以降低功耗，在负载升高时再把从核拉起来恢复算力。

CP 子系统是一个独立的 2-core FreeRTOS SMP：

CP hotplug 角色映射

| 主核（不可下线） | 从核（可 hotplug） | CPU 架构 | CLI 前缀 |
| --- | --- | --- | --- |
| CPU0 | CPU1 | Cortex-M52 | `cpu ...` |

CP 只能 hotplug 从核 CPU1。主核 CPU0 是 tick owner，不支持下线。下线 / 上线采用
graceful（优雅）方式，即先迁移任务和中断、等待从核安全停下后再复位，不会丢任务、
不会破坏系统状态。

重要

当前版本仅支持 CP 从核 CPU1 的 graceful offline/online，不支持主核 CPU0 下线，
不支持强制（force）复位。如果 CPU1 上存在 **hard-pin 到该核的任务** 或

**不可迁移的中断**，offline 会被拒绝并返回 `BK_ERR_BUSY`。


## 2 三种使用方式

CPU Hotplug 提供三种使用方式，可按需选择：

1. **手动 CLI**：在串口下用 `cpu offline` / `cpu online` 手动控制，便于调试和验证；
2. **应用 API**：在应用代码里调用 `bk_cpu_hp_offline()` / `bk_cpu_hp_online()`，
   按业务逻辑控制从核上下线；
3. **动态负载策略（governor）**：内核根据 CPU 负载自动上下线从核，应用无需关心，可按需开关（见第 5 章）。


## 3 配置与默认上电行为


### 3.1 配置项

通过 `menuconfig` 配置：

主要配置项

| 配置项 | CP 默认 | 说明 |
| --- | --- | --- |
| `CONFIG_CPU_HOTPLUG` | y | 使能 CPU Hotplug 功能（依赖 `SOC_SMP`） |
| `CONFIG_CPU_HOTPLUG_BOOT_OFFLINE` | y | 上电时从核是否保持 offline，见 3.2 |
| `CONFIG_CPU_HP_GOVERNOR` | y | 使能动态负载策略，自动上下线从核，见第 5 章 |


### 3.2 默认上电行为

从核上电后处于什么状态，由 `CONFIG_CPU_HOTPLUG_BOOT_OFFLINE` 决定。CP 默认

**打开**：上电后 **只有主核 CPU0 online，从核 CPU1 保持 offline**，直到通过
`cpu online` 命令、API 或 governor 把它拉起来，适合默认低功耗、按需扩核的场景。

因此 CP 子系统默认上电后 CPU1 是 offline 的，配合默认开启的 governor。governor
会在负载升高时自动把 CPU1 拉起，使系统任务调度处理能力最大化；负载下降时再自动
放下，以节省功耗。

备注

上电后可用 `cpu state` 确认实际状态：CP 默认会看到 `cpu1: state=offline`。


## 4 CLI 使用方法

CP 命令直接在 CP CLI 通道输入:


```
cpu list                   # 查看 CP 两个 CPU 的状态
cpu state                  # 同 list
cpu offline 1              # 下线从核 CPU1
cpu online 1               # 上线从核 CPU1
cpu gov on                 # 打开动态负载策略
cpu gov off                # 关闭动态负载策略
cpu gov status             # 查看 governor 状态和实时负载

```

命令说明：


- `cpu list` / `cpu state`：显示 CPU0/CPU1 的 state、online、active；

- `cpu offline 1` / `cpu online 1`：手动下线 / 上线从核 CPU1；

- `cpu gov on|off`：打开 / 关闭动态负载策略；

- `cpu gov status`：查看 governor 是否使能、从核是否在线、各核负载和切换计数。

还有几条用于调试 / 自测的命令：


- `cpu irq-affinity` ：dump 中断路由

- `cpu task-affinity` ：检查是否有 hard-pin 任务

- `cpu stress 1 <loops>` ：offline/online 循环压测

- `cpu busy-test` ：验证 pinned 任务场景返回 busy

- `cpu gov stress <cycles>` ：governor 压测


## 5 动态负载策略（Governor）

使能 `CONFIG_CPU_HP_GOVERNOR` 后，内核会周期性采样各核 CPU 负载，并自动上下线
从核，应用层无需手动调用 offline/online。

策略：


- 当 **主核负载持续偏高** （主核 load 超过上门限）时，自动 online 从核分担负载；

- 当 **两核合计负载持续偏低** （主核 + 从核 load 低于下门限）时，自动 offline 从核
  以省电；

- 为防止频繁抖动（flapping），采用「上下门限不对称 + 连续多次采样去抖 + 切换后冷却」
  三重保护。

可调参数（`menuconfig` 中 `CONFIG_CPU_HP_GOVERNOR_*`）：

Governor 参数

| 配置项 | 默认值 | 说明 |
| --- | --- | --- |
| `CPU_HP_GOVERNOR_AUTOSTART` | y | 上电后是否立即自动调节（否则需 `cpu gov on`） |
| `CPU_HP_GOVERNOR_UP_THRESHOLD` | 80 | 主核负载超过该百分比则准备 online 从核 |
| `CPU_HP_GOVERNOR_DOWN_THRESHOLD` | 60 | 两核合计负载低于该百分比则准备 offline 从核 |
| `CPU_HP_GOVERNOR_PERIOD_MS` | 100 | 负载采样周期（ms） |
| `CPU_HP_GOVERNOR_UP_DEBOUNCE` | 2 | 连续多少次过载采样后才 online |
| `CPU_HP_GOVERNOR_DOWN_DEBOUNCE` | 5 | 连续多少次轻载采样后才 offline |
| `CPU_HP_GOVERNOR_COOLDOWN_MS` | 1000 | 每次切换后的最小冷却时间（ms） |
| `CPU_HP_GOVERNOR_LOAD_EMA_DIV` | 1 | 负载平滑系数（EMA），默认直接使用当前负载 |

运行时可用 `cpu gov on/off` 临时开关，`cpu gov status` 观察当前负载与切换情况。
若从核上有 hard-pin 任务导致无法 offline，governor 会自动跳过、下个周期再评估。


## 6 应用 API

接口声明在 CP 的 `multicore_driver.h`，以 CP 从核 `CPU1_CORE_ID` 为操作对象。


```
/* 上下线 */
bk_err_t bk_cpu_hp_offline(uint32_t cpu_id);
bk_err_t bk_cpu_hp_online(uint32_t cpu_id);

/* 状态查询 */
uint32_t bk_cpu_hp_is_online(uint32_t cpu_id);
uint32_t bk_cpu_hp_is_active(uint32_t cpu_id);
const char *bk_cpu_hp_get_state_name(uint32_t cpu_id);

/* 在主核上执行 hotplug：把当前任务临时迁到主核 / 恢复原 core */
uint32_t bk_cpu_hp_enter_primary(void);
void bk_cpu_hp_exit_primary(uint32_t old_core_id);

/* 动态负载策略（CONFIG_CPU_HP_GOVERNOR）*/
bk_err_t bk_cpu_hp_governor_start(void);
bk_err_t bk_cpu_hp_governor_stop(void);
void bk_cpu_hp_governor_get_status(bk_cpu_hp_governor_status_t *status);

```

返回值：


- `BK_OK`：成功，或目标已处于期望状态；

- `BK_ERR_NOT_SUPPORT`：目标不是 CP 从核 CPU1；

- `BK_ERR_STATE`：调用者不在 CP 主核 CPU0 上下文，或状态不允许；

- `BK_ERR_BUSY`：从核上有 hard-pin 任务 / 不可迁移中断，或正在状态切换中；

- `BK_ERR_TIMEOUT`：等待从核停核 / 启核握手超时。

使用示例：


```
bk_err_t ret;

ret = bk_cpu_hp_offline(CPU1_CORE_ID);
if (ret != BK_OK) {
    return ret;
}

/* 从核 offline 期间，未绑核的任务会自动跑在主核上 */

ret = bk_cpu_hp_online(CPU1_CORE_ID);
return ret;

```

备注

`bk_cpu_hp_offline()` / `bk_cpu_hp_online()` 内部已包含任务迁移，
无需手动调用 `bk_cpu_hp_enter_primary()` / `bk_cpu_hp_exit_primary()`。
可在任意核的非绑核任务上调用，内部会自动把当前任务临时迁到主核再执行。

警告

`bk_cpu_hp_offline()` / `bk_cpu_hp_online()` **只能在任务（task）上下文
中调用，禁止在任何中断上下文中调用**，一旦在中断上下文中调用会立即触发断言，
而不是返回错误码。二者内部需要与从核握手并存在不确定的等待，建议运行在可睡眠、
可调度的任务上下文中。
