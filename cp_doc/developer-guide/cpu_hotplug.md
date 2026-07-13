# CPU Hotplug


BK7259 CP 子系统由 CPU0 和 CPU1 组成一个独立的 2-core FreeRTOS SMP。CPU Hotplug
支持在运行时动态下线 / 上线从核 CPU1，从而按负载在功耗与算力之间平衡。本章节介绍
CP 侧 hotplug 的功能、配置、默认上电行为、CLI / API 使用方法、动态负载策略
（governor）以及验证方法。


- [CPU Hotplug 使用指南](cpu_hotplug/bk_cpu_hotplug_user.md "bk_cpu_hotplug_user.md")

- CPU Hotplug 测试方法?????
