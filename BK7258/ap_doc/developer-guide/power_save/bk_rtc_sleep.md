---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/bk_rtc_sleep.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rtc"></a>

# 设置RTC作为唤醒源-系统进入深度,超深度睡眠以及低压睡眠配置说明

<a id="id1"></a>

## RTC-深度睡眠调用函数和调用顺序说明

备注

**具体代码参考AP侧PM demo工程代码：ap/middleware/driver/pwr\_clk/pm\_ap\_demo.c**

- 1. 配置RTC唤醒源的参数

```
pm_ap_rtc_info_t low_power_info = {0};
low_power_info.period_tick                = 5000;//unit:ms;eg:5000(5s)
low_power_info.period_cnt                 = 1;//total period count == 0Xffffffff means forever period;else period how many times
low_power_info.callback                   = rtc_sleep_wakeup_callback;
low_power_info.param_p                    = NULL;

bk_pm_ap_rtc_regsiter_wakeup(PM_MODE_DEEP_SLEEP,&low_power_info);
```

回调函数示例：

```
static bk_err_t rtc_sleep_wakeup_callback(pm_sleep_mode_e sleep_mode,pm_wakeup_source_e wake_source,void* param_p)
{
    pm_ap_core_msg_t msg = {0};
    msg.event= PM_DEMO_CALLBACK_MSG_HANDLE;
    msg.param1 = PM_MODE_LOW_VOLTAGE;
    msg.param2 = PM_WAKEUP_SOURCE_INT_RTC;
    msg.param3 = 0;
    bk_pm_demo_send_msg(&msg);
    return BK_OK;
}
```

- 2. bk\_pm\_sleep\_mode\_set(PM\_MODE\_DEEP\_SLEEP);
  > 设置睡眠模式，进入深度睡眠

<a id="id2"></a>

## RTC-低压睡眠调用函数和调用顺序说明

- 1. 配置RTC唤醒源的参数;

```
pm_ap_rtc_info_t low_power_info = {0};
low_power_info.period_tick                = 5000;//unit:ms;eg:5000(5s)
low_power_info.period_cnt                 = 1;//total period count == 0Xffffffff means forever period;else period how many times
low_power_info.callback                   = rtc_sleep_wakeup_callback;
low_power_info.param_p                    = NULL;

bk_pm_ap_rtc_regsiter_wakeup(PM_MODE_LOW_VOLTAGE,&low_power_info);
```

回调函数示例：

```
static bk_err_t rtc_sleep_wakeup_callback(pm_sleep_mode_e sleep_mode,pm_wakeup_source_e wake_source,void* param_p)
{
    pm_ap_core_msg_t msg = {0};
    msg.event= PM_DEMO_CALLBACK_MSG_HANDLE;
    msg.param1 = PM_MODE_LOW_VOLTAGE;
    msg.param2 = PM_WAKEUP_SOURCE_INT_RTC;
    msg.param3 = 0;
    bk_pm_demo_send_msg(&msg);
    return BK_OK;
}
```

- 2. bk\_pm\_module\_vote\_sleep\_ctrl(PM\_SLEEP\_MODULE\_NAME\_APP,0x1,0x0);
  > 向系统中投应用程序的票

备注

- 1. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入低压和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。
- 2. 当系统中BT或WIFI模块没有上电时，系统会自动给这两个模块投上sleep的票。
- 3. 追求最优功耗时，当系统开启音频，视频，LCD，CPU1，CPU2后，进入低压睡眠前需要把音频，视频，LCD先关闭，再进入睡眠。
     当前SMP架构，AP是不下电的。
