---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_adc.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="saradc"></a>

# SARADC

Beken chip supports get every adc channel value function for user.

<a id="adc-api-status"></a>

## ADC API Status

| API | BK7258\_AP |
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

<a id="adc-channel-number"></a>

## ADC Channel Number

| Capability | BK7258\_AP |
| --- | --- |
| Channel Number | 6 |

<a id="adc-api-reference"></a>

## ADC API Reference

<a id="header-file"></a>

### Header File

- [adc.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/adc.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_adc_driver_initv"></a>

<a id="_CPPv318bk_adc_driver_initv"></a> <a id="_CPPv218bk_adc_driver_initv"></a> <a id="bk_adc_driver_init__void"></a> <a id="group__bk__api__adc_1ga684e48484c76e3b06cb958deab3bb31c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_driver\_init(void)
:   Init the ADC driver.

    This API init the resoure common to all ADC id:

    - Init ADC driver control memory

    **Attention**
    :   1\. This API should be called before any other ADC APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv414bk_adc_acquirev"></a>

<a id="_CPPv314bk_adc_acquirev"></a> <a id="_CPPv214bk_adc_acquirev"></a> <a id="bk_adc_acquire__void"></a> <a id="group__bk__api__adc_1gad5680a6994fc0fb9d511b99ddbaf413a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_acquire(void)
:   lock the runing ADC channel

    This API lock ADC channel which is runing.

    参数
    :   **id** – ADC id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv414bk_adc_releasev"></a>

<a id="_CPPv314bk_adc_releasev"></a> <a id="_CPPv214bk_adc_releasev"></a> <a id="bk_adc_release"></a> <a id="group__bk__api__adc_1ga64ed3c9fd2993162237fcbfd5ece8938"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_release()
:   release the runing ADC channel

    This API release ADC channel which is runing.

    参数
    :   **id** – ADC id

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_adc_driver_deinitv"></a>

<a id="_CPPv320bk_adc_driver_deinitv"></a> <a id="_CPPv220bk_adc_driver_deinitv"></a> <a id="bk_adc_driver_deinit__void"></a> <a id="group__bk__api__adc_1ga1cab56766442da4369c77b089f07ef9b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_driver\_deinit(void)
:   Deinit the ADC driver.

    This API free all resource related to ADC and power down all ADC.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_adc_init10adc_chan_t"></a>

<a id="_CPPv311bk_adc_init10adc_chan_t"></a> <a id="_CPPv211bk_adc_init10adc_chan_t"></a> <a id="bk_adc_init__adc_chan_t"></a> <a id="group__bk__api__adc_1ga99c945973b47e3eca9edc063e174cc7f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_init([adc\_chan\_t](#_CPPv410adc_chan_t "adc_chan_t") adc\_id)
:   Init the ADC.

    This API init the ADC:

    - Power up the ADC
    - Map the ADC id to dedicated GPIO port
    - Set adc work channel

    参数
    :   - **id** – ADC channel
        - **size** – ADC recieve data size

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_ADC\_NOT\_INIT: ADC driver not init
        - BK\_ERR\_ADC\_INVALID\_ID: ADC id is invalid
        - others: other errors.

<a id="_CPPv413bk_adc_deinit10adc_chan_t"></a>

<a id="_CPPv313bk_adc_deinit10adc_chan_t"></a> <a id="_CPPv213bk_adc_deinit10adc_chan_t"></a> <a id="bk_adc_deinit__adc_chan_t"></a> <a id="group__bk__api__adc_1ga23b94dc65f032ae17da87e868aec3f04"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_deinit([adc\_chan\_t](#_CPPv410adc_chan_t "adc_chan_t") id)
:   Deinit the ADC id.

    This API deinit the ADC id:

    - Stop the ADC
    - Disable the ADC id interrupt
    - Power down the ADC
    - Unmap gpio id

    **Attention**
    :   1\. This API should be called before use adc.

    参数
    :   **id** – ADC id

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_ADC\_NOT\_INIT: ADC driver not init
        - BK\_ERR\_ADC\_INVALID\_ID: ADC id is invalid
        - others: other errors.

<a id="_CPPv412bk_adc_startv"></a>

<a id="_CPPv312bk_adc_startv"></a> <a id="_CPPv212bk_adc_startv"></a> <a id="bk_adc_start__void"></a> <a id="group__bk__api__adc_1ga252d590fe1c9e9e5718c65a31f8c4559"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_start(void)
:   Start the ADC.

    This API start adc:

    - enable the ADC id interrupt

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_ADC\_BUSY: ADC is busy
        - others: other errors.

<a id="_CPPv411bk_adc_stopv"></a>

<a id="_CPPv311bk_adc_stopv"></a> <a id="_CPPv211bk_adc_stopv"></a> <a id="bk_adc_stop__void"></a> <a id="group__bk__api__adc_1gaa9fd8fac599692028959169fc54768ad"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_stop(void)
:   Stop the ADC.

    This API stop adc:

    - disable the ADC en bit

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_ADC\_BUSY: ADC is busy
        - others: other errors.

<a id="_CPPv415bk_adc_read_rawP8uint16_t8uint32_t8uint32_t"></a>

<a id="_CPPv315bk_adc_read_rawP8uint16_t8uint32_t8uint32_t"></a> <a id="_CPPv215bk_adc_read_rawP8uint16_t8uint32_t8uint32_t"></a> <a id="bk_adc_read_raw__uint16_tP.uint32_t.uint32_t"></a> <a id="group__bk__api__adc_1ga810b203a3974846f6f68e84358aa6e35"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_read\_raw(uint16\_t \*read\_buf, uint32\_t size, uint32\_t timeout)
:   Start read the raw ADC data in continuous mode.

    **Attention**
    :   1\. The read\_buf is in unit of uint16\_t, the application needs to malloc (size \* 2\) bytes for read\_buf.

    **Attention**
    :   2\. The maximum value of size is CONFIG\_ADC\_BUF\_SIZE, if the size exceeds CONFIG\_ADC\_BUF\_SIZE, the API returns BK\_ERR\_ADC\_SIZE\_TOO\_BIG.

    参数
    :   - **read\_buf** – application malloc buffer which save the current adc value
        - **size** – the size of read\_buf, the unit of size is uint16\_t
        - **timeout** – adc read semaphore timeout

    返回
    :   - BK\_ERR\_ADC\_BUSY: ADC is busy
        - BK\_ERR\_ADC\_INVALID\_MODE: ADC mode is invalid
        - BK\_ERR\_ADC\_SIZE\_TOO\_BIG: size is too big
        - others: other errors.

<a id="_CPPv418bk_adc_single_readP8uint16_t"></a>

<a id="_CPPv318bk_adc_single_readP8uint16_t"></a> <a id="_CPPv218bk_adc_single_readP8uint16_t"></a> <a id="bk_adc_single_read__uint16_tP"></a> <a id="group__bk__api__adc_1ga9431bd97e046ab34eba81c146d7fdf59"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_single\_read(uint16\_t \*data)
:   Start read the raw ADC data in single mode.

    参数
    :   **data** – ADC sample data

    返回
    :   - BK\_OK: success.

<a id="_CPPv411bk_adc_readP8uint16_t8uint32_t"></a>

<a id="_CPPv311bk_adc_readP8uint16_t8uint32_t"></a> <a id="_CPPv211bk_adc_readP8uint16_t8uint32_t"></a> <a id="bk_adc_read__uint16_tP.uint32_t"></a> <a id="group__bk__api__adc_1ga648053302fa9186907fc723c77b3f17f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_read(uint16\_t \*data, uint32\_t timeout)
:   Start read the average value of sampling data.

    - BK\_ERR\_ADC\_BUSY: ADC is busy
    - BK\_ERR\_ADC\_INVALID\_MODE: ADC mode is invalid
    - others: other errors.

    参数
    :   - **data** – store the average value of all sample values in ADC software buffers
        - **timeout** – adc read semaphore timeout

    返回

<a id="_CPPv419bk_adc_register_isr9adc_isr_t8uint32_t"></a>

<a id="_CPPv319bk_adc_register_isr9adc_isr_t8uint32_t"></a> <a id="_CPPv219bk_adc_register_isr9adc_isr_t8uint32_t"></a> <a id="bk_adc_register_isr__adc_isr_t.uint32_t"></a> <a id="group__bk__api__adc_1ga127f9b2b6913c420df064aa8f35dd679"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_register\_isr([adc\_isr\_t](#_CPPv49adc_isr_t "adc_isr_t") isr, uint32\_t param)
:   Register the adc interrupt service routine.

    参数
    :   - **isr** – ADC intterrupt callback
        - **param** – ADC sample data size which depend on user

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_ADC\_NOT\_INIT: adc not init
        - others: other errors.

<a id="_CPPv414bk_adc_set_clk13adc_src_clk_t8uint32_t"></a>

<a id="_CPPv314bk_adc_set_clk13adc_src_clk_t8uint32_t"></a> <a id="_CPPv214bk_adc_set_clk13adc_src_clk_t8uint32_t"></a> <a id="bk_adc_set_clk__adc_src_clk_t.uint32_t"></a> <a id="group__bk__api__adc_1ga6b62c0998f5a21a36e3b5d6e6a430b09"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_set\_clk([adc\_src\_clk\_t](#_CPPv413adc_src_clk_t "adc_src_clk_t") src\_clk, uint32\_t clk)
:   set ADC source clock and work frequence

    This API set adc clock source and frequence

    参数
    :   - **src\_clk** – adc source clock
        - **clk** – adc work clock :adc clk

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_ADC\_INVALID\_SCLK\_MODE: ADC source clock is invalid
        - others: other errors.

<a id="_CPPv418bk_adc_set_channel10adc_chan_t"></a>

<a id="_CPPv318bk_adc_set_channel10adc_chan_t"></a> <a id="_CPPv218bk_adc_set_channel10adc_chan_t"></a> <a id="bk_adc_set_channel__adc_chan_t"></a> <a id="group__bk__api__adc_1ga6bbf3cfb04b3864819eb8a85c325954e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_set\_channel([adc\_chan\_t](#_CPPv410adc_chan_t "adc_chan_t") adc\_id)
:   set ADC work channel

    This API set adc work channel

    参数
    :   **adc\_id** – adc channel

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_ADC\_INVALID\_ID: ADC invalid id
        - others: other errors.

<a id="_CPPv422bk_adc_set_sample_rate8uint32_t"></a>

<a id="_CPPv322bk_adc_set_sample_rate8uint32_t"></a> <a id="_CPPv222bk_adc_set_sample_rate8uint32_t"></a> <a id="bk_adc_set_sample_rate__uint32_t"></a> <a id="group__bk__api__adc_1ga8968ce1f7c61824cfdb967cddc3478f1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_set\_sample\_rate(uint32\_t sample\_rate)
:   set ADC sample rate

    This API set adc work sample rate, period \= (16 \+ sample\_rate)\*adc\_clk mcu output 16 adc\_clks every period

    参数
    :   **sample\_rate** – adc sample rate

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv417bk_adc_set_filter8uint32_t"></a>

<a id="_CPPv317bk_adc_set_filter8uint32_t"></a> <a id="_CPPv217bk_adc_set_filter8uint32_t"></a> <a id="bk_adc_set_filter__uint32_t"></a> <a id="group__bk__api__adc_1ga51e961413bd4719c4c5986dad53841ca"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_set\_filter(uint32\_t filter)
:   set ADC filter

    This API set adc filter, the value default \< 64, data output rate \= period/(filter \+ 1\)

    参数
    :   **filter** – adc filter

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_adc_set_steady_time8uint32_t"></a>

<a id="_CPPv322bk_adc_set_steady_time8uint32_t"></a> <a id="_CPPv222bk_adc_set_steady_time8uint32_t"></a> <a id="bk_adc_set_steady_time__uint32_t"></a> <a id="group__bk__api__adc_1ga313e473f2d3e33d19e6378ba095c6122"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_set\_steady\_time(uint32\_t steady\_ctrl)
:   set ADC steady time

    This API set adc filter, adc wait (steady\_ctrl \+1)\*8 adc\_clks to send valid

    参数
    :   **steady\_ctrl** – adc steady time

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_adc_set_sample_cnt8uint32_t"></a>

<a id="_CPPv321bk_adc_set_sample_cnt8uint32_t"></a> <a id="_CPPv221bk_adc_set_sample_cnt8uint32_t"></a> <a id="bk_adc_set_sample_cnt__uint32_t"></a> <a id="group__bk__api__adc_1gaa8eca5b05e2e634defd34861c3475c7f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_set\_sample\_cnt(uint32\_t cnt)
:   set ADC sample cnt

    This API sets ADC sample cnt per-interrupt, the ADC raises the interrupt when every time it samples number of cnt times. The maximum value of cnt is 32\.

    参数
    :   **cnt** – per-interrupt sample cnt

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_adc_set_saturate_mode19adc_saturate_mode_t"></a>

<a id="_CPPv324bk_adc_set_saturate_mode19adc_saturate_mode_t"></a> <a id="_CPPv224bk_adc_set_saturate_mode19adc_saturate_mode_t"></a> <a id="bk_adc_set_saturate_mode__adc_saturate_mode_t"></a> <a id="group__bk__api__adc_1ga76871725d13d595bb993ad31ecc0e855"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_set\_saturate\_mode([adc\_saturate\_mode\_t](#_CPPv419adc_saturate_mode_t "adc_saturate_mode_t") mode)
:   set adc saturate

    This API set adc saturate, auto process adc fifo data in cpu ,just get the data from reg ADC\_DATA\_16

    参数
    :   **mode** – adc saturate

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_adc_get_saturateP19adc_saturate_mode_t"></a>

<a id="_CPPv319bk_adc_get_saturateP19adc_saturate_mode_t"></a> <a id="_CPPv219bk_adc_get_saturateP19adc_saturate_mode_t"></a> <a id="bk_adc_get_saturate__adc_saturate_mode_tP"></a> <a id="group__bk__api__adc_1gad7b6ea9ea20167759fd1713ab4275dbc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_get\_saturate([adc\_saturate\_mode\_t](#_CPPv419adc_saturate_mode_t "adc_saturate_mode_t") \*mode)
:   get adc saturate

    This API get adc saturate

    返回
    :   - adc\_saturate\_mode\_t: adc saturate mode

<a id="_CPPv433bk_adc_enable_bypass_clalibrationv"></a>

<a id="_CPPv333bk_adc_enable_bypass_clalibrationv"></a> <a id="_CPPv233bk_adc_enable_bypass_clalibrationv"></a> <a id="bk_adc_enable_bypass_clalibration__void"></a> <a id="group__bk__api__adc_1ga0657e69221bb57e9c10af2b6ce929899"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_enable\_bypass\_clalibration(void)
:   enable ADC bypass calibration

    返回
    :   - BK\_OK: succeed

<a id="_CPPv434bk_adc_disable_bypass_clalibrationv"></a>

<a id="_CPPv334bk_adc_disable_bypass_clalibrationv"></a> <a id="_CPPv234bk_adc_disable_bypass_clalibrationv"></a> <a id="bk_adc_disable_bypass_clalibration__void"></a> <a id="group__bk__api__adc_1ga41d941cee2d5a3461e37baeb4f0b1272"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_disable\_bypass\_clalibration(void)
:   disable ADC bypass calibration

    返回
    :   - BK\_OK: succeed

<a id="_CPPv417bk_adc_set_configP12adc_config_t"></a>

<a id="_CPPv317bk_adc_set_configP12adc_config_t"></a> <a id="_CPPv217bk_adc_set_configP12adc_config_t"></a> <a id="bk_adc_set_config__adc_config_tP"></a> <a id="group__bk__api__adc_1ga90a99d57dfe3020a02fb9d9e96f2c6db"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_set\_config([adc\_config\_t](#_CPPv412adc_config_t "adc_config_t") \*config)
:   adc set config

    This API config adc params

    参数
    :   **config** – adc parameter settings

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM : param is null
        - BK\_ERR\_ADC\_INVALID\_MODE:adc invalid mode
        - BK\_ERR\_ADC\_INVALID\_SCLK\_MODE: ADC source clock is invalid
        - BK\_ERR\_ADC\_INVALID\_ID: ADC id is invalid
        - others: other errors.

<a id="_CPPv415bk_adc_set_mode10adc_mode_t"></a>

<a id="_CPPv315bk_adc_set_mode10adc_mode_t"></a> <a id="_CPPv215bk_adc_set_mode10adc_mode_t"></a> <a id="bk_adc_set_mode__adc_mode_t"></a> <a id="group__bk__api__adc_1ga4c279ac3f55d129745f1ecd81230f9af"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_set\_mode([adc\_mode\_t](#_CPPv410adc_mode_t "adc_mode_t") adc\_mode)
:   adc set mode

    This API config adc mode

    参数
    :   **mode** – : adc mode:

        - 0: sleep mode: adc is power down in this mode
        - 1: single step mode: adc finish sample data convesion once after enable adc and wait mcu to read sample data. The mode will turn to sleep mode after mcu read this sample date It must be enabled again when you want to sample next data.
        - 2: software control mode: adc gengerate interrupt after sample data convesion wait mcu to read sample data. adc will convert sample data after mcu reading this sample date from data register and software cleaning int flag.
        - 3: continous mode:adc wait adc\_setting time to sample data, and generate int flag after finish sample data convesion, then always repeat last sample way. This mode don’t depend on muc reading data register.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_ADC\_INVALID\_MODE:adc invalid mode
        - others: other errors.

<a id="_CPPv415bk_adc_get_modev"></a>

<a id="_CPPv315bk_adc_get_modev"></a> <a id="_CPPv215bk_adc_get_modev"></a> <a id="bk_adc_get_mode__void"></a> <a id="group__bk__api__adc_1ga66a8f42fe602d669b99c568eadfd4506"></a> [adc\_mode\_t](#_CPPv410adc_mode_t "adc_mode_t") bk\_adc\_get\_mode(void)
:   get adc mode

    This API get adc work mode

    返回
    :   - adc\_mode\_t: adc\_mode

<a id="_CPPv421bk_adc_data_calculate6UINT165UINT8"></a>

<a id="_CPPv321bk_adc_data_calculate6UINT165UINT8"></a> <a id="_CPPv221bk_adc_data_calculate6UINT165UINT8"></a> <a id="bk_adc_data_calculate__UINT16.UINT8"></a> <a id="group__bk__api__adc_1ga86c2bbaba81a7789f26fb0ff5cb94c2d"></a> UINT16 bk\_adc\_data\_calculate(UINT16 adc\_val, UINT8 adc\_chan)
:   calculate adc data

    This API get volt

    返回
    :   - UINT16: volt

<a id="_CPPv421bk_adc_chan_init_gpio10adc_chan_t"></a>

<a id="_CPPv321bk_adc_chan_init_gpio10adc_chan_t"></a> <a id="_CPPv221bk_adc_chan_init_gpio10adc_chan_t"></a> <a id="bk_adc_chan_init_gpio__adc_chan_t"></a> <a id="group__bk__api__adc_1ga63991fb445849ea642f298983ed03977"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_chan\_init\_gpio([adc\_chan\_t](#_CPPv410adc_chan_t "adc_chan_t") chan)
:   Init the ADC GPIO.

    This API init the ADC gpio:

    - Map the ADC gpio

    **Attention**
    :   1\. This API should be called before use adc.

    参数
    :   **id** – ADC id

    返回

<a id="_CPPv423bk_adc_chan_deinit_gpio10adc_chan_t"></a>

<a id="_CPPv323bk_adc_chan_deinit_gpio10adc_chan_t"></a> <a id="_CPPv223bk_adc_chan_deinit_gpio10adc_chan_t"></a> <a id="bk_adc_chan_deinit_gpio__adc_chan_t"></a> <a id="group__bk__api__adc_1ga7192617a3580239d03abd4d352e27a26"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_adc\_chan\_deinit\_gpio([adc\_chan\_t](#_CPPv410adc_chan_t "adc_chan_t") chan)
:   Deinit the ADC GPIO.

    This API Deinit the ADC gpio:

    - Unmap the ADC gpio

    **Attention**
    :   1\. This API should be called before use adc.

    参数
    :   **id** – ADC id

    返回

<a id="adc-api-typedefs"></a>

## ADC API Typedefs

<a id="id1"></a>

### Header File

- [adc\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/adc_types.h)

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_ADC_NOT_INIT"></a>

<a id="group__bk__api__adc__defs_1ga350f0dde45b4a51614db477f64b48353"></a> BK\_ERR\_ADC\_NOT\_INIT
:   ADC driver not init

<a id="c.BK_ERR_ADC_INVALID_CHAN"></a>

<a id="group__bk__api__adc__defs_1ga0c3d590294f1e20ea111ea721a0daf83"></a> BK\_ERR\_ADC\_INVALID\_CHAN
:   ADC chan number is invalid

<a id="c.BK_ERR_ADC_BUSY"></a>

<a id="group__bk__api__adc__defs_1gafef8ce1c14945a1213248b17fa61f675"></a> BK\_ERR\_ADC\_BUSY
:   ADC channel is busy

<a id="c.BK_ERR_ADC_INVALID_MODE"></a>

<a id="group__bk__api__adc__defs_1gae1993ad295e7e596d84e508581cffaa2"></a> BK\_ERR\_ADC\_INVALID\_MODE
:   ADC invalid mode

<a id="c.BK_ERR_ADC_CHAN_NOT_INIT"></a>

<a id="group__bk__api__adc__defs_1ga8dfcab3444843e3ab071edf63de2cf8b"></a> BK\_ERR\_ADC\_CHAN\_NOT\_INIT
:   ADC chan not init

<a id="c.BK_ERR_ADC_INVALID_SCLK_MODE"></a>

<a id="group__bk__api__adc__defs_1gae84ab7f2ec81ab02d23182e1e1eddca1"></a> BK\_ERR\_ADC\_INVALID\_SCLK\_MODE
:   ADC no such source clock

<a id="c.BK_ERR_ADC_INIT_MUTEX"></a>

<a id="group__bk__api__adc__defs_1gaf7ab363e33889917104dfcaf62c921bc"></a> BK\_ERR\_ADC\_INIT\_MUTEX
:   ADC mutex lock

<a id="c.BK_ERR_ADC_GET_READ_SEMA"></a>

<a id="group__bk__api__adc__defs_1ga5ffe8762f3bf5d19d649908a51de76af"></a> BK\_ERR\_ADC\_GET\_READ\_SEMA
:   ADC get semaphore error

<a id="c.BK_ERR_ADC_INIT_READ_SEMA"></a>

<a id="group__bk__api__adc__defs_1ga9abd36057cd64cba90f90a528d9bc41b"></a> BK\_ERR\_ADC\_INIT\_READ\_SEMA
:   ADC read data error

<a id="c.BK_ERR_ADC_SIZE_TOO_BIG"></a>

<a id="group__bk__api__adc__defs_1gafaaecb00e1127f8e5ef834e5d9a728d4"></a> BK\_ERR\_ADC\_SIZE\_TOO\_BIG
:   ADC read size is bigger than adc driver buffer size

<a id="c.BK_ERR_SARADC_WAIT_CB_NOT_REGISTER"></a>

<a id="group__bk__api__adc__defs_1gacd481d1447dab7704c2c7357459a932a"></a> BK\_ERR\_SARADC\_WAIT\_CB\_NOT\_REGISTER
:   ADC wait cb is not registered but tried to unregister

<a id="c.CONFIG_ADC_BUF_SIZE"></a>

<a id="group__bk__api__adc__defs_1ga274c074e9d56014405a269a629583af7"></a> CONFIG\_ADC\_BUF\_SIZE

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv49adc_isr_t"></a>

<a id="_CPPv39adc_isr_t"></a> <a id="_CPPv29adc_isr_t"></a> <a id="adc_isr_t"></a> <a id="group__bk__api__adc__defs_1ga7b069cf11944fce08d87265c9241f42d"></a> typedef void (\*adc\_isr\_t)(uint32\_t param)
:   ADC interrupt service routine.

<a id="id2"></a>

### Header File

- [hal\_adc\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_adc_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv412adc_config_t"></a>

<a id="_CPPv312adc_config_t"></a> <a id="_CPPv212adc_config_t"></a> <a id="adc_config_t"></a> <a id="structadc__config__t"></a> struct adc\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N12adc_config_t3clkE"></a>

    <a id="_CPPv3N12adc_config_t3clkE"></a> <a id="_CPPv2N12adc_config_t3clkE"></a> <a id="adc_config_t::clk__uint32_t"></a> <a id="structadc__config__t_1af0b68a20a8a2316501f80cdcc42e376d"></a> uint32\_t clk
    :   ADC sample clock division: adc\_clk\=clk/\[2\*(pre\_div \+1)\]

    <a id="_CPPv4N12adc_config_t11sample_rateE"></a>

    <a id="_CPPv3N12adc_config_t11sample_rateE"></a> <a id="_CPPv2N12adc_config_t11sample_rateE"></a> <a id="adc_config_t::sample_rate__uint32_t"></a> <a id="structadc__config__t_1abb995fe6c62563de88fbff31fb4a7222"></a> uint32\_t sample\_rate
    :   ADC sample rate, every period ouput 16 adc\_clks in continuous mode period \= (16\+samp\_rate)\*adc\_clk

    <a id="_CPPv4N12adc_config_t10adc_filterE"></a>

    <a id="_CPPv3N12adc_config_t10adc_filterE"></a> <a id="_CPPv2N12adc_config_t10adc_filterE"></a> <a id="adc_config_t::adc_filter__uint32_t"></a> <a id="structadc__config__t_1a93db228d9839ed42f03e1ccf508f8aab"></a> uint32\_t adc\_filter
    :   ADC filter: the output data rate \= period/(adc\_filter \+1)

    <a id="_CPPv4N12adc_config_t11steady_ctrlE"></a>

    <a id="_CPPv3N12adc_config_t11steady_ctrlE"></a> <a id="_CPPv2N12adc_config_t11steady_ctrlE"></a> <a id="adc_config_t::steady_ctrl__uint32_t"></a> <a id="structadc__config__t_1adff3f8a8b72393ba4245a3df336d4d68"></a> uint32\_t steady\_ctrl
    :   ADC steady\_ctrl : steady time \= (steady\_ctrl \+1)\*8 adc\_clk

    <a id="_CPPv4N12adc_config_t8adc_modeE"></a>

    <a id="_CPPv3N12adc_config_t8adc_modeE"></a> <a id="_CPPv2N12adc_config_t8adc_modeE"></a> <a id="adc_config_t::adc_mode__adc_mode_t"></a> <a id="structadc__config__t_1a05418731a8959fe4a90a5734e7badabc"></a> [adc\_mode\_t](#_CPPv410adc_mode_t "adc_mode_t") adc\_mode
    :   ADC mode set

    <a id="_CPPv4N12adc_config_t7src_clkE"></a>

    <a id="_CPPv3N12adc_config_t7src_clkE"></a> <a id="_CPPv2N12adc_config_t7src_clkE"></a> <a id="adc_config_t::src_clk__adc_src_clk_t"></a> <a id="structadc__config__t_1a5ce7fc423f75706d114b59e544e1e997"></a> [adc\_src\_clk\_t](#_CPPv413adc_src_clk_t "adc_src_clk_t") src\_clk
    :   ADC source clcok choose

    <a id="_CPPv4N12adc_config_t4chanE"></a>

    <a id="_CPPv3N12adc_config_t4chanE"></a> <a id="_CPPv2N12adc_config_t4chanE"></a> <a id="adc_config_t::chan__adc_chan_t"></a> <a id="structadc__config__t_1ace079218c300783ed088479feb849005"></a> [adc\_chan\_t](#_CPPv410adc_chan_t "adc_chan_t") chan
    :   ADC work channel

    <a id="_CPPv4N12adc_config_t13saturate_modeE"></a>

    <a id="_CPPv3N12adc_config_t13saturate_modeE"></a> <a id="_CPPv2N12adc_config_t13saturate_modeE"></a> <a id="adc_config_t::saturate_mode__adc_saturate_mode_t"></a> <a id="structadc__config__t_1a17af80ccd84d7975291d40a295c667aa"></a> [adc\_saturate\_mode\_t](#_CPPv419adc_saturate_mode_t "adc_saturate_mode_t") saturate\_mode
    :   ADC saturate\_mode

    <a id="_CPPv4N12adc_config_t7is_openE"></a>

    <a id="_CPPv3N12adc_config_t7is_openE"></a> <a id="_CPPv2N12adc_config_t7is_openE"></a> <a id="adc_config_t::is_open__uint32_t"></a> <a id="structadc__config__t_1ab6d1bb5689d757bf606d55c22ed20df5"></a> uint32\_t is\_open
    :   ADC channel is open or not

    <a id="_CPPv4N12adc_config_t10output_bufE"></a>

    <a id="_CPPv3N12adc_config_t10output_bufE"></a> <a id="_CPPv2N12adc_config_t10output_bufE"></a> <a id="adc_config_t::output_buf__uint16_tP"></a> <a id="structadc__config__t_1ac2c8808df59a2b21970da040a26504b0"></a> uint16\_t \*output\_buf
    :   ADC channel output buffer

    <a id="_CPPv4N12adc_config_t14output_buf_lenE"></a>

    <a id="_CPPv3N12adc_config_t14output_buf_lenE"></a> <a id="_CPPv2N12adc_config_t14output_buf_lenE"></a> <a id="adc_config_t::output_buf_len__int32_t"></a> <a id="structadc__config__t_1a80c54bd7fa448065048b8705f4726030"></a> int32\_t output\_buf\_len
    :   ADC channel output buffer length

    <a id="_CPPv4N12adc_config_t7vol_divE"></a>

    <a id="_CPPv3N12adc_config_t7vol_divE"></a> <a id="_CPPv2N12adc_config_t7vol_divE"></a> <a id="adc_config_t::vol_div__adc_vol_div_t"></a> <a id="structadc__config__t_1aaebfe2ffd1e28bdaa55ba55c3bd73bf0"></a> [adc\_vol\_div\_t](#_CPPv413adc_vol_div_t "adc_vol_div_t") vol\_div
    :   ADC channel attenuation coefficient

<a id="_CPPv414adc_gpio_map_t"></a>

<a id="_CPPv314adc_gpio_map_t"></a> <a id="_CPPv214adc_gpio_map_t"></a> <a id="adc_gpio_map_t"></a> <a id="structadc__gpio__map__t"></a> struct adc\_gpio\_map\_t

<a id="id3"></a>

### Macros

<a id="c.CONFIG_ADC_STATIS"></a>

<a id="hal__adc__types_8h_1a90244032a35b93d9f0575e29f202a622"></a> CONFIG\_ADC\_STATIS

<a id="c.ADC_ACURACY_10_BIT"></a>

<a id="group__bk__api__adc__defs_1ga2a88682036d2ab2c1d40c1e6ab57e7d8"></a> ADC\_ACURACY\_10\_BIT

<a id="c.ADC_ACURACY_12_BIT"></a>

<a id="group__bk__api__adc__defs_1ga02d4ff8893fa30cbdb57de3817ac93f7"></a> ADC\_ACURACY\_12\_BIT

<a id="c.ADC_READ_SEMAPHORE_WAIT_TIME"></a>

<a id="group__bk__api__adc__defs_1gaf8907bd90fcc2ff383673953fc9a615e"></a> ADC\_READ\_SEMAPHORE\_WAIT\_TIME

<a id="c.ADC_SRC_DCO_CLK"></a>

<a id="group__bk__api__adc__defs_1gaf045e0adda21dd020ca5c46fa1f78500"></a> ADC\_SRC\_DCO\_CLK

<a id="c.ADC_SRC_DPLL_CLK"></a>

<a id="group__bk__api__adc__defs_1ga738a619dbc2e8945e931dbab272ffaee"></a> ADC\_SRC\_DPLL\_CLK

<a id="c.ADC_SRC_26M_CLK"></a>

<a id="group__bk__api__adc__defs_1ga55383acb27379f77d2c4bebb6313912e"></a> ADC\_SRC\_26M\_CLK

<a id="c.ADC_SRC_32M_CLK"></a>

<a id="group__bk__api__adc__defs_1ga46fe6b556bf3f5f5d313ff5204791b92"></a> ADC\_SRC\_32M\_CLK

<a id="c.ADC_FIFO_LEVEL_MAX"></a>

<a id="group__bk__api__adc__defs_1gab4e15d68d8022fe5504e274fe43dab29"></a> ADC\_FIFO\_LEVEL\_MAX

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv413adc_src_clk_t"></a>

<a id="_CPPv313adc_src_clk_t"></a> <a id="_CPPv213adc_src_clk_t"></a> <a id="group__bk__api__adc__enum_1gac2b917bbd3309983d6399fd5f850eae2"></a> enum adc\_src\_clk\_t
:   *Values:*

    <a id="_CPPv4N13adc_src_clk_t12ADC_SCLK_DCOE"></a>

    <a id="_CPPv3N13adc_src_clk_t12ADC_SCLK_DCOE"></a> <a id="_CPPv2N13adc_src_clk_t12ADC_SCLK_DCOE"></a> <a id="group__bk__api__adc__enum_1ggac2b917bbd3309983d6399fd5f850eae2a08a9fa1307f766f2dd174befd429b49b"></a> enumerator ADC\_SCLK\_DCO
    :   ADC source clock dco

    <a id="_CPPv4N13adc_src_clk_t17ADC_SCLK_XTAL_26ME"></a>

    <a id="_CPPv3N13adc_src_clk_t17ADC_SCLK_XTAL_26ME"></a> <a id="_CPPv2N13adc_src_clk_t17ADC_SCLK_XTAL_26ME"></a> <a id="group__bk__api__adc__enum_1ggac2b917bbd3309983d6399fd5f850eae2a83d5b3d6c70e0fcfafaf1159a03e064b"></a> enumerator ADC\_SCLK\_XTAL\_26M
    :   ADC source clock xtal 26M

    <a id="_CPPv4N13adc_src_clk_t13ADC_SCLK_DPLLE"></a>

    <a id="_CPPv3N13adc_src_clk_t13ADC_SCLK_DPLLE"></a> <a id="_CPPv2N13adc_src_clk_t13ADC_SCLK_DPLLE"></a> <a id="group__bk__api__adc__enum_1ggac2b917bbd3309983d6399fd5f850eae2a4596be204b310c9feb998c1c2bf680db"></a> enumerator ADC\_SCLK\_DPLL
    :   ADC source clock dpll

    <a id="_CPPv4N13adc_src_clk_t12ADC_SCLK_32ME"></a>

    <a id="_CPPv3N13adc_src_clk_t12ADC_SCLK_32ME"></a> <a id="_CPPv2N13adc_src_clk_t12ADC_SCLK_32ME"></a> <a id="group__bk__api__adc__enum_1ggac2b917bbd3309983d6399fd5f850eae2ae50c0be0103fa72de108028913f09443"></a> enumerator ADC\_SCLK\_32M
    :   ADC source clock 32M

    <a id="_CPPv4N13adc_src_clk_t13ADC_SCLK_NONEE"></a>

    <a id="_CPPv3N13adc_src_clk_t13ADC_SCLK_NONEE"></a> <a id="_CPPv2N13adc_src_clk_t13ADC_SCLK_NONEE"></a> <a id="group__bk__api__adc__enum_1ggac2b917bbd3309983d6399fd5f850eae2ac692c76705bc66f6e8966f85ac3f7ef3"></a> enumerator ADC\_SCLK\_NONE
    :   ADC has not such source clock

<a id="_CPPv410adc_mode_t"></a>

<a id="_CPPv310adc_mode_t"></a> <a id="_CPPv210adc_mode_t"></a> <a id="group__bk__api__adc__enum_1ga760a8dafdcddcfadfea0aa3e01159164"></a> enum adc\_mode\_t
:   *Values:*

    <a id="_CPPv4N10adc_mode_t14ADC_SLEEP_MODEE"></a>

    <a id="_CPPv3N10adc_mode_t14ADC_SLEEP_MODEE"></a> <a id="_CPPv2N10adc_mode_t14ADC_SLEEP_MODEE"></a> <a id="group__bk__api__adc__enum_1gga760a8dafdcddcfadfea0aa3e01159164a35fd0f9784510f4d64ec80b1c5bdea7e"></a> enumerator ADC\_SLEEP\_MODE
    :   ADC sleep mode

    <a id="_CPPv4N10adc_mode_t20ADC_SINGLE_STEP_MODEE"></a>

    <a id="_CPPv3N10adc_mode_t20ADC_SINGLE_STEP_MODEE"></a> <a id="_CPPv2N10adc_mode_t20ADC_SINGLE_STEP_MODEE"></a> <a id="group__bk__api__adc__enum_1gga760a8dafdcddcfadfea0aa3e01159164a6f76882b6c8e57b4f690bdc0adf5ce7f"></a> enumerator ADC\_SINGLE\_STEP\_MODE
    :   ADC single step mode

    <a id="_CPPv4N10adc_mode_t24ADC_SOFTWARE_CONTRL_MODEE"></a>

    <a id="_CPPv3N10adc_mode_t24ADC_SOFTWARE_CONTRL_MODEE"></a> <a id="_CPPv2N10adc_mode_t24ADC_SOFTWARE_CONTRL_MODEE"></a> <a id="group__bk__api__adc__enum_1gga760a8dafdcddcfadfea0aa3e01159164aa8d0f586eb7153600330be62df83b13d"></a> enumerator ADC\_SOFTWARE\_CONTRL\_MODE
    :   ADC software control mode

    <a id="_CPPv4N10adc_mode_t19ADC_CONTINUOUS_MODEE"></a>

    <a id="_CPPv3N10adc_mode_t19ADC_CONTINUOUS_MODEE"></a> <a id="_CPPv2N10adc_mode_t19ADC_CONTINUOUS_MODEE"></a> <a id="group__bk__api__adc__enum_1gga760a8dafdcddcfadfea0aa3e01159164ae2a4cdf355c05733b7d576963c9100c0"></a> enumerator ADC\_CONTINUOUS\_MODE
    :   ADC continuous mode

    <a id="_CPPv4N10adc_mode_t13ADC_NONE_MODEE"></a>

    <a id="_CPPv3N10adc_mode_t13ADC_NONE_MODEE"></a> <a id="_CPPv2N10adc_mode_t13ADC_NONE_MODEE"></a> <a id="group__bk__api__adc__enum_1gga760a8dafdcddcfadfea0aa3e01159164ab7be33f484976aeae6dc7d48ee29cca2"></a> enumerator ADC\_NONE\_MODE

<a id="_CPPv410adc_chan_t"></a>

<a id="_CPPv310adc_chan_t"></a> <a id="_CPPv210adc_chan_t"></a> <a id="group__bk__api__adc__enum_1ga1e38e6e0ab10be4c51bbb48d72e3bad3"></a> enum adc\_chan\_t
:   *Values:*

    <a id="_CPPv4N10adc_chan_t5ADC_0E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_0E"></a> <a id="_CPPv2N10adc_chan_t5ADC_0E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3aa7f4d8267a3e7e544f3f867f2b429a02"></a> enumerator ADC\_0

    <a id="_CPPv4N10adc_chan_t5ADC_1E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_1E"></a> <a id="_CPPv2N10adc_chan_t5ADC_1E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3ac7f9ee52a56e7cb14a6f4ab1104436a1"></a> enumerator ADC\_1

    <a id="_CPPv4N10adc_chan_t5ADC_2E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_2E"></a> <a id="_CPPv2N10adc_chan_t5ADC_2E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3a9b15ce3dc96b90458f5c3a1c8e05f8e6"></a> enumerator ADC\_2

    <a id="_CPPv4N10adc_chan_t5ADC_3E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_3E"></a> <a id="_CPPv2N10adc_chan_t5ADC_3E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3ae2c2b7b21e22e66c73894b8b1423b332"></a> enumerator ADC\_3

    <a id="_CPPv4N10adc_chan_t5ADC_4E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_4E"></a> <a id="_CPPv2N10adc_chan_t5ADC_4E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3a02dd8ff053e7f4a2e090b55f4cab2238"></a> enumerator ADC\_4

    <a id="_CPPv4N10adc_chan_t5ADC_5E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_5E"></a> <a id="_CPPv2N10adc_chan_t5ADC_5E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3a2fff1c2f268d83011737ff7ac38370c0"></a> enumerator ADC\_5

    <a id="_CPPv4N10adc_chan_t5ADC_6E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_6E"></a> <a id="_CPPv2N10adc_chan_t5ADC_6E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3a76a5bdfd79c729ab14b6cf77498e75fc"></a> enumerator ADC\_6

    <a id="_CPPv4N10adc_chan_t5ADC_7E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_7E"></a> <a id="_CPPv2N10adc_chan_t5ADC_7E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3acde258d896f735fd042a121f9a231dbc"></a> enumerator ADC\_7

    <a id="_CPPv4N10adc_chan_t5ADC_8E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_8E"></a> <a id="_CPPv2N10adc_chan_t5ADC_8E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3aab7fe862b2625e2af4c67441f0eeeddc"></a> enumerator ADC\_8

    <a id="_CPPv4N10adc_chan_t5ADC_9E"></a>

    <a id="_CPPv3N10adc_chan_t5ADC_9E"></a> <a id="_CPPv2N10adc_chan_t5ADC_9E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3ab940d890c3734d5474baf92af3c7f0df"></a> enumerator ADC\_9

    <a id="_CPPv4N10adc_chan_t6ADC_10E"></a>

    <a id="_CPPv3N10adc_chan_t6ADC_10E"></a> <a id="_CPPv2N10adc_chan_t6ADC_10E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3aa9f719a27f29b98faff5c817fd0c7a39"></a> enumerator ADC\_10

    <a id="_CPPv4N10adc_chan_t6ADC_11E"></a>

    <a id="_CPPv3N10adc_chan_t6ADC_11E"></a> <a id="_CPPv2N10adc_chan_t6ADC_11E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3ab80bf877dae1b8e84879661e850df113"></a> enumerator ADC\_11

    <a id="_CPPv4N10adc_chan_t6ADC_12E"></a>

    <a id="_CPPv3N10adc_chan_t6ADC_12E"></a> <a id="_CPPv2N10adc_chan_t6ADC_12E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3ae39fdb757f98ce6b4ae835d8c413be88"></a> enumerator ADC\_12

    <a id="_CPPv4N10adc_chan_t6ADC_13E"></a>

    <a id="_CPPv3N10adc_chan_t6ADC_13E"></a> <a id="_CPPv2N10adc_chan_t6ADC_13E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3a0992532ff2d28601e0c5354a56bef0ba"></a> enumerator ADC\_13

    <a id="_CPPv4N10adc_chan_t6ADC_14E"></a>

    <a id="_CPPv3N10adc_chan_t6ADC_14E"></a> <a id="_CPPv2N10adc_chan_t6ADC_14E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3a4efa10b29ab50fb090cfe7e0bdc64ad8"></a> enumerator ADC\_14

    <a id="_CPPv4N10adc_chan_t6ADC_15E"></a>

    <a id="_CPPv3N10adc_chan_t6ADC_15E"></a> <a id="_CPPv2N10adc_chan_t6ADC_15E"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3ae693320a2c0da1bd5985106496789025"></a> enumerator ADC\_15

    <a id="_CPPv4N10adc_chan_t7ADC_MAXE"></a>

    <a id="_CPPv3N10adc_chan_t7ADC_MAXE"></a> <a id="_CPPv2N10adc_chan_t7ADC_MAXE"></a> <a id="group__bk__api__adc__enum_1gga1e38e6e0ab10be4c51bbb48d72e3bad3a2caf3ec827224fca2fe75224519064e5"></a> enumerator ADC\_MAX

<a id="_CPPv419adc_saturate_mode_t"></a>

<a id="_CPPv319adc_saturate_mode_t"></a> <a id="_CPPv219adc_saturate_mode_t"></a> <a id="group__bk__api__adc__enum_1gad205831ed2346df0491bfc6009ee2651"></a> enum adc\_saturate\_mode\_t
:   *Values:*

    <a id="_CPPv4N19adc_saturate_mode_t22ADC_SATURATE_MODE_NONEE"></a>

    <a id="_CPPv3N19adc_saturate_mode_t22ADC_SATURATE_MODE_NONEE"></a> <a id="_CPPv2N19adc_saturate_mode_t22ADC_SATURATE_MODE_NONEE"></a> <a id="group__bk__api__adc__enum_1ggad205831ed2346df0491bfc6009ee2651add8b6d28e77036ad8454fe8b5bc20e06"></a> enumerator ADC\_SATURATE\_MODE\_NONE

    <a id="_CPPv4N19adc_saturate_mode_t19ADC_SATURATE_MODE_0E"></a>

    <a id="_CPPv3N19adc_saturate_mode_t19ADC_SATURATE_MODE_0E"></a> <a id="_CPPv2N19adc_saturate_mode_t19ADC_SATURATE_MODE_0E"></a> <a id="group__bk__api__adc__enum_1ggad205831ed2346df0491bfc6009ee2651aa1fc454bd7eb921d49f98c995f8a523b"></a> enumerator ADC\_SATURATE\_MODE\_0

    <a id="_CPPv4N19adc_saturate_mode_t19ADC_SATURATE_MODE_1E"></a>

    <a id="_CPPv3N19adc_saturate_mode_t19ADC_SATURATE_MODE_1E"></a> <a id="_CPPv2N19adc_saturate_mode_t19ADC_SATURATE_MODE_1E"></a> <a id="group__bk__api__adc__enum_1ggad205831ed2346df0491bfc6009ee2651a0a3e2c3550159f3ecde78612a7eab90c"></a> enumerator ADC\_SATURATE\_MODE\_1

    <a id="_CPPv4N19adc_saturate_mode_t19ADC_SATURATE_MODE_2E"></a>

    <a id="_CPPv3N19adc_saturate_mode_t19ADC_SATURATE_MODE_2E"></a> <a id="_CPPv2N19adc_saturate_mode_t19ADC_SATURATE_MODE_2E"></a> <a id="group__bk__api__adc__enum_1ggad205831ed2346df0491bfc6009ee2651a23cc86e130111f25dc1779f3d8eeec55"></a> enumerator ADC\_SATURATE\_MODE\_2

    <a id="_CPPv4N19adc_saturate_mode_t19ADC_SATURATE_MODE_3E"></a>

    <a id="_CPPv3N19adc_saturate_mode_t19ADC_SATURATE_MODE_3E"></a> <a id="_CPPv2N19adc_saturate_mode_t19ADC_SATURATE_MODE_3E"></a> <a id="group__bk__api__adc__enum_1ggad205831ed2346df0491bfc6009ee2651a0f1e407de174704dd50b0e29f4ecedd6"></a> enumerator ADC\_SATURATE\_MODE\_3

<a id="_CPPv413adc_vol_div_t"></a>

<a id="_CPPv313adc_vol_div_t"></a> <a id="_CPPv213adc_vol_div_t"></a> <a id="group__bk__api__adc__enum_1ga5d00f85a3f7ce4e651b531cca9fabc7c"></a> enum adc\_vol\_div\_t
:   *Values:*

    <a id="_CPPv4N13adc_vol_div_t16ADC_VOL_DIV_NONEE"></a>

    <a id="_CPPv3N13adc_vol_div_t16ADC_VOL_DIV_NONEE"></a> <a id="_CPPv2N13adc_vol_div_t16ADC_VOL_DIV_NONEE"></a> <a id="group__bk__api__adc__enum_1gga5d00f85a3f7ce4e651b531cca9fabc7cad92a9fc05d99be97174d0346206849fc"></a> enumerator ADC\_VOL\_DIV\_NONE

    <a id="_CPPv4N13adc_vol_div_t13ADC_VOL_DIV_1E"></a>

    <a id="_CPPv3N13adc_vol_div_t13ADC_VOL_DIV_1E"></a> <a id="_CPPv2N13adc_vol_div_t13ADC_VOL_DIV_1E"></a> <a id="group__bk__api__adc__enum_1gga5d00f85a3f7ce4e651b531cca9fabc7ca5f1220c515e2ac318079984fc6e3d800"></a> enumerator ADC\_VOL\_DIV\_1

    <a id="_CPPv4N13adc_vol_div_t13ADC_VOL_DIV_2E"></a>

    <a id="_CPPv3N13adc_vol_div_t13ADC_VOL_DIV_2E"></a> <a id="_CPPv2N13adc_vol_div_t13ADC_VOL_DIV_2E"></a> <a id="group__bk__api__adc__enum_1gga5d00f85a3f7ce4e651b531cca9fabc7cae12b9754f0adaf2e3a45dd95b6a5babe"></a> enumerator ADC\_VOL\_DIV\_2

    <a id="_CPPv4N13adc_vol_div_t13ADC_VOL_DIV_3E"></a>

    <a id="_CPPv3N13adc_vol_div_t13ADC_VOL_DIV_3E"></a> <a id="_CPPv2N13adc_vol_div_t13ADC_VOL_DIV_3E"></a> <a id="group__bk__api__adc__enum_1gga5d00f85a3f7ce4e651b531cca9fabc7ca8ea6d2f2bad39efd492b1df1b3b82b63"></a> enumerator ADC\_VOL\_DIV\_3

    <a id="_CPPv4N13adc_vol_div_t13ADC_VOL_DIV_4E"></a>

    <a id="_CPPv3N13adc_vol_div_t13ADC_VOL_DIV_4E"></a> <a id="_CPPv2N13adc_vol_div_t13ADC_VOL_DIV_4E"></a> <a id="group__bk__api__adc__enum_1gga5d00f85a3f7ce4e651b531cca9fabc7ca916d6aa00046213665f61fa0eaa67f7c"></a> enumerator ADC\_VOL\_DIV\_4

    <a id="_CPPv4N13adc_vol_div_t13ADC_VOL_DIV_5E"></a>

    <a id="_CPPv3N13adc_vol_div_t13ADC_VOL_DIV_5E"></a> <a id="_CPPv2N13adc_vol_div_t13ADC_VOL_DIV_5E"></a> <a id="group__bk__api__adc__enum_1gga5d00f85a3f7ce4e651b531cca9fabc7ca46f5d4c89d120343307f7e887f9b0f18"></a> enumerator ADC\_VOL\_DIV\_5

    <a id="_CPPv4N13adc_vol_div_t13ADC_VOL_DIV_7E"></a>

    <a id="_CPPv3N13adc_vol_div_t13ADC_VOL_DIV_7E"></a> <a id="_CPPv2N13adc_vol_div_t13ADC_VOL_DIV_7E"></a> <a id="group__bk__api__adc__enum_1gga5d00f85a3f7ce4e651b531cca9fabc7ca8e2208ef72019a2f9bf8441ddd43cd9e"></a> enumerator ADC\_VOL\_DIV\_7
