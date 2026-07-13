# SARADC


Beken chip supports get every adc channel value function for user.


## ADC API Status

| API | BK7259_AP |
| --- | --- |
| [`bk_adc_driver_init()`](#_CPPv418bk_adc_driver_initv "bk_adc_driver_init") | Y |
| `bk_adc_aquire()` | Y |
| [`bk_adc_release()`](#_CPPv414bk_adc_releasev "bk_adc_release") | Y |
| [`bk_adc_driver_deinit()`](#_CPPv420bk_adc_driver_deinitv "bk_adc_driver_deinit") | Y |
| [`bk_adc_init()`](#_CPPv411bk_adc_init10adc_chan_t "bk_adc_init") | Y |
| [`bk_adc_deinit()`](#_CPPv413bk_adc_deinit10adc_chan_t "bk_adc_deinit") | Y |
| [`bk_adc_start()`](#_CPPv412bk_adc_startv "bk_adc_start") | Y |
| [`bk_adc_stop()`](#_CPPv411bk_adc_stopv "bk_adc_stop") | Y |
| [`bk_adc_read_raw()`](#_CPPv415bk_adc_read_rawP8uint16_t8uint32_t8uint32_t "bk_adc_read_raw") | Y |
| [`bk_adc_read()`](#_CPPv411bk_adc_readP8uint16_t8uint32_t "bk_adc_read") | Y |
| [`bk_adc_register_isr()`](#_CPPv419bk_adc_register_isr9adc_isr_t8uint32_t "bk_adc_register_isr") | Y |
| [`bk_adc_set_clk()`](#_CPPv414bk_adc_set_clk13adc_src_clk_t8uint32_t "bk_adc_set_clk") | Y |
| [`bk_adc_set_channel()`](#_CPPv418bk_adc_set_channel10adc_chan_t "bk_adc_set_channel") | Y |
| [`bk_adc_set_sample_rate()`](#_CPPv422bk_adc_set_sample_rate8uint32_t "bk_adc_set_sample_rate") | Y |
| [`bk_adc_set_filter()`](#_CPPv417bk_adc_set_filter8uint32_t "bk_adc_set_filter") | Y |
| [`bk_adc_set_steady_time()`](#_CPPv422bk_adc_set_steady_time8uint32_t "bk_adc_set_steady_time") | Y |
| [`bk_adc_set_sample_cnt()`](#_CPPv421bk_adc_set_sample_cnt8uint32_t "bk_adc_set_sample_cnt") | Y |
| `bk_adc_enable_saturate()` | Y |
| `bk_adc_disable_saturate()` | Y |
| `bk_adc_set_saturate()` | Y |
| [`bk_adc_get_saturate()`](#_CPPv419bk_adc_get_saturateP19adc_saturate_mode_t "bk_adc_get_saturate") | Y |
| [`bk_adc_set_config()`](#_CPPv417bk_adc_set_configP12adc_config_t "bk_adc_set_config") | Y |
| [`bk_adc_set_mode()`](#_CPPv415bk_adc_set_mode10adc_mode_t "bk_adc_set_mode") | Y |
| [`bk_adc_get_mode()`](#_CPPv415bk_adc_get_modev "bk_adc_get_mode") | Y |


## ADC Channel Number

| Capability | BK7259_AP |
| --- | --- |
| Channel Number | 6 |


## ADC API Reference


### Header File


- [adc.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/adc.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/adc.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_driver_init(void)
:   Init the ADC driver.

    This API init the resoure common to all ADC id:


    - Init ADC driver control memory


    **Attention**
    :   1. This API should be called before any other ADC APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_acquire(void)
:   lock the runing ADC channel

    This API lock ADC channel which is runing.

    参数
    :   **id** – ADC id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_release()
:   release the runing ADC channel

    This API release ADC channel which is runing.

    参数
    :   **id** – ADC id

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_driver_deinit(void)
:   Deinit the ADC driver.

    This API free all resource related to ADC and power down all ADC.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_init([adc_chan_t](#_CPPv410adc_chan_t "adc_chan_t") adc_id)
:   Init the ADC.

    This API init the ADC:


    - Power up the ADC

    - Map the ADC id to dedicated GPIO port

    - Set adc work channel

    参数
    :   - **id** – ADC channel

        - **size** – ADC recieve data size

    返回
    :   - BK_OK: succeed

        - BK_ERR_ADC_NOT_INIT: ADC driver not init

        - BK_ERR_ADC_INVALID_ID: ADC id is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_deinit([adc_chan_t](#_CPPv410adc_chan_t "adc_chan_t") id)
:   Deinit the ADC id.

    This API deinit the ADC id:


    - Stop the ADC

    - Disable the ADC id interrupt

    - Power down the ADC

    - Unmap gpio id


    **Attention**
    :   1. This API should be called before use adc.

    参数
    :   **id** – ADC id

    返回
    :   - BK_OK: succeed

        - BK_ERR_ADC_NOT_INIT: ADC driver not init

        - BK_ERR_ADC_INVALID_ID: ADC id is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_start(void)
:   Start the ADC.

    This API start adc:


    - enable the ADC id interrupt

    返回
    :   - BK_OK: succeed

        - BK_ERR_ADC_BUSY: ADC is busy

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_stop(void)
:   Stop the ADC.

    This API stop adc:


    - disable the ADC en bit

    返回
    :   - BK_OK: succeed

        - BK_ERR_ADC_BUSY: ADC is busy

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_read_raw(uint16_t *read_buf, uint32_t size, uint32_t timeout)
:   Start read the raw ADC data in continuous mode.


    **Attention**
    :   1. The read_buf is in unit of uint16_t, the application needs to malloc (size * 2) bytes for read_buf.


    **Attention**
    :   2. The maximum value of size is CONFIG_ADC_BUF_SIZE, if the size exceeds CONFIG_ADC_BUF_SIZE, the API returns BK_ERR_ADC_SIZE_TOO_BIG.

    参数
    :   - **read_buf** – application malloc buffer which save the current adc value

        - **size** – the size of read_buf, the unit of size is uint16_t

        - **timeout** – adc read semaphore timeout

    返回
    :   - BK_ERR_ADC_BUSY: ADC is busy

        - BK_ERR_ADC_INVALID_MODE: ADC mode is invalid

        - BK_ERR_ADC_SIZE_TOO_BIG: size is too big

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_single_read(uint16_t *data)
:   Start read the raw ADC data in single mode.

    参数
    :   **data** – ADC sample data

    返回
    :   - BK_OK: success.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_read(uint16_t *data, uint32_t timeout)
:   Start read the average value of sampling data.


    - BK_ERR_ADC_BUSY: ADC is busy

    - BK_ERR_ADC_INVALID_MODE: ADC mode is invalid

    - others: other errors.

    参数
    :   - **data** – store the average value of all sample values in ADC software buffers

        - **timeout** – adc read semaphore timeout

    返回

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_register_isr([adc_isr_t](#_CPPv49adc_isr_t "adc_isr_t") isr, uint32_t param)
:   Register the adc interrupt service routine.

    参数
    :   - **isr** – ADC intterrupt callback

        - **param** – ADC sample data size which depend on user

    返回
    :   - BK_OK: succeed

        - BK_ERR_ADC_NOT_INIT: adc not init

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_set_clk([adc_src_clk_t](#_CPPv413adc_src_clk_t "adc_src_clk_t") src_clk, uint32_t clk)
:   set ADC source clock and work frequence

    This API set adc clock source and frequence

    参数
    :   - **src_clk** – adc source clock

        - **clk** – adc work clock :adc clk

    返回
    :   - BK_OK: succeed

        - BK_ERR_ADC_INVALID_SCLK_MODE: ADC source clock is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_set_channel([adc_chan_t](#_CPPv410adc_chan_t "adc_chan_t") adc_id)
:   set ADC work channel

    This API set adc work channel

    参数
    :   **adc_id** – adc channel

    返回
    :   - BK_OK: succeed

        - BK_ERR_ADC_INVALID_ID: ADC invalid id

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_set_sample_rate(uint32_t sample_rate)
:   set ADC sample rate

    This API set adc work sample rate, period = (16 + sample_rate)*adc_clk mcu output 16 adc_clks every period

    参数
    :   **sample_rate** – adc sample rate

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_set_filter(uint32_t filter)
:   set ADC filter

    This API set adc filter, the value default < 64, data output rate = period/(filter + 1)

    参数
    :   **filter** – adc filter

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_set_steady_time(uint32_t steady_ctrl)
:   set ADC steady time

    This API set adc filter, adc wait (steady_ctrl +1)*8 adc_clks to send valid

    参数
    :   **steady_ctrl** – adc steady time

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_set_sample_cnt(uint32_t cnt)
:   set ADC sample cnt

    This API sets ADC sample cnt per-interrupt, the ADC raises the interrupt when every time it samples number of cnt times. The maximum value of cnt is 32.

    参数
    :   **cnt** – per-interrupt sample cnt

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_set_saturate_mode([adc_saturate_mode_t](#_CPPv419adc_saturate_mode_t "adc_saturate_mode_t") mode)
:   set adc saturate

    This API set adc saturate, auto process adc fifo data in cpu ,just get the data from reg ADC_DATA_16

    参数
    :   **mode** – adc saturate

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_get_saturate([adc_saturate_mode_t](#_CPPv419adc_saturate_mode_t "adc_saturate_mode_t") *mode)
:   get adc saturate

    This API get adc saturate

    返回
    :   - adc_saturate_mode_t: adc saturate mode

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_enable_bypass_clalibration(void)
:   enable ADC bypass calibration

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_disable_bypass_clalibration(void)
:   disable ADC bypass calibration

    返回
    :   - BK_OK: succeed

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_set_config([adc_config_t](#_CPPv412adc_config_t "adc_config_t") *config)
:   adc set config

    This API config adc params

    参数
    :   **config** – adc parameter settings

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM : param is null

        - BK_ERR_ADC_INVALID_MODE:adc invalid mode

        - BK_ERR_ADC_INVALID_SCLK_MODE: ADC source clock is invalid

        - BK_ERR_ADC_INVALID_ID: ADC id is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_set_mode([adc_mode_t](#_CPPv410adc_mode_t "adc_mode_t") adc_mode)
:   adc set mode

    This API config adc mode

    参数
    :   **mode** – : adc mode:


        - 0: sleep mode: adc is power down in this mode

        - 1: single step mode: adc finish sample data convesion once after enable adc and wait mcu to read sample data. The mode will turn to sleep mode after mcu read this sample date It must be enabled again when you want to sample next data.

        - 2: software control mode: adc gengerate interrupt after sample data convesion wait mcu to read sample data. adc will convert sample data after mcu reading this sample date from data register and software cleaning int flag.

        - 3: continous mode:adc wait adc_setting time to sample data, and generate int flag after finish sample data convesion, then always repeat last sample way. This mode don’t depend on muc reading data register.

    返回
    :   - BK_OK: succeed

        - BK_ERR_ADC_INVALID_MODE:adc invalid mode

        - others: other errors.

[adc_mode_t](#_CPPv410adc_mode_t "adc_mode_t") bk_adc_get_mode(void)
:   get adc mode

    This API get adc work mode

    返回
    :   - adc_mode_t: adc_mode

UINT16 bk_adc_data_calculate(UINT16 adc_val, UINT8 adc_chan)
:   calculate adc data

    This API get volt

    返回
    :   - float: volt

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_chan_init_gpio([adc_chan_t](#_CPPv410adc_chan_t "adc_chan_t") chan)
:   Init the ADC GPIO.

    This API init the ADC gpio:


    - Map the ADC gpio


    **Attention**
    :   1. This API should be called before use adc.

    参数
    :   **id** – ADC id

    返回

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_chan_deinit_gpio([adc_chan_t](#_CPPv410adc_chan_t "adc_chan_t") chan)
:   Deinit the ADC GPIO.

    This API Deinit the ADC gpio:


    - Unmap the ADC gpio


    **Attention**
    :   1. This API should be called before use adc.

    参数
    :   **id** – ADC id

    返回

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_key_sampler_start([adc_chan_t](#_CPPv410adc_chan_t "adc_chan_t") chan, uint32_t sample_period_ms)
:   Start CP-side periodic ADC key sampler.

    参数
    :   - **chan** – ADC channel to sample.

        - **sample_period_ms** – Sampling period in milliseconds.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_adc_key_sampler_stop(void)
:   Stop CP-side periodic ADC key sampler.

    返回
    :   - BK_OK: succeed

        - others: other errors.


## ADC API Typedefs


### Header File


- [adc_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/adc_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/adc_types.h")


### Macros

BK_ERR_ADC_NOT_INIT
:   ADC driver not init

BK_ERR_ADC_INVALID_CHAN
:   ADC chan number is invalid

BK_ERR_ADC_BUSY
:   ADC channel is busy

BK_ERR_ADC_INVALID_MODE
:   ADC invalid mode

BK_ERR_ADC_CHAN_NOT_INIT
:   ADC chan not init

BK_ERR_ADC_INVALID_SCLK_MODE
:   ADC no such source clock

BK_ERR_ADC_INIT_MUTEX
:   ADC mutex lock

BK_ERR_ADC_GET_READ_SEMA
:   ADC get semaphore error

BK_ERR_ADC_INIT_READ_SEMA
:   ADC read data error

BK_ERR_ADC_SIZE_TOO_BIG
:   ADC read size is bigger than adc driver buffer size

BK_ERR_SARADC_WAIT_CB_NOT_REGISTER
:   ADC wait cb is not registered but tried to unregister

BK_ERR_ADC_INSUFFICIENT_MEM
:   ADC out of memory

BK_ERR_ADC_DEINIT_MUTEX
:   ADC mutex deinit failed

BK_ERR_ADC_DEINIT_READ_SEMA
:   ADC read sync deinit failed

BK_ERR_ADC_DPLL_NOT_SUPPORTED
:   ADC DPLL clock source not supported

CONFIG_ADC_BUF_SIZE

CONFIG_ADC_SAMPLE_CAPACITY_CNT


### Type Definitions

typedef void (*adc_isr_t)(uint32_t param)
:   ADC interrupt service routine.

typedef void (*adc_isr_cb)(uint32_t param)


### Header File


- [hal/hal_adc_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_adc_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_adc_types.h")


### Structures

struct adc_config_t

struct adc_gpio_map_t


### Macros

CONFIG_ADC_STATIS

ADC_ACURACY_10_BIT

ADC_ACURACY_12_BIT

ADC_READ_SEMAPHORE_WAIT_TIME

ADC_SRC_DCO_CLK

ADC_SRC_DPLL_CLK

ADC_SRC_26M_CLK

ADC_SRC_40M_CLK

ADC_SRC_32M_CLK

ADC_FIFO_LEVEL_MAX


### Enumerations

enum adc_src_clk_t
:   *Values:*

    enumerator ADC_SCLK_DCO
    :   ADC source clock dco

    enumerator ADC_SCLK_XTAL
    :   ADC source clock xtal 26M/40M

    enumerator ADC_SCLK_DPLL
    :   ADC source clock dpll

    enumerator ADC_SCLK_32M
    :   ADC source clock 32M

    enumerator ADC_SCLK_NONE
    :   ADC has not such source clock

enum adc_mode_t
:   *Values:*

    enumerator ADC_SLEEP_MODE
    :   ADC sleep mode

    enumerator ADC_SINGLE_STEP_MODE
    :   ADC single step mode

    enumerator ADC_SOFTWARE_CONTRL_MODE
    :   ADC software control mode

    enumerator ADC_CONTINUOUS_MODE
    :   ADC continuous mode

    enumerator ADC_NONE_MODE

enum adc_chan_t
:   *Values:*

    enumerator ADC_0

    enumerator ADC_1

    enumerator ADC_2

    enumerator ADC_3

    enumerator ADC_4

    enumerator ADC_5

    enumerator ADC_6

    enumerator ADC_7

    enumerator ADC_8

    enumerator ADC_9

    enumerator ADC_10

    enumerator ADC_11

    enumerator ADC_12

    enumerator ADC_13

    enumerator ADC_14

    enumerator ADC_15

    enumerator ADC_MAX

enum adc_saturate_mode_t
:   *Values:*

    enumerator ADC_SATURATE_MODE_NONE

    enumerator ADC_SATURATE_MODE_0

    enumerator ADC_SATURATE_MODE_1

    enumerator ADC_SATURATE_MODE_2

    enumerator ADC_SATURATE_MODE_3

enum adc_vol_div_t
:   *Values:*

    enumerator ADC_VOL_DIV_NONE

    enumerator ADC_VOL_DIV_1

    enumerator ADC_VOL_DIV_2

    enumerator ADC_VOL_DIV_3

    enumerator ADC_VOL_DIV_4

    enumerator ADC_VOL_DIV_5

    enumerator ADC_VOL_DIV_7
