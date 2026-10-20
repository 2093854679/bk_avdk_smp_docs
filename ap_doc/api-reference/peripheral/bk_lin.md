---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_lin.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="lin"></a>

# LIN

BK7259 AP 侧 LIN API（`include/driver/lin.h`）。

<a id="lin-api-reference"></a>

## LIN API Reference

<a id="header-file"></a>

### Header File

- [lin.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/lin.h)

<a id="functions"></a>

### Functions

<a id="_CPPv416bk_lin_gpio_init13lin_channel_t"></a>

<a id="_CPPv316bk_lin_gpio_init13lin_channel_t"></a> <a id="_CPPv216bk_lin_gpio_init13lin_channel_t"></a> <a id="bk_lin_gpio_init__lin_channel_t"></a> <a id="lin_8h_1a0ffc8374b6177700e1be2ad666ec8ffb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_gpio\_init([lin\_channel\_t](#_CPPv413lin_channel_t "lin_channel_t") chn)
:   Select the LIN gpio.

    This API adaptation hardware link channel

    参数
    :   **chn** – gpio channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv410bk_lin_cfgP12lin_config_t"></a>

<a id="_CPPv310bk_lin_cfgP12lin_config_t"></a> <a id="_CPPv210bk_lin_cfgP12lin_config_t"></a> <a id="bk_lin_cfg__lin_config_tP"></a> <a id="lin_8h_1ae5ba59a061a0dbbd7e525c4c1863772c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_cfg([lin\_config\_t](#_CPPv412lin_config_t "lin_config_t") \*cfg)
:   the LIN config

    This API lin configure interface

    参数
    :   **cfg** – basic configuration information

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_lin_driver_initv"></a>

<a id="_CPPv318bk_lin_driver_initv"></a> <a id="_CPPv218bk_lin_driver_initv"></a> <a id="bk_lin_driver_init__void"></a> <a id="lin_8h_1a3fb92d21e209318a6a8570c747885581"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_driver\_init(void)
:   Init the LIN driver.

    This API init the resoure common:

    - Init LIN driver control memory

    **Attention**
    :   1\. This API should be called before any other LIN APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_lin_driver_deinitv"></a>

<a id="_CPPv320bk_lin_driver_deinitv"></a> <a id="_CPPv220bk_lin_driver_deinitv"></a> <a id="bk_lin_driver_deinit__void"></a> <a id="lin_8h_1a2431bb175afb01d4c712281ca6d99bb8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_driver\_deinit(void)
:   Deinit the LIN driver.

    This API free all resource related to LIN and disable LIN.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_lin_interrupt_enablev"></a>

<a id="_CPPv323bk_lin_interrupt_enablev"></a> <a id="_CPPv223bk_lin_interrupt_enablev"></a> <a id="bk_lin_interrupt_enable__void"></a> <a id="lin_8h_1a61e30da85e7164de71c1246651b69d24"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_interrupt\_enable(void)
:   Enable LIN interrupt.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_lin_interrupt_disablev"></a>

<a id="_CPPv324bk_lin_interrupt_disablev"></a> <a id="_CPPv224bk_lin_interrupt_disablev"></a> <a id="bk_lin_interrupt_disable__void"></a> <a id="lin_8h_1a03fb5762359e33a1e69a01369bf9dfc6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_interrupt\_disable(void)
:   Disable LIN interrupt.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_lin_register_isr14lin_int_type_t9lin_isr_tPv"></a>

<a id="_CPPv319bk_lin_register_isr14lin_int_type_t9lin_isr_tPv"></a> <a id="_CPPv219bk_lin_register_isr14lin_int_type_t9lin_isr_tPv"></a> <a id="bk_lin_register_isr__lin_int_type_t.lin_isr_t.voidP"></a> <a id="lin_8h_1aeb0223c56e6cb99292cff853d172f096"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_register\_isr([lin\_int\_type\_t](#_CPPv414lin_int_type_t "lin_int_type_t") type, [lin\_isr\_t](#_CPPv49lin_isr_t "lin_isr_t") isr, void \*arg)
:   Register the interrupt service routine for LIN.

    This API register lin isr callback function.

    参数
    :   - **type** – register interrupt type
        - **isr** – lin callback
        - **arg** – lin callback arg

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv414bk_lin_set_dev9lin_dev_t"></a>

<a id="_CPPv314bk_lin_set_dev9lin_dev_t"></a> <a id="_CPPv214bk_lin_set_dev9lin_dev_t"></a> <a id="bk_lin_set_dev__lin_dev_t"></a> <a id="lin_8h_1a5080da5ac215b0f75f2476d2143807fe"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_dev([lin\_dev\_t](#_CPPv49lin_dev_t "lin_dev_t") dev)
:   Set this device as master or slave.

    参数
    :   **lin\_dev\_t** – device type

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv414bk_lin_get_devv"></a>

<a id="_CPPv314bk_lin_get_devv"></a> <a id="_CPPv214bk_lin_get_devv"></a> <a id="bk_lin_get_dev__void"></a> <a id="lin_8h_1ac96a203f16c5e18e7a6a2dd2a4298c7b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_get\_dev(void)
:   Get this device as master or slave.

    参数
    :   **lin\_dev\_t** – device type

    返回
    :   - 0: slave
        - 1: master
        - others: other errors.

<a id="_CPPv416bk_lin_set_ident8uint32_t"></a>

<a id="_CPPv316bk_lin_set_ident8uint32_t"></a> <a id="_CPPv216bk_lin_set_ident8uint32_t"></a> <a id="bk_lin_set_ident__uint32_t"></a> <a id="lin_8h_1aec77cc0927a4fdf4a98f04980d778a35"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_ident(uint32\_t ident)
:   Set this device ident.

    This interface will set the id and transmission direction of the data frame

    参数
    :   **ident** – bit3 for master indicates whether this frame is a sending or receving bit \[4\] is direction :0 recv,1 send bit\[3:0\] is id number

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_lin_get_identv"></a>

<a id="_CPPv316bk_lin_get_identv"></a> <a id="_CPPv216bk_lin_get_identv"></a> <a id="bk_lin_get_ident__void"></a> <a id="lin_8h_1a4e9aabcdadfb3fb8be0952390c768f1c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_get\_ident(void)
:   get this device ident

    get identifer and transmittion direction

    返回
    :   - bit \[4\] is direction :0 recv,1 send bit\[3:0\] is id number

<a id="_CPPv415bk_lin_set_rated"></a>

<a id="_CPPv315bk_lin_set_rated"></a> <a id="_CPPv215bk_lin_set_rated"></a> <a id="bk_lin_set_rate__double"></a> <a id="lin_8h_1af1a7f949246def0840d2893f9c4d1a8e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_rate(double rate)
:   Set this device bit rate (master only)

    This interface will set data rate between 1 Kbit/s and 20 Kbit/s (for master) automatic bit rate detection (for slave)

    参数
    :   **rate** – data rate

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_lin_get_ratev"></a>

<a id="_CPPv315bk_lin_get_ratev"></a> <a id="_CPPv215bk_lin_get_ratev"></a> <a id="bk_lin_get_rate__void"></a> <a id="lin_8h_1a1a2a4818237704546985a93d185b8223"></a> double bk\_lin\_get\_rate(void)
:   Get this device bit rate (master only)

    get data rate

    返回
    :   - data rate value

<a id="_CPPv422bk_lin_set_data_length14lin_data_len_t"></a>

<a id="_CPPv322bk_lin_set_data_length14lin_data_len_t"></a> <a id="_CPPv222bk_lin_set_data_length14lin_data_len_t"></a> <a id="bk_lin_set_data_length__lin_data_len_t"></a> <a id="lin_8h_1ad071819df63c4351d13b01c5d6ffaf52"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_data\_length([lin\_data\_len\_t](#_CPPv414lin_data_len_t "lin_data_len_t") len)
:   Set the transmission data length.

    the max data length is 8bytes

    参数
    :   **len** – data length

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_lin_get_data_lengthv"></a>

<a id="_CPPv322bk_lin_get_data_lengthv"></a> <a id="_CPPv222bk_lin_get_data_lengthv"></a> <a id="bk_lin_get_data_length__void"></a> <a id="lin_8h_1a9fecbb7784c66983c6fa309200dc293f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_get\_data\_length(void)
:   Get the transmission data length.

    the max data length is 8bytes

    返回
    :   - data length value.

<a id="_CPPv420bk_lin_set_enh_check14lin_checksum_t"></a>

<a id="_CPPv320bk_lin_set_enh_check14lin_checksum_t"></a> <a id="_CPPv220bk_lin_set_enh_check14lin_checksum_t"></a> <a id="bk_lin_set_enh_check__lin_checksum_t"></a> <a id="lin_8h_1a26c9728e6b37c2790981d34921af821c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_enh\_check([lin\_checksum\_t](#_CPPv414lin_checksum_t "lin_checksum_t") check)
:   Set the checksum type.

    参数
    :   **checksum** – type:0 classic checksum,1 enhanced checksum

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_lin_get_enh_checkv"></a>

<a id="_CPPv320bk_lin_get_enh_checkv"></a> <a id="_CPPv220bk_lin_get_enh_checkv"></a> <a id="bk_lin_get_enh_check__void"></a> <a id="lin_8h_1ad6127d0fed4a4cae9e43860401a9b76f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_get\_enh\_check(void)
:   Get the checksum type.

    返回
    :   - checksum value.

<a id="_CPPv430bk_lin_set_bus_inactivity_time25lin_bus_inactivity_time_t"></a>

<a id="_CPPv330bk_lin_set_bus_inactivity_time25lin_bus_inactivity_time_t"></a> <a id="_CPPv230bk_lin_set_bus_inactivity_time25lin_bus_inactivity_time_t"></a> <a id="bk_lin_set_bus_inactivity_time__lin_bus_inactivity_time_t"></a> <a id="lin_8h_1a803c1e514caa214b70719c71f18c8f75"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_bus\_inactivity\_time([lin\_bus\_inactivity\_time\_t](#_CPPv425lin_bus_inactivity_time_t "lin_bus_inactivity_time_t") time)
:   Set bus inactivity time(slave only),.

    This API will generate an bus idle timeout interrupt when it detectes no bus activity for a set time.

    参数
    :   **time** – set timeout, 0:4s, 1:6s, 2:8s, 3:10s

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv430bk_lin_get_bus_inactivity_timev"></a>

<a id="_CPPv330bk_lin_get_bus_inactivity_timev"></a> <a id="_CPPv230bk_lin_get_bus_inactivity_timev"></a> <a id="bk_lin_get_bus_inactivity_time__void"></a> <a id="lin_8h_1ad4cc980fa9ad8733b9f00cbac91476b6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_get\_bus\_inactivity\_time(void)
:   Get bus inactivity time(slave only),.

    返回
    :   - bus inactivity enum

<a id="_CPPv426bk_lin_set_wup_repeat_time21lin_wup_repeat_time_t"></a>

<a id="_CPPv326bk_lin_set_wup_repeat_time21lin_wup_repeat_time_t"></a> <a id="_CPPv226bk_lin_set_wup_repeat_time21lin_wup_repeat_time_t"></a> <a id="bk_lin_set_wup_repeat_time__lin_wup_repeat_time_t"></a> <a id="lin_8h_1a712e95db3b90e7b8cc57482ee05da29c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_wup\_repeat\_time([lin\_wup\_repeat\_time\_t](#_CPPv421lin_wup_repeat_time_t "lin_wup_repeat_time_t") time)
:   Set wake up repeat time(slave only),.

    The time for repeating of wake up because of no reaction on the bus

    参数
    :   **time** – set time, 0:180ms, 1:200ms, 2:220ms, 3:240ms

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_lin_get_wup_repeat_timev"></a>

<a id="_CPPv326bk_lin_get_wup_repeat_timev"></a> <a id="_CPPv226bk_lin_get_wup_repeat_timev"></a> <a id="bk_lin_get_wup_repeat_time__void"></a> <a id="lin_8h_1a689ec4cdfde6c0db62656b3b3cd26635"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_get\_wup\_repeat\_time(void)
:   Get wake up repeat time(slave only),.

    返回
    :   - repeat time enum

<a id="_CPPv419bk_lin_set_transmit11lin_trans_t"></a>

<a id="_CPPv319bk_lin_set_transmit11lin_trans_t"></a> <a id="_CPPv219bk_lin_set_transmit11lin_trans_t"></a> <a id="bk_lin_set_transmit__lin_trans_t"></a> <a id="lin_8h_1a2fe1378b675e8bcaf51b8fe15127c6da"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_transmit([lin\_trans\_t](#_CPPv411lin_trans_t "lin_trans_t") trans)
:   Set transmit operation,.

    The API determines whether the current frame is transmit frame or a receive frame for the LIN node.

    参数
    :   **trans** – 1 \- transmit operation, 0 \- receive operation

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_lin_get_transmitv"></a>

<a id="_CPPv319bk_lin_get_transmitv"></a> <a id="_CPPv219bk_lin_get_transmitv"></a> <a id="bk_lin_get_transmit__void"></a> <a id="lin_8h_1a72fe53316998947f1e6f8e37b785050a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_get\_transmit(void)
:   get transmit operation,

    参数
    :   **trans** – 1 \- transmit operation, 0 \- receive operation

    返回
    :   - 1: transmit operation,
        - 0: receive operation,
        - others: other errors.

<a id="_CPPv411bk_lin_sendP7uint8_t8uint32_t"></a>

<a id="_CPPv311bk_lin_sendP7uint8_t8uint32_t"></a> <a id="_CPPv211bk_lin_sendP7uint8_t8uint32_t"></a> <a id="bk_lin_send__uint8_tP.uint32_t"></a> <a id="lin_8h_1a84643041182e8f1e3c8d499a8ac74781"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_send(uint8\_t \*buf, uint32\_t len)
:   load buf to the data bytes

    参数
    :   - **buf** – source data buffer
        - **len** – data length,max 8 bytes

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_lin_recvP7uint8_t8uint32_t"></a>

<a id="_CPPv311bk_lin_recvP7uint8_t8uint32_t"></a> <a id="_CPPv211bk_lin_recvP7uint8_t8uint32_t"></a> <a id="bk_lin_recv__uint8_tP.uint32_t"></a> <a id="lin_8h_1adbdb68e2ac3d345b535d3bed9ccd7f19"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_recv(uint8\_t \*buf, uint32\_t len)
:   load data bytes to buf,

    参数
    :   - **buf** – destination data buffer
        - **len** – data length,max 8 bytes

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv49bk_lin_tx8lin_id_tP7uint8_t8uint32_t"></a>

<a id="_CPPv39bk_lin_tx8lin_id_tP7uint8_t8uint32_t"></a> <a id="_CPPv29bk_lin_tx8lin_id_tP7uint8_t8uint32_t"></a> <a id="bk_lin_tx__lin_id_t.uint8_tP.uint32_t"></a> <a id="lin_8h_1a93d863ab6cf0b159f1611e4bc421df37"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_tx([lin\_id\_t](#_CPPv48lin_id_t "lin_id_t") id, uint8\_t \*tx, uint32\_t len)
:   Send data based on specified id,.

    参数
    :   - **id** – target id of sending data
        - **tx** – send data buffer
        - **len** – data length,max 8 bytes

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv49bk_lin_rx8lin_id_tP7uint8_t8uint32_t8uint32_t"></a>

<a id="_CPPv39bk_lin_rx8lin_id_tP7uint8_t8uint32_t8uint32_t"></a> <a id="_CPPv29bk_lin_rx8lin_id_tP7uint8_t8uint32_t8uint32_t"></a> <a id="bk_lin_rx__lin_id_t.uint8_tP.uint32_t.uint32_t"></a> <a id="lin_8h_1a515cd8ab9a33ff8f20446b3a5c255189"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_rx([lin\_id\_t](#_CPPv48lin_id_t "lin_id_t") id, uint8\_t \*rx, uint32\_t len, uint32\_t timeout)
:   Recevie data based on specified id.

    This interface has blocking function. using freeROTS task notification mechanism

    The API recevie data max 8 bytes

    参数
    :   - **id** – target id to recevie data
        - **rx** – recevie data buffer
        - **len** – data length,max 8 bytes
        - **timeout** – The maximum amount of time that the task should wait in the Blocked state for a notification to be received.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_lin_set_start_reqv"></a>

<a id="_CPPv320bk_lin_set_start_reqv"></a> <a id="_CPPv220bk_lin_set_start_reqv"></a> <a id="bk_lin_set_start_req__void"></a> <a id="lin_8h_1a9afa326acbf0c8cdc72ee499a5f9ea0f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_start\_req(void)
:   Set start transmission request,.

    The API is celled to start the LIN transmission after loading identifier, data length and data buffer

    master only,slaver reserved

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_lin_get_start_reqv"></a>

<a id="_CPPv320bk_lin_get_start_reqv"></a> <a id="_CPPv220bk_lin_get_start_reqv"></a> <a id="bk_lin_get_start_req__void"></a> <a id="lin_8h_1afdca48589d933e9d609c19e0945b81c1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_get\_start\_req(void)
:   Get start transmission request status,.

    The API is celled to start the LIN transmission after loading identifier, data length and data buffer

    master only,slaver reserved

    返回
    :   - 0: The transmission is finished or an error is occurred
        - 1: Transmitting.

<a id="_CPPv416bk_lin_set_sleepv"></a>

<a id="_CPPv316bk_lin_set_sleepv"></a> <a id="_CPPv216bk_lin_set_sleepv"></a> <a id="bk_lin_set_sleep__void"></a> <a id="lin_8h_1a59f9573b90d1fbda60459015a7d80d7c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_sleep(void)
:   Set sleep mode,.

    The API is used by LIN to determine whether the LIN bus is in sleep mode or not

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_lin_get_sleepv"></a>

<a id="_CPPv316bk_lin_get_sleepv"></a> <a id="_CPPv216bk_lin_get_sleepv"></a> <a id="bk_lin_get_sleep__void"></a> <a id="lin_8h_1ace4767b836b65db4450e80c3c6df2eeb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_get\_sleep(void)
:   Get sleep mode,.

    返回
    :   - 1: sleep
        - 0: wakeup
        - others: other errors.

<a id="_CPPv417bk_lin_set_wakeupv"></a>

<a id="_CPPv317bk_lin_set_wakeupv"></a> <a id="_CPPv217bk_lin_set_wakeupv"></a> <a id="bk_lin_set_wakeup__void"></a> <a id="lin_8h_1ac368b3a1c242290fd6d1637b5b5b9ee6"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_lin\_set\_wakeup(void)
:   Set wakeup request,.

    The API terminate the sleep mode of LIN bus by sending a wakeup signal

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="lin-api-typedefs"></a>

## LIN API Typedefs

<a id="id1"></a>

### Header File

- [lin\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/lin_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv414lin_callback_t"></a>

<a id="_CPPv314lin_callback_t"></a> <a id="_CPPv214lin_callback_t"></a> <a id="lin_callback_t"></a> <a id="structlin__callback__t"></a> struct lin\_callback\_t

<a id="_CPPv414lin_gpio_map_t"></a>

<a id="_CPPv314lin_gpio_map_t"></a> <a id="_CPPv214lin_gpio_map_t"></a> <a id="lin_gpio_map_t"></a> <a id="structlin__gpio__map__t"></a> struct lin\_gpio\_map\_t

<a id="_CPPv410lin_gpio_t"></a>

<a id="_CPPv310lin_gpio_t"></a> <a id="_CPPv210lin_gpio_t"></a> <a id="lin_gpio_t"></a> <a id="structlin__gpio__t"></a> struct lin\_gpio\_t

<a id="_CPPv49lin_buf_t"></a>

<a id="_CPPv39lin_buf_t"></a> <a id="_CPPv29lin_buf_t"></a> <a id="lin_buf_t"></a> <a id="structlin__buf__t"></a> struct lin\_buf\_t

<a id="_CPPv412lin_config_t"></a>

<a id="_CPPv312lin_config_t"></a> <a id="_CPPv212lin_config_t"></a> <a id="lin_config_t"></a> <a id="structlin__config__t"></a> struct lin\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12lin_config_t16bus_inactiv_timeE"></a>

    <a id="_CPPv3N12lin_config_t16bus_inactiv_timeE"></a> <a id="_CPPv2N12lin_config_t16bus_inactiv_timeE"></a> <a id="lin_config_t::bus_inactiv_time__lin_bus_inactivity_time_t"></a> <a id="structlin__config__t_1a93f4b7a76923a7e28484fd4490d286a9"></a> [lin\_bus\_inactivity\_time\_t](#_CPPv425lin_bus_inactivity_time_t "lin_bus_inactivity_time_t") bus\_inactiv\_time
    :   master only

    <a id="_CPPv4N12lin_config_t15wup_repeat_timeE"></a>

    <a id="_CPPv3N12lin_config_t15wup_repeat_timeE"></a> <a id="_CPPv2N12lin_config_t15wup_repeat_timeE"></a> <a id="lin_config_t::wup_repeat_time__lin_wup_repeat_time_t"></a> <a id="structlin__config__t_1a74756cc5da072f9f9da4cf6890c8e3d2"></a> [lin\_wup\_repeat\_time\_t](#_CPPv421lin_wup_repeat_time_t "lin_wup_repeat_time_t") wup\_repeat\_time
    :   slave only

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_LIN_NOT_INIT"></a>

<a id="lin__types_8h_1ab11bacc2e23b0311b0dd29594c4267e8"></a> BK\_ERR\_LIN\_NOT\_INIT
:   LIN driver not init

<a id="c.BK_ERR_LIN_INT_TYPE"></a>

<a id="lin__types_8h_1affec5111ceb4d8cae84b0afcfdee447c"></a> BK\_ERR\_LIN\_INT\_TYPE
:   LIN interrupte type error

<a id="c.BK_ERR_LIN_BIT_ERROR"></a>

<a id="lin__types_8h_1ada5f28e82e71255bfe40df56556b8d5d"></a> BK\_ERR\_LIN\_BIT\_ERROR
:   LIN bit error

<a id="c.BK_ERR_LIN_CHK_ERROR"></a>

<a id="lin__types_8h_1a3d0b4a8d1cc92c926a9d9178bd19edf9"></a> BK\_ERR\_LIN\_CHK\_ERROR
:   LIN checksum error

<a id="c.BK_ERR_LIN_TIMEOUT_ERROR"></a>

<a id="lin__types_8h_1a75d01dc7ae264f3bc4166e71b6714700"></a> BK\_ERR\_LIN\_TIMEOUT\_ERROR
:   LIN timeout error

<a id="c.BK_ERR_LIN_PARITY_ERROR"></a>

<a id="lin__types_8h_1adfb8c4773dfd78b25bb7feed76b9e0e5"></a> BK\_ERR\_LIN\_PARITY\_ERROR
:   LIN identifier parity error

<a id="c.BK_ERR_LIN_HAL_INVALID_ADDR"></a>

<a id="lin__types_8h_1a6a562b40e3c5fe2f886025b2df12b7af"></a> BK\_ERR\_LIN\_HAL\_INVALID\_ADDR
:   LIN invalid addr

<a id="c.BK_ERR_LIN_HAL_INVALID_ARG"></a>

<a id="lin__types_8h_1a04b160cc3d49f064907d38100b7bb721"></a> BK\_ERR\_LIN\_HAL\_INVALID\_ARG
:   LIN invalid arg

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv49lin_isr_t"></a>

<a id="_CPPv39lin_isr_t"></a> <a id="_CPPv29lin_isr_t"></a> <a id="lin_isr_t"></a> <a id="lin__types_8h_1a5b80c1fd43d0173535640c1f05e241d9"></a> typedef void (\*lin\_isr\_t)(void \*arg)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv414lin_int_type_t"></a>

<a id="_CPPv314lin_int_type_t"></a> <a id="_CPPv214lin_int_type_t"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3"></a> enum lin\_int\_type\_t
:   *Values:*

    <a id="_CPPv4N14lin_int_type_t16LIN_INT_COMPLETEE"></a>

    <a id="_CPPv3N14lin_int_type_t16LIN_INT_COMPLETEE"></a> <a id="_CPPv2N14lin_int_type_t16LIN_INT_COMPLETEE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3a0cbfeff8859816515f50cf2d4713bc2c"></a> enumerator LIN\_INT\_COMPLETE

    <a id="_CPPv4N14lin_int_type_t14LIN_INT_WAKEUPE"></a>

    <a id="_CPPv3N14lin_int_type_t14LIN_INT_WAKEUPE"></a> <a id="_CPPv2N14lin_int_type_t14LIN_INT_WAKEUPE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3a0814e16eeb2082e7fd3f58fb5f5dd98b"></a> enumerator LIN\_INT\_WAKEUP

    <a id="_CPPv4N14lin_int_type_t20LIN_INT_IDLE_TIMEOUTE"></a>

    <a id="_CPPv3N14lin_int_type_t20LIN_INT_IDLE_TIMEOUTE"></a> <a id="_CPPv2N14lin_int_type_t20LIN_INT_IDLE_TIMEOUTE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3a64efd0e66f1e22b16926c652af610140"></a> enumerator LIN\_INT\_IDLE\_TIMEOUT

    <a id="_CPPv4N14lin_int_type_t15LIN_INT_ABORTEDE"></a>

    <a id="_CPPv3N14lin_int_type_t15LIN_INT_ABORTEDE"></a> <a id="_CPPv2N14lin_int_type_t15LIN_INT_ABORTEDE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3a7db0dedf9f4c0210d628e4a47857022f"></a> enumerator LIN\_INT\_ABORTED

    <a id="_CPPv4N14lin_int_type_t16LIN_INT_DATA_REQE"></a>

    <a id="_CPPv3N14lin_int_type_t16LIN_INT_DATA_REQE"></a> <a id="_CPPv2N14lin_int_type_t16LIN_INT_DATA_REQE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3a080f56fedff56b42b9aa87c0d34a5e0b"></a> enumerator LIN\_INT\_DATA\_REQ

    <a id="_CPPv4N14lin_int_type_t15LIN_INT_BIT_ERRE"></a>

    <a id="_CPPv3N14lin_int_type_t15LIN_INT_BIT_ERRE"></a> <a id="_CPPv2N14lin_int_type_t15LIN_INT_BIT_ERRE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3a5dcae3a2dabfc8e44743fcbb8029fcd0"></a> enumerator LIN\_INT\_BIT\_ERR

    <a id="_CPPv4N14lin_int_type_t15LIN_INT_CHK_ERRE"></a>

    <a id="_CPPv3N14lin_int_type_t15LIN_INT_CHK_ERRE"></a> <a id="_CPPv2N14lin_int_type_t15LIN_INT_CHK_ERRE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3a450f17b3d814238d24ba5bc9aa6588c8"></a> enumerator LIN\_INT\_CHK\_ERR

    <a id="_CPPv4N14lin_int_type_t19LIN_INT_TIMEOUT_ERRE"></a>

    <a id="_CPPv3N14lin_int_type_t19LIN_INT_TIMEOUT_ERRE"></a> <a id="_CPPv2N14lin_int_type_t19LIN_INT_TIMEOUT_ERRE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3a93d5340bfd3441f1cdbb8eb45b474ebc"></a> enumerator LIN\_INT\_TIMEOUT\_ERR

    <a id="_CPPv4N14lin_int_type_t18LIN_INT_PARITY_ERRE"></a>

    <a id="_CPPv3N14lin_int_type_t18LIN_INT_PARITY_ERRE"></a> <a id="_CPPv2N14lin_int_type_t18LIN_INT_PARITY_ERRE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3a7de37a5462978066a71324348d3e9cd6"></a> enumerator LIN\_INT\_PARITY\_ERR

    <a id="_CPPv4N14lin_int_type_t11LIN_INT_MAXE"></a>

    <a id="_CPPv3N14lin_int_type_t11LIN_INT_MAXE"></a> <a id="_CPPv2N14lin_int_type_t11LIN_INT_MAXE"></a> <a id="lin__types_8h_1a5cfec5b2208c1c74ef5554e337e5dec3ab55d9b226f0badebd5a0c079c34d5cfc"></a> enumerator LIN\_INT\_MAX

<a id="_CPPv411lin_trans_t"></a>

<a id="_CPPv311lin_trans_t"></a> <a id="_CPPv211lin_trans_t"></a> <a id="lin__types_8h_1aa1f4981f69426333a3ab62f2b4971d55"></a> enum lin\_trans\_t
:   *Values:*

    <a id="_CPPv4N11lin_trans_t8LIN_RECVE"></a>

    <a id="_CPPv3N11lin_trans_t8LIN_RECVE"></a> <a id="_CPPv2N11lin_trans_t8LIN_RECVE"></a> <a id="lin__types_8h_1aa1f4981f69426333a3ab62f2b4971d55a0fbcf05703c1ca71e9c0e47ed90f5213"></a> enumerator LIN\_RECV

    <a id="_CPPv4N11lin_trans_t8LIN_SENDE"></a>

    <a id="_CPPv3N11lin_trans_t8LIN_SENDE"></a> <a id="_CPPv2N11lin_trans_t8LIN_SENDE"></a> <a id="lin__types_8h_1aa1f4981f69426333a3ab62f2b4971d55a1ada94b0326874547f90f9f6933dc0a7"></a> enumerator LIN\_SEND

<a id="_CPPv48lin_en_t"></a>

<a id="_CPPv38lin_en_t"></a> <a id="_CPPv28lin_en_t"></a> <a id="lin__types_8h_1a80ca3f907b81636755494c49f6f1c652"></a> enum lin\_en\_t
:   *Values:*

    <a id="_CPPv4N8lin_en_t11LIN_DISABLEE"></a>

    <a id="_CPPv3N8lin_en_t11LIN_DISABLEE"></a> <a id="_CPPv2N8lin_en_t11LIN_DISABLEE"></a> <a id="lin__types_8h_1a80ca3f907b81636755494c49f6f1c652a8052be4c34070dc5b1f52e8c6ac812ba"></a> enumerator LIN\_DISABLE

    <a id="_CPPv4N8lin_en_t10LIN_ENABLEE"></a>

    <a id="_CPPv3N8lin_en_t10LIN_ENABLEE"></a> <a id="_CPPv2N8lin_en_t10LIN_ENABLEE"></a> <a id="lin__types_8h_1a80ca3f907b81636755494c49f6f1c652a2bd4208267d069879750fbbe59319161"></a> enumerator LIN\_ENABLE

<a id="_CPPv425lin_bus_inactivity_time_t"></a>

<a id="_CPPv325lin_bus_inactivity_time_t"></a> <a id="_CPPv225lin_bus_inactivity_time_t"></a> <a id="lin__types_8h_1acf701a1518671653b6755496af29fd06"></a> enum lin\_bus\_inactivity\_time\_t
:   *Values:*

    <a id="_CPPv4N25lin_bus_inactivity_time_t21LIN_BUS_INACTIVITY_4SE"></a>

    <a id="_CPPv3N25lin_bus_inactivity_time_t21LIN_BUS_INACTIVITY_4SE"></a> <a id="_CPPv2N25lin_bus_inactivity_time_t21LIN_BUS_INACTIVITY_4SE"></a> <a id="lin__types_8h_1acf701a1518671653b6755496af29fd06acbb04a385135f74a38c6b827c5a9ac64"></a> enumerator LIN\_BUS\_INACTIVITY\_4S

    <a id="_CPPv4N25lin_bus_inactivity_time_t21LIN_BUS_INACTIVITY_6SE"></a>

    <a id="_CPPv3N25lin_bus_inactivity_time_t21LIN_BUS_INACTIVITY_6SE"></a> <a id="_CPPv2N25lin_bus_inactivity_time_t21LIN_BUS_INACTIVITY_6SE"></a> <a id="lin__types_8h_1acf701a1518671653b6755496af29fd06a6c991f8340703bf88fdf52f7d106a8f5"></a> enumerator LIN\_BUS\_INACTIVITY\_6S

    <a id="_CPPv4N25lin_bus_inactivity_time_t21LIN_BUS_INACTIVITY_8SE"></a>

    <a id="_CPPv3N25lin_bus_inactivity_time_t21LIN_BUS_INACTIVITY_8SE"></a> <a id="_CPPv2N25lin_bus_inactivity_time_t21LIN_BUS_INACTIVITY_8SE"></a> <a id="lin__types_8h_1acf701a1518671653b6755496af29fd06afeb872864f19d3f30b1052ebee213061"></a> enumerator LIN\_BUS\_INACTIVITY\_8S

    <a id="_CPPv4N25lin_bus_inactivity_time_t22LIN_BUS_INACTIVITY_10SE"></a>

    <a id="_CPPv3N25lin_bus_inactivity_time_t22LIN_BUS_INACTIVITY_10SE"></a> <a id="_CPPv2N25lin_bus_inactivity_time_t22LIN_BUS_INACTIVITY_10SE"></a> <a id="lin__types_8h_1acf701a1518671653b6755496af29fd06a2dcd26192366a30704a7b72c0c5a7049"></a> enumerator LIN\_BUS\_INACTIVITY\_10S

<a id="_CPPv421lin_wup_repeat_time_t"></a>

<a id="_CPPv321lin_wup_repeat_time_t"></a> <a id="_CPPv221lin_wup_repeat_time_t"></a> <a id="lin__types_8h_1ac49334805c2eec4f8edde84b09b3f2b9"></a> enum lin\_wup\_repeat\_time\_t
:   *Values:*

    <a id="_CPPv4N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_180MSE"></a>

    <a id="_CPPv3N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_180MSE"></a> <a id="_CPPv2N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_180MSE"></a> <a id="lin__types_8h_1ac49334805c2eec4f8edde84b09b3f2b9a62324dc59da96990f8cba68b78eda69c"></a> enumerator LIN\_WUP\_REPEAT\_180MS

    <a id="_CPPv4N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_200MSE"></a>

    <a id="_CPPv3N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_200MSE"></a> <a id="_CPPv2N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_200MSE"></a> <a id="lin__types_8h_1ac49334805c2eec4f8edde84b09b3f2b9a6dba8a4175870a74de05f890bf50f4f5"></a> enumerator LIN\_WUP\_REPEAT\_200MS

    <a id="_CPPv4N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_220MSE"></a>

    <a id="_CPPv3N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_220MSE"></a> <a id="_CPPv2N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_220MSE"></a> <a id="lin__types_8h_1ac49334805c2eec4f8edde84b09b3f2b9a070e0a28573e5e6220fd58fabd5ccd6f"></a> enumerator LIN\_WUP\_REPEAT\_220MS

    <a id="_CPPv4N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_240MSE"></a>

    <a id="_CPPv3N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_240MSE"></a> <a id="_CPPv2N21lin_wup_repeat_time_t20LIN_WUP_REPEAT_240MSE"></a> <a id="lin__types_8h_1ac49334805c2eec4f8edde84b09b3f2b9a5ad4bbaac25c1f226d772a377fdad6c3"></a> enumerator LIN\_WUP\_REPEAT\_240MS

<a id="_CPPv48lin_id_t"></a>

<a id="_CPPv38lin_id_t"></a> <a id="_CPPv28lin_id_t"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bb"></a> enum lin\_id\_t
:   *Values:*

    <a id="_CPPv4N8lin_id_t13LIN_IDENT_MINE"></a>

    <a id="_CPPv3N8lin_id_t13LIN_IDENT_MINE"></a> <a id="_CPPv2N8lin_id_t13LIN_IDENT_MINE"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bbaacd3a70f3c3d51dab6bdef53b487c6fc"></a> enumerator LIN\_IDENT\_MIN

    <a id="_CPPv4N8lin_id_t10LIN_IDENT0E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT0E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT0E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bbaf06253c3b1bd86bfad0c84198b9c8674"></a> enumerator LIN\_IDENT0

    <a id="_CPPv4N8lin_id_t10LIN_IDENT1E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT1E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT1E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bbaded071afa1c2bb4fbb994d55de561c1e"></a> enumerator LIN\_IDENT1

    <a id="_CPPv4N8lin_id_t10LIN_IDENT2E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT2E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT2E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba8835cd8586597c3236a1907c8de0f77c"></a> enumerator LIN\_IDENT2

    <a id="_CPPv4N8lin_id_t10LIN_IDENT3E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT3E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT3E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba5520812cf4d6141aad0167e9692b89b3"></a> enumerator LIN\_IDENT3

    <a id="_CPPv4N8lin_id_t10LIN_IDENT4E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT4E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT4E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bbac17dd35ef503d69d3953ad021255f282"></a> enumerator LIN\_IDENT4

    <a id="_CPPv4N8lin_id_t10LIN_IDENT5E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT5E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT5E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bbac8801101543e2d08f0bc19d7face0c90"></a> enumerator LIN\_IDENT5

    <a id="_CPPv4N8lin_id_t10LIN_IDENT6E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT6E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT6E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba546a2c42500ce59fd08103ea7a69c138"></a> enumerator LIN\_IDENT6

    <a id="_CPPv4N8lin_id_t10LIN_IDENT7E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT7E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT7E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bbafc80f48dd125439a823372874a62a6c3"></a> enumerator LIN\_IDENT7

    <a id="_CPPv4N8lin_id_t10LIN_IDENT8E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT8E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT8E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba0b5158cc823eab2e62ababfe055911d9"></a> enumerator LIN\_IDENT8

    <a id="_CPPv4N8lin_id_t10LIN_IDENT9E"></a>

    <a id="_CPPv3N8lin_id_t10LIN_IDENT9E"></a> <a id="_CPPv2N8lin_id_t10LIN_IDENT9E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bbafbcf79d85a1ed1c8cb48be22f1478151"></a> enumerator LIN\_IDENT9

    <a id="_CPPv4N8lin_id_t11LIN_IDENT10E"></a>

    <a id="_CPPv3N8lin_id_t11LIN_IDENT10E"></a> <a id="_CPPv2N8lin_id_t11LIN_IDENT10E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba0d7cc66942d9096a2c7c54b48e980e1e"></a> enumerator LIN\_IDENT10

    <a id="_CPPv4N8lin_id_t11LIN_IDENT11E"></a>

    <a id="_CPPv3N8lin_id_t11LIN_IDENT11E"></a> <a id="_CPPv2N8lin_id_t11LIN_IDENT11E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba2d5c8747d69da2a3acc4c2523bf25f06"></a> enumerator LIN\_IDENT11

    <a id="_CPPv4N8lin_id_t11LIN_IDENT12E"></a>

    <a id="_CPPv3N8lin_id_t11LIN_IDENT12E"></a> <a id="_CPPv2N8lin_id_t11LIN_IDENT12E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba4722d359051674a5d09ceecaa10608b5"></a> enumerator LIN\_IDENT12

    <a id="_CPPv4N8lin_id_t11LIN_IDENT13E"></a>

    <a id="_CPPv3N8lin_id_t11LIN_IDENT13E"></a> <a id="_CPPv2N8lin_id_t11LIN_IDENT13E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bbaaf37675ba4c602960bc89ca07e706a2a"></a> enumerator LIN\_IDENT13

    <a id="_CPPv4N8lin_id_t11LIN_IDENT14E"></a>

    <a id="_CPPv3N8lin_id_t11LIN_IDENT14E"></a> <a id="_CPPv2N8lin_id_t11LIN_IDENT14E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba5f32b9d7b681c57f320fdb839a226889"></a> enumerator LIN\_IDENT14

    <a id="_CPPv4N8lin_id_t11LIN_IDENT15E"></a>

    <a id="_CPPv3N8lin_id_t11LIN_IDENT15E"></a> <a id="_CPPv2N8lin_id_t11LIN_IDENT15E"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba4f1ebc6d5d9c0553e97c3376e32237da"></a> enumerator LIN\_IDENT15

    <a id="_CPPv4N8lin_id_t13LIN_IDENT_MAXE"></a>

    <a id="_CPPv3N8lin_id_t13LIN_IDENT_MAXE"></a> <a id="_CPPv2N8lin_id_t13LIN_IDENT_MAXE"></a> <a id="lin__types_8h_1a37f309f378cf003f9d5fb7ccf9d195bba1535141e1e3a67a58e9dbd607cb6433d"></a> enumerator LIN\_IDENT\_MAX

<a id="_CPPv414lin_checksum_t"></a>

<a id="_CPPv314lin_checksum_t"></a> <a id="_CPPv214lin_checksum_t"></a> <a id="lin__types_8h_1a0f0aeceeef6ea12c9635f49c87fbd61c"></a> enum lin\_checksum\_t
:   *Values:*

    <a id="_CPPv4N14lin_checksum_t11LIN_CLASSICE"></a>

    <a id="_CPPv3N14lin_checksum_t11LIN_CLASSICE"></a> <a id="_CPPv2N14lin_checksum_t11LIN_CLASSICE"></a> <a id="lin__types_8h_1a0f0aeceeef6ea12c9635f49c87fbd61ca7adf6c9b7a3d143c8137be7aa8b444e2"></a> enumerator LIN\_CLASSIC

    <a id="_CPPv4N14lin_checksum_t12LIN_ENHANCEDE"></a>

    <a id="_CPPv3N14lin_checksum_t12LIN_ENHANCEDE"></a> <a id="_CPPv2N14lin_checksum_t12LIN_ENHANCEDE"></a> <a id="lin__types_8h_1a0f0aeceeef6ea12c9635f49c87fbd61caa466f26833f92bea73e74fae580a84d9"></a> enumerator LIN\_ENHANCED

<a id="_CPPv414lin_data_len_t"></a>

<a id="_CPPv314lin_data_len_t"></a> <a id="_CPPv214lin_data_len_t"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2"></a> enum lin\_data\_len\_t
:   *Values:*

    <a id="_CPPv4N14lin_data_len_t16LIN_DATA_LEN_MINE"></a>

    <a id="_CPPv3N14lin_data_len_t16LIN_DATA_LEN_MINE"></a> <a id="_CPPv2N14lin_data_len_t16LIN_DATA_LEN_MINE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2a7dc04bd8c7179ec2740b493c952ac5c3"></a> enumerator LIN\_DATA\_LEN\_MIN

    <a id="_CPPv4N14lin_data_len_t19LIN_DATA_LEN_1BYTESE"></a>

    <a id="_CPPv3N14lin_data_len_t19LIN_DATA_LEN_1BYTESE"></a> <a id="_CPPv2N14lin_data_len_t19LIN_DATA_LEN_1BYTESE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2a3feabfe42b087462f9bb091e6cd584e6"></a> enumerator LIN\_DATA\_LEN\_1BYTES

    <a id="_CPPv4N14lin_data_len_t19LIN_DATA_LEN_2BYTESE"></a>

    <a id="_CPPv3N14lin_data_len_t19LIN_DATA_LEN_2BYTESE"></a> <a id="_CPPv2N14lin_data_len_t19LIN_DATA_LEN_2BYTESE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2a1bbe5cef30d1b1a9f728d8003e8b13eb"></a> enumerator LIN\_DATA\_LEN\_2BYTES

    <a id="_CPPv4N14lin_data_len_t19LIN_DATA_LEN_3BYTESE"></a>

    <a id="_CPPv3N14lin_data_len_t19LIN_DATA_LEN_3BYTESE"></a> <a id="_CPPv2N14lin_data_len_t19LIN_DATA_LEN_3BYTESE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2ae23a29923885ec5cec400c0a1f214f53"></a> enumerator LIN\_DATA\_LEN\_3BYTES

    <a id="_CPPv4N14lin_data_len_t19LIN_DATA_LEN_4BYTESE"></a>

    <a id="_CPPv3N14lin_data_len_t19LIN_DATA_LEN_4BYTESE"></a> <a id="_CPPv2N14lin_data_len_t19LIN_DATA_LEN_4BYTESE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2a7d423b44b48de6edca897e1f9652b307"></a> enumerator LIN\_DATA\_LEN\_4BYTES

    <a id="_CPPv4N14lin_data_len_t19LIN_DATA_LEN_5BYTESE"></a>

    <a id="_CPPv3N14lin_data_len_t19LIN_DATA_LEN_5BYTESE"></a> <a id="_CPPv2N14lin_data_len_t19LIN_DATA_LEN_5BYTESE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2af2080c134a44c74ff7374b2b8f90614f"></a> enumerator LIN\_DATA\_LEN\_5BYTES

    <a id="_CPPv4N14lin_data_len_t19LIN_DATA_LEN_6BYTESE"></a>

    <a id="_CPPv3N14lin_data_len_t19LIN_DATA_LEN_6BYTESE"></a> <a id="_CPPv2N14lin_data_len_t19LIN_DATA_LEN_6BYTESE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2aa012c632310494d005f128afeaab461b"></a> enumerator LIN\_DATA\_LEN\_6BYTES

    <a id="_CPPv4N14lin_data_len_t19LIN_DATA_LEN_7BYTESE"></a>

    <a id="_CPPv3N14lin_data_len_t19LIN_DATA_LEN_7BYTESE"></a> <a id="_CPPv2N14lin_data_len_t19LIN_DATA_LEN_7BYTESE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2a16654e63a4d444c5422a4edb052a5b02"></a> enumerator LIN\_DATA\_LEN\_7BYTES

    <a id="_CPPv4N14lin_data_len_t19LIN_DATA_LEN_8BYTESE"></a>

    <a id="_CPPv3N14lin_data_len_t19LIN_DATA_LEN_8BYTESE"></a> <a id="_CPPv2N14lin_data_len_t19LIN_DATA_LEN_8BYTESE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2ac8e38090b7d106b8b0859906d94e44ac"></a> enumerator LIN\_DATA\_LEN\_8BYTES

    <a id="_CPPv4N14lin_data_len_t16LIN_DATA_LEN_MAXE"></a>

    <a id="_CPPv3N14lin_data_len_t16LIN_DATA_LEN_MAXE"></a> <a id="_CPPv2N14lin_data_len_t16LIN_DATA_LEN_MAXE"></a> <a id="lin__types_8h_1a0d61435a3be833cd8f9a6b5eee6aece2a6bd551b7c09bc39ea7b4bd065776298a"></a> enumerator LIN\_DATA\_LEN\_MAX

<a id="id2"></a>

### Header File

- [hal\_lin\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_lin_types.h)

<a id="id3"></a>

### Macros

<a id="c.LIN_RATE_20KBIT"></a>

<a id="hal__lin__types_8h_1a958a52e8fb8be8765603c5a6b10e0a5e"></a> LIN\_RATE\_20KBIT

<a id="c.LIN_CLK_26M"></a>

<a id="hal__lin__types_8h_1a1dd39e46fd937c10378749b824969652"></a> LIN\_CLK\_26M

<a id="c.LIN_BAUD_RATE_MIN"></a>

<a id="hal__lin__types_8h_1af65443ce33f7d894269342ba3e97fd61"></a> LIN\_BAUD\_RATE\_MIN

<a id="c.LIN_BAUD_RATE_MAX"></a>

<a id="hal__lin__types_8h_1a016f909338204c354486cbf3e438ffc2"></a> LIN\_BAUD\_RATE\_MAX

<a id="id4"></a>

### Enumerations

<a id="_CPPv49lin_dev_t"></a>

<a id="_CPPv39lin_dev_t"></a> <a id="_CPPv29lin_dev_t"></a> <a id="hal__lin__types_8h_1a1688ea67cbd309a5bf7a2da035a69607"></a> enum lin\_dev\_t
:   *Values:*

    <a id="_CPPv4N9lin_dev_t9LIN_SLAVEE"></a>

    <a id="_CPPv3N9lin_dev_t9LIN_SLAVEE"></a> <a id="_CPPv2N9lin_dev_t9LIN_SLAVEE"></a> <a id="hal__lin__types_8h_1a1688ea67cbd309a5bf7a2da035a69607a326ed930dc6417255e705aba8b7a55c1"></a> enumerator LIN\_SLAVE

    <a id="_CPPv4N9lin_dev_t10LIN_MASTERE"></a>

    <a id="_CPPv3N9lin_dev_t10LIN_MASTERE"></a> <a id="_CPPv2N9lin_dev_t10LIN_MASTERE"></a> <a id="hal__lin__types_8h_1a1688ea67cbd309a5bf7a2da035a69607a73a0e921bd2baed5e258f7035637709f"></a> enumerator LIN\_MASTER

<a id="_CPPv413lin_channel_t"></a>

<a id="_CPPv313lin_channel_t"></a> <a id="_CPPv213lin_channel_t"></a> <a id="hal__lin__types_8h_1af002607853db1aca4e8a8835547c5a0a"></a> enum lin\_channel\_t
:   *Values:*

    <a id="_CPPv4N13lin_channel_t10LIN_CHAN_0E"></a>

    <a id="_CPPv3N13lin_channel_t10LIN_CHAN_0E"></a> <a id="_CPPv2N13lin_channel_t10LIN_CHAN_0E"></a> <a id="hal__lin__types_8h_1af002607853db1aca4e8a8835547c5a0aad38377bd43705584e9b3c7e95e06b5ef"></a> enumerator LIN\_CHAN\_0
    :   lin gpio0/gpio1/gpuo2

    <a id="_CPPv4N13lin_channel_t10LIN_CHAN_1E"></a>

    <a id="_CPPv3N13lin_channel_t10LIN_CHAN_1E"></a> <a id="_CPPv2N13lin_channel_t10LIN_CHAN_1E"></a> <a id="hal__lin__types_8h_1af002607853db1aca4e8a8835547c5a0aad9aab998df8d9ff1cd60716f00aabe39"></a> enumerator LIN\_CHAN\_1
    :   lin gpio30/gpio31/gpuo42

    <a id="_CPPv4N13lin_channel_t10LIN_CHAN_2E"></a>

    <a id="_CPPv3N13lin_channel_t10LIN_CHAN_2E"></a> <a id="_CPPv2N13lin_channel_t10LIN_CHAN_2E"></a> <a id="hal__lin__types_8h_1af002607853db1aca4e8a8835547c5a0aa23d4e1ebab3678d585c50e7d54c32eb5"></a> enumerator LIN\_CHAN\_2
    :   lin gpio40/gpio41/gpuo42

    <a id="_CPPv4N13lin_channel_t12LIN_CHAN_MAXE"></a>

    <a id="_CPPv3N13lin_channel_t12LIN_CHAN_MAXE"></a> <a id="_CPPv2N13lin_channel_t12LIN_CHAN_MAXE"></a> <a id="hal__lin__types_8h_1af002607853db1aca4e8a8835547c5a0aa0131170ed127ec5299cd282fbab78754"></a> enumerator LIN\_CHAN\_MAX
