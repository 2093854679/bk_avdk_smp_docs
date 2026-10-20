---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_i2s.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="i2s"></a>

# I2S

BK7259 CP 侧 I2S API（`include/driver/i2s.h`）。详细说明见
[I2S 开发指南](../../developer-guide/peripheral/bk_i2s.md)。

<a id="i2s-api-reference"></a>

## I2S API Reference

<a id="header-file"></a>

### Header File

- [i2s.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/i2s.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_i2s_driver_initv"></a>

<a id="_CPPv318bk_i2s_driver_initv"></a> <a id="_CPPv218bk_i2s_driver_initv"></a> <a id="bk_i2s_driver_init__void"></a> <a id="group__bk__api__i2s_1ga98f8ce5e1decfab56000d63f4a952c29"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_driver\_init(void)
:   Init i2s module driver.

    This API init i2s driver :

    - Power on clock
    - config apll clock
    - enable interrupts

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_i2s_driver_deinitv"></a>

<a id="_CPPv320bk_i2s_driver_deinitv"></a> <a id="_CPPv220bk_i2s_driver_deinitv"></a> <a id="bk_i2s_driver_deinit__void"></a> <a id="group__bk__api__i2s_1gad4e4c62483659f0225edd981ec0e8637"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_driver\_deinit(void)
:   Deinit i2s module driver.

    This API deinit i2s driver :

    - Power down clock
    - reconfig apll clock to defailt value
    - disable interrupts

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_i2s_init19i2s_gpio_group_id_tPK12i2s_config_t"></a>

<a id="_CPPv311bk_i2s_init19i2s_gpio_group_id_tPK12i2s_config_t"></a> <a id="_CPPv211bk_i2s_init19i2s_gpio_group_id_tPK12i2s_config_t"></a> <a id="bk_i2s_init__i2s_gpio_group_id_t.i2s_config_tCP"></a> <a id="group__bk__api__i2s_1ga4b461679e7bc688e0927d68d6cf80afd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_init([i2s\_gpio\_group\_id\_t](#_CPPv419i2s_gpio_group_id_t "i2s_gpio_group_id_t") id, const [i2s\_config\_t](#_CPPv412i2s_config_t "i2s_config_t") \*config)
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
    :   - BK\_OK: succeed
        - BK\_ERR\_I2S\_PARAM: config is NULL
        - BK\_ERR\_I2S\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv413bk_i2s_deinitv"></a>

<a id="_CPPv313bk_i2s_deinitv"></a> <a id="_CPPv213bk_i2s_deinitv"></a> <a id="bk_i2s_deinit__void"></a> <a id="group__bk__api__i2s_1gaf40fa1faece9fceb44e8833b15a03d9e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_deinit(void)
:   Deinit i2s module.

    This API deinit the i2s module:

    - reconfig i2s parameters to default value

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_i2s_get_read_readyP8uint32_t"></a>

<a id="_CPPv321bk_i2s_get_read_readyP8uint32_t"></a> <a id="_CPPv221bk_i2s_get_read_readyP8uint32_t"></a> <a id="bk_i2s_get_read_ready__uint32_tP"></a> <a id="group__bk__api__i2s_1ga7de623fc4d7276bbab541b2d4f0c1f8d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_get\_read\_ready(uint32\_t \*read\_flag)
:   Get the i2s Rx fifo status.

    This API get the i2s Rx fifo status that check whether the fifo data can be read

    参数
    :   **read\_flag** – save Rx fifo status

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2S\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv422bk_i2s_get_write_readyP8uint32_t"></a>

<a id="_CPPv322bk_i2s_get_write_readyP8uint32_t"></a> <a id="_CPPv222bk_i2s_get_write_readyP8uint32_t"></a> <a id="bk_i2s_get_write_ready__uint32_tP"></a> <a id="group__bk__api__i2s_1ga6362338e966ef3298d688ffb2161809e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_get\_write\_ready(uint32\_t \*write\_flag)
:   Get the i2s Tx fifo status.

    This API get the i2s Tx fifo status that check whether the fifo data can be write

    参数
    :   **read\_flag** – save Tx fifo status

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_I2S\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv413bk_i2s_enable8i2s_en_t"></a>

<a id="_CPPv313bk_i2s_enable8i2s_en_t"></a> <a id="_CPPv213bk_i2s_enable8i2s_en_t"></a> <a id="bk_i2s_enable__i2s_en_t"></a> <a id="group__bk__api__i2s_1gacf03e0918c58089d45b022e29d500ba7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_enable([i2s\_en\_t](#_CPPv48i2s_en_t "i2s_en_t") en\_value)
:   Enable i2s.

    This API enable i2s

    参数
    :   **en\_value** – disable/enable i2s

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv417bk_i2s_int_enable12i2s_isr_id_t8uint32_t"></a>

<a id="_CPPv317bk_i2s_int_enable12i2s_isr_id_t8uint32_t"></a> <a id="_CPPv217bk_i2s_int_enable12i2s_isr_id_t8uint32_t"></a> <a id="bk_i2s_int_enable__i2s_isr_id_t.uint32_t"></a> <a id="group__bk__api__i2s_1ga7157a8e0ef073b0986e8b43eb782db44"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_int\_enable([i2s\_isr\_id\_t](#_CPPv412i2s_isr_id_t "i2s_isr_id_t") int\_id, uint32\_t value)
:   Config i2s interrupt.

    This API config i2s interrupt

    参数
    :   - **int\_id** – interrupt id
        - **value** – 0:disable 1:enable

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv415bk_i2s_set_role10i2s_role_t"></a>

<a id="_CPPv315bk_i2s_set_role10i2s_role_t"></a> <a id="_CPPv215bk_i2s_set_role10i2s_role_t"></a> <a id="bk_i2s_set_role__i2s_role_t"></a> <a id="group__bk__api__i2s_1gadb3ecd82272e186b564cf3a610d6cc65"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_role([i2s\_role\_t](#_CPPv410i2s_role_t "i2s_role_t") role)
:   Config i2s work role.

    This API config i2s work role

    参数
    :   **role** – work role slave/master

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv420bk_i2s_set_work_mode15i2s_work_mode_t"></a>

<a id="_CPPv320bk_i2s_set_work_mode15i2s_work_mode_t"></a> <a id="_CPPv220bk_i2s_set_work_mode15i2s_work_mode_t"></a> <a id="bk_i2s_set_work_mode__i2s_work_mode_t"></a> <a id="group__bk__api__i2s_1ga8a66495e26aea67629ac8b3f2dad0201"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_work\_mode([i2s\_work\_mode\_t](#_CPPv415i2s_work_mode_t "i2s_work_mode_t") work\_mode)
:   Config i2s work mode.

    This API config i2s work mode

    参数
    :   **work\_mode** – i2s work mode

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv422bk_i2s_set_lrck_invert20i2s_lrck_invert_en_t"></a>

<a id="_CPPv322bk_i2s_set_lrck_invert20i2s_lrck_invert_en_t"></a> <a id="_CPPv222bk_i2s_set_lrck_invert20i2s_lrck_invert_en_t"></a> <a id="bk_i2s_set_lrck_invert__i2s_lrck_invert_en_t"></a> <a id="group__bk__api__i2s_1ga40d98b88e42f0248eb8dc1444c712f80"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_lrck\_invert([i2s\_lrck\_invert\_en\_t](#_CPPv420i2s_lrck_invert_en_t "i2s_lrck_invert_en_t") lrckrp)
:   Config i2s lrck invert.

    This API config i2s lrck invert

    参数
    :   **lrckrp** – i2s lrck invert enable/disable

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv421bk_i2s_set_sck_invert19i2s_sck_invert_en_t"></a>

<a id="_CPPv321bk_i2s_set_sck_invert19i2s_sck_invert_en_t"></a> <a id="_CPPv221bk_i2s_set_sck_invert19i2s_sck_invert_en_t"></a> <a id="bk_i2s_set_sck_invert__i2s_sck_invert_en_t"></a> <a id="group__bk__api__i2s_1ga5c705943aa6f69332d3261ebfa023ac3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_sck\_invert([i2s\_sck\_invert\_en\_t](#_CPPv419i2s_sck_invert_en_t "i2s_sck_invert_en_t") sck\_invert)
:   Config i2s sck invert.

    This API config i2s sck invert

    参数
    :   **sck\_invert** – i2s sck invert enable/disable

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv420bk_i2s_set_lsb_first18i2s_lsb_first_en_t"></a>

<a id="_CPPv320bk_i2s_set_lsb_first18i2s_lsb_first_en_t"></a> <a id="_CPPv220bk_i2s_set_lsb_first18i2s_lsb_first_en_t"></a> <a id="bk_i2s_set_lsb_first__i2s_lsb_first_en_t"></a> <a id="group__bk__api__i2s_1ga069d352f39fe9506392eae04add933c0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_lsb\_first([i2s\_lsb\_first\_en\_t](#_CPPv418i2s_lsb_first_en_t "i2s_lsb_first_en_t") lsb\_first)
:   Config i2s lsb first.

    This API config i2s lsb first

    参数
    :   **lsb\_first** – i2s lsb first enable/disable

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv419bk_i2s_set_sync_len8uint32_t"></a>

<a id="_CPPv319bk_i2s_set_sync_len8uint32_t"></a> <a id="_CPPv219bk_i2s_set_sync_len8uint32_t"></a> <a id="bk_i2s_set_sync_len__uint32_t"></a> <a id="group__bk__api__i2s_1ga0ffe8c3f34539d6331d1b0d2e2d78d13"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_sync\_len(uint32\_t sync\_len)
:   Config i2s sync length.

    This API config i2s sync length

    参数
    :   **sync\_len** – i2s sync length

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv419bk_i2s_set_data_len8uint32_t"></a>

<a id="_CPPv319bk_i2s_set_data_len8uint32_t"></a> <a id="_CPPv219bk_i2s_set_data_len8uint32_t"></a> <a id="bk_i2s_set_data_len__uint32_t"></a> <a id="group__bk__api__i2s_1ga2fc30067b3f8a8317c008725580d57d9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_data\_len(uint32\_t data\_len)
:   Config i2s data length.

    This API config i2s data length

    参数
    :   **data\_len** – i2s data length

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv419bk_i2s_set_pcm_dlen8uint32_t"></a>

<a id="_CPPv319bk_i2s_set_pcm_dlen8uint32_t"></a> <a id="_CPPv219bk_i2s_set_pcm_dlen8uint32_t"></a> <a id="bk_i2s_set_pcm_dlen__uint32_t"></a> <a id="group__bk__api__i2s_1ga986fd8dc9a839ab6ede9394a3effa665"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_pcm\_dlen(uint32\_t pcm\_dlen)
:   Config i2s pcm D length of 2B\+D.

    This API config i2s pcm D length of 2B\+D

    参数
    :   **pcm\_dlen** – pcm D length

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv421bk_i2s_set_store_mode22i2s_lrcom_store_mode_t"></a>

<a id="_CPPv321bk_i2s_set_store_mode22i2s_lrcom_store_mode_t"></a> <a id="_CPPv221bk_i2s_set_store_mode22i2s_lrcom_store_mode_t"></a> <a id="bk_i2s_set_store_mode__i2s_lrcom_store_mode_t"></a> <a id="group__bk__api__i2s_1ga73d2b798189eff00aec1fb5b12ba2375"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_store\_mode([i2s\_lrcom\_store\_mode\_t](#_CPPv422i2s_lrcom_store_mode_t "i2s_lrcom_store_mode_t") store\_mode)
:   Config i2s store mode.

    This API config i2s store mode

    **Attention**
    :   1\. LRLR mode: left and right channel data are written alternately in chronological order(L-\>R-\>L-\>R-\>……)

    **Attention**
    :   2\. 16R16L mode: left and right channel data are written to FIFO in 32 bits, in which the lower 16 bits correspond to the left channel and the higher 16 bits correspond to the right channel({R,L}-\>{R,L}-\>……)

    参数
    :   **store\_mode** – lrcom store mode LRLR/16R16L

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv419bk_i2s_clear_rxfifov"></a>

<a id="_CPPv319bk_i2s_clear_rxfifov"></a> <a id="_CPPv219bk_i2s_clear_rxfifov"></a> <a id="bk_i2s_clear_rxfifo__void"></a> <a id="group__bk__api__i2s_1gad997ca8a59f252eff10b30aa7bde3247"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_clear\_rxfifo(void)
:   clear i2s rx fifo

    This API clear i2s rx fifo

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv419bk_i2s_clear_txfifov"></a>

<a id="_CPPv319bk_i2s_clear_txfifov"></a> <a id="_CPPv219bk_i2s_clear_txfifov"></a> <a id="bk_i2s_clear_txfifo__void"></a> <a id="group__bk__api__i2s_1ga5056d5a464b56ce6f258dce354cac557"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_clear\_txfifo(void)
:   clear i2s tx fifo

    This API clear i2s tx fifo

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv422bk_i2s_set_txint_level17i2s_txint_level_t"></a>

<a id="_CPPv322bk_i2s_set_txint_level17i2s_txint_level_t"></a> <a id="_CPPv222bk_i2s_set_txint_level17i2s_txint_level_t"></a> <a id="bk_i2s_set_txint_level__i2s_txint_level_t"></a> <a id="group__bk__api__i2s_1gaebf6ac2b5e964e61d4e3197997e9f0b8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_txint\_level([i2s\_txint\_level\_t](#_CPPv417i2s_txint_level_t "i2s_txint_level_t") txint\_level)
:   config i2s tx interrupt level

    This API config i2s tx interrupt level

    参数
    :   **txint\_level** – tx interrupt trigger level

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv422bk_i2s_set_rxint_level17i2s_rxint_level_t"></a>

<a id="_CPPv322bk_i2s_set_rxint_level17i2s_rxint_level_t"></a> <a id="_CPPv222bk_i2s_set_rxint_level17i2s_rxint_level_t"></a> <a id="bk_i2s_set_rxint_level__i2s_rxint_level_t"></a> <a id="group__bk__api__i2s_1ga3c5505f7a80facea0cc2ca88e988e443"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_rxint\_level([i2s\_rxint\_level\_t](#_CPPv417i2s_rxint_level_t "i2s_rxint_level_t") rxint\_level)
:   config i2s rx interrupt level

    This API config i2s rx interrupt level

    参数
    :   **rxint\_level** – rx interrupt trigger level

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv417bk_i2s_write_data8uint32_tP8uint32_t8uint32_t"></a>

<a id="_CPPv317bk_i2s_write_data8uint32_tP8uint32_t8uint32_t"></a> <a id="_CPPv217bk_i2s_write_data8uint32_tP8uint32_t8uint32_t"></a> <a id="bk_i2s_write_data__uint32_t.uint32_tP.uint32_t"></a> <a id="group__bk__api__i2s_1ga765b05145b4df5882daac7712002d964"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_write\_data(uint32\_t channel\_id, uint32\_t \*data\_buf, uint32\_t data\_len)
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
    :   - **channel\_id** – i2s channel 1/2/3/4
        - **data\_buf** – data to write
        - **data\_len** – data length to write

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv416bk_i2s_read_dataP8uint32_t8uint32_t"></a>

<a id="_CPPv316bk_i2s_read_dataP8uint32_t8uint32_t"></a> <a id="_CPPv216bk_i2s_read_dataP8uint32_t8uint32_t"></a> <a id="bk_i2s_read_data__uint32_tP.uint32_t"></a> <a id="group__bk__api__i2s_1ga4b4a1f0e29c3ed0fd1f3e00950c3f19b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_read\_data(uint32\_t \*data\_buf, uint32\_t data\_len)
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
    :   - **data\_buf** – save data read from rx fifo
        - **data\_len** – data length to read

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv420bk_i2s_get_data_addr16i2s_channel_id_tP8uint32_t"></a>

<a id="_CPPv320bk_i2s_get_data_addr16i2s_channel_id_tP8uint32_t"></a> <a id="_CPPv220bk_i2s_get_data_addr16i2s_channel_id_tP8uint32_t"></a> <a id="bk_i2s_get_data_addr__i2s_channel_id_t.uint32_tP"></a> <a id="group__bk__api__i2s_1ga500a50be6544e91fabfa76f1fc953966"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_get\_data\_addr([i2s\_channel\_id\_t](#_CPPv416i2s_channel_id_t "i2s_channel_id_t") chl\_id, uint32\_t \*i2s\_data\_addr)
:   get i2s data address

    This API get i2s data address

    参数
    :   **i2s\_data\_addr** – save i2s data address

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv420bk_i2s_set_samp_rate15i2s_samp_rate_t"></a>

<a id="_CPPv320bk_i2s_set_samp_rate15i2s_samp_rate_t"></a> <a id="_CPPv220bk_i2s_set_samp_rate15i2s_samp_rate_t"></a> <a id="bk_i2s_set_samp_rate__i2s_samp_rate_t"></a> <a id="group__bk__api__i2s_1gac5c107c7b881731428dd59f0d10e35a8"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_set\_samp\_rate([i2s\_samp\_rate\_t](#_CPPv415i2s_samp_rate_t "i2s_samp_rate_t") samp\_rate)
:   config i2s sample rate

    This API config i2s sample rate

    参数
    :   **rate** – sample rate and data width

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv423bk_i2s_register_i2s_isr12i2s_isr_id_t9i2s_isr_tPv"></a>

<a id="_CPPv323bk_i2s_register_i2s_isr12i2s_isr_id_t9i2s_isr_tPv"></a> <a id="_CPPv223bk_i2s_register_i2s_isr12i2s_isr_id_t9i2s_isr_tPv"></a> <a id="bk_i2s_register_i2s_isr__i2s_isr_id_t.i2s_isr_t.voidP"></a> <a id="group__bk__api__i2s_1gaaa1f3f42d50b97a2b1fc916930ec8238"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_register\_i2s\_isr([i2s\_isr\_id\_t](#_CPPv412i2s_isr_id_t "i2s_isr_id_t") isr\_id, [i2s\_isr\_t](#_CPPv49i2s_isr_t "i2s_isr_t") isr, void \*param)
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
    :   - **isr\_id** – i2s isr id
        - **isr** – isr function
        - **param** – isr parameters

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - BK\_ERR\_I2S\_ISR\_ID: i2s isr id is invalid
        - others: other errors.

<a id="_CPPv415bk_i2s_chl_init16i2s_channel_id_t15i2s_txrx_type_t8uint32_t18i2s_data_handle_cbPP17RingBufferContext"></a>

<a id="_CPPv315bk_i2s_chl_init16i2s_channel_id_t15i2s_txrx_type_t8uint32_t18i2s_data_handle_cbPP17RingBufferContext"></a> <a id="_CPPv215bk_i2s_chl_init16i2s_channel_id_t15i2s_txrx_type_t8uint32_t18i2s_data_handle_cbPP17RingBufferContext"></a> <a id="bk_i2s_chl_init__i2s_channel_id_t.i2s_txrx_type_t.uint32_t.i2s_data_handle_cb.RingBufferContextPP"></a> <a id="group__bk__api__i2s_1gab2c7671f8985cf249045a5bbf5b232dd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_chl\_init([i2s\_channel\_id\_t](#_CPPv416i2s_channel_id_t "i2s_channel_id_t") chl, [i2s\_txrx\_type\_t](#_CPPv415i2s_txrx_type_t "i2s_txrx_type_t") type, uint32\_t buff\_size, [i2s\_data\_handle\_cb](#_CPPv418i2s_data_handle_cb "i2s_data_handle_cb") data\_handle\_cb, RingBufferContext \*\*rb)
:   init i2s channel to send or receive data by dma

    This API config dma to carry i2s data

    参数
    :   **chl** – i2s channel @type Tx or Rx config @buff\_size the size(byte) of ring buffer to send or receive data @data\_handle\_cb the callback called by dma finish isr when dma carry “buff\_size/2” data complete @rb save RingBufferContext, and send or receive data use it

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv417bk_i2s_chl_deinit16i2s_channel_id_t15i2s_txrx_type_t"></a>

<a id="_CPPv317bk_i2s_chl_deinit16i2s_channel_id_t15i2s_txrx_type_t"></a> <a id="_CPPv217bk_i2s_chl_deinit16i2s_channel_id_t15i2s_txrx_type_t"></a> <a id="bk_i2s_chl_deinit__i2s_channel_id_t.i2s_txrx_type_t"></a> <a id="group__bk__api__i2s_1gac936e6039947974c59de2dad950d769c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_chl\_deinit([i2s\_channel\_id\_t](#_CPPv416i2s_channel_id_t "i2s_channel_id_t") chl, [i2s\_txrx\_type\_t](#_CPPv415i2s_txrx_type_t "i2s_txrx_type_t") type)
:   deinit i2s channel

    This API config dma to carry i2s data

    参数
    :   **chl** – i2s channel @type Tx or Rx config

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="_CPPv412bk_i2s_startv"></a>

<a id="_CPPv312bk_i2s_startv"></a> <a id="_CPPv212bk_i2s_startv"></a> <a id="bk_i2s_start__void"></a> <a id="group__bk__api__i2s_1gad463a6490380a72dca06a99259ff32b3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_start(void)
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
    os_printf("ring_buffer_write, size: %d \n", size);
    os_free(temp_data);
    bk_i2s_start();
    ```

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - BK\_ERR\_I2S\_ISR\_ID: i2s isr id is invalid
        - others: other errors.

<a id="_CPPv411bk_i2s_stopv"></a>

<a id="_CPPv311bk_i2s_stopv"></a> <a id="_CPPv211bk_i2s_stopv"></a> <a id="bk_i2s_stop__void"></a> <a id="group__bk__api__i2s_1gae82d981553d3dd31830f973de2f717b4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_i2s\_stop(void)
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
    :   - BK\_OK: succeed
        - BK\_ERR\_AUD\_NOT\_INIT: i2s driver is not init
        - others: other errors.

<a id="i2s-api-typedefs"></a>

## I2S API Typedefs

<a id="id1"></a>

### Header File

- [i2s\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/i2s_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv416i2s_int_config_t"></a>

<a id="_CPPv316i2s_int_config_t"></a> <a id="_CPPv216i2s_int_config_t"></a> <a id="i2s_int_config_t"></a> <a id="structi2s__int__config__t"></a> struct i2s\_int\_config\_t

<a id="_CPPv412i2s_config_t"></a>

<a id="_CPPv312i2s_config_t"></a> <a id="_CPPv212i2s_config_t"></a> <a id="i2s_config_t"></a> <a id="structi2s__config__t"></a> struct i2s\_config\_t

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_I2S_NOT_INIT"></a>

<a id="group__bk__api__i2s__defs_1ga323ed386bad2238b3ca8a4c06764a535"></a> BK\_ERR\_I2S\_NOT\_INIT
:   I2S driver not init

<a id="c.BK_ERR_I2S_PARAM"></a>

<a id="group__bk__api__i2s__defs_1ga66c0505fd73b35acb1e7778db3db09ea"></a> BK\_ERR\_I2S\_PARAM
:   I2S parameter invalid

<a id="c.BK_ERR_I2S_ISR_ID"></a>

<a id="group__bk__api__i2s__defs_1gaeabfa8d9351c563e998913613745fe1d"></a> BK\_ERR\_I2S\_ISR\_ID
:   I2S isr id invalid

<a id="c.DEFAULT_I2S_CONFIG"></a>

<a id="group__bk__api__i2s__structs_1gafdca2e3bb1db65d354cf56d7fb9d92fa"></a> DEFAULT\_I2S\_CONFIG()

<a id="c.DEFAULT_PCM_CONFIG"></a>

<a id="group__bk__api__i2s__structs_1ga360ba887f2d0748c4e05eb40e42a07f9"></a> DEFAULT\_PCM\_CONFIG()

<a id="c.DEFAULT_TDM_CONFIG"></a>

<a id="group__bk__api__i2s__structs_1ga884c2858e43693845b611db31e0010c4"></a> DEFAULT\_TDM\_CONFIG()

<a id="c.DEFAULT_2BD_CONFIG"></a>

<a id="group__bk__api__i2s__structs_1gab87cba1e8113be6e524eb9a473065f3c"></a> DEFAULT\_2BD\_CONFIG()

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv49i2s_isr_t"></a>

<a id="_CPPv39i2s_isr_t"></a> <a id="_CPPv29i2s_isr_t"></a> <a id="i2s_isr_t"></a> <a id="i2s__types_8h_1a2b7806792752cc9850769949cb4e7ee2"></a> typedef void (\*i2s\_isr\_t)(void \*param)

<a id="_CPPv418i2s_data_handle_cb"></a>

<a id="_CPPv318i2s_data_handle_cb"></a> <a id="_CPPv218i2s_data_handle_cb"></a> <a id="i2s_data_handle_cb"></a> <a id="group__bk__api__i2s__structs_1ga43827dad85e1a2eeb7bd14c32a3d6f36"></a> typedef int (\*i2s\_data\_handle\_cb)(uint32\_t size)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv419i2s_gpio_group_id_t"></a>

<a id="_CPPv319i2s_gpio_group_id_t"></a> <a id="_CPPv219i2s_gpio_group_id_t"></a> <a id="group__bk__api__i2s__enum_1ga11e2e8101e580387f9d1dfcef80f9b3a"></a> enum i2s\_gpio\_group\_id\_t
:   *Values:*

    <a id="_CPPv4N19i2s_gpio_group_id_t16I2S_GPIO_GROUP_0E"></a>

    <a id="_CPPv3N19i2s_gpio_group_id_t16I2S_GPIO_GROUP_0E"></a> <a id="_CPPv2N19i2s_gpio_group_id_t16I2S_GPIO_GROUP_0E"></a> <a id="group__bk__api__i2s__enum_1gga11e2e8101e580387f9d1dfcef80f9b3aafbf8ba783786f4bc4a2a90b14d67f1de"></a> enumerator I2S\_GPIO\_GROUP\_0
    :   I2S gpio group 0: GPIO6, GPIO7, GPIO8, GPIO9

    <a id="_CPPv4N19i2s_gpio_group_id_t16I2S_GPIO_GROUP_1E"></a>

    <a id="_CPPv3N19i2s_gpio_group_id_t16I2S_GPIO_GROUP_1E"></a> <a id="_CPPv2N19i2s_gpio_group_id_t16I2S_GPIO_GROUP_1E"></a> <a id="group__bk__api__i2s__enum_1gga11e2e8101e580387f9d1dfcef80f9b3aa8313a03739f6dad3adbc682ab09af0cc"></a> enumerator I2S\_GPIO\_GROUP\_1
    :   I2S gpio group 1: GPIO40, GPIO41, GPIO42, GPIO43

    <a id="_CPPv4N19i2s_gpio_group_id_t16I2S_GPIO_GROUP_2E"></a>

    <a id="_CPPv3N19i2s_gpio_group_id_t16I2S_GPIO_GROUP_2E"></a> <a id="_CPPv2N19i2s_gpio_group_id_t16I2S_GPIO_GROUP_2E"></a> <a id="group__bk__api__i2s__enum_1gga11e2e8101e580387f9d1dfcef80f9b3aa463aff0a05473b66b240d4cdb3a2464d"></a> enumerator I2S\_GPIO\_GROUP\_2
    :   I2S gpio group 2: GPIO44, GPIO45, GPIO46, GPIO47

    <a id="_CPPv4N19i2s_gpio_group_id_t18I2S_GPIO_GROUP_MAXE"></a>

    <a id="_CPPv3N19i2s_gpio_group_id_t18I2S_GPIO_GROUP_MAXE"></a> <a id="_CPPv2N19i2s_gpio_group_id_t18I2S_GPIO_GROUP_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga11e2e8101e580387f9d1dfcef80f9b3aa5430981c9f9a1fc4390de3d53d03762d"></a> enumerator I2S\_GPIO\_GROUP\_MAX

<a id="_CPPv412i2s_isr_id_t"></a>

<a id="_CPPv312i2s_isr_id_t"></a> <a id="_CPPv212i2s_isr_id_t"></a> <a id="group__bk__api__i2s__enum_1ga0085fea492264745accf06b8a848c371"></a> enum i2s\_isr\_id\_t
:   *Values:*

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL1_TXUDFE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL1_TXUDFE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL1_TXUDFE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a7fd12775d01b6136d97920cfef956492"></a> enumerator I2S\_ISR\_CHL1\_TXUDF
    :   I2S channel1 tx\_udf interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL1_RXOVFE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL1_RXOVFE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL1_RXOVFE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a416484c64f29612b372e9dc8a2df2f32"></a> enumerator I2S\_ISR\_CHL1\_RXOVF
    :   I2S channel1 rx\_ovf interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL1_TXINTE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL1_TXINTE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL1_TXINTE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a4a520298d5135a860b95bfaf91297d7d"></a> enumerator I2S\_ISR\_CHL1\_TXINT
    :   I2S channel1 tx interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL1_RXINTE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL1_RXINTE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL1_RXINTE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a16a7397f62b6094362f5e13d55c183e9"></a> enumerator I2S\_ISR\_CHL1\_RXINT
    :   I2S channel1 rx interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL2_TXUDFE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL2_TXUDFE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL2_TXUDFE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371aacb7a5b0183c983d9c2b25ab3e95591f"></a> enumerator I2S\_ISR\_CHL2\_TXUDF
    :   I2S channel2 tx\_udf interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL2_RXOVFE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL2_RXOVFE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL2_RXOVFE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371ab8710b14ba65534279b4352c0905dc56"></a> enumerator I2S\_ISR\_CHL2\_RXOVF
    :   I2S channel2 rx\_ovf interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL2_TXINTE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL2_TXINTE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL2_TXINTE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a5360977b28c4f2ef4692ef7b036aaee3"></a> enumerator I2S\_ISR\_CHL2\_TXINT
    :   I2S channel2 tx interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL2_RXINTE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL2_RXINTE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL2_RXINTE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a3847b1340c035598a807629edca451d1"></a> enumerator I2S\_ISR\_CHL2\_RXINT
    :   I2S channel2 rx interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL3_TXUDFE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL3_TXUDFE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL3_TXUDFE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a8a9f2ef5c92926d1b7054241b345b7f1"></a> enumerator I2S\_ISR\_CHL3\_TXUDF
    :   I2S channel3 tx\_udf interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL3_RXOVFE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL3_RXOVFE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL3_RXOVFE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a6ff178dc7d2b91624a544064649a931e"></a> enumerator I2S\_ISR\_CHL3\_RXOVF
    :   I2S channel3 rx\_ovf interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL3_TXINTE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL3_TXINTE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL3_TXINTE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a21ba0f8106872d51ec053fc23e51e5d5"></a> enumerator I2S\_ISR\_CHL3\_TXINT
    :   I2S channel3 tx interrupt

    <a id="_CPPv4N12i2s_isr_id_t18I2S_ISR_CHL3_RXINTE"></a>

    <a id="_CPPv3N12i2s_isr_id_t18I2S_ISR_CHL3_RXINTE"></a> <a id="_CPPv2N12i2s_isr_id_t18I2S_ISR_CHL3_RXINTE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a76569b40fcdb3b9b2b5cfa15fa30130c"></a> enumerator I2S\_ISR\_CHL3\_RXINT
    :   I2S channel3 rx interrupt

    <a id="_CPPv4N12i2s_isr_id_t11I2S_ISR_MAXE"></a>

    <a id="_CPPv3N12i2s_isr_id_t11I2S_ISR_MAXE"></a> <a id="_CPPv2N12i2s_isr_id_t11I2S_ISR_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga0085fea492264745accf06b8a848c371a3efda8060f99c45bcb67373f936db8e4"></a> enumerator I2S\_ISR\_MAX

<a id="_CPPv48i2s_en_t"></a>

<a id="_CPPv38i2s_en_t"></a> <a id="_CPPv28i2s_en_t"></a> <a id="group__bk__api__i2s__enum_1gae347833578a5da2bb43ea3e4f2032772"></a> enum i2s\_en\_t
:   *Values:*

    <a id="_CPPv4N8i2s_en_t11I2S_DISABLEE"></a>

    <a id="_CPPv3N8i2s_en_t11I2S_DISABLEE"></a> <a id="_CPPv2N8i2s_en_t11I2S_DISABLEE"></a> <a id="group__bk__api__i2s__enum_1ggae347833578a5da2bb43ea3e4f2032772aa8ea46aedad74fcae63c71a306e35c12"></a> enumerator I2S\_DISABLE
    :   I2S disable

    <a id="_CPPv4N8i2s_en_t10I2S_ENABLEE"></a>

    <a id="_CPPv3N8i2s_en_t10I2S_ENABLEE"></a> <a id="_CPPv2N8i2s_en_t10I2S_ENABLEE"></a> <a id="group__bk__api__i2s__enum_1ggae347833578a5da2bb43ea3e4f2032772a6faf07430ba366b6ca862d9977b64cf1"></a> enumerator I2S\_ENABLE
    :   I2S enable

    <a id="_CPPv4N8i2s_en_t10I2S_EN_MAXE"></a>

    <a id="_CPPv3N8i2s_en_t10I2S_EN_MAXE"></a> <a id="_CPPv2N8i2s_en_t10I2S_EN_MAXE"></a> <a id="group__bk__api__i2s__enum_1ggae347833578a5da2bb43ea3e4f2032772a3feef6a6d0c365e63ba90a57a00a10b6"></a> enumerator I2S\_EN\_MAX

<a id="_CPPv410i2s_role_t"></a>

<a id="_CPPv310i2s_role_t"></a> <a id="_CPPv210i2s_role_t"></a> <a id="group__bk__api__i2s__enum_1ga49215c9704dec85391a43c397c686cb0"></a> enum i2s\_role\_t
:   *Values:*

    <a id="_CPPv4N10i2s_role_t14I2S_ROLE_SLAVEE"></a>

    <a id="_CPPv3N10i2s_role_t14I2S_ROLE_SLAVEE"></a> <a id="_CPPv2N10i2s_role_t14I2S_ROLE_SLAVEE"></a> <a id="group__bk__api__i2s__enum_1gga49215c9704dec85391a43c397c686cb0ad1aad5aa5bddd1e447c7775b7ba921dc"></a> enumerator I2S\_ROLE\_SLAVE
    :   I2S role: slave

    <a id="_CPPv4N10i2s_role_t15I2S_ROLE_MASTERE"></a>

    <a id="_CPPv3N10i2s_role_t15I2S_ROLE_MASTERE"></a> <a id="_CPPv2N10i2s_role_t15I2S_ROLE_MASTERE"></a> <a id="group__bk__api__i2s__enum_1gga49215c9704dec85391a43c397c686cb0a150cd0ed470f1cab13a6c0cacf4a090d"></a> enumerator I2S\_ROLE\_MASTER
    :   I2S role: master

    <a id="_CPPv4N10i2s_role_t12I2S_ROLE_MAXE"></a>

    <a id="_CPPv3N10i2s_role_t12I2S_ROLE_MAXE"></a> <a id="_CPPv2N10i2s_role_t12I2S_ROLE_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga49215c9704dec85391a43c397c686cb0a4573ea790f558f06cc51220d3b7c78a4"></a> enumerator I2S\_ROLE\_MAX

<a id="_CPPv415i2s_work_mode_t"></a>

<a id="_CPPv315i2s_work_mode_t"></a> <a id="_CPPv215i2s_work_mode_t"></a> <a id="group__bk__api__i2s__enum_1gad77d5d6c9ac2a5d762d61a0f5df9d679"></a> enum i2s\_work\_mode\_t
:   *Values:*

    <a id="_CPPv4N15i2s_work_mode_t17I2S_WORK_MODE_I2SE"></a>

    <a id="_CPPv3N15i2s_work_mode_t17I2S_WORK_MODE_I2SE"></a> <a id="_CPPv2N15i2s_work_mode_t17I2S_WORK_MODE_I2SE"></a> <a id="group__bk__api__i2s__enum_1ggad77d5d6c9ac2a5d762d61a0f5df9d679a2e12af3e9690ef0618a3cb680a5f1049"></a> enumerator I2S\_WORK\_MODE\_I2S
    :   I2S work mode: I2S (Philips)

    <a id="_CPPv4N15i2s_work_mode_t22I2S_WORK_MODE_LEFTJUSTE"></a>

    <a id="_CPPv3N15i2s_work_mode_t22I2S_WORK_MODE_LEFTJUSTE"></a> <a id="_CPPv2N15i2s_work_mode_t22I2S_WORK_MODE_LEFTJUSTE"></a> <a id="group__bk__api__i2s__enum_1ggad77d5d6c9ac2a5d762d61a0f5df9d679a3c702e2d3a21db1fe080801d920c5f7d"></a> enumerator I2S\_WORK\_MODE\_LEFTJUST
    :   I2S work mode: Left Justified

    <a id="_CPPv4N15i2s_work_mode_t23I2S_WORK_MODE_RIGHTJUSTE"></a>

    <a id="_CPPv3N15i2s_work_mode_t23I2S_WORK_MODE_RIGHTJUSTE"></a> <a id="_CPPv2N15i2s_work_mode_t23I2S_WORK_MODE_RIGHTJUSTE"></a> <a id="group__bk__api__i2s__enum_1ggad77d5d6c9ac2a5d762d61a0f5df9d679a030590ed7d068399977ff9cd419ff67c"></a> enumerator I2S\_WORK\_MODE\_RIGHTJUST
    :   I2S work mode: Right Justified

    <a id="_CPPv4N15i2s_work_mode_t18I2S_WORK_MODE_RSVDE"></a>

    <a id="_CPPv3N15i2s_work_mode_t18I2S_WORK_MODE_RSVDE"></a> <a id="_CPPv2N15i2s_work_mode_t18I2S_WORK_MODE_RSVDE"></a> <a id="group__bk__api__i2s__enum_1ggad77d5d6c9ac2a5d762d61a0f5df9d679a6f0a7e85fc0dcbd8f0d3d865a7f1fba6"></a> enumerator I2S\_WORK\_MODE\_RSVD
    :   I2S work mode: reserved for future use

    <a id="_CPPv4N15i2s_work_mode_t26I2S_WORK_MODE_SHORTFAMSYNCE"></a>

    <a id="_CPPv3N15i2s_work_mode_t26I2S_WORK_MODE_SHORTFAMSYNCE"></a> <a id="_CPPv2N15i2s_work_mode_t26I2S_WORK_MODE_SHORTFAMSYNCE"></a> <a id="group__bk__api__i2s__enum_1ggad77d5d6c9ac2a5d762d61a0f5df9d679aae606568ef94be22a3574dd88be0a1d4"></a> enumerator I2S\_WORK\_MODE\_SHORTFAMSYNC
    :   I2S work mode: Short Frame Sync

    <a id="_CPPv4N15i2s_work_mode_t25I2S_WORK_MODE_LONGFAMSYNCE"></a>

    <a id="_CPPv3N15i2s_work_mode_t25I2S_WORK_MODE_LONGFAMSYNCE"></a> <a id="_CPPv2N15i2s_work_mode_t25I2S_WORK_MODE_LONGFAMSYNCE"></a> <a id="group__bk__api__i2s__enum_1ggad77d5d6c9ac2a5d762d61a0f5df9d679a5b7cce38875443d91cc380a0f2bb7386"></a> enumerator I2S\_WORK\_MODE\_LONGFAMSYNC
    :   I2S work mode: Long Frame Sync

    <a id="_CPPv4N15i2s_work_mode_t23I2S_WORK_MODE_NORMAL2BDE"></a>

    <a id="_CPPv3N15i2s_work_mode_t23I2S_WORK_MODE_NORMAL2BDE"></a> <a id="_CPPv2N15i2s_work_mode_t23I2S_WORK_MODE_NORMAL2BDE"></a> <a id="group__bk__api__i2s__enum_1ggad77d5d6c9ac2a5d762d61a0f5df9d679af7296b7f933ea70302639a93eec7de87"></a> enumerator I2S\_WORK\_MODE\_NORMAL2BD
    :   I2S work mode: Normal 2B\+D

    <a id="_CPPv4N15i2s_work_mode_t22I2S_WORK_MODE_DELAY2BDE"></a>

    <a id="_CPPv3N15i2s_work_mode_t22I2S_WORK_MODE_DELAY2BDE"></a> <a id="_CPPv2N15i2s_work_mode_t22I2S_WORK_MODE_DELAY2BDE"></a> <a id="group__bk__api__i2s__enum_1ggad77d5d6c9ac2a5d762d61a0f5df9d679aeff94f73ad0e4534c732b9ab22feb82d"></a> enumerator I2S\_WORK\_MODE\_DELAY2BD
    :   I2S work mode: Delay 2B\+D

    <a id="_CPPv4N15i2s_work_mode_t17I2S_WORK_MODE_MAXE"></a>

    <a id="_CPPv3N15i2s_work_mode_t17I2S_WORK_MODE_MAXE"></a> <a id="_CPPv2N15i2s_work_mode_t17I2S_WORK_MODE_MAXE"></a> <a id="group__bk__api__i2s__enum_1ggad77d5d6c9ac2a5d762d61a0f5df9d679ab07a5bc6092b9904bd22962559e32039"></a> enumerator I2S\_WORK\_MODE\_MAX

<a id="_CPPv420i2s_lrck_invert_en_t"></a>

<a id="_CPPv320i2s_lrck_invert_en_t"></a> <a id="_CPPv220i2s_lrck_invert_en_t"></a> <a id="group__bk__api__i2s__enum_1ga293a2a08e26445e6eb2dfd36edff3687"></a> enum i2s\_lrck\_invert\_en\_t
:   *Values:*

    <a id="_CPPv4N20i2s_lrck_invert_en_t23I2S_LRCK_INVERT_DISABLEE"></a>

    <a id="_CPPv3N20i2s_lrck_invert_en_t23I2S_LRCK_INVERT_DISABLEE"></a> <a id="_CPPv2N20i2s_lrck_invert_en_t23I2S_LRCK_INVERT_DISABLEE"></a> <a id="group__bk__api__i2s__enum_1gga293a2a08e26445e6eb2dfd36edff3687af02e245761ff8a06b803cae9117658ac"></a> enumerator I2S\_LRCK\_INVERT\_DISABLE
    :   I2S lrck invert disable

    <a id="_CPPv4N20i2s_lrck_invert_en_t22I2S_LRCK_INVERT_ENABLEE"></a>

    <a id="_CPPv3N20i2s_lrck_invert_en_t22I2S_LRCK_INVERT_ENABLEE"></a> <a id="_CPPv2N20i2s_lrck_invert_en_t22I2S_LRCK_INVERT_ENABLEE"></a> <a id="group__bk__api__i2s__enum_1gga293a2a08e26445e6eb2dfd36edff3687ac2894149014e9c8b61dde9de8f63fcf4"></a> enumerator I2S\_LRCK\_INVERT\_ENABLE
    :   I2S lrck invert enable

    <a id="_CPPv4N20i2s_lrck_invert_en_t19I2S_LRCK_INVERT_MAXE"></a>

    <a id="_CPPv3N20i2s_lrck_invert_en_t19I2S_LRCK_INVERT_MAXE"></a> <a id="_CPPv2N20i2s_lrck_invert_en_t19I2S_LRCK_INVERT_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga293a2a08e26445e6eb2dfd36edff3687a9ebf1fac6780be357c176a5dee4cfa4d"></a> enumerator I2S\_LRCK\_INVERT\_MAX

<a id="_CPPv419i2s_sck_invert_en_t"></a>

<a id="_CPPv319i2s_sck_invert_en_t"></a> <a id="_CPPv219i2s_sck_invert_en_t"></a> <a id="group__bk__api__i2s__enum_1ga777e3efb07c7e3b429fc06a58a7419d2"></a> enum i2s\_sck\_invert\_en\_t
:   *Values:*

    <a id="_CPPv4N19i2s_sck_invert_en_t22I2S_SCK_INVERT_DISABLEE"></a>

    <a id="_CPPv3N19i2s_sck_invert_en_t22I2S_SCK_INVERT_DISABLEE"></a> <a id="_CPPv2N19i2s_sck_invert_en_t22I2S_SCK_INVERT_DISABLEE"></a> <a id="group__bk__api__i2s__enum_1gga777e3efb07c7e3b429fc06a58a7419d2acde83124b12c762e0de6c381abbf88c1"></a> enumerator I2S\_SCK\_INVERT\_DISABLE
    :   I2S sck invert disable

    <a id="_CPPv4N19i2s_sck_invert_en_t21I2S_SCK_INVERT_ENABLEE"></a>

    <a id="_CPPv3N19i2s_sck_invert_en_t21I2S_SCK_INVERT_ENABLEE"></a> <a id="_CPPv2N19i2s_sck_invert_en_t21I2S_SCK_INVERT_ENABLEE"></a> <a id="group__bk__api__i2s__enum_1gga777e3efb07c7e3b429fc06a58a7419d2ae685749dc0c03af13cb5ab001953aa5b"></a> enumerator I2S\_SCK\_INVERT\_ENABLE
    :   I2S sck invert enable

    <a id="_CPPv4N19i2s_sck_invert_en_t18I2S_SCK_INVERT_MAXE"></a>

    <a id="_CPPv3N19i2s_sck_invert_en_t18I2S_SCK_INVERT_MAXE"></a> <a id="_CPPv2N19i2s_sck_invert_en_t18I2S_SCK_INVERT_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga777e3efb07c7e3b429fc06a58a7419d2a01c3ec65fdb77ead240e28d3c9af7114"></a> enumerator I2S\_SCK\_INVERT\_MAX

<a id="_CPPv418i2s_lsb_first_en_t"></a>

<a id="_CPPv318i2s_lsb_first_en_t"></a> <a id="_CPPv218i2s_lsb_first_en_t"></a> <a id="group__bk__api__i2s__enum_1ga708ad2e52ec73d42c15cdc3333b3e387"></a> enum i2s\_lsb\_first\_en\_t
:   *Values:*

    <a id="_CPPv4N18i2s_lsb_first_en_t21I2S_LSB_FIRST_DISABLEE"></a>

    <a id="_CPPv3N18i2s_lsb_first_en_t21I2S_LSB_FIRST_DISABLEE"></a> <a id="_CPPv2N18i2s_lsb_first_en_t21I2S_LSB_FIRST_DISABLEE"></a> <a id="group__bk__api__i2s__enum_1gga708ad2e52ec73d42c15cdc3333b3e387ac2263c4e26876fcb30a17b91046ab484"></a> enumerator I2S\_LSB\_FIRST\_DISABLE
    :   I2S lsb first disable

    <a id="_CPPv4N18i2s_lsb_first_en_t20I2S_LSB_FIRST_ENABLEE"></a>

    <a id="_CPPv3N18i2s_lsb_first_en_t20I2S_LSB_FIRST_ENABLEE"></a> <a id="_CPPv2N18i2s_lsb_first_en_t20I2S_LSB_FIRST_ENABLEE"></a> <a id="group__bk__api__i2s__enum_1gga708ad2e52ec73d42c15cdc3333b3e387ad615b4a17e2fcc0c83b8a5b50b0e76b7"></a> enumerator I2S\_LSB\_FIRST\_ENABLE
    :   I2S lsb first enable

    <a id="_CPPv4N18i2s_lsb_first_en_t20I2S_LSB_FIRST_EN_MAXE"></a>

    <a id="_CPPv3N18i2s_lsb_first_en_t20I2S_LSB_FIRST_EN_MAXE"></a> <a id="_CPPv2N18i2s_lsb_first_en_t20I2S_LSB_FIRST_EN_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga708ad2e52ec73d42c15cdc3333b3e387a724093fbe50335997586e4511ab255f4"></a> enumerator I2S\_LSB\_FIRST\_EN\_MAX

<a id="_CPPv417i2s_parallel_en_t"></a>

<a id="_CPPv317i2s_parallel_en_t"></a> <a id="_CPPv217i2s_parallel_en_t"></a> <a id="group__bk__api__i2s__enum_1ga6810be6ead675ceab19dbbf64ae754dd"></a> enum i2s\_parallel\_en\_t
:   *Values:*

    <a id="_CPPv4N17i2s_parallel_en_t20I2S_PARALLEL_DISABLEE"></a>

    <a id="_CPPv3N17i2s_parallel_en_t20I2S_PARALLEL_DISABLEE"></a> <a id="_CPPv2N17i2s_parallel_en_t20I2S_PARALLEL_DISABLEE"></a> <a id="group__bk__api__i2s__enum_1gga6810be6ead675ceab19dbbf64ae754ddaf35a820ba926dcd97fe653dd395c65c7"></a> enumerator I2S\_PARALLEL\_DISABLE
    :   I2S parallel disable

    <a id="_CPPv4N17i2s_parallel_en_t19I2S_PARALLEL_ENABLEE"></a>

    <a id="_CPPv3N17i2s_parallel_en_t19I2S_PARALLEL_ENABLEE"></a> <a id="_CPPv2N17i2s_parallel_en_t19I2S_PARALLEL_ENABLEE"></a> <a id="group__bk__api__i2s__enum_1gga6810be6ead675ceab19dbbf64ae754ddaecbd200132a39b844b272da7be610f77"></a> enumerator I2S\_PARALLEL\_ENABLE
    :   I2S parallel enable

    <a id="_CPPv4N17i2s_parallel_en_t19I2S_PARALLEL_EN_MAXE"></a>

    <a id="_CPPv3N17i2s_parallel_en_t19I2S_PARALLEL_EN_MAXE"></a> <a id="_CPPv2N17i2s_parallel_en_t19I2S_PARALLEL_EN_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga6810be6ead675ceab19dbbf64ae754dda6dfa9a15f38b7ceac7c2957d7a8dd612"></a> enumerator I2S\_PARALLEL\_EN\_MAX

<a id="_CPPv422i2s_lrcom_store_mode_t"></a>

<a id="_CPPv322i2s_lrcom_store_mode_t"></a> <a id="_CPPv222i2s_lrcom_store_mode_t"></a> <a id="group__bk__api__i2s__enum_1ga20383be83284262fc1214b1645d6cf3b"></a> enum i2s\_lrcom\_store\_mode\_t
:   *Values:*

    <a id="_CPPv4N22i2s_lrcom_store_mode_t20I2S_LRCOM_STORE_LRLRE"></a>

    <a id="_CPPv3N22i2s_lrcom_store_mode_t20I2S_LRCOM_STORE_LRLRE"></a> <a id="_CPPv2N22i2s_lrcom_store_mode_t20I2S_LRCOM_STORE_LRLRE"></a> <a id="group__bk__api__i2s__enum_1gga20383be83284262fc1214b1645d6cf3bad2eff697af7d063fdf5a9ae5e322424b"></a> enumerator I2S\_LRCOM\_STORE\_LRLR
    :   I2S lrcom store mode: L-\>R-\>L-\>R

    <a id="_CPPv4N22i2s_lrcom_store_mode_t22I2S_LRCOM_STORE_16R16LE"></a>

    <a id="_CPPv3N22i2s_lrcom_store_mode_t22I2S_LRCOM_STORE_16R16LE"></a> <a id="_CPPv2N22i2s_lrcom_store_mode_t22I2S_LRCOM_STORE_16R16LE"></a> <a id="group__bk__api__i2s__enum_1gga20383be83284262fc1214b1645d6cf3ba5eb32a90ae7b51a910aa0e68b5984b8a"></a> enumerator I2S\_LRCOM\_STORE\_16R16L
    :   I2S lrcom store mode: {16bitR,16bitL}

    <a id="_CPPv4N22i2s_lrcom_store_mode_t24I2S_LRCOM_STORE_MODE_MAXE"></a>

    <a id="_CPPv3N22i2s_lrcom_store_mode_t24I2S_LRCOM_STORE_MODE_MAXE"></a> <a id="_CPPv2N22i2s_lrcom_store_mode_t24I2S_LRCOM_STORE_MODE_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga20383be83284262fc1214b1645d6cf3ba00613127e00e2e54fbf04a48b0bbb2e5"></a> enumerator I2S\_LRCOM\_STORE\_MODE\_MAX

<a id="_CPPv417i2s_txint_level_t"></a>

<a id="_CPPv317i2s_txint_level_t"></a> <a id="_CPPv217i2s_txint_level_t"></a> <a id="group__bk__api__i2s__enum_1gade6e9a3f5e6ead066b32c6438c6114f0"></a> enum i2s\_txint\_level\_t
:   *Values:*

    <a id="_CPPv4N17i2s_txint_level_t17I2S_TXINT_LEVEL_1E"></a>

    <a id="_CPPv3N17i2s_txint_level_t17I2S_TXINT_LEVEL_1E"></a> <a id="_CPPv2N17i2s_txint_level_t17I2S_TXINT_LEVEL_1E"></a> <a id="group__bk__api__i2s__enum_1ggade6e9a3f5e6ead066b32c6438c6114f0a096402cf7d0c3ee250062196e7a8eb30"></a> enumerator I2S\_TXINT\_LEVEL\_1
    :   I2S tx\_int level: 1

    <a id="_CPPv4N17i2s_txint_level_t17I2S_TXINT_LEVEL_8E"></a>

    <a id="_CPPv3N17i2s_txint_level_t17I2S_TXINT_LEVEL_8E"></a> <a id="_CPPv2N17i2s_txint_level_t17I2S_TXINT_LEVEL_8E"></a> <a id="group__bk__api__i2s__enum_1ggade6e9a3f5e6ead066b32c6438c6114f0a7d73af4dda231d6d6065b3e90adb7c90"></a> enumerator I2S\_TXINT\_LEVEL\_8
    :   I2S tx\_int level: 8

    <a id="_CPPv4N17i2s_txint_level_t18I2S_TXINT_LEVEL_16E"></a>

    <a id="_CPPv3N17i2s_txint_level_t18I2S_TXINT_LEVEL_16E"></a> <a id="_CPPv2N17i2s_txint_level_t18I2S_TXINT_LEVEL_16E"></a> <a id="group__bk__api__i2s__enum_1ggade6e9a3f5e6ead066b32c6438c6114f0ae7b9df58ca1b90085400faba9aac66bd"></a> enumerator I2S\_TXINT\_LEVEL\_16
    :   I2S tx\_int level: 16

    <a id="_CPPv4N17i2s_txint_level_t18I2S_TXINT_LEVEL_24E"></a>

    <a id="_CPPv3N17i2s_txint_level_t18I2S_TXINT_LEVEL_24E"></a> <a id="_CPPv2N17i2s_txint_level_t18I2S_TXINT_LEVEL_24E"></a> <a id="group__bk__api__i2s__enum_1ggade6e9a3f5e6ead066b32c6438c6114f0ac8fb4e07f40269fb30db8abbd5b7e5c3"></a> enumerator I2S\_TXINT\_LEVEL\_24
    :   I2S tx\_int level: 24

    <a id="_CPPv4N17i2s_txint_level_t19I2S_TXINT_LEVEL_MAXE"></a>

    <a id="_CPPv3N17i2s_txint_level_t19I2S_TXINT_LEVEL_MAXE"></a> <a id="_CPPv2N17i2s_txint_level_t19I2S_TXINT_LEVEL_MAXE"></a> <a id="group__bk__api__i2s__enum_1ggade6e9a3f5e6ead066b32c6438c6114f0af642f40449ead5ec58a5b0e6d8d62a8e"></a> enumerator I2S\_TXINT\_LEVEL\_MAX

<a id="_CPPv417i2s_rxint_level_t"></a>

<a id="_CPPv317i2s_rxint_level_t"></a> <a id="_CPPv217i2s_rxint_level_t"></a> <a id="group__bk__api__i2s__enum_1ga868a4b0c12d7ac67de0be215233ceafb"></a> enum i2s\_rxint\_level\_t
:   *Values:*

    <a id="_CPPv4N17i2s_rxint_level_t17I2S_RXINT_LEVEL_1E"></a>

    <a id="_CPPv3N17i2s_rxint_level_t17I2S_RXINT_LEVEL_1E"></a> <a id="_CPPv2N17i2s_rxint_level_t17I2S_RXINT_LEVEL_1E"></a> <a id="group__bk__api__i2s__enum_1gga868a4b0c12d7ac67de0be215233ceafbaba0e0066a15aa1f12db25b28e8847846"></a> enumerator I2S\_RXINT\_LEVEL\_1
    :   I2S rx\_int level: 1

    <a id="_CPPv4N17i2s_rxint_level_t17I2S_RXINT_LEVEL_8E"></a>

    <a id="_CPPv3N17i2s_rxint_level_t17I2S_RXINT_LEVEL_8E"></a> <a id="_CPPv2N17i2s_rxint_level_t17I2S_RXINT_LEVEL_8E"></a> <a id="group__bk__api__i2s__enum_1gga868a4b0c12d7ac67de0be215233ceafba530abee71b1824777aa893d11b3b0a3e"></a> enumerator I2S\_RXINT\_LEVEL\_8
    :   I2S rx\_int level: 8

    <a id="_CPPv4N17i2s_rxint_level_t18I2S_RXINT_LEVEL_16E"></a>

    <a id="_CPPv3N17i2s_rxint_level_t18I2S_RXINT_LEVEL_16E"></a> <a id="_CPPv2N17i2s_rxint_level_t18I2S_RXINT_LEVEL_16E"></a> <a id="group__bk__api__i2s__enum_1gga868a4b0c12d7ac67de0be215233ceafba4a10ed5aa05a37c159a66dfaa652d2be"></a> enumerator I2S\_RXINT\_LEVEL\_16
    :   I2S rx\_int level: 16

    <a id="_CPPv4N17i2s_rxint_level_t18I2S_RXINT_LEVEL_24E"></a>

    <a id="_CPPv3N17i2s_rxint_level_t18I2S_RXINT_LEVEL_24E"></a> <a id="_CPPv2N17i2s_rxint_level_t18I2S_RXINT_LEVEL_24E"></a> <a id="group__bk__api__i2s__enum_1gga868a4b0c12d7ac67de0be215233ceafbae2d5e7e2f43102a6e1c2abf24a096c87"></a> enumerator I2S\_RXINT\_LEVEL\_24
    :   I2S rx\_int level: 24

    <a id="_CPPv4N17i2s_rxint_level_t19I2S_RXINT_LEVEL_MAXE"></a>

    <a id="_CPPv3N17i2s_rxint_level_t19I2S_RXINT_LEVEL_MAXE"></a> <a id="_CPPv2N17i2s_rxint_level_t19I2S_RXINT_LEVEL_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga868a4b0c12d7ac67de0be215233ceafbafcdd86edd707b7983c0f6c7af1b3ff42"></a> enumerator I2S\_RXINT\_LEVEL\_MAX

<a id="_CPPv412i2s_int_en_t"></a>

<a id="_CPPv312i2s_int_en_t"></a> <a id="_CPPv212i2s_int_en_t"></a> <a id="group__bk__api__i2s__enum_1ga8d95c0b103f09ea24afb76f828ed1bc8"></a> enum i2s\_int\_en\_t
:   *Values:*

    <a id="_CPPv4N12i2s_int_en_t15I2S_INT_DISABLEE"></a>

    <a id="_CPPv3N12i2s_int_en_t15I2S_INT_DISABLEE"></a> <a id="_CPPv2N12i2s_int_en_t15I2S_INT_DISABLEE"></a> <a id="group__bk__api__i2s__enum_1gga8d95c0b103f09ea24afb76f828ed1bc8aa2eabd2de96ec233bda2406a1cf5e004"></a> enumerator I2S\_INT\_DISABLE
    :   I2S interrupt disable

    <a id="_CPPv4N12i2s_int_en_t14I2S_INT_ENABLEE"></a>

    <a id="_CPPv3N12i2s_int_en_t14I2S_INT_ENABLEE"></a> <a id="_CPPv2N12i2s_int_en_t14I2S_INT_ENABLEE"></a> <a id="group__bk__api__i2s__enum_1gga8d95c0b103f09ea24afb76f828ed1bc8a0008a1ae8328ae6f5297056a4b6fb6a6"></a> enumerator I2S\_INT\_ENABLE
    :   I2S interrupt enable

    <a id="_CPPv4N12i2s_int_en_t14I2S_INT_EN_MAXE"></a>

    <a id="_CPPv3N12i2s_int_en_t14I2S_INT_EN_MAXE"></a> <a id="_CPPv2N12i2s_int_en_t14I2S_INT_EN_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga8d95c0b103f09ea24afb76f828ed1bc8a7dc6b25735532059a5c24228fcd7cce1"></a> enumerator I2S\_INT\_EN\_MAX

<a id="_CPPv416i2s_channel_id_t"></a>

<a id="_CPPv316i2s_channel_id_t"></a> <a id="_CPPv216i2s_channel_id_t"></a> <a id="group__bk__api__i2s__enum_1ga4f53a06646c134b140c0428889bf8a75"></a> enum i2s\_channel\_id\_t
:   *Values:*

    <a id="_CPPv4N16i2s_channel_id_t13I2S_CHANNEL_1E"></a>

    <a id="_CPPv3N16i2s_channel_id_t13I2S_CHANNEL_1E"></a> <a id="_CPPv2N16i2s_channel_id_t13I2S_CHANNEL_1E"></a> <a id="group__bk__api__i2s__enum_1gga4f53a06646c134b140c0428889bf8a75a39b0397e7c2c9c7fc6839897755d0af5"></a> enumerator I2S\_CHANNEL\_1
    :   I2S channel: 1

    <a id="_CPPv4N16i2s_channel_id_t13I2S_CHANNEL_2E"></a>

    <a id="_CPPv3N16i2s_channel_id_t13I2S_CHANNEL_2E"></a> <a id="_CPPv2N16i2s_channel_id_t13I2S_CHANNEL_2E"></a> <a id="group__bk__api__i2s__enum_1gga4f53a06646c134b140c0428889bf8a75a36b83f657450578d529b81a0960ce6d9"></a> enumerator I2S\_CHANNEL\_2
    :   I2S channel: 2

    <a id="_CPPv4N16i2s_channel_id_t13I2S_CHANNEL_3E"></a>

    <a id="_CPPv3N16i2s_channel_id_t13I2S_CHANNEL_3E"></a> <a id="_CPPv2N16i2s_channel_id_t13I2S_CHANNEL_3E"></a> <a id="group__bk__api__i2s__enum_1gga4f53a06646c134b140c0428889bf8a75ac61b88a1bcaa40d300c0f1603bb4c8b6"></a> enumerator I2S\_CHANNEL\_3
    :   I2S channel: 3

    <a id="_CPPv4N16i2s_channel_id_t15I2S_CHANNEL_MAXE"></a>

    <a id="_CPPv3N16i2s_channel_id_t15I2S_CHANNEL_MAXE"></a> <a id="_CPPv2N16i2s_channel_id_t15I2S_CHANNEL_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga4f53a06646c134b140c0428889bf8a75a2c489e4a718f667a14ecee4f19a670c4"></a> enumerator I2S\_CHANNEL\_MAX

<a id="_CPPv416i2s_data_width_t"></a>

<a id="_CPPv316i2s_data_width_t"></a> <a id="_CPPv216i2s_data_width_t"></a> <a id="group__bk__api__i2s__enum_1gab2447b7de6d72d4c513c68163db6464f"></a> enum i2s\_data\_width\_t
:   *Values:*

    <a id="_CPPv4N16i2s_data_width_t16I2S_DATA_WIDTH_8E"></a>

    <a id="_CPPv3N16i2s_data_width_t16I2S_DATA_WIDTH_8E"></a> <a id="_CPPv2N16i2s_data_width_t16I2S_DATA_WIDTH_8E"></a> <a id="group__bk__api__i2s__enum_1ggab2447b7de6d72d4c513c68163db6464faaa80783c88591793a371506b8076fa7b"></a> enumerator I2S\_DATA\_WIDTH\_8
    :   I2S data width: 8

    <a id="_CPPv4N16i2s_data_width_t17I2S_DATA_WIDTH_16E"></a>

    <a id="_CPPv3N16i2s_data_width_t17I2S_DATA_WIDTH_16E"></a> <a id="_CPPv2N16i2s_data_width_t17I2S_DATA_WIDTH_16E"></a> <a id="group__bk__api__i2s__enum_1ggab2447b7de6d72d4c513c68163db6464fa104fe189510e62a1366f15ccd8664267"></a> enumerator I2S\_DATA\_WIDTH\_16
    :   I2S data width: 16

    <a id="_CPPv4N16i2s_data_width_t17I2S_DATA_WIDTH_24E"></a>

    <a id="_CPPv3N16i2s_data_width_t17I2S_DATA_WIDTH_24E"></a> <a id="_CPPv2N16i2s_data_width_t17I2S_DATA_WIDTH_24E"></a> <a id="group__bk__api__i2s__enum_1ggab2447b7de6d72d4c513c68163db6464faa843edefe102386baa83f9c1e5e62be6"></a> enumerator I2S\_DATA\_WIDTH\_24
    :   I2S data width: 24

    <a id="_CPPv4N16i2s_data_width_t17I2S_DATA_WIDTH_32E"></a>

    <a id="_CPPv3N16i2s_data_width_t17I2S_DATA_WIDTH_32E"></a> <a id="_CPPv2N16i2s_data_width_t17I2S_DATA_WIDTH_32E"></a> <a id="group__bk__api__i2s__enum_1ggab2447b7de6d72d4c513c68163db6464fae5961b266bbc1cae077a78f6aae22669"></a> enumerator I2S\_DATA\_WIDTH\_32
    :   I2S data width: 32

<a id="_CPPv415i2s_samp_rate_t"></a>

<a id="_CPPv315i2s_samp_rate_t"></a> <a id="_CPPv215i2s_samp_rate_t"></a> <a id="group__bk__api__i2s__enum_1ga813d4b1c9cd0012cd24c87a41e691916"></a> enum i2s\_samp\_rate\_t
:   *Values:*

    <a id="_CPPv4N15i2s_samp_rate_t18I2S_SAMP_RATE_8000E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t18I2S_SAMP_RATE_8000E"></a> <a id="_CPPv2N15i2s_samp_rate_t18I2S_SAMP_RATE_8000E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916a46169b31a66985305953b0b2751138b4"></a> enumerator I2S\_SAMP\_RATE\_8000
    :   I2S sample rate: 8K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_12000E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_12000E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_12000E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916ad7fc2ebe630d03a6926350d20ea0e38f"></a> enumerator I2S\_SAMP\_RATE\_12000
    :   I2S sample rate: 12K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_16000E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_16000E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_16000E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916aa776252ffa27fe8020cb59d730dbf842"></a> enumerator I2S\_SAMP\_RATE\_16000
    :   I2S sample rate: 16K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_24000E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_24000E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_24000E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916abc5bb814c8992516189dd999a58c907b"></a> enumerator I2S\_SAMP\_RATE\_24000
    :   I2S sample rate: 24K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_32000E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_32000E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_32000E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916aab831fccbb42359ed7541dfed7de9738"></a> enumerator I2S\_SAMP\_RATE\_32000
    :   I2S sample rate: 32K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_48000E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_48000E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_48000E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916af26436dd4ceb95e36b79b8a889c52ea8"></a> enumerator I2S\_SAMP\_RATE\_48000
    :   I2S sample rate: 48K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_96000E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_96000E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_96000E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916a9f03a91cbe39ed4d3b31a985a32e080f"></a> enumerator I2S\_SAMP\_RATE\_96000
    :   I2S sample rate: 96K

    <a id="_CPPv4N15i2s_samp_rate_t18I2S_SAMP_RATE_8018E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t18I2S_SAMP_RATE_8018E"></a> <a id="_CPPv2N15i2s_samp_rate_t18I2S_SAMP_RATE_8018E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916ab1c2110d4695f8676ae37f183f566006"></a> enumerator I2S\_SAMP\_RATE\_8018
    :   I2S sample rate: 8.0182K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_11025E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_11025E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_11025E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916af89ff6913b451717cd1fdcfa1daec707"></a> enumerator I2S\_SAMP\_RATE\_11025
    :   I2S sample rate: 11.025K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_22050E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_22050E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_22050E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916a808f4fb35c5ce0255c8a09b6708e680b"></a> enumerator I2S\_SAMP\_RATE\_22050
    :   I2S sample rate: 22.050K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_44100E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_44100E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_44100E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916acedae405cd98bd534feaf9f647c138c9"></a> enumerator I2S\_SAMP\_RATE\_44100
    :   I2S sample rate: 44.1K

    <a id="_CPPv4N15i2s_samp_rate_t19I2S_SAMP_RATE_88200E"></a>

    <a id="_CPPv3N15i2s_samp_rate_t19I2S_SAMP_RATE_88200E"></a> <a id="_CPPv2N15i2s_samp_rate_t19I2S_SAMP_RATE_88200E"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916ab361e8338aa0f2875928a92082b6d26a"></a> enumerator I2S\_SAMP\_RATE\_88200
    :   I2S sample rate: 88.2K

    <a id="_CPPv4N15i2s_samp_rate_t17I2S_SAMP_RATE_MAXE"></a>

    <a id="_CPPv3N15i2s_samp_rate_t17I2S_SAMP_RATE_MAXE"></a> <a id="_CPPv2N15i2s_samp_rate_t17I2S_SAMP_RATE_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga813d4b1c9cd0012cd24c87a41e691916a3aed3cf606813f7bbfbbbf51085c4a9c"></a> enumerator I2S\_SAMP\_RATE\_MAX

<a id="_CPPv415i2s_txrx_type_t"></a>

<a id="_CPPv315i2s_txrx_type_t"></a> <a id="_CPPv215i2s_txrx_type_t"></a> <a id="group__bk__api__i2s__enum_1ga22a2a721fda3063d27d1a484f949ca07"></a> enum i2s\_txrx\_type\_t
:   *Values:*

    <a id="_CPPv4N15i2s_txrx_type_t16I2S_TXRX_TYPE_TXE"></a>

    <a id="_CPPv3N15i2s_txrx_type_t16I2S_TXRX_TYPE_TXE"></a> <a id="_CPPv2N15i2s_txrx_type_t16I2S_TXRX_TYPE_TXE"></a> <a id="group__bk__api__i2s__enum_1gga22a2a721fda3063d27d1a484f949ca07a60f15ba867a4e01e7644637bccbb06c8"></a> enumerator I2S\_TXRX\_TYPE\_TX

    <a id="_CPPv4N15i2s_txrx_type_t16I2S_TXRX_TYPE_RXE"></a>

    <a id="_CPPv3N15i2s_txrx_type_t16I2S_TXRX_TYPE_RXE"></a> <a id="_CPPv2N15i2s_txrx_type_t16I2S_TXRX_TYPE_RXE"></a> <a id="group__bk__api__i2s__enum_1gga22a2a721fda3063d27d1a484f949ca07ab32b985b97331f9239c867d04fb40046"></a> enumerator I2S\_TXRX\_TYPE\_RX

    <a id="_CPPv4N15i2s_txrx_type_t17I2S_TXRX_TYPE_MAXE"></a>

    <a id="_CPPv3N15i2s_txrx_type_t17I2S_TXRX_TYPE_MAXE"></a> <a id="_CPPv2N15i2s_txrx_type_t17I2S_TXRX_TYPE_MAXE"></a> <a id="group__bk__api__i2s__enum_1gga22a2a721fda3063d27d1a484f949ca07a1b279e3019a075de21b51703363612a0"></a> enumerator I2S\_TXRX\_TYPE\_MAX
