---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_rtc_sleep.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# 设置RTC作为唤醒源-系统进入深度、超深度睡眠以及睡眠模式配置说明

<a id="id1"></a>

## RTC-深度睡眠调用函数和调用顺序说明

- 1. 配置RTC唤醒源的参数
  > alarm\_info\_t low\_voltage\_alarm \= {
  >
  > > “low\_vol”,
  > >
  > > 3000\*RTC\_TICKS\_PER\_1MS,//设置为3000ms后唤醒，唤醒时间可以根据需求更改
  > >
  > > 1,
  > >
  > > cli\_pm\_rtc\_callback,
  > >
  > > NULL
  > >
  > > };
  >
  > bk\_alarm\_register(AON\_RTC\_ID\_1, \&low\_voltage\_alarm);
- 2. bk\_pm\_wakeup\_source\_set(PM\_WAKEUP\_SOURCE\_INT\_RTC, NULL);
  > 向系统中设置RTC方式作为唤醒源
- 3. bk\_pm\_sleep\_mode\_set(PM\_MODE\_DEEP\_SLEEP);
  > 设置睡眠模式，进入深度睡眠

<a id="id2"></a>

## RTC-超深度睡眠调用函数和调用顺序说明

- 1. bk\_rtc\_ana\_register\_wakeup\_source(0x5)
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

- 2. bk\_pm\_sleep\_mode\_set(PM\_MODE\_SUPER\_DEEP\_SLEEP);
  > 设置睡眠模式，进入超深度睡眠

<a id="id3"></a>

## RTC-睡眠模式调用函数和调用顺序说明

- 1. 配置RTC唤醒源的参数;
  > alarm\_info\_t low\_voltage\_alarm \= {
  >
  > > “low\_vol”,
  > >
  > > 3000\*RTC\_TICKS\_PER\_1MS,//设置为3000ms后唤醒，唤醒时间可以根据需求更改
  > >
  > > 1,
  > >
  > > cli\_pm\_rtc\_callback,
  > >
  > > NULL
  > >
  > > };
  >
  > bk\_alarm\_register(AON\_RTC\_ID\_1, \&low\_voltage\_alarm);
- 2. bk\_pm\_wakeup\_source\_set(PM\_WAKEUP\_SOURCE\_INT\_RTC, NULL);
  > 向系统中设置RTC方式作为唤醒源
- 3. bk\_pm\_sleep\_mode\_set(PM\_MODE\_LOW\_VOLTAGE);
  > 设置睡眠模式，进入睡眠模式
  > (备注：当前系统默认设置为睡眠模式，只需要满足投的票，就可以进入睡眠模式)
- 4. bk\_pm\_module\_vote\_sleep\_ctrl(PM\_SLEEP\_MODULE\_NAME\_APP,0x1,0x0);
  > 向系统中投应用程序的票

备注

- 1. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入睡眠模式和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。
- 2. 当前代码不会因为BT或WIFI未上电而自动替应用投对应的sleep票；需要进入睡眠模式时，应以 `pm_debug 8` 输出的 `not_sleeped` 字段确认仍未满足的票。
- 3. 追求最优功耗时，当系统开启音频，视频，LCD，CPU1，CPU2后，进入睡眠模式前需要把音频，视频，LCD，CPU1,CPU2先关闭，再进入睡眠。
- 4. 超深度睡眠的RTC模拟唤醒由 `CONFIG_RTC_ANA_WAKEUP_SUPPORT` 控制，当前BK7259默认使能；`bk_rtc_ana_register_wakeup_source()` 的 `period` 是0\~15的枚举索引，不是毫秒值。深度睡眠和睡眠模式的AON RTC闹钟不受该表限制。
