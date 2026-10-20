---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# I3C



## 1 功能概述

I3C demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [I3C 开发指南](../../developer-guide/peripheral/bk_i3c.md "../../developer-guide/peripheral/bk_i3c.md")。

API 参考见 [I3C API](../../api-reference/peripheral/bk_i3c.md "../../api-reference/peripheral/bk_i3c.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/i3c/i3c_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/i3c/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_I3C` | I3C 驱动 | 依项目配置 |
| `CONFIG_I3C_TEST` | I3C CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 I3C 测试配置后，使用 `i3c` 命令验证 I3C 总线。

备注

具体子命令以固件 `help` 输出为准。
