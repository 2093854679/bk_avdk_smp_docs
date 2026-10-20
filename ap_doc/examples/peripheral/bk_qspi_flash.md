---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_qspi_flash.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="qspi-flash"></a>

# QSPI Flash

<a id="id1"></a>

## 1 功能概述

QSPI Flash 示例演示如何通过 AP 侧 QSPI 控制器读写外挂 NOR Flash 或 SPI-NAND。

- 驱动说明：[QSPI Flash 使用指南](../../developer-guide/peripheral/bk_qspi_flash.md)
- QSPI 控制器：[QSPI 使用指南](../../developer-guide/peripheral/bk_qspi.md)

<a id="id2"></a>

## 2 代码路径

- CLI 测试：`components/bk_external_flash/qspi_flash/qspi_flash_test.c`（NOR/NAND Flash CLI）；QSPI 控制器/PSRAM CLI 仍在 `middleware/driver/qspi/qspi_test.c`
- NOR Flash 驱动：`components/bk_external_flash/qspi_flash/qspi_nor_flash.c`
- SPI-NAND 驱动：`components/bk_external_flash/qspi_flash/qspi_nand_flash.c`

<a id="id3"></a>

## 3 宏配置

在 QSPI 基础配置之上，选择器件类型（二选一）：

| NAME | Description |
| --- | --- |
| CONFIG\_QSPI\_NOR\_FLASH | NOR Flash 驱动 |
| CONFIG\_QSPI\_NAND\_FLASH | SPI-NAND 驱动 |
| CONFIG\_QSPI\_LINE\_MODE | 线模式：2\=双线，4\=四线（默认 4） |
| CONFIG\_QSPI\_TEST | 启用 CLI 测试命令 |

<a id="id4"></a>

## 4 硬件连接

开发板通过 QSPI 外接 Flash 的典型连接：

<a id="id6"></a>
![QSPI Flash 硬件连接](../../../../_assets/730fadef680f57fc572e-qspi_flash_board.png)


Figure 1\. 开发板通过 QSPI 外接 Flash

外接 Flash 通常使用 3.3 V 供电。管脚定义见 [QSPI 示例](bk_qspi.md) PIN 脚章节。

<a id="cli"></a>

## 5 CLI 命令

需开启 `CONFIG_QSPI`、`CONFIG_QSPI_TEST` 及 ``` CONFIG_QSPI_NOR_FLASH``（或 ``CONFIG_QSPI_NAND_FLASH ```）。

备注

QSPI 驱动运行在 AP 侧，从串口下发命令需加 ``` ap_cmd `` 前缀（本 SMP SDK 用法），
例如 ``ap_cmd qspi_flash 1 get_id ```。下表 Command 列为简洁省略前缀，实际输入请补上。

<a id="nor-flash-config-qspi-nor-flash"></a>

### NOR Flash 命令（`CONFIG_QSPI_NOR_FLASH`）

| Command | Param | Description |
| --- | --- | --- |
| **qspi\_flash** **{id}** **get\_id** | id: 0\~1 | 读取 Flash JEDEC ID，并尝试解除保护、使能 QE |
| **qspi\_flash** **{id}** **read** **{addr} {len}** | addr: 偏移地址，len: 长度 | 按 `CONFIG_QSPI_LINE_MODE` 读写 |
| **qspi\_flash** **{id}** **write** **{addr} {len}** | 同上 | 写入（写入前需先擦除） |
| **qspi\_flash** **{id}** **erase** **{addr} {len}** | 同上 | 擦除（按扇区对齐） |
| **qspi\_flash** **{id}** **read\_sr** **\[reg\]** | reg: 0\=S0-S7, 1\=S8-S15, 2\=S16-S23 | 读状态寄存器 |
| **qspi\_flash** **{id}** **write\_sr** **{reg} {val}** | reg \+ 十六进制值 | 写状态寄存器 |
| **qspi** **{id}** **flash\_test** **{addr} {len}** | 同上 | 一键测试：get\_id → 擦除 → 写 → 读 |
| **qspi** **{id}** **flash\_write\_read\_test** **{addr} {len}** | 同上 | 详细擦写读验证（含状态寄存器检查） |

<a id="spi-nand-flash-config-qspi-nand-flash"></a>

### SPI-NAND Flash 命令（`CONFIG_QSPI_NAND_FLASH`）

命令前缀为 `qspi_nand`，默认操作 QSPI0。NAND 页大小 2048 字节、每块 64 页（128 KB）。

| Command | Description |
| --- | --- |
| **qspi\_nand init** | 初始化 QSPI 驱动与 NAND |
| **qspi\_nand get\_id** | 读取 NAND JEDEC ID |
| **qspi\_nand protect\_none** | 解除块写保护 |
| **qspi\_nand quad\_enable** | 清 WP-E，使能四线模式 |
| **qspi\_nand get\_feature {addr}** | 读特征寄存器 |
| **qspi\_nand set\_feature {addr} {value}** | 写特征寄存器 |
| **qspi\_nand block\_erase {block}** | 擦除指定块（128 KB） |
| **qspi\_nand page\_program {page} {column} {pattern} {len}** | 单线写页（pattern 为填充字节） |
| **qspi\_nand page\_read {page} {column} {len}** | 单线读页 |
| **qspi\_nand page\_program\_quad {page} {column} {pattern} {len}** | 四线写页 |
| **qspi\_nand page\_read\_quad {page} {column} {len}** | 四线读页 |
| **qspi\_nand page\_test {page}** | 单页 擦除→写→读 校验 |
| **qspi\_nand block\_test {block}** | 整块 擦除→写→读 校验 |
| **qspi\_nand factory\_bad {block}** | 检查出厂坏块标记 |

<a id="spi-nand-bbm"></a>

### SPI-NAND 坏块管理（BBM）命令

BBM 层为 littleFS on NAND 提供连续好块逻辑地址空间。

| Command | Description |
| --- | --- |
| **qspi\_nand bbm init** | 初始化坏块管理层，打印逻辑空间大小 |
| **qspi\_nand bbm dump** | 打印坏块表（BBT）：布局、坏块、重映射 |
| **qspi\_nand bbm inject {logical\_block}** | 强制退役并重映射一个逻辑块（测试用） |

备注

`qspi_nand` 系列为 NAND 裸驱动/坏块层测试命令，主要用于产线与调试。
日常文件读写请使用 VFS 接口，见
[QSPI 文件系统（VFS/littleFS/FATFS）使用指南](../../developer-guide/peripheral/bk_qspi_filesystem.md)。

<a id="nor-flash"></a>

## 6 命令行演示（NOR Flash）

1. 初始化 QSPI 驱动与 QSPI1：

```
ap_cmd qspi_driver init
ap_cmd qspi 1 set_clk 40000000
```

2. 获取 Flash ID（同时解除保护并使能 QE）：

```
ap_cmd qspi_flash 1 get_id
```

3. 擦除 4 KB 扇区：

```
ap_cmd qspi_flash 1 erase 0 4096
```

4. 写入 256 字节：

```
ap_cmd qspi_flash 1 write 0 256
```

5. 读取验证：

```
ap_cmd qspi_flash 1 read 0 512
```

6. 一键测试：

```
ap_cmd qspi 1 flash_test 0 256
```

<a id="spi-nand-flash"></a>

## 7 命令行演示（SPI-NAND Flash）

1. 初始化并读取 ID：

```
ap_cmd qspi_nand init
ap_cmd qspi_nand get_id
```

2. 解除保护、使能四线：

```
ap_cmd qspi_nand protect_none
ap_cmd qspi_nand quad_enable
```

3. 单页擦写读校验（page 0）：

```
ap_cmd qspi_nand page_test 0
```

4. 查看坏块表：

```
ap_cmd qspi_nand bbm init
ap_cmd qspi_nand bbm dump
```

<a id="id5"></a>

## 8 常见问题

A）获取 Flash ID 失败
:   - 检查 3.3 V 供电与管脚连接
    - 确认 QSPI 已初始化，SCK 不超过 80 MHz

B）读 ID 正确但擦写失败
:   - 确认已执行 `get_id`（内部会解除保护并使能 QE）
    - 写入前必须先擦除对应区域
    - 不同厂商状态寄存器位域不同，可用 `read_sr` / `write_sr` 调试

更多说明见 [QSPI Flash 使用指南](../../developer-guide/peripheral/bk_qspi_flash.md)。
