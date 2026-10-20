---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# I3C


BK7259 CP 侧 I3C API（`middleware/driver/i3c/`），提供 Master 与 Slave 模式。


## I3C Master API


- `bk_i3c_master_init` / `bk_i3c_master_deinit`

- `bk_i3c_master_write` / `bk_i3c_master_read`

- `bk_i3c_master_devices_print`


## I3C Slave API


- `bk_i3c_slave_init` / `bk_i3c_slave_deinit`

- `bk_i3c_slave_write` / `bk_i3c_slave_read`


## 头文件


- `middleware/driver/i3c/i3c_master.h`

- `middleware/driver/i3c/i3c_slave.h`

- `middleware/driver/i3c/i3c_common.h`
