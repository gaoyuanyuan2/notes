## SQL
### 1、MySQL的索引
<br>1. 普通索引和唯- -索引
<br>普通索引是MySQL中的基本索引类型，允许在定义索引的列中插入重复值和空值。
<br>唯一索引，索引列的值必须唯- - "，但允许有空值。如果是组合索引，则列值的组合必须唯一。主键索引是一种特殊的唯一“索引，不允许有空值。
<br><br>2. 单列索引和组合索引
<br>单列索引即一个索引只包含单个列，一个表可以有多个单列索引。
<br>组合索引指在表的多个字段组合上创建的索引，只有在查询条件中使用了这些字段的左边字段时，索引才会被使用。使用组合索引时遵循最左前缀集合。
<br><br>3. 全文索引
<br>全文索引类型为FULLTEXT,在定义索引的列.上支持值的全文查找，允许在这些索引列中插入重复值和空值。全文索引可以在CHAR、VARCHAR或者TEXT类型的列上创建。MySQL中只有MyISAM存储引擎支持全文索引。
<br><br>4. 空间索引
<br>空间索引是对空间数据类型的字段建立的索引，MySQL中的空间数据类型有4种，分别是:GEOMETRY. POINT. LINESTRING 和POLYGON。MySQL使用SPATIAL关键字进行扩展，使得能够用于创建正规索引类似的语法创建空间索引。创建空间索引的列，必须将其声明为NOTNULL，空间索引只能在存储引擎为MyISAM的表中创建。
<br><br>5. mysql联合索引
<br>命名规则：表名_字段名
<br><br>1、需要加索引的字段，要在where条件中
<br><br>2、数据量少的字段不需要加索引
<br><br>3、如果where条件中是OR关系，加索引不起作用
<br><br>4、符合最左原则
<br>联合索引又叫复合索引。对于复合索引:Mysql从左到右的使用索引中的字段，一个查询可以只使用索引中的一部份，但只能是最左侧部分。例如索引是key index (a,b,c). 可以支持a | a,b| a,b,c 3种组合进行查找，但不支持 b,c进行查找 .当最左侧字段是常量引用时，索引就十分有效。
<br><br>6. Mysql索引会失效的几种情况分析
<br>索引并不是时时都会生效的，比如以下几种情况，将导致索引失效：
<br><br>1) 如果条件中有or，即使其中有条件带索引也不会使用(这也是为什么尽量少用or的原因)
<br>注意：要想使用or，又想让索引生效，只能将or条件中的每个列都加上索引
<br><br>2) 对于多列索引，不是使用的第一部分，则不会使用索引
<br><br>3) like查询是以%开头
<br><br>4) 如果列类型是字符串，那一定要在条件中将数据使用引号引用起来,否则不使用索引
<br><br>5) 如果mysql估计使用全表扫描要比使用索引快,则不使用索引
<br><br>此外，查看索引的使用情况
<br>show status like ‘Handler_read%';
<br><br>大家可以注意：
<br>handler_read_key:这个值越高越好，越高表示使用索引查询到的次数
<br>handler_read_rnd_next:这个值越高，说明查询低效
### 2、锁
<br>1. 悲观锁
<br><br>1) 排它锁，当事务在操作数据时把这部分数据进行锁定,直到操作完毕后再解锁,其他事务操作才可操作该部分数据。这将防止其他进程读取或修改表中的数据。
<br><br>2) 实现:大多数情况下依靠数据库的锁机制实现
<br>一般使用 select ..for update对所选择的数据进行加锁处理,例如select * from account where name="Max" for update。这条sql 语句锁定了account表中所有符合检索条件( name="Max" )的记录。本次事务提交之前(事务提交时会释放事务过程中的锁) ,外界无法修改这些记录。
<br><br>2. 乐观锁
<br>1) 如果有人在你之前更新了,你的更新应当是被拒绝的,可以让用户重新操作。
<br>2) 实现:大多数基于数据版本( Version )记录机制实现
<br>3) 具体可通过给表加一个版本号或时间戳字段实现,当读取数据时，将version字段的值一同读出，数据每更新次，对此version
值加。当我们提交更新的时候，判断当前版本信息与第一次取出来的版本值大小，如果数据库表当前版本号与第一次取出来的version值相等 ，则予以更新，否则认为是过期数据，拒绝更新，让用户重新操作。


