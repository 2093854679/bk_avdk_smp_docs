---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_irda.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="irda"></a>

# IRDA

BK7259 AP 侧 IRDA API（`include/driver/irda.h`）。

<a id="irda-api-reference"></a>

## IRDA API Reference

<a id="header-file"></a>

### Header File

- [irda.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/irda.h)

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

<a id="_CPPv419bk_irda_write_bytesPKv8uint32_t"></a>

<a id="_CPPv319bk_irda_write_bytesPKv8uint32_t"></a> <a id="_CPPv219bk_irda_write_bytesPKv8uint32_t"></a> <a id="bk_irda_write_bytes__voidCP.uint32_t"></a> <a id="irda_8h_1ae64a407a8adc8370ee17cb224ac0cc36"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_irda\_write\_bytes(const void \*data, uint32\_t size)

<a id="_CPPv418bk_irda_read_bytesPv8uint32_t"></a>

<a id="_CPPv318bk_irda_read_bytesPv8uint32_t"></a> <a id="_CPPv218bk_irda_read_bytesPv8uint32_t"></a> <a id="bk_irda_read_bytes__voidP.uint32_t"></a> <a id="irda_8h_1aee28490a1683603a13e0c91c311d5723"></a> int bk\_irda\_read\_bytes(void \*data, uint32\_t size)

<a id="irda-api-typedefs"></a>

## IRDA API Typedefs

<a id="id1"></a>

### Header File

- [irda\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/irda_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv421irda_tx_init_config_t"></a>

<a id="_CPPv321irda_tx_init_config_t"></a> <a id="_CPPv221irda_tx_init_config_t"></a> <a id="irda_tx_init_config_t"></a> <a id="structirda__tx__init__config__t"></a> struct irda\_tx\_init\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N21irda_tx_init_config_t20carrier_period_cycleE"></a>

    <a id="_CPPv3N21irda_tx_init_config_t20carrier_period_cycleE"></a> <a id="_CPPv2N21irda_tx_init_config_t20carrier_period_cycleE"></a> <a id="irda_tx_init_config_t::carrier_period_cycle__uint32_t"></a> <a id="structirda__tx__init__config__t_1a76b4cee7afbed7ca515a0591b21e0b0d"></a> uint32\_t carrier\_period\_cycle
    :   carrier period cycle, unit:1us

    <a id="_CPPv4N21irda_tx_init_config_t18carrier_duty_cycleE"></a>

    <a id="_CPPv3N21irda_tx_init_config_t18carrier_duty_cycleE"></a> <a id="_CPPv2N21irda_tx_init_config_t18carrier_duty_cycleE"></a> <a id="irda_tx_init_config_t::carrier_duty_cycle__uint32_t"></a> <a id="structirda__tx__init__config__t_1ad8b3fb82942d631856866d0e1130541b"></a> uint32\_t carrier\_duty\_cycle
    :   carrier duty cycle, unit:1us

<a id="_CPPv421irda_rx_init_config_t"></a>

<a id="_CPPv321irda_rx_init_config_t"></a> <a id="_CPPv221irda_rx_init_config_t"></a> <a id="irda_rx_init_config_t"></a> <a id="structirda__rx__init__config__t"></a> struct irda\_rx\_init\_config\_t
