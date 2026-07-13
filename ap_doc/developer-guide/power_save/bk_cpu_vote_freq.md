# 如何动态切换CPU主频


## 切换时钟的策略


- 1.配置CPU主频统一在CP上(避免多核操作相同的寄存器不同步而出现异常)。

- 2.CPU选择投频最高的模块的CPU主频。

- 3.支持CP侧调用bk_pm_module_vote_cpu_freq()接口投频。

- 4.启动AP时，当前SDK默认把主频升到最高，应用程序可以不用额外再调接口投频。

- 5.CP侧CPU主频和AP侧CPU主频可以独立配置，互不干扰；CP侧可根据业务需求动态投不同的CPU主频。

- 6.AP侧CPU主频当前默认为480M。


## 支持配置的CPU主频

投频后CPU和BUS的频率对应关系：
:   - 0. PM_CPU_FRQ_XTAL = 0, // 0:CPU使用XTAL时钟，BK7259默认外部晶振为26M

    - 1. PM_CPU_FRQ_60M, // 1:CPU0:60M,BUS:60M

    - 2. PM_CPU_FRQ_80M, // 2:CPU0:80M,BUS:80M

    - 3. PM_CPU_FRQ_120M, // 3:CPU0:120M,BUS:120M

    - 4. PM_CPU_FRQ_160M, // 4:CPU0:160M,BUS:160M

    - 5. PM_CPU_FRQ_240M, // 5:CPU0:240M,BUS:240M

    - 6. PM_CPU_FRQ_HIGHEST, // 6:使用当前配置的最高主频，具体值由CONFIG_PM_CPU_FRQ_HIGHEST决定

    - 7. PM_CPU_FRQ_DEFAULT // 默认主频，由PM模块控制


## 动态投CPU主频的接口

> - bk_err_t bk_pm_module_vote_cpu_freq(pm_dev_id_e module,pm_cpu_freq_e cpu_freq);
>   :   - module：模块名字（选择一个使用的模块，如果自己新的模块，可以添加）
>       - cpu_freq：需要投的主频


## 获取当前投的最高CPU主频的接口

pm_cpu_freq_e bk_pm_current_max_cpu_freq_get()


## 示例：参考以下步骤1和步骤2

> - 步骤1： DISP模块投160M:
>   - bk_pm_module_vote_cpu_freq(PM_DEV_ID_DISP, PM_CPU_FRQ_160M);
> - 步骤2： DISP模块使用完高平后，把自己的模块主频恢复默认：
>   - bk_pm_module_vote_cpu_freq(PM_DEV_ID_DISP, PM_CPU_FRQ_DEFAULT);

备注

投频使用的dev_id和使用完之后的dev_id需要一样，不然会引起错误。使用前可以搜索，确认DEV_ID没有被其他业务占用。应用程序如不关心具体最高频点，可以投 `PM_CPU_FRQ_HIGHEST`；需要恢复默认时投 `PM_CPU_FRQ_DEFAULT`。

