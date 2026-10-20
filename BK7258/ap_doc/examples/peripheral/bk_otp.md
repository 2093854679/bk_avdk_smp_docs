---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_otp.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="otp"></a>

# OTP

<a id="id1"></a>

## 1 功能概述

- OTP相关的理论介绍参考: [OTP的驱动](../../developer-guide/peripheral/bk_otp.md)

备注

- 默认CP侧开启OTP功能，AP侧没有开启。如果用户需要使用OTP功能，需要自行手动使能OTP的配置。

<a id="id3"></a>

## 2 代码路径

> - demo路径：
>   :   `ap\components\bk_cli\cli_otp.c`
> - 驱动源码路径：
>   :   `ap\middleware\driver\otp\otp_driver_v1_1.c`

备注

- 1.otp\_driver\_v1\_1.c :OTP驱动实现代码
  :   - 2.cli\_otp.c:OTP功能测试命令实现

<a id="id4"></a>

## 3 OTP 重要数据结构

```
typedef enum{
        OTP_READ_WRITE = 0,
        OTP_READ_ONLY,
        OTP_NO_ACCESS,
} otp_privilege_t;

typedef enum{
        OTP_BUSY = 0x1,
        OTP_ERROR = 0x2,
        OTP_WARNING = 0x4,
        OTP_WRONG = 0x8,
        OTP_FORBID = 0x10,
} otp_status_t;
```

**说明：**
\- OTP的权限包括：可读可写/只读/不可访问 3种权限，分别对应命令参数的 0/1/2。

- OTP的状态信息包括：忙碌/错误/警告/出错/进制 5种状态，分别对应参数 1/2/4/8/16。

<a id="cli"></a>

## 4 cli命令简介

demo运行依赖的宏配置：

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG\_OTP\_V1 | support OTP | `ap\middleware\soc\bk7236\bk7236.defconfig` | n |
> | CONFIG\_OTP\_TEST | support OTP test command | `ap\middleware\soc\bk7236\bk7236.defconfig` | n |

demo支持的命令如下表：

> | Command | Param | Description |
> | --- | --- | --- |
> | otp\_apb self\_test | none | self-test of OTP function in ATE mode |
> | otp\_apb read\_permission \[item\_id\] | item\_id: item id | Check the read permission in the OTP1 area |
> | otp\_apb write\_permission \[item\_id\]\[permission\] | item\_id: item id | Update the write permissions  in the OTP1 section |
> | permission: RW/RO/NA |
> | otp\_apb read \[item\_id\]\[size\] | item\_id: item id | Read the data content in the  OTP1 area |
> | size: size of each item |
> | otp\_apb write \[item\_id\]\[size\]\[data\] | item\_id: item id | Update the data content in the  OTP1 area |
> | size: size of each item |
> | data: need write data |
> | otp\_ahb self\_test | none | self-test of OTP function in ATE mode |
> | otp\_ahb read\_permission \[item\_id\] | item\_id: item id | Check the read permission in the OTP2 area |
> | otp\_ahb write\_permission \[item\_id\]\[permission\] | item\_id: item id | Update the write permissions  in the OTP1 section |
> | permission: RW/RO/NA |
> | otp\_ahb read \[item\_id\]\[size\] | item\_id: item id | Read the data content in the  OTP1 area |
> | size: size of each item |
> | otp\_ahb write \[item\_id\]\[size\]\[data\] | item\_id: item id | Update the data content in the  OTP1 area |
> | size: size of each item |
> | data: need write data |
