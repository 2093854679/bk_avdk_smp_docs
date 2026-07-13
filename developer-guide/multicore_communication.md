# 多核通讯



- 多核通讯在Armino AP(SMP)+CP系统中主要是指AP子系统和CP子系统之间的通讯;

- 对于完全在AP子系统上开发的模块, 可以不用关注.

当前系统提供了两套多核通讯的接口:


- [基于Mailbox的IPC通讯接口](multicore_communication/bk_api_ipc.md "bk_api_ipc.md")

- [基于Mailbox虚拟的Uart通讯接口](multicore_communication/bk_api_uart.md "bk_api_uart.md")

- [AP/CP异常Dump协同机制](multicore_communication/bk_ap_cp_dump_handoff.md "bk_ap_cp_dump_handoff.md")
