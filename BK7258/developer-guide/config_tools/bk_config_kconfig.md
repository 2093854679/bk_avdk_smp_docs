---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7258/zh_CN/v3.1.1/developer-guide/config_tools/bk_config_kconfig.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: SMP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="kconfig"></a>

<a id="bk-config-kconfig"></a>

# Kconfig 配置

本节介绍 Armino Kconfig 使用过程中常见问题。

<a id="id1"></a>

## Kconfig 配置文件

Armino Kconfig 组织如下图所示：

```
- armino/
    - ap/
        - components/
            - c1/
                - Kconfig
        - middleware/
            - soc/
                - bk7258_ap/
                    - bk7258_ap.defconfig
    - cp/
        - components/
            - c1/
                - Kconfig
        - middleware/
            - soc/
                - bk7258/
                    - bk7258.defconfig
    - projects/
        - my_project/
            - ap/
                - config/
                    - bk7258_ap/config
                - Kconfig.projbuild
                - components/
                    - c2/
                        - Kconfig
            - cp/
                - config/
                    - bk7258/config
```

可以将这些文件归为两类：

> - 配置定义文件:
>
>   - Kconfig \- 通常定义在组件中。
>   - Kconfig.projbuild \- 定义在组件或者工程目录下。
> - 配置修改文件:
>
>   - ap/middleware/boards/bk7258\_ap/bk7258\_ap.defconfig \- Armino 提供的 BK7258 AP 默认配置。
>   - cp/middleware/boards/bk7258/bk7258.defconfig \- Armino 提供的 BK7258 CP 默认配置。
>   - projects/xx/ap/config/bk7258\_ap/config \- 工程中 BK7258 AP 专有配置。
>   - projects/xx/cp/config/bk7258/config \- 工程中 BK7258 CP 专有配置。

重要

特定配置项只有在 Kconfig/Kconfig.projbuild 中定义之后才能通过配置修改文件去修改该配置，
如果偿试修改一个未定义的配置，则不会在 sdkconfig.h 中生成任何定义。

备注

Kconfig.projbuild 是针对 menuconfig 来设计的，当向 Kconfig.projbuild 中增加一项时，
会在 menuconfig 顶层菜单中显示该配置项。BK7258 不支持 menuconfig，因此 Kconfig.projbuild
与 Kconfig 作用相同。

备注

在Kconfig文件中定义的配置项名称，在config、defconfig和C代码中使用需要加上 `CONFIG_` 前缀。

备注

在配置修改文件（如 `config` 和 `defconfig`）中，您可能会看到如下格式的配置项：

- `CONFIG_XXX=y` 表示该配置项已启用
- `CONFIG_XXX=n` 表示该配置项已禁用
- `# CONFIG_XXX is not set` 表示该配置项未设置（等同于禁用状态）

`# CONFIG_XXX is not set` 是 Kconfig 系统生成的注释格式，用于明确表示某个配置项未被设置。
这种格式与 `CONFIG_XXX=n` 在功能上等效，都表示该配置项处于禁用状态。

在 Armino AP 工程中，Kconfig 配置优先级为:

> bk7258\_ap/config \> bk7258.defconfig \> 配置定义文件

在 Armino CP 工程中，Kconfig 配置优先级为:

> bk7258/config \> bk7258.defconfig \> 配置定义文件

<a id="menuconfig"></a>

<a id="bk-config-menuconfig"></a>

## menuconfig 支持

BK7258 Kconfig 配置支持 menuconfig 配置。

以app工程为例
配置ap工程，输入命令如下:

```
make bk7258_ap_menuconfig PROJECT=app
```

保存后，配置将保存到projects/app/ap/config/bk7258\_ap/config

配置cp工程，输入命令如下:

```
make bk7258_cp_menuconfig PROJECT=app
```

保存后，配置将保存到projects/app/ap/config/bk7258\_cp/config

menuconfig中常用快捷键如下:

```
SPACE/Enter 选中/取消
S 保存配置
O 载入配置
? 查看配置详细信息
/ 搜索并跳转
F 切换帮助信息显示
C 切换配置名称显示
A 显示所有配置
Q 离开
ESC 返回
```

备注

如果在solution工程中，在工程目录下输入 make bk7258\_ap\_menuconfig 来进行ap侧 menuconfig配置，输入 make bk7258\_cp\_menuconfig 来进行cp侧 menuconfig配置。

<a id="id2"></a>

## 配置依赖

相互依赖的配置项自动更改成正确的值，仅发生在使用 menuconfig 配置时，建议使用menuconfig来配置依赖的配置项。
当手动通过配置修改文件更改某项配置时，与该项配置相互依赖的配置不会自动更改。

重要

在 Armino 中所有配置项均需显式指定，或者使用默认值。

<a id="cmakelists-txt-kconfig"></a>

## CMakeLists.txt 中使用 Kconfig

在 CMakeLists.txt 中可直接使用 Kconfig 中定义的配置项，唯一要注意的问题不要将
armino\_component\_register() 放在任何配置条件中。
