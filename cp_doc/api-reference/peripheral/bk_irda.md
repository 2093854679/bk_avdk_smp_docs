---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_irda.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="irda"></a>

# IRDA

BK7259 CP 侧 IRDA API（`include/driver/irda.h`）。

<a id="irda-api-reference"></a>

## IRDA API Reference

<a id="header-file"></a>

### Header File

- [irda.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/irda.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419bk_irda_driver_initv"></a>

<a id="_CPPv319bk_irda_driver_initv"></a> <a id="_CPPv219bk_irda_driver_initv"></a> <a id="bk_irda_driver_init__void"></a> <a id="irda_8h_1aeea1409eed90c64f2b5c2fe3740efc37"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_irda\_driver\_init(void)

<a id="_CPPv421bk_irda_driver_deinitv"></a>

<a id="_CPPv321bk_irda_driver_deinitv"></a> <a id="_CPPv221bk_irda_driver_deinitv"></a> <a id="bk_irda_driver_deinit__void"></a> <a id="irda_8h_1aeb6d1f61bcf77cf61da4a9e430415229"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_irda\_driver\_deinit(void)

<a id="_CPPv415bk_irda_init_txPK21irda_tx_init_config_t"></a>

<a id="_CPPv315bk_irda_init_txPK21irda_tx_init_config_t"></a> <a id="_CPPv215bk_irda_init_txPK21irda_tx_init_config_t"></a> <a id="bk_irda_init_tx__irda_tx_init_config_tCP"></a> <a id="irda_8h_1a6cddfed57be46655f40b4251314de061"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_irda\_init\_tx(const [irda\_tx\_init\_config\_t](#_CPPv421irda_tx_init_config_t "irda_tx_init_config_t") \*tx\_config)

<a id="_CPPv415bk_irda_init_rxPK21irda_rx_init_config_t"></a>

<a id="_CPPv315bk_irda_init_rxPK21irda_rx_init_config_t"></a> <a id="_CPPv215bk_irda_init_rxPK21irda_rx_init_config_t"></a> <a id="bk_irda_init_rx__irda_rx_init_config_tCP"></a> <a id="irda_8h_1a35c93a7bd41a5cb4b18cb2bae31f3a99"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_irda\_init\_rx(const [irda\_rx\_init\_config\_t](#_CPPv421irda_rx_init_config_t "irda_rx_init_config_t") \*rx\_config)

<a id="_CPPv419bk_irda_write_wordsPK8uint16_t8uint32_t"></a>

<a id="_CPPv319bk_irda_write_wordsPK8uint16_t8uint32_t"></a> <a id="_CPPv219bk_irda_write_wordsPK8uint16_t8uint32_t"></a> <a id="bk_irda_write_words__uint16_tCP.uint32_t"></a> <a id="irda_8h_1afb88822566ea1009d228b8e3b9d2fc0e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_irda\_write\_words(const uint16\_t \*data, uint32\_t entry\_count)

<a id="_CPPv418bk_irda_read_wordsP8uint16_t8uint32_t8uint32_t"></a>

<a id="_CPPv318bk_irda_read_wordsP8uint16_t8uint32_t8uint32_t"></a> <a id="_CPPv218bk_irda_read_wordsP8uint16_t8uint32_t8uint32_t"></a> <a id="bk_irda_read_words__uint16_tP.uint32_t.uint32_t"></a> <a id="irda_8h_1a82aa959120af5258397b74a5b31d82ab"></a> int bk\_irda\_read\_words(uint16\_t \*data, uint32\_t entry\_count, uint32\_t timeout\_ms)

<a id="irda-api-typedefs"></a>

## IRDA API Typedefs

<a id="id1"></a>

### Header File

- [irda\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/irda_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv421irda_tx_init_config_t"></a>

<a id="_CPPv321irda_tx_init_config_t"></a> <a id="_CPPv221irda_tx_init_config_t"></a> <a id="irda_tx_init_config_t"></a> <a id="structirda__tx__init__config__t"></a> struct irda\_tx\_init\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21irda_tx_init_config_t14clk_freq_inputE"></a>

    <a id="_CPPv3N21irda_tx_init_config_t14clk_freq_inputE"></a> <a id="_CPPv2N21irda_tx_init_config_t14clk_freq_inputE"></a> <a id="irda_tx_init_config_t::clk_freq_input__uint32_t"></a> <a id="structirda__tx__init__config__t_1a48dc81ff452b5aa15e709fd44808357b"></a> uint32\_t clk\_freq\_input
    :   Clock Division Factor, range \[1, 127\]. IRDA default clock is 26MHz

    <a id="_CPPv4N21irda_tx_init_config_t20carrier_period_cycleE"></a>

    <a id="_CPPv3N21irda_tx_init_config_t20carrier_period_cycleE"></a> <a id="_CPPv2N21irda_tx_init_config_t20carrier_period_cycleE"></a> <a id="irda_tx_init_config_t::carrier_period_cycle__uint32_t"></a> <a id="structirda__tx__init__config__t_1a76b4cee7afbed7ca515a0591b21e0b0d"></a> uint32\_t carrier\_period\_cycle
    :   Carrier period cycle, range \[0, 255\], unit: 1us

    <a id="_CPPv4N21irda_tx_init_config_t18carrier_duty_cycleE"></a>

    <a id="_CPPv3N21irda_tx_init_config_t18carrier_duty_cycleE"></a> <a id="_CPPv2N21irda_tx_init_config_t18carrier_duty_cycleE"></a> <a id="irda_tx_init_config_t::carrier_duty_cycle__uint32_t"></a> <a id="structirda__tx__init__config__t_1ad8b3fb82942d631856866d0e1130541b"></a> uint32\_t carrier\_duty\_cycle
    :   Carrier duty cycle, range \[0, 255\], unit: 1us

    <a id="_CPPv4N21irda_tx_init_config_t16tx_initial_levelE"></a>

    <a id="_CPPv3N21irda_tx_init_config_t16tx_initial_levelE"></a> <a id="_CPPv2N21irda_tx_init_config_t16tx_initial_levelE"></a> <a id="irda_tx_init_config_t::tx_initial_level__uint32_t"></a> <a id="structirda__tx__init__config__t_1a137ed3cfe806d237c9c966ea9c6ba4f9"></a> uint32\_t tx\_initial\_level
    :   TX initial level, 0 or 1

<a id="_CPPv421irda_rx_init_config_t"></a>

<a id="_CPPv321irda_rx_init_config_t"></a> <a id="_CPPv221irda_rx_init_config_t"></a> <a id="irda_rx_init_config_t"></a> <a id="structirda__rx__init__config__t"></a> struct irda\_rx\_init\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21irda_rx_init_config_t14clk_freq_inputE"></a>

    <a id="_CPPv3N21irda_rx_init_config_t14clk_freq_inputE"></a> <a id="_CPPv2N21irda_rx_init_config_t14clk_freq_inputE"></a> <a id="irda_rx_init_config_t::clk_freq_input__uint32_t"></a> <a id="structirda__rx__init__config__t_1a1c7b3814a4fd600d18cf9c7c2158863d"></a> uint32\_t clk\_freq\_input
    :   Clock Division Factor, range \[1, 127\]. IRDA default clock is 26MHz

    <a id="_CPPv4N21irda_rx_init_config_t13rx_timeout_usE"></a>

    <a id="_CPPv3N21irda_rx_init_config_t13rx_timeout_usE"></a> <a id="_CPPv2N21irda_rx_init_config_t13rx_timeout_usE"></a> <a id="irda_rx_init_config_t::rx_timeout_us__uint32_t"></a> <a id="structirda__rx__init__config__t_1a79c0e538aa4a4ca9aa1622e108ff14d6"></a> uint32\_t rx\_timeout\_us
    :   RX done timeout, range \[1, 65535\], unit: 1us. No edge transition detected for this duration means transfer ended

    <a id="_CPPv4N21irda_rx_init_config_t21rx_start_threshold_usE"></a>

    <a id="_CPPv3N21irda_rx_init_config_t21rx_start_threshold_usE"></a> <a id="_CPPv2N21irda_rx_init_config_t21rx_start_threshold_usE"></a> <a id="irda_rx_init_config_t::rx_start_threshold_us__uint32_t"></a> <a id="structirda__rx__init__config__t_1af872c75d6cf4353744273a17f92db798"></a> uint32\_t rx\_start\_threshold\_us
    :   RX start threshold, range \[0, 4095\], unit: 1us. First data packet exceeding this threshold begins the transfer

    <a id="_CPPv4N21irda_rx_init_config_t16rx_initial_levelE"></a>

    <a id="_CPPv3N21irda_rx_init_config_t16rx_initial_levelE"></a> <a id="_CPPv2N21irda_rx_init_config_t16rx_initial_levelE"></a> <a id="irda_rx_init_config_t::rx_initial_level__uint32_t"></a> <a id="structirda__rx__init__config__t_1a9f7c2e531f9f1b46265111a8fe43f78d"></a> uint32\_t rx\_initial\_level
    :   RX initial level, 0 or 1

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_IRDA_NOT_INIT"></a>

<a id="irda__types_8h_1a0187a85af78921d56c7f12c845a9ff60"></a> BK\_ERR\_IRDA\_NOT\_INIT
:   IRDA driver not init

<a id="c.IRDA_CLK_FREQ_INPUT_MAX"></a>

<a id="irda__types_8h_1a5c5358f25b3229107efa25310866a1f6"></a> IRDA\_CLK\_FREQ\_INPUT\_MAX

<a id="c.IRDA_CARRIER_PERIOD_CYCLE_MAX"></a>

<a id="irda__types_8h_1a7f2171123ac02032c21d1b7b15096a88"></a> IRDA\_CARRIER\_PERIOD\_CYCLE\_MAX

<a id="c.IRDA_CARRIER_DUTY_CYCLE_MAX"></a>

<a id="irda__types_8h_1a0ff03f3f8699c606ba2aef03a1a7fa97"></a> IRDA\_CARRIER\_DUTY\_CYCLE\_MAX

<a id="c.IRDA_RX_TIMEOUT_US_MAX"></a>

<a id="irda__types_8h_1ac0459cee58d2554c2aa30373a7561d71"></a> IRDA\_RX\_TIMEOUT\_US\_MAX

<a id="c.IRDA_RX_START_THRESHOLD_US_MAX"></a>

<a id="irda__types_8h_1a00af0d468b1f3d39ae84efa2932929fd"></a> IRDA\_RX\_START\_THRESHOLD\_US\_MAX
