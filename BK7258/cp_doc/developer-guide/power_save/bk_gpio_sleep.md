---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/bk_gpio_sleep.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="gpio"></a>

# 设置GPIO作为唤醒源-系统进入深度,超深度睡眠以及低压睡眠配置说明

<a id="id1"></a>

## GPIO-深度睡眠调用函数和调用顺序说明

- 1. bk\_gpio\_register\_wakeup\_source(GPIO\_18,GPIO\_INT\_TYPE\_FALLING\_EDGE);
  1. 设置唤醒的GPIO id : GPIO18
  2. 设置GPIO唤醒模式:

```
GPIO_INT_TYPE_FALLING_EDGE: 下降延唤醒;
GPIO_INT_TYPE_RISING_EDGE: 上升延唤醒;
GPIO_INT_TYPE_LOW_LEVEL: 低电平唤醒;
GPIO_INT_TYPE_HIGH_LEVEL: 高电平唤醒;
```

- 2. bk\_pm\_wakeup\_source\_set(PM\_WAKEUP\_SOURCE\_INT\_GPIO, NULL);
  > 向系统中设置GPIO方式作为唤醒源；
- 3. bk\_pm\_sleep\_mode\_set(PM\_MODE\_DEEP\_SLEEP);
  > 设置睡眠模式，进入深度睡眠
  >
  > (系统从深度睡眠唤醒后，可以通过调用 \- bk\_gpio\_get\_wakeup\_gpio\_id() \- 函数接口获取当前时哪个GPIO ID唤醒系统)

<a id="id2"></a>

## GPIO-超深度睡眠调用函数和调用顺序说明

- 1. bk\_gpio\_ana\_register\_wakeup\_source(GPIO\_12,GPIO\_INT\_TYPE\_HIGH\_LEVEL);
  1. 设置唤醒的GPIO id: GPIO12
  > (与深度睡眠不同，超深度睡眠只支持GPIO0～15作为唤醒源，且可同时作唤醒源的GPIO个数为2个)

  2. 设置GPIO唤醒模式:
  > GPIO\_INT\_TYPE\_LOW\_LEVEL: 低电平唤醒;
  >
  > GPIO\_INT\_TYPE\_HIGH\_LEVEL: 高电平唤醒;
  >
  > （超深度睡眠只支持两种唤醒模式，且同时作唤醒源的两个GPIO的唤醒模式需一致）
- 2. bk\_pm\_sleep\_mode\_set(PM\_MODE\_SUPER\_DEEP\_SLEEP);
  > 设置睡眠模式，进入超深度睡眠
  >
  > (系统从超深度睡眠唤醒后，同样可以通过调用 \- bk\_gpio\_get\_wakeup\_gpio\_id() \- 函数接口获取当前时哪个GPIO ID唤醒系统)

<a id="id3"></a>

## GPIO-低压睡眠调用函数和调用顺序说明

- 1. bk\_gpio\_register\_wakeup\_source(GPIO\_18,GPIO\_INT\_TYPE\_FALLING\_EDGE);

  a.设置唤醒的GPIO id:GPIO18;

  b.设置GPIO唤醒模式:

  > GPIO\_INT\_TYPE\_FALLING\_EDGE: 下降延唤醒;
  >
  > GPIO\_INT\_TYPE\_RISING\_EDGE: 上升延唤醒;
  >
  > GPIO\_INT\_TYPE\_LOW\_LEVEL: 低电平唤醒;
  >
  > GPIO\_INT\_TYPE\_HIGH\_LEVEL: 低电平唤醒;
- 2. bk\_pm\_wakeup\_source\_set(PM\_WAKEUP\_SOURCE\_INT\_GPIO, NULL);
  > 向系统中设置GPIO方式作为唤醒源；
- 3. bk\_pm\_sleep\_mode\_set(PM\_MODE\_LOW\_VOLTAGE);
  > 设置睡眠模式，进入低压睡眠。(备注：当前系统默认设置为低压睡眠，只需要满足投的票，就可以进入低压睡眠)
- 4. bk\_pm\_module\_vote\_sleep\_ctrl(PM\_SLEEP\_MODULE\_NAME\_APP,0x1,0x0);
  > 向系统中投应用程序的票。

备注

- 1. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入低压和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。
- 2. 当系统中BT或WIFI模块没有上电时，系统会自动给这两个模块投上sleep的票。
- 3. 追求最优功耗时，当系统开启音频，视频，LCD，CPU1，CPU2后，进入低压睡眠前需要把音频，视频，LCD，CPU1,CPU2先关闭，再进入睡眠。
