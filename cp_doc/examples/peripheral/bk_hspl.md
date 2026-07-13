# HSPL



## 1 功能概述

HSPL demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [HSPL 开发指南](../../developer-guide/peripheral/bk_hspl.md "../../developer-guide/peripheral/bk_hspl.md")。

API 参考见 [HSPL API](../../api-reference/peripheral/bk_hspl.md "../../api-reference/peripheral/bk_hspl.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/hspl/hspl_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/hspl/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_HSPL` | HSPL 驱动 | 依项目配置 |
| `CONFIG_HSPL_TEST` | HSPL CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 `CONFIG_HSPL_TEST` 后，使用 `hspl` 命令验证硬件锁与资源锁。

备注

具体子命令以固件 `help` 输出为准。
