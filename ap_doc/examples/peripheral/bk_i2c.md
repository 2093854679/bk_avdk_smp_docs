---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/ap_doc/bk7259/zh_CN/v4.0.1/examples/peripheral/bk_i2c.html
sdk_family: bk_avdk_smp
chip: BK7259
processor: AP
sdk_version: v4.0.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="i2c"></a>

# I2C

<a id="id1"></a>

## 1 功能概述

- I2C 接口可以通过数据引脚 (SDA) 和时钟引脚 (SCL) 连接到 I2C或 SMBus总线。SDA 线和 SCL 线均设置为漏极开漏 (open-drain) 输出，并接上拉电阻 (pull-up resistor)。因此，I2C 和 SMBus 总线上可以挂载多个器件。I2C 接口的每次传输都是由主器件 (Master) 发起和控制，
- 本章主要介绍通过I2C接口完成对EEPROM芯片的数据读写。目前，cp侧不允许使用I2C，ap侧支持使用I2C0和I2C1。
- I2C相关的理论介绍参考: [I2C的驱动](../../developer-guide/peripheral/bk_i2c.md)

备注

- 1.cp侧不允许使用I2C0和I2C1；
- 2.ap侧支持使用I2C0和I2C1;

<a id="id3"></a>

## 2 代码路径

> - demo路径：
>   :   `components\bk_cli\cli_i2c.c`
> - 驱动源码路径：
>   :   `ap\middleware\driver\i2c\i2c_driver.c` (硬件I2C驱动实现，CONFIG\_SIM\_I2C\=n 时编译)
>
>       `ap\middleware\driver\i2c\sim_i2c_driver.c` (软件模拟I2C驱动实现，CONFIG\_SIM\_I2C\=y 时编译)
> - I2C相关的api介绍参考: [I2C的api介绍](../../api-reference/peripheral/bk_i2c.md)

备注

- 1.硬件I2C与软件模拟I2C通过 `CONFIG_SIM_I2C` 在编译期二选一，二者不能共存，对外都是同一套 `bk_i2c_*` API。
- 2.i2c\_driver.c: 硬件I2C驱动实现，使用硬件中断方式。
- 3.sim\_i2c\_driver.c: 软件模拟I2C驱动实现，通过GPIO bit-bang模拟I2C时序，引脚由 `CONFIG_SIM_I2C0/1_SDA/SCL_GPIO` 配置。

<a id="cli"></a>

## 3 cli命令简介

demo运行依赖的宏配置：

> | NAME | Description | File | value |
> | --- | --- | --- | --- |
> | CONFIG\_I2C | support i2c | `ap\middleware\soc\bk7259\bk7259.defconfig` | y |
> | CONFIG\_I2C\_SUPPORT\_ID\_BITS | support i2c0 or i2c1 | `ap\middleware\soc\bk7259\bk7259.defconfig` | 1 |
> | CONFIG\_SIM\_I2C | y:软件模拟I2C(bit-bang)； n:硬件I2C(二选一) | `ap\middleware\soc\bk7259\bk7259.defconfig` | n |
> | CONFIG\_SIM\_I2C0\_SDA\_GPIO | 模拟I2C id\=0 的 SDA GPIO (仅 SIM\_I2C\=y) | `ap\middleware\soc\bk7259\bk7259.defconfig` | 1 |
> | CONFIG\_SIM\_I2C0\_SCL\_GPIO | 模拟I2C id\=0 的 SCL GPIO (仅 SIM\_I2C\=y) | `ap\middleware\soc\bk7259\bk7259.defconfig` | 0 |

demo支持的命令如下表：

> | Command | Param | Description |
> | --- | --- | --- |
> | i2c\_driver init | none | init I2C driver control memory |
> | i2c\_driver deinit | none | free all resource related to I2C |
> | i2c {id} init | i2c id number | power up and start the I2C id |
> | i2c {id} deinit | i2c id number | power down and Stop the I2C id |
> | i2c {id} memory\_write {data\_size} {dev\_addr} {mem\_addr\_size} | id: i2c id number | write data\_size bytes of data to the slave device with address dev\_id |
> | data\_size:size of data written |
> | dev\_addr: slave device address |
> | mem\_addr\_size: size of memory\_addr |
> | i2c {id} memory\_read {data\_size} {dev\_addr} {mem\_addr\_size} | id: i2c id | read data\_size bytes of data from slave device |
> | data\_size:size of data read |
> | dev\_addr: slave device address |
> | mem\_addr\_size: size of memory\_addr |

<a id="i2c-pin"></a>

## 4 I2C PIN脚描述

> - I2C0对应有1组PIN脚，对应的硬件管脚如下：
>
>   > | I2C0功能 | 组0 |
>   > | --- | --- |
>   > | I2C0\_CLK | GPIO0 |
>   > | I2C0\_SDA | GPIO1 |
> - I2C1对应有1组PIN脚，对应的硬件管脚如下：
>   :   | I2C1功能 | 组0 |
>       | --- | --- |
>       | I2C1\_CLK | GPIO20 |
>       | I2C1\_SDA | GPIO21 |

---

<a id="id4"></a>

## 4 演示介绍

> > demo1执行的步骤如下：
>
> 1、准备好EEPROM的模块，型号为ZD24C128A，使用I2C1连接方式如下：
>
> <a id="id5"></a>
> ![i2c_connect](../../../../_assets/166ca7e2b6160ee70fce-i2c_connect.png)
>
>
> Figure 1\. i2c\_connect图
>
> 2、顺序发送以下命令
>
> > **cpu1 i2c 1 init**
> >
> > ```
> > [11:45:42.140]发→◇cpu1 i2c 1 init
> > [11:45:42.145]收←◆cpu1 i2c 1 init
> > os:I(6720):create shell_handle, tcb=28078db0, stack=[28077188-28078d88:7168], prio=5
> > $
> > $cpu1:i2c:I(6178):I2C(1) init ok, baud_rate:400000
> > cpu1:cli:I(6178):i2c(1) init
> > ```
> >
> > **cpu1 i2c 1 memory\_write 8 50 1**//向EEPROM中写入8字节数据
> >
> > ```
> > [11:45:43.027]发→◇cpu1 i2c 1 memory_write 8 50 1
> > [11:45:43.034]收←◆cpu1 i2c 1 memory_write 8 50 1
> > os:I(7608):create shell_handle, tcb=28078db0, stack=[28077188-28078d88:7168], prio=5
> > $
> > $cpu1:cli:I(7066):i2c(1) memory_write buf_len:8
> > ```
> >
> > **cpu1 i2c 1 memory\_read 8 50 1** //从EEPROM中读取8字节数据
> > :   ```
> >     [11:45:44.825]发→◇cpu1 i2c 1 memory_read 8 50 1
> >     [11:45:44.831]收←◆cpu1 i2c 1 memory_read 8 50 1
> >     os:I(9406):create shell_handle, tcb=28078db0, stack=[28077188-28078d88:7168], prio=5
> >     $
> >     $cpu1:cli:I(8864):i2c_read_buf[0]=1
> >     cpu1:cli:I(8864):i2c_read_buf[1]=2
> >     cpu1:cli:I(8864):i2c_read_buf[2]=3
> >     cpu1:cli:I(8864):i2c_read_buf[3]=4
> >     cpu1:cli:I(8864):i2c_read_buf[4]=5
> >     cpu1:cli:I(8864):i2c_read_buf[5]=6
> >     cpu1:cli:I(8864):i2c_read_buf[6]=7
> >     cpu1:cli:I(8864):i2c_read_buf[7]=8
> >     cpu1:cli:I(8864):i2c(1) memory_read buf_len:8
> >     ```
>
> 3、时序图
>
> - 写时序图
>
> <a id="id6"></a>
> ![i2c_Sequence_ZD24C128A](../../../../_assets/8b95e32bdd8f7764715a-i2c_Sequence_ZD24C128A_wr.png)
>
>
> Figure 2\. i2c\_wr\_Sequence\_ZD24C128A
>
> - 读时序图
>
> <a id="id7"></a>
> ![i2c_Sequence_ZD24C128A](../../../../_assets/f4c8dd244dbbf3aaf4f0-i2c_Sequence_ZD24C128A_rd.png)
>
>
> Figure 3\. i2c\_rd\_Sequence\_ZD24C128A

demo2执行的步骤如下：

> 1、准备好EEPROM的模块，型号为FM24C04B，使用I2C1连接方式如下：
>
> <a id="id8"></a>
> ![i2c_connect2](../../../../_assets/2730b4f3449fdc43d151-i2c_connect2.png)
>
>
> Figure 4\. i2c\_connect图
>
> 2、顺序发送以下命令
>
> > **cpu1 i2c 1 init**
> >
> > ```
> > [16:44:55.619]发→◇cpu1 i2c 1 init
> > [16:44:55.622]收←◆cpu1 i2c 1 init
> > os:I(3120):create shell_handle, tcb=28078db0, stack=[28077188-28078d88:7168], prio=5
> > $
> > $cpu1:i2c:I(2984):I2C(1) init ok, baud_rate:400000
> > cpu1:cli:I(2984):i2c(1) init
> > ```
> >
> > **cpu1 i2c 1 memory\_write 8 50 0**//向EEPROM中写入8字节数据
> >
> > ```
> > [16:44:58.285]发→◇cpu1 i2c 1 memory_write 8 50 0
> > [16:44:58.292]收←◆cpu1 i2c 1 memory_write 8 50 0
> > os:I(5788):create shell_handle, tcb=28078db0, stack=[28077188-28078d88:7168], prio=5
> > $
> > $cpu1:cli:I(5652):i2c(1) memory_write buf_len:8
> > ```
> >
> > **cpu1 i2c 1 memory\_read 8 50 0** //从EEPROM中读取8字节数据
> > :   ```
> >     [16:44:59.919]发→◇cpu1 i2c 1 memory_read 8 50 0
> >     [16:44:59.926]收←◆cpu1 i2c 1 memory_read 8 50 0
> >     os:I(7422):create shell_handle, tcb=28078db0, stack=[28077188-28078d88:7168], prio=5
> >     $
> >     $cpu1:cli:I(7286):i2c_read_buf[0]=1
> >     cpu1:cli:I(7286):i2c_read_buf[1]=2
> >     cpu1:cli:I(7286):i2c_read_buf[2]=3
> >     cpu1:cli:I(7286):i2c_read_buf[3]=4
> >     cpu1:cli:I(7286):i2c_read_buf[4]=5
> >     cpu1:cli:I(7286):i2c_read_buf[5]=6
> >     cpu1:cli:I(7286):i2c_read_buf[6]=7
> >     cpu1:cli:I(7286):i2c_read_buf[7]=8
> >     cpu1:cli:I(7286):i2c(1) memory_read buf_len:8
> >     ```
>
> 3、时序图
>
> - 写时序图
>
> <a id="id9"></a>
> ![i2c_Sequence_FM24C04B](../../../../_assets/edeaa0fb8272d28a5173-i2c_Sequence_FM24C04B_wr.png)
>
>
> Figure 5\. i2c\_wr\_Sequence\_FM24C04B
>
> - 读时序图
>
> <a id="id10"></a>
> ![i2c_Sequence_FM24C04B](../../../../_assets/e690a61f264fa80b174e-i2c_Sequence_FM24C04B_rd.png)
>
>
> Figure 6\. i2c\_rd\_Sequence\_FM24C04B

备注

注意：memory\_write命令中的dev\_addr 50为16进制，因为i2c驱动中会将dev\_addr左移一位，所以传入的dev\_addr需要将ZD24C128A的dev\_addr（1010b）右移一位。
