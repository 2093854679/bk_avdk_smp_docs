# OTP



## 1 功能概述

OTP demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [OTP 开发指南](../../developer-guide/peripheral/bk_otp.md "../../developer-guide/peripheral/bk_otp.md")。

API 参考见 [OTP API](../../api-reference/peripheral/bk_otp.md "../../api-reference/peripheral/bk_otp.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/components/bk_cli/cli_otp.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/otp/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_OTP` | OTP 驱动 | 依项目配置 |
| `CONFIG_CLI` | CLI 支持 | 依项目配置 |


## 4 CLI 命令简介

使能 OTP 后，使用 `otp_apb`、`otp_ahb` 命令读写 OTP 区域。

备注

具体子命令以固件 `help` 输出为准。
