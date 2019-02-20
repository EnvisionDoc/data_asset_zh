# 术语

本文介绍数据资产管理涉及的术语。

## 流数据分析相关术语

与流数据分析相关的术语主要包括：流数据、流数据分析、数据类型、数据处理策略等。有关这些术语的详细解释，参见[流数据分析术语](https://www.envisioniot.com/docs/online-data/zh_CN/latest/streaming_concepts.html)。

## 数据订阅相关术语

数据订阅相关的专有名词及术语的定义和解释如下，方便你理解相关概念并使用数据订阅功能进行应用开发。

### Kafka

Kafka是一个分布式的消息系统，只需要把数据传给Kafka，在需要的时候可直接读取，实现异步非IO阻塞。

### Topic

消息主题，一级消息类型，通过 Topic 对消息流进行分类和存储。

### Partition

分区，每个Topic可以按特定的分区逻辑分区。Partition的数据决定了一个Topic可以同时支持的进程（用户）数量（如果一个Topic的Partition为3，那么Producer只能同时起3个进程写入，Consumer同时有3个进程进行消费，如果启动的数量超过3个则会一直等待）。

### Data producer

数据生产者，也称为消息发布者，生产并发送消息。

### Data consumer

数据消费者，也称为消息订阅者，接收并消费消息。

### Consumer instance

Consumer 的一个对象实例，不同的 Consumer 实例可以运行在不同进程内或者不同机器上。一个 Consumer 实例内配置线程池消费消息。

### Consumer group

一类 Consumer 的标识，这类 Consumer 通常接收并消费一类消息，且消费逻辑一致。

### Group consumption

集群消费。一个 Consumer Group 所标识的所有 Consumer 平均分摊消费消息。例如某个 Topic 有 9 条消息，一个 Consumer Group 有 3 个 Consumer 实例，那么在集群消费模式下每个实例平均分摊，只消费其中的 3 条消息。

### Sequential publish

顺序发布。对于指定的一个 Topic，客户端将按照一定的先后顺序发送消息。

### Sequential consumption

顺序消费。对于指定的一个 Topic，按照一定的先后顺序进行接收消息，即先发送的消息一定会先被客户端接收到。

### Message pileup

消息堆积。Producer 已经将消息发送到 订阅 服务端，但由于 Consumer 消费能力有限，未能在短时间内将所有消息正确消费掉，此时在 订阅 服务端保存着未被消费的消息，该状态即消息堆积。

### Message filtering

消息过滤。订阅者可以根据过滤条件对消息进行过滤，确保订阅者最终只接收被过滤后的数据。消息过滤在 订阅 服务端完成。

<!--

## About Storage Policy

To help you understand data storage policy related concepts and customize data storage policies, definition and description of related terms are as follows.

**Storage group**

A storage group is

**Storage type**

A storage type is

-->
