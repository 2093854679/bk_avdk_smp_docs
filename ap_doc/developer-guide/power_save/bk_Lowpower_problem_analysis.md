---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_Lowpower_problem_analysis.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap"></a>

# AP低功耗问题分析

<a id="id1"></a>

## 一、获取AP低功耗调试信息

AP启动并且串口命令可用时，发送以下命令：

```
ap_cmd pm_debug 8
```

该命令用于输出AP侧多媒体电源域投票、CPU频率投票、实际CPU频率、VDDDIG电压以及电源域硬件状态。

典型日志如下：

```
ap_cmd pm_debug 8

$ap0:pm:D(15862):pm video_post,h26e,isp,npu:0x0 0x0 0x0 0x0

$ap0:pm:I(15864):pm vote freq:50(DEFAULT),1(80M)
ap0:D(15864):Cur freq: AP:(160/2)M,VDDDIG:0.950000V
ap0:D(15864):AP_Freq_reg:0x100004
ap0:D(15865):AP power: VIDEO_POST:OFF, H26E:OFF, ISP:OFF, NPU:OFF
```

<a id="id2"></a>

## 二、日志解析

<a id="id3"></a>

### 1\. 多媒体电源域投票状态

```
pm video_post,h26e,isp,npu:0x0 0x0 0x0 0x0
```

四个值依次表示 `VIDEO_POST`、`H26E`、`ISP` 和 `NPU` 电源域的模块投票状态。

- 值为 `0x0`：当前没有模块阻止该电源域下电。
- 值非 `0x0`：对应bit仍有模块使用该电源域，电源域不能下电。命令会继续打印 `not PD` 和对应的模块名称，可根据模块名称检查业务是否已释放电源投票。

该行反映的是软件投票状态，不等同于电源域硬件已经下电。实际硬件状态应结合后面的 `AP power` 日志确认。

<a id="cpu"></a>

### 2\. CPU频率投票

```
pm vote freq:50(DEFAULT),1(80M)
```

- `50(DEFAULT)`：当前最高CPU频率投票来自 `PM_DEV_ID_DEFAULT` 模块，其设备ID为50。
- `1(80M)`：投票频点为 `PM_CPU_FRQ_80M`，枚举值为1，对应AP CPU目标频率80 MHz。

如果该行显示的模块或频率高于预期，应检查对应模块是否在业务结束后使用相同的设备ID恢复了默认频率投票。

<a id="apcpuvdddig"></a>

### 3\. AP实际CPU频率和VDDDIG电压

```
Cur freq: AP:(160/2)M,VDDDIG:0.950000V
```

- `160` 表示当前AP CPU时钟源频率为160 MHz。
- `/2` 表示时钟分频系数为2。
- 实际AP CPU频率为 `160 / 2 = 80 MHz`，与80 MHz投票一致。
- `VDDDIG:0.950000V` 表示当前AP数字核心电压为0.95 V。

<a id="id4"></a>

### 4\. AP频率寄存器

```
AP_Freq_reg:0x100004
```

该值为AP侧 `SYS_AHBP_REG8` 寄存器原始值。与CPU频率相关的字段为：

- bit\[1:0\] `cksel_core`：值为0，选择160 MHz时钟源。
- bit\[3:2\] `ckdiv_core`：值为1，实际分频系数为 `1 + 1 = 2`。

因此该寄存器对应的实际AP CPU频率为80 MHz。其余bit为总线或外设时钟配置，不应只根据CPU频率字段判断。

<a id="id5"></a>

### 5\. AP多媒体电源域硬件状态

```
AP power: VIDEO_POST:OFF, H26E:OFF, ISP:OFF, NPU:OFF
```

该行直接读取AP侧电源控制寄存器，显示四个多媒体电源域的实际硬件状态：

- `ON`：电源域处于上电状态。
- `OFF`：电源域处于下电状态。

示例中四个电源域均为 `OFF`，与软件投票值均为 `0x0` 的预期一致。

<a id="id6"></a>

## 三、常见异常判断

- 投票状态非 `0x0` 且硬件状态为 `ON`：仍有业务模块持有电源投票。根据随后打印的模块名称检查对应业务，并在业务结束后释放投票。
- 投票状态为 `0x0`，但硬件状态仍为 `ON`：软件已经允许下电，但硬件尚未下电。检查电源控制流程、模块时钟和复位状态。
- CPU投票频率与实际频率不一致：结合 `AP_Freq_reg` 检查时钟源和分频配置，并确认切频接口是否执行成功。
- CPU频率符合预期但VDDDIG电压异常：检查切频时的电压配置和电源寄存器设置。
