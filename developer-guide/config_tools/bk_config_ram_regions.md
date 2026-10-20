---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/config_tools/bk_config_ram_regions.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ram"></a>

<a id="bk-config-ram-regions"></a>

# RAM资源分区配置

备注

本节旨在介绍如何为工程配置RAM资源

<a id="ram-regions"></a>

## RAM Regions配置表

RAM Regions配置表为 csv 文件，以下为一个配置示例

| #Name | Type | Offset | Size |
| --- | --- | --- | --- |
| AP\_SPINLOCK | SRAM | 0x28000000 | 0x010000 |
| AP\_RAM | SRAM |  | 0x054000 |
| CP\_RAM | SRAM |  | 0x03b800 |
| SWAP | SRAM |  | 0x000800 |
| PSRAM\_MEM\_SLAB\_UNCODED | PSRAM | 0x60000000 | 工程配置 |
| PSRAM\_MEM\_SLAB\_CODED | PSRAM | 0x64000000 | 工程配置 |
| CP\_PSRAM\_HEAP | PSRAM |  | 工程配置 |
| AP\_PSRAM\_DATA\_SECTION | PSRAM |  | 工程配置 |
| AP\_PSRAM\_HEAP | PSRAM |  | 工程配置 |
| AP\_PSRAM\_CACHE\_HEAP | PSRAM |  | 工程配置 |
| AP\_PSRAM\_CODE\_SECTION | PSRAM |  | 工程配置 |

在自动分区表中，不可修改SRAM的基地址和大小，不可修改PSRAM的基地址，但可根据实际情况配置PSRAM的大小，如下:

```
PSRAM_CAPACITY_SIZE=8M
```

BK7259 当前推荐布局中，`AP_PSRAM_HEAP` 用于普通 AP PSRAM 动态分配，默认
non-cacheable；`AP_PSRAM_CACHE_HEAP` 用于 OS task 创建路径中的 PSRAM task 相关分配，
默认 L2 write-back cacheable。各工程可以独立配置大小，允许分区之间存在空洞，但不能重叠。
建议将 cache 属性相同的 PSRAM 分区连续放置，以减少 MPU region 占用。

`AP_PSRAM_CACHE_HEAP` 的大小应根据工程中 PSRAM task stack 的峰值需求预留；非 fast boot
场景还需考虑 TCB 等任务内部对象开销。客户业务 buffer 不应从该区域分配，应继续使用
`psram_malloc` / `psram_zalloc` 申请普通 non-cacheable PSRAM。

分区表固定为六列：

> - `Name` \- 必选项，表示分区名字。
>
>   - **分区名必须唯一**。构建系统会依据分区名字来生成一组宏，只有分区名字唯一才能确保生成宏不会重复定义。
> - `Type` \- 必选项。可配置为SRAM或PSRAM时，表示分区所属RAM类型。
> - `Offset` \- 可选项。表示分区的物理偏移地址，表中第一项必须填写，后续项缺省时，偏移地址为上一项结束地址。
> - `Size` \- 必选项。表示分区大小。

若有修改SRAM或PSRAM分区的需求，可修改ram分区表 ram\_regions.csv：

> - 基于自动化分区CSV表 partitions/bk7259/ram\_regions.csv 进行分区信息修改
>
>   - RAM分区的地址空间需要在有效范围内
> - 修改分区后 建议使用make clean清理编译缓存

编译后在build目录下生成ram\_regions.h头文件，所有的.c文件都会默认包含这个文件，在开发过程中默认可直接使用此头文件定义的宏。
编译时将会生成相关的ADDR宏定义和SIZE宏定义，如AP\_SPINLOCK分区将会生成 `CONFIG_AP_SPINLOCK_ADDR` 和 `CONFIG_AP_SPINLOCK_SIZE` 宏定义。

<a id="psram-mpu"></a>

## PSRAM MPU 自动配置

BK7259 的 AP 侧 PSRAM MPU 不再使用固定地址边界。构建系统根据
`partitions/bk7259/ram_regions.csv` 中各 PSRAM 分区的实际地址和分区名生成 MPU
配置，因此移动 `AP_PSRAM_HEAP`、`AP_PSRAM_DATA_SECTION` 或其它 PSRAM 分区后，
不需要再手工修改 `mpu_cfg.c` / `mpu_cfg_s.c`。

配置生成流程如下：

> 1. 读取并校验 `ram_regions.csv`，展开省略的 Offset。
> 2. 根据分区名查找 MPU 属性策略；未单独配置的 PSRAM 分区使用默认属性。
> 3. 未分配的地址空洞使用默认属性，避免留下未受 MPU 管理的 PSRAM 地址。
> 4. 合并地址连续且 MPU 属性相同的分区，减少硬件 MPU region 的占用。
> 5. 按 MPU 要求处理 32 字节边界，在 `ram_regions.h` 中生成
>    `CONFIG_PSRAM_MPU_REGION_<n>_{BASE,LIMIT,ATTR}`。
> 6. 同时生成 `CONFIG_PSRAM_MPU_NS_REGION_<n>_{BASE,LIMIT}`，供 Secure MPU
>    配置 Non-Secure PSRAM 别名。
> 7. `mpu_cfg.c` 和 `mpu_cfg_s.c` 根据 `CONFIG_PSRAM_MPU_REGION_COUNT`
>    注册实际生成的 MPU region。

BK7259 当前为 AP PSRAM 预留最多 4 个 MPU region。若某种分区排列在合并后仍需要
5 个或更多 region，构建会报错，而不是静默丢弃 MPU 配置。此时应调整分区顺序，
使相同属性的分区尽量连续，或重新评估属性划分。

支持的 PSRAM MPU 属性如下：

| 策略名称 | attr index | 含义 |
| --- | --- | --- |
| `NON_CACHE` | 1 | L1/L2 均不缓存 |
| `L1_L2_WRITE_BACK` | 3 | L1/L2 均为 write-back cache |
| `L2_WRITE_BACK` | 5 | L1 不缓存，L2 为 write-back cache |

<a id="id1"></a>

### 默认策略

平台默认策略位于
`tools/build_tools/build_process/bk_sdk/smp_ram_setting_bk7259.json`：

```
{
    "PSRAM_MPU_DEFAULT_ATTR": "NON_CACHE",
    "PSRAM_MPU_POLICIES": {
        "AP_PSRAM_HEAP": "NON_CACHE",
        "AP_PSRAM_CACHE_HEAP": "L2_WRITE_BACK",
        "AP_PSRAM_CODE_SECTION": "L1_L2_WRITE_BACK"
    }
}
```

因此，默认情况下：

> - `AP_PSRAM_HEAP` 使用 attr 1，作为普通 non-cacheable PSRAM heap。
> - `AP_PSRAM_CACHE_HEAP` 使用 attr 5，仅用于 OS task 创建路径中的 PSRAM task 相关分配。
> - `AP_PSRAM_CODE_SECTION` 使用 attr 3，支持 L1/L2 cache。
> - 其它 PSRAM 分区（包括空洞）使用默认 attr 1，保持 non-cache。

<a id="region-mpu"></a>

### 工程级修改某个 region 的 MPU 属性

如果只需要修改某个工程，不应修改平台默认 JSON。请在该工程的
`partitions/bk7259` 目录中新建可选文件 `ram_regions_mpu.json`。JSON 的 key
必须与 `ram_regions.csv` 中的 PSRAM 分区名完全一致，value 为上表中的策略名称
或合法 attr index。

例如，要让某工程的 `AP_PSRAM_DATA_SECTION` 使用 L2 write-back cache，新建：

```
{
    "AP_PSRAM_DATA_SECTION": "L2_WRITE_BACK"
}
```

重新 clean 编译后，生成器会使用 attr 5 配置该分区，并在可能时将它与相邻的 attr 5
分区合并。如果填写了不存在的分区名、非法属性或最终超过 4 个 PSRAM MPU region，
构建会直接报错。

重要

修改 cache 属性会改变软件一致性要求。当前推荐方案下，普通业务 buffer 应保持
non-cacheable。若工程自行将某个业务分区改为 `L2_WRITE_BACK` 或
`L1_L2_WRITE_BACK`，且该内存会被 CP、DMA、WiFi/BT 或其它硬件 master 访问，
需要由工程自行评估并处理 cache 一致性。

<a id="id2"></a>

### 生成结果验证

修改分区或 MPU 属性后，建议执行以下检查：

> 1. clean 编译工程，确认没有 overlap、非法属性或 MPU region 超限错误。
> 2. 查看 `build/bk7259/<project>/partitions/ram_regions.h` 中的
>    `CONFIG_PSRAM_MPU_REGION_COUNT` 及各 region 的 BASE/LIMIT/ATTR。
> 3. 固件运行后执行 `ap_cmd mpudump`，确认 MPU 寄存器中的地址和 attr index
>    与生成头文件一致。
> 4. 若修改了 cache 属性，执行对应的 CP/DMA/外设共享 buffer 用例，验证 cache
>    一致性处理。

备注

当出现如下编译log时，表示出现RAM分区配置出错，出现分区地址重叠的情况:

> RuntimeError: RAM regions config overlaps
