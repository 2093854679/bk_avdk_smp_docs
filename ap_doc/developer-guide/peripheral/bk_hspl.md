---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_hspl.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="hspl"></a>

# HSPL 使用指南

<a id="id1"></a>

## 概述

HSPL（Hardware Spin Lock）是 BK7259 芯片提供的硬件自旋锁机制，用于 4 核（CPU0/CPU1 与 CPU2/CPU3）之间的互斥同步。
芯片提供两个 HSPL 硬件块，每个实例 16 个独立通道，可实现高效的跨核互斥访问。

主要特性：

> - 双实例支持：两个 HSPL 硬件块，基地址不同
> - 16 通道：每个实例支持 16 个独立通道
> - 硬件原子操作：基于硬件实现的原子加锁/解锁
> - 资源级抽象：提供 `bk_hspl_res_*` 封装，将逻辑资源映射到实例与通道

<a id="id2"></a>

## 硬件架构

<a id="id3"></a>

### HSPL 实例映射

> - BK\_HSPL\_ID\_0：实例 0，基址 0x45010000，CP 侧映射，用于 CP/AP 跨核互斥
> - BK\_HSPL\_ID\_1：实例 1，基址 0x480C0000，AP 侧映射，用于 AP SMP 内部互斥

实例分工与中断归属：

> - `BK_HSPL_ID_0`：用于 CP 与 AP 之间 4 个 CPU 的资源互斥，HSPL 超时中断由 CP 侧处理
> - `BK_HSPL_ID_1`：用于 AP 侧 SMP（CPU2/CPU3）内部资源互斥，HSPL 超时中断由 AP 侧处理

备注

AP 侧跨核共享资源建议使用 BK\_HSPL\_ID\_0；AP SMP（CPU2/CPU3）内部互斥建议使用 BK\_HSPL\_ID\_1。
CP 侧资源锁接口限制使用 BK\_HSPL\_ID\_0，在 CP 上调用 BK\_HSPL\_ID\_1 相关路径会返回 `BK_ERR_NOT_SUPPORT`。

<a id="id4"></a>

### 寄存器说明

每个通道占用两个寄存器：

> - LOCK\[ch\]：读写寄存器，实现硬件自旋锁
>   \- 读操作（尝试加锁）：返回 0x1 表示加锁成功；返回 6’b1xxxx0 表示已被锁定，xxxx 为 owner core\_id
>   \- 写操作（释放锁）：写入 0xA55A80AF 释放锁
> - STA\[ch\]：只读辅助寄存器，不改变锁状态，便于调试

<a id="id5"></a>

## 驱动初始化

在应用初始化阶段调用 `bk_hspl_driver_init()`；可选注册超时回调用于调试。

```
#include "hspl_driver.h"

void app_init(void)
{
    bk_err_t ret;

    ret = bk_hspl_driver_init();
    if (ret != BK_OK) {
        BK_LOGE("HSPL driver init failed: %d\r\n", ret);
        return;
    }

    /* 可选：注册超时回调 */
    bk_hspl_register_timeout_callback(BK_HSPL_ID_0,
                                      hspl_timeout_cb,
                                      NULL);
}
```

反初始化（如需要）：

```
bk_hspl_driver_deinit();
```

<a id="api"></a>

## 底层 API 使用

底层 API 直接操作 HSPL 实例和通道，适合需要精确控制的场景。头文件：`middleware/driver/hspl/hspl_driver.h`。

<a id="id6"></a>

### 尝试加锁与释放

```
uint8_t owner_id = 0xFF;
bk_err_t ret = bk_hspl_try_lock(BK_HSPL_ID_0, 0, &owner_id);

if (ret == BK_OK) {
    /* 临界区 */
    bk_hspl_unlock(BK_HSPL_ID_0, 0);
} else if (owner_id != 0xFF) {
    BK_LOGI("Locked by core %u\r\n", owner_id);
}
```

<a id="id7"></a>

### 查询锁状态

```
hspl_state_t state = {0};
if (bk_hspl_get_state(BK_HSPL_ID_0, 0, &state) == BK_OK) {
    if (state.locked) {
        BK_LOGI("ch0 locked by core %u\r\n", state.owner_id);
    }
}
```

<a id="id8"></a>

## 资源级 API 使用

资源级 API 将逻辑资源（如 FLASH、CLOCK）映射到具体的 HSPL 实例和通道。头文件：`middleware/driver/hspl/hspl_res_lock.h`。

<a id="id9"></a>

### 常用资源类型

BK\_HSPL\_ID\_0（资源 0-15，CP/AP 共享）：

> - `BK_HSPL_RES_FLASH`、`BK_HSPL_RES_CLOCK`、`BK_HSPL_RES_POWER`、`BK_HSPL_RES_SYS`
> - `BK_HSPL_RES_RTC`、`BK_HSPL_RES_ANA`、`BK_HSPL_RES_FUSE`、`BK_HSPL_RES_TRNG`
> - `BK_HSPL_RES_WDT`、`BK_HSPL_RES_SPI`、`BK_HSPL_RES_GPIO`、`BK_HSPL_RES_PWM`
> - `BK_HSPL_RES_ADC`、`BK_HSPL_RES_DAC`、`BK_HSPL_RES_PMU`、`BK_HSPL_RES_PSRAM`

BK\_HSPL\_ID\_1（资源 16-31，仅 AP SMP）：

> - `BK_HSPL_RES_OS`、`BK_HSPL_RES_LVGL`、`BK_HSPL_RES_AUDIO`、`BK_HSPL_RES_VIDEO`
> - `BK_HSPL_RES_GPU`、`BK_HSPL_RES_NPU`、`BK_HSPL_RES_DSP`、`BK_HSPL_RES_ISP`
> - `BK_HSPL_RES_VDEC`、`BK_HSPL_RES_VENC`、`BK_HSPL_RES_SDIO`、`BK_HSPL_RES_USB`
> - `BK_HSPL_RES_PSRAM`、`BK_HSPL_RES_USER2`

资源映射规则：资源 ID 0-15 映射到 BK\_HSPL\_ID\_0 通道 0-15；资源 ID 16-31 映射到 BK\_HSPL\_ID\_1 通道 0-15。映射固定，无需手动配置。

<a id="id10"></a>

### 加锁与解锁

带超时加锁：

```
if (bk_hspl_res_lock(BK_HSPL_RES_FLASH, 1000) == BK_OK) {
    /* Flash 操作 */
    bk_hspl_res_unlock(BK_HSPL_RES_FLASH);
}
```

立即尝试（无等待）：

```
bk_hspl_res_try_lock(BK_HSPL_RES_FLASH);
/* 或 bk_hspl_res_lock(BK_HSPL_RES_FLASH, 0) */
```

IRQ-safe 包装（本地关中断，仅 try-lock 一次）：

```
uint32_t flags;
if (bk_hspl_res_lock_irqsave(BK_HSPL_RES_FLASH, &flags) == BK_OK) {
    /* 临界区，本地中断已关闭 */
    bk_hspl_res_unlock_irqrestore(BK_HSPL_RES_FLASH, flags);
}
```

永久等待（仅任务上下文，ISR 禁止）：

```
if (bk_hspl_res_lock(BK_HSPL_RES_FLASH, BK_HSPL_WAIT_FOREVER) == BK_OK) {
    /* 临界区 */
    bk_hspl_res_unlock(BK_HSPL_RES_FLASH);
}
```

<a id="flash"></a>

### 完整示例：Flash 写保护

```
#include "hspl_res_lock.h"

void safe_flash_write(uint32_t addr, const void *data, size_t len)
{
    if (bk_hspl_res_lock(BK_HSPL_RES_FLASH, 1000) != BK_OK) {
        BK_LOGE("Failed to acquire FLASH lock\r\n");
        return;
    }

    flash_write_internal(addr, data, len);
    bk_hspl_res_unlock(BK_HSPL_RES_FLASH);
}
```

<a id="id11"></a>

## 配置说明

Kconfig 配置项（`middleware/driver/hspl/Kconfig`）：

> - `CONFIG_HSPL=y`：启用 HSPL 驱动
> - `CONFIG_HSPL_TEST=y`：启用 HSPL 测试功能（可选）
> - `CONFIG_AON_RTC=y`：使用 AON RTC 作为超时基准（可选；未开启时回退为 rtos\_get\_time）

启用 `CONFIG_HSPL` 后自动编译 `hspl_driver.c` 与 `hspl_res_lock.c`。

<a id="id12"></a>

## 使用规范与注意事项

<a id="id13"></a>

### 使用规范（建议）

> - 避免默认无限等待：优先使用有限超时或 bk\_hspl\_res\_try\_lock，仅在明确场景使用 BK\_HSPL\_WAIT\_FOREVER
> - ISR 中不可阻塞：中断上下文只允许 try-lock
> - 同核 ISR/任务复用同一锁：任务侧取锁前建议本地关中断，并保证临界区尽量短
> - 长临界区不要关中断：避免中断延迟过大；此时应保证 ISR 不使用同一锁

<a id="id14"></a>

### 锁的持有与死锁预防

> - 锁持有时间尽量短，避免在持有锁期间执行阻塞操作
> - 多通道加锁时，所有核心按相同顺序加锁
> - 尽量避免在持有锁的情况下再次获取锁
> - 始终检查 API 返回值，确保异常路径也能正确释放锁

<a id="id15"></a>

## 测试与验证

<a id="id16"></a>

### 测试环境准备

启用以下配置后可通过 CLI 进行功能与压力测试：

> - `CONFIG_HSPL=y`、`CONFIG_HSPL_TEST=y`
> - `CONFIG_CLI=y`、`CONFIG_DRIVER_TEST=y`

测试前初始化驱动（压力测试还需 IPI）：

```
hspl_driver init
ipi_driver init
```

<a id="cli"></a>

### 常用 CLI 命令

底层锁操作：

```
hspl lock 0 0          # 实例 0 通道 0 加锁
hspl unlock 0 0        # 释放锁
hspl state 0 all       # 查询实例 0 所有通道状态
```

资源级锁操作：

```
hspl res_lock flash 1000
hspl res_unlock flash
hspl res_lock os 2000
```

<a id="id17"></a>

### 自动化压力测试（推荐）

在 CPU0 上执行，自动在 CP CPU0 与 AP CPU2 上并行竞争同一通道：

```
hspl stress_auto 0 0 10000 2
hspl stress_stat       # 查看统计
hspl stress_stop       # 停止测试
```

参数依次为：hspl\_id、通道号、每核迭代次数、每次持有锁时间（ms）。

结果验证要点：

> - `lock_success + lock_fail = iter`
> - `unlock_success = lock_success`，`unlock_fail = 0`
> - 两核测试时间接近，成功率在激烈竞争下通常约 30-50%

<a id="id18"></a>

### 典型测试用例

1. 基本功能：`hspl lock 0 0` → `hspl state 0 0` → `hspl unlock 0 0`
2. 资源级 API：`hspl res_lock flash 1000` → `hspl res_unlock flash`
3. 多核竞争：`hspl stress_auto 0 0 10000 2`，分别在 CPU0/CPU2 查看 `hspl stress_stat`
4. 多通道独立：通道 0 加锁后，通道 1 仍可独立加锁

<a id="id19"></a>

### 故障排查

> - 命令未找到（`$cmd NOT found: hspl`）：检查 `CONFIG_HSPL_TEST=y` 并重新编译
> - Invalid hspl\_id：hspl\_id 仅支持 0 或 1，通道号 0-15
> - 压力测试无法启动另一 CPU：执行 `ipi_driver init`，检查 IPI 配置
> - 锁操作全部失败：确认已执行 `hspl_driver init`，参数合法

<a id="id20"></a>

## 相关代码路径

> - 驱动头文件：`middleware/driver/hspl/hspl_driver.h`、`hspl_res_lock.h`
> - 驱动实现：`middleware/driver/hspl/hspl_driver.c`、`hspl_res_lock.c`
> - 测试代码：`middleware/driver/hspl/hspl_test.c`
> - 详细文档：`middleware/driver/hspl/HSPL_USER_GUIDE.md`、`HSPL_TEST_GUIDE.md`

<a id="id21"></a>

## API 参考

详见 [HSPL](../../api-reference/peripheral/bk_hspl.md)。
