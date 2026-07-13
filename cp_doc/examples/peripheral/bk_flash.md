# FLASH



## 1 功能概述

FLASH demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [FLASH 开发指南](../../developer-guide/peripheral/bk_flash.md "../../developer-guide/peripheral/bk_flash.md")。

API 参考见 [FLASH API](../../api-reference/peripheral/bk_flash.md "../../api-reference/peripheral/bk_flash.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/flash/flash_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/flash/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_FLASH` | Flash 驱动 | 依项目配置 |
| `CONFIG_FLASH_TEST` | Flash CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 Flash 测试配置后，使用 `flash` 或 `flash_test` 命令验证 Flash 读写擦除。

备注

具体子命令以固件 `help` 输出为准。
