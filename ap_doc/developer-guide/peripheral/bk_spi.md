---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_spi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="spi"></a>

# SPI 使用指南

<a id="id1"></a>

## 概述

SPI (Serial Peripheral Interface, 串行外设接口) 是一种同步串行通信接口，被广泛应用在 ADC、LCD 等与 MCU 的通信过程中。
外置 Flash 推荐使用 QSPI（见 [QSPI 使用指南](bk_qspi.md)）；SPI Flash 驱动仅用于兼容/调试（`CONFIG_SPI_MST_FLASH`，默认关闭）。
BK7259 AP 侧 SPI 驱动支持全双工通信，可配置为主模式或从模式；主模式下由 SPI 提供 SCK 时钟。

- SPI 相关 demo 和配置介绍: [SPI 相关 demo 和配置介绍](../../examples/peripheral/bk_spi.md)
- GPIO 引脚配置方法: [GPIO 使用指南](bk_gpio.md)

<a id="id2"></a>

## 1 SPI 特性

BK7259 AP 支持 1\~4 路 SPI 控制器（SPI0\~SPI3），具体数量由 Kconfig `CONFIG_SOC_SPI_UNIT_NUM` 决定，SDK 默认值为 2（SPI0、SPI1）。

SPI 接口具有如下特性：

> - 基于三线或四线的全双工同步传输
> - 支持主模式或从模式
> - 数据位宽 8 位或 16 位
> - 可编程时钟极性、相位（Mode 0\~3）
> - 可编程 MSB/LSB 先发
> - 64 深度 RX/TX FIFO，支持 DMA
> - CPU 单次最大传输 4096 Byte；DMA 单次最大 65536 Byte
> - SPI0\~SPI3 的 SCK/CSN/MOSI/MISO 均为灵活映射，可在工程 usr\_gpio\_cfg.h 中配置到任意合法 GPIO（见下文「GPIO 引脚配置」）

<a id="id3"></a>

## 2 SPI 功能说明

- SPI 框图

<a id="id12"></a>
![spi design](../../../../_assets/cb7976cb00cdf89e16a8-spi_design.png)


Figure 1\. SPI 框图

- SPI 信号

下表列出了四个与外部通信的 SPI 信号：

> | 信号名称 | 信号类型 | 描述 |
> | --- | --- | --- |
> | SCK | 数字输入/输出 | 串行时钟。主模式下输出，从模式下输入。 |
> | MOSI | 数字输入/输出 | 主输出/从输入。主模式发送、从模式接收。 |
> | MISO | 数字输入/输出 | 主输入/从输出。从模式发送、主模式接收。 |
> | CSN | 数字输入/输出 | 片选，低电平有效。四线模式下由主器件驱动。 |

- SPI 通信

  > SPI 总线支持单主单从全双工通信（3 线或 4 线）。通信由主机发起，SCK 同步数据移位与采样。
  > 主从双方通过 MOSI/MISO 同时收发数据，传输完成后 CSN 释放。

<a id="id13"></a>
![SPI Connection](../../../../_assets/45d0629b728ed91390c7-spi_connection.png)


Figure 2\. SPI 全双工单主/单从应用示例

- 时钟速率

  > 应用层通过 bk\_spi\_set\_baud\_rate 或 spi\_config\_t.baud\_rate 设置目标波特率，驱动自动选择时钟源并计算分频：
  >
  > - 目标波特率 ≤ XTAL 频率：选用 XTAL 作为 SPI 时钟源
  > - 目标波特率 \> XTAL 频率：选用 160MHz 作为 SPI 时钟源
  >
  > 实际 SCK 频率公式：
  >
  > > f\_SCK \= src\_clk / (2 × (clk\_div \+ 1))
  >
  > 其中 src\_clk 为所选时钟源频率，clk\_div 为 8 位分频系数（0\~255）。BK7259 AP 最大支持 80MHz（`CONFIG_SPI_MAX_BAUD_RATE`）。
- 通信格式

  > 通信格式由 CPOL、CPHA 和数据帧格式共同决定，主从必须使用相同配置。
  >
  > 1）时钟相位和时钟极性
  >
  > | SPI 模式 | CPOL | CPHA | 空闲状态下 SCK 引脚 | 用于采样和/或移位数据的时钟相位 |
  > | --- | --- | --- | --- | --- |
  > | 0 | 0 | 0 | 低电平 | 在上升沿采样数据，在下降沿移出数据 |
  > | 1 | 0 | 1 | 低电平 | 在下降沿采样数据，在上升沿移出数据 |
  > | 2 | 1 | 0 | 高电平 | 在下降沿采样数据，在上升沿移出数据 |
  > | 3 | 1 | 1 | 高电平 | 在上升沿采样数据，在下降沿移出数据 |
  >
  > 应用层可通过 `bk_spi_set_mode()` 设置 Mode 0\~3，或在 `spi_config_t` 中分别设置 `polarity` / `phase`。
  >
  > 2）数据帧格式
  >
  > 位宽 8/16 位通过 `bk_spi_set_bit_width()` 设置；MSB/LSB 通过 `bk_spi_set_bit_order()` 设置。
- GPIO 引脚配置

  > SPI0\~SPI3 的 SCK、CSN、MOSI、MISO 均支持灵活映射，不属于 fixed GPIO。用户可在工程
  > projects/\<工程\>/config/bk7259\_ap/usr\_gpio\_cfg.h 的 GPIO\_DEFAULT\_DEV\_CONFIG 表中，
  > 将任意合法 GPIO 配置为对应 SPI 功能（GPIO\_DEV\_SPIx 的 CSN、SCK、MOSI、MISO）。
  >
  > 配置要点：
  >
  > - SPI 属于 GPIO\_DEV\_TO\_IOMX\_CODE\_MAP 灵活映射类，可选 pad 以 gpio\_map.h 中 IO Matrix 定义为准
  > - bk\_spi\_init 内部通过 gpio\_dev\_map\_by\_func 查找 GPIO\_DEFAULT\_DEV\_CONFIG，将已配置的功能映射到对应 pad
  > - 若某 SPI 功能未写入 GPIO\_DEFAULT\_DEV\_CONFIG，初始化时会报错 func xxx not in GPIO\_DEFAULT\_DEV\_CONFIG
  > - 同一组 pad 可通过 time\_sharing\_func\_dev 字段分时复用不同 SPI 单元（例如 SPI0 与 SPI2 共用一组 pin，但同一时刻只能使用其中一个单元）
  > - 详细配置步骤见 [GPIO 使用指南](bk_gpio.md) 中「配置 usr\_gpio\_cfg.h」章节
  >
  > projects/app 工程参考配置（仅作示例，非固定管脚）:
  >
  > ```
  > /* SPI0: GPIO_14~17 */
  > {GPIO_14, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_SPI0_CSN,  GPIO_DEV_SPI2_CSN,  ...},
  > {GPIO_15, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_SPI0_SCK,  GPIO_DEV_SPI2_SCK,  ...},
  > {GPIO_16, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_SPI0_MOSI, GPIO_DEV_SPI2_MOSI, ...},
  > {GPIO_17, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_SPI0_MISO, GPIO_DEV_SPI2_MISO, ...},
  > /* SPI1: GPIO_18~21 */
  > {GPIO_18, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_SPI1_CSN,  GPIO_DEV_SPI3_CSN,  ...},
  > {GPIO_19, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_SPI1_SCK,  GPIO_DEV_SPI3_SCK,  ...},
  > {GPIO_20, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_SPI1_MOSI, GPIO_DEV_SPI3_MOSI, ...},
  > {GPIO_21, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_SPI1_MISO, GPIO_DEV_SPI3_MISO, ...},
  > ```
- 驱动初始化流程

  > 应用层推荐按以下顺序使用 SPI API：
  >
  > 1. bk\_spi\_driver\_init — 初始化驱动公共资源
  > 2. 在 usr\_gpio\_cfg.h 中配置 SPI 引脚（或在运行时通过 GPIO API 映射）
  > 3. 填写 spi\_config\_t（role、bit\_width、mode、wire\_mode、baud\_rate、bit\_order 等）
  > 4. bk\_spi\_init — 上电、映射 GPIO、配置并启动 SPI
  > 5. 调用 bk\_spi\_write\_bytes、bk\_spi\_read\_bytes，或 DMA 接口 bk\_spi\_dma\_write\_bytes、bk\_spi\_dma\_read\_bytes、bk\_spi\_dma\_duplex\_xfer 传输数据
  > 6. bk\_spi\_deinit / bk\_spi\_driver\_deinit — 释放资源
- RX FIFO 和 TX FIFO

  > TX/RX FIFO 均为 64 × 16 位。FIFO 阈值可通过寄存器配置产生中断；应用层也可注册
  > `bk_spi_register_rx_isr()` / `bk_spi_register_tx_finish_isr()` 等回调处理异步传输。

<a id="id5"></a>

## 3 SPI 时序示例

<a id="id14"></a>
![SPI Timing](../../../../_assets/71765207046bf06b4e56-spi_timing.png)


SPI Timing

上图为 master 传输 0x56 (0b01010110) 给 slave 的时序（CPOL\=1, CPHA\=1, MSB first）：

> - CS 拉低，选中 slave
> - 每个 SCK 周期 MOSI 输出对应 bit，高位先发
> - slave 在约定边沿采样 MOSI

<a id="id6"></a>

## 5 测试套件说明

> SDK 在 `ap/middleware/driver/spi/spi_test.c` 中提供三套标准化 CLI 测试，启用 `CONFIG_SPI_TEST=y` 后可用。
> 命令用法与 demo 示例见 [SPI 相关 demo 和配置介绍](../../examples/peripheral/bk_spi.md) 第 7 节。

<a id="id8"></a>

### 设计目标

> - 可自动化：日志带固定前缀（SPI\_LB、SPI\_PEER、SPI\_API），CI 可直接 grep ALL PASS 或 SUMMARY: N/N PASS 判定结果
> - 可复现：`spi_lb` / `spi_api_test` 使用 LCG 伪随机 pattern（seed 0x53504954）；`spi_peer` 使用确定性轮次 pattern（m2s: round\+idx；s2m: 0xC0\+round\+idx）
> - 可定位：比对失败时打印 offset 及前后 16 字节 expected vs received hex diff

<a id="id9"></a>

### 测试命令一览

| 命令 | 场景 | 核心 API / 路径 |
| --- | --- | --- |
| spi\_lb | 单板回环 | bk\_spi\_dma\_duplex\_xfer（需 DMA） |
| `spi_peer` | 双板对测 | 独立线程；FIFO: write/read\_bytes；DMA: dma\_write/read \+ master duplex 驱动时钟 |
| `spi_api_test` | API 负向 | init/write 参数合法性 |

<a id="spi-lb"></a>

### spi\_lb（单板回环）

> 硬件：MOSI ↔ MISO 短接；CONFIG\_SPI\_DMA\=y。
>
> 每次 case 以 Master 角色 init SPI，通过 DMA duplex 同时收发并校验 RX。
> quick 模式跳过大部分 \>256 字节的长度（保留 4096 边界 case），stress 轮数为 20；
> full 模式跑完整 16 档长度 \+ 100 轮随机长度 stress。
>
> 除长度 sweep 外，还覆盖 Mode 0\~3 与 100k/1M/4M/8M 四档波特率（固定 len\=256）。

<a id="spi-peer"></a>

### spi\_peer（双板对测）

> 硬件：两板 SPI 四线互连 \+ 共地。不再需要 SYNC GPIO。
>
> 命令：`spi_peer {master|slave} {id} {baud} {rounds} {data_len} [gap_ms] [dma|fifo]`；
> 另支持 `spi_peer stop`。
>
> Master 与 slave 须执行参数完全一致的 spi\_peer（仅 role 不同）。slave 先启动，master 后启动。
> 每侧在独立测试线程内自动 bk\_spi\_init，按 rounds 轮次循环，每轮 Phase A (m2s) \+ Phase B (s2m)。
>
> 默认 dma 模式（CONFIG\_SPI\_DMA 开启时）；传 fifo 走 CPU/FIFO 路径（可与 SPI0 flash 操作共存）。
> DMA 模式下 master 接收使用 bk\_spi\_dma\_duplex\_xfer \+ dummy 驱动时钟，避免 RX-only DMA 卡死。
>
> s2m 方向：slave 只发 payload，HW 自动在首字节前插入 0x72；master 读 data\_len\+1 并剥离后校验。
> 阻塞传输期间暂停 task WDT。

<a id="spi-api-test-api"></a>

### spi\_api\_test（API 负向）

> 单板运行，验证三类错误路径：NULL config、非法 id、未 init id 上 write。
> 全部 3 项 PASS 时输出 SPI\_API: ALL PASS。

<a id="flash"></a>

### 外置 Flash 访问

> - 推荐：使用 QSPI 访问外置 Flash（更高吞吐、四线宽总线），参见 [QSPI 使用指南](bk_qspi.md) 与 qspi\_flash CLI。
> - 兼容/调试：ap/middleware/driver/spi/spi\_flash.c 提供基于 SPI 主模式的 Flash 读写擦，由 CONFIG\_SPI\_MST\_FLASH 控制，SDK 默认关闭。
>   仅在需要验证 SPI 总线或兼容旧方案时手动开启；CLI spi\_flash 在未开启时会提示「请启用 CONFIG\_SPI\_MST\_FLASH」。

<a id="id11"></a>

## 6 已知限制

- Slave 发送首字节：当前部分芯片在 SPI 从模式发送时，硬件会在有效数据前自动插入 1 字节冗余字节（0x72）。
  双板对测时 slave 只发送 payload（不要在软件里再补 0x72），master 侧读 data\_len\+1 并剥离首字节后校验。
  详见 spi\_test.c 中 SPI\_PEER\_REDUNDANT\_BYTE 说明。
- TrustZone：CONFIG\_SPE 使能时，SPI2/SPI3 需满足安全属性要求。
