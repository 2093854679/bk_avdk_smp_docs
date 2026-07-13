# 多核通讯-IPC通讯接口



## 1 功能概述


- IPC通讯接口基于Mailbox


## 2 AP侧代码路径

> - 测试代码路径:
>   :   `ap\middleware\driver\mailbox\bk_api_ipc_test.c`
> - 驱动源码路径：
>   :   `ap\middleware\driver\mailbox\bk_api_ipc.c`


## 3 CP侧代码路径

> - 测试代码路径:
>   :   `cp\middleware\driver\mailbox\bk_api_ipc_test.c`
> - 驱动源码路径：
>   :   `cp\middleware\driver\mailbox\bk_api_ipc.c`


## 4 IPC通讯接口


```
#define MIPC_CHAN_SEND_FLAG_SYNC        (1 << 0)
#define MIPC_CHAN_HAND_FLAG_ASYNC       (1 << 1)
#define MIPC_CHAN_SEND_FLAG_DEFAULT     (0)

#define BK_IPC_CHANNEL_DEF(section_name)                  \
    extern bk_ipc_t section_name;                         \

#define BK_IPC_CHANNEL_REGISTER(_channel, _route, _rx_cb, _param, _tx_cb)                                  \
    bk_ipc_t _channel;                                                                                \
    BK_SECTION_ITEM_REGISTER(ipc_chan_reg, const bk_ipc_chan_cfg_t _channel##section) =             \
    {                                                                                                   \
                .ipc = &(_channel),                                                                     \
                .route = (_route),                                                                      \
                .name = #_channel,                                                                      \
                .rx_cb = _rx_cb,                                                                        \
                .param = _param,                                                                        \
                .tx_cb = _tx_cb,                                                                        \
    }

typedef uint32_t (*bk_ipc_rx_cb)(uint8_t *data, uint32_t size, void *param, ipc_obj_t ipc_obj);
typedef uint32_t (*bk_ipc_tx_cb)(ipc_obj_t ipc_obj);

int bk_ipc_init(void);
int bk_ipc_send(bk_ipc_t *ipc, void *data, uint32_t size, uint32_t flags, uint32_t *result);

```

描述：
:   - AP和CP子系统通过IPC接口通讯, 需要分别调用bk_ipc_init初始化

    - 然后通过BK_IPC_CHANNEL_DEF申明应用的逻辑通路

    - 接着通过BK_IPC_CHANNEL_REGISTER注册rx和tx的callback


## 5 AP侧使用示例


```
//0. 申明应用的逻辑通路, 定义rx, tx callback函数
BK_IPC_CHANNEL_DEF(ui_ipc_test);

uint32_t ap_rx_callback(uint8_t *data, uint32_t size, void *param, ipc_obj_t ipc_obj)
{
    bk_mem_dump_ex("AP Rx data:", data, size);

    // 用户逻辑处理
    // ...

    return ret;
}

uint32_t ap_tx_callback(ipc_obj_t ipc_obj)
{
    // 用户可以在这里释放上层申请的内存
    // ...

    return ret;
}

//1. 注册rx和tx的callback函数
BK_IPC_CHANNEL_REGISTER(ui_ipc_test, IPC_ROUTE_CPU0_CPU1, ap_rx_callback, NULL, ap_tx_callback);

//2. 异步发送：
ret = bk_ipc_send(&ui_ipc_test, (uint8_t *)data, sizeof(data), 0, 0);

//3. 同步发送：
ret = bk_ipc_send(&ui_ipc_test, (uint8_t *)data, sizeof(data), MIPC_CHAN_SEND_FLAG_SYNC, 0);

```


## 6 CP侧使用示例


```
//0. 申明应用的逻辑通路
BK_IPC_CHANNEL_DEF(ui_ipc_test);

uint32_t cp_rx_callback(uint8_t *data, uint32_t size, void *param, ipc_obj_t ipc_obj)
{
    bk_mem_dump_ex("CP Rx data:", data, size);

    // 用户逻辑处理
    // ...

    return ret;
}

uint32_t cp_tx_callback(ipc_obj_t ipc_obj)
{
    // 用户可以在这里释放上层申请的内存
    // ...

    return ret;
}

//1. 注册rx和tx的callback函数
BK_IPC_CHANNEL_REGISTER(ui_ipc_test, IPC_ROUTE_CPU0_CPU1, cp_rx_callback, NULL, cp_tx_callback);

//2. 异步发送：
ret = bk_ipc_send(&ui_ipc_test, (uint8_t *)data, sizeof(data), 0, 0);

//3. 同步发送：
ret = bk_ipc_send(&ui_ipc_test, (uint8_t *)data, sizeof(data), MIPC_CHAN_SEND_FLAG_SYNC, 0);

```


## 7 UT测试用例

以app工程为例, 可以通过ipc命令运行CP侧IPC通讯接口的单元测试用例:


```
$ ipc

Unity test run 1 of 1ap0:MIPC-UT:I(1071873):Rx: [Sync Hello From CPU: 0, @time: 671642780], size: 128
MIPC-UT:I(1072043):Rx: [Ack From CPU: 1, @time: 1071873], size: 128
ap0:MIPC-UT:I(1071873):Rx: [Sync Hello From CPU: 0, @time: 0], size: 128
MIPC-UT:I(1072043):Rx: [Ack From CPU: 1, @time: 1071873], size: 128
ap0:MIPC-UT:I(1071874):Rx: [Sync Hello From CPU: 0, @time: 0], size: 128
MIPC-UT:I(1072043):Rx: [Ack From CPU: 1, @time: 1071874], size: 128
ap0:MIPC-UT:I(1071874):Rx: [Sync Hello From CPU: 0, @time: 0], size: 128
MIPC-UT:I(1072044):Rx: [Ack From CPU: 1, @time: 1071874], size: 128
ap0:MIPC-UT:I(1071874):Rx: [Sync Hello From CPU: 0, @time: 0], size: 128
MIPC-UT:I(1072044):Rx: [Ack From CPU: 1, @time: 1071874], size: 128
ap0:MIPC-UT:I(1071875):Rx: [Async Hello From CPU: 0, @time: 671642788], size: 128
MIPC-UT:I(1072045):Rx: [Ack From CPU: 1, @time: 1071875], size: 128
ap0:MIPC-UT:I(1071975):Rx: [Async Hello From CPU: 0, @time: 3758153728], size: 128
MIPC-UT:I(1072145):Rx: [Ack From CPU: 1, @time: 1071975], size: 128
ap0:MIPC-UT:I(1072075):Rx: [Async Hello From CPU: 0, @time: 3758153728], size: 128
MIPC-UT:I(1072245):Rx: [Ack From CPU: 1, @time: 1072075], size: 128
ap0:MIPC-UT:I(1072174):Rx: [Async Hello From CPU: 0, @time: 3758153728], size: 128
MIPC-UT:I(1072345):Rx: [Ack From CPU: 1, @time: 1072174], size: 128
ap0:MIPC-UT:I(1072274):Rx: [Async Hello From CPU: 0, @time: 3758153728], size: 128
MIPC-UT:I(1072445):Rx: [Ack From CPU: 1, @time: 1072274], size: 128


-----------------------
2 Tests 0 Failures 0 Ignored
OK

```

以app工程为例, 可以通过ap_cmd ipc命令运行AP侧IPC通讯接口的单元测试用例:


```
$ ap_cmd ipc

Unity test run 1 of 1MIPC-UT:I(1064699):Rx: [Sync Hello From CPU: 1, @time: 671206708], size: 128
MIPC-UT:I(1064699):Rx: [Sync Hello From CPU: 1, @time: 0], size: 128
MIPC-UT:I(1064700):Rx: [Sync Hello From CPU: 1, @time: 0], size: 128
MIPC-UT:I(1064700):Rx: [Sync Hello From CPU: 1, @time: 0], size: 128
MIPC-UT:I(1064700):Rx: [Sync Hello From CPU: 1, @time: 0], size: 128
MIPC-UT:I(1064700):Rx: [Async Hello From CPU: 1, @time: 671206716], size: 128
MIPC-UT:I(1064799):Rx: [Async Hello From CPU: 1, @time: 3758153728], size: 128
MIPC-UT:I(1064899):Rx: [Async Hello From CPU: 1, @time: 3758153728], size: 128
MIPC-UT:I(1064999):Rx: [Async Hello From CPU: 1, @time: 3758153728], size: 128
MIPC-UT:I(1065099):Rx: [Async Hello From CPU: 1, @time: 3758153728], size: 128


-----------------------
2 Tests 0 Failures 0 Ignored
OK

```
