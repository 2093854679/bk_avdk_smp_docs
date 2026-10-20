---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7258/zh_CN/v3.1.1/developer-guide/peripheral/bk_gpio.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: AP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="gpio"></a>

# GPIO 使用指南

<a id="id1"></a>

## 概述

GPIO（通用输入输出）模块是芯片上用于外部设备信号通信的核心模块。BK7258芯片有56个通用输入输出管脚（GPIO Pin），每个管脚都可用作一个通用IO，或连接一个内部的外设信号。

<a id="gpio-map-config"></a>

## GPIO MAP Config

gpio\_map.h

> 在每个 CPU 核心驱动初始化过程中，GPIO会根据映射表（**GPIO\_DEFAULT\_DEV\_CONFIG**）进行配置。该映射表中的每一行包含11个元素。
> 这11个元素含义如下:
>
> > - gpio\_id：从 0 开始编号的对应GPIO引脚号。
> > - second\_func\_en：是否启用第二功能。
> > - second\_func\_dev:选择引脚的第二功能。（目前，单个GPIO引脚最多可复用八种第二功能，同一时间只能复用一个第二功能，详见 **GPIO\_DEV\_MAP**。该表格用户不可修改。）
> > - io\_mode：选择输入输出（IO）操作模式，包括输入模式、输出模式或高阻态。
> > - pull\_mode：选择GPIO的上拉或下拉模式。
> > - int\_en：是否开启中断。
> > - int\_type：选择触发中断的条件，包括高电平触发、低电平触发、上升沿触发、下降沿触发。
> > - low\_power\_io\_ctrl：低功耗模式下是否保持GPIO的输出状态或设置为唤醒源。（配置GPIO\_LOW\_POWER\_KEEP\_INPUT\_STATUS可以将GPIO设置为唤醒源，若设为唤醒源，需要开启中断，配置中断类型。若未对该位进行设置，GPIO 在进入低功耗模式时GPIO将处于高阻状态）
> > - driver\_capacity：驱动能力选择，共有四个等级。
> > - gpio\_init：上电初始化时，是否按照（**GPIO\_DEFAULT\_DEV\_CONFIG**）的配置操作GPIO
> > - gpio\_time\_sharing\_multiplex：GPIO分时复用标志（enable:允许动态map/unmap GPIO，disable:不允许动态配置GPIO第二功能，GPIO如果有分时复用需求，则需要使能 **gpio\_time\_sharing\_multiplex** 字段）。

<a id="id3"></a>
![GPIO](../../../../../_assets/bb5713a4b7050bcfd679-gpio_initialization.png)


gpio\_initialization

<a id="id4"></a>
![GPIO](../../../../../_assets/baac8f3ed10cffea5360-upper_call_map.png)


upper\_call\_map.png

<a id="id2"></a>

## GPIO 部分使用介绍:

> 1. 新建工程时，客户必须要根据其开发板的配置需求来配置 **GPIO\_DEFAULT\_DEV\_CONFIG** 表。您可以依据 **GPIO\_DEV\_MAP** 表中定义的每个 GPIO 的功能，自由地配置 **GPIO\_DEFAULT\_DEV\_CONFIG** 表。
>    GPIO外设初始化时会在gpio\_hal.c的gpio\_hal\_default\_map\_init（）函数里按照 **GPIO\_DEFAULT\_DEV\_CONFIG** 表初始化GPIO（需要打开宏CONFIG\_GPIO\_DEFAULT\_SET\_SUPPORT，平台只会操作一次，
>    后面以用户配置为准,如果没有开启该宏，则平台不会操作GPIO，GPIO默认值为 **高阻态**）。
> 2. 以自定义方式覆盖默认的 **GPIO\_DEFAULT\_DEV\_CONFIG** 时，可按以下步骤操作：
>
> > - 打开宏定义：在项目配置文件中开启 CONFIG\_USR\_GPIO\_CFG\_EN 宏，以启用自定义 GPIO 配置功能。
> > - 创建 usr\_gpio\_cfg.h 文件：在项目的合适位置创建 usr\_gpio\_cfg.h 头文件，并在该文件中定义你自定义的 GPIO\_DEFAULT\_DEV\_CONFIG。此配置应包含你所需的所有 GPIO 的初始化设置和映射关系。如 bk\_avdk\_smp\_release\\projects\\app\\config\\bk7258 所示。
> >
> > > 需要注意的是，新映射的功能必须已在 **GPIO\_DEV\_MAP** 表中定义。在初始化过程中，芯片会根据 **GPIO\_DEFAULT\_DEV\_CONFIG** 表来配置 GPIO 的状态。（注意：确保在代码中包含 usr\_gpio\_cfg.h 文件，这样在编译时就会使用你自定义的 GPIO 配置。）
>
> 3. 低功耗状态：在低功耗状态下，GPIO 可配置为输入模式（唤醒源）和输出模式。如果在低功耗期间不使用相应的 GPIO（GPIO\_LOW\_POWER\_DISCARD\_IO\_STATUS），低功耗模式程序会将GPIO 设置为高阻状态，以防止在低功耗模式下出现漏电现象。
> 4. 当你需要在低功耗模式下保持 GPIO 的输出状态时，有两种办法设置：
>
> > - 按照说明配置 **GPIO\_DEFAULT\_DEV\_CONFIG** 表。
> > - 使用 bk\_gpio\_register\_lowpower\_keep\_status() 函数注册。（目前默认数量为4，可使用CONFIG\_GPIO\_DYNAMIC\_KEEP\_STATUS\_MAX\_CNT修改数量）
> > - 使用 bk\_gpio\_unregister\_lowpower\_keep\_status（）函数可以取消之前注册需要保持的GPIO。
>
> 5. 当进入低功耗模式时，可以将多个外部 GPIO 设置为唤醒源。如果任何一个 GPIO 产生中断信号，芯片就能从低功耗模式中唤醒。目前有三种办法设置为唤醒源：
>
> > - 按照说明配置 **GPIO\_DEFAULT\_DEV\_CONFIG** 表。
> > - **GPIO\_STATIC\_WAKEUP\_SOURCE\_MAP** 中设置多个唤醒源。
> > - 使用 bk\_gpio\_register\_wakeup\_source（）函数注册。（目前默认数量为4，可使用CONFIG\_GPIO\_DYNAMIC\_WAKEUP\_SOURCE\_MAX\_CNT修改数量）
> > - 使用 bk\_gpio\_unregister\_wakeup\_source（）函数可以取消注册的唤醒源。
>
> 6. 当进入低功耗模式（仅适用于低压情况）时，GPIO 的状态将被备份。退出低功耗模式后，GPIO 会自动恢复到进入该模式之前的状态。
>    （**note**：从深度睡眠模式退出后，相当于进行了一次软重启，GPIO状态不会自动恢复，会重新走初始化流程，如果需要从深度睡眠模式退出保持GPIO的状态，见第8点）
> 7. GPIO在软件重启过程中保持状态
>
> > - 将对应GPIO\_ID的gpio\_init字段置为disable
>
> 8. 设置输入中断检测时，需要确保开启中断前，电平状态稳定，处理逻辑如下：先将电平钳位在高电平或者低电平（根据中断触发方式决定），即如果是上升沿触发中断，则一开始就需要
>    将GPIO设置到拉低状态，防止抖动或高阻态随机值引起误触发。
> 9. CP/AP必须配置自己的GPIO，且同一GPIO不能在CP和AP上重复配置。
> 10. 未明确分配的GPIO无法map/unmap，默认状态为高阻态，只能当做GPIO使用。
> 11. SDK内部集成了key组件，用户可以通过该组件快速实现按键检测功能。key组件路径为 `ap\components\key`，使用方式可以参考 `ap\components\bk_cli\cli_key.c`。

备注

- usr\_gpio\_cfg.h 必须被配置。
- 当GPIO设置为电平触发中断时，若检测引脚的有效电平持续存在，将导致中断反复触发。
- GPIO 的驱动能力如下表所示。REG 表示 GPIO 寄存器的设置值，驱动能力共有四个等级。
  :   |  | REG\=2 | REG\=102 | REG\=202 | REG\=302 |
      | --- | --- | --- | --- | --- |
      | P14 | 10.49 | 19.95 | 33.72 | 40.8 |
      | P15 | 10.48 | 19.9 | 33.28 | 40.03 |
      | P16 | 10.41 | 19.65 | 32.76 | 39.35 |
      | P17 | 10.36 | 19.45 | 32.26 | 38.6 |

      > - 高电平拉电流(mA)

      |  | REG\=0 | REG\=100 | REG\=200 | REG\=300 |
      | --- | --- | --- | --- | --- |
      | P14 | 8.54 | 16.09 | 26.05 | 32 |
      | P15 | 8.56 | 16.19 | 26.47 | 32.6 |
      | P16 | 8.56 | 16.35 | 26.87 | 33.24 |
      | P17 | 8.62 | 16.5 | 27.24 | 33.85 |

      > - 低电平灌电流(mA)

Example:

GPIO\_0 配置为 \[GPIO\_DEV\_I2C1\_SCL\] 功能，将 GPIO\_1 配置为 \[GPIO\_DEV\_I2C1\_SDA\] 功能：
:   | gpio\_id | second\_func\_en | second\_func\_dev | io\_mode | pull\_mode | int\_en | int\_type | low\_power\_io\_ctrl | driver\_capacity | gpio\_init | gpio\_time\_sharing\_multiplex |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | GPIO\_0 | GPIO\_SECOND\_FUNC\_ENABLE | GPIO\_DEV\_I2C1\_SCL | GPIO\_IO\_DISABLE | GPIO\_PULL\_UP\_EN | GPIO\_INT\_DISABLE | GPIO\_INT\_TYPE\_LOW\_LEVEL | GPIO\_LOW\_POWER\_DISCARD\_IO\_STATUS | GPIO\_DRIVER\_CAPACITY\_3 | GPIO\_INIT\_ENABLE | GPIO\_TIME\_SHARING\_MULTIPLEX\_DISABLE |
    | GPIO\_1 | GPIO\_SECOND\_FUNC\_ENABLE | GPIO\_DEV\_I2C1\_SDA | GPIO\_IO\_DISABLE | GPIO\_PULL\_UP\_EN | GPIO\_INT\_DISABLE | GPIO\_INT\_TYPE\_LOW\_LEVEL | GPIO\_LOW\_POWER\_DISCARD\_IO\_STATUS | GPIO\_DRIVER\_CAPACITY\_3 | GPIO\_INIT\_ENABLE | GPIO\_TIME\_SHARING\_MULTIPLEX\_DISABLE |

    > - PS：当使用 GPIO 的第二功能时，GPIO 默认处于关闭状态（输入输出模式 io\_mode 为 \[GPIO\_IO\_DISABLE\]）。I2C 需要更强的驱动能力（驱动能力 driver\_capacity 设为 \[GPIO\_DRIVER\_CAPACITY\_3\]）

GPIO\_0 被设置为高阻态（默认状态）：
:   | gpio\_id | second\_func\_en | second\_func\_dev | io\_mode | pull\_mode | int\_en | int\_type | low\_power\_io\_ctrl | driver\_capacity | gpio\_init | gpio\_time\_sharing\_multiplex |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | GPIO\_0 | GPIO\_SECOND\_FUNC\_DISABLE | GPIO\_DEV\_INVALID | GPIO\_IO\_DISABLE | GPIO\_PULL\_DISABLE | GPIO\_INT\_DISABLE | GPIO\_INT\_TYPE\_LOW\_LEVEL | GPIO\_LOW\_POWER\_DISCARD\_IO\_STATUS | GPIO\_DRIVER\_CAPACITY\_0 | GPIO\_INIT\_DISABLE | GPIO\_TIME\_SHARING\_MULTIPLEX\_DISABLE |

    > - PS：禁用所有配置,初始化时不操作该GPIO

GPIO\_0 设置为输入模式，并配置为下降沿触发中断：
:   | gpio\_id | second\_func\_en | second\_func\_dev | io\_mode | pull\_mode | int\_en | int\_type | low\_power\_io\_ctrl | driver\_capacity | gpio\_init | gpio\_time\_sharing\_multiplex |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | GPIO\_0 | GPIO\_SECOND\_FUNC\_DISABLE | GPIO\_DEV\_INVALID | GPIO\_INPUT\_ENABLE | GPIO\_PULL\_UP\_EN | GPIO\_INT\_ENABLE | GPIO\_INT\_TYPE\_FALLING\_EDGE | GPIO\_LOW\_POWER\_DISCARD\_IO\_STATUS | GPIO\_DRIVER\_CAPACITY\_0 | GPIO\_INIT\_ENABLE | GPIO\_TIME\_SHARING\_MULTIPLEX\_DISABLE |

    > - PS：关闭第二功能。有 4 种中断触发条件：低电平触发、高电平触发、上升沿触发、下降沿触发

GPIO\_0 作为低功耗唤醒源，下降沿唤醒：
:   | gpio\_id | second\_func\_en | second\_func\_dev | io\_mode | pull\_mode | int\_en | int\_type | low\_power\_io\_ctrl | driver\_capacity | gpio\_init | gpio\_time\_sharing\_multiplex |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | GPIO\_0 | GPIO\_SECOND\_FUNC\_DISABLE | GPIO\_DEV\_INVALID | GPIO\_INPUT\_ENABLE | GPIO\_PULL\_UP\_EN | GPIO\_INT\_ENABLE | GPIO\_INT\_TYPE\_FALLING\_EDGE | GPIO\_LOW\_POWER\_KEEP\_INPUT\_STATUS | GPIO\_DRIVER\_CAPACITY\_0 | GPIO\_INIT\_ENABLE | GPIO\_TIME\_SHARING\_MULTIPLEX\_DISABLE |

    > - PS：low\_power\_io\_ctrl 设置为 \[GPIO\_LOW\_POWER\_KEEP\_INPUT\_STATUS\]

<a id="q-a"></a>

## Q\&A

1. 低压模式设置了RTC和GPIO中断，RTC触发后GPIO则失效了。

   该问题原因为在进入低压模式之前，MCU会备份GPIO的状态。为了防止未使能唤醒GPIO引脚的中断，导致MCU无法被唤醒，在低压模式下，唤醒GPIO的引脚中断会被使能。
   退出中断后，该引脚的状态会恢复到进入低压之前的状态。如果在进入低压模式之前未使能唤醒引脚的中断，那么在退出低压后，该引脚的中断仍然未被使能，因此在正
   常工作模式下唤醒GPIO的中断无法被触发。
2. 进入深度休眠后，敲一下串口，设备会唤醒。
   因为一些场景需求，默认支持在low voltage、 deepsleep时使用uart来唤醒设备。如果不需要该功能，可以在gpio\_map.h中将GPIO\_STATIC\_WAKEUP\_SOURCE\_MAP中GPIO\_10注释掉。
3. 多核操作同一个GPIO之间的协同问题，某客户在多核系统中未采用CPU独立配置GPIO方案，导致以下典型问题，表象如下：

> - 使用dvp摄像头打开后，按键中断偶现丢失。
> - 单独打开lcd或uvc时，按键gpio中断50%概率左右不会触发
>
> 多个CPU共享硬件资源。所有的GPIO引脚共享GPIO中断线。如果每个CPU没有配置自己需要控制的GPIO，在GPIO发生中断时，多个CPU核心都会接到中断通知，执行中断处理函数。
> 开dvp和lcd等操作都会开启CPU1，CPU1的主频比CPU0快，可能会清掉中断标志位，造成CPU0的GPIO中断丢失，导致程序未按照预期执行。为避免这种情况，每个CPU必须配置各自的GPIO\_MAP表。

<a id="application-example"></a>

## Application Example

DEMO1:
:   GPIO\_0 as wake-up source for DeepSleep or LowPower, pseudo code description and interpretation.

<a id="id5"></a>
![GPIO](../../../../../_assets/c86ff1505549c67e76ca-GPIO_Lowpower_Deepsleep.png)


GPIO as wake-up source for DeepSleep or LowPower

<a id="gpio-api-reference"></a>

## GPIO API Reference

> [GPIO的驱动API](../../api-reference/peripheral/bk_gpio.md)
