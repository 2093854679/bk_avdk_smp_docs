# USB



## 1 功能概述

USB demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [USB 开发指南](../../developer-guide/peripheral/bk_usb.md "../../developer-guide/peripheral/bk_usb.md")。

API 参考见 [USB API](../../api-reference/peripheral/bk_usb.md "../../api-reference/peripheral/bk_usb.md")。


## 2 代码路径

> - demo 路径：
>   :   `ap/components/bk_cli/cli_usb.c`
> - 驱动源码路径：
>   :   `ap/components/usb/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_USB` | USB 功能 | 依项目配置 |
| `CONFIG_CLI` | CLI 支持 | 依项目配置 |


## 4 CLI 命令简介

使能 `CONFIG_USB` 后，通过 `usb` 相关命令测试 USB Host/Device 功能（具体子命令取决于工程 USB 模式配置）。

备注

具体子命令以固件 `help` 输出为准。
