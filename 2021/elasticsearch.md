# Elasticsearch

## Elasticsearch 能做什么？

Elasticsearch 是一款非常强大的开源搜索及分析引擎。可以帮助你从海量数据中，快速找到相关的信息。Elasticsearch 不仅可以帮你找到相关的代码仓库，还可以帮助你实现代码级的搜索与高亮显示 ；当你在网上购物时，Elasticsearch 可以帮你推荐相关的商品；当你下班打车回家时，Elasticsearch 可以通过定位附近的乘客和司机，帮助平台优化调度。

除了搜索，结合 Kibana、Logstash、Beats，Elastic Stack 还被广泛运用在大数据近实时分析领域，包括日志分析、指标监控、信息安全等多个领域。它可以帮助你探索海量结构化、非结构化数据，按需创建可视化报表，对监控数据设置报警阈值。甚至通过使用机器学习技术，自动识别异常状况。


### 到底能够使用 Elasticsearch 做什么？

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
预防、检测、猎捕并应对

### 主要功能

* 海量数据的分户式存储以及集群管理
  * 服务与数据的高可用，水平扩展
* 近实时搜索，性能卓越
  * 结构化/全文/地理位置/自动完成
* 海量数据的近实时分析
  * 聚合功能
  

### 注意事项

1. 大版本更新， API会有向后不兼容的情况发生

2. 大版本的升级，数据需要重建索引

### 问答

* mysql同步es有什么比较靠谱的中间件？

logstash的jdbc plugin

* 如果文档的id采用自定义id而不是系统自动生成，需要注意什么吗？

es的hash函数会确保id被均匀分配到不同的分片的。自增id一般不会有什么问题。但是如果你自己指定了routing参数，有可能会引起分配不均匀的情况发生。

* 跳页问题有没有好的解决方案呢?

跳页应该只能用from size做，避免页数太深即可。搜索引擎真的返回几千页，其实也没啥意义。

* _msearch与_search的查询语法是一样通用的吧？

语法通用

相比普通search，msearch可以通过一次网络请求，获得多条查询结果。所以，减少了网络开销，所以提升了性能。



## Elastic Stack生态圈

![生态圈](/img/es生态圈.png)

### Logstash:数据处理管道

开源的服务器端数据处理管道，支持从不同来源采集数据，转换数据，并将数据发送到不同的存储库中

### Logstash特性

* 实时解析和转换数据
  * 从IP地址破译出地理坐标
  * 将PII数据匿名化，完全排除敏感字段
* 可扩展
  * 200多个插件(日志/数据库/Arcsigh/Netflow)
* 可靠性安全性
  * Logstash 会通过持久化队列来保证至少将运行中的事件送达一次
  * 数据传输加密
* 监控

### Kibana:可视化分析利器

* Kibana 名字的含义= Kiwifruit + Banana
* 数据可视化工具，帮助用户解开对数据的任何疑问
* 基于Logstash的工具，2013 年加入Elastic公司


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

### Elasticsearch的文件目录结构

|目录|配置文件|描述|
|:--:|:--:|:--:|
|bin||脚本文件，包括启动elasticsearch,安装插件。运行统计数据等|
|config|elasticsearch.yml|集群配置文件，user, role based相关配置|
|JDK||Java运行坏境|
|data|path.data|数据文件|
|lib||Java类库|
|logs|path.log |日志文件|
|modules||包含所有ES模块|
|plugins||包含所有已安装插件|

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

### 抽象与类比

|RDBMS|Elasticsearch|
|:--:|:--:|
|RDBMS|Elasticsearch|
|Table|Index(Type)|
|Row|Document|
|Column|Filed|
|Schema|Mapping|
|SQL|DSL|

### Master-eligible nodes和Master Node

* 每个节点启动后， 默认就是一个Master eligible 节点
  * 可以设置node.master: false禁止
* Master-eligible节点可以参加选主流程，成为Master节点
* 当第一个节点启动时候，它会将自己选举成Master节点
* 每个节点上都保存了集群的状态，只有Master节点才能修改集群的状态信息
  * 集群状态. (Cluster State)， 维护了一个集群中，必要的信息
    * 所有的节点信息
    * 所有的索引和其相关的Mapping与Setting 信息
    * 分片的路由信息
    
### Data Node & Coordinating Node

* Data Node 
  * 可以保存数据的节点， 叫做Data Node。负责保存分片数据。在数据扩展上起到了至关重要的作用
* Coordinating Node
  * 负责接受Client的请求，将请求分发到合适的节点，最终把结果汇集到一起
  * 每个节点默认都起到了Coordinating Node的职责

### 分片(Primary Shard & Replica Shard)

* 主分片，用以解决数据水平扩展的问题。通过主分片，可以将数据分布到集群内的所有节点之上
  * 一个分片是一个运行的Lucene的实例
  * 主分片数在索引创建时指定，后续不允许修改，除非Reindex
* 副本，用以解决数据高可用的问题。分片是主分片的拷贝
  * 副本分片数，可以动态题调整
  * 增加副本数，还可以在一定程度上提高服务的可用性(读取的吞吐)


## 文档的基本CRUD与批量操作

### Create一个文档

* 支持自动生成文档Id和指定文档ld两种方式
* 通过调用"post /users/_doc"
  * 系统会自动生成documentId
* 使用HTTP PUT user/_create/1 创建时，URI中显示指定_create， 此时如果该id的文档已经存在，操作失败

### Get一个文档

GET users/_doc/1

### Index文档

Index和Create不一样的地方:如果文档不存在，就索引新的文档。否则现有文档会被删除，新的文档被索引。版本信息+1

### Update文档

POST users/_update/1

### 批量读取

批量操作，可以减少网络连接所产生的开销，提高性能

mget 是通过文档ID列表得到文档信息。

msearch 是根据查询条件，搜索到相应文档。


## 倒排索引

* 正排索引-文档Id到文档内容和单词的关联
* 倒排索引-单词到文档Id的关系

### 倒排索引包含两个部分

* 单词词典(Term Dictionary)，记录所有文档的单词，记录单词到倒排列表的关联关系
  * 单词词典一般比较大，可以通过B+树或哈希拉链法实现，以满足高性能的插入与查询
* 倒排列表(Posting List) -记录 了单词对应的文档结合，由倒排索引|项组成
  * 倒排索引项 (Posting)
  * 文档ID
  * 词频 TF-该单词在文档中出现的次数，用于相关性评分
  * 位置(Position) - 单词在文档中分词的位置。用于语句搜索(phrase query)
  * 偏移(Offset) -记录单词的开始结束位置，实现高亮显示
  
* Elasticsearch的JSON文档中的每个字段，都有自己的倒排索引可以指定对某些字段不做索引
  * 优点:节省存储空间
  * 缺点:字段无法被搜索

### Elasticsearch的内置分词器
* Standard Analyzer 默认分词器，按词切分，小写处理
* Simple Analyzer 按照非字母切分(符号被过滤) ，小写处理
* Stop Analyzer 小写处理，停用词过滤(the， a，is)
* Whitespace Analyzer 按照空格切分，不转小写
* Keyword Analyzer 不分词，直接将输入当作输出
* Patter Analyzer 正则表达式，默认\W+ (非字符分隔)
* Language 提供了30多种常见语言的分词器
* Customer Analyzer 自定义分词器

### Analyzer由哪几，个部分组成?

Character Filter + Tokenizer + Token Filter


## Dynamic Mapping

* Mapping类似数据库中的schema的定义，作用如下
  * 定义索引中的字段的名称
  * 定义字段的数据类型，例如字符串，数字，布尔....
  * 字段，倒排索引的相关配置，(Analyzed or Not Analyzed,Analyzer)
* Mapping会把JSON文档映射成Lucene所需要的扁平格式
* 一个Mapping属于一个索引的Type
  * 每个文档都属于一个 Type
  * 一个Type有一个Mapping定义
  * 7.0开始，不需要在Mapping定义中指定type信息

### 什么是Dynamic Mapping
* 在写入文档时候， 如果索引不存在,会自动创建索引
* Dynamic Mapping的机制，使得我们无需手动定义Mappings。Elasticsearch会自动根据文档信息，推算出字段的类型
* 但是有时候会推算 的不对，例如地理位置信息
* 当类型如果设置不对时，会导致一些功能无法正常运行，例如Range查询

### 能否更改Mapping的字段类型

* 两种情况
  * 新增加字段Dynamic设为true时，一旦有新增字段的文档写入，Mapping也同时被更新Dynamic设为false, Mapping 不会被更新，新增字段的数据无法被索引，但是信息会出现在_source中Dynamic设置成Strict，文档写入失败
  * 对已有字段，一旦已经有数据写入，就不再支持修改字段定义Lucene实现的倒排索引，一但生成后，就不允许修改
  * 如果希望改变字段类型，必须Reindex API，重建索引
* 原因
  * 如果修改了字段的数据类型，会导致已被索引的属于无法被搜索
  * 但是如果是增加新的字段，就不会有这样的影响

### 自定义Mapping的一些建议

* 可以参考API手册，纯手写
* 为了减少输入的工作量，减少出错概率，可以依照以下步骤
  * 创建一个临时的index，写入一些样本数据
  * 通过访问Mapping API获得该临时文件的动态Mapping定义
  * 修改后用， 使用该配置创建你的索引
  * 删除临时索引

### 什么是Index Template

Index Templates -帮助你设定Mappings和Settings,并按照- -定的规则，自动匹配到新创建的索引之上
* 当一个索引被新创建时
  * 应用Elasticsearch默认的settings和mappings
  * 应用order数值低的Index Template中的设定
  * 应用order高的Index Template中的设定，之前的设定会被覆盖
  * 应用创建索引时，用户所指定的Settings和Mappings, 并覆盖之前模版中的设定

### 什么是Dynamic Template

保证推断类型正确

* 根据Elasticsearch识别的数据类型，结合字段名称，来动态设定字段类型
  * 所有 的字符串类型都设定成Keyword,或者关闭keyword字段
  * is开头的字段都设置成boolean
  * long开头的都设置成long类型


### 控制当前字段是否被索引

Index 控制当前字段是否被索引。默认为true。如果设置成false， 该字段不可被搜索

Index Options

* 四种不同级别的Index Options配置，可以控制倒排索引记录的内容
  * docs-记录doc id
  * freqs -记录doc id和term frequencies
  * positions -记录doc id / term frequencies / term position
  * offsets - doc id / term frequencies / term posistion / character offects
* Text类型默认记录postions，其他默认为docs
* 记录内容越多，占用存储空间越大

### Exact Values不需要被分词

## 字段的数据类型

* 简单类型
  * Text / Keyword
  *  Date
  * Integer / Floating
Boolean
  * IPv4 & IPv6
  * 复杂类型- 对象和嵌套对象
  * 对象类型/嵌套类型
* 特殊类型
  * geo_ point & geo_ shape / percolator

字段类型修改，需要重新reindex

## 查询
### 基于Term的查询

* Term的重要性
  * Term是表达语意的最小单位。搜索和利用统计语言模型进行自然语言处理都需要处理Term
* 特点
  * Term Level Query: Term Query / Range Query / Exists Query / Prefix Query /Wildcard Query
  * 在ES 中，Term查询，对输入不做分词。会将输入作为一个整体，在倒排索引中查找准确的词项，并且使用相关度算分公式为每个包含该词项的文档进行相关度算分-例如“Apple Store“
  * 可以通过Constant Score将查询转换成一个Filtering, 避免算分,并利用缓存，提高性能

### 基于全文的查询

* 基于全文本的查找
  * Match Query / Match Phrase Query / Query String Query
* 特点
  * 索引和搜索时都会进行分词， 查询字符串先传递到一个合适的分词器，然后生成一个供查询的词项列表
  * 查询时候，先会对输入的查询进行分词，然后每个词项逐个进行底层的查询，最终将结果进行合并。并为每个文档生成一个算分。例如查“Matrix reloaded”,会查到包括Matrix或者reload的所有结果。

### 结构化数据

* 结构化搜索(Structured search) 是指对结构化数据的搜索
  * 日期，布尔类型和数字都是结构化的
* 文本也可以是结构化的。
  * 如彩色笔可以有离散的颜色集合:红(red) 、 绿(green) 、 蓝(blue)
  * 一个博客可能被标记了标签，例如，分布式(distributed) 和搜索(search)
  * 电商网站上的商品都有UPCs (通用产品码Universal Product Codes) 或其他的唯一标识，它们都需要遵从严格规定的、结构化的格式。

### 在Elasticsearch中，有Query和Filter两种不同的Context

* Query Context:相关性算分
* Filter Context:不需要算分( Yes or No) ,可以利用Cache，获得 更好的性能

### 条件组合

### bool查询

|类型|说明|
|:--:|:--:|
|must|必须匹配。贡献算分|
|should|选择性匹配。贡献算分|
|must_not|Filter Context 查询字句，必须不能匹配|
|filter|Filter Context 必须匹配，但是不贡献算分|

如何解决结构化查询”包含而不是相等”的问题
增加count字段，使用bool 查询解决

### 单字符串多字段查询: Dis Max Query

* 算分过程
  * 查询 should语句中的两个查询
  * 加和两个查 询的评分
  * 乘以匹配语句的总数
  * 除以所有语句的总数

* 有一些情况下，同时匹配title和body字段的文档比只与一个字段匹配的文档的相关度更高
* 但disjunction max query查询只会简单地使用单个最佳匹配语句的评分。score 作为整体评分。怎么办?
* 通过Tie Breaker参数调整
  * 获得最佳匹配语句的评分_score
  * 将其他匹配语句的评分与tie_breaker 相乘
  * 对以上评分求和并规范化


### 单字符串多字段查询: Multi Match

三种场景

* 最佳字段(Best Fields)
  * 是默认类型，可以不⽤指定
  * 当字段之间相互竞争，又相互关联。例如title和body这样的字段。评分来自最匹配字段
* 多数字段 (Most Fields)
  * 处理英文内容时:一种常见的手段是，在主字段( English Analyzer), 抽取词干，加入同义词，以匹配更多的文档。相同的文本，加入子字段(Standard Analyzer),以提供更加精确的匹配。其他字段作为匹配文档提高相关度的信号。匹配字段越多则越好
* 混合字段(Cross Field)
  * 对于某些实体，例如人名，地址，图书信息。需要在多个字段中确定信息，单个字段只能作为整体的一部分。希望在任何这些列出的字段中找到尽可能多的词


### 跨字段搜索

* 无法使用Operator
* 可以用copy_to 解决，但是需要额外的存储空间
* 支持使用Operator
* 与copy_to 相比，其中一个优势就是它可以在搜索时为单个字段提升权重。

### 综合排序：Function Score Query 优化算分

* Function Score Query
  * 可以在查询结束后， 对每一个匹配的文档进行一系列的重新算分，根据新生成的分数进行排序。
  
* 提供了几种默认的计算分值的函数
 * Weight :为每一个文档设置一个简单而不被规范化的权重
 * Field Value Factor:使用该数值来修改_ score, 例如将“热度”和“点赞数”作为算分的参考因素
 * Random Score:为每一个用户使用一个不同的，随机算分结果
 * 衰减函数:以某个字段的值为标准，距离某个值越近，得分越高
 * Script Score:自定义脚本完全控制所需逻辑

## Suggesters搜索建议

* 现代的搜索引擎， 一般都会提供Suggest as you type的功能
* 帮助用户在输入搜索的过程中， 进行自动补全或者纠错。通过协助用户输入更加精准的关键词，提高后续搜索阶段文档匹配的程度
* 在google.上搜索，一开始会自动补全。当输入到一定长度,如因为单词拼写错误无法补全，就会开始提示相似的词或者句子


### 4种类别的Suggesters

原理:将输入的文本分解为Token,然后在索引的字典里查找相似的Term并返回

* Term Suggester
* Phrase Suggester
* Complete Suggester
* Context Suggester

###  Term Suggester

### Phrase Suggester

* Phrase Suggester在Term Suggester.上增加了一些额外的逻辑
* 一些参数
  * Suggest Mode : missing, popular, always
  * Max Errors: 最多可以拼错的Terms数
  * Confidence: 限制返回结果数，默认为1

* 几种 Suggestion Mode
  * Missing -如索引中已经存在，就不提供建议
  * Popular-推荐出现频率更加高的词
  * Always -无论是否存在，都提供建议

### Completion Suggester

* Completion：⾃动补全与基于上下⽂的提示

### Context Suggester

什么是Context Suggester
* Completion Suggester的扩展
  * 可以在搜索中加入更多的上下文信息，例如，输入"star"
  * 咖啡相关:建议"Starbucks"
  * 电影相关: "star wars"

实现Context Suggester
* 可以定义两种类型的Context
  * Category -任意的字符串
  * Geo -地理位置信息
* 实现Context Suggester的具体步骤
  * 定制一个 Mapping
  * 索引数据，并且为每个文档加入Context信息
  * 结合Context进行Suggestion查询


### 精准度和召回率

* 精准度
  * Completion > Phrase > Term
* 召回率
  * Term > Phrase > Completion
* 性能
  * Completion > Phrase > Term

## 分片

### Lucene Index

在Lucene中，单个倒排索引文件被称为Segment。Segment是自包含的，不可变更的。多个Segments汇总在一起，称为Lucene的Index，其对应的就是ES中的Shard

当有新文档写入时，会生成新Segment，查询时会同时查询所有Segments,并且对结果汇总。Lucene中有一个文件，用来记录所有Segments信息，叫做Commit Point

删除的文档信息，保存在“.del”文件中


### 什么是Refresh

* 将Index buffer写入Segment的过程叫Refresh。Refresh 不执行fsync操作
* Refresh频率:默认1秒发生一次，可通过index.refresh_interval 配置。Refresh 后，数据就可以被搜索到了。这也是为什么Elasticsearch被称为近实时搜索
* 如果系统有大量的数据写入，那就会产生很多的Segment
* Index Buffer被占满时，会触发Refresh, 默认值是JVM的10%

### 什么是Transaction Log

* Segment写入磁盘的过程相对耗时，借助文件系统缓存，Refresh 时，先将Segment写入缓存以开放查询

* 为了保证数据不会丢失。所以在Index文档时，同时写Transaction L og，高版本开始，Transaction Log默认落盘。每个分片有一个Transaction Log

* 在ES Refresh时，Index Buffer被清空,Transaction log不会清空

### 什么是Flush

* ES Flush & Lucene Commit
  * 调用Refresh, Index Buffer清空并且Refresh
  * 调用fsync,将缓存中的Segments写入磁盘.
  * 清空(删除) Transaction Log
  * 默认30分钟调用一次
  * TransactionLog满(默认512 MB)


### 分布式搜索的运行机制

* Easticsearch的搜索，会分两阶段进行

  * 第一阶段 Query
    * 用户发出搜索请求到ES节点。节点收到请求后，会以Coordinating节点的身份，在6个主副分片中随机选择3个分片，发送查询请求
    * 被选中的分片执行查询，进行排序。然后，每个分片都会返回From + Size个排序后的文档Id和排序值给Coordinating节点
  * 第二阶段 Fetch
    * Coordiating Node会将Query阶段，从从每个分片获取的排序后的文档Id列表, 重新进行排序。选取From到From + Size个文档的Id
    * 以multi get请求的方式，到相应的分片获取详细的文档数据
    
* Query-then- Fetch

## Update By Query & Reindex API

使用场景
* 一般在以下几种情况时，我们需要重建索引
  * 索引的 Mappings发生变更:字段类型更改，分词器及字典更新
  * 索引的Settings发生变更:索引的主分片数发生改变
  * 集群内， 集群间需要做数据迁移
* Elasticsearch的内置提供的API
  * Update By Query:在现有索引上重建
  * Reindex:在其他索引上重建索引
  
## 集群

### JVM设定

* 从ES6开始，只支持64位的JVM
  * 配置config / jvm. options
* 避免修改默认配置
  * 将内存Xms和Xmx设置成一样，避免heap resize 时引发停顿
  * Xmx设置不要超过物理内存的50%; 单个节点上，最大内存建议不要超过32 G内存
    * https://www.elastic.co/blog/a-heap-of-trouble
  * 生产环境，JVM必须使用Server模式
  * 关闭JVM Swapping
  
### 索引生命周期常见的阶段

* Hot: 索引还存在着大量的读写操作
* Warm:索引不存在写操作，还有被查询的需要
* Cold:数据不存在写操作，读操作也不多
* Delete:索引不再需要，可以被安全删除


## Logstash

ELT工具/数据搜集处理引擎。支持200多个插件
