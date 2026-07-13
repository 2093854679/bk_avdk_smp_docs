# Watchdog



## AP `wwdt` API 状态

BK7259 AP 侧没有 AON_WDT 硬件 API，对外可用的硬件看门狗 API 只有 `wwdt`。

| API | BK7259_AP |
| --- | --- |
| `bk_wwdt_driver_init()` | Y |
| `bk_wwdt_driver_deinit()` | Y |
| `bk_wwdt_start()` | Y |
| `bk_wwdt_stop()` | Y |
| `bk_wwdt_feed()` | Y |
| `bk_wwdt_get_feed_time()` | Y |
| `bk_wwdt_set_feed_time()` | Y |
| `bk_wwdt_is_driver_inited()` | Y |
| `bk_wwdt_get_cpu_id()` | Y |


## `wwdt` API 头文件

> - API 头文件：`ap/include/driver/wwdt.h`
> - 类型定义：`ap/include/driver/wwdt_types.h`、`ap/include/driver/hal/hal_wwdt_types.h`
