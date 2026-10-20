---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# 四.Bootloader镜像文件生成



- 1.直接编译生成bootloader.bin；具体编译步骤如下：


  - 1）进入bootloader代码目录下；

  - 2）make clean

  - 3）make

  - 4）在PACK目录下执行generate.bat脚本，在generate_out目录下生成bootloader.bin以及对应的bootloader_crc.bin
