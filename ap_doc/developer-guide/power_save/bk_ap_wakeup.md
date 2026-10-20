---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_ap_wakeup.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="apgpiortc"></a>

# AP侧配置GPIO和RTC唤醒说明

BK7259低功耗主体在CP侧，AP侧不负责维护完整低功耗状态机。AP侧应用需要进入低功耗时，主要完成业务收尾、GPIO/RTC唤醒配置、APP睡眠投票和AP关闭投票；随后由CP侧完成真正的低功耗进入、唤醒源保持和AP上下电控制。

本章节基于AP侧示例代码 `ap/middleware/driver/pwr_clk/pm_ap_demo.c`，说明应用在AP侧如何配置GPIO和RTC作为唤醒源，并触发系统进入睡眠模式或深度睡眠。CP侧完整低功耗说明请参考：

> - `cp/docs/bk7259/zh_CN/developer-guide/power_save/index.rst`

<a id="id1"></a>

## 整体流程

AP侧示例通过消息队列处理低功耗请求：

> - `PM_DEMO_ENTER_LOW_VOLTAGE`：配置睡眠模式RTC/GPIO唤醒源，投APP睡眠票，并投AP关闭票。
> - `PM_DEMO_ENTER_DEEP_SLEEP`：配置深度睡眠RTC/GPIO唤醒源，设置AP侧深睡模式，并投AP关闭票。
> - `PM_DEMO_CALLBACK_MSG_HANDLE`：处理睡眠模式唤醒回调，恢复默认睡眠模式并取消APP睡眠票。

AP侧demo消息参数含义如下：

> - `param1`：RTC唤醒时间，单位为ms；传入0时默认50s。
> - `param2`：RTC唤醒次数；传入0时默认1次，`0xffffffff` 表示永久周期唤醒。
> - `param3`：GPIO唤醒源ID，仅在 `CONFIG_GPIO_WAKEUP_SUPPORT` 使能时使用。
> - `param4`：GPIO唤醒触发类型，类型为 `gpio_int_type_t`。

<a id="rtc"></a>

## RTC唤醒配置

AP侧RTC唤醒使用 `pm_ap_rtc_info_t` 配置唤醒周期、唤醒次数和回调函数。AP侧调用 `bk_pm_ap_rtc_regsiter_wakeup()` 后，唤醒配置会交由CP侧低功耗框架处理。

关键参数如下：

> - `period_tick`：RTC唤醒周期，单位为ms。示例中如果传入0，则默认使用 `50*1000`，即50s。
> - `period_cnt`：RTC唤醒次数。`0xffffffff` 表示永久周期唤醒；其他值表示唤醒次数。示例中如果传入0，则默认使用1次。
> - `callback`：RTC唤醒回调。示例中使用 `pm_demo_rtc_sleep_wakeup_callback`。

睡眠模式下注册RTC唤醒：

```
pm_ap_rtc_info_t low_power_info = {0};

low_power_info.period_tick = rtc_sleep_time;
low_power_info.period_cnt  = rtc_sleep_repeat_count;
low_power_info.callback    = pm_demo_rtc_sleep_wakeup_callback;
low_power_info.param_p     = NULL;

bk_pm_ap_rtc_regsiter_wakeup(PM_MODE_LOW_VOLTAGE, &low_power_info);
```

深度睡眠下注册RTC唤醒：

```
bk_pm_ap_rtc_regsiter_wakeup(PM_MODE_DEEP_SLEEP, &low_power_info);
```

<a id="gpio"></a>

## GPIO唤醒配置

AP侧GPIO唤醒需要在 `CONFIG_GPIO_WAKEUP_SUPPORT` 使能时使用。示例采用统一接口配置GPIO唤醒：AP在线时注册GPIO ISR，AP关闭后GPIO唤醒事件由CP侧保持并在唤醒AP后回放给AP侧回调处理。

示例中GPIO唤醒配置包含两步：

> - 注册GPIO中断回调 `bk_gpio_register_isr()`。
> - 通过 `bk_gpio_set_wakeup()` 配置GPIO唤醒源和触发类型。

```
bk_gpio_register_isr(gpio_id, pm_demo_gpio_callback);
bk_gpio_set_wakeup(gpio_id, (gpio_int_type_t)gpio_wakeup_int_type, true);
```

其中：

> - `gpio_id`：用作唤醒源的GPIO ID。
> - `gpio_wakeup_int_type`：GPIO唤醒触发类型，类型为 `gpio_int_type_t`，可使用高/低电平或上升/下降沿等触发方式。
> - `pm_demo_gpio_callback`：GPIO唤醒回调。示例中回调会把 `PM_WAKEUP_SOURCE_INT_GPIO` 和唤醒GPIO ID通过消息队列发送给AP侧demo线程。

<a id="id2"></a>

## 进入睡眠模式

AP侧配置RTC/GPIO唤醒源后，睡眠模式流程还需要投APP睡眠票，并投AP关闭票。AP关闭后，后续低功耗进入由CP侧在满足各模块投票后完成：

```
bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP, 0x1, 0x0);
bk_pm_module_vote_boot_ap_ctrl(PM_BOOT_AP_MODULE_NAME_APP, PM_POWER_MODULE_STATE_OFF);
```

睡眠模式唤醒后，示例在 `PM_DEMO_CALLBACK_MSG_HANDLE` 中恢复默认模式并取消APP睡眠票：

```
bk_pm_ap_sleep_mode_set(PM_MODE_DEFAULT);
bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP, 0x0, 0x0);
```

<a id="id3"></a>

## 进入深度睡眠

AP侧配置RTC/GPIO唤醒源后，深度睡眠流程调用 `bk_pm_ap_sleep_mode_set()` 设置深度睡眠模式，并投AP关闭票。深度睡眠唤醒后系统会复位，业务需要按启动流程重新初始化：

```
bk_pm_ap_sleep_mode_set(PM_MODE_DEEP_SLEEP);
bk_pm_module_vote_boot_ap_ctrl(PM_BOOT_AP_MODULE_NAME_APP, PM_POWER_MODULE_STATE_OFF);
```

<a id="id4"></a>

## 唤醒回调说明

RTC唤醒回调 `pm_demo_rtc_sleep_wakeup_callback` 会发送以下信息给demo线程：

> - `param1 = PM_MODE_LOW_VOLTAGE`
> - `param2 = PM_WAKEUP_SOURCE_INT_RTC`
> - `param3 = 0`

GPIO唤醒回调 `pm_demo_gpio_callback` 会发送以下信息给demo线程：

> - `param1 = PM_MODE_LOW_VOLTAGE`
> - `param2 = PM_WAKEUP_SOURCE_INT_GPIO`
> - `param3 = gpio_id`

备注

AP侧配置唤醒源前，应先关闭不需要的音频、视频、LCD、多媒体和外设业务，避免AP侧模块继续持有启动AP投票或阻止系统进入低功耗。进入睡眠模式时，唤醒后应取消APP睡眠票；进入深度睡眠时，系统唤醒后会复位，业务需要按启动流程重新初始化。
