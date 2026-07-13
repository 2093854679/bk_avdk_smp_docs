# I2S


BK7259 CP 侧 I2S API（`include/driver/i2s.h`）。详细说明见
[I2S 开发指南](../../developer-guide/peripheral/bk_i2s.md "../../developer-guide/peripheral/bk_i2s.md")。


## I2S API Reference


### Header File


- [i2s.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/i2s.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/i2s.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_driver_init(void)
:   Init i2s module driver.

    This API init i2s driver :


    - Power on clock

    - config apll clock

    - enable interrupts

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_driver_deinit(void)
:   Deinit i2s module driver.

    This API deinit i2s driver :


    - Power down clock

    - reconfig apll clock to defailt value

    - disable interrupts

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_init([i2s_gpio_group_id_t](#_CPPv419i2s_gpio_group_id_t "i2s_gpio_group_id_t") id, const [i2s_config_t](#_CPPv412i2s_config_t "i2s_config_t") *config)
:   Init i2s module.

    This API init the i2s module:


    - Init gpios i2s used

    - Configure the i2s parameters

    Usage example:

    ```
    //init i2s driver
    bk_i2s_driver_init();

    //init i2s configure
    i2s_config_t i2s_config;
    i2s_config.i2s_en = I2S_DISABLE;
    i2s_config.role = I2S_ROLE_MASTER;
    i2s_config.work_mode = I2S_WORK_MODE_I2S;
    i2s_config.lrck_invert = I2S_LRCK_INVERT_DISABLE;
    i2s_config.sck_invert = I2S_SCK_INVERT_DISABLE;
    i2s_config.lsb_first_en = I2S_LSB_FIRST_DISABLE;
    i2s_config.sync_length = 0;
    i2s_config.data_length = 15;
    i2s_config.pcm_dlength = 0;
    i2s_config.sample_ratio = 0;
    i2s_config.sck_ratio = 0;
    i2s_config.parallel_en = I2S_PARALLEL_DISABLE;
    i2s_config.store_mode = I2S_LRCOM_STORE_16R16L;
    i2s_config.sck_ratio_h4b = 0;
    i2s_config.sample_ratio_h2b = 0;
    i2s_config.txint_level = I2S_TXINT_LEVEL_1;
    i2s_config.rxint_level = I2S_RXINT_LEVEL_1;
    bk_i2s_init(I2S_GPIO_GROUP_0, &i2s_config);
    CLI_LOGI("init i2s driver and config successful \r\n");
    ```

    参数
    :   - **id** – gpio config “GPIO6, GPIO7, GPIO8, GPIO9”/”GPIO40, GPIO41, GPIO42, GPIO43”

        - **config** – i2s parameters include work role, work mode and so on

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2S_PARAM: config is NULL

        - BK_ERR_I2S_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_deinit(void)
:   Deinit i2s module.

    This API deinit the i2s module:


    - reconfig i2s parameters to default value

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_get_read_ready(uint32_t *read_flag)
:   Get the i2s Rx fifo status.

    This API get the i2s Rx fifo status that check whether the fifo data can be read

    参数
    :   **read_flag** – save Rx fifo status

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2S_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_get_write_ready(uint32_t *write_flag)
:   Get the i2s Tx fifo status.

    This API get the i2s Tx fifo status that check whether the fifo data can be write

    参数
    :   **read_flag** – save Tx fifo status

    返回
    :   - BK_OK: succeed

        - BK_ERR_I2S_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_enable([i2s_en_t](#_CPPv48i2s_en_t "i2s_en_t") en_value)
:   Enable i2s.

    This API enable i2s

    参数
    :   **en_value** – disable/enable i2s

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_int_enable([i2s_isr_id_t](#_CPPv412i2s_isr_id_t "i2s_isr_id_t") int_id, uint32_t value)
:   Config i2s interrupt.

    This API config i2s interrupt

    参数
    :   - **int_id** – interrupt id

        - **value** – 0:disable 1:enable

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_role([i2s_role_t](#_CPPv410i2s_role_t "i2s_role_t") role)
:   Config i2s work role.

    This API config i2s work role

    参数
    :   **role** – work role slave/master

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_work_mode([i2s_work_mode_t](#_CPPv415i2s_work_mode_t "i2s_work_mode_t") work_mode)
:   Config i2s work mode.

    This API config i2s work mode

    参数
    :   **work_mode** – i2s work mode

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_lrck_invert([i2s_lrck_invert_en_t](#_CPPv420i2s_lrck_invert_en_t "i2s_lrck_invert_en_t") lrckrp)
:   Config i2s lrck invert.

    This API config i2s lrck invert

    参数
    :   **lrckrp** – i2s lrck invert enable/disable

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_sck_invert([i2s_sck_invert_en_t](#_CPPv419i2s_sck_invert_en_t "i2s_sck_invert_en_t") sck_invert)
:   Config i2s sck invert.

    This API config i2s sck invert

    参数
    :   **sck_invert** – i2s sck invert enable/disable

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_lsb_first([i2s_lsb_first_en_t](#_CPPv418i2s_lsb_first_en_t "i2s_lsb_first_en_t") lsb_first)
:   Config i2s lsb first.

    This API config i2s lsb first

    参数
    :   **lsb_first** – i2s lsb first enable/disable

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_sync_len(uint32_t sync_len)
:   Config i2s sync length.

    This API config i2s sync length

    参数
    :   **sync_len** – i2s sync length

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_data_len(uint32_t data_len)
:   Config i2s data length.

    This API config i2s data length

    参数
    :   **data_len** – i2s data length

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_pcm_dlen(uint32_t pcm_dlen)
:   Config i2s pcm D length of 2B+D.

    This API config i2s pcm D length of 2B+D

    参数
    :   **pcm_dlen** – pcm D length

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_store_mode([i2s_lrcom_store_mode_t](#_CPPv422i2s_lrcom_store_mode_t "i2s_lrcom_store_mode_t") store_mode)
:   Config i2s store mode.

    This API config i2s store mode


    **Attention**
    :   1. LRLR mode: left and right channel data are written alternately in chronological order(L->R->L->R->……)


    **Attention**
    :   2. 16R16L mode: left and right channel data are written to FIFO in 32 bits, in which the lower 16 bits correspond to the left channel and the higher 16 bits correspond to the right channel({R,L}->{R,L}->……)

    参数
    :   **store_mode** – lrcom store mode LRLR/16R16L

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_clear_rxfifo(void)
:   clear i2s rx fifo

    This API clear i2s rx fifo

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_clear_txfifo(void)
:   clear i2s tx fifo

    This API clear i2s tx fifo

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_txint_level([i2s_txint_level_t](#_CPPv417i2s_txint_level_t "i2s_txint_level_t") txint_level)
:   config i2s tx interrupt level

    This API config i2s tx interrupt level

    参数
    :   **txint_level** – tx interrupt trigger level

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_rxint_level([i2s_rxint_level_t](#_CPPv417i2s_rxint_level_t "i2s_rxint_level_t") rxint_level)
:   config i2s rx interrupt level

    This API config i2s rx interrupt level

    参数
    :   **rxint_level** – rx interrupt trigger level

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_write_data(uint32_t channel_id, uint32_t *data_buf, uint32_t data_len)
:   write data to i2s tx fifo

    This API write data to i2s tx fifo

    Usage example:

    ```
    //init i2s driver
    bk_i2s_driver_init();

    //init i2s configure
    i2s_config.i2s_en = I2S_DISABLE;
    i2s_config.role = I2S_ROLE_MASTER;
    i2s_config.work_mode = I2S_WORK_MODE_I2S;
    i2s_config.lrck_invert = I2S_LRCK_INVERT_DISABLE;
    i2s_config.sck_invert = I2S_SCK_INVERT_DISABLE;
    i2s_config.lsb_first_en = I2S_LSB_FIRST_DISABLE;
    i2s_config.sync_length = 0;
    i2s_config.data_length = 15;
    i2s_config.pcm_dlength = 0;
    i2s_config.sample_ratio = 0;
    i2s_config.sck_ratio = 0;
    i2s_config.parallel_en = I2S_PARALLEL_DISABLE;
    i2s_config.store_mode = I2S_LRCOM_STORE_16R16L;
    i2s_config.sck_ratio_h4b = 0;
    i2s_config.sample_ratio_h2b = 0;
    i2s_config.txint_level = I2S_TXINT_LEVEL_1;
    i2s_config.rxint_level = I2S_RXINT_LEVEL_1;
    bk_i2s_init(I2S_GPIO_GROUP_0, &i2s_config);
    CLI_LOGI("init i2s driver and config successful \r\n");

    //set sample and bitclk ratio
    rate.datawidth = i2s_rate_table[i].datawidth;
    rate.samp_rate = i2s_rate_table[i].samp_rate;
    bk_i2s_set_ratio(&rate);

    //enable i2s
    bk_i2s_enable(I2S_ENABLE);
    CLI_LOGI("enable i2s successful \r\n");

    bk_i2s_get_write_ready(&write_flag);
    if (write_flag)
        bk_i2s_write_data(1, &data_buf_rl, 1);
    ```

    Usage example:

    ```
    //init i2s driver
    bk_i2s_driver_init();

    //init i2s configure
    i2s_config_t i2s_config;
    i2s_config.i2s_en = I2S_DISABLE;
    i2s_config.role = I2S_ROLE_MASTER;
    i2s_config.work_mode = I2S_WORK_MODE_I2S;
    i2s_config.lrck_invert = I2S_LRCK_INVERT_DISABLE;
    i2s_config.sck_invert = I2S_SCK_INVERT_DISABLE;
    i2s_config.lsb_first_en = I2S_LSB_FIRST_DISABLE;
    i2s_config.sync_length = 0;
    i2s_config.data_length = 15;
    i2s_config.pcm_dlength = 0;
    i2s_config.sample_ratio = 0;
    i2s_config.sck_ratio = 0;
    i2s_config.parallel_en = I2S_PARALLEL_DISABLE;
    i2s_config.store_mode = I2S_LRCOM_STORE_16R16L;
    i2s_config.sck_ratio_h4b = 0;
    i2s_config.sample_ratio_h2b = 0;
    i2s_config.txint_level = I2S_TXINT_LEVEL_1;
    i2s_config.rxint_level = I2S_RXINT_LEVEL_1;
    bk_i2s_init(I2S_GPIO_GROUP_0, &i2s_config);
    CLI_LOGI("init i2s driver and config successful \r\n");

    //set sample and bitclk ratio
    rate.datawidth = i2s_rate_table[i].datawidth;
    rate.samp_rate = i2s_rate_table[i].samp_rate;
    bk_i2s_set_ratio(&rate);

    //enable i2s
    bk_i2s_enable(I2S_ENABLE);
    CLI_LOGI("enable i2s successful \r\n");

    //get write ready status and write data
    bk_i2s_get_write_ready(&write_flag);
    if (write_flag)
        bk_i2s_write_data(1, &data_buf_rl, 1);
    ```

    参数
    :   - **channel_id** – i2s channel 1/2/3/4

        - **data_buf** – data to write

        - **data_len** – data length to write

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_read_data(uint32_t *data_buf, uint32_t data_len)
:   read data from i2s rx fifo

    This API read data from i2s rx fifo

    Usage example:

    ```
    //init i2s driver
    bk_i2s_driver_init();

    //init i2s configure
    i2s_config_t i2s_config;
    i2s_config.i2s_en = I2S_DISABLE;
    i2s_config.role = I2S_ROLE_MASTER;
    i2s_config.work_mode = I2S_WORK_MODE_I2S;
    i2s_config.lrck_invert = I2S_LRCK_INVERT_DISABLE;
    i2s_config.sck_invert = I2S_SCK_INVERT_DISABLE;
    i2s_config.lsb_first_en = I2S_LSB_FIRST_DISABLE;
    i2s_config.sync_length = 0;
    i2s_config.data_length = 15;
    i2s_config.pcm_dlength = 0;
    i2s_config.sample_ratio = 0;
    i2s_config.sck_ratio = 0;
    i2s_config.parallel_en = I2S_PARALLEL_DISABLE;
    i2s_config.store_mode = I2S_LRCOM_STORE_16R16L;
    i2s_config.sck_ratio_h4b = 0;
    i2s_config.sample_ratio_h2b = 0;
    i2s_config.txint_level = I2S_TXINT_LEVEL_1;
    i2s_config.rxint_level = I2S_RXINT_LEVEL_1;
    bk_i2s_init(I2S_GPIO_GROUP_0, &i2s_config);
    CLI_LOGI("init i2s driver and config successful \r\n");

    //set sample and bitclk ratio
    rate.datawidth = i2s_rate_table[i].datawidth;
    rate.samp_rate = i2s_rate_table[i].samp_rate;
    bk_i2s_set_ratio(&rate);

    //enable i2s
    bk_i2s_enable(I2S_ENABLE);
    CLI_LOGI("enable i2s successful \r\n");

    //get read ready status and read data
    bk_i2s_get_read_ready(&read_flag);
    if (read_flag)
        bk_i2s_read_data(&data_buf, 1);
    ```

    参数
    :   - **data_buf** – save data read from rx fifo

        - **data_len** – data length to read

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_get_data_addr([i2s_channel_id_t](#_CPPv416i2s_channel_id_t "i2s_channel_id_t") chl_id, uint32_t *i2s_data_addr)
:   get i2s data address

    This API get i2s data address

    参数
    :   **i2s_data_addr** – save i2s data address

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_set_samp_rate([i2s_samp_rate_t](#_CPPv415i2s_samp_rate_t "i2s_samp_rate_t") samp_rate)
:   config i2s sample rate

    This API config i2s sample rate

    参数
    :   **rate** – sample rate and data width

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_register_i2s_isr([i2s_isr_id_t](#_CPPv412i2s_isr_id_t "i2s_isr_id_t") isr_id, [i2s_isr_t](#_CPPv49i2s_isr_t "i2s_isr_t") isr, void *param)
:   register i2s isr

    This API config register i2s isr

    Usage example:

    ```
    void cli_i2s_master_txudf_isr(void *param)
    {
        CLI_LOGI("enter cli_i2s_txudf_isr \r\n");
    }

    //register isr
    bk_i2s_register_i2s_isr(I2S_ISR_CHL1_TXUDF, cli_i2s_master_txudf_isr, NULL);
    CLI_LOGI("register i2s isr successful \r\n");

    //enable i2s rxovf interrupt
    bk_i2s_int_enable(I2S_ISR_CHL1_TXUDF, I2S_INT_ENABLE);
    CLI_LOGI("enable i2s interrupt successful \r\n");
    ```

    参数
    :   - **isr_id** – i2s isr id

        - **isr** – isr function

        - **param** – isr parameters

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - BK_ERR_I2S_ISR_ID: i2s isr id is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_chl_init([i2s_channel_id_t](#_CPPv416i2s_channel_id_t "i2s_channel_id_t") chl, [i2s_txrx_type_t](#_CPPv415i2s_txrx_type_t "i2s_txrx_type_t") type, uint32_t buff_size, [i2s_data_handle_cb](#_CPPv418i2s_data_handle_cb "i2s_data_handle_cb") data_handle_cb, RingBufferContext **rb)
:   init i2s channel to send or receive data by dma

    This API config dma to carry i2s data

    参数
    :   **chl** – i2s channel @type Tx or Rx config @buff_size the size(byte) of ring buffer to send or receive data @data_handle_cb the callback called by dma finish isr when dma carry “buff_size/2” data complete @rb save RingBufferContext, and send or receive data use it

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_chl_deinit([i2s_channel_id_t](#_CPPv416i2s_channel_id_t "i2s_channel_id_t") chl, [i2s_txrx_type_t](#_CPPv415i2s_txrx_type_t "i2s_txrx_type_t") type)
:   deinit i2s channel

    This API config dma to carry i2s data

    参数
    :   **chl** – i2s channel @type Tx or Rx config

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_start(void)
:   start i2s

    This API start dma and i2s to send and receive data

    Usage example:

    ```
    static RingBufferContext *ch1_tx_rb;

    //channel 1 tx callback
    static int ch1_tx_data_handle_cb(uint32_t size)
    {
        ring_buffer_write(ch1_tx_rb, ch1_temp, size);
        return size;
    }

    i2s_config_t i2s_config = DEFAULT_I2S_CONFIG();
    //init i2s driver
    bk_i2s_driver_init();
    //init and config i2s
    bk_i2s_init(I2S_GPIO_GROUP_0, &i2s_config);
    bk_i2s_chl_init(I2S_CHANNEL_1, I2S_TXRX_TYPE_TX, 640, ch1_tx_data_handle_cb, &ch1_tx_rb);
    uint8_t *temp_data = (uint8_t *)os_malloc(640);
    os_memset(temp_data, 0x00, 640);
    size = ring_buffer_write(ch1_tx_rb, temp_data, 640);
    BK_LOGD(NULL,"ring_buffer_write, size: %d \n", size);
    os_free(temp_data);
    bk_i2s_start();
    ```

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - BK_ERR_I2S_ISR_ID: i2s isr id is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_i2s_stop(void)
:   stop i2s

    This API stop i2s and dma to carry i2s data

    Usage example:

    ```
    bk_i2s_stop();
    bk_i2s_chl_deinit(I2S_CHANNEL_1, I2S_TXRX_TYPE_TX);
    bk_i2s_deinit();
    bk_i2s_driver_deinit();
    ```

    返回
    :   - BK_OK: succeed

        - BK_ERR_AUD_NOT_INIT: i2s driver is not init

        - others: other errors.


## I2S API Typedefs


### Header File


- [i2s_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/i2s_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/i2s_types.h")


### Structures

struct i2s_int_config_t

struct i2s_config_t


### Macros

BK_ERR_I2S_NOT_INIT
:   I2S driver not init

BK_ERR_I2S_PARAM
:   I2S parameter invalid

BK_ERR_I2S_ISR_ID
:   I2S isr id invalid

DEFAULT_I2S_CONFIG()

DEFAULT_PCM_CONFIG()

DEFAULT_TDM_CONFIG()

DEFAULT_2BD_CONFIG()


### Type Definitions

typedef void (*i2s_isr_t)(void *param)

typedef int (*i2s_data_handle_cb)(uint32_t size)


### Enumerations

enum i2s_gpio_group_id_t
:   *Values:*

    enumerator I2S_GPIO_GROUP_0
    :   I2S gpio group 0: GPIO6, GPIO7, GPIO8, GPIO9

    enumerator I2S_GPIO_GROUP_1
    :   I2S gpio group 1: GPIO40, GPIO41, GPIO42, GPIO43

    enumerator I2S_GPIO_GROUP_2
    :   I2S gpio group 2: GPIO44, GPIO45, GPIO46, GPIO47

    enumerator I2S_GPIO_GROUP_MAX

enum i2s_isr_id_t
:   *Values:*

    enumerator I2S_ISR_CHL1_TXUDF
    :   I2S channel1 tx_udf interrupt

    enumerator I2S_ISR_CHL1_RXOVF
    :   I2S channel1 rx_ovf interrupt

    enumerator I2S_ISR_CHL1_TXINT
    :   I2S channel1 tx interrupt

    enumerator I2S_ISR_CHL1_RXINT
    :   I2S channel1 rx interrupt

    enumerator I2S_ISR_CHL2_TXUDF
    :   I2S channel2 tx_udf interrupt

    enumerator I2S_ISR_CHL2_RXOVF
    :   I2S channel2 rx_ovf interrupt

    enumerator I2S_ISR_CHL2_TXINT
    :   I2S channel2 tx interrupt

    enumerator I2S_ISR_CHL2_RXINT
    :   I2S channel2 rx interrupt

    enumerator I2S_ISR_CHL3_TXUDF
    :   I2S channel3 tx_udf interrupt

    enumerator I2S_ISR_CHL3_RXOVF
    :   I2S channel3 rx_ovf interrupt

    enumerator I2S_ISR_CHL3_TXINT
    :   I2S channel3 tx interrupt

    enumerator I2S_ISR_CHL3_RXINT
    :   I2S channel3 rx interrupt

    enumerator I2S_ISR_MAX

enum i2s_en_t
:   *Values:*

    enumerator I2S_DISABLE
    :   I2S disable

    enumerator I2S_ENABLE
    :   I2S enable

    enumerator I2S_EN_MAX

enum i2s_role_t
:   *Values:*

    enumerator I2S_ROLE_SLAVE
    :   I2S role: slave

    enumerator I2S_ROLE_MASTER
    :   I2S role: master

    enumerator I2S_ROLE_MAX

enum i2s_work_mode_t
:   *Values:*

    enumerator I2S_WORK_MODE_I2S
    :   I2S work mode: I2S (Philips)

    enumerator I2S_WORK_MODE_LEFTJUST
    :   I2S work mode: Left Justified

    enumerator I2S_WORK_MODE_RIGHTJUST
    :   I2S work mode: Right Justified

    enumerator I2S_WORK_MODE_RSVD
    :   I2S work mode: reserved for future use

    enumerator I2S_WORK_MODE_SHORTFAMSYNC
    :   I2S work mode: Short Frame Sync

    enumerator I2S_WORK_MODE_LONGFAMSYNC
    :   I2S work mode: Long Frame Sync

    enumerator I2S_WORK_MODE_NORMAL2BD
    :   I2S work mode: Normal 2B+D

    enumerator I2S_WORK_MODE_DELAY2BD
    :   I2S work mode: Delay 2B+D

    enumerator I2S_WORK_MODE_MAX

enum i2s_lrck_invert_en_t
:   *Values:*

    enumerator I2S_LRCK_INVERT_DISABLE
    :   I2S lrck invert disable

    enumerator I2S_LRCK_INVERT_ENABLE
    :   I2S lrck invert enable

    enumerator I2S_LRCK_INVERT_MAX

enum i2s_sck_invert_en_t
:   *Values:*

    enumerator I2S_SCK_INVERT_DISABLE
    :   I2S sck invert disable

    enumerator I2S_SCK_INVERT_ENABLE
    :   I2S sck invert enable

    enumerator I2S_SCK_INVERT_MAX

enum i2s_lsb_first_en_t
:   *Values:*

    enumerator I2S_LSB_FIRST_DISABLE
    :   I2S lsb first disable

    enumerator I2S_LSB_FIRST_ENABLE
    :   I2S lsb first enable

    enumerator I2S_LSB_FIRST_EN_MAX

enum i2s_parallel_en_t
:   *Values:*

    enumerator I2S_PARALLEL_DISABLE
    :   I2S parallel disable

    enumerator I2S_PARALLEL_ENABLE
    :   I2S parallel enable

    enumerator I2S_PARALLEL_EN_MAX

enum i2s_lrcom_store_mode_t
:   *Values:*

    enumerator I2S_LRCOM_STORE_LRLR
    :   I2S lrcom store mode: L->R->L->R

    enumerator I2S_LRCOM_STORE_16R16L
    :   I2S lrcom store mode: {16bitR,16bitL}

    enumerator I2S_LRCOM_STORE_MODE_MAX

enum i2s_txint_level_t
:   *Values:*

    enumerator I2S_TXINT_LEVEL_1
    :   I2S tx_int level: 1

    enumerator I2S_TXINT_LEVEL_8
    :   I2S tx_int level: 8

    enumerator I2S_TXINT_LEVEL_16
    :   I2S tx_int level: 16

    enumerator I2S_TXINT_LEVEL_24
    :   I2S tx_int level: 24

    enumerator I2S_TXINT_LEVEL_MAX

enum i2s_rxint_level_t
:   *Values:*

    enumerator I2S_RXINT_LEVEL_1
    :   I2S rx_int level: 1

    enumerator I2S_RXINT_LEVEL_8
    :   I2S rx_int level: 8

    enumerator I2S_RXINT_LEVEL_16
    :   I2S rx_int level: 16

    enumerator I2S_RXINT_LEVEL_24
    :   I2S rx_int level: 24

    enumerator I2S_RXINT_LEVEL_MAX

enum i2s_int_en_t
:   *Values:*

    enumerator I2S_INT_DISABLE
    :   I2S interrupt disable

    enumerator I2S_INT_ENABLE
    :   I2S interrupt enable

    enumerator I2S_INT_EN_MAX

enum i2s_channel_id_t
:   *Values:*

    enumerator I2S_CHANNEL_1
    :   I2S channel: 1

    enumerator I2S_CHANNEL_2
    :   I2S channel: 2

    enumerator I2S_CHANNEL_3
    :   I2S channel: 3

    enumerator I2S_CHANNEL_MAX

enum i2s_data_width_t
:   *Values:*

    enumerator I2S_DATA_WIDTH_8
    :   I2S data width: 8

    enumerator I2S_DATA_WIDTH_16
    :   I2S data width: 16

    enumerator I2S_DATA_WIDTH_24
    :   I2S data width: 24

    enumerator I2S_DATA_WIDTH_32
    :   I2S data width: 32

enum i2s_samp_rate_t
:   *Values:*

    enumerator I2S_SAMP_RATE_8000
    :   I2S sample rate: 8K

    enumerator I2S_SAMP_RATE_12000
    :   I2S sample rate: 12K

    enumerator I2S_SAMP_RATE_16000
    :   I2S sample rate: 16K

    enumerator I2S_SAMP_RATE_24000
    :   I2S sample rate: 24K

    enumerator I2S_SAMP_RATE_32000
    :   I2S sample rate: 32K

    enumerator I2S_SAMP_RATE_48000
    :   I2S sample rate: 48K

    enumerator I2S_SAMP_RATE_96000
    :   I2S sample rate: 96K

    enumerator I2S_SAMP_RATE_8018
    :   I2S sample rate: 8.0182K

    enumerator I2S_SAMP_RATE_11025
    :   I2S sample rate: 11.025K

    enumerator I2S_SAMP_RATE_22050
    :   I2S sample rate: 22.050K

    enumerator I2S_SAMP_RATE_44100
    :   I2S sample rate: 44.1K

    enumerator I2S_SAMP_RATE_88200
    :   I2S sample rate: 88.2K

    enumerator I2S_SAMP_RATE_MAX

enum i2s_txrx_type_t
:   *Values:*

    enumerator I2S_TXRX_TYPE_TX

    enumerator I2S_TXRX_TYPE_RX

    enumerator I2S_TXRX_TYPE_MAX
