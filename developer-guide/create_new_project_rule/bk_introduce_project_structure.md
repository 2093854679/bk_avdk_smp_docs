---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/create_new_project_rule/bk_introduce_project_structure.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 工程目录结构简介

<a id="id2"></a>

## 新建工程目录结构

新建工程的目录结构如下：以bk7259的test/platform工程为例;

> <a id="id3"></a>
> ![project](../../../_assets/729c5c7ee4e3720334d7-project_struct.png)
>
>
> 图1 project\_struct
>
> - bk\_package.json是用于最后的固件打包，其中的数值在编译时根据分区表自动生成,路径在： `build/bk7259/platform/partitions/bk_package.json`；
> - 新建工程的ap\_main.c中的main函数中需包含bk\_init();已确保响应基本的命令；

## 模块导航

- [快速入门](../../get-started.md)
- [开发者指南](../../developer-guide.md)
- [AP(SMP)+CP架构](../architecture.md)
- [系统启动流程](../system_boot.md)
- [音频](../audio.md)
- [配置工具](../config_tools.md)
- [内存资源](../memory_resource.md)
- [中断管理](../interrupt.md)
- [多核通讯](../multicore_communication.md)
- [外设资源](../peripheral_resource.md)
- [构建系统](../build_config.md)
- [新建工程介绍](../create_new_project_rule.md)
- [分区表的配置简介](bk_configure_partition_Table.md)
- [修改分区简介](bk_modify_new_partition.md)
