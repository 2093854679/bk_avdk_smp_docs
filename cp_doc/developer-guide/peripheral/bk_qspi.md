---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# QSPI 使用指南



## 概述

QSPI 作为 Master 访问 Flash、PSRAM 等外设，支持间接模式与内存映射模式。BK7259 CP 侧提供 QSPI 控制器驱动。

> - API 参考：[QSPI](../../api-reference/peripheral/bk_qspi.md "../../api-reference/peripheral/bk_qspi.md")


## 相关代码路径

> - API 头文件：`include/driver/qspi.h`、`include/driver/qspi_psram.h`
> - 驱动实现：`middleware/driver/qspi/`
