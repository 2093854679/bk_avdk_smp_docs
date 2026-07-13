# CPU时钟源说明

CPU有以下时钟源：


- 26M

- DCO

- 320M

- 480M

备注：
CP主频最高可以达到240M（通过480M分频得到），AP主频最高可以达到480M。


## CPU主频切换说明


- 可以根据业务需要动态的切频率来达到最优功耗,CPU主频切换相对来说比较复杂,SDK内部来实现。
  具体如何切换CPU主频请参考 [如何动态切换CPU主频](bk_cpu_vote_freq.md "bk_cpu_vote_freq.md") 。

