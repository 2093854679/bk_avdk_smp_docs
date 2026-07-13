# DMA



## 1 功能概述

DMA demo 通过 CLI 命令验证驱动基础功能。

驱动说明见 [DMA 开发指南](../../developer-guide/peripheral/bk_dma.md "../../developer-guide/peripheral/bk_dma.md")。

API 参考见 [DMA API](../../api-reference/peripheral/bk_dma.md "../../api-reference/peripheral/bk_dma.md")。


## 2 代码路径

> - demo 路径：
>   :   `cp/middleware/driver/general_dma/dma_test.c`
> - 驱动源码路径：
>   :   `cp/middleware/driver/general_dma/`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_GENERAL_DMA` | DMA 驱动 | 依项目配置 |
| `CONFIG_DMA_TEST` | DMA CLI 测试 | 依项目配置 |


## 4 CLI 命令简介

使能 DMA 测试配置后，使用 `dma` 命令验证内存拷贝、链表传输等。

备注

具体子命令以固件 `help` 输出为准。
