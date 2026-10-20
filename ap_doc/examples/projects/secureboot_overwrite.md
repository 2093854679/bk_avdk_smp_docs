---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/secureboot_overwrite/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="overwrite-ota"></a>

# 安全启动 Overwrite OTA 工程

<a id="id1"></a>

## 工程概述

`secureboot_overwrite` 演示 BK7259 安全启动流程和单执行槽 Overwrite OTA 升级方案。

生成的软件包包含安全启动元数据、二级引导程序、安全服务固件、CP 应用和 AP 应用。升级时，签名并压缩的镜像写入 `ota` 暂存分区；复位后，引导程序校验镜像并覆盖可执行的 `primary_all` 槽。`ota_control` 分区记录升级进度，用于掉电恢复。

<a id="id2"></a>

## 工程目录

- `ap/` 和 `cp/`：AP/CP 非安全应用入口和配置
- `config/bk7259/config`：启用安全固件打包
- `config/key/`：示例签名密钥文件
- `partitions/bk7259/auto_partitions.csv`：单执行槽和 OTA 暂存区布局
- `partitions/bk7259/security.csv`：安全打包配置
- `partitions/bk7259/pack.json`：输出镜像组成

<a id="id3"></a>

## 编译

在 SDK 根目录执行：

```
make bk7259 PROJECT=secureboot_overwrite
```

<a id="id4"></a>

## 运行与验证

1. 执行编译命令，生成的安全启动镜像，生成路径buildbk7259secureboot\_overwritepackage；
2. 通过BKFIL工具下载生成路径下的bootloader.bin，烧写otp\_efuse\_config.json中的默认密钥到OTP；
3. 下载all-app.bin；
4. 复位开发板，确认 CP 日志显示已进入非安全应用，且 AP 能正常启动。
5. 通过已启用的 OTA 流程将兼容的签名 OTA 镜像写入 `ota` 暂存分区。
6. 再次复位，确认引导程序将镜像安装到 `primary_all`。

<a id="id5"></a>

## 安全注意事项

- `config/key/` 中的密钥仅供 SDK 示例使用，量产前必须替换为受保护的产品密钥。
- 私钥不得提交到源码仓库，也不得放入固件交付包。
- 修改分区名称或大小前，必须检查 `auto_partitions.csv` 中记录的安全打包和引导程序约束。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [项目示例](../projects.md)
- [私有 2.4GHz（BK24G）收发示例工程](24g.md)
- [AP 仿真启动工程](ap_emuboot.md)
- [AP Powerdown Keepalive 示例工程](ap_powerdown_keepalive.md)
- [默认应用工程](app.md)
- [A/B OTA 应用工程](app_ab.md)
- [bluetooth](bluetooth.md)
- [Flash / PSRAM 硬件验证工程](flash_psram_test.md)
- [KVS AWS Sample 示例工程](kvs_aws_sample.md)
- [lvgl](lvgl.md)
- [lwIP PSRAM 示例工程](lwip_psram_example.md)
- [multimedia](multimedia.md)
- [pm](pm.md)
- [安全启动 Overwrite OTA 工程（关闭 Flash AES）](secureboot_overwrite_no_en.md)
- [安全启动 XIP OTA 工程](secureboot_xip.md)
- [SRAM Lite 工程](sram_lite.md)
- [test](test.md)
- [tflite micro](tflite_micro.md)
- [Wi-Fi 项目示例](wifi.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
