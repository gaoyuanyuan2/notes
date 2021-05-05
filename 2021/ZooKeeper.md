### 什么是ZooKeeper

ZooKeeper是一个开源的分布式协同服务系统。ZooKeeper 的设计目标是将那些复杂且容易出错的分布式协同服务封装起来,抽象出一个高效可靠的原语集, 并以一系列简单的接口提供给用户使用。

* Hadoop :使用ZooKeeper做Namenode的高可用。
* HBase :保证集群中只有一个master ,保存集群中的RegionServer列表,保存
* hbase:meta表的位置。
* Kafka :集群成员管理, controller 节点选举。

ZooKeeper适用于存储和协同相关的关键数据,不适合用于大数据量存。
