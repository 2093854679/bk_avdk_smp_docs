---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/cpu_hotplug/bk_cpu_hotplug_user.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cpu-hotplug-cp"></a>

# CPU Hotplug 使用指南（CP）

<a id="id1"></a>

## 1 功能简介

CPU Hotplug 允许在系统运行过程中动态下线（offline）和上线（online）CP 从核，
从而在负载较轻时关闭从核以降低功耗，在负载升高时再把从核拉起来恢复算力。

CP 子系统是一个独立的 2-core FreeRTOS SMP：

<a id="id6"></a>

CP hotplug 角色映射


| 主核（不可下线） | 从核（可 hotplug） | CLI 前缀 |
| --- | --- | --- |
| CPU0 | CPU1 | `cpu ...` |

CP 只能 hotplug 从核 CPU1。主核 CPU0 是 tick owner，不支持下线。下线 / 上线采用
graceful（优雅）方式，即先迁移任务和中断、等待从核安全停下后再复位，不会丢任务、
不会破坏系统状态。

重要

当前版本仅支持 CP 从核 CPU1 的 graceful offline/online，不支持主核 CPU0 下线。
如果 CPU1 上存在 **hard-pin 到该核的任务** 或 **不可迁移的中断**，offline 会被
拒绝并返回 `BK_ERR_BUSY`。所有上下线（含 `_direct` 变体）都走同一套 graceful
握手，不存在跳过握手、直接硬复位从核的接口；`_direct` 仅表示绕过投票层计票
（见第 6、7 章），并非 ungraceful 复位。

<a id="id2"></a>

## 2 四种使用方式

CPU Hotplug 提供四种使用方式，可按需选择：

1. **手动 CLI**：在串口下用 `cpu offline` / `cpu online` 手动控制，便于调试和验证；
2. **应用 API**：在应用代码里调用 `bk_cpu_hp_offline()` / `bk_cpu_hp_online()`，
   按业务逻辑控制从核上下线；
3. **投票层（vote）**：多个模块各自作为 voter（投票者）表达对从核 online 的诉求，
   由投票层按「或上线、与下线」聚合后统一驱动 hotplug，避免多个模块直接调用
   offline/online 相互覆盖，应用只需管理自己的一票（见第 6 章）；
4. **动态负载策略（governor）**：内核根据 CPU 负载自动上下线从核，应用无需关心，可按需开关（见第 5 章）。

警告

在使用 **投票层（vote）** 的情况下不使用 **应用 API** 与 **手动 CLI** 。
如果需要直接尝试上下电且绕过投票层计票，调用 `bk_cpu_hp_offline_direct()` / `bk_cpu_hp_online_direct()`，但这会使投票层计票脱节。

<a id="id3"></a>

## 3 配置与默认上电行为

<a id="id4"></a>

### 3.1 配置项

通过 `menuconfig` 配置：

<a id="id7"></a>

主要配置项


| 配置项 | CP 默认 | 说明 |
| --- | --- | --- |
| `CONFIG_CPU_HOTPLUG` | y | 使能 CPU Hotplug 功能（依赖 `SOC_SMP`） |
| `CONFIG_CPU_HOTPLUG_BOOT_OFFLINE` | y | 上电时从核是否保持 offline，见 3.2 |
| `CONFIG_CPU_HP_VOTE` | y | 使能投票层，多模块投票聚合驱动从核上下线，见第 6 章 |
| `CONFIG_CPU_HP_GOVERNOR` | n | 使能动态负载策略，自动上下线从核，见第 5 章 |

<a id="id5"></a>

### 3.2 默认上电行为

从核上电后处于什么状态，由 `CONFIG_CPU_HOTPLUG_BOOT_OFFLINE` 决定。CP 默认
**打开**：上电后 **只有主核 CPU0 online，从核 CPU1 保持 offline**，直到通过
`cpu online` 命令、API 或投票层把它拉起来，适合默认低功耗、按需扩核的场景。

CP 子系统默认 **启用投票层** （`CONFIG_CPU_HP_VOTE=y`）、**不启用 governor**
（`CONFIG_CPU_HP_GOVERNOR=n`）：CPU1 上电后为 offline，由各业务模块通过 voter
表达诉求按需拉起，当没有任何 voter 持票时自动放下以省电（聚合规则见第 6 章）。
若希望改为按 CPU 负载自动调节，可在 menuconfig 中打开 governor（见第 5 章）。

备注

上电后可用 `cpu state` 确认实际状态：CP 默认会看到 `cpu1: state=offline`。

<a id="cli"></a>

## 4 CLI 使用方法

CP 命令直接在 CP CLI 通道输入 (部分命令需要开启相关功能):

```
cpu list                   # 查看 CP 两个 CPU 的状态
cpu state                  # 同 list
cpu offline 1              # 下线从核 CPU1
cpu online 1               # 上线从核 CPU1
cpu gov on                 # 打开动态负载策略
cpu gov off                # 关闭动态负载策略
cpu gov status             # 查看 governor 状态和实时负载
cpu vote reg <name>        # 注册一个名为 <name> 的 voter
cpu vote on <name>         # 该 voter 投 online（按需拉起从核）
cpu vote off <name>        # 该 voter 投 offline（释放）
cpu vote unreg <name>      # 注销 voter（等价于先投 offline 再释放）
cpu vote status            # 查看计票与各 voter 状态
```

命令说明：

- `cpu list` / `cpu state`：显示 CPU0/CPU1 的 state、online、active；
- `cpu offline 1` / `cpu online 1`：手动下线 / 上线从核 CPU1；
- `cpu gov on|off`：打开 / 关闭动态负载策略；
- `cpu gov status`：查看 governor 是否使能、从核是否在线、各核负载和切换计数；
- `cpu vote reg|unreg|on|off <name>`：注册 / 注销 voter、投 online / offline；
- `cpu vote status`：查看当前计票（online\_count / voter\_count）与各 voter 状态。

还有几条用于调试 / 自测的命令：

- `cpu irq-affinity` ：dump 中断路由
- `cpu task-affinity` ：检查是否有 hard-pin 任务
- `cpu stress 1 <loops>` ：offline/online 循环压测
- `cpu busy-test` ：验证 pinned 任务场景返回 busy
- `cpu gov stress <cycles>` ：governor 压测

<a id="governor"></a>

## 5 动态负载策略（Governor）

使能 `CONFIG_CPU_HP_GOVERNOR` 后，内核会周期性采样各核 CPU 负载，并自动上下线
从核，应用层无需手动调用 offline/online。

策略：

- 当 **主核负载持续偏高** （主核 load 超过上门限）时，自动 online 从核分担负载；
- 当 **两核合计负载持续偏低** （主核 \+ 从核 load 低于下门限）时，自动 offline 从核
  以省电；
- 为防止频繁抖动（flapping），采用「上下门限不对称 \+ 连续多次采样去抖 \+ 切换后冷却」
  三重保护。

可调参数（`menuconfig` 中 `CONFIG_CPU_HP_GOVERNOR_*`）：

<a id="id8"></a>

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

<a id="voting-layer"></a>

## 6 投票层（Voting Layer）

使能 `CONFIG_CPU_HP_VOTE` 后，多个模块可以各自作为一个 **voter（投票者）** 表达
对从核 CPU1 是否需要 online 的诉求，由投票层聚合后统一驱动 hotplug，避免多个模块
直接调用 offline/online 相互覆盖。

可调参数（`menuconfig` 中 `CONFIG_CPU_HP_VOTE_*`）：

<a id="id9"></a>

Voter 参数


| 配置项 | 默认值 | 说明 |
| --- | --- | --- |
| `CONFIG_CPU_HP_VOTE_MAX_VOTERS` | 64 | 最大可注册的 voter 数 |
| `CONFIG_CPU_HP_VOTE_DUMP` | y | 使能 `bk_cpu_hp_vote_dump()`，打印逐 voter 列表（用户句柄单链表串联） |
| `CONFIG_CPU_HP_VOTE_NAME` | n | 是否为每个 voter 记录 name（供 find/dump 使用） |
| `CONFIG_CPU_HP_VOTE_NAME_LEN` | 16 | voter name 缓冲长度（依赖 `CPU_HP_VOTE_NAME`） |
| `CONFIG_CPU_HP_VOTE_STATIC` | n | voter 句柄改用静态池分配（不使用 malloc） |
| `CONFIG_CPU_HP_VOTE_FIND` | n | 使能 `bk_cpu_hp_vote_find()` 按 name 查找（依赖 `CPU_HP_VOTE_NAME` 与 `CPU_HP_VOTE_DUMP`） |

聚合规则为 **「或上线、与下线」**：

- 只要 **任意一个** voter 投 online，从核 CPU1 就会被拉起（online）；
- 只有 **全部** voter 都释放（投 offline 或注销）后，从核 CPU1 才会被放下（offline）。

为使计票始终与 hotplug 物理态一致， **voter 注册时会按当前核的在线状态对齐初值** ——
若注册时 CPU1 已在线（如 boot-online 场景），该 voter 初值即为 online 并计入计票；
若注册时 CPU1 已离线，初值为 offline。

备注

由于注册按当前核态对齐，多个「在核在线时注册」的 voter 会各自持有一张 online
票，核需等这些票全部释放后才下电。若某模块只是注册而当前并不需要核在线，应在
注册后显式投 offline 释放，以免钉住从核。此外不要把手动 `cpu offline/online`
与投票混用，否则计票会与物理态脱节。

典型用法：某业务模块启动重负载任务前，注册一个 voter 并投 online 把从核拉起；任务
结束后投 offline 或注销，让投票层在没有其他 voter 持票时自动把从核放下。

运行时可用 `cpu vote status` 查看当前计票与各 voter 状态（开启 `CPU_HP_VOTE_NAME` 与 `CPU_HP_VOTE_DUMP` 时效果最好）。
voter 的编程接口见第 7 章。

备注

投票层与 governor 是两套独立机制：投票层按模块诉求上下线，governor 按 CPU
负载上下线。二者可同时使能，但两者逻辑上存在冲突，通常按方案二选一作为默认驱动方式。
CP 默认启用投票层、不启用 governor。

<a id="api"></a>

## 7 应用 API

接口声明在 CP 的 `multicore_driver.h`，以 CP 从核 `CPU1_CORE_ID` 为操作对象。下面列出主要使用接口：

```
/* 上下线（未使能投票层时的直接接口）*/
bk_err_t bk_cpu_hp_offline(uint32_t cpu_id);
bk_err_t bk_cpu_hp_online(uint32_t cpu_id);

/* 直接上下线（direct）：绕过投票层计票，直接驱动 hotplug（仍为 graceful 握手）*/
bk_err_t bk_cpu_hp_offline_direct(uint32_t cpu_id);
bk_err_t bk_cpu_hp_online_direct(uint32_t cpu_id);

/* 状态查询 */
uint32_t bk_cpu_hp_is_online(uint32_t cpu_id); /* 是否在线 */

/* 动态负载策略（CONFIG_CPU_HP_GOVERNOR）*/
bk_err_t bk_cpu_hp_governor_start(void);
bk_err_t bk_cpu_hp_governor_stop(void);
void bk_cpu_hp_governor_get_status(bk_cpu_hp_governor_status_t *status);

/* 投票层（CONFIG_CPU_HP_VOTE）*/
cpu_hp_voter_handle_t bk_cpu_hp_vote_register(const char *name);
bk_err_t bk_cpu_hp_vote_unregister(cpu_hp_voter_handle_t voter);
bk_err_t bk_cpu_hp_vote_online(cpu_hp_voter_handle_t voter);
bk_err_t bk_cpu_hp_vote_offline(cpu_hp_voter_handle_t voter);
bk_err_t bk_cpu_hp_vote_get_wanted(cpu_hp_voter_handle_t voter, uint32_t *wanted); /* 获取该 voter 的当前票状态 */
uint32_t bk_cpu_hp_vote_get_online_count(void); /* 获取当前在线的 voter 数 */
uint32_t bk_cpu_hp_vote_get_voter_count(void);  /* 获取当前注册的 voter 数 */
/* 仅在对应宏开启时提供 */
cpu_hp_voter_handle_t bk_cpu_hp_vote_find(const char *name); /* CONFIG_CPU_HP_VOTE_FIND */
void bk_cpu_hp_vote_dump(void);                              /* CONFIG_CPU_HP_VOTE_DUMP */
```

返回值：

- `BK_OK`：成功，或目标已处于期望状态；
- `BK_ERR_NOT_SUPPORT`：目标不是 CP 从核 CPU1；或在使能投票层
  （`CONFIG_CPU_HP_VOTE`，CP 默认开启）时直接调用了 `bk_cpu_hp_offline()` /
  `bk_cpu_hp_online()` —— 此时这两个接口不生效，应改用投票层接口，或用
  `bk_cpu_hp_offline_direct()` / `bk_cpu_hp_online_direct()` 绕过计票；
- `BK_ERR_STATE`：调用者不在 CP 主核 CPU0 上下文，或状态不允许；
- `BK_ERR_BUSY`：从核上有 hard-pin 任务 / 不可迁移中断，或正在状态切换中；
- `BK_ERR_TIMEOUT`：等待从核停核 / 启核握手超时。

重要

CP 默认启用投票层（`CONFIG_CPU_HP_VOTE=y`），此时下面示例中的
`bk_cpu_hp_offline()` / `bk_cpu_hp_online()` 会返回 `BK_ERR_NOT_SUPPORT`
而不生效。请改用投票层接口（第 6 章），或换成 `bk_cpu_hp_offline_direct()` /
`bk_cpu_hp_online_direct()`。下面的直接调用示例仅在关闭投票层
（`CONFIG_CPU_HP_VOTE=n`）时适用。

使用示例（投票层关闭时）：

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
可在任意核的非绑核任务上调用，内部会自动把当前任务临时迁到主核再执行。（包括 `_direct` 变体）

警告

`bk_cpu_hp_offline()` / `bk_cpu_hp_online()` **只能在任务（task）上下文
中调用，禁止在任何中断上下文中调用**，一旦在中断上下文中调用会立即触发断言，
而不是返回错误码。二者内部需要与从核握手并存在不确定的等待，建议运行在可睡眠、
可调度的任务上下文中。（包括 `_direct` 变体）

投票层接口（`CONFIG_CPU_HP_VOTE`）以 voter 句柄为操作对象，返回值：

- `bk_cpu_hp_vote_register()`：返回 voter 句柄；`name` 为 NULL 或 voter 表已满时返回 NULL；注册时按当前核在线状态设定该 voter 的初始票（boot-online 则初值为 online），只记账不下发 hotplug；
- `BK_OK`：投票成功（含目标已处于期望状态、或本次投票未跨越计票边界）；
- `BK_ERR_PARAM`：voter 句柄为 NULL 或非法；
- `BK_ERR_NOT_INIT`：投票层尚未初始化（还没有任何 voter 注册过）；
- 当投票跨越计票边界触发上下线时，透传 `bk_cpu_hp_online()` / `bk_cpu_hp_offline()` 的返回码。

投票层使用示例：

```
cpu_hp_voter_handle_t v = bk_cpu_hp_vote_register("audio");
if (v == NULL) {
    return BK_ERR_NO_MEM;
}

bk_cpu_hp_vote_online(v);    /* 需要算力：拉起从核 CPU1 */
/* ... 重负载业务 ... */
bk_cpu_hp_vote_offline(v);   /* 释放：无其他 voter 持票时自动放下从核 */

bk_cpu_hp_vote_unregister(v);
```

备注

`bk_cpu_hp_vote_register()` / `bk_cpu_hp_vote_unregister()` 内部同样会驱动
hotplug（注销等价于先投 offline），因此与 `bk_cpu_hp_offline/online()` 一样
**必须在任务上下文中调用**。`bk_cpu_hp_vote_find()` 可按 name 查找已注册的
voter，但仅在 `CONFIG_CPU_HP_VOTE_FIND` 开启时提供；`bk_cpu_hp_vote_dump()`
仅在 `CONFIG_CPU_HP_VOTE_DUMP` 开启时提供。关闭 `CONFIG_CPU_HP_VOTE_NAME`
后 `register` 的 `name` 参数会被忽略（仍不可为 NULL）。
