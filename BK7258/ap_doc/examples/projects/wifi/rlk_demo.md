---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/examples/projects/wifi/rlk_demo/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="rlk-demo"></a>

# rlk\_demo 工程中文说明

本工程是 BK7258 SMP 的 BK-RLK（Raw Link，原链路）演示。启动时在 AP 核初始化 RLK、随机选信道并注册 CLI，可通过 ping / iperf 等命令做配对与吞吐测试。

开发者指南：`ap/docs/bk7258/zh_CN/developer-guide/wifi/bk_rlk.rst`。

<a id="id1"></a>

## 1\. 目录结构

```
rlk_demo/
├── CMakeLists.txt                 # 顶层 CMake 构建入口
├── Makefile                       # Make 构建入口
├── app.rst                        # Sphinx 工程说明
├── ap/                            # AP 核业务代码
│   ├── ap_main.c                  # AP 入口；初始化 RLK 并注册 CLI
│   ├── include/                   # RLK demo / ping / iperf 头文件
│   ├── src/                       # rlk_demo_cli、rlk_ping、rlk_iperf
│   └── config/                    # BK7258 AP 侧配置
├── cp/                            # CP 核代码
│   ├── cp_main.c                  # CP 入口；拉起 AP 核
│   └── config/                    # BK7258 CP 侧配置
└── partitions/                    # 分区与 RAM 区域配置
```

<a id="id2"></a>

## 2\. 功能特点

- 启动即调用 `bk_rlk_init()`，随机信道 `1`–`13`，并注册接收回调。
- `rlk_ping`：按对端 MAC 做原链路 ping。
- `rlk_iperf`：原链路 client / server 吞吐测试。
- 角色与信道：`rlk_master`、`rlk_slave`、`rlk_dubid`、`rlk_chan`、`rlk_scan`、`rlk_acs`。

<a id="id3"></a>

## 3\. 硬件与配置

- 硬件：两块 BK7258 SMP 开发板（或一块板 \+ 支持 BK-RLK 的对端）；UART0 作为 AP 核 CLI。
- 通信前两侧信道必须一致；可用 `rlk_chan` 对齐，不要依赖启动时的随机信道。
- Flash / RAM：使用本工程默认分区即可。

<a id="id4"></a>

## 4\. 编译与烧录

```
make bk7258 PROJECT=wifi/rlk_demo
```

按 SDK 烧录工具烧录 AP/CP 镜像后复位开发板。

<a id="id5"></a>

## 5\. 运行流程

在 **AP 核** 串口操作。两侧先对齐信道，再 ping 或 iperf。

1. 设置信道（两侧相同，例如 6）：

   > rlk\_chan 6
2. 可选角色 / 扫描：

   > rlk\_master
   > rlk\_slave role
   > rlk\_slave ssid \<ssid\>
   > rlk\_slave bssid \<12位十六进制，无冒号\>
   > rlk\_scan
   > rlk\_acs
3. Ping 对端（MAC 为完整 6 字节，或后 3 字节，此时前 3 字节按 `c8:47:8c` 补齐）：

   > rlk\_ping \<mac\>
   > rlk\_ping \<mac\> -c 4 -i 1 -s 32 -t 1
   > rlk\_ping –stop
4. 原链路 iPerf（一侧 server，一侧 client）：

   > rlk\_iperf -s -i 1
   > rlk\_iperf -c \<peer\_mac\> -i 1 -t 60 -b 20M
   > rlk\_iperf –stop
   > rlk\_iperf -h

典型双板流程：两侧 `rlk_chan` 到同一信道；一侧 `rlk_iperf -s`，另一侧 `rlk_iperf -c <对端MAC>`。

<a id="id6"></a>

## 6\. 常见问题

- **没有 \`\`rlk\_ping\`\` / \`\`rlk\_iperf\`\` 命令**：确认烧录的是本工程。
- **ping / iperf 无响应**：两侧信道必须一致；client 的 MAC 必须是对端 STA MAC。
- **启动后信道不一致**：`ap_main` 会随机选信道，测试前务必两边都执行 `rlk_chan`。
- **client 报未连接**：先在对端启动 `rlk_iperf -s`，再发 `-c`；必要时 `--stop` 后重试。
