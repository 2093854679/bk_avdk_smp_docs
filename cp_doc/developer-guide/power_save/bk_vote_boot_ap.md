---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_vote_boot_ap.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap"></a>

# 如何启动和关闭AP

<a id="id1"></a>

## 启动和关闭AP的策略

- 1.启动AP，有一个模块投票启动，则启动AP。
- 2.关闭AP时，需要所有投启动AP的模块，都投关闭的票，才能关闭。

<a id="id2"></a>

## 当前预置启动AP的模块名称

> ```
> typedef enum
> {
>  PM_BOOT_AP_MODULE_NAME_FFT          = 0,
>  PM_BOOT_AP_MODULE_NAME_AUDP_SBC        ,// 1
>  PM_BOOT_AP_MODULE_NAME_AUDP_AUDIO      ,// 2
>  PM_BOOT_AP_MODULE_NAME_AUDP_I2S        ,// 3
>  PM_BOOT_AP_MODULE_NAME_VIDP_JPEG_EN    ,// 4
>  PM_BOOT_AP_MODULE_NAME_VIDP_JPEG_DE    ,// 5
>  PM_BOOT_AP_MODULE_NAME_VIDP_DMA2D      ,// 6
>  PM_BOOT_AP_MODULE_NAME_VIDP_LCD        ,// 7
>  PM_BOOT_AP_MODULE_NAME_MULTIMEDIA      ,// 8
>  PM_BOOT_AP_MODULE_NAME_APP             ,// 9
>  PM_BOOT_AP_MODULE_NAME_VIDP_ROTATE     ,// 10
>  PM_BOOT_AP_MODULE_NAME_VIDP_SCALE      ,// 11
>  PM_BOOT_AP_MODULE_NAME_GET_MEDIA_MSG   ,// 12
>  PM_BOOT_AP_MODULE_NAME_LVGL            ,// 13
>  PM_BOOT_AP_MODULE_NAME_USER            ,// 14
>  PM_BOOT_AP_MODULE_NAME_MAX             ,// attention: MAX value can not exceed 31.
>  }pm_boot_ap_module_name_e;
> ```

<a id="id3"></a>

## 启动AP的接口

> - bk\_err\_t bk\_pm\_module\_vote\_boot\_ap\_ctrl(pm\_boot\_ap\_module\_name\_e module,pm\_power\_module\_state\_e power\_state)
>
>   > - module：模块名字（选择一个没有应用程序使用的模块名字。应用程序根据需求，可以自己添加一个模块名字）
>   > - power\_state：PM\_POWER\_MODULE\_STATE\_ON:启动AP; PM\_POWER\_MODULE\_STATE\_OFF:关闭AP

<a id="id4"></a>

## 获取当前启动AP是否成功的接口

> - pm\_mailbox\_communication\_state\_e bk\_pm\_cp1\_work\_state\_get()
>   :   - 返回值：
>         :   - 0x1:表示启动AP成功了
>             - 0x0:表示启动AP失败或者没有启动AP

<a id="apap"></a>

## 示例：启动AP和关闭AP

> - 启动AP： MULTIMEDIA模块：
>   \- bk\_pm\_module\_vote\_boot\_ap\_ctrl(PM\_BOOT\_AP\_MODULE\_NAME\_MULTIMEDIA,PM\_POWER\_MODULE\_STATE\_ON);
> - 关闭AP： MULTIMEDIA模块：
>   \- bk\_pm\_module\_vote\_boot\_ap\_ctrl(PM\_BOOT\_AP\_MODULE\_NAME\_MULTIMEDIA,PM\_POWER\_MODULE\_STATE\_OFF);

<a id="id5"></a>

## 如何查看启动AP是否成功或者关闭AP哪些模块投下电的票

> - 可以发送pm\_debug 8命令，通过log分析“pm\_cp1\_ctrl\_state:0x0”字段，详细参考 [低功耗问题分析](bk_Lowpower_problem_analysis.md) 。

备注

启动AP使用的module名字和使用完关闭AP的module名字需要一样，如果不一样，启动和关闭模块不对称，会出现不符合预期的。应用层没有专用模块名时，优先使用预留的 `PM_BOOT_AP_MODULE_NAME_USER`，不要复用已被多媒体或音频模块占用的模块名。
