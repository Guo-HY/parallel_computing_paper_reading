# 论文概要

## 《论文1》

概述



## 《论文2》

概述



## 《论文3》

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
