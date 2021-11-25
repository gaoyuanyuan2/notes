# ES 官方文档笔记

## Index Shard Allocation 

1、如果主节点只是等待几分钟，那么丢失的分片可以以最小的网络流量重新分配给节点 5。对于已自动同步刷新的空闲分片（未接收索引请求的分片），此过程将更快。

[delayed-allocation](https://www.elastic.co/guide/en/elasticsearch/reference/7.16/delayed-allocation.html)
