**flink牛客网**

Flink 的 checkpoint 流程，都是同步 checkpoint 吗？ 

Flink 任务故障重启流程，full restart 和 region restart 区别，举例 region restart 

Window 的概念

这部分是实习项目里用到的比较有价值的点

- Flink 的 operator chain 机制一般会提升性能，但有耗时逻辑时把对应的 operator 拆开来跑，可以提高性能 
- 上游数据不均匀的情况下，采用 rebalance 的连接方式均衡消费 
- 多流 Join 的实现， connect stream + keyBy + CoProcessFunction + state 
- state 和 timerService 的使用，很关键的一点是延时任务是 per key per timestamp 的，这里踩过坑

  4、Flink backPressure反压机制，指标监控你是怎么做的

3、讲一讲Flink相比其他流式处理框架的优点（当时答了eventTime+watermark机制和窗口），讲一讲你对Flink窗口机制及其触发的了解

\11. Flink里的watermark和exactly-once语义如何实现