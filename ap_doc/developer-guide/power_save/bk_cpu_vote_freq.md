---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_cpu_vote_freq.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cpu"></a>

# 如何动态切换CPU主频

<a id="id1"></a>

## 切换时钟的策略

- 1.AP侧CPU主频由AP侧PM模块管理，与CP侧CPU主频独立配置，互不干扰。
- 2.AP侧CPU选择所有模块投票中的最高主频。
- 3.AP侧应用通过 `bk_pm_module_vote_cpu_freq()` 接口投票CPU主频。
- 4.启动AP时，当前SDK默认将AP侧CPU主频升至480M；应用程序无特殊需求时不需要额外投频。
- 5.AP侧应用可以根据业务需求动态投票不同的CPU主频，业务结束后应恢复默认投票。

<a id="id2"></a>

## 支持配置的CPU主频

投频后CPU和BUS的频率对应关系：
:   - 0. PM\_CPU\_FRQ\_XTAL \= 0, // 0:CPU使用XTAL时钟，BK7259默认外部晶振为26M
    - 1. PM\_CPU\_FRQ\_80M, // 1:AP CPU:80M,BUS:80M
    - 2. PM\_CPU\_FRQ\_120M, // 2:AP CPU:120M,BUS:120M
    - 3. PM\_CPU\_FRQ\_160M, // 3:AP CPU:160M,BUS:160M
    - 4. PM\_CPU\_FRQ\_240M, // 4:AP CPU:240M,BUS:120M
    - 5. PM\_CPU\_FRQ\_320M, // 5:AP CPU:320M,BUS:160M
    - 6. PM\_CPU\_FRQ\_480M, // 6:AP CPU:480M,BUS:240M
    - 7. PM\_CPU\_FRQ\_HIGHEST, // 7:使用当前配置的最高主频，具体值由CONFIG\_PM\_CPU\_FRQ\_HIGHEST决定
    - 8. PM\_CPU\_FRQ\_DEFAULT // 默认主频，由PM模块控制

<a id="ap"></a>

## 配置AP侧默认主频

`CONFIG_PM_AP_CPU_FRQ_DEFAUL` 宏用于控制是否在AP初始化结束时配置默认主频。将该宏配置为 `y` 后，
AP侧会通过以下代码投票 `CONFIG_PM_CPU_FRQ_DEFAULT` 所指定的默认主频：

```
#if CONFIG_PM_AP_CPU_FRQ_DEFAUL
    bk_pm_module_vote_cpu_freq(PM_DEV_ID_DEFAULT, CONFIG_PM_CPU_FRQ_DEFAULT);
#endif
```

当前BK7259 AP默认配置中，`CONFIG_PM_CPU_FRQ_DEFAULT` 的值为 `1`，对应AP默认主频80M。
该宏也可以根据业务需求配置为其他频率，具体配置值与主频的对应关系请参考
`PM_CPU_FRQ_XTAL`、`PM_CPU_FRQ_80M` 至 `PM_CPU_FRQ_480M` 的宏值定义。

<a id="id3"></a>

## 动态投CPU主频的接口

> - bk\_err\_t bk\_pm\_module\_vote\_cpu\_freq(pm\_dev\_id\_e module,pm\_cpu\_freq\_e cpu\_freq);
>   :   - module：模块名字（选择一个使用的模块，如果自己新的模块，可以添加）
>       - cpu\_freq：需要投的主频

<a id="id4"></a>

## 获取当前投的最高CPU主频的接口

pm\_cpu\_freq\_e bk\_pm\_current\_max\_cpu\_freq\_get()

<a id="id5"></a>

## 示例：参考以下步骤1和步骤2

> - 步骤1： DISP模块投160M:
>   \- bk\_pm\_module\_vote\_cpu\_freq(PM\_DEV\_ID\_DISP, PM\_CPU\_FRQ\_160M);
> - 步骤2： DISP模块使用完高平后，把自己的模块主频恢复默认：
>   \- bk\_pm\_module\_vote\_cpu\_freq(PM\_DEV\_ID\_DISP, PM\_CPU\_FRQ\_DEFAULT);

备注

投频使用的dev\_id和使用完之后的dev\_id需要一样，不然会引起错误。使用前可以搜索，确认DEV\_ID没有被其他业务占用。应用程序如不关心具体最高频点，可以投 `PM_CPU_FRQ_HIGHEST`；需要恢复默认时投 `PM_CPU_FRQ_DEFAULT`。
