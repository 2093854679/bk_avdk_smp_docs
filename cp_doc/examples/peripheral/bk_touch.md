# TOUCH



## 1 功能概述

TOUCH demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [TOUCH 开发指南](../../developer-guide/peripheral/bk_touch.md "../../developer-guide/peripheral/bk_touch.md")。

API 参考见 [TOUCH API](../../api-reference/peripheral/bk_touch.md "../../api-reference/peripheral/bk_touch.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/touch/touch_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/touch/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_TOUCH` | Touch 驱动 | 依项目配置 |
| `CONFIG_TOUCH_TEST` | Touch CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 `CONFIG_TOUCH_TEST` 后，使用 `touch` 命令进行触摸测试。

备注

具体子命令以固件 `help` 输出为准。
