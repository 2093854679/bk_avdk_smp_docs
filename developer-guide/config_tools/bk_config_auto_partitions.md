---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/config_tools/bk_config_auto_partitions.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bk-config-auto-partitions"></a>

<a id="id1"></a>

# 自动化分区配置

备注

本节旨在介绍如何为新增工程适配自动化分区

<a id="id2"></a>

## 自动化分区配置表

自动化分区配置表为 csv 文件，以下为一个配置示例（BK7259 不在 Flash 中为 code 分区插入 CRC，占用空间即为配置的 `Size`）：

| #Name | Offset | Size | Type | Read | Write |
| --- | --- | --- | --- | --- | --- |
| primary\_bootloader |  | 64k | code | TRUE | FALSE |
| primary\_cp\_app |  | 1836k | code | TRUE | FALSE |
| primary\_ap\_app |  | 476k | code | TRUE | FALSE |
| ota |  | 1428k | data | TRUE |  |
| usr\_config |  | 136k | data | TRUE |  |
| easyflash | 0x7fc000 | 8k | data | TRUE |  |
| sys\_rf | 0x7fe000 | 4k | data | TRUE |  |
| sys\_net | 0x7ff000 | 4k | data | TRUE |  |

<a id="bk-config-partitions-table"></a>

分区表固定为六列：

> - `Name` \- 必选项，表示分区名字。
>
>   - **分区名必须唯一**。构建系统会依据分区名字来生成一组宏，只有分区名字唯一才能确保生成宏不会重复定义。
>   - binname 表示分区中放置的二进制文件名字，Type被配置为code的分区对应构建系统中生成的二进制文件。
>     例如，bootloader分区中放置的二进制文件为bootloader.bin; app分区中放置的二进制文件为app.bin。
>   - 保留分区，保留分区为 Armino 已有特定用途的分区：
>
>     - primary\_bootloader \- Type 被配置为 code，对应构建系统编译出来 bootloader.bin；Size 为 CSV 中配置的 Flash 大小（须 ≥ 实际镜像大小，4K 对齐）
>     - primary\_cp\_app \- Type 被配置为 code，对应构建系统编译出来 app.bin；Size 为配置的 Flash 大小（须 ≥ 实际镜像大小，4K 对齐）
>     - primary\_ap\_app \- Type 被配置为 code，对应构建系统编译出来 app.bin；Size 为配置的 Flash 大小（须 ≥ 实际镜像大小，4K 对齐）
>     - ota \- Armino 中特有分区，ota会用到这个分区，当不需要ota功能时，该分区Size可以保留配置为4K
>     - usr\_config \- Armino 中特有分区，文件系统会用到这个分区，该分区Size可以以4K为单位适当增减
>     - easyflash \- Armino 中特有分区，Size和Offset固定不可自定义变更
>     - sys\_rf, sys\_net \- Armino 中特有分区，RF 校准，Wi-Fi/TCPIP 会用到这两个分区。Size和Offset固定不可自定义变更
> - `Offset` \- 可选项。表示分区在 FLASH 的物理偏移量。
> - `Size` \- 必选项。表示分区大小，单位 k/K 表示 Kbytes，m/M 表示 Mbytes。data 与 code 分区均须 **4K 对齐**；code 分区 Size 须 **不小于** 实际 bin 大小。
> - `Type` \- 必选项。配置为code时，表示分区为可执行的代码区。配置为data时，表示分区为不可执行的数据区。
> - `Read` \- 可选项。分区可读权限，不配置时，表不可读。
> - `Write` \- 可选项。分区可写权限，不配置时，表不可写。

以bk7259芯片为例，参考/projects/app，工程目录结构如下

```
app
├── ap
│   ├── ap_main.c
│   ├── CMakeLists.txt
│   └── config
│       └── bk7259_ap
│           ├── defconfig
│           └── usr_gpio_cfg.h
├── app.rst
├── CMakeLists.txt
├── cp
│   ├── CMakeLists.txt
│   ├── config
│   │   └── bk7259
│   │       ├── defconfig
│   │       └── usr_gpio_cfg.h
│   └── cp_main.c
├── partitions
│   └── bk7259
│       └── auto_partitions.csv
└── pj_config.mk
```

若有修改分区的需求，修改自动分区表 auto\_partitions.csv：

> - 基于自动化分区CSV表 partitions/bk7259/auto\_partitions.csv 进行分区信息修改
>
>   - 保留分区需要遵循保留分区的修改规则
>   - 新增分区建议加在user\_config和easyflash分区之间，且需要的Size建议通过缩减user\_config分区Size获得
>   - 所有分区的Size总和不得超过所用flash的实际Size
> - 修改分区后 建议使用make clean清理编译缓存

备注

当出现如下编译log时，表示出现分区配置出错，出现分区地址重叠的情况:

> RuntimeError: partition table config overlaps
