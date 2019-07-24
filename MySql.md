# MySql

## SQL优化

1.业务拆分，相关字段冗余或者合并成临时表；

2.分表查询，单表查询之后的结果进行字段整合；

3.查询条件做索引（mysql数据库索引在内存里面）；

4.数量大的表进行历史表分离（500w到1000w）；

5.数据库主从分离，读写分离，mysql有自带的binlog实现 主从同步；

6.explain分析sql语句，查看执行计划，分析索引是否用上，分析扫描行数等等。

7.大量更新不能建索引

8.增加冗余字段

设计数据表时应尽量遵循范式理论的规约，尽可能的减少冗余字段，让数据库设计看起来精致、优雅。但是，合理的加入冗余字段可以提高查询速度。
  
表的规范化程度越高，表和表之间的关系越多，需要连接查询的情况也就越多，性能也就越差。

*冗余字段的值在一个表中修改了，就要想办法在其他表中更新，否则就会导致数据不一致的问题。*

## PreparedStatement接口代表预编译的语句

它主要的优势在于可以减少SQL的编译错误并增加SQL的安全性（减少SQL注射攻击的可能性）、性能高。

## SQL标准定义了4类隔离级别

用来限定事务内外的哪些改变是可见的，哪些是不可见的。

1.Read Uncommitted（读取未提交内容）,脏读（Dirty Read）.

  脏读又称无效数据的读出，是指在数据库访问中，事务T1将某一值修改，然后事务T2读取该值，此后T1因为某种原因撤销对该值的修改，这就导致了T2所读取到的数据是无效的。

2.Read Committed（读取提交内容）不可重复读（Nonrepeatable Read），因为同一事务的其他实例在该实例处理其间可能会有新的commit，所以同一select可能返回不同结果。

3.Repeatable Read（可重读）,MySQL的默认事务隔离级别,幻读 （Phantom Read）。简单的说，幻读指当用户读取某一范围的数据行时，另一个事务又在该范围内插入了新行，当用户再读取该范围的数据行时，会发现有新的“幻影” 行。

InnoDB和Falcon存储引擎通过多版本并发控制（MVCC，Multiversion Concurrency Control）机制解决了该问题。

4.Serializable（可串行化）,每个读的数据行上加上共享锁。在这个级别，可能导致大量的超时现象和锁竞争。

![四种隔离级别](https://github.com/gaoyuanyuan2/notes/blob/master/img/1.jpg) 

## CHAR

固定长度，所以速度比VARCHAR（长度可变，比较节省空间，所以对磁盘I/O和数据存储总量比较好）速度要快，但是它的缺点就是浪费存储空间。

## EXISTS

关键字后面的参数是一个任意的子查询，判断是否返回行，如果至少返回一行，那么EXISTS的结果为true，如果没有任何行，此时外层语句将不进行查询。

### 数据库存储引擎

数据库底层软件组件，DBMS使用数据引擎进行创建、更新、删除数据操作。MySQL的核心就是存储引擎。包括处理安全事务安全表引擎和处理非事务安全表的引擎。MySQL5.5支持的存储引擎有：

InnoDB：支持事务安全表（ACID）,支持行锁定和外键。

MyISAM：较高的插入查询速度，但不支持事务。

Memory：将表中的数据存储到内存中，为查询和引用其他表数据提供快速访问。,Merge,Archive,Federated,CSV,BLACKHOLE等

MySQL不同版本中默认存储引擎不同，MySQL允许修改默认存储引擎，方法是修改配置文件。

### 索引

没有索引必须遍历整个表，索引是在存储引擎中实现的,索引的本质：索引是数据结构。

[原理](https://blog.csdn.net/debug_zhang/article/details/52168552)

LIKE 关键字匹配字符串以“%”开头，索引不会起作用。OR查询，一个字段没有使用索引，那么其他的索引也不会起作用。（注意：要想使用or，又想让索引生效，只能将or条件中的每个列都加上索引）

尽量使用短索引，短索引不仅可以提高查询速度而且可以节省磁盘空间、减少I/O操作。

如果列类型是字符串，那一定要在条件中将数据使用引号引用起来,否则不使用索引。

(1)索引并非越多越好，一个表中如有大量的索引,不仅占用磁盘空间，而且会影响INSERT、DEL ETE. UPDATE等语句的性能，因为当表中的数据更改的同时，索引也会进行调整和更新。

(2)避免对经常更新的表进行过多的索引，并且索引中的列尽可能少。而对经常用于查询的字段应该创建索引，但要避免添加不必要的字段。

(3)数据量小的表最好不要使用索引，由于数据较少，查询花费的时向可能比遍历索引的时间还要短，索引可能不会产生优化效果。

(4)在条件表达式中经常用到的不同值较多的列上建立索引，在不同值少的列上不要建立索引。比如在学生表的“性别”字段上只有“男”与“女”两个不同值，因此就无须建立索引。如果建立索引不但不会提高查询效率，反而会严重降低更新速度。

(5)当唯一性是某种数据本身的特征时，指定唯一霸引。使用唯一索引需能确保定义的列的数据完整性，以提高查询速度。

(6)在频繁进行排序或分组(即进行group by或order by操作)的列上建立索引，如果待排序的列有多个，可以在这些列上建立组合索引。
  

MySQL的索引可以分为以下几类:

1.普通索引和唯一索引

普通索引是MySQL中的基本索引类型，允许在定义索引的列中插入重复值和空值。

唯一索引，索引列的值必须唯一 ，但允许有空值。如果是组合索引，则列值的组合必须唯一。主键索引是一种特殊的唯一索引，不允许有空值。

2.单列索引和组合索引

单列索引即一个索引只包含单个列，一个表可以有多个单列索引。

组合索引指在表的多个字段组合，上创建的索引，只有在查询条件中使用了这些字段的`左边`字段时，索引才会被使用。使用组合索引时遵循最左前缀集合。

3.全文索引

用 like + % 就可以实现模糊匹配了，为什么还要全文索引？like + % 在文本比较少时是合适的，但是对于大量的文本数据检索，是不可想象的。全文索引在大量的数据面前，能比 like + % 快 N 倍，速度不是一个数量级，但是全文索引可能存在精度问题。

全文索引类型为FULLTEXT,在定义索引的列上支持值的全文查找，允许在这些索引列中插入重复值和空值。全文索引可以在CHAR、VARCHAR或者TEXT类型的列上创建。

MySQL 5.6 以前的版本，只有 MyISAM 存储引擎支持全文索引；MySQL 5.6 及以后的版本，MyISAM 和 InnoDB 存储引擎均支持全文索引。

4.空间索引

空间索引是对空间数据类型的字段建立的索引，MySQL中的空间数据类型有4种，分别是:GEOMETRY. POINT、LINESTRING 和POLYGON。MySQL使用SPATIAL关键字进行扩展，使得能够用于创建正规索引类似的语法创建空间索引。创建空间索引的列，必须将其声明为NOTNULL，空间索引只能在存储引擎为My1SAM的表中创建。

5.mysql联合索引

命名规则：表名_字段名

1、需要加索引的字段，要在where条件中

2、数据量少的字段不需要加索引

3、如果where条件中是OR关系，加索引不起作用

4、符合最左原则

联合索引又叫复合索引。对于复合索引:Mysql从左到右的使用索引中的字段，一个查询可以只使用索引中的一部份，但只能是最左侧部分。例如索引是key index (a,b,c). 可以支持a | a,b| a,b,c 3种组合进行查找，但不支持 b,c进行查找 .当最左侧字段是常量引用时，索引就十分有效。

![EXPLAIN](https://github.com/gaoyuanyuan2/notes/blob/master/img/40.png) 

## 索引创建规则

1.最左前缀匹配原则，非常重要的原则，mysql会一直向右匹配直到遇到范围查询(>、<、between、like)就停止匹配，比如a = 1 and b = 2 and c > 3 and d = 4 如果建立(a,b,c,d)

2.顺序的索引，d是用不到索引的，如果建立(a,b,d,c)的索引则都可以用到，a,b,d的顺序可以任意调整。

3.=和in可以乱序，比如a = 1 and b = 2 and c = 3 建立(a,b,c)索引可以任意顺序，mysql的查询优化器会帮你优化成索引可以识别的形式

4.尽量选择区分度高的列作为索引,区分度的公式是count(distinct col)/count(*)，表示字段不重复的比例，比例越大我们扫描的记录数越少，唯一键的区分度是1，而一些状态、性别字段可能在大数据面前区分度就是0，
那可能有人会问，这个比例有什么经验值吗？使用场景不同，这个值也很难确定，一般需要join的字段我们都要求是0.1以上，即平均1条扫描10条记录

5.索引列不能参与计算，保持列“干净”，比如from_unixtime(create_time) = ’2014-05-29’就不能使用到索引，原因很简单，b+树中存的都是数据表中的字段值，但进行检索时，
需要把所有元素都应用函数才能比较，显然成本太大。所以语句应该写成create_time = unix_timestamp(’2014-05-29’);尽量的扩展索引，不要新建索引。比如表中已经有a的索引，现在要加(a,b)的索引，那么只需要修改原来的索引即可

此外，查看索引的使用情况

show status like ‘Handler_read%';

注意：

handler_read_key:这个值越高越好，越高表示使用索引查询到的次数

handler_read_rnd_next:这个值越高，说明查询低效

## 锁

1.悲观锁

排它锁，当事务在操作数据时把这部分数据进行锁定,直到操作完毕后再解锁,其他事务操作才可操作该部分数据。这将防止其他进程读取或修改表中的数据。

实现:大多数情况下依靠数据库的锁机制实现

一般使用 select ..for update对所选择的数据进行加锁处理,例如select * from account where name="Max" for update。这条sql 语句锁定了account表中所有符合检索条件( name="Max" )的记录。
本次事务提交之前(事务提交时会释放事务过程中的锁) ,外界无法修改这些记录。

2.乐观锁

如果有人在你之前更新了,你的更新应当是被拒绝的,可以让用户重新操作。

实现:大多数基于数据版本( Version )记录机制实现
 
具体可通过给表加一个版本号或时间戳字段实现,当读取数据时，将version字段的值一同读出，数据每更新次，对此version值加。
当我们提交更新的时候，判断当前版本信息与第一次取出来的版本值大小，如果数据库表当前版本号与第一次取出来的version值相等 ，则予以更新，否则认为是过期数据，拒绝更新，让用户重新操作。


## 数据库性能参数

我们可以通过SHOW STATUS语句查看MySQL数据库的性能参数

Slow_queries  慢查询次数：

什么是慢查询？  mysql读写分离的时候的日志，里面记录了执行某条sql语句超过某个时间后的记录，方便我们做一个后期的优化，我们可以通过Slow_queries显示慢查询
查看你的mysql数据库是否有慢查询：SHOW STATUS LIKE 'Slow_queries'

Com_(CRUD) 操作的次数

`SHOW STATUS LIKE 'Com_select'`

## 查询优化 EXPLAIN

![EXPLAIN](https://github.com/gaoyuanyuan2/notes/blob/master/img/33.png) 

### 1.id

SELECT识别符。这是SELECT查询序列号。

### 2.select_type

表示查询中每个select子句的类型（简单 OR复杂）。

有以下几种值：

1、SIMPLE

查询中不包含子查询或者UNION

2、PRIMARY

查询中若包含任何复杂的子部分，最外层查询则被标记为：PRIMARY。

![PRIMARY](https://github.com/gaoyuanyuan2/notes/blob/master/img/34.png) 

3、UNION

表示连接查询的第2个或后面的查询语句。

![PRIMARY](https://github.com/gaoyuanyuan2/notes/blob/master/img/35.png) 

4、DEPENDENT UNION

UNION中的第二个或后面的SELECT语句，取决于外面的查询。

5、UNION RESULT

连接查询的结果。

6、SUBQUERY

子查询中的第1个SELECT语句。

![PRIMARY](https://github.com/gaoyuanyuan2/notes/blob/master/img/36.png) 

7、DEPENDENT SUBQUERY

子查询中的第1个SELECT语句，取决于外面的查询。

8、DERIVED

SELECT(FROM 子句的子查询)。

### 3.table

表示查询的表。

### 4.type（重要）

表示表的连接类型。

以下的连接类型的顺序是从最佳类型到最差类型：

1、system

表仅有一行，这是const类型的特列，平时不会出现，这个也可以忽略不计。

2、const

数据表最多只有一个匹配行，因为只匹配一行数据，所以很快，常用于PRIMARY KEY或者UNIQUE索引的查询，可理解为const是最优化的。

3、eq_ref
mysql手册是这样说的:"对于每个来自于前面的表的行组合，从该表中读取一行。这可能是最好的联接类型，除了const类型。它用在一个索引的所有部分被联接使用并且索引是UNIQUE或PRIMARY KEY"。eq_ref可以用于使用=比较带索引的列。

![PRIMARY](https://github.com/gaoyuanyuan2/notes/blob/master/img/37.png) 


4、ref
查询条件索引既不是UNIQUE也不是PRIMARY KEY的情况。ref可用于=或<或>操作符的带索引的列。

5、ref_or_null

该联接类型如同ref，但是添加了MySQL可以专门搜索包含NULL值的行。在解决子查询中经常使用该联接类型的优化。

上面这五种情况都是很理想的索引使用情况。

6、index_merge

该联接类型表示使用了索引合并优化方法。在这种情况下，key列包含了使用的索引的清单，key_len包含了使用的索引的最长的关键元素。

7、unique_subquery

该类型替换了下面形式的IN子查询的ref: value IN (SELECT primary_key FROM single_table WHERE some_expr) 

unique_subquery是一个索引查找函数,可以完全替换子查询,效率更高。

8、index_subquery

该联接类型类似于unique_subquery。可以替换IN子查询,但只适合下列形式的子查询中的非唯一索引: value IN (SELECT key_column FROM single_table WHERE some_expr)

9、range

只检索给定范围的行,使用一个索引来选择行。

![PRIMARY](https://github.com/gaoyuanyuan2/notes/blob/master/img/38.png) 

10、index

该联接类型与ALL相同,除了只有索引树被扫描。这通常比ALL快,因为索引文件通常比数据文件小。

11、ALL

对于每个来自于先前的表的行组合,进行完整的表扫描。（性能最差）

### 5.possible_keys

指出MySQL能使用哪个索引在该表中找到行。

如果该列为NULL，说明没有使用索引，可以对该列创建索引来提高性能。

### 6.key

显示MySQL实际决定使用的键(索引)。如果没有选择索引,键是NULL。

可以强制使用索引或者忽略索引：

       强制使用索引：USE INDEX(列名)
       
       忽略使用索引：IGNORE INDEX(列名)
 
![PRIMARY](https://github.com/gaoyuanyuan2/notes/blob/master/img/39.png) 

### 7.key_len

显示MySQL决定使用的键长度。如果键是NULL,则长度为NULL。

注意：key_len是确定了MySQL将实际使用的索引长度。

### 8.ref

显示使用哪个列或常数与key一起从表中选择行。

### 9.rows

显示MySQL认为它执行查询时必须检查的行数。

### 10.4.2.10.Extra

该列包含MySQL解决查询的详细信息

Distinct:MySQL发现第1个匹配行后,停止为当前的行组合搜索更多的行。

Not exists:MySQL能够对查询进行LEFT JOIN优化,发现1个匹配LEFT JOIN标准的行后,不再为前面的的行组合在该表内检查更多的行。

range checked for each record (index map: #):MySQL没有发现好的可以使用的索引,但发现如果来自前面的表的列值已知,可能部分索引可以使用。

Using filesort:MySQL需要额外的一次传递,以找出如何按排序顺序检索行。

Using index:从只使用索引树中的信息而不需要进一步搜索读取实际的行来检索表中的列信息。

Using temporary:为了解决查询,MySQL需要创建一个临时表来容纳结果。

Using where:WHERE 子句用于限制哪一个行匹配下一个表或发送到客户。

Using sort_union(...), Using union(...), Using intersect(...):这些函数说明如何为index_merge联接类型合并索引扫描。

Using index for group-by:类似于访问表的Using index方式,Using index for group-by表示MySQL发现了一个索引,可以用来查 询GROUP BY或DISTINCT查询的所有列,而不要额外搜索硬盘访问实际的表。

## 子查询优化

执行子查询时，MYSQL需要创建临时表，查询完毕后再删除这些临时表，所以，子查询的速度会受到一定的影响。这多了一个创建临时表和销毁表的过程。

优化方式：

可以使用连接查询（JOIN）代替子查询，连接查询时不需要建立临时表，其速度比子查询快。

## 插入数据的优化

插入数据时，影响插入速度的主要是索引、唯一性校验、一次插入的数据条数等。

为什么索引会影响插入速度呢？

索引越多，当你写入数据的时候就会越慢，因为我们在插入数据的时候不只是把数据写入文件，而且还要把这个数据写到索引中，索引索引越多插入越慢

那么插入数据的优化，根据不同的存储引擎优化手段不一样，在MySQL中常用的存储引擎有，MyISAM和InnoDB，[两者的区别](https://www.cnblogs.com/panfeng412/archive/2011/08/16/2140364.html)

## MyISAM

1.禁用索引

对于非空表，插入记录时，MySQL会根据表的索引对插入的记录建立索引。如果插入大量数据，建立索引会降低插入数据速度。

为了解决这个问题，可以在批量插入数据之前禁用索引，数据插入完成后再开启索引。

禁用索引的语句：

ALTER TABLE table_name DISABLE KEYS

开启索引语句：

ALTER TABLE table_name ENABLE KEYS

对于空表批量插入数据，则不需要进行操作，因为MyISAM引擎的表是在导入数据后才建立索引。

2.禁用唯一性检查

唯一性校验会降低插入记录的速度，可以在插入记录之前禁用唯一性检查，插入数据完成后再开启。

禁用唯一性检查的语句：SET UNIQUE_CHECKS = 0;

开启唯一性检查的语句：SET UNIQUE_CHECKS = 1;

3.批量插入数据

插入数据时，可以使用一条INSERT语句插入一条数据，也可以插入多条数据。

4.使用LOAD DATA INFILE

当需要批量导入数据时，使用LOAD DATA INFILE语句比INSERT语句插入速度快很多。


## 服务器优化

1.优化服务器硬件

服务器的硬件性能直接决定着MySQL数据库的性能，硬件的性能瓶颈，直接决定MySQL数据库的运行速度和效率。

需要从以下几个方面考虑：

1、配置较大的内存。足够大的内存，是提高MySQL数据库性能的方法之一。内存的IO比硬盘快的多，可以增加系统的缓冲区容量，使数据在内存停留的时间更长，以减少磁盘的IO。

2、配置高速磁盘，比如SSD。

3、合理分配磁盘IO，把磁盘IO分散到多个设备上，以减少资源的竞争，提高并行操作能力。

4、配置多核处理器，MySQL是多线程的数据库，多处理器可以提高同时执行多个线程的能力。

2.优化MySQL的参数

通过优化MySQL的参数可以提高资源利用率，从而达到提高MySQL服务器性能的目的。

MySQL的配置参数都在my.conf或者my.ini文件的[mysqld]组中，常用的参数如下：

![参数](https://github.com/gaoyuanyuan2/notes/blob/master/img/41.png) 

## 慢查询日志查看：

`show variables like '%quer%';`

其中红框标注的选项是：

-slow_query_log是否记录慢查询。用long_query_time变量的值来确定“慢查询”。

-slow_query_log_file慢日志文件路径

-long_query_time慢日志执行时长（秒），超过设定的时间才会记日志


查看索引参数使用情况 ：SHOW STATUS LIKE 'Handler_read%'

如果索引正在工作，Handler_read_key的值将很高，这个值代表一行被索引读到的次数

Handler_read_rnd_next的值高则意味着查询运行效率低，并且应该建立索引补救

![参数](https://github.com/gaoyuanyuan2/notes/blob/master/img/42.png) 

这里就要结合咱们的慢查询 和DSC去建立索引

## 索引的存储分类

MyISAM存储引擎的表的数据和索引是自动分开存储的，各自是一个独一的一个文件;

InnoDB存储引擎的表的数据和索引是存储在同一个表空间里面的，但可以有多个文件组成。

MySQl目前不支持函数索引，但是能对列的面前某一部分进行索引，这个特性可以大大的缩小索引文件的大小，用户在设计表结构的时候也可以对文本列根据此特性经行灵活设计。

create index ind_company_name on company(name(4))


