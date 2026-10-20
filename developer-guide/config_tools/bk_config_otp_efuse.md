---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/config_tools/bk_config_otp_efuse.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="otp-efuse"></a>

<a id="bk-config-otp-efuse"></a>

# OTP/EFUSE 配置

<a id="otp"></a>

## OTP

<a id="id1"></a>

### 概述

OTP模块共有三组接口,分别为系统端的AHB和APB,加密端的APB。其中系统端连接总线,而加密端通过shanhai安全引擎访问。AHB的基地址为0x42010000,APB的基地址为0x42100000。

OTP主要有三块区域,分别为OTP,OTP2,PUF区域。

- OTP有256\*32bit共8Kb存储空间,系统端权限为读写/只读/无法访问,加密端权限为读写。
- OTP2有768\*32共24Kb存储空间,系统端权限为读写/只读/无法访问,加密端没有连接OTP2的通路。
- PUF有64\*32共2Kb存储空间。前1K用于存放UID,后1K用于存放生成随机数的熵池。系统端对于UID的权限为只读或无法访问,对熵池的权限为只读/无法访问。加密端对UID的权限为只读/无法访问。PUF需要注册后才能生效。

OTP对区域的操作有四种:安全范围划分,权限管理、屏蔽和清零。

- 安全范围划分可以将区域划分为安全与非安全,系统端的非安全访问安全区域会得到被屏蔽后的全F数据。加密端不受影响。安全范围可以多次划分,但是不能划分OTP2区域。
- 权限管理可以配置每个otp8bit的权限,将访问权限从只读变为不可访问。权限管理的配置是一次性的。
- 屏蔽也可以将区域的只读权限变为不可访问,但是重新上电复位可以将屏蔽恢复。屏蔽操作也有一个锁来控制,如果置锁,则连同锁一起,将不能再更改屏蔽,但重新上电后会恢复。
- 清零操作可以将OTP和PUF区域进行清零,可以读取指示来得知某区域是否被清零,并且可以限制非安全清零操作。清零操作只可以操作OTP和PUF区域。

<a id="id2"></a>

### OTP 布局

![8](../../../_assets/595761b4ddad287eb797-otp_region.png)
<a id="ahb-side"></a>

#### AHB Side

0x000\~0x2FF OTP2:存储区2
可读可编程的OTP2区域，被分为767个小分区。每个分区都可以通过改变LOCK OTP2 CELL来更改权限：读写-\>只读-\>不可访问。

<a id="apb-side"></a>

#### APB Side

0x000\~0x100 PIF:配置PUF和OTP权限的区域
0x200\~0x240 PTR:Test Row
0x240\~0x280 PTC:Test Column
0x2A0\~0x2A4 RNG:随机数生成区域
0x2B0\~0x2B4 INT
0x2B4\~0x2C0 PMK:Mask区域
0x2C0\~0x2F4 PTM:状态表征区域
0x300\~0x400 PUF:随机数注册区域
0x400\~0x7FC OTP:主存储区

三组接口可访问的区域如上图所示，其中系统端的权限可以被NA，但是shanhai加密端不能被NA。另外，shanhai需要使用OTP部分的信息作为自己的配置。但是shanhai不支持偏移地址，而OTP的存储区是有0x0400的偏移地址的。所以在设计上shanhai访问OTP的地址进行了相应的偏移，偏移量为0x500。

<a id="id3"></a>

#### OTP 硬件区

1.0x400\~0x45F: 存放memcheck结果
2.0x460\~0x47F: 存放flash\_key
3.0x480\~0x47F: 预留给硬件使用

<a id="id4"></a>

#### OTP 软件区

![8](../../../_assets/da359ec2b31447748c13-otp_software.png)

<a id="bl1-otp"></a>

### BL1 OTP 项

需要使能efuse的第3bit，从而进行安全启动(该操作不可回退！一旦启用安全启动就不能关闭，请谨慎。)

<a id="bl2-otp"></a>

### BL2 OTP 项

**TODO**

<a id="flash-aes-key"></a>

### FLASH AES KEY

用于 FLASH AES 加密的密钥存放在 OTP 安全数据区域，可通过 BKFIL 的 security data 区域进行配置，具体方法参见后文『配置 FLASH AES KEY』小节。

<a id="id5"></a>

### 其他 OTP 项

<a id="efuse"></a>

## EFUSE

EFUSE 共有 4x8 共 32 Bits, 其中每个 Bit 的含义不同。可以通过总 BKFIL 配置。

| Bit | 名称 | 说明 |
| --- | --- | --- |
| 0 | reserved | 保留位。 |
| 1 | bl1 info log disable | 0: 使能 BL1 安全启动普通日志；1: 关闭 BL1 安全启动普通日志。 |
| 2 | fast boot disable | 0: Deep Sleep 唤醒执行快速启动；1: Deep Sleep 唤醒执行完整安全启动。 |
| 3 | disable download \+ enable secure boot | 0: 不禁用下载；1: 禁用下载并使能安全启动，为安全启动总开关（开启验签、关闭下载）。 |
| 4 | sb clock select | 0: 安全启动使用 XTAL 时钟；1: 使能 PLL。 |
| 5 | random delay enable | 0: 关闭随机延时；1: 使能随机延时。 |
| 6 | power on fast boot | 0: 上电时跳过安全启动；1: 上电时不跳过安全启动。 |
| 7 | bl1 error log disable | 0: 使能 BL1 安全启动错误日志；1: 关闭 BL1 安全启动错误日志。 |
| 8 | bl2 info log disable | 0: 使能 BL2 普通日志；1: 关闭 BL2 普通日志。 |
| 9 | bl2 error log disable | 0: 使能 BL2 错误日志；1: 关闭 BL2 错误日志。 |
| 10 | bl2 secure download disable | 0: 使能 BL2 安全下载；1: 关闭 BL2 安全下载。 |
| 11 | long bl1 security counter enable | 0: BL1 security counter 占用 4 Bytes；1: 占用 68 Bytes。 |
| 12 | secure download | 0: 关闭安全下载；1: 使能安全下载。 |
| 13 | disable BKFIL channel temporary | 取值 0/2/3/4/5 时 BKFIL 通道使能；取值 1/7 时 BKFIL 通道关闭。 |
| 14\~15 | reserved | 保留位。 |
| 16 | disable download high freq | 0: 下载阶段关闭 CPU/FLASH/SPI 高频；1: 下载阶段使能高频（复位后恢复默认）。 |
| 17 | enable CPU 120M | 0: CPU 80M；1: CPU 120M（配合 BIT(4) 使用）。 |
| 18 | enable flash 80M | 0: FLASH 40M；1: FLASH 80M（取决于 FLASH 型号是否支持）。 |
| 19 | reserved | 保留位。 |
| 20 | attack\_nmi\_enable | 0: 检测到注入攻击时不产生 NMI；1: 检测到注入攻击时产生 NMI。 |
| 21 | spi\_to\_ahb\_disable | 0: SPI 到 AHB 通路不关闭；1: SPI 到 AHB 通路关闭。 |
| 22 | auto\_reset\_enable\[0\] | 0: 温度/电压异常不复位；1: 温度/电压异常复位。 |
| 23 | auto\_reset\_enable\[1\] | 0: 温度/电压异常不复位；1: 温度/电压异常复位。 |
| 24 | memchk\_bps | 0: 冷启动执行 memcheck；1: 冷启动跳过 memcheck。 |
| 25 | forever disable JTAG | 0: 不永久禁用 JTAG；1: 硬件永久禁用全部 JTAG 通道。 |
| 26 | shanhai\_clkgating\_en | 0: 关闭 shanhai 时钟门控；1: 使能 shanhai 时钟门控。 |
| 27 | flash\_crc\_mode | 0: 使能 FLASH CRC；1: 关闭 FLASH CRC。 |
| 28 | flash\_aes\_mode | 0: 128bit；1: 256bit。 |
| 29 | flash aes enable | 0: FLASH AES 加密未使能；1: FLASH AES 加密使能。 |
| 30 | spi download disable | 0: SPI 下载使能；1: SPI 下载关闭。 |
| 31 | debug\_sw\_disable | 0: 不禁用 JTAG；1: 禁用除 secure debug 外的 JTAG 通道，仅 Shanhai 可打开（依赖 BIT(25)）。 |

<a id="bit-1-security-boot-debug-mode"></a>

<a id="bit1-ref"></a>

### BIT(1) \- security boot debug mode

BL1 定义了两级调试信息来供用户定位问题，分别由 EFUSE BIT(1)/BIT(7) 来控制，其中 BIT(1) 控制普通调试信息，BIT(7) 控制严重错误。

普通调试信息除了错误之外，还包括一些流程性的日志打印。

严重错误通常是指会导致 BL1 启动失败的错误，当前 BL1 支持下述严重错误:

| 错误码 | 含义 |
| --- | --- |
| 0x1 | 读 EFUSE 出错 1 |
| 0x2 | 读 EFUSE 出错 2 |
| 0x3 | 读 FLASH 出错 1 |
| 0x11 | CPU 异常 NMI |
| 0x12 | CPU 异常 MemMange |
| 0x13 | CPU 异常 HardFault |
| 0x14 | CPU 异常 BusFault |
| 0x15 | CPU 异常 UserFault |
| 0x16 | CPU 异常 SecurityFault |
| 0x21 | OTP 为空 |
| 0x22 | 公钥为空 |
| 0x23 | 跳转 BIN 校验失败 |
| 0x1xxx | OTP 读失败 |
| 0x8yyyyyyy | 验签失败 |

其中 xxx 指 OTP 的 OFFSET，yyyyyyy 指具体的验签失败点。

严重错误在打印时仅打出错误码，如 “E16” 表示CPU 异常 SecurityFault。

备注

当严重错误使能时，BL1 安全启动时并不会初始化 UART，仅当产生了不可回复的严重错误时才会初始化 UART，进行打印。
因此，严重错误并不会影响正常启动功能，也不会带来安全问题。

重要

一般在开发阶段，尤其是尚未在任何板子上成功配置过安全启动之前，建议开启普通日志，这样，可以看到更多调试信息；
在熟悉了安全启动配置之后，或者在量产阶段，应该关闭普通日志。严重错误则建议在量产版本中也不要关闭。

<a id="bit-2-fast-boot-disable"></a>

### BIT(2) \- fast boot disable

BIT(2) 用于关闭 Fast Boot 启动。0 表示 Fast Boot 使能，1 表示关闭。

Fast Boot 用于控制系统从 Deep Sleep 醒来的流程，当 Fast Boot 使能时，Deep Sleep 醒来后跳过安全启动，直接跳转到应用程序中；
当 Fast Boot 关闭时，则与上电重启类似，会做完整的安全启动。

重要

Fast Boot 使能时，启动速度更快，但不够安全；Fast Boot 关闭时，启动速度较慢，但安全可靠。
应用应该依据实际需求决定是否开关 Fast Boot。

<a id="bit-3-disable-download-and-enable-secure-boot"></a>

### BIT(3) \- disable download and enable secure boot

BIT(3) 是安全启动的总开关，用于禁用下载并使能安全启动：

> - 0 表示不禁用下载，此时可通过 UART 下载版本，安全启动未使能；
> - 1 表示禁用下载并进入安全启动模式。

当 BIT(3) 置 1 时，安全启动使能，要求 OTP 中必须配置公钥 HASH，否则启动失败。

<a id="bit-4-sb-clock-select"></a>

### BIT(4) \- sb clock select

BIT(4) 用于使能安全启动高频模式。0 表示 CPU 与 FLASH 使用 XTAL 作为时钟，通常为 26Mhz，1 表示使能 PLL，CPU 与 FLASH 配置
在高频模式。在高频模式下，安全启动速度更快，对启动性能有要求的应用一般建议使能高频模式。

<a id="bit-5-random-delay-enable"></a>

### BIT(5) \- random delay enable

BIT(5) 用于使能随机延时，0 表示随机延时关闭，1 表示开启。当随机延时开启时，BL1 在调用关键函数前，都会做一个随机 delay，
通过这种机制减缓故障注入攻击带来的影响。

备注

随机延时使能会增加安全启动时间，除非对注入攻击防范特别高的应用，通常不建议打开随机延迟功能。

<a id="bit-6-power-on-fast-boot"></a>

### BIT(6) \- power on fast boot

BIT(6) 用于配置上电（power on）时是否跳过安全启动。0 表示上电时跳过安全启动，直接跳转到应用程序；1 表示上电时不跳过安全启动，执行完整的安全启动流程。

备注

BIT(2) 控制 Deep Sleep 唤醒时的快速启动，BIT(6) 控制上电时的快速启动，二者相互独立。

<a id="bit-7-security-boot-critical-error"></a>

### BIT(7) \- security boot critical error

请参考 [BIT1](#bit1-ref)。

<a id="bit-20-attack-nmi"></a>

### BIT(20) \- attack NMI

BIT(20) 用于配置在检测到故障注入攻击之后是否产生 NMI 异常。为 0 时 BL1 不会进行硬件层面的故障注入攻击检测，
为 1 时 BL1 会进行硬件层面的故障注入攻击检测，当检测到攻击时产生 NMI 异常。

备注

对故障注入攻击特别关注的应用，建议打开这个开关。

<a id="bit-29-flash-aes-enable"></a>

### BIT(29) \- flash aes enable

BIT(29) 用于使能 FLASH AES 加密，0 表示 FLASH AES 加密不使能，1 表示 FLASH AES 加密使能。

<a id="bit-30-spi-download-disable"></a>

### BIT(30) \- spi download disable

关闭 SPI 下载功能。为 0 时支持 SPI 下载；为 1 时关闭 SPI 下载。

重要

为避免带来安全隐患，量产版本中应该禁用 SPI 下载。但在尚未成功部署安全启动之前，可先不要禁用 SPI 下载，
这样，当安全启动部署失败时，依然可通过 SPI 下载将版本下载到 FLASH。否则，一旦安全启动部署失败，就再
也无法下载版本，板子变砖。

<a id="id6"></a>

## OTP/EFUSE 配置

<a id="bkfil"></a>

### 使用BKFIL

使用BKFIL工具将配置表文件内容配置OTP和EFUSE,在BKFIL命令行使用–safe-json选项可按照配置表.json文件配置OTP和EFUSE。
或者使用BKFIL界面来进行配置，如图所示

![8](../../../_assets/7415053123553eeb8419-otp_bkfil.png)

配置文件的格式如下：

数据格式：

```
"name":              "otp_ns_user_space", #名称,仅用于区分含义,无其他功能
"mode":              "write",             #读或写操作,write/read
"permission"         "NA",                #配置该OTP区域权限，仅在写模式生效
"start_addr":        "0x42100590",        #操作的起始地址
"last_valid_addr":   "0x42100600",        #当前区域可以最大合法操作的位置
"byte_len":          "0x8",               #操作的数据的长度
"data":              "123456789ABCDEF",   #操作的数据的内容,读时为空,写为空时不写入
"data_type":         "hex",               #操作的数据的类型,有hex/ascii两种
"status":            "false"              #该操作是否生效,true时执行,false为不执行
```

区域开关:控制四个区域的开关,分别为用户可操作区域,efuse区域,安全控制区域,安全数据区域。其中efuse区域和安全控制区域用于配置efuse相关bit,而用户操作区域和安全数据区域用于配置otp相关bit。开关设置为“true”生效,为”false”时失效。

用户可操作区域:当User\_Operate\_Status设置为true时该配置区域生效，可以根据用户自己的需求配置相关区域。用户可配置的区域为0x42100600\~0x42100700,对应的OTP location为128\~192。

efuse区域:对efuse进行读写操作,由于efuse按bit生效,整体操作容易出错,一般在安全控制区域用单个bit进行写,一般在efuse区域进行读操作。

安全控制区域:用于单个bit写入efuse,数据格式如下：

```
"enable_security_boot":         "0,0,1",
"disable_fast_boot":            "0,2,0",
"enable_flash_aes":             "3,5,1"
```

前面的为名称,后面的三个数据分别代表第几个字节,第几bit,写1还是0。示例分别向第0字节的第0和2bit写入1和0，向第3字节的第5个Bit写1。

安全数据区域:对otp区域进行读写操作。如读取AES加密用密钥。

```
"name":              "flash_aes_key",
"mode":              "read",
"start_addr":        "0x42100460",
"last_valid_addr":   "0x42100480",
"byte_len":          "0x20",
"data":              "",
"data_type":         "hex",
"status":            "true"
```

<a id="cpu"></a>

### 通过CPU读写寄存器

通过CPU读写寄存器可以实现前述的四种操作,将OTP，Efuse作为一般外设来进行操作。
需要进入Armino的Cli窗口。在otp driver初始化之后，输入otp write/read location data命令，如 otp write 156 0x1234，即可在location 156的otp区域写入数据0x1234。
如需更改权限等操作，可以参考cli端的help。

<a id="bl1-hash"></a>

### 配置 BL1 公钥 HASH

Public key hash地址为 0x42100528\~0x42100548,内容为(low)2af1f2236872981bdf2f17975fb3029fad171de61741a383ef2c621fd5f5cf62(high)
如下图所示在config的security data区域中添加相应字段。

![8](../../../_assets/52fddb4ddab59f09b440-otp_hashkey.png)

<a id="bl2-hash"></a>

### 配置 BL2 公钥 HASH

<a id="id7"></a>

### 配置 FLASH AES KEY

如下图所示在config的security data区域中添加相应字段。

![8](../../../_assets/2c55ce1fec800bd1ab4f-otp_aeskey.png)

<a id="id8"></a>

### 配置示例

如图所示，在User\_operate区域添加一个字段，写入6个字节BK7259,以ascii码的方式解析，

![8](../../../_assets/2d1dee6069c47c984708-otp_user_example.png)
