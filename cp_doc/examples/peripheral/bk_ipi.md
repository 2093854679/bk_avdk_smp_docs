# IPI



## 1 功能概述

IPI demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [IPI 开发指南](../../developer-guide/peripheral/bk_ipi.md "../../developer-guide/peripheral/bk_ipi.md")。

API 参考见 [IPI API](../../api-reference/peripheral/bk_ipi.md "../../api-reference/peripheral/bk_ipi.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/ipi/ipi_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/ipi/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_IPI` | IPI 驱动 | 依项目配置 |
| `CONFIG_IPI_TEST` | IPI CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 `CONFIG_IPI_TEST` 后，使用 `ipi` 命令验证核间中断。

备注

具体子命令以固件 `help` 输出为准。
