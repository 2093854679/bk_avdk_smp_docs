---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_psram.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="psram"></a>

# PSRAM

<a id="id1"></a>

## 1 功能概述

- PSRAM相关的理论介绍参考: [PSRAM的驱动](../../developer-guide/peripheral/bk_psram.md)

备注

BK7259 平台 AP 与 CP 默认 defconfig 均使能 `CONFIG_PSRAM=y`。

<a id="id3"></a>

## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_psram.c`
> - 驱动源码路径：
>   :   `middleware\driver\psram\psram_driver.c`

备注

- 1.psram\_driver.c :PSRAM驱动实现代码
- 2.cli\_psram.c:PSRAM功能测试命令实现

<a id="id4"></a>

## 3 PSRAM 主要函数列表

<a id="id5"></a>

## 初始化与配置

```
bk_err_t bk_psram_init(void);
bk_err_t bk_psram_deinit(void);
bk_err_t bk_psram_id_auto_detect(void);
bk_err_t bk_psram_set_clk(psram_clk_t clk);
bk_err_t bk_psram_set_voltage(psram_voltage_t voltage);
```

描述：
\- 初始化和释放 PSRAM 硬件资源。examples/peripheral/bk\_i2c.html
\- 设置工作频率（如 80M/120M/160M）与供电电压（如 1.8V）。
\- 自动识别芯片 ID，适用于开机自适配流程。

<a id="id6"></a>

## 数据读写接口

```
bk_err_t bk_psram_memcpy(uint8_t *dst, uint8_t *src, uint32_t len);
bk_err_t bk_psram_memread(uint8_t *src, uint8_t *dst, uint32_t len);
```

描述：块状内存读写操作，性能优于 DTCM，可用于音视频缓存等场景。

<a id="id7"></a>

## 低层读写（字节/半字/字）

```
void bk_psram_byte_write(uint8_t *addr, uint8_t val);
void bk_psram_half_word_write(uint16_t *addr, uint16_t val);
void bk_psram_word_write(uint32_t *addr, uint32_t val);
void bk_psram_word_memcpy(void *dst, void *src, uint32_t len);
```

描述：支持非对齐数据的写操作，内部处理地址对齐与遮罩操作。

<a id="id8"></a>

## 字符串操作

```
char *bk_psram_strcat(char *start_addr, const char *data_buf);
```

描述：类似 strcat 的接口，将字符串追加写入 PSRAM。

<a id="heap"></a>

## Heap 初始化标志

```
bool bk_psram_heap_init_flag_get(void);
bk_err_t bk_psram_heap_init_flag_set(bool init);
```

描述：用于标识 PSRAM heap 是否已初始化，适用于动态内存分配管理。

<a id="write-through-area"></a>

## 写透区域（Write Through Area）管理

```
psram_write_through_area_t bk_psram_alloc_write_through_channel(void);
bk_err_t bk_psram_free_write_through_channel(psram_write_through_area_t area);
bk_err_t bk_psram_enable_write_through(psram_write_through_area_t area, uint32_t start, uint32_t end);
bk_err_t bk_psram_disable_write_through(psram_write_through_area_t area);
```

描述：
\- 写透区域适用于 DMA2D 高性能读写，不走 cache。
\- 配置区域地址需 32 字节对齐，写入数据需为 32 字节整数倍。
\- 每个区域仅允许一个主设备访问。

<a id="cli"></a>

## 4 cli命令简介

demo运行依赖的宏配置：

| NAME | Description | File | value |
| --- | --- | --- | --- |
| CONFIG\_PSRAM | support PSRAM | `middleware\soc\bk7236\bk7236.defconfig` | y |
| CONFIG\_PSRAM\_TEST | support PSRAM test command | `middleware\soc\bk7236\bk7236.defconfig` | y |

demo支持的命令如下表：

| Command | Param | Description |
| --- | --- | --- |
| psram\_test start | cpu  cacheable: 0/1 delay\_time: N | Test the read/write function of PSRAM. Options: Enable or disable cache. Number of loop delays. Cache base \= 0x64000000 |
| psram\_test stop | none | Stop test psram |
| psram\_task\_create | none | Create a task using PSRAM memory |
| psram\_test start | dma cacheable: 0/1 delay\_time: N | Use DMA copy instead of CPU Enable or disable cache Number of loop delays |
