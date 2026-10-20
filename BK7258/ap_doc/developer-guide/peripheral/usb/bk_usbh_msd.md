---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/usb/bk_usbh_msd.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="usb-host-msd"></a>

# USB Host MSD

> BK7258的 USB MSD 使用的是FATFS文件系统，支持从 USB 设备读取/写入。由于文件系统默认在AP侧进行编译和使用需要将USB MSD相关宏开关在AP侧的config中打开。

<a id="usb-msd"></a>

## USB MSD的宏定义配置

CONFIG\_USB\=y 打开USB的总开关宏定义 使能USB的代码功能

CONFIG\_USB\_VBAT\_CONTROL\_GPIO\_ID\=0x1C 默认使用的GPIO是GPIO\_28进行USB Vbus电的控制，用户根据自己的实际情况进行配置

CONFIG\_USB\_HOST\=y 主程序作为HOST 对接口连接的设备进行枚举

CONFIG\_TASK\_USB\_PRIO\=2 USB的处理程序的TASK优先级配置为2

CONFIG\_USBH\_MSC\=y 打开MSD驱动的编译，能够做到打开USB后自动识别 U盘

<a id="msd-cli"></a>

## MSD 主机驱动CLI测试示例

注：HOST MSD的使用依赖文件系统。默认文件系统的代码主要在CPU0上运行，且支持SDCARD和FLASH。

对USB的Vbus进行上电/下电操作cli示例：
:   输入命令：
    usb power 1c 1 打开USB Vbus供电
    usb power 1c 0 关闭USB Vbus供电

<a id="id2"></a>
![powneron_powner_down](../../../../../../_assets/ebde69c37edb2a32b11f-poweron_powerdown.png)


USB Vbus poweron and powerdown

打开USB对U盘进行枚举：
:   输入命令：
    usb open\_host

<a id="id3"></a>
![open USB for enumeration](../../../../../../_assets/c08d1169c4b9eb4f0639-open_usb_enum.png)


open USB for enumeration

调用cli\_fatfs的测试命令进行U盘的操作:
:   输入命令：fatfstest M 2

<a id="id4"></a>
![mount_udisk](../../../../../../_assets/27ddc5c652fcaf591a8d-mount_udisk.png)


Mount Udisk

> 输入命令：fatfstest S 2

<a id="id5"></a>
![scan udisk](../../../../../../_assets/652bdb2be805f542c210-scan_udisk.png)


Scan Udisk

> 输入命令：fatfstest U 2

<a id="id6"></a>
![umount udisk](../../../../../../_assets/c8f73d052aa698e0a7a0-umount_udisk.png)


Unmount Udisk

> 输入命令：fatfstest R 2 abc.txt 100

<a id="id7"></a>
![read file](../../../../../../_assets/bc587c62f273faa663c0-read_file.png)


Read file

输入命令：fatfstest W 2 abc.txt ABCDEFG

<a id="id8"></a>
![write file](../../../../../../_assets/3babbd098ca065b43acb-write_file.png)


Write file

<a id="id1"></a>

## USB MSD

> 更多详细开发可参考CherryUSB相关文档， <https://github.com/cherry-embedded/CherryUSB/blob/master/README_zh.md>
