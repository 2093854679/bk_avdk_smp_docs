# SARADC



## 1 功能概述

SARADC demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [SARADC 开发指南](../../developer-guide/peripheral/bk_adc.md "../../developer-guide/peripheral/bk_adc.md")。

API 参考见 [SARADC API](../../api-reference/peripheral/bk_adc.md "../../api-reference/peripheral/bk_adc.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/saradc/v1_2/adc_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/saradc/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_SARADC` | SARADC 驱动 | 依项目配置 |
| `CONFIG_ADC_TEST` | ADC CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 ADC 测试配置后，使用 `adc` 命令读取模拟通道采样值。

备注

具体子命令以固件 `help` 输出为准。
