---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/power_save/bk_wakeup_source.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="deepsleep"></a>

# 获取低压和deepsleep的唤醒源

<a id="id1"></a>

## 1 功能概述

本模块提供获取系统从不同睡眠模式唤醒时的唤醒源信息的接口。支持获取深度睡眠（deepsleep）和低压睡眠（low voltage）两种模式的唤醒源。

低压睡眠唤醒源类型包括：

- PM\_WAKEUP\_SOURCE\_INT\_GPIO：GPIO唤醒
- PM\_WAKEUP\_SOURCE\_INT\_RTC：RTC唤醒
- PM\_WAKEUP\_SOURCE\_INT\_TOUCHED：触摸唤醒
- PM\_WAKEUP\_SOURCE\_INT\_WIFI：WIFI唤醒
- PM\_WAKEUP\_SOURCE\_INT\_BT：BT唤醒

深度睡眠唤醒源类型包括：

- PM\_WAKEUP\_SOURCE\_INT\_GPIO：GPIO唤醒
- PM\_WAKEUP\_SOURCE\_INT\_RTC：RTC唤醒
- PM\_WAKEUP\_SOURCE\_INT\_TOUCHED：触摸唤醒
- PM\_WAKEUP\_SOURCE\_INT\_NONE：无唤醒源

<a id="api"></a>

## 2 API接口说明

<a id="id2"></a>

### 获取深度睡眠唤醒源

**函数原型**

```
pm_wakeup_source_e bk_pm_deep_sleep_wakeup_source_get(void)
```

**功能描述**

获取系统从深度睡眠（deepsleep）状态唤醒时的唤醒源。

**参数说明**

- 无

**返回值**

- pm\_wakeup\_source\_e：唤醒源类型，返回值为上述深度睡眠唤醒源类型之一

**使用说明**

- 该接口用于在系统从深度睡眠唤醒后，查询是哪个唤醒源触发的唤醒
- 通常在唤醒回调函数中调用此接口，以便根据不同的唤醒源做相应的处理
- 在SMP架构中，AP侧通过mailbox从CP侧获取唤醒源信息

**示例代码**

```
pm_wakeup_source_e source = bk_pm_deep_sleep_wakeup_source_get();

switch(source) {
    case PM_WAKEUP_SOURCE_INT_GPIO:
        // 处理GPIO唤醒
        break;
    case PM_WAKEUP_SOURCE_INT_RTC:
        // 处理RTC唤醒
        break;
    default:
        break;
}
```

<a id="id3"></a>

### 获取低压睡眠唤醒源

**函数原型**

```
pm_wakeup_source_e bk_pm_exit_low_vol_wakeup_source_get(void)
```

**功能描述**

获取系统从低压睡眠（low voltage）状态唤醒时的唤醒源。

**参数说明**

- 无

**返回值**

- pm\_wakeup\_source\_e：唤醒源类型，返回值为上述低压睡眠唤醒源类型之一

**使用说明**

- 该接口用于在系统从低压睡眠唤醒后，查询是哪个唤醒源触发的唤醒
- 通常在唤醒回调函数中调用此接口，以便根据不同的唤醒源做相应的处理
- 在SMP架构中，AP侧通过mailbox从CP侧获取唤醒源信息
- 可以配合GPIO、RTC、触摸等唤醒源使用

**示例代码**

```
pm_wakeup_source_e source = bk_pm_exit_low_vol_wakeup_source_get();

switch(source) {
    case PM_WAKEUP_SOURCE_INT_GPIO:
        // 处理GPIO唤醒
        break;
    case PM_WAKEUP_SOURCE_INT_RTC:
        // 处理RTC唤醒
        break;
    default:
        break;
}
```

备注

- 这两个接口只能获取唤醒源，不能设置唤醒源
- 在SMP架构中，唤醒源信息由CP侧管理，AP侧需要通过mailbox通信获取
