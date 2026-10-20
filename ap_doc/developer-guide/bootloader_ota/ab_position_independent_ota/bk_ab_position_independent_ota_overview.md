---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# AB分区位置无关OTA介绍



## 一、概述

> - AB分区位置无关方案是指将程序镜像存放在bootloader分区之后的flash的任何位置，程序均可以运行起来。假设存在两个执行区（A区和B区），当程序运行在A区时，通过OTA将升级镜像成功下载到B区之后并进行reboot；在bootloader里面通过设置flash相关控制寄存器bit位来决定执行哪个区，若该bit位值1，则程序将运行到B区；若该bit位值0，则程序将运行到A区。AB分区对应的flash视角、cpu视角分布如下图1所示（仅包含Bootloader、app（A/B）等三个分区，user以及RF、Net未列出，请知悉）。

![ab_flash_cpu_partition](../../../_images/ab_flash_cpu_partition.png)

图1 flash视角&cpu视角的分区
