# FLASH



## 1 功能概述


- FLASH相关的理论介绍参考: [FLASH的驱动](../../developer-guide/peripheral/bk_flash.md "../../developer-guide/peripheral/bk_flash.md")

备注


- 默认FLASH 在CP和AP侧都会使能。


## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_flash_test.c`
> - 驱动源码路径：
>   :   `middleware\driver\flash\flash_driver.c`
>
>       `middleware\driver\flash\flash_driver_ext.c`
>
>       `middleware\driver\flash\flash_server.c`
>
>       `middleware\driver\flash\flash_client.c`

备注


- 1.flash_driver.c :FLASH驱动实现代码
  :   - 2.cli_flash_test.c:FLASH功能测试命令实现

- 3.flash_server.c:FLASH基于CP+AP框架下的CP的操作实现

- 4.flash_client.c:FLASH基于CP+AP框架下的AP的操作实现


## 3 FLASH 关键数据结构说明


```
typedef struct {
    uint32_t flash_id;
    uint32_t flash_size;
    uint8_t status_reg_size;
    flash_line_mode_t line_mode;
    uint8_t cmp_post;
    uint8_t protect_post;
    uint8_t protect_mask;
    uint16_t protect_all;
    uint16_t protect_none;
    uint16_t unprotect_last_block;
    uint8_t quad_en_post;
    uint8_t quad_en_val;
    uint8_t coutinuous_read_mode_bits_val;
} flash_config_t;

```


```
flash_config_t 定义的 flash_config[] 数组存放了目前所支持的 flash vendor 的参数：

- flash_id: Flash 的 ID 信息

- flash_size: Flash 支持的地址空间大小

- status_reg_size: 状态寄存器字节数

- line_mode: Flash 的线模式（2线/4线）

- cmp_post / protect_post / protect_mask: 状态寄存器保护位设置

- quad_en_post / quad_en_val: 四线使能位配置

- coutinuous_read_mode_bits_val: 持续读模式设置值

```


```
typedef struct {
    flash_hal_t hal;
    uint32_t flash_id;
    uint32_t flash_status_reg_val;
    uint32_t flash_line_mode;
    const flash_config_t *flash_cfg;
} flash_driver_t;

```


```
flash_config_t 定义的 flash_config[] 数组存放了目前所支持的 flash vendor 的参数：

- flash_id: Flash 的 ID 信息

- flash_size: Flash 支持的地址空间大小

- status_reg_size: 状态寄存器字节数

- line_mode: Flash 的线模式（2线/4线）

- cmp_post / protect_post / protect_mask: 状态寄存器保护位设置

- quad_en_post / quad_en_val: 四线使能位配置

- coutinuous_read_mode_bits_val: 持续读模式设置值

```


```
typedef enum {
    FLASH_LINE_MODE_TWO = 2,
    FLASH_LINE_MODE_FOUR = 4
} flash_line_mode_t;

```


```
typedef enum {
    FLASH_PROTECT_NONE = 0,
    FLASH_PROTECT_ALL,
    FLASH_PROTECT_HALF,
    FLASH_UNPROTECT_LAST_BLOCK
} flash_protect_type_t;

```


```
flash_protect_type_t 定义了 FLASH 中的保护区域方式：

- FLASH_PROTECT_NONE  --  不保护

- FLASH_PROTECT_ALL   --  全保护

- FLASH_PROTECT_HALF  --  半保护

- FLASH_UNPROTECT_LAST_BLOCK  -- 不保护最后 block 区域

```


## 4 FLASH 主要函数列表


### 初始化与反初始化


```
bk_err_t bk_flash_driver_init(void);

```

描述：初始化 Flash 驱动，分配控制内存。


```
bk_err_t bk_flash_driver_deinit(void);

```

描述：反初始化 Flash 驱动，释放资源。


### 基本控制接口


```
flash_line_mode_t bk_flash_get_line_mode(void);

```

描述：获取当前 Flash 传输线模式。


```
uint8_t bk_flash_get_coutinuous_read_mode(void);

```

描述：获取当前连续读模式状态。


```
uint32_t bk_flash_get_id(void);

```

描述：获取 Flash 芯片 ID。


```
bool bk_flash_is_driver_inited(void);

```

描述：检查 Flash 驱动是否已初始化。


### Flash 保护功能


```
bk_err_t bk_flash_set_protect_type(flash_protect_type_t type);
flash_protect_type_t bk_flash_get_protect_type(void);

```

描述：设置/获取 Flash 保护类型。


```
bk_err_t bk_flash_write_enable(void);
bk_err_t bk_flash_write_disable(void);

```

描述：启用或禁用 Flash 写操作。


```
uint16_t bk_flash_read_status_reg(void);
bk_err_t bk_flash_write_status_reg(uint16_t status_reg_data);

```

描述：读/写 Flash 状态寄存器。


### 擦除接口


```
bk_err_t bk_flash_erase_sector(uint32_t address);
bk_err_t bk_flash_erase_block(uint32_t address);
bk_err_t bk_flash_erase_fast(uint32_t erase_off, uint32_t len);

```

描述：按扇区（4K）或块（64K）擦除 Flash，也支持自动选择大小的快速擦除。


### 读写接口


```
bk_err_t bk_flash_write_bytes(uint32_t address, const uint8_t *user_buf, uint32_t size);
bk_err_t bk_flash_read_bytes(uint32_t address, uint8_t *user_buf, uint32_t size);
bk_err_t bk_flash_read_word(uint32_t address, uint32_t *user_buf, uint32_t size);

```

描述：读写 Flash 的字节或字方式数据，word读需 4 字节对齐。


### 低功耗接口


```
bk_err_t bk_flash_enter_deep_sleep(void);
bk_err_t bk_flash_exit_deep_sleep(void);

```

描述：进入/退出 Flash 深度休眠状态。


### 功耗回调与速度调节


```
bk_err_t bk_flash_register_ps_suspend_callback(flash_ps_callback_t cb);
bk_err_t bk_flash_register_ps_resume_callback(flash_ps_callback_t cb);

```

描述：注册 Flash 电源管理 suspend/resume 回调函数。


```
bk_err_t bk_flash_clk_switch(uint32_t speed_type, uint32_t modules);

```

描述：根据模块动态切换 Flash 时钟频率。


### 操作状态管理


```
bk_err_t bk_flash_set_operate_status(flash_op_status_t status);
flash_op_status_t bk_flash_get_operate_status(void);

```

描述：设置/获取 Flash 当前操作状态。


### 等待与异步通知接口


```
bk_err_t bk_flash_register_wait_cb(flash_wait_callback_t wait_cb);
bk_err_t bk_flash_unregister_wait_cb(flash_wait_callback_t wait_cb);

```

描述：注册/注销 Flash 操作等待回调，用于在 Flash 正忙时执行替代逻辑（如回调应放入 ITCM 中）。


### 其他接口


```
uint32_t bk_flash_get_current_total_size(void);

```

描述： 获取当前 Flash 总容量（单位 Byte）。


## 5 cli命令简介

demo运行依赖的宏配置：

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG_FLASH | support FLASH | `middleware\soc\bk7236\bk7236.defconfig` | y |
> | CONFIG_FLASH_TEST | support FLASH test command | `middleware\soc\bk7236\bk7236.defconfig` | y |

demo支持的命令如下表：

| Command | Param | Description |
| --- | --- | --- |
| flash_test R | test start address (hex) | Read the data from the address starting with the start address to the length of the size and print, e.g.: flash_test R 0x7fe000 0x100 |
| test size (hex) |
| flash_test W | test start address (hex) | Write data from the address of the start address to the length of the size, the data is looped from 0 to 0xFF every 256 bytes, e.g.: flash_test W 0x7fe000 0x100 |
| test size (hex) |
| flash_test E | test start address (hex) | Erase the data from the address starting from the start address to the size of the data, and the data after erasure is all 0xFF, eg: flash_test E 0x7fe000 0x100 |
| test size (hex) |
| flash_test C | test start address (hex) | Test the read/write/erase function from the address starting from the start address to the length of size and count the time, and print the statistical time print_cnt every interval in us, eg: flash_test C 0x7fe000 0x1000 100 |
| test size (hex) |
| print interval |
| flash_test P | none | Flash unlocks all areas |
| flash_test U | none | Flash unlocks the last block area |
| flash_test RSR | none | Read the status register value |
| flash_test WSR | status register data | Write status register values |
| fmap_test | none | Print partition information |


## 6 FLASH 示例代码

以下示例函数展示了 Flash 的擦除、写入与读取流程，适用于开发中快速验证 Flash 功能。


**函数：** test_flash_erase


```
static bk_err_t test_flash_erase(volatile uint32_t start_addr, uint32_t len)
{
    uint32_t addr = start_addr;
    uint32_t tmp = addr + len;

    for (; addr < tmp; addr += 0x1000) {
        bk_flash_erase_sector(addr);
    }
    return kNoErr;
}

```

说明：

- 每次以 4KB 扇区为单位调用 bk_flash_erase_sector 进行擦除。


- start_addr 应该是 4KB 对齐地址。

- 擦除范围为 [start_addr, start_addr + len)。

- 建议在写入 Flash 前调用此函数以避免数据写入失败。


**函数：** test_flash_write


```
static bk_err_t test_flash_write(volatile uint32_t start_addr, uint32_t len)
{
    uint32_t i;
    u8 buf[256];
    uint32_t addr = start_addr;
    uint32_t tmp = addr + len;

    for (i = 0; i < 256; i++)
        buf[i] = i;

    for (; addr < tmp; addr += 256) {
        bk_flash_write_bytes(addr, (uint8_t *)buf, 256);
    }

    return kNoErr;
}

```


**说明：**

- 每次写入 256 字节固定数据，数据内容为 0x00 到 0xFF 依次递增。


- 起始地址 start_addr 可为任意有效地址，长度 len 建议为 256 的倍数。

- 写入前应确保目标区域已擦除（通过 test_flash_erase 函数）。


**函数：** test_flash_read_print


```
static bk_err_t test_flash_read_print(volatile uint32_t start_addr, uint32_t len)
{
    uint32_t tmp;
    u8 buf[256];
    uint32_t addr = start_addr;
    tmp = addr + len;

    for (; addr < tmp; addr += 256) {
        os_memset(buf, 0, 256);
        bk_flash_read_bytes(addr, (uint8_t *)buf, 256);
    }

    return kNoErr;
}

```

说明：


- 读取 Flash 中的数据，每次读取 256 字节，存入临时缓冲区 buf。

- 本函数未打印读取内容，仅用于读操作验证或做性能测试。

- 可配合 test_flash_write 使用，确认写入后数据是否可正确读取。
