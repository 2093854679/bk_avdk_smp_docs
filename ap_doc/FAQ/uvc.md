# UVC常见问题



## 1. 简介

> 在使用uvc时，有些常见的问题，可能会遇到，下面提供一些调试方法。
>
> Q：调用power on的接口后，摄像头不枚举（没有提示连接成功）
>
> A：这种问题一般是摄像头没有上电，或者供电不足，一半建议给USB供5.0v的电压。BK7258控制USB的LDO是通过GPIO28，拉高即可使能USB的电源，拉低即给USB掉电，可以通过宏进行配置：
>
> |  |  |  |
> | --- | --- | --- |
> | marco | value | implication |
> | CONFIG_USB_VBAT_CONTROL_GPIO_ID | 0x1C | The gpio id control usb power |
>
> Q：枚举成功，但是camera open不出图
>
> A：这种问题一般需要检查参数是否配置错误，比如此摄像头不支持你配置的分辨率，这就需要你重新配置。
> 当分辨率配置错误时，会打印如下log: “uvc_camera_set_param, not support this format or resolution, please check!”。
> 如果不是，则需要抓包分析，UVC数据包是否正常。包含包头+有效数据，且有效数据为正常值。
>
> Q：帧率低于预期
>
> A：所谓的预期是相对于PC而言，比如配置30fps，实际出来只有一半，或者低了很多，插到电脑上分析一下，
> 是不是帧率也同样低，这样可以排除摄像头本身的影响。若不是摄像头本身的问题，则考虑是不是SDK的问题。
> 这个需要拉逻分分析，或者用协议分析仪抓包分析。
>
> Q：图像出现切屏异常，图像不完整
>
> A：这种情况一般需要检查传输方式ISO/BULK是否有配置错误，然后检查上层解包逻辑是否有误。
>
> Q：图像出现不正常的光晕和畸变
>
> A：这个一般考虑摄像头本身的问题，插到PC上分析是否有同样的问题。
>
> Q：出现异常log: “uvc_camera_urb_malloc failed”，或同步出图异常切屏。
>
> A：出现该问题的原因是，usb申请urb存储fifo里面的数据，但是申请不到。申请不到的原因是，所有的usb都被用完了，没有空闲态的urb。出现的根本原因有两个：
>
> > - 一个是消耗（解析）已经存储fifo数据的urb效率太低了，或者被卡住了，导致所有的空闲的urb的被消耗完，urb池中都是待解析的urb。
> >   :   参考代码：“./ap/bk_uvc/bk_uvc.c”, 是由任务“uvc_pro_task”进行解析，需要分析时是否被卡住了，或者说效率太低了。
> > - 另一个原因是urb的数量真不够了，比如使用双摄时，urb的个数建议是默认值4的至少两倍。
>
> 下面的宏定义了urb的数量。
>
> |  |  |  |
> | --- | --- | --- |
> | marco | value | implication |
> | CONFIG_UVC_URB_NUM | 4 | receive usb data urb number |
> | CONFIG_UVC_NUM_PACKET_PER_URB | 8 | an urb include packets |
>
> Q：使用UVC进行H264 pipeline编码时，打印“h264_encode_finish_handle 26430-65536, error:1”。
>
> A：打印该log的原因有两个：
>
> > - 一个是当第一个数字（26430）大于第二个数字（65536）时，说明此时I帧的长度大于frame_buffer的长度（第二个数字）；
> >
> > 修改方式：将宏CONFIG_H264_FRAME_SIZE配置成一个更大的值；
> >
> > - 另一个是“error:”的值为1，表示出来的JPEG图像解码长度不对，说明JPEG图像有填充位，为了防止图像异常，解码器内部做了严格的图像长度检查；
> >
> > 修改方式：建议修改摄像头固件，保证UVC输出的JPEG图像没有填充位，这种类型的填充位一般在末尾且为0xFF或0x00，或者图像真的有问题；
> > 另一种方法是降低解码器内部的图像长度检查机制，不建议这么做，这样有可能会有JPEG异常图像造成显示花屏。
>
> Q：PC端出图正常，接到板子上不出图，而且log打印“uvc_id1:0[348 85KB], uvc_id2: 0[0 0KB], uvc_id3:0[0 0KB], packets:[all:95832, err:0]”；
>
> A：log的格式解析如下：uvc port id：当前帧率[当前帧号 当前图片大小]；此时请检查错误log，是否有打开失败的对应log。
