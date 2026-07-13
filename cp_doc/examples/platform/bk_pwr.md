# power manager



## 1 功能概述

> 支持平台power manager（normal sleep、sleep mode 、deepsleep）。
>
> BK7259低功耗采用CP主控、AP从属的架构，整个低功耗控制流程在CP侧完成。系统开机后默认启动CP和AP；进入sleep mode或deepsleep前，CP会根据业务状态关闭AP，并在满足低功耗投票和唤醒源配置后进入低功耗状态。Wi-Fi、BLE保活场景下，周期性唤醒只需要CP参与，AP保持关闭；当业务需要音频、视频、LCD、多媒体等AP侧能力时，再通过 `pm_boot_ap` 或对应接口唤醒AP。整体架构和模块组成请参考 [低功耗整体架构](../../developer-guide/power_save/bk_lowpower_architecture.md "../../developer-guide/power_save/bk_lowpower_architecture.md") 。


## 2 代码路径

> demo路径：`components\bk_cli\cli_pwr.c`


## 3 cli命令简介

demo运行依赖的宏配置：

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG_PM_ENABLE | enable pwr cli source compile | `components\bk_cli\CMakeLists.txt` | y |
> | CLI_CFG_PWR | enable pwr cli init | `components\bk_cli\cli_main.c` | 1 |

demo支持的命令如下：


### cmd line 1:

> pm [sleep_mode] [wake_source] [vote1] [vote2] [vote3] [param1] [param2] [param3]
>
> > ```
> > sleep_mode：代表休眠模式(参数范围：0-3): 0:normal sleep; 1:sleep; 2:deep sleep;3:none
> > wake_source：表示唤醒源(参数范围：0-5)： 0：GPIO唤醒；1：RTC唤醒；2：WIFI或者BT唤醒；3：USB唤醒（BK72xx不支持);4：touch唤醒；5：none
> > Vote1: vote2: vote3: 代表投的票（取值范围8(BT)，9(WIFI)，12(APP))
> > param1：根据唤醒源有不同含义 -- GPIO：gpio的id号  RTC：唤醒时间  WIFI或者BT： touch：touch的channel号
> > param2：根据唤醒源有不同含义 -- GPIO：代表唤醒方式（0：低电平唤醒，1：高电平唤醒，2：上升沿唤醒，3：下降沿唤醒）  RTC和touch：唤醒时不用该参数，默认是0
> > param3：BT休眠时间，该参数对于发送命令是兼容接口，建议设置的时间1000000000（100s）,设置这么大的值为了使用BT模块内部模块设置的时间为准
> > ```


#### EXAMPLE 1: 使用GPIO作为唤醒源来唤醒deepsleep设备

> 测试步骤：
>
> > ```
> > 1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
> > 2）输入命令：
> > A. pm 2 0 8 9 12 8 0 1000000000（让系统进入deepsleep，使用gpio进行唤醒，8表示gpio的id，0代表低电平唤醒)；
> > B. 如果希望某个GPIO从高电平唤醒，则测试前把该GPIO初始状态接为低电平，唤醒时接高电平；
> > C. 如果希望某个GPIO从低电平唤醒，则测试前把该GPIO初始状态接为高电平，唤醒时接低电平；
> > D. 如果希望某个GPIO从上升沿唤醒，则测试前把该GPIO初始状态接为低电平，唤醒时接高电平；
> > E. 如果希望某个GPIO从下降沿唤醒，则测试前不要把该GPIO初始状态接为高电平，唤醒时接低电平；
> > 3）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成设定的电压，例如0.875v；
> > 4）同时通过使用精密电源来测量整个deep sleep到唤醒过程的功耗。
> > ```
>
> 期望结果：
>
> > ```
> > 1）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成设定的电压，例如0.875v；
> > 2）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗；
> > 3）deepsleep之后的功耗符合预期为15ua-20ua左右。
> > ```


#### EXAMPLE 2: 使用RTC设置唤醒时间来唤醒deepsleep设备

> 测试步骤：
>
> > ```
> > 1）开机启动5s之后（开机之后，BT、WIFI、CPU做初始化）；
> > 2）输入命令: pm 2 1 8 9 12 3000 0 1000000000（让系统进入deepsleep，使用RTC进行唤醒，3000表示设置的唤醒时间，可自行修改，单位为ms)；
> > 3）系统到达设定的的唤醒时间后，系统会被唤醒；
> > 4）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> > 5）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗。
> > ```
>
> 期望结果：
>
> > ```
> > 1）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。；
> > 2）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗；
> > 3）deepsleep之后的功耗符合预期为15ua-20ua左右。
> > ```


#### EXAMPLE 3:使用触摸(touch)作为唤醒源来唤醒deepsleep设备

> 测试步骤：
>
> > ```
> > 1）开机启动5s之后（开机之后，BT、WIFI、CPU做初始化）；
> > 2）输入以下两条命令：
> > A. touch_single_channel_calib_mode_test 2 1（数字2代表touch的channel号，现在测试版本默认是2,channnel根据实际使用确定；数字1表示touch channel设置的强度，取值范围0~3）；
> > B. pm 2 4 8 9 12 2 0 1000000000（让系统进入deepsleep，使用touch进行唤醒）；
> > C.手动触摸touch,可以把系统从deepsleep状态中唤醒；
> > 3）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> > 4）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗。
> > ```
>
> 期望结果：
>
> > ```
> > 1）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒（使用touch）之后，唤醒之后，VDDDIG的电压会变成0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> > 2）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗；
> > 3）deepsleep之后的功耗符合预期为15ua-20ua左右。
> > ```


#### EXAMPLE 4: 使用GPIO来唤醒进入睡眠设备

> 测试步骤：
>
> > ```
> > 1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
> > 2）输入以下命令：
> > A0.p(为了最优的功耗，BT使用完毕后，请关闭，关闭命令：AT+BLEPOWER=0)
> > A. pm_boot_ap 9 1（9表示APP模块，1：表示关闭AP，0：表示开启AP）；
> > B. pm 1 0 8 9 12 8 2 1000000000（让系统进入sleep mode，使用gpio进行唤醒，8表示gpio的id，2代表上升沿唤醒)；
> > C. 如果希望某个GPIO从高电平唤醒，则测试前把该GPIO初始状态接为低电平，唤醒时接高电平；
> > D. 如果希望某个GPIO从低电平唤醒，则测试前把该GPIO初始状态接为高电平，唤醒时接低电平；
> > E. 如果希望某个GPIO从上升沿唤醒，则测试前把该GPIO初始状态接为低电平，唤醒时接高电平；
> > F. 如果希望某个GPIO从下降沿唤醒，则测试前不要把该GPIO初始状态接为高电平，唤醒时接低电平；
> > 3）在sleep mode过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> > 4）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
> > ```
>
> 期望结果：
>
> > ```
> > 1）在sleep mode过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> > 2）同时通过使用精密电源来测量整个sleep mode到唤醒过程的功耗。
> > ```


#### EXAMPLE 5: 使用RTC作为唤醒源来唤醒进入睡眠设备

> 测试步骤：
>
> > ```
> > 测试步骤如下：
> > 1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
> > 2）输入以下命令：
> > A. WIFI没有业务的时候，默认进入sleep状态；
> > B. 蓝牙默认进入sleep(为了最优的功耗，BT使用完毕后，请关闭，关闭命令：AT+BLEPOWER=0)；
> > C. pm_boot_ap 9 1（9表示APP模块，1：表示关闭AP，0：表示开启AP）；
> > D. pm 1 1 0 0 12 10000 0 1（让系统进入sleep，使用RTC进行唤醒，10000表示设置的唤醒时间，可自行修改，单位为ms)；
> > 3）系统到了指定的唤醒时间后，系统会被从睡眠状态下唤醒
> > 4）在sleep过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> > 5）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
> > ```
>
> 期望结果：
>
> > ```
> > 1）在sleep过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> > 2）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
> > ```


#### EXAMPLE 6: 使用触摸(touch)来唤醒进入睡眠设备（—-当前还不支持，后续测试命令会完善支持）

> 测试步骤：
>
> > ```
> > 1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
> > 2）输入以下命令：
> > A0.为了最优的功耗，BT使用完毕后，请关闭，关闭命令：AT+BLEPOWER=0)
> > A. touch_single_channel_calib_mode_test 2 1（数字2代表touch的channel号，现在测试版本默认是2,channnel根据实际使用确定；数字1表示touch channel设置的强度，取值范围0~3）
> > B. pm_boot_ap 9 1（9表示APP模块，1：表示关闭AP，0：表示开启AP）
> > C. pm 1 4 8 9 12 2 0 1000000000（让系统进入sleep mode，使用touch进行唤醒，2表示touch的channel号)
> > D. 手动触摸touch,可以把系统从sleep mode状态中唤醒；
> > 3）在sleep mode过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> > 4）同时通过使用精密电源来测量整个sleep mode到唤醒过程的功耗。
> > ```
>
> 期望结果：
>
> > ```
> > 1）在sleep过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> > 2）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
> > ```


### cmd line 2:

> pm_vote [sleep_mode] [pm_vote] [pm_vote_value] [pm_sleep_time]
>
> > ```
> > sleep_mode：代表休眠模式(参数范围：0-3): 0:normal sleep; 1:sleep; 2:deep sleep;3:none
> > pm_vote:代表投的票（取值范围8(BT)，9(WIFI)，12(APP)）
> > pm_vote_value：投票值（取值范围0：MODULE_STATE_ON   1：MODULE_STATE_OFF）
> > pm_sleep_time：BT休眠时间，该参数对于发送命令是兼容接口，建议设置的时间1000000000（100s）,设置这么大的值为了使用BT模块内部模块设置的时间为准
> > ```


#### EXAMPLE 1: 使用WIFI保活来唤醒睡眠设备

> 测试步骤：
>
> > ```
> >     测试步骤如下：
> >     1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
> >     2）输入以下五条命令：
> >     A. set_interval 10 (该命令是设置DTIM10）
> > (备注：配置其他值：DTIM1命令：set_interval 1； DTIM3命令：set_interval 3)
> >     B. sta 123(路由器名称) 12345678（路由器密码）（连接路由器，WIFI会进入sleep wakeup流程）
> >     C. 蓝牙默认进入sleep(为了最优的功耗，BT使用完毕后，请关闭，关闭命令：AT+BLEPOWER=0)
> >     D. pm_boot_ap 9 1（9表示APP模块，1：表示关闭AP，0：表示开启AP）
> >     E. pm_vote 1 12 1 0（投app票）
> >     3）在sleep过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v。
> >     4）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗(底电流为50uA左右)。
> > ```

备注

pm_vote命令和pm命令差异:

> - pm_vote命令是只投进睡眠的票，不配置唤醒源;使用场景是使用其他命令配置了唤醒源，例如wifi和路由器连接上之后，发该命令进入睡眠。
> - pm命令不但投进睡眠的票，还配置RTC,GPIO,TOUCH唤醒源。


---

pm_demo {init||cmd|config_data}

init: 初始化pm_demo线程

send_cmd: 发送命令给pm_demo线程，例如：


- 进入睡眠：ap_cmd pm_demo sleep 50000 1 8 2

- 进入深度睡眠：ap_cmd pm_demo deep_sleep 50000 1 8 2

config_data: 配置数据给pm_demo线程，格式如下:

5000：睡眠时间，以ms为单位，5000表示5s

1: 表示睡眠次数，Deepsleep只支持1次

8：表示GPIO ID

2:表示上升沿（0：低电平；1：高电平；2：上升沿；3：下降延）


#### EXAMPLE 1: 使用GPIO,RTC保活来唤醒睡眠设备


```
ap_cmd pm_demo init
ap_cmd pm_demo sleep 50000 1 8 2

```

以上命令作用是配置进入睡眠时间为5s，使用GPIO8作为唤醒源，使用上升沿唤醒。


#### EXAMPLE 2: 使用GPIO,RTC保活来唤醒deepsleep设备


```
ap_cmd pm_demo init
ap_cmd pm_demo deep_sleep 50000 1 8 2

```

以上命令作用是配置进入深度睡眠时间为5s，使用GPIO8作为唤醒源，使用上升沿唤醒。
