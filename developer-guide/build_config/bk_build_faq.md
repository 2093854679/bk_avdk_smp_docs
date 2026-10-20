---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/smp_doc/bk7259/zh_CN/v4.0.1/developer-guide/build_config/bk_build_faq.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: SMP
sdk_version: v4.0.1
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
如 bk7259 的 app 工程，可在 CP `build/bk7259/app/bk7259/compile_commands.json` 或 AP `build/bk7259/app/bk7259_ap/compile_commands.json` 中查看相应的编译命令。

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

<a id="ap"></a>

## 005 \- AP子系统第三方库编译选项及工具链

本节说明 AP 子系统（如 BK7259 AP）下第三方库（如 TFLite Micro）使用的编译选项与工具链配置，便于集成或移植第三方库时保持一致。

<a id="id4"></a>

### 工具链配置

AP 子系统使用 ARM bare-metal 工具链（arm-none-eabi）。BK7259 AP 工具链下载路径:

```
https://dl.bekencorp.com/tools/toolchain/arm/arm-gnu-toolchain-14.3.rel1-x86_64-arm-none-eabi.tar.xz
```

解压后通过环境变量 `TOOLCHAIN_DIR` 指定工具链根目录（或工程中 `COMPILER_TOOLCHAIN_PATH` 指定 `bin` 目录）。CMake 配置见 `ap/middleware/soc/<soc>_ap/toolchain-<soc>_ap.cmake`。

<a id="id5"></a>

### 第三方库编译选项

第三方库（含 Makefile/CMake 等非 Armino 构建）需与 AP 子系统使用相同的 CPU/FPU/ABI 及关键宏，否则可能出现链接或运行异常。编译选项应与 `ap/middleware/soc/bk7259_ap/toolchain-bk7259_ap.cmake` 中的 `c_link_options` 保持一致（含 CPU 架构、FPU、CMSE 等），典型片段如下:

```
-mcpu=<ap-core> -mfloat-abi=hard -mfpu=fpv5-sp-d16 -mcmse ...（其余选项见 toolchain 文件）
```

选项说明摘要:

```
- CPU/FPU/ABI/CMSE 须与 AP toolchain 一致，第三方库必须保持一致。
- 平台宏如 -DBK_MAC -D_GNU_SOURCE -DBEKEN_PLATFORM 等按需与工程一致。
- 链接选项 -Wl,--gc-sections 等建议与主工程一致，便于裁剪。
```
