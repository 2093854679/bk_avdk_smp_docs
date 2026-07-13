# Calendar



## 1 功能概述

Calendar demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [Calendar 开发指南](../../developer-guide/peripheral/bk_calendar.md "../../developer-guide/peripheral/bk_calendar.md")。

API 参考见 [Calendar API](../../api-reference/peripheral/bk_calendar.md "../../api-reference/peripheral/bk_calendar.md")。


## 2 代码路径

> - demo 路径：
>   :   `ap/components/bk_cli/cli_calendar.c`
> - 驱动源码路径：
>   :   `ap/middleware/driver/calendar/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_CALENDAR` | Calendar 驱动 | 依项目配置 |
| `CONFIG_CLI` | CLI 支持 | 依项目配置 |


## 4 CLI 命令简介

使能 `CONFIG_CALENDAR` 后，使用 `calendar_driver init` 与 `calendar get_time_us` 读取日历时间。

备注

具体子命令以固件 `help` 输出为准。
