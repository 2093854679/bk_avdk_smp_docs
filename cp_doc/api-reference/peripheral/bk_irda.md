# IRDA


BK7259 CP 侧 IRDA API（`include/driver/irda.h`）。


## IRDA API Reference


### Header File


- [irda.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/irda.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/irda.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_driver_init(void)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_driver_deinit(void)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_init_tx(const [irda_tx_init_config_t](#_CPPv421irda_tx_init_config_t "irda_tx_init_config_t") *tx_config)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_init_rx(const [irda_rx_init_config_t](#_CPPv421irda_rx_init_config_t "irda_rx_init_config_t") *rx_config)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_write_words(const uint16_t *data, uint32_t entry_count)

int bk_irda_read_words(uint16_t *data, uint32_t entry_count, uint32_t timeout_ms)


## IRDA API Typedefs


### Header File


- [irda_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/irda_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/irda_types.h")


### Structures

struct irda_tx_init_config_t
:   Public Members

    uint32_t clk_freq_input
    :   Clock Division Factor, range [1, 127]. IRDA default clock is 26MHz

    uint32_t carrier_period_cycle
    :   Carrier period cycle, range [0, 255], unit: 1us

    uint32_t carrier_duty_cycle
    :   Carrier duty cycle, range [0, 255], unit: 1us

    uint32_t tx_initial_level
    :   TX initial level, 0 or 1

struct irda_rx_init_config_t
:   Public Members

    uint32_t clk_freq_input
    :   Clock Division Factor, range [1, 127]. IRDA default clock is 26MHz

    uint32_t rx_timeout_us
    :   RX done timeout, range [1, 65535], unit: 1us. No edge transition detected for this duration means transfer ended

    uint32_t rx_start_threshold_us
    :   RX start threshold, range [0, 4095], unit: 1us. First data packet exceeding this threshold begins the transfer

    uint32_t rx_initial_level
    :   RX initial level, 0 or 1


### Macros

BK_ERR_IRDA_NOT_INIT
:   IRDA driver not init

IRDA_CLK_FREQ_INPUT_MAX

IRDA_CARRIER_PERIOD_CYCLE_MAX

IRDA_CARRIER_DUTY_CYCLE_MAX

IRDA_RX_TIMEOUT_US_MAX

IRDA_RX_START_THRESHOLD_US_MAX
