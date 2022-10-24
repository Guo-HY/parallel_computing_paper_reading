# 论文概要

## An Evaluation of Directory Schemes for Cache Coherence

#### notes

这篇文章主要对比了目录式协议和广播/侦听协议，并且认为大型多处理器系统中目录式协议更有效率，而且更有可扩展性。

这篇文章使用的性能评估方法是trace模拟。

#### Abstract

The problem of cache coherence in shared-memory multiprocessors has been addressed using two basic approaches: directory schemes and snoopy cache schemes. Directory schemes have been given less attention in the past several years, while snoopy cache methods have become extremely popular. Directory schemes for cache coherence are potentially attractive in large multiprocessor systems that are beyond the scaling limits of the snoopy cache schemes. Slight modifications to directory schemes can make them competitive in performance with snoopy cache schemes for small multiprocessors. Trace driven simulation, using data collected from several real multiprocessor applications, is used to compare the performance of standard directory schemes, modifications to these schemes, and snoopy cache protocols.

共享内存多处理器中的缓存一致性问题已使用两种基本方法解决：目录式方案和广播/侦听方案。在过去的几年里，目录方案很少受到关注，而 广播/侦听方法已经变得非常流行。用于缓存一致性的目录方案在超出广播/侦听 缓存方案的扩展限制的大型多处理器系统中具有潜在的吸引力。对目录方案的轻微修改可以使它们在性能上与小型多处理器的广播/侦听缓存方案具有竞争力。跟踪驱动的模拟，使用从几个真实的多处理器应用程序收集的数据，用于比较标准目录方案、对这些方案的修改和 snoopy 缓存协议的性能。

#### Conclusions

这篇文章展示了在大型多处理器系统中使用目录式缓存一致性方案提供共享内存模型是一种值得研究的方法。目录式方案在去掉广播/侦听方案的主要限制-广播操作的同时，在处理缓存一致性中可以获得和广播/侦听方案相近的效率。目录所需要的带宽长期以来被认为是潜在的瓶颈，然而这篇文章展示了目录所需要的带宽远没有内存需要的带宽多。对内存和目录的带宽的基本限制可以通过将它们分散到多个处理器板上来缓解。这种技术允许目录和内带宽随着处理器数量增加而增长。

我们使用trace驱动的模拟在小型多处理器系统上评估了目录方案的性能。目录式方案的性能相比广播/侦听方案很有竞争力。另外仿真还显示出大多数被写入的块都集中在少数cache上，这使得广播操作很低效。这个结果显示目录式方案是高效的。在大型多处理器系统中使用目录式方案来提供共享内存模型将会取得很高的效率。



## 《论文2》

概述



