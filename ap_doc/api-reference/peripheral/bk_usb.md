# USB



## USB API Status

| API | BK7259_AP |
| --- | --- |
| [`bk_usb_driver_init()`](#_CPPv418bk_usb_driver_initv "bk_usb_driver_init") | Y |
| [`bk_usb_driver_deinit()`](#_CPPv420bk_usb_driver_deinitv "bk_usb_driver_deinit") | Y |
| [`bk_usb_power_ops()`](#_CPPv416bk_usb_power_ops8uint32_tb "bk_usb_power_ops") | Y |
| [`bk_usb_open()`](#_CPPv411bk_usb_open8uint32_t "bk_usb_open") | Y |
| [`bk_usb_close()`](#_CPPv412bk_usb_closev "bk_usb_close") | Y |


## USB Port Number

| Capability | BK7259_AP |
| --- | --- |
| Port Number | 1 |


## USB Pin and GPIO Map

| USB Pin | BK7259_AP |
| --- | --- |
| USB power | 28 |


## USB API Reference


### Header File


- [usb.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/usb.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/usb.h")


### Functions

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_usb_driver_init(void)
:   USB Driver initialization.

    Register the adaptation layer and pass the function pointers used by the closed source library. Register the current USB Class type to be supported, and it can be uninstalled and reinitialized during execution. But be sure to do so before calling other interfaces.


    - Configure Interrupt handling function registration

    - Configure Class Driver Registration

    This API should be called before any other USB APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_usb_driver_deinit(void)
:   USB Driver uninstallation.

    Turn off the USB main interrupt switch Unregister Total Interrupt Handling Function Unregistered Class Driver

    This API should be called after any other USB APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_usb_power_ops(uint32_t gpio_id, bool ops)
:   Pin controlled USB Vbus.

    This API controls VBUS for USB:


    - Determine whether to output voltage through the high and low levels of a GPIO output parameter: gpio_id Select the corresponding pin number ops Choose to power on or off

    - Configure whether USB is power on

    When the fusion device is working, if there is a device voting for use, it cannot be directly turned off.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_usb_open(uint32_t usb_mode)
:   open the USB

    This API configure the resoure common to USB:


    - Select the identity as host or slave parameter: usb_mode USB_HOST_MODE = 0 USB_DEVICE_MODE = 1

    - Configure USB common clock

    - Configure USB common registers

    This API should be called before any other USB APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

[bk_err_t](../system/os.md#_CPPv48bk_err_t "bk_err_t") bk_usb_close(void)
:   close the USB

    This API release USB resources:


    - Restore register

    - Turn off the power and clock

    This API should be called after any other USB APIs.

    返回
    :   - BK_OK: succeed

        - others: other errors.

bool bk_usb_get_device_connect_status(void)
:   Obtain whether there is currently a device connection.

    返回
    :   - TRUE: connect

        - FALSE: disconnect


## USB API Typedefs


### Header File


- [usb_types.h](http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/usb_types.h "http://192.168.0.46/gerrit/plugins/gitiles/iot/wcn/projects/+/refs/heads/armino_main/components/usb_types.h")


### Structures

struct usb_device_descriptor_t

struct usb_configuration_descriptor_t

struct usb_interface_association_descriptor_t

struct usb_interface_descriptor_t

struct usb_audio_endpoint_general_descriptor_t

struct s_bk_usb_endpoint_descriptor

struct bk_uvc_format_index

struct bk_uvc_frame

struct bk_uvc_all_frame

struct bk_uvc_device_brief_info_t

struct bk_uvc_config_t

struct audio_packet_t

struct audio_packet_control_t

struct bk_uac_ring_buffer_t

struct bk_uac_device_brief_info_t

struct bk_uac_mic_config_t

struct bk_uac_spk_config_t

struct bk_uac_config_t

struct bk_uvc_uac_app_callback

struct s_usb_device_request

struct s_usb_transfer_buffer_info

struct bk_usb_hub_port_info

struct usb_hub_pipe


### Macros

BK_ERR_USB_NOT_POWER
:   USB vbus poweron, etc

BK_ERR_USB_NOT_OPEN
:   USB dose not turn on clock and power, etc

BK_ERR_USB_NOT_CLOSE
:   USB dose not turn off clock and power, etc

BK_ERR_USB_NOT_CONNECT
:   USB device not connected

BK_ERR_USB_OPERATION_NULL_POINTER
:   USB Operated with null pointer

BK_ERR_USB_UVC_NOT_START
:   UVC Transfer not started

BK_ERR_USB_UVC_NOT_STOP
:   UVC Transfer not stopped

BK_ERR_USB_UVC_NOT_PAUSE
:   UVC Transfer not paused

BK_ERR_USB_UVC_GET_PARAMETER_FAILED
:   UVC The command to obtain parameters did not respond

BK_ERR_USB_UVC_SET_PARAMETER_FAILED
:   UVC Configuration parameter command did not respond

BK_ERR_USB_UVC_SET_INTERFACE_FAILED
:   UVC The set port command did not respond

BK_ERR_USB_UVC_NOSUPPORT_ATTRIBUTE
:   UVC The attribute configuration is not supported

BK_ERR_USB_UAC_NOT_START
:   UAC Transfer not started

BK_ERR_USB_UAC_NOT_STOP
:   UAC Transfer not stopped

BK_ERR_USB_UAC_NOT_PAUSE
:   UAC Transfer not paused

BK_ERR_USB_UAC_GET_PARAMETER_FAILED
:   UAC The command to obtain parameters did not respond

BK_ERR_USB_UAC_SET_PARAMETER_FAILED
:   UAC Configuration parameter command did not respond

BK_ERR_USB_UAC_SET_INTERFACE_FAILED
:   UAC The set port command did not respond

BK_ERR_USB_UAC_NOSUPPORT_ATTRIBUTE
:   UAC The attribute configuration is not supported

BK_USB_ENDPOINT_XFERTYPE_MASK


### Enumerations

enum E_USB_MODE
:   *Values:*

    enumerator USB_HOST_MODE

    enumerator USB_DEVICE_MODE

enum E_USB_CONNECTION_STATUS
:   *Values:*

    enumerator USB_DEVICE_DISCONNECT

    enumerator USB_DEVICE_CONNECT

enum E_FRAME_RATE_ID
:   *Values:*

    enumerator FPS_60

    enumerator FPS_30

    enumerator FPS_25

    enumerator FPS_20

    enumerator FPS_15

    enumerator FPS_10

    enumerator FPS_5

enum E_USB_DEVICE_T
:   *Values:*

    enumerator USB_UVC_DEVICE

    enumerator USB_UVC_H26X_DEVICE

    enumerator USB_UAC_MIC_DEVICE

    enumerator USB_UAC_SPEAKER_DEVICE

    enumerator USB_MSD_DEVICE

    enumerator USB_OTA_DEVICE

    enumerator USB_USER_CHECK_DEVICE

    enumerator USB_CDC_DEVICE

    enumerator USB_DEVICE_MAX

enum E_USB_ENDPOINT_TRANSFER_MODE_T
:   *Values:*

    enumerator USB_ENDPOINT_CONTROL_TRANSFER

    enumerator USB_ENDPOINT_ISOCH_TRANSFER

    enumerator USB_ENDPOINT_BULK_TRANSFER

    enumerator USB_ENDPOINT_INT_TRANSFER

    enumerator USB_ENDPOINT_INVALID_TRANSFER

enum bk_usb_drv_op_t
:   *Values:*

    enumerator USB_DRV_IDLE

    enumerator USB_DRV_EXIT

    enumerator USB_POWER_OPS

    enumerator USB_DRV_USB_INIT

    enumerator USB_DRV_USB_DEINIT

    enumerator USB_DRV_SET_DEV_USE

    enumerator USB_DRV_USB_OPEN

    enumerator USB_DRV_USB_CLOSE

    enumerator USB_DRV_CONNECT_HANDLE

    enumerator USB_DRV_DISCONNECT_HANDLE

    enumerator USB_DRV_GET_DEV_CONNECT_STATUS

    enumerator USB_DRV_CHECK_DEV_SUPPORT

    enumerator USB_DRV_PRASE_DESCRIPTOR

    enumerator USB_DRV_INIT_CONTROL_TRANS

    enumerator USB_DRV_DEINIT_CONTROL_TRANS

    enumerator USB_DRV_CONTROL_TRANSFER

    enumerator USB_DRV_UVC_REGISTER_CONNECT_CB

    enumerator USB_DRV_UVC_REGISTER_DISCONNECT_CB

    enumerator USB_DRV_UVC_GET_PARAM

    enumerator USB_DRV_UVC_SET_PARAM

    enumerator USB_DRV_UVC_REGISTER_TRANSFER_OPS

    enumerator USB_DRV_UVC_TRANSFER_BUFFER_MALLOC

    enumerator USB_DRV_UVC_TRANSFER_BUFFER_PUSH

    enumerator USB_DRV_UVC_TRANSFER_BUFFER_POP

    enumerator USB_DRV_UVC_TRANSFER_BUFFER_FREE

    enumerator USB_DRV_VIDEO_OPEN_PIPE

    enumerator USB_DRV_VIDEO_CLOSE_PIPE

    enumerator USB_DRV_VIDEO_START

    enumerator USB_DRV_VIDEO_STOP

    enumerator USB_DRV_VIDEO_RX

    enumerator USB_DRV_VIDEO_RXED

    enumerator USB_DRV_UAC_REGISTER_CONNECT_CB

    enumerator USB_DRV_UAC_REGISTER_DISCONNECT_CB

    enumerator USB_DRV_UAC_GET_PARAM

    enumerator USB_DRV_UAC_SET_PARAM

    enumerator USB_DRV_UAC_REGISTER_TRANSFER_OPS

    enumerator USB_DRV_UAC_TRANSFER_BUFFER_MALLOC

    enumerator USB_DRV_UAC_TRANSFER_BUFFER_PUSH

    enumerator USB_DRV_UAC_TRANSFER_BUFFER_POP

    enumerator USB_DRV_UAC_TRANSFER_BUFFER_FREE

    enumerator USB_DRV_AUDIO_OPEN_PIPE

    enumerator USB_DRV_AUDIO_CLOSE_PIPE

    enumerator USB_DRV_AUDIO_MIC_START

    enumerator USB_DRV_AUDIO_MIC_STOP

    enumerator USB_DRV_AUDIO_SPK_START

    enumerator USB_DRV_AUDIO_SPK_STOP

    enumerator USB_DRV_AUDIO_RX

    enumerator USB_DRV_AUDIO_RXED

    enumerator USB_DRV_AUDIO_TX

    enumerator USB_DRV_AUDIO_TXED

    enumerator USB_DRV_UVC_TRANSFER_DUAL_BUFFER_MALLOC

    enumerator USB_DRV_UVC_TRANSFER_DUAL_BUFFER_PUSH

    enumerator USB_DRV_UVC_TRANSFER_DUAL_BUFFER_POP

    enumerator USB_DRV_UVC_TRANSFER_DUAL_BUFFER_FREE

    enumerator USB_DRV_VIDEO_DUAL_START

    enumerator USB_DRV_VIDEO_DUAL_STOP

    enumerator USB_DRV_VIDEO_DUAL_RX

    enumerator USB_DRV_VIDEO_DUAL_RXED

enum E_USB_ATTRIBUTE_OP
:   *Values:*

    enumerator USB_ATTRIBUTE_RC_UNDEFINED

    enumerator USB_ATTRIBUTE_SET_CUR

    enumerator USB_ATTRIBUTE_GET_CUR

    enumerator USB_ATTRIBUTE_GET_MIN

    enumerator USB_ATTRIBUTE_GET_MAX

    enumerator USB_ATTRIBUTE_GET_RES

    enumerator USB_ATTRIBUTE_GET_LEN

    enumerator USB_ATTRIBUTE_GET_INFO

    enumerator USB_ATTRIBUTE_GET_DEF

enum E_UVC_ATTRIBUTE_T
:   *Values:*

    enumerator UVC_ATTRIBUTE_CONTROL_UNDEFINED

    enumerator UVC_ATTRIBUTE_BACKLIGHT_COMPENSATION

    enumerator UVC_ATTRIBUTE_BRIGHTNESS

    enumerator UVC_ATTRIBUTE_CONTRAST

    enumerator UVC_ATTRIBUTE_GAIN

    enumerator UVC_ATTRIBUTE_POWER_LINE_FREQUENCY

    enumerator UVC_ATTRIBUTE_HUE

    enumerator UVC_ATTRIBUTE_SATURATION

    enumerator UVC_ATTRIBUTE_SHARPNESS

    enumerator UVC_ATTRIBUTE_GAMMA

    enumerator UVC_ATTRIBUTE_WHITE_BALANCE_TEMPERATURE

    enumerator UVC_ATTRIBUTE_WHITE_BALANCE_TEMPERATURE_AUTO

    enumerator UVC_ATTRIBUTE_WHITE_BALANCE_COMPONENT

    enumerator UVC_ATTRIBUTE_WHITE_BALANCE_COMPONENT_AUTO

    enumerator UVC_ATTRIBUTE_DIGITAL_MULTIPLIER

    enumerator UVC_ATTRIBUTE_DIGITAL_MULTIPLIER_LIMIT

    enumerator UVC_ATTRIBUTE_HUE_AUTO

    enumerator UVC_ATTRIBUTE_ANALOG_VIDEO_STANDARD

    enumerator UVC_ATTRIBUTE_ANALOG_LOCK_STATUS

    enumerator UVC_ATTRIBUTE_NUM

enum E_UAC_ATTRIBUTE_T
:   *Values:*

    enumerator UAC_ATTRIBUTE_UNDEF

    enumerator UAC_ATTRIBUTE_MUTE

    enumerator UAC_ATTRIBUTE_VOLUME

    enumerator UAC_ATTRIBUTE_BASS

    enumerator UAC_ATTRIBUTE_MID

    enumerator UAC_ATTRIBUTE_TREBLE

    enumerator UAC_ATTRIBUTE_GRAPHIC_EQUALIZER

    enumerator UAC_ATTRIBUTE_AUTOMATIC_GAIN

    enumerator UAC_ATTRIBUTE_DEALY

    enumerator UAC_ATTRIBUTE_BASS_BOOST

    enumerator UAC_ATTRIBUTE_LOUDNESS

    enumerator UAC_ATTRIBUTE_INP_GAIN

    enumerator UAC_ATTRIBUTE_INP_GAIN_PAD

    enumerator UAC_ATTRIBUTE_PHASE_INVERT

    enumerator UAC_ATTRIBUTE_UNDERFLOW

    enumerator UAC_ATTRIBUTE_OVERFLOW

    enumerator UAC_ATTRIBUTE_LATENCY

    enumerator UAC_ATTRIBUTE_NUM

enum E_USB_HUB_PORT_INDEX
:   *Values:*

    enumerator USB_HUB_PORT_1

    enumerator USB_HUB_PORT_2

    enumerator USB_HUB_PORT_3

    enumerator USB_HUB_PORT_4

    enumerator USB_HUB_PORT_5

    enumerator USB_HUB_PORT_6

    enumerator USB_HUB_PORT_7

    enumerator USB_HUB_PORT_8

    enumerator USB_HUB_PORT_MAX
