---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_bluetooth_sleep_mode.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 蓝牙睡眠模式使用说明

睡眠模式（sleep mode）是系统低功耗运行的一种模式，对应代码中的 `PM_MODE_LOW_VOLTAGE` 。在蓝牙保活场景下，若追求极低功耗，就需要让系统处于该模式。

本文介绍系统睡眠模式的设计、蓝牙在该模式下的支持范围与宏配置，并说明具体用法。关于睡眠模式的通用说明，另见 [睡眠模式说明](bk_sleep_mode.md) 。

在该模式下，CP侧始终是CPU下电、RAM保持；差异主要在AP侧的下电方式，据此分为两种方案：

> - **方案一：AP RAM 不保持**。AP的CPU与RAM同时下电，RAM内容丢失。再次上电等同于冷启动，
>   需重新初始化并区分首次/非首次启动。适用于极低功耗的纯BLE slave保活（广播/连接）与配网等场景。
> - **方案二：AP fast boot（AP RAM 保持）**。AP的CPU下电但RAM保持，再次上电通过fast boot
>   恢复执行上下文，无需重新初始化协议栈与业务。适用于需要保留较复杂运行时状态、且希望快速
>   恢复的场景（如A2DP耳机播放）。详见 [方案二：AP fast boot（AP RAM 保持）](#ap-fast-boot-ap-ram) 。

<a id="ap-ram"></a>

## 方案一：AP RAM 不保持

在该方案下，AP侧与CP侧的处理方式并不相同：

> - AP侧：CPU会下电，且RAM也会下电、**不做保持**。
> - CP侧：CPU会下电，但RAM会**保持**。

备注

由于该模式下AP下电后再次上电时，RAM内容会丢失（不保持），所以用户在开发时需要尤为关注：
AP再次启动等同于一次重新启动，所有依赖RAM的运行时状态都不会保留，需要重新初始化或从持久化存储/CP侧恢复。

<a id="id2"></a>

## 蓝牙支持范围

该方案（AP RAM 不保持）下蓝牙目前**只支持BLE slave only场景**，即 `BROADCASTER + PERIPHERAL` （广播 \+ 从机），不支持主机（Central/Observer）相关角色。

蓝牙相关宏配置如下，平台通用低功耗配置见 [睡眠模式说明](bk_sleep_mode.md) 。

CP侧：

```
CONFIG_BLUETOOTH=y
CONFIG_BLUETOOTH_BLE_SLAVE_ONLY=y
CONFIG_BLUETOOTH_SUPPORT_LPO_ROSC=y
CONFIG_BLE_LV_SUPPORT=y
CONFIG_BTDM_CONTROLLER_ONLY=n
CONFIG_BLUETOOTH_SUPPORT_AP_PWD_ALL=y
```

AP侧：

```
CONFIG_BLUETOOTH_AP=y
CONFIG_BLUETOOTH_HOST_ONLY=n
CONFIG_BLUETOOTH_SUPPORT_AP_PWD_ALL=y
```

<a id="id3"></a>

## 使用说明

下面以经典的BLE配网场景为例进行介绍。

配网场景下，板子上电后，工程用户的AP代码中会默认执行开启广播的操作。这个过程中，蓝牙相关操作主要涉及以下三个方面：

> 1. 注册BLE事件回调函数： `bk_ble_set_notice_cb` 。
> 2. 添加配网服务： `bk_ble_create_db` 。
> 3. 开启广播。

如果此时没有业务需要处理，就可以进入睡眠模式，具体流程详见 [睡眠模式说明](bk_sleep_mode.md) 。进入后，CP侧会按设定的广播间隔持续广播，AP侧则可下电以降低功耗。

<a id="cpap"></a>

### CP唤醒AP与首次启动的区分

若需要进行BLE配网，此时用手机App连接该广播。CP侧收到BLE连接事件后会**自动启动AP**。这时AP的启动流程与首次板子上电时的AP启动流程完全一样，工程用户代码中BLE的那些操作（添加服务、开启广播）同样会被执行。

由于前面已经添加过服务、开过广播，再执行一遍会导致**CP侧蓝牙状态错乱**。因此需要针对“非首次AP正常启动”（即CP唤醒AP）的场景做特殊区分：只有首次启动才添加服务、开启广播，而 `bk_ble_set_notice_cb` 无论是否首次都必须执行。

可通过 `bk_pm_ap_first_boot_get()` 判断是否为首次启动：

```
/* 无论是否首次启动，都必须注册 BLE 事件回调 */
bk_ble_set_notice_cb(ble_notice_cb);

if (bk_pm_ap_first_boot_get())
{
    /* 仅首次启动执行：避免 CP 唤醒 AP 后重复操作导致状态错乱 */
    bk_ble_create_db(...);   /* 添加配网服务 */
    start_adv();             /* 开启广播 */
}
```

备注

`bk_ble_set_notice_cb` 一定要注册，且不能放在 `bk_pm_ap_first_boot_get()` 的首次分支里。
因为CP收到连接事件、启动AP后，会把连接事件上报到此回调；如果没有注册此回调，整个流程会卡住。

两种AP启动流程的对比如下。

正常AP启动（板子首次上电）：

```
+----------------------------------+
|          板子首次上电            |
+----------------+-----------------+
                 |
                 v
+----------------------------------+
|   AP 启动（first_boot = true）   |
+----------------+-----------------+
                 |
                 v
+----------------------------------+
|  bk_ble_set_notice_cb 注册回调   |
+----------------+-----------------+
                 |
                 v
+----------------------------------+
|  first_boot == true              |
|   -> bk_ble_create_db 添加服务   |
|   -> start_adv 开启广播          |
+----------------+-----------------+
                 |
                 v
+----------------------------------+
|  无业务 -> 进入睡眠模式          |
|  AP 下电，CP 按间隔广播          |
+----------------------------------+
```

CP唤醒启动AP（手机连接或应用数据事件）：

```
+----------------------------------+
|  CP 广播中/维持连接（AP 已下电） |
+----------------+-----------------+
                 |
                 v
+----------------------------------+
|  手机连接 或 应用数据到达        |
|  CP 收到 BLE 事件 -> 自动启动 AP |
+----------------+-----------------+
                 |
                 v
+----------------------------------+
|  AP 启动（first_boot = false）   |
|  注意：RAM 已丢失，等同重启      |
+----------------+-----------------+
                 |
                 v
+----------------------------------+
|  bk_ble_set_notice_cb 注册回调   |
|  （必须，否则事件上报会卡住）    |
+----------------+-----------------+
                 |
                 v
+----------------------------------+
|  first_boot == false             |
|   -> 跳过 create_db / start_adv  |
+----------------+-----------------+
                 |
                 v
+----------------------------------+
|  CP 上报事件到 notice_cb         |
|  -> AP 业务处理 -> 再次进睡眠    |
+----------------------------------+
```

<a id="id4"></a>

### 配网与再次进入睡眠

BLE连接建立后，即可正常进行常规的配网流程。配网结束后，如果需要BLE保持此连接进行保活，就可以再次进入睡眠模式（AP再次下电，CP维持连接）。

之后如果手机端有应用数据过来，CP侧会**自动唤醒AP**，并将数据/事件上报到已注册的事件回调函数中，由AP侧业务处理；处理完成后可再次进入睡眠模式。

<a id="ap-fast-boot-ap-ram"></a>

## 方案二：AP fast boot（AP RAM 保持）

前述方案一中，AP再次上电等同于冷启动，所有依赖RAM的运行时状态都会丢失，因此需要区分
首次/非首次启动并重新初始化。对于需要保留较复杂运行时状态、且希望快速恢复的业务
（例如A2DP耳机播放场景），可改用 **AP fast boot** 方案：AP下电但其RAM **保持**，
再次上电时通过fast boot恢复执行上下文，**无需重新初始化协议栈与业务**。

<a id="id5"></a>

### 与方案一的差异

> - AP侧：CPU下电，RAM **保持**；恢复时走fast boot，不重跑 `main` 的协议栈/业务初始化。
> - CP侧：与方案一一致，CPU下电、RAM保持，负责在有HCI需要上送时唤醒AP。
> - 由于RAM保持，唤醒后 **不需要** 重新执行 `bk_ble_set_notice_cb` 、
>   `bk_ble_create_db` 、开启广播等操作，也 **不需要** `bk_pm_ap_first_boot_get()`
>   区分首次启动——运行时状态在RAM中原样保留。
> - mailbox / BT IPC通道在AP下电期间由CP维护，AP恢复后 **无需重挂**；协议栈通过注册的
>   PM退出低压/恢复回调完成transport恢复。

<a id="id6"></a>

### 蓝牙相关配置

双模配置参见 `projects/bluetooth/headset_lp` ，此处仅列蓝牙相关关键项，平台通用低功耗配置见 [睡眠模式说明](bk_sleep_mode.md) ，AP fast boot 相关配置见 [AP快速启动配置说明](bk_ap_fast_boot_config.md) 。

CP侧：

```
CONFIG_BLUETOOTH=y
CONFIG_BT=y
CONFIG_BTDM_CONTROLLER_ONLY=y
CONFIG_BLUETOOTH_SUPPORT_LPO_ROSC=y
CONFIG_BLE_LV_SUPPORT=y
CONFIG_BLUETOOTH_SUPPORT_AP_PWD_RETENTION=y
```

AP侧：

```
CONFIG_BLUETOOTH_AP=y
CONFIG_BT=y
CONFIG_BLUETOOTH_SUPPORT_AP_PWD_RETENTION=y
```

备注

`CONFIG_BLUETOOTH_SUPPORT_AP_PWD_RETENTION` （方案二）与 `CONFIG_BLUETOOTH_SUPPORT_AP_PWD_ALL`
（方案一）互斥：前者AP RAM保持（fast boot），后者AP RAM丢失（冷启动）。二者不可同时开启。

<a id="id7"></a>

### 使用说明

因运行时状态保留，AP侧业务代码 **无需** 为“CP唤醒AP”做首次/非首次区分：AP恢复后从
下电前的上下文继续执行，CP将HCI事件/数据上报后由AP侧业务直接处理，处理完成后可再次
进入睡眠。
