# HSPL 使用指南



## 概述

HSPL（Hardware Spin Lock）是 BK7259 提供的硬件自旋锁，用于多核之间的互斥同步。芯片提供两个 HSPL 硬件实例，每个实例 16 个独立通道。

主要特性：

> - 双实例：BK_HSPL_ID_0（基址 0x45010000，CP/AP 跨核互斥）、BK_HSPL_ID_1（基址 0x480C0000，AP SMP 内部互斥）
> - 每实例 16 路通道，硬件原子加锁/解锁
> - 提供底层 channel API 与上层资源级 `bk_hspl_res_*` 封装

备注

CP 侧 `bk_hspl_res_*` 资源锁请使用 BK_HSPL_ID_0；在 CP 上调用 BK_HSPL_ID_1 相关路径可能返回 `BK_ERR_NOT_SUPPORT`。


## 驱动初始化


```
bk_hspl_driver_init();
/* 使用 bk_hspl_try_lock / bk_hspl_res_lock 等接口 */
bk_hspl_driver_deinit();

```


## 相关代码路径

> - 驱动头文件：`middleware/driver/hspl/hspl_driver.h`、`hspl_res_lock.h`
> - 驱动实现：`middleware/driver/hspl/hspl_driver.c`、`hspl_res_lock.c`
> - 测试代码：`middleware/driver/hspl/hspl_test.c`
> - Kconfig：middleware/driver/hspl/Kconfig（CONFIG_HSPL、CONFIG_HSPL_TEST）


## API 参考

详见 [HSPL](../../api-reference/peripheral/bk_hspl.md "../../api-reference/peripheral/bk_hspl.md")。
