# 构建概述



## 基本概念

> - `项目` - 特指 armino/projects/ 下一个目录或者子目录，其中包含了构建可执行应用程序所需的全部文件和配置，以及其他支持型文件，例如分区表、数据/文件系统分区和引导程序。
> - `项目配置` - 特指构建过程中在构建目录build下生成的 sdkconfig.h 文件。如app工程的sdkconfig.h位于build/bk7259/app/bk7259/config目录下。
> - `应用程序` - 是由 ARMINO 构建得到的可执行文件。一个项目通常会构建两个应用程序：项目应用程序（可执行的主文件，即用户自定义的固件）和引导程序（启动并初始化项目应用程序）。
> - `组件` - 是模块化且独立的代码，会被编译成静态库（.a 文件）并链接到应用程序。
> - `目标` - 特指运行构建后应用程序的硬件设备，如 bk7259 等。


## 项目示例


```

- armino/

    - ap/

        - components/

        - include/

        - middleware/

            - arch/

                - bk7259_ap/

                    - bk7259_ap.defconfig

                    - ...

    - cp/

        - components/

        - include/

        - middleware/

            - arch/

                - bk7259/

                    - bk7259.defconfig

                    - ...

    - projects/

        - my_project/

            - ap/

                - config/

                    - bk7259_ap/config

                - CMakeLists.txt

                - main/

                    - main.c

                    - Kconfig

                    - CMakeLists.txt

            - cp/

                - config/

                    - bk7259/config

                - CMakeLists.txt

                - main/

                    - main.c

                    - Kconfig

                    - CMakeLists.txt

            - components/

                - c1/

                    - c1.c

                    - Kconfig

                    - CMakeLists.txt

                - c2/

```


## 使用 make 触发构建

在 armino 根目录下运行　make， 最常用的 make 命令如下：

> - `make bkxxx` - 构建目标 bkxxx，项目为默认项目 armino/projects/app 示例： make bk7259
> - `make bkxxx PROJECT=a/b` - 构建 bkxxx，项目为 armino/projects/a/b 示例： make bk7259 PROJECT=a/b
> - `make clean` - 清理所有目标
> - `make bkxxx_ap` - 单独构建 bkxxx AP，项目为默认项目 armino/projects/app 示例： make bk7259_ap PROJECT=app
> - `make bkxxx_cp` - 单独构建 bkxxx CP，项目为默认项目 armino/projects/app 示例： make bk7259_cp PROJECT=app

make 构建是通过 armino/Makefile 间接调用 armino 工具来进行构建，它省去了使用 armino 工具构建时要
设置环境变量的麻烦，推荐您使用这种方式进行构建。

同时也可以在工程目录下执行make命令，无需再指定工程：

> - `make bkxxx` - 构建目标，项目为当前项目
> - `make clean` - 清理构建内容

编译成功后，在build目录下将生成all-app.bin文件，如app工程的all-app.bin文件位于build/bk7259/app/package目录下，烧录此文件既可。


## 编译版本

通过config可以配置编译版本，默认编译类型为Release版本。
在工程config文件中添加以下配置可以显示指定编译Debug版本:

> CONFIG_DEBUG_VERSION=y

在工程config文件中添加以下配置可以显示指定编译Release版本:

> CONFIG_RELEASE_VERSION=y

Debug和Release版本的区别:

> 1. Debug版本会定义CONFIG_DEBUG_VERSION=1，Release版本会定义CONFIG_RELEASE_VERSION=1。
> 2. Debug版本出现异常或者Assert时，会Dump所有内存信息和寄存器信息，然后重启；Release版本出现异常或者Assert时，直接重启。
>    在Release版本下打开CONFIG_DUMP_ENABLE宏即可Dump所有内存信息和寄存器信息。
