---
layout: blogs_item
title: Flume1.6.0连接Kafka0.8.2以及其中可能出现的问题
author: AcePeak
categories: [Internet]
tags: 
- 原生
- Flume
- Kafka
---




最终正确的example.conf文件如下：


{% highlight bash %}
 example.conf: A single-node Flume configuration

# Name the components on this agent
a1.sources = r2
a1.sinks = k1
a1.channels = c1

a1.sources.r1.type = netcat
a1.sources.r1.bind = localhost
a1.sources.r1.port = 44444

a1.sources.r2.type = org.apache.flume.source.kafka.KafkaSource
a1.sources.r2.zookeeperConnect = localhost:2181
a1.sources.r2.topic = my-replicated-topic

# Describe the sink
a1.sinks.k1.type = logger

# Use a channel which buffers events in memory
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

# Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sources.r2.channels = c1
a1.sinks.k1.channel = c1
{% endhighlight %}


问题：

1 Class Not Found

需要使用正确的type即KafkaSource，网上有些type是`org.apache.flume.plugins.KafkaSource`，已经与Flume1.6.0不兼容了。

{% highlight bash %}
a1.sources.r2.type = org.apache.flume.source.kafka.KafkaSource
{% endhighlight %}



2 Unable to start PollableSourceRunner

主要原因是zookeeper.jar没有被Flume找到，因此解决这个问题的步骤如下：

* clone flume.env.template and rename one to flume.env.
* edit flume.env and set the zookeeper path like this:

{% highlight bash %}
FLUME_CLASSPATH="/Codes/apache-kafka/kafka_2.10-0.8.2.2/libs/zookeeper-3.4.6.jar"
{% endhighlight %}

* restart flume

3 Flume与kafka通讯速度慢

把partition.key和partition.class配置去掉，调整flume日志级别为ERROR级，处理性能可以提升不少。

80万数据不到10S处理完成。

