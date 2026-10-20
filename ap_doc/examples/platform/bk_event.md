---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/platform/bk_event.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="event"></a>

# Event

<a id="id1"></a>

## 1 功能概述

事件框架 CLI，用于注册、注销与投递模块事件。

<a id="id2"></a>

## 2 代码路径

> - demo 路径：`ap/components/bk_cli/cli_event.c`

<a id="id3"></a>

## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_EVENT` | 事件框架 | 依项目配置 |
| `CONFIG_CLI` | CLI 支持 | 依项目配置 |

<a id="cli"></a>

## 4 CLI 命令简介

使用 `event reg {mod_id} {event_id}` 注册回调，`event post` 投递事件，`event unreg` 注销。

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
- [exception](bk_exception.md)
- [ICU](bk_icu.md)
- [项目示例](../projects.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
- [常见问题](../../FAQ.md)
- [支持的外设](../../support_peripherals.md)
