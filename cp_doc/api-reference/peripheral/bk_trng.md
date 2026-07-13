# 随机数 (RNG)


BK7259 已移除独立 TRNG 外设驱动（`bk_trng_*` 不再提供）。CP 侧随机数统一通过
`bk_rand()` 与 `bk_fill_rand()` 获取，定义于 `components/bk_platform.h`。

详细说明见 [RNG 开发指南](../../developer-guide/peripheral/bk_trng.md "../../developer-guide/peripheral/bk_trng.md")。


## RNG API Reference

int bk_rand(void)
:   获取一个 32 位随机整数。

int bk_fill_rand(void *buff, size_t len)
:   向缓冲区填充 `len` 字节随机数据。

    参数
    :   - **buff** – 输出缓冲区指针

        - **len** – 待填充字节数

    返回
    :   成功返回 `0`；参数无效时返回 `-1`


## 头文件


- `components/bk_platform.h`
