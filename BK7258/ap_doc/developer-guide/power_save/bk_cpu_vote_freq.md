---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/bk_cpu_vote_freq.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cpu"></a>

# 如何动态切换CPU主频

<a id="id1"></a>

## 切换时钟的策略

- 1.配置CPU主频统一在CPU0上(避免多核操作相同的寄存器不同步而出现异常)。
- 2.CPU选择投频最高的模块的CPU主频。
- 3.支持CPU0和CPU1调用bk\_pm\_module\_vote\_cpu\_freq()接口投频，**不支持CPU2上调用该接口**。
- 4.启动CPU1时，当前SDK默认把主频升到最高，应用程序可以不用额外再调接口投频。
- 5.CPU0或CPU1上调接口投频之后，CPU0,CPU1,CPU2的主频和BUS频率都会变化。因为他们的频率是联动的，不是独立的。

<a id="id2"></a>

## 支持配置的CPU主频

投频后CPU和BUS的频率对应关系：
:   - 0. PM\_CPU\_FRQ\_26M \= 0, // 0:CPU1:26M,CPU0:26M,BUS:26M
    - 1. PM\_CPU\_FRQ\_60M, // 1:CPU1:60M,CPU0:60M,BUS:60M
    - 2. PM\_CPU\_FRQ\_80M, // 2:CPU1:80M,CPU0:80M,BUS:80M
    - 3. PM\_CPU\_FRQ\_120M, // 3:CPU1:120M,CPU0:120M,BUS:120M
    - 4. PM\_CPU\_FRQ\_240M, // 4:CPU1:240M,CPU0:240m,BUS:240M
    - 5. PM\_CPU\_FRQ\_320M, // 5:CPU1:320M,CPU0:160M,BUS:160M
    - 6. PM\_CPU\_FRQ\_480M, // 6:CPU1:480M,CPU0:240M,BUS:240M
    - 7. PM\_CPU\_FRQ\_DEFAULT // default cpu frequency which control by pm module

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

> - 步骤1： DISP模块投320M:
>   \- bk\_pm\_module\_vote\_cpu\_freq(PM\_DEV\_ID\_DISP, PM\_CPU\_FRQ\_320M);
> - 步骤2： DISP模块使用完高平后，把自己的模块主频恢复默认：
>   \- bk\_pm\_module\_vote\_cpu\_freq(PM\_DEV\_ID\_DISP, PM\_CPU\_FRQ\_DEFAULT);

备注

投频使用的dev\_id和使用完之后的dev\_id需要一样，不然会引起错误。使用前可以搜索,确认DEV\_ID是其他模块没有其他业务使用
