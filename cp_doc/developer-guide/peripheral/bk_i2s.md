---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_i2s.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="i2s"></a>

# I2S 使用指南

<a id="id1"></a>

## 概述

I2S/PCM总线接口是一个双向的4线接口，主要用于音频数据的传输。该接口可以支持I2S模式的各种格式，如Philips、Left Justified、Right Justified；还可以支持PCM模式的各种格式，如Short Sync、Long Sync、GCI、IDL等。

模块支持下述工作模式:

I2S (Philips)
:   在此工作模式下信号传输时序图如 `图1` 所示:

<a id="id8"></a>
![Philips_mode_time_sequence_diagram](../../../../_assets/d1f64488b77a3e3cde19-i2s_Philips.png)


Figure 1\. Philips mode time sequence diagram

Left Justified
:   在此工作模式下信号传输时序图如 `图2` 所示:

<a id="id9"></a>
![Left Justified mode time sequence diagram](../../../../_assets/1abb46230f92502eb99e-i2s_Left_Justified.png)


Figure 2\. Left Justified mode time sequence diagram

Right Justified
:   在此工作模式下信号传输时序图如 `图3` 所示:

<a id="id10"></a>
![Right Justified mode time sequence diagram](../../../../_assets/aa50935192c88fafb0f6-i2s_RightJustified.png)


Figure 3\. Right Justified mode time sequence diagram

Short Frame Sync
:   在此工作模式下信号传输时序图如 `图4` 所示:

<a id="id11"></a>
![Short Frame Sync mode time sequence diagram](../../../../_assets/d0f65a45cd6618033f1b-i2s_ShortSyncFrame.png)


Figure 4\. Short Frame Sync mode time sequence diagram

Long Frame Sync
:   在此工作模式下信号传输时序图如 `图5` 所示:

<a id="id12"></a>
![Long Frame Sync mode time sequence diagram](../../../../_assets/ea2f73b5188bcc781d7c-i2s_LongSyncFrame.png)


Figure 5\. Long Frame Sync mode time sequence diagram

Normal 2B\+D
:   在此工作模式下信号传输时序图如 `图6和图7` 所示:

<a id="id13"></a>
![Normal 2B+D mode time sequence diagram](../../../../_assets/da51eb5b2fa210c9948b-i2s_Normal2BD_D0.png)


Figure 6\. Normal 2B\+D mode time sequence diagram

<a id="id14"></a>
![Normal 2B+D mode time sequence diagram](../../../../_assets/8281bcb0ef368a141a85-i2s_Normal2BD_Dx.png)


Figure 7\. Normal 2B\+D mode time sequence diagram

Delay 2B\+D
:   在此工作模式下信号传输时序图如 `图8和图9` 所示:

<a id="id15"></a>
![Delay 2B+D mode time sequence diagram](../../../../_assets/a3d1096f40a8755f1053-i2s_Delay2BD_D0.png)


Figure 8\. Delay 2B\+D mode time sequence diagram

<a id="id16"></a>
![Delay 2B+D mode time sequence diagram](../../../../_assets/e1e838241b4377a60ffb-i2s_Delay2BD_Dx.png)


Figure 9\. Delay 2B\+D mode time sequence diagram

<a id="id2"></a>

## 硬件连接

I2S通讯的引脚说明如下：

| GPIO | in/out | 说明 |
| --- | --- | --- |
| SCLK | in\&out | I2S工作的时钟信号，也称为BCLK |
| LRCK | in\&out | 左右声道时钟，也称WS（PCM中是sync时钟） |
| DIN | in | 数据输入引脚 |
| DOUT | out | 数据输出引脚 |

<a id="id3"></a>

## I2S调试注意事项

> 1. I2S通讯时，两个设备分别为 `master` 和 `slave`， `SCLK` 和 `LRCK` 由 `master` 提供。
> 2. 调用接口前需要确认设备的角色、工作模式、采样率、声道数、位宽、数据发送顺序、数据存储格式等信息，根据这些信息来配置I2S。
> 3. 针对I2S四种典型的工作模式，驱动提供了默认的配置，你可以在默认配置的基础上根据实际应用调整。
> 4. slave的配置需要和master保持一致，如果不确定master的工作模式，可以通过逻辑分析仪抓取master的引脚波形进行分析。

<a id="id4"></a>

## I2S 接口使用说明

I2S接口的使用流程如下：

> 1. 调用 `bk_i2s_driver_init` 接口初始化I2S的驱动
> 2. 调用 `bk_i2s_init` 接口初始化并配置选择的I2S Group
> 3. 调用 `bk_i2s_chl_init` 接口初始化指定的通道
> 4. 调用 `bk_i2s_start` 接口启动I2S的通讯
> 5. 在通道注册的回调函数里向通道发送待发的数据，或读取接收到的数据

接下来以I2S模式下的收发为例，对接口的配置使用进行详细说明。

主机工作在I2S模式下发送数据示例如下：

```
/* 创建通道的TX回调，并在回调中不断向通道发送固定的数据 */
static int ch1_tx_data_handle_cb(uint32_t size)
{
        ring_buffer_write(ch1_tx_rb, ch1_temp, size);

        return size;
}

/* 采用默认的I2S配置 */
i2s_config_t i2s_config = DEFAULT_I2S_CONFIG();
bk_err_t ret = BK_OK;
uint32_t size = 0;

uint8_t *ch1_temp = os_malloc(320);
os_memset(ch1_temp, 0xF1, 320);

//init i2s driver
bk_i2s_driver_init();

//init i2s configure
i2s_config.samp_rate = I2S_SAMP_RATE_48000;
bk_i2s_init(I2S_GPIO_GROUP_2, &i2s_config);
os_printf("init i2s driver and config successful \r\n");

/* 配置第一个通道用于发送数据，每帧数据的size为（640/2）字节 */
ret = bk_i2s_chl_init(I2S_CHANNEL_1, I2S_TXRX_TYPE_TX, 640, ch1_tx_data_handle_cb, &ch1_tx_rb);
if (ret != BK_OK) {
        os_printf("bk_i2s_chl_init fail \n");
        return;
}

uint8_t *temp_data = (uint8_t *)os_malloc(640);
os_memset(temp_data, 0x00, 640);
/* 开始发送前先向通道灌满数据 */
size = ring_buffer_write(ch1_tx_rb, temp_data, 640);
os_printf("ring_buffer_write, size: %d \n", size);
os_free(temp_data);
/* 启动I2S开始发送数据 */
bk_i2s_start();
```

I2S的配置信息如下：

```
    #define DEFAULT_I2S_CONFIG() {                     \
    .role = I2S_ROLE_MASTER,                       \
    .work_mode = I2S_WORK_MODE_I2S,                \
    .lrck_invert = I2S_LRCK_INVERT_DISABLE,        \
    .sck_invert = I2S_SCK_INVERT_DISABLE,          \
    .lsb_first_en = I2S_LSB_FIRST_DISABLE,         \
    .sync_length = 0,                              \
    .data_length = 16,                             \
    .pcm_dlength = 0,                              \
    .store_mode = I2S_LRCOM_STORE_LRLR,            \
    .samp_rate = I2S_SAMP_RATE_8000,               \
    .pcm_chl_num = 2,                              \
}
```

备注

- `lrck_invert` 用于配置 `LRCK` 信号是否反转（仅在传输双声道数据的I2S工作模式下有效），默认情况下 `LRCK` 的低电平表示右声道，高电平表示左声道。
- `sck_invert` 用于配置\`\`SCLK\`\` 信号是否反转，默认情况下输入数据在 `SCLK` 的上升沿采样，输出数据在 `SCLK` 的下降沿变化。
- `lsb_first_en` 用于配置是否数据的发送时序，如果使能则先发送低位再发送高位，默认情况下先发送高位再发送低位。
- `sync_length` 用于配置同步的bit位数（仅在PCM工作模式下有效），I2S模式下可忽略。
- `data_length` 用于配置单声道数据的位数，需要注意是单声道的位数。
- `pcm_dlength` 用于配置PCM数据的位数（仅在PCM工作模式下有效），I2S模式下可忽略。
- `store_mode` 用于配置通道内数据的存储模式，I2S\_LRCOM\_STORE\_16R16L：左右声道数据拼成一个32bit同时写入PCM\_DAT中，低16bit对应左声道，高16bit对应右声道，即{R,L}-\>{R,L}-\>……（仅当数据长度小于16时才能配置此模式）。I2S\_LRCOM\_STORE\_LRLR：左右声道数据按时间顺序交替写入PCM\_DAT中，即L-\>R-\>L-\>R-\>…… 。

以下示例展示I2S从机模式接收数据的主要工作流程：

```
#define I2S_RX_RING_BUFFER_SIZE  640
#define I2S_RX_CHUNK_SIZE        (I2S_RX_RING_BUFFER_SIZE / 2)

static RingBufferContext *s_i2s_rx_rb = NULL;
static uint8_t s_i2s_rx_data[I2S_RX_CHUNK_SIZE];

/* DMA每接收半个RingBuffer后调用该回调。 */
static int i2s_rx_data_callback(uint32_t size)
{
        if (size > sizeof(s_i2s_rx_data)) {
                size = sizeof(s_i2s_rx_data);
        }

        return (int)ring_buffer_read(s_i2s_rx_rb, s_i2s_rx_data, size);
}

static bk_err_t i2s_rx_example_start(void)
{
        i2s_config_t i2s_config = DEFAULT_I2S_CONFIG();
        bk_err_t ret;

        /* 1. 初始化I2S驱动。 */
        ret = bk_i2s_driver_init();
        if (ret != BK_OK) {
                return ret;
        }

        /* 2. 将Group 0配置为48 kHz I2S从机。 */
        i2s_config.role = I2S_ROLE_SLAVE;
        i2s_config.samp_rate = I2S_SAMP_RATE_48000;
        ret = bk_i2s_init(I2S_GPIO_GROUP_0, &i2s_config);
        if (ret != BK_OK) {
                bk_i2s_driver_deinit();
                return ret;
        }

        /* 3. 配置通道1及其RX RingBuffer。 */
        ret = bk_i2s_chl_init(I2S_CHANNEL_1,
                              I2S_TXRX_TYPE_RX,
                              I2S_RX_RING_BUFFER_SIZE,
                              i2s_rx_data_callback,
                              &s_i2s_rx_rb);
        if (ret != BK_OK) {
                bk_i2s_deinit();
                bk_i2s_driver_deinit();
                return ret;
        }

        /* 4. 启动I2S及RX DMA。 */
        ret = bk_i2s_start();
        if (ret != BK_OK) {
                bk_i2s_chl_deinit(I2S_CHANNEL_1, I2S_TXRX_TYPE_RX);
                bk_i2s_deinit();
                bk_i2s_driver_deinit();
        }

        return ret;
}

static void i2s_rx_example_stop(void)
{
        bk_i2s_stop();
        bk_i2s_chl_deinit(I2S_CHANNEL_1, I2S_TXRX_TYPE_RX);
        bk_i2s_deinit();
        bk_i2s_driver_deinit();
}
```

`I2S_RX_RING_BUFFER_SIZE` 表示RX RingBuffer的总字节数，每次DMA回调处理其中一半。回调运行在DMA完成中断上下文中，应仅搬运数据或通知其他任务，避免在回调中执行阻塞操作或输出大量日志。

<a id="id5"></a>

## 参考链接

> API 参考 : @api-reference/peripheral/bk\_i2s.html 介绍I2S API接口
>
> [用户开发指南 :](bk_i2s.md) 介绍I2S调试开发流程
>
> [示例 :](../../examples/peripheral/bk_i2s.md) 介绍I2S测试demo的使用
