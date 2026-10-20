---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/multimedia_network_transfer/bk_network_transfer.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="multimedia-network-transfer-component"></a>

# 多媒体网络传输组件 (Multimedia Network Transfer Component)

<a id="id1"></a>

## 概述

Multimedia Network Transfer 是 BK 提供的统一多媒体网络传输抽象层组件，用于多媒体数据（音频、视频）和控制命令的网络传输。该组件采用 **分层架构** 和 **模块化设计** ，通过标准化的接口将上层多媒体应用与底层传输协议解耦，使开发者能够灵活切换或自定义传输方案。

**核心特性**：

- **统一抽象接口**：为上层应用提供一致的API，屏蔽底层传输协议差异
- **通道化管理**：独立的控制、视频、音频三个通道，各通道独立配置和管理
- **模块化设计**：提供可复用的数据打包、分片重组、丢帧策略等功能模块
- **协议可插拔**：支持动态注册传输方案，方便集成自定义协议
- **事件驱动机制**：通过回调机制实时通知应用层状态变化和数据接收

**应用场景**：

- 音视频实时传输（视频监控、音频对讲、实时直播）
- 远程控制命令传输（IoT设备控制、参数配置）

<a id="id2"></a>

## 组件架构

<a id="id3"></a>

### 整体架构图

Network Transfer 组件采用\*\*三层架构\*\*设计：

<a id="id32"></a>
![network transfer design](../../../../../_assets/a16442b8911cbbc7d4da-ntwk_whole_struct.png)


Figure 1\. Network Transfer 组件架构图

<a id="id4"></a>

### 核心数据结构

**1\. 网络传输上下文 (ntwk\_trans\_ctxt\_t)**

整个组件的核心管理结构，维护三个通道的配置和状态：

```
typedef struct {
    char service_name[NTWK_TRANS_SERVICE_NAME_LEN];  // 传输服务名称
    ntwk_trans_ctrl_chan_t *cntrl_chan;              // 控制通道
    ntwk_trans_video_chan_t *video_chan;             // 视频通道
    ntwk_trans_audio_chan_t *audio_chan;             // 音频通道
    bool initialized;                                 // 初始化标志
} ntwk_trans_ctxt_t;
```

**2\. 通道结构 (Channel Structure)**

每个通道包含数据处理的完整回调链：

```
typedef struct {
    chan_type_t type;                                      // 通道类型
    int (*send)(uint8_t *data, uint32_t length);          // 发送回调
    int (*recive)(uint8_t *data, uint32_t length);        // 接收回调
    int (*pack)(uint8_t *data, uint32_t length, ...);     // 打包回调
    int (*unpack)(uint8_t *data, uint32_t length);        // 解包回调
    bk_err_t (*fragment)(uint8_t *data, uint32_t length); // 分片回调
    bk_err_t (*unfragment)(uint8_t *data, uint32_t len);  // 重组回调
} ntwk_trans_ctrl_chan_t;

typedef struct {
    chan_type_t type;
    image_format_t vid_type;                               // 视频格式
    int (*send)(uint8_t *data, uint32_t len, image_format_t type);
    // ... 其他回调与ctrl_chan类似
    bool (*drop_check)(frame_buffer_t *frame);            // 丢帧策略
} ntwk_trans_video_chan_t;

typedef struct {
    chan_type_t type;
    audio_enc_type_t aud_type;                            // 音频编码
    int (*send)(uint8_t *data, uint32_t len, audio_enc_type_t type);
    // ... 其他回调与ctrl_chan类似
} ntwk_trans_audio_chan_t;
```

<a id="id5"></a>

### 通道类型与状态机

**通道类型**：

```
typedef enum {
    NTWK_TRANS_CHAN_CTRL = 0,    // 控制通道：传输控制命令和信令
    NTWK_TRANS_CHAN_VIDEO,        // 视频通道：传输视频流数据
    NTWK_TRANS_CHAN_AUDIO,        // 音频通道：传输音频流数据
    NTWK_TRANS_CHAN_MAX
} chan_type_t;
```

**通道状态机**：

```
typedef enum {
    NTWK_TRANS_CHAN_START,              // 启动状态
    NTWK_TRANS_CHAN_WAITING_CONNECTED,  // 等待连接
    NTWK_TRANS_CHAN_CONNECTED,          // 已连接
    NTWK_TRANS_CHAN_DISCONNECTED,       // 已断开
    NTWK_TRANS_CHAN_STOP,               // 停止状态
} ntwk_trans_chan_state;
```

**事件类型**：

```
typedef enum {
    NTWK_TRANS_EVT_START,        // 通道启动事件
    NTWK_TRANS_EVT_CONNECTED,    // 连接建立事件
    NTWK_TRANS_EVT_DISCONNECTED, // 连接断开事件
    NTWK_TRANS_EVT_STOP,         // 通道停止事件
} evt_code_t;
```

<a id="id6"></a>

## 组件功能模块

Network Transfer 提供了一系列可复用的公共功能模块，各传输方案可根据需要选择性集成：

<a id="pack-unpack"></a>

### 1\. 数据打包/解包模块 (Pack/Unpack)

**功能说明**：

为媒体数据添加/解析传输协议头，包含序列号、时间戳、CRC校验等元信息，确保数据完整性和可追踪性。

**数据包格式**：

```
typedef struct {
    uint16_t magic;         // 魔数 0xF0D5
    uint16_t flags;         // 标志位（CRC使能等）
    uint32_t timestamp;     // 时间戳（毫秒）
    uint16_t sequence;      // 序列号
    uint16_t length;        // 载荷长度
    uint8_t  crc;           // CRC8 校验值
    uint8_t  reserved[3];   // 保留字段
    uint8_t  payload[];     // 实际数据载荷
} __attribute__((__packed__)) ntwk_pack_head_t;
```

**头部大小**：16 字节 (HEAD\_SIZE\_TOTAL)

**主要API**：

```
// 初始化和启动
bk_err_t ntwk_pack_init(chan_type_t chan_type);
bk_err_t ntwk_pack_chan_start(chan_type_t chan_type,
                               uint16_t max_rx_size,
                               uint16_t max_tx_size);

// 注册接收回调
bk_err_t ntwk_pack_register_recv_cb(chan_type_t chan_type,
                                     ntwk_pack_recv_cb_t recv_cb);

// 打包/解包函数（通道回调接口）
int ntwk_pack_ctrl_pack(uint8_t *data, uint32_t length,
                        uint8_t **pack_ptr, uint32_t *pack_ptr_length);
int ntwk_pack_ctrl_unpack(uint8_t *data, uint32_t length);

int ntwk_pack_video_pack(...);
int ntwk_pack_video_unpack(...);

int ntwk_pack_audio_pack(...);
int ntwk_pack_audio_unpack(...);
```

**使用场景**：

- 提供序列号检测丢包
- 提供时间戳实现音视频同步
- CRC8 校验保证数据完整性

<a id="fragment-unfragment"></a>

### 2\. 数据分片/重组模块 (Fragment/Unfragment)

**功能说明**：

当媒体帧大小超过网络MTU时，自动将大帧拆分为多个小包发送，接收端自动重组还原完整帧。

**分片头格式**：

```
typedef struct {
    uint8_t id;       // 帧ID（来自frame->sequence）
    uint8_t eof;      // End Of Frame标志
    uint8_t cnt;      // 当前分片序号
    uint8_t size;     // 总分片数量
    uint8_t data[];   // 分片数据载荷
} __attribute__((__packed__)) ntwk_fragm_head_t;
```

**分片头大小**：4 字节 (NTWK\_FRAG\_HEADER\_SIZE)

**主要API**：

```
// 初始化
bk_err_t ntwk_fragmentation_init(chan_type_t chan_type);

// 发送端：启动分片模块
bk_err_t ntwk_fragment_start(chan_type_t chan_type,
                              uint32_t fragment_size,  // 每个分片大小
                              void *user_data);
bk_err_t ntwk_fragment_register_recv_cb(chan_type_t chan_type,
                                         fragment_recv_t cb);

// 接收端：启动重组模块
bk_err_t ntwk_unfragment_start(chan_type_t chan_type,
                                uint32_t frame_size,  // 最大帧大小
                                void *user_data);

// 注册重组回调（三个必须成套配置）
bk_err_t ntwk_unfragment_register_malloc_cb(chan_type_t chan_type,
                                             unfragment_data_malloc_cb_t cb);
bk_err_t ntwk_unfragment_register_send_cb(chan_type_t chan_type,
                                           unfragment_data_send_cb_t cb);
bk_err_t ntwk_unfragment_register_free_cb(chan_type_t chan_type,
                                           unfragment_data_free_cb_t cb);

// 分片/重组函数（通道回调接口）
int ntwk_fragment_video_fragment(uint8_t *data, uint32_t length);
int ntwk_fragment_video_unfragment(uint8_t *data, uint32_t length);
```

**分片大小计算**：

```
// 有效载荷大小 = MTU - Pack头 - Fragment头
int pack_hdr_size = ntwk_pack_get_header_size();     // 16字节
int frag_hdr_size = ntwk_fragm_get_header_size();    // 4字节
int payload_size = MTU - pack_hdr_size - frag_hdr_size;

// 示例：UDP MTU=1472
// payload_size = 1472 - 16 - 4 = 1452字节
```

**使用场景**：

- H.264 视频 I 帧（通常几十KB）
- JPEG 图像（根据分辨率可能超过MTU）
- 大块控制数据传输

**重组机制**：

- 接收端维护帧缓冲区，按分片序号(cnt)重组
- 支持乱序接收
- 超时机制丢弃不完整帧（防止内存泄漏）

<a id="video-drop-policy"></a>

### 3\. 视频丢帧策略模块 (Video Drop Policy)

**功能说明**：

在网络拥塞或性能瓶颈时，智能丢弃部分视频帧以保证整体流畅性，优先保留关键帧（I帧）。

**主要API**：

```
// 初始化丢帧模块
bk_err_t ntwk_video_drop_init(void);

// 默认丢帧策略（可在通道配置中使用）
bool ntwk_video_drop_check_default(frame_buffer_t *frame);
```

**使用方式**：

```
// 在传输服务初始化时配置
ctxt->video_chan->drop_check = ntwk_video_drop_check_default;

// 或自定义丢帧策略
bool custom_drop_policy(frame_buffer_t *frame) {
    int queue_depth = get_video_send_queue_depth();

    // 队列过深时只保留I帧
    if (queue_depth > 10) {
        return (frame->frame_type != FRAME_TYPE_I);
    }
    return false;
}
ctxt->video_chan->drop_check = custom_drop_policy;
```

**丢帧策略考虑因素**：

- 发送队列深度
- 帧类型（I/P/B帧）
- 网络带宽估计
- 缓冲区状态

<a id="event-notification"></a>

### 4\. 事件通知模块 (Event Notification)

**功能说明**：

通过事件队列和回调机制，将通道状态变化异步通知给应用层，避免阻塞底层传输线程。

**事件结构**：

```
typedef struct {
    chan_type_t chan_type;  // 发生事件的通道
    evt_code_t code;        // 事件代码
    int param;              // 事件参数
} ntwk_trans_event_t;
```

**主要API**：

```
// 应用层注册事件回调
bk_err_t ntwk_trans_register_msg_event_cb(ntwk_trans_msg_event_cb_t cb);

// 传输服务上报事件（内部API）
void ntwk_msg_event_report(uint32_t event, uint32_t param, uint32_t chan_type);
```

**事件处理流程**：

1. 传输服务调用 `ntwk_msg_event_report()` 发送事件到消息队列
2. 事件处理线程 `ntwk_msg_message_handle()` 从队列中取出事件
3. 调用应用层注册的回调函数 `event_cb(&event)`

**典型事件流程**：

```
通道启动:  START -> CONNECTED -> 数据传输 -> DISCONNECTED -> STOP

异常断线:  CONNECTED -> DISCONNECTED -> (应用层重连) -> CONNECTED
```

<a id="sdp-session-description-protocol"></a>

### 5\. SDP 协商模块 (Session Description Protocol)

**功能说明**：

提供会话描述和能力协商功能，用于媒体格式、编解码参数的协商（可选模块）。

**应用场景**：

- 点对点通信建立时的能力协商
- 动态切换编码格式
- 多媒体会话管理

<a id="id7"></a>

## 组件运行机制

<a id="id8"></a>

### 1\. 初始化流程

```
应用层调用 ntwk_trans_ctxt_init()
    ↓
分配全局上下文 s_ntwk_trans_ctxt
    ↓
初始化三个通道结构体
(cntrl_chan, video_chan, audio_chan)
    ↓
初始化公共功能模块
├─ ntwk_msg_init/start()         // 事件通知
├─ ntwk_video_drop_init()        // 丢帧策略
├─ ntwk_pack_init() × 3          // Pack模块（三通道）
└─ ntwk_fragmentation_init() × 3 // Fragment模块（三通道）
    ↓
设置 initialized = true
```

<a id="id9"></a>

### 2\. 传输服务注册流程

以TCP服务为例：

```
应用调用 bk_tcp_trans_service_init("tcp_service")
    ↓
调用 ntwk_trans_ctxt_init()  // 初始化核心上下文
    ↓
初始化TCP底层资源 ntwk_tcp_init() × 3
    ↓
获取上下文 ctxt = ntwk_trans_get_ctxt()
    ↓
配置通道回调函数
├─ 控制通道:
│   ├─ ctxt->cntrl_chan->send = ntwk_tcp_ctrl_send_packet
│   ├─ ctxt->cntrl_chan->pack = ntwk_pack_ctrl_pack
│   ├─ ctxt->cntrl_chan->unpack = ntwk_pack_ctrl_unpack
│   └─ 注册启动/停止回调
│       ntwk_in_register_ctrl_start_cb(ntwk_tcp_ctrl_chan_start)
│       ntwk_in_register_ctrl_stop_cb(ntwk_tcp_ctrl_chan_stop)
│
├─ 视频通道:
│   ├─ ctxt->video_chan->send = ntwk_tcp_video_send_packet
│   ├─ ctxt->video_chan->pack = ntwk_pack_video_pack
│   ├─ ctxt->video_chan->fragment = ntwk_fragment_video_fragment
│   ├─ 启动Pack模块
│   ├─ 启动Fragment模块
│   └─ 注册启动/停止回调
│
└─ 音频通道: （类似配置）
    ↓
服务注册完成
```

<a id="id10"></a>

### 3\. 数据发送流程

```
应用调用 ntwk_trans_video_send(data, len, IMAGE_H264)
    ↓
检查上下文和通道有效性
    ↓
[可选] 调用 drop_check() 检查是否丢帧
    ↓
[可选] 调用 fragment(data, len) 进行分片
    ↓       如果数据无需分片，继续下一步
    ↓
[可选] 调用 pack(data, len, &pack_ptr, &pack_len) 打包
    ↓       添加协议头（序列号、时间戳、CRC等）
    ↓
调用 send(pack_ptr, pack_len, vid_type)
    ↓       传输服务具体实现（TCP/UDP/CS2）
    ↓
底层网络发送 (socket send)
```

**分片发送流程**：

```
fragment(data, len)
    ↓
计算分片数量: count = len / fragment_size
    ↓
循环发送每个分片:
for (i = 0; i < count; i++)
    ↓
    构造分片头: {id, cnt=i+1, eof, size}
    ↓
    拷贝分片数据
    ↓
    调用 fragment_recv_cb()  // 即 ntwk_trans_fragment_rx_handler
        ↓
        pack(fragment_data)  // 对分片再打包
        ↓
        send(packed_fragment) // 发送分片
```

<a id="id11"></a>

### 4\. 数据接收流程

```
底层网络接收线程收到数据
    ↓
调用 ntwk_trans_xxx_recv_handler(data, len)
    ↓
[可选] 调用 unpack(data, len) 解包
    ↓       验证魔数、CRC、提取payload
    ↓       调用 pack_recv_cb() -> ntwk_trans_pack_rx_handler()
    ↓
[可选] 调用 unfragment(data, len) 重组
    ↓       缓存分片到内存
    ↓       检查是否收到所有分片 (eof=1)
    ↓       重组完成后调用 unfragment_send_cb()
    ↓
调用通道的 recive(data, len)
    ↓       即应用层注册的接收回调
    ↓
应用层处理数据
```

**重组流程详解**：

```
unfragment(fragment_data, len)
    ↓
将分片加入数据池队列
    ↓
重组线程 unfragment_process_task_entry() 处理
    ↓
解析分片头: {id, cnt, eof, size}
    ↓
如果 cnt=1:  // 第一个分片
    ├─ 调用 malloc_cb() 申请帧缓冲区
    └─ 初始化重组状态
    ↓
拷贝分片数据到帧缓冲区对应位置
    ↓
如果 eof=1 且 cnt=size:  // 最后一个分片且完整
    ├─ 调用 send_cb(frame_buffer) 发送完整帧到应用层
    └─ 调用 free_cb(frame_buffer) 释放缓冲区
```

<a id="id12"></a>

### 5\. 通道启动流程

```
应用调用 ntwk_trans_chan_start(NTWK_TRANS_CHAN_VIDEO, NULL)
    ↓
调用 ntwk_in_start(chan_type, param)
    ↓
根据通道类型调用对应的启动回调:
switch (chan_type)
├─ CTRL:  ntwk_in_cfg->ctrl_start(param)
├─ VIDEO: ntwk_in_cfg->video_start(param)
└─ AUDIO: ntwk_in_cfg->audio_start(param)
    ↓
传输服务的启动实现 (如 ntwk_tcp_video_chan_start)
    ↓
创建Socket / 绑定端口 / 监听连接
    ↓
创建接收线程
    ↓
上报事件: ntwk_msg_event_report(NTWK_TRANS_EVT_START, ...)
    ↓
等待远程连接
    ↓
连接建立后上报: ntwk_msg_event_report(NTWK_TRANS_EVT_CONNECTED, ...)
```

<a id="id13"></a>

### 6\. 通道停止流程

```
应用调用 ntwk_trans_chan_stop(NTWK_TRANS_CHAN_VIDEO)
    ↓
调用 ntwk_in_stop(chan_type)
    ↓
调用传输服务的停止回调 (如 ntwk_tcp_video_chan_stop)
    ↓
更新通道状态: state = NTWK_TRANS_CHAN_STOP
    ↓
等待接收线程退出
    ↓
关闭Socket / 释放资源
    ↓
上报事件: ntwk_msg_event_report(NTWK_TRANS_EVT_STOP, ...)
```

<a id="bk"></a>

## BK集成的传输方案

BK Network Transfer 已集成三种典型传输方案，涵盖局域网和公网场景：

<a id="tcp"></a>

### TCP 传输方案

**实现文件**：

- `bk_network_service/bk_ntwk_tcp_service/bk_tcp_service.c`
- `bk_network_service/bk_ntwk_tcp_service/ntwk_tcp_service.c`

**适用场景**：

- 局域网内音视频传输
- 对数据可靠性要求高的应用
- 网络质量稳定的环境

**技术特点**：

- 基于 LwIP TCP Socket 实现
- 支持 TCP Keepalive 机制检测连接状态
- 三个独立通道使用不同端口：

  - 控制通道：7100
  - 视频通道：7150
  - 音频通道：7140
- 支持大数据包的分片传输
- 保证数据可靠送达（自动重传）

**MTU配置**：1460 字节 (NTWK\_TRANS\_TCP\_DATA\_MAX\_SIZE)

**Keepalive参数**：

```
// 控制通道
#define NTWK_TRANS_CTRL_CHAN_KEEPALIVE_IDLE_TIME   60  // 空闲60秒开始探测
#define NTWK_TRANS_CTRL_CHAN_KEEPALIVE_INTERVAL     5  // 探测间隔5秒
#define NTWK_TRANS_CTRL_CHAN_KEEPALIVE_COUNT        3  // 探测3次失败判定断开

// 视频/音频通道
#define NTWK_TRANS_VIDEO_CHAN_KEEPALIVE_IDLE_TIME  30  // 空闲30秒开始探测
```

**服务初始化示例**：

```
bk_err_t bk_tcp_trans_service_init(char *service_name)
{
    // 1. 初始化核心上下文
    ntwk_trans_ctxt_init(NULL);

    // 2. 初始化TCP底层资源
    ntwk_tcp_init(NTWK_TRANS_CHAN_CTRL);
    ntwk_tcp_init(NTWK_TRANS_CHAN_VIDEO);
    ntwk_tcp_init(NTWK_TRANS_CHAN_AUDIO);

    // 3. 获取上下文并配置服务名
    ctxt = ntwk_trans_get_ctxt();
    strncpy(ctxt->service_name, service_name, ...);

    // 4. 配置视频通道（示例）
    ctxt->video_chan->type = NTWK_TRANS_CHAN_VIDEO;
    ctxt->video_chan->send = ntwk_tcp_video_send_packet;

    // 使用Pack模块
    ctxt->video_chan->pack = ntwk_pack_video_pack;
    ctxt->video_chan->unpack = ntwk_pack_video_unpack;

    // 使用Fragment模块
    ctxt->video_chan->fragment = ntwk_fragment_video_fragment;
    ctxt->video_chan->unfragment = ntwk_fragment_video_unfragment;

    // 注册启动/停止回调
    ntwk_in_register_video_start_cb(ntwk_tcp_video_chan_start);
    ntwk_in_register_video_stop_cb(ntwk_tcp_video_chan_stop);

    // 启动Pack模块
    ntwk_pack_register_recv_cb(NTWK_TRANS_CHAN_VIDEO,
                               ntwk_trans_pack_rx_handler);
    ntwk_pack_chan_start(NTWK_TRANS_CHAN_VIDEO, 1460, 1460);

    // 启动Fragment模块
    ntwk_fragment_register_recv_cb(NTWK_TRANS_CHAN_VIDEO,
                                   ntwk_trans_fragment_rx_handler);
    int payload_size = 1460 - 16 - 4;  // MTU - Pack头 - Frag头
    ntwk_fragment_start(NTWK_TRANS_CHAN_VIDEO, payload_size, NULL);

    // 注册接收处理函数
    ntwk_tcp_video_register_receive_cb(ntwk_trans_video_recv_handler);

    return BK_OK;
}
```

<a id="udp"></a>

### UDP 传输方案

**实现文件**：

- `bk_network_service/bk_ntwk_udp_service/bk_udp_service.c`
- `bk_network_service/bk_ntwk_udp_service/ntwk_udp_service.c`

**适用场景**：

- 实时性要求高的音视频传输
- 对少量丢包容忍度高的应用
- 广播/组播场景

**技术特点**：

- 基于 LwIP UDP Socket 实现
- 无连接开销，传输延迟低
- 三个独立通道使用不同端口：

  - 控制通道：7100
  - 视频通道：7180
  - 音频通道：7170
- 支持数据包分片与重组（必须使用Fragment模块）
- 可配置视频丢帧策略优化带宽利用

**MTU配置**：1472 字节 (NTWK\_TRANS\_UDP\_DATA\_MAX\_SIZE)

**与TCP的主要区别**：

```
// UDP服务初始化关键配置

// 视频通道：必须启用Fragment模块（UDP无重传机制）
ctxt->video_chan->fragment = ntwk_fragment_video_fragment;
ctxt->video_chan->unfragment = ntwk_fragment_video_unfragment;

// 计算UDP有效载荷
payload_size = 1472 - 16 - 4;  // UDP MTU更大
ntwk_fragment_start(NTWK_TRANS_CHAN_VIDEO, payload_size, NULL);

// UDP视频通道需要配置丢帧策略（可选）
ctxt->video_chan->drop_check = ntwk_video_drop_check_default;
```

<a id="cs2-p2p"></a>

### CS2 P2P 传输方案

**实现文件**：

- `bk_network_service/bk_ntwk_cs2_service/bk_cs2_service.c`
- `bk_network_service/bk_ntwk_cs2_service/ntwk_cs2_service.c`

**适用场景**：

- 跨公网的远程音视频传输
- 需要 NAT 穿透的应用
- 移动端远程监控
- 外网访问家庭摄像头

**技术特点**：

- 基于 CS2 P2P 协议实现 NAT 穿透
- 支持服务器中继模式（当穿透失败时）
- 集成 P2P 会话管理和连接维护
- 自适应网络环境，动态调整传输策略
- 支持加密传输（可选）

**MTU配置**：1024 字节 (NTWK\_TRANS\_DATA\_MAX\_SIZE)

**配置选项**：

```
#define CONFIG_CS2_P2P_SERVER  1  // 使能服务器模式
#define CONFIG_CS2_P2P_CLIENT  1  // 使能客户端模式
```

**P2P连接流程**：

```
1. 设备端向CS2服务器注册（提供设备ID）
2. 客户端通过设备ID连接CS2服务器
3. CS2服务器协助NAT穿透（交换外网地址和端口）
4. 尝试P2P直连
5. 若直连失败，使用服务器中继模式
6. 建立数据传输通道
```

<a id="id14"></a>

### 方案对比总结

| 特性 | TCP | UDP | CS2 P2P |
| --- | --- | --- | --- |
| 可靠性 | 高（保证送达） | 低（可能丢包） | 中（可配置） |
| 实时性 | 中 | 高 | 中 |
| NAT穿透 | 不支持 | 不支持 | 支持 |
| 适用网络 | 局域网 | 局域网 | 公网/局域网 |
| MTU | 1460 | 1472 | 1024 |
| CPU开销 | 中 | 低 | 高 |
| Fragment模块 | 可选 | 可选 | 可选 |
| 应用场景 | 监控 | 实时对讲、直播 | 远程监控 |

<a id="id15"></a>

## 自定义传输方案开发指南

本章节以 BK 已集成的 CS2 P2P 传输方案为参考，说明如何使用 Network Transfer 组件对接自定义传输协议实现多媒体传输。

<a id="id16"></a>

### 开发流程概述

使用 Network Transfer 组件开发自定义传输方案的核心思路：**实现底层传输协议，并通过标准接口对接 Network Transfer 框架**，框架会自动处理数据打包、分片、丢帧等功能。

```
开发步骤：
1. 实现底层传输协议收发
2. 实现三个通道的发送回调函数
3. 实现通道启动/停止回调
4. 创建服务初始化函数（对接Network Transfer）
5. 应用层使用统一API
```

<a id="id17"></a>

### 组件对接架构

以CS2方案为例，展示组件对接层次：

<a id="id33"></a>
![network transfer integration layer design](../../../../../_assets/5938c0b167f20e867ac0-ntwk_integration_layer.png)


Figure 2\. Network Transfer 组件对接架构图

<a id="id18"></a>

### 必须实现的接口

参考CS2的接口签名，自定义传输方案需要实现以下回调函数：

**1\. 通道发送函数（必须实现）**

```
// 控制通道发送（签名参考：ntwk_cs2_p2p_ctrl_send）
int your_ctrl_send(uint8_t *data, uint32_t length);

// 视频通道发送（签名参考：ntwk_cs2_video_send_packet）
int your_video_send(uint8_t *data, uint32_t length,
                    image_format_t video_type);

// 音频通道发送（签名参考：ntwk_cs2_audio_send_packet）
int your_audio_send(uint8_t *data, uint32_t length,
                    audio_enc_type_t audio_type);
```

**2\. 通道生命周期回调（必须实现）**

```
// 控制通道启动（签名参考：ntwk_cs2_ctrl_chan_start）
bk_err_t your_ctrl_chan_start(void *param);
bk_err_t your_ctrl_chan_stop(void);

// 视频通道启动（签名参考：ntwk_cs2_video_chan_start）
bk_err_t your_video_chan_start(void *param);
bk_err_t your_video_chan_stop(void);

// 音频通道启动（签名参考：ntwk_cs2_audio_chan_start）
bk_err_t your_audio_chan_start(void *param);
bk_err_t your_audio_chan_stop(void);
```

**3\. 接收数据处理（在接收线程中调用）**

```
// 在底层接收线程中调用Network Transfer的handler
void your_receive_thread(void)
{
    while (is_running) {
        len = your_protocol_recv(buffer, size);
        if (len > 0) {
            // 根据通道类型调用对应的handler
            // Network Transfer会自动unpack和unfragment
            ntwk_trans_video_recv_handler(buffer, len);  // 视频
            ntwk_trans_audio_recv_handler(buffer, len);  // 音频
            ntwk_trans_ctrl_recv_handler(buffer, len);   // 控制
        }
    }
}
```

<a id="id19"></a>

### 服务初始化对接

参考 CS2 的 `bk_cs2_trans_service_init()` 实现，关键步骤如下：

```
bk_err_t your_trans_service_init(char *service_name)
{
    ntwk_trans_ctxt_t *ctxt = NULL;

    // 1. 初始化Network Transfer核心框架
    ntwk_trans_ctxt_init(NULL);

    // 2. 初始化底层传输协议
    your_protocol_init();

    // 3. 获取上下文并配置服务名
    ctxt = ntwk_trans_get_ctxt();
    strncpy(ctxt->service_name, service_name, ...);

    // 4. 配置控制通道
    ctxt->cntrl_chan->send = your_ctrl_send;           // 发送回调
    ctxt->cntrl_chan->pack = ntwk_pack_ctrl_pack;      // 使用Pack模块
    ctxt->cntrl_chan->unpack = ntwk_pack_ctrl_unpack;

    ntwk_in_register_ctrl_start_cb(your_ctrl_chan_start);  // 启动回调
    ntwk_in_register_ctrl_stop_cb(your_ctrl_chan_stop);    // 停止回调

    ntwk_pack_register_recv_cb(NTWK_TRANS_CHAN_CTRL,
                               ntwk_trans_pack_rx_handler);
    ntwk_pack_chan_start(NTWK_TRANS_CHAN_CTRL, MTU, MTU);

    // 5. 配置视频通道（类似控制通道，但需要Fragment模块）
    ctxt->video_chan->send = your_video_send;
    ctxt->video_chan->pack = ntwk_pack_video_pack;
    ctxt->video_chan->fragment = ntwk_fragment_video_fragment;      // 视频分片
    ctxt->video_chan->unfragment = ntwk_fragment_video_unfragment;  // 视频重组
    ctxt->video_chan->drop_check = ntwk_video_drop_check;           // 丢帧策略

    ntwk_in_register_video_start_cb(your_video_chan_start);
    ntwk_in_register_video_stop_cb(your_video_chan_stop);

    ntwk_pack_chan_start(NTWK_TRANS_CHAN_VIDEO, MTU, MTU);

    // 计算Fragment有效载荷（MTU - Pack头 - Fragment头）
    int payload_size = MTU - 16 - 4;
    ntwk_fragment_start(NTWK_TRANS_CHAN_VIDEO, payload_size, NULL);

    // 6. 配置音频通道（类似控制通道，通常不需要Fragment）
    ctxt->audio_chan->send = your_audio_send;
    ctxt->audio_chan->pack = ntwk_pack_audio_pack;
    // ...类似配置

    return BK_OK;
}
```

<a id="id20"></a>

### 应用层使用示例

使用自定义传输服务的完整流程：

```
// 1. 初始化传输服务
your_trans_service_init("your_service");

// 2. 注册事件和数据接收回调
ntwk_trans_register_msg_event_cb(on_event);
ntwk_trans_register_video_recv_cb(on_video_recv);
ntwk_trans_register_audio_recv_cb(on_audio_recv);
ntwk_trans_register_ctrl_recv_cb(on_ctrl_recv);

// 3. 启动通道
ntwk_trans_chan_start(NTWK_TRANS_CHAN_CTRL, &init_param);
ntwk_trans_chan_start(NTWK_TRANS_CHAN_VIDEO, NULL);
ntwk_trans_chan_start(NTWK_TRANS_CHAN_AUDIO, NULL);

// 4. 发送数据（Network Transfer自动处理pack/fragment/drop_check）
ntwk_trans_video_send(frame->frame, frame->length, IMAGE_H264);
ntwk_trans_audio_send(audio_data, audio_len, AUDIO_ENC_TYPE_G711A);
ntwk_trans_ctrl_send(cmd_data, cmd_len);

// 5. 接收回调中处理数据（已自动unpack/unfragment）
int on_video_recv(uint8_t *data, uint32_t length) {
    h264_decoder_input(data, length);  // 直接送入解码器
    return length;
}

// 6. 清理
ntwk_trans_chan_stop(NTWK_TRANS_CHAN_VIDEO);
ntwk_trans_chan_stop(NTWK_TRANS_CHAN_AUDIO);
ntwk_trans_chan_stop(NTWK_TRANS_CHAN_CTRL);
your_trans_service_deinit();
```

<a id="id21"></a>

### 关键设计要点

**1\. 必须调用的接收处理函数**

在底层接收线程中必须调用Network Transfer的handler：

```
// 接收线程中
ntwk_trans_video_recv_handler(buffer, len);  // 自动触发unpack->unfragment
ntwk_trans_audio_recv_handler(buffer, len);
ntwk_trans_ctrl_recv_handler(buffer, len);
```

**2\. 必须上报的状态事件**

在关键状态变化时调用 `ntwk_msg_event_report()`：

```
ntwk_msg_event_report(NTWK_TRANS_EVT_CONNECTED, 0, chan_type);   // 连接建立
ntwk_msg_event_report(NTWK_TRANS_EVT_DISCONNECTED, 0, chan_type); // 连接断开
ntwk_msg_event_report(NTWK_TRANS_EVT_STOP, 0, chan_type);         // 通道停止
```

**3\. 公共功能模块配置建议**

| 功能模块 | 使用建议 | 说明 |
| --- | --- | --- |
| Pack/Unpack | 强烈推荐 | 保证数据格式统一 |
| Fragment/Unfragment | 视频必须 | 处理大帧（I帧） |
| Video Drop Policy | 建议使用 | 优化带宽和性能 |
| Event Notification | 必须 | 状态通知应用层 |

**4\. 线程安全**

send回调可能被多个线程调用，需要保护共享资源（如连接句柄、会话ID等）。

**5\. 参考实现**

- CS2 服务：`bk_network_service/bk_ntwk_cs2_service/`
- TCP 服务：`bk_network_service/bk_ntwk_tcp_service/`
- UDP 服务：`bk_network_service/bk_ntwk_udp_service/`

<a id="id22"></a>

### 数据流向示意

**发送流程**：

```
编码器 → ntwk_trans_video_send() → drop_check → fragment → pack
→ your_video_send() → 底层协议 → 网络
```

**接收流程**：

```
网络 → 底层协议 → ntwk_trans_video_recv_handler() → unpack
→ unfragment → 用户回调 → 解码器
```

<a id="id23"></a>

## 使用示例

<a id="id24"></a>

### 基本使用流程

**1\. 初始化传输服务**

```
#include "network_transfer.h"
#include "bk_network_service/bk_ntwk_tcp_service/bk_tcp_service.h"

// 选择并初始化传输方案
bk_tcp_trans_service_init("tcp_service");   // TCP方案
// 或
// bk_udp_trans_service_init("udp_service"); // UDP方案
// bk_cs2_trans_service_init("cs2_service"); // CS2方案
```

**2\. 注册回调**

```
// 注册事件回调
ntwk_trans_register_msg_event_cb(event_callback);

// 注册数据接收回调
ntwk_trans_register_ctrl_recv_cb(ctrl_recv_callback);
ntwk_trans_register_video_recv_cb(video_recv_callback);
ntwk_trans_register_audio_recv_cb(audio_recv_callback);
```

**3\. 启动通道**

```
// 根据需要启动相应通道
ntwk_trans_chan_start(NTWK_TRANS_CHAN_CTRL, NULL);
ntwk_trans_chan_start(NTWK_TRANS_CHAN_VIDEO, NULL);
ntwk_trans_chan_start(NTWK_TRANS_CHAN_AUDIO, NULL);
```

**4\. 发送数据**

```
// 发送视频
ntwk_trans_video_send(video_data, video_len, IMAGE_H264);

// 发送音频
ntwk_trans_audio_send(audio_data, audio_len, AUDIO_ENC_TYPE_G711A);

// 发送控制命令
ntwk_trans_ctrl_send(ctrl_data, ctrl_len);
```

**5\. 停止和清理**

```
// 停止通道
ntwk_trans_chan_stop(NTWK_TRANS_CHAN_VIDEO);
ntwk_trans_chan_stop(NTWK_TRANS_CHAN_AUDIO);
ntwk_trans_chan_stop(NTWK_TRANS_CHAN_CTRL);

// 清理服务
bk_tcp_trans_service_deinit();  // 对应初始化的服务
```

<a id="id25"></a>

### 回调函数示例

```
// 事件回调
void event_callback(ntwk_trans_event_t *event)
{
    switch (event->code) {
        case NTWK_TRANS_EVT_START:
            BK_LOGI("APP", "通道 %d 启动\n", event->chan_type);
            break;
        case NTWK_TRANS_EVT_CONNECTED:
            BK_LOGI("APP", "通道 %d 已连接\n", event->chan_type);
            // 可以在这里开始发送数据
            break;
        case NTWK_TRANS_EVT_DISCONNECTED:
            BK_LOGI("APP", "通道 %d 断开连接\n", event->chan_type);
            // 可以在这里实现自动重连
            break;
        case NTWK_TRANS_EVT_STOP:
            BK_LOGI("APP", "通道 %d 停止\n", event->chan_type);
            break;
    }
}

// 视频接收回调
int video_recv_callback(uint8_t *data, uint32_t length)
{
    BK_LOGI("APP", "收到视频帧：%d字节\n", length);
    // 处理视频数据（如送入解码器）
    return length;
}

// 音频接收回调
int audio_recv_callback(uint8_t *data, uint32_t length)
{
    // 处理音频数据
    return length;
}

// 控制命令接收回调
int ctrl_recv_callback(uint8_t *data, uint32_t length)
{
    // 处理控制命令
    return length;
}
```

<a id="id26"></a>

## 常见问题

<a id="q1"></a>

### Q1: 视频传输出现花屏或卡顿？

**原因分析**：

- 网络丢包导致帧不完整
- MTU 设置过大导致IP层分片丢失
- 接收端重组超时
- 未使用Fragment模块

**解决方案**：

1. 视频通道必须启用Fragment模块：

```
ctxt->video_chan->fragment = ntwk_fragment_video_fragment;
ctxt->video_chan->unfragment = ntwk_fragment_video_unfragment;
```

2. 调整分片大小匹配网络MTU：

```
int payload = MTU - 16 - 4;  // MTU - Pack头 - Frag头
ntwk_fragment_start(NTWK_TRANS_CHAN_VIDEO, payload, NULL);
```

3. 使用TCP替代UDP（牺牲实时性换取可靠性）

<a id="q2"></a>

### Q2: 音视频不同步？

**原因分析**：

- 音频和视频通道延迟不一致
- 缺少时间戳同步机制

**解决方案**：

1. 启用Pack功能，利用时间戳同步：

```
ctxt->video_chan->pack = ntwk_pack_video_pack;
ctxt->audio_chan->pack = ntwk_pack_audio_pack;
```

2. 在应用层实现音视频同步队列，根据时间戳对齐播放

<a id="q3"></a>

### Q3: 内存泄漏问题？

**常见原因**：

- 分片重组后未调用free回调
- 发送失败后未释放缓冲区
- 通道停止时未完全清理资源

**排查方法**：

```
// 确保注册了Unfragment free回调
ntwk_trans_register_unfragment_free_cb(NTWK_TRANS_CHAN_VIDEO,
                                        my_free_callback);

// 定期打印内存使用情况
void print_mem_info(void) {
    uint32_t free_size = xPortGetFreeHeapSize();
    BK_LOGI("MEM", "Free: %d bytes\n", free_size);
}
```

<a id="q4"></a>

### Q4: 如何选择合适的传输方案？

**决策树**：

```
是否需要跨公网？
├─ 是 → 使用 CS2 P2P
└─ 否 → 是否要求高可靠性？
    ├─ 是 → 使用 TCP
    └─ 否 → 是否要求低延迟？
        ├─ 是 → 使用 UDP
        └─ 否 → 使用 TCP
```

**综合建议**：

- **监控应用**：TCP（局域网）/ CS2（公网）
- **对讲应用**：UDP（局域网）/ CS2（公网）

<a id="id27"></a>

## 注意事项

- 在调用其他API前必须先调用 `ntwk_trans_ctxt_init()` 初始化上下文
- 发送数据前需要先启动对应通道（等待 CONNECTED 事件）
- 确保在 `ntwk_trans_ctxt_deinit()` 前停止所有通道
- 回调函数中不应执行耗时操作，避免阻塞接收线程
- 视频通道必须使用Fragment模块处理大帧
- 分片功能的 malloc/send/free 回调必须成套配置
- 自定义传输方案务必正确上报状态事件
- 注意线程安全，send回调可能被多线程调用
- 合理设置线程栈大小（建议4KB以上），避免栈溢出
- 定期检查内存使用情况，防止内存泄漏

<a id="api"></a>

## API 参考

<a id="id28"></a>

### API 状态

| API | BK7258\_AP |
| --- | --- |
| `ntwk_trans_ctxt_init()` | Y |
| `ntwk_trans_ctxt_deinit()` | Y |
| `ntwk_trans_get_ctxt()` | Y |
| `ntwk_trans_chan_start()` | Y |
| `ntwk_trans_chan_stop()` | Y |
| `ntwk_trans_ctrl_send()` | Y |
| `ntwk_trans_video_send()` | Y |
| `ntwk_trans_audio_send()` | Y |
| `ntwk_trans_ctrl_recv_handler()` | Y |
| `ntwk_trans_video_recv_handler()` | Y |
| `ntwk_trans_audio_recv_handler()` | Y |
| `ntwk_trans_pack_rx_handler()` | Y |
| `ntwk_trans_fragment_rx_handler()` | Y |
| `ntwk_trans_register_msg_event_cb()` | Y |
| `ntwk_trans_register_ctrl_recv_cb()` | Y |
| `ntwk_trans_register_video_recv_cb()` | Y |
| `ntwk_trans_register_audio_recv_cb()` | Y |
| `ntwk_trans_register_unfragment_malloc_cb()` | Y |
| `ntwk_trans_register_unfragment_send_cb()` | Y |
| `ntwk_trans_register_unfragment_free_cb()` | Y |

<a id="id29"></a>

### 宏定义和配置

| 宏名称 | 说明 |
| --- | --- |
| NTWK\_TRANS\_SERVICE\_NAME\_LEN | 服务名称最大长度（100字节） |
| NTWK\_TRANS\_TCP\_DATA\_MAX\_SIZE | TCP MTU大小（1460字节） |
| NTWK\_TRANS\_UDP\_DATA\_MAX\_SIZE | UDP MTU大小（1472字节） |
| NTWK\_TRANS\_DATA\_MAX\_SIZE | 通用MTU大小（1024字节） |
| NTWK\_TRANS\_CMD\_PORT | 控制通道端口（7100） |
| NTWK\_TRANS\_TCP\_VIDEO\_PORT | TCP视频端口（7150） |
| NTWK\_TRANS\_UDP\_VIDEO\_PORT | UDP视频端口（7180） |
| CONFIG\_CS2\_P2P\_SERVER | 使能CS2 P2P服务器模式 |
| CONFIG\_CS2\_P2P\_CLIENT | 使能CS2 P2P客户端模式 |

<a id="id30"></a>

### API 函数参考

详细的 API 函数定义请参考头文件：

- 核心接口：`ap/components/bk_network_transfer/network_transfer.h`
- 内部接口：`ap/components/bk_network_transfer/network_transfer_internal.h`
- 类型定义：`ap/components/bk_network_transfer/network_type.h`

<a id="id31"></a>

### 类型定义

详细的类型定义请参考头文件：`ap/components/bk_network_transfer/network_type.h`
