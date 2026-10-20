---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_qspi_filesystem.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="qspi-vfs-littlefs-fatfs"></a>

# [QSPI 文件系统（VFS/littleFS/FATFS）使用指南](#id10)

<a id="id1"></a>

目录

- [QSPI 文件系统（VFS/littleFS/FATFS）使用指南](#qspi-vfs-littlefs-fatfs)

  - [概述](#id2)
  - [整体架构](#id3)
  - [对应关系一览](#id4)
  - [选型建议](#id5)
  - [Kconfig 配置](#kconfig)
  - [VFS 挂载说明](#vfs)
  - [API 调用 demo（统一使用 VFS）](#api-demo-vfs)
  - [CLI 测试命令](#cli)
  - [命令行演示](#id8)
  - [常见问题](#id9)

<a id="id2"></a>

## [概述](#id11)

BK7259 在 QSPI NOR/NAND Flash 之上提供了一套完整的文件系统栈，从上到下分为三层：

- **VFS 层（统一接口）**：BK 虚拟文件系统（Virtual File System），对应用提供标准 POSIX 接口（`open` / `read` / `write` / `close` / `mount` 等），屏蔽底层文件系统与存储介质差异。
- **文件系统层**：littleFS 与 FATFS 两种实现，分别适用于不同场景。
- **介质与驱动层**：QSPI NOR Flash 与 QSPI SPI-NAND Flash，通过 QSPI 控制器访问。

重要

**强烈建议客户统一使用 VFS(POSIX) 接口访问文件系统。**

VFS 用标准 POSIX 语义封装了 littleFS / FATFS 的差异，也屏蔽了 QSPI NOR / NAND / SD 卡等不同存储介质的差异。
业务代码只需按 POSIX 方式读写文件，**切换文件系统或存储介质时业务逻辑零改动，只需修改一次性的挂载（mount）配置**，从而实现不同文件系统与不同存储介质的统一兼容管理。

只有在裸驱动调试、性能极限调优等特殊场景，才建议直接调用文件系统原生接口（`lfs_*` / `f_*`）或 QSPI 裸驱动（`bk_qspi_flash_*`），这些\*\*不作为日常推荐用法\*\*。

相关文档：

- QSPI 控制器：[QSPI 使用指南](bk_qspi.md)
- QSPI Flash 驱动：[QSPI Flash 使用指南](bk_qspi_flash.md)

<a id="id3"></a>

## [整体架构](#id12)

```
+-------------------------------------------------------------+
|                     应用程序 / 业务代码                       |
|            (统一 POSIX 接口: open/read/write/close)          |
+-------------------------------------------------------------+
                          |  #include "bk_posix.h"
                          v
+-------------------------------------------------------------+
|                  VFS 虚拟文件系统 (bk_vfs)                    |
|         注册的文件系统类型: "littlefs" / "fatfs"             |
+----------------------------+--------------------------------+
             |                                |
             v                                v
    +----------------+               +----------------+
    |    littleFS    |               |     FATFS      |
    +--------+-------+               +--------+-------+
             |                                |
     NOR ----+---- NAND             NOR ------+------ NAND
      |            |                 |                 |
      v            v                 v                 v
bk_qspi_flash_*   BBM         bk_qspi_flash_*     Dhara FTL
 (线性读写)   (坏块管理)      (线性,4KB扇区)   (512B逻辑扇区)
      |            |                 |                 |
      |     bk_qspi_flash_nand_*     |         bk_qspi_flash_nand_*
      v            v                 v                 v
+-------------------------------------------------------------+
|         QSPI 驱动 / QSPI 控制器 (QSPI0 / QSPI1)              |
+-------------------------------------------------------------+
```

**NOR 与 NAND 的底层路径差异（关键，容易混淆）：**

- **NOR Flash**：littleFS 与 FATFS 都直接走线性 `bk_qspi_flash_*` 接口。
- **NAND Flash**：

  - **littleFS on NAND** → 经 **BBM（坏块管理层）** → `bk_qspi_flash_nand_*`
  - **FATFS on NAND** → 经 **Dhara FTL（提供 512B 逻辑扇区、磨损均衡、掉电安全）** → `bk_qspi_flash_nand_*`

  两者中间层不同：littleFS 自带磨损均衡与坏块处理，只需 BBM 提供连续好块地址空间；FATFS 需要标准块设备，由 Dhara FTL 提供。

<a id="id4"></a>

## [对应关系一览](#id13)

| 介质 | 文件系统 | 中间层 | 底层 API |
| --- | --- | --- | --- |
| QSPI NOR | littleFS | 无（线性） | `bk_qspi_flash_*` |
| QSPI NOR | FATFS | disk\_io（4KB 扇区） | `bk_qspi_flash_*` |
| QSPI NAND | littleFS | BBM 坏块管理 | `bk_qspi_flash_nand_*` |
| QSPI NAND | FATFS | Dhara FTL（512B） | `bk_qspi_flash_nand_*` |

备注

VFS 内部实际注册的文件系统类型字符串只有 `"littlefs"` 和 `"fatfs"` 两个。
底层选择哪种介质（QSPI0 / QSPI1 等）不是靠文件系统类型区分，而是靠挂载时传入的\*\*分区结构体\*\*：

- littleFS：``` struct bk_little_fs_partition.part_type``（如 ``LFS_QSPI_FLASH ```）
- FATFS：``` struct bk_fatfs_partition.part_dev.device_name``（如 ``"qspi0_flash" ```）

CLI 里的 `qspi_lfs` / `qspi0_fatfs` 等只是\*\*测试子命令名\*\*，并非 VFS 的文件系统类型字符串。

<a id="id5"></a>

## [选型建议](#id14)

**接口层：无论选哪种文件系统，上层一律用 VFS(POSIX) 访问**，以获得统一的兼容管理能力。

**文件系统层选型：**

| 文件系统 | 适用场景 | 特点 |
| --- | --- | --- |
| littleFS | 参数/配置存储、日志、小文件、掉电频繁 | 掉电安全、磨损均衡、RAM 占用小 |
| FATFS | 需 PC 可读、USB MSC 挂载、大文件/多媒体 | 兼容 PC、生态成熟、可作 U 盘 |

<a id="kconfig"></a>

## [Kconfig 配置](#id15)

基础 QSPI 与介质（`menuconfig` → QSPI）
:   - `CONFIG_QSPI`：QSPI 驱动总开关
    - `CONFIG_QSPI_NOR_FLASH` 或 `CONFIG_QSPI_NAND_FLASH`：选择介质类型（互斥）
    - `CONFIG_QSPI_LINE_MODE`：Flash 线模式（NOR 建议 4）

VFS 层
:   - `CONFIG_VFS`：使能 VFS（依赖 `CONFIG_LITTLEFS` 或 `CONFIG_FATFS`）
    - `CONFIG_VFS_MAX_FD_NUM`：同时打开文件的最大个数（默认 20）
    - `CONFIG_VFS_TEST`：使能 `vfs` CLI 测试命令

littleFS
:   - `CONFIG_LITTLEFS`：使能 littleFS
    - `CONFIG_LFS_THREADSAFE`：线程安全（默认开启）

FATFS（及 NAND 所需 FTL）
:   - `CONFIG_FATFS`：使能 FATFS
    - `CONFIG_FATFS_QSPI_0_FLASH` / `CONFIG_FATFS_QSPI_1_FLASH`：将 QSPI0/QSPI1 挂为 FATFS 盘
    - `CONFIG_DHARA_FTL`：**FATFS on NAND 必需**，提供 512B 逻辑扇区块设备
    - `CONFIG_NAND_FTL_START_BLOCK` / `CONFIG_NAND_FTL_BLOCK_COUNT`：FTL 占用的 NAND 物理块范围（注意：无法借此与 littleFS/BBM 错开，BBM 按整片布局）

备注

本 SDK 中 **不存在** 旧文档提到的 `CONFIG_QSPI_FLASH` 与 `CONFIG_LITTLEFS_QSPI_FLASH_ID` 宏，请勿沿用。
QSPI 设备号由分区 `part_type` 推导（`LFS_QSPI_FLASH` → QSPI0，`LFS_QSPI_1_FLASH` → QSPI1）。

<a id="vfs"></a>

## [VFS 挂载说明](#id16)

VFS 的挂载通过 `mount()` 完成，首次使用（介质未格式化）需先 `mkfs()`。两者原型（经 `bk_posix.h` 重定向）如下：

```
int mount(const char *source, const char *target,
          const char *fs_type, unsigned long flags, const void *data);
int mkfs(const char *source, const char *fs_type, const void *data);
```

<a id="id6"></a>

### 各参数用途

| 参数 | 用途与取值 |
| --- | --- |
| `source` | 固定填 `"SOURCE_NONE"`。**介质不由 source 解析**，而由 data 分区结构体指定；此参数仅为 POSIX 形式保留 |
| `target` | 挂载点路径（如 `/qf0`）。仅作为 VFS 树中的挂载位置，按介质命名（见上文命名约定），后续文件路径均以此为前缀 |
| `fs_type` | 文件系统类型字符串，**只能是** `"littlefs"` 或 `"fatfs"` |
| `flags` | 挂载标志，当前填 `0` |
| `data` | **关键**：指向分区结构体，决定底层介质、分区与参数。littleFS 传 `struct bk_little_fs_partition *`，FATFS 传 `struct bk_fatfs_partition *` |

重要

`fs_type` 决定「用哪种文件系统」，`data` 分区结构体决定「用哪块介质/哪个分区」。
二者正交组合，这正是 VFS 能统一兼容不同文件系统与不同存储介质的核心。

<a id="littlefs-struct-bk-little-fs-partition"></a>

### littleFS 分区结构体关键字段（`struct bk_little_fs_partition`）

| 字段 | 用途 |
| --- | --- |
| `part_type` | 介质/接口选择：`LFS_QSPI_FLASH`（QSPI0）、`LFS_QSPI_1_FLASH`（QSPI1）；据此推导 QSPI 设备号 |
| `mount_path` | 挂载点路径，需与 `mount()` 的 `target` 一致 |
| `part_flash.start_addr` | 分区在 Flash 线性空间的\*\*起始字节地址\*\*（NAND 须 128KB 对齐） |
| `part_flash.size` | 分区\*\*大小（字节）\*\*（NAND 须为 128KB 块的整数倍） |

<a id="fatfs-struct-bk-fatfs-partition"></a>

### FATFS 分区结构体关键字段（`struct bk_fatfs_partition`）

| 字段 | 用途 |
| --- | --- |
| `part_type` | 分区类型，QSPI/SD 等设备类介质填 `FATFS_DEVICE` |
| `mount_path` | 挂载点路径，需与 `mount()` 的 `target` 一致 |
| `part_dev.device_name` | 设备名，决定底层介质：`FATFS_DEV_QSPI0_FLASH`(`"qspi0_flash"`)、`FATFS_DEV_QSPI1_FLASH`、`FATFS_DEV_SDCARD` 等 |

<a id="id7"></a>

### 挂载注意事项

- **首次格式化**：介质从未格式化时，先调用一次 `mkfs("SOURCE_NONE", fs_type, &part)` 再 `mount()`；已格式化的分区直接 `mount()` 即可，不要重复 `mkfs`（会清空数据）。
- **target 与 mount\_path 必须一致**：`mount()` 的 `target` 参数应与分区结构体的 `mount_path` 相同。
- **分区结构体生命周期**：`mount()` 只在挂载时读取分区信息，可用栈上局部变量；挂载完成后即可释放。
- **NAND 对齐**：littleFS on NAND 的 `start_addr` 与 `size` 必须 128KB 块对齐；FATFS on NAND 必须开启 `CONFIG_DHARA_FTL`。
- **fs\_type 只认全称**：只能是 `"littlefs"` / `"fatfs"`，不可用 `"lfs"` 或 CLI 子命令名（如 `"qspi_lfs"`）。
- **卸载**：使用结束调用 `umount(mount_path)`；重复挂载同一路径前需先卸载。

<a id="api-demo-vfs"></a>

## [API 调用 demo（统一使用 VFS）](#id17)

客户代码统一遵循两段式结构：**一次性的挂载配置\*\*（选文件系统 \+ 选介质） \+ \*\*统一的 POSIX 文件操作**。

备注

**挂载点命名约定**：挂载点（`mount_path`）只是 VFS 树中的一个路径，功能上可任意取名，但建议\*\*按存储介质/分区命名，而非按文件系统命名\*\*。
SDK 在 `bk_partition.h` 中已为各介质预定义了标准挂载路径与访问宏：

- QSPI0：`VFS_QSPI_FLASH_0_PATITION_0` \= `/qf0`，配套 `PATH_QSPI_FLASH_0_FILE("config.txt")`
- QSPI1：`VFS_QSPI_FLASH_1_PATITION_0` \= `/qf1`，配套 `PATH_QSPI_FLASH_1_FILE(...)`
- SD 卡：`VFS_SD_0_PATITION_0` \= `/sd0`

同一片介质无论跑 littleFS 还是 FATFS，都用同一个介质挂载点（如 QSPI0 统一用 `/qf0`）。
避免用 `/fat` / `/lfs` 这类按文件系统命名的挂载点，以免与「挂载点\=介质、文件系统可换」的模型冲突。

重要

调用 VFS/POSIX 接口前，必须包含头文件 `bk_posix.h`：

```
#include "bk_posix.h"
```

该头文件把标准 `open` / `read` / `write` / `close` / `mount` / `umount` / `mkfs` 等重定向到 VFS 实现（`bk_vfs_*`）。
**若不包含 bk\_posix.h，这些调用会落到系统/编译器自带原型上，导致行为异常或编译链接错误。**

统一的文件操作（与文件系统、介质无关）
:   以下读写代码对任何文件系统、任何介质都完全一致，是客户业务侧应固定使用的写法：

    ```
    #include "bk_posix.h"

    static void fs_demo_rw(const char *path)
    {
        int fd = open(path, O_RDWR | O_CREAT | O_TRUNC);
        if (fd < 0) {
            return;
        }

        const char *msg = "hello bk7259";
        write(fd, msg, strlen(msg));

        lseek(fd, 0, SEEK_SET);

        char buf[64] = {0};
        read(fd, buf, sizeof(buf) - 1);

        close(fd);
    }
    ```

组合 A：QSPI NOR \+ littleFS
:   仅挂载配置不同，读写沿用上面的 `fs_demo_rw()`：

    ```
    #include "bk_posix.h"
    #include "bk_partition.h"

    void demo_nor_littlefs(void)
    {
        struct bk_little_fs_partition part = {
            .part_type = LFS_QSPI_FLASH,                        /* QSPI0 介质 */
            .mount_path = VFS_QSPI_FLASH_0_PATITION_0,          /* "/qf0"，QSPI0 标准挂载点 */
            .part_flash = { .start_addr = 0, .size = 0x40000 }, /* 分区 256KB */
        };

        /* 首次使用需格式化：mkfs("SOURCE_NONE", "littlefs", &part); */
        mount("SOURCE_NONE", VFS_QSPI_FLASH_0_PATITION_0, "littlefs", 0, &part);

        /* PATH_QSPI_FLASH_0_FILE("config.txt") 展开为 "/qf0/config.txt" */
        fs_demo_rw(PATH_QSPI_FLASH_0_FILE("config.txt"));   /* 统一 POSIX 读写 */

        umount(VFS_QSPI_FLASH_0_PATITION_0);
    }
    ```

组合 B：QSPI NAND \+ FATFS
:   只改挂载段，业务读写代码完全不变（需 `CONFIG_DHARA_FTL` \+ `CONFIG_FATFS_QSPI_0_FLASH`）：

    ```
    #include "bk_posix.h"
    #include "bk_partition.h"

    void demo_nand_fatfs(void)
    {
        struct bk_fatfs_partition part = {
            .part_type = FATFS_DEVICE,
            .mount_path = VFS_QSPI_FLASH_0_PATITION_0,             /* "/qf0"，同为 QSPI0 介质 */
            .part_dev = { .device_name = FATFS_DEV_QSPI0_FLASH },  /* "qspi0_flash" */
        };

        /* 首次使用需格式化：mkfs("SOURCE_NONE", "fatfs", &part); */
        mount("SOURCE_NONE", VFS_QSPI_FLASH_0_PATITION_0, "fatfs", 0, &part);

        /* 挂载点与文件路径宏与组合 A 一致，仅文件系统与设备名不同 */
        fs_demo_rw(PATH_QSPI_FLASH_0_FILE("config.txt"));   /* 与组合 A 完全相同的读写代码 */

        umount(VFS_QSPI_FLASH_0_PATITION_0);
    }
    ```

组合 C（对照）：SD 卡 \+ FATFS
:   换存储介质同样只改 `device_name`，说明「换介质业务代码不变」：

    ```
    struct bk_fatfs_partition part = {
        .part_type = FATFS_DEVICE,
        .mount_path = VFS_SD_0_PATITION_0,                /* "/sd0"，SD 卡标准挂载点 */
        .part_dev = { .device_name = FATFS_DEV_SDCARD },  /* 仅此处不同（换介质） */
    };
    mount("SOURCE_NONE", VFS_SD_0_PATITION_0, "fatfs", 0, &part);
    /* PATH_SD_FILE("config.txt") 展开为 "/sd0/config.txt" */
    fs_demo_rw(PATH_SD_FILE("config.txt"));
    ```

**结论**：切换文件系统（littleFS↔FATFS）或存储介质（QSPI NOR↔NAND↔SD），客户只需修改 mount 段的分区结构体，`open/read/write/close` 业务逻辑零改动。

littleFS 与 FATFS 能否共用同一片 NAND
:   **不能。** littleFS on NAND 依赖的 BBM 按整片布局（坏块表固定在最高两块、备用池紧邻其下），
    没有起始块概念，必然与 Dhara FTL 的范围重叠，调 `CONFIG_NAND_FTL_START_BLOCK` 也错不开；
    且先后混用会因 ECC 写入污染 spare\[0\] 而让后者把已写块误判为出厂坏块。
    需要两种文件系统时，请分别使用 QSPI0 / QSPI1 两片器件。详见下文 CLI 测试命令一节的说明。

    NOR 则可以按地址范围错开：littleFS 用 `part_flash.start_addr/size`，FATFS 走线性盘，
    两者划分互不重叠的区域即可。

<a id="cli"></a>

## [CLI 测试命令](#id18)

重要

文件系统与 QSPI 驱动运行在 **AP 侧**，从串口下发命令时需加 ``` ap_cmd `` 前缀（本 SMP SDK 用法）。
例如：``ap_cmd vfs mount qspi_lfs /qf0 ```。

VFS 测试（推荐，需 `CONFIG_VFS_TEST`）
:   命令：`vfs`

    | 命令 | 说明 |
    | --- | --- |
    | `ap_cmd vfs format qspi_lfs` | QSPI0 littleFS 格式化（默认分区） |
    | `ap_cmd vfs format qspi_lfs <offset> <size>` | QSPI0 littleFS 按指定范围格式化（QSPI NAND 需 128KB 对齐） |
    | `ap_cmd vfs format qspi0_1_lfs` | QSPI0 littleFS 第二分区格式化 |
    | `ap_cmd vfs format qspi0_fatfs` | QSPI0 FATFS 格式化 |
    | `ap_cmd vfs mount qspi_lfs <mount_point>` | 挂载 QSPI0 littleFS 到指定路径 |
    | `ap_cmd vfs mount qspi_lfs <mount_point> <offset> <size>` | 按指定范围挂载 QSPI0 littleFS，范围需与格式化一致 |
    | `ap_cmd vfs mount qspi0_fatfs <mount_point>` | 挂载 QSPI0 FATFS 到指定路径 |
    | `ap_cmd vfs umount <mount_point>` | 卸载 |
    | `ap_cmd vfs write <file> <content>` | 写文件 |
    | `ap_cmd vfs read <file>` | 读文件 |
    | `ap_cmd vfs unlink <file>` | 删除文件 |
    | `ap_cmd vfs devs` | 列出所有存储设备及本次编译中 littlefs / fatfs 的可用性 |
    | `ap_cmd vfs bench <dev> [lfs|fatfs|all] [file_kb] [rounds]` | 一键性能 \+ 数据校验测试（前台跑完出报告，**破坏性**） |
    | `ap_cmd vfs soak start <dev> [lfs|fatfs] [file_kb]` | 后台长时间挂测（导入/老化测试用，**破坏性**）；`stop` / `status` 停止与查询 |
    | `ap_cmd vfs threadsafe_test <tasks> [file_kb] [mount_point]` | 多任务并发压测；`stop` / `status` 查询与停止 |

设备参数 `<dev>`
:   介质与文件系统是 **正交** 的两个维度：`<dev>` 选介质/接口，`lfs`/`fatfs` 选文件系统。
    新增一种介质只需在设备表里加一行，不必新增一组子命令。

    | `<dev>` | 默认挂载点 | littleFS | FATFS |
    | --- | --- | --- | --- |
    | `flash` | `/if0` | 片内 Flash 分区表中的 littlefs 分区 | 需 `CONFIG_FATFS_INTERNAL_FLASH` |
    | `spi0` / `spi1` | `/sf0` / `/sf1` | 需 `CONFIG_SPI_MST_FLASH` | 需 `CONFIG_FATFS_SPI_0_FLASH` / `_1_` |
    | `qspi0` / `qspi1` | `/qf0` / `/qf1` | 需 `CONFIG_QSPI_NOR_FLASH` 或 `CONFIG_QSPI_NAND_FLASH` | 需 `CONFIG_FATFS_QSPI_0_FLASH` / `_1_` |
    | `sd` | `/sd0` | 不支持 | 需 `CONFIG_FATFS_SDCARD` |

    设备表始终列出全部设备，某个组合在当前编译配置下不可用时会明确提示缺哪个宏，
    而不是报“未知设备”。用 `ap_cmd vfs devs` 可直接查看当前固件的可用性矩阵。

    `qspi1` 还要求芯片存在第二个 QSPI 单元（`SOC_QSPI_UNIT_NUM > 1`，BK7259 为 2）。

    **NOR / NAND 不是 dev 参数**：它由编译期互斥宏 `CONFIG_QSPI_NOR_FLASH` /
    `CONFIG_QSPI_NAND_FLASH` 决定，运行时无法选择，也意味着两个 QSPI 口只能接同类型器件。

`vfs format` / `vfs mount` 的两种写法
:   推荐使用与上面一致的正交写法：

    ```
    ap_cmd vfs format <dev> <lfs|fatfs> [offset size]
    ap_cmd vfs mount  <dev> <lfs|fatfs> [mount_point] [offset size]
    ```

    原有的 `qspi_lfs` / `qspi0_fatfs` / `flash_fatfs` / `spi_lfs` / `qspi0_1_lfs` 等
    写法把介质和文件系统混在一个名字里，**作为 legacy 别名继续保留**，现有脚本无需修改。
    其中 `qspi0_1_lfs`（QSPI0 第二个 littlefs 分区）只有 legacy 写法。

    `offset size` 目前只支持 QSPI littleFS，用于覆盖默认测试分区；FATFS 暂不支持运行时指定范围，
    继续使用原有全盘 / FTL 配置。QSPI NAND 上 `offset` 与 `size` 必须按 128KB block 对齐，
    QSPI NOR 上按 4KB sector 对齐。格式化和挂载必须使用同一组范围参数。

性能 \+ 校验测试（`vfs bench` / `vfs soak`）
:   两条命令共用同一套测试内核：按伪随机序列（LCG，每轮换种子）写满一个文件，再整文件回读，
    做 **逐字节比对 \+ CRC32 双重校验**，只对 `write()` / `read()` 计时（用 AON-RTC 微秒计数），
    因此吞吐数字反映存储栈本身而不含比对开销。

    `vfs bench` 前台执行，跑完打印报告；`vfs soak` 起后台任务持续循环，
    每 16 轮打印一次累计统计，适合作为 **Flash 导入 / 长时间挂测** 命令。

    报告字段：

    | 字段 | 含义 |
    | --- | --- |
    | `rounds` / `pass` | 总轮数 / 通过轮数，两者不等即有失败 |
    | `Write` / `Read` | 累计字节数、累计耗时、平均吞吐（KB/s） |
    | `crc_err` | 整文件 CRC32 不一致的次数 |
    | `bad_bytes` / `first_bad_off` | 比对失败的字节总数 / 首个错误字节偏移 |
    | `IO errors` | `open` / `read` / `write` 返回失败的次数 |
    | `ECC corrected` / `uncorrectable` | NAND 片内 ECC 累计纠错次数 / 不可纠错次数。**corrected 持续增长是 NAND 老化最早的信号**， 此时数据仍正确、上层不报错，但 ECC 余量已在消耗，适合作为挂测的主要观察指标 |

    命令结束会额外打印所在中间层的坏块统计（littleFS 走 BBM，FATFS 走 Dhara FTL）。

    **NOR 与 NAND 通用。** 三条命令都走 VFS 挂载配置（`LFS_QSPI_FLASH` / `FATFS_DEV_QSPI0_FLASH`），
    这套配置本身与介质无关：底层是 NOR 还是 NAND 由编译期的 `CONFIG_QSPI_NOR_FLASH` /
    `CONFIG_QSPI_NAND_FLASH`（二选一）决定，littleFS 适配层与 FATFS `disk_io` 各自在内部分流。
    所以同一条命令在 NOR 工程上直接可用，无需改动，区别只有：

    - NOR 不需要 `CONFIG_DHARA_FTL`（该宏 `depends on QSPI_NAND_FLASH`，NOR 下不可选）
    - NOR 没有坏块与片内 ECC，报告不输出 `ECC` 与坏块统计
    - **分区容量不同**：QSPI0 littleFS 分区在 NAND 上是 1MB，在 NOR 上只有 256KB
      （见 `qspi_lfs_p0_size`）。命令会在挂载后用 `statfs()` 查询实际可用空间，
      请求超出时自动下调并打印 `exceeds ... capacity, using NKB`，因此默认参数在两种介质上都能跑通，
      不需要针对 NOR 另外指定 `file_kb`。

警告

`vfs bench` 与 `vfs soak` 都是 **破坏性** 操作：每次运行都会先 `mkfs` 重新格式化 QSPI0 NAND
上的 `/qf0` 分区，原有数据全部丢失。请勿在带有用户数据的产品机上执行。

重要

**同一片 SPI-NAND 上 littleFS 与 FATFS 无法共存，也不能先后混用。**

littleFS on NAND 走 BBM，而 BBM 的布局按 **整片** 计算（坏块表固定在最高两块、
备用池紧邻其下，见 `qspi_nand_bbm.c`），没有起始块概念；FATFS on NAND 走 Dhara FTL，
范围由 `CONFIG_NAND_FTL_START_BLOCK` / `CONFIG_NAND_FTL_BLOCK_COUNT` 决定。
两者必然重叠，**调整 \`\`CONFIG\_NAND\_FTL\_START\_BLOCK\`\` 并不能把它们错开**。

先后混用同样不行：开着片内 ECC 写过的页，其 spare\[0\] 不再是 0xFF，
而出厂坏块检查恰恰是 **关掉 ECC 去读 spare\[0\]**，于是先跑的文件系统写过的块
会被后跑的那个当成出厂坏块。Dhara 连续撞上 `DHARA_MAX_RETRIES`（8）个”坏块”后，
`mkfs` 直接失败并报 `Too many bad blocks`。

因此在 NAND 设备上 `vfs bench <dev> all` 会 **直接拒绝执行** 并提示改用单一文件系统；
`vfs soak` 本来就一次只测一种。需要在同一片 NAND 上换文件系统时，必须先用
`qspi_nand block_erase <blk>` 把先前使用过的块裸擦一遍（这些块已知是好块，擦除安全），
再格式化新的文件系统。

NOR 无此问题：没有 spare 与坏块标记，两种文件系统可以先后各自 `mkfs`，
`vfs bench <dev> all` 正常可用。

其他底层测试命令（调试用，非日常推荐）
:   - ``` ap_cmd fatfstest ...``（``CONFIG_FATFS ```）：直连 FATFS，QSPI0 盘号为 6，如 `ap_cmd fatfstest M 6` 挂载、`ap_cmd fatfstest F 6` 格式化
    - `ap_cmd qspi_flash ...` / ``` ap_cmd qspi_nand ...``（``CONFIG_QSPI_TEST ```）：QSPI 裸驱动读写
    - `ap_cmd qspi_nand range_loop <offset> <size> <times> [tag] [print_cnt]`：指定 NAND 区域反复执行预读、擦除、擦后读校验、写入、写后读校验（**破坏性**，offset/size 需 128KB 对齐）
    - ``` ap_cmd nand_ftl ...``（``CONFIG_DHARA_FTL ```）：Dhara FTL 层测试

<a id="id8"></a>

## [命令行演示](#id19)

NOR \+ littleFS
:   ```
    ap_cmd vfs format qspi_lfs
    ap_cmd vfs mount qspi_lfs /qf0
    ap_cmd vfs write /qf0/test.txt BK7259_littlefs
    ap_cmd vfs read /qf0/test.txt
    ap_cmd vfs umount /qf0
    ```

NAND \+ FATFS
:   需工程已开启 `CONFIG_QSPI_NAND_FLASH` \+ `CONFIG_DHARA_FTL` \+ `CONFIG_FATFS_QSPI_0_FLASH`。

    ```
    ap_cmd vfs format qspi0_fatfs
    ap_cmd vfs mount qspi0_fatfs /qf0
    ap_cmd vfs write /qf0/test.txt BK7259_fatfs
    ap_cmd vfs read /qf0/test.txt
    ap_cmd vfs umount /qf0
    ```

一键性能 \+ 校验测试
:   一条命令在指定设备上依次测完 littleFS 与 FATFS（各 256KB 文件、8 轮），自动完成格式化与挂载：

    ```
    ap_cmd vfs devs                    # 先看当前固件支持哪些设备
    ap_cmd vfs bench qspi0 all 256 8
    ap_cmd vfs bench qspi1 all 256 8   # 第二个 QSPI 口
    ap_cmd vfs bench sd fatfs 1024 4   # SD 卡只支持 fatfs
    ```

    典型输出：

    ```
    === VFS BENCH: littlefs on qspi0 ===
      file=256KB rounds=8 pass=8
      Write: 2097152 B in 2269005 us, avg 902.6 KB/s
      Read : 2097152 B in 617570 us, avg 3316.2 KB/s
      Verify: crc_err=0 bad_bytes=0 first_bad_off=-
      IO errors: 0   ECC corrected: 42  uncorrectable: 0
    === RESULT: PASS (littlefs on qspi0) ===
    ```

Flash 导入长时间挂测
:   后台跑，随时查看累计统计；不停则一直跑下去：

    ```
    ap_cmd vfs soak start qspi0 lfs 256
    ap_cmd vfs soak status
    ap_cmd vfs soak stop
    ```

多任务并发压测
:   需先自行挂载，再在该挂载点下起多个任务并发读写校验：

    ```
    ap_cmd vfs format qspi0 lfs
    ap_cmd vfs mount qspi0 lfs
    ap_cmd vfs threadsafe_test 4 64 /qf0
    ap_cmd vfs threadsafe_test status
    ap_cmd vfs threadsafe_test stop
    ```

    `mount_point` 省略时默认 `/qf0`。注意该参数必须是 **已挂载** 的路径：
    VFS 按挂载点前缀解析路径，传入未挂载的路径会导致每次 `open` 都失败。

<a id="id9"></a>

## [常见问题](#id20)

调用文件接口编译报错或行为异常？
:   确认业务文件已 `#include "bk_posix.h"`，否则 `open/read/write` 等会落到系统原型上。

挂载时文件系统类型字符串填什么？
:   只能是 `"littlefs"` 或 `"fatfs"`；`"lfs"`、`"qspi_lfs"` 等不是有效的 fs\_type。

FATFS 挂在 NAND 上失败？
:   FATFS on NAND 必须开启 `CONFIG_DHARA_FTL`（提供 512B 逻辑扇区）；NOR 则无需 FTL。

littleFS 挂在 NAND 上分区大小要求？
:   NAND 擦除单位为 128KB 块，分区 `start_addr` 与 `size` 必须按 128KB 块对齐。

littleFS 与 FATFS 想共用一片 NAND？
:   做不到。BBM 按整片布局，与 Dhara FTL 必然重叠；先后混用还会因 ECC 污染 spare\[0\]
    导致后者报 `Too many bad blocks`。请改用 QSPI0 / QSPI1 两片器件分别承载。
    若必须在同一片上换文件系统，先 `qspi_nand block_erase <blk>` 裸擦先前用过的块再格式化。
