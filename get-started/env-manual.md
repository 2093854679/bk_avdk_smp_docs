---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/get-started/env-manual.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="env-manual"></a>

<a id="id1"></a>

# 本地部署

<a id="linux"></a>

## Linux编译环境

备注

Armino 在Linux下编译环境要求Ubuntu 20.04 LTS 版本及以上，Centos 7版本及以上，Archlinux或者Debian 11版本及以上，本章节将以 Ubuntu 20.04 LTS 版本为例，介绍整个编译环境的搭建。

编译环境可以使用环境安装脚本进行安装，也可以手动安装，这里推荐使用脚本安装的方式。

- 脚本安装：

  > SDK 中存在安装脚本，那么进入 SDK 目录后执行安装脚本，按照安装脚本引导即可完成构建环境安装:
  >
  > ```
  > cd ~/armino/bk_avdk_smp
  > sudo bash tools/env_tools/setup/armino_env_setup.sh
  > ```
  >
  > 如果 SDK 中不存在安装脚本，建议检查 SDK 是否完整，或选择手动安装。
  >
  > 如果安装脚本出现失败，可以根据提示与手动安装指南完成环境搭建。
- 手动安装：

  > 手动安装请参考 [链接](manual_install.md#manual-install)

备注

AP的工具链默认路径在 ap/middleware/soc/bk7259\_ap/soc\_config.mk 文件中定义，CP的工具链默认路径在 cp/middleware/soc/bk7259/soc\_config.mk 文件中定义，您也可以在项目文件pj\_config.mk中更改工具链路径:

```
COMPILER_TOOLCHAIN_PATH := /opt/arm-gnu-toolchain-14.3.rel1-x86_64-arm-none-eabi/bin
```

<a id="windows"></a>

## Windows编译环境

Armino 在Windows下环境要求Windows10及以上64位操作系统，Windows下集成编译环境为Armino Bash，点击 [链接](https://dl.bekencorp.com/d/tools/arminosdk/WindowsInstaller/Armino-Bash-Setup_0.3.0.exe) 下载安装包。
安装路径不能带有中文和空格，安装完成后在桌面生成Armino Bash的快捷图标，双击快捷图标即可进入Armino Bash终端。
Armino Bash终端中基于git bash制作，支持常用的linux的命令和执行shell脚本，路径风格和git bash一致，如 C:\\Programs 在armino bash中表示为 /c/Programs 。

备注

如果需要使用windows风格的路径，可以使用单引号包含，比如：

> cd ‘C:\\Programs’

备注

Windows工具安装路径和SDK代码路径不能带有中文和空格。

<a id="id2"></a>

## 编译工程

在Linux终端中输入下述命令编译 Armino 默认工程，PROJECT为可选参数，默认为app，默认工程为启动 WiFi，BLE，初始化常见驱动，并启动 Armino 默认 Cli 程序:

```
cd ~/armino/bk_avdk_smp
make bk7259
```

更多编译相关命令请参考 [链接](../developer-guide/build_config/bk_build_overview.md#bk-build-overview)
