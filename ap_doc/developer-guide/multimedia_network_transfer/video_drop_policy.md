---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/multimedia_network_transfer/video_drop_policy.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 视频丢帧策略

<a id="id2"></a>

## 概述

Network Transfer 组件当前包含两类视频丢帧策略：

- **通道发送缓存丢帧策略**：实现文件为 `video_drop.c` / `video_drop.h`，通过视频通道的 `drop_check` 回调接入发送链路，根据下游发送缓存量和 H264 帧类型动态丢弃部分帧。
- **H264 编码输出 Buffer 反压丢帧策略**：实现文件为 `h264_backpressure_drop.c` / `h264_backpressure_drop.h`，在 H264 编码完成后、帧进入 ready queue 前工作，根据可用编码输出 buffer 数量保护 buffer 池。

两种策略解决的问题不同。`video_drop` 关注网络发送链路是否积压，`h264_backpressure_drop` 关注编码输出 buffer 是否即将耗尽。

<a id="id3"></a>

## 通道发送缓存丢帧策略

<a id="id4"></a>

### 功能说明

`video_drop` 是 Network Transfer 视频通道中的通用丢帧策略。发送视频帧时，`ntwk_trans_video_send()` 会先调用视频通道注册的 `drop_check` 回调；如果回调返回 `true`，当前帧不再进入后续的分片、打包和网络发送流程。

该策略主要用于网络发送侧缓存积压场景。例如 CS2 P2P 服务中，组件通过 `ntwk_register_get_drop_size_cb()` 注册发送缓存大小查询回调，然后由 `ntwk_video_drop_check()` 根据当前缓存量和 H264 帧类型决定是否丢帧。

<a id="id5"></a>

### 实现架构

核心状态由 `ntwk_h264_drop_info_t` 保存：

- `buffer_thd`：发送缓存阈值，由 `ntwk_video_drop_start(buffer_size)` 传入。
- `start_drop_thd`：开始丢帧阈值，当前为 `buffer_size / 2`。
- `drop_level_interval`：丢帧等级步进，当前为 `(buffer_size / 2) / 7`。
- `drop_level`：当前丢帧等级，缓存越高等级越高。
- `I_num` / `P_num`：当前 GOP 内 I/P 帧计数。
- `drop_period` / `status_total_size` / `status_cnt`：用于统计和降低丢帧等级。
- `write_size`：由传输服务注册的发送缓存大小查询回调。

处理流程如下：

<a id="id15"></a>
![video drop policy flow](../../../../_assets/ee74986221a563f48d09-ntwk_video_drop_policy_flow.png)


Figure 1\. 通道发送缓存丢帧策略流程图

<a id="id6"></a>

### 核心逻辑

1. `ntwk_video_drop_check(frame)` 只处理 `PIXEL_FMT_H264`。
2. 首次运行时读取 H264 基础配置，只在 GOP P 帧数量满足策略要求时启用。
3. 通过 `write_size` 回调读取当前发送缓存量 `WriteSize`。
4. 计算 `cur_size = frame->length + WriteSize`。
5. 当 `cur_size > start_drop_thd` 时，根据超过阈值的程度提升 `drop_level`。
6. 当缓存回落时，通过 `ntwk_h264_down_drop_level()` 按统计周期降低 `drop_level`。
7. 对 P 帧，根据 `P_num` 和 `drop_level` 决定是否丢弃。
8. 在最高丢帧等级下，策略也可能丢弃部分 I 帧，并标记当前 GOP 的后续帧需要继续丢弃，直到缓存恢复。

<a id="id7"></a>

### 使用方式

Network Transfer 初始化时会调用 `ntwk_video_drop_init()` 创建策略状态。传输服务需要在配置视频通道时注册 `drop_check`，并启动策略：

```
ctxt->video_chan->drop_check = ntwk_video_drop_check;

ntwk_register_get_drop_size_cb(ntwk_cs2_get_current_write_size);
ntwk_video_drop_start(CONFIG_CS2_TX_BUFFER_THD);
```

发送路径中无需应用层额外调用。`ntwk_trans_video_send()` 会在分片和打包之前自动执行：

```
if (s_ntwk_trans_ctxt->video_chan->drop_check != NULL)
{
    if (s_ntwk_trans_ctxt->video_chan->drop_check((frame_buffer_t *)data) == true)
    {
        return BK_OK;
    }
}
```

<a id="id8"></a>

### 适用场景

该策略适用于网络发送缓存持续增大、发送端来不及把视频帧送到下游协议栈的场景。它属于发送链路上的主动降载策略，可以减少进入分片、打包和底层发送的数据量。

<a id="h264-buffer"></a>

## H264 编码输出 Buffer 反压丢帧策略

<a id="id9"></a>

### 功能说明

`h264_backpressure_drop` 用于保护 H264 编码输出 buffer 池。它不通过视频通道的 `drop_check` 回调接入，而是在编码帧完成后、放入 ready queue 前执行。

当下游消费速度慢时，编码输出 free queue 中可用 buffer 数量会减少。如果数量低于低水位，策略进入 drop 状态：新完成的 H264 帧不进入 ready queue，而是直接回收到 free queue。等可用 buffer 数量恢复到高水位后，策略停止 drop，并请求下一帧强制 IDR，帮助解码端从丢帧后的参考帧断裂中恢复。

该策略由 `CONFIG_NTWK_H264_DROP_POLICY` 控制编译。

<a id="id10"></a>

### 实现架构

策略状态由 `h264_backpressure_drop.c` 内部静态变量维护，调用方不需要保存 policy 实例：

- `policy_enable`：策略是否启用。
- `drop_enable`：当前是否处于丢帧状态。
- `force_idr_pending`：是否存在待消费的强制 IDR 请求。
- `max_available_buffer_count`：可用编码输出 buffer 的最大数量。
- `start_available_buffer_count`：开始 drop 的低水位。
- `stop_available_buffer_count`：停止 drop 的高水位。

处理流程如下：

<a id="id16"></a>
![h264 backpressure drop policy flow](../../../../_assets/8f73eb0e520e1c0f41c4-ntwk_h264_backpressure_drop_policy_flow.png)


Figure 2\. H264 编码输出 Buffer 反压丢帧策略流程图

<a id="doorbell"></a>

### Doorbell 工程使用示例

`projects/multimedia/doorbell` 工程中，H264 反压丢帧策略通过 `projects/common_components/multimedia_device_service` 模块接入。该模块维护编码输出 `free_queue` / `ready_queue`，并使用 `h264_available_buffer_count` 统计当前可用编码输出 buffer 数量。

使用流程如下：

<a id="id17"></a>
![h264 backpressure drop doorbell usage flow](../../../../_assets/3179470d046c2a436c91-ntwk_h264_backpressure_drop_doorbell_flow.png)


Figure 3\. Doorbell 工程 H264 反压丢帧使用示例流程图

<a id="id11"></a>

### 水位策略

初始化时通过 `ntwk_h264_backpressure_drop_init(max_available_buffer_count)` 计算阈值：

```
#define NTWK_H264_DROP_MIN_AVAILABLE_BUFFER_COUNT   (5)
#define NTWK_H264_DROP_START_AVAILABLE_BUFFER_COUNT (2)
#define NTWK_H264_DROP_STOP_AVAILABLE_BUFFER_MARGIN (4)
```

阈值规则如下：

- `max_available_buffer_count <= 5` 时，策略不启用。
- `available_buffer_count <= 2` 时，开始 drop。
- `available_buffer_count >= max_available_buffer_count - 4` 时，停止 drop。

例如 `max_available_buffer_count` 为 20 时，`available_buffer_count <= 2` 开始 drop，`available_buffer_count >= 16` 停止 drop。

<a id="id12"></a>

### 使用方式

初始化 encoded frame buffer 队列时初始化策略：

```
ntwk_h264_backpressure_drop_init(MAX_QUE_LEN);
```

编码完成并准备将 H264 帧送入 ready queue 前，读取当前可用 buffer 数量，并调用 drop 判断：

```
drop_frame = ntwk_h264_backpressure_drop_check(available_buffer_count, frame);
```

如果返回 `true`，调用方应将当前帧直接回收到 free queue。回收成功后更新可用 buffer 计数，并通知策略：

```
ret = rtos_push_to_queue(&free_queue, &msg, BEKEN_NO_WAIT);
if (ret == BK_OK)
{
    available_buffer_count++;
    ntwk_h264_backpressure_drop_on_recycle(available_buffer_count, frame);
}
```

编码完成回调中消费一次性 IDR 请求。如果返回 `true`，调用编码器接口强制下一帧输出 IDR：

```
if (ntwk_h264_backpressure_drop_consume_force_idr())
{
    bk_h264_encode_force_idr(encoder);
}
```

<a id="id13"></a>

### 注意事项

- `available_buffer_count` 必须由调用方维护，并和 free queue 的增减保持一致。
- 如果 `available_buffer_count` 在多个上下文中读写，需要使用临界区或锁保护。
- 策略只处理 H264 帧，非 H264 帧会直接忽略。
- 当前实现是单实例静态 policy，适合当前单路 H264 编码流。如果后续存在多路独立 H264 流，需要扩展为显式 policy 实例。
- 该策略解决的是编码输出 buffer 池耗尽风险，不解决单帧 H264 输出 buffer 太小导致的编码溢出问题。

<a id="id14"></a>

## 两种策略对比

| 策略 | 触发依据 | 接入位置 |
| --- | --- | --- |
| `video_drop` | 网络发送缓存量、H264 帧类型 | `ntwk_trans_video_send()` |
| `h264_backpressure_drop` | 可用编码输出 buffer 数量 | 编码完成到 ready queue 之前 |

`video_drop` 适合处理网络发送链路积压，`h264_backpressure_drop` 适合处理编码输出 buffer 池被下游阻塞耗尽。两者可以同时存在，但接入点和保护对象不同。
