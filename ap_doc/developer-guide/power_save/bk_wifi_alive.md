# 设置WIFI睡眠模式保活说明


## WIFI-调用函数和调用顺序说明


- 1. 当使用BT配置完网络且后续不再使用BT时，可以关闭BT以降低功耗。
  > bk_bluetooth_deinit();
  >
  > 关闭BT

- 2. 连接路由器，等待STA拿到IP地址。
  > demo_sta_app_init(“a”, “b”);
  >
  > 连接路由器（a:路由器的名字；b:路由器的密码）

- 3. bk_wifi_send_listen_interval_req(10);
  > 设置监听间隔为10个DTIM周期（1表示DTIM1）。监听间隔越大，功耗越低，但广播包丢失风险也会增加，需要按业务场景选择。

- 4. bk_pm_sleep_mode_set(PM_MODE_LOW_VOLTAGE);
  > 设置睡眠模式，进入睡眠模式。

- 5. bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP,0x1,0x0);
  > 向系统中投应用程序的票。

(备注：一定需要设备连接上路由器并拿到IP地址后，才调用 `bk_pm_module_vote_sleep_ctrl()` 投APP的票，否则移动设备不能通过网络唤醒测试设备。)

备注


- 1. BT和WIFI的票，BT和WIFI模块内部进入睡眠后自己投上，SDK内部做好，应用程序不用关注。应用程序需要做的事情是，进入睡眠模式和deepsleep休眠前，把上层业务关闭，再配置唤醒源，调用接口进入睡眠。

- 2. 当前代码不会因为BT或WIFI未上电而自动替应用投对应的sleep票；需要进入睡眠模式时，应以 `pm_debug 8` 输出的 `not_sleeped` 字段确认仍未满足的票。

- 3. WIFI模块投 `PM_SLEEP_MODULE_NAME_WIFIP_MAC` sleep票时，SDK内部会设置MAC唤醒源，应用程序不需要再调用 `bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_WIFI, ...)`。

- 4. 追求最优功耗时，当系统开启音频，视频，LCD，CPU1，CPU2后，进入睡眠模式前需要把音频，视频，LCD，CPU1,CPU2先关闭，再进入睡眠。

