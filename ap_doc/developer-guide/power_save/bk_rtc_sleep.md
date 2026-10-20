---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# 设置RTC作为唤醒源-系统进入深度、超深度睡眠以及睡眠模式配置说明



## RTC-深度睡眠调用函数和调用顺序说明


- 1. 配置RTC唤醒源的参数
  > alarm_info_t low_voltage_alarm = {
  >
  > > “low_vol”,
  > >
  > > 3000*RTC_TICKS_PER_1MS,//设置为3000ms后唤醒，唤醒时间可以根据需求更改
  > >
  > > 1,
  > >
  > > cli_pm_rtc_callback,
  > >
  > > NULL
  > >
  > > };
  >
  > bk_alarm_register(AON_RTC_ID_1, &low_voltage_alarm);

- 2. bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_RTC, NULL);
  > 向系统中设置RTC方式作为唤醒源

- 3. bk_pm_sleep_mode_set(PM_MODE_DEEP_SLEEP);
  > 设置睡眠模式，进入深度睡眠


## RTC-超深度睡眠调用函数和调用顺序说明


- 1. bk_rtc_ana_register_wakeup_source(0x5)
  > 设置超深度睡眠RTC模拟唤醒时间。该接口只用于超深度睡眠，支持的时间设置如下：


```
0x0:  1/32 s
0x1:  1/16 s
0x2:  1/8  s
\.\.\.
0x5:  1    s
0x6:  2    s
0x7:  4    s
\.\.\.
0x0d: 256  s
0x0e: 512  s
0x0f: 1024 s

```


- 2. bk_pm_sleep_mode_set(PM_MODE_SUPER_DEEP_SLEEP);
  > 设置睡眠模式，进入超深度睡眠


## RTC-睡眠模式调用函数和调用顺序说明


- 1. 配置RTC唤醒源的参数;
  > alarm_info_t low_voltage_alarm = {
  >
  > > “low_vol”,
  > >
  > > 3000*RTC_TICKS_PER_1MS,//设置为3000ms后唤醒，唤醒时间可以根据需求更改
  > >
  > > 1,
  > >
  > > cli_pm_rtc_callback,
  > >
  > > NULL
  > >
  > > };
  >
  > bk_alarm_register(AON_RTC_ID_1, &low_voltage_alarm);

- 2. bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_RTC, NULL);
  > 向系统中设置RTC方式作为唤醒源

- 3. bk_pm_sleep_mode_set(PM_MODE_LOW_VOLTAGE);
  > 设置睡眠模式，进入睡眠模式
  > (备注：当前系统默认设置为睡眠模式，只需要满足投的票，就可以进入睡眠模式)

- 4. bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP,0x1,0x0);
  > 向系统中投应用程序的票

备注


- 1. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入睡眠模式和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。

- 2. 当前代码不会因为BT或WIFI未上电而自动替应用投对应的sleep票；需要进入睡眠模式时，应以 `pm_debug 8` 输出的 `not_sleeped` 字段确认仍未满足的票。

- 3. 追求最优功耗时，当系统开启音频，视频，LCD，CPU1，CPU2后，进入睡眠模式前需要把音频，视频，LCD，CPU1,CPU2先关闭，再进入睡眠。

- 4. 超深度睡眠的RTC模拟唤醒由 `CONFIG_RTC_ANA_WAKEUP_SUPPORT` 控制，当前BK7259默认使能；`bk_rtc_ana_register_wakeup_source()` 的 `period` 是0~15的枚举索引，不是毫秒值。深度睡眠和睡眠模式的AON RTC闹钟不受该表限制。
