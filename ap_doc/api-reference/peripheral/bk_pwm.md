# PWM



## PWM API Status

| API | BK7259_AP |
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


## PWM Channel Number

| Capability | BK7259_AP |
| --- | --- |
| Channel Number | 12 |


## PWM Group Support

| Capability | BK7259_AP |
| --- | --- |
| Software Group | Y |
| Hardware Group | Y |


## PWM Duty Support

| Capability | BK7259_AP |
| --- | --- |
| period_cycle | Y |
| duty_cycle | Y |

For unsupported duty fileds, we should set them to 0.


## PWM Capture Edge Support Status

| Capability | BK7259_AP |
| --- | --- |
| PWM_CAPTURE_POS | Y |
| PWM_CAPTURE_NEG | Y |
| PWM_CAPTURE_EDGE | Y |


## PWM Channel and GPIO Map

| Channel Number | BK7259_AP |
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

If the channel has more than one GPIO to map. Please refer to the <gpio_map.h> file for the default GPIO port <GPIO_PWM_MAP_TABLE>.


## PWM API Reference


### Header File


- [pwm.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/pwm.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/pwm.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_driver_init(void)
:   Init the PWM driver.

    This API init the resoure common to all PWM channels:


    - Init PWM driver control memory

    - Configure PWM common clock to 26M

    This API should be called before any other PWM APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_driver_deinit(void)
:   Deinit the PWM driver.

    This API free all resource related to PWM and power down all PWM channels.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_init([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, const [pwm_init_config_t](#_CPPv417pwm_init_config_t "pwm_init_config_t") *config)
:   Init the PWM channel.

    This API init the PWM channel:


    - Power up the PWM channel

    - Configure the PWM channel clock to 26M

    - Map the PWM channel to dedicated GPIO port

    - Set the period and duty cycle.

    For duty/cycle relationship, refer to [bk_pwm_set_period_duty()](#group__bk__api__pwm_1ga45326f56e267f9deb61f8b45c459b44a "#group__bk__api__pwm_1ga45326f56e267f9deb61f8b45c459b44a")

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_NOT_INIT: PWM driver not init

        - BK_ERR_NULL_PARAM: config is NULL

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - BK_ERR_PWM_PERIOD_DUTY: PWM duty/period relationship is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_deinit([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Deinit a PWM channel.

    This API deinit the PWM channel:


    - Stop the PWM channel

    - Reset all configuration of PWM channel to default value

    - Power down the PWM channel

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_start([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Stop a PWM channel.

    This API init the resoure common to all PWM channels:


    - Init PWM driver control memory

    - Configure PWM common clock to 26M

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_stop([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Stop a PWM channel.

    This API init the resoure common to all PWM channels:


    - Init PWM driver control memory

    - Configure PWM common clock to 26M

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_set_period_duty([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, [pwm_period_duty_config_t](#_CPPv424pwm_period_duty_config_t "pwm_period_duty_config_t") *config)
:   Configure the PWM period and duty cycle.

    This API is used to configure the period and duty time. The unit is cycle of PWM channel clock, since the PWM channel clock is default to 26M, the unit is 1/26M (1/26 000 000) seconds.

    The beken chip supports up to 3 duties, the exact duty numbers depends on the target type.

    EXample1 - the simplest case::

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

    Example2 - 3 duty with initial signal high::

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

    Example3 - 3 duty with initial signal low::

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

    Example4 - 3 duty with initial signal low and period > (D1 + D2 + D3)::

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
    :   1. The period should great or equal to (D1 + D2 + D3)


    **Attention**
    :   2. If the duty Dx is 0, then Dx+1 to D3 should also be 0. If D1 is 0, it indicates the duty ratio is 0% and the signal is always low.


    **Attention**
    :   3. If D1 equals period, it indicates the duty ratio is 100% and the signal is always high.


    **Attention**
    :   4. The signal strengh between two successive duties is opposite, e.g. if signal of D1 is high, then signal of D2 is low.


    **Attention**
    :   5. The initial signal is the signal strengh of D1 if D1 is not 0.


    **Attention**
    :   6. The duty/period configuration is very flexible, different configurations may have same result.

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: config is NULL

        - BK_ERR_PWM_CHAN_NOT_INIT: PWM channel not init

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - BK_ERR_PWM_PERIOD_DUTY: PWM duty/period relationship is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_set_init_signal_low([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Set the initial signal to low.

    Set the initial signal level of the first duty which is indicated by duty_cycle.


    **Attention**
    :   The signal will always be high if the duty_cycle equals period cycle (duty ratio is 100%), regardless whether this API is called or NOT.

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_CHAN_NOT_INIT: PWM channel not init

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_set_init_signal_high([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Set the initial signal to high.

    Set the initial signal level of the first duty which is indicated by duty_cycle.


    **Attention**
    :   The signal will always be low if the duty_cycle is 0 (duty ratio is 0%), regardless whether this API is called or NOT.

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_CHAN_NOT_INIT: PWM channel not init

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_register_isr([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, [pwm_isr_t](#_CPPv49pwm_isr_t "pwm_isr_t") isr)
:   Register the interrupt service routine for PWM channel.


    **Attention**
    :   1. Both [bk_pwm_capture_init()](#group__bk__api__pwm_1gab70684dbb531cabcd790bcf5cfe6d074 "#group__bk__api__pwm_1gab70684dbb531cabcd790bcf5cfe6d074") and this API can set the ISR, the one called later makes sense.

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_NOT_INIT: PWM driver not init

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_enable_interrupt([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Enable interrupt of PWM channel.

    The PWM channel interrupt is disabled by default when starting the channel by [bk_pwm_start()](#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919 "#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919") or [bk_pwm_group_start()](#group__bk__api__pwm_1gaf87327843711c56cab915f02b42a602a "#group__bk__api__pwm_1gaf87327843711c56cab915f02b42a602a"), while it’s enabled by default when starting the channel by [bk_pwm_capture_start()](#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a "#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a").

    This API is designed mainly for debug purpose, we can use it to enable the interrupt of any PWM channel, regardless of whether the channel is started by [bk_pwm_start()](#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919 "#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919") or [bk_pwm_group_start()](#group__bk__api__pwm_1gaf87327843711c56cab915f02b42a602a "#group__bk__api__pwm_1gaf87327843711c56cab915f02b42a602a") or [bk_pwm_capture_start()](#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a "#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a").

    The [bk_pwm_stop()](#group__bk__api__pwm_1gad88155b2ed4b16afc638696ee389c995 "#group__bk__api__pwm_1gad88155b2ed4b16afc638696ee389c995") and [bk_pwm_group_stop()](#group__bk__api__pwm_1gae78db60193a534fa44665e4397c4d3c9 "#group__bk__api__pwm_1gae78db60193a534fa44665e4397c4d3c9") also disable the interrupt, but the [bk_pwm_start()](#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919 "#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919") and bk_pwm_group_start will not enable the interrupt. So if the channel interrupt is enabled, and then stop and start the channel, we need to call this API to re-enable the interrupt.


    **Attention**
    :   1. The interrupt can be enabled only after PWM channel is started by [bk_pwm_start()](#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919 "#group__bk__api__pwm_1gad7adc69069f8645766d1056d7ff2f919").

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_NOT_INIT: PWM driver not init

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - BK_ERR_PWM_CHAN_NOT_START: PWM channel is not started

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_disable_interrupt([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Disable interrupt of PWM channel.

    Stop the interrupt of any PWM channel, regardless whether the channel is in PWM mode, or PWM capture mode, or PWM group mode.


    **Attention**
    :   1. [bk_pwm_capture_start()](#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a "#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a") will enable the interrupt anyway, so if we want to disable the interrupt of PWM capture channel, we need to call this API anytime [bk_pwm_capture_start()](#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a "#group__bk__api__pwm_1gaa8d1d9cee6831f6f03360a2fa3d3915a") is called.

    参数
    :   **chan** – the channel ID

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_NOT_INIT: PWM driver not init

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_group_init(const [pwm_group_init_config_t](#_CPPv423pwm_group_init_config_t "pwm_group_init_config_t") *config, [pwm_group_t](#_CPPv411pwm_group_t "pwm_group_t") *group)
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

    The D1/D2 indicates the dead time cycle, it’s calculated based on following formula: D1 = D2 = (period - chan1_duty_cycle - chan2_duty_cycle)/2


    **Attention**
    :   1. This API doesn’t check whether the PWM channel is already used in other mode. e.g. If the API doesn’t returns error if config->chan1 is already used in capture mode, the application need to make sure the channel configured in the group is not used for other purpose.


    **Attention**
    :   2. The chan2_duty_cycle is actually the 2nd signal wave for channel 2, as depicted in above picture.


    **Attention**
    :   3. This API supports to group any two available channel into a PWM group, however, we recommend to group 0/1, 2/3, 4/5 into a group, because hardware can support these group directly and we can start the channels in the group at exactly same time.


    **Attention**
    :   4. The chan1_duty_cycle and chan2_duty_cycle should be great than 0.

    参数
    :   - **config** – configuration of PWM group

        - **group** – store the group ID if the API is succeed.

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_NOT_INIT: PWM driver not init

        - BK_ERR_NULL_PARAM: config or group is NULL

        - BK_ERR_PWM_CHAN_ID: channel 1 or 2 in the group is invalid

        - BK_ERR_PWM_GROUP_SAME_CHAN: channel 1 and 2 are same

        - BK_ERR_PWM_GROUP_EXIST: a group with channel 1 and 2 is already exists

        - BK_ERR_PWM_GROUP_CHAN_USED: a existing group has a channel equals to channel 1 or 2

        - BK_ERR_PWM_GROUP_DUTY: period cycle < (chan1_duty_cycle + chan2_duty_cycle)

        - BK_ERR_PWM_PERIOD_DUTY: PWM duty/period relationship is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_group_deinit([pwm_group_t](#_CPPv411pwm_group_t "pwm_group_t") group)
:   Deinit a PWM group.

    This API stops and powers down channels in a PWM group.


    **Attention**
    :   This API returns BK_OK directly if the group doesn’t exist.

    参数
    :   **group** – the group ID returned bk [bk_pwm_group_init()](#group__bk__api__pwm_1gab3f68971d07e8e7f589b57f1eda510e7 "#group__bk__api__pwm_1gab3f68971d07e8e7f589b57f1eda510e7")

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_group_set_config([pwm_group_t](#_CPPv411pwm_group_t "pwm_group_t") group, const [pwm_group_config_t](#_CPPv418pwm_group_config_t "pwm_group_config_t") *config)
:   Configure the PWM group.

    Configure the duty and period of a PWM group, for duty/period relationship refer to [bk_pwm_group_init()](#group__bk__api__pwm_1gab3f68971d07e8e7f589b57f1eda510e7 "#group__bk__api__pwm_1gab3f68971d07e8e7f589b57f1eda510e7").


    **Attention**
    :   The configuration can’t take effect until the current period is ended

    参数
    :   - **group** – the group ID to be configured

        - **config** – configuration of PWM group

    返回
    :   - BK_OK: succeed

        - BK_ERR_NULL_PARAM: config or group is NULL

        - BK_ERR_PWM_GROUP_NOT_EXIST: the group doesn’t exist

        - BK_ERR_PWM_GROUP_DUTY: period cycle < (chan1_duty_cycle + chan2_duty_cycle)

        - BK_ERR_PWM_PERIOD_DUTY: PWM duty/period relationship is invalid

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_group_start([pwm_group_t](#_CPPv411pwm_group_t "pwm_group_t") group)
:   Start the PWM group.

    参数
    :   **group** – the group ID to be started

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_GROUP_NOT_EXIST: the group doesn’t exist

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_group_stop([pwm_group_t](#_CPPv411pwm_group_t "pwm_group_t") group)
:   Stop the PWM group.

    参数
    :   **group** – the group ID to be stopped

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_GROUP_NOT_EXIST: the group doesn’t exist

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_capture_init([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, const [pwm_capture_init_config_t](#_CPPv425pwm_capture_init_config_t "pwm_capture_init_config_t") *config)
:   Init the PWM capture.

    The PWM capture can calculate the cycles between two different edges, currently we support following mode:

    1. PWM_CAPTURE_POS - calcualte cycles between two pos-edge, the interrupt trigger in post edge
    2. PWM_CAPTURE_NEG - calcualte cycles between two neg-edge, the interrupt trigger in neg edge
    3. PWM_CAPTURE_EDGE - calculate cycles between two edge (pos or neg), the interrupt trigger in post or neg edge.

    Example 1 - init the capture in PWM_CAPTURE_POS mode::

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
    :   - BK_OK: succeed

        - BK_ERR_PWM_NOT_INIT: PWM driver not init

        - BK_ERR_NULL_PARAM: config is NULL

        - BK_ERR_PWM_CHAN_ID: invalid channel

        - BK_ERR_PWM_CAPTURE_EDGE: capture edge is invalid or not supported.

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_capture_deinit([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Deinit the PWM capture.

    参数
    :   **chan** – the capture channel

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_NOT_INIT: PWM driver not init

        - BK_ERR_PWM_CHAN_ID: invalid channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_capture_start([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Start the PWM capture.

    参数
    :   **chan** – channel to be started

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_NOT_INIT: PWM driver not init

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_capture_stop([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Stop the PWM capture.

    参数
    :   **chan** – channel to be stopped

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_NOT_INIT: PWM driver not init

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - others: other errors.

uint32_t bk_pwm_capture_get_value([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Get the capture value.


    **Attention**
    :   The caller need to make sure the parameter chan is correct!

    参数
    :   **chan** – PWM channel

    返回
    :   capture value

uint32_t bk_pwm_capture_get_period_duty_cycle([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan, uint32_t timeout_ms)
:   Get the capture period and duty cycle.


    **Attention**
    :   The caller need to make sure the parameter chan is correct!

    参数
    :   - **chan** – PWM channel

        - **timeout_ms** – timeout ms

    返回
    :   period and duty cycle

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_pwm_set_mode_timer([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   Set pwm channel as timer mode.


    **Attention**
    :   The caller need to make sure the parameter chan is correct!

    参数
    :   **chan** – PWM channel

    返回
    :   - BK_OK: succeed

        - BK_ERR_PWM_CHAN_ID: invalid PWM channel

        - others: other errors.


## PWM API Typedefs


### Header File


- [pwm_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/pwm_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/pwm_types.h")


### Structures

struct pwm_init_config_t

struct pwm_period_duty_config_t

struct pwm_capture_init_config_t

struct pwm_group_init_config_t

struct pwm_group_config_t

struct pwm_chan_duty_config_t

struct pwm_phase_shift_config_t


### Macros

BK_ERR_PWM_CLOCK
:   PWM global clock type not supported

BK_ERR_PWM_CHAN_CLOCK
:   PWM channel clock type not supported

BK_ERR_PWM_CHAN_ID
:   PWM channel number is invalid

BK_ERR_PWM_PERIOD_DUTY
:   PWM all duty cycle > period cycle

BK_ERR_PWM_CAPTURE_EDGE
:   PWM capture edge is invalid

BK_ERR_PWM_NOT_INIT
:   PWM driver not init

BK_ERR_PWM_CHAN_NOT_INIT
:   PWM channel not init

BK_ERR_PWM_CHAN_NOT_START
:   PWM channel not init

BK_ERR_PWM_GROUP_ID
:   PWM group ID is invalid

BK_ERR_PWM_GROUP_EXIST
:   PWM group already exists

BK_ERR_PWM_GROUP_CHAN_USED
:   PWM channel is used by other group

BK_ERR_PWM_GROUP_NOT_EXIST
:   PWM group doesn’t exist

BK_ERR_PWM_GROUP_DUTY
:   PWM group cycle invalid

BK_ERR_PWM_GROUP_SAME_CHAN
:   PWM group channel is same

BK_ERR_PWM_INVALID_GPIO_MODE
:   PWM invalid gpio mode

BK_ERR_PWM_PHASE_SHIFT_CHAN_NUM
:   PWM phase shift invalid chan number

BK_ERR_PWM_UNIT_ID
:   PWM unit ID is invalid

PWM_DEFAULT_PWM_CONFIG()
:   default PWM configuration

PWM_DEFAULT_PWM_CAPTURE_CONFIG()
:   default PWM capture configuration

PWM_PHASE_SHIFT_CHAN_NUM

PWM_GROUP_ID_INVALID
:   Invalid PWM group ID


### Type Definitions

typedef void (*pwm_isr_t)([pwm_chan_t](#_CPPv410pwm_chan_t "pwm_chan_t") chan)
:   PWM interrupt service routine.

typedef uint8_t pwm_group_t
:   PWM group type.


### Enumerations

enum pwm_fade_mode_t
:   *Values:*

    enumerator PWM_DUTY_DIR_DECREASE
    :   PWM duty decrease direction

    enumerator PWM_DUTY_DIR_INCREASE
    :   PWM duty increase direction

    enumerator PWM_DUTY_DIR_MAX


### Header File


- [hal/hal_pwm_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_pwm_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/hal/hal_pwm_types.h")


### Macros

BK_ERR_PWM_HAL_CLOCK


### Type Definitions

typedef uint8_t pwm_unit_t

typedef uint8_t pwm_chan_t


### Enumerations

enum pwm_mode_t
:   *Values:*

    enumerator PWM_MODE_IDLE

    enumerator PWM_MODE_PWM

    enumerator PWM_MODE_CAPTUR

enum pwm_id_t
:   *Values:*

    enumerator PWM_ID_0
    :   pwm id 0

    enumerator PWM_ID_1
    :   pwm id 1

    enumerator PWM_ID_2
    :   pwm id 2

    enumerator PWM_ID_3
    :   pwm id 3

    enumerator PWM_ID_4
    :   pwm id 4

    enumerator PWM_ID_5
    :   pwm id 5

    enumerator PWM_ID_6

    enumerator PWM_ID_7

    enumerator PWM_ID_8

    enumerator PWM_ID_9

    enumerator PWM_ID_10

    enumerator PWM_ID_11

    enumerator PWM_ID_MAX
    :   pwm id max

enum pwm_ch_t
:   *Values:*

    enumerator PWM_CH_0

    enumerator PWM_CH_1

    enumerator PWM_CH_2

    enumerator PWM_CH_3

    enumerator PWM_CH_4

    enumerator PWM_CH_5

    enumerator PWM_CH_MAX

enum pwm_src_clk_t
:   *Values:*

    enumerator PWM_SCLK_CLK32
    :   PWM source clock dco

    enumerator PWM_SCLK_XTAL
    :   PWM source clock xtal 26M

enum sys_sel_pwm_t
:   *Values:*

    enumerator SYS_SEL_PWM0

    enumerator SYS_SEL_PWM1

enum pwm_capture_edge_t
:   *Values:*

    enumerator PWM_CAPTURE_POS
    :   Calculate cycles between two post edges

    enumerator PWM_CAPTURE_NEG
    :   Calculate cycles between two negtive edges

    enumerator PWM_CAPTURE_EDGE
    :   Calculate cycles between two edges (post or negative)

    enumerator PWM_CAPTURE_MAX
    :   Invalid capture mode

enum pwm_polarity_t
:   *Values:*

    enumerator PWM_POLARITY_POSITIVE
    :   PWM positive polarity

    enumerator PWM_POLARITY_NEGATIVE
    :   PWM negative polarity

    enumerator PWM_POLARITY_MAX
    :   Invalid polarity
