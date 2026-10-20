---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/cli/bluetooth/ble.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ble-cli"></a>

# BLE Cli

<a id="id1"></a>

## 1、功能概述

> 为了便于验证BLE相关的功能，为此设计了一系列AT CMD。所有BLE AT CMD命令以 `AT+` 开头，后接具体命令和参数。如果命令执行成功，则返回 `CMDRSP:OK`。如果命令执行失败，则返回 `CMDRSP:ERROR`。

<a id="id2"></a>

## 2、代码路径

> 路径: `\components\bk_bluetooth\at\bk_at_ble.c`

<a id="cli"></a>

## 3、cli命令简介

支持的命令如下:

> 1.AT\+BLEADVPARAM
> :   - 功能说明
>       :   用来设置广播参数（包括传统广播、扩展广播和周期性广播）
>     - 命令格式
>       :   AT\+BLEADVPARAM\=param1,param2,param3,param4,param5,param6,param7,param8
>
>           |  |  |
>           | --- | --- |
>           | param1 | adv channel map |
>           | param2 | Minimum advertising interval  Range: 0x000020 to 0xFFFFFF(Time \= N \* 0.625 ms) |
>           | param3 | Maximum advertising interval  Range: 0x000020 to 0xFFFFFF(Time \= N \* 0.625 ms) |
>           | param4 | Own\_Address\_Type  0x00 : Public Device Address  0x01 : Random Device Address  0x02 : Resolvable Private Address,if no IRK use the public address  0x03 : Resolvable Private Address,if no IRK use the random address |
>           | param5 | adv\_type  0x00 : Legacy advertising  0x01 : Extended advertising  0x02 : Periodic advertising |
>           | param6 | adv\_properties(Bit number)  0 : Connectable advertising  1 : Scannable advertising  2 : Directed advertising  3 : High Duty Cycle Directed Connectable advertising  4 : Use legacy advertising PDUs  5 : Omit advertiser’s address from all PDUs(“anonymous advertising”)  6 : Include TxPower in the extended header of the advertising PDU |
>           | param7 | Primary\_Advertising\_PHY  0x01 : Primary advertisement PHY is LE 1M  0x03 : Primary advertisement PHY is LE Coded |
>           | param8 | Secondary\_Advertising\_PHY  0x01 : Secondary advertisement PHY is LE 1M  0x02 : Secondary advertisement PHY is LE 2M  0x03 : Secondary advertisement PHY is LE Coded |
>     - 测试用例
>       :   设置传统adv参数：`AT+BLEADVPARAM=7,120,160,0,0,3,1,1`
>
>           设置扩展adv参数：`AT+BLEADVPARAM=7,120,160,0,1,1,1,1`
>
>           设置周期adv参数：`AT+BLEADVPARAM=7,120,160,0,2,0,1,3`
>
> 2.AT\+BLEADVDATA
> :   - 功能说明
>       :   这条AT命令用来设置广播的数据，adv包括传统ADV和ext\_ADV
>     - 命令格式
>       :   AT\+BLEADVDATA\=param1,param2
>
>           |  |  |
>           | --- | --- |
>           | param1 | Advertising data, the data format is shown in Figure 1 |
>           | param2 | Advertising\_Data\_Length  Range: 0x00 to 0x1F |
>
>           <a id="id3"></a>
>           ![adv_data_format](../../../../../_assets/afb3f877193da6883cc4-adv_data_format.png)
>
>
>           Figure 1\. Advertising and Scan Response data format
>
>           常用AD type见下表：
>
>           | Type Value | Description |
>           | --- | --- |
>           | 0x01 | «Flags» |
>           | 0x02 | «Incomplete List of 16-bit Service Class UUIDs» |
>           | 0x03 | «Complete List of 16-bit Service Class UUIDs» |
>           | 0x04 | «Incomplete List of 32-bit Service Class UUIDs» |
>           | 0x05 | «Complete List of 32-bit Service Class UUIDs» |
>           | 0x06 | «Incomplete List of 128-bit Service Class UUIDs» |
>           | 0x07 | «Complete List of 128-bit Service Class UUIDs» |
>           | 0x08 | «Shortened Local Name» |
>           | 0x09 | «Complete Local Name» |
>     - 测试用例
>       :   `AT+BLEADVDATA=0201060909373235365f424c45,D`，此广播中配置了«Complete Local Name» ，参考ASSIC码表，可知Name为 `7256_BLE`
>
> 3.AT\+BLESCANRSPDATA
> :   - 功能说明
>       :   这条AT命令用来设置扫描响应数据
>     - 命令格式
>       :   AT\+BLESCANRSPDATA\=param1,param2
>
>           |  |  |
>           | --- | --- |
>           | param1 | Scan\_Response\_Data, the data format is shown in Figure 1 |
>           | param2 | Scan\_Response\_Data\_Length  Range: 0x00 to 0x1F |
>     - 测试用例
>       :   `AT+BLESCANRSPDATA=0909373235365f424c45,A`
>
> 4.AT\+BLEPERADVDATA
> :   - 功能说明
>       :   这条AT命令用来设置周期性广播的数据
>     - 命令格式
>       :   AT\+BLEPERADVDATA\=param1,param2
>
>           |  |  |
>           | --- | --- |
>           | param1 | Periodic\_Advertising\_Data, the data format is shown in Figure 1 |
>           | param2 | Periodic\_Advertising\_Data\_Length  Range: 0x00 to 0x1F |
>     - 测试用例
>       :   `AT+BLEPERADVDATA=0909373235365f424c45,A`
>
> 5.AT\+BLEADVENABLE
> :   - 功能说明
>       :   这条AT命令用来开关传统/扩展/周期性广播
>     - 命令格式
>       :   AT\+BLEADVENABLE\=param1
>
>           |  |  |
>           | --- | --- |
>           | param1 | Advertising\_Enable  0x00 : Advertising is disabled  0x01 : Advertising is enabled |
>     - 测试用例
>       :   关闭广播：`AT+BLEADVENABLE=0`
>
>           开启广播：`AT+BLEADVENABLE=1`
>
> 6.AT\+BLESCANPARAM
> :   - 功能说明
>       :   这条AT命令用来设置扫描参数
>     - 命令格式
>       :   AT\+BLESCANPARAM\=param1,param2,param3,param4
>
>           |  |  |
>           | --- | --- |
>           | param1 | Own\_Address\_Type  0x00 : Public Device Address  0x01 : Random Device Address  0x02 : Resolvable Private Address,if no IRK use the public address  0x03 : Resolvable Private Address,if no IRK use the random address |
>           | param2 | Scanning\_PHYs  0x01 : Scan advertisements on the LE 1M PHY  0x04 : Scan advertisements on the LE Coded PHY  0x05 : Scan advertisements on the LE 1M PHY and Coded PHY |
>           | param3 | Scan\_Interval  Range: 0x0004 to 0xFFFF(Time \= N \* 0.625 ms) |
>           | param4 | Scan\_Window  Range: 0x0004 to 0xFFFF(Time \= N \* 0.625 ms) |
>     - 测试用例
>       :   `AT+BLESCANPARAM=0,1,64,1e`
>
> 7.AT\+BLESCANENABLE
> :   - 功能说明
>       :   这条AT命令用来开关扫描
>     - 命令格式
>       :   AT\+BLESCANENABLE\=param1
>
>           |  |  |
>           | --- | --- |
>           | param1 | LE\_Scan\_Enable  0x00 : Scanning disabled  0x01 : Scanning enabled |
>     - 测试用例
>       :   关闭扫描：`AT+BLESETSCANENABLE=0`
>
>           开启扫描：`AT+BLESETSCANENABLE=1`
>
> 8.AT\+BLECREATECONNECT
> :   - 功能说明
>       :   这条AT命令用来进行BLE连接
>     - 命令格式
>       :   AT\+BLECREATECONNECT\=param1,param2,param3,param4,param5,param6
>
>           |  |  |
>           | --- | --- |
>           | param1 | Connection\_Interval  Range: 0x0006 to 0x0C80(Time \= N \* 1.25 ms) |
>           | param2 | Con\_Latency  Range: 0x0000 to 0x01F3 |
>           | param3 | Supervision\_Timeout  Range: 0x000A to 0x0C80(Time \= N \* 10 ms) |
>           | param4 | Initiating\_PHYs(Bit number)  0 : Scan connectable advertisements on the LE 1M PHY  1 : Connection parameters for the LE 2M PHY are provided  2 : Scan connectable advertisements on the LE Coded PHY |
>           | param5 | Peer\_Address\_Type  0x00 : Public Device Address or Public Identity Address  0x01 : Random Device Address or Random (static) Identity Address |
>           | param6 | Peer\_Address |
>     - 测试用例
>       :   `AT+BLECREATECONNECT=17,0,1f4,1,1,db:b4:6f:66:8a:db`
>
> 9.AT\+BLECANCELCONNECT
> :   - 功能说明
>       :   这条AT命令用来取消正在进行的BLE连接
>     - 命令格式
>       :   AT\+BLECANCELCONNECT
>
>           此命令没有参数。
>     - 测试用例
>       :   `AT+BLECANCELCONNECT`
>
> 10.AT\+BLEDISCONNECT
> :   - 功能说明
>       :   这条AT命令用来断开指定的BLE链路
>     - 命令格式
>       :   AT\+BLEDISCONNECT\=param1
>
>           |  |  |
>           | --- | --- |
>           | param1 | Peer\_Address |
>     - 测试用例
>       :   `AT+BLEDISCONNECT=db:b4:6f:66:8a:db`
>
> 11.AT\+BLEPOWER
> :   - 功能说明
>       :   这条AT命令用来开关蓝牙
>     - 命令格式
>       :   AT\+BLEPOWER\=param1
>
>           |  |  |
>           | --- | --- |
>           | param1 | bluetooth on/off  0x00 : turn on bluetooth  0x01 : turn off bluetooth |
>     - 测试用例
>       :   关闭蓝牙：`AT+BLEPOWER=0`
>
>           开启蓝牙：`AT+BLEPOWER=1`
>
> 12.AT\+BLEREGISTERSERVICE
> :   - 功能说明
>       :   这条AT命令用来进行注册一个新服务
>     - 命令格式
>       :   AT\+BLEREGISTERSERVICE\=param1,param2,\[param3,param4,param5\]
>
>           |  |  |
>           | --- | --- |
>           | param1 | service\_id  Range: 0 to 35 |
>           | param2 | Service UUID  Range: 0x0000 to 0xFFFF |
>           | param3 | Characteristic UUID(optional)  Range: 0x0000 to 0xFFFF |
>           | param4 | data\_len  this param is optional, used for notification test, that specifys  the length of value to be notified |
>           | param5 | interval(ms)  this param is optional, used for notification test, that specifys  the interval to notify value |
>     - 测试用例
>       :   `AT+BLEREGISTERSERVICE=1,ff11,ff12,20,2000`
>
> 13.AT\+BLEUNREGISTERSERVICE
> :   - 功能说明
>       :   这条AT命令用来进行注销指定的服务
>     - 命令格式
>       :   AT\+BLEUNREGISTERSERVICE\=param1
>
>           |  |  |
>           | --- | --- |
>           | param1 | Service UUID  Range: 0x0000 to 0xFFFF |
>     - 测试用例
>       :   `AT+BLEUNREGISTERSERVICE=ff11`
>
> 14.AT\+BLEBOND
> :   - 功能说明
>       :   这条AT命令用来进行BLE配对
>     - 命令格式
>       :   AT\+BLEBOND\=param1
>
>           |  |  |
>           | --- | --- |
>           | param1 | Peer\_Address |
>     - 测试用例
>       :   `AT+BLEBOND=db:b4:6f:66:8a:db`
>
> 15.AT\+BLEATTREAD
> :   - 功能说明
>       :   这条AT命令用来设备作为master时进行读取slave的特征值
>     - 命令格式
>       :   AT\+BLEATTREAD\=param1,param2,param3
>
>           |  |  |
>           | --- | --- |
>           | param1 | Device\_ID  Default: 0 (Start from value 0\) |
>           | param2 | Con\_Idx  Default: 0 (Start from value 0\) |
>           | param3 | Attribute\_Handle  Start from value 0 (The value is reported during the BLE connection) |
>     - 测试用例
>       :   `AT+BLEATTREAD=0,0,9`
>
> 16.AT\+BLEREGPERFORMANCESERVICE
> :   - 功能说明
>       :   注册 BLE 吞吐量测试使用的 GATT Performance Service。
>     - 命令格式
>       :   AT\+BLEREGPERFORMANCESERVICE\=param1,param2,param3
>
>           |  |  |
>           | --- | --- |
>           | param1 | Service task ID |
>           | param2 | Service UUID |
>           | param3 | Notify Characteristic UUID |
>     - 测试用例
>       :   `AT+BLEREGPERFORMANCESERVICE=1,0x1234,0x5678`
>
> 17.AT\+BLETXTESTPARAM
> :   - 功能说明
>       :   设置吞吐量测试的 ATT Value 长度和发送间隔。Performance 模式采用发送完成回调连续发包。
>     - 命令格式
>       :   AT\+BLETXTESTPARAM\=param1,param2
>
>           |  |  |
>           | --- | --- |
>           | param1 | ATT Value length(bytes) |
>           | param2 | Send interval(ms) |
>     - 测试用例
>       :   `AT+BLETXTESTPARAM=244,100`
>
> 18.AT\+BLETXTESTENABLE
> :   - 功能说明
>       :   启动或停止 BLE 吞吐量发流。缺省模式为本地 GATT Server Notify；
>           `write_no_rsp` 模式为 GATT Client Write Without Response。
>     - 命令格式
>       :   AT\+BLETXTESTENABLE\=param1,\[param2\],\[param3\]
>
>           |  |  |
>           | --- | --- |
>           | param1 | Enable: 1\=start, 0\=stop |
>           | param2 | Connection index(optional, default 0\) |
>           | param3 | TX mode(optional): notify(default) or write\_no\_rsp |
>     - 测试用例
>       :   启动 Notify：`AT+BLETXTESTENABLE=1,0`
>
>           停止 Notify：`AT+BLETXTESTENABLE=0,0`
>
>           启动 Write Without Response：`AT+BLETXTESTENABLE=1,0,write_no_rsp`
>
>           停止 Write Without Response：`AT+BLETXTESTENABLE=0,0,write_no_rsp`
>
>           备注
>
>           Write NR 吞吐测试设计为同一时刻仅支持一个活动连接。启动前必须完成
>           Write Test Characteristic 发现；断开重连后必须重新发现，否则命令返回
>           `CMDRSP:ERROR`。
>
> 19.AT\+BLEPERFORMANCESTATISTICENABLE
> :   - 功能说明
>       :   开启或关闭 BLE 吞吐量 TX/RX 统计。开启后每秒输出 ATT Value 字节数。
>     - 命令格式
>       :   AT\+BLEPERFORMANCESTATISTICENABLE\=param1,param2
>
>           |  |  |
>           | --- | --- |
>           | param1 | Direction: tx or rx |
>           | param2 | Enable: 1\=start, 0\=stop |
>     - 测试用例
>       :   开启 TX 统计：`AT+BLEPERFORMANCESTATISTICENABLE=tx,1`
>
>           开启 RX 统计：`AT+BLEPERFORMANCESTATISTICENABLE=rx,1`
>
>           关闭 TX 统计：`AT+BLEPERFORMANCESTATISTICENABLE=tx,0`
>
>           关闭 RX 统计：`AT+BLEPERFORMANCESTATISTICENABLE=rx,0`

<a id="ble"></a>

## 4、BLE 吞吐量测试

> 测试角色：
>
> - Slave：广播侧，GATT Server。
> - Master：发起连接侧，GATT Client。
> - Notify 和 Write NR 吞吐测试同一时刻仅支持一个活动连接；断开重连后，
>   Master 必须重新执行 Characteristic 发现。
>
> 推荐参数：
>
> - Connection interval：`0x41` （81.25 ms）。
> - ATT Value length：244 bytes。加上 3-byte ATT Header 和 4-byte L2CAP Header 后，
>   正好填满一个 251-byte LL Data PDU，不发生 LL 分片。
>
> 如果从 BK7259 CLI 执行以下命令，需要在 AT 命令前增加 `ap_cmd`。
>
> 公共建链流程：
>
> ```
> # Slave
> AT+BLEREGPERFORMANCESERVICE=1,0x1234,0x5678
> AT+BLEADVPARAM=7,120,160,0,0,3,1,1
> AT+BLEADVDATA=0201060909373235365F424C45,D
> AT+BLEADVENABLE=1
>
> # Master
> AT+BLEREGPERFORMANCESERVICE=1,0x1234,0x5678
> AT+BLECREATECONNECT=41,0,1f4,1,0,<slave_addr>
> AT+BLECONNECTSTATE=<slave_addr>
> AT+BLEUPDATEMTU2MAX=<slave_addr>
> ```
>
> 2M PHY 测试时，Master 建链后增加：
>
> ```
> AT+BLEPHY=<slave_addr>,2,2,0
> ```
>
> 并确认日志包含 `tx_phy:0x02, rx_phy:0x02`。
>
> 场景 1：Slave Notify 到 Master
>
> ```
> # Slave
> AT+BLETXTESTPARAM=244,100
> AT+BLEPERFORMANCESTATISTICENABLE=tx,1
>
> # Master
> AT+BLEPERFORMANCESTATISTICENABLE=rx,1
>
> # Slave start
> AT+BLETXTESTENABLE=1,0
>
> # Stop
> # Slave
> AT+BLETXTESTENABLE=0,0
> AT+BLEPERFORMANCESTATISTICENABLE=tx,0
> # Master
> AT+BLEPERFORMANCESTATISTICENABLE=rx,0
> ```
>
> 场景 2：Master Write Without Response 到 Slave
>
> ```
> # Master
> AT+BLEDISCOVERCHAR=0,1,ffff
> # Wait for: char rsp uuid 0x12f0 ... and discover complete
> AT+BLETXTESTPARAM=244,100
> AT+BLEPERFORMANCESTATISTICENABLE=tx,1
>
> # Slave
> AT+BLEPERFORMANCESTATISTICENABLE=rx,1
>
> # Master start
> AT+BLETXTESTENABLE=1,0,write_no_rsp
>
> # Stop
> # Master
> AT+BLETXTESTENABLE=0,0,write_no_rsp
> AT+BLEPERFORMANCESTATISTICENABLE=tx,0
> # Slave
> AT+BLEPERFORMANCESTATISTICENABLE=rx,0
> ```
>
> 场景 3：Slave Notify 和 Master Write Without Response 双向发送
>
> ```
> # Slave
> AT+BLETXTESTPARAM=244,100
> AT+BLEPERFORMANCESTATISTICENABLE=tx,1
> AT+BLEPERFORMANCESTATISTICENABLE=rx,1
>
> # Master
> AT+BLEDISCOVERCHAR=0,1,ffff
> # Wait for: char rsp uuid 0x12f0 ... and discover complete
> AT+BLETXTESTPARAM=244,100
> AT+BLEPERFORMANCESTATISTICENABLE=tx,1
> AT+BLEPERFORMANCESTATISTICENABLE=rx,1
>
> # Start bidirectional traffic
> # Slave
> AT+BLETXTESTENABLE=1,0
> # Master
> AT+BLETXTESTENABLE=1,0,write_no_rsp
>
> # Stop
> # Slave
> AT+BLETXTESTENABLE=0,0
> AT+BLEPERFORMANCESTATISTICENABLE=tx,0
> AT+BLEPERFORMANCESTATISTICENABLE=rx,0
> # Master
> AT+BLETXTESTENABLE=0,0,write_no_rsp
> AT+BLEPERFORMANCESTATISTICENABLE=tx,0
> AT+BLEPERFORMANCESTATISTICENABLE=rx,0
> ```
>
> 统计日志格式：
>
> ```
> current tx <bytes> bytes/sec
> current rx <bytes> bytes/sec
> ```
>
> 同一方向的 TX 和 RX 平均值应接近。切换 PHY 或测试场景前，建议重启两块板，
> 避免连接、统计 timer 或 Characteristic handle 状态残留。
