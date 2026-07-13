# 手动安装



## 安装步骤

> - 工具链下载与安装
> - 程序编译依赖库安装


## 工具链下载与安装

点击 [下载](https://dl.bekencorp.com/tools/toolchain/arm/arm-gnu-toolchain-14.3.rel1-x86_64-arm-none-eabi.tar.xz "https://dl.bekencorp.com/tools/toolchain/arm/arm-gnu-toolchain-14.3.rel1-x86_64-arm-none-eabi.tar.xz") 下载 BK7259 工具链。

工具包下载后，通过如下操作命令解压至 /opt/ 目录下:


```
$ sudo tar -xJf arm-gnu-toolchain-14.3.rel1-x86_64-arm-none-eabi.tar.xz -C /opt/

```


## 程序编译依赖库安装

使用Ubuntu或Debian操作系统，需要输入以下命令:


```
sudo apt update
sudo apt install make cmake python3 python3-pip ninja-build -y

```

使用Centos操作系统，需要输入以下命令:


```
sudo yum update
sudo yum install -y python38 make git cmake3 ninja-build bzip2 wget

```

使用Archlinux操作系统，需要输入以下命令:


```
sudo pacman -Syyu
sudo pacman -S --noconfirm make wget git cmake python3 python-pip python-setuptools ninja

```

在终端输入下述命令安装python依赖库:


```
sudo pip3 install pycryptodome click future click_option_group cryptography jinja2 PyYAML cbor2 intelhex

```

如果您的 Python 默认为 Python2，请使用下述命令更改成 Python3，Python最低要求版本为Python3.8:


```
sudo ln -s /usr/bin/python3 /usr/bin/python

```

备注

如果Ubuntu版本在23.04以上，python的三方库会使用外部环境管理，使用pip安装三方库时需要传入–break-system-packages。
Centos7 从软件源无法安装python3.8，需要使用源码编译方式安装。
