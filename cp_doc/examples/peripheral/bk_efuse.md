# EFUSE



## 1 功能概述

EFUSE demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [EFUSE 开发指南](../../developer-guide/peripheral/bk_efuse.md "../../developer-guide/peripheral/bk_efuse.md")。

API 参考见 [EFUSE API](../../api-reference/peripheral/bk_efuse.md "../../api-reference/peripheral/bk_efuse.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/efuse/efuse_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/efuse/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_EFUSE` | EFUSE 驱动 | 依项目配置 |
| `CONFIG_EFUSE_TEST` | EFUSE CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 EFUSE 测试配置后，使用 `efuse` 命令读写 eFuse。

备注

具体子命令以固件 `help` 输出为准。
