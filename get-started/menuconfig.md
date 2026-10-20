---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/get-started/menuconfig.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="menuconfig"></a>

<a id="bk7259-get-started-menuconfig"></a>

# Menuconfig 使用指南

本文介绍 BK7259 SDK 中 `menuconfig` 的使用方法，包括 AP/CP 菜单布局、配置保存方式、配置生效规则，以及应用层和外层 solution 工程如何加入自己的配置项。

<a id="id1"></a>

## 基本概念

`menuconfig` 是 BK7259 SDK 提供的交互式配置界面，用于查看和修改当前工程的 Kconfig 配置。工程编译时最终使用的是生成后的 `sdkconfig`、`sdkconfig.h` 和 `sdkconfig.cmake`，`menuconfig` 打开的也是同一份工程配置视图。

需要区分以下几类文件：

| 文件类型 | 作用 |
| --- | --- |
| `Kconfig` | 定义配置项，例如配置项名称、类型、默认值、依赖关系、帮助信息以及菜单显示位置。 |
| `Kconfig.projbuild` | 定义工程级额外配置。该文件通常作为项目级配置直接进入当前工程菜单，不建议用于普通组件配置收敛。 |
| SoC `defconfig` | 定义芯片或子系统默认配置，例如 AP 的 `ap/middleware/soc/bk7259_ap/bk7259_ap.defconfig`，CP 的 `cp/middleware/soc/bk7259/bk7259.defconfig`。 |
| 工程 `defconfig` | 定义当前工程相对 SoC 默认配置的差异，例如 `projects/app/ap/config/bk7259_ap/defconfig`。 |
| `sdkconfig` | 构建目录中生成的完整配置文件，编译和 `menuconfig` 都以它作为当前工程的最终配置。 |
| `sdkconfig.h` | 编译时包含的 C 头文件，代码中通过 `CONFIG_xxx` 宏使用配置结果。 |

重要

只有在当前工程 Kconfig 树中定义过的配置项，才能通过 `defconfig` 或 `menuconfig` 生效。手动在 `defconfig` 中写入一个不存在的 `CONFIG_xxx`，不会自动创建配置项。

<a id="id2"></a>

## 打开 menuconfig

BK7259 包含 AP 与 CP 两个子系统，二者独立生成配置和镜像。使用 `menuconfig` 时也需要分别打开 AP 或 CP 配置。

SDK 内置工程以 `app` 工程为例:

```
cd ~/armino/bk_avdk_smp

# 打开 AP 工程配置
make bk7259_ap_menuconfig PROJECT=app

# 打开 CP 工程配置
make bk7259_cp_menuconfig PROJECT=app
```

编译整个工程仍然使用:

```
make bk7259 PROJECT=app
```

如果使用 SDK 默认工程，`PROJECT=app` 可以省略。

外层 solution 工程需要在 solution 工程根目录下执行，例如 doorbell solution:

```
cd ~/armino/doorbell_solution_release

# 打开 doorbell 工程 AP 配置
make bk7259_ap_menuconfig PROJECT=doorbell

# 打开 doorbell 工程 CP 配置
make bk7259_cp_menuconfig PROJECT=doorbell
```

备注

从 SDK 目录打开 `menuconfig`，看到的是 SDK 当前工程上下文。外层 solution 的组件和项目配置，只有在 solution 工程根目录下打开对应工程的 `menuconfig` 时才会被纳入。

<a id="id3"></a>

## 常用快捷键

进入 `menuconfig` 后，界面顶部显示当前配置工程，中间显示菜单和配置项，底部显示常用快捷键。带 `--->` 的条目表示可以进入下一级菜单。

<a id="id10"></a>
![menuconfig overview](../../_assets/32ceaad3245a39270c30-menuconfig_overview.svg)

`menuconfig` 界面总览示意图

进入 `menuconfig` 后，可使用以下快捷键：

| 快捷键 | 说明 |
| --- | --- |
| `方向键` / `j` / `k` | 在菜单项之间移动。 |
| `Enter` | 进入子菜单，或编辑当前配置项。 |
| `Space` / `Y` / `N` | 切换 bool 类型配置项。 |
| `Esc` / `H` / `Backspace` | 返回上一级菜单。 |
| `/` | 搜索配置项，可按配置名称或提示文本查找。 |
| `?` | 查看当前配置项的详细信息，包括 `CONFIG` 名称、依赖关系和 help 信息。 |
| `F` | 显示或隐藏 help 信息。 |
| `C` | 显示或隐藏配置项名称，例如 `CONFIG_WIFI_ENABLE`。 |
| `A` | 显示所有配置项，包括当前依赖不满足或不可见的配置项。 |
| `S` | 保存完整 `sdkconfig`。 |
| `D` | 保存工程差异 `defconfig`，推荐用于把当前工程配置固化到源码工程中。 |
| `Q` | 退出 `menuconfig`。 |

<a id="id4"></a>

## 配置保存到哪里

`menuconfig` 中有两类保存方式，使用场景不同。

<a id="s"></a>

### `S` 保存完整配置

按 `S` 会保存完整 `sdkconfig`。该文件位于构建目录中，用于当前 build 目录后续编译。

完整 `sdkconfig` 适合临时调试，但不适合作为工程默认配置提交到源码仓库。原因是它包含大量由默认值计算出来的配置，文件较大，也容易受 SDK 默认值变化影响。

<a id="d"></a>

### `D` 保存工程差异配置

按 `D` 会保存当前工程相对 SoC 默认配置的差异，推荐用于产品工程或示例工程长期维护。默认保存路径如下：

| 子系统 | 工程差异配置路径 |
| --- | --- |
| AP | `projects/<project>/ap/config/bk7259_ap/defconfig` |
| CP | `projects/<project>/cp/config/bk7259/defconfig` |

外层 solution 工程的路径规则相同，只是 `projects` 目录位于 solution 仓库中，例如:

```
doorbell_solution_release/projects/doorbell/ap/config/bk7259_ap/defconfig
doorbell_solution_release/projects/doorbell/cp/config/bk7259/defconfig
```

备注

如果只是本地试验，可以只保存 `sdkconfig`。如果希望配置随工程长期保存、提交或给其他用户复现，应保存到工程 `defconfig`。

<a id="id5"></a>

## 配置加载与生效顺序

生成最终配置时，Kconfig 工具会先加载默认配置，再加载工程配置，最后在已有构建目录中继续加载已有 `sdkconfig`。因此最终编译结果以构建目录生成后的 `sdkconfig`、`sdkconfig.h` 为准。

典型加载顺序如下：

1. Kconfig 中定义的默认值。
2. SoC 默认配置，例如 AP 的 `bk7259_ap.defconfig` 或 CP 的 `bk7259.defconfig`。
3. 工程默认配置，例如 `projects/<project>/ap/config/bk7259_ap/defconfig`。
4. 构建目录中已有的 `sdkconfig`，如果存在，会继续作为当前工程配置加载。

因此，当修改了工程 `defconfig` 但发现 `menuconfig` 或编译结果没有变化时，建议先清理该工程构建目录，或重新打开 `menuconfig` 并保存配置。

重要

`menuconfig` 与编译使用的是同一个最终配置视图。正常情况下，从同一个工程上下文打开 `menuconfig` 看到的配置，与该工程编译出来的 `CONFIG_xxx` 是一致的。如果不一致，通常是因为打开了不同工程、旧 `sdkconfig` 覆盖了默认配置、配置项依赖不满足，或 `defconfig` 中写入了当前 Kconfig 树不存在的 symbol。

<a id="ap"></a>

## AP 菜单布局

AP 侧面向应用处理器，包含多媒体、显示、AI、应用服务等更多产品功能。当前 AP 顶层菜单按功能域组织：

<a id="id11"></a>
![AP menuconfig top menu](../../_assets/385316ee6c8ce54b1d87-menuconfig_ap_top.svg)

AP 侧 `menuconfig` 顶层菜单示意图

| 顶层菜单 | 主要内容 |
| --- | --- |
| `Build & Target` | 编译目标、版本类型、栈保护、代码放置策略等编译相关配置。 |
| `Board & SoC` | SoC、板级、架构、MPU、内存能力等硬件和芯片基础配置。 |
| `RTOS & Kernel` | FreeRTOS、任务调度、内核能力、系统启动相关配置。 |
| `System Services` | 系统服务、组件适配层、运行时公共服务等配置。 |
| `Device Drivers` | GPIO、UART、I2C、SPI、PWM、DMA、Flash、LCD、USB 等驱动配置。 |
| `Wireless Connectivity` | Wi-Fi、Bluetooth、无线能力开关和相关协议配置。 |
| `Network Services` | LWIP、hosted mode、网络协议和网络服务配置。 |
| 功能分组菜单 | 由组件 `Kconfig` 中的 `KCONFIG_GROUP` 自动生成，例如 Multimedia、Audio、Display、Storage、Power、Security 等。 |
| `Debug` | Assert、JTAG、SWD、日志、dump、调试探针等调试相关配置。 |
| `Demos` | SDK 示例、demo 和验证类功能配置。 |
| `Third Party` | 第三方库相关配置，例如外部开源库、编码库或通用工具库。 |
| `Solution & Product` | 外层 solution 或产品组件配置，例如 doorbell、dashboard、AI solution 中的应用组件。该菜单只在外层 solution 工程存在对应分组内容时显示。 |

AP 侧 `Solution & Product` 主要用于外层产品功能配置，只有在外层 solution 工程上下文中，且组件 Kconfig 被工程纳入时才会显示对应内容。

<a id="board-soc"></a>

### Board \& SoC 菜单布局

`Board & SoC` 用于收纳芯片、板级和基础架构相关配置。AP 侧主要包含两个子菜单：

<a id="id12"></a>
![Board and SoC menu](../../_assets/69cdfce0c9eaf4701a56-menuconfig_board_soc.svg)

`Board & SoC` 菜单示意图

| 子菜单 | 主要内容 |
| --- | --- |
| `SoC Configuration` | SoC 选择、SoC 字符串、CPU 数量、SMP core 数量、CPU ID offset、TCM size、TrustZone、SoC 级 workaround、UART 默认管脚等目标相关配置。 |
| `Architecture` | Core、Cortex-M、MPU、CMSIS、板级能力等架构和基础平台配置。 |

这些配置通常与芯片型号、内存布局、启动方式和板级硬件相关。普通应用功能不建议放在该菜单下，应用或产品功能应优先放到 `Solution & Product`、`Multimedia`、`Device Drivers` 等功能菜单中。

<a id="cp"></a>

## CP 菜单布局

CP 侧面向通信处理器，主要负责通信、基础系统服务和与 AP 的协同能力。CP 顶层菜单与 AP 保持类似的功能化布局，但不包含 AP 专用的 `Solution & Product` 顶层菜单。

| 顶层菜单 | 主要内容 |
| --- | --- |
| `Build & Target` | CP 编译版本、栈保护、代码放置策略等配置。 |
| `Board & SoC` | CP 侧 SoC、架构、板级基础配置。 |
| `RTOS & Kernel` | CP 侧 FreeRTOS、任务、内核和启动相关配置。 |
| `System Services` | CP 公共系统服务、兼容层和运行时服务。 |
| `Device Drivers` | CP 侧可用驱动配置。properties 库构建场景下，部分源码驱动菜单不会显示。 |
| `Wireless Connectivity` | Wi-Fi、Bluetooth、2.4G 等无线通信相关配置。 |
| `Network Services` | LWIP、hosted mode 和网络协议配置。 |
| 功能分组菜单 | 由 CP 侧组件 `KCONFIG_GROUP` 自动生成的功能菜单。 |
| `Debug` | Assert、JTAG、SWD、GPIO log、watchdog、dump 等调试和诊断配置。 |
| `Demos` | CP 侧 demo 或验证类配置。 |
| `Third Party` | CP 侧第三方库配置。 |

AP 与 CP 是两个独立配置空间。同名 `CONFIG_xxx` 如果分别出现在 AP 和 CP 工程中，也分别生成到各自的 `sdkconfig.h` 中。需要某个模块运行在 AP 还是 CP，应在对应子系统的 `menuconfig` 或工程 `defconfig` 中配置。

<a id="id6"></a>

## 应用层如何添加配置项

应用层组件通常通过 `Kconfig` 定义自己的配置项。以一个外层 solution 组件为例，目录结构可以是：

```
doorbell_solution_release/
    components/
        smart_lock/
            CMakeLists.txt
            Kconfig
            smart_lock.c
```

组件 `Kconfig` 示例：

```
# KCONFIG_GROUP: Solution & Product
menu "Smart Lock"

    config INTEGRATION_DOORBELL
        bool "Enable smart lock doorbell integration"
        default y
        help
            Enable integration between smart lock service and doorbell application.

endmenu
```

这里需要注意：

1. `config` 定义的名称不带 `CONFIG_` 前缀，例如写 `config INTEGRATION_DOORBELL`。
2. 在 C 代码、`defconfig` 和 `sdkconfig` 中使用时需要加 `CONFIG_` 前缀，例如 `CONFIG_INTEGRATION_DOORBELL`。
3. `help` 建议写清楚该配置项影响的功能、默认值原因和使用限制，方便用户在 `menuconfig` 中按 `?` 查看。
4. `depends on` 用于声明依赖条件。依赖不满足时，即使 `defconfig` 中写了 `CONFIG_xxx=y`，最终也不会打开。
5. `select` 会强制选择其它配置，使用时要谨慎，避免绕过被选择项自身的依赖。

<a id="id7"></a>

## 应用层菜单应该放在哪里

BK7259 当前使用 `KCONFIG_GROUP` 注释来将组件配置归类到功能菜单。该标记只影响 `menuconfig` 展示层级，不会改变 Kconfig symbol、默认值、依赖关系，也不会直接影响编译或运行行为。

常见写法如下：

```
# KCONFIG_GROUP: Solution & Product
```

或多级菜单：

```
# KCONFIG_GROUP: Solution & Product::Multimedia Service
```

分组建议：

| 组件类型 | 建议菜单 |
| --- | --- |
| 产品或 solution 专用组件 | `Solution & Product` |
| SDK 示例和验证 demo | `Demos` |
| 驱动能力 | `Device Drivers` |
| Wi-Fi、Bluetooth、2.4G | `Wireless Connectivity` |
| LWIP、网络协议、网络应用服务 | `Network Services` |
| OS、任务、调度、内核能力 | `RTOS & Kernel` |
| log、dump、assert、调试开关 | `Debug` |
| 第三方库 | `Third Party` |

备注

`KCONFIG_GROUP` 需要放在 `Kconfig` 文件前几行。构建脚本只读取文件开头附近的分组标记。

<a id="kconfig-projbuild"></a>

## Kconfig.projbuild 的使用场景

`Kconfig.projbuild` 适合放工程级额外配置，例如某个具体产品工程的项目级菜单、演示工程参数或不属于普通组件的全局选项。它会随工程配置一起 source 到 Kconfig 树中。

与普通组件 `Kconfig` 的建议分工如下：

| 文件 | 建议用途 |
| --- | --- |
| `components/<component>/Kconfig` | 组件自身功能开关，推荐通过 `KCONFIG_GROUP` 放到合适功能菜单。 |
| `projects/<project>/ap/Kconfig.projbuild` | AP 工程级额外配置，可作为独立项目菜单显示。 |
| `projects/<project>/cp/Kconfig.projbuild` | CP 工程级额外配置，可作为独立项目菜单显示。 |

不要为了让工程级配置进入 `Solution & Product` 而强行把 `Kconfig.projbuild` 改成普通 `Kconfig`。如果它表达的是项目级额外配置，保留 `Kconfig.projbuild` 更清晰。

<a id="solution"></a>

## 外层 solution 工程接入规则

外层 solution 工程通常具有自己的 `projects` 和 `components` 目录，SDK 作为下层依赖被引入。只要 solution 工程构建时将外层组件目录加入构建系统，这些组件中的 `Kconfig` 就会被 SDK 的 Kconfig 生成流程发现。

<a id="id13"></a>
![Solution menuconfig top menu](../../_assets/c1de9ca3feaefc00c038-menuconfig_solution_top.svg)

外层 solution 工程 `menuconfig` 顶层菜单示意图

其中，`Solution & Product` 用于收纳外层 solution 的产品组件配置；如果工程存在 `Kconfig.projbuild` 定义的项目级菜单，该菜单会作为项目额外配置独立显示。

推荐规则如下：

1. 普通产品组件在 `components/<component>/Kconfig` 中定义配置项。
2. 如果希望组件显示在 AP 的产品菜单下，在 `Kconfig` 文件开头添加 `# KCONFIG_GROUP: Solution & Product`。
3. 如果是项目级额外配置，保留在 `projects/<project>/ap/Kconfig.projbuild` 或 `projects/<project>/cp/Kconfig.projbuild`。
4. AP 专用 solution 组件只需要在 AP 工程中启用，不需要放入 CP 菜单。
5. 打开外层工程 `menuconfig` 时，应在 solution 工程根目录执行 `make bk7259_ap_menuconfig PROJECT=<project>`。

示例：

```
solution_ai/
    components/
        robot_ctrl_service/
            Kconfig                  # 添加 KCONFIG_GROUP 后进入 Solution & Product
    projects/
        beken_robot/
            ap/
                Kconfig.projbuild    # 项目级额外配置，保持独立
                config/bk7259_ap/defconfig
            cp/
                config/bk7259/defconfig
```

重要

从 SDK 自身工程打开 `menuconfig` 时，不会自动显示某个外层 solution 的组件菜单。必须从对应 solution 工程上下文打开，才能看到该 solution 的组件和项目配置。

<a id="id8"></a>

## 如何判断配置是否生效

配置是否生效，以最终生成文件为准：

| 文件 | 说明 |
| --- | --- |
| `build/.../sdkconfig` | 当前工程完整配置。 |
| `build/.../config/sdkconfig.h` | C 代码实际包含的配置宏。 |
| `build/.../config/sdkconfig.cmake` | CMake 构建使用的配置变量。 |

如果 `defconfig` 中写了某项配置，但 `menuconfig` 中没有打开，可按以下顺序排查：

1. 确认当前打开的是同一个工程和同一个子系统，例如 AP 与 CP 不要混用。
2. 在 `menuconfig` 中按 `/` 搜索配置项名称，确认该 symbol 存在。
3. 按 `?` 查看依赖关系，确认 `depends on` 条件满足。
4. 检查外层 solution 的组件是否已被当前工程构建系统纳入。
5. 清理旧 build 目录后重新打开 `menuconfig`，避免旧 `sdkconfig` 覆盖工程 `defconfig`。

<a id="id9"></a>

## 常见问题

<a id="defconfig-y-menuconfig-n"></a>

### 为什么 defconfig 写了 y，但 menuconfig 显示为 n？

通常有三种原因：配置项未在当前 Kconfig 树中定义；依赖条件不满足；旧 `sdkconfig` 覆盖了工程 `defconfig`。可以通过 `menuconfig` 搜索、查看 help 和清理 build 目录定位。

<a id="solution-solution-product"></a>

### 为什么外层 solution 组件没有出现在 Solution \& Product？

请确认：

1. 是在 solution 工程根目录打开 `menuconfig`，不是在纯 SDK 工程目录打开。
2. 组件目录已被当前工程构建系统纳入。
3. 组件 `Kconfig` 文件开头包含 `# KCONFIG_GROUP: Solution & Product`。
4. 该组件是 AP 工程可见组件。当前 `Solution & Product` 是 AP 侧产品菜单。

<a id="kconfig-group"></a>

### KCONFIG\_GROUP 会改变编译行为吗？

不会。`KCONFIG_GROUP` 是一行注释，Kconfig 解析器会忽略它。BK7259 的构建脚本会读取这行注释，用来决定该组件在 `menuconfig` 中显示到哪个功能菜单下。它不会改变 `CONFIG` 名称、默认值、依赖关系或运行行为。

<a id="defconfig-menuconfig"></a>

### 应该手动改 defconfig，还是用 menuconfig？

推荐优先使用 `menuconfig`。因为 `menuconfig` 会展示依赖关系，并且只允许配置当前工程可见的选项。手动修改 `defconfig` 时，容易写入不存在的 symbol，或打开一个依赖不满足的选项。

如果需要提交工程默认配置，建议使用 `menuconfig` 修改后按 `D` 保存工程差异 `defconfig`，再提交对应工程目录下的 `defconfig`。

<a id="ap-cp"></a>

### AP 和 CP 要配置同一个功能时应该怎么做？

AP 和 CP 配置空间独立。需要模块运行在哪个子系统，就打开对应子系统的 `menuconfig` 并配置。对于只有一份硬件资源的外设，应避免 AP 与 CP 同时启用冲突配置，具体归属以产品设计和驱动支持情况为准。
