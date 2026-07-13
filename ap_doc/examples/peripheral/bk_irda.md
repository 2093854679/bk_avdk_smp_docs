# IRDA



## 1 功能概述

IRDA demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [IRDA 开发指南](../../developer-guide/peripheral/bk_irda.md "../../developer-guide/peripheral/bk_irda.md")。

API 参考见 [IRDA API](../../api-reference/peripheral/bk_irda.md "../../api-reference/peripheral/bk_irda.md")。


## 2 代码路径

> - demo 路径：
>   :   `ap/middleware/driver/irda/irda_test.c`
> - 驱动源码路径：
>   :   `ap/middleware/driver/irda/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_IRDA` | IRDA 驱动 | 依项目配置 |
| `CONFIG_IRDA_TEST` | IRDA CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 `CONFIG_IRDA_TEST` 后，使用 `irda` 命令测试红外收发。

备注

具体子命令以固件 `help` 输出为准。
