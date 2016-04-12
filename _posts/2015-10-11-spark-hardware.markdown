---
layout: blogs_item
title: Spark的硬件配置
author: AcePeak
categories:
  - 积累
tags:
  - spark
  - hadoop
  - 大数据
  - 转载
---

从MapReduce的兴起，就带来一种思路，就是希望通过大量廉价的机器来处理以前需要耗费昂贵资源的海量数据。这种方式事实上是一种架构的水平伸缩模式——真正的以量取胜。毕竟，以现在的硬件发展来看，CPU的核数、内存的容量以及海量存储硬盘，都慢慢变得低廉而高效。然而，对于商业应用的海量数据挖掘或分析来看，硬件成本依旧是开发商非常关注的。当然最好的结果是：既要马儿跑得快，还要马儿少吃草。

Spark相对于Hadoop的MapReduce而言，确乎要跑得迅捷许多。然而，Spark这种In-Memory的计算模式，是否在硬件资源尤其是内存资源的消耗上，要求更高呢？我既找不到这么多机器，也无法租用多台虚拟instance，再没法测评的情况下，只要寻求Spark的官方网站，又或者通过Google搜索。从Spark官方网站，Databricks公司Patrick Wendell的演讲以及Matei Zaharia的Spark论文，找到了一些关于Spark硬件配置的支撑数据。

Spark与存储系统

如果Spark使用HDFS作为存储系统，则可以有效地运用Spark的standalone mode cluster，让Spark与HDFS部署在同一台机器上。这种模式的部署非常简单，且读取文件的性能更高。当然，Spark对内存的使用是有要求的，需要合理分配它与HDFS的资源。因此，需要配置Spark和HDFS的环境变量，为各自的任务分配内存和CPU资源，避免相互之间的资源争用。

若HDFS的机器足够好，这种部署可以优先考虑。若数据处理的执行效率要求非常高，那么还是需要采用分离的部署模式，例如部署在Hadoop YARN集群上。

Spark对磁盘的要求

Spark是in memory的迭代式运算平台，因此它对磁盘的要求不高。Spark官方推荐为每个节点配置4-8块磁盘，且并不需要配置为RAID（即将磁盘作为单独的mount point）。然后，通过配置spark.local.dir来指定磁盘列表。

Spark对内存的要求

Spark虽然是in memory的运算平台，但从官方资料看，似乎本身对内存的要求并不是特别苛刻。官方网站只是要求内存在8GB之上即可（Impala要求机器配置在128GB）。当然，真正要高效处理，仍然是内存越大越好。若内存超过200GB，则需要当心，因为JVM对超过200GB的内存管理存在问题，需要特别的配置。

内存容量足够大，还得真正分给了Spark才行。Spark建议需要提供至少75%的内存空间分配给Spark，至于其余的内存空间，则分配给操作系统与buffer cache。这就需要部署Spark的机器足够干净。

考虑内存消耗问题，倘若我们要处理的数据仅仅是进行一次处理，用完即丢弃，就应该避免使用cache或persist，从而降低对内存的损耗。若确实需要将数据加载到内存中，而内存又不足以加载，则可以设置Storage Level。0.9版本的Spark提供了三种Storage Level：MEMORY_ONLY（这是默认值），MEMORY_AND_DISK，以及DISK_ONLY。

关于数据的持久化，Spark默认是持久化到内存中。但它也提供了三种持久化RDD的存储方式：

in-memory storage as deserialized Java objects

in-memory storage as serialised data

on-disk storage

第一种存储方式性能最优，第二种方式则对RDD的展现方式（Representing）提供了扩展，第三种方式则用于内存不足时。

然而，在最新版（V1.0.2）的Spark中，提供了更多的Storage Level选择。一个值得注意的选项是OFF_HEAP，它能够将RDD以序列化格式存储到Tachyon中。相比MEMORY_ONLY_SER，这一选项能够减少执行垃圾回收，使Spark的执行器（executor）更小，并能共享内存池。Tachyon是一个基于内存的分布式文件系统，性能远超HDFS。Tachyon与Spark同源同宗，都烙有伯克利AMPLab的印记。目前，Tachyon的版本为0.5.0，还处于实验阶段。

注意，RDDs是Lazy的，在执行Transformation操作如map、filter时，并不会提交Job，只有在执行Action操作如count、first时，才会执行Job，此时才会进行数据的加载。当然，对于一些shuffle操作，例如reduceByKey，虽然仅是Transformation操作，但它在执行时会将一些中间数据进行持久化，而无需显式调用persist()函数。这是为了应对当节点出现故障时，能够避免针对大量数据进行重计算。要计算Spark加载的Dataset大小，可以通过Spark提供的Web UI Monitoring工具来帮助分析与判断。

Spark的RDD是具有分区（partition）的，Spark并非是将整个RDD一次性加载到内存中。Spark针对partition提供了eviction policy，这一Policy采用了LRU（Least Recently Used）机制。当一个新的RDD分区需要计算时，如果没有合适的空间存储，就会根据LRU策略，将最少访问的RDD分区弹出，除非这个新分区与最少访问的分区属于同一个RDD。这也在一定程度上缓和了对内存的消耗。

Spark对内存的消耗主要分为三部分：

数据集中对象的大小；

访问这些对象的内存消耗；

垃圾回收GC的消耗。

一个通常的内存消耗计算方法是：内存消耗大小= 对象字段中原生数据 * (2~5)。 这是因为Spark运行在JVM之上，操作的Java对象都有定义的“object header”，而数据结构（如Map，LinkedList）对象自身也需要占用内存空间。此外，对于存储在数据结构中的基本类型，还需要装箱（Boxing）。Spark也提供了一些内存调优机制，例如执行对象的序列化，可以释放一部分内存空间。还可以通过为JVM设置flag来标记存放的字节数（选择4个字节而非8个字节）。在JDK 7下，还可以做更多优化，例如对字符编码的设置。这些配置都可以在spark-env.sh中设置。

Spark对网络的要求

Spark属于网络绑定型系统，因而建议使用10G及以上的网络带宽。

Spark对CPU的要求

Spark可以支持一台机器扩展至数十个CPU core，它实现的是线程之间最小共享。若内存足够大，则制约运算性能的就是网络带宽与CPU数。

Spark官方利用Amazon EC2的环境对Spark进行了基准测评。例如，在交互方式下进行数据挖掘（Interative Data Mining），租用Amazon EC2的100个实例，配置为8核、68GB的内存。对1TB的维基百科页面查阅日志（维基百科两年的数据）进行数据挖掘。在查询时，针对整个输入数据进行全扫描，只需要耗费5-7秒的时间。如下图所示：

![DataSize](/img/151011_1.png)

在Matei Zaharia的Spark论文中还给出了一些使用Spark的真实案例。视频处理公司Conviva，使用Spark将数据子集加载到RDD中。报道说明，对于200GB压缩过的数据进行查询和聚合操作，并运行在两台Spark机器上，占用内存为96GB，执行完全部操作需要耗费30分钟左右的时间。同比情况下，Hadoop需要耗费20小时。注意：之所以200GB的压缩数据只占用96GB内存，是因为RDD的处理方式，使得我们可以只加载匹配客户过滤的行和列，而非所有压缩数据。
