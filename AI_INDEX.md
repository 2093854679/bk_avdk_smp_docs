# BK7259 AVDK SMP AI Index

> 给 AI/Codex/Claude Code 使用的轻量入口。复制 `bk_avdk_smp/` 文件夹到工程后，优先读本文件，再按相对路径查原始文档。

## 这个文件夹是什么

这是 Beken BK7259 AVDK SMP 文档镜像，核心是 AP(SMP) + CP 架构：

- AP 文档入口：[ap_doc/index.md](ap_doc/index.md)
- CP 文档入口：[cp_doc/index.md](cp_doc/index.md)
- SMP 总入口：[index.md](index.md)
- 快速入门：[get-started.md](get-started.md)
- SMP 开发指南：[developer-guide.md](developer-guide.md)

回答问题或写代码时，优先引用本文件夹内的 `.md` 原文路径，不要只凭记忆生成 API。

## 推荐检索流程

1. 先判断问题属于 `SMP 架构`、`AP`、`CP`、`API reference`、`example/demo`、`外设`、`编译/烧录/配置` 中哪一类。
2. 先读对应入口页，再进入子文档。
3. 写代码前同时查 `API reference` 和 `examples`，用示例确认初始化、参数和调用顺序。
4. AP/CP 不确定时，同时查 `ap_doc/` 和 `cp_doc/`，不要混用不同处理器侧的 API。

常用搜索命令示例：

```bash
rg -n "UART|bk_uart|uart" .
rg -n "GPIO|bk_gpio|gpio" .
rg -n "Wi-Fi|wifi|bk_wifi" .
rg -n "BLE|Bluetooth|bk_ble|bk_bt" .
rg -n "DMA|bk_dma" .
```

## 快速定位

### 架构与 AP/CP 分工

- SMP 总架构：[developer-guide/architecture.md](developer-guide/architecture.md)
- AP/CP 外设资源分配：[developer-guide/peripheral_resource.md](developer-guide/peripheral_resource.md)
- 多核通信：[developer-guide/multicore_communication.md](developer-guide/multicore_communication.md)
- AP/CP dump handoff：[developer-guide/multicore_communication/bk_ap_cp_dump_handoff.md](developer-guide/multicore_communication/bk_ap_cp_dump_handoff.md)
- 内存资源：[developer-guide/memory_resource.md](developer-guide/memory_resource.md)
- 系统启动：[developer-guide/system_boot.md](developer-guide/system_boot.md)

### 编译、配置、烧录

- 快速入门：[get-started.md](get-started.md)
- Menuconfig：[get-started/menuconfig.md](get-started/menuconfig.md)
- 构建系统：[developer-guide/build_config.md](developer-guide/build_config.md)
- 构建概述：[developer-guide/build_config/bk_build_overview.md](developer-guide/build_config/bk_build_overview.md)
- Kconfig 配置：[developer-guide/config_tools/bk_config_kconfig.md](developer-guide/config_tools/bk_config_kconfig.md)
- 分区配置：[developer-guide/config_tools/bk_config_auto_partitions.md](developer-guide/config_tools/bk_config_auto_partitions.md)
- 烧录工具 BKFIL：[developer-guide/config_tools/bk_tool_bkfil.md](developer-guide/config_tools/bk_tool_bkfil.md)

### AP 侧文档

- AP 首页：[ap_doc/index.md](ap_doc/index.md)
- AP 概述：[ap_doc/introduction.md](ap_doc/introduction.md)
- AP 开发指南：[ap_doc/developer-guide.md](ap_doc/developer-guide.md)
- AP API 参考：[ap_doc/api-reference.md](ap_doc/api-reference.md)
- AP 示例：[ap_doc/examples.md](ap_doc/examples.md)
- AP 外设支持：[ap_doc/support_peripherals.md](ap_doc/support_peripherals.md)
- AP FAQ：[ap_doc/FAQ.md](ap_doc/FAQ.md)

AP 常见模块：

- AP 外设开发：[ap_doc/developer-guide/peripheral.md](ap_doc/developer-guide/peripheral.md)
- AP 外设 API：[ap_doc/api-reference/peripheral.md](ap_doc/api-reference/peripheral.md)
- AP 蓝牙开发：[ap_doc/developer-guide/bluetooth.md](ap_doc/developer-guide/bluetooth.md)
- AP 蓝牙 API：[ap_doc/api-reference/bluetooth.md](ap_doc/api-reference/bluetooth.md)
- AP 多媒体：[ap_doc/developer-guide/multimedia.md](ap_doc/developer-guide/multimedia.md)
- AP USB：[ap_doc/developer-guide/peripheral/bk_usb.md](ap_doc/developer-guide/peripheral/bk_usb.md)

### CP 侧文档

- CP 首页：[cp_doc/index.md](cp_doc/index.md)
- CP 概述：[cp_doc/introduction.md](cp_doc/introduction.md)
- CP 开发指南：[cp_doc/developer-guide.md](cp_doc/developer-guide.md)
- CP API 参考：[cp_doc/api-reference.md](cp_doc/api-reference.md)
- CP 示例：[cp_doc/examples.md](cp_doc/examples.md)

CP 常见模块：

- CP 外设开发：[cp_doc/developer-guide/peripheral.md](cp_doc/developer-guide/peripheral.md)
- CP 外设 API：[cp_doc/api-reference/peripheral.md](cp_doc/api-reference/peripheral.md)
- CP Wi-Fi 开发：[cp_doc/developer-guide/wifi.md](cp_doc/developer-guide/wifi.md)
- CP 蓝牙开发：[cp_doc/developer-guide/bluetooth.md](cp_doc/developer-guide/bluetooth.md)
- CP 蓝牙 API：[cp_doc/api-reference/bluetooth.md](cp_doc/api-reference/bluetooth.md)
- CP 低功耗：[cp_doc/developer-guide/power_save.md](cp_doc/developer-guide/power_save.md)
- CP 调试与日志：[cp_doc/developer-guide/debug_trace.md](cp_doc/developer-guide/debug_trace.md)

## 按问题类型查哪里

| 问题 | 优先查 |
| --- | --- |
| BK7259 AP/CP/SMP 是什么关系 | `developer-guide/architecture.md`, `developer-guide/peripheral_resource.md` |
| 怎么编译、配置、烧录 | `get-started.md`, `get-started/menuconfig.md`, `developer-guide/build_config.md`, `developer-guide/config_tools/` |
| 某个外设怎么用 | `ap_doc/developer-guide/peripheral/`, `cp_doc/developer-guide/peripheral/`, 再查对应 `api-reference/peripheral/` |
| 某个 API 函数参数 | `ap_doc/api-reference/` 或 `cp_doc/api-reference/` |
| 有没有示例代码流程 | `ap_doc/examples/`, `cp_doc/examples/` |
| Wi-Fi 相关 | `cp_doc/developer-guide/wifi/`, `cp_doc/api-reference/` 中的网络/系统相关文档 |
| BLE/BT 相关 | `ap_doc/developer-guide/bluetooth/`, `cp_doc/developer-guide/bluetooth/`, `api-reference/bluetooth/` |
| 低功耗 | `cp_doc/developer-guide/power_save/` |
| 日志、调试、异常 | `cp_doc/developer-guide/debug_trace.md`, `cp_doc/developer-guide/error_log/` |
| POSIX/OS 抽象 | `ap_doc/api-reference/system/posix/`, `cp_doc/api-reference/system/posix/`, `os.md` |

## 写代码时的注意事项

- 先确认目标代码运行在 AP 侧还是 CP 侧。
- 不要把 AP API 和 CP API 直接混用；同名模块也可能有不同约束。
- API 参考通常只说明函数，示例文档更适合确认初始化流程和调用顺序。
- 涉及外设时，同时检查 `support_peripherals.md` 或外设资源分配文档，确认该外设属于 AP、CP 还是共享资源。
- 回答时尽量附上原文路径，例如 `cp_doc/developer-guide/peripheral/bk_uart.md`。

## 关键词别名

- BK7259, AVDK SMP, Armino SMP, AP, CP
- UART, serial, bk_uart
- GPIO, bk_gpio
- I2C, SPI, QSPI, I2S, PWM, ADC, DMA
- Wi-Fi, wifi, bk_wifi
- BLE, BT, Bluetooth, bk_ble, bk_bt
- power save, low power, sleep, wakeup
- menuconfig, Kconfig, partition, BKFIL, bootloader
