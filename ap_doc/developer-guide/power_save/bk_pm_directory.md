---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_pm_directory.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap-bk-pm"></a>

# AP侧 `bk_pm` 目录文件说明

AP侧低功耗组件目录位于 `ap/components/bk_pm`，主要提供AP侧PM接口封装、CP通信client
和公共头文件。目录文件说明如下：

| 分类 | 文件 | 说明 |
| --- | --- | --- |
| 构建配置 | `CMakeLists.txt` | 定义 `bk_pm` 组件编译源文件；在 `CONFIG_PM_ENABLE` 和 `CONFIG_PM_CLIENT` 使能时编译 `src/clients` 下的AP侧PM client实现。 |
| 构建配置 | `Kconfig` | 定义AP侧PM相关配置项，用于控制PM功能、PM client以及相关子功能是否参与编译。 |
| 说明文档 | `README.md`、`PM_SLEEP_CALLBACK_README.md` | 提供 `bk_pm` 模块结构、接口和睡眠回调机制说明。 |
| 公共头文件 | `include/pm_interface.h`、`include/bk_pm_internal_api.h` | 提供PM内部管理接口和AP侧内部调用声明。 |
| 公共头文件 | `include/pm_power.h`、`include/pm_sleep.h`、`include/pm_wakeup_source.h` | 定义电源投票、睡眠模式、唤醒源等低功耗核心接口和类型。 |
| 公共头文件 | `include/pm_mailbox.h` | 定义AP与CP通过mailbox交互时使用的PM消息、命令和通信状态。 |
| 公共头文件 | `include/pm_debug.h`、`include/pm_types.h`、`include/pm_psram.h` | 提供PM调试、公共类型和PSRAM低功耗相关接口定义。 |
| 接口入口 | `src/bk_pm.c` | AP侧PM接口入口，提供 `bk_pm_*` API封装；在未启用完整PM功能时也提供部分weak 默认实现。 |
| Client实现 | `src/clients/bk_pm_client.c` | AP侧PM client公共实现，包含睡眠回调注册、电源投票等基础client逻辑。 |
| Client实现 | `src/clients/bk_pm_client_power.c`、`bk_pm_client_clock.c`、 `bk_pm_client_sleep.c`、`bk_pm_client_ap_ctrl.c` | 分别处理电源控制、时钟/频率、睡眠模式和AP启动关闭控制相关的CP通信。 |
| Client实现 | `src/clients/bk_pm_client_mailbox.c`、`bk_pm_client_thread.c`、 `bk_pm_client_misc.c` | 负责mailbox通信、client线程和杂项PM接口处理。 |
| 示例代码 | `ap/middleware/driver/pwr_clk/pm_ap_demo.c` | 演示AP侧发起低功耗流程：创建demo线程和消息队列，配置RTC/GPIO唤醒源，投APP sleep票和AP关闭票，并在低压唤醒回调后恢复默认模式。 |
| 测试命令 | `ap/components/bk_cli/cli_pwr.c` | 注册 `pm_ap_demo` CLI命令，支持 `init`、`sleep`、`deep_sleep` 子命令， 用于初始化AP低功耗demo并触发sleep/deep sleep测试流程。 |
