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



## An_Adaptive_Cache_Coherence_Protocol_Optimized_for_Producer-Consumer_Sharing

### 翻译

共享内存的多处理器在企业和科研的计算设施中是一个很重要的角色。
远程未命中限制了共享内存应用的性能，在网络延迟越来越低的环境下，远程未命中对于处理器速度的影响显得越来越大。
本文提出了两个方法来改善共享内存的性能：消除远程未命中，和降低维持缓存一致性的成本。
我们聚焦于改善显示出生产者-消费者共享关系的应用的性能。
我们首先提供了一个简单的硬件方法来探测生产者-消费者式的共享，然后描述了一个目录委托方法，通过这个方法，一个缓存的“家节点”可以被委托成生产者节点，因此可以将3hop一致性操作转换成2hop一致性操作。

然后，我们扩展了委托机制，以支持生产者-消费者模式访问数据的推测性更新，这可以将2跳失误转换为本地失误，从而消除远程内存延迟。

这两种机制都可以在不改变处理器的情况下实现。
我们在七个基准程序上评估了我们的目录委托和推测性更新机制，这些程序使用未来16节点SGI多处理器的周期精确的执行驱动模拟器，表现出生产者-消费者共享。

我们发现，本文提出的机制将平均远程失误率降低了40%，将网络流量降低了15%，并将性能提高了21%。

最后，我们用Murphi来验证每个机制是没有错误的，并且不违反顺序一致性。

### 原文

Shared memory multiprocessors play an increasingly important role in enterprise and scientific computing facilities.
Remote misses limit the performance of shared memory applications, and their significance is growing as network latency
increases relative to processor speeds.

This paper proposes two mechanisms that improve shared memory performance by eliminating remote misses and/or reducing the amount of communication required to maintain coherence. 

We focus on improving the performance of applications that exhibit producer-consumer sharing. 

We first present a simple hardware mechanism for detecting producerconsumer sharing. We then describe a directory delegation mechanism whereby the "home node" of a cache line can be delegated to a producer node, thereby converting 3-hop coherence operations into 2-hop operations. 

We then extend the delegation mechanism to support speculative updates for data accessed in a producer-consumer pattern, which can convert 2-hop misses into local misses, thereby eliminating the remote memory latency. 

Both mechanisms can be implemented without changes to the processor. 
We evaluate our directory delegation and speculative update mechanisms on seven benchmark programs that exhibit producer-consumer sharing using a cycle-accurate executiondriven simulator of a future 16-node SGI multiprocessor.

We find that the mechanisms proposed in this paper reduce the average remote miss rate by 40%, reduce network traffic by 15%, and improve performance by 21%. 

Finally, we use Murphi to verify that each mechanism is error-free and does not violate 
sequential consistency.
