#### MapReduce过程解析



分区数及reduce数目

一组数据只能放到一个reduce及一个分区之中计算，如果只有2组数据，开启了三个reduce则有一个reduce是空的。

当然两组数据可以放到一个reduce之中计算。

一个分片对应一个map

