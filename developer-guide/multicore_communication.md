---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/multicore_communication/index.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 多核通讯

- 多核通讯在Armino AP(SMP)\+CP系统中主要是指AP子系统和CP子系统之间的通讯;
- 对于完全在AP子系统上开发的模块, 可以不用关注.

当前系统提供了两套多核通讯的接口:

- [基于Mailbox的IPC通讯接口](multicore_communication/bk_api_ipc.md)
- [基于Mailbox虚拟的Uart通讯接口](multicore_communication/bk_api_uart.md)
- [AP/CP异常Dump协同机制](multicore_communication/bk_ap_cp_dump_handoff.md)

## 模块导航

- [快速入门](../get-started.md)
- [开发者指南](../developer-guide.md)
- [AP(SMP)+CP架构](architecture.md)
- [系统启动流程](system_boot.md)
- [音频](audio.md)
- [配置工具](config_tools.md)
- [内存资源](memory_resource.md)
- [中断管理](interrupt.md)
- [基于Mailbox的IPC通讯接口](multicore_communication/bk_api_ipc.md)
- [基于Mailbox虚拟的Uart通讯接口](multicore_communication/bk_api_uart.md)
- [AP/CP异常Dump协同机制](multicore_communication/bk_ap_cp_dump_handoff.md)
- [外设资源](peripheral_resource.md)
- [构建系统](build_config.md)
- [新建工程介绍](create_new_project_rule.md)
