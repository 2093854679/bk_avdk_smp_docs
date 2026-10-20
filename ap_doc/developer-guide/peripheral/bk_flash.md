---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/peripheral/bk_flash.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="flash"></a>

# [FLASH](#id6)

<a id="id1"></a>

目录

- [FLASH](#flash)

  - [FLASH 模块概述](#id2)
  - [FLASH 功能支持情况](#id3)
  - [FLASH 注意事项和限制](#id4)
  - [FLASH 常见问题与调试建议](#id5)

<a id="id2"></a>

## [FLASH 模块概述](#id7)

bk\_flash组件提供片上Flash (on-chip) 数据读取、写入、擦除和内存映射相关的API函数。

备注

外部 Flash (off-chip) 通过 SPI/QSPI 接入时，请参考：

- QSPI 外挂 Flash：[QSPI Flash 使用指南](bk_qspi_flash.md)
- QSPI 控制器：[QSPI 使用指南](bk_qspi.md)

<a id="id3"></a>

## [FLASH 功能支持情况](#id8)

支持的FLASH列表：

不同厂商的Flash芯片在特性和操作方式上存在差异，因此部分型号需要定制化的驱动进行支持。当前的Flash驱动可兼容大多数厂家在24位地址范围内的标准快速读、慢速读操作，以及无需定制命令的二线传输模式（DIO/DOUT）。

对于四线传输模式（QIO/QOUT），驱动已适配以下厂商或型号的 Flash：

- GD
- MXIC
- XTX
- Tsingteng
- Winbond

备注

上述厂商的Flash不是每款都进行了支持，具体支持的Flash根据其Flash ID进行匹配，其通用的功能和配置在 `flash_config_t` 结构体中进行定义。
若需要对新增Flash进行支持，在 `flash_driver.c` 中的 `flash_config[]` 进行追加定义即可。

<a id="id4"></a>

## [FLASH 注意事项和限制](#id9)

- Flash 擦除粒度通常为 4KB。
- 写操作前建议先擦除相关区域，避免擦写失败。
- Flash 操作建议在中断关闭或加锁状态下执行，防止任务抢占引发冲突。
- 多核系统中应保证 Flash 操作互斥访问。由于SDK中已经做了相关的处理，AP核在有操作flash的需求时，会通过mailbox的方式通知CP核去操作。
- 由于每个Flash有固定的大小，所以在操作Flash具体地址前，需要注意地址是否超过实际Flash的大小，尽管函数中做了size和address的检查和保护。
- 默认的SDK中，会对Flash进行分区管理，某些地址分区由于权限限制，会进行读/写/执行进行权限管理。具体可以参考 `partitions_gen.h` 文件中的 `BK_FLASH_PARTITIONS_MAP` 变量。

<a id="id5"></a>

## [FLASH 常见问题与调试建议](#id10)

常见错误码及说明：

- `BK_ERR_FLASH_NOT_INIT (-0x3701)`：Flash 驱动未初始化。
- `BK_ERR_FLASH_ADDR_OUT_OF_RANGE (-0x3702)`：Flash 操作地址非法。
- `BK_ERR_FLASH_PARTITION_NOT_FOUND (-0x3703)`：Flash 分区不存在。
- `BK_ERR_FLASH_WAIT_CB_FULL (-0x3704)`：Flash 回调注册数超过限制。
- `BK_ERR_FLASH_WAIT_CB_NOT_REGISTER (-0x3705)`：未注册的回调被尝试注销。

Flash ID 不识别
\- Flash不识别时会出现以下日志信息，不会影响后续的启动，但是Flash的操作后续都会以2-wire的方式进行操作。

```
flash:E(0):This flash is not identified, choose default config
```

- 此时需要确认Flash的 chip ID 以及相关配置是否在 \`\` flash\_config\[\] \`\` 变量中，同时确认代码是否为库上最新版本。

Flash 地址写入失败的可能原因
\- 确认写入地址是否在合法范围内。

- 确认写入地址是否在不可写分区内，对比 `bk_flash_partitions` 变量中的地址信息以及权限位。

Flash写入速率慢的情况
\- 确认初始化中的日志是否按照已有的Flash ID进行初始化，否则可能后续读写操作都是按照2-wire的方式

- 单次写入时间不长，但整体写入慢。建议合并多次写操作，尽量减少 \`\` bk\_flash\_write\_bytes() \`\` 调用次数
- 若写入速率不稳定，可能存在写入过程中被高优先级任务打断，会导致写入过程分段，整体变慢。

使用BKFIL烧写Flash失败
\- 确保BKFIL使用最新版本
