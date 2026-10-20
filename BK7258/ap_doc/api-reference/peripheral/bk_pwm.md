---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/api-reference/peripheral/bk_pwm.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="pwm"></a>

# PWM

<a id="pwm-api-status"></a>

## PWM API Status

| API | BK7258\_AP |
| --- | --- |
| [`bk_pwm_driver_init()`](#_CPPv418bk_pwm_driver_initv "bk_pwm_driver_init") | Y |
| [`bk_pwm_driver_deinit()`](#_CPPv420bk_pwm_driver_deinitv "bk_pwm_driver_deinit") | Y |
| [`bk_pwm_init()`](#_CPPv411bk_pwm_init10pwm_chan_tPK17pwm_init_config_t "bk_pwm_init") | Y |
| [`bk_pwm_deinit()`](#_CPPv413bk_pwm_deinit10pwm_chan_t "bk_pwm_deinit") | Y |
| [`bk_pwm_set_period_duty()`](#_CPPv422bk_pwm_set_period_duty10pwm_chan_tP24pwm_period_duty_config_t "bk_pwm_set_period_duty") | Y |
| [`bk_pwm_start()`](#_CPPv412bk_pwm_start10pwm_chan_t "bk_pwm_start") | Y |
| [`bk_pwm_stop()`](#_CPPv411bk_pwm_stop10pwm_chan_t "bk_pwm_stop") | Y |
| [`bk_pwm_set_init_signal_low()`](#_CPPv426bk_pwm_set_init_signal_low10pwm_chan_t "bk_pwm_set_init_signal_low") | N |
| [`bk_pwm_set_init_signal_high()`](#_CPPv427bk_pwm_set_init_signal_high10pwm_chan_t "bk_pwm_set_init_signal_high") | N |
| [`bk_pwm_register_isr()`](#_CPPv419bk_pwm_register_isr10pwm_chan_t9pwm_isr_t "bk_pwm_register_isr") | Y |
| [`bk_pwm_enable_interrupt()`](#_CPPv423bk_pwm_enable_interrupt10pwm_chan_t "bk_pwm_enable_interrupt") | Y |
| [`bk_pwm_disable_interrupt()`](#_CPPv424bk_pwm_disable_interrupt10pwm_chan_t "bk_pwm_disable_interrupt") | N |
| [`bk_pwm_group_init()`](#_CPPv417bk_pwm_group_initPK23pwm_group_init_config_tP11pwm_group_t "bk_pwm_group_init") | Y |
| [`bk_pwm_group_deinit()`](#_CPPv419bk_pwm_group_deinit11pwm_group_t "bk_pwm_group_deinit") | Y |
| [`bk_pwm_group_start()`](#_CPPv418bk_pwm_group_start11pwm_group_t "bk_pwm_group_start") | Y |
| [`bk_pwm_group_stop()`](#_CPPv417bk_pwm_group_stop11pwm_group_t "bk_pwm_group_stop") | Y |
| [`bk_pwm_capture_init()`](#_CPPv419bk_pwm_capture_init10pwm_chan_tPK25pwm_capture_init_config_t "bk_pwm_capture_init") | Y |
| [`bk_pwm_capture_deinit()`](#_CPPv421bk_pwm_capture_deinit10pwm_chan_t "bk_pwm_capture_deinit") | N |
| [`bk_pwm_capture_start()`](#_CPPv420bk_pwm_capture_start10pwm_chan_t "bk_pwm_capture_start") | Y |
| [`bk_pwm_capture_stop()`](#_CPPv419bk_pwm_capture_stop10pwm_chan_t "bk_pwm_capture_stop") | Y |
| [`bk_pwm_capture_get_value()`](#_CPPv424bk_pwm_capture_get_value10pwm_chan_t "bk_pwm_capture_get_value") | N |

<a id="pwm-channel-number"></a>

## PWM Channel Number

| Capability | BK7258 |
| --- | --- |
| Channel Number | 12 |

<a id="pwm-group-support"></a>

## PWM Group Support

| Capability | BK7258 |
| --- | --- |
| Software Group | Y |
| Hardware Group | Y |

<a id="pwm-duty-support"></a>

## PWM Duty Support

| Capability | BK7258 |
| --- | --- |
| period\_cycle | Y |
| duty\_cycle | Y |

For unsupported duty fileds, we should set them to 0\.

<a id="pwm-capture-edge-support-status"></a>

## PWM Capture Edge Support Status

| Capability | BK7258 |
| --- | --- |
| PWM\_CAPTURE\_POS | Y |
| PWM\_CAPTURE\_NEG | Y |
| PWM\_CAPTURE\_EDGE | Y |

<a id="pwm-channel-and-gpio-map"></a>

## PWM Channel and GPIO Map

| Channel Number | BK7258 |
| --- | --- |
| 0 | 6/18 |
| 1 | 7/19 |
| 2 | 8/22 |
| 3 | 9/23 |
| 4 | 24 |
| 5 | 25 |
| 6 | 32 |
| 7 | 33 |
| 8 | 34 |
| 9 | 35 |
| 10 | 36 |
| 11 | 37 |

If the channel has more than one GPIO to map. Please refer to the \<gpio\_map.h\> file for the default GPIO port \<GPIO\_PWM\_MAP\_TABLE\>.

<a id="pwm-api-reference"></a>

## PWM API Reference

<a id="header-file"></a>

### Header File

- [pwm.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/pwm.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_pwm_driver_initv"></a>

<a id="_CPPv318bk_pwm_driver_initv"></a> <a id="_CPPv218bk_pwm_driver_initv"></a> <a id="bk_pwm_driver_init__void"></a> <a id="group__bk__api__pwm_1gadb3ef9a0e49ce3d96b68298f66803993"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_driver\_init(void)
:   Init the PWM driver.

    This API init the resoure common to all PWM channels:

    - Init PWM driver control memory
    - Configure PWM common clock to 26M

    This API should be called before any other PWM APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_pwm_driver_deinitv"></a>

<a id="_CPPv320bk_pwm_driver_deinitv"></a> <a id="_CPPv220bk_pwm_driver_deinitv"></a> <a id="bk_pwm_driver_deinit__void"></a> <a id="group__bk__api__pwm_1ga06b5d6366210b50610c2f6d30e208d71"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_driver\_deinit(void)
:   Deinit the PWM driver.

    This API free all resource related to PWM and power down all PWM channels.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_pwm_init10pwm_chan_tPK17pwm_init_config_t"></a>

<a id="_CPPv311bk_pwm_init10pwm_chan_tPK17pwm_init_config_t"></a> <a id="_CPPv211bk_pwm_init10pwm_chan_tPK17pwm_init_config_t"></a> <a id="bk_pwm_init__pwm_chan_t.pwm_init_config_tCP"></a> <a id="group__bk__api__pwm_1ga914e2099ce92d433b1a6c76ade4d0f5a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_init([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, const [pwm\_init\_config\_t](#_CPPv417pwm_init_config_t "pwm_init_config_t") \*config)
:   Init the PWM channel.

    This API init the PWM channel:

    - Power up the PWM channel
    - Configure the PWM channel clock to 26M
    - Map the PWM channel to dedicated GPIO port
    - Set the period and duty cycle.

    For duty/cycle relationship, refer to [bk\_pwm\_set\_period\_duty()](#group__bk__api__pwm_1ga45326f56e267f9deb61f8b45c459b44a)

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_NOT\_INIT: PWM driver not init
        - BK\_ERR\_NULL\_PARAM: config is NULL
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - BK\_ERR\_PWM\_PERIOD\_DUTY: PWM duty/period relationship is invalid
        - others: other errors.

<a id="_CPPv413bk_pwm_deinit10pwm_chan_t"></a>

<a id="_CPPv313bk_pwm_deinit10pwm_chan_t"></a> <a id="_CPPv213bk_pwm_deinit10pwm_chan_t"></a> <a id="bk_pwm_deinit__pwm_chan_t"></a> <a id="group__bk__api__pwm_1ga2becd6367591a52bb4938b9297a116ef"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_deinit([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Deinit a PWM channel.

    This API deinit the PWM channel:

    - Stop the PWM channel
    - Reset all configuration of PWM channel to default value
    - Power down the PWM channel

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv412bk_pwm_start10pwm_chan_t"></a>

<a id="_CPPv312bk_pwm_start10pwm_chan_t"></a> <a id="_CPPv212bk_pwm_start10pwm_chan_t"></a> <a id="bk_pwm_start__pwm_chan_t"></a> <a id="group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_start([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Stop a PWM channel.

    This API init the resoure common to all PWM channels:

    - Init PWM driver control memory
    - Configure PWM common clock to 26M

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_pwm_stop10pwm_chan_t"></a>

<a id="_CPPv311bk_pwm_stop10pwm_chan_t"></a> <a id="_CPPv211bk_pwm_stop10pwm_chan_t"></a> <a id="bk_pwm_stop__pwm_chan_t"></a> <a id="group__bk__api__pwm_1gad88155b2ed4b16afc638696ee389c995"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_stop([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Stop a PWM channel.

    This API init the resoure common to all PWM channels:

    - Init PWM driver control memory
    - Configure PWM common clock to 26M

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv422bk_pwm_set_period_duty10pwm_chan_tP24pwm_period_duty_config_t"></a>

<a id="_CPPv322bk_pwm_set_period_duty10pwm_chan_tP24pwm_period_duty_config_t"></a> <a id="_CPPv222bk_pwm_set_period_duty10pwm_chan_tP24pwm_period_duty_config_t"></a> <a id="bk_pwm_set_period_duty__pwm_chan_t.pwm_period_duty_config_tP"></a> <a id="group__bk__api__pwm_1ga45326f56e267f9deb61f8b45c459b44a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_set\_period\_duty([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, [pwm\_period\_duty\_config\_t](#_CPPv424pwm_period_duty_config_t "pwm_period_duty_config_t") \*config)
:   Configure the PWM period and duty cycle.

    This API is used to configure the period and duty time. The unit is cycle of PWM channel clock, since the PWM channel clock is default to 26M, the unit is 1/26M (1/26 000 000\) seconds.

    The beken chip supports up to 3 duties, the exact duty numbers depends on the target type.

    EXample1 \- the simplest case::

    ```
    Clock cycle = 1/26M
    Initial signal is High
    duty_cycle = D1 = 3
    duty2_cycle = 0
    duty3_cycle = 0
    period_cycle = 3 + 2 = 5

                      |<-C->|
                       __    __    __    __    __    __    __    __    __    __    __    __
    Clock Signal:   __|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__
                      __________________             _________________             ___________
    PWM Signal:    __|                  |___________|                 |___________|

    Duty1:           |<------- D1 ----->|

    Period:          |<---------- Period1 --------->|<------ Period2 ------------>|
    ```

    Example2 \- 3 duty with initial signal high::

    ```
    Clock cycle = 1/26M
    Duty_cycle = D1 = 1
    Duty2_cycle = D2 = 2
    Duty3_cycle = D3 = 3
    period_cycle = D1 + D2 + D3 = 6

                      |<-C->|
                       __    __    __    __    __    __    __    __    __    __    __    __    __
    Clock Signal:   __|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|
                      ______             _________________ _____             _________________
    PWM Signal:    __|      |___________|                 |     |___________|                 |__

    Duty1:           |<-D1->|<----D2--->|<------D3------->|

    Period:          |<--------------- Period1 ---------->|<------------ Period2 ------------>|
    ```

    Example3 \- 3 duty with initial signal low::

    ```
    Clock cycle = 1/26M
    Duty_cycle = D1 = 1
    Duty2_cycle = D2 = 2
    Duty3_cycle = D3 = 3
    period_cycle = D1 + D2 + D3 = 6

                      |<-C->|
                       __    __    __    __    __    __    __    __    __    __    __    __    __
    Clock Signal:   __|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|
                    __       ___________                         ___________
    PWM Signal:       |_____|           |_________________|_____|           |_________________|__

    Duty1:           |<-D1->|<----D2--->|<------D3------->|

    Period:          |<--------------- Period1 ---------->|<------------ Period2 -------------|
    ```

    Example4 \- 3 duty with initial signal low and period \> (D1 \+ D2 \+ D3)::

    ```
    Clock cycle = 1/26M
    Duty_cycle = D1 = 1
    Duty2_cycle = D2 = 2
    Duty3_cycle = D3 = 3
    period_cycle = D1 + D2 + D3 + 1 = 7

                      |<-C->|
                       __    __    __    __    __    __    __    __    __    __    __    __    __
    Clock Signal:   __|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|  |__|
                    __       ___________                   _____       ___________
    PWM Signal:       |_____|           |_________________|     |_____|           |______________

    Duty1:           |<-D1->|<----D2--->|<------D3------->|

    Period:          |<--------------- Period ----------------->|
    ```

    **Attention**
    :   1\. The period should great or equal to (D1 \+ D2 \+ D3)

    **Attention**
    :   2\. If the duty Dx is 0, then Dx\+1 to D3 should also be 0\. If D1 is 0, it indicates the duty ratio is 0% and the signal is always low.

    **Attention**
    :   3\. If D1 equals period, it indicates the duty ratio is 100% and the signal is always high.

    **Attention**
    :   4\. The signal strengh between two successive duties is opposite, e.g. if signal of D1 is high, then signal of D2 is low.

    **Attention**
    :   5\. The initial signal is the signal strengh of D1 if D1 is not 0\.

    **Attention**
    :   6\. The duty/period configuration is very flexible, different configurations may have same result.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: config is NULL
        - BK\_ERR\_PWM\_CHAN\_NOT\_INIT: PWM channel not init
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - BK\_ERR\_PWM\_PERIOD\_DUTY: PWM duty/period relationship is invalid
        - others: other errors.

<a id="_CPPv426bk_pwm_set_init_signal_low10pwm_chan_t"></a>

<a id="_CPPv326bk_pwm_set_init_signal_low10pwm_chan_t"></a> <a id="_CPPv226bk_pwm_set_init_signal_low10pwm_chan_t"></a> <a id="bk_pwm_set_init_signal_low__pwm_chan_t"></a> <a id="group__bk__api__pwm_1ga6210cfbd8239cde480100268d3d6eb2d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_set\_init\_signal\_low([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Set the initial signal to low.

    Set the initial signal level of the first duty which is indicated by duty\_cycle.

    **Attention**
    :   The signal will always be high if the duty\_cycle equals period cycle (duty ratio is 100%), regardless whether this API is called or NOT.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_CHAN\_NOT\_INIT: PWM channel not init
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - others: other errors.

<a id="_CPPv427bk_pwm_set_init_signal_high10pwm_chan_t"></a>

<a id="_CPPv327bk_pwm_set_init_signal_high10pwm_chan_t"></a> <a id="_CPPv227bk_pwm_set_init_signal_high10pwm_chan_t"></a> <a id="bk_pwm_set_init_signal_high__pwm_chan_t"></a> <a id="group__bk__api__pwm_1gac1e4ba10c716f1d8bd68cf45bf14170b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_set\_init\_signal\_high([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Set the initial signal to high.

    Set the initial signal level of the first duty which is indicated by duty\_cycle.

    **Attention**
    :   The signal will always be low if the duty\_cycle is 0 (duty ratio is 0%), regardless whether this API is called or NOT.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_CHAN\_NOT\_INIT: PWM channel not init
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - others: other errors.

<a id="_CPPv419bk_pwm_register_isr10pwm_chan_t9pwm_isr_t"></a>

<a id="_CPPv319bk_pwm_register_isr10pwm_chan_t9pwm_isr_t"></a> <a id="_CPPv219bk_pwm_register_isr10pwm_chan_t9pwm_isr_t"></a> <a id="bk_pwm_register_isr__pwm_chan_t.pwm_isr_t"></a> <a id="group__bk__api__pwm_1gad668632575533971376f69f2babbf5c2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_register\_isr([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, [pwm\_isr\_t](#_CPPv49pwm_isr_t "pwm_isr_t") isr)
:   Register the interrupt service routine for PWM channel.

    **Attention**
    :   1\. Both [bk\_pwm\_capture\_init()](#group__bk__api__pwm_1gab70684dbb531cabcd790bcf5cfe6d074) and this API can set the ISR, the one called later makes sense.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_NOT\_INIT: PWM driver not init
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - others: other errors.

<a id="_CPPv423bk_pwm_enable_interrupt10pwm_chan_t"></a>

<a id="_CPPv323bk_pwm_enable_interrupt10pwm_chan_t"></a> <a id="_CPPv223bk_pwm_enable_interrupt10pwm_chan_t"></a> <a id="bk_pwm_enable_interrupt__pwm_chan_t"></a> <a id="group__bk__api__pwm_1ga2b5f618eada64568c0855e6236e91a40"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_enable\_interrupt([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Enable interrupt of PWM channel.

    The PWM channel interrupt is disabled by default when starting the channel by [bk\_pwm\_start()](#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919) or [bk\_pwm\_group\_start()](#group__bk__api__pwm_1gaf87327843711c56cab915f02b42a602a), while it’s enabled by default when starting the channel by [bk\_pwm\_capture\_start()](#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a).

    This API is designed mainly for debug purpose, we can use it to enable the interrupt of any PWM channel, regardless of whether the channel is started by [bk\_pwm\_start()](#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919) or [bk\_pwm\_group\_start()](#group__bk__api__pwm_1gaf87327843711c56cab915f02b42a602a) or [bk\_pwm\_capture\_start()](#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a).

    The [bk\_pwm\_stop()](#group__bk__api__pwm_1gad88155b2ed4b16afc638696ee389c995) and [bk\_pwm\_group\_stop()](#group__bk__api__pwm_1gae78db60193a534fa44665e4397c4d3c9) also disable the interrupt, but the [bk\_pwm\_start()](#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919) and bk\_pwm\_group\_start will not enable the interrupt. So if the channel interrupt is enabled, and then stop and start the channel, we need to call this API to re-enable the interrupt.

    **Attention**
    :   1\. The interrupt can be enabled only after PWM channel is started by [bk\_pwm\_start()](#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919).

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_NOT\_INIT: PWM driver not init
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - BK\_ERR\_PWM\_CHAN\_NOT\_START: PWM channel is not started
        - others: other errors.

<a id="_CPPv424bk_pwm_disable_interrupt10pwm_chan_t"></a>

<a id="_CPPv324bk_pwm_disable_interrupt10pwm_chan_t"></a> <a id="_CPPv224bk_pwm_disable_interrupt10pwm_chan_t"></a> <a id="bk_pwm_disable_interrupt__pwm_chan_t"></a> <a id="group__bk__api__pwm_1gab330fccd473ffc2b1431e06c6179127e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_disable\_interrupt([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Disable interrupt of PWM channel.

    Stop the interrupt of any PWM channel, regardless whether the channel is in PWM mode, or PWM capture mode, or PWM group mode.

    **Attention**
    :   1\. [bk\_pwm\_capture\_start()](#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a) will enable the interrupt anyway, so if we want to disable the interrupt of PWM capture channel, we need to call this API anytime [bk\_pwm\_capture\_start()](#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a) is called.

    参数
    :   **chan** – the channel ID

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_NOT\_INIT: PWM driver not init
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - others: other errors.

<a id="_CPPv417bk_pwm_group_initPK23pwm_group_init_config_tP11pwm_group_t"></a>

<a id="_CPPv317bk_pwm_group_initPK23pwm_group_init_config_tP11pwm_group_t"></a> <a id="_CPPv217bk_pwm_group_initPK23pwm_group_init_config_tP11pwm_group_t"></a> <a id="bk_pwm_group_init__pwm_group_init_config_tCP.pwm_group_tP"></a> <a id="group__bk__api__pwm_1gab3f68971d07e8e7f589b57f1eda510e7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_group\_init(const [pwm\_group\_init\_config\_t](#_CPPv423pwm_group_init_config_t "pwm_group_init_config_t") \*config, [pwm\_group\_t](#_CPPv411pwm_group_t "pwm_group_t") \*group)
:   Init the PWM group.

    This API init the PWM group. The PWM group is a channel pair that has following attributes:

    - The period is same
    - The initial signal level is opposite
    - Start and stop at the same time

    Below is a picture to demonstrate the relationship between duty and period::

    ```
                 |<------------------------ period_cycle ---------------------------->|
                 |<--chan1_duty_cycle -->|<- D1 --|<--- chan2_duty_cycle --->|<- D2 ->|
                  _______________________
     channe1 1   |                       |____________________________________________|
                                                   __________________________
     channel 2   |________________________________|                          |________|
    ```

    The D1/D2 indicates the dead time cycle, it’s calculated based on following formula: D1 \= D2 \= (period \- chan1\_duty\_cycle \- chan2\_duty\_cycle)/2

    **Attention**
    :   1\. This API doesn’t check whether the PWM channel is already used in other mode. e.g. If the API doesn’t returns error if config-\>chan1 is already used in capture mode, the application need to make sure the channel configured in the group is not used for other purpose.

    **Attention**
    :   2\. The chan2\_duty\_cycle is actually the 2nd signal wave for channel 2, as depicted in above picture.

    **Attention**
    :   3\. This API supports to group any two available channel into a PWM group, however, we recommend to group 0/1, 2/3, 4/5 into a group, because hardware can support these group directly and we can start the channels in the group at exactly same time.

    **Attention**
    :   4\. The chan1\_duty\_cycle and chan2\_duty\_cycle should be great than 0\.

    参数
    :   - **config** – configuration of PWM group
        - **group** – store the group ID if the API is succeed.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_NOT\_INIT: PWM driver not init
        - BK\_ERR\_NULL\_PARAM: config or group is NULL
        - BK\_ERR\_PWM\_CHAN\_ID: channel 1 or 2 in the group is invalid
        - BK\_ERR\_PWM\_GROUP\_SAME\_CHAN: channel 1 and 2 are same
        - BK\_ERR\_PWM\_GROUP\_EXIST: a group with channel 1 and 2 is already exists
        - BK\_ERR\_PWM\_GROUP\_CHAN\_USED: a existing group has a channel equals to channel 1 or 2
        - BK\_ERR\_PWM\_GROUP\_DUTY: period cycle \< (chan1\_duty\_cycle \+ chan2\_duty\_cycle)
        - BK\_ERR\_PWM\_PERIOD\_DUTY: PWM duty/period relationship is invalid
        - others: other errors.

<a id="_CPPv419bk_pwm_group_deinit11pwm_group_t"></a>

<a id="_CPPv319bk_pwm_group_deinit11pwm_group_t"></a> <a id="_CPPv219bk_pwm_group_deinit11pwm_group_t"></a> <a id="bk_pwm_group_deinit__pwm_group_t"></a> <a id="group__bk__api__pwm_1gaa774c10fdd0ae71899c60f91e71f6b54"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_group\_deinit([pwm\_group\_t](#_CPPv411pwm_group_t "pwm_group_t") group)
:   Deinit a PWM group.

    This API stops and powers down channels in a PWM group.

    **Attention**
    :   This API returns BK\_OK directly if the group doesn’t exist.

    参数
    :   **group** – the group ID returned bk [bk\_pwm\_group\_init()](#group__bk__api__pwm_1gab3f68971d07e8e7f589b57f1eda510e7)

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_pwm_group_set_config11pwm_group_tPK18pwm_group_config_t"></a>

<a id="_CPPv323bk_pwm_group_set_config11pwm_group_tPK18pwm_group_config_t"></a> <a id="_CPPv223bk_pwm_group_set_config11pwm_group_tPK18pwm_group_config_t"></a> <a id="bk_pwm_group_set_config__pwm_group_t.pwm_group_config_tCP"></a> <a id="group__bk__api__pwm_1ga19fda5d66250886025881f6dd020c94c"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_group\_set\_config([pwm\_group\_t](#_CPPv411pwm_group_t "pwm_group_t") group, const [pwm\_group\_config\_t](#_CPPv418pwm_group_config_t "pwm_group_config_t") \*config)
:   Configure the PWM group.

    Configure the duty and period of a PWM group, for duty/period relationship refer to [bk\_pwm\_group\_init()](#group__bk__api__pwm_1gab3f68971d07e8e7f589b57f1eda510e7).

    **Attention**
    :   The configuration can’t take effect until the current period is ended

    参数
    :   - **group** – the group ID to be configured
        - **config** – configuration of PWM group

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_NULL\_PARAM: config or group is NULL
        - BK\_ERR\_PWM\_GROUP\_NOT\_EXIST: the group doesn’t exist
        - BK\_ERR\_PWM\_GROUP\_DUTY: period cycle \< (chan1\_duty\_cycle \+ chan2\_duty\_cycle)
        - BK\_ERR\_PWM\_PERIOD\_DUTY: PWM duty/period relationship is invalid
        - others: other errors.

<a id="_CPPv418bk_pwm_group_start11pwm_group_t"></a>

<a id="_CPPv318bk_pwm_group_start11pwm_group_t"></a> <a id="_CPPv218bk_pwm_group_start11pwm_group_t"></a> <a id="bk_pwm_group_start__pwm_group_t"></a> <a id="group__bk__api__pwm_1gaf87327843711c56cab915f02b42a602a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_group\_start([pwm\_group\_t](#_CPPv411pwm_group_t "pwm_group_t") group)
:   Start the PWM group.

    参数
    :   **group** – the group ID to be started

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_GROUP\_NOT\_EXIST: the group doesn’t exist
        - others: other errors.

<a id="_CPPv417bk_pwm_group_stop11pwm_group_t"></a>

<a id="_CPPv317bk_pwm_group_stop11pwm_group_t"></a> <a id="_CPPv217bk_pwm_group_stop11pwm_group_t"></a> <a id="bk_pwm_group_stop__pwm_group_t"></a> <a id="group__bk__api__pwm_1gae78db60193a534fa44665e4397c4d3c9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_group\_stop([pwm\_group\_t](#_CPPv411pwm_group_t "pwm_group_t") group)
:   Stop the PWM group.

    参数
    :   **group** – the group ID to be stopped

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_GROUP\_NOT\_EXIST: the group doesn’t exist
        - others: other errors.

<a id="_CPPv419bk_pwm_capture_init10pwm_chan_tPK25pwm_capture_init_config_t"></a>

<a id="_CPPv319bk_pwm_capture_init10pwm_chan_tPK25pwm_capture_init_config_t"></a> <a id="_CPPv219bk_pwm_capture_init10pwm_chan_tPK25pwm_capture_init_config_t"></a> <a id="bk_pwm_capture_init__pwm_chan_t.pwm_capture_init_config_tCP"></a> <a id="group__bk__api__pwm_1gab70684dbb531cabcd790bcf5cfe6d074"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_capture\_init([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, const [pwm\_capture\_init\_config\_t](#_CPPv425pwm_capture_init_config_t "pwm_capture_init_config_t") \*config)
:   Init the PWM capture.

    The PWM capture can calculate the cycles between two different edges, currently we support following mode:

    1. PWM\_CAPTURE\_POS \- calcualte cycles between two pos-edge, the interrupt trigger in post edge
    2. PWM\_CAPTURE\_NEG \- calcualte cycles between two neg-edge, the interrupt trigger in neg edge
    3. PWM\_CAPTURE\_EDGE \- calculate cycles between two edge (pos or neg), the interrupt trigger in post or neg edge.

    Example 1 \- init the capture in PWM\_CAPTURE\_POS mode::

    ```
                    |<------ C1 ---->|<------- C2 ------->|
                     ______           ___________          ________________            _
     PWM input     _|      |_________|           |________|                |__________|

     Capture value                   |    C1              |             C2            |
    ```

    参数
    :   - **chan** – the capture channel
        - **config** – the configuration of capture

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_NOT\_INIT: PWM driver not init
        - BK\_ERR\_NULL\_PARAM: config is NULL
        - BK\_ERR\_PWM\_CHAN\_ID: invalid channel
        - BK\_ERR\_PWM\_CAPTURE\_EDGE: capture edge is invalid or not supported.
        - others: other errors.

<a id="_CPPv421bk_pwm_capture_deinit10pwm_chan_t"></a>

<a id="_CPPv321bk_pwm_capture_deinit10pwm_chan_t"></a> <a id="_CPPv221bk_pwm_capture_deinit10pwm_chan_t"></a> <a id="bk_pwm_capture_deinit__pwm_chan_t"></a> <a id="group__bk__api__pwm_1gacc5c6613d4e8f1fea9f3e4a557b220a9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_capture\_deinit([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Deinit the PWM capture.

    参数
    :   **chan** – the capture channel

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_NOT\_INIT: PWM driver not init
        - BK\_ERR\_PWM\_CHAN\_ID: invalid channel
        - others: other errors.

<a id="_CPPv420bk_pwm_capture_start10pwm_chan_t"></a>

<a id="_CPPv320bk_pwm_capture_start10pwm_chan_t"></a> <a id="_CPPv220bk_pwm_capture_start10pwm_chan_t"></a> <a id="bk_pwm_capture_start__pwm_chan_t"></a> <a id="group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_capture\_start([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Start the PWM capture.

    参数
    :   **chan** – channel to be started

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_NOT\_INIT: PWM driver not init
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - others: other errors.

<a id="_CPPv419bk_pwm_capture_stop10pwm_chan_t"></a>

<a id="_CPPv319bk_pwm_capture_stop10pwm_chan_t"></a> <a id="_CPPv219bk_pwm_capture_stop10pwm_chan_t"></a> <a id="bk_pwm_capture_stop__pwm_chan_t"></a> <a id="group__bk__api__pwm_1ga24d919012ae64d84daf61063aa8eff05"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_capture\_stop([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Stop the PWM capture.

    参数
    :   **chan** – channel to be stopped

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_NOT\_INIT: PWM driver not init
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - others: other errors.

<a id="_CPPv424bk_pwm_capture_get_value10pwm_chan_t"></a>

<a id="_CPPv324bk_pwm_capture_get_value10pwm_chan_t"></a> <a id="_CPPv224bk_pwm_capture_get_value10pwm_chan_t"></a> <a id="bk_pwm_capture_get_value__pwm_chan_t"></a> <a id="group__bk__api__pwm_1ga22fa4105ec2ca1e86c7e041327d418a2"></a> uint32\_t bk\_pwm\_capture\_get\_value([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Get the capture value.

    **Attention**
    :   The caller need to make sure the parameter chan is correct!

    参数
    :   **chan** – PWM channel

    返回
    :   capture value

<a id="_CPPv436bk_pwm_capture_get_period_duty_cycle10pwm_chan_t8uint32_t"></a>

<a id="_CPPv336bk_pwm_capture_get_period_duty_cycle10pwm_chan_t8uint32_t"></a> <a id="_CPPv236bk_pwm_capture_get_period_duty_cycle10pwm_chan_t8uint32_t"></a> <a id="bk_pwm_capture_get_period_duty_cycle__pwm_chan_t.uint32_t"></a> <a id="group__bk__api__pwm_1gaae0e6d04a844d9ef917e605184006760"></a> uint32\_t bk\_pwm\_capture\_get\_period\_duty\_cycle([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, uint32\_t timeout\_ms)
:   Get the capture period and duty cycle.

    **Attention**
    :   The caller need to make sure the parameter chan is correct!

    参数
    :   - **chan** – PWM channel
        - **timeout\_ms** – timeout ms

    返回
    :   period and duty cycle

<a id="_CPPv421bk_pwm_set_mode_timer10pwm_chan_t"></a>

<a id="_CPPv321bk_pwm_set_mode_timer10pwm_chan_t"></a> <a id="_CPPv221bk_pwm_set_mode_timer10pwm_chan_t"></a> <a id="bk_pwm_set_mode_timer__pwm_chan_t"></a> <a id="group__bk__api__pwm_1gaa2eb2adac89054fe6518549ce66095af"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_pwm\_set\_mode\_timer([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Set pwm channel as timer mode.

    **Attention**
    :   The caller need to make sure the parameter chan is correct!

    参数
    :   **chan** – PWM channel

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_PWM\_CHAN\_ID: invalid PWM channel
        - others: other errors.

<a id="pwm-api-typedefs"></a>

## PWM API Typedefs

<a id="id1"></a>

### Header File

- [pwm\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/pwm_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv417pwm_init_config_t"></a>

<a id="_CPPv317pwm_init_config_t"></a> <a id="_CPPv217pwm_init_config_t"></a> <a id="pwm_init_config_t"></a> <a id="structpwm__init__config__t"></a> struct pwm\_init\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N17pwm_init_config_t12period_cycleE"></a>

    <a id="_CPPv3N17pwm_init_config_t12period_cycleE"></a> <a id="_CPPv2N17pwm_init_config_t12period_cycleE"></a> <a id="pwm_init_config_t::period_cycle__uint32_t"></a> <a id="structpwm__init__config__t_1ab749468cfef62b6c2b86adc19d89b38d"></a> uint32\_t period\_cycle
    :   PWM period cycle, unit is (1/clock\_frequency)

    <a id="_CPPv4N17pwm_init_config_t10duty_cycleE"></a>

    <a id="_CPPv3N17pwm_init_config_t10duty_cycleE"></a> <a id="_CPPv2N17pwm_init_config_t10duty_cycleE"></a> <a id="pwm_init_config_t::duty_cycle__uint32_t"></a> <a id="structpwm__init__config__t_1ac68cd0863edce926e4546624fe27c54d"></a> uint32\_t duty\_cycle
    :   PWM duty cycle, unit is (1/clock\_frequency)

    <a id="_CPPv4N17pwm_init_config_t11duty2_cycleE"></a>

    <a id="_CPPv3N17pwm_init_config_t11duty2_cycleE"></a> <a id="_CPPv2N17pwm_init_config_t11duty2_cycleE"></a> <a id="pwm_init_config_t::duty2_cycle__uint32_t"></a> <a id="structpwm__init__config__t_1aa67a29752cdd231412d86664cc723cc1"></a> uint32\_t duty2\_cycle
    :   PWM duty2 cycle, unit is (1/clock\_frequency)

    <a id="_CPPv4N17pwm_init_config_t11duty3_cycleE"></a>

    <a id="_CPPv3N17pwm_init_config_t11duty3_cycleE"></a> <a id="_CPPv2N17pwm_init_config_t11duty3_cycleE"></a> <a id="pwm_init_config_t::duty3_cycle__uint32_t"></a> <a id="structpwm__init__config__t_1a15ad2c46dfe5ec63bf7d9921dda970a4"></a> uint32\_t duty3\_cycle
    :   PWM duty2 cycle, unit is (1/clock\_frequency)

    <a id="_CPPv4N17pwm_init_config_t3pscE"></a>

    <a id="_CPPv3N17pwm_init_config_t3pscE"></a> <a id="_CPPv2N17pwm_init_config_t3pscE"></a> <a id="pwm_init_config_t::psc__uint32_t"></a> <a id="structpwm__init__config__t_1ade8cb5254dbf52b4479d62a581060563"></a> uint32\_t psc
    :   Specifies the prescaler value used to divide the TIM clock. This parameter can be a number between Min Data\=0x00 and Max atа \= 0xFF

    <a id="_CPPv4N17pwm_init_config_t8reservedE"></a>

    <a id="_CPPv3N17pwm_init_config_t8reservedE"></a> <a id="_CPPv2N17pwm_init_config_t8reservedE"></a> <a id="pwm_init_config_t::reserved__uint32_tA"></a> <a id="structpwm__init__config__t_1a078437b04f78004a55e100aa3162a8c9"></a> uint32\_t reserved\[4\]
    :   Reserved for future extend, must set to 0

<a id="_CPPv424pwm_period_duty_config_t"></a>

<a id="_CPPv324pwm_period_duty_config_t"></a> <a id="_CPPv224pwm_period_duty_config_t"></a> <a id="pwm_period_duty_config_t"></a> <a id="structpwm__period__duty__config__t"></a> struct pwm\_period\_duty\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N24pwm_period_duty_config_t12period_cycleE"></a>

    <a id="_CPPv3N24pwm_period_duty_config_t12period_cycleE"></a> <a id="_CPPv2N24pwm_period_duty_config_t12period_cycleE"></a> <a id="pwm_period_duty_config_t::period_cycle__uint32_t"></a> <a id="structpwm__period__duty__config__t_1a20f9d203849b18c5d71d7fb4bc3840ba"></a> uint32\_t period\_cycle
    :   PWM period cycle, unit is (1/clock\_frequency)

    <a id="_CPPv4N24pwm_period_duty_config_t10duty_cycleE"></a>

    <a id="_CPPv3N24pwm_period_duty_config_t10duty_cycleE"></a> <a id="_CPPv2N24pwm_period_duty_config_t10duty_cycleE"></a> <a id="pwm_period_duty_config_t::duty_cycle__uint32_t"></a> <a id="structpwm__period__duty__config__t_1af7650b485e8af6f2e6690ba37b456ead"></a> uint32\_t duty\_cycle
    :   PWM duty cycle, unit is (1/clock\_frequency)

    <a id="_CPPv4N24pwm_period_duty_config_t11duty2_cycleE"></a>

    <a id="_CPPv3N24pwm_period_duty_config_t11duty2_cycleE"></a> <a id="_CPPv2N24pwm_period_duty_config_t11duty2_cycleE"></a> <a id="pwm_period_duty_config_t::duty2_cycle__uint32_t"></a> <a id="structpwm__period__duty__config__t_1a6eb7cdcb8abaf68f1018a54b38dab4f5"></a> uint32\_t duty2\_cycle
    :   PWM duty2 cycle, unit is (1/clock\_frequency)

    <a id="_CPPv4N24pwm_period_duty_config_t11duty3_cycleE"></a>

    <a id="_CPPv3N24pwm_period_duty_config_t11duty3_cycleE"></a> <a id="_CPPv2N24pwm_period_duty_config_t11duty3_cycleE"></a> <a id="pwm_period_duty_config_t::duty3_cycle__uint32_t"></a> <a id="structpwm__period__duty__config__t_1a099b4b9afb7de038addeb8359bff49f9"></a> uint32\_t duty3\_cycle
    :   PWM duty3 cycle, unit is (1/clock\_frequency)

    <a id="_CPPv4N24pwm_period_duty_config_t3pscE"></a>

    <a id="_CPPv3N24pwm_period_duty_config_t3pscE"></a> <a id="_CPPv2N24pwm_period_duty_config_t3pscE"></a> <a id="pwm_period_duty_config_t::psc__uint32_t"></a> <a id="structpwm__period__duty__config__t_1af0ef26045d8e9c700b473a32d5065bd6"></a> uint32\_t psc
    :   Specifies the prescaler value used to divide the TIM clock. This parameter can be a number between Min Data\=0x00 and Max atа \= 0xFF

<a id="_CPPv425pwm_capture_init_config_t"></a>

<a id="_CPPv325pwm_capture_init_config_t"></a> <a id="_CPPv225pwm_capture_init_config_t"></a> <a id="pwm_capture_init_config_t"></a> <a id="structpwm__capture__init__config__t"></a> struct pwm\_capture\_init\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N25pwm_capture_init_config_t4edgeE"></a>

    <a id="_CPPv3N25pwm_capture_init_config_t4edgeE"></a> <a id="_CPPv2N25pwm_capture_init_config_t4edgeE"></a> <a id="pwm_capture_init_config_t::edge__pwm_capture_edge_t"></a> <a id="structpwm__capture__init__config__t_1ab92f0c5e232aae465319d99f0eb646ce"></a> [pwm\_capture\_edge\_t](#_CPPv418pwm_capture_edge_t "pwm_capture_edge_t") edge
    :   PWM chan capture edge

    <a id="_CPPv4N25pwm_capture_init_config_t3isrE"></a>

    <a id="_CPPv3N25pwm_capture_init_config_t3isrE"></a> <a id="_CPPv2N25pwm_capture_init_config_t3isrE"></a> <a id="pwm_capture_init_config_t::isr__pwm_isr_t"></a> <a id="structpwm__capture__init__config__t_1a108b6775a5534edaadcb543b002fd80e"></a> [pwm\_isr\_t](#_CPPv49pwm_isr_t "pwm_isr_t") isr
    :   PWM capture interrupt routine

<a id="_CPPv423pwm_group_init_config_t"></a>

<a id="_CPPv323pwm_group_init_config_t"></a> <a id="_CPPv223pwm_group_init_config_t"></a> <a id="pwm_group_init_config_t"></a> <a id="structpwm__group__init__config__t"></a> struct pwm\_group\_init\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N23pwm_group_init_config_t5chan1E"></a>

    <a id="_CPPv3N23pwm_group_init_config_t5chan1E"></a> <a id="_CPPv2N23pwm_group_init_config_t5chan1E"></a> <a id="pwm_group_init_config_t::chan1__pwm_chan_t"></a> <a id="structpwm__group__init__config__t_1a0a6efec5c253d009bc856f33630b881d"></a> [pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan1
    :   The first PWM channel ID in a group

    <a id="_CPPv4N23pwm_group_init_config_t5chan2E"></a>

    <a id="_CPPv3N23pwm_group_init_config_t5chan2E"></a> <a id="_CPPv2N23pwm_group_init_config_t5chan2E"></a> <a id="pwm_group_init_config_t::chan2__pwm_chan_t"></a> <a id="structpwm__group__init__config__t_1a92c7b624ff527f1c1c27c5c4a8bc1a84"></a> [pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan2
    :   The second PWM channel ID in a group

    <a id="_CPPv4N23pwm_group_init_config_t12period_cycleE"></a>

    <a id="_CPPv3N23pwm_group_init_config_t12period_cycleE"></a> <a id="_CPPv2N23pwm_group_init_config_t12period_cycleE"></a> <a id="pwm_group_init_config_t::period_cycle__uint32_t"></a> <a id="structpwm__group__init__config__t_1a057ed822167f13e18e13d8ae03478ef3"></a> uint32\_t period\_cycle
    :   PWM Group period cycle

    <a id="_CPPv4N23pwm_group_init_config_t16chan1_duty_cycleE"></a>

    <a id="_CPPv3N23pwm_group_init_config_t16chan1_duty_cycleE"></a> <a id="_CPPv2N23pwm_group_init_config_t16chan1_duty_cycleE"></a> <a id="pwm_group_init_config_t::chan1_duty_cycle__uint32_t"></a> <a id="structpwm__group__init__config__t_1ae637e51c6f0fee537ceecafa5d6ecc63"></a> uint32\_t chan1\_duty\_cycle
    :   Duty cycle of chan1

    <a id="_CPPv4N23pwm_group_init_config_t16chan2_duty_cycleE"></a>

    <a id="_CPPv3N23pwm_group_init_config_t16chan2_duty_cycleE"></a> <a id="_CPPv2N23pwm_group_init_config_t16chan2_duty_cycleE"></a> <a id="pwm_group_init_config_t::chan2_duty_cycle__uint32_t"></a> <a id="structpwm__group__init__config__t_1a8c8046ff3ccc21244efac6fbf0adb19b"></a> uint32\_t chan2\_duty\_cycle
    :   Duty cycle of chan2

    <a id="_CPPv4N23pwm_group_init_config_t3pscE"></a>

    <a id="_CPPv3N23pwm_group_init_config_t3pscE"></a> <a id="_CPPv2N23pwm_group_init_config_t3pscE"></a> <a id="pwm_group_init_config_t::psc__uint32_t"></a> <a id="structpwm__group__init__config__t_1aeae0a0989011a54738ee8b0ec9a2e958"></a> uint32\_t psc
    :   Specifies the prescaler value used to divide the TIM clock

<a id="_CPPv418pwm_group_config_t"></a>

<a id="_CPPv318pwm_group_config_t"></a> <a id="_CPPv218pwm_group_config_t"></a> <a id="pwm_group_config_t"></a> <a id="structpwm__group__config__t"></a> struct pwm\_group\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N18pwm_group_config_t12period_cycleE"></a>

    <a id="_CPPv3N18pwm_group_config_t12period_cycleE"></a> <a id="_CPPv2N18pwm_group_config_t12period_cycleE"></a> <a id="pwm_group_config_t::period_cycle__uint32_t"></a> <a id="structpwm__group__config__t_1ae336c5000e2e449e6030ed8a2c966fe0"></a> uint32\_t period\_cycle
    :   PWM Group period cycle

    <a id="_CPPv4N18pwm_group_config_t16chan1_duty_cycleE"></a>

    <a id="_CPPv3N18pwm_group_config_t16chan1_duty_cycleE"></a> <a id="_CPPv2N18pwm_group_config_t16chan1_duty_cycleE"></a> <a id="pwm_group_config_t::chan1_duty_cycle__uint32_t"></a> <a id="structpwm__group__config__t_1a440c9a79a03a0593b81082bad1ac987f"></a> uint32\_t chan1\_duty\_cycle
    :   Duty cycle of channel 1

    <a id="_CPPv4N18pwm_group_config_t16chan2_duty_cycleE"></a>

    <a id="_CPPv3N18pwm_group_config_t16chan2_duty_cycleE"></a> <a id="_CPPv2N18pwm_group_config_t16chan2_duty_cycleE"></a> <a id="pwm_group_config_t::chan2_duty_cycle__uint32_t"></a> <a id="structpwm__group__config__t_1a33de8d0b3a25085d638e60af204072b2"></a> uint32\_t chan2\_duty\_cycle
    :   Duty cycle of channel 2

    <a id="_CPPv4N18pwm_group_config_t3pscE"></a>

    <a id="_CPPv3N18pwm_group_config_t3pscE"></a> <a id="_CPPv2N18pwm_group_config_t3pscE"></a> <a id="pwm_group_config_t::psc__uint32_t"></a> <a id="structpwm__group__config__t_1a8531a8bbf20ebaea296f635e1eb73cc4"></a> uint32\_t psc
    :   Specifies the prescaler value used to divide the TIM clock

<a id="_CPPv422pwm_chan_duty_config_t"></a>

<a id="_CPPv322pwm_chan_duty_config_t"></a> <a id="_CPPv222pwm_chan_duty_config_t"></a> <a id="pwm_chan_duty_config_t"></a> <a id="structpwm__chan__duty__config__t"></a> struct pwm\_chan\_duty\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N22pwm_chan_duty_config_t4chanE"></a>

    <a id="_CPPv3N22pwm_chan_duty_config_t4chanE"></a> <a id="_CPPv2N22pwm_chan_duty_config_t4chanE"></a> <a id="pwm_chan_duty_config_t::chan__pwm_chan_t"></a> <a id="structpwm__chan__duty__config__t_1af59bb851e36de79b4cec90cb3f9ccef0"></a> [pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan
    :   PWM channel

    <a id="_CPPv4N22pwm_chan_duty_config_t10duty_cycleE"></a>

    <a id="_CPPv3N22pwm_chan_duty_config_t10duty_cycleE"></a> <a id="_CPPv2N22pwm_chan_duty_config_t10duty_cycleE"></a> <a id="pwm_chan_duty_config_t::duty_cycle__uint32_t"></a> <a id="structpwm__chan__duty__config__t_1aad6c27092a949be28b0f726622e27b3e"></a> uint32\_t duty\_cycle
    :   PWM period cycle

<a id="_CPPv424pwm_phase_shift_config_t"></a>

<a id="_CPPv324pwm_phase_shift_config_t"></a> <a id="_CPPv224pwm_phase_shift_config_t"></a> <a id="pwm_phase_shift_config_t"></a> <a id="structpwm__phase__shift__config__t"></a> struct pwm\_phase\_shift\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N24pwm_phase_shift_config_t3pscE"></a>

    <a id="_CPPv3N24pwm_phase_shift_config_t3pscE"></a> <a id="_CPPv2N24pwm_phase_shift_config_t3pscE"></a> <a id="pwm_phase_shift_config_t::psc__uint32_t"></a> <a id="structpwm__phase__shift__config__t_1a498a5e304c308f6a7e197321a9d0d0f0"></a> uint32\_t psc
    :   PWM prescaler value used to divide the TIM clock

    <a id="_CPPv4N24pwm_phase_shift_config_t12period_cycleE"></a>

    <a id="_CPPv3N24pwm_phase_shift_config_t12period_cycleE"></a> <a id="_CPPv2N24pwm_phase_shift_config_t12period_cycleE"></a> <a id="pwm_phase_shift_config_t::period_cycle__uint32_t"></a> <a id="structpwm__phase__shift__config__t_1a491d6be629bdb3a6e88fed878c0c3bf0"></a> uint32\_t period\_cycle
    :   PWM period cycle

    <a id="_CPPv4N24pwm_phase_shift_config_t8chan_numE"></a>

    <a id="_CPPv3N24pwm_phase_shift_config_t8chan_numE"></a> <a id="_CPPv2N24pwm_phase_shift_config_t8chan_numE"></a> <a id="pwm_phase_shift_config_t::chan_num__uint32_t"></a> <a id="structpwm__phase__shift__config__t_1a2620cc927025f18e010e8c350766d366"></a> uint32\_t chan\_num
    :   PWM phase shift channel number

    <a id="_CPPv4N24pwm_phase_shift_config_t11duty_configE"></a>

    <a id="_CPPv3N24pwm_phase_shift_config_t11duty_configE"></a> <a id="_CPPv2N24pwm_phase_shift_config_t11duty_configE"></a> <a id="pwm_phase_shift_config_t::duty_config__pwm_chan_duty_config_tA"></a> <a id="structpwm__phase__shift__config__t_1acff9bdf946bee9b6c812b7149f96ecf4"></a> [pwm\_chan\_duty\_config\_t](#_CPPv422pwm_chan_duty_config_t "pwm_chan_duty_config_t") duty\_config\[PWM\_PHASE\_SHIFT\_CHAN\_NUM\]
    :   PWM phase shift duty configuration

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_PWM_CLOCK"></a>

<a id="group__bk__api__pwm__defs_1gabf5c42b5b0387f2e00e5f911812925e8"></a> BK\_ERR\_PWM\_CLOCK
:   PWM global clock type not supported

<a id="c.BK_ERR_PWM_CHAN_CLOCK"></a>

<a id="group__bk__api__pwm__defs_1ga885446ebbf565d18c7329d7b86b8c325"></a> BK\_ERR\_PWM\_CHAN\_CLOCK
:   PWM channel clock type not supported

<a id="c.BK_ERR_PWM_CHAN_ID"></a>

<a id="group__bk__api__pwm__defs_1gabd542d224be84b7b798d4124fda4e6e7"></a> BK\_ERR\_PWM\_CHAN\_ID
:   PWM channel number is invalid

<a id="c.BK_ERR_PWM_PERIOD_DUTY"></a>

<a id="group__bk__api__pwm__defs_1ga03230b60af4b3e9dda99c1f90e259a22"></a> BK\_ERR\_PWM\_PERIOD\_DUTY
:   PWM all duty cycle \> period cycle

<a id="c.BK_ERR_PWM_CAPTURE_EDGE"></a>

<a id="group__bk__api__pwm__defs_1gaf5dd08f1c4a450fba4d2eb2aedeb8001"></a> BK\_ERR\_PWM\_CAPTURE\_EDGE
:   PWM capture edge is invalid

<a id="c.BK_ERR_PWM_NOT_INIT"></a>

<a id="group__bk__api__pwm__defs_1ga92c4037f7b9c81a69b4cb0edfa3e12f8"></a> BK\_ERR\_PWM\_NOT\_INIT
:   PWM driver not init

<a id="c.BK_ERR_PWM_CHAN_NOT_INIT"></a>

<a id="group__bk__api__pwm__defs_1ga904d83b9db9f83106edebc7e00913cd8"></a> BK\_ERR\_PWM\_CHAN\_NOT\_INIT
:   PWM channel not init

<a id="c.BK_ERR_PWM_CHAN_NOT_START"></a>

<a id="group__bk__api__pwm__defs_1ga364f36b1cc5b65d7e29ed7b4ec8feb0a"></a> BK\_ERR\_PWM\_CHAN\_NOT\_START
:   PWM channel not init

<a id="c.BK_ERR_PWM_GROUP_ID"></a>

<a id="group__bk__api__pwm__defs_1ga276ddf2b711f37c05be8716ef47c155e"></a> BK\_ERR\_PWM\_GROUP\_ID
:   PWM group ID is invalid

<a id="c.BK_ERR_PWM_GROUP_EXIST"></a>

<a id="group__bk__api__pwm__defs_1ga9d4677cebf2e7dde1e31ae59d4c70ace"></a> BK\_ERR\_PWM\_GROUP\_EXIST
:   PWM group already exists

<a id="c.BK_ERR_PWM_GROUP_CHAN_USED"></a>

<a id="group__bk__api__pwm__defs_1gaf7ad5022b975ef06996af44ea51437f5"></a> BK\_ERR\_PWM\_GROUP\_CHAN\_USED
:   PWM channel is used by other group

<a id="c.BK_ERR_PWM_GROUP_NOT_EXIST"></a>

<a id="group__bk__api__pwm__defs_1gaf1c60ca888f32320630e7e00a68c04c3"></a> BK\_ERR\_PWM\_GROUP\_NOT\_EXIST
:   PWM group doesn’t exist

<a id="c.BK_ERR_PWM_GROUP_DUTY"></a>

<a id="group__bk__api__pwm__defs_1ga18de2b44ee3cd46e4b9f5342eca66259"></a> BK\_ERR\_PWM\_GROUP\_DUTY
:   PWM group cycle invalid

<a id="c.BK_ERR_PWM_GROUP_SAME_CHAN"></a>

<a id="group__bk__api__pwm__defs_1ga25e629a59e4c2b8c4f60314413877693"></a> BK\_ERR\_PWM\_GROUP\_SAME\_CHAN
:   PWM group channel is same

<a id="c.BK_ERR_PWM_INVALID_GPIO_MODE"></a>

<a id="group__bk__api__pwm__defs_1gaa410e8dc2e65c5daf4d37d63849f97ec"></a> BK\_ERR\_PWM\_INVALID\_GPIO\_MODE
:   PWM invalid gpio mode

<a id="c.BK_ERR_PWM_PHASE_SHIFT_CHAN_NUM"></a>

<a id="group__bk__api__pwm__defs_1ga352b68c84169d21ef92129fe467a8811"></a> BK\_ERR\_PWM\_PHASE\_SHIFT\_CHAN\_NUM
:   PWM phase shift invalid chan number

<a id="c.BK_ERR_PWM_UNIT_ID"></a>

<a id="group__bk__api__pwm__defs_1ga8677603524f2de213f53b9f2ed3c4053"></a> BK\_ERR\_PWM\_UNIT\_ID
:   PWM unit ID is invalid

<a id="c.PWM_DEFAULT_PWM_CONFIG"></a>

<a id="group__bk__api__pwm__defs_1ga320bf462556b243418dcaf53b511248f"></a> PWM\_DEFAULT\_PWM\_CONFIG()
:   default PWM configuration

<a id="c.PWM_DEFAULT_PWM_CAPTURE_CONFIG"></a>

<a id="group__bk__api__pwm__defs_1ga79bd19031593c9106e0d24b2359165eb"></a> PWM\_DEFAULT\_PWM\_CAPTURE\_CONFIG()
:   default PWM capture configuration

<a id="c.PWM_PHASE_SHIFT_CHAN_NUM"></a>

<a id="group__bk__api__pwm__defs_1gaf45d5ccbd0a362f8a53d20a619d083cc"></a> PWM\_PHASE\_SHIFT\_CHAN\_NUM

<a id="c.PWM_GROUP_ID_INVALID"></a>

<a id="group__bk__api__pwm__defs_1ga65162e88dcc0c530728c892315e7fb7c"></a> PWM\_GROUP\_ID\_INVALID
:   Invalid PWM group ID

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv49pwm_isr_t"></a>

<a id="_CPPv39pwm_isr_t"></a> <a id="_CPPv29pwm_isr_t"></a> <a id="pwm_isr_t"></a> <a id="group__bk__api__pwm__defs_1gadae38e8f179a2edeba3f11e8cfcdc78c"></a> typedef void (\*pwm\_isr\_t)([pwm\_chan\_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   PWM interrupt service routine.

<a id="_CPPv411pwm_group_t"></a>

<a id="_CPPv311pwm_group_t"></a> <a id="_CPPv211pwm_group_t"></a> <a id="pwm_group_t"></a> <a id="group__bk__api__pwm__defs_1ga115385da2e9bd346e0216e21fd281208"></a> typedef uint8\_t pwm\_group\_t
:   PWM group type.

<a id="id2"></a>

### Header File

- [hal\_pwm\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/_header_files/include/driver/hal/hal_pwm_types.h)

<a id="id3"></a>

### Macros

<a id="c.BK_ERR_PWM_HAL_CLOCK"></a>

<a id="hal__pwm__types_8h_1ad98076dd62b0ffe7092aa2668c55bd29"></a> BK\_ERR\_PWM\_HAL\_CLOCK

<a id="id4"></a>

### Type Definitions

<a id="_CPPv410pwm_unit_t"></a>

<a id="_CPPv310pwm_unit_t"></a> <a id="_CPPv210pwm_unit_t"></a> <a id="pwm_unit_t"></a> <a id="hal__pwm__types_8h_1a5b753ea72e34f3f6d8adcadfbcdd6254"></a> typedef uint8\_t pwm\_unit\_t

<a id="_CPPv410pwm_chan_t"></a>

<a id="_CPPv310pwm_chan_t"></a> <a id="_CPPv210pwm_chan_t"></a> <a id="pwm_chan_t"></a> <a id="hal__pwm__types_8h_1a2135f4dfe7ab04cc7a81d3afea48e071"></a> typedef uint8\_t pwm\_chan\_t

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv410pwm_mode_t"></a>

<a id="_CPPv310pwm_mode_t"></a> <a id="_CPPv210pwm_mode_t"></a> <a id="hal__pwm__types_8h_1a562b5946a0edd6f5eebb63db7d154d56"></a> enum pwm\_mode\_t
:   *Values:*

    <a id="_CPPv4N10pwm_mode_t13PWM_MODE_IDLEE"></a>

    <a id="_CPPv3N10pwm_mode_t13PWM_MODE_IDLEE"></a> <a id="_CPPv2N10pwm_mode_t13PWM_MODE_IDLEE"></a> <a id="hal__pwm__types_8h_1a562b5946a0edd6f5eebb63db7d154d56ab31b0831f95f93c39dbc55fd5ad10981"></a> enumerator PWM\_MODE\_IDLE

    <a id="_CPPv4N10pwm_mode_t12PWM_MODE_PWME"></a>

    <a id="_CPPv3N10pwm_mode_t12PWM_MODE_PWME"></a> <a id="_CPPv2N10pwm_mode_t12PWM_MODE_PWME"></a> <a id="hal__pwm__types_8h_1a562b5946a0edd6f5eebb63db7d154d56a510580d0f1af744862f6e92551085e3c"></a> enumerator PWM\_MODE\_PWM

    <a id="_CPPv4N10pwm_mode_t15PWM_MODE_CAPTURE"></a>

    <a id="_CPPv3N10pwm_mode_t15PWM_MODE_CAPTURE"></a> <a id="_CPPv2N10pwm_mode_t15PWM_MODE_CAPTURE"></a> <a id="hal__pwm__types_8h_1a562b5946a0edd6f5eebb63db7d154d56a102ca80bba24c0ad71041c4e019569e7"></a> enumerator PWM\_MODE\_CAPTUR

<a id="_CPPv48pwm_id_t"></a>

<a id="_CPPv38pwm_id_t"></a> <a id="_CPPv28pwm_id_t"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876a"></a> enum pwm\_id\_t
:   *Values:*

    <a id="_CPPv4N8pwm_id_t8PWM_ID_0E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_0E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_0E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa5993abe85bee1d06921c26669cffeb62"></a> enumerator PWM\_ID\_0
    :   pwm id 0

    <a id="_CPPv4N8pwm_id_t8PWM_ID_1E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_1E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_1E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa09c27b6b43ee33117227218c4cc578a4"></a> enumerator PWM\_ID\_1
    :   pwm id 1

    <a id="_CPPv4N8pwm_id_t8PWM_ID_2E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_2E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_2E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa2333eaad15ddc974f4b0216cbeb589ff"></a> enumerator PWM\_ID\_2
    :   pwm id 2

    <a id="_CPPv4N8pwm_id_t8PWM_ID_3E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_3E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_3E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa9b694d64ab94700ec622fee63b6f34d5"></a> enumerator PWM\_ID\_3
    :   pwm id 3

    <a id="_CPPv4N8pwm_id_t8PWM_ID_4E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_4E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_4E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa59d635d4e436052c2424bd19933dd7e6"></a> enumerator PWM\_ID\_4
    :   pwm id 4

    <a id="_CPPv4N8pwm_id_t8PWM_ID_5E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_5E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_5E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa6dfde548e67a9e8ca70224c178d6477e"></a> enumerator PWM\_ID\_5
    :   pwm id 5

    <a id="_CPPv4N8pwm_id_t8PWM_ID_6E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_6E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_6E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa179360014ec4cf17504b1ea4315721ba"></a> enumerator PWM\_ID\_6

    <a id="_CPPv4N8pwm_id_t8PWM_ID_7E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_7E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_7E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa45d022c592359b4cef40baee2d8eb707"></a> enumerator PWM\_ID\_7

    <a id="_CPPv4N8pwm_id_t8PWM_ID_8E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_8E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_8E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa730d7f836658024db3fd8e5488b6cbf7"></a> enumerator PWM\_ID\_8

    <a id="_CPPv4N8pwm_id_t8PWM_ID_9E"></a>

    <a id="_CPPv3N8pwm_id_t8PWM_ID_9E"></a> <a id="_CPPv2N8pwm_id_t8PWM_ID_9E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa249e20f5fe6097ea6bbe7a574fd200c5"></a> enumerator PWM\_ID\_9

    <a id="_CPPv4N8pwm_id_t9PWM_ID_10E"></a>

    <a id="_CPPv3N8pwm_id_t9PWM_ID_10E"></a> <a id="_CPPv2N8pwm_id_t9PWM_ID_10E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aae4159b65db03bf0bb3c11503c7f9f747"></a> enumerator PWM\_ID\_10

    <a id="_CPPv4N8pwm_id_t9PWM_ID_11E"></a>

    <a id="_CPPv3N8pwm_id_t9PWM_ID_11E"></a> <a id="_CPPv2N8pwm_id_t9PWM_ID_11E"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aa20fee1364e89639db4d43e27fe47c2c1"></a> enumerator PWM\_ID\_11

    <a id="_CPPv4N8pwm_id_t10PWM_ID_MAXE"></a>

    <a id="_CPPv3N8pwm_id_t10PWM_ID_MAXE"></a> <a id="_CPPv2N8pwm_id_t10PWM_ID_MAXE"></a> <a id="hal__pwm__types_8h_1aa07dfec16bd76056216d48bf2bb3876aaa1e81e39e848d4e023f4ba4e939b4f43"></a> enumerator PWM\_ID\_MAX
    :   pwm id max

<a id="_CPPv48pwm_ch_t"></a>

<a id="_CPPv38pwm_ch_t"></a> <a id="_CPPv28pwm_ch_t"></a> <a id="hal__pwm__types_8h_1a28b207509aa7b6a0186762e4e1a09dc7"></a> enum pwm\_ch\_t
:   *Values:*

    <a id="_CPPv4N8pwm_ch_t8PWM_CH_0E"></a>

    <a id="_CPPv3N8pwm_ch_t8PWM_CH_0E"></a> <a id="_CPPv2N8pwm_ch_t8PWM_CH_0E"></a> <a id="hal__pwm__types_8h_1a28b207509aa7b6a0186762e4e1a09dc7ad2bd10b32596ca573ec2ec31daaf4998"></a> enumerator PWM\_CH\_0

    <a id="_CPPv4N8pwm_ch_t8PWM_CH_1E"></a>

    <a id="_CPPv3N8pwm_ch_t8PWM_CH_1E"></a> <a id="_CPPv2N8pwm_ch_t8PWM_CH_1E"></a> <a id="hal__pwm__types_8h_1a28b207509aa7b6a0186762e4e1a09dc7a6300613564a56414ac0eec80a6ce4e71"></a> enumerator PWM\_CH\_1

    <a id="_CPPv4N8pwm_ch_t8PWM_CH_2E"></a>

    <a id="_CPPv3N8pwm_ch_t8PWM_CH_2E"></a> <a id="_CPPv2N8pwm_ch_t8PWM_CH_2E"></a> <a id="hal__pwm__types_8h_1a28b207509aa7b6a0186762e4e1a09dc7af6884c8a61b8619059be65933bdecded"></a> enumerator PWM\_CH\_2

    <a id="_CPPv4N8pwm_ch_t8PWM_CH_3E"></a>

    <a id="_CPPv3N8pwm_ch_t8PWM_CH_3E"></a> <a id="_CPPv2N8pwm_ch_t8PWM_CH_3E"></a> <a id="hal__pwm__types_8h_1a28b207509aa7b6a0186762e4e1a09dc7ab42018afa904659c002b91ecb2b0b7db"></a> enumerator PWM\_CH\_3

    <a id="_CPPv4N8pwm_ch_t8PWM_CH_4E"></a>

    <a id="_CPPv3N8pwm_ch_t8PWM_CH_4E"></a> <a id="_CPPv2N8pwm_ch_t8PWM_CH_4E"></a> <a id="hal__pwm__types_8h_1a28b207509aa7b6a0186762e4e1a09dc7acd159437c492ba2b4416e28d3cf13d05"></a> enumerator PWM\_CH\_4

    <a id="_CPPv4N8pwm_ch_t8PWM_CH_5E"></a>

    <a id="_CPPv3N8pwm_ch_t8PWM_CH_5E"></a> <a id="_CPPv2N8pwm_ch_t8PWM_CH_5E"></a> <a id="hal__pwm__types_8h_1a28b207509aa7b6a0186762e4e1a09dc7ab3c9cf720279143b50c9829544c52f02"></a> enumerator PWM\_CH\_5

    <a id="_CPPv4N8pwm_ch_t10PWM_CH_MAXE"></a>

    <a id="_CPPv3N8pwm_ch_t10PWM_CH_MAXE"></a> <a id="_CPPv2N8pwm_ch_t10PWM_CH_MAXE"></a> <a id="hal__pwm__types_8h_1a28b207509aa7b6a0186762e4e1a09dc7a2dda23738e7e21a014e66102399e387b"></a> enumerator PWM\_CH\_MAX

<a id="_CPPv413pwm_src_clk_t"></a>

<a id="_CPPv313pwm_src_clk_t"></a> <a id="_CPPv213pwm_src_clk_t"></a> <a id="hal__pwm__types_8h_1aadf7638b929b475ca773ea25e93332ed"></a> enum pwm\_src\_clk\_t
:   *Values:*

    <a id="_CPPv4N13pwm_src_clk_t14PWM_SCLK_CLK32E"></a>

    <a id="_CPPv3N13pwm_src_clk_t14PWM_SCLK_CLK32E"></a> <a id="_CPPv2N13pwm_src_clk_t14PWM_SCLK_CLK32E"></a> <a id="hal__pwm__types_8h_1aadf7638b929b475ca773ea25e93332eda11c687a67e141e313c5b2cb13cf85f09"></a> enumerator PWM\_SCLK\_CLK32
    :   PWM source clock dco

    <a id="_CPPv4N13pwm_src_clk_t13PWM_SCLK_XTALE"></a>

    <a id="_CPPv3N13pwm_src_clk_t13PWM_SCLK_XTALE"></a> <a id="_CPPv2N13pwm_src_clk_t13PWM_SCLK_XTALE"></a> <a id="hal__pwm__types_8h_1aadf7638b929b475ca773ea25e93332eda3fd4a9086bd04a94d2394bbc5d646c74"></a> enumerator PWM\_SCLK\_XTAL
    :   PWM source clock xtal 26M

<a id="_CPPv413sys_sel_pwm_t"></a>

<a id="_CPPv313sys_sel_pwm_t"></a> <a id="_CPPv213sys_sel_pwm_t"></a> <a id="hal__pwm__types_8h_1a28cc0069b46ad944dc520fa88d692721"></a> enum sys\_sel\_pwm\_t
:   *Values:*

    <a id="_CPPv4N13sys_sel_pwm_t12SYS_SEL_PWM0E"></a>

    <a id="_CPPv3N13sys_sel_pwm_t12SYS_SEL_PWM0E"></a> <a id="_CPPv2N13sys_sel_pwm_t12SYS_SEL_PWM0E"></a> <a id="hal__pwm__types_8h_1a28cc0069b46ad944dc520fa88d692721a8144cf160c0b3324ad84d7b03382d0db"></a> enumerator SYS\_SEL\_PWM0

    <a id="_CPPv4N13sys_sel_pwm_t12SYS_SEL_PWM1E"></a>

    <a id="_CPPv3N13sys_sel_pwm_t12SYS_SEL_PWM1E"></a> <a id="_CPPv2N13sys_sel_pwm_t12SYS_SEL_PWM1E"></a> <a id="hal__pwm__types_8h_1a28cc0069b46ad944dc520fa88d692721ac2628281a826d8ad27dc9c1f3ec6ad35"></a> enumerator SYS\_SEL\_PWM1

<a id="_CPPv418pwm_capture_edge_t"></a>

<a id="_CPPv318pwm_capture_edge_t"></a> <a id="_CPPv218pwm_capture_edge_t"></a> <a id="hal__pwm__types_8h_1aedd7b5d94a532f360672e0c15a9a0fca"></a> enum pwm\_capture\_edge\_t
:   *Values:*

    <a id="_CPPv4N18pwm_capture_edge_t15PWM_CAPTURE_POSE"></a>

    <a id="_CPPv3N18pwm_capture_edge_t15PWM_CAPTURE_POSE"></a> <a id="_CPPv2N18pwm_capture_edge_t15PWM_CAPTURE_POSE"></a> <a id="hal__pwm__types_8h_1aedd7b5d94a532f360672e0c15a9a0fcaa3e9f31e4a9782ef4ede3c230c5a49826"></a> enumerator PWM\_CAPTURE\_POS
    :   Calculate cycles between two post edges

    <a id="_CPPv4N18pwm_capture_edge_t15PWM_CAPTURE_NEGE"></a>

    <a id="_CPPv3N18pwm_capture_edge_t15PWM_CAPTURE_NEGE"></a> <a id="_CPPv2N18pwm_capture_edge_t15PWM_CAPTURE_NEGE"></a> <a id="hal__pwm__types_8h_1aedd7b5d94a532f360672e0c15a9a0fcaa00d9538d24f8e37caef7e9fd8fd9fca2"></a> enumerator PWM\_CAPTURE\_NEG
    :   Calculate cycles between two negtive edges

    <a id="_CPPv4N18pwm_capture_edge_t16PWM_CAPTURE_EDGEE"></a>

    <a id="_CPPv3N18pwm_capture_edge_t16PWM_CAPTURE_EDGEE"></a> <a id="_CPPv2N18pwm_capture_edge_t16PWM_CAPTURE_EDGEE"></a> <a id="hal__pwm__types_8h_1aedd7b5d94a532f360672e0c15a9a0fcaae8c0bad41012e9a936e6087c9b638d4d"></a> enumerator PWM\_CAPTURE\_EDGE
    :   Calculate cycles between two edges (post or negative)

    <a id="_CPPv4N18pwm_capture_edge_t15PWM_CAPTURE_MAXE"></a>

    <a id="_CPPv3N18pwm_capture_edge_t15PWM_CAPTURE_MAXE"></a> <a id="_CPPv2N18pwm_capture_edge_t15PWM_CAPTURE_MAXE"></a> <a id="hal__pwm__types_8h_1aedd7b5d94a532f360672e0c15a9a0fcaa6e9bad4f81380aafb96e07c9103ea794"></a> enumerator PWM\_CAPTURE\_MAX
    :   Invalid capture mode
