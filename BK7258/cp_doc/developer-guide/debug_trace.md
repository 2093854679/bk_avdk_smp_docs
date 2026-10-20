---
type: official-document
source_url: https://docs.bekencorp.com/arminodoc/bk_avdk_smp/cp_doc/bk7258/zh_CN/v3.1.1/developer-guide/debug_trace/index.html
sdk_family: bk_avdk_smp
chip: BK7258
processor: CP
sdk_version: v3.1.1
language: zh_CN
fetched_at: '2026-10-20T16:59:36.586772+00:00'
mirror_status: current
---

<a id="id1"></a>

# 系统调试

<a id="arminocp"></a>

## **Armino平台CP系统调试命令**

> - BK7258 CP端的log通过串口DL\_UART0输出(默认波特率为115200)
> - BK7258 AP的log通过mailbox转发到CP串口DL\_UART0输出(默认波特率为115200)
> - AP log带cpu1标签（异常log除外）
> - 通过串口输入log命令查看当前log配置
> - 宏CONFIG\_UART\_ATE\_PORT表示使用哪一个PIN管脚检测ATE模式；宏CONFIG\_UART\_PRINT\_PORT表示默认初始化时，LOG的UART口；CONFIG\_UART\_ATE\_PRINT\_PORT表示ATE检测时，将LOG的UART口做一次切换（但此时LOG口还没有初始化,初始化时，根据CONFIG\_UART\_ATE\_PRINT\_PORT选择）
>   示例：ate识别用uart1的tx，正常应用的日志用uart1，进ate模式后，log及命令行用uart0，配置如下：CONFIG\_UART\_ATE\_PORT\=1，CONFIG\_UART\_PRINT\_PORT\=1，CONFIG\_UART\_ATE\_PRINT\_PORT\=0
> - 通过串口输入help命令查看当前支持的调试命令：
>
> > ```
> > #
> > #log
> > log: echo 1, level 3, sync 0.
> >
> > #
> > #help
> >
> >     ====Build-in Commands====
> >     help
> >     log: log [echo(0,1)] [level(0~5)] [sync(0,1)] [Whitelist(0,1)]
> >     debug: debug cmd [param] (ex:debug help)
> >     cpu1: cpu1 cmd (ex:cpu1 help)
> >     loginfo: log statistics.
> >     modlog: modlog tag_name on/off
> >
> >     ====User Commands====
> >     aon_rtc_auto_test: {id} {start|stop}
> >     aon_rtc_clock_src: aon_rtc_clock_src {26m|rosc}
> >     aon_rtc_driver: aon_rtc_driver {init|deinit}
> >     aon_rtc_dump: {id}
> >     aon_rtc_get_time: aon_rtc_get_time {id}
> >     aon_rtc_register: aon_rtc_register {id} {name} {period_tick} {period_cnt}, {callback}
> >     aon_rtc_rosc_cal: aon_rtc_rosc_cal interval
> >     aon_rtc_rosc_test: aon_rtc_rosc_test
> >     aon_rtc_unregister: aon_rtc_unregister {id} {name}
> >     ap: ap ssid [password] [channel[1:14]]
> >     assert: asset and dump system information
> >     auto_pwr_change_by_rssi: 1:enable,0:disable
> >     backtrace: show task backtrace
> >     bcn_loss_intv: bcn_loss_intv interval repeat_num}
> >     bcn_loss_time: bcn_loss_time wait_cnt wake_cnt}
> >     bcn_miss_time: bcn misstime}
> >     bcn_recv_win: bcn_recv_win default_win max_win step}
> >     blacklist: Set ssid blacklist
> >     bootcore: bootcore [core id] [mode: 1:start,0:stop]
> >     cali: cali auto_test
> >     capa: wifi capability config
> >     cca: cca open\close\show
> >     channel: channel {1~13} - set monitor channel
> >     cif: controller test cmd
> >     ckmn: ckmn ckeck32k {32|other}
> >     ckmn_driver: ckmn_driver {init|deinit}
> >     ckmn_show_reg: ckmn show_reg
> >     ckmnautosw: ckmnautosw {26m|32k}
> >     ckmncorr: ckmncorr {26m|32k} {0|1|2|3}
> >     close_coex_csa: close csa in coexist mode {1|0}
> >     cpuload: show task cpu load
> >     cputest: cputest [count]
> >     dhcpc: dhcpc
> >     dma: dma {id} {init|deinit|start|stop|set_tran_len|get_remain_len}
> >     dma_chnl: dma_chnl alloc
> >     dma_chnl_free: dma_chnl_free {id}
> >     dma_chnl_test: {start|stop} {uart1|uart2|uart3} {wait_ms}
> >     dma_config: dma_config {mode|priority|pasue|src|dst}{mode value/priority value/dev,width,increase_en,loop_en,start_addr,end_addr}
> >     dma_copy: copy {src} {dst} {len}
> >     dma_driver: dma_driver {init|deinit}
> >     dma_int: dma_int {id} {reg|enable_hf_fini|disable_hf_fini|enable_fini|disable_fini|pause}
> >     dma_memcopy_test: copy {count|in_number1|in_number2|out_number1|out_number2}
> >     dvfs: dvfs [cksel_core] [ckdiv_core] [ckdiv_bus] [ckdiv_cpu0] [ckdiv_cpu1]
> >     dvfs_auto_test: dvfs_auto_test [period]
> >     dwtd: dwtd r/w/b data_address
> >     dwtdd: dwtdd data_address data_value
> >     dwtdr: dwtdr data_address data_address_limit
> >     dwti: dwt instruction_addr
> >     easyflashtest: easyflashtest {write|read|del}
> >     efuse: efuse [-r addr] [-w addr data]
> >     efuse_driver: efuse_driver {init|deinit}
> >     efuse_test: efuse_test {write|read}
> >     efusemac: efusemac [-r] [-w] [mac]
> >     event: event {reg|unreg|post} {mod_id} {event_id}
> >     exception: {undefine|dabort|illegal|irq|fiq}
> >     filter: filter <bits> - bit0/d, 1/preq, 2/prsp, 3/b, 4/a
> >     flash: flash {erase|read|write} [start_addr] [len]
> >     flash_erase_test: cli_flash_erase_test with ble connecting
> >     flash_partition: flash_partition {show}
> >     fpb: fpb instruction_addr
> >     get: get wifi status
> >     gpio: gpio     [set_mode/output_low/output_high/input/spi_mode]      [id]     [mode]
> >     gpio_driver: gpio_driver    [init/deinit]}
> >     gpio_int: gpio_int    [index]     [inttype/start/stop]     [low/high_level/rising/falling edge]
> >     gpio_kpsta: gpio_kpsta [register/unregister][index][io_mode][pull_mode][func_mode]
> >     gpio_low_power: gpio_low_power [simulate][param]
> >     gpio_map: gpio_map     [sdio_map/spi_map]
> >     gpio_retention_test: gpio_retention_test
> >     gpio_wake: gpio_wake [index][low/high_level/rising/falling edge][enable/disable wakeup]
> >     id
> >     int: retarget {int_group0} {int_group1}
> >     ip: ip [sta|ap][{ip}{mask}{gate}{dns}]
> >     ipconfig: ipconfig [sta|ap][{ip}{mask}{gate}{dns}]
> >     ipdbg: ipdbg [function][value]
> >     iperf: iperf help
> >     iplog: iplog [modle][type]
> >     la: la rf_adc_40M/rf_adc[_80M]/fe_adc/rf_dac/fe_dac
> >     lwip_mem: print lwip memory information
> >     lwip_pbuf: print lwip pbuf information
> >     lwip_stats: print lwip protocal statistics
> >     mac: mac <mac>, get/set mac. e.g. mac c89346000001
> >     mem_apply: mem_apply [module][value]
> >     memdump: <addr> <length>
> >     memleak: [show memleak
> >     memset: <addr> <value 1> [<value 2> ... <value n>]
> >     memshow: show free heap
> >     memstack: show stack memory usage
> >     memtest: <addr> <length>
> >     memtest_r: <src> <dest> <size>
> >     memtest_wr: <addr> <count>
> >     memtime: <addr> <count> <0:write,1:read>
> >     micodebug: micodebug on/off
> >     monitor: monitor {1~13|15|99}
> >     mpucfg: <rnr> <rbar> <rlar>
> >     mpuclr: <rnr>
> >     mpudump: dump mpu config
> >     net: net {sta/ap} ... - wifi net config
> >     osinfo: show os runtime information
> >     per_packet_info: per_packet_info [per_packet_info_output_bitmap(base 16)]
> >     ping: ping <ip>
> >     pkt_dbg: packet debug config
> >     pm: pm [sleep_mode] [wake_source] [vote1] [vote2] [vote3] [param1] [param2] [param3]
> >     pm_ana: pm_ana [1/0]
> >     pm_auto_vote: pm_auto_vote [auto_vote_value]
> >     pm_boot_cp1: pm_boot_cp1 [module_name] [ctrl_state:0x0:bootup; 0x1:shutdowm]
> >     pm_boot_cp2: pm_boot_cp2 [module_name] [ctrl_state:0x0:bootup; 0x1:shutdowm]
> >     pm_buck: pm_buck [1/0]
> >     pm_clk: pm_clk [module_name][clk_state]
> >     pm_cp1_ctrl: pm_cp1_ctrl [cp1_auto_pw_ctrl]
> >     pm_ctrl: pm_ctrl [ctrl_value]
> >     pm_debug: pm_debug [debug_en_value]
> >     pm_freq: pm_freq [module_name][ frequency]
> >     pm_gpio: pm_gpio [1/0]
> >     pm_ldo: pm_ldo[module_name][gpio id][gpio_output_state:0x0->low voltage, 0x1->high voltage]
> >     pm_lpo: pm_lpo [lpo_type]
> >     pm_power: pm_power [module_name][ power state]
> >     pm_psram: pm_psram[module_name][ctrl_state:0x0:power&clk on; 0x1:power&clk off]
> >     cpu2:(5008):cpu2_test_task run core: 2
> >     cpu1:(5008):cpu1_test_task run core: 1
> >     pm_pwr_state: pm_pwr_state [pwr_state]
> >     pm_rosc: pm_rosc [rosc_accuracy_count_interval]
> >     pm_rosc_cali: pm_rosc_cali [cali_mode][cal_intval]
> >     pm_rosc_pin: pm_rosc_pin [lpo_clk:0:ana;1:dig]
> >     pm_rosc_ppm: pm_rosc_ppm [interval] [count]
> >     pm_vcore: pm_vcore [value]
> >     pm_vol: pm_vol [vol_value]
> >     pm_vote: pm_vote [pm_sleep_mode] [pm_vote] [pm_vote_value] [pm_sleep_time]
> >     pm_wakeup_source: pm_wakeup_source [pm_sleep_mode]
> >     ps: ps enable and debug info config
> >     psram_cache: psram_cache <addr> <size>
> >     psram_free: psram_free <addr>
> >     psram_malloc: psram_malloc <length>
> >     psram_state: psram_state
> >     psram_task_create: create task on psram
> >     psram_task_delete: delete task on psram
> >     psram_test: start|stop
> >     psram_test_ext: init|byte|word|rewirte|deinit
> >     puf: puf {version|enrollment|read_uid}
> >     rc: wifi rate control config
> >     reboot: reboot system
> >     regdump: regdump {module}
> >     regshow: regshow -w/r addr [value]
> >     rfcali_cfg_mode: 1:manual, 0:auto
> >     rfcali_cfg_rate_dist: b g n40 ble (0-31)
> >     rfcali_cfg_tssi_b: 0-255
> >     rfcali_cfg_tssi_g: 0-255
> >     rfcali_flag_in_otp2:
> >     rfcali_show_data:
> >     rfcfg_test_log: 1:open,0:close
> >     rfconfig: rfconfig bt_polar|bt_btpll|bt_wifipll|wifi_btpll|wifi_wifipll
> >     rxsens: rxsens [-m] [-d] [-c] [-l]
> >     scan: scan [ssid]
> >     sdmadc: sdmadc_test
> >     set_arp_rate: set arp rate}
> >     set_interval: set listen interval}
> >     setcpufreq: setcpufreq [ckdiv_core] [ckdiv_bus] [ckdiv_cpu0] [ckdiv_cpu1]
> >     setjtagmode: set jtag mode {cpu0|cpu1|cpu2} {group1|group2}
> >     setprintport: set log/shell uart port 0/1/2
> >     sta: sta ssid [password][bssid][channel]
> >     stackguard: stackguard <override_len>
> >     start_hidden_softap: start_hidden_softap ssid [password] [channel[1:14]]
> >     starttype: show start reason type
> >     state: state - show STA/AP state
> >     stop: stop {sta|ap}
> >     tasklist: list tasks
> >     tempd: tempd [init|deinit|stop|start|update]
> >     time: system time
> >     timer: timer {chan} {start|stop|read} [...]
> >     touch_multi_channel_cyclic_calib_test: touch_multi_channel_cyclic_calib_test {start|stop} {0|1|2|3}
> >     touch_multi_channel_scan_mode_test: touch_multi_channel_scan_mode_test {start|stop} {0|1|2|3}
> >     touch_single_channel_calib_mode_test: touch_single_channel_calib_mode_test {0|1|...|15} {0|1|2|3}
> >     touch_single_channel_manul_mode_test: touch_single_channel_manul_mode_test {0|1|...|15} {calibration_value}
> >     touch_single_channel_multi_calib_test: touch_single_channel_multi_calib_test {0|1|...|15} {0|1|2|3}
> >     trng: trng {start|stop|get}
> >     trng_driver: {init|deinit}
> >     txevm: txevm [-m] [-c] [-l] [-r] [-w]
> >     uart: uart {id} {init|deinit|write|read|write_string|dump_statis} [...]
> >     uart_config: uart_config {id} {baud_rate|data_bits} [...]
> >     uart_driver: {init|deinit}
> >     uart_int: uart_int {id} {enable|disable|reg} {tx|rx}
> >     uid: uid [init/get]/
> >     version
> >     wdt: wdt {start|stop|feed} [...]
> >     wdt_driver: {init|deinit}
> >     wifi_diag: Wi-Fi HW diagnostics config
> > ```

<a id="arminocpswd"></a>

## **Armino平台CP系统swd调试**

cp系统支持在线调试，使用jlink工具及Eclipse上位机工具，即可快速搭建调式环境。

> - JLink环境通过Eclipse集成JLink gdb server \+ gdb 工具
> - Jlink和BK7258连线:
>
>   ```
>   1# VTref  ---- VREF
>   7# SWDIO  ---- SWDIO
>   9# SWCLK  ---- SWCLK
>   20# GND   ---- GND
>   ```
> - JLink软件版本
>   <https://www.segger.com/downloads/jlink/JLink_Windows_V768_x86_64.exe>
> - Arm工具链版本
>   <https://armkeil.blob.core.windows.net/developer/Files/downloads/gnu-rm/10.3-2021.10/gcc-arm-none-eabi-10.3-2021.10-win32.exe>
> - Eclipse版本
>   eclipse-embedcpp-2020-12-R-win32-x86\_64.zip
> - Eclipse工程配置
>
> > ![BK7258 JLink configuration](../../../../_assets/d7023a03e829199096a2-bk7236_jlink_config.png)
> >
> > ![BK7258 JLink configuration](../../../../_assets/6a6019dab2bb446aee72-bk7236_jlink_config2.png)
> >
> > ![BK7258 JLink configuration](../../../../_assets/5246f9ceeff366c26377-bk7236_jlink_config3.png)
>
> - 默认swd连接CP端，BK7258有两个Jtag口(grou1/group2)
> - 可以通过setjtagmode cpu0 group1命令设置swd连接cpu0(CP端)
> - 可以通过setjtagmode cpu1 group1设置swd连接cpu1(AP端)
> - 可以通过jtagmode命令查看当前jtag状态

备注

使用Jlink进行SWD调试连接，需要编译DEBUG版本。

如果是开机异常，在串口输入命令的形式可能无法连接上Jlink。可以在driver\_init里bk\_gpio\_driver\_init();之后手动调用：
bk\_set\_jtag\_mode(0,0); //第一个参数0表示调试cpu0，第二个参数0表示使用第一组SWD gpio管脚
while(g\_test\_mode); //定义一个volitale的全局变量，而不是while（1）；是防止编译器将后面的代码全部优化掉

然后接入Jlink后，修改g\_test\_mode变量值，开始往下调试。

由于GPIO管脚复用，所以默认版本接入JLINK调试，需要输入调试命令，或者在代码里设置调试模式：

- 关闭看门狗
- 重新配置SWD相关的gpio

<a id="swd"></a>

### swd调试示例

连接好jlink后，可以按照以下步骤打断点调试：

- 根据函数指针或者函数名在Disassembly页找到dump的地址

<a id="id3"></a>
![BK7258 JLink configuration](../../../../_assets/9f15249d2b618b049986-jlink_1.png)


示意图1

<a id="id4"></a>
![BK7258 JLink configuration](../../../../_assets/b3803ddff00cd57d08af-jlink_2.png)


示意图2

- 在dump函数之前的语句设置断点，将断点属性设置为hardware

<a id="id5"></a>
![BK7258 JLink configuration](../../../../_assets/ad07b4d183bda49f5700-jlink_3.png)


示意图3

- 点击resume继续运行程序。运行错误代码，如我在sta命令里，加了错误代码

<a id="id6"></a>
![BK7258 JLink configuration](../../../../_assets/fcd2976008c2e1498cd2-jlink_4.png)


示意图4

- 程序在断点处停下

<a id="id7"></a>
![BK7258 JLink configuration](../../../../_assets/28f1f90f97efe5a7837d-jlink_5.png)


示意图5

<a id="arminodump"></a>

## **Armino平台异常dump一键恢复现场工具**

> - 请参考发布工具中使用文档:
>   <https://dl.bekencorp.com/tools/Debug_tool/BK7258-debug.zip>
> - BK7258 dump工具常见问题:
>
>   - 默认Release版本dump功能是关闭的, 可以通过CONFIG\_DUMP\_ENABLE配置打开
>   - 当前的架构采用cp\+ap模式, 可以通过两者的config文件修改打开dump功能
>   - Dump工具恢复现场的原理是脚本通过分析log,解析出regs,itcm,dtcm,sram内容,然后通过gdb将这些内容恢复到qemu虚拟机中
>   - Log文件的后缀支持txt, log, DAT
>   - Log文件的编码当前只支持utf-8, 其他编码格式可用通过notepad\+\+手动转换为utf-8编码格式
>   - 如果工具目录下有多份Log, 或者Log中有多次Dump, 工具会分析最后一次Dump, 需要保证工具目录下只有一份Log, 且Log中只有一份dump
>   - Dump工具可以自动去掉日志里规则的时间戳: \[2024-02-03 14:35:13.375193\], 如果遇到不规则的时间戳, 需要手动去除
>   - Dump过程中如果出现2次异常, 常见的如检测内存越界时, 遇到Assert, 会多打印一次寄存器, 解析时需要删掉第二次寄存器打印
>   - 任一个cpu Dump都会将当前cpu的寄存器, itcm, dtcm, 以及640k sram全部dump出来
>   - 默认cp侧的Log和Dump通过UART0输出
>   - 默认ap侧的Log和Dump通过MAILBOX到cp再通过UART0输出
>   - Dump过程中如果遇到多个cpu同时dump, 需要将Log拆分成两份dump文件,分别用cp和ap的elf来恢复现场
>   - 每个cpu需要当前cpu的寄存器, itcm, dtcm, sram加上elf就可以恢复现场
>
>     > > 寄存器格式:
>     > >
>     > > ```
>     > > CPU1 Current regs: =========> CPU1 表示当前寄存器是cpu1出现异常的寄存器
>     > > 0 r0 x 0x0
>     > > 1 r1 x 0x28061ca0
>     > > 2 r2 x 0x0
>     > > 3 r3 x 0x8061ca0
>     > > 4 r4 x 0x28061d74
>     > > 5 r5 x 0x28061d70
>     > > 6 r6 x 0x28085a90
>     > > 7 r7 x 0x28061de4
>     > > 8 r8 x 0x8080808
>     > > 9 r9 x 0x9090909
>     > > 10 r10 x 0x10101010
>     > > 11 r11 x 0x11111111
>     > > 12 r12 x 0x1
>     > > 14 sp x 0x20000928
>     > > 15 lr x 0x21ec909
>     > > 16 pc x 0x21ec8fa
>     > > 17 xpsr x 0x61000000
>     > > 18 msp x 0x2808ff48
>     > > 19 psp x 0x20000908
>     > > 20 primask x 0x0
>     > > 21 basepri x 0x0
>     > > 22 faultmask x 0x0
>     > > 23 fpscr x 0x0
>     > > 30 CPU1 xPSR x 0x4
>     > > 31 LR x 0xfffffffd
>     > > 32 control x 0xc
>     > > 40 MMFAR x 0x8061ca0
>     > > 41 BFAR x 0x8061ca0
>     > > 42 CFSR x 0x82
>     > > 43 HFSR x 0x0
>     > > MemFault              =========> 初步异常原因是内存访问异常
>     > > ```
>     >
>     > dtcm格式:
>     >
>     > ```
>     > >>>>stack mem dump begin, stack_top=20000000, stack end=20004000
>     > <<<<stack mem dump end. stack_top=20000000, stack end=20004000
>     > ```
>     >
>     > itcm格式:
>     >
>     > ```
>     > >>>>stack mem dump begin, stack_top=00000020, stack end=00004000
>     > <<<<stack mem dump end. stack_top=00000020, stack end=00004000
>     > ```
>     >
>     > sram格式:
>     >
>     > ```
>     > >>>>stack mem dump begin, stack_top=28040000, stack end=28060000
>     > <<<<stack mem dump end. stack_top=28040000, stack end=28060000
>     >
>     > >>>>stack mem dump begin, stack_top=28060000, stack end=280a0000
>     > <<<<stack mem dump end. stack_top=28060000, stack end=280a0000
>     >
>     > >>>>stack mem dump begin, stack_top=28000000, stack end=28010000
>     > <<<<stack mem dump end. stack_top=28000000, stack end=28010000
>     >
>     > >>>>stack mem dump begin, stack_top=28010000, stack end=28020000
>     > <<<<stack mem dump end. stack_top=28010000, stack end=28020000
>     >
>     > >>>>stack mem dump begin, stack_top=28020000, stack end=28040000
>     > <<<<stack mem dump end. stack_top=28020000, stack end=28040000
>     > ```
>   - 当系统打开CONFIG\_MEM\_DEBUG时, Dump过程会将当前系统正在使用的Heap内存全部打印出来, 并检查是否有内存越界:
>
>     ```
>     tick       addr         size   line    func                               task
>     --------   ----------   ----   -----   --------------------------------   ----------------
>     6976       0x28064b68   80     425     xQueueGenericCreate                media_ui_task
>     6976       0x28064be0   80     425     xQueueGenericCreate                media_ui_task
>     6976       0x28064c58   160    425     xQueueGenericCreate                media_ui_task
>     6976       0x28064d20   1024   863     xTaskCreate_ex                     media_ui_task
>     6976       0x28065148   104    868     xTaskCreate_ex                     media_ui_task
>     6976       0x2807d098   80     425     xQueueGenericCreate                transfer_major_task
>     6976       0x2807d110   80     425     xQueueGenericCreate                transfer_major_task
>     ```
>   - 正常情况下也会将task相关信息dump到日志, 供问题分析时参考

<a id="armino"></a>

## **Armino平台系统稳定性问题分析**

嵌入式稳定性问题是一类常见但不容易定位的问题，其具有以下特征：

> - 不可预测性：系统故障的时间点不固定，难以预测，可能在长时间运行后突然发生
> - 多样性：问题可能以崩溃、死机、卡顿或错误行为等多种形式出现
> - 累计效应：系统运行时间越长，资源泄漏或数据损坏等问题可能积累，最终导致崩溃
> - 环境依赖性：稳定性还可能受温度、湿度和电源波动等环境因素的影响

为了帮助用户更好的定位稳定性问题，下面的链接文档中提供了常见的分析手段

备注

> 本文档仅针对软件引起的稳定性问题,建议用户在碰到稳定性问题时，优先参考该文档

- 文档 [下载链接](https://dl.bekencorp.com/tools/system_debug/稳定性问题软件分析.pdf)
- 文档内容说明:

  - 文中介绍了系统调试相关的工具，请参考上述章节
  - 文中列举了系统可能出现异常的各种场景
  - 文中还列举了一些经典的稳定性问题的分析案例
