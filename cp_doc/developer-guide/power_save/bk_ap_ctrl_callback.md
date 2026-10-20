---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7259/zh_CN/v4.0.1/developer-guide/power_save/bk_ap_ctrl_callback.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: CP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="cpap"></a>

# CP侧AP上下电回调使用说明

<a id="id1"></a>

## 概述

CP侧应用可以通过AP上下电回调接口，接收AP电源状态切换通知。典型用途包括：

> - AP上电后恢复CP与AP之间的通信状态，或通知依赖AP的CP侧模块。
> - AP下电后清理CP侧保存的AP相关状态，或停止向AP发送数据。

接口声明和回调类型定义位于 `include/modules/pm.h`。回调在CP侧电源管理流程中同步执行，不会在AP侧执行。

<a id="id2"></a>

## 回调函数类型

```
   typedef void (*ap_ctrl_callback_t)(void *arg);

   typedef enum {
       PM_AP_CTRL_CB_TYPE_POWER_ON = 0,
       PM_AP_CTRL_CB_TYPE_POWER_OFF = 1,
   } pm_ap_ctrl_cb_type_t;

- ``arg``：注册时传入的用户参数，系统调用回调时原样传回。
- ``PM_AP_CTRL_CB_TYPE_POWER_ON``：注册AP上电回调。
- ``PM_AP_CTRL_CB_TYPE_POWER_OFF``：注册AP下电回调。
```

<a id="id3"></a>

## 注册接口

```
bk_err_t bk_pm_ap_ctrl_callback_register(
    ap_ctrl_callback_t callback,
    void *arg,
    pm_ap_ctrl_cb_type_t type);
```

参数说明：

> - `callback`：需要注册的回调函数，不能为 `NULL`。
> - `arg`：传递给回调函数的用户参数，可以为 `NULL`。该参数由应用管理，系统不会复制或释放其指向的数据。
> - `type`：需要监听的AP电源事件类型。

返回值：

> - `BK_OK`：注册成功。
> - `-1`：`callback` 为 `NULL`。
> - `-2`：回调节点内存申请失败。

如果同一模块需要同时监听AP上电和下电，必须使用不同的 `type` 分别注册两次。新注册的回调被插入链表头部，因此同一类型的多个回调按照注册顺序的逆序执行。

<a id="id4"></a>

## 注销接口

```
bk_err_t bk_pm_ap_ctrl_callback_unregister(
    ap_ctrl_callback_t callback,
    pm_ap_ctrl_cb_type_t type);
```

参数说明：

> - `callback`：注册时使用的回调函数，不能为 `NULL`。
> - `type`：注册时使用的回调类型。

返回值：

> - `BK_OK`：注销成功。
> - `-1`：`callback` 为 `NULL`。
> - `-2`：未找到同时匹配 `callback` 和 `type` 的回调节点。

注销时必须同时保证回调函数和回调类型与注册时一致。接口不使用 `arg` 匹配节点；如果重复注册相同的 `callback` 和 `type`，每次注销只删除一个匹配节点。

<a id="id5"></a>

## 系统调用时机

<a id="ap"></a>

### AP上电回调

系统在AP上电启动流程中执行 `PM_AP_CTRL_CB_TYPE_POWER_ON` 类型的回调：

> - 未使能 `CONFIG_PM_AP_FAST_BOOT_ENABLE` 时，在 `bk_start_ap_system()` 返回后执行，然后系统继续等待AP上报启动成功。
> - 使能 `CONFIG_PM_AP_FAST_BOOT_ENABLE` 时，在AP上报 `boot_success`、调度器恢复就绪后执行。

因此，普通启动配置下收到上电回调只表示AP启动动作已经发起，不能据此假设AP业务、跨核服务或邮箱接收端已经全部初始化完成。应用如需立即与AP通信，还应使用对应模块的就绪握手或状态检查机制。

<a id="id6"></a>

### AP下电回调

当所有AP启动投票均已释放，系统等待AP进入可下电状态并关闭AP电源域。电源域关闭完成后，系统执行 `PM_AP_CTRL_CB_TYPE_POWER_OFF` 类型的回调。

该回调用于通知CP侧模块AP已经下电。不要在下电回调中访问AP内存、向AP发送消息，或执行依赖AP仍在线的操作；需要与AP交互的清理工作应在AP进入可下电状态前完成。

<a id="id7"></a>

## 调用示例

下面的示例同时注册AP上电和下电回调，并在模块退出时注销。实际应用应在模块初始化阶段、AP可能发生上下电切换之前完成注册。

```
#include <components/log.h>
#include <modules/pm.h>
#include <os/os.h>

#define TAG "ap_cb_demo"

typedef struct {
    uint32_t module_id;
} ap_callback_context_t;

static ap_callback_context_t s_ap_cb_context = {
    .module_id = 1,
};

static void ap_power_on_callback(void *arg)
{
    ap_callback_context_t *context = (ap_callback_context_t *)arg;

    BK_LOGI(TAG, "AP power on, module=%u\r\n", context->module_id);

    /*
     * 普通启动配置下，AP业务可能尚未完全就绪。
     * 如需跨核通信，应在此触发业务自己的就绪检查或握手。
     */
}

static void ap_power_off_callback(void *arg)
{
    ap_callback_context_t *context = (ap_callback_context_t *)arg;

    BK_LOGI(TAG, "AP power off, module=%u\r\n", context->module_id);

    /* 这里只清理CP侧状态，不再访问AP或向AP发送消息。 */
}

bk_err_t ap_callback_demo_init(void)
{
    bk_err_t ret;

    ret = bk_pm_ap_ctrl_callback_register(
        ap_power_on_callback,
        &s_ap_cb_context,
        PM_AP_CTRL_CB_TYPE_POWER_ON);
    if (ret != BK_OK) {
        BK_LOGE(TAG, "register AP power-on callback failed: %d\r\n", ret);
        return ret;
    }

    ret = bk_pm_ap_ctrl_callback_register(
        ap_power_off_callback,
        &s_ap_cb_context,
        PM_AP_CTRL_CB_TYPE_POWER_OFF);
    if (ret != BK_OK) {
        BK_LOGE(TAG, "register AP power-off callback failed: %d\r\n", ret);
        bk_pm_ap_ctrl_callback_unregister(
            ap_power_on_callback,
            PM_AP_CTRL_CB_TYPE_POWER_ON);
        return ret;
    }

    return BK_OK;
}

void ap_callback_demo_deinit(void)
{
    bk_err_t ret;

    ret = bk_pm_ap_ctrl_callback_unregister(
        ap_power_off_callback,
        PM_AP_CTRL_CB_TYPE_POWER_OFF);
    if (ret != BK_OK) {
        BK_LOGW(TAG, "unregister AP power-off callback failed: %d\r\n", ret);
    }

    ret = bk_pm_ap_ctrl_callback_unregister(
        ap_power_on_callback,
        PM_AP_CTRL_CB_TYPE_POWER_ON);
    if (ret != BK_OK) {
        BK_LOGW(TAG, "unregister AP power-on callback failed: %d\r\n", ret);
    }
}
```

<a id="id8"></a>

## 应用注意事项

> - 注册成功后，回调及 `arg` 指向的数据必须在注销完成前保持有效。不要把局部变量地址作为长期使用的 `arg`。
> - 回调由CP侧AP电源管理流程同步调用。回调应尽快返回，不要长时间阻塞、等待AP响应、执行耗时操作或进入无限等待，否则会延长甚至阻塞AP上下电流程。
> - 不要在回调执行期间注册或注销AP上下电回调，也不要在回调函数内部注销自身。当前回调链表遍历不支持此类修改，可能造成链表节点失效。
> - 模块退出或其上下文即将释放时应先注销回调，并确保此时没有AP上下电回调正在执行。
> - 接口允许重复注册，不会自动去重。应用应记录注册状态，避免同一回调被意外执行多次；如果发生重复注册，需要对应注销多次。
> - 上电和下电是两个独立的回调类型。注销其中一种类型不会影响另一种类型。
> - 应检查注册和注销接口返回值。注册第二个回调失败时，应回滚已经成功的第一个注册，避免模块处于部分初始化状态。
> - 应传入枚举中定义的有效 `type`。接口当前不会主动校验枚举范围，错误类型将导致回调无法在正常上下电流程中执行。

备注

这些接口只提供AP电源状态切换通知，不负责发起AP上电或下电。控制AP上下电请使用 `bk_pm_module_vote_boot_ap_ctrl()`，详细用法参考 [如何启动和关闭AP](bk_vote_boot_ap.md)。
