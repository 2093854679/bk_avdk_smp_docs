# IRDA


BK7259 AP 侧 IRDA API（`include/driver/irda.h`）。


## IRDA API Reference


### Header File


- [irda.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/irda.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/irda.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_driver_init(void)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_driver_deinit(void)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_init_tx(const [irda_tx_init_config_t](#_CPPv421irda_tx_init_config_t "irda_tx_init_config_t") *tx_config)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_init_rx(const [irda_rx_init_config_t](#_CPPv421irda_rx_init_config_t "irda_rx_init_config_t") *rx_config)

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_irda_write_bytes(const void *data, uint32_t size)

int bk_irda_read_bytes(void *data, uint32_t size)


## IRDA API Typedefs


### Header File


- [irda_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/irda_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/irda_types.h")


### Structures

struct irda_tx_init_config_t
:   Public Members

    uint32_t carrier_period_cycle
    :   carrier period cycle, unit:1us

    uint32_t carrier_duty_cycle
    :   carrier duty cycle, unit:1us

struct irda_rx_init_config_t
