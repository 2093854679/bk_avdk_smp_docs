---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_qspi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="qspi"></a>

# QSPI

<a id="id1"></a>

## 1 功能概述

BK7259 AP 侧具有 **2 路** QSPI 控制器（QSPI0、QSPI1），用于驱动外挂 Flash、PSRAM 或 QSPI LCD 等从设备。

工作模式：

- **间接模式**：通过寄存器与 FIFO 操作，适用于 Flash 命令下发
- **内存映射模式**：设备映射到 `0x68000000` 起地址空间，适用于 PSRAM / 部分 LCD 场景
- QSPI 控制器说明：[QSPI 使用指南](../../developer-guide/peripheral/bk_qspi.md)
- QSPI Flash 演示：[QSPI Flash 示例](bk_qspi_flash.md)
- QSPI LCD 演示：[QSPI LCD 显示示例](../../developer-guide/display/qspi_lcd_display.md)

<a id="id2"></a>

## 2 代码路径

- CLI 测试：``` middleware/driver/qspi/qspi_test.c``（需 ``CONFIG_QSPI_TEST ```）
- 驱动源码：`middleware/driver/qspi/qspi_driver.c`

<a id="id3"></a>

## 3 QSPI 相关宏配置

| NAME | Description | File | value |
| --- | --- | --- | --- |
| CONFIG\_QSPI | QSPI 驱动总开关 | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | y |
| CONFIG\_QSPI\_TEST | QSPI CLI 测试命令 | 工程 defconfig | y/n |
| CONFIG\_QSPI\_MST\_PSRAM | 外挂 QSPI PSRAM 驱动 | 工程 defconfig | y/n |
| CONFIG\_QSPI\_NOR\_FLASH | 外挂 QSPI NOR Flash 驱动 | 工程 defconfig | y/n |
| CONFIG\_QSPI\_NAND\_FLASH | 外挂 QSPI SPI-NAND 驱动 | 工程 defconfig | y/n |
| CONFIG\_QSPI\_LINE\_MODE | Flash 线模式（2\=双线，4\=四线） | 工程 defconfig | 4 |

<a id="qspi-pin"></a>

## 4 QSPI PIN 脚描述

QSPI0（组 0）：

| QSPI0 功能 | GPIO |
| --- | --- |
| QSPI0\_SCK | GPIO22 |
| QSPI0\_CS | GPIO23 |
| QSPI0\_DAT\[0\] | GPIO24 |
| QSPI0\_DAT\[1\] | GPIO25 |
| QSPI0\_DAT\[2\] | GPIO26 |
| QSPI0\_DAT\[3\] | GPIO27 |

QSPI1（组 0）：

| QSPI1 功能 | GPIO |
| --- | --- |
| QSPI1\_SCK | GPIO2 |
| QSPI1\_CS | GPIO3 |
| QSPI1\_DAT\[0\] | GPIO4 |
| QSPI1\_DAT\[1\] | GPIO5 |
| QSPI1\_DAT\[2\] | GPIO6 |
| QSPI1\_DAT\[3\] | GPIO7 |

<a id="qspi-cli"></a>

## 5 QSPI CLI 命令

需开启 `CONFIG_QSPI` 与 `CONFIG_QSPI_TEST`。

| Command | Param | Description |
| --- | --- | --- |
| **qspi\_driver** **{init\|deinit}** | init / deinit | 初始化/反初始化 QSPI 驱动公共资源 |
| **qspi** **{id}** **init** **{src\_clk} {src\_clk\_div} {clk\_div}** | id: 0\~1；src\_clk: 0\=160M, 1\=240M；src\_clk\_div: 0\~15 | 初始化 QSPI 并配置时钟；实际 SCK \= src\_clk / (1 \+ src\_clk\_div)；clk\_div 参数已忽略 |
| **qspi** **{id}** **set\_clk** **{hz}** | hz: 目标 SCK 频率（1\~80000000） | 按频率自动选时钟源与分频（推荐） |

<a id="id4"></a>

## 6 QSPI 初始化演示

1. 初始化 QSPI 驱动公共资源：

```
qspi_driver init
```

2. 按目标频率初始化 QSPI1（推荐）：

```
qspi 1 set_clk 40000000
```

或手动指定时钟源与分频：

```
qspi 1 init 0 3 0
```

（160 MHz / (1\+3) \= 40 MHz）

3. 反初始化：

```
qspi 1 deinit
qspi_driver deinit
```

Flash 相关 CLI 命令见 [QSPI Flash 示例](bk_qspi_flash.md)。
