# 随机数 (RNG)



## RNG API Status

| API | BK7259_AP |
| --- | --- |
| [`bk_rand()`](#c.bk_rand "bk_rand") | Y |
| [`bk_fill_rand()`](#c.bk_fill_rand "bk_fill_rand") | Y |

备注

以下 API 已移除，请勿在新代码中使用：`bk_trng_driver_init`、`bk_trng_driver_deinit`、
`bk_trng_start`、`bk_trng_stop`。随机数请改用 `bk_rand()` 与 `bk_fill_rand()`。


## RNG API Reference

int bk_rand(void)
:   获取一个 32 位随机整数。

    返回值与 `RAND_MAX` 按位与后返回。熵源取决于工程配置（TrustEngine / OTP / 软件 `rand()`），
    详见 [随机数 (RNG) 使用指南](../../developer-guide/peripheral/bk_trng.md "../../developer-guide/peripheral/bk_trng.md")。

int bk_fill_rand(void *buff, size_t len)
:   向缓冲区填充 `len` 字节随机数据。

    参数
    :   - **buff** – 输出缓冲区指针

        - **len** – 待填充字节数

    返回
    :   成功返回 `0`；`buff` 为 `NULL` 或 `len` 为 `0` 时返回 `-1`


## 头文件


- [include/components/bk_platform.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/include/components/bk_platform.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/include/components/bk_platform.h")
