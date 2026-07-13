# HPDMA



## 1 功能概述

HPDMA demo 通过 CLI 命令验证 HPDMA driver 的基础通道控制、memory copy、链表传输、2D stride 传输、多通道并发、吞吐测试、长时间压测以及负向参数测试。

> - HPDMA 功能具体描述参考：[HPDMA 使用指南](../../developer-guide/peripheral/bk_hpdma.md "../../developer-guide/peripheral/bk_hpdma.md")
> - 本文所有命令均为 AP 侧命令，命令前使用 `ap_cmd`。
> - 地址参数使用 16 进制，不需要 `0x` 前缀。
> - 长度、size、count、id 参数使用 10 进制。


## 2 代码路径

> - demo 路径：
>   :   `ap/middleware/driver/hp_dma/hpdma_test.c`
> - 驱动源码路径：
>   :   `ap/middleware/driver/hp_dma/hpdma_driver.c`
> - API 头文件路径：
>   :   `ap/include/driver/hpdma.h`
>
>       `ap/include/driver/hal/hal_hpdma_types.h`


## 3 HPDMA 相关宏配置

| NAME | Description | File | value |
| --- | --- | --- | --- |
| `CONFIG_DRV_CLI_SUPPORT` | 驱动 CLI 命令注册支持 | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | y |
| `CONFIG_SUPPORT_CACHEABLE_SRAM` | Cacheable SRAM 支持 | `middleware/soc/bk7259_ap/bk7259_ap.defconfig` | 依项目 |

备注

HPDMA demo 是否被编译还取决于工程的 driver test/CLI 配置。若 `ap_cmd hpdma help` 无响应，请先确认当前工程已使能 driver CLI。


## 4 demo 命令总览

> | Command | Param | Description |
> | --- | --- | --- |
> | `hpdma help` | 无 | 打印 HPDMA 命令帮助 |
> | `hpdma driver {init|deinit}` | `init/deinit` | 初始化或反初始化 HPDMA driver |
> | `hpdma chnl alloc` | 无 | 申请一个 HPDMA 通道 |
> | `hpdma chnl_free {free|force} {id}` | `id` 为 10 进制通道号 | 释放或强制回收通道 |
> | `hpdma chan {id} {init|start|stop|deinit}` | `id` 为 10 进制通道号 | 验证普通通道 init/start/stop/deinit 流程 |
> | `hpdma int {id} {op}` | `op` 为中断注册/使能/关闭操作 | 验证中断 API |
> | `hpdma copy {src_hex} {dst_hex} {len_dec}` | 地址为 16 进制，长度为 10 进制 | 使用 HPDMA 做 memory copy |
> | `hpdma link_test_1d {cnt} {len}` | `cnt/len` 为 10 进制 | 1D 链表传输测试 |
> | `hpdma link_test_2d {cnt} {x} {y} {step}` | 参数均为 10 进制 | 2D stride 链表传输测试 |
> | `hpdma concurrent_test {chan_cnt} {len}` | 参数均为 10 进制 | 多通道并发单轮传输测试 |
> | `hpdma throughput {size_kb} {iter}` | 参数均为 10 进制 | 单通道吞吐测试 |
> | `hpdma stress {start|stop|status} [size_kb] [chan_cnt]` | size/count 为 10 进制 | | 长时间压测，支持多通道并发 |
> | `hpdma neg_test` | 无 | 负向参数测试 |
> | `hpdma auto [iter]` | `iter` 为 10 进制 | 自动回归测试 |


## 5 demo 命令行演示


### 5.1 查看 help

命令：


```
ap_cmd hpdma help

```

预期结果：


```
HPDMA command help: addr=hex, len/size/count/id=dec
hpdma help
hpdma driver {init|deinit}
hpdma chan {id} {init|deinit|start|stop|get_remain_len}
hpdma int {id} {reg|enable_hf_fini|disable_hf_fini|enable_fini|disable_fini}
hpdma chnl alloc
hpdma chnl_free {free|force} {id}
hpdma copy {src_hex} {dst_hex} {len_dec}
...

```


### 5.2 Driver 初始化

命令：


```
ap_cmd hpdma driver init

```

预期结果：


```
hpdma driver init

```

说明：初始化 HPDMA driver 公共资源。多数测试命令会在注册 CLI 时自动初始化 driver；手动执行该命令可确认 driver 初始化路径正常。


### 5.3 通道申请和释放

申请通道：


```
ap_cmd hpdma chnl alloc

```

预期结果：


```
hpdma channel id:0

```

释放通道：


```
ap_cmd hpdma chnl_free free 0

```

预期结果：


```
hpdma channel free id:0 OK

```

如果通道 busy，可能输出：


```
hpdma channel free id:0 TIMEOUT - engine wedged; use 'hpdma chnl_free force {id}' to recover

```

此时可在确认允许丢弃在途数据后执行：


```
ap_cmd hpdma chnl_free force 0

```

预期结果：


```
hpdma channel force reclaim id:0 ret:0

```


### 5.4 普通通道控制

命令：


```
ap_cmd hpdma chan 0 init
ap_cmd hpdma chan 0 start
ap_cmd hpdma chan 0 stop
ap_cmd hpdma chan 0 get_remain_len
ap_cmd hpdma chan 0 deinit

```

预期结果：


```
hpdma init, id=0 src=0xXXXXXXXX dst=0xXXXXXXXX len=16
hpdma start, id=0
hpdma stop, id=0
hpdma get remain_len, id=0, len=0
hpdma deinit, id=0

```

说明：

> - `chan init` 会自动分配一组 16 字节对齐的 source/destination buffer，用于验证普通通道流程。
> - 该 case 主要验证 API 调用链，不用于大块数据正确性验证。


### 5.5 Memory copy 测试

命令：


```
ap_cmd hpdma copy 64cf0000 64cf1000 4096

```

参数说明：

> - `64cf0000`：source 地址，16 进制。
> - `64cf1000`：destination 地址，16 进制。
> - `4096`：搬运长度，10 进制，单位 byte。

预期成功结果：


```
hpdma copy: src=0x64cf0000 dst=0x64cf1000 len=4096 SUCCESS

```

预期失败结果：


```
hpdma copy: src=0x64cf0000 dst=0x64cf1000 len=4096 FAILED ret=-xxxx

```

说明：该命令按 `bk_hpdma_memcpy()` 返回值判断 SUCCESS/FAILED，不额外对任意地址做 CPU 读回比对。


### 5.6 1D 链表测试

命令：


```
ap_cmd hpdma link_test_1d 4 1024

```

参数说明：

> - `4`：descriptor 数量。
> - `1024`：每个 descriptor 搬运长度，单位 byte。

预期结果：


```
hpdma_link_test_1d: link_cnt=4 trans_len=1024
hpdma_link_test_1d: SUCCESS

```

说明：该 case 会分配 source/destination buffer，填充测试 pattern，执行链表传输后比较数据。


### 5.7 2D 链表测试

命令：


```
ap_cmd hpdma link_test_2d 2 128 8 256

```

参数说明：

> - `2`：descriptor 数量。
> - `128`：每行有效搬运字节数。
> - `8`：搬运行数。
> - `256`：源地址相邻行步进。

预期结果：


```
HPDMA_TEST: link_test_2d: link_cnt=2 xsize=128 ysize=8 step=256
HPDMA_TEST: link_test_2d: SUCCESS

```

说明：该 case 用于验证 stride 场景。destination 为连续布局，停止后逐行比较数据。


### 5.8 多通道并发单轮测试

命令：


```
ap_cmd hpdma concurrent_test 4 4096

```

参数说明：

> - `4`：并发通道数量。
> - `4096`：每个通道搬运长度。

预期结果：


```
HPDMA_TEST: concurrent_test: chan_cnt=4 trans_len=4096
HPDMA_TEST: concurrent_test: SUCCESS (4/4)

```

说明：

> - 每个通道使用独立 source buffer 和 destination buffer。
> - 所有通道 back-to-back 启动，等待所有通道完成后逐通道比较数据。


### 5.9 吞吐测试

命令：


```
ap_cmd hpdma throughput 4 200

```

参数说明：

> - `4`：单次搬运大小，单位 KB。
> - `200`：循环次数。

预期成功结果：


```
HPDMA_TEST: throughput: RESULT: SUCCESS size_kb=4 iter=200 errs=0 elapsed_ms=...
total_bytes=819200 rate=...MB/s (...KB/s)

```

预期失败结果：


```
HPDMA_TEST: throughput: RESULT: FAILED size_kb=4 iter=200 errs=1 elapsed_ms=...
total_bytes=819200 rate=...MB/s (...KB/s)

```

说明：该 case 使用一个通道和一个 descriptor 循环执行同步传输，按 `errs == 0` 判断 SUCCESS。


### 5.10 单通道长时间压测

启动：


```
ap_cmd hpdma stress start 4

```

查看状态：


```
ap_cmd hpdma stress status

```

停止：


```
ap_cmd hpdma stress stop

```

预期结果：


```
HPDMA_TEST: stress: started chan_cnt=1 size=4096
HPDMA_TEST: stress: running=1 chan_cnt=1 size=4096 loops=... err=0 elapsed_ms=... total_bytes=... rate~...KB/s
HPDMA_TEST: stress: ch0 dma_id=0 loops=... err=0
HPDMA_TEST: stress: stopped RESULT: SUCCESS chan_cnt=1 data_ok=1/1 loops=... err=0 size=4096 elapsed_ms=...

```

说明：finish ISR 中会自动重启下一轮传输，直到执行 `stress stop`。


### 5.11 多通道并发长时间压测

启动 4 通道并发压测，每个通道单次搬运 4KB：


```
ap_cmd hpdma stress start 4 4

```

查看状态：


```
ap_cmd hpdma stress status

```

停止：


```
ap_cmd hpdma stress stop

```

预期结果：


```
HPDMA_TEST: stress: started chan_cnt=4 size=4096
HPDMA_TEST: stress: running=1 chan_cnt=4 size=4096 loops=... err=0 elapsed_ms=... total_bytes=... rate~...KB/s
HPDMA_TEST: stress: ch0 dma_id=0 loops=... err=0
HPDMA_TEST: stress: ch1 dma_id=1 loops=... err=0
HPDMA_TEST: stress: ch2 dma_id=2 loops=... err=0
HPDMA_TEST: stress: ch3 dma_id=3 loops=... err=0
HPDMA_TEST: stress: stopped RESULT: SUCCESS chan_cnt=4 data_ok=4/4 loops=... err=0 size=4096 elapsed_ms=...

```

说明：

> - 每个通道都有独立 source buffer 和 destination buffer。
> - 该 case 覆盖多通道同时长时间循环传输。
> - 若 `chan_cnt` 超过 `HPDMA_ID_MAX`，命令会报参数错误。


### 5.12 负向测试

命令：


```
ap_cmd hpdma neg_test

```

预期结果：


```
HPDMA_TEST: [neg] init bad_id                 PASS
HPDMA_TEST: [neg] init null_cfg               PASS
...
HPDMA_TEST: neg_test: SUCCESS

```

说明：该 case 验证非法 id、空指针、loop 模式未对齐窗口、非法 descriptor 等参数是否被驱动拒绝。


### 5.13 自动回归测试

命令：


```
ap_cmd hpdma auto 1

```

预期结果：


```
HPDMA_TEST: ==== auto round 1/1 start ====
HPDMA_TEST: [CASE 01] link_1d small              PASS
HPDMA_TEST: [CASE 02] link_1d medium             PASS
...
HPDMA_TEST: RESULT: PASS 12/12 elapsed=...ms rounds=1

```

说明：该 case 串行执行 1D、2D、memcpy、通道申请释放和负向测试，适合作为基础回归。


## 6 常见失败和处理

> - `Source ysize must be >= 1`：配置中的 `ysize` 为 0，需要改为 1 或更大。
> - `each dim must <= 0xFFFF`：HPDMA x/y/step 字段为 16 bit，单字段不能超过 `0xFFFF`。
> - `bad params`：通道数量为 0、超过 `HPDMA_ID_MAX`，或传输长度为 0。
> - `FAILED ret=-xxxx`：查看 ret 对应错误码，重点检查 loop 模式地址窗口 16 字节对齐、长度、通道状态。
> - `stress` 停止时 `data_ok` 不等于 `chan_cnt`：表示至少一个通道数据比对失败，需要结合逐通道日志定位。
