---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/system/mem.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="api"></a>

# 内存 API

BK7259 CP 侧内存接口由 `include/os/mem.h` 提供。动态分配与释放\*\*不能在中断上下文\*\*调用。

<a id="id1"></a>

## **快速索引**

完整说明、示例与宏定义见 [内存接口](../../os/bk_mem.md)。

- **默认堆**：`os_malloc`、`os_zalloc`、`os_free`
- **专用 SRAM 堆**：`os_sram_malloc`、`os_sram_zalloc`、``` os_sram_calloc``（释放统一用 ``os_free ```）
- **PSRAM 堆**：`psram_malloc`、``` psram_zalloc``（释放用 ``psram_free ```，实为 `os_free`）
- **内存操作**：`os_memcpy`、`os_memset`、`os_memcmp`、`os_memmove` 等
- **调试统计**：``` os_dump_memory_stats``（需 ``CONFIG_MEM_DEBUG ``` 或 `CONFIG_MALLOC_STATIS`）
- **PSRAM 用量**：`bk_psram_heap_get_used_count`、`bk_psram_heap_get_used_state`、`bk_psram_heap_dump_data`
- **其他**：`os_malloc_wifi_buffer`、`os_show_memory_config_info`

<a id="os"></a>

## **与 OS 抽象层关系**

任务、队列、信号量等 RTOS 接口见 [操作系统](os.md)。堆内存调试 CLI（`memshow` 等）见 [问题定位](../../developer-guide/debug_trace.md)。

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [外设](../peripheral.md)
- [系统](../system.md)
- [操作系统](os.md)
- [事件机制](bk_event.md)
- [POSIX](posix.md)
- [多核 Mailbox](logic_mailbox.md)
- [开发者指南](../../developer-guide.md)
- [操作系统与内存管理](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
