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

Geohashes是交错的纬度和经度位的base32编码字符串。geohash 中的每个字符都会向精度增加额外的 5 位。因此，哈希值越长，它就越精确。出于索引目的，地理哈希被转换为经纬度对。在此过程中，仅使用前 12 个字符，因此在 geohash 中指定超过 12 个字符不会提高精度。

### Keyword type family

* 关键字系列包括以下字段类型：
  * 关键字，用于结构化内容，如 ID、电子邮件地址、主机名、状态代码、邮政编码或标签。
  * 对于始终包含相同值的关键字字段，constant_keyword。
  * 非结构化机器生成内容的通配符。该类型针对具有较大值或高基数的字段进行了优化。wildcard
* 关键字字段通常用于排序、聚合和术语级查询

* 请考虑将数字标识符映射为以下情况：keyword
  * 不打算使用范围查询搜索标识符数据。
C快速检索非常重要。 对字段的查询搜索通常比对数值字段的搜索更快。termkeywordterm
* 如果不确定要使用哪种类型，可以使用多字段将数据映射为 a数据类型和数值数据类型。keyword

* 在以下情况下使用字段类型：text
  * 内容是人类可读的，例如电子邮件正文或产品描述。
  * 您计划使用全文查询在字段中搜索单个单词或短语，例如 。Elasticsearch分析字段以返回与这些查询最相关的结果。

* 文本系列包括以下字段类型：
  * text，全文内容（如电子邮件正文或产品描述）的传统字段类型。
  * match_only_text，一个空间优化的变体，它禁用了评分，并且在需要位置的查询上执行速度较慢。它最适合为日志消息编制索引。text

### Numeric field types

应该选择适合您的用例的最小类型。这将有助于提高索引和搜索的效率。

### Point field typeedit

数据类型有助于索引和搜索落在二维平面坐标系中的任意对。point x, y

### Range field typesedit

范围字段类型表示介于上限和下限之间的连续值范围。

