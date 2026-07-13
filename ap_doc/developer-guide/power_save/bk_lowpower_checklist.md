# 低功耗问题分析Checklist


- 进入睡眠模式(sleep mode)或者deep sleep失败分析步骤


---

> - 1.异常后，发送pm_debug 8命令抓取log,根据前面log分析步骤 [低功耗问题分析](bk_Lowpower_problem_analysis.md "bk_Lowpower_problem_analysis.md") ，分析哪几个模块没有投票等,如果能快速找出问题，则解决。
>
>   > 备注：如果不好发pm_debug 8命令，可以在进入睡眠模式失败的时候，调用以下函数，抓取log:
>   > :   - 1. pm_debug_ctrl(8);
>   >     - 2. pm_debug_pwr_clk_state();
>   >     - 3. pm_debug_lv_state();
> - 2.如果不好找出问题，则可以先下载原版SDK，通过发命令的方式进入睡眠模式和deepsleep，确认是否成功。如果是失败的，则可以提问题单，让我们分析确认。
> - 3.如果成功，那么失败的原因可能是自己添加代码导致的，可以采用一点一点添加代码的方式确认，哪块有问题。
> - 4.确认进入睡眠模式或者deepsleep前，应用层代码结束了业务，再进入睡眠模式或者deepsleep。
> - 5.如果该投票的票，都投了，在睡眠过程中异常了，则需要抓取发生问题前后的电流图。通过电流图查看，发生问题的时机；可以通过执行部分代码发方式，找出是哪块代码执行异常。
> - 6.分析时可以抓取正常和异常时的log和电流图对比，分析差异，找出问题。
> - 7.以上排查完，找不出原因，如果需要协助，可以提供发生问题的步骤，抓取pm_debug 8的log，抓取发生问题前后的电流图，SDK版本等信息提问题单给我们。


- 进入睡眠模式(sleep mode)或者deep sleep功耗高分析步骤


---

> - 1.首先确认是否是当前PCB上额外挂载的外设模块，没有下电导致功耗高。
> - 2.首先下载原版SDK，通过选择RTC唤醒方式，发命令的方式进入睡眠模式或者deepsleep(命令可以参考文档中样例演示->平台-> power manager中示例)，对比功耗差异。
> - 3.通过发送pm_debug 8,查看log中“pm power and pmu state[0x202a25e8][0x7d000272] ”、“pm low vol[…]”和“pm deepsleep[…]”，并根据log分析 [低功耗问题分析](bk_Lowpower_problem_analysis.md "bk_Lowpower_problem_analysis.md") 。
>
>   解析0x202a25e8：低4bit对应以下电源门控状态(0:表示该power domain是开启的; 1:表示该power domain是关闭的)。
>   0x7d000272：以上值的最后2bit表示32K时钟源,0:表示26M时钟分下来的32k; 1:表示外部32k时钟; 2:表示内部的ROSC时钟。
>
>   以下为各个bit对应的power domain:
>
>   ```
>   bit0:pwd_cpu1  (cp1、bakp、audp)
>   bit1:pwd_vehp  (vehp、spi_debug)
>   bit2:pwd_wrls  (wrlp、encp)
>   bit3:rom_pgen  (rom power gate enable)
>   ```
>
> > 备注
> >
> > 进入睡眠模式的预期值为：pm power,pmu[0x2a][0x602f2][7],[0x0][0x0][0x0],[0x0][0x0][0x0]
> > 32K时钟源以工程配置为准。当前BK7259 `PM_LPO_SOURCE` 默认配置为 `PM_LPO_SRC_DIVD`，即26M分频得到32K。
> > 睡眠模式票据和深睡电源域票据的预期掩码会随 `PM_ENTER_LOW_VOL_MODULES_CONFIG` 和 `PM_ENTER_DEEP_SLEEP_MODULES_CONFIG` 变化，不建议脱离当前 `pm.h` 配置写死判断。
>
> - 4.同时通过电流波形图，查看功耗差异，是否存在异常电流。
> - 5.另外排查下系统会不会误入了ATE模式(通过查看log，由提示ate enabled is 1,值预期为0:关闭)或者DTIM参数设置和预期的不一样等。


- 进入睡眠模式(sleep mode)或者deep sleep唤醒失败分析步骤


---

> - 1.需要使用唤醒源唤醒处于睡眠中(睡眠模式(sleep mode)或者deep sleep)的系统, 唤醒的前提是系统成功进入了睡眠模式或者deep sleep睡眠状态
> - 2.如果唤醒失败，可以通过测量电流的方式确认是否成功进入了睡眠模式或者deep sleep睡眠状态。睡眠模式时底电流小于100uA左右,deep sleep时底电流小于25uA左右；该值与板级外设、32K源、GPIO电平和工程配置相关，仅作为经验参考。

