---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/multicore_communication/bk_api_uart.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="uart"></a>

# 多核通讯-Uart通讯接口

<a id="id1"></a>

## 1 功能概述

- Uart通讯接口基于Mailbox, 模拟出了一个带自动流控的UART, 如下所示:

<a id="id3"></a>
![Mailbox Uart](../../../_assets/0e38d5d019e78e4235db-mailbox_uart.png)


Virtual Uart Based on Mailbox

<a id="ap"></a>

## 2 AP侧代码路径

> - 驱动源码路径：
>   :   `ap\middleware\driver\mailbox\mb_uart_driver.c`

<a id="cp"></a>

## 3 CP侧代码路径

> - 驱动源码路径：
>   :   `cp\middleware\driver\mailbox\mb_uart_driver.c`

<a id="id2"></a>

## 4 Uart通讯接口

默认实现了两个MB\_UART:

```
enum
{
    MB_UART0 = 0,
    MB_UART1,
    MB_UART_MAX,
};

//MB_UART的接收状态：
#define MB_UART_STATUS_OVF                  0x01
#define MB_UART_STATUS_PARITY_ERR   0x02

typedef void (* mb_uart_isr_t)(void * param);

/// 2.1  bk_mb_uart_dev_init
/**
* @brief      initialize the mailbox UART device.
*
* Initialize the mailbox-emulated UART.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
*
* @return
*  - BK_OK: initialized success.
*  - other: failed, fail code.
*/
bk_err_t bk_mb_uart_dev_init(u8 id);


/// 2.2  bk_mb_uart_dev_deinit
/**
* @brief      de-initialize the mailbox UART device.
*
* De-initialize the mailbox-emulated UART.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
*
* @return
*  - BK_OK: initialized success.
*  - other: failed, fail code.
*/
bk_err_t bk_mb_uart_dev_deinit(u8 id);


/// 2.3  bk_mb_uart_register_rx_isr
/**
* @brief      register rx ISR callback to the mailbox UART device.
*
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
*
* @isr    rx isr, prototype is void (* mb_uart_isr_t)(void * param)
*
* @param  will be passed to rx isr callback.
*
* @attention   isr callback is called in interrupt disabled context, when received data.
*
* @return
*  - BK_OK: success.
*  - other: failed, fail code.
*/
bk_err_t bk_mb_uart_register_rx_isr(u8 id, mb_uart_isr_t isr, void *param);


/// 2.4  bk_mb_uart_register_tx_isr
/**
* @brief      register tx ISR callback to the mailbox UART device.
*
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
*
* @isr    tx isr, prototype is void (* mb_uart_isr_t)(void * param)
*
* @param  will be passed to tx isr callback.
*
* @attention   isr callback is called in interrupt disabled context, after sent cmpelete.
*
* @return
*  - BK_OK: success.
*  - other: failed, fail code.
*/
bk_err_t bk_mb_uart_register_tx_isr(u8 id, mb_uart_isr_t isr, void *param);


/// 2.5  bk_mb_uart_write_ready
/**
* @brief      get free FIFO space in UART device.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
*
* @return
*  - free FIFO space size in byte.
*/
u16 bk_mb_uart_write_ready(u8 id);


/// 2.6  bk_mb_uart_read_ready
/**
* @brief      get data bytes in FIFO of UART device.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
*
* @return
*  - data bytes ready in mailbox-UART FIFO.
*/
u16 bk_mb_uart_read_ready(u8 id);


/// 2.7  bk_mb_uart_write_byte
/**
* @brief      send one byte data via UART device.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
* @data   data byte to be sent.
*
* @return
*  - data bytes sent via mailbox-UART (1 or 0).
*/
u16 bk_mb_uart_write_byte(u8 id, u8 data);


/// 2.8  bk_mb_uart_write
/**
* @brief      send data in buffer via UART device.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
* @data_buf   data to be sent.
* @data_len   data bytes in buffer.
*
* @return
*  - data bytes sent via mailbox-UART (0 ~ data_len).
*/
u16 bk_mb_uart_write(u8 id, u8 *data_buf, u16 data_len);


/// 2.9  bk_mb_uart_read_byte
/**
* @brief      receive one byte data via UART device.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
* @data   data buffer to receive one byte.
*
* @return
*  - data bytes received via mailbox-UART (1 or 0).
*/
u16 bk_mb_uart_read_byte(u8 id, u8 * data);


/// 2.10  bk_mb_uart_read
/**
* @brief      receive data via UART device.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
* @data_buf   used to receive data.
* @buf_len    buffer length.
*
* @return
*  - data bytes received via mailbox-UART (0 ~ buf_len).
*/
u16 bk_mb_uart_read(u8 id, u8 *data_buf, u16 buf_len);


/// 2.11  bk_mb_uart_is_tx_over
/**
* @brief      check whether data has been flushed out to UART device.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
*
* @return
*  - 1 : no data is pending in Tx FIFO.
*  - 0 : there are data pending in Tx FIFO.
*/
bool bk_mb_uart_is_tx_over(u8 id);


/// 2.12  bk_mb_uart_get_status
/**
* @brief      get status of UART device.
*
* @id     mailbox uart ID (MB_UART0, MB_UART1).
*
* @return
*  - uart rx/tx status (0, MB_UART_STATUS_OVF, MB_UART_STATUS_PARITY_ERR, or bitwise of these 2 status.).
*/
u16 bk_mb_uart_get_status(u8 id);
```

使用例子：

从接口到行为, 这个MB\_UART都类似于常规的UART设备, 除了一点: MB\_UART基于mailbox的逻辑通道, 而逻辑通道的通讯依赖于mailbox硬件中断的通知,
因此MB\_UART的实现依赖于系统的中断和mailbox硬件中断, 也就是在系统关中断情况下MB\_UART无法工作。
(尽管MB\_UART可以轮询方式使用, 那也只是说可以不向MB\_UART注册Tx/Rx ISR回调函数, 而不是真正意义上的关中断轮询方式。)

> - 在系统启动时候, 或者业务模块启动初始化时候, 先初始化MB\_UART设备:
>
>   ```
>   bk_mb_uart_dev_init(MB_UART0);
>   ```
> - 如果工作在中断通知方式下, 在业务task的初始化模块中向MB\_UART注册Tx/Rx ISR回调函数:
>
>   ```
>   struct mb_uart_rx_param
>   {
>       u8     uart_id;
>       beken_semaphore_t       rx_sema
>   } dev_rx_param;
>   struct mb_uart_tx_param
>   {
>       u8     uart_id;
>       beken_semaphore_t       tx_sema
>   } dev_tx_param;
>
>   bk_mb_uart_register_rx_isr(MB_UART0, debug_mb_uart_rx_callback, &dev_rx_param);
>   bk_mb_uart_register_tx_isr(MB_UART0, debug_mb_uart_tx_callback, &dev_tx_param);
>   ```
> - 回调函数的原型是:
>
>   ```
>   void (* mb_uart_isr)(void * param)
>
>   static void debug_mb_uart_rx_callback(void * param)
>   {
>       struct mb_uart_param * mbu_para = (struct mb_uart_rx_param *)param;
>
>       rtos_set_semaphore(&mbu_para-> rx_sema);  // 通知数据到达
>
>       BK_LOGI(TAG," MB_Uart:%d Rx OK\r\n", mbu_para->uart_id);
>   }
>
>   static void debug_mb_uart_tx_callback(void * param)
>   {
>       struct mb_uart_param * mbu_para = (struct mb_uart_tx_param *)param;
>
>       rtos_set_semaphore(&mbu_para-> tx_sema);  // 通知数据发送完成
>
>       BK_LOGI(TAG," MB_Uart:%d Tx OK\r\n", mbu_para->uart_id);
>   }
>   ```
> - 业务task 收到数据到达通知后用以下API获知MB\_UART状态并接收数据:
>
>   ```
>   rtos_get_semaphore(&mbu_para-> rx_sema, BEKEN_WAIT_FOREVER);
>
>   u8          test_buf[80];
>   temp = bk_mb_uart_get_status(uart_id);
>   BK_LOGI(TAG,"m_uart%d state:%d \r\n", uart_id, temp);
>
>   temp = bk_mb_uart_read_ready(uart_id);
>   BK_LOGI(TAG,"m_uart%d RxFIFO data:%d bytes\r\n", uart_id, temp);
>
>   while(temp > 0)
>   {
>       rd_len = bk_mb_uart_read(uart_id, test_buf, sizeof(test_buf));
>
>       BK_LOGI(TAG,"rx:%d bytes\r\n", rd_len);
>       // BK_LOGI(TAG,"rx:%s \r\n", test_buf);
>
>       for(i = 0; i < rd_len; )
>       {
>           if(rd_len - i >= 8)
>           {
>               os_printf(" %x %x %x %x %x %x %x %x\r\n", test_buf[i], test_buf[i+1],test_buf[i+2],test_buf[i+3],
>                   test_buf[i+4],test_buf[i+5],test_buf[i+6],test_buf[i+7]);
>               i+= 8;
>           }
>           else
>           {
>               os_printf(" %x", test_buf[i]);
>               i++;
>           }
>       }
>       os_printf("\r\n");
>
>       // temp -= rd_len;
>       temp = bk_mb_uart_read_ready(uart_id);
>   }
>   ```
> - 业务task 收到数据发送完成通知后用以下API继续数据发送:
>
>   ```
>   rtos_get_semaphore(&mbu_para->tx_sema, BEKEN_WAIT_FOREVER);
>
>   do
>   {
>       if (bk_mb_uart_write_ready(uart_id) == 0)  // Tx FIFO has space for new data?
>           rtos_delay_milliseconds(2);
>
>       temp = bk_mb_uart_write(uart_id, data_buf, data_len);
>
>       BK_LOGI(TAG,"m_uart%d tx:%d bytes \r\n", uart_id, temp);
>       data_len -= temp;
>
>   } while(data_len > 0);
>   ```
