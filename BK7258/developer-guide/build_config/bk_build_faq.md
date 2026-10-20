---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7258/zh_CN/v3.1.1/developer-guide/build_config/bk_build_faq.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: SMP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 常见问题

<a id="config"></a>

## 001 \- 使用CONFIG宏控制组件注册

下面是错误的禁用组件方法。因为 armino 构建系统在生成组件列表阶段（即早期扩充阶段）依赖 `armino_component_register()`
来生成该组件，而只有先生成该组件才会在组件处理阶段加载组件的 Kconfig 配置:

```
if (CONFIG_C1)
    armino_component_register(SRCS ${src} INCLUDE_DIRS ${inc})
endif()
```

下述写法也可能带来问题, 当组件使用CONFIG宏来控制组件注册:

```
if (CONFIG_C1)
    armino_component_register(SRCS ${src} INCLUDE_DIRS ${inc} REQUIRES c2 c3 c4)
else()
    armino_component_register()
endif()
```

<a id="id2"></a>

## 002 \- 工程中找不到函数定义

在工程main目录下的源文件中，如果出现某个组件的函数或者宏未定义的情况，往往是由于这个工程未被添加到main组件中，应该在main目录下的CMakeLists.txt中加上组件依赖，如添加 `dependency_component` 组件:

```
armino_component_register(SRCS "${srcs}" INCLUDE_DIRS "${incs}" PRIV_REQUIRES dependency_component)
```

<a id="id3"></a>

## 003 \- 编译工具链和编译参数查看

在编译目录下相应工程目录里面中compile\_commands.json文件，其中包含所有源文件的编译命令，可以查看每个源文件编译工具链和编译参数。
如bk7258的app工程，在build/bk7258/app/bk7258/compile\_commands.json中可以查看相应的编译命令。

<a id="armino"></a>

## 004 \- 如何为工程添加armino组件

armino smp构建系统默认会自动搜索components组件, ap子系统的默认搜索路径为 `ap/components` 目录 ，cp子系统的默认搜索路径为 `cp/components` 目录，
工程目录下ap的默认搜索路径为 `projects/xxx/ap/components` 目录 ，cp的默认搜索路径为 `projects/xxx/cp/components` 目录.

用户也可在工程目录下的CMakeLists.txt中设置 `EXTRA_COMPONENTS_DIRS` 来添加额外的组件搜索路径，这将仅为ap子系统添加组件搜索路径，添加方式如下:

```
set(EXTRA_COMPONENTS_DIRS
    ${CMAKE_CURRENT_SOURCE_DIR}/user_components
)
```

在组件搜索路径下创建组件目录，并在目录中创建CMakeLists.txt，在组件的CMakeLists.txt中使用 `armino_component_register()` 来注册。
armino将自动搜索默认components和extra\_components目录下的所有组件。实现代码参考tools/build\_tools/cmake/project.cmake:

```
armino_build_get_property(armino_path ARMINO_PATH)
get_filename_component(sub_sys ${armino_path} NAME) #ap/cp

if("${sub_sys}" STREQUAL "ap")
    foreach(component_dir ${EXTRA_COMPONENTS_DIRS})
        __project_component_dir("${component_dir}")
    endforeach()
endif()
```

总结:
:   1. 如果需要在AP里添加组件, 可以在projects/xxx/ap/components下添加组件目录, 并在目录中创建CMakeLists.txt, 在组件的CMakeLists.txt中使用 `armino_component_register()` 来注册。
    2. 如果需要在CP里添加组件, 可以在projects/xxx/cp/components下添加组件目录, 并在目录中创建CMakeLists.txt, 在组件的CMakeLists.txt中使用 `armino_component_register()` 来注册。
    3. extra\_components目录下(如user\_components)的组件仅会被ap子系统搜索到，cp子系统不会搜索到。
    4. extra\_components目录下(如user\_components)的组件可以依赖默认components目录下的组件，也可以依赖extra\_components目录下的组件。
    5. extra\_components目录下(如user\_components)的组件不能依赖cp子系统的组件。
    6. 可以添加多个extra\_components目录，如:

       ```
       set(EXTRA_COMPONENTS_DIRS
           ${CMAKE_CURRENT_SOURCE_DIR}/user_components
           ${CMAKE_CURRENT_SOURCE_DIR}/user_components2
           ${user_dir}/user_components3
       )
       ```
    7. 每个extra\_components目录下的组件都需要有一个独立的目录，不能直接在extra\_components目录下创建组件文件，如:

       ```
       user_components
       ├── component1
       │   ├── CMakeLists.txt
       │   ├── component1.c
       │   └── component1.h
       ├── component2
       │   ├── CMakeLists.txt
       │   ├── component2.c
       │   └── component2.h
       └── component3
           ├── CMakeLists.txt
           ├── component3.c
           └── component3.h
       ```

<a id="id4"></a>

## 005 \- 组件客制化标准

1. 对于经常变动的需求，提供功能的配置宏开关，功能独立解耦，方便开关
2. 需要修改的配置头文件，参考平台gpio/mbedtls机制，提供配置的方法：

   > 1. projects/app/ap/config/bk7258\_ap/usr\_gpio\_cfg.h
   > 2. projects/app/ap/config/bk7258\_ap/mbedtls\_custom\_config\_file.h
   > 3. projects/app/ap/config/bk7258\_ap/lwipopts\_custom.h
3. 对于非通用，非标准需求，建议使用如下方案，直接override组件的方法：

projects/lvgl/lvgl\_conf/
└── ap/

> └── components/
> :   └── lvgl/ \# 同名组件，会覆盖SDK的lvgl
>     :   ├── CMakeLists.txt
>         └── (复制整个lvgl组件)

缺点：
· 代码重复多

BK7258 SMP 构建系统支持项目组件覆盖 SDK 内部同名组件。

核心机制
1\. 组件添加顺序：
· 先添加 SDK 组件：${ARMINO\_PATH}/ap/components
· 后添加项目组件：projects/xxx/ap/components

2\. 覆盖机制：
· 在 component.cmake 的 \_\_component\_add() 函数中（第202-234行）：

> \# If a component of the same name has been added before, just override the properties.
> \# As a side effect, components added later ‘override’ components added earlier.

· 后添加的组件会覆盖先添加的同名组件
· 被覆盖的 SDK 组件路径保存在 COMPONENT\_OVERRIDEN\_DIR 属性中
