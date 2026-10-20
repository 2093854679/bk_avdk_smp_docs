---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# I2C


BK7259 CP 侧支持 2 路 I2C（`include/soc/bk7259/i2c_cap.h`）。

备注

CP 公共头文件树中 I2C API 与 AP 侧 `include/driver/i2c.h` 定义一致。
驱动接口包括 `bk_i2c_driver_init`、`bk_i2c_init`、`bk_i2c_master_read`、
`bk_i2c_master_write`、`bk_i2c_memory_read`、`bk_i2c_memory_write` 等。


## 头文件


- `include/driver/i2c.h`

- `include/driver/i2c_types.h`

- `include/driver/hal/hal_i2c_types.h`
