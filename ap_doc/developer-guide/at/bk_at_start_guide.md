# **BK IDK AT 入门指南**



- [1. AT命令格式和类型](#at-guide-1 "#at-guide-1")

- [2. AT回显消息](#at-guide-2 "#at-guide-2")

- [3. Log端口与AT端口](#at-guide-3 "#at-guide-3")

- [4. 检查BK AT是否烧录成功](#at-guide-4 "#at-guide-4")

- [5 如何添加自定义AT命令](#at-guide-5 "#at-guide-5")

- [6 如何提升BK AT的性能](#at-guide-6 "#at-guide-6")

注意

由于SMP版AT在AP侧实现，并且由于当前串口绑定在CP上，因此再实际操作中，每条AT命令输入前都需要携带将命令发送到AP侧处理的标志【ap_cmd 】。


## **1. AT命令格式和类型**

BK AT目前支持两种AT命令格式，如下表所示：

> | 类型 | 命令格式 | 说明 |
> | --- | --- | --- |
> | 查询命令 | AT+<FUNCTION>=? | 返回当前查询的FUNCTION的值 |
> | 执行命令 | AT+<FUNCTION> [=parm1,parm2,…,paramN] | 设置当前FUNCTION的执行参数并执行此命令 |

需要注意的是：


- 不是每条AT命令都包含两种类型，但至少包含其中一个类型。

- param参数目前只支持 字符串 和 整形参数。

- <>内的参数不可省略。

- []内的参数可以忽略，

- 在FUNCTION和param中的特殊字符需要 转义处理 ，如 逗号(,) 、 等号(=) 、 反斜杠(\) 等。

- AT命令的默认波特率为115200。

- AT命令的长度不超过256字节。

- AT执行命令的参数个数不能超过16个。

- AT命令以 \r 和 \n 结尾。


## **2. AT回显消息**

AT回显消息分为两种：一种是BK AT的被动响应消息(AT-RSP)和BK AT主动对外上报的信息消息(AT-IND)。


### **2.1 AT-RSP**

> > AT-RSP是每条AT命令都会必须返回的响应消息，以通知主机这条AT命令得到执行结果，其最终消息必然是 OK 或者 ERROR 。
>
> | AT响应 | 说明 |
> | --- | --- |
> | CMDRSP:OK | 本条AT命令执行成功 |
> | CMDRSP:ERROR | 本条AT命令执行失败 |


### **2.2 AT-IND**

> > AT-IND是报告系统中重要的状态变化或消息。
>
> 例如：
>
> | AT IND | 说明 |
> | --- | --- |
> | ready | BK AT上电完成，等待输入 |
> | busy | BK AT正在处理上条命令，无法处理新的AT命令 |
> | EVT:WLAN STA SCAN_DONE | WIFI扫描完成 |
> | EVT:WLAN STA CONNECTED | WIFI连接AP完成 |
> | EVT:WLAN STA DISCONNECTED | WIFI已经断连 |
> | EVT:WLAN SAP CONNECTED | SoftAP创建完成 |
> | EVT:WLAN SAP DISCONNECTED | SoftAP已经删除 |
> | EVT:GOT-IP | 已经获取到DHCP分配的IP地址 |

备注:AT-IND可以是用户自己想要输出的消息和内部变量值，只要通过API：atsvr_output_msg(char* msg) 即可完成输出


## **3. Log端口与AT端口**


- BK AT支持Log和AT命令分流，即Log与AT使用不同的UART口进行通信，双方互不干扰。

- BK AT所需的硬件资源如下：

> | UART端口 | 功能 |
> | --- | --- |
> | UART0 | Log端口，主要负责固件下载和Log输出 |
> | UART1 | 默认AT端口，主要负责AT命令的接收和AT回显事件的发送，也负责在socket模式下传输数据包 |

备注

BK AT不推荐Log端口与AT端口使用相同配置，因为可能会发生意想不到的错误与时序问题

BK AT默认使用的是UART0端口作为AT端口，方便支持设备只有一个UART端口的情况，如果硬件资源支持可以通过修改配置修改AT命令的端口，修改方式：

1、修改对应的config文件中的配置宏: CONFIG_DEFAULT_AT_PORT 如果您想将AT端口设置为Log端口,请将该值置为0;如果您想要更改至其他UART端口，将该值改为对应端口值，例如设为UART1，则将此值置为1；

2、重新编译版本

备注

除了BK7235，其余模组均是多核芯片，相关配置修改请在CPU0侧的config上配置，即bk72xx不带 _cpx 的文件夹


## **4. 检查BK AT是否烧录成功**

请按照如下操作检查烧录的BK AT固件是否烧录成功：


- 打开串口工具，如sscom, SecureCRT等；

- 选择串口AT端口；

- 波特率设为115200；

- 数据位：8；

- 检验位：None;

- 停止位：1；

- 流控：None;

- 输入: AT

发送AT命令，响应是 CMDRSP:OK ，则表示BK AT固件烧录成功。


```
AT
CMDRSP:OK

```

如果您在烧录之后还未上电，则可以在串口工具连接上模组之后上电，当看到下图所示的 AT:READY 时 说明烧录成功：


```
AT:READY

```

如果您需要查看 Log端口 信息判断是否烧录成功，则您需要在AT端口侧输入AT+RST后，看到如下的开机 日志后，也代表烧录成功:


```
AT_SVR:I(162):AT TASK Create OK!

```


## **5 如何添加自定义AT命令**

想让一条AT命令合理且正确的运行，需要至少两个动作：


- 定义一条AT命令及其回调函数

- 注册这条AT命令至合适的位置

下面将以 **AT+USERCMD** 为例子展示如何新增一条AT命令。


### **5.1 一条AT命令的属性**

在BK AT，一条AT命令拥有如下几个属性：


- AT命令名称

- AT命令帮助

- 查询回调函数

- 执行回调函数

- sync标志位

- 超时时间

- 超时标志位

- 超时回调函数

用户可以定义AT命令的各种属性来丰富AT命令的运用场景


### **5.2 AT命令名称和HELP规则**

BK AT并不限制AT命令名称的写法，但请注意，请在使用 ‘=’ 和 ‘,’ 时需要使用转义符，请尽量避免使用上述两个符号作为名称和参数。

备注

请注意不要使用中文字符符号！

BK AT的AT命令名称格式以 AT+XXX 的格式命名。
AT命令的HELP功能是为AT+HELP命令准备的字符串，用来帮助用户了解AT命令的使用方式， 在BK AT，我们推荐将AT命令整个格式放入HELP字符串中，方便使用。


### **5.3 AT命令查询和执行函数**

BK AT的查询和执行函数是实现AT命令查询与执行的基础，BK AT不限制用户自定义的函数格式， 只限制了函数的名称格式为 int xxx(int sync, int argc, char** argv),下面是查询和执行函数的一个demo范例:


```
/*sync属性在下方表述，argc为本条AT命令传入的参数个数，
也就是等号之后的参数个数，argv是一个数组指针，该指针指向参数所存放的数组*/
static int at_user_xxx(int sync,int argc, char **argv)
{
    int err;
    if(argv==NULL)
    {
        goto error;
    }
    /*不同的参数代表不同的处理分支*/
    if(argc==1)
    {
        err = xxx_func();//想要调用的函数
        if(err)
            goto error;
        ATSVR_SEND_OK();//如果执行满足需求，则返回OK
        return 0;
    }
    ...
    else
    {
        err = xxx_func();//想要调用的函数
        if(err)
            goto error;
        ATSVR_SEND_OK();//如果执行满足需求，则返回OK
        return 0;
    }
error:
    ATSVR_SEND_ERROR();//如果执行不满足需求，则返回ERROR
    return -1;
}

```


### **5.4 AT命令的额外属性**

BK AT除了设置名称和函数等属性外，还支持用户自定义一些属性，下面介绍一下对应的属性，方便 用户使用。


- sync:BK AT开放给用户使用的资源使用标志位。以方便用户在AT命令表上自定义回调函数的资源使用，用户需要自己在回调函数中基于此标志位判断是否使用系统资源，并且可以在AT命令上置true或者false来开关。

备注

BK AT并不使用这个标志位，BK AT所做的只是将其从AT命令表传递至回调函数中，如果用户有新的资源调用方式或者不使用资源，则将sync置为false即可。


- timeout:修改AT命令执行超时标志位。当用户决定这条AT命令需要一定时间的处理才能决定是否执行成功时，用户需要通知BK AT 以方便BK AT知晓用户的行为，因为BK AT内部针对每条AT命令都设有超时保护处理机制。

- sync_time: 超时时间。用户配置的命令处理超时时间，以ms为单位；

- timeout_func：用户提供的超时发生时的回调函数。方便用户自行处理超时机制；


### **5.5 如何注册一条AT命令**

当定义好AT命令时，用户将其填到user_cmds_table全局列表中，

demo如下:


```
const struct _atsvr_command user_cmds_table[] =
{
    AT_CMD_HADLER("AT+USERCMD","AT_USER func demo:AT+USERCMD=? for query","AT+USERCMD = param1,param2,...,paramN for setup",at_user_query,at_user_setup,false,0,0,NULL,false)
};

```

然后，调用atsvr_register_commands将全局列表user_cmds_table注册到AT 命令集中即可，at_user_event_handler函数是EVENT上报处理函数。


```
int ret;
ret = atsvr_register_commands(user_cmds_table, sizeof(user_cmds_table) / sizeof(user_cmds_table[0]),"user",at_user_event_handler);
if(0 == ret)
    BK_LOGD(TAG,"USER-AT init done\r\n");

```

备注

AT命令的注册操作，需要在AT命令使用之前，并且避免反复注册。


### **5.6 如何执行一条AT命令**

在完成上述定义与注册之后，用户只需要重新编译并烧录版本即可使用新的AT命令。

发送新添加的命令，如果返回 CMDRSP:OK 则代表添加成功。


## **6 如何提升BK AT的性能**

目前BK AT使用的I/O交互方式是UART，受限于UART的性能，可以选择SDIO方式进行通信，提高通信带宽。
