---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_lowpower_architecture.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 低功耗整体架构

BK7259低功耗采用CP主控、AP从属的主从架构。CP负责低功耗状态机、睡眠投票、唤醒源、电源域和AP上下电控制；AP主要承载音频、视频、LCD、多媒体等高算力业务，只有业务需要时才被唤醒。

系统开机默认启动CP和AP。进入sleep mode或deepsleep前，应用需要先关闭不需要的业务模块，CP根据投票状态关闭AP、配置唤醒源并控制系统进入低功耗。Wi-Fi、BLE保活场景下，周期性唤醒只需要CP参与，AP保持关闭；当有需要AP处理的业务时，再由CP唤醒AP。

<a id="id2"></a>

## 整体框图

```
+---------------------------------------------------------------+
|                         Application                           |
|  业务策略 / 关闭业务模块 / 配置唤醒源 / 投睡眠票 / 请求AP唤醒 |
+-------------------------------+-------------------------------+
                                |
                                v
+---------------------------------------------------------------+
|                              CP                               |
|  低功耗主控：PM Core / Sleep Vote / Wakeup / Power / Clock    |
|                                                               |
|  +----------------+  +----------------+  +----------------+   |
|  | Sleep Manager  |  | Wakeup Source  |  | Power Domain   |   |
|  | sleep/deepsleep|  | GPIO/RTC/Wi-Fi |  | AP/外设上下电  |   |
|  | 状态机与投票   |  | BLE/Touch      |  |                |   |
|  +----------------+  +----------------+  +----------------+   |
|                                                               |
|  +----------------+  +----------------+  +----------------+   |
|  | Clock Manager  |  | AP Ctrl        |  | Debug/Trace    |   |
|  | 32K/模块时钟   |  | pm_boot_ap     |  | pm_debug       |   |
|  +----------------+  +----------------+  +----------------+   |
+-------------------------------+-------------------------------+
                                |
             按业务需要启动/关闭AP |
                                v
+---------------------------------------------------------------+
|                              AP                               |
|       音频 / 视频 / LCD / 多媒体 / 需要高算力的业务处理       |
+---------------------------------------------------------------+
                                |
                                v
+---------------------------------------------------------------+
|                     AON / 32K / Wakeup Logic                  |
|        低功耗保持域，负责RTC、GPIO、Wi-Fi/BLE周期唤醒等       |
+---------------------------------------------------------------+
```

<a id="id3"></a>

## 模块组成

| 模块 | 作用 |
| --- | --- |
| PM Core | 维护低功耗状态机，协调sleep mode和deepsleep流程。 |
| Sleep Vote | 管理各模块是否允许进入低功耗，APP票由业务侧控制。 |
| Wakeup Source | 管理GPIO、RTC、Touch、Wi-Fi、BLE等唤醒源。 |
| Power Domain | 控制AP、外设和电源域上下电。 |
| Clock Manager | 管理32K时钟源、模块时钟和低功耗时钟切换。 |
| AP Ctrl | 通过 `pm_boot_ap` 或接口按需启动、关闭AP。 |
| Debug/Trace | 通过 `pm_debug` 等命令查看投票、唤醒和电源状态。 |

<a id="id4"></a>

## 开机与低功耗控制关系

> | 场景 | CP状态 | AP状态 |
> | --- | --- | --- |
> | 开机默认 | 启动，负责系统控制 | 默认启动 |
> | sleep mode | 进入睡眠，保留唤醒逻辑 | 进入前关闭 |
> | deepsleep | 进入深睡，唤醒后复位启动 | 进入前关闭 |
> | Wi-Fi/BLE保活唤醒 | 周期性唤醒并处理保活事件 | 默认保持关闭 |
> | 需要AP侧业务 | 投票启动AP并协调业务 | 被CP唤醒，业务完成后再关闭 |

<a id="id5"></a>

## 典型流程

<a id="sleep-modedeepsleep"></a>

### 进入sleep mode或deepsleep

1. 应用完成当前业务，关闭不需要的音频、视频、LCD、多媒体和外设模块。
2. 如不需要AP参与后续保活或唤醒处理，调用 `pm_boot_ap 9 1` 或对应接口关闭AP。
3. 配置GPIO、RTC、Touch、Wi-Fi或BLE等唤醒源。
4. APP投睡眠票，满足各模块低功耗条件。
5. CP侧PM状态机进入sleep mode或deepsleep。

<a id="wi-fi-ble"></a>

### Wi-Fi/BLE保活

1. Wi-Fi或BLE连接建立后，协议栈按DTIM、listen interval、BLE连接间隔等参数配置周期唤醒。
2. 应用关闭AP和不需要的业务模块，APP投睡眠票。
3. 系统进入sleep mode，AP保持关闭。
4. 保活周期到来时，CP被唤醒并处理Wi-Fi/BLE事件。
5. 如果只是保活或少量控制消息，CP处理完成后重新进入sleep mode。
6. 如果事件需要音频、视频、LCD或多媒体能力，CP再唤醒AP处理业务。

<a id="ap"></a>

### AP按需唤醒

1. CP收到需要AP参与的事件，例如图像、音频、LCD显示或复杂业务处理。
2. CP调用 `bk_pm_module_vote_boot_ap_ctrl()` 或CLI命令 `pm_boot_ap` 启动AP。
3. AP完成业务后，业务模块撤销启动AP投票。
4. 所有启动AP的模块都投关闭票后，CP关闭AP，系统重新具备进入低功耗的条件。

<a id="id6"></a>

## 相关文档

> - 睡眠模式说明：[睡眠模式说明](bk_sleep_mode.md)
> - 系统状态机说明：[系统状态机说明](bk_fsm.md)
> - 如何启动和关闭AP：请参考CP侧低功耗文档中的“如何启动和关闭AP”。
> - Wi-Fi睡眠模式保活：请参考CP侧低功耗文档中的“设置WIFI睡眠模式保活说明”。
> - 低功耗问题分析：请参考CP侧低功耗文档中的“低功耗问题分析”。
