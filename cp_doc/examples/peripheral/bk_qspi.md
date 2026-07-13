# QSPI



## 1 功能概述

QSPI demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [QSPI 开发指南](../../developer-guide/peripheral/bk_qspi.md "../../developer-guide/peripheral/bk_qspi.md")。

API 参考见 [QSPI API](../../api-reference/peripheral/bk_qspi.md "../../api-reference/peripheral/bk_qspi.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/qspi/qspi_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/qspi/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_QSPI` | QSPI 驱动 | 依项目配置 |
| `CONFIG_QSPI_TEST` | QSPI CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 QSPI 测试配置后，使用 `qspi` 命令验证 QSPI 读写。

备注

具体子命令以固件 `help` 输出为准。
