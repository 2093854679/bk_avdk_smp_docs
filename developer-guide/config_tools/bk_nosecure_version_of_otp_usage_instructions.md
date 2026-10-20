---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/config_tools/bk_nosecure_version_of_otp_usage_instructions.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="otp"></a>

<a id="bk-nosecure-version-of-otp-usage-instructions"></a>

# 非安全版本OTP使用介绍

<a id="id1"></a>

## OTP

<a id="id2"></a>

### 一、概述

OTP的详细概述，详情请参考 [OTP/EFUSE配置](bk_config_otp_efuse.md#bk-config-otp-efuse)。

备注

其中，客户可使用的OTP区域仅有OTP2的存储空间，且操作存储地址区间是\[0x4B010600—-0x4B010C00\]，大小是1.5k字节空间。

<a id="otp2"></a>

#### OTP2的使用布局

![8](../../../_assets/7a686a3d9bc92c837920-otp2_use_region.png)

<a id="otp2-side"></a>

#### OTP2 Side

OTP2:可读可编程的OTP2区域，0x000\~0x2FF被分为767个小分区。其存储地址区间是\[0x4B010000—-0x4B010C00\]每个分区都可以通过改变LOCK OTP2 CELL来更改权限：读写-\>只读-\>不可访问。

重要

其中，前1.5k字节大小空间已被BEKEN内部使用，其存储地址区间是\[0x4B010000—-0x4B010600\],客户不予使用; 客户可操作的存储地址区间是\[0x4B010600—-0x4B010C00\]，大小是1.5k字节空间。

<a id="id3"></a>

### 二、Otp2的驱动使用介绍

> 参考 [OTP的驱动使用介绍](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/ap/docs/bk7259/zh_CN/developer-guide/peripheral/bk_otp.html)

## 模块导航

- [快速入门](../../get-started.md)
- [开发者指南](../../developer-guide.md)
- [AP(SMP)+CP架构](../architecture.md)
- [系统启动流程](../system_boot.md)
- [音频](../audio.md)
- [配置工具](../config_tools.md)
- [概述](bk_config_overview.md)
- [Kconfig 配置](bk_config_kconfig.md)
- [自动化分区配置](bk_config_auto_partitions.md)
- [ram资源分区配置](bk_config_ram_regions.md)
- [OTP/Efuse 配置](bk_config_otp_efuse.md)
- [烧录工具 BKFIL](bk_tool_bkfil.md)
- [内存资源](../memory_resource.md)
- [中断管理](../interrupt.md)
- [多核通讯](../multicore_communication.md)
- [外设资源](../peripheral_resource.md)
- [构建系统](../build_config.md)
- [新建工程介绍](../create_new_project_rule.md)
