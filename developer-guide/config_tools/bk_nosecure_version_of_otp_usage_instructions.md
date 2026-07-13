# 非安全版本OTP使用介绍



## OTP


### 一、概述

OTP的详细概述，详情请参考 [OTP/EFUSE配置](bk_config_otp_efuse.md#bk-config-otp-efuse "bk_config_otp_efuse.md#bk-config-otp-efuse")。

备注

其中，客户可使用的OTP区域仅有OTP2的存储空间，且操作存储地址区间是[0x4B010600—-0x4B010C00]，大小是1.5k字节空间。


#### OTP2的使用布局

![8](../_images/otp2_use_region.png)


#### OTP2 Side

OTP2:可读可编程的OTP2区域，0x000~0x2FF被分为767个小分区。其存储地址区间是[0x4B010000—-0x4B010C00]每个分区都可以通过改变LOCK OTP2 CELL来更改权限：读写->只读->不可访问。

重要

其中，前1.5k字节大小空间已被BEKEN内部使用，其存储地址区间是[0x4B010000—-0x4B010600],客户不予使用; 客户可操作的存储地址区间是[0x4B010600—-0x4B010C00]，大小是1.5k字节空间。


### 二、Otp2的驱动使用介绍

> 参考 [OTP的驱动使用介绍](../../ap_doc/developer-guide/peripheral/bk_otp.md "../../ap_doc/developer-guide/peripheral/bk_otp.md")
