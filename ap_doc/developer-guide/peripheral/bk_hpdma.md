---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_hpdma.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="hpdma"></a>

# HPDMA 使用指南

:

<a id="id1"></a>

## 概述

HPDMA（High Performance DMA）用于在存储器与外设之间进行高吞吐数据搬运。它提供普通通道模式和链表 descriptor 模式，适合显示、图形、音视频 buffer、PSRAM/SRAM 大块搬运等场景。

> - HPDMA 测试用例和命令说明请参考：[HPDMA 测试用例](../../examples/peripheral/bk_hpdma.md)
> - HPDMA API 定义路径：`ap/include/driver/hpdma.h`
> - HPDMA 类型定义路径：`ap/include/driver/hal/hal_hpdma_types.h`
> - HPDMA 驱动实现路径：`ap/middleware/driver/hp_dma/hpdma_driver.c`
> - HPDMA CLI 测试路径：`ap/middleware/driver/hp_dma/hpdma_test.c`

<a id="id3"></a>

## 1 HPDMA 特性

HPDMA 具有如下特性：

> - 支持 memory-to-memory 和 memory-to-peripheral 数据搬运。
> - 支持 `SINGLE` 和 `REPEAT` 工作模式。
> - 支持 8/16/32/64/128 bit 数据宽度配置。
> - 支持源地址和目的地址自增。
> - 支持源地址和目的地址 loop。
> - 支持 finish 和 half finish 中断。
> - 支持链表 descriptor 传输。
> - 支持 2D stride 传输。
> - 支持多通道并发工作。

当前 BK7259 AP 侧 HPDMA 通道数量由 `HPDMA_ID_MAX` 定义，当前枚举为 `HPDMA_ID_0` \~ `HPDMA_ID_3`。

<a id="id4"></a>

## 2 HPDMA 功能说明

<a id="id5"></a>

### 2.1 传输维度

HPDMA 使用 `xsize` 和 `ysize` 描述搬运规模：

> - `xsize`：每行搬运字节数。
> - `ysize`：搬运行数。用户配置中 `ysize=1` 表示 1 行，不能配置为 0。
> - `step`：2D 传输中相邻行之间的步进。

普通模式中，如果源和目的 `xsize` 都非 0，则源和目的总字节数必须相同：

```
src.xsize * src.ysize == dst.xsize * dst.ysize
```

链表模式中，每个 descriptor 使用 `hpdma_link_config_t` 描述一段传输：

```
typedef struct {
    uint32_t src_addr;
    uint32_t dst_addr;
    uint16_t src_xsize;
    uint16_t src_ysize;
    uint16_t dst_xsize;
    uint16_t dst_ysize;
    uint16_t src_step;
    uint16_t dst_step;
    uint8_t finish_int_en;
    uint8_t half_finish_int_en;
} hpdma_link_config_t;
```

<a id="id6"></a>

### 2.2 对齐要求

HPDMA 的 16 字节对齐限制仅适用于地址 loop 模式：

> - 普通传输和链表传输的 source/destination 地址、长度不强制 16 字节对齐。
> - 当 source 或 destination 使能 `addr_loop_en` 时，对应 loop window 的起始地址和结束地址需要 16 字节对齐。
> - 链表 descriptor table 需要 16 字节对齐。

如果 loop 模式的地址窗口未对齐，驱动会返回参数错误。

<a id="cache"></a>

### 2.3 Cache 一致性

当前推荐配置下，普通业务 buffer 应优先使用 non-cacheable 内存，通常不需要业务层手动
维护 cache 一致性。若工程自行引入 cacheable DMA buffer，需要结合内存属性、访问方向
和 buffer 生命周期单独设计一致性处理。无论内存属性如何，业务侧仍需避免以下行为：

> - DMA 传输未完成前释放 source 或 destination buffer。
> - DMA 传输未完成前复用 destination buffer。
> - 在未确认传输完成前读取 destination buffer 并作为最终结果。

推荐使用 finish interrupt、semaphore 或任务通知等待传输完成。

<a id="x2c-0x28"></a>

### 2.4 地址别名与 0x2C/0x28 转换约定

BK7259 的片内 SRAM 对 CPU 和外设暴露不同的地址别名：

> - `0x28xxxxxx`：外设别名，HPDMA 引擎只能访问这个别名。
> - `0x2Cxxxxxx`：CPU 侧别名（Bit26\=1），是否 cacheable 取决于 MPU 属性配置。

两个别名指向同一块物理 SRAM，仅 Bit26 不同。因此把一个 `0x2Cxxxxxx` 的 SRAM 指针直接交给 HPDMA，引擎是访问不到的，必须先转换为 `0x28xxxxxx`。

**约定：这层 0x2C-\>0x28 转换全部由驱动内部统一消化，应用层只管传自己持有的 0x2C 指针即可，无需关心别名。** 转换宏为 ``` SOC_SRAM_PERI_ADDR()``（定义于 ``ap/include/soc/bk7259/reg_base.h ```），带范围保护——只对 `0x2C000000 ~ 0x2CFFFFFF` 生效，PSRAM/QSPI/寄存器以及本就是 `0x28` 的地址原样透传，可无条件套用。

驱动已覆盖的转换点：

> - `src/dst start_addr` 寄存器（`bk_hpdma_init` / `bk_hpdma_set_src_start_addr` / `bk_hpdma_set_dest_start_addr`）
> - `src/dst loop_end_addr` 寄存器（loop 模式）
> - `src/dst pause_addr` 寄存器
> - `next_ll_addr` 寄存器（`bk_hpdma_set_next_ll_addr`）
> - 链表描述符的 `src_addr` / ``` dst_addr``（``bk_hpdma_link_set_desc ```）
> - 链表描述符的 `next_desc_addr` 链指针（`bk_hpdma_link_init`）

使用时需要注意的几条约定：

备注

**1\. 链表描述符必须经 API 构建，禁止直接写结构体。**
构建链表时只能通过 `bk_hpdma_link_init()` \+ `bk_hpdma_link_set_desc()` / `bk_hpdma_link_set_descs()` 填写内容。不要自行 `malloc` 一块内存后直接写 `hpdma_descriptor_t` 的 `src_addr` / `dst_addr` / `next_desc_addr` 字段——那样驱动只会转换首个 `next_ll_addr` 寄存器，描述符内部地址仍是 `0x2C`，引擎在第一个节点后就会 stall（`dma_en` 卡住、无 finish 中断）。这是”边构建边转换、不额外重扫链表”的性能取舍带来的契约。

备注

**2\. get 类接口返回的是 0x28 硬件别名，不做反向转换。**
`bk_hpdma_get_next_ll_addr()` 等返回的是硬件寄存器里的 `0x28` 值，不会反向转回 `0x2C`。当前仅用于判空/判”链表是否走完”（与 0 比较，别名无关），无功能影响。若要把返回值与应用持有的 `0x2C` 指针做比较，或做”当前地址 \- 缓冲基址”的偏移计算，需先用 ``` SOC_SRAM_CPU_ADDR()``（``0x28->0x2C ``` 反向宏）换算，否则会差 `0x04000000`。

备注

**3\. cacheable 特殊场景需使用 CPU 侧原始地址处理一致性。**
若工程自行配置了 cacheable DMA buffer，一致性处理应基于应用传入的 CPU 侧原始地址，
而不是写给硬件寄存器的 `0x28` 外设别名。当前推荐方案下，普通业务 buffer 默认
non-cacheable，应用通常不需要手动 clean/invalidate。

备注

**4\. 该转换依赖 CONFIG\_SRAM\_DIRECT\_ADDR。**
仅当 `CONFIG_SRAM_DIRECT_ADDR` 打开时 `SOC_SRAM_PERI_ADDR()` 才真正生效（关闭时为恒等宏）。若切换工程配置需留意 AP 侧是否使能。

<a id="hpdma-api"></a>

## 3 HPDMA API 使用流程

<a id="driver"></a>

### 3.1 Driver 初始化

所有 HPDMA API 使用前，需要先初始化 driver：

```
bk_err_t ret = bk_hpdma_driver_init();
if (ret != BK_OK) {
    return ret;
}
```

不再使用 HPDMA 时可调用：

```
bk_hpdma_driver_deinit();
```

<a id="id7"></a>

### 3.2 通道申请和释放

应用层需要先申请通道：

```
hpdma_id_t id = bk_hpdma_alloc(HPDMA_DEV_DTCM);
if (id >= HPDMA_ID_MAX) {
    return BK_FAIL;
}
```

使用完成后释放：

```
bk_err_t ret = bk_hpdma_free(HPDMA_DEV_DTCM, id);
if (ret == BK_ERR_HPDMA_TIMEOUT) {
    /*
     * 通道停止超时，驱动会保留该通道，避免硬件仍在访问旧 buffer。
     * 只有确认可以接受丢弃在途数据时，才使用强制回收。
     */
    bk_hpdma_force_reclaim(HPDMA_DEV_DTCM, id);
}
```

<a id="id8"></a>

### 3.3 普通模式

普通模式适合一次性配置一个通道，然后通过 `bk_hpdma_start()` 启动传输。

```
hpdma_config_t cfg = {0};

cfg.mode = HPDMA_WORK_MODE_SINGLE;
cfg.chan_prio = 2;

cfg.src.dev = HPDMA_DEV_DTCM;
cfg.src.width = HPDMA_DATA_WIDTH_32BITS;
cfg.src.addr_inc_en = HPDMA_ADDR_INC_ENABLE;
cfg.src.addr_loop_en = HPDMA_ADDR_LOOP_DISABLE;
cfg.src.start_addr = (uint32_t)src;
cfg.src.xsize = len;
cfg.src.ysize = 1;

cfg.dst.dev = HPDMA_DEV_DTCM;
cfg.dst.width = HPDMA_DATA_WIDTH_32BITS;
cfg.dst.addr_inc_en = HPDMA_ADDR_INC_ENABLE;
cfg.dst.addr_loop_en = HPDMA_ADDR_LOOP_DISABLE;
cfg.dst.start_addr = (uint32_t)dst;
cfg.dst.xsize = len;
cfg.dst.ysize = 1;

bk_hpdma_init(id, &cfg);
bk_hpdma_start(id);

/* 等待 finish 中断或按业务逻辑确认传输完成。 */

bk_hpdma_stop(id);
bk_hpdma_deinit(id);
bk_hpdma_free(HPDMA_DEV_DTCM, id);
```

备注

普通模式中 `hpdma chan {id} init` CLI 会自动准备一段 16 字节的默认 source/destination buffer，主要用于验证通道 init/start/stop/deinit 流程。实际业务代码应使用自己的 buffer 和配置。

<a id="id9"></a>

### 3.4 链表模式

链表模式适合多个 descriptor 串联，也适合 2D stride 传输。

```
void *desc = bk_hpdma_link_init(link_cnt);
if (desc == NULL) {
    return BK_FAIL;
}

hpdma_link_config_t cfg = {0};
cfg.src_addr = (uint32_t)src;
cfg.dst_addr = (uint32_t)dst;
cfg.src_xsize = len;
cfg.src_ysize = 1;
cfg.dst_xsize = len;
cfg.dst_ysize = 1;
cfg.finish_int_en = 1;

bk_hpdma_link_set_descs(desc, &cfg, 1);

bk_hpdma_register_isr(id, NULL, NULL, finish_cb, user_data);
bk_hpdma_enable_finish_interrupt(id);
bk_hpdma_link_transfer(id, desc);

/* finish_cb 中通知任务，任务侧等待完成后释放资源。 */

bk_hpdma_disable_finish_interrupt(id);
bk_hpdma_register_isr(id, NULL, NULL, NULL, NULL);
bk_hpdma_free(HPDMA_DEV_DTCM, id);
bk_hpdma_link_deinit(desc);
```

<a id="d-stride"></a>

### 3.5 2D stride 传输

2D 传输中，`xsize` 表示每行有效数据长度，`ysize` 表示行数，`step` 表示相邻行之间的地址步进。常见场景是从带 pitch 的图像 buffer 中搬运有效区域。

例如：

> - `xsize=128`：每行搬运 128 字节。
> - `ysize=8`：搬运 8 行。
> - `step=256`：源或目的相邻行间隔 256 字节。

如果 source 和 destination 使用不同布局，可分别配置 `src_step` 和 `dst_step`。

<a id="id10"></a>

### 3.6 内存拷贝接口

如果只需要做 memory-to-memory 拷贝，可使用便捷接口：

```
bk_err_t ret = bk_hpdma_memcpy(dst, src, len);
```

该接口会自动申请通道、配置、启动传输并释放通道。普通 memcpy 路径不要求 source/destination 地址或长度 16 字节对齐。

<a id="id11"></a>

## 4 中断回调

HPDMA 支持 half finish 和 finish 中断回调：

```
static void finish_cb(hpdma_id_t hpdma_id, void *user_data)
{
    beken_semaphore_t *sem = (beken_semaphore_t *)user_data;
    rtos_set_semaphore(sem);
}

bk_hpdma_register_isr(id, NULL, NULL, finish_cb, &sem);
bk_hpdma_enable_finish_interrupt(id);
```

备注

中断回调中不要做耗时操作，也不要高频打印日志。长时间压测中如果每次完成都打印日志，可能导致 shell 日志缓冲被打满。

<a id="id12"></a>

## 5 低压恢复和异常回收

低压唤醒后，HPDMA 控制器全局寄存器可能需要恢复。平台电源管理流程应在重新使用 HPDMA 前调用：

```
bk_hpdma_recover_after_low_voltage();
```

当释放通道返回 `BK_ERR_HPDMA_TIMEOUT` 时，表示 DMA engine 未在限定时间内停止。此时驱动会保留通道，避免新用户拿到仍可能访问旧 buffer 的通道。若业务确认可接受丢弃在途数据，可调用：

```
bk_hpdma_force_reclaim(HPDMA_DEV_DTCM, id);
```

<a id="id13"></a>

## 6 常见问题

<a id="source-ysize-must-be-1"></a>

### 6.1 `Source ysize must be >= 1`

原因：`src.ysize` 或 `dst.ysize` 配置为 0。

处理：用户配置中 `ysize=1` 表示 1 行，普通模式和链表模式都需要大于 0。

<a id="src-bytes-dst-bytes"></a>

### 6.2 `src bytes != dst bytes`

原因：源和目的总搬运字节数不一致。

处理：确保：

```
src.xsize * src.ysize == dst.xsize * dst.ysize
```

<a id="id14"></a>

### 6.3 释放通道超时

原因：DMA 硬件仍处于 busy 状态。

处理：先停止传输并等待 idle；确认可接受数据丢失后再强制回收。
