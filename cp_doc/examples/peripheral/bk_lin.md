# LIN



## 1 功能概述

LIN demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [LIN 开发指南](../../developer-guide/peripheral/bk_lin.md "../../developer-guide/peripheral/bk_lin.md")。

API 参考见 [LIN API](../../api-reference/peripheral/bk_lin.md "../../api-reference/peripheral/bk_lin.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/lin/lin_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/lin/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_LIN` | LIN 驱动 | 依项目配置 |
| `CONFIG_LIN_TEST` | LIN CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 LIN 测试配置后，使用 `lin` 命令验证 LIN 总线通信。

备注

具体子命令以固件 `help` 输出为准。
