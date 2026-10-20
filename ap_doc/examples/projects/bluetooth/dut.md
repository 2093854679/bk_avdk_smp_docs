---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/projects/bluetooth/dut/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="bluetooth-dut"></a>

# Bluetooth DUT 测试

本工程用于在 BK7259 上进行 Bluetooth DUT（Device Under Test）测试，可通过 CLI 命令控制设备进入或退出 DUT 模式。

<a id="id1"></a>

## 支持的芯片

| 芯片 | 状态 |
| --- | --- |
| BK7259 | 支持 |

<a id="id2"></a>

## 1\. 工程概述

本工程启动后默认进入 Bluetooth DUT 测试模式，也可通过 `bt_dut_test` CLI 命令控制 DUT 模式。

经典蓝牙设备名称为 `BK_DUT_TEST`。

<a id="id3"></a>

## 2\. 测试环境

| 项目 | 要求 |
| --- | --- |
| 目标板 | BK7259 开发板 |
| 测试仪表 | CMW 或其他支持 Bluetooth DUT 测试的仪表 |
| 串口 | UART0，用于烧录、日志和 CLI 命令 |
| 硬件配置 | 必须短接串口小板上的 ATE 跳线 |
| 固件产物 | `build/bk7259/dut/package/all-app.bin` |

<a id="id4"></a>

## 3\. 编译与烧录

在 SDK 根目录编译：

```
make bk7259 PROJECT=bluetooth/dut
```

使用 Docker 编译：

```
./dbuild.sh make bk7259 PROJECT=bluetooth/dut
```

使用 BKFIL 或项目标准烧录工具烧录合并镜像：

```
build/bk7259/dut/package/all-app.bin
```

<a id="id5"></a>

## 4\. 测试流程

1. 将 `all-app.bin` 烧录到 BK7259 开发板。
2. 短接串口小板上的 ATE 跳线。
3. 连接 UART0，并重新给开发板上电。
4. 等待以下日志：

```
DUT test initialized and enabled
```

5. 在测试仪表上搜索 `BK_DUT_TEST`，连接设备并执行所需的 Bluetooth DUT 测试。
6. 测试结束后关闭 DUT 模式：

```
ap_cmd bt_dut_test disable
```

本工程在 ATE 跳线生效时仍会启动 AP，以保证 AP CLI 命令可用。

<a id="cli"></a>

## 5\. CLI 命令

在 BK7259 SMP 架构中，该命令注册在 AP 上，因此必须添加 `ap_cmd` 前缀。

| 命令 | 说明 |
| --- | --- |
| `ap_cmd bt_dut_test enable` | 启动 Controller DUT 模式，开启经典蓝牙 Inquiry/Page Scan，并发送 HCI opcode `0x1803`。 |
| `ap_cmd bt_dut_test disable` | 停止 Controller DUT 模式，并关闭经典蓝牙 Inquiry/Page Scan。 |
| `ap_cmd bt_dut_test scan_enable` | 仅开启经典蓝牙 Inquiry/Page Scan，不启动 DUT 模式。 |

命令执行成功返回：

```
DUT TEST RSP:OK
```

命令参数错误或底层操作失败返回：

```
DUT TEST RSP:ERROR
```

<a id="id6"></a>

## 6\. 问题排查

<a id="cmd-not-found-bt-dut-test"></a>

### 提示 `cmd NOT found: bt_dut_test`

确认已烧录 `bluetooth/dut` 工程固件，并等待 `DUT test initialized and enabled` 日志出现后再输入命令。命令必须包含 `ap_cmd` 前缀。

<a id="id7"></a>

### 测试仪表搜索不到设备

确认命令返回 `DUT TEST RSP:OK`，然后执行：

```
ap_cmd bt_dut_test scan_enable
```

重新搜索 `BK_DUT_TEST`。

<a id="dut"></a>

### DUT 模式未启动

确认 ATE 跳线在上电前已经短接。改变跳线状态后，需要重新给开发板上电。

<a id="id8"></a>

## 7\. 注意事项

- 本工程仅支持 BK7259 AP/CP 架构。
- DUT 测试必须使用本工程固件；普通 Bluetooth 示例在 ATE 跳线生效时不会启动 AP。
- 测试结束后建议执行 `disable`，断开 ATE 跳线并重新上电，以恢复普通运行 模式。
