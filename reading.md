# 论文概要

## An Evaluation of Directory Schemes for Cache Coherence

### notes

这篇文章主要对比了目录式协议和广播/侦听协议，并且认为大型多处理器系统中目录式协议更有效率，而且更有可扩展性。

这篇文章使用的性能评估方法是trace模拟。

### Abstract

The problem of cache coherence in shared-memory multiprocessors has been addressed using two basic approaches: directory schemes and snoopy cache schemes. Directory schemes have been given less attention in the past several years, while snoopy cache methods have become extremely popular. Directory schemes for cache coherence are potentially attractive in large multiprocessor systems that are beyond the scaling limits of the snoopy cache schemes. Slight modifications to directory schemes can make them competitive in performance with snoopy cache schemes for small multiprocessors. Trace driven simulation, using data collected from several real multiprocessor applications, is used to compare the performance of standard directory schemes, modifications to these schemes, and snoopy cache protocols.

共享内存多处理器中的缓存一致性问题已使用两种基本方法解决：目录式方案和广播/侦听方案。在过去的几年里，目录方案很少受到关注，而 广播/侦听方法已经变得非常流行。用于缓存一致性的目录方案在超出广播/侦听 缓存方案的扩展限制的大型多处理器系统中具有潜在的吸引力。对目录方案的轻微修改可以使它们在性能上与小型多处理器的广播/侦听缓存方案具有竞争力。跟踪驱动的模拟，使用从几个真实的多处理器应用程序收集的数据，用于比较标准目录方案、对这些方案的修改和 snoopy 缓存协议的性能。

### Conclusions

这篇文章展示了在大型多处理器系统中使用目录式缓存一致性方案提供共享内存模型是一种值得研究的方法。目录式方案在去掉广播/侦听方案的主要限制-广播操作的同时，在处理缓存一致性中可以获得和广播/侦听方案相近的效率。目录所需要的带宽长期以来被认为是潜在的瓶颈，然而这篇文章展示了目录所需要的带宽远没有内存需要的带宽多。对内存和目录的带宽的基本限制可以通过将它们分散到多个处理器板上来缓解。这种技术允许目录和内带宽随着处理器数量增加而增长。

我们使用trace驱动的模拟在小型多处理器系统上评估了目录方案的性能。目录式方案的性能相比广播/侦听方案很有竞争力。另外仿真还显示出大多数被写入的块都集中在少数cache上，这使得广播操作很低效。这个结果显示目录式方案是高效的。在大型多处理器系统中使用目录式方案来提供共享内存模型将会取得很高的效率。

### Introduction

简略介绍了一下广播/侦听式缓存一致性协议与目录式缓存一致性协议。

广播/侦听式缓存一致性协议的特点是所有的需要别的cache的状态变化或者从别的cache获取数据的事务都需要在总线上进行广播。

广播/侦听式缓存一致性协议在小型多处理器系统上很流行，因为很方便。然而扩展到大型多处理器系统的可扩展性不好。同时这种协议影响着处理器与cache之间的带宽。

在这篇文章中我们指出目录式缓存一致性协议更适合构建大型多处理器系统。这篇文章首次使用来自真实处理器的trace来评估目录式缓存一致性协议。

### Directory Schemes for Cache Consistency

广播侦听协议主要缺点：

- 依赖总线，可扩展性弱

- 竞争处理器-cache之间的带宽

目录式协议相对于广播侦听协议的主要优点：

- 拥有共享数据块的缓存的地址是已知的，这意味着可以进行点对点通信，而不用广播。

#### 一些广播/侦听式协议

##### Tang's method

允许干净的块存在于多个cache中，但是不允许脏块存在于多于一个块中。每个cache中对每一个块保存一个dirty位。位于内存中的中央目录保存所有cache中块的tags和dirty位的拷贝。

##### Censier and Feautrier

感觉就是全位向量模式的Tang's method

#### 对广播/侦听式协议的分类法

$$
Dir_iX
$$

- i表示对于一个块在目录中可以存放的处理器索引个数
- X是B或NB。对于NB，i一定大于等于系统中处理器个数。

目录式协议有两个潜在的可扩展性相关的困难：

- 如果需要经常性的广播，那么性能一定不如广播/侦听式更好。
- 对目录的访问可能称为潜在的瓶颈。



### Evaluation Methodology

使用多处理器系统的内存访问trace。这样做的缺点是一种trace被用来评估所有的缓存一致性协议，然而由于不同的协议有不同的行为，在现实中对于同一个程序它们产生的trace大概利率是不同的。但是这种trace至少反映了真实程序的一种可能的内存trace，因此可以准确区分不同缓存一致性协议之间的性能。

同时消除了trace中cache冷启动带来的缺失。因此就剩下两种cache缺失了：

- 访问数据的缺失
- 由于一致性操作造成的缺失

我们希望只评估一致性操作对多处理器间交流于内存访问带宽的影响，因此假定cache无限大。

#### Performance Measures

我们希望评估的性能不依赖于特定的处理器架构或者互联网络结构。因此我们使用内存访问代价作为基本的评价标准。这个代价就是每一次数据传输需要花费的时钟周期。



## An Economical Solution to the Cache Coherence Problem 

### Abstract

在本文中，我们回顾并定性地评估了在紧密耦合的多处理器系统中保持高速缓存一致性的方案。这导致我们提出“全局目录”方法的更经济（硬件方面）、可扩展和模块化的变体。本文描述了此解决方案的协议。性能评估研究表明了这种方法可行的限制（处理器数量、共享级别）.

### A Spectrum of Solutions to the Cache Coherence Problem

简要回顾了已有的几种保持缓存一致性的方案。

- 软件保证

- 经典的方法（内存中数据永远是最新的）
- 目录式
- 广播/侦听式

### The Two-bit Directory Scheme







## An_Adaptive_Cache_Coherence_Protocol_Optimized_for_Producer-Consumer_Sharing

### Abstract

共享内存的多处理器在企业和科研的计算设施中是一个很重要的角色。
远程未命中限制了共享内存应用的性能，在网络延迟越来越低的环境下，远程未命中对于处理器速度的影响显得越来越大。
本文提出了两个方法来改善共享内存的性能：消除远程未命中，和降低维持缓存一致性的成本。
我们聚焦于改善显示出生产者-消费者共享关系的应用的性能。
我们首先提供了一个简单的硬件方法来探测生产者-消费者式的共享，然后描述了一个目录委托方法，通过这个方法，一个缓存的“家节点”可以被委托成生产者节点，因此可以将 3 次通讯一致性操作转换成 2 次通讯一致性操作。

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

### 出发点

- 对于生产者消费者模型，我们抽象为
     - 生产者向托盘写东西
     - 消费者向托盘读东西 

- 当生产者不处在主节点上时
     - 生产者每次写入需要 3 次网络通讯
          - 生产者向主节点申请独占读 
          - 主节点向生产者回复，主节点向消费者节点干预读
          - 消费者节点向生产者节点发送“我知道不读了”的消息
     - 消费者每次读取需要 3 次通讯
          - 消费者向主节点“我要读”
          - 主节点向生产者“不许写”，向消费者“可以读”
          - 生产者写回主节点，向消费者“现在可以读了” 
- 显然，这样做要等三次节点间通讯，代价有点大

#### 改进思想

- 改进一：使得“主节点”不是固定的了，作者提出了一种新的目录委托协议
     - 可以把“主节点”的工作委托给另一个节点
          - 主节点把请求转发给生产者节点
          - 其它知道“生产者当主节点”的消费者节点可以直接向生产者发请求 
     - 改善了生产者不在主节点时导致的通讯问题
     - 使得许多三通讯操作现在变成两通讯了
- 改进二：让“生产者主节点”预测其它消费者“要读”的数据（生产出东西就提前写回）
     - 这样就使得消费者每次读取变成了本地缓存失效，不用再两次通讯了
- 改进二的问题
     - 提前写回毕竟是一个投机取巧的事，容易出现人家不读你还写，瞎忙活占了总线流量
     - 所以说改进二能起到作用和预测的准确性关系很大
     - 作者的目标：使得这种预测机制的失败代价期望小于原来不预测时候的通信代价，这样总体上来说就是成功  
- 两个改进都是说减小节点间的通讯代价来改善性能 

### 具体实现

- 暂时还没看，感觉不用太细

## Using Preditcion to Accelerate Coherence Protocols

### Abstract

大多数共享内存的多核系统都采用目录式协议(*directory protocols*)为维护缓存一致性. 为了改善这个延迟, 研究者针对特定共享模式(例如*producer-consumer*, *read-modify-write*)来对一致性协议进行优化. 该文章力求使用检测一致性活动并且触发合适动作的预测逻辑 来代替上述直接的优化方案. 

该篇文章开创了通过预测(维护和评估*Cosmos*一致性消息预测器)来加速cache一致性协议的先河, 其沿用并扩展*Yeh and Patt's two-level PAp branch predictor*的思路, 来预测下一条发送至缓存块的一致性消息(*coherence message*)的消息来源和种类. 对于跑在16核多处理器的五个科学计算应用, *Cosmos*的预测成功率达到62%~93%.  这正是由于缓存块稳定的共享模式所发出的可预测一致性消息信号, *Cosmos*才会有如此高的预测正确率. 

### Conclusions

该文章探索了通过预测来加速一致性协议的一种方案. 如果可以预测出未来的一致性协议动作并可以提前执行, 则整个系统将会更快执行. 

该文章的第一个贡献在于*Cosmos*一致性消息预测器的设计. Cosmos使用类似于*Yeh and Patt's two-level PAp branch predictor*, 来预测下一条<处理器号, 消息种类>二元组. Cosmos所面临的更大挑战在于上述预测元组是多位的(*multi-bit*). 

该文章的第二个贡献在于提出一套详尽的对Comos预测器的效果评估方案. 在16核多处理器共享内存系统的目标机上, 使用5套科学基准来跑Stache directory protocol, Cosmos(及其几种变种)的预测成功率达到了惊人的62~69%(barnes), 84~86%(modlyn), 84~85(appbt)， 74~92%(unstructured), 和 84~93%(dsmc). 

Comos的高预测率源自于 与特定缓存块地址相关的一致性信号的可预测性. 共享模式所发出的信号在在程序执行过程中可能不会出现变化或变化程度较小. Cosmos比直接优化方案(*directed optimizations*)更加普适. 并且由于Cosmos所使用的资源更少, 其成本也更低. 

不过还需要进一步确定Cosmos如此高的预测率是否能真的减少执行时间. 该工作类似于将高预测率的分支预测器嵌入到微体系结构来更真实的评估预测器价值. 

### 文章结构

#### 1. 介绍

#### 2. 背景

- 目录式协议简单介绍(需要)

- Cosmos预测器参考的原型 -- PAp分支预测器(可选)
     - PAp分支预测器, 采用特殊硬件结构(Pattern History Table), 基于过去的分支行为来进行预测.

> Each entry in the Pattern History Table is a fsm, which returns predictions based
> on the behavior of a finite number of previous occurrences of this branch.

#### 3. 预测一致性消息

该部分主要讨论Cosmos预测器的需求, 基本结构以及预测原理. 

> This section describes the Cosmos coherence message predictor

- Cosmos基本结构 : Cosmos is a two-level adaptive predictor

  - The first-level table : Message History Table, which consists of a series of MHRs.  Message History Registers由多个二元组<sender, type>组成, 其代表过去几条到达该缓存块的一致性消息.

  - The Second-level table : Pattern History Tables, one for each MHR.

- Cosmos预测原理 (如何预测, 如何维护)

  - Obtaining Predictions from Cosmos(预测)

  - Updating Cosmos(维护)

- Cosmos的高适应性adaptive

#### 4. 一致性协议预测器的应用

该部分主要讨论如何把一致性消息预测器融入到一致性协议中. 

- 将Cosmos预测器的预测映射成动作, 并在合适的时间完成该动作.
- 能够监测预测的成功与否, 若预测失败则应进行回滚.

#### 5. 基于预测加速一致性协议动作的效果

- 理论加速比, 仅仅是理论上.
- 实验结果 : 包括实验情况下的预测成功率和该项指标的影响因素分析(后者可以不讲)

> 需要注意的是, 由于并没有真正将Cosmos嵌入式应用于支持某种一致性协议的硬件之中, 故而并没有应用实验结果分析.

- 与传统直接优化一致性协议的方式进行比较.
    - Cosmos成本开销大, 因为需要额外的硬件支持.
    - Cosmos嵌入难度较小.
    - Cosmos适用范围更加广, 其不仅可识别已知的共享模式, 还可适应于应用独属的共享模式. 
