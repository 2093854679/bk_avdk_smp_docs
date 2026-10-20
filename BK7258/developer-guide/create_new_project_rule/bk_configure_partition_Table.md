---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7258/zh_CN/v3.1.1/developer-guide/create_new_project_rule/bk_configure_partition_Table.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: SMP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="project"></a>

# 新建project规则简介

备注

创建新的project规则主要分为以下几个部分，以bk7258的test/platform工程为例，将详细介绍如何新建工程。

- 1、分区表的配置；
- 2、config文件中配置宏的修改；

<a id="id1"></a>

## 分区表的配置

分区表的配置为CSV文件，以bk7258的test/platform工程为例，auto\_partitions.csv其格式如下：

> <a id="id2"></a>
> ![partition_layout](../../../../_assets/6e37f799e8ed2e624896-partition_layout.png)
>
>
> 图1 partition\_layout
>
> - `Name` \- 分区表命名为：auto\_partitions.csv；分区表固定为6列，其中Name列为必选项且须唯一，表示分区的名字；
>
>   - 构建时会根据分区的名字来生成唯一的宏定义，代码中会操作该宏定义来访问相关的分区；
>   - 编译生成的二进制文件名，也是根据该分区名字来命名，如primary\_bootloader,则二进制文件名为bootloader.bin，primary\_cp\_app则为app.bin,
>   - 打包的时候，也是根据分区的名字更新bk\_package.json文件来进行打包。
>   - 保留分区，保留分区为 Armino 已有特定用途的分区：
>
>     - primary\_bootloader \- Type被配置为code，对应构建系统编译出来路径是： `build/bk7258/platform/package/tmp/bootloader.binc`，Size为bootloader.bin的实际大小的34/32倍
>     - primary\_cp\_app \- Type被配置为code，对应构建系统编译出来路径是： `build/bk7258/platform/bk7258/app.bin`, Size为app.bin的实际大小的34/32倍
>     - primary\_ap\_app \- Type被配置为code，对应构建系统编译出来路径是： `build/bk7258/platform/bk7258_ap/app.bin`， Size为app.bin的实际大小的34/32倍
>     - ota \- Armino 中特有分区，ota会用到这个分区，当不需要ota功能时，该分区Size可以保留配置为4K
>     - usr\_config \- Armino 中特有分区，文件系统会用到这个分区，该分区Size可以以4K为单位适当增减
>     - easyflash \- Armino 中特有分区，为cp侧easyflash使用， 其Size和Offset固定不可自定义变更
>     - easyflash\_ab \- Armino 中特有分区，为ap侧easyflash使用,其Size和Offset固定不可自定义变更
>     - rf\_firmware，net\_param \- Armino 中特有分区，RF 校准，Wi-Fi/TCPIP 会用到这两个分区。Size和Offset固定不可自定义变更
> - `Offset` \- 为可选项，代表放置在flash中的物理偏移位置；若没写，则默认会衔接在前一个分区后面;
> - `Size` \- 必选项。为必选项，代表分区的物理大小，单位时k/K(bytes)，对于data类型区域，必须要4K对齐，对于code区域，需要68k对齐；
> - `Type` \- 必选项。代表区域的类型，code:代表可执行代码的区域（68K对齐）；data:代表存放数据区;
> - `Read` \- 可选项。代码该区域的可读权限，如不配置的话，默认是FALSE; 应该配置成TRUE，代表可读；
> - `Write` \- 可选项。分代表该区域的可写权限，一般来说，对于code区域，应该配置成FLASE(避免该区域被误操作)，data区域，应该配置成TRUE;
> - 所有分区的size累加不能超过flash的大小，目前BK7258的大小为8M/bytes.
