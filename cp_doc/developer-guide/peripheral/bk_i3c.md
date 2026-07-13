# I3C 使用指南



## 概述

I3C（Improved I3C）在 I2C 基础上扩展，BK7259 CP 提供 Master/Slave 驱动，支持 SDR/HDR 等模式。

> - API 参考：[I3C](../../api-reference/peripheral/bk_i3c.md "../../api-reference/peripheral/bk_i3c.md")


## 相关代码路径

> - 头文件：`middleware/driver/i3c/i3c_master.h`、`i3c_slave.h`
> - 驱动实现：`middleware/driver/i3c/`
> - Kconfig：`CONFIG_I3C`
