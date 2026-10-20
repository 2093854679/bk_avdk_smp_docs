---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_efuse.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="efuse"></a>

# EFUSE 使用指南

<a id="id1"></a>

## 概述

eFuse（electronic fuse） 是一种\*\*一次性可编程（One-Time Programmable, OTP）\*\*的非易失性存储器，广泛应用于芯片中，用于永久保存设备标识、配置参数、安全密钥、调试权限等关键信息。

<a id="id2"></a>

## eFuse 使用方法

> - eFuse使能，可调用 bk\_efuse\_driver\_init() 使能
> - 读取eFuse中特定地址的信息，调用 bk\_efuse\_read\_byte(addr, data) 获取
> - 写入eFuse中特定地址的信息，调用 bk\_efuse\_write\_byte(addr, data) 写入数据

备注

如果 \`\` CONFIG\_EFUSE \`\` 宏配置为 y ，系统会在 driver 初始化阶段初始化 eFuse 模块。eFuse模块供电后，即可通过特定函数访问eFuse的特定地址。

备注

如果需要通过BKFIL工具从上层写入EFUSE密钥等操作，需要参考 \`\` SMP开发框架 \`\` 中的 \`\` OTP/EFUSE 配置 \`\` 章节。

<a id="efuse-bit"></a>

## eFuse 中各bit位含义

EFUSE 共有 4x8 共 32 Bits, 其中每个 Bit 的含义不同。可以通过总 BKFIL 配置。

| index | name |  |
| --- | --- | --- |
| 0 | security boot enable | 0: 不使能安全启动。1: 使能安全启动。 |
| 1 | security boot debug mode | 0: 使能安全启动调试信息。1: 关闭安全启动调试信息。 |
| 2 | fast boot disable | 0: 使能快速启动；1: 关闭快速使能。 |
| 3 | boot mode | 0：传统下载模式；1: 安全启动模式。 |
| 4 | security boot clock select | 0: 安全启动使用 XTAL 时钟；1: 安全启动使能 PLL。 |
| 5 | random delay enable | 0: 关闭了随机延时；1: 使能随机延迟。 |
| 6 | direct jump enable | 0: 关闭安全启动直接跳转；1: 使能安全启动直接跳转。 |
| 7 | security boot critical error | 0: 不关闭安全启动中严重错误打印；1: 关闭安全启动中严重错误打印。 |
| 8\~19 | reserved | 保留位 |
| 20 | attack\_nmi\_enable | 0: 检测到注入攻击时不产生 NMI；1: 检测到注入攻击时产生 NMI。 |
| 21 | spi\_to\_ahb\_disable | 0：SPI 到 AHB 通路不关闭；1: SPI 到 AHB 通路关闭。 |
| 22 | auto\_reset\_enable\[0\] | 温度电压异常复位 |
| 23 | auto\_reset\_enable\[1\] | 温度电压异常复位 |
| 24\~28 | reserved | 保留位 |
| 29 | flash aes enable | 0: FLASH AES 加密未使能；1: FLASH AES 加密使能。 |
| 30 | spi\_dld\_disable | 0: SPI 下载使能；1: SPI 下载关闭。 |
| 31 | reserved | 保留位 |

<a id="bit-0-security-boot-enable"></a>

<a id="bit0-ref"></a>

### BIT(0) \- security boot enable

EFUSE 中有两位与安全启动使能相关：

> - BIT(3) \- boot mode 用于设置启动模式。0 表示传统下载模式，此时可通过 UART 下载版本；1 表示安全启动模式，设置成安全启动模式之后还需要通过 BIT(3) 使能安全启动。
> - BIT(0) \- 使能安全启动。仅在 BIT(3) 设置成 1（安全启动模式）时有效，表示是否使能安全启动。

当 BIT(0) 置 0 时，表示安全启动未使能，此时 BL1 认为 IMAGE 中的公钥合法，即不会使用 IMAGE 中的公钥与 OTP 中的公钥 HASH
做比对，仅做 IMAGE 完整性验证。因此，这时 OTP 中即使不配置公钥 HASH 系统依然能启动。

当 BIT(0) 置 1 时，表示安全启动使能，要求 OTP 中必须配置公钥 HASH，否则启动失败。

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

<a id="bit-3-boot-mode"></a>

### BIT(3) \- boot mode

请参考 [BIT0](#bit0-ref)。

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

<a id="bit-6-direct-jump"></a>

### BIT(6) \- Direct Jump

BIT(6) 用于配置 BL1 验签完之后的跳转方法，0 表示间接跳转，1 表示直接跳转。

使用间接跳转时，BL1 在验签完之后不是直接跳转到被验的 IMAGE，而是先跳转到一个中间 BIN，然后由中间 BIN 再跳转到目标 IMAGE。
使用直接跳转时，BL1 在验签完成之后直接跳转到被验的 IMAGE。

备注

当使用间接跳转时，中间 BIN 也会包含在 IMAGE 中一起验签，因此是安全的。

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
