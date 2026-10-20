---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/cpu_hotplug/bk_cpu_hotplug_test.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cpu-hotplug-ap"></a>

# CPU Hotplug 测试方法（AP）

本文档逐条说明 AP CPU Hotplug 提供的 CLI 测试命令、用法和预期输出。所有命令都是
固件内已实现的命令，不依赖任何额外的测试工程。AP 从核为 CPU3，命令通过 `ap_cmd`
转发到 AP 子系统。

<a id="id1"></a>

## 1 测试环境

- BK7259 开发板 \+ 串口工具；AP 通过 `ap_cmd` 发命令；
- 固件已使能 `CONFIG_SOC_SMP` 和 `CONFIG_CPU_HOTPLUG`，并已烧录；
- `cpu vote` 系列命令需固件使能 `CONFIG_CPU_HP_VOTE` （AP 默认开启）；
- `cpu gov` 系列命令需固件使能 `CONFIG_CPU_HP_GOVERNOR` （AP 默认关闭，需手动打开）。

警告

Voter 不要和其他命令业务逻辑混合测试。Voter 和 Governor 二选一，不要同时使能。
非 Governor 测试时，请关闭 Governor `cpu gov off`。

<a id="id2"></a>

## 2 命令总览

完整命令列表（不带参数发送 `ap_cmd cpu` 也会打印该帮助）:

```
ap_cmd cpu list
ap_cmd cpu state
ap_cmd cpu offline 3 # 在开启投票层时，会直接绕开投票层计票，直接尝试下线从核，请谨慎使用
ap_cmd cpu online 3  # 在开启投票层时，会直接绕开投票层计票，直接尝试上线从核，请谨慎使用
ap_cmd cpu irq-affinity
ap_cmd cpu task-affinity
ap_cmd cpu stress 3 <loops>
ap_cmd cpu busy-test
ap_cmd cpu gov on|off|status        # 需 CONFIG_CPU_HP_GOVERNOR
ap_cmd cpu gov stress <cycles>      # 需 CONFIG_CPU_HP_GOVERNOR
ap_cmd cpu vote reg|unreg|on|off <name>   # 需 CONFIG_CPU_HP_VOTE 且开启 CONFIG_CPU_HP_VOTE_FIND（依赖 NAME 与 DUMP）
ap_cmd cpu vote status              # 需 CONFIG_CPU_HP_VOTE
ap_cmd cpu vote test                # 需 CONFIG_CPU_HP_VOTE
```

<a id="cpu-list-cpu-state"></a>

## 3 cpu list / cpu state

打印 AP 两个 CPU 的状态（`list` 与 `state` 等价）:

```
ap_cmd cpu state
```

输出每个 CPU 的 `state` （状态名）、`online`、`active` 以及 domain 各 mask。
AP domain `possible=0xc`。可用它确认默认上电行为（由
`CONFIG_CPU_HOTPLUG_BOOT_OFFLINE` 决定）：AP 默认（boot-offline\=n）CPU3 为
`state=online`，domain `online=0xc`。

AP 期望输出示例（两核都 online 时）:

```
ap0:cli:I(...):cpu2: state=online  online=1 active=1 domain possible=0xc online=0xc active=0xc dying=0x0 offline=0x0
ap0:cli:I(...):cpu3: state=online  online=1 active=1 domain possible=0xc online=0xc active=0xc dying=0x0 offline=0x0
```

<a id="cpu-offline-cpu-online"></a>

## 4 cpu offline / cpu online

手动下线 / 上线从核，返回码 `ret=0` 表示成功:

```
ap_cmd cpu offline 3
ap_cmd cpu online 3
```

offline 后用 `cpu state` 复查：CPU3 变为 `state=offline online=0 active=0`，
主核 CPU2 保持 online；online 后 CPU3 恢复 `state=online online=1 active=1`。

AP 期望输出示例:

```
ap0:cli:I(...):cpu3 offline ret=0
ap0:cli:I(...):cpu3 online ret=0
```

非法目标会被拒绝（只允许 AP 从核 CPU3），CPU 状态不变、不触发 reset:

```
ap_cmd cpu offline 2     # AP 主核，拒绝
ap_cmd cpu offline 0     # 非本子系统，拒绝

ap0:cli:E(...):AP hotplug only supports cpu3, cpu2 is not allowed
```

<a id="cpu-stress"></a>

## 5 cpu stress

对从核连续做 `<loops>` 次 offline→online 循环，验证状态机稳定性:

```
ap_cmd cpu stress 3 100
ap_cmd cpu stress 3 1000
```

成功时打印循环完成；中途失败会打印失败所在的 loop 和返回码:

```
ap0:cli:I(...):cpu3 hotplug stress 100 loops done
```

期望：循环期间无 `HardFault` / `MemFault` / `BusFault` / `UsageFault`，
结束后从核状态正常。

<a id="cpu-busy-test"></a>

## 6 cpu busy-test

自检命令：自动创建一个 hard-pin 到从核的任务，再尝试 offline，验证有 pinned 任务时
offline 会返回 `BK_ERR_BUSY` （-4107），随后删除任务、从核保持 online:

```
ap_cmd cpu busy-test
```

期望输出（`PASS`）:

```
ap0:cli:I(...):cpu busy-test PASS expect=busy(-4107) actual=-4107 state=online
```

<a id="cpu-task-affinity"></a>

## 7 cpu task-affinity

查询当前是否存在 hard-pin 到从核 CPU3（SMP core1）的任务:

```
ap_cmd cpu task-affinity
```

无 pinned 任务时打印 `no`，存在时打印 `yes` （此时 offline 会返回 busy）:

```
ap0:cli:I(...):hard-pinned task on AP cpu3/core1: no
```

<a id="cpu-irq-affinity"></a>

## 8 cpu irq-affinity

dump AP 的中断路由寄存器，用于排查中断迁移:

```
ap_cmd cpu irq-affinity

ap0:cli:I(...):AP irq affinity routes: cpu2 reg10=0x.. reg11=0x.., cpu3 reg12=0x.. reg13=0x.. reg14=0x..
```

<a id="cpu-gov-status-on-off"></a>

## 9 cpu gov status / on / off

仅在使能 `CONFIG_CPU_HP_GOVERNOR` 时可用（AP 默认关闭）。

查看动态负载策略状态（是否使能、从核是否在线、各核实时负载、去抖与切换计数）:

```
ap_cmd cpu gov status

ap0:cli:I(...):cpu gov: enabled=1 cpu3_online=0 load0=.. load1=.. up_cnt=.. down_cnt=.. online=.. offline=..
```

运行时开关自动调节（`ret=0` 成功）:

```
ap_cmd cpu gov on        # cpu gov start ret=0
ap_cmd cpu gov off       # cpu gov stop ret=0
```

<a id="cpu-gov-stress"></a>

## 10 cpu gov stress

仅在使能 `CONFIG_CPU_HP_GOVERNOR` 时可用。该命令自带负载任务，自动验证 governor
能随负载上下线从核，无需手动制造负载:

```
ap_cmd cpu gov stress 100
```

执行过程：命令先创建负载任务把主核压满、等待 governor 自动 online 从核，再撤掉负载、
等待 governor 自动 offline 从核，逐周期判定 PASS/FAIL，最后汇总:

```
ap0:cli:I(...):cpu gov stress: start, cycles=100 load_tasks=..
ap0:cli:I(...):cpu gov stress: cycle 1/100 PASS (online=yes offline=yes) online_cnt=.. offline_cnt=..
...
ap0:cli:I(...):cpu gov stress: done, 100/100 cycles PASS
```

期望：所有 cycle 均 PASS，全程无 fault、无 watchdog reset。

<a id="cpu-vote-status-test"></a>

## 11 cpu vote status / test

仅在使能 `CONFIG_CPU_HP_VOTE` 时可用（AP 默认开启）。投票层按「或上线、与下线」
聚合各 voter 的诉求驱动从核 CPU3 上下线（原理见使用指南第 6 章）。

`cpu vote status` 打印当前计票与各已注册 voter 的投票状态:

```
ap_cmd cpu vote status

ap0:cli:I(...):cpu vote: online_count=.. voter_count=..
ap0:cli:I(...):cpu_hp_vote: target=cpu3 online=.. online_votes=.. voters=..
```

`cpu vote test` 为投票层自检，覆盖：NULL 句柄参数校验、注册两个 voter、
「或上线」（任一 voter 投 online 即拉起 CPU3）、计票增长、投票幂等、
「与下线」（全部释放后才放下 CPU3）、以及注销即释放（注销在线 voter 会下线 CPU3）；
随后还有一段与票池大小无关的批量用例：注册 voter 直到票池满（顺带覆盖池满返回
NULL）、逐个按 name 回查（`bk_cpu_hp_vote_find`，仅 `CONFIG_CPU_HP_VOTE_FIND`
开启时执行）、用最后一个 voter 拉起 / 放下 CPU3，再全部注销归零。
运行前需满足：当前没有已注册的 voter，且从核上没有 hard-pin 任务，否则 CPU3 会
合理地保持 online，命令会跳过并给出提示。由于 voter 注册时会按当前核态对齐初值，
自检会先把 CPU3 offline 建立确定基线，跑完再恢复到测试前状态:

```
ap_cmd cpu vote test

ap0:cli:I(...):cpu vote test: start
ap0:cli:I(...):  [PASS] A online -> cpu3 online
...
ap0:cli:I(...):cpu vote test: done, N/N checks PASS
```

也可手动逐条验证聚合语义（先 offline 建立离线基线，注册的 voter 才从 want\=0 起步）:

```
ap_cmd cpu offline 3        # 建立离线基线（无 pinned 任务时）
ap_cmd cpu vote reg a
ap_cmd cpu vote reg b
ap_cmd cpu vote on a        # 计票 0->1，从核 CPU3 上线
ap_cmd cpu vote on b        # 计票增长，从核保持 online
ap_cmd cpu vote off a       # 仍有 b 持票，从核保持 online
ap_cmd cpu vote off b       # 全部释放，从核 CPU3 下线
ap_cmd cpu vote unreg a
ap_cmd cpu vote unreg b
```

期望：`cpu vote test` 全部 check PASS，全程无 fault、无 watchdog reset。

<a id="id3"></a>

## 12 返回码与故障定位

`offline` / `online` / `busy-test` 返回失败时，按返回码定位：

- `ret=-4102` （`BK_ERR_TIMEOUT`）：从核停核 / 启核握手超时；
- `ret=-4103` （`BK_ERR_STATE`）：未在 AP 主核 CPU2 上下文调用，或状态不允许；
- `ret=-4107` （`BK_ERR_BUSY`）：从核有 hard-pin 任务 / 不可迁移中断，或正在切换中。

出现 `HardFault` / `MemFault` 时，用 `addr2line` 反解 PC/LR:

```
arm-none-eabi-addr2line -piaf -e build/bk7259/app/bk7259_ap/app.elf <pc> <lr>
```

<a id="id4"></a>

## 13 验收标准

- `cpu state` 初始状态符合 boot-offline 配置；
- `cpu offline 3` / `cpu online 3` 单次操作返回 `ret=0`，状态切换正确；
- `cpu stress 3 100` 与 `cpu stress 3 1000` 完成且无 fault；
- `cpu busy-test` 返回 PASS；
- 非法目标 CPU 被拒绝，状态不变；
- 使能 vote 时 `cpu vote test` 全部 check PASS；
- 使能 governor 时 `cpu gov stress` 全部 cycle PASS；
- 全程无 fault、无 watchdog reset、无状态机卡死。
