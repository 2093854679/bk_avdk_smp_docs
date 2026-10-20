---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/create_new_project_rule/bk_modify_new_partition.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 修改分区简介

<a id="id2"></a>

## 修改分区

> - 1） 建议从usr\_config和easyflash分区之间插入新增分区；
> - 2） name不可和已有的分区重名;
> - 3） 需要的Size建议通过缩减user\_config分区Size获得，所有分区的Size总和不得超过所用flash的实际Size；
> - 4） 在sdk默认分区csv表中新增test\_part分区示例如下。
>
> <a id="id3"></a>
> ![add_partition](../../../_assets/989d3ade40543954944c-add_partition.png)
>
>
> 图7 add\_partition
>
> - 5） 看新增分区是否生效，可以在\`\`partitions\_gen.h\`\`中查看是否有该分区。
>
> <a id="id4"></a>
> ![new_part1](../../../_assets/f71c4135c6e921335acf-new_part1.png)
>
>
> 图9 partitions\_csv
>
> -6) 新增分区之后，若想在代码区调用该分区，如test\_part这个分区 ，
> 则使用BK\_PARTITION\_TEST\_PART 这个宏定义即可，定义在 `partitions_gen.h` 中，通过引用 `<driver/flash_partition.h>`
> 即可访问该宏。
>
> -7) 分区修改之后，需要先执行make clean;

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
- [工程目录结构简介](bk_introduce_project_structure.md)
