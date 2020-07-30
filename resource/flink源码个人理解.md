**flink源码个人理解**

一、生成StreamGraph模块

http://matt33.com/2019/12/08/flink-stream-graph-2/

StreamGraph 内存储着StreamNode的Map，由StreamNode内部存储Streamedage

addStreamNode 然后addStreamedge的时候会得到StreamNode并在其中加入Streamedge，也就是说StreamNode里面存储着StreamEdge。