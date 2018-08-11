### 1、sql优化
1.业务拆分，相关字段冗余或者合并成临时表；
<br>2.分表查询，单表查询之后的结果进行字段整合；
<br>3.查询条件做索引（mysql数据库索引在内存里面）；
<br>4.数量大的表进行历史表分离（500w到1000w）；
<br>5.数据库主从分离，读写分离，mysql有自带的binlog实现 主从同步；
<br>6.explain分析sql语句，查看执行计划，分析索引是否用上，分析扫描行数等等。
### 2、PreparedStatement接口代表预编译的语句
它主要的优势在于可以减少SQL的编译错误并增加SQL的安全性（减少SQL注射攻击的可能性）、性能高。
### 3、 SQL标准定义了4类隔离级别
用来限定事务内外的哪些改变是可见的，哪些是不可见的。
<br>1.Read Uncommitted（读取未提交内容）,脏读（Dirty Read）.
<br>2.Read Committed（读取提交内容）不可重复读（Nonrepeatable Read），
因为同一事务的其他实例在该实例处理其间可能会有新的commit，所以同一select可能返回不同结果。
<br>3.Repeatable Read（可重读）,MySQL的默认事务隔离级别,
幻读 （Phantom Read）。简单的说，幻读指当用户读取某一范围的数据行时，
另一个事务又在该范围内插入了新行，当用户再读取该范围的数据行时，会发现有新的“幻影” 行。
InnoDB和Falcon存储引擎通过多版本并发控制（MVCC，Multiversion Concurrency Control）机制解决了该问题。
<br>4.Serializable（可串行化）,每个读的数据行上加上共享锁。在这个级别，可能导致大量的超时现象和锁竞争。
![四种隔离级别](https://github.com/gaoyuanyuan2/notes/blob/master/img/1.jpg) 