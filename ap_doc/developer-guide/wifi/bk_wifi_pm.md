---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/wifi/bk_wifi_pm.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="wi-fi-sta"></a>

# Wi-Fi STA 低功耗

Armino 支持 Wi-Fi6 TWT 及协议定义的传统省电模式，并针对低性能、高省电场景做了优化。BK7259 SMP 上，客户应用在 **AP 核** 通过 `bk_wifi_sta_pm_enable()` / `bk_wifi_sta_pm_disable()`、`bk_wifi_send_listen_interval_req()` 等 API 控制 STA 休眠；Listen Interval 等驱动级 Kconfig 通常在 **CP** defconfig 中配置。

<a id="wi-fi"></a>

## **Wi-Fi 省电基本原理**

Armino Wi-Fi 省电的基本原理是通过减少监听时间来降低耗能。当 station 通知 AP 进入休眠模式后，AP 会缓存该 station 的包，并在接下来的 Beacon 帧中携带 TIM IE：bitmap 指示 AP 缓存的单播包，DTIM 指示缓存广播包。对 station 来说，TIM 非必听，DTIM 为必听，因此 station 可以选择只在每个 DTIM 帧前醒来监听。

<a id="id4"></a>
![../../_images/station_ps_mode.png](../../../../_assets/01ee660c83fd17ae3573-station_ps_mode.png)


station 省电模式示意图

除减少监听外，整体功耗还受 CPU 主频、唤醒工作时长、丢失 Beacon 补偿等影响。用户可配置流量监控 TD 时间，直接影响唤醒工作时长。

<a id="id5"></a>
![../../_images/station_wakeup_current.png](../../../../_assets/ec513d0860c2c44af146-station_wakeup_current.png)


station 唤醒电流示例

<a id="dtim"></a>

## **传统省电（基于 DTIM）**

<a id="id6"></a>
![../../_images/Based_on_DTIM.png](../../../../_assets/280e7f0c7be91593ae55-Based_on_DTIM.png)


基于 DTIM 的省电流程

- STA 关联 AP 后协商 Beacon Period、DTIM Period、Listen Interval
- 无业务时 STA 通知 AP 进入 sleep，关闭 RF/MAC/PHY 相关电源域后在 DTIM 周期唤醒，接收广播/单播
- 关联 AP 后 station 定期在活动与睡眠状态间切换，modem-sleep 下可与 AP 保持连接
- 与 BLE 共存时 RF 可能无法完全关闭

<a id="listen-interval"></a>

## **Listen Interval 递进省电**

<a id="id7"></a>
![../../_images/Based_on_Listen_Interval.png](../../../../_assets/7da6abe6d233b44c7d0d-Based_on_Listen_Interval.png)


基于 Listen Interval 的省电

默认节能模式下，每个 DTIM 间隔 station 唤醒接收 beacon。递进模式下，station 按监听间隔（可长于 AP 的 DTIM 周期）唤醒；间隔越长越省电，但广播包更容易丢失。

初始化 Wi-Fi 驱动后 modem-sleep 处于默认节能模式。调用 [`bk_wifi_send_listen_interval_req()`](../../api-reference/wifi/bk_wifi.md#_CPPv432bk_wifi_send_listen_interval_req7uint8_t "bk_wifi_send_listen_interval_req") 可配置递进节能模式。**递进模式可能丢失广播包，请根据应用自行设置。**

驱动级 Kconfig（通常在 CP defconfig 中，由平台集成）:

```
CONFIG_MM_PS_SET_LISTEN_INTERVAL_VALUE=30
CONFIG_MM_PS_BASED_ON_LISTEN_INTERVAL=y
```

备注

AP 在 DTIM 间隔发送广播帧；启用「仅按 Listen Interval 唤醒」时 station 可能错过广播包。Listen Interval 过大时 AP 可能缓存过多单播包导致丢包。该机制仅适合对性能要求低、对省电要求高的应用。

<a id="modem-sleep"></a>

## **Modem Sleep**

Modem sleep 基于 DTIM 机制，周期性醒来处理 Wi-Fi 业务并在间隔间睡眠；Wi-Fi 业务结束后自动进入休眠，关闭 PHY/RF，其余模块保持上电。

- 已关联路由器：默认按 listen interval 醒来，系统主动发包也可唤醒
- 未关联路由器：主动发起业务即可从 modem sleep 唤醒

<a id="id8"></a>
![../../_images/modem_sleep_procedure.png](../../../../_assets/c452bc0c770a1507998a-modem_sleep_procedure.png)


modem sleep 流程

<a id="id9"></a>
![../../_images/modem_sleep_current.png](../../../../_assets/cf2f380fb9513da830d7-modem_sleep_current.png)


modem sleep 电流设想

<a id="sta"></a>

## **关闭 / 开启 STA 休眠**

默认开启 STA 休眠（modem-sleep）。应用可调用：

- [`bk_wifi_sta_pm_disable()`](../../api-reference/wifi/bk_wifi.md#_CPPv422bk_wifi_sta_pm_disablev "bk_wifi_sta_pm_disable") — 关闭 modem-sleep，降低延迟、增加功耗
- [`bk_wifi_sta_pm_enable()`](../../api-reference/wifi/bk_wifi.md#_CPPv421bk_wifi_sta_pm_enablev "bk_wifi_sta_pm_enable") — 重新开启

注意：

- AP\+STA 共存时即使开启也可能无法真正进入低功耗
- STA\+BLE 共存时通常需保持 sleep，以协调 RF 切换，否则可能丢包
- 对功耗不敏感的应用（如部分家电）可关闭 sleep 以获得最佳性能

<a id="softap-sta"></a>

## **SoftAP 与 STA 睡眠**

AP 会缓存所连 station 的数据；按协议 AP 本身不进入节能模式，仅处理对端休眠。上述 STA 低功耗说明均指 station 模式；AP 模式下暂不支持与 station 相同的低功耗模式。

<a id="id1"></a>

## **收发数据下的睡眠管理**

station 休眠期间可随时被唤醒主动发数据，并在 beacon 接收点被动收包。[`bk_wifi_set_td_active_percent()`](../../api-reference/wifi/bk_wifi.md#_CPPv429bk_wifi_set_td_active_percent7uint8_t "bk_wifi_set_td_active_percent") 配置（未配置则用默认值）：

- `interval` — 本轮收/发包工作时长
- `max_pck_cnt` — 门限：低于该值则本轮结束后进入 modem-sleep；达到或超过则再保持一个 `interval` 周期后继续比较

<a id="id2"></a>

## **功耗状态与调试**

判断 Wi-Fi 是否进入节能：

- 外接电流测量设备
- CLI ``` get ps status``（示例返回 ``ps status: sleep/active ```）

若无法进入节能，执行 `ps debug 1` 观察 Log：

| **Log** | **描述** |
| --- | --- |
| ps function is close | ps 功能关闭（命令关闭或 SOFTAP/Monitor 模式） |
| connect instrument | 与仪表连接 |
| ATE mode | ATE 模式 |
| Video Transfer | 图传未关闭 |
| KE EVT in process | 有 KE 消息 |
| MSG in process | 有 msg 消息 |
| TXL in process | 有未完成的 TX |
| TIMER in process | 即将有 HW 定时器超时 |
| HW INTERRUPT | 中断处理中 |
| PS VOTE still on | Wi-Fi 业务还未清票（PSVOTE/VIFVOTE） |

调试结束后输入 `ps debug 0` 关闭。

<a id="twt"></a>

## **TWT**

Wi-Fi6 TWT 省电模式：待补充。

<a id="id3"></a>

## **示例工程**

详见 [sta\_example](../../examples/projects/wifi/sta_example.md)；驱动级 PM 参数见 CP 文档；系统级低电压 sleep 见 [AP侧低功耗配置说明](../power_save.md)。
