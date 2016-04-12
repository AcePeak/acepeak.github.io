---
layout: blogs_item
title: 'Spark性能调优实战'
author: AcePeak
categories:
  - 积累
tags:
  - spark
  - 大数据
  - 转载
---

【原文地址  http://blog.csdn.net/zcc_0015/article/details/38460917】

Spark特别适用于多次操作特定的数据，分mem-only和mem & disk。其中mem-only:效率高，但占用大量的内存，成本很高;mem & disk:内存用完后，会自动向磁盘迁移，解决了内存不足的问题，却带来了数据的置换的消费。Spark常见的调优工具有nman、Jmeter和Jprofile,以下是Spark调优的一个实例分析：

1、场景：精确客户群

对一个容量为300g的客户信息表在spark上进行查询优化，该大宽表有1800多列，有效使用的有20列。

2、优化达到的效果：查询由原来的40.232s降低为2.7s

3、优化过程分析

第一步：首先发现磁盘存在大量的iowait，通过查看相关日志文件，发现一个block的大小进而推算出整个数据文件大小为300G整个内存无法容纳，采用压缩的方法实现优化，结合本数据文件的特点，存在大量的0和1，选 Gzip算法进行压缩，压缩后的大小为1.9G，该步使得查询从40.232降为了20.12s。

第二步：大宽表存在1800多列，而有效使用的只有20多列，故通过RCFILE只将有效的列加载，该步使得查询从20s降为12s。

第三步：通过Jprofile分析出CPU的负载过高，到底是什么原因造成的，仔细发现序列化机制有问题。Spark的serialization框架有两种：java自身的和kryo的。其中kryo 是一个快速高效的Java对象图形序列化框架,主要特点是性能、高效和易用，换成kryo后，查询从12s降到7s。

第四步：进一步分析CPU各核负载量很不均匀，内存也没有用满，系统的资源没有得到充分利用，该如何利用？ (1)Spark的RDD的partition个数创建task的个数是对应的;(2)Partition的个数在hadoop的RDD中由block的个数决定的，内存：系统总内存数=work内存大小*work数=SPARK_WORKER_MEMORY*SPARK_WORKER_INSTANCES;

CPU:系统总的task数=work数×work所占的cores数=SPARK_WORKER_INSTANCES*SPARK_WORKER_CORES，计算task并行度，内存分配情况，调优参数：

SPARK_WORKER_INSTANCES=4

SPARK_WORKER_CORES = 3

SPARK_WORKER_MEMORY = 6G

Cpu(12core)  mem(24G)，通过这几个参数的优化，查询由7s降到5s。

第五步：进一步发现Sharkserver端出现明显的fullGC,通过调优参数

Export SHARK_MASTER_MEM=2g,该步由6s降到3sl;

第六步：又发现当两表关联时，cpu 出现瓶颈，分析原因是日表做了gzip压缩，优化方法：日表不使用gzip压缩，将日表做成内存表。查询从3s降到2s。

4、总结

优化是一个逐步求精的过程，回顾该优化过程，主要是从以下几个因素考虑：(1)mem;(2)cpu;(3)dis;(4)网络IO;(5)序列化机制。认真这些因素为主线，挖掘与其相关的内容时行大胆尝试。
