---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# 设置touch作为唤醒源-系统进入深度睡眠以及睡眠模式配置说明


## Touch-进入深度睡眠调用函数和调用顺序说明


- 1. 使用touch使用唤醒源时，首先需要touch模块初始化后才能使用，可以在代码中调用初始化代码，也可以通过cli command命令来测试。

  touch初始化的cli command例如：


  - 1.1. Cli command: “touch_single_channel_calib_mode_test 2 1”
  > 备注：使用touch的channel 2作为唤醒的触发channel,设置的值为1

- 2. 调用pm模块接口进入深度睡眠

  - 2.1. 配置TOUCH唤醒源的参数

    ```
    touch_wakeup_param_t   touch_wakeup_param  = {0};
    touch_wakeup_param.touch_channel = 2;
    bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_TOUCHED, &touch_wakeup_param);
    ```

    备注：使用touch的channel 2作为唤醒的触发channel

  - 2.2. bk_pm_sleep_mode_set(PM_MODE_DEEP_SLEEP);
    备注：设置睡眠模式，进入深度睡眠


## Touch-进入睡眠模式调用函数说明


- 1. 使用touch使用唤醒源时，首先需要touch模块初始化后才能使用，可以在代码中调用初始化代码，也可以通过cli command命令来测试。
  > touch初始化的cli command例如：
  >
  > - 1.1 Cli command: “touch_single_channel_calib_mode_test 2 1”
  >
  > 备注：以上cli command 命令的含义：使用touch的channel 2作为唤醒的触发channel,设置的值为1

- 2. 调用pm模块接口进入睡眠模式

  - 2.1 配置TOUCH唤醒源的参数

    > ```
    > touch_wakeup_param_t    touch_wakeup_param  = {0};
    > touch_wakeup_param.touch_channel = 2;
    > bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_TOUCHED, &touch_wakeup_param);
    > ```

  - 2.2 bk_pm_sleep_mode_set(PM_MODE_LOW_VOLTAGE)
    :   备注： 设置睡眠模式，进入睡眠模式。
        (当前系统默认设置为睡眠模式，只需要满足投的票，就可以进入睡眠模式)

  - 2.3 bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP,0x1,0x0)
    :   备注：向系统中投应用程序的票。

备注


- 1. 当前低功耗状态机中，TOUCH可作为深度睡眠和睡眠模式唤醒源，不支持超深度睡眠唤醒。

- 2. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入睡眠模式和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。

- 3. 当前代码不会因为BT或WIFI未上电而自动替应用投对应的sleep票；需要进入睡眠模式时，应以 `pm_debug 8` 输出的 `not_sleeped` 字段确认仍未满足的票。

- 4. 追求最优功耗时，当系统开启音频，视频，LCD，CPU1，CPU2后，进入睡眠模式前需要把音频，视频，LCD，CPU1,CPU2先关闭，再进入睡眠。

