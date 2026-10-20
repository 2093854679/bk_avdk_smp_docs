---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_adc.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="saradc"></a>

# SARADC

<a id="id1"></a>

## 概述

BK7259 使用 SARADC V1.2。硬件与驱动实现位于 CP；AP 侧通过 SARADC Client
（mailbox）访问同一套 `bk_adc_*` 接口，不直接操作 SARADC 寄存器。

AP 相关代码路径：

> - Client：`middleware/driver/saradc/saradc_client.c`
> - Example：`middleware/driver/saradc/saradc_example.c`

常用配置：`CONFIG_SARADC`、`CONFIG_SARADC_CLIENT`、`CONFIG_SARADC_MB`。

<a id="id2"></a>

## 工作模式

BK7259 SARADC V1.2 硬件支持以下两种模式：

> - 单步模式（`ADC_SINGLE_STEP_MODE`）：硬件 `adc_mode` 为 0。
> - 连续模式（`ADC_CONTINUOUS_MODE`）：硬件 `adc_mode` 为 1。

公共类型中保留的 `ADC_SLEEP_MODE` 和 `ADC_SOFTWARE_CONTRL_MODE` 是兼容枚举，
BK7259 V1.2 HAL 不会将这两种枚举写入硬件模式寄存器，不应作为 BK7259
可用的硬件工作模式使用。

<a id="id3"></a>

## 连续采样与中断

连续模式下，CP 侧驱动的数据处理流程如下：

> 1. 驱动选择通道、配置时钟并启动转换。
> 2. 采样结果进入硬件 FIFO。
> 3. FIFO 数据量达到中断条件后产生中断。
> 4. 中断服务程序逐个读取 FIFO 数据并写入用户请求的 `uint16_t` 缓冲区。
> 5. 收集到请求的样本数后，驱动停止转换并唤醒等待任务。

BK7259 V1.2 驱动将 FIFO 中断阈值限制为 32。该阈值表示 FIFO 的中断触发条件，
不是 FIFO 容量，也不是用户读取缓冲区的大小。单步模式固定在采集两个数据后
产生中断。

AP 侧推荐使用公共接口：

> - `bk_adc_read()`：读取当前通道采样结果（经校准换算前的原始值读取路径）
> - `bk_adc_read_raw()`：读取指定数量的原始采样结果

示例流程见 `saradc_example()`：`bk_adc_acquire` → 配置/初始化通道 →
`bk_adc_start` → `bk_adc_read` → 停止并释放资源。使用前需完成对应通道的
GPIO 映射（`bk_adc_chan_init_gpio`）。

备注

驱动级 `sadc` 系列 CLI 注册在 CP，请在 CP 串口验证。AP CLI 示例说明见
[SARADC Cli](../../examples/cli/saradc/saradc.md)。
