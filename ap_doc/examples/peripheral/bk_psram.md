# PSRAM



## 1 功能概述


- PSRAM相关的理论介绍参考: [PSRAM的驱动](../../developer-guide/peripheral/bk_psram.md "../../developer-guide/peripheral/bk_psram.md")

备注

默认BK7258 CP侧已经开启PSRAM功能，AP侧无需额外开启PSRAM使能。


## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_psram.c`
> - 驱动源码路径：
>   :   `middleware\driver\psram\psram_driver.c`

备注


- 1.psram_driver.c :PSRAM驱动实现代码

- 2.cli_psram.c:PSRAM功能测试命令实现


## 3 PSRAM 主要函数列表


## 初始化与配置


```
bk_err_t bk_psram_init(void);
bk_err_t bk_psram_deinit(void);
bk_err_t bk_psram_id_auto_detect(void);
bk_err_t bk_psram_set_clk(psram_clk_t clk);
bk_err_t bk_psram_set_voltage(psram_voltage_t voltage);

```

描述：

- 初始化和释放 PSRAM 硬件资源。examples/peripheral/bk_i2c.html

- 设置工作频率（如 80M/120M/160M）与供电电压（如 1.8V）。

- 自动识别芯片 ID，适用于开机自适配流程。


## 数据读写接口


```
bk_err_t bk_psram_memcpy(uint8_t *dst, uint8_t *src, uint32_t len);
bk_err_t bk_psram_memread(uint8_t *src, uint8_t *dst, uint32_t len);

```

描述：块状内存读写操作，性能优于 DTCM，可用于音视频缓存等场景。


## 低层读写（字节/半字/字）


```
void bk_psram_byte_write(uint8_t *addr, uint8_t val);
void bk_psram_half_word_write(uint16_t *addr, uint16_t val);
void bk_psram_word_write(uint32_t *addr, uint32_t val);
void bk_psram_word_memcpy(void *dst, void *src, uint32_t len);

```

描述：支持非对齐数据的写操作，内部处理地址对齐与遮罩操作。


## 字符串操作


```
char *bk_psram_strcat(char *start_addr, const char *data_buf);

```

描述：类似 strcat 的接口，将字符串追加写入 PSRAM。


## Heap 初始化标志


```
bool bk_psram_heap_init_flag_get(void);
bk_err_t bk_psram_heap_init_flag_set(bool init);

```

描述：用于标识 PSRAM heap 是否已初始化，适用于动态内存分配管理。


## 写透区域（Write Through Area）管理


```
psram_write_through_area_t bk_psram_alloc_write_through_channel(void);
bk_err_t bk_psram_free_write_through_channel(psram_write_through_area_t area);
bk_err_t bk_psram_enable_write_through(psram_write_through_area_t area, uint32_t start, uint32_t end);
bk_err_t bk_psram_disable_write_through(psram_write_through_area_t area);

```

描述：

- 写透区域适用于 DMA2D 高性能读写，不走 cache。

- 配置区域地址需 32 字节对齐，写入数据需为 32 字节整数倍。

- 每个区域仅允许一个主设备访问。


## 4 cli命令简介

demo运行依赖的宏配置：

| NAME | Description | File | value |
| --- | --- | --- | --- |
| CONFIG_PSRAM | support PSRAM | `middleware\soc\bk7236\bk7236.defconfig` | y |
| CONFIG_PSRAM_TEST | support PSRAM test command | `middleware\soc\bk7236\bk7236.defconfig` | y |

demo支持的命令如下表：

| Command | Param | Description |
| --- | --- | --- |
| psram_test start | cpu  cacheable: 0/1 delay_time: N | Test the read/write function of PSRAM. Options: Enable or disable cache. Number of loop delays. Cache base = 0x64000000 |
| psram_test stop | none | Stop test psram |
| psram_task_create | none | Create a task using PSRAM memory |
| psram_test start | dma cacheable: 0/1 delay_time: N | Use DMA copy instead of CPU Enable or disable cache Number of loop delays |
