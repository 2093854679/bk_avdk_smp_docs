# 内存接口



## **内存管理介绍**

> - 内存管理接口提供了动态内存分配和释放的统一接口
> - BK7259 支持多堆：默认堆、专用 SRAM 堆、PSRAM，AP 侧另有 HSRAM 堆
> - 提供了内存操作相关的辅助函数（拷贝、设置、比较等）
> - 支持内存调试功能，可以跟踪内存分配和泄漏
> - 所有内存分配/释放函数**不能在中断上下文中调用**

警告


- 在中断上下文中调用os_malloc/os_free会触发断言错误

- 内存分配失败时会返回NULL，使用前必须检查返回值

- 释放内存后应将指针设置为NULL，避免野指针

- 频繁的小内存分配可能导致内存碎片化


## **内存类型说明**

Armino平台支持两种内存类型：


**SRAM (Static RAM)**
:   - 片上静态随机存储器，访问速度快

    - 容量相对较小（通常几百KB）

    - 适合存储频繁访问的数据和代码

    - 功耗相对较低


**PSRAM (Pseudo Static RAM)**
:   - 片外伪静态随机存储器，容量大

    - 访问速度相对SRAM较慢

    - 适合存储大块数据缓冲区

    - 需要通过CONFIG_PSRAM_AS_SYS_MEMORY使能


**HSRAM（仅 AP）**
:   - 高速 SRAM 专用堆，与默认堆、`os_sram_*` 池相互独立

    - 适合对延迟敏感且需与默认堆隔离的缓冲区

    - 通过 `hsram_malloc`、`hsram_zalloc`、`hsram_realloc` 分配，`hsram_free` 释放（宏映射为 `os_free`）


**堆选择说明**
:   - `os_malloc`：默认堆；在部分配置下 SRAM 不足时可回落到 PSRAM

    - `os_sram_malloc`：仅从专用 SRAM 堆分配，不回落 PSRAM

    - `psram_malloc`：仅从 PSRAM 堆分配

    - `hsram_malloc`：仅从 HSRAM 堆分配（AP）


## **SRAM内存接口**


- 分配SRAM内存:

  ```
  void *os_malloc(size_t size)

  从SRAM堆中分配指定大小的内存块

  参数说明：

  -size: 要分配的字节数

  返回值：

  -成功：返回分配的内存指针

  -失败：返回NULL


  **FreeRTOS对应接口**: pvPortMalloc()
  ```

注意

不能在中断上下文中调用此函数


- 分配并清零的SRAM内存:

  ```
  void *os_zalloc(size_t size)

  从SRAM堆中分配内存并将其初始化为0

  参数说明：

  -size: 要分配的字节数

  返回值：

  -成功：返回分配的内存指针（内容已清零）

  -失败：返回NULL

  实现：内部调用os_malloc()后，使用os_memset()清零
  ```

- 释放SRAM内存:

  ```
  void os_free(void *ptr)

  释放之前通过os_malloc()或os_zalloc()分配的内存

  参数说明：

  -ptr: 要释放的内存指针，可以为NULL（安全）


  **FreeRTOS对应接口**: vPortFree()
  ```

注意

不能在中断上下文中调用此函数


- 重新分配SRAM内存:

  ```
  void *os_realloc(void *ptr, size_t size)

  改变已分配内存块的大小

  参数说明：

  -ptr: 原内存指针，可以为NULL

  -size: 新的大小（字节）

  返回值：

  -成功：返回新的内存指针

  -失败：返回NULL，原内存保持不变

  实现：分配新内存，拷贝原数据，释放原内存
  ```


## **专用 SRAM 堆接口**

与 `os_malloc` 不同，以下接口**仅**从专用 SRAM 堆分配，不会在 SRAM 不足时自动申请 PSRAM。


- 分配专用 SRAM 内存:

  ```
  void *os_sram_malloc(size_t size)

  参数与返回值同 ``os_malloc``；释放使用 ``os_free``。
  ```

- 分配并清零的专用 SRAM 内存:

  ```
  void *os_sram_zalloc(size_t size)

  内部在 ``os_sram_malloc`` 后清零。
  ```


## **HSRAM 堆接口（仅 AP）**


- 分配 HSRAM 内存:

  ```
  void *hsram_malloc(size_t size)
  ```

- 分配并清零:

  ```
  void *hsram_zalloc(size_t size)
  ```

- 重新分配:

  ```
  void *hsram_realloc(void *ptr, size_t size)
  ```

- 释放:

  ```
  ``hsram_free(ptr)`` 为 ``os_free`` 的宏别名。
  ```


## **PSRAM内存接口**


- 分配PSRAM内存:

  ```
  void *psram_malloc(size_t size)

  从PSRAM堆中分配指定大小的内存块

  参数说明：

  -size: 要分配的字节数

  返回值：

  -成功：返回分配的内存指针

  -失败：返回NULL

  使用场景：

  - 大块数据缓冲区（如图像、音视频缓冲）

  - 不需要频繁访问的数据
  ```

备注

需要使能CONFIG_PSRAM_AS_SYS_MEMORY配置


- 分配并清零的PSRAM内存:

  ```
  void *psram_zalloc(size_t size)

  从PSRAM堆中分配内存并将其初始化为0

  参数说明：

  -size: 要分配的字节数

  返回值：

  -成功：返回分配的内存指针（内容已清零）

  -失败：返回NULL
  ```

- 释放PSRAM内存:

  ```
  void psram_free(void *ptr)

  释放之前通过psram_malloc()或psram_zalloc()分配的内存

  参数说明：

  -ptr: 要释放的内存指针
  ```

备注

psram_free实际是os_free的宏定义，统一使用os_free释放内存


- 重新分配PSRAM内存:

  ```
  void *psram_realloc(void *ptr, size_t size)

  宏 ``bk_psram_realloc`` 与其等价。

  改变已分配PSRAM内存块的大小

  参数说明：

  -ptr: 原PSRAM内存指针

  -size: 新的大小（字节）

  返回值：

  -成功：返回新的内存指针

  -失败：返回NULL
  ```


## **内存操作接口**


- 内存拷贝:

  ```
  void *os_memcpy(void *out, const void *in, UINT32 n)

  将源地址的n个字节拷贝到目标地址

  参数说明：

  -out: 目标地址

  -in: 源地址（不能为NULL）

  -n: 拷贝的字节数

  返回值：

  -返回目标地址指针


  **标准C接口**: memcpy()
  ```

- 内存拷贝（字对齐优化）:

  ```
  void os_memcpy_word(uint32_t *out, const uint32_t *in, uint32_t n)

  按字（4字节）拷贝内存，比os_memcpy()更高效

  参数说明：

  -out: 目标地址（uint32_t指针）

  -in: 源地址（uint32_t指针）

  -n: 拷贝的字节数（建议4字节对齐）

  使用场景：

  - PSRAM数据拷贝（建议使用）

  - 大块数据传输
  ```

- 内存设置:

  ```
  void *os_memset(void *b, int c, UINT32 len)

  将指定内存区域设置为特定值

  参数说明：

  -b: 目标地址

  -c: 要设置的值（通常为0）

  -len: 设置的字节数

  返回值：

  -返回目标地址指针


  **标准C接口**: memset()
  ```

- 内存设置（字对齐优化）:

  ```
  void os_memset_word(uint32_t *b, int32_t c, uint32_t n)

  按字（4字节）设置内存，比os_memset()更高效

  参数说明：

  -b: 目标地址（uint32_t指针）

  -c: 要设置的值

  -n: 设置的字节数
  ```

- 内存比较:

  ```
  INT32 os_memcmp(const void *s1, const void *s2, UINT32 n)

  比较两块内存区域的内容

  参数说明：

  -s1: 第一块内存地址

  -s2: 第二块内存地址

  -n: 比较的字节数

  返回值：

  -0: 两块内存内容相同

  -<0: s1 < s2

  ->0: s1 > s2


  **标准C接口**: memcmp()
  ```

- 常量时间内存比较:

  ```
  int os_memcmp_const(const void *a, const void *b, size_t len)

  与 ``os_memcmp`` 语义相同，实现避免分支泄露，适用于密码学相关比较场景。
  ```

- 内存移动:

  ```
  void *os_memmove(void *out, const void *in, UINT32 n)

  将源地址的n个字节移动到目标地址，支持内存重叠

  参数说明：

  -out: 目标地址

  -in: 源地址（不能为NULL）

  -n: 移动的字节数

  返回值：

  -返回目标地址指针


  **标准C接口**: memmove()
  ```

备注

当源地址和目标地址有重叠时，应使用os_memmove()而不是os_memcpy()


## **内存调试接口**

当使能CONFIG_MEM_DEBUG或CONFIG_MALLOC_STATIS配置时，内存分配函数会自动记录调用位置，用于内存泄漏检测。


- 调试版内存分配:

  ```
  void *os_malloc_debug(const char *func_name, int line, size_t size, int need_zero)

  参数说明：

  -func_name: 调用函数名（通常使用__FUNCTION__）

  -line: 调用行号（通常使用__LINE__）

  -size: 分配大小

  -need_zero: 是否需要清零（0：不清零，1：清零）

  返回值：

  -成功：返回分配的内存指针

  -失败：返回NULL
  ```

- 调试版内存释放:

  ```
  void *os_free_debug(const char *func_name, int line, void *pv)

  参数说明：

  -func_name: 调用函数名

  -line: 调用行号

  -pv: 要释放的内存指针

  返回值：

  -返回NULL
  ```

- 导出内存统计信息:

  ```
  void os_dump_memory_stats(uint32_t start_tick, uint32_t ticks_since_malloc, const char* task)

  导出内存使用统计信息，用于分析内存泄漏

  参数说明：

  -start_tick: 起始tick

  -ticks_since_malloc: 从分配到现在的tick数

  -task: 任务名称过滤
  ```

当同时使能 `CONFIG_HEAP_UAF_AUDIT_POISON` 时，可调用以下接口辅助 UAF 定位（对应 CLI `memhistory`、`memtrace`）：


- 导出 free 历史:

  ```
  void os_dump_heap_free_history(uint32_t count)

  打印最近 ``count`` 条堆释放审计记录（块地址、大小、调用栈等）。
  ```

- 追踪指定地址:

  ```
  void os_trace_heap_free_addr(uint32_t addr)

  在 free 审计环中查找是否曾释放过 ``addr``，并打印匹配记录。
  ```


## **特殊用途接口**


- 显示内存配置信息:

  ```
  void os_show_memory_config_info(void)

  打印当前系统的内存配置和使用情况
  ```

- 查询 PSRAM 堆用量:

  ```
  uint32_t bk_psram_heap_get_used_count(void)

  返回当前 PSRAM 堆已用字节数（实现以头文件为准）。

  void bk_psram_heap_get_used_state(void)

  打印 PSRAM 堆详细占用信息。

  void bk_psram_heap_dump_data(void)

  导出 PSRAM 堆内部数据结构，供深度调试。
  ```

- Wi-Fi 缓冲区分配:

  ```
  void *os_malloc_wifi_buffer(size_t size)

  向 Wi-Fi 子系统申请专用缓冲区，释放仍使用 ``os_free``。
  ```


## **使用示例**

基本内存分配示例:


```
#include <os/mem.h>

void memory_basic_example(void)
{
    void *buffer;
    size_t size = 1024;

    // 分配内存
    buffer = os_malloc(size);
    if (buffer == NULL) {
        os_printf("Failed to allocate memory\r\n");
        return;
    }

    // 使用内存
    os_memset(buffer, 0, size);
    os_printf("Allocated %d bytes at %p\r\n", size, buffer);

    // 释放内存
    os_free(buffer);
    buffer = NULL;  // 避免野指针
}

```

分配并清零的内存:


```
void *buffer = os_zalloc(512);  // 分配512字节并清零
if (buffer) {
    // 使用buffer
    os_free(buffer);
}

```

PSRAM内存分配示例:


```
#include <os/mem.h>

void psram_example(void)
{
    #define LARGE_BUFFER_SIZE  (100 * 1024)  // 100KB

    // 分配大块PSRAM内存
    void *large_buffer = psram_malloc(LARGE_BUFFER_SIZE);
    if (large_buffer == NULL) {
        os_printf("Failed to allocate PSRAM\r\n");
        return;
    }

    // 使用PSRAM缓冲区
    os_memset(large_buffer, 0, LARGE_BUFFER_SIZE);

    // 释放PSRAM内存
    psram_free(large_buffer);  // 等同于os_free()
}

```

内存重新分配示例:


```
void realloc_example(void)
{
    void *buffer;
    void *new_buffer;

    // 初始分配100字节
    buffer = os_malloc(100);
    if (buffer == NULL) return;

    // 重新分配为200字节
    new_buffer = os_realloc(buffer, 200);
    if (new_buffer != NULL) {
        buffer = new_buffer;  // 更新指针
    } else {
        // 重新分配失败，原内存仍有效
        os_printf("Realloc failed\r\n");
    }

    os_free(buffer);
}

```

内存操作示例:


```
void memory_operations_example(void)
{
    uint8_t src[100], dst[100];

    // 内存设置
    os_memset(src, 0xAA, sizeof(src));

    // 内存拷贝
    os_memcpy(dst, src, sizeof(src));

    // 内存比较
    if (os_memcmp(src, dst, sizeof(src)) == 0) {
        os_printf("Memory content is same\r\n");
    }

    // 内存移动（支持重叠）
    os_memmove(src + 10, src, 50);
}

```

结构体内存管理示例:


```
typedef struct {
    int id;
    char name[32];
    void *data;
} my_struct_t;

void struct_memory_example(void)
{
    my_struct_t *obj;

    // 分配结构体内存并清零
    obj = (my_struct_t *)os_zalloc(sizeof(my_struct_t));
    if (obj == NULL) {
        return;
    }

    // 初始化结构体
    obj->id = 1;
    os_memcpy(obj->name, "test", 5);
    obj->data = os_malloc(256);

    // 使用结构体...

    // 释放内存
    if (obj->data) {
        os_free(obj->data);
    }
    os_free(obj);
}

```

备注


- **内存释放原则**：
  :   - 使用os_malloc分配的内存，使用os_free释放

      - 使用psram_malloc分配的内存，使用psram_free（即os_free）释放

      - 释放后立即将指针设置为NULL

- **性能考虑**：
  :   - SRAM访问速度快，适合频繁访问

      - PSRAM容量大但访问慢，适合大块缓冲

      - 使用os_memcpy_word进行字对齐拷贝可提高性能

- **调试支持**：
  :   - 使能 CONFIG_MEM_DEBUG 或 CONFIG_MALLOC_STATIS 可跟踪分配位置并调用 os_dump_memory_stats

      - 使能 CONFIG_HEAP_UAF_AUDIT_POISON 后可调用 os_dump_heap_free_history、os_trace_heap_free_addr

      - AP 侧可通过 ap_cmd memshow、memhistory、memtrace 等 CLI 查看堆状态


## **内存管理宏定义**

`CONFIG_MEM_DEBUG` 或 `CONFIG_MALLOC_STATIS` 开启时，`os_malloc`、`os_sram_malloc`、`psram_malloc`、`hsram_malloc` 等宏自动展开为带 `__FUNCTION__`、`__LINE__` 的 `*_debug` 实现；关闭时使用 `*_release` 路径。

关闭调试宏时仍可用的典型映射:


```
#define psram_free          os_free
#define hsram_free          os_free
#define os_sram_free        os_free
#define bk_psram_realloc    psram_realloc

```

调试模式下部分宏展开示例:


```
#if (CONFIG_MALLOC_STATIS || CONFIG_MEM_DEBUG)
#define os_malloc(size)       os_malloc_debug(__FUNCTION__, __LINE__, size, 0)
#define os_sram_malloc(size)  sram_malloc_debug(__FUNCTION__, __LINE__, size, 0)
#define psram_malloc(size)    psram_malloc_debug(__FUNCTION__, __LINE__, size, 0)
#define hsram_malloc(size)    hsram_malloc_debug(__FUNCTION__, __LINE__, size, 0)
#endif

```

在 `CONFIG_HEAP_UAF_AUDIT_POISON` 开启且处于上述调试宏分支时，头文件另声明 `os_dump_heap_free_history`、`os_trace_heap_free_addr`。


## **参考信息**


- API头文件：`include/os/mem.h`

- 实现文件：`components/bk_rtos/freertos/mem_arch.c`
