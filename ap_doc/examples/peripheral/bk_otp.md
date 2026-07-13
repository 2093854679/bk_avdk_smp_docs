# OTP



## 1 功能概述


- OTP相关的理论介绍参考: [OTP的驱动](../../developer-guide/peripheral/bk_otp.md "../../developer-guide/peripheral/bk_otp.md")

备注


- 默认CP侧开启OTP功能，AP侧没有开启。如果用户需要使用OTP功能，需要自行手动使能OTP的配置。


## 2 代码路径

> - demo路径：
>   :   `ap\components\bk_cli\cli_otp.c`
> - 驱动源码路径：
>   :   `ap\middleware\driver\otp\otp_driver_v1_1.c`

备注


- 1.otp_driver_v1_1.c :OTP驱动实现代码
  :   - 2.cli_otp.c:OTP功能测试命令实现


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

- OTP的权限包括：可读可写/只读/不可访问 3种权限，分别对应命令参数的 0/1/2。


- OTP的状态信息包括：忙碌/错误/警告/出错/进制 5种状态，分别对应参数 1/2/4/8/16。


## 4 cli命令简介

demo运行依赖的宏配置：

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG_OTP_V1 | support OTP | `ap\middleware\soc\bk7236\bk7236.defconfig` | n |
> | CONFIG_OTP_TEST | support OTP test command | `ap\middleware\soc\bk7236\bk7236.defconfig` | n |

demo支持的命令如下表：

> | Command | Param | Description |
> | --- | --- | --- |
> | otp_apb self_test | none | self-test of OTP function in ATE mode |
> | otp_apb read_permission [item_id] | item_id: item id | Check the read permission in the OTP1 area |
> | otp_apb write_permission [item_id][permission] | item_id: item id | Update the write permissions  in the OTP1 section |
> | permission: RW/RO/NA |
> | otp_apb read [item_id][size] | item_id: item id | Read the data content in the  OTP1 area |
> | size: size of each item |
> | otp_apb write [item_id][size][data] | item_id: item id | Update the data content in the  OTP1 area |
> | size: size of each item |
> | data: need write data |
> | otp_ahb self_test | none | self-test of OTP function in ATE mode |
> | otp_ahb read_permission [item_id] | item_id: item id | Check the read permission in the OTP2 area |
> | otp_ahb write_permission [item_id][permission] | item_id: item id | Update the write permissions  in the OTP1 section |
> | permission: RW/RO/NA |
> | otp_ahb read [item_id][size] | item_id: item id | Read the data content in the  OTP1 area |
> | size: size of each item |
> | otp_ahb write [item_id][size][data] | item_id: item id | Update the data content in the  OTP1 area |
> | size: size of each item |
> | data: need write data |
