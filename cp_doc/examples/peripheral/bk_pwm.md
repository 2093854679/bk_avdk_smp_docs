# PWM



## 1 功能概述

PWM demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [PWM 开发指南](../../developer-guide/peripheral/bk_pwm.md "../../developer-guide/peripheral/bk_pwm.md")。

API 参考见 [PWM API](../../api-reference/peripheral/bk_pwm.md "../../api-reference/peripheral/bk_pwm.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/pwm/pwm_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/pwm/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_PWM` | PWM 驱动 | 依项目配置 |
| `CONFIG_PWM_TEST` | PWM CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 `CONFIG_PWM_TEST` 后，使用 `pwm` 命令测试 PWM 输出。

备注

具体子命令以固件 `help` 输出为准。
