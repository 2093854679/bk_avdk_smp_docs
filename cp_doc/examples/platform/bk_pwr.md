---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/examples/platform/bk_pwr.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="power-manager"></a>

# power manager

<a id="id1"></a>

## 1 功能概述

支持平台power manager（normal sleep、sleep mode 、deepsleep）。

BK7259低功耗采用CP主控、AP从属的架构，整个低功耗控制流程在CP侧完成。系统开机后默认启动CP和AP；进入sleep mode或deepsleep前，CP会根据业务状态关闭AP，并在满足低功耗投票和唤醒源配置后进入低功耗状态。Wi-Fi、BLE保活场景下，周期性唤醒只需要CP参与，AP保持关闭；当业务需要音频、视频、LCD、多媒体等AP侧能力时，再通过 `pm_boot_ap` 或对应接口唤醒AP。整体架构和模块组成请参考 [低功耗整体架构](../../developer-guide/power_save/bk_lowpower_architecture.md) 。

<a id="id2"></a>

## 2 代码路径

demo路径：`components\bk_cli\cli_pwr.c`

<a id="cli"></a>

## 3 cli命令简介

demo运行依赖的宏配置：

| NAME | Description | File | value |
| --- | --- | --- | --- |
| CONFIG\_PM\_ENABLE | enable pwr cli source compile | `components\bk_cli\CMakeLists.txt` | y |
| CLI\_CFG\_PWR | enable pwr cli init | `components\bk_cli\cli_main.c` | 1 |

demo支持的命令如下：

<a id="cmd-line-1"></a>

### cmd line 1:

> pm \[sleep\_mode\] \[wake\_source\] \[vote1\] \[vote2\] \[vote3\] \[param1\] \[param2\] \[param3\]

参数说明：

```
sleep_mode：代表休眠模式(参数范围：0-3): 0:normal sleep; 1:sleep; 2:deep sleep;3:none
wake_source：表示唤醒源(参数范围：0-5)： 0：GPIO唤醒；1：RTC唤醒；2：WIFI或者BT唤醒；3：USB唤醒（BK72xx不支持);4：touch唤醒；5：none
Vote1: vote2: vote3: 代表投的票（取值范围8(BT)，9(WIFI)，12(APP))
param1：根据唤醒源有不同含义 -- GPIO：gpio的id号  RTC：唤醒时间  WIFI或者BT： touch：touch的channel号
param2：根据唤醒源有不同含义 -- GPIO：代表唤醒方式（0：低电平唤醒，1：高电平唤醒，2：上升沿唤醒，3：下降沿唤醒）  RTC和touch：唤醒时不用该参数，默认是0
param3：BT休眠时间，该参数对于发送命令是兼容接口，建议设置的时间1000000000（100s）,设置这么大的值为了使用BT模块内部模块设置的时间为准
```

<a id="deep-sleep"></a>

### deep sleep 睡眠模式

本组示例用于验证设备进入 deepsleep 后，通过 GPIO、RTC 或 touch 唤醒设备。deepsleep 场景下 VDDDIG 会掉电，唤醒后恢复到设定电压。

<a id="example-1-gpiodeepsleep"></a>

#### EXAMPLE 1: 使用GPIO唤醒deepsleep设备

测试步骤：

```
1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
2）输入命令：
   A. pm 2 0 8 9 12 8 0 1000000000
      （让系统进入deepsleep，使用GPIO进行唤醒，8表示GPIO ID，0表示低电平唤醒）；
   B. 如果希望某个GPIO从高电平唤醒，则测试前把该GPIO初始状态接为低电平，唤醒时接高电平；
   C. 如果希望某个GPIO从低电平唤醒，则测试前把该GPIO初始状态接为高电平，唤醒时接低电平；
   D. 如果希望某个GPIO从上升沿唤醒，则测试前把该GPIO初始状态接为低电平，唤醒时接高电平；
   E. 如果希望某个GPIO从下降沿唤醒，则测试前把该GPIO初始状态接为高电平，唤醒时接低电平；
3）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成设定的电压，例如0.875v；
4）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗。
```

期望结果：

```
1）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成设定的电压，例如0.875v；
2）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗；
3）deepsleep之后的功耗符合预期为15ua-20ua左右。
```

<a id="example-2-rtcdeepsleep"></a>

#### EXAMPLE 2: 使用RTC唤醒deepsleep设备

测试步骤：

```
1）开机启动5s之后（开机之后，BT、WIFI、CPU做初始化）；
2）输入命令：
   pm 2 1 8 9 12 3000 0 1000000000
   （让系统进入deepsleep，使用RTC进行唤醒，3000表示设置的唤醒时间，可自行修改，单位为ms）；
3）系统到达设定的唤醒时间后，系统会被唤醒；
4）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
5）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗。
```

期望结果：

```
1）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
2）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗；
3）deepsleep之后的功耗符合预期为15ua-20ua左右。
```

<a id="example-3-touch-deepsleep"></a>

#### EXAMPLE 3: 使用触摸(touch)唤醒deepsleep设备

测试步骤：

```
1）开机启动5s之后（开机之后，BT、WIFI、CPU做初始化）；
2）输入以下命令：
   A. touch_single_channel_calib_mode_test 2 1
      （数字2代表touch的channel号，现在测试版本默认是2，channel根据实际使用确定；数字1表示touch channel设置的强度，取值范围0~3）；
   B. pm 2 4 8 9 12 2 0 1000000000
      （让系统进入deepsleep，使用touch进行唤醒）；
   C. 手动触摸touch，可以把系统从deepsleep状态中唤醒；
3）在deepsleep过程中，通过测量VDDDIG的电压会变成0；唤醒之后，VDDDIG的电压会变成0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
4）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗。
```

期望结果：

```
1）在deepsleep过程中，通过测量VDDDIG的电压会变成0；使用touch唤醒之后，VDDDIG的电压会变成0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
2）同时通过使用精密电源来测量整个deepsleep到唤醒过程的功耗；
3）deepsleep之后的功耗符合预期为15ua-20ua左右。
```

<a id="sleep"></a>

### sleep 睡眠模式

本组示例用于验证设备进入 sleep mode 后，通过 GPIO、RTC、touch 或 Wi-Fi 保活唤醒设备。sleep 场景进入低功耗前通常需要关闭 AP，并结合业务状态配置唤醒源或低功耗投票。

<a id="example-1-gpiosleep"></a>

#### EXAMPLE 1: 使用GPIO唤醒sleep设备

测试步骤：

```
1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
2）输入以下命令：
   A. 为了最优的功耗，BT使用完毕后，请关闭，关闭命令：AT+BLEPOWER=0；
   B. pm_boot_ap 9 1
      （9表示APP模块，1表示关闭AP，0表示开启AP）；
   C. pm 1 0 8 9 12 8 2 1000000000
      （让系统进入sleep mode，使用GPIO进行唤醒，8表示GPIO ID，2表示上升沿唤醒）；
   D. 如果希望某个GPIO从高电平唤醒，则测试前把该GPIO初始状态接为低电平，唤醒时接高电平；
   E. 如果希望某个GPIO从低电平唤醒，则测试前把该GPIO初始状态接为高电平，唤醒时接低电平；
   F. 如果希望某个GPIO从上升沿唤醒，则测试前把该GPIO初始状态接为低电平，唤醒时接高电平；
   G. 如果希望某个GPIO从下降沿唤醒，则测试前把该GPIO初始状态接为高电平，唤醒时接低电平；
3）在sleep mode过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
4）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
```

期望结果：

```
1）在sleep mode过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
2）同时通过使用精密电源来测量整个sleep mode到唤醒过程的功耗。
```

<a id="example-2-rtcsleep"></a>

#### EXAMPLE 2: 使用RTC唤醒sleep设备

测试步骤：

```
1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
2）输入以下命令：
   A. WIFI没有业务的时候，默认进入sleep状态；
   B. 蓝牙默认进入sleep（为了最优的功耗，BT使用完毕后，请关闭，关闭命令：AT+BLEPOWER=0）；
   C. pm_boot_ap 9 1
      （9表示APP模块，1表示关闭AP，0表示开启AP）；
   D. pm 1 1 0 0 12 10000 0 1
      （让系统进入sleep，使用RTC进行唤醒，10000表示设置的唤醒时间，可自行修改，单位为ms）；
3）系统到了指定的唤醒时间后，系统会被从睡眠状态下唤醒；
4）在sleep过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
5）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
```

期望结果：

```
1）在sleep过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
2）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
```

<a id="example-3-touch-sleep"></a>

#### EXAMPLE 3: 使用触摸(touch)唤醒sleep设备

备注

注意：使用我们的BK7259开发板测试Touch，需要把EVB上R65上电阻移到R66上;Touch默认使用Channel0,占用GPIO19，GPIO19是给多媒体使用，因此支持touch的evb设计时需要注意避免GPIO19被占用或者使用其他GPIO给touch使用。

测试步骤：

```
1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
2）输入以下命令：
   A. 为了最优的功耗，BT使用完毕后，请关闭，关闭命令：AT+BLEPOWER=0；
   B. touch_single_channel_calib_mode_test 0 1
      （数字2代表touch的channel号，现在测试版本默认是0，channel根据实际使用确定；数字1表示touch channel设置的强度，取值范围0~3）；
   C. pm_boot_ap 9 1
      （9表示APP模块，1表示关闭AP，0表示开启AP）；
   D. pm 1 4 8 9 12 0 0 1000000000
      （让系统进入sleep mode，使用touch进行唤醒，0:第一个0表示touch的channel号）；
   E. 手动触摸touch，可以把系统从sleep mode状态中唤醒；
3）在sleep mode过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
4）同时通过使用精密电源来测量整个sleep mode到唤醒过程的功耗。
```

期望结果：

```
1）在sleep过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
2）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
```

<a id="cmd-line-2"></a>

### cmd line 2:

> pm\_vote \[sleep\_mode\] \[pm\_vote\] \[pm\_vote\_value\] \[pm\_sleep\_time\]

```
sleep_mode：代表休眠模式(参数范围：0-3): 0:normal sleep; 1:sleep; 2:deep sleep;3:none
pm_vote:代表投的票（取值范围8(BT)，9(WIFI)，12(APP)）
pm_vote_value：投票值（取值范围0：MODULE_STATE_ON   1：MODULE_STATE_OFF）
pm_sleep_time：BT休眠时间，该参数对于发送命令是兼容接口，建议设置的时间1000000000（100s）,设置这么大的值为了使用BT模块内部模块设置的时间为准
```

<a id="example-4-wifisleep"></a>

#### EXAMPLE 4: 使用WIFI保活唤醒sleep设备

测试步骤：

```
1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
2）输入以下五条命令：
   A. set_interval 10
      （该命令是设置DTIM10；配置其他值：DTIM1命令为set_interval 1，DTIM3命令为set_interval 3）；
   B. sta 123 12345678
      （连接路由器，123表示路由器名称，12345678表示路由器密码，WIFI会进入sleep wakeup流程）；
   C. 蓝牙默认进入sleep（为了最优的功耗，BT使用完毕后，请关闭，关闭命令：AT+BLEPOWER=0）；
   D. pm_boot_ap 9 1
      （9表示APP模块，1表示关闭AP，0表示开启AP）；
   E. pm_vote 1 12 1 0
      （投APP票）；
3）在sleep过程中，通过测量VDDDIG的电压会变成0v；唤醒之后，VDDDIG的电压会变成睡眠前的电压值，例如0.875v，如果提频了电压也会提高，例如VDDDIG的电压为0.925v；
4）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗，底电流为50uA左右。
```

<a id="example-5-blesleep"></a>

#### EXAMPLE 5: 使用BLE广播保活唤醒sleep设备

测试步骤：

```
1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
2）输入以下命令：
   A. ap_cmd AT+BLEADVPARAM=7,640,640,0,0,3,1,1
      （创建1s间隔adv）；
   B. ap_cmd AT+BLEADVDATA=0201060A09373235364e5f424c45,E
      （配置广播数据）；
   C. ap_cmd AT+BLEADVENABLE=1
      （开启BLE广播）；
   D. pm_boot_ap 9 1
      （9表示APP模块，1表示关闭AP，0表示开启AP）；
   E. pm_vote 1 12 1 0
      （投APP票，关闭CP进入sleep）；
3）在BLE广播保活过程中，系统进入sleep并周期性唤醒处理广播事件；
4）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
```

<a id="example-6-blesleep"></a>

#### EXAMPLE 6: 使用BLE连接保活唤醒sleep设备

测试步骤：

```
1）开机启动5s之后，（开机之后，BT、WIFI、CPU做初始化）；
2）输入以下命令：
   A. ap_cmd AT+BLEADVPARAM=7,320,320,0,0,3,1,1
      （创建广播）；
   B. ap_cmd AT+BLEADVDATA=0201060A09373235364e5f424c45,E
      （配置广播数据）；
   C. ap_cmd AT+BLEADVENABLE=1
      （开启BLE广播）；
   D. 使用nRF Connect连接该BLE广播；
   E. ap_cmd AT+BLECONNPARAM=57:16:ef:df:e0:7e,320,320,0,1f4
      （更新连接间隔为1s）；
   F. pm_boot_ap 9 1
      （9表示APP模块，1表示关闭AP，0表示开启AP）；
   G. pm_vote 1 12 1 0
      （投APP票，关闭CP进入sleep）；
3）在BLE连接保活过程中，系统进入sleep并按连接间隔周期性唤醒；
4）同时通过使用精密电源来测量整个sleep到唤醒过程的功耗。
```

备注

pm\_vote命令和pm命令差异:

> - pm\_vote命令是只投进睡眠的票，不配置唤醒源;使用场景是使用其他命令配置了唤醒源，例如wifi和路由器连接上之后，发该命令进入睡眠。
> - pm命令不但投进睡眠的票，还配置RTC,GPIO,TOUCH唤醒源。

<a id="ap-gpiortc"></a>

### AP侧低功耗验证：配置GPIO和RTC唤醒

重要

AP侧 `pm_ap_demo` 低功耗测试命令

本节单独介绍AP侧通过 `pm_ap_demo` 命令配置GPIO和RTC唤醒源，验证sleep和deepsleep低功耗唤醒流程。

<a id="id3"></a>

#### 命令格式

```
pm_ap_demo {init|sleep|deep_sleep}
```

<a id="id4"></a>

#### 命令说明

- `init`：初始化 `pm_ap_demo` 线程。
- `sleep`：配置设备进入睡眠状态。
- `deep_sleep`：配置设备进入深度睡眠状态。

常用命令示例：

- 进入 sleep：`ap_cmd pm_ap_demo sleep 50000 1 8 2`
- 进入 deepsleep：`ap_cmd pm_ap_demo deep_sleep 50000 1 8 2`

<a id="id5"></a>

#### 参数说明

`config_data` 参数格式如下：

| 参数 | 说明 |
| --- | --- |
| `50000` | 睡眠时间，单位为 ms，`50000` 表示 50s。 |
| `1` | 睡眠次数，deepsleep 只支持 1 次。 |
| `8` | GPIO ID，表示使用 GPIO8 作为唤醒源。 |
| `2` | 唤醒触发方式，`0` 表示低电平，`1` 表示高电平，`2` 表示上升沿，`3` 表示下降沿。 |

<a id="example-1-gpiortcsleep"></a>

#### EXAMPLE 1: 使用GPIO和RTC唤醒sleep设备

```
ap_cmd pm_ap_demo init
ap_cmd pm_ap_demo sleep 50000 1 8 2
```

以上命令配置设备进入 sleep 50s，使用 GPIO8 作为唤醒源，并通过上升沿触发唤醒。

<a id="example-2-gpiortcdeepsleep"></a>

#### EXAMPLE 2: 使用GPIO和RTC唤醒deepsleep设备

```
ap_cmd pm_ap_demo init
ap_cmd pm_ap_demo deep_sleep 50000 1 8 2
```

以上命令配置设备进入 deepsleep 50s，使用 GPIO8 作为唤醒源，并通过上升沿触发唤醒。
