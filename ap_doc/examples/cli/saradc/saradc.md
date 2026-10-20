---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/cli/saradc/saradc.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="saradc-cli"></a>

# SARADC Cli

<a id="id1"></a>

## 1、功能概述

> BK7259 AP 侧不直接操作 SARADC 硬件，而是通过 SARADC Client（mailbox）访问
> CP 侧驱动。AP 提供 example 代码，演示通道初始化、采样读取和电压换算。
>
> 驱动级 `sadc` 系列 CLI 注册在 CP，用于在 CP 串口验证硬件与驱动；AP 侧
> 无对应 CLI 命令。

<a id="id2"></a>

## 2、代码路径

> - AP example：`middleware/driver/saradc/saradc_example.c`
> - AP client：`middleware/driver/saradc/saradc_client.c`
> - CP CLI 测试：`cp/middleware/driver/saradc/v1_2/adc_test.c`

<a id="id3"></a>

## 3、宏配置

> AP 侧常用配置：
>
> > - `CONFIG_SARADC`：使能 SARADC
> > - `CONFIG_SARADC_CLIENT`：使能 AP SARADC Client（默认开启）
> > - `CONFIG_SARADC_MB`：使能 SARADC mailbox 通知
>
> CP 侧 CLI 测试还需使能：
>
> > - `CONFIG_DRIVER_TEST`
> > - `CONFIG_SARADC_TEST`

<a id="ap-example"></a>

## 4、AP example 入口

支持的接口如下:

> 1.saradc\_test
> :   - 功能说明
>       :   完成 GPIO 映射后调用 `saradc_example`，读取指定通道校准电压值。
>     - 接口格式
>       :   `uint16_t saradc_test(UINT8 adc_chan)`
>
>           | Param | value |
>           | --- | --- |
>           | adc\_chan | ADC channel id |
>     - 测试用例
>       :   读取 ADC 通道 3：调用 `saradc_test(3)`
>
> 2.saradc\_example
> :   - 功能说明
>       :   演示 `bk_adc_acquire` → 配置/初始化通道 → `bk_adc_start` →
>           `bk_adc_read` → 停止并释放资源的完整流程。
>     - 接口格式
>       :   `uint16_t saradc_example(UINT8 adc_chan)`

<a id="cp-cli-cp"></a>

## 5、CP CLI 命令（CP 串口）

使能 CP 侧 SARADC 测试配置后，可在 CP 串口使用以下命令：

| 命令 | 格式 | 功能 |
| --- | --- | --- |
| `sadc_driver` | `sadc_driver init|deinit` | 初始化或反初始化 SARADC 驱动 |
| `sadc` | `sadc <channel> <subcommand> [parameters]` | 配置通道、读取数据或查询校准电压 |
| `sadc_cont` | `sadc_cont start|read|stop [parameters]` | 验证连续采样 |
| `sadc_multi` | `sadc_multi config|read [channel]` | 验证多通道采样 |
| `sadc_rate` | `sadc_rate <channel> <clock>` | 验证指定采样时钟 |

例如，在 CP 串口初始化驱动并读取 ADC3 的校准电压值：

```
sadc_driver init
sadc 3 config 3 1 13000000 3 0
sadc 3 get_value
```

备注

可用子命令受固件配置影响，请以当前固件的 `help` 输出为准。
