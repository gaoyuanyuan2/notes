# Elasticsearch

## Elasticsearch 能做什么？

Elasticsearch 是一款非常强大的开源搜索及分析引擎。可以帮助你从海量数据中，快速找到相关的信息。Elasticsearch 不仅可以帮你找到相关的代码仓库，还可以帮助你实现代码级的搜索与高亮显示 ；当你在网上购物时，Elasticsearch 可以帮你推荐相关的商品；当你下班打车回家时，Elasticsearch 可以通过定位附近的乘客和司机，帮助平台优化调度。

除了搜索，结合 Kibana、Logstash、Beats，Elastic Stack 还被广泛运用在大数据近实时分析领域，包括日志分析、指标监控、信息安全等多个领域。它可以帮助你探索海量结构化、非结构化数据，按需创建可视化报表，对监控数据设置报警阈值。甚至通过使用机器学习技术，自动识别异常状况。


### 到底能够使用 Elasticsearch 做什么？

订单搜索，商品推荐，日志管理，安全监控，定位附件司机和乘客

日志搜集->格式化分析->全文检索->风险告警




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
  

### 版本

1. 大版本更新， API会有向后不兼容的情况发生

2. 大版本的升级，数据需要重建索引

新特性6.x

* Lucene 7.x
* 新功能
  * 跨集群复制(CCR) 
  * 索引生命周期管理，
  * SQL的支持
* 更友好的的升级及数据迁移
  * 在主要版本之间的迁移更为简化，体验升级
  * 全新的基于操作的数据复制框架，可加快恢复数据
* 性能优化
  * 有效存储稀疏字段的新方法，降低了存储成本
  * 在索引时进行排序，可加快排序的查询性能


新特性7.x
* Lucene8.0
* 重大改进-正式废除单个索引下多Type的支持
* 7.1开始，Security 功能免费使用
* ECK - Elasticseach Operator on Kubernetes
* 新功能
  * New Cluster coordination
  * Feature-Complete High Level REST Client 
  * Script Score Query
* 性能优化
  * 默认的Primary Shard数从5改为1， 避免Over Sharding
  * 性能优化，更快的Top K

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

* Kibana 名字的含义 = Kiwifruit + Banana
* 数据可视化工具，帮助用户解开对数据的任何疑问
* 基于Logstash的工具，2013 年加入Elastic公司

键盘命令
Ctrl/Cmd + I
自动缩进当前请求
Ctrl/Cmd + /
打开当前请求的文档
Ctrl + Space
打开自动完成（即使未键入）
Ctrl/Cmd + Enter
提交请求
Ctrl/Cmd + Up/Down
跳转至前一/后一请求开头或结尾。
Ctrl/Cmd + Alt + L
折叠/展开当前范围。
Ctrl/Cmd + Option + 0
折叠当前范围除外的所有范围。通过加按 Shift 键来展开。
Down arrow
将焦点切换到自动完成菜单。使用箭头进一步选择词
Enter/Tab
选择自动完成菜单中当前选定的词或最顶部的词
Esc
关闭自动完成菜单

## 安装

docker pull docker.elastic.co/elasticsearch/elasticsearch:7.10.2

docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.10.2

查看节点：
http://localhost:9200/_cat/nodes
http://localhost:9200/?pretty

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

* 文档会被序列化成JSON格式，保存在Elasticsearch中

* 每个文档都有一个Unique ID

### 文档的元数据

* 元数据，用于标注文档的相关信息
  * _index: 文档所属的索引名
  * _type: 文档所属的类型名
  * _id: 文档唯一Id
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



## 文档的基本CRUD与批量操作

### Create一个文档

* 支持自动生成文档Id和指定文档Id两种方式
* 通过调用"post /users/_doc"
  * 系统会自动生成documentId
* 使用HTTP PUT user/_create/1 创建时，URI中显示指定_create， 此时如果该id的文档已经存在，操作失败

### Get一个文档

GET users/_doc/1

### Index文档

Index和Create不一样的地方:如果文档不存在，就索引新的文档。否则现有文档会被删除，新的文档被索引。版本信息+1

### Update文档

POST users/_update/1

### 删除文档

DELETE my_index/_doc/1


### 批量读取

批量操作，可以减少网络连接所产生的开销，提高性能

mget 是通过文档ID列表得到文档信息。

msearch 是根据查询条件，搜索到相应文档。

### Bulk API 

* 支持在一次API调用中，对不同的索引进行操作
* 支持四种类型操作
  * Index
  * Create
  * Update
  * Delete
* 可以再URI中指定Index,也可以在请求的Payload中进行
* 操作中单条操作失败，并不会影响其他操作
* 返回结果包括了每一条操作执行的结果



## 倒排索引

* 正排索引-文档Id到文档内容和单词的关联
* 倒排索引-单词到文档Id的关系

### 倒排索引包含两个部分

* 单词词典(Term Dictionary)，记录所有文档的单词，记录单词到倒排列表的关联关系
  * 单词词典一般比较大，可以通过B+树或哈希拉链法实现，以满足高性能的插入与查询
* 倒排列表(Posting List) 记录了单词对应的文档结合，由倒排索引项组成
  * 倒排索引项 (Posting)
  * 文档ID
  * 词频 TF 该单词在文档中出现的次数，用于相关性评分
  * 位置(Position) 单词在文档中分词的位置。用于语句搜索(phrase query)
  * 偏移(Offset) 记录单词的开始结束位置，实现高亮显示
  
* Elasticsearch的JSON文档中的每个字段，都有自己的倒排索引可以指定对某些字段不做索引
  * 优点:节省存储空间
  * 缺点:字段无法被搜索

## Elasticsearch的内置分词器

* Standard Analyzer 默认分词器，按词切分，小写处理
* Simple Analyzer 按照非字母切分(符号被过滤) ，小写处理
* Stop Analyzer 小写处理，停用词过滤(the， a，is)
* Whitespace Analyzer 按照空格切分，不转小写
* Keyword Analyzer 不分词，直接将输入当作输出
* Patter Analyzer 正则表达式，默认\W+ (非字符分隔)
* Language 提供了30多种常见语言的分词器
* Customer Analyzer 自定义分词器

直接指定Analyzer进行测试

GET _analyze
{
  "analyzer": "standard",
  "text": "2 running Quick brown-foxes leap over lazy dogs in the summer evening."
}

指定索引的字段进行测试

POST books/_analyze
 "field":"title",
 "text":"Mastering Elasticseach"
}

自定义分词起进行测试

POST  /_analyze
{
    "tokenizer":"standard",
    "filter": ["lowercase"],
    "text":"Mastering Elasticseach"
}

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
  
### 字段的数据类型

* 简单类型
  * Text / Keyword
  * Date
  * Integer / Floating
  * Boolean
  * IPv4 & IPv6
* 复杂类型:对象和嵌套对象
  * 对象类型/嵌套类型
* 特殊类型
  * geo_point & geo_shape / percolator
  
字段类型修改，需要重新reindex

### 什么是Dynamic Mapping

* 在写入文档时候， 如果索引不存在,会自动创建索引
* Dynamic Mapping的机制，使得我们无需手动定义Mappings。Elasticsearch会自动根据文档信息，推算出字段的类型
* 但是有时候会推算 的不对，例如地理位置信息
* 当类型如果设置不对时，会导致一些功能无法正常运行，例如Range查询

* 查看 Mapping文件
  * GET mapping_test/_mapping

### 能否更改Mapping的字段类型

* 两种情况
  * 新增加字段Dynamic设为true时，一旦有新增字段的文档写入，Mapping也同时被更新Dynamic设为false, Mapping 不会被更新，新增字段的数据无法被索引，但是信息会出现在_source中Dynamic设置成Strict，文档写入失败
  * 对已有字段，一旦已经有数据写入，就不再支持修改字段定义Lucene实现的倒排索引，一但生成后，就不允许修改
  * 如果希望改变字段类型，必须Reindex API，重建索引
* 原因
  * 如果修改了字段的数据类型，会导致已被索引的属性无法被搜索
  * 但是如果是增加新的字段，就不会有这样的影响


* 当dynamic被设置成false时候， 存在新增字段的数据写入，该数据可以被索引,但是新增字段被丢弃。
* 当设置成Strict模式时候，数据写入直接出错。


Index 控制当前字段是否被索引。默认为true。如果设置成false, 该字段不可被搜索节省磁盘开销。


* 需要对Null值实现搜索
* 只有Keyword类型支持设定Null_Value

```json
{
 "lastName":{
        "type": "text",
        "copy_to": "fullName"
         },
 "mobile" : {
          "type" : "keyword",
          "null_value": "NULL"
        }
}
```

###  Excat values V.S Full Text

* Exact Value:包括数字/日期/具体一个字符串(例如"Apple Store" )
  * Elasticsearch 中的keyword，不需要分词处理。
* 全文本， 非结构化的文本数据
  * Elasticsearch 中的text


### 自定义Mapping的一些建议

* 可以参考API手册，纯手写
* 为了减少输入的工作量，减少出错概率，可以依照以下步骤
  * 创建一个临时的index，写入一些样本数据
  * 通过访问Mapping API获得该临时文件的动态Mapping定义
  * 修改后用，使用该配置创建你的索引
  * 删除临时索引

### 什么是Index Template

Index Templates 帮助你设定Mappings和Settings,并按照一定的规则，自动匹配到新创建的索引之上
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





## 查询
### 基于Term的查询

* Term的重要性
  * Term是表达语意的最小单位。搜索和利用统计语言模型进行自然语言处理都需要处理Term
* 特点
  * Term Level Query: Term Query / Range Query / Exists Query / Prefix Query /Wildcard Query
  * 在ES 中，Term查询，对输入不做分词。会将输入作为一个整体，在倒排索引中查找准确的词项，并且使用相关度算分公式为每个包含该词项的文档进行相关度算分 例如"Apple Store"
  * 可以通过Constant Score将查询转换成一个Filtering, 避免算分,并利用缓存，提高性能

### 基于全文的查询

* 基于全文本的查找
  * Match Query / Match Phrase Query / Query String Query
* 特点
  * 索引和搜索时都会进行分词， 查询字符串先传递到一个合适的分词器，然后生成一个供查询的词项列表
  * 查询时候，先会对输入的查询进行分词，然后每个词项逐个进行底层的查询，最终将结果进行合并。并为每个文档生成一个算分。例如查"Matrix reloaded",会查到包括Matrix或者reload的所有结果。

即便是对Keyword进行Term查询，同样会进行算分

可以将查询转为Filtering, 取消相关性算分的环节，以提升性能

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

  
### bool查询

|类型|说明|
|:--:|:--:|
|must|必须匹配。贡献算分|
|should|选择性匹配。贡献算分|
|must_not|Filter Context 查询字句，必须不能匹配|
|filter|Filter Context 必须匹配，但是不贡献算分|

如何解决结构化查询”包含而不是相等”的问题
增加count字段，使用bool 查询解决

## 单字符串多字段查询: Dis Max Query

* 算分过程
  * 查询 should语句中的两个查询
  * 加和两个查询的评分
  * 乘以匹配语句的总数
  * 除以所有语句的总数

* 有一些情况下，同时匹配title和body字段的文档比只与一个字段匹配的文档的相关度更高
* 但disjunction max query查询只会简单地使用单个最佳匹配语句的评分。

score 作为整体评分。怎么办?

* 通过Tie Breaker参数调整
  * 获得最佳匹配语句的评分_score
  * 将其他匹配语句的评分与tie_breaker相乘
  * 对以上评分求和并规范化


### 单字符串多字段查询: Multi Match

三种场景

* 最佳字段(Best Fields)
  * 是默认类型，可以不指定
  * 当字段之间相互竞争，又相互关联。例如title和body这样的字段。评分来自最匹配字段
* 多数字段 (Most Fields)
  * 处理英文内容时:一种常见的手段是，在主字段( English Analyzer), 抽取词干，加入同义词，以匹配更多的文档。相同的文本，加入子字段(Standard Analyzer),以提供更加精确的匹配。其他字段作为匹配文档提高相关度的信号。匹配字段越多则越好
  * 累计叠加
* 混合字段(Cross Field)
  * 对于某些实体，例如人名，地址，图书信息。需要在多个字段中确定信息，单个字段只能作为整体的一部分。希望在任何这些列出的字段中找到尽可能多的词


### 跨字段搜索

* 无法使用Operator
* 可以用copy_to 解决，但是需要额外的存储空间
* 支持使用Operator
* 与copy_to 相比，其中一个优势就是它可以在搜索时为单个字段提升权重。

## 自然语言与查询Recall

* 当处理人类自然语言时，有些情况，尽管搜索和原文不完全匹配，但是希望搜到一些内容
  * Quick brown fox和fast brown fox / Jumping fox和Jumped foxes
* 一些可采取的优化
  * 归一化词元: 清除变音符号，如`rôle`的时候也会匹配role
  * 抽取词根: 清除单复数和时态的差异
  * 包含同义词
  * 拼写错误: 拼写错误，或者同音异形词


### 混合多语言的挑战

* 一些具体的多语言场景
  * 不同的索引使用不同的语言/同一个索引中，不同的字段使用不同的语言/一个文档的一个字段内混合不同的语言
* 混合语言存在的一些挑战
  * 词干提取: 以色列文档，包含了希伯来语，阿拉伯语，俄语和英文
  * 不正确的文档频率:英文为主的文章中，德文算分高(稀有)
  * 需要判断用户搜索时使用的语言，语言识别(Compact Language Detector)

### 分词的挑战

* 英文分词: You're 分成一个还是多个? Half-baked
* 中文分词
  * 分词标准:哈工大标准中，姓和名分开。HanLP 是在一起的。具体情况需制定不同的标准
  * 歧义(组合型歧义， 交集型歧义，真歧义)
    * 中华人民共和国/美国会通过对台售武法案/上海仁和服装厂

* 统计语言模型，1990年前后，清华大学电子工程系郭进博士
  * 解决了二义性问题，将中文分词的错误率降低了一个数量级。概率问题，动态规划+利用维特比算法快速找到最佳分词

* 基于统计的机器学习算法
  * 这类 目前常用的是算法是HMM、CRF、SVM、深度学习等算法。比如HanLP.分词工具是基于CRF算法以CRF为例，基本思路是对汉字进行标注训练，不仅考虑了词语出现的频率，还考虑上下文,具备较好的学习能力，因此其对歧义词和未登录词的识别都具有良好的效果。
  * 随着深度学习的兴起， 也出现了基于神经网络的分词器，有人尝试使用双向LSTM+CRF实现分词器,其本质上是序列标注，据报道其分词器字符准确率可高达97.5%


常见的分词器都是使用机器学习算法和词典相结合，一方面能够提高分词准确率，另一方面能够改善领域适应性。

### 一些中文分诃器

* HanLP 面向生产环境的自然语言处理工具包
* IK 分词器
* Pinyin
* icu

安装：./elasticsearch-plugin inStall https://github.com/KennFalcon/elasticsearch-analysis-hanlp/releases/download/v7.1.0/elasticsearch-analysis-hanlp-7.1.0.zip

## Search Template 解耦程序&搜索DSL


## 算分

### Elasticsearch有三种控制相关度分数的方法:

* boost
* boosting
* function_score

* boosting
  * positive 必须匹配的条件
  * negative 匹配该条件的文档要减低相关度分数, 最终分数为匹配positive条件的分数 * negative_boost
  * negative_boost 降低匹配negative条件相关度分数的系数, 取值范围为0~1.0

* Boosting Relevance
  * Boosting是控制相关度的一种手段
  * 索引，字段或查询子条件

* 参数boost的含义
  * 当boost> 1时，打分的相关度相对性提升
  * 当0< boost< 1时，打分的权重相对性降低
  * 当boost<0时，贡献负分


### 综合排序：Function Score Query 优化算分

* Function Score Query
  * 可以在查询结束后， 对每一个匹配的文档进行一系列的重新算分，根据新生成的分数进行排序。
  
* 提供了几种默认的计算分值的函数
 * Weight :为每一个文档设置一个简单而不被规范化的权重
 * Field Value Factor:使用该数值来修改_score, 例如将“热度”和“点赞数”作为算分的参考因素
 * Random Score:为每一个用户使用一个不同的，随机算分结果
 * Decay Functions 衰减函数:以某个字段的值为标准，距离某个值越近，得分越高
 * Script Score:自定义脚本完全控制所需逻辑

### modifier

新的算分=老的算分*log(1+投票数)


|修饰符|意义|
|:--:|:--:|
|none| 不要对字段值应用任何乘数|
|log |取字段值的常用对数。因为此函数将返回负值，并且如果将其用于0到1之间的值，则会导致错误，因此建议改用它log1p。|
|log1p |将1加到字段值并取对数|
|log2p |在字段值上加2并取公共对数|
|ln| 取字段值的自然对数。因为此函数将返回负值，并且如果将其用于0到1之间的值，则会导致错误，因此建议改用它ln1p。|
|ln1p |将1加到栏位值并取自然对数|
|ln2p| 将2加到栏位值并取自然对数|
|square |对字段值求平方（乘以它本身）|
|sqrt| 取字段值的平方根|

### Factor

新的算分=老的算分* log(1 + factor *投票数)

### function_score

* score_mode 存在多个函数时, 计算最终函数分数的方式.
  * multiply 多个函数分数相乘, 默认.
  * sum 多个函数分数相加.
  * avg 取平均值.
  * first 匹配条件的第一个函数分数.
  * max 取最大值.
  * min 取最小值.
* Boost Mode
  * Multiply: 算分与函数值的乘积
  * Sum: 算分与函数的和
  * Min / Max: 算分与函数取最小/最大值
  * Replace:使用函数值取代算分
* Max Boost 可以将算分控制在一个最大值
* min_score 最小综合分数, 最终综合分数小于min_score的文档将会被过滤掉.
* boost 设置一个基础分数

### 一致性随机函数

* 使用场景:网站的广告需要提高展现率
* 具体需求:让每个用户能看到不同的随机排名，但是也希望同一个用户访问时，结果的相对顺序，保持一致(Consistently Random)


## Index Alias实现零停机运维

## Suggesters搜索建议

* 现代的搜索引擎， 一般都会提供Suggest as you type的功能
* 帮助用户在输入搜索的过程中， 进行自动补全或者纠错。通过协助用户输入更加精准的关键词，提高后续搜索阶段文档匹配的程度
* 在google上搜索，一开始会自动补全。当输入到一定长度,如因为单词拼写错误无法补全，就会开始提示相似的词或者句子


### 4种类别的Suggesters

原理:将输入的文本分解为Token,然后在索引的字典里查找相似的Term并返回

* Term Suggester
* Phrase Suggester
* Complete Suggester
* Context Suggester

###  Term Suggester

* Suggester 就是一种特殊类型的搜索。”text” 里是调用时候提供的文本，通常来自于用户界面上用户输入的内容
* 用户输入的 “lucen”是一个错误的拼写
* 会到指定的字段“body”上搜索，当无法搜索到结果时(missing),返回建议的词

* 几种 Suggestion Mode
  * Missing 如索引中已经存在，就不提供建议
  * Popular 推荐出现频率更加高的词
  * Always 无论是否存在，都提供建议
  
### Phrase Suggester

* Phrase Suggester在Term Suggester.上增加了一些额外的逻辑
* 一些参数
  * Suggest Mode : missing, popular, always
  * Max Errors: 最多可以拼错的Terms数
  * Confidence: 限制返回结果数，默认为1



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
  * Category 任意的字符串
  * Geo 地理位置信息
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

## 节点

### Coordinating Node

* 处理请求的节点， 叫Coordinating Node
  * 路由请求到正确的节点，例如创建索引的请求，需要路由到Master节点
* 所有 节点默认都是Coordinating Node
* 通过将其他类型设置 成False,使其成为Dedicated Coordinating Node

### Cerebro 可视化节点管理工具

docker run --name cerebro -d -p 9100:9000 lmenezes/cerebro:0.8.4

### Data Node

* 可以保存 数据的节点，叫做Data Node
  * 节点启动后，默认就是数据节点。可以设置node.data: false禁止
* Data Node的职责
  * 保存分片数据。在数据扩展上起到了至关重要的作用(由Master Node决定如何把分片分发到数据节点上)
* 通过增加数据节点
  * 可以解决数据水平扩展和解决数据单点问题

### Master Node

* Master Node的职责
  * 处理创建，删除索引等请求/决定分片被分配到哪个节点/负责索引的创建与删除
  * 维护并且更新Cluster State
* Master Node的最佳实践
  * Master节点非常重要，在部署上需要考虑解决单点的问题
  * 为一个集群设置多个Master节点/每个节点只承担Master的单一角色

### Master Eligible Nodes & 选主流程

* 一个集群， 支持配置多个Master Eligible 节点。这些节点可以在必要时(如Master节点出现故障，网络故障时)参与选主流程，成为Master节点
* 每个节点启动后，默认就是-个Master eligible 节点
  * 可以设置node.master: false禁止
* 当集群内第一个Master eligible节点启动时候，它会将自己选举成Master节点

### 集群状态

* 集群状态信息(Cluster State)，维护了一个集群中，必要的信息
  * 所有的节点信息
  * 所有的索引和其相关的Mapping与Setting信息
  * 分片的路由信息
* 在每个节 点上都保存了集群的状态信息
* 但是， 只有Master节点才能修改集群的状态信息，并负责同步给其他节点
  * 因为，任意节点都能修改信息会导致Cluster State信息的不一致

###  Master Eligible Nodes & 选主的过程

* 互相Ping对方，Node Id低的会成为被选举的节点
* 其他节点会加入集群，但是不承担Master节点的角色。一旦发现被选中的主节点丢失,就会选举出新的Master节点

###  如何避免脑裂问题

* 限定一个选举条件，设置quorum(仲裁)， 只有在Master eligible 节点数大于quorum时，才能进行选举
  * Quorum= (master 节点总数/2) + 1
  * 当3个master eligible 时，设置discovery.zen.minimum master_ nodes 为2，即可避免脑裂
* 从7.0开始，无需这个配置)
  * 移除minimum_master_nodes参数，让Elasticsearch自己选择可以形成仲裁的节点。
  * 典型的主节点选举现在只需要很短的时间就可以完成。集群的伸缩变得更安全、更容易，并且可能造成丢失数据的系统配置选项更少了。
  * 节点更清楚地记录它们的状态，有助于诊断为什么它们不能加入集群或为什么无法选举出主节点


## 文档存储在分片

* 文档会存储在具体的某个主分片和副本分片上: 例如文档1，会存储在PO和RO分片上
* 文档到分片的映射算法
  * 确保文档能均匀分布在所用分片上，充分利用硬件资源，避免部分机器空闲，部分机器繁忙
  * 潜在的算法
    * 随机/ Round Robin。当查询文档1，分片数很多，需要多次查询才可能查到文档1
    * 维护文档到分片的映射关系，当文档数据量大的时候，维护成本高
    * 实时计算，通过文档1，自动算出，需要去那个分片，上获取文档

## 分片

### 分片(Primary Shard & Replica Shard)

* 主分片，用以解决数据水平扩展的问题。通过主分片，可以将数据分布到集群内的所有节点之上
  * 一个分片是一个运行的Lucene的实例
  * 主分片数在索引创建时指定，后续不允许修改，除非Reindex
* 副本，用以解决数据高可用的问题。分片是主分片的拷贝
  * 副本分片数，可以动态题调整
  * 增加副本数，还可以在一定程度上提高服务的可用性(读取的吞吐)


* 对于生产环境中分片的设定，需要提前做好容量规划
  * 分片数设置过小
    * 导致后续无法增加节点实现水品扩展
    * 单个分片的数据量太大，导致数据重新分配耗时
* 分片数设置过大，7.0开始，默认主分片设置成1， 解决了over-sharding的问题
    * 影响搜索结果的相关性打分，影响统计结果的准确性
    * 单个节点上过多的分片，会导致资源浪费，同时也会影响性能

查看集群的健康状况

GET_ cluster/health

* Green 主分片与副本都正常分配
* Yellow 主分片全部正常分配，有副本分片未能正常分配
* Red 有主分片未能分配
  * 例如，当服务器的磁盘容量超过85%时,去创建了一个新的索引
  
GET_ cat/nodes

GET_ cat/shards

### 倒排索引不可变性

* 倒排索引采用Immutable Design, 一旦生成，不可更改
* 不可变性，带来了的好处如下:
  * 无需考虑并发写文件的问题，避免了锁机制带来的性能问题
  * 一旦读入内核的文件系统缓存，便留在哪里。只要文件系统存有足够的空间，大部分请求就会直接请求内存，不会命中磁盘，提升了很大的性能
  * 缓存容 易生成和维护/数据可以被压缩
* 不可变更性,带来了的挑战:如果需要让一个新的文档可以被搜索，需要重建整个索引。

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
  
### Merge
* Segment 很多，需要被定期被合并
  * 减少Segments /删除已经删除的文档
* ES和Lucene会自动进行Merge操作
  * POST my_index/_forcemerge


## 分布式搜索的运行机制

### ElasticSearch的搜索，会分两阶段进行

* 第一阶段 Query
  * 用户发出搜索请求到ES节点。节点收到请求后，会以Coordinating节点的身份，在6个主副分片中随机选择3个分片，发送查询请求
  * 被选中的分片执行查询，进行排序。然后，每个分片都会返回From + Size个排序后的文档Id和排序值给Coordinating节点
* 第二阶段 Fetch
  * Coordinating Node会将Query阶段，从从每个分片获取的排序后的文档Id列表, 重新进行排序。选取From到From + Size个文档的Id
  * 以multi get请求的方式，到相应的分片获取详细的文档数据
* Query-then-Fetch

### Query Then Fetch潜在的问题

* 性能问题
  * 每个分片，上需要查的文档个数= from + size
  * 最终协调节 点需要处理: number_of_shard * ( from+size )
  * 深度分页
* 相关性算分
  * 每个分片都基于自己的分片上的数据进行相关度计算。这会导致打分偏离的情况，特别是数据量很少时。相关性算分在分片之间是相互独立。当文档总数很少的情况下，如果主分片大于1，主分片数越多，相关性算分会越不准

### 解决算分不准的方法
* 数据量不大的时候， 可以将主分片数设置为1
  * 当数据量足够大时候， 只要保证文档均匀分散在各个分片上，结果一般就不会出现偏差
* 使用 DFS Query Then Fetch
  * 搜索的URL 中指定参数"_search?search_type=dfs_query_then_fetch"
  * 到每个分片把各分片的词频和文档频率进行搜集，然后完整的进行一次相关性算分，耗费更加多的CPU和内存，执行性能低下，一般不建议使用


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


## 排序

### 排序的过程

* 排序 是针对字段原始内容进行的。倒排索引无法发挥作用
* 需要用到正排索引。通过文档Id和字段快速得到字段原始内容
* Elasticsearch 有两种实现方法
  * FieldData
    * 索引速度快，不占用额外的磁盘空间
    * 文档过多时，动态创建开销大，占用过多JVM Heap
    * 搜索时候动态创建
  * Doc Values (列式存储， 对Text类型无效)
    * 降低索引速度，占用额外磁盘空间 
    * 避免大量内存占用
    * 索引时，和倒排索引一起创建


### 关闭Doc Values

* 默认启用，可以通过Mapping设置关闭
  * 增加索引的速度/减少磁盘空间
* 如果重新打开，需要重建索引
* 什么时候需要关闭
  * 明确不需要做排序及聚合分析


## 分页

### 分布式系统中深度分页的问题

* ES天生就是分布式的。查询信息，但是数据分别保存在多个分片，多台机器上，ES天生就需要满足排序的需要(按照相关性算分)
* 当一个查询: From= 990，Size=10
  * 会在每个分片，上先都获取1000个文档。然后，通过Coordinating Node聚合所有结果。最后再通过排序选取前1000个文档
  * 页数越深，占用内存越多。为了避免深度分页带来的内存开销。ES有一个设定，默认限定到10000个文档

### Search After避免深度分页的问题

* 避免深度分页的性能问题，可以实时获取下一页文档信息
  * 不支持指定页数(From)
  * 只能往下翻
* 第一步搜索需要指定sort,并且保证值是唯一的(可以通过加入_id保证唯一性)
* 然后使用上一次，最后一个文档的sort值进行查询

### Search After是如何解决深度分页的问题

* 假定Size是10
* 当查询990 - 1000
* 通过唯一排序值定位，将每次要处理的文档数都控制在10


### Scroll API

* 创建一个快照，有新的数据写入以后，无法被查到
* 每次查询后，输入上一次的Scroll Id


### 不同的搜索类型和使用场景

* Regular 需要实时获取顶部的部分文档。例如查询最新的订单
* Scroll 需要全部文档，例如导出全部数据
* Pagination From和Size如果需要深度分页，则选用Search After


### 并发控制的必要性

* 两个Web程序同时更新某个文档，如果缺乏有效的并发，会导致更改的数据丢失
* 悲观并发控制
  * 假定有变更冲突的可能。会对资源加锁，防止冲突。例如数据库行锁
* 乐观并发控制
  * 假定冲突是不会发生的，不会阻塞正在尝试的操作。如果数据在读写中被修改，更新将会失败。应用程序决定如何解决冲突，例如重试更新，使用新的数据，或者将错误报告给用户
  * ES 采用的是乐观并发控制

### ES的乐观并发控制

* ES中的文档是不可变更的。如果你更新一个文档，会将就文档标记为删除，同时增加一个全新的文档。同时文档的version字段加1
* 内部版本控制
  * If_seq_no + If_primary_term
* 使用外部版本(使用其他数据库作为主要数据存储)
  * version + version_type=external

## Bucket & Metric Aggregation

Metric 一些系列的统计方法
Bucket 一组满足条件的文档


### Metric Aggregation

* 单值分析：只输出一个分析结果
  * min, max, avg, sum
  * Cardinality (类似 distinct Count)
* 多值分析：输出多个分析结果
  * stats, extended stats
  * percentile, percentile rank
  * top hits (排在前面的示例)

### Terms Aggregation

* 字段需要打开fielddata,才能进行Terms Aggregation
  * Keyword 默认支持fielddata
  * Text需要在Mapping中enable。 会按照分词后的结果进行分
  
### Range & Histogram聚合

* 按照数字的范围，进行分桶
* 在Range Aggregation中，可以自定义Key

### Pipeline

* 管道的概念: 支持对聚合分析的结果，再次进行聚合分析
* Pipeline 的分析结果会输出到原结果中，根据位置的不同，分为两类
  * Sibling -结果和现有分析结果同级
    * Max，min， Avg & Sum Bucket
    * Stats， Extended Status Bucket
    * Percentiles Bucket
  * Parent -结果内嵌到现有的聚合分析结果之中
    * Derivative (求导)
    * cumulative Sum (累计求和)
    * Moving Function (滑动窗口)


### 聚合的作用范围

* ES聚合分析的默认作用范围是query的查询结果集
* 同时ES还支持以下方式改变聚合的作用范围
  * Filter
  * Post Filter
  * Global
  
### 排序

* 指定order,按照count和key进行排序
  * 默认情况，按照count降序排序
  * 指定size，就能返回相应的桶

### 如何解决Terms不准的问题:提升shard_size 的参数

* Terms聚合分析不准的原因，数据分散在多个分片上，Coordinating Node无法获取数据全貌
* 方案1:当数据量不大时，设置PrimaryShard为1;实现准确性
* 方案2:在分布式数据上，设置shard_size 参数，提高精确度
  * 原理:每次从Shard上额外多获取数据，提升准确率


## 关系型数据库的范式化设计

* 范式化设计(Normalization)的主要目标是减少不必要的更新
* 副作用:一个完全范式化设计的数据库会经常面临“查询缓慢”的问题
  * 数据库越范式化，就需要Join越多的表
* 范式化节省了存储空间，但是存储空间却越来越便宜
* 范式化简化了更新,但是数据“读”取操作可能更多

### 反范式化设计

* 数据“Flattening”,不使用关联关系，而是在文档中保存冗余的数据拷贝
* 优点:无需处理Joins操作,工数据读取性能好
  * Elasticsearch通过压缩_source 字段，减少磁盘空间的开销
*  缺点:不适合在数据频繁修改的场景
  * 一条数据(用户名) 的改动，可能会引起很多数据的更新

### Elasticsearch并不擅长处理关联关系。我们一般采用以下四种方法处理关联

* 对象类型
* 嵌套对象(Nested Object)
* 父子关联关系(Parent/Child)
* 应用端关联

### 为什么会搜到不需要的结果?

* 存储时，内部对象的边界并没有考虑在内，JSON格式被处理成扁平式键值对的结构
* 当对多个字段进行查询时，导致了意外的搜索结果
* 可以用Nested Data Type解决这个问题

### 什么是Nested Data Type

* Nested数据类型:允许对象数组中的对象被独立索引
* 使用nested和properties关键字，将所有actors 索引到多个分隔的文档
* 在内部,Nested文档会被保存在两个Lucene文档中，在查询时做Join处理

## Parent / Child

* 对象和Nested对象的局限性
  * 每次更新，需要重新索引整个对象(包括根对象和嵌套对象)
* ES提供了类似关系型数据库中Join的实现。使用Join数据类型实现，可以通过维护Parent/Child的关系，从而分离两个对象
  * 父文档和子文档是两个独立的文档
  * 更新父文档无需重新索引子文档。 子文档被添加，更新或者删除也不会影响到父文档和其他的子文档

### 嵌套对象v.S父子文档

|比较项|Nested Object|Parent / Child|
|:--:|:--:|:--:|
|优点|文档存储在一起，读取性能高|父子文档可以独立更新|
|缺点|更新嵌套的子文档时，需要更新整个文档|需要额外的内存维护关系。读取性能相对差|
|适用场景|子文档偶尔更新，以查询为主|子文档更新频繁|

## UpdateByQuery&ReindexAPI

### 使用场景

* 一般在以下几种情况时，我们需要重建索引
  * 索引的Mappings发生变更:字段类型更改，分词器及字典更新
  * 索引的Settings发生变更:索引的主分片数发生改变
  * 集群内，集群间需要做数据迁移
* Elasticsearch 的内置提供的API
  * Update By Query:在现有索引上重建
  * Reindex:在其他索引上重建索引

###  Reindex API

* Reindex API支持把文档从一个索引拷贝到另外一个索引
* 使用Reindex API的于些场景
  * 修改索引的主分片数
  * 改变字段的Mapping中的字段类型
  * 集群内数据迁移/跨集群的数据迁移

## Ingest Node

* Elasticsearch 5.0后，引入的一种新的节点类型。默认配置下，每个节点都是Ingest Node
  * 具有预处理数据的能力，可拦截Index或Bulk API的请求
  * 对数据进行转换，并重新返回给Index或BulkAPI
* 无需Logstash,就可以进行数据的预处理，例如
  * 为某个字 段设置默认值;重命名某个字段的字段名;对字段值进行Split 操作
  * 支持设置Painless脚本，对数据进行更加复杂的加工

### 一些内置Processors

[内置Processors](https://www.elastic.co/guide/en/elasticsearch/reference/7.10/ingest-processors.html)


* Split Processor (例: 将给定字段值分成一个数组)
* Remove / Rename Processor (例: 移除一个重命名字段)
* Append (例: 为商品增加一个新的标签)
* Convert (例:将商品价格, 从字符串转换成float类型)
* Date / JSON (例:日期格式转换，字符串转JSON对象)
* Date Index Name Processor (例: 将通过该处理器的文档，分配到指定时间格式的索引中)

### Ingest Node V.S Logstash
|比较项|Logstash|Ingest Node|
|:--:|:--:|:--:|
|数据输入与输出|支持从不同的数据源读取并写入不同的数据源|支持从ES REST API获取数据并且写入Elasticsearch|
|数据缓冲|实现了简单的数据队列，支持重写|不支持缓冲|
|数据处理|支持大量的插件，也支持定制开发|内置的插件，可以开发Plugin 进行扩展(Plugin 更新需要重启)|
| 配置和使用 |增加一定的架构复杂度|无需额外部署 | 

### Painless简介

* Painless Script具备以下特性
  * 高性能/安全
  * 支持显示类型或者动态定义类型
  
### Painless的用途

* 可以对文档字段进行加工处理
  * 更新或删除字段，处理数据聚合操作
  * Script Field:对返回的字段提前进行计算
  * Function Score:对文档的算分进行处理
* 在 Ingest Pipeline中执行脚本
* 在 Reindex API，Update By Query时，对数据进行处理

### 数据建模(Data modeling)

数据建模:功能需求+性能需求.

* 实体属性
* 实体之间的关系
* 搜索相关的配置


* 索引模版
  * 分片数量
* 索引Mapping
  * 字段配置
  * 关系处理

* 字段类型
* 是否要搜索及分词
* 是否要聚合及排序
* 是否要额外的存储

### 字段类型: Text v.s Keyword

* Text
  * 用于全文本字段， 文本会被Analyzer分词
  * 默认不支持聚合分析 及排序。需要设置`fielddata` 为true
* Keyword
  * 用于 id,枚举及不需要分词的文本。例如电话号码，email地址， 手机号码，邮政编码,性别等
  * 适用于 Filter (精确匹配)， Sorting 和Aggregations
* 设置多字段类型
  * 默认会为文本类型设置成 text,并且设置一个keyword的子字段
  * 在处理人类语言时， 通过增加“英文”，“拼音”和“标准”分词器，提高搜索结构
  
### 字段类型:结构化数据

* 数值类型
  * 尽量选择贴近的类型。 例如可以用byte，就不要用long
* 枚举类型
  * 设置为keyword。即便是数字，也应该设置成keyword,获取更加好的性能
* 其他
  * 日期/布尔/地理信息


### 检索

* 如不需要检索，排序和聚合分析
  * Enable 设置成false
* 如不需要检索 
  * Index 设置成false
* 对需要检索的字段，可以通过如下配置，设定存储粒度
  * Index options / Norms :不需要归一化数据时，可以关闭


### 聚合及排序

* 如不需要检索，排序和聚合分析
  * Enable 设置成false
* 如不需要排序或者聚合分析功能
  * Doc_values / `fielddata`设置成false
* 更新频繁，聚合查询频繁的keyword类型的字段
  * 推荐将eager_global_ordinals 设置为true

### 额外的存储

* 是否需要专门存储当前字段数据
  * Store 设置成true，可以存储该字段的原始内容
  * 一般结合_source 的enabled为false时候使用
* Disable_source: 节约磁盘;适用于指标型数据
  * 一般建议先考虑增加压缩比
  * 无法看到_source字段, 无法做ReIndex，无法做Update


### 解决字段过大引发的性能问题

* 返回结果不包含_source 字段
* 对于需要显示的信息，可以在在查询中指定"stored_fields"
* 禁止_source 字段后，还是支持使用highlights
* API，高亮显示content 中匹配的相关信息

### Mapping字段的相关设置

[Mapping字段的相关设置](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-params.html)

* Enabled 设置成false,仅做存储，不支持搜索和聚合分析(数据保存在_source中)
* Index 是否构倒排索引。设置成false, 无法被搜索，但还是支持aggregation, 并出现在. source中
* Norms 如果字段用来过滤和聚合分析，可以关闭，节约存储
* Doc values 是否启用doc_values,用于排序和聚合分析
* Field data 如果要对text类型启用排序和聚合分析，fielddata 需要设置成true
* Store 默认不存储，数据默认存储在_source
* Coerce 默认开启，是否开启数据类型的自动转换(例如，字符串转数字)
* Multifields 多字段特性
* Dynamic true/false/strict 控制Mapping的自动更新

### 一些相关的API

* Index Template & Dynamic Template
  * 根据索引的名字匹配不同的 Mappings和Settings
  * 可以在一个Mapping上动态的设定字段类型
* Index Alias
  * 无需停机， 无需修改程序，即可进行修改
* Update By Query & Reindex

### 如何处理关联关系

* 优先考虑Denormalization
* 当数据包含多数值对象(多个演员)同时有查询需求
* 关联文档更新非常频繁时


### 避免过多字段


* 一个文档中，最好避免大量的字段
  * 过多的字段数不容易维护
  * Mapping 信息保存在Cluster State中，数据量过大，对集群性能会有影响(Cluster State信息需要和所有的节点同步)
  * 删除或者修改数据需要reindex
* 默认最大字段数是1000，可以设置index.mapping.total_fields.limit 限定最大字段数。
* 什么原因会导致文档中有成百上千的字段?

### Dynamic v.S Strict

* Dynamic (生产环境中，尽量不要打开Dynamic)
  * true 未知字段会被自动加入
  * false 新字段不会被索引。但是会保存在_source
  * strict 新增字段不会被索引，文档写入失败
* Strict
  * 可以控制到字段级别

解决方案: Nested Object & Key Value

* 可以减少字段数量，解决Cluster State中保存过多Meta信息的问题，但是
  * 导致查询语句复杂度增加
  * Nested对象，不利于在Kibana中实现可视化分析

### 避免正则查询

* 正则，通配符查询，前缀查询属于Term查询，但是性能不够好
* 特别是将通配符放在开头，会导致性能的灾难

解决方案:将字符串转换为对象


### 避免空值引起的聚合不准


### 为索引的Mapping加入Meta信息

* Mappings设置非常重要，需要从两个维度进行考虑
  * 功能: 搜索,聚合,排序
  * 性能: 存储的开销;内存的开销;搜索的性能
* Mappings设置是一个迭代的过程
  * 加入新的字段很容易(必要时需要update_by_query)
  * 更新删除字段不允许(需要Reindex重建数据)
  * 最好能对Mappings加入Meta信息，更好的进行版本管理
  * 可以考虑将Mapping文件上传git进行管理


## 集群身份认证与用户鉴权

* 身份认证
  * 鉴定用户是否合法
* 用户鉴权
  * 指定那个用户可以访问哪个索引
* 传输加密
* 日志审计

### Authentication -身份认证

* 认证体系的几种类型
  * 提供用户名和密码
  * 提供秘钥或Kerberos票据
* Realms: X-Pack中的认证服务
  * 内置Realms (免费)
    * File / Native (用户名密码保存在Elasticsearch)
  * 外部Realms (收 费)

### RBAC 用户鉴权

什么是RBAC: Role Based Access Control,定义一个角色，并分配一组权限。权限包括索引级，字段级，集群级的不同的操作。然后通过将角色分配给用户，使得用户拥有这些权限

* User
* Role
* Permission
* Privilege
  * Cluster Privileges 集群级别
    * all / monitor / manager / manage_index / manage_index_template / manage_rollup
  * Indices Privileges 索引级别
    * all / create / create_index / delete / delete_index / index / manage / read /write view_index_metadata

### 集群内部安全通信

* 加密数据避免数据抓包，敏感信息泄漏
* 验证身份一避免Impostor Node
  * Data / Cluster State

### 集群与外部间的安全通信

配置Elasticsearch for HTTPS

## 常见的集群部署方式

### 节点参数配置

一个节点在默认情况会下同时扮演: master eligible, data node和ingest node

|节点类型|配置参数|默认值|
|:--:|:--:|:--:|
|master eligible|node.master|true|
|data|node.data|true|
|ingest|node.ingest|true|
|coordinating only|无|设置上面三个参数全部为false|
|machine learning|node.ml|true (需要enable x-pack)|

* 单一职责的节点
  * 一个节点只承担一个角色


### 单一角色:职责分离的好处

* Dedicated master eligible nodes:负责集群状态(cluster state)的管理
  * 使用低配置的CPU，RAM和磁盘
* Dedicated data nodes:负责数据存储及处理客户端请求
  * 使用高配置的CPU, RAM和磁盘
* Dedicated ingest nodes:负责数据处理
  * 使用高配置CPU;中等配置的RAM;低配置的磁盘

### Dedicate Coordinating Only Node (Client Node)

* 配置:将Master，Data， Ingest都配置成False
  * Medium/High CUP; Medium/High RAM; Low Disk
* 生产环境中，建议为一些大的集群配置Coordinating Only Nodes
  * 扮演 LoadBalancer。降低Master和Data Nodes的负载
  * 负责搜索结果的Gather/Reduce
  * 有时候无法预知客户端会发送怎么样的请求
    * 大量占用内存的结合操作，一个深度聚合可能会引发0OM


### Dedicate Master Node

* 从高可用 &避免脑裂的角度出发
  * 一般在生产环境中配置3台
  * 一个集群只有1台活跃的主节点
    * 负责分片管理，索引创建，集群管理等操作
* 如果和数据节点或者Coordinate节点混合部署
  * 数据节点相对有比较大的内存占用
  * Coordinate节点有时候可能会有开销很高的查询，导致OOM
  * 这些都有可能影响Master节点，导致集群的不稳定
  
  
### 基本部署:增加节点，水平扩展

* 当磁盘容量无法满足需求时，可以增加数据节点;磁盘读写压力大时， 增加数据节点


### 水平扩展: Coordinating Only Node

* 当系统中有大量的复杂查询及聚合时候，增加Coordinating 节点，增加查询的性能

### 读写分离

### 将Kibana部署在Coordinating节点

### 异地多活的部署

* 集群处在三个数据中心;数据三写; GTM分发读请求

### Hot & Warm架构与Shard Filtering

* Hot & Warm Architecture
  * 数据通常不会有Update操作;适用于Time based索引数据(生命周期管理)，同时数据量比较大的场景。
  * 引入Warm节点，低配置大容量的机器存放老数据，以降低部署成本
* 两类数据节点,不同的硬件配置
  * Hot节点(通常使用SSD) :索引有不断有新文档写入。通常使用SSD
  * Warm节点(通常使用HDD) :索引不存在新数据的写入;同时也不存在大量的数据查询

### Rack Awareness

* ES的节点可能分布在不同的机架当一个机架断电，可能会同时丢失几个节点
* 如果一个索引相同的主分片和副本分片，同时在这个机架上，就有可能导致数据的丢失
* 通过Rack Awareness的机制，就可以尽可能避免将同一个索引的主副分片同时分配在一个机架的节点上


### 单个分片

* 7.0开始，新创建一个索引时，默认只有一个主分片
  * 单个分片，查询算分，聚合不准的问题都可以得以避免
* 单个索引，单个分片时候，集群无法实现水平扩展
  * 即使增加新的节点， 无法实现水平扩展

### 两个分片

* 集群增加一个节点后，Elasticsearch 会自动进行分片的移动，也叫Shard Rebalancing


### 如何设计分片数

* 当分片数 > 节点数时
  * 一旦集群中有新的数据节点加入，分片就可以自动进行分配
  * 分片在重新分配时，系统不会有downtime
* 多分片的好处:一个索引如果分布在不同的节点，多个节点可以并行执行
  * 查询可以并行执行
  * 数据写入可以分散到多个机器

### 分片过多所带来的副作用

* Shard 是Elasticsearch实现集群水平扩展的最小单位
* 过多设置分片数会带来一些潜在的问题
  * 每个分片是一个 Lucene的索引，会使用机器的资源。过多的分片会导致额外的性能开销
    * Lucene Indices / File descriptors / RAM / CPU
    * 每次搜索的请求， 需要从每个分片上获取数据
    * 分片的Meta信息由Master节点维护。过多会增加管理的负担。经验是控制分片总数在10W 以内

### 如何确定主分片数

* 从存储的物理角度看
  * 日志类应用，单个分片不要大于50 GB
  * 搜索类应用，单个分片不要超过20 GB
* 为什么要控制分片存储大小
  * 提高Update的性能
  * Merge时，减少所需的资源
  * 丢失节点后，具备更快的恢复速度/便于分片在集群内Rebalancing

### 如何确定副本分片数

* 副本是主分片的拷贝
  * 提高系统可用性: 相应查询请求，防止数据丢失
  * 需要占用和主分片一样的资源
* 对性能的影响
  * 副本会降低数据的索引速度:有几份副本就会有几倍的CPU资源消耗在索引上
  * 会减缓对主分片的查询压力，但是会消耗同样的内存资源
    * 如果机器资源充分，提高副本数，可以提高整体的查询QPS

### 调整分片总数设定，避免分配不均衡

* ES的分片策略会尽量保证节点上的分片数大致相同
  * 扩容的新节点没有数据，导致新索引集中在新的节点
  * 热点数据过于集中，可能会产生新能问题

### 容量规划

* 一个集群总共需要多少个节点? 一个索引需要设置几个分片?
  * 规划上需要保持一定的余量，当负载出现波动，节点出现丢失时，还能正常运行
* 做容量规划时，一些需要考虑的因素
  * 机器的软硬件配置
  * 单条文档的尺寸 /文档的总数据量/索引的总数据量(Time base数据保留的时间) /副本分片数
  * 文档是如何写入的(Bulk的尺寸)
  * 文档的复杂度， 文档是如何进行读取的(怎么样的查询和聚合)

### 评估业务的性能需求

* 数据吞吐及性能需求
  * 数据写入的吞吐量，每秒要求写入多少数据? 
  * 查询的吞吐量?
  * 单条查询可接受的最大返回时间?
* 了解你的数据
  * 数据的格式和数据的 Mapping
  * 实际的查询和聚合时长的是什么样的

#### 常见用例

* 搜索:固定大小的数据集
  * 搜索的数据集增长相对比较缓慢
* 日志:基于时间序列的数据
  * 使用ES存放日志与性能指标。数据每天不断写入，增长速度较快
  * 结合 Warm Node做数据的老化处理

### 硬件配置

* 选择合理的硬件，数据节点尽可能使用SSD
* 搜索等性能要求高的场景，建议SSD
  * 按照1 :10的比例配置内存和硬盘
* 日志类和查询并发低的场景，可以考虑使用机械硬盘存储
  * 按照1: 50的比例配置内存和硬盘
* 单节点数据建议控制在2 TB以内，最大不建议超过5 TB
* JVM配置机器内存的一半，JVM内存配置不建议超过32 G

### 部署方式

* 按需选择合理的部署方式
* 如果需要考虑可靠性高可用，建议部署3台dedicated的Master节点
* 如果有复杂的查询和聚合，建议设置Coordinating节点

###  固定大小的数据集

* 一些案例:唱片信息库/产品信息
* 一些特性
  * 被搜索的数据集很大，但是增长相对比较慢(不会有大量的写入)。更关心搜索和聚合的读取性能
  * 数据的重要性与时间范围无关。关注的是搜索的相关度
* 估算索引的的数据量，然后确定分片的大小
  * 单个分片的数据不要超过20 GB
  * 可以通过增加副本分片，提高查询的吞吐量

### 拆分索引 

* 如果业务上有大量的查询是基于一个字段进行Filter, 该字段又是一个数量有限的枚举值
  * 例如订单所在的地区
* 如果在单个索引有大量的数据，可以考虑将索引拆分成多个索引
  * 查询性能可以得到提高
  * 如果要对多个索引进行查询， 还是可以在查询中指定多个索引得以实现
* 如果业务.上有大量的查询是基于一个字段进行Filter, 该字段数值并不固定
  * 可以启用 Routing功能，按照filter 字段的值分布到集群中不同的shard,降低查询时相关的shard高CPU利用率

### 基于时间序列的数据

* 相关的用案
  * 日志/指标/安全相关的Events
  * 舆情分析
* 一些特性
  * 每条数据都有时间戳;文档基本不会被更新(日志和指标数据)
  * 用户更多的会查询近期的数据;对旧的数据查询相对较少
  * 对数据的写入性能要求比较高

### 创建基于时间序列的索引

* 创建time-based索引
  * 在索引的名 字中增加时间信息
  * 按照 每天/每周/每月的方式进行划分
* 带来的好处
  * 更加合理的组织索引， 例如随着时间推移，便于对索引做的老化处理
    * 利用Hot & Warm Architecture
    * 备份和删除以及删除的效率高。( Delete By Query执行速度慢，底层不也不会立刻释放空间，而Merge时资源)

### 写入时间序列的数据

* 基于Date Math的方式
  * 容易使用
  * 如果时间发生变化，需要重新部署代码
* 基于Index Alias
  * Time-based索引
    * 创建索引，每天/每周/每月
    * 在索引的名字中增加时间信息

### 集群扩容

* 增加 Coordinating / Ingest Node
  * 解决CPU和内存开销的问题
* 增加数据节点
  * 解决存储的容量的问题
  * 为避免分片分布不均的问题，要提前监控磁盘空间，提前清理数据或增加节点(70%)

## 集群

### ECE Elastic Cloud Enterprise

[ECE](https://www.elastic.co/cn/products/ece)

* 通过单个控制台，管理多个集群
  * 支持不同方式的集群部署(支持各类部署)/跨数据中心/部署AntiAffinity
  * 统一监控所有集群的状态
  * 图形化操作
    * 增加删除节点
    * 升级集群/滚动更新/自动数据备份

### 基于Kubernetes的方案

* 基于容器技术，使用Operator模式进行编排管理
* 配置，管理监控多个集群
* 支持Hot & Warm
* 数据快照和恢复

### 构建自己的管理系统

* 基于虚拟机的编排管理方式
  * Puppet Infrastructure (Puppet / Elasticsearch Puppet Module / Foreman)
  * WorkFlow based Provision & Management
* 基于Kubernetes的容器化编排管理方式
  * 基于 Operator模式
  * Kubernetes - Customer Resource Definition

### Development vs. Production Mode

* 从ES 5开始，支持Development和Production 两种运行模式
  * 开发模式
  * 生产模式

### Bootstrap Checks

* 一个集群在Production Mode时，启动时必须通过所有Bootstrap检测，否则会启动失败
* Bootstrap Checks可以分为两类: JVM & Linux Checks。Linux Checks只针对Linux系统

### JVM设定

* 从ES6开始，只支持64位的JVM
  * 配置config / jvm.options
* 避免修改默认配置
  * 将内存Xms和Xmx设置成一样,避免heap resize时引发停顿
  * Xmx 设置不要超过物理内存的50%;单个节点上，最大内存建议不要超过32 G内存
    * 小于32G会采取内存对象指针压缩的机制性能更好
    * https://www.elastic.co/blog/a-heap-of-trouble
  * 生产环境，JVM必须使用Server模式关闭JVM Swapping

### 集群的API设定

* 静态设置和动态设定
  * 静态配置文件尽量简洁:按照文档设置所有相关系统参数。elasticsearch.yml 配置文件中尽量只写必备参数
* 其他的设置项可以通过API动态进行设定。动态设定分transient和persistent两种，都会覆盖elasticsearch.yaml中的设置
  * Transient 在集群重启后会丢失
  * Persistent 在集群中重启后不会丢失

* 优先级
  * 1 Transient Settings
  * 2 Persistent Settings
  * 3 Command-line settings
  * 4 Config file settings

[系统设置](https://www.elastic.co/guide/en/elasticsearch/reference/7.11/system-config.html)

Disable Swapping，Increase file descriptor，虚拟内存，number of thread

### 最佳实践:网络

* 单个集群不要跨数据中心进行 部署(不要使用WAN)节点之间的hops越少越好
* 如果有多块网卡， 最好将transport和http绑定到不同的网卡，并设置不同的防火墙Rules
* 按需为Coordinating Node或Ingest Node配置负载均衡


### 最佳实践:内存设定计算实例

* 内存大小要根据Node需要存储的数据来进行估算
  * 搜索类的比例建议: 1:16
  * 日志类: 1:48- 1:96之间
* 总数据量1T，设置一个副本 = 2T总数据量
  * 如果搜索类的项目，每个节点31 * 16 = 496 G,加上预留空间。所以每个节点最多400 G数据，至少需要5个数据节点
  * 如果是日志类项目，每个节点31*50 = 1550 GB, 2个数据节点即可

### 最佳实践:存储

* 推荐使用SSD，使用本地存储(Local Disk)。避免使用SAN NFS / AWS / Azure filesystem
* 可以在本地指定多个“path.data”,以支持使用多块磁盘
* ES本身提供了很好的HA机制;无需使用RAID 1/5/10
* 可以在Warm节点上使用Spinning Disk,但是需要关闭Concurrent Merges
  * Index.merge.scheduler.max_thread_count: 1
* Trim你的SSD
  * https://www.elastic.co/blog/is-your-elasticsearch-trimmed

### 最佳实践:服务器硬件

* 建议使用中等 配置的机器，不建议使用过于强劲的硬件配置
  * Medium machine over large machine
* 不建议在一台服务器上运行多个节点

### 集群设置: Throttles限流

* 为Relocation和Recovery设置限流，避免过多任务对集群产生性能影响
  * Recovery
* Cluster.routing.allocation.node_concurrent_recoveries: 2 
  * Relocation
* Cluster.routing.allocation.cluster_concurrent_rebalance: 2

### 集群设置:关闭Dynamic Indexes

#### 可以考虑关闭动态索引创建的功能


```
PUT_cluster/settings
{
    "persistent": {
      "action.auto_create_index":false
    }
}
```

#### 或者通过模版设置白名单

```
PUT_cluster/settings
{
    "persistent": {
      "action.auto_create_index" :"logstash-*,kibana*"
    }
}
```

### 集群安全设定

* 为Elasticsearch和Kibana配置安全功能
  * 打开Authentication & Authorization
  * 实现索引和和字段级的安全控制
* 节点间通信加密
* Enable HTTPS
* Audit logs


### Elasticsearch Stats相关的API

* Elasticsearch提供了多个监控相关的API
  * Node Stats:_nodes/stats
  * Cluster Stats:_cluster/stats
  * Index Stats: index_name/_stats


### Elasticsearch Task API

* 查看Task相关的API
  * Pending Cluster Tasks API: GET_cluster/ pending_tasks
  * Task Management API :GET _tasks (可以用来Cancel 一个Task) 
* 监控Thread Pools
  * GET _nodes/thread_pool
  * GET _nodes/stats/thread_pool
  * GET _cat/thread_pool?v
  * GET _nodes/hot_threads

### The Index & Query Slow Log

* 支持将分片上，Search 和Fetch阶段的慢查询写入文件
* 支持为Query和Fetch分别定义阈值索引级的动态设置
* 可以按需设置,或者通过Index Template统一设定
* Slog log文件通过log4j2.properties 配置

```
# Node Stats：
GET _nodes/stats

#Cluster Stats:
GET _cluster/stats

#Index Stats:
GET kibana_sample_data_ecommerce/_stats

#Pending Cluster Tasks API:
GET _cluster/pending_tasks

# 查看所有的 tasks，也支持 cancel task
GET _tasks


GET _nodes/thread_pool
GET _nodes/stats/thread_pool
GET _cat/thread_pool?v
GET _nodes/hot_threads
GET _nodes/stats/thread_pool


# 设置 Index Slowlogs
# the first 1000 characters of the doc's source will be logged
PUT my_index/_settings
{
  "index.indexing.slowlog":{
    "threshold.index":{
      "warn":"10s",
      "info": "4s",
      "debug":"2s",
      "trace":"0s"
    },
    "level":"trace",
    "source":1000  
  }
}

# 设置查询
DELETE my_index
//"0" logs all queries
PUT my_index/
{
  "settings": {
    "index.search.slowlog.threshold": {
      "query.warn": "10s",
      "query.info": "3s",
      "query.debug": "2s",
      "query.trace": "0s",
      "fetch.warn": "1s",
      "fetch.info": "600ms",
      "fetch.debug": "400ms",
      "fetch.trace": "0s"
    }
  }
}

GET my_index


```


### 如何创建监控Dashboard

* 开发Elasticsearch plugin,通过读取相关的监控API，将数据发送到ES，或者TSDB
* 使用Metricbeats 搜集相关指标
* 使用 Kibana或Graffna创建Dashboard
* 可以开发 Elasticsearch Exporter, 通过Prometheus监控Elasticsearch集群

### 集群运维所面临的挑战

* 用户集群数量多，业务场景差异大
* 使用与配置不当，优化不够
  * 如何让用户更加高效和正确的使用ES
  * 如何让用户更全面的了解自己的集群的使用状况
* 发现问题滞后，需要防患于未然
  * 需要“有迹可循”，做到“有则改之，无则加勉”
  * Elastic 有提供Support Diagnostics Tool https://github.com/elastic/support-diagnostics


### 为什么要诊断集群的潜在问题

* 防患于未然，避免集群奔溃
  * Master 节点/数据节点宕机，负载过高，导致节点失联
  * 副本丢失，导致数据可靠性受损
  * 集群压力过大，数据写入失败
* 提升集群性能
  * 数据节点负载不均衡(避免单节点瓶颈) / 优化分片，segment
  * 规范操作方式 (利用别名/避免Dynamic Mapping引发过多字段，对索引的合理性进行管控)

### eBay Diagnostic Tool

### 阿里云 EYOU智能运维工具

### 集群健康度

* 分片健康
  * 红:至少有一个主分片没有分配
  * 黄:至少有一个副本没有分配
  * 绿:主副本分片全部正常分配
* 索引健康:最差的分片的状态
* 集群健康:最差的索引的状态

### Health相关的API 

```
# 检查集群状态，查看是否有节点丢失，有多少分片无法分配
GET /_cluster/health/

# 查看索引级别,找到红色的索引
GET /_cluster/health?level=indices


#查看索引的分片
GET /_cluster/health?level=shards

# Explain 变红的原因
GET /_cluster/allocation/explain

# 单个索引的健康状态(查看具体的索引)
GET /_cluster/health/my_index

```


### 症状:集群变红

* 分析:通过Allocation Explain API发现创建索引失败，因为无法找到标记了相应box type的节点
* 解决:删除索引，集群变绿。重新创建索引，并且指定正确的routing box type,索引创建成功。集群保持绿色状态


### 症状:集群变黄

* 分析:通过Allocation Explain API发现无法在相同的节点上创建副本
* 解决:将索引的副本数设置为0,或者通过增加节点解决


### 分片没有被分配的一些原因

* INDEX_CREATE:创建索引导致。在索引的全部分片分配完成之前，会有短暂的Red,不一定代表有问题
* CLUSTER_RECOVER:集群重启阶段，会有这个问题
* INDEX_REOPEN: Open 一个之前Close的索引
* DANGLING_INDEX_IMPORTED:一个节点离开集群期间，有索引被删除。这个节点重新返回时，会导致Dangling的问题
    
https://www.elastic.co/guide/en/elasticsearch/reference/7.11/cat-shards.html

### 集群Red & Yellow问题的总结

* Red & Yellow是集群运维中常见的问题

* 除了集群故障，一些创建，增加副本等操作,都会导致集群短暂的Red和Yellow，所以监控和报警时需要设置一定的延时

* 通过检查节点数，使用ES提供的相关API,找到真正的原因

* 可以指定Move或者Reallocate 分片


## 提高写入性能的方法

* 写性能优化的目标:增大写吞吐量(Events Per Second)， 越高越好
* 客户端:多线程，批量写
  * 可以通过性能测试，确定最佳文档数量
  * 多线程:需要观察是否有HTTP 429返回，实现Retry以及线程数量的自动调节
* 服务器端:单个性能问题，往往是多个因素造成的。需要先分解问题，在单个节点上进行调整并
  * 且结合测试，尽可能压榨硬件资源，以达到最高吞吐量
  * 使用更好的硬件。观察CPU/IO Block
  * 线程切换/堆栈状况

### 服务器端优化写入性能的一些手段

* 降低IO操作
  * 使用ES 自动生成的文档Id/一些相关的ES配置，如Refresh Interval
* 降低CPU和存储开销
  * 减少不必要分分词/避免不需要的doc_values/文档的字段尽量保证相同的顺序，可以提高文档的压缩率
* 尽可能做到写入和分片的均衡负载，实现水平扩展
  * Shard Filtering / Write Load Balancer
* 调整 Bulk线程池和队列

### 优化写入性能

* ES 的默认设置，已经综合考虑了数据可靠性，搜索的实时性质，写入速度，一般不要盲目修改
* 切优化，都要基于高质量的数据建模

### 关闭无关的功能

* 只需要聚合不需要搜索，Index 设置成false
* 不需要算分，Norms 设置成false
* 不要对字符串使用默认的dynamic mapping。字段数量过多，会对性能产生比较大的影响
* Index_options控制在创建倒排索引时，哪些内容会被添加到倒排索引中。优化这些设置，一定程度，可以节约CPU
* 关闭_source，减少IO操作;(适合指标型数据)
  * 无法做ReIndex，无法做Update

### 针对性能的取舍

* 如果需要追求极致的写入速度，可以牺牲数据可靠性及搜索实时性以换取性能
  * 牺牲可靠性:将副本分片设置为0，写入完毕再调整回去
  * 牺牲搜索实时性:增加Refresh Interval 的时间
  * 牺牲可靠性:修改Translog的配置

### 数据写入的过程

* Refresh
  * 将文档先保存在Index buffer中，以refresh_interval 为间隔时间，定期清空buffer,生成segment,借助文件系统缓存的特性，先将segment放在文件系统缓存中，并开放查询，以提升搜索的实时性
* Translog
  * Segment 没有写入磁盘，即便发生了当机，重启后，数据也能恢复，默认配置是每次请求都会落盘
* Flush
  * 删除旧的translog文件
  * 生成Segment并写入磁盘/更新commit point并写入磁盘。ES 自动完成，可优化点不多

### Refresh Interval

* 降低Refresh的频率
  * 增加refresh_interval 的数值。默认为1s，如果设置成-1，会禁止自动refresh 
    * 避免过于频繁的refresh,而生成过多的segment文件
    * 但是会降低搜索的实时性
  * 增大静态配置参数indices.memory.index_buffer_size
    * 默认是10%，会导致自动触发refresh

### Translog

* 降低写磁盘的频率，但是会降低容灾能力
  * Index.translog.durability: 默认是request, 每个请求都落盘。设置成async, 异步写入
  * Index.translog.sync_interval 设置为60s, 每分钟执行一次
  * Index.translog.flush_threshod_size: 默认512 mb， 可以适当调大。 当translog超过该值，会触发flush

### 分片设定

* 副本在写入时设为0，完成后再增加
* 合理设置主分片数， 确保均匀分配在所有数据节点上
  * Index.routing.allocation.total_share_per_node: 限定每个索引在每个节点上可分配的主分片数
  * 5个节点的集群。索引有 5个主分片，1个副本，应该如何设置?
    * (5+5) / 5=2
    * 生产环境中要适 当调大这个数字,避免有节点下线时，分片无法正常迁移

### Bulk，线程池和队列大小

* 客户端
  * 单个bulk请求体的数据量不要太大，官方建议大约5-15mb
  * 写入端的bulk请求超时需要足够长，建议60s以上
  * 写入端尽量将数据轮询打到不同节点。
* 服务器端
  * 索引创建属于计算密集型任务，应该使用固定大小的线程池来配置。来不及处理的放入队列，线程数应该配置成CPU核心数+1，避免过多的上下文切换
  * 队列大小可以适当增加，不要过大，否则占用的内存会成为GC的负担.


* 30秒一次Refresh
* 控制分片，避免数据热点
* 降低translog落盘
* 避免不必要的字段索引。必要时可以通过update by query索引必要的字段

```
PUT myindex
{
  "settings": {
    "index": {
      "refresh_interval": "30s",
      "number_of_shards": "2"
    },
    "routing": {
      "allocation": {
        "total_shards_per_node": "3"
      }
    },
    "translog": {
      "sync_interval": "30s",
      "durability": "async"
    },
    "number_of_replicas": 0
  },
  "mappings": {
    "dynamic": false,
    "properties": {}
  }
}
```


## 提升进群读性能

### 尽量Denormalize数据

* Elasticsearch ! =关系型数据库
* 尽可 能Denormalize数据，从而获取最佳的性能
  * 使用Nested类型的数据。查询速度会慢几倍
  * 使用Parent / Child关系。查询速度会慢几百倍


### 数据建模

* 尽量将数据先行计算， 然后保存到Elasticsearch中。尽量避免查询时的Script计算
* 尽量使用 Filter Context,利用缓存机制，减少不必要的算分
* 结合 profile, explain API分析慢查询的问题，持续优化数据模型
  * 严禁使用*开头通配符Terms查询

* 避免查询时脚本
  * 可以在Index文档时，使用Ingest Pipeline， 计算并写入某个字段
  
  
* 使用Query Context

```
GET blogs/_search
{
  "query": {
    "bool": {
      "must": [
        {"match": {"title": "elasticsearch"}},
        {
          "range": {
            "publish_date": {
              "gte": 2017,
              "lte": 2019
            }
          }
        }
      ]
    }
  }
}

# filter利用了缓存，性能更高
GET blogs/_search
{
  "query": {
    "bool": {
      "must": [
        {"match": {"title": "elasticsearch"}},
        "filter"{
          "range": {
            "publish_date": {
              "gte": 2017,
              "lte": 2019
            }
          }
        }
      ]
    }
  }
}
```

### 聚合文档消耗内存

* 聚合查询会消耗内存，特别是针对很大的数据集进行聚合运算
  * 如果可以控制聚合的数量,就能减少内存的开销
* 当需要使用不同的Query Scope,，可以使用Filter Bucket

### 通配符开始的正则表达

* 通配符开头的正则，性能非常糟糕,需避免使用

### 优化分片

* 避免Over Sharing
  * 一个查询需要访问每一个分片，分片过多，会导致不必要的查询开销
* 结合应用场景，控制单个分片的尺寸
  * Search: 20GB
  * Logging: 40GB
* Force-merge Read-only索引
  * 使用基于时间序列的索引，将只读的索引进行force merge, 减少segment数量

## 压力测试

* 压力测试的目的
  * 容量规划/性能优化/版本间性能比较/性能问题诊断
  * 确定系统稳定性，考察系统功能极限和隐患
* 压力测试的方法与步骤
  * 测试计划(确定测试场景和测试数据集)
  * 脚本开发
  * 测试环境搭建(不同的软硬件配置) & 运行测试分析比较结果

## 测试目标&测试数据

* 测试目标
  * 测试集群的读写性能/做集群容量规划
  * 对ES配置参数进行修改，评估优化效果
  * 修改 Mapping和Setting，对数据建模进行优化，并测试评估性能改进
  * 测试ES新版本，结合实际场景和老版本进行比较，评估是否进行升级
* 测试数据
  * 数据量/数据分布

### 测试脚本

* ES 本身提供了REST API，所以，可以通过很多传统的性能测试工具
  * Load Runner (商业软件，支持录制+重放+ DSL)
  * JMeter ( Apache开源，Record & Play)
  * Gatling (开源，支持写Scala代码+ DSL)
* 专门为Elasticsearch设计的工具
  * ES Pref & Elasticsearch-stress-test
  * Elastic Rally

### Lucene Index原理回顾

* 在Lucene中，单个倒排索引文件被称为Segment。Segment 是自包含的，不可变更的。多个Segments汇总在一起，称为Lucene 的Index，其对应的就是ES中的Shard 
* 当有新文档写入时，并且执行Refresh,就会会生成一个新Segment。Lucene 中有一个文件，用来记录所有Segments信息，叫做Commit Point。查询时会同时查询所有Segments，并且对结果汇总。
* 删除的文档信息，保存在“.del”文件中，查询后会进行过滤。
* Segment会定期Merge，合并成一个， 同时删除已删除文档

### Merge优化

* ES和Lucene会自动进行Merge操作
* Merge 操作相对比较重，需要优化，降低对系统的影响
* 优化点一: 降低分段产生的数量/频率工
  * 可以将 Refresh Interval 调整到分钟级别/ indices.memory.index_buffer_size (默认是10%)
  * 尽量避免文档的更新操作

### Force Merge

* 当Index不再有写入操作的时候，建议对其进行force merge，
  * 提升查询速度/减少内存开销
* 最终分成几个segments比较合适?
  * 越少越好，最好可以force merge成1个，但是，Force Merge会占用大量的网络，IO和CPU
  * 如果不能在业务高峰期之前做完，就需要考虑增大最终的分段数
    * Shard 的大小/Index.merge.policy.max_merged_segment的大小

### Inside the JVM Heap

* Elasticsearch的缓存主要分成三大类
  * Node Query Cache (Filter Context)
  * Shard Query Cache (Cache Query的结果)
  * Fielddata Cache

### Node Query Cache

* 每一个节点有一个Node Query缓存
  * 由该节点的所有Shard共享，只缓存Filter Context相关内容
  * Cache采用LRU算法
* 静态配置，需要设置在每个Data Node上
  * Node Level - indices.queries.cache.size:"10%"
  * Index Level: index.queries.cache.enabled: true


### Shard Request Cache

* 缓存每个分片.上的查询结果
  * 只会缓存设置了size=0的查询对应的结果。不会缓存hits。但是会缓存Aggregations和Suggestions
* Cache Key
  * LRU算法，将整个JSON查询串作为Key, 与JSON对象的顺序相关
* 静态配置
  * 数据节点: indices.requests.cache.size: “1%”

### FieldData Cache

* 除了Text类型，默认都采用doc_ _values。 节约了内存
  * Aggregation 的Global ordinals也保存在Fielddata cache中
* Text 类型的字段需要打开Fileddata才能对其进行聚合和排序
  * Text 经过分词，排序和聚合效果不佳，建议不要轻易使用
* 配置
  * 可以控制Indices.fielddata.cache.size,避免产生GC (默认无限制)

### 缓存失效

* Node Query Cache
  * 保存的是Segment级缓存命中的结果。Segment被合并后，缓存会失效
* Shard Request Cache
  * 分片Refresh时候，Shard Request Cache会失效。如果Shard对应的数据频繁发生变化，该缓存的效率会很差
* Fielddata Cache
  * Segment被合并后，会失效

### 管理内存的重要性

* Elasticsearch 高效运维依赖于内存的合理分配
  * 可用内存一半分配给JVM，一半留给操作系统，缓存索引文件
* 内存问题，引发的问题
  * 长时间GC，影响节点，导致集群响应缓慢
  * OOM， 导致丢节点
 
 
### 查看各个节点的内存状况

```
GET _cat/nodes?v

GET _nodes/stats/indices?pretty

GET _cat/nodes?v&h=name,queryCacheMemory,queryCacheEvictions,requestCacheMemory,requestCacheHitCount,request_cache.miss_count

GET _cat/nodes?h=name,port,segments.memory,segments.index_writer_memory,fielddata.memory_size,query_cache.memory_size,request_cache.memory_size&v


PUT /_cluster/settings
{
    "persistent" : {
       "indices.breaker.request.limit" : "90%"
    }
}

```

### 一些常见的内存问题

#### Segments 个数过多，导致full GC

* 现象: 集群整体响应缓慢，也没有特别多的数据读写。但是发现节点在持续进行Full GC

* 分析: 查看Elasticsearch的内存使用，发现segments.memory占用很大空间
* 解决:通过 force merge,把segments合并成一个。
* 建议:对于不在写入和更新的索引，可以将其设置成只读。同时，进行force merge操作。如果问题依然存在，则需要考虑扩容。此外，对索引进行force merge，还可以减少对global_ordinals 数据结构的构建，减少对fielddata cache的开销

* 分析:查看Elasticsearch的内存使用，发现fielddata.memory.size 占用很大空间。同时，数据不存在写入和更新，也执行过segments merge。
* 解决:将indices.fielddata.cache.size设小，重启节点，堆内存恢复正常
* 建议: Field data cache的构建比较重，Elasticsearch不会主动释放，所以这个值应该设置的保守一些。如果业务.上确实有所需要，可以通过增加节点，扩容解决


#### 复杂的嵌套聚合，导致集群full GC

* 现象:节点响应缓慢，持续进行Full GC
* 分析:导出Dump分析。发现内存中有大量bucket对象，查看日志，发现复杂的嵌套聚合
* 解决:优化聚合
* 建议:在大量数据集上进行嵌套聚合查询，需要很大的堆内存来完成。如果业务场景确实需要。则需要增加硬件进行扩展。同时，为了避免这类查询影响整个集群，需要设置Circuit Break和search.max.buckets的数值

#### Circuit Breaker

* 包含 多种断路器，避免不合理操作引发的0OM，每个断路器可以指定内存使用的限制
  * Parent circuit breaker: 设置所有的熔断器可以使用的内存的总量
  * Fielddata circuit breaker:加载fielddata所需要的内存
  * Request circuit breaker:防止每个请求级数据结构超过一定的内存(例如聚合计算的内存)
  * In flight circuit breaker: Request中的断路器
  * Accounting request circuit breaker:请求结束后不能释放的对象所占用的内存

####  Circuit Breaker统计信息

* GET /_nodes/stats/breaker?
  * Tripped大于0， 说明有过熔断
  * Limit size与estimated size约接近，越可能引发熔断
* 千万不要触发了熔断，就盲目调大参数，有可能会导致集群出问题，也不因该盲目调小，需要进行评估
* 建议将集群升级到7.x，更好的Circuit Breaker实现机制
  * 增加了indices.breaker.total.use_real_memory配置项，可以更加精准的分析内存状况，避免OOM

## 集群的生命周期管理

* 预上线
  * 评估用户的需求及使用场景/数据建模/容量规划/选择合适的部署架构/性能测试
* 上线
  * 监控流量/定期检查潜在问题(防患于未然，发现错误的使用方式，及时增加机器)
  * 对索引进行优化(Index Lifecycle Management) ，检测是否存在不均衡而导致有部分节点过热
  * 定期数据备份/滚动升级
* 下架前监控流量，实现Stage Decommission


### 部署的建议

* 根据实际场景，选择合适的部署方式，选择合理的硬件配置
  * 搜索类
  * 日志/指标
* 部署要考虑，反亲和性(Anti-Affinity)
  * 尽量将机器分散在不同的机架。例如，3台Master节点必须分散在不同的机架.上
  * 善用Shard Filtering进行配置

### 使用要遵循一定的规范

* Mapping
  * 生产环境中索引应考虑禁止Dynamic IndexMapping，避免过多字段导致Cluster State占用过多
  * 禁止索引自动创建的功能，创建时必须提供Mapping或通过Index Template进行设定

### 使用要遵循一定的规范

* 设置Slowlogs发现一些性能不好，甚至是错误的使用Pattern
  * 例如:错误的将网址映射成keyword, 然后用通配符查询。应该使用Text，结合URL分词器
  * 严禁一切“*”开头的通配符查询


### ES的版本

* Elasticsearch 的版本格式是: X.Y.Z
  * X: Major
  * Y: Minor
  * Z: Patch
* Elasticsearch 可以使用上一个主版本的索引
  * 7.x 可以使用6.x / 7.x不支持使用5.x
  * 5.x 可以使用2.x

### Rolling Upgrade V.S Full Cluster Restart

* Rolling Upgrade
  * 没有Downtime
* Full Cluster Restart
  * 集群在更新期间不可用
  * 升级更快

### Full Restart的步骤

* 停止索引数据，同时备份集群I
* Disable Shard Allocation (Persistent)
* 执行Synced Flush
* 关闭并更新所有节点
* 先运行所有Master 节点/再运行其他节点
* 等集群变黄后打开Shard Allocation


### 运维Cheat Sheet:移动分片

* 从一个节点移动分片到另外一个节点
* 使用场景:
  * 当一个数据节点上有过多Hot Shards; 可以通过手动分配分片到特定的节点解决

### 运维Cheat Sheet :从集群中移除一个节点

* 使用场景:当你想移除- -个节点，或者对一个机器进行维护。同时你又不希望导致集群的颜色变
  * 黄或者变红

### 运维Cheat Sheet :控制Allocation和Recovery

* 使用场景:控制Allocation和Recovery的速率

### 运维CheatSheet:清空节点上的缓存

* 使用场景:节点上出现了高内存占用。可以执行清除缓存的操作。这个操作会影响集群的性能,但是会避免你的集群出现OOM的问题

### 运维Cheat Sheet :控制搜索的队列

* 使用场景:当搜索的响应时间过长，看到有“reject” 指标的增加，都可以适当增加该数值

### 运维Cheat Sheet :设置Circuit Breaker

* 使用场景:设置各类Circuit Breaker。避免OOM的发生。

## 索引管理API

* Open/Close Index: 索引关闭后无法进行读写，但是索引数据不会被删除
* Shrink Index:可以将索引的主分片数收缩到较小的值
* Split Index:可以扩大主分片个数
* Rollover Index:类似Log4J记录日志的方式，索引尺寸或者时间超过一定值后，创建新的
* Rollup Index:对数据进行处理后，重新写入，减少数据量

### Shrink API

* ES 5.x后推出的一个新功能，使用场景
  * 索引保存的数据量比较小，需要重新设定主分片数
  * 索引从Hot移动到Warm后，需要降低主分片数
* 会使用和源索引相同的配置创建一个新的索引，仅仅降低主分片数
  * 源分片数必须是目标分片数的倍数。如果源分片数是素数，目标分片数只能为1
  * 如果文件系统支持硬链接，会将Segments硬连接到目标索引，所以性能好
* 完成后，可以删除源索引

* 分片必须只读
* 所有的分片必须在同一个节点上
* 集群健康状态为Green

### Split API

### Rollover API

* 当满足一系列的条件，Rollover API支持将一个Alias 指向一个新的索引
  * 存活的时间/最大文档数/最大的文件尺寸
* 应用场景
  * 当一个索引数据量过大
* 一般需要和Index Lifecycle Management Policies结合使用
  * 只有调用 Rollover API时，才会去做相应的检测。ES并不会自动去监控这些索引

### 时间序列的索引

* 特点
  * 索引中的数据随着时间，持续不断增长
* 按照时间序列划分索引的好处&挑战
  * 按照时间进行划分索引，会使得管理更加简单。例如，完整删除一个索引，性能比delete by query好
  * 如何进行自动化管理，减少人工操作
    * 从Hot移动到Warm
    * 定期关闭或者删除索引
    
### 索引生命周期常见的阶段

* Hot:索引还存在着大量的读写操作
* Warm:索引不存在写操作，还有被查询的需要
* Cold:数据不存在写操作，读操作也不多
* Delete:索引不再需要，可以被安全删除

### Elasticsearch Curator

* Elastic官方推出的工具
  * 基于python的命令行工具
* 配置Actions 
  * 内置10多种Index相关的操作
  * 每个动作可以顺序执行
* Filters
  * 支持各种条件，过滤出需要操作的索引

### eBay Lifecycle Management Tool

* eBay Pronto team自研图形化工具
  * 支持Curator的功能
  * 一个界面，管理多个ES集群
  * 支持不同的ES版本
* 支持图形化配置
* Job定时触发
  * 系统高可用

### Index Lifecycle Management

* Elasticsearch 6.6推出的新功能
  * 基于X-Pack Basic License, 可免费使用
* ILM概念
  * Policy 
  * Phase
  * Action


## Logstash入门及架构介绍

* ELT工具/数据搜集处理引擎。支持200多个插件

* 来源
  * 文件(日志/ Filebeats)
  * HTTP(Twitter)
  * 数据库
  * Kafka

* 下游
  * Analysis (MongoDB)
  * Elasticsearch
  * Archiving(HDFS & S3)
  * Alerting (Email/PageDuty)

### Logstash Concepts

* Pipeline
  * 包含了linput-filter-output三个阶段的处理流程
  * 插件生命周期管理
  * 队列管理
* Logstash Event
  * 数据在内部流转时的具体表现形式。数据在input阶段被转换为Event， 在output被转化成目标格式数据
  * Event其实是一个Java Object， 在配置文件中，对Event的属性进行增删改查


### Logstash架构简介

* Codec (Code / Decode) : 将原始数据decode成Event;将Event encode成目标数据

* Input 数据采集
  * Stdin
  * JDBC 
* Filter 数据解析
  * Mutate
  * Date 
  * User Agent
* Output 数据输出
  * Elasticsearch

### Input Plugins

* 一个Pipeline可以有多个input插件
  * Stdin / File
  * Beats / L og4J / Elasticsearch / JDBC / Kafka / Rabbitmq / Redis
  * JMX / HTTP / Websocket / UDP / TCP
  * Google Cloud Storage / S3
  * Github / Twitter

### Output Plugins

* 将Event发送到特定的目的地，是Pipeline的最后一个阶段
* [常见Output Plugins](https://www.elastic.co/guide/en/logstash/7.11/output-plugins.html)
  * Elasticsearch
  * Email / Pageduty
  * Influxdb / Kafka / Mongodb / Opentsdb / Zabbix
  * Http / TCP / Websocket

### Codec Plugins

* 将原始数据decode成Event;将Event encode成目标数据
* [内置的Codec Plugins](https://www.elastic.co/guide/en/logstash/7.11/codec-plugins.html)
  * Line / Multiline
  * JSON / Avro / Cef (ArcSight Common Event Format)
  * Dots / Rubydebug

### Filter Plugins

* 处理Event
* [内置的Filter Plugins](https://www.elastic.co/guide/en/logstash/7.11/filter-plugins.html)
  * Mutate 操作Event的字段
  * Metrics Aggregate metrics
  * Ruby 执行Ruby代码

Queue

### 多Pipelines

* Pipeline.works: Pipeline线程数，默认是CPU核数
* Pipeline.batch.size: Batcher一次批量获取等待处理的文档数，默认125。需结合jvm.options调节
* Pipeline.batch.delay: Batcher等待时间

### Logstash Queue

* In Memory Queue
  * 进程Crash， 机器当机，都会引起数据的丢失
* Persistent Queue
  * Queue.type.persisted (默认是memory)
  * Queue.max_bytes: 4gb
  * 机器当机，数据也不会丢失;数据保证会被消费;可以替代Kafka等消息队列缓冲区的作用
  * [地址](https://www.elastic.co/guide/en/logstash/7.11/persistent-queues.html)

### Codec Plugin  Multiline

* 设置参数
  *  Pattern: 设置行匹配的正则表达式
  * What :如果匹配成功，那么匹配行属于上一个事件还是下一个事件
    * Previous / Next
  * Negate true / false: 是否对pattern结果取反
    * True / False

### Input Plugin File

* 支持从文件中读取数据，如日志文件.
* 文件读取需要解决的问题
  * 只被读取一次。重启后需要从上次读取的位置继续(通过sincedb实现)
* 读取到文件新内容，发现新文件
* 文件发生归档操作(文档位置发生变化，日志rotation)，不能影响当前的内容读取

### Filter Plugin

* Filter Plugin可以对Logstash Event进行各种处理，例如解析，删除字段，类型转换
  * Date:日期解析
  * Dissect:分割符解析
  * Grok:正则匹配解析
  * Mutate:处理字段。重命名，删除，替换
  * Ruby:利用Ruby代码来动态修改Event

### Filter Plugin-Mutate

* 对字段做各种操作
  * Convert类型转换
  * Gsub字符串替换
  * Split/Join/Merge字符串切割，数组合并字符串，数组合并数组
  * Rename字段重命名
  * Update/Replace字段内容更新替换
  * Remove_field 字段删除

### 利用JDBC插件导入数据到Elasticsearch

JDBC Input Plugin &设计实现思路

* 支持通过JDBC Input Plugin将数
  * 据从数据库从读到Logstash
  * 需要自己提供所需的JDBC Driver
* Scheduling
  * 语法来自Rufus-scheduler
  * 扩展了Cron,支持时区
* State
  * Tracking_column / sql_last_value

## 什么是Beats


### 全品类采集器，搞定所有数据类型

* Filebeat 日志文件
* Metricbeat 指标
* Packetbeat 网络数据
* Winlogbeat 事件日志
* Auditbeat 审计数据
* Heartbeat 运行时间监控
* Functionbeat 无需服务器的采集器


* Light weight data shippers
  * 以搜集数据为主
  * 支持与Logstash或ES集成
* 全品类/轻量级/开箱即用/可插拔/可扩展/可视化

### Metricbeat简介

* 用来定期搜集操作系统，软件的指标数据
  * Metric VS Logs
  * Metric 可聚合的数据，定期搜集
  * Logs 文本数据，随机搜集
* 指标存储在Elasticsearch中，可以通过Kibana进行实时的数据分析

### Metricbeat组成

* Module
  * 搜集的指标对象， 例如不同的操作系统，不同的数据库，不同的应用系统
* Metricset
  * 一个Module可以有多个metricset
  * 具体的指标集合。以减少调用次数为原则进行划分
    * 不同的metricset可以设置不同的抓取时长

### Module

* Metricbeat提供了大量的开箱即用的Module
  * [Module](https://www.elastic.co/guide/en/beats/metricbeat/7.11/index.html)
* 通过执行 metricbeat module list 查看
* 通过 执行metricbeat moudle enable module_name 定制

### Packetbeat

* Packetbeat 实时网络数据分析，监控应用服务器之间的网络流量
  * 常见抓包工具 Tcpdump /wireshark
  * 常 见抓包配置 Pcap基于libpcap，跨平台/ Af_packet 仅支持Linux,基于内存映射嗅探，高性能
* Packetbeat 支持的协议
  * ICMP / DHCP / DNS / HTTP / Cassandra / Mysql / PostgresSQL / Redis / MongoDB /Memcache / TLS
* Network flows: 抓取记录网络流量数据，不涉及协议解析


### X-Pack Monitoring

* X-Pack提供了免费集群监控的功能
* 使用Elasticsearch 监控Elasticsearch
  * Xpack.monitoring collection.interval 默认设置10秒
* 在生产环境中，建议搭建dedicated集群用于ES集群的监控。有以下几个好处
  * 减少负载和数据
  * 当被监控集群出现问题，还能看到监控相关的数据

### 用APM进行程序性能监控

* Elastic全栈监控
  * Real User Monitoring
  * Application Level Monitoring
  * Server-Level Monitoring
  * Logging

* 核心应用指标
  * 请求响应时间
  * 未处理的错误及异常
  * 可视化调用关系
  * 发现性能瓶颈
  * 代码下钻

## 用机器学习实现时序数据的异常检测

### 异常检测所解决的问题

* 解决一些基于规则或者Dashboard难以实时发现的问题
* IT运维
  * 如何知道系统正常运行/如何调节阈值触发合适的报警/如何进行归因分析
* 信息安全
  * 哪些用户构成了内部威胁/系统是否感染了病毒
* 物联网/数据采集监控
  * 工厂和设备是否正常运营

* 什么是异常
  * 和自己比-个体的行为发生了急剧的变化
  * 和他人比-个体明显区别于其他的个体

### 相关术语

* Elastic 平台的机器学习功能I
  * Elastic的ML，主要针对时序数据的异常检测和预测
* 非监督机器学习
  * 不需要使用人工标签的数据来学习，仅仅依靠历史数据自动学习
* 贝叶斯统计
  * 一种概率计算方法，使用先验结果来计算现值或者预测未来的数值
* 异常检测
  * 异常代表的是不同的，但未必代表的是坏的/定义异常需要一些指导，从哪个方面去看

### 机器学习帮你自动挑选模型

* 使用成熟的机器学 习技术，挑选适合数据的正确的统计模型
* 更好的模型=更好的异常检测=更少的误报和漏报
* 出现在低概率区域，发现异常

## 用ELK进行日志管理

### 日志的重要性

* 为什么重要
  * 运维:医生给病人看病。日志就是病人对自己的陈述
  * 恶意攻击，恶意注册，刷单,恶意密码猜测
* 挑战
  * 关注点很多，任何一个点都有可能引起问题
  * 日志分散在很多机器，出了问题时，才发现日志被删了
  * 很多运维人员是消防员，哪里有问题去哪里

* 集中化日志管理
  * 日志搜集
  * 格式化分析
  * 检索与可视化
  * 风险告警


### Filebeat简介

*  A log data shipper for local files
* 读取日志文件，Filebeat不做数据的解析，加工处理
  * 日志是非结构化数据
  * 需要进行处理后，以结构化的方式保存到Elasticsearch
* 保证数据至少被读取一次
* 处理多行数据，解析JSON格式，简单的过滤

### Filebeat执行流程

* 定义数据采集: Prospector 配置。通过filebeat.yml
* 建立数据模型: Index Template
* 建立数据处理流程 : Ingest Pipeline
* 存储并提供可视化分析: ES + Kibana Dashboard


## 用Canvas做数据演示

### 实时展示数据，并且达到完美像素级要求

* 用更加酷炫的方式， 演绎你的数据
  * 基于ES实现准实时的数据分析
* 更好的想法，更大的屏幕
  * 品牌宣传，会议大屏
* 高度定制化
  * 调色板/ CSS /拖放元素
  
## 项目需求分析及架构设计

* 需求分析
  * IMDB: Movie DB
  * 搜索框，支持输入提示
  * 过滤器过滤结果， 支持排序
  * 搜索结果的相关性排序

### 后端UI

* 自定义同义词(Matrix = 黑客帝国 = 矩阵革命)
* 获取用户搜索统计数据
* 调整字段的相关性权重

### App Search后台管理 http://localhost:3002

* 功能概览
  * Analytics:获取用户搜索相关的统计数据
* 管理
  * 文档/Schema/API日志
* 搜索设定
  * 自定义同意词(Matrix = 黑客帝国 = 矩阵革命)
  * 调整字段的相关性权重

### 集群的备份与恢复

* 备份数据
* 备份集群的相关配置
* 备份集群安全配置


EFK(Elasticsearch+Filebeat+Kibana)收集容器日志