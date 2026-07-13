# AP 侧 PSRAM (heap/data 段) L2 Cache 一致性使用说明


备注

本文针对 `ap/middleware/soc/bk7259_ap/mpu_cfg.c` 中把 AP 侧 PSRAM 的
`heap` 段与 `data` 段配置成 **L2 cacheable / L1 non-cacheable** (MPU attr 5)
的内存区，说明在多核 (CP0/CP1) 或其它硬件 master (DMA、WiFi/BT、外设) 也会
访问同一片内存时，必须由软件主动做 cache clean / invalidate 维护，否则会读到
旧数据或写丢数据。供团队同事开发和定位问题时参考。


## 1. 背景与适用范围

BK7259 采用 **AP + CP** 双 cluster 架构：

> - **AP cluster** = AP0 + AP1，共享一套 L1 (每核私有) + L2 (cluster 共享) cache 层级。
> - **CP cluster** = CP0 + CP1，是 **独立的** cache 层级，看不到 AP 的 L2。
> - **DMA / WiFi / BT / 各类外设 master** 直接访问 PSRAM 物理内存，**不经过** AP 的 L2。

AP 侧 PSRAM 的 MPU 划分 (以 non-interleave 路径为例，见 `mpu_cfg.c`)：

> | 区段 | MPU attr index | cache 属性 |
> | --- | --- | --- |
> | `0x6000_0000` ~ heap 之前 | attr 1 | L1/L2 都 **non-cacheable** |
> | heap + data (heap ~ code-0x20) | attr 5 | **L2 write-back / L1 non-cacheable** |
> | code section (code ~ 0x67FF…) | attr 3 | **L1 + L2 都 write-back cacheable** |

attr 定义见 `mpu_cfg.c` 的 `mpu_attrs[]`：


```
// attr 5: ARM_MPU_ATTR(0xf, 0x4)  Outer(L2)=write-back, Inner(L1)=non-cacheable
// attr 3: ARM_MPU_ATTR(0xf, 0xf)  Outer(L2)+Inner(L1) 都 write-back

```

重要


- **本文聚焦 attr 5 的 heap/data 段**：该区 L1 不缓存、L2 缓存。

- 这些 region 的 Shareability 都是 `ARM_MPU_SH_NON` (Non-shareable)，即硬件

  **不会** 在 AP cluster 之外维护一致性。跨 cluster / 跨 master 的一致性 **完全靠软件**。


## 2. 一致性模型：哪些自动保证、哪些必须手动维护


**自动保证 (无需软件干预)**

> - **AP0 与 AP1 之间**：heap/data 段 L1 non-cacheable，两个 AP 核的访问都直接落到
>   共享的 L2，L2 硬件天然保证 AP0/AP1 看到一致的数据。**这是 attr 5 的核心收益。**


**必须手动维护 (否则数据不一致)**

> 只要这片内存还会被下面任意一种”AP L2 之外的观察者”访问，就必须做 cache 维护：
>
> 1. **CP0 / CP1 访问** —— CP 是独立 cache 层级，看不到 AP L2 里尚未回写的脏数据，
>    也不知道自己写的数据 AP L2 里有旧副本。
> 2. **DMA / 硬件 master 访问** —— DMA、WiFi/BT、display、音视频等直接读写 PSRAM 物理内存，
>    绕过 AP L2。
> 3. (相关) **code section (attr 3) 的自修改 / 动态加载** —— 涉及 L1 D-cache、L2、I-cache
>    多级，见第 6 节。


## 3. 黄金规则

把”谁最后写、谁接下来读”想清楚，套用两条规则即可：

> - **生产者写完 → CLEAN (回写)**：AP 写完数据、在通知 CP / 启动 DMA **之前**，
>   必须 `clean` 把 AP L2 里的脏数据回写到 PSRAM 物理内存。
> - **消费者读前 → INVALIDATE (作废)**：CP / DMA 写完数据后，AP 在读取 **之前**，
>   必须 `invalidate` 作废 AP L2 里可能存在的旧副本，强制从 PSRAM 重新取。

时序示意（AP 生产、CP 消费）：


```
AP:   写 buffer  ->  cache clean(buffer)  ->  __DSB()  ->  发 IPI/mailbox 通知 CP
CP:                                              收到通知  ->  读 buffer (得到新数据)

```

时序示意（CP 生产、AP 消费）：


```
CP:   写 buffer  ->  (CP 侧回写)  ->  发 IPI/mailbox 通知 AP
AP:                                       收到通知 -> cache invalidate(buffer) -> 读 buffer

```

时序示意（AP 与 DMA）：


```
DMA 发送(内存->外设): AP 填好 buffer -> clean(buffer) -> __DSB() -> 启动 DMA
DMA 接收(外设->内存): AP 启动 DMA -> ... DMA 完成中断 -> invalidate(buffer) -> AP 读

```

小技巧

上面时序里的 `clean(buffer)` / `invalidate(buffer)` 既可以用第 4.2 节按方向细分的
`cache_clean_range` / `cache_invalidate_range`，**也可以直接用第 4.1 节的
``flush_dcache(buffer, len)`` 一行替代** —— 它一次性 clean+invalidate L1+L2，
生产者、消费者两个方向都覆盖，最省心(代价是开销略大)。

备注


**关于时序里的 ``__DSB()``**：自 `[Jira BK7259SW-1120]` 起，按范围/全量的 L2 维护
(`flush_dcache` / `cache_*_range` / `cache_*_all` / `l2_cache_maintain_*`)
在写完 `CACHE_SYNC` 后**内部已执行 `__DSB()` + ``` __ISB()``**。因此上图中的 ``__DSB() ```
已由这些接口内置，**上层调用后无需再手动补屏障**。（旧 SDK 若不含该修复，则仍需在
clean 之后、通知其它 master 之前自行 `__DSB()`。）


## 4. API 速查表

刷 cache 有两层接口，**都已经同时维护 L1 + L2**，按使用习惯任选其一即可。


### 4.1 一行搞定的封装 (`cache.h`)

`ap/middleware/arch/cortex-m/include/cache.h` 提供的 `flush_dcache` / `flush_all_dcache`
是最简单的入口。**当 ``CONFIG_L2_CACHE_ENABLE`` 打开时 (本平台默认打开)，它们会一次性
clean + invalidate L1 和 L2**，所以”刷 cache 只调用 `flush_dcache` / `flush_all_dcache` 就够了”，
对绝大多数场景成立。

> | 封装 | 等价行为 (L2 使能时) |
> | --- | --- |
> | `flush_dcache(va, size)` | `arch_dcache_flush_and_invd_range` → `cache_clean_invalidate_range` (L1+L2 clean&invalidate 指定范围) |
> | `flush_all_dcache()` | `arch_dcache_flush_and_invd_all` → `cache_clean_invalidate_all` (L1+L2 clean&invalidate 全部) |

重要


- `flush_dcache` / `flush_all_dcache` 做的是 **clean + invalidate (回写并作废)**，
  生产者(只需 clean)和消费者(只需 invalidate)两种方向都能正确覆盖，是”最省心”的选择。
  代价是每次都多做一遍 invalidate/clean，开销略大；对性能敏感的热路径可改用 4.2 的细分接口。

- 这套封装只有在 `CONFIG_L2_CACHE_ENABLE` 打开时才会维护 L2；若该宏未定义，它们只刷 L1
  (`SCB_*`)，对本文的 L2-cacheable 区 **无效**。本平台该宏默认打开，可放心使用。

- `flush_all_dcache()` 是按 way 全量遍历，开销大，建议仅用于粗粒度同步 / 调试兜底，
  正常路径请用按范围的 `flush_dcache`。


```
#include "cache.h"

/* 生产者 / 消费者通用：交给 CP/DMA 前、或从 CP/DMA 取回后，对 buffer 刷一次。
   内部已含尾部 __DSB()/__ISB()，刷完即可直接通知对端 / 启动 DMA，无需再补屏障 */
flush_dcache(psram_buf, len);   /* L1+L2 clean & invalidate (+ DSB/ISB) */

```


### 4.2 可分别 clean / invalidate 的细分接口 (`l2_cache.h`)

需要按方向精确控制(只 clean 或只 invalidate)以降低开销时，用
`ap/middleware/arch/cortex-m/l2_cache.h`：

> | 操作 | API |
> | --- | --- |
> | 生产者回写 (clean) | `cache_clean_range(CACHE_TYPE_DCACHE, L2C_OP_CLEAN, addr, size)` |
> | 消费者作废 (invalidate) | `cache_invalidate_range(CACHE_TYPE_DCACHE, L2C_OP_INVALID, addr, size)` |
> | 回写并作废 (clean+invalidate) | `cache_clean_invalidate_range(CACHE_TYPE_DCACHE, L2C_OP_CLEAN_INVALID, addr, size)` |
> | 仅维护 L2 (attr 5 区最小开销可选) | `l2_cache_maintain_range(L2C_OP_CLEAN/INVALID/CLEAN_INVALID, start, end)` |

备注


- `cache_*_range` 内部先做 L1 (`SCB_*DCache_by_Addr`) 再做 L2。对 attr 5 的
  heap/data 段，L1 部分实际无副本、等于空操作，主要生效的是 L2。

- 4.1 的 `flush_dcache` 本质就是 `cache_clean_invalidate_range`，两套接口最终走同一路径。

- 自 `[Jira BK7259SW-1120]` 起，`cache_*_range` / `l2_cache_maintain_range` 在维护完成后

  **内部已带 ``__DSB()`` + ``__ISB()``**，调用后无需再手动补屏障。

- 对 **attr 3 的 code 段** (L1+L2 都缓存)，必须用组合接口，不能只维护 L2。

- 单纯只想动 L2 时，可直接调用 `l2_cache_maintain_range` 省一次 L1 遍历。

代码示例：


```
#include "l2_cache.h"

/* 生产者：AP 写完，准备交给 CP / DMA */
memcpy(psram_buf, src, len);
cache_clean_range(CACHE_TYPE_DCACHE, L2C_OP_CLEAN, (uint32_t)psram_buf, len);
/* 内部已含尾部 __DSB()，可直接通知；也可用 flush_dcache(psram_buf, len) 一行替代上面这句 */
notify_cp_or_start_dma(psram_buf, len);

```


```
/* 消费者：CP / DMA 写完，AP 读之前 */
cache_invalidate_range(CACHE_TYPE_DCACHE, L2C_OP_INVALID, (uint32_t)psram_buf, len);
/* 也可直接用 flush_dcache(psram_buf, len); 一行替代上面这句 */
process(psram_buf, len);

```

获取 heap/data/code 段实际地址区间，便于校验地址落在哪个 attr 区
(见 `ap/middleware/soc/bk7259_ap/memory.h`)：


```
bk_dump_mem_info_t info;
bk_get_psram_heap_info(&info);   /* heap 段起止 */
bk_get_psram_data_info(&info);   /* data 段起止 */
bk_get_psram_bss_info(&info);
bk_check_addr_in_code_section(addr);  /* 判断是否落在 attr 3 code 段 */

```


## 5. 对齐要求与典型陷阱

重要


**L2 cache line = 32 字节** (`L2C_CACHE_LINE_SIZE`)，L1 D-cache line 同为 32 字节。
`invalidate` 是 **破坏性** 操作，会丢弃整条 cache line。

> - **buffer 起始地址必须 32 字节对齐，长度建议向上补齐到 32 字节的整数倍。**
>   否则 `invalidate` 时与该 buffer 共享首/尾 cache line 的相邻变量会被一起作废，
>   造成相邻数据被旧值覆盖（极难定位的随机踩内存）。
>
>   ```
>   __attribute__((aligned(32))) static uint8_t dma_buf[ROUND_UP(N, 32)];
>   ```
> - `l2_cache_maintain_range` 会把 `start_addr` 向下对齐到 line，但 **不会** 处理
>   `end_addr` 的尾部不对齐；尾部 buffer 与他人共享一条 line 时同样有风险。
> - **屏障**：自 `[Jira BK7259SW-1120]` 起，`l2_cache_maintain_range` 在写完 `CACHE_SYNC`
>   后已补 `__DSB()` + `__ISB()` (与 `l2_cache_maintain_all` 一致)，因此
>   `flush_dcache` / `cache_*_range` 调用返回时回写已完成并对外可见，**上层无需再手动 ``__DSB()``**。
>   若使用不含该修复的旧 SDK，则仍须在 clean 之后、通知其它 master 之前自行 `__DSB()`。
> - **顺序不能错**：生产者必须”先 clean，再通知”；消费者必须”先 invalidate，再读”。
>   顺序颠倒会读到旧数据。
> - **并发/抢占**：对同一 buffer 的 clean/invalidate 与对该 buffer 的写不要被其它核/中断
>   穿插。若 invalidate 之后、读取之前 AP 又写了该 region，会再次进入 L2，需要重新维护。
> - **避免 false sharing**：不同 master 各自的 buffer 不要落在同一条 32B line 上。


## 6. code section (attr 3) 自修改 / 动态加载补充

code 段是 L1+L2 都缓存。若运行期改写了该区的指令 (overlay、动态加载、热补丁)，
需要：先 `clean` D-cache (把新指令从 D-cache 回写到 L2/PSRAM)，再 `invalidate` I-cache，
最后 `__DSB()` + `__ISB()`：


```
cache_clean_range(CACHE_TYPE_DCACHE, L2C_OP_CLEAN, (uint32_t)code_addr, len);
l1_cache_invalidate_range(CACHE_TYPE_ICACHE, (uint32_t)code_addr, len);
__DSB();
__ISB();

```


## 7. 问题排查指引

> | 症状 | 排查方向 |
> | --- | --- |
> | CP / DMA 读到旧数据、字段为 0 或上一帧值 | AP 生产者写完 **漏了 clean**，或 clean 后没有 `__DSB()` 就通知 |
> | AP 读到旧数据 (CP/DMA 已更新) | AP 消费者读前 **漏了 invalidate** |
> | 相邻无关变量被随机改写 / 偶发踩内存 | buffer **未 32B 对齐** 或长度未补齐，invalidate 误伤相邻 line |
> | 偶发、与时序/负载相关、加打印就消失 | 典型 cache 一致性竞态：确认 clean/invalidate 与通知/读取的先后顺序 |
> | 自修改代码后跑飞 / 执行旧指令 | code 段改写后漏了 D-cache clean + I-cache invalidate + ISB |

定位手段：

> - 用 `bk_get_psram_heap_info` / `bk_get_psram_data_info` / `bk_check_addr_in_code_section`
>   确认出问题的地址到底落在 attr 5 还是 attr 3 区，判断需要哪种维护。
> - 临时验证：在可疑读取前后强制 `cache_invalidate_range`，若问题消失，基本可锁定为缺维护。
> - 检查 buffer 定义是否 `aligned(32)`、size 是否补齐。


## 8. 开发自检清单

下面任一条涉及到 attr 5 的 heap/data buffer 与 CP / DMA / 其它 master 交互时，逐条对照：

> - [ ] 跨 cluster / 跨 master 共享的 PSRAM buffer **32 字节对齐**，长度补齐到 32 的倍数。
> - [ ] AP 作为生产者：写完数据 → `flush_dcache` / `cache_clean_range` (内部已含 `__DSB()`) → 再通知 / 启动 DMA。
> - [ ] AP 作为消费者：被通知 / DMA 完成 → `flush_dcache` / `cache_invalidate_range` → 再读数据。
> - [ ] 不同 master 的 buffer 没有共享同一条 32B cache line (无 false sharing)。
> - [ ] 维护范围 (addr, size) 覆盖了实际读写的全部字节。
> - [ ] code 段被改写时做了 D-cache clean + I-cache invalidate + `__DSB()`/`__ISB()`。
> - [ ] 纯 AP0/AP1 之间共享、且不涉及 CP/DMA 的 buffer：可依赖 L2 硬件一致性，无需手动维护。


## 参考代码

> - MPU 配置：`ap/middleware/soc/bk7259_ap/mpu_cfg.c`
> - Cache 维护 API：`ap/middleware/arch/cortex-m/l2_cache.h` / `l2_cache.c`
> - PSRAM 段信息查询：`ap/middleware/soc/bk7259_ap/memory.h` / `memory.c`
