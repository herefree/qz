#### ES面试自己整理

1.es倒排索引与相关性算法

https://zhuanlan.zhihu.com/p/91603911

2.ES搜索流程

https://segmentfault.com/a/1190000019577908

3.ES模板

https://zhuanlan.zhihu.com/p/95532434

4.ES分词器

https://zhuanlan.zhihu.com/p/91604790

5.ES返回字段

```sql
{
    "took":4,                            请求花了多少时间
    "time_out":false,				  	 有没有超时
    "_shards":{    						 执行请求时查询的分片信息
        "total":5,     					 查询的分片数量
        "successful":5,  				 成功返回结果的分片数量
        "failed":0   					 失败的分片数量
    },
    "hits":{
        "total":2,       				 查询返回的文档总数
        "max_score":0.625,  			 计算所得的最高分
        "hits":[						 返回文档的hits数组
            {
                "_index":"books",		 索引
                "_type":"es",     		 属性
                "_id":"1",      		 标志符
                "_score":0.625,      	 得分
                "_source":{			  	 发送到索引的JSON对象
                    "title":"Elasticsearch Server",
                    "publish":2013
                }
            },
            {
                "_index":"books",
                "_type":"es",
                "_id":"2",
                "_score":0.19178301,
                "_source":{
                    "title":"Mastering Elasticsearch",
                    "published":2013
                }
            }
        ]
    }
}```
```

6.ES检索策略
6.5Elasticsearch写入过程
https://zhuanlan.zhihu.com/p/94915597

7.ES选主流程

https://www.cnblogs.com/zziawanblog/p/6577383.html

8.ES索引文档过程

9.三种分页方式

https://www.cnblogs.com/hello-shf/p/11543453.html

10.ES更新删除文档步骤

11.ES大数据量聚合如何实现？

12.并发，ES读写一致

13.ElasticSearch中的集群、节点、索引、文档、类型是什么

14.ElasticSearch中的分片是什么?

15.ES中的副本是什么

16.如何监控 Elasticsearch 集群状态？

17.介绍一下你们的个性化搜索方案？

18.拼写纠错是如何实现的？

19.如何压缩存储（增量存储），trie树

20.elasticsearch匹配具体命令，分词包用的什么

21.一次检索请求的流程

22.Shard 和 Replicas 的含义

23.Segment 文件会一直增加吗？

24.为什么 ElasticSearch 是近实时的？

25elasticsearch为什么检索快，它的底层数据结构是怎么样的

26.项目里面用了ElasticSearch，所以问了ES索引的构建和查询流程，跳跃表的构建和在ES中的使用，倒插排序、跳跃表的实现

27谈谈分布式搜索引擎的架构设计



28.**分布式搜索引擎服务于大数据量（百万上亿级）的优化查询功能是如何的**？-----保证内存filesystem ***足够大……ES+hbase架构……内存有限但数据量太大的情况下尽量把查找频繁的放入内存中，其他的放入hbase或者mysql中。元数据文档设计和分页上的优化……



29**Elasticsearch使用的索引与关系型数据库的索引异同和效率，为什么另一个索引机制更快**？-------其实就是ES使用的**倒排索引**和关系型数据库使用的**B-Tree**索引做个对比（实际上我没有手撕红黑树、B树的相关经验，仅仅停留在数据结构的皮毛阶段），大致地说了下树的高度logN复杂度，提高了逐个查询的慢效率，相当于**逐个查询**换成了**区间查**询。倒排索引查询就是根据文档内容查询文档

31.说一下Elasticsearch的原理

32.谈谈你用的ElasticSearch如何进行分布式索引的？如何实现的？

33.elasticSearch结构以及语法 index和term

34、Elasticsearch的索引，单field索引和多field的联合索引

35.[Elasticsearch索引原理](https://blog.csdn.net/cyony/article/details/65437708?locationNum=9&fps=1)
