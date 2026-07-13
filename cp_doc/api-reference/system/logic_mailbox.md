# 多核 Mailbox API


BK7259 CP 侧通过逻辑通道与 AP（`MAILBOX_CPU2`、`MAILBOX_CPU3`）及 CP 内另一核通信。
应用使用 `include/driver/mailbox_channel.h`；CP 编译时 `SELF_CPU` 为 `MAILBOX_CPU0`。


## **逻辑通道编号**


- 位 7–6：目标 CPU；位 5–4：源 CPU；位 3–0：通道序号（每对最多 16 个）

- 同向通道内数值越小优先级越高

CP → AP 方向预定义 `MB_CHNL_WIFI_CMD`、`MB_CHNL_LOG` 等系统通道，`MB_CHNL_LOG` 优先级
最低且须保持在枚举末尾。自定义通道勿与 `mailbox_channel.h` 中 `MB_CHNL_*` 冲突。


## **典型流程**

`mb_chnl_init` → `mb_chnl_open` → ``` mb_chnl_ctrl``（注册 RX/TX 回调）→
``mb_chnl_write ``` / `mb_chnl_read` → `mb_chnl_close`。

大块数据或跨核拷贝见 `mb_chnl_buff.h`；IPC 服务注册见 `bk_api_ipc.c`。


## **示例**

[multi-core mailbox](../../examples/platform/bk_logic_mailbox.md "../../examples/platform/bk_logic_mailbox.md")


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

    enumerator CP0_MB_LOG_CHNL_START

    enumerator CP0_MB_LOG_CHNL_END

    enumerator CP0_MB_LOG_CHNL_MAX

enum [anonymous]
:   *Values:*

    enumerator CP1_MB_LOG_CHNL_START

    enumerator CP1_MB_LOG_CHNL_END

    enumerator CP1_MB_LOG_CHNL_MAX

enum [anonymous]
:   *Values:*

    enumerator CP2_MB_LOG_CHNL_START

    enumerator MB_CHNL_HW_CTRL

    enumerator CP2_MB_CHNL_IPC

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

    enumerator CP2_MB_LOG_CHNL_END

    enumerator CP2_MB_LOG_CHNL_MAX

enum [anonymous]
:   *Values:*

    enumerator CP3_MB_LOG_CHNL_START

    enumerator CP3_MB_LOG_CHNL_END

    enumerator CP3_MB_LOG_CHNL_MAX

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
