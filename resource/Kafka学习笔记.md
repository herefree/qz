#### Kafka学习笔记

##### 一、配置与启动

config/server.properties

```shell
broker.id=0 #如果是集群的话每台机器从0开始依次
delete.topic.enable=true #设置是否可以删除主题
log.dirs=/xxxx               #设置kafka数据路径
zookeeper.connect=node01:2181,node02:2181,node03:2181#zookeeper路径

#配置外网访问的ip 需要填外网的ip
advertised.listeners=PLAINTEXT://ip:9092
```

启动

每台机器都要单独启动

```shell
./bin/kafka-server-start.sh -daemon config/server.properties
```

##### 二、命令行操作

```shell
#1.查看当前服务器中的所有topic
./bin/kafka-topics.sh --zookeeper 123.207.92.128:2181 --list
#2.创建topic
./bin/kafka-topics.sh --zookeeper 123.207.92.128:2181 --create --topic second --partitions 2 --replication-factor 1
#3.删除数据
./bin/kafka-topics.sh --zookeeper 123.207.92.128:2181 --delete --topic second
#4.查看详情
./bin/kafka-topics.sh --zookeeper 123.207.92.128:2181 --describe --topic first
#5.生产数据
./bin/kafka-console-producer.sh --broker-list 114.116.66.89:9100 --topic first
#6.消费数据
./bin/kafka-console-consumer.sh --bootstrap-server 114.116.66.89:9100 --topic first --from-beginning
```

