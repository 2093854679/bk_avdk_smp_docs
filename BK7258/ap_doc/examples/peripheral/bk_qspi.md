---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/peripheral/bk_qspi.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="qspi"></a>

# QSPI

<a id="id1"></a>

## 1 功能概述

> ```
> QSPI 作为主设备 (Master) 用于对通用的从设备 (Slave)（如 Flash、PSRAM 或者显示屏）进行读写操作，
> 支持单线、双线或四线（数据线）SPI 操作；
> BK7258具有2路QSPI控制器，用户可以根据硬件实际情况进行使用；
> 可以在如下两种模式下工作：
> a) 间接模式：使用 QSPI 寄存器执行全部操作
> b) 内存映射模式：外部设备映射到内部存储地址空间，从而系统将其视为内部存储器
> ```
>
> - QSPI功能具体描述参考: [QSPI驱动工作原理](../../developer-guide/peripheral/bk_qspi.md)

<a id="id3"></a>

## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_qspi.c`
> - 驱动源码路径：
>   :   `middleware\driver\qspi\qspi_driver.c`
>
>       `middleware\driver\qspi\qspi_flash.c`

<a id="id4"></a>

## 3 QSPI相关宏配置

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG\_QSPI | QSPI驱动及其测试命令使能配置 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
> | CONFIG\_QSPI\_MST\_FLASH | QSPI flash驱动使能配置 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
> | CONFIG\_QSPI\_FLASH\_GD\=y | 用于QSPI flash驱动区分不同类型的flash厂商，写状态寄 存器01H命令作用域为S0\~7时使能，作用域为S0\~15时关闭 | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | y |
> | CONFIG\_QSPI\_LINE\_MODE | QSPI flash读写线宽选择:1\=单/2\=双/4\=四线(默认4) | `middleware\soc\bk7258_ap\bk7258_ap.defconfig` | 4 |

<a id="qspi-pin"></a>

## 4 QSPI PIN脚描述

> - QSPI0 和 QSPI1 各对应1组PIN脚，描述如下：
>   :   | QSPI0功能 | 组0 |
>       | --- | --- |
>       | QSPI0\_SCK(IOZ) | GPIO22 |
>       | QSPI0\_CS(O) | GPIO23 |
>       | QSPI0\_DAT\[0\](IO) | GPIO24 |
>       | QSPI0\_DAT\[1\](IO) | GPIO25 |
>       | QSPI0\_DAT\[2\](IO) | GPIO26 |
>       | QSPI0\_DAT\[3\](IO) | GPIO27 |
> - QSPI1对应1组PIN脚，对应管脚如下：
>   :   | QSPI1功能 | 组0 |
>       | --- | --- |
>       | QSPI1\_SCK(IOZ) | GPIO2 |
>       | QSPI1\_CS(O) | GPIO3 |
>       | QSPI1\_DAT\[0\](IO) | GPIO4 |
>       | QSPI1\_DAT\[1\](IO) | GPIO5 |
>       | QSPI1\_DAT\[2\](IO) | GPIO6 |
>       | QSPI1\_DAT\[3\](IO) | GPIO7 |

<a id="qspi-demo"></a>

## 5 QSPI demo 配置

> - demo支持的命令如下表：
>
> | Command | Param | Description |
> | --- | --- | --- |
> | **qspi\_driver** **{init\|deinit}** | {init\|deinit}: | Init/deinit the qspi resoure common |
> | **qspi {id} init {src\_clock}** **{src\_clk\_div} {qspi\_clk\_div}** | {id}: qspi device id, range 0 \~ 1 {src\_clock}: qspi source clock, 0 means QSPI\_CLK\_320M, 1 means QSPI\_CLK\_480M {src\_clk\_div}: qspi source clock divider {qspi\_clk\_div}: qspi internal clock divider | Enable qspi and set the qspi clock  qspi\_actual\_clock \= {src\_clock\_value}/{1\+src\_clk\_div}/{2\*qspi\_clk\_div} |
> | **qspi\_flash {id} get\_id {addr} {len}** | {id}: qspi device id, range 0 \~ 1 {addr}: any value would be ok {len}: any value would be ok | Send 9fH cmd to get flash vendor id this get id cmd would unprotect the flash and set QE (quad enable) status register |
> | **qspi\_flash {id} read {addr} {len}** | {id}: qspi device id, range 0 \~ 1 {addr}: the flash offset to access {len}: the data length to access | Send ebH cmd to read flash data with 4 bus wide, Remember to enable the flash QE bit firstly. |
> | **qspi\_flash {id} erase {addr} {len}** | {id}: qspi device id, range 0 \~ 1 {addr}: the flash offset to access {len}: the data length to access | Send 20H cmd to erase flash |
> | **qspi\_flash {id} write {addr} {len}** | {id}: qspi device id, range 0 \~ 1 {addr}: the flash offset to access {len}: the data length to access | Send 32H cmd to write flash |
> | **qspi {id} flash\_test {addr} {len}** | {id}: qspi device id, range 0 \~ 1 {addr}: the flash offset to access {len}: the data length to access | Auto test the flash, such as get id, erase, write, and read, once meet fail, it will report error. |
>
> 备注
>
> 上表 `qspi {id} init {src_clk} {src_clk_div} {qspi_clk_div}` 为手动指定分频。使用 flash 相关 API 时，
> `bk_qspi_flash_init()` 内部会自动调用 `bk_qspi_init_by_freq(id, QSPI_FLASH_MAX_SCK_HZ)` 完成时钟初始化，
> 其中 ``` QSPI_FLASH_MAX_SCK_HZ = 80 MHz``（QSPI 可配置的最高 SCK）。``bk_qspi_init_by_freq ``` 会在不超过目标
> 频率的前提下，自动搜索最接近目标频率的分频组合。
>
> 时钟换算公式（SCK 为 QSPI 实际输出时钟）：
>
> ```
> SCK = src_clk / ((1 + src_clk_div) * (clk_div == 0 ? 1 : 2 * clk_div))
>
> - src_clk     ：源时钟，可选 480 MHz 或 320 MHz
> - src_clk_div ：一级分频，硬件要求 >= 4
> - clk_div     ：二级分频，为 0 时旁路(÷1)，否则为 2 * clk_div
>
> 示例：
> 480 MHz / ((1 + 5) * 1)       = 80 MHz  （bk_qspi_init_by_freq(id, 80 MHz) 实际选中：src_clk_div=5, clk_div=0 旁路）
> 480 MHz / ((1 + 4) * (2 * 2)) = 24 MHz  （默认回退组合：src_clk_div=4, clk_div=2）
> 480 MHz / ((1 + 5) * (2 * 5)) = 8  MHz  （对应 demo 命令 qspi 1 init 1 5 5）
> ```

<a id="id5"></a>

## 6 QSPI demo 命令行演示

> 1. bk7258开发板直连带底座的外置flash，按照下图进行连接并3.3V供电：

<a id="id6"></a>
![QSPI](../../../../../_assets/aae49633995ba02e4b27-qspi_flash_board.png)


Figure 1\. 开发板通过QSPI外接Flash

2. 启动开发板，对开发板分别输入初始化命令，分别设置QSPI系统时钟源，系统时钟分频和QSPI时钟分频。

   > - master： **cpu1 qspi 1 init 1 5 5**
   >
   >   > ```
   >   > [19:52:59.261]发→◇cpu1 qspi 1 init 1 5 5
   >   > [19:52:59.307]收←◆cpu1 qspi 1 init 1 5 5
   >   > $cpu1:cli:I(2832):qspi_id:00000001
   >   > (2964):cp0_mb_rx_isr 1 104 0 0 0
   >   > pwr_core:I(2964):LP event:5
   >   > cpu1:cli:I(2832):qspi init
   >   > ```

> 3. 获取flash vendor id
>
> > - master： **cpu1 qspi\_flash 1 get\_id 0 100**
> >
> >   > ```
> >   > [20:11:43.441]发→◇cpu1 qspi_flash 1 get_id  0  100
> >   > [20:11:43.478]收←◆cpu1 qspi_flash 1 get_id  0  100
> >   > $cpu1:qspi:I(1127010):[bk_qspi_flash_write_s0_s7]: status_reg_data to be writen is 0x0.
> >   > cpu1:qspi:I(1127010):[bk_qspi_flash_write_s8_s15]: status_reg_data to be writen is 0x2.
> >   > ```
>
> 4. 对flash指定地址和长度，进行擦除。
>
> > - master： **cpu1 qspi\_flash 1 erase 0 4096**
> >
> >   > ```
> >   > [19:53:09.405]发→◇cpu1 qspi_flash 1 erase 0 4096
> >   > [19:53:09.446]收←◆cpu1 qspi_flash 1 erase 0 4096
> >   > [19:53:09.489]收←◆
> >   > $
> >   > ```
>
> 5. 对flash指定地址和长度的区域，在擦除后进行读写。
>
> > - master： **cpu1 qspi\_flash 1 read 0 512**
> >
> >   > ```
> >   > [19:53:11.077]发→◇cpu1 qspi_flash 1 read 0 512
> >   > [19:53:11.121]收←◆cpu1 qspi_flash 1 read 0 512
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ```
>
> 6. 对flash指定地址和长度，进行写入。
>
> > - master： **cpu1 qspi\_flash 1 write 0x0 256**
> >
> >   > ```
> >   > [19:53:12.573]发→◇cpu1 qspi_flash 1 write 0x0 256
> >   > [19:53:12.614]收←◆cpu1 qspi_flash 1 write 0x0 256
> >   > [19:53:12.654]收←◆
> >   > ```
>
> 7. 对flash指定地址和长度，进行读取。
>
> > - master： **cpu1 qspi\_flash 1 read 0 512**
> >
> >   > ```
> >   > [19:53:06.117]发→◇cpu1 qspi_flash 1 read 0 512
> >   > [19:53:06.157]收←◆cpu1 qspi_flash 1 read 0 512
> >   > 00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f
> >   > 10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f
> >   > 20 21 22 23 24 25 26 27 28 29 2a 2b 2c 2d 2e 2f
> >   > 30 31 32 33 34 35 36 37 38 39 3a 3b 3c 3d 3e 3f
> >   > 40 41 42 43 44 45 46 47 48 49 4a 4b 4c 4d 4e 4f
> >   > 50 51 52 53 54 55 56 57 58 59 5a 5b 5c 5d 5e 5f
> >   > 60 61 62 63 64 65 66 67 68 69 6a 6b 6c 6d 6e 6f
> >   > 70 71 72 73 74 75 76 77 78 79 7a 7b 7c 7d 7e 7f
> >   > 80 81 82 83 84 85 86 87 88 89 8a 8b 8c 8d 8e 8f
> >   > 90 91 92 93 94 95 96 97 98 99 9a 9b 9c 9d 9e 9f
> >   > a0 a1 a2 a3 a4 a5 a6 a7 a8 a9 aa ab ac ad ae af
> >   > b0 b1 b2 b3 b4 b5 b6 b7 b8 b9 ba bb bc bd be bf
> >   > c0 c1 c2 c3 c4 c5 c6 c7 c8 c9 ca cb cc cd ce cf
> >   > d0 d1 d2 d3 d4 d5 d6 d7 d8 d9 da db dc dd de df
> >   > e0 e1 e2 e3 e4 e5 e6 e7 e8 e9 ea eb ec ed ee ef
> >   > f0 f1 f2 f3 f4 f5 f6 f7 f8 f9 fa fb fc fd fe ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff ff
> >   > ```
> >
> > h） QSPI flash一键测试命令
> > \- master： **cpu1 qspi 1 flash\_test 0 256**
> >
> > > ```
> > > [19:53:01.253]发→◇cpu1 qspi 1 flash_test 0 256
> > > [19:53:01.291]收←◆cpu1 qspi 1 flash_test 0 256
> > > ```

<a id="qspi-flash"></a>

## 7 QSPI flash调试常见问题：

> A） QSPI支持位宽是多少？
> :   Ans:支持1、2、4线半双工读写，`bk_qspi_flash_read` / `bk_qspi_flash_write` 根据 `CONFIG_QSPI_LINE_MODE` (1\=单线/2\=双线/4\=四线) 自动选择单/双/四线路径，默认4线读写。
>
> B） 获取flash ID失败原因？
> :   Ans:a）检查flash供电，通常接3.3V VBAT;
>     :   b）检查QSPI是否初始化成功，时钟是否过高，最大支持80MHz。
>
> C） 读flash id正确，但是擦写读失败？
> :   Ans:检查flash状态寄存器，是否解保护，是否使能QE 4线使能bit位。不同厂家的flash，写状态寄存器的命令及范围会有所区别，
>     :   有的是S0\~7和S8\~15，有的是S0\~15，写状态寄存器的API中，两种类型都有提供，可根据flash厂家spec按需使用。
