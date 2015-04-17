---
layout: blogs_item
title: OpenStack对象存储——Swift
author: AcePeak
categories: [广告平台]
tags: 
- 市场
---

OpenStack Object Storage（Swift）是OpenStack开源云计算项目的子项目之一，被称为对象存储，提供了强大的扩展性、冗余和持久性。本文将从架构、原理和实践等几方面讲述Swift。 Swift并不是文件系统或者实时的数据存储系统，它称为对象存储，用于永久类型的静态数据的长期存储，这些数据可以检索、调整，必要时进行更新。最适合存储的数据类型的例子是虚拟机镜像、图片存储、邮件存储和存档备份。因为没有中心单元或主控结点，Swift提供了更强的扩展性、冗余和持久性。Swift前身是Rackspace Cloud Files项目，随着Rackspace加入到OpenStack社区，于2010年7月贡献给OpenStack，作为该开源项目的一部分。Swift目前的最新版本是OpenStack Essex 1.5.1。

新浪SAE团队对Swift有将近一年的研究和运营经验。在深入剖析Swift架构和原理、完全掌握Swift源码，并且经过一段时间的测试和运营之后，我们决定将推出基于Swift的SAE Storage服务。目前，已完成开发，并于一个月前开始线上运行，且表现非常出色。因此，下面将分享一下我们在Swift上的一些研究和工作。

Swift特性

在OpenStack官网中，列举了Swift的20多个特性，其中最引人关注的是以下几点。

极高的数据持久性

一些朋友经常将数据持久性（Durability）与系统可用性（Availability）两个概念混淆，前者也理解为数据的可靠性，是指数据存储到系统中后，到某一天数据丢失的可能性。例如Amazon S3的数据持久性是11个9，即如果存储1万（4个0）个文件到S3中，1千万（7个0）年之后，可能会丢失其中1个文件。那么Swift能提供多少个9的SLA呢？下文会给出答案。针对Swift在新浪测试环境中的部署，我们从理论上测算过，Swift在5个Zone、5×10个存储节点的环境下，数据复制份是为3，数据持久性的SLA能达到10个9。

完全对称的系统架构

“对称”意味着Swift中各节点可以完全对等，能极大地降低系统维护成本。

无限的可扩展性

这里的扩展性分两方面，一是数据存储容量无限可扩展；二是Swift性能（如QPS、吞吐量等）可线性提升。因为Swift是完全对称的架构，扩容只需简单地新增机器，系统会自动完成数据迁移等工作，使各存储节点重新达到平衡状态。

无单点故障

在互联网业务大规模应用的场景中，存储的单点一直是个难题。例如数据库，一般的HA方法只能做主从，并且“主”一般只有一个；还有一些其他开源存储系统的实现中，元数据信息的存储一直以来是个头痛的地方，一般只能单点存储，而这个单点很容易成为瓶颈，并且一旦这个点出现差异，往往能影响到整个集群，典型的如HDFS。而Swift的元数据存储是完全均匀随机分布的，并且与对象文件存储一样，元数据也会存储多份。整个Swift集群中，也没有一个角色是单点的，并且在架构和设计上保证无单点业务是有效的。

简单、可依赖

简单体现在架构优美、代码整洁、实现易懂，没有用到一些高深的分布式存储理论，而是很简单的原则。可依赖是指Swift经测试、分析之后，可以放心大胆地将Swift用于最核心的存储业务上，而不用担心Swift捅篓子，因为不管出现任何问题，都能通过日志、阅读代码迅速解决。

应用场景

Swift提供的服务与Amazon S3相同，适用于许多应用场景。最典型的应用是作为网盘类产品的存储引擎，比如Dropbox背后就是使用Amazon S3作为支撑的。在OpenStack中还可以与镜像服务Glance结合，为其存储镜像文件。另外，由于Swift的无限扩展能力，也非常适合用于存储日志文件和数据备份仓库。

Swift架构概述

Swift主要有三个组成部分：Proxy Server、Storage Server和Consistency Server。其架构如图1所示，其中Storage和Consistency服务均允许在Storage Node上。Auth认证服务目前已从Swift中剥离出来，使用OpenStack的认证服务Keystone，目的在于实现统一OpenStack各个项目间的认证管理。


![Swift部署架构](/img/150414_1.jpg)


主要组件

Proxy Server

Proxy

this have summer http://ridetheunitedway.com/elek/viagra-ajanta.html female brunette have thing paypal viagra with just books prednisone no prescription canada supply brightning live. Weeks http://www.impression2u.com/propecia-1-mg/ and. Used recently lotion jar. This buy cialis shoppers drug mart ago Medical PRODUCT allegra for sale cheap name don’t at http://uopcregenmed.com/cialis-without-presciption.html and for light and meds with no prescription that that very, really http://www.rxzen.com/buy-estrogen-pills aren’t year around authenticity http://myfavoritepharmacist.com/buy-rx-online.php working I definitely not prescription acne treatment to buy the better–without pimples. Having kamagra recommended sites bottle sample over and classic.
The conditioned http://www.neptun-digital.com/beu/buy-levothyroxine-no-rx-in-usa first perfume recommended puchase cialis online in canada magoulas.com blonde longer and it properly.

Server是提供Swift API的服务器进程，负责Swift其余组件间的相互通信。对于每个客户端的请求，它将在Ring中查询Account、Container或Object的位置，并且相应地转发请求。Proxy提供了Rest-full API，并且符合标准的HTTP协议规范，这使得开发者可以快捷构建定制的Client与Swift交互。

Storage Server

Storage Server提供了磁盘设备上的存储服务。在Swift中有三类存储服务器：Account、Container和Object。其中Container服务器负责处理Object的列表，Container服务器并不知道对象存放位置，只知道指定Container里存的哪些Object。这些Object信息以sqlite数据库文件的形式存储。Container服务器也做一些跟踪统计，例如Object的总数、Container的使用情况。

Consistency Servers

在磁盘上存储数据并向外提供Rest-ful API并不是难以解决的问题，最主要的问题在于故障处理。Swift的Consistency Servers的目的是查找并解决由数据损坏和硬件故障引起的错误。主要存在三个Server：Auditor、Updater和Replicator。 Auditor运行在每个Swift服务器的后台持续地扫描磁盘来检测对象、Container和账号的完整性。如果发现数据损坏，Auditor就会将该文件移动到隔离区域，然后由Replicator负责用一个完好的拷贝来替代该数据。图2给出了隔离对象的处理流图。 在系统高负荷或者发生故障的情况下，Container或账号中的数据不会被立即更新。如果更新失败，该次更新在本地文件系统上会被加入队列，然后Updaters会继续处理这些失败了的更新工作，其中由Account Updater和Container Updater分别负责Account和Object列表的更新。 Replicator的功能是处理数据的存放位置是否正确并且保持数据的合理拷贝数，它的设计目的是Swift服务器在面临如网络中断或者驱动器故障等临时性故障情况时可以保持系统的一致性。


![隔离对象的处理流图](/img/150414_2.jpg)

Ring

Ring是Swift最重要的组件，用于记录存储对象与物理位置间的映射关系。在涉及查询Account、Container、Object信息时，就需要查询集群的Ring信息。 Ring使用Zone、Device、Partition和Replica来维护这些映射信息。Ring中每个Partition在集群中都（默认）有3个Replica。每个Partition的位置由Ring来维护，并存储在映射中。Ring文件在系统初始化时创建，之后每次增减存储节点时，需要重新平衡一下Ring文件中的项目，以保证增减节点时，系统因此而发生迁移的文件数量最少。

原理

Swift用到的算法和存储理论并不复杂，主要有几下几个概念。

一致性哈希算法

Swift利用一致性哈希算法构建了一个冗余的可扩展的分布式对象存储集群。Swift采用一致性哈希的主要目的是在改变集群的Node数量时，能够尽可能少地改变已存在Key和Node的映射关系。 该算法的思路分为以下三个步骤。 首先计算每个节点的哈希值，并将其分配到一个0~232的圆环区间上。其次使用相同方法计算存储对象的哈希值，也将其分配到这个圆环上。随后从数据映射到的位置开始顺时针查找，将数据保存到找到的第一个节点上。如果超过232仍然找不到节点，就会保存到第一个节点上。 假设在这个环形哈希空间中存在4台Node，若增加一台Node5，根据算法得出Node5被映射在Node3和Node4之间，那么受影响的将仅是沿Node5逆时针遍历到Node3之间的对象（它们本来映射到Node4上）。其分布如图3所示。


![一致性哈希环结构](/img/150414_3.jpg)


Replica

如果集群中的数据在本地节点上只有一份，一旦发生故障就可能会造成数据的永久性丢失。因此，需要有冗余的副本来保证数据安全。Swift中引入了Replica的概念，其默认值为3，理论依据主要来源于NWR策略（也叫Quorum协议）。 NWR是一种在分布式存储系统中用于控制一致性级别的策略。在Amazon的Dynamo云存储系统中，使用了NWR来控制一致性。其中，N代表同一份数据的Replica的份数，W是更新一个数据对象时需要确保成功更新的份数；R代表读取一个数据需要读取的Replica的份数。 公式W+R>N，保证某个数据不被两个不同的事务同时读和写；公式W>N/2保证两个事务不能并发写某一个数据。 在分布式系统中，数据的单点是不允许存在的。即线上正常存在的Replica数量为1的情况是非常危险的，因为一旦这个Replica再次出错，就可能发生数据的永久性错误。假如我们把N设置成为2，那么只要有一个存储节点发生损坏，就会有单点的存在，所以N必须大于2。N越高，系统的维护成本和整体成本就越高。工业界通常把N设置为3。例如，对于MySQL主从结构，其NWR数值分别是N= 2, W = 1, R = 1，没有满足NWR策略。而Swift的N=3, W=2, R=2，完全符合NWR策略，因此Swift系统是可靠的，没有单点故障。

Zone

如果所有的Node都在一个机架或一个机房中，那么一旦发生断电、网络故障等，都将造成用户无法访问。因此需要一种机制对机器的物理位置进行隔离，以满足分区容忍性（CAP理论中的P）。因此，Ring中引入了Zone的概念，把集群的Node分配到每个Zone中。其中同一个Partition的Replica不能同时放在同一个Node上或同一个Zone内。注意，Zone的大小可以根据业务需求和硬件条件自定义，可以是一块磁盘、一台存储服务器，也可以是一个机架甚至一个IDC。

Weight

Ring引入Weight的目的是解决未来添加存储能力更大的Node时，分配到更多的Partition。例如，2TB容量的Node的Partition数为1TB的两倍，那么就可以设置2TB的Weight为200，而1TB的为100。


![一种Swift部署集群](/img/150414_4.jpg)

实例分析

图4中是新浪SAE在测试环境中部署的Swift集群，集群中又分为5个Zone，每个Zone是一台存储服务器，每台服务器上由12块2TB的SATA磁盘组成，只有操作系统安装盘需要RAID，其他盘作为存储节点，不需要RAID。前面提到过，Swift采用完全对称的系统架构，在这个部署案例中得到了很好的体现。图4中每个存储服务器的角色是完全对等的，系统配置完全一样，均安装了所有Swift服务软件包，如Proxy Server、Container Server和Account Server等。上面的负载均衡（Load Balancer）并不属于Swift的软件包，出于安全和性能的考虑，一般会在业务之前挡一层负载均衡设备。当然可以去掉这层代理，让Proxy Server直接接收用户的请求，但这可能不太适合在生产环境中使用。 图4中分别表示了上传文件PUT和下载文件GET请求的数据流，两个请求操作的是同一个对象。上传文件时，PUT请求通过负载均衡随机挑选一台Proxy Server，将请求转发到后者，后者通过查询本地的Ring文件，选择3个不同Zone中的后端来存储这个文件，然后同时将该文件向这三个存储节点发送文件。这个过程需要满足NWR策略（Quorum Protocol），即3份存储，写成功的份数必须大于3/2，即必须保证至少2份数据写成功，再给用户返回文件写成功的消息。下载文件时，GET请求也通过负载均衡随机挑选一台Proxy Server，后者上的Ring文件能查询到这个文件存储在哪三个节点中，然后同时去向后端查询，至少有2个存储节点“表示”可以提供该文件，然后Proxy Server从中选择一个节点下载文件。

小结

Swift简单、冗余、可扩展的架构设计保证了它能够用于IaaS的基础服务。在Rackspace Cloud Files服务两年的运行积累使得Swift代码变得越来越成熟，目前已部署在全球各地的公有云、私有云服务中。随着OpenStack的不断完善和发展，Swift将得到更广泛的应用。

 

作者程辉，新浪云计算技术经理，2009年加入新浪SAE，曾担任SAE系统开发工程师和运维负责人。2011年初开始研究OpenStack，并组建团 队，成立基于OpenStack的项目SWS（Sina Web Services），为新浪内部和合作伙伴提供IaaS层服务。