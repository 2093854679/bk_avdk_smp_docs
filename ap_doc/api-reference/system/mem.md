# 内存 API


BK7259 AP 侧内存接口由 `include/os/mem.h` 提供。动态分配与释放**不能在中断上下文**调用。


## **快速索引**

完整说明、示例与宏定义见 [内存接口](../../os/bk_mem.md "../../os/bk_mem.md")。


- **默认堆**：`os_malloc`、`os_zalloc`、`os_free`、`os_realloc`

- **专用 SRAM 堆**：`os_sram_malloc`、``` os_sram_zalloc``（释放统一用 ``os_free ```）

- **HSRAM 堆（仅 AP）**：`hsram_malloc`、`hsram_zalloc`、``` hsram_realloc``（释放用 ``hsram_free ```，实为 `os_free`）

- **PSRAM 堆**：`psram_malloc`、`psram_zalloc`、``` psram_realloc``（``bk_psram_realloc ``` 为其别名）

- **内存操作**：`os_memcpy`、`os_memset`、`os_memcmp`、`os_memcmp_const`、`os_memmove` 等

- **调试统计**：``` os_dump_memory_stats``（需 ``CONFIG_MEM_DEBUG ``` 或 `CONFIG_MALLOC_STATIS`）

- **UAF 辅助（仅 AP）**：`os_dump_heap_free_history`、``` os_trace_heap_free_addr``（需 ``CONFIG_HEAP_UAF_AUDIT_POISON ```）

- **PSRAM 用量**：`bk_psram_heap_get_used_count`、`bk_psram_heap_get_used_state`、`bk_psram_heap_dump_data`

- **其他**：`os_malloc_wifi_buffer`、`os_show_memory_config_info`


## **与 OS 抽象层关系**

任务、队列、信号量等 RTOS 接口见 [操作系统](os.md "os.md")。堆内存调试 CLI（`memshow`、`memhistory`、`memtrace` 等）见 [问题定位](../../developer-guide/debug_trace.md "../../developer-guide/debug_trace.md")。
