---
mirror_status: historical-unverified
catalog_checked: '2026-10-21'
---

> 本文件未出现在本次官网默认文档目录中，按历史资料保留；当前资料请从 wiki 的 Beken 官方文档分类进入。

# 五.Bootloader升级固件相关info



- 1.升级固件制作有两种方式：


  - 1）方式一：通过工具手动生成；

  - 2）方式二：由编译打包的时候自动化生成；（首选方式二）

- 2.升级固件路径为：

重要

在bk_avdk_smp/build/bk7259/app/package/app_pack.rbl


- 3.打开Everything-1.4.1.935.x64-Setup.exe，工具->选项->HTTP服务器，绑定本机ip。使用浏览器打开本机的ip地址，找到本地的升级文件 *.rbl，拷贝url出来，用于cli命令。

> ![bootlaoder_everthing](../../../_images/bootlaoder_everthing.png)
>
>
> 图6 Everything工具页面


- 4.使用串口发送cli命令，例如：
  cpu1 http_ota [http://192.168.21.101/D%3A/E/build/app_pack.rbl](http://192.168.21.101/D%3A/E/build/app_pack.rbl "http://192.168.21.101/D%3A/E/build/app_pack.rbl")
