# AP侧配置GPIO和RTC唤醒说明

本章节基于AP侧 `pm_ap_demo.c` 示例，说明应用在AP侧如何配置GPIO和RTC作为唤醒源，并触发系统进入睡眠模式或深度睡眠。


## 整体流程

AP侧示例通过消息队列处理低功耗请求：

> - `PM_DEMO_ENTER_LOW_VOLTAGE`：配置睡眠模式唤醒源，投APP睡眠票，并关闭AP。
> - `PM_DEMO_ENTER_DEEP_SLEEP`：配置深度睡眠唤醒源，设置AP侧睡眠模式，并关闭AP。
> - `PM_DEMO_CALLBACK_MSG_HANDLE`：处理睡眠模式唤醒回调，恢复默认睡眠模式并取消APP睡眠票。


## RTC唤醒配置

AP侧RTC唤醒使用 `pm_ap_rtc_info_t` 配置唤醒周期、唤醒次数和回调函数。

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


## GPIO唤醒配置

AP侧GPIO唤醒需要在 `CONFIG_GPIO_WAKEUP_SUPPORT` 使能时使用。

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


## 进入睡眠模式

AP侧配置RTC/GPIO唤醒源后，睡眠模式流程还需要投APP睡眠票，并投AP关闭票：


```
bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP, 0x1, 0x0);
bk_pm_module_vote_boot_ap_ctrl(PM_BOOT_AP_MODULE_NAME_APP, PM_POWER_MODULE_STATE_OFF);

```

睡眠模式唤醒后，示例在 `PM_DEMO_CALLBACK_MSG_HANDLE` 中恢复默认模式并取消APP睡眠票：


```
bk_pm_ap_sleep_mode_set(PM_MODE_DEFAULT);
bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP, 0x0, 0x0);

```


## 进入深度睡眠

AP侧配置RTC/GPIO唤醒源后，深度睡眠流程调用 `bk_pm_ap_sleep_mode_set()` 设置深度睡眠模式，并投AP关闭票：


```
bk_pm_ap_sleep_mode_set(PM_MODE_DEEP_SLEEP);
bk_pm_module_vote_boot_ap_ctrl(PM_BOOT_AP_MODULE_NAME_APP, PM_POWER_MODULE_STATE_OFF);

```


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

AP侧配置唤醒源后，需要确保AP关闭票和睡眠票与业务流程匹配。进入睡眠模式时，唤醒后应取消APP睡眠票；进入深度睡眠时，系统唤醒后会复位，业务需要按启动流程重新初始化。

