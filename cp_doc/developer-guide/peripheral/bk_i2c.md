# I2C 使用指南



## 概述

I2C 为串行同步半双工总线，BK7259 CP 支持 2 路硬件 I2C（见 `i2c_cap.h`）。可作为 Master 或 Slave 访问外设。

> - API 参考：[I2C](../../api-reference/peripheral/bk_i2c.md "../../api-reference/peripheral/bk_i2c.md")


## 相关代码路径

> - API 头文件：`include/driver/i2c.h`，与 AP 共用定义
> - 驱动实现：middleware/driver/i2c/，按工程配置启用
