---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_qspi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="qspi"></a>

# [QSPI 使用指南](#id9)

<a id="id1"></a>

目录

- [QSPI 使用指南](#qspi)

  - [概述](#id2)
  - [主要特性](#id3)
  - [内存映射地址](#id4)
  - [QSPI 传输阶段](#id5)
  - [代码路径](#id7)
  - [Kconfig 配置](#kconfig)
  - [典型初始化流程](#id8)
  - [API 参考](#api)

<a id="id2"></a>

## [概述](#id10)

QSPI 作为主设备 (Master) 用于对通用从设备 (Slave)（如 Flash、PSRAM 或显示屏）进行读写操作，支持单线、双线或四线（数据线）SPI 传输。

BK7259 **AP 侧** 提供 **2 路** QSPI 控制器（QSPI0、QSPI1），CP 侧不提供 QSPI 驱动封装，外接 QSPI 设备请在 AP 工程中使用。

QSPI 可在如下两种模式下工作：

- **间接模式**：通过 QSPI 寄存器与 TX/RX FIFO 完成命令与数据传输，适用于 Flash 擦写、命令下发等场景。
- **内存映射模式**：外部设备映射到内部存储地址空间，CPU 可直接按地址读写，适用于 PSRAM、部分 LCD 刷新场景。

相关文档：

- QSPI Flash 使用说明：[QSPI Flash 使用指南](bk_qspi_flash.md)
- QSPI 文件系统：[QSPI 文件系统（VFS/littleFS/FATFS）使用指南](bk_qspi_filesystem.md)
- QSPI PSRAM：[PSRAM 使用指南](bk_psram.md)（合封 PSRAM 与 QSPI 外挂 PSRAM 为不同路径）
- QSPI LCD 显示：[QSPI LCD 显示](../display/qspi_lcd_display.md)
- CLI 示例：[QSPI 示例](../../examples/peripheral/bk_qspi.md)、[QSPI Flash 示例](../../examples/peripheral/bk_qspi_flash.md)

<a id="id3"></a>

## [主要特性](#id11)

- 两种工作模式：间接模式与内存映射模式
- 完全可编程操作码和帧格式
- 集成 FIFO，独立的发射 FIFO 和接收 FIFO（最大 256 字节）
- 收发传输完成可产生中断
- SCK 最高可配置至 **80 MHz**（`bk_qspi_init_by_freq()`）

<a id="id4"></a>

## [内存映射地址](#id12)

QSPI 内存映射基地址由 `QSPI_DCACHE_BASE_ADDR(id)` 定义：

- QSPI0：`0x68000000`
- QSPI1：`0x6C000000`（每个 QSPI 实例间隔 64 MB）

间接模式下，地址由软件通过 CMD 寄存器配置；内存映射模式下，偏移地址由总线自动产生。

<a id="id5"></a>

## [QSPI 传输阶段](#id13)

QSPI 与外部设备之间一般包含如下阶段：CMD 指令阶段、ADDR 地址阶段、WAIT 等待阶段和数据阶段。

<a id="cmd"></a>

### CMD 指令阶段

指令通常为单线模式，也可配置为双线或四线模式。CMD 寄存器最多支持 8 个字节。

有 4 个预设寄存器 CMDA、CMDB、CMDC 和 CMDD，每次 SPI 操作选一个 CMD 模式：

1. **CMDA**：内存映射模式向设备写数据
2. **CMDB**：内存映射模式从设备读数据
3. **CMDC**：间接模式通过 TX FIFO 向设备写数据
4. **CMDD**：间接模式通过 RX FIFO 从设备读数据

使用内存映射模式时，CMDA 和 CMDB 只需配置一次；使用间接模式时，每次 FIFO 操作或下发设备指令都需配置 CMD。

模式选择建议：PSRAM 适用内存映射；Flash 擦写适用间接模式。

<a id="addr"></a>

### ADDR 地址阶段

地址可为单线、双线或四线模式，长度一般为 3\~4 字节。内存映射模式下地址由硬件自动产生；间接模式下，CMDC/CMDD 中 1\~8 字节内容由软件按器件手册配置（指令、地址、Dummy 及线宽）。

<a id="wait"></a>

### WAIT 等待阶段

在两个 CMD 字节之间插入等待时隙，等待周期数由 `DUMMY_CLK` 配置，插入位置由 `DUMMY_MODE` 配置。例如 CMD1 为指令、CMD2\~4 为地址时，可在 CMD4 之后插入 Dummy 周期。

<a id="id6"></a>

### 数据阶段

发送或接收数据，内部 FIFO 最大长度 256 字节。数据阶段线宽由 `DATA_LINE` 配置，长度由 `DATA_LEN` 配置。

间接模式下通过写 TX FIFO / 读 RX FIFO 交互数据；内存映射模式下数据直接来自或回到总线。

<a id="id7"></a>

## [代码路径](#id14)

- 驱动公共层：`middleware/driver/qspi/qspi_driver.c`
- HAL 层：`middleware/soc/bk7259_ap/hal/qspi_hal.c`
- CLI 测试：``` middleware/driver/qspi/qspi_test.c``（需 ``CONFIG_QSPI_TEST ```）

子模块驱动（按 Kconfig 条件编译）：

- NOR/NAND Flash：`components/bk_external_flash/qspi_flash/qspi_nor_flash.c`、`qspi_nand_flash.c`（已从 middleware 迁至 `bk_external_flash` 组件）
- QSPI PSRAM：`middleware/driver/qspi/qspi_psram.c`
- QSPI LCD：`middleware/driver/lcd/lcd_qspi_driver.c`

<a id="kconfig"></a>

## [Kconfig 配置](#id15)

在 `menuconfig` → **QSPI** 中配置：

| 宏 | 说明 |
| --- | --- |
| `CONFIG_QSPI` | QSPI 驱动总开关 |
| `CONFIG_QSPI_STATIS` | QSPI 统计信息 |
| `CONFIG_QSPI_MST_PSRAM` | 外挂 QSPI PSRAM 驱动 |
| `CONFIG_QSPI_NOR_FLASH` | 外挂 QSPI NOR Flash 驱动（与 NAND 互斥） |
| `CONFIG_QSPI_NAND_FLASH` | 外挂 QSPI SPI-NAND 驱动（与 NOR 互斥） |
| `CONFIG_QSPI_NAND_FLASH_SIZE` \| SPI-NAND 容量（字节，默认 128 MB） | |
| `CONFIG_QSPI_LINE_MODE` | Flash 线模式：2\=双线，4\=四线（默认 4） |
| `CONFIG_QSPI_TEST` | CLI 测试命令（依赖 `CONFIG_DRIVER_TEST`） |

<a id="id8"></a>

## [典型初始化流程](#id16)

```
// 1. 初始化 QSPI 驱动公共资源
bk_qspi_driver_init();

// 2. 按目标 SCK 频率初始化指定 QSPI 实例（推荐，自动选时钟源与分频）
bk_qspi_init_by_freq(QSPI_ID_0, 40000000);  // 40 MHz

// 3. 间接模式读写（需先 bk_qspi_command() 配置 CMD）
bk_qspi_write(QSPI_ID_0, tx_buf, len);
bk_qspi_read(QSPI_ID_0, rx_buf, len);

// 4. 使用完毕
bk_qspi_deinit(QSPI_ID_0);
bk_qspi_driver_deinit();
```

外挂 Flash 请使用 [QSPI Flash 使用指南](bk_qspi_flash.md) 中的 `bk_qspi_flash_*` 接口。

<a id="api"></a>

## [API 参考](#id17)

详见 [QSPI API](../../api-reference/peripheral/bk_qspi.md)。
