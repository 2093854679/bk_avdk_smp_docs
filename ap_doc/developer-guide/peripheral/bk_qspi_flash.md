---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_qspi_flash.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="qspi-flash"></a>

# [QSPI Flash 使用指南](#id14)

<a id="id1"></a>

目录

- [QSPI Flash 使用指南](#qspi-flash)

  - [概述](#id2)
  - [器件类型](#id3)
  - [Kconfig 与文件系统](#kconfig)
  - [硬件连接](#id4)
  - [驱动初始化](#id5)
  - [读写擦除 API](#api)
  - [状态寄存器与保护](#id9)
  - [SPI-NAND 补充说明](#spi-nand)
  - [典型使用流程（NOR）](#id12)
  - [常见问题](#id13)

<a id="id2"></a>

## [概述](#id15)

QSPI Flash 驱动基于 AP 侧 QSPI 控制器，通过间接模式对外挂 NOR Flash 或 QSPI SPI-NAND（下称 SPI-NAND）进行读写擦除。

与片上 Flash（[FLASH 使用指南](bk_flash.md)）不同，QSPI Flash 由 AP 直接操作，不经过 CP Mailbox。

- QSPI 控制器原理：[QSPI 使用指南](bk_qspi.md)
- 文件系统（VFS/littleFS/FATFS）：[QSPI 文件系统使用指南](bk_qspi_filesystem.md)
- CLI 演示：[QSPI Flash 示例](../../examples/peripheral/bk_qspi_flash.md)
- API 列表：[QSPI API](../../api-reference/peripheral/bk_qspi.md)（QSPI Flash API 章节）

<a id="id3"></a>

## [器件类型](#id16)

NOR Flash 与 SPI-NAND 通过 Kconfig **choice** 互斥选择，共用 `bk_qspi_flash_*` 前缀 API，编译期只链接一种驱动：

| 配置 | 说明 |
| --- | --- |
| `CONFIG_QSPI_NOR_FLASH` | 标准 NOR Flash，支持扇区/块擦除与页编程 |
| `CONFIG_QSPI_NAND_FLASH` | SPI-NAND，页大小 2 KB，块大小 128 KB |

若两者同时被强制使能，**NAND 优先**。

<a id="kconfig"></a>

## [Kconfig 与文件系统](#id17)

基础配置（`menuconfig` → **QSPI**）：

- `CONFIG_QSPI`：必须先开启
- `CONFIG_QSPI_NOR_FLASH` 或 `CONFIG_QSPI_NAND_FLASH`：选择器件类型
- `CONFIG_QSPI_LINE_MODE`：Flash 线模式，NOR 建议 4（四线），最小为 2（双线）
- `CONFIG_QSPI_NAND_FLASH_SIZE`：SPI-NAND 总容量

文件系统（可选）：

QSPI NOR/NAND Flash 可通过 VFS 统一接口配合 littleFS / FATFS 使用。文件系统的分层关系、Kconfig、
API demo 与 CLI 命令请参考 [QSPI 文件系统（VFS/littleFS/FATFS）使用指南](bk_qspi_filesystem.md)。

备注

建议客户统一使用 VFS(POSIX) 接口访问文件，以便在不同文件系统与存储介质间兼容切换。
USB MSC 场景可通过 `CONFIG_USBD_MSC_STORAGE_QSPI_NAND` 将 SPI-NAND 暴露为 U 盘。

<a id="id4"></a>

## [硬件连接](#id18)

BK7259 AP 侧 QSPI 管脚（组 0）：

| QSPI0 功能 | GPIO |
| --- | --- |
| QSPI0\_SCK | GPIO22 |
| QSPI0\_CS | GPIO23 |
| QSPI0\_DAT\[0..3\] | GPIO24\~27 |

| QSPI1 功能 | GPIO |
| --- | --- |
| QSPI1\_SCK | GPIO2 |
| QSPI1\_CS | GPIO3 |
| QSPI1\_DAT\[0..3\] | GPIO4\~7 |

外接 Flash 通常使用 3.3 V 供电，请确认硬件供电与 IO 电平匹配。

<a id="id5"></a>

## [驱动初始化](#id19)

推荐使用封装好的初始化接口，内部会自动配置 80 MHz 以内的 SCK、解除保护并尝试使能四线模式：

```
bk_qspi_driver_init();
bk_qspi_flash_init(QSPI_ID_1);   // 初始化 QSPI1 及外挂 Flash
```

`bk_qspi_flash_init()` 等价于：

1. `bk_qspi_init_by_freq(id, 80000000)`
2. `bk_qspi_flash_set_protect_none(id)`
3. `bk_qspi_flash_quad_enable(id)`（按器件能力）

<a id="api"></a>

## [读写擦除 API](#id20)

<a id="id6"></a>

### 高层封装（推荐）

`bk_qspi_flash_read()` / `bk_qspi_flash_write()` / `bk_qspi_flash_erase()` 会根据 `CONFIG_QSPI_LINE_MODE` 自动选择双线或四线底层实现，并处理页对齐与跨页写入。

<a id="id7"></a>

### 底层接口

| API | 说明 |
| --- | --- |
| `bk_qspi_flash_read_id()` | 读取 3 字节 JEDEC ID |
| `bk_qspi_flash_erase_sector()` | 擦除 4 KB 扇区 |
| `bk_qspi_flash_erase_32k()` | 擦除 32 KB 块 |
| `bk_qspi_flash_erase_64k()` | 擦除 64 KB 块 |
| `bk_qspi_flash_quad_read()` | 四线快读（0xEB） |
| `bk_qspi_flash_quad_page_program()` | 四线页写（0x32） |
| `bk_qspi_flash_single_read()` | 单线读 |
| `bk_qspi_flash_single_page_program()` | 单线页写 |

NOR Flash 参数（默认描述符）：

- 扇区大小：4 KB
- 页大小：256 字节
- 默认容量：16 MB；识别到的器件按描述符自适应，支持 4 字节寻址 / \>16 MB

<a id="nor"></a>

### NOR 多型号支持与新增器件

与 SPI-NAND 一致，NOR 也支持多型号自动识别：`bk_qspi_flash_init()` 读取 JEDEC ID（9Fh），
在已注册的器件描述符中按 ID 匹配，opcode、QE 位、保护位布局、dummy、容量、地址字节数（3/4）
均从命中的描述符获取；未命中时使用内置 GD 默认描述符（可用 `CONFIG_QSPI_NOR_ALLOW_UNKNOWN` 关闭）。
可用 `bk_qspi_flash_nor_total_size(id)` 查询实际容量。

每个器件用一个 `qspi_nor_dev_t` 描述符描述，通过 `QSPI_NOR_DEVICE_SECTION()` 宏放入
链接段 `.qspi_nor_device_list`，驱动启动时遍历该段按 Read ID 选中匹配项（与 NAND / LCD 面板段式
注册一致）。内置样板位于 ``` ap/components/bk_external_flash/qspi_flash/nor/``（``GD25Q128E ```，JEDEC `C8 40 18`）。

**新增一款 NOR（三步）**：

1. 复制 `nor/qspi_nor_gd25.c` 为新文件，修改 `name` / `id` / `id_len` /
   `geometry` 及与该器件不同的 opcode 与状态寄存器布局（重点 `reg.qe_sr_index` / `qe_bit` /
   `sr1_preserve_mask`，按数据手册确认），文件末尾用 `QSPI_NOR_DEVICE_SECTION(描述符符号)` 注册。
2. 把新文件加入构建（SDK 内置参考 `ap/components/bk_external_flash/CMakeLists.txt`，
   并把描述符符号追加到 `GLOBAL_FUNCTION_SYMBOLS` 以便非 whole-archive 链接下保活；
   客户私有器件放工程侧并加入工程 `CMakeLists.txt`）。
3. 编译烧录，启动日志应打印 `nor <name> detected, <N>MB`。全程无需改动驱动、链接脚本或注册函数。

**4 字节寻址 / \>16 MB**：描述符设 `cmd.addr_bytes = 4`，并给 ``` cmd.enter_4byte``（通常 0xB7）；
``bk_qspi_flash_init() ``` 会在探测后自动进入 4 字节地址模式，所有带地址相位的读/写/擦除按 4 字节寻址。
个别器件四线 4B 读需 `0xEC` 而非 `0xEB`，由描述符 `cmd.quad_read` 指定。

<a id="id8"></a>

#### 工程侧适配示例（推荐客户使用）

与 SPI-NAND 一致，客户无需修改 SDK：把私有 NOR 描述符文件放进自己的工程目录、加入工程 `CMakeLists.txt` 即可。描述符经链接段自动收集，连 `ap_main.c` 都不用改（无注册函数调用）。
以 `projects/app` 为例：

1. 在工程 AP 侧新建描述符文件，例如
   `projects/app/ap/qspi_nor/qspi_nor_myflash.c`：

   ```
   #include <driver/qspi_nor_dev.h>
   #include <soc/soc.h>

   #if CONFIG_QSPI_NOR_FLASH

   const qspi_nor_dev_t qspi_nor_myflash_dev = {
       .name = "MYNOR",
       .id = {0xNN, 0xNN, 0xNN},      /* Read ID(9Fh)：MID + ID15-8 + ID7-0 */
       .id_len = 3,
       .geometry = { .total_size = 16U * 1024U * 1024U,
                     .sector_size = 4U * 1024U, .page_size = 256U, },
       /* 3 字节寻址通用命令集，见 nor/qspi_nor_gd25.c；>16MB 器件改为
        * .addr_bytes = 4 并换 4B opcode，见 nor/qspi_nor_xmc_xm25qh256.c */
       .cmd = { .read_id = 0x9F, .write_enable = 0x06,
                .read_sr1 = 0x05, .read_sr2 = 0x35, .write_sr1 = 0x01,
                .write_sr2 = 0x31, .page_program = 0x02,
                .quad_page_program = 0x32, .read = 0x03, .dual_read = 0x3B,
                .quad_read = 0xEB, .erase_sector = 0x20, .erase_32k = 0x52,
                .erase_64k = 0xD8, .addr_bytes = 3,
                .dual_read_dummy_cycle = 8, .dual_read_dummy_mode = 4,
                .quad_read_dummy_cycle = 4, .quad_read_dummy_mode = 5, },
       /* QE 所在状态寄存器与位、BP 保护位布局按数据手册确认 */
       .reg = { .qe_sr_index = 1, .qe_bit = BIT(1),
                .srp0_bit = BIT(7), .srp1_bit = BIT(0),
                .sr1_preserve_mask = 0x83, .bp_shift = 2, .bp_mask = 0x07, },
   };

   QSPI_NOR_DEVICE_SECTION(qspi_nor_myflash_dev);

   #endif
   ```
2. 在工程 `projects/app/ap/CMakeLists.txt` 的 `srcs` 里加入该文件：

   ```
   set(incs .)
   set(srcs
       ap_main.c
       qspi_nor/qspi_nor_myflash.c   # 新增：客户私有 NOR 描述符
       )

   set(priv_req bk_network_provisioning)

   armino_component_register(SRCS "${srcs}" INCLUDE_DIRS "${incs}" PRIV_REQUIRES "${priv_req}")
   ```
3. 重新编译工程即可。上电若探测到该器件，日志打印
   `nor MYNOR detected, 16MB`；读写/擦除与文件系统会按此容量与命令集自适应。

这样客户的 NOR 器件适配完全隔离在工程目录内，SDK 升级不受影响，也便于多工程各自维护不同器件表。

备注

NOR 未识别器件的行为由 `CONFIG_QSPI_NOR_ALLOW_UNKNOWN` 决定：为 ``` y``（默认）时告警后
用内置 GD 默认描述符继续（容量取 ``CONFIG_QSPI_NOR_FLASH_SIZE ```），便于新片调试；**量产建议设为** `n`，使未知器件初始化直接失败，避免按错误命令集/保护位/容量运行。

<a id="id9"></a>

## [状态寄存器与保护](#id21)

擦写前需确保 Flash 未处于写保护状态，并使能 QE（Quad Enable）位以支持四线传输。

| API | 说明 |
| --- | --- |
| `bk_qspi_flash_set_protect_none()` | 清除块保护位（BP） |
| `bk_qspi_flash_quad_enable()` | 设置 QE 位 |
| `bk_qspi_flash_read_s0_s7()` | 读状态寄存器 S0\~S7 |
| `bk_qspi_flash_read_s8_s15()` | 读状态寄存器 S8\~S15（含 QE） |
| `bk_qspi_flash_write_s8_s15()` | 写 S8\~S15（部分厂商 QE 在此寄存器） |

备注

不同厂商 Flash 的状态寄存器布局不同：部分器件 S0\~S7 与 S8\~S15 需分两次写入（命令 0x01 / 0x31），部分支持一次写入 S0\~S15。请对照器件手册选择对应 API。

<a id="spi-nand"></a>

## [SPI-NAND 补充说明](#id22)

开启 `CONFIG_QSPI_NAND_FLASH` 后，除共用 `bk_qspi_flash_init()` 外，还提供 NAND 专用 API：

- `bk_qspi_flash_nand_page_read()` / `bk_qspi_flash_nand_page_program()`
- `bk_qspi_flash_nand_block_erase()`
- `bk_qspi_flash_nand_read_oob()` / `bk_qspi_flash_nand_write_oob()`
- `bk_qspi_flash_nand_is_factory_bad()` / `bk_qspi_flash_nand_mark_bad()`

几何参数：页 2 KB，块 64 页（128 KB）。应用层建议通过 Dhara FTL 访问，避免直接操作坏块管理。

<a id="id10"></a>

### 多型号支持与新增器件

SPI-NAND 驱动支持多型号自动识别：`bk_qspi_flash_init()` 会读取 JEDEC ID（9Fh），
在已注册的器件描述符中匹配型号，容量、写保护位等从命中的描述符获取，FTL/坏块管理
按识别到的容量自适应。可用 `bk_qspi_flash_nand_total_size(id)` 查询实际容量。

每个器件用一个 `qspi_nand_dev_t` 描述符描述，并通过
`QSPI_NAND_DEVICE_SECTION()` 宏放入链接段 `.qspi_nand_device_list`，驱动启动时
遍历该段按 Read ID 选中匹配项（与 LCD 面板/Camera Sensor 的段式注册一致，区别在于
NAND 由 JEDEC ID **自动探测**，无需应用层指定型号）。

备注

QSPI NOR/NAND 协议引擎、坏块管理与内置器件描述符已从 `ap/middleware` 迁至
组件 ``` ap/components/bk_external_flash/qspi_flash/``（客户可修改；middleware 只保留
QSPI 控制器与 QSPI-PSRAM）。公共 API（``bk_qspi_flash_* ```）与 Kconfig 选项
（`CONFIG_QSPI_NOR_FLASH` / `CONFIG_QSPI_NAND_FLASH` 等）保持不变，仍在
`menuconfig` 的 QSPI 菜单下配置。换料或改协议请改
`bk_external_flash`，无需改动 middleware。

内置描述符位于 `ap/components/bk_external_flash/qspi_flash/nand/`：

| 型号 | JEDEC ID | 容量 |
| --- | --- | --- |
| ZB35Q01CYIG | `5E C1` | 128 MB |
| GD5F05M7UE | `C8 90` | 64 MB |
| GD5F05M7RE | `C8 80` | 64 MB |

**新增一款 Flash（三步）**：

1. 复制 `qspi_nand_zb35q01.c` 为新文件，修改 `name` / `id` / `id_len` /
   `geometry.total_size` 及与该器件不同的位域（重点 `bit.wp_enable`，按数据手册确认；
   命令集若与通用 SPI-NAND 一致可沿用模板），文件末尾用
   `QSPI_NAND_DEVICE_SECTION(描述符符号)` 注册。
2. 把新文件加入所在组件构建（SDK 内置参考
   `ap/components/bk_external_flash/CMakeLists.txt`，同时把描述符符号
   追加到 `GLOBAL_FUNCTION_SYMBOLS` 以便非 whole-archive 链接下保活；客户私有器件
   放工程侧并加入工程 `CMakeLists.txt`）。
3. 编译烧录，启动日志应打印 `nand <name> detected, <N>MB`。全程无需改动驱动、
   链接脚本或注册函数。

<a id="id11"></a>

#### 工程侧适配示例（推荐客户使用）

客户无需修改 SDK，只要把私有器件的描述符文件放进自己的工程目录、加入工程 `CMakeLists.txt` 即可。由于描述符通过链接段自动收集，连 `ap_main.c` 都不用改（无注册函数调用）。以 `projects/app` 为例：

1. 在工程 AP 侧新建描述符文件，例如
   `projects/app/ap/qspi_nand/qspi_nand_myflash.c`：

   ```
   #include <driver/qspi_nand_dev.h>
   #include <soc/soc.h>

   #if CONFIG_QSPI_NAND_FLASH

   const qspi_nand_dev_t qspi_nand_myflash_dev = {
       .name = "MYFLASH",
       .id = {0xNN, 0xNN},            /* Read ID(9Fh) 返回字节 */
       .id_len = 2,
       .geometry = { .total_size = 64U * 1024U * 1024U,
                     .page_size = 2048U, .spare_size = 64U,
                     .pages_per_block = 64U, },
       .cmd = { /* 通常沿用通用 SPI-NAND 命令集，见 qspi_nand_zb35q01.c */ },
       .reg = { .block_lock = 0xA0, .configuration = 0xB0,
                .status = 0xC0, .block_unlock_value = 0x00, },
       .bit = { .oip = BIT(0), .wel = BIT(1),
                .wp_enable = BIT(1),  /* 按数据手册确认 */
                .ecc_status_mask = BIT(4) | BIT(5), .ecc_status_shift = 4,
                .ecc_uncorrectable = 0x2, /* ... */ },
   };

   QSPI_NAND_DEVICE_SECTION(qspi_nand_myflash_dev);

   #endif
   ```
2. 在工程 `projects/app/ap/CMakeLists.txt` 的 `srcs` 里加入该文件：

   ```
   set(incs .)
   set(srcs
       ap_main.c
       qspi_nand/qspi_nand_myflash.c   # 新增：客户私有 SPI-NAND 描述符
       )

   set(priv_req bk_network_provisioning)

   armino_component_register(SRCS "${srcs}" INCLUDE_DIRS "${incs}" PRIV_REQUIRES "${priv_req}")
   ```
3. 重新编译工程即可。上电若探测到该器件，日志打印
   `nand MYFLASH detected, 64MB`；FTL/FATFS 会按此容量自适应。

这样客户的器件适配完全隔离在工程目录内，SDK 升级不受影响，也便于多工程各自维护不同器件表。

备注

页/块几何当前固定校验为 2048 / 64 页，几何不一致的器件会被 `nand_probe()` 拒绝。
未识别器件的行为由 `CONFIG_QSPI_NAND_ALLOW_UNKNOWN` 决定：为 ``` y``（默认）时告警后
用默认描述符继续（容量取 ``CONFIG_QSPI_NAND_FLASH_SIZE ```），便于新片调试；**量产建议设为** `n`，使未知器件初始化直接失败，避免按错误容量/保护位运行。

<a id="id12"></a>

## [典型使用流程（NOR）](#id23)

```
bk_qspi_driver_init();
bk_qspi_flash_init(QSPI_ID_1);

uint32_t id = bk_qspi_flash_read_id(QSPI_ID_1);

bk_qspi_flash_erase_sector(QSPI_ID_1, 0x0);

uint8_t buf[256];
// ... 填充 buf ...
bk_qspi_flash_write(QSPI_ID_1, 0x0, buf, sizeof(buf));

uint8_t read_buf[256];
bk_qspi_flash_read(QSPI_ID_1, 0x0, read_buf, sizeof(read_buf));
```

<a id="id13"></a>

## [常见问题](#id24)

<a id="qspi"></a>

### QSPI 支持哪些线宽？

控制器支持 1/2/4 线半双工。Flash 驱动 API 封装了单线、双线、四线接口；`CONFIG_QSPI_LINE_MODE` 决定 `bk_qspi_flash_read/write` 默认走双线还是四线。

<a id="flash-id"></a>

### 获取 Flash ID 失败？

1. 检查 Flash 供电（通常 3.3 V）
2. 确认 QSPI 已初始化，管脚映射正确
3. 检查 SCK 频率是否过高（最大 80 MHz）
4. 确认 CS、DAT 接线与 QSPI ID 匹配

<a id="id"></a>

### 读 ID 正确但擦写失败？

1. 检查是否已 `bk_qspi_flash_set_protect_none()`
2. 四线读写前确认 QE 位已置位（`bk_qspi_flash_quad_enable()`）
3. 写入前是否已擦除对应扇区
4. 对照器件手册确认状态寄存器写入命令与位域
