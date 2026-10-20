---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/bk_touch_sleep.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="touch"></a>

# 设置touch作为唤醒源-系统进入深度,超深度睡眠以及低压睡眠配置说明

<a id="id1"></a>

## Touch-进入深度睡眠调用函数和调用顺序说明

- 1. 使用touch使用唤醒源时，首先需要touch模块初始化后才能使用，可以在代码中调用初始化代码，也可以通过cli command命令来测试。

  touch初始化的cli command例如：

  - 1.1. Cli command: “touch\_single\_channel\_calib\_mode\_test 2 1”
  > 备注：使用touch的channel 2作为唤醒的触发channel,设置的值为1
- 2. 调用pm模块接口进入深度睡眠
  - 2.1. 配置TOUCH唤醒源的参数
    touch\_wakeup\_param\_t touch\_wakeup\_param \= {0};
    touch\_wakeup\_param.touch\_channel \= 2;
    bk\_pm\_wakeup\_source\_set(PM\_WAKEUP\_SOURCE\_INT\_TOUCHED, \&touch\_wakeup\_param);
    备注：使用touch的channel 2作为唤醒的触发channel
  - 2.2. bk\_pm\_sleep\_mode\_set(PM\_MODE\_DEEP\_SLEEP);
    备注：设置睡眠模式，进入深度睡眠

<a id="id2"></a>

## Touch-进入低压睡眠调用函数说明

- 1. 使用touch使用唤醒源时，首先需要touch模块初始化后才能使用，可以在代码中调用初始化代码，也可以通过cli command命令来测试。
  > touch初始化的cli command例如：
  >
  > - 1.1 Cli command: “touch\_single\_channel\_calib\_mode\_test 2 1”
  >
  > 备注：以上cli command 命令的含义：使用touch的channel 2作为唤醒的触发channel,设置的值为1
- 2. 调用pm模块接口进入低压睡眠
  - 2.1 配置TOUCH唤醒源的参数
    :   touch\_wakeup\_param\_t touch\_wakeup\_param \= {0};
        touch\_wakeup\_param.touch\_channel \= 2;
        bk\_pm\_wakeup\_source\_set(PM\_WAKEUP\_SOURCE\_INT\_TOUCHED, \&touch\_wakeup\_param);
  - 2.2 bk\_pm\_sleep\_mode\_set(PM\_MODE\_LOW\_VOLTAGE)
    :   备注： 设置睡眠模式，进入低压睡眠。
        (当前系统默认设置为低压睡眠，只需要满足投的票，就可以进入低压睡眠)
  - 2.3 bk\_pm\_module\_vote\_sleep\_ctrl(PM\_SLEEP\_MODULE\_NAME\_APP,0x1,0x0)
    :   备注：向系统中投应用程序的票。

备注

- 1. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入低压和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。
- 2. 当系统中BT或WIFI模块没有上电时，系统会自动给这两个模块投上sleep的票。
- 3. 追求最优功耗时，当系统开启音频，视频，LCD，CPU1，CPU2后，进入低压睡眠前需要把音频，视频，LCD，CPU1,CPU2先关闭，再进入睡眠。
