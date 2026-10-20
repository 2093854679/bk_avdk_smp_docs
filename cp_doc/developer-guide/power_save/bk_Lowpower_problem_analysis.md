---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_Lowpower_problem_analysis.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 低功耗问题分析

<a id="id2"></a>

## 一、睡眠模式问题分析指导

<a id="id3"></a>

### 1.进睡眠模式失败

如果进睡眠模式失败，首先确认是否满足进入睡眠模式的条件：

- 1. 业务线程可能有类似while(1)的操作,业务线程一直在运行，导致系统无法进入IDLE task。

该问题debug方法：

> a) 异常后，通过串口发送测试命令：pm\_debug 1
> 观察是否有以下log打印：
>
> > ```
> > “lowvol1 0x3 0x1FFFFEFFF 0x1FFFFFFFFF”
> > “lowvol2 0x0 0x0 0x0 0x0”
> > ```
>
> 如果没有以上打印，则有可能是这个问题。
>
> b) 以上问题的解决方案：
> 线程运行不能一直while(1)进行运行或者等待，应该使用信号量或者事件标识，没有业务工作时，线程进入sleep。

- 2. 相应的模块没有投sleep的票，导致无法进入睡眠模式。

该问题debug方法：

> a) 异常后，通过串口发送测试命令：pm\_debug 1
> 有以下log打印：
>
> > ```
> > “lowvol1 0x3 0x1FFFFEFFF 0x1FFFFFFFFF”
> > “lowvol2 0x0 0x0 0x0 0x0”
> > ```
> >
> > 当前投的票的值：0x1FFFFEFFF(bit位为1，表示该位的票投上了票)
> > 需要满足的票值：0x1FFFFFFFFF
>
> 从以上两个值对比来看，bit12的值为0，表示该位置的票没有投上，
> 查看pm\_sleep\_module\_name\_e枚举类型，值为12的票
> 为PM\_SLEEP\_MODULE\_NAME\_APP，则表示该APP票没有投上。
>
> b) 以上问题的解决方案：
> 需要在业务线程处理完响应的工作后，调用以下接口把票投上：
>
> > ```
> > bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP,0x1,0x0);
> > typedef enum
> > {
> >     PM_SLEEP_MODULE_NAME_I2C1 = 0, // 0
> >     PM_SLEEP_MODULE_NAME_SPI_1,    // 1
> >     PM_SLEEP_MODULE_NAME_UART1,    // 2
> >     PM_SLEEP_MODULE_NAME_PWM_1,    // 3
> >     PM_SLEEP_MODULE_NAME_TIMER_1,  // 4
> >     PM_SLEEP_MODULE_NAME_SARADC,   // 5
> >     PM_SLEEP_MODULE_NAME_AUDP,     // 6
> >     PM_SLEEP_MODULE_NAME_VIDP,     // 7
> >     PM_SLEEP_MODULE_NAME_BTSP,     // 8
> >     PM_SLEEP_MODULE_NAME_WIFIP_MAC,// 9
> >     PM_SLEEP_MODULE_NAME_WIFI_PHY, // 10
> >     PM_SLEEP_MODULE_NAME_TIMER_2,  // 11
> >     PM_SLEEP_MODULE_NAME_APP,      // 12
> >     PM_SLEEP_MODULE_NAME_OTP,      // 13
> >     PM_SLEEP_MODULE_NAME_I2S_1,    // 14
> >     PM_SLEEP_MODULE_NAME_USB_1,    // 15
> >     PM_SLEEP_MODULE_NAME_CAN,      // 16
> >     PM_SLEEP_MODULE_NAME_PSRAM,    // 17
> >     PM_SLEEP_MODULE_NAME_QSPI_1,   // 18
> >     PM_SLEEP_MODULE_NAME_QSPI_2,   // 19
> >     PM_SLEEP_MODULE_NAME_SDIO,     // 20
> >     PM_SLEEP_MODULE_NAME_AUXS,     // 21
> >     PM_SLEEP_MODULE_NAME_LOG,      // 22
> >     PM_SLEEP_MODULE_NAME_AT,       // 23
> >     PM_SLEEP_MODULE_NAME_I2C2,     // 24
> >     PM_SLEEP_MODULE_NAME_UART2,    // 25
> >     PM_SLEEP_MODULE_NAME_UART3,    // 26
> >     PM_SLEEP_MODULE_NAME_WDG,      // 27
> >     PM_SLEEP_MODULE_NAME_AUDIO_ASR,// 28
> >     PM_SLEEP_MODULE_NAME_APP1,     // 29
> >     PM_SLEEP_MODULE_NAME_AP,     // 30
> >     PM_SLEEP_MODULE_NAME_ROSC_PROG,// 31
> >     PM_SLEEP_MODULE_NAME_ROSC,     // 32
> >     PM_SLEEP_MODULE_NAME_FLASH_OP, // 33
> >     PM_SLEEP_MODULE_NAME_LV_WAKEUP,// 34
> >     PM_SLEEP_MODULE_NAME_BK_MODEM, // 35
> >     PM_SLEEP_MODULE_NAME_ENCP,     // 36
> >
> >     PM_SLEEP_MODULE_NAME_MAX       // MAX value is 63
> > }pm_sleep_module_name_e;
> > ```

<a id="id4"></a>

### 2.睡眠模式唤醒后系统自动复位

睡眠模式唤醒后系统自动复位，可能的原因如下：

- 1. wdt复位:睡眠模式唤醒后，有中断没有清除掉，导致中断不断的上报，WDT无法喂狗导致

该问题debug方法：

> a) 该类问题，一般会进行dump，通过查看LR的地址，地址是否在pm.c出开中断后或者interrupts.c文件中的中断函数中，如果在，一般是这类问题。
> 在接收中断的函数中通过逻辑分析仪拉GPIO信号或者打印log，确定哪个中断，再结合代码和流程找出问题。
>
> b) 以上问题的解决方案：
> 中断响应完后，需要把中断清除，防止中断不断往上报。

<a id="id5"></a>

## 二、深度睡眠问题分析指导

<a id="id6"></a>

### 1.进深度睡眠失败

如果进深度睡眠失败，首先确认是否满足进入深度睡眠的条件：

- 1. 业务线程可能有类似while(1)的操作,业务线程一直在运行，导致系统无法进入IDLE task。

该问题debug方法：

> 1. 异常后，通过串口发送测试命令：pm\_debug 2

观察是否有以下log打印：

> ```
> deepsleep1 0x0 0x0
> deepsleep2 0x0 0x0 0x0 0x0
> ```

如果没有以上打印，则有可能是这个问题。

> 2. 以上问题的解决方案：

线程运行不能一直while(1)进行运行或者等待，应该使用信号量或者事件标识，没有业务工作时，线程进入sleep。

- 2. 没有满足进入深度睡眠的电源域票。当前默认 `PM_ENTER_DEEP_SLEEP_MODULES_CONFIG` 为空；如果项目中自定义增加了必须关闭的电源域，需要确认这些电源域已经投下电票。

重要

1)BT和WIFI进入SLEEP并下电，是有SDK内部代码完成，客户或者应用层代码不需要调用关闭和下电的接口
2)即使默认深睡票为空，进入deepsleep前仍建议关闭多媒体(audio,video,lcd等)和不需要的外设，避免功耗异常或唤醒后状态异常。

该问题debug方法：

> a)异常后，通过串口发送测试命令：pm\_debug 1

有以下log打印：

> > ```
> > deepsleep1 0x0 0x0
> > deepsleep2 0x0 0x0 0x0 0x0
> > ```
> >
> > 当前投的票的值：第一个0x0 (bit位为1，表示该电源域已经下电)
> > 需要满足的票值：第二个0x0
> >
> > 当前默认 `PM_ENTER_DEEP_SLEEP_MODULES_CONFIG` 为空，因此need值为0x0。如果项目自定义了该宏，例如增加BTSP、WIFIP\_MAC、AUDP、VIDP等模块，则需要对比两个值中对应bit是否已经置1。
> >
> > ```
> > #define PM_ENTER_DEEP_SLEEP_MODULES_CONFIG \
> > {\
> >     /* 当前默认配置为空。项目需要时可增加必须关闭的电源域模块。 */\
> > }
> > ```
>
> b)以上问题的解决方案：
> 如果项目在 `PM_ENTER_DEEP_SLEEP_MODULES_CONFIG` 中增加了某些电源域，则需要在进入deepsleep之前调用对应模块接口完成关闭或下电投票。

<a id="id7"></a>

## 三、获取低功耗相关调试信息

> > > 通过串口发送测试命令：pm\_debug 8，获取低功耗相关调试信息（模块未使用则不输出相关调试信息）
> >
> > 当前 `pm_debug 8` 的典型输出及解释如下：
> >
> > - `pm ahpb,bakp:0x0 0x0`：记录AHPB和BAKP电源域的投票状态；两个值均为0，表示当前没有模块投票要求对应电源域保持开启。
> > - `pm cpu1_bakp_audp:0x0`：CPU1/BAKP/AUDP电源域投票值为0，没有子模块投票要求该电源域保持开启。
> > - `pm vehp_spi_debug:0x0`：VEHP/SPI\_DEBUG电源域投票值为0，没有子模块投票要求该电源域保持开启。
> > - `pm wrlp_encp:0x8`：WRLP/ENCP电源域投票值为0x8，即bit3（MAC）仍在投票，因此该电源域保持开启。
> > - `pm hssub_power:0x0`：HSSUB电源域投票值为0，没有子模块投票要求该电源域保持开启。
> > - `pm xtal_rx_tx_anabuf:0x1`：晶振收发模拟缓冲区的休眠投票值为0x1，即bit0（DSSS\_ONLY）已经投进入休眠票。
> > - `pm sleep[module:0x1fbfffefff][need module:0x1fffffffff][not_sleeped:APP,AP][extra_sleeped:none]`：进入低压睡眠要求的票值为0x1fffffffff，当前票值为0x1fbfffefff；APP和AP尚未投休眠票，没有额外投票模块，因此当前不满足进入低压睡眠的条件。
> > - `pm deepsleep[module:0x9][need module:0x0]`：记录已经下电的电源域和进入deepsleep要求下电的电源域；当前默认 `need module` 为0x0，没有额外的强制下电要求。
> > - `pm normal sleep[module:0x1fbfffefff][need module:0x1fffffffff]`：normal sleep当前票值与要求值不一致，缺少APP和AP两张休眠票。
> > - `pm normal sleep wakeup src:0`：normal sleep唤醒源编号为0。
> > - `pm power,pmu[0x2a(pwd_cpu1:ON,pwd_vehp:OFF,pwd_wrls:ON,rom_pgen:OFF)][0x682f2(lpo_src:clk_ROSC)][7],...`：CPU1和WRLS电源域处于开启状态，VEHP和ROM电源域处于关闭状态；当前LPO时钟源为内部ROSC；7为最近一次退出低压睡眠的唤醒源编号。后面两组3个寄存器值分别记录进入和退出低压睡眠时的电源域、LPO及PSRAM状态，本次均为0，表示尚未记录到一次完整的低压睡眠过程。
> > - `AP not PD[state:0x0]`：AP电源域尚未下电，与前面的AP未投休眠票一致。
> > - `pm_psram:0x1000 0x0`：PSRAM开启投票值为0x1000，即bit12（MEDIA）仍要求PSRAM保持开启；第二个值0x0表示PSRAM heap未初始化。
> > - `pm_ap_boot_ready:0x1 0xffffffff`：第一个值0x1表示AP已经启动并处于boot ready状态；第二个值记录AP模块恢复状态。
> > - `pm_module_lv_sleep_state:0x0`：当前没有需要在退出低压睡眠后恢复的模块。
> > - `pm vote freq:40(AP),5(240M)`：当前最高CPU频率投票来自AP模块，投票频率为240 MHz。
> > - `Cur freq: CP:(480/2)M,VDDDIG:0.950000V`：CP当前实际频率为480/2，即240 MHz，VDDDIG为0.95 V。
> > - `Freq_reg:0x70003c7`：当前CPU频率配置寄存器值。
> >
> > 从以上信息可以判断：当前系统尚未满足睡眠条件，主要阻塞项为APP和AP未投休眠票；同时AP电源域仍处于开启状态，MAC仍要求WRLS电源域开启，MEDIA仍要求PSRAM开启。排查时应优先确认APP休眠投票流程以及AP关机流程是否执行完成，再根据业务场景确认MAC和MEDIA的投票是否可以释放。
> >
> > - 1)pm ahpb,bakp:0x0 0x0
> >   记录ahpb和bakp电源域上下电投票状态。
> >
> > > 备注：ahpb和bakp比较特殊，由SDK底层进行管理，一般使用场景，应用程序不需要关注。进入睡眠模式时会备份相关寄存器，退出睡眠模式时会恢复相关寄存器。
>
> - 2)pm sleep\[module:0x1fffbfefff\]\[need module:0x1fffffffff\]\[not\_sleeped:APP,LOG\]\[extra\_sleeped:none\]
>
> > 记录进入睡眠模式需要投票的模块和已经投票的模块。
> > 当系统无法进入睡眠模式时，确认该项：
> > need module:0x1fffffffff 表示当前默认睡眠模式配置中的37张票都需要投1，表示都进入睡眠状态。
> > module:0x1fffbfefff 其中为1的bit位，表示已经进入了睡眠的模块；其中为0的bit位，表示还没有进入睡眠的模块。`not_sleeped` 字段会直接列出未投票模块名称，例如APP、LOG。
> > 各个bit为对应的模块，请参考pm\_sleep\_module\_name\_e中定义的票。
>
> - 3)pm deepsleep\[module:0x9\]\[need module:0x0\]
>
> > 记录进入deepsleep需要投票的模块和已经投票的模块
> > 当前默认 `PM_ENTER_DEEP_SLEEP_MODULES_CONFIG` 为空，因此need值为0x0。如果项目自定义了该宏，need值会按宏内电源域置bit；module值中对应bit为1表示该电源域已经下电。
> >
> > > ```
> > > #define PM_ENTER_DEEP_SLEEP_MODULES_CONFIG \
> > > {\
> > >     /* 当前默认配置为空。 */\
> > > }
> > > ```
>
> - 4)pm power,pmu\[0x2a\]\[0x602f2\]\[7\],\[0x0\]\[0x0\]\[0x0\],\[0x0\]\[0x0\]\[0x0\]
>
> > 输出电源域状态、PMU状态和lpo时钟源选择状态。
> > 第一项 `0x2a` 表示电源关闭状态，关注低4bit，各个bit位代表的含义如下图。
> > 其中值为1, 表示该电源域关闭，值为0，表示该电源域开启。
> >
> > 例如:
> > a)0x2a(进入低功耗预期以下模块都关闭了)
> >
> > 其中低4bit为0xa，表示 `pwd_vehp` 和 `rom_pgen` 对应bit为1。
> >
> > 以下为每bit对应的电源(0:表示开; 1:表示关闭)：
> >
> > ```
> > bit0:pwd_cpu1  (cp1、bakp、audp)
> > bit1:pwd_vehp  (vehp、spi_debug)
> > bit2:pwd_wrls  (wrlp、encp)
> > bit3:rom_pgen  (rom power gate enable)
> > ```
> >
> > b)0x602f2
> > 以上PMU值的最后2bit表示32K时钟源,
> > 0:表示26M时钟分下来的32k; 1:表示外部32k时钟; 2:表示内部的ROSC时钟
> >
> > > 备注
> > >
> > > 进入睡眠模式的预期值为：pm power,pmu\[0x2a\]\[0x602f2\]\[7\],\[0x0\]\[0x0\]\[0x0\],\[0x0\]\[0x0\]\[0x0\]
> > > 32K时钟源以工程配置为准。当前BK7259 `PM_LPO_SOURCE` 默认配置为 `PM_LPO_SRC_DIVD`，即26M分频得到32K。
>
> - 5)Cp1 not PD\[state:0x0\]
>
> > 输出CPU1电源域状态，用于确认CPU1是否已经下电。
>
> - 6)pm\_ap\_boot\_ready:0x0 0xffffffff
>
> > 记录ap启动状态和相关状态值。
> > 当第一个值为0x0时，表示ap没有处于boot ready状态；当值为0x1时，表示ap已经启动。
>
> - 7)pm\_module\_lv\_sleep\_state:0x0
>
> > 记录退出睡眠模式时需要恢复的模块状态。
> > 该state主要是给SDK内部的bakp模块使用。
>
> - 8)pm vote freq:27(MAC),1(60M)
>
> > 记录当前CPU投频模块和投频值。例如 `27(MAC),1(60M)` 表示MAC模块投60M。
>
> - 9)Cur freq: CP:(480/8)M / Freq\_reg:0x70003df
>
> > 记录当前CP侧CPU频率和频率寄存器值。

<a id="id8"></a>

## 四、低功耗问题问答

> - 1.进入深度睡眠后功耗偏高问题确认
>   :   - a.进入深度睡眠成功后，VDDDIG的电压为0v.电流在20uA左右.
>       - b.如果VDDDIG的电压为0v, 电流超过了25uA则需要确认是否外围电路漏电。
> - 2.进入睡眠模式后功耗偏高问题确认
>   :   - a.通过pm\_debug 8确认该关闭的模块都关闭了，功耗还偏高，则确认外围电路是否由漏电。通过万用表确认各个GPIO是否有高电平。
>       - b.确认测试环境，温度高睡眠模式功耗也会变高。
>       - c.WIFI保活功耗高，则首先确认底电流是否符合预期，然后确认WIFI开窗时长是否符合预期，WIFI接收电流是否符合预期。WIFI发包周期是否频繁，DTIM的值是否符合预期。
