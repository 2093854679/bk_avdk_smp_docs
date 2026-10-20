---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/wifi/bk_wifi_multimedia.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="armino-wi-fi"></a>

# **Armino Wi-Fi音视频传输使用指南**

<a id="id1"></a>

## **概述**

音视频传输需要保证传输信息的实时性、完整性，当音视频数据流使用Wi-Fi传输时，为了保证传输质量，ARMINO SDK对该场景做了特定优化，本章节介绍Wi-Fi音视频传输相关接口及使用指南。

<a id="id2"></a>

## **接口介绍**

Wi-Fi音视频传输相关接口主要有如下两类：

> - 开启/查询Wi-Fi音视频传输策略接口

```
bk_err_t bk_wifi_set_wifi_media_mode(bool flag);
bk_err_t bk_wifi_get_wifi_media_mode_config(bool *flag);
```

调用 bk\_wifi\_set\_wifi\_media\_mode()接口开启Wi-Fi音视频传输策略，调用bk\_wifi\_get\_wifi\_media\_mode\_config()接口查询该策略是否配置生效。

> - 开启/查询音视频传输抗干扰接口

```
bk_err_t bk_wifi_set_video_quality(uint8_t quality);
bk_err_t bk_wifi_get_video_quality_config(uint8_t *quality);
```

调用bk\_wifi\_set\_video\_quality()接口开启音视频传输抗干扰性选择，以适应复杂环境的音视频流畅性。调用bk\_wifi\_get\_video\_quality\_config()接口查询该策略是否生效。

抗干扰性接口相关宏定义如下表所示：

| **宏定义** | **描述** |
| --- | --- |
| WIFI\_VIDEO\_QUALITY\_FD | video quality choose Fluent definition(FD) |
| WIFI\_VIDEO\_QUALITY\_SD | video quality choose Standard definition(SD) |
| WIFI\_VIDEO\_QUALITY\_HD | video quality choose High definition(HD) |

<a id="id3"></a>

### **接口使用**

使用Wi-Fi音视频功能时，请在音视频初始化时，Wi-Fi连接之前调用音视频传输策略接口：

> bk\_err\_t bk\_wifi\_set\_wifi\_media\_mode(bool flag);

该接口是优化音视频传输信息的实时性，完整性的必选项，默认配置为不使用该策略。
如果在开启音视频前调用了上述接口，请在关闭Wi-Fi音视频之后调用上述接口配置为：

> bk\_wifi\_set\_wifi\_media\_mode(false);

重要

*若在关闭时未配置上述模式会影响Wi-Fi功耗*

如果音视频运行环境相当复杂，可以在配置音视频传输策略接口的同时选择配置音视频传输抗干扰接口：

> bk\_err\_t bk\_wifi\_set\_video\_quality(uint8\_t quality);

该接口为Wi-Fi音视频可选项，有三个挡位可选择：

> - 流畅(FD): 该挡位有较强的抗干扰能力，可以在较复杂环境下保证音视频的稳定传输；
> - 标准(SD): 该挡位在相对干净环境下可以稳定传输，在相对复杂环境下音视频有轻微卡顿；
> - 高清(HD): 该挡位优先保证高带宽音视频传输，适用于较干净的环境，复杂环境下音视频有卡顿现象；

建议根据产品使用环境选择合适的挡位以保证音视频传输的流畅性和稳定性。
如果在开启音视频前调用了上述接口，请在关闭Wi-Fi音视频之后调用上述接口配置为：

> bk\_wifi\_set\_video\_quality(WIFI\_VIDEO\_QUALITY\_HD);

已确保ARMINO SDK 切换到其它功能模式时不影响其策略性传输，默认情况下为高清(HD)挡位；

重要

*音视频传输抗干扰接口是基于Wi-Fi音视频传输策略接口生效的，单独调用音视频传输抗干扰接口配置不生效。*

<a id="id4"></a>

### **参考链接**

> > Wi-Fi 音视频传输具体API接口介绍说明请参阅如下链接：
>
> - `bk_wifi_set_wifi_media_mode()`
> - `bk_wifi_set_video_quality()`
> - `bk_wifi_get_video_quality_config()`
> - `bk_wifi_get_wifi_media_mode_config()`
