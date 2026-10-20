---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_otp.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="otp"></a>

# OTP 使用指南

<a id="id1"></a>

## 概述

OTP（One-Time Programmable Memory，一次性可编程存储器）是一种只能写入一次、但可多次读取的非易失性存储器，广泛用于存储安全配置、唯一标识、工厂校准参数等不可更改的数据。

<a id="id2"></a>

## 典型特性

| 特性 | 描述 |
| --- | --- |
| 写入一次 | 每个位在写入后即被永久锁定，不可擦除或重写 |
| 掉电不丢失 | 属于非易失性存储器，断电后仍可保存数据 |
| 按位可编程 | 支持按位写入，部分芯片支持逐字节编程 |
| 高安全性 | 适用于存储加密密钥、芯片ID、MAC地址等敏感信息 |
| 访问受控 | 可设置只读区域、写保护或访问权限限制 |

<a id="id3"></a>

## OTP 特性

BK7259芯片中的OTP包含两部分，OTP1和OTP2区域，OTP1部分仅供公司内部使用，内容包括Device ID、MAC address、Public key以及其他保留区域信息。
仅OTP2中的区域提供给客户使用，且操作存储地址区间是\[0x4B010600—-0x4B010C00\]，大小是1.5k字节空间。

<a id="otp2"></a>

### OTP2的使用布局

![8](../../../../_assets/db4dd032200059d87061-otp2_use_region.png)

<a id="otp2-side"></a>

### OTP2 Side

OTP2:可读可编程的OTP2区域，0x000\~0x2FF被分为767个小分区。其存储地址区间是\[0x4B010000—-0x4B010C00\]每个分区都可以通过改变LOCK OTP2 CELL来更改权限：读写-\>只读-\>不可访问。

重要

其中，前1.5k字节大小空间已被BEKEN内部使用，其存储地址区间是\[0x4B010000—-0x4B010600\],客户不予使用; 客户可操作的存储地址区间是\[0x4B010600—-0x4B010C00\]，大小是1.5k字节空间。

<a id="id4"></a>

## 使用注意事项

- 写入后不可更改，请在写入前仔细验证数据正确性
- 建议先使用“仿真烧写模式”进行软件验证
- 写入操作通常需要一定延时（如5\~10ms烧录时间）

<a id="id5"></a>

## OTP的驱动使用介绍

<a id="id6"></a>

### OTP2中添加自定义分区信息的使用介绍

- 1）若需要在otp2中增加特定大小分区使用，只需要在 `ap/middleware/boards/bk7259_ap/csv/otp2.csv` 中添加\[id,name,size,offset,end,privilege,security\]所对应内容即可，参考见文末；
- 2）SDK里的工具会在编译的时候自动生成相关头文件，无需手动修改头文件中的内容，生成后的头文件内容如下。位于../\_build/\_otp.c

![8](../../../../_assets/c8439666d00f7ebc519e-otp_header.png)

- 3）配置好上述的配置之后，可以使用cli命令进行测试, 相关的测试代码路径是： `ap/components/bk_cli/cli_otp.c` (例如 测试命令是otp\_ahb read item size)

备注

操作写otp2某个区域之前，最好将该区域读出来确认一下，确认该otp区域是否已经被使用过。（otp原始值是0）

<a id="otp-ahb-map"></a>

### 结构体数组otp\_ahb\_map配置介绍

- 1）结构体数组otp\_ahb\_map的结构体如下：具体路径是 `ap/middleware/driver/otp/otp_driver.h`

![8](../../../../_assets/06e90d0fa2684acbca5b-otp_item.png)

备注

- name：访问区域的item\_id,后续操作该区域可根据该item\_id进行访问d\_size的大小，即所需要分配的字节大小空间；
- allocated\_size：分配的字节大小空间
- offset：相对基地址的偏移量
- privilege：设定访问区域的权限

- 2）otp2\_id\_t中存放的是name字段；工具自动生成的路径是 `../_build/_otp.h`

![8](../../../../_assets/050e59baf4b98ee653b9-otp2_id_t.png)

备注

- 以name\=OTP\_CUSTOMER\_KEY2举例介绍如何配置otp2
- 首先，在opt2.csv文件中新增id为6，按照顺序依次增加；增加自行定义的name字段，如OTP\_CUSTOMER\_KEY2；
- 其次，需要配置size的大小，即所需要分配的字节大小空间。若大小为256字节，则size为256；（十进制大小）
- offset大小等于（前一个name字段的end） （十六进制）
- 权限为OTP\_READ\_WRITE，安全为FALSE；

![8](../../../../_assets/122ad459c750c687fb58-otp2_csv.png)
