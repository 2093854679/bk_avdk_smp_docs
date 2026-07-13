# 多核 Mailbox API


BK7259 为 CP+AP 异构多核：CP 侧逻辑 CPU 为 `MAILBOX_CPU0`、`MAILBOX_CPU1`，AP 侧为
`MAILBOX_CPU2`、`MAILBOX_CPU3`。跨核控制与数据（Wi-Fi、log、AT、电源等）在硬件 Mailbox
之上通过**逻辑通道**抽象；应用层使用 `include/driver/mailbox_channel.h` 中的 API 即可，
无需直接操作底层 `bk_mailbox_*` 硬件驱动（见 [外设 Mailbox](../peripheral/bk_mailbox.md "../peripheral/bk_mailbox.md")）。


## **逻辑通道编号**

逻辑通道号 `log_chnl` 为 8 位，编码规则如下（详见头文件宏）：


- 位 7–6：目标 CPU（`GET_DST_CPU_ID`）

- 位 5–4：源 CPU（`GET_SRC_CPU_ID`）

- 位 3–0：该源/目标对上的通道序号（`GET_LOG_CHNL_ID`，每对最多 16 个）

同一源/目标对内，**数值越小优先级越高**。AP 侧编译时 `SELF_CPU` 为 `MAILBOX_CPU2`。


## **系统预留通道（CP ↔ AP）**

`mailbox_channel.h` 中为 CP 与 AP 间预定义了多条系统通道，应用**不得占用**下列名称对应的
ID（节选）：


- `MB_CHNL_HW_CTRL`、`CP0_MB_CHNL_IPC` / `CP2_MB_CHNL_IPC`

- `MB_CHNL_PWC`、`MB_CHNL_WIFI_CMD`、`MB_CHNL_WIFI_DATA`

- `MB_CHNL_USB`、`MB_CHNL_MIPC_SYNC`、`MB_CHNL_AT`

- `MB_CHNL_UART0`、`MB_CHNL_UART1`、`MB_CHNL_FLASH`

- `MB_CHNL_SARADC`、`MB_CHNL_PHY`、`MB_CHNL_AUD_AEC`

- `MB_CHNL_LOG`：同向通道中**优先级最低**，枚举中须保持在末尾

自定义业务通道请在同向 `*_MB_LOG_CHNL_START` 与系统通道之间选取未使用的序号，或参考
`middleware/driver/mailbox/mb_ipc_test.c` 中的 IPC 通道规划。


## **典型调用流程**

1. `mb_chnl_init()` 初始化逻辑通道模块
2. `mb_chnl_open(log_chnl, callback_param)` 打开通道
3. `mb_chnl_ctrl()` 注册 `MB_CHNL_SET_RX_ISR`、`MB_CHNL_SET_TX_ISR`、
   `MB_CHNL_SET_TX_CMPL_ISR` 等回调
4. 填充 `mb_chnl_cmd_t` 后 `mb_chnl_write()` 发送；对端在 RX 回调中处理并回填
   `mb_chnl_ack_t`
5. 轮询场景可 `mb_chnl_read()`；结束时 `mb_chnl_close()`


## **大数据与指针传递**


- 命令结构 `mb_chnl_cmd_t` 仅含 `hdr` 与三个 `param` 字，适合传小参数或指针

- 跨核传递指针须保证对端 CPU 可访问该地址（共享 RAM 等）

- 需拷贝较大 payload 时，使用 `include/driver/mb_chnl_buff.h` 的
  `mb_chnl_get_tx_buff`、`mb_chnl_get_rx_buff` 交换区

- 复杂 RPC/服务注册可参考 `middleware/driver/mailbox/bk_api_ipc.c` 与
  `BK_IPC_CHANNEL_REGISTER` 宏


## **示例与调试**


- 示例说明：[multi-core mailbox](../../examples/platform/bk_logic_mailbox.md "../../examples/platform/bk_logic_mailbox.md")

- AP log 默认经 `MB_CHNL_LOG` 转发到 CP 串口，见 [日志系统](../../developer-guide/error_log/bk_log.md "../../developer-guide/error_log/bk_log.md")


### Header File


- [mailbox_channel.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/mailbox_channel.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/mailbox_channel.h")


### Functions

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") mb_chnl_init(void)

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") mb_chnl_open(u8 log_chnl, void *callback_param)

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") mb_chnl_close(u8 log_chnl)

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") mb_chnl_read(u8 log_chnl, [mb_chnl_cmd_t](#_CPPv413mb_chnl_cmd_t "mb_chnl_cmd_t") *read_buf)

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") mb_chnl_write(u8 log_chnl, [mb_chnl_cmd_t](#_CPPv413mb_chnl_cmd_t "mb_chnl_cmd_t") *cmd_buf)

[bk_err_t](os.md#_CPPv48bk_err_t "bk_err_t") mb_chnl_ctrl(u8 log_chnl, u8 cmd, void *param)


### Unions

union mb_chnl_hdr_t
:   Public Members

    u32 cmd

    u32 state

    u32 Reserved

    struct [mb_chnl_hdr_t](#_CPPv413mb_chnl_hdr_t "mb_chnl_hdr_t")::[anonymous] [anonymous]

    u32 data


### Structures

struct mb_chnl_cmd_t

struct mb_chnl_ack_t


### Macros

SYSTEM_CPU_NUM

DST_CPU_ID_MASK

DST_CPU_ID_POS

SRC_CPU_ID_MASK

SRC_CPU_ID_POS

LOG_CHNL_ID_MASK

GET_SRC_CPU_ID(log_chnl)

GET_DST_CPU_ID(log_chnl)

CPX_LOG_CHNL_START(src_cpu, dst_cpu)

GET_LOG_CHNL_ID(log_chnl)

SELF_CPU

MB_CHNL_MIPC

SRC_CPU

CHNL_STATE_MASK

CHNL_STATE_COM_FAIL


### Type Definitions

typedef void (*chnl_tx_cmpl_isr_t)(void *param, [mb_chnl_ack_t](#_CPPv413mb_chnl_ack_t "mb_chnl_ack_t") *ack_buf)

typedef void (*chnl_tx_isr_t)(void *param)

typedef void (*chnl_rx_isr_t)(void *param, [mb_chnl_cmd_t](#_CPPv413mb_chnl_cmd_t "mb_chnl_cmd_t") *cmd_buf)


### Enumerations

enum [anonymous]
:   *Values:*

    enumerator CP2_MB_LOG_CHNL_START

    enumerator CP2_MB_LOG_CHNL_END

    enumerator CP2_MB_LOG_CHNL_MAX

enum [anonymous]
:   *Values:*

    enumerator CP3_MB_LOG_CHNL_START

    enumerator CP3_MB_LOG_CHNL_END

    enumerator CP3_MB_LOG_CHNL_MAX

enum [anonymous]
:   *Values:*

    enumerator CP0_MB_LOG_CHNL_START

    enumerator MB_CHNL_HW_CTRL

    enumerator CP0_MB_CHNL_IPC

    enumerator MB_CHNL_PWC

    enumerator MB_CHNL_BT_CMD

    enumerator MB_CHNL_WIFI_CMD

    enumerator MB_CHNL_WIFI_DATA

    enumerator MB_CHNL_USB

    enumerator MB_CHNL_MIPC_SYNC

    enumerator MB_CHNL_AT

    enumerator MB_CHNL_UART0

    enumerator MB_CHNL_UART1

    enumerator MB_CHNL_FLASH

    enumerator MB_CHNL_SARADC

    enumerator MB_CHNL_PHY

    enumerator MB_CHNL_AUD_AEC

    enumerator MB_CHNL_LOG

    enumerator CP0_MB_LOG_CHNL_END

    enumerator CP0_MB_LOG_CHNL_MAX

enum [anonymous]
:   *Values:*

    enumerator ACK_STATE_PENDING

    enumerator ACK_STATE_COMPLETE

    enumerator ACK_STATE_FAIL

enum [anonymous]
:   *Values:*

    enumerator MB_CHNL_GET_STATUS

    enumerator MB_CHNL_SET_RX_ISR

    enumerator MB_CHNL_SET_TX_ISR

    enumerator MB_CHNL_SET_TX_CMPL_ISR

    enumerator MB_CHNL_WRITE_SYNC

    enumerator MB_CHNL_TX_RESET
