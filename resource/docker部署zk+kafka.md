# docker部署zk+kafka
## 首先拉取镜像
```
docker pull wurstmeister/zookeeper
docker pull wurstmeister/kafka
```
## 启动zk
```
docker run -d --name zookeeper -p 2181:2181 -t wurstmeister/zookeeper
```
-d 表示退出不停止容器
--name 用于命名容器
-p 表示定义映射端口
-t 代表从什么镜像生成容器
## 启动kafka（需要定义）
```
docker run  -d --name kafka -p 9092:9092 -e KAFKA_BROKER_ID=0  -e KAFKA_ZOOKEEPER_CONNECT=10.10.17.43:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://10.10.17.43:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka 
```
其中-e 后面接的语句是kafka的特定定义
第一句定义broker的 id 这边单节点所以设为0
第二句代表它依赖的zk的ip:端口
listeners是kafka真正bind的地址
advertised.listeners是暴露给外部的listeners，如果没有设置，会用listeners（这边直接定义本机ID进行配置）
## 进入docker容器
```
docker exec -ti 容器名（打一半就行） bash
```
## 进入容器配置kafka
目录在 opt/kafka-版本号
进去之后就可以用原来的命令进行节点测试