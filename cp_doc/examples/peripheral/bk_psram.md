# PSRAM



## 1 功能概述

PSRAM demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [PSRAM 开发指南](../../developer-guide/peripheral/bk_psram.md "../../developer-guide/peripheral/bk_psram.md")。

API 参考见 [PSRAM API](../../api-reference/peripheral/bk_psram.md "../../api-reference/peripheral/bk_psram.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/psram/psram_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/psram/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_PSRAM` | PSRAM 驱动 | 依项目配置 |
| `CONFIG_PSRAM_TEST` | PSRAM CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 PSRAM 测试配置后，使用 `psram` 命令验证 PSRAM 读写与压测。

备注

具体子命令以固件 `help` 输出为准。
