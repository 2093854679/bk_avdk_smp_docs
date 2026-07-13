# CKMN



## 1 功能概述

CKMN demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [CKMN 开发指南](../../developer-guide/peripheral/bk_ckmn.md "../../developer-guide/peripheral/bk_ckmn.md")。

API 参考见 [CKMN API](../../api-reference/peripheral/bk_ckmn.md "../../api-reference/peripheral/bk_ckmn.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/ckmn/ckmn_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/ckmn/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_CKMN` | CKMN 驱动 | 依项目配置 |
| `CONFIG_CKMN_TEST` | CKMN CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 CKMN 测试配置后，使用 `ckmn` 命令验证时钟监测。

备注

具体子命令以固件 `help` 输出为准。
