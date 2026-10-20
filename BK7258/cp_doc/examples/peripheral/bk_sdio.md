---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_sdio.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="fatfssd"></a>

# fatfs文件系统和SD卡读写

<a id="id1"></a>

## 1 功能概述

> SDK工程中使用fatfs文件系统对SD卡进行文件管理，用户只需要进行简单的配置就可以使用SD卡，本文档对操作fatfs文件系统的cli命令进行介绍。

<a id="id2"></a>

## 2 代码路径

> demo路径：`components\bk_cli\cli_fatfs.c` `components\fatfs\test_fatfs.c`

<a id="cli"></a>

## 3 cli命令简介

> > SDK工程中已经移植好fatfs文件系统，fatfs相关API介绍见：`http://elm-chan.org/fsw/ff/00index_e.html`
> >
> > SDIO demo运行依赖的宏配置：
> >
> > | NAME | Description | File | value |
> > | --- | --- | --- | --- |
> > | CONFIG\_SDIO\_V1P0 | support SDIO version V1P0,unused | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_SDIO\_V2P0 | support SDIO version V2P0,current version | `middleware\soc\bk7236\bk7236.defconfig` | y |
> > | CONFIG\_SDIO\_HOST | set to host mode for connecting SD card | `middleware\soc\bk7236\bk7236.defconfig` | y |
> > | CONFIG\_SDIO\_SLAVE | support SDIO slave mode,unused | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_SDIO\_CHANNEL\_EN | support SDIO logical channel,depend on CONFIG\_SDIO\_SLAVE | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_SDIO\_BIDIRECT\_CHANNEL\_EN | support SDIO bidirect channel,depend on CONFIG\_SDIO\_SLAVE | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_SDIO\_GDMA\_EN | support SDIO GDMA,unsuport,depend on CONFIG\_SDIO\_SLAVE | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_GPIO\_NOTIFY\_TRANSACTION\_EN | support notify transaction,,depend on CONFIG\_SDIO\_SLAVE | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_SDIO\_4LINES\_EN | support SDIO 4 line,if no,support 1 line | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_SDIO\_TEST\_EN | support SDIO testself | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_SDIO\_DEBUG\_EN | support SDIO debug | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_SDIO\_HOST\_DEFAULT\_CLOCK\_FREQ\=7 | set SDIO host clk,default 100k | `middleware\soc\bk7236\bk7236.defconfig` | 7 |
> >
> > SD card demo运行依赖的宏配置：
> >
> > | NAME | Description | File | value |
> > | --- | --- | --- | --- |
> > | CONFIG\_SDCARD\_HOST | support SD card,host mode | `middleware\soc\bk7236\bk7236.defconfig` | y |
> > | CONFIG\_SDCARD\_V2P0 | support SD version V2P0 | `middleware\soc\bk7236\bk7236.defconfig` | y |
> > | CONFIG\_SDCARD\_V1P0 | support SD version V1P0 | `middleware\soc\bk7236\bk7236.defconfig` | n |
> > | CONFIG\_SDCARD\_BUSWIDTH\_4LINE | support SD card 4 line | `middleware\soc\bk7236\bk7236.defconfig` | n |
> >
> > fatfs demo运行依赖的宏配置：
> >
> > | NAME | Description | File | value |
> > | --- | --- | --- | --- |
> > | CONFIG\_FATFS | support fatfs | `middleware\soc\bk7236\bk7236.defconfig` | y |
> > | CONFIG\_FATFS\_SDCARD | SD card support fatfs | `middleware\soc\bk7236\bk7236.defconfig` | y |
> >
> > demo支持的cli命令如下表：
> >
> > | Command | Param | Description |
> > | --- | --- | --- |
> > | fatfstest {M\|U} {DISK\_NUMBER} | {M\|U}: mount\|unmount | apply for or release the workspace for logical drivers |
> > | {DISK\_NUMBER}:logical driver number |
> > | fatfstest G {DISK\_NUMBER} | {DISK\_NUMBER}:logical driver number | get the size of remaining disk space |
> > | fatfstest S {DISK\_NUMBER} | {DISK\_NUMBER}:logical driver number | scan all files on disk |
> > | fatfstest F {DISK\_NUMBER} | {DISK\_NUMBER}:logical driver number | format disk |
> > | fatfstest R {DISK\_NUMBER}{file\_name}  {length} | {DISK\_NUMBER}:logical driver number | read specified length of data  from the file |
> > | {file\_name}:file to story read data |
> > | {length}: length to be read |
> > | fatfstest W {DISK\_NUMBER}{file\_name}  {content\_p}{content\_len} | {DISK\_NUMBER}:logical driver number | write data to a file |
> > | {file\_name}:file to be written |
> > | {content\_p}: pointer to the data to be written |
> > | {content\_len}:length to be written |
> > | fatfstest D {DISK\_NUMBER}{file\_name}  {start\_addr}{content\_len} | {DISK\_NUMBER}:logical driver number | read the specified length of data from the specified address and write it to the specified file |
> > | {file\_name}:file to be written |
> > | {start\_addr}: start address for reading |
> > | {content\_len}:length to be written |
> > | fatfstest A {DISK\_NUMBER}{file\_name}  {content\_len}{test\_cnt} {start\_addr} | {DISK\_NUMBER}:logical driver number | auto test,write the data to the file and then read it, and compare the result  note: the data written to the SD card is read from the specified start\_addr |
> > | {file\_name}:file to be written |
> > | {content\_len}: length of comparison |
> > | {test\_cnt}:number of cycle tests |
> > | {start\_addr}:start address for reading |
> >
> > disk\_number的定义：
>
> ```
>         typedef enum
> {
>     DISK_NUMBER_RAM  = 0,
>     DISK_NUMBER_SDIO_SD = 1,
>     DISK_NUMBER_UDISK   = 2,
>     DISK_NUMBER_FLASH   = 3,
>     DISK_NUMBER_COUNT,
> } DISK_NUMBER;
> ```

<a id="id3"></a>

## 4 演示介绍

> demo执行的步骤如下：
>
> 1、将SD卡插入开发板，GPIO 连接方式如下（因为GPIO复用，此demo SDIO配置为单线模式）：
>
> ```
> SD_CLK----GPIO14
> SD_CMD----GPIO15
> SD_D0-----GPIO16
> SD_D1-----GPIO17
> SD_D2-----GPIO18
> SD_D3-----GPIO19
> ```
>
> 2、SD卡操作

fatfstest M 1 //挂载SD卡

> ```
> [16:06:10.103]发→◇fatfstest M 1
> [16:06:10.108]收←◆fatfstest M 1
> error file name,use defaultfilename.txt
> sd_card:I(203942):sd card has inited
> fmt=2
> fmt2=0
> Fatfs:I(203944):f_mount OK!
> Fatfs:I(203944):----- test_mount 1 over  -----
> ```

fatfstest S 1 //扫描SD卡

> ```
> [16:11:39.041]发→◇fatfstest S 1
> [16:11:39.046]收←◆fatfstest S 1
> error file name,use defaultfilename.txt
> Fatfs:I(532878):
> ----- scan_file_system 1 start -----
> Fatfs:I(532878):1:/
> Fatfs:I(532880):1:/autotest_400.txt
> Fatfs:I(532882):1:/dump_1.txt
> Fatfs:I(532884):scan_files OK!
> Fatfs:I(532886):----- scan_file_system 1 over  -----
> ```

fatfstest W 1 test.txt acl\_bk7236\_write\_to\_test 24 //向文件test.txt中写入字符串”acl\_bk7236\_write\_to\_test”

> ```
> [16:15:02.687]发→◇fatfstest W 1 test.txt acl_bk7236_write_to_test 24
>
> [16:15:02.696]收←◆fatfstest W 1 test.txt acl_bkFatfs:I(736530):
> ----- test_fatfs 1 start -----
> Fatfs:I(736530):f_open "1:/test.txt"
> Fatfs:I(736530):.7236_write_to_test 24
>
> [16:15:02.837]收←◆TODO:FATFS sync feature
> Fatfs:I(736678):f_close OK
> Fatfs:I(736678):----- test_fatfs 1 over  -----
>
> append and write:test.txt
> [16:15:02.866]收←◆,acl_bk7236_write_to_test
> ```

fatfstest R 1 test.txt 32 //从文件test.txt中读取32字节数据

> ```
> [16:18:30.473]发→◇fatfstest R 1 test.txt 32
> [16:18:30.478]收←◆fatfstest R 1 test.txt 32
> Fatfs:I(944312):
> ----- test_fatfs 1 start -----
> Fatfs:I(944312):f_open "1:/test.txt"
> Fatfs:I(944314):will read left_len = 24
> Fatfs:I(944314):f_read start:24 bytes
>
> ====== f_read one cycle - dump(len=24) begin ======
> 61 63 6c 5f 62 6b 37 32 35 36 5f 77 72 69 74 65
> 5f 74 6f 5f 74 65 73 74
> ====== f_read one cycle - dump(len=24)   end ======
>
> Fatfs:I(944328):f_read one cycle finish:left_len = 0
> Fatfs:I(944332):f_read: read total byte = 24
> Fatfs:I(944336):f_close OK
> Fatfs:I(944338):----- test_fatfs 1 over  -----
>
> read test.txt, len_h = 0, len_l = 32
> ```

fatfstest A 1 autotest.txt 2222 1 0 //从flash 0x0 地址读取2222字节数据保存到SD卡autotest.txt中，再将数据从autotest.txt中读取出来进行比较；此操作进行1次

> ```
> [16:31:11.077]发→◇fatfstest A 1 autotest.txt 2222 1 0
> [16:31:11.083]收←◆fatfstest A 1 autotest.txt 2222 1 0
>
> [16:31:11.143]收←◆TODO:FATFS sync feature
> Fatfs:I(195362):auto test succ
> ```

fatfstest D 1 dump.txt 0 10240 //从0x0地址读取10240字节数据保存到文件dump.txt中

> ```
> [16:33:15.934]发→◇fatfstest D 1 dump.txt 0 10240
> [16:33:15.939]收←◆fatfstest D 1 dump.txt 0 10240
> Fatfs:I(320154):
> ----- test_fatfs_dump 1 start -----
> Fatfs:I(320154):file_name=dump.txt,start_addr=0x0,len=10240
> Fatfs:I(320154):f_open start "1:/dump.txt"
> Fatfs:I(320154):f_write start
> Fatfs:I(320158):f_write end len = 10240
> Fatfs:I(320158):f_lseek start
> Fatfs:I(320158):f_close start
> TODO:FATFS sync feature
> ```

fatfstest F 1 //对SD卡进行格式化

> ```
> [17:43:49.985]发→◇fatfstest F 1
> [17:43:49.990]收←◆fatfstest F 1
> error file name,use defaultfilename.txt
> sd_card:I(327564):sd card has inited
> part=0
> sd_card:I(327564):card ver=2.0,size:0x01dacc00 sector(sector=512bytes)
> sdcard sector cnt=31116288
>
> [17:43:55.480]收←◆TODO:FATFS sync feature
> Fatfs:I(333054):f_mkfs OK!
> format :1
> ```
