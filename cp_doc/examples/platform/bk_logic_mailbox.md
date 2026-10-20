---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/examples/platform/bk_logic_mailbox.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="multi-core-mailbox"></a>

# multi-core mailbox

<a id="id1"></a>

## 1 功能概述

BK7259 为 CP\+AP 异构多核：CP 侧 `cpu0`、`cpu1` 对应 `MAILBOX_CPU0`、`MAILBOX_CPU1`；
AP 侧 `ap0`、`ap1` 对应 `MAILBOX_CPU2`、`MAILBOX_CPU3`。硬件 Mailbox 每对 CPU 间有
数据通路与应答通路；驱动在其上抽象出逻辑通道，应用只需调用逻辑通道 API 即可跨核收发。

逻辑通道号同时表示优先级：同一源、目标对内，编号数值越小优先级越高（系统通道如
`MB_CHNL_LOG` 通常排在同向枚举末尾，优先级最低）。

<a id="id6"></a>
![mailbox](../../../../_assets/988a38b25c11538dcd45-multi_core_mailbox.png)


Figure 1\. 逻辑通道示意图

<a id="id2"></a>

## 2 参考代码

- 逻辑通道实现：`middleware/driver/mailbox/mailbox_channel.c`
- IPC 测试示例：`middleware/driver/mailbox/mb_ipc_test.c`
- 高层 IPC 注册：`middleware/driver/mailbox/bk_api_ipc.c`
- 大块数据交换区：`middleware/driver/mailbox/mb_chnl_buff.c`

<a id="api"></a>

## 3 API 文档

详见 [多核 Mailbox API](../../api-reference/system/logic_mailbox.md)。

<a id="id3"></a>

## 4 使用步骤

典型流程如下：

- 调用 `mb_chnl_init()` 初始化
- 调用 `mb_chnl_open()` 打开逻辑通道
- 调用 `mb_chnl_ctrl()` 注册回调：

  - `MB_CHNL_SET_RX_ISR`：接收命令
  - `MB_CHNL_SET_TX_ISR`：发送侧通知（可选）
  - `MB_CHNL_SET_TX_CMPL_ISR`：发送完成及 ACK
- 填充 `mb_chnl_cmd_t` 后 `mb_chnl_write()` 发送
- 轮询场景可 `mb_chnl_read()`；处理完毕 `mb_chnl_close()`

<a id="id4"></a>

## 5 注意事项

- 勿占用 `mailbox_channel.h` 中已定义的 `MB_CHNL_*` 系统通道 ID
- 跨核传递指针须使用双方均可访问的内存；大数据请用 `mb_chnl_get_tx_buff` 等交换区 API
- CP 侧为 AP log 汇聚出口；AP log 经 `MB_CHNL_LOG` 转发，见 [日志系统](../../developer-guide/error_log/bk_log.md)

<a id="id5"></a>

## 6 运行现象（示意）

CP 与 AP 互发短消息后，串口可见类似 log（具体通道号因工程而异）:

```
APP_MBOX:I(...):open channel: 0x46 on CPU
APP_MBOX:I(...):cpu0 recv ap0 msg seq:[0]- info:[...]
ap0:APP_MBOX:I(...):ap0 recv cpu0 msg seq:[1]- info:[...]
```
