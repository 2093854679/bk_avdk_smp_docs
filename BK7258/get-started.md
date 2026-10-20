---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7258/zh_CN/v3.1.1/get-started/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: SMP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 快速入门

本文档以 BK7258 开发板为例，通过一个简单的示例项目向您展示:

> - 代码下载；
> - 环境部署及编译；
> - 工程配置；
> - 固件编译与烧录；

<a id="id2"></a>

## 准备工作

硬件：

> - BK7258 开发板( [开发板简介](get-started/bk7258.md#bk7258) ， [购买链接](https://item.taobao.com/item.htm) )；
> - 串口烧录工具；
> - PC；

<a id="armino-sdk"></a>

## Armino SDK 代码下载

您可从 gitlab 上下载 Armino SMP 代码:

```
mkdir -p ~/armino
cd ~/armino
git clone https://gitlab.bekencorp.com/armino/bk_avdk_smp.git -b release/v3.1.1
```

警告

Windows下通过git clone拉取代码，存在换行符的问题，会导致编译失败，请按照以下方式解决:

- 换行符问题:

  1.下载代码前先配置git环境变量:

  ```
  git config --global core.autocrlf false
  ```

备注

gitlab只针对企业用户开放，请找对应接口人申请。

<a id="smp-get-started-env"></a>

<a id="id4"></a>

## 环境部署及编译

我们提供了本地编译环境和Docker编译环境两种部署方式，用户可根据硬件和使用习惯选择一种方式部署，我们更推荐使用本地编译环境。

本地部署方案目前仅支持Windows和Linux系统下的编译。

Docker部署是基于Docker容器的环境部署与编译方案，支持在Linux、macOS及Windows系统上高效完成编译工作。
借助Docker容器化技术，您无需手动安装编译所需的各类库文件及工具链，从而显著简化了部署与编译流程。
该方案适用于熟悉Docker环境并了解其基本使用方法的用户，可帮助您快速实现环境的部署与编译。
对于不熟悉Docker技术或因网络条件限制无法使用Docker环境的用户，请使用本地编译部署方案。

- [本地部署](get-started/env-manual.md)
- [Docker部署](get-started/env-docker.md)

<a id="id5"></a>

## 配置工程

- 您可以通过工程配置文件来进行更改默认配置或者针对不同芯片进行差异化配置:

  ```
  工程配置文件 Override 芯片配置文件 Override 默认配置
  如： projects/app/ap/config/bk7258_ap/config >> ap/middleware/soc/bk7258_ap/bk7258_ap.defconfig >> KConfig
  + 工程配置文件示例：
      projects/app/ap/config/bk7258_ap/config
      projects/app/cp/config/bk7258/config
  + 芯片配置文件示例：
      ap/middleware/soc/bk7258_ap/bk7258_ap.defconfig
      cp/middleware/soc/bk7258/bk7258.defconfig
  + KConfig 配置文件示例：
      ap/middleware/arch/cm33/Kconfig
      ap/components/bk_cli/Kconfig
      cp/middleware/arch/cm33/Kconfig
      cp/components/bk_cli/Kconfig
  ```
- 模块选择CPUx执行

  > - 目前BK7258是三核系统架构，CPU1,CPU2组成应用处理器(AP)，为SMP架构，CPU0为通信处理器(CP)，AP和CP组成AMP架构，各自独立编译。
  > - 比如TRNG随机数控制器只有一份，使用多核配置时，应用程序需要互斥配置在哪一个系统(AP/CP)中执行。
  > - 模块的功能开关CONFIG\_TRNG宏默认关闭, 若AP或CP系统需要, 应在相应的系统的配置文件中打开。
  >   假设CP需要使用TRNG，而AP不需要使用，则在cp的默认配置文件bk7258.defconfig中的CONFIG\_TRNG\=y。
  > - 在软件代码中，使用CONFIG\_TRNG宏隔离调用。
  >   示例如下:
  >
  >   ```
  >   #if CONFIG_TRNG             #使用模块功能开关宏隔离代码
  >   #include "driver/trng.h"
  >   #endif
  >   ...
  >   #if CONFIG_TRNG             #使用模块功能开关宏隔离代码
  >   bk_rand();
  >   #endif
  >   ```

<a id="id6"></a>

## 新建工程

- 新建工程介绍: [create\_new\_project](developer-guide/create_new_project_rule/bk_configure_partition_Table.md)
- 创建工程后，可以进行menuconfig配置，配置方法参考 [menuconfig 配置](developer-guide/config_tools/bk_config_kconfig.md#bk-config-menuconfig)

<a id="smp-get-started-flash"></a>

<a id="id7"></a>

## 烧录代码

Armino 支持在 Windows/Linux 平台进行固件烧录, 烧录方法参考烧录工具中指导文档。
以Windows 平台为例， Armino 目前支持 UART 烧录。
app工程在编译完成后，在build/bk7258/app/package目录下生成all-app.bin，使用此bin文件烧录即可。

<a id="id8"></a>

### 通过串口烧录

备注

Armino 支持 UART 烧录，推荐使用 CH340 串口工具小板进行下载。BEKEN 串口工具小板 [淘宝链接](https://www.taobao.com/list/item/Z0RXSzFtdXdMU2FEYit2RzdVdEdTdz09.htm) 。

串口烧录工具如下图所示:

<a id="id10"></a>
![Uart](../../_assets/78fa1c9aded901b1a5fc-download_tool_uart.png)


UART

烧录工具（BKFIL）获取：

> <https://dl.bekencorp.com/tools/bkfil/v4>
> 在此目录下获取对应系统的最新版本。

BKFIL.exe 界面及相关配置如下图所示：

<a id="id11"></a>
![BKFIL GUI](../../_assets/78ebd6b027ef3147b89c-download_all_app.png)


BKFIL GUI

选择烧录串口 DL\_UART0，点击 `烧录` 进行版本烧录, 烧录完成之后掉电重启设备。
如果烧录过程无法获取设备，卡在 `Getting Bus...` 时，可以按一下重启键，恢复cpu状态。

点击 [BKFIL](../../bk_toolkit/bkfil/intro/intro.md) 进一步了解 Armino 烧录工具。

<a id="log"></a>

## 开机log和命令行工具

烧录后连接串口DL\_UART0(UART0)，设置波特率为115200，开机后即可看到开机log。
在BK7258 SMP系统中，Cli 命令通过也通过DL\_UART0(UART0)串口进行通信；使用串口通信工具输入help 命令查看支持命令列表。
