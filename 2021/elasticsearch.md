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


## 问答

* mysql同步es有什么比较靠谱的中间件？

logstash的jdbc plugin

* 如果文档的id采用自定义id而不是系统自动生成，需要注意什么吗？

es的hash函数会确保id被均匀分配到不同的分片的。自增id一般不会有什么问题。但是如果你自己指定了routing参数，有可能会引起分配不均匀的情况发生。


## 注意事项

1. 大版本更新， API会有向后不兼容的情况发生

2.大版本的升级，数据需要重建索引
