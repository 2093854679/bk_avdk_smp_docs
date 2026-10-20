---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/api-reference/peripheral/bk_usb.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="usb"></a>

# USB

<a id="usb-api-status"></a>

## USB API Status

| API | BK7259\_AP |
| --- | --- |
| [`bk_usb_driver_init()`](#_CPPv418bk_usb_driver_initv "bk_usb_driver_init") | Y |
| [`bk_usb_driver_deinit()`](#_CPPv420bk_usb_driver_deinitv "bk_usb_driver_deinit") | Y |
| [`bk_usb_power_ops()`](#_CPPv416bk_usb_power_ops8uint32_tb "bk_usb_power_ops") | Y |
| [`bk_usb_open()`](#_CPPv411bk_usb_open8uint32_t "bk_usb_open") | Y |
| [`bk_usb_close()`](#_CPPv412bk_usb_closev "bk_usb_close") | Y |

<a id="usb-port-number"></a>

## USB Port Number

| Capability | BK7259\_AP |
| --- | --- |
| Port Number | 1 |

<a id="usb-pin-and-gpio-map"></a>

## USB Pin and GPIO Map

| USB Pin | BK7259\_AP |
| --- | --- |
| USB power | 28 |

<a id="usb-api-reference"></a>

## USB API Reference

<a id="header-file"></a>

### Header File

- [usb.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/usb.h)

<a id="functions"></a>

### Functions

<a id="_CPPv418bk_usb_driver_initv"></a>

<a id="_CPPv318bk_usb_driver_initv"></a> <a id="_CPPv218bk_usb_driver_initv"></a> <a id="bk_usb_driver_init__void"></a> <a id="usb_8h_1a61ee930ba0a949d90286534c11675ede"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_usb\_driver\_init(void)
:   USB Driver initialization.

    Register the adaptation layer and pass the function pointers used by the closed source library. Register the current USB Class type to be supported, and it can be uninstalled and reinitialized during execution. But be sure to do so before calling other interfaces.

    - Configure Interrupt handling function registration
    - Configure Class Driver Registration

    This API should be called before any other USB APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv420bk_usb_driver_deinitv"></a>

<a id="_CPPv320bk_usb_driver_deinitv"></a> <a id="_CPPv220bk_usb_driver_deinitv"></a> <a id="bk_usb_driver_deinit__void"></a> <a id="usb_8h_1a345ce9b732b59145b01fb92641d975ce"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_usb\_driver\_deinit(void)
:   USB Driver uninstallation.

    Turn off the USB main interrupt switch Unregister Total Interrupt Handling Function Unregistered Class Driver

    This API should be called after any other USB APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv416bk_usb_power_ops8uint32_tb"></a>

<a id="_CPPv316bk_usb_power_ops8uint32_tb"></a> <a id="_CPPv216bk_usb_power_ops8uint32_tb"></a> <a id="bk_usb_power_ops__uint32_t.b"></a> <a id="usb_8h_1a74ba405168673ef5fdf9a2611944bd6b"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_usb\_power\_ops(uint32\_t gpio\_id, bool ops)
:   Pin controlled USB Vbus.

    This API controls VBUS for USB:

    - Determine whether to output voltage through the high and low levels of a GPIO output parameter: gpio\_id Select the corresponding pin number ops Choose to power on or off
    - Configure whether USB is power on

    When the fusion device is working, if there is a device voting for use, it cannot be directly turned off.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv411bk_usb_open8uint32_t"></a>

<a id="_CPPv311bk_usb_open8uint32_t"></a> <a id="_CPPv211bk_usb_open8uint32_t"></a> <a id="bk_usb_open__uint32_t"></a> <a id="usb_8h_1a9ff1ed19438e52293dd1fdd3bf3e8fbd"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_usb\_open(uint32\_t usb\_mode)
:   open the USB

    This API configure the resoure common to USB:

    - Select the identity as host or slave parameter: usb\_mode USB\_HOST\_MODE \= 0 USB\_DEVICE\_MODE \= 1
    - Configure USB common clock
    - Configure USB common registers

    This API should be called before any other USB APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv412bk_usb_closev"></a>

<a id="_CPPv312bk_usb_closev"></a> <a id="_CPPv212bk_usb_closev"></a> <a id="bk_usb_close__void"></a> <a id="usb_8h_1a84d007b8ce2c6c1c07312e5777bb8948"></a> [bk\_err\_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk\_usb\_close(void)
:   close the USB

    This API release USB resources:

    - Restore register
    - Turn off the power and clock

    This API should be called after any other USB APIs.

    返回
    :   - BK\_OK: succeed
        - others: other errors.

<a id="_CPPv432bk_usb_get_device_connect_statusv"></a>

<a id="_CPPv332bk_usb_get_device_connect_statusv"></a> <a id="_CPPv232bk_usb_get_device_connect_statusv"></a> <a id="bk_usb_get_device_connect_status__void"></a> <a id="usb_8h_1ae4bee4e0e4f3af5fbee8b15fec1f8d5f"></a> bool bk\_usb\_get\_device\_connect\_status(void)
:   Obtain whether there is currently a device connection.

    返回
    :   - TRUE: connect
        - FALSE: disconnect

<a id="usb-api-typedefs"></a>

## USB API Typedefs

<a id="id1"></a>

### Header File

- [usb\_types.h](https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/_header_files/include/components/usb_types.h)

<a id="structures"></a>

### Structures

<a id="_CPPv423usb_device_descriptor_t"></a>

<a id="_CPPv323usb_device_descriptor_t"></a> <a id="_CPPv223usb_device_descriptor_t"></a> <a id="usb_device_descriptor_t"></a> <a id="structusb__device__descriptor__t"></a> struct usb\_device\_descriptor\_t

<a id="_CPPv430usb_configuration_descriptor_t"></a>

<a id="_CPPv330usb_configuration_descriptor_t"></a> <a id="_CPPv230usb_configuration_descriptor_t"></a> <a id="usb_configuration_descriptor_t"></a> <a id="structusb__configuration__descriptor__t"></a> struct usb\_configuration\_descriptor\_t

<a id="_CPPv438usb_interface_association_descriptor_t"></a>

<a id="_CPPv338usb_interface_association_descriptor_t"></a> <a id="_CPPv238usb_interface_association_descriptor_t"></a> <a id="usb_interface_association_descriptor_t"></a> <a id="structusb__interface__association__descriptor__t"></a> struct usb\_interface\_association\_descriptor\_t

<a id="_CPPv426usb_interface_descriptor_t"></a>

<a id="_CPPv326usb_interface_descriptor_t"></a> <a id="_CPPv226usb_interface_descriptor_t"></a> <a id="usb_interface_descriptor_t"></a> <a id="structusb__interface__descriptor__t"></a> struct usb\_interface\_descriptor\_t

<a id="_CPPv439usb_audio_endpoint_general_descriptor_t"></a>

<a id="_CPPv339usb_audio_endpoint_general_descriptor_t"></a> <a id="_CPPv239usb_audio_endpoint_general_descriptor_t"></a> <a id="usb_audio_endpoint_general_descriptor_t"></a> <a id="structusb__audio__endpoint__general__descriptor__t"></a> struct usb\_audio\_endpoint\_general\_descriptor\_t

<a id="_CPPv428s_bk_usb_endpoint_descriptor"></a>

<a id="_CPPv328s_bk_usb_endpoint_descriptor"></a> <a id="_CPPv228s_bk_usb_endpoint_descriptor"></a> <a id="s_bk_usb_endpoint_descriptor"></a> <a id="structs__bk__usb__endpoint__descriptor"></a> struct s\_bk\_usb\_endpoint\_descriptor

<a id="_CPPv419bk_uvc_format_index"></a>

<a id="_CPPv319bk_uvc_format_index"></a> <a id="_CPPv219bk_uvc_format_index"></a> <a id="bk_uvc_format_index"></a> <a id="structbk__uvc__format__index"></a> struct bk\_uvc\_format\_index

<a id="_CPPv412bk_uvc_frame"></a>

<a id="_CPPv312bk_uvc_frame"></a> <a id="_CPPv212bk_uvc_frame"></a> <a id="bk_uvc_frame"></a> <a id="structbk__uvc__frame"></a> struct bk\_uvc\_frame

<a id="_CPPv416bk_uvc_all_frame"></a>

<a id="_CPPv316bk_uvc_all_frame"></a> <a id="_CPPv216bk_uvc_all_frame"></a> <a id="bk_uvc_all_frame"></a> <a id="structbk__uvc__all__frame"></a> struct bk\_uvc\_all\_frame

<a id="_CPPv426bk_uvc_device_brief_info_t"></a>

<a id="_CPPv326bk_uvc_device_brief_info_t"></a> <a id="_CPPv226bk_uvc_device_brief_info_t"></a> <a id="bk_uvc_device_brief_info_t"></a> <a id="structbk__uvc__device__brief__info__t"></a> struct bk\_uvc\_device\_brief\_info\_t

<a id="_CPPv415bk_uvc_config_t"></a>

<a id="_CPPv315bk_uvc_config_t"></a> <a id="_CPPv215bk_uvc_config_t"></a> <a id="bk_uvc_config_t"></a> <a id="structbk__uvc__config__t"></a> struct bk\_uvc\_config\_t

<a id="_CPPv414audio_packet_t"></a>

<a id="_CPPv314audio_packet_t"></a> <a id="_CPPv214audio_packet_t"></a> <a id="audio_packet_t"></a> <a id="structaudio__packet__t"></a> struct audio\_packet\_t

<a id="_CPPv422audio_packet_control_t"></a>

<a id="_CPPv322audio_packet_control_t"></a> <a id="_CPPv222audio_packet_control_t"></a> <a id="audio_packet_control_t"></a> <a id="structaudio__packet__control__t"></a> struct audio\_packet\_control\_t

<a id="_CPPv420bk_uac_ring_buffer_t"></a>

<a id="_CPPv320bk_uac_ring_buffer_t"></a> <a id="_CPPv220bk_uac_ring_buffer_t"></a> <a id="bk_uac_ring_buffer_t"></a> <a id="structbk__uac__ring__buffer__t"></a> struct bk\_uac\_ring\_buffer\_t

<a id="_CPPv426bk_uac_device_brief_info_t"></a>

<a id="_CPPv326bk_uac_device_brief_info_t"></a> <a id="_CPPv226bk_uac_device_brief_info_t"></a> <a id="bk_uac_device_brief_info_t"></a> <a id="structbk__uac__device__brief__info__t"></a> struct bk\_uac\_device\_brief\_info\_t

<a id="_CPPv419bk_uac_mic_config_t"></a>

<a id="_CPPv319bk_uac_mic_config_t"></a> <a id="_CPPv219bk_uac_mic_config_t"></a> <a id="bk_uac_mic_config_t"></a> <a id="structbk__uac__mic__config__t"></a> struct bk\_uac\_mic\_config\_t

<a id="_CPPv419bk_uac_spk_config_t"></a>

<a id="_CPPv319bk_uac_spk_config_t"></a> <a id="_CPPv219bk_uac_spk_config_t"></a> <a id="bk_uac_spk_config_t"></a> <a id="structbk__uac__spk__config__t"></a> struct bk\_uac\_spk\_config\_t

<a id="_CPPv415bk_uac_config_t"></a>

<a id="_CPPv315bk_uac_config_t"></a> <a id="_CPPv215bk_uac_config_t"></a> <a id="bk_uac_config_t"></a> <a id="structbk__uac__config__t"></a> struct bk\_uac\_config\_t

<a id="_CPPv423bk_uvc_uac_app_callback"></a>

<a id="_CPPv323bk_uvc_uac_app_callback"></a> <a id="_CPPv223bk_uvc_uac_app_callback"></a> <a id="bk_uvc_uac_app_callback"></a> <a id="structbk__uvc__uac__app__callback"></a> struct bk\_uvc\_uac\_app\_callback

<a id="_CPPv420s_usb_device_request"></a>

<a id="_CPPv320s_usb_device_request"></a> <a id="_CPPv220s_usb_device_request"></a> <a id="s_usb_device_request"></a> <a id="structs__usb__device__request"></a> struct s\_usb\_device\_request

<a id="_CPPv426s_usb_transfer_buffer_info"></a>

<a id="_CPPv326s_usb_transfer_buffer_info"></a> <a id="_CPPv226s_usb_transfer_buffer_info"></a> <a id="s_usb_transfer_buffer_info"></a> <a id="structs__usb__transfer__buffer__info"></a> struct s\_usb\_transfer\_buffer\_info

<a id="_CPPv420bk_usb_hub_port_info"></a>

<a id="_CPPv320bk_usb_hub_port_info"></a> <a id="_CPPv220bk_usb_hub_port_info"></a> <a id="bk_usb_hub_port_info"></a> <a id="structbk__usb__hub__port__info"></a> struct bk\_usb\_hub\_port\_info

<a id="_CPPv412usb_hub_pipe"></a>

<a id="_CPPv312usb_hub_pipe"></a> <a id="_CPPv212usb_hub_pipe"></a> <a id="usb_hub_pipe"></a> <a id="structusb__hub__pipe"></a> struct usb\_hub\_pipe

<a id="macros"></a>

### Macros

<a id="c.BK_ERR_USB_NOT_POWER"></a>

<a id="usb__types_8h_1ae342dc30db10f42691e3412446c953e0"></a> BK\_ERR\_USB\_NOT\_POWER
:   USB vbus poweron, etc

<a id="c.BK_ERR_USB_NOT_OPEN"></a>

<a id="usb__types_8h_1acf7f4df0a4092f3bcbd726024fd5c1d2"></a> BK\_ERR\_USB\_NOT\_OPEN
:   USB dose not turn on clock and power, etc

<a id="c.BK_ERR_USB_NOT_CLOSE"></a>

<a id="usb__types_8h_1ac555acef69b5a00363983dd332031680"></a> BK\_ERR\_USB\_NOT\_CLOSE
:   USB dose not turn off clock and power, etc

<a id="c.BK_ERR_USB_NOT_CONNECT"></a>

<a id="usb__types_8h_1ab046162f499d3e34e9e783c752e57c0a"></a> BK\_ERR\_USB\_NOT\_CONNECT
:   USB device not connected

<a id="c.BK_ERR_USB_OPERATION_NULL_POINTER"></a>

<a id="usb__types_8h_1a8fb925e2e8d31d318e5c8fe4559a3092"></a> BK\_ERR\_USB\_OPERATION\_NULL\_POINTER
:   USB Operated with null pointer

<a id="c.BK_ERR_USB_UVC_NOT_START"></a>

<a id="usb__types_8h_1aa4373075c1c27d8778d9e6356da23600"></a> BK\_ERR\_USB\_UVC\_NOT\_START
:   UVC Transfer not started

<a id="c.BK_ERR_USB_UVC_NOT_STOP"></a>

<a id="usb__types_8h_1a14183723df05bacd705f7d393b2d24a7"></a> BK\_ERR\_USB\_UVC\_NOT\_STOP
:   UVC Transfer not stopped

<a id="c.BK_ERR_USB_UVC_NOT_PAUSE"></a>

<a id="usb__types_8h_1aa3f2bf77aea12db3dafb53b13e14dc6b"></a> BK\_ERR\_USB\_UVC\_NOT\_PAUSE
:   UVC Transfer not paused

<a id="c.BK_ERR_USB_UVC_GET_PARAMETER_FAILED"></a>

<a id="usb__types_8h_1a9cea19f1d1c7d63469262125ff9ac7ba"></a> BK\_ERR\_USB\_UVC\_GET\_PARAMETER\_FAILED
:   UVC The command to obtain parameters did not respond

<a id="c.BK_ERR_USB_UVC_SET_PARAMETER_FAILED"></a>

<a id="usb__types_8h_1a550b3b9c80aec730b554bf0d99244ca8"></a> BK\_ERR\_USB\_UVC\_SET\_PARAMETER\_FAILED
:   UVC Configuration parameter command did not respond

<a id="c.BK_ERR_USB_UVC_SET_INTERFACE_FAILED"></a>

<a id="usb__types_8h_1a774ff87f04c7594700bf3d42c3cdae8c"></a> BK\_ERR\_USB\_UVC\_SET\_INTERFACE\_FAILED
:   UVC The set port command did not respond

<a id="c.BK_ERR_USB_UVC_NOSUPPORT_ATTRIBUTE"></a>

<a id="usb__types_8h_1a5b80b32ba4d5608015fec289d8b2fad4"></a> BK\_ERR\_USB\_UVC\_NOSUPPORT\_ATTRIBUTE
:   UVC The attribute configuration is not supported

<a id="c.BK_ERR_USB_UAC_NOT_START"></a>

<a id="usb__types_8h_1a91c239b528c260cb385bfb3f940a7e44"></a> BK\_ERR\_USB\_UAC\_NOT\_START
:   UAC Transfer not started

<a id="c.BK_ERR_USB_UAC_NOT_STOP"></a>

<a id="usb__types_8h_1aa3a4ffd1582f2cf354a312efaf967137"></a> BK\_ERR\_USB\_UAC\_NOT\_STOP
:   UAC Transfer not stopped

<a id="c.BK_ERR_USB_UAC_NOT_PAUSE"></a>

<a id="usb__types_8h_1a89f3e52eef2a7c02e3d9d22bee4bae44"></a> BK\_ERR\_USB\_UAC\_NOT\_PAUSE
:   UAC Transfer not paused

<a id="c.BK_ERR_USB_UAC_GET_PARAMETER_FAILED"></a>

<a id="usb__types_8h_1a94e6af71e65b2e4badfb0e7e1f75294e"></a> BK\_ERR\_USB\_UAC\_GET\_PARAMETER\_FAILED
:   UAC The command to obtain parameters did not respond

<a id="c.BK_ERR_USB_UAC_SET_PARAMETER_FAILED"></a>

<a id="usb__types_8h_1afc8ee34ebacbc925f250640fae384620"></a> BK\_ERR\_USB\_UAC\_SET\_PARAMETER\_FAILED
:   UAC Configuration parameter command did not respond

<a id="c.BK_ERR_USB_UAC_SET_INTERFACE_FAILED"></a>

<a id="usb__types_8h_1a94a6d8a0a36fb567f2b88967fb2948a4"></a> BK\_ERR\_USB\_UAC\_SET\_INTERFACE\_FAILED
:   UAC The set port command did not respond

<a id="c.BK_ERR_USB_UAC_NOSUPPORT_ATTRIBUTE"></a>

<a id="usb__types_8h_1a70b134093038a924d9128a285bdb4588"></a> BK\_ERR\_USB\_UAC\_NOSUPPORT\_ATTRIBUTE
:   UAC The attribute configuration is not supported

<a id="c.BK_USB_ENDPOINT_XFERTYPE_MASK"></a>

<a id="usb__types_8h_1aa6777a6aa0333f1bc42fa87ab7c8b82d"></a> BK\_USB\_ENDPOINT\_XFERTYPE\_MASK

<a id="type-definitions"></a>

### Type Definitions

<a id="_CPPv419control_irpcomplete"></a>

<a id="_CPPv319control_irpcomplete"></a> <a id="_CPPv219control_irpcomplete"></a> <a id="control_irpcomplete"></a> <a id="usb__types_8h_1a1f5ff6dbe882f0a33c26273375c925b4"></a> typedef void (\*control\_irpcomplete)(void\*, void\*)

<a id="_CPPv432usbh_hub_connect_disconnect_cb_t"></a>

<a id="_CPPv332usbh_hub_connect_disconnect_cb_t"></a> <a id="_CPPv232usbh_hub_connect_disconnect_cb_t"></a> <a id="usbh_hub_connect_disconnect_cb_t"></a> <a id="usb__types_8h_1a4cc5dc6350f782efdf64077ec355b384"></a> typedef void (\*usbh\_hub\_connect\_disconnect\_cb\_t)([bk\_usb\_hub\_port\_info](#_CPPv420bk_usb_hub_port_info "bk_usb_hub_port_info") \*port\_info, void \*arg)

<a id="enumerations"></a>

### Enumerations

<a id="_CPPv410E_USB_MODE"></a>

<a id="_CPPv310E_USB_MODE"></a> <a id="_CPPv210E_USB_MODE"></a> <a id="usb__types_8h_1ab0d6996efe8639524a1d4fabab3c5cdd"></a> enum E\_USB\_MODE
:   *Values:*

    <a id="_CPPv4N10E_USB_MODE13USB_HOST_MODEE"></a>

    <a id="_CPPv3N10E_USB_MODE13USB_HOST_MODEE"></a> <a id="_CPPv2N10E_USB_MODE13USB_HOST_MODEE"></a> <a id="usb__types_8h_1ab0d6996efe8639524a1d4fabab3c5cdda142f736df9dbdc48900865328d62ced4"></a> enumerator USB\_HOST\_MODE

    <a id="_CPPv4N10E_USB_MODE15USB_DEVICE_MODEE"></a>

    <a id="_CPPv3N10E_USB_MODE15USB_DEVICE_MODEE"></a> <a id="_CPPv2N10E_USB_MODE15USB_DEVICE_MODEE"></a> <a id="usb__types_8h_1ab0d6996efe8639524a1d4fabab3c5cddaeeaed6848b639f7608b4a3df5b7256a3"></a> enumerator USB\_DEVICE\_MODE

<a id="_CPPv423E_USB_CONNECTION_STATUS"></a>

<a id="_CPPv323E_USB_CONNECTION_STATUS"></a> <a id="_CPPv223E_USB_CONNECTION_STATUS"></a> <a id="usb__types_8h_1ae328ddc4897101d0a3fe851aef045d29"></a> enum E\_USB\_CONNECTION\_STATUS
:   *Values:*

    <a id="_CPPv4N23E_USB_CONNECTION_STATUS21USB_DEVICE_DISCONNECTE"></a>

    <a id="_CPPv3N23E_USB_CONNECTION_STATUS21USB_DEVICE_DISCONNECTE"></a> <a id="_CPPv2N23E_USB_CONNECTION_STATUS21USB_DEVICE_DISCONNECTE"></a> <a id="usb__types_8h_1ae328ddc4897101d0a3fe851aef045d29a1f2bbbe5ed3d5d4f8ce50a1a4795d814"></a> enumerator USB\_DEVICE\_DISCONNECT

    <a id="_CPPv4N23E_USB_CONNECTION_STATUS18USB_DEVICE_CONNECTE"></a>

    <a id="_CPPv3N23E_USB_CONNECTION_STATUS18USB_DEVICE_CONNECTE"></a> <a id="_CPPv2N23E_USB_CONNECTION_STATUS18USB_DEVICE_CONNECTE"></a> <a id="usb__types_8h_1ae328ddc4897101d0a3fe851aef045d29a7e8bcc465dab897c0a2097c71b67a677"></a> enumerator USB\_DEVICE\_CONNECT

<a id="_CPPv415E_FRAME_RATE_ID"></a>

<a id="_CPPv315E_FRAME_RATE_ID"></a> <a id="_CPPv215E_FRAME_RATE_ID"></a> <a id="usb__types_8h_1a960101fe35e0c5ded720bf9ff124749c"></a> enum E\_FRAME\_RATE\_ID
:   *Values:*

    <a id="_CPPv4N15E_FRAME_RATE_ID6FPS_60E"></a>

    <a id="_CPPv3N15E_FRAME_RATE_ID6FPS_60E"></a> <a id="_CPPv2N15E_FRAME_RATE_ID6FPS_60E"></a> <a id="usb__types_8h_1a960101fe35e0c5ded720bf9ff124749ca4e9e16d822c672d29d29f3750f97a9e4"></a> enumerator FPS\_60

    <a id="_CPPv4N15E_FRAME_RATE_ID6FPS_30E"></a>

    <a id="_CPPv3N15E_FRAME_RATE_ID6FPS_30E"></a> <a id="_CPPv2N15E_FRAME_RATE_ID6FPS_30E"></a> <a id="usb__types_8h_1a960101fe35e0c5ded720bf9ff124749caf7794f29353c4771e2875068b9efb3f0"></a> enumerator FPS\_30

    <a id="_CPPv4N15E_FRAME_RATE_ID6FPS_25E"></a>

    <a id="_CPPv3N15E_FRAME_RATE_ID6FPS_25E"></a> <a id="_CPPv2N15E_FRAME_RATE_ID6FPS_25E"></a> <a id="usb__types_8h_1a960101fe35e0c5ded720bf9ff124749ca28958ab86fa6dd4be0974ce70782840f"></a> enumerator FPS\_25

    <a id="_CPPv4N15E_FRAME_RATE_ID6FPS_20E"></a>

    <a id="_CPPv3N15E_FRAME_RATE_ID6FPS_20E"></a> <a id="_CPPv2N15E_FRAME_RATE_ID6FPS_20E"></a> <a id="usb__types_8h_1a960101fe35e0c5ded720bf9ff124749ca56d753e189a9e6f8e64c8a84fdb08813"></a> enumerator FPS\_20

    <a id="_CPPv4N15E_FRAME_RATE_ID6FPS_15E"></a>

    <a id="_CPPv3N15E_FRAME_RATE_ID6FPS_15E"></a> <a id="_CPPv2N15E_FRAME_RATE_ID6FPS_15E"></a> <a id="usb__types_8h_1a960101fe35e0c5ded720bf9ff124749cae1d0c7a25ad26139d2dea48cfac471af"></a> enumerator FPS\_15

    <a id="_CPPv4N15E_FRAME_RATE_ID6FPS_10E"></a>

    <a id="_CPPv3N15E_FRAME_RATE_ID6FPS_10E"></a> <a id="_CPPv2N15E_FRAME_RATE_ID6FPS_10E"></a> <a id="usb__types_8h_1a960101fe35e0c5ded720bf9ff124749ca07a0de8b13b66ec6f0294b1cce75eb02"></a> enumerator FPS\_10

    <a id="_CPPv4N15E_FRAME_RATE_ID5FPS_5E"></a>

    <a id="_CPPv3N15E_FRAME_RATE_ID5FPS_5E"></a> <a id="_CPPv2N15E_FRAME_RATE_ID5FPS_5E"></a> <a id="usb__types_8h_1a960101fe35e0c5ded720bf9ff124749ca3fe08a5e6fbf9e328b1253be8294fc53"></a> enumerator FPS\_5

<a id="_CPPv414E_USB_DEVICE_T"></a>

<a id="_CPPv314E_USB_DEVICE_T"></a> <a id="_CPPv214E_USB_DEVICE_T"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbc"></a> enum E\_USB\_DEVICE\_T
:   *Values:*

    <a id="_CPPv4N14E_USB_DEVICE_T14USB_UVC_DEVICEE"></a>

    <a id="_CPPv3N14E_USB_DEVICE_T14USB_UVC_DEVICEE"></a> <a id="_CPPv2N14E_USB_DEVICE_T14USB_UVC_DEVICEE"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbcad8b5bbdbb27b221ef460fd32463358c1"></a> enumerator USB\_UVC\_DEVICE

    <a id="_CPPv4N14E_USB_DEVICE_T19USB_UVC_H26X_DEVICEE"></a>

    <a id="_CPPv3N14E_USB_DEVICE_T19USB_UVC_H26X_DEVICEE"></a> <a id="_CPPv2N14E_USB_DEVICE_T19USB_UVC_H26X_DEVICEE"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbca369deacd1f9ced3475f00225b9990075"></a> enumerator USB\_UVC\_H26X\_DEVICE

    <a id="_CPPv4N14E_USB_DEVICE_T18USB_UAC_MIC_DEVICEE"></a>

    <a id="_CPPv3N14E_USB_DEVICE_T18USB_UAC_MIC_DEVICEE"></a> <a id="_CPPv2N14E_USB_DEVICE_T18USB_UAC_MIC_DEVICEE"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbca91adec9d7b9eabe9c83d275caa1d352d"></a> enumerator USB\_UAC\_MIC\_DEVICE

    <a id="_CPPv4N14E_USB_DEVICE_T22USB_UAC_SPEAKER_DEVICEE"></a>

    <a id="_CPPv3N14E_USB_DEVICE_T22USB_UAC_SPEAKER_DEVICEE"></a> <a id="_CPPv2N14E_USB_DEVICE_T22USB_UAC_SPEAKER_DEVICEE"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbca27e54b919b86a6e9ee4f19b19ab7718c"></a> enumerator USB\_UAC\_SPEAKER\_DEVICE

    <a id="_CPPv4N14E_USB_DEVICE_T14USB_MSD_DEVICEE"></a>

    <a id="_CPPv3N14E_USB_DEVICE_T14USB_MSD_DEVICEE"></a> <a id="_CPPv2N14E_USB_DEVICE_T14USB_MSD_DEVICEE"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbcaeb943a64cbe00d9c0c53baa4bb8da2fa"></a> enumerator USB\_MSD\_DEVICE

    <a id="_CPPv4N14E_USB_DEVICE_T14USB_OTA_DEVICEE"></a>

    <a id="_CPPv3N14E_USB_DEVICE_T14USB_OTA_DEVICEE"></a> <a id="_CPPv2N14E_USB_DEVICE_T14USB_OTA_DEVICEE"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbcad5b425c27c1b0d97bf70665e6708211b"></a> enumerator USB\_OTA\_DEVICE

    <a id="_CPPv4N14E_USB_DEVICE_T21USB_USER_CHECK_DEVICEE"></a>

    <a id="_CPPv3N14E_USB_DEVICE_T21USB_USER_CHECK_DEVICEE"></a> <a id="_CPPv2N14E_USB_DEVICE_T21USB_USER_CHECK_DEVICEE"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbca3babedb04cb05d745a27cc1a00e36334"></a> enumerator USB\_USER\_CHECK\_DEVICE

    <a id="_CPPv4N14E_USB_DEVICE_T14USB_CDC_DEVICEE"></a>

    <a id="_CPPv3N14E_USB_DEVICE_T14USB_CDC_DEVICEE"></a> <a id="_CPPv2N14E_USB_DEVICE_T14USB_CDC_DEVICEE"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbca4249a202d9a21cdf5fa61b6f2a750de0"></a> enumerator USB\_CDC\_DEVICE

    <a id="_CPPv4N14E_USB_DEVICE_T14USB_DEVICE_MAXE"></a>

    <a id="_CPPv3N14E_USB_DEVICE_T14USB_DEVICE_MAXE"></a> <a id="_CPPv2N14E_USB_DEVICE_T14USB_DEVICE_MAXE"></a> <a id="usb__types_8h_1abe4bdd7729b0cfe2767786259fc3bbbcaf7fd9a4c5b6ea3514c9bf85cb7d15592"></a> enumerator USB\_DEVICE\_MAX

<a id="_CPPv430E_USB_ENDPOINT_TRANSFER_MODE_T"></a>

<a id="_CPPv330E_USB_ENDPOINT_TRANSFER_MODE_T"></a> <a id="_CPPv230E_USB_ENDPOINT_TRANSFER_MODE_T"></a> <a id="usb__types_8h_1a8a0494314c57c095f522df510c88006d"></a> enum E\_USB\_ENDPOINT\_TRANSFER\_MODE\_T
:   *Values:*

    <a id="_CPPv4N30E_USB_ENDPOINT_TRANSFER_MODE_T29USB_ENDPOINT_CONTROL_TRANSFERE"></a>

    <a id="_CPPv3N30E_USB_ENDPOINT_TRANSFER_MODE_T29USB_ENDPOINT_CONTROL_TRANSFERE"></a> <a id="_CPPv2N30E_USB_ENDPOINT_TRANSFER_MODE_T29USB_ENDPOINT_CONTROL_TRANSFERE"></a> <a id="usb__types_8h_1a8a0494314c57c095f522df510c88006da7b0946fc6864f8f358768ba8c576952a"></a> enumerator USB\_ENDPOINT\_CONTROL\_TRANSFER

    <a id="_CPPv4N30E_USB_ENDPOINT_TRANSFER_MODE_T27USB_ENDPOINT_ISOCH_TRANSFERE"></a>

    <a id="_CPPv3N30E_USB_ENDPOINT_TRANSFER_MODE_T27USB_ENDPOINT_ISOCH_TRANSFERE"></a> <a id="_CPPv2N30E_USB_ENDPOINT_TRANSFER_MODE_T27USB_ENDPOINT_ISOCH_TRANSFERE"></a> <a id="usb__types_8h_1a8a0494314c57c095f522df510c88006da0a43ea38e01179d4f84fa45ac2c610db"></a> enumerator USB\_ENDPOINT\_ISOCH\_TRANSFER

    <a id="_CPPv4N30E_USB_ENDPOINT_TRANSFER_MODE_T26USB_ENDPOINT_BULK_TRANSFERE"></a>

    <a id="_CPPv3N30E_USB_ENDPOINT_TRANSFER_MODE_T26USB_ENDPOINT_BULK_TRANSFERE"></a> <a id="_CPPv2N30E_USB_ENDPOINT_TRANSFER_MODE_T26USB_ENDPOINT_BULK_TRANSFERE"></a> <a id="usb__types_8h_1a8a0494314c57c095f522df510c88006daba5bf639dea24c882a1c8f51d888f221"></a> enumerator USB\_ENDPOINT\_BULK\_TRANSFER

    <a id="_CPPv4N30E_USB_ENDPOINT_TRANSFER_MODE_T25USB_ENDPOINT_INT_TRANSFERE"></a>

    <a id="_CPPv3N30E_USB_ENDPOINT_TRANSFER_MODE_T25USB_ENDPOINT_INT_TRANSFERE"></a> <a id="_CPPv2N30E_USB_ENDPOINT_TRANSFER_MODE_T25USB_ENDPOINT_INT_TRANSFERE"></a> <a id="usb__types_8h_1a8a0494314c57c095f522df510c88006da6ffee1b8fc6c4496c5b3b0c8e2a36578"></a> enumerator USB\_ENDPOINT\_INT\_TRANSFER

    <a id="_CPPv4N30E_USB_ENDPOINT_TRANSFER_MODE_T29USB_ENDPOINT_INVALID_TRANSFERE"></a>

    <a id="_CPPv3N30E_USB_ENDPOINT_TRANSFER_MODE_T29USB_ENDPOINT_INVALID_TRANSFERE"></a> <a id="_CPPv2N30E_USB_ENDPOINT_TRANSFER_MODE_T29USB_ENDPOINT_INVALID_TRANSFERE"></a> <a id="usb__types_8h_1a8a0494314c57c095f522df510c88006da0646db08831f5641c28408db150e5802"></a> enumerator USB\_ENDPOINT\_INVALID\_TRANSFER

<a id="_CPPv415bk_usb_drv_op_t"></a>

<a id="_CPPv315bk_usb_drv_op_t"></a> <a id="_CPPv215bk_usb_drv_op_t"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0e"></a> enum bk\_usb\_drv\_op\_t
:   *Values:*

    <a id="_CPPv4N15bk_usb_drv_op_t12USB_DRV_IDLEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t12USB_DRV_IDLEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t12USB_DRV_IDLEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eae5b20d8289ea5dc814fa82bc94c7e033"></a> enumerator USB\_DRV\_IDLE

    <a id="_CPPv4N15bk_usb_drv_op_t12USB_DRV_EXITE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t12USB_DRV_EXITE"></a> <a id="_CPPv2N15bk_usb_drv_op_t12USB_DRV_EXITE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea86e0130864a5cace6d4f423b61edadfe"></a> enumerator USB\_DRV\_EXIT

    <a id="_CPPv4N15bk_usb_drv_op_t13USB_POWER_OPSE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t13USB_POWER_OPSE"></a> <a id="_CPPv2N15bk_usb_drv_op_t13USB_POWER_OPSE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eac36767174e367d7713574fb27df6e69f"></a> enumerator USB\_POWER\_OPS

    <a id="_CPPv4N15bk_usb_drv_op_t16USB_DRV_USB_INITE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t16USB_DRV_USB_INITE"></a> <a id="_CPPv2N15bk_usb_drv_op_t16USB_DRV_USB_INITE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea262a1a8798e849366046e7341a02d3ae"></a> enumerator USB\_DRV\_USB\_INIT

    <a id="_CPPv4N15bk_usb_drv_op_t18USB_DRV_USB_DEINITE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t18USB_DRV_USB_DEINITE"></a> <a id="_CPPv2N15bk_usb_drv_op_t18USB_DRV_USB_DEINITE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eac82fae4166924c9a2a147201b2cd4673"></a> enumerator USB\_DRV\_USB\_DEINIT

    <a id="_CPPv4N15bk_usb_drv_op_t19USB_DRV_SET_DEV_USEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t19USB_DRV_SET_DEV_USEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t19USB_DRV_SET_DEV_USEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eae44c2a2e54468f957ab91b1ac0899423"></a> enumerator USB\_DRV\_SET\_DEV\_USE

    <a id="_CPPv4N15bk_usb_drv_op_t16USB_DRV_USB_OPENE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t16USB_DRV_USB_OPENE"></a> <a id="_CPPv2N15bk_usb_drv_op_t16USB_DRV_USB_OPENE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea132d0e5fb266c52756d07411226dc120"></a> enumerator USB\_DRV\_USB\_OPEN

    <a id="_CPPv4N15bk_usb_drv_op_t17USB_DRV_USB_CLOSEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t17USB_DRV_USB_CLOSEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t17USB_DRV_USB_CLOSEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea676de86224337b08c54eb439c849ccb0"></a> enumerator USB\_DRV\_USB\_CLOSE

    <a id="_CPPv4N15bk_usb_drv_op_t22USB_DRV_CONNECT_HANDLEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t22USB_DRV_CONNECT_HANDLEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t22USB_DRV_CONNECT_HANDLEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea0736dce3f774eb08a3eef0a67f249980"></a> enumerator USB\_DRV\_CONNECT\_HANDLE

    <a id="_CPPv4N15bk_usb_drv_op_t25USB_DRV_DISCONNECT_HANDLEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t25USB_DRV_DISCONNECT_HANDLEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t25USB_DRV_DISCONNECT_HANDLEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eab2203fa340722412367f3f7fef117abe"></a> enumerator USB\_DRV\_DISCONNECT\_HANDLE

    <a id="_CPPv4N15bk_usb_drv_op_t30USB_DRV_GET_DEV_CONNECT_STATUSE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t30USB_DRV_GET_DEV_CONNECT_STATUSE"></a> <a id="_CPPv2N15bk_usb_drv_op_t30USB_DRV_GET_DEV_CONNECT_STATUSE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea116249c4fbe45c0e2c1e8c46360e46a3"></a> enumerator USB\_DRV\_GET\_DEV\_CONNECT\_STATUS

    <a id="_CPPv4N15bk_usb_drv_op_t25USB_DRV_CHECK_DEV_SUPPORTE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t25USB_DRV_CHECK_DEV_SUPPORTE"></a> <a id="_CPPv2N15bk_usb_drv_op_t25USB_DRV_CHECK_DEV_SUPPORTE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ead314e493254135c2f2f8db5c6ff56c26"></a> enumerator USB\_DRV\_CHECK\_DEV\_SUPPORT

    <a id="_CPPv4N15bk_usb_drv_op_t24USB_DRV_PRASE_DESCRIPTORE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t24USB_DRV_PRASE_DESCRIPTORE"></a> <a id="_CPPv2N15bk_usb_drv_op_t24USB_DRV_PRASE_DESCRIPTORE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eaa3c809d5ca9b33aa114d80a4fdac370c"></a> enumerator USB\_DRV\_PRASE\_DESCRIPTOR

    <a id="_CPPv4N15bk_usb_drv_op_t26USB_DRV_INIT_CONTROL_TRANSE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t26USB_DRV_INIT_CONTROL_TRANSE"></a> <a id="_CPPv2N15bk_usb_drv_op_t26USB_DRV_INIT_CONTROL_TRANSE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea96ee48b83de0370d4a3736bf9cf6dc02"></a> enumerator USB\_DRV\_INIT\_CONTROL\_TRANS

    <a id="_CPPv4N15bk_usb_drv_op_t28USB_DRV_DEINIT_CONTROL_TRANSE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t28USB_DRV_DEINIT_CONTROL_TRANSE"></a> <a id="_CPPv2N15bk_usb_drv_op_t28USB_DRV_DEINIT_CONTROL_TRANSE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eac1e4560bac31a02553aee9b07029844a"></a> enumerator USB\_DRV\_DEINIT\_CONTROL\_TRANS

    <a id="_CPPv4N15bk_usb_drv_op_t24USB_DRV_CONTROL_TRANSFERE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t24USB_DRV_CONTROL_TRANSFERE"></a> <a id="_CPPv2N15bk_usb_drv_op_t24USB_DRV_CONTROL_TRANSFERE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ead2aa5eff53fe11c17e38a39c6c44db68"></a> enumerator USB\_DRV\_CONTROL\_TRANSFER

    <a id="_CPPv4N15bk_usb_drv_op_t31USB_DRV_UVC_REGISTER_CONNECT_CBE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t31USB_DRV_UVC_REGISTER_CONNECT_CBE"></a> <a id="_CPPv2N15bk_usb_drv_op_t31USB_DRV_UVC_REGISTER_CONNECT_CBE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eaee7ad298b8577dbe050822f565c5cc93"></a> enumerator USB\_DRV\_UVC\_REGISTER\_CONNECT\_CB

    <a id="_CPPv4N15bk_usb_drv_op_t34USB_DRV_UVC_REGISTER_DISCONNECT_CBE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t34USB_DRV_UVC_REGISTER_DISCONNECT_CBE"></a> <a id="_CPPv2N15bk_usb_drv_op_t34USB_DRV_UVC_REGISTER_DISCONNECT_CBE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea18d88db082e9edab446080de59bdfbc5"></a> enumerator USB\_DRV\_UVC\_REGISTER\_DISCONNECT\_CB

    <a id="_CPPv4N15bk_usb_drv_op_t21USB_DRV_UVC_GET_PARAME"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t21USB_DRV_UVC_GET_PARAME"></a> <a id="_CPPv2N15bk_usb_drv_op_t21USB_DRV_UVC_GET_PARAME"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eaaab5adab0bf77f6eecbcdd0efb264161"></a> enumerator USB\_DRV\_UVC\_GET\_PARAM

    <a id="_CPPv4N15bk_usb_drv_op_t21USB_DRV_UVC_SET_PARAME"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t21USB_DRV_UVC_SET_PARAME"></a> <a id="_CPPv2N15bk_usb_drv_op_t21USB_DRV_UVC_SET_PARAME"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eaa0875c556f91ce6da5d13efc5ad314ae"></a> enumerator USB\_DRV\_UVC\_SET\_PARAM

    <a id="_CPPv4N15bk_usb_drv_op_t33USB_DRV_UVC_REGISTER_TRANSFER_OPSE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t33USB_DRV_UVC_REGISTER_TRANSFER_OPSE"></a> <a id="_CPPv2N15bk_usb_drv_op_t33USB_DRV_UVC_REGISTER_TRANSFER_OPSE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eaa772fc1be1c5138d71a2dcc5a6373a85"></a> enumerator USB\_DRV\_UVC\_REGISTER\_TRANSFER\_OPS

    <a id="_CPPv4N15bk_usb_drv_op_t34USB_DRV_UVC_TRANSFER_BUFFER_MALLOCE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t34USB_DRV_UVC_TRANSFER_BUFFER_MALLOCE"></a> <a id="_CPPv2N15bk_usb_drv_op_t34USB_DRV_UVC_TRANSFER_BUFFER_MALLOCE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eaf548c7fc658fe2246d2c73f6d8d856ee"></a> enumerator USB\_DRV\_UVC\_TRANSFER\_BUFFER\_MALLOC

    <a id="_CPPv4N15bk_usb_drv_op_t32USB_DRV_UVC_TRANSFER_BUFFER_PUSHE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t32USB_DRV_UVC_TRANSFER_BUFFER_PUSHE"></a> <a id="_CPPv2N15bk_usb_drv_op_t32USB_DRV_UVC_TRANSFER_BUFFER_PUSHE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eac33d7424b4db3b1f7cb7464326f90952"></a> enumerator USB\_DRV\_UVC\_TRANSFER\_BUFFER\_PUSH

    <a id="_CPPv4N15bk_usb_drv_op_t31USB_DRV_UVC_TRANSFER_BUFFER_POPE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t31USB_DRV_UVC_TRANSFER_BUFFER_POPE"></a> <a id="_CPPv2N15bk_usb_drv_op_t31USB_DRV_UVC_TRANSFER_BUFFER_POPE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea4c7c69726e9d11a556ab83efeef0a0ac"></a> enumerator USB\_DRV\_UVC\_TRANSFER\_BUFFER\_POP

    <a id="_CPPv4N15bk_usb_drv_op_t32USB_DRV_UVC_TRANSFER_BUFFER_FREEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t32USB_DRV_UVC_TRANSFER_BUFFER_FREEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t32USB_DRV_UVC_TRANSFER_BUFFER_FREEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eada915ae1706aa8864981794fe9c7151d"></a> enumerator USB\_DRV\_UVC\_TRANSFER\_BUFFER\_FREE

    <a id="_CPPv4N15bk_usb_drv_op_t23USB_DRV_VIDEO_OPEN_PIPEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t23USB_DRV_VIDEO_OPEN_PIPEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t23USB_DRV_VIDEO_OPEN_PIPEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea10dd300765bf3fb39e2e45dcf488087d"></a> enumerator USB\_DRV\_VIDEO\_OPEN\_PIPE

    <a id="_CPPv4N15bk_usb_drv_op_t24USB_DRV_VIDEO_CLOSE_PIPEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t24USB_DRV_VIDEO_CLOSE_PIPEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t24USB_DRV_VIDEO_CLOSE_PIPEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea9b4d7e6712caac9de3009c0153bafaa2"></a> enumerator USB\_DRV\_VIDEO\_CLOSE\_PIPE

    <a id="_CPPv4N15bk_usb_drv_op_t19USB_DRV_VIDEO_STARTE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t19USB_DRV_VIDEO_STARTE"></a> <a id="_CPPv2N15bk_usb_drv_op_t19USB_DRV_VIDEO_STARTE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eaefc89d8b7edd958b9bf97e8f6571c96c"></a> enumerator USB\_DRV\_VIDEO\_START

    <a id="_CPPv4N15bk_usb_drv_op_t18USB_DRV_VIDEO_STOPE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t18USB_DRV_VIDEO_STOPE"></a> <a id="_CPPv2N15bk_usb_drv_op_t18USB_DRV_VIDEO_STOPE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea614c6891b79e2b082fd16918e86bc08f"></a> enumerator USB\_DRV\_VIDEO\_STOP

    <a id="_CPPv4N15bk_usb_drv_op_t16USB_DRV_VIDEO_RXE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t16USB_DRV_VIDEO_RXE"></a> <a id="_CPPv2N15bk_usb_drv_op_t16USB_DRV_VIDEO_RXE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eafea3e5f310948b0c334d8745796018e5"></a> enumerator USB\_DRV\_VIDEO\_RX

    <a id="_CPPv4N15bk_usb_drv_op_t18USB_DRV_VIDEO_RXEDE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t18USB_DRV_VIDEO_RXEDE"></a> <a id="_CPPv2N15bk_usb_drv_op_t18USB_DRV_VIDEO_RXEDE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eafe626a5ab9415ed343678d7d6d86471d"></a> enumerator USB\_DRV\_VIDEO\_RXED

    <a id="_CPPv4N15bk_usb_drv_op_t31USB_DRV_UAC_REGISTER_CONNECT_CBE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t31USB_DRV_UAC_REGISTER_CONNECT_CBE"></a> <a id="_CPPv2N15bk_usb_drv_op_t31USB_DRV_UAC_REGISTER_CONNECT_CBE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea39c4bb841f6475a4a9f04e4fc69c81af"></a> enumerator USB\_DRV\_UAC\_REGISTER\_CONNECT\_CB

    <a id="_CPPv4N15bk_usb_drv_op_t34USB_DRV_UAC_REGISTER_DISCONNECT_CBE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t34USB_DRV_UAC_REGISTER_DISCONNECT_CBE"></a> <a id="_CPPv2N15bk_usb_drv_op_t34USB_DRV_UAC_REGISTER_DISCONNECT_CBE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea87ba1203d2d62ffa1d344c7a30f108fc"></a> enumerator USB\_DRV\_UAC\_REGISTER\_DISCONNECT\_CB

    <a id="_CPPv4N15bk_usb_drv_op_t21USB_DRV_UAC_GET_PARAME"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t21USB_DRV_UAC_GET_PARAME"></a> <a id="_CPPv2N15bk_usb_drv_op_t21USB_DRV_UAC_GET_PARAME"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea76593c0981e06731324425411be8e541"></a> enumerator USB\_DRV\_UAC\_GET\_PARAM

    <a id="_CPPv4N15bk_usb_drv_op_t21USB_DRV_UAC_SET_PARAME"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t21USB_DRV_UAC_SET_PARAME"></a> <a id="_CPPv2N15bk_usb_drv_op_t21USB_DRV_UAC_SET_PARAME"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eafbef8db5bdc639b5c30d4745527bd22b"></a> enumerator USB\_DRV\_UAC\_SET\_PARAM

    <a id="_CPPv4N15bk_usb_drv_op_t33USB_DRV_UAC_REGISTER_TRANSFER_OPSE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t33USB_DRV_UAC_REGISTER_TRANSFER_OPSE"></a> <a id="_CPPv2N15bk_usb_drv_op_t33USB_DRV_UAC_REGISTER_TRANSFER_OPSE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eae17e7beaeafb058f8edd39638fc49544"></a> enumerator USB\_DRV\_UAC\_REGISTER\_TRANSFER\_OPS

    <a id="_CPPv4N15bk_usb_drv_op_t34USB_DRV_UAC_TRANSFER_BUFFER_MALLOCE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t34USB_DRV_UAC_TRANSFER_BUFFER_MALLOCE"></a> <a id="_CPPv2N15bk_usb_drv_op_t34USB_DRV_UAC_TRANSFER_BUFFER_MALLOCE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea49b6a338e5f988834b8e0724c045fc17"></a> enumerator USB\_DRV\_UAC\_TRANSFER\_BUFFER\_MALLOC

    <a id="_CPPv4N15bk_usb_drv_op_t32USB_DRV_UAC_TRANSFER_BUFFER_PUSHE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t32USB_DRV_UAC_TRANSFER_BUFFER_PUSHE"></a> <a id="_CPPv2N15bk_usb_drv_op_t32USB_DRV_UAC_TRANSFER_BUFFER_PUSHE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea7d57654f8048a478037c2bf76972cd11"></a> enumerator USB\_DRV\_UAC\_TRANSFER\_BUFFER\_PUSH

    <a id="_CPPv4N15bk_usb_drv_op_t31USB_DRV_UAC_TRANSFER_BUFFER_POPE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t31USB_DRV_UAC_TRANSFER_BUFFER_POPE"></a> <a id="_CPPv2N15bk_usb_drv_op_t31USB_DRV_UAC_TRANSFER_BUFFER_POPE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eac7881c7d7611f3b7725a4b371f4cc92b"></a> enumerator USB\_DRV\_UAC\_TRANSFER\_BUFFER\_POP

    <a id="_CPPv4N15bk_usb_drv_op_t32USB_DRV_UAC_TRANSFER_BUFFER_FREEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t32USB_DRV_UAC_TRANSFER_BUFFER_FREEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t32USB_DRV_UAC_TRANSFER_BUFFER_FREEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea92a753611584844d97c753dfdf81fdfa"></a> enumerator USB\_DRV\_UAC\_TRANSFER\_BUFFER\_FREE

    <a id="_CPPv4N15bk_usb_drv_op_t23USB_DRV_AUDIO_OPEN_PIPEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t23USB_DRV_AUDIO_OPEN_PIPEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t23USB_DRV_AUDIO_OPEN_PIPEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eade453d52aaa93be886759fe67c8d63be"></a> enumerator USB\_DRV\_AUDIO\_OPEN\_PIPE

    <a id="_CPPv4N15bk_usb_drv_op_t24USB_DRV_AUDIO_CLOSE_PIPEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t24USB_DRV_AUDIO_CLOSE_PIPEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t24USB_DRV_AUDIO_CLOSE_PIPEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea2f595035141814d06b4e0fe7de6fded2"></a> enumerator USB\_DRV\_AUDIO\_CLOSE\_PIPE

    <a id="_CPPv4N15bk_usb_drv_op_t23USB_DRV_AUDIO_MIC_STARTE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t23USB_DRV_AUDIO_MIC_STARTE"></a> <a id="_CPPv2N15bk_usb_drv_op_t23USB_DRV_AUDIO_MIC_STARTE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea0dee62afe974e289b0e89fddacd292e7"></a> enumerator USB\_DRV\_AUDIO\_MIC\_START

    <a id="_CPPv4N15bk_usb_drv_op_t22USB_DRV_AUDIO_MIC_STOPE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t22USB_DRV_AUDIO_MIC_STOPE"></a> <a id="_CPPv2N15bk_usb_drv_op_t22USB_DRV_AUDIO_MIC_STOPE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea1c80bb403212aa2198d9fffc6c16c293"></a> enumerator USB\_DRV\_AUDIO\_MIC\_STOP

    <a id="_CPPv4N15bk_usb_drv_op_t23USB_DRV_AUDIO_SPK_STARTE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t23USB_DRV_AUDIO_SPK_STARTE"></a> <a id="_CPPv2N15bk_usb_drv_op_t23USB_DRV_AUDIO_SPK_STARTE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea45dd42107c99e005a97d05269bd76a42"></a> enumerator USB\_DRV\_AUDIO\_SPK\_START

    <a id="_CPPv4N15bk_usb_drv_op_t22USB_DRV_AUDIO_SPK_STOPE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t22USB_DRV_AUDIO_SPK_STOPE"></a> <a id="_CPPv2N15bk_usb_drv_op_t22USB_DRV_AUDIO_SPK_STOPE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eaa1a833f62c56f8c97679b4a6c981482b"></a> enumerator USB\_DRV\_AUDIO\_SPK\_STOP

    <a id="_CPPv4N15bk_usb_drv_op_t16USB_DRV_AUDIO_RXE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t16USB_DRV_AUDIO_RXE"></a> <a id="_CPPv2N15bk_usb_drv_op_t16USB_DRV_AUDIO_RXE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea6e18bb87769d4d2b495fd54e9939c437"></a> enumerator USB\_DRV\_AUDIO\_RX

    <a id="_CPPv4N15bk_usb_drv_op_t18USB_DRV_AUDIO_RXEDE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t18USB_DRV_AUDIO_RXEDE"></a> <a id="_CPPv2N15bk_usb_drv_op_t18USB_DRV_AUDIO_RXEDE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea3a0703905f5dd10de863ffc960dd0d9b"></a> enumerator USB\_DRV\_AUDIO\_RXED

    <a id="_CPPv4N15bk_usb_drv_op_t16USB_DRV_AUDIO_TXE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t16USB_DRV_AUDIO_TXE"></a> <a id="_CPPv2N15bk_usb_drv_op_t16USB_DRV_AUDIO_TXE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea9ed23b63be421b5d6bb67232c62b1824"></a> enumerator USB\_DRV\_AUDIO\_TX

    <a id="_CPPv4N15bk_usb_drv_op_t18USB_DRV_AUDIO_TXEDE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t18USB_DRV_AUDIO_TXEDE"></a> <a id="_CPPv2N15bk_usb_drv_op_t18USB_DRV_AUDIO_TXEDE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea0541d9c8ac87913312c1cfc42ee0371b"></a> enumerator USB\_DRV\_AUDIO\_TXED

    <a id="_CPPv4N15bk_usb_drv_op_t39USB_DRV_UVC_TRANSFER_DUAL_BUFFER_MALLOCE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t39USB_DRV_UVC_TRANSFER_DUAL_BUFFER_MALLOCE"></a> <a id="_CPPv2N15bk_usb_drv_op_t39USB_DRV_UVC_TRANSFER_DUAL_BUFFER_MALLOCE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ead8ecd1b3d271f7fa433c637e6e04c9ba"></a> enumerator USB\_DRV\_UVC\_TRANSFER\_DUAL\_BUFFER\_MALLOC

    <a id="_CPPv4N15bk_usb_drv_op_t37USB_DRV_UVC_TRANSFER_DUAL_BUFFER_PUSHE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t37USB_DRV_UVC_TRANSFER_DUAL_BUFFER_PUSHE"></a> <a id="_CPPv2N15bk_usb_drv_op_t37USB_DRV_UVC_TRANSFER_DUAL_BUFFER_PUSHE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea03df6a0cb6b8c1a438ed3f770495a48b"></a> enumerator USB\_DRV\_UVC\_TRANSFER\_DUAL\_BUFFER\_PUSH

    <a id="_CPPv4N15bk_usb_drv_op_t36USB_DRV_UVC_TRANSFER_DUAL_BUFFER_POPE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t36USB_DRV_UVC_TRANSFER_DUAL_BUFFER_POPE"></a> <a id="_CPPv2N15bk_usb_drv_op_t36USB_DRV_UVC_TRANSFER_DUAL_BUFFER_POPE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea3bcbb9451489651842a1db9de7b2c9c6"></a> enumerator USB\_DRV\_UVC\_TRANSFER\_DUAL\_BUFFER\_POP

    <a id="_CPPv4N15bk_usb_drv_op_t37USB_DRV_UVC_TRANSFER_DUAL_BUFFER_FREEE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t37USB_DRV_UVC_TRANSFER_DUAL_BUFFER_FREEE"></a> <a id="_CPPv2N15bk_usb_drv_op_t37USB_DRV_UVC_TRANSFER_DUAL_BUFFER_FREEE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea507414113d22d17a34a7f4b8e6105da4"></a> enumerator USB\_DRV\_UVC\_TRANSFER\_DUAL\_BUFFER\_FREE

    <a id="_CPPv4N15bk_usb_drv_op_t24USB_DRV_VIDEO_DUAL_STARTE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t24USB_DRV_VIDEO_DUAL_STARTE"></a> <a id="_CPPv2N15bk_usb_drv_op_t24USB_DRV_VIDEO_DUAL_STARTE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0eaa217e902d121c32f4b9137abf5e178d2"></a> enumerator USB\_DRV\_VIDEO\_DUAL\_START

    <a id="_CPPv4N15bk_usb_drv_op_t23USB_DRV_VIDEO_DUAL_STOPE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t23USB_DRV_VIDEO_DUAL_STOPE"></a> <a id="_CPPv2N15bk_usb_drv_op_t23USB_DRV_VIDEO_DUAL_STOPE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea91f6ec5adbec153a60d74c81e5f1857b"></a> enumerator USB\_DRV\_VIDEO\_DUAL\_STOP

    <a id="_CPPv4N15bk_usb_drv_op_t21USB_DRV_VIDEO_DUAL_RXE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t21USB_DRV_VIDEO_DUAL_RXE"></a> <a id="_CPPv2N15bk_usb_drv_op_t21USB_DRV_VIDEO_DUAL_RXE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea5666d33305ba143af8d09135fa8688ce"></a> enumerator USB\_DRV\_VIDEO\_DUAL\_RX

    <a id="_CPPv4N15bk_usb_drv_op_t23USB_DRV_VIDEO_DUAL_RXEDE"></a>

    <a id="_CPPv3N15bk_usb_drv_op_t23USB_DRV_VIDEO_DUAL_RXEDE"></a> <a id="_CPPv2N15bk_usb_drv_op_t23USB_DRV_VIDEO_DUAL_RXEDE"></a> <a id="usb__types_8h_1aa9ea0c0ae69e7bea991362a9190adb0ea2dfabb77f3c4d7adacd63ce0ee6cbd4a"></a> enumerator USB\_DRV\_VIDEO\_DUAL\_RXED

<a id="_CPPv418E_USB_ATTRIBUTE_OP"></a>

<a id="_CPPv318E_USB_ATTRIBUTE_OP"></a> <a id="_CPPv218E_USB_ATTRIBUTE_OP"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6"></a> enum E\_USB\_ATTRIBUTE\_OP
:   *Values:*

    <a id="_CPPv4N18E_USB_ATTRIBUTE_OP26USB_ATTRIBUTE_RC_UNDEFINEDE"></a>

    <a id="_CPPv3N18E_USB_ATTRIBUTE_OP26USB_ATTRIBUTE_RC_UNDEFINEDE"></a> <a id="_CPPv2N18E_USB_ATTRIBUTE_OP26USB_ATTRIBUTE_RC_UNDEFINEDE"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6a09d7c72d8fc4524589951ada6cd026e6"></a> enumerator USB\_ATTRIBUTE\_RC\_UNDEFINED

    <a id="_CPPv4N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_SET_CURE"></a>

    <a id="_CPPv3N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_SET_CURE"></a> <a id="_CPPv2N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_SET_CURE"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6ae1a1826fe68971aaaa17eb612eccd4c7"></a> enumerator USB\_ATTRIBUTE\_SET\_CUR

    <a id="_CPPv4N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_CURE"></a>

    <a id="_CPPv3N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_CURE"></a> <a id="_CPPv2N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_CURE"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6aaa96904c47af48f71ae3b8ab8a619eba"></a> enumerator USB\_ATTRIBUTE\_GET\_CUR

    <a id="_CPPv4N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_MINE"></a>

    <a id="_CPPv3N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_MINE"></a> <a id="_CPPv2N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_MINE"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6abcd14c8f7ae9697340f3f11013214a20"></a> enumerator USB\_ATTRIBUTE\_GET\_MIN

    <a id="_CPPv4N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_MAXE"></a>

    <a id="_CPPv3N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_MAXE"></a> <a id="_CPPv2N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_MAXE"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6ae3dbd5ceaf8af25c85a364130707c116"></a> enumerator USB\_ATTRIBUTE\_GET\_MAX

    <a id="_CPPv4N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_RESE"></a>

    <a id="_CPPv3N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_RESE"></a> <a id="_CPPv2N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_RESE"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6ade64a96e9cc5260de778be22948d96bf"></a> enumerator USB\_ATTRIBUTE\_GET\_RES

    <a id="_CPPv4N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_LENE"></a>

    <a id="_CPPv3N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_LENE"></a> <a id="_CPPv2N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_LENE"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6a988a1181a8765513f8c32eb0593a045f"></a> enumerator USB\_ATTRIBUTE\_GET\_LEN

    <a id="_CPPv4N18E_USB_ATTRIBUTE_OP22USB_ATTRIBUTE_GET_INFOE"></a>

    <a id="_CPPv3N18E_USB_ATTRIBUTE_OP22USB_ATTRIBUTE_GET_INFOE"></a> <a id="_CPPv2N18E_USB_ATTRIBUTE_OP22USB_ATTRIBUTE_GET_INFOE"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6ac926d795432612c0c6e041bf092c6f66"></a> enumerator USB\_ATTRIBUTE\_GET\_INFO

    <a id="_CPPv4N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_DEFE"></a>

    <a id="_CPPv3N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_DEFE"></a> <a id="_CPPv2N18E_USB_ATTRIBUTE_OP21USB_ATTRIBUTE_GET_DEFE"></a> <a id="usb__types_8h_1afdedffc83cd2eef446c50329998df7b6a2064bcd82d9b5a960c39bf8b13a93a8a"></a> enumerator USB\_ATTRIBUTE\_GET\_DEF

<a id="_CPPv417E_UVC_ATTRIBUTE_T"></a>

<a id="_CPPv317E_UVC_ATTRIBUTE_T"></a> <a id="_CPPv217E_UVC_ATTRIBUTE_T"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0"></a> enum E\_UVC\_ATTRIBUTE\_T
:   *Values:*

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T31UVC_ATTRIBUTE_CONTROL_UNDEFINEDE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T31UVC_ATTRIBUTE_CONTROL_UNDEFINEDE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T31UVC_ATTRIBUTE_CONTROL_UNDEFINEDE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a3e23661b5cebe52eedfe004486476e4d"></a> enumerator UVC\_ATTRIBUTE\_CONTROL\_UNDEFINED

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T36UVC_ATTRIBUTE_BACKLIGHT_COMPENSATIONE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T36UVC_ATTRIBUTE_BACKLIGHT_COMPENSATIONE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T36UVC_ATTRIBUTE_BACKLIGHT_COMPENSATIONE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0ae0ed136589f07ca592fe358c5cfc1042"></a> enumerator UVC\_ATTRIBUTE\_BACKLIGHT\_COMPENSATION

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T24UVC_ATTRIBUTE_BRIGHTNESSE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T24UVC_ATTRIBUTE_BRIGHTNESSE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T24UVC_ATTRIBUTE_BRIGHTNESSE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a97235e2f8616c446954257c2b06dbeae"></a> enumerator UVC\_ATTRIBUTE\_BRIGHTNESS

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T22UVC_ATTRIBUTE_CONTRASTE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T22UVC_ATTRIBUTE_CONTRASTE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T22UVC_ATTRIBUTE_CONTRASTE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a756e0758412ec8ebb6baca3d38a0b4fb"></a> enumerator UVC\_ATTRIBUTE\_CONTRAST

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T18UVC_ATTRIBUTE_GAINE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T18UVC_ATTRIBUTE_GAINE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T18UVC_ATTRIBUTE_GAINE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0af09bf96019ce7163453a4b3e75373eda"></a> enumerator UVC\_ATTRIBUTE\_GAIN

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T34UVC_ATTRIBUTE_POWER_LINE_FREQUENCYE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T34UVC_ATTRIBUTE_POWER_LINE_FREQUENCYE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T34UVC_ATTRIBUTE_POWER_LINE_FREQUENCYE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a531f2c814d7200d29597a4bffdc10fae"></a> enumerator UVC\_ATTRIBUTE\_POWER\_LINE\_FREQUENCY

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T17UVC_ATTRIBUTE_HUEE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T17UVC_ATTRIBUTE_HUEE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T17UVC_ATTRIBUTE_HUEE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a45bcbd011f8968a02ba6794bf609984f"></a> enumerator UVC\_ATTRIBUTE\_HUE

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T24UVC_ATTRIBUTE_SATURATIONE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T24UVC_ATTRIBUTE_SATURATIONE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T24UVC_ATTRIBUTE_SATURATIONE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a0c20681ace5de6928f8100998ddf3cb5"></a> enumerator UVC\_ATTRIBUTE\_SATURATION

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T23UVC_ATTRIBUTE_SHARPNESSE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T23UVC_ATTRIBUTE_SHARPNESSE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T23UVC_ATTRIBUTE_SHARPNESSE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0ac8453e7299ece5a993df1b39b4b75515"></a> enumerator UVC\_ATTRIBUTE\_SHARPNESS

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T19UVC_ATTRIBUTE_GAMMAE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T19UVC_ATTRIBUTE_GAMMAE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T19UVC_ATTRIBUTE_GAMMAE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0aedd1f51cbfdcf3da9a4332a126288554"></a> enumerator UVC\_ATTRIBUTE\_GAMMA

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T39UVC_ATTRIBUTE_WHITE_BALANCE_TEMPERATUREE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T39UVC_ATTRIBUTE_WHITE_BALANCE_TEMPERATUREE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T39UVC_ATTRIBUTE_WHITE_BALANCE_TEMPERATUREE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0ae4bd75f258a94f8909fc9f237f4fb263"></a> enumerator UVC\_ATTRIBUTE\_WHITE\_BALANCE\_TEMPERATURE

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T44UVC_ATTRIBUTE_WHITE_BALANCE_TEMPERATURE_AUTOE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T44UVC_ATTRIBUTE_WHITE_BALANCE_TEMPERATURE_AUTOE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T44UVC_ATTRIBUTE_WHITE_BALANCE_TEMPERATURE_AUTOE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a914c347fd0804f607d1e16a6f96361e8"></a> enumerator UVC\_ATTRIBUTE\_WHITE\_BALANCE\_TEMPERATURE\_AUTO

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T37UVC_ATTRIBUTE_WHITE_BALANCE_COMPONENTE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T37UVC_ATTRIBUTE_WHITE_BALANCE_COMPONENTE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T37UVC_ATTRIBUTE_WHITE_BALANCE_COMPONENTE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a8951142b7575d72f2650aea3797d945d"></a> enumerator UVC\_ATTRIBUTE\_WHITE\_BALANCE\_COMPONENT

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T42UVC_ATTRIBUTE_WHITE_BALANCE_COMPONENT_AUTOE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T42UVC_ATTRIBUTE_WHITE_BALANCE_COMPONENT_AUTOE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T42UVC_ATTRIBUTE_WHITE_BALANCE_COMPONENT_AUTOE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a288e2e7da735348cb0a9ea1419edbc45"></a> enumerator UVC\_ATTRIBUTE\_WHITE\_BALANCE\_COMPONENT\_AUTO

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T32UVC_ATTRIBUTE_DIGITAL_MULTIPLIERE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T32UVC_ATTRIBUTE_DIGITAL_MULTIPLIERE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T32UVC_ATTRIBUTE_DIGITAL_MULTIPLIERE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a5ae742c3d1579492159e35902501e5b2"></a> enumerator UVC\_ATTRIBUTE\_DIGITAL\_MULTIPLIER

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T38UVC_ATTRIBUTE_DIGITAL_MULTIPLIER_LIMITE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T38UVC_ATTRIBUTE_DIGITAL_MULTIPLIER_LIMITE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T38UVC_ATTRIBUTE_DIGITAL_MULTIPLIER_LIMITE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a6d880b53a970e666cefaa1568481802a"></a> enumerator UVC\_ATTRIBUTE\_DIGITAL\_MULTIPLIER\_LIMIT

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T22UVC_ATTRIBUTE_HUE_AUTOE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T22UVC_ATTRIBUTE_HUE_AUTOE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T22UVC_ATTRIBUTE_HUE_AUTOE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a9376cfda9549b05aa66f4a9d95b48010"></a> enumerator UVC\_ATTRIBUTE\_HUE\_AUTO

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T35UVC_ATTRIBUTE_ANALOG_VIDEO_STANDARDE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T35UVC_ATTRIBUTE_ANALOG_VIDEO_STANDARDE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T35UVC_ATTRIBUTE_ANALOG_VIDEO_STANDARDE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a46c442e92b17ef08597db3ee9db6d6e9"></a> enumerator UVC\_ATTRIBUTE\_ANALOG\_VIDEO\_STANDARD

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T32UVC_ATTRIBUTE_ANALOG_LOCK_STATUSE"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T32UVC_ATTRIBUTE_ANALOG_LOCK_STATUSE"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T32UVC_ATTRIBUTE_ANALOG_LOCK_STATUSE"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a31e72bab48cbba191acf7cecbcab85cc"></a> enumerator UVC\_ATTRIBUTE\_ANALOG\_LOCK\_STATUS

    <a id="_CPPv4N17E_UVC_ATTRIBUTE_T17UVC_ATTRIBUTE_NUME"></a>

    <a id="_CPPv3N17E_UVC_ATTRIBUTE_T17UVC_ATTRIBUTE_NUME"></a> <a id="_CPPv2N17E_UVC_ATTRIBUTE_T17UVC_ATTRIBUTE_NUME"></a> <a id="usb__types_8h_1ae753f271f5ae961463135c1f533370e0a53f3f4f90ee783bf7c73f348347fd1c2"></a> enumerator UVC\_ATTRIBUTE\_NUM

<a id="_CPPv417E_UAC_ATTRIBUTE_T"></a>

<a id="_CPPv317E_UAC_ATTRIBUTE_T"></a> <a id="_CPPv217E_UAC_ATTRIBUTE_T"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04"></a> enum E\_UAC\_ATTRIBUTE\_T
:   *Values:*

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T19UAC_ATTRIBUTE_UNDEFE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T19UAC_ATTRIBUTE_UNDEFE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T19UAC_ATTRIBUTE_UNDEFE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04ab7a4d9fa576be50aca52f055140f287f"></a> enumerator UAC\_ATTRIBUTE\_UNDEF

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T18UAC_ATTRIBUTE_MUTEE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T18UAC_ATTRIBUTE_MUTEE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T18UAC_ATTRIBUTE_MUTEE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04ae68f7e21cda511ecaac8fb5ff99b36d5"></a> enumerator UAC\_ATTRIBUTE\_MUTE

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T20UAC_ATTRIBUTE_VOLUMEE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T20UAC_ATTRIBUTE_VOLUMEE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T20UAC_ATTRIBUTE_VOLUMEE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a3079f022f9fe79c026e92334eec0ae0e"></a> enumerator UAC\_ATTRIBUTE\_VOLUME

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T18UAC_ATTRIBUTE_BASSE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T18UAC_ATTRIBUTE_BASSE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T18UAC_ATTRIBUTE_BASSE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04adf7833231e1e35d712e831b0f946b94a"></a> enumerator UAC\_ATTRIBUTE\_BASS

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T17UAC_ATTRIBUTE_MIDE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T17UAC_ATTRIBUTE_MIDE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T17UAC_ATTRIBUTE_MIDE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a45a35bc12ebceeff1d699452f35a4fd9"></a> enumerator UAC\_ATTRIBUTE\_MID

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T20UAC_ATTRIBUTE_TREBLEE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T20UAC_ATTRIBUTE_TREBLEE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T20UAC_ATTRIBUTE_TREBLEE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04aa5222fcb4fb8dedc913cba8aa985abc3"></a> enumerator UAC\_ATTRIBUTE\_TREBLE

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T31UAC_ATTRIBUTE_GRAPHIC_EQUALIZERE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T31UAC_ATTRIBUTE_GRAPHIC_EQUALIZERE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T31UAC_ATTRIBUTE_GRAPHIC_EQUALIZERE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a64fa86d701318c7c6f0e92e0cddefb69"></a> enumerator UAC\_ATTRIBUTE\_GRAPHIC\_EQUALIZER

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T28UAC_ATTRIBUTE_AUTOMATIC_GAINE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T28UAC_ATTRIBUTE_AUTOMATIC_GAINE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T28UAC_ATTRIBUTE_AUTOMATIC_GAINE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a8b3b978bb827d9abb95d6d871429eca4"></a> enumerator UAC\_ATTRIBUTE\_AUTOMATIC\_GAIN

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T19UAC_ATTRIBUTE_DEALYE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T19UAC_ATTRIBUTE_DEALYE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T19UAC_ATTRIBUTE_DEALYE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04ae65e4bb81ae16004835743025af430fe"></a> enumerator UAC\_ATTRIBUTE\_DEALY

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T24UAC_ATTRIBUTE_BASS_BOOSTE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T24UAC_ATTRIBUTE_BASS_BOOSTE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T24UAC_ATTRIBUTE_BASS_BOOSTE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a86e110f4e83191df732e1d318145a27d"></a> enumerator UAC\_ATTRIBUTE\_BASS\_BOOST

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T22UAC_ATTRIBUTE_LOUDNESSE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T22UAC_ATTRIBUTE_LOUDNESSE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T22UAC_ATTRIBUTE_LOUDNESSE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04ad1ffd57fbf4c59ce41b7d8cdd46d3e03"></a> enumerator UAC\_ATTRIBUTE\_LOUDNESS

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T22UAC_ATTRIBUTE_INP_GAINE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T22UAC_ATTRIBUTE_INP_GAINE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T22UAC_ATTRIBUTE_INP_GAINE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a1601448a0166bd422c13c125ab138337"></a> enumerator UAC\_ATTRIBUTE\_INP\_GAIN

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T26UAC_ATTRIBUTE_INP_GAIN_PADE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T26UAC_ATTRIBUTE_INP_GAIN_PADE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T26UAC_ATTRIBUTE_INP_GAIN_PADE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04ade47b7e7d7ab6ad5db716d8d774ae215"></a> enumerator UAC\_ATTRIBUTE\_INP\_GAIN\_PAD

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T26UAC_ATTRIBUTE_PHASE_INVERTE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T26UAC_ATTRIBUTE_PHASE_INVERTE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T26UAC_ATTRIBUTE_PHASE_INVERTE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a5f251c3a23012addcded73b31e25ab00"></a> enumerator UAC\_ATTRIBUTE\_PHASE\_INVERT

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T23UAC_ATTRIBUTE_UNDERFLOWE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T23UAC_ATTRIBUTE_UNDERFLOWE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T23UAC_ATTRIBUTE_UNDERFLOWE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a13ffe14e5dfbafe6a4b3bf829674e3b3"></a> enumerator UAC\_ATTRIBUTE\_UNDERFLOW

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T22UAC_ATTRIBUTE_OVERFLOWE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T22UAC_ATTRIBUTE_OVERFLOWE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T22UAC_ATTRIBUTE_OVERFLOWE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a9a35007f0fba5f85e946805684ec4fc5"></a> enumerator UAC\_ATTRIBUTE\_OVERFLOW

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T21UAC_ATTRIBUTE_LATENCYE"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T21UAC_ATTRIBUTE_LATENCYE"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T21UAC_ATTRIBUTE_LATENCYE"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04aa2b2dc1c8496db7f36577e620d40df6a"></a> enumerator UAC\_ATTRIBUTE\_LATENCY

    <a id="_CPPv4N17E_UAC_ATTRIBUTE_T17UAC_ATTRIBUTE_NUME"></a>

    <a id="_CPPv3N17E_UAC_ATTRIBUTE_T17UAC_ATTRIBUTE_NUME"></a> <a id="_CPPv2N17E_UAC_ATTRIBUTE_T17UAC_ATTRIBUTE_NUME"></a> <a id="usb__types_8h_1a77c6c838c167e1236fce0adaa667bc04a38a4beb69ae7c441fef3272e36cde98e"></a> enumerator UAC\_ATTRIBUTE\_NUM

<a id="_CPPv420E_USB_HUB_PORT_INDEX"></a>

<a id="_CPPv320E_USB_HUB_PORT_INDEX"></a> <a id="_CPPv220E_USB_HUB_PORT_INDEX"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5"></a> enum E\_USB\_HUB\_PORT\_INDEX
:   *Values:*

    <a id="_CPPv4N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_1E"></a>

    <a id="_CPPv3N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_1E"></a> <a id="_CPPv2N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_1E"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5a24eb5efa777dbf9302c3f786c774059f"></a> enumerator USB\_HUB\_PORT\_1

    <a id="_CPPv4N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_2E"></a>

    <a id="_CPPv3N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_2E"></a> <a id="_CPPv2N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_2E"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5a0aded3caf62b0ba359c9d9d0348096dd"></a> enumerator USB\_HUB\_PORT\_2

    <a id="_CPPv4N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_3E"></a>

    <a id="_CPPv3N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_3E"></a> <a id="_CPPv2N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_3E"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5a30cc801a657544031a489ba6c9b6fe72"></a> enumerator USB\_HUB\_PORT\_3

    <a id="_CPPv4N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_4E"></a>

    <a id="_CPPv3N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_4E"></a> <a id="_CPPv2N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_4E"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5a143280d9da2aa460ffeafc135670a641"></a> enumerator USB\_HUB\_PORT\_4

    <a id="_CPPv4N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_5E"></a>

    <a id="_CPPv3N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_5E"></a> <a id="_CPPv2N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_5E"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5ab43dc8c8123c90b8c18e985f51e6f992"></a> enumerator USB\_HUB\_PORT\_5

    <a id="_CPPv4N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_6E"></a>

    <a id="_CPPv3N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_6E"></a> <a id="_CPPv2N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_6E"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5abaf1a7f968421616a3991763f52e3e16"></a> enumerator USB\_HUB\_PORT\_6

    <a id="_CPPv4N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_7E"></a>

    <a id="_CPPv3N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_7E"></a> <a id="_CPPv2N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_7E"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5a64201871c015aa0cfc3a405c284746d1"></a> enumerator USB\_HUB\_PORT\_7

    <a id="_CPPv4N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_8E"></a>

    <a id="_CPPv3N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_8E"></a> <a id="_CPPv2N20E_USB_HUB_PORT_INDEX14USB_HUB_PORT_8E"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5a33cef9b0e55c8f1462d9cc4f190a7627"></a> enumerator USB\_HUB\_PORT\_8

    <a id="_CPPv4N20E_USB_HUB_PORT_INDEX16USB_HUB_PORT_MAXE"></a>

    <a id="_CPPv3N20E_USB_HUB_PORT_INDEX16USB_HUB_PORT_MAXE"></a> <a id="_CPPv2N20E_USB_HUB_PORT_INDEX16USB_HUB_PORT_MAXE"></a> <a id="usb__types_8h_1a74a4fd34b47e2700cc13ec1775fa32d5a5f7beed0c19c3e563b5f36713cae6289"></a> enumerator USB\_HUB\_PORT\_MAX
