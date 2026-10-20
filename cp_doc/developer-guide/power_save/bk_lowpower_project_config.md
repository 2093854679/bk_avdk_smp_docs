---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_lowpower_project_config.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 低功耗工程配置说明

本章节以 `projects/pm/pm` 工程为例，说明支持低功耗时CP侧和AP侧需要配置的主要宏，以及CP侧唤醒GPIO的配置方法。

<a id="cp"></a>

## CP侧工程配置

CP侧配置文件为 `projects/pm/pm/cp/config/bk7259/defconfig`。低功耗相关配置如下：

```
# platform
CONFIG_SOC_SMP=n
CONFIG_CPU_ID_OFFSET=0
CONFIG_FREERTOS_V10=y
CONFIG_FREERTOS_SMP=n
CONFIG_PSRAM=y
CONFIG_PSRAM_AS_SYS_MEMORY=n

# PM
CONFIG_FREERTOS_USE_TICKLESS_IDLE=2
CONFIG_PM_AP_POWERDOWN_WHEN_LV=y
CONFIG_PM_ONLY_CP_ENABLE=y
CONFIG_DEEP_LV=y
CONFIG_DEEP_LV_DEBUG_GPIO=n
CONFIG_DEEP_LV_DEBUG_LOG=n
CONFIG_AON_RTC=y
CONFIG_GPIO_WAKEUP_SUPPORT=y
CONFIG_GPIO_DYNAMIC_WAKEUP_SUPPORT=y
CONFIG_TOUCH=n
CONFIG_TOUCH_TEST=n
CONFIG_PM_POWER_VOTE_RECORD=n
CONFIG_PM_CLOCK_VOTE_RECORD=n
CONFIG_CKMN_TEST=n
CONFIG_OPTIMIZE_AON_CURRENT=y
CONFIG_AON_LDO_SEL=2
CONFIG_DEBUG_VERSION=n
CONFIG_PM_CURRENT_OPTIMIZE_XTAL_RX_TX_ANABUF=y
CONFIG_CPU_DEFAULT_FREQ_60M=y
CONFIG_PM_CP_PERI_CLK_DEFAULT_OFF=y
CONFIG_PM_XTAL_RX_TX_ANABUF_DEFAULT_OFF=y

# WIFI
CONFIG_STA_PS=y

# BLE
CONFIG_BLUETOOTH=y
CONFIG_BLUETOOTH_SUPPORT_LPO_ROSC=y
CONFIG_BLUETOOTH_BLE_SLAVE_ONLY=y
CONFIG_BLE_LV_SUPPORT=y
CONFIG_BTDM_CONTROLLER_ONLY=n
CONFIG_BLUETOOTH_SUPPORT_AP_PWD_ALL=y
```

主要配置说明如下：

> - `CONFIG_SOC_SMP=n`、`CONFIG_FREERTOS_SMP=n`、`CONFIG_PM_ONLY_CP_ENABLE=y`：CP使用非SMP模式运行，低功耗期间以CP为常驻核，允许AP关闭。
> - `CONFIG_FREERTOS_USE_TICKLESS_IDLE=2`：使能FreeRTOS Tickless Idle，空闲时停止周期Tick，为系统进入睡眠创造条件。
> - `CONFIG_PM_AP_POWERDOWN_WHEN_LV=y`：系统进入低压睡眠时关闭AP电源。
> - `CONFIG_DEEP_LV=y`：使能Deep Low Voltage低功耗流程。
> - `CONFIG_DEEP_LV_DEBUG_GPIO`、`CONFIG_DEEP_LV_DEBUG_LOG`：分别控制Deep LV GPIO时序标记和AON寄存器快照日志。测量正式功耗时建议保持关闭，避免调试功能影响结果。
> - `CONFIG_AON_RTC=y`：使能AON RTC，可用于低功耗计时和RTC唤醒。
> - `CONFIG_GPIO_WAKEUP_SUPPORT=y`：使能GPIO低功耗唤醒能力。
> - `CONFIG_GPIO_DYNAMIC_WAKEUP_SUPPORT=y`：使能GPIO唤醒源的动态注册能力，依赖 `CONFIG_GPIO_WAKEUP_SUPPORT`。
> - `CONFIG_TOUCH=n`、`CONFIG_TOUCH_TEST=n`：默认关闭Touch驱动及测试功能；需要Touch唤醒或测试时再将对应宏配置为 `y`。
> - `CONFIG_PM_POWER_VOTE_RECORD`、`CONFIG_PM_CLOCK_VOTE_RECORD`：记录电源票和时钟票，便于调试。示例为降低额外开销将其关闭，定位低功耗问题时可临时打开。
> - `CONFIG_CKMN_TEST=n`：默认关闭时钟监测测试功能，需要相应测试能力时再配置为 `y`。
> - `CONFIG_OPTIMIZE_AON_CURRENT=y`：低压睡眠期间降低AON LDO电压，以优化AON域电流。
> - `CONFIG_AON_LDO_SEL=2`：设置AON LDO档位为2，对应0.7 V。修改前需结合芯片、电源和板级条件验证稳定性。
> - `CONFIG_PM_CURRENT_OPTIMIZE_XTAL_RX_TX_ANABUF=y`：优化XTAL RX/TX模拟缓冲相关的低功耗电流。
> - `CONFIG_CPU_DEFAULT_FREQ_60M=y`：将CP默认CPU频率设置为60 MHz。
> - `CONFIG_PM_CP_PERI_CLK_DEFAULT_OFF=y`：CP启动早期默认关闭未使用的外设时钟。
> - `CONFIG_PM_XTAL_RX_TX_ANABUF_DEFAULT_OFF=y`：默认关闭XTAL RX/TX模拟缓冲，使用相关功能前需由业务按需打开。
> - `CONFIG_PSRAM=y`、`CONFIG_PSRAM_AS_SYS_MEMORY=n`：使能PSRAM，但不将其作为CP系统内存使用。
> - `CONFIG_STA_PS=y`：使能Wi-Fi STA省电能力。
> - `CONFIG_BLUETOOTH_SUPPORT_LPO_ROSC=y`、`CONFIG_BLE_LV_SUPPORT=y`：使能BLE低功耗时钟和低压睡眠支持。
> - `CONFIG_BLUETOOTH_BLE_SLAVE_ONLY=y`：将BLE业务限制为从设备角色，适用于示例的低功耗使用方式。
> - `CONFIG_BLUETOOTH_SUPPORT_AP_PWD_ALL=y`：允许Bluetooth在AP完全掉电的场景下工作。

备注

上述配置是 `projects/pm/pm` 示例工程的低功耗配置组合。`TOUCH`、`TOUCH_TEST` 和 `CKMN_TEST` 默认关闭，需要对应唤醒源或测试功能时再开启；改变AON LDO档位、默认关闭时钟或模拟缓冲后，必须完成目标板稳定性和功能验证。

<a id="cpgpio"></a>

## CP侧唤醒GPIO配置

CP侧GPIO配置文件为 `projects/pm/pm/cp/config/bk7259/usr_gpio_cfg.h`。该文件在CP侧只用于声明需要中断的GPIO以及配置UART0引脚；其他GPIO的复用、上下拉和输出电平等设置应在AP侧完成。

例如，将GPIO17声明为下降沿唤醒输入，需要在 `GPIO_DEFAULT_DEV_CONFIG` 中加入：

```
{GPIO_17, GPIO_SECOND_FUNC_ENABLE, GPIO_DEV_GPIO_INPUT,
 GPIO_DEV_GPIO_INPUT, GPIO_PULL_DISABLE, GPIO_INT_DISABLE,
 GPIO_INT_TYPE_FALLING_EDGE, GPIO_LOW_POWER_DISCARD_IO_STATUS,
 GPIO_DRIVER_CAPACITY_3, GPIO_INIT_ENABLE},\
```

配置项含义如下：

> - `GPIO_17`：选择GPIO17。
> - `GPIO_DEV_GPIO_INPUT`：将主功能和分时功能配置为GPIO输入。
> - `GPIO_PULL_DISABLE`：关闭内部上下拉；如果板级输入可能悬空，应根据外部电路选择合适的上下拉。
> - `GPIO_INT_TYPE_FALLING_EDGE`：指定下降沿触发类型。
> - `GPIO_INIT_ENABLE`：启动时应用该GPIO配置。

工程配置只完成GPIO声明。运行时还必须注册GPIO17并设置GPIO为系统唤醒源：

```
bk_gpio_register_wakeup_source(GPIO_17, GPIO_INT_TYPE_FALLING_EDGE);
bk_pm_wakeup_source_set(PM_WAKEUP_SOURCE_INT_GPIO, NULL);
```

进入睡眠模式时，再按业务流程完成睡眠投票：

```
bk_pm_module_vote_sleep_ctrl(PM_SLEEP_MODULE_NAME_APP, 0x1, 0x0);
```

若进入深度睡眠，则在配置唤醒源后调用：

```
bk_pm_sleep_mode_set(PM_MODE_DEEP_SLEEP);
```

`usr_gpio_cfg.h` 中的触发类型应与 `bk_gpio_register_wakeup_source()` 传入的触发类型保持一致。GPIO17被其他外设复用时，还需要先解除冲突；同时确保睡眠前GPIO电平不处于持续有效的唤醒状态，否则系统可能无法稳定进入低功耗或会立即唤醒。

<a id="ap"></a>

## AP侧工程配置

AP侧配置文件为 `projects/pm/pm/ap/config/bk7259_ap/defconfig`。低功耗相关配置如下：

```
CONFIG_FREERTOS_USE_TICKLESS_IDLE=2
CONFIG_GPIO_WAKEUP_SUPPORT=y
CONFIG_GPIO_DYNAMIC_WAKEUP_SUPPORT=y
CONFIG_PM_AP_SUBPOWER_DOMAIN_DEFAULT_DISABLE=y
CONFIG_PM_AP_CPU_FRQ_DEFAUL=y
CONFIG_BLUETOOTH_HOST_ONLY=n
CONFIG_BLUETOOTH_SUPPORT_AP_PWD_ALL=y
```

各配置的作用如下：

> - `CONFIG_FREERTOS_USE_TICKLESS_IDLE=2`：使能AP侧FreeRTOS Tickless Idle。
> - `CONFIG_GPIO_WAKEUP_SUPPORT=y`、`CONFIG_GPIO_DYNAMIC_WAKEUP_SUPPORT=y`：使能AP侧GPIO唤醒及动态配置能力。
> - `CONFIG_PM_AP_SUBPOWER_DOMAIN_DEFAULT_DISABLE=y`：AP电源管理初始化时默认关闭VIDEO\_POST、H26E、ISP和NPU子电源域，业务使用对应模块前需按流程重新上电。
> - `CONFIG_PM_AP_CPU_FRQ_DEFAUL=y`：AP初始化结束时投票设置默认CPU频率。
> - `CONFIG_BLUETOOTH_HOST_ONLY=n`：AP侧不使用仅Host模式。
> - `CONFIG_BLUETOOTH_SUPPORT_AP_PWD_ALL=y`：使能AP完全掉电场景下的Bluetooth协同支持。

完成CP和AP配置后，还需要由应用关闭不使用的音频、视频、LCD、CPU及外设，并正确配置电源票、时钟票和睡眠票。仅设置 `defconfig` 宏不会自动保证系统进入最低功耗状态。
