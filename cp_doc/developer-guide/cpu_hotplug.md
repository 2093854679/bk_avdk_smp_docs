---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/cpu_hotplug/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cpu-hotplug"></a>

# CPU Hotplug

BK7259 CP 子系统由 CPU0 和 CPU1 组成一个独立的 2-core FreeRTOS SMP。CPU Hotplug
支持在运行时动态下线 / 上线从核 CPU1，从而按负载在功耗与算力之间平衡。本章节介绍
CP 侧 hotplug 的功能、配置、默认上电行为、CLI / API 使用方法、动态负载策略
（governor）以及验证方法。

- [CPU Hotplug 使用指南](cpu_hotplug/bk_cpu_hotplug_user.md)
- [CPU Hotplug 测试方法](cpu_hotplug/bk_cpu_hotplug_test.md)

## 模块导航

- [简介](../introduction.md)
- [H/W 参考手册](../hw-reference.md)
- [API 参考手册](../api-reference.md)
- [开发者指南](../developer-guide.md)
- [软件架构与分层](architecture.md)
- [系统安全](security.md)
- [低功耗与电源管理](power_save.md)
- [设备管理框架](driver_model.md)
- [外设与驱动](peripheral.md)
- [出错与日志](error_log.md)
- [系统调试](debug_trace.md)
- [CPU Hotplug 使用指南](cpu_hotplug/bk_cpu_hotplug_user.md)
- [CPU Hotplug 测试方法](cpu_hotplug/bk_cpu_hotplug_test.md)
- [Wi-Fi](wifi.md)
- [HTTP](http.md)
- [用例编写](examples.md)
- [文档系统](documentation.md)
- [操作系统与内存管理](../os.md)
- [样例演示](../examples.md)
- [应用开发](../application.md)
- [开发与贡献代码流程](../process.md)
- [云平台](../cloud.md)
