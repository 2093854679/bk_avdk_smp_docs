---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/platform/bk_icu.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="icu"></a>

# ICU

<a id="id1"></a>

## 1 功能概述

中断控制器 CLI，用于查询与配置中断相关状态。

<a id="id2"></a>

## 2 代码路径

> - demo 路径：`ap/components/bk_cli/cli_icu.c`

<a id="id3"></a>

## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_CLI` | CLI 支持 | 依项目配置 |

<a id="cli"></a>

## 4 CLI 命令简介

使用 `icu` 命令查看或配置中断控制器状态（子命令以 `help` 为准）。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [命令](../cli.md)
- [外设](../peripheral.md)
- [平台](../platform.md)
- [os](bk_os.md)
- [log_set](bk_log_set.md)
- [power manager](bk_pwr.md)
- [multi-core mailbox](bk_logic_mailbox.md)
- [event](bk_event.md)
- [exception](bk_exception.md)
- [项目示例](../projects.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
