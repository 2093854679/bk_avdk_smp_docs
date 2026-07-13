# PSRAM


BK7259 AP 侧 PSRAM API（`include/driver/psram.h`、`include/driver/qspi_psram.h`）。
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

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_deinit(void)
:   Deinit the PSRAM HW.

    This API free the resoure common to PSRAM:


    - Init PSRAM HW control register

    - power down PSRAM voltage

    @attation 1. after calling this function, this api bk_psram_resume can not enable psram function

    返回
    :   - BK_OK: succeed

        - others: other errors.

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

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_set_clk([psram_clk_t](#_CPPv411psram_clk_t "psram_clk_t") clk)
:   set psram clk

    This API used to set psram work clk

    参数
    :   **clk:80/120/160/240** – @attation 1. current only support 80/120/160

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_set_voltage([psram_voltage_t](#_CPPv415psram_voltage_t "psram_voltage_t") voltage)
:   set psram voltage

    This API used to set psram work voltage

    @attation 1. current only used 1.8v

    参数
    :   **voltage** – 1.8/2.0/3.0/3.2

    返回
    :   - BK_OK: succeed

        - others: other errors.

char *bk_psram_strcat(char *start_addr, const char *data_buf)
:   string cat to psram

    This API is like strcat

    参数
    :   - **start_addr** – write to psram start addr

        - **data_buf** – string buffer pointer

    返回
    :   psram start addr

[psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") bk_psram_alloc_write_through_channel(void)
:   Allocate a write-through channel (area) from the default pool.

    Returns the next available area (0~7) for configuring PSRAM write-through. Prefer [bk_psram_alloc_write_through_channel_with_psram_id()](#group__bk__api__psram_1ga119f58f6fca3b43c6d868398180e6820 "#group__bk__api__psram_1ga119f58f6fca3b43c6d868398180e6820") when the buffer is known to lie in PSRAM0 or PSRAM1 so that the area matches the chip.

    返回
    :   Allocated area (PSRAM_WRITE_THROUGH_AREA_0 ~ _AREA_7), or PSRAM_WRITE_THROUGH_AREA_COUNT if no channel is available.

[psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") bk_psram_alloc_write_through_channel_with_psram_id(uint8_t psram_id)
:   alloc write_through_area for specific PSRAM

    Use when buffer is in a known PSRAM: psram_id 0 -> returns area 0~3, psram_id 1 -> returns area 4~7.

    参数
    :   **psram_id** – 0=PSRAM0, 1=PSRAM1

    返回
    :   allocated area (0~7), or PSRAM_WRITE_THROUGH_AREA_COUNT on failure

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

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_psram_disable_write_through([psram_write_through_area_t](#_CPPv426psram_write_through_area_t "psram_write_through_area_t") area)
:   Disable PSRAM write through area.


    - BK_OK: succeed

    - BK_ERR_PSRAM_AREA: invalid area

    参数
    :   **area** – PSRAM write through area id

    返回

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

PSRAM_WRITE_THROUGH_AREA_PER_PSRAM


### Enumerations

enum psram_clk_t
:   *Values:*

    enumerator PSRAM_240M

    enumerator PSRAM_160M

    enumerator PSRAM_120M

    enumerator PSRAM_80M

enum psram_voltage_t
:   *Values:*

    enumerator PSRAM_OUT_3_20V

    enumerator PSRAM_OUT_3_0V

    enumerator PSRAM_OUT_2_0V

    enumerator PSRAM_OUT_1_95V

    enumerator PSRAM_OUT_1_90V

    enumerator PSRAM_OUT_1_85V

    enumerator PSRAM_OUT_1_80V

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

    enumerator PSRAM_WRITE_THROUGH_AREA_4

    enumerator PSRAM_WRITE_THROUGH_AREA_5

    enumerator PSRAM_WRITE_THROUGH_AREA_6

    enumerator PSRAM_WRITE_THROUGH_AREA_7

    enumerator PSRAM_WRITE_THROUGH_AREA_COUNT

备注

QSPI PSRAM 相关 API（`qspi_psram.h`）见 [QSPI API](bk_qspi.md "bk_qspi.md")。
