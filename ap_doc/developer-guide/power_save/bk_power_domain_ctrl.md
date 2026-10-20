---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_power_domain_ctrl.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="ap"></a>

# AP侧电源域控制

<a id="id1"></a>

## 电源域控制策略

- AP侧应用通过 `bk_pm_module_vote_power_ctrl()` 接口控制业务模块对应的电源域。
- 接口以子模块为单位记录上、下电状态。同一父电源域中只要有一个子模块投上电票，父电源域就保持上电；所有子模块均投下电票后，父电源域才会下电。
- 模块开始工作前应先投上电票，停止工作并释放相关资源后再投下电票。
- 上电和下电必须使用同一个子模块枚举，避免父电源域因投票未释放而无法下电。
- 本接口只负责电源域投票，模块时钟、复位、引脚和中断等资源仍需由对应驱动完成配置和释放。

<a id="id2"></a>

## 支持控制的AP电源域

AP侧可控制以下四个父电源域：

| 父电源域 | 硬件控制位 | 可使用的子模块枚举 |
| --- | --- | --- |
| Video Post | `pwd_video_post` | `PM_POWER_SUB_DOMAIN_DPU`、`PM_POWER_SUB_DOMAIN_H26D`、`PM_POWER_SUB_DOMAIN_MIPI_DSI`、`PM_POWER_SUB_DOMAIN_DPHY`、`PM_POWER_SUB_DOMAIN_PERI`、`PM_POWER_SUB_DOMAIN_GPU` |
| H26E | `pwd_h26e` | `PM_POWER_SUB_DOMAIN_H26E` |
| ISP | `pwd_isp` | `PM_POWER_SUB_DOMAIN_ISP`、`PM_POWER_SUB_DOMAIN_MIPI_CSI` |
| NPU | `pwd_npu` | `PM_POWER_SUB_DOMAIN_NPU` |

Video Post中的DPU、H26D、MIPI DSI、DPHY、PERI和GPU共享同一个父电源域。例如DPU和H26D均已投上电票时，仅释放DPU的票不会关闭Video Post电源域；还需要释放H26D的票。

<a id="id3"></a>

## 配置AP侧默认关闭的电源域

`CONFIG_PM_AP_SUBPOWER_DOMAIN_DEFAULT_DISABLE` 宏用于控制是否在AP侧电源管理硬件初始化时关闭默认电源域。
将该宏配置为 `y` 后，AP侧默认关闭Video Post、H26E、ISP和NPU电源域：

```
#if CONFIG_PM_AP_SUBPOWER_DOMAIN_DEFAULT_DISABLE
    sys_hal_module_power_ctrl(POWER_DOMAIN_NAME_VIDEO_POST, POWER_MODULE_STATE_OFF);
    sys_hal_module_power_ctrl(POWER_DOMAIN_NAME_H26E, POWER_MODULE_STATE_OFF);
    sys_hal_module_power_ctrl(POWER_DOMAIN_NAME_ISP, POWER_MODULE_STATE_OFF);
    sys_hal_module_power_ctrl(POWER_DOMAIN_NAME_NPU, POWER_MODULE_STATE_OFF);
#endif
```

<a id="id4"></a>

## 电源状态枚举

`power_state` 参数使用 `pm_power_module_state_e`：

> - `PM_POWER_MODULE_STATE_ON`：上电，枚举值为0。
> - `PM_POWER_MODULE_STATE_OFF`：下电，枚举值为1。

<a id="id5"></a>

## 电源域控制接口

```
bk_err_t bk_pm_module_vote_power_ctrl(
    pm_power_module_name_e module,
    pm_power_module_state_e power_state);
```

参数说明：

> - `module`：需要投票的AP子模块，取值见“支持控制的AP电源域”。
> - `power_state`：需要设置的电源状态，使用 `PM_POWER_MODULE_STATE_ON` 或 `PM_POWER_MODULE_STATE_OFF`。

返回值：

> - `BK_OK`：接口调用成功。
> - 其他值：接口调用失败。

<a id="id6"></a>

## 使用示例

以下示例在H26D开始工作前打开Video Post电源域，并在H26D停止工作后释放电源域投票：

```
bk_err_t ret;

ret = bk_pm_module_vote_power_ctrl(PM_POWER_SUB_DOMAIN_H26D,
                                   PM_POWER_MODULE_STATE_ON);
if (ret != BK_OK) {
    return ret;
}

/* 初始化并使用H26D。 */

/* 停止H26D并释放时钟、中断等资源后，再投下电票。 */
ret = bk_pm_module_vote_power_ctrl(PM_POWER_SUB_DOMAIN_H26D,
                                   PM_POWER_MODULE_STATE_OFF);
```

备注

不要在其他共享同一父电源域的模块仍在工作时直接操作硬件 `pwd_*` 位。应统一通过电源域投票接口控制，由PM模块在最后一个子模块释放投票后关闭父电源域。
多媒体的相关电源域Video Post、H26E、ISP、NPU,在多媒体驱动内部开启该模块时会投票上电，关闭该模块时会投票下电。
一般情况下是不需要单独调用该接口关闭该电源域，只需要调用响应接口关闭该模块即可，例如关闭NPU,ISP。
