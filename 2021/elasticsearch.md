# Elasticsearch

## Elasticsearch 能做什么？

Elasticsearch 是一款非常强大的开源搜索及分析引擎。可以帮助你从海量数据中，快速找到相关的信息。Elasticsearch 不仅可以帮你找到相关的代码仓库，还可以帮助你实现代码级的搜索与高亮显示 ；当你在网上购物时，Elasticsearch 可以帮你推荐相关的商品；当你下班打车回家时，Elasticsearch 可以通过定位附近的乘客和司机，帮助平台优化调度。

除了搜索，结合 Kibana、Logstash、Beats，Elastic Stack 还被广泛运用在大数据近实时分析领域，包括日志分析、指标监控、信息安全等多个领域。它可以帮助你探索海量结构化、非结构化数据，按需创建可视化报表，对监控数据设置报警阈值。甚至通过使用机器学习技术，自动识别异常状况。

我到底能够使用 Elasticsearch 做什么？
数字、文本、地理位置、结构化数据、非结构化数据。适用于所有数据类型。全文本搜索只是全球众多公司利用 Elasticsearch 解决各种挑战的冰山一角。查看直接依托 Elastic Stack 所构建解决方案的完整列表。

Metrics
对您的系统指标进行监测和可视化。

APM
获得有关自己应用程序性能的洞见。
Uptime
监测可用性问题并进行应对。

Site Search
轻松为您的网站打造卓越的搜索体验。

App Search
搜索文档、地理数据等形形色色的内容。

Workplace Search
集中式搜索，应对企业内的数据孤岛情况。

Maps
实时探索位置数据。

SIEM
交互式调查和自动威胁检测。

Endpoint Security
预防、检测、猎捕并应对威

## 安装

docker pull docker.elastic.co/elasticsearch/elasticsearch:7.10.2

docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.10.2

查看节点：
http://localhost:9200/_cat/nodes


docker pull docker.elastic.co/kibana/kibana:7.10.2
docker run --link YOUR_ELASTICSEARCH_CONTAINER_NAME_OR_ID:elasticsearch -p 5601:5601 docker.elastic.co/kibana/kibana:7.10.2

docker pull docker.elastic.co/logstash/logstash:7.10.2


localhost:9200/_cat/nodes?v=true&pretty

docker-compose down -v

localhost:5601/app/kibana

http://localhost:5601/app/home#/tutorial_directory

开发工具`ctrl /` 跳转到官方文档

## 文档的基本CRUD与批量操作

mget 是通过文档ID列表得到文档信息。

msearch 是根据查询条件，搜索到相应文档。

## Elasticsearch基本概念

* Index索引
  * Type类型
  * Document文档

### 文档(Document)

* Elasticsearch 是面向文档的，文档是所有可搜索数据的最小单位

* 文档会 被序列化成JSON格式，保存在Elasticsearch 中

* 每个文档都有一个Unique ID

### 文档的元数据

* 元数据，用于标注文档的相关信息
  * _ index: 文档所属的索引名
  * _type: 文档所属的类型名
  * _id: 文档唯一ld
  * _source: 文档的原始Json数据
  * _all: 整合所有字段内容到该字段，已被废除
  * _version: 文档的版本信息
  * _score: 相关性打分

### 索引

* Index-索引是文档的容器，是一类文档的结合
  * Index体现了逻辑空间的概念:每个索引都有自己的Mapping定义，用于定义包含的文档的字段名和字段类型。
  * Shard体现了物理空间的概念:索引中的数据,分散在Shard上。
* 索引的Mapping与Settings
  * Mapping定义文档字段的类型
  * Setting定义不同的数据分布

### 索引的不同语意

* 名词:一个Elasticsearch 集群中,可以创建很多个不同的索引
* 动词:保存一个文档到Elasticsearch的过程也叫索引(indexing)
  * ES中，创建一个倒排索引的过程
* 名词:一个B树索引，一个倒排索引



## 倒排索引

## 分析器

倒排索引的核心组成

倒排索引包含两个部分
*  单词词典(Term Dictionary)，记录所有文档的单词，记录单词到倒排列表的关联关系
  * 单词词典一般比较大，可以通过B+树或哈希拉链法实现，以满足高性能的插入与查询
* 倒排列表(Posting List) -记录 了单词对应的文档结合，由倒排索引|项组成
  * 倒排索引项 (Posting)
  * 文档ID
  * 词频 TF-该单词在文档中出现的次数，用于相关性评分
  * 位置(Position) - 单词在文档中分词的位置。用于语句搜索(phrase query)
  * 偏移(Offset) -记录单词的开始结束位置，实现高亮显示
  
## 注意事项

1. 大版本更新， API会有向后不兼容的情况发生

2.大版本的升级，数据需要重建索引

## 问答

* mysql同步es有什么比较靠谱的中间件？

logstash的jdbc plugin

* 如果文档的id采用自定义id而不是系统自动生成，需要注意什么吗？

es的hash函数会确保id被均匀分配到不同的分片的。自增id一般不会有什么问题。但是如果你自己指定了routing参数，有可能会引起分配不均匀的情况发生。

* 跳页问题有没有好的解决方案呢?

跳页应该只能用from size做，避免页数太深即可。搜索引擎真的返回几千页，其实也没啥意义。

* _msearch与_search的查询语法是一样通用的吧？

语法通用

相比普通search，msearch可以通过一次网络请求，获得多条查询结果。所以，减少了网络开销，所以提升了性能。

