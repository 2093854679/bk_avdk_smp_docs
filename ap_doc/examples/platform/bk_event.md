# Event



## 1 功能概述

事件框架 CLI，用于注册、注销与投递模块事件。


## 2 代码路径

> - demo 路径：`ap/components/bk_cli/cli_event.c`


## 3 宏配置

| NAME | Description | 说明 |
| --- | --- | --- |
| `CONFIG_EVENT` | 事件框架 | 依项目配置 |
| `CONFIG_CLI` | CLI 支持 | 依项目配置 |


## 4 CLI 命令简介

使用 `event reg {mod_id} {event_id}` 注册回调，`event post` 投递事件，`event unreg` 注销。
