# 设置GPIO作为唤醒源-系统进入深度、超深度睡眠以及睡眠模式配置说明


## GPIO-深度睡眠调用函数和调用顺序说明


- 1. bk_gpio_register_wakeup_source(GPIO_18,GPIO_INT_TYPE_FALLING_EDGE);
  1. 设置唤醒的GPIO id : GPIO18
  2. 设置GPIO唤醒模式:


```
GPIO_INT_TYPE_FALLING_EDGE: 下降沿唤醒;
GPIO_INT_TYPE_RISING_EDGE: 上升沿唤醒;
GPIO_INT_TYPE_LOW_LEVEL: 低电平唤醒;
GPIO_INT_TYPE_HIGH_LEVEL: 高电平唤醒;

```


- 2. bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_GPIO, NULL);
  > 向系统中设置GPIO方式作为唤醒源；

- 3. bk_pm_sleep_mode_set(PM_MODE_DEEP_SLEEP);
  > 设置睡眠模式，进入深度睡眠
  >
  > 系统从深度睡眠唤醒后，可以通过调用 `bk_gpio_get_wakeup_gpio_id()` 获取本次唤醒的GPIO ID。


## GPIO-超深度睡眠调用函数和调用顺序说明

待补充


## GPIO-睡眠模式调用函数和调用顺序说明


- 1. bk_gpio_register_wakeup_source(GPIO_18,GPIO_INT_TYPE_FALLING_EDGE);

  a.设置唤醒的GPIO id:GPIO18;

  b.设置GPIO唤醒模式:

  > GPIO_INT_TYPE_FALLING_EDGE: 下降沿唤醒;
  >
  > GPIO_INT_TYPE_RISING_EDGE: 上升沿唤醒;
  >
  > GPIO_INT_TYPE_LOW_LEVEL: 低电平唤醒;
  >
  > GPIO_INT_TYPE_HIGH_LEVEL: 高电平唤醒;

- 2. bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_GPIO, NULL);
  > 向系统中设置GPIO方式作为唤醒源；

- 3. bk_pm_sleep_mode_set(PM_MODE_LOW_VOLTAGE);
  > 设置睡眠模式，进入睡眠模式。(备注：当前系统默认设置为睡眠模式，只需要满足投的票，就可以进入睡眠模式)

- 4. bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP,0x1,0x0);
  > 向系统中投应用程序的票。

备注


- 1. `bk_gpio_register_wakeup_source()` 支持动态注册GPIO唤醒源，默认最大数量由 `CONFIG_GPIO_DYNAMIC_WAKEUP_SOURCE_MAX_CNT` 决定，当前BK7259默认值为4。注册数量超过上限时会返回 `BK_ERR_GPIO_WAKESOURCE_OVER_MAX_CNT`，可以先调用 `bk_gpio_unregister_wakeup_source()` 取消不再使用的唤醒源。

- 2. 超深度睡眠使用 `bk_gpio_ana_register_wakeup_source()`，当前默认只支持2个模拟GPIO唤醒源，并且只用于超深度睡眠。

- 3. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入睡眠模式和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。

- 4. 当前代码不会因为BT或WIFI未上电而自动替应用投对应的sleep票；需要进入睡眠模式时，应以 `pm_debug 8` 输出的 `not_sleeped` 字段确认仍未满足的票。

- 5. 追求最优功耗时，当系统开启音频，视频，LCD，CPU1，CPU2后，进入睡眠模式前需要把音频，视频，LCD，CPU1,CPU2先关闭，再进入睡眠。

