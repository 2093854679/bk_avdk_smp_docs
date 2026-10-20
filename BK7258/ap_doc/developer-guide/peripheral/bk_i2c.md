---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_i2c.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="i2c"></a>

# I2C 使用指南

<a id="id1"></a>

## 概述

I2C 是一种串行同步半双工通信协议，总线上可以同时挂载多个主机和从机。I2C 总线由串行数据线 (SDA) 和串行时钟线 (SCL) 线构成。这些线都需要上拉电阻。

I2C 具有简单且制造成本低廉等优点，主要用于低速外围设备的短距离通信（一英尺以内）。

- I2C相关测试和配置介绍: [I2C\_test\_config\_driver](../../examples/peripheral/bk_i2c.md)

<a id="id10"></a>
![I2C Connection](../../../../../_assets/5b9d2f846ce3c488c5d4-i2c_connection.png)


Figure 1\. I2C\_Connection

上图为 I2C 硬件连接，其中：

> - SCL：时钟信号, 提供传输数据的时钟，用来同步数据传输；
> - SDA：用于传输数据。

Beken 芯片通常具有 2 个 I2C 控制器(I2C0和I2C1)；

<a id="i2c-id"></a>

## I2C ID 说明

<a id="id2"></a>

### I2C ID 分配规则

Beken I2C 驱动支持硬件 I2C 和软件模拟 I2C（Simulated I2C）的共存使用。I2C ID 用于区分不同的 I2C 实例：

- **硬件 I2C**：使用 SoC 硬件 I2C 外设
  \- ID 范围：`0` 到 `SOC_I2C_UNIT_NUM - 1`
  \- 对于 BK7258：`id = 0, 1` 对应 I2C0 和 I2C1
  \- 特点：使用硬件寄存器，支持中断，性能高
- **模拟 I2C**：使用 GPIO 软件模拟 I2C 时序
  \- ID 范围：`SIM_I2C_START_ID` 及以上（通常 `SIM_I2C_START_ID = SOC_I2C_UNIT_NUM`）
  \- 对于 BK7258：`id >= 2` 为模拟 I2C
  \- 特点：通过 GPIO 控制实现，灵活配置任意 GPIO 作为 SDA/SCL

<a id="id"></a>

### ID 路由机制

统一 API 层（`i2c_unified.c`）会根据 I2C ID 自动路由到对应的实现：

- `id < SOC_I2C_UNIT_NUM` → 自动使用硬件 I2C 驱动
- `id >= SIM_I2C_START_ID` → 自动使用模拟 I2C 驱动

应用程序无需关心底层实现，统一使用 `bk_i2c_\*` API 即可。

备注

当 `CONFIG_SIM_I2C` 未启用时，只支持硬件 I2C（id \= 0, 1）。
启用 `CONFIG_SIM_I2C` 后，可以同时使用硬件 I2C 和模拟 I2C。

<a id="id3"></a>

### 使用注意事项

1. **ID 选择**：
   \- 使用硬件 I2C 时，选择 `id = 0` 或 `id = 1`
   \- 使用模拟 I2C 时，选择 `id >= 2` （如 `id = 2, 3, ...`）
   \- 不要在运行时混合使用超出范围的 ID，否则会返回 `BK_ERR_I2C_INVALID_ID` 错误
2. **初始化顺序**：
   \- 必须先调用 `bk_i2c_driver_init()` 初始化驱动层
   \- 然后对每个要使用的 I2C ID 调用 `bk_i2c_init(id, cfg)`
3. **模拟 I2C 配置**：
   \- 使用模拟 I2C 前，需在 Kconfig 中启用 `CONFIG_SIM_I2C`
   \- 配置 `CONFIG_SIM_I2C0_SDA_GPIO` 和 `CONFIG_SIM_I2C0_SCL_GPIO` （或 I2C1 对应配置）
   \- 模拟 I2C 通过互斥锁保护，确保线程安全，但性能低于硬件 I2C
4. **错误处理**：
   \- `BK_ERR_I2C_INVALID_ID`：ID 超出有效范围
   \- `BK_ERR_I2C_NOT_INIT`：驱动未初始化
   \- `BK_ERR_I2C_ID_NOT_INIT`：指定 ID 未初始化

<a id="id4"></a>

### 示例代码

```
// 初始化驱动（只需调用一次）
bk_i2c_driver_init();

// 使用硬件 I2C (id = 0)
i2c_config_t hw_i2c_cfg = {
    .baud_rate = 100000,
    .addr_mode = I2C_ADDR_MODE_7BIT,
    .role = I2C_ROLE_MASTER,
};
bk_i2c_init(I2C_ID_0, &hw_i2c_cfg);

// 使用模拟 I2C (id = 2, 需要 CONFIG_SIM_I2C 启用)
#if CONFIG_SIM_I2C
i2c_config_t sim_i2c_cfg = {
    .baud_rate = 100000,
    .addr_mode = I2C_ADDR_MODE_7BIT,
    .role = I2C_ROLE_MASTER,
};
bk_i2c_init(I2C_ID_2, &sim_i2c_cfg);  // 自动路由到模拟 I2C
#endif

// 使用统一的 API，无需区分硬件/模拟
i2c_mem_param_t param = {
    .dev_addr = 0x50,
    .mem_addr = 0x0000,
    .mem_addr_size = I2C_MEM_ADDR_SIZE_8BIT,
    .data = buffer,
    .data_size = 16,
    .timeout_ms = 1000,
};
bk_i2c_memory_read(I2C_ID_0, &param);  // 硬件 I2C
bk_i2c_memory_read(I2C_ID_2, &param);  // 模拟 I2C（如果启用）
```

<a id="id5"></a>

## I2C 通信流程

> - 在主模式下，I2C 接口会启动数据传输并生成时钟信号。串行数据传输始终是在出现 START 位 (STA) 时开始，在出现 STOP 位 (STO) 时结束。起始位和停止位均在主模式下由软件生成。START 位通过在 SCL 为高电平时将 SDA 线拉低而生成，STOP 位通过在 SCL 为高电平时将 SDA 线拉高而生成。
> - 在从模式下，该接口能够识别其自身地址（7 或 10 位）以及广播呼叫地址。数据和地址均以 8 位字节传输，最高有效位 (MSB) 在先。起始位后紧随地址字节（7 位地址占据一个字节；10 位地址占据两个字节）。地址始终在主模式下传送。
> - 在 (N)ACK 后通过在总线上发送 STOP 位来结束传输。在 STOP 位之后，任何希望在总线上启动传输的主器件都可以尝试获得对总线的控制。如果当前主器件希望在当前之后立即进行另一次传输，它可以通过发送重复的 START 位 (Sr) 来直接开始新的传输，而不是先发送 STOP 后再发送 START。

<a id="id11"></a>
![i2c_Communication](../../../../../_assets/b9eee72f94121bf6787e-i2c_Communication.png)


Figure 2\. I2C通信图

<a id="id6"></a>

## I2C 时序

- 该接口支持7 位和10 位寻址模式，不同寻址模式下的接口传输时序如下图所示。7 位寻址模式下，主器件在发送 STA 之后只需发送 1 个地址字节，其内容为 SLV\_ADDR\[6:0\]\+W；10 位寻址模式下，主器件在发送 STA 后需要发送 2 个地址字节，第 1 个地址字节内容为 11110\+SLV\_ADDR\[9:8\]\+W，第 2 个地址字节的内容为 SLV\_ADDR\[7:0\]。
- 从器件检测到 STA 后开始接收地址字节。7 位寻址模式下，接收到的第一个地址字节与软件配置的从地址匹配时将上报中断；10 位寻址模式下，接收到的前 2 个地址字节于软件配置的从地址匹配时才上报中断，且地址字节不会写入内部接收 FIFO 中。

<a id="id12"></a>
![i2c_Sequence](../../../../../_assets/e10a25416eafab7baa67-i2c_Sequence.png)


Figure 3\. I2C时序图

<a id="id7"></a>

## I2C 使用方法

Beken I2C 既可工作在主机模式下，也可工作在从机模式下。无论主机还是从机，读写之前需要先调用 bk\_i2c\_init() 配置 I2C。
bk\_i2c\_init() 主要配置 I2C SCL 的时钟频率，如果工作在从机模式下，还需要配置 Beken I2C 的器件地址。

<a id="id8"></a>

### I2C 主机模式下通信

调用 bk\_i2c\_master\_write() 写入数据到从设备，bk\_i2c\_master\_read() 读取数据。
针对 eeprom 这类内存设备，Beken 提供 bk\_i2c\_memory\_write()/bk\_i2c\_memory\_read() 接口，可以指定到从设备内部的地址去执行读写操作。以下是

<a id="id13"></a>
![I2C memory write](../../../../../_assets/aab0aa5f0cb9e68f967a-i2c_memory_write.png)


I2C memory write

<a id="id14"></a>
![I2C memory read](../../../../../_assets/eb239e4feb193ac9a73c-i2c_memory_read.png)


I2C memory read

<a id="id9"></a>

### I2C 从机模式下通信

针对从机模式下，Beken 提供 bk\_i2c\_slave\_write()/bk\_i2c\_slave\_read()，用于发送/接收数据。

<a id="i2c-api"></a>

### I2C api介绍

- I2C相关的api介绍参考: [I2C的api介绍](../../api-reference/peripheral/bk_i2c.md)
