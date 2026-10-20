---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_spi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="spi"></a>

# SPI

<a id="id1"></a>

## 1 功能概述

> BK7259 AP 支持 1\~4 路 SPI 控制器（SPI0\~SPI3），数量由 `CONFIG_SOC_SPI_UNIT_NUM` 决定，SDK 默认 2 路（SPI0、SPI1）。
>
> SPI 支持主/从模式、三线/四线全双工同步传输，常用于 LCD 等外设；外置 Flash 推荐使用 QSPI（见 [QSPI 示例](bk_qspi.md)），
> SPI Flash 仅用于兼容/调试（`CONFIG_SPI_MST_FLASH`，默认关闭）。
> SPI0\~SPI3 的 SCK/CSN/MOSI/MISO 均可灵活映射到任意合法 GPIO，用户在工程 `usr_gpio_cfg.h` 中配置即可。
>
> - SPI 驱动原理: [SPI 使用指南](../../developer-guide/peripheral/bk_spi.md)
> - GPIO 引脚配置: [GPIO 使用指南](../../developer-guide/peripheral/bk_gpio.md)

<a id="id3"></a>

## 2 代码路径

> - CLI 测试命令（`CONFIG_SPI_TEST=y`）：
>   :   `ap/middleware/driver/spi/spi_test.c`
> - 驱动源码：
>   :   `ap/middleware/driver/spi/spi_driver.c`
>
>       `ap/middleware/driver/spi/spi_statis.c`
> - SPI Flash 驱动（`CONFIG_SPI_MST_FLASH`，**兼容/调试，默认关闭**）：
>   :   `ap/middleware/driver/spi/spi_flash.c`

<a id="id4"></a>

## 3 SPI 相关宏配置

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG\_SPI | SPI 使能 | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | y |
> | CONFIG\_SOC\_SPI\_UNIT\_NUM | SPI 单元数量（1\~4） | menuconfig / Kconfig | 2 |
> | CONFIG\_SPI\_DMA | SPI DMA 使能 | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | y |
> | CONFIG\_SPI\_TEST | SPI CLI 测试命令（spi\_test.c） | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | y |
> | CONFIG\_SPI\_STATIS | SPI 统计/Debug | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | y |
> | CONFIG\_SPI\_SUPPORT\_TX\_FIFO\_WR\_READY | TX FIFO 写就绪检测 | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | y |
> | CONFIG\_SPI\_BYTE\_INTERVAL | Master 字节间隔 | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | y |
> | CONFIG\_SPI\_PM\_CB\_SUPPORT | SPI 低功耗回调 | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | n |
> | CONFIG\_SPI\_MST\_FLASH | SPI Flash 驱动（兼容/调试） | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | n |
> | CONFIG\_SPI\_MST\_PSRAM | SPI PSRAM 驱动 | Kconfig | n |

<a id="id5"></a>

## 4 SPI 引脚配置

> SPI0\~SPI3 的四个信号（SCK、CSN、MOSI、MISO）均属于 **灵活映射**，用户可在
> `projects/<工程>/config/bk7259_ap/usr_gpio_cfg.h` 的 **GPIO\_DEFAULT\_DEV\_CONFIG** 中
> 选择任意合法 GPIO 进行配置，**无固定管脚组合**。
>
> 配置步骤：
>
> 1. 查阅 `ap/middleware/soc/bk7259_ap/soc/gpio_map.h` 确认目标 pad 支持 SPI 功能
> 2. 在 usr\_gpio\_cfg.h 中将四根信号分别映射为 GPIO\_DEV\_SPIx 的 CSN、SCK、MOSI、MISO 宏（x 为 SPI 单元号 0\~3）
> 3. 确保 CONFIG\_USR\_GPIO\_CFG\_EN 已使能（SDK 默认已使能）
> 4. 调用 bk\_spi\_init 时驱动自动通过 gpio\_dev\_map\_by\_func 完成引脚映射
>
> `projects/app` 参考示例（仅供参考，请按实际硬件修改）：
>
> > | SPI 单元 | CSN | SCK | MOSI | MISO |
> > | --- | --- | --- | --- | --- |
> > | SPI0 | GPIO\_14 | GPIO\_15 | GPIO\_16 | GPIO\_17 |
> > | SPI1 | GPIO\_18 | GPIO\_19 | GPIO\_20 | GPIO\_21 |
>
> 同一组 pad 可通过 `time_sharing_func_dev` 分时复用 SPI2/SPI3 功能，但同一时刻只能启用其中一个 SPI 单元。

<a id="spi-cli"></a>

## 5 SPI CLI 命令

> 需使能 `CONFIG_SPI_TEST=y`。SPI id 范围为 `0 ~ (CONFIG_SOC_SPI_UNIT_NUM - 1)`，默认 0\~1。

**基础命令**

> | Command | Param | Description |
> | --- | --- | --- |
> | `spi_driver {init|deinit}` | init / deinit | 初始化/反初始化 SPI 驱动公共资源 |
> | `spi {id} init {master|slave} {8|16} {cpol} {cpha} {3|4} {baud_rate} {MSB|LSB} {dma_mode}` | id: SPI 单元号；master/slave: 主从模式；8/16: 位宽；3/4: 线模式；cpol/cpha: 0 或 1；dma\_mode: 0\=PIO, 1\=DMA | 初始化 SPI 并设置工作参数 |
> | `spi {id} deinit` | id | 反初始化指定 SPI 单元 |
> | `spi {id} write {len}` | len: 发送字节数 | PIO 写，数据为 0x00\~0xFF 递增模式 |
> | `spi {id} read {len}` | len: 接收字节数 | PIO 读 |
> | `spi {id} write_async {len}` | len: 异步发送字节数 | 异步 PIO 写 |
> | `spi {id} read_async {len}` | len: 异步接收字节数 | 异步 PIO 读 |
> | `spi {id} dma_write {len}` | len | DMA 写（需 CONFIG\_SPI\_DMA） |
> | `spi {id} dma_read {len}` | len | DMA 读 |
> | `spi {id} dma_duplex {len}` | len | DMA 全双工（需 duplex init） |

**运行时配置与中断**

> | Command | Param | Description |
> | --- | --- | --- |
> | `spi_config {id} baud_rate {value}` | 动态修改波特率 |  |
> | `spi_config {id} mode {0~3}` | 动态修改 SPI Mode |  |
> | `spi_config {id} bit_width {8|16}` | 动态修改位宽 |  |
> | `spi_config {id} wire_mode {3|4}` | 动态修改线模式 |  |
> | `spi_config {id} bit_order {LSB|MSB}` | 动态修改 bit order |  |
> | `spi_int {id} reg tx` | 注册 TX finish ISR |  |
> | `spi_int {id} reg rx` | 注册 RX ISR |  |

**标准化测试命令**

> | Command | Param | Description |
> | --- | --- | --- |
> | `spi_lb {id} [quick|full]` | 单板回环测试 | 需短接 MOSI↔MISO，CONFIG\_SPI\_DMA\=y |
> | `spi_peer {master|slave} {id} {baud} {rounds} {data_len} [gap_ms] [dma|fifo]` | dma/fifo: 传输路径；默认 dma | 双板对测；独立测试线程 \+ gap\_ms 时序对齐；两板共地 |
> | `spi_peer stop` | 停止正在运行的 peer 测试线程 |  |
> | `spi_api_test {id}` | API 负向/边界测试 | 输出 SPI\_API: PASS/FAIL 前缀 |
> | `spi_flash {id} readid` | 读取 Flash JEDEC ID | 兼容/调试；需 CONFIG\_SPI\_MST\_FLASH\=y；未开启时 CLI 提示请启用该宏 |
> | `spi_flash {id} {read|write|erase} {addr} {len}` | addr(hex) len(hex) \[read\_times\] | SPI Flash 读写擦（同上）；生产环境请用 QSPI Flash |
>
> 测试套件详细说明见下文第 7 节，设计背景见 [SPI 使用指南](../../developer-guide/peripheral/bk_spi.md) 中「测试套件说明」。
>
> - SPI Mode 与 CPOL/CPHA 对应关系：
>
>   > | Mode | CPOL | CPHA |
>   > | --- | --- | --- |
>   > | 0 | 0 | 0 |
>   > | 1 | 0 | 1 |
>   > | 2 | 1 | 0 |
>   > | 3 | 1 | 1 |
> - 波特率说明：
>
>   > BK7259 AP 通过动态分频设置波特率，非固定档位列表。驱动根据目标值自动选择 XTAL 或 160MHz 时钟源，
>   > 最大 **80MHz**。详见 [SPI 使用指南](../../developer-guide/peripheral/bk_spi.md) 中时钟速率章节。

<a id="spi-demo"></a>

## 6 SPI demo 命令行演示

> 以下示例基于 `projects/app` 默认引脚（SPI0 \= GPIO\_14\~17），实际使用时请按 `usr_gpio_cfg.h` 中配置的管脚接线。
>
> **A) 单板回环测试（推荐入门）**
>
> 前提：已在 `usr_gpio_cfg.h` 配置 SPI0 引脚，并将 MOSI 与 MISO 短接。
>
> ```
> spi_driver init
> spi_lb 0 quick
> ```
>
> 期望输出含 `SPI_LB: PASS` 及 `SPI_LB SUMMARY: x/x PASS`。
>
> **B) 双板 master/slave 对测**
>
> 前提：两块板 SPI 四线对接（SCK↔SCK, MOSI↔MOSI, MISO↔MISO, CSN↔CSN）并共地。
> `spi_peer` 会在独立测试线程内自动 bk\_spi\_init，无需额外 SYNC GPIO，也无需事先手动 spi init。
>
> Slave 板（先启动）:
>
> ```
> spi_peer slave 0 1000000 100 256 dma
> ```
>
> Master 板（后启动，除 role 外参数须一致）:
>
> ```
> spi_peer master 0 1000000 100 256 dma
> ```
>
> 期望输出含 `[SPI-PEER][S/M] DONE ... result=PASS` 及每轮 `[M] round N PASS` / `[S] round N PASS`。
> 停止测试：`spi_peer stop`。
>
> **C) 基础 PIO 读写**
>
> Master:
>
> ```
> spi_driver init
> spi 0 init master 8 1 1 4 1000000 MSB 0
> spi 0 write 1024
> ```
>
> Slave:
>
> ```
> spi_driver init
> spi 0 init slave 8 1 1 4 1000000 MSB 0
> spi 0 read 1024
> ```
>
> **D) SPI Flash 读 ID（兼容/调试，需 CONFIG\_SPI\_MST\_FLASH\=y）**
>
> 生产环境请使用 QSPI Flash（`qspi_flash` CLI，见 [QSPI 示例](bk_qspi.md)）。
> 本节 SPI Flash demo 仅在手动开启 `CONFIG_SPI_MST_FLASH` 后可用；未开启时执行 `spi_flash` 将提示「请启用 CONFIG\_SPI\_MST\_FLASH」。
>
> ```
> spi_driver init
> spi 0 init master 8 0 0 4 1000000 MSB 0
> spi_flash 0 readid
> ```
>
> **E) API 负向测试（单板）**
>
> ```
> spi_driver init
> spi_api_test 0
> ```
>
> 期望输出含 `SPI_API: PASS` 及 `SPI_API SUMMARY: 3/3 PASS`、`SPI_API: ALL PASS`。
>
> **F) 异步 PIO 读写（双板场景下可配合使用）**
>
> ```
> spi_driver init
> spi 0 init master 8 1 1 4 1000000 MSB 0
> spi 0 write_async 256
> spi 0 read_async 256
> ```

<a id="id9"></a>

## 7 SPI 测试套件说明

> 源码位于 `ap/middleware/driver/spi/spi_test.c`，启用 `CONFIG_SPI_TEST=y` 后注册 CLI。
> 三套标准化测试（`spi_lb`、`spi_peer`、`spi_api_test`）输出均带固定前缀，便于 CI / 脚本 grep 判定：
>
> - `spi_lb` / `spi_api_test`：使用 LCG 伪随机 pattern（seed 起始 `0x53504954`），失败时打印 mismatch 偏移及前后 16 字节 hex diff
> - `spi_peer`：每轮使用确定性字节 pattern（m2s: `round+idx`；s2m: `0xC0+round+idx`），按轮逐字节比对
>
> 日志前缀参考：
>
> | 前缀 | 含义 | 通过判定示例 |
> | --- | --- | --- |
> | `SPI_LB:` / `SPI_LB SUMMARY:` / `SPI_LB: ALL PASS` | 单板回环单条 case / 汇总 / 全部通过 | `SPI_LB: PASS (len=...)`；`SPI_LB SUMMARY: N/N PASS`；行末出现 ALL PASS 即通过 |
> | `[SPI-PEER][M]` / `[SPI-PEER][S]` / `result=PASS` | 双板对测 master/slave 启动与结束汇总 | `[M] round N PASS`；`[SPI-PEER][M] DONE ... result=PASS` |
> | `SPI_API:` / `SPI_API SUMMARY:` / `SPI_API: ALL PASS` | API 负向单条 case / 汇总 / 全部通过 | `SPI_API: PASS xxx`；`SPI_API SUMMARY: 3/3 PASS`；行末出现 ALL PASS 即通过 |

<a id="spi-lb"></a>

### 7.1 spi\_lb — 单板回环

> **命令**：`spi_lb {id} [quick|full]`
>
> **硬件前提**：
>
> - ``` CONFIG_SPI_DMA=y``（使用 ``bk_spi_dma_duplex_xfer ``` 全双工 DMA，PIO 不支持本测试）
> - 目标 SPI 单元的 **MOSI 与 MISO 短接**
> - `usr_gpio_cfg.h` 中已配置对应 SPI 引脚
>
> **工作原理**：以 Master \+ 8bit \+ 4线 \+ MSB \+ Mode 可配 初始化 SPI，填充 TX pattern，
> 经 `bk_spi_dma_duplex_init()` \+ `bk_spi_dma_duplex_xfer()` 同时收发，回读 RX 与 pattern 比对。
>
> **模式差异**：
>
> | 模式 | 长度 sweep | 额外 sweep |
> | --- | --- | --- |
> | quick | 跳过 len\>256（4096 除外） | Mode 0\~3；波特率 sweep；20 轮随机 stress |
> | full | 全部长度 | 同上；100 轮随机 stress |
>
> 长度集（字节）：`1, 3, 4, 16, 21, 32, 36, 63, 64, 128, 129, 255, 256, 1024, 4095, 4096`
>
> 波特率集（Hz）：`100000, 1000000, 4000000, 8000000`
>
> 典型日志:
>
> ```
> SPI_LB START: id=0 quick (jumper MOSI<->MISO required)
> SPI_LB: PASS (len=256 baud=1000000 mode=0)
> SPI_LB SUMMARY: 42/42 PASS
> SPI_LB: ALL PASS
> ```

<a id="spi-peer-master-slave"></a>

### 7.2 spi\_peer — 双板 master/slave 对测

> **命令**：`spi_peer {master|slave} {id} {baud} {rounds} {data_len} [gap_ms] [dma|fifo]`
>
> 另支持 `spi_peer stop` 停止正在运行的测试线程。
>
> **参数默认值**：
>
> | 参数 | 默认值 | 说明 |
> | --- | --- | --- |
> | baud | （必填） | 对测波特率（Hz） |
> | rounds | （必填） | 测试轮数 |
> | data\_len | （必填） | 每轮每方向 payload 字节数 |
> | gap\_ms | 5 | 每轮 Phase A/B 之间的延时（ms），用于 master/slave 切换 |
> | dma/fifo | dma | dma \= DMA 路径（默认，需 CONFIG\_SPI\_DMA）；fifo \= CPU/FIFO 路径 |
>
> **硬件前提**：
>
> - 两块板共地，SPI 四线对接（SCK/MOSI/MISO/CSN 同名相连）
> - 两块板除 role 外必须执行完全相同参数的 spi\_peer（一板 master、一板 slave）
> - slave 先启动，master 后启动（数秒内即可）
> - usr\_gpio\_cfg.h 中已配置对应 SPI 引脚
>
> **工作原理**：
>
> - 每侧创建独立测试线程，线程内自动 bk\_spi\_init（Mode 3：CPOL\=1, CPHA\=1；8bit；4线；MSB）
> - 每轮分两个阶段（master 驱动时钟）：
>   :   - Phase A (m2s)：master 写 data\_len 字节，slave 读 data\_len 字节并校验
>       - Phase B (s2m)：slave 写 data\_len 字节 payload，master 读 data\_len\+1 字节并校验
> - 阻塞传输期间暂停 task WDT，避免对端未就绪时触发看门狗复位
> - DMA 模式：master 侧使用 bk\_spi\_dma\_duplex\_xfer \+ dummy 缓冲驱动时钟（避免 RX-only DMA 不产生 SCLK 而卡死）
> - FIFO 模式：使用 bk\_spi\_write\_bytes、bk\_spi\_read\_bytes；可与 SPI0 flash 操作共存
>
> 数据 pattern（确定性，非 LCG）：
>
> - m2s：byte\[i\] \= round \+ i
> - s2m：byte\[i\] \= 0xC0 \+ round \+ i
>
> Slave TX 冗余字节 (0x72)：s2m 方向下，硬件会在 slave 首字节前自动插入 0x72。
> slave 侧只发送 payload（不要在软件里再补 0x72）；master 侧读 data\_len\+1 字节，
> 校验首字节为 0x72 后丢弃，再校验 payload。
>
> **典型日志**:
>
> ```
> [SPI-PEER] slave start mode=dma (run the peer as the opposite role first)
> [SPI-PEER][S] start id=0 baud=1000000 rounds=100 len=256 mode=dma
> [S] round 0 PASS (rx errs=0)
> ...
> [SPI-PEER][S] DONE rounds=100 total_errs=0 result=PASS
>
> [SPI-PEER][M] start id=0 baud=1000000 rounds=100 len=256 gap=5ms mode=dma
> [M] round 0 PASS (errs=0)
> ...
> [SPI-PEER][M] DONE rounds=100 total_errs=0 result=PASS
> ```

<a id="spi-api-test-api"></a>

### 7.3 spi\_api\_test — API 负向/边界测试

> **命令**：``` spi_api_test {id}``（``id ``` 默认 0）
>
> **说明**：单板即可运行，不依赖 SPI 接线。每条 case 独立判定 PASS/FAIL。
>
> **测试项**：
>
> | \# | Case 名称 | 期望行为 |
> | --- | --- | --- |
> | 1 | null-config-rejected | `bk_spi_init(id, NULL)` 返回失败 |
> | 2 | invalid-id-rejected | `bk_spi_init(SPI_ID_MAX, &cfg)` 失败 |
> | 3 | uninit-id-write-rejected | 未 init 的 id 上 `bk_spi_write_bytes` 返回 `BK_ERR_SPI_ID_NOT_INIT` |
>
> **典型日志**:
>
> ```
> SPI_API: PASS null-config-rejected
> SPI_API: PASS invalid-id-rejected
> SPI_API: PASS uninit-id-write-rejected
> SPI_API SUMMARY: 3/3 PASS
> SPI_API: ALL PASS
> ```

<a id="spi-flash"></a>

### 7.4 spi\_flash 补充参数（兼容/调试）

> **说明**：外置 Flash 推荐使用 QSPI（`qspi_flash`）；`spi_flash` 仅在 `CONFIG_SPI_MST_FLASH=y` 时可用，SDK 默认关闭。
> 未开启时执行 `spi_flash` 命令，CLI 输出「请启用 CONFIG\_SPI\_MST\_FLASH」。
>
> **read 可选重复次数**：`spi_flash {id} read {addr_hex} {len_hex} [read_times]`
>
> - `read_times` 默认为 1，用于 stress 重复读同一地址
> - `write` 按 256 字节 page 循环写入递增 pattern；`erase` 按指定 size 擦除
>
> **示例**:
>
> ```
> spi_flash 0 read 0x1000 0x100
> spi_flash 0 read 0x1000 0x100 10
> spi_flash 0 erase 0x1000 0x1000
> spi_flash 0 write 0x1000 0x400
> ```
