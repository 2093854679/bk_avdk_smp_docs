# RAM资源分区配置


备注

本节旨在介绍如何为工程配置RAM资源


## RAM Regions配置表

RAM Regions配置表为 csv 文件，以下为一个配置示例

| #Name | Type | Offset | Size |
| --- | --- | --- | --- |
| AP_SPINLOCK | SRAM | 0x28000000 | 0x010000 |
| AP_RAM | SRAM |  | 0x054000 |
| CP_RAM | SRAM |  | 0x03b800 |
| SWAP | SRAM |  | 0x000800 |
| PSRAM_MEM_SLAB_USER | PSRAM | 0x60000000 | 0x019000 |
| PSRAM_MEM_SLAB_AUDIO | PSRAM |  | 0x019000 |
| PSRAM_MEM_SLAB_ENCODE | PSRAM |  | 0x15E000 |
| PSRAM_MEM_SLAB_DISPLAY | PSRAM |  | 0x570000 |
| CP_PSRAM_HEAP | PSRAM |  | 0x020000 |
| AP_PSRAM_HEAP | PSRAM |  | 0x0a0000 |
| AP_PSRAM_SECTION | PSRAM |  | 0x040000 |

在自动分区表中，不可修改SRAM的基地址和大小，不可修改PSRAM的基地址，但可根据实际情况配置PSRAM的大小，如下:


```
PSRAM_CAPCAITY_SIZE=8M

```

分区表固定为六列：

> - `Name` - 必选项，表示分区名字。
>
>   - **分区名必须唯一**。构建系统会依据分区名字来生成一组宏，只有分区名字唯一才能确保生成宏不会重复定义。
> - `Type` - 必选项。可配置为SRAM或PSRAM时，表示分区所属RAM类型。
> - `Offset` - 可选项。表示分区的物理偏移地址，表中第一项必须填写，后续项缺省时，偏移地址为上一项结束地址。
> - `Size` - 必选项。表示分区大小。

若有修改SRAM或PSRAM分区的需求，可修改ram分区表 ram_regions.csv：

> - 基于自动化分区CSV表 partitions/bk7259/ram_regions.csv 进行分区信息修改
>
>   - RAM分区的地址空间需要在有效范围内
> - 修改分区后 建议使用make clean清理编译缓存

编译后在build目录下生成ram_regions.h头文件，所有的.c文件都会默认包含这个文件，在开发过程中默认可直接使用此头文件定义的宏。
编译时将会生成相关的ADDR宏定义和SIZE宏定义，如AP_SPINLOCK分区将会生成 `CONFIG_AP_SPINLOCK_ADDR` 和 `CONFIG_AP_SPINLOCK_SIZE` 宏定义。

备注

当出现如下编译log时，表示出现RAM分区配置出错，出现分区地址重叠的情况:

> RuntimeError: RAM regions config overlaps
