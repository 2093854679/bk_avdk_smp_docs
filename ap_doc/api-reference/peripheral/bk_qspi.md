---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_qspi.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="qspi"></a>

# QSPI

BK7259 AP 侧 QSPI API（`include/driver/qspi.h`、`include/driver/qspi_flash.h`、`include/driver/qspi_psram.h`）。
详细说明见 [QSPI 使用指南](../../developer-guide/peripheral/bk_qspi.md) 与 [QSPI Flash 使用指南](../../developer-guide/peripheral/bk_qspi_flash.md)。

<a id="qspi-api-reference"></a>

## QSPI API Reference

<a id="header-file"></a>

### Header File

- [qspi.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/qspi.h)

<a id="functions"></a>

### Functions

<a id="_CPPv419bk_qspi_driver_initv"></a>

<a id="_CPPv319bk_qspi_driver_initv"></a> <a id="_CPPv219bk_qspi_driver_initv"></a> <a id="bk_qspi_driver_init__void"></a> <a id="qspi_8h_1a63a7b7ae4f3d001688a3fb0e551ca831"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_driver\_init(void)
:   Init the QSPI driver.

    This API init the resoure common:

    - Init QSPI driver control memory

    **Attention**
    :   1\. This API should be called before any other QSPI APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv421bk_qspi_driver_deinitv"></a>

<a id="_CPPv321bk_qspi_driver_deinitv"></a> <a id="_CPPv221bk_qspi_driver_deinitv"></a> <a id="bk_qspi_driver_deinit__void"></a> <a id="qspi_8h_1a61c6929521c3047b04ac61250dc695b4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_driver\_deinit(void)
:   Deinit the QSPI driver.

    This API free all resource related to QSPI and disable QSPI.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv412bk_qspi_init9qspi_id_tPK13qspi_config_t"></a>

<a id="_CPPv312bk_qspi_init9qspi_id_tPK13qspi_config_t"></a> <a id="_CPPv212bk_qspi_init9qspi_id_tPK13qspi_config_t"></a> <a id="bk_qspi_init__qspi_id_t.qspi_config_tCP"></a> <a id="qspi_8h_1a3392bf144fde8fc8d684289a5baef30d"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_init([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, const [qspi\_config\_t](#_CPPv413qspi_config_t "qspi_config_t") \*config)
:   Init the QSPI.

    This API init the QSPI:

    - Power up the QSPI
    - Configure the QSPI clock
    - Map the QSPI to dedicated GPIO port
    - Enabel QSPI interrupt

    参数
    :   **config** – QSPI parameter settings

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_QSPI\_NOT\_INIT: QSPI driver not init
        - BK\_ERR\_NULL\_PARAM: QSPI config parameter is NULL
        - others: other errors.

<a id="_CPPv420bk_qspi_init_by_freq9qspi_id_t8uint32_t"></a>

<a id="_CPPv320bk_qspi_init_by_freq9qspi_id_t8uint32_t"></a> <a id="_CPPv220bk_qspi_init_by_freq9qspi_id_t8uint32_t"></a> <a id="bk_qspi_init_by_freq__qspi_id_t.uint32_t"></a> <a id="qspi_8h_1a86f48ae8c309e31c25a33f65fc5a2bfc"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_init\_by\_freq([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t clk\_hz)
:   Init the QSPI by target SCK frequency (convenience wrapper)

    This API picks the source clock and dividers whose resulting SCK is closest to clk\_hz (SCK \= src\_clock / (1 \+ src\_clk\_div)), fills a [qspi\_config\_t](#structqspi__config__t) and then calls bk\_qspi\_init(). The application only needs to provide the QSPI id and the desired clock in Hz, without caring about the source clock selection or divider details.

    参数
    :   - **id** – QSPI id
        - **clk\_hz** – target SCK frequency in Hz (max 80000000\)

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_QSPI\_NOT\_INIT: QSPI driver not init
        - others: forwarded from bk\_qspi\_init

<a id="_CPPv414bk_qspi_deinit9qspi_id_t"></a>

<a id="_CPPv314bk_qspi_deinit9qspi_id_t"></a> <a id="_CPPv214bk_qspi_deinit9qspi_id_t"></a> <a id="bk_qspi_deinit__qspi_id_t"></a> <a id="qspi_8h_1ae6412c224e1a1d76f41315d6a1ac6c72"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_deinit([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   Deinit the QSPI.

    This API deinit the QSPI:

    - Disable the QSPI interrupt
    - Power down the QSPI

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv415bk_qspi_command9qspi_id_tPK10qspi_cmd_t"></a>

<a id="_CPPv315bk_qspi_command9qspi_id_tPK10qspi_cmd_t"></a> <a id="_CPPv215bk_qspi_command9qspi_id_tPK10qspi_cmd_t"></a> <a id="bk_qspi_command__qspi_id_t.qspi_cmd_tCP"></a> <a id="qspi_8h_1a3ef60464b761592ce3dad19206c632fb"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_command([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, const [qspi\_cmd\_t](#_CPPv410qspi_cmd_t "qspi_cmd_t") \*cmd)
:   Init the QSPI command.

    参数
    :   **cmd** – QSPI device command

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv413bk_qspi_write9qspi_id_tPKv8uint32_t"></a>

<a id="_CPPv313bk_qspi_write9qspi_id_tPKv8uint32_t"></a> <a id="_CPPv213bk_qspi_write9qspi_id_tPKv8uint32_t"></a> <a id="bk_qspi_write__qspi_id_t.voidCP.uint32_t"></a> <a id="qspi_8h_1a8171c0338a4a0a372052f3087dff4bb7"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_write([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, const void \*data, uint32\_t size)
:   QSPI indirect mode write.

    参数
    :   - **base\_addr** – QSPI write address
        - **data** – QSPI write data
        - **size** – the size of QSPI write data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv412bk_qspi_read9qspi_id_tPv8uint32_t"></a>

<a id="_CPPv312bk_qspi_read9qspi_id_tPv8uint32_t"></a> <a id="_CPPv212bk_qspi_read9qspi_id_tPv8uint32_t"></a> <a id="bk_qspi_read__qspi_id_t.voidP.uint32_t"></a> <a id="qspi_8h_1a06c78f54e934f268448c6fd190bb3ced"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_read([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, void \*data, uint32\_t size)
:   QSPI indirect mode read.

    参数
    :   - **base\_addr** – QSPI read address
        - **data** – QSPI read data
        - **size** – the size of QSPI read data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_qspi_register_tx_isr10qspi_isr_tPv"></a>

<a id="_CPPv323bk_qspi_register_tx_isr10qspi_isr_tPv"></a> <a id="_CPPv223bk_qspi_register_tx_isr10qspi_isr_tPv"></a> <a id="bk_qspi_register_tx_isr__qspi_isr_t.voidP"></a> <a id="qspi_8h_1acde18cf937a31a42f9542747e862ebee"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_register\_tx\_isr([qspi\_isr\_t](#_CPPv410qspi_isr_t "qspi_isr_t") isr, void \*param)
:   Register the TX interrupt service routine for QSPI.

    参数
    :   - **isr** – QSPI TX callback
        - **param** – QSPI TX callback parameter

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_qspi_register_rx_isr10qspi_isr_tPv"></a>

<a id="_CPPv323bk_qspi_register_rx_isr10qspi_isr_tPv"></a> <a id="_CPPv223bk_qspi_register_rx_isr10qspi_isr_tPv"></a> <a id="bk_qspi_register_rx_isr__qspi_isr_t.voidP"></a> <a id="qspi_8h_1a7fd21409c7e06cd6095ffd389587f0f2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_register\_rx\_isr([qspi\_isr\_t](#_CPPv410qspi_isr_t "qspi_isr_t") isr, void \*param)
:   Register the RX interrupt service routine for QSPI.

    参数
    :   - **isr** – QSPI RX callback
        - **param** – QSPI RX callback parameter

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="qspi-flash-api-reference"></a>

## QSPI Flash API Reference

<a id="id1"></a>

### Header File

- [qspi\_flash.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/qspi_flash.h)

<a id="id2"></a>

### Functions

<a id="_CPPv418bk_qspi_flash_init9qspi_id_t"></a>

<a id="_CPPv318bk_qspi_flash_init9qspi_id_t"></a> <a id="_CPPv218bk_qspi_flash_init9qspi_id_t"></a> <a id="bk_qspi_flash_init__qspi_id_t"></a> <a id="qspi__flash_8h_1a44ca4cee42182d88a762637cb86ee1dd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_init([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   Init the QSPI flash.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_QSPI\_NOT\_INIT: QSPI driver not init
        - others: other errors.

<a id="_CPPv420bk_qspi_flash_deinit9qspi_id_t"></a>

<a id="_CPPv320bk_qspi_flash_deinit9qspi_id_t"></a> <a id="_CPPv220bk_qspi_flash_deinit9qspi_id_t"></a> <a id="bk_qspi_flash_deinit__qspi_id_t"></a> <a id="qspi__flash_8h_1aa77fa250aacc2c6997a0ad478c9801cf"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_deinit([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   Deinit the QSPI flash.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_QSPI\_NOT\_INIT: QSPI driver not init
        - others: other errors.

<a id="_CPPv421bk_qspi_flash_read_id9qspi_id_t"></a>

<a id="_CPPv321bk_qspi_flash_read_id9qspi_id_t"></a> <a id="_CPPv221bk_qspi_flash_read_id9qspi_id_t"></a> <a id="bk_qspi_flash_read_id__qspi_id_t"></a> <a id="qspi__flash_8h_1aa725e3b386c5167a1825430de06ad013"></a> uint32\_t bk\_qspi\_flash\_read\_id([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI flash read id.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv430bk_qspi_flash_set_protect_none9qspi_id_t"></a>

<a id="_CPPv330bk_qspi_flash_set_protect_none9qspi_id_t"></a> <a id="_CPPv230bk_qspi_flash_set_protect_none9qspi_id_t"></a> <a id="bk_qspi_flash_set_protect_none__qspi_id_t"></a> <a id="qspi__flash_8h_1a4482d8061dd956924f008af9cb9fe141"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_set\_protect\_none([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI flash set protect type as none to do erase / write.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_qspi_flash_erase_sector9qspi_id_t8uint32_t"></a>

<a id="_CPPv326bk_qspi_flash_erase_sector9qspi_id_t8uint32_t"></a> <a id="_CPPv226bk_qspi_flash_erase_sector9qspi_id_t8uint32_t"></a> <a id="bk_qspi_flash_erase_sector__qspi_id_t.uint32_t"></a> <a id="qspi__flash_8h_1a5e9dc2096ef13a742218ba29ae1d83e2"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_erase\_sector([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t addr)
:   QSPI flash erase sector.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_qspi_flash_erase9qspi_id_t8uint32_t8uint32_t"></a>

<a id="_CPPv319bk_qspi_flash_erase9qspi_id_t8uint32_t8uint32_t"></a> <a id="_CPPv219bk_qspi_flash_erase9qspi_id_t8uint32_t8uint32_t"></a> <a id="bk_qspi_flash_erase__qspi_id_t.uint32_t.uint32_t"></a> <a id="qspi__flash_8h_1af75d12b9ac737d946c613c5a645c70a1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_erase([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t addr, uint32\_t size)
:   QSPI flash erase.

    QSPI flash erase 4k/32k/64k with different type.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_qspi_flash_quad_enable9qspi_id_t"></a>

<a id="_CPPv325bk_qspi_flash_quad_enable9qspi_id_t"></a> <a id="_CPPv225bk_qspi_flash_quad_enable9qspi_id_t"></a> <a id="bk_qspi_flash_quad_enable__qspi_id_t"></a> <a id="qspi__flash_8h_1ad1bedda924048286ae615b51acdee444"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_quad\_enable([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI flash enable quad mode.

    返回
    :   - NA.

<a id="_CPPv423bk_qspi_flash_erase_32k9qspi_id_t8uint32_t"></a>

<a id="_CPPv323bk_qspi_flash_erase_32k9qspi_id_t8uint32_t"></a> <a id="_CPPv223bk_qspi_flash_erase_32k9qspi_id_t8uint32_t"></a> <a id="bk_qspi_flash_erase_32k__qspi_id_t.uint32_t"></a> <a id="qspi__flash_8h_1adeb912af681717ec08c75133c51e93ed"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_erase\_32k([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t addr)
:   QSPI flash erase 32k.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_qspi_flash_erase_64k9qspi_id_t8uint32_t"></a>

<a id="_CPPv323bk_qspi_flash_erase_64k9qspi_id_t8uint32_t"></a> <a id="_CPPv223bk_qspi_flash_erase_64k9qspi_id_t8uint32_t"></a> <a id="bk_qspi_flash_erase_64k__qspi_id_t.uint32_t"></a> <a id="qspi__flash_8h_1ab6460b2ed88214acbf0ccfb47d350185"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_erase\_64k([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t addr)
:   QSPI flash erase 64k.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv431bk_qspi_flash_quad_page_program9qspi_id_t8uint32_tPKv8uint32_t"></a>

<a id="_CPPv331bk_qspi_flash_quad_page_program9qspi_id_t8uint32_tPKv8uint32_t"></a> <a id="_CPPv231bk_qspi_flash_quad_page_program9qspi_id_t8uint32_tPKv8uint32_t"></a> <a id="bk_qspi_flash_quad_page_program__qspi_id_t.uint32_t.voidCP.uint32_t"></a> <a id="qspi__flash_8h_1aeab813ec0fc6501935e4e694bfaa6564"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_quad\_page\_program([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t addr, const void \*data, uint32\_t size)
:   QSPI flash quad write.

    参数
    :   - **addr** – QSPI write address
        - **data** – QSPI write data
        - **size** – the size of QSPI write data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv433bk_qspi_flash_single_page_program9qspi_id_t8uint32_tPKv8uint32_t"></a>

<a id="_CPPv333bk_qspi_flash_single_page_program9qspi_id_t8uint32_tPKv8uint32_t"></a> <a id="_CPPv233bk_qspi_flash_single_page_program9qspi_id_t8uint32_tPKv8uint32_t"></a> <a id="bk_qspi_flash_single_page_program__qspi_id_t.uint32_t.voidCP.uint32_t"></a> <a id="qspi__flash_8h_1a58fa74ac7e305ff43190434cf81adec9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_single\_page\_program([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t addr, const void \*data, uint32\_t size)
:   QSPI flash single write.

    参数
    :   - **addr** – QSPI write address
        - **data** – QSPI write data
        - **size** – the size of QSPI write data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_qspi_flash_quad_read9qspi_id_t8uint32_tPv8uint32_t"></a>

<a id="_CPPv323bk_qspi_flash_quad_read9qspi_id_t8uint32_tPv8uint32_t"></a> <a id="_CPPv223bk_qspi_flash_quad_read9qspi_id_t8uint32_tPv8uint32_t"></a> <a id="bk_qspi_flash_quad_read__qspi_id_t.uint32_t.voidP.uint32_t"></a> <a id="qspi__flash_8h_1aff06a791a09dc45c438642c4500b53ba"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_quad\_read([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t addr, void \*data, uint32\_t size)
:   QSPI flash quad read.

    参数
    :   - **addr** – QSPI read address
        - **data** – QSPI read data
        - **size** – the size of QSPI read data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_qspi_flash_single_read9qspi_id_t8uint32_tPv8uint32_t"></a>

<a id="_CPPv325bk_qspi_flash_single_read9qspi_id_t8uint32_tPv8uint32_t"></a> <a id="_CPPv225bk_qspi_flash_single_read9qspi_id_t8uint32_tPv8uint32_t"></a> <a id="bk_qspi_flash_single_read__qspi_id_t.uint32_t.voidP.uint32_t"></a> <a id="qspi__flash_8h_1a5f5dd7b9112640ece9cd166cd3f89d79"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_single\_read([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t addr, void \*data, uint32\_t size)
:   QSPI flash single read.

    参数
    :   - **addr** – QSPI read address
        - **data** – QSPI read data
        - **size** – the size of QSPI read data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_qspi_flash_write9qspi_id_t8uint32_tPKv8uint32_t"></a>

<a id="_CPPv319bk_qspi_flash_write9qspi_id_t8uint32_tPKv8uint32_t"></a> <a id="_CPPv219bk_qspi_flash_write9qspi_id_t8uint32_tPKv8uint32_t"></a> <a id="bk_qspi_flash_write__qspi_id_t.uint32_t.voidCP.uint32_t"></a> <a id="qspi__flash_8h_1a6d7e7f65d7385f1ecbb145d2e33c62e0"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_write([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t base\_addr, const void \*data, uint32\_t size)
:   QSPI flash write data.

    参数
    :   - **base\_addr** – QSPI write address
        - **data** – QSPI write data
        - **size** – the size of QSPI write data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_qspi_flash_read9qspi_id_t8uint32_tPv8uint32_t"></a>

<a id="_CPPv318bk_qspi_flash_read9qspi_id_t8uint32_tPv8uint32_t"></a> <a id="_CPPv218bk_qspi_flash_read9qspi_id_t8uint32_tPv8uint32_t"></a> <a id="bk_qspi_flash_read__qspi_id_t.uint32_t.voidP.uint32_t"></a> <a id="qspi__flash_8h_1ae6ddf61997f5b1aaa09c73082463a9a3"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_read([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t base\_addr, void \*data, uint32\_t size)
:   QSPI flash read data.

    参数
    :   - **base\_addr** – QSPI read address
        - **data** – QSPI read data
        - **size** – the size of QSPI read data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_qspi_flash_read_s0_s79qspi_id_t"></a>

<a id="_CPPv324bk_qspi_flash_read_s0_s79qspi_id_t"></a> <a id="_CPPv224bk_qspi_flash_read_s0_s79qspi_id_t"></a> <a id="bk_qspi_flash_read_s0_s7__qspi_id_t"></a> <a id="qspi__flash_8h_1a88e5b42b21c2fbdb183dc05fa805f2f5"></a> uint32\_t bk\_qspi\_flash\_read\_s0\_s7([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI flash read status register S0-S7.

    参数
    :   **id** – QSPI ID

    返回
    :   Status register S0-S7 value

<a id="_CPPv425bk_qspi_flash_read_s8_s159qspi_id_t"></a>

<a id="_CPPv325bk_qspi_flash_read_s8_s159qspi_id_t"></a> <a id="_CPPv225bk_qspi_flash_read_s8_s159qspi_id_t"></a> <a id="bk_qspi_flash_read_s8_s15__qspi_id_t"></a> <a id="qspi__flash_8h_1a1bb72a6ded2deeaf93d5ab93d308cb73"></a> uint32\_t bk\_qspi\_flash\_read\_s8\_s15([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI flash read status register S8-S15.

    参数
    :   **id** – QSPI ID

    返回
    :   Status register S8-S15 value

<a id="_CPPv426bk_qspi_flash_read_s16_s239qspi_id_t"></a>

<a id="_CPPv326bk_qspi_flash_read_s16_s239qspi_id_t"></a> <a id="_CPPv226bk_qspi_flash_read_s16_s239qspi_id_t"></a> <a id="bk_qspi_flash_read_s16_s23__qspi_id_t"></a> <a id="qspi__flash_8h_1a98e5fdde13a930cf21bff3482ac0715c"></a> uint32\_t bk\_qspi\_flash\_read\_s16\_s23([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI flash read status register S16-S23.

    参数
    :   **id** – QSPI ID

    返回
    :   Status register S16-S23 value

<a id="_CPPv427bk_qspi_flash_write_s16_s239qspi_id_t7uint8_t"></a>

<a id="_CPPv327bk_qspi_flash_write_s16_s239qspi_id_t7uint8_t"></a> <a id="_CPPv227bk_qspi_flash_write_s16_s239qspi_id_t7uint8_t"></a> <a id="bk_qspi_flash_write_s16_s23__qspi_id_t.uint8_t"></a> <a id="qspi__flash_8h_1a307bc7a376c5879e7ddbd37de17c71f4"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_flash\_write\_s16\_s23([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint8\_t status\_reg\_data)
:   QSPI flash write status register S16-S23.

    参数
    :   - **id** – QSPI ID
        - **status\_reg\_data** – Status register S16-S23 value to write

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="qspi-psram-api-reference"></a>

## QSPI PSRAM API Reference

<a id="id3"></a>

### Header File

- [qspi\_psram.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/qspi_psram.h)

<a id="id4"></a>

### Functions

<a id="_CPPv418bk_qspi_psram_init9qspi_id_t"></a>

<a id="_CPPv318bk_qspi_psram_init9qspi_id_t"></a> <a id="_CPPv218bk_qspi_psram_init9qspi_id_t"></a> <a id="bk_qspi_psram_init__qspi_id_t"></a> <a id="qspi__psram_8h_1ab04991b5145658d88673ae3d756afe96"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_init([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   Init the QSPI psram.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_QSPI\_NOT\_INIT: QSPI driver not init
        - others: other errors.

<a id="_CPPv420bk_qspi_psram_deinit9qspi_id_t"></a>

<a id="_CPPv320bk_qspi_psram_deinit9qspi_id_t"></a> <a id="_CPPv220bk_qspi_psram_deinit9qspi_id_t"></a> <a id="bk_qspi_psram_deinit__qspi_id_t"></a> <a id="qspi__psram_8h_1a4934cd813123afb2a2d7e976763ef14e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_deinit([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   Deinit the QSPI psram.

    返回
    :   - BK\_OK: succeed
        - BK\_ERR\_QSPI\_NOT\_INIT: QSPI driver not init
        - others: other errors.

<a id="_CPPv429bk_qspi_psram_enter_quad_mode9qspi_id_t"></a>

<a id="_CPPv329bk_qspi_psram_enter_quad_mode9qspi_id_t"></a> <a id="_CPPv229bk_qspi_psram_enter_quad_mode9qspi_id_t"></a> <a id="bk_qspi_psram_enter_quad_mode__qspi_id_t"></a> <a id="qspi__psram_8h_1a82473e78e7d68aa0fce4401e3af55c33"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_enter\_quad\_mode([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram enter quad mode.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv428bk_qspi_psram_exit_quad_mode9qspi_id_t"></a>

<a id="_CPPv328bk_qspi_psram_exit_quad_mode9qspi_id_t"></a> <a id="_CPPv228bk_qspi_psram_exit_quad_mode9qspi_id_t"></a> <a id="bk_qspi_psram_exit_quad_mode__qspi_id_t"></a> <a id="qspi__psram_8h_1a785c8b984f913184ba752c6ea03a11b1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_exit\_quad\_mode([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram exit quad mode.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv424bk_qspi_psram_quad_write9qspi_id_t"></a>

<a id="_CPPv324bk_qspi_psram_quad_write9qspi_id_t"></a> <a id="_CPPv224bk_qspi_psram_quad_write9qspi_id_t"></a> <a id="bk_qspi_psram_quad_write__qspi_id_t"></a> <a id="qspi__psram_8h_1a326c0a17c84668753fca1a0883d3ca90"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_quad\_write([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram init quad write.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv426bk_qspi_psram_single_write9qspi_id_t"></a>

<a id="_CPPv326bk_qspi_psram_single_write9qspi_id_t"></a> <a id="_CPPv226bk_qspi_psram_single_write9qspi_id_t"></a> <a id="bk_qspi_psram_single_write__qspi_id_t"></a> <a id="qspi__psram_8h_1a526f0ea3a13515153e5edac093388572"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_single\_write([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram init single write.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv423bk_qspi_psram_quad_read9qspi_id_t"></a>

<a id="_CPPv323bk_qspi_psram_quad_read9qspi_id_t"></a> <a id="_CPPv223bk_qspi_psram_quad_read9qspi_id_t"></a> <a id="bk_qspi_psram_quad_read__qspi_id_t"></a> <a id="qspi__psram_8h_1a21a7cf0670a478b43915dcc48d3097a1"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_quad\_read([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram init quad read.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv425bk_qspi_psram_single_read9qspi_id_t"></a>

<a id="_CPPv325bk_qspi_psram_single_read9qspi_id_t"></a> <a id="_CPPv225bk_qspi_psram_single_read9qspi_id_t"></a> <a id="bk_qspi_psram_single_read__qspi_id_t"></a> <a id="qspi__psram_8h_1ab211ea40c4a3838f9f399bbf651daba9"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_single\_read([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id)
:   QSPI psram init single read.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv419bk_qspi_psram_write9qspi_id_t8uint32_tPKv8uint32_t"></a>

<a id="_CPPv319bk_qspi_psram_write9qspi_id_t8uint32_tPKv8uint32_t"></a> <a id="_CPPv219bk_qspi_psram_write9qspi_id_t8uint32_tPKv8uint32_t"></a> <a id="bk_qspi_psram_write__qspi_id_t.uint32_t.voidCP.uint32_t"></a> <a id="qspi__psram_8h_1ac3171b26cf87270b2b72862cd61b5e1e"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_write([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t base\_addr, const void \*data, uint32\_t size)
:   QSPI psram write data.

    参数
    :   - **base\_addr** – QSPI write address
        - **data** – QSPI write data
        - **size** – the size of QSPI write data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv418bk_qspi_psram_read9qspi_id_t8uint32_tPv8uint32_t"></a>

<a id="_CPPv318bk_qspi_psram_read9qspi_id_t8uint32_tPv8uint32_t"></a> <a id="_CPPv218bk_qspi_psram_read9qspi_id_t8uint32_tPv8uint32_t"></a> <a id="bk_qspi_psram_read__qspi_id_t.uint32_t.voidP.uint32_t"></a> <a id="qspi__psram_8h_1ae5100b085aad9f1a047620c3f3dea44f"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_qspi\_psram\_read([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, uint32\_t base\_addr, void \*data, uint32\_t size)
:   QSPI psram read data.

    参数
    :   - **base\_addr** – QSPI read address
        - **data** – QSPI read data
        - **size** – the size of QSPI read data

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="qspi-api-typedefs"></a>

## QSPI API Typedefs

<a id="id5"></a>

### Header File

- [qspi\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/qspi_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv413qspi_driver_t"></a>

<a id="_CPPv313qspi_driver_t"></a> <a id="_CPPv213qspi_driver_t"></a> <a id="qspi_driver_t"></a> <a id="structqspi__driver__t"></a> struct qspi\_driver\_t

<a id="_CPPv415qspi_callback_t"></a>

<a id="_CPPv315qspi_callback_t"></a> <a id="_CPPv215qspi_callback_t"></a> <a id="qspi_callback_t"></a> <a id="structqspi__callback__t"></a> struct qspi\_callback\_t

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv410qspi_isr_t"></a>

<a id="_CPPv310qspi_isr_t"></a> <a id="_CPPv210qspi_isr_t"></a> <a id="qspi_isr_t"></a> <a id="qspi__types_8h_1ac9fa06bd88a9b0ee04f1cfdfd131ad09"></a> typedef void (\*qspi\_isr\_t)([qspi\_id\_t](#_CPPv49qspi_id_t "qspi_id_t") id, void \*param)
:   QSPI interrupt service routine.

<a id="id6"></a>

### Header File

- [hal\_qspi\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/driver/hal/hal_qspi_types.h)

<a id="id7"></a>

### Structures

<a id="_CPPv413qspi_config_t"></a>

<a id="_CPPv313qspi_config_t"></a> <a id="_CPPv213qspi_config_t"></a> <a id="qspi_config_t"></a> <a id="structqspi__config__t"></a> struct qspi\_config\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N13qspi_config_t7src_clkE"></a>

    <a id="_CPPv3N13qspi_config_t7src_clkE"></a> <a id="_CPPv2N13qspi_config_t7src_clkE"></a> <a id="qspi_config_t::src_clk__qspi_src_clk_t"></a> <a id="structqspi__config__t_1a3aa215cf6e8cc548a0a37a0891cfd05b"></a> [qspi\_src\_clk\_t](#_CPPv414qspi_src_clk_t "qspi_src_clk_t") src\_clk
    :   QSPI source clock

    <a id="_CPPv4N13qspi_config_t11src_clk_divE"></a>

    <a id="_CPPv3N13qspi_config_t11src_clk_divE"></a> <a id="_CPPv2N13qspi_config_t11src_clk_divE"></a> <a id="qspi_config_t::src_clk_div__uint32_t"></a> <a id="structqspi__config__t_1a302a07bedf7f2f67b95a21914aa1975a"></a> uint32\_t src\_clk\_div
    :   QSPI source clock divide number

    <a id="_CPPv4N13qspi_config_t7clk_divE"></a>

    <a id="_CPPv3N13qspi_config_t7clk_divE"></a> <a id="_CPPv2N13qspi_config_t7clk_divE"></a> <a id="qspi_config_t::clk_div__uint32_t"></a> <a id="structqspi__config__t_1a510229fa3c25b9aef180a6f3fed50326"></a> uint32\_t clk\_div
    :   QSPI controller clock divide number

<a id="_CPPv410qspi_cmd_t"></a>

<a id="_CPPv310qspi_cmd_t"></a> <a id="_CPPv210qspi_cmd_t"></a> <a id="qspi_cmd_t"></a> <a id="structqspi__cmd__t"></a> struct qspi\_cmd\_t
:   <a id="breathe-section-title-public-members"></a>

    Public Members

    <a id="_CPPv4N10qspi_cmd_t9work_modeE"></a>

    <a id="_CPPv3N10qspi_cmd_t9work_modeE"></a> <a id="_CPPv2N10qspi_cmd_t9work_modeE"></a> <a id="qspi_cmd_t::work_mode__qspi_work_mode"></a> <a id="structqspi__cmd__t_1aae51d30661115ef0fd9689a8865a6cd9"></a> [qspi\_work\_mode](#_CPPv414qspi_work_mode "qspi_work_mode") work\_mode
    :   QSPI work mode

    <a id="_CPPv4N10qspi_cmd_t2opE"></a>

    <a id="_CPPv3N10qspi_cmd_t2opE"></a> <a id="_CPPv2N10qspi_cmd_t2opE"></a> <a id="qspi_cmd_t::op__qspi_op_t"></a> <a id="structqspi__cmd__t_1a6cfe20ea2034ef8a47a5dd34820f7935"></a> [qspi\_op\_t](#_CPPv49qspi_op_t "qspi_op_t") op
    :   QSPI operation

    <a id="_CPPv4N10qspi_cmd_t3cmdE"></a>

    <a id="_CPPv3N10qspi_cmd_t3cmdE"></a> <a id="_CPPv2N10qspi_cmd_t3cmdE"></a> <a id="qspi_cmd_t::cmd__uint32_t"></a> <a id="structqspi__cmd__t_1a1aeb3dfb9b280bc8087e2a954896d4df"></a> uint32\_t cmd
    :   QSPI command

    <a id="_CPPv4N10qspi_cmd_t4addrE"></a>

    <a id="_CPPv3N10qspi_cmd_t4addrE"></a> <a id="_CPPv2N10qspi_cmd_t4addrE"></a> <a id="qspi_cmd_t::addr__uint32_t"></a> <a id="structqspi__cmd__t_1a8e15dcd7bbfa62b689f9085a996a90cf"></a> uint32\_t addr
    :   QSPI address

    <a id="_CPPv4N10qspi_cmd_t8addr_lenE"></a>

    <a id="_CPPv3N10qspi_cmd_t8addr_lenE"></a> <a id="_CPPv2N10qspi_cmd_t8addr_lenE"></a> <a id="qspi_cmd_t::addr_len__uint32_t"></a> <a id="structqspi__cmd__t_1a1aaecfd6de5316c49add5bbc79059825"></a> uint32\_t addr\_len
    :   QSPI address length

    <a id="_CPPv4N10qspi_cmd_t14addr_wire_modeE"></a>

    <a id="_CPPv3N10qspi_cmd_t14addr_wire_modeE"></a> <a id="_CPPv2N10qspi_cmd_t14addr_wire_modeE"></a> <a id="qspi_cmd_t::addr_wire_mode__qspi_wire_mode_t"></a> <a id="structqspi__cmd__t_1aaee1b664fa2c7c343f81d1cdb63cbe8c"></a> [qspi\_wire\_mode\_t](#_CPPv416qspi_wire_mode_t "qspi_wire_mode_t") addr\_wire\_mode
    :   QSPI address wire mode

    <a id="_CPPv4N10qspi_cmd_t11dummy_cycleE"></a>

    <a id="_CPPv3N10qspi_cmd_t11dummy_cycleE"></a> <a id="_CPPv2N10qspi_cmd_t11dummy_cycleE"></a> <a id="qspi_cmd_t::dummy_cycle__uint32_t"></a> <a id="structqspi__cmd__t_1aa264a9ff3a0762b9505aab9c71f311e3"></a> uint32\_t dummy\_cycle
    :   QSPI dummy cycle

    <a id="_CPPv4N10qspi_cmd_t10dummy_modeE"></a>

    <a id="_CPPv3N10qspi_cmd_t10dummy_modeE"></a> <a id="_CPPv2N10qspi_cmd_t10dummy_modeE"></a> <a id="qspi_cmd_t::dummy_mode__uint32_t"></a> <a id="structqspi__cmd__t_1afd711fc86e925e7dc9ce0e67e23090e2"></a> uint32\_t dummy\_mode
    :   QSPI dummy mode, means the offset to insert dummy clock

    <a id="_CPPv4N10qspi_cmd_t8data_lenE"></a>

    <a id="_CPPv3N10qspi_cmd_t8data_lenE"></a> <a id="_CPPv2N10qspi_cmd_t8data_lenE"></a> <a id="qspi_cmd_t::data_len__uint32_t"></a> <a id="structqspi__cmd__t_1a65a735d0ce1a5e4b38192f5a549a80cb"></a> uint32\_t data\_len
    :   QSPI data length

    <a id="_CPPv4N10qspi_cmd_t14data_wire_modeE"></a>

    <a id="_CPPv3N10qspi_cmd_t14data_wire_modeE"></a> <a id="_CPPv2N10qspi_cmd_t14data_wire_modeE"></a> <a id="qspi_cmd_t::data_wire_mode__qspi_wire_mode_t"></a> <a id="structqspi__cmd__t_1a4e8d9c4ce3c033b470353553444d4bc5"></a> [qspi\_wire\_mode\_t](#_CPPv416qspi_wire_mode_t "qspi_wire_mode_t") data\_wire\_mode
    :   QSPI data wire mode

    <a id="_CPPv4N10qspi_cmd_t6deviceE"></a>

    <a id="_CPPv3N10qspi_cmd_t6deviceE"></a> <a id="_CPPv2N10qspi_cmd_t6deviceE"></a> <a id="qspi_cmd_t::device__qspi_device_t"></a> <a id="structqspi__cmd__t_1ac331cf031c5e7fc750f0aea28a9adfcf"></a> [qspi\_device\_t](#_CPPv413qspi_device_t "qspi_device_t") device
    :   QSPI slave device

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_QSPI_NOT_INIT"></a>

<a id="hal__qspi__types_8h_1a52c7bd4672700d18661fe66825418826"></a> BK\_ERR\_QSPI\_NOT\_INIT
:   QSPI driver not init

<a id="c.BK_ERR_QSPI_ID_NOT_INIT"></a>

<a id="hal__qspi__types_8h_1a9ec612470938855108407c6a135558a7"></a> BK\_ERR\_QSPI\_ID\_NOT\_INIT
:   QSPI id not init

<a id="c.BK_ERR_QSPI_NAND_PROG_FAIL"></a>

<a id="hal__qspi__types_8h_1a2617122fd05981839d9803155256ec76"></a> BK\_ERR\_QSPI\_NAND\_PROG\_FAIL
:   NAND program status P-FAIL

<a id="c.BK_ERR_QSPI_NAND_ERASE_FAIL"></a>

<a id="hal__qspi__types_8h_1ac58efe6557ef05968699dd14659bdd1c"></a> BK\_ERR\_QSPI\_NAND\_ERASE\_FAIL
:   NAND erase status E-FAIL

<a id="c.BK_ERR_QSPI_NAND_ECC_FAIL"></a>

<a id="hal__qspi__types_8h_1a23588d60ed9d6e3b7a7746fdfa4d04fb"></a> BK\_ERR\_QSPI\_NAND\_ECC\_FAIL
:   NAND on-die ECC uncorrectable

<a id="c.BK_ERR_QSPI_NAND_NO_SPARE"></a>

<a id="hal__qspi__types_8h_1a0e1d24857f29f82eedc8faca28b7f36f"></a> BK\_ERR\_QSPI\_NAND\_NO\_SPARE
:   NAND bad-block spare pool exhausted

<a id="c.QSPI_FIFO_LEN_MAX"></a>

<a id="hal__qspi__types_8h_1a2629bc9d2472a2a95bcd2008310ed609"></a> QSPI\_FIFO\_LEN\_MAX

<a id="id8"></a>

### Type Definitions

<a id="_CPPv411qspi_unit_t"></a>

<a id="_CPPv311qspi_unit_t"></a> <a id="_CPPv211qspi_unit_t"></a> <a id="qspi_unit_t"></a> <a id="hal__qspi__types_8h_1a7929bd69b5e415f85137dd204be94a71"></a> typedef uint8\_t qspi\_unit\_t
:   QSPI uint id

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv49qspi_id_t"></a>

<a id="_CPPv39qspi_id_t"></a> <a id="_CPPv29qspi_id_t"></a> <a id="hal__qspi__types_8h_1ab9f20a764a7da48bb87ffe86c3893d55"></a> enum qspi\_id\_t
:   *Values:*

    <a id="_CPPv4N9qspi_id_t9QSPI_ID_0E"></a>

    <a id="_CPPv3N9qspi_id_t9QSPI_ID_0E"></a> <a id="_CPPv2N9qspi_id_t9QSPI_ID_0E"></a> <a id="hal__qspi__types_8h_1ab9f20a764a7da48bb87ffe86c3893d55ad4023da85ad2994c94f7f0a91e0f1f25"></a> enumerator QSPI\_ID\_0
    :   QSPI id 1

    <a id="_CPPv4N9qspi_id_t11QSPI_ID_MAXE"></a>

    <a id="_CPPv3N9qspi_id_t11QSPI_ID_MAXE"></a> <a id="_CPPv2N9qspi_id_t11QSPI_ID_MAXE"></a> <a id="hal__qspi__types_8h_1ab9f20a764a7da48bb87ffe86c3893d55a5639d9f0646c50576a75f3a2a6856f1b"></a> enumerator QSPI\_ID\_MAX
    :   QSPI id max

<a id="_CPPv49qspi_op_t"></a>

<a id="_CPPv39qspi_op_t"></a> <a id="_CPPv29qspi_op_t"></a> <a id="hal__qspi__types_8h_1a77335dd084359dc56ff4c03e705935af"></a> enum qspi\_op\_t
:   *Values:*

    <a id="_CPPv4N9qspi_op_t9QSPI_READE"></a>

    <a id="_CPPv3N9qspi_op_t9QSPI_READE"></a> <a id="_CPPv2N9qspi_op_t9QSPI_READE"></a> <a id="hal__qspi__types_8h_1a77335dd084359dc56ff4c03e705935afa1a541623e80efa0306dba25c99246554"></a> enumerator QSPI\_READ
    :   QSPI read operation

    <a id="_CPPv4N9qspi_op_t10QSPI_WRITEE"></a>

    <a id="_CPPv3N9qspi_op_t10QSPI_WRITEE"></a> <a id="_CPPv2N9qspi_op_t10QSPI_WRITEE"></a> <a id="hal__qspi__types_8h_1a77335dd084359dc56ff4c03e705935afa720357c63583c4445ed98377a3367429"></a> enumerator QSPI\_WRITE
    :   QSPI write operation

<a id="_CPPv414qspi_src_clk_t"></a>

<a id="_CPPv314qspi_src_clk_t"></a> <a id="_CPPv214qspi_src_clk_t"></a> <a id="hal__qspi__types_8h_1a6c489a246d98b08f4ab77a658110890e"></a> enum qspi\_src\_clk\_t
:   *Values:*

    <a id="_CPPv4N14qspi_src_clk_t14QSPI_SCLK_160ME"></a>

    <a id="_CPPv3N14qspi_src_clk_t14QSPI_SCLK_160ME"></a> <a id="_CPPv2N14qspi_src_clk_t14QSPI_SCLK_160ME"></a> <a id="hal__qspi__types_8h_1a6c489a246d98b08f4ab77a658110890ea805ab9ff065bc95a95b353be56aeb6f7"></a> enumerator QSPI\_SCLK\_160M
    :   QSPI source clock 160M

    <a id="_CPPv4N14qspi_src_clk_t14QSPI_SCLK_240ME"></a>

    <a id="_CPPv3N14qspi_src_clk_t14QSPI_SCLK_240ME"></a> <a id="_CPPv2N14qspi_src_clk_t14QSPI_SCLK_240ME"></a> <a id="hal__qspi__types_8h_1a6c489a246d98b08f4ab77a658110890eaae78dee31ffaa009841a176a6e64d87a"></a> enumerator QSPI\_SCLK\_240M
    :   QSPI source clock 240M

<a id="_CPPv414qspi_work_mode"></a>

<a id="_CPPv314qspi_work_mode"></a> <a id="_CPPv214qspi_work_mode"></a> <a id="hal__qspi__types_8h_1af594a43ae0d66055edb60bb2f3f21860"></a> enum qspi\_work\_mode
:   *Values:*

    <a id="_CPPv4N14qspi_work_mode18MEMORY_MAPPED_MODEE"></a>

    <a id="_CPPv3N14qspi_work_mode18MEMORY_MAPPED_MODEE"></a> <a id="_CPPv2N14qspi_work_mode18MEMORY_MAPPED_MODEE"></a> <a id="hal__qspi__types_8h_1af594a43ae0d66055edb60bb2f3f21860a1fe6aec6e7850cf0c4a3ef3dd638bd25"></a> enumerator MEMORY\_MAPPED\_MODE

    <a id="_CPPv4N14qspi_work_mode13INDIRECT_MODEE"></a>

    <a id="_CPPv3N14qspi_work_mode13INDIRECT_MODEE"></a> <a id="_CPPv2N14qspi_work_mode13INDIRECT_MODEE"></a> <a id="hal__qspi__types_8h_1af594a43ae0d66055edb60bb2f3f21860a28fc42c46d45b9ccc3545dc27b443a71"></a> enumerator INDIRECT\_MODE

<a id="_CPPv416qspi_wire_mode_t"></a>

<a id="_CPPv316qspi_wire_mode_t"></a> <a id="_CPPv216qspi_wire_mode_t"></a> <a id="hal__qspi__types_8h_1a83275aaf0277716df663b7a0c31a77db"></a> enum qspi\_wire\_mode\_t
:   *Values:*

    <a id="_CPPv4N16qspi_wire_mode_t10QSPI_1WIREE"></a>

    <a id="_CPPv3N16qspi_wire_mode_t10QSPI_1WIREE"></a> <a id="_CPPv2N16qspi_wire_mode_t10QSPI_1WIREE"></a> <a id="hal__qspi__types_8h_1a83275aaf0277716df663b7a0c31a77dbaf10bed27cc009230c45ab5959193c91b"></a> enumerator QSPI\_1WIRE
    :   QSPI 1\_wire mode, standard SPI

    <a id="_CPPv4N16qspi_wire_mode_t10QSPI_2WIREE"></a>

    <a id="_CPPv3N16qspi_wire_mode_t10QSPI_2WIREE"></a> <a id="_CPPv2N16qspi_wire_mode_t10QSPI_2WIREE"></a> <a id="hal__qspi__types_8h_1a83275aaf0277716df663b7a0c31a77dba0b75fa2c084a4ed288a318e865aa1434"></a> enumerator QSPI\_2WIRE
    :   QSPI 2\_wire mode, DUAL SPI

    <a id="_CPPv4N16qspi_wire_mode_t10QSPI_4WIREE"></a>

    <a id="_CPPv3N16qspi_wire_mode_t10QSPI_4WIREE"></a> <a id="_CPPv2N16qspi_wire_mode_t10QSPI_4WIREE"></a> <a id="hal__qspi__types_8h_1a83275aaf0277716df663b7a0c31a77dbab3c2b5a4d440864365e75108d7903472"></a> enumerator QSPI\_4WIRE
    :   QSPI 4\_wire mode, QUAD SPI

    <a id="_CPPv4N16qspi_wire_mode_t16QSPI_CMD_DISABLEE"></a>

    <a id="_CPPv3N16qspi_wire_mode_t16QSPI_CMD_DISABLEE"></a> <a id="_CPPv2N16qspi_wire_mode_t16QSPI_CMD_DISABLEE"></a> <a id="hal__qspi__types_8h_1a83275aaf0277716df663b7a0c31a77dba43f3e8cc911d35cdc998d8bf0ce9e554"></a> enumerator QSPI\_CMD\_DISABLE
    :   QSPI command disable flag

<a id="_CPPv413qspi_device_t"></a>

<a id="_CPPv313qspi_device_t"></a> <a id="_CPPv213qspi_device_t"></a> <a id="hal__qspi__types_8h_1adf68dfaac44222be68628b930bf3d921"></a> enum qspi\_device\_t
:   *Values:*

    <a id="_CPPv4N13qspi_device_t10QSPI_PSRAME"></a>

    <a id="_CPPv3N13qspi_device_t10QSPI_PSRAME"></a> <a id="_CPPv2N13qspi_device_t10QSPI_PSRAME"></a> <a id="hal__qspi__types_8h_1adf68dfaac44222be68628b930bf3d921a398947dd2fbea09748280646e621a390"></a> enumerator QSPI\_PSRAM
    :   QSPI PSRAM

    <a id="_CPPv4N13qspi_device_t10QSPI_FLASHE"></a>

    <a id="_CPPv3N13qspi_device_t10QSPI_FLASHE"></a> <a id="_CPPv2N13qspi_device_t10QSPI_FLASHE"></a> <a id="hal__qspi__types_8h_1adf68dfaac44222be68628b930bf3d921a1638f84790eda34f063fbc439f95348a"></a> enumerator QSPI\_FLASH
    :   QSPI FLASH

    <a id="_CPPv4N13qspi_device_t9QSPI_OLEDE"></a>

    <a id="_CPPv3N13qspi_device_t9QSPI_OLEDE"></a> <a id="_CPPv2N13qspi_device_t9QSPI_OLEDE"></a> <a id="hal__qspi__types_8h_1adf68dfaac44222be68628b930bf3d921a9fcd1d7857694043045850f9ad85334f"></a> enumerator QSPI\_OLED
    :   QSPI OLED
