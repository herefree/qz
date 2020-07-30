#### Flink 面试题

https://zhuanlan.zhihu.com/p/95619533

https://cloud.tencent.com/developer/article/1550785

flink savepoint checkpoint区别
功能的原理是一样的, 只是目的不同, 一个是自动的备份, 另一个是手动的保持状态, 用做版本升级/服务重启等
flink checkpoint原理
意义: 被checkpoint保存的每个subtask的状态只有raw state和managed state两种。raw state是用户自己进行序列化，而managed state是在operator生命周期初始化时就被注册到backend storage对象中了，在进行checkpoint时，会直接拿到注册的state进行保存（中间会调用回调函数，在UDF中对state进行赋值）。所以checkpoint的state不是很大的数据。

exactly once小结: kafka, spark streaming receiverAPI 和directAPI, flink 都是如何保证exactly once的那?



flink如何保证exactly once的, 主要有以下两点
https://blog.csdn.net/rlnLo2pNEfx9c/article/details/81369878

1. 两阶段提交 预提交+实际提交 这是分布式事务的一种实现方式
2. checkpoint机制, 两次checkpoint之间为一次事务, 用checkpoint保证exactly once

加上分布式事务的checkpoint实现:
a.pre-commit阶段
Flink checkpointing开始时便进入到pre-commit阶段。具体来说，一旦checkpoint开始，Flink的JobManager向输入流中写入一个checkpoint barrier将流中所有消息分割成属于本次checkpoint的消息以及属于下次checkpoint的。barrier也会在操作算子间流转。对于每个operator来说，该barrier会触发operator状态后端为该operator状态打快照。例如flink kafka source保存Kafka消费offset, 当checkpoint barrier在所有operator都传递了一遍且对应的快照也都成功完成之后，pre-commit阶段才算完成。该过程中所有创建的快照都被视为是checkpoint的一部分
b.commit阶段
下一步就是通知所有的operator，告诉它们checkpoint已成功完成。这便是两阶段提交协议的第二个阶段：commit阶段。该阶段中JobManager会为应用中每个operator发起checkpoint已完成的回调逻辑。

什么时候会被降级到at least once
快照发生时，flink会在某些有状态的operator上对data record进行对齐操作（alignment），目的是避免失败恢复时重复消费数据。这个过程也是exactly once的保证。通常对齐操作的时间仅是毫秒级的。但是对于某些极端的应用，在每个operator上产生的毫秒级延迟也不能允许的话，则可以选择降级到at least once，即跳过对齐操作，当失败恢复时可能发生重复消费数据的情况

作者：THESUN4
https://www.nowcoder.com/discuss/341617?type=post&order=time&pos=&page=1&subType=2来源：牛客网

这部分是问的问题，基本官方文档都有

- Flink 的 Exactly Once 语义怎么保证 
- Flink 的 checkpoint 流程，都是同步 checkpoint 吗？ 
- Flink 任务故障重启流程，full restart 和 region restart 区别，举例 region restart 
- Window 的概念 

这部分是实习项目里用到的比较有价值的点

- Flink 的 operator chain 机制一般会提升性能，但有耗时逻辑时把对应的 operator 拆开来跑，可以提高性能 
- 上游数据不均匀的情况下，采用 rebalance 的连接方式均衡消费 
- 多流 Join 的实现， connect stream + keyBy + CoProcessFunction + state 
- state 和 timerService 的使用，很关键的一点是延时任务是 per key per timestamp 的，这里踩过坑 

其它主要问的是 Java 基础和算法题

- 实现 ImmutableStack 即 pop 和 push 都要生成新的 stack，要求复杂度为 O(1) 
- 二叉树中序和先序遍历数组，求后序遍历数组 
- 实现 36 进制加法 "1z"+"1" = "20"

3. flink中的window实现机制。

4. flink中状态的保存于实现机制。

数据倾斜

https://cloud.tencent.com/developer/article/1506784

- 简单介绍一下Flink
- Flink相比传统的Spark Streaming有什么区别？和Spark中的structured streaming 相比呢？Flink相比ss和storm有什么优势？
- Flink的组件栈是怎么样的？
- Flink的基础编程模型了解吗？
- 说说Flink架构中的角色和作用？
- 说说Flink中常用的算子？用过哪些？
- Flink中的分区策略有哪几种？
- Flink的并行度有了解吗？Flink中设置并行度需要注意什么？
- Flink支持哪几种重启策略？分别如何配置？
- **Flink的分布式缓存有什么作用？如何使用？**
- Flink中的广播变量，使用广播变量需要注意什么事项？
- Flink中对窗口的支持包括哪几种？说说他们的使用场景
- Flink 中的 State Backends是什么？有什么作用？分成哪几类？说说他们各自的优缺点？
- Flink中的时间种类有哪些？各自介绍一下？
- WaterMark是什么？是用来解决什么问题？如何生成水印？水印的原理是什么？
- Flink的table和SQL熟悉吗？Table API和SQL中TableEnvironment这个类有什么作用？
- Flink如何实现SQL解析的呢？

**进阶篇**

- Flink是如何做到批处理与流处理统一的？
- Flink中的数据传输模式是怎么样的？
- Flink的容错机制知道吗？
- Flink中的分布式快照机制是怎么样的？
- Flink是如何实现Exactly-once的？
- Flink的Kafka-connector是如何做到向下兼容的呢？
- Flink中的内存管理是如何做的？
- Flink中的序列化是如何做的？
- Flink中的RPC框架选型是怎么样的？
- Flink在使用Window时出现数据倾斜，你有什么解决办法？
- Flink SQL在使用Groupby时出现热点数据，如何处理？
- 现在我有Flink任务，delay极高，请问你有什么调优策略？
- Flink是如何处理反压的？和Spark有什么区别？Storm呢？
- Operator Chains（算子链）这个概念你了解吗？Flink是如何优化的？什么情况下Operator才会chain在一起？

**源码篇**

- 讲讲一个Flink job提交的整个流程吗？
- 讲讲一个Flink job调度和执行的流程吗？ 
- Flink所谓"三层图"结构是哪几个"图"？它们之间是什么关系？他们之间是如何转化的？
- JobManger和TaskManager分别在集群中扮演了什么角色，说说它们都做了些什么？
- 简单说说Flink数据的抽象和数据的交换过程 
- Flink的分布式快照机制是如何实现的？ 
- Flink的反压是如何实现的？
- 说说FlinkSQL是如何转化的？了解逻辑计划和和物理计划吗？FlinkSQL的维表JOIN是如何做的？了解Async IO吗？解决了什么问题？ 

