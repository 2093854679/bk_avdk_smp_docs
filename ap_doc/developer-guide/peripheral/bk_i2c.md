---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_i2c.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
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

<a id="id12"></a>
![I2C Connection](../../../../_assets/bbf31d90a29ee2370391-i2c_connection.png)


Figure 1\. I2C\_Connection

上图为 I2C 硬件连接，其中：

> - SCL：时钟信号, 提供传输数据的时钟，用来同步数据传输；
> - SDA：用于传输数据。

Beken 芯片通常具有 2 个 I2C 控制器(I2C0和I2C1)；

<a id="i2c-id"></a>

## I2C ID 说明

<a id="id2"></a>

### I2C 实现选择

Beken 提供两种 I2C 实现，通过 Kconfig 选项 `CONFIG_SIM_I2C` 在 **编译期二选一**（互斥，不能同时存在）。两种实现对外暴露完全相同的 `bk_i2c_*` API，应用代码无需改动，只是编译配置不同：

- **硬件 I2C**（`CONFIG_SIM_I2C=n`，默认）：编译 `i2c_driver.c`，使用 SoC 硬件 I2C 外设，支持中断和 DMA，性能高。
- **软件模拟 I2C**（`CONFIG_SIM_I2C=y`）：编译 `sim_i2c_driver.c`，使用 GPIO 软件 bit-bang 模拟 I2C 时序，可将任意 GPIO 用作 SDA/SCL，但性能低于硬件 I2C。

备注

`CONFIG_SIM_I2C` 是编译期开关，二者不能共存：使能后整个 `bk_i2c_*` API 由模拟 I2C 实现，硬件 I2C 驱动不再参与编译。

<a id="id3"></a>

### I2C ID 与引脚映射

无论硬件还是模拟实现，`id` 取值均为 `0` 到 `SOC_I2C_UNIT_NUM - 1`（BK7259 为 `id = 0, 1`）：

- **硬件 I2C**：`id` 对应 I2C0 / I2C1 外设，引脚由 SoC 固定管脚决定。
- **模拟 I2C**：`id` 映射到 Kconfig 配置的一组 GPIO：

  - `id = 0` → `CONFIG_SIM_I2C0_SDA_GPIO` / `CONFIG_SIM_I2C0_SCL_GPIO`
  - `id = 1` → `CONFIG_SIM_I2C1_SDA_GPIO` / `CONFIG_SIM_I2C1_SCL_GPIO`

<a id="id4"></a>

### 模拟 I2C 特性

- **总线互斥锁**：所有传输由一把全局总线互斥锁串行化保证线程安全（bit-bang 共用同一 GPIO 控制器，需要全局串行）。
- **每 id 引用计数**：同一 id 被多个模块使用时，只有最后一个模块 `bk_i2c_deinit` 时才真正释放总线，避免其中一个模块 deinit 影响其他仍在使用该 id 的模块。
- **引脚编译期确定**：SDA/SCL 由上述 Kconfig 决定。

<a id="id5"></a>

### 使用注意事项

1. **初始化顺序**：

   - 必须先调用 `bk_i2c_driver_init()` 初始化驱动层。
   - 然后对每个要使用的 I2C `id` 调用 `bk_i2c_init(id, cfg)`。
2. **模拟 I2C 配置**：

   - 在 Kconfig 中启用 `CONFIG_SIM_I2C`。
   - 配置 `CONFIG_SIM_I2C0_SDA_GPIO` / `CONFIG_SIM_I2C0_SCL_GPIO`（以及需要用到的 I2C1 对应配置）。
   - **必须在工程的** `usr_gpio_cfg.h` **中把所选 SDA/SCL 引脚声明为 GPIO 方向**（见下方 “模拟 I2C 的 GPIO 配置”）。
3. **错误处理**：

   - `BK_ERR_I2C_NOT_INIT`：驱动未初始化。
   - `BK_ERR_I2C_ID_NOT_INIT`：指定 ID 未初始化。

<a id="i2c-gpio"></a>

### 模拟 I2C 的 GPIO 配置

模拟 I2C 通过 GPIO API（`bk_gpio_enable_output` / `bk_gpio_enable_input`）驱动引脚。当工程启用 `CONFIG_USR_GPIO_CFG_EN`（BK7259 默认开启）时，这两个 API 会被工程 `usr_gpio_cfg.h` 中的 `GPIO_DEFAULT_DEV_CONFIG` 表 **门控**：只有当对应引脚的 `second_func_dev` 或 `time_sharing_func_dev` 被声明为 `GPIO_DEV_GPIO_OUTPUT` / `GPIO_DEV_GPIO_INPUT` 时才允许切换方向，否则返回 `BK_ERR_GPIO_CHAN_ID`，`bk_i2c_init` 随之失败并打印 `gpio ... not configured as OUTPUT/INPUT in usr_gpio_cfg.h`。

因此使用模拟 I2C 前，必须在工程的 `usr_gpio_cfg.h`（如 `projects/<工程>/ap/config/bk7259_ap/usr_gpio_cfg.h`）中把所选引脚声明为 GPIO 方向：

- **SCL**：仅用作输出，声明 `second_func_dev = GPIO_DEV_GPIO_OUTPUT`。
- **SDA**：需要输出与输入（读 ACK），两栏各占一个，例如 `second_func_dev = GPIO_DEV_GPIO_OUTPUT`、`time_sharing_func_dev = GPIO_DEV_GPIO_INPUT`。

备注

工程默认可能把这些引脚配成了硬件外设功能（例如 app 工程默认将 GPIO0/GPIO1 配成 `GPIO_DEV_I2C1_SCL` / `GPIO_DEV_I2C1_SDA`）。改用模拟 I2C 时必须改成上述 GPIO 方向，否则引脚被外设占用，bit-bang 无法工作。建议开启内部上拉（`GPIO_PULL_UP_EN`），或在硬件上外接上拉电阻。

以 `id = 0`（默认 SCL\=GPIO0、SDA\=GPIO1）为例，在 `GPIO_DEFAULT_DEV_CONFIG` 中配置：

```
/* gpio_id  second_func_en  second_func_dev  time_sharing_func_dev  pull_mode  int_en  int_type  low_power_io_ctrl  driver_capacity  gpio_skip */
// SCL (GPIO0): output only
{GPIO_0, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_GPIO_OUTPUT, GPIO_DEV_INVALID,     GPIO_PULL_UP_EN, GPIO_INT_DISABLE, GPIO_INT_TYPE_LOW_LEVEL, GPIO_LOW_POWER_DISCARD_IO_STATUS, GPIO_DRIVER_CAPACITY_3, GPIO_INIT_ENABLE},
// SDA (GPIO1): output + input
{GPIO_1, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_GPIO_OUTPUT, GPIO_DEV_GPIO_INPUT,  GPIO_PULL_UP_EN, GPIO_INT_DISABLE, GPIO_INT_TYPE_LOW_LEVEL, GPIO_LOW_POWER_DISCARD_IO_STATUS, GPIO_DRIVER_CAPACITY_3, GPIO_INIT_ENABLE},
```

<a id="id6"></a>

### 示例代码

以下代码在硬件 I2C 与模拟 I2C 下完全一致，仅由 `CONFIG_SIM_I2C` 决定底层实现：

```
// 初始化驱动（只需调用一次）
bk_i2c_driver_init();

// 初始化 I2C id = 0
i2c_config_t i2c_cfg = {
    .baud_rate = 100000,
    .addr_mode = I2C_ADDR_MODE_7BIT,
};
bk_i2c_init(I2C_ID_0, &i2c_cfg);

// 读写从设备（如 EEPROM）内部地址
uint8_t buffer[16];
i2c_mem_param_t param = {
    .dev_addr = 0x50,
    .mem_addr = 0x0000,
    .mem_addr_size = I2C_MEM_ADDR_SIZE_8BIT,
    .data = buffer,
    .data_size = 16,
    .timeout_ms = 1000,
};
bk_i2c_memory_read(I2C_ID_0, &param);
```

<a id="id7"></a>

## I2C 通信流程

> - 在主模式下，I2C 接口会启动数据传输并生成时钟信号。串行数据传输始终是在出现 START 位 (STA) 时开始，在出现 STOP 位 (STO) 时结束。起始位和停止位均在主模式下由软件生成。START 位通过在 SCL 为高电平时将 SDA 线拉低而生成，STOP 位通过在 SCL 为高电平时将 SDA 线拉高而生成。
> - 在从模式下，该接口能够识别其自身地址（7 或 10 位）以及广播呼叫地址。数据和地址均以 8 位字节传输，最高有效位 (MSB) 在先。起始位后紧随地址字节（7 位地址占据一个字节；10 位地址占据两个字节）。地址始终在主模式下传送。
> - 在 (N)ACK 后通过在总线上发送 STOP 位来结束传输。在 STOP 位之后，任何希望在总线上启动传输的主器件都可以尝试获得对总线的控制。如果当前主器件希望在当前之后立即进行另一次传输，它可以通过发送重复的 START 位 (Sr) 来直接开始新的传输，而不是先发送 STOP 后再发送 START。

<a id="id13"></a>
![i2c_Communication](../../../../_assets/a131d210c922ae54f98d-i2c_Communication.png)


Figure 2\. I2C通信图

<a id="id8"></a>

## I2C 时序

- 该接口支持7 位和10 位寻址模式，不同寻址模式下的接口传输时序如下图所示。7 位寻址模式下，主器件在发送 STA 之后只需发送 1 个地址字节，其内容为 SLV\_ADDR\[6:0\]\+W；10 位寻址模式下，主器件在发送 STA 后需要发送 2 个地址字节，第 1 个地址字节内容为 11110\+SLV\_ADDR\[9:8\]\+W，第 2 个地址字节的内容为 SLV\_ADDR\[7:0\]。
- 从器件检测到 STA 后开始接收地址字节。7 位寻址模式下，接收到的第一个地址字节与软件配置的从地址匹配时将上报中断；10 位寻址模式下，接收到的前 2 个地址字节于软件配置的从地址匹配时才上报中断，且地址字节不会写入内部接收 FIFO 中。

<a id="id14"></a>
![i2c_Sequence](../../../../_assets/86e036f96806c7942e7d-i2c_Sequence.png)


Figure 3\. I2C时序图

<a id="id9"></a>

## I2C 使用方法

Beken I2C 既可工作在主机模式下，也可工作在从机模式下。无论主机还是从机，读写之前需要先调用 bk\_i2c\_init() 配置 I2C。
bk\_i2c\_init() 主要配置 I2C SCL 的时钟频率，如果工作在从机模式下，还需要配置 Beken I2C 的器件地址。

<a id="id10"></a>

### I2C 主机模式下通信

调用 bk\_i2c\_master\_write() 写入数据到从设备，bk\_i2c\_master\_read() 读取数据。
针对 eeprom 这类内存设备，Beken 提供 bk\_i2c\_memory\_write()/bk\_i2c\_memory\_read() 接口，可以指定到从设备内部的地址去执行读写操作。以下是

<a id="id15"></a>
![I2C memory write](../../../../_assets/e65d97b1a2d06d9cf5fc-i2c_memory_write.png)


I2C memory write

<a id="id16"></a>
![I2C memory read](../../../../_assets/eadef9869c5e0f1ec083-i2c_memory_read.png)


I2C memory read

<a id="id11"></a>

### I2C 从机模式下通信

针对从机模式下，Beken 提供 bk\_i2c\_slave\_write()/bk\_i2c\_slave\_read()，用于发送/接收数据。

<a id="i2c-api"></a>

### I2C api介绍

- I2C相关的api介绍参考: [I2C的api介绍](../../api-reference/peripheral/bk_i2c.md)
