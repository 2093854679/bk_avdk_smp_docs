---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/examples/bk_example.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 用例编写

$ARMINO\_PATH/examples 目录下存放 ARMINO 用例，用例用于:

> - 展示 ARMINO API 的用法， 如 WiFi API 等
> - ARMINO 关键模块的用法，如 Kconfig 配置， Backtrace 查看， 编译等

每个用例可以独立地进行编译与测试。

<a id="id2"></a>

## 何时编写用例？

下列情况需要增加用例：

> - 单个 API 较为复杂时，如 WiFi 配置 bk\_wifi\_sta\_set\_config() 等
> - 使用某个功能涉及一组相关 API 时
> - ARMINO 用户容易出错的 API
> - ARMINO 用户经常使用的功能，如 Debug, 编译， CLI 等
> - ARMINO 用户明确提出需求时

备注

当一个用例是说明 ARMINO API 或者功能时， 就应该放在 $ARMINO\_PATH/examples 中， 而非放在其他位置.

<a id="id3"></a>

## 用例编写规范

用例编写规范如下：

> - 一个用例只说明一个功能，或者一组强相关 API
> - 用例尽量简单
> - 同一功能不要重复编写用例
> - 定义 main() 函数的文件命名成 example\_main.c, 如定义 hello world 用例，
>   则命名成 hello\_world\_main.c, 不要命名成 main.c，因为过多 main.c 不便于 IDE 工具搜索
> - 用例 Kconfig 中的配置建议以 EXAMPLE 开头，避免与 SDK 其他配置生命，方便 IDE 工具搜索
> - 每个用例都需要文档，即 README.md 文件， 未来会通过 README.md 自动生成用例文档

## 模块导航

- [简介](../../introduction.md)
- [H/W 参考手册](../../hw-reference.md)
- [API 参考手册](../../api-reference.md)
- [开发者指南](../../developer-guide.md)
- [软件架构与分层](../architecture.md)
- [系统安全](../security.md)
- [低功耗与电源管理](../power_save.md)
- [设备管理框架](../driver_model.md)
- [外设与驱动](../peripheral.md)
- [出错与日志](../error_log.md)
- [系统调试](../debug_trace.md)
- [Wi-Fi](../wifi.md)
- [Bluetooth](../bluetooth.md)
- [HTTP](../http.md)
- [用例编写](../examples.md)
- [文档系统](../documentation.md)
- [OS 相关参考](../../os.md)
- [样例演示](../../examples.md)
- [应用开发](../../application.md)
- [开发与贡献代码流程](../../process.md)
- [云平台](../../cloud.md)
