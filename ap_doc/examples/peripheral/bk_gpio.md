# GPIO



## 1 功能概述

GPIO demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [GPIO 开发指南](../../developer-guide/peripheral/bk_gpio.md "../../developer-guide/peripheral/bk_gpio.md")。

API 参考见 [GPIO API](../../api-reference/peripheral/bk_gpio.md "../../api-reference/peripheral/bk_gpio.md")。


## 2 代码路径

> - demo 路径：
>   :   `ap/middleware/driver/gpio/gpio_test.c`
> - 驱动源码路径：
>   :   `ap/middleware/driver/gpio/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_GPIO` | GPIO 驱动 | 依项目配置 |
| `CONFIG_GPIO_TEST` | GPIO CLI 测试 | 依项目配置 |
| `CONFIG_DRV_CLI_SUPPORT` | 驱动 CLI 支持 | 依项目配置 |


## 4 CLI 命令简介

使能 `CONFIG_GPIO_TEST` 与 `CONFIG_DRV_CLI_SUPPORT` 后，执行 `gpio_driver init` 初始化，再使用 `gpio`、`gpio_int` 等子命令测试输入输出与中断。

备注

具体子命令以固件 `help` 输出为准。
