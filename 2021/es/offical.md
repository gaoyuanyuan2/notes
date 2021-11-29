# ES 官方文档笔记

## Index Shard Allocation 

1、如果主节点只是等待几分钟，那么丢失的分片可以以最小的网络流量重新分配给节点 5。对于已自动同步刷新的空闲分片（未接收索引请求的分片），此过程将更快。

[delayed-allocation](https://www.elastic.co/guide/en/elasticsearch/reference/7.16/delayed-allocation.html)

## mapping

### 防止映射爆炸的设置编辑

在索引中定义太多字段可能会导致映射爆炸，从而导致内存不足错误和难以恢复的情况。

考虑这样一种情况：插入的每个新文档都会引入新字段，例如动态映射。每个新字段都会添加到索引映射中，随着映射的增长，这可能会成为一个问题。

使用映射限制设置可以限制字段映射（手动或动态创建）的数量，并防止文档导致映射爆炸。

[Settings to prevent mapping explosionedit](https://www.elastic.co/guide/en/elasticsearch/reference/7.16/mapping.html#mapping-limit-settings)

### 运行时字段编辑

运行时字段在处理日志数据时很有用，尤其是在不确定数据结构时。搜索速度会降低，但索引大小要小得多，您可以更快地处理日志，而无需为日志编制索引。

为了平衡搜索性能和灵活性，请为您将经常搜索和筛选的字段（如时间戳）编制索引。Elasticsearch 在运行查询时会首先自动使用这些索引字段，从而缩短响应时间。

## Field data types

### Flattened field type

扁平化的对象字段在搜索功能方面存在权衡。只允许使用基本查询，不支持数值范围查询或突出显示。

用于以下查询类型：

* term和termsterms_set
* prefix
* range
* match和multi_match
* query_string和simple_query_string
* exists

### Geopoint field type

* 以查找边界框内、中心点一定距离内、多边形内或geo_shape查询内的地理点。
* 以地理方式或按距中心点的距离聚合文档。
* 将距离集成到文档的相关性分数中。
* 以按距离对文档进行排序。
