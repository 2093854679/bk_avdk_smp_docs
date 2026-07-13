# PSRAM


BK7259 CP 侧 PSRAM API（`include/driver/psram.h`、`include/driver/qspi_psram.h`）。
详细说明见 [PSRAM 开发指南](../../developer-guide/peripheral/bk_psram.md "../../developer-guide/peripheral/bk_psram.md")。


## PSRAM API Reference


### Header File


- [psram.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/psram.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/psram.h")


### Functions

static inline void bk_psram_byte_write(unsigned char *addr, unsigned char value)
:   write one byte of data to psram

    参数
    :   - **addr** – the psram address to write to

        - **value** – the value of one byte of data

    返回
    :   - NULL

static inline void bk_psram_half_word_write(unsigned short *dst, unsigned short value)
:   write two bytes of data to psram

    参数
    :   - **addr** – the psram address to write to

        - **value** – the value of two bytes of data

    返回
    :   - NULL

static inline void bk_psram_word_write(unsigned int *src, unsigned int value)
:   write one word of data to psram

    参数
    :   - **addr** – the psram address to write to

        - **value** – the value of one word of data

    返回
    :   - NULL

static inline void bk_psram_word_memcpy(void *dst_t, void *src_t, unsigned int length)
:   psram memory copy

    @attation 1. length unit is byte

    参数
    :   - **dst_t** – the destination address to be copied to

        - **src_t** – the source address to be copied

        - **length** – length of the data copy

    返回
    :   - NULL

bool bk_psram_heap_init_flag_get()
:   get psram heap init flag

    This API to get psram heap init flag:


    - init: true:init ;false:uninit

    返回
    :   heap_init_flag

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_heap_init_flag_set(bool init)
:   set psram heap init flag

    This API set psram heap init flag:


    - init: true:init;false:uninit

    This API should be called before using the psram heap.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_id_auto_detect(void)
:   detect psram id

    This API get psram chip id from easy flash, if easy flash function enable

    This API should be called when chip boot, must before bk_psram_init.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_init(void)
:   Init the PSRAM HW.

    This API init the resoure common to all PSRAM:


    - Psram power up, configure the clock control register

    - Select a frequency multiple

    - Psram config

    This API should be called before any other PSRAM APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_init_with_id([psram_id_t](#_CPPv410psram_id_t "psram_id_t") psram_id)
:   Init the specified PSRAM instance (PSRAM0/PSRAM1)

    参数
    :   **psram_id** – PSRAM instance id (PSRAM_ID_0 / PSRAM_ID_1)

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_deinit(void)
:   Deinit the PSRAM HW.

    This API free the resoure common to PSRAM:


    - Init PSRAM HW control register

    - power down PSRAM voltage

    @attation 1. after calling this function, this api bk_psram_resume can not enable psram function

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_deinit_with_id([psram_id_t](#_CPPv410psram_id_t "psram_id_t") psram_id)
:   Deinit the specified PSRAM instance (PSRAM0/PSRAM1)

    参数
    :   **psram_id** – PSRAM instance id (PSRAM_ID_0 / PSRAM_ID_1)

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_data_retention(void)
:   Prepare PSRAM for data-retention across an AP/M55 power-down.

    Replaces [bk_psram_deinit()](#group__bk__api__psram_1ga6769383edf8fcb4123d7ff969df851ca "#group__bk__api__psram_1ga6769383edf8fcb4123d7ff969df851ca") in scenarios where PSRAM cell data must survive the AP power cycle. Unlike [bk_psram_deinit()](#group__bk__api__psram_1ga6769383edf8fcb4123d7ff969df851ca "#group__bk__api__psram_1ga6769383edf8fcb4123d7ff969df851ca") this function:


    - flushes the controller write buffer (no dirty data lost when AHBP clock is gated together with the M55 power-domain);

    - latches PSRAM I/O pads at 3V (ana_reg5.gpio_latch=1);

    - keeps PSRAM voltage LDO ON.

    Pair with [bk_psram_data_retention_recover()](#group__bk__api__psram_1ga057c1e2c7152e32d00f36aede540349a "#group__bk__api__psram_1ga057c1e2c7152e32d00f36aede540349a") after AP power-on.

    返回
    :   BK_OK on success.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_data_retention_recover(void)
:   Recover the PSRAM controller after a retention cycle.

    Pair function of [bk_psram_data_retention()](#group__bk__api__psram_1ga8e75bd8851e39c0084e1f15a6037c87e "#group__bk__api__psram_1ga8e75bd8851e39c0084e1f15a6037c87e"). Releases the GPIO/PSRAM pad latch and rebuilds the minimum controller state (clock-gating bypass + clock re-select + soft-reset + mode-register reload) so that the external PSRAM cells, whose data was preserved, become addressable again without going through the full [bk_psram_init()](#group__bk__api__psram_1gabf47723a4eb610a6ceb7b3d441b8d6a5 "#group__bk__api__psram_1gabf47723a4eb610a6ceb7b3d441b8d6a5") detection sequence.

    If [bk_psram_data_retention()](#group__bk__api__psram_1ga8e75bd8851e39c0084e1f15a6037c87e "#group__bk__api__psram_1ga8e75bd8851e39c0084e1f15a6037c87e") was not called before (i.e. no active retention state), this falls back to [bk_psram_init()](#group__bk__api__psram_1gabf47723a4eb610a6ceb7b3d441b8d6a5 "#group__bk__api__psram_1gabf47723a4eb610a6ceb7b3d441b8d6a5").

    返回
    :   BK_OK on success.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_memcpy(uint8_t *start_addr, uint8_t *data_buf, uint32_t len)
:   continue write data to psram

    This API will write more fast than dtim

    @attation 1. len uint byte

    参数
    :   - **start_addr** – write to psram start addr

        - **data_buf** – data buffer pointer

        - **len** – data len need write to psram

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_memread(uint8_t *start_addr, uint8_t *data_buf, uint32_t len)
:   continue read data from psram

    This API will read more fast than dtim

    @attation 1. len uint byte

    参数
    :   - **start_addr** – read from psram start addr

        - **data_buf** – data buffer pointer

        - **len** – data len need read from psram

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_set_clk_with_id([psram_id_t](#_CPPv410psram_id_t "psram_id_t") psram_id, [psram_clk_t](#_CPPv411psram_clk_t "psram_clk_t") clk)
:   set psram clk

    This API used to set psram work clk

    参数
    :   **clk:80/120/160/240** – @attation 1. current only support 80/120/160 @attation 2. Recommended default PSRAM clock: 120 MHz

    返回
    :   - BK_OK: succeed

        - others: other errors.

uint32_t bk_psram_get_psram_id(void)
:   get psram id

    This API used to get psram id

    返回
    :   - psram_id

uint32_t bk_psram_get_psram_data_length(uint32_t id)
:   get psram data length

    This API used to get psram data length

    参数
    :   **id:psram** – chip id

    返回
    :   - data_length

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_set_voltage([psram_voltage_t](#_CPPv415psram_voltage_t "psram_voltage_t") voltage)
:   set psram voltage

    This API used to set psram work voltage

    @attation 1. current only used 1.8v

    参数
    :   **voltage** – 1.8/2.0/3.0/3.2

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_init_with_para(uint32_t psram_clk, uint32_t psram_vol)
:   Init psram with specified clock/voltage (legacy CLI helper)

    参数
    :   - **psram_clk** – Clock in MHz (80/120/160/240) or psram_clk_t enum value

        - **psram_vol** – Voltage in mV (e.g. 1950) or centi-volt (e.g. 195)

char *bk_psram_strcat(char *start_addr, const char *data_buf)
:   string cat to psram

    This API is like strcat

    参数
    :   - **start_addr** – write to psram start addr

        - **data_buf** – string buffer pointer

    返回
    :   psram start addr

[psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") bk_psram_alloc_write_through_channel(void)
:   alloc write_through_area

    This API is alloc a area


    **Attention**
    :   1. The write through area is used for DMA2D accessing only, do not use it for CPU accessing PSRAM

    返回
    :   channel

[psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") bk_psram_alloc_write_through_channel_with_id([psram_id_t](#_CPPv410psram_id_t "psram_id_t") psram_id)
:   alloc write_through_area for specified PSRAM instance

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_free_write_through_channel([psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area)
:   free write_through_area

    This API is free a area


    - BK_OK: succeed

    - BK_ERR_PSRAM_ADDR_ALIGN: start or end is not 32 bytes aligned

    - BK_ERR_PSRAM_ADDR_OUT_OF_RANGE: start or end is invalid PSRAM address

    - BK_ERR_PSRAM_ADDR_RELATION: start >= end

    - BK_ERR_PSRAM_AREA: invalid area


    **Attention**
    :   1. The write through area is used for DMA2D accessing only, do not use it for CPU accessing PSRAM

    返回

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_free_write_through_channel_with_id([psram_id_t](#_CPPv410psram_id_t "psram_id_t") psram_id, [psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area)
:   free write_through_area for specified PSRAM instance

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_enable_write_through([psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area, uint32_t start, uint32_t end)
:   Enable and config PSRAM write through area.

    This API enables PSRAM write through area. The PSRAM hardware will always flush it’s internal cache-line, without considering whether the cache line is full or not, thus to improve the writing performance.


    - BK_OK: succeed

    - BK_ERR_PSRAM_ADDR_ALIGN: start or end is not 32 bytes aligned

    - BK_ERR_PSRAM_ADDR_OUT_OF_RANGE: start or end is invalid PSRAM address

    - BK_ERR_PSRAM_ADDR_RELATION: start >= end

    - BK_ERR_PSRAM_AREA: invalid area


    **Attention**
    :   1. The write through area must only one master access, and the write length must integer multiples 32bytes, you can write by cpu/dma/dma2d.

    参数
    :   - **area** – PSRAM write through area

        - **start** – PSRAM write through area start address, should be 32 bytes aligned

        - **start** – PSRAM write through area end address, should be 32 bytes aligned

    返回

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_enable_write_through_with_id([psram_id_t](#_CPPv410psram_id_t "psram_id_t") psram_id, [psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area, uint32_t start, uint32_t end)
:   Enable and config PSRAM write through area for specified PSRAM instance.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_disable_write_through([psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area)
:   Disable PSRAM write through area.


    - BK_OK: succeed

    - BK_ERR_PSRAM_AREA: invalid area

    参数
    :   **area** – PSRAM write through area id

    返回

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_disable_write_through_with_id([psram_id_t](#_CPPv410psram_id_t "psram_id_t") psram_id, [psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area)
:   Disable PSRAM write through area for specified PSRAM instance.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_calibrate(void)


## PSRAM API Typedefs


### Header File


- [psram_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/psram_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/psram_types.h")


### Macros

PSRAM_CHIP_ID

BK_ERR_PSRAM_SERVER_NOT_INIT
:   psram server not init

BK_ERR_PSRAM_ADDR_ALIGN

BK_ERR_PSRAM_ADDR_OUT_OF_RANGE

BK_ERR_PSRAM_ADDR_RELATION

BK_ERR_PSRAM_AREA


### Enumerations

enum psram_id_t
:   *Values:*

    enumerator PSRAM_ID_0

    enumerator PSRAM_ID_1

    enumerator PSRAM_ID_MAX

enum psram_clk_t
:   *Values:*

    enumerator PSRAM_480M

    enumerator PSRAM_240M

    enumerator PSRAM_160M

    enumerator PSRAM_120M

    enumerator PSRAM_80M

    enumerator PSRAM_640M

enum psram_voltage_t
:   *Values:*

    enumerator PSRAM_OUT_3_20V

    enumerator PSRAM_OUT_3_0V

    enumerator PSRAM_OUT_2_0V

    enumerator PSRAM_OUT_1_95V

    enumerator PSRAM_OUT_1_90V

    enumerator PSRAM_OUT_1_85V

    enumerator PSRAM_OUT_1_80V

    enumerator PSRAM_OUT_1_50V

    enumerator PSRAM_OUT_1_20V

enum psram_tansfer_mode_t
:   *Values:*

    enumerator PSRAM_INCRASE_TRANS

    enumerator PSRAM_32_WORD_WRAP

    enumerator PSRAM_64_WORD_WRAP

    enumerator PSRAM_128_WORD_WRAP

    enumerator PSRAM_256_WORD_WRAP

    enumerator PSRAM_512_WORD_WRAP

    enumerator PSRAM_1024_WORD_WRAP

    enumerator PSRAM_2048_WORD_WRAP

enum psram_write_through_area_t
:   *Values:*

    enumerator PSRAM_WRITE_THROUGH_AREA_0

    enumerator PSRAM_WRITE_THROUGH_AREA_1

    enumerator PSRAM_WRITE_THROUGH_AREA_2

    enumerator PSRAM_WRITE_THROUGH_AREA_3

    enumerator PSRAM_WRITE_THROUGH_AREA_COUNT

备注

QSPI PSRAM 相关 API（`qspi_psram.h`）见 [QSPI API](bk_qspi.md "bk_qspi.md")。
