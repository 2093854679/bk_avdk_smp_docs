---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7258/zh_CN/v3.1.1/developer-guide/architecture/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: SMP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap-smp-cp"></a>

# AP(SMP)\+CP 架构

<a id="id1"></a>

## **架构概述**

BK7258由三个core组成,为了更加方便应用层开发, 在原来的架构基础上, Armino SDK设计了新的AP\+CP架构, 即SMP(CPU1\+CPU2)\+CPU0的模式。
其中CPU1\+CPU2组成SMP系统, 称为AP, CPU0为单核系统, 称为CP。

<a id="id12"></a>
![FreeRTOS Architecture](../../../_assets/1e9e7ec8a8a5e75beb42-smp_system.png)


AP(SMP)\+CP 架构

如上图所示, AP和CP是独立的两个子系统, 其独立性体现为：

> - CP代码完全独立, 只包含Wi-Fi, BLE和少部分基础外设, 运行在cpu0上
> - AP代码完全独立, 包含多媒体方案, 客户主要在AP上开发, cpu1和cpu2实现SMP

从应用层的视角看, CP上运行Wi-Fi, BLE, 用于低功耗保活的LWIP协议栈, 及必要的外设；AP上运行多媒体模块, 给上层提供的LWIP协议栈, 应用经常使用的外设。
AP和CP之间通过Mailbox\+共享内存通讯。从应用层的视角, AP和CP之间通过虚拟Uart接口通讯。
AP的Log通过MailBox发送到CP从UART0输出。

在新的架构下, 用户所有的开发都在AP上, 不再需要关注CP侧的开发。CP测的功能、AP与CP间的交互都由底层保证。

新架构的SDK组成也采用全新的目录, 具体结构如下:

```
ubuntu240:~/bk_avdk_smp$ tree -L 2
├── ap
│   ├── CMakeLists.txt
│   ├── components
│   ├── docs
│   ├── include
│   ├── Kconfig
│   ├── Makefile
│   ├── middleware
│   ├── properties
│   └── requirements.txt
├── cp
│   ├── CMakeLists.txt
│   ├── components
│   ├── docs
│   ├── include
│   ├── Kconfig
│   ├── Makefile
│   ├── middleware
│   ├── properties
│   └── requirements.txt
├── docs
│   ├── bk7258
│   └── version.json
├── LICENSE
├── Makefile
├── projects
│   ├── app
│   ├── app_ab
│   ├── doorbell
│   ├── lvgl
│   └── test
├── README_CN.md
├── README.md
└── tools
    ├── armino_doc.py
    ├── bk_bootloader_post.py
    ├── bk_smp_auto_partition.py
    ├── bk_smp_package.py
    ├── build_main.mk
    ├── build_tools
    └── env_tools
```

AP和CP代码分别在各自的目录下, 两者间的代码完全独立。工程目录下包含ap\_main文件夹和cp\_main文件夹, 用来分别存放客户对于AP和CP的需求代码。

基于以上的目录结构, 构建过程如下:

> - 先根据Project配置的分区表, 自动分区工具生成对应的分区表及相关文件
> - 然后编译BK7258 AP系统, 生成SMP镜像
> - 然后编译BK7258 CP系统, 生成bootloader和cp.bin镜像
> - 将bootloader.bin,cp.bin,ap.bin根据分区表打包成all-app.bin

<a id="id2"></a>

## **系统控制**

<a id="id3"></a>

### **资源划分**

当前的内存划分为: 每个core内有16KB的ITCM和16KB DTCM空间, sram/psram以及flash空间是AP和CP共享的。

当前的SDK中已经按照资源的需求划分好了CP与AP的内存。

如果上层应用需要重新划分资源, 可以在工程中修改ram\_regions.csv配置。

具体请参考 [RAM资源分区配置](config_tools/bk_config_ram_regions.md#bk-config-ram-regions) .

考虑到sram资源有限, 为了系统资源的充分利用。新架构中sram的布局也进行了调整。

当前sram内存布局如下(以doorbell工程为例):

```
/***************************************************************************
|--spinlock--|--hardware acc--|--ap sram--|--cp sram--|--pwr-mng--|--swap--|
****************************************************************************/
```

备注

建议客户不要随意改变该布局, 但可以根据实际需求调整ap和cp上sram的大小。

对于psram的使用, 考虑PSRAM可能需要掉电, CP上使用PSRAM仅限于动态Log等用完就释放的场景, CP上不允许将TASK或Queue或代码放到PSRAM上。

<a id="id4"></a>

### **系统复位**

架构采用的是全复位方案, 即CP或AP系统出现异常时, 整个系统全部复位。

也支持上层应用主动调用bk\_reboot接口进行复位。

<a id="id5"></a>

### **系统看门狗**

由于看门狗硬件资源只有一份, 所以将其放在了CP上进行管理。由以下的宏进行配置:

```
CONFIG_INT_WDT=y
CONFIG_INT_WDT_PERIOD_MS=8000
CONFIG_TASK_WDT=y
CONFIG_TASK_WDT_PERIOD_MS=16000
```

喂狗的操作在CP上进行, 如果超过配置的时间没有喂狗, 会触发系统重启。

AP侧没有看门狗, 通过核间心跳机制来检测AP是否正常运行。

<a id="id6"></a>

### **核间心跳**

AP侧在启动后, 会定时向CP发送心跳包(默认间隔时间为2S)。该功能由宏CONFIG\_SLAVE\_HEART\_BEAT控制, 默认开启。

当CP侧超过一定时间(与配置的INT WDT超时时间一致)没有接收到AP侧的心跳包, 则认为AP侧异常掉线, 会触发系统重启。

<a id="id7"></a>

### **系统调试**

系统的log由CP管理, 如果是CP侧的log, 则直接通过串口输出; 如果是AP侧的log, 由AP通过mailbox传送到CP侧, 再由串口输出。
CP侧的log不带任何前缀, AP侧的log会带ap0或ap1前缀。

如以下是系统启动的部分log示例:

```
os:I(7):mem_type start    end      size
os:I(7):-------- -------- -------- --------
os:I(7):itcm     0x20     0x3e88   15976
os:I(7):dtcm     0x20000000 0x200035f8 13816
os:I(7):ram      0x28064e00 0x2809e7f8 236024
os:I(7):non_heap 0x28064e00 0x280853a0 132512
os:I(7):iram     0x8064000 0x8064c40 3136
os:I(7):data     0x28064e00 0x28066128 4904
os:I(7):bss      0x28066140 0x2808539c 127580
os:I(7):heap     0x280853a0 0x2809e7f8 103512
os:I(7):psram    0x60700000 0x60720000 131072
os:I(8):create flash_svr, tcb=28088e00, stack=[280887d8-28088dd8:1536], prio=3
flash:I(8):id=0xc86517
ef:I(9):ENV start address is 0x007FA000, size is 8192 bytes.
ef:I(10):EasyFlash V4.1.0 is initialize success.
(11):ate enabled is 0
(11):driver_init end
sensor:I(11):saradc low value:[9bb]
sensor:I(11):saradc high value:[136a]
sensor:I(11):sdmadc low value:[6ec1]
sensor:I(11):sdmadc high value:[89e4]
init:I(11):reason - power on
init:I(11):regs - 0, 0, 0
init:I(11):armino rev:
init:I(11):armino soc id:53434647_72360101
bk_init:I(11):armino app init: Jun  6 2025 17:30:09
bk_init:I(11):verify id: unknown
bk_init:I(11):APP Version: unknown
nv:I(11):vnd_cal_version = 24-04-10 00:00:00
os:I(12):create event, tcb=28089ba8, stack=[28089380-28089b80:2048], prio=1

......

bluetoot:I(97):bk_bluetooth_init ok
os:I(98):create rosc_calib, tcb=28095028, stack=[28094000-28095000:4096], prio=1
(98):user app entry(0x2033561)
(99):reset_cpu1_core at: 02150000, start=1
ap0:AP:E(13):Mailbox send data fail[ret:-4103]
ap0:os:I(13):psram:0x60720000,size:655360
ap0:os:I(1):
ap0:os:I(13):mem_type start    end      size
ap0:os:I(13):-------- -------- -------- --------
ap0:os:I(13):itcm     0x20     0xa0     128
ap0:os:I(13):dtcm     0x20000004 0x20000004 0
ap0:os:I(13):ram      0x28010600 0x28060ff8 330232
ap0:os:I(13):non_heap 0x28010600 0x2801a400 40448
ap0:os:I(13):iram     0x8010000 0x8010508 1288
ap0:os:I(13):data     0x28010600 0x28010f44 2372
ap0:os:I(13):bss      0x28011d40 0x2801a3fc 34492
ap0:os:I(13):heap     0x2801a400 0x28060ff8 289784
ap0:os:I(13):psram    0x60720000 0x607c0000 655360
ap0:ef:I(14):ENV start address is 0x007FC000, size is 8192 bytes.
ap0:ef:I(32):EasyFlash V4.1.0 is initialize success.
ap0:(33):driver_init end
ap0:init:I(33):reason - power on
ap0:init:I(33):regs - 0, 0, 0
ap0:init:I(33):armino rev:
ap0:init:I(33):armino soc id:53434647_72360101
ap0:bk_init:I(33):armino app init: Jun  6 2025 17:30:00
ap0:bk_init:I(33):verify id: unknown
ap0:bk_init:I(33):APP Version: unknown
ap0:gpio:I(34):bk_gpio_driver_init:has inited
ap0:OS:I(34):create cli, tcb=2801ede8, stack=[2801d1c0-2801edc0:7168], prio=5, xCoreID=0
```

系统支持通过CLI命令对模块进行调试。CP侧的CLI命令不需要带任何前缀; AP侧的CLI命令必须带上 ap\_cmd 前缀。

以下是CP侧和AP侧输入memshow命令的示例:

```
CP侧
memshow （输入命令）

os:I(108703):create shell_handle, tcb=28087270, stack=[28085648-28087248:7168], prio=5
cli:I(108704):================Static memory================
os:I(108704):
os:I(108704):mem_type start    end      size
os:I(108704):-------- -------- -------- --------
os:I(108704):itcm     0x20     0x3e88   15976
os:I(108704):dtcm     0x20000000 0x200035f8 13816
os:I(108704):ram      0x28064e00 0x2809e7f8 236024
os:I(108704):non_heap 0x28064e00 0x280853a0 132512
os:I(108704):iram     0x8064000 0x8064c40 3136
os:I(108704):data     0x28064e00 0x28066128 4904
os:I(108704):bss      0x28066140 0x2808539c 127580
os:I(108704):heap     0x280853a0 0x2809e7f8 103512
os:I(108704):psram    0x60700000 0x60720000 131072
cli:I(108704):================Dynamic memory================
name    total   free    minimum   peak
heap        103512  31688   26200   77312
psram       131072  131040  129104  1968

AP侧
ap_cmd memshow （输入命令）
os:I(2009):create shell_handle, tcb=280871e0, stack=[280855b8-280871b8:7168], prio=5

$ap0:cli:I(1857):================Static memory================
ap0:os:I(1857):
ap0:os:I(1857):mem_type start    end      size
ap0:os:I(1857):-------- -------- -------- --------
ap0:os:I(1857):itcm     0x20     0xa0     128
ap0:os:I(1857):dtcm     0x20000004 0x20000004 0
ap0:os:I(1857):ram      0x28010600 0x28060ff8 330232
ap0:os:I(1857):non_heap 0x28010600 0x2801a408 40456
ap0:os:I(1857):iram     0x8010000 0x8010508 1288
ap0:os:I(1857):data     0x28010600 0x28010f44 2372
ap0:os:I(1857):bss      0x28011d40 0x2801a404 34500
ap0:os:I(1857):heap     0x2801a408 0x28060ff8 289776
ap0:os:I(1857):psram    0x60720000 0x607c0000 655360
ap0:cli:I(1857):================Dynamic memory================
name    total   free    minimum   peak
heap        289784  250736  246400  43384
psram       655360  655328  655288  72
```

当系统发生了异常时, 如果开启了宏CONFIG\_DEBUG\_FIRMWARE或CONFIG\_DUMP\_ENABLE, 会有dump log输出。如果是CP侧发生了异常, dump log直接通过串口进行输出;
如果是AP侧发生了异常, dump log通过mailbox传输到CP侧, 由CP侧控制串口进行输出。

备注

为了兼容性, AP侧的cli命令统一带ap\_cmd前缀, 因为此时AP为smp系统, 两个core可以看作一个整体。
但是AP侧的log 输出可能带有ap0 和 ap1, 这是为了区分具体是哪个core在运行代码输出的log。

如：

ap1:(95040):cpu2\_test\_task run core: 2

ap0:(95040):cpu1\_test\_task run core: 1

ap0:(96040):cpu1\_test\_task run core: 1

ap1:(96040):cpu2\_test\_task run core: 2

<a id="cp"></a>

## **CP子系统**

CP侧的功能比较简单, 主要分为以下部分：

> - 运行Wi-Fi, BLE, 用于低功耗保活的LWIP协议栈
> - 管理系统的log输出以及cli命令响应
> - 管理核间心跳, 检测AP是否在线
> - 系统的低功耗管理

<a id="ap"></a>

## **AP子系统**

<a id="id8"></a>

### **概述**

按照新的架构设计, Bk7258支持双核SMP架构, 这两个核共享所有的外设以及内存资源。每个core又各自含有自身的NVIC、cache等私有资源。核间可以通过mailbox交互必要的信息。

<a id="id13"></a>
![FreeRTOS Architecture](../../../_assets/08c5b81d1cd2b7a604ca-smp.png)


SMP 架构示意图

备注

1.图中的CPU0/CPU1指的是逻辑core id, 具体解释见下一章节, 后续我们统一用逻辑id来表述。

2.SMP中的mailbox指的是一条物理mailbox通道, 用来给两个内核间传递必要信息。

<a id="core-id"></a>

### **core id管理**

按照新架构的设计, smp系统运行在物理CPU1和CPU2上。

从内核的视角看, 采用的是逻辑id, 即不管实际在什么物理核上, 总是按0、1这样排列;

而从应用层的视角, 由于某些配置的资源需要与具体的物理核绑定, 所以获取到的是物理id。通过os.h文件中的rtos\_get\_core\_id()来得到。该接口返回值为1或者2, 代表物理的CPU1或CPU2。

在SMP启动过程中, 每个core会分别将自身的core id记录到特定位置。

重要

注意: 上层只允许调用rtos\_get\_core\_id()来获取core id,返回值为CPU1\_CORE\_ID或CPU2\_CORE\_ID, 对应物理CPU1和CPU2。

<a id="smp"></a>

### **SMP启动流程**

在系统的引导和初始化阶段, 只有一个上下文, 只能由一个处理器来处理。

所以对于SMP系统, 一般会有一个先启动的core(称为primary core), 由其负责初始化整个系统的资源, 而其他的core则等待这些资源准备好后再开始工作。

对于新的SMP架构,primary core为Core 0(注意此处指的是逻辑ID),由Core 0负责引导这个系统的资源, 如各种外设、memory等。

Core 0在资源引导完毕后, 会释放Core 1,让Core 1开始启动, 之后开始进行系统的任务调度, 整个系统在此时就运行起来了。

<a id="id14"></a>
![SMP boot](../../../_assets/d898e9dfb7a62e412f3b-smp_boot.png)


SMP 启动流程

<a id="id9"></a>

### **SMP编程注意事项**

从软件的时间看, SMP系统与单CPU系统在编程上还是有一些差异的。这些差异主要体现在:

- 虽然外设与内存资源都是共享的, 但是如果多个CPU同时对共享资源进行访问时, 需要加临界区保护。并且此时传统的关中断方式已经不足以起到临界保护作用, 需要采用关中断
  加自旋锁的方式。具体可以参考：[SMP 临界区使用](../ap_doc/os/bk_freertos.md)
- 每个core都有自身的中断管理器, 但外设的中断通常是由某一个core来进行处理。需要根据实际需求配置中断路由。
  具体可以参考： [中断管理](interrupt.md)
- 上层创建的任务可以绑定到SMP系统的某个CPU, 也可以不绑定核, 由内核自行管理。在不绑定核的情形下, 需要注意对访问资源的独占保护。
  创建任务的API可以参考: [OS适配层API](../ap_doc/os/bk_os_abstract.md)
